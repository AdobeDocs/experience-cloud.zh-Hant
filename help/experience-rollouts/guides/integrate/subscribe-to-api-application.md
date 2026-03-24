---
title: 訂閱Adobe Developer Console中的API應用程式
description: 瞭解如何透過Adobe Developer Console將您的應用程式訂閱到Experience Rollouts API，以便您可以呼叫功能標幟端點。
source-git-commit: 120a2ea34682c878aaf6f6cb75504a8704d10e3d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 3%

---


# 訂閱Adobe Developer Console中的API應用程式 {#subscribe-to-api}

若要從應用程式呼叫體驗轉出API，您必須透過[Adobe Developer Console](https://developer.adobe.com/console)訂閱。 這可讓您的應用程式取得使用者端ID，Experience Rollouts會使用此ID來識別來電者。

## 先決條件 {#prerequisites}

訂閱前，請確認下列事項：

* 您的應用程式已上線到體驗轉出主控台 — 請參閱[上線您的應用程式](../applications/onboard-your-application.md)
* 您可以存取貴組織的Adobe Developer Console

## 訂閱Experience Rollout API {#subscribe}

若要讓應用程式訂閱體驗轉出API，請遵循下列步驟：

1. 移至[Adobe Developer Console](https://developer.adobe.com/console)並使用您的組織認證登入。
2. 選取您的專案，或建立新專案。
3. 選取&#x200B;**新增API**。
4. 搜尋並選取&#x200B;**體驗轉出API**。
5. 依照提示設定API並產生認證。
6. 請注意專案產生的&#x200B;**使用者端識別碼**。 這是您在呼叫Experience Rollouts API以及在Experience Rollouts主控台中上線應用程式時使用的識別碼。

## 伺服器端SDK整合 {#server-sdk}

如果您使用Java SDK或Node.js SDK進行整合，則除了API金鑰之外，您還需要&#x200B;**服務權杖**&#x200B;使用者端ID。 服務權杖可讓SDK在背景呼叫Experience Rollout API。

>[!NOTE]
>
>伺服器端SDK使用者端ID必須先由Experience Rollout支援加入允許清單，才能進行API呼叫。 完成Developer Console設定後，請聯絡支援人員。

## 另請參閱 {#see-also}

* [啟動指南](startup-guide.md)
* [SDK](sdks.md)
* [將您的應用程式上線](../applications/onboard-your-application.md)
* [整合步驟](integration-steps.md)
