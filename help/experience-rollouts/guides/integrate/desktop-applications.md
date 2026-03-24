---
title: 案頭應用程式
description: 瞭解如何使用Feature API V2將Adobe體驗轉出整合到案頭應用程式中。
source-git-commit: b82520eebe0070b5f76e0f7daeb2bb79a4bccca0
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---


# 案頭應用程式 {#desktop-applications}

透過進行直接REST API呼叫，將案頭應用程式與體驗轉出整合。 針對案頭使用者端使用&#x200B;**功能API V2**。

如需完整API參考資料，請參閱本指南的功能API區段中的&#x200B;**GET功能API V2**。

## 整合需求 {#requirements}

案頭使用者端必須：

* **執行API回應中傳回的TTL值**。 TTL會定義使用者端在再次呼叫API之前應該快取功能標幟資料的時間。 實作可驗證此行為的測試案例，以確保在沒有提供功能標幟時，較舊的應用程式版本正確進入休眠。
* **正常處理HTTP錯誤案例**。 建置後援功能集，如果API暫時無法使用，應用程式仍可運作。
* **維護詳細的整合測試計畫**，其中涵蓋上述TTL和錯誤處理需求。

## 應用程式ID {#app-id}

案頭使用者端在呼叫API時，可以使用&#x200B;**產品代碼和產品版本**&#x200B;做為應用程式識別碼，以取代標準使用者端識別碼。

## 另請參閱 {#see-also}

* [整合步驟](integration-steps.md)
* [啟動指南](startup-guide.md)
