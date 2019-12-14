---
title: 發佈您的啟動屬性
description: 瞭解如何將您的Launch屬性從開發環境發佈至測試和生產環境。 本課是「在Mobile iOS Objective-C應用程式中使用Launch教學課程實作Experience Cloud」的一部分。
seo-description: null
seo-title: 發佈您的啟動屬性
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: 7166d2933cc99bcbbd4713fba8f87fb0826b711e

---


# 發佈您的啟動屬性

現在，您已在您的開發環境中實作了一些Adobe Experience cloud的主要解決方案，您該學習發佈工作流程了。

## 必要條件

您的Launch使用者帳戶需要「核准」和「發佈」的權限，才能完成本課程。 如果您因為使用者介面選項不適用而無法完成上述任何步驟，請連絡您的Experience cloud管理員以取得存取權。 For more information on Launch permissions, see [the documentation](https://docs.adobe.com/content/help/en/launch/using/reference/admin/user-permissions.html).

## 學習目標

在本課程結束時，您將能夠:

1. 將開發程式庫發佈到測試環境
1. 更新您的應用程式以載入不同的Launch環境
1. 將測試程式庫發佈到生產環境

## 發佈到測試環境

現在您已在開發環境中建立並驗證您的程式庫，是時候將它發佈至測試版了。

1. Go to the **[!UICONTROL Publishing]** page

1. 開啟您資料庫旁的下拉式清單，並選取「 **[!UICONTROL 送出以供核准」]**

   ![提交以進行核准](images/mobile-publishing-submitForApproval.png)

1. 在對話方 **[!UICONTROL 塊中]** ，按一下「提交」按鈕：

   ![在模型中按一下「提交」](images/mobile-publishing-submit.png)

1. 您的資料庫現在會以未建置的 [!UICONTROL 狀態] ，出現在「已提交」欄中：

1. 開啟下拉式清單，然後選 **[!UICONTROL 取「階段建置」]**:

   ![建置以測試](images/mobile-publishing-buildForStaging.png)
1. 綠點圖示顯示之後，即可在測試環境中預覽程式庫。

在實際案例中，此程序的下一步通常是讓 QA 團隊在測試程式庫中驗證變更。

**驗證測試庫中的更改**

1. 在您的Launch屬性中，開啟「環 [!UICONTROL 境] 」頁

1. 在「 [!UICONTROL 測試] 」列中，按一下「安裝」圖示

   ![安裝圖示](images/mobile-launch-installIcon.png) ，以開啟模式
   ![前往「環境」頁面，然後按一下以開啟模式](images/ios/objective-c/mobile-publishing-getStagingCode.png)

如果您的「測試」應用程式使用不同的工作區，您必須確定此工作區包含您在本教學課程中進行的所有Pod和應用程式更新。 目前，您的開發環境中安裝指示的唯一差異，是核心組態中的啟動參考，如上述螢幕擷取所強調。 您需要更新AppDelegate.h檔案中的對應行，並重建應用程式。

在現實中，一旦您的QA團隊通過查看測試環境中的更改而簽約後，就應該發佈到生產環境。

## 發佈到生產環境

1. Go to the [!UICONTROL Publishing] page

1. 從下拉式清單中，按一下「 **[!UICONTROL 核准發佈]**:

   ![核准以發佈](images/mobile-publishing-approveForPublishing.png)

1. 在對話方 **[!UICONTROL 塊中]** ，按一下「核准」按鈕：

   ![按一下「核准」](images/mobile-publishing-approve.png)

1. 程式庫現在會以未建立狀態( [!UICONTROL 黃色圓點] )出現在「已核准」欄中：

1. 開啟下拉式清單，然後選 **[!UICONTROL 取「建立並發佈至生產」]**:

   ![按一下「建立並發佈至生產」](images/mobile-publishing-buildAndPublishToProduction.png)

1. 在對話 **[!UICONTROL 方塊中]** ，按一下「發佈」:

   ![按一下「發佈」](images/mobile-publishing-publish.png)

1. 程式庫現在會出現在「已發 [!UICONTROL 布」欄] :

   ![已發佈](images/mobile-publishing-published.png)

同樣地，請注意，生產環境使用核心組態中的啟動參考，如下方螢幕擷取所強調。  如果您的「測試」應用程式使用不同的工作區，您必須確定此工作區包含您在本教學課程中進行的所有Pod和應用程式更新。
![前往「環境」頁面，然後按一下以開啟模式](images/ios/objective-c/mobile-publishing-getProductionCode.png)

>[!WARNING] 下次您變更Launch設定時，就需要在「開發」環境中建立新的「程式庫」。 請記住，新增和移除擴充功能需要更新應用程式本身。 請小心讓您的Launch環境和應用程式程式碼彼此同步，以避免發生問題。

就這樣！ 您已完成教學課程，並在Launch！中發佈了您的第一個行動裝置屬性。