---
title: 建立設定檔維度
description: 瞭解如何根據設定檔資料建立設定檔維度。
audience: reporting
content-type: reference
level: Intermediate
exl-id: a12dc772-13c7-45ff-9fbf-3dfdd3801eae
TQID: https://experienceleague.adobe.com/eru99ME-JlrcRl074heBXwVhBLgeQJaQdiJkM-QT2SY
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
feature_v2: id: fdbb8fc9-ffa3-4b86-88fe-aa4c5a3e1bc6
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: ad84694f2f6f45e4ee30fc51379106835ac302be
workflow-type: tm+mt
source-wordcount: 517
ht-degree: 3%

---

# 建立設定檔維度{#creating-a-custom-profile-dimension}

您也可以根據在收件者方案擴充功能期間建立的設定檔資料，來建立和管理報表。

* [步驟1：擴充收件者綱要](##extend-schema)
* [步驟2：連結您的新自訂欄位](#link-custom)
* [步驟3：建立動態報告，以使用設定檔維度篩選收件者](#create-report)

## 步驟1：擴充收件者綱要 {#extend-schema}

若要新增設定檔欄位，您需要擴充結構，請遵循下列步驟：

1. 瀏覽至總管中的&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 組態]** > **[!UICONTROL 資料結構描述]**&#x200B;資料夾。

   ![](assets/custom_field_1.png)

1. 識別您的自訂收件者綱要並加以選取。 如果您尚未擴充內建nms:recipient結構描述，請參閱[此程式](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/developer/shemas-forms/extend-schema)。

1. 將您的自訂欄位新增到結構描述編輯器。

   例如，若要在收件者綱要中新增「忠誠度」自訂欄位：

   ```
   <attribute label="Loyalty" name="loyalty" type="string"/>
   ```

   ![](assets/custom_field_2.png)

1. 按一下&#x200B;**[!UICONTROL 儲存]**。

1. 然後，識別您的自訂broadLogRcp結構描述並加以選取。 如果您尚未擴充內建的傳遞記錄結構描述，請參閱[此程式](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/developer/shemas-forms/extend-schema)。

1. 將和收件者結構描述相同的自訂欄位新增到結構描述編輯器。

   ![](assets/custom_field_3.png)

1. 按一下&#x200B;**[!UICONTROL 儲存]**。

1. 若要套用對結構描述所做的修改，請透過&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 進階]** > **[!UICONTROL 更新資料庫結構]**&#x200B;啟動資料庫更新精靈，然後執行更新資料庫結構。 [了解更多](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/developer/shemas-forms/update-database-structure)

   ![](assets/custom_field_4.png)

您的新設定檔欄位現在已可供收件者使用及選取。

## 步驟2：連結您的新自訂欄位 {#link-custom}

>[!NOTE]
>
> 您最多只能新增20個自訂欄位至動態報表。

現在您的設定檔欄位已建立，我們需要將其連結至對應的動態報告維度。

在使用我們的設定檔欄位擴充記錄前，請確定已接受PII視窗，以便能夠將PII資料傳送至動態報表。 如需關於此項目的詳細資訊，請參閱此[頁面](pii-agreement.md)。

1. 導覽至Explorer中的&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 組態]** > **[!UICONTROL 資料結構描述]** > **[!UICONTROL 其他報告欄位]**&#x200B;資料夾。

   ![](assets/custom_field_5.png)

1. 按一下&#x200B;**[!UICONTROL 新增]**&#x200B;以建立您對應的動態報告維度。

1. 選取&#x200B;**[!UICONTROL 編輯運算式]**&#x200B;並瀏覽收件者結構描述以尋找您先前建立的設定檔欄位。

   ![](assets/custom_field_6.png)

1. 按一下&#x200B;**[!UICONTROL 完成]**。

1. 輸入維度&#x200B;**[!UICONTROL 標籤]** （顯示在動態報告中），然後按一下&#x200B;**[!UICONTROL 儲存]**。

   ![](assets/custom_field_7.png)

您的設定檔欄位現在可作為報告中的設定檔維度。 若要刪除您的設定檔維度，您可以選取該維度，然後按一下&#x200B;**[!UICONTROL 刪除]**&#x200B;圖示。

現在，收件者綱要已使用此設定檔欄位擴充，並且已建立您的自訂維度，您可以在傳送中開始鎖定收件者。

## 步驟3：建立動態報告，以使用設定檔維度篩選收件者 {#create-report}

傳送傳遞後，您可以使用設定檔維度來劃分報表。

1. 從&#x200B;**[!UICONTROL 報表]**&#x200B;索引標籤中，選取現成可用的報表，或按一下&#x200B;**[!UICONTROL 建立]**&#x200B;按鈕，從頭開始建立。

   ![](assets/custom_field_8.png)

1. 在&#x200B;**[!UICONTROL 維度]**&#x200B;類別中，按一下&#x200B;**[!UICONTROL 設定檔]**，然後將您的設定檔維度拖放至自由表格。

   ![](assets/custom_field_9.png)

1. 拖放任何量度以開始篩選資料。

1. 視需要在工作區中拖放視覺效果。

