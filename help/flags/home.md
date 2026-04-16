---
title: 旗標
description: 瞭解如何使用Adobe Target中的旗標，透過受控制的轉出、功能旗標和目標受眾管理，安全且逐步地傳遞功能。
hide: true
index: false
exl-id: c400d75d-d928-4cf6-a094-1a2f443389f0
source-git-commit: 8a3a8f0293e32db896f62a63ea6a886868ffe1a3
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 1%

---

# 旗標 {#experience-rollouts-home}

>[!AVAILABILITY]
>
>標幟目前位於Beta中，可供Adobe Target客戶使用。 請聯絡您的Adobe代表以要求存取權。

Adobe Target中的旗標可讓產品團隊逐步、安全地傳送新功能，而不需要重新部署或停機。 您可以定義哪些人可以看到什麼、何時以及以什麼步調。 如果發生錯誤，您會立即關閉該功能。 如果一切順利，您就會按照排程擴大對象。

## 您可以做什麼

**控制誰能看到新功能。** Target發行至特定使用者、組織、區域或自訂屬性。 從小組開始，驗證體驗，然後展開 — 全部從主控台進行，沒有程式碼變更。

**執行A/B實驗。** 為對象的不同區段提供不同的變體，並測量表現較佳的變體。 在完整版發行之前，使用結果來做出明智的產品決策。

**降低發行風險。** 將大型變更分成較小且受控制的轉出。 如果出現錯誤或效能問題，請僅停用受影響的功能 — 應用程式的其餘部分會維持穩定。

**跨應用程式協調。** 功能群組可讓您一起管理多個功能標幟，跨應用程式共用相同的轉出對象。

**匯出您的資料。** 將Flags資料匯出至您偏好的報表環境，以便與其他Adobe資料一起進行分析和測量。

## 載入您的第一個旗標

從標幟取得值會從三個步驟開始：

1. **透過Adobe Target存取旗標** — Adobe Target中有旗標可以使用。 從Target介面中[要求存取權](guides/console/request-access.md)並開啟旗標。

1. **建立並發佈標幟** — 請依照[建立您的第一個功能標幟](guides/feature-flags/create-your-first-feature-flag.md)指南中的指示來定義標幟、設定您的初始對象並將其發佈到您的環境。

1. **與您的應用程式整合** — 使用AEP Web SDK或AEP Mobile SDK連線您的應用程式，以便在執行階段擷取並套用旗標。 從應用程式型別的[整合步驟](guides/integrate/integration-steps.md)開始。

一旦您的第一個旗標上線，您就可以調整其對象、設定逐步轉出，並將其從儲存提升為完全轉出。

## 需要協助嗎?

如果某些專案的行為與預期不符，請聯絡您的Adobe代表以尋求支援。

<!-- 
Bob was here. Again.
-->
