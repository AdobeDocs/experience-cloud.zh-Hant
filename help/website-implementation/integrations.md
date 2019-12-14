---
title: 與Launch實作Experience cloud整合
description: 瞭解如何驗證Adobe Experience cloud實作中的「觀眾」、「A4T」和「客戶屬性」整合。 本課程是「使用Launch在網站中實作Experience cloud」教學課程的一部分。
seo-description: null
seo-title: 與Launch實作Experience cloud整合
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: e9dee6d0aa3b775d0ce617e2b2c57b56de491b8d

---


# Experience Cloud 整合

在本課中，您將檢閱您剛實作之解決方案之間的主要整合。 好消息是，完成先前的課程後，您就已實作整合的程式碼部分！ 除了閱讀和驗證外，您不需要在本課程中做任何額外的工作。

## 學習目標

在本課程結束時，您將能夠:

1. 說明「觀眾共用」、「Analytics for Target」(A4T)和「客戶屬性」整合的基本使用案例
1. 驗證這些整合的基本用戶端實施環節

## 必要條件

您應先完成本教學課程中的所有先前課程，然後再依照本課程中的指示進行。

>[!NOTE]  若要完整使用這些整合，有許多必要的使用者權限需求、帳戶設定，以及佈建步驟，這些不在本教學課程的討論範圍內。如果您目前的Experience cloud實作中尚未使用這些整合，請考慮下列事項：
>
> * 檢視[核心服務整合](https://docs.adobe.com/content/help/en/core-services/interface/about-core-services/core-services.html)的完整需求
> * 檢視 [Analytics for Target 整合](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/before-implement.html)的完整需求
> * Have an Administrator of your Experience Cloud Organization [request provisioning of these integrations](https://www.adobe.com/go/audiences)


## 受眾

[Audiences](https://docs.adobe.com/content/help/en/core-services/interface/audiences/audience-library.htm) 是People Core service的一部分，可讓您在解決方案之間共用觀眾。 例如，您可以在Audience manager中建立觀眾，並使用它透過Target傳遞個人化內容。

實施A4T（您已經做過）的主要要求是：

1. 實作Adobe Experience Platform Identity Service
1. 實作Audience Manager
1. 實作您想要接收或建立觀眾的其他解決方案，例如Target和Analytics

### 驗證「觀眾」整合

驗證「對象」整合的最佳方式是實際建立對象，將其共用給其他解決方案，然後在其他解決方案中充分使用（例如，確認符合AAM區段資格的訪客可符合該區段目標活動的資格）。 不過，這不在本教學課程的討論範圍內。

這些驗證步驟將著重於用戶端實作中可見的關鍵部分——訪客ID。

1. Open the [Luma site](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Make sure the Debugger is mapping the Launch property to *your* Development environment, as described in the [earlier lesson](launch-switch-environments.md)

   ![Debugger中顯示的Launch開發環境](images/switchEnvironments-debuggerOnWeRetail.png)

1. 轉到調試器的「網路」頁籤

1. 按一 **[!UICONTROL 下「清除所有請求]** 」，只要清除

1. 重新載入Luma頁面，確保您在除錯程式中同時看到Target和Analytics請求

1. 再次重新載入Luma頁

1. 您現在應會在除錯程式的「網路」索引標籤中看到四個請求——兩個用於Target，兩個用於Analytics

1. 查看標示「Experience cloud訪客ID」的列。 所有解決方案的所有要求中的 ID 應一律相同。

   ![確認匹配的SDID](images/integrations-matchingECIDs.png)

1. 每個訪客的 ID 皆為唯一，您可以請同事執行這些步驟以進行確認。

## 目標分析 (A4T)

The [Analytics for Target (A4T)](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html) integration allows you to leverage your Analytics data as the source for reporting metrics in Target.

實施A4T（您已經做過）的主要要求是：

1. 實作Adobe Experience Platform Identity Service
1. 在Analytics頁面檢視信標之前觸發Target頁面載入請求

A4T的運作方式是將Target的伺服器端要求與Analytics頁面檢視信標（我們稱為「點擊拼接」）相結合。  「點擊接合」要求傳送活動的Target請求（或遞增Target型目標量度）具有與Analytics頁面檢視信標中的參數相符的參數。 此參數稱為補充資料ID(SDID)。

### 驗證 A4T 實施

驗證A4T整合的最佳方式，是實際使用A4T建立Target活動並驗證報告資料，但這超出本教學課程的範圍。 本教學課程將示範如何確認補充資料ID在解決方案呼叫之間是否相符。

**驗證SDID**

1. Open the [Luma site](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Make sure the Debugger is mapping the Launch property to *your* Development environment, as described in the [earlier lesson](launch-switch-environments.md)

   ![Debugger中顯示的Launch開發環境](images/switchEnvironments-debuggerOnWeRetail.png)

1. 轉到調試器的「網路」頁籤

1. 按一 **[!UICONTROL 下「清除所有請求]** 」，只要清除

1. 重新載入Luma頁面，確保您在除錯程式中同時看到Target和Analytics請求

1. 再次重新載入Luma頁

1. 您現在應會在除錯程式的「網路」索引標籤中看到四個請求——兩個用於Target，兩個用於Analytics

1. 查看標示為「Supplemental Data ID」的這一列。第一個頁面載入的ID應與Target和Analytics之間的ID相符。 來自第二個頁面載入的 ID 也應彼此相符，但與來自第一個頁面載入的 ID 不同。

   ![確認匹配的SDID](images/integrations-matchingSDIDs.png)

如果您在屬於A4T活動的頁面載入範圍（不包括單頁應用程式）中提出其他Target請求，請為其指定唯一名稱（非target-global-mbox），如此他們就能繼續擁有初始Target和Analytics請求的相同SDID。

## 客戶屬性

[「客戶屬性](https://docs.adobe.com/content/help/en/core-services/interface/customer-attributes/attributes.html) 」是「人員核心服務」的一部分，可讓您從客戶關係管理(CRM)資料庫上傳資料，並在Adobe Analytics和Adobe Target中運用。

實施客戶屬性（您已經完成）的主要要求是：

1. 實作Adobe Experience Platform Identity Service
1. Set Customer Ids via the Id Service *before* Target and Analytics fire their requests (which you accomplished using the rule ordering feature in Launch)

### 驗證客戶屬性實作

您已經驗證客戶ID已同時傳遞至Identity service和Target。 您也可以在Analytics點擊中驗證客戶ID。
目前，客戶ID是Experience cloud除錯程式中未顯示的少數參數之一，因此您將使用瀏覽器的JavaScript Console來檢視它。

1. 開啟Luma網站
1. 開啟您瀏覽器的開發人員工具
1. 轉到「網路」頁籤
1. 在篩選欄位中，輸 `b/ss` 入可限制您看到Adobe Analytics請求的內容

   ![開啟「開發人員工具」並篩選「網路」標籤，以僅顯示Analytics請求](images/aam-openTheJSConsole.png)

1. 按一 **[!UICONTROL 下網站右上角]** LOGIN連結

   ![按一下頂端導覽中的登入](images/idservice-loginNav.png)

1. 輸入 `test@adobe.com` 為用戶名
1. 輸入 `test` 為密碼
1. 按一下「 **[!UICONTROL LOGIN]** （登錄）」按鈕

   ![輸入認證並按一下登入](images/idservice-login.png)

1. 它應會將您返回首頁，而首頁也會觸發您在「開發人員工具」中可看到的信標。 如果您進入帳戶資訊頁面，請按一下WE.RETAIL標誌以返回首頁。
1. 按一下請求並選取「標題」標籤
1. 向下捲動，直到您看到某些巢狀參數為止
   1. cid —— 這是請求「客戶ID」部分的標準分隔字元
   1. crm_id —— 這是您在Identity service課程中指定的自訂整合代碼
   1. id —— 來自您資料元素的客戶ID `Email (Hashed)` 值
   1. as —— 驗證狀態，"1"表示已登錄
   ![Analytics客戶ID驗證](images/integrations-analyticsCustomerIDValidation.png)

[下一個「發佈您的屬性」&gt;](publish.md)