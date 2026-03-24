---
title: 整合步驟
description: 請依照應用程式型別的整合步驟，將Adobe Experience轉出連線至您的網頁服務、網頁或行動應用程式或案頭應用程式。
source-git-commit: b82520eebe0070b5f76e0f7daeb2bb79a4bccca0
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 3%

---


# 整合步驟 {#integration-steps}

選擇符合您應用程式型別的整合路徑。

## 網路服務 {#web-services}

後端服務使用伺服器端SDK整合。 為您的技術棧疊選擇SDK 。

**Java**

請依照[Java SDK整合指南](../sdk-releases/java/java-sdk-integration-guide.md)的說明進行設定、相依性設定和初始化。

**Node.js**

請依照[Node.js SDK整合指南](../sdk-releases/nodejs/nodejs-sdk-integration-guide.md)的說明進行設定和初始化。

**其他語言**

如果您的棧疊未在上方列出，請直接與&#x200B;**功能API V3**&#x200B;整合（請參閱本指南的功能API一節）。 如果您需要指引，請聯絡體驗轉出支援。

## 網頁和行動應用程式 {#web-mobile}

網頁和行動應用程式呼叫&#x200B;**功能API V3**&#x200B;以擷取目前使用者的功能標幟，並在應用程式中套用條件式邏輯。

如需完整API參考資料，請參閱本指南的功能API區段中的&#x200B;**GET功能API V3**。

## 案頭應用程式 {#desktop}

案頭應用程式呼叫&#x200B;**功能API V2**&#x200B;以擷取功能標幟。

如需完整API參考資料，請參閱本指南的功能API區段中的&#x200B;**GET功能API V2**。

>[!IMPORTANT]
>
>案頭使用者端必須遵守API回應中的TTL值，並針對API無法使用狀態實作妥善的錯誤處理。 如需需求，請參閱[案頭應用程式](desktop-applications.md)。

## 另請參閱 {#see-also}

* [啟動指南](startup-guide.md)
* [SDK](sdks.md)
* [網路服務](web-services.md)
* [案頭應用程式](desktop-applications.md)
