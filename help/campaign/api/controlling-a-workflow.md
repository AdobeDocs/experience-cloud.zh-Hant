---
title: 控管工作流程
description: 瞭解如何使用API控制工作流程。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
exl-id: 79eacc31-d5a2-4e13-aa0b-744d7ab7004f
source-git-commit: 3f4400f24b75e8e435610afbe49e9d9444dbf563
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 9%

---

# 控管工作流程 {#controlling-a-workflow}

您可以透過包含工作流程ID和所需執行命令的POST請求，直接從REST API控制工作流程：

`POST https://mc.adobe.io/<ORGANIZATION>/campaign/workflow/execution/<workflowID>/commands`

>[!CAUTION]
>
>如果工作流程ID在Adobe Campaign中變更，API請求將無法再運作。

有四個執行命令可用於控制工作流程：

* 開始
* 暫停
* 繼續
* 停止

如需執行命令的詳細資訊，請參閱 [Campaign檔案](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/executing-a-workflow/about-workflow-execution.html).

<br/>

***範例要求***

* 啟動工作流程。

  ```
  -X POST https://mc.adobe.io/<ORGANIZATION>/campaign/workflow/execution/<workflowID>/commands \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  -H 'Cache-Control: no-cache' \
  -H 'X-Api-Key: <API_KEY>' \
  -i
  -d '{"method":"start"}'
  ```

  <!-- + réponse -->

* 停止工作流程。

  ```
  -X POST https://mc.adobe.io/<ORGANIZATION>/campaign/workflow/execution/<workflowID>/commands \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  -H 'Cache-Control: no-cache' \
  -H 'X-Api-Key: <API_KEY>' \
  -i
  -d '{"method":"stop"}'
  ```

  <!-- + réponse -->
