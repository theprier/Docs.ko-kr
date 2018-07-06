---
uid: web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
title: GridView의 바닥글 (C#)에 요약 정보 표시 | Microsoft Docs
author: rick-anderson
description: 요약 정보를 요약 행 내에서 보고서의 맨 아래에 종종 표시 됩니다. GridView 컨트롤 pr 수 인 셀에 바닥글 행을 포함할 수 있습니다...
ms.author: aspnetcontent
ms.date: 03/31/2010
ms.assetid: d50edc31-9286-4c6a-8635-be09e72752a4
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
msc.type: authoredcontent
ms.openlocfilehash: 34d5dbf4a019f798714f80964789cd85a466b43e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818811"
---
<a name="displaying-summary-information-in-the-gridviews-footer-c"></a>GridView의 바닥글 (C#)에서 요약 정보를 표시합니다.
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_15_CS.exe) 또는 [PDF 다운로드](displaying-summary-information-in-the-gridview-s-footer-cs/_static/datatutorial15cs1.pdf)

> 요약 정보를 요약 행 내에서 보고서의 맨 아래에 종종 표시 됩니다. GridView 컨트롤에는 해당 셀에 프로그래밍 방식으로 집계 데이터를 삽입 수 바닥글 행을 포함할 수 있습니다. 이 자습서에서는이 바닥글 행에 집계 데이터를 표시 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

순서 및 재주문 수준에서 각 제품의 가격, 재고 단위를 표시 하는 것 외에도 사용자 수 또한 평균 가격, 재고 단위의 총 수와 같은 집계 정보에 관심이 있을 수 등에입니다. 이러한 요약 정보를 요약 행 내에서 보고서의 맨 아래에 종종 표시 됩니다. GridView 컨트롤에는 해당 셀에 프로그래밍 방식으로 집계 데이터를 삽입 수 바닥글 행을 포함할 수 있습니다.

이 작업에서는 세 가지 과제:

1. GridView의 바닥글 행을 표시 하려면 구성
2. 요약 데이터를 결정합니다. 즉, 방법에서는 계산 수행 평균 가격 또는 총 재고 단위?
3. 바닥글 행의 적절 한 셀에 요약 데이터 삽입

이 자습서에서는 이러한 문제를 해결 하는 방법을 살펴보겠습니다. 특히 GridView에 표시 되는 선택한 범주의 제품을 사용 하 여 드롭다운 목록에서 범주를 나열 하는 페이지를 만들겠습니다. GridView 재고 및 주문 해당 범주의 제품에 대 한 평균 가격과 단위의 총 수를 보여 주는 바닥글 행이 포함 됩니다.


[![GridView의 바닥글 행에 요약 정보가 표시 됩니다.](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image2.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image1.png)

**그림 1**: GridView의 바닥글 행에 요약 정보가 표시 됩니다 ([큰 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image3.png))


이전에 적용 된 개념을 기반으로 제품 마스터/세부 인터페이스에 해당 범주를 사용 하 여이 자습서에서는 [마스터/세부 정보 필터링으로 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) 자습서입니다. 이전 자습서를 통해 아직 했었다면, 그렇게 해 주세요이 계속 진행 하기 전에 합니다.

## <a name="step-1-adding-the-categories-dropdownlist-and-products-gridview"></a>1 단계: 추가 제품 GridView 고 범주 DropDownList

직접를 관련 된 GridView의 바닥글에 요약 정보를 추가, 전에 먼저 간단히 만들어 보겠습니다 마스터/세부 정보 보고서. 이 첫 번째 단계를 완료 한 후 요약 데이터를 포함 하는 방법을 살펴보겠습니다.

열어서 시작 합니다 `SummaryDataInFooter.aspx` 페이지에 `CustomFormatting` 폴더입니다. DropDownList 컨트롤을 추가 하 고 설정 해당 `ID` 에 `Categories`입니다. 다음으로, DropDownList의 스마트 태그의 데이터 소스 선택 링크를 클릭 하 고 라는 새 ObjectDataSource를 추가 하도록 선택할 `CategoriesDataSource` 를 호출 하는 `CategoriesBLL` 클래스의 `GetCategories()` 메서드.


[![CategoriesDataSource 라는 새 ObjectDataSource를 추가 합니다.](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image5.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image4.png)

**그림 2**: 새 ObjectDataSource 라는 추가 `CategoriesDataSource` ([클릭 하 여 큰 이미지 보기](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image6.png))


[![CategoriesBLL 클래스의 GetCategories() 메서드를 호출 하는 ObjectDataSource가](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image8.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image7.png)

**그림 3**: 호출 하는 ObjectDataSource가 합니다 `CategoriesBLL` 클래스의 `GetCategories()` 메서드 ([클릭 하 여 큰 이미지 보기](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image9.png))


ObjectDataSource를 구성한 후 마법사 반환 DropDownList의 데이터 소스 구성 마법사는 데이터 필드 값을 지정 해야 표시 하는 하나는 값에 해당 하의 DropDownList의 `ListItem` s입니다. 있어야 합니다 `CategoryName` 필드를 표시 하 고 사용 하 여는 `CategoryID` 값으로.


[![텍스트 및 ListItems에 대 한 값으로 CategoryName 및 CategoryID 필드를 각각 사용](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image11.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image10.png)

**그림 4**: 사용 하 여는 `CategoryName` 및 `CategoryID` 로 필드를 `Text` 및 `Value` 에 대 한 합니다 `ListItem` s, 각각 ([큰 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image12.png))


DropDownList 했으므로 시점에서 (`Categories`) 시스템의 범주를 나열 하는 합니다. 이제 선택한 범주에 속하는 해당 제품을 나열 하는 GridView를 추가 해야 합니다. 그러나 수행 하기 전에 잠시 DropDownList의 스마트 태그에 AutoPostBack 사용 확인란 합니다. 에 설명 된 대로 합니다 *마스터/세부 정보 필터링으로 DropDownList* DropDownList의을 설정 하 여 자습서 `AutoPostBack` 속성을 `true` 페이지 게시 될 다시 DropDownList 값이 변경 될 때마다 합니다. 이렇게 하면 새로 고쳐져 야 GridView 새로 선택한 범주에 대 한 해당 제품을 표시 합니다. 경우는 `AutoPostBack` 속성이 `false` (기본값), 변경 범주 포스트백을 발생 하지 않습니다 하 고 따라서 나열된 된 제품 업데이트 되지 않습니다.


[![확인란을 사용 하도록 설정 AutoPostBack DropDownList의 스마트 태그](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image14.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image13.png)

**그림 5**: 확인란을 사용 하도록 설정 AutoPostBack DropDownList의 스마트 태그 ([큰 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image15.png))


선택한 범주에 대 한 제품을 전시 하기 위해 페이지에 GridView 컨트롤을 추가 합니다. GridView의 설정 `ID` 하 `ProductsInCategory` 라는 새 ObjectDataSource를 바인딩할 `ProductsInCategoryDataSource`합니다.


[![ProductsInCategoryDataSource 라는 새 ObjectDataSource를 추가 합니다.](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image17.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image16.png)

**그림 6**: 새 ObjectDataSource 라는 추가 `ProductsInCategoryDataSource` ([클릭 하 여 큰 이미지 보기](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image18.png))


호출 되도록 ObjectDataSource를 구성 합니다 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드.


[![GetProductsByCategoryID(categoryID) 메서드를 호출 하는 ObjectDataSource가](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image20.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image19.png)

**그림 7**: ObjectDataSource 호출 있어야 합니다 `GetProductsByCategoryID(categoryID)` 메서드 ([클릭 하 여 큰 이미지 보기](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image21.png))


이후를 `GetProductsByCategoryID(categoryID)` 메서드는 입력된 매개 변수에서는 마법사의 마지막 단계에서 매개 변수 값의 원본을 지정할 수 있습니다. 선택한 범주에서 제품을 표시 하기 위해 있는에서 가져온 매개 변수는 `Categories` DropDownList 합니다.


[![선택한 범주 드롭다운 목록에서 categoryID 매개 변수 값 가져오기](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image23.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image22.png)

**그림 8**: 가져오기 합니다 *`categoryID`* 선택한 범주 드롭다운 목록에서 매개 변수 값 ([클릭 하 여 큰 이미지 보기](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image24.png))


마법사를 완료 한 후 각 제품 속성에 대해는 BoundField GridView에 게 해야 합니다. 보겠습니다 되도록 이러한 BoundFields 정리 합니다 `ProductName`, `UnitPrice`를 `UnitsInStock`, 및 `UnitsOnOrder` BoundFields 표시 됩니다. 나머지 BoundFields에 모든 필드 수준 설정을 추가 하려면 자유롭게 (형식 지정과 같은 `UnitPrice` 통화로). 다음과 같이 변경한 후 GridView의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample1.aspx)]

이 시점에서 주문 선택한 범주에 속하는 해당 제품에 대 한 이름, 단가, 재고 단위 및 단위를 보여 주는 마스터/세부 정보 보고서를 완벽 하 게 작동 했습니다.


[![선택한 범주 드롭다운 목록에서 categoryID 매개 변수 값 가져오기](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image26.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image25.png)

**그림 9**: 가져오기 합니다 *`categoryID`* 선택한 범주 드롭다운 목록에서 매개 변수 값 ([클릭 하 여 큰 이미지 보기](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image27.png))


## <a name="step-2-displaying-a-footer-in-the-gridview"></a>2 단계: GridView의 바닥글 표시

GridView 컨트롤을 머리글 및 바닥글 행을 표시할 수 있습니다. 이러한 행의 값에 따라 표시 되는 `ShowHeader` 하 고 `ShowFooter` 속성을 각각 `ShowHeader` 기본값으로 `true` 및 `ShowFooter` 에 `false`. 단순히 GridView의 바닥글을 포함 하려면 해당 `ShowFooter` 속성을 `true`입니다.


[![GridView의 ShowFooter 속성도 true로 설정](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image29.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image28.png)

**그림 10**: GridView의 설정 `ShowFooter` 속성을 `true` ([클릭 하 여 큰 이미지 보기](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image30.png))


바닥글 행 GridView;에 정의 된 필드의 각 셀에 그러나 이러한 셀은 기본적으로 비어 있습니다. 시간을 내어 브라우저에서 진행 상황을 보고 합니다. 사용 하 여 합니다 `ShowFooter` 속성으로 `true`를 GridView에는 빈 바닥글 행이 포함 됩니다.


[![GridView 이제 바닥글 행이 포함 됩니다.](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image32.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image31.png)

**그림 11**: GridView 이제 바닥글 행이 포함 됩니다 ([큰 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image33.png))


그림 11에 있는 바닥글 행 하지 눈에 띄는 흰색 배경을 있습니다. 만들어 보겠습니다를 `FooterStyle` CSS 클래스의 `Styles.css` 진한 빨간색 배경이 지정 하 고 다음을 구성 하는 합니다 `GridView.skin` 스킨 파일에는 `DataWebControls` 테마 GridView의에이 CSS 클래스를 할당할 `FooterStyle`의 `CssClass` 속성. 스킨 및 테마에 필요한 경우 다시 참조를 [the ObjectDataSource 사용 하 여 데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) 자습서입니다.

다음 CSS 클래스를 추가 하 여 시작 `Styles.css`:


[!code-css[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample2.css)]

합니다 `FooterStyle` CSS 클래스 스타일로 비슷합니다는 `HeaderStyle` 클래스를 `HeaderStyle`의 배경색 음영이 짙을 수록 미묘한 이며 해당 텍스트가 굵은 글꼴로 표시 됩니다. 또한 바닥글에 텍스트를 오른쪽 맞춤 되 반면 헤더의 텍스트는 가운데에 맞춥니다.

다음으로 열고 모든 GridView의 바닥글을 사용 하 여이 CSS 클래스를 연결할를 `GridView.skin` 파일을 `DataWebControls` 테마 설정 하 고는 `FooterStyle`의 `CssClass` 속성. 이 추가 후 파일의 태그 같이 표시 됩니다.


[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample3.aspx)]

이 변경은 아래 스크린샷, 바닥글을 통해 더 명확 하 게 돋보이게 합니다.


[![GridView의 바닥글 행에는 이제 빨강 배경색에](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image35.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image34.png)

**그림 12**: GridView의 바닥글 행에는 이제 빨강 배경색에 ([큰 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image36.png))


## <a name="step-3-computing-the-summary-data"></a>3 단계: 컴퓨팅의 요약 데이터

GridView의 바닥글 표시를 사용 하 여 다음 미국의 당면 과제를 사용 하면 요약 데이터를 계산할 방법이 있습니다. 두 가지 방법으로이 정보를 집계를 계산 합니다.

1. SQL 쿼리를 통해 특정 범주에 대 한 요약 데이터를 계산 하려면 데이터베이스에는 추가 쿼리를 실행 수 없습니다. SQL과 함께 집계 함수의 수를 포함 한 `GROUP BY` 데이터를 요약 해야는 데이터를 지정 하는 절. 필요한 정보를 다음 SQL 쿼리를 다시 표시 됩니다.  

    [!code-sql[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample4.sql)]

    물론에서 직접이 쿼리를 실행 하 려 합니다 `SummaryDataInFooter.aspx` 아니라 메서드를 만들어 페이지를 `ProductsTableAdapter` 및 `ProductsBLL`합니다.
2. 에 설명 된 대로 GridView에 추가 되는이 정보를 계산 [데이터를 기반으로 사용자 지정 서식 지정](custom-formatting-based-upon-data-cs.md) 자습서를 GridView의 `RowDataBound` 후 GridView에 추가 되 고 각 행에 대해 한 번 실행 되는 이벤트 처리기는 되었습니다 데이터 바인딩입니다. 이 이벤트에 대 한 이벤트 처리기를 만들어 실행 하는 유지할 수 있습니다 하고자 하는 값의 총 집계 합니다. 마지막 데이터 행은 합계 및 평균을 계산 하는 데 필요한 정보를 GridView에 바인딩 되었습니다.

두 번째 방법은 여정 데이터베이스 및 데이터 액세스 계층 및 비즈니스 논리 계층에서 요약 기능을 구현 하는 데 필요한 노력을 절약할 수 있지만 어느 방법이 든 스캔이 일반적으로 사용 했습니다. 이 자습서에 대 한 보겠습니다 두 번째 옵션을 사용 및 사용 하 여 누계 기록해는 `RowDataBound` 이벤트 처리기입니다.

만들기는 `RowDataBound` 를 선택 하 GridView 디자이너에서 속성 창에서 번개 모양 아이콘을 클릭 하 고 두 번 클릭 하면 GridView에 대 한 이벤트 처리기는 `RowDataBound` 이벤트입니다. 라는 새 이벤트 처리기를 만들어집니다 `ProductsInCategory_RowDataBound` 에 `SummaryDataInFooter.aspx` 페이지의 코드 숨김 클래스입니다.


[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample5.cs)]

누적 합계를 유지 하기 위해 이벤트 처리기의 범위 외부에서 변수를 정의 해야 합니다. 다음 4 개의 페이지 수준 변수를 만듭니다.

- `_totalUnitPrice`를 형식 `decimal`
- `_totalNonNullUnitPriceCount`를 형식 `int`
- `_totalUnitsInStock`를 형식 `int`
- `_totalUnitsOnOrder`를 형식 `int`

그런 다음에서 발생 한 각 데이터 행에 대 한 이러한 세 변수를 증가 시키는 코드를 작성 합니다 `RowDataBound` 이벤트 처리기입니다.


[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample6.cs)]

`RowDataBound` 이벤트 처리기는 DataRow를 사용 하 여 처리 함으로써 시작 합니다. 설정 된 되 면 합니다 `Northwind.ProductsRow` 방금에 바인딩된 인스턴스를 `GridViewRow` 개체 `e.Row` 변수에 저장 됩니다 `product`합니다. 다음으로, 실행 중인 총 변수는 현재 제품의 해당 값 만큼 증분됩니다 (데이터베이스를 포함 하지 않는다는 가정 `NULL` 값). 모두 실행 한 추적 했습니다 `UnitPrice` 이외 수와 총`NULL` `UnitPrice` 평균 가격에는 이러한 두 값의 몫입니다 때문에 기록 합니다.

## <a name="step-4-displaying-the-summary-data-in-the-footer"></a>바닥글에 요약 데이터를 표시 하는 4 단계:

합계의 요약 데이터를 사용 하 여 마지막 단계 GridView의 바닥글 행에 표시 됩니다. 이 작업을 수행할 수 있습니다 통해 프로그래밍 방식으로 `RowDataBound` 이벤트 처리기입니다. 이전에 설명한 대로 합니다 `RowDataBound` 이벤트 처리기에 대 한 발생 *모든* 바닥글 행을 포함 하 여 GridView에 바인딩되는 행입니다. 따라서 다음 코드를 사용 하 여 바닥글 행에 데이터를 표시 하는 이벤트 처리기를 살펴보면서 수 있습니다.


[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample7.cs)]

모든 데이터 행을 추가한 후 GridView에 바닥글 행이 추가 되므로 시간 준비가 되었다고 누계 계산을 완료 합니다 바닥글에 요약 데이터를 표시할 확신할 수 있습니다. 마지막 단계는 다음의 바닥글 셀에서 이러한 값을 설정 방법은입니다.

사용 하 여 특정 바닥글 셀에 텍스트를 표시 하려면 `e.Row.Cells[index].Text = value`여기서는 `Cells` 인덱싱 0부터 시작 합니다. 다음 코드 (제품의 수로 나눈 총 가격)의 평균 가격을 계산 주식형 및 GridView의 바닥글 적절 한 셀에는 순서에 대 한 단위에서 총 단위 수와 함께 표시 합니다.


[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample8.cs)]

그림 13이이 코드를 추가한 다음 보고서를 보여 줍니다. 참고 하는 방법을 `ToString("c")` 하면 평균 가격 요약 정보가 통화 형식으로 지정 되어야 합니다.


[![GridView의 바닥글 행에는 이제 빨강 배경색에](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image38.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image37.png)

**그림 13**: GridView의 바닥글 행에는 이제 빨강 배경색에 ([큰 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image39.png))


## <a name="summary"></a>요약

일반 보고서 요구 사항이 요약 데이터를 표시 및 GridView 컨트롤을 사용 하면 해당 바닥글 행에서 이러한 정보를 포함 하는 일을 쉽게 합니다. 바닥글 행이 표시 됩니다 때 GridView의 `ShowFooter` 속성이 `true` 텍스트를 통해 프로그래밍 방식으로 설정 하는 해당 셀에 있을 수 있습니다는 `RowDataBound` 이벤트 처리기입니다. 요약 데이터를 계산 하거나 수행할 수 있습니다는 데이터베이스를 다시 쿼리하여 또는 ASP.NET 페이지의 코드 숨김 클래스에서 코드를 사용 하 여 프로그래밍 방식으로 요약 데이터를 계산 하 여.

이 자습서는 검사 GridView, DetailsView 및 FormView 컨트롤을 사용 하 여 사용자 지정 서식 지정을 완료 했습니다. 다음 자습서를 삽입, 업데이트 및 이러한 동일한 컨트롤을 사용 하 여 데이터를 삭제 한 탐색을 시작 합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](using-the-formview-s-templates-cs.md)
> [다음](custom-formatting-based-upon-data-vb.md)
