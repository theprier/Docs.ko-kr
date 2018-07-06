---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
title: 사용자 지정 형식 지정 데이터를 기반으로 (VB) | Microsoft Docs
author: rick-anderson
description: GridView, DetailsView 또는 FormView에 바인딩된 데이터를 기반으로 형식을 조정 하는 여러 가지 방법으로 수행할 수 있습니다. 이 자습서에서는 l을 합니다...
ms.author: aspnetcontent
ms.date: 03/31/2010
ms.assetid: df5a1525-386f-4632-972c-57b199870bc3
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
msc.type: authoredcontent
ms.openlocfilehash: d55a9ece22805d7f5d248e81a01d059dbde0ee18
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37809591"
---
<a name="custom-formatting-based-upon-data-vb"></a>사용자 지정 형식 지정 데이터를 기반으로 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_11_VB.exe) 또는 [PDF 다운로드](custom-formatting-based-upon-data-vb/_static/datatutorial11vb1.pdf)

> GridView, DetailsView 또는 FormView에 바인딩된 데이터를 기반으로 형식을 조정 하는 여러 가지 방법으로 수행할 수 있습니다. 이 자습서에서는 데이터 바인딩된 데이터 바인딩 및 RowDataBound 이벤트 처리기를 사용 하 여 서식 지정을 수행 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

GridView, DetailsView 및 FormView 컨트롤의 모양은 다양 한 스타일 관련 속성을 통해 사용자 지정할 수 있습니다. 등의 속성 `CssClass`, `Font`, `BorderWidth`, `BorderStyle`, `BorderColor`를 `Width`, 및 `Height`, 특히 일반 렌더링 된 컨트롤의 모양을 결정 합니다. 속성을 포함 하 여 `HeaderStyle`, `RowStyle`, `AlternatingRowStyle`, 스타일 설정과 특정 섹션에 적용할 수 있도록 다른 및 합니다. 마찬가지로, 다음 스타일 설정은 필드 수준에서 적용할 수 있습니다.

대부분의 시나리오에서 그러나 형식 지정 요구 사항에 따라 달라 표시 된 데이터의 값. 예를 들어 강조 하기 위해 단순하게 개 제품을 주식형, 제품 정보를 나열 하는 보고서 설정할 수 인 제품에 노란색 배경색 `UnitsInStock` 고 `UnitsOnOrder` 필드는 모두 0입니다. 비용이 많이 드는 products를 강조 하기 위해 굵은 글꼴로 둘 $75.00 비용 해당 제품의 가격을 표시 하려면 원하는 수 있습니다.

GridView, DetailsView 또는 FormView에 바인딩된 데이터를 기반으로 형식을 조정 하는 여러 가지 방법으로 수행할 수 있습니다. 데이터 바인딩된 사용 하 여 서식 지정을 수행 하는 방법을 살펴보겠습니다이 자습서는 `DataBound` 및 `RowDataBound` 이벤트 처리기입니다. 다음 자습서에서는 또 다른 방법은 살펴봅니다.

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a>DetailsView 컨트롤을 사용 하 여`DataBound`이벤트 처리기

때 데이터에 바인딩되어 DetailsView를 데이터 소스 컨트롤에서 또는 프로그래밍 방식으로 데이터를 컨트롤의 할당을 통해 `DataSource` 속성과 호출 해당 `DataBind()` 메서드에서 다음 일련의 단계를 수행 합니다.

1. 데이터 웹 컨트롤의 `DataBinding` 이벤트가 발생 합니다.
2. 데이터를 데이터 웹 컨트롤에 바인딩되어 있습니다.
3. 데이터 웹 컨트롤의 `DataBound` 이벤트가 발생 합니다.

1 단계와 3 단계는 이벤트 처리기를 통해 직후 사용자 지정 논리를 주입할 수 있습니다. 에 대 한 이벤트 처리기를 만들어는 `DataBound` 이벤트 데이터 웹 컨트롤에 바인딩되고 필요에 따라 형식을 조정 된 데이터 프로그래밍 방식으로 확인할 수 있습니다. 보겠습니다 보여 주기 위해 제품에 대 한 일반 정보를 표시 하지만 나타납니다 DetailsView 만듭니다는 `UnitPrice` 값을 ***굵게, 기울임꼴 글꼴*** $75.00 초과 하는 경우.

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a>1 단계:는 DetailsView에서 제품 정보 표시

열기는 `CustomColors.aspx` 페이지에서 `CustomFormatting` 폴더를 디자이너 도구 상자에서 DetailsView 컨트롤을 끌어, 설정 해당 `ID` 속성 값을 `ExpensiveProductsPriceInBoldItalic`를 호출 하는 새 ObjectDataSource 컨트롤을 바인딩할는 `ProductsBLL` 클래스의 `GetProducts()` 메서드. 이 작업을 수행 하는 것에 대 한 자세한 단계는 이전 자습서에서 자세히 검사 하는 이후 간단한 설명을 위해 여기 생략 됩니다.

ObjectDataSource DetailsView에 바인딩된 했습니다 되 면 잠시 필드 목록을 수정 합니다. 제거 하기로 했습니다 합니다 `ProductID`, `SupplierID`, `CategoryID`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`, 및 `Discontinued` BoundFields 이름을 변경 하 고 나머지 BoundFields 서식이 다시 지정 합니다. 도 삭제 합니다 `Width` 및 `Height` 설정 합니다. DetailsView 레코드가 하나만 표시 되므로 최종 사용자가 모든 제품을 볼 수 있도록 하기 위해 페이징 사용 하도록 설정 해야 합니다. 이렇게 하려면 DetailsView의 스마트 태그의 페이징 사용 확인란을 선택 합니다.


[![그림 1: 확인란을 사용 하도록 설정 페이징 DetailsView의 스마트 태그](custom-formatting-based-upon-data-vb/_static/image2.png)](custom-formatting-based-upon-data-vb/_static/image1.png)

**그림 1**: 그림 1: 확인란을 사용 하도록 설정 페이징 DetailsView의 스마트 태그 ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image3.png))


이러한 변경 내용은 다음 DetailsView 태그 수 있습니다.


[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample1.aspx)]

시간을 내어이 페이지를 브라우저에서 테스트 합니다.


[![DetailsView 컨트롤을 한 번에 한 제품 표시](custom-formatting-based-upon-data-vb/_static/image5.png)](custom-formatting-based-upon-data-vb/_static/image4.png)

**그림 2**: The DetailsView 컨트롤 표시 한 제품 번 ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image6.png))


## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>2 단계: 데이터 바인딩된 이벤트 처리기에서 데이터의 값을 프로그래밍 방식으로 결정

이러한 제품에 대해 굵게, 기울임꼴 글꼴의 가격을 표시 하기 위해 해당 `UnitPrice` 75.00 달러를 초과 하는 값을 프로그래밍 방식으로 결정을 해야는 `UnitPrice` 값입니다. DetailsView에 대 한이 수행할 수 있습니다는 `DataBound` 이벤트 처리기입니다. 이벤트를 만들면 처리기 디자이너에서 DetailsView 클릭 속성 창으로 이동 합니다. F4 키를 눌러를 불러오려면 없으면 표시할지 보기 메뉴로 이동 하 고 속성 창 메뉴 옵션을 선택 합니다. 속성 창에서 DetailsView의 이벤트를 나열 하려면 번개 모양 아이콘을 클릭 합니다. 다음으로 두 번 클릭 합니다 `DataBound` 이벤트 또는 이벤트 처리기를 만들려는 이름을 입력 합니다.


![DataBound 이벤트에 대 한 이벤트 처리기 만들기](custom-formatting-based-upon-data-vb/_static/image7.png)

**그림 3**: 만들기에 대 한 이벤트 처리기는 `DataBound` 이벤트


> [!NOTE]
> 또한 ASP.NET 페이지의 코드 부분에서 이벤트 처리기를 만들 수 있습니다. 페이지의 맨 위에 있는 두 개의 드롭다운 목록을 찾을 수 있습니다. 왼쪽된 드롭다운 목록에서 개체를 선택 하 고 오른쪽 드롭다운 목록에서 Visual Studio에 대 한 처리기를 만들려는 이벤트에서 자동으로 적절 한 이벤트 처리기를 만듭니다.


이렇게 자동으로 이벤트 처리기를 만들고 여기서 추가한 코드 부분을 이동 합니다. 이 시점에서 표시 됩니다.


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample2.vb)]

DetailsView로 바인딩된 데이터를 통해 액세스할 수 있습니다는 `DataItem` 속성입니다. 강력한 DataRow 인스턴스의 컬렉션으로 이루어진 강력한 형식화 된 DataTable에이 컨트롤을 바인딩하는 것을 기억 하십시오. 첫 번째 DataTable에서 DataRow는 DetailsView에 할당 된 DataTable DetailsView에 바인딩되면 `DataItem` 속성입니다. 특히 합니다 `DataItem` 속성에 할당 되는 `DataRowView` 개체입니다. 사용할 수 있습니다는 `DataRowView`의 `Row` 인 기본 DataRow 개체에 대 한 액세스를 가져올 속성을 보면 `ProductsRow` 인스턴스. 이 있으면 `ProductsRow` 인스턴스 단순히 개체의 속성 값을 검사 하 여이 결정을 내릴 수 있습니다.

다음 코드를 확인 하는 방법을 보여 줍니다 여부는 `UnitPrice` DetailsView 컨트롤에 바인딩된 값 $75.00 보다 큽니다.:


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample3.vb)]

> [!NOTE]
> 이후 `UnitPrice` 있을 수 있습니다를 `NULL` 값 데이터베이스에 먼저 확인을 사용 하 여 총비율 되지 있는지 확인을 `NULL` 값에 액세스 하기 전에 `ProductsRow`의 `UnitPrice` 속성. 이 검사는 중요 한 때문에 액세스 하려고 하는 경우는 `UnitPrice` 에 있을 때 속성을 `NULL` 값을 `ProductsRow` 개체를 throw 합니다를 [StrongTypingException 예외](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx).


## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a>3 단계: DetailsView UnitPrice 값 서식 지정

이 시점에서 확인할 수 있습니다 여부는 `UnitPrice` DetailsView에 바인딩된 값 $75.00를 초과 하는 값이 있지만 아직 DetailsView를 프로그래밍 방식으로 조정 하는 방법을 보려면의 서식 지정 적절 하 게 되었습니다. DetailsView에 있는 전체 행의 서식 지정을 수정 하려면 프로그래밍 방식으로 액세스를 사용 하 여 행 `DetailsViewID.Rows(index)`사용 하 여 액세스를 특정 셀을 수정 하려면 `DetailsViewID.Rows(index).Cells(index)`합니다. 행 또는 셀에 대 한 참조가 있으면 해당 스타일 관련 속성을 설정 하 여 모양을 다음 조정할 수 있습니다.

행을 프로그래밍 방식으로 액세스 0부터 시작 하는 행의 인덱스를 알고 있어야 합니다. 합니다 `UnitPrice` 행은 4의 인덱스를 지정 하 고 프로그래밍 방식으로 액세스할 수 있도록 DetailsView의 다섯 번째 행을 사용 하 여 `ExpensiveProductsPriceInBoldItalic.Rows(4)`입니다. 이 시점에서 다음 코드를 사용 하 여 굵게, 기울임꼴 글꼴에 표시 되는 전체 행의 콘텐츠가 있을 수 없습니다.


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample4.vb)]

그러나 그러면 *둘 다* 레이블 (Price) 및 굵게 및 기울임꼴 값입니다. 값만 굵게 및 기울임꼴 다음을 사용 하 여 수행할 수 있는 행의 두 번째 셀에 서식을 적용 하기 위해서 필요를 확인 하려면:


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample5.vb)]

지금 있으므로 자습서를 명확히 구분 된 렌더링 된 태그 및 스타일 관련 정보를 유지 하기 위해 스타일 시트를 사용 있어야, 있으므로 위와 같이 보겠습니다 대신 특정 스타일 속성을 설정 하는 대신 CSS 클래스를 사용 합니다. 엽니다는 `Styles.css` 스타일 시트 라는 새 CSS 클래스를 추가 하 고 `ExpensivePriceEmphasis` 다음 정의 사용 하 여:


[!code-css[Main](custom-formatting-based-upon-data-vb/samples/sample6.css)]

그런 다음 합니다 `DataBound` 셀의을 설정 하는 이벤트 처리기 `CssClass` 속성을 `ExpensivePriceEmphasis`입니다. 다음 코드에서는 `DataBound` 전체에서 이벤트 처리기:


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample7.vb)]

가격은 일반 글꼴로 표시 됩니다 Chai 75.00 달러 비용에서 볼 때 (그림 4 참조). 그러나 $97.00 가격이 있는 Mishi 산호세 Niku 보기 가격에에서 표시 됩니다 굵게, 기울임꼴 글꼴 (그림 5 참조).


[![$75.00 보다 적은 가격 보통 글꼴로 표시 됩니다.](custom-formatting-based-upon-data-vb/_static/image9.png)](custom-formatting-based-upon-data-vb/_static/image8.png)

**그림 4**: $75.00 보다 적은 가격 보통 글꼴로 표시 됩니다 ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image10.png))


[![비용이 많이 드는 제품의 가격은 기울임꼴 글꼴을 굵게 표시 됩니다.](custom-formatting-based-upon-data-vb/_static/image12.png)](custom-formatting-based-upon-data-vb/_static/image11.png)

**그림 5**: 비용이 많이 드는 제품의 가격은 기울임꼴 글꼴을 굵게 표시 됩니다 ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image13.png))


## <a name="using-the-formview-controlsdataboundevent-handler"></a>FormView 컨트롤을 사용 하 여`DataBound`이벤트 처리기

DetailsView 만들기에 대 한 FormView에 바인딩된 내부 데이터를 확인 하기 위한 단계는 동일 하 게는 `DataBound` 이벤트 처리기를 캐스팅 합니다 `DataItem` 속성을 적절 한 개체 형식 컨트롤에 바인딩되고 진행 하는 방법을 결정 합니다. 하지만 FormView 및 DetailsView 다 해당 사용자 인터페이스의 모양을 업데이트 되는 방식을에서.

FormView 모든 BoundFields 포함 하지 않으며 따라서 부족을 `Rows` 컬렉션입니다. 정적 HTML의 혼합을 포함할 수 있는 템플릿의 FormView가 구성 하는 대신 웹 컨트롤 및 데이터 바인딩 구문입니다. FormView의 스타일을 일반적으로 조정 FormView의 템플릿 내에서 웹 컨트롤의 하나 이상의 스타일을 조정 됩니다.

이 예에 표시 해 보겠습니다 목록 제품 FormView 보겠습니다 앞의 예에서 이번에서 같이 사용 하 여 제품 이름 및 단위 10 보다 작거나 경우 빨간색 글꼴로 표시 되는 재고 단위를 사용 하 여 재고.

## <a name="step-4-displaying-the-product-information-in-a-formview"></a>FormView에서 제품 정보를 표시 하는 4 단계:

FormView를 추가 합니다 `CustomColors.aspx` 집합과 DetailsView 아래 페이지 해당 `ID` 속성을 `LowStockedProductsInRed`입니다. FormView 이전 단계에서 만든 ObjectDataSource 컨트롤에 바인딩하십시오. 이렇게 하면 만들어집니다는 `ItemTemplate`, `EditItemTemplate`, 및 `InsertItemTemplate` FormView에 대 한 합니다. 제거는 `EditItemTemplate` 및 `InsertItemTemplate` 간소화 및 합니다 `ItemTemplate` 포함 하도록만 `ProductName` 및 `UnitsInStock` 자신의 적절 하 게 명명 된 레이블 컨트롤의 각 값입니다. 이전 예제에서 DetailsView와 마찬가지로 또한 FormView의 스마트 태그의 페이징 사용 확인란을 확인 합니다.

이러한 편집 후 FormView의 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample8.aspx)]

`ItemTemplate` 포함 되어 있습니다.

- **정적 HTML** 텍스트를 "제품:" 및 "재고 단위:"와 함께 합니다 `<br />` 및 `<b>` 요소입니다.
- **웹 컨트롤** 두 레이블 컨트롤 `ProductNameLabel` 고 `UnitsInStockLabel`입니다.
- **데이터 바인딩 구문을** 는 `<%# Bind("ProductName") %>` 하 고 `<%# Bind("UnitsInStock") %>` 레이블 컨트롤의 이러한 필드에서 값을 할당 하는 구문은 `Text` 속성입니다.

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>5 단계: 데이터 바인딩된 이벤트 처리기에서 데이터의 값을 프로그래밍 방식으로 결정

전체 FormView의 태그를 사용 하 여 프로그래밍 방식으로 확인 하는 경우 다음 단계는는 `UnitsInStock` 10 보다 작거나 같은 값이 있습니다. DetailsView를 사용 하 여 처럼 FormView와 정확히 동일한 방식으로 수행 됩니다. FormView의에 대 한 이벤트 처리기를 만들어 시작 `DataBound` 이벤트입니다.


![데이터 바인딩된 이벤트 처리기 만들기](custom-formatting-based-upon-data-vb/_static/image14.png)

**그림 6**: 만들기는 `DataBound` 이벤트 처리기


처리기 FormView의 캐스팅 하는 이벤트 `DataItem` 속성을를 `ProductsRow` 인스턴스를 확인 하는지 여부를 `UnitsInPrice` 값은 빨간색 글꼴로 표시할 필요는 합니다.


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample9.vb)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a>6 단계: FormView의 ItemTemplate의 UnitsInStockLabel 레이블 컨트롤 서식 지정

표시 서식을 지정 하는 최종 단계입니다 `UnitsInStock` 빨간색 글꼴로 값 10 이하의 값이 있습니다. 프로그래밍 방식으로 액세스 해야 하는 것이 `UnitsInStockLabel` 에서 제어할는 `ItemTemplate` 빨간색에서 텍스트 표시 되도록 스타일 속성을 설정 합니다. 템플릿에서 웹 컨트롤에 액세스 하려면 사용 된 `FindControl("controlID")` 다음과 같이 메서드:


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample10.vb)]

컨트롤 레이블 액세스 하려는 예제 `ID` 값은 `UnitsInStockLabel`이므로 사용 하면 됩니다.


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample11.vb)]

웹 컨트롤에 대 한 프로그래밍 방식으로 참조 한 후 필요에 따라 해당 스타일 관련 속성을 수정할 수 있습니다. CSS 클래스 이전 예에서 만들었습니다 처럼 `Styles.css` 라는 `LowUnitsInStockEmphasis`합니다. 이 스타일 레이블을 웹 컨트롤에 적용할 설정 해당 `CssClass` 속성 적절 하 게 합니다.


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample12.vb)]

> [!NOTE]
> 프로그래밍 방식으로 사용 하 여 웹 컨트롤에 액세스 하는 템플릿 서식 지정에 대 한 구문을 `FindControl("controlID")` 스타일 관련 속성을 다음 설정도 사용할 수 있습니다 사용 하는 경우 [TemplateFields](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) DetailsView 또는 GridView 컨트롤입니다. 다음 자습서에서 TemplateFields를 살펴보겠습니다.


제품을 볼 때 그림 7 FormView에 나와 있는 `UnitsInStock` 그림 8에 있는 제품에 해당 값이 10 보다 작은 값이 10 보다 큰 합니다.


[![제품으로는 충분히 큰 Units In Stock, 사용자 지정 서식 없이 적용 됩니다.](custom-formatting-based-upon-data-vb/_static/image16.png)](custom-formatting-based-upon-data-vb/_static/image15.png)

**그림 7**:에 대 한 제품으로는 충분히 큰 Units In Stock, 사용자 지정 서식 없이 적용 됩니다 ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image17.png))


[![재고 수 단위 값에 대 한 해당 제품으로 10 개 이하의의 빨간색으로 표시 됩니다.](custom-formatting-based-upon-data-vb/_static/image19.png)](custom-formatting-based-upon-data-vb/_static/image18.png)

**그림 8**: 재고 수의 장치는 해당 제품으로의 값이 10 개 이하의 빨간색으로 표시 됩니다 ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image20.png))


## <a name="formatting-with-the-gridviewsrowdataboundevent"></a>Gridview의 서식 지정`RowDataBound`이벤트

이전 DetailsView 단계의 시퀀스를 살펴보았습니다 및 FormView 데이터 바인딩 중 진행을 제어 합니다. 살펴보겠습니다 다음이 단계를 통해 다시 한 번으로 쉽게 찾아볼.

1. 데이터 웹 컨트롤의 `DataBinding` 이벤트가 발생 합니다.
2. 데이터를 데이터 웹 컨트롤에 바인딩되어 있습니다.
3. 데이터 웹 컨트롤의 `DataBound` 이벤트가 발생 합니다.

이러한 세 가지 간단한 단계는 단일 레코드를 표시 하므로 FormView 및 DetailsView를 충분히 있습니다. 표시 하는 gridview *모든* 바인딩된 레코드 2 단계를 좀 더 복잡 하지만 (첫 번째 뿐 아니라 함).

GridView 열거 데이터 원본을 만들고, 각 레코드에 대해 2 단계에서 한 `GridViewRow` 인스턴스 및 현재 레코드를 바인딩합니다. 각 `GridViewRow` GridView에 추가 두 이벤트가 발생 합니다.

- **`RowCreated`** 후 발생 합니다 `GridViewRow` 만들었습니다
- **`RowDataBound`** 현재 레코드에 바인딩된 후에 발생 합니다 `GridViewRow`합니다.

GridView에 대 한 다음, 데이터 바인딩 보다 정확 하 게에서 설명한 단계의 다음 시퀀스:

1. GridView의 `DataBinding` 이벤트가 발생 합니다.
2. 데이터를 GridView에 바인딩됩니다.   
  
   데이터 소스의 각 레코드에 대 한 

    1. 만들기는 `GridViewRow` 개체
    2. 실행 된 `RowCreated` 이벤트
    3. 레코드를 바인딩하는 `GridViewRow`
    4. 실행 된 `RowDataBound` 이벤트
    5. 추가 된 `GridViewRow` 에 `Rows` 컬렉션
3. GridView의 `DataBound` 이벤트가 발생 합니다.

GridView의 개별 레코드 형식의 사용자 지정 하려면 다음을 생성 해야에 대 한 이벤트 처리기는 `RowDataBound` 이벤트입니다. 이 예에 GridView를 추가 해 보겠습니다는 `CustomColors.aspx` 이름, 범주 및 가격이 미만 $10.00 노란색 배경 색을 사용 하 여 해당 제품을 강조 표시 하는 각 제품에 대 한 가격을 나열 하는 페이지입니다.

## <a name="step-7-displaying-product-information-in-a-gridview"></a>GridView의 제품 정보를 표시 하는 7 단계:

이전 예제에서 GridView FormView 아래에 추가 하 고 설정 해당 `ID` 속성을 `HighlightCheapProducts`입니다. 페이지의 모든 제품을 반환 하는 ObjectDataSource에 이미 있으므로 GridView를 바인딩하십시오. GridView의 BoundFields 방금: 제품 이름, 범주 및 가격을 포함 하도록 마지막으로 편집 합니다. 이러한 편집 후 GridView의 태그 같이 표시 됩니다.


[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample13.aspx)]

그림 9에서는 브라우저를 통해 볼 때이 여태 까지의 진행 상황을 보여 줍니다.


[![이름, 범주 및 각 제품에 대 한 가격을 나열 하는 GridView](custom-formatting-based-upon-data-vb/_static/image22.png)](custom-formatting-based-upon-data-vb/_static/image21.png)

**그림 9**: 이름, 범주 및 각 제품에 대 한 가격을 나열 하는 GridView ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image23.png))


## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a>8 단계: RowDataBound 이벤트 처리기에서 데이터의 값을 프로그래밍 방식으로 결정

경우는 `ProductsDataTable` GridView에 바인딩됩니다 해당 `ProductsRow` 열거 되 고 각 인스턴스가 `ProductsRow` 는 `GridViewRow` 만들어집니다. 합니다 `GridViewRow`의 `DataItem` 속성은 특정에 할당 `ProductRow`는 GridView의 `RowDataBound` 이벤트 처리기는 발생 합니다. 확인 하는 `UnitPrice` GridView에 바인딩된 각 제품에 대 한 값이 다음 GridView의에 대 한 이벤트 처리기를 생성 해야 `RowDataBound` 이벤트입니다. 이 이벤트 처리기에서 검사할 수 있습니다 합니다 `UnitPrice` 현재 값 `GridViewRow` 해당 행에 대 한 서식 지정 의사 결정을 확인 합니다.

FormView 및 DetailsView와 같은 일련의 단계를 사용 하 여이 이벤트 처리기를 만들 수 있습니다.


![GridView의 RowDataBound 이벤트에 대 한 이벤트 처리기 만들기](custom-formatting-based-upon-data-vb/_static/image24.png)

**그림 10**: GridView의에 대 한 이벤트 처리기를 만들고 `RowDataBound` 이벤트


이 방식으로 이벤트 처리기를 만드는 다음 코드를 ASP.NET 페이지의 코드 부분을 자동으로 추가 하면:


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample14.vb)]

경우는 `RowDataBound` 이벤트가 발생 이벤트 처리기 매개 변수로 전달 되는 두 번째 형식의 개체 `GridViewRowEventArgs`에 라는 속성이 있는 `Row`합니다. 이 속성에 대 한 참조를 반환 합니다.는 `GridViewRow` 바인딩된 데이터 뿐 이었습니다. 액세스 하는 `ProductsRow` 에 바인딩된 인스턴스를 `GridViewRow` 사용 하 여는 `DataItem` 같이 속성:


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample15.vb)]

작업할 때 합니다 `RowDataBound` GridView 행의 다른 형식으로 구성 된 및 마다이 이벤트가 발생 하는 점에 유의 해야 하는 이벤트 처리기 *모든* 행 형식입니다. A `GridViewRow`의 형식을 확인 하 여 해당 `RowType` 속성에 가능한 값 중 하나일 수 있습니다:

- `DataRow` GridView의에서 레코드에 바인딩되는 행 `DataSource`
- `EmptyDataRow` 경우에 표시 되는 행 GridView의 `DataSource` 비어
- `Footer` 바닥글 행입니다. 경우에 표시 된 GridView의 `ShowFooter` 속성 `True`
- `Header` 머리글 행입니다. GridView의 ShowHeader 속성이로 설정 되어 있으면 표시 `True` (기본값)
- `Pager` GridView의에 대 한 구현 하는 페이징, 페이징 인터페이스를 표시 하는 행
- `Separator` GridView에 대 한 사용 되지 않고 사용한는 `RowType` DataList 및 반복기에 대 한 속성 컨트롤을 두 개의 데이터 웹 컨트롤 하겠습니다 나중에 자습서

하므로 합니다 `EmptyDataRow`, `Header`, `Footer`, 및 `Pager` 행 연관 되지 않습니다는 `DataSource` 레코드를 항상 갖습니다 값 `Nothing` 에 대 한 해당 `DataItem` 속성. 현재 사용 하기 전에 이러한 이유로 `GridViewRow`의 `DataItem` 속성인 것 먼저 확인 해야 사용 하 여 총비율을 `DataRow`입니다. 이 확인 하 여 수행할 수 있습니다 합니다 `GridViewRow`의 `RowType` 같이 속성:


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample16.vb)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a>9 단계: $10.00 미만 행 노란색 When the UnitPrice 값을 강조 표시

프로그래밍 방식으로 전체 강조 표시 하는 마지막 단계입니다 `GridViewRow` 경우는 `UnitPrice` 행이 $10.00 보다 작은 값입니다. GridView의 행 또는 셀에 액세스 하기 위한 구문은와 동일 하 게 DetailsView `GridViewID.Rows(index)` 전체 행에 액세스 하려면 `GridViewID.Rows(index).Cells(index)` 특정 셀에 액세스 해야 합니다. 그러나 경우 합니다 `RowDataBound` 이벤트 처리기 실행 데이터 바인딩된 `GridViewRow` GridView의 추가할 아직 `Rows` 컬렉션입니다. 따라서 현재 액세스할 수 없습니다 `GridViewRow` 에서 인스턴스는 `RowDataBound` 행 컬렉션을 사용 하 여 이벤트 처리기입니다.

대신 `GridViewID.Rows(index)`, 현재 참조할 수 있습니다 `GridViewRow` 의 인스턴스를 `RowDataBound` 이벤트 처리기를 사용 하 여 `e.Row`입니다. 즉, 하려면 현재 강조 표시 `GridViewRow` 에서 인스턴스를 `RowDataBound` 이벤트 처리기를 사용 하면 됩니다.


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample17.vb)]

설정 하지 않고 합니다 `GridViewRow`의 `BackColor` 속성을 직접 CSS 클래스를 사용 하 여 집중 하겠습니다. 명명 된 CSS 클래스를 만들었습니다 `AffordablePriceEmphasis` 노란색으로 배경색을 설정 하는입니다. 완료 된 `RowDataBound` 이벤트 처리기를 따릅니다.


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample18.vb)]


[![가장 저렴 한 제품 노란색 강조 표시 됩니다.](custom-formatting-based-upon-data-vb/_static/image26.png)](custom-formatting-based-upon-data-vb/_static/image25.png)

**그림 11**: 가장 많이 저렴 한 제품 노란색 강조 표시 됩니다 ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image27.png))


## <a name="summary"></a>요약

이 자습서에서 GridView, DetailsView 및 FormView 컨트롤에 바인딩된 데이터를 기반으로 형식을 지정 하는 방법에 살펴보았습니다. 이벤트 처리기에 대 한 만든이 수행 하는 `DataBound` 또는 `RowDataBound` 이벤트, 필요한 경우 서식 변경 함께 내부 데이터 검사 되었습니다. DetailsView 또는 FormView에 바인딩된 데이터에 액세스 하려면 사용 하 여는 `DataItem` 속성에는 `DataBound` 이벤트 처리기를 GridView에 대 한 각 `GridViewRow` 인스턴스의 `DataItem` 는에서사용할수있는해당행에바인딩된데이터를포함하는속성`RowDataBound` 이벤트 처리기입니다.

프로그래밍 방식으로 데이터 웹 컨트롤의 서식 지정을 조정 하는 구문은 웹 컨트롤 및 서식을 지정할 데이터 표시 방법을 따라 달라 집니다. GridView 및 DetailsView 컨트롤, 행 및 셀 서 수 인덱스에 의해 액세스할 수 있습니다. 서식 파일을 사용 하는 FormView에 대 한는 `FindControl("controlID")` 메서드는 일반적으로 템플릿 내에서 웹 컨트롤을 찾는 데 사용 됩니다.

다음 자습서에서 GridView 및 DetailsView를 사용 하 여 템플릿을 사용 하는 방법을 살펴보겠습니다. 또한 기본 데이터를 기반으로 서식을 사용자 지정 하기 위한 다른 기법을 살펴보겠습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 E.R. 되었습니다. Gilmore, Dennis Patterson 및 Dan Jagers 합니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](displaying-summary-information-in-the-gridview-s-footer-cs.md)
> [다음](using-templatefields-in-the-gridview-control-vb.md)
