---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-vb
title: 마스터/세부 정보 필터링 (VB)의 두 페이지에 걸쳐 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 두 페이지에 걸쳐 마스터/세부 정보 보고서를 구분 하는 방법에 살펴봅니다. 'Master' 페이지를 사용 하 여 반복기 컨트롤 categ 목록을 렌더링 하는 중...
ms.author: aspnetcontent
ms.date: 10/30/2010
ms.assetid: f1a1be2c-6fd9-4a09-916e-aa1b98d5cf17
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 5cfbd685344bdd223f8d07f8bad5a54b63735839
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37813700"
---
<a name="masterdetail-filtering-across-two-pages-vb"></a>마스터/세부 정보 필터링 (VB)의 두 페이지에 걸쳐
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_34_VB.exe) 또는 [PDF 다운로드](master-detail-filtering-acess-two-pages-datalist-vb/_static/datatutorial34vb1.pdf)

> 이 자습서에서는 두 페이지에 걸쳐 마스터/세부 정보 보고서를 구분 하는 방법에 살펴봅니다. "마스터" 페이지에서 클릭, 두 개의 열 DataList 선택한 범주에 속하는 해당 제품을 표시 하는 위치 "정보" 페이지로 사용자 이동 됩니다 때 범주 목록이 렌더링할 Repeater 컨트롤을 사용 합니다.


## <a name="introduction"></a>소개

에 [마스터/세부 정보 필터링에서 두 페이지가](../masterdetail/master-detail-filtering-across-two-pages-vb.md) 자습서에서는 시스템 공급 업체의 모든 표시를 GridView를 사용 하 여이 패턴에서는 검사 합니다. 이 GridView와 함께 전달 된 두 번째 페이지 링크로 렌더링을 HyperLinkField 포함 된 `SupplierID` 쿼리 문자열에서. 선택한 공급자가 제공 하는 이러한 제품을 나열 하는 GridView를 사용 하는 두 번째 페이지입니다.

DataList 및 반복기 컨트롤을 사용 하 여 이러한 두 페이지 마스터/세부 정보 보고서를 수행할 수 있습니다. 유일한 차이점은 DataList 또는 Repeater 모두 HyperLinkField 컨트롤에 대 한 지원을 제공 합니다. 대신, 하이퍼링크 웹 컨트롤 또는 HTML 앵커 요소를 추가 해야 합니다 (`<a>`) 컨트롤의 내 `ItemTemplate`합니다. 하이퍼링크 `NavigateUrl` 속성 또는 앵커 `href` 특성 후 사용자 지정할 수 있습니다 프로그래밍 방식으로 또는 선언적 방법을 사용 하 여 합니다.

이 자습서에서는 반복기 컨트롤을 사용 하 여 한 페이지에 글머리 기호 목록에서 범주를 나열 하는 예제를 살펴보겠습니다. 각 목록 항목을 두 번째 페이지 링크로 표시 되는 범주 이름을 사용 하 여 범주 이름과 설명이 포함 됩니다. 이 링크를 클릭 하는 whisk 두 번째 페이지에서 사용자 DataList는 선택한 범주에 속하는 해당 제품을 표시 하는 위치입니다.

## <a name="step-1-displaying-the-categories-in-a-bulleted-list"></a>1 단계: 글머리 기호 목록에서 범주 표시

마스터/세부 정보 보고서를 만드는 첫 번째 단계는 "마스터" 레코드를 표시 하 여 시작 하는 것입니다. 따라서 우선 "마스터" 페이지에서 범주를 표시 하는 것입니다. 엽니다는 `CategoryListMaster.aspx` 페이지에 `DataListRepeaterFiltering` 폴더 Repeater 컨트롤을 추가 하 고, 스마트 태그에서 새 ObjectDataSource를 추가 하도록 선택할. 해당 데이터에 액세스할 수 있도록 새 ObjectDataSource를 구성 합니다 `CategoriesBLL` 클래스의 `GetCategories` 메서드 (그림 1 참조).


[![CategoriesBLL 클래스의 GetCategories 메서드를 사용 하는 ObjectDataSource 구성](master-detail-filtering-acess-two-pages-datalist-vb/_static/image2.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image1.png)

**그림 1**: ObjectDataSource 사용 하도록 구성 된 `CategoriesBLL` 클래스의 `GetCategories` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-acess-two-pages-datalist-vb/_static/image3.png))


그런 다음 각 범주 이름과 설명을 글머리 기호 목록에 항목으로 표시 되도록 반복기의 템플릿을 정의 합니다. 보겠습니다 아직 걱정할 범주별 세부 정보 페이지에 링크 합니다. 다음은 반복기 및 ObjectDataSource에 대 한 선언적 태그.

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample1.aspx)]

전체이 태그를 사용 하 여 시간을 내어 브라우저를 통해 진행 상황을 확인 합니다. 그림 2에서 볼 수 있듯이 각 범주 이름과 설명을 보여 주는 글머리 기호 목록으로 반복기를 렌더링 합니다.


[![각 범주에 글머리 기호 목록 항목으로 표시 됩니다.](master-detail-filtering-acess-two-pages-datalist-vb/_static/image5.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image4.png)

**그림 2**: 각 범주에 글머리 기호 목록 항목으로 표시 됩니다 ([큰 이미지를 보려면 클릭](master-detail-filtering-acess-two-pages-datalist-vb/_static/image6.png))


## <a name="step-2-turning-the-category-name-into-a-link-to-the-details-page"></a>2 단계: 세부 정보 페이지에 대 한 링크에 범주 이름 설정

지정된 된 범주에 대 한 "details" 정보를 표시할 사용자를 허용 하려면 링크 클릭, 두 번째 페이지로 걸리는 경우, 각 글머리 기호 목록 항목을 추가 해야 (`ProductsForCategoryDetails.aspx`). 그러면이 두 번째 페이지 DataList를 사용 하 여 선택한 범주에 대 한 제품을 표시 됩니다. 해당 링크를 클릭 한 범주를 확인 하기 위해 클릭 한 범주를 전달 해야 `CategoryID` 몇 가지 메커니즘을 통해 두 번째 페이지입니다. 다른 한 페이지에서 스칼라 데이터를 전송 하는 가장 간단 하 고 가장 간단한 방법은 쿼리 문자열을 통해이 자습서에서 사용 해야 하는 옵션입니다. 특히 합니다 `ProductsForCategoryDetails.aspx` 페이지는 선택한 예상 *`categoryID`* 라는 쿼리 문자열 필드를 통해 전달 될 값입니다 `CategoryID`합니다. 예를 들어 음료 범주에 대 한 제품을 보려면 표시 된를 `CategoryID` 방문 하는 사용자 1 `ProductsForCategoryDetails.aspx?CategoryID=1`합니다.

하이퍼링크 웹 컨트롤 또는 HTML 앵커 요소를 추가 해야 하는 반복기의 각 글머리 기호 목록 항목에 대 한 하이퍼링크를 만들려면 (`<a>`)에 `ItemTemplate`합니다. 하이퍼링크 인 시나리오 각 행에 대해 동일 하 게 표시, 두 가지 방법만 사용 해도 충분 합니다. 반복기에 대 한 앵커 요소를 사용 하 여 필자 선호 합니다. 앵커 요소를 사용 하려면 업데이트를 반복기의 ItemTemplate.

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample2.aspx)]

`CategoryID` 앵커 요소 내에서 직접 주입할 수 있습니다 `href` 특성을 그러나 수행 하므로 반드시 구분 하는 `href` 이후 아포스트로피 (및 참고 따옴표)를 사용 하 여 특성의 값을 `Eval` 메서드 내 합니다 `href` 해당 문자열을 구분 하는 특성 (`"CategoryID"`) 따옴표를 사용 하 여 합니다. 또는 하이퍼링크 웹 컨트롤을 대신 사용할 수 있습니다.

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample3.aspx)]

참고 어떻게 URL의 정적 부분 — `ProductsForCategoryDetails.aspx?CategoryID` -결과에 추가 됩니다 `Eval("CategoryID")` 문자열 연결을 사용 하 여 데이터 바인딩 구문 내에서 직접.

하이퍼링크 컨트롤을 사용 하 여의 이점 중 하나는 프로그래밍 방식으로 액세스할 수는 반복기에서 `ItemDataBound` 필요한 경우 이벤트 처리기입니다. 예를 들어, 다음 제품이 없습니다. 연결된을 사용 하 여 범주에 대 한 링크가 아닌 텍스트 범주 이름을 표시 하는 것이 좋습니다. 이러한 확인을 프로그래밍 방식으로 수행할 수 없습니다는 `ItemDataBound` 이벤트 처리기 연결 된 제품 하이퍼링크의 없는 범주에 대 한 `NavigateUrl` 해당 특정 범주 이름과 그 결과로 빈 문자열로, 속성을 설정할 수 일반 텍스트로 (아닌 링크)를 렌더링 합니다. 다시 참조를 [DataList 및 반복기 기반으로 데이터 서식 지정](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb.md) 를 통해 프로그래밍 방식으로 논리를 기반으로 DataList 및 반복기의 내용 서식 지정에 대 한 자세한 내용은 자습서를 `ItemDataBound` 이벤트 처리기입니다.

수행 하는 경우 자유롭게 페이지 앵커 요소 또는 하이퍼링크 컨트롤 접근 방식을 사용 합니다. 각 범주 이름에 대 한 링크로 렌더링 되어야 하는 브라우저를 통해 페이지를 볼 때 접근 방식에 관계 없이 `ProductsForCategoryDetails.aspx`해당 전달 `CategoryID` 값 (그림 3 참조).


[![범주 이름이 이제 ProductsForCategoryDetails.aspx에 연결](master-detail-filtering-acess-two-pages-datalist-vb/_static/image8.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image7.png)

**그림 3**:의 범주 이름을 이제 연결할 `ProductsForCategoryDetails.aspx` ([클릭 하 여 큰 이미지 보기](master-detail-filtering-acess-two-pages-datalist-vb/_static/image9.png))


## <a name="step-3-listing-the-products-that-belong-to-the-selected-category"></a>선택한 범주에 속하는 제품을 나열 하는 3 단계:

사용 하 여 합니다 `CategoryListMaster.aspx` 완료 페이지에서 준비가 "정보" 페이지를 구현 하는 데 알아보겠습니다 `ProductsForCategoryDetails.aspx`합니다. 이 페이지를 열려면 DataList 디자이너 도구 상자에서 끌어서 설정 해당 `ID` 속성을 `ProductsInCategory`입니다. 다음으로, DataList의 스마트 태그에서 새 ObjectDataSource 이름을 지정 하는 페이지에 추가 하도록 선택할 `ProductsInCategoryDataSource`합니다. 호출 되도록 구성 합니다 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 방법으로, 드롭다운 목록에서 INSERT, UPDATE 및 DELETE 탭 (없음)을 나열 하는 집합입니다.


[![ProductsBLL 클래스의 GetProductsByCategoryID(categoryID) 메서드를 사용 하는 ObjectDataSource 구성](master-detail-filtering-acess-two-pages-datalist-vb/_static/image11.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image10.png)

**그림 4**: ObjectDataSource 사용 하도록 구성 된 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-acess-two-pages-datalist-vb/_static/image12.png))


이후 합니다 `GetProductsByCategoryID(categoryID)` 메서드에서 입력된 매개 변수 (*`categoryID`*), 매개 변수의 소스를 지정할 수 있도록 데이터 원본 선택 마법사에서 제공 합니다. QueryStringField를 사용 하 여 쿼리 문자열 매개 변수 원본으로 `CategoryID`합니다.


[![Querystring 필드 CategoryID 매개 변수의 원본으로 사용](master-detail-filtering-acess-two-pages-datalist-vb/_static/image14.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image13.png)

**그림 5**: 쿼리 문자열 필드를 사용 하 여 `CategoryID` 매개 변수의 소스로 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-acess-two-pages-datalist-vb/_static/image15.png))


앞서 설명한 것 처럼 이전 자습서에서는 데이터 소스 선택 마법사를 완료 한 후 자동으로 만들어지고는 `ItemTemplate` 각 데이터 필드 이름 및 값을 나열 하는 DataList에 대 한 합니다. 제품의 이름, 공급자 및 가격을 나열 하는 하나를 사용 하 여이 서식 파일을 대체 합니다. DataList의 설정, `RepeatColumns` 속성을 2로 합니다. 이러한 변경 된 후에 DataList 및 ObjectDataSource의 선언 태그 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample4.aspx)]

시작 작업에서이 페이지를 보려는 `CategoryListMaster.aspx` 페이지를 다음으로, 범주 글머리 기호 목록에서 링크를 클릭 합니다. 이렇게 하면 `ProductsForCategoryDetails.aspx`함께 전달 된 `CategoryID` querystring을 통해. `ProductsInCategoryDataSource` ObjectDataSource `ProductsForCategoryDetails.aspx` 지정한 범주에 대 한 해당 제품을 가져옵니다 되며 행 마다 두 개의 제품을 렌더링 하는 DataList를 표시 합니다. 그림 6의 스크린샷이 나와 `ProductsForCategoryDetails.aspx` 음료를 볼 때.


[![음료 표시 되는 행 당 2 개](master-detail-filtering-acess-two-pages-datalist-vb/_static/image17.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image16.png)

**그림 6**: The 음료 표시 되는 행 당 2 개 ([큰 이미지를 보려면 클릭](master-detail-filtering-acess-two-pages-datalist-vb/_static/image18.png))


## <a name="step-4-displaying-category-information-on-productsforcategorydetailsaspx"></a>4 단계: ProductsForCategoryDetails.aspx에 범주 정보를 표시합니다.

사용자 범주를 클릭할 때 `CategoryListMaster.aspx`는 `ProductsForCategoryDetails.aspx` 선택한 범주에 속하는 제품을 표시 합니다. 그러나 `ProductsForCategoryDetails.aspx` 가지 범주 선택에 대 한 시각적 표식이 없습니다. 음료를 입력 하면 조미료 실수로 클릭된, 클릭 하려는 사용자의 도달 하면 해당 실수를 인식 하지 못함을 `ProductsForCategoryDetails.aspx`합니다. 이 잠재적 문제를 완화 하려면 경우에 선택한 범주에 대 한 정보를 표시할 수 있습니다-해당 이름 및 설명을-맨 위에 있는 `ProductsForCategoryDetails.aspx` 페이지입니다.

이렇게 하려면 추가 Repeater 컨트롤 위에 FormView `ProductsForCategoryDetails.aspx`합니다. 그런 다음 새 ObjectDataSource 라는 FormView의 스마트 태그에서 페이지 추가 `CategoryDataSource` 를 사용 하도록 구성 합니다 `CategoriesBLL` 클래스의 `GetCategoryByCategoryID(categoryID)` 메서드.


[![CategoriesBLL 클래스의 GetCategoryByCategoryID(categoryID) 메서드를 통해 범주에 대 한 액세스 정보](master-detail-filtering-acess-two-pages-datalist-vb/_static/image20.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image19.png)

**그림 7**: 통해 범주에 대 한 액세스 정보를 `CategoriesBLL` 클래스의 `GetCategoryByCategoryID(categoryID)` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-acess-two-pages-datalist-vb/_static/image21.png))


와 마찬가지로 `ProductsInCategoryDataSource` ObjectDataSource 3 단계에서에서 추가 `CategoryDataSource`의 데이터 소스 구성 마법사에 대 한 소스에 대 한 요청을 `GetCategoryByCategoryID(categoryID)` 메서드 매개 변수 입력 합니다. 정확히 동일한 설정을 사용 앞으로 QueryString QueryStringField 값을로 설정 하는 매개 변수 원본 `CategoryID` (그림 5를 다시 참조).

마법사를 완료 한 후 Visual Studio 자동으로 만듭니다는 `ItemTemplate`, `EditItemTemplate`, 및 `InsertItemTemplate` FormView에 대 한 합니다. 읽기 전용 인터페이스를 제공 하 고, 때문에 자유롭게 삭제 합니다 `EditItemTemplate` 고 `InsertItemTemplate`입니다. 또한 자유롭게 FormView의 `ItemTemplate`합니다. 불필요 한 템플릿을 제거 하 고 ItemTemplate을 사용자 지정을 프로그램 FormView 및 ObjectDataSource의 선언 태그 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample5.aspx)]

그림 8에서는 브라우저를 통해이 페이지를 볼 때를 지정 하 여 화면을 보여 줍니다.

> [!NOTE]
> FormView, 외에도 추가 했습니다 하는 데 필요한 사용자 범주의 목록으로 돌아가기 FormView 위에 하이퍼링크 컨트롤 (`CategoryListMaster.aspx`). 이 링크를 다른 곳에서 배치 하거나 완전히 생략 해도 됩니다.


[![범주 정보는 이제 페이지의 맨 위에 표시](master-detail-filtering-acess-two-pages-datalist-vb/_static/image23.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image22.png)

**그림 8**: 이제 페이지의 맨 위에 표시 되는 범주 정보는 ([큰 이미지를 보려면 클릭](master-detail-filtering-acess-two-pages-datalist-vb/_static/image24.png))


## <a name="step-5-displaying-a-message-if-no-products-belong-to-the-selected-category"></a>5 단계: 제품이 없습니다. 선택한 범주에 속하는 경우 메시지 표시

`CategoryListMaster.aspx` 페이지에 관계 없이 시스템에서 모든 범주를 나열 있는지 제품을 연결 합니다. DataList에서 연결 된 제품은 없습니다를 사용 하 여 범주를 두 번 클릭할 경우 `ProductsForCategoryDetails.aspx` 렌더링 되지 않음, 해당 데이터 원본 항목 것 처럼 합니다. GridView를 제공 하는 이전 자습서에서 살펴본 대로 `EmptyDataText` 레코드가 해당 데이터 원본에 없는 경우 표시할 텍스트 메시지를 지정 하는 속성입니다. 아쉽게도 DataList 또는 Repeater를 모두 이러한 속성이 있습니다.

선택한 범주에 대 한 일치 하는 제품이 추가 해야 사용자에 게 알리는 메시지를 표시 하기 위해 레이블 컨트롤 페이지로 `Text` 속성은 일치 하는 제품이 없습니다 하는 경우에 표시할 메시지를 할당 합니다. 그런 다음 프로그래밍 방식으로 설정 해야 해당 `Visible` 속성 DataList 모든 항목을 포함 하는 여부에 따라 합니다.

이렇게 하려면 DataList 아래에 레이블을 추가 하 여 시작 합니다. 설정 해당 `ID` 속성을 `NoProductsMessage` 고 `Text` "제품이 없습니다... 선택한 범주에 대 한" 속성 프로그래밍 방식으로이 레이블의 설정 해야이 어 `Visible` 속성에 데이터 바인딩된 여부에 따라는 `ProductsInCategory` DataList 합니다. DataList에 데이터 바인딩된 후에이 할당을 수행 되어야 합니다. GridView, DetailsView 및 FormView 컨트롤에 대 한 이벤트 처리기를 만들 수 것 `DataBound` databinding 완료 된 후 발생 하는 이벤트입니다. 그러나 DataList 아니고 반복기에는 `DataBound` 이벤트를 사용할 수 있습니다.

이 특정 예제의 레이블 할당할 수 있습니다 `Visible` 속성에는 `Page_Load` 이벤트 처리기에서 데이터는 할당 된 페이지의 이전 DataList 있으므로 `Load` 이벤트입니다. 그러나이 방법은 대로 ObjectDataSource의 데이터 페이지의 수명 주기에서 나중에 DataList 바인딩할 수 있습니다 일반 경우에서 도움이 되지 않습니다. 예를 들어, DropDownList를 사용 하 여 "마스터" 레코드를 보유 하는 마스터/세부 정보 보고서를 표시 하는 경우와 같은 다른 컨트롤의 값으로 표시 되는 데이터 기반, 경우 데이터 수 다시 바인딩되지 될 때까지 데이터 웹 컨트롤에는 `PreRender` 단계는 페이지의 수명 주기입니다.

할당할 모든 사례에 대해 작동 하는 한 가지 해결책은는 `Visible` 속성을 `False` DataList의에서 `ItemDataBound` (또는 `ItemCreated`)의 항목 종류를 바인딩할 때 이벤트 처리기 `Item` 또는 `AlternatingItem`합니다. 이러한 경우 알 수 있는 하나 이상의 데이터 데이터 소스의 항목 및 따라서 숨길 수는 `NoProductsMessage` 레이블. 이 이벤트 처리기에 외에 이벤트 처리기에 필요한 DataList의 `DataBinding` 이벤트에 있는 레이블의 초기화 `Visible` 속성을 `True`입니다. 그러나 있으므로 합니다 `DataBinding` 이벤트가 발생 하기 전에 `ItemDataBound` 이벤트 레이블의 `Visible` 속성에 처음 설정할 `True`데이터 항목이 있는 경우 설정 됩니다 `False`. 다음 코드는이 논리를 구현합니다.

[!code-vb[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample6.vb)]

모든 Northwind 데이터베이스의 범주는 하나 이상의 제품을 사용 하 여 연결 합니다. 이 기능을 테스트 하려면 있습니까 수동으로 조정한 Northwind 데이터베이스가 자습서에서는 생성 범주와 관련 된 모든 제품을 다시 할당 (`CategoryID` = 7) Seafood 범주 (`CategoryID` = 8). 이렇게 하려면 서버 탐색기에서 새 쿼리를 선택 하 고 다음을 사용 하 여 `UPDATE` 문:

[!code-sql[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample7.sql)]

데이터베이스를 그에 따라 업데이트 한 후에 반환 된 `CategoryListMaster.aspx` 페이지 및 생성 링크를 클릭 합니다. 더 이상 생성 범주에 속하는 모든 제품을 없으므로 그림 9에 표시 된 대로 "제품이 없습니다 선택한 범주..." 메시지를 표시 됩니다.


[![선택한 범주에 없는 제품 속하는 경우 메시지가 표시 됩니다.](master-detail-filtering-acess-two-pages-datalist-vb/_static/image26.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image25.png)

**그림 9**: 선택한 범주에 없는 제품 속하는 경우에 메시지가 표시 됩니다 ([큰 이미지를 보려면 클릭](master-detail-filtering-acess-two-pages-datalist-vb/_static/image27.png))


## <a name="summary"></a>요약

마스터/세부 정보 보고서는 단일 페이지에 마스터 및 세부 정보 레코드를 표시할 수 있습니다, 있지만 여러 웹 사이트에서 구분 됩니다 두 웹 페이지에 걸쳐. 이 자습서에서는 Repeater를 사용 하 여 "마스터" 웹 페이지에서 글머리 기호 목록에 나열 된 범주 및 관련된 제품이 "정보" 페이지에서 나열 하 여 이러한 마스터/세부 정보 보고서를 구현 하는 방법에 살펴보았습니다. 마스터 웹 페이지의 각 목록 항목의 행을 전달 하는 세부 정보 페이지에 대 한 링크 포함 `CategoryID` 값입니다.

세부 정보 페이지에서를 통해 수행 된 지정 된 공급자에 대 한 해당 제품을 검색 합니다 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드. 합니다 *`categoryID`* 매개 변수 값을 사용 하 여 선언적으로 지정 했습니다는 `CategoryID` 매개 변수 원본으로 쿼리 문자열 값입니다. 또한 살펴보았습니다 FormView를 사용 하 여 세부 정보 페이지에서 범주 세부 정보를 표시 하는 방법 및 선택한 범주에 속하는 제품이 있다면 메시지를 표시 하는 방법.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사 하는 중...

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Zack Jones와 Liz Shulok 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-filtering-with-a-dropdownlist-datalist-vb.md)
> [다음](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)
