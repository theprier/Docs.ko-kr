---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs
title: 마스터 레코드의 글머리 기호 목록 사용 세부 정보 (C#) 사용 하 여 마스터/세부 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 म 합니다 압축 이전 자습서의 2 페이지 마스터/세부 정보 보고서를 단일 페이지에 t에 범주 이름 글머리 기호 목록이 표시 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2006
ms.topic: article
ms.assetid: c727bb73-7b59-41a1-8dc3-623c6d69e7c2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: c041c352c379dc1d3c0f13013e7e323faa500912
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="masterdetail-using-a-bulleted-list-of-master-records-with-a-details-datalist-c"></a>마스터/세부 글머리 기호 목록이 마스터 레코드를 사용 하 여 사용 세부 정보 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_35_CS.exe) 또는 [PDF 다운로드](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/datatutorial35cs1.pdf)

> 이 자습서에서는 म 합니다 압축 이전 자습서의 2 페이지 마스터/세부 정보 보고서를 단일 페이지에 범주 이름의 글머리 기호 목록 화면 및 화면 오른쪽에 선택한 범주의 제품의 왼쪽에 표시 합니다.


## <a name="introduction"></a>소개

에 [이전 자습서](master-detail-filtering-acess-two-pages-datalist-cs.md) 두 페이지에 걸쳐 마스터/세부 정보 보고서를 구분 하는 방법을 살펴보았습니다. 마스터 페이지 글머리 기호 목록이 범주를 렌더링 하는 반복기 컨트롤을 사용 했습니다. 각 범주 이름은 된 하이퍼링크, 클릭 하면 것 take 2 열 DataList 해당 제품을 보인 세부 정보 페이지를 사용자에 속하는 선택한 범주입니다.

이 자습서에서는 म 합니다 압축 두 페이지 자습서는 단일 페이지에 LinkButton으로 렌더링 하는 각 범주 이름은 범주 이름의 글머리 기호 목록 화면 왼쪽에 표시 합니다. Linkbutton이 있는 범주 이름 중 하나를 클릭에서 포스트백을 수행 하 고 화면 오른쪽에 열이 두 DataList에 선택한 범주의 제품을 바인딩합니다. 왼쪽에 반복 각 범주의 이름을 표시할 뿐 아니라 특정된 범주에 있는 총 제품 있을 수를 보여 (그림 1 참조).


[![제품의 총 수 및 범주의 이름 왼쪽에 표시 됩니다.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image2.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image1.png)

**그림 1**: s The 범주 이름 및 제품의 총 수는 왼쪽에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image3.png))


## <a name="step-1-displaying-a-repeater-in-the-left-portion-of-the-screen"></a>1 단계: 화면 왼쪽된 부분에는 반복기를 표시합니다.

이 자습서에 대 한 글머리 기호 목록이 있는 범주 선택한 범주의 제품의 왼쪽에 표시 해야 합니다. 웹 페이지 내에서 콘텐츠는 표준 HTML 요소 단락 태그를 줄 바꿈하지 않는 공백을 사용 하 여 배치 될 수 있습니다 `<table>` s, 등에 또는 연계 스타일 시트 (CSS) 기술을 통해. 이 자습서의 모든 지금까지 사용 CSS 기술을 위치를 지정 합니다. 마스터 페이지의 탐색 사용자 인터페이스를 빌드 했습니다는 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-cs.md) 사용 자습서 *절대 위치*, 탐색에 대 한 정확한 픽셀 오프셋을 나타내는 목록 및 주 콘텐츠입니다. 오른쪽 또는 왼쪽의를 통해 다른 하나의 요소를 배치에 CSS를 사용할 수 또는 *부동*합니다. 이전 점이 DataList의 왼쪽에 반복 부동 하 여 선택한 범주의 제품의 왼쪽에 표시 범주 글머리 기호 목록

열기는 `CategoriesAndProducts.aspx` 에서 페이지는 `DataListRepeaterFiltering` 폴더는 반복기 및 DataList 페이지에 추가 합니다. 반복기 s 설정 `ID` 를 `Categories` 및를 s DataList `CategoryProducts`합니다. 소스 보기로 이동 하 고 자체 내에서 반복기 및 DataList 컨트롤이 추가 `<div>` 요소입니다. 즉, 내에서 반복기를 묶습니다는 `<div>` 요소 첫 번째 및 다음에 자체 DataList `<div>` 반복 바로 뒤 요소입니다. 태그에이 시점에서 같아야 합니다 다음과 비슷합니다.


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample1.aspx)]

사용 하도록 설정 해야 DataList의 왼쪽에 반복 float는 `float` CSS 스타일 특성 같이:


[!code-html[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample2.html)]

`float: left;` 첫 번째 부동 `<div>` 두 번째 식의 왼쪽에 있는 요소입니다. `width` 및 `padding-right` 설정에 따르면 첫 번째 `<div>` s `width` 안쪽 여백 사이 추가 하 고는 `<div>`의 요소 내용 및 오른쪽 여백이 합니다. 부동 요소 CSS에 대 한 자세한 내용은 체크 아웃 된 [Floatutorial](http://css.maxdesign.com.au/floatutorial/)합니다.

첫 번째를 통해 직접 스타일 설정 값을 지정 하지 않고 `<p>` 요소 s `style` 특성에서 새 CSS 클래스를 만드는 대신 s `Styles.css` 라는 `FloatLeft`:


[!code-css[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample3.css)]

다음 대체할 수는 `<div>` 와 `<div class="FloatLeft">`합니다.

CSS 클래스를 추가 하 고의 태그를 구성한 후의 `CategoriesAndProducts.aspx` 페이지 디자이너에 있습니다. 반복기 (오른쪽 이제 모두 방금가 표시 되지만 회색 상자에서는 이후에 해당 데이터 원본 또는 서식 파일을 구성 하는 아직 했습니다 대로) 부동 DataList의 왼쪽에 표시 됩니다.


[![DataList의 왼쪽으로 움직이는 반복](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image5.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image4.png)

**그림 2**: The 반복기 DataList의 왼쪽으로 움직이는 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image6.png))


## <a name="step-2-determining-the-number-of-products-for-each-category"></a>2 단계: 각 범주에 대 한 제품의 수를 결정

완료 태그 주변 반복기 및 DataList s로 제어 반복기의 범주 데이터를 바인딩할 준비 된 것입니다. 그러나 범주 그림 1에 글머리 기호 목록에서 볼 수 있듯이 각 범주의 이름 외에 필요는 범주와 관련 된 제품의 수를 표시 해야 합니다. 이 정보에 액세스 하려면 가능 하거나 합니다.

- **ASP.NET 페이지의 코드 숨김 클래스에서이 정보를 확인 합니다.** 특정 *`categoryID`* 호출 하 여 연결 된 제품 수를 확인할 수 있습니다는 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드. 이 메서드는 반환는 `ProductsDataTable` 개체 `Count` 속성 나타냅니다 개수 `ProductsRow` s가 지정 된 제품의 수는 *`categoryID`*합니다. 만들 수 있습니다는 `ItemDataBound` 반복 바인딩된 각 범주에 대 한 호출 하는 반복기에 대 한 이벤트 처리기는 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드 출력의 개수를 포함 합니다.
- **업데이트는 `CategoriesDataTable` 포함 하도록 입력 데이터 집합에는 `NumberOfProducts` 열입니다.** 그런 다음 업데이트할 수는 `GetCategories()` 에서 메서드는 `CategoriesDataTable` 이 정보를 포함 하거나, 또는 두고 `GetCategories()` 로-이며 새 `CategoriesDataTable` 라는 메서드가 `GetCategoriesAndNumberOfProducts()`합니다.

S 이러한 두 기술 모두를 탐색할 수 있도록 합니다. 첫 번째 방법은 더 간단 하 게 데이터 액세스 계층; 업데이트를 t 필요 하지 않는 것 때문에 구현 그러나 데이터베이스와의 통신을 더 걸립니다. 에 대 한 호출에서 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 에서 메서드는 `ItemDataBound` 이벤트 처리기 반복 표시 된 각 범주에 대 한 추가 데이터베이스 호출을 추가 합니다. 이 기술을 사용 하 여 없는 *N* + 1 데이터베이스 호출, 여기서 *N* 반복기에 표시 되는 범주 수입니다. 두 번째 접근 방식으로 제품 수가에서 각 범주에 대 한 정보가 반환 됩니다는 `CategoriesBLL` s 클래스 `GetCategories()` (또는 `GetCategoriesAndNumberOfProducts()`) 메서드를 사용 하므로 데이터베이스에 한 번만 발생 합니다.

## <a name="determining-the-number-of-products-in-the-itemdatabound-event-handler"></a>ItemDataBound 이벤트 처리기에서 제품 수를 결정합니다.

반복기 s의에서 각 범주에 대 한 제품의 수를 결정 하 `ItemDataBound` 이벤트 처리기에서 기존 데이터 액세스 계층을 수정 하지 않아도 됩니다. 모든 수정 하기 바로 아래에 `CategoriesAndProducts.aspx` 페이지. 라는 새 ObjectDataSource를 추가 하 여 시작 `CategoriesDataSource` 반복기 s 스마트 태그를 통해 합니다. 다음으로 구성 된 `CategoriesDataSource` ObjectDataSource 한다는에서 해당 데이터를 검색 하므로 `CategoriesBLL` s 클래스 `GetCategories()` 메서드.


[![ObjectDataSource의 GetCategories() 메서드 CategoriesBLL 클래스를 사용 하도록 구성](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image8.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image7.png)

**그림 3**: 구성에 사용 하 여 ObjectDataSource는 `CategoriesBLL` s 클래스 `GetCategories()` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image9.png))


각 항목에는 `Categories` 반복기를 클릭할 수 고를 클릭 하면 발생 하는 데 필요한는 `CategoryProducts` DataList 선택한 범주에 대 한 해당 제품을 표시 합니다. 각 범주는 하이퍼링크를이 동일한 페이지에 다시 연결 하 여이 작업을 수행할 수 있습니다 (`CategoriesAndProducts.aspx`)를 전달 하지만 `CategoryID` 이전 자습서에서 설명한 것 처럼 쿼리 문자열을 통해. 이 방법의 장점은 경우 특정 범주의의 제품을 표시 하는 페이지 수 책갈피가 표시 된 검색 엔진에 의해 인덱싱됩니다.

또는 위해 각 범주 LinkButton을 하는이 자습서에서는 방법입니다. LinkButton을 하이퍼링크로 s 사용자 브라우저에서 변환 하지만를 클릭 하면 포스트백을 수행 합니다. 다시 게시 될 DataList의 ObjectDataSource 새로 고칠 필요가 선택한 범주에 속하는 해당 제품을 표시 합니다. 이 자습서에 대 한 하이퍼링크를 사용 하 여 보다 합리적 LinkButton;를 사용 하 여 보다 그러나 다른 시나리오는 LinkButton을 사용 하는 편이 좋은 더 있을 수 있습니다. 하이퍼링크 방법은이 예제에 대 한 이상적인 것을 하는 동안에 대신 LinkButton을 사용 하 여 탐색 s 사용 수 있습니다. 볼 수 있겠지만, LinkButton을 사용 하 여는 하이퍼링크와 그렇지 않은 경우 발생 하지 하는 몇 가지 과제를 소개 합니다. 따라서 LinkButton을 사용 하 여이 자습서에서는 이러한 문제를 강조 표시 되며 여기서 하려는 LinkButton 하이퍼링크를 대신 사용 하 여 이러한 시나리오에 대 한 솔루션을 제공 하는 데 도움이 됩니다.

> [!NOTE]
> 하이퍼링크 컨트롤을 사용 하 여이 자습서를 반복 하는 것이 좋습니다 또는 `<a>` LinkButton 대신이 구성 요소는 요소입니다.


다음 태그는 ObjectDataSource 및 반복기에 대 한 선언적 구문을 보여 줍니다. S 템플릿에 글머리 기호 목록 LinkButton로 각 항목을 렌더링 하는 참고:


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample4.aspx)]

> [!NOTE]
> 이 자습서에 대 한 반복기에서 뷰 상태를 사용할 수 있어야 합니다 (생략 참고는 `EnableViewState="False"` 반복기 s 선언적 구문에서). 3 단계에서 우리 만들게 됩니다 한 이벤트 처리기 반복 s에 대 한 `ItemCommand` 이벤트를 업데이트 합니다 s ObjectDataSource의 DataList `SelectParameters` 컬렉션입니다. 반복기의 `ItemCommand`그러나 뷰 상태를 비활성화 하는 경우 t 화재를 획득 합니다. 참조 [ASP.NET 질문의 A Stumper](http://scottonwriting.net/sowblog/posts/1263.aspx) 및 [되면서 솔루션](http://scottonwriting.net/sowBlog/posts/1268.aspx) 이유에 대 한 자세한 내용은 뷰 상태를 반복 s에 대 한 사용 해야 `ItemCommand` 이벤트를 발생 합니다.


인 LinkButton는 `ID` 속성 값이 `ViewCategory` 없는 해당 `Text` 속성 집합입니다. 방금 범주 이름을 표시 하 려 했습니다, 하는 경우에서는 설정한 것과 Text 속성, 선언적 데이터 바인딩 구문을 통해 같이:


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample5.aspx)]

그러나 s 범주 이름을 표시 하려고 *및* 해당 범주에 속하는 제품의 수입니다. S 반복기에서이 정보를 검색할 수 있습니다 `ItemDataBound` 호출 하 여 이벤트 처리기는 `ProductBLL` s 클래스 `GetCategoriesByProductID(categoryID)` 메서드와 레코드 개수 결과에 반환될지를 결정 `ProductsDataTable`, 다음 코드와 보여 줍니다.


[!code-csharp[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample6.cs)]

다음을 통해 일부 터 시작 우리는 데이터 항목 작업 다시 (하나의 인 `ItemType` 은 `Item` 또는 `AlternatingItem`)을 참조할 수는 `CategoriesRow` 현재 방금 바인딩된 인스턴스 `RepeaterItem`합니다. 인스턴스를 만들어이 범주에 대 한 제품의 수를 결정 우리는 다음으로 `ProductsBLL` 클래스, 호출의 `GetCategoriesByProductID(categoryID)` 메서드를 사용 하 여 반환 된 레코드의 수를 결정 하는 `Count` 속성입니다. 마지막으로 `ViewCategory` LinkButton ItemTemplate에는 참조 및 해당 `Text` 속성이 *CategoryName* (*NumberOfProductsInCategory*) 여기서  *NumberOfProductsInCategory* 소수 자릿수 0을 사용 하 여 서식이 지정 됩니다.

> [!NOTE]
> 또는 수를 추가 했습니다는 *함수를 서식* 범주 s 허용 하는 ASP.NET 페이지의 코드 숨김 클래스를 `CategoryName` 및 `CategoryID` 값을 반환는 `CategoryName` 의 번호로 연결 제품 범주에 있는 (호출 하 여 결정 되는 `GetCategoriesByProductID(categoryID)` 메서드). Text 속성에 대 한 필요성 LinkButton s에 선언적으로 지정할 수 있습니다 이러한 서식 지정 함수 결과 `ItemDataBound` 이벤트 처리기입니다. 참조는 [GridView 컨트롤에 사용 하 여 TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) 또는 [DataList 및 데이터에 따라 반복기 서식 지정](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs.md) 서식 지정 함수를 사용 하는 방법은 대 한 자습서입니다.


이 이벤트 처리기를 추가한 후 브라우저를 통해 페이지를 테스트 하려면 보십시오. S 범주 이름 및 범주와 관련 된 제품 수를 표시 하는 글머리 기호 목록에서 각 범주는 나열 하는 방법 (그림 4 참조).


[![각 범주의 이름 및 제품의 수 표시 됩니다.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image11.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image10.png)

**그림 4**: 각 범주 이름 및 제품의 수 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image12.png))


## <a name="updating-thecategoriesdatatableandcategoriestableadapterto-include-the-number-of-products-for-each-category"></a>업데이트는`CategoriesDataTable`및`CategoriesTableAdapter`각 범주에 대 한 제품 개수를 포함 하려면

각 범주에 대 한 제품의 수를 결정 하는 대신 s는 반복기에 바인딩된 조정 하 여이 프로세스를 간소화할 수 있습니다는 `CategoriesDataTable` 및 `CategoriesTableAdapter` 기본적으로이 정보를 포함 하도록 데이터 액세스 계층에서. 이를 위해 새 열을 추가 해야 `CategoriesDataTable` 관련된 제품의 수를 보유 하 합니다. DataTable에 새 열을 추가 하려면 입력 데이터 집합을 엽니다 (`App_Code\DAL\Northwind.xsd`)을 수정 하려면 DataTable을 마우스 오른쪽 단추로 클릭 하 고 추가 선택 / 열입니다. 새 열을 추가 하는 `CategoriesDataTable` (그림 5 참조).


[![CategoriesDataSource에 새 열 추가](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image14.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image13.png)

**그림 5**: 새 열을 추가 하는 `CategoriesDataSource` ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image15.png))


라는 새 열이 추가 됩니다 `Column1`, 다른 이름을 입력 하 여 변경할 수 있습니다. 이 새 열을 이름 바꾸기 `NumberOfProducts`합니다. 다음으로,이 열의 속성을 구성 해야 합니다. 속성 창으로 이동 하 고 새 열을 클릭 합니다. S 열 변경 `DataType` 속성 `System.String` 를 `System.Int32` 설정 하 고는 `ReadOnly` 속성을 `True`그림 6에 나와 있는 것 처럼, 합니다.


![데이터 형식 및 새 열의 ReadOnly 속성 설정](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image16.png)

**그림 6**: 설정의 `DataType` 및 `ReadOnly` 새 열의 속성


동안는 `CategoriesDataTable` 이제는 `NumberOfProducts` 열에서 해당 값 해당 TableAdapter의 쿼리 중 하나에 의해 설정 되지 않았습니다. 업데이트할 수는 `GetCategories()` 범주 정보를 검색할 때마다 이러한 정보를 원하는 경우이 정보를 반환 하는 메서드 반환 합니다. 하지만 드문 경우 (예:이 자습서에 앞서) 범주에 대 한 관련된 제품 수가 선택만 하면 경우 삭제할 수 있습니다. `GetCategories()` 로-이며이 정보를 반환 하는 새 메서드를 만듭니다. 라는 새 메서드를 만들기,이 방법을 통해를 사용 하 여 s let `GetCategoriesAndNumberOfProducts()`합니다.

이 새로 추가 하려면 `GetCategoriesAndNumberOfProducts()` 메서드를 마우스 오른쪽 단추로 클릭은 `CategoriesTableAdapter` 새 쿼리를 선택 합니다. 이렇게 하면 위쪽 TableAdapter 쿼리 구성 마법사, 우리는 여러 번 이전 자습서에서에서 사용 했습니다. 이 메서드에 대 한 쿼리는 행을 반환 하는 임시 SQL 문 사용을 지정 하 여 마법사를 시작 합니다.


[![임시 SQL 문을 사용 하 여 메서드 만들기](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image18.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image17.png)

**그림 7**: 특별 SQL 문을 사용 하 여 메서드 만들기 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image19.png))


[![SQL 문은 행을 반환](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image21.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image20.png)

**그림 8**: SQL 문이 반환 행 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image22.png))


마법사의 다음 화면 쿼리에서 사용 하 라는 메시지가 나타납니다. 각 범주 s 반환할 `CategoryID`, `CategoryName`, 및 `Description` 필드는 범주와 관련 된 제품 수와 함께 사용 하 여 다음 `SELECT` 문:


[!code-sql[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample7.sql)]


[![쿼리를 사용 하 여 지정](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image24.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image23.png)

**그림 9**: 쿼리를 사용 하 여 지정 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image25.png))


범주와 관련 된 제품 수를 계산 하는 하위 쿼리는 별칭이 `NumberOfProducts`합니다. 이 명명 일치 하면와 연결할이 하위 쿼리에서 반환한 값은 `CategoriesDataTable` s `NumberOfProducts` 열입니다.

이 쿼리를 입력 한 후 새 메서드에 대 한 이름을 선택 하려면 마지막 단계가입니다. 사용 하 여 `FillWithNumberOfProducts` 및 `GetCategoriesAndNumberOfProducts` 채우기 DataTable 및 반환 DataTable 패턴, 각각.


[![새 TableAdapter의 메서드 FillWithNumberOfProducts 이름과 GetCategoriesAndNumberOfProducts](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image27.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image26.png)

**그림 10**: 새 tableadapter 메서드 이름을 `FillWithNumberOfProducts` 및 `GetCategoriesAndNumberOfProducts` ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image28.png))


이 시점에서 데이터 액세스 계층에 속한 제품의 수를 포함 하도록 확장 되었습니다. 이 모든 프레젠테이션 계층에 대 한 모든 호출에는 dal과 별도 비즈니스 논리 계층을 통해 라우팅합니다 있으므로 해당 추가 해야 `GetCategoriesAndNumberOfProducts` 메서드는 `CategoriesBLL` 클래스:


[!code-csharp[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample8.cs)]

DAL 및 BLL 전체를 다시 म 준비 됨이 데이터를 바인딩하는 `Categories` 반복기에서 `CategoriesAndProducts.aspx`! 적에서 확인 된 반복기에 대 한 프로그램 ObjectDataSource를 이미 만든 경우의 제품 수의 `ItemDataBound` 이 ObjectDataSource를 삭제 하 고 s 반복기를 제거 하는 이벤트 처리기 섹션이 `DataSourceID` 속성 무선의 자유도 설정;는 반복기 s `ItemDataBound` 제거 하 여 이벤트 처리기에서 이벤트는 `Handles Categories.OnItemDataBound` ASP.NET 코드 숨김 클래스의 구문이 있습니다.

원래 상태로 다시에 반복 이라는 새 ObjectDataSource 추가 `CategoriesDataSource` 반복기 s 스마트 태그를 통해 합니다. ObjectDataSource 사용 하도록 구성 된 `CategoriesBLL` 클래스 하지만 사용 하지 않고는 `GetCategories()` 메서드를 사용 했습니다 `GetCategoriesAndNumberOfProducts()` 대신 (11 그림 참조).


[![ObjectDataSource GetCategoriesAndNumberOfProducts 메서드를 사용 하도록 구성](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image30.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image29.png)

**그림 11**: 구성에 사용 하 여 ObjectDataSource는 `GetCategoriesAndNumberOfProducts` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image31.png))


다음을 업데이트 하는 `ItemTemplate` 있도록 LinkButton s `Text` 속성 databinding 구문을 사용 하 여 선언적으로 할당 되었고이 모두 포함 됩니다는 `CategoryName` 및 `NumberOfProducts` 데이터 필드입니다. 반복기에 대 한 전체 선언적 태그 및 `CategoriesDataSource` ObjectDataSource 수행:


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample9.aspx)]

DAL 포함 하도록 업데이트 하 여 렌더링 된 출력은 `NumberOfProducts` 사용할 때와 같은 열이는 `ItemDataBound` 이벤트 처리기 방법 (다시 화면이 표시를 그림 4 참조 샷 범주 이름 및 제품의 수를 보여 주는 반복).

## <a name="step-3-displaying-the-selected-category-s-products"></a>3 단계: 선택한 범주의 제품 표시

이 시점에서 했으므로 `Categories` 각 범주에서 제품 수와 함께 범주의 목록을 표시 하는 반복기입니다. 반복기 LinkButton을 클릭 하면로 인해 포스트백을 가리키는지에서는 각 범주에 대 한 사용 하 여 해당 제품에는 선택한 범주에 대 한 표시 하기 위해 필요한는 `CategoryProducts` DataList 합니다.

Us 직면 됩니다 DataList만 선택한 범주에 대 한 해당 제품을 표시 하는 방법. 에 [마스터/세부 정보 DetailsView 선택 가능한 마스터 GridView 사용에 대해 자세히 설명](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) 는 GridView 행이 있는 작성 하는 방법에 살펴보았습니다 자습서를 선택할 수 없습니다, 선택 된 행으로 s 세부 정보 같은 페이지에 DetailsView에 표시 되 고 있습니다. GridView의 ObjectDataSource를 사용 하 여 모든 제품에 대 한 정보를 반환 되는 `ProductsBLL` s `GetProducts()` DetailsView의 ObjectDataSource 하는 동안 메서드를 사용 하 여 선택한 제품에 대 한 정보를 검색는 `GetProductsByProductID(productID)` 메서드. *`productID`* 매개 변수 값이 GridView s의 값과 연결 하 여 선언적으로 제공 `SelectedValue` 속성입니다. 안타깝게도, 반복기가 없습니다는 `SelectedValue` 속성 및 매개 변수 원본으로 사용할 수 없습니다.

> [!NOTE]
> 반복기에서 LinkButton을 사용할 때 나타나는 이러한 과제 중 하나입니다. 하이퍼링크에 전달 하도록 사용에 `CategoryID` querystring을 통해 대신 우리 수 해당 QueryString 필드 원본으로 사용할 매개 변수의 값에 대 한 합니다.


부족 걱정 전에 `SelectedValue` 는 반복기에 대 한 속성에 s 먼저 DataList는 ObjectDataSource 바인딩할 하 고 지정 하지만 수 있도록 해당 `ItemTemplate`합니다.

DataList s 스마트 태그에서 명명 된 새 ObjectDataSource를 추가 하도록 선택할 `CategoryProductsDataSource` 사용 하도록 구성 하 고는 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드. 읽기 전용 인터페이스를 제공 하는이 자습서에서는 DataList을 이후 자유롭게 INSERT, UPDATE, 드롭 다운 목록을 설정 하 고 각 탭 (없음)을 삭제 합니다.


[![ObjectDataSource ProductsBLL 클래스의 GetProductsByCategoryID(categoryID) 메서드를 사용 하도록 구성](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image33.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image32.png)

**그림 12**: 구성에 사용 하 여 ObjectDataSource `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image34.png))


이후는 `GetProductsByCategoryID(categoryID)` 메서드에서 입력된 매개 변수를 예상 (*`categoryID`*), 데이터 소스 구성 마법사를 사용 하면 매개 변수의 소스를 지정할 수 있도록 합니다. 범주는 GridView 또는 DataList에 나열 된, d 설정 하 여 매개 변수 소스 드롭 다운 목록을 제어 하 고에 ControlID는 `ID` 웹 컨트롤 데이터의 합니다. 그러나 반복기에 이후는 `SelectedValue` 속성 매개 변수 원본으로 사용할 수 없습니다. 을 선택 하면 있습니다 ControlID 드롭 다운 목록 컨트롤만 포함 되어 있는지 `ID``CategoryProducts`, `ID` DataList의 합니다.

지금은 매개 변수 소스 드롭 다운 목록 None으로 설정 합니다. 프로그래밍 방식으로 범주 반복기에서 LinkButton을 클릭할 때이 매개 변수 값을 할당 남게 됩니다.


[![매개 변수 categoryID에 대 한 매개 변수 소스를 지정 하지 마십시오](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image36.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image35.png)

**그림 13**:에 대 한 매개 변수 소스를 지정 하지 않으면는 *`categoryID`* 매개 변수 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image37.png))


데이터 소스 구성 마법사를 완료 한 후 Visual Studio 자동으로 생성 s DataList `ItemTemplate`합니다. 이 기본 대체 `ItemTemplate` 템플릿을 사용 하 여 이전 자습서에서 사용 했습니다;이 또한 s DataList 설정 `RepeatColumns` 속성을 2로 합니다. 이러한 변경을 수행한 후 여 DataList 및 해당 관련된 ObjectDataSource에 대 한 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample10.aspx)]

현재는 `CategoryProductsDataSource` ObjectDataSource s *`categoryID`* 매개 변수가 설정 되지 않은, 이므로 페이지를 볼 때 제품이 표시 됩니다. 이 매개 변수 값 설정에 따라 수행에 필요한 것은 `CategoryID` 반복기 클릭 한 범주입니다. 두 가지 문제에 소개: 먼저 어떻게 결정 하지 때 s 반복기에서 LinkButton `ItemTemplate` 경과 했는데도; 클릭, 두 번째 수 결정 하는 방법의 `CategoryID` 해당 범주에 속하는 인 LinkButton이 클릭 되었습니다?

단추와 ImageButton 컨트롤 같이 LinkButton에는 `Click` 이벤트 및 [ `Command` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.command.aspx)합니다. `Click` 이벤트 LinkButton 클릭 했음을 기록할 하도록 설계 되었습니다. 그러나 시간에 LinkButton 클릭 했음을 확인 하는 것 외에도 또한 해야 이벤트 처리기에 몇 가지 추가 정보를 전달 합니다. LinkButton s 좋다고 [ `CommandName` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandname.aspx) 및 [ `CommandArgument` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandargument.aspx) 속성이 추가 정보를 할당할 수 있습니다. 그런 다음 LinkButton을 클릭할 경우 해당 `Command` 이벤트 발생 (대신 해당 `Click` 이벤트) 이벤트 처리기가 값을 전달 하 고는 `CommandName` 및 `CommandArgument` 속성입니다.

경우는 `Command` 반복기의 반복기에서 서식 파일 내에서 이벤트를 발생 [ `ItemCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeater.itemcommand.aspx) 발생 하 고 전달 되는 `CommandName` 및 `CommandArgument` 클릭할된 LinkButton의 값 (또는 단추 또는 ImageButton)입니다. 따라서 범주 반복기에서 LinkButton 클릭 했는지 시기를 확인 하려면 해야 다음 작업을 수행 합니다.

1. 설정의 `CommandName` s 반복기에서 LinkButton 속성 `ItemTemplate` 를 값으로 (I ListProducts을 사용한 적). 이 설정 하 여 `CommandName` 값을 LinkButton의 `Command` LinkButton을 클릭할 때이 이벤트가 발생 합니다.
2. LinkButton s 설정 `CommandArgument` 속성 s 현재 항목의 값을 `CategoryID`합니다.
3. S 반복기에 대 한 이벤트 처리기를 만들고 `ItemCommand` 이벤트입니다. 이벤트 처리기를 집합에 `CategoryProductsDataSource` ObjectDataSource s `CategoryID` 매개 변수 값의 전달 기능이 `CommandArgument`합니다.

다음 `ItemTemplate` 범주 반복기에 대 한 태그 1 및 2 단계를 구현 합니다. 참고 방법을 `CommandArgument` 값이 할당 된 데이터 항목의 `CategoryID` databinding 구문을 사용 하 여:


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample11.aspx)]

만들 때마다는 `ItemCommand` 항상 먼저 들어오는 확인 하려면 운영 하는 이벤트 처리기 `CommandName` 때문에 값 *모든* `Command` 이벤트에 의해 발생 *모든* 단추, LinkButton을 또는 반복 내에서 ImageButton 하면는 `ItemCommand` 이벤트를 발생 합니다. 에서는 현재만 있을 이러한 하나 LinkButton 이제, 나중에 있습니다 (또는 우리 팀에 다른 개발자) 수 추가 단추 웹 컨트롤을 추가 반복기는 동일한 클릭 하면 발생 `ItemCommand` 이벤트 처리기입니다. 따라서 그 s 체크이 있는지 항상 확인 하는 최선의 `CommandName` 속성만 예상 값에 일치 하는 경우 프로그래밍 논리로 계속 진행 합니다.

전달 기능을 확인 한 후 `CommandName` ListProducts 같은 값을, 이벤트 처리기 다음 할당는 `CategoryProductsDataSource` ObjectDataSource s `CategoryID` 매개 변수 값의 전달 기능이 `CommandArgument`합니다. ObjectDataSource s에이 수정 `SelectParameters` 자체 새로 선택한 범주에 대 한 제품을 표시 하는 데이터 원본에 바인딩할 DataList는 자동으로 합니다.


[!code-csharp[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample12.cs)]

이러한 추가 내용은 자습서를 완료! 브라우저에서 테스트 하는 데 시간을 갖고자 합니다. 그림 14 먼저 페이지를 방문 하는 경우 화면을 보여 줍니다. 범주를 선택 해야 아직에 있으므로 제품이 표시 됩니다. 생성, 같은 범주를 클릭 하면 해당 제품의 제품 범주 열이 두 보기에 표시 됩니다 (그림 15 참조).


[![제품이 표시 되는 경우 첫 번째 페이지를 방문 됩니다.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image39.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image38.png)

**그림 14**: No 제품이 표시 되는 경우 첫 번째 페이지를 방문 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image40.png))


[![생성 범주 목록이 일치 하는 제품 오른쪽을 클릭 하면](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image42.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image41.png)

**그림 15**: 오른쪽으로 일치 하는 제품을 나열 생성 범주를 클릭 하면 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image43.png))


## <a name="summary"></a>요약

이 자습서와 앞에서 살펴본 것 처럼 마스터/세부 보고서 두 페이지에 걸쳐 분산 될 수 있습니다 또는 하나에 통합 합니다. 그러나 레이아웃 마스터 및 세부 정보 페이지의 레코드에 몇 가지 과제는 방법에 가장을 소개 마스터/세부 정보 보고서를 한 페이지에 표시 합니다. 에 *마스터/세부 정보 DetailsView 선택 가능한 마스터 GridView 사용에 대해 자세히 설명* 했습니다. 마스터 레코드 위에 표시 되는 세부 정보 레코드가;이 자습서에서는 마스터 레코드 float 있어야 CSS 기술을 사용 자습서는 왼쪽의 세부 정보입니다.

마스터/세부 정보 보고서를 표시, 함께 했습니다 내에서 클릭할 LinkButton (또는 단추 또는 ImageButton) 하는 경우 서버 쪽 논리를 수행 하는 방법에 각 범주와 관련 된 제품 수를 검색 하는 방법을 탐색 하는 반복기입니다.

이 자습서는 DataList 및 반복기 사용 하 여 마스터/세부 정보 보고서의이 검사를 완료합니다. 자습서의 다음 집합을 편집 및 삭제 기능 DataList 컨트롤을 추가 하는 방법을 설명 합니다.

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Floatutorial](http://css.maxdesign.com.au/floatutorial/) 부동 css의 CSS 요소에 대 한 자습서
- [CSS 위치](http://www.brainjar.com/css/positioning/) css 요소 위치 지정에 대 한 자세한 내용은
- [레이아웃으로 콘텐츠를 HTML](http://www.w3schools.com/html/html_layout.asp) 를 사용 하 여 `<table>` s 및 위치 지정에 대 한 다른 HTML 요소

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Zack jones 이면 특정 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-filtering-acess-two-pages-datalist-cs.md)
> [다음](master-detail-filtering-with-a-dropdownlist-datalist-vb.md)
