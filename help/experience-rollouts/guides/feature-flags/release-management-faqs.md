---
title: 發行管理常見問題集
description: 在Adobe體驗轉出中尋找有關版本管理的常見問題解答。
source-git-commit: d311efb995b20ffc17370d68d57dd84a8605896c
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 1%

---


# 發行管理常見問題集 {#release-management-faqs}

## 如何請求版本？ {#request-release}

請參閱[要求版本](request-a-release.md)，以取得完整程式以及您需要提供的資訊。

## 發行支援哪些對象條件？ {#audience-criteria}

版本支援下列對象規則：

* ID型別（帳戶型別）
* 國家/地區
* 使用者ID (GUID)
* 電子郵件地址（個別或大量清單）
* 電子郵件網域
* 使用者端IP
* 百分比（所有使用者）
* 百分比（僅限已驗證的使用者）

您可以使用AND/OR邏輯（包括巢狀條件）來合併多個規則。 如需逐步設定指示，請參閱[更新發行對象規則](update-release-audience-rules.md)。

## 如何將應用程式新增至發行版本？ {#onboard-application}

建立發行版本後，在主控台中開啟它，並將您的應用程式新增到發行版本設定。 接著，每個應用程式的產品發行擁有者可以新增相關功能標幟。 如需完整順序，請參閱[端對端發行工作流程](release-workflow-end-to-end.md)。

## 應符合資格的使用者不會傳回功能。 如何進行疑難排解？ {#troubleshoot}

請依照下列步驟進行除錯：

1. **檢查發行狀態。** 發行版本必須處於&#x200B;**已發佈**&#x200B;或&#x200B;**完整轉出**&#x200B;狀態才能提供功能。 請參閱[發行狀態](release-states.md)。
2. **檢查應用程式和功能標幟。** 確認已針對正確的應用程式建立功能標幟，且應用程式與正確版本相關聯。
3. **檢查功能標幟是否已啟用。** 即使發行版本作用中，也不會提供停用的標幟。
4. **檢閱對象條件。** 確認使用者符合對象規則中定義的所有條件。 仔細檢查與功能相關聯之特定版本的條件。

## 另請參閱 {#see-also}

* [要求發行](request-a-release.md)
* [更新發行對象規則](update-release-audience-rules.md)
* [發行狀態](release-states.md)
* [端對端發行工作流程](release-workflow-end-to-end.md)
