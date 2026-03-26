---
title: 發行管理API
description: Experience Rollouts發行管理API的API參考資料，包括取得、建立及編輯發行和跨團隊功能群組的端點。
exl-id: e8d1d025-0645-4cf2-921f-d94c9f71282d
source-git-commit: 454b5c719a5f8be82d1ed835da58bfca6316def2
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 13%

---

# 發行管理API {#release-management-apis}

發行管理API可讓您以程式設計方式擷取、建立和編輯發行版本和跨團隊功能群組(CTFG)。 這些API使用v2管理端點。

**基底路徑：** `/m/api/v2/mgmt/release`

所有要求都需要[一般需求](feature-management-apis-overview.md#common-requirements)中說明的標頭，加上下列其他標頭。

## 其他必要的標頭 {#additional-header}

| 標頭 | 說明 | 必要 |
|---|---|---|
| `x-user-context-org` | 貴組織的數值團隊ID。 您可以在團隊設定底下的「體驗轉出」主控台中找到此值。 | 是 |

## 依ID取得版本 {#get-release}

依數值ID擷取單一版本或跨團隊功能群組。

| | |
|---|---|
| **端點** | `GET /m/api/v2/mgmt/release/{id}` |
| **方法** | GET |

### 查詢參數 {#get-query-params}

| 參數 | 類型 | 說明 | 預設 |
|---|---|---|---|
| `includePermissions` | 布林值 | 包含更新或刪除此版本的許可權。 | `true` |
| `includeOrg` | 布林值 | 包含此版本的組織資訊。 | `true` |
| `includeAnalyzeInfo` | 布林值 | 包含Analytics資訊。 | `false` |

### 回應 {#get-response}

| 狀態 | 說明 |
|---|---|
| `200` | 成功。 回應本文是發行物件 — 請參閱[發行物件參考](#release-object)。 |
| `400` | 無效的發行ID或格式錯誤的請求。 |

## 建立版本 {#create-release}

建立新版本或跨團隊功能群組。

| | |
|---|---|
| **端點** | `POST /m/api/v2/mgmt/release` |
| **方法** | POST |

### 要求內文 {#create-request-body}

要求內文使用[發行物件](#release-object)。 若要建立，跨團隊功能群組（`CROSS_TEAM_FEATURE_GROUP`型別）的`status`必須設定為`"SAVED"`，或標準版本（`RELEASE`型別）的`"DRAFT"`。

**範例 — 建立跨團隊功能群組：**

```json
{
  "params": {
    "rolloutType": "manual",
    "cohortingType": "guid",
    "tags": [],
    "canContextOverridePUP": false,
    "label": "my-cross-team-group"
  },
  "status": "SAVED",
  "type": "CROSS_TEAM_FEATURE_GROUP",
  "name": "my-cross-team-group",
  "description": null,
  "meta": "",
  "variations": [{ "variantPercentage": 100, "variantName": "Variant 1", "features": [] }],
  "audience": [{}],
  "clients": [],
  "pollInterval": 300,
  "org": { "id": "95" },
  "comment": ""
}
```

### 回應 {#create-response}

| 狀態 | 說明 |
|---|---|
| `200` | 成功。 回應內文是已建立的發行物件。 |
| `400` | 無效的承載。 |

## 編輯版本 {#edit-release}

更新現有的版本或跨團隊功能群組。 傳遞包含`id`欄位的完整發行物件。

| | |
|---|---|
| **端點** | `PUT /m/api/v2/mgmt/release/{id}` |
| **方法** | PUT |

### 回應 {#edit-response}

| 狀態 | 說明 |
|---|---|
| `200` | 成功。 回應內文是更新的發行物件。 |
| `417` | 並行更新衝突。 此版本已在GET和PUT呼叫之間修改。 擷取最新版本並重試。 |

## 發行物件參考 {#release-object}

| 欄位 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `id` | 整數 | 版本ID。 只有更新呼叫才需要。 | 條件式 |
| `name` | 字串 | 發行版本名稱。 最多50個字元。 模式： `^[a-zA-Z0-9_ ,.:()-]*$`。 必須是唯一的。 | 是 |
| `description` | 字串 | 選擇性說明。 最多255個字元。 | 無 |
| `type` | 字串 | 標準發行為`"RELEASE"`；跨團隊功能群組為`"CROSS_TEAM_FEATURE_GROUP"`。 | 是 |
| `status` | 字串 | 發行狀態。 針對IMS：建立時`"DRAFT"`；更新時`"DRAFT"`、`"SAVED"`、`"PUBLISHED"`。 針對CTFG：建立時`"SAVED"`；更新時`"SAVED"`，`"PUBLISHED"`。 | 是 |
| `clients` | 陣列 | 與此版本關聯的應用程式。 每個專案都需要`id` （數值）和`imsClientId` （字串）。 | 無 |
| `audience` | 陣列 | 對象規則清單。 請參閱[條件物件](feature-flags-management-api.md#condition-object)。 | 無 |
| `variations` | 陣列 | 變數清單。 提交期間僅支援1個變數。 | 提交所需 |
| `params` | 物件 | 版本引數。 請參閱[支援的引數欄位](#supported-params)。 | 提交所需 |
| `org` | 物件 | 組織物件。 必須包含`id`。 | 無 |

### 支援的引數欄位 {#supported-params}

| 欄位 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `label` | 字串 | 顯示名稱。 最多50個字元。 | 是 |
| `tags` | 陣列\&lt;字串\> | 選用的標籤。 每個最多50個字元。 | 無 |
| `canContextOverridePUP` | 布林值 | 如果`true`，則內容規則會覆寫設定檔規則。 預設值： `false`。 | 是 |
| `isBetaRelease` | 布林值 | 如果`true`，則將此版本標籤為測試版。 預設值： `false`。 | 無 |

### 變數物件 {#variation-object}

| 欄位 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `id` | 整數 | 變數ID。 只有更新呼叫才需要。 | 條件式 |
| `variantName` | 字串 | 變體名稱。 最多50個字元。 | 是 |
| `variantPercentage` | 雙精度 | 接收此變體的對象百分比。 範圍： [0,100]。 | 是 |
| `features` | 陣列 | 此變化中包括的功能。 每個專案都必須包含`id`、`name`、`clientId`和`state`。 | 無 |

## 另請參閱 {#see-also}

* [功能管理API概述](feature-management-apis-overview.md)
* [功能標幟管理API](feature-flags-management-api.md)
* [功能群組管理API](feature-group-management-api.md)
