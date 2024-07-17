---
title: 退回摘要
description: 使用彈回摘要現成可用報告，瞭解您傳送的行銷活動狀態及其可能遇到的錯誤。
audience: end-user
level: Intermediate
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
exl-id: b341edad-aa82-43d8-a5a1-b33a19973a1a
source-git-commit: 34c6f8a137a9085b26c0ea8f78930cff6192cfc9
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---

# 退回摘要{#bounce-summary}

此報表詳細說明傳送期間遇到的整體硬式和軟式錯誤，以及自動處理退信。

![](assets/campaign_reports_bounces.png)

每個表格都由摘要數字和圖表表示。 您可以變更詳細資訊在其各自視覺效果設定中的顯示方式。

**失敗5重新分割**&#x200B;列出隔離數量最多的五個傳遞：

**退回原因**&#x200B;表格包含造成每個傳遞退回的錯誤型別的可用資料：

* **[!UICONTROL 使用者不明]**：傳送至無效電子郵件地址時產生的錯誤型別。
* **[!UICONTROL 無效的網域]**：傳送至網域錯誤或不再存在的電子郵件地址時，產生的錯誤型別。
* **[!UICONTROL 無法連線]**：在訊息傳遞字串中遇到的錯誤型別，例如暫時無法連線的網域。
* **[!UICONTROL 帳戶已停用]**：傳送至已不存在的電子郵件地址時，所產生的錯誤型別。
* **[!UICONTROL 信箱已滿]**：收件者的收件匣已滿時產生的錯誤型別。 在產生此錯誤之前，會嘗試五次傳遞訊息。
* **[!UICONTROL 未連線]**：收件者的行動電話已關機或傳送訊息時未連線至網路時產生的錯誤型別。

  >[!NOTE]
  >
  >這類錯誤只與行動裝置頻道上的傳遞有關。

* **[!UICONTROL 已拒絕]**：當網際網路服務提供者(ISP)拒絕位址時產生的錯誤型別。 例如，反垃圾郵件軟體已套用安全性規則時。

**網域重新分割**&#x200B;表格會顯示根據收件者網域進行傳遞時遇到的整體問題。
