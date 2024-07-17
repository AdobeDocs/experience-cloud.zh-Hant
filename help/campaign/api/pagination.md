---
title: 分頁
description: 瞭解如何執行分頁作業。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
exl-id: d6ebce3c-1e84-4b3b-a68d-90df4680af64
source-git-commit: 14d8cf78192bcad7b89cc70827f5672bd6e07f4a
workflow-type: tm+mt
source-wordcount: '169'
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

顯示設定檔資源1個記錄的範例GET要求。

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
