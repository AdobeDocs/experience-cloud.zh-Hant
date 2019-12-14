---
title: 透過Launch實作Adobe Audience Manager
description: 瞭解如何使用伺服器端轉送和啟動功能，在您的網站上實作Adobe Audience Manager。 本課是「在Mobile android應用程式中實作Experience cloud」教學課程的一部分。
seo-description: null
seo-title: 透過Launch實作Adobe Audience Manager
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: e9dee6d0aa3b775d0ce617e2b2c57b56de491b8d

---


# 新增Adobe Audience Manager

本課將引導您逐步實作Adobe Audience Manager至使用伺服器端轉送的Experience Platform Mobile SDK。

[Adobe Audience Manager](https://docs.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html) (AAM)提供領先業界的線上受眾資料管理服務，為數位廣告商和出版業者提供所需的工具，以控制並運用其資料資產，協助推動銷售成功。

## 學習目標

在本課程結束時，您將能夠:

1. 說明在行動應用程式中實作Audience manager的兩種主要方式
1. 使用Analytics信標的伺服器端轉送來新增Audience Manager
1. 驗證Audience manager實作

## 必要條件

要完成本課程，您需要：

1. 若要完成「設定啟動」區段下的課程，即「 [建立啟動屬性](launch-create-a-property.md)、新增擴充功能 [、建立程式庫](launch-add-extensions.md)，以及 [](launch-create-a-library.md)[](launch-install-the-mobile-sdk.md)安裝Mobile SDK Property」。

1. 管理員存取Adobe Analytics，以便您能夠針對您在本教學課程中使用的報表套裝啟用伺服器端轉送。 或者，您也可以請組織的現有管理員按照下列指示為您執行此操作。

## 實施選項

在應用程式中實作Audience manager有兩種方式：

* 伺服器端轉送(SSF)-對於使用Adobe Analytics的客戶，這是最簡單且建議的實作方式。 Adobe Analytics會將資料轉送至Adobe後端的AAM，因此您不需要直接從應用程式向Audience manager提出要求。 這也可啟用主要整合功能，並符合我們在Audience manager程式碼實作和部署方面的最佳實務。

* 用戶端DIL —— 此方法適用於沒有Adobe Analytics的客戶。 應用程式中的Audience manager方法會直接將資料傳送至Audience Manager。 在此情況下，當您設定行動啟動屬性時，會在Launch中使用Audience Manager擴充功能。

當您先前在本教學課程的「新增擴充功能 [](launch-add-extensions.md) 」區段中設定Analytics擴充功能時，已勾選此方塊，以啟動從Analytics將資料從伺服器端轉送至Audience Manager的程式。 這會將處理Audience manager區段回應所需的程式碼動態插入您的應用程式。 我們不會在本教學課程中新增Audience Manager擴充功能，因為這僅適用於您沒有Adobe Analytics的使用案例。

## 啟用伺服器端轉送

實施SSF有三個主要步驟：

1. 將Experience Cloud Mobile SDK和Analytics擴充功能新增至應用程式***中已在設定啟動課程中** 「完成」
1. 在Analytics擴充功能設定中啟用Audience Manager轉送， ***您在「新增擴充功能*** 」課程中只 [](launch-add-extensions.md) 要勾選方塊即可完成。
1. 在Analytics管理控制台中開啟「切換」，將資料從Analytics轉送至每個報表套裝的Audience Manager **，我們將在本課的其餘章節中檢閱。

### 在 Analytics Admin Console 中啟用伺服器端轉送

必須具備Adobe Analytics管理控制台中的設定，才能開始將資料從Adobe Analytics轉送至Adobe Audience Manager。 請注意，系統最多需要4小時才能開始轉發資料，因此在排除轉發故障時請記住這一點。

#### 在Analytics管理控制台中啟用SSF

1. 透過Experience Cloud UI登入Analytics。 如果您沒有Analytics的管理員存取權，則需要與Experience cloud或Analytics管理員聯絡，以指派存取權或完成這些步驟。

   ![登入Adobe Analytics UI](images/mobile-aam-logIntoAnalytics.png)

1. 從Analytics的頂端導覽中，選擇「 **[!UICONTROL 管理&gt;報表套裝」]**，然後從清單中選取（或多選）您要轉送至Audience Manager的報表套裝。

   ![按一下至「管理控制台」](images/mobile-aam-analyticsAdminConsoleReportSuites.png)

1. 從「報表套裝」螢幕中，在選取報表套裝後，選擇「編輯設 **[!UICONTROL 定&gt;一般&gt;伺服器端轉送」]**。

   ![選擇SSF菜單](images/mobile-aam-selectSSFmenu.png)

   >[!WARNING]  如上所述，您必須有管理員權限才能看到此功能表項目。

1. 在「伺服器端轉送」頁面上，閱讀資訊並核取該方塊，以 **[!UICONTROL 啟用報表套裝的伺服器端轉送]** 。

1. Click **[!UICONTROL Save]**

   ![完成SSF設定](images/mobile-aam-enableSSFcomplete.png)

>[!NOTE] 由於每個報表套裝都需要啟用SSF，所以在實際應用程式的報表套裝中部署SSF時，請記得對實際報表套裝重複此步驟。
>
>此外，如果SSF選項呈灰色，您將需要「將報表套裝對應至您的Experience cloud組織，以啟用此選項。 這在[文件](https://docs.adobe.com/content/help/en/core-services/interface/about-core-services/report-suite-mapping.html)中皆有說明。

只要您已實作Adobe Experience Platform Identity Service，此交換機就會開始將資料實際轉送至AAM。 其餘的SSF實作會在程式碼中進行，當您勾選Analytics擴充功能中的方塊以轉送至AAM時，就會在Launch中處理。

伺服器端轉送代碼現在已實作給您的應用程式！

[下一個「發佈您的屬性」&gt;](publish.md)