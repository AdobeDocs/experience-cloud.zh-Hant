---
title: API疑難排解
description: 進一步瞭解與Campaign StandardAPI相關的常見問題
role: Data Engineer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
source-git-commit: 84b72258789ba61016deb813e93bdca0ea142712
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# API疑難排解 {#troubleshooting}

* **前往Adobe.io主控台時，您會收到下列錯誤：「Adobe I/O主控台僅適用於選取企業帳戶的成員。 如果您認為您應該擁有存取權，請聯絡您的系統管理員。」**

您只能為您所管理的組織建立API金鑰。 如果顯示此訊息，而您想要建立API金鑰，並且想要詢問組織的管理員之一。

* **向Adobe.io發出請求時，您會收到{&quot;error_code&quot;：&quot;403023&quot;，&quot;message&quot;：&quot;Profile is not valid&quot;}**

這表示您特定Campaign產品的IMS布建發生問題：IMS團隊需要加以修正。

若要取得詳細資訊，您可以使用權杖呼叫IMS API，以檢視您的IMS設定檔看起來是什麼樣子：您需要使用一個prodCtx，其中organization_id與您放入URL中的相同，以便Adobe.io能夠路由您的請求。
如果缺少，則需要修正IMS布建。

```
-X GET https://mc.adobe.io/{ORGANIZATION}/campaign/profileAndServices/profile \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

它會傳回以下錯誤。

```
{"error_code":"403023","message":"Profile is not valid"}
```

透過此請求檢查您的IMS設定檔。

```
-X GET https://ims-na1.adobelogin.com/ims/profile/v1 \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

在回應中，ORGANIZATION_ID值必須與您第一個GET要求中的值相同。

```
{
  "countryCode": "FR",
  "mrktPermEmail": null,
  "projectedProductContext": [
    {
    "prodCtx": {
      "statusCode": "ACTIVE",
      "ident": "ZQ9FRQK7BF09YXAESFY9DDQP1G",
      "modDts": 1448307260000,
      "organization_id": "actest",
      "owningEntity": "6096892F54B5819E0A4C98A2@AdobeOrg",
      "serviceCode": "dma_tartan",
      "label": "Adobe Marketing Cloud",
      "serviceLevel": "standard",
      "createDts": 1421181343000,
      "deal_id": " "
      }
    }
  ]
}
```

* **向Adobe.io發出請求時，您會收到{&quot;code&quot;：500， &quot;message&quot;：&quot;Oops. 發生錯誤。 請檢查您的URI，然後再試一次。&quot;}**

Adobe.io會宣告您無效的URI：很可能是您請求的URI無效。 在Adobe.io上，當您選取Campaign服務時，畫面會顯示一個選擇器，其中包含可能的organization_id清單。 您需要確認您選擇的檔案是否為放入URL中的檔案。

* **向Adobe.io發出請求時，您會收到{&quot;error_code&quot;：&quot;401013&quot;，&quot;message&quot;：&quot;Oauth權杖無效&quot;}**

您的權杖無效（用來產生權杖的不正確IMS呼叫）或您的權杖已過期。

* **建立後看不到我的設定檔**

視執行個體組態而定，建立的設定檔需要關聯至 **orgUnit**. 若要瞭解如何在建立中新增此欄位，請參閱 [本節](creating-profiles-api.md).

<!-- * (error duplicate key : quand tu crées un profile qui existe déjà , il faut faire un patch pour updater le profile plutôt qu'un POST)

With Curl
List all profiles

Create a profile

Update the mobilePhone attribute of a profile

API Calls on Service

GET the list of services

-->

<!--

How to find and use a filter?
Error codes:

* PAtch sur Age = message d'erreur :
500
Cannot update the 'age' property that is read-only
'age' property is not valid for the 'profile' resource.
-->

<!--
How to filter a list of subscribed profiles with available profile filters ? by date (by les filtres dispo sur la ressource) ?

Pattern classique :

recupérer la liste des subscriptions filtrées d'un profile
1) get sur profile
2) recup PKey
3) get sur PKey
4) get sur href des subscriptions

Comment savoir quel filtre appliquer ?

1) get sur metadata de profile
2) retourne description de la collection subscription
3) get sur la valeur du champ resTarget
4) get sur le href dans filters
5) retourne les filtres applicables sur l'url des data.

-->
