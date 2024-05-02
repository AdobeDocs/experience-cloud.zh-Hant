---
title: 疑難排解動態報告
description: 在此處尋找與動態報告相關的常見問題。
audience: end-user
level: Intermediate
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
source-git-commit: 3f4400f24b75e8e435610afbe49e9d9444dbf563
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 1%

---

# 疑難排解{#troubleshooting}

您可以在本小節中找到與動態報告相關的常見問題。

## 對於不重複開啟和不重複點按，彙總列中的計數與個別列中的計數不相符 {#unique-open-clicks-no-match}

這是預期行為。
我們可藉由下列範例來解釋此行為。

會傳送電子郵件給設定檔P1和P2。

P1會在第一天開啟電子郵件兩次，然後在第二天開啟樹狀結構。

然而，P2會在第一天開啟電子郵件一次，且不會在後續幾天重新開啟。
設定檔與已傳送電子郵件間互動的視覺化呈現方式如下：

<table> 
 <thead> 
  <tr> 
   <th align="center"> <strong>日</strong> <br/> </th> 
   <th align="center"> <strong>開啟次數</strong> <br/> </th> 
   <th align="center"> <strong>不重複開啟</strong> <br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td align="center"> 第1天<br/> </td> 
   <td align="center"> 2 + 1 = 3<br/> </td> 
   <td align="center"> 1 + 1 = 2<br/> </td> 
  </tr> 
  <tr> 
   <td align="center"> 第2天<br/> </td> 
   <td align="center"> 3 + 0 = 3<br/> </td> 
   <td align="center"> 1 + 0 = 1<br/> </td> 
  </tr>
 </tbody> 
</table>

若要瞭解不重複開啟的總數，我們需要將 **[!UICONTROL 不重複開啟次數]** 因此值為3。 但由於電子郵件僅針對2個設定檔，因此開啟率應顯示150%。

若要取得高於100的百分比，定義 **[!UICONTROL 不重複開啟次數]** 將維持為已開啟的不重複broadlog數。 在此案例中，即使P1在第1天和第2天開啟電子郵件，其唯一開啟次數仍為1。

這會產生下表：

<table> 
 <thead> 
  <tr> 
   <th align="center"> <strong></strong> <br/> </th> 
   <th align="center"> <strong>開啟次數</strong> <br/> </th> 
   <th align="center"> <strong>不重複開啟</strong> <br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td align="center"> <strong> 日 </strong><br/> </td> 
   <td align="center"> <strong> 6 </strong><br/> </td> 
   <td align="center"> <strong> 2</strong><br/> </td>
  </tr> 
  <tr> 
   <td align="center"> 第1天<br/> </td> 
   <td align="center"> 3<br/> </td> 
   <td align="center"> 2<br/> </td>
  </tr> 
  <tr> 
   <td align="center"> 第2天<br/> </td> 
   <td align="center"> 3<br/> </td> 
   <td align="center"> 1<br/> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>不重複計數是以HLL型草圖為基礎的，這可能會導致大量計數出現細微的不準確性。

## 開啟計數與資料庫計數不符 {#open-counts-no-match-database}

這可能是因為，即使我們無法追蹤開啟，動態報告中也會使用啟發式來追蹤開啟。 **[!UICONTROL 開啟]** 動作。

例如，如果使用者在其使用者端上停用影像並按一下電子郵件中的連結，則 **[!UICONTROL 開啟]** 資料庫可能不會追蹤，但 **[!UICONTROL 按一下]** 會。

因此， **[!UICONTROL 開啟]** 追蹤記錄檔計數在資料庫中可能沒有相同的計數。

此類相符專案會新增為 **「電子郵件點按表示電子郵件已開啟」**.

>[!NOTE]
>
>由於不重複計數是以HLL型草圖為基礎，因此可能會出現計數之間的細微不一致。

## 如何計算週期性/交易式傳送的計數？ {#counts-recurring-deliveries}

處理循環和交易式傳送時，這些計數將同時歸因於父傳送和子傳送。
我們以名為的循環傳送為例 **R1** 設為在第1天(RC1)、第2天(RC2)和第3天(RC3)每天執行。
假設只有一個人員會多次開啟所有子傳送。 在此情況下，個別循環的子傳送將會顯示 **[!UICONTROL 開啟]** 各計為1。
不過，由於同一人按一下所有傳送，因此父級循環傳送也會有 **[!UICONTROL 不重複開啟]** as 1.

報表應如下所示：

<table> 
 <thead> 
  <tr> 
   <th align="center"> <strong>傳遞</strong> <br/> </th> 
   <th align="center"> <strong>已傳送</strong> <br/> </th> 
   <th align="center"> <strong>已傳遞</strong> <br/> </th>
   <th align="center"> <strong>開啟次數</strong> <br/> </th> 
   <th align="center"> <strong>不重複開啟</strong> <br/> </th>
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td align="center"> <strong>R1</strong><br/> </td> 
   <td align="center"> <strong>100</strong><br/> </td> 
   <td align="center"> <strong>90</strong><br/> </td> 
   <td align="center"> <strong>10</strong><br/> </td> 
   <td align="center"> <strong>3</strong><br/> </td> 
  </tr> 
  <tr> 
   <td align="center"> RC1<br/> </td> 
   <td align="center"> 20<br/> </td> 
   <td align="center"> 20<br/> </td> 
   <td align="center"> 6<br/> </td> 
   <td align="center"> 1<br/> </td> 
  </tr>
    <tr> 
   <td align="center"> RC2<br/> </td> 
   <td align="center"> 40<br/> </td> 
   <td align="center"> 30<br/> </td> 
   <td align="center"> 2<br/> </td> 
   <td align="center"> 1<br/> </td> 
  </tr> 
    <tr> 
   <td align="center"> RC3<br/> </td> 
   <td align="center"> 40<br/> </td> 
   <td align="center"> 40<br/> </td> 
   <td align="center"> 2<br/> </td> 
   <td align="center"> 1<br/> </td> 
  </tr> 
 </tbody> 
</table>

## 顏色在報表表格中的意義為何？ {#reports-color-signification}

報表上顯示的顏色是隨機的，無法個人化。 它們代表進度列，可協助您更清楚地強調報告中達到的最大值。

在下列範例中，儲存格的顏色相同，因為其值為100%。

![](assets/troubleshooting_1.png)

如果您變更 **[!UICONTROL 條件式格式]** 若要自訂，當值達到上限時，儲存格會變得更綠色。 然而，如果達到下限，則會變紅。

舉例來說，我們在此設定 **[!UICONTROL 上限]** 至500和 **[!UICONTROL 下限]** 至0。

![](assets/troubleshooting_2.png)

## 為什麼值N/A會出現在我的報表中？

![](assets/troubleshooting_3.png)

值 **不適用** 有時也會出現在動態報告中。 原因有三：

* 傳遞已刪除，並在這裡顯示為 **不適用** 並不會導致結果不一致。
* 拖放 **[!UICONTROL 異動傳送]** 維度至您的報表，值 **不適用** 可能會顯示結果。 這是因為動態報告會擷取每個傳送，即使它們不是交易式傳送。 拖放 **[!UICONTROL 傳遞]** 維度，但在此案例中， **不適用** 值將代表異動傳送。
* 當維度搭配與維度無關的量度使用時。 在下列範例中，會新增劃分並包含 **[!UICONTROL 追蹤URL]** 維度，即使 **[!UICONTROL 按一下]** 在此傳遞中，計數設為0。

  ![](assets/troubleshooting_4.png)

## 使用自訂目標對應時，傳遞的報表顯示不完整的資料

如果您在傳送中使用匯入的自訂Target對應，但不同的報表中未顯示任何資料，則可能表示系統並未針對這些Target對應建立報表擴充功能。

若要解決此問題：

* 從XML匯入Target對應後，您也需要匯入Reporting擴充。

* 您可以直接在Adobe Campaign Web使用者介面中建立對應，而不匯入Target對應，該介面會自動建立報告擴充。

## 欄標題編號與列總和之間的差異

在下列情況下，欄標題編號與所有列的總和之間應該會有差異：

* **不重複量度**：使用唯一量度可能會變更標題中顯示的總計數，因為它是根據收件者ID，而不是簡單的列計數總和。 因此，單一設定檔可能會觸發多個不同維度的事件，導致資料集出現多個列。 不過在標題中，每個設定檔只會計算一次。

  例如：

   * 如果設定檔A在三天開啟電子郵件，依日劃分的會在三列中顯示A，但在標題中，A會計為1。

   * 如果設定檔A在同日點選電子郵件中的三個不同連結，依追蹤URL的劃分會在三列中顯示A，但在標題中，A會計為1。 同樣的套用也適用於依裝置和瀏覽器進行的劃分。

* **開啟量度**：開啟次數計數是透過彙總實際「開啟」事件和「不重複」點按事件（依收件者ID）的總計來決定，不包括由於沒有開啟事件無法點按電子郵件連結而未發生開啟事件的情況。

  例如：

   * 當設定檔A開啟追蹤的電子郵件（包含URL U1）時，它會註冊為開啟事件，且URL標示為null。 稍後按一下U1會產生點選事件。 雖然U1上的A點選也會計為開啟事件，但U1沒有特定的開啟事件。 因此，A在不重複開啟計數中只會計算一次。

   * 設定檔R會在第1天開啟電子郵件、註冊開啟事件，然後按一下連結。 在接下來的兩天內， R會重新開啟電子郵件，然後再次點按連結，每天都會產生點按事件。 雖然R的參與在每日開啟數中進行追蹤，但R在欄標題中只會計算一次，並專注於不重複參與。

* **否定事件**：在報表中，否定事件表示最初標籤為成功，但在重試後最終失敗的傳送嘗試。 這些會以計數–1表示。 為避免混淆，這些負數會從顯示的傳遞量度數字中排除。 因此，傳遞量度的所有列總數可能與欄標題數字不符。
