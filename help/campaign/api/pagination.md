---
title: 分頁
description: 瞭解如何執行分頁作業。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Developer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限已移轉Campaign Standard的使用者使用"
exl-id: d6ebce3c-1e84-4b3b-a68d-90df4680af64
TQID: https://experienceleague.adobe.com/Ft50AgZSedRcL8pvSbeMkWG9Zgz38Dq-3fC7XN2j1-w
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: ad84694f2f6f45e4ee30fc51379106835ac302be
workflow-type: tm+mt
source-wordcount: 168
ht-degree: 1%

---

# 分頁

依預設，清單中會載入25個資源。

**_lineCount**&#x200B;引數可讓您限制回應中列出的資源數目。  然後您可以使用&#x200B;**next**&#x200B;節點來顯示下一個結果。

>[!NOTE]
>
>一律使用&#x200B;**next**&#x200B;節點中傳回的URL值來執行分頁要求。
>
>已計算&#x200B;**_lineStart**&#x200B;要求，且必須一律用於&#x200B;**next**&#x200B;節點中傳回的URL。

<br/>

***範例要求***

顯示設定檔資源1個記錄的範例GET請求。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile?_lineCount=1 \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

回應要求，使用&#x200B;**next**&#x200B;節點執行分頁。

```
{
    "content": [
        {
            "PKey": "<PKEY>",
            "firstName": "John",
            "lastName":"Doe",
            "birthDate": "1980-10-24",
            ...
        }
    ],
    "next": {
        "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/email?_lineCount=10&_
        lineStart=@Qy2MRJCS67PFf8soTf4BzF7BXsq1Gbkp_e5lLj1TbE7HJKqc"
    }
    ...
}
```

依預設，在與含有大量資料的資料表互動時，**next**&#x200B;節點無法使用。 若要執行分頁，您必須將&#x200B;**_forcePagination=true**&#x200B;引數新增至您的呼叫URL。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile?_forcePagination=true \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

>[!NOTE]
>
>在Campaign Standard **XtkBigTableThreshold**&#x200B;選項中定義了資料表被視為大型的記錄數。 預設值為100,000筆記錄。
