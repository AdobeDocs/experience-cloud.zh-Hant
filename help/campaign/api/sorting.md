---
title: 排序
description: 深入瞭解如何執行排序作業
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Developer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限已移轉Campaign Standard的使用者使用"
exl-id: 7db25b8d-a6f1-4151-bf37-c47e9991ae48
source-git-commit: 11c49b273164b632bcffb7de01890c6f9d7ae9c2
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 10%

---

# 排序

排序預設為依遞增順序提供。 若要以遞減順序排序，請將&#x200B;**%20desc**&#x200B;附加至&#x200B;**_order**&#x200B;引數的值。

若要知道欄位是否可以排序，請將「可排序」引數核取至資源中繼資料中。 如需詳細資訊，請參閱[本章節](metadata-mechanism.md)。

<br/>

***範例要求***

* 擷取資料庫中電子郵件依字母順序排序的GET要求範例。

  ```
  -X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/email?_order=email \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  -H 'Cache-Control: no-cache' \
  -H 'X-Api-Key: <API_KEY>'
  ```

  對要求的回應。

  ```
  {
  "content": [
      "adam@email.com",
      "allison.durance@example.com",
      "amy.dakota@mail.com",
      "andrea.johnson@mail.com",
      ...
  ]
  ...
  }
  ```

* 範例GET請求以遞減Alpha順序擷取資料庫中的電子郵件。

  ```
  -X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/email?_order=email%20desc \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  -H 'Cache-Control: no-cache' \
  -H 'X-Api-Key: <API_KEY>'
  ```

  對要求的回應。

  ```
  {
  "content": [
      "tombinder@example.com",
      "tombinder@example.com",
      "timross@example.com",
      "john.smith@example.com",
      ...
  ]
  }
  ```
