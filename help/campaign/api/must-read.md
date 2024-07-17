---
title: 必讀
description: 使用API前必須先讀取。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
exl-id: 9e2d1b59-55a5-4715-adfb-35191a9df536
source-git-commit: 14d8cf78192bcad7b89cc70827f5672bd6e07f4a
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# 必讀 {#must-read}

## 技術需求

* Adobe Campaign API必須僅用於伺服器對伺服器。
* 如果您要實作的使用案例與Adobe Campaign API允許的規模一致，請一律與您的Adobe技術聯絡人確認。
* 設定AdobeIO存取權需要特定許可權，如有任何問題，請聯絡Adobe支援。

## 許可權與存取權

* 依預設，Adobe Campaign API會使用管理員內容，因此組織單位和角色不適用。
* Adobe Campaign API會從角色內容中排除。
* 如果您想要使用一個或多個組織單位來設定API，請洽詢您的以Adobe技術連絡人。

## 資源表示

所有API資源都可在&#x200B;**JSON**&#x200B;中使用URL副檔名或HTTP Accept標頭：

`GET /profileAndServices/<resourceName>.json`

>[!NOTE]
>
>在URL中沒有副檔名，**json格式是內容型別的預設格式**。

<br/>

***要求樣本***

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile.json \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

## 主索引鍵與URL

* 請勿嘗試自行建立URL。 API會傳回所有URL。 不過，您也可以根據最上層資源名稱來建置URL。

* 說明範例的自動主要金鑰(PKey)值不適合用於其他特定部署。 它們是由Adobe Campaign API所產生。

* Adobe Campaign產生的自動主索引鍵值絕對不可儲存在外部資料庫或網站中。 您必須在資料庫定義中產生特定的關鍵欄位，並在開發期間加以使用。

## 自訂金鑰 {#custom-keys}

如果設定檔資源已使用自訂金鑰欄位擴展，您可以使用此欄位作為金鑰，而不是Adobe Campaign產生的自動主金鑰：

`GET /.../profileAndServicesExt/profile/<customKey>`

如果金鑰值與原始金鑰不同，或您使用自己的商業金鑰作為URI，而不是Adobe提供的商業金鑰，則無法使用PATCH操作修改自訂金鑰。

僅對&#x200B;**最上層設定檔資源**&#x200B;使用自訂金鑰。 API會傳回URL，且絕對不應由您自行建立。

<br/>

***範例要求***

若要使用自訂金鑰擷取設定檔的訂閱，請在自訂金鑰上執行GET操作。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServicesExt/profile/<customKey> \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

對傳回的訂閱URL執行GET要求。

```
-X GET <SUBSCRIPTION_URL> \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

它會傳回設定檔的訂閱清單。

```
"service": {
"PKey": "<PKEY>",
"href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/<PKEY>",
"label": "Sport Newsletter",
"name": "SVC1",
"title": "Sport Newsletter (SVC1)"
}
```
