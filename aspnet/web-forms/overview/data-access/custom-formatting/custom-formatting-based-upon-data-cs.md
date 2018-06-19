---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-cs
title: 데이터 (C#)를 기반으로 사용자 지정 서식을 | Microsoft Docs
author: rick-anderson
description: GridView, DetailsView, 또는 데이터를 바인딩할 기반 FormView의 형식이 조정 하는 여러 가지 방법으로 수행할 수 있습니다. 이 자습서에서는 त ु म च l...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 871a4574-f89c-4214-b786-79253ed3653b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 31cf628baf2250c2e7e71ab38cd64b218dc927e7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30876867"
---
<a name="custom-formatting-based-upon-data-c"></a>데이터 (C#)를 기반으로 사용자 지정 형식 지정
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_11_CS.exe) 또는 [PDF 다운로드](custom-formatting-based-upon-data-cs/_static/datatutorial11cs1.pdf)

> GridView, DetailsView, 또는 데이터를 바인딩할 기반 FormView의 형식이 조정 하는 여러 가지 방법으로 수행할 수 있습니다. 이 자습서에서는 데이터 바인딩된 데이터 바인딩된 및 RowDataBound 이벤트 처리기를 사용 하 여 서식 지정을 수행 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

GridView, DetailsView, FormView 컨트롤의 모양은 다양 한 스타일 관련 속성을 통해 사용자 지정할 수 있습니다. 같은 속성 `CssClass`, `Font`, `BorderWidth`, `BorderStyle`, `BorderColor`, `Width`, 및 `Height`, 맺음 렌더링 된 컨트롤의 일반적인 모양을 지정 합니다. 포함 하 여 속성 `HeaderStyle`, `RowStyle`, `AlternatingRowStyle`, 스타일 설정과 특정 섹션에 적용 될 수 있도록 다른 사용자입니다. 마찬가지로, 이러한 스타일 설정은 필드 수준에서 적용할 수 있습니다.

대부분의 시나리오에서 하지만 형식 지정 요구 사항에 따라 달라 표시 된 데이터의 값. 예를 들어 하기 위해의 제품을 판매, 제품 정보를 나열 하는 보고서 수 배경색 설정 갖는 해당 제품에 대 한 노란색 `UnitsInStock` 및 `UnitsOnOrder` 필드는 모두 0입니다. 비용이 많이 드는 products를 강조 표시 굵은 글꼴로 이상 $75.00 비용 계산과 해당 제품의 가격을 표시 하려고 수 있습니다.

GridView, DetailsView, 또는 데이터를 바인딩할 기반 FormView의 형식이 조정 하는 여러 가지 방법으로 수행할 수 있습니다. 이 자습서에서 살펴보게 데이터 연결을 사용 하 여 서식 지정을 수행 하는 방법의 `DataBound` 및 `RowDataBound` 이벤트 처리기입니다. 다음 자습서는 대체 접근 방식을 살펴보겠습니다.

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a>DetailsView 컨트롤을 사용 하 여`DataBound`이벤트 처리기

경우에 바인딩된 데이터가 DetailsView, 데이터 소스 제어에서 또는 프로그래밍 방식으로 데이터를 컨트롤의 할당을 통해 `DataSource` 속성과 호출 해당 `DataBind()` 메서드를 다음 단계를 순서 대로 발생:

1. 데이터 웹 컨트롤의 `DataBinding` 이벤트 발생 합니다.
2. 데이터는 데이터 웹 컨트롤에 바인딩됩니다.
3. 데이터 웹 컨트롤의 `DataBound` 이벤트 발생 합니다.

1 단계와 3 단계는 이벤트 처리기를 통해 직후 사용자 지정 논리 삽입 될 수 있습니다. 에 대 한 이벤트 처리기를 만들어서는 `DataBound` 이벤트 데이터 웹 컨트롤에 바인딩되고 서식이 필요에 따라 조정 된 데이터를 프로그래밍 방식으로 확인할 수 있습니다. 이 설명 하기 위해 이제 제품에 대 한 일반 정보를 표시 하지만 ½ ֳ µ DetailsView를 만들는 `UnitPrice` 값에 ***굵게, 기울임꼴 글꼴*** $75.00 초과 하는 경우.

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a>1 단계: DetailsView에 제품 정보를 표시합니다.

열기는 `CustomColors.aspx` 페이지에 `CustomFormatting` 폴더를 디자이너 도구 상자에서 DetailsView 컨트롤을 끌어, 설정 해당 `ID` 속성 값을 `ExpensiveProductsPriceInBoldItalic`, 고 호출 하는 새 ObjectDataSource 컨트롤에 바인딩하는 `ProductsBLL` 클래스의 `GetProducts()` 메서드. 이 작업을 수행 하는 자세한 단계는 이전 자습서에서 자세히 살펴보고 이러한 이후 편의상 여기 생략 됩니다.

DetailsView에는 ObjectDataSource를 바인딩된 한 후 필드 목록을 수정 하려면 잠시. 제거를 선택한 이유는 `ProductID`, `SupplierID`, `CategoryID`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`, 및 `Discontinued` BoundFields 바뀌고 나머지 BoundFields 다시 포맷 하 고 있습니다. 도 취소는 `Width` 및 `Height` 설정 합니다. DetailsView에 하나의 레코드만 표시, 되므로 최종 사용자를 모든 제품을 볼 수 있도록 하기 위해 페이징 사용 하도록 설정 해야 합니다. DetailsView의 스마트 태그에서 페이징 사용 확인란을 선택 하 여 그렇게 합니다.


[![확인란을 사용 하도록 설정 페이징 DetailsView의 스마트 태그](custom-formatting-based-upon-data-cs/_static/image2.png)](custom-formatting-based-upon-data-cs/_static/image1.png)

**그림 1**: 확인란을 사용 하도록 설정 페이징 DetailsView의 스마트 태그 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image3.png))


이러한 변경 내용은 다음 DetailsView 태그 수 있습니다.


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample1.aspx)]

브라우저에서이 페이지를 테스트해 보십시오.


[![DetailsView 컨트롤은 한 번에 제품 중 하나를 표시합니다.](custom-formatting-based-upon-data-cs/_static/image5.png)](custom-formatting-based-upon-data-cs/_static/image4.png)

**그림 2**: The DetailsView 컨트롤 표시 한 제품 한 번에 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image6.png))


## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>2 단계: 데이터 바인딩된 이벤트 처리기에 있는 데이터의 값을 프로그래밍 방식으로 결정

이러한 제품에 대 한 굵게, 기울임꼴 글꼴의 가격을 표시 하려면 해당 `UnitPrice` 값 초과 $75.00, 프로그래밍 방식으로 결정을 해야는 `UnitPrice` 값입니다. 수행할 수이 고 DetailsView에 대 한는 `DataBound` 이벤트 처리기입니다. 이벤트를 만들면 처리기 디자이너에서 DetailsView 클릭 속성 창으로 이동 합니다. F4 키를 눌러를 불러오는 되지 않았으면 표시할지 보기 메뉴로 이동 하 고 속성 창 메뉴 옵션을 선택 합니다. 속성 창에서 DetailsView의 이벤트를 나열 하려면 번개 모양 아이콘을 클릭 합니다. 다음으로, 두 번 클릭은 `DataBound` 이벤트 또는 이벤트 처리기를 만들려는 이름을 입력 합니다.


![데이터 바인딩된 이벤트에 대 한 이벤트 처리기 만들기](custom-formatting-based-upon-data-cs/_static/image7.png)

**그림 3**:에 대 한 이벤트 처리기 만들기는 `DataBound` 이벤트


이렇게 해도 이벤트 처리기를 만들고 있으며 코드 부분으로 이동 위치에 추가 된 자동으로 됩니다. 이 시점에서 볼 수 있습니다.


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample2.cs)]

DetailsView에 바인딩된 데이터를 통해 액세스할 수는 `DataItem` 속성입니다. DataRow 인스턴스 강력한 형식의 컬렉션으로 이루어진 강력한 형식의 DataTable에 컨트롤을 바인딩하는 것을 기억 하십시오. DataTable의 첫 번째 DataRow DetailsView의에 할당 된 DataTable DetailsView에 바인딩되면 `DataItem` 속성입니다. 특히,는 `DataItem` 속성에 할당 되는 `DataRowView` 개체입니다. 사용할 수는 `DataRowView`의 `Row` 속성은 기본 DataRow 개체에 액세스 하는 실제로 `ProductsRow` 인스턴스. 이 있으면 `ProductsRow` 단순히 개체의 속성 값을 검사 하 여 결정을 위해 인스턴스.

다음 코드를 확인 하는 방법을 보여 줍니다 여부는 `UnitPrice` DetailsView 컨트롤에 바인딩된 값이 $75.00 보다 큽니다.


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample3.cs)]

> [!NOTE]
> 이후 `UnitPrice` 가질 수 있습니다는 `NULL` 값은 데이터베이스에 먼저 확인을 있는지 지금 하지 다루고 있는 있는지 확인 한 `NULL` 값에 액세스 하기 전에 `ProductsRow`의 `UnitPrice` 속성입니다. 이 검사는 중요 하기 때문에 액세스 하려고 하면는 `UnitPrice` 속성에 있을 때는 `NULL` 값은 `ProductsRow` 개체를 발생 시킵니다는 [StrongTypingException 예외](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx)합니다.


## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a>3 단계: DetailsView에서 UnitPrice 값 서식 지정

이 시점에서 확인할 수 있습니다 여부는 `UnitPrice` DetailsView에 바인딩된 값 $75.00를 초과 하는 값을 갖지만을 프로그래밍 방식으로 DetailsView를 조정 하는 방법을 참조의 서식 지정에 따라 아직 했습니다. DetailsView에 있는 전체 행의 서식을 수정 하려면 프로그래밍 방식으로 액세스를 사용 하 여 행 `DetailsViewID.Rows[index]`사용 하 여 액세스를 특정 셀을 수정 하려면 `DetailsViewID.Rows[index].Cells[index]`합니다. 행 또는 셀에 대 한 참조가 있으면 해당 스타일 관련 속성을 설정 하 여 모양을 다음 조정 수 합니다.

행을 프로그래밍 방식으로 액세스 0에서 시작 하는 행의 인덱스를 알고 있어야 합니다. `UnitPrice` 행이 다섯 번째 행 4의 인덱스를 제공 하 고 프로그래밍 방식으로 액세스할 수 있게 DetailsView에서 사용 하 여 `ExpensiveProductsPriceInBoldItalic.Rows[4]`합니다. 이 시점에서 다음 코드를 사용 하 여 굵게, 기울임꼴 글꼴에 표시 되는 행의 전체 내용을 만들어졌을:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample4.cs)]

그러나 이렇게 하면 *둘 다* (Price) 레이블과 굵게 및 기울임꼴 값입니다. 값만 굵게 및 기울임꼴는 다음을 사용 하 여 수행할 수는 행의 두 번째 셀에 서식을 적용 하기 위해서 필요를 확인 하려면:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample5.cs)]

이 자습서 지금까지 스타일 시트를 명확히 구분 된 렌더링 된 태그 및 스타일 관련 정보를 유지 관리를 사용한 이후 위와 같이 보겠습니다 대신 특정 스타일 속성을 설정 하는 대신 CSS 클래스를 사용 합니다. 열기는 `Styles.css` 스타일 시트 라는 새 CSS 클래스를 추가 하 고 `ExpensivePriceEmphasis` 다음 정의 사용 합니다.


[!code-css[Main](custom-formatting-based-upon-data-cs/samples/sample6.css)]

그런 다음는 `DataBound` 이벤트 처리기 설정 셀의 `CssClass` 속성을 `ExpensivePriceEmphasis`합니다. 다음 코드는 `DataBound` 전체에서 이벤트 처리기.


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample7.cs)]

Chai 75.00 $ 비용을 보는 가격 보통 글꼴에 표시 됩니다 (그림 4 참조). 그러나, $97.00 가격이 있는 Mishi 산호세 Niku 볼 때 가격에에서 표시 됩니다 굵게, 기울임꼴 글꼴 (그림 5 참조).


[![$75.00 보다 적은 가격 보통 글꼴로 표시 됩니다.](custom-formatting-based-upon-data-cs/_static/image9.png)](custom-formatting-based-upon-data-cs/_static/image8.png)

**그림 4**: $75.00 보다 적은 가격 보통 글꼴로 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image10.png))


[![비용이 많이 드는 제품의 가격이 굵게, 기울임꼴 글꼴에에서 표시 됩니다.](custom-formatting-based-upon-data-cs/_static/image12.png)](custom-formatting-based-upon-data-cs/_static/image11.png)

**그림 5**: 비용이 많이 드는 제품의 가격이 굵게, 기울임꼴 글꼴에에서 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image13.png))


## <a name="using-the-formview-controlsdataboundevent-handler"></a>FormView 컨트롤을 사용 하 여`DataBound`이벤트 처리기

DetailsView 만들기에 대 한 기본 데이터는 FormView에 바인딩된을 결정 하기 위한 단계는 동일 하 게 한 `DataBound` 캐스팅 하는 이벤트 처리기는 `DataItem` 속성을 적절 한 개체 형식에는 컨트롤에 바인딩된 하 고 계속 진행 하는 방법을 결정 합니다. 그러나 FormView 및 DetailsView 다 해당 사용자 인터페이스의 모양을 업데이트 하는 방법에.

FormView 모든 BoundFields 포함 하지 않으며 따라서에 게 없는 경우는 `Rows` 컬렉션입니다. 정적 HTML의 혼합을 포함할 수 있는 템플릿의 FormView은 구성 하는 대신, 웹 컨트롤 및 데이터 바인딩 구문입니다. 일반적으로 FormView의 스타일을 조정 FormView의 템플릿 내에서 웹 컨트롤 중 하나 이상의 스타일을 조정 해야 합니다.

이 설명 하기 보겠습니다 사용할 목록 제품에 FormView 보겠습니다 앞의 예에서 하지만이 이번에서와 같이 표시 제품 이름 및 단위 재고 제품의 재고 10 보다 작거나 경우 빨간색 글꼴로 표시.

## <a name="step-4-displaying-the-product-information-in-a-formview"></a>4 단계:는 FormView에 제품 정보를 표시합니다.

에 FormView 추가 `CustomColors.aspx` 집합과 DetailsView 아래에 있는 페이지의 `ID` 속성을 `LowStockedProductsInRed`합니다. FormView의 이전 단계에서 만든 ObjectDataSource 컨트롤에 바인딩하십시오. 이렇게 하면 만들어집니다는 `ItemTemplate`, `EditItemTemplate`, 및 `InsertItemTemplate` FormView에 대 한 합니다. 제거는 `EditItemTemplate` 및 `InsertItemTemplate` 를 빠르고 간편 하는 `ItemTemplate` 포함 하도록 테이블만 `ProductName` 및 `UnitsInStock` 서로 자체 적절 하 게 이름이 지정 된 레이블 컨트롤에 있는 값입니다. 앞의 예제에서 DetailsView와 마찬가지로 또한 FormView의 스마트 태그에서 페이징 사용 확인란을 확인 합니다.

이 편집 내용을 후 FormView의 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample8.aspx)]

`ItemTemplate` 포함:

- **정적 HTML** 텍스트 "제품:" 및 "재고 수량이:"와 함께 `<br />` 및 `<b>` 요소입니다.
- **웹 컨트롤** 두 Label 컨트롤 `ProductNameLabel` 및 `UnitsInStockLabel`합니다.
- **데이터 바인딩된 구문을** 는 `<%# Bind("ProductName") %>` 및 `<%# Bind("UnitsInStock") %>` Label 컨트롤에 이러한 필드에서 값을 할당 하는 구문은 `Text` 속성입니다.

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>5 단계: 데이터 바인딩된 이벤트 처리기에 있는 데이터의 값을 프로그래밍 방식으로 결정

다음 단계는 태그로 FormView의 완료를 프로그래밍 방식으로 하는 경우를 확인 하는 `UnitsInStock` 값이 10 보다 작습니다. 이 인해 DetailsView 에서처럼 FormView와 정확히 같은 방식으로 수행 됩니다. FormView의에 대 한 이벤트 처리기를 만들어 시작 `DataBound` 이벤트입니다.


![데이터 바인딩된 이벤트 처리기 만들기](custom-formatting-based-upon-data-cs/_static/image14.png)

**그림 6**: 만들기는 `DataBound` 이벤트 처리기


이벤트 처리기 캐스팅 FormView의 `DataItem` 속성을는 `ProductsRow` 인스턴스를 확인 여부는 `UnitsInPrice` 값은 빨간색 글꼴로 표시 해야 하 합니다.


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample9.cs)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a>6 단계: FormView의 ItemTemplate에 UnitsInStockLabel Label 컨트롤 서식 지정

마지막 단계는 표시 된 형식을 지정 하는 `UnitsInStock` 값이 10 이하인 경우 빨간색 글꼴로 값입니다. 프로그래밍 방식으로 액세스 해야이를 위해는 `UnitsInStockLabel` 컨트롤에 `ItemTemplate` 해당 텍스트가 빨간색으로 표시 되도록 스타일 속성을 설정 합니다. 서식 파일에서 웹 컨트롤에 액세스 하려면 사용 된 `FindControl("controlID")` 다음과 같이 메서드:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample10.cs)]

컨트롤 레이블에 액세스 하려는 예제 `ID` 값은 `UnitsInStockLabel`이므로 사용:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample11.cs)]

웹 컨트롤에 대 한 프로그래밍 참조 했으므로 필요에 따라 해당 스타일 관련 속성 수정할 수 있습니다. 이전 예에서 만들었습니다.이 안에에서 CSS 클래스 처럼 `Styles.css` 라는 `LowUnitsInStockEmphasis`합니다. 이 스타일 웹 컨트롤에 적용할 설정 해당 `CssClass` 속성 적절 하 게 합니다.


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample12.cs)]

> [!NOTE]
> 프로그래밍 방식으로 사용 하 여 웹 컨트롤에 액세스 하는 서식 파일의 서식을 지정 하기 위한 구문을 `FindControl("controlID")` 스타일 관련 속성을 다음 설정도 사용할 수 있습니다 사용할 때 [TemplateFields](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) DetailsView 또는 GridView 제어 합니다. 이 다음 자습서 TemplateFields 검토 합니다.


그림 7에는 제품을 볼 때 FormView 나와 있는 `UnitsInStock` 그림 8에 있는 제품의 해당 값이 10 보다 작은 값이 10 보다 크고 합니다.


[![제품으로 정도 충분히 큰 Units In Stock, 사용자 지정 서식 없이 적용 됩니다.](custom-formatting-based-upon-data-cs/_static/image16.png)](custom-formatting-based-upon-data-cs/_static/image15.png)

**그림 7**:에 대 한 제품으로 정도 충분히 큰 Units In Stock, 사용자 지정 서식 없이 적용 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image17.png))


[![재고 수의 단위는 해당 제품으로의 값이 10 이하의 빨간색으로 표시 됩니다.](custom-formatting-based-upon-data-cs/_static/image19.png)](custom-formatting-based-upon-data-cs/_static/image18.png)

**그림 8**: 재고 수의 장치는 해당 제품으로의 값이 10 이하의 빨간색으로 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image20.png))


## <a name="formatting-with-the-gridviewsrowdataboundevent"></a>GridView의 서식을`RowDataBound`이벤트

이전 DetailsView 단계의 순서를 검사 했습니다 하 고 FormView 데이터 바인딩 중 통해 진행 상황을 제어 합니다. 살펴보겠습니다 다음이 단계를 통해 다시 한 번으로 쉽게 찾아볼.

1. 데이터 웹 컨트롤의 `DataBinding` 이벤트 발생 합니다.
2. 데이터는 데이터 웹 컨트롤에 바인딩됩니다.
3. 데이터 웹 컨트롤의 `DataBound` 이벤트 발생 합니다.

이러한 세 가지 간단한 단계는 하나의 레코드만 표시 하므로 DetailsView 및 FormView에 대 한 충분 한 합니다. 표시 하는 GridView에 대 한 *모든* 바인딩된 레코드를 (첫 번째 뿐 아니라 함), 2 단계가 약간 더 개입 됩니다.

GridView 데이터 원본 열거 만들고, 각 레코드에 대해 2 단계에서 한 `GridViewRow` 인스턴스를 현재 레코드 어셈블리에 바인딩합니다. 각 `GridViewRow` GridView에 추가 된 두 개의 이벤트가 발생 합니다.

- **`RowCreated`** 후에 발생는 `GridViewRow` 만든
- **`RowDataBound`** 현재 레코드에 바인딩된 후에 발생는 `GridViewRow`합니다.

GridView에 대 한 다음, 데이터 바인딩 보다 정확 하 게 설명에서 다음 단계를 순서 대로:

1. GridView의 `DataBinding` 이벤트 발생 합니다.
2. 데이터가는 GridView에 바인딩됩니다.   
  
   데이터 원본에 있는 각 레코드에 대 한 

    1. 만들기는 `GridViewRow` 개체
    2. 화재는 `RowCreated` 이벤트
    3. 해당 레코드를 바인딩하는 `GridViewRow`
    4. 화재는 `RowDataBound` 이벤트
    5. 추가 `GridViewRow` 에 `Rows` 컬렉션
3. GridView의 `DataBound` 이벤트 발생 합니다.

GridView의 개별 레코드의 형식의 사용자 지정 하려면 다음을 만들어야 한다는 대 한 이벤트 처리기는 `RowDataBound` 이벤트입니다. 이 설명 하기에 GridView를 추가 해 보겠습니다는 `CustomColors.aspx` 이름, 범주 및 해당 제품 가격이 $10.00 보다 작은 노란색 배경색으로 강조 표시 하는 각 제품에 대 한 가격을 나열 하는 페이지입니다.

## <a name="step-7-displaying-product-information-in-a-gridview"></a>7 단계:는 GridView에 제품 정보를 표시합니다.

이전 예제에서 FormView 아래에 GridView를 추가 하 고 설정의 `ID` 속성을 `HighlightCheapProducts`합니다. 페이지에서 모든 제품을 반환 하는 ObjectDataSource 이미 했기 때문에 바인딩할 GridView입니다. GridView의 BoundFields 방금: 제품의 이름, 범주 및 가격을 포함 하도록 마지막으로 편집 합니다. 이 편집 내용을 후 GridView의 태그는 같습니다.


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample13.aspx)]

그림 9 브라우저를 통해 표시 될 때 까지의 진행률을 보여줍니다.


[![이름, 범주 및 각 제품에 대 한 가격을 나열 하는 GridView](custom-formatting-based-upon-data-cs/_static/image22.png)](custom-formatting-based-upon-data-cs/_static/image21.png)

**그림 9**: 이름, 범주 및 각 제품에 대 한 가격을 나열 하는 GridView ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image23.png))


## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a>8 단계: RowDataBound 이벤트 처리기에 있는 데이터의 값을 프로그래밍 방식으로 결정

경우는 `ProductsDataTable` GridView에 바인딩됩니다 해당 `ProductsRow` 열거 하 고 각 인스턴스는 `ProductsRow` 는 `GridViewRow` 만들어집니다. `GridViewRow`의 `DataItem` 하는 특정 속성에 할당 됩니다 `ProductRow`는 GridView의 `RowDataBound` 이벤트 처리기는 발생 합니다. 확인 하는 `UnitPrice` GridView에 바인딩된 각 제품에 대 한 값이 다음 GridView의에 대 한 이벤트 처리기를 만들어야 한다는 `RowDataBound` 이벤트입니다. 이 이벤트 처리기에서 검사할 수 있습니다는 `UnitPrice` 현재에 대 한 값 `GridViewRow` 있도록 해당 행에 대 한 서식 지정 결정 합니다.

FormView와 DetailsView 같은 일련의 단계를 사용 하 여이 이벤트 처리기를 만들 수 있습니다.


![GridView의 RowDataBound 이벤트에 대 한 이벤트 처리기 만들기](custom-formatting-based-upon-data-cs/_static/image24.png)

**그림 10**: GridView의에 대 한 이벤트 처리기를 만들고 `RowDataBound` 이벤트


이런이 방식으로 이벤트 처리기를 만들면 다음 코드를 자동으로 ASP.NET 페이지의 코드 부분에 추가 하면:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample14.cs)]

경우는 `RowDataBound` 이벤트 발생 이벤트 처리기 매개 변수로 전달 되는 두 번째 형식의 개체 `GridViewRowEventArgs`, 라는 속성이 있는 `Row`합니다. 이 속성에 대 한 참조를 반환 합니다.는 `GridViewRow` 를 바인딩된 데이터 뿐입니다. 액세스는 `ProductsRow` 에 바인딩된 인스턴스는 `GridViewRow` 사용 하 여는 `DataItem` 같이 속성:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample15.cs)]

작업할 때의 `RowDataBound` GridView 다양 한 유형의 행으로 구성 된 하 고이 이벤트에 대해 발생 하는 점에 유의 해야 하는 이벤트 처리기 *모든* 행 형식입니다. A `GridViewRow`의 형식을 확인 하 여 해당 `RowType` 속성을 가능한 값 중 하나일 수 있습니다.

- `DataRow` GridView의에서 레코드에 바인딩되는 행 `DataSource`
- `EmptyDataRow` 경우에 표시 되는 행 GridView의 `DataSource` 비어
- `Footer` 바닥글 행입니다. 경우에 표시 된 GridView의 `ShowFooter` 속성 `true`
- `Header` 머리글 행입니다. GridView의 ShowHeader 속성이로 설정 되어 있으면 표시 `true` (기본값)
- `Pager` GridView의에 대 한 구현 하는 페이징, 페이징 인터페이스를 표시 하는 행
- `Separator` GridView에 대 한 사용 되지 않지만에서 사용 하는 `RowType` DataList와 반복기에 대 한 속성 컨트롤을 두 개의 데이터 웹 컨트롤에 설명 합니다 이후 자습서

이후는 `EmptyDataRow`, `Header`, `Footer`, 및 `Pager` 행 연관 되지 않습니다는 `DataSource` 레코드, 항상 수는 `null` 값을 해당 `DataItem` 속성입니다. 현재 사용 하 려 하기 전에 이러한 이유로 `GridViewRow`의 `DataItem` 속성을 항상 먼저 않도록 해야 것으로 처리 하는 한 `DataRow`합니다. 이 확인 하 여 수행할 수 있습니다는 `GridViewRow`의 `RowType` 같이 속성:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample16.cs)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a>9 단계: $10.00 보다 작은 행 노란색 When the UnitPrice 값을 강조 표시

마지막 단계는 프로그래밍 방식으로 전체 강조 표시 하는 `GridViewRow` 경우는 `UnitPrice` 행이 $10.00 보다 작은 값입니다. GridView의 행 또는 셀에 액세스 하기 위한 구문은 DetailsView와 마찬가지로 동일 `GridViewID.Rows[index]` 전체 행에 액세스 하 `GridViewID.Rows[index].Cells[index]` 특정 셀에 액세스할 수 있습니다. 그러나 때는 `RowDataBound` 이벤트 처리기를 데이터 바인딩된 발생 `GridViewRow` GridView의에 추가할 수는 아직 `Rows` 컬렉션입니다. 현재 액세스할 수 없는 따라서 `GridViewRow` 에서 인스턴스는 `RowDataBound` 행 컬렉션을 사용 하 여 이벤트 처리기입니다.

대신 `GridViewID.Rows[index]`, 현재를 참조할 수 있습니다 `GridViewRow` 인스턴스는 `RowDataBound` 이벤트 처리기를 사용 하 여 `e.Row`합니다. 즉, 순서를 현재 강조 표시 `GridViewRow` 에서 인스턴스는 `RowDataBound` 이벤트 처리기를 사용 합니다.


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample17.cs)]

설정 하지 않고는 `GridViewRow`의 `BackColor` 속성을 직접 CSS 클래스를 사용 하 여 집중 하겠습니다. 명명 된 CSS 클래스를 만들었습니다 `AffordablePriceEmphasis` 노란색으로 명령 프롬프트 창의 배경색을 설정 하는 합니다. 전체 `RowDataBound` 이벤트 처리기가 따르는:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample18.cs)]


[![가장 저렴 한 제품 노란색으로 강조 표시 됩니다.](custom-formatting-based-upon-data-cs/_static/image26.png)](custom-formatting-based-upon-data-cs/_static/image25.png)

**그림 11**: 가장 저렴 한 제품을 노란색으로 강조 표시 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image27.png))


## <a name="summary"></a>요약

이 자습서에서는 GridView, DetailsView, 및 컨트롤에 바인딩된 데이터를 기반으로 FormView 서식을 지정 하는 방법에 살펴보았습니다. 에 대 한 이벤트 처리기에서 만든이를 위해는 `DataBound` 또는 `RowDataBound` 이벤트, 필요한 경우 서식 변경 함께 기본 데이터 검사 되었습니다. DetailsView 또는 FormView에 바인딩된 데이터에 액세스 하려면 사용는 `DataItem` 속성에는 `DataBound` 이벤트 처리기는 GridView에 대 한; 각 `GridViewRow` 인스턴스의 `DataItem` 는 에서사용할수있는해당행에바인딩된데이터를포함하는속성`RowDataBound` 이벤트 처리기입니다.

프로그래밍 방식으로 데이터 웹 컨트롤의 서식 지정을 조정 하는 구문은 웹 컨트롤 및 서식을 지정할 데이터 표시 방법을 따라 달라 집니다. DetailsView 및 GridView에 대 한 컨트롤, 행 및 셀 서 수 인덱스에서 액세스할 수 있습니다. 서식 파일을 사용 하 여 FormView에 대 한는 `FindControl("controlID")` 메서드는 템플릿 내에서 웹 컨트롤을 찾기 위해 일반적으로 사용 됩니다.

다음 자습서는 GridView와 DetailsView 템플릿을 사용 하는 방법을 살펴보겠습니다. 또한 기본 데이터에 따라 서식을 사용자 지정 하기 위한 또 다른 방법은 살펴보겠습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 E.R. 되었습니다. Gilmore, Dennis Patterson 및 Dan Jagers 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](using-templatefields-in-the-gridview-control-cs.md)
