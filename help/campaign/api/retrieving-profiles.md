---
title: 擷取設定檔
description: 進一步瞭解如何使用API擷取設定檔
role: Data Engineer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
exl-id: 19679804-f728-49fa-b26e-8f31b67c29bf
source-git-commit: 14d8cf78192bcad7b89cc70827f5672bd6e07f4a
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 4%

---

# 使用API擷取設定檔 {#retrieving-profiles}

擷取設定檔是透過&#x200B;**GET**&#x200B;要求執行的。

接著，您就可以使用篩選器、排序和分頁來縮小搜尋範圍。 如需詳細資訊，請參閱[其他作業](sorting.md)區段。

此外，Campaign StandardAPI可讓您根據以下欄位之一搜尋設定檔：電子郵件、名字、姓氏或任何自訂欄位。 如需詳細資訊，請參閱[本章節](#searching-field)。

<br/>

***範例要求***

* 擷取所有設定檔的範例GET請求。

  ```
  -X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  -H 'Cache-Control: no-cache' \
  -H 'X-Api-Key: <API_KEY>'
  ```

  對要求的回應。

  ```
  {
      "content": [
          {
              "PKey": "<PKEY>",
              "firstName": "John",
              "lastName":"Doe",
              "birthDate": "1980-10-24",
              ...
          },
          ...
  }
  ```

* 擷取前10個電子郵件值的範例GET請求。

  ```
  -X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/email?_lineCount=10 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  -H 'Cache-Control: no-cache' \
  -H 'X-Api-Key: <API_KEY>'
  ```

  對要求的回應。 「下一個」節點會傳回URL，讓您存取下一個10個電子郵件值。

  ```
  {
  "content": [
      "amy.dakota@mail.com",
      "kristen.smith@mail.com",
      "omalley@mail.com",
      "xander.harrys@mail.com",
      "jane.summer@mail.com",
      "gloria.boston@mail.com",
      "edward.snow@mail.com",
      "dorian.simons@mail.com",
      "peter.paolini@mail.com",
      "mingam+test08@adobe.com"
  ],
  "next": {
      "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/email?_lineCount=10&_
      lineStart=@Qy2MRJCS67PFf8soTf4BzF7BXsq1Gbkp_e5lLj1TbE7HJKqc"
  }
  }
  ```

## 根據欄位搜尋設定檔 {#searching-field}

**[!UICONTROL filterType]**&#x200B;引數可讓您根據以下欄位之一擷取設定檔：電子郵件、名字、姓氏，或在擴充設定檔資源時已在進階篩選中新增的任何自訂欄位。

>[!NOTE]
>
>搜尋會區分大小寫，且僅會在首碼上執行。 例如，您將無法使用設定檔的姓氏來查詢設定檔。

***範例要求***

* 根據名字篩選設定檔的範例請求。

  ```
  -X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/byText?text=John&filterType=firstName \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  -H 'Cache-Control: no-cache' \
  -H 'X-Api-Key: <API_KEY>'
  ```

* 根據姓氏篩選設定檔的範例請求。

  ```
  -X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/byText?text=Miller&filterType=lastName \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  -H 'Cache-Control: no-cache' \
  -H 'X-Api-Key: <API_KEY>'
  ```

* 根據電子郵件篩選設定檔的範例請求。

  ```
  -X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/byText?text=John%40gmail.com&filterType=email \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  -H 'Cache-Control: no-cache' \
  -H 'X-Api-Key: <API_KEY>'
  ```

* 根據「愛好」自訂欄位篩選設定檔的範例請求。

  ```
  -X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServicesExt/profile/byText?cusHobby=Dancing&filterType=Hobby \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  -H 'Cache-Control: no-cache' \
  -H 'X-Api-Key: <API_KEY>'
  ```
