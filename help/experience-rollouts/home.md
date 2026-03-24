---
title: Adobe體驗轉出
description: 瞭解如何使用Adobe體驗轉出，透過受控制的轉出、功能標幟和目標受眾管理，安全且逐步地提供功能。
exl-id: c400d75d-d928-4cf6-a094-1a2f443389f0
source-git-commit: 65effd7e3b12404359e3693820bbf9e5080bea03
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 1%

---

# Adobe體驗轉出 {#experience-rollouts-home}

Adobe體驗推出可讓產品團隊逐步、安全地推出新功能，無需重新部署或停機。 您可以定義哪些人可以看到什麼、何時以及以什麼步調。 如果發生錯誤，您會立即關閉該功能。 如果一切順利，您就會按照排程擴大對象。

## 您可以做什麼

**控制誰能看到新功能。** Target發行至特定使用者、組織、區域或自訂屬性。 從小組開始，驗證體驗，然後展開 — 全部從主控台進行，沒有程式碼變更。

**執行A/B實驗。** 為對象的不同區段提供不同的變體，並測量表現較佳的變體。 在完整版發行之前，使用結果來做出明智的產品決策。

**降低發行風險。** 將大型變更分成較小且受控制的轉出。 如果出現錯誤或效能問題，請僅停用受影響的功能 — 應用程式的其餘部分會維持穩定。

**跨團隊的座標。** 跨團隊功能群組可讓多個團隊參與單一協調發行，每個團隊在共用通用轉出排程和受眾時，管理各自的功能標幟。

## 載入您的第一個功能

從Experience轉出取得價值始於三個步驟：

1. **設定您的團隊和應用程式** — [要求主控台的存取權](guides/console/request-access.md)，然後[將應用程式上線](guides/applications/onboard-your-application.md)，讓Experience Rollout知道要提供哪些使用者端。

2. **建立並發佈功能標幟** — 請依照[建立您的第一個功能標幟](guides/feature-flags/create-your-first-feature-flag.md)指南中的指示定義標幟、設定您的初始對象並將其發佈到您的環境。

3. **與您的應用程式整合** — 將您的應用程式連線至Experience Rollouts API或SDK，以便在執行階段擷取並套用功能標幟。 從應用程式型別的[整合步驟](guides/integrate/integration-steps.md)開始。

一旦您的第一個旗標上線，您就可以調整其對象、設定逐步轉出，並透過[發行狀態](guides/feature-flags/release-states.md)將它從儲存到完整轉出。

## 需要協助嗎?

如果某些專案的行為與預期不符，[疑難排解指南](guides/support/troubleshooting.md)會涵蓋最常見的問題。 如需其他資訊，[請連絡支援人員](guides/support/contact-support.md)。
