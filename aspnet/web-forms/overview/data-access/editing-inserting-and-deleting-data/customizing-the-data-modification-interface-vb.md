---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
title: 데이터 수정 인터페이스 (VB) 사용자 지정 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서 살펴보게 표준 텍스트 상자를 대체 하 여 편집할 수는 GridView의 인터페이스를 사용자 지정 하는 방법을 사용 하 게 확인란 제어 alternati 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/17/2006
ms.topic: article
ms.assetid: 4830d984-bd2c-4a08-bfe5-2385599f1f7d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 7d334a86fcf2fbd1069628527c6e89f3ab655dd5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30888632"
---
<a name="customizing-the-data-modification-interface-vb"></a>데이터 수정 인터페이스 (VB) 사용자 지정
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_20_VB.exe) 또는 [PDF 다운로드](customizing-the-data-modification-interface-vb/_static/datatutorial20vb1.pdf)

> 이 자습서에서 살펴보게 표준 텍스트 상자를 대체 하 여 편집할 수는 GridView의 인터페이스를 사용자 지정 하는 방법 및 CheckBox 컨트롤 입력 웹 컨트롤을 대체 합니다.


## <a name="introduction"></a>소개

BoundFields 및 CheckBoxFields GridView 및 DetailsView 컨트롤에서 사용 하는 읽기 전용, 편집할 수 및 삽입 가능 인터페이스를 렌더링 하는 기능으로 인해 데이터 수정 프로세스를 간소화 합니다. 모든 선언적 태그를 추가 또는 코드를 추가 하는 데 필요 없이 이러한 인터페이스를 렌더링할 수 있습니다. 그러나 BoundField 및 CheckBoxField의 인터페이스는 종종 실제 시나리오에 필요한 가능성을 부족 합니다. GridView 또는 DetailsView의 편집 가능 하거나 삽입 가능 인터페이스를 사용자 지정 하기 위해를 TemplateField를 대신 사용 해야 합니다.

에 [이전 자습서](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) 유효성 검사 웹 컨트롤을 추가 하 여 데이터 수정 인터페이스를 사용자 지정 하는 방법에 대해 살펴보았습니다. 이 자습서는 BoundField 및 CheckBoxField의 표준 텍스트 상자를 교체 실제 데이터 컬렉션 웹 컨트롤 및 대체 입력된 웹 컨트롤을 사용 하 여 확인란 컨트롤을 사용자 지정 하는 방법을 살펴보겠습니다. 특히, 제품의 이름, 범주, 공급자 및 지원 되지 않는 상태 업데이트를 허용 하는 편집 가능한 GridView 빌드합니다. 특정 행을 편집할 때 공급 업체 범주 필드는 dropdownlist 활용을로 렌더링 될 사용 가능한 범주와 공급 업체에서 선택할 수 세트를 포함 합니다. 두 옵션을 제공 하는 RadioButtonList 컨트롤과 함께 CheckBoxField의 기본 확인란에서는 바꿉니다 또한: "활성" 및 "중단"입니다.


[![GridView의 편집 인터페이스 dropdownlist 활용 및 라디오 단추를 포함합니다.](customizing-the-data-modification-interface-vb/_static/image2.png)](customizing-the-data-modification-interface-vb/_static/image1.png)

**그림 1**: GridView의 인터페이스 포함 dropdownlist 활용 편집 및 라디오 단추 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image3.png))


## <a name="step-1-creating-the-appropriateupdateproductoverload"></a>1 단계: 적절 한 만들기`UpdateProduct`오버 로드

이 자습서에서는 제품 이름, 범주, 공급 업체의 편집을 허용 하 고 상태를 중단 하는 편집 가능한 GridView을 작성 합니다. 따라서 필요는 `UpdateProduct` 5 4 개의 제품 값이 입력 매개 변수를 허용 하는 오버 로드와 `ProductID`합니다. 이전 우리의 오버 로드를이 하나에와 같이:

1. 지정 된 데이터베이스에서 제품 정보를 검색할 `ProductID`,
2. 업데이트는 `ProductName`, `CategoryID`, `SupplierID`, 및 `Discontinued` 필드 및
3. 에 dal과 TableAdapter의를 통해 업데이트 요청을 보내기 `Update()` 메서드.

간단한 설명을 위해이 오버 로드에 대 한 생략 했습니다 중단 하는 것으로 표시 되 고 제품의 공급 업체에서 제공 하는 유일한 제품 되지 않습니다 보장 하는 비즈니스 규칙 검사 합니다. 느낌을 원하는 경우에 추가 또는 이상적으로 논리는 별도 메서드를 리팩터링 합니다.

다음 코드에서는 새 `UpdateProduct` 에 오버 로드는 `ProductsBLL` 클래스:


[!code-vb[Main](customizing-the-data-modification-interface-vb/samples/sample1.vb)]

## <a name="step-2-crafting-the-editable-gridview"></a>2 단계: 직접 편집할 수 있는 GridView

와 `UpdateProduct` 우리의 편집 가능한 GridView 만들 준비가 오버 로드를 추가 합니다. 열기는 `CustomizedUI.aspx` 페이지에 `EditInsertDelete` 폴더 GridView 컨트롤 디자이너에 추가 합니다. GridView의 스마트 태그에서 새 ObjectDataSource를 다음으로 만듭니다. 구성 ObjectDataSource를 통해 제품 정보를 검색 하는 `ProductBLL` 클래스의 `GetProducts()` 메서드를 사용 하 여 제품 데이터 업데이트는 `UpdateProduct` 방금 만든 오버 로드 합니다. INSERT 및 DELETE 탭 중에서 드롭 다운 목록에서 (없음)를 선택 합니다.


[![ObjectDataSource 방금 만든 UpdateProduct 오버 로드를 사용 하도록 구성](customizing-the-data-modification-interface-vb/_static/image5.png)](customizing-the-data-modification-interface-vb/_static/image4.png)

**그림 2**: 구성에 사용 하 여 ObjectDataSource는 `UpdateProduct` 방금 만든 오버 로드 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image6.png))


Visual Studio에서 만든 ObjectDataSource에 대 한 선언적 구문 할당 데이터 수정 자습서 전체에서 살펴본 대로 `OldValuesParameterFormatString` 속성을 `original_{0}`합니다. 이 물론,와 작동 하지 않는 비즈니스 논리 계층 우리의 메서드는 원래 원하지 이후 `ProductID` 에 전달 될 값입니다. 따라서 이전 자습서에서 수행한 대로 잠시 하는 선언적 구문에서이 속성 할당을 제거 하거나 대신,이 속성의이 값을 설정 `{0}`합니다.

이 변경 후 ObjectDataSource의 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample2.aspx)]

`OldValuesParameterFormatString` 속성을 제거 하 고 있다는 `Parameter` 에 `UpdateParameters` 필요한 입력된 매개 변수를 각각에 대 한 컬렉션 우리의 `UpdateProduct` 오버 로드 합니다.

GridView에 현재 표시 된 ObjectDataSource를 제품 값의 하위 집합만 업데이트 하도록 구성 하는 동안 *모든* 제품 필드입니다. GridView 편집을 있도록:

- 포함 된 `ProductName`, `SupplierName`, `CategoryName` BoundFields 및 `Discontinued` CheckBoxField
- `CategoryName` 및 `SupplierName` 필드 (왼쪽)을 앞에 표시 하는 `Discontinued` CheckBoxField
- `CategoryName` 및 `SupplierName` BoundFields' `HeaderText` 속성이 각각 "범주"와 "공급 업체"로 설정 되어
- 편집 지원을 사용 하도록 설정 (확인란을 설정 하려면 편집 GridView의 스마트 태그)

이러한 변경 된 후 디자이너는 유사 그림 3에 아래 표시 된 GridView의 선언 구문을 사용 합니다.


[![GridView에서 불필요 한 필드를 제거 합니다.](customizing-the-data-modification-interface-vb/_static/image8.png)](customizing-the-data-modification-interface-vb/_static/image7.png)

**그림 3**: GridView에서 불필요 한 필드를 제거 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image9.png))


[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample3.aspx)]

이 시점에서 GridView의 읽기 전용 동작이 완료 되었습니다. 데이터를 볼 때 각 제품 제품의 이름, 범주, 공급 업체를 보여 주는 GridView에서 행으로 렌더링 되 고 상태를 중단 합니다.


[![GridView의 읽기 전용 인터페이스는 완료](customizing-the-data-modification-interface-vb/_static/image11.png)](customizing-the-data-modification-interface-vb/_static/image10.png)

**그림 4**: GridView의 읽기 전용 인터페이스는 완료 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image12.png))


> [!NOTE]
> 에 설명 된 대로 [는 개요의 삽입, 업데이트 및 삭제 데이터 자습서](an-overview-of-inserting-updating-and-deleting-data-cs.md), 반드시 s 뷰 상태 수 GridView (기본 동작)을 사용할 수 있도록 합니다. GridView s를 설정 하면 `EnableViewState` 속성을 `false`, 위험을 실수로 삭제 하거나 편집을 기록 하는 동시 사용자가 실행 합니다. 참조 [경고: 동시성 문제가 있는 ASP.NET 2.0 Gridview/DetailsView/FormViews 해당 편집을 원하는 및/또는 삭제 및 뷰 상태를 사용 하지 않으면](http://scottonwriting.net/sowblog/posts/10054.aspx) 자세한 정보에 대 한 합니다.


## <a name="step-3-using-a-dropdownlist-for-the-category-and-supplier-editing-interfaces"></a>3 단계: DropDownList를 사용 하 여 범주 및 인터페이스를 편집 하는 공급 업체에 대 한

이전에 설명한 대로 `ProductsRow` 개체에 포함 되어 `CategoryID`, `CategoryName`, `SupplierID`, 및 `SupplierName` 에 실제 외래 키 ID 값을 제공 하는 속성은 `Products` 데이터베이스 테이블 및 해당 `Name` 값에 `Categories` 및 `Suppliers` 테이블입니다. `ProductRow`의 `CategoryID` 및 `SupplierID` 수 둘 다에서 읽고 쓸 수는 동안에 `CategoryName` 및 `SupplierName` 속성은 읽기 전용으로 표시 됩니다.

읽기 전용 상태에 따라는 `CategoryName` 및 `SupplierName` 속성을 해당 BoundFields 했습니다 자신의 `ReadOnly` 속성이로 설정 `True`, 이러한 값 행을 편집할 때 수정 되지 않도록 방지 합니다. 설정 수 하는 동안는 `ReadOnly` 속성을 `False`렌더링는 `CategoryName` 및 `SupplierName` BoundFields 편집 하는 동안 입력란으로, 이러한 접근 방식은 예외가 발생 합니다는 사용자가 없기 때문에 제품을 업데이트 하려고 할 때 없습니다 `UpdateProduct` 는 수행 하는 오버 로드 `CategoryName` 및 `SupplierName` 입력 합니다. 실제로 두 가지 이유로 이러한 오버 로드를 만들지 않으려는:

- `Products` 테이블 한 `SupplierName` 또는 `CategoryName` 필드 하지만 `SupplierID` 및 `CategoryID`합니다. 따라서 이러한 특정 ID 값의 조회 테이블의 값이 아닌 전달할 메서드의 주시기 바랍니다.
- 되므로 사용자는 해당 공급 업체 또는 범주 이름을 입력 하는 사용자에 게 사용 가능한 범주 및 공급 업체 및 해당 올바른 맞춤법을 알려 필요 하기에 적합 하지 않습니다.

범주 및 읽기 전용 모드에 있을 때 공급자 이름 공급 업체와 범주 필드가 표시 됩니다 (마찬가지로 이제) 및 편집 하 고 때 해당 옵션의 드롭다운 목록입니다. 드롭 다운 목록을 사용 하 여, 최종 사용자는 범주와 공급 업체 중에서 선택할 수는 사용할 수 있는 빠르게 확인할 수 있습니다 수 있으며 더 쉽게 선택.

이 동작을 제공 하려면 변환 해야는 `SupplierName` 및 `CategoryName` TemplateFields에 BoundFields 인 `ItemTemplate` 내보냅니다는 `SupplierName` 및 `CategoryName` 값이 고 `EditItemTemplate` 목록에 필요한 DropDownList 컨트롤을 사용 하는 사용 가능한 범주와 공급 업체입니다.

## <a name="adding-thecategoriesandsuppliersdropdownlists"></a>추가`Categories`및`Suppliers`dropdownlist 활용

변환 하 여 시작 된 `SupplierName` 및 `CategoryName` BoundFields 여 TemplateFields에: GridView의 스마트 태그에서 열 편집 링크를 클릭 하면; 왼쪽 아래에 있는 목록에서는 BoundField를 선택 하 고 클릭 하는 "이이 필드로 변환는 TemplateField"링크입니다. 둘 다와 함께 변환 프로세스를 TemplateField 만들어집니다는 `ItemTemplate` 및 `EditItemTemplate`아래 선언적 구문에 나타난 것 처럼:


[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample4.aspx)]

BoundField 읽기 전용으로 표시 된 이후에 모두는 `ItemTemplate` 및 `EditItemTemplate` Label 웹 포함 컨트롤 `Text` 속성 적용 가능한 데이터 필드에 바인딩된 (`CategoryName`, 위 구문에). 수정 해야는 `EditItemTemplate`, DropDownList 컨트롤과 웹 컨트롤을 대체 합니다.

이전 자습서에서 살펴본 대로 템플릿 디자이너를 통해 또는 선언적 구문에서 직접 편집할 수 있습니다. 디자이너를 통해 편집할 GridView의 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 범주 필드를 사용 하도록 선택할 `EditItemTemplate`합니다. 웹 컨트롤을 제거 하 고 DropDownList의 ID 속성을 설정 하는 DropDownList 컨트롤을 대신 `Categories`합니다.


[![텍스트 상자를 제거 하 고는 EditItemTemplate를 DropDownList 추가](customizing-the-data-modification-interface-vb/_static/image14.png)](customizing-the-data-modification-interface-vb/_static/image13.png)

**그림 5**:는 텍스트 상자를 제거 하 고 DropDownList를 추가할는 `EditItemTemplate` ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image15.png))


다음 사용 가능한 범주와 DropDownList를 채우는 해야 합니다. DropDownList의 스마트 태그에서 데이터 소스 선택 링크를 클릭 하 고 라는 새 ObjectDataSource를 만들도록 선택한 `CategoriesDataSource`합니다.


[![CategoriesDataSource 라는 새 ObjectDataSource 컨트롤 만들기](customizing-the-data-modification-interface-vb/_static/image17.png)](customizing-the-data-modification-interface-vb/_static/image16.png)

**그림 6**: 명명 된 새 ObjectDataSource 컨트롤 만들기 `CategoriesDataSource` ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image18.png))


이 ObjectDataSource 모든 범주를 반환 하려면에 바인딩하는 `CategoriesBLL` 클래스의 `GetCategories()` 메서드.


[![ObjectDataSource CategoriesBLL의 GetCategories() 메서드에 바인딩합니다](customizing-the-data-modification-interface-vb/_static/image20.png)](customizing-the-data-modification-interface-vb/_static/image19.png)

**그림 7**: ObjectDataSource를 바인딩하는 `CategoriesBLL`의 `GetCategories()` 메서드 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image21.png))


마지막으로, DropDownList의 설정을 구성 되도록는 `CategoryName` 필드가 각 DropDownList에 표시 될 `ListItem` 와 `CategoryID` 필드의 값으로 사용 합니다.


[![범주 필드를 표시 하 고 값으로 사용 하 여 CategoryID가](customizing-the-data-modification-interface-vb/_static/image23.png)](customizing-the-data-modification-interface-vb/_static/image22.png)

**그림 8**: 있어야는 `CategoryName` 필드의 표시 및 `CategoryID` 값으로 사용 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image24.png))


이러한 변경한 후에 대 한 선언적 태그는 `EditItemTemplate` 에 `CategoryName` TemplateField DropDownList과는 ObjectDataSource를 모두 포함 됩니다.


[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample5.aspx)]

> [!NOTE]
> 에 필요한 DropDownList는 `EditItemTemplate` 뷰 상태의 사용 하도록 설정 되어 있어야 합니다. DropDownList의 선언적 구문을 구문이 추가 곧와 같은 데이터 바인딩 명령은 `Eval()` 및 `Bind()` 뷰 상태가 사용 하도록 설정 하는 컨트롤에만 사용할 수 있습니다.


명명 된 DropDownList를 추가 하려면 다음이 단계를 반복 `Suppliers` 에 `SupplierName` TemplateField의 `EditItemTemplate`합니다. DropDownList를 추가 합니다.이 포함 됩니다는 `EditItemTemplate` 및 다른 ObjectDataSource 만들기. 하지만 `Suppliers` 호출 하도록 구성 해야 DropDownList의 ObjectDataSource는 `SuppliersBLL` 클래스의 `GetSuppliers()` 메서드. 또한 구성 하는 `Suppliers` DropDownList 표시 하는 `CompanyName` 필드를 사용 하 여는 `SupplierID` 필드에 대 한 값으로 해당 `ListItem` s 합니다.

두 개의 dropdownlist 활용을 추가한 후 `EditItemTemplate` s, 브라우저에서 페이지를 로드 하 고 Chef 100 케이준 Seasoning 제품에 대 한 편집 단추를 클릭 합니다. 그림 9에서 볼 수 있듯이 제품의 범주와 공급 업체 열은 사용 가능한 범주 및 공급 업체에서 선택할 수를 포함 하는 드롭다운 목록으로 렌더링 됩니다. 하지만는 *첫 번째* 모두 드롭 다운 목록에서 항목 기본적으로 선택 됩니다 (음료 범주에 대해) 및 삼 화 음료는 공급자로 서 새로운 식품 케이준 제공한 Condiment는 Chef 한 100 케이준 Seasoning 이지만 편리 합니다.


[![드롭다운 목록에서 첫 번째 항목은 기본적으로 선택](customizing-the-data-modification-interface-vb/_static/image26.png)](customizing-the-data-modification-interface-vb/_static/image25.png)

**그림 9**: 드롭 다운 목록에 첫 번째 항목은 기본적으로 선택 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image27.png))


또한 업데이트를 클릭 하면 있습니다 하는 제품의 `CategoryID` 및 `SupplierID` 값으로 설정 되며 `NULL`합니다. 동작 때문에 일반적인 원인은 의도 하지 않은 둘 다에 해당에서 dropdownlist 활용은 `EditItemTemplate` 제품 데이터의 모든 데이터 필드에 s 바인딩되지 않습니다.

## <a name="binding-the-dropdownlists-to-thecategoryidandsupplieriddata-fields"></a>dropdownlist 활용 바인딩는`CategoryID`및`SupplierID`데이터 필드

편집 된 제품의 범주 및 공급 업체를 가지려면 드롭 다운 목록을 적절 한 값으로 및를 BLL의 다시 전송 하는 이러한 값을 설정 `UpdateProduct` dropdownlist 활용 바인딩할 필요 시 업데이트를 클릭 하는 메서드를 `SelectedValue` 속성에는 `CategoryID` 및 `SupplierID` 양방향 데이터 바인딩을 사용 하 여 데이터 필드입니다. 와이를 위해는 `Categories` 추가할 수 있습니다 DropDownList를 `SelectedValue='<%# Bind("CategoryID") %>'` 선언적 구문에 직접 합니다.

또는 DropDownList의 데이터 바인딩 디자이너를 통해 서식 파일을 편집 하 고 DropDownList의 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 하 여 설정할 수 있습니다. 다음으로 나타내는 `SelectedValue` 속성에 각각 바인딩해야는 `CategoryID` 양방향 데이터 바인딩을 사용 하 여 필드 (그림 10 참조). 바인딩할 선언적 또는 디자이너 과정을 반복 하는 `SupplierID` 데이터 필드를 `Suppliers` DropDownList 합니다.


[![CategoryID 양방향 데이터 바인딩을 사용 하 여 DropDownList의 SelectedValue 속성에 바인딩](customizing-the-data-modification-interface-vb/_static/image29.png)](customizing-the-data-modification-interface-vb/_static/image28.png)

**그림 10**: 바인딩하는 `CategoryID` 는 DropDownList를 `SelectedValue` 속성을 사용 하 여 양방향 데이터 바인딩을 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image30.png))


바인딩을에 적용 되 면는 `SelectedValue` 속성 두 dropdownlist 활용의 편집 된 제품의 범주와 공급 업체 열 됩니다의 기본값은 현재 제품의 값입니다. 업데이트를 클릭 하면는 `CategoryID` 및 `SupplierID` 선택한 드롭 다운 목록 항목의 값에 전달 될는 `UpdateProduct` 메서드. 그림 11 데이터 바인딩된 문; 추가한 후에 자습서를 보여 줍니다. note Chef 한 100 케이준 Seasoning에 대 한 선택 된 드롭 다운 목록 항목와 되는 방식 올바르게 Condiment 새로 식품 케이준 편리 합니다.


[![기본적으로 선택 되어 편집할 제품의 현재 범주와 공급 업체 값](customizing-the-data-modification-interface-vb/_static/image32.png)](customizing-the-data-modification-interface-vb/_static/image31.png)

**그림 11**: The 편집할 제품의 현재 범주와 공급 업체 값은 기본적으로 선택 됩니다 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image33.png))


## <a name="handlingnullvalues"></a>처리`NULL`값

`CategoryID` 및 `SupplierID` 열에는 `Products` 테이블 일 수 있습니다 `NULL`, 아직에 dropdownlist 활용은 `EditItemTemplate` s를 나타내는 목록 항목을 포함 하지 않습니다는 `NULL` 값입니다. 이 두 개의 결과.

- 사용자가 아닌에서 제품의 범주 또는 공급자를 변경 하려면이 인터페이스를 사용할 수 없습니다`NULL` 값을 한 `NULL` 하나
- 제품에는 `NULL` `CategoryID` 또는 `SupplierID`, 예외 편집 단추를 클릭 하면 표시 됩니다. ¿¡´는 `NULL` 에서 반환 된 값 `CategoryID` (또는 `SupplierID`)에 `Bind()` 문을 드롭다운 목록에 있는 값에 매핑되지 않는 (DropDownList 예외를 throw 때 해당 `SelectedValue` 값속성*하지* 목록 항목의 컬렉션에서).

지원 하기 위해 `NULL` `CategoryID` 및 `SupplierID` 값을 추가 해야 다른 `ListItem` 를 나타내는 각 DropDownList를는 `NULL` 값입니다. 에 [마스터/세부 정보 필터링 된 정도 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) 자습서, 추가 추가 하는 방법에 살펴보았습니다 `ListItem` DropDownList 데이터 바인딩된은 관련에 필요한 DropDownList의 설정 `AppendDataBoundItems` 속성을 `True` 및 수동으로 추가 하는 추가 `ListItem`합니다. 그러나 해당 이전 자습서의 추가 `ListItem` 와 `Value` 의 `-1`합니다. 그러나 asp.net에서는 데이터 바인딩에서 논리를 빈 문자열을 자동으로 변환 된 `NULL` 값과는 반대로 합니다. 따라서이 자습서에 대 한 원하는 `ListItem`의 `Value` 빈 문자열 이어야 합니다.

두 dropdownlist 활용을 설정 하 여 시작 `AppendDataBoundItems` 속성을 `True`합니다. 다음으로 추가 된 `NULL` `ListItem` 추가 하 여 `<asp:ListItem>` 요소 각 DropDownList 선언적 태그 표시 되도록 같은:


[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample6.aspx)]

필자 "(None)"를 사용 하 여 텍스트 값으로이 `ListItem`, 하지만 원하는 경우에 빈 문자열 수도를 변경할 수 있습니다.

> [!NOTE]
> 설명한 것 처럼는 *마스터/세부 정보 필터링 된 정도 DropDownList* 자습서 `ListItem` s는 DropDownList를 클릭 하 여 디자이너를 통해 DropDownList에 추가할 수 `Items` 속성 창에서 속성 ( ½ ֳ µ는 `ListItem` 컬렉션 편집기). 그러나 추가 해야는 `NULL` `ListItem` 선언적 구문을 통해이 자습서에 대 한 합니다. 사용 하는 경우는 `ListItem` 생성 된 선언적 구문에서 생략 됩니다 컬렉션 편집기는 `Value` 같은 선언적 태그가 만드는 빈 문자열로 지정 된 경우 설정을 모두: `<asp:ListItem>(None)</asp:ListItem>`합니다. 누락 값 해 보일 수 있습니다, 에서도 DropDownList를 사용 하 여이 인해는 `Text` 그 자리에 속성 값입니다. 즉, 되는 경우가 `NULL` `ListItem` 은 선택 "(None)" 값을 시도에 할당 될는 `CategoryID`, 되 고 예외가 만들어집니다. 명시적으로 설정 하 여 `Value=""`, `NULL` 값에 할당할 `CategoryID` 때는 `NULL` `ListItem` 을 선택 합니다.


Suppliers 드롭다운 목록에 대 한 이러한 단계를 반복 합니다.

이 추가 `ListItem`, 편집 인터페이스 이제 할당할 수 `NULL` 값을 특정 제품에 `CategoryID` 및 `SupplierID` 그림 12에 표시 된 대로 필드입니다.


[![제품의 범주 또는 공급 업체에 대해 NULL 값을 할당 하려면 (없음)을 선택 합니다.](customizing-the-data-modification-interface-vb/_static/image35.png)](customizing-the-data-modification-interface-vb/_static/image34.png)

**그림 12**: 할당 (없음) 선택 된 `NULL` 제품의 범주 또는 공급 업체에 대 한 값 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image36.png))


## <a name="step-4-using-radiobuttons-for-the-discontinued-status"></a>4 단계: 지원 되지 않는 상태에 대 한 라디오 단추를 사용 하 여

현재 제품 `Discontinued` 데이터 필드는 읽기 전용 행에 대 한 비활성화 된 확인란 및 편집 되는 행에 대 한 활성화는 확인란을 렌더링 하는 CheckBoxField를 사용 하 여 표현 됩니다. 이 사용자 인터페이스에 적합 한 종종 상태인 동안에서는 사용자 지정할 수를 TemplateField를 사용 하 여 필요한 경우. 이 자습서에서는 바꿔보겠습니다 CheckBoxField 제품의 사용자 지정할 수 있는 두 가지 옵션을 "활성" 및 "중단" RadioButtonList 컨트롤을 사용 하는 TemplateField로 `Discontinued` 값입니다.

변환 하 여 시작 된 `Discontinued` CheckBoxField와 TemplateField 만드는 TemplateField로는 `ItemTemplate` 및 `EditItemTemplate`합니다. 두 템플릿에 있는 확인란을 포함 해당 `Checked` 속성에 바인딩된는 `Discontinued` 데이터 필드를 하 되 고 둘 사이의 유일한 차이점은 `ItemTemplate`의 확인란의 `Enabled` 속성이로 설정 된 `False`합니다.

확인란을 모두 대체는 `ItemTemplate` 및 `EditItemTemplate` RadioButtonList 컨트롤과 두 RadioButtonLists' 설정 `ID` 속성을 `DiscontinuedChoice`합니다. 다음으로 RadioButtonLists 해야 각각 포함 된 두 개의 라디오 단추, 레이블 지정 된 "활성" 값이 "False" 및 "중단" 레이블이 지정 된 하나를 나타내는 값이 "True"입니다. 입력 하거나이를 위해는 `<asp:ListItem>` 선언적 구문 또는 사용을 통해 직접의 요소는 `ListItem` 디자이너에서 컬렉션 편집기입니다. 그림 13은는 `ListItem` 두 라디오 단추 옵션 후 컬렉션 편집기를 지정 합니다.


[![활성 상태이 고 지원 되지 않는 옵션을 RadioButtonList 추가](customizing-the-data-modification-interface-vb/_static/image38.png)](customizing-the-data-modification-interface-vb/_static/image37.png)

**그림 13**: 활성 추가 및 RadioButtonList에 지원 되지 않는 옵션 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image39.png))


RadioButtonList 이후는 `ItemTemplate` 편집 가능 되지 않아야 설정 해당 `Enabled` 속성을 `False`를 `Enabled` 속성을 `True` (기본값)에서 RadioButtonList에 대 한는 `EditItemTemplate`합니다. 읽기 전용으로 비 편집할 행에서 라디오 단추를 만드는 사용자 편집된 된 행에 대 한 RadioButton 값을 변경할 수 있지만.

RadioButtonList 컨트롤의 할당을 계속 합니다 `SelectedValue` 제품에 따라 적절 한 라디오 단추가 선택 되어 있도록 속성 `Discontinued` 데이터 필드입니다. 이 자습서의 앞부분에 나오는 검사 dropdownlist 활용와 마찬가지로이 구문이 하거나 추가할 수 있습니다 선언 태그에 직접 또는 RadioButtonLists의 스마트 태그에 데이터 바인딩 편집 링크를 통해.

두 개의 RadioButtonLists를 추가 하 고, 구성 후의 `Discontinued` TemplateField의 선언적 태그와 같습니다.


[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample7.aspx)]

이러한 변경 내용으로는 `Discontinued` 열의 라디오 단추 쌍 (그림 14 참조)의 목록에 확인란이 선택 목록에서 변환 된 합니다. 제품을 편집할 때 적절 한 라디오 단추가 선택 되 고 다른 라디오 단추를 선택 하 고 업데이트를 클릭 하 여 제품의 지원 되지 않는 상태를 업데이트할 수 있습니다.


[![지원 되지 않는 확인란 라디오 단추 쌍에 의해 대체 되었습니다.](customizing-the-data-modification-interface-vb/_static/image41.png)](customizing-the-data-modification-interface-vb/_static/image40.png)

**그림 14**: The 지원 되지 않는 확인란으로 바뀌는 라디오 단추 쌍 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image42.png))


> [!NOTE]
> 이후는 `Discontinued` 열에는 `Products` 데이터베이스 가질 수 없습니다 `NULL` 값에서는 필요가 없습니다 캡처에 대 한 걱정 `NULL` 인터페이스에 대 한 정보입니다. 그러나 If, `Discontinued` 열 포함 될 수 `NULL` 값 세 번째 추가 하려는 라디오 단추를 사용 하 여 목록 해당 `Value` 빈 문자열로 설정 (`Value=""`) 마찬가지로 된 범주와 공급 업체 dropdownlist 활용 합니다.


## <a name="summary"></a>요약

BoundField 및 CheckBoxField 자동으로 읽기 전용, 편집 및 삽입 인터페이스를 렌더링 하는 동안 사용자 지정 기능이 부족 합니다. 종종 하지만 해야를 편집 하는 인터페이스를 삽입 하거나 사용자 지정할 수 아마도 (이전 자습서에서 확인)에 따라 유효성 검사 컨트롤을 추가 하거나 (보았듯이이 자습서에서는) 데이터 수집 사용자 인터페이스 사용자 지정 하 여 합니다. 인터페이스를 TemplateField와 사용자 지정 합계를 계산할 수 다음 단계에:

1. TemplateField를 추가 하거나 기존 BoundField 또는 CheckBoxField를 TemplateField로 변환
2. 인터페이스를 확장 하 여 필요에 따라
3. 양방향 데이터 바인딩을 사용 하 여 새로 추가 된 웹 컨트롤에 적절 한 데이터 필드 바인딩

기본 제공 ASP.NET 웹 컨트롤을 사용 하는 것 외에도 사용자 정의 컴파일된 서버 컨트롤 및 사용자 정의 컨트롤 TemplateField 템플릿을 사용자 지정할 수도 있습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
> [다음](implementing-optimistic-concurrency-vb.md)
