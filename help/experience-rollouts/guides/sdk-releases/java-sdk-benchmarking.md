---
title: SDK基準
description: 檢閱Adobe體驗轉出的Java SDK基準測試結果，包括在一般負載條件下，對多種功能標幟進行的回應時間測量。
source-git-commit: 8b8b5db1a28af3a3ac29aecf26482f70eb84c714
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 7%

---


# SDK基準 {#sdk-benchmarking}

Experience Rollouts Java SDK已設定基準，可讓整合團隊可靠地估計在SDK在其基礎架構內執行時可預期的資源和回應時間。

## 測試環境 {#test-environment}

使用下列固定組態在Spring Boot應用程式上執行基準測試：

* **CPU核心：** 8
* **JVM記憶體：** 4096 MB

## 測試假設 {#test-assumptions}

下列條件在所有基準執行中保持不變：

* 已測試功能標幟：8到128
* 每個功能標幟的內容變數： 2 （型別`STRING`，長度36個字元）
* 平均負載：每分鐘15,000個要求(RPM)
* 作用中執行緒： 100

## 結果 {#results}

下表顯示`getFeatures()`個呼叫的第99.99個百分位回應時間，因為功能旗標數目增加：

| 功能標幟的數量 | 每個標幟的內容變數 | 回應時間(ms， p99.99) |
|---|---|---|
| 8 | 2 | &lt; 0.5 |
| 16 | 2 | &lt; 0.5 |
| 32 | 2 | &lt; 0.5 |
| 64 | 2 | &lt; 1 |
| 128 | 2 | &lt; 1 |

## 解譯結果 {#interpretation}

上述效能標竿代表上述特定測試條件下的效能。 由於SDK會在應用程式的基礎架構中執行，實際回應時間會因您環境的特定因素而異：

* 可用的CPU與核心數量
* JVM棧積大小和記憶體回收行為
* 執行緒可用性與內容切換
* 要求時的目前系統載入

使用這些數字作為計畫基準，而不是作為生產環境的保證效能目標。

## 另請參閱 {#see-also}

* [Java SDK整合指南](java/java-sdk-integration-guide.md)
* [Java SDK發行說明](java/java-sdk-release-notes.md)
* [SDK](../integrate/sdks.md)
