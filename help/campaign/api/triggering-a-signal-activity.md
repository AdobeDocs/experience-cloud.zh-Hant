---
title: 觸發訊號活動
description: 瞭解如何使用API觸發訊號活動。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
exl-id: 9f94e98f-fe04-4369-8946-1380e02cdece
source-git-commit: 3f4400f24b75e8e435610afbe49e9d9444dbf563
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 2%

---

# 觸發訊號活動 {#triggering-a-signal-activity}

在Adobe Campaign Standard工作流程中，可以有一或多個 **外部訊號** 活動。 這些活動是等待觸發的「監聽器」。

Campaign StandardAPI可讓您觸發 **外部訊號** 活動以呼叫工作流程。 API呼叫可包含將擷取至工作流程事件變數的引數（要定位的對象名稱、要匯入的檔案名稱、部分訊息內容等）。 如此一來，您便可輕鬆將Campaign自動化與外部系統整合。

>[!NOTE]
>
>外部訊號活動的觸發頻率不得超過每10分鐘一次，且目標工作流程必須已在執行中。

若要觸發工作流程，請遵循下列步驟：

1. 執行 **GET** 請求工作流程以擷取外部訊號活動觸發URL。

   `GET https://mc.adobe.io/<ORGANIZATION>/campaign/workflow/execution/<workflowID>`

1. 執行 **POST** 對傳回URL的要求以觸發訊號活動，使用 **&quot;source&quot;** 引數。 此屬性為必要屬性，可讓您指定觸發要求來源。

如果您想要使用引數呼叫工作流程，請將其新增至具有的裝載 **&quot;parameters&quot;** 屬性。 語法由引數名稱及其值組成(支援下列型別： **字串**， **數字**， **布林值** 和 **日期/時間**)。

```
  -X POST <TRIGGER_URL>
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  -H 'Cache-Control: no-cache' \
  -H 'X-Api-Key: <API_KEY>' \
  -H 'Content-Type: application/json;charset=utf-8' \
  -H 'Content-Length:79' \
  -i
  -d {
  -d    "source":"<SOURCE>",
  -d    "parameters":{
  -d      "<PARAMETER_NAME":"<PARAMETER_VALUE>",
  -d      "<PARAMETER_NAME":"<PARAMETER_VALUE>",
  -d      "<PARAMETER_NAME":"<PARAMETER_VALUE>",  
  -d      "<PARAMETER_NAME":"<PARAMETER_VALUE>"
  -d    }
  -d }
```

>[!NOTE]
>
>將引數新增至裝載時，請確定其 **名稱** 和 **type** 值與外部訊號活動中宣告的資訊一致。 此外，承載大小不應超過64Ko。

<br/>

***範例要求***

在工作流程上執行GET要求。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/workflow/execution/<workflowID> \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

它會傳回工作流程訊號活動和相關的觸發程式URL。

```
{
"PKey": "<PKEY>",
"activities": {
  "activity": {
    "signal1": {
      ...
      "trigger": {
        "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/workflow/execution/<PKEY>/activities/activity/<PKEY>/trigger/"
        },
        ...
      }
    }
  }
}
```

若要觸發訊號活動，請使用「source」在觸發程式url上執行POST要求。 如果要使用引數呼叫工作流程，請新增「引數」屬性。

```
-X POST https://mc.adobe.io/<ORGANIZATION>/campaign/workflow/execution/<PKEY>/activities/activity/<PKEY>/trigger \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>' \
-i
-d '{
-d "source":"API",
-d "parameters":{
-d    "audience":"audience",
-d    "email":"anna.varney@mail.com",
-d    "template":"05",
-d    "contentURL":"http://www.adobe.com",
-d    "test":"true",
-d    "segmentCode":"my segment",
-d    "attribute":"2019-04-03 08:17:19.100Z"}
-d  }'
```

<!-- + réponse -->

如果未在外部訊號活動中宣告其中一個引數，POST要求會傳回以下錯誤，指出遺漏了哪個引數。

```
RST-360011 An error has occurred - please contact your administrator.
'contentURL' parameter isn't defined in signal activity.
XTK-170006 Unable to parse expression 'HandleTrigger(@name, $(source), $({parameters}))'.
RST-360000 Error while assessing 'HandleTrigger(@name, $(source), $({parameters}))' expression ('xtk:workflow:execution/activities/signal/trigger' resource)
```
