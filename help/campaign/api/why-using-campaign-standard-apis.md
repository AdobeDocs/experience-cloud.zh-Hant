---
title: 為何要使用Campaign Standard API？
description: 進一步瞭解Campaign Standard API及為何使用。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
source-git-commit: 84b72258789ba61016deb813e93bdca0ea142712
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 2%

---

# 為何使用Campaign Standard API {#why-using-campaign-standard-apis}

Adobe Campaign Standard提供的API可讓現有系統與Campaign平台整合，以即時解決現實世界中的問題。

公開網站（例如註冊或退出頁面）需要連線至後端系統以儲存設定檔資訊。 Adobe Campaign等後端系統擁有彈性和功能，可將設定檔資料擷取到其中並對其執行自訂操作。

以下是一些範例：

* 潛在客戶線上註冊。
* 現有的客戶設定檔和行銷通訊偏好設定管理。
* 基於事件的交易式通訊觸發 — 訂單確認、預訂行程、密碼重設等。
* 甚至放棄電子郵件通訊。

註冊登入頁面可為客戶或潛在客戶提供登入其名稱和電子郵件地址的方法。 Campaign Standard擷取設定檔資訊和偏好設定後，就可以根據使用者的興趣傳送個人化訊息。

使用下列元素建置：

1. 包含Campaign API接聽程式的登錄檔單。

   ![替代文字](assets/apis_uc1.png)

1. 根據核取方塊要採取的自訂動作。 與一般註冊程式相比，選取「電子郵件特殊優惠」的客戶會收到一封包含贈券的不同自訂郵件。

   ![替代文字](assets/apis_uc2.png)

1. 設定檔在按一下電子郵件中的「更新詳細資訊」連結後，可能會變更其詳細資訊。 這會將設定檔帶至「更新您的設定檔和偏好設定詳細資料」頁面。 為了執行操作，設定檔詳細資訊(Pkey)會傳遞至Campaign伺服器，並擷取及表示設定檔。 一旦設定檔按一下「更新」按鈕，資訊就會更新到系統中(透過PATCH命令)。

   ![替代文字](assets/apis_uc3.png)

請求集合可協助您熟悉Campaign Standard API請求。 此集合以JSON格式提供，預先設計的API要求代表常見的使用案例。

以下步驟說明匯入並使用集合在Campaign Standard資料庫中建立設定檔的逐步使用案例。

>[!NOTE]
>
>我們的範例使用Postman。 不過，您可以隨意使用您最愛的REST使用者端。

1. 按一下「 」以下載JSON集合 [此處](https://helpx.adobe.com/content/dam/help/en/campaign/kb/working-with-acs-api/_jcr_content/main-pars/download_section/download-1/KB_postman_collection.json.zip).

1. 開啟Postman，然後選取 **檔案** / **匯入** 功能表。

1. 將下載的檔案拖放至視窗中。 預先設計的API要求隨即顯示，可供使用。

   ![替代文字](assets/postman_collection.png)

1. 選取 **建立設定檔** 請求，然後更新POST請求和 **標頭** 以您自己的資訊定位(&lt;organization>， &lt;api_key>， &lt;access_token>)。 如需詳細資訊，請參閱[本章節](setting-up-api-access.md)。

   ![替代文字](assets/postman_uc1.png)

1. 填入 **內文** 以您要新增至新設定檔的資訊標籤，然後按一下 **傳送** 按鈕以執行要求。

   ![替代文字](assets/postman_uc2.png)

1. 建立物件後，就會有主索引鍵(PKey)與其相關聯。 它會顯示於要求回應中，以及其他屬性中。

   ![替代文字](assets/postman_uc3.png)

1. 開啟您的Campaign Standard例項，然後檢查設定檔是否已建立，包含來自裝載的所有資訊。

   ![替代文字](assets/postman_uc4.png)
