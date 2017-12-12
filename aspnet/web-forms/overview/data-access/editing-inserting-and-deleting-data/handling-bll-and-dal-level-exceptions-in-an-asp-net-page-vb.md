---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb
title: "ASP.NET 페이지 (VB)에서 BLL 및 DAL 수준 예외를 처리 | Microsoft Docs"
author: rick-anderson
description: "이 자습서는 삽입, 업데이트 또는 삭제 작업의 동안 예외가 발생 해야 친숙 하 고 자세한 오류 메시지를 표시 하는 방법을 살펴보겠습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/17/2006
ms.topic: article
ms.assetid: 129d4338-1315-4f40-89b5-2b84b807707d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb
msc.type: authoredcontent
ms.openlocfilehash: f5ebdf168610b715dc918ff6addf88d3c2a67097
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="handling-bll--and-dal-level-exceptions-in-an-aspnet-page-vb"></a>ASP.NET 페이지 (VB)에서 BLL 및 DAL 수준의 예외 처리
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_18_VB.exe) 또는 [PDF 다운로드](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/datatutorial18vb1.pdf)

> 이 자습서는 insert, update 또는 웹 컨트롤은 ASP.NET 데이터의 삭제 작업 동안 예외가 발생 해야 친숙 하 고 자세한 오류 메시지를 표시 하는 방법을 살펴봅니다.


## <a name="introduction"></a>소개

계층화 된 응용 프로그램 아키텍처를 사용 하 여 ASP.NET 웹 응용 프로그램에서 데이터 작업을에 다음 세 가지 일반적인 단계가 포함 됩니다.

1. 비즈니스 논리 계층의 어떤 메서드를 호출 해야 하 고 전달 하는 매개 변수 값을 확인 합니다. 사용자가 입력 한 입력 또는 하드 코드 된, 프로그래밍 방식으로-할당 된 매개 변수 값 수 있습니다.
2. 메서드를 호출합니다.
3. 결과 처리 합니다. 데이터를 반환 하는 BLL 메서드를 호출할 때 데이터 웹 컨트롤에 데이터 바인딩 눌러야 할 수 있습니다. 데이터를 수정 하는 BLL 메서드의 경우 반환 값에 따라 또는 2 단계에서에서 발생 하는 모든 예외를 처리 하는 정상적으로 동작을 수행 포함 됩니다.

설명한 것 처럼는 [이전 자습서](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)는 ObjectDataSource와 웹 컨트롤 데이터를 모두 1 단계 및 3에 대 한 확장 지점을 제공 합니다. GridView 예를 들어 발생 해당 `RowUpdating` 해당 ObjectDataSource을 필드 값을 할당 하기 전에 이벤트 `UpdateParameters` 컬렉션; 해당 `RowUpdated` 는 ObjectDataSource 작업 완료 이벤트가 발생 합니다.

1 단계 중에 발생 하 고 입력된 매개 변수를 사용자 지정 하거나 작업을 취소 하는 수 방법에 대해 알아보았습니다 하는 이벤트를 이미 검사 했습니다 했습니다. 이 자습서는 작업이 완료 된 후 실행 하는 이벤트에 설정 합니다. 무엇 보다도 원하므로 이러한 사후 수준의 이벤트 처리기와 작업 하는 동안 예외가 발생 하는 경우 확인 하 고 표준 ASP.NET로 기본 설정 하지 않고 화면에 정보를 제공 하 고 친숙 한 오류 메시지를 표시, 정상적으로 처리 예외 페이지입니다.

를 설명 하기 위해 이러한 사후 수준 이벤트 작업에는 편집 가능한 GridView의 제품을 나열 하는 페이지를 만들어 보겠습니다. 예외가 발생 하는 경우에 제품 업데이트는 ASP.NET을 발생 하는 경우 페이지에 문제가 발생 했음을 설명 하는 GridView 위에 간단한 메시지가 표시 됩니다. 이제 시작 하겠습니다.

## <a name="step-1-creating-an-editable-gridview-of-products"></a>1 단계: 제품의 편집 가능한는 GridView 만들기

이전 자습서에서는 두 개의 필드가 편집 가능한 GridView 만든 `ProductName` 및 `UnitPrice`합니다. 이 작업은 필요에 대 한 추가적인 오버 헤드가 만들기는 `ProductsBLL` 클래스의 `UpdateProduct` 메서드만 각 제품 필드에 대 한 달리 매개 변수 세 개의 입력된 매개 변수 (제품의 이름, 단가 및 ID)를 허용 하는 것입니다. 이 자습서에서는 재고 제품의 이름, 단위, unit price 및 단위 당 수량을 표시 하지만 편집할 수는 재고 이름, 단가 및 단위를 허용 하는 편집 가능한 GridView 만드는이 기법을 다시를 연습해 보겠습니다.

이 시나리오에 맞게 다른 오버 로드 해야는 `UpdateProduct` 메서드, 4 개의 매개 변수를 허용 하: 제품의 이름, 단가, 단위, 주식형 및 id입니다. 다음 메서드를 추가 `ProductsBLL` 클래스:


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample1.vb)]

이 방법을 완료 여러분 이러한 네 가지 특정 제품 필드를 편집할 수 있는 ASP.NET 페이지를 만들 수 있습니다. 열기는 `ErrorHandling.aspx` 페이지에 `EditInsertDelete` 폴더는 GridView 디자이너를 통해 페이지에 추가 합니다. 새 ObjectDataSource GridView 바인딩할 매핑은 `Select()` 메서드를는 `ProductsBLL` 클래스의 `GetProducts()` 메서드 및 `Update()` 메서드를는 `UpdateProduct` 방금 만든 오버 로드 합니다.


[![4 개의 입력된 매개 변수를 받는 UpdateProduct 메서드 오버 로드를 사용 하 여](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image2.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image1.png)

**그림 1**: 사용 된 `UpdateProduct` 메서드 오버 로드를 허용 4 개의 입력 매개 변수 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image3.png))


이렇게 하면와 ObjectDataSource 만들어집니다는 `UpdateParameters` 4 개의 매개 변수 및 필드와 GridView를 사용 하 여 각 제품 필드에 대 한 컬렉션입니다. ObjectDataSource의 선언적 태그 할당는 `OldValuesParameterFormatString` 속성 값 `original_{0}`, 라는 입력된 매개 변수는 예상 우리의 BLL 클래스의 이후 하면 예외가 발생 `original_productID` 에 전달 되도록 합니다. 이 설정을 완전히 선언적 구문에서 제거 하도록 설정 (기본 값으로 설정 하거나 `{0}`).

그런 다음만 포함 하도록 GridView 축소는 `ProductName`, `QuantityPerUnit`, `UnitPrice`, 및 `UnitsInStock` BoundFields 합니다. 또한 필요 하다 고 필드 수준 서식을 적용을 자유롭게 (예: 변경는 `HeaderText` 속성).

이전 자습서에서 보이는 것 처럼 서식을 지정 하는 방법의 `UnitPrice` 모두 읽기 전용 모드와 편집 모드에서 통화로 BoundField 합니다. 동일한 여기를 보겠습니다. 이 BoundField 설정 필수 회수 `DataFormatString` 속성을 `{0:c}`, 해당 `HtmlEncode` 속성을 `false`, 및 해당 `ApplyFormatInEditMode` 를 `true`그림 2에 표시 된 것 처럼 합니다.


[![통화로 표시할 UnitPrice BoundField 구성](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image5.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image4.png)

**그림 2**: 구성에서 `UnitPrice` 통화로 표시할 BoundField ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image6.png))


서식 지정은 `UnitPrice` 편집 인터페이스에는 통화의 GridView의에 대 한 이벤트 처리기를 만드는 필요에 따라 `RowUpdating` 에 통화 형식 문자열을 구문 분석 하는 이벤트는 `decimal` 값입니다. 이전에 설명한 대로 `RowUpdating` 지난 자습서에서 이벤트 처리기도 검사 하 여 확인 하는 사용자가 제공한는 `UnitPrice` 값입니다. 그러나이 자습서에 대 한 보겠습니다 수는 가격을 생략할 수 있습니다.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample2.vb)]

우리의 GridView에 포함 되어는 `QuantityPerUnit` BoundField 하지만이 BoundField 표시 용도로 이어야 하며 사용자가 편집 가능한 되지 않아야 합니다. 이 정렬 하려면 BoundFields'를 설정 하기만 `ReadOnly` 속성을 `true`합니다.


[![읽기 전용 QuantityPerUnit BoundField 만들기](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image8.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image7.png)

**그림 3**: 확인 된 `QuantityPerUnit` BoundField 읽기 전용 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image9.png))


마지막으로 확인 GridView의 스마트 태그에서 편집 사용 확인란을 선택 합니다. 다음이 단계를 완료 한 후의 `ErrorHandling.aspx` 그림 4 페이지의 디자이너 유사 합니다.


[![제외한 모든 필요한 BoundFields 및 확인 확인란 편집 사용](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image11.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image10.png)

**그림 4**: 제거 제외 하 고 모두 the 필요한 BoundFields 및 확인을 사용 하도록 설정 편집 확인란 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image12.png))


이 시점에서 모든 제품의 목록이 있는 `ProductName`, `QuantityPerUnit`, `UnitPrice`, 및 `UnitsInStock` 필드; 그러나만 `ProductName`, `UnitPrice`, 및 `UnitsInStock` 필드는 편집할 수 있습니다.


[![사용자가 이제 쉽게 편집할 수 제품의 이름과 가격, 재고 필드 단위](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image14.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image13.png)

**그림 5**: 사용자 수 이제 쉽게 편집 제품의 이름과 가격, 재고 필드에서 단위 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image15.png))


## <a name="step-2-gracefully-handling-dal-level-exceptions"></a>2 단계: DAL 수준 예외를 정상적으로 처리

작동 하는 동안 우리의 편집 가능한 GridView 아주 사용자가 편집 된 제품의 이름, 가격 및 재고에 대 한 올바른 값을 입력 하는 경우 잘못 된 값을 입력 하면 예외가 발생 합니다. 예를 들어 생략는 `ProductName` 원인을 값는 [NoNullAllowedException](https://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpref/html/frlrfsystemdatanonullallowedexceptionclasstopic.asp) 이후 throw 되는 `ProductName` 속성에는 `ProdcutsRow` 클래스에 해당 `AllowDBNull` 속성이로 설정 `false`경우는 다운 되는 데이터베이스는 `SqlException` 데이터베이스에 연결 하려고 할 때 TableAdapter에 의해 throw 됩니다. 작업을 수행 하지 않고 이러한 예외 버블 업 데이터 액세스 계층에서 ASP.NET 페이지에는 다음 비즈니스 논리 계층을 마지막으로 ASP.NET 런타임에 합니다.

웹 응용 프로그램 구성 하는 방법에서 응용 프로그램을 방문 중인 여부에 따라 `localhost`, 일반 서버 오류 페이지, 자세한 오류 보고서 또는 사용자에 게 친숙 웹 페이지 처리 되지 않은 예외가 발생할 수 있습니다. 참조 [웹 응용 프로그램 Error Handling in ASP.NET](http://www.15seconds.com/issue/030102.htm) 및 [customErrors 요소](https://msdn.microsoft.com/en-US/library/h0hfz6fc(VS.80).aspx) 확인할 수 없는 예외가에 ASP.NET 런타임이 응답 하는 방법에 대 한 자세한 내용은 합니다.

그림 6 지정 하지 않고 제품을 업데이트 하려고 할 때 발생 하는 화면 표시는 `ProductName` 값입니다. 이 자세한 오류 보고서를 통해 들어오는 경우에 표시 되는 기본 `localhost`합니다.


[![예외 세부 정보를 표시 합니다 제품의 이름을 생략합니다.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image17.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image16.png)

**그림 6**: 제품의 이름이 됩니다 예외 세부 정보를 표시를 생략 하는 것 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image18.png))


이러한 예외 세부 정보는 응용 프로그램을 테스트할 때 유용한, 예외가 발생할 때 이러한 화면을 가진 최종 사용자를 제시는 보다 작은 이상적입니다. 가능성이 최종 사용자가 무엇 인지 인식 하지는 `NoNullAllowedException` 은 한 이유 또는 합니다. 사용자 했음을 제품을 업데이트 하는 동안 문제를 설명 하는 보다 친숙 한 메시지를 표시 하는 것이 좋습니다.

작업을 수행할 때 예외가 발생 하는 경우는 ObjectDataSource와 데이터 웹 컨트롤 사후 수준 이벤트는 구성 요소를 검색 하 고 ASP.NET 런타임이까지 증가에서 예외를 취소 하는 수단을 제공 합니다. 이 예에서는 만들겠습니다 이벤트 처리기는 GridView에 대 한 `RowUpdated` 경우 예외가 발생 하며,이 경우 예외 정보를에서 표시 Label 웹 컨트롤을 결정 하는 이벤트입니다.

레이블을 설정 하는 ASP.NET 페이지에 추가 하 여 시작 해당 `ID` 속성을 `ExceptionDetails` 정리 하 고 해당 `Text` 속성입니다. 이 메시지에 사용자의 눈 그리려면 설정 해당 `CssClass` 속성을 `Warning`, CSS 클래스에 추가 되는 `Styles.css` 이전 자습서에서 파일입니다. 이 CSS 클래스 빨간색, 기울임꼴, 굵게, 특대 글꼴에 표시할 레이블 텍스트를 회수 합니다.


[![페이지에 레이블 웹 컨트롤 추가](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image20.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image19.png)

**그림 7**: 페이지에 레이블 웹 컨트롤을 추가 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image21.png))


예외가 발생 했음을이 Label 웹 컨트롤이 표시 될 수만 즉시 후 할 것 이므로, 설정 해당 `Visible` 속성을 false로에 `Page_Load` 이벤트 처리기.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample3.vb)]

첫 번째 페이지 방문 및 후속 포스트백에서이 코드는 `ExceptionDetails` 컨트롤을 갖게 됩니다 해당 `Visible` 속성이로 설정 `false`합니다. GridView의에서 검색 수 DAL 또는 BLL 수준 예외를 한 경우에도 `RowUpdated` 설정 해 드립니다 이벤트 처리기는 `ExceptionDetails` 컨트롤의 `Visible` 속성을 true로 합니다. 웹 컨트롤 이벤트 처리기 후 나타나므로 `Page_Load` 페이지 수명 주기의 이벤트 처리기는 레이블이 표시 됩니다. 그러나 다음 포스트백에는 `Page_Load` 이벤트 처리기는 전환는 `Visible` 속성을 다시 `false`, 다시 뷰에서 숨기기.

> [!NOTE]
> 설정에 대 한 필요성을 제거 수 또는 `ExceptionDetails` 컨트롤의 `Visible` 속성 `Page_Load` 할당 하 여 해당 `Visible` 속성 `false` 선언적 구문 및 해당 뷰 상태 (해당 설정사용안함`EnableViewState` 속성을 `false`). 이후 자습서에서이 대체 방법을 사용 합니다.


레이블 컨트롤을 추가, 다음 단계는 GridView에 대 한 이벤트 처리기를 만드는 것 `RowUpdated` 이벤트입니다. 디자이너에서 GridView 선택한 속성 창으로 이동 GridView의 이벤트를 나열 하 고 번개 모양 아이콘을 클릭 합니다. Gridview의 발생 한 항목이 있어야 이미 `RowUpdating` 이벤트,이 자습서의 앞부분에서이 이벤트에 대 한 이벤트 처리기를 생성 했습니다. 에 대 한 이벤트 처리기를 만들고는 `RowUpdated` 이벤트 뿐입니다.


![GridView의 RowUpdated 이벤트에 대 한 이벤트 처리기 만들기](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image22.png)

**그림 8**: GridView의에 대 한 이벤트 처리기를 만들고 `RowUpdated` 이벤트


> [!NOTE]
> 또한 코드 숨김 클래스 파일 맨 위에 있는 드롭다운 목록을 통해 이벤트 처리기를 만들 수 있습니다. GridView 왼쪽에 있는 드롭 다운 목록에서 선택 및 `RowUpdated` 오른쪽에 있는 것에서 이벤트 발생 합니다.


이 이벤트 처리기를 만드는 ASP.NET 페이지의 코드 숨김 클래스에 다음 코드를 추가 합니다.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample4.vb)]

이 이벤트 처리기의 두 번째 입력된 매개 변수 형식의 개체는 [GridViewUpdatedEventArgs](https://msdn.microsoft.com/en-US/library/system.web.ui.webcontrols.gridviewupdatedeventargs.aspx), 예외 처리에 대 한 관심 있는 세 속성이 있는:

- `Exception`throw 된 예외;에 대 한 참조 이 속성의 값을 갖습니다 예외가 throw 되는 경우`null`
- `ExceptionHandled`예외가 처리 되었는지 여부를 나타내는 부울 값은 `RowUpdated` 이벤트 처리기 경우 `false` (기본값) 이면 예외가 다시 throw ASP.NET 런타임에 percolating
- `KeepInEditMode`경우로 설정 `true` 있으면 편집된 GridView 행이 편집 모드에 유지 되므로 `false` (기본값) 이면 GridView 행 되돌아갑니다 해당 읽기 전용 모드

그런 다음 코드를 있는지 확인 해야 `Exception` 않습니다 `null`, 즉 작업을 수행 하는 동안 예외가 발생 했습니다. 이 경우 되기를 원하는 합니다.

- 에 친숙 한 메시지를 표시는 `ExceptionDetails` 레이블
- 예외가 처리 되었는지 나타냅니다.
- 편집 모드에 GridView 행을 유지 합니다.

다음 코드에서는 이러한 목표를 수행합니다.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample5.vb)]

이 이벤트 처리기 하는지를 확인 하 여 시작 `e.Exception` 은 `null`합니다. 그렇지 않을 경우는 `ExceptionDetails` 레이블의 `Visible` 속성이 `true` 및 해당 `Text` 속성을 "제품을 업데이트 하는 데 문제가 있었습니다." 에 상주 하는 실제 throw 된 예외에 대 한 세부 정보는 `e.Exception` 개체의 `InnerException` 속성입니다. 이 내부 예외를 검사 하 고 추가, 유용한 메시지에 추가 특정 유형의 경우는 `ExceptionDetails` 레이블의 `Text` 속성입니다. 마지막으로,는 `ExceptionHandled` 및 `KeepInEditMode` 속성 둘 다로 설정 `true`합니다.

그림 9; 제품의 이름을 생략 하는 경우이 페이지의 스크린 샷을 표시합니다 그림 10 잘못 된 입력할 때 결과 보여 줍니다 `UnitPrice` 값 (-50).


[![ProductName BoundField 값이 있어야 합니다.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image24.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image23.png)

**그림 9**:는 `ProductName` BoundField 값이 있어야 합니다. ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image25.png))


[![음수 UnitPrice 값이 허용 되지 않습니다.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image27.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image26.png)

**그림 10**: 음수 `UnitPrice` 값은 허용 되지 않습니다 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image28.png))


설정 하 여는 `e.ExceptionHandled` 속성을 `true`, `RowUpdated` 이벤트 처리기는 예외를 처리 했는지를 나타냅니다. 따라서 ASP.NET 런타임에 예외 전파 되지 않습니다.

> [!NOTE]
> 그림 9와 10 잘못 된 사용자 입력으로 인해 발생 한 예외를 처리 하는 적절 한 방법을 보여 줍니다. 이상적으로 하지만 이러한 잘못 된 입력 되지 것입니다 도달 범위는 비즈니스 논리 계층 처음에 ASP.NET 페이지를 호출 하기 전에 사용자의 입력이 유효한 지 확인 해야 하는 대로 `ProductsBLL` 클래스의 `UpdateProduct` 메서드. 비즈니스 논리 계층에 제출 된 데이터를 충족 되도록 편집 하 고 삽입 인터페이스에 유효성 검사 컨트롤을 추가 하는 방법을 살펴보려는 우리의 다음 자습서에서는 비즈니스 규칙을 따릅니다. 유효성 검사 컨트롤의 호출을 뿐만 아니라 방지는 `UpdateProduct` 메서드 때까지 사용자가 제공한 데이터 유효 하지만 또한 데이터 입력 문제를 식별 하는 데 보다 유용한 사용자 환경을 제공 합니다.


## <a name="step-3-gracefully-handling-bll-level-exceptions"></a>3 단계: BLL 수준 예외를 정상적으로 처리

를 삽입할 경우 업데이트 또는 삭제, 데이터 액세스 계층 예외가 throw 될 수는 데이터 관련 오류가 발생 한 경우에도 합니다. 데이터베이스가 오프 라인일 수 있습니다, 필수 데이터베이스 테이블 열을 하지 미쳤을 수를 지정 하는 값 또는 테이블 수준 제약 조건을 위반 했습니다. 데이터를 엄격 하 게 관련 예외 뿐 아니라 비즈니스 논리 계층 비즈니스 규칙 위반이 발생 했을 때를 나타내는 예외를 사용할 수 있습니다. 에 [는 비즈니스 논리 계층을 만드는](../introduction/creating-a-business-logic-layer-vb.md) 자습서, 예를 들어 비즈니스 규칙 확인을 원래에 추가한 `UpdateProduct` 오버 로드 합니다. 특히 사용자가 중단을으로 제품을 표시 하, म 경우 한 제품 되지 유일 하 게의 공급 업체에서 제공 합니다. 이 조건을 위반 된 경우는 `ApplicationException` throw 되었습니다.

에 대 한는 `UpdateProduct` 오버 로드는이 자습서에서 만든, 금지 하는 비즈니스 규칙을 추가 해 보겠습니다는 `UnitPrice` 필드를 두 배 이상 많은 원본 새 값으로 설정 되 고 `UnitPrice` 값입니다. 이를 위해 조정는 `UpdateProduct` 이 검사를 수행 하 고 throw 되도록 오버 로드는 `ApplicationException` 규칙을 위반 하는 경우. 업데이트 된 방법을 따릅니다.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample6.vb)]

이러한 변경으로 인해 기존 가격 두 배 이상 되는 가격 업데이트 하면는 `ApplicationException` throw 됩니다. 이 BLL 발생 DAL에서 발생 한 예외와 마찬가지로 `ApplicationException` 검색 하는 GridView에서 처리 `RowUpdated` 이벤트 처리기입니다. 실제로 `RowUpdated` 이벤트 처리기의 코드 작성 된 대로 올바르게이 예외를 검색 되며 표시는 `ApplicationException`의 `Message` 속성 값입니다. 그림 11 스크린 샷 사용자가 double 이상의 해당 현재 가격이 $19.95의 변수인 $50.00에 Chai의 가격을 업데이트 하는 경우를 보여 줍니다.


[![비즈니스 규칙 이상 제품의 가격을 두 번 가격 증가 허용 안 함](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image30.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image29.png)

**그림 11**: 비즈니스 규칙의 제품의 가격 두 번 이상 허용 안 함 가격이 상승 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image31.png))


> [!NOTE]
> 비즈니스 논리 규칙 우리의 리팩터링한 이상적으로 `UpdateProduct` 메서드 오버 로드는 일반적인 방법으로 합니다. 이 판독기에 대 한 연습으로 남아 있습니다.


## <a name="summary"></a>요약

삽입, 업데이트 및 삭제 작업을 하는 동안 데이터 웹 컨트롤과 관련 된 ObjectDataSource 모두 이벤트를 발생 시킬 전처리 및 후 수준 해당 북엔드 실제 작업 합니다. 설명한 것 처럼이 자습서와 이전 편집 가능한 GridView 작업할 때 GridView의 `RowUpdating` 이벤트 실행 되 면 뒤에 objectdatasource `Updating` 이 시점에서 업데이트 명령을 하려고 ObjectDataSource의 이벤트 기본 개체입니다. 작업이 완료 되 면 ObjectDataSource의 `Updated` 이벤트 실행 되 면 뒤에 GridView의 `RowUpdated` 이벤트입니다.

입력된 매개 변수를 사용자 지정 하기 위해 미리 수준 이벤트를 검사 하 고 작업의 결과에 응답 하기 위해 사후 수준 이벤트에 대 한 이벤트 처리기를 만들 수 있습니다. 사후 수준의 이벤트 처리기는 작업 중에 예외가 발생 했는지 여부를 검색 하는 주로 사용 됩니다. 예외가 발생 한 경우에도 이러한 사후 수준의 이벤트 처리기 필요에 따라 자체적으로 예외를 처리할 수 있습니다. 이 자습서에서는 친숙 한 오류 메시지를 표시 하 여 이러한 예외를 처리 하는 방법에 살펴보았습니다.

다음 자습서에서는 데이터 형식 문제에서에서 발생 하는 예외가 발생할 가능성을 줄일 수 하는 방법을 보겠습니다 (음수를 입력 하는 등 `UnitPrice`). 특히, 편집 및 삽입 인터페이스에 유효성 검사 컨트롤을 추가 하는 방법을 살펴보겠습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Liz Shulok 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)
[다음](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
