---
title: 使用API建立服務
description: 瞭解如何使用API建立服務
role: Data Engineer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
exl-id: 91bbce9e-a618-4be2-840b-c7d021271f4e
source-git-commit: 3f4400f24b75e8e435610afbe49e9d9444dbf563
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 使用API建立服務{#creating-a-service-api}

使用執行服務建立 **POST** 服務資源上的要求。

如果您想要使用特定屬性建立服務，請將其新增至裝載。 否則，將使用預設服務建立新服務。

<br/>

***範例要求***

使用特定屬性建立服務的範例POST要求。

```
-X POST https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/ \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
-i
-d {
-d "label": "My newsletter",
-d "messageType": "email",
-d "name": "email_newsletter",
-d "start": "2019-10-06"
-d }
```

它會傳回具有更新屬性的新建立服務。

```
{
    "PKey": "<PKEY>",
    "builtIn": false,
    "created": "2019-09-26 12:00:37.005Z",
    "href": "https://mc.adobe.io/<ORGANIZATION>/profileAndServices/service/@NLscZuVHxdVu9rPftvrMWFfR1zRIxQGswSOmGLrK09JTF_iWhB0JCUHEndA_vvy__k9mzOYa5NVkcWDcrK8qGh0wygahX9kRcD44kiWWSEceShn3",
    "label": "My newsletter",
    ...
}
```
