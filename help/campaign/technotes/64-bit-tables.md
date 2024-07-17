---
title: Adobe Campaign網頁使用者介面
description: 64位元表格
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
exl-id: ab5f01fd-4ad5-46e9-b132-011fe0f7bbd2
source-git-commit: 34c6f8a137a9085b26c0ea8f78930cff6192cfc9
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 6%

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
| nms：broadLogRcp | ID |
| nms：trackingLogRcp | ID |
| nms：excludeLogRcp | ID |
| nms：broadLogVisitor | ID |
| nms：trackingLogVisitor | ID |
| nms：propositionRcp | interactionId |
| nms：propositionVisitor | interactionId |
| nms：webTrackingLog | ID |
| nms：tmpBroadcast | message-id |
| nms：tmpMarketingPressure | message-id |
| nms：tmpBroadcastExclusion | message-id |
| nms：tmpBroadcastPaper | message-id |
| nms：broadLogAppSubRcp | ID |
| nms：trackingLogAppSubRcp | ID |
| nms：excludeLogAppSubRcp | ID |
| nms：webEvent | broadLogSrc-id， broadLogRemkt-id |
| nms：broadLogMid | mktBroadLogId |
| nms：mirrorPageSearch | remoteMessageId |
