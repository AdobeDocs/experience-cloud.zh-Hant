---
title: 取得所需的對象條件
description: 瞭解如何使用主控台和GET功能API，產生正確的對象條件JSON結構以用於體驗轉出管理API。
source-git-commit: 6ecedbfc6c7de392f214f3f8f2e71aa18e1bacb9
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 1%

---


# 取得所需的對象條件 {#get-audience-criteria}

管理API中的對象條件欄位使用結構化JSON格式，手寫時可能會很複雜。 建議的方法是使用主控台建置所要的對象，然後透過API擷取其JSON表示法。

## 步驟 {#steps}

若要針對所需的對象條件取得JSON，請執行以下步驟：

1. 在「體驗轉出」主控台中，以您要在API呼叫中使用的對象條件建立暫時功能標幟。
2. 儲存後，請注意瀏覽器URL中的功能標幟ID。 ID會顯示在使用者端ID之後的URL中。 例如，在`.../feature-flags/1191/22080`中，功能識別碼為`22080`。
3. 使用功能ID呼叫[依ID](feature-flags-management-api.md#get-feature-by-id)端點取得功能。
4. 在回應JSON中，找出`audience`欄位。 這包含您所需的精確對象條件結構。
5. 複製`audience`值，從每個規則物件移除`id`屬性。 在您的「建立」或「更新」功能API呼叫中使用此專案。

## 範例 {#example}

呼叫GET `/m/api/v1/mgmt/feature/22080`後，回應包括：

```json
{
  "audience": [
    {
      "id": 10034665,
      "criteria": {
        "and": [
          {
            "operator": "EQ",
            "attr": "LOCALE",
            "val": "EN",
            "ruleId": 1,
            "category": "default"
          }
        ]
      }
    }
  ]
}
```

若要在「建立」功能呼叫中使用此專案，請從對象物件移除`id`欄位：

```json
{
  "audience": [
    {
      "criteria": {
        "and": [
          {
            "operator": "EQ",
            "attr": "LOCALE",
            "val": "EN",
            "ruleId": 1,
            "category": "default"
          }
        ]
      }
    }
  ]
}
```

## 另請參閱 {#see-also}

* [功能標幟管理API](feature-flags-management-api.md)
* [取得應用程式的使用者端ID](get-client-id.md)
* [管理修補程式API](management-patch-api.md)
