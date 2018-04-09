---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-cs
title: 마스터/세부 두 dropdownlist 활용 (C#)를 사용 하 여 필터링 | Microsoft Docs
author: rick-anderson
description: 이 자습서는 DropDownList 컨트롤을 두 가지를 사용 하 여 원하는 부모 및 최상위 항목 recor 선택, 세 번째 계층을 추가 하려면 마스터/세부 관계를 확장 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: ac4b0d77-4816-4ded-afd0-88dab667aedd
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-cs
msc.type: authoredcontent
ms.openlocfilehash: d971dcb3814dc088202c3a3e4addb03375049ca0
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="masterdetail-filtering-with-two-dropdownlists-c"></a>마스터/세부 두 dropdownlist 활용 (C#)를 사용 하 여 필터링
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_8_CS.exe) 또는 [PDF 다운로드](master-detail-filtering-with-two-dropdownlists-cs/_static/datatutorial08cs1.pdf)

> 이 자습서에서는 두 DropDownList 컨트롤을 사용 하 여 원하는 부모 및 최상위 항목 레코드를 선택 하는 세 번째 계층을 추가 하려면 마스터/세부 관계를 확장 합니다.


## <a name="introduction"></a>소개

에 [이전 자습서](master-detail-filtering-with-a-dropdownlist-cs.md) 된 범주 및 선택한 범주에 속해 있는 해당 제품을 표시 하는 GridView 단일 DropDownList를 사용 하 여 간단한 마스터/세부 정보 보고서를 표시 하는 방법을 검사 했습니다. 이 보고서 패턴 대 다 관계가 설정 되어 있으며 여러 대 다 관계를 포함 하는 시나리오에 대 한 작업으로 손쉽게 확장할 수 있는 레코드를 표시 하는 경우에 작동 합니다. 예를 들어 주문 입력 시스템 테이블에 고객, 주문 및 주문 라인 항목에 해당 하는 것입니다. 지정 된 고객은 여러 항목으로 구성 된 각 order에 여러 주문 있을 수 있습니다. 이러한 데이터는 GridView 두 dropdownlist 활용와 사용자에 게 표시할 수 있습니다. 첫 번째 DropDownList 각 고객 데이터베이스에 있는 두 번째 목록 항목이 선택된 된 고객의 주문 되 고 1의 콘텐츠입니다. GridView는 선택 된 주문의 품목을 나열 합니다.

Northwind 데이터베이스에 정식 고객/순서/주문 세부 정보를 포함 하는 동안 해당 `Customers`, `Orders`, 및 `Order Details` 가이드의 아키텍처에서 테이블, 이러한 테이블은 캡처할 되지 않습니다. 그럼에도 불구 하 고 설명할 수 있습니다 여전히 두 종속 dropdownlist 활용을 사용 하 여 합니다. 첫 번째 DropDownList 나열 됩니다는 범주와 두 번째 선택한 범주에 속하는 제품. DetailsView은 다음 선택된 된 제품의 세부 정보를 나열 합니다.

## <a name="step-1-creating-and-populating-the-categories-dropdownlist"></a>1 단계: 만들기 및 범주 DropDownList를 채우기

첫 번째 목표 범주를 나열 하는 DropDownList를 추가 하는 것입니다. 이러한 단계 이전 자습서를 자세히 검사 되지만 완전성을 위해 여기 요약 되어 있습니다.

열기는 `MasterDetailsDetails.aspx` 페이지에 `Filtering` 폴더 설정 페이지에 DropDownList를 추가 해당 `ID` 속성을 `Categories`을 클릭 한 다음 스마트 태그에 데이터 소스 구성 링크를 클릭 합니다. 데이터 소스 구성 마법사에서 새 데이터 원본을 추가 하려면 선택 합니다.


[![드롭다운 목록에 대 한 새 데이터 소스를 추가 합니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image2.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image1.png)

**그림 1**: 드롭다운 목록에 대 한 새 데이터 원본을 추가 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image3.png))


새 데이터 원본, 당연히 해야는 ObjectDataSource 합니다. 이 새 ObjectDataSource 이름을 `CategoriesDataSource` 호출 게는 `CategoriesBLL` 개체의 `GetCategories()` 메서드.


[![CategoriesBLL 클래스를 사용 하려면 선택 합니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image5.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image4.png)

**그림 2**: 사용 하도록 선택 된 `CategoriesBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image6.png))


[![ObjectDataSource GetCategories() 메서드를 사용 하도록 구성](master-detail-filtering-with-two-dropdownlists-cs/_static/image8.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image7.png)

**그림 3**: 구성에 사용 하 여 ObjectDataSource는 `GetCategories()` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image9.png))


ObjectDataSource를 구성한 후 작업을 계속 합니다 데이터 소스 필드에 표시 되도록 지정 된 `Categories` DropDownList 어떤 목록 항목에 대 한 값으로 구성 해야 합니다. 설정의 `CategoryName` 디스플레이와 필드 및 `CategoryID` 각 목록 항목에 대 한 값으로.


[![DropDownList 표시 범주 필드와 사용 하 여 CategoryID는는 값으로](master-detail-filtering-with-two-dropdownlists-cs/_static/image11.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image10.png)

**그림 4**: DropDownList 디스플레이 `CategoryName` 필드 및 사용 `CategoryID` 값으로 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image12.png))


이 시점에서 DropDownList 컨트롤이 (`Categories`)의 레코드와 채워집니다는 `Categories` 테이블입니다. 드롭다운 목록에서 새 범주를 선택 하면 발생 하 여 2 단계에서에서 만드는 DropDownList 제품을 새로 고치는 데에 대 한 포스트백을 좋을 것입니다. 따라서에서 AutoPostBack 사용 옵션을 선택는 `categories` DropDownList의 스마트 태그입니다.


[![AutoPostBack 범주 드롭다운 목록에 대 한 사용](master-detail-filtering-with-two-dropdownlists-cs/_static/image14.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image13.png)

**그림 5**:에 대 한 사용 AutoPostBack는 `Categories` DropDownList ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image15.png))


## <a name="step-2-displaying-the-selected-categorys-products-in-a-second-dropdownlist"></a>2 단계: 두 번째 DropDownList에 선택한 범주의 제품 표시

와 `Categories` DropDownList 완료 되 면 다음 단계는 선택한 범주에 속하는 제품의 DropDownList를 표시 합니다. 이를 위해 다른 DropDownList 라는 페이지에 추가 `ProductsByCategory`합니다. 과 마찬가지로 `Categories` DropDownList를 만들기에 대 한 새 ObjectDataSource는 `ProductsByCategory` 라는 DropDownList `ProductsByCategoryDataSource`합니다.


[![ProductsByCategory 드롭다운 목록에 대 한 새 데이터 소스를 추가 합니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image17.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image16.png)

**그림 6**:에 대 한 새 데이터 원본을 추가 `ProductsByCategory` DropDownList ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image18.png))


[![ProductsByCategoryDataSource 라는 새 ObjectDataSource 만들기](master-detail-filtering-with-two-dropdownlists-cs/_static/image20.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image19.png)

**그림 7**: 명명 된 새 ObjectDataSource 만드는 `ProductsByCategoryDataSource` ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image21.png))


이후는 `ProductsByCategory` DropDownList 요구 된 선택한 범주에 속하는 제품을 표시 하는 호출 ObjectDataSource는 `GetProductsByCategoryID(categoryID)` 에서 메서드는 `ProductsBLL` 개체입니다.


[![ProductsBLL 클래스를 사용 하려면 선택 합니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image23.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image22.png)

**그림 8**: 사용 하도록 선택 된 `ProductsBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image24.png))


[![ObjectDataSource GetProductsByCategoryID(categoryID) 메서드를 사용 하도록 구성](master-detail-filtering-with-two-dropdownlists-cs/_static/image26.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image25.png)

**그림 9**: 구성에 사용 하 여 ObjectDataSource는 `GetProductsByCategoryID(categoryID)` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image27.png))


값을 지정 해야 마법사의 마지막 단계에서는 *`categoryID`* 매개 변수입니다. 이 매개 변수에서 선택한 항목에 할당 된 `Categories` DropDownList 합니다.


[![범주 드롭다운 목록에서 매개 변수 값 categoryID 끌어오기](master-detail-filtering-with-two-dropdownlists-cs/_static/image29.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image28.png)

**그림 10**: 끌어오기는 *`categoryID`* 에서 매개 변수 값은 `Categories` DropDownList ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image30.png))


구성 된 ObjectDataSource를 사용 하는 모든 남아 지정 하는 것 어떤 데이터 소스 필드를 표시 하 고 DropDownList의 항목의 값 사용 됩니다. 표시는 `ProductName` 필드를 사용 하 여는 `ProductID` 값 필드입니다.


[![DropDownList의 ListItems 텍스트 및 값 속성에 사용 되는 데이터 원본 필드를 지정 합니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image32.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image31.png)

**그림 11**: 사용 되는 데이터 원본 필드의 드롭다운 목록에 대 한 지정 `ListItem` s' `Text` 및 `Value` 속성 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image33.png))


ObjectDataSource와 및 `ProductsByCategory` DropDownList 구성 가격 페이지 두 dropdownlist 활용 ½ ֳ µ: 첫 번째 두 번째는 선택한 범주에 속하는 제품을 나열 하는 동안 모든 범주가 나열 됩니다. 첫 번째 드롭다운 목록에서 새 범주를 선택 하면 계속 다시 게시 될 것 이라고 하 고 두 번째 DropDownList은 다시 바인딩할 수에 새로 선택한 범주에 속해 있는 해당 제품을 표시 합니다. 그림 12 및 13 표시 `MasterDetailsDetails.aspx` 브라우저를 통해 볼 때 작동에서 합니다.


[![음료 범주를 선택 하는 페이지를 처음 방문 하는 경우](master-detail-filtering-with-two-dropdownlists-cs/_static/image35.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image34.png)

**그림 12**: 음료 범주를 선택 하는 페이지를 처음 방문 하는 경우 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image36.png))


[![새 범주의 제품을 다른 범주를 선택 하면 표시 됩니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image38.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image37.png)

**그림 13**: 새 범주의 제품 다른 범주 표시를 선택 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image39.png))


현재는 `productsByCategory` DropDownList를 변경 되 면 않습니다 *하지* 포스트백을 발생 합니다. 그러나 한 다시 게시를 선택된 된 제품 세부 정보 (3 단계)를 표시 하려면 DetailsView 추가 되 면 발생 합니다. 따라서 확인란을 사용 하도록 설정 AutoPostBack에서는 `productsByCategory` DropDownList의 스마트 태그입니다.


[![ProductsByCategory DropDownList에 대 한 AutoPostBack 기능을 사용 하도록 설정](master-detail-filtering-with-two-dropdownlists-cs/_static/image41.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image40.png)

**그림 14**:에 대 한 AutoPostBack 기능을 사용 하도록 설정 된 `productsByCategory` DropDownList ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image42.png))


## <a name="step-3-using-a-detailsview-to-display-details-for-the-selected-product"></a>3 단계: DetailsView를 사용 하 여 선택한 제품에 대 한 정보를 표시 하려면

마지막 단계는 DetailsView에 선택한 제품에 대 한 세부 정보를 표시 하는 것입니다. 이 위해를 추가 하려면 DetailsView 페이지로 설정 해당 `ID` 속성을 `ProductDetails`에 대 한 새 ObjectDataSource를 만듭니다. 구성에서 해당 데이터를 가져오도록이 ObjectDataSource는 `ProductsBLL` 클래스의 `GetProductByProductID(productID)` 의 선택된 된 값을 사용 하 여 메서드는 `ProductsByCategory` 의 값에 필요한 DropDownList는 *`productID`* 매개 변수입니다.


[![ProductsBLL 클래스를 사용 하려면 선택 합니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image44.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image43.png)

**그림 15**: 사용 하도록 선택 된 `ProductsBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image45.png))


[![ObjectDataSource GetProductByProductID(productID) 메서드를 사용 하도록 구성](master-detail-filtering-with-two-dropdownlists-cs/_static/image47.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image46.png)

**그림 16**: 구성에 사용 하 여 ObjectDataSource는 `GetProductByProductID(productID)` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image48.png))


[![ProductsByCategory 드롭다운 목록에서 매개 변수 값 productID 끌어오기](master-detail-filtering-with-two-dropdownlists-cs/_static/image50.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image49.png)

**그림 17**: 끌어오기는 *`productID`* 에서 매개 변수 값은 `ProductsByCategory` DropDownList ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image51.png))


DetailsView에서 사용 가능한 필드를 표시할 수 있습니다. 제거를 선택한 이유는 `ProductID`, `SupplierID`, 및 `CategoryID` 필드 다시 정렬 하 고 나머지 필드 형식이 지정 합니다. DetailsView의을 선택을 취소 또한 `Height` 및 `Width` 속성을 DetailsView 데이터 대신 지정 된 크기로 제한 최적으로 표시 하는 데 필요한 너비를 확장 합니다. 전체 태그 아래에 나타납니다.


[!code-aspx[Main](master-detail-filtering-with-two-dropdownlists-cs/samples/sample1.aspx)]

사용해 보십시오는 `MasterDetailsDetails.aspx` 브라우저에서 페이지입니다. 얼핏 보기에 원하는 대로 모든 기능이 작동 하지만 미묘한 문제가 나타날 수 있습니다. 새 범주를 선택 하는 경우는 `ProductsByCategory` DropDownList 선택한 범주에 대 한 해당 제품을 포함 하도록 업데이트 됩니다 되지만 `ProductDetails` DetailsView 계속 이전 제품 정보를 표시 합니다. DetailsView에는 선택한 범주에 대 한 다른 제품을 선택할 때 업데이트 됩니다. 또한 충분히 철저히 테스트 하는 경우 있습니다를 지속적으로 새 범주를 선택 하는 경우 (에서 음료를 선택 하는 등의 `Categories` DropDownList를 다음 입력 하면 조미료, 다음 과자류) 마다 다른 범주 선택 하면는 `ProductDetails`DetailsView를 새로 고칠 수 있습니다.

이 문제를 구체화할 하려면 살펴보겠습니다는 특정 예제. 먼저 해당 페이지를 방문 하면 음료 범주를 선택 하 고 관련된 제품에 로드 된는 `ProductsByCategory` DropDownList 합니다. Chai 응용 프로그램은 선택한 제품 및 해당 세부 정보가 표시 됩니다는 `ProductDetails` DetailsView, 그림 18과 같이 합니다.


[![DetailsView에 선택한 제품의 세부 정보가 표시 됩니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image53.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image52.png)

**그림 18**: DetailsView의 선택 된 제품의 세부 정보가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image54.png))


포스트백이 발생할 조미료로 음료에서 범주 선택을 변경한 경우 및 `ProductsByCategory` DropDownList 적절 하 게 업데이트 되지만 여전히 DetailsView Chai에 대 한 세부 정보를 표시 합니다.


[![이전에 선택한 제품의 세부 정보는 계속 표시](master-detail-filtering-with-two-dropdownlists-cs/_static/image56.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image55.png)

**그림 19**: 이전에 선택한 제품의 세부 정보는 계속 표시 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image57.png))


선택 목록에서 새 제품을 예상 대로 DetailsView를 새로 고칩니다. 제품을 변경한 후 새 범주를 선택 하면 DetailsView 다시 새로 고치지 않습니다. 그러나 새 제품을 선택 하는 대신 새 범주를 선택한 경우 DetailsView 새로 고침 합니다. 전 세계에는 무슨 일 여기?

문제는 페이지의 수명 주기의 타이밍 문제입니다. 때마다 페이지를 사용 하는 렌더링으로는 몇 가지 단계를 진행 요청 됩니다. 다음이 단계 중 하나에 ObjectDataSource 제어 중 없는지 확인 자신의 `SelectParameters` 값이 변경 되었습니다. 데이터 웹 컨트롤에 연결 하는 등의 ObjectDataSource의 표시를 새로 고칠 필요가 있는 알고 있습니다. 예를 들어 새 범주를 선택 하면는 `ProductsByCategoryDataSource` ObjectDataSource에서 해당 매개 변수 값이 변경 되었는지 검색 및 `ProductsByCategory` DropDownList 다시 바인딩 횟수 자체 선택한 범주의 제품을 시작 합니다.

포인트는 ObjectDataSources 변경 된 매개 변수를 확인 하는 페이지 수명 주기에서 발생 하 고이 경우에 발생 하는 문제 *하기 전에* 웹 컨트롤 관련된 데이터를 다시 바인딩해야 합니다. 따라서 새 범주를 선택 하는 경우는 `ProductsByCategoryDataSource` ObjectDataSource에서 해당 매개 변수 값에 변경 내용을 검색 합니다. 그러나 사용 하는 ObjectDataSource는 `ProductDetails` DetailsView, 하지 않는 참고 변경 하기 때문에 `ProductsByCategory` DropDownList는 아직 다시 바인딩할 수 있습니다. 수명 주기의 뒷부분에 나오는 `ProductsByCategory` DropDownList 새로 선택한 범주의 제품을 클릭 한 다음 해당 ObjectDataSource에 다시 바인딩합니다. 동안는 `ProductsByCategory` DropDownList의 값이 변경 되는 `ProductDetails` DetailsView의 ObjectDataSource에서 매개 변수 값 검사를 이미 완료; 따라서 DetailsView 이전 결과 표시 합니다. 그림 20에서이 상호 작용 표시 됩니다.


[![제품 세부 내용을 DetailsView의 ObjectDataSource 변경 내용을 확인 한 후 ProductsByCategory DropDownList 값이 변경](master-detail-filtering-with-two-dropdownlists-cs/_static/image59.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image58.png)

**그림 20**:는 `ProductsByCategory` DropDownList 값 변경 후의 `ProductDetails` 변경 내용을 DetailsView의 ObjectDataSource 확인 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image60.png))


명시적으로 바인딩할 해야이 해결 하려면는 `ProductDetails` 후 DetailsView의 `ProductsByCategory` DropDownList 바인딩 되었습니다. 호출 하 여이 작업을 수행할 수 있습니다는 `ProductDetails` DetailsView의 `DataBind()` 메서드 때는 `ProductsByCategory` DropDownList의 `DataBound` 이벤트 발생 합니다. 다음 이벤트 처리기 코드를 추가 하는 `MasterDetailsDetails.aspx` 페이지의 코드 숨김 클래스 (참조는 "[ObjectDataSource의 매개 변수 값을 프로그래밍 방식으로 설정](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)" 이벤트 처리기를 추가 하는 방법에 대 한 내용은):


[!code-csharp[Main](master-detail-filtering-with-two-dropdownlists-cs/samples/sample2.cs)]

이 명시적으로 호출 후의 `ProductDetails` DetailsView의 `DataBind()` 예상 대로 작동 하는 자습서, 메서드가 추가 되었습니다. 그림 21 하이라이트 어떻게 변경 이전 문제를 해결 합니다.


[![제품 세부 내용을 DetailsView은 명시적으로 새로 고칠 때 the ProductsByCategory DropDownList의 데이터 바인딩된 이벤트 발생](master-detail-filtering-with-two-dropdownlists-cs/_static/image62.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image61.png)

**그림 21**:는 `ProductDetails` DetailsView은 명시적으로 새로 고칠 경우는 `ProductsByCategory` DropDownList의 `DataBound` 이벤트 발생 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image63.png))


## <a name="summary"></a>요약

마스터/세부 정보 보고서에 대 한 이상적인 사용자 인터페이스 요소로 DropDownList 역할 마스터 / 세부 레코드 간에 일 대 다 관계는 합니다. 이전 자습서에서 단일 DropDownList를 사용 하 여 선택한 범주에서 표시 되는 제품을 필터링 하는 방법에 살펴보았습니다. 이 자습서에서는 제품의 GridView DropDownList를 바꿔야 하 고 DetailsView 선택된 된 제품의 정보를 표시 하는 데 사용 합니다. 이 자습서에 설명 된 개념은 고객, 주문 및 주문 항목 등 여러 1 대 다 관계와 관련 된 데이터 모델을 쉽게 확장할 수 있습니다. 일반적으로 각 일 대 다 관계의 "일" 엔터티에 대 한 언제 DropDownList를 추가할 수 있습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Hilton Giesenow 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-filtering-with-a-dropdownlist-cs.md)
> [다음](master-detail-filtering-across-two-pages-cs.md)
