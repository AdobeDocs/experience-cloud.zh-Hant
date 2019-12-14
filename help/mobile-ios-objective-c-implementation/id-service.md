---
title: 透過Launch實作Adobe Experience Platform Identity Service
description: 瞭解如何新增Adobe Experience Platform Identity Service擴充功能，並使用「設定客戶ID」動作來收集客戶ID。 本課是「在Mobile iOS Objective-C應用程式中實作Experience cloud」教學課程的一部分。
seo-description: null
seo-title: 透過Launch實作Adobe Experience Platform Identity Service
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: e9dee6d0aa3b775d0ce617e2b2c57b56de491b8d

---


# 新增Adobe Experience Platform Identity Service

Adobe [Experience Platform Identity Service](https://docs.adobe.com/content/help/en/id-service/using/home.html) 會在所有Adobe解決方案中設定共同的訪客ID，以強化Experience cloud功能，例如解決方案之間的觀眾共用。  您也可以將您自己的客戶ID傳送至服務，以啟用跨裝置鎖定並整合您的客戶關係管理(CRM)系統。

Identity service是Mobile Core擴充功能的一部分， ***因此您在安裝Mobile SDK時已實作***! 目前，本教學課程不包含設定客戶ID的指示。 如需如何設定客戶ID的詳 [細資訊，請參閱檔案](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference)。

## 驗證步驟

若要驗證對Identity service的呼叫，請在Xcode或Developer studio中執行範例應用程式，開啟Debug Console並尋找請求和回應：

1. **向Identity Service** (將控制台篩選為 `demdex.net`)請求在此範例中，ID(`d_mid`)已設定，且正在重新報告)

```objective-c
2019-03-13 16:53:26.655908-0400 BusBookingObjectiveC[56630:3854937] [AMSDK DEBUG <com.adobe.module.identity>]:Sending request (https://dpm.demdex.net/id?d_rtbd=json&d_ver=2&d_orgid=7ABB3E6A5A7491460A495D61@AdobeOrg&d_mid=67027929491180584128922600814231770586)
```

1. **來自Identity Service的回應** (將控制台篩選為 `ID Service`)。 請注意此 `mid` 值如何符合 `d_mid` 上述請求中的值：

```objective-c
2019-03-13 16:53:27.397048-0400 BusBookingObjectiveC[56630:3854937] [AMSDK DEBUG <com.adobe.module.identity>]: ID Service - Got ID Response (mid: 67027929491180584128922600814231770586, blob: j8Odv6LonN4r3an7LhD3WZrU1bUpAkFkkiY1ncBR96t2PTI, hint: 9, ttl: "604800000 ms")
```

[下一個「新增Adobe Target VEC支援」&gt;](target-vec.md)
