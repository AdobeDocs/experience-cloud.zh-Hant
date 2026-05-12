---
title: 開始使用動態報告
description: 進一步瞭解動態報告使用協定
level: Beginner
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限已移轉Campaign Standard的使用者使用"
audience: end-user
exl-id: 9fcef466-f306-480e-b42e-d18daa8bcf06
TQID: https://experienceleague.adobe.com/AGXqq-XOQU8SmHobDIA-nZqw3eNSa2THnw2jQQP54YA
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
feature_v2:
  - id: fdbb8fc9-ffa3-4b86-88fe-aa4c5a3e1bc6
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: ad84694f2f6f45e4ee30fc51379106835ac302be
workflow-type: tm+mt
source-wordcount: 549
ht-degree: 2%

---

# 動態報告使用合約 {#pii-agreement}

動態報告使用合約的目的是當做資料處理的快顯同意。 依預設，協定僅可見，且僅能被指派管理許可權的使用者接受或拒絕。

若要存取動態報告使用協定，請選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 進階]** > **[!UICONTROL 部署精靈]**。

![](assets/pii-agreement.png)

有三個可用選項：

* **[!UICONTROL 稍後再問我]**：在您接受或拒絕合約之前，設定檔維度不會出現在您的報告中，而且不會收集或傳送您客戶的個人識別資訊。
* **[!UICONTROL 接受]**：一旦接受此合約，即表示您授權Adobe Campaign收集客戶的個人識別資訊，並將這些資訊傳輸至報表或資料中心。
* **[!UICONTROL 拒絕]**：拒絕合約後，設定檔維度將不會出現在您的報告中，也不會收集或傳送您客戶的個人識別資訊。 請注意，在此情況下，仍會收集externalID並使用其識別一般使用者。

下表會依據您所在的區域，顯示接受此合約後會發生什麼事。

|  | 動態報告 | Microsoft Dynamics 365聯結器 |
|---|---|---|
| 美洲和APAC （亞太） | **功能可用**。 <br>所有立即可用（亦即城市、國家/地區、州、性別和年齡區段）與推播至美國報告中心的自訂設定檔資訊。 | **功能可用**。 <br>所有現成可用的和自訂設定檔欄位和Adobe Campaign事件欄位都在美國資料中心處理。 |
| EMEA （歐洲、中東及非洲） | **功能可用**。 <br>所有現成可用的資訊（亦即根據年齡區分的城市、國家/地區、州、性別和區段），以及推播至EMEA報告中心的自訂設定檔資訊。 | **功能可用。** <br>所有現成可用的與自訂設定檔欄位，以及EMEA資料中心處理的Adobe Campaign事件欄位。 <br>**[!UICONTROL 控制資料&#x200B;]**，其中包含Adobe I/O註冊資料以及傳送並儲存在美國資料中心的客戶一般使用者事件識別碼。 |

下表顯示根據您所在的地區，拒絕此合約後會發生什麼事情。 請注意，即使您拒絕此合約，仍可提供有關傳遞和Microsoft Dynamics 365整合的報告。

| 區域 | 動態報告 | Microsoft Dynamics 365聯結器 |
|---|---|---|
| 美洲和APAC （亞太） | **可用功能**。<br> 除了ExternalID，沒有現成可用的和自訂設定檔資訊推送至美國報表中心。 | **功能可用**。 <br>除了外部ID和收件者ID之外，沒有現成可用的或自訂的設定檔欄位傳送至美國資料中心。 <br>所有Adobe Campaign事件欄位都在美國資料中心處理，但映象頁面ID除外。 |
| EMEA （歐洲、中東及非洲） | **功能可用**。 <br>除了ExternalID之外，沒有現成可用的和自訂設定檔資訊推送至EMEA報告中心。 | **功能可用。** <br>除了外部ID和收件者ID之外，沒有現成可用的或自訂的設定檔欄位傳送至EMEA資料中心。 <br>所有Adobe Campaign事件欄位都在EMEA資料中心處理，但映象頁面ID除外。 |

這個選擇不是最終選擇，您可以隨時變更它，只要在&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 平台]** > **[!UICONTROL 選項]**&#x200B;中選取&#x200B;**[!UICONTROL realtimeReporting_collectPII]**&#x200B;選項。

此值可隨時變更。 值1對應至&#x200B;**[!UICONTROL 稍後詢問我]**、2 **[!UICONTROL 拒絕]**&#x200B;和3 **[!UICONTROL 接受]**。
