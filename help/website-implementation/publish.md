---
title: 發佈您的啟動屬性
description: 瞭解如何將您的Launch屬性從開發環境發佈至測試和生產環境。 本課程是「使用Launch在網站中實作Experience cloud」教學課程的一部分。
seo-description: null
seo-title: 發佈您的啟動屬性
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: aacd691c176da6ae5b247a19051de57289c128c5

---


# 發佈您的啟動屬性

現在，您已在您的開發環境中實作了一些Adobe Experience cloud的主要解決方案，您該學習發佈工作流程了。

## 學習目標

在本課程結束時，您將能夠:

1. 將開發程式庫發佈到測試環境
1. 使用除錯程式將測試程式庫對應至您的生產網站
1. 將測試程式庫發佈到生產環境

## 發佈到測試環境

現在您已在開發環境中建立並驗證您的程式庫，是時候將它發佈至測試版了。

1. Go to the **[!UICONTROL Publishing]** page

1. 開啟您資料庫旁的下拉式清單，並選取「 **[!UICONTROL 送出以供核准」]**

   ![提交以進行核准](images/publishing-submitForApproval.png)

1. 在對話方 **[!UICONTROL 塊中]** ，按一下「提交」按鈕：

   ![在模型中按一下「提交」](images/publishing-submit.png)

1. 您的資料庫現在會以未建置的 [!UICONTROL 狀態] ，出現在「已提交」欄中：

1. 開啟下拉式清單，然後選 **[!UICONTROL 取「階段建置」]**:

   ![建置以測試](images/publishing-buildForStaging.png)

1. 綠點圖示顯示之後，即可在測試環境中預覽程式庫。

在實際案例中，此程序的下一步通常是讓 QA 團隊在測試程式庫中驗證變更。他們可以使用除錯程式來執行此動作。

**驗證測試庫中的更改**

1. 在您的Launch屬性中，開啟「環 [!UICONTROL 境] 」頁

1. 在「 [!UICONTROL 測試] 」列中，按一下「安裝」圖示 ![「安裝」圖示](images/launch-installIcon.png) ，以開啟模式

   ![前往「環境」頁面，然後按一下以開啟模式](images/publishing-getStagingCode.png)

1. 按一下「複製」圖 ![示「複製](images/launch-copyIcon.png) 」圖示，將內嵌代碼複製到剪貼簿

1. Click **[!UICONTROL Close]** to close the modal

   ![安裝圖示](images/publishing-copyStagingCode.png)

1. Open the [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html) in your Chrome browser

1. 按一下「 [Debugger圖示」圖示](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) ，開啟 ![Experience Cloud Debugger擴充功能](images/icon-debugger.png)

   ![按一下「除錯程式」圖示](images/switchEnvironments-openDebugger.png)

1. 前往「工具」標籤

1. 按一 **** 下「Adobe Launch &gt;動態插入啟動&gt;內嵌代碼」按鈕，以開啟文字輸入欄位（它目前可能有您的開發內嵌代碼的URL）:

   ![按一下「Adobe Launch &gt;動態插入啟動&gt;內嵌代碼」按鈕](images/switchEnvironments-debugger-editEmbedCode.png)

1. 貼上剪貼簿中的「測試內嵌」代碼

1. 按一下磁碟圖示以儲存

   ![Debugger中顯示的啟動環境](images/switchEnvironments-debugger-save.png)

1. 重新載入並勾選除錯程式的「摘要」標籤。 在「啟動」區段下，您現在應會看到您的「測試屬性」已實作，並顯示您的屬性名稱(例如「啟動教學課程」或您為屬性命名的任何內容)!

   ![Debugger中顯示的啟動環境](images/publishing-debugger-staging.png)

在現實中，一旦您的QA團隊通過查看測試環境中的更改而簽約後，就應該發佈到生產環境。

## 發佈到生產環境

1. Go to the [!UICONTROL Publishing] page

1. 從下拉式清單中，按一下「 **[!UICONTROL 核准發佈]**:

   ![核准以發佈](images/publishing-approveForPublishing.png)

1. 在對話方 **[!UICONTROL 塊中]** ，按一下「核准」按鈕：

   ![按一下「核准」](images/publishing-approve.png)

1. 程式庫現在會以未建立狀態( [!UICONTROL 黃色圓點] )出現在「已核准」欄中：

1. 開啟下拉式清單並選 **[!UICONTROL 取**建立並發佈至生產]**:

   ![按一下「建立並發佈至生產」](images/publishing-buildAndPublishToProduction.png)

1. 在對話 **[!UICONTROL 方塊中]** ，按一下「發佈」:

   ![按一下「發佈」](images/publishing-publish.png)

1. 程式庫現在會出現在「已發 [!UICONTROL 布」欄] :

   ![已發佈](images/publishing-published.png)

就這樣！ 您已完成教學課程，並在Launch！中發佈了您的第一個屬性！