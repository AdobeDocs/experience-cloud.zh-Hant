---
title: 透過Launch實作Adobe Audience Manager
description: 瞭解如何使用伺服器端轉送和啟動功能，在您的網站上實作Adobe Audience Manager。 本課程是「使用Launch在網站中實作Experience cloud」教學課程的一部分。
seo-description: null
seo-title: 透過Launch實作Adobe Audience Manager
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: e9dee6d0aa3b775d0ce617e2b2c57b56de491b8d

---


# 新增Adobe Audience Manager

本課將引導您完成啟用「伺服器端轉送」Adobe Audience Manager的步驟。

[Adobe Audience Manager](https://docs.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html) (AAM)提供領先業界的線上受眾資料管理服務，為數位廣告商和出版業者提供所需的工具，以控制並運用其資料資產，協助推動銷售成功。

## 學習目標

在本課程結束時，您將能夠:

1. 說明在網站中實作Audience manager的兩種主要方式
1. 使用Analytics信標的伺服器端轉送來新增Audience Manager
1. 驗證Audience manager實作

## 必要條件

要完成本課程，您需要：

1. 若要完成「設定啟 [動」、「新增Adobe Analytics](launch.md)」和「 [新增Identity Service」的課程](analytics.md)[](id-service.md)。

1. 管理員存取Adobe Analytics，以便您能夠針對您在本教學課程中使用的報表套裝啟用伺服器端轉送。 或者，您也可以請組織的現有管理員按照下列指示為您執行此操作。

1. 您的「Audience Manager子網域」（也稱為「合作夥伴名稱」「合作夥伴ID」或「合作夥伴子網域」）。 如果您已在實際網站上實作Audience Manager，取得Audience Manager最簡單的方法就是前往實際網站並開啟除錯程式。 子網域可在「摘要」標籤的「觀眾管理員」區段中使用：

   ![您可以使用除錯程式在實際網站上尋找Audience manager子網域](images/aam-debugger-partner.png)

如果您尚未實作Audience Manager，請依照下列指示取得 [Audience Manager子網域](https://docs.adobe.com/content/help/en/audience-manager-learn/tutorials/web-implementation/how-to-identify-your-partner-id-or-subdomain.html)。

## 實施選項

在網站中實作Audience manager有兩種方式：

* **伺服器端轉送(SSF)**—對於使用Adobe Analytics的客戶，這是最簡單且建議的實作方式。 Adobe Analytics會將資料轉送至Adobe後端的AAM，讓頁面上的要求減少一次。 這也可啟用主要整合功能，並符合我們在Audience manager程式碼實作和部署方面的最佳實務。

* **用戶端DIL**—— 此方法適用於沒有Adobe Analytics的客戶。 DIL程式碼（資料整合程式庫程式碼，AAM javaScript組態程式碼）會直接從網頁將資料傳送至Audience Manager。

由於您在本教學課程中已部署Adobe Analytics，因此您將使用伺服器端轉送來部署Audience Manager。 For a complete description and requirements list for Server-Side forwarding, please review the [documentation](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/server-side-forwarding/ssf.html), so that you are familiar with how it works, what is required, and how to validate.

## 啟用伺服器端轉送

執行SSF實施有兩個主要步驟：

1. 在Analytics管理控制台中開啟「切換」，將資料從Analytics轉送至每個報表套裝 *的Audience Manager*。
1. 將程式碼放置到位，透過Launch完成。 為了讓此功能正常運作，您需要安裝Adobe Experience Platform Identity Service擴充功能以及Analytics擴充功能(您實際上不需要 ** AAM擴充功能，請見下文說明)。

### 在 Analytics Admin Console 中啟用伺服器端轉送

必須具備Adobe Analytics管理控制台中的設定，才能開始將資料從Adobe Analytics轉送至Adobe Audience Manager。 由於開始轉送資料可能需要4小時，因此您應先執行此步驟。

#### 在Analytics管理控制台中啟用SSF

1. 透過Experience Cloud UI登入Analytics。 如果您沒有Analytics的管理員存取權，則需要與Experience cloud或Analytics管理員聯絡，以指派存取權或完成這些步驟。

   ![登入Adobe Analytics](images/aam-logIntoAnalytics.png)

1. 從Analytics的頂端導覽中，選擇「管 **[!UICONTROL 理&gt;報表套裝]**」，然後從清單中選擇（多選）您要轉送至Audience Manager的報表套裝。

   ![按一下至「管理控制台」](images/aam-analyticsAdminConsoleReportSuites.png)

1. 從「報表套裝」螢幕中，在選取報表套裝後，選擇「編輯設 **[!UICONTROL 定&gt;一般&gt;伺服器端轉送」]**。

   ![選擇SSF菜單](images/aam-selectSSFmenu.png)

   >[!WARNING]  如上所述，您必須有管理員權限才能看到此功能表項目。

1. 在「伺服器端轉送」頁面上，閱讀資訊並核取該方塊，以 **[!UICONTROL 啟用報表套裝的伺服器端轉送]** 。

1. Click **[!UICONTROL Save]**

   ![完成SSF設定](images/aam-enableSSFcomplete.png)

>[!NOTE] 由於每個報表套裝都需要啟用SSF，所以在實際網站的報表套裝上部署SSF時，請記得對實際報表套裝重複此步驟。
>
>此外，如果SSF選項呈灰色，您將需要「將報表套裝對應至您的Experience cloud組織，以啟用此選項。 這在[文件](https://docs.adobe.com/content/help/en/core-services/interface/about-core-services/report-suite-mapping.html)中皆有說明。

完成此步驟後，如果您啟用Adobe Experience Platform Identity Service，資料將從Analytics轉送至AAM。 不過，若要完成程式，讓回應從AAM正確返回至頁面（以及透過「對象分析」功能傳回至Analytics），您也必須在Launch中完成下列步驟。 別擔心，很簡單。

### 在 Launch 中啟用伺服器端轉送

這是啟用SSF的兩個步驟中的第二個步驟。 您已在Analytics管理控制台中翻轉開關，現在您只需要新增程式碼，如果您只要勾選正確的方塊，Launch就會為您做這些。

>[!NOTE] 若要將Analytics資料的伺服器端轉送實作為AAM，我們實際上會在Launch中編輯／設定Analytics擴充功能， **而非** AAM擴充功能。 AAM擴充功能僅用於用戶端DIL實作，適用於沒有Adobe Analytics的使用者。 因此，當您傳送至Analytics擴充功能以設定此功能時，下列步驟是正確的。

#### 在Launch中啟用SSF

1. 前往「 **[!UICONTROL 擴充功能&gt;已安裝]** 」，然後按一下以設定Analytics擴充功能。

   ![設定Analytics擴充功能](images/aam-configAnalyticsExtension.png)

1. 展開部 `Adobe Audience Manager` 分

1. 核取方塊以「 **[!UICONTROL 自動與Audience manager共用Analytics資料」]**。 這會將Audience Manager的「模組」（程式碼）新增至Analytics實 `AppMeasurement.js` 作。

1. 新增您的「Audience Manager子網域」（也稱為「合作夥伴名稱」、「合作夥伴ID」或「合作夥伴子網域」）。 請依照下列指示 [取得您的Audience Manager子網域](https://docs.adobe.com/content/help/en/audience-manager-learn/tutorials/web-implementation/how-to-identify-your-partner-id-or-subdomain.html)。

1. 按一 **[!UICONTROL 下「儲存至程式庫並建立」]**

   ![配置SSF](images/aam-configLaunchSSF.png)

伺服器端轉送代碼現在已實作！

### 驗證伺服器端轉送

驗證伺服器端轉送是否已啟動並執行的主要方式，是查看您對任何Adobe Analytics點擊的回應。 我們一會兒再說。 同時，讓我們檢查一下其他一些可以幫助我們確保它以我們想要的方式運行。

#### 驗證代碼是否正確載入

Adobe Launch安裝的程式碼來處理轉送，尤其是AAM對頁面的回應，稱為Audience Manager「模組」。 我們可以使用Experience cloud除錯程式來確保它已載入。

1. 開啟Luma網站
1. 按一下瀏覽器中的除錯程式圖示，以開啟Experience cloud除錯程式
1. 在「摘要」標籤上，向下捲動至「分析」區段
1. Verify that **AudienceManagement** is listed under the Modules section

   ![在除錯程式中驗證AAM模組](images/aam-verifyAAMmodule.png)

#### 驗證 Debugger 中的合作夥伴 ID

接下來，我們也可以驗證除錯程式是否取得正確的「合作夥伴ID」（亦即「合作夥伴子網域」等）從程式碼中。

1. 在除錯程式中，但仍在「摘要」索引標籤上，向下捲動至「Audience Manager」區段
1. 在「合作夥伴」下驗證您的合作夥伴ID/子網域

   ![在除錯程式中驗證合作夥伴ID](images/aam-verifyPartnerID.png)

>[!WARNING] 您可能會注意到除錯程式的「Audience Manager」區段會參照「DIL」（即「資料整合庫」），通常會參照用戶端實作，而非我們在此實作的伺服器端方法。 事實是，AAM "Module"（用於此SSF方法）使用與用戶端DIL程式庫相同的許多程式碼，因此此除錯程式目前會依此類型報告。 如果您遵循本教學課程中的步驟，而此驗證區段中的其餘項目正確無誤，您可放心伺服器端轉送正常運作。

#### 驗證Analytics請求和回應

好吧，這才是關鍵。 如果您未從Analytics將資料從伺服器端轉送至Audience Manager，則Analytics信標（除2x2像素外）確實沒有回應。 不過，如果您正在執行SSF，則有些項目可在Analytics請求和回應中驗證，讓您知道它正常運作。
很遺憾，目前Experience cloud除錯程式不支援顯示對信標的回應。 因此，您應使用其他偵錯器／封包嗅探器，例如Charles proxy或瀏覽器的「開發人員工具」。

1. 在您的瀏覽器中開啟「開發人員工具」，並前往「網路」標籤
1. 在篩選欄位中，輸 `b/ss` 入可限制您看到Adobe Analytics請求的內容
1. 重新整理頁面以查看Analytics請求

   ![開啟開發人員工具](images/aam-openTheJSConsole.png)

1. 在Analytics信標（請求）中，尋找「回呼」參數。 它將設定為這樣： `s_c_il[1].doPostbacks`

   ![AA要求——回呼參數](images/aam-callbackParam.png)

1. 您將會收到Analytics信標的回應。 它將包含對doPostbacks的參照（在請求中呼叫），最重要的是，它應該有「stuff」物件。 AAM區段ID將會傳回至瀏覽器的位置。 如果您有「stuff」對象，SSF正在運行！

   ![AA響應——填充對象](images/aam-stuffObjectInResponse.png)

>[!WARNING] 小心錯誤的「成功」—如果有回應，而且一切似乎都在起作用， **請確定** ，您有「東西」。 如果您不這麼做，您可能會在回應中看到訊息，指出「狀態」:「成功」。 雖然這聽起來很瘋狂，但這實際上證明它不 **正確** 。 如果您看到這個，表示您已完成第二個步驟（Launch中的程式碼），但Analytics管理控制台（本節的第一個步驟）中的轉送尚未完成。 在此情況下，您需要確認您已在Analytics管理控制台中啟用SSF。 如果你有，而且還沒有4小時，請耐心等待。

![AA回應——錯誤成功](images/aam-responseFalseSuccess.png)

[下一個「Experience cloud整合」&gt;](integrations.md)