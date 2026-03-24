---
title: 取得應用程式的使用者端ID
description: 瞭解如何在Experience Rollout主控台中找到應用程式的數值使用者端ID，這是呼叫管理API時的必要專案。
source-git-commit: 6ecedbfc6c7de392f214f3f8f2e71aa18e1bacb9
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 1%

---


# 取得應用程式的使用者端ID {#get-client-id}

功能標幟和功能群組管理API需要數值`clientId`來識別該功能屬於哪個應用程式。 這與用於API驗證的字串型IMS使用者端ID不同。

請依照下列步驟，尋找應用程式的數值使用者端ID。

## 步驟 {#steps}

若要尋找應用程式的數值使用者端ID，請遵循下列步驟：

1. 登入「體驗轉出」主控台。
2. 瀏覽至&#x200B;**功能與版本**。
3. 選取&#x200B;**功能旗標**&#x200B;標籤。
4. 開啟&#x200B;**Application**&#x200B;下拉式清單，並選取您需要的使用者端識別碼的應用程式。
5. 檢視瀏覽器位址列中的URL。 在`feature-flags/`之後，顯示的數字是該應用程式的數值使用者端ID。

例如，如果URL結尾為`.../feature-flags/1191/...`，則使用者端識別碼為`1191`。

## 在API呼叫中使用使用者端ID {#use-in-api}

將此值作為管理API要求中的`clientId`引數傳遞。 例如，在建立功能標幟時：

```json
{
  "name": "my-feature-flag",
  "clientId": 1191,
  "state": "disabled"
}
```

## 另請參閱 {#see-also}

* [功能標幟管理API](feature-flags-management-api.md)
* [功能群組管理API](feature-group-management-api.md)
* [取得所需的對象條件](get-audience-criteria.md)
