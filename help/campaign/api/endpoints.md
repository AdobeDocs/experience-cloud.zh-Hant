---
title: 端點
description: 進一步瞭解API端點。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
exl-id: 9f6d3da6-374d-47f5-bc8f-b31b19cbb5ca
source-git-commit: 14d8cf78192bcad7b89cc70827f5672bd6e07f4a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 9%

---

# 端點 {#endpoints}

Adobe Campaign REST API的可用端點：

* **/profileAndServices**：與立即可用的欄位互動。 無法透過此端點存取延伸欄位。
* **/profileAndServicesExt**：與設定檔或服務自訂資源擴充期間新增的自訂欄位互動。 如需自訂資源的詳細資訊，請參閱[本節](custom-resources.md)。
* **/&lt;transactionalAPI>**：與交易式訊息API互動（交易式訊息API端點的名稱取決於您的執行個體設定）。 如需詳細資訊，請參閱[本章節](managing-transactional-messages.md)。
* **/工作流程/執行**：與工作流程互動。 如需詳細資訊，請參閱[本章節](controlling-a-workflow.md)。

依預設，**profileAndServices**&#x200B;與&#x200B;**profileAndServicesExt** API可用的主要資源為：

* **/設定檔**：與Campaign資料庫的設定檔互動。 若要將設定檔新增至服務，請使用&#x200B;**/服務**&#x200B;端點。 如需Campaign中設定檔的詳細資訊，請參閱[Campaign檔案](https://helpx.adobe.com/tw/campaign/standard/audiences/using/about-profiles.html)。
* **/服務**：管理訂閱服務。 如需Campaign中服務的詳細資訊，請參閱[Campaign檔案](https://helpx.adobe.com/tw/campaign/standard/audiences/using/creating-a-service.html)。

>[!NOTE]
>
>已擴充或建立的所有其他資源只能透過&#x200B;**ProfileAndServicesExt** API使用。 它們必須連結到&#x200B;**設定檔**&#x200B;資源才能存取。
