---
title: 品牌
description: 瞭解如何設定您的品牌
audience: administration
context-tags: branding,overview;branding,main
role: Admin
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
exl-id: 7afc802d-e90c-48c8-aa04-3ea543dfdfbc
source-git-commit: 34c6f8a137a9085b26c0ea8f78930cff6192cfc9
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 57%

---

# 設定品牌 {#branding-configure}

>[!IMPORTANT]
>
>一般使用者不能建立或修改品牌：這些操作必須由 Adobe Campaign 技術管理員執行。如需任何請求，請與 Adobe 客戶服務聯繫。

在Adobe Campaign V8中，您可以在&#x200B;**[!UICONTROL 管理>平台>品牌]**&#x200B;功能表中找到品牌。

**[!UICONTROL 品牌]**&#x200B;由以下特性所定義：

* **[!UICONTROL 身分識別]**&#x200B;可以定義並個人化您的品牌。本章節包含以下欄位：

   * **[!UICONTROL 標籤]** 在此介面中可見
   * **[!UICONTROL ID]**
   * **[!UICONTROL 品牌名稱]**
   * 品牌的&#x200B;**[!UICONTROL 網站 URL]** 與&#x200B;**[!UICONTROL 網站標籤]**
   * **[!UICONTROL 品牌標誌]**

  ![](assets/branding_1.png)

* **[!UICONTROL 已傳送電子郵件的標題引數]**，可個人化行銷活動的收件者所看到之內容。 本章節包含以下欄位：

   * 使用品牌電子郵件的&#x200B;**[!UICONTROL 寄件者（電子郵件）]**。
   * 使用品牌名稱的&#x200B;**[!UICONTROL 寄件者（姓名）]**。
   * 使用客戶可回覆的電子郵件地址&#x200B;**[!UICONTROL 回覆（電子郵件地址）]**。
   * 使用品牌名稱&#x200B;**[!UICONTROL 回覆（姓名）]**。
   * 使用的電子郵件有錯誤&#x200B;**[!UICONTROL 的錯誤（電子郵件地址）]**。

  >[!IMPORTANT]
  >
  >更新電子郵件的標題參數後，如果在範本建立的電子郵件中寄件者的姓名與電子郵件地址未更改時，請檢查範本的進階設定。

  ![](assets/branding_2.png)

* **[!UICONTROL 品牌設定]**&#x200B;定義用於追蹤及登入頁面存取的伺服器。 本章節包含以下欄位：

   * **[!UICONTROL 品牌子網域]**&#x200B;參考到Adobe要求委派給此品牌的特定指定子網域URL。

  請注意，追蹤、映象和應用程式伺服器的設定會儲存在與路由關聯的個別外部帳戶中。 這些設定會在布建期間套用，且不應加以修改。 若要顯示URL，請從您的外部帳戶存取&#x200B;**[!UICONTROL 品牌首碼]**&#x200B;索引標籤。

  ![](assets/branding_3.png)

<!--![](assets/branding_05.png)-->

<!--
* **[!UICONTROL Tracking URL configs]**, which defines the configuration of the URLs tracking for your brand.

  The additional parameters that allow the links to be tracked on external systems such as Web Analytics tools like Adobe Analytics or Google Analytics are defined here.
-->
