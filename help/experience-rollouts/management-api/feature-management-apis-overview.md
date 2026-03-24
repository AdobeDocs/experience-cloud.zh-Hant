---
title: 功能管理API概述
description: Experience Rollouts管理API的總覽，可讓您以程式設計方式建立、讀取、更新和刪除功能標幟、功能群組和版本。
source-git-commit: 6ecedbfc6c7de392f214f3f8f2e71aa18e1bacb9
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# 功能管理API概述 {#feature-management-apis-overview}

體驗轉出管理API可讓您以程式設計方式管理功能標幟、功能群組和版本。 需要自動化工作流程或將體驗轉出整合到現有部署管道中的團隊可以使用這些API，而不是控制檯。

>[!NOTE]
>
>使用服務權杖的管理API的存取權會根據請求授予。 請聯絡體驗轉出支援，並提供要求存取權的業務理由。

## 可用的管理API {#available-apis}

下列管理API可供使用：

* [功能標幟管理API](feature-flags-management-api.md) — 建立、讀取、更新和刪除應用程式的功能標幟。
* [功能群組管理API](feature-group-management-api.md) — 建立、讀取、更新、刪除及控制功能群組的自動轉出計畫。
* [發行管理API](release-management-apis.md) — 建立和編輯跨團隊功能群組和發行。

## 常見需求 {#common-requirements}

所有管理API呼叫都需要下列專案：

* 來自Adobe Developer Console的&#x200B;**API金鑰** — 請參閱[訂閱API應用程式](../guides/integrate/subscribe-to-api-application.md)。
* **IMS使用者存取權杖**&#x200B;或&#x200B;**服務權杖**，在`Authorization`標頭中傳遞為`Bearer <token>`。
* `Content-Type: application/json`標頭。

中繼和生產環境必須分別布建API金鑰和權杖。

## 協助程式指南 {#helper-guides}

下列指南可協助您建立正確的API裝載：

* [取得應用程式的使用者端識別碼](get-client-id.md) — 查詢功能標幟與功能群組管理API所需的數值使用者端識別碼。
* [取得想要的對象條件](get-audience-criteria.md) — 使用主控台和GET API產生正確的對象條件JSON結構。
* [管理修補程式API](management-patch-api.md) — 更新功能標幟、功能群組或跨團隊功能群組的個別欄位，而不傳遞完整的物件。

## 另請參閱 {#see-also}

* [GET功能API V3](../feature-api/get-feature-api-v3.md)
* [GET功能API V2](../feature-api/get-feature-api-v2.md)
* [訂閱API應用程式](../guides/integrate/subscribe-to-api-application.md)
