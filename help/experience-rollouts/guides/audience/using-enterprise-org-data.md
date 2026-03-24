---
title: 在對象規則中使用企業組織資料
description: 瞭解如何在Adobe體驗轉出中使用企業組織ID作為對象條件，以鎖定特定客戶組織。
source-git-commit: 3f3f7145b3c58dc721cbeb850e9e8571e3255bb1
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---


# 在對象規則中使用企業組織資料 {#enterprise-org-data}

體驗轉出支援根據企業組織（組織） ID鎖定使用者。 這可讓您在廣泛提供功能之前，先將功能推出給特定客戶組織。

## 在對象規則中新增組織 {#adding-org-rule}

企業組織鎖定目標可在&#x200B;**對象規則>設定檔>企業**&#x200B;底下的&#x200B;**對象**&#x200B;標籤中使用。

支援兩種組織型別：

### DME組織 {#dme-orgs}

DME組織由其組織ID識別。 建立規則時，僅輸入組織ID — 不包含驗證來源。

### DMA組織 {#dma-orgs}

DMA組織使用`XXXXXXXXXXXXXXXXXXXXXXXX@ADOBEORG`格式的組織ID。 輸入DMA組織ID時：

* 使用包含`@ADOBEORG`尾碼的完整組織ID。
* 輸入大寫的`ADOBEORG`。

**範例：** `57F22B5D5A5F83AE0A495E6E@ADOBEORG`

## 重要備註 {#important-notes}

* 系統會針對與使用者的已驗證工作階段相關聯的組織，評估以組織為基礎的目標定位。 測試時，確保使用者已登入正確的組織。
* 如果您期望找到的組織未出現在對象條件中，或功能未如預期傳回特定組織，請聯絡體驗轉出支援。
* 中繼和生產環境可能會因可用的組織而異。 在提升至生產環境之前，請先在階段中測試對象規則。

## 另請參閱 {#see-also}

* [功能標幟和功能群組中的對象](audience-in-feature-flags-and-feature-groups.md)
* [更新發行對象規則](../feature-flags/update-release-audience-rules.md)
* [複雜的受眾規則](complex-rules.md)
