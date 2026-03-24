---
title: Node.js SDK發行說明
description: Experience Rollouts Node.js SDK的發行說明，包括所有發佈版本的新功能、改善和錯誤修正的變更記錄。
source-git-commit: 9bfe0e55e89c1d7fbd77cde63831a6a186820e24
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 1%

---


# Node.js SDK發行說明 {#nodejs-sdk-release-notes}

本頁面列出Experience Rollouts Node.js SDK的版本記錄。 如需整合設定，請參閱[Node.js SDK整合指南](nodejs-sdk-integration-guide.md)。

## 1.0.10版 {#v1-0-10}

**錯誤修正和通訊端改善**

* 修正排定的快取重新整理期間擲回的`ESOCKETTIMEDOUT`例外狀況。 已從`createInstance()`中的`featureRequestHttpParams`和`ingestAnalyticsHttpParams`移除`maxSockets`引數。
* 修正在HTTP 304 （未修改）回應後，可快取的使用者端被錯誤地標示為不可快取的錯誤。
* 已移除`isReleaseBitEnabled()` — 不再支援此方法。
* 改善記錄輸出，提供更好的診斷。
* 測試和涵蓋範圍資料夾不再包含在已發佈的npm套件中。

## 版本1.0.5 {#v1-0-5}

**穩定性改善**

快取重新整理處理和SDK初始化邊緣案例的一般修正。

## 版本1.0.3 {#v1-0-3}

**初始穩定版本**

Node.js SDK的第一個生產版本支援驗證、匿名及預設的完整轉出功能標幟擷取。

## 另請參閱 {#see-also}

* [Node.js SDK整合指南](nodejs-sdk-integration-guide.md)
* [Java SDK發行說明](../../sdk-releases/java/java-sdk-release-notes.md)
* [SDK](../../integrate/sdks.md)
