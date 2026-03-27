---
title: SDK
description: 瞭解Adobe Experience轉出中的SDK架構，以及Java和Node.js適用的可用SDK。
exl-id: 110a440d-b52a-4e1e-a94f-86f9741a223a
source-git-commit: 2a946868f58e25f8aafbf3ccfcf6571e7d0d8d20
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 2%

---

# SDK {#sdks}

Experience轉出提供伺服器端SDK，用於後端服務整合。 本頁說明SDK架構和可用選項。

## SDK架構 {#architecture}

所有Experience Rollout SDK共用相同的核心架構：

* **初始化** — SDK是透過傳回單一物件的`createInstance()`呼叫所設定。
* **功能擷取** — `getFeatures()`方法會從SDK擷取功能標幟資料。
* **快取** — SDK會快取來自Experience Rollouts服務的回應。 快取管理員會以可設定的輪詢間隔(TTL)重新整理快取。
* **錯誤處理** — 如果服務傳回503，快取管理員會保留現有的快取資料，並繼續提供功能旗標評估。 如果資料自上次呼叫(304)以來未變更，則不會更新快取。

## 先決條件 {#prerequisites}

整合SDK之前，請確定您具備下列條件：

1. **應用程式ID** — Experience Rollout主控台中上線的每個應用程式的使用者端ID。
2. **服務Token** — SDK用來在背景呼叫Experience Rollouts API。
3. **API金鑰** — 與API驗證的服務權杖搭配使用。

## 可用的SDK {#available-sdks}

### Java SDK {#java-sdk}

Java SDK是透過Maven發佈。 將相依性新增到專案的`pom.xml`以進行整合。 對於以Spring為基礎的應用程式，Maven相依性會在應用程式完全載入之前自動設定SDK快取。

Java SDK的主要規格：

* **支援的JDK：** JDK 8和更新版本
* **無法快取的使用者端：**&#x200B;由SDK 0.8版以後支援。 對於不可快取的使用者端，`getFeature()`會進行即時API呼叫，而不是從快取讀取。 SDK會在背景繼續輪詢，如果使用者端變成可快取，就會切換為快取型服務。

如需設定指示，請參閱[Java SDK整合指南](../sdk-releases/java/java-sdk-integration-guide.md)。

### Node.js SDK {#nodejs-sdk}

Node.js SDK是透過npm發佈。

如需設定指示，請參閱[Node.js SDK整合指南](../sdk-releases/nodejs/nodejs-sdk-integration-guide.md)。

## 另請參閱 {#see-also}

* [網路服務](web-services.md)
* [整合步驟](integration-steps.md)
* [Java SDK整合指南](../sdk-releases/java/java-sdk-integration-guide.md)
* [Node.js SDK整合指南](../sdk-releases/nodejs/nodejs-sdk-integration-guide.md)
