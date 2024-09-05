---
title: Recommendations與限制
description: Recommendations以及移轉至Campaign v8 REST API時的限制。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
mini-toc-levels: 1
badge: label="可用性限制" type="Informative" url="../campaign-standard-migration-home.md" tooltip="僅限Campaign Standard已移轉的使用者"
exl-id: 45acebb1-9325-4e26-8fe9-cc73f745d801
source-git-commit: 6e4e214731b9772014d01dde89b3f80e4c4e93a6
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 1%

---

# Recommendations與限制 {#limitations}

## 許可權與安全性 {#permissions}

### 產品設定檔對應

在Campaign Standard中，無論您獲指派的產品設定檔為何，皆已授予您較高許可權的API管理員角色存取權。 Campaign v8引入一組不同的產品設定檔，需要從Campaign Standard對應到Campaign v8產品設定檔。

移轉後，會將兩個產品設定檔新增至您現有或預先建立的技術帳戶：管理員和訊息中心（用於存取交易API）。 如果您不希望管理員產品設定檔對應至您的技術帳戶，請檢閱產品設定檔對應，並指派所需的產品設定檔。

### 租使用者ID

移轉後，對於未來的任何整合，建議在REST URL中使用您的&#x200B;**Campaign v8租使用者ID**，取代您之前的Campaign Standard租使用者ID。

### 金鑰使用方法

Campaign Standard和Campaign v8的PKey值管理方式不同。 如果您使用Campaign Standard儲存PKeys，請確定您的實作會使用從先前API呼叫取得的PKeys或href，以動態方式形成後續API呼叫。

## 可用的API {#deprecated}

目前，下列REST API可供使用：

* **設定檔**
* **服務與訂閱**
* **自訂資源**
* **工作流程**

>[!AVAILABILITY]
>
>目前無法使用&#x200B;**交易式訊息** REST API。
>
>下列REST API已過時，無法使用：
>* 行銷歷史記錄
>* 組織單位
>* 隱私權管理

## 篩選

* 若要在REST API裝載中使用篩選器，您需要在Campaign v8中編輯篩選器，並提供要在裝載中使用的名稱。 若要這麼做，請從&#x200B;**[!UICONTROL 引數]**&#x200B;索引標籤存取篩選器的其他引數，並在REST API ]**欄位的**[!UICONTROL &#x200B;篩選名稱中提供所需的名稱。

  ![](assets/api-filtering.png)


* 使用自訂篩選器所需的「by」首碼已不再需要。 篩選器名稱的使用方式應與請求相同。

  範例：

  `GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServicesExt/<resourceName>/<customFilterName>?<customFilterparam>=<customFilterValue>`

## 捨棄的資料庫欄位

移轉期間會捨棄資料庫中的部分欄位。 使用下拉欄位時，REST API會傳回空白值。 所有捨棄的欄位都將被取代和移除。

## 使用連結的資源POST

使用以下要求內文格式時，「vehicleOwner」代表「nms：recipient」的連結：

```
{
    "vehicleNumber": "20009",
    "vehicleName": "Model E",
    "vehicleOwner":{
        "firstName":"tester 11",
        "lastName":"Smith 11"
    }
}
```

連結資訊會被忽略。 因此，「cusVehicle」下會產生只包含「vehicleNumber」和「vehicleName」值的新記錄。 不過，連結仍保持空值，導致「vehicleOwner」設定為null。

在Campaign v8中，當使用相同的要求內文結構且「vehicle」連結至設定檔時，會發生錯誤。 發生此錯誤是因為「firstName」屬性無法辨識為「cusVehicle」有效。 不過，請求內文僅包含屬性，卻不包含連結函式，且沒有任何問題。

## PATCH作業

* Campaign v8不支援具有空白請求本文的PATCH：它會傳回204無內容狀態。
* 雖然Campaign Standard支援對結構描述中的元素/屬性進行PATCH，但請注意，Campaign v8不支援對位置進行PATCH操作。 嘗試在位置PATCH將導致500內部伺服器錯誤，並出現錯誤訊息，指出「zipCode」屬性對「profile」資源無效。

## REST回應

下節列出Campaign Standard和v8 REST回應之間的細微差異。

* 對於單一GET記錄，回應會將href納入回應中。
* 使用屬性查詢時，Campaign v8會在回應中提供計數和分頁。
* POST作業後，回應中會傳回連結資源的值。

## 錯誤碼和訊息

下節列出Campaign Standard與Campaign v8錯誤代碼和訊息之間的差異。

| 情境 | Campaign Standard | Campaign v8 |
|  ---  |  ---  |  ---  |
| 在請求內文中使用無效的PKey | 500 - &#39;O5iRp40EGA&#39;屬性不明(請參閱&#39;Profiles (nms：recipient)&#39;綱要的定義)。 XTK-170036無法剖析運算式&#39;@id = @O5iRp40EGA&#39;。 | 404 — 無法解密PKey。 (PKey=@jksad) |
| 在URI中使用無效的API | 500 - &#39;O5iRp40EGA&#39;屬性不明(請參閱&#39;Profiles (nms：recipient)&#39;綱要的定義)。 XTK-170036無法剖析運算式&#39;@id = @O5iRp40EGA&#39;。 | 404 — 無法解密PKey。 (PKey=@jksad)不支援的端點。 (endpoint=rest/profileAndServices/profile/@jksad) |
| 在URI和請求內文中使用兩個不同的原始Pkey | 500 - RST-360011發生錯誤 — 請聯絡您的管理員。 RST-360012資源&#39;service&#39;上的作業不一致 — 無法將索引鍵&#39;SVC3&#39;更新為&#39;SVC4&#39;。 | 500 — 發生錯誤 — 請聯絡您的管理員。 |
| 在URI中使用PKey，並在請求內文中使用不同的原始PKey | 500 — 具有相同索引鍵&#39;SVC4&#39;的&#39;Service&#39;已經存在。 PGS-220000 PostgreSQL錯誤：錯誤：重複的索引鍵值違反唯一條件約束「nmsservice_name」。詳細資料：索引鍵(sname)=(SVC4)已存在。 | 500 — 發生錯誤 — 請聯絡您的管理員。 |
| 在URI中使用不存在的原始識別碼 | 404 - RST-360011發生錯誤 — 請聯絡您的管理員。 無法從索引鍵「adobe_nl：0」（結構描述為「service」且名稱為「adobe_nl」的檔案）找到路徑為「Service」的檔案 | 404 — 無法從索引鍵「adobe_nl」找到路徑為「Service」的檔案（結構描述為「service」且名稱為「adobe_nl」的檔案） |
| 在請求內文中使用不存在的原始ID | 404 - RST-360011發生錯誤 — 請聯絡您的管理員。 無法從索引鍵「adobe_nl」找到路徑為「Service」的檔案（結構描述為「service」且名稱為「adobe_nl」的檔案） | 404 — 無法從索引鍵「adobe_nl」找到路徑為「Service」的檔案（結構描述為「service」且名稱為「adobe_nl」的檔案） |
| - | 500 - RST-360011發生錯誤 — 請聯絡您的管理員。 | 500 — 發生錯誤 — 請聯絡您的管理員。 |
| 插入包含無效性別（或任何）列舉值的設定檔/服務 | 500 - RST-360011發生錯誤 — 請聯絡您的管理員。 &#39;invalid&#39;值對&#39;@gender&#39;欄位的&#39;nms:recipient:gender&#39;列舉無效 | 500 — 發生錯誤 — 請聯絡您的管理員。 |

## 設定檔 — 時區

透過Campaign Standard，時區會顯示為&#x200B;**profileAndServices/profile** REST API呼叫的JSON回應的一部分。

使用Campaign v8時，時區只會顯示為&#x200B;**profileAndServicesExt/profile** REST API呼叫的一部分。 它不是&#x200B;**profileAndServices/profile** REST API呼叫的一部分，因為它已新增至擴充型結構描述。

## 工作流程 — 外部訊號觸發

Campaign Standard工作流程GETAPI會傳回引數名稱，例如工作流程例項變數及其資料型別（布林值、字串等）。 當透過POSTAPI呼叫觸發訊號時，可用來建立適當格式化的JSON要求內文。

Campaign v8不支援廣告工作流程執行個體變數，但預期開發人員會知道這些變數。 因此，在移轉後，若沒有POSTAPI回應中的引數資訊，就必須建構GET要求內文中的引數資訊。

<!--## Transactional messages

* With Campaign Standard, a POST request returns empty fields for elements and attributes in the request body. With Campaign v8, the response returns values that match the ones in the request body instead.

* When publishing an event configuration, the API preview panel displays the REST URL alongside the request body syntax.

    Since Campaign v8 does not support event configuration fields definition (event creation is just adding a value to eventType enumeration), there is no API preview panel when adding an event type. The REST URL is displayed  in the transactional message user interface once an event transactional message is published.-->
