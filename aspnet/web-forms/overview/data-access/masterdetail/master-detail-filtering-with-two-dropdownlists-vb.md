---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-vb
title: 마스터/세부 정보 필터링 (VB) Dropdownlist 두 개로 | Microsoft Docs
author: rick-anderson
description: 이 자습서는 두 DropDownList 컨트롤을 사용 하 여 원하는 부모 및 최상위 항목 레코드를 선택, 세 번째 계층을 추가 하려면 마스터/세부 관계를 확장 하는 중...
ms.author: aspnetcontent
ms.date: 03/31/2010
ms.assetid: 11ae4f64-01ba-4823-95f4-a2fe1f84f7d7
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-vb
msc.type: authoredcontent
ms.openlocfilehash: 17bbaa346925585b5b184127fa80fd2203869492
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37805287"
---
<a name="masterdetail-filtering-with-two-dropdownlists-vb"></a>마스터/세부 정보 (VB) Dropdownlist 두 개로 필터링
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_8_VB.exe) 또는 [PDF 다운로드](master-detail-filtering-with-two-dropdownlists-vb/_static/datatutorial08vb1.pdf)

> 이 자습서는 두 개의 DropDownList 컨트롤을 사용 하 여 원하는 부모 및 최상위 항목 레코드를 선택 하는 세 번째 계층을 추가 하려면 마스터/세부 관계를 확장 합니다.


## <a name="introduction"></a>소개

에 [이전 자습서](master-detail-filtering-with-a-dropdownlist-vb.md) 범주 및 선택한 범주에 속하는 해당 제품을 표시 하는 GridView로 채워진 단일 DropDownList를 사용 하 여 간단한 마스터/세부 정보 보고서를 표시 하는 방법을 살펴보았습니다. 이 보고서 패턴-일대다 관계가 설정 되어 있으며 여러에 일 대 다 관계를 포함 하는 시나리오에 맞게 쉽게 확장 될 수 있는 레코드를 표시 하는 경우에 작동 합니다. 예를 들어 주문 입력 시스템 테이블에 고객, 주문 및 주문 품목에 해당 하는 것입니다. 지정된 된 고객은 여러 항목으로 구성 된 각 순서를 사용 하 여 여러 개의 주문이 있을 수 있습니다. Dropdownlist 두 및 GridView를 사용 하 여 사용자에 게 이러한 데이터를 표시할 수 있습니다. 첫 번째 DropDownList 두 번째를 사용 하 여 데이터베이스에 있는 각 고객 목록 항목에는 선택한 고객의 주문 중인 1의 콘텐츠입니다. GridView는 선택한 주문의 품목을 나열 합니다.

Northwind 데이터베이스의 정식 순서/주문 고객/세부 정보를 포함 하는 동안 해당 `Customers`, `Orders`, 및 `Order Details` 아키텍처에는 테이블, 이러한 테이블 캡처되지 합니다. 그럼에도 불구 하 고 설명할 수 있습니다 여전히 두 종속 Dropdownlist를 사용 하 여 합니다. 첫 번째 DropDownList 표시 범주 및 두 번째 선택한 범주에 속하는 제품. 다음을 DetailsView 선택한 제품의 세부 정보를 나열 합니다.

## <a name="step-1-creating-and-populating-the-categories-dropdownlist"></a>1 단계: 만들기 및 범주 DropDownList를 채우기

첫 번째 목표는 범주를 나열 하는 드롭다운 목록에 추가 됩니다. 이러한 단계는 이전 자습서에서 자세히 살펴본 된 되지만 완전성을 위해 여기에 요약 되어.

열기는 `MasterDetailsDetails.aspx` 페이지에 `Filtering` 폴더 집합 페이지로 DropDownList를 추가 해당 `ID` 속성을 `Categories`, 스마트 태그의 데이터 소스 구성 링크를 클릭 하 고 합니다. 데이터 소스 구성 마법사에서 새 데이터 원본을 추가 하려면 선택 합니다.


[![DropDownList에 대 한 새 데이터 원본 추가](master-detail-filtering-with-two-dropdownlists-vb/_static/image2.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image1.png)

**그림 1**: 드롭다운 목록에 대 한 새 데이터 원본 추가 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-vb/_static/image3.png))


새 데이터 원본은 물론 되어야 ObjectDataSource 합니다. 이름을 새 ObjectDataSource `CategoriesDataSource` 호출 하도록 합니다 `CategoriesBLL` 개체의 `GetCategories()` 메서드.


[![CategoriesBLL 클래스를 사용 하려면 선택 합니다.](master-detail-filtering-with-two-dropdownlists-vb/_static/image5.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image4.png)

**그림 2**: 사용 하도록 선택 합니다 `CategoriesBLL` 클래스 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-two-dropdownlists-vb/_static/image6.png))


[![GetCategories() 메서드를 사용 하는 ObjectDataSource 구성](master-detail-filtering-with-two-dropdownlists-vb/_static/image8.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image7.png)

**그림 3**: ObjectDataSource 사용 하도록 구성 된 `GetCategories()` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-two-dropdownlists-vb/_static/image9.png))


ObjectDataSource를 구성한 후 해야 데이터 원본 필드에 표시 되도록 지정 합니다 `Categories` DropDownList 어느 목록 항목에 대 한 값으로 구성 해야 합니다. 설정 합니다 `CategoryName` 필드를 표시 하 고 `CategoryID` 각 목록 항목에 대 한 값으로.


[![가 DropDownList 표시를 사용 하 여 CategoryID와 CategoryName 필드 값](master-detail-filtering-with-two-dropdownlists-vb/_static/image11.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image10.png)

**그림 4**: DropDownList을 표시 합니다 `CategoryName` 필드 및 사용 `CategoryID` 값으로 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-two-dropdownlists-vb/_static/image12.png))


이 시점에서 DropDownList 컨트롤이 있습니다 (`Categories`)에서 기록으로 채워진는 `Categories` 테이블. 사용자가 드롭다운 목록에서 새 범주를 선택할 때 DropDownList 2 단계에서에서 만들 하려고 하는 제품을 새로 고치는 데 발생에 대 한 포스트백 하 려 합니다. 따라서에서 AutoPostBack을 사용 하도록 설정 옵션을 선택 합니다 `categories` DropDownList의 스마트 태그입니다.


[![범주 DropDownList에 AutoPostBack을 사용 하도록 설정](master-detail-filtering-with-two-dropdownlists-vb/_static/image14.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image13.png)

**그림 5**:에 대 한 AutoPostBack을 사용 하도록 설정 합니다 `Categories` DropDownList ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-two-dropdownlists-vb/_static/image15.png))


## <a name="step-2-displaying-the-selected-categorys-products-in-a-second-dropdownlist"></a>2 단계: 두 번째 DropDownList에 선택한 범주의 제품 표시

사용 하 여는 `Categories` DropDownList 완료, 다음 단계는 선택한 범주에 속하는 제품의 DropDownList를 표시 하는 것입니다. 이렇게 하려면 다른 DropDownList 라는 페이지에 추가 `ProductsByCategory`합니다. 와 마찬가지로 합니다 `Categories` 드롭다운 목록에서 만들기에 대 한 새 ObjectDataSource 합니다 `ProductsByCategory` DropDownList 라는 `ProductsByCategoryDataSource`.


[![ProductsByCategory DropDownList에 대 한 새 데이터 원본 추가](master-detail-filtering-with-two-dropdownlists-vb/_static/image17.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image16.png)

**그림 6**:에 대 한 새 데이터 원본을 추가 합니다 `ProductsByCategory` DropDownList ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-two-dropdownlists-vb/_static/image18.png))


[![ProductsByCategoryDataSource 라는 새로운 ObjectDataSource는 만들기](master-detail-filtering-with-two-dropdownlists-vb/_static/image20.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image19.png)

**그림 7**: 명명 된 새 ObjectDataSource 만들려면 `ProductsByCategoryDataSource` ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-two-dropdownlists-vb/_static/image21.png))


있으므로 합니다 `ProductsByCategory` 선택한 범주에 속하는 해당 제품을 전시 하기 DropDownList 요구를 호출 하는 ObjectDataSource가는 `GetProductsByCategoryID(categoryID)` 메서드에서 `ProductsBLL` 개체.


[![ProductsBLL 클래스를 사용 하려면 선택 합니다.](master-detail-filtering-with-two-dropdownlists-vb/_static/image23.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image22.png)

**그림 8**: 사용 하도록 선택 합니다 `ProductsBLL` 클래스 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-two-dropdownlists-vb/_static/image24.png))


[![GetProductsByCategoryID(categoryID) 메서드를 사용 하는 ObjectDataSource 구성](master-detail-filtering-with-two-dropdownlists-vb/_static/image26.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image25.png)

**그림 9**: ObjectDataSource 사용 하도록 구성 된 `GetProductsByCategoryID(categoryID)` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-two-dropdownlists-vb/_static/image27.png))


마법사의 마지막 단계에서의 값을 지정 해야 합니다 *`categoryID`* 매개 변수입니다. 이 매개 변수에서 선택한 항목에 할당 된 `Categories` DropDownList 합니다.


[![범주 드롭다운 목록에서 categoryID 매개 변수 값을 끌어오기](master-detail-filtering-with-two-dropdownlists-vb/_static/image29.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image28.png)

**그림 10**: 끌어오기는 *`categoryID`* 매개 변수 값을 `Categories` DropDownList ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-two-dropdownlists-vb/_static/image30.png))


구성 ObjectDataSource를 사용 하 여는 DropDownList의 항목 값을 표시 되는 데이터 원본 필드를 지정 합니다. 표시 된 `ProductName` 필드를 사용 하 여는 `ProductID` 값으로 필드입니다.


[![DropDownList의 ListItems 텍스트 및 값 속성에 사용 되는 데이터 원본 필드를 지정 합니다.](master-detail-filtering-with-two-dropdownlists-vb/_static/image32.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image31.png)

**그림 11**: 사용 되는 데이터 원본 필드를 지정 하 여 DropDownList에 대 한 `ListItem` s' `Text` 하 고 `Value` 속성 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-two-dropdownlists-vb/_static/image33.png))


ObjectDataSource를 사용 하 여 및 `ProductsByCategory` DropDownList 구성 페이지 Dropdownlist 두 표시 됩니다: 첫 번째 두 번째는 선택한 범주에 속하는 해당 제품을 나열 하는 동안 모든 범주가 나열 됩니다. 사용자가 첫 번째 드롭다운 목록에서 새 범주를 선택 하면 포스트백 계속 될 것 이라고 하 고 두 번째 DropDownList를 다시 바인딩할 새로 선택한 범주에 속하는 해당 제품을 표시 합니다. 그림 12, 13 표시 `MasterDetailsDetails.aspx` 브라우저를 통해 볼 때 작동에서 합니다.


[![음료 범주를 선택 하는 경우 먼저 페이지를 방문 하 고,](master-detail-filtering-with-two-dropdownlists-vb/_static/image35.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image34.png)

**그림 12**: 음료 범주를 선택 하는 경우 먼저 페이지를 방문 하 고, ([큰 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-vb/_static/image36.png))


[![다른 범주를 선택 하면 새 범주의 제품 표시 됩니다.](master-detail-filtering-with-two-dropdownlists-vb/_static/image38.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image37.png)

**그림 13**: 새 범주의 제품을 다른 범주 표시를 선택 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-vb/_static/image39.png))


현재는 `productsByCategory` DropDownList를 변경 하는 경우 않습니다 *하지* 포스트백을 발생 합니다. 그러나에서는 선택한 제품의 세부 정보 (3 단계)를 표시할 DetailsView 추가 되 면 되려면 다시 게시를 합니다. 따라서에서 AutoPostBack 사용 확인란을 `productsByCategory` DropDownList의 스마트 태그입니다.


[![DropDownList productsByCategory AutoPostBack 기능을 사용 하도록 설정](master-detail-filtering-with-two-dropdownlists-vb/_static/image41.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image40.png)

**그림 14**: AutoPostBack 기능을 사용 하도록 설정 합니다 `productsByCategory` DropDownList ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-two-dropdownlists-vb/_static/image42.png))


## <a name="step-3-using-a-detailsview-to-display-details-for-the-selected-product"></a>3 단계:는 DetailsView를 사용 하 여 선택한 제품에 대 한 세부 정보를 표시 하려면

마지막 단계는 DetailsView에서 선택한 제품에 대 한 세부 정보를 표시 하는 것입니다. 이렇게 DetailsView를 페이지에 추가 하려면 설정 해당 `ID` 속성을 `ProductDetails`에 대 한 새 ObjectDataSource를 만듭니다. 이 ObjectDataSource에서 해당 데이터를 가져오도록 구성 합니다 `ProductsBLL` 클래스의 `GetProductByProductID(productID)` 의 선택된 된 값을 사용 하 여 메서드를 `ProductsByCategory` DropDownList의 값에 대 한 합니다 *`productID`* 매개 변수.


[![ProductsBLL 클래스를 사용 하려면 선택 합니다.](master-detail-filtering-with-two-dropdownlists-vb/_static/image44.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image43.png)

**그림 15**: 사용 하도록 선택 합니다 `ProductsBLL` 클래스 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-two-dropdownlists-vb/_static/image45.png))


[![GetProductByProductID(productID) 메서드를 사용 하는 ObjectDataSource 구성](master-detail-filtering-with-two-dropdownlists-vb/_static/image47.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image46.png)

**그림 16**: ObjectDataSource 사용 하도록 구성 된 `GetProductByProductID(productID)` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-two-dropdownlists-vb/_static/image48.png))


[![ProductsByCategory 드롭다운 목록에서 매개 변수 값 productID 끌어오기](master-detail-filtering-with-two-dropdownlists-vb/_static/image50.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image49.png)

**그림 17**: 끌어오기는 *`productID`* 매개 변수 값을 `ProductsByCategory` DropDownList ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-two-dropdownlists-vb/_static/image51.png))


사용 가능한 필드 중 하나를 표시 하도록 선택할 수는 `ProductDetails` DetailsView 합니다. 제거 하기로 했습니다 합니다 `ProductID`, `SupplierID`, 및 `CategoryID` 필드 다시 정렬 하 고 나머지 필드를 포맷 합니다. 또한 out DetailsView의 선택을 취소 `Height` 및 `Width` 속성을 DetailsView 데이터 대신 지정된 된 크기를 제한 하기 최적으로 표시 하는 데 필요한 너비를 확장 합니다. 전체 태그 아래에 나타납니다.


[!code-aspx[Main](master-detail-filtering-with-two-dropdownlists-vb/samples/sample1.aspx)]

잠시 사용해는 `MasterDetailsDetails.aspx` 브라우저에서 페이지입니다. 얼핏 보기에 모든 것이 원하는 대로 작동 하지만 미묘한 문제가 나타날 수 있습니다. 새 범주를 선택 하는 경우는 `ProductsByCategory` DropDownList 선택한 범주에 대 한 해당 제품을 포함 하도록 업데이트 됩니다 있지만 `ProductDetails` DetailsView 계속 이전 제품 정보를 표시 합니다. DetailsView 선택한 범주에 대 한 다른 제품을 선택할 때 업데이트 됩니다. 또한 충분히 철저히 테스트 하는 경우 있습니다는 지속적으로 새 범주를 선택 하면 (에서 음료를 선택 하는 등의 `Categories` 드롭다운 목록에서를 입력 하면 조미료, 다음 과자류) 다른 모든 범주 선택 하면 합니다 `ProductDetails`DetailsView 새로 고쳐져 야 합니다.

이 문제를을 구체화할 수 있도록 하겠습니다 특정 예제를 살펴봅니다. 페이지를 처음 방문 하면 음료 범주를 선택 하 고 관련 된 제품에서 로드 되는 `ProductsByCategory` DropDownList 합니다. Chai 선택한 제품 이며 해당 세부 정보에 표시 되는 `ProductDetails` DetailsView 그림 18 에서처럼 합니다.


[![선택한 제품의 세부 정보를 DetailsView에 표시 됩니다.](master-detail-filtering-with-two-dropdownlists-vb/_static/image53.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image52.png)

**그림 18**: 선택한 제품의 세부 정보를 DetailsView에 표시 됩니다 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-vb/_static/image54.png))


포스트백이 발생할 음료 범주 선택 입력 하면 조미료를 변경 하면 및 `ProductsByCategory` DropDownList 그에 따라 업데이트 되지만 여전히 DetailsView Chai에 대 한 세부 정보를 표시 합니다.


[![이전에 선택한 제품의 세부 정보는 계속 표시](master-detail-filtering-with-two-dropdownlists-vb/_static/image56.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image55.png)

**그림 19**: 이전에 선택한 제품의 세부 정보는 계속 표시 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-vb/_static/image57.png))


선택 목록에서 새 제품을 예상 대로 DetailsView를 새로 고칩니다. 제품을 변경한 후 새 범주를 선택 하면 DetailsView 다시 새로 고치지 않습니다. 그러나 새 제품을 선택 하는 대신 새 범주를 선택한 경우 DetailsView 새로 고침 됩니다. 전 세계에서 무엇 일까요?

문제는 페이지의 수명 주기에서 타이밍 문제입니다. 때마다 페이지 렌더링 단계 숫자 진행 요청 됩니다. ObjectDataSource 컨트롤 있으면 확인이 단계 중 하나에 해당 `SelectParameters` 값이 변경 되었습니다. 따라서, 데이터 웹 컨트롤을 바인딩할 경우 ObjectDataSource 디스플레이 새로 고침 해야 한다고 알고 있습니다. 예를 들어, 새 범주를 선택할 경우 합니다 `ProductsByCategoryDataSource` ObjectDataSource의 매개 변수 값이 변경 되었는지 감지 및 `ProductsByCategory` DropDownList 다시 바인딩 횟수 자체 선택한 범주의 제품을 시작 합니다.

이 상황에서 발생 하는 문제는 변경 된 매개 변수는 경우, ObjectDataSources 확인 하는 페이지 수명 주기에서 발생 하는지 *하기 전에* 연결 된 데이터 웹 컨트롤의 다시 바인딩. 따라서 새 범주를 선택 하는 경우는 `ProductsByCategoryDataSource` ObjectDataSource의 매개 변수 값에서 변경을 감지 합니다. 사용 하는 ObjectDataSource 합니다 `ProductDetails` DetailsView 없습니다 그러나 이러한 변경 때문에 `ProductsByCategory` DropDownList를 아직 합니다. 수명 주기에서 나중의 `ProductsByCategory` DropDownList 새로 선택한 범주의 제품을 클릭 한 다음, 해당 ObjectDataSource에 다시 바인딩합니다. 하는 동안 합니다 `ProductsByCategory` DropDownList의 값이 변경의 `ProductDetails` DetailsView의 ObjectDataSource 이미 해당 매개 변수 값 확인을 수행 합니다. 즉 DetailsView 이전 결과 표시 하는 따라서 합니다. 이 상호 작용은 그림 20에서 표시 됩니다.


[![제품 세부 내용을 DetailsView ObjectDataSource의 변경 내용을 확인 한 후 ProductsByCategory DropDownList 값 변경](master-detail-filtering-with-two-dropdownlists-vb/_static/image59.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image58.png)

**그림 20**: 합니다 `ProductsByCategory` DropDownList 값 변경 후 합니다 `ProductDetails` DetailsView의 ObjectDataSource 변경에 대 한 확인 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-vb/_static/image60.png))


명시적으로 바인딩할 해야이 문제를 해결 하는 `ProductDetails` 후 DetailsView를 `ProductsByCategory` DropDownList 바인딩 되었습니다. 호출 하 여이 작업을 수행할 수 있습니다 것을 `ProductDetails` DetailsView의 `DataBind()` 메서드 때를 `ProductsByCategory` DropDownList의 `DataBound` 이벤트가 발생 합니다. 다음 이벤트 처리기 코드를 추가 합니다 `MasterDetailsDetails.aspx` 페이지의 코드 숨김 클래스 (참조는 "[ObjectDataSource의 매개 변수 값을 프로그래밍 방식으로 설정](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)" 이벤트 처리기를 추가 하는 방법에 대 한 논의):


[!code-vb[Main](master-detail-filtering-with-two-dropdownlists-vb/samples/sample2.vb)]

이 명시적으로 호출 후의 `ProductDetails` DetailsView의 `DataBind()` 예상 대로 작동 하는 자습서, 메서드가 추가 되었습니다. 이 변화는 그림 21 강조 표시 이전 문제를 해결 합니다.


[![제품 세부 내용을 DetailsView가 명시적으로 새로 고칠 때 the ProductsByCategory DropDownList의 데이터 바인딩된 이벤트 발생](master-detail-filtering-with-two-dropdownlists-vb/_static/image62.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image61.png)

**그림 21**: 합니다 `ProductDetails` DetailsView가 명시적으로 새로 고칠 때 합니다 `ProductsByCategory` DropDownList의 `DataBound` 이벤트가 발생 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-vb/_static/image63.png))


## <a name="summary"></a>요약

DropDownList 마스터/세부 정보 보고서에 대 한 이상적인 사용자 인터페이스 요소 역할도 마스터 / 세부 레코드 사이 일 대 다 관계가 있는 합니다. 이전 자습서에서 단일 DropDownList를 사용 하 여 선택한 범주에 따라 표시 되는 제품을 필터링 하는 방법에 살펴보았습니다. 이 자습서에서는 제품의 GridView DropDownList를 대체 하 고는 DetailsView 선택한 제품의 세부 정보를 표시 하는 데. 이 자습서에 설명 된 개념은 고객, 주문 및 주문 항목 등 여러 1 대 다 관계와 관련 된 데이터 모델을 쉽게 확장할 수 있습니다. 일반적으로 각에 일 대 다 관계의 한쪽 엔터티에 대해 항상 DropDownList를 추가할 수 있습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Hilton giesenow와 함께 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-filtering-with-a-dropdownlist-vb.md)
> [다음](master-detail-filtering-across-two-pages-vb.md)
