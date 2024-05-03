---
title: 開始使用Campaign REST API
description: 將 Campaign 與一組技術結合，以建立整合並建置您自己的生態系統。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
source-git-commit: 84b72258789ba61016deb813e93bdca0ea142712
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 48%

---

# 開始使用Campaign REST API {#get-started-apis}

>[!CAUTION]
>
>本檔案旨在供移轉至Campaign v8的Adobe Campaign Standard客戶使用。
>
>在執行 API 呼叫之前，請檢查與您的授權合約相應的比例限制。如需詳細資訊，請參閱[此頁面](https://helpx.adobe.com/legal/product-descriptions/campaign-standard.html#ITInfrastructureResourcesbyActiveProfilesTiers)。

Campaign REST API的目的是讓您能夠 **建立整合** 適用於Adobe Campaign和 **打造專屬生態系統** 將Adobe Campaign與您使用的技術面板連線。

透過Adobe Campaign REST API，您可以存取下列功能：

<table><tr>
 <td valign="top"><a href="retrieving-profiles.md"><img width="60px" alt="條件" src="assets/icon_profile.svg"/></a><p><a href="retrieving-profiles.md">設定檔</a></p></td>
<td valign="top"><a href="creating-a-service.md"><img width="60px" alt="條件" src="assets/icon_services.svg"/></a><p><a href="creating-a-service.md">服務與訂閱</a></p></td>
<td valign="top"><a href="interacting-with-custom-resources.md"><img width="60px" alt="條件" src="assets/icon_customresources.svg"/></a><p><a href="interacting-with-custom-resources.md">自訂資源</a></p></td>
<td valign="top"><a href="controlling-a-workflow.md"><img width="60px" alt="條件" src="assets/icon_workflows.svg"/></a><p><a href="controlling-a-workflow.md">工作流程</a></p></td>
</tr></table>

若要使用Campaign REST API，您需要Adobe I/O帳戶。 這是前進並探索 API 功能的必備第一步。如需詳細資訊，請參閱[本章節](setting-up-api-access.md)。

我們提供的 API 使用&#x200B;**標準概念**，以及 REST 介面和 JSON 負載。

本檔案中詳細說明了所有端點，其中包含您應瞭解的控制API的一般概念、完整的API參考、代碼示例和快速入門手冊。 所有範例都可以與 Postman 搭配使用，但您可以自由使用您最愛的 REST 用戶端。

如果有任何遺漏或看起來不正確，請詢問[社群](https://experienceleaguecommunities.adobe.com/t5/adobe-campaign-standard/ct-p/adobe-campaign-standard-community)。
