---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
title: "마스터/세부 DropDownList (VB)를 사용 하 여 필터링 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 displ 하려면 'master' 레코드와 DataList를 표시 하려면 dropdownlist 활용을 사용 하 여 단일 웹 페이지에서 마스터/세부 보고서를 표시 하는 방법을 표시 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/18/2007
ms.topic: article
ms.assetid: ad0f1014-1eff-465f-bdc6-93058de00e44
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 1f480cfcfb3b02c9398b2db3e66cec432152a05d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="masterdetail-filtering-with-a-dropdownlist-vb"></a>마스터/세부 DropDownList (VB)를 사용 하 여 필터링
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_VB.exe) 또는 [PDF 다운로드](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/datatutorial33vb1.pdf)

> 이 자습서에서는 dropdownlist 활용을 사용 하 여 "마스터" 레코드와 "정보"를 표시 하려면 DataList 표시 하려면 단일 웹 페이지에서 마스터/세부 보고서를 표시 하는 방법을 알아봅니다.


## <a name="introduction"></a>소개

마스터/세부 정보 보고서에는 먼저는 GridView를 사용 하 여 이전에 만든 [마스터/세부 정보 필터링 된 정도 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) 자습서에서는 몇 가지 "마스터" 레코드 집합을 표시 하 여 시작 합니다. 사용자는 다음으로 드릴 다운할 수 마스터 레코드 중 하나 함으로써 해당 마스터 레코드의 세부 정보를 "." 보기 마스터/세부 정보 보고서는 일 대 다 관계를 시각화 하 고 (더 많은 열이 있는)는 특히 "와이드" 테이블에서 자세한 정보를 표시 하는 것에 대 한 적합 한 버전입니다. 이전 자습서에서 GridView 및 DetailsView 컨트롤을 사용 하 여 마스터/세부 보고서를 구현 하는 방법에서 살펴본 했습니다. 이 자습서에는 다음 두 DataList를 사용 하 여에 집중 되지만 이러한 개념을 다시 검사할 수 우리 및 반복기 대신 제어 합니다.

이 자습서에서는 DropDownList를 사용 하 여 DataList에 표시 된 "details" 레코드 "마스터" 레코드를 포함 하는 방법을 살펴보겠습니다.

## <a name="step-1-adding-the-masterdetail-tutorial-web-pages"></a>1 단계: 마스터/세부 자습서 웹 페이지 추가

이 자습서를 시작 하기 전에 먼저 간단히 살펴보겠습니다 폴더와이 자습서와 다음 두 DataList 및 반복기 제어를 사용 하 여 마스터/세부 보고서 처리에 대 한 사용 해야 하는 ASP.NET 페이지를 추가 합니다. 시작 이라는 프로젝트에 새 폴더를 만들어서 `DataListRepeaterFiltering`합니다. 다음으로 마스터 페이지를 사용 하도록 구성 된 모두이 폴더에 다음과 같은 5 개의 ASP.NET 페이지를 추가 `Site.master`:

- `Default.aspx`
- `FilterByDropDownList.aspx`
- `CategoryListMaster.aspx`
- `ProductsForCategoryDetails.aspx`
- `CategoriesAndProducts.aspx`


![DataListRepeaterFiltering 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image1.png)

**그림 1**: 만들기는 `DataListRepeaterFiltering` 폴더 자습서 ASP.NET 페이지를 추가 합니다.


을 열고는 `Default.aspx` 끌어서 페이지는 `SectionLevelTutorialListing.ascx` 에서 사용자 정의 컨트롤의 `UserControls` 디자인 화면으로 폴더입니다. 만든이 사용자 정의 컨트롤의 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-vb.md) 자습서에서는 사이트 맵을 열거 하 고 글머리 기호 목록에서 현재 섹션의 자습서를 표시 합니다.


[![Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image2.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image4.png))


글머리 기호 목록을 표시 하기 위해 म 만들게 됩니다, 마스터/세부 자습서 해야 사이트 맵에 추가 합니다. 열기는 `Web.sitemap` 파일을 "표시 데이터와 the DataList 및 반복기" 사이트 맵 노드 태그 뒤에 다음 태그를 추가 합니다.

[!code-xml[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample1.xml)]


![새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image5.png)

**그림 3**: 새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트


## <a name="step-2-displaying-the-categories-in-a-dropdownlist"></a>2 단계: DropDownList에 범주를 표시합니다.

마스터/세부 정보 보고서는 선택한 목록 항목의 제품이 표시와 DropDownList에서 범주별 나열 됩니다 아래로 DataList의 페이지에 추가 합니다. 그런 다음 미리 us, 첫 번째 작업 범주 DropDownList에 표시 되는 것입니다. 열어 시작는 `FilterByDropDownList.aspx` 페이지에 `DataListRepeaterFiltering` 폴더와 페이지의 디자이너 도구 상자에서 끌어서 DropDownList 합니다. 다음으로 DropDownList 설정 `ID` 속성을 `Categories`합니다. DropDownList의 스마트 태그에서 데이터 소스 선택 링크를 클릭 하 고 라는 새 ObjectDataSource 만들 `CategoriesDataSource`합니다.


[![CategoriesDataSource 라는 새 ObjectDataSource를 추가 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image6.png)

**그림 4**: 새 ObjectDataSource 라는 추가 `CategoriesDataSource` ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image8.png))


새 ObjectDataSource 호출 갖도록 구성 해야는 `CategoriesBLL` 클래스의 `GetCategories()` 메서드. 드롭다운 목록에서 어떤 데이터 소스 필드를 표시 해야 하와 지정 해야 ObjectDataSource를 구성한 후 각 목록 항목에 대 한 값으로 연결 해야 하나 합니다. 있어야는 `CategoryName` 디스플레이와 필드 및 `CategoryID` 각 목록 항목에 대 한 값으로.


[![DropDownList 표시 범주 필드와 사용 하 여 CategoryID는는 값으로](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image9.png)

**그림 5**: DropDownList 디스플레이 `CategoryName` 필드 및 사용 `CategoryID` 값으로 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image11.png))


이 시점에서의 레코드와 채워지는 DropDownList 컨트롤이 `Categories` 테이블 (모두 약 6 초 후에 수행). 그림 6 브라우저를 통해 표시 될 때까지 진행률을 보여줍니다.


[![드롭 다운 현재 범주를 나열합니다.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image12.png)

**그림 6**: A 드롭다운 목록이 현재 범주 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image14.png))


## <a name="step-2-adding-the-products-datalist"></a>2 단계: 추가 제품 DataList

마스터/세부 정보 보고서의 마지막 단계는 선택한 범주와 관련 된 제품을 나열 하는 것입니다. 이를 위해 DataList 페이지에 추가 하 고 라는 새 ObjectDataSource 만들 `ProductsByCategoryDataSource`합니다. 있어야는 `ProductsByCategoryDataSource` 컨트롤에서 데이터를 검색 된 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드. 이 마스터/세부 보고서 읽기 전용 이므로 (없음)는 INSERT, UPDATE 및 DELETE 탭에서 옵션을 선택 합니다.


[![GetProductsByCategoryID(categoryID) 방법 선택](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image15.png)

**그림 7**: 선택 된 `GetProductsByCategoryID(categoryID)` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image17.png))


다음을 클릭 한 후 ObjectDataSource 마법사 라는 메시지가 나타납니다에 대 한 값의 출처는 `GetProductsByCategoryID(categoryID)` 메서드의  *`categoryID`*  매개 변수입니다. 선택 된 값을 사용 하려면 `categories` DropDownList 항목 매개 변수 소스 제어 및에 ControlID를 설정 `Categories`합니다.


[![매개 변수 categoryID 범주 DropDownList의 값으로 설정](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image18.png)

**그림 8**: 설정의  *`categoryID`*  의 값에 대 한 매개 변수는 `Categories` DropDownList ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image20.png))


Visual Studio에서 자동으로 데이터 소스 구성 마법사를 완료 될 때 생성 된 `ItemTemplate` DataList 이름 및 각 데이터 필드의 값을 표시 하는 대 한 합니다. 대신 사용 하 여 DataList을 향상 해 보겠습니다는 `ItemTemplate` 제품의 이름, 범주, 공급 업체, 단위 테스트와 함께 가격 및 수량만 표시 하는 `SeparatorTemplate` 삽입 하는 `<hr>` 각 항목 사이 요소입니다. 사용 하도록 하겠습니다는 `ItemTemplate` 의 예제에서는 [DataList 및 반복기 컨트롤을 사용 하 여 데이터 표시](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb.md) 자습서 하지만 느낌 매력적인 시각적으로 가장 찾을 어떤 템플릿 태그 있습니다 사용할 수 있습니다.

다음과 같이 변경한 후 여 DataList 및 해당 ObjectDataSource 태그 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample2.aspx)]

브라우저에서 진행률을 확인해 보십시오. 페이지를 처음 방문 하는 경우 (음료) 선택한 범주에 속하는 제품 같이 표시 됩니다 (그림 9에서), 하지만 DropDownList 변경 데이터를 업데이트 하지는 않습니다. 업데이트 하려면 DataList 포스트백 발생 해야 발생 때문입니다. 활용해 서 하거나이를 위해 설정 DropDownList의 `AutoPostBack` 속성을 `true` 또는 페이지에 단추 웹 컨트롤을 추가 합니다. 이 자습서에서는 선택한 이유는 DropDownList를 설정 하려면 `AutoPostBack` 속성을 `true`합니다.

그림 9와 10 작업에서 마스터/세부 정보 보고서를 보여 줍니다.


[![처음 방문 하 여 페이지 음료 제품 표시 됩니다.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image21.png)

**그림 9**: 처음 방문 하 여 페이지 음료 제품 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image23.png))


[![DataList 업데이트의 포스트백을 사용 하면 새 제품 (생성)을 선택 하면 자동으로](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image24.png)

**그림 10**: DataList 업데이트 포스트백 신제품 (생성)를 자동으로 선택 하면 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image26.png))


## <a name="adding-a----choose-a-category----list-item"></a>"-범주 선택-" 목록 항목 추가

처음 방문할 때는 `FilterByDropDownList.aspx` DropDownList의 첫 번째 목록 항목 (음료) DataList 음료 제품을 보여 주는 기본적으로 선택 되어 범주 페이지입니다. 에 *마스터/세부 정보 필터링 된 정도 DropDownList* 자습서 "-범주 선택-" 옵션을 기본적으로 선택 되었으며 옵션을 선택 하면 표시 되는 드롭다운 목록에 추가한 *모든* 의 데이터베이스에서 제품입니다. 이러한 접근 방식은 관리할 수는 GridView에 제품을 나열 하는 경우 각 제품 행 적은 양의 화면 자원을를 걸렸습니다. 그러나 datalist, 각 제품 정보를이 훨씬 더 큰 청크 화면을 사용합니다. 여전히 보겠습니다 "-범주 선택-" 옵션을 추가 하 고 기본적으로 선택 하 게 이지만 모든 제품을 표시 하지 않고 옵션을 선택 하면 보겠습니다 구성할 제품이 표시 되도록 합니다.

DropDownList를 새 목록 항목을 추가 하려면 속성 창으로 이동 하 고의 줄임표를 클릭 하 고 `Items` 속성입니다. 추가 된 새 목록 항목의 `Text` "-범주 선택-" 및 `Value` `0`합니다.


![추가](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image27.png)

**그림 11**: "-범주 선택-" 목록 항목 추가


또는 드롭다운 목록에 다음 태그를 추가 하 여 목록 항목을 추가할 수 있습니다.

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample3.aspx)]

또한 DropDownList 제어를 설정 하려면 할 `AppendDataBoundItems` 를 `true` 때문에로 설정 되어 있으면 `false` (기본값), 수동으로 추가 하는 모든 목록 덮어씁니다 범주는 ObjectDataSource에서 드롭다운 목록에 바인딩되는 경우 항목입니다.


![AppendDataBoundItems 속성이 True로 설정](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image28.png)

**그림 12**: 설정의 `AppendDataBoundItems` 속성을 True로


값 선택 이유 `0` "-범주 선택-" 목록에 대 한 항목은 범주가 있는 시스템의 값에 있기 때문에 `0`, 따라서 "-범주 선택-" 목록 항목을 선택 하는 경우 제품 레코드가 없습니다 항목이 반환 됩니다. 이 확인 하려면 브라우저를 통해 페이지를 방문 하 여 보십시오. 그림 13에서는 처음 페이지 보기 "-범주 선택-" 목록 항목을 선택 하면 제품이 표시 됩니다.


[![경우는](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image29.png)

**그림 13**: "-범주 선택-" 목록 항목을 선택 하면 No 제품 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image31.png))


대신 표시 하는 경우 *모든* 제품 "-범주 선택-" 옵션을 선택 하면 값이 사용 됩니다. `-1` 대신 합니다. 예리한 독자에 그 뒤로 다시 호출 됩니다는 *마스터/세부 정보 필터링 된 정도 DropDownList* 을 업데이트 했습니다. 자습서는 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드 되도록 하는 경우는  *`categoryID`*  값 `-1` 반환 된 레코드가 모든 제품에 전달 되었습니다.

## <a name="summary"></a>요약

계층적으로 관련 데이터를 표시할 때 종종 사용자 계층의 최상위에서 데이터를 읽는 데 시작 하 고 세부 정보로 드릴 다운는 마스터/세부 보고서를 사용 하 여 데이터를 제공할 수 있습니다. 이 자습서에서는 선택한 범주의 제품을 보여 주는 간단한 마스터/세부 보고서 작성을 검사 합니다. 이 범주에는 선택한 범주에 속한 제품에 대 한 DataList의 목록과 DropDownList를 사용 하 여 수행 되었습니다.

다음 자습서 두 페이지에 걸쳐 마스터 및 세부 정보 레코드를 구분 하는 방법을 살펴보겠습니다. 첫 번째 페이지에서 "마스터" 레코드 목록이 표시 됩니다, 정보를 보려면 해당 링크. 링크를 클릭 하면 사용자는 선택된 된 마스터 레코드에 대 한 정보를 표시 하는 두 번째 페이지를 whisk 됩니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특히 감사 드립니다.

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Randy Schmidt 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
[다음](master-detail-filtering-acess-two-pages-datalist-vb.md)
