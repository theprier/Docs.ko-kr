---
uid: web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs
title: 추가 하 고 응답 하는 GridView (C#)에 단추 | Microsoft Docs
author: rick-anderson
description: 이 자습서와 GridView 또는 DetailsView 컨트롤의 필드에 서식 파일에 사용자 지정 단추를 추가 하는 방법을 살펴보겠습니다. 특히, त ु म च 작성기 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/13/2006
ms.topic: article
ms.assetid: 128fdb5f-4c5e-42b5-b485-f3aee90a8e38
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs
msc.type: authoredcontent
ms.openlocfilehash: 90648e10d5d058ea2e4aa5b3d8c4ed7448ea7166
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-and-responding-to-buttons-to-a-gridview-c"></a>추가 하 고 응답 하는 GridView (C#)에 단추
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_28_CS.exe) 또는 [PDF 다운로드](adding-and-responding-to-buttons-to-a-gridview-cs/_static/datatutorial28cs1.pdf)

> 이 자습서와 GridView 또는 DetailsView 컨트롤의 필드에 서식 파일에 사용자 지정 단추를 추가 하는 방법을 살펴보겠습니다. 특히, 사용자는 공급 업체를 통해 페이지 수 있도록 FormView 있는 인터페이스를 빌드합니다.


## <a name="introduction"></a>소개

보고서 데이터에 읽기 전용 액세스를 포함 하는 다양 한 보고 시나리오를 하는 동안 표시 되는 데이터를 기준으로 작업을 수행 하는 기능을 포함 하도록 보고서에 대 한 일반적이 지 않습니다. 일반적으로이 관련 된 각 레코드는 보고서에 표시할 단추, LinkButton을 또는 ImageButton 웹 컨트롤을 추가 하는를 클릭 하면 포스트백을 발생 하 고 일부 서버 쪽 코드를 호출 합니다. 편집 및-레코드도 데이터를 삭제은 가장 일반적인 예입니다. 사실, 부터는 살펴본 것 처럼는 [개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) 자습서, 편집 및 삭제는 GridView, DetailsView, FormView 컨트롤 없이 이러한 기능을 지원할 수 있는지는 많지는 코드의 한 줄도 작성 필요 합니다.

또한를 편집 및 삭제 단추, GridView, DetailsView, 및 FormView 컨트롤 포함할 수도 단추, 링크, 단추가 또는 ImageButtons를 클릭 하면 일부 사용자 지정 서버 쪽 논리를 수행 합니다. 이 자습서와 GridView 또는 DetailsView 컨트롤의 필드에 서식 파일에 사용자 지정 단추를 추가 하는 방법을 살펴보겠습니다. 특히, 사용자는 공급 업체를 통해 페이지 수 있도록 FormView 있는 인터페이스를 빌드합니다. 지정 된 공급자에 대 한 FormView 클릭 하면은 표시 관련 제품 중단 하는 단추 웹 컨트롤이 함께 공급자에 대 한 정보를 표시 됩니다. GridView 증가 가격과 할인 가격 하는 단추를 클릭 한 경우 높이 거 나 제품의 줄일 포함 된 각 행은 선택한 공급자가 제공 하는 해당 제품을 나열 하는 또한 `UnitPrice` 10% (그림 1 참조).


[![FormView와 GridView 포함 사용자 지정 작업을 수행 하는 단추](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image2.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image1.png)

**그림 1**: 모두 FormView 및 GridView 포함 단추는 사용자 지정 작업 수행 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image3.png))


## <a name="step-1-adding-the-button-tutorial-web-pages"></a>1 단계: 추가 단추 자습서 웹 페이지

사용자 지정 단추를 추가 하는 방법을 살펴보기 전에 먼저 간단히 살펴보겠습니다이 자습서에 사용 해야 하는 웹 사이트 프로젝트에 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `CustomButtons`합니다. 다음에 있는 각 페이지에 연결할 수 있도록 해당 폴더에 다음과 같은 두 ASP.NET 페이지를 추가 `Site.master` 마스터 페이지:

- `Default.aspx`
- `CustomButtons.aspx`


![사용자 지정 단추와 관련 된 자습서에 대 한 ASP.NET 페이지 추가](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image4.png)

**그림 2**: 사용자 지정 단추와 관련 된 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더에서와 같이 `Default.aspx` 에 `CustomButtons` 폴더는 해당 섹션의 자습서를 나열 합니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 이 기능을 제공 하는 사용자 정의 컨트롤입니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx` 페이지의 디자인 뷰에서 하려면 솔루션 탐색기에서 끌어서 합니다.


[![Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image6.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image5.png)

**그림 3**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image7.png))


마지막으로, 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히, 페이징 및 정렬 한 후에 다음 태그를 추가할 `<siteMapNode>`:

[!code-xml[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 브라우저를 통해 자습서 웹 사이트를 보려면 보십시오. 왼쪽 메뉴에는 이제 편집, 삽입 및 삭제 자습서에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 사용자 지정 단추 자습서에 대 한 항목을 포함](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image8.png)

**그림 4**: 이제 사이트 맵 사용자 지정 단추 자습서에 대 한 항목을 포함


## <a name="step-2-adding-a-formview-that-lists-the-suppliers"></a>2 단계: 추가 공급자를 나열 하는 FormView

이제 시작 하겠습니다이 자습서와 함께 공급 업체를 나열 하 여 FormView를 추가 하 여. 소개 부분에서 설명 했 듯이이 FormView는 수는 GridView에 공급 업체에서 제공 하는 제품을 보여 주는 공급 업체, 페이징할 수 있습니다. 또한이 FormView에는 단추가 포함 됩니다를 클릭 하면은 표시 모든 공급 업체의 제품의 사용이 중지 합니다. 먼저 म 하는 데 문제가 논의 FormView에 사용자 지정 단추를 추가, 보겠습니다 방금 만듭니다 FormView 공급 업체 정보 표시 되도록 합니다.

열어 시작는 `CustomButtons.aspx` 페이지에 `CustomButtons` 폴더입니다. 도구 상자에서 디자이너와 세트가으로 끌어 페이지에는 FormView 추가 해당 `ID` 속성을 `Suppliers`합니다. FormView의 스마트 태그에서 만들도록 선택한 라는 새 ObjectDataSource `SuppliersDataSource`합니다.


[![SuppliersDataSource 라는 새 ObjectDataSource 만들기](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image10.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image9.png)

**그림 5**: 명명 된 새 ObjectDataSource 만드는 `SuppliersDataSource` ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image11.png))


구성에서 쿼리를이 새 ObjectDataSource는 `SuppliersBLL` 클래스의 `GetSuppliers()` 메서드 (그림 6 참조). 이 FormView에서 공급 업체 정보를 선택 (없음) 업데이트 탭에서 드롭 다운 목록에서 옵션을 업데이트 하기 위한 인터페이스를 제공 하지 않습니다.


[![S GetSuppliers() 메서드 SuppliersBLL 클래스를 사용 하도록 데이터 원본을 구성합니다](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image13.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image12.png)

**그림 6**: 사용 하도록 데이터 원본을 구성는 `SuppliersBLL` 클래스의 `GetSuppliers()` 메서드 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image14.png))


ObjectDataSource를 구성한 후 Visual Studio에서 생성 한 `InsertItemTemplate`, `EditItemTemplate`, 및 `ItemTemplate` FormView에 대 한 합니다. 제거는 `InsertItemTemplate` 및 `EditItemTemplate` 및 수정 된 `ItemTemplate` 공급 업체의 회사 이름과 전화 번호만 표시 되도록 합니다. 마지막으로, 스마트 태그에서 페이징 사용 확인란을 선택 하 여 FormView에 대 한 페이징 지원을 설정 (또는 설정 하 여 해당 `AllowPaging` 속성을 `True`). 이러한 변경 된 후 페이지의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample2.aspx)]

그림 7 CustomButtons.aspx 페이지를 브라우저를 통해 볼 때를 보여줍니다.


[![FormView는 CompanyName 및 현재 선택 된 공급 업체에서 전화 번호 필드를 나열합니다.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image16.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image15.png)

**그림 7**: The FormView 나열 된 `CompanyName` 및 `Phone` 현재 선택 된 공급자 로부터 필드 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image17.png))


## <a name="step-3-adding-a-gridview-that-lists-the-selected-suppliers-products"></a>3 단계: 추가 선택한 공급 업체의 제품을 나열 하는 GridView

FormView의 서식 파일에 모든 제품을 중단 단추를 추가 하기 전에 먼저 추가해보겠습니다 선택한 공급자가 제공 하는 제품을 나열 하 여 FormView 아래에 GridView. 이 위해를 추가 하려면는 GridView 페이지로 설정 해당 `ID` 속성을 `SuppliersProducts`, 라는 새 ObjectDataSource 추가 `SuppliersProductsDataSource`합니다.


[![SuppliersProductsDataSource 라는 새 ObjectDataSource 만들기](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image19.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image18.png)

**그림 8**: 명명 된 새 ObjectDataSource 만드는 `SuppliersProductsDataSource` ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image20.png))


구성 ProductsBLL 클래스를 사용 하려면이 ObjectDataSource `GetProductsBySupplierID(supplierID)` 메서드 (그림 9 참조). 이 GridView 조정 해야 하는 제품의 가격에 대 한을 허용 하는 동안 편집 하거나 기능을 GridView에서에서 삭제 하는 기본 제공을 사용 하지 않습니다. 따라서는 ObjectDataSource의 UPDATE, INSERT 및 탭은 삭제할 드롭 다운 목록 (없음)으로 설정할 수 있습니다.


[![S GetProductsBySupplierID(supplierID) 메서드 ProductsBLL 클래스를 사용 하도록 데이터 원본을 구성합니다](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image22.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image21.png)

**그림 9**: 사용 하도록 데이터 원본을 구성는 `ProductsBLL` 클래스의 `GetProductsBySupplierID(supplierID)` 메서드 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image23.png))


이후는 `GetProductsBySupplierID(supplierID)` 입력된 매개 변수를 허용 하는 메서드, ObjectDataSource 만들라는 주세요.이 매개 변수 값의 출처입니다. 에 전달 하는 `SupplierID` FormView에서 값을 제어 및 ControlID 드롭 다운 목록에 매개 변수 소스 드롭 다운 목록 설정 `Suppliers` (2 단계에서에서 만든 FormView의 ID)입니다.


[![SupplierID 매개 변수는에서 가져왔는지 Suppliers FormView 컨트롤 표시](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image25.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image24.png)

**그림 10**: 있음을 *`supplierID`* 매개 변수에서 가져와야 하는 `Suppliers` FormView 컨트롤 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image26.png))


ObjectDataSource 마법사를 완료 한 후 GridView가 BoundField 또는 CheckBoxField 각 제품의 데이터 필드에 대해 포함 됩니다. 보겠습니다 축소이 표시 테이블만 `ProductName` 및 `UnitPrice` BoundFields와 함께 `Discontinued` CheckBoxField; 또한에 서식을 지정 하겠습니다는 `UnitPrice` BoundField를 해당 텍스트를 통화 형식을 지정 합니다. 에 GridView 및 `SuppliersProductsDataSource` ObjectDataSource의 선언적 태그에 다음 태그 유사 합니다.

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample3.aspx)]

이 시점에서 자습서에는 사용자가 맨 위에 있는 FormView에서 공급 업체를 선택 하 고 맨 아래에 GridView 통해 해당 공급 업체에서 제공 하는 제품을 볼 수 있도록 마스터/세부 정보 보고서를 표시 합니다. 그림 11 FormView에서 도쿄 무역 공급 업체가 제공을 선택할 때이 페이지의 스크린 샷을 보여 줍니다.


[![선택한 공급 업체의 제품 GridView에 표시 됩니다.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image28.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image27.png)

**그림 11**: The 선택한 공급 업체의 제품 GridView에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image29.png))


## <a name="step-4-creating-dal-and-bll-methods-to-discontinue-all-products-for-a-supplier"></a>4 단계: 공급 업체에 대 한 모든 제품을 중단 하려면 DAL 및 BLL 메서드 만들기

FormView에 단추를 추가 하기 전에, 모두 중단 됩니다를 클릭 하면 공급 업체의 제품의 먼저 필요 DAL 및 BLL이이 작업을 수행 하는 메서드를 추가 하 합니다. 이 메서드를 지정 됩니다. 특히, `DiscontinueAllProductsForSupplier(supplierID)`합니다. FormView의 단추를 클릭할 때 म 합니다이 메서드를 호출 비즈니스 논리 계층에 전달에서 선택한 공급자의 `SupplierID`; 그런 다음 BLL이 호출에서 발생 하는 해당 데이터 액세스 계층 메서드로 `UPDATE` 문 데이터베이스에 지정 된 공급 업체의 제품을 중단 하는 합니다.

우리의 이전 자습서에 했던 대로에서는 상향식 접근 DAL 메서드를 다음 BLL 메서드를 작성 및 마지막으로 ASP.NET 페이지의 기능을 구현부터 시작 합니다. 열기는 `Northwind.xsd` 형식화 된 데이터 집합에는 `App_Code/DAL` 폴더에 새 메서드를 추가 하 고는 `ProductsTableAdapter` (마우스 오른쪽 단추로 클릭는 `ProductsTableAdapter` Query 추가 선택 하 고). 이렇게 우리 새 메서드를 추가 하는 과정을 안내 하는 TableAdapter 쿼리 구성 마법사를 표시 합니다. 우리의 DAL 메서드는 임시 SQL 문 사용을 시작 합니다.


[![임시 SQL 문을 사용 하 여 DAL 메서드 만들기](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image31.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image30.png)

**그림 12**: 특별 SQL 문을 사용 하 여 DAL 메서드 만들기 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image32.png))


다음으로, 마법사 어떤 유형의 쿼리를 만들에 대 한 미국 메시지 표시 합니다. 이후는 `DiscontinueAllProductsForSupplier(supplierID)` 메서드를 업데이트 해야 합니다는 `Products` 설정 하는 데이터베이스 테이블의 `Discontinued` 필드를 지정 된에서 제공 하는 모든 제품에 대 한 1 *`supplierID`*, 데이터를 업데이트 하는 쿼리를 만들어야 하 합니다.


[![업데이트 쿼리 형식 선택](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image34.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image33.png)

**그림 13**: 업데이트 쿼리 형식 선택 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image35.png))


마법사의 다음 화면에서는 TableAdapter의 기존 `UPDATE` 각에 정의 된 필드를 업데이트 하는 문에 `Products` DataTable입니다. 이 쿼리 텍스트를 다음 문으로 바꿉니다.

[!code-sql[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample4.sql)]

이 쿼리를 입력 하 고 다음을 클릭 한 후 마법사의 마지막 화면 새 메서드의 이름 사용 하기 위해 요청 `DiscontinueAllProductsForSupplier`합니다. "마침" 단추를 클릭 하 여 마법사를 완료 합니다. 데이터 집합 디자이너를 반환할 때에 새로운 방법이 표시 됩니다는 `ProductsTableAdapter` 라는 `DiscontinueAllProductsForSupplier(@SupplierID)`합니다.


[![새 DAL 메서드 DiscontinueAllProductsForSupplier 이름](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image37.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image36.png)

**그림 14**: 새 DAL 메서드 이름을 `DiscontinueAllProductsForSupplier` ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image38.png))


와 `DiscontinueAllProductsForSupplier(supplierID)` 우리의 다음 작업은 데이터 액세스 계층에서 만든 메서드를 만드는 것은 `DiscontinueAllProductsForSupplier(supplierID)` 비즈니스 논리 계층에서 메서드. 이를 위해 열고는 `ProductsBLL` 클래스 파일을 다음에 추가 합니다.

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample5.cs)]

이 메서드를 단순히 호출는 `DiscontinueAllProductsForSupplier(supplierID)` 메서드 함께 제공 된 전달 DAL에서 *`supplierID`* 매개 변수 값입니다. 특정 상황에서 중단 되도록 공급 업체의 제품에만 허용 하는 모든 비즈니스 규칙 인 경우 이러한 규칙 BLL에 여기에서 구현 되어야 합니다.

> [!NOTE]
> 와 달리는 `UpdateProduct` 에서 오버 로드는 `ProductsBLL` 클래스는 `DiscontinueAllProductsForSupplier(supplierID)` 메서드 시그니처는 포함 되지 않습니다는 `DataObjectMethodAttribute` 특성 (`<System.ComponentModel.DataObjectMethodAttribute(System.ComponentModel.DataObjectMethodType.Update, Boolean)>`). 이 인덱스나 관계는 `DiscontinueAllProductsForSupplier(supplierID)` 업데이트 탭 ObjectDataSource의 데이터 소스 구성 마법사의 드롭다운 목록에서 메서드. I 했습니다 호출할 때문에이 특성을 생략는 `DiscontinueAllProductsForSupplier(supplierID)` 가격 ASP.NET 페이지에서 이벤트 처리기에서 직접 메서드.


## <a name="step-5-adding-a-discontinue-all-products-button-to-the-formview"></a>5 단계: 추가 된 모든 제품 단추 FormView 중단 합니다.

와 `DiscontinueAllProductsForSupplier(supplierID)` 에 BLL 및 완료 DAL, 선택한 공급자에 대 한 모든 제품을 중단 하는 기능을 추가 하기 위한 마지막 단계는 Button 웹 컨트롤을 FormView의 추가 `ItemTemplate`합니다. 모든 제품을 중단 단추 텍스트와 공급 업체의 전화 번호 아래 단추를 추가 해 보겠습니다 및 `ID` 속성 값이 `DiscontinueAllProductsForSupplier`합니다. FormView의 스마트 태그에서 템플릿 편집 링크를 클릭 하 여 디자이너를 통해이 단추 웹 컨트롤을 추가할 수 있습니다 (그림 15 참조) 또는 선언적 구문을 통해 직접 합니다.


[![추가 된 모든 제품 단추 웹 컨트롤 FormView의 ItemTemplate 중단 합니다.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image40.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image39.png)

**그림 15**:는 중단 모든 제품 단추 웹 컨트롤을 추가 FormView의 `ItemTemplate` ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image41.png))


FormView의 페이지에서 포스트백 계속 사용자 방문 여는 단추를 클릭할 때 [ `ItemCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.itemcommand.aspx) 발생 합니다. 이 단추 클릭 되 고이에 대 한 응답 사용자 지정 코드를 실행 하려면이 이벤트에 대 한 이벤트 처리기를 만들 수 있습니다. 이해, 하지만 하는 `ItemCommand` 이벤트가 발생할 때마다 *모든* FormView 안에서 LinkButton을 단추나 ImageButton 웹 컨트롤을 클릭 합니다. 즉, 사용자는 FormView에서 다른 한 페이지에서 이동할 때의 `ItemCommand` 이벤트 발생 않으면 새로 만들기, 편집를 클릭 하거나 삽입, 업데이트 또는 삭제를 지 원하는 FormView에서 삭제 하는 경우 동일 합니다.

이후는 `ItemCommand` 이벤트 처리기를 모든 제품을 중단 단추 클릭 한 경우 확인 하는 방법이 필요 또는 기타 단추 인 경우 어떤 단추를 클릭 하는 것에 관계 없이 발생 합니다. 이를 위해 웹 단추 컨트롤의 설정할 수 있습니다 `CommandName` 속성을 식별 일부 값입니다. 단추를 클릭할 때,이 `CommandName` 에 값이 전달 되는 `ItemCommand` 수 있어 모든 제품을 중단 단추는 단추 클릭 했는지 확인 하려면 이벤트 처리기입니다. 중단 모든 제품 단추의 설정 `CommandName` 속성 DiscontinueProducts 합니다.

마지막으로, 선택한 공급 업체의 제품을 중단 하려면 사용자가 실제로 있는지 확인 하는 클라이언트 쪽 확인 대화 상자를 사용 합니다. 설명한 것 처럼는 [추가 클라이언트 쪽 확인 때 삭제](../editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs.md) 자습서, 약간 JavaScript의이 작업을 수행할 수 있습니다. 특히, Button 웹 컨트롤 OnClientClick 속성을 설정 `return confirm('This will mark _all_ of this supplier\'s products as discontinued. Are you certain you want to do this?');`

다음과 같이 변경한 후 FormView의 선언적 구문 다음과 같이 표시 됩니다.

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample6.aspx)]

FormView의에 대 한 이벤트 처리기를 다음으로 만들고 `ItemCommand` 이벤트입니다. 이 이벤트 처리기에서 먼저 모든 제품을 중단 단추가 클릭 되었습니다 여부를 결정 해야 합니다. 인스턴스를 만드는 할까요,는 `ProductsBLL` 클래스 및 호출 해당 `DiscontinueAllProductsForSupplier(supplierID)` 전달 하는 메서드는 `SupplierID` 선택한 FormView의:

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample7.cs)]

`SupplierID` FormView에서 현재 선택 된 공급 업체의 액세스할 수 FormView의를 사용 하 여 [ `SelectedValue` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.selectedvalue.aspx)합니다. `SelectedValue` 속성 첫 번째 데이터 키 FormView에 표시 되는 레코드에 대 한 값을 반환 합니다. FormView의 [ `DataKeyNames` 속성](https://msdn.microsoft.com/system.web.ui.webcontrols.formview.datakeynames.aspx),으로 자동으로 설정 된에서 필드를 데이터 값을 키를 가져오는 데이터를 나타내는 `SupplierID` 는 ObjectDataSource FormView에 바인딩할 때 Visual Studio에서 2 단계에 다시.

와 `ItemCommand` 이벤트 처리기를 만든 보십시오 페이지를 테스트 합니다. Cooperativa de Quesos로 이동 ' Las Cabras' 공급 업체 (이 다섯 번째 레코드에 내 FormView). 이 공급자를 두 개의 제품이 Queso Cabrales 및 Queso Manchego La Pastora 둘 다 제공 *하지* 중단 되었습니다.

Cooperativa de Quesos ' Las Cabras' 벗어난 비즈니스 해당 제품은 중단 되도록 하는 따라서 한다고 가정 합니다. 클릭는 모든 제품 단추를 중단 합니다. 클라이언트 쪽 확인 대화 상자가 표시 됩니다 상자 (그림 16 참조).


[![Cooperativa de Quesos Las Cabras 공급 두 활성 제품](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image43.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image42.png)

**그림 16**: Cooperativa de Quesos Las Cabras 공급 제품 두 개의 활성 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image44.png))


클라이언트 쪽 확인 대화 상자에서 확인을 클릭 하면 양식 전송이 진행 됩니다는 포스트백을 발생 시키거나 FormView의 `ItemCommand` 이벤트가 발생 합니다. 호출 만든 이벤트 처리기가 실행 한 다음는 `DiscontinueAllProductsForSupplier(supplierID)` 메서드와 Queso Cabrales와 Queso Manchego La Pastora 제품을 중단 합니다.

GridView의 뷰 상태를 비활성화 한 경우 GridView 포스트백이 발생할 때마다, 기본 데이터 저장소에 리바운드 되 고 고 따라서는 즉시 반영 하도록 업데이트는이 두 제품은 이제 사용 되지 않습니다 (그림 17 참조). 그러나 GridView에서 뷰 상태를 해제 하지 않은, 경우에이 같이 변경한 후 GridView에 데이터를 수동으로 다시 바인딩 해야 합니다. 이를 위해 GridView의 호출을 수행 하면 `DataBind()` 호출 직후 메서드는 `DiscontinueAllProductsForSupplier(supplierID)` 메서드.


[![모든 제품을 중단 단추를 클릭 한 후 s 공급 업체 제품에 업데이트 됩니다.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image46.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image45.png)

**그림 17**: 모든 제품을 중단 단추를 클릭 한 후 공급 업체의 제품에 업데이트 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image47.png))


## <a name="step-6-creating-an-updateproduct-overload-in-the-business-logic-layer-for-adjusting-a-products-price"></a>6 단계: 제품의 가격을 조정 하기 위한 비즈니스 논리 계층에서 UpdateProduct 오버 로드를 만들기

마찬가지로 모든 제품을 중단 단추는 FormView에서 GridView의 제품에 대 한 가격을 늘리고에 대 한 단추를 추가 하기 위해 해야 먼저 적절 한 데이터 액세스 계층 및 비즈니스 논리 계층 메서드를 추가 합니다. DAL에 단일 제품 행을 업데이트 하는 메서드를 이미 했기 때문에 대 한 새 오버 로드를 만들어서 이러한 기능을 제공할 수 있습니다는 `UpdateProduct` BLL에 메서드.

우리의 과거 `UpdateProduct` 오버 로드 스칼라 입력된 값으로 제품 필드 중 일부 조합에서 사항이 다음 지정된 된 제품에 대 한 필드를 업데이트 합니다. 이 오버 로드에 대해이 표준에서 조금씩 알아보고는 제품에 대신 전달 하겠습니다 `ProductID` 및 비율 조정에 사용 되는 `UnitPrice` (새 전달, 달리 조정 `UnitPrice` 자체). 이 방법을 사용 하면 현재 제품의 판단에 대해서는 신경 쓰지 않아도 되므로 ASP.NET 페이지 코드 숨김 클래스에서 작성 해야 하는 코드를 간편 하 게 `UnitPrice`합니다.

`UpdateProduct` 아래 나와이 자습서에 대 한 오버 로드 합니다.

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample8.cs)]

이 오버 로드는 DAL 통해 지정된 된 제품에 대 한 정보를 검색 `GetProductByProductID(productID)` 메서드. 참조를 확인 하는지 여부를 제품의 `UnitPrice` 는 데이터베이스가 할당 `NULL` 값입니다. 가격 남아 인 경우 변경 되지 않도록 합니다. 그러나이 아닌 경우`NULL` `UnitPrice` 값, 메서드는 제품의 업데이트 `UnitPrice` 지정 된 % (`unitPriceAdjustmentPercent`).

## <a name="step-7-adding-the-increase-and-decrease-buttons-to-the-gridview"></a>GridView에 증가 및 감소 단추를 추가 하는 7 단계:

GridView (및 DetailsView) 둘 다 구성 된 필드의 컬렉션입니다. ASP.NET 및 뿐만 아니라 BoundFields, CheckBoxFields, TemplateFields, 이름에서 알 수 있듯이 각 행에 대해 단추나 LinkButton을 ImageButton 인 열으로 렌더링 하는 ButtonField를 포함 합니다. 클릭 하 여 FormView 비슷합니다 *모든* GridView 페이징 단추, 편집 또는 삭제 단추, 단추 정렬, 및 등 내에서 단추 포스트백 및 GridView의 발생 [ `RowCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowcommand.aspx)합니다.

ButtonField에는 `CommandName` 각 단추에 지정 된 값을 할당 하는 속성 `CommandName` 속성입니다. FormView와 함께 `CommandName` 값에서 사용 됩니다는 `RowCommand` 이벤트 처리기는 단추를 클릭 했는지 확인 합니다.

단추 텍스트 가격 + 10으로 GridView에 두 개의 새 ButtonFields을 추가 하겠습니다. % 오류 코드 및 텍스트-10 가격와 기타 %입니다. 이러한 ButtonFields를 추가 하려면 GridView의 스마트 태그에서 열 편집 링크를 클릭 하 고 왼쪽 위에 있는 목록에서 ButtonField 필드 유형을 선택 추가 단추를 클릭 합니다.


![두 개의 ButtonFields GridView에 추가](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image48.png)

**그림 18**: 두 ButtonFields GridView에 추가


처음 두 GridView 필드로 표시 되도록 두 개의 ButtonFields를 이동 합니다. 다음으로 설정 된 `Text` 가격 + 10 %를 이러한 두 ButtonFields 및 Price-10의 속성 %와 `CommandName` IncreasePrice 고 DecreasePrice, 속성을 각각. 기본적으로는 ButtonField 링크 단추가으로 단추의 해당 열을 렌더링합니다. 그러나이 변경할 수 있습니다, ButtonField의 통해 [ `ButtonType` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.buttonfieldbase.buttontype.aspx)합니다. 이러한 두 ButtonFields 일반 누름 단추;로 렌더링 죠 따라서 설정 하는 `ButtonType` 속성을 `Button`합니다. 그림 19 필드 대화 상자를 표시 한 후 이러한 변경 사항이; 그 다음에 GridView의 선언적 태그입니다.


![ButtonFields 텍스트, CommandName, 및 ButtonType 속성 구성](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image49.png)

**그림 19**:는 ButtonFields 구성 `Text`, `CommandName`, 및 `ButtonType` 속성


[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample9.aspx)]

만든 이러한 ButtonFields, 마지막 단계는 GridView의에 대 한 이벤트 처리기를 만들 것 `RowCommand` 이벤트입니다. 때문에 발생 한 경우이 이벤트 처리기는 가격 + 10% 또는 가격-10% 단추 클릭 된를 결정 하는 요구는 `ProductID` 단추를 클릭 한 다음 행에 대 한는 `ProductsBLL` 클래스의 `UpdateProduct` 적절 한 전달 메서드 `UnitPrice` 와 함께 비율 조정은 `ProductID`합니다. 다음 코드에서는 이러한 작업을 수행합니다.

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample10.cs)]

확인 하기 위해는 `ProductID` 행에 대 한 가격 + 10% 또는 가격-10% 단추가 클릭 되었습니다, GridView의를 참조 해야 `DataKeys` 컬렉션입니다. 이 컬렉션에 지정 된 필드의 값만 포함 된 `DataKeyNames` 각 GridView 행에 대 한 속성입니다. GridView의 이후 `DataKeyNames` 속성이로 설정 된 ProductID Visual Studio에서 GridView에는 ObjectDataSource를 바인딩할 때 `DataKeys(rowIndex).Value` 제공는 `ProductID` 지정 된 *rowIndex*합니다.

ButtonField에 자동으로 전달 된 *rowIndex* 를 통해 해당 단추를 클릭 한 행의는 `e.CommandArgument` 매개 변수입니다. 따라서 결정 하는 `ProductID` 행에 대 한 가격 + 10% 또는 가격-10% 단추가 클릭 되었습니다, 사용: `Convert.ToInt32(SuppliersProducts.DataKeys(Convert.ToInt32(e.CommandArgument)).Value)`합니다.

로 모든 제품을 중단 단추와 GridView의 뷰 상태를 해제 한 경우 GridView 포스트백이 발생할 때마다, 기본 데이터 저장소에 리바운드 되 고 고 따라서 즉시 업데이트 됩니다를 클릭 하면 발생 하 여 가격 변경을 반영 하기 위해 단추 중 하나입니다. 그러나 GridView에서 뷰 상태를 해제 하지 않은, 경우에이 같이 변경한 후 GridView에 데이터를 수동으로 다시 바인딩 해야 합니다. 이를 위해 GridView의 호출을 수행 하면 `DataBind()` 호출 직후 메서드는 `UpdateProduct` 메서드.

그림 20 대양 농산에서 제공 하는 제품을 볼 때 페이지를 보여줍니다. 그림 21는 % 버튼을 클릭 할머니의 블루베리 확산 및 Price-10% 단추에 대해 두 번 한 번 대양 특선 딸기 소스에 대 한 가격 + 10 후 결과.


[![GridView 포함 가격 + 10% 및 가격-10% 단추](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image51.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image50.png)

**그림 20**: GridView 포함 가격 + 10% 및 % 단추 가격-10 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image52.png))


[![첫 번째 및 세 번째 제품에 대 한 가격 + 10 가격을 통해 업데이트 되었습니다. % 및 가격-10% 단추](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image54.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image53.png)

**그림 21**: The 가격을 첫 번째 및 세 번째 제품 업데이트 되었습니다. + 10 가격을 통해 % 및 % 단추 가격-10 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image55.png))


> [!NOTE]
> GridView (및 DetailsView) 단추, 링크 단추가, 또는 해당 TemplateFields에 추가 ImageButtons 있을 수도 있습니다. BoundField, 이러한 단추를 클릭 하면는 포스트백을 유도할 됩니다, 처럼 발생 GridView의 `RowCommand` 이벤트입니다. 그러나 때 추가 단추를 TemplateField 단추의 `CommandArgument` ButtonFields를 사용 하 여 일 때와 행의 인덱스를 자동으로 설정 되지 됩니다. 내에서 클릭 된 단추의의 행 인덱스를 결정 하는 경우는 `RowCommand` 단추의 수동으로 설정 해야 이벤트 처리기 `CommandArgument` 같은 코드를 사용 하 여 TemplateField 내에서 해당 선언적 구문에서 속성:  
> `<asp:Button runat="server" ... CommandArgument='<%# ((GridViewRow) Container).RowIndex %>'`.


## <a name="summary"></a>요약

단추, 링크, 단추가 또는 ImageButtons GridView, DetailsView, 및 FormView 컨트롤을 모두 포함할 수 있습니다. 이러한 단추를 클릭 하면 포스트백을 발생 시키고는 `ItemCommand` FormView 및 DetailsView 컨트롤에 이벤트 및 `RowCommand` GridView에서 이벤트입니다. 이러한 데이터 웹 컨트롤 삭제 레코드 편집 등과 같은 일반 명령 관련 동작을 처리 하도록 기본 제공 기능이 있습니다. 그러나을 활용해 서도 사용 하 여 단추를 클릭 했을 때, 고유한 사용자 지정 코드를 실행 하 여 응답 합니다.

이 수행 하기에 대 한 이벤트 처리기를 만들고 해야는 `ItemCommand` 또는 `RowCommand` 이벤트입니다. 이 이벤트 처리기에서 먼저 확인 들어오는 `CommandName` 단추를 클릭 했는지 확인 한 다음 적절 한 조치 사용자 지정 하는 값입니다. 이 자습서를 사용 하 여 단추와 ButtonFields 지정 된 공급자에 대 한 모든 제품을 중단 높이 거 나 특정 제품의 가격을 10% 감소 하는 방법에 살펴보았습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [다음](adding-and-responding-to-buttons-to-a-gridview-vb.md)
