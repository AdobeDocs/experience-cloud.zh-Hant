---
title: 管理異動訊息
description: 瞭解如何使用API管理異動訊息。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
exl-id: 00d39438-a232-49f1-ae5e-1e98c73397e3
source-git-commit: 6f9c9dd7dcac96980bbf5f7228e021471269d187
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---

# 管理異動訊息 {#managing-transactional-messages}

>[!AVAILABILITY]
>
>目前，使用REST API的交易式傳訊僅適用於電子郵件頻道和交易式事件(擴充資料僅透過裝載提供，類似Adobe Campaign V8的運作)。

建立並發佈交易式事件後，您需要將此事件的觸發專案整合至您的網站。

例如，您想要在客戶購買購物車中的產品之前，於其中一人離開您的網站時觸發「購物車放棄」事件。 若要這麼做，身為網頁開發人員，您必須使用REST異動訊息API。

1. 根據POST方法傳送要求，這會觸發異動事件的[傳送](#sending-a-transactional-event)。
1. 對POST要求的回應包含主索引鍵，可讓您透過GET要求傳送一或多個要求。 然後，您就可以取得[事件狀態](#transactional-event-status)。

## 傳送異動事件 {#sending-a-transactional-event}

交易式事件會透過具有下列URL結構的POST請求傳送：

```
POST https://mc.adobe.io/<ORGANIZATION>/campaign/<transactionalAPI>/<eventID>
```

* **&lt;組織>**：您的個人組織識別碼。 請參閱[本節](must-read.md)。

* **&lt;transactionalAPI>**： Transactional Messages API端點。

  異動訊息API端點的名稱取決於您的執行個體設定。 它與值「mc」相對應，後接您的個人組織ID。 讓我們以「geometrixx」作為其組織ID的Geometrixx公司為例。 在此情況下，POST要求會如下所示：

  `POST https://mc.adobe.io/geometrixx/campaign/mcgeometrixx/<eventID>`

  請注意，交易式訊息API端點也會在API預覽期間顯示。

* **&lt;eventID>**：您要傳送的事件型別。 此ID是在建立事件設定時產生的

### POST請求標頭

請求必須包含「Content-Type： application/json」標頭。

您必須新增字元集，例如&#x200B;**utf-8**。 請注意，此值取決於您使用的REST應用程式。

```
-X POST \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>' \
-H 'Content-Type: application/json;charset=utf-8' \
-H 'Content-Length:79' \
```

### POST要求內文

事件資料包含在JSONPOST內文中。 事件結構取決於其定義。 資源定義畫面中的API預覽按鈕提供請求範例。

您可以將下列選用引數新增至事件內容，以管理連結至事件的異動訊息的傳送：

* **到期** （選用）：在此日期之後，將會取消交易式事件的傳送。
* **已排程** （選用）：從這個日期起，將會處理交易式事件並傳送交易式訊息。

>[!NOTE]
>
>「expiration」和「scheduled」引數的值會遵循ISO 8601格式。 ISO 8601指定使用大寫字母「T」來分隔日期和時間。 不過，可將其從輸入或輸出中移除，以提高可讀性。

### 回應POST要求

POST回應會傳回建立交易式事件時的狀態。 若要擷取其目前狀態（事件資料、事件狀態……），請在GET要求中使用POST回應傳回的主索引鍵：

`GET https://mc.adobe.io/<ORGANIZATION>/campaign/<transactionalAPI>/<eventID>/`

<br/>

***範例要求***

傳送事件的POST要求。

```
-X POST https://mc.adobe.io/<ORGANIZATION>/campaign/mcAdobe/EVTcartAbandonment \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>' \
-H 'Content-Type: application/json;charset=utf-8' \
-H 'Content-Length:79'

{
  "email":"test@example.com",
  "scheduled":"2017-12-01 08:00:00.768Z",
  "expiration":"2017-12-31 08:00:00.768Z",
  "ctx":
  {
    "cartAmount": "$ 125",
    "lastProduct": "Leather motorbike jacket",
    "firstName": "Jack"
  }
}
```

對POST要求的回應。

```
{
  "PKey":"<PKEY>",
  "ctx":
  {
    "cartAmount": "",
    "lastProduct": "",
    "firstName": ""
  }
  "email":"",
  "scheduled":"2017-12-01 08:00:00.768Z",
  "expiration":"2017-12-31 08:00:00.768Z",
  "href": "mcAdobe/EVTcartAbandonment/<PKEY>",
  "serverUrl":" https://myserver.com ",
  "status":"pending",
  "type":""
}
```

### 異動事件狀態 {#transactional-event-status}

在回應中，「狀態」欄位可讓您知道事件是否已處理：

* **擱置中**：事件擱置中 — 事件會在剛觸發時採取此狀態。
* **正在處理**：事件正在等候傳遞 — 它正在轉換成訊息，而且正在傳送訊息。
* **已暫停**：事件處理序正在暫停。 系統將不再處理該檔案，但會將其保留在Adobe Campaign資料庫的佇列中。
* **已處理**：事件已處理，訊息已成功傳送。
* **已忽略**：傳送已忽略事件，通常是在隔離位址時。
* **deliveryFailed**：處理事件時發生傳遞錯誤。
* **routingFailed**：路由階段失敗 — 例如，當找不到指定的事件型別時，可能會發生這種情況。
* **tooOld**：事件在可以處理之前就過期了 — 這可能是由多種原因造成的，例如，傳送多次失敗（這會導致事件不再最新），或是伺服器在超載後無法再處理事件。
