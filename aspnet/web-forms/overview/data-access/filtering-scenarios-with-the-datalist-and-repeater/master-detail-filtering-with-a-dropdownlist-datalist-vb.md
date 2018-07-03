---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
title: 마스터/세부 정보 필터링 (VB) DropDownList 한 개로 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 단일 웹 페이지 'master' 레코드 및 DataList displ 표시할 Dropdownlist를 사용 하 여 마스터/세부 정보 보고서를 표시 하는 방법을 표시 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/18/2007
ms.topic: article
ms.assetid: ad0f1014-1eff-465f-bdc6-93058de00e44
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: e58448da80f1024c2007e23b07c9a1f676ab0980
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37377349"
---
<a name="masterdetail-filtering-with-a-dropdownlist-vb"></a>마스터/세부 정보 (VB) DropDownList 한 개로 필터링
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_VB.exe) 또는 [PDF 다운로드](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/datatutorial33vb1.pdf)

> 이 자습서 Dropdownlist를 사용 하 여 "마스터" 레코드와 "정보"를 표시 하는 DataList 표시 하려면 단일 웹 페이지에서 마스터/세부 정보 보고서를 표시 하는 방법을 볼 수 있습니다.


## <a name="introduction"></a>소개

마스터/세부 정보 보고서를 먼저 GridView를 사용 하 여 이전에 만든 [마스터/세부 정보 필터링으로 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) 일부 "마스터" 레코드 집합을 표시 하 여 자습서를 시작 합니다. 사용자를 살펴볼 수 아래로 마스터 레코드 중 하나 있으므로 해당 마스터 레코드의 세부 정보를 "." 보기 마스터/세부 정보 보고서는 이상적인에 일 대 다 관계를 시각화 하 고 (많은 열 임)는 특히 "와이드" 테이블에서 자세한 정보를 표시 합니다. 이전 자습서에서 GridView 및 DetailsView 컨트롤을 사용 하 여 마스터/세부 정보 보고서를 구현 하는 방법을 살펴보았습니다. 이 자습서에는 다음 두 DataList를 사용 하 여 포커스가 있지만 이러한 개념을 판별 됩니다 것 및 반복기 대신 제어 합니다.

이 자습서에서는 DropDownList를 사용 하 여 DataList에서 표시 되는 "details" 레코드를 사용 하 여 "마스터" 레코드를 포함 하는 방법을 살펴보겠습니다.

## <a name="step-1-adding-the-masterdetail-tutorial-web-pages"></a>1 단계: 마스터/세부 자습서 웹 페이지 추가

이 자습서를 시작 하기 전에 먼저 살펴보겠습니다 폴더와이 자습서에는 다음 두 DataList 및 반복기 컨트롤을 사용 하 여 마스터/세부 정보 보고서를 사용 하 여 처리 해야 하는 ASP.NET 페이지를 추가 합니다. 이라는 프로젝트에 새 폴더를 만들어 시작 `DataListRepeaterFiltering`합니다. 다음으로 마스터 페이지를 사용 하도록 구성 된 모든 것이 폴더에 다음 5 개의 ASP.NET 페이지를 추가 `Site.master`:

- `Default.aspx`
- `FilterByDropDownList.aspx`
- `CategoryListMaster.aspx`
- `ProductsForCategoryDetails.aspx`
- `CategoriesAndProducts.aspx`


![DataListRepeaterFiltering 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image1.png)

**그림 1**: 만들기는 `DataListRepeaterFiltering` 폴더 및 자습서 ASP.NET 페이지 추가


을 엽니다는 `Default.aspx` 끌어서 페이지를 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `UserControls` 디자인 화면으로 폴더입니다. 만든이 사용자 정의 컨트롤을 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-vb.md) 자습서에서는 사이트 맵을 열거 하 고 글머리 기호 목록에 현재 섹션의 자습서를 표시 합니다.


[![Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image2.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 `Default.aspx` ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image4.png))


글머리 기호 목록을 표시 하기 위해 우리가 만들 것을 마스터/세부 자습서 해야 사이트 맵을 추가 합니다. 열기는 `Web.sitemap` 파일과 "표시 데이터와 the DataList 및 Repeater" 사이트 맵 노드 태그 뒤에 다음 태그를 추가 합니다.

[!code-xml[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample1.xml)]


![사이트 맵을 업데이트 하 여 새 ASP.NET 페이지를 포함 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image5.png)

**그림 3**: 사이트 맵을 업데이트 하 여 새 ASP.NET 페이지를 포함 합니다.


## <a name="step-2-displaying-the-categories-in-a-dropdownlist"></a>2 단계: DropDownList에 범주를 표시합니다.

마스터/세부 정보 보고서는 선택한 목록 항목의 제품이 표시를 사용 하 여 DropDownList, 범주 표시 페이지 DataList에서 더 아래쪽 합니다. 첫 번째 작업을 미리 한는 DropDownList에 표시 되는 범주를 것입니다. 열어서 시작 합니다 `FilterByDropDownList.aspx` 페이지에 `DataListRepeaterFiltering` 폴더 및 페이지의 디자이너 도구 상자에서 끌어서 DropDownList. 다음으로 DropDownList를 설정 `ID` 속성을 `Categories`입니다. DropDownList의 스마트 태그의 데이터 소스 선택 링크를 클릭 하 고 라는 새로운 ObjectDataSource는 만들 `CategoriesDataSource`합니다.


[![CategoriesDataSource 라는 새 ObjectDataSource를 추가 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image6.png)

**그림 4**: 새 ObjectDataSource 라는 추가 `CategoriesDataSource` ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image8.png))


호출 되도록 새 ObjectDataSource를 구성 합니다 `CategoriesBLL` 클래스의 `GetCategories()` 메서드. DropDownList에 어떤 데이터 원본 필드를 표시 해야 하 고는 지정 해야 하는 ObjectDataSource를 구성한 후 각 목록 항목에 대 한 값으로 연결 해야 하나입니다. 있어야 합니다 `CategoryName` 필드를 표시 및 `CategoryID` 각 목록 항목에 대 한 값으로.


[![가 DropDownList 표시를 사용 하 여 CategoryID와 CategoryName 필드 값](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image9.png)

**그림 5**: DropDownList을 표시 합니다 `CategoryName` 필드 및 사용 `CategoryID` 값으로 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image11.png))


이 시점에서 레코드를 사용 하 여 채워지는 DropDownList 컨트롤이 있습니다를 `Categories` 테이블 (모두 약 6 초 후에 수행). 그림 6 브라우저를 통해 볼 때 지금 진행 상황을 보여줍니다.


[![현재 범주를 나열 하는 드롭다운](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image12.png)

**그림 6**:는 드롭다운 목록이 현재 범주 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image14.png))


## <a name="step-2-adding-the-products-datalist"></a>2 단계: 추가 제품 DataList

마스터/세부 정보 보고서의 마지막 단계는 선택한 범주와 관련 된 제품을 나열 하는 것입니다. 이렇게 하려면 페이지로 DataList를 추가 하 고 라는 새로운 ObjectDataSource는 만들 `ProductsByCategoryDataSource`합니다. 가 합니다 `ProductsByCategoryDataSource` 컨트롤에서 해당 데이터를 검색 합니다 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드. 이 마스터/세부 정보 보고서 읽기 전용 이므로 INSERT, UPDATE 및 DELETE 탭 옵션 (없음)을 선택 합니다.


[![GetProductsByCategoryID(categoryID) 메서드를 선택 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image15.png)

**그림 7**: 선택 된 `GetProductsByCategoryID(categoryID)` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image17.png))


다음을 클릭 한 후 ObjectDataSource 마법사 요청에 대 한 값의 출처를 `GetProductsByCategoryID(categoryID)` 메서드의 *`categoryID`* 매개 변수입니다. 선택한 값을 사용 하도록 `categories` DropDownList 항목으로 매개 변수 원본 컨트롤과를 ControlID `Categories`합니다.


[![CategoryID 매개 변수 범주 DropDownList의 값으로 설정](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image18.png)

**그림 8**: 설정 합니다 *`categoryID`* 매개 변수 값으로는 `Categories` DropDownList ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image20.png))


Visual Studio에서 자동으로 데이터 소스 구성 마법사를 완료 하면 생성 된 `ItemTemplate` 이름과 각 데이터 필드의 값을 표시 하는 DataList에 대 한 합니다. 대신 사용 하 여 DataList를 개선해 보겠습니다를 `ItemTemplate` 제품의 이름, 범주, 공급자, 단위 및 함께 가격 당 수량만을 표시 하는 `SeparatorTemplate` 삽입 하는 `<hr>` 각 항목 사이 요소입니다. 사용 하려는 `ItemTemplate` 에서 예제로는 [DataList 및 반복기 컨트롤을 사용 하 여 데이터 표시](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb.md) 자습서에서는 있지만 자유롭게 가장 좋고 찾아야는 어떤 템플릿 태그를 사용 합니다.

다음과 같이 변경한 후에 DataList 및 해당 ObjectDataSource의 태그가 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample2.aspx)]

시간을 내어 브라우저에서 진행 상황을 확인 합니다. 페이지를 처음 방문 하는 경우 (음료) 선택한 범주에 속하는 제품 같이 표시 됩니다 (그림 9에서), 있지만 DropDownList 변경 데이터를 업데이트 하지 않습니다. 즉, DataList 업데이트에 대 한 포스트백을 발생 해야 합니다. DropDownList의 설정에 이렇게 수행할 수 있습니다 `AutoPostBack` 속성을 `true` 또는 페이지에 단추 웹 컨트롤을 추가 합니다. DropDownList의 설정에 여러분도이 자습서용 `AutoPostBack` 속성을 `true`입니다.

그림 9와 10 중인 마스터/세부 정보 보고서를 보여 줍니다.


[![먼저 페이지를 방문 하 고, 음료 제품 표시 됩니다.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image21.png)

**그림 9**: 먼저 페이지를 방문 하 고, 음료 제품 표시 됩니다 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image23.png))


[![새 제품 (생성)을 선택 하면 자동으로 포스트백, DataList를 업데이트 하는 중](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image24.png)

**그림 10**: 새 제품 (생성)을 선택 하면 자동으로 포스트백, DataList를 업데이트 하는 중 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image26.png))


## <a name="adding-a----choose-a-category----list-item"></a>"-범주-" 선택 목록 항목 추가

먼저 방문할 때는 `FilterByDropDownList.aspx` DropDownList의 첫 번째 목록 항목 (음료)는 선택, 기본적으로 DataList에서 음료 제품을 보여 주는 범주 페이지입니다. 에 *마스터/세부 정보 필터링으로 DropDownList* "-범주 선택-" 옵션을 기본적으로 선택을 선택 하면 표시 DropDownList에 추가한 자습서 *모든* 의 데이터베이스에서 제품입니다. 이러한 접근 방식을 처럼 관리할 수는 GridView에 제품을 나열 하는 경우 각 제품 행 적은 양의 화면 공간을 차지 합니다. 그러나 DataList를 사용 하 여 각 제품 정보가 훨씬 큰 청크의 화면을 사용합니다. 여전히 보겠습니다 "-범주 선택-" 옵션을 추가 및 기본적으로 선택 게 이지만 모든 제품을 표시 하는 대신 옵션을 선택 하면 보겠습니다 구성할 제품이 없습니다. 표시 되도록 합니다.

DropDownList에 새 목록 항목을 추가 하려면 속성 창으로 이동 하 고에서 줄임표를 클릭 합니다 `Items` 속성입니다. 사용 하 여 새 목록 항목을 추가 합니다 `Text` "-범주 선택-" 및 `Value` `0`합니다.


![추가](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image27.png)

**그림 11**: "-범주-" 선택 목록 항목 추가


또는 드롭다운 목록에 다음 태그를 추가 하 여 목록 항목을 추가할 수 있습니다.

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample3.aspx)]

또한 DropDownList 컨트롤을 설정 해야 `AppendDataBoundItems` 하 `true` 때문에로 설정 된 경우 `false` (기본값), 수동으로 추가 된 목록을 덮어씁니다 ObjectDataSource의 범주 DropDownList에 바인딩된 경우 항목입니다.


![AppendDataBoundItems 속성도 True로 설정](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image28.png)

**그림 12**: 설정의 `AppendDataBoundItems` 속성을 true로


값 선택 이유 `0` "-범주 선택-" 목록에 대 한 항목은에 있기 때문에 없는 범주 값을 사용 하 여 시스템 `0`, "-범주-" 선택 목록 항목이 선택 될 때 제품 레코드가 반환 될 따라서 합니다. 이 확인 하려면 잠시 브라우저를 통해 페이지를 방문 합니다. 와 같이 그림 13, 처음에 페이지를 보고 "-범주-" 선택 목록 항목을 선택 하면 제품이 표시 됩니다.


[![경우는](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image29.png)

**그림 13**: 아니요 제품이 표시 되는 "-범주-" 선택 목록 항목을 선택 하면 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image31.png))


대신 표시 하는 경우 *모든* 제품 "-범주 선택-" 옵션을 선택 하면 값이 사용 됩니다. `-1` 대신 합니다. 예리한 독자는 다시 기억 하겠지만 합니다 *마스터/세부 정보 필터링으로 DropDownList* 업데이트 하는 자습서를 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드 있도록 경우를 *`categoryID`* 값 `-1` 레코드가 반환 된 모든 제품에 전달 되었습니다.

## <a name="summary"></a>요약

계층적으로 관련 데이터를 표시할 때 종종 사용자 계층의 최상위에서 데이터를 읽는 데 시작 하 고 세부 정보로 드릴 다운 하는 마스터/세부 정보 보고서를 사용 하 여 데이터를 제공할 수 있습니다. 이 자습서에서는 선택한 범주의 제품을 표시 하는 간단한 마스터/세부 정보 보고서 작성을 검사 합니다. 이 작업은 범주 및 선택한 범주에 속하는 제품 DataList 목록은 DropDownList를 사용 하 여 수행 되었습니다.

다음 자습서 두 페이지에 걸쳐 마스터 및 세부 정보 레코드를 구분 하는 방법을 살펴보겠습니다. 첫 번째 페이지에서 "마스터" 레코드 목록을 표시할 세부 정보를 보려면 링크를 사용 하 여 합니다. 링크를 클릭 하면 선택한 마스터 레코드의 세부 정보를 표시 하는 두 번째 페이지로 whisk 됩니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사 하는 중...

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Randy Schmidt 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
> [다음](master-detail-filtering-acess-two-pages-datalist-vb.md)
