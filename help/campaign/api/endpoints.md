---
title: 端點
description: 進一步瞭解API端點。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
source-git-commit: 84b72258789ba61016deb813e93bdca0ea142712
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 9%

---

# 端點 {#endpoints}

Adobe Campaign REST API的可用端點：

* **/profileAndServices**：與現成可用欄位互動。 無法透過此端點存取延伸欄位。
* **/profileAndServicesExt**：與設定檔或服務自訂資源擴充期間新增的自訂欄位互動。 如需自訂資源的詳細資訊，請參閱 [本節](custom-resources.md).
* **/&lt;transactionalapi>**：與交易式訊息API互動（交易式訊息API端點的名稱取決於您的執行個體設定）。 如需詳細資訊，請參閱[本章節](managing-transactional-messages.md)。
* **/workflow/execution**：與工作流程互動。 如需詳細資訊，請參閱[本章節](controlling-a-workflow.md)。

依預設，可用於的主要資源 **profileAndServices** 和 **profileAndServicesExt** API包括：

* **/profile**：與Campaign資料庫的設定檔互動。 若要將設定檔新增至服務，請使用 **/service** 端點。 如需Campaign中設定檔的詳細資訊，請參閱 [Campaign檔案](https://helpx.adobe.com/campaign/standard/audiences/using/about-profiles.html).
* **/service**：管理訂閱服務。 如需Campaign中服務的詳細資訊，請參閱 [Campaign檔案](https://helpx.adobe.com/campaign/standard/audiences/using/creating-a-service.html).

>[!NOTE]
>
>所有其他已擴充或建立的資源可透過 **設定檔與服務分機** 僅限API。 它們必須連結至 **個人資料** 資源，以方便存取。
