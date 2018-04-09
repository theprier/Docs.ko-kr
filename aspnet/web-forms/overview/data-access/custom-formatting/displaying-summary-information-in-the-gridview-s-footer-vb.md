---
uid: web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb
title: GridView의 바닥글 (VB)의 요약 정보를 표시 합니다. | Microsoft Docs
author: rick-anderson
description: 요약 정보는 종종 요약 행에 대 한 보고서의 맨 아래에 표시 됩니다. GridView 컨트롤에 해당 셀을 활용해 서 pr 바닥글 행을 포함할 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 41c818b7-603a-402b-8847-890a63547b6f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb
msc.type: authoredcontent
ms.openlocfilehash: d9a1a3f3c680f367395f984254da6cdcdd3c08d4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="displaying-summary-information-in-the-gridviews-footer-vb"></a>GridView의 바닥글 (VB)의 요약 정보를 표시합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_15_VB.exe) 또는 [PDF 다운로드](displaying-summary-information-in-the-gridview-s-footer-vb/_static/datatutorial15vb1.pdf)

> 요약 정보는 종종 요약 행에 대 한 보고서의 맨 아래에 표시 됩니다. GridView 컨트롤 해당 셀에 프로그래밍 방식으로 집계 데이터를 삽입 수 바닥글 행을 포함할 수 있습니다. 이 자습서에서는이 바닥글 행에 집계 데이터를 표시 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

순서 및 재주문 수준에 각 제품의 가격, 재고, 단위를 표시, 외에도 사용자 수 또한 평균 가격, 재고, 단위의 총 수 등의 집계 정보에 관심이 있을 수 등에입니다. 이러한 요약 정보는 종종 요약 행에 대 한 보고서의 맨 아래에 표시 됩니다. GridView 컨트롤 해당 셀에 프로그래밍 방식으로 집계 데이터를 삽입 수 바닥글 행을 포함할 수 있습니다.

이 작업에서는 세 가지 문제가 있었습니다.

1. GridView의 바닥글 행을 표시 하려면 구성
2. 요약 데이터를 결정합니다. 즉, 어떻게에서는 계산 수행의 평균 가격 또는 총 재고 수량이?
3. 바닥글 행의 적절 한 셀에 요약 데이터를 삽입합니다.

이 자습서에서는 이러한 문제를 해결 하는 방법을 살펴보겠습니다. 특히, 드롭 다운 목록에서 범주는 GridView에 표시 되는 선택한 범주의 제품으로 나열 된 페이지를 만들겠습니다. GridView 재고 및 주문 해당 범주에는 제품에 대 한 평균 가격 및 총 단위 수를 보여 주는 바닥글 행이 포함 됩니다.


[![GridView의 바닥글 행에 요약 정보가 표시 됩니다.](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image2.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image1.png)

**그림 1**: GridView의 바닥글 행에 요약 정보가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image3.png))


이전에 적용 된 개념을 바탕으로 제품 마스터/세부 인터페이스에 해당 범주와이 자습서에서는 [마스터/세부 정보 필터링 된 정도 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) 자습서입니다. 이전 자습서를 통해 아직 보았다면이 이와 계속 진행 하기 전에 않은 하십시오.

## <a name="step-1-adding-the-categories-dropdownlist-and-products-gridview"></a>1 단계: DropDownList 범주 및 제품 GridView를 추가합니다.

직접와 관련 된 GridView의 바닥글에 요약 정보를 추가, 하기 전에 먼저 단순히을 제작 해 보겠습니다 마스터/세부 정보 보고서입니다. 이 첫 번째 단계를 완료 한 것 되 면 요약 데이터를 포함 하는 방법을 살펴보겠습니다.

열어 시작는 `SummaryDataInFooter.aspx` 페이지에 `CustomFormatting` 폴더입니다. 예를 추가 하 고 설정의 `ID` 를 `Categories`합니다. 다음으로 DropDownList의 스마트 태그에서 데이터 소스 선택 링크를 클릭 하 고 명명 된 새 ObjectDataSource 추가 하기로 `CategoriesDataSource` 를 호출 하 여 `CategoriesBLL` 클래스의 `GetCategories()` 메서드.


[![CategoriesDataSource 라는 새 ObjectDataSource를 추가 합니다.](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image5.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image4.png)

**그림 2**: 새 ObjectDataSource 라는 추가 `CategoriesDataSource` ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image6.png))


[![CategoriesBLL 클래스 GetCategories() 메서드를 호출 ObjectDataSource 있어야 합니다.](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image8.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image7.png)

**그림 3**: ObjectDataSource 호출가 `CategoriesBLL` 클래스의 `GetCategories()` 메서드 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image9.png))


ObjectDataSource를 구성 했으면 마법사 DropDownList의 데이터 소스 구성 있는 어떤 데이터 필드 값을 지정 해야 하는 마법사를 표시할 수 및 DropDownList의 의값에해당해야어떤것을반환합니다`ListItem` s입니다. 있어야는 `CategoryName` 필드를 표시 하 고 사용 하 여는 `CategoryID` 값으로.


[![텍스트 및 ListItems에 대 한 값으로 CategoryName 및 CategoryID 필드를 각각 사용](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image11.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image10.png)

**그림 4**: 사용 된 `CategoryName` 및 `CategoryID` 에 따라 필드는 `Text` 및 `Value` 에 대 한는 `ListItem` s, 각각 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image12.png))


DropDownList 했으므로 시점에서 (`Categories`) 시스템의 범주를 나열 하는입니다. 이제 선택한 범주에 속해 있는 해당 제품을 나열 하는 GridView를 추가 해야 합니다. 그러나 수행 하기 전 보십시오 DropDownList의 스마트 태그에 AutoPostBack 사용 확인란을 선택 합니다. 에 설명 된 대로 *마스터/세부 정보 필터링 된 정도 DropDownList* 는 DropDownList를 설정 하 여 자습서 `AutoPostBack` 속성을 `True` 페이지 게시 될 다시 DropDownList 값이 변경 될 때마다 합니다. 이렇게 하면 새로 고칠 수에 GridView 새로 선택한 범주에 대 한 해당 제품을 표시 합니다. 경우는 `AutoPostBack` 속성이 `False` (기본값) 이면 다시 게시 하지 않습니다 범주를 변경 하 고 따라서 나열 된 제품 업데이트 되지 않습니다.


[![확인란을 사용 하도록 설정 AutoPostBack DropDownList의 스마트 태그](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image14.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image13.png)

**그림 5**: 확인란을 사용 하도록 설정 AutoPostBack DropDownList의 스마트 태그 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image15.png))


선택한 범주에 대 한 제품을 전시 하기 위해 페이지에 GridView 컨트롤을 추가 합니다. GridView의 설정 `ID` 를 `ProductsInCategory` 라는 새 ObjectDataSource 바인딩할 `ProductsInCategoryDataSource`합니다.


[![ProductsInCategoryDataSource 라는 새 ObjectDataSource를 추가 합니다.](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image17.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image16.png)

**그림 6**: 새 ObjectDataSource 라는 추가 `ProductsInCategoryDataSource` ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image18.png))


호출 되도록 구성 된 ObjectDataSource는 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드.


[![GetProductsByCategoryID(categoryID) 메서드를 호출 ObjectDataSource 있어야 합니다.](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image20.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image19.png)

**그림 7**: ObjectDataSource 호출가 `GetProductsByCategoryID(categoryID)` 메서드 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image21.png))


이후는 `GetProductsByCategoryID(categoryID)` 메서드는 입력 매개 변수로 마법사의 마지막 단계에서 매개 변수 값의 원본을 지정할 수 있습니다. 선택한 범주에서 해당 제품을 표시 하기 위해 매개 변수에서 찾아볼 수 있는 `Categories` DropDownList 합니다.


[![선택한 범주 드롭다운 목록에서 매개 변수 값 categoryID 가져오기](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image23.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image22.png)

**그림 8**: 가져오기는 *`categoryID`* 선택한 범주 드롭다운 목록에서 매개 변수 값 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image24.png))


마법사 완료 후 GridView 각 제품 속성에 대해 BoundField를 갖게 됩니다. 이제 이러한 BoundFields 있도록 정리는 `ProductName`, `UnitPrice`, `UnitsInStock`, 및 `UnitsOnOrder` BoundFields 표시 됩니다. 나머지 BoundFields에 모든 필드 수준 설정을 추가할 수 (예: 서식의 `UnitPrice` 통화로). 다음과 같이 변경한 후 GridView의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample1.aspx)]

이 시점에서 주문에 선택한 범주에 속해 있는 해당 제품에 대 한 이름, 단가, 재고, 단위 및 단위를 표시 하는 완벽 하 게 작동 마스터/세부 보고서를 했습니다.


[![선택한 범주 드롭다운 목록에서 매개 변수 값 categoryID 가져오기](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image26.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image25.png)

**그림 9**: 가져오기는 *`categoryID`* 선택한 범주 드롭다운 목록에서 매개 변수 값 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image27.png))


## <a name="step-2-displaying-a-footer-in-the-gridview"></a>2 단계: GridView의 바닥글 표시

GridView 컨트롤에 머리글 및 바닥글 행을 표시할 수 있습니다. 이러한 행의 값에 따라 표시 됩니다는 `ShowHeader` 및 `ShowFooter` 속성을 각각와 `ShowHeader` 기본값으로 `True` 및 `ShowFooter` 를 `False`합니다. 단순히 GridView에 바닥글을 포함 하려면 설정 해당 `ShowFooter` 속성을 `True`합니다.


[![GridView의 ShowFooter 속성이 True로 설정](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image29.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image28.png)

**그림 10**: GridView의 설정 `ShowFooter` 속성을 `True` ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image30.png))


바닥글 행에 각; GridView에 정의 된 필드에 대 한 셀이 그러나 이러한 셀은 기본적으로 비어 있습니다. 브라우저에서 진행률을 볼 보십시오. 와 `ShowFooter` 속성이 이제로 설정 `True`, GridView에는 빈 바닥글 행이 포함 됩니다.


[![GridView 이제는 바닥글 행을 포함 시킵니다.](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image32.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image31.png)

**그림 11**: GridView 이제 바닥글 행이 포함 됩니다 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image33.png))


그림 11의 바닥글 행이 흰색 배경 out, 의미 하지 않습니다. 만들어 보겠습니다는 `FooterStyle` CSS 클래스 `Styles.css` 진한 빨간색 배경을 지정 하 고 구성 합니다는 `GridView.skin` 스킨 파일에는 `DataWebControls` GridView의에이 CSS 클래스를 할당 하는 테마 `FooterStyle`의 `CssClass` 속성. 테마 및 스킨 기술에 해야 할 경우 다시 참조는 [the ObjectDataSource와 데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) 자습서입니다.

다음과 같은 CSS 클래스를 추가 하 여 시작 `Styles.css`:


[!code-css[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample2.css)]

`FooterStyle` CSS 클래스는 비슷한 스타일로 된 `HeaderStyle` 클래스를 `HeaderStyle`의 배경색은 짙을 수록 주의 해야 하 고 해당 텍스트가 굵은 글꼴로 표시 됩니다. 또한 바닥글에 텍스트 오른쪽 맞춤 머리글의 텍스트를 가운데 표시 되는 반면 합니다.

이 CSS 클래스 마다 GridView의 바닥글을 연결 하려면 열고 다음으로 `GridView.skin` 파일에 `DataWebControls` 테마 및 집합은 `FooterStyle`의 `CssClass` 속성. 이 추가 후 파일의 태그는 같습니다.


[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample3.aspx)]

이러한 변경을 통해 바닥글의 스크린 샷을 다음으로 명확 하 게 보다 잘 보이도록 합니다.


[![GridView의 바닥글 행에는 이제 빨강 배경색에](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image35.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image34.png)

**그림 12**: GridView의 바닥글 행에는 이제 빨강 배경색에 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image36.png))


## <a name="step-3-computing-the-summary-data"></a>3 단계: 계산 요약 데이터

GridView의 바닥글 표시 us를 연결 하면 다음 단계 된는 요약 데이터를 계산 하는 방법입니다. 이 정보를 집계를 계산 하는 방법은 두 가지가 있습니다.

1. SQL 쿼리를 통해 특정 범주에 대 한 요약 데이터를 계산 하려면 데이터베이스에는 추가 쿼리를 발급할 수 있습니다 있습니다. 와 함께 집계 함수의 수를 포함 하는 SQL는 `GROUP BY` 절 데이터가 해야 요약 된 데이터를 지정할 수 있습니다. 다음 SQL 쿼리에서 필요한 정보를 다시 가져오기는:  

    [!code-sql[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample4.sql)]

    직접이 쿼리를 발급 하도록 원하지 물론는 `SummaryDataInFooter.aspx` 페이지의 메서드를 만들어서 그 보다는 `ProductsTableAdapter` 및 `ProductsBLL`합니다.
2. 이 정보를 계산 하에 설명 된 대로 GridView에 추가 되 고 되므로 [데이터 기반 시 사용자 지정 서식](custom-formatting-based-upon-data-cs.md) 자습서 GridView의 `RowDataBound` 이벤트 처리기 후 GridView에 추가 되 고 각 행에 대해 한 번씩 발생 해당 되었습니다 데이터 바인딩된 합니다. 이 이벤트에 대 한 이벤트 처리기를 만들어 실행을 유지할 수 있습니다 하고자 하는 값의 합계를 집계 합니다. 마지막 데이터 행의 합계와 평균을 계산 하는 데 필요한 정보가 있는 GridView에 바인딩 되었습니다.

있지만 개인적으로 일반적으로 두 번째 방법은 여행 데이터 액세스 계층 및 비즈니스 논리 계층에서 요약 기능을 구현 하는 데 필요한 노력 및 데이터베이스에 저장 되지만 어느 방법이 든을 적절 하 게 합니다. 이 자습서에 대 한 보겠습니다 두 번째 옵션을 사용 하 고 추적 사용 하 여 누적 합계는 `RowDataBound` 이벤트 처리기입니다.

만들기는 `RowDataBound` GridView 디자이너에서 선택 하 속성 창에서 번개 모양 아이콘을 두 번 클릭 하 여 GridView에 대 한 이벤트 처리기는 `RowDataBound` 이벤트입니다. 또는 ASP.NET 코드 숨김 클래스 파일 맨 위에 있는 드롭다운 목록에서 GridView 및 해당 RowDataBound 이벤트를 선택할 수 있습니다. 이렇게 하면 라는 새 이벤트 처리기를 만들어집니다 `ProductsInCategory_RowDataBound` 에 `SummaryDataInFooter.aspx` 페이지의 코드 숨김 클래스입니다.


[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample5.vb)]

누적 합계를 유지 하기 위해 이벤트 처리기의 범위 외부의 변수를 정의 해야 합니다. 다음과 같은 네 개의 페이지 수준 변수를 만듭니다.

- `_totalUnitPrice`형식 `Decimal`
- `_totalNonNullUnitPriceCount`형식 `Integer`
- `_totalUnitsInStock`형식 `Integer`
- `_totalUnitsOnOrder`형식 `Integer`

다음으로에서 발생 한 각 데이터 행에 대해 이러한 세 개의 변수를 증가 하는 코드를 작성은 `RowDataBound` 이벤트 처리기입니다.


[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample6.vb)]

`RowDataBound` DataRow를 처리 하는 것을 확인 하 여 이벤트 처리기를 시작 합니다. 설정 된 되 면는 `Northwind.ProductsRow` 방금에 바인딩된 인스턴스는 `GridViewRow` 개체 `e.Row` 변수에 저장 `product`합니다. 다음에서 실행 되며, 총 변수는 현재 제품의 해당 값 만큼 증분됩니다 (데이터베이스를 포함 하지 않는다는 이라고 가정할 `NULL` 값). 모두 실행 한 추적에서는 `UnitPrice` 합계와 수가 이외의`NULL` `UnitPrice` 평균 가격은이 두 숫자의 몫 때문에 기록 합니다.

## <a name="step-4-displaying-the-summary-data-in-the-footer"></a>4 단계: 바닥글의 요약 데이터를 표시합니다.

합계의 요약 데이터를 GridView의 바닥글 행에 표시를 하는 마지막 단계가입니다. 이 작업을 수행할 수 있습니다 통해 프로그래밍 방식으로 `RowDataBound` 이벤트 처리기입니다. 이전에 설명한 대로 `RowDataBound` 이벤트 처리기에 대해 발생 *모든* 바닥글 행을 포함 하 여 GridView에 바인딩되는 행입니다. 따라서 다음 코드를 사용 하 여 바닥글 행에 데이터를 표시 하려면 이벤트 처리기를 추가할 수 있습니다.


[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample7.vb)]

바닥글 행의 모든 데이터 행 추가 되 고 나면 GridView에 추가 되 면 시간순으로 한다는 것 누적 합계 계산은 완료 바닥글에 요약 데이터를 표시할 준비가 신뢰할 수 있습니다. 그런 다음 이전 단계를 바닥글의 셀에서 이러한 값을 설정 됩니다.

사용 하 여 특정 바닥글 셀에 텍스트를 표시 하려면 `e.Row.Cells(index).Text = value`, 여기서는 `Cells` 0에서 시작 하는 인덱스가 있습니다. 다음 코드는 평균 가격 (제품의 수로 나눈 총 가격)를 계산 하 고 주식형 및 GridView의 적절 한 바닥글 셀에서 순서에는 단위에 단위의 총 수와 함께 표시 됩니다.


[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample8.vb)]

그림 13에서는이 코드를 추가한 후 보고서를 표시 합니다. 참고 방법을 `ToString("c")` 하면 평균 가격 요약 정보가 통화 형식으로 지정 되어야 합니다.


[![GridView의 바닥글 행에는 이제 빨강 배경색에](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image38.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image37.png)

**그림 13**: GridView의 바닥글 행에는 이제 빨강 배경색에 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image39.png))


## <a name="summary"></a>요약

요약 데이터를 표시 하는 것은 일반적인 보고서 요구 사항 및 GridView 컨트롤을 사용 하면 손쉽게의 바닥글 행에 이러한 정보를 포함할 수 있습니다. 바닥글 행이 표시 때 GridView의 `ShowFooter` 속성이 `True` 통해 프로그래밍 방식으로 설정 하는 셀에 텍스트를 사용할 수 있습니다 및는 `RowDataBound` 이벤트 처리기입니다. 요약 데이터를 계산 하거나 가능 다시 쿼리 하는 데이터베이스 또는 요약 데이터를 프로그래밍 방식으로 계산 하는 ASP.NET 페이지의 코드 숨김 클래스에서 코드를 사용 하 여 합니다.

이 자습서에는 우리의 검사 GridView, DetailsView, FormView 컨트롤 사용자 지정 형식으로 마칩니다. 이 다음 자습서를 삽입, 업데이트 및 이러한 동일한 컨트롤을 사용 하 여 데이터를 삭제 한 탐색을 시작 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](using-the-formview-s-templates-vb.md)
