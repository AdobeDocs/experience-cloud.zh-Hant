---
title: Java SDK發行說明
description: Experience Rollouts Java SDK的發行說明，包括所有發佈版本的新功能、改善和錯誤修正的變更記錄。
source-git-commit: 9bfe0e55e89c1d7fbd77cde63831a6a186820e24
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 2%

---


# Java SDK發行說明 {#java-sdk-release-notes}

本頁面列出Experience Rollouts Java SDK的發行歷史記錄。 如需整合設定，請參閱[Java SDK整合指南](java-sdk-integration-guide.md)。

## 版本4.0.6 {#v4-0-6}

**回應中的控制組資料**

您現在可以在SDK回應中擷取變體和控制群組資料，並比對REST功能API的行為。 若要啟用此功能，請新增`.includeControlGroup()`至您的`FloodgateConfiguration`產生器。

## 版本4.0.5 {#v4-0-5}

**穩定性與效能改善**

對快取重新整理可靠性和連線處理進行微幅內部改進。

## 版本4.0.4 {#v4-0-4}

**重試原則改善**

改善暫時性服務錯誤的預設重試行為。

## 版本4.0.3 {#v4-0-3}

**錯誤修正**

非同步初始化中邊緣案例的一般穩定性修正。

## 版本4.0.1 (Beta) {#v4-0-1-beta}

4.x SDK的&#x200B;**Beta版本**

推出DX使用者端支援、DX區域設定和AEP （沙箱）支援。

## 3.1.0 版 {#v3-1-0}

**DX使用者端的串流支援**

新增SSE型串流功能，以近乎即時地通知SDK使用者端旗標更新。

## 版本3.0.x {#v3-0-x}

已推出&#x200B;**Java 11需求**

從3.0.0版開始，SDK需使用JDK 11或更新版本。 舊版主要版本支援JDK 8+。

推出適用於DX使用者端的逐一參考對象支援，允許功能實體中的ID參考可重複使用的對象定義。

## 2.x版 {#v2-x}

**不可快取的使用者端支援（來自0.8）**

不可快取的使用者端可以呼叫`getFeature()`即時，而不是從SDK快取讀取。 SDK會在背景中持續輪詢，並在使用者端變成可快取時，切換為快取型服務。

其他2.x改善專案包括新的產生器選項（`alwaysCache()`、`neverCache()`、自訂HTTP使用者端和執行器支援）、功能和發行金鑰篩選以及模擬使用者擷取。

## 1.x版 {#v1-x}

初始發行系列。 支援的JDK 8+、Maven相依性整合以及基本驗證和匿名功能標幟擷取。

## 另請參閱 {#see-also}

* [Java SDK整合指南](java-sdk-integration-guide.md)
* [Node.js SDK發行說明](../../sdk-releases/nodejs/nodejs-sdk-release-notes.md)
* [SDK](../../integrate/sdks.md)
