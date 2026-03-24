---
title: 設定逐步推出的功能群組
description: 瞭解如何在Adobe體驗轉出中為功能群組設定以百分比為基礎的逐步轉出。
source-git-commit: 9bfe0e55e89c1d7fbd77cde63831a6a186820e24
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 3%

---


# 設定逐步推出的功能群組 {#gradual-rollout-feature-group}

已在&#x200B;**基本詳細資料**&#x200B;索引標籤中設定功能群組的百分比轉出。 您可以隨時在轉出過程中將此值調整為向上或向下。

## 運作方式 {#how-it-works}

當您設定百分比轉出（例如60%）時，已定義對象的百分比會向功能群組顯示。 剩下的40%會放置在&#x200B;**控制組**&#x200B;中，此控制組會接收預設行為。

如果您已設定多個變體（針對A/B測試），曝光百分比會平均分配給各個變體。 例如，三種變體的60%曝光率會導致每個變體20%，而控制組為40%。

您可以隨時增加或減少百分比，以展開、減少或暫停轉出。

## 另請參閱 {#see-also}

* [建立功能群組](create-a-feature-group.md)
* [使用功能標幟的A/B測試](a-b-testing.md)
* [逐步轉出](../../concepts/gradual-rollout.md)
