---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
title: (VB)의 데이터 수정 인터페이스 사용자 지정 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 살펴보겠습니다 표준 텍스트 상자를 대체 하 여 편집할 수는 GridView의 인터페이스를 사용자 지정 하는 방법 및 alternati 사용 확인란을 선택 하 여 제어 하는 중...
ms.author: aspnetcontent
ms.date: 07/17/2006
ms.assetid: 4830d984-bd2c-4a08-bfe5-2385599f1f7d
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 991f8d07c12c13b1477c2df072847b3730bc1051
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37840770"
---
<a name="customizing-the-data-modification-interface-vb"></a>(VB)의 데이터 수정 인터페이스 사용자 지정
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_20_VB.exe) 또는 [PDF 다운로드](customizing-the-data-modification-interface-vb/_static/datatutorial20vb1.pdf)

> 이 자습서에서는 살펴보겠습니다 표준 텍스트 상자를 대체 하 여 편집할 수는 GridView의 인터페이스를 사용자 지정 하는 방법 및 CheckBox 컨트롤이 대체 입력된 웹 컨트롤을 사용 하 여 합니다.


## <a name="introduction"></a>소개

BoundFields 및 CheckBoxFields GridView 및 DetailsView 컨트롤에서 사용 하는 읽기 전용, 편집 및 삽입 인터페이스를 렌더링 하는 기능으로 인해 데이터를 수정 하는 프로세스를 간소화 합니다. 모든 추가 선언적 태그 또는 코드를 추가 하지 않고도 이러한 인터페이스를 렌더링할 수 있습니다. 그러나 BoundField 및 CheckBoxField의 인터페이스는 실제 시나리오에서는 대개 가능성을 부족 합니다. GridView 또는 DetailsView 편집 가능 하거나 삽입 가능 인터페이스를 사용자 지정 하려면 대신 templatefield로 사용 해야 합니다.

에 [이전 자습서](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) 유효성 검사 웹 컨트롤을 추가 하 여 데이터 수정 인터페이스 사용자 지정 하는 방법에 살펴보았습니다. 이 자습서는 BoundField 및 CheckBoxField의 표준 텍스트 상자를 대체 합니다. 실제 데이터 컬렉션 웹 컨트롤 및 대체 입력된 웹 컨트롤을 사용 하 여 CheckBox 컨트롤을 사용자 지정 하는 방법을 살펴보겠습니다. 특히, 제품의 이름, 범주, 공급자 및 지원 되지 않는 상태를 업데이트할 수 있도록 편집 가능한 GridView를 빌드 해 보겠습니다. 특정 행을 편집할 때 category와 supplier 필드도 렌더링 됩니다. Dropdownlist, 사용 가능한 범주 및 공급자에서 선택 집합을 포함 하 합니다. 또한 바꿉니다 CheckBoxField의 기본 확인란을 두 가지 옵션을 제공 하는 RadioButtonList 컨트롤: "활성" 및 "중단"입니다.


[![GridView의 편집 인터페이스 Dropdownlist 및 라디오 단추가 포함 됩니다.](customizing-the-data-modification-interface-vb/_static/image2.png)](customizing-the-data-modification-interface-vb/_static/image1.png)

**그림 1**: GridView의 편집 인터페이스 포함 Dropdownlist 및 라디오 단추 ([큰 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image3.png))


## <a name="step-1-creating-the-appropriateupdateproductoverload"></a>1 단계: 적절 한 만들기`UpdateProduct`오버 로드

이 자습서에서는 제품 이름, 범주, 공급자 편집 허용 상태를 중단 하는 편집 가능한 GridView 빌드합니다. 따라서 먼저를 `UpdateProduct` 5 개의 입력 매개 변수가 이러한 네 가지 제품 값을 허용 하는 오버 로드와 `ProductID`. 이전이 오버 로드를 하나의 그러면 에서처럼:

1. 지정 된 데이터베이스에서 제품 정보를 검색할 `ProductID`,
2. 업데이트를 `ProductName`, `CategoryID`를 `SupplierID`, 및 `Discontinued` 필드 및
3. TableAdapter의 통해서만 dal과 업데이트 요청 보내기 `Update()` 메서드.

간단히 하기 위해이 오버 로드에 대 한 생략 했습니다 중단으로 표시 되는 제품의 공급 업체에서 제공 하는 제품만 되지 않습니다 보장 하는 비즈니스 규칙 검사 합니다. 언제 든 지 원하는 경우에 추가 또는 이상적으로 논리를 별도 메서드로 리팩터링 합니다.

다음 코드에서는 새 `UpdateProduct` 의 오버 로드는 `ProductsBLL` 클래스:


[!code-vb[Main](customizing-the-data-modification-interface-vb/samples/sample1.vb)]

## <a name="step-2-crafting-the-editable-gridview"></a>2 단계: 선별 편집할 수 있는 GridView

사용 하 여는 `UpdateProduct` 편집할 수는 GridView를 만들 준비가 오버 로드를 추가 합니다. 열기를 `CustomizedUI.aspx` 페이지를 `EditInsertDelete` 폴더 GridView 컨트롤을 디자이너에 추가 합니다. 다음으로 새 ObjectDataSource GridView의 스마트 태그를 만듭니다. 통해 제품 정보를 검색할 ObjectDataSource 구성 합니다 `ProductBLL` 클래스의 `GetProducts()` 메서드를 사용 하 여 제품 데이터 업데이트는 `UpdateProduct` 방금 만든 오버 로드. INSERT 및 DELETE 탭에서 드롭 다운 목록에서 (없음)를 선택 합니다.


[![방금 만든 UpdateProduct 오버 로드를 사용 하는 ObjectDataSource 구성](customizing-the-data-modification-interface-vb/_static/image5.png)](customizing-the-data-modification-interface-vb/_static/image4.png)

**그림 2**: ObjectDataSource 사용 하도록 구성 된 `UpdateProduct` 방금 만든 오버 로드 ([클릭 하 여 큰 이미지 보기](customizing-the-data-modification-interface-vb/_static/image6.png))


데이터 수정 자습서 전체에서 살펴본 대로 Visual Studio에서 만든 ObjectDataSource의 선언 구문 할당 합니다 `OldValuesParameterFormatString` 속성을 `original_{0}`입니다. 따라서 물론 작동 하지 않습니다는 비즈니스 논리 레이어를 사용 하 여 메서드가 원래 예상 하지 되므로 `ProductID` 에 전달 될 값입니다. 따라서 이전 자습서에서 수행한 대로 잠시 선언적 구문에서이 속성 할당을 제거 하거나이 대신이 속성의이 값을 설정 `{0}`합니다.

이렇게 변경 하면 ObjectDataSource의 선언 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample2.aspx)]

`OldValuesParameterFormatString` 속성이 제거 되 고 있는지를 `Parameter` 에 `UpdateParameters` 에 필요한 입력된 매개 변수의 각 컬렉션 우리의 `UpdateProduct` 오버 로드.

ObjectDataSource를 제품 값의 하위 집합만 업데이트 하도록 구성 하는 동안 GridView에 현재 표시 된 *모든* 제품 필드입니다. 잠시 GridView를 편집할 수 있도록 합니다.

- 만 포함 된 `ProductName`, `SupplierName`를 `CategoryName` BoundFields 및 `Discontinued` CheckBoxField
- `CategoryName` 하 고 `SupplierName` 필드를 표시 하기 전에 (왼쪽)는 `Discontinued` CheckBoxField
- 합니다 `CategoryName` 하 고 `SupplierName` BoundFields' `HeaderText` 속성이 각각 "Category" 및 "공급자"로 설정 되어
- 편집 지원 됩니다 (GridView의 스마트 태그 편집 사용 확인란을 확인 합니다.)

이러한 변경 이후 디자이너가 비슷합니다 그림 3, 아래에 표시 된 GridView의 선언적 구문을 사용 하 여 합니다.


[![GridView에서 불필요 한 필드를 제거 합니다.](customizing-the-data-modification-interface-vb/_static/image8.png)](customizing-the-data-modification-interface-vb/_static/image7.png)

**그림 3**: GridView에서 불필요 한 필드를 제거 ([큰 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image9.png))


[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample3.aspx)]

이 시점에서 GridView의 읽기 전용 동작이 완료 되었습니다. 데이터를 볼 때 각 제품 공급 업체, 제품의 이름, 범주를 보여 주는 GridView의 행으로 렌더링 되 고 상태를 중단 합니다.


[![GridView의 읽기 전용 인터페이스는 완료](customizing-the-data-modification-interface-vb/_static/image11.png)](customizing-the-data-modification-interface-vb/_static/image10.png)

**그림 4**: GridView의 읽기 전용 인터페이스는 완료 ([큰 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image12.png))


> [!NOTE]
> 에 설명 된 대로 [An 개요의 삽입, 업데이트 및 삭제 데이터 자습서](an-overview-of-inserting-updating-and-deleting-data-cs.md), 반드시 s 보기 상태가 GridView (기본 동작)을 사용할 수 있도록 합니다. GridView가 설정 하는 경우 `EnableViewState` 속성을 `false`, 동시 사용자가 실수로 삭제 하거나 편집할 레코드의 위험이 있습니다. 참조 [경고: 동시성 문제 사용 하 여 ASP.NET 2.0 Gridview/DetailsView/FormViews 해당 지원 편집 및/또는 삭제 하 고 있는 뷰 상태를 사용 하지 않도록 설정](http://scottonwriting.net/sowblog/posts/10054.aspx) 자세한 내용은 합니다.


## <a name="step-3-using-a-dropdownlist-for-the-category-and-supplier-editing-interfaces"></a>3 단계: DropDownList를 사용 하 여 인터페이스를 편집 하는 공급자 및 범주에 대 한

이전에 설명한 대로 합니다 `ProductsRow` 개체에 포함 되어 `CategoryID`, `CategoryName`, `SupplierID`, 및 `SupplierName` 속성의 실제 외래 키 ID 값을 제공 하는 `Products` 데이터베이스 테이블 및 해당 `Name` 값을 `Categories` 고 `Suppliers` 테이블입니다. `ProductRow`의 `CategoryID` 및 `SupplierID` 둘 다에서 읽고 수 하는 동안에 기록 합니다 `CategoryName` 및 `SupplierName` 속성은 읽기 전용으로 표시 됩니다.

읽기 전용 상태에 따라 합니다 `CategoryName` 및 `SupplierName` 속성을 해당 BoundFields 했 해당 `ReadOnly` 속성이로 설정 `True`, 행을 편집 하는 경우 수정 되지 않도록 이러한 값을 방지 합니다. 설정할 수 있습니다 하는 동안 합니다 `ReadOnly` 속성을 `False`렌더링, 합니다 `CategoryName` 및 `SupplierName` BoundFields 편집 하는 동안 텍스트 상자와, 이러한 접근 하면 예외가 사용자가 있기 때문에 제품을 업데이트 하려고 할 때 없습니다 `UpdateProduct` 에 오버 로드 `CategoryName` 고 `SupplierName` 입력 합니다. 사실 두 가지 이유로 이러한 오버 로드를 만들 하려고 하지 않습니다.

- `Products` 표에 없습니다 `SupplierName` 또는 `CategoryName` 필드에 있지만 `SupplierID` 및 `CategoryID`합니다. 따라서이 메서드를 이러한 특정 ID 값을 해당 조회 테이블의 값이 아닌 전달 하도록 하려고 합니다.
- 사용 가능한 범주 및 공급자가 올바른 철자를 알고 사용자 필요 하므로 사용자는 공급 업체 또는 범주 이름을 입력 하도록 요구 하는 것은 보다 작은 적합 합니다.

공급자 및 범주 필드를 읽기 전용 모드에 있을 때 공급자의 이름과 범주에 표시 됩니다 (마찬가지로 이제) 및 편집 하 고 있는 경우 해당 옵션의 드롭다운 목록입니다. 드롭 다운 목록을 사용 하 최종 사용자는 범주 및 공급자 중에서 선택에 사용할 수를 신속 하 게 볼 수 및 수 더 쉽게 선택 합니다.

이 동작을 제공 하려면 변환 해야 합니다 `SupplierName` 및 `CategoryName` BoundFields TemplateFields에입니다 `ItemTemplate` 내보냅니다를 `SupplierName` 및 `CategoryName` 값 및 해당 `EditItemTemplate` 목록 DropDownList 컨트롤을 사용 하는 사용 가능한 범주 및 공급 업체입니다.

## <a name="adding-thecategoriesandsuppliersdropdownlists"></a>추가 된`Categories`고`Suppliers`Dropdownlist

변환 하 여 시작 합니다 `SupplierName` 및 `CategoryName` 에서 TemplateFields에 BoundFields: GridView의 스마트 태그에서 열 편집 링크를 클릭 하는 BoundField 왼쪽; 목록에서 선택 하 고 클릭 하는 "이이 필드를 변환는 TemplateField"링크입니다. 둘 다를 사용 하 여 변환 프로세스를 TemplateField 만듭니다는 `ItemTemplate` 및 `EditItemTemplate`선언적 구문 아래에 나와 있는 것 처럼:


[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample4.aspx)]

BoundField 읽기 전용으로 표시 된 이후 모두를 `ItemTemplate` 및 `EditItemTemplate` 포함 레이블 웹 컨트롤 `Text` 속성은 해당 데이터 필드에 바인딩됩니다 (`CategoryName`, 위의 구문에서). 수정 해야 합니다 `EditItemTemplate`, DropDownList 컨트롤을 사용 하 여 웹 컨트롤을 대체 합니다.

이전 자습서에서 살펴본 대로 디자이너를 통해 또는 선언적 구문에서 직접 템플릿을 편집할 수 있습니다. 디자이너를 통해 편집을 GridView의 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 범주 필드를 사용 하 여 작업을 선택 `EditItemTemplate`합니다. 웹 컨트롤을 제거 하 고 DropDownList의 ID 속성을 설정 하는 DropDownList 컨트롤을 사용 하 여 대체 `Categories`합니다.


[![텍스트 상자를 제거 하 고는 EditItemTemplate DropDownList 추가](customizing-the-data-modification-interface-vb/_static/image14.png)](customizing-the-data-modification-interface-vb/_static/image13.png)

**그림 5**:의 텍스트 상자를 제거 하 고는 DropDownList를 추가 합니다 `EditItemTemplate` ([클릭 하 여 큰 이미지 보기](customizing-the-data-modification-interface-vb/_static/image15.png))


다음 사용 가능한 범주를 사용 하 여 DropDownList를 채우는 해야 합니다. DropDownList의 스마트 태그의 데이터 소스 선택 링크를 클릭 하 고 명명 된 새 ObjectDataSource를 만들도록 선택할 `CategoriesDataSource`합니다.


[![CategoriesDataSource 라는 새 ObjectDataSource 컨트롤 만들기](customizing-the-data-modification-interface-vb/_static/image17.png)](customizing-the-data-modification-interface-vb/_static/image16.png)

**그림 6**: 명명 된 새 ObjectDataSource 컨트롤을 만듭니다 `CategoriesDataSource` ([클릭 하 여 큰 이미지 보기](customizing-the-data-modification-interface-vb/_static/image18.png))


모든 범주를 반환 하는이 ObjectDataSource가 바인딩할 하는 `CategoriesBLL` 클래스의 `GetCategories()` 메서드.


[![ObjectDataSource CategoriesBLL의 GetCategories() 메서드에 바인딩](customizing-the-data-modification-interface-vb/_static/image20.png)](customizing-the-data-modification-interface-vb/_static/image19.png)

**그림 7**: ObjectDataSource에 바인딩하는 `CategoriesBLL`의 `GetCategories()` 메서드 ([클릭 하 여 큰 이미지 보기](customizing-the-data-modification-interface-vb/_static/image21.png))


마지막으로, DropDownList의 설정을 구성 되도록 합니다 `CategoryName` 필드는 각 DropDownList에 표시 됩니다 `ListItem` 사용 하 여는 `CategoryID` 값으로 사용 되는 필드입니다.


[![범주 필드 표시 있고 CategoryID 값으로 사용 됩니다.](customizing-the-data-modification-interface-vb/_static/image23.png)](customizing-the-data-modification-interface-vb/_static/image22.png)

**그림 8**:가 합니다 `CategoryName` 필드가 표시 하며 `CategoryID` 값으로 사용 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image24.png))


이러한 변경한 후에 대 한 선언적 태그를 `EditItemTemplate` 에 `CategoryName` TemplateField DropDownList 및 ObjectDataSource를 모두 포함 됩니다:


[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample5.aspx)]

> [!NOTE]
> DropDownList를 `EditItemTemplate` 보기 상태로 사용할 수 있어야 합니다. DropDownList의 선언적 구문에 데이터 바인딩 구문을 추가 곧 및와 같은 데이터 바인딩 명령도 `Eval()` 고 `Bind()` 뷰 상태가 사용 하도록 설정 하는 컨트롤에만 나타날 수 있습니다.


라는 DropDownList를 추가 하려면 다음이 단계를 반복 `Suppliers` 에 `SupplierName` TemplateField의 `EditItemTemplate`합니다. DropDownList를 추가 합니다. 여기서는 `EditItemTemplate` 다른 ObjectDataSource를 만들고 있습니다. 하지만 합니다 `Suppliers` 를 호출 하도록 구성 해야, DropDownList의 ObjectDataSource 합니다 `SuppliersBLL` 클래스의 `GetSuppliers()` 메서드. 또한 구성 합니다 `Suppliers` 표시할 DropDownList를 `CompanyName` 필드를 사용 하 여를 `SupplierID` 필드의 값으로 해당 `ListItem` s입니다.

두는 Dropdownlist를 추가한 후 `EditItemTemplate` 브라우저에서 페이지를 로드 및 Chef 100 케이준 Seasoning 제품에 대 한 편집 단추를 클릭 합니다. 그림 9에서 알 수 있듯이, 제품의 category와 supplier 열 공급자에서 선택 하 고 사용 가능한 범주를 포함 하는 드롭다운 목록으로 렌더링 됩니다. 그러나 합니다 *첫 번째* 모두 드롭 다운 목록에서 항목 기본적으로 선택 됩니다 (음료 범주) 및 특이 한 액체 공급자에 New Orleans 케이준에서 제공 하는 Condiment는 Chef 100 케이준 Seasoning Delights 합니다.


[![드롭다운 목록에서 첫 번째 항목은 기본적으로 선택](customizing-the-data-modification-interface-vb/_static/image26.png)](customizing-the-data-modification-interface-vb/_static/image25.png)

**그림 9**: 드롭다운 목록에서 첫 번째 항목은 기본적으로 선택 됩니다 ([큰 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image27.png))


또한 업데이트를 클릭 하면 알 수 있는 제품 `CategoryID` 하 고 `SupplierID` 값으로 설정 됩니다 `NULL`합니다. 때문에 한 동작이 의도 하지 않은 두 가지 모두에서 Dropdownlist를 `EditItemTemplate` 제품 데이터의 모든 데이터 필드에 s 바인딩되지 않은 합니다.

## <a name="binding-the-dropdownlists-to-thecategoryidandsupplieriddata-fields"></a>Dropdownlist 바인딩 합니다`CategoryID`고`SupplierID`데이터 필드

편집 된 제품의 category와 supplier 하려면 드롭다운 목록 설정 BLL의 다시 전송 하는 이러한 값을 적절 한 값을 `UpdateProduct` Dropdownlist 바인딩할 해야 업데이트를 클릭 하면 메서드를 `SelectedValue` 속성에는 `CategoryID` 고 `SupplierID` 양방향 데이터 바인딩을 사용 하 여 데이터 필드입니다. 사용 하 여이 작업을 수행 하는 `Categories` 드롭다운 목록에서 추가한 `SelectedValue='<%# Bind("CategoryID") %>'` 선언적 구문에 직접.

또는 디자이너를 통해 템플릿을 편집 하 고 DropDownList의 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 하 여 DropDownList의 데이터 바인딩을 설정할 수 있습니다. 다음으로 나타내는 합니다 `SelectedValue` 속성에 각각 바인딩해야 합니다 `CategoryID` 양방향 데이터 바인딩을 사용 하 여 필드 (그림 10 참조). 바인딩할 선언적 또는 디자이너 프로세스를 반복 합니다 `SupplierID` 데이터 필드를 `Suppliers` DropDownList 합니다.


[![CategoryID 양방향 데이터 바인딩을 사용 하 여 DropDownList의 SelectedValue 속성에 바인딩](customizing-the-data-modification-interface-vb/_static/image29.png)](customizing-the-data-modification-interface-vb/_static/image28.png)

**그림 10**: 바인딩하는 `CategoryID` DropDownList의에 `SelectedValue` 사용 하 여 양방향 데이터 바인딩 속성 ([클릭 하 여 큰 이미지 보기](customizing-the-data-modification-interface-vb/_static/image30.png))


바인딩이 적용 된 후의 `SelectedValue` Dropdownlist 두의 속성을 편집된 하는 제품의 category와 supplier 열은 기본적으로 현재 제품의 값입니다. 업데이트를 클릭 하면를 `CategoryID` 하 고 `SupplierID` 선택한 드롭 다운 목록 항목의 값에 전달 됩니다는 `UpdateProduct` 메서드. 데이터 바인딩 문을 추가한; 후 그림 11은 자습서 Chef 100 케이준 Seasoning 선택한 드롭다운 목록에서 항목와 되는 방식 올바르게 Condiment New Orleans 케이준 Delights note 합니다.


[![기본적으로 선택 되어 편집할 제품의 현재 범주 및 공급자 값](customizing-the-data-modification-interface-vb/_static/image32.png)](customizing-the-data-modification-interface-vb/_static/image31.png)

**그림 11**: The 편집할 제품의 현재 범주 및 공급자 값은 기본적으로 선택 됩니다 ([큰 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image33.png))


## <a name="handlingnullvalues"></a>처리`NULL`값

`CategoryID` 및 `SupplierID` 열에는 `Products` 테이블 일 수 있습니다 `NULL`, 아직에서 Dropdownlist를 `EditItemTemplate` s를 나타내는 목록 항목을 포함 하지 않습니다는 `NULL` 값. 여기에 두 개의 결과가 있습니다.

- 비-에서 제품의 범주 또는 공급 업체를 변경 하려면 사용자 인터페이스를 사용할 수 없습니다`NULL` 값을 `NULL` 하나
- 제품에는 `NULL` `CategoryID` 또는 `SupplierID`에 편집 단추를 클릭 하면 예외가 발생 됩니다. 왜냐하면를 `NULL` 에서 반환 된 값 `CategoryID` (또는 `SupplierID`)에 `Bind()` 문을 DropDownList의 값에 매핑되지 않는 경우 (DropDownList 예외를 throw 때 해당 `SelectedValue` 값속성*되지* 목록 항목의 컬렉션에서).

지원 하기 위해 `NULL` `CategoryID` 하 고 `SupplierID` 값을 추가 해야 다른 `ListItem` 나타내는 각 DropDownList를는 `NULL` 값입니다. 에 [마스터/세부 정보 필터링으로 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) 자습서를 더 추가 하는 방법에 살펴보았습니다 `ListItem` DropDownList 데이터 바인딩된에는 관련 DropDownList의 설정 `AppendDataBoundItems` 속성을 `True` 및 일일이 추가 `ListItem`합니다. 그러나 이전 자습서에서 추가한를 `ListItem` 사용 하 여는 `Value` 의 `-1`합니다. 그러나 asp.net에서 데이터 바인딩 논리는 빈 문자열을 자동으로 변환 된 `NULL` 값과는 반대로 합니다. 따라서이 자습서에 대 한 원하는 합니다 `ListItem`의 `Value` 는 빈 문자열일 수 있습니다.

Dropdownlist 두를 설정 하 여 시작 `AppendDataBoundItems` 속성을 `True`입니다. 다음을 추가 합니다 `NULL` `ListItem` 다음을 추가 하 여 `<asp:ListItem>` 요소 각 DropDownList 선언적 태그 표시 되도록 같은:


[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample6.aspx)]

했다는 "(None)"를 사용 하 여 텍스트 값으로이 `ListItem`, 원하는 경우 빈 문자열도 수를 변경할 수 있습니다.

> [!NOTE]
> 설명한 것 처럼 합니다 *마스터/세부 정보 필터링으로 DropDownList* 자습서 `ListItem` s DropDownList의에서 클릭 하 여 디자이너를 통해 DropDownList에 추가할 수 있습니다 `Items` 속성 창에서 속성 ( 표시 된 `ListItem` 컬렉션 편집기). 그러나 추가 해야 합니다 `NULL` `ListItem` 선언적 구문을 통해이 자습서에 대 한 합니다. 사용 하는 경우는 `ListItem` 생성 된 선언적 구문에서 생략 됩니다 컬렉션 편집기를 `Value` 와 같은 선언적 태그를 만들 빈 문자열로 할당 된 경우 설정을 완전히: `<asp:ListItem>(None)</asp:ListItem>`합니다. 누락 값 DropDownList를 사용 하면 치명적이 지 보일 수 있습니다, 있지만 `Text` 해당 위치에서 속성 값입니다. 즉, 해당 경우가 `NULL` `ListItem` 는 선택 "(None)" 값 하려고 할당할 수는 `CategoryID`는 예외가 발생 합니다. 명시적으로 설정 하 여 `Value=""`, `NULL` 값에 할당할 `CategoryID` 때 합니다 `NULL` `ListItem` 을 선택 합니다.


공급 업체 DropDownList에 대해 이러한 단계를 반복 합니다.

이 사용 하 여 추가 `ListItem`, 이제 편집 인터페이스를 할당할 수 있습니다 `NULL` 제품의 값 `CategoryID` 및 `SupplierID` 그림 12에 나와 있는 것 처럼 필드입니다.


[![제품의 범주 또는 공급 업체에 대해 NULL 값을 할당할 (없음)을 선택 합니다.](customizing-the-data-modification-interface-vb/_static/image35.png)](customizing-the-data-modification-interface-vb/_static/image34.png)

**그림 12**: 할당할 (없음)를 선택 된 `NULL` 제품의 범주 또는 공급 업체에 대 한 값 ([클릭 하 여 큰 이미지 보기](customizing-the-data-modification-interface-vb/_static/image36.png))


## <a name="step-4-using-radiobuttons-for-the-discontinued-status"></a>4 단계: 지원 되지 않는 상태에 대 한 라디오 단추를 사용 하 여

현재 제품의 `Discontinued` 데이터 필드는 읽기 전용으로 행에 대 한 비활성화 된 확인란 및 편집 되는 행에 대 한 사용된 확인란을 렌더링 하는 한 CheckBoxField를 사용 하 여 표현 됩니다. 이 사용자 인터페이스 적합 하지만 우리 사용자 지정할 수를 TemplateField를 사용 하 여 필요한 경우. 이 자습서에서는 변경해 보겠습니다는 CheckBoxField 제품의 사용자 지정할 수 있는 두 가지 옵션 "활성" 및 "중단" RadioButtonList 컨트롤을 사용 하는 TemplateField로 `Discontinued` 값입니다.

변환 하 여 시작 합니다 `Discontinued` CheckBoxField templatefield로 사용 하 여 만드는 TemplateField로는 `ItemTemplate` 및 `EditItemTemplate`합니다. 두 템플릿 모두 사용 하는 확인란을 포함 해당 `Checked` 속성에 바인딩됩니다를 `Discontinued` 데이터 필드에 둘 사이의 유일한 차이점은 `ItemTemplate`의 확인란의 `Enabled` 속성이 `False`.

확인란을 모두 대체 합니다 `ItemTemplate` 및 `EditItemTemplate` RadioButtonList 컨트롤과 두 RadioButtonLists' 설정 `ID` 속성을 `DiscontinuedChoice`입니다. 다음으로, 나타냅니다는 RadioButtonLists 해야 각각 포함 하는 두 개의 라디오 단추를 레이블이 지정 된 "활성" 값이 "False" 및 "중단" 레이블이 지정 된 값이 "True" 인. 입력 하거나이 수행 하는 `<asp:ListItem>` 선언적 구문 또는 사용을 통해 직접 요소를 `ListItem` 디자이너에서 컬렉션 편집기입니다. 그림 13은는 `ListItem` 컬렉션 편집기 후 두 개의 라디오 단추 옵션 지정 되었습니다.


[![RadioButtonList 활성 상태이 고 지원 되지 않는 옵션 추가](customizing-the-data-modification-interface-vb/_static/image38.png)](customizing-the-data-modification-interface-vb/_static/image37.png)

**그림 13**: 활성 추가 및 RadioButtonList에 지원 되지 않는 옵션 ([큰 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image39.png))


RadioButtonList 이후 합니다 `ItemTemplate` 편집할 수 없습니다 설정 해당 `Enabled` 속성을 `False`를 `Enabled` 속성을 `True` (기본값)에서 RadioButtonList에 대 한는 `EditItemTemplate`합니다. 이 읽기 전용으로 편집 되지 않은 행의 라디오 단추를 확인 하는 있지만 편집된 된 행에 대 한 RadioButton 값을 변경 하려면 사용자 수 있게 됩니다.

RadioButtonList 컨트롤의 할당 해야 `SelectedValue` 제품에 따라 적절 한 라디오 단추를 선택할 속성 `Discontinued` 데이터 필드입니다. 이 자습서의 앞부분에서 검사 Dropdownlist, 마찬가지로이 데이터 바인딩 구문을 추가할 수 있습니다 선언적 태그에 직접 또는 RadioButtonLists의 스마트 태그에 데이터 바인딩 편집 링크를 통해.

두 RadioButtonLists를 추가 하 고, 구성한는 `Discontinued` TemplateField의 선언적 태그와 같습니다.


[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample7.aspx)]

이러한 변경으로는 `Discontinued` 열 확인란 목록에서 라디오 단추 쌍 (그림 14 참조)로 변환 되었습니다. 제품을 편집할 때 적절 한 라디오 단추를 선택한 다른 라디오 단추를 선택 하 고 업데이트를 클릭 하 여 제품의 지원 되지 않는 상태를 업데이트할 수 있습니다.


[![지원 되지 않는 확인란 라디오 단추 쌍으로 대체 되었습니다.](customizing-the-data-modification-interface-vb/_static/image41.png)](customizing-the-data-modification-interface-vb/_static/image40.png)

**그림 14**:은 지원 되지 않는 확인란 바뀌었습니다 라디오 단추 쌍 ([큰 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image42.png))


> [!NOTE]
> 있으므로 합니다 `Discontinued` 열에는 `Products` 데이터베이스 가질 수 없습니다 `NULL` 값에서는 캡처에 대해 걱정 하지 않아도 `NULL` 인터페이스에 대 한 정보. 그러나 If, `Discontinued` 열이 포함 될 수 있습니다 `NULL` 세 번째를 추가 하려고 하는 값 라디오 단추를 사용 하 여 목록 해당 `Value` 빈 문자열로 설정 (`Value=""`) 마찬가지로 category와 supplier Dropdownlist 사용 하 여 합니다.


## <a name="summary"></a>요약

BoundField 및 CheckBoxField를 자동으로 읽기 전용, 편집 및 삽입 인터페이스를 렌더링 하는 동안 사용자 지정 기능을 부족 합니다. 종종 그러나 해야 편집 또는 삽입 인터페이스를 사용자 지정 하려면 아마도 (보았듯이 이전 자습서에서) 유효성 검사 컨트롤을 추가 하거나 (에서 보았듯이이 자습서) 데이터 수집 사용자 인터페이스를 사용자 지정 합니다. 인터페이스를 TemplateField 사용 하 여 사용자 지정 합계를 구할 수 다음 단계에서:

1. Templatefield로 추가 하거나 기존 BoundField 또는 CheckBoxField를 TemplateField로 변환
2. 필요에 따라 인터페이스를 보강
3. 양방향 데이터 바인딩을 사용 하 여 새로 추가 된 웹 컨트롤에 적절 한 데이터 필드 바인딩

또한 기본 제공 ASP.NET 웹 컨트롤을 사용 하는 것 외에도 templatefield로 컴파일된 사용자 지정 서버 컨트롤 및 사용자 컨트롤을 사용 하 여 템플릿을 사용자 지정할 수 있습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
> [다음](implementing-optimistic-concurrency-vb.md)
