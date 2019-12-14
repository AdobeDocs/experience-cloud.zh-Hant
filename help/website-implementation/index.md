---
title: 使用Adobe Experience Platform Launch在網站中實作Adobe Experience Cloud
description: 使用Launch在網站中實作Experience cloud是前端開發人員或技術行銷人員的最佳起點，他們想要瞭解如何在其網站上實作Adobe Experience cloud解決方案。
seo-description: null
seo-title: 使用Adobe Experience Platform Launch在網站中實作Adobe Experience Cloud
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: 7166d2933cc99bcbbd4713fba8f87fb0826b711e

---


# 概述

_使用Launch在網站中實作Experience Cloud_ ，是想要瞭解如何在其網站上實作Adobe Experience cloud解決方案的前端開發人員或技術行銷人員的最佳起點。

每堂課都包含操作練習和基礎資訊，可協助您實作Experience Cloud並瞭解其價值。  我們提供的註解會反白標示資訊，這些資訊可能對從我們舊版標籤管理程式（動態標籤管理）移轉的客戶有用。 示範網站是供您完成本教學課程使用，讓您可以在安全的環境中瞭解基礎技術。完成本教學課程後，您應準備好透過Launch在您自己的網站上開始實作所有行銷解決方案。

完成此作業後，您將能夠：

* 建立啟動屬性

* 在網站上安裝Launch屬性

* 新增下列Adobe Experience cloud解決方案：
   * **[Adobe Experience Platform Identity Service](id-service.md)**
   * **[Adobe Target](target.md)**
   * **[Adobe Analytics](analytics.md)**
   * **[Adobe Audience Manager](audience-manager.md)**

* 建立規則和資料元素，以傳送資料至Adobe解決方案

* 使用Adobe Experience cloud除錯程式驗證實作

* 透過開發、接移和生產環境，在Launch中發佈變更

>[!NOTE] 下列平台也提供類似的多解決方案教學課程：
>
> * [在Mobile iOS Swift™應用程式中實作Experience Cloud](/help/mobile-ios-swift-implementation/index.md)
* [在Mobile iOS Objective-C應用程式中實作Experience Cloud](/help/mobile-ios-objective-c-implementation/index.md)
* [在行動Android應用程式中實作Experience Cloud](/help/mobile-android-implementation/index.md)


## 必要條件

在這些課程中，您假設您擁有Adobe id和完成練習所需的權限。 如果沒有，您可能需要聯絡您的Experience cloud管理員以請求存取權。

* 對於Launch，您必須擁有「開發」、「核准」、「發佈」、「管理擴充功能」和「管理環境」的權限。 For more information on Launch permissions, see [the documentation](https://docs.adobe.com/content/help/en/launch/using/reference/admin/user-permissions.html).
* 若是Adobe Analytics，您必須知道追蹤伺服器，以及您要使用哪些報表套裝來完成本教學課程
* 對於Audience Manager，您必須知道您的Audience Manager子網域（也稱為「合作夥伴名稱」、「合作夥伴ID」或「合作夥伴子網域」）

此外，我們假設您已熟悉 HTML 和 JavaScript 等前端開發語言。您並不需要精通這些語言才能完成這些課程，但如果您熟悉且瞭解程式碼，將能從中學到更多。

## 關於 Launch

Adobe Experience Platform Launch是Adobe提供的新一代網站標籤和行動SDK管理功能。 Launch為客戶提供簡單的方式，來部署和管理所有必要的分析、行銷和廣告解決方案，以推動相關的客戶體驗。 Launch不需額外付費。 它適用於任何Adobe Experience cloud客戶。

針對網站的啟動可讓您集中管理案頭和行動網站上使用之分析、行銷和廣告解決方案的所有JavaScript。 例如，如果您部署Adobe Analytics,Launch將會管理AppMeasurement javaScript程式庫、填入變數和觸發請求。

Launch容器標籤比DTM輕60%，比Google Tag Manager輕40%。 容器的內容皆經過適當縮製，包括自訂程式碼。一切皆採取模組化。如果您不需要某個項目，就不必將該項目納入程式庫。如此可使實作流程更加快速和精簡。

Launch也是一個平台，可讓協力廠商建立擴充功能，以便透過Launch輕鬆部署其解決方案。 擴充功能是擴充Launch UI和用戶端功能的程式碼套件（JavaScript、HTML和CSS）。 您可以將 Launch 想像成一個作業系統，而延伸模組則是您用來完成工作的應用程式。

## 關於課程

在這些課程中，您將將Adobe Experience cloud實作至名為Luma的假零售網站。 Luma網 [站擁有豐富的資料層](https://luma.enablementadobe.com/content/luma/us/en.html) ，並具備可讓您建立實際實作的功能。 您將在您自己的Experience cloud組織中建立自己的Launch屬性，並使用Experience cloud除錯程式將其對應至我們代管的Luma網站。

[![Luma網站](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

## 取得工具

1. Because you will be using some browser-specific extensions, we recommend completing the tutorial using the [Chrome Web Browser](https://www.google.com/chrome/)
1. Add the [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) extension to your Chrome browser
1. Download the [sample html page](https://www.enablementadobe.com/multi/web/basic-sample.html) (right-click on this link and click "Save Link As")
1. 取得文字編輯器，您可在其中變更範例html頁面。 (如果您沒有，建議您試用 [Brackets](http://brackets.io/))
1. 為Luma網站 [建立書籤](https://luma.enablementadobe.com/content/luma/us/en.html)

>[!NOTE] 在Chrome中開啟的Luma網站中，當您閱讀本教學課程並在不同的瀏覽器中完成啟動介面步驟時，可能會發現完成本教學課程會更輕鬆。

開始吧！

[下一個「建立啟動屬性」&gt;](launch.md)