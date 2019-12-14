---
title: 建立啟動屬性
description: 瞭解如何登入Launch介面並建立Launch屬性。 本課程是「使用Launch在網站中實作Experience cloud」教學課程的一部分。
seo-description: null
seo-title: 建立啟動屬性
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: 7166d2933cc99bcbbd4713fba8f87fb0826b711e

---


# 建立啟動屬性

在本課中，您將建立您的第一個Launch屬性。

屬性基本上是個容器，當您將標籤部署至網站時，在其中裝入擴充功能、規則、資料元素和程式庫。

## 必要條件

為了完成下幾堂課，您必須擁有在Launch中開發、核准、發佈、管理擴充功能和管理環境的權限。 如果您因為使用者介面選項不適用而無法完成上述任何步驟，請連絡您的Experience cloud管理員以要求存取權。 For more information on Launch permissions, see [the documentation](https://docs.adobe.com/content/help/en/launch/using/reference/admin/user-permissions.html).

## 學習目標

在本課程結束時，您將能夠:

* 登入Launch使用者介面
* 建立新的啟動屬性
* 設定啟動屬性

## 前往 Launch

**若要開始使用**

1. 登入 [Adobe Experience Cloud](https://experiencecloud.adobe.com)

1. 按一下「解 ![決方案切換器圖示](images/launch-solutionSwitcher.png) 」圖示以開啟解決方案切換器

1. 從選 **[!UICONTROL 單中選取]** 「啟動」使 ![用圖示開啟解決方案切換器，然後按一下「啟動」](images/launch-solutionSwitcherActivation.png)

1. 在「 **[!UICONTROL Adobe Experience Cloud Launch]**」下方，按一下「 **[!UICONTROL 跳至Launch」按鈕]**

   ![按一下「啟動」按鈕](images/launch-goToLaunch.png)

You should now see the `Properties` screen (if no properties have ever been created in the account, this screen might be empty):

![屬性畫面](images/launch-propertiesScreen.png)

如果您經常使用Launch，您也可以將下列URL建立書籤並直接登入 [https://launch.adobe.com](https://launch.adobe.com)

## 建立屬性

屬性基本上是個容器，當您將標籤部署至網站時，在其中裝入擴充功能、規則、資料元素和程式庫。 屬性可以是一或多個網域和子網域的任何群組。同樣地，您可以管理及追蹤這些資產。例如，假設您有多個網站是根據同一個範本，且想要追蹤這所有網站上的相同資產。您可以將一個 屬性套用到多個網域。如需建立屬性的詳細資訊，請參 [閱產品檔案中的](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html) 「公司與屬性」。

**建立屬性**

1. 按一下「 **[!UICONTROL New Property]** （新建屬性）」按鈕：

   ![按一下「新增屬性」](images/launch-addNewProperty.png)

1. 命名您的屬性(例如 `Launch Tutorial` 或 `Daniel's Launch Tutorial`)
1. 作為域，輸入 `enablementadobe.com` ，因為這是Luma演示站點托管的域。 雖然「網域」欄位是必填欄位，但Launch屬性將可用於實施網域的任何網域。 此欄位的主要用途是在規則產生器中預先填入功能表選項。
1. 按一下「 **[!UICONTROL 儲存]** 」按鈕

   ![建立新屬性](images/launch-newProperty.png)

您的新屬性應顯示在「屬性」頁面上。 Note that if you check the box next to the property name, options to **[!UICONTROL Configure]** or **[!UICONTROL Delete]** the property appear above the property list. 按一下您屬性的名稱(例如 `Launch Tutorial`)開啟畫 `Overview` 面。
![按一下屬性名稱以開啟它](images/launch-openProperty.png)

[下一個「新增啟動內嵌代碼」&gt;](launch-add-embed.md)
