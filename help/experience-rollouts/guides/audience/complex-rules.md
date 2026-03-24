---
title: 複雜的受眾規則
description: 瞭解如何在Adobe體驗轉出中使用大型或複雜的受眾規則集，包括大量值限制以及如何跨多個條件分割規則。
source-git-commit: 3f3f7145b3c58dc721cbeb850e9e8571e3255bb1
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# 複雜的受眾規則 {#complex-rules}

## 大量值限制 {#bulk-value-limits}

將大量值新增至單一受眾規則時（例如電子郵件地址長清單），您可能會遇到錯誤，指出規則已超出允許的大小上限。

每個對象規則都有每個屬性的大小限制。 對於電子郵件地址，限製取決於專案的字元長度總計，而不是固定計數。 一般而言，請針對每個規則&#x200B;**使用約** 100-115個電子郵件地址。

如果您需要鎖定超過此限制允許的目標專案，請將清單分割為較小的區塊，並使用巢狀邏輯將這些區段套用為個別的OR連線條件。

## 對複雜規則使用巢狀邏輯 {#nested-logic}

巢狀邏輯可讓您結合多個對象條件與精確的AND/OR控制項。 若要啟用此功能：

1. 新增您需要的對象條件。
2. 在對象規則區段中啟用&#x200B;**巢狀邏輯**。
3. 每個條件都會指定一個數字。 輸入參照這些數字的邏輯運算式，例如：
   * `1 and (2 or 3)`
   * `(1 and 2) or 3`
   * `(1 and 2) or (3 and 4)`

這是百分比規則搭配其他條件所使用的相同機制。 如需已處理的範例，請參閱[在對象條件](adding-percentage-rules.md)中新增百分比規則。

## 另請參閱 {#see-also}

* [功能標幟和功能群組中的對象](audience-in-feature-flags-and-feature-groups.md)
* [在對象條件中新增百分比規則](adding-percentage-rules.md)
* [更新發行對象規則](../feature-flags/update-release-audience-rules.md)
