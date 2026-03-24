---
title: 環境概觀
description: 瞭解Adobe Experience轉出中的階段和生產環境，以及何時使用環境。
source-git-commit: 9bfe0e55e89c1d7fbd77cde63831a6a186820e24
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 4%

---


# 環境概觀 {#environments}

體驗轉出提供不同的環境，讓您在將變更提升至已上線使用者之前，可以驗證您的功能標幟。

## 可用環境 {#available-environments}

| 環境 | 目的 |
|---|---|
| **階段** | 測試和驗證。 在生產環境中啟用功能標幟之前，請使用此環境來設定和測試功能標幟。 |
| **生產** | 即時轉出。 這裡設定的功能標幟會根據您的實際使用者群進行評估。 |

>[!IMPORTANT]
>
>在階段中所做的變更不會自動結轉至生產環境。 功能標幟和受眾規則必須在每個環境中個別設定。

## 選取環境 {#selecting}

登入「體驗轉出」主控台後，從介面頂端的環境切換器選取環境。 在建立或修改功能標幟之前，請確定您是在正確的環境中工作。

## 最佳做法 {#best-practices}

請遵循下列建議，以避免設定錯誤並保護您的生產對象：

* 一律先在&#x200B;**階段**&#x200B;中建立和測試功能標幟。
* 在生產環境中複製之前，請先驗證階段中的對象規則、轉出百分比和目標定位邏輯。
* 使用[跨環境工作流程](../cross-environment/cross-environment-concept.md)檢視和管理跨環境的旗標狀態。

## 另請參閱 {#see-also}

* [登入主控台](log-in-to-the-console.md)
* [將環境與應用程式建立關聯](../cross-environment/associate-environments.md)
* [檢視不同環境的功能標幟](../cross-environment/view-feature-flags-across-environments.md)
