---
title: 退回摘要
description: 使用彈回摘要現成可用報告，瞭解您傳送的行銷活動狀態及其可能遇到的錯誤。
audience: end-user
level: Intermediate
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
source-git-commit: 3f4400f24b75e8e435610afbe49e9d9444dbf563
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---

# 退回摘要{#bounce-summary}

此報表詳細說明傳送期間遇到的整體硬式和軟式錯誤，以及自動處理退信。

![](assets/campaign_reports_bounces.png)

每個表格都由摘要數字和圖表表示。 您可以變更詳細資訊在其各自視覺效果設定中的顯示方式。

**失敗5重新分割** 列出隔離數量最多的五個傳送：

此 **退回原因** 此表格含有可造成每次傳送退回的錯誤型別可用資料：

* **[!UICONTROL 使用者不明]**：將傳遞傳送至無效的電子郵件地址時產生的錯誤型別。
* **[!UICONTROL 無效的網域]**：將傳遞傳送至網域錯誤或不再存在的電子郵件地址時產生的錯誤型別。
* **[!UICONTROL 無法聯絡]**：在訊息傳送字串中遇到的錯誤型別，例如暫時無法存取網域。
* **[!UICONTROL 帳戶已停用]**：將傳遞傳送至已不存在的電子郵件地址時產生的錯誤型別。
* **[!UICONTROL 郵箱已滿]**：收件者的收件匣已滿時產生的錯誤型別。 在產生此錯誤之前，會嘗試五次傳遞訊息。
* **[!UICONTROL 未連線]**：收件者的行動電話關閉或在傳送訊息時未連線至網路時產生的錯誤型別。

  >[!NOTE]
  >
  >這類錯誤只與行動裝置頻道上的傳遞有關。

* **[!UICONTROL 已拒絕]**：網際網路服務提供者(ISP)拒絕位址時產生的錯誤型別。 例如，反垃圾郵件軟體已套用安全性規則時。

此 **網域重新分割** 此表格會根據收件者網域顯示傳送期間遇到的整體問題。
