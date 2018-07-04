---
uid: web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs
title: 추가 (C#) GridView에 단추를 하 고 응답 | Microsoft Docs
author: rick-anderson
description: 이 자습서는 템플릿에 GridView 또는 DetailsView 컨트롤의 필드에 사용자 지정 단추를 추가 하는 방법을 살펴보겠습니다. 특히 빌드를 합니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/13/2006
ms.topic: article
ms.assetid: 128fdb5f-4c5e-42b5-b485-f3aee90a8e38
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs
msc.type: authoredcontent
ms.openlocfilehash: 25e9574a861d23579ce1a18da895159d47881457
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368595"
---
<a name="adding-and-responding-to-buttons-to-a-gridview-c"></a>추가 (C#) GridView에 단추를 하 고 응답
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_28_CS.exe) 또는 [PDF 다운로드](adding-and-responding-to-buttons-to-a-gridview-cs/_static/datatutorial28cs1.pdf)

> 이 자습서는 템플릿에 GridView 또는 DetailsView 컨트롤의 필드에 사용자 지정 단추를 추가 하는 방법을 살펴보겠습니다. 특히, 공급 업체를 통해 페이지를 사용 하면 FormView 있는 인터페이스를 빌드 해 보겠습니다.


## <a name="introduction"></a>소개

보고서 데이터에 대 한 읽기 전용 액세스를 포함 하는 다양 한 보고 시나리오를 하는 동안 보고서에 표시 되는 데이터에 따라 작업을 수행 하는 기능을 포함 하려면도 드물지 않습니다. 일반적으로이 관련 된 보고서에 표시 되는 각 레코드를 사용 하 여 단추, LinkButton, ImageButton 웹 컨트롤을 추가 클릭 하면 포스트백을 발생 시키는 및 일부 서버 쪽 코드를 호출 합니다. 레코드에서 기준 데이터 편집 및 삭제는 가장 일반적인 예입니다. 부터 본 것 처럼, 실제로 [개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) 자습서, 편집 및 삭제 하는 GridView, DetailsView 및 FormView 컨트롤 하지 않고 이러한 기능을 지원할 수 있는지 일반적인 합니다 코드 한 줄도 작성에 대 한 필요 합니다.

또한 편집 및 삭제 단추, GridView, DetailsView 및 FormView 컨트롤 포함할 수도 Linkbutton을 단추나 ImageButtons,를 클릭 하면 일부 사용자 지정 서버 쪽 논리를 수행 합니다. 이 자습서는 템플릿에 GridView 또는 DetailsView 컨트롤의 필드에 사용자 지정 단추를 추가 하는 방법을 살펴보겠습니다. 특히, 공급 업체를 통해 페이지를 사용 하면 FormView 있는 인터페이스를 빌드 해 보겠습니다. 지정 된 공급자, FormView 단추를 클릭 하면 됩니다 됨으로 관련 제품 중단 하는 단추 웹 컨트롤이 함께 공급자에 대 한 정보를 표시 됩니다. GridView 증가 가격 및 단추를 클릭 하면 발생 하거나 제품의 줄이기는 할인 가격 단추가 포함 된 각 행을 사용 하 여 선택한 공급자가 제공 하는 이러한 제품을 나열 하는 또한 `UnitPrice` 10% (그림 1 참조).


[![FormView 및 GridView에는 사용자 지정 작업을 수행 하는 단추가 포함](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image2.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image1.png)

**그림 1**: 두 FormView 및 GridView 포함 단추는 사용자 지정 작업 수행 ([큰 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image3.png))


## <a name="step-1-adding-the-button-tutorial-web-pages"></a>1 단계: 추가 단추 자습서 웹 페이지

사용자 지정 단추를 추가 하는 방법을 살펴보기 전에 먼저 살펴보겠습니다이 자습서용 해야 하는 웹 사이트 프로젝트에서 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `CustomButtons`합니다. 다음에 있는 각 페이지에 연결할 수 있도록 해당 폴더에 다음 두 ASP.NET 페이지를 추가 합니다 `Site.master` 마스터 페이지:

- `Default.aspx`
- `CustomButtons.aspx`


![사용자 지정 단추 관련 자습서에 대 한 ASP.NET 페이지 추가](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image4.png)

**그림 2**: 사용자 지정 단추 관련 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더와 같이 `Default.aspx` 에 `CustomButtons` 폴더 섹션의 자습서를 나열 됩니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 사용자 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx` 페이지의 디자인 뷰로 솔루션 탐색기에서 끌어 합니다.


[![Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image6.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image5.png)

**그림 3**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 `Default.aspx` ([클릭 하 여 큰 이미지 보기](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image7.png))


마지막으로, 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히, 페이징 및 정렬 한 후 다음 태그를 추가 `<siteMapNode>`:

[!code-xml[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 잠시 브라우저를 통해 자습서 웹 사이트를 확인 합니다. 왼쪽 메뉴에는 이제 편집, 삽입 및 삭제 자습서에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 사용자 지정 단추 자습서에 대 한 항목을 포함](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image8.png)

**그림 4**: 이제 사이트 맵 사용자 지정 단추 자습서에 대 한 항목을 포함


## <a name="step-2-adding-a-formview-that-lists-the-suppliers"></a>2 단계: 추가 공급자를 나열 하는 FormView

시작이 자습서를 사용 하 여 공급자를 나열 하는 FormView를 추가 하 여 합니다. 소개에서 설명 했 듯이이 FormView GridView에서 공급자가 제공 하는 제품을 보여 주는 공급 업체를 통해 페이지에서 사용자가 수입니다. 또한이 FormView 단추는를 클릭 하면 표시 됩니다 모든 공급 업체의 제품 지원 되지 않는으로 합니다. 우리가 하는 데 문제가 직접 FormView에 사용자 지정 단추를 추가, 전에 먼저 만들겠습니다 FormView 공급자 정보를 표시 합니다.

열어서 시작 합니다 `CustomButtons.aspx` 페이지에 `CustomButtons` 폴더입니다. FormView 집합과 디자이너 도구 상자에서 끌어와 페이지에 추가할 해당 `ID` 속성을 `Suppliers`입니다. FormView의 스마트 태그를 만들도록 선택할 라는 새로운 ObjectDataSource는 `SuppliersDataSource`합니다.


[![SuppliersDataSource 라는 새로운 ObjectDataSource는 만들기](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image10.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image9.png)

**그림 10**: 합니다 `SuppliersDataSource` 하 고 [ Dropdownlist를 포함 하는 (없음) 옵션 (](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image11.png)클릭 하 여 큰 이미지 보기)


쿼리는이 새 ObjectDataSource를 구성 합니다 `SuppliersBLL` 클래스의 `GetSuppliers()` 메서드 (그림 6 참조). 이후이 FormView 공급 업체 정보, 선택 [업데이트] 탭의 드롭다운 목록에서 옵션 (없음)를 업데이트 하기 위한 인터페이스를 제공 하지 않습니다.


[![S GetSuppliers() 메서드 SuppliersBLL 클래스를 사용 하는 데이터 원본의 구성](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image13.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image12.png)

**그림 6**: 사용 하도록 데이터 원본을 구성 합니다 `SuppliersBLL` 클래스의 `GetSuppliers()` 메서드 ([클릭 하 여 큰 이미지 보기](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image14.png))


ObjectDataSource를 구성한 후 Visual Studio에서 생성 한 `InsertItemTemplate`, `EditItemTemplate`, 및 `ItemTemplate` FormView에 대 한. 제거 합니다 `InsertItemTemplate` 및 `EditItemTemplate` 수정 하 고는 `ItemTemplate` 공급 업체의 회사 이름과 전화 번호만 표시 되도록 합니다. 마지막으로, 스마트 태그에서의 페이징 사용 확인란을 선택 하 여 페이징 지원을 FormView 켜기 (또는 설정 하 여 해당 `AllowPaging` 속성을 `True`). 이러한 변경 된 후 페이지의 선언적 태그는 다음과 같아야 합니다.

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample2.aspx)]

그림 7에서는 브라우저를 통해 볼 때 CustomButtons.aspx 페이지를 보여 줍니다.


[![FormView의 CompanyName 및 현재 선택 된 공급자 로부터 전화 필드를 나열합니다.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image16.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image15.png)

**그림 7**: The FormView 나열 합니다 `CompanyName` 하 고 `Phone` 현재 선택한 공급자에서 필드 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image17.png))


## <a name="step-3-adding-a-gridview-that-lists-the-selected-suppliers-products"></a>3 단계: 추가 선택한 공급 업체의 제품을 나열 하는 GridView

FormView의 템플릿을 모든 제품을 중단 단추를 추가 하기 전에 먼저 추가해보겠습니다 FormView 선택한 공급자가 제공 하는 제품을 나열 하는 아래에 GridView입니다. 이렇게 GridView를 페이지에 추가 하려면 해당 `ID` 속성을 `SuppliersProducts`, 라는 새로운 ObjectDataSource는 추가 `SuppliersProductsDataSource`합니다.


[![SuppliersProductsDataSource 라는 새로운 ObjectDataSource는 만들기](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image19.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image18.png)

**그림 8**: 명명 된 새 ObjectDataSource 만들려면 `SuppliersProductsDataSource` ([클릭 하 여 큰 이미지 보기](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image20.png))


ProductsBLL 클래스의 사용 하 여이 ObjectDataSource 구성 `GetProductsBySupplierID(supplierID)` 메서드 (그림 9 참조). 이 GridView를 조정 해야 하는 제품의 가격에 대 한 허용, 편집 또는 GridView에서 기능을 삭제 하는 기본 제공을 사용 하지 않습니다. 따라서 ObjectDataSource의 UPDATE, INSERT 및 탭 삭제에 대 한 드롭다운 목록 (None)으로 설정할 수 있습니다.


[![S GetProductsBySupplierID(supplierID) 메서드 ProductsBLL 클래스를 사용 하는 데이터 원본의 구성](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image22.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image21.png)

**그림 9**: 사용 하도록 데이터 원본을 구성 합니다 `ProductsBLL` 클래스의 `GetProductsBySupplierID(supplierID)` 메서드 ([클릭 하 여 큰 이미지 보기](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image23.png))


이후를 `GetProductsBySupplierID(supplierID)` 메서드에서 입력된 매개 변수, ObjectDataSource 마법사는이 매개 변수 값의 원본에 대 한 요청입니다. 전달 된 `SupplierID` FormView에서 값을 매개 변수 원본 드롭다운 목록 컨트롤 및 ControlID 드롭 다운 목록으로 설정 `Suppliers` (FormView의 ID는 2 단계에서에서 만든).


[![supplierID 매개 변수에서에서 가져와야 Suppliers FormView 컨트롤 표시](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image25.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image24.png)

**그림 10**: 나타내는 합니다 *`supplierID`* 매개 변수에서 가져와야 하는 `Suppliers` FormView 컨트롤 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image26.png))


ObjectDataSource 마법사를 완료 한 후 GridView가 BoundField 또는 CheckBoxField 각 제품의 데이터 필드에 대 한 포함 됩니다. 보겠습니다 줄여야이 표시할만 `ProductName` 및 `UnitPrice` 함께 BoundFields를 `Discontinued` CheckBoxField; 또한 보겠습니다 형식를 `UnitPrice` BoundField 해당 텍스트를 통화로 형식이 되도록 합니다. 에 GridView 및 `SuppliersProductsDataSource` ObjectDataSource의 선언 태그는 다음 태그와 비슷하게 표시 됩니다.

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample3.aspx)]

이 시점에서 자습서는 사용자가 맨 위에 있는 FormView에서 공급 업체를 선택 하 고 맨 아래에 GridView 통해 해당 공급 업체에서 제공 하는 제품을 볼 수 있도록 마스터/세부 정보 보고서를 표시 합니다. 그림 11 FormView에서 도쿄 Traders 공급자를 선택 하는 경우이 페이지의 스크린 샷을 보여 줍니다.


[![선택한 공급자가의 제품 GridView에 표시 됩니다.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image28.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image27.png)

**그림 11**: GridView에는 선택한 공급자의 제품 표시 됩니다 ([큰 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image29.png))


## <a name="step-4-creating-dal-and-bll-methods-to-discontinue-all-products-for-a-supplier"></a>4 단계: 만들기 DAL 메서드와 BLL 공급자에 대 한 모든 제품을 중단

FormView에 단추를 추가할 수 있기 전에,를 클릭 하면 중단 모든 공급 업체의 제품에서는 먼저이 작업을 수행 하는 BLL 및 DAL에 메서드를 추가 합니다. 이 메서드 이름은 특히 `DiscontinueAllProductsForSupplier(supplierID)`합니다. FormView의 단추를 클릭 하면 됩니다 호출 비즈니스 논리 계층에서이 메서드 전달에서 선택한 공급자의 `SupplierID`; BLL을 호출 합니다 발급할는 해당 데이터 액세스 계층 메서드를 `UPDATE` 문 데이터베이스에는 지정 된 공급자의 제품을 중단합니다.

이전 자습서에서 수행한 대로 사용 하겠습니다 상향식 경우 DAL 메서드를 다음 BLL 메서드를 만들고 마지막으로 ASP.NET 페이지에서 기능을 구현부터. 열기를 `Northwind.xsd` 형식화 된 데이터 집합에는 `App_Code/DAL` 폴더에 새 메서드를 추가 하 고를 `ProductsTableAdapter` (마우스 오른쪽 단추로 클릭는 `ProductsTableAdapter` 쿼리 추가 선택 하 고). 이렇게 우리는 새 메서드를 추가 하는 과정을 안내 하는 TableAdapter 쿼리 구성 마법사를 표시 합니다. DAL 메서드는 임시 SQL 문을 사용 하 여 지정 하 여 시작 합니다.


[![임시 SQL 문을 사용 하는 DAL 메서드 만들기](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image31.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image30.png)

**그림 12**: 임시 SQL 문을 사용 하 여 DAL 메서드를 만듭니다 ([큰 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image32.png))


다음으로, 마법사 요청 만들 쿼리 유형을 대 한 합니다. 이후를 `DiscontinueAllProductsForSupplier(supplierID)` 메서드를 업데이트 해야 합니다는 `Products` 데이터베이스 테이블에 설정를 `Discontinued` 필드를 지정 된 제공 하는 모든 제품에 대 한 1 *`supplierID`*, 데이터를 업데이트 하는 쿼리를 만들어야 합니다.


[![업데이트 쿼리 형식 선택](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image34.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image33.png)

**그림 13**: 업데이트 쿼리 형식을 선택 ([큰 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image35.png))


마법사의 다음 화면에서는 TableAdapter의 기존 제공 `UPDATE` 각 정의 된 필드를 업데이트 하는 문을 `Products` DataTable입니다. 다음 문을 사용 하 여이 쿼리 텍스트를 바꿉니다.

[!code-sql[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample4.sql)]

이 쿼리를 입력 하 고 다음을 클릭 하면, 마법사의 마지막 화면 새 메서드의 이름 사용 하기 위해 요청 `DiscontinueAllProductsForSupplier`합니다. "마침" 단추를 클릭 하 여 마법사를 완료 합니다. 데이터 집합 디자이너 돌아가면의 새로운 방법으로 표시 되어야 합니다 `ProductsTableAdapter` 라는 `DiscontinueAllProductsForSupplier(@SupplierID)`합니다.


[![새 DAL 메서드 DiscontinueAllProductsForSupplier 이름](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image37.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image36.png)

**그림 14**: 새 DAL 메서드 이름을 `DiscontinueAllProductsForSupplier` ([클릭 하 여 큰 이미지 보기](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image38.png))


사용 하 여 합니다 `DiscontinueAllProductsForSupplier(supplierID)` 데이터 액세스 계층에서 만든 메서드를 만들기는 다음 작업은는 `DiscontinueAllProductsForSupplier(supplierID)` 비즈니스 논리 계층에서 메서드. 이를 위해 열기를 `ProductsBLL` 클래스 파일 및 다음을 추가 합니다.

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample5.cs)]

으로 간단히이 메서드를 호출 합니다 `DiscontinueAllProductsForSupplier(supplierID)` 와 함께 제공 된 전달 DAL에서 메서드 *`supplierID`* 매개 변수 값입니다. 모든 비즈니스 규칙만 특정 상황에서 중단 되도록 공급 업체의 제품을 허용 하는 경우 해당 규칙 BLL에 여기에 구현 되어야 합니다.

> [!NOTE]
> 달리 합니다 `UpdateProduct` 에서 오버 로드는 `ProductsBLL` 클래스는 `DiscontinueAllProductsForSupplier(supplierID)` 메서드 시그니처에 포함 되지 않습니다는 `DataObjectMethodAttribute` 특성 (`<System.ComponentModel.DataObjectMethodAttribute(System.ComponentModel.DataObjectMethodType.Update, Boolean)>`). 이 `DiscontinueAllProductsForSupplier(supplierID)` 업데이트 탭에서 ObjectDataSource의 데이터 소스 구성 마법사의 드롭다운 목록에서 메서드. I ve 호출할 때문에이 특성을 생략 하면는 `DiscontinueAllProductsForSupplier(supplierID)` ASP.NET 페이지에 이벤트 처리기에서 직접 메서드.


## <a name="step-5-adding-a-discontinue-all-products-button-to-the-formview"></a>5 단계: 추가 된 모든 제품 단추 FormView 중단 합니다.

사용 하 여 합니다 `DiscontinueAllProductsForSupplier(supplierID)` FormView의 단추 웹 컨트롤을 추가 하는 BLL 및 DAL 완료에서 메서드를 선택한 공급자에 대 한 모든 제품을 중단 하는 기능을 추가 하기 위한 마지막 단계는 `ItemTemplate`합니다. 이러한 모든 제품을 중단 단추 텍스트를 사용 하 여 공급 업체의 전화 번호 아래 단추를 추가 해 보겠습니다 및 `ID` 속성 값의 `DiscontinueAllProductsForSupplier`합니다. FormView의 스마트 태그에서 템플릿 편집 링크를 클릭 하 여 디자이너를 통해이 단추 웹 컨트롤을 추가할 수 있습니다 (그림 15 참조) 또는 선언적 구문을 통해 직접.


[![추가 된 모든 제품 단추 웹 컨트롤 FormView의 ItemTemplate 중단 합니다.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image40.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image39.png)

**그림 15**: FormView의 중단 모든 제품 단추 웹 컨트롤을 추가할 `ItemTemplate` ([클릭 하 여 큰 이미지 보기](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image41.png))


사용자 방문 페이지에서 포스트백 근거가 및 FormView의 단추를 클릭할 때 [ `ItemCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.itemcommand.aspx) 발생 합니다. 클릭 되는이 단추에 대 한 응답에서 사용자 지정 코드를 실행 하려면이 이벤트에 대 한 이벤트 처리기를 만들 수 있습니다. 이해를 하는 합니다 `ItemCommand` 이벤트가 발생할 때마다 *모든* FormView 내 단추나 LinkButton, ImageButton 웹 컨트롤을 클릭 합니다. 즉, FormView, 다른 한 페이지에서 이동 하면는 `ItemCommand` 이벤트가 발생; 사용자가 새로 만들기, 편집 또는 삽입, 업데이트 또는 삭제를 지 원하는 FormView에서 삭제 하는 경우에 마찬가지입니다.

이후는 `ItemCommand` 이벤트 처리기에서는 필요한 모든 제품을 중단 단추를 클릭 한 경우를 결정 하는 방법 또는 단추인 경우 일부 다른 어떤 단추를 클릭 하는 것에 관계 없이 발생 합니다. 이렇게 하려면 단추 웹 컨트롤의 설정할 수 있습니다 `CommandName` 식별 값 속성입니다. 단추를 클릭할 때,이 `CommandName` 에 값이 전달 되는 `ItemCommand` 빠르므로 우리는 모든 제품을 중단 단추를 클릭 한 단추의 했는지 확인 하려면 이벤트 처리기입니다. 중단 모든 제품 단추의 설정 `CommandName` DiscontinueProducts 속성입니다.

마지막으로, 선택한 공급자의 제품을 중단 하는 사용자가 실제로 확인을 사용해 클라이언트 쪽 확인 대화 상자를 보겠습니다. 설명한 것 처럼 합니다 [삭제 하는 경우 클라이언트 쪽 확인 추가](../editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs.md) 자습서, javascript를 사용 하 여이 작업을 수행할 수 있습니다. 특히 단추 웹 컨트롤의 OnClientClick 속성을 설정 `return confirm('This will mark _all_ of this supplier\'s products as discontinued. Are you certain you want to do this?');`

다음과 같이 변경한 후 FormView의 선언적 구문을 다음과 같이 표시 됩니다.

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample6.aspx)]

다음으로, FormView의에 대 한 이벤트 처리기를 만들고 `ItemCommand` 이벤트입니다. 이 이벤트 처리기에서 먼저 모든 제품을 중단 단추가 클릭 되었는지 여부를 결정 해야 합니다. 따라서의 인스턴스를 생성 하려는 경우는 `ProductsBLL` 클래스 및 호출 해당 `DiscontinueAllProductsForSupplier(supplierID)` 전달 하는 메서드는 `SupplierID` 선택한 FormView의:

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample7.cs)]

합니다 `SupplierID` FormView에서 현재 선택한 공급자의 액세스할 수 있습니다는 FormView [ `SelectedValue` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.selectedvalue.aspx)합니다. `SelectedValue` 속성에서 첫 번째 데이터 키 FormView에 표시 되는 레코드에 대 한 값을 반환 합니다. FormView의 [ `DataKeyNames` 속성](https://msdn.microsoft.com/system.web.ui.webcontrols.formview.datakeynames.aspx), 자동으로 설정 된 필드를 데이터 키 값에서 가져온 데이터를 나타내는 `SupplierID` FormView ObjectDataSource에 바인딩할 때 Visual Studio에서 2 단계 년대.

사용 하 여는 `ItemCommand` 이벤트 처리기를 생성 하 고, 잠시 페이지를 테스트 합니다. Cooperativa de Quesos 이동할 ' 라스베이거스에서 Cabras' 공급자 (르네 FormView에서 다섯 번째 공급자 임). 이 공급자의 두 가지 제품이 Queso Cabrales 및 Queso Manchego La Pastora, 있으며 둘 모두를 제공 *되지* 중단 합니다.

Cooperativa de Quesos ' 라스베이거스에서 Cabras' 벗어난 비즈니스 제품 계획을 세워야 많으므로 한다고 가정 합니다. 클릭 된 모든 제품 단추를 중단 합니다. 클라이언트 쪽 확인 대화 상자를 표시 하는이 상자 (그림 16 참조).


[![Cooperativa de Quesos 라스베이거스에서 Cabras 제공 두 활성 제품](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image43.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image42.png)

**그림 16**: Cooperativa de Quesos 라스베이거스에서 Cabras 제공 두 활성 제품 ([큰 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image44.png))


클라이언트 쪽 확인 대화 상자에서 확인을 클릭 하면 양식 전송이 진행 됩니다는 포스트백을 발생 FormView의 `ItemCommand` 이벤트가 발생 합니다. 호출에서 만든 이벤트 처리기가 실행 한 다음는 `DiscontinueAllProductsForSupplier(supplierID)` 메서드와 Queso Cabrales와 Queso Manchego La Pastora 제품을 중단 합니다.

GridView의 뷰 상태를 해제 하면 GridView, 포스트백이 발생할 때마다 내부 데이터 저장소에 차츰 되는 및 따라서는 즉시 반영 하도록 업데이트는이 두 제품은 이제 사용 되지 않습니다 (그림 17 참조). 그러나 GridView에서 뷰 상태를 해제 하지 않은, 경우 이렇게 변경한 후 GridView에 데이터를 수동으로 바인딩할 해야 합니다. 이렇게 하려면 단순히 GridView의 호출을 수행 `DataBind()` 메서드 호출 바로 뒤의 `DiscontinueAllProductsForSupplier(supplierID)` 메서드.


[![모든 제품을 중단 단추를 클릭 한 후 공급자가의 제품에 업데이트 됩니다.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image46.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image45.png)

**그림 17**: 모든 제품을 중단 단추를 클릭 한 후 공급 업체의 제품에 따라 업데이트 됩니다 ([큰 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image47.png))


## <a name="step-6-creating-an-updateproduct-overload-in-the-business-logic-layer-for-adjusting-a-products-price"></a>6 단계: 제품의 가격을 조정 하기 위해 비즈니스 논리 계층에서 UpdateProduct 오버 로드 만들기

와 같은 모든 제품을 중단 단추 FormView에서 사용 하 여 GridView에서 제품 가격을 늘리고 단추를 추가 하기 위해 해야 먼저 적절 한 데이터 액세스 계층 및 비즈니스 논리 계층 메서드를 추가 합니다. DAL에 단일 제품 행을 업데이트 하는 메서드를 이미 있기 때문에 대 한 새 오버 로드를 만들어 이러한 기능을 제공할 수 있습니다 것은 `UpdateProduct` BLL에는 메서드.

이 이전 `UpdateProduct` 오버 로드 스칼라 입력된 값으로 product 필드 중 일부가 조합에서 수행 및 지정된 된 제품에 대 한 해당 필드로 업데이트 합니다. 이 오버 로드에 대 한 것이 표준 조금씩 하 고 제품의 대신 전달 `ProductID` 비율 조정에 사용 되는 `UnitPrice` (새 통과, 달리 조정 `UnitPrice` 자체). 이 방법은 현재 제품의 판단에 신경을 쓰지 않아도 되므로 ASP.NET 페이지 코드 숨김 클래스에 작성 해야 하는 코드를 간소화 됩니다 `UnitPrice`합니다.

`UpdateProduct` 이 자습서는 아래에 대 한 오버 로드 합니다.

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample8.cs)]

이 오버 로드를 DAL 통해 지정 된 제품에 대 한 정보를 검색 합니다. `GetProductByProductID(productID)` 메서드. 그런 다음 확인 여부를 제품의 `UnitPrice` 데이터베이스에 할당 된 `NULL` 값입니다. 가격은 그대로 인 경우 변경 되지 않은 합니다. 그러나 방법이 아닌 경우`NULL` `UnitPrice` 값, 메서드는 제품의 업데이트 `UnitPrice` 지정 된 % (`unitPriceAdjustmentPercent`).

## <a name="step-7-adding-the-increase-and-decrease-buttons-to-the-gridview"></a>GridView에 증가 및 감소 단추를 추가 하는 7 단계:

GridView와 DetailsView 모두 구성 된 필드의 컬렉션입니다. BoundFields, CheckBoxFields, 및 TemplateFields 외에도 ASP.NET 이름에서 알 수 있듯이 각 행에 대해 단추나 LinkButton, ImageButton 인 열으로 렌더링 하는 ButtonField를 포함 합니다. 클릭 하 여 FormView 비슷합니다 *모든* GridView 페이징 단추, 편집 또는 삭제 단추, 단추 정렬, 및 등 내에서 단추 포스트백을 발생 시키는 및 GridView의 시킵니다 [ `RowCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowcommand.aspx)합니다.

ButtonField에는 `CommandName` 각 해당 단추에 지정된 된 값을 할당 하는 속성 `CommandName` 속성입니다. FormView에서와 마찬가지로 합니다 `CommandName` 값에서 사용 됩니다는 `RowCommand` 클릭 된 단추를 결정 하는 이벤트 처리기입니다.

GridView에 단추 텍스트 가격 + 10 개에 두 개의 새 ButtonFields 추가해보겠습니다 % 및 텍스트 가격-10%입니다. 이러한 ButtonFields 추가할 GridView의 스마트 태그에서 열 편집 링크를 클릭, ButtonField 필드 형식을 왼쪽 위에 있는 목록에서 선택 하 고 추가 단추를 클릭 합니다.


![GridView에 두 ButtonFields 추가](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image48.png)

**그림 18**: 두 ButtonFields GridView에 추가


처음 두 GridView 필드로 나타나도록 두 ButtonFields를 이동 합니다. 다음으로 설정 합니다 `Text` 속성 + 10% 가격에 이러한 두 ButtonFields 및 가격-10% 및 `CommandName` IncreasePrice 고 DecreasePrice, 속성을 각각. 기본적으로 ButtonField Linkbutton으로 단추의 해당 열을 렌더링합니다. 이 변경할 수 있지만 ButtonField의를 통해 [ `ButtonType` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.buttonfieldbase.buttontype.aspx)합니다. 이러한 두 ButtonFields 일반 누름 단추; 렌더링 보겠습니다 따라서 설정 된 `ButtonType` 속성을 `Button`입니다. 그림 19 필드 대화 상자를 표시 한 후 이러한 변경 내용이; 그 다음은 GridView의 선언적 태그입니다.


![ButtonFields 텍스트, CommandName을 및 ButtonType 속성 구성](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image49.png)

**그림 19**: 구성 된 ButtonFields `Text`를 `CommandName`, 및 `ButtonType` 속성


[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample9.aspx)]

GridView의에 대 한 이벤트 처리기를 만드는 마지막 단계는 만든 이러한 ButtonFields를 사용 하 여 `RowCommand` 이벤트입니다. 때문에 발생 하는 경우이 이벤트 처리기는 가격 + 10% 또는 가격-10% 단추가 클릭 된를 확인 해야 합니다 `ProductID` 해당 단추를 클릭 한를 호출 하는 행에 대 한 합니다 `ProductsBLL` 클래스의 `UpdateProduct` 전달 적절 한 메서드를 `UnitPrice` 와 함께 비율 조정 된 `ProductID`합니다. 다음 코드는 이러한 작업을 수행합니다.

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample10.cs)]

확인 하기 위해 합니다 `ProductID` 행에 대 한 가격이 + 10% 또는 가격-10% 단추 클릭 했을 GridView의를 참조 해야 `DataKeys` 컬렉션입니다. 이 컬렉션에서 지정 된 필드의 값을 포함 합니다 `DataKeyNames` 각 GridView 행에 대 한 속성입니다. GridView의 이후 `DataKeyNames` 속성이 설정 된 ProductID를 Visual Studio에서 GridView의 ObjectDataSource 바인딩할 때 `DataKeys(rowIndex).Value` 를 제공 합니다 `ProductID` 지정 된 *rowIndex*합니다.

ButtonField에 자동으로 전달 합니다 *rowIndex* 를 통해 해당 단추를 클릭 한 행의는 `e.CommandArgument` 매개 변수입니다. 따라서 결정 하는 `ProductID` 행에 대 한 가격이 + 10% 또는 가격-10% 단추 클릭 했을 사용 하 여: `Convert.ToInt32(SuppliersProducts.DataKeys(Convert.ToInt32(e.CommandArgument)).Value)`합니다.

로 모든 제품을 중단 단추를 사용 하 여 GridView의 뷰 상태를 사용 하지 않도록 설정한 경우 GridView, 포스트백이 발생할 때마다 내부 데이터 저장소에 다시 바인딩되 되 고 따라서 즉시 업데이트 됩니다 클릭에서 발생 하는 가격 변경을 반영 하도록 단추 중 하나입니다. 그러나 GridView에서 뷰 상태를 해제 하지 않은, 경우 이렇게 변경한 후 GridView에 데이터를 수동으로 바인딩할 해야 합니다. 이렇게 하려면 단순히 GridView의 호출을 수행 `DataBind()` 메서드 호출 바로 뒤의 `UpdateProduct` 메서드.

그림 20 대양 농산에서 제공 하는 제품을 볼 때 페이지를 보여 줍니다. 그림 21에는 가격 + 10 후 % 단추를 클릭 했습니다 할머니의 블루베리 분산 및 가격-10% 단추 하기 위해 한 번 대양 특선 딸기 소스에 대 한 결과.


[![GridView 포함 가격 + 10% 및 가격-10% 단추](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image51.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image50.png)

**그림 20**: GridView 포함 가격 + 10% 및 가격-10% 단추 ([큰 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image52.png))


[![첫 번째 및 세 번째 제품에 대 한 가격은 가격 + 10 통해 업데이트 되었습니다. % 및 가격-10% 단추](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image54.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image53.png)

**그림 21**: 첫 번째 및 세 번째 제품 업데이트 된 가격 + 10 통해 The 가격은 % 및 가격-10% 단추 ([큰 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image55.png))


> [!NOTE]
> 단추, Linkbutton, 또는 해당 TemplateFields 추가할 ImageButtons를 GridView와 DetailsView 있을 수도 있습니다. BoundField를 사용 하 여이 단추를 클릭 하면 포스트백을 유도 됩니다을 하는 대로 발생 GridView의 `RowCommand` 이벤트입니다. 그러나 경우 추가 단추를 TemplateField 단추의 `CommandArgument` ButtonFields를 사용 하는 경우 이므로 행의 인덱스를 자동으로 설정 되지 됩니다. 내에서 클릭 된 단추의 행 인덱스를 확인 하는 경우는 `RowCommand` 단추를 수동으로 설정 해야 이벤트 처리기 `CommandArgument` 같은 코드를 사용 하 여를 TemplateField 내에서 해당 선언적 구문에서 속성:  
> `<asp:Button runat="server" ... CommandArgument='<%# ((GridViewRow) Container).RowIndex %>'`.


## <a name="summary"></a>요약

Linkbutton, 단추나 ImageButtons GridView, DetailsView 및 FormView 컨트롤을 모두 포함할 수 있습니다. 이러한 단추를 클릭 하면 포스트백을 발생 시키고 합니다 `ItemCommand` FormView 및 DetailsView 컨트롤에서 이벤트 및 `RowCommand` GridView에는 이벤트입니다. 이러한 데이터 웹 컨트롤에는 레코드를 편집 또는 삭제와 같은 일반적인 명령 관련 작업을 처리 하도록 기본 제공 기능이 있습니다. 또한 수 있지만 클릭 했을 때를 사용 하 여 단추, 응답 고유한 사용자 지정 코드를 실행 합니다.

이를 위해 이벤트 처리기를 생성 해야 합니다 `ItemCommand` 또는 `RowCommand` 이벤트입니다. 이 이벤트 처리기에서 먼저 확인 들어오는 `CommandName` 단추를 클릭 했는지 확인 한 다음 적절 한 사용자 지정 작업을 수행 하는 값입니다. 이 자습서를 사용 하 여 단추와 ButtonFields 지정 된 공급자에 대 한 모든 제품을 중단 늘리거나 특정 제품의 가격을 10% 감소 하는 방법에 살펴보았습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [다음](adding-and-responding-to-buttons-to-a-gridview-vb.md)
