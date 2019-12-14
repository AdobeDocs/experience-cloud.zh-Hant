---
title: 使用Adobe Experience cloud除錯程式切換啟動環境
description: 瞭解如何使用Experience cloud除錯程式來載入不同的Launch內嵌代碼。 本課程是「使用Launch在網站中實作Experience cloud」教學課程的一部分。
seo-description: null
seo-title: 使用Adobe Experience cloud除錯程式切換啟動環境
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: 79d5274d09d66b80a49aba5db3e0a997d0f0ff61

---


# 使用Experience cloud除錯程式切換啟動環境

In this lesson you will use the [Adobe Experience Cloud Debugger extension](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) to replace the Launch property hardcoded on the [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html) with your own property.

此技術稱為環境切換，日後當您在自己的網站上使用Launch時，將會有所幫助。 您可以在瀏覽器中載入生產網站，但可搭配您的開發 *Launch環境* 。 這可讓您放心地進行和驗證Launch變更，而不受一般程式碼版本的限制。  畢竟，將行銷標籤發行與一般程式碼發行分開，是客戶首先使用Launch的主要原因之一！

## 學習目標

在本課程結束時，您將能夠:

* 使用除錯程式載入替代的啟動環境
* 使用除錯程式來驗證您是否已載入替代的啟動環境

## 取得您的開發環境的URL

1. In your Launch property, open the `Environments` page

1. In the **[!UICONTROL Development]** row, click the Install icon ![Install icon](images/launch-installIcon.png) to open the modal

1. 按一下「複製」圖 ![示「複製](images/launch-copyIcon.png) 」圖示，將內嵌代碼複製到剪貼簿

1. Click **[!UICONTROL Close]** to close the modal

   ![安裝圖示](images/launch-copyInstallCode.png)

## 取代Luma展示網站上的啟動URL

1. Open the [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html) in your Chrome browser

1. 按一下「 [Debugger圖示」圖示](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) ，開啟 ![Experience Cloud Debugger擴充功能](images/icon-debugger.png)

   ![按一下「除錯程式」圖示](images/switchEnvironments-openDebugger.png)

1. 請注意，目前實作的Launch屬性會顯示在「摘要」標籤上

   ![Debugger中顯示的啟動環境](images/switchEnvironments-debuggerOnWeRetail-prod.png)

1. 前往「工具」標籤

1. 捲動至「取代啟 **[!UICONTROL 動內嵌代碼」一節]**

1. 請確定Luma網站的Chrome標籤位於除錯程式的後面（而非本教學課程的標籤或Launch介面的標籤）。  將剪貼簿中的內嵌代碼貼入輸入欄位

1. 切換「套用至luma.enablementadobe.com」功能，讓Luma網站上的所有頁面都對應至您的Launch屬性

1. 按一下「 **[!UICONTROL 儲存]** 」按鈕

   ![Debugger中顯示的啟動環境](images/switchEnvironments-debugger-save.png)

1. 重新載入Luma網站並勾選除錯程式的「摘要」標籤。 在「啟動」區段下，您現在應會看到您的開發屬性正在使用中。 確認屬性的名稱與您的名稱相符，且環境會顯示「開發」。

   ![Debugger中顯示的啟動環境](images/switchEnvironments-debuggerOnWeRetail.png)

>[!NOTE] 每當您回到Luma網站時，除錯程式會儲存此設定並取代Launch內嵌代碼。 它不會影響您在其他開啟標籤中造訪的其他網站。 To stop the Debugger from replacing the embed code, click the **[!UICONTROL Remove]** button next to the embed code in the Tools tab of the Debugger.

在繼續教學課程時，您將使用此技巧將Luma網站對應至您自己的Launch屬性，以驗證您的Launch實作。 當您在生產網站上開始使用Launch時，可以使用相同的技巧來驗證變更。

[接下來的「新增Adobe Experience Platform Identity Service」&gt;](id-service.md)