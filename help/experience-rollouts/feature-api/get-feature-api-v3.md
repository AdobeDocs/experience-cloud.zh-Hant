---
title: GET功能API V3
description: 體驗轉出功能API V3的API參考，用於擷取網頁和行動應用程式的功能標幟。
source-git-commit: 6ecedbfc6c7de392f214f3f8f2e71aa18e1bacb9
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 9%

---


# GET功能API V3 {#get-feature-api-v3}

功能API V3是擷取網頁和行動應用程式中功能標幟的主要端點。 它會根據使用者的身分和在主控台中設定的對象規則，傳回使用者符合資格的功能和發行版本。

**端點：** `GET {HOST}/fg/api/v3/feature`

將`https://p13-stage.adobe.io`用於暫存，將`https://p13n.adobe.io`用於生產。

## 請求 {#request}

### 請求標頭 {#request-headers}

| 標頭 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `x-api-key` | 字串 | 您應用程式的Adobe Developer Console API金鑰。 必須為中繼和生產分別布建。 | 是 |
| `Authorization` | 字串 | **不需要**&#x200B;用於未驗證的案例。 使用`Bearer <AccessToken>`驗證使用者。 針對伺服器端SDK快取情況使用`Bearer <ServiceToken>`。 | 無 |
| `x-adobe-uuid` | 字串 | 不重複訪客或裝置ID。 用於支援未驗證使用者的百分比轉出，並維護跨工作階段的粘著度及未驗證至已驗證的轉換。 | 無 |

### 查詢參數 {#query-parameters}

| 參數 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `clientId` | 字串 | 您應用程式的使用者端ID，已上線至體驗轉出主控台。 | 是 |
| `ignore_rf` | 布林值 | 如果`true`，會忽略發行旗標，並傳回使用者端的所有發行版本。 預設值： `false`。 | 無 |
| `rf` | 字串 | 發行旗標。 僅在`ignore_rf`為`false`時使用。 | 無 |
| `meta` | 布林值 | 如果是`true`，回應中會包含每個功能的中繼資料，並以索引鍵/值組傳回，其中值為Base64編碼。 預設值： `false`。 | 無 |
| `userId` | 字串 | 需要服務權杖。 您要擷取功能標幟的使用者GUID。 | 無 |
| *內容引數* | 不適用 | 以上未列出的任何查詢引數都會視為內容變數，並用於評估對象規則。 傳遞多個值做為`?key1=val1&key2=val2`。 範例：`?clientLanguage=ja_JP&contractCurrency=JPY`。 | 無 |

## 回應 {#response}

### 回應狀態代碼 {#response-status}

| 狀態代碼 | 說明 |
|---|---|
| `200 OK` | 回應本文中傳回的功能標幟資料。 |
| `304 Not Modified` | 使用者端所傳遞的ETag符合最新的伺服器狀態。 將此視為免操作 — 不套用任何變更。 |
| `400 Bad Request` | `clientId`未上線或要求格式錯誤。 |
| `403 Forbidden` | API金鑰無效或應用程式未在Adobe Developer Console中訂閱體驗轉出API。 |

### 回應標頭 {#response-headers}

| 標頭 | 說明 |
|---|---|
| `x-request-id` | 用於偵錯的唯一要求識別碼。 將此納入任何支援請求中。 |
| `ETag` | 代表此使用者功能之目前伺服器狀態的權杖。 在後續要求中傳遞此值為`If-None-Match`。 如果狀態未變更，API會傳回`304`。 |
| `x-adobe-fg-poll-interval` | 使用者端本機快取的TTL （秒）。 在此間隔過後，才重新呼叫API。 |

### 回應內文 {#response-body}

回應為JSON物件，其頂層欄位如下：

| 欄位 | 類型 | 說明 |
|---|---|---|
| `api_version` | 字串 | API版本。 內部欄位 — 不需要處理。 |
| `json_version` | 字串 | JSON結構描述版本。 內部欄位 — 不需要處理。 |
| `ttl` | 整數 | 快取TTL （秒）。 與`x-adobe-fg-poll-interval`回應標頭的值相同。 預設值： 300。 |
| `caching_enabled` | 布林值 | 如果`true`，則會在使用者端本機進行功能評估。 如果`false`，則評估會在每個要求的伺服器端進行。 |
| `client_analytics_params` | 物件 | 應用程式的Analytics設定。 請參閱下方的[client_analytics_params欄位](#client-analytics-params)。 |
| `releases` | 陣列 | 版本清單和功能標幟使用者符合資格。 請參閱下方的[發行欄位](#releases-fields)。 |

#### client_analytics_params欄位 {#client-analytics-params}

| 欄位 | 說明 |
|---|---|
| `app_id` | 應用程式的數值ID。 |
| `safe_event_required` | 如果此使用者端已啟用重新定位事件，則為`true`。 |
| `analytics_required` | V3回應中一律為`false`。 |

#### 發行欄位 {#releases-fields}

| 欄位 | 說明 |
|---|---|
| `release_name` | 使用者有資格使用的版本或功能群組的名稱。 |
| `bit_index` | 發行位元索引。 負值表示「完整轉出」狀態。 |
| `features` | 使用者符合資格的功能標幟鍵陣列。 只有在使用者符合資格且旗標處於啟用狀態時，才會傳回功能金鑰。 這是應用程式邏輯應該建置的主要欄位。 |
| `meta` | 選用的與功能相關的Base64編碼中繼資料。 使用前先解碼。 |
| `release_analytics_params` | 每個合格功能的分析中繼資料物件陣列。 請參閱下方的[release_analytics_params欄位](#release-analytics-params)。 在控制組案例中，`features`是空的。 |

#### release_analytics_params欄位 {#release-analytics-params}

| 欄位 | 類型 | 說明 |
|---|---|---|
| `app_id` | 整數 | 應用程式ID。 |
| `release_id` | 整數 | 版本ID。 |
| `bit_index` | 整數 | 發行位元索引。 已棄用。 |
| `variant_id` | 整數 | 如果使用者在控制組中，則為`0`；否則為非零。 |
| `feature_id` | 整數 | 內部功能識別碼。 |
| `f_key` | 字串 | 功能標幟鍵。 |

## 範例要求與回應 {#sample}

### 範例要求 {#sample-request}

```http
GET /fg/api/v3/feature?clientId=MyWebApp&meta=true HTTP/1.1
Host: p13n.adobe.io
Authorization: Bearer <ACCESS_TOKEN>
x-api-key: <YOUR_API_KEY>
If-None-Match: <ETAG>
```

### 範例回應 — 測試群組中的使用者 {#sample-response-test}

```json
{
  "api_version": "0.1",
  "json_version": "0.1",
  "clients": {
    "MyWebApp": {
      "analyticsVersion": "2.0",
      "client_analytics_params": {
        "app_id": 1378,
        "safe_event_required": false,
        "analytics_required": false
      },
      "releases": [
        {
          "bit_index": -160,
          "release_name": "||features||",
          "features": ["ff1", "ff2", "ff3"],
          "release_analytics_params": [
            {
              "app_id": 1378,
              "release_id": -1,
              "bit_index": -160,
              "variant_id": 10040476,
              "feature_id": 26059,
              "f_key": "ff1",
              "analytics_required": true
            }
          ]
        }
      ]
    }
  },
  "ttl": 60
}
```

### 範例回應 — 控制組中的使用者 {#sample-response-control}

當使用者在控制組中時，`features`陣列是空的，而`variant_id`是`0`：

```json
{
  "api_version": "0.1",
  "json_version": "0.1",
  "clients": {
    "MyWebApp": {
      "releases": [
        {
          "bit_index": -160,
          "release_name": "||features||",
          "features": [],
          "release_analytics_params": [
            {
              "app_id": 1378,
              "release_id": -1,
              "bit_index": -160,
              "variant_id": 0,
              "feature_id": 26059,
              "f_key": "ff1"
            }
          ]
        }
      ]
    }
  },
  "ttl": 60
}
```

## 另請參閱 {#see-also}

* [GET功能API V2](get-feature-api-v2.md)
* [網頁應用程式](../guides/integrate/web-applications.md)
* [行動應用程式](../guides/integrate/mobile-applications.md)
* [整合步驟](../guides/integrate/integration-steps.md)
