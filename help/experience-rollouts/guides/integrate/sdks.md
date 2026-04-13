---
title: SDK
description: 瞭解Adobe Experience轉出中的SDK架構，以及Android可用的行動SDK擴充功能。
hide: true
exl-id: 110a440d-b52a-4e1e-a94f-86f9741a223a
source-git-commit: 12032cbed45e694a3f25f16afe80308b3eb82924
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---

# SDK {#sdks}

體驗轉出提供SDK，將功能標幟整合至您的應用程式中。 本頁說明SDK架構和可用選項。

## SDK架構 {#architecture}

所有Experience Rollout SDK共用相同的核心架構：

* **初始化** — SDK是在啟動時設定，並向Experience Rollouts服務註冊。
* **功能擷取** — SDK會擷取功能旗標資料，並在本機評估旗標。
* **快取** — SDK會快取功能標幟資料，並在可設定的輪詢間隔(TTL)上重新整理。
* **錯誤處理** — 如果服務無法使用，SDK會繼續從本機快取中提供功能旗標評估。

## 可用的SDK {#available-sdks}

### Android擴充功能 {#android-extension}

Android的Experience Rollout擴充功能與Adobe Experience Platform Mobile SDK整合。

如需設定指示，請參閱[Android擴充功能整合指南](../sdk-releases/android/android-extension-integration-guide.md)。

>[!NOTE]
>
>適用於Web和其他行動平台的其他SDK選項正在準備中，即將推出。 如需搶先使用的指引，請聯絡您的Adobe代表。

## 另請參閱 {#see-also}

* [Android擴充功能整合指南](../sdk-releases/android/android-extension-integration-guide.md)
* [網路服務](web-services.md)
* [整合步驟](integration-steps.md)

<!-- -->
