---
title: 設定API存取
description: 瞭解如何設定Campaign Standard API的存取許可權。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
exl-id: efbbd0cd-9c56-4ad0-8bcb-efba4b63c28b
source-git-commit: 18979fea28f4f3adce1139293203a59876831313
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 27%

---

# 設定 API 存取 {#setting-up-api-access}

Adobe Campaign Standard API存取權是透過下列步驟設定。 [Adobe Developer檔案](https://developer.adobe.com/developer-console/docs/guides/#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md)中會詳細說明這些步驟。

>[!IMPORTANT]
>
>若要在[Adobe Developer](https://developer.adobe.com/)中管理憑證，請確定您對該組織具有&#x200B;**系統管理員**&#x200B;許可權，或在Admin Console中具有[開發人員帳戶](https://helpx.adobe.com/jp/enterprise/using/manage-developers.html)。

1. **請確認您擁有數位憑證**，或視需要建立。 下列步驟需要憑證隨附的公開金鑰與私人金鑰。
1. **在[Adobe Developer](https://developer.adobe.com/)中建立與Adobe Campaign服務的新整合**&#x200B;並加以設定。 然後，將產生您的認證 (API 金鑰、用戶端密碼……)。
1. **依照下列[實作步驟，建立OAuth伺服器對伺服器**&#x200B;認證](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)

   >[!IMPORTANT]
   >
   >JWT (JSON Web 權杖) 目前正在折舊中，並即將由 OAuth 取代。此轉換將在Campaign即將發行的版本中逐步執行。 服務帳戶(JWT)憑證已標示為已棄用，並將繼續使用至2025年1月27日。 因此，您必須移轉應用程式或整合，才能在2025年1月27日之前使用新的OAuth伺服器對伺服器認證。 建議使用OAuth驗證。 您將在以下頁面上找到要從JWT驗證移轉至OAuth驗證的所有元素：
   >* [移轉](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)
   >* [實作](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)
   >* [棄用JWT常見問題集](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/faqs/)

若要建立安全的服務對服務 Adobe I/O API 工作階段，對 Adobe 服務的每個請求都必須在授權標題中包含下列資訊。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

* **&lt;組織>**：這是您的個人組織ID，Adobe會為您每個執行個體提供一個組織ID：

   * &lt;組織> ：您的生產執行個體，
   * &lt;ORGANIZATION-mkt-stage>：您的階段例項。

  若要取得組織 ID 值，請洽詢您的管理員或 Adobe 技術聯絡人。 您也可以在建立新整合時，在授權清單中將其擷取到Adobe I/O (請參閱<a href="https://developer.adobe.com/developer-console/docs/guides/authentication/">Adobe Developer檔案</a>)。

* **&lt;ACCESS_TOKEN>**：您的個人存取權杖，這是透過POST要求交換您的JSON Web Token時擷取的。

* **&lt;API_KEY>**：您的個人 API 金鑰。 在建立Adobe Campaign服務的新整合後，以Adobe I/O提供。

  ![替代文字](assets/tenant.png)

## 疑難排解

在AdobeIO整合期間，如果出現下列錯誤：

```
{ 
"code": 502, 
"message": "Oops. Something went wrong. Check your URI and try again." 
}
```


請洽詢您的管理員或您的Adobe技術連絡人，以檢查CNAME引數是否正確建立。
