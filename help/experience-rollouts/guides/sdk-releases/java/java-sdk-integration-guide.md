---
title: Java SDK整合指南
description: 瞭解如何將Experience Rollouts Java SDK整合至您的後端服務，以擷取及評估功能標幟。
exl-id: 7c12bd6c-1883-4f1c-985f-a2b0432e61ce
source-git-commit: 2a946868f58e25f8aafbf3ccfcf6571e7d0d8d20
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 1%

---

# Java SDK整合指南 {#java-sdk-integration-guide}

Experience Rollouts Java SDK是伺服器端程式庫，可在本機快取功能標幟資料，並在每個要求上評估標幟，而不需要同步API呼叫。 本指南涵蓋目前的SDK (4.x)。

## 先決條件 {#prerequisites}

在整合Java SDK之前，請確定您已：

* JDK 11或更新版本（從SDK 3.0.0版開始；舊版支援JDK 8+）
* Maven型組建系統
* 來自您Adobe Developer Console專案的&#x200B;**API金鑰**&#x200B;和&#x200B;**服務權杖**&#x200B;使用者端ID — 請連絡Experience Rollout支援，將您的使用者端ID加入允許清單
* 您的&#x200B;**應用程式使用者端ID**&#x200B;已在Experience Rollouts主控台中註冊 — 請參閱[將您的應用程式上線](../../applications/onboard-your-application.md)

## 新增Maven相依性 {#maven-dependency}

將Experience Rollouts Java SDK新增至專案的`pom.xml`：

```xml
<dependency>
  <groupId>com.adobe.cloudtech</groupId>
  <artifactId>fg-client-sdk</artifactId>
  <version>4.0.6</version>
</dependency>
```

## 初始化SDK {#initialize}

使用`FloodgateClient.createInstance()`在應用程式啟動時初始化SDK一次。 方法會採用您使用組態產生器建置的`FloodgateConfiguration`物件。

### 實作服務權杖回呼 {#service-token-callback}

SDK使用回呼介面在執行階段擷取新的服務權杖：

```java
private class FgConfigCallBack implements FGConfigBaseCallBack {

  @Override
  public String getIMSServiceToken() {
    // Fetch and return a valid service token
  }

  @Override
  public boolean isAnalyticsEnabled() {
    return false; // Set to true to enable analytics
  }
}
```

### 建立設定物件 {#configuration}

使用設定產生器來設定SDK：

```java
FloodgateConfiguration configuration = FloodgateConfiguration.FloodgateConfigurationBuilder
    .aFloodgateConfiguration(
        FgEnv.PRD,                   // Use FgEnv.STG for Stage
        "<YOUR_API_KEY>",
        Set.of("<CLIENT_ID_1>", "<CLIENT_ID_2>"),
        new FgConfigCallBack(),
        CallType.ASYNC
    )
    .withRetryPolicy(retryPolicy)    // Optional: defaults to 5 retries, 10s interval
    .build();
```

將`FgEnv.STG`用於中繼環境，將`FgEnv.PRD`用於生產。

### 建立使用者端執行個體 {#client-instance}

```java
FloodgateClient fgClient = FloodgateClient.createInstance(configuration);
```

## 擷取功能標幟 {#retrieve-features}

### 已驗證的使用者 {#authenticated-user}

使用IMS存取權杖為目前使用者擷取功能標幟：

```java
GetFeatureRequest request = GetFeatureRequestBuilder
    .aGetFeatureRequest("<CLIENT_ID>")
    .withAccessToken("<USER_ACCESS_TOKEN>")
    .withContext(context)
    .build();

FeaturesResponse[] features = fgClient.getFeatures(request);
```

### 匿名使用者 {#anonymous-user}

對於未驗證的使用者，請傳遞訪客ID與您的服務權杖：

```java
GetFeatureRequest request = GetFeatureRequestBuilder
    .aGetFeatureRequest("<CLIENT_ID>")
    .withServiceToken("<SERVICE_TOKEN>")
    .withVisitorId("<VISITOR_ID>")
    .withContext(context)
    .build();

FeaturesResponse[] features = fgClient.getFeatures(request);
```

### 擷取特定功能標幟或版本 {#specific-feature}

若要依索引鍵擷取單一功能標幟：

```java
GetFeatureRequest request = GetFeatureRequestBuilder
    .aGetFeatureRequest("<CLIENT_ID>")
    .withAccessToken("<ACCESS_TOKEN>")
    .withFeatureKey("<FEATURE_KEY>")
    .build();
```

若要透過發行金鑰擷取，請將`.withFeatureKey()`取代為`.withReleaseKey()`。

## 檢查功能是否已啟用 {#check-feature}

```java
boolean isEnabled = FloodgateClient.isFeatureEnabled(features, "MY_FEATURE_FLAG");

if (isEnabled) {
  // Serve the new experience
} else {
  // Serve the default experience
}
```

針對發行版本檢查：

```java
boolean isEnabled = FloodgateClient.isFeatureEnabled(features, "MY_RELEASE", "MY_FEATURE_FLAG");
```

## 快取管理 {#cache-management}

SDK會快取功能標幟資料，並在主控台中為每個應用程式設定的輪詢間隔上重新整理資料。 若要觸發隨選快取重新整理：

```java
fgClient.refreshClientCache("<CLIENT_ID>");
```

### 無法快取的使用者端 {#non-cacheable}

對於不可快取的使用者端，`getFeature()`每次都會進行即時API呼叫。 當使用者端變成可快取時，SDK會繼續背景輪詢並切換至快取型服務。 從SDK 0.8版開始支援。

## 設定選項 {#configuration-options}

產生器提供下列選用的設定方法：

| 選項 | 方法 | 說明 |
|---|---|---|
| 永遠使用快取 | `.alwaysCache()` | 繞過API的快取回應；用於沒有對象規則的標幟 |
| 停用快取 | `.neverCache()` | 停用預設快取；對自訂快取重新整理邏輯很有用 |
| 自訂HTTP使用者端 | `.withHttpClient(client)` | 使用您自己的HTTP使用者端 |
| 自訂執行程式 | `.withScheduledExecutorService(executor)` | 使用您自己的排程執行器進行背景輪詢 |
| 包含控制組 | `.includeControlGroup()` | 傳回功能回應中的控制組資料 |

## 處理錯誤 {#error-handling}

自動換行`getFeatures()`個呼叫以捕捉SDK例外狀況：

```java
try {
  features = fgClient.getFeatures(request);
} catch (FgClientException e) {
  int statusCode = e.getStatusCode();
  // Handle error and serve default experience
} catch (FgInitException e) {
  e.printStackTrace();
}
```

## 另請參閱 {#see-also}

* [Java SDK發行說明](java-sdk-release-notes.md)
* [SDK](../../integrate/sdks.md)
* [整合步驟](../../integrate/integration-steps.md)
