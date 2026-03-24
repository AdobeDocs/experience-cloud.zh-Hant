---
title: 啟動指南
description: 請依照下列步驟，從請求存取權到建立您的第一個功能標幟，讓您的應用程式與Adobe體驗轉出整合。
source-git-commit: 9bfe0e55e89c1d7fbd77cde63831a6a186820e24
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 1%

---


# 啟動指南 {#startup-guide}

請依照下列步驟，將體驗轉出整合至您的應用程式。

## 步驟1：要求存取權 {#step-1-access}

請求存取體驗轉出主控台並加入您的團隊。 如需逐步指示，請參閱[要求存取權](../console/request-access.md)。

## 步驟2：啟動您的應用程式 {#step-2-onboard}

取得存取權後，請登入Experience Rollouts主控台，並確認您的應用程式列在您的團隊底下。 如果沒有，請要求您的團隊管理員新增它。 請參閱[將您的應用程式上線](../applications/onboard-your-application.md)。

上線之前，請準備以下內容：

| 需求 | 詳細資料 |
|---|---|
| **應用程式識別碼** | 呼叫Experience Rollouts API時使用的唯一使用者端識別碼。 在可用的情況下，使用您應用程式現有的使用者端ID。 |
| **伺服器端使用者端** | 如果與伺服器端SDK整合，您需要具有適當許可權的管理員使用者端ID。 |
| **案頭使用者端** | 產品代碼和產品版本可用來取代使用者端ID。 |

## 步驟3：訂閱體驗轉出API {#step-3-subscribe}

透過Adobe Developer Console訂閱Experience Rollouts API，讓您的應用程式可以呼叫功能標幟端點。 請參閱[在Adobe Developer Console中訂閱API應用程式](subscribe-to-api-application.md)。

>[!NOTE]
>
>如果您透過伺服器端SDK進行整合，則需要服務權杖使用者端ID。 請聯絡Experience Rollout支援，將您的使用者端ID加入允許清單。

## 步驟4：使用SDK或API進行整合 {#step-4-integrate}

請針對您的應用程式型別，執行[整合步驟](integration-steps.md)。 選擇適合您棧疊的路徑：

* **網頁服務** → Java SDK或Node.js SDK
* **網頁和行動應用程式** → Feature API V3
* **案頭應用程式** → Feature API V2

## 步驟5：建立並測試您的第一個功能標幟 {#step-5-feature-flag}

整合完成後，請在主控台中建立您的第一個功能標幟並進行測試：

* [建立您的第一個功能標幟](../feature-flags/create-your-first-feature-flag.md)

## 另請參閱 {#see-also}

* [在您的應用程式中整合體驗轉出](integrating-in-your-app.md)
* [整合步驟](integration-steps.md)
* [SDK](sdks.md)
