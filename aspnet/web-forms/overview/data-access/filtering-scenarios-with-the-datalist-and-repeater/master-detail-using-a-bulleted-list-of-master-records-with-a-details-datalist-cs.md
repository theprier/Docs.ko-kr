---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs
title: 마스터/세부 정보 (C#) 세부 정보 DataList와 함께 마스터 레코드의 글머리 기호 목록을 사용 하 여 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서 압축할 이전 자습서의 2 페이지 분량 마스터/세부 정보 보고서를 단일 페이지에 t에 범주 이름 글머리 기호 목록을 표시 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2006
ms.topic: article
ms.assetid: c727bb73-7b59-41a1-8dc3-623c6d69e7c2
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 52fd8d1f04b3082250d369b30b5be4db8eac738a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370408"
---
<a name="masterdetail-using-a-bulleted-list-of-master-records-with-a-details-datalist-c"></a>마스터/세부 정보 (C#) 세부 정보 DataList와 함께 마스터 레코드의 글머리 기호 목록을 사용 하 여
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_35_CS.exe) 또는 [PDF 다운로드](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/datatutorial35cs1.pdf)

> 이 자습서에서 압축할 이전 자습서의 2 페이지 분량 마스터/세부 정보 보고서를 단일 페이지에 화면 및 화면 오른쪽에는 선택한 범주 제품의 좌 변에 범주 이름의 글머리 기호 목록을 표시 합니다.


## <a name="introduction"></a>소개

에 [이전 자습서](master-detail-filtering-acess-two-pages-datalist-cs.md) 두 페이지에 걸쳐 마스터/세부 정보 보고서를 구분 하는 방법에 살펴보았습니다. 마스터 페이지에서 범주의 글머리 기호 목록을 렌더링 하려면 Repeater 컨트롤을 사용 했습니다. 각 범주 이름은 된 하이퍼링크,를 클릭 하면는 take 2 열 DataList 해당 제품을 표시 하는 위치, 세부 정보 페이지로 사용자 범주에 속하는 선택 합니다.

이 자습서에서는 압축할 두 페이지 자습서는 단일 페이지에 LinkButton으로 렌더링 되는 각 범주 이름의 범주 이름의 글머리 기호 목록 화면 왼쪽에 표시 합니다. Linkbutton 범주 이름 중 하나를 클릭 포스트백을 유도 하 고 화면 오른쪽에 열이 두 DataList를 선택한 범주의 제품을 바인딩합니다. 왼쪽 반복기 각 s 범주 이름을 표시 하는 것 외에도 지정된 된 범주에 있는 총 제품 있습니다 수를 보여 (그림 1 참조).


[![이름이 범주와 제품의 총 수는 왼쪽에 표시 됩니다.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image2.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image1.png)

**그림 1**:의 범주 이름 및 제품의 총 수는 왼쪽에 표시 됩니다 ([큰 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image3.png))


## <a name="step-1-displaying-a-repeater-in-the-left-portion-of-the-screen"></a>1 단계: Repeater를 화면의 왼쪽된 부분에 표시

이 자습서에 대 한 글머리 기호 목록이 있으면 범주는 선택한 범주의 제품의 왼쪽에 표시 해야 합니다. 표준 HTML 요소 단락 태그를 줄 바꿈하지 않는 공백을 사용 하 여 웹 페이지 내에서 콘텐츠를 배치할 수 있습니다 `<table>` 및 등 또는 연계 스타일 시트 (CSS) 기술을 통해. 이 자습서의 모든 지금 사용 했습니다 CSS 기술 위치 지정. 마스터 페이지에 탐색 사용자 인터페이스를 작성 했습니다 합니다 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-cs.md) 자습서를 사용 했습니다 *절대 위치*, 탐색에 대 한 정확한 픽셀 오프셋을 나타내는 목록 및 주요 내용입니다. 또는, 하나의 요소를 오른쪽 이나 왼쪽을 통해 다른 위치로 CSS를 사용할 수 있습니다 *부동*합니다. DataList의 왼쪽에 반복기를 부동으로 선택한 범주의 제품의 왼쪽에 표시 범주 글머리 기호 목록 있다는

엽니다는 `CategoriesAndProducts.aspx` 에서 페이지를 `DataListRepeaterFiltering` 폴더 Repeater 및 DataList 페이지에 추가 합니다. 반복기가 설정 `ID` 하 `Categories` 에 s DataList 및 `CategoryProducts`합니다. 소스 뷰로 이동 하 고 자체 내에서 Repeater 및 DataList 컨트롤을 배치 `<div>` 요소입니다. 즉, 내에서 반복기를 묶습니다를 `<div>` 요소 첫 번째 및 자체에서 DataList 다음 `<div>` Repeater 바로 뒤 요소입니다. 태그가 시점에서 표시 됩니다 다음과 비슷합니다.


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample1.aspx)]

DataList의 왼쪽에 반복기를 float로 사용 해야는 `float` CSS 스타일 특성을 다음과 같이 합니다.


[!code-html[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample2.html)]

합니다 `float: left;` 첫 번째 부동 `<div>` 왼쪽의 두 번째 요소입니다. `width` 및 `padding-right` 설정에 따르면 첫 번째 `<div>` s `width` 여백 사이 추가 하 고는 `<div>`의 요소 내용 및 오른쪽 여백에 해당 합니다. 부동 요소 CSS에 대 한 자세한 내용은 체크 아웃 합니다 [Floatutorial](http://css.maxdesign.com.au/floatutorial/)합니다.

첫 번째를 통해 직접 스타일 설정을 지정 하지 않고 `<p>` 요소 s `style` 특성에서 새로운 CSS 클래스를 대신 만든 `Styles.css` 라는 `FloatLeft`:


[!code-css[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample3.css)]

바꾼 수는 `<div>` 사용 하 여 `<div class="FloatLeft">`입니다.

CSS 클래스를 추가 하 고 태그를 구성한 후의 `CategoriesAndProducts.aspx` 페이지, 디자이너로 이동 합니다. DataList의 왼쪽에 부동 (오른쪽 이제 둘 다 표시 회색 상자 이후로 ve 해당 데이터 원본 또는 템플릿을 구성 하는 대로) 하지만 반복기에 표시 됩니다.


[![DataList의 왼쪽으로 움직이는 반복기](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image5.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image4.png)

**그림 2**: The Repeater DataList의 왼쪽으로 움직이는 ([큰 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image6.png))


## <a name="step-2-determining-the-number-of-products-for-each-category"></a>각 범주에 대 한 제품의 수를 결정 하는 2 단계:

전체 태그를 둘러싸는 Repeater 및 DataList s를 사용 하 여 반복기의 범주 데이터를 바인딩할 준비가 제어 합니다. 그러나 그림 1에는 범주 글머리 기호 목록에서 볼 수 있듯이 각 범주의 이름 외에 해야 범주와 관련 된 제품 수를 표시 합니다. 이 정보에 액세스 하려면 다음이 가능 하거나

- **ASP.NET 페이지의 코드 숨김 클래스에서이 정보를 확인 합니다.** 특정 *`categoryID`* 호출 하 여 연결 된 제품의 수를 확인할 수 있습니다 합니다 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드. 이 메서드가 반환을 `ProductsDataTable` 개체 `Count` 속성을 나타냅니다 개수 `ProductsRow` s가 지정 된 제품의 수 인 *`categoryID`* 합니다. 만들 수 있습니다는 `ItemDataBound` Repeater를 바인딩할 각 범주에 대 한 호출 하는 반복기에 대 한 이벤트 처리기는 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드 출력의 개수를 포함 합니다.
- **업데이트를 `CategoriesDataTable` 포함 하도록 입력 데이터 집합에는 `NumberOfProducts` 열입니다.** 업데이트할 수 있습니다는 `GetCategories()` 의 메서드를 `CategoriesDataTable` 이 정보를 포함 하거나, 또는 `GetCategories()` 으로-이며 새 `CategoriesDataTable` 라는 메서드 `GetCategoriesAndNumberOfProducts()`합니다.

이러한 두 기술 모두를 탐색 하는 s 수 있습니다. 첫 번째 방법은 데이터 액세스 계층을 업데이트 해야 하는 t 하지 것 때문에 구현 하기 쉽습니다. 그러나 데이터베이스를 사용 하 여 자세한 통신 해야합니다. 에 대 한 호출을 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 에서 메서드는 `ItemDataBound` Repeater에 표시 된 각 범주에 대 한 추가 데이터베이스 호출을 추가 하는 이벤트 처리기입니다. 이 기술을 사용 하 여 가지 *N* + 1 데이터베이스 호출, 여기서 *N* Repeater에 표시 되는 범주입니다. 각 범주에 대 한 정보를 사용 하 여 두 번째 방법을 사용 하 여 제품 수가 반환 됩니다 합니다 `CategoriesBLL` s 클래스 `GetCategories()` (또는 `GetCategoriesAndNumberOfProducts()`) 메서드를 사용 하므로 데이터베이스에 한 번만 발생 합니다.

## <a name="determining-the-number-of-products-in-the-itemdatabound-event-handler"></a>ItemDataBound 이벤트 처리기에서 제품의 수를 결정합니다.

반복기가 각 범주에 대 한 제품의 수를 결정 `ItemDataBound` 이벤트 처리기의 기존 데이터 액세스 계층을 수정할 필요가 없습니다. 내에서 직접 모든 수정을 만들 수는 `CategoriesAndProducts.aspx` 페이지입니다. 라는 새 ObjectDataSource를 추가 하 여 시작 `CategoriesDataSource` Repeater가 스마트 태그를 통해. 다음으로 구성 합니다 `CategoriesDataSource` ObjectDataSource는 해당 데이터를 검색 하도록 합니다 `CategoriesBLL` s 클래스 `GetCategories()` 메서드.


[![S GetCategories() 메서드 CategoriesBLL 클래스를 사용 하는 ObjectDataSource 구성](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image8.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image7.png)

**그림 3**: ObjectDataSource를 사용 하 여 구성 합니다 `CategoriesBLL` s 클래스 `GetCategories()` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image9.png))


각 항목에는 `Categories` Repeater를 클릭할 수 고를 클릭 하면 발생 해야 하는 `CategoryProducts` DataList 선택한 범주에 대 한 해당 제품을 전시 하기. 각 범주를이 동일한 페이지에 다시 연결 하 여 하이퍼링크를 만들어이 작업을 수행할 수 있습니다 (`CategoriesAndProducts.aspx`), 하지만 전달 된 `CategoryID` 이전 자습서에서 본 것과 마찬가지로 문자열을 통해. 이 방식의 장점은 특정 범주의 제품을 표시 하는 페이지를 책갈피 및 검색 엔진에 의해 인덱싱된 수는입니다.

또는 최선을 각 범주는 LinkButton는는이 자습서를 사용 하는 방법입니다. LinkButton 하이퍼링크로 사용자가의 브라우저에서 렌더링 하지만 클릭 하면 포스트백을 수행 합니다. 포스트백에서 DataList의 ObjectDataSource 해야 선택한 범주에 속하는 해당 제품을 전시 하기 새로 고쳐져 야 합니다. 이 자습서에서는 LinkButton;를 사용 하 여 보다 자세한 이해를 통해 하이퍼링크를 사용 하 여 그러나 다른 시나리오는 LinkButton을 사용 하 여 더 유리 있을 수 있습니다. 하이퍼링크 접근 방식은이 예제에 대 한 이상적인 것을 하는 동안에 s를 대신 LinkButton을 사용 하 여를 탐색할 수 있습니다. 앞으로 살펴보겠지만, LinkButton을 사용 하 여 하이퍼링크를 사용 하 여 그렇지 않은 경우 발생 하지는 몇 가지 과제를 도입 되었습니다. 따라서 LinkButton을 사용 하 여이 자습서에서는 이러한 문제를 강조 표시를 수 하려는 하이퍼링크 대신 LinkButton을 사용 하 여 이러한 시나리오에 대 한 솔루션을 제공 합니다.

> [!NOTE]
> 하이퍼링크 컨트롤을 사용 하 여이 자습서를 반복 하는 것이 좋습니다 또는 `<a>` LinkButton 대신 요소입니다.


다음 태그에는 Repeater 및 ObjectDataSource에 대 한 선언적 구문을 보여 줍니다. S 템플릿에 LinkButton 표시 된 각 항목을 사용 하 여 글머리 기호 목록을 렌더링 하는 참고:


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample4.aspx)]

> [!NOTE]
> 이 자습서에 대 한 반복기 사용 하도록 설정 하는 해당 뷰 상태의 있어야 합니다 (생략 참고는 `EnableViewState="False"` Repeater가 선언적 구문에서). 3 단계에서는 만듭니다 이벤트 처리기가의 반복기에 대 한 `ItemCommand` 이벤트를 업데이트 합니다 DataList의 ObjectDataSource `SelectParameters` 컬렉션입니다. 반복기가의 `ItemCommand`그러나 보기 상태가 비활성화 되 면 t 실행 성공 합니다. 참조 [는 ASP.NET 질문는 Stumper](http://scottonwriting.net/sowblog/posts/1263.aspx) 및 [자사 솔루션](http://scottonwriting.net/sowBlog/posts/1268.aspx) 이유에 대 한 자세한 내용은 뷰 상태를 Repeater s에 대 한 사용 해야 합니다 `ItemCommand` 이벤트가 발생 합니다.


인 LinkButton 합니다 `ID` 속성 값이 `ViewCategory` 되지 않은 해당 `Text` 속성 집합입니다. 범주 이름을 표시 하려면 바로 원했던 것을 하는 경우는 설정 텍스트 속성 선언적으로 데이터 바인딩 구문을 통해 다음과 같이 합니다.


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample5.aspx)]

S 범주 이름을 표시 하려고 하는 반면 *고* 해당 범주에 속하는 제품의 수입니다. S 반복기에서이 정보를 검색할 수 있습니다 `ItemDataBound` 이벤트 처리기를 호출 하 여는 `ProductBLL` s 클래스 `GetCategoriesByProductID(categoryID)` 메서드와 레코드 개수 결과에 반환 됩니다 결정 `ProductsDataTable`, 다음 코드와 보여 줍니다.


[!code-csharp[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample6.cs)]

먼저 확인 다시 데이터 항목을 사용 했습니다 (하나입니다 `ItemType` 는 `Item` 또는 `AlternatingItem`) 다음을 참조 합니다 `CategoriesRow` 만 현재 바인딩된 인스턴스 `RepeaterItem`합니다. 다음으로의 인스턴스를 만들어이 범주에 대 한 제품의 수를 결정 했습니다 합니다 `ProductsBLL` 클래스를 호출 해당 `GetCategoriesByProductID(categoryID)` 메서드를 사용 하 여 반환 된 레코드의 수를 결정 하는 `Count` 속성입니다. 마지막으로 `ViewCategory` LinkButton ItemTemplate에는 참조 및 해당 `Text` 속성이 *CategoryName* (*NumberOfProductsInCategory*) 여기서  *NumberOfProductsInCategory* 소수 자릿수 0을 사용 하 여 서식이 지정 됩니다.

> [!NOTE]
> 추가한 수 또는 *함수를 서식 지정* s 범주를 허용 하는 ASP.NET 페이지가 코드 숨김 클래스에 `CategoryName` 및 `CategoryID` 값 및 반환는 `CategoryName` 개수를 사용 하 여 연결 범주에는 제품 (호출 하 여 결정 된 대로 `GetCategoriesByProductID(categoryID)` 메서드). LinkButton s에 대 한 필요성을 대체 하는 텍스트 속성에 선언적으로 지정할 수 있습니다 이러한 서식 지정 함수 결과 `ItemDataBound` 이벤트 처리기입니다. 참조를 [GridView 컨트롤에서 TemplateFields 사용 하 여](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) 또는 [DataList 및 반복기 기반으로 데이터 서식 지정](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs.md) 서식 지정 함수를 사용 하 여 자세한 정보에 대 한 자습서입니다.


이 이벤트 처리기를 추가한 후 시간을 내어 브라우저를 통해 페이지를 테스트 합니다. 각 범주의 범주 이름 및 범주와 관련 된 제품의 수를 표시, 글머리 기호 목록에 표시 됩니다 하는 방법 (그림 4 참조).


[![각 이름이 범주와 제품 번호 표시 됩니다.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image11.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image10.png)

**그림 4**: 각 범주 이름 및 제품의 수 표시 됩니다 ([큰 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image12.png))


## <a name="updating-thecategoriesdatatableandcategoriestableadapterto-include-the-number-of-products-for-each-category"></a>업데이트를`CategoriesDataTable`고`CategoriesTableAdapter`각 범주에 대 한 제품 개수를 포함 하려면

하므로 각 범주에 대 한 제품 개수를 확인 하는 대신 s 바인딩할 반복기를 조정 하 여이 프로세스를 간소화할 수 있습니다 것 합니다 `CategoriesDataTable` 및 `CategoriesTableAdapter` 기본적으로이 정보를 포함 하도록 데이터 액세스 계층에서. 이렇게 하려면 새 열을 추가 해야 합니다 `CategoriesDataTable` 관련된 제품의 수를 보유 하 합니다. DataTable에 새 열을 추가할 입력 데이터 집합을 엽니다 (`App_Code\DAL\Northwind.xsd`), 데이터를 수정 하려면 테이블을 마우스 오른쪽 단추로 클릭 하 고 추가 선택 / 열입니다. 새 열을 추가 하 여 `CategoriesDataTable` (그림 5 참조).


[![CategoriesDataSource에 새 열 추가](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image14.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image13.png)

**그림 5**: 새 열을 추가 하는 `CategoriesDataSource` ([클릭 하 여 큰 이미지 보기](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image15.png))


이라는 새 열이 추가 `Column1`, 다른 이름을 입력 하 여 변경할 수 있습니다. 이 새 열 이름 바꾸기 `NumberOfProducts`합니다. 다음으로,이 열의 속성을 구성 해야 합니다. 새 열에서 클릭 하 고 속성 창으로 이동 합니다. S 열 변경 `DataType` 속성을 `System.String` 를 `System.Int32` 설정 합니다 `ReadOnly` 속성을 `True`그림 6 에서처럼 합니다.


![데이터 형식 및 새 열의 읽기 전용 속성을 설정 합니다.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image16.png)

**그림 6**: 설정 된 `DataType` 고 `ReadOnly` 새 열의 속성


하는 동안를 `CategoriesDataTable` 이제는 `NumberOfProducts` 열, 해당 TableAdapter가의 쿼리 중 하나에서 해당 값을 설정 하지 않으면. 업데이트할 수 있습니다는 `GetCategories()` 범주 정보를 검색할 때마다 이러한 정보를 원하는 경우이 정보를 반환 하는 메서드 반환 합니다. 그러나 경우 드문 경우 (예:이 자습서를 위해 간단히) 범주에 대 한 연결 된 제품의 수를 가져오는 하기만 삭제할 수 있습니다. `GetCategories()` 으로-이며이 정보를 반환 하는 새 메서드를 만듭니다. Let s 라는 새 메서드 생성이 두 번째 접근 방식을 사용 `GetCategoriesAndNumberOfProducts()`합니다.

이 새로 추가 하려면 `GetCategoriesAndNumberOfProducts()` 메서드를 마우스 오른쪽 단추로 클릭은 `CategoriesTableAdapter` 새 쿼리를 선택 합니다. 이렇게 하면 TableAdapter 쿼리 구성 마법사, 우리는 여러 번 이전 자습서에서에서 사용한 ve 가동 됩니다. 이 메서드에 대 한 쿼리는 행을 반환 하는 임시 SQL 문을 지정 하 여 마법사를 시작 합니다.


[![임시 SQL 문을 사용 하는 메서드 만들기](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image18.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image17.png)

**그림 7**: 특별 SQL 문을 사용 하 여 메서드를 만듭니다 ([큰 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image19.png))


[![SQL 문이 행을 반환합니다.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image21.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image20.png)

**그림 8**: SQL 문이 반환 행 ([큰 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image22.png))


마법사의 다음 화면을 사용 하 여 쿼리에 대 한 요청입니다. 범주별 s 반환할 `CategoryID`, `CategoryName`, 및 `Description` 필드를 범주에 연관 된 제품 수와 함께 다음 사용 하 여 `SELECT` 문:


[!code-sql[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample7.sql)]


[![사용 하 여 쿼리를 지정 합니다.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image24.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image23.png)

**그림 9**: 쿼리를 사용 하 여 지정 합니다 ([큰 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image25.png))


범주와 관련 된 제품의 수를 계산 하는 하위 쿼리는 별칭이 `NumberOfProducts`합니다. 이 명명 일치 항목으로 인해 연결할이 하위 쿼리에서 반환한 값을 `CategoriesDataTable` s `NumberOfProducts` 열입니다.

이 쿼리를 입력 한 후 마지막 단계는 새 메서드의 이름을 선택 하는 것입니다. 사용 하 여 `FillWithNumberOfProducts` 및 `GetCategoriesAndNumberOfProducts` 채우기 돌아가 DataTable DataTable 패턴, 각각.


[![새 TableAdapter의 메서드 FillWithNumberOfProducts 이름과 GetCategoriesAndNumberOfProducts](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image27.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image26.png)

**그림 10**: 새 tableadapter 메서드 이름을 `FillWithNumberOfProducts` 하 고 `GetCategoriesAndNumberOfProducts` ([클릭 하 여 큰 이미지 보기](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image28.png))


이 시점에서 데이터 액세스 계층 범주별 제품의 수를 포함 하도록 확장 되었습니다. 해당 추가 해야 하므로 모든 프레젠테이션 계층에는 dal과 별도 비즈니스 논리 레이어를 통해 모든 호출을 라우팅합니다 `GetCategoriesAndNumberOfProducts` 메서드는 `CategoriesBLL` 클래스:


[!code-csharp[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample8.cs)]

DAL 및 완료 하는 BLL을 사용 하 여 다시에서는 준비 된이 데이터를 바인딩하는 `Categories` 반복기에서 `CategoriesAndProducts.aspx`! 적 만들지 않은 경우 ObjectDataSource에서 확인 된 반복기에 대 한 수의 제품에는 `ItemDataBound` 이 ObjectDataSource를 삭제 하 고 s Repeater를 제거 하는 이벤트 처리기 섹션이 `DataSourceID` 속성 무선의 자유도 설정이 Repeater s `ItemDataBound` 제거 하 여 이벤트 처리기에서 이벤트를 `Handles Categories.OnItemDataBound` ASP.NET 코드 숨김 클래스에는 구문입니다.

원래 상태의 Repeater를 사용 하 여 추가 라는 새로운 ObjectDataSource는 `CategoriesDataSource` Repeater가 스마트 태그를 통해. ObjectDataSource 사용 하도록 구성 합니다 `CategoriesBLL` 클래스를 사용 하는 대신 합니다 `GetCategories()` 메서드를 사용 했습니다 `GetCategoriesAndNumberOfProducts()` 대신 (그림 11 참조).


[![GetCategoriesAndNumberOfProducts 메서드를 사용 하는 ObjectDataSource 구성](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image30.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image29.png)

**그림 11**: ObjectDataSource 사용 하도록 구성 된 `GetCategoriesAndNumberOfProducts` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image31.png))


다음으로 업데이트 하는 `ItemTemplate` 있도록 LinkButton s `Text` 속성이 데이터 바인딩 구문을 사용 하 여 선언적으로 할당 되었고이 모두 포함 합니다 `CategoryName` 및 `NumberOfProducts` 데이터 필드. 반복기에 대 한 전체 선언적 태그 및 `CategoriesDataSource` ObjectDataSource 따릅니다.


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample9.aspx)]

DAL 포함 하도록 업데이트 하 여 렌더링 된 출력을 `NumberOfProducts` 를 사용 하 여 같은 열이를 `ItemDataBound` 이벤트 처리기 방법 (그림 4는 화면을 다시 참조 범주 이름 및 제품의 수를 보여 주는 Repeater 샷).

## <a name="step-3-displaying-the-selected-category-s-products"></a>3 단계: 선택한 범주의 제품 표시

이때 했습니다는 `Categories` 각 범주에서 제품 수와 함께 범주의 목록을 표시 하는 반복기입니다. 를 클릭 하면는 포스트백을 발생 지점에서는 각 범주에 대 한 반복기에서는 LinkButton에서 선택한 범주에 대 한 해당 제품을 표시 해야 하는 `CategoryProducts` DataList 합니다.

우리를 연결 하는 한 가지 문제를 사용 하면 선택한 범주에 대 한 제품만 표시 DataList 할 방법이 있습니다. 에 [마스터/세부 정보 DetailsView를 사용 하 여 선택 가능한 마스터 GridView를 사용 하 여 세부 정보](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) 행이 있는 GridView를 빌드하는 방법에 살펴보았습니다 자습서를 선택할 수 없습니다, 선택 된 행으로 s 정보 같은 페이지에 DetailsView에 표시 되 고 합니다. GridView의 ObjectDataSource를 사용 하 여 모든 제품에 대 한 정보를 반환 합니다는 `ProductsBLL` s `GetProducts()` 사용 하 여 선택한 제품에 대 한 정보를 검색 하는 동안 DetailsView의 ObjectDataSource 메서드는 `GetProductsByProductID(productID)` 메서드. 합니다 *`productID`* GridView s의 값을 사용 하 여 연결 하 여 선언적으로 제공 된 매개 변수 값 `SelectedValue` 속성입니다. 그러나 반복기 없는 `SelectedValue` 속성 및 매개 변수 원본으로 사용할 수 없습니다.

> [!NOTE]
> Repeater에 LinkButton을 사용 하는 경우 표시 되는 이러한 과제 중 하나입니다. 에서는 사용한 하이퍼링크에 전달 하는 `CategoryID` querystring을 통해 대신에서는 수 QueryString 필드 원본으로 사용할 매개 변수 s 값입니다.


부족이 지 걱정 되기 전에 `SelectedValue` 는 반복기에 대 한 속성에는 하지만 먼저 DataList ObjectDataSource에 바인딩하고 지정 s 수 있도록 해당 `ItemTemplate`합니다.

DataList s 스마트 태그에서 이라는 새 ObjectDataSource를 추가 하도록 선택할 `CategoryProductsDataSource` 를 사용 하도록 구성 합니다 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드. 이 자습서에서는 DataList 읽기 전용 인터페이스를 제공 하므로 자유롭게는 insert, UPDATE, 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제 합니다.


[![ProductsBLL 클래스의 GetProductsByCategoryID(categoryID) 메서드를 사용 하는 ObjectDataSource 구성](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image33.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image32.png)

**그림 12**: 구성 사용 하 여 ObjectDataSource `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image34.png))


있으므로 합니다 `GetProductsByCategoryID(categoryID)` 메서드에서 입력된 매개 변수를 예상 (*`categoryID`*), 데이터 소스 구성 마법사를 사용 하면 매개 변수의 소스를 지정할 수 있도록 합니다. GridView 또는 DataList에 나열 된 범주를 d 설정 매개 변수 원본 드롭다운 목록 컨트롤에 대 한 ControlID를는 `ID` 데이터 웹 컨트롤입니다. Repeater에 있지만 이후에 `SelectedValue` 속성 매개 변수 원본으로 사용할 수 없습니다. 를 확인 하는 경우 있습니다 ControlID 드롭다운 목록 컨트롤을 하나씩만 포함 되어 있는지 `ID``CategoryProducts`, `ID` DataList입니다.

이제 매개 변수 원본 드롭 다운 목록 None으로 설정 합니다. 우리가 최종적으로 프로그래밍 방식으로 범주 반복기에서 LinkButton을 클릭할 때이 매개 변수 값을 할당 합니다.


[![매개 변수 원본에 대 한 categoryID 매개 변수를 지정 하지 않습니다](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image36.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image35.png)

**그림 13**:에 대 한 매개 변수 소스를 지정 하지 않으면 합니다 *`categoryID`* 매개 변수 ([클릭 하 여 큰 이미지 보기](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image37.png))


데이터 소스 구성 마법사를 완료 한 후 Visual Studio 자동으로 생성 DataList의 `ItemTemplate`입니다. 이 기본값을 바꿉니다 `ItemTemplate` 템플릿을 사용 하 여 이전 자습서에서 사용 되는 것,이 또한 s DataList를 설정 `RepeatColumns` 속성을 2로 합니다. 이러한 변경을 수행한 후에 DataList 및 해당 관련된 ObjectDataSource의 선언 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample10.aspx)]

현재는 `CategoryProductsDataSource` ObjectDataSource s *`categoryID`* 매개 변수가 설정 되지 않은, 제품이 없습니다. 페이지를 볼 때 표시 됩니다. 위해 필요한 것은이 매개 변수 값 설정에 따라는 `CategoryID` 반복기 범주의 클릭 합니다. 이 두 가지 과제가: 먼저 하는 방법을 결정 하지 경우 반복기가 LinkButton `ItemTemplate` ; 클릭 하 여 두 번째에서는 확인할 수는 `CategoryID` 인 LinkButton이 클릭 되었습니다 해당 범주의?

단추 및 ImageButton 컨트롤 같은 LinkButton에는 `Click` 이벤트와 [ `Command` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.command.aspx)합니다. `Click` 이벤트는 단순히 LinkButton 클릭 했는지를 확인 하도록 설계 되었습니다. 그러나 때때로 LinkButton 클릭 했는지를 확인 하는 것 외에도 또한 해야 이벤트 처리기에 몇 가지 추가 정보를 전달 합니다. LinkButton의 경우 이것이 [ `CommandName` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandname.aspx) 하 고 [ `CommandArgument` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandargument.aspx) 속성이 추가 정보를 할당할 수 있습니다. LinkButton 클릭 하면 다음 해당 `Command` 이벤트가 발생 (대신 해당 `Click` 이벤트) 및 이벤트 처리기의 값을 전달 되는 `CommandName` 및 `CommandArgument` 속성.

경우는 `Command` Repeater가 반복기를 템플릿 내에서 이벤트를 발생 [ `ItemCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeater.itemcommand.aspx) 발생 하 고 전달 되는 `CommandName` 및 `CommandArgument` 클릭할된 LinkButton의 값 (또는 단추 또는 ImageButton)입니다. 따라서 경우 범주 반복기에서 LinkButton 클릭 했는지를 확인 하려면 해야 다음 작업을 수행 합니다.

1. 설정 합니다 `CommandName` LinkButton s 반복기에서의 속성 `ItemTemplate` 일부 값 (I ListProducts을 사용한 적). 이 설정 하 여 `CommandName` 값을 LinkButton의 `Command` LinkButton을 클릭할 때 이벤트가 발생 합니다.
2. 집합 LinkButton s `CommandArgument` 속성을 현재 항목 s의 값 `CategoryID`합니다.
3. S 반복기에 대 한 이벤트 처리기를 만들고 `ItemCommand` 이벤트입니다. 이벤트 처리기를 설정 합니다 `CategoryProductsDataSource` ObjectDataSource s `CategoryID` 매개 변수 값의 전달 기능 `CommandArgument`합니다.

다음 `ItemTemplate` 범주 반복기에 대 한 태그 1 및 2 단계를 구현 합니다. 참고 하는 방법을 `CommandArgument` 값은 s 데이터 항목을 할당 `CategoryID` 데이터 바인딩 구문을 사용 하 여:


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample11.aspx)]

만들 때마다를 `ItemCommand` 이벤트 처리기를 항상 먼저 들어오는 확인 하는 것이 바람직합니다 `CommandName` 때문에 값 *든* `Command` 이벤트에 의해 발생 *모든* 단추, LinkButton, 또는 Repeater 내에서 ImageButton 하면는 `ItemCommand` 이벤트가 발생 합니다. 있지만 현재만 이러한 LinkButton 하나 지금, 나중에 것 (또는 팀의 다른 개발자) 수 추가 단추 웹 컨트롤을 추가 Repeater를 클릭 하면 발생 동일한 `ItemCommand` 이벤트 처리기입니다. 따라서이 항상 확인 해야 하는 최선의 s는 `CommandName` 속성 예상 값에 일치 하는 경우만 프로그래밍 논리를 진행 합니다.

전달-에서 확인 한 후 `CommandName` 값이 ListProducts 이면 이벤트 처리기를 할당 합니다 `CategoryProductsDataSource` ObjectDataSource s `CategoryID` 매개 변수 값의 전달 기능 `CommandArgument`합니다. ObjectDataSource가이 수정 `SelectParameters` 자체 새로 선택한 범주의 제품을 보여 주는 데이터 원본에 바인딩할 DataList를 자동으로 발생 합니다.


[!code-csharp[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample12.cs)]

이러한 추가 기능을 사용 하 여 자습서 완료 되었습니다! 브라우저에서 테스트에 대해 잠시 설명. 그림 14에서는 먼저 페이지를 방문할 때 화면을 보여 줍니다. 범주를 선택 해야 아직에 있으므로 제품이 표시 됩니다. 생성, 같은 범주를 클릭 하면 해당 제품 2 열 뷰에서 제품 범주에 표시 됩니다 (그림 15 참조).


[![제품이 표시 되는 경우 첫 번째 페이지를 방문 하는](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image39.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image38.png)

**그림 14**: 아니요 제품 표시 되는 경우 첫 번째 페이지를 방문 하는 ([큰 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image40.png))


[![생성 범주 목록이 일치 하는 제품 오른쪽을 클릭합니다.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image42.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image41.png)

**그림 15**: 오른쪽에 일치 하는 제품을 나열 생성 범주를 클릭 하면 ([큰 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image43.png))


## <a name="summary"></a>요약

이 자습서에서 이전에 살펴본 것 처럼 마스터/세부 정보 보고서는 두 페이지에 걸쳐 분산 될 수 있습니다 또는 하나에 통합 합니다. 하지만 마스터 레이아웃 페이지의 세부 정보 레코드를 몇 가지 과제는 방법에 가장을 소개 단일 페이지에는 마스터/세부 정보 보고서를 표시 합니다. 에 *마스터/세부 정보 DetailsView를 사용 하 여 선택 가능한 마스터 GridView를 사용 하 여 세부 정보* 했습니다. 세부 정보 레코드 마스터 레코드 위에 표시 하는이 자습서에서는 데 CSS 기술을 마스터 레코드 float가 자습서는 왼쪽 세부 정보입니다.

마스터/세부 정보 보고서를 표시 하는 함께 했습니다. 내에서 클릭할는 LinkButton (단추 또는 ImageButton) 하는 경우 서버 쪽 논리를 수행 하는 방법으로 각 범주와 관련 된 제품의 수를 검색 하는 방법을 탐색할 수 있는 기회를 반복기입니다.

이 자습서는 DataList 및 반복기를 사용 하 여 마스터/세부 정보 보고서는 검사를 완료합니다. 자습서의 다음 집합에서는 편집 및 삭제 기능 DataList 컨트롤을 추가 하는 방법을 설명 합니다.

즐거운 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Floatutorial](http://css.maxdesign.com.au/floatutorial/) 부동 CSS 사용 하 여 CSS 요소에 대 한 자습서
- [CSS 위치 설정을](http://www.brainjar.com/css/positioning/) CSS 사용 하 여 요소를 배치 하는 방법은
- [레이아웃 아웃 콘텐츠를 HTML](http://www.w3schools.com/html/html_layout.asp) 를 사용 하 여 `<table>` s 및 기타 HTML 요소 위치 지정

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Zack Jones 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-filtering-acess-two-pages-datalist-cs.md)
> [다음](master-detail-filtering-with-a-dropdownlist-datalist-vb.md)
