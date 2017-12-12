---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-vb
title: "DataList 사용자 지정의 편집 인터페이스 (VB) | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 DataList dropdownlist 활용 하 고 확인란을 포함 하는 대 한 보다 다양 한 편집 인터페이스를 만듭니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/30/2006
ms.topic: article
ms.assetid: 718628e2-224c-455f-b33a-a41efd48d5a0
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: bd31c18b9fced12feeda8ca8dea7dace0ef63573
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="customizing-the-datalists-editing-interface-vb"></a>DataList의 편집 인터페이스 (VB) 사용자 지정
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_40_VB.exe) 또는 [PDF 다운로드](customizing-the-datalist-s-editing-interface-vb/_static/datatutorial40vb1.pdf)

> 이 자습서에서는 DataList dropdownlist 활용 하 고 확인란을 포함 하는 대 한 보다 다양 한 편집 인터페이스를 만듭니다.


## <a name="introduction"></a>소개

태그 및 DataList s에서에서 웹 컨트롤 `EditItemTemplate` 의 편집 가능한 인터페이스를 정의 합니다. 모든 편집 가능한 DataList 예제에서 우리 했습니다 편집 가능한 지금까지 검사할 TextBox 웹 컨트롤로 인터페이스에 구성 되었습니다. 에 [이전 자습서](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md) 유효성 검사 컨트롤을 추가 하 여 편집 시간 사용자 환경을 개선 했습니다.

`EditItemTemplate` 고 dropdownlist 활용, RadioButtonLists, 일정과 같은 텍스트 이외의 다른 웹 컨트롤을 포함 하도록 확장할 수 있습니다. 입력란, 다른 웹 컨트롤을 포함 하도록 편집 하는 인터페이스를 사용자 지정할 때와 마찬가지로 다음 단계를 사용 합니다.

1. 웹 컨트롤을 추가 `EditItemTemplate`합니다.
2. 적절 한 속성에 해당 데이터 필드 값을 할당할 databinding 구문을 사용 합니다.
3. 에 `UpdateCommand` 이벤트 처리기를 프로그래밍 방식으로 웹 액세스 값을 제어 하 고 적절 한 BLL 메서드에 전달 합니다.

이 자습서에서는 DataList dropdownlist 활용 하 고 확인란을 포함 하는 대 한 보다 다양 한 편집 인터페이스를 만듭니다. 특히, 제품 정보를 나열 하 고 s 제품 이름, 공급 업체, 범주 및 중단 된 상태 업데이트를 허용 하는 DataList를 만들겠습니다 (그림 1 참조).


[![TextBox, 두 개의 dropdownlist 활용 및 CheckBox 편집 인터페이스 포함](customizing-the-datalist-s-editing-interface-vb/_static/image2.png)](customizing-the-datalist-s-editing-interface-vb/_static/image1.png)

**그림 1**: TextBox, 두 개의 dropdownlist 활용 및 CheckBox 편집 인터페이스 포함 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image3.png))


## <a name="step-1-displaying-product-information"></a>1 단계: 제품 정보를 표시합니다.

DataList s 편집 가능한 인터페이스를 만들 수 있습니다, 전에 먼저 읽기 전용 인터페이스를 작성 해야 합니다. 열어 시작는 `CustomizedUI.aspx` 에서 페이지는 `EditDeleteDataList` 폴더 및 설정 DataList의 페이지를 추가, 디자이너에서 해당 `ID` 속성을 `Products`합니다. DataList s 스마트 태그에서 새 ObjectDataSource를 만듭니다. 이 새 ObjectDataSource 이름을 `ProductsDataSource` 에서 데이터를 검색 하도록 구성 하는 `ProductsBLL` s 클래스 `GetProducts` 메서드. 로 이전 편집 가능한 DataList 자습서와 업데이트 하는 편집 된 제품의 정보는 비즈니스 논리 계층으로 직접 이동 하 여. 적절 하 게 삽입, 업데이트에서 드롭 다운 목록을 설정 하 고 각 탭 (없음)을 삭제 합니다.


[![UPDATE, INSERT 및 DELETE 탭 드롭 다운 목록을 (없음)으로 설정](customizing-the-datalist-s-editing-interface-vb/_static/image5.png)](customizing-the-datalist-s-editing-interface-vb/_static/image4.png)

**그림 2**: (None)로 업데이트, 삽입 및 삭제 탭 드롭 다운 목록 설정 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image6.png))


Visual Studio는 기본은 ObjectDataSource를 구성한 후 만듭니다 `ItemTemplate` DataList의 각 데이터 필드에 대 한 이름 및 값을 나열 하는 반환 합니다. 수정 된 `ItemTemplate` 서식 파일에서 제품 이름을 나열 하는 `<h4>` 범주 이름, 공급 업체 이름, 가격 및 중단 된 상태와 함께 요소입니다. 또한 지도록 하 고 있는 편집 단추를 추가 해당 `CommandName` 속성을 편집으로 설정 합니다. 에 대 한 선언적 태그 내 `ItemTemplate` 따릅니다.


[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample1.aspx)]

위의 태그를 사용 하 여 제품 정보 레이아웃는 &lt;h4&gt; s 제품 이름 및 4 개 열에 대 한 제목 `<table>` 나머지 필드에 대 한 합니다. `ProductPropertyLabel` 및 `ProductPropertyValue` 에 정의 된 CSS 클래스 `Styles.css`, 이전 자습서에서 설명 했습니다. 그림 3에서는 브라우저를 통해 볼 때 진행률을 보여 줍니다.


[![표시 되는 이름, 공급 업체, 범주, 지원 되지 않는 상태 및 각 제품의 가격](customizing-the-datalist-s-editing-interface-vb/_static/image8.png)](customizing-the-datalist-s-editing-interface-vb/_static/image7.png)

**그림 3**: Name, 공급 업체, 범주, 지원 되지 않는 상태 및 각 제품의 가격 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image9.png))


## <a name="step-2-adding-the-web-controls-to-the-editing-interface"></a>2 단계: 편집 인터페이스에 웹 컨트롤 추가

필요한 웹 컨트롤을 추가 하려면 편집 인터페이스는 사용자 지정 된 DataList를 작성 하는 첫 번째 단계는 `EditItemTemplate`합니다. 특히, 범주, 공급 업체를 관리를 위한 및 중단 된 상태에 대 한 확인란에 대 한 DropDownList 필요합니다. 제품의 가격이이 예제에서 편집할 수 없기 때문 Label 웹 컨트롤을 사용 하 여 표시 계속할 수 있습니다.

편집 인터페이스를 사용자 지정 하려면 DataList s 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 선택 된 `EditItemTemplate` 드롭 다운 목록에서 옵션입니다. DropDownList를 추가 `EditItemTemplate` 설정 하 고 해당 `ID` 를 `Categories`합니다.


[![DropDownList 범주에 대 한 추가](customizing-the-datalist-s-editing-interface-vb/_static/image11.png)](customizing-the-datalist-s-editing-interface-vb/_static/image10.png)

**그림 4**: DropDownList 범주에 대 한 추가 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image12.png))


다음으로 DropDownList s 스마트 태그에서 데이터 소스 선택 옵션을 선택 하 고 라는 새 ObjectDataSource 만들 `CategoriesDataSource`합니다. 이 ObjectDataSource 사용 하도록 구성 된 `CategoriesBLL` s 클래스 `GetCategories()` 메서드 (그림 5 참조). 다음으로, DropDownList의 데이터 소스 구성 마법사는 각에 사용할 데이터 필드에 대 한을 프롬프트 `ListItem` s `Text` 및 `Value` 속성입니다. DropDownList 디스플레이 `CategoryName` 데이터 필드와 사용 하 여는 `CategoryID` 그림 6에 나와 있는 것 처럼 값으로.


[![CategoriesDataSource 라는 새 ObjectDataSource 만들기](customizing-the-datalist-s-editing-interface-vb/_static/image14.png)](customizing-the-datalist-s-editing-interface-vb/_static/image13.png)

**그림 5**: 명명 된 새 ObjectDataSource 만드는 `CategoriesDataSource` ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image15.png))


[![DropDownList의 화면을 구성 하 고 필드 값](customizing-the-datalist-s-editing-interface-vb/_static/image17.png)](customizing-the-datalist-s-editing-interface-vb/_static/image16.png)

**그림 6**: DropDownList의 표시 및 값 필드 구성 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image18.png))


이 일련의 DropDownList를 만드는 공급 업체에 대 한 단계를 반복 합니다. 설정의 `ID` 이 DropDownList를이 대 한 `Suppliers` 하 고 해당 ObjectDataSource 이름을 `SuppliersDataSource`합니다.

두 개의 dropdownlist 활용을 추가한 후 중단 된 상태에 대 한 확인란 및 제품의 이름에 대 한 입력란을 추가 합니다. 설정의 `ID` 확인란 및를 텍스트 상자에 대 한 s `Discontinued` 및 `ProductName`각각. 사용자의 제품 이름에 대 한 값을 제공 하도록 RequiredFieldValidator를 추가 합니다.

마지막으로, 업데이트 및 취소 단추를 추가 합니다. 이 두 단추에 대 한 것은 명령적는 자신의 `CommandName` 속성을 업데이트 하 고 취소 각각으로 설정 됩니다.

그러나 원하는 편집 인터페이스의 레이아웃에 자유롭게 합니다. I 같은 네 개의 열 사용 하기로 선택 했습니다 `<table>` 읽기 전용 인터페이스는 다음과 같은 선언 구문을 스크린 샷으로 레이아웃을 보여 줍니다.


[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample2.aspx)]


[![읽기 전용 인터페이스와 같은 Out 배치 편집 인터페이스는](customizing-the-datalist-s-editing-interface-vb/_static/image20.png)](customizing-the-datalist-s-editing-interface-vb/_static/image19.png)

**그림 7**: The 편집 인터페이스는 읽기 전용 인터페이스와 같은 Out 배치 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image21.png))


## <a name="step-3-creating-the-editcommand-and-cancelcommand-event-handlers"></a>3 단계: EditCommand 및 CancelCommand 이벤트 처리기 만들기

현재 구문은 없습니다 databinding에서는 `EditItemTemplate` (을 제외 하 고는 `UnitPriceLabel`에서 정확 하 게 위로 복사 된 하는 `ItemTemplate`). 구문이 일시적으로 추가 되지만 첫 번째 let s DataList s에 대 한 이벤트 처리기를 만들 `EditCommand` 및 `CancelCommand` 이벤트입니다. 이전에 설명한 대로의 책임은 `EditCommand` 반면 인 편집 단추가 클릭 되었으며, DataList 항목에 대 한 편집 인터페이스를 렌더링 하는 이벤트 처리기는 `CancelCommand`의 작업을 미리 편집 상태로 DataList를 반환 하는 것입니다.

이러한 두 개의 이벤트 처리기를 만들고 다음 코드를 사용 하도록 합니다.


[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample3.vb)]

이러한 두 명의 이벤트 처리기를에서 편집 단추를 클릭 하면 편집 인터페이스를 표시 하 고 읽기 전용 모드로 편집한 항목을 반환 취소 단추를 클릭 합니다. 그림 8에서는 Chef 한 100의 수프에 대 한 편집 버튼을 클릭 한 후 DataList를 보여 줍니다. 에서는 이후 편집 인터페이스에는 데이터 바인딩 구문이 추가를 아직 했습니다는 `ProductName` TextBox 비어는 `Discontinued` 확인란을 선택된 하 고 첫 번째 항목에서 선택한는 `Categories` 및 `Suppliers` dropdownlist 활용 합니다.


[![편집 단추 표시 편집 인터페이스를 클릭합니다.](customizing-the-datalist-s-editing-interface-vb/_static/image23.png)](customizing-the-datalist-s-editing-interface-vb/_static/image22.png)

**그림 8**: 편집 인터페이스를 편집 단추를 클릭 하면 표시 됩니다. ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image24.png))


## <a name="step-4-adding-the-databinding-syntax-to-the-editing-interface"></a>4 단계: 편집 인터페이스에 구문이 추가

편집 인터페이스 현재 제품의 값을 표시 하려면 적절 한 웹 컨트롤 값에 데이터 필드 값을 할당 하려면 databinding 구문을 사용 해야 합니다. 구문이 템플릿 편집 화면으로 이동 하 여 디자이너를 통해 적용할 수 있습니다 하 고 스마트 태그를 제어 하는 웹에서 데이터 바인딩 편집 링크를 선택 합니다. 또는 구문이 선언 태그에 직접 추가할 수 있습니다.

할당는 `ProductName` 데이터 필드 값을는 `ProductName` TextBox s `Text` 속성에는 `CategoryID` 및 `SupplierID` 데이터 필드 값을는 `Categories` 및 `Suppliers` dropdownlist 활용 `SelectedValue` 속성 및 `Discontinued` 을 데이터 필드 값은 `Discontinued` 확인란의 `Checked` 속성입니다. 디자이너를 통해 또는 직접 선언 태그를 통해 이러한 변경을 수행한 후 브라우저를 통해 페이지를 다시 확인 하 고 Chef 한 100의 수프에 대 한 편집 단추를 클릭 합니다. 그림 9에서 볼 수 있듯이 데이터 바인딩 구문이 현재 값 텍스트 상자, dropdownlist 활용, 확인란에 추가 합니다.


[![편집 단추 표시 편집 인터페이스를 클릭합니다.](customizing-the-datalist-s-editing-interface-vb/_static/image26.png)](customizing-the-datalist-s-editing-interface-vb/_static/image25.png)

**그림 9**: 편집 인터페이스를 편집 단추를 클릭 하면 표시 됩니다. ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image27.png))


## <a name="step-5-saving-the-user-s-changes-in-the-updatecommand-event-handler"></a>5 단계: UpdateCommand 이벤트 처리기에서 사용자 s 변경 내용 저장

사용자는 제품을 편집 하 고 포스트백이 발생할 업데이트 단추를 클릭 하는 경우 및 s DataList `UpdateCommand` 이벤트 발생 합니다. 이벤트 처리기를 필요에 있는 웹 컨트롤에서 값을 읽는 데는 `EditItemTemplate` 및 BLL 데이터베이스에 제품 업데이트를 사용 하는 인터페이스입니다. म으로 이전 자습서에서 했습니다는 `ProductID` 업데이트 된 제품을 통해 액세스할 수는 `DataKeys` 컬렉션입니다. 사용자가 입력 한 필드에 사용 하 여 웹 컨트롤을 프로그래밍 방식으로 참조 하 여 액세스 `FindControl("controlID")`처럼 다음 코드를 보여 줍니다.


[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample4.vb)]

참조 하 여 시작 하는 코드는 `Page.IsValid` 속성을 페이지에 있는 모든 유효성 검사 컨트롤 올바른지 확인 하십시오. 경우 `Page.IsValid` 은 `True`, 편집한 제품 s `ProductID` 에서 값을 읽은 `DataKeys` 컬렉션 및 웹 컨트롤에 데이터 입력은 `EditItemTemplate` 프로그래밍 방식으로 참조 됩니다. 그런 다음 이러한 웹 컨트롤의 값에서 읽어 들이는 적절 한 다음 전달 되는 변수 `UpdateProduct` 오버 로드 합니다. 데이터를 업데이트 한 후 DataList 미리 편집 상태로 반환 됩니다.

> [!NOTE]
> I 했습니다 예외에서 추가 논리를 처리 합니다. 생략 하면는 [처리 BLL-및 DAL 수준 예외](handling-bll-and-dal-level-exceptions-vb.md) 코드 및이 예제를 유지 하기 위해 자습서 집중 합니다. 연습으로이 자습서를 완료 한 후이 기능을 추가 합니다.


## <a name="step-6-handling-null-categoryid-and-supplierid-values"></a>6 단계: Id가 NULL이 고 SupplierID 값 처리

Northwind 데이터베이스에 대 한 허용 `NULL` 에 대 한 값은 `Products` 테이블 s `CategoryID` 및 `SupplierID` 열입니다. 그러나 우리 편집 인터페이스 대상이 t 수용 현재 `NULL` 값입니다. 가 제품을 편집 하려고 하면는 `NULL` 값 중 하나에 대 한 해당 `CategoryID` 또는 `SupplierID` 살펴보겠습니다 열은 `ArgumentOutOfRangeException` 와 유사한 오류 메시지가 나타나면서: *'범주' 수행 하기 때문에 올바르지 않은 SelectedValue가 항목 목록에 없습니다.* 또한 없어 s 현재 s 제품 범주 또는 공급 업체를 변경할 수 없으므로 값에서 비-`NULL` 값을 한 `NULL` 하나입니다.

지원 하기 위해 `NULL` 범주 및 공급 업체 dropdownlist 활용에 대 한 값을 추가 해야 추가 `ListItem`합니다. I (없음)으로 사용 하도록 선택 했습니다는 `Text` 값이 `ListItem`, d 원한다 면 (예: 빈 문자열) 다른 것로 변경할 수 있습니다. 마지막으로 dropdownlist 활용을 설정 해야 `AppendDataBoundItems` 를 `True`그러려면 범주를 잊었거나 경우 드롭다운 목록에 연결 하는 공급 업체를 정적으로 추가 덮어씁니다; `ListItem`합니다.

DataList s의에서 dropdownlist 활용 태그를 이러한 변경을 수행한 후 `EditItemTemplate` 다음과 비슷해야 합니다.


[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample5.aspx)]

> [!NOTE]
> 정적 `ListItem`의 디자이너를 통해 또는 직접 선언 구문을 통해 DropDownList에 추가할 수 있습니다. 데이터베이스를 나타내는 DropDownList 항목을 추가할 때 `NULL` 값에 추가 하는 `ListItem` 선언적 구문입니다. 사용 하는 경우는 `ListItem` 생성 된 선언적 구문에서 생략 됩니다 디자이너에서 컬렉션 편집기는 `Value` 같은 선언적 태그가 만드는 빈 문자열로 지정 된 경우 설정을 모두: `<asp:ListItem>(None)</asp:ListItem>`합니다. 무해 보일 수이 하는 동안 누락 된 `Value` DropDownList를 사용 하면는 `Text` 그 자리에 속성 값입니다. 즉, 되는 경우가 `NULL` `ListItem` 은 선택 값 (None)을 시도 제품 데이터 필드에 할당할 (`CategoryID` 또는 `SupplierID`,이 자습서에서는), 되 고 예외가 만들어집니다. 명시적으로 설정 하 여 `Value=""`, `NULL` 제품에 값을 할당할 경우 데이터 필드는 `NULL` `ListItem` 을 선택 합니다.


잠시 브라우저를 통해 진행률을 볼 수 있습니다. 제품을 편집할 때 유의 `Categories` 및 `Suppliers` dropdownlist 활용 모두 (없음)가 DropDownList의 시작 부분에 대 한 옵션입니다.


[![범주 및 공급 업체 dropdownlist 활용 포함 (None) 옵션](customizing-the-datalist-s-editing-interface-vb/_static/image29.png)](customizing-the-datalist-s-editing-interface-vb/_static/image28.png)

**그림 10**:는 `Categories` 및 `Suppliers` dropdownlist 활용을 포함 하는 (없음) 옵션 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image30.png))


데이터베이스 옵션 (없음)을 저장 하려면 `NULL` 값을 반환 해야 하는 `UpdateCommand` 이벤트 처리기입니다. 변경 된 `categoryIDValue` 및 `supplierIDValue` 변수를 nullable 정수 여야 하며 해당 값을 할당할 이외의 `Nothing` 경우에만 DropDownList의 `SelectedValue` 은 빈 문자열이 아닙니다:


[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample6.vb)]

값이이 변경으로 인해 `Nothing` 으로 전달 되는 `UpdateProduct` BLL 메서드 (없음) 사용자 선택 옵션에 해당 하는 드롭다운 목록 중 하나에서 `NULL` 데이터베이스 값입니다.

## <a name="summary"></a>요약

이 자습서에서는 텍스트 상자, 두 개의 dropdownlist 활용와 함께 유효성 검사 컨트롤 CheckBox 세 가지 다른 입력된 웹 컨트롤을 포함 하는 보다 복잡 한 DataList 편집 인터페이스를 만드는 방법에 대해 살펴보았습니다. 단계는 사용 중인 웹 컨트롤에 관계 없이 동일 하 게 편집 인터페이스를 작성할 때: s DataList에 웹 컨트롤을 추가 하 여 시작 `EditItemTemplate`; databinding 구문을 사용 하 여 적절 한 웹과 해당 데이터 필드 값을 할당 하려면 컨트롤 속성입니다. 에 `UpdateCommand` 이벤트 처리기 웹 컨트롤 및 BLL에 해당 값을 전달 하는 적절 한 속성을 프로그래밍 방식으로 액세스 합니다.

여부는 편집 인터페이스를 만들 때 해당 s 방금: 텍스트 상자 또는 다른 웹 컨트롤의 컬렉션으로 구성, 데이터베이스를 올바르게 처리 해야 `NULL` 값입니다. 가정 하에 때 `NULL` s, 사실이 표시 해야 합니다만 올바르게 하지 기존 `NULL` 편집 인터페이스 뿐만 아니라 해당 사용자에 대 한 값으로 값을 표시 하 여는 방법을 제공 `NULL`합니다. DataLists에 dropdownlist 활용에 대 한 일반적으로 즉, 정적 추가 `ListItem` 인 `Value` 명시적으로 속성이 빈 문자열 (`Value=""`), 약간의 코드를 추가 하 고는 `UpdateCommand` 결정 하는 이벤트 처리기 여부는 `NULL``ListItem` 선택 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가 Dennis Patterson, David Suru 및 Randy Schmidt 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md)
