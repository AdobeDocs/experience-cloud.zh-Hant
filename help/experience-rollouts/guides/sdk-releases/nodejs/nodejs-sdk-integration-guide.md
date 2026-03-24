---
title: Node.js SDK整合指南
description: 瞭解如何將Experience Rollouts Node.js SDK整合至您的後端服務，以擷取及評估功能標幟。
source-git-commit: 9bfe0e55e89c1d7fbd77cde63831a6a186820e24
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---


# Node.js SDK整合指南 {#nodejs-sdk-integration-guide}

Experience Rollouts Node.js SDK是適用於Node.js服務的伺服器端程式庫。 它會在本機快取功能標幟資料，並在每個請求上評估標幟，而不使用同步API呼叫。

>[!NOTE]
>
>Node.js SDK僅供伺服器端使用。 若是使用者端網頁應用程式，請直接呼叫功能API V3 REST端點。

## 先決條件 {#prerequisites}

在整合Node.js SDK之前，請確定您擁有：

* Node.js伺服器端應用程式
* 透過Adobe Developer Console取得的&#x200B;**API金鑰**&#x200B;和&#x200B;**服務權杖** — 請參閱[訂閱API應用程式](../../integrate/subscribe-to-api-application.md)
* 您的&#x200B;**應用程式使用者端ID**&#x200B;已在Experience Rollouts主控台中註冊 — 請參閱[將您的應用程式上線](../../applications/onboard-your-application.md)

## 安裝SDK {#install}

將SDK新增至專案的`package.json`：

```json
"@floodgate/fg-client-sdk": "~1.0.10"
```

然後在您的程式碼中要求：

```javascript
const { floodgateClient } = require('@floodgate/fg-client-sdk');
```

## 初始化SDK {#initialize}

應用程式啟動時呼叫`createInstance()`一次：

```javascript
floodgateClient.createInstance(
  {
    adobeIoApiKey: "<YOUR_API_KEY>",
    clientIds: ["<CLIENT_ID_1>", "<CLIENT_ID_2>"],
    env: "PRD",    // Use "STG" for Stage
    featureRequestHttpParams: {
      timeout: 60 * 1000  // Optional: request timeout in ms
    },
    ingestAnalyticsHttpParams: {
      timeout: 5 * 1000   // Optional: analytics timeout in ms
    }
  },
  function(cb) {
    // Fetch a fresh service token from IMS and pass it in the callback
    cb(null, SERVICE_TOKEN);
  },
  function() {
    return true;  // Return false to disable analytics
  },
  function(response) {
    // Called when the SDK initializes successfully
    console.log("SDK initialized");
  },
  function(err) {
    // Called if initialization fails
    console.error("SDK init error:", err);
  }
);
```

## 擷取功能標幟 {#retrieve-features}

在回撥中會非同步傳回功能標幟。 根據您的使用者內容選擇適當的方法。

### 已驗證的使用者 {#authenticated-user}

```javascript
floodgateClient.getFeatures(
  {
    userAccessToken: "<USER_ACCESS_TOKEN>",
    visitorId: "<VISITOR_ID>",
    clientId1: "<CLIENT_ID>",
    meta: true
  },
  function(err, features) {
    if (err) {
      // Handle error and serve default experience
      return;
    }
    const isEnabled = floodgateClient.isFeatureEnabled(features, "MY_FEATURE_FLAG");
    // Serve experience based on isEnabled
  }
);
```

### 匿名使用者 {#anonymous-user}

當沒有可用的使用者存取權杖時，請使用版本標幟或省略該權杖以接收完整轉出版本：

```javascript
floodgateClient.getFeatures(
  {
    releaseFlag: "<RELEASE_FLAG>",
    visitorId: "<VISITOR_ID>",
    clientId1: "<CLIENT_ID>",
    meta: false
  },
  callback
);
```

### 預設完整轉出版本 {#default-releases}

若未提供存取權杖或發行標幟，SDK會傳回&#x200B;**完整轉出**&#x200B;或&#x200B;**基準**&#x200B;狀態的功能：

```javascript
floodgateClient.getFeatures(
  {
    clientId1: "<CLIENT_ID>",
    visitorId: "<VISITOR_ID>",
    meta: false
  },
  callback
);
```

## 檢查功能是否已啟用 {#check-feature}

```javascript
const isEnabled = floodgateClient.isFeatureEnabled(features, "MY_FEATURE_FLAG");

if (isEnabled) {
  // Serve the new experience
} else {
  // Serve the default experience
}
```

## 啟用偵錯記錄 {#debug-logging}

若要啟用詳細的SDK記錄，請在呼叫`createInstance()`時傳遞偵錯層級的記錄器執行個體：

```javascript
const bunyan = require('bunyan');
const logger = bunyan.createLogger({ name: "fg", sourceType: "SDK", level: "debug" });

floodgateClient.createInstance(
  { ..., log: logger },
  ...
);
```

## 另請參閱 {#see-also}

* [Node.js SDK發行說明](nodejs-sdk-release-notes.md)
* [SDK](../../integrate/sdks.md)
* [訂閱API應用程式](../../integrate/subscribe-to-api-application.md)
* [整合步驟](../../integrate/integration-steps.md)
