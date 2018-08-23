---
uid: web-forms/overview/data-access/working-with-batched-data/batch-inserting-vb
title: 일괄 처리 삽입 (VB) | Microsoft Docs
author: rick-anderson
description: 단일 작업에서 여러 데이터베이스 레코드를 삽입 하는 방법에 알아봅니다. 사용자 인터페이스 계층에서 사용자를 여러 n을 입력할 수 있도록 GridView 확장 하는 중...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 48e2a4ae-77ca-4208-a204-c38c690ffb59
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-inserting-vb
msc.type: authoredcontent
ms.openlocfilehash: 58338d8bfdd782167aafaa440f2d549d6eeb838e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838169"
---
<a name="batch-inserting-vb"></a>일괄 삽입 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_66_VB.zip) 또는 [PDF 다운로드](batch-inserting-vb/_static/datatutorial66vb1.pdf)

> 단일 작업에서 여러 데이터베이스 레코드를 삽입 하는 방법에 알아봅니다. 사용자 인터페이스 계층에서 GridView를 여러 개의 새 레코드를 입력할 수 있도록 확장 합니다. 데이터 액세스 계층에는 모든 삽입이 성공 하거나 모든 삽입 롤백되는 트랜잭션 내에서 여러 삽입 작업에서는 래핑합니다.


## <a name="introduction"></a>소개

에 [일괄 처리 업데이트](batch-updating-vb.md) 자습서 된 여러 레코드 편집할 수 있는 인터페이스를 제공 하는 GridView 컨트롤 사용자 지정에 대해 살펴보았습니다. 페이지를 방문 하는 사용자 수 일련의 변경 확인 하 고 그런 다음 한 번의 단추 클릭으로 일괄 업데이트를 수행 합니다. 이러한 인터페이스를 한꺼번에 여러 레코드에 사용자가 일반적으로 업데이트할 경우 수많은 클릭을 저장할 수 있으며 키보드 / 마우스 컨텍스트 전환의 기본에 비해 행별 먼저 다시 탐색 된 편집 기능을 [는 삽입, 업데이트 및 삭제 하는 데이터에 대 한 개요](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 자습서입니다.

이 개념 레코드를 추가 하는 경우에 적용할 수 있습니다. Imagine는 Northwind traders에서는 일반적으로 구할 배송 특정 범주에 대 한 제품을 포함 하는 공급 업체에서 합니다. 예를 들어 도쿄 Traders에서 6 개의 다른 tea 및 coffee 제품의 배송을 수신할 수 있습니다 했습니다. 사용자가 DetailsView 컨트롤을 통해 한 번에 6 개의 제품 하나를 입력 하는 경우 대부분의 동일한 값을 반복 해 서 선택 해야 합니다: 동일한 공급자 (도쿄 Traders) 같은 범주 (음료)를 선택 해야 합니다 (지원 되지 않는 동일한, False) 및 순서 값 (0)에 동일한 단위입니다. 이 반복 되는 데이터 항목은만 시간이 오래 걸릴 있지만 오류가 발생할 가능성이 높습니다.

약간의 작업을 사용 하 여 공급자 및 범주를 한 번 일련의 제품 이름과 단위 가격이 입력 한 다음 데이터베이스에 새 제품을 추가 하는 단추를 클릭을 선택할 수 있도록 해 주는 인터페이스를 삽입 하는 일괄 처리를 만들 수 있습니다 (그림 1 참조). 각 제품 추가 됨에 따라 해당 `ProductName` 및 `UnitPrice` 데이터 필드는 텍스트 상자에 입력 된 값을 할당 하는 동안 해당 `CategoryID` 및 `SupplierID` 값 상위 fo 폼에서 Dropdownlist의 값이 할당 됩니다. `Discontinued` 하 고 `UnitsOnOrder` 값의 하드 코드 된 값으로 설정 됩니다 `False` 0, 각각.


[![일괄 처리 삽입 인터페이스](batch-inserting-vb/_static/image2.png)](batch-inserting-vb/_static/image1.png)

**그림 1**: 일괄 처리 삽입 인터페이스 ([큰 이미지를 보려면 클릭](batch-inserting-vb/_static/image3.png))


이 자습서에서는 그림 1에 표시 된 인터페이스를 삽입 하는 일괄 처리를 구현 하는 페이지를 만들겠습니다. 로 이전 두 자습서를 통해 삽입을 원자성을 보장 하기 하기 위한 트랜잭션의 범위 내에서 배치 됩니다 했습니다. Let s 시작!

## <a name="step-1-creating-the-display-interface"></a>1 단계: 표시 인터페이스를 만드는 방법

이 자습서는 두 개의 영역으로 나뉩니다는 단일 페이지의 구성 됩니다: 표시 영역 및 영역을 삽입 합니다. 이 단계에서는 만들겠습니다는 표시 인터페이스를 GridView에 제품이 표시 하 고 프로세스 제품 배송과 라는 단추를 포함 합니다. 이 단추를 클릭 하면 표시 인터페이스는 그림 1에 나와 있는 삽입 인터페이스를 사용 하 여 대체 됩니다. 취소 단추를 클릭할 또는 배송에서 추가 제품 후 표시 인터페이스를 반환 합니다. 2 단계에서에서 삽입 인터페이스를 만들겠습니다.

두 개의 인터페이스를 한 번에 하나씩만 표시 되는 페이지를 만드는 경우 각 인터페이스 일반적으로 내에 배치 됩니다는 [패널 웹 컨트롤](http://www.w3schools.com/aspnet/control_panel.asp), 다른 컨트롤에 대 한 컨테이너 역할을 하는 합니다. 따라서 페이지 각 인터페이스에 대 한 두 개의 패널 컨트롤과 하나를 갖습니다.

열어서 시작 합니다 `BatchInsert.aspx` 페이지는 `BatchData` 폴더 및 디자이너 도구 상자에서 끌어서 패널 (그림 2 참조). 설정 패널 s `ID` 속성을 `DisplayInterface`입니다. 디자이너에 패널을 추가 하는 경우 해당 `Height` 고 `Width` 속성 50px를 125px를 각각 설정 됩니다. 속성 창에서 이러한 속성 값을 지웁니다.


[![디자이너 도구 상자에서 패널을 끌어 옵니다.](batch-inserting-vb/_static/image5.png)](batch-inserting-vb/_static/image4.png)

**그림 2**: 패널 디자이너 도구 상자에서 끌어 ([큰 이미지를 보려면 클릭](batch-inserting-vb/_static/image6.png))


그런 다음 패널에 단추와 GridView 컨트롤을 끕니다. S 단추 설정 `ID` 속성을 `ProcessShipment` 고 `Text` 프로세스 제품 배송과 속성입니다. 집합 GridView s `ID` 속성을 `ProductsGrid` 및 스마트 태그를 바인딩할 라는 새로운 ObjectDataSource는 `ProductsDataSource`합니다. ObjectDataSource에서 해당 데이터를 가져오도록 구성 합니다 `ProductsBLL` s 클래스 `GetProducts` 메서드. 데이터 표시에이 GridView를 사용 하므로 삽입, 업데이트, 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제 합니다. 데이터 소스 구성 마법사를 완료 하려면 마침을 클릭 합니다.


[![S ProductsBLL 클래스 GetProducts 메서드에서 반환 되는 데이터를 표시 합니다.](batch-inserting-vb/_static/image8.png)](batch-inserting-vb/_static/image7.png)

**그림 3**:에서 반환 된 데이터를 표시 합니다 `ProductsBLL` s 클래스 `GetProducts` 메서드 ([클릭 하 여 큰 이미지 보기](batch-inserting-vb/_static/image9.png))


[![UPDATE, INSERT 드롭 다운 목록을 설정 하 고 탭 삭제 (없음)](batch-inserting-vb/_static/image11.png)](batch-inserting-vb/_static/image10.png)

**그림 4**: 드롭다운 목록에서 업데이트, 삽입 및 삭제 탭 하도록 설정 (없음) ([큰 이미지를 보려면 클릭](batch-inserting-vb/_static/image12.png))


ObjectDataSource 마법사를 완료 한 후 Visual Studio는 BoundFields 및 제품 데이터 필드에 대 한 CheckBoxField를 추가 합니다. 제거를 제외한 모든 `ProductName`, `CategoryName`를 `SupplierName`를 `UnitPrice`, 및 `Discontinued` 필드입니다. 시각적인 사용자 지정 해도 됩니다. 서식을 지정 하는 `UnitPrice` 통화 값으로 필드의 필드 다시 정렬 및 다양 한 필드 이름을 바꿀 `HeaderText` 값입니다. 페이징 및 정렬 GridView가 스마트 태그에서 페이징을 사용 하도록 설정 하 고 정렬 사용 확인란을 선택 하 여 지원을 포함 하도록 GridView를 구성할 수도 있습니다.

패널, 단추, GridView 및 ObjectDataSource 컨트롤을 추가 하 고 GridView의 필드를 사용자 지정 페이지 s 선언적 태그 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](batch-inserting-vb/samples/sample1.aspx)]

내 열기 및 닫기 단추와 GridView 태그에 나타나는 참고 `<asp:Panel>` 태그입니다. 이러한 컨트롤 내에 있으므로 합니다 `DisplayInterface` 패널에서는 숨길 수 단순히 s 패널을 설정 하 여 `Visible` 속성을 `False`입니다. 3 단계에서 프로그래밍 방식으로 패널 s 변경 살펴봅니다 `Visible` 속성 단추에 대 한 응답으로 다른 숨기면 하나의 인터페이스를 표시 하려면 클릭 합니다.

시간을 내어 브라우저를 통해 진행 상황을 확인 합니다. 그림 5에서 알 수 있듯이, 한 번에 10 개 제품을 나열 하는 GridView 위에 프로세스 제품 배송과 단추가 표시 됩니다.


[![제품을 나열 하 고 정렬 및 페이징 기능을 제공 하는 GridView](batch-inserting-vb/_static/image14.png)](batch-inserting-vb/_static/image13.png)

**그림 5**: 제품 및 제공 정렬 및 페이징 기능을 나열 하는 GridView ([큰 이미지를 보려면 클릭](batch-inserting-vb/_static/image15.png))


## <a name="step-2-creating-the-inserting-interface"></a>2 단계: 삽입 인터페이스를 만드는 방법

인터페이스로 표시 완료 준비 된 삽입 인터페이스를 만드는 것입니다. 이 자습서에서는 s를 단일 공급자 및 범주 값에 대 한 메시지를 표시 하 고 사용자를 최대 5 개 제품 이름과 단위 가격 값을 입력할 수 있게 하는 삽입 인터페이스를 만들 수 있습니다. 사용자는이 인터페이스를 모두 동일한 범주 및 공급자를 공유 하지만 고유한 제품 이름 및 가격과 있는 5 개의 새 제품을 추가할 수 있습니다.

기존 아래에 배치 디자이너 도구 상자에서 패널을 끌어서 시작 `DisplayInterface` 패널입니다. 설정 합니다 `ID` 패널을 새로 추가 된 속성 `InsertingInterface` 설정 하 고 해당 `Visible` 속성을 `False`입니다. 설정 하는 코드 추가 합니다 `InsertingInterface` s 패널 `Visible` 속성을 `True` 3 단계. 또한 s 패널을 지울 `Height` 고 `Width` 속성 값입니다.

다음으로, 다시 그림 1에에서 나온 삽입 인터페이스를 만들기 위해 필요 합니다. 다양 한 HTML 기술을 통해이 인터페이스를 만들 수 있지만 간단 하나를 사용 합니다: 네 개의 열과 7 행 테이블입니다.

> [!NOTE]
> Html 태그를 입력할 때 `<table>` 요소인 않겠습니다 소스 뷰를 사용 합니다. Visual Studio에 추가 하기 위한 도구를가 하는 동안 `<table>` 디자이너를 통해 요소를 디자이너 삽입할 너무 감수 모든 것을 원하지 않는 메일 `style` 태그에 설정 합니다. 만든 후는 `<table>` 태그, 일반적으로 돌아가면 디자이너 웹 컨트롤을 추가 하 고 해당 속성을 설정 합니다. 정적 HTML을 사용 하 여 원하는 미리 결정된 된 열과 행을 사용 하 여 테이블을 만들 때 대신 [Table 웹 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.table.aspx) 테이블 웹 컨트롤 내에 있는 웹 컨트롤을 다시 액세스를 사용 하 여 하므로 `FindControl("controlID")` 패턴입니다. 그러나 컨트롤을 프로그래밍 방식으로 생성할 수 있습니다. 테이블 웹 이후 동적으로 크기 조정 테이블 (행 또는 열에 있는 일부 데이터베이스 또는 사용자가 지정한 기준에 기반한 항목)에 대 한 테이블 웹 컨트롤 사용을 않습니다.


내에서 다음 태그를 입력 합니다 `<asp:Panel>` 태그를 `InsertingInterface` 패널:


[!code-html[Main](batch-inserting-vb/samples/sample2.html)]

이 `<table>` 태그는 모든 웹 컨트롤이 포함 되지 않습니다 아직 이러한 일시적으로 추가 합니다. 각 `<tr>` 특정 CSS 클래스 설정을 포함 하는 요소: `BatchInsertHeaderRow` 공급자 및 범주 Dropdownlist 어디로; 머리글 행 `BatchInsertFooterRow` 에 있는 제품에서 배송 및 취소 단추 추가 될; 바닥글 행을 교대로 반복 되는 `BatchInsertRow` 및 `BatchInsertAlternatingRow` 제품 및 단위를 포함 하는 행에 대 한 값 가격 TextBox 컨트롤입니다. I ve에 해당 하는 CSS 클래스를 생성 합니다 `Styles.css` GridView 및 DetailsView 비슷한 모양의 삽입 인터페이스를 제공 하는 파일을 제어 ve이이 자습서 전체에서 사용 했습니다. 이러한 CSS 클래스는 다음과 같습니다.


[!code-css[Main](batch-inserting-vb/samples/sample3.css)]

입력이 태그를 사용 하 여 디자인 뷰로 돌아갑니다. 이 `<table>` 그림 6에서 볼 수 있듯이 디자이너에서 네 개의 열과 7 행 테이블로 표시 됩니다.


[![삽입 인터페이스에 구성 된 열을 4-7 행 테이블](batch-inserting-vb/_static/image17.png)](batch-inserting-vb/_static/image16.png)

**그림 6**: The 삽입 인터페이스에 구성 된 열을 4-7 행 테이블 ([큰 이미지를 보려면 클릭](batch-inserting-vb/_static/image18.png))


이제 다시에서는 웹 컨트롤이 삽입 인터페이스에 추가할 준비가 되었습니다. Dropdownlist 두 도구 상자에서 적절 한 공급자 및 범주에 대 한 테이블 셀 끌어다 놓습니다.

DropDownList의 공급자를 설정 `ID` 속성을 `Suppliers` 라는 새 ObjectDataSource를 바인딩할 `SuppliersDataSource`합니다. 해당 데이터를 검색할 새 ObjectDataSource 구성 합니다 `SuppliersBLL` s 클래스 `GetSuppliers` 메서드와 업데이트 집합 탭 (없음) s 드롭 다운 목록. 마법사를 완료 하려면 마침을 클릭 합니다.


[![S SuppliersBLL 클래스 GetSuppliers 메서드를 사용 하는 ObjectDataSource 구성](batch-inserting-vb/_static/image20.png)](batch-inserting-vb/_static/image19.png)

**그림 7**: ObjectDataSource를 사용 하 여 구성 합니다 `SuppliersBLL` s 클래스 `GetSuppliers` 메서드 ([클릭 하 여 큰 이미지 보기](batch-inserting-vb/_static/image21.png))


가 `Suppliers` DropDownList 표시 합니다 `CompanyName` 데이터 필드와 사용 하 여는 `SupplierID` 으로 데이터 필드 해당 `ListItem`의 값입니다.


[![CompanyName 데이터 필드를 표시 하 고 값으로 SupplierID 사용](batch-inserting-vb/_static/image23.png)](batch-inserting-vb/_static/image22.png)

**그림 8**: 표시 된 `CompanyName` 데이터 필드와 사용 하 여 `SupplierID` 값으로 ([클릭 하 여 큰 이미지 보기](batch-inserting-vb/_static/image24.png))


이름을 두 번째 DropDownList `Categories` 라는 새 ObjectDataSource를 바인딩할 `CategoriesDataSource`합니다. 구성 합니다 `CategoriesDataSource` ObjectDataSource 사용 하는 `CategoriesBLL` s 클래스 `GetCategories` 마법사를 완료 하려면 완료 하는 방법으로, UPDATE 및 DELETE 탭 (없음) 하 고 드롭다운 목록 나열 하는 집합입니다. 마지막으로, DropDownList 표시는는 `CategoryName` 데이터 필드와 사용 하 여는 `CategoryID` 값으로.

Dropdownlist 이러한 두 추가 되었으며 적절 하 게 구성 된 경우, ObjectDataSources에 바인딩된 후 화면은 그림 9와 비슷하게 표시 됩니다.


[![공급자 및 범주 Dropdownlist 머리글 행을 포함 하는 이제](batch-inserting-vb/_static/image26.png)](batch-inserting-vb/_static/image25.png)

**그림 9**: The 헤더 행 이제 포함 된 `Suppliers` 및 `Categories` Dropdownlist ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image27.png))


이제 이름과 각 새 제품 가격을 수집 하는 텍스트 상자를 생성 해야 합니다. 각 5 제품 이름과 가격 행에 대 한 디자이너 도구 상자에서 텍스트 상자 컨트롤을 끕니다. 설정 합니다 `ID` 하려면 입력란의 속성 `ProductName1`, `UnitPrice1`, `ProductName2`, `UnitPrice2`, `ProductName3`, `UnitPrice3`등.

CompareValidator 단가 텍스트 상자 설정의 각 추가 합니다 `ControlToValidate` 속성을 적절 한 `ID`합니다. 설정 합니다 `Operator` 속성을 `GreaterThanEqual`, `ValueToCompare` 0으로 및 `Type` 에 `Currency`. 이러한 설정은 되도록에 가격을 입력 하는 경우 유효한 통화 값을 0 보다 크거나 CompareValidator 지시 합니다. 설정 된 `Text` 속성을 \*, 및 `ErrorMessage` 가격에는 0 보다 크거나 이어야 합니다. 또한 모든 통화 기호를 생략 하세요.

> [!NOTE]
> 삽입 인터페이스 RequiredFieldValidator 컨트롤에도 포함 되지 않습니다 합니다 `ProductName` 필드를 `Products` 데이터베이스 테이블을 허용 하지 않습니다 `NULL` 값입니다. 사용자가 최대 5 개 제품을 입력할 수 있도록 하고자 때문입니다. 예를 들어, 사용자가 처음 3 개 행에 대 한 제품 이름과 단위 가격이 제공을 마지막 두 행을 비워 두면 d 추가할 새 제품이 시스템입니다. 그러나 이후 `ProductName` 는 필요한에서는 프로그래밍 방식으로 확인 해야 해당 제품 이름 값이 제공 입력은 단가 있는지 확인 합니다. 에서는에서는 4 단계에서에서이 확인을 수행할 수 있습니다.


사용자가의 입력의 유효성을 검사할 때 CompareValidator 값 통화 기호를 포함 하는 경우 잘못 된 데이터를 보고 합니다. 각 단위 가격은 가격을 입력 하는 경우 통화 기호를 생략 하는 사용자에 게 지시 하는 시각적 표현으로 처리 하는 텍스트 앞에 $를 추가 합니다.

마지막으로, 내의 ValidationSummary 컨트롤을 추가 합니다 `InsertingInterface` 설정 패널 해당 `ShowMessageBox` 속성을 `True` 고 `ShowSummary` 속성을 `False`입니다. 이러한 설정을 사용 하 여 사용자가는 잘못 된 단위 가격 값을 입력 하는 경우 별표에 잘못 된 TextBox 컨트롤 옆에 표시 됩니다 및는 ValidationSummary 이전에 지정한 오류 메시지를 표시 하는 클라이언트 쪽 messagebox가 표시 됩니다.

이 시점에서 화면 그림 10 유사 합니다.


[![삽입 인터페이스 이제 텍스트 상자 제품에 대 한 이름 및 가격](batch-inserting-vb/_static/image29.png)](batch-inserting-vb/_static/image28.png)

**그림 10**: The 삽입 인터페이스 이제 포함 텍스트 상자 제품 이름과 가격 ([큰 이미지를 보려면 클릭](batch-inserting-vb/_static/image30.png))


다음 배송 및 취소 단추가의 바닥글 행에 제품 추가 추가 해야 합니다. 끌어서 두 단추 컨트롤을 도구 상자에서 삽입 인터페이스의 바닥글에 단추를 설정 `ID` 속성을 `AddProducts` 하 고 `CancelButton` 및 `Text` 배송 및 취소에서 제품을 각각 추가할 속성입니다. 또한 설정 합니다 `CancelButton` s control `CausesValidation` 속성을 `false`입니다.

마지막으로, 두 인터페이스에 대 한 상태 메시지를 표시 하는 레이블 웹 컨트롤을 추가 해야 합니다. 예를 들어 사용자가 제품의 배송 항목을 새를 성공적으로 추가 하려고 표시 인터페이스를 반환 하 고 확인 메시지를 표시 합니다. 하지만 이후 경고 메시지를 표시 해야 사용자는 제품 이름 해제 하지만 새 제품에 대 한 가격을 제공 하면 하는 경우는 `ProductName` 필드는 필수입니다. 두 인터페이스를 표시 하려면이 메시지에 필요 하므로 패널 외부에서 페이지의 위쪽에 배치 합니다.

디자이너에서 페이지의 위쪽에 도구 상자에서 레이블 웹 컨트롤을 끕니다. 설정 합니다 `ID` 속성을 `StatusLabel`아웃의 선택을 취소 합니다 `Text` 속성을 설정 하 고는 `Visible` 및 `EnableViewState` 속성을 `False`합니다. 이전 자습서에서 살펴본 대로 설정 합니다 `EnableViewState` 속성을 `False` 프로그래밍 방식으로 레이블의 속성 값을 변경 하 고 자동으로 후속 포스트백에서 기본값으로 다시 되돌리려면 되도록 할 수 있습니다. 이 후속 포스트백에서 사라집니다 일부 사용자 작업에 대 한 응답에 상태 메시지를 표시 하는 것에 대 한 코드를 단순화 합니다. 마지막으로 설정 합니다 `StatusLabel` s control `CssClass` 에 정의 된 경고는 CSS 클래스의 이름인 속성 `Styles.css` 큰, 기울임꼴, 굵게, 빨간색 글꼴로 텍스트를 표시 하는 합니다.

그림 11에서는 레이블을 추가 및 구성 된 후 Visual Studio 디자이너를 보여 줍니다.


[![두 개의 패널 컨트롤 위에 statuslabel은 컨트롤 배치](batch-inserting-vb/_static/image32.png)](batch-inserting-vb/_static/image31.png)

**그림 11**: 현재 위치를 `StatusLabel` 컨트롤 위에 두 개의 패널 컨트롤 ([클릭 하 여 큰 이미지 보기](batch-inserting-vb/_static/image33.png))


## <a name="step-3-switching-between-the-display-and-inserting-interfaces"></a>3 단계: 표시 간에 전환 및 삽입 인터페이스

이 시점에서 태그를 표시 및 왼쪽에 두 가지 작업을 사용 하 여 다시 인터페이스 했지만 삽입 했습니다.

- 표시를 전환 및 삽입 인터페이스
- 데이터베이스에 배송에 제품 추가

현재 표시 인터페이스는 표시 되지만 삽입 인터페이스 숨겨집니다. 때문에 이것이 `DisplayInterface` 패널 s `Visible` 속성이로 설정 되어 `True` (기본값) 동안를 `InsertingInterface` 패널 s `Visible` 속성이 `False`. 각 컨트롤 s 설정/해제 해야 두 인터페이스 간에 전환 하려면 `Visible` 속성 값입니다.

제품 배송 프로세스 단추를 클릭할 때 삽입 인터페이스에는 표시 인터페이스에서 이동 하려고 합니다. 따라서이 단추 s에 대 한 이벤트 처리기를 만들고 `Click` 다음 코드를 포함 하는 이벤트:


[!code-vb[Main](batch-inserting-vb/samples/sample4.vb)]

이 코드를 단순히 숨깁니다 합니다 `DisplayInterface` 패널과 표시를 `InsertingInterface` 패널.

다음으로 삽입 인터페이스에서 배송 및 취소 단추 컨트롤에서 추가 제품에 대 한 이벤트 처리기를 만듭니다. 이러한 단추 중 하나를 클릭할 때 표시 인터페이스를 다시 전환 해야 합니다. 만들 `Click` 둘 다에 대 한 이벤트 처리기를 호출 하는 단추 컨트롤 `ReturnToDisplayInterface`를 일시적으로 추가 하는 메서드. 숨기기 외에도 `InsertingInterface` 패널과 보여 주는 `DisplayInterface` 패널은 `ReturnToDisplayInterface` 메서드를 미리 편집 상태로 웹 컨트롤을 반환 해야 합니다. Dropdownlist를 설정 하는 것이 `SelectedIndex` 속성을 0과 정리는 `Text` TextBox 컨트롤의 속성입니다.

> [!NOTE]
> 어떤 일이 발생 하는 것이 좋습니다 경우에서는 동작 t 표시 인터페이스를 반환 하기 전에 미리 편집 상태로 컨트롤을 반환 합니다. 사용자 제품 배송 프로세스 단추를 클릭 하 고 배송을에서 제품을 입력 하 고 추가 제품 배송을 클릭 수 있습니다. 이 제품을 추가 하 고 사용자는 표시 인터페이스를 반환 합니다. 이 시점에서 사용자는 다른 운송을 통해를 추가 하 려 수 있습니다. 삽입 인터페이스 있지만 DropDownList 돌아왔을 프로세스 제품 배송과 단추를 클릭 하면 선택 항목 및 입력란 값은 여전히 채울 수 이전 값입니다.


[!code-vb[Main](batch-inserting-vb/samples/sample5.vb)]

둘 다 `Click` 이벤트 처리기를 호출 하면 됩니다 합니다 `ReturnToDisplayInterface` 메서드를 배송에서 추가 제품 다시 돌아갈 것 이지만 `Click` 이벤트 처리기에서 4 단계 및 제품을 저장 하는 코드를 추가 합니다. `ReturnToDisplayInterface` 반환 하 여 시작 합니다 `Suppliers` 및 `Categories` Dropdownlist 해당 첫 번째 옵션입니다. 두 상수가 `firstControlID` 하 고 `lastControlID` 시작 및 끝 입력란 삽입 인터페이스에서 사용 하는 범위 제품 이름과 단위 가격 명명에 사용 되는 컨트롤 인덱스 값을 표시는 `For` 를설정하는루프`Text`텍스트 상자 컨트롤의 속성을 빈 문자열로 다시 합니다. 마지막으로, 패널 `Visible` 속성 삽입 인터페이스가 숨겨진다는 있도록 및 표시 하는 표시 인터페이스를 다시 설정 됩니다.

시간을 내어이 페이지를 브라우저에서 테스트 합니다. 먼저 페이지를 방문 하는 경우 그림 5에 표시 된 대로 표시 인터페이스를 표시 됩니다. 제품 배송 프로세스 단추를 클릭 합니다. 페이지를 포스트백 및 그림 12 에서처럼 삽입 인터페이스를 이제 표시 됩니다. 중 하나는 추가 제품을 배송 하거나 취소 단추를 클릭 하면 표시 인터페이스를 반환 합니다.

> [!NOTE]
> 삽입 인터페이스를 보면서 잠시 단가 텍스트 상자에 CompareValidators 테스트 합니다. 클라이언트 쪽 messagebox에서 잘못 된 통화 값을 사용 하 여 배송 단추나 가격은 0 보다 작은 값을 사용 하 여 제품 추가 클릭 하면 경고를 표시 됩니다.


[![제품 배송 프로세스 단추를 클릭 한 후 삽입 인터페이스가 표시](batch-inserting-vb/_static/image35.png)](batch-inserting-vb/_static/image34.png)

**그림 12**: The 삽입 인터페이스 프로세스 제품 배송 단추를 클릭 한 후 표시 됩니다 ([큰 이미지를 보려면 클릭](batch-inserting-vb/_static/image36.png))


## <a name="step-4-adding-the-products"></a>4 단계: 추가 제품

모든 제품을 배송 단추 s에서 추가 제품의 데이터베이스에 저장 하려면이 자습서에 남아 있는 `Click` 이벤트 처리기입니다. 만들어 이렇게를 `ProductsDataTable` 추가 `ProductsRow` 제공 된 제품 이름 각각에 대 한 인스턴스. 이 한 번 `ProductsRow` s에 대 한 호출을 만들겠습니다 추가한 합니다 `ProductsBLL` s 클래스 `UpdateWithTransaction` 전달 하는 메서드는 `ProductsDataTable`합니다. 이전에 설명한 대로 `UpdateWithTransaction` 메서드를 다시 생성 된를 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](wrapping-database-modifications-within-a-transaction-vb.md) 자습서를 전달을 `ProductsDataTable` 에 `ProductsTableAdapter` s `UpdateWithTransaction` 메서드. 여기에서 ADO.NET 트랜잭션이 시작 및 TableAdatper 문제는 `INSERT` 데이터베이스에 추가 된 각 문을 `ProductsRow` DataTable에서. 모든 제품이 오류 없이 추가 될 트랜잭션이 커밋될 때 가정 하 고, 그렇지 않으면이 롤백됩니다.

배송 단추 s에서 추가 제품에 대 한 코드 `Click` 이벤트 처리기도 약간의 오류 검사를 수행 해야 합니다. 없습니다 RequiredFieldValidators 삽입 인터페이스에서 사용 되므로 사용자는 해당 이름을 생략 하는 동안 가격을 제품에 대 한 입력할 수 있습니다. S 제품 이름을 필수 이므로 해야 이러한 조건을 화면의 경우 사용자 알림 및 삽입을 사용 하 여 진행 되지 않습니다. 전체 `Click` 이벤트 처리기 코드는 다음과 같습니다.


[!code-vb[Main](batch-inserting-vb/samples/sample6.vb)]

이벤트 처리기는 함으로써 시작 합니다 `Page.IsValid` 속성 값을 반환 합니다. `True`합니다. 반환 하는 경우 `False`, 한 다음 하나를 의미 하는 잘못 된 데이터를 보고 하는 CompareValidators 많은; 이렇게에서 하지 입력 한 제품을 삽입 하기 위해 또는에서는 빠지기 예외가 발생 하 여 사용자가 입력 한 단가 할당 하려고 하면 값을 `ProductsRow` s `UnitPrice` 속성입니다.

다음으로 새 `ProductsDataTable` 인스턴스가 생성 됩니다 (`products`). A `For` 루프를 사용 하 여 제품 이름과 단위 가격이 입력란을 반복 하 고 `Text` 로컬 변수로 속성은 읽기 `productName` 및 `unitPrice`합니다. 사용자가 해당 제품 이름, 아니라 단위 가격에 대 한 값을 입력 하는 경우는 `StatusLabel` 표시 해야 하는 단위 가격을 제공 하는 경우 메시지는 제품의 이름을 포함 하 고 이벤트 처리기를 종료 합니다.

새 제품 이름을 입력 하는 경우 `ProductsRow` 인스턴스가 사용 하 여 생성 되는 `ProductsDataTable` s `NewProductsRow` 메서드. 이 새로운 `ProductsRow` 인스턴스 s `ProductName` 현재 제품 속성 이름을 지정 하는 동안 텍스트 상자를 `SupplierID` 및 `CategoryID` 속성에 할당 된는 `SelectedValue` 삽입 인터페이스의 헤더에 Dropdownlist의 속성입니다. 에 할당 된 경우 사용자가의 제품 가격에 대 한 값을 입력 합니다는 `ProductsRow` 인스턴스 s `UnitPrice` 속성 속성이 고, 그렇지 됩니다 할당 하지 않은 경우 왼쪽을 `NULL` 에 대 한 값 `UnitPrice` 데이터베이스에서. 마지막으로 `Discontinued` 및 `UnitsOnOrder` 속성은 하드 코드 된 값에 할당 된 `False` 0, 각각.

속성에 할당 된 후의 `ProductsRow` 에 추가 되는 인스턴스는 `ProductsDataTable`합니다.

완료 되 면는 `For` 제품 추가 되었는지 여부를 확인 루프를 했습니다. 사용자 수, 추가 제품 가격이 나 제품 이름을 입력 하기 전에 배송을 클릭 했습니다. 하나 이상의 제품의 경우는 `ProductsDataTable`는 `ProductsBLL` s 클래스 `UpdateWithTransaction` 메서드가 호출 됩니다. 데이터를 다음으로, 다시 바인딩되는 `ProductsGrid` GridView 새로 추가 된 제품 표시 인터페이스에 표시 되도록 합니다. 합니다 `StatusLabel` 확인 메시지를 표시 하도록 업데이트 됩니다 및 `ReturnToDisplayInterface` 인터페이스를 삽입 하 고 표시 인터페이스를 보여 주는 숨기면 호출 됩니다.

제품이 없습니다. 입력 된 경우 삽입 인터페이스를 계속 하지만 제품이 없습니다. 추가 된 메시지가 표시 됩니다. 제품 이름을 입력 하 고 입력란에서 단위 가격이 표시 됩니다.

그림 13, 14 및 15의 표시를 삽입 하 고 작업에서 인터페이스를 표시 합니다. 그림 13에서는 사용자가 해당 제품 이름이 없는 단위 가격 값을 입력 합니다. 그림 14 인터페이스를 보여 줍니다 표시 세 후 새 제품 추가 된 성공적으로 그림 15 (이전 페이지는 세 번째) GridView에 새로 추가 된 제품 중 두 가지를 보여 줍니다.


[![제품 이름이 필요한 경우 입력 단가](batch-inserting-vb/_static/image38.png)](batch-inserting-vb/_static/image37.png)

**그림 13**:는 제품 이름이 필요한 경우 입력 된 단위 가격 ([큰 이미지를 보려면 클릭](batch-inserting-vb/_static/image39.png))


[![공급자에 대 한 세 개의 새 Veggies 추가한 유미 식품 s](batch-inserting-vb/_static/image41.png)](batch-inserting-vb/_static/image40.png)

**그림 14**: 세 가지 새 Veggies 추가한 공급자 유미 식품 s ([큰 이미지를 보려면 클릭](batch-inserting-vb/_static/image42.png))


[![GridView의 마지막 페이지에서 새 제품을 찾을 수 있습니다.](batch-inserting-vb/_static/image44.png)](batch-inserting-vb/_static/image43.png)

**그림 15**:의 새 제품에서에서 찾을 수 있습니다 GridView의 마지막 페이지 ([큰 이미지를 보려면 클릭](batch-inserting-vb/_static/image45.png))


> [!NOTE]
> 이 자습서에서 사용 되는 논리를 삽입 하는 일괄 처리는 트랜잭션의 범위 내에서 삽입을 래핑합니다. 이 확인 하려면 데이터베이스 수준 오류를 의도적으로 소개 합니다. 새 할당 하는 대신에 예를 들어 `ProductsRow` 인스턴스 s `CategoryID` 속성에서 선택한 값을 합니다 `Categories` 드롭다운 목록에서 같은 값이 할당 `i * 5`합니다. 여기 `i` 루프 인덱서 이며 1부터 5 까지의 값입니다. 따라서 경우 첫 번째 제품을 삽입 하는 일괄 처리에서 두 개 이상의 제품을 추가 해야 올바른 `CategoryID` 값 (5), 있지만 후속 제품 갖습니다 `CategoryID` 최대 일치 하지 않는 값 `CategoryID` 값을 `Categories` 테이블. 적용 하는 동안 첫 번째는 `INSERT` 성공 하 고 이후의 조건은 foreign key 제약 조건 위반 하지 못합니다. 일괄 처리 삽입 원자성 이므로 첫 번째 `INSERT` 롤백됩니다, 일괄 처리 삽입 프로세스 이전의 상태로 데이터베이스 시작을 반환 합니다.


## <a name="summary"></a>요약

삭제, 업데이트를 허용 하는 인터페이스가 고 이전 두 자습서를 통해 만든 및 트랜잭션 지원의 데이터 액세스 계층에 추가한 사용 하는 모든 데이터의 일괄 처리 삽입은 [데이터베이스 수정 내용을 래핑 트랜잭션 내에서](wrapping-database-modifications-within-a-transaction-vb.md) 자습서입니다. 특정 시나리오의 경우 이러한 일괄 처리 사용자 인터페이스 크게 효율성을 향상 시킬 최종 사용자 줄여 아래로 클릭, 포스트백 및 키보드 / 마우스 컨텍스트 전환 수에는 기본 데이터의 무결성을 유지 하면서 합니다.

이 자습서는 살펴보겠습니다 일괄 처리 된 데이터를 사용 하 여 작업을 완료 합니다. 자습서의 다음 집합 다양을 한 DAL, 암호화 연결 문자열에서 연결 및 명령 수준 설정 구성 TableAdapter의 메서드를 사용 하는 작업에서 저장된 프로시저를 사용 하는 등 고급 데이터 액세스 계층 시나리오를 살펴봅니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. Hilton Giesenow와 S ren Jacob Lauritsen 된이 자습서에 대 한 검토자를 발생할. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](batch-deleting-vb.md)
