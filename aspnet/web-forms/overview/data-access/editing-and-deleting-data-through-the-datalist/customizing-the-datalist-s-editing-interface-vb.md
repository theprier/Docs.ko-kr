---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-vb
title: DataList를 사용자 지정의 편집 인터페이스 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 Dropdownlist 및 CheckBox를 포함 하는 DataList에 대 한 다양 한 편집 인터페이스를 만들겠습니다.
ms.author: aspnetcontent
ms.date: 10/30/2006
ms.assetid: 718628e2-224c-455f-b33a-a41efd48d5a0
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 78001e977a4696e905317eab35604518d059e66d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37828759"
---
<a name="customizing-the-datalists-editing-interface-vb"></a>DataList의 편집 인터페이스 (VB)를 사용자 지정
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_40_VB.exe) 또는 [PDF 다운로드](customizing-the-datalist-s-editing-interface-vb/_static/datatutorial40vb1.pdf)

> 이 자습서에서는 Dropdownlist 및 CheckBox를 포함 하는 DataList에 대 한 다양 한 편집 인터페이스를 만들겠습니다.


## <a name="introduction"></a>소개

태그 및 DataList s의에서 웹 컨트롤 `EditItemTemplate` 해당 편집 가능한 인터페이스를 정의 합니다. 모든 편집 가능한 DataList 예제에서에서는 ve 편집 가능한 지금 검사 텍스트 웹 컨트롤 인터페이스에 구성 되었습니다. 에 [이전 자습서](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md) 유효성 검사 컨트롤을 추가 하 여 편집 사용자 환경을 개선 했습니다.

`EditItemTemplate` 고 Dropdownlist, RadioButtonLists, 일정 같은 텍스트 이외의 웹 컨트롤을 포함 하도록 확장할 수 있습니다. 텍스트 상자에 다른 웹 컨트롤을 포함 하도록 편집 인터페이스 사용자 지정 하는 경우에서와 마찬가지로 다음 단계를 사용 합니다.

1. 웹 컨트롤을 추가 합니다 `EditItemTemplate`합니다.
2. 데이터 바인딩 구문을 사용 하 여 해당 속성에 해당 데이터 필드 값을 할당 합니다.
3. 에 `UpdateCommand` 이벤트 처리기를 프로그래밍 방식으로 웹 액세스 값을 제어 하 고 해당 BLL 메서드에 전달 합니다.

이 자습서에서는 Dropdownlist 및 CheckBox를 포함 하는 DataList에 대 한 다양 한 편집 인터페이스를 만들겠습니다. 특히, 제품 정보를 나열 하 고 s 제품 이름, 공급 업체, 범주 및 지원 되지 않는 상태 업데이트를 허용 하는 DataList를 만들겠습니다 (그림 1 참조).


[![TextBox, Dropdownlist 두 및 CheckBox 편집 인터페이스 포함](customizing-the-datalist-s-editing-interface-vb/_static/image2.png)](customizing-the-datalist-s-editing-interface-vb/_static/image1.png)

**그림 1**: TextBox, Dropdownlist 두 및 CheckBox 편집 인터페이스에 포함 되어 있습니다 ([큰 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image3.png))


## <a name="step-1-displaying-product-information"></a>1 단계: 제품 정보를 표시합니다.

DataList s 편집할 수 있는 인터페이스를 만들 수 있습니다, 전에 먼저 읽기 전용 인터페이스를 작성 해야 합니다. 열어서 시작 합니다 `CustomizedUI.aspx` 에서 페이지를 `EditDeleteDataList` 폴더 디자이너에서 페이지로 DataList 추가 설정 및 해당 `ID` 속성을 `Products`입니다. DataList s 스마트 태그에서 새 ObjectDataSource를 만듭니다. 이름을 새 ObjectDataSource `ProductsDataSource` 에서 데이터를 검색 하도록 구성 하는 `ProductsBLL` s 클래스 `GetProducts` 메서드. 로 이전 편집 가능한 DataList 자습서를 사용 하 여 업데이트 편집된 제품의 정보는 비즈니스 논리 계층으로 직접 이동 하 여. 그에 따라 삽입, 업데이트, 드롭 다운 목록을 설정 하 고 탭 (없음)을 삭제 합니다.


[![(없음)을 업데이트, 삽입 및 삭제 탭 드롭 다운 목록 설정](customizing-the-datalist-s-editing-interface-vb/_static/image5.png)](customizing-the-datalist-s-editing-interface-vb/_static/image4.png)

**그림 2**: (없음)로 업데이트, 삽입 및 탭 드롭다운 목록이 삭제를 설정 ([큰 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image6.png))


ObjectDataSource를 구성한 후 Visual Studio 기본값 만들어집니다 `ItemTemplate` 각 데이터 필드에 대 한 이름 및 값을 나열 하는 DataList 반환 합니다. 수정 된 `ItemTemplate` 서식 파일에 해당 제품 이름이 표시 되도록는 `<h4>` 범주 이름, 공급 업체 이름, 가격 및 지원 되지 않는 상태와 함께 요소입니다. 또한 지도록 하 고 있는 편집 단추를 추가 해당 `CommandName` 속성을 편집으로 설정 합니다. 에 대 한 선언적 태그 내 `ItemTemplate` 따릅니다.


[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample1.aspx)]

위의 태그를 사용 하 여 제품 정보 레이아웃을 &lt;h4&gt; s 제품 이름 및 네 개의 열에 대 한 제목 `<table>` 나머지 필드에 대 한 합니다. 합니다 `ProductPropertyLabel` 하 고 `ProductPropertyValue` 에 정의 된 CSS 클래스를 `Styles.css`, 이전 자습서에서 설명 했습니다. 그림 3에서는 브라우저를 통해 볼 때 진행 상황을 보여 줍니다.


[![이름, 공급 업체, 범주, 지원 되지 않는 상태 및 각 제품의 가격이 표시 됩니다.](customizing-the-datalist-s-editing-interface-vb/_static/image8.png)](customizing-the-datalist-s-editing-interface-vb/_static/image7.png)

**그림 3**: 표시 되는 이름, 공급 업체, 범주, 지원 되지 않는 상태 및 각 제품의 가격 ([큰 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image9.png))


## <a name="step-2-adding-the-web-controls-to-the-editing-interface"></a>2 단계: 웹 컨트롤을 편집 인터페이스에 추가

편집 인터페이스에 필요한 웹 컨트롤을 추가 하는 사용자 지정된 DataList를 빌드하는 첫 번째 단계는 `EditItemTemplate`합니다. 특히, DropDownList 범주에 다른 공급자 및 지원 되지 않는 상태에 대 한 확인란 필요합니다. 제품의 가격,이 예제에서 편집할 수 아니므로 레이블 웹 컨트롤을 사용 하 여 표시 계속 수 있습니다.

편집 인터페이스를 사용자 지정 하려면 DataList s 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 선택 된 `EditItemTemplate` 드롭 다운 목록에서 옵션입니다. DropDownList를 추가 합니다 `EditItemTemplate` 설정 및 해당 `ID` 에 `Categories`입니다.


[![DropDownList 범주에 대 한 추가](customizing-the-datalist-s-editing-interface-vb/_static/image11.png)](customizing-the-datalist-s-editing-interface-vb/_static/image10.png)

**그림 4**: DropDownList 범주에 대 한 추가 ([큰 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image12.png))


다음으로, DropDownList s 스마트 태그에서 데이터 소스 선택 옵션을 만들고 라는 새로운 ObjectDataSource는 `CategoriesDataSource`합니다. 이 ObjectDataSource를 사용 하 여 구성 합니다 `CategoriesBLL` s 클래스 `GetCategories()` 메서드 (그림 5 참조). 다음으로, DropDownList의 데이터 소스 구성 마법사는 각에 사용할 데이터 필드에 대 한을 프롬프트 `ListItem` s `Text` 고 `Value` 속성입니다. DropDownList을 표시 합니다 `CategoryName` 데이터 필드와 사용을 `CategoryID` 그림 6 에서처럼 값으로.


[![CategoriesDataSource 라는 새로운 ObjectDataSource는 만들기](customizing-the-datalist-s-editing-interface-vb/_static/image14.png)](customizing-the-datalist-s-editing-interface-vb/_static/image13.png)

**그림 5**: 명명 된 새 ObjectDataSource 만들려면 `CategoriesDataSource` ([클릭 하 여 큰 이미지 보기](customizing-the-datalist-s-editing-interface-vb/_static/image15.png))


[![DropDownList의 표시를 구성 하 고 필드 값](customizing-the-datalist-s-editing-interface-vb/_static/image17.png)](customizing-the-datalist-s-editing-interface-vb/_static/image16.png)

**그림 6**: DropDownList의 표시 및 값 필드 구성 ([큰 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image18.png))


이 일련의 공급 업체에 대 한 DropDownList를 만드는 단계를 반복 합니다. 설정 합니다 `ID` 이 DropDownList를에 대 한 `Suppliers` 하 고 해당 ObjectDataSource 이름을 `SuppliersDataSource`입니다.

Dropdownlist 두를 추가한 후 지원 되지 않는 상태에 대 한 확인란 및 제품의 이름에 대 한 텍스트를 추가 합니다. 설정 된 `ID` 확인란 및 텍스트 상자 `Discontinued` 및 `ProductName`각각. 사용자가의 제품 이름에 대 한 값을 제공 하는지 확인 하려면 RequiredFieldValidator를 추가 합니다.

마지막으로, 업데이트 및 취소 단추를 추가 합니다. 이러한 두 단추에 대 한 것을 기억 하는 해당 `CommandName` 속성 업데이트 하 고 취소를 각각 설정 됩니다.

자유롭게 원하는 편집 인터페이스를 레이아웃할 수 있습니다. I ve 네 개의 열과 사용 하기로 `<table>` 스크린 샷 선언적 구문을와 읽기 전용 인터페이스에서 레이아웃을 보여 줍니다.


[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample2.aspx)]


[![편집 인터페이스는 읽기 전용 인터페이스와 같은 아웃 배치](customizing-the-datalist-s-editing-interface-vb/_static/image20.png)](customizing-the-datalist-s-editing-interface-vb/_static/image19.png)

**그림 7**: 읽기 전용 인터페이스와 같은 아웃 배치의 편집 인터페이스는 ([큰 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image21.png))


## <a name="step-3-creating-the-editcommand-and-cancelcommand-event-handlers"></a>3 단계: EditCommand 및 CancelCommand 이벤트 처리기 만들기

현재 방법이 없는 데이터 바인딩 구문을 합니다 `EditItemTemplate` (제외 하 고는 `UnitPriceLabel`는 정확 하 게에서 복사를 `ItemTemplate`). 데이터 바인딩 구문을 일시적으로 추가 되지만 첫 번째 let s DataList s에 대 한 이벤트 처리기를 만들 `EditCommand` 고 `CancelCommand` 이벤트입니다. 이전에 설명한 대로의 책임을 `EditCommand` 반면 해당 편집 단추가 클릭 되었으며, DataList 항목에 대 한 편집 인터페이스를 렌더링 하는 이벤트 처리기는 `CancelCommand`의 작업은 DataList를 미리 편집 상태로 돌아갑니다.

이러한 두 이벤트 처리기를 만들고 다음 코드를 사용 하도록 합니다.


[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample3.vb)]

이러한 두 명의 이벤트 처리기 위치에 편집 단추를 클릭 하면 편집 인터페이스를 표시 하 고 읽기 전용 모드로 편집된 된 항목을 반환 취소 단추를 클릭 합니다. 그림 8에서는 Chef 한 100 s 수프 편집 버튼을 클릭 한 후 DataList를 보여 줍니다. 이후로 ve 모든 데이터 바인딩 구문을 편집 인터페이스에 추가 하는 `ProductName` 텍스트 상자가 비어를 `Discontinued` 에서 확인란을 선택 취소 하 고 첫 번째 항목을 선택 합니다 `Categories` 및 `Suppliers` Dropdownlist.


[![편집 인터페이스의 편집 단추 표시를 클릭합니다.](customizing-the-datalist-s-editing-interface-vb/_static/image23.png)](customizing-the-datalist-s-editing-interface-vb/_static/image22.png)

**그림 8**: 편집 인터페이스 표시 [편집] 단추 ([큰 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image24.png))


## <a name="step-4-adding-the-databinding-syntax-to-the-editing-interface"></a>4 단계: 편집 인터페이스에 데이터 바인딩 구문을 추가

가 현재 제품의 값을 표시 하는 편집 인터페이스에 데이터 바인딩 구문을 사용 하 여 적절 한 웹 컨트롤 값에 데이터 필드 값을 할당 해야 합니다. 데이터 바인딩 구문을 템플릿 편집 화면으로 이동 하 여 디자이너를 통해 적용할 수 있으며 스마트 태그를 제어 하는 웹에서 데이터 바인딩 편집 링크를 선택 합니다. 또는 데이터 바인딩 구문은 선언적 태그에 직접 추가할 수 있습니다.

할당를 `ProductName` 데이터 필드 값을는 `ProductName` s 텍스트 상자에 붙여넣습니다 `Text` 속성을 `CategoryID` 및 `SupplierID` 데이터 필드 값을를 `Categories` 및 `Suppliers` Dropdownlist `SelectedValue` 속성 및 `Discontinued` 데이터 필드에 값을 `Discontinued` 확인란 `Checked` 속성. 디자이너 또는 선언적 태그를 통해 직접 이러한 변경을 수행한 후 브라우저를 통해 페이지를 다시 방문 하 고 Chef 한 100의 수프에 대 한 편집 단추를 클릭 합니다. 그림 9에서 알 수 있듯이, 데이터 바인딩 구문을 텍스트 상자, Dropdownlist, 및 확인란에 현재 값을 추가 했습니다.


[![편집 인터페이스의 편집 단추 표시를 클릭합니다.](customizing-the-datalist-s-editing-interface-vb/_static/image26.png)](customizing-the-datalist-s-editing-interface-vb/_static/image25.png)

**그림 9**: 편집 인터페이스 표시 [편집] 단추 ([큰 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image27.png))


## <a name="step-5-saving-the-user-s-changes-in-the-updatecommand-event-handler"></a>5 단계: UpdateCommand 이벤트 처리기에서 사용자가 변경 내용을 저장

사용자 제품을 편집 하 고 포스트백이 발생할 [업데이트] 단추를 클릭 하는 경우 및 s DataList `UpdateCommand` 이벤트가 발생 합니다. 이벤트 처리기를 해야의 웹 컨트롤에서 값을 읽는 `EditItemTemplate` 및 데이터베이스에 제품 업데이트 하려면 BLL 사용 하 여 인터페이스입니다. 것으로 ve 이전 자습서에 표시 합니다 `ProductID` 업데이트 된 제품의를 통해 액세스할 수는 `DataKeys` 컬렉션입니다. 사용자가 입력 한 필드를 사용 하 여 웹 컨트롤을 프로그래밍 방식으로 참조 하 여 액세스 `FindControl("controlID")`처럼 다음 코드를 보여 줍니다.


[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample4.vb)]

코드를 참조 하 여 시작 합니다 `Page.IsValid` 속성 페이지에서 모든 유효성 검사 컨트롤 유효 하도록 합니다. 경우 `Page.IsValid` 는 `True`, 편집된 제품 s `ProductID` 에서 값을 읽은 `DataKeys` 컬렉션과 웹 컨트롤에서 데이터 항목은 `EditItemTemplate` 프로그래밍 방식으로 참조 됩니다. 다음에 전달 되는 적절 한 변수로 이러한 웹 컨트롤에서 값을 읽은 다음으로, `UpdateProduct` 오버 로드 합니다. 데이터를 업데이트 한 후 DataList 미리 편집 상태로 반환 됩니다.

> [!NOTE]
> I ve 예외 처리에 추가 하는 논리를 생략 합니다 [처리 BLL 및 DAL 수준의 예외](handling-bll-and-dal-level-exceptions-vb.md) 코드 및이 예제를 유지 하기 위해 자습서 초점을 맞춘 합니다. 연습으로이 자습서를 완료 한 후이 기능을 추가 합니다.


## <a name="step-6-handling-null-categoryid-and-supplierid-values"></a>6 단계: NULL CategoryID 및 SupplierID 값 처리

Northwind 데이터베이스에 대 한 허용 `NULL` 에 대 한 값을 `Products` 테이블 s `CategoryID` 및 `SupplierID` 열입니다. 그러나이 편집 인터페이스 만들어지고 t 수용 현재 `NULL` 값입니다. 가 있는 제품을 편집 하려고 하는 경우는 `NULL` 값 중 하나에 대 한 해당 `CategoryID` 또는 `SupplierID` 드리겠습니다 열은 `ArgumentOutOfRangeException` 유사한 오류 메시지와 함께: *'범주'에 잘못 된 수행 하기 때문에 SelectedValue 항목의 목록에 없습니다.* 또한 있는 s 현재 s 제품 범주 또는 공급 업체를 변경할 수 없으므로 값에서 비-`NULL` 값을 `NULL` 하나입니다.

지원 하기 위해 `NULL` category와 supplier Dropdownlist에 대 한 값을 추가 해야 추가 `ListItem`합니다. 있나요 ve (없음)으로 사용 하기로 합니다 `Text` 값이 `ListItem`, d 원하는 경우 (예: 빈 문자열) 다른 것으로 변경할 수 있습니다. 마지막으로 Dropdownlist를 설정 해야 `AppendDataBoundItems` 하 `True`suppliers DropDownList에 바인딩된 정적으로 추가 덮어씁니다. 이렇게 하려면 범주를 잊었거나 경우; `ListItem`합니다.

DataList의 Dropdownlist 태그 이러한 변경을 수행한 후 `EditItemTemplate` 다음과 유사 합니다.


[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample5.aspx)]

> [!NOTE]
> 정적 `ListItem`의 DropDownList 디자이너 또는 선언적 구문을 통해 직접 추가할 수 있습니다. 데이터베이스를 나타내는 DropDownList 항목을 추가할 때 `NULL` 값을 추가 해야 합니다 `ListItem` 선언적 구문을 통해. 사용 하는 경우는 `ListItem` 생성 된 선언적 구문에서 생략 됩니다 디자이너에서 컬렉션 편집기를 `Value` 와 같은 선언적 태그를 만들 빈 문자열로 할당 된 경우 설정을 완전히: `<asp:ListItem>(None)</asp:ListItem>`합니다. 이 문제가 보일 수 있지만 누락 `Value` DropDownList를 사용 하면는 `Text` 해당 위치에서 속성 값입니다. 즉, 해당 경우가 `NULL` `ListItem` 는 선택 값 (None) 하려고 product 데이터 필드에 할당할 (`CategoryID` 또는 `SupplierID`,이 자습서에서는), 예외가 만들어집니다. 명시적으로 설정 하 여 `Value=""`, `NULL` 제품에 값을 할당할 경우 데이터 필드를 `NULL` `ListItem` 을 선택 합니다.


시간을 내어 브라우저를 통해 진행 상황을 확인 합니다. 제품을 편집할 때는 유의 합니다 `Categories` 및 `Suppliers` Dropdownlist 두 (없음)가 DropDownList의 시작 옵션입니다.


[![범주 및 공급 업체 Dropdownlist 포함 (None) 옵션](customizing-the-datalist-s-editing-interface-vb/_static/image29.png)](customizing-the-datalist-s-editing-interface-vb/_static/image28.png)

**그림 10**: 합니다 `Categories` 하 고 `Suppliers` Dropdownlist를 포함 하는 (없음) 옵션 ([클릭 하 여 큰 이미지 보기](customizing-the-datalist-s-editing-interface-vb/_static/image30.png))


데이터베이스 옵션 (없음)을 저장할 `NULL` 값을 반환 해야 하는 `UpdateCommand` 이벤트 처리기입니다. 변경 합니다 `categoryIDValue` 하 고 `supplierIDValue` 변수를 null 허용 정수 여야 하 고 할당할 값 이외의 `Nothing` 경우에만 DropDownList의 `SelectedValue` 빈 문자열이 아닙니다:


[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample6.vb)]

값이이 변경으로 `Nothing` 에 전달 될 합니다 `UpdateProduct` BLL 메서드는 사용자 (없음)를 선택한 경우에 해당 하는 드롭다운 목록에서 옵션을 `NULL` 데이터베이스 값.

## <a name="summary"></a>요약

이 자습서에서는 텍스트 상자, Dropdownlist 두 및 유효성 검사 컨트롤과 함께 확인란 세 가지 다른 입력된 웹 컨트롤을 포함 하는 더 복잡 한 DataList 편집 인터페이스를 만드는 방법에 살펴보았습니다. 단계는 사용 중인 웹 컨트롤에 관계 없이 동일 하 게 편집 인터페이스를 작성할 때: DataList s 웹 컨트롤을 추가 하 여 시작 `EditItemTemplate`; 데이터 바인딩 구문을 사용 하 여 해당 하는 웹을 사용 하 여 해당 데이터 필드 값 할당 컨트롤 속성 `UpdateCommand` 이벤트 처리기를 웹 컨트롤 및 BLL에 해당 값을 전달 하는 적절 한 속성을 프로그래밍 방식으로 액세스 합니다.

여부 편집 인터페이스를 만들 때 해당 s 텍스트 상자 또는 다른 웹 컨트롤의 컬렉션만의 구성, 데이터베이스를 올바르게 처리 하도록 `NULL` 값입니다. 고려 하는 경우 `NULL` 개이면 반드시만 잘못 표시할 수 있는 기존 `NULL` 으로 값을 표시 하기 위한 수단을 제공 하는 값의 편집 인터페이스 뿐만 아니라는 `NULL`합니다. DataLists에서 Dropdownlist에 대 한 즉, 일반적으로 정적 추가 `ListItem` 해당 `Value` 속성이 빈 문자열을 명시적으로 설정 됩니다 (`Value=""`), 약간의 코드를 추가 하 고는 `UpdateCommand` 결정 하는 이벤트 처리기 여부는 `NULL``ListItem` 선택 되었습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Dennis Patterson, David Suru 및 Randy Schmidt 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md)
