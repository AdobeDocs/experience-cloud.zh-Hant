---
title: 體驗轉出中的發行管理
description: 瞭解Experience轉出的版本管理如何透過黑暗部署、生產測試和逐步轉出，協調多團隊功能交付。
source-git-commit: 1c8fd9b42d08f657b4e6b16efae86faa04d15565
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---


# 體驗轉出中的發行管理 {#release-management}

典型的主要發行涉及多個團隊和多個應用程式，每個應用程式都有各自的部署時間表和相依性。 體驗轉出提供發行管理模型，讓團隊可獨立工作，同時仍為使用者提供協調、可控的發行。

## 主要功能 {#capabilities}

### 深色部署 {#dark-deployments}

團隊不再需要以特定上線日期來安排程式碼部署時間。 程式碼可隨時部署到功能標幟之後的生產環境。 一般使用者在版本啟動後才會看到任何變更。 團隊可以按照自己的進度部署，確信不會過早暴露任何內容。

### 在生產環境中測試 {#testing-in-production}

一旦計畫碼部署到生產環境（深色部署），體驗轉出即可對內部測試人員和QA團隊開啟功能。 如此一來，您就可以針對生產環境和真實生產資料進行完整測試，不會面臨任何讓使用者看到變更的風險。

### 逐步轉出 {#gradual-rollout}

當版本準備上線時，它不必是all或nothing。 體驗轉出可讓您以漸進方式控制轉出 — 從一小部分使用者開始、監控回饋和效能，並隨著時間擴展對象。 這樣可減輕後端系統的負擔，讓團隊在完整曝光之前有時間回應任何問題。

### 協調啟用 {#coordinated-activation}

多個團隊分別開發功能，每個團隊都有各自的功能標幟。 所有團隊都準備就緒後，體驗轉出會提供單一控制點，以便同時（或逐步）啟動團隊和應用程式中的所有旗標，讓版本以一個整合體驗的形式上線。

## 另請參閱 {#see-also}

* [發行管理概念](concept-of-release-management.md)
* [控制多個特徵的特徵群組](feature-groups-to-control-multiple-features.md)
* [逐步轉出](gradual-rollout.md)
