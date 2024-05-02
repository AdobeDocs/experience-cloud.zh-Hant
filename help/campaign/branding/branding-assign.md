---
title: 品牌
description: 瞭解如何指派您的品牌
audience: administration
context-tags: branding,overview;branding,main
role: Admin
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
source-git-commit: 51abadc86b97097d13824651d8c50d4ddd014a51
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 18%

---

# 指派您的品牌 {#branding-assign}

>[!IMPORTANT]
>
>品牌推廣選專案前僅限於電子郵件和推播傳遞。

## 將品牌連結至範本 {#linking-a-brand-to-a-template}

若要使用為品牌定義的引數，必須將其連結至傳遞範本。 您必須建立或編輯範本，才能執行此操作。

您的範本將連結至品牌。 在電子郵件編輯工具中，「 **預設寄件者的電子郵件地址**」、「 **預設寄件者名稱**」或「 **Logo** 」等元素將使用已設定的品牌資料。

>[!BEGINTABS]

>[!TAB Adobe Campaign V8]

若要建立傳遞範本，您可以複製內建範本、將現有傳遞轉換為範本或從頭開始建立傳遞範本。 [了解更多](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/create-templates)

建立範本後，您就可以將其連結至品牌。執行方法：

1. 瀏覽至 **[!UICONTROL 資源]** `>` **[!UICONTROL 範本]** `>` **[!UICONTROL 傳遞範本]** 在Adobe Campaign explorer中。

1. 選取傳遞範本或複製現有範本。

   ![](assets/branding_assign_V8_1.png)

1. 存取 **[!UICONTROL 屬性]** 所選傳遞範本的ID。

   ![](assets/branding_assign_V8_2.png)

1. 從 **[!UICONTROL 一般]** 索引標籤中，選取您的品牌 **[!UICONTROL 品牌化]** 下拉式清單。

   ![](assets/branding_assign_V8_3.png)

1. 設定後，選取 **確定**.

您現在可以使用此範本來傳送您的傳遞。

>[!TAB Adobe Campaign Web]

若要建立傳遞範本，您可以複製內建範本、將現有傳遞轉換為範本或從頭開始建立傳遞範本。 [了解更多](https://experienceleague.adobe.com/en/docs/campaign-web/v8/msg/delivery-template)

建立範本後，您就可以將其連結至品牌。執行方法：

1. 瀏覽至 **[!UICONTROL 範本]** 標籤，從 **[!UICONTROL 傳遞]** 左側功能表，並選取傳遞範本。

   ![](assets/branding_assign_web_1.png)

1. 按一下 **[!UICONTROL 設定]**.

   ![](assets/branding_assign_web_2.png)

1. 從 **[!UICONTROL 傳遞]** 標籤，存取 **[!UICONTROL 品牌化]** 欄位並選取您要連結至範本的品牌。

   ![](assets/branding_assign_web_3.png)

1. 確認您所選的項目並儲存範本。

您現在可以使用此範本來傳送您的傳遞。

>[!ENDTABS]

## 指派品牌給您的傳遞 {#assigning-a-brand-to-an-email}

>[!BEGINTABS]

>[!TAB Adobe Campaign V8]

若要建立新的獨立傳送，請遵循下列步驟。

1. 若要建立新傳遞，請瀏覽至 **[!UICONTROL 行銷活動]** 標籤。

1. 按一下 **[!UICONTROL 傳遞]** 並按一下 **[!UICONTROL 建立]** 按鈕。

   ![](assets/branding_assign_V8_4.png)

1. 選取傳遞範本。

1. 存取 **[!UICONTROL 屬性]** 所選傳遞範本的ID。

   ![](assets/branding_assign_V8_5.png)

1. 從 **[!UICONTROL 一般]** 索引標籤中，選取您的品牌 **[!UICONTROL 品牌化]** 下拉式清單。

   ![](assets/branding_assign_V8_6.png)

1. 設定後，選取 **確定**.

1. 進一步個人化您的傳遞。 如需建立電子郵件的詳細資訊，請參閱 [設計和傳送電子郵件](https://experienceleague.adobe.com/en/docs/campaign-web/v8/msg/email/create-email) 區段。

>[!TAB Adobe Campaign Web]

若要建立新的獨立傳送，請遵循下列步驟。

1. 瀏覽至 **[!UICONTROL 傳遞]** 功能表，然後按一下 **[!UICONTROL 建立傳遞]** 按鈕。

   ![](assets/branding_assign_web_4.png)

1. 選取電子郵件或推播通知作為頻道，然後從清單中選擇傳遞範本。

1. 按一下「**[!UICONTROL 建立傳遞]**」按鈕以確認。

1. 從 **[!UICONTROL 屬性]** 頁面，按一下 **[!UICONTROL 設定]**.

   ![](assets/branding_assign_web_5.png)

1. 從 **[!UICONTROL 傳遞]** 標籤，存取 **[!UICONTROL 品牌化]** 欄位。

   ![](assets/branding_assign_web_6.png)

1. 選取您要連結至範本的品牌。

   ![](assets/branding_assign_web_7.png)

1. 進一步個人化您的傳遞。 如需建立電子郵件的詳細資訊，請參閱 [建立您的第一封電子郵件](https://experienceleague.adobe.com/en/docs/campaign-web/v8/msg/email/create-email) 區段。

>[!ENDTABS]
