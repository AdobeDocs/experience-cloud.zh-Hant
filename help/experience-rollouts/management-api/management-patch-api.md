---
title: 管理修補程式API
description: 使用體驗轉出PATCH API來更新功能標幟、功能群組或跨團隊功能群組的個別欄位，而不傳遞完整物件。
source-git-commit: 6ecedbfc6c7de392f214f3f8f2e71aa18e1bacb9
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 3%

---


# 管理修補程式API {#management-patch-api}

PATCH API可讓您更新功能標幟、功能群組或跨團隊功能群組的特定欄位，而不需在請求內文中傳送完整物件。 這對於目標更新（例如變更對象規則、切換狀態或調整變化百分比）非常有用。

## 功能標幟PATCH {#feature-flag-patch}

更新功能標幟的一或多個欄位。

| | |
|---|---|
| **端點** | `PATCH /m/api/v1/mgmt/feature/{featureFlagId}` |
| **方法** | PATCH |

### 請求標頭 {#ff-request-headers}

所有要求都需要[一般需求](feature-management-apis-overview.md#common-requirements)中說明的標頭。

### Path引數 {#ff-path-param}

| 參數 | 類型 | 說明 | 必要 |
|---|---|---|---|
| `featureFlagId` | 整數 | 要更新的功能標幟的數值ID。 | 是 |

### 要求內文 {#ff-request-body}

僅傳遞您要更新的欄位。 回應一律會傳回完整的更新功能標幟物件。

**範例 — 僅更新說明：**

```json
{
  "description": "Updated description"
}
```

**範例 — 移除現有的對象：**

```json
{
  "audience": null
}
```

**範例 — 在沒有對象存在時新增對象：**

```json
{
  "audience": [
    {
      "criteria": {
        "and": [
          { "operator": "EQ", "attr": "sandboxType", "val": "DEVELOPMENT", "ruleId": 1, "category": "contextual" }
        ]
      }
    }
  ]
}
```

**範例 — 更新現有的對象規則：**

```json
{
  "audience": [
    {
      "id": 10020035,
      "criteria": {
        "and": [
          { "operator": "EQ", "attr": "sandboxType", "val": "PRODUCTION", "ruleId": 1, "category": "contextual" }
        ]
      }
    }
  ]
}
```

**範例 — 變更狀態和變數百分比：**

```json
{
  "state": "disabled",
  "variations": [
    {
      "id": 10017188,
      "variantName": "Variation 1",
      "variantPercentage": 80.0
    }
  ]
}
```

>[!NOTE]
>
>更新現有的對象規則時，請包含規則的`id` （可從GET功能回應中取得）以就地更新。 更新變數時，請包含變數的`id`以避免建立重複。

### 回應 {#ff-response}

| 狀態 | 說明 |
|---|---|
| `200` | 成功。 回應內文是完整的更新功能標幟物件。 |
| `400` | 無效的承載。 |
| `403` | 許可權不足。 |
| `417` | 並行更新衝突。 擷取目前功能並重試。 |

## 功能群組PATCH {#feature-group-patch}

更新功能群組的一或多個欄位。 要求和回應結構與功能標幟PATCH相同，只有端點不同。

| | |
|---|---|
| **端點** | `PATCH /m/api/v1/mgmt/group/{featureGroupId}` |
| **方法** | PATCH |

## 跨團隊功能群組PATCH {#ctfg-patch}

更新跨團隊功能群組的一或多個欄位。 使用v2發行端點。

| | |
|---|---|
| **端點** | `PATCH /m/api/v2/mgmt/release/{CTFGId}` |
| **方法** | PATCH |

## 另請參閱 {#see-also}

* [功能標幟管理API](feature-flags-management-api.md)
* [功能群組管理API](feature-group-management-api.md)
* [發行管理API](release-management-apis.md)
* [功能管理API概述](feature-management-apis-overview.md)
