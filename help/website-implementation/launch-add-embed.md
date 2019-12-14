---
title: 實作啟動內嵌代碼
description: 瞭解如何取得Launch屬性的內嵌代碼並在您的網站中實作。 本課程是「使用Launch在網站中實作Experience cloud」教學課程的一部分。
seo-description: null
seo-title: 實作啟動內嵌代碼
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: 14e46fa7d806f2713a69fe5d3a0a8c326de26d23

---


# 新增 Launch 內嵌程式碼

在本課中，您將實作Launch屬性的「開發」環境的非同步內嵌代碼。 在此過程中，您將瞭解Launch的兩個主要概念——環境和內嵌代碼。

## 學習目標

在本課程結束時，您將能夠:

* 取得Launch屬性的內嵌代碼
* 瞭解開發、測試和生產環境之間的差異
* 將Launch內嵌代碼新增至html檔案
* Explain the optimal location of the Launch embed code in relation to other code in the `<head>` of an html document

## 複製內嵌代碼

The embed code is a `<script>` tag that you put on your webpages to load and execute the logic you build in Launch. 如果您以非同步方式載入程式庫，瀏覽器會繼續載入頁面、擷取啟動程式庫並並行執行它。 在這種情況下，只會有一個內嵌程式碼，您會將其放在 `<head>` 中。(When Launch is deployed synchronously, there are two embed codes, one which you put in the `<head>` and another which you put before the `</body>`).

從屬性概述畫面中按一下 `Environments` 標籤以前往環境頁面。請注意，您已預先建立開發、測試和生產環境。

![按一下頂端導覽中的「環境」](images/launch-environments.png)

開發、測試和生產環境對應至程式碼開發和發佈程序中的典型環境。程式碼首先由開發人員在開發環境中編寫。 當開發人員完成其工作時，就會將其傳送至測試環境，讓 QA 和其他團隊進行審查。一旦QA和其他團隊滿意後，程式碼就會發佈至「生產」環境，這是您的訪客造訪您網站時所體驗到的公開環境。

Launch允許額外的開發環境，這對於同時有多位開發人員處理不同專案的大型組織非常有用。

這些是我們完成教學課程所需的唯一環境。 環境允許您在不同URL上托管不同的Launch程式庫工作版本，因此您可以安全地新增功能，並讓適當的使用者（例如開發人員、QA工程師、公眾等）使用這些功能在正確的時間。

現在，讓我們複製內嵌代碼：

1. In the **[!UICONTROL Development]** row, click the Install icon ![Install icon](images/launch-installIcon.png) to open the modal.

1. 請注意，Launch將預設為非同步內嵌代碼

1. 按一下「複製」圖 ![示「複製](images/launch-copyIcon.png) 」圖示，將內嵌代碼複製到剪貼簿。

1. Click **[!UICONTROL Close]** to close the modal.

   ![安裝圖示](images/launch-copyInstallCode.png)

## Implement the Embed Code in the `<head>` of the Sample HTML Page

The embed code should be implemented in the `<head>` element of all HTML pages that will share the property. You might have one or several template files which control the `<head>` globally across the site, making it a straightforward process to add Launch.

如果您尚未下載範例html頁 [面](https://www.enablementadobe.com/multi/web/basic-sample.html) （在此連結上按一下滑鼠右鍵，然後按一下「另存連結為」），然後在程式碼編輯器中開啟它。 [Brackets](http://brackets.io/) 是免費的開放原始碼編輯器，如果您需要它。

以剪貼簿上的內嵌代碼取代第34行或第34行附近的現有內嵌代碼，並儲存頁面。 現在，在網頁瀏覽器中開啟頁面。 If you are loading the page using the `file://` protocol, you will need to add "https:" at the beginning of the embed code URL in your code editor). 範例頁面的第 33 到 36 行看起來可能像這樣:

```html
    <!--Launch Header Embed Code: REPLACE LINE 39 WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="https://assets.adobedtm.com/launch-ENa21cfed3f06f4ddf9690de8077b39e81-development.min.js" async></script>
    <!--/Launch Header Embed Code-->
```

開啟您網頁瀏覽器的開發人員工具，並前往「網路」標籤。 At this point you should see a 404 error for the Launch environment URL:
![404 error](images/samplepage-404.png)

預期會出現404錯誤，因為您尚未在此Launch環境中建立程式庫。 您會在下一個課程中執行該操作。如果您看到「失敗」訊息 (而不是 404 錯誤)，表示您可能忘了將 `https://` 通訊協定加入內嵌程式碼中。同樣地，如果您使用 `file://` 通訊協定載入範例頁面，則只需指定 `https://` 通訊協定即可。進行該變更並重新載入頁面，直到 404 錯誤出現為止。

## 啟動實施最佳實踐

讓我們花點時間來檢閱範例頁面中展示的Launch實作最佳實務：

* **資料層**:

   * We *strongly* recommend creating a digital data layer on your site containing all of the attributes needed to populate variables in Analytics, Target, and other marketing solutions. 此範例頁面只包含非常簡單的資料層，但實際資料層可能包含有關頁面的更多詳細資料、訪客、其購物車詳細資料等內容。For more info on data layers, please see [Customer Experience Digital Data Layer 1.0](https://www.w3.org/2013/12/ceddl-201312.pdf)

   * 在啟動內嵌程式碼之前定義您的資料層，以發揮您在Target、客戶屬性和Analytics中的最大作用。

* **JavaScript協助程式庫**:如果您的頁面中已實作JQuery等程式庫， `<head>` 請在啟動前載入，以便在啟動和目標中運用其語法

* **HTML5 doctype**:Target需要HTML5 doctype

* **preconnect 和 dns-prefetch**: 使用 preconnect 和 dns-prefetch 來改善頁面載入時間。See also: [https://w3c.github.io/resource-hints/](https://w3c.github.io/resource-hints/)

* **非同步Target實作的預先隱藏程式碼片段**:您會在Target課程中進一步瞭解，但是當Target透過非同步的Launch內嵌代碼部署時，您應在Launch內嵌代碼之前，先在頁面上加上預先隱藏的程式碼片段，以管理內容閃爍

以下依建議順序呈現這些最佳做法的摘要。請注意，帳戶特定詳細資訊有一些預留位置：

```html
<!doctype html>
<html lang="en">
<head>
    <title>Basic Demo</title>
    <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
    <link rel="preconnect" href="//dpm.demdex.net">
    <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//cm.everesttech.net">
    <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
    <link rel="dns-prefetch" href="//dpm.demdex.net">
    <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//cm.everesttech.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
    <!--/Preconnect and DNS-Prefetch-->
    <!--Data Layer to enable rich data collection and targeting-->
    <script>
    var digitalData = {
        "page": {
            "pageInfo" : {
                "pageName": "Home"
                }
            }
    };
    </script>
    <!--/Data Layer-->
    <!--jQuery or other helper libraries-->
    <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
    <!--/jQuery-->
    <!--prehiding snippet for Adobe Target with asynchronous Launch deployment-->
    <script>
        (function(g,b,d,f){(function(a,c,d){if(a){var e=b.createElement("style");e.id=c;e.innerHTML=d;a.appendChild(e)}})(b.getElementsByTagName("head")[0],"at-body-style",d);setTimeout(function(){var a=b.getElementsByTagName("head")[0];if(a){var c=b.getElementById("at-body-style");c&&a.removeChild(c)}},f)})(window,document,"body {opacity: 0 !important}",3E3);
    </script>
    <!--/prehiding snippet for Adobe Target with asynchronous Launch deployment-->
    <!--Launch Header Embed Code: REPLACE LINE 39 WITH THE INSTALL CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Launch Header Embed Code-->
</head>
<body>
    <h1>Launch by Adobe: Basic Demo</h1>
    <p>This is a very simple page to demonstrate basic concepts of Launch by Adobe</p>
</body>
</html>
```

現在您知道如何將Launch內嵌代碼新增至您的網站！

[下一個「新增資料元素、規則和程式庫」&gt;](launch-data-elements-rules.md)