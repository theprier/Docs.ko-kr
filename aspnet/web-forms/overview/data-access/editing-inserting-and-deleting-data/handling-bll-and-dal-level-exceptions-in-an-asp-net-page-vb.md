---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb
title: ASP.NET (VB) 페이지에서 BLL 및 DAL 수준의 예외 처리 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 삽입, 업데이트 또는 삭제 작업을 하는 동안 예외가 발생 해야 표시, 정보 오류 메시지를 표시 하는 방법에 살펴보겠습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/17/2006
ms.topic: article
ms.assetid: 129d4338-1315-4f40-89b5-2b84b807707d
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 41a0ec0db4cb2093d7fadd2de7e65ee4874f0063
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37394685"
---
<a name="handling-bll--and-dal-level-exceptions-in-an-aspnet-page-vb"></a>ASP.NET (VB) 페이지에서 BLL 및 DAL 수준의 예외 처리
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_18_VB.exe) 또는 [PDF 다운로드](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/datatutorial18vb1.pdf)

> 이 자습서는 insert, update 또는 ASP.NET 데이터 웹 컨트롤의 삭제 작업 동안 예외가 발생 해야 친숙 하 고 정보 오류 메시지를 표시 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

계층화 된 응용 프로그램 아키텍처를 사용 하 여 ASP.NET 웹 응용 프로그램에서 데이터를 사용 하 여 작업 세 가지 일반 단계를 다음과 같습니다.

1. 비즈니스 논리 계층의 어떤 메서드를 호출 해야 하 고 전달 하는 매개 변수 값을 결정 합니다. 사용자가 입력 한 입력 또는 매개 변수 값을 하드 코드 된, 프로그래밍 방식으로 할당을 수 있습니다.
2. 메서드를 호출합니다.
3. 결과 처리 합니다. 데이터를 반환 하는 BLL 메서드를 호출할 때 데이터 웹 컨트롤에 데이터 바인딩이 수행할 수 있습니다. 데이터를 수정 하는 BLL 메서드의 반환 값을 기준으로 또는 2 단계에서에서 발생 하는 모든 예외를 처리 하는 정상적으로 일부 작업을 수행 포함 됩니다.

설명한 것 처럼 합니다 [이전 자습서](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md), ObjectDataSource와 데이터 웹 컨트롤 1 단계 및 3에 대 한 확장성 지점을 제공 합니다. GridView, 예를 들어 발생 합니다. 해당 `RowUpdating` 이벤트는 ObjectDataSource에 해당 필드 값을 할당 하기 전에 `UpdateParameters` 컬렉션 해당 `RowUpdated` ObjectDataSource 작업 완료 이벤트가 발생 합니다.

1 단계 중에 발생 하는 사용할 수 있는 방법이 입력된 매개 변수를 사용자 지정 하거나 작업을 취소 하는 데 적 이벤트를 이미 살펴보았습니다. 이 자습서는 작업이 완료 된 후 실행 하는 이벤트에 살펴보겠습니다. 무엇 보다도 원하므로 이러한 후 수준 이벤트 처리기를 사용 하 여 작업 하는 동안 예외가 발생 하는 경우를 확인 하 고 표준 asp.net 기본값으로 지정 하는 것이 아니라 화면에 정보를 제공 하 고 친숙 한 오류 메시지를 표시 합니다. 정상적으로 처리 예외 페이지입니다.

작업 후 수준 이벤트를 보여 주기 위해 제품을 편집할 수 있는 GridView에 나열 된 페이지를 만들어 보겠습니다. 예외인 경우는 제품을 업데이트 하는 ASP.NET를 발생 하는 경우 페이지에 문제가 발생 했음을 설명 하는 GridView 위에 짧은 메시지가 표시 됩니다. 이제 시작 하겠습니다.

## <a name="step-1-creating-an-editable-gridview-of-products"></a>1 단계: 제품을 편집할 수 있는 GridView 만들기

이전 자습서에서 두 개의 필드만 사용 하 여 편집할 수는 GridView 만든 `ProductName` 고 `UnitPrice`입니다. 이 필수 만들기에 대 한 추가 오버 로드는 `ProductsBLL` 클래스의 `UpdateProduct` 메서드를 세 개의 입력된 매개 변수 (제품의 이름, 단가 및 ID)과 달리 매개 변수 각 product 필드를 허용 하는 것입니다. 이 자습서에서는 재고 제품의 이름, unit, unit price 및 단위 당 수량을 표시 하지만 이름, 단가 및 단위를 편집할 수는 재고 허용 하는 편집 가능한 GridView를 만들어이 기법을 다시를 연습해 보겠습니다.

이 시나리오에 맞게 다른 오버 로드 해야는 `UpdateProduct` 메서드, 4 개의 매개 변수를 취하는: 제품의 이름, 단가, 재고 및 ID 단위 다음 메서드를 추가 합니다 `ProductsBLL` 클래스:


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample1.vb)]

이 메서드 완료를에서는 이러한 네 가지 특정 제품 필드를 편집할 수 있도록 하는 ASP.NET 페이지를 만들 준비가 된 것입니다. 열기를 `ErrorHandling.aspx` 페이지는 `EditInsertDelete` 폴더 디자이너를 통해 페이지에 GridView를 추가 합니다. GridView 새 ObjectDataSource를 바인딩할 매핑 합니다 `Select()` 메서드를 합니다 `ProductsBLL` 클래스의 `GetProducts()` 메서드 및 `Update()` 메서드를는 `UpdateProduct` 방금 만든 오버 로드.


[![네 개의 입력된 매개 변수를 받아들이는 UpdateProduct 메서드와 같이 오버 로드를 사용 하 여](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image2.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image1.png)

**그림 1**: 사용 된 `UpdateProduct` 메서드 오버 로드는 허용 네 개의 입력 매개 변수 ([클릭 하 여 큰 이미지 보기](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image3.png))


사용 하 여 ObjectDataSource 만들어집니다는 `UpdateParameters` 각 제품 필드에 대 한 4 개의 매개 변수 및 필드를 사용 하 여 GridView를 사용 하 여 컬렉션입니다. ObjectDataSource의 선언 태그 할당 합니다 `OldValuesParameterFormatString` 속성 값을 `original_{0}`, BLL 클래스의 명명 된 입력된 매개 변수를 예상 하지 되므로 예외가 발생 하는 `original_productID` 전달할 합니다. 이 설정을 완전히 선언적 구문에서 제거할 것을 잊지 마세요 (기본 값으로 설정 하거나 `{0}`).

그런 다음만 포함 하도록 GridView를 줄이려면 합니다 `ProductName`, `QuantityPerUnit`를 `UnitPrice`, 및 `UnitsInStock` BoundFields 합니다. 또한 자유롭게 적용 필요 하다 고 판단할 서식 필드 수준 (변경 하는 등의 `HeaderText` 속성).

이전 자습서에서 살펴보았습니다 서식 지정 방법을 `UnitPrice` 모두 읽기 전용 모드와 편집 모드에서 통화로 BoundField 합니다. 동일한 여기를 보겠습니다. 이 BoundField의 설정 필수 회수 `DataFormatString` 속성을 `{0:c}`, 해당 `HtmlEncode` 속성을 `false`, 및 해당 `ApplyFormatInEditMode` 에 `true`그림 2에 나와 있는 것 처럼 합니다.


[![통화로 표시할 UnitPrice BoundField 구성](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image5.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image4.png)

**그림 2**: 구성 된 `UnitPrice` 통화로 표시할 BoundField ([클릭 하 여 큰 이미지 보기](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image6.png))


서식 지정 된 `UnitPrice` GridView의에 대 한 이벤트 처리기를 만들고 편집 인터페이스에는 통화의 요구에 따라 `RowUpdating` 통화 형식 문자열을 구문 분석 하는 이벤트를 `decimal` 값입니다. 이전에 설명한 대로 합니다 `RowUpdating` 마지막 자습서에서 이벤트 처리기도 있는지 확인 하는 사용자가 제공한는 `UnitPrice` 값입니다. 그러나이 자습서에 대 한 허용 해 보겠습니다 가격을 생략 하는 사용자입니다.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample2.vb)]

우리의 GridView를 포함 한 `QuantityPerUnit` BoundField 있지만이 BoundField 표시 용도로 이어야 하며 사용자가 편집할 수 없습니다. 이 정렬 하려면 BoundFields'를 설정 하기만 `ReadOnly` 속성을 `true`입니다.


[![읽기 전용으로 QuantityPerUnit BoundField 설정](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image8.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image7.png)

**그림 3**: 확인 합니다 `QuantityPerUnit` BoundField 읽기 전용 ([클릭 하 여 큰 이미지 보기](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image9.png))


GridView의 스마트 태그에서 편집 사용 확인란을 마지막으로 확인 합니다. 다음이 단계를 완료 한 후의 `ErrorHandling.aspx` 페이지의 디자이너는 그림 4와 비슷하게 표시 됩니다.


[![남기고 모두 제거 필요한 BoundFields 및 확인 확인란 편집 사용](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image11.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image10.png)

**그림 4**: 제거 하지만 모든 the 필요한 BoundFields 및 확인란을 사용 하도록 설정 편집 ([큰 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image12.png))


그러나이 시점에서 모든 제품의 목록이 있다고 `ProductName`, `QuantityPerUnit`, `UnitPrice`, 및 `UnitsInStock` ; 필드만 합니다 `ProductName`, `UnitPrice`, 및 `UnitsInStock` 필드를 편집할 수 있습니다.


[![사용자가 이제 쉽게 편집할 수 제품의 이름, 가격 및 주식 필드 단위](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image14.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image13.png)

**그림 5**: 사용자 수 이제 쉽게 편집 제품의 이름, 가격 및 필드 재고에서 단위 ([큰 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image15.png))


## <a name="step-2-gracefully-handling-dal-level-exceptions"></a>2 단계: DAL 수준의 예외를 정상적으로 처리

사용자 편집된 제품의 이름, 가격 및 재고 단위에 대 한 올바른 값을 입력 하는 경우 편집할 수는 GridView 쌓아가는 작동을 하는 동안 잘못 된 값을 입력 하면 예외가 발생 합니다. 예를 들어, 생략를 `ProductName` 원인 값을 [NoNullAllowedException](https://msdn.microsoft.com/library/default.asp?url=/library/cpref/html/frlrfsystemdatanonullallowedexceptionclasstopic.asp) 이후 throw 될 수는 `ProductName` 속성에는 `ProdcutsRow` 클래스에 해당 `AllowDBNull` 속성이로 설정 `false`같으면는 데이터베이스 다운 된 경우는 `SqlException` 데이터베이스에 연결 하려고 할 때 TableAdapter에서 throw 됩니다. 작업을 수행 하지 않고 이러한 예외 버블링 데이터 액세스 계층에서 비즈니스 논리 계층으로 다음 ASP.NET 페이지에 마지막으로 ASP.NET 런타임에서 합니다.

웹 응용 프로그램은 구성 하는 방법 및 응용 프로그램을 방문 하는 여부에 따라 `localhost`, 일반 서버 오류 페이지, 자세한 오류 보고서 또는 친숙 한 웹 페이지에서 처리 되지 않은 예외가 발생할 수 있습니다. 참조 [웹 응용 프로그램 오류 처리 ASP.NET](http://www.15seconds.com/issue/030102.htm) 하며 [customErrors 요소](https://msdn.microsoft.com/library/h0hfz6fc(VS.80).aspx) ASP.NET 런타임 예외로에 응답 하는 방법에 대 한 자세한 내용은 합니다.

그림 6을 지정 하지 않고 제품을 업데이트 하려고 시도할 때 발생 하는 화면을 보여 줍니다.는 `ProductName` 값입니다. 자세한 오류 보고서를 통해 들어오는 경우에 표시 된 기본 `localhost`입니다.


[![예외 세부 정보를 표시는 제품의 이름을 생략합니다.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image17.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image16.png)

**그림 6**: 제품의 이름을 예외 세부 정보를 표시를 생략 하면 ([큰 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image18.png))


이러한 예외 세부 정보는 응용 프로그램을 테스트할 때 유용한, 예외가 발생 하는 경우 이러한 화면을 사용 하 여 최종 사용자를 표시는 그다지 적합 합니다. 가능성이 높은 최종 사용자가 무엇 인지 인식 하지는 `NoNullAllowedException` 는 또는 발생 했습니다. 제품을 업데이트 하는 동안 문제가 발생 했습니다를 설명 하는 보다 친숙 한 메시지를 사용 하 여 사용자를 표시 하는 것이 좋습니다.

작업을 수행할 때 예외가 발생 하는 경우 ObjectDataSource와 데이터 웹 컨트롤에서 사후 수준 이벤트를 검색 하 고 ASP.NET 런타임이 확산에서 예외를 취소 하는 방법을 제공 합니다. 예를 들어 보겠습니다 이벤트 처리기를 만들고 gridview의 `RowUpdated` 이벤트 및 결정 하는 경우 예외가 발생 한, 그렇다면 레이블 웹 컨트롤에서 예외 정보를 표시 합니다.

시작 설정, ASP.NET 페이지에 레이블을 추가 하 여 해당 `ID` 속성을 `ExceptionDetails` 정리 및 해당 `Text` 속성입니다. 설정 하려면이 메시지에 사용자의 눈을 그리려면, 해당 `CssClass` 속성을 `Warning`에 추가한 CSS 클래스인는 `Styles.css` 이전 자습서에서 파일입니다. 이 CSS 클래스, 빨간색, 기울임꼴, 굵게, 초대형 글꼴로 표시할 레이블의 텍스트는 회수 합니다.


[![레이블 웹 컨트롤을 페이지에 추가](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image20.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image19.png)

**그림 7**: 페이지 레이블 웹 컨트롤을 추가 ([큰 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image21.png))


예외가 발생 한이 Label 웹 컨트롤이 표시 될 수만 즉시 후 것 이므로, 설정 해당 `Visible` 속성을 false는 `Page_Load` 이벤트 처리기:


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample3.vb)]

첫 번째 페이지 방문 및 후속 포스트백에서이 코드는 `ExceptionDetails` 컨트롤에 해당 `Visible` 속성이로 설정 `false`합니다. GridView의에를 감지할 수 DAL 또는 BLL 수준 예외를 발생 하는 경우 `RowUpdated` 이벤트 처리기를 설정 합니다 `ExceptionDetails` 컨트롤의 `Visible` 속성을 true로 합니다. 웹 컨트롤 이벤트 처리기 후 발생 하므로 `Page_Load` 페이지 수명 주기의 이벤트 처리기의 레이블이 표시 됩니다. 그러나 다음 포스트백에는 `Page_Load` 이벤트 처리기 되돌아갑니다 합니다 `Visible` 속성을 다시 `false`, 다시 뷰에서 숨기기.

> [!NOTE]
> 또는 설정에 대 한 필요성을 제거할 수는 것은 `ExceptionDetails` 컨트롤의 `Visible` 속성에서 `Page_Load` 할당 하 여 해당 `Visible` 속성 `false` 선언적 구문 및 ( 해당설정보기상태를사용하지않도록설정`EnableViewState` 속성을 `false`). 이후 자습서에서이 대체 방법을 사용 하겠습니다.


추가 레이블 컨트롤을 사용 하 여 다음 단계를 GridView에 대 한 이벤트 처리기를 만들 때 `RowUpdated` 이벤트입니다. 디자이너에서 GridView 선택한 속성 창으로 이동 GridView의 이벤트를 나열 하 고 번개 모양 아이콘을 클릭 합니다. GridView의에 대 한 항목이 있습니다 해야 이미 `RowUpdating` 이벤트 처럼이 자습서의 앞부분에서이 이벤트에 대 한 이벤트 처리기를 만들었습니다. 에 대 한 이벤트 처리기를 만들고는 `RowUpdated` 이벤트도 합니다.


![GridView의 RowUpdated 이벤트에 대 한 이벤트 처리기 만들기](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image22.png)

**그림 8**: GridView의에 대 한 이벤트 처리기를 만들고 `RowUpdated` 이벤트


> [!NOTE]
> 또한 코드 숨김 클래스 파일의 맨 위에 있는 드롭다운 목록을 통해 이벤트 처리기를 만들 수 있습니다. GridView의 왼쪽에 있는 드롭다운 목록에서 선택 및 `RowUpdated` 오른쪽에서 이벤트입니다.


이 이벤트 처리기를 만드는 ASP.NET 페이지의 코드 숨김 클래스에 다음 코드를 추가 합니다.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample4.vb)]

이 이벤트 처리기의 두 번째 입력된 매개 변수 형식의 개체인 [GridViewUpdatedEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdatedeventargs.aspx), 예외 처리에 대 한 관심의 세 가지 속성에는:

- `Exception` throw 된 예외;에 대 한 참조 이 속성의 값이 있는 예외가 throw 되는 경우 `null`
- `ExceptionHandled` 예외가 처리 되었는지 여부를 나타내는 부울 값을 `RowUpdated` 이벤트 처리기 같으면 `false` (기본값), 예외가 다시 throw ASP.NET 런타임에 percolating
- `KeepInEditMode` 경우로 `true` 경우에 편집된 된 GridView 행이 편집 모드에 유지 됩니다 `false` (기본값), GridView 행 돌아갑니다 해당 읽기 전용 모드

그런 다음 코드에 있는지 확인 해야 `Exception` 아닙니다 `null`, 즉 작업을 수행 하는 동안 예외가 발생 했습니다. 이 경우 해야 합니다.

- 에 친숙 한 메시지를 표시 합니다 `ExceptionDetails` 레이블
- 예외가 처리 되었는지 나타냅니다.
- 편집 모드에서 GridView 행 유지

다음이 코드는 이러한 목표를 수행합니다.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample5.vb)]

이 이벤트 처리기 하는지를 확인 하 여 시작 `e.Exception` 는 `null`합니다. 그렇지 않을 경우 합니다 `ExceptionDetails` 레이블의 `Visible` 속성이 `true` 고 `Text` 속성을 "제품을 업데이트 하는 데 문제가 있었습니다." 실제 throw 된 예외의 세부 정보에는 `e.Exception` 개체의 `InnerException` 속성입니다. 이 내부 예외를 검사 하 고, 추가, 유용한 메시지를에 추가 인 경우 특정 유형의 합니다 `ExceptionDetails` 레이블의 `Text` 속성입니다. 마지막으로, 합니다 `ExceptionHandled` 하 고 `KeepInEditMode` 속성이 둘 다로 설정 됩니다 `true`합니다.

그림 9 제품 이름을 생략 하는 경우이 페이지의 스크린 샷을 보여 줍니다. 그림 10 잘못 된 입력 하면 결과 보여 줍니다 `UnitPrice` 값 (-50).


[![ProductName BoundField 값이 있어야 합니다.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image24.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image23.png)

**그림 9**: 합니다 `ProductName` BoundField 값이 있어야 합니다. ([클릭 하 여 큰 이미지 보기](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image25.png))


[![UnitPrice 음수를 사용할 수 없습니다.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image27.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image26.png)

**그림 10**: 음수 `UnitPrice` 값은 허용 되지 않습니다 ([클릭 하 여 큰 이미지 보기](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image28.png))


설정 하 여 합니다 `e.ExceptionHandled` 속성을 `true`, `RowUpdated` 이벤트 처리기는 예외 처리 했음을 나타냅니다. 따라서 예외 ASP.NET 런타임에 전파 되지 않습니다.

> [!NOTE]
> 그림 9 및 10에는 잘못 된 사용자 입력으로 인해 발생 하는 예외를 처리 하는 적절 한 방법을 보여 줍니다. 이상적으로, 그러나 이러한 잘못 된 입력 두지 도달률 비즈니스 논리 계층 처음에 ASP.NET 페이지를 호출 하기 전에 사용자의 입력 유효한 지 확인 해야 합니다 `ProductsBLL` 클래스의 `UpdateProduct` 메서드. 비즈니스 논리 계층 전송 된 데이터가 되도록 편집 및 삽입 인터페이스에 유효성 검사 컨트롤을 추가 하는 방법을 살펴보겠습니다 다음 자습서에서 비즈니스 규칙을 따릅니다. 유효성 검사 컨트롤 뿐만 아니라 호출을 방지 합니다 `UpdateProduct` 사용자가 제공한 데이터 유효 하지만 데이터 입력 문제를 식별 하는 데는 많은 정보를 제공 하는 사용자 환경을 제공 될 때까지 메서드.


## <a name="step-3-gracefully-handling-bll-level-exceptions"></a>3 단계: BLL 수준의 예외를 정상적으로 처리

를 삽입할 때 업데이트 또는 삭제, 데이터 액세스 계층 예외가 throw 데이터 관련 오류를 발생 합니다. 데이터베이스를 오프 라인 상태가 될 수 있습니다, 필수 데이터베이스 테이블 열 수 있습니다 권한이 없는, 지정 된 값 또는 테이블 수준 제약 조건을 위반 했습니다. 데이터를 엄격 하 게 관련 예외 외에도 비즈니스 논리 계층 비즈니스 규칙 위반이 발생 했을 때를 나타내는 예외를 사용할 수 있습니다. 에 [비즈니스 논리 레이어 만들기](../introduction/creating-a-business-logic-layer-vb.md) 자습서에서는 예를 들어 원래 비즈니스 규칙 검사를 추가한 `UpdateProduct` 오버 로드 합니다. 특히 사용자가 제품을 중단으로 표시 하는 경우에서는 필요한 제품의 공급 업체에서 제공 되는 유일한 수 없습니다. 이 조건을 위반 된 경우는 `ApplicationException` throw 되었습니다.

에 대 한 합니다 `UpdateProduct` 오버 로드는이 자습서에서 만든, 금지 하는 비즈니스 규칙을 추가 해 보겠습니다 합니다 `UnitPrice` 원래 두 배 이상 많은 새 값으로 설정 된 필드 `UnitPrice` 값입니다. 이를 위해 조정 합니다 `UpdateProduct` 이 검사를 수행 하 고 throw 되도록 오버 로드는 `ApplicationException` 규칙을 위반 하는 경우. 업데이트 된 메서드는 다음과 같습니다.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample6.vb)]

기존 가격은 두 배 이상 많은 수 있는 모든 가격 업데이트 하면이 변경으로 `ApplicationException` throw 됩니다. 이 BLL 발생 DAL에서 발생 하는 예외와 마찬가지로 `ApplicationException` 탐지 및 GridView의 처리 `RowUpdated` 이벤트 처리기입니다. 실제로 `RowUpdated` 이벤트 처리기의 코드를 작성 하는 대로 올바르게 감지이 예외 하 고 표시 합니다 `ApplicationException`의 `Message` 속성 값입니다. 그림 11에서는 사용자는 현재 가격은 $19.95의 2 배 이상의 $50.00에 Chai의 가격을 업데이트 하려고 할 때를 지정 하 여 화면을 보여 줍니다.


[![비즈니스 규칙 두 개 제품의 가격을 두 번 가격 증가 허용 안 함](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image30.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image29.png)

**그림 11**: 비즈니스 규칙의 두 개 제품의 가격을 두 번 가격 증가 허용 안 함 ([큰 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image31.png))


> [!NOTE]
> 개는 비즈니스 논리 규칙은 리팩터링 하는 것이 가장 좋습니다를 `UpdateProduct` 메서드 오버 로드는 일반적인 방법으로 합니다. 이 판독기에 대 한 연습으로 남아 있습니다.


## <a name="summary"></a>요약

삽입, 업데이트 및 삭제 작업을 하는 동안 데이터 웹 컨트롤 및 ObjectDataSource와 관련 된 이벤트를 발생 시킬 전처리 및 후 수준 해당 북엔드 실제 작업 합니다. 우리가 본 것 처럼이 자습서에서 이전에는 편집 가능한 GridView를 사용 하 여 작업 하는 경우 GridView의 `RowUpdating` ObjectDataSource의 뒤에 이벤트가 실행 `Updating` 이때 업데이트 명령 하려고 ObjectDataSource의 이벤트 기본 개체입니다. 작업이 완료 된 ObjectDataSource의 후 `Updated` GridView의 뒤에 이벤트가 실행 `RowUpdated` 이벤트입니다.

검사 하 고 작업의 결과에 응답 하기 위해 사후 수준 이벤트 또는 입력된 매개 변수를 사용자 지정 하기 위해 미리 수준 이벤트에 대 한 이벤트 처리기를 만들 수 있습니다. 사후 수준 이벤트 처리기는 작업 중에 예외가 발생 했는지 여부를 검색할 가장 흔히 사용 됩니다. 예외가 발생 하는 경우 이러한 후 수준 이벤트 처리기 필요에 따라 자체적으로 예외를 처리할 수 있습니다. 이 자습서에서는 친숙 한 오류 메시지를 표시 하 여 이러한 예외를 처리 하는 방법에 살펴보았습니다.

다음 자습서에서 데이터 서식 지정 문제에서에서 발생 하는 예외 발생 가능성을 줄이기 위해 하는 방법을 알아봅니다 (음수를 입력 하는 등 `UnitPrice`). 특히, 편집 및 삽입 인터페이스에 유효성 검사 컨트롤을 추가 하는 방법을 살펴보겠습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Liz Shulok 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)
> [다음](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
