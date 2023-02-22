---
title: 全球禁止名單
description: 探索全球禁止名單
hide: true
source-git-commit: a946cfb1027896f6e45aaf88d25ad7114d6b5ac6
workflow-type: ht
source-wordcount: '628'
ht-degree: 100%

---

# 全球禁止名單 {#global-suppression-list}

禁止名單包含客戶要從傳遞中排除的電子郵件地址，因為傳送給這些聯絡人可能會損害他們的傳送信譽和傳遞率。 目前，Adobe 保有一份更新清單，當中列有已證明對參與度和郵寄信譽有害的已知不良電子郵件地址，並且會確保不將電子郵件傳送到這些地址。 此清單在所有 Adobe 客戶通用的全球禁止名單中進行管理。 全球禁止名單中包含的地址和網域名稱都會隱藏起來。 傳遞報告中僅顯示排除的收件者人數。

現在可以從內部可用的介面管理全球禁止名單。 此清單僅由交付顧問維護。 全球禁止名單可以包括電子郵件或網域地址。

## 存取全球禁止名單

要存取排除的電子郵件地址和網域的詳細清單，請前往&#x200B;**[!UICONTROL 全球禁止名單]**。

>[!CAUTION]
>
>檢視、匯出和管理全球禁止名單的權限取決於指派給您的分送清單。更多詳情

會顯示兩個標籤：**[!UICONTROL 電子郵件]**&#x200B;和&#x200B;**[!UICONTROL 網域]**。

篩選器可幫助您瀏覽清單。

## 新增地址和網域

目前有兩種方式可以將地址加入全球禁止名單：

* 由交付團隊策劃的清單。
* 由協力廠商服務提供者 Blackbox 提供的清單。

您可以[一次新增一個](#add-one-address-or-domain)電子郵件地址或網域，或[在大量模式中](#upload-csv-file)透過 CSV 檔案上傳的方式新增。

若要這麼做，請選取「**[!UICONTROL 新增電子郵件或網域]**」按鈕，然後按照以下方法之一操作。

### 新增一個地址或網域 {#add-one-address-or-domain}

1. 選取「**[!UICONTROL 逐一]**」選項。

1. 選擇地址類型：**[!UICONTROL 電子郵件地址]**&#x200B;或&#x200B;**[!UICONTROL 網域地址]**。

1. 輸入您要從傳送中排除的電子郵件地址或網域。

   >[!NOTE]
   >
   >確定輸入有效的電子郵件地址 (例如 abc@company.com) 或網域 (例如 abc.company.com)。

1. 如果需要，請指定原因。

   >[!NOTE]
   >
   >此欄位允許包含 32 到 126 個字元之間組成的所有 ASCII 可列印字元。 例如，完整清單可在[此頁面](https://en.wikipedia.org/wiki/Wikipedia:ASCII#ASCII_printable_characters){target="_blank"}中找到。

1. 按一下「**[!UICONTROL 提交]**」進行確認。

### 上傳 CSV 檔案 {#upload-csv-file}

1. 選取「**[!UICONTROL 上傳 CSV]**」選項。

1. 下載要使用的 CSV 範本，其中包括以下欄和格式：

   ```
   TYPE,VALUE,COMMENT
   EMAIL,abc@somedomain.com,Comment
   DOMAIN,somedomain.com,Comment
   ```

   >[!CAUTION]
   >
   >請勿變更 CSV 範本中的欄名。
   >
   >檔案大小不應超過 1 MB。

1. 將您要新增到禁止名單的電子郵件地址和/或網域填入 CSV 範本。

   >[!NOTE]
   >
   >「**註解**」欄允許包含 32 到 126 個字元之間組成的所有 ASCII 可列印字元。 例如，完整清單可在[此頁面](https://en.wikipedia.org/wiki/Wikipedia:ASCII#ASCII_printable_characters){target="_blank"}中找到。

1. 完成後，拖放您的 CSV 檔案，然後按一下「**[!UICONTROL 提交]**」進行確認。

>[!NOTE]
>
>上傳完成後，從介面檢查其狀態以確保上傳成功。[了解作法](#recent-uploads)

### 檢查最近的上傳狀態 {#recent-uploads}

按一下「**[!UICONTROL 最近上傳]**」按鈕，檢查您上傳的最新 CSV 檔案的狀態。

可能的狀態有：

* **[!UICONTROL 擱置中]**：檔案上傳正在處理中。
* **[!UICONTROL 錯誤]**：由於技術問題或檔案格式錯誤，文件上傳過程失敗。
* **[!UICONTROL 完成]**：檔案上傳過程已成功完成。

上傳過程中，如果部分地址格式不正確，則不會加入全球禁止名單。

在這種情況下，上傳完成後，即會與報告相關聯。 您可以下載來檢查遇到的錯誤。

## 移除地址

要從全球禁止名單中移除地址，請使用「**[!UICONTROL 刪除]**」按鈕。

>[!CAUTION]
>
>顧問無法透過介面移除協力廠商服務提供者 Blackbox 自動新增的地址或網域。這只能透過後端票證來完成。

