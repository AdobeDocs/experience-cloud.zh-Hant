---
title: SDK
description: 瞭解Flags中的SDK架構，以及可用的AEP Web SDK和AEP Mobile SDK擴充功能。
hide: true
exl-id: 110a440d-b52a-4e1e-a94f-86f9741a223a
source-git-commit: b3e13a42c19eb7b8b7d5d402bf9a56f89f573044
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 4%

---

# SDK {#sdks}

標幟會提供SDK，以便將功能標幟整合至您的應用程式。 透過AEP Web SDK和AEP Mobile SDK部署旗標。

## SDK架構 {#architecture}

所有Flags SDK都共用相同的核心架構：

* **初始化** — SDK是在啟動時設定，並向Flags服務註冊。
* **功能擷取** — SDK會擷取功能旗標資料，並在本機評估旗標。
* **快取** — SDK會快取功能標幟資料，並在可設定的輪詢間隔(TTL)上重新整理。
* **錯誤處理** — 如果服務無法使用，SDK會繼續從本機快取中提供功能旗標評估。

## 可用的SDK {#available-sdks}

### AEP Web SDK {#web-sdk}

Web的Flags擴充功能整合了Adobe Experience Platform Web SDK，可在Web應用程式中評估旗標。

### Android擴充功能 {#android-extension}

Android的Flags擴充功能與Adobe Experience Platform Mobile SDK整合。

如需設定指示，請參閱[Android擴充功能整合指南](../sdk-releases/android/android-extension-integration-guide.md)。

### iOS擴充功能 {#ios-extension}

iOS的Flags擴充功能與Adobe Experience Platform Mobile SDK整合。

如需設定指示，請參閱[iOS擴充功能整合指南](../sdk-releases/ios/ios-extension-integration-guide.md)。

## 另請參閱 {#see-also}

* [Android擴充功能整合指南](../sdk-releases/android/android-extension-integration-guide.md)
* [網路服務](web-services.md)
* [整合步驟](integration-steps.md)

<!-- -->
