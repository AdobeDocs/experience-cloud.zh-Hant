---
title: 端對端發行工作流程
description: 瞭解在Adobe Experience轉出中管理協調發行的端對端工作流程，從定義功能標幟到上線。
source-git-commit: d311efb995b20ffc17370d68d57dd84a8605896c
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---


# 端對端發行工作流程 {#release-workflow}

本頁說明由「版本管理員」管理的協調發行所涉及的全序列活動。

## &#x200B;1. 為每個應用程式定義功能旗標 {#define-flags}

每個產品團隊都會指派一名&#x200B;**產品發行版本擁有者**，此人會登入Experience Rollouts主控台，並為他們擁有的應用程式建立功能標幟。 然後，產品團隊會在其程式碼中實作條件式邏輯，將功能置於這些標幟後面。

## &#x200B;2. 建立版本 {#create-release}

建立新版本需要支援要求，但並非完全自助服務。 請聯絡Experience Rollouts支援以建立版本。 提供發行版本名稱、所屬團隊、目標環境、目標、參與應用程式及預期持續時間。

在確認發行後， Release Manager會開啟主控台並完成發行設定。

## &#x200B;3. 將功能標幟新增至發行 {#add-flags}

對於新增至版本的每個應用程式，該應用程式的產品版本所有者會登入並將相關功能標幟新增至版本。 這些旗標代表將隨發行上線的功能。

## &#x200B;4. 設定對象 {#configure-audience}

Release Manager會選取發行的對象，例如，特定國家/地區的1%使用者、具有特定電子郵件網域的所有使用者，或特定使用者ID的清單。 設定之後，Release Manager會儲存並發佈版本，將版本推送到指定的對象。

## &#x200B;5. 展開並管理轉出 {#expand}

在發行上線後，發行管理員可以調整對象規則以逐步擴大推出、監視問題，並使用發行狀態控制來管理生命週期。 如需詳細資訊，請參閱[發行狀態](release-states.md)。

## 要點 {#key-points}

* 所有參與的應用程式都會在功能旗標後面獨立地將程式碼部署到生產環境 — 不需要協調部署時間。
* 此版本是單一控制點，可同時啟用跨團隊的所有標幟。
* 發行版本的對象鎖定目標是根據驗證權杖屬性（國家/地區、電子郵件、使用者ID、百分比）。

## 另請參閱 {#see-also}

* [要求發行](request-a-release.md)
* [更新發行對象規則](update-release-audience-rules.md)
* [發行狀態](release-states.md)
