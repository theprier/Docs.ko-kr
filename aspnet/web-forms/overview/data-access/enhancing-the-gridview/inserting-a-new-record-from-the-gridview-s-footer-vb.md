---
uid: web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-vb
title: "GridView의 바닥글 (VB)에서 새 레코드 삽입 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 포함 하 여 GridView를 추가 하는 방법을 GridView 컨트롤 데이터의 새 레코드를 삽입 하기 위한 기본 제공 지원을 제공 하지 않습니다는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/06/2007
ms.topic: article
ms.assetid: 528acc48-f20c-4b4e-aa16-4cc02f068ebb
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-vb
msc.type: authoredcontent
ms.openlocfilehash: 4d452e15ced52fd9dcac8201598146cb9ef38d7b
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="inserting-a-new-record-from-the-gridviews-footer-vb"></a>GridView의 바닥글 (VB)에서 새 레코드 삽입
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_53_VB.exe) 또는 [PDF 다운로드](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/datatutorial53vb1.pdf)

> GridView 컨트롤에서는 데이터의 새 레코드를 삽입 하기 위한 기본 제공 지원을 제공 하지이 자습서에는 삽입 인터페이스를 포함 하 여 GridView를 보강 하는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

에 설명 된 대로 [는 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 자습서, GridView, DetailsView, 및 FormView 웹 제어 각 기본 제공 데이터 수정 기능을 포함 합니다. 선언적 데이터 소스 제어를 사용할 때는 이러한 세 가지 웹 컨트롤 신속 하 고 쉽게 하도록 구성할 수 있습니다-데이터를 수정 및 코드를 전혀 작성 하지 않고도 시나리오에서 합니다. 그러나 DetailsView 및 FormView 컨트롤 기본 삽입, 편집 및 삭제 기능을 제공 합니다. GridView는 편집 및 삭제 지원만 제공 합니다. 그러나 약간 꺾은 그리스를 사용에서는 삽입 인터페이스를 포함 하도록 GridView을 강화할 수 있습니다.

GridView에 삽입 기능을 추가, 어떻게 새 레코드에 추가 됩니다 결정 삽입 인터페이스를 만들고 새 레코드를 삽입 하는 코드 작성 담당 하는 합니다. GridView의 바닥글에 삽입 하는 인터페이스를 추가 대해서는이 자습서에서 (그림 1 참조)을 행입니다. 각 열에 대 한 바닥글 셀 (s 제품 이름에 대 한 텍스트 상자, 공급자, 등에 대 한 DropDownList) 적절 한 데이터 수집 사용자 인터페이스 요소에 포함 됩니다. 또한 열이 필요 했습니다 추가 단추를 클릭 하면에 대 한 다시 게시 되며에 새 레코드를 삽입는 `Products` 바닥글 행에 제공 된 값을 사용 하 여 테이블입니다.


[![새 제품을 추가 하기 위한 인터페이스를 제공 하는 바닥글 행](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image1.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image1.png)

**그림 1**: 새 제품 추가 대 한 인터페이스를 제공 하는 바닥글 행 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image2.png))


## <a name="step-1-displaying-product-information-in-a-gridview"></a>1 단계:는 GridView에 제품 정보를 표시합니다.

GridView의 바닥글에 삽입 하는 인터페이스를 만드는 것부터 직접 관련이 म 하기 전에 s 첫 번째 포커스를 GridView 데이터베이스에 제품을 나열 하는 페이지에 추가 하는 방법에 있습니다. 열어 시작는 `InsertThroughFooter.aspx` 페이지에 `EnhancedGridView` 폴더 및 GridView s 설정 디자이너 도구 상자에서 끌어서는 GridView `ID` 속성을 `Products`합니다. 다음으로 GridView s 스마트 태그를 사용 하 여 명명 된 새 ObjectDataSource 바인딩할 `ProductsDataSource`합니다.


[![ProductsDataSource 라는 새 ObjectDataSource 만들기](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image2.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image3.png)

**그림 2**: 명명 된 새 ObjectDataSource 만드는 `ProductsDataSource` ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image4.png))


ObjectDataSource 사용 하도록 구성 된 `ProductsBLL` s 클래스 `GetProducts()` 제품 정보를 검색 하는 메서드입니다. 이 자습서에 대 한 s 중점을 엄격 하 게 삽입 기능을 추가 및 편집 및 삭제 걱정할 필요가 있습니다. 따라서 삽입 탭에서 드롭 다운 목록으로 설정 되어 있는지를 확인 `AddProduct()` 한 UPDATE 및 DELETE 탭에 있는 드롭 다운 목록을 (없음)으로 설정 됩니다.


[![ObjectDataSource s insert () 메서드를 map AddProduct 메서드](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image3.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image5.png)

**그림 3**: 지도 `AddProduct` 메서드 ObjectDataSource s `Insert()` 메서드 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image6.png))


[![(없음)으로 업데이트 및 삭제 탭 드롭 다운 목록을 설정 합니다.](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image4.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image7.png)

**그림 4**: (None)로 업데이트 및 삭제 탭 드롭 다운 목록 설정 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image8.png))


ObjectDataSource의 데이터 소스 구성 마법사를 완료 한 후 Visual Studio는 자동으로 필드를 추가할 GridView 각 해당 데이터 필드에 대 한. 이제 Visual Studio에 의해 추가 되는 필드의 모든를 둡니다. 다시 알아보고 제거 하겠습니다이 자습서의 뒷부분에 나오는 값을 가진 인할 필드 중 일부를 지정 해야 할 새 레코드를 추가 하는 경우.

데이터베이스에 80 제품 가까운가 있을 경우 사용자는 새 레코드를 추가 하려면 웹 페이지의 맨 아래까지 스크롤해야 할 됩니다. 따라서 사용 s 삽입 인터페이스 보다 잘 드러내고 액세스할 수 있도록 페이징을 활성화 수 있습니다. 페이징을 설정 하려면 단순히 GridView s 스마트 태그에서 페이징 사용 확인란을 확인 합니다.

이 시점에서 GridView 및 ObjectDataSource s 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample1.aspx)]


[![모든 제품 데이터 필드는 페이징 GridView에 표시](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image5.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image9.png)

**그림 5**: 페이징 GridView에 모든 제품 데이터 필드가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image10.png))


## <a name="step-2-adding-a-footer-row"></a>바닥글 행을 추가 하는 2 단계:

헤더와 데이터 행을 함께 GridView 바닥글 행을 포함합니다. 머리글 및 바닥글 행이 GridView s의 값에 따라 표시 되 [ `ShowHeader` ](https://msdn.microsoft.com/en-gb/library/system.web.ui.webcontrols.gridview.showheader.aspx) 및 [ `ShowFooter` ](https://msdn.microsoft.com/en-gb/library/system.web.ui.webcontrols.gridview.showfooter.aspx) 속성입니다. 바닥글 행을 표시 하려면 설정 하기만 `ShowFooter` 속성을 `True`합니다. 그림 6에서 알 수 있듯이, 설정 된 `ShowFooter` 속성을 `True` 바닥글 행을 표에 추가 합니다.


[![바닥글 행을 표시 하려면 ShowFooter을 True로 설정](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image6.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image11.png)

**그림 6**: 표시 하려면 바닥글 행 설정 `ShowFooter` 를 `True` ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image12.png))


바닥글 행 진한 빨간색 배경이 참고 합니다. 이것은 생성 하 고 모든 페이지에 적용 DataWebControls 테마 때문에 다시는 [the ObjectDataSource와 데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) 자습서입니다. 특히,는 `GridView.skin` 파일 구성는 `FooterStyle` 이러한 않는 속성이 사용 하 여는 `FooterStyle` CSS 클래스입니다. `FooterStyle` 클래스에 정의 된 `Styles.css` 다음과 같습니다.


[!code-css[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample2.css)]

> [!NOTE]
> 에서는 이전 자습서에서 GridView의 바닥글 행을 사용 하 여 탐색 했습니다. 필요한 경우 다시 참조는 [GridView의 바닥글에 요약 정보 표시](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md) 세부 정보에 대 한 자습서입니다.


설정한 후는 `ShowFooter` 속성을 `True`, 잠시 브라우저에서 출력을 볼 수 있습니다. 현재 바닥글 행 대상이 t 텍스트 또는 웹 컨트롤을 포함 합니다. 3 단계에서에서 적절 한 삽입 인터페이스 포함 되도록 각 GridView 필드에 대 한 바닥글을 수정 합니다.


[![빈 바닥글 행은 표시 위에 the 페이징 인터페이스 제어](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image7.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image13.png)

**그림 7**: 빈 바닥글 행이 표시 위에 the 페이징 인터페이스 컨트롤 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image14.png))


## <a name="step-3-customizing-the-footer-row"></a>3 단계: 바닥글 행을 사용자 지정

에 [GridView 컨트롤에 사용 하 여 TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) 크게 TemplateFields (BoundFields CheckBoxFields 반대)를 사용 하 여 특정 GridView 열의 표시를 사용자 지정 하는 방법에 살펴보았습니다 자습서, [ 데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) TemplateFields를 사용 하 여 편집 인터페이스는 GridView에 사용자 지정 하려면 살펴보았습니다. 회수를 TemplateField 태그, 웹 컨트롤 및 데이터 바인딩 구문을 함께 정의 하는 템플릿의 수 이루어져 있는지 사용 되는 특정 형식의 행. `ItemTemplate`, 예를 들어, 읽기 전용 행에 사용 되는 서식 파일을 지정 하는 동안는 `EditItemTemplate` 편집 가능한 행에 대 한 템플릿을 정의 합니다.

와 함께 `ItemTemplate` 및 `EditItemTemplate`는 TemplateField도 포함 되어는 `FooterTemplate` 바닥글 행에 대 한 콘텐츠를 지정 하는 합니다. 따라서 각 필드 s 삽입에 대 한 인터페이스에 필요한 웹 컨트롤을 추가할 수 우리는 `FooterTemplate`합니다. 를 시작 하려면 모든 GridView에서 필드를 TemplateFields를 변환 합니다. GridView s 스마트 태그를 하단 왼쪽된 모서리 쪽의 각 필드를 선택 하 고를 TemplateField 링크로 변환이이 필드를 클릭 하면 열 편집 링크를 클릭 하 수행할 수 있습니다.


![각 필드를 TemplateField로 변환](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image8.gif)

**그림 8**: 각 필드를 TemplateField로 변환


이 필드를 TemplateField로 변환을 클릭 하면 해당 TemplateField로 현재 필드 형식을 설정 합니다. 예를 들어 각 BoundField를 TemplateField로 바뀝니다는 `ItemTemplate` 해당 데이터 필드를 표시 하는 레이블을 포함 하는 및 `EditItemTemplate` 텍스트 상자에 데이터 필드를 표시 하는 합니다. `ProductName` BoundField TemplateField 태그를 다음으로 변환 되었습니다:


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample3.aspx)]

마찬가지로,는 `Discontinued` CheckBoxField 변환 된를 TemplateField로 갖는 `ItemTemplate` 및 `EditItemTemplate` CheckBox 웹 컨트롤이 포함 되어 (으로 `ItemTemplate` s 확인란 사용 하지 않도록 설정). 읽기 전용 `ProductID` BoundField 둘 다에서 레이블 컨트롤과 TemplateField로 변환 되어는 `ItemTemplate` 및 `EditItemTemplate`합니다. 즉, 변환 기존 GridView 필드를 TemplateField로는 기존 필드의 기능 손실 없이 지정할 TemplateField로 전환 하는 빠르고 쉬운 방법을 합니다.

GridView 이후 다시 대상이 t 지원 편집, 작업에서는 간편 하 게 제거는 `EditItemTemplate` 각 TemplateField에서 방금를 두면는 `ItemTemplate`합니다. 이 작업을 수행한 후 GridView s 선언 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample4.aspx)]

각 필드 s에 적절 한 삽입 인터페이스 입력할 수 있습니다 각 GridView 필드를 TemplateField로 변환 되어, 했으므로 `FooterTemplate`합니다. 일부 필드는 삽입 인터페이스를 제공 하지 것입니다 (`ProductID`예를 들어); 새 s 제품 정보를 수집 하는 데 사용 되는 웹 컨트롤에 다른 사용자가 달라 집니다.

편집 인터페이스를 만들려면 GridView s 스마트 태그에서 템플릿 편집 링크를 선택 합니다. 그런 다음 드롭다운 목록에서 적절 한 필드 s를 선택 `FooterTemplate` 디자이너 도구 상자에서 적절 한 컨트롤을 끕니다.


[![각 필드의 먼저에 적절 한 삽입 인터페이스 추가](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image9.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image15.png)

**그림 9**: 각 필드 s에 적절 한 삽입 인터페이스를 추가 `FooterTemplate` ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image16.png))


다음 목록에 추가 하려면 삽입 인터페이스를 지정 하는 GridView 필드 열거:

- `ProductID`없음입니다.
- `ProductName`TextBox를 추가 하 고 설정의 `ID` 를 `NewProductName`합니다. 사용자가 새 s 제품 이름에 대 한 값을 입력을 확인 하는 RequiredFieldValidator 컨트롤을 추가 합니다.
- `SupplierID`없음입니다.
- `CategoryID`없음입니다.
- `QuantityPerUnit`설정 된 TextBox를 추가 해당 `ID` 를 `NewQuantityPerUnit`합니다.
- `UnitPrice`라는 텍스트 상자 추가 `NewUnitPrice` 이 고 입력 한 값을 보장 하는 CompareValidator는 0 보다 크거나 통화 값입니다.
- `UnitsInStock`텍스트 상자를 사용 하 여 해당 `ID` 로 설정 된 `NewUnitsInStock`합니다. 입력 한 값이 0 보다 크거나 정수 값을 보장 하는 CompareValidator 포함 됩니다.
- `UnitsOnOrder`텍스트 상자를 사용 하 여 해당 `ID` 로 설정 된 `NewUnitsOnOrder`합니다. 입력 한 값이 0 보다 크거나 정수 값을 보장 하는 CompareValidator 포함 됩니다.
- `ReorderLevel`텍스트 상자를 사용 하 여 해당 `ID` 로 설정 된 `NewReorderLevel`합니다. 입력 한 값이 0 보다 크거나 정수 값을 보장 하는 CompareValidator 포함 됩니다.
- `Discontinued`확인란 설정을 추가 해당 `ID` 를 `NewDiscontinued`합니다.
- `CategoryName`DropDownList를 추가 하 고 설정의 `ID` 를 `NewCategoryID`합니다. 라는 새 ObjectDataSource 바인딩할 `CategoriesDataSource` 사용 하도록 구성 하 고는 `CategoriesBLL` s 클래스 `GetCategories()` 메서드. DropDownList s `ListItem` s 표시는 `CategoryName` 데이터 필드를 사용 하 여 `CategoryID` 데이터 필드를 해당 값으로 합니다.
- `SupplierName`DropDownList를 추가 하 고 설정의 `ID` 를 `NewSupplierID`합니다. 라는 새 ObjectDataSource 바인딩할 `SuppliersDataSource` 사용 하도록 구성 하 고는 `SuppliersBLL` s 클래스 `GetSuppliers()` 메서드. DropDownList s `ListItem` s 표시는 `CompanyName` 데이터 필드를 사용 하 여 `SupplierID` 데이터 필드를 해당 값으로 합니다.

각 유효성 검사 컨트롤에 대 한 지울는 `ForeColor` 속성 있도록는 `FooterStyle` CSS 클래스 s 흰색 전경 색을 빨간색 기본 대신 사용 됩니다. 또한 사용 하 여는 `ErrorMessage` 대 한 자세한 내용은 속성을 설정할 수 있지만 `Text` 별표로 속성입니다. 유효성 검사 컨트롤의 텍스트가 두 줄으로 줄 삽입 인터페이스 발생 하지 못하도록 하려면 설정는 `FooterStyle` s `Wrap` 속성 각각에 대해 false로는 `FooterTemplate` 유효성 검사 컨트롤을 사용 하는 합니다. 마지막으로, 집합과 GridView 아래 ValidationSummary 컨트롤을 추가 해당 `ShowMessageBox` 속성을 `True` 및 해당 `ShowSummary` 속성을 `False`합니다.

새 제품을 추가할 때 제공 해야는 `CategoryID` 및 `SupplierID`합니다. 에 대 한 바닥글 셀에서 dropdownlist 활용을 통해이 정보는 캡처는 `CategoryName` 및 `SupplierName` 필드입니다. 과 반대 이러한 필드를 사용 하기로 하는 경우는 `CategoryID` 및 `SupplierID` TemplateFields 표 s의에서 데이터 행 사용자 이므로 해당 ID 값 보다는 범주와 공급 업체 이름에 더 관심이 가능성이 높습니다. 이후는 `CategoryID` 및 `SupplierID` 값에 기록 되 고 이제 되는 `CategoryName` 및 `SupplierName` 필드 s 삽입 인터페이스를 제거할 수 있다는 것은 `CategoryID` 및 `SupplierID` TemplateFields GridView에서 합니다.

마찬가지로,는 `ProductID` 새 제품을 추가 하는 경우에 사용 되지 않습니다 하므로 `ProductID` TemplateField도 제거할 수 있습니다. 그러나 둡니다 s 수는 `ProductID` 표에서 필드입니다. 텍스트 상자, dropdownlist 활용, 확인란, 및 삽입 인터페이스를 구성 하는 유효성 검사 컨트롤 외에 사용 해야 추가 단추를 클릭 하면 데이터베이스에 새 제품을 추가 하려면 논리를 수행 합니다. 4 단계에서에서의 삽입 인터페이스에는 추가 단추가 포함 됩니다는 `ProductID` TemplateField의 `FooterTemplate`합니다.

GridView의 다양 한 필드의 모양이 개선 자유롭게 합니다. 서식을 지정할 수 예를 들어는 `UnitPrice` 통화로, 값 오른쪽에 맞추려면는 `UnitsInStock`, `UnitsOnOrder`, 및 `ReorderLevel` 필드 및 업데이트는 `HeaderText` 는 TemplateFields에 대 한 값입니다.

인터페이스 삽입 회전을 만든 후의 `FooterTemplate` s, 제거는 `SupplierID`, 및 `CategoryID` TemplateFields, 서식 및 선언적 GridView s 프로그램 TemplateFields 맞춤 방식을 통해 눈금의 시각적 효과 향상 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample5.aspx)]

브라우저를 통해 보면 GridView의 바닥글 행 이제 포함 됩니다는 전체 (그림 10 참조) 인터페이스를 삽입 합니다. 이 시점에서 삽입 인터페이스 대상이 t 그녀는 s 새 제품에 대 한 데이터를 입력 하 고 데이터베이스에 새 레코드를 삽입 하려는 나타내기 위해 사용자에 대 한 의미를 포함 합니다. 에서는 또한 했습니다 아직에서 새 레코드에 바닥글에 입력 된 데이터는 변환 하는 방법을 주소를 지정 하는 `Products` 데이터베이스입니다. 코드를 실행 하는 방법과 추가 단추는 삽입 인터페이스를 포함 하는 방법을 살펴보겠습니다 4 단계에서에서 다시 게시 될 때 그 s 클릭 합니다. 5 단계 바닥글에서 데이터를 사용 하 여 새 레코드를 삽입 하는 방법을 보여 줍니다.


[![새 레코드를 추가 하기 위한 인터페이스를 제공 하는 GridView 바닥글](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image10.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image17.png)

**그림 10**: 새 레코드를 추가 하기 위한 인터페이스를 제공 하는 GridView 바닥글 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image18.png))


## <a name="step-4-including-an-add-button-in-the-inserting-interface"></a>4 단계: 추가 단추를 포함 하 여 삽입 인터페이스

바닥글 행의 인터페이스를 현재 삽입 된 새 s 제품 정보를 입력 완료 했음을 표시 하기 위해 사용자를 위한 없으므로 삽입 인터페이스에는 추가 단추가 어딘가에 포함 해야 합니다. 기존 중 하나에 배치할 수 있습니다 `FooterTemplate` s 또는 여기서 추가할 수는 새 열 표에이 목적을 위해 합니다. 이 자습서에 대 한 s let 배치에서 추가 단추는 `ProductID` TemplateField의 `FooterTemplate`합니다.

디자이너에서 GridView s 스마트 태그에서 템플릿 편집 링크 클릭 한 다음 선택에서 `ProductID` 필드의 `FooterTemplate` 드롭 다운 목록에서 합니다. Button 웹 컨트롤 (또는 LinkButton 또는 ImageButton을 원하는 경우)을 추가 해당 ID를 설정 하 고 서식 파일을 `AddProduct`, 해당 `CommandName` 삽입을 및 해당 `Text` 속성을 그림 11에 표시 된 대로 추가 합니다.


[![ProductID TemplateField의 먼저에서 추가 단추를 배치 합니다.](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image11.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image19.png)

**그림 11**:에서 추가 단추는 `ProductID` TemplateField s `FooterTemplate` ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image20.png))


적 추가 단추를 포함 되 면 브라우저에서 페이지를 테스트 합니다. 삽입 인터페이스에 잘못 된 데이터가 있는 추가 단추를 클릭 하면 포스트백 circuited 간단히 말해은 및 ValidationSummary 컨트롤 (그림 12 참조) 잘못 된 데이터를 나타냅니다. 입력 한 적절 한 데이터와 함께 추가 단추를 클릭 하면 다시 게시 합니다. 그러나 데이터베이스에 레코드가 추가 됩니다. 약간의 실제로 삽입을 수행 하는 코드를 작성 해야 합니다.


[![단추 추가 s 포스트백이 짧은 Circuited 삽입 인터페이스에 잘못 된 데이터가 있는 경우](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image12.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image21.png)

**그림 12**: 단추 추가 s 포스트백 짧은 Circuited 삽입 인터페이스에 잘못 된 데이터가 있는 경우는 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image22.png))


> [!NOTE]
> 삽입 인터페이스에서 유효성 검사 컨트롤 유효성 검사 그룹에 할당 되지 않았습니다. 이 기능이 제대로 작동으로 삽입 인터페이스는 유일한 집합 유효성 검사 페이지에 있는 컨트롤입니다. 하지만 삽입 유효성 검사 컨트롤 인터페이스를 단추 s 추가 (예: 표 s 편집 인터페이스에서 유효성 검사 컨트롤) 페이지에 있는 다른 유효성 검사 컨트롤 인 경우 `ValidationGroup` 속성에 동일한 값을 할당 해야로 so 특정 유효성 검사 그룹으로 이러한 컨트롤을 연결 합니다. 참조 [ASP.NET 2.0에서 유효성 검사 컨트롤 나누어서](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx) 유효성 검사 그룹으로 분할 유효성 검사 컨트롤 및 단추 페이지에 대 한 자세한 내용은 합니다.


## <a name="step-5-inserting-a-new-record-into-theproductstable"></a>5 단계:에 새 레코드 삽입는`Products`테이블

GridView의 기본 제공 편집 기능을 사용할 때는 GridView 자동으로 처리는 업데이트를 실행 하는 데 필요한 작업을 모두 합니다. 특히, [업데이트] 단추를 클릭할 때 복사 ObjectDataSource s에서 매개 변수를 편집 인터페이스에서 입력 값 `UpdateParameters` 컬렉션과 ObjectDataSource s 호출 하 여 업데이트 해제 작동 `Update()` 메서드. ObjectDataSource s 호출 하는 코드를 구현 해야 GridView 삽입 하는 데 이러한 기본 제공 기능을 제공 하지 않는 이후 `Insert()` 메서드와 ObjectDataSource s 인터페이스는 삽입에서 값 복사 `InsertParameters` 컬렉션 .

추가 단추를 클릭 한 후이 insert 논리를 실행 합니다. 에 설명 된 대로 [추가 하 고 응답 하는 GridView의 단추](../custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb.md) 자습서에서는 단추나 LinkButton을 GridView에서 ImageButton을 클릭 하면 GridView s 언제 든 지 `RowCommand` 다시 게시 될 때 이벤트 발생 합니다. 이 이벤트는 단추, LinkButton을 또는 ImageButton 바닥글 행에 추가 단추와 같은 명시적으로 추가 되었는지 여부 또는 GridView에서 자동으로 추가 된 경우 (정렬 사용을 선택 하면 각 열 맨 위에 있는 링크 단추가 같은 또는 링크 단추가 페이징 사용을 선택한 경우 페이징 인터페이스에서).

따라서 하려면 추가 단추를 클릭 하면 사용자에 게 응답 해야 GridView s에 대 한 이벤트 처리기를 만들고 `RowCommand` 이벤트입니다. 이 이벤트가 발생할 때마다 이후 *모든* 단추나 LinkButton을 GridView에서 ImageButton을 클릭 하면 그 s는만 계속 진행 논리를 삽입 하는 경우 중요 한는 `CommandName` 는 에이벤트처리기맵에전달된속성`CommandName` 추가 단추 (Insert)의 값입니다. 또한 유효한 데이터를 보고 하는 유효성 검사 컨트롤 경우만 제공 됩니다 진행 해야 했습니다. 에 대 한 이벤트 처리기를 만들고이 위해는 `RowCommand` 다음 코드를 사용 하 여 이벤트:


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample6.vb)]

> [!NOTE]
> 이벤트 처리기 고민 검사 하는 이유 할까요는 `Page.IsValid` 속성입니다. 즉, 잘못 된 데이터 삽입 인터페이스에 제공 하는 경우 성공한 t 포스트백 억제? 이 가정을 사용자 JavaScript 비활성화 되지 않은 또는 클라이언트 쪽 유효성 검사 논리를 방지 하기 위해 조치를 취하지 올바릅니다. 즉, 하나에 의존 하지 않아야 엄격 하 게 클라이언트 쪽 유효성 검사. 서버 쪽 유효성 검사 데이터 작업을 하기 전에 항상 수행 되어야 합니다.


1 단계에서에서 만든는 `ProductsDataSource` ObjectDataSource 되도록 해당 `Insert()` 메서드가 매핑되는 `ProductsBLL` s 클래스 `AddProduct` 메서드. 에 새 레코드를 삽입 하는 `Products` 테이블 ObjectDataSource s 호출 하면 됩니다 수 `Insert()` 메서드:


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample7.vb)]

이제는 `Insert()` 메서드 호출, 매개 변수를 삽입 하는 인터페이스에서 값을 복사을 모두으로 전달 되는 `ProductsBLL` s 클래스 `AddProduct` 메서드. 다시에서 설명한 것 처럼는 [삽입, 업데이트 및 삭제와 관련 된 이벤트를 검사 하](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) 자습서, ObjectDataSource s 통해 이렇게 `Inserting` 이벤트입니다. 에 `Inserting` 컨트롤을 프로그래밍 방식으로 참조 해야 하는 이벤트는 `Products` GridView의 바닥글 행 및 해당 값에 할당할는 `e.InputParameters` 컬렉션입니다. 종료 등의 값을 생략 한 경우는 `ReorderLevel` 부터 데이터베이스에 삽입 된 값이 되도록 지정 해야 하는 텍스트 상자에 붙여넣습니다 blank `NULL`합니다. 이후는 `AddProducts` 메서드 수용 nullable 형식은 nullable 데이터베이스 필드에 대해 단순히 nullable 형식을 사용 하 고, 해당 값을 설정 `Nothing` 사용자 입력을 생략 하는 경우에서.


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample8.vb)]

와 `Inserting` 완료 하는 이벤트 처리기에서 새 레코드에 추가할 수 있습니다는 `Products` GridView의 바닥글 행을 통해 데이터베이스 테이블입니다. 계속 해 년도 추가 해 보십시오.

## <a name="enhancing-and-customizing-the-add-operation"></a>사용자 지정 하 고는 추가 작업

현재 추가 단추를 클릭 하는 데이터베이스 테이블에 새 레코드를 추가 하지만에서는 모든 종류의 시각적 피드백 레코드를 추가 했습니다. 이상적으로 Label 웹 컨트롤이 나 클라이언트 쪽 경고 상자 자신의 삽입 성공적으로 완료 된 사용자에 게 알리는 것입니다. I이 그대로 실행으로 판독기에 대 한 합니다.

이 자습서에 사용 된 GridView 나열 된 제품에 정렬 순서가 적용 되지 않습니다 하거나 최종 사용자 데이터를 정렬 될 수 없습니다. 따라서 레코드는 데이터베이스 필드를 기준으로 기본 키에 있는 것 처럼 정렬 됩니다. 각 새 레코드에 있으므로 `ProductID` 마지막 식는 눈금의 끝에 얻으려면는 새 제품 추가 될 때마다 보다 큰 값입니다. 따라서 다음 GridView의 마지막 페이지를 새 레코드를 추가한 후 사용자를 자동으로 전송 하는 것이 좋습니다. 호출 후 다음 코드 줄을 추가 하 여이 작업을 수행할 수 있습니다 `ProductsDataSource.Insert()` 에 `RowCommand` 사용자를 보낼 수 마지막 페이지 GridView에 데이터를 바인딩한 후 해야 함을 나타내기 위해 이벤트 처리기.


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample9.vb)]

`SendUserToLastPage`페이지 수준 부울 변수는 초기 값이 할당은 `False`합니다. GridView s에서 `DataBound` 이벤트 처리기 인 경우 `SendUserToLastPage` 이 false 이면는 `PageIndex` 속성은 마지막 페이지에 연결 하도록 업데이트 합니다.


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample10.vb)]

이유는 `PageIndex` 에서 속성을 설정할는 `DataBound` 이벤트 처리기 (반대인는 `RowCommand` 이벤트 처리기) ¿¡´ 때는 `RowCommand` 이벤트 처리기에 새 레코드를 추가 하는 아직 했습니다 म 발생는 `Products` 데이터베이스 테이블입니다. 따라서는 `RowCommand` 이벤트 처리기 마지막 페이지 인덱스 (`PageCount - 1`) 마지막 페이지 인덱스를 나타내는 *전에* 신제품 추가 되었습니다. 추가 되는 제품의 대부분에 대 한 마지막 페이지 인덱스는 새 제품을 추가한 후 때 추가 된 제품 결과 새 마지막 페이지 인덱스의 경우 올바르게 업데이트 되지 않지만 `PageIndex` 에 `RowCommand` 새 마지막 페이지 i와 반대 이벤트 처리기 그런 다음 마지막 페이지 (새 제품을 추가 하기 전에 마지막 페이지 인덱스)에서 두 번째 작업으로 이동 합니다 ndex 합니다. 이후는 `DataBound` 신제품 개가 추가 되 고 데이터를 설정 하 여 눈금에 리바운드 후에 이벤트 처리기 실행는 `PageIndex` 속성 있습니다 알 म 올바른 마지막 페이지 인덱스를 가져오는 다시 합니다.

마지막으로,이 자습서에 사용 된 GridView는 새 제품을 추가 하는 데를 수집 해야 하는 필드 수에 따라 매우 다양 합니다. 이 너비 인해 DetailsView s 세로 레이아웃 기본 수 있습니다. GridView s 더 적은 수의 입력을 수집 하 여 전체 너비를 줄일 수 없습니다. T를 수집할 필요가 않는 우리는 아마도 `UnitsOnOrder`, `UnitsInStock`, 및 `ReorderLevel` 새 제품을 추가 하는 경우 필드 GridView에서 이러한 필드를 제거할 수는 경우.

수집 된 데이터를 조정 하려면 두 가지 방법 중 하나를 사용할 수 있습니다.

- 계속 사용 하는 `AddProduct` 에 대 한 값을 가지는 메서드는 `UnitsOnOrder`, `UnitsInStock`, 및 `ReorderLevel` 필드입니다. 에 `Inserting` 이벤트 처리기를 하드 코드 된 제공, 기본값을 삽입 하는 인터페이스에서 제거 된 이러한 입력으로 사용 합니다.
- 새 오버 로드를 만들기는 `AddProduct` 에서 메서드는 `ProductsBLL` 클래스에 대 한 입력을 허용 하지 않는 `UnitsOnOrder`, `UnitsInStock`, 및 `ReorderLevel` 필드입니다. 그런 다음 ASP.NET 페이지에서이 새 오버 로드를 사용 하도록 ObjectDataSource를 구성 합니다.

두 옵션 모두도 동일 하 게 작동 합니다. 이전 자습서에서는 사용 후자 옵션에 대 한 여러 개의 오버 로드를 만들기는 `ProductsBLL` s 클래스 `UpdateProduct` 메서드.

## <a name="summary"></a>요약

GridView에 DetailsView 및 FormView, 기본 제공 삽입 기능 부족 하지만 약간의 노력 삽입 인터페이스 바닥글 행에 추가할 수 있습니다. 단순히는 GridView에 바닥글 행을 표시 하려면 해당 `ShowFooter` 속성을 `True`합니다. 바닥글 행 내용을 사용자 지정할 수 있습니다 각 필드에 대 한 필드를 TemplateField 변환 하 여 및에 인터페이스는 삽입 추가 `FooterTemplate`합니다. 이 자습서에서 살펴본 것 처럼는 `FooterTemplate` 단추, 텍스트 상자, dropdownlist 활용, 확인란, 데이터 기반 웹 컨트롤 (예: dropdownlist 활용)를 채우기 위한 데이터 소스 제어 및 유효성 검사 컨트롤 포함 될 수 있습니다. S 사용자 입력을 수집 하기 위한 컨트롤과 함께 추가 단추, LinkButton을 또는 ImageButton 필요 합니다.

추가 단추를 클릭할 때, ObjectDataSource의 `Insert()` 메서드를 호출 하는 삽입 워크플로 시작 합니다. ObjectDataSource는 다음 구성 된 insert 메서드를 호출 합니다 (의 `ProductsBLL` s 클래스 `AddProduct` 이 자습서에서는 메서드). GridView의 ObjectDataSource s에 대 한 인터페이스를 삽입에서 값을 복사 해야 우리 `InsertParameters` 호출 되는 insert 메서드가 이전 컬렉션입니다. ObjectDataSource s에서 삽입 인터페이스 웹 컨트롤을 프로그래밍 방식으로 참조 하 여이 작업을 수행할 수 수 `Inserting` 이벤트 처리기입니다.

이 자습서는 GridView의 모양을 향상에 대 한 기술 참조를 완료 합니다. 자습서의 다음 집합 이미지, Pdf, Word 문서와 같은 이진 데이터와 함께 작동 하는 방법과 웹 컨트롤 데이터를 검사 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 박 광 준 Leigh 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](adding-a-gridview-column-of-checkboxes-vb.md)
