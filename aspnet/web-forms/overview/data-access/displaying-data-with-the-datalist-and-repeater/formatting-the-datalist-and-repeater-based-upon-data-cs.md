---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs
title: "데이터 (C#)에 따라 서식 DataList 및 반복기 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 서식을 म 있는 서식 지정 함수를 사용 하 여 DataList 및 반복기 컨트롤의 모양을 지정 방법의 예제를 단계별로 합니다 म 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/13/2006
ms.topic: article
ms.assetid: 83e3d759-82b8-41e6-8d62-f0f4b3edec41
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 6e5bc0d9ac26801f48560cf07d4a0ab3854d5f74
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="formatting-the-datalist-and-repeater-based-upon-data-c"></a>DataList 및 데이터 (C#)를 기반으로 반복기 서식 지정
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_30_CS.exe) 또는 [PDF 다운로드](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/datatutorial30cs1.pdf)

> 이 자습서에서는 서식을 म 템플릿 내에서 서식 지정 기능을 사용 하 여 또는 데이터 바인딩된 이벤트를 처리 하 여 DataList 및 반복기 컨트롤의 모양을 지정 방법의 예를 단계별로 합니다 했습니다.


## <a name="introduction"></a>소개

이전 자습서에서 살펴본 것 처럼 DataList는 다양 한 모양에 영향을 주는 스타일 관련 속성을 제공 합니다. DataList s에 기본 CSS 클래스를 지정 하는 방법을 살펴보았습니다 특히 `HeaderStyle`, `ItemStyle`, `AlternatingItemStyle`, 및 `SelectedItemStyle` 속성입니다. DataList 이러한 네 가지 속성 외에 다른 스타일 관련 속성의 숫자와 같은 포함 `Font`, `ForeColor`, `BackColor`, 및 `BorderWidth`, 등입니다. 반복기 컨트롤에 모든 스타일 관련 속성이 없습니다. 이러한 스타일 설정의 템플릿에의 태그 내에서 직접 수행 되어야 합니다.

종종 하지만 데이터 서식을 방식에 따라 달라 집니다 데이터 자체입니다. 예를 들어 제품을 나열 하는 경우 수 원하는 중단 또는 강조 표시 하려는 경우 밝은 회색 글꼴 색으로 제품 정보를 표시 하는 `UnitsInStock` 값이 기본값은 0입니다. 이전 자습서에서 살펴본 것 처럼 GridView, DetailsView, 및 FormView 두 가지 방법에 해당 데이터에 따라 모양의 서식을 제공 합니다.

- **`DataBound` 이벤트** 적절 한 작업에 대 한 이벤트 처리기를 만들고 `DataBound` 각 항목에는 데이터 바인딩된 후 발생 하는 이벤트 (된 GridView에 대 한는 `RowDataBound` 이벤트; 한 DataList 및 반복기는 는`ItemDataBound`이벤트). 해당 이벤트에 처리기를 정당한 바인딩된 데이터를 검사할 수 있습니다 하 고 의사 결정을 서식 지정. 이 기술을 검사 했습니다는 [데이터 기반 시 사용자 지정 서식](../custom-formatting/custom-formatting-based-upon-data-cs.md) 자습서입니다.
- **서식 파일의 함수를 서식 지정** TemplateFields DetailsView 또는 GridView 컨트롤 또는 FormView 컨트롤에서 서식 파일을 사용할 경우 ASP.NET 페이지의 코드 숨김 클래스, 비즈니스 논리 계층 또는을 형식 지정 함수를 추가할 수 있습니다 웹 응용 프로그램에서 액세스할 수 있는 다른 클래스 라이브러리입니다. 서식 지정이 함수는 임의 개수의 입력된 매개 변수를 사용할 수 있습니다 하는 서식 파일에서 렌더링할 HTML을 반환 해야 합니다. 서식 지정 함수에 처음 검사 된는 [GridView 컨트롤에 사용 하 여 TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) 자습서입니다.

이러한 기술을 서식 모두 DataList 및 반복기 컨트롤과 함께 사용할 수 있습니다. 이 자습서에서는 두 컨트롤에 대 한 두 가지 방법을 모두 사용 하는 예제를 단계별로 합니다 했습니다.

## <a name="using-theitemdataboundevent-handler"></a>사용 하 여`ItemDataBound`이벤트 처리기

경우에 바인딩된 데이터가 데이터 소스 제어에서 또는 프로그래밍 방식으로 s 컨트롤에 데이터 할당을 통해 `DataSource` 속성과 호출 해당 `DataBind()` 메서드, s DataList `DataBinding` 이벤트가 발생 하면 데이터 원본 열거 및 각 데이터 레코드 DataList에 바인딩됩니다. 데이터 원본의 각 레코드에 대해 DataList 만듭니다는 [ `DataListItem` ](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.datalistitem.aspx) 되는 개체를 다음 현재 레코드에 바인딩됩니다. 이 과정에서 DataList 두 이벤트를 발생 시킵니다.

- **`ItemCreated`**후에 발생는 `DataListItem` 만든
- **`ItemDataBound`**현재 레코드에 바인딩된 후에 발생는`DataListItem`

다음 단계 DataList 컨트롤에 대 한 데이터 바인딩 프로세스를 간략하게 설명합니다.

1. DataList s [ `DataBinding` 이벤트](https://msdn.microsoft.com/en-us/library/system.web.ui.control.databinding.aspx) 발생 합니다.
2. DataList에 데이터 바인딩된  
  
 데이터 원본에 있는 각 레코드에 대 한 

    1. 만들기는 `DataListItem` 개체
    2. 화재는 [ `ItemCreated` 이벤트](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.datalist.itemcreated.aspx)
    3. 해당 레코드를 바인딩하는`DataListItem`
    4. 화재는 [ `ItemDataBound` 이벤트](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.datalist.itemdatabound.aspx)
    5. 추가 `DataListItem` 에 `Items` 컬렉션

반복기 컨트롤을 데이터 바인딩하는 경우 동일한 일련의 단계를 통해 진행 됩니다. 유일한 차이점은 대신 `DataListItem` 인스턴스를 만들고, 반복기 사용 하 여 [ `RepeaterItem` ](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.repeateritem(VS.80).aspx)s입니다.

> [!NOTE]
> 예리한 독자 GridView 데이터에 바인딩될 때 DataList와 반복기와 데이터에 연결 되는 경우 지정 전까지 대기 하는 단계의 순서 간에 약간의 비정상을 보았을 수 있습니다. 데이터 바인딩 프로세스의 꼬리 끝 GridView 발생는 `DataBound` 이벤트가 있습니다; 그러나 DataList 아니고 반복기 제어는 이러한 이벤트입니다. 전처리 및 후 수준의 이벤트 처리기 패턴 일반적인 렸 전에 DataList 및 반복기 컨트롤은 ASP.NET 1.x 기간에 다시 만든 때문입니다.


GridView와 데이터를 기반으로 서식을 지정 하기 위한 한 가지 옵션에 대 한 이벤트 처리기를 만드는 것 처럼는 `ItemDataBound` 이벤트입니다. 이 이벤트 처리기에 바인딩된 것에 데이터를 검사 합니다는 `DataListItem` 또는 `RepeaterItem` 필요에 따라 컨트롤의 서식에 영향을 줍니다.

DataList 컨트롤에 대 한 변경 내용을 사용 하 여 전체 항목을 구현할 수 있습니다에 대 한 서식는 `DataListItem` s 스타일 관련를 포함 하는 속성은 표준 `Font`, `ForeColor`, `BackColor`, `CssClass`등입니다. DataList의 템플릿 내에서 특정 웹 컨트롤의 서식에 영향을 주지만를 프로그래밍 방식으로 액세스 하 고 해당 웹 컨트롤의 스타일을 수정 해야 합니다. 이 다시 수행 하는 방법에 살펴보았습니다는 *데이터 기반 시 사용자 지정 서식* 자습서입니다. 반복기 컨트롤 같은 `RepeaterItem` 클래스 속성이 없는 스타일 관련; 모든 스타일 관련 변경 내용이 따라서는 `RepeaterItem` 에 `ItemDataBound` 이벤트 처리기를 프로그래밍 방식으로 액세스 하 고 내에서 웹 컨트롤을 업데이트 하 여 수행 해야 합니다 템플릿입니다.

이후는 `ItemDataBound` DataList 및 반복기는 거의 동일 예제 중점적으로 DataList를 사용 하 여 기술 서식 지정 합니다.

## <a name="step-1-displaying-product-information-in-the-datalist"></a>1 단계: DataList에서 제품 정보를 표시합니다.

서식을 걱정, 먼저 let s DataList를 사용 하 여 제품 정보를 표시 하는 페이지를 만듭니다. 에 [이전 자습서](displaying-data-with-the-datalist-and-repeater-controls-cs.md) DataList 만든 인 `ItemTemplate` 각 s 제품 이름, 범주, 공급 업체, 단위, 가격과 수량을 표시 합니다. 이 자습서에서는이 기능을 여기 반복 s를 사용 합니다. 이를 위해 DataList 및 처음부터 해당 ObjectDataSource 하거나 다시 만들 수 있고 이전 자습서에서 만든 페이지에서 이러한 컨트롤에 복사할 수도 있습니다 (`Basics.aspx`)이이 자습서에 대 한 페이지에 붙여 넣습니다 (`Formatting.aspx`).

DataList 및 ObjectDataSource 기능을 복제 한 후 `Basics.aspx` 에 `Formatting.aspx`, s DataList를 변경 하려면 잠시 `ID` 속성을 `DataList1` 하는 보다 자세한 `ItemDataBoundFormattingExample`합니다. 다음으로 브라우저에서 DataList를 봅니다. 그림 1에서 볼 수 있듯이 서식 각 제품 간의 점만 배경색 번갈아 전환 합니다.


[![DataList 컨트롤에서 제품 나와](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image2.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image1.png)

**그림 1**: The 제품 DataList 컨트롤에 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image3.png))


이 자습서에 대 한 s $20.00 보다 낮은 가격으로 제품 이름이 지정 됩니다 모두 해당 하 고 단위 가격 강조 표시 된 노란색 DataList 서식을 사용 수 있습니다.

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-itemdatabound-event-handler"></a>2 단계: ItemDataBound 이벤트 처리기에 있는 데이터의 값을 프로그래밍 방식으로 결정

제품 가격이 $20.00가 적용할 사용자 지정 서식에 한에서는 각 제품의 가격을 확인할 수 여야 합니다. DataList 데이터를 바인딩할 때 DataList 데이터 소스에서 레코드를 열거 하 고, 각 레코드를 만듭니다는 `DataListItem` 하도록 데이터 원본 레코드 바인딩 인스턴스는 `DataListItem`합니다. 특정 레코드 s 후 데이터에 바인딩된 현재 `DataListItem` 개체, s DataList `ItemDataBound` 이벤트가 발생 합니다. 현재에 대 한 데이터 값을 검사 하려면이 이벤트에 대 한 이벤트 처리기를 만들 수 있습니다 `DataListItem` 및 해당 값에 따라, 서식 필요한 경우 변경 합니다.

만들기는 `ItemDataBound` DataList에 대 한 이벤트를 다음 코드를 추가 합니다.


[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample1.cs)]

개념 및 s DataList 뒤 의미 하는 동안 `ItemDataBound` 이벤트 처리기는 GridView s에서 사용 하는 것과 동일 `RowDataBound` 의 이벤트 처리기는 *데이터 기반 시 사용자 지정 서식* 자습서에서는 구문을 다릅니다 약간 합니다. 경우는 `ItemDataBound` 이벤트 발생은 `DataListItem` 만 데이터에 바인딩된을 통해 해당 이벤트 처리기에 전달 되 `e.Item` (대신 `e.Row`GridView s와 마찬가지로, `RowDataBound` 이벤트 처리기). DataList s `ItemDataBound` 이벤트 처리기에 대해 발생 *각* 행 머리글 행, 바닥글 행 및 행 구분 기호를 포함 하 여 DataList에 추가 합니다. 그러나 제품 정보만 데이터 행에 바인딩되어 있습니다. 따라서 사용 하는 경우는 `ItemDataBound` 있는지 먼저 확인 해야 이벤트 데이터를 검사할 DataList에 바인딩된 다시 데이터 항목을 사용 했습니다. 이 확인 하 여 수행할 수 있습니다는 `DataListItem` s [ `ItemType` 속성](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.datalistitem.itemtype.aspx), 중 하나를 사용할 수 있는 [다음 8 개의 값](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.listitemtype.aspx):

- `AlternatingItem`
- `EditItem`
- `Footer`
- `Header`
- `Item`
- `Pager`
- `SelectedItem`
- `Separator`

둘 다 `Item` 및 `AlternatingItem``DataListItem`의 구성 DataList의 데이터 항목입니다. 작업을 다시 가정 우리는 `Item` 또는 `AlternatingItem`, 우리는 실제 액세스 `ProductsRow` 현재에 바인딩된 인스턴스 `DataListItem`합니다. `DataListItem` s [ `DataItem` 속성](https://msdn.microsoft.com/en-us/system.web.ui.webcontrols.datalistitem.dataitem.aspx) 포함에 대 한 참조는 `DataRowView` 개체의 `Row` 속성은 실제에 대 한 참조를 제공 `ProductsRow` 개체입니다.

다음으로 확인 된 `ProductsRow` 인스턴스의 `UnitPrice` 속성. Products 테이블 s 이후 `UnitPrice` 필드를 사용 하면 `NULL` 값에 액세스 하기 전에 `UnitPrice` 속성에서는 있는지 먼저 확인 해야 있는지는 `NULL` 를 사용 하 여 값의 `IsUnitPriceNull()` 메서드. 경우는 `UnitPrice` 값이 `NULL`, 그런 다음 확인 있는지 것 s $20.00 보다 작은 합니다. 인 경우 아래에서 실제로 $20.00 다음 사용자 지정 서식 지정을 적용 해야 합니다.

## <a name="step-3-highlighting-the-product-s-name-and-price"></a>3 단계: 제품 s 이름과 가격을 강조 표시

S 제품 가격이 $20.00 보다 작은 인지 알고 있으므로, 이제 남은 것의 이름과 가격을 강조 표시 합니다. 이를 위해에서는 먼저 프로그래밍 방식으로 참조 해야에서 Label 컨트롤은 `ItemTemplate`의 제품 이름 및 가격을 표시 하는 합니다. 다음으로, 노란색 배경을 표시 하도록 해야 합니다. 레이블을 직접 수정 하 여 이러한 서식 지정 정보를 적용할 수 있습니다 `BackColor` 속성 (`LabelID.BackColor = Color.Yellow`); 이상적으로 연계 스타일 시트를 통해 모든 디스플레이 관련 된 문제 하지만 표현 해야 합니다. 실제로 스타일 시트에 정의 된 원하는 형식을 제공 하는 이미 보유 `Styles.css`  -  `AffordablePriceEmphasis`, 생성 되어에서 설명 하는 *데이터 기반 시 사용자 지정 서식* 자습서입니다.

서식 지정을 적용 하려면 두 Label 웹 컨트롤을 설정 하기만 하면 `CssClass` 속성을 `AffordablePriceEmphasis`다음 코드에 나온 것 처럼:


[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample2.cs)]

와 `ItemDataBound` 다시 확인을 완료 하는 이벤트 처리기는 `Formatting.aspx` 브라우저에서 페이지입니다. 그림 2에서 알 수 있듯이, 해당 제품 가격이 $20.00 아래에 들어 있는 이름 및 강조 표시 하는 가격 모두 합니다.


[![이러한 제품 보다 작은 $20.00 강조 표시 됩니다.](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image5.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image4.png)

**그림 2**: 된 제품 보다 작은 $20.00 강조 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image6.png))


> [!NOTE]
> DataList는 HTML로 렌더링 됩니다 이후 `<table>`, 해당 `DataListItem` 인스턴스 특정 스타일 전체 항목을 적용 하려면 설정할 수 있는 스타일 관련 속성을 가집니다. 예를 들어, 강조 표시 하 려 하는 경우는 *전체* 해당 가격을 $20.00 보다 작은 경우 항목 노란색, 수 있는 교체 레이블을 참조 하는 코드 설정 하 고 해당 `CssClass` 코드의 다음 줄을 사용 하 여 속성: `e.Item.CssClass = "AffordablePriceEmphasis"` (그림 3 참조).


그러나 `RepeaterItem` s don t 반복기 컨트롤을 구성 하는 등의 스타일 수준 속성을 제공 합니다. 따라서 반복기에는 사용자 지정 서식을 적용 그림 2에서 했던 것 처럼 반복기의 템플릿 내에서 웹 컨트롤에 대 한 스타일 속성의 응용 프로그램이 필요 합니다.


[![$20.00에서 제품에 대 한 전체 제품 항목 강조 표시 됩니다.](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image8.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image7.png)

**그림 3**: $20.00에서 제품에 대 한 전체 제품 항목은 강조 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image9.png))


## <a name="using-formatting-functions-from-within-the-template"></a>템플릿 내에서 서식 지정 기능을 사용 하 여

에 *GridView 컨트롤에 사용 하 여 TemplateFields* GridView의 행에 바인딩된 자습서에서 데이터에 기반한 사용자 지정 서식을 적용 하려면 GridView TemplateField 내에서 형식 지정 함수를 사용 하는 방법에 살펴보았습니다. 서식 지정 함수는 서식 파일에서 호출할 수 있으며 HTML 그 자리에 내보낼 수를 반환 하는 메서드. 서식 지정 기능 ASP.NET 페이지의 코드 숨김 클래스에 있을 수 있습니다 또는의 클래스 파일을 중앙 집중화할 수 있습니다는 `App_Code` 폴더 또는 별도 클래스 라이브러리 프로젝트. ASP.NET 페이지의 코드 숨김 클래스 외부에서 형식 지정 함수를 이동 하는 것은 다른 ASP.NET 웹 응용 프로그램 또는 여러 ASP.NET 페이지에 동일한 서식 지정 기능을 사용 하려는 경우에 이상적입니다.

서식 지정 기능을 보여 주기 위해 s 수 있는 경우 s 제품 이름 옆에 있는 텍스트 [단종]를 포함 하는 제품 정보 것 s 이상 사용 되지 않습니다. 또한 let s 가격 강조 표시 된 노란색 경우는 두 개 것 s $20.00 보다 작은 (에서 같이 `ItemDataBound` 이벤트 처리기 예제) 가격이 $20.00 또는 더 높은, let s에 실제 가격을 모두 표시 되지 않지만 하십시오 텍스트 견적 가격에 대 한 호출 하는 대신 하는 경우. 그림 4에서는 이러한 서식 지정 규칙이 적용 된 나열 하는 제품의 스크린 샷을 보여 줍니다.


[![호출 하 여 견적 가격에 대 한 텍스트로 바뀝니다 가격이 비싼 제품에 대 한](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image11.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image10.png)

**그림 4**: 비용이 많이 드는 제품에 대 한 가격 견적 가격에 대 한 호출 하 여 하십시오 텍스트로 바뀝니다 ([전체 크기 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image12.png))


## <a name="step-1-create-the-formatting-functions"></a>1 단계: 서식 함수 만들기

이 예에서는 두 가지 서식 지정 기능, 필요한 경우 [단종] 텍스트와 함께 제품 이름을 표시 하 고 다른 필요한 경우 강조 표시 된 가격을 표시 하는 대 한 것 s $20.00, 또는 텍스트를 호출 하 여 가격 견적을 다른 방법에 대 한 보다 작은 합니다. ASP.NET 페이지의 코드 숨김 클래스에서 이러한 함수를 만들고 이름을 지정 하 여 s `DisplayProductNameAndDiscontinuedStatus` 및 `DisplayPrice`합니다. 두 방법 모두를 HTML 문자열로 렌더링을 반환 해야 합니다. 및 표시 해야 하는 둘 다 `Protected` (또는 `Public`) ASP.NET 페이지 s 선언적 구문 부분에서 호출할 수 있도록 합니다. 이러한 두 가지 방법에 대 한 코드는 다음과 같습니다.


[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample3.cs)]

`DisplayProductNameAndDiscontinuedStatus` 메서드는 값의는 `productName` 및 `discontinued` 반면 스칼라 값으로 데이터 필드는 `DisplayPrice` 메서드에 `ProductsRow` 인스턴스 (아닌 `unitPrice` 스칼라 값). 어느 방법이 든 작동 합니다. 그러나 서식 지정 기능 작업 데이터베이스를 포함할 수 있는 스칼라 값 하는 경우 `NULL` 값 (같은 `UnitPrice`모두; `ProductName` 나 `Discontinued` 허용 `NULL` 값), 특별 한 주의 해야 이러한 처리 스칼라 입력 합니다.

특히 입력된 매개 변수 형식 이어야 합니다 `Object` 들어오는 값이 될 수는 `DBNull` 예상된 데이터 형식 대신 인스턴스. 또한 들어오는 값 데이터베이스 인지 여부를 결정 하기 위해 확인을 수행 해야 `NULL` 값입니다. 즉, 있으니까요는 `DisplayPrice` d 우리는 스칼라 값으로 가격을 적용 하려면 다음 코드를 사용 해야 합니다.


[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample4.cs)]

`unitPrice` 형식의 입력된 매개 변수는 `Object` 및 확인 하는 경우 수정 된 조건 문에 `unitPrice` 은 `DBNull` 여부입니다. 또한 이후에 `unitPrice` 입력된 매개 변수로 전달 됩니다는 `Object`, 10 진수 값으로 캐스팅 되어야 합니다.

## <a name="step-2-calling-the-formatting-function-from-the-datalist-s-itemtemplate"></a>S DataList의 ItemTemplate에서 서식 지정 함수를 호출 하는 2 단계:

ASP.NET 페이지의 코드 숨김 클래스에 추가 하는 서식 지정 함수를 사용 했으므로 이제 남은 것 이러한 서식 s DataList의 함수를 호출 하려면 `ItemTemplate`합니다. 서식 파일에서 형식 지정 함수를 호출 하려면 databinding 구문 내에서 함수 호출을 배치 합니다.


[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample5.aspx)]

DataList s에서에서 `ItemTemplate` 는 `ProductNameLabel` Label 웹 컨트롤 현재 이름을 표시 하는 제품 s 할당 하 여 해당 `Text` 결과 속성의 `<%# Eval("ProductName") %>`합니다. 유지 하기 위해 필요한 경우 이름과 [단종] 텍스트를 표시, 선언적 구문 대신 할당 되도록 업데이트는 `Text` 속성 값의는 `DisplayProductNameAndDiscontinuedStatus` 메서드. 이렇게 할 경우 s 제품 이름 및 사용 하 여 지원 되지 않는 값에 전달 해야는 `Eval("columnName")` 구문입니다. `Eval`형식의 값을 반환 `Object`, 하지만 `DisplayProductNameAndDiscontinuedStatus` 메서드에서 입력된 매개 변수 형식의 예상 `String` 및 `Boolean`이므로, 반환 하는 값을 캐스팅 해야 했습니다는 `Eval` 같이 메서드를 필요한 입력된 매개 변수 형식:


[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample6.aspx)]

가격을 표시 하려면 설정 하기만 했습니다는 `UnitPriceLabel` 레이블 s `Text` 속성에서 반환 된 값을는 `DisplayPrice` 메서드를 것 처럼 s 제품 이름을 표시 하기 위한을 [중단] 텍스트입니다. 그러나에 전달 하는 대신에는 `UnitPrice` 스칼라 입력된 매개 변수로 대신 전달 하면 전체에서 `ProductsRow` 인스턴스:


[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample7.aspx)]

위치에 서식 지정 함수를 호출을 하는 브라우저에서 진행률을 볼 수 보십시오. [단종] 텍스트를 포함 하 여 지원 되지 않는 제품과 함께 화면이 그림 5와 유사한 표시 고 해당 제품의 가격 필요 $20.00 이상 비용 계산과 대체 텍스트 하십시오 견적 가격에 대 한 호출.


[![호출 하 여 견적 가격에 대 한 텍스트로 바뀝니다 가격이 비싼 제품에 대 한](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image14.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image13.png)

**그림 5**: 비용이 많이 드는 제품에 대 한 가격 견적 가격에 대 한 호출 하 여 하십시오 텍스트로 바뀝니다 ([전체 크기 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image15.png))


## <a name="summary"></a>요약

DataList 또는 반복기 컨트롤에서 데이터에 기반한 내용의 서식을 지정 두 기술을 사용 하 여 수행할 수 있습니다. 첫 번째 방법은 대 한 이벤트 처리기를 만들려는 `ItemDataBound` 새에 바인딩된 데이터 소스의 각 레코드에에서 따라 발생 하는 이벤트 `DataListItem` 또는 `RepeaterItem`합니다. 에 `ItemDataBound` 이벤트 처리기는 현재 s 항목 데이터를 검사 하 고 서식을 지정 하는 템플릿 또는 내용에 적용할 수 있습니다 `DataListItem` s 전체 항목 자체를 합니다.

또는 사용자 지정 형식 지정 함수를 서식 지정을 통해 실현할 수 있습니다. 서식 지정 함수는 DataList에서 호출할 수 있는 메서드를 내보내는 해당 위치에 HTML을 반환 하는 반복기의 템플릿을입니다. 종종 HTML 서식 지정 함수에서 반환 된 현재 항목에 바인딩되는 값에 의해 결정 됩니다. 스칼라 값 또는 항목에 바인딩되는 전체 개체를 전달 하 여 이러한 값 서식 지정 함수에 전달할 수 있습니다 (예:는 `ProductsRow` 인스턴스).

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가 Yaakov Ellis, Randy Schmidt 및 Liz Shulok 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](displaying-data-with-the-datalist-and-repeater-controls-cs.md)
[다음](showing-multiple-records-per-row-with-the-datalist-control-cs.md)
