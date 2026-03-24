---
title: 什麼是功能標幟
description: 瞭解什麼是功能旗標，以及可如何讓您在執行階段開啟或關閉應用程式功能，而不需要重新部署。
source-git-commit: 1c8fd9b42d08f657b4e6b16efae86faa04d15565
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# 什麼是功能標幟 {#what-is-a-feature-flag}

功能標幟是一種機制，可讓您在執行階段開啟或關閉應用程式的功能，而不需重新部署程式碼。

功能標幟會將&#x200B;**程式碼部署**&#x200B;與&#x200B;**功能可用性**&#x200B;分離。 您可以將功能隱藏在標幟後的新程式碼傳送至生產環境，然後在準備好時將其開啟 — 適用於所有使用者或目標子集。

此分隔可大幅降低風險。 開發人員能夠以最小的干擾持續建置和出貨，而產品團隊可完整控制功能何時和對誰可見。

>[!NOTE]
>
>在體驗轉出中，功能標幟是功能控制中最原子化的單位。 它可單獨使用以鎖定單一功能，或與[功能群組](feature-groups-to-control-multiple-features.md)或[版本](release-management.md)中的其他旗標結合。
