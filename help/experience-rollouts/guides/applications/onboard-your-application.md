---
title: 將您的應用程式上線
description: 瞭解如何在Adobe Experience轉出中啟動新應用程式，以便開始建立和管理功能標幟。
exl-id: d88c27a5-f490-4504-9764-5e4ce98fdf20
source-git-commit: fcb1d36fc92b3954a902d818a98f579672c577e9
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 2%

---

# 將您的應用程式上線 {#onboard-your-application}

您必須擁有&#x200B;**管理員**&#x200B;角色才能新增應用程式。 如果您需要驗證或更新您的角色，請聯絡管理員。

## 新增應用程式 {#add-application}

1. 登入「體驗轉出」主控台，並導覽至&#x200B;**體驗轉出>應用程式**。

   >[!NOTE]
   >
   >如果看不到&#x200B;**新應用程式**&#x200B;按鈕，請確認您有&#x200B;**Floodgate管理員**&#x200B;角色。

2. 選取&#x200B;**新應用程式**。

3. 選取符合您的應用程式型別（網頁或行動裝置）的&#x200B;**平台**。

4. 提供下列資訊：

   | 欄位 | 說明 |
   |---|---|
   | **應用程式識別碼** | 從您的程式碼呼叫體驗轉出時使用的唯一識別碼。 使用您應用程式的使用者端ID。 |
   | **TTL** | 重新整理每個應用程式快取的輪詢間隔（秒）。 僅適用於伺服器端SDK。 |

5. 選取&#x200B;**新增**。 您的應用程式現在已註冊，可設定功能標幟。

## 後續功能 {#next-steps}

您的應用程式上線後，您就可以開始建立功能標幟：

* [建立您的第一個功能標幟](../feature-flags/create-your-first-feature-flag.md)
* [在您的應用程式中整合體驗轉出](../integrate/integrating-in-your-app.md)

## 另請參閱 {#see-also}

* [管理應用程式](manage-applications.md)
* [登入主控台](../console/log-in-to-the-console.md)
