---
title: 推播通知報告
description: 使用立即可用推播通知報表，瞭解推播通知是否成功。
level: Intermediate
audience: end-user
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
source-git-commit: 3f4400f24b75e8e435610afbe49e9d9444dbf563
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# 推播通知報告{#push-notification-report}

>[!CAUTION]
>
>請注意，您必須將&#x200B;**[!UICONTROL 訊息型別]**&#x200B;量度拖放至表格，才能根據您的傳送型別分割資料，在此例中，是以推播通知傳送。

**推播通知**&#x200B;報告提供Adobe Campaign中推播通知行銷績效的詳細資料。 這個現成的報告可協助您瞭解使用者如何與推播通知、行動應用程式和傳遞互動。

![](assets/dynamic_report_push.png)

每個表格都由摘要數字和圖表表示。 您可以變更詳細資訊在其各自視覺效果設定中的顯示方式。

第一個資料表&#x200B;**推播通知參與摘要**&#x200B;分為三個類別：依日期、依行動應用程式及依傳遞。 它包含可用於收件者對傳遞的反應性的資料：

* **[!UICONTROL 已處理/傳送]**：已傳送的推播通知總數。
* **[!UICONTROL 已傳遞]**：成功傳送的推播通知數目（與已傳送的推播通知總數相關）。
* **[!UICONTROL 曝光次數]**：推播通知已傳送至裝置並在通知中心保持未觸及的次數。 在大多數情況下，曝光次數應該與傳送的數目類似。 這可確保裝置收到訊息，並將該資訊轉送回伺服器。
* **[!UICONTROL 不重複曝光次數]**：收件者的曝光次數。
* **[!UICONTROL 點進率]**：與推播通知互動的使用者百分比。
* **[!UICONTROL 開啟率]**：已開啟推播通知的百分比。

![](assets/dynamic_report_push_2.png)

第二個資料表&#x200B;**推播通知點按與開啟**&#x200B;分為三個類別：依日期、依行動應用程式及依傳遞。 它包含每個傳遞的收件者行為可用資料：

* **[!UICONTROL 曝光次數]**：收件者看到的推播通知總數。
* **[!UICONTROL 不重複曝光次數]**：收件者的曝光次數。
* **[!UICONTROL 點按]**：推播通知已傳送至裝置且使用者點按的次數。 使用者想要檢視通知（通知隨後將移至推播開啟追蹤）或將其關閉。
* **[!UICONTROL 不重複點按]**：不重複使用者與推播通知互動的次數，例如點按通知或按鈕。
* **[!UICONTROL 開啟]**：傳送至裝置的推播通知總數，使用者因此開啟應用程式而點按。 這類似於「推送點按」，但如果通知已關閉，則不會觸發「推送開啟」。
* **[!UICONTROL 不重複開啟]**：開啟傳遞的收件者人數。
