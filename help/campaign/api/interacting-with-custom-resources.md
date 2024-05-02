---
title: 與自訂資源互動
description: 進一步瞭解使用API進行自訂資源管理/
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
exl-id: 19bfeecb-da60-479c-a929-0cfb72ef59e3
source-git-commit: 3f4400f24b75e8e435610afbe49e9d9444dbf563
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 與自訂資源互動 {#interacting-with-custom-resources}

此 **/customResources** 端點可讓您在REST中公開Campaign自訂資源。 根據此API，可整合自訂實體和外部端點。

/customResources端點的行為與/profileAndServices端點完全相同。

此API中公開的自訂資源為：

* 所有未在/profileAndServicesExt底下公開的實體
* 所有未連結至設定檔的實體，以及這些實體的子系與孫系。
* 依預設，所有未連結至任何專案的實體，及其子系與孫系。

>[!NOTE]
>/profileAndServicesExt底下可用的自訂資源不會在/customResources API中公開。


以下是從自訂資源擷取中繼資料的範例：

```
GET /customResources/resourceType/<customResourceName>
```

若要執行建立、更新或刪除，會使用GET、POST、PATCH、DELETE。

```
POST /customResources/<customResourceName>
```
