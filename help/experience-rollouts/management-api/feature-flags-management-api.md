---
title: 功能標幟管理API
description: 體驗轉出功能的API參考資料會標籤管理API，包括取得、建立、更新和刪除應用程式功能標籤的端點。
source-git-commit: 8a92b7a3e8c52da8bb2474f52c831e159420b878
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 12%

---


# 功能標幟管理API {#feature-flags-management-api}

功能標幟管理API可讓您以程式設計方式為體驗轉出中的應用程式建立、讀取、更新和刪除功能標幟。

**基底路徑：** `/m/api/v1/mgmt/feature`

所有要求都需要[一般需求](feature-management-apis-overview.md#common-requirements)中說明的標頭。

## 取得所有功能標幟 {#get-all-features}

擷取指定應用程式的所有功能標幟。

| | |
|---|---|
| **端點** | `GET /m/api/v1/mgmt/feature` |
| **方法** | GET |

### 查詢參數 {#get-all-query-params}

| 參數 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `clientId` | 整數 | 應用程式的數值ID。 請參閱[取得使用者端識別碼](get-client-id.md)。 如果未提供`imsClientId`，則為必要。 | 條件式 |
| `imsClientId` | 字串 | 應用程式的字串格式使用者端ID。 如果未提供`clientId`，則為必要。 | 條件式 |
| `nonReleaseFeature` | 布林值 | 設定為`true`以包含與任何群組或版本無關的獨立功能標幟。 以API為基礎的工作流程需要。 | 是 |

### 回應 {#get-all-response}

| 狀態 | 說明 |
|---|---|
| `200` | 成功。 回應內文包含功能標幟物件的清單。 |

回應本文包含`features`陣列。 每個元素都是功能標幟物件，其欄位在[FeatureDTO物件參考](#featuredto-object)中描述。

**範例回應：**

```json
{
  "features": [
    {
      "id": 22079,
      "name": "new.FF.1",
      "clientId": 1191,
      "state": "enabled",
      "description": "first feature flag",
      "release": { "id": 2631, "name": "FF.group", "status": "SAVED" },
      "audience": null,
      "params": { "label": "new FF 1", "rolloutType": "manual" }
    },
    {
      "id": 22080,
      "name": "new.FF.2",
      "clientId": 1191,
      "state": "enabled",
      "description": "second feature flag",
      "audience": [
        {
          "id": 10034665,
          "criteria": { "and": [{ "operator": "EQ", "attr": "LOCALE", "val": "EN" }] }
        }
      ]
    }
  ]
}
```

## 依ID取得功能標幟 {#get-feature-by-id}

依數值ID擷取單一功能標幟。

| | |
|---|---|
| **端點** | `GET /m/api/v1/mgmt/feature/{featureId}` |
| **方法** | GET |

### 回應 {#get-by-id-response}

| 狀態 | 說明 |
|---|---|
| `200` | 成功。 回應本文是單一[FeatureDTO物件](#featuredto-object)。 |
| `400` | 無效的功能ID。 |

## 建立功能標幟 {#create-feature}

建立新的功能標幟。

| | |
|---|---|
| **端點** | `POST /m/api/v1/mgmt/feature` |
| **方法** | POST |

### 要求內文 {#create-request-body}

要求內文是[FeatureDTO物件](#featuredto-object)。 建立時需要下列欄位：

| 欄位 | 必要 | 附註 |
|---|---|---|
| `name` | 是 | 功能標幟鍵。 最多50個字元。 模式： `^[a-zA-Z0-9_.-]*$` |
| `clientId` | 是 | 數值應用程式ID。 請參閱[取得使用者端識別碼](get-client-id.md)。 |
| `state` | 是 | `"enabled"`或 `"disabled"` |

### 回應 {#create-response}

| 狀態 | 說明 |
|---|---|
| `200` | 成功。 回應本文包含`{ "generatedFeatureId": <id> }`。 |
| `400` | 無效的承載。 |
| `403` | 此使用者端或對象規則的許可權不足。 |
| `417` | 具有開發人員角色的使用者無法儲存具有公開規則的功能 — 至少需要一個對象規則。 |

**範例要求：**

```json
{
  "name": "my-new-feature",
  "clientId": 1191,
  "state": "disabled",
  "description": "A new feature flag",
  "meta": "VGVzdA==",
  "audience": [
    {
      "criteria": {
        "and": [{ "operator": "EQ", "attr": "COUNTRY", "category": "default", "ruleId": 1, "val": "US" }]
      }
    }
  ],
  "variations": [{ "variantPercentage": 100, "variantName": "Variation 1" }],
  "params": { "label": "My New Feature", "tags": [] }
}
```

## 更新功能標幟 {#update-feature}

更新現有的功能標幟。 傳遞包含`id`欄位的完整[FeatureDTO物件](#featuredto-object)。

| | |
|---|---|
| **端點** | `PUT /m/api/v1/mgmt/feature` |
| **方法** | PUT |

### 回應 {#update-response}

| 狀態 | 說明 |
|---|---|
| `200` | 成功。 回應內文是更新的FeatureDTO物件。 |
| `400` | 無效的承載。 |
| `403` | 許可權不足。 |
| `417` | 並行更新衝突。 請先擷取目前的功能，然後從`params`以最新的`version`值重試。 |

## 刪除功能標幟 {#delete-feature}

依據其數值ID刪除功能標幟。

| | |
|---|---|
| **端點** | `DELETE /m/api/v1/mgmt/feature/{featureId}` |
| **方法** | DELETE |

### 回應 {#delete-response}

| 狀態 | 說明 |
|---|---|
| `204` | 成功。 無回應內文。 |
| `403` | 許可權不足。 |

## FeatureDTO物件參考 {#featuredto-object}

| 欄位 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `id` | 整數 | 功能標幟ID。 只有更新呼叫才需要。 | 條件式 |
| `name` | 字串 | 功能標幟金鑰（在API回應中傳回）。 最多50個字元。 模式： `^[a-zA-Z0-9_.-]*$` | 是（建立） |
| `clientId` | 整數 | 數值應用程式ID。 | 是 |
| `state` | 字串 | `"enabled"`或 `"disabled"` | 是 |
| `meta` | 字串 | API回應中隨功能傳回的Base64編碼中繼資料。 最多1024個字元。 | 無 |
| `description` | 字串 | 顯示說明。 最多225個字元。 | 無 |
| `audience` | 陣列 | 對象規則清單。 請參閱[FeatureRule物件](#featurerule-object)。 使用[取得所需的對象條件](get-audience-criteria.md)來產生此專案。 | 無 |
| `variations` | 陣列 | 變體清單。 最多3個。 請參閱[FeatureVariation物件](#featurevariation-object)。 | 無 |
| `params` | 物件 | 其他中繼資料。 支援的索引鍵： `label` （UI中的顯示名稱）、`tags` （字串陣列）。 | 無 |
| `release` | 物件 | 版本/群組關聯。`null` 如果旗標不在群組中。 唯讀。 | 無 |

### FeatureVariation物件 {#featurevariation-object}

| 欄位 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `id` | 整數 | 變數ID。 只有更新呼叫才需要。 | 條件式 |
| `variantName` | 字串 | 變體名稱。 固定值： `"Variation 1"`、`"Variation 2"`、`"Variation 3"`。 | 是 |
| `variantPercentage` | 小數 | 接收此變體的對象百分比。 必須大於0且不能超過100，最多小數點後2位。 | 是 |

### FeatureRule物 {#featurerule-object}

| 欄位 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `id` | 整數 | 規則ID。 只有更新呼叫才需要。 新增規則時設為`null`。 | 條件式 |
| `criteria` | 物件 | 定義對象規則的條件物件。 請參閱[條件物件](#condition-object)。 | 是 |

### 條件物件 {#condition-object}

| 欄位 | 類型 | 說明 |
|---|---|---|
| `and` | 陣列\&lt;條件\> | 所有條件都必須為true。 |
| `or` | 陣列\&lt;條件\> | 至少一個條件必須為true。 |
| `not` | 條件 | 此條件必須為false。 |
| `attr` | 字串 | 要評估的使用者屬性（例如，`COUNTRY`、`LOCALE`）。 |
| `operator` | 字串 | 比較運運算元（例如，`EQ`、`IN`、`LT`）。 |
| `val` | 字串 | 要比較的值。 |
| `meta` | 物件 | 選擇性條件中繼資料。`desc` 欄位會設定UI中的顯示標籤。 |

每個條件都必須提供`and`、`or`或`not`之一，或`attr`、`operator`和`val`的組合。

## 另請參閱 {#see-also}

* [功能管理API概述](feature-management-apis-overview.md)
* [管理修補程式API](management-patch-api.md)
* [取得應用程式的使用者端ID](get-client-id.md)
* [取得所需的對象條件](get-audience-criteria.md)
