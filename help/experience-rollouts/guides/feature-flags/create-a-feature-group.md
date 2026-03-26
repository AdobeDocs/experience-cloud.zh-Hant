---
title: 建立功能群組
description: 瞭解如何在Adobe Experience轉出中建立功能群組，以單一單位管理團隊中跨應用程式的多個功能標幟。
exl-id: 58148df1-84ee-4a78-a4b4-71f74cd8ce0a
source-git-commit: 454b5c719a5f8be82d1ed835da58bfca6316def2
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# 建立功能群組 {#create-feature-group}

## 先決條件 {#prerequisites}

在建立特徵群組之前，請完成下列操作：

* 您可以存取Experience Rollout主控台 — 請參閱[登入主控台](../console/log-in-to-the-console.md)
* 您的應用程式已上線 — 請參閱[將應用程式上線](../applications/onboard-your-application.md)
* 您有&#x200B;**開發人員**&#x200B;或&#x200B;**產品發行擁有者**&#x200B;角色
* 您已建立要新增至群組的功能標幟 — 請參閱[建立您的第一個功能標幟](create-your-first-feature-flag.md)

如需功能群組的簡介，請參閱[控制多個功能的功能群組](../../concepts/feature-groups-to-control-multiple-features.md)。

## 步驟1：建立特徵群組 {#create}

開啟主控台並啟動新功能群組：

1. 登入「體驗轉出」主控台，並導覽至「**功能測試>功能群組**」。
2. 選取&#x200B;**新功能群組**。

## 步驟2：基本詳細資訊 {#basic-details}

設定功能群組的一般設定：

1. 提供標題、索引鍵、說明，以及選用的標籤。
2. 設定功能群組的&#x200B;**百分比轉出**。
3. 如果要執行A/B測試，請選取多個變體。 否則，請將其保留在一個變體中。 如需詳細資訊，請參閱具有功能旗標](a-b-testing.md)的[A/B測試。

## 步驟3：對象 {#audience}

定義將接收此群組中功能的人員：

1. 在&#x200B;**對象**&#x200B;索引標籤上，新增對象條件以定義哪些使用者會收到該功能。
2. 在&#x200B;**應用程式**&#x200B;下，從您的團隊新增一或多個應用程式。 功能群組可以跨越多個應用程式，只要這些應用程式都屬於同一個團隊即可。

>[!NOTE]
>
>**開發人員**&#x200B;角色是沙箱式。 在&#x200B;**受眾>設定檔>使用者ID**&#x200B;下新增您自己的使用者ID，以進行私人測試。 若要鎖定外部使用者，您需要&#x200B;**產品發行擁有者**&#x200B;角色。

## 步驟4：功能 {#features}

指派將由此群組控制的功能標幟：

1. 在「**功能**」標籤下，您會看到每個所選應用程式的方塊。
2. 為每個應用程式新增功能標幟。
3. 如果您選取了多個變體（用於A/B測試），則會看到每個變體的標籤。 為每個專案新增適當的功能標幟。

>[!IMPORTANT]
>
>功能標幟只能透過一種方法提供 — 直接作為功能標幟、透過功能群組或透過發行。 當您將功能標幟新增至功能群組時，在該標幟上設定的任何對象或轉出百分比都會被移除。 已指派給其他版本或功能群組的功能標幟將不會出現在清單中。

## 步驟5：排程（選擇性） {#schedule}

您可以排程功能群組在未來日期和時間啟動。 如需詳細資訊，請參閱[排程](schedule.md)。

## 另請參閱 {#see-also}

* [設定逐步推出的功能群組](set-feature-group-gradual-rollout.md)
* [使用功能標幟的A/B測試](a-b-testing.md)
* [控制多個特徵的特徵群組](../../concepts/feature-groups-to-control-multiple-features.md)
