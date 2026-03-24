---
title: 具有使用者端IP內容變數的對象規則
description: 瞭解如何在Adobe體驗轉出的對象規則中使用使用者端IP內容變數，包括支援IP位址、CIDR區塊和網路範圍。
source-git-commit: 3f3f7145b3c58dc721cbeb850e9e8571e3255bb1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---


# 具有使用者端IP內容變數的對象規則 {#clientip-rule}

`clientip`內容變數可讓您根據使用者的使用者端IP位址來鎖定使用者。 這對於根據使用者存取您的應用程式的網路來限制或啟用功能非常有用，例如，限制公司網路上的使用者提早存取。

## 支援的輸入型別 {#input-types}

`clientip`內容變數支援三種型別的輸入值：

| 輸入型別 | 說明 | 支援的運運算元 |
|---|---|---|
| **IP位址** | 單一IPv4或IPv6位址 | 是、不等於、在 |
| **CIDR區塊** | CIDR標籤法的IP位址範圍（例如，`192.168.1.0/24`） | 在中，不等於 |
| **網路範圍** | 由平台維護的預定義具名網路範圍 | 屬於 |

## 新增使用者端IP規則 {#adding-rule}

1. 在主控台中開啟功能標幟、功能群組或跨團隊功能群組。
2. 前往&#x200B;**對象**&#x200B;標籤。
3. 在&#x200B;**內容**&#x200B;下，使用&#x200B;**clientip**&#x200B;變數新增條件。
4. 選取運運算元並輸入值（IP位址、CIDR區塊或選取預先定義的網路範圍）。

## 另請參閱 {#see-also}

* [在對象規則中使用內容](using-context-in-audience-rules.md)
* [功能標幟和功能群組中的對象](audience-in-feature-flags-and-feature-groups.md)
* [複雜的受眾規則](complex-rules.md)
