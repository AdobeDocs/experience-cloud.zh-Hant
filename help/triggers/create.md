---
title: 建立和管理 Experience Cloud 觸發器
description: 探索 Adobe Experience Cloud 觸發器 UI
hide: true
hidefromtoc: true
source-git-commit: ce0faf9fab45c931feb666ac0c77f5ab5c231746
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 建立 Experience Cloud 觸發器 {#create-triggers}

>[!NOTE]
>
> Experience Cloud觸發器的新使用者介面提供直覺式體驗，以管理消費者行為並個人化使用者體驗。 若要切換回上一個介面，請按一下 **[!UICONTROL 轉到傳統模式]** 按鈕。

建立觸發器並設定觸發器的條件。例如，您可以指定造訪期間觸發器規則的條件，例如「購物車放棄」等量度，或產品名稱等維度。符合規則時，觸發器就會執行。

1. 在Experience Cloud中，依序選取進階功能表和觸發器。

   ![](assets/triggers_7.png)

1. 在您的觸發程式首頁，按一下 **[!UICONTROL 建立觸發程式]**，然後指定觸發器的類型。

   有三種觸發器類型可供使用：

   * **[!UICONTROL 放棄]**:您可以建立觸發器，在訪客檢視產品但未新增任何項目至購物車時引發。

   * **[!UICONTROL 動作]**:例如，您可以建立觸發器，在電子報註冊、電子郵件訂閱或信用卡申請（確認）後引發。 如果您是零售商，可針對註冊忠誠度計畫的訪客建立觸發器。若為媒體和娛樂產業，可針對觀看特定節目的訪客建立觸發器，而您可能會想透過意見調查給予回應。

   * **[!UICONTROL 工作階段開始和工作階段結束]**:為工作階段開始和工作階段結束事件建立觸發器。

   ![](assets/triggers_1.png)

1. 新增 **[!UICONTROL 名稱]** 和 **[!UICONTROL 說明]** 觸發器。

1. 選取Analytics **[!UICONTROL 報表套裝]** 用於此觸發器。 此設定可識別要使用的報表資料。

   [進一步了解報表套裝](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite.html).

1. 選擇 **[!UICONTROL 無動作時觸發]** 有效期。

1. 從 **[!UICONTROL 瀏覽必須包括]** 和 **[!UICONTROL 瀏覽不得包括]** 類別中，您可以定義要或不要發生的條件或訪客行為。 您可以指定 **和** 或 **或** 條件內或條件之間的邏輯，視您決定的准則而定。

   例如，簡單的購物車丟棄觸發器的規則可能是：

   * **[!UICONTROL 瀏覽必須包括]**: `Carts (metric) Is greater or equal to 1` 以定位購物車中至少包含一項的訪客。
   * **[!UICONTROL 瀏覽不得包括]**: `Checkout (metric) Exists.` 移除購物車中購買項目的訪客。

   ![](assets/triggers_2.png)

1. 按一下 **[!UICONTROL 容器]** 建立並儲存定義觸發器的規則、條件或篩選器。 若要讓事件同時發生，您應將其置於相同的容器中。

   每個容器在點擊層級獨立處理，這表示如果兩個容器以 **[!UICONTROL 和]** 運算元，則規則只有在兩個點擊符合要求時才符合資格。

1. 從 **[!UICONTROL 中繼資料]** 欄位，按一下 **[!UICONTROL +Dimension]** 選擇與訪客行為相關的特定促銷活動維度或變數。

   ![](assets/triggers_3.png)

1. 按一下「**[!UICONTROL 儲存]**」。

1. 選取新建立的 **[!UICONTROL 觸發]** ，存取觸發器的詳細資料報表。

   ![](assets/triggers_4.png)

1. 從觸發器的詳細檢視中，您可以存取關於觸發數的報表。 如有需要，您可以使用鉛筆圖示編輯觸發器。

   ![](assets/triggers_5.png)
