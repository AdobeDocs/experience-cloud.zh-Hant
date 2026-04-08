---
title: Android整合指南的Experience Rollout擴充功能
description: 瞭解如何在Android上將Experience Rollout擴充功能與Adobe Experience Platform Mobile SDK整合。
source-git-commit: fcb1d36fc92b3954a902d818a98f579672c577e9
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 7%

---


# Android的Experience Rollout擴充功能 {#android-extension-integration-guide}

本指南說明如何在Android上將Experience Rollout擴充功能與Adobe Experience Platform Mobile SDK整合。

## 先決條件 {#prerequisites}

在實作Experience Rollout擴充功能之前，請確定您已：

* 在[Adobe Experience Platform Data Collection](https://experience.adobe.com/#/data-collection)中設定的行動屬性
* 已在您的行動屬性中安裝並設定的Experience Rollout擴充功能
* Adobe Experience Cloud組織ID
* 最低SDK： API 21 (Android 5.0 Lollipop)

## 擴充功能相依性 {#extension-dependencies}

Experience Rollout擴充功能需要下列Adobe Experience Platform擴充功能：

| 擴充功能 | 說明 | 必要 |
|---|---|---|
| Mobile Core | 提供核心功能，包括設定和事件處理 | 是 |
| 生命週期 | 收集行動SDK的應用程式生命週期和工作階段資料 | 是 |
| Edge Network | 啟用與Adobe Experience Platform Edge Network的通訊 | 是 |
| Edge身分 | 管理Edge Network的使用者身分 | 是 |

請確認這些擴充功能已安裝在您的資料收集行動屬性中，並包含在您的應用程式相依性中。

## 在資料收集中設定Experience Rollout擴充功能 {#configure}

### 安裝擴充功能 {#install-extension}

1. 登入[Adobe Experience Platform資料彙集](https://experience.adobe.com/#/data-collection)。
1. 選取&#x200B;**標籤**&#x200B;標籤，然後選擇您的行動裝置屬性。
1. 瀏覽至&#x200B;**擴充功能** > **目錄**。
1. 搜尋&#x200B;**Experience Rollout擴充功能**&#x200B;並選取&#x200B;**安裝**。
1. 設定擴充功能設定：

   | 設定 | 說明 |
   |---|---|
   | 沙箱 | 包含您的體驗轉出設定的Adobe Experience Platform沙箱 |
   | 應用程式ID | 您在體驗轉出中的應用程式唯一識別碼 |
   | 資料集 ID | 分析事件資料的Adobe Experience Platform資料集ID |

1. 選取&#x200B;**「儲存」**。
1. 依照[發佈程式](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/tags/publish/overview)更新您的設定。

### 取得環境檔案ID {#environment-file-id}

1. 在您的行動屬性中，瀏覽至&#x200B;**環境**。
1. 為您的環境選取&#x200B;**安裝**&#x200B;欄下的方塊圖示。
1. 在&#x200B;**行動安裝指示**&#x200B;對話方塊中，複製&#x200B;**環境檔案識別碼**。

## 將Experience Rollout擴充功能新增至您的應用程式 {#add-to-app}

### 新增相依性 {#add-dependencies}

將行動SDK相依性新增至您的專案。 Experience Rollout擴充功能需要行動核心及下列與Edge相關的擴充功能。

#### 搭配BOM使用Gradle （建議） {#gradle-bom}

將下列相依性新增至應用程式的`build.gradle.kts`檔案：

```kotlin
dependencies {
    // Adobe Experience Platform Mobile SDK BOM
    implementation(platform("com.adobe.marketing.mobile:sdk-bom:3.+"))

    // Required extensions
    implementation("com.adobe.marketing.mobile:core")
    implementation("com.adobe.marketing.mobile:lifecycle")
    implementation("com.adobe.marketing.mobile:edge")
    implementation("com.adobe.marketing.mobile:edgeidentity")

    // Experience Rollout extension
    implementation("com.adobe.marketing.mobile:rollout")
}
```

#### 使用Gradle (Groovy) {#gradle-groovy}

```groovy
dependencies {
    // Adobe Experience Platform Mobile SDK BOM
    implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')

    // Required extensions
    implementation 'com.adobe.marketing.mobile:core'
    implementation 'com.adobe.marketing.mobile:lifecycle'
    implementation 'com.adobe.marketing.mobile:edge'
    implementation 'com.adobe.marketing.mobile:edgeidentity'

    // Experience Rollout extension
    implementation 'com.adobe.marketing.mobile:rollout'
}
```

>[!IMPORTANT]
>
>對於生產應用程式，Adobe建議使用明確版本編號，而非動態版本。 如需詳細資訊，請參閱[管理Gradle相依性](https://docs.gradle.org/current/userguide/dependency_management.html)。

### 新增許可權 {#add-permissions}

將下列許可權新增至您的`AndroidManifest.xml`檔案：

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

### 初始化SDK {#initialize-sdk}

呼叫任何Experience Rollout擴充功能API之前，請先初始化`Application`類別中的Mobile SDK。 使用您行動屬性中的環境檔案ID搭配`MobileCore.initialize`，讓應用程式挑選您在Data Collection中發佈的轉出設定。

#### 使用MobileCore.initialization {#mobile-core-initialize}

自Android BOM 3.8.0版開始，此API即會自動註冊擴充功能並啟用生命週期追蹤。

>[!IMPORTANT]
>
>對於生產應用程式，僅使用`LoggingMode.ERROR`。 請勿在發行版本組建中使用`DEBUG`或`VERBOSE`。

**Kotlin**

```kotlin
import android.app.Application
import com.adobe.marketing.mobile.LoggingMode
import com.adobe.marketing.mobile.MobileCore

class MainApplication : Application() {

    override fun onCreate() {
        super.onCreate()

        MobileCore.setLogLevel(LoggingMode.ERROR)

        // Initialize with your Environment File ID from Data Collection
        MobileCore.initialize(this, "YOUR_ENVIRONMENT_FILE_ID")
    }
}
```

**Java**

```java
import android.app.Application;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;

public class MainApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();

        MobileCore.setLogLevel(LoggingMode.ERROR);

        // Initialize with your Environment File ID from Data Collection
        MobileCore.initialize(this, "YOUR_ENVIRONMENT_FILE_ID", null);
    }
}
```

### 註冊Application類別 {#register-application}

在`AndroidManifest.xml`中註冊您的`Application`類別：

```xml
<application
    android:name=".MainApplication"
    ... >
</application>
```

## 評估內容 {#evaluation-context}

`FeatureEvaluationContext`包含目標屬性（用於轉出規則比對）和選擇性身分（用於analytics）。

| 方法 | 必要 | 說明 |
|---|---|---|
| `withIdentity(namespace, id)` | 無 | 第一個引數：身分名稱空間（請參閱[Adobe身分名稱空間](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/identity/features/namespaces)）。 第二個引數：身分值。 當您想要在Analytics中表示該名稱空間和ID以用於此評估時，請包含此專案。 若未提供，Analytics預設會使用ECID。 這不會用來推動功能啟用決策。 |
| `withAttributes(map)` | 無 | `Map<String, List<String>>`. 索引鍵是轉出規則所使用的內容屬性名稱（例如`locale`、`platform`、`appVersion`、`deviceType`）。 值是目前使用者/工作階段之索引鍵的候選屬性值清單（例如`["en_US"]`或`["phone"]`）。 |

**Kotlin**

```kotlin
import com.adobe.marketing.mobile.rollout.FeatureEvaluationContext

val attrs = mapOf(
    "locale" to listOf("en_US"),
    "platform" to listOf("ANDROID"),
    "appVersion" to listOf("3.0.0")
)

val ctx = FeatureEvaluationContext.builder()
    .withIdentity("Email", "customer@example.com")
    .withAttributes(attrs)
    .build()
```

**Java**

```java
import com.adobe.marketing.mobile.rollout.FeatureEvaluationContext;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

Map<String, List<String>> attrs = new HashMap<>();
attrs.put("locale", Arrays.asList("en_US"));
attrs.put("platform", Arrays.asList("ANDROID"));
attrs.put("appVersion", Arrays.asList("3.0.0"));

FeatureEvaluationContext ctx = FeatureEvaluationContext.builder()
        .withIdentity("Email", "customer@example.com")
        .withAttributes(attrs)
        .build();
```

### 目標屬性範例 {#sample-attributes}

| 屬性 | 說明 | 範例值 |
|---|---|---|
| `locale` | 使用者的地區/語言 | `["en_US"]`, `["fr_FR"]` |
| `platform` | 平台識別碼 | `["ANDROID"]` |
| `appVersion` | 應用程式版本 | `["3.0.0"]` |
| `deviceType` | 裝置型別 | `["phone"]`, `["tablet"]` |

## API 參考 {#api-reference}

### isFeatureEnable {#is-feature-enabled}

`isFeatureEnabled`會傳回指定內容的體驗轉出功能是開啟還是關閉。 傳遞`featureKey`、`FeatureEvaluationContext` （選擇性的目標定位屬性和analytics的選擇性身分）以及回呼。 請參閱[評估內容](#evaluation-context)。

**簽章**

*Kotlin*

```kotlin
Rollout.isFeatureEnabled(
    featureKey: String,
    evaluationContext: FeatureEvaluationContext,
    callback: AdobeCallback<Boolean>
)
```

*Java*

```java
Rollout.isFeatureEnabled(
    String featureKey,
    FeatureEvaluationContext evaluationContext,
    AdobeCallback<Boolean> callback);
```

**參數**

| 參數 | 類型 | 說明 |
|---|---|---|
| `featureKey` | 字串 | 要在Experience轉出中評估的功能索引鍵 |
| `evaluationContext` | FeatureEvaluationContext | 視需要包含目標屬性以及分析的可選身分識別；針對空白內容使用`FeatureEvaluationContext.builder().build()`。 請參閱[評估內容](#evaluation-context)。 |
| `callback` | AdobeCallback&lt;Boolean> | 如果功能已啟用，則使用`true`叫用，否則使用`false`。 您也可以傳遞`AdobeCallbackWithError<Boolean>`以處理`fail(...)`。 |

**範例**

*Kotlin*

```kotlin
import com.adobe.marketing.mobile.AdobeCallback
import com.adobe.marketing.mobile.rollout.Rollout

Rollout.isFeatureEnabled(
    "new-checkout-experience",
    ctx,
    object : AdobeCallback<Boolean> {
        override fun call(isEnabled: Boolean?) {
            if (isEnabled == true) {
                showNewCheckout()
            } else {
                showDefaultCheckout()
            }
        }
    }
)
```

*Java*

```java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.rollout.Rollout;

Rollout.isFeatureEnabled(
    "new-checkout-experience",
    ctx,
    new AdobeCallback<Boolean>() {
        @Override
        public void call(Boolean isEnabled) {
            if (Boolean.TRUE.equals(isEnabled)) {
                showNewCheckout();
            } else {
                showDefaultCheckout();
            }
        }
    }
);
```

### getFeature {#get-feature}

`getFeature`會針對提供的內容傳回評估的功能裝載。 當您需要更多已啟用/已停用，並且想要功能中繼資料或值時，請使用此API。

**簽章**

*Kotlin*

```kotlin
Rollout.getFeature(
    featureKey: String,
    evaluationContext: FeatureEvaluationContext,
    callback: AdobeCallback<FeatureEvaluationResult>
)
```

*Java*

```java
Rollout.getFeature(
    String featureKey,
    FeatureEvaluationContext evaluationContext,
    AdobeCallback<FeatureEvaluationResult> callback);
```

**參數**

| 參數 | 類型 | 說明 |
|---|---|---|
| `featureKey` | 字串 | 要在Experience轉出中評估的功能索引鍵 |
| `evaluationContext` | FeatureEvaluationContext | 視需要包含目標屬性以及分析的可選身分識別；針對空白內容使用`FeatureEvaluationContext.builder().build()`。 請參閱[評估內容](#evaluation-context)。 |
| `callback` | AdobeCallback&lt;FeatureEvaluationResult> | 以評估的功能裝載叫用；找不到功能時，可能是`null`。 您也可以傳遞`AdobeCallbackWithError<FeatureEvaluationResult>`以處理`fail(...)`。 |

**回應**

*FeatureEvaluationResult*

| 欄位 | 類型 | 說明 |
|---|---|---|
| `id` | 整數 | 數值功能識別碼 |
| `key` | 字串 | 功能鍵 |
| `releaseKey` | 字串？ | 此功能的發行金鑰（可用時） |
| `meta` | 字串？ | 可用時以JSON字串形式顯示功能中繼資料 |
| `analyticsParam` | AnalyticsParam？ | 已評估功能的Analytics詳細資料 |

*AnalyticsParam*

| 欄位 | 類型 | 說明 |
|---|---|---|
| `releaseId` | 整數 | 數值發行識別碼 |
| `featureId` | 整數 | 數值功能識別碼 |
| `variantId` | 字串？ | 變體識別碼 |

**範例**

*Kotlin*

```kotlin
import com.adobe.marketing.mobile.AdobeCallback
import com.adobe.marketing.mobile.rollout.FeatureEvaluationResult
import com.adobe.marketing.mobile.rollout.Rollout

Rollout.getFeature(
    "new-checkout-experience",
    ctx,
    object : AdobeCallback<FeatureEvaluationResult> {
        override fun call(feature: FeatureEvaluationResult?) {
            val meta = feature?.meta
            if (!meta.isNullOrEmpty()) {
                applyMetaDrivenExperience(meta)
            } else {
                showFallbackExperience()
            }
        }
    }
)
```

*Java*

```java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.rollout.FeatureEvaluationResult;
import com.adobe.marketing.mobile.rollout.Rollout;

Rollout.getFeature(
    "new-checkout-experience",
    ctx,
    new AdobeCallback<FeatureEvaluationResult>() {
        @Override
        public void call(FeatureEvaluationResult feature) {
            String meta = feature != null ? feature.getMeta() : null;
            if (meta != null && !meta.isEmpty()) {
                applyMetaDrivenExperience(meta);
            } else {
                showFallbackExperience();
            }
        }
    }
);
```

### refreshCache {#refresh-cache}

根據預設，Experience Rollout擴充功能會定期根據您可設定的排程同步來自伺服器的最新轉出規則和功能。 如果您需要比下一次排定的同步處理更早的更新，請呼叫`refreshCache`以強制重新整理。 典型案例包括登入後或應用程式狀態改變而影響鎖定目標時。

**語法**

*Kotlin*

```kotlin
Rollout.refreshCache()
```

*Java*

```java
Rollout.refreshCache();
```

### extensionVersion {#extension-version}

傳回Experience Rollout擴充功能的版本字串。

**語法**

```kotlin
Rollout.extensionVersion(): String
```

**範例**

*Kotlin*

```kotlin
val version = Rollout.extensionVersion()
```

*Java*

```java
String version = Rollout.extensionVersion();
```

## API摘要 {#api-summary}

| API | 傳回值 |
|---|---|
| `isFeatureEnabled(featureKey, evaluationContext, callback)`. `FeatureEvaluationContext`攜帶規則的鎖定目標屬性和analytics的選用身分識別。 請參閱[功能評估](#is-feature-enabled)。 | 布林值（透過callback） |
| `getFeature(featureKey, evaluationContext, callback)`. 傳回給定內容的評估功能裝載。 請參閱[getFeature](#get-feature)。 | 透過回呼的FeatureEvaluationResult |
| `refreshCache()` | 無效 |
| `extensionVersion()` | 字串 |

## 另請參閱 {#see-also}

* [行動應用程式](../../integrate/mobile-applications.md)
* [整合步驟](../../integrate/integration-steps.md)
* [SDK](../../integrate/sdks.md)
