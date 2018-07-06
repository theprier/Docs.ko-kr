---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb
title: 데이터 (VB)를 기반으로 DataList 및 반복기 서식 지정 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 서식을에서는 서식 지정 함수를 사용 하 여 DataList 및 반복기 컨트롤의 모양을 지정 방법의 예제를 통해 단계별로...
ms.author: aspnetcontent
ms.date: 09/13/2006
ms.assetid: e2f401ae-37bb-4b19-aa97-d6b385d40f88
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 428438b2bae062c09d13c002f4729c3c394975a1
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37807712"
---
<a name="formatting-the-datalist-and-repeater-based-upon-data-vb"></a>DataList 및 반복기 (VB) 데이터를 기반으로 서식 지정
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_30_VB.exe) 또는 [PDF 다운로드](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/datatutorial30vb1.pdf)

> 이 자습서에서는 서식을에서는 템플릿 내에서 서식 지정 함수를 사용 하 여 또는 데이터 바인딩된 이벤트를 처리 하면 DataList 및 반복기 컨트롤의 모양을 지정 방법의 예제를 단계별로 실행 했습니다.


## <a name="introduction"></a>소개

이전 자습서에서 보았듯이 DataList는 다양 한 해당 모양에 영향을 주는 스타일 관련 속성을 제공 합니다. DataList s에 기본 CSS 클래스를 할당 하는 방법을 살펴보았습니다 특히 `HeaderStyle`, `ItemStyle`를 `AlternatingItemStyle`, 및 `SelectedItemStyle` 속성입니다. DataList 이러한 네 가지 속성 외에 다른 스타일 관련 속성의 숫자와 같은 포함 `Font`, `ForeColor`를 `BackColor`, 및 `BorderWidth`, 등입니다. Repeater 컨트롤에는 모든 스타일 관련 속성이 없습니다. 이러한 스타일 설정은 Repeater가 템플릿에 태그 내에서 직접 수행 되어야 합니다.

종종 하지만 데이터를 포맷 해야 하는 방법에 따라 달라 집니다 데이터 자체입니다. 예를 들어, 제품을 나열할 때 수 하고자 단종 된 경우 강조 표시 해야 할 수도 있으므로 밝은 회색 글꼴 색으로 제품 정보를 표시 합니다 `UnitsInStock` 값 이면 0입니다. 이전 자습서에서 보았듯이 GridView, DetailsView 및 FormView 해당 서식을 지정 해당 데이터를 기반으로 하는 두 가지 방법으로 제공 합니다.

- **`DataBound` 이벤트** 적절 한에 대 한 이벤트 처리기를 만듭니다 `DataBound` 데이터를 각 항목에 바인딩된 후 발생 하는 경우 (된 gridview는 `RowDataBound` 이벤트 DataList 및 반복기는 것은 `ItemDataBound`이벤트). 이벤트의 처리기를 바인딩된만 데이터를 검사할 수 있습니다 하 고 의사 결정을 서식 지정. 이 기법을 살펴보았습니다 합니다 [데이터를 기반으로 사용자 지정 서식 지정](../custom-formatting/custom-formatting-based-upon-data-vb.md) 자습서입니다.
- **템플릿 함수를 서식 지정** FormView 컨트롤에서 템플릿이나 DetailsView 또는 GridView 컨트롤에서 TemplateFields 사용 하는 경우 ASP.NET 페이지가 코드 숨김 클래스, 비즈니스 논리 레이어 또는에 서식 지정 함수를 추가할 수 있습니다 웹 응용 프로그램에서 액세스할 수 있는 다른 클래스 라이브러리입니다. 이 서식 지정 함수는 임의 개수의 입력된 매개 변수를 수락할 수 있지만 템플릿에서 렌더링 하는 HTML을 반환 해야 합니다. 서식 지정 함수에서 먼저 검사 된 합니다 [GridView 컨트롤에서 TemplateFields 사용 하 여](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) 자습서입니다.

이러한 기술을 서식 모두 DataList 및 반복기 컨트롤을 사용 하 여 사용할 수 있습니다. 이 자습서에서는 두 컨트롤에 대 한 두 가지 방법을 모두 사용 하는 예제를 단계별로 실행 했습니다.

## <a name="using-theitemdataboundevent-handler"></a>사용 하 여`ItemDataBound`이벤트 처리기

경우에 바인딩된 데이터가 DataList, 데이터 소스 컨트롤에서 또는 프로그래밍 방식으로 s 컨트롤에 데이터를 할당 하 여 `DataSource` 속성과 호출 해당 `DataBind()` 메서드, DataList의 `DataBinding` 이벤트가 발생 하면 데이터 원본 열거 및 각 데이터 레코드 DataList에 바인딩됩니다. 데이터 소스의 각 레코드에 대해 DataList 만듭니다는 [ `DataListItem` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.aspx) 되는 개체를 현재 레코드에 바인딩됩니다. 이 과정에서 DataList 두 이벤트를 발생 시킵니다.

- **`ItemCreated`** 후 발생 합니다 `DataListItem` 만들었습니다
- **`ItemDataBound`** 현재 레코드에 바인딩된 후에 발생 합니다 `DataListItem`

다음 단계에는 DataList 컨트롤에 대 한 데이터 바인딩 프로세스를 간략하게 설명합니다.

1. S DataList [ `DataBinding` 이벤트](https://msdn.microsoft.com/library/system.web.ui.control.databinding.aspx) 발생 합니다.
2. DataList에 바인딩된 데이터  
  
   데이터 소스의 각 레코드에 대 한 

    1. 만들기는 `DataListItem` 개체
    2. 실행 된 [ `ItemCreated` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemcreated.aspx)
    3. 레코드를 바인딩하는 `DataListItem`
    4. 실행 된 [ `ItemDataBound` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemdatabound.aspx)
    5. 추가 된 `DataListItem` 에 `Items` 컬렉션

Repeater 컨트롤 데이터 바인딩, 동일한 일련의 단계를 진행 합니다. 유일한 차이점은 대신 `DataListItem` 사용 하 여 만들어지는 경우 반복기 [ `RepeaterItem` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem(VS.80).aspx)s입니다.

> [!NOTE]
> 예리한 독자 GridView 데이터에 바인딩될 때 DataList 및 반복기와 데이터에 바인딩되는 경우 지정 전까지 대기 하는 단계의 순서 간에 약간의 변칙을 알 수 있습니다. GridView 데이터 바인딩 프로세스 비상 끝날 때 발생 합니다 `DataBound` 이벤트 DataList 아니고 반복기 컨트롤에서 이러한 이벤트를 포함 하는 단, 합니다. DataList 및 반복기 컨트롤을 전처리 및 후 수준 이벤트 처리기 패턴 했습니다 보편화 전에 ASP.NET 1.x 기간에서 다시 만든 때문입니다.


GridView를 사용 하 여 데이터를 기반으로 하는 서식 지정 하는 한 가지 옵션에 대 한 이벤트 처리기를 만들 때 처럼는 `ItemDataBound` 이벤트입니다. 이 이벤트 처리기는 바인딩할 바로 있었습니다 하는 데이터를 검사 합니다 `DataListItem` 또는 `RepeaterItem` 필요에 따라 컨트롤의 서식에 영향을 줍니다.

DataList 컨트롤에 대 한 변경 내용 서식 지정에 사용 하 여 전체 항목을 구현할 수 있습니다 합니다 `DataListItem` 스타일 관련 속성을 표준을 포함 하는 `Font`를 `ForeColor`, `BackColor`, `CssClass`등입니다. DataList의 템플릿 내에서 특정 웹 컨트롤의 서식에 영향을 주는를 프로그래밍 방식으로 액세스 하 고 해당 웹 컨트롤의 스타일을 수정 해야 합니다. 이 다시 수행 하는 방법에 살펴보았습니다 합니다 *데이터를 기반으로 사용자 지정 서식 지정* 자습서입니다. Repeater 컨트롤을 같은 합니다 `RepeaterItem` 클래스 없는 스타일 관련 속성에는 모든 스타일 관련 변경 내용이 있으므로 `RepeaterItem` 에 `ItemDataBound` 이벤트 처리기를 프로그래밍 방식으로 액세스 하 고 내에서 웹 컨트롤을 업데이트 하 여 수행 해야 합니다 템플릿입니다.

이후는 `ItemDataBound` DataList 및 반복기는 거의 동일한 예에서 DataList를 사용 하 여 중점적 기술 형식입니다.

## <a name="step-1-displaying-product-information-in-the-datalist"></a>DataList에서 제품 정보를 표시 하는 1 단계:

서식 지정 걱정을 먼저 let s DataList를 사용 하 여 제품 정보를 표시 하는 페이지를 만듭니다. 에 [이전 자습서](displaying-data-with-the-datalist-and-repeater-controls-vb.md) DataList를 만들었습니다 인 `ItemTemplate` 각 s 제품 이름, 범주, 공급자, 단위 및 가격 당 수량을 표시 합니다. 이 자습서에서는이 기능을 여기서 반복 s 수 있습니다. 이렇게 하려면 DataList 및부터 해당 ObjectDataSource 하거나 다시 만들 수 있습니다 또는 이전 자습서에서 만든 페이지에서 이러한 컨트롤을 복사할 수 있습니다 (`Basics.aspx`)이이 자습서에 대 한 페이지에 붙여 넣을 (`Formatting.aspx`).

DataList 및 ObjectDataSource 기능을 복제 한 후 `Basics.aspx` 에 `Formatting.aspx`, s DataList를 변경 하려면 잠시 `ID` 속성을 `DataList1` 하는 보다 자세한 `ItemDataBoundFormattingExample`합니다. 다음으로, 브라우저에서 DataList를 봅니다. 그림 1에서 알 수 있듯이, 서식 지정 각 제품 간의 점만 배경색 교대로 나타납니다.


[![제품은 DataList 컨트롤에 나열 됩니다.](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image2.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image1.png)

**그림 1**: DataList 컨트롤에 있는 제품 나열 됩니다 ([큰 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image3.png))


이 자습서에서는 s $20.00 보다 낮은 가격으로 모든 제품에는 해당 이름을 모두 있고 단위 가격 노란색으로 강조 표시 되도록 DataList 서식을 지정 하도록 합니다.

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-itemdatabound-event-handler"></a>2 단계: ItemDataBound 이벤트 처리기에서 데이터의 값을 프로그래밍 방식으로 결정

$20.00는 아래 가격을 사용 하 여 해당 제품에만 적용 되는 사용자 지정 서식이에서는 각 제품의 가격을 결정할 수 있어야 합니다. DataList에 데이터 바인딩할 경우 DataList 열거 데이터 원본에서 레코드를 만들고, 각 레코드에 대 한는 `DataListItem` 인스턴스를 바인딩 데이터 소스 레코드는 `DataListItem`합니다. 특정 레코드 s 후 데이터에 바인딩된 현재 `DataListItem` DataList의 개체 `ItemDataBound` 이벤트가 발생 합니다. 현재 데이터 값을 검사 하려면이 이벤트에 대 한 이벤트 처리기를 만들 수 있습니다 `DataListItem` 및 해당 값을 기준으로 서식 지정 필요한 경우 변경 합니다.

만들기는 `ItemDataBound` DataList에 대 한 이벤트 다음 코드를 추가 합니다.


[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample1.vb)]

개념 및 DataList s 뒤 의미 체계를 while `ItemDataBound` 이벤트 처리기는 GridView s에서 사용 하는 것과 동일 `RowDataBound` 이벤트 처리기는 *데이터를 기반으로 사용자 지정 서식 지정* 자습서에서는 구문을 다릅니다 약간 있습니다. 경우는 `ItemDataBound` 이벤트가 발생 합니다 `DataListItem` 만 데이터에 바인딩된을 통해 해당 이벤트 처리기에 전달 됩니다 `e.Item` (대신 `e.Row`GridView s와 마찬가지로, `RowDataBound` 이벤트 처리기). S DataList `ItemDataBound` 이벤트 처리기에 대 한 발생 *각* 행이 머리글 행을 바닥글 행 및 행 구분 기호를 포함 하 여 DataList를 추가 합니다. 그러나 제품 정보를만 데이터 행에 바인딩되어 있습니다. 따라서 사용 하는 경우는 `ItemDataBound` DataList에 바인딩된 이벤트 데이터 검사를 먼저 확인 해야 하는 데이터 항목을 사용 하는 다시 했습니다. 이 확인 하 여 수행할 수 있습니다 합니다 `DataListItem` s [ `ItemType` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.itemtype.aspx), 중 하나일 수 있습니다 하는 [다음 8 개 값](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listitemtype.aspx):

- `AlternatingItem`
- `EditItem`
- `Footer`
- `Header`
- `Item`
- `Pager`
- `SelectedItem`
- `Separator`

둘 다 `Item` 고 `AlternatingItem``DataListItem`의 구성 DataList의 데이터 항목입니다. 작업 다시 가정 하는 것을 `Item` 또는 `AlternatingItem`, 실제 액세스 `ProductsRow` 현재 바인딩된 인스턴스 `DataListItem`합니다. 합니다 `DataListItem` s [ `DataItem` 속성](https://msdn.microsoft.com/system.web.ui.webcontrols.datalistitem.dataitem.aspx) 에 대 한 참조를 포함 합니다 `DataRowView` 개체입니다 `Row` 속성은 실제에 대 한 참조를 제공 `ProductsRow` 개체입니다.

다음으로 확인 합니다 `ProductsRow` 인스턴스의 `UnitPrice` 속성입니다. S 제품 이므로 `UnitPrice` 필드를 사용 하면 `NULL` 값에 액세스 하기 전에 `UnitPrice` 속성에서는 먼저 확인 해야 있는지를 `NULL` 를 사용 하 여 값를 `IsUnitPriceNull()` 메서드. 경우는 `UnitPrice` 값이 아닙니다 `NULL`, 하 고 확인 하 고 $20.00 보다 작거나. $20.00 실제로 아래에 있는 경우 다음 사용자 지정 서식을 적용 해야 합니다.

## <a name="step-3-highlighting-the-product-s-name-and-price"></a>3 단계: 제품 s 이름과 가격을 강조 표시

S 제품 가격 20.00 달러 임을 알고 있으므로에 이름과 가격을 강조 표시 합니다. 이렇게 하려면 해야 먼저 프로그래밍 방식으로 참조에서 Label 컨트롤은 `ItemTemplate`의 제품 이름 및 가격을 표시 하는 합니다. 다음으로, 노란색 배경이 표시 하도록 해야 합니다. 이 서식 지정 정보를 직접 레이블을 수정 하 여 적용할 수 있습니다 `BackColor` 속성 (`LabelID.BackColor = Color.Yellow`); 이상적으로 그러나 연계 스타일 시트를 통해 모든 표시와 관련 된 문제를 표현 되어야 합니다. 사실, 스타일 시트에 정의 된 원하는 형식 지정을 제공 하는 이미 보유 `Styles.css`  -  `AffordablePriceEmphasis`, 생성 되어에서 설명 하는 합니다 *데이터를 기반으로 사용자 지정 서식 지정* 자습서.

서식 지정을 적용 하려면 두 Label 웹 컨트롤을 설정 하기만 `CssClass` 속성을 `AffordablePriceEmphasis`다음 코드 에서처럼:


[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample2.vb)]

사용 하 여 합니다 `ItemDataBound` 다시 확인을 완료 하는 이벤트 처리기는 `Formatting.aspx` 브라우저에서 페이지입니다. 그림 2에서 알 수 있듯이, 해당 이름 및 강조 표시 된 가격은 $20.00 아래 가격을 사용 하 여 해당 제품에 있습니다.


[![이러한 제품 보다 $20.00 강조 표시 됩니다.](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image5.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image4.png)

**그림 2**: 이러한 제품 보다 $20.00 강조 표시 됩니다 ([큰 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image6.png))


> [!NOTE]
> DataList를 HTML로 렌더링 됩니다 때문 `<table>`, 해당 `DataListItem` 인스턴스 전체 항목을 특정 스타일을 적용 하려면 설정할 수 있는 스타일 관련 속성을 가집니다. 예를 들어 드리고자 합니다 *전체* 가격은 20.00 달러를 때 노란색 항목, 수로 교체 했습니다 레이블을 참조 하는 코드를 설정 및 해당 `CssClass` 코드의 다음 줄을 사용 하 여 속성: `e.Item.CssClass = "AffordablePriceEmphasis"` (그림 3 참조).


그러나 `RepeaterItem` don t Repeater 컨트롤을 구성 하는 이러한 수준의 스타일 속성을 제공 합니다. 따라서 반복기에는 사용자 지정 서식을 적용 그림 2에서 수행한 것 처럼 반복기의 템플릿 내에서 웹 컨트롤에 스타일 속성의 응용 프로그램이 필요 합니다.


[![전체 제품 항목이 $20.00 아래에서 제품에 대 한 강조 표시](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image8.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image7.png)

**그림 3**: $20.00 아래에서 제품에는 전체 제품 항목 강조 표시 됩니다 ([큰 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image9.png))


## <a name="using-formatting-functions-from-within-the-template"></a>템플릿 내에서 서식 지정 함수를 사용 하 여

에 *GridView 컨트롤에서 TemplateFields 사용 하 여* GridView s 개의 행에 바인딩된 자습서에서 데이터에 기반한 사용자 지정 서식을 적용 하려면 GridView templatefield로 내에서 서식 지정 함수를 사용 하는 방법에 살펴보았습니다. 서식 지정 함수는 서식 파일에서 호출할 수 있으며 해당 위치에 내보낼 HTML을 반환 하는 메서드. 서식 지정 함수는 ASP.NET 페이지의 코드 숨김 클래스에 있을 수 있습니다 또는 있는 클래스 파일을 중앙 집중화할 수 있습니다는 `App_Code` 폴더 또는 별도 클래스 라이브러리 프로젝트. ASP.NET 페이지의 코드 숨김 클래스 외부에서 서식 지정 함수를 이동 하는 것은 여러 ASP.NET 페이지 또는 다른 ASP.NET 웹 응용 프로그램에서 동일한 서식 지정 기능을 사용 하려는 경우에 적합 합니다.

서식 지정 함수를 보여 주기 위해 s 수 있는 경우 제품의 이름 옆에 있는 [지원 되지 않는] 텍스트를 포함 하는 제품 정보를 해당 s 중단 합니다. 또한 let s가 가격 강조 표시 된 노란색 경우 해당 $20.00 보다 작거나 (에서 수행한 것 처럼는 `ItemDataBound` 이벤트 처리기 예제) 가격은 $20.00 또는 더 높은, s에 실제 가격을 표시 하지 이지만 가격 견적에 대 한 텍스트 하세요를 호출 하는 대신 하는 경우. 그림 4에 적용 되는 이러한 서식 지정 규칙을 사용 하 여 나열 하는 제품의 스크린 샷을 보여 줍니다.


[![비용이 많이 드는 제품에 대 한 가격을 가격 견적에 대 한 호출 하십시오 텍스트로 바뀝니다.](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image11.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image10.png)

**그림 4**: 비용이 많이 드는 제품에 대 한 가격을 가격 견적에 대 한 호출 하십시오 텍스트로 바뀝니다 ([큰 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image12.png))


## <a name="step-1-create-the-formatting-functions"></a>1 단계: 서식 지정 함수 만들기

이 예제에서는 두 가지 서식 지정, 필요한 경우 [DISCONTINUED], 텍스트와 함께 제품 이름을 표시 하는 함수와 다른 해야 하는 경우 강조 표시 된 가격을 표시 하는 대 한이 s 보다 작은지 $20.00, 또는 텍스트가 고 그렇지 가격 견적에 대 한 호출 하세요. ASP.NET 페이지가 코드 숨김 클래스에서 이러한 함수를 만들고 이름을 s `DisplayProductNameAndDiscontinuedStatus` 고 `DisplayPrice`입니다. 두 메서드를 문자열로 렌더링 하는 HTML을 반환 해야 하며 둘 다 표시 해야 `Protected` (또는 `Public`) 하려면 ASP.NET 페이지 s 선언적 구문 부분에서 호출할 수 있습니다. 이러한 두 가지 방법에 대 한 코드는 다음과 같습니다.


[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample3.vb)]

`DisplayProductNameAndDiscontinuedStatus` 의 값을 허용 하는 메서드를 `productName` 및 `discontinued` 반면 스칼라 값으로 데이터 필드를 `DisplayPrice` 메서드에서 `ProductsRow` 인스턴스 (아닌 `unitPrice` 스칼라 값). 어느 방법이 든 작동 합니다. 그러나 데이터베이스를 포함할 수 있는 스칼라 값을 사용 하 여 서식 지정 함수가 작동 하는지 `NULL` 값 (같은 `UnitPrice`; 모두 `ProductName` 나 `Discontinued` 허용 `NULL` 값), 특별 한 주의 해야 이러한 처리 스칼라 입력 합니다.

특히 입력된 매개 변수 형식 이어야 합니다 `Object` 들어오는 값이 될 수는 `DBNull` 예상된 데이터 형식 대신 인스턴스. 들어오는 값 데이터베이스 인지 여부를 결정 하는 검사가 해야 수행 하는 또한 `NULL` 값입니다. 즉, 원하는 경우는 `DisplayPrice` d에서는 스칼라 값으로 가격을 적용할 메서드를 다음 코드를 사용 해야 합니다.:


[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample4.vb)]

합니다 `unitPrice` 입력된 매개 변수는 형식 `Object` 및 경우를 정확 하 게 수정 된 조건문 `unitPrice` 는 `DBNull` 여부입니다. 또한 이후 합니다 `unitPrice` 입력된 매개 변수로 전달 됩니다는 `Object`, 10 진수 값으로 캐스팅 되어야 합니다.

## <a name="step-2-calling-the-formatting-function-from-the-datalist-s-itemtemplate"></a>DataList의 ItemTemplate에서 서식 지정 함수를 호출 하는 2 단계:

ASP.NET 페이지가 코드 숨김 클래스에 추가 하는 서식 지정 함수를 사용 하 여에 이러한 서식 s DataList에서 함수를 호출 하 `ItemTemplate`합니다. 템플릿에서 서식 지정 함수를 호출 하려면 데이터 바인딩 구문 내에서 함수 호출을 배치:


[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample5.aspx)]

DataList s에서에서 `ItemTemplate` 는 `ProductNameLabel` Label 웹 컨트롤 현재 이름을 표시 하는 제품 s 할당 하 여 해당 `Text` 결과 속성의 `<%# Eval("ProductName") %>`합니다. 가 필요한 경우 이름과 [DISCONTINUED], 텍스트를 표시 하기 위해 선언적 구문 대신 할당 되도록 업데이트 합니다 `Text` 속성 값의는 `DisplayProductNameAndDiscontinuedStatus` 메서드. S 제품 이름 및 사용 하 여 지원 되지 않는 값의 전달 해야이 작업을 수행 하는 경우는 `Eval("columnName")` 구문입니다. `Eval` 형식의 값을 반환 `Object`, 하지만 `DisplayProductNameAndDiscontinuedStatus` 메서드에서 입력된 매개 변수 형식의 예상 `String` 및 `Boolean`이므로 반환 하는 값을 캐스팅 해야 했습니다는 `Eval` 같이 필요한 입력된 매개 변수 형식에 메서드:


[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample6.aspx)]

가격을 표시 하려면 설정 하기만 했습니다 합니다 `UnitPriceLabel` 레이블 s `Text` 속성에서 반환 된 값을는 `DisplayPrice` 메서드를 수행한 s 제품 이름을 표시 하 고 [중단] 텍스트 처럼 합니다. 그러나에 전달 하는 대신에 합니다 `UnitPrice` 스칼라 입력된 매개 변수로 대신 전달 된 전체 `ProductsRow` 인스턴스:


[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample7.aspx)]

곳의 서식 지정 함수에 대 한 호출을 사용 하 여 시간을 내어 브라우저에서 진행 상황을 보고 합니다. [지원 되지 않는] 텍스트를 포함 하 여 지원 되지 않는 제품을 사용 하 여 그림 5와 유사한 화면이 표시 됩니다 및 해당 제품 가격을 가진 $20.00 개 비용으로 대체 텍스트 하세요 가격 견적에 대 한 호출 합니다.


[![비용이 많이 드는 제품에 대 한 가격을 가격 견적에 대 한 호출 하십시오 텍스트로 바뀝니다.](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image14.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image13.png)

**그림 5**: 비용이 많이 드는 제품에 대 한 가격을 가격 견적에 대 한 호출 하십시오 텍스트로 바뀝니다 ([큰 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image15.png))


## <a name="summary"></a>요약

데이터를 기반으로 DataList 또는 Repeater 컨트롤 내용의 서식을 두 기술을 사용 하 여 수행할 수 있습니다. 첫 번째 방법은 대 한 이벤트 처리기를 만들려면 합니다 `ItemDataBound` 새에 바인딩된 데이터 소스의 각 레코드가 발생 하는 이벤트 `DataListItem` 또는 `RepeaterItem`합니다. 에 `ItemDataBound` 이벤트 처리기의 현재 항목의 데이터를 검사할 수 있습니다 및 서식을 지정 하는 템플릿 또는 내용에 적용할 수 있습니다 `DataListItem` 전체 항목 자체가 s입니다.

또는 사용자 지정 서식 지정 함수를 서식 지정을 통해 실현할 수 있습니다. 서식 지정 기능은 DataList에서 호출할 수 있는 메서드 또는 해당 위치에 내보낼 HTML을 반환 하는 반복기가의 템플릿. 종종 HTML 서식 지정 함수에서 반환 된 현재 항목에 바인딩되는 값을 기준으로 결정 됩니다. 스칼라 값 또는 항목에 바인딩되는 전체 개체에 전달 하 여 서식 지정 함수에 이러한 값을 전달할 수 있습니다 (예는 `ProductsRow` 인스턴스).

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Yaakov Ellis, Randy Schmidt 및 Liz Shulok 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](displaying-data-with-the-datalist-and-repeater-controls-vb.md)
> [다음](showing-multiple-records-per-row-with-the-datalist-control-vb.md)
