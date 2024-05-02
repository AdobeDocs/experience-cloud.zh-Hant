---
title: 指標計算
description: 使用每個量度的公式清單瞭解報表的結果。
level: Intermediate
audience: end-user
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
source-git-commit: 031d5b692d9b9e4420b14ba1ab892fbafed57ec0
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---

# 指標計算{#indicator-calculation}

>[!NOTE]
>
>為了更好地處理和管理高容量和即時分析，動態報告使用近似彙總來得出不同的計數預估。 近似彙總提供有限的記憶體使用量，通常比精確計算更快。

下表提供不同報表中使用的指標清單，及其計算公式（視傳遞型別而定）。

## 電子郵件傳遞 {#email-delivery}

<table> 
 <thead> 
  <tr> 
   <th> <strong>標籤</strong> <br/> </th> 
   <th> <strong>欄位名稱</strong> <br/> </th> 
   <th> <strong>指標計算公式</strong> <br/> </th> 
   <th> <strong>註解</strong><br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> 帳戶已停用<br/> </td> 
   <td> @disabled<br/> </td> 
   <td> count(@failureReason=4)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 在封鎖清單上<br/> </td> 
   <td> @blacklisted<br/> </td> 
   <td> count(@failureReason=8， @failureType=2)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 封鎖清單率<br/> </td> 
   <td> @rateBlacklisted<br/> </td> 
   <td> @blacklisted/@sent<br/> </td> 
   <td> 費率計算的分母是以「已傳送」計數（已傳遞+跳出數）為基礎。<br/> </td> 
  </tr> 
  <tr> 
   <td> 退回+錯誤<br/> </td> 
   <td> @bounces<br/> </td> 
   <td> count(@status=2)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 退回+錯誤率<br/> </td> 
   <td> @rateBounces<br/> </td> 
   <td> @bounces/@sent<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 按一下<br/> </td> 
   <td> @clicks<br/> </td> 
   <td> count(@trackingUrlType=1或10或11)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 點進率<br/> </td> 
   <td> @clickthrough<br/> </td> 
   <td> @uniqueclicks/@delivered<br/> </td> 
   <td> 費率計算的分母僅以「已傳遞」為基礎。<br/> </td> 
  </tr> 
  <tr> 
   <td> 已傳遞<br/> </td> 
   <td> @delivered<br/> </td> 
   <td> count(@status=1)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 傳遞率<br/> </td> 
   <td> @rateDelivered<br/> </td> 
   <td> @delivered/@sent<br/> </td> 
   <td> 費率計算的分母是以「已傳送」計數（已傳遞+跳出數）為基礎。<br/> </td> 
  </tr> 
  <tr> 
   <td> 硬跳出<br/> </td> 
   <td> @hardBounces<br/> </td> 
   <td> count(@failureType=2且@failureReason=8)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 硬跳出率<br/> </td> 
   <td> @rateHardBounces<br/> </td> 
   <td> @hardBounces/@sent<br/> </td> 
   <td> 費率計算的分母是以「已傳送」計數（已傳遞+跳出數）為基礎。<br/> </td> 
  </tr> 
  <tr> 
   <td> 無效的網域<br/> </td> 
   <td> @invalidDomain<br/> </td> 
   <td> count(@failureReason=2)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 郵箱已滿<br/> </td> 
   <td> @mailBoxFull<br/> </td> 
   <td> count(@failureReason=5)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 映象頁面<br/> </td> 
   <td> @mirrorPage<br/> </td> 
   <td> count(@trackingUrlType=6)<br/> </td> 
   <td> 費率計算的分母僅以「已傳遞」為基礎。<br/> </td> 
  </tr> 
  <tr> 
   <td> 映象頁面速率<br/> </td> 
   <td> @rateMirrorPage<br/> </td> 
   <td> @mirrorPage/@delivered<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 未連線<br/> </td> 
   <td> @notConnected<br/> </td> 
   <td> count(@failureReason=6)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 開啟<br/> </td> 
   <td> @uniqueOpens<br/> </td> 
   <td> count(@trackingUrlType=2 +唯一(@trackingUrlType=1,2，3,6，10,11) — 唯一(@trackingUrlType=2))<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 開啟率<br/> </td> 
   <td> @rateOpens<br/> </td> 
   <td> @opens/@delivered<br/> </td> 
   <td> 費率計算的分母僅以「已傳遞」為基礎。<br/> </td> 
  </tr> 
  <tr> 
   <td> 隔離<br/> </td> 
   <td> @quarantine<br/> </td> 
   <td> isQuarantine=true<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 隔離率<br/> </td> 
   <td> @rateQuarantine<br/> </td> 
   <td> @quarantine/@sent<br/> </td> 
   <td> 費率計算的分母是以「已傳送」計數（已傳遞+跳出數）為基礎。<br/> </td> 
  </tr>
  <tr> 
   <td> 已拒絕<br/> </td> 
   <td> @rejected<br/> </td> 
   <td> count(@failureReason=20， @failureType=2)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 拒絕率<br/> </td> 
   <td> @rateRejected<br/> </td> 
   <td> @rejected/@sent<br/> </td> 
   <td> 費率計算的分母是以「已傳送」計數（已傳遞+跳出數）為基礎。<br/> </td> 
  </tr> 
  <tr> 
   <td> 已處理/傳送<br/> </td> 
   <td> @sent<br/> </td> 
   <td> @delivered + @bounces<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 軟退信<br/> </td> 
   <td> @softBounces<br/> </td> 
   <td> count(@failureType=1)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 軟跳出率<br/> </td> 
   <td> @rateSoftBounces<br/> </td> 
   <td> @softBounces/@sent<br/> </td> 
   <td> 費率計算的分母是以「已傳送」計數（已傳遞+跳出數）為基礎。<br/> </td> 
  </tr> 
  <tr> 
   <td> 不重複點按<br/> </td> 
   <td> @uniqueclicks<br/> </td> 
   <td> 不重複點按次數是使用ThetaSketch概念計算的。 </a>.<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 不重複開啟<br/> </td> 
   <td> @uniqueopens<br/> </td> 
   <td> 唯一(@trackingUrlType=1,2，3,6，10,11)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 無法聯絡 <br/> </td> 
   <td> @unreachable<br/> </td> 
   <td> count(@failureReason=3)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 取消訂閱<br/> </td> 
   <td> @unsubscribes<br/> </td> 
   <td> count(@trackingUrlType=3)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 取消訂閱率<br/> </td> 
   <td> @rateUnsubscribes<br/> </td> 
   <td> @unsubscribes/@delivered<br/> </td> 
   <td> 費率計算的分母僅以「已傳遞」為基礎。<br/> </td> 
  </tr> 
  <tr> 
   <td> 使用者不明<br/> </td> 
   <td> @unknownUser<br/> </td> 
   <td> count(@failureReason=1)<br/> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

<!--
## Push notification delivery {#push-notification-delivery}

<table> 
 <thead> 
  <tr> 
   <th> <strong>Label</strong> <br/> </th> 
   <th> <strong>Field name</strong> <br/> </th> 
   <th> <strong>Indicator calculation formula</strong> <br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> Processed/sent<br/> </td> 
   <td> @sent<br/> </td> 
   <td> @count(status=sent)<br/> </td> 
  </tr> 
  <tr> 
   <td> Delivered<br/> </td> 
   <td> @delivered<br/> </td> 
   <td> @count(status=delivered)<br/> </td> 
  </tr> 
  <tr> 
   <td> Delivered rate<br/> </td> 
   <td> @rateDelivered<br/> </td> 
   <td> (@delivered/@sent)*100<br/> </td> 
  </tr> 
  <tr> 
   <td> Bounce + Error rate<br/> </td> 
   <td> @rateBounces<br/> </td> 
   <td> (@delivered/@sent)*100<br/> </td> 
  </tr> 
  <tr> 
   <td> Open<br/> </td> 
   <td> @opens<br/> </td> 
   <td> @count(status=open)<br/> </td> 
  </tr> 
  <tr> 
   <td> Open rate<br/> </td> 
   <td> @rateOpens<br/> </td> 
   <td> (@opens/@delivered)*100<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique opens<br/> </td> 
   <td> @uniqueopens<br/> </td> 
   <td> Unique opens is calculated using ThetaSketch concepts of unique RecipientIds.<br/> </td> 
  </tr> 
  <tr> 
   <td> Impressions<br/> </td> 
   <td> @impressions<br/> </td> 
   <td> @count(status=delivered)<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique impressions<br/> </td> 
   <td> @uniqueimpressions<br/> </td> 
   <td> @unique(@count(status=view))<br/> </td> 
  </tr> 
  <tr> 
   <td> Click<br/> </td> 
   <td> @clicks<br/> </td> 
   <td> @count(status=interact)<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique clicks<br/> </td> 
   <td> @uniqueclicks<br/> </td> 
   <td> Unique clicks is calculated using ThetaSketch concepts.<br/> </td> 
  </tr> 
  <tr> 
   <td> Click through rate<br/> </td> 
   <td> @clickthrough<br/> </td> 
   <td> (@interact/@delivered)*100<br/> </td> 
  </tr> 
 </tbody> 
</table>

## In-App delivery {#in-app-delivery}

<table> 
 <thead> 
  <tr> 
   <th> <strong>Label</strong> <br/> </th> 
   <th> <strong>Field name</strong> <br/> </th> 
   <th> <strong>Indicator calculation formula</strong> <br/> </th> 
   <th> <strong>Comments</strong><br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> Processed/sent<br/> </td> 
   <td> @sent<br/> </td> 
   <td> @count(status=sent)<br/> </td> 
   <td> sent=delivered<br/> </td> 
  </tr> 
  <tr> 
   <td> Delivered<br/> </td> 
   <td> @delivered<br/> </td> 
   <td> @count(status=delivered)<br/> </td> 
   <td> delivered=sent<br/> </td> 
  </tr> 
  <tr> 
   <td> Impressions<br/> </td> 
   <td> @impressions<br/> </td> 
   <td> @count(status=view) or @count(status=button 1 click + button 2 click + dismissals)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> Unique impressions<br/> </td> 
   <td> @uniqueimpressions<br/> </td> 
   <td> @unique(@count(status=view))<br/> </td> 
   <td> For <span class="uicontrol">Target users based on their Campaign profile (inAppProfile)</span> template, user = Recipient Id.<br/> For <span class="uicontrol">Target all users of a Mobile app (inAppBroadcast)</span> and <span class="uicontrol">Target users based on their Mobile profile (inApp)</span> templates, user = MC Id or equivalent that represents a unique combination of user, mobile app and device.<br/> </td> 
  </tr> 
  <tr> 
   <td> In-App clicks <br/> </td> 
   <td> @inappclicks<br/> </td> 
   <td> @count (status=click)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> Unique In-App clicks<br/> </td> 
   <td> @uniqueinapp<br/> </td> 
   <td> @unique(@count (status=clicks))<br/> </td> 
   <td> For <span class="uicontrol">Target users based on their Campaign profile (inAppProfile)</span> template, user = Recipient Id.<br/> For <span class="uicontrol">Target all users of a Mobile app (inAppBroadcast)</span> and <span class="uicontrol">Target users based on their Mobile profile (inApp)</span> templates, user = MC Id or equivalent that represents a unique combination of user, mobile app and device.<br/> </td> 
  </tr> 
  <tr> 
   <td> In-App click through rate<br/> </td> 
   <td> @inappclickthrough<br/> </td> 
   <td> Total clicks on Button 1 or Button 2/total impressions*100<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> In-App dismissal<br/> </td> 
   <td> @dismissal<br/> </td> 
   <td> @count (status=close)<br/> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> Unique In-App dismissals<br/> </td> 
   <td> @uniquedismissal<br/> </td> 
   <td> @unique(@count (status=close))<br/> </td> 
   <td> For <span class="uicontrol">Target users based on their Campaign profile (inAppProfile)</span> template, user = Recipient Id.<br/> For <span class="uicontrol">Target all users of a Mobile app (inAppBroadcast)</span> and <span class="uicontrol">Target users based on their Mobile profile (inApp)</span> templates, user = MC Id or equivalent that represents a unique combination of user, mobile app and device.<br/> </td> 
  </tr> 
  <tr> 
   <td> In-App dismissal rate<br/> </td> 
   <td> @dismissalrate<br/> </td> 
   <td> Total close/total impressions*100<br/> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>
-->