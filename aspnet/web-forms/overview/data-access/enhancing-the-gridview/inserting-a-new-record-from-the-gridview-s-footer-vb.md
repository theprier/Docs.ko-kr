---
uid: web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-vb
title: GridView의 바닥글 (VB)에서 새 레코드 삽입 | Microsoft Docs
author: rick-anderson
description: 이 자습서에 포함 하도록 GridView를 보강 하는 방법을 보여 줍니다 GridView 컨트롤 데이터의 새 레코드를 삽입 하기 위한 기본 제공 지원을 제공 하지 않지만는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/06/2007
ms.topic: article
ms.assetid: 528acc48-f20c-4b4e-aa16-4cc02f068ebb
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-vb
msc.type: authoredcontent
ms.openlocfilehash: c228128e551f58aa003af10cf787875d26b1fab7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37375181"
---
<a name="inserting-a-new-record-from-the-gridviews-footer-vb"></a>GridView의 바닥글 (VB)에서 새 레코드 삽입
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_53_VB.exe) 또는 [PDF 다운로드](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/datatutorial53vb1.pdf)

> GridView 컨트롤 데이터의 새 레코드를 삽입 하기 위한 기본 제공 지원을 제공 하지 않지만,이 자습서에는 삽입 인터페이스를 포함 하는 GridView를 보강 하는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

에 설명 된 대로 합니다 [An 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 자습서, 기본 제공 데이터 수정 기능을 포함 하는 GridView, DetailsView 및 FormView 웹 컨트롤입니다. 선언적 데이터 소스 컨트롤을 사용 하는 경우 이러한 세 웹 컨트롤 구성할 수 있습니다 쉽고 빠르게 데이터를 수정 하 고 코드 한 줄도 작성 하지 않고도 시나리오에서. 아쉽게도 FormView 및 DetailsView 컨트롤 기본 삽입, 편집 및 삭제 기능을 제공 합니다. GridView는 편집 및 삭제 지원만 제공 합니다. 그러나 약간 엘보우 그리스 사용에서는 삽입 인터페이스를 포함 하도록 GridView 강화할 수 있습니다.

GridView에 삽입 기능을 추가,는에서는 새로운 레코드에 추가 됩니다 결정 삽입 인터페이스를 만들고 새 레코드를 삽입 하는 코드를 작성 하는 일을 담당 합니다. 이 자습서를 GridView가의 바닥글 삽입 인터페이스에 추가 살펴보도록 하겠습니다 (그림 1 참조)을 행 합니다. 각 열에 대 한 바닥글 셀 (s 제품 이름에 대 한 텍스트 상자, 공급 업체, 등에 대 한 DropDownList) 적절 한 데이터 컬렉션 사용자 인터페이스 요소를 포함합니다. 또한 열이 필요 했습니다 추가 단추를 클릭할 때에 대 한 포스트백을 발생 되며에 새 레코드를 삽입 합니다 `Products` 바닥글 행에 제공 된 값을 사용 하 여 테이블입니다.


[![새 제품을 추가 하기 위한 인터페이스를 제공 하는 바닥글 행](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image1.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image1.png)

**그림 1**: 새 제품 추가 대 한 인터페이스를 제공 하는 바닥글 행 ([큰 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image2.png))


## <a name="step-1-displaying-product-information-in-a-gridview"></a>GridView의 제품 정보를 표시 하는 1 단계:

우리가 하는 데 문제가 직접 GridView가의 바닥글에 삽입 인터페이스를 만드는 방법, 전에 데이터베이스에서 제품을 나열 하는 페이지에 GridView를 추가 하는 방법에 첫 번째 포커스를 s 수 있습니다. 열어서 시작 합니다 `InsertThroughFooter.aspx` 페이지에서 `EnhancedGridView` 폴더 및 GridView s 설정 디자이너 도구 상자에서 끌어서 GridView `ID` 속성을 `Products`합니다. 그런 다음 GridView가 스마트 태그를 사용 하 여 명명 된 새 ObjectDataSource를 바인딩할 `ProductsDataSource`합니다.


[![ProductsDataSource 라는 새로운 ObjectDataSource는 만들기](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image2.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image3.png)

**그림 2**: 명명 된 새 ObjectDataSource 만들려면 `ProductsDataSource` ([클릭 하 여 큰 이미지 보기](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image4.png))


ObjectDataSource를 사용 하 여 구성 합니다 `ProductsBLL` s 클래스 `GetProducts()` 제품 정보를 검색할 메서드입니다. 이 자습서에서는 편집 및 삭제 걱정 하지 않고 s 집중 엄격 하 게 삽입 기능을 추가 하도록 합니다. 따라서 삽입 탭에서 드롭 다운 목록 설정 되어 있는지를 확인 `AddProduct()` 있고 UPDATE 및 DELETE 탭의 드롭다운 목록 (없음)으로 설정 됩니다.


[![지도 ObjectDataSource가 insert () 메서드에 AddProduct 메서드](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image3.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image5.png)

**그림 3**: 맵 합니다 `AddProduct` ObjectDataSource의 방법 `Insert()` 메서드 ([클릭 하 여 큰 이미지 보기](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image6.png))


[![(없음)으로 업데이트 및 삭제 탭 드롭다운 목록 설정](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image4.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image7.png)

**그림 4**: (none) 업데이트 및 삭제 탭 드롭 다운 목록 설정 ([큰 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image8.png))


ObjectDataSource가의 데이터 소스 구성 마법사를 완료 한 후 Visual Studio는 자동으로 필드를 추가할 GridView 각 해당 데이터 필드에 대 한. 이제 모든 Visual Studio에서 추가 필드를 둡니다. 다시 방문 하 고 제거 드리겠습니다이 자습서의 뒷부분에서 새 레코드를 추가 하는 경우 지정 해야 일부 필드 값이 포함 하지 않습니다.

80 제품 가까이에서 있으므로 데이터베이스에 새 레코드를 추가 하기 위해 웹 페이지의 맨 끝으로 아래로 스크롤하여 사용자 해야 합니다. 따라서 s를 삽입 인터페이스 보다 투명 하 고 액세스할 수 있도록 페이징 사용을 수 있습니다. 페이징을 설정 하려면 단순히 GridView가 스마트 태그에서 페이징을 사용 확인란을 확인 합니다.

이 시점에서 GridView 및 ObjectDataSource가 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample1.aspx)]


[![페이징 GridView에서 제품 데이터 필드를 모두 표시](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image5.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image9.png)

**그림 5**: 페이징 GridView의 모든 제품 데이터 필드가 표시 됩니다 ([큰 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image10.png))


## <a name="step-2-adding-a-footer-row"></a>바닥글 행을 추가 하는 2 단계:

헤더와 데이터 행을 함께 GridView 바닥글 행이 포함 됩니다. 머리글 및 바닥글 행 GridView s의 값에 따라 표시 됩니다 [ `ShowHeader` ](https://msdn.microsoft.com/en-gb/library/system.web.ui.webcontrols.gridview.showheader.aspx) 하 고 [ `ShowFooter` ](https://msdn.microsoft.com/en-gb/library/system.web.ui.webcontrols.gridview.showfooter.aspx) 속성입니다. 바닥글 행을 표시 하려면 설정 하기만 합니다 `ShowFooter` 속성을 `True`입니다. 그림 6에서 알 수 있듯이, 설정 된 `ShowFooter` 속성을 `True` 바닥글 행을 표에 추가 합니다.


[![바닥글 행을 표시 하려면 ShowFooter을 True로 설정](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image6.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image11.png)

**그림 6**: 표시 하려면 바닥글 행 집합 `ShowFooter` 하 `True` ([클릭 하 여 큰 이미지 보기](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image12.png))


바닥글 행을 진한 빨간색 배경이 참고 합니다. DataWebControls 테마를 만들고 모든 페이지에 적용할 것 때문에 다시를 [the ObjectDataSource 사용 하 여 데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) 자습서입니다. 특히를 `GridView.skin` 파일은 구성의 `FooterStyle` 속성 이러한 사용를 `FooterStyle` CSS 클래스입니다. 합니다 `FooterStyle` 클래스에 정의 된 `Styles.css` 다음과 같습니다.


[!code-css[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample2.css)]

> [!NOTE]
> 에서는 ve GridView가의 바닥글 행을 사용 하 여 이전 자습서에서 탐색 합니다. 필요한 경우 다시 참조를 [GridView의 바닥글에 요약 정보 표시](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md) 세부 정보에 대 한 자습서입니다.


설정한 후 합니다 `ShowFooter` 속성을 `True`, 잠시 브라우저에서 출력을 확인 합니다. 현재 바닥글 행 만들어지고 t 텍스트 또는 웹 컨트롤을 포함 합니다. 3 단계에서에서 적절 한 삽입 인터페이스를 포함 하도록 각 GridView 필드에 대 한 바닥글을 수정 합니다.


[![빈 바닥글 행이 표시 위에 페이징 인터페이스 컨트롤](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image7.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image13.png)

**그림 7**: The 빈 바닥글 행이 표시 위에 페이징 인터페이스 컨트롤 ([큰 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image14.png))


## <a name="step-3-customizing-the-footer-row"></a>3 단계: 바닥글 행을 사용자 지정

다시 합니다 [GridView 컨트롤에서 TemplateFields 사용 하 여](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) 크게 TemplateFields (BoundFields CheckBoxFields 아님)를 사용 하 여 특정 GridView 열 표시를 사용자 지정 하는 방법에 살펴보았습니다 자습서, [ 데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) GridView의 편집 인터페이스를 사용자 지정할 TemplateFields 사용에 대해 살펴보았습니다. 회수를 TemplateField 태그, 웹 컨트롤 및 데이터 바인딩 구문을 조합을 정의 하는 템플릿의 숫자로 이루어집니다는 특정 행의 유형에 사용 합니다. 합니다 `ItemTemplate`, 예를 들어, 읽기 전용 행에 사용 된 템플릿을 지정 하는 동안는 `EditItemTemplate` 편집할 수 있는 행의 템플릿을 정의 합니다.

와 함께 `ItemTemplate` 하 고 `EditItemTemplate`를 templatefield로 포함 되어 있습니다를 `FooterTemplate` 바닥글 행에 대 한 콘텐츠를 지정 하는 합니다. 웹 컨트롤에 인터페이스를 삽입 하는 각 필드 s에 대 한 필요한 추가할 수 있습니다 따라서는 `FooterTemplate`합니다. 를 시작 하려면 모든 GridView에서 필드를 TemplateFields 변환할 놓습니다. GridView가 스마트 태그에서 왼쪽된 아래 모퉁이에서 각 필드를 선택 하 고 TemplateField 링크로 변환이이 필드를 클릭 하면 열 편집 링크를 클릭 하 수행할 수 있습니다.


![각 필드를 TemplateField로 변환](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image8.gif)

**그림 8**: 각 필드를 TemplateField로 변환


이 필드를 TemplateField로의 변환을 클릭 하는 해당 TemplateField로 현재 필드 형식이 설정 합니다. 예를 들어, 각 BoundField 바뀝니다 templatefield로 사용 하 여는 `ItemTemplate` 해당 데이터 필드를 표시 하는 레이블을 포함 하는 및 `EditItemTemplate` 텍스트 상자에 데이터 필드를 표시 하는 합니다. `ProductName` BoundField TemplateField 태그를 다음으로 변환 되었습니다.


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample3.aspx)]

마찬가지로 합니다 `Discontinued` CheckBoxField 변환 된 templatefield로 갖는 `ItemTemplate` 및 `EditItemTemplate` CheckBox 웹 컨트롤이 포함 되어 (사용 하 여는 `ItemTemplate` s 사용 하지 않도록 설정 하는 확인란을 선택). 읽기 전용 `ProductID` BoundField 둘 다에서 레이블 컨트롤을 사용 하 여 templatefield로 변환 된 합니다 `ItemTemplate` 및 `EditItemTemplate`합니다. 즉, 기존 GridView는 변환 필드를 TemplateField로 방법이 쉽고 빠르게 기존 필드 s 기능 손실 없이 더 사용자 지정 가능한 TemplateField로 전환 합니다.

GridView 이후 다시 만들어지고 t 지원 편집, 작업에서는 자유롭게 제거할 합니다 `EditItemTemplate` 각 TemplateField에서 벗어나지 방금는 `ItemTemplate`합니다. 이 작업을 수행한 후 GridView가 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample4.aspx)]

각 필드 s에 적절 한 삽입 인터페이스 입력할 수 있습니다 각 GridView 필드를 TemplateField로 변환 했으므로 `FooterTemplate`합니다. 일부 필드는 삽입 인터페이스 없습니다 (`ProductID`예를 들어); 다른 새 s 제품 정보를 수집 하는 데 웹 컨트롤에 달라 집니다.

편집 인터페이스를 만들려면 GridView가 스마트 태그에서 템플릿 편집 링크를 선택 합니다. 드롭다운 목록에서 적절 한 s 필드를 선택한 `FooterTemplate` 디자이너 도구 상자에서 적절 한 컨트롤을 끕니다.


[![각 필드의 먼저에 적절 한 삽입 인터페이스 추가](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image9.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image15.png)

**그림 9**: 각 필드에 적절 한 삽입 인터페이스를 추가 `FooterTemplate` ([클릭 하 여 큰 이미지 보기](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image16.png))


다음 글머리 기호 목록에 추가 하려면 삽입 인터페이스를 지정 하는 GridView 필드 열거:

- `ProductID` None입니다.
- `ProductName` TextBox를 추가 하 고 설정 해당 `ID` 에 `NewProductName`입니다. 사용자가 새 s 제품 이름에 대 한 값을 입력 하는 되도록도 RequiredFieldValidator 컨트롤을 추가 합니다.
- `SupplierID` None입니다.
- `CategoryID` None입니다.
- `QuantityPerUnit` 설정 하는 텍스트 상자 추가 해당 `ID` 에 `NewQuantityPerUnit`입니다.
- `UnitPrice` 라는 텍스트 상자 추가 `NewUnitPrice` 이 고 입력 한 값을 보장 하는 CompareValidator는 0 보다 크거나 통화 값입니다.
- `UnitsInStock` 텍스트 상자를 사용 하 여 해당 `ID` 로 설정 된 `NewUnitsInStock`합니다. 입력 한 값이 0 보다 크거나 정수 값을 보장 하는 CompareValidator 포함 됩니다.
- `UnitsOnOrder` 텍스트 상자를 사용 하 여 해당 `ID` 로 설정 된 `NewUnitsOnOrder`합니다. 입력 한 값이 0 보다 크거나 정수 값을 보장 하는 CompareValidator 포함 됩니다.
- `ReorderLevel` 텍스트 상자를 사용 하 여 해당 `ID` 로 설정 된 `NewReorderLevel`합니다. 입력 한 값이 0 보다 크거나 정수 값을 보장 하는 CompareValidator 포함 됩니다.
- `Discontinued` 추가 설정 CheckBox를 해당 `ID` 에 `NewDiscontinued`입니다.
- `CategoryName` DropDownList를 추가 하 고 설정 해당 `ID` 에 `NewCategoryID`입니다. 라는 한 새 ObjectDataSource에 바인딩할 `CategoriesDataSource` 를 사용 하도록 구성 합니다 `CategoriesBLL` s 클래스 `GetCategories()` 메서드. DropDownList s `ListItem` s 표시 합니다 `CategoryName` 데이터 필드를 사용 하 여는 `CategoryID` 해당 값으로 데이터 필드입니다.
- `SupplierName` DropDownList를 추가 하 고 설정 해당 `ID` 에 `NewSupplierID`입니다. 라는 한 새 ObjectDataSource에 바인딩할 `SuppliersDataSource` 를 사용 하도록 구성 합니다 `SuppliersBLL` s 클래스 `GetSuppliers()` 메서드. DropDownList s `ListItem` s 표시 합니다 `CompanyName` 데이터 필드를 사용 하 여는 `SupplierID` 해당 값으로 데이터 필드입니다.

지울 각 유효성 검사 컨트롤에 대해 합니다 `ForeColor` 속성 있도록는 `FooterStyle` 빨간색 기본값 대신 사용할 CSS 클래스 s 흰색 전경 색입니다. 또한 사용 하 여는 `ErrorMessage` 에 대 한 자세한 속성을 설정할 수 있지만 `Text` 별표 속성. 유효성 검사 컨트롤의 텍스트 두 줄으로 줄 삽입 인터페이스를 유발 하지 못하도록 설정 합니다 `FooterStyle` s `Wrap` 속성을 false로 각각에 대 한는 `FooterTemplate` 유효성 검사 컨트롤을 사용 하는 합니다. GridView 및 집합 아래에 ValidationSummary 컨트롤을 추가 하는 마지막으로, 해당 `ShowMessageBox` 속성을 `True` 및 해당 `ShowSummary` 속성을 `False`입니다.

새 제품을 추가할 때 제공 해야 합니다 `CategoryID` 고 `SupplierID`합니다. 바닥글 셀에 있는 Dropdownlist를 통해이 정보가 캡처됩니다 합니다 `CategoryName` 고 `SupplierName` 필드입니다. 와 반대로 이러한 필드를 사용 하는 `CategoryID` 및 `SupplierID` TemplateFields s 표의 데이터 행 사용자 이므로 해당 ID 값 보다는 category와 supplier 이름 확인에 더 관심이 있을 수 있습니다. 하므로 `CategoryID` 및 `SupplierID` 값에서 이제 캡처 중인를 `CategoryName` 및 `SupplierName` 필드 s 삽입 인터페이스를 제거할 수 있다는 것을 `CategoryID` 및 `SupplierID` GridView에서 TemplateFields.

마찬가지로, 합니다 `ProductID` 새 제품을 추가 하는 경우에 사용 되지 않습니다 하므로 `ProductID` TemplateField도 제거할 수 있습니다. 그러나 s 유지 하도록 합니다 `ProductID` 표의 필드입니다. 텍스트 상자, Dropdownlist, 확인란 및 삽입 인터페이스를 구성 하는 유효성 검사 컨트롤 외에 필요 추가 단추를 클릭 하면 데이터베이스에 새 제품을 추가 하는 논리를 수행 합니다. 4 단계에서에서의 삽입 인터페이스에는 추가 단추가 포함 됩니다는 `ProductID` TemplateField의 `FooterTemplate`입니다.

자유롭게 GridView의 다양 한 필드의 표시를 개선할 수 있습니다. 서식을 지정 하려는 하는 예를 들어를 `UnitPrice` 통화 값 오른쪽 맞춤 합니다 `UnitsInStock`, `UnitsOnOrder`, 및 `ReorderLevel` 필드 및 업데이트를 `HeaderText` 는 TemplateFields에 대 한 값.

인터페이스를 삽입 하는 회전을 만든 후는 `FooterTemplate` s, 제거 합니다 `SupplierID`, 및 `CategoryID` TemplateFields, 서식 및 맞춤 TemplateFields, 선언적 GridView s에 통해 그리드의 미관 향상 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample5.aspx)]

브라우저를 통해 보면 GridView가의 바닥글 행을 이제 완료 된 (그림 10 참조) 인터페이스를 삽입 합니다. 이 시점에서 삽입 인터페이스 만들어지고 t를 나타내고 해당 그녀는 s 새 제품에 대 한 데이터를 입력 한 데이터베이스에 새 레코드를 삽입 하려는 사용자에 대 한 의미를 포함 합니다. 에서는 또한 ve에서 새 레코드에 바닥글에 입력 된 데이터를 변환 하는 어떻게 해결 하는 `Products` 데이터베이스입니다. 4 단계에서 코드를 실행 하는 방법 및 삽입 인터페이스에 추가 단추를 포함 하는 방법을 살펴보겠습니다 포스트백 될 때 해당 s 클릭 합니다. 5 단계에 바닥글에서 데이터를 사용 하 여 새 레코드를 삽입 하는 방법을 보여 줍니다.


[![새 레코드를 추가 하는 것에 대 한 인터페이스를 제공 하는 GridView 바닥글](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image10.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image17.png)

**그림 10**: 새 레코드를 추가 하는 것에 대 한 인터페이스를 제공 하는 GridView 바닥글 ([큰 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image18.png))


## <a name="step-4-including-an-add-button-in-the-inserting-interface"></a>4 단계: 추가 단추를 포함 하 여 삽입 인터페이스에

인터페이스를 현재 삽입 바닥글 행 s에 새 제품의 정보 입력 완료 했음을 나타내기 위해 사용자를 위한 없으므로 삽입 인터페이스에 위치 추가 단추를 포함 해야 합니다. 기존 중 하나에 배치 될 수 있습니다이 `FooterTemplate` 또는에서는 열을 추가할 수도 새 표에이 목적입니다. 이 자습서에서는 let s에서 추가 단추를 배치 합니다 `ProductID` TemplateField의 `FooterTemplate`입니다.

디자이너에서 GridView가 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 다음을 선택 합니다 `ProductID` 필드의 `FooterTemplate` 드롭 다운 목록에서. 단추 웹 컨트롤 (또는 LinkButton 또는 추가 ImageButton을 원하는 경우) 해당 ID를 설정 합니다. 템플릿에 `AddProduct`, 해당 `CommandName` 삽입을 고 `Text` 그림 11 에서처럼 추가할 속성입니다.


[![ProductID TemplateField의 먼저 추가 단추 배치](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image11.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image19.png)

**그림 11**:에서 추가 단추를 배치 합니다 `ProductID` TemplateField s `FooterTemplate` ([클릭 하 여 큰 이미지 보기](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image20.png))


적 추가 단추에 포함 되 면 브라우저에서 페이지를 테스트 합니다. 삽입 인터페이스에 잘못 된 데이터를 사용 하 여 추가 단추를 클릭 하면 포스트백은 circuited 즉 및 ValidationSummary 컨트롤 (그림 12 참조) 잘못 된 데이터를 나타냅니다. 입력 한 적절 한 데이터를 사용 하 여 추가 단추를 클릭 하면 포스트백 합니다. 그러나 레코드가 없습니다 데이터베이스에 추가 됩니다. 약간의 실제로 삽입을 수행 하는 코드를 작성 해야 합니다.


[![단추 추가 s 포스트백이 짧은 Circuited 삽입 인터페이스에 잘못 된 데이터가 있는 경우](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image12.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image21.png)

**그림 12**: 추가 단추 포스트백이 짧은 Circuited 삽입 인터페이스에 잘못 된 데이터가 있는 경우 ([큰 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image22.png))


> [!NOTE]
> 유효성 검사 컨트롤이 삽입 인터페이스에 유효성 검사 그룹에 할당 되지 않은 합니다. 이 정상적으로 삽입 인터페이스는 페이지의 유효성 검사 컨트롤의 유일한 설정 하기만 합니다. 그러나 다른 유효성 검사 컨트롤 (예: 표 s 편집 인터페이스에 유효성 검사 컨트롤) 페이지의 인 경우 유효성 검사 컨트롤이 삽입 인터페이스 추가한 단추의 `ValidationGroup` 속성에 동일한 값을 할당 해야로 so 특정 유효성 검사 그룹을 사용 하 여 이러한 컨트롤을 연결 합니다. 참조 [ASP.NET 2.0의 유효성 검사 컨트롤 분석](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx) 유효성 검사 컨트롤과 단추가 페이지에 유효성 검사 그룹으로 분할 하는 방법은 합니다.


## <a name="step-5-inserting-a-new-record-into-theproductstable"></a>5 단계:에 새 레코드를 삽입 합니다`Products`테이블

GridView의 기본 편집 기능을 이용 하면 GridView 자동으로 처리의 모든 업데이트를 수행 하는 데 필요한 작업입니다. 특히, [업데이트] 단추를 클릭할 때 복사 ObjectDataSource에서 매개 변수를 편집 인터페이스에서 입력 한 값 `UpdateParameters` 수집 및 ObjectDataSource가 호출 하 여 업데이트를 시작 `Update()` 메서드. GridView는 삽입에 대 한 이러한 기본 제공 기능을 제공 하지 않으므로 ObjectDataSource가 호출 하는 코드를 구현 해야 했습니다 `Insert()` 메서드와 ObjectDataSource s 인터페이스는 삽입에서 값 복사 `InsertParameters` 컬렉션 .

이 삽입 논리 추가 버튼을 클릭 한 후 실행 되어야 합니다. 에 설명 된 대로 합니다 [추가한 단추를 GridView에 응답](../custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb.md) 자습서에서는 단추나 LinkButton, ImageButton GridView에서를 클릭 하면 GridView가 언제 든 지 `RowCommand` 포스트백 될 때 이벤트가 발생 합니다. 단추나 LinkButton, ImageButton 바닥글 행에 추가 단추와 같이 명시적으로 추가 된 여부 또는 GridView에서 자동으로 추가 된 경우이 이벤트 발생 (정렬 사용을 선택 하면 각 열의 맨 위에 있는 Linkbutton 같은 또는 Linkbutton 페이징 사용을 선택한 경우 페이징 인터페이스에서).

따라서 사용자 추가 단추 클릭에 응답 하려면 해야 GridView s에 대 한 이벤트 처리기를 만들고 `RowCommand` 이벤트입니다. 이 이벤트가 발생할 때마다 때문 *모든* 단추나 LinkButton, ImageButton GridView에서를 클릭 하면 해당 s는만 진행 논리를 삽입 하는 경우 중요 한를 `CommandName` 는이벤트처리기맵으로전달된속성`CommandName` 추가 단추 (Insert)의 값입니다. 또한 유효성 검사 컨트롤이 유효한 데이터를 보고 하는 경우 진행만 해야 합니다. 이 위해 만들기에 대 한 이벤트 처리기는 `RowCommand` 다음 코드를 사용 하 여 이벤트:


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample6.vb)]

> [!NOTE]
> 궁금할 이벤트 처리기 걸린다면 확인 하는 이유는 `Page.IsValid` 속성입니다. 결국 획득된 t 포스트백은 잘못 된 데이터 삽입 인터페이스에 제공 된 경우 표시 하지 않을 수 있습니까? 이 가정으로 JavaScript를 비활성화 되지 않은 사용자나 클라이언트 쪽 유효성 검사 논리를 우회 하는 단계를 수행 하는 올바릅니다. 즉, 하나에 의존 하지 않아야 엄격 하 게 클라이언트 쪽 유효성 검사 서버 쪽 유효성 검사를 데이터로 작업 하기 전에 항상 수행 되어야 합니다.


1 단계에서에서 만든 합니다 `ProductsDataSource` ObjectDataSource 되도록 해당 `Insert()` 메서드 매핑되는 `ProductsBLL` s 클래스 `AddProduct` 메서드. 에 새 레코드를 삽입 하는 `Products` 테이블 ObjectDataSource가 호출할 수 있습니다 단순히 `Insert()` 메서드:


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample7.vb)]

이제는 `Insert()` 메서드가 호출 되었고, 전달할 매개 변수에 삽입 인터페이스에서 값을 복사 하려면 유지 된 모든 합니다 `ProductsBLL` s 클래스 `AddProduct` 메서드. 다시 살펴본 것 처럼 합니다 [삽입, 업데이트 및 삭제와 관련 된 이벤트 검사](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) 자습서를 통해 ObjectDataSource가 작업을 수행할 수 있습니다 `Inserting` 이벤트. 에 `Inserting` 컨트롤을 프로그래밍 방식으로 참조 해야 하는 이벤트를 `Products` GridView가의 바닥글 행 및 해당 값을 할당 합니다 `e.InputParameters` 컬렉션. 종료 등의 값을 생략 한 경우는 `ReorderLevel` 값이 데이터베이스에 삽입 되도록 지정 해야 하는 텍스트 상자 빈 `NULL`합니다. 이후 합니다 `AddProducts` 메서드에서 nullable 데이터베이스 필드에 대 한 nullable 형식, 단순히 nullable 형식을 사용 하 고 해당 값을 설정 `Nothing` 사용자 입력은 생략 되는 경우에 합니다.


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample8.vb)]

사용 하 여는 `Inserting` 완료 되는 이벤트 처리기에서 새 레코드에 추가할 수 있습니다는 `Products` GridView가의 바닥글 행을 통해 데이터베이스 테이블입니다. 계속 해 서 여러 새로운 제품을 추가 해 보세요.

## <a name="enhancing-and-customizing-the-add-operation"></a>개선 및 사용자 지정 된 작업 추가

현재 추가 단추를 클릭 하면 데이터베이스 테이블에 새 레코드를 추가 하지만 제공 하지 않습니다 모든 종류의 시각적 피드백 레코드를 추가 했습니다. 이상적으로 레이블 웹 컨트롤 또는 클라이언트 쪽 경고 상자를는 해당 insert 성공적으로 완료 된 사용자를 게 알립니다. 필자는 판독기에 대 한 연습으로 둡니다.

이 자습서에 사용 되는 GridView 정렬 순서로 나열 된 제품에 적용 되지 않습니다도 최종 사용자가 데이터를 정렬 될 수 없습니다. 따라서 레코드는 해당 기본 키 필드에서 데이터베이스에 있는 것 처럼 정렬 됩니다. 각 새 레코드에는 `ProductID` 마지막 항목 눈금의 끝에 추가 되는 새 제품 추가 될 때마다 보다 큰 값입니다. 따라서 다음 GridView의 마지막 페이지에 새 레코드를 추가한 후 해당 사용자를 자동으로 전송 하는 것이 좋습니다. 이 호출 후 다음 코드 줄을 추가 하 여 수행할 수 있습니다 `ProductsDataSource.Insert()` 에 `RowCommand` 사용자를 보낼 마지막 페이지 GridView에 데이터를 바인딩한 후 해야 함을 나타내기 위해 이벤트 처리기:


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample9.vb)]

`SendUserToLastPage` 처음에 페이지 수준 부울 변수 값이 할당은 `False`합니다. GridView `DataBound` 이벤트 처리기 경우 `SendUserToLastPage` 이 false 인 경우는 `PageIndex` 마지막 페이지에 사용자를 보낼 속성이 업데이트 됩니다.


[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample10.vb)]

이유는 `PageIndex` 에서 속성을 설정할를 `DataBound` 이벤트 처리기 (아닌 사이트별로 `RowCommand` 이벤트 처리기) 이므로 때를 `RowCommand` 에서는 이벤트 처리기에 새 레코드를 추가 하는 ve를 제공 하는 발생는 `Products` 데이터베이스 테이블입니다. 따라서 합니다 `RowCommand` 이벤트 처리기 마지막 페이지 인덱스 (`PageCount - 1`) 마지막 페이지 인덱스를 나타내는 *전에* 새 제품이 추가 되었습니다. 대부분 추가 되는 제품의 마지막 페이지 인덱스는 새 제품을 추가한 후 없지만 경우 추가 제품 새 마지막 페이지 인덱스를 올바르게 업데이트 되지 경우 합니다 `PageIndex` 에 `RowCommand` 이벤트 처리기 그런 다음 이동 마지막 페이지 (새 제품을 추가 하기 전에 마지막 페이지 인덱스)에서 두 번째 새 마지막 페이지 i 달리 ndex 합니다. 이후를 `DataBound` 이벤트 처리기에 추가한 새 제품을 그리드로 설정 하 여 차츰 회복 데이터 후 발생 합니다 `PageIndex` 속성 있습니다 알게에서는 올바른 마지막 페이지 인덱스를 보시기.

마지막으로,이 자습서에 사용 되는 GridView는 새 제품을 추가 하는 것에 대 한 수집 해야 하는 필드 수가 매우 다양 합니다. 이 너비 인해 DetailsView s 세로 레이아웃을 기본 수 있습니다. GridView가 더 적은 수의 입력을 수집 하 여 전체 너비를 줄어들 수 있습니다. 수집 해야 하는 t 하지 우리는 아마도 합니다 `UnitsOnOrder`, `UnitsInStock`, 및 `ReorderLevel` 새 제품을 추가 하는 경우 필드 GridView에서 이러한 필드를 제거할 수 있는 경우에 합니다.

수집 된 데이터를 조정 하려면 두 가지 방법 중 하나를 사용 했습니다.

- 계속 사용 합니다 `AddProduct` 에 대 한 값을 필요로 하는 메서드를 `UnitsOnOrder`, `UnitsInStock`, 및 `ReorderLevel` 필드입니다. 에 `Inserting` 이벤트 처리기를 하드 코드 된 제공, 삽입 인터페이스에서 제거 된 이러한 입력에 사용할 기본값입니다.
- 새 오버 로드 만들기를 `AddProduct` 에서 메서드를 `ProductsBLL` 클래스에 대 한 입력을 받아들이지 않는 합니다 `UnitsOnOrder`, `UnitsInStock`, 및 `ReorderLevel` 필드. 그런 다음 ASP.NET 페이지에서이 새 오버 로드를 사용 하는 ObjectDataSource를 구성 합니다.

두 옵션 중 하나 에서도 동일 하 게 작동 합니다. 이전 자습서에서는 사용 후자 옵션을 만들기에 대 한 여러 오버 로드 된 `ProductsBLL` s 클래스 `UpdateProduct` 메서드.

## <a name="summary"></a>요약

GridView FormView 및 DetailsView 삽입 기본 제공 기능 부족 하지만 약간의 노력 삽입 인터페이스 바닥글 행에 추가할 수 있습니다. 단순히 GridView의 바닥글 행을 표시 하려면 해당 `ShowFooter` 속성을 `True`입니다. 바닥글 행 내용을 사용자 지정할 수 있습니다 각 필드에 대 한 필드를 templatefield로 변환 하 여 및 삽입을 추가 하는 인터페이스를 `FooterTemplate`입니다. 이 자습서에서 보았듯이 `FooterTemplate` Button, Textbox, Dropdownlist, 확인란, 데이터 기반 웹 컨트롤 (예: Dropdownlist)를 채우기 위한 데이터 소스 컨트롤 및 유효성 검사 컨트롤을 포함할 수 있습니다. 사용자가의 입력을 수집 하기 위한 컨트롤을 함께 추가 단추, LinkButton, imagebutton이 필요 합니다.

추가 단추를 클릭할 때, ObjectDataSource의 `Insert()` 메서드 삽입 워크플로를 시작 합니다. ObjectDataSource 구성된 삽입 메서드를 호출 하는 (합니다 `ProductsBLL` s 클래스 `AddProduct` 메서드를이 자습서). ObjectDataSource s에 대 한 인터페이스를 삽입 하는 GridView s에서 값을 복사 해야 `InsertParameters` insert 메서드를 호출 하기 전에 컬렉션입니다. ObjectDataSource에서 삽입 인터페이스 웹 컨트롤을 프로그래밍 방식으로 참조 하 여이 작업을 수행할 수 있습니다 `Inserting` 이벤트 처리기입니다.

이 자습서는 GridView의 모양을 향상에 대 한 기술에는 확인을 완료 합니다. 다음 일련의 자습서에서는 Pdf, Word 문서, 이미지 등 이진 데이터로 작업 하는 방법 및 데이터 웹 컨트롤을 검사 합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 박 광 준 Leigh 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](adding-a-gridview-column-of-checkboxes-vb.md)
