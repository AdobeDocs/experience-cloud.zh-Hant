---
title: 功能群組管理API
description: 體驗轉出功能群組管理API的API參考資料，包括取得、建立、更新、刪除和控制功能群組轉出計畫的端點。
source-git-commit: db719ba7b9db91aea818d8ef216a28fcedc6aa65
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 14%

---


# 功能群組管理API {#feature-group-management-api}

功能群組管理API可讓您以程式設計方式建立、讀取、更新和刪除體驗轉出中的功能群組，包括自動化和A/B測試轉出計畫。

**基底路徑：** `/m/api/v1/mgmt/group`

所有要求都需要[一般需求](feature-management-apis-overview.md#common-requirements)中說明的標頭。

## 取得所有功能群組 {#get-all-groups}

擷取貴組織的所有功能群組。

| | |
|---|---|
| **端點** | `GET /m/api/v1/mgmt/group` |
| **方法** | GET |

### 查詢參數 {#get-all-query-params}

| 參數 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `myOrg` | 布林值 | 設定為`true`以包含組織資訊。 | 是 |
| `includeClientInfo` | 布林值 | 設定為`true`以包含每個群組的應用程式資訊。 | 是 |

### 回應 {#get-all-response}

| 狀態 | 說明 |
|---|---|
| `200` | 成功。 回應內文是功能群組物件的陣列。 |

## 依ID取得功能群組 {#get-group-by-id}

依數值ID擷取單一特徵群組。

| | |
|---|---|
| **端點** | `GET /m/api/v1/mgmt/group/{groupId}` |
| **方法** | GET |
| **查詢引數** | `includeAnalyzeInfo=true` （選擇性 — 將分析資料新增至回應） |

### 回應 {#get-by-id-response}

| 狀態 | 說明 |
|---|---|
| `200` | 成功。 回應主體是功能群組物件。 |
| `400` | 無效的功能群組識別碼。 |

## 建立功能群組 {#create-group}

使用手動、自動化或A/B測試轉出型別建立新功能群組。

| | |
|---|---|
| **端點** | `POST /m/api/v1/mgmt/group` |
| **方法** | POST |

### 要求內文 {#create-request-body}

要求內文使用[功能群組物件](#feature-group-object)。 `params`內的`rolloutType`是必要的，並決定承載的結構。

**範例 — 手動轉出：**

```json
{
  "params": {
    "rolloutType": "manual",
    "label": "my-feature-group",
    "tags": [],
    "canContextOverridePUP": false
  },
  "status": "SAVED",
  "type": "group",
  "name": "my.feature.group",
  "description": "A manual feature group",
  "variations": [{ "variantPercentage": 100, "variantName": "Variant 1", "features": [] }],
  "audience": [{ "criteria": { "and": [{ "operator": "EQ", "attr": "COUNTRY", "val": "US", "ruleId": 1, "category": "default" }] } }],
  "clients": [],
  "org": { "id": 95 }
}
```

### 回應 {#create-response}

| 狀態 | 說明 |
|---|---|
| `200` | 成功。 回應主體是已建立的功能群組物件。 |
| `400` | 無效的承載 — 請參閱[錯誤訊息](#error-messages)以取得詳細資料。 |
| `403` | 許可權不足。 |

## 更新功能群組 {#update-group}

更新現有的功能群組。 傳遞與建立要求內文相同的結構，包括`id`欄位。

| | |
|---|---|
| **端點** | `PUT /m/api/v1/mgmt/group` |
| **方法** | PUT |

### 回應 {#update-response}

| 狀態 | 說明 |
|---|---|
| `200` | 成功。 回應內文是更新的功能群組物件。 |
| `400` | 無效的承載。 |
| `403` | 許可權不足。 |

## 刪除功能群組 {#delete-group}

依數值識別碼刪除功能群組。

| | |
|---|---|
| **端點** | `DELETE /m/api/v1/mgmt/group/{groupId}` |
| **方法** | DELETE |

### 回應 {#delete-response}

| 狀態 | 說明 |
|---|---|
| `204` | 成功。 無回應內文。 |
| `403` | 許可權不足。 |

## 功能群組物件參考 {#feature-group-object}

| 欄位 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `id` | 整數 | 功能群組識別碼。 只有更新呼叫才需要。 | 條件式 |
| `name` | 字串 | 功能群組金鑰。 最多50個字元。 模式： `^[a-zA-Z0-9_.-]*$` | 是（建立） |
| `clients` | 陣列 | 與群組關聯的應用程式。 每個專案都必須包含`id`和`imsClientId`。 | 是 |
| `status` | 字串 | `"SAVED"`或 `"PUBLISHED"` | 是 |
| `type` | 字串 | 功能群組一律為`"group"`。 | 是 |
| `org` | 物件 | 組織詳細資料。 必須包含`id`。 | 是 |
| `params` | 物件 | 群組引數。`rolloutType` 是必要的（`"manual"`、`"automated"`或`"ab-testing"`）。 也支援`label`和`tags`。 | 是 |
| `audience` | 陣列 | 手動轉出型別的對象規則。 | 無 |
| `variations` | 陣列 | 變體清單。 請參閱[FeatureGroupVariation物件](#featuregroupvariation-object)。 | 無 |
| `phaseRollOutPlan` | 物件 | 階段轉出計畫。 自動化和A/B測試型別需要。 請參閱[PhaseRollOutPlan物件](#phaserolloutplan-object)。 | 條件式 |
| `description` | 字串 | 選用的顯示說明。 最多225個字元。 | 無 |

### FeatureGroupVariation物件 {#featuregroupvariation-object}

| 欄位 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `id` | 整數 | 變數ID。 只有更新呼叫才需要。 | 條件式 |
| `variantName` | 字串 | 變體名稱。 硬式編碼為`"Variant 1"`。 | 是 |
| `variantPercentage` | 小數 | 接收此變體的對象百分比。 必須大於0且不得大於100。 | 是 |

### PhaseRollOutPlan物件 {#phaserolloutplan-object}

| 欄位 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `phaseRollOutBlocks` | 陣列 | 階段區塊和等待區塊的有序清單。 最後一個區塊必須是階段區塊。 | 是 |
| `rollOutPlanState` | 字串 | `"DRAFT"`、`"RUNNING"`、`"PAUSED"`或`"ABORTED"` | 是 |

`phaseRollOutBlocks`中的每個區塊都是包含具有對象條件之`phaseRule`的&#x200B;**階段區塊** (`isPhaseBlock: true`)，或是包含具有`waitDuration` （相對）或`executionDate` （固定時間戳記） `waitRule`的&#x200B;**等待區塊** (`isPhaseBlock: false`)。

## 錯誤訊息 {#error-messages}

| 條件 | 狀態 | 錯誤訊息 |
|---|---|---|
| 無效或空白的名稱 | 400 | `Error: Invalid value for release name.` |
| 空白的對象條件 | 400 | `Error: Release is not valid` |
| 自動化型別的多個變數 | 400 | `Error: Feature variation is not valid. Variation name should be unique across variations` |
| 無使用者端的已發佈群組 | 400 | `Error: At least one client must be associated with enabled feature group.` |
| 計畫中的最後一個區塊不是階段區塊 | 400 | `Error: The last block in the Phase Rollout plan should be phase block` |
| 等候區塊計時順序錯誤 | 400 | `Error: Wait block timings are not in order in the phase rollout plan` |
| 不一致的等待區塊型別 | 400 | `Error: Wait block should be of same type.` |
| 編輯已啟動的階段區塊 | 400 | `Error: Activated phase block should not be changed` |
| 空轉出型別 | 400 | `Error: Rollout type cannot be empty while feature group creation` |
| 以手動型別傳遞的階段計畫 | 400 | `Error: PhaseRollOutPlan can't be added with manual rollout type while feature group creation` |
| 排程通過，狀態為「已發佈」 | 400 | `Error: Schedule can't be added in published state while release/group creation` |

## 另請參閱 {#see-also}

* [功能管理API概述](feature-management-apis-overview.md)
* [功能標幟管理API](feature-flags-management-api.md)
* [管理修補程式API](management-patch-api.md)
