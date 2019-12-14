---
title: 建立行動應用程式的啟動屬性
description: 瞭解如何登入Launch介面並建立行動Launch屬性。 本課是「在Mobile android應用程式中實作Experience cloud」教學課程的一部分。
seo-description: null
seo-title: 建立行動應用程式的啟動屬性
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: 7166d2933cc99bcbbd4713fba8f87fb0826b711e

---


# 建立啟動屬性

Adobe Experience Platform Launch是新一代的行動SDK和網站標籤管理功能。 Launch為客戶提供簡單的方式，來部署和管理所有必要的分析、行銷和廣告解決方案，以推動相關的客戶體驗。 Launch不需額外付費。 它可供任何Adobe Experience cloud客戶使用。

在本課中，您將為行動應用程式建立Launch屬性。

## 必要條件

為了完成下幾堂課，您必須擁有在Launch中開發、核准、發佈、管理擴充功能和管理環境的權限。 如果您因為使用者介面選項不適用而無法完成上述任何步驟，請連絡您的Experience cloud管理員以要求存取權。 For more information on Launch permissions, see [the documentation](https://docs.adobe.com/content/help/en/launch/using/reference/admin/user-permissions.html).

## 學習目標

在本課程結束時，您將能夠:

* 登入Launch使用者介面
* 建立新的Launch Mobile屬性
* 設定Launch Mobile屬性

## 前往 Launch

**若要開始使用**

1. 登入 [Adobe Experience Cloud](https://experiencecloud.adobe.com)

1. 按一下「解 ![決方案切換器圖示](images/mobile-launch-solutionSwitcher.png) 」圖示以開啟解決方案切換器

1. Select **[!UICONTROL Launch]** from the menu

   ![使用圖示開啟解決方案切換器，然後按一下「啟動」](images/mobile-launch-solutionSwitcherActivation.png)

1. 在「 **[!UICONTROL Adobe Experience Cloud Launch]**」下方，按一下「 **[!UICONTROL 跳至Launch」按鈕]**

   ![按一下「啟動」按鈕](images/mobile-launch-goToLaunch.png)

You should now see the `Properties` screen (if no properties have ever been created in the account, this screen might be empty):

![屬性畫面](images/mobile-launch-propertiesScreen.png)

如果您經常使用Launch，您也可以將下列URL建立書籤並直接登入 [https://launch.adobe.com](https://launch.adobe.com)

## 建立屬性

屬性基本上就是容器，當您將標籤部署至應用程式時，會填入擴充功能、規則、資料元素和程式庫。 單一行動裝置屬性可用於多個應用程式平台（例如iOS和Android），前提是應用程式包含類似的功能，並需要建置相同的解決方案。  如需建立屬性的詳細資訊，請 [參閱產品檔案中的「設定行動裝置屬性](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property) 」。

**建立屬性**

1. 按一下「 **[!UICONTROL New Property]** （新建屬性）」按鈕：

   ![按一下「新增屬性」](images/mobile-launch-addNewProperty.png)

1. 命名您的屬性(例如 `Mobile Tutorial`)
1. 在平台上，按一下 **[!UICONTROL Mobile]**
1. 按一下「 **[!UICONTROL 儲存]** 」按鈕

   ![建立新屬性](images/mobile-launch-newProperty.png)

您的新屬性應顯示在「屬性」頁面上。 Note that if you check the box next to the property name, options to **[!UICONTROL Configure]** or **[!UICONTROL Delete]** the property appear above the property list. 按一下您屬性的名稱(例如 `Mobile Tutorial`)開啟畫 `Overview` 面。
![按一下屬性名稱以開啟它](images/mobile-launch-openProperty.png)

[下一個「新增擴充功能」&gt;](launch-add-extensions.md)
