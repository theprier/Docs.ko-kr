---
uid: web-forms/overview/data-access/working-with-batched-data/batch-inserting-vb
title: 일괄 처리 삽입 (VB) | Microsoft Docs
author: rick-anderson
description: 한 번에 여러 데이터베이스 레코드를 삽입 하는 방법을 알아봅니다. 사용자 인터페이스 계층에서 사용자를 여러 n 입력할 수 있도록 GridView 내용을 확장 하였습니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2007
ms.topic: article
ms.assetid: 48e2a4ae-77ca-4208-a204-c38c690ffb59
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-inserting-vb
msc.type: authoredcontent
ms.openlocfilehash: a25c889784ccc6cee3ae01df59bd489b48114e74
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="batch-inserting-vb"></a>일괄 처리 (VB)를 삽입 합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_66_VB.zip) 또는 [PDF 다운로드](batch-inserting-vb/_static/datatutorial66vb1.pdf)

> 한 번에 여러 데이터베이스 레코드를 삽입 하는 방법을 알아봅니다. 사용자 인터페이스 계층에서 사용자를 여러 개의 새 레코드를 입력할 수 있도록 GridView 내용을 확장 하였습니다. 데이터 액세스 계층에서 모든 삽입이 성공적으로 또는 모든 삽입 롤백됩니다 보장 하기 위해 트랜잭션 내에서 여러 삽입 작업을 래핑할 합니다.


## <a name="introduction"></a>소개

에 [일괄 처리 업데이트](batch-updating-vb.md) 자습서 여러 레코드 े न ् न 편집할 수 있는 인터페이스를 제공 하는 GridView 컨트롤의 사용자 지정 살펴보았습니다. 페이지를 방문 하는 사용자 수 일련의 변경 내용 확인 한 다음, 한 번의 단추 클릭으로 일괄 업데이트 합니다. 이러한 인터페이스 한꺼번에 여러 레코드에 사용자가 일반적으로 업데이트 하는 상황에 맞는 무수 한 번의 클릭을 저장할 수 있으며 기본값에 비해 키보드와 마우스-컨텍스트 전환 행에서 뒤로 탐색할 먼저 된 편집 기능이 [는 삽입, 업데이트 및 삭제 하는 데이터의 개요](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 자습서입니다.

이 개념 레코드를 추가 하는 경우에 적용할 수 있습니다. 상상할 여기 Northwind Traders에 일반적으로 수신 운송을 받은 특정 범주에 대 한 제품 개수를 포함 하는 공급 업체에서 합니다. 예를 들어, 우리 도쿄 Traders에서 6 개의 다른 차 및 커피 제품의 배송을 받을 수 있습니다. 사용자가 DetailsView 컨트롤을 통해 한 번에 하나씩 6 개의 제품을 입력 하는 경우 대부분의 동일한 값을 반복 해 서 다시 선택 해야 합니다: 동일한 공급 업체 (도쿄 Traders) 동일한 범주 (음료)를 선택 해야 합니다 (지원 되지 않는 동일한, False) 및 순서 값 (0)에 동일한 단위입니다. 이 반복 되는 데이터 항목은만 시간을 소모 하지 않지만 오류가 발생할 가능성이 높습니다.

약간의 작업으로 일괄 처리 삽입 공급 업체와 범주를 한 번 일련의 제품 이름과 단위 가격이 입력 한 후 데이터베이스에 새 제품을 추가 하는 단추를 클릭을 선택할 수 있도록 해 주는 인터페이스를 만들 수 있습니다 (그림 1 참조). 각 제품에 추가 되 면 해당 `ProductName` 및 `UnitPrice` 데이터 필드는 텍스트 상자에 입력 된 값이 할당 됩니다 하는 동안 해당 `CategoryID` 및 `SupplierID` 값 상위 fo 폼에서 dropdownlist 활용에서 값을 할당 됩니다. `Discontinued` 및 `UnitsOnOrder` 값의 하드 코드 된 값으로 설정 됩니다 `False` 과 0 각각.


[![일괄 처리 삽입 인터페이스](batch-inserting-vb/_static/image2.png)](batch-inserting-vb/_static/image1.png)

**그림 1**: 일괄 처리 삽입 인터페이스 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image3.png))


이 자습서에서는 그림 1에 표시 된 인터페이스를 삽입 하는 일괄 처리를 구현 하는 페이지를 만듭니다. 로 이전 두 자습서에서는 줄 바꿈됩니다 삽입 원자성을 유지 하는 트랜잭션의 범위 내에서. Let s가 시작 되었습니다.

## <a name="step-1-creating-the-display-interface"></a>1 단계: 디스플레이 인터페이스 만들기

이 자습서에서는 두 가지 영역으로 분할 하는 단일 페이지 단계로 구성 됩니다: 디스플레이 지역 및 삽입은 지역입니다. 이 단계에서는 만들겠습니다는 표시 인터페이스는 GridView에 제품을 보여 주고 단추가 프로세스 제품 배송 합니다. 이 단추를 클릭 하면 디스플레이 인터페이스 그림 1에 나와 있는 삽입 인터페이스도 바뀝니다. 취소 단추를 클릭 하거나 디스플레이 인터페이스에서 배송 제품 추가 후 반환 합니다. 2 단계에서에서 삽입 인터페이스를 만들어 보겠습니다.

그 중 하나만 한 번에 표시 하는 두 가지 인터페이스에 페이지를 만드는 경우 각 인터페이스 일반적으로 내에 배치 되는 [패널 웹 컨트롤](http://www.w3schools.com/aspnet/control_panel.asp), 있는 컨테이너 역할을 다른 컨트롤에 대 한 합니다. 따라서, 가격 페이지에는 각 인터페이스에 대 한 두 개의 패널 컨트롤 하나 포함 됩니다.

열어 시작는 `BatchInsert.aspx` 페이지에 `BatchData` 폴더를 끌어 패널 디자이너 도구 상자에서 (그림 2 참조). S 패널 설정 `ID` 속성을 `DisplayInterface`합니다. 디자이너에 패널을 추가 하는 경우 해당 `Height` 및 `Width` 속성을 각각 50px 및 125px로 설정 합니다. 이러한 속성 값은 속성 창에서를 비웁니다.


[![디자이너 도구 상자에서 패널을 끌어 옵니다.](batch-inserting-vb/_static/image5.png)](batch-inserting-vb/_static/image4.png)

**그림 2**: 패널 디자이너 도구 상자에서 끌어 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image6.png))


다음으로, 단추 및 GridView 컨트롤을 패널으로 끌어 옵니다. S 단추 설정 `ID` 속성을 `ProcessShipment` 및 해당 `Text` 프로세스 제품 배송과 속성입니다. GridView s 설정 `ID` 속성을 `ProductsGrid` 및 스마트 태그를 바인딩할 라는 새 ObjectDataSource `ProductsDataSource`합니다. 구성에서 해당 데이터를 가져오도록 ObjectDataSource는 `ProductsBLL` s 클래스 `GetProducts` 메서드. 이 GridView 사용 하 여 데이터를 표시를 삽입, 업데이트에 드롭 다운 목록을 설정 하 고 각 탭 (없음)을 삭제 합니다. 데이터 소스 구성 마법사를 완료 하려면 마침을 클릭 합니다.


[![ProductsBLL 클래스의 GetProducts 메서드에서 반환 되는 데이터를 표시 합니다.](batch-inserting-vb/_static/image8.png)](batch-inserting-vb/_static/image7.png)

**그림 3**:에서 반환 된 데이터 표시는 `ProductsBLL` s 클래스 `GetProducts` 메서드 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image9.png))


[![삽입, 업데이트에서 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제](batch-inserting-vb/_static/image11.png)](batch-inserting-vb/_static/image10.png)

**그림 4**: 드롭 다운 목록에서 업데이트, 삽입 및 삭제 탭 하도록 설정 (None) ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image12.png))


ObjectDataSource 마법사를 완료 한 후 Visual Studio는 BoundFields 및 제품 데이터 필드에 대 한 CheckBoxField를 추가 합니다. 제거 제외한 모두 `ProductName`, `CategoryName`, `SupplierName`, `UnitPrice`, 및 `Discontinued` 필드입니다. 사용자 지정 미적인 자유롭게 합니다. 서식을 지정 하는 `UnitPrice` 통화 값으로 필드는 필드 순서가 다시 매겨지고 이름이 변경 된 필드 중 몇 개 `HeaderText` 값입니다. 또한 GridView 페이징 및 GridView s 스마트 태그에서 페이징 기능 설정 및 정렬 사용 확인란을 선택 하 여 정렬 지원을 포함 하도록 구성 합니다.

패널, 단추, GridView, ObjectDataSource 컨트롤을 추가 하는 GridView의 필드 사용자 지정 후 s 페이지 선언 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](batch-inserting-vb/samples/sample1.aspx)]

열기 및 닫기에 표시할 단추와 GridView에 대 한 태그는 `<asp:Panel>` 태그입니다. 내에서 이러한 컨트롤은는 `DisplayInterface` 패널에서는 숨길 수 s 패널을 설정 하면 `Visible` 속성을 `False`합니다. 3 단계에서는 프로그래밍 방식으로 s 패널 변경 `Visible` 속성 단추에 대 한 응답으로 다른는 숨기 려 하나의 인터페이스를 표시 하려면 클릭 합니다.

잠시 브라우저를 통해 진행률을 볼 수 있습니다. 그림 5에서 볼 수 있듯이 한 번에 10 개의 제품을 나열 하는 GridView 위에 프로세스 제품 배송과 단추가 나타납니다.


[![GridView 제품을 나열 하 고 정렬 하 고 페이징 기능을 제공 합니다.](batch-inserting-vb/_static/image14.png)](batch-inserting-vb/_static/image13.png)

**그림 5**: 제품 및 정렬 제공 및 페이징 기능을 나열 하는 GridView ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image15.png))


## <a name="step-2-creating-the-inserting-interface"></a>2 단계: 삽입 인터페이스 만들기

인터페이스와 함께 표시 완료 준비 된 삽입 인터페이스를 만들 수 있습니다. 이 자습서에 대 한 s 단일 공급 업체와 범주 값을 입력 해야 하 고 다음 사용자를 최대 5 개 제품 이름과 단위 가격 값을 입력을 허용 하는 삽입 인터페이스를 만들 수 있도록 합니다. 이 인터페이스를 사용자 1 ~ 5 개의 새로운 제품 모두 동일한 범주 및 공급 업체를 공유 하지만 고유한 제품 이름 및 가격을 추가할 수 있습니다.

패널 기존 아래에 배치 하는 것은 디자이너 도구 상자에서 끌어 시작 `DisplayInterface` 패널입니다. 설정의 `ID` 속성 패널을 새로 추가 된 `InsertingInterface` 설정 하 고 해당 `Visible` 속성을 `False`합니다. 추가 설정 하는 코드는 `InsertingInterface` 패널 s `Visible` 속성을 `True` 3 단계에서에서 합니다. 또한 s 패널 지울 `Height` 및 `Width` 속성 값입니다.

다음으로, 그림 1에 다시 표시 된 삽입 인터페이스를 만드는 필요 합니다. 다양 한 HTML 기술을 통해이 인터페이스를 만들 수 있지만 매우 간단한 하나를 사용 합니다: 네 개의 열과 7 행 테이블입니다.

> [!NOTE]
> HTML에 대 한 태그를 입력할 때 `<table>` 요소 않겠습니다. 소스 뷰를 사용 합니다. Visual Studio에 추가 하기 위한 도구는 동안 `<table>` 디자이너를 통해 요소를 디자이너 보이는 모든 너무 기꺼이 삽입을 원하지 않는 메일 `style` 태그에 설정 합니다. 만든 후의 `<table>` 태그, 일반적으로 반환 해야 디자이너로 웹 컨트롤을 추가 하 고 해당 속성을 설정 합니다. 정적 HTML을 사용 하 여 원하는 미리 결정된 된 열과 행 테이블을 만들 때 보다는 [Table 웹 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.table.aspx) Table 웹 컨트롤 내에 있는 웹 컨트롤만 액세스할 수 있으므로 사용 하는 `FindControl("controlID")` 패턴입니다. 그러나 Table 웹 컨트롤을 프로그래밍 방식으로 생성할 수 있습니다. 이후 동적으로 크기의 테이블 (텍스처를 행 또는 열 일부 데이터베이스 또는 사용자 지정 기준에 기반)에 대 한 테이블 웹 컨트롤 사용을 않습니다.


내에서 다음 태그를 입력에서 `<asp:Panel>` 의 태그는 `InsertingInterface` 패널:


[!code-html[Main](batch-inserting-vb/samples/sample2.html)]

이 `<table>` 태그에는 모든 웹 컨트롤이 아직 일시적으로 추가 하는 것입니다. 각 `<tr>` 요소 포함 특정 CSS 클래스 설정: `BatchInsertHeaderRow` 공급 업체와 범주 dropdownlist 활용 됩니다 어디로; 머리글 행에 대 한 `BatchInsertFooterRow` 교대로 반복 되는 및에서 배송 및 취소 단추 추가 제품 됩니다 어디로; 바닥글 행에 대 한 `BatchInsertRow` 및 `BatchInsertAlternatingRow` 제품 및 단위를 포함 하는 행에 대 한 값 가격 TextBox 컨트롤입니다. I에 해당 하는 CSS 클래스를 생성 했습니다는 `Styles.css` GridView 및 DetailsView 비슷한 모양의 삽입 인터페이스를 제공할 수 파일을 제어 했습니다 이러한 자습서 전체에서 사용 했습니다. 이러한 CSS 클래스 아래에 표시 됩니다.


[!code-css[Main](batch-inserting-vb/samples/sample3.css)]

입력이 태그로 디자인 보기로 돌아가 합니다. 이 `<table>` 그림 6와 같이 네 개의 열과 7 행 테이블 디자이너를 표시 해야 합니다.


[![인터페이스 삽입은 구성의 열을 4-7 행 테이블](batch-inserting-vb/_static/image17.png)](batch-inserting-vb/_static/image16.png)

**그림 6**: The 삽입 인터페이스에 구성 된 열, 4-7 행 테이블 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image18.png))


지금 다시 우리 삽입 인터페이스에 웹 컨트롤을 추가할 준비가 되었습니다. 공급자 및 범주에 대 한 테이블에 적절 한 셀에 도구 상자에서 두 개의 dropdownlist 활용을 끕니다.

설정 공급자 DropDownList s `ID` 속성을 `Suppliers` 라는 새 ObjectDataSource 바인딩할 `SuppliersDataSource`합니다. 구성에서 데이터를 검색 하도록 새 ObjectDataSource는 `SuppliersBLL` s 클래스 `GetSuppliers` 메서드와 업데이트 집합 탭 (없음)으로 s 드롭 다운 목록입니다. 마법사를 완료 하려면 마침을 클릭 합니다.


[![ObjectDataSource SuppliersBLL 클래스의 GetSuppliers 메서드를 사용 하도록 구성](batch-inserting-vb/_static/image20.png)](batch-inserting-vb/_static/image19.png)

**그림 7**: 구성에 사용 하 여 ObjectDataSource는 `SuppliersBLL` s 클래스 `GetSuppliers` 메서드 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image21.png))


있어야는 `Suppliers` DropDownList 표시는 `CompanyName` 데이터 필드와 사용은 `SupplierID` 으로 데이터 필드의 `ListItem`의 값입니다.


[![CompanyName 데이터 필드를 표시 하 고 공급 업체 Id 값으로 사용](batch-inserting-vb/_static/image23.png)](batch-inserting-vb/_static/image22.png)

**그림 8**: 표시 된 `CompanyName` 데이터 필드와 사용 하 여 `SupplierID` 값으로 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image24.png))


두 번째 DropDownList 이름을 `Categories` 라는 새 ObjectDataSource 바인딩할 `CategoriesDataSource`합니다. 구성는 `CategoriesDataSource` ObjectDataSource 사용 하는 `CategoriesBLL` s 클래스 `GetCategories` 마법사를 완료 하려면 마침 방법으로, 집합 드롭 다운 목록에서 UPDATE 및 DELETE 탭 (없음)을 클릭 합니다. 마지막으로,은 DropDownList 표시는 `CategoryName` 데이터 필드와 사용 하 여는 `CategoryID` 값으로.

이러한 두 dropdownlist 활용을 추가 하 고 적절 하 게 구성 된 ObjectDataSources에 바인딩된 한 후 화면 그림 9 비슷해야 합니다.


[![공급 업체 및 범주 dropdownlist 활용에 이제 머리글 행 포함](batch-inserting-vb/_static/image26.png)](batch-inserting-vb/_static/image25.png)

**그림 9**: The 머리글 행 이제 포함 된 `Suppliers` 및 `Categories` dropdownlist 활용 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image27.png))


이제 입력란의 이름 및 새 각 제품에 대 한 가격을 수집 하도록 만드는 해야 합니다. 디자이너 도구 상자에서 각 5 개 제품 이름과 가격 행에 대 한 TextBox 컨트롤을 끕니다. 설정의 `ID` 를 입력란의 속성 `ProductName1`, `UnitPrice1`, `ProductName2`, `UnitPrice2`, `ProductName3`, `UnitPrice3`등입니다.

CompareValidator 단가 설정 입력란의 각 추가 `ControlToValidate` 속성을 적절 한 `ID`합니다. 설정의 `Operator` 속성을 `GreaterThanEqual`, `ValueToCompare` 0으로 및 `Type` 를 `Currency`합니다. 이러한 설정은 되는지 알아보려면 가격을 입력 하는 경우 올바른 통화 값을 0 보다 크거나 CompareValidator 지시 합니다. 설정의 `Text` 속성을 \*, 및 `ErrorMessage` 가격에는 0 보다 크거나 이어야 합니다. 또한 모든 통화 기호를 생략 하세요.

> [!NOTE]
> 삽입 인터페이스 RequiredFieldValidator 컨트롤이 모든 경우에 포함 되지 않습니다는 `ProductName` 필드에 `Products` 데이터베이스 테이블에서는 `NULL` 값입니다. 즉, 사용자가 최대 5 개 제품 입력 주시기 바랍니다. 예를 들어 처음 세 개의 행에 대 한 제품 이름과 단위 가격을 제공 하는 사용자가을 하는 경우 마지막 두 개의 행을 비워 d 방금 추가 세 개의 새로운 제품 시스템에 있습니다. 하지만 이후 `ProductName` 가 필요 해야 합니다 프로그래밍 방식으로 해당 제품 이름 값이 제공 입력은 단가 확인을 확인 합니다. 4 단계에서에서이 검사를 해결할 합니다.


S 사용자 입력의 유효성을 검사할 때 값에 통화 기호를 포함 하는 경우는 CompareValidator 잘못 된 데이터를 보고 합니다. $ 단가 가격을 입력할 때 통화 기호를 생략 하려면 사용자에 게 지시 하는 시각적 표시로 사용할 입력란의 각 앞에 추가 합니다.

ValidationSummary 컨트롤 내에서 마지막으로, 추가 `InsertingInterface` 패널에서 설정 해당 `ShowMessageBox` 속성을 `True` 및 해당 `ShowSummary` 속성을 `False`합니다. 이러한 설정을 사용 하 여 사용자가 잘못 된 단위 가격 값을 입력 하는 경우 별표 잘못 된 TextBox 컨트롤 옆에 있는 표시 되 고 ValidationSummary는 앞에서 지정한 오류 메시지를 표시 하는 클라이언트 쪽 messagebox를 표시 합니다.

이 시점에서 화면 그림 10에 비슷해야 합니다.


[![제품에 대 한 삽입 인터페이스 이제에 포함 되어 입력란 이름과 가격](batch-inserting-vb/_static/image29.png)](batch-inserting-vb/_static/image28.png)

**그림 10**: The 삽입 인터페이스 이제 포함 입력란 제품 이름과 가격에 대 한 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image30.png))


다음 바닥글 행에 배송 및 취소 단추 추가 제품을 추가 해야 합니다. 단추 끌어 두 제어 도구 상자에서 삽입 인터페이스의 바닥글에는 단추 설정 `ID` 속성을 `AddProducts` 및 `CancelButton` 및 `Text` 배송 및 취소에서 제품을 각각 추가할 속성입니다. 또한 설정는 `CancelButton` 컨트롤 s `CausesValidation` 속성을 `false`합니다.

마지막으로, 두 인터페이스에 대 한 상태 메시지를 표시 하는 Label 웹 컨트롤을 추가 해야 합니다. 예를 들어 사용자가 제품의 새로운 배송에 성공적으로 추가 하는 경우 하려고 디스플레이 인터페이스를 반환 하 고 확인 메시지를 표시 합니다. 하지만 이후에 경고 메시지를 표시 해야 사용자는 제품 이름 해제 하지만 새 제품에 대 한 가격을 제공 하면 하는지는 `ProductName` 필드는 필수입니다. 두 인터페이스를 표시 하려면이 메시지를 필요 하므로 패널 외부 페이지의 위쪽에 배치 합니다.

도구 상자에서 디자이너에 있는 페이지의 맨 위에 Label 웹 컨트롤을 끕니다. 설정는 `ID` 속성을 `StatusLabel`아웃 일반는 `Text` 속성과 집합은 `Visible` 및 `EnableViewState` 속성을 `False`합니다. 이전 자습서에서 살펴본 대로 설정 된 `EnableViewState` 속성을 `False` 를 프로그래밍 방식으로 s 레이블 속성 값을 변경 하 고 자동으로 후속 포스트백에서 기본값으로로 되돌아갈 수 있습니다. 후속 포스트백에서 사라집니다 일부 사용자 동작에 대 한 응답에 상태 메시지를 표시 하기 위한 코드를 간소화 합니다. 마지막으로 설정 된 `StatusLabel` 컨트롤 s `CssClass` 에 정의 된 속성을 경고 하는 CSS 클래스의 이름인 `Styles.css` 큰, 기울임꼴, 굵게, 빨강 글꼴의 텍스트를 표시 하 합니다.

그림 11 레이블을 추가 및 구성 된 후 Visual Studio 디자이너를 보여 줍니다.


[![두 개의 패널 컨트롤 위에 StatusLabel 컨트롤 배치](batch-inserting-vb/_static/image32.png)](batch-inserting-vb/_static/image31.png)

**그림 11**: 현재 위치는 `StatusLabel` 컨트롤 위에 두 개의 패널 컨트롤 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image33.png))


## <a name="step-3-switching-between-the-display-and-inserting-interfaces"></a>3 단계: 디스플레이 삽입 인터페이스 간 전환

이 시점에서 우리의 표시 및 두 개의 작업 엄청 인터페이스 했지만 다시 삽입을 위한 태그를 완성 했습니다.

- 표시를 전환 하 고 인터페이스를 삽입 합니다.
- 데이터베이스에 배송 중에 제품 추가

현재 디스플레이 인터페이스는 표시 하지만 삽입 인터페이스 숨겨집니다. 때문에 이것이 `DisplayInterface` 패널 s `Visible` 속성이로 설정 되어 `True` (기본값) 동안는 `InsertingInterface` 패널 s `Visible` 속성이로 설정 되어 `False`합니다. 단순히 각 컨트롤 s 설정/해제 해야 하는 두 인터페이스 간에 전환 하려면 `Visible` 속성 값입니다.

프로세스 제품 배송과 단추를 클릭할 때 삽입 인터페이스 표시 인터페이스에서 이동 하려고 합니다. 따라서이 단추 s에 대 한 이벤트 처리기를 만들고 `Click` 다음 코드를 포함 하는 이벤트:


[!code-vb[Main](batch-inserting-vb/samples/sample4.vb)]

이 코드는 단순히 숨깁니다는 `DisplayInterface` 패널과 표시는 `InsertingInterface` 패널입니다.

다음으로 삽입 인터페이스에서 배송 및 취소 단추 컨트롤에서 추가 제품에 대 한 이벤트 처리기를 만듭니다. 이 단추 중 하나를 클릭 하면 디스플레이 인터페이스 다시 돌아가려면 해야 합니다. 만들 `Click` 모두에 대 한 이벤트 처리기 호출 되도록 단추 제어 `ReturnToDisplayInterface`, 일시적으로 추가 하는 방법입니다. 숨기기 외에 `InsertingInterface` 패널 및 표시는 `DisplayInterface` 패널의 `ReturnToDisplayInterface` 메서드를 미리 편집 상태로 웹 컨트롤을 반환 해야 합니다. dropdownlist 활용을 설정 하는 것이 `SelectedIndex` 속성을 0과 정리는 `Text` TextBox 컨트롤의 속성입니다.

> [!NOTE]
> 어떤 일이 발생 하는 것이 좋습니다. 경우 म 않았음에도 t 디스플레이 인터페이스를 반환 하기 전에 미리 편집 상태로 컨트롤을 반환 합니다. 사용자 수 프로세스 제품 배송과 단추를 클릭 제품의 배송에서 입력을 배송에서 추가 제품을 클릭 한 다음. 이 제품을 추가 하 고 디스플레이 인터페이스를 사용자가을 반환 합니다. 이 시점에서 사용자가 다른 배송을 추가 해야 합니다. 삽입 인터페이스 하지만 DropDownList 되돌아가 프로세스 제품 배송과 단추 클릭 하면 선택 항목 및 입력란 값은 여전히으로 채울 수 이전 값.


[!code-vb[Main](batch-inserting-vb/samples/sample5.vb)]

둘 다 `Click` 이벤트 처리기를 호출 하기만 하면는 `ReturnToDisplayInterface` 메서드를 하겠습니다로 반환 하는 제품 추가에서 배송 있지만 `Click` 이벤트 처리기에서 4 단계 하 고 코드를 추가 하는 제품을 저장 합니다. `ReturnToDisplayInterface` 반환 하 여 시작 되는 `Suppliers` 및 `Categories` 가 첫 번째 옵션을 dropdownlist 활용 합니다. 두 개 상수 `firstControlID` 및 `lastControlID` 시작 및 끝 입력란 삽입 인터페이스와의 경계에서 사용 되 제품 이름과 단위 가격이 명명에 사용 되는 컨트롤 인덱스 값을 표시는 `For` 는 를설정하는루프`Text`TextBox 컨트롤의 속성을 빈 문자열로 백업 합니다. 마지막으로, 패널 `Visible` 표시 된 디스플레이 인터페이스 및 삽입 인터페이스가 숨겨진다는 있도록 속성이 다시 설정 됩니다.

브라우저에서이 페이지를 테스트해 보십시오. 그림 5에 표시 된 대로 먼저 페이지를 방문 하는 경우 디스플레이 인터페이스를 표시 됩니다. 프로세스 제품 배송과 단추를 클릭 합니다. 페이지에서 포스트백 고 이제 표시 삽입 인터페이스 그림 12에 나와 있는 것 처럼 합니다. 중의 추가 제품 배송 또는 취소 단추를 클릭 하면 디스플레이 인터페이스를 반환 합니다.

> [!NOTE]
> 삽입 인터페이스를 보면서 CompareValidators 단가 텍스트 상자에을 테스트 하려면 보십시오. 잘못 된 통화 값으로 배송 단추나 가격은 0 보다 작은 값에서 추가 제품을 클릭 하면 경고 클라이언트 쪽 messagebox를 표시 되어야 합니다.


[![삽입 인터페이스가 처리 제품 배송 단추를 클릭 한 후 표시](batch-inserting-vb/_static/image35.png)](batch-inserting-vb/_static/image34.png)

**그림 12**: 프로세스 제품 배송 단추를 클릭 한 후의 삽입 인터페이스가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image36.png))


## <a name="step-4-adding-the-products"></a>4 단계: 추가 제품

이 자습서는 제품 저장 하 고 데이터베이스에 제품 추가 '에서 배송 단추 s에 대해 남아 있는 모든 `Click` 이벤트 처리기입니다. 만들어서이 작업을 수행할 수 있습니다는 `ProductsDataTable` 추가 하 고는 `ProductsRow` 각 제품 이름 제공 됨에 대 한 인스턴스. 이러한 두 번 `ProductsRow` 추가 되었는지를에 대 한 호출을 만듭니다는 `ProductsBLL` s 클래스 `UpdateWithTransaction` 전달 메서드는 `ProductsDataTable`합니다. 이전에 설명한 대로 `UpdateWithTransaction` 에 다시 생성 된 메서드는 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](wrapping-database-modifications-within-a-transaction-vb.md) 자습서, 전달은 `ProductsDataTable` 에 `ProductsTableAdapter` s `UpdateWithTransaction` 메서드. 여기에서는 ADO.NET 트랜잭션이 시작 되 고 TableAdatper 문제는 `INSERT` 데이터베이스에 추가 된 각 문을 `ProductsRow` DataTable의 합니다. 모든 제품 오류 없이 추가 되 고 트랜잭션이 커밋될 때 가정, 그렇지 않으면 롤백됩니다.

배송 단추 s에서 추가 제품에 대 한 코드 `Click` 이벤트 처리기도 약간의 오류 검사를 수행 해야 합니다. 없는 RequiredFieldValidators 삽입 인터페이스에서 사용 되므로 입력할 수 있습니다 된 가격으로 제품에 대 한 해당 이름을 생략 하는 동안 합니다. S 제품 이름을 필수 이므로 이러한 조건을 펼칩니다 사용자 경고 및 작업을 진행할 삽입 해야 합니다. 전체 `Click` 이벤트 처리기 코드 뒤에 오는:


[!code-vb[Main](batch-inserting-vb/samples/sample6.vb)]

이벤트 처리기는 다음을 통해 시작 되는 `Page.IsValid` 속성의 값을 반환 `True`합니다. 반환 하는 경우 `False`, 다음 하나를 의미 하는 또는 잘못 된 데이터를 보고 하는 CompareValidators 중,이 경우에서는 하지 않을 입력 한 제품을 삽입 하기 위해 또는 म 남게 됩니다 예외와 함께 사용자가 입력 한 단가 할당 하려고 하면 값을 `ProductsRow` s `UnitPrice` 속성입니다.

다음, 새 `ProductsDataTable` 인스턴스가 생성 됩니다 (`products`). A `For` 루프를 사용 하 여 제품 이름과 단위 가격이 입력란을 반복 하 고 `Text` 속성에서 읽어 들이는 지역 변수 `productName` 및 `unitPrice`합니다. 사용자가 해당 제품 이름 아니라 단위 가격에 대 한 값을 입력 하는 경우는 `StatusLabel` 제품의 이름을 포함 하는 메시지 하는 단위 가격을 제공 하는 경우 수행 해야 하는 표시 및 이벤트 처리기를 종료 합니다.

제품 이름을 제공 된 경우, 새 `ProductsRow` 인스턴스가 사용 하 여 생성 되는 `ProductsDataTable` s `NewProductsRow` 메서드. 이 새로운 `ProductsRow` 인스턴스 s `ProductName` 현재 제품 속성 이름을 지정 하는 동안 텍스트 상자는 `SupplierID` 및 `CategoryID` 속성에 할당 된는 `SelectedValue` 삽입 인터페이스의 헤더에 dropdownlist 활용의 속성입니다. 할당 된 사용자의 s 제품 가격에 대 한 값을 입력 하면는 `ProductsRow` 인스턴스 s `UnitPrice` 속성; 속성은 그렇지 않은 경우 져 왼쪽 할당 하지 않은 경우는 `NULL` 에 대 한 값 `UnitPrice` 데이터베이스에 합니다. 마지막으로 `Discontinued` 및 `UnitsOnOrder` 속성 하드 코드 된 값에 할당 된 `False` , 0, 각각.

속성에 할당 된 후의 `ProductsRow` 에 추가 되는 인스턴스는 `ProductsDataTable`합니다.

완료는 `For` 루프 확인 제품을 모두 추가 되었습니다. 사용자 수, 즉, 모든 제품 이름이 나 가격으로 유입 되기 전에 배송에서 추가 제품 클릭 했습니다. 하나 이상의 제품의 경우는 `ProductsDataTable`, `ProductsBLL` s 클래스 `UpdateWithTransaction` 메서드를 호출 합니다. 데이터를 다시 바인딩할는 다음으로 `ProductsGrid` GridView 새로 추가 된 제품 디스플레이 인터페이스에 표시 되도록 합니다. `StatusLabel` 확인 메시지를 표시 하도록 업데이트 됩니다 및 `ReturnToDisplayInterface` 인터페이스를 삽입 하 고 디스플레이 인터페이스를 보여 주는 숨기기 호출 됩니다.

제품이 입력 된 삽입 인터페이스 제품이 추가 된 메시지를 제외한 표시 된 상태로 유지 됩니다. 제품 이름을 입력 하 고 단가 텍스트 상자에 표시 됩니다.

그림 13, 14 및 15의 표시는 삽입 및 동작에서 인터페이스를 표시 합니다. 그림 13에서는 사용자가 제품 이름에 해당 하지 않고 단위 가격 값을 입력 합니다. 그림 14 인터페이스를 보여 줍니다 디스플레이 3 새 제품 요소가 추가 되었지만, 그림 15 (이전 페이지는 세 번째) GridView에서 두 새로 추가 된 제품을 보여 줍니다.


[![제품 이름은 필요한 경우 입력 Unit Price](batch-inserting-vb/_static/image38.png)](batch-inserting-vb/_static/image37.png)

**그림 13**: A 제품 이름이 필요한 경우 입력 Unit Price ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image39.png))


[![공급자에 대 한 추가 된 3 개의 새 Veggies 유미 식품 s](batch-inserting-vb/_static/image41.png)](batch-inserting-vb/_static/image40.png)

**그림 14**: 3 개의 새 Veggies 추가 된 공급 업체 유미 식품 s에 대 한 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image42.png))


[![GridView의 마지막 페이지에서 새 제품을 찾을 수 있습니다.](batch-inserting-vb/_static/image44.png)](batch-inserting-vb/_static/image43.png)

**그림 15**:의 새 제품 있습니다 GridView의 마지막 페이지에서 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image45.png))


> [!NOTE]
> 이 자습서에 사용 되는 논리를 삽입 하는 일괄 처리는 트랜잭션의 범위 내에서 삽입을 래핑합니다. 이 확인 하려면 데이터베이스 수준 오류에 대해 의도적으로. 새 할당 하는 대신에 예를 들어 `ProductsRow` 인스턴스 s `CategoryID` 속성에서 선택된 된 값에는 `Categories` DropDownList를 같은 값으로 할당 `i * 5`합니다. 여기 `i` 루프 인덱서 이며 1부터 5 까지의 값입니다. 그러므로 경우 첫 번째 제품을 삽입 하는 일괄 처리에서 둘 이상의 제품을 추가 해야 합니다는 유효한 `CategoryID` 값 (5), 있지만 후속 제품 `CategoryID` 최대 일치 하지 않는 값 `CategoryID` 값에 `Categories` 테이블입니다. 한 순수 효과 하는 동안 첫 번째 `INSERT` 성공 하 고 나머지는 외래 키 제약 조건 위반으로 실패 합니다. 일괄 처리 삽입 원자성 이므로 첫 번째 `INSERT` 다시 롤백되며, 시작 된 일괄 처리 프로세스를 삽입 하기 전에 상태로 데이터베이스를 반환 합니다.


## <a name="summary"></a>요약

업데이트, 삭제, 사용할 수 있는 인터페이스에서 만든이 및 이전 두 자습서를 통해 및의 데이터 액세스 계층에 추가한 트랜잭션 지원은 모두 사용 데이터의 일괄 처리를 삽입 하는 [래핑 데이터베이스 수정 트랜잭션 내에서](wrapping-database-modifications-within-a-transaction-vb.md) 자습서입니다. 특정 시나리오에서는 이러한 일괄 처리 사용자 인터페이스 크게 효율성을 향상 시킬 최종 사용자도 기본 데이터의 무결성을 유지 하면서 클릭, 포스트백 및 키보드와 마우스-컨텍스트 전환 수에 다운 가공 합니다.

이 자습서 모양에 일괄 처리 된 데이터 작업을 완료 합니다. 다양 한 DAL, 암호화 연결 문자열 등의 연결 및 명령 수준 설정을 구성 하는 TableAdapter의 메서드에서 저장된 프로시저를 사용 하는 등 고급 데이터 액세스 계층 시나리오를 탐색 하는 자습서의 다음 집합!

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 Hilton Giesenow 및 S ren 야곱의 Lauritsen 된 검토자를 될 있습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](batch-deleting-vb.md)
