---
title: iOS整合指南的Experience Rollout擴充功能
description: 瞭解如何在iOS上將Experience Rollout擴充功能與Adobe Experience Platform Mobile SDK整合。
hide: true
source-git-commit: 12032cbed45e694a3f25f16afe80308b3eb82924
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 7%

---

# iOS的Experience Rollout擴充功能 {#ios-extension-integration-guide}

本指南說明如何在iOS上將Experience Rollout擴充功能與Adobe Experience Platform Mobile SDK整合。

## 先決條件 {#prerequisites}

在實作Experience Rollout擴充功能之前，請確定您已：

* 在[Adobe Experience Platform Data Collection](https://experience.adobe.com/#/data-collection)中設定的行動屬性
* 已在您的行動屬性中安裝並設定的Experience Rollout擴充功能
* Adobe Experience Cloud組織ID
* 最低部署目標： iOS 12.0
* Xcode 14.1或更新版本

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
1. 依照[發佈程式](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/overview)更新您的設定。

### 取得環境檔案ID {#environment-file-id}

1. 在您的行動屬性中，瀏覽至&#x200B;**環境**。
1. 為您的環境選取&#x200B;**安裝**&#x200B;欄下的方塊圖示。
1. 在&#x200B;**行動安裝指示**&#x200B;對話方塊中，複製&#x200B;**環境檔案識別碼**。

## 將Experience Rollout擴充功能新增至您的應用程式 {#add-to-app}

### 新增相依性 {#add-dependencies}

將行動SDK相依性新增至您的專案。 Experience Rollout擴充功能需要行動核心及下列與Edge相關的擴充功能。

#### 使用Swift Package Manager （建議） {#swift-package-manager}

1. 在Xcode中，瀏覽至&#x200B;**檔案** > **新增套件相依性**。
1. 輸入Adobe Experience Platform Mobile SDK存放庫URL：

   ```
   https://github.com/adobe/aepsdk-core-ios
   ```

1. 新增下列套件：

   | 套件 | 存放庫 |
   |---|---|
   | AEPCore， AEPLifecycle | `https://github.com/adobe/aepsdk-core-ios` |
   | AEPEdge | `https://github.com/adobe/aepsdk-edge-ios` |
   | AEPEdgeIdentity | `https://github.com/adobe/aepsdk-edgeidentity-ios` |
   | AEPRollout | `https://github.com/adobe/aepsdk-rollout-ios` |

#### 使用CocoaPods {#cocoapods}

將下列Pod新增至您的`Podfile`：

```ruby
pod 'AEPCore'
pod 'AEPLifecycle'
pod 'AEPEdge'
pod 'AEPEdgeIdentity'
pod 'AEPRollout'
```

然後執行：

```bash
pod install
```

>[!IMPORTANT]
>
>對於生產應用程式，Adobe建議釘選到明確的版本編號，而不是使用`~>`或開啟的範圍。 如需詳細資訊，請參閱[CocoaPods版本設定指南](https://guides.cocoapods.org/using/the-podfile.html)。

### 初始化SDK {#initialize-sdk}

呼叫任何Experience Rollout擴充功能API之前，請先在您的`AppDelegate` （或`SceneDelegate`）中初始化Mobile SDK。 使用您行動屬性中的環境檔案ID，讓應用程式會挑選您在「資料收集」中發佈的轉出設定。

**Swift**

```swift
import AEPCore
import AEPLifecycle
import AEPEdge
import AEPEdgeIdentity
import AEPRollout

@main
class AppDelegate: UIResponder, UIApplicationDelegate {

    func application(
        _ application: UIApplication,
        didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
    ) -> Bool {

        MobileCore.setLogLevel(.error)

        MobileCore.registerExtensions(
            [Lifecycle.self, Edge.self, Identity.self, Rollout.self]
        ) {
            // Initialize with your Environment File ID from Data Collection
            MobileCore.configureWith(appId: "YOUR_ENVIRONMENT_FILE_ID")
        }

        return true
    }
}
```

**Objective-C**

```objc
@import AEPCore;
@import AEPLifecycle;
@import AEPEdge;
@import AEPEdgeIdentity;
@import AEPRollout;

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application
    didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    [AEPMobileCore setLogLevel:AEPLogLevelError];

    NSArray *extensions = @[
        AEPMobileLifecycle.class,
        AEPMobileEdge.class,
        AEPMobileEdgeIdentity.class,
        AEPMobileRollout.class
    ];

    [AEPMobileCore registerExtensions:extensions completion:^{
        // Initialize with your Environment File ID from Data Collection
        [AEPMobileCore configureWithAppId:@"YOUR_ENVIRONMENT_FILE_ID"];
    }];

    return YES;
}

@end
```

>[!IMPORTANT]
>
>對於生產應用程式，僅使用`LogLevel.error`。 請勿在發行版本組建中使用`.debug`或`.verbose`。

## 評估內容 {#evaluation-context}

`FeatureEvaluationContext`包含目標屬性（用於轉出規則比對）和選擇性身分（用於analytics）。

| 方法 | 必要 | 說明 |
|---|---|---|
| `withIdentity(namespace:id:)` | 無 | 第一個引數：身分名稱空間（請參閱[Adobe身分名稱空間](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/identity/features/namespaces)）。 第二個引數：身分值。 當您想要在Analytics中表示該名稱空間和ID以用於此評估時，請包含此專案。 若未提供，Analytics預設會使用ECID。 這不會用來推動功能啟用決策。 |
| `withAttributes(_:)` | 無 | `[String: [String]]`. 索引鍵是轉出規則所使用的內容屬性名稱（例如`locale`、`platform`、`appVersion`、`deviceType`）。 值是目前使用者/工作階段之索引鍵的候選屬性值清單（例如`["en_US"]`或`["phone"]`）。 |

**Swift**

```swift
import AEPRollout

let attrs: [String: [String]] = [
    "locale": ["en_US"],
    "platform": ["IOS"],
    "appVersion": ["3.0.0"]
]

let ctx = FeatureEvaluationContext.builder()
    .withIdentity(namespace: "Email", id: "customer@example.com")
    .withAttributes(attrs)
    .build()
```

**Objective-C**

```objc
@import AEPRollout;

NSDictionary<NSString *, NSArray<NSString *> *> *attrs = @{
    @"locale": @[@"en_US"],
    @"platform": @[@"IOS"],
    @"appVersion": @[@"3.0.0"]
};

AEPFeatureEvaluationContext *ctx = [[[AEPFeatureEvaluationContextBuilder builder]
    withIdentityNamespace:@"Email" id:@"customer@example.com"]
    withAttributes:attrs]
    .build;
```

### 目標屬性範例 {#sample-attributes}

| 屬性 | 說明 | 範例值 |
|---|---|---|
| `locale` | 使用者的地區/語言 | `["en_US"]`, `["fr_FR"]` |
| `platform` | 平台識別碼 | `["IOS"]` |
| `appVersion` | 應用程式版本 | `["3.0.0"]` |
| `deviceType` | 裝置型別 | `["phone"]`, `["tablet"]` |

## API 參考 {#api-reference}

### isFeatureEnable {#is-feature-enabled}

`isFeatureEnabled`會傳回指定內容的體驗轉出功能是開啟還是關閉。 傳遞`featureKey`、`FeatureEvaluationContext` （選擇性的目標定位屬性和analytics的選擇性身分）以及完成處理常式。 請參閱[評估內容](#evaluation-context)。

**簽章**

*Swift*

```swift
Rollout.isFeatureEnabled(
    featureKey: String,
    evaluationContext: FeatureEvaluationContext,
    completion: @escaping (Bool) -> Void
)
```

*Objective-C*

```objc
[AEPMobileRollout isFeatureEnabled:(NSString *)featureKey
               evaluationContext:(AEPFeatureEvaluationContext *)evaluationContext
                      completion:(void (^)(BOOL))completion];
```

**參數**

| 參數 | 類型 | 說明 |
|---|---|---|
| `featureKey` | 字串 | 要在Experience轉出中評估的功能索引鍵 |
| `evaluationContext` | FeatureEvaluationContext | 視需要包含目標屬性以及分析的可選身分識別；針對空白內容使用`FeatureEvaluationContext.builder().build()`。 請參閱[評估內容](#evaluation-context)。 |
| `completion` | `(Bool) -> Void` | 如果功能已啟用，則使用`true`呼叫，否則使用`false`。 |

**範例**

*Swift*

```swift
import AEPRollout

Rollout.isFeatureEnabled(
    featureKey: "new-checkout-experience",
    evaluationContext: ctx
) { isEnabled in
    if isEnabled {
        showNewCheckout()
    } else {
        showDefaultCheckout()
    }
}
```

*Objective-C*

```objc
@import AEPRollout;

[AEPMobileRollout isFeatureEnabled:@"new-checkout-experience"
               evaluationContext:ctx
                      completion:^(BOOL isEnabled) {
    if (isEnabled) {
        [self showNewCheckout];
    } else {
        [self showDefaultCheckout];
    }
}];
```

### getFeature {#get-feature}

`getFeature`會針對提供的內容傳回評估的功能裝載。 當您需要更多已啟用/已停用，並且想要功能中繼資料或值時，請使用此API。

**簽章**

*Swift*

```swift
Rollout.getFeature(
    featureKey: String,
    evaluationContext: FeatureEvaluationContext,
    completion: @escaping (FeatureEvaluationResult?) -> Void
)
```

*Objective-C*

```objc
[AEPMobileRollout getFeature:(NSString *)featureKey
         evaluationContext:(AEPFeatureEvaluationContext *)evaluationContext
                completion:(void (^)(AEPFeatureEvaluationResult * _Nullable))completion];
```

**參數**

| 參數 | 類型 | 說明 |
|---|---|---|
| `featureKey` | 字串 | 要在Experience轉出中評估的功能索引鍵 |
| `evaluationContext` | FeatureEvaluationContext | 視需要包含目標屬性以及分析的可選身分識別；針對空白內容使用`FeatureEvaluationContext.builder().build()`。 請參閱[評估內容](#evaluation-context)。 |
| `completion` | `(FeatureEvaluationResult?) -> Void` | 使用評估的功能裝載呼叫；找不到功能時，可能為`nil`。 |

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

*Swift*

```swift
import AEPRollout

Rollout.getFeature(
    featureKey: "new-checkout-experience",
    evaluationContext: ctx
) { feature in
    if let meta = feature?.meta, !meta.isEmpty {
        applyMetaDrivenExperience(meta)
    } else {
        showFallbackExperience()
    }
}
```

*Objective-C*

```objc
@import AEPRollout;

[AEPMobileRollout getFeature:@"new-checkout-experience"
         evaluationContext:ctx
                completion:^(AEPFeatureEvaluationResult * _Nullable feature) {
    NSString *meta = feature.meta;
    if (meta != nil && meta.length > 0) {
        [self applyMetaDrivenExperience:meta];
    } else {
        [self showFallbackExperience];
    }
}];
```

### refreshCache {#refresh-cache}

根據預設，Experience Rollout擴充功能會定期根據您可設定的排程同步來自伺服器的最新轉出規則和功能。 如果您需要比下一次排定的同步處理更早的更新，請呼叫`refreshCache`以強制重新整理。 典型案例包括登入後或應用程式狀態改變而影響鎖定目標時。

**語法**

*Swift*

```swift
Rollout.refreshCache()
```

*Objective-C*

```objc
[AEPMobileRollout refreshCache];
```

### extensionVersion {#extension-version}

傳回Experience Rollout擴充功能的版本字串。

**語法**

```swift
Rollout.extensionVersion(): String
```

**範例**

*Swift*

```swift
let version = Rollout.extensionVersion()
```

*Objective-C*

```objc
NSString *version = [AEPMobileRollout extensionVersion];
```

## API摘要 {#api-summary}

| API | 傳回值 |
|---|---|
| `isFeatureEnabled(featureKey:evaluationContext:completion:)`. `FeatureEvaluationContext`攜帶規則的鎖定目標屬性和analytics的選用身分識別。 請參閱[isFeatureEnabled](#is-feature-enabled)。 | 透過完成處理常式布林值 |
| `getFeature(featureKey:evaluationContext:completion:)`. 傳回給定內容的評估功能裝載。 請參閱[getFeature](#get-feature)。 | FeatureEvaluationResult？ 透過完成處理常式 |
| `refreshCache()` | 無效 |
| `extensionVersion()` | 字串 |

## 另請參閱 {#see-also}

* [行動應用程式](../../integrate/mobile-applications.md)
* [整合步驟](../../integrate/integration-steps.md)
* [SDK](../../integrate/sdks.md)
* [Android擴充功能整合指南](../android/android-extension-integration-guide.md)

<!-- -->
