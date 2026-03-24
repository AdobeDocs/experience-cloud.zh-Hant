---
title: GET功能API V2
description: 體驗轉出功能API V2的API參考，用於擷取案頭應用程式的功能標幟。
source-git-commit: 6ecedbfc6c7de392f214f3f8f2e71aa18e1bacb9
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 11%

---


# GET功能API V2 {#get-feature-api-v2}

功能API V2專為案頭應用程式整合而設計。 它會擷取已驗證使用者的功能標幟和發行資料，除了標準使用者端ID外，還支援產品代碼和產品版本作為應用程式識別碼。

**端點：** `GET {HOST}/fg/api/v2/feature`

將`https://p13-stage.adobe.io`用於暫存，將`https://p13n.adobe.io`用於生產。

## 請求 {#request}

### 請求標頭 {#request-headers}

| 標頭 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `x-api-key` | 字串 | 您應用程式的Adobe Developer Console API金鑰。 必須為中繼和生產分別布建。 | 是 |
| `Authorization` | 字串 | `Bearer <AccessToken>`或`Bearer <ServiceToken>`。 | 是 |
| `x-adobe-uuid` | 字串 | 不重複訪客或裝置ID。 用於在未驗證的情況下提供百分比轉出，並維護工作階段粘著度。 | 無 |

### 查詢參數 {#query-parameters}

| 參數 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `clientId` | 字串 | 已上線至「體驗轉出」主控台的應用程式使用者端ID。 可傳遞多個值： `clientId=C1&clientId=C2`。 | 無 |
| `p` | 字串 | 產品、版本、平台、地區字串（PVPL格式）。 範例：`PHSP:17.0:WIN:en_US`。 可傳遞多個值： `p=PHSP:17.0:WIN:en_US&p=PPRO:8:WIN:en_US`。 評估中只會使用產品代碼和產品版本。 | 無 |
| `meta` | 布林值 | 若為`true`，會針對每個功能傳回Base64編碼的中繼資料。 預設值： `false`。 | 無 |
| *內容引數* | 不適用 | 任何其他索引鍵/值組都會視為內容變數，以進行對象規則評估。 範例：`clientLanguage=ja_JP&contractCurrency=JPY`。 | 無 |

>[!NOTE]
>
>識別應用程式至少需要`clientId`或`p`其中之一。

## 回應 {#response}

### 回應狀態代碼 {#response-status}

| 狀態代碼 | 說明 |
|---|---|
| `200 OK` | 回應本文中傳回的功能標幟資料。 |
| `304 Not Modified` | ETag符合目前的伺服器狀態。 視為免操作 — 不套用任何變更。 |
| `401 Unauthorized` | 授權權杖無效。 |

### 回應標頭 {#response-headers}

| 標頭 | 說明 |
|---|---|
| `x-request-id` | 用於偵錯的唯一要求識別碼。 將此納入任何支援請求中。 |
| `ETag` | 代表使用者目前功能狀態的權杖。 在後續要求中以`If-None-Match`傳遞。 若未變更，則傳回`304`。 |
| `x-adobe-fg-poll-interval` | 使用者端本機快取的TTL （以秒為單位）。 在此間隔過後重新呼叫API。 |

### 回應內文 {#response-body}

回應為JSON物件，其頂層欄位如下：

| 欄位 | 類型 | 說明 |
|---|---|---|
| `api_version` | 字串 | API版本。 內部欄位 — 不需要處理。 |
| `json_version` | 字串 | JSON結構描述版本。 內部欄位 — 不需要處理。 |
| `ttl` | 整數 | 快取TTL （秒）。 預設值： 300。 |
| `clients` | 物件 | 使用者端ID （或PVPL字串）與其發行資料的對應。 每個索引鍵都包含下述欄位。 |

#### 每個使用者端回應欄位 {#per-client-fields}

| 欄位 | 說明 |
|---|---|
| `releases` | 使用者可使用的發行版本陣列。 請參閱下方的[發行欄位](#releases-fields)。 |
| `client_analytics_params` | Analytics設定物件。 請參閱下方的[client_analytics_params欄位](#analytics-fields)。 |

#### 發行欄位 {#releases-fields}

| 欄位 | 說明 |
|---|---|
| `release_name` | 發行版本或功能群組的名稱。 |
| `bit_index` | 發行位元索引。 已棄用。 視發行狀態而定，可能是`null`或負值。 |
| `features` | 使用者符合資格的功能標幟鍵陣列。 只有在使用者符合資格且已啟用標幟時，才會顯示功能金鑰。 |
| `meta` | 選用的Base64編碼中繼資料。 使用前先解碼。 |
| `release_analytics_params` | 適用於合格功能的Analytics中繼資料。 在控制組案例中，`features`是空的。 |

#### release_analytics_params欄位 {#release-analytics-params}

| 欄位 | 類型 | 說明 |
|---|---|---|
| `app_id` | 整數 | 應用程式ID。 |
| `release_id` | 整數 | 版本ID。 |
| `bit_index` | 整數 | 已棄用。 |
| `variant_id` | 整數 | 控制組為`0`，否則為非零。 |
| `feature_id` | 整數 | 內部功能識別碼。 |
| `f_key` | 字串 | 功能標幟鍵。 |

#### client_analytics_params欄位 {#analytics-fields}

| 欄位 | 類型 | 說明 |
|---|---|---|
| `app_id` | 整數 | 應用程式ID。 |
| `safe_event_required` | 布林值 | 啟用重新定位事件時為`true`。 |
| `analytics_required` | 布林值 | 如果停用分析或預設流程為`false`；如果啟用Kinesis流程，則為`true`。 |

## 範例要求與回應 {#sample}

### 範例要求 {#sample-request}

```http
GET /fg/api/v2/feature?clientId=MyDesktopApp&p=PHSP:17.0:WIN:en_US&meta=true HTTP/1.1
Host: p13n.adobe.io
Authorization: Bearer <ACCESS_TOKEN>
x-api-key: <YOUR_API_KEY>
If-None-Match: <ETAG>
```

### 範例回應 {#sample-response}

```json
{
  "api_version": "0.1",
  "json_version": "0.1",
  "clients": {
    "PHSP:17.0:WIN:en_US": {
      "analyticsVersion": "1.0",
      "releases": []
    },
    "MyDesktopApp": {
      "analyticsVersion": "1.0",
      "client_analytics_params": {
        "app_id": 388,
        "safe_event_required": false,
        "analytics_required": false
      },
      "releases": [
        {
          "bit_index": 160,
          "release_name": "||features||",
          "features": ["feature_a", "feature_b"],
          "release_analytics_params": [
            {
              "app_id": 388,
              "release_id": -1,
              "bit_index": 160,
              "variant_id": 10031741,
              "feature_id": 2918,
              "f_key": "feature_a"
            }
          ],
          "meta": []
        }
      ]
    }
  },
  "ttl": 300
}
```

## 另請參閱 {#see-also}

* [GET功能API V3](get-feature-api-v3.md)
* [案頭應用程式](../guides/integrate/desktop-applications.md)
* [整合步驟](../guides/integrate/integration-steps.md)
