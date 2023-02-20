---
title: 全局隱藏清單
description: 發現全局隱藏清單
hide: true
source-git-commit: a946cfb1027896f6e45aaf88d25ad7114d6b5ac6
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# 全局隱藏清單 {#global-suppression-list}

隱藏清單包含客戶希望從其傳送中排除的電子郵件地址，因為向這些聯繫人發送可能會損害其發送信譽和傳送率。 目前，Adobe會保留已知錯誤電子郵件地址的更新清單，這些地址已被證明對參與和郵件信譽有損，並確保不會向他們發送電子郵件。 此清單會以全域隱藏清單來管理，所有Adobe客戶都會看到這份清單。 全局隱藏清單中包含的地址和域名將被隱藏。 傳送報告中只會指出已排除的收件者數目。

現在可以從內部可用的介面管理全局隱藏清單。 此清單僅由傳遞能力顧問維護。 全域隱藏清單可包含電子郵件或網域地址。

## 訪問全局隱藏清單

若要存取排除的電子郵件地址和網域的詳細清單，請前往 **[!UICONTROL 全域隱藏清單]**.

>[!CAUTION]
>
>查看、導出和管理全局隱藏清單的權限取決於分配給的通訊組清單。 更多詳情

畫面上會顯示兩個標籤： **[!UICONTROL 電子郵件]** 和 **[!UICONTROL 網域]**.

篩選器可協助您瀏覽清單。

## 新增地址和網域

目前，將地址添加到全局隱藏清單的方法有兩種：

* 由傳遞團隊組織的清單。
* 由第三方服務提供商Blackbox提供的清單。

您可以新增電子郵件地址或網域 [一次一個](#add-one-address-or-domain)，或 [在大量模式中](#upload-csv-file) 透過CSV檔案上傳。

若要這麼做，請選取 **[!UICONTROL 新增電子郵件或網域]** 按鈕，然後遵循以下方法之一。

### 添加一個地址或域 {#add-one-address-or-domain}

1. 選取 **[!UICONTROL 逐一]** 選項。

1. 選擇地址類型： **[!UICONTROL 電子郵件地址]** 或 **[!UICONTROL 網域位址]**.

1. 輸入要從傳送中排除的電子郵件地址或網域。

   >[!NOTE]
   >
   >請務必輸入有效的電子郵件地址(如abc@company.com)或網域（如abc.company.com）。

1. 視需要指定原因。

   >[!NOTE]
   >
   >此欄位允許包含32到126之間的所有ASCII可打印字元。 您可以在 [本頁](https://en.wikipedia.org/wiki/Wikipedia:ASCII#ASCII_printable_characters){target="_blank"} 例如，

1. 按一下 **[!UICONTROL 提交]** 確認。

### 上傳CSV檔案 {#upload-csv-file}

1. 選取 **[!UICONTROL 上傳CSV]** 選項。

1. 下載要使用的CSV範本，其中包含下列欄和格式：

   ```
   TYPE,VALUE,COMMENT
   EMAIL,abc@somedomain.com,Comment
   DOMAIN,somedomain.com,Comment
   ```
   >[!CAUTION]
   >
   >請勿變更CSV範本中的欄名稱。
   >
   >檔案大小不應超過1 MB。

1. 在CSV範本中填入您要新增至隱藏清單的電子郵件地址和/或網域。

   >[!NOTE]
   >
   >在 **註解** 欄。 您可以在 [本頁](https://en.wikipedia.org/wiki/Wikipedia:ASCII#ASCII_printable_characters){target="_blank"} 例如，

1. 完成後，拖放CSV檔案，然後按一下 **[!UICONTROL 提交]** 確認。

>[!NOTE]
>
>上傳完成後，請從介面檢查狀態，以確定上傳成功。 [了解如何](#recent-uploads)

### 檢查最近的上載狀態 {#recent-uploads}

按一下 **[!UICONTROL 最近上載]** 按鈕，以檢查您上傳的最新CSV檔案的狀態。

可能的狀態包括：

* **[!UICONTROL 待定]**:檔案上傳正在處理中。
* **[!UICONTROL 錯誤]**:檔案上傳程式因技術問題或檔案格式錯誤而失敗。
* **[!UICONTROL 完成]**:檔案上載過程已成功完成。

在上傳期間，如果某些位址的格式不正確，則不會將其新增至全域隱藏清單。

在這種情況下，上傳完成時，就會與報表相關聯。 您可以下載它以檢查遇到的錯誤。

## 刪除地址

要從全局隱藏清單中刪除地址，請使用 **[!UICONTROL 刪除]** 按鈕。

>[!CAUTION]
>
>顧問無法透過介面移除由第三方服務提供者Blackbox自動新增的位址或網域。 這只能透過後端票證完成。

