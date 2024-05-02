---
title: 元件清單
description: 請在此處尋找動態報告中每個可用元件的清單及其定義。
level: Beginner
audience: end-user
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
source-git-commit: b11d696767209145511b38735f22275a38676ade
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# 元件清單 {#list-of-components}

請注意，如果兩個元件不相容，儲存格會顯示值 **無**.

## 維度 {#dimensions}

下表列出報表中使用的維度及其定義。

<table> 
 <thead> 
  <tr> 
   <th> Dimension<br/> </th> 
   <th> 定義<br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> 瀏覽器<br/> </td> 
   <td> 開啟或點選訊息的來源瀏覽器。<br/> </td> 
  </tr> 
  <tr> 
   <td> Campaign<br/> </td> 
   <td> 行銷活動的標籤和ID。<br/> </td> 
  </tr> 
  <tr> 
   <td> 傳遞<br/> </td> 
   <td> 傳遞的標籤和ID。<br/> </td> 
  </tr> 
  <tr> 
   <td> 裝置<br/> </td> 
   <td> 電子郵件/簡訊/推播通知開啟/檢視/點按的裝置。<br/> </td> 
  </tr> 
  <tr> 
   <td> 失敗原因<br/> </td> 
   <td> 導致每次傳遞跳出的錯誤型別，例如使用者不明、網域無效或信箱已滿。<br/> </td> 
  </tr> 
  <tr> 
   <td> 行動應用程式名稱<br/> </td> 
   <td> 行動應用程式的名稱<br/> </td> 
  </tr>
  <tr> 
   <td> Platform<br/> </td> 
   <td> 開啟/檢視/點選訊息的來源裝置平台。<br/> </td> 
  </tr> 
  <tr> 
   <td> 個人資料<br/> </td> 
   <td> 重新分組在設定檔資源擴充期間建立的現成可用和自訂設定檔欄位。<br/> </td> 
  </tr> 
  <tr> 
   <td> 收件者網域<br/> </td> 
   <td> 用來開啟電子郵件的網域。<br/> </td> 
  </tr> 
  <tr> 
   <td> 循環傳遞<br/> </td> 
   <td> 重複傳送的標籤和ID。<br/> </td> 
  </tr> 
  <tr> 
   <td> 寄件者網域<br/> </td> 
   <td> 用來傳送電子郵件的網域。<br/> </td> 
  </tr> 
  <tr> 
   <td> 寄件者IP<br/> </td> 
   <td> 用來傳送電子郵件的IP。<br/> </td> 
  </tr> 
  <tr> 
   <td> 追蹤URL<br/> </td> 
   <td> 使用者從訊息中點按的URL。<br/> </td> 
  </tr> 
  <tr> 
   <td> 追蹤網址類別<br/> </td> 
   <td> 指派給追蹤URL的類別。<br/> </td> 
  </tr> 
  <tr> 
   <td> 追蹤網址標籤<br/> </td> 
   <td> 指定給URL的標籤，例如映象頁面、聯絡我們或開啟。<br/> </td> 
  </tr> 
  <tr> 
   <td> 異動傳遞<br/> </td> 
   <td> 異動傳送的標籤和ID。<br/> </td> 
  </tr> 
  <tr> 
   <td> 變體<br/> </td> 
   <td> A/B測試時的電子郵件變體。<br/> </td> 
  </tr> 
 </tbody> 
</table>

## 量度 {#metrics}

下表提供報表中使用的量度清單，以及量度定義（視傳送型別而定）。

### 電子郵件量度 {#email-and-sms-metrics}

<table> 
 <thead> 
  <tr> 
   <th> 量度<br/> </th> 
   <th> 定義<br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> 在封鎖清單上<br/> </td> 
   <td> 已將電子郵件宣告為垃圾郵件或垃圾郵件的收件者人數。<br/> </td> 
  </tr> 
  <tr> 
   <td> 封鎖清單率<br/> </td> 
   <td> 封鎖清單上標籤的傳遞百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 退回+錯誤<br/> </td> 
   <td> 與已傳送訊息總數相關的傳遞和自動回訪處理期間累計的錯誤總數。<br/> </td> 
  </tr> 
  <tr> 
   <td> 退回+錯誤率<br/> </td> 
   <td> 與已傳送的電子郵件相比跳出的電子郵件百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 按一下<br/> </td> 
   <td> 內容在傳遞中被點按的次數。<br/> </td> 
  </tr> 
  <tr> 
   <td> 點進率<br/> </td> 
   <td> 傳遞中的點按百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 已傳遞<br/> </td> 
   <td> 成功傳送的訊息數（與已傳送訊息總數相關）。<br/> </td> 
  </tr> 
  <tr> 
   <td> 傳遞率<br/> </td> 
   <td> 已成功傳送的訊息百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 硬退信<br/> </td> 
   <td> 永久錯誤總數，例如錯誤的電子郵件地址。<br/> </td> 
  </tr> 
  <tr> 
   <td> 硬跳出率<br/> </td> 
   <td> 因永久錯誤而失敗的傳遞百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 映象頁面<br/> </td> 
   <td> 點按映象頁面連結的收件者人數。<br/> </td> 
  </tr> 
  <tr> 
   <td> 映象頁面速率<br/> </td> 
   <td> 相較於傳遞訊息總數，映象頁面連結的點按百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 優惠點選次數<br/> </td> 
   <td> 在傳遞中點按優惠方案的次數。<br/> </td> 
  </tr> 
  <tr> 
   <td> 優惠點按率<br/> </td> 
   <td> 優惠的點按百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 開啟<br/> </td> 
   <td> 訊息在傳遞中開啟的次數。<br/> </td> 
  </tr> 
  <tr> 
   <td> 開啟率<br/> </td> 
   <td> 已開啟訊息的百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 已處理/傳送<br/> </td> 
   <td> 傳遞的傳送總數。<br/> </td> 
  </tr> 
  <tr> 
   <td> 隔離<br/> </td> 
   <td> 退回並導致地址隔離的郵件數。<br/> </td> 
  </tr> 
  <tr> 
   <td> 隔離率<br/> </td> 
   <td> 相較於已傳送訊息的隔離百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 已拒絕<br/> </td> 
   <td> SMTP伺服器分類為垃圾郵件的郵件數。<br/> </td> 
  </tr> 
  <tr> 
   <td> 拒絕率<br/> </td> 
   <td> 標示為拒絕的郵件百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 軟退信<br/> </td> 
   <td> 暫時性錯誤總數，例如完整收件匣。<br/> </td> 
  </tr> 
  <tr> 
   <td> 軟跳出率<br/> </td> 
   <td> 因暫時原因而失敗的傳遞百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 不重複點按<br/> </td> 
   <td> 在傳遞中點按內容的收件者人數。<br/> </td> 
  </tr> 
  <tr> 
   <td> 不重複開啟<br/> </td> 
   <td> 開啟傳遞的收件者人數。<br/> </td> 
  </tr> 
  <tr> 
   <td> 不重複取消訂閱<br/> </td> 
   <td> 點按取消訂閱連結的收件者人數。<br/> </td> 
  </tr> 
  <tr> 
   <td> 取消訂閱率<br/> </td> 
   <td> 與傳遞的訊息比較的不重複取消訂閱數。<br/> </td> 
  </tr> 
  <tr> 
   <td> 已取消訂閱<br/> </td> 
   <td> 對取消訂閱連結的點按次數。<br/> </td> 
  </tr> 
 </tbody> 
</table>

<!--
### Push notification metrics {#push-notification-metrics}

<table> 
 <thead> 
  <tr> 
   <th> Metric<br/> </th> 
   <th> Definition<br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> Bounces + Errors<br/> </td> 
   <td> Total of errors cumulated during delivery in relation to the total number of sent messages, e.g. errors from MCPNS or provider.<br/> </td> 
  </tr> 
  <tr> 
   <td> Bounce + Error rate<br/> </td> 
   <td> Percentage of push notifications that bounced compared to push notifications sent.<br/> </td> 
  </tr> 
  <tr> 
   <td> Click<br/> </td> 
   <td> Number of times a push notification has been delivered to the device and clicked on by the user. The user either wanted to view the notification, which will then be moved to Push Open tracking, or dismiss it.<br/> </td> 
  </tr> 
  <tr> 
   <td> Click through rate<br/> </td> 
   <td> Percentage of users who interacted with the push notification.<br/> </td> 
  </tr> 
  <tr> 
   <td> Delivered<br/> </td> 
   <td> Number of push notifications successfully sent, in relation to the total number of sent push notifications.<br/> </td> 
  </tr> 
  <tr> 
   <td> Delivered rate<br/> </td> 
   <td> Percentage of push notifications successfully sent.<br/> </td> 
  </tr> 
  <tr> 
   <td> Impressions<br/> </td> 
   <td> Number of times a push notification has been delivered to the device and left untouched in the notification center. In most cases, impressions number should be similar to the delivered number. This ensures that the device got the message and relayed that information back to the server.<br/> </td> 
  </tr> 
  <tr> 
   <td> Processed/sent<br/> </td> 
   <td> Total number of push notifications sent.<br/> </td> 
  </tr> 
  <tr> 
   <td> Open<br/> </td> 
   <td> Total number of push notifications delivered to the device and clicked on by users thus opening the app. This is similar to the Push Click except a Push Open will not be triggered if the notification was dismissed.<br/> </td> 
  </tr> 
  <tr> 
   <td> Open rate<br/> </td> 
   <td> Percentage of opened push notifications.<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique clicks<br/> </td> 
   <td> Number of times a unique user interacts with the push notification, e.g. clicks on the notification or button.<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique impressions<br/> </td> 
   <td> Number of impressions by recipient.<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique Opens<br/> </td> 
   <td> Number of recipients who opened the delivery.<br/> </td> 
  </tr> 
 </tbody> 
</table>

### In-App metrics {#in-app-metrics}

<table> 
 <thead> 
  <tr> 
   <th> Metric<br/> </th> 
   <th> Definition<br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> Delivered<br/> </td> 
   <td> Total number of In-App messages delivered to the device by the service provider.<br/> </td> 
  </tr> 
  <tr> 
   <td> Impressions<br/> </td> 
   <td> Total of In-App messages seen by recipients depending on whether trigger criterion was met.<br/> </td> 
  </tr> 
  <tr> 
   <td> In-App clicks <br/> </td> 
   <td> Total number of recipients who clicked on Button 1 or Button 2.<br/> </td> 
  </tr> 
  <tr> 
   <td> In-App click through rate<br/> </td> 
   <td> Percentage of users who clicked on Button 1 or Button 2 compared to users who saw the message.<br/> </td> 
  </tr> 
  <tr> 
   <td> In-App dismissal<br/> </td> 
   <td> Total number of messages that recipients dismissed either by clicking the close button or auto-dismiss.<br/> </td> 
  </tr> 
  <tr> 
   <td> In-App dismissal rate<br/> </td> 
   <td> Percentage of In-App messages that recipients dismissed.<br/> </td> 
  </tr> 
  <tr> 
   <td> Processed/sent<br/> </td> 
   <td> Total number of In-App messages sent from Adobe Campaign as part of the delivery sent process.<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique impressions<br/> </td> 
   <td> Number of impressions by a unique recipient.<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique In-App clicks<br/> </td> 
   <td> Number of times recipients clicked on Button 1 or Button 2.<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique In-App dismissals<br/> </td> 
   <td> Number of time recipients dismissed an In-App message.<br/> </td> 
  </tr> 
 </tbody> 
</table>
-->

## 區段 {#segments}

下表提供報告中使用的區段清單及其定義。

<table> 
 <thead> 
  <tr> 
   <th> 區段<br/> </th> 
   <th> 定義<br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> 年齡：嬰兒潮1<br/> </td> 
   <td> 1946年至1954年出生的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年齡：嬰兒潮一代2<br/> </td> 
   <td> 1955年至1965年出生的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年齡：從18到25<br/> </td> 
   <td> 18到25歲的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年齡：從26到30<br/> </td> 
   <td> 26到30歲的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年齡：從31到40<br/> </td> 
   <td> 31到40歲的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年齡：從41到50<br/> </td> 
   <td> 41到50歲的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年齡：第X代<br/> </td> 
   <td> 1966年至1976年出生的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年齡：Y代（千禧一代）<br/> </td> 
   <td> 1977年至1994年出生的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年齡：Z代<br/> </td> 
   <td> 1995年至今的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年齡：大於50<br/> </td> 
   <td> 年齡超過50歲的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年齡：25歲以下<br/> </td> 
   <td> 年齡小於25歲的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年齡：少於30歲<br/> </td> 
   <td> 年齡小於30歲的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年齡：40歲以下<br/> </td> 
   <td> 年齡小於40歲的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年齡：少於50歲<br/> </td> 
   <td> 年齡小於50歲的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年齡：靜音產生<br/> </td> 
   <td> 1945年或之前出生的收件者。<br/> </td> 
  </tr> 
  <tr> 
   <td> 所有造訪<br/> </td> 
   <td> 每個收件者<br/> </td> 
  </tr>
 </tbody> 
</table>
