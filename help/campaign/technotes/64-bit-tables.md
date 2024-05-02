---
title: Adobe Campaign網頁使用者介面
description: 64位元表格
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
source-git-commit: 47b06a42fad73254025d8e21d14724f6fe93345b
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 1%

---


# 64位元結構描述 {#64-bit-tables}

為了方便從Campaign Standard轉換到Campaign v8，有幾個表格已從32位元變更為64位元。 事實上，Campaign Standard在數個現成可用的綱要中支援64位元PK，而在大多數綱要中，Campaign v8支援32位元PK。

## 限制

* 這項技術變更僅適用於從Campaign Standard移轉的客戶。
* 結構描述和broadlog擴充功能不支援64位元。 它將保持在32位元。
* 與傳送給技術使用者的傳遞相關的記錄將無法在Campaign v8中使用。
* 僅支援PostgreSQL。

## 修改的結構描述

以下是變更為64位元及其修改屬性的結構描述清單。

| 方案名稱 | 屬性名稱 |
|--- |--- |
| nms：broadLogRcp | id |
| nms：trackingLogRcp | id |
| nms：excludeLogRcp | id |
| nms：broadLogVisitor | id |
| nms：trackingLogVisitor | id |
| nms：propositionRcp | interactionId |
| nms：propositionVisitor | interactionId |
| nms：webTrackingLog | id |
| nms：tmpBroadcast | message-id |
| nms：tmpMarketingPressure | message-id |
| nms：tmpBroadcastExclusion | message-id |
| nms：tmpBroadcastPaper | message-id |
| nms：broadLogAppSubRcp | id |
| nms：trackingLogAppSubRcp | id |
| nms：excludeLogAppSubRcp | id |
| nms：webEvent | broadLogSrc-id， broadLogRemkt-id |
| nms：broadLogMid | mktBroadLogId |
| nms：mirrorPageSearch | remoteMessageId |


