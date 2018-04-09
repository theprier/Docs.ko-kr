---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-vb
title: DataList 또는 반복기 컨트롤 (VB)에서 데이터 정렬 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 정렬 지원을 DataList 및 반복기를 포함 하는 방법 뿐만 아니라 해당 데이터가 수 DataList 또는 반복기를 생성 하는 방법을 검토 합니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/13/2006
ms.topic: article
ms.assetid: 97c13898-0741-45f9-b3fa-7540ab1679e6
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 66d6833e69a91aef39cc4a202ef662ecaeeee839
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="sorting-data-in-a-datalist-or-repeater-control-vb"></a>DataList 또는 반복기 컨트롤 (VB)에서 데이터 정렬
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_45_VB.exe) 또는 [PDF 다운로드](sorting-data-in-a-datalist-or-repeater-control-vb/_static/datatutorial45vb1.pdf)

> 이 자습서에서는 정렬 지원을 DataList 및 반복기를 포함 하는 방법 뿐만 아니라 DataList 또는 해당 데이터를 페이징 및 정렬 수 반복기를 생성 하는 방법을 검토 합니다.


## <a name="introduction"></a>소개

에 [이전 자습서](paging-report-data-in-a-datalist-or-repeater-control-vb.md) DataList에 페이징 지원을 추가 하는 방법을 검사 했습니다. 새로운 방법으로 만든는 `ProductsBLL` 클래스 (`GetProductsAsPagedDataSource`) 반환 되는 `PagedDataSource` 개체입니다. DataList 또는 반복기에 바인딩할 경우 데이터의 요청 된 페이지 뿐 DataList 또는 반복기를 만들 표시 됩니다. 이 방법은 용도 내부적으로 GridView, DetailsView, 및 FormView 컨트롤에서 해당 기본 제공 페이징 기능을 제공 하도록 유사 합니다.

페이징 지원을 제공 하는 것 외에도 GridView 정렬 지원을 유틸리티로 포함 됩니다. DataList 아니고 반복기 기본 제공 정렬 기능이 있습니다. 그러나 정렬 기능으로 약간의 코드를 추가할 수 있습니다. 이 자습서에서는 정렬 지원을 DataList 및 반복기를 포함 하는 방법 뿐만 아니라 DataList 또는 해당 데이터를 페이징 및 정렬 수 반복기를 생성 하는 방법을 검토 합니다.

## <a name="a-review-of-sorting"></a>정렬에 대 한 검토

설명한 것 처럼는 [페이징 및 보고서 데이터 정렬](../paging-and-sorting/paging-and-sorting-report-data-vb.md) 자습서에서는 GridView 컨트롤 즉시 정렬 지원을 제공 합니다. 각 GridView 필드를 연결 된 점이 `SortExpression`, 데이터를 정렬 하는 기준인 데이터 필드를 나타냅니다. 때 GridView s `AllowSorting` 속성이 `true`, 지정 된 각 GridView 필드는 `SortExpression` 속성 값에는 헤더는 LinkButton로 렌더링 합니다. 포스트백이 발생할 및 s 클릭 한 필드에 따라 데이터가 정렬 되는 사용자가 특정 GridView 필드의 헤더를 클릭 하면 `SortExpression`합니다.

GridView 컨트롤에는 `SortExpression` 속성도 저장 되는 `SortExpression` GridView 필드의 데이터 정렬에 의해 합니다. 또한 한 `SortDirection` 속성 데이터를 오름차순 또는 내림차순 (경우 특정 GridView의 필드 헤더의에서 링크를 두 번 연속 해 서 제공 되는 정렬 순서 설정/해제 되는 사용자가 클릭)에서 정렬 하는 지 여부를 나타냅니다.

GridView의 데이터 소스 제어에 바인딩되면 핸드 오프 해당 `SortExpression` 및 `SortDirection` 속성을 데이터 소스 제어 합니다. 데이터 소스 제어의 데이터를 검색 한 다음 제공 된에 따라 정렬 `SortExpression` 및 `SortDirection` 속성입니다. 데이터를 정렬 한 후 데이터 소스 제어 GridView에 반환 됩니다.

DataList 또는 반복기 컨트롤과 함께이 기능을 복제 해야 합니다.

- 정렬 인터페이스 만들기
- 데이터 필드를 기준으로 정렬 하 고 오름차순 또는 내림차순으로 정렬할 것인지를 기억 합니다.
- 특정 데이터 필드에 따라 데이터를 정렬 하려면 ObjectDataSource를 지시 합니다.

이러한 세 가지 작업 3 및 4 단계에서 해결할 합니다. 그런 다음, 페이징 및 정렬 DataList 또는 반복기에 대 한 지원을 모두 포함 하는 방법을 검토 합니다.

## <a name="step-2-displaying-the-products-in-a-repeater"></a>2 단계:는 반복기에는 제품 표시

정렬 관련 기능 중 하나를 구현 하는 방법에 대 한 걱정 म 전에 반복기 컨트롤에서 제품을 나열 하 여 시작 s가 있습니다. 열어 시작는 `Sorting.aspx` 페이지에 `PagingSortingDataListRepeater` 폴더입니다. 반복기 컨트롤을 설정 하는 웹 페이지 추가 해당 `ID` 속성을 `SortableProducts`합니다. 반복기 s 스마트 태그를 만들고 라는 새 ObjectDataSource `ProductsDataSource` 에서 데이터를 검색 하도록 구성 하는 `ProductsBLL` s 클래스 `GetProducts()` 메서드. (없음)가 INSERT, UPDATE 및 DELETE 탭에 있는 드롭 다운 목록에서 옵션을 선택 합니다.


[![ObjectDataSource 만들고 GetProductsAsPagedDataSource() 메서드를 사용 하도록 구성](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image2.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image1.png)

**그림 1**:는 ObjectDataSource를 만들고 사용 하도록 구성 된 `GetProductsAsPagedDataSource()` 메서드 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image3.png))


[![UPDATE, INSERT에에서 드롭다운 목록이 설정 하 고 각 탭 (없음)을 삭제 합니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image5.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image4.png)

**그림 2**: 삽입, 업데이트에서 드롭 다운 목록를 설정 하 고 각 탭 (없음)을 삭제 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image6.png))


와 달리 datalist, Visual Studio 자동으로 만들지 않으므로 `ItemTemplate` 데이터 소스에 바인딩한 후 반복기 컨트롤에 대 한 합니다. 이 추가 해야 또한 `ItemTemplate` , 선언적으로 반복기 컨트롤 s 스마트 태그 템플릿 편집 옵션 DataList s에서에서 찾을 수 없습니다. 같은 let s 사용 `ItemTemplate` 이전 자습서에서 표시 되는 s 제품 이름, 공급 업체 및 범주입니다.

추가한 후의 `ItemTemplate`, 반복기 및 ObjectDataSource s 선언적 태그는 다음과 비슷해야 합니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample1.aspx)]

그림 3에서는 브라우저를 통해 볼 때이 페이지를 보여 줍니다.


[![각 제품 이름, 공급 업체 및 범주 s 표시 됩니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image8.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image7.png)

**그림 3**: 각 제품 이름, 공급 업체 및 범주에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image9.png))


## <a name="step-3-instructing-the-objectdatasource-to-sort-the-data"></a>3 단계: 데이터를 정렬 하려면 ObjectDataSource 지시

반복기에 표시 된 데이터를 정렬 하려면 데이터를 정렬 해야 하는 정렬 식의 ObjectDataSource에 알려야 할 합니다. 먼저 발생 ObjectDataSource에서 해당 데이터를 검색 하기 전에 해당 [ `Selecting` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting.aspx), 정렬 식을 지정 하기 위해 기회를 제공 하는 합니다. `Selecting` 형식의 개체를 전달 된 이벤트 처리기 [ `ObjectDataSourceSelectingEventArgs` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.aspx), 라는 속성이 있는 [ `Arguments` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.arguments.aspx) 형식의 [ `DataSourceSelectArguments` ](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)합니다. `DataSourceSelectArguments` 클래스는 데이터 소비자에 관련 된 데이터 요청 된 데이터 소스 제어를 전달 하기 위해 설계 되었으며 포함 한 [ `SortExpression` 속성](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.sortexpression.aspx)합니다.

에 대 한 이벤트 처리기를 만들고 정렬 정보를 ASP.NET 페이지에서는 ObjectDataSource를 전달 하려면는 `Selecting` 이벤트 및 다음 코드를 사용 하 여:


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample2.vb)]

*sortExpression* 값 (예: ProductName) 하 여 데이터를 정렬 하려면 데이터 필드의 이름을 할당 해야 합니다. 정렬 방향 관련 속성은, 데이터를 내림차순으로 정렬 하려면 DESC 문자열을 추가 하므로 하는 *sortExpression* 값 (예: ProductName DESC).

계속 해 서 일부 다른 하드 코드 된 값에 대 한 *sortExpression* 및 브라우저에서 결과 테스트 합니다. 그림 4와 같이로 ProductName DESC를 사용 하는 경우는 *sortExpression*, 제품 이름에 내림차순으로 정렬 됩니다.


[![제품 이름 역방향 사전순에서으로 정렬 됩니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image11.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image10.png)

**그림 4**: The 제품 이름 역방향 사전순에서으로 정렬 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image12.png))


## <a name="step-4-creating-the-sorting-interface-and-remembering-the-sort-expression-and-direction"></a>4 단계: 정렬 인터페이스 만들기 및 정렬 식 및 방향 기억

LinkButton 각 s 정렬 가능한 필드 머리글 텍스트 변환 정렬 GridView에서 지원을 설정 하는를 클릭 하면 데이터를 그에 따라 정렬 합니다. 해당 정렬 인터페이스에 해당 데이터 깔끔하게 레이아웃을 열에 GridView에 대 한 합리적입니다. DataList 및 반복기 컨트롤에 대 한 반면 다른 정렬 인터페이스 필요 합니다. 목록이 데이터 그리드), (반대로 데이터에 대 한 공통 정렬 인터페이스에는 데이터를 정렬할 수 있는 필드를 제공 하는 드롭다운 목록입니다. 이 자습서에 대 한 이러한 인터페이스를 구현 하는 s를 사용 합니다.

위의 DropDownList 웹 컨트롤을 추가 `SortableProducts` 반복기 집합과 해당 `ID` 속성을 `SortBy`합니다. 속성 창에서 줄임표는 `Items` 속성을 목록 항목 컬렉션 편집기를 표시 합니다. 추가 `ListItem` s로 데이터를 정렬 하는 `ProductName`, `CategoryName`, 및 `SupplierName` 필드입니다. 또한 추가 `ListItem` 제품 이름에 내림차순으로 정렬 합니다.

`ListItem` `Text` 속성 (예: 이름) 값으로 설정할 수 있습니다 하지만 `Value` 속성 (예: ProductName) 데이터 필드의 이름으로 설정 되어 있어야 합니다. 내림차순으로 정렬 결과 정렬 하려면 DESC 문자열 데이터 필드 이름을 ProductName DESC 등을 추가 합니다.


![각 정렬 가능한 데이터 필드에 대 한 목록 항목 추가](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image13.png)

**그림 5**: 추가 된 `ListItem` 각각의 정렬 가능한 데이터 필드에 대 한


마지막으로, 오른쪽 드롭다운 목록에 Button 웹 컨트롤을 추가 합니다. 설정의 `ID` 를 `RefreshRepeater` 및 해당 `Text` 속성 새로 고침을 합니다.

만든 후의 `ListItem` DropDownList 및 단추 s 선언적 구문 다음과 비슷해야 s 및 새로 고침 단추를 추가 합니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample3.aspx)]

전체 정렬 DropDownList와 다음 업데이트 해야 ObjectDataSource s `Selecting` 이벤트 처리기를 사용 하 여 선택한 `SortBy``ListItem` s `Value` 하드 코드 된 정렬 식 달리 속성입니다.


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample4.vb)]

페이지를 처음 방문할 때 지정 된이 위치에는 제품 순서로 정렬 되어 여는 `ProductName` 데이터 필드를 s는 `SortBy` `ListItem` 기본적으로 선택 (그림 6 참조). 다른 옵션 범주와 같이 정렬 및 새로 고침을 클릭 하면 선택 다시 게시 되며 그림 7 볼 수 있듯이 범주 이름을 사용 하 여 데이터를 다시 정렬 합니다.


[![제품이 처음 이름 기준으로 정렬 됩니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image15.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image14.png)

**그림 6**: The 제품은 처음 이름 기준으로 정렬 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image16.png))


[![제품은 범주별으로 정렬 됩니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image18.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image17.png)

**그림 7**: The 제품은 이제 범주별으로 정렬 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image19.png))


> [!NOTE]
> 새로 고침 단추를 클릭 하면 데이터를 자동으로 다시 정렬 된 반복기의 뷰 상태에서 사용 하지 않으므로 클라이언트별 포스트백이 발생할 때마다 해당 데이터 소스에 다시 바인딩하려면 반복. 적 왼쪽 정렬 변경 사용 반복기의 뷰 상태 드롭 다운 목록 t 성공한 경우에 적용 정렬 순서에 있습니다. 이 해결 하려면 새로 고침 단추에 대 한 이벤트 처리기를 만들고 `Click` 이벤트 및 데이터 원본에 반복 rebind (s 반복기를 호출 하 여 `DataBind()` 메서드).


## <a name="remembering-the-sort-expression-and-direction"></a>정렬 식 및 방향 기억

비 정렬 포스트백이 발생할 수 있습니다, 관련 된 페이지에 정렬 가능한 DataList 또는 반복기를 만들 때 것 s 명령적 정렬 식과 방향을 게시할 기억할 수 있습니다. 예를 들어 각 제품 삭제 단추를 포함 하려면이 자습서의 반복으로 업데이트 되었습니다 한다고 가정 합니다. 삭제 단추를 클릭할 때 d에서는 선택된 된 제품 삭제 한 다음 데이터 반복을 다시 바인딩해야 하는 코드를 실행 합니다. 정렬 세부 정보가 다시 게시를 통해 유지 되지 화면에 표시 되는 데이터 원본 정렬 순서로 되돌아갑니다.

이 자습서에서는 DropDownList 암시적으로 정렬 식과 방향을에 저장 뷰 상태의을 수행해 줍니다. 하나는 다른 정렬 인터페이스와 다양 한 정렬 옵션을 제공 하는 예를 들어, 링크 단추가 사용할 d를 해야 게시할 정렬 순서를 기억 하지 않도록 주의 합니다. 이 쿼리 문자열에 또는 다른 상태 지 속성 기술을 통해 정렬 매개 변수를 포함 하 여 페이지의 뷰 상태에 정렬 매개 변수를 저장 하 여 수행할 수 없습니다.

이 자습서의 이후 예제 페이지의 뷰 상태에서 정렬 세부 정보를 저장 하는 방법을 살펴봅니다.

## <a name="step-5-adding-sorting-support-to-a-datalist-that-uses-default-paging"></a>5 단계: 기본 페이징을 사용 하 여 DataList에 정렬 기능 추가

에 [이전 자습서](paging-report-data-in-a-datalist-or-repeater-control-vb.md) 기본 페이징 사용을 구현 하는 방법을 검사 했습니다. S 페이징된 데이터 정렬 기능을 포함 하도록 이전 예제를 확장할 수 있도록 합니다. 열어 시작는 `SortingWithDefaultPaging.aspx` 및 `Paging.aspx` 페이지에 `PagingSortingDataListRepeater` 폴더입니다. `Paging.aspx` 페이지에서 페이지 s 선언적 태그를 보려면 원본 단추를 클릭 합니다. 선택한 텍스트를 복사 (그림 8 참조)의 선언 태그에 붙여 넣습니다 `SortingWithDefaultPaging.aspx` 사이 `<asp:Content>` 태그입니다.


[![복제에 선언적 태그는 &lt;asp: Content&gt; 태그는 Paging.aspx SortingWithDefaultPaging.aspx](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image21.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image20.png)

**그림 8**: 복제에 선언적 태그는 `<asp:Content>` 에서 태그를 삽입 `Paging.aspx` 를 `SortingWithDefaultPaging.aspx` ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image22.png))


선언적 태그를 복사한 후 복사 메서드와 속성에는 `Paging.aspx` s 코드 숨김 클래스에 대 한 코드 숨김 클래스를 페이지 `SortingWithDefaultPaging.aspx`합니다. 다음으로를 보려면 잠시는 `SortingWithDefaultPaging.aspx` 브라우저에서 페이지입니다. 동일한 기능 및 모양으로 나타내야 `Paging.aspx`합니다.

## <a name="enhancing-productsbll-to-include-a-default-paging-and-sorting-method"></a>페이징 및 정렬 방법을 기본값을 포함 하도록 ProductsBLL 향상

이전 자습서에서 만든는 `GetProductsAsPagedDataSource(pageIndex, pageSize)` 에서 메서드는 `ProductsBLL` 반환 되는 클래스는 `PagedDataSource` 개체입니다. 이 `PagedDataSource` 개체는로 채워 졌 *모든* 제품 (BLL s 통해 `GetProducts()` 메서드)에 바인딩되면 DataList는 레코드에 해당 하는 지정 된 하지만 *pageIndex* 및 *pageSize* 입력된 매개 변수가 표시 되었습니다.

이 자습서의 앞부분에 나오는 ObjectDataSource s에서 정렬 식을 지정 하 여 정렬 지원을 추가 `Selecting` 이벤트 처리기입니다. 이 효과적으로 작동는 ObjectDataSource 같은 정렬 될 수 있는 개체를 반환 될 때는 `ProductsDataTable` 에서 반환 되는 `GetProducts()` 메서드 합니다. 그러나는 `PagedDataSource` 에서 반환 된 개체는 `GetProductsAsPagedDataSource` 메서드 내부 데이터 소스의 정렬을 지원 하지 않습니다. 반환 된 결과 정렬 해야 대신는 `GetProducts()` 메서드 *전에* 넣을까요는 `PagedDataSource`합니다.

이 수행 하기에 새 메서드를 만들는 `ProductsBLL` 클래스 `GetProductsSortedAsPagedDataSource(sortExpression, pageIndex, pageSize)`합니다. 정렬 하려면는 `ProductsDataTable` 에서 반환 되는 `GetProducts()` 메서드를 지정 된 `Sort` 의 기본 속성 `DataTableView`:


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample5.vb)]

`GetProductsSortedAsPagedDataSource` 메서드 약간만 다릅니다에서 `GetProductsAsPagedDataSource` 이전 자습서에서 만든 메서드. 특히, `GetProductsSortedAsPagedDataSource` 추가 입력된 매개 변수를 허용 `sortExpression` 이 값을 할당 하 고는 `Sort` 의 속성은 `ProductDataTable` s `DefaultView`합니다. 이상 버전에서는 코드 몇 줄의 `PagedDataSource` s 데이터 원본 개체를 할당 하는 `ProductDataTable` s `DefaultView`합니다.

## <a name="calling-the-getproductssortedaspageddatasource-method-and-specifying-the-value-for-the-sortexpression-input-parameter"></a>GetProductsSortedAsPagedDataSource 메서드를 호출 하 고 SortExpression 입력 매개 변수 값 지정

와 `GetProductsSortedAsPagedDataSource` 전체 메서드를 다음 단계는이 매개 변수에 대 한 값을 제공 합니다. ObjectDataSource에서 `SortingWithDefaultPaging.aspx` 현재 호출 하도록 구성 되어는 `GetProductsAsPagedDataSource` 메서드와 2를 통해 두 개의 입력된 매개 변수를 전달 `QueryStringParameters`에 지정 하는 `SelectParameters` 컬렉션입니다. 이 두 `QueryStringParameters` 있음을 대 한 소스는 `GetProductsAsPagedDataSource` s 메서드에 *pageIndex* 및 *pageSize* querystring 필드에서 매개 변수를 가져오는 `pageIndex` 및 `pageSize`합니다.

ObjectDataSource s 업데이트 `SelectMethod` 속성이 새 호출 한다는 있도록 `GetProductsSortedAsPagedDataSource` 메서드. 그런 다음 새 추가 `QueryStringParameter` 있도록는 *sortExpression* 입력된 매개 변수 querystring 필드에서 액세스 하는 `sortExpression`합니다. 설정의 `QueryStringParameter` s `DefaultValue` ProductName을 합니다.

이러한 변경 된 후 ObjectDataSource s 선언 태그는 같습니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample6.aspx)]

이 시점에서 `SortingWithDefaultPaging.aspx` 페이지는 그 결과 사전순 정렬 제품 이름으로 (그림 9 참조). 기본적으로 값이 ProductName 변수로 전달 됩니다 때문에 이것이 `GetProductsSortedAsPagedDataSource` s 메서드에 *sortExpression* 매개 변수입니다.


[![기본적으로 결과 제품 이름별으로 정렬](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image24.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image23.png)

**그림 9**: 기본적으로 결과 기준으로 정렬 됩니다 `ProductName` ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image25.png))


수동으로 추가 하는 경우는 `sortExpression` querystring 필드와 같은 `SortingWithDefaultPaging.aspx?sortExpression=CategoryName` 결과 정렬에서 지정 된 `sortExpression`합니다. 그러나이 `sortExpression` 매개 변수 데이터의 다른 페이지로 이동할 때 쿼리 문자열에 포함 되지 않습니다. 실제로로 다시 우리는 단추 다음] 또는 [마지막 페이지에서 클릭 하면 `Paging.aspx`! 또한 없어 s 현재 정렬 없음 인터페이스입니다. 사용자는 페이징된 데이터의 정렬 순서를 변경할 수 하는 유일한 방법은 쿼리 문자열을 직접 조작 하 여입니다.

## <a name="creating-the-sorting-interface"></a>정렬 인터페이스 만들기

먼저 업데이트 해야는 `RedirectUser` 메서드를 사용자에 게 보낼를 `SortingWithDefaultPaging.aspx` (대신 `Paging.aspx`)를 포함 하려면는 `sortExpression` 쿼리 문자열의 값입니다. 읽기 전용 페이지 수준 라는 추가 해야 `SortExpression` 속성입니다. 이 속성을 비슷합니다는 `PageIndex` 및 `PageSize` 이전 자습서에서 만든 속성의 값을 반환는 `sortExpression` 이 특성이 있으면 쿼리 문자열 필드의 기본 최대값 (ProductName) 그렇지 않은 경우.

현재는 `RedirectUser` 메서드는 하나의 입력된 매개 변수만 표시 하려면 페이지의 인덱스를 허용 합니다. 그러나 사용자는 쿼리 문자열에 지정 된 어떤 s 이외의 정렬 식을 사용 하 여 데이터의 특정 페이지를 리디렉션합니다 하고자 하는 경우 시간이 있을 수 있습니다. 잠시 후에 일련의 지정한 열에 의해 데이터 정렬에 대 한 Button 웹 컨트롤을 포함 하는이 페이지에 대 한 정렬 인터페이스를 만들어 보겠습니다. 이러한 단추 중 하나를 클릭할 때 적절 한 정렬 식 값을 전달 하는 사용자를 리디렉션하는 것이 좋습니다. 이 기능을 제공 하려면 두 가지 버전의 만듭니다는 `RedirectUser` 메서드. 첫 번째는 두 번째 페이지 인덱스와 정렬 식을 허용 하는 동안 표시할 페이지 인덱스만 사용 해야 합니다.


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample7.vb)]

이 자습서의 첫 번째 예에서 DropDownList를 사용 하 여 정렬 인터페이스를 만들었습니다. 이 예제에서는 let s 사용 하 여 정렬에 대 한 하나 DataList 위에 배치 하는 세 가지 Button 웹 컨트롤 `ProductName`이며 다음 중 하나에 대 한 `CategoryName`, 되 고 다른 하나 `SupplierName`합니다. 설정에 세 개의 단추 웹 컨트롤을 추가 자신의 `ID` 및 `Text` 속성 적절 하 게 합니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample8.aspx)]

다음으로 만듭니다는 `Click` 각각에 대 한 이벤트 처리기입니다. 이벤트 처리기를 호출 해야 합니다는 `RedirectUser` 메서드를 적절 한 정렬 식을 사용 하 여 첫 번째 페이지에 사용자를 반환 합니다.


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample9.vb)]

데이터 제품 이름별 사전순으로 정렬 되므로 페이지 처음 방문 하는 경우 (그림 9를 다시 참조). 데이터의 두 번째 페이지로 이동한 다음 정렬 범주 단추를 클릭 하 고 다음 단추를 클릭 합니다. 이렇게 우리 범주 이름별으로 정렬 된 데이터의 첫 번째 페이지로 반환 (그림 10 참조). 마찬가지로, 공급자 단추 정렬 클릭 하면 데이터의 첫 페이지부터 시작 하는 공급자를 통해 데이터를 정렬 합니다. 으로 통해 페이징 되는 데이터 정렬 선택 기억 됩니다. 그림 11 범주별으로 정렬 하 고 데이터의 열 세 번째 페이지로 이동한 다음 페이지를 보여줍니다.


[![제품은 범주별으로 정렬 되며](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image27.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image26.png)

**그림 10**: The 제품 범주별으로 정렬 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image28.png))


[![정렬 식은 기억 때 페이징를 통해 데이터를](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image30.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image29.png)

**그림 11**:의 정렬 식은 기억 때 페이징 통해 Data ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image31.png))


## <a name="step-6-custom-paging-through-records-in-a-repeater"></a>한 반복기의 레코드를 통해 사용자 지정 페이징 6 단계:

DataList 예제 단계에서 비효율적인 기본 페이징 기술을 사용 하 여 해당 데이터를 통해 5 페이지를 검사 합니다. 충분히 많은 양의 데이터를 페이징 하는 경우 반드시 사용자 지정 페이징을 사용할 수 있습니다. 에 [효율적으로 통해 큰 크기의 데이터를 페이징](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md) 및 [사용자 지정 페이징 데이터 정렬](../paging-and-sorting/sorting-custom-paged-data-vb.md) 자습서에 대 한 BLL에 기본 및 사용자 지정 페이징 및 만든된 메서드 간의 차이 검사 했습니다 사용자 지정 페이징 및 정렬 사용자 지정 페이징된 데이터를 활용할 수 있습니다. 특히이 두 이전 자습서에 추가한 이유를 다음 세 가지 방법에서 `ProductsBLL` 클래스:

- `GetProductsPaged(startRowIndex, maximumRows)` 시작 하는 레코드의 특정 하위 집합을 반환 *startRowIndex* 초과 하지 않는 및 *maximumRows*합니다.
- `GetProductsPagedAndSorted(sortExpression, startRowIndex, maximumRows)` 레코드에서 지정 된 정렬의 특정 하위 집합을 반환 *sortExpression* 입력된 매개 변수입니다.
- `TotalNumberOfProducts()` 에 있는 레코드의 총 수를 제공는 `Products` 데이터베이스 테이블입니다.

이러한 메서드를 효율적으로 페이지 및 정렬 DataList 또는 반복기 컨트롤을 사용 하 여 데이터를 통해 사용할 수 있습니다. 이 설명 하기 s 페이징 지원을 사용자 지정 된 반복기 컨트롤을 만들어 시작 사용 그런 다음 정렬 기능을 추가 합니다.

열기는 `SortingWithCustomPaging.aspx` 페이지에 `PagingSortingDataListRepeater` 폴더 설정 페이지에는 반복기를 추가 하 고 해당 `ID` 속성을 `Products`합니다. 반복기 s 스마트 태그를 만들고 라는 새 ObjectDataSource `ProductsDataSource`합니다. 해당 데이터를 선택 하도록 구성 된 `ProductsBLL` s 클래스 `GetProductsPaged` 메서드.


[![ObjectDataSource ProductsBLL 클래스의 GetProductsPaged 메서드를 사용 하도록 구성](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image33.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image32.png)

**그림 12**: 구성에 사용 하 여 ObjectDataSource는 `ProductsBLL` s 클래스 `GetProductsPaged` 메서드 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image34.png))


삽입, 업데이트에서 드롭 다운 목록을 설정 하 고 탭 (없음)을 삭제 한 다음 다음 단추를 클릭 합니다. 데이터 소스 구성 마법사에서 이제 원본에 대 한 요구는 `GetProductsPaged` s 메서드에 *startRowIndex* 및 *maximumRows* 입력 매개 변수입니다. 실제로 이러한 입력된 매개 변수는 무시 됩니다. 대신,는 *startRowIndex* 및 *maximumRows* 값을 통해 전달 됩니다는 `Arguments` ObjectDataSource s에서 속성 `Selecting` 지정 방법을 마찬가지로 이벤트 처리기는 *sortExpression* 이 자습서 s 첫 번째 데모입니다. 따라서 매개 변수 소스를 없음에서 설정 마법사에서 드롭 다운 목록을 유지 합니다.


[![None으로 매개 변수 원본 집합을 그대로 둡니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image36.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image35.png)

**그림 13**: None으로 매개 변수가 소스 설정 유지 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image37.png))


> [!NOTE]
> 수행 *하지* ObjectDataSource s 설정 `EnablePaging` 속성을 `true`합니다. 이렇게 하면 자동으로 자체를 포함 하도록 ObjectDataSource *startRowIndex* 및 *maximumRows* 에 매개 변수는 `SelectMethod` s 기존 매개 변수 목록입니다. `EnablePaging` 바인딩 사용자 지정 이러한 컨트롤의 ObjectDataSource에서 특정 동작을 예상 하기 때문에 GridView, DetailsView, 또는 FormView 컨트롤에 데이터를 페이징 하는 경우 속성이 유용 합니다. 경우에만 사용할 수 `EnablePaging` 속성은 `true`합니다. DataList 및 반복기에 대 한 페이징 지원을 수동으로 추가 했기 때문에이 속성을 설정 둡니다 `false` (기본값) 이면 가격 ASP.NET 페이지 내에서 직접 필요한 기능에 빵 할인 됩니다 것 처럼 합니다.


마지막으로, 정의 s 반복기 `ItemTemplate`의 제품 이름, 범주 및 공급 업체 표시 되도록 합니다. 이러한 변경 된 후 반복기 및 ObjectDataSource s 선언적 구문 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample10.aspx)]

잠시 브라우저를 통해 페이지를 방문 하 여 레코드가 반환 됩니다. ¿¡´ म 지정 하려면 아직 했습니다는 *startRowIndex* 및 *maximumRows* 매개 변수 값이 있습니다; 따라서 0 값 전달 되 고에 모두에 대 한 합니다. ObjectDataSource s에 대 한 이벤트 처리기를 만들고 이러한 값을 지정 하려면 `Selecting` 이벤트 및 이러한 매개 변수 값을 프로그래밍 방식으로 0에서 5의 하드 코드 된 값에 각각 설정:


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample11.vb)]

이러한 변경으로 인해 브라우저를 통해 볼 때 페이지는 처음 다섯 개의 제품을 표시 합니다.


[![처음 다섯 개의 레코드가 표시](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image39.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image38.png)

**그림 14**: The 처음 다섯 개의 레코드가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image40.png))


> [!NOTE]
> 그림 14에 나열 된 제품은 있다면 해당 설정 때문에 제품 이름으로 정렬할 수는 `GetProductsPaged` 하 여 결과 정렬 하는 효율적인 사용자 지정 페이징 쿼리를 수행 하는 저장된 프로시저 `ProductName`합니다.


사용자 페이지를 단계별로 실행 되도록 할 수 있도록, 시작 하는 행 인덱스 및 최대 행 기억 하 고 이러한 값 게시할 필요 합니다. 기본 페이징 예에 이러한 값을 유지 하도록 querystring 필드 사용 이 데모에서는 s 페이지의 뷰 상태에이 정보를 저장 하도록 합니다. 다음 두 속성을 만듭니다.


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample12.vb)]

사용 하도록 선택 하면 이벤트 처리기에서 코드를 다음으로 업데이트는 `StartRowIndex` 및 `MaximumRows` 0에서 5의 하드 코드 된 값 대신 속성:


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample13.vb)]

이 시점에서 가격 페이지에는 여전히 처음 다섯 개의 레코드만 표시 됩니다. 그러나 이러한 속성이 있는 원위치에서 준비 된 우리의 페이징 인터페이스를 만들 수 있습니다.

## <a name="adding-the-paging-interface"></a>페이징 인터페이스 추가

Let 사용 하 여 동일한 첫 번째, Previous, 마지막 페이징 다음 인터페이스 사용 Label 웹 페이지에 데이터의 관계를 표시 하는 컨트롤은 보고를 포함 하 여 기본 페이징 예제와 총 페이지 수가 존재 합니다. 네 개의 단추 웹 컨트롤 및 반복 아래에 레이블을 추가 합니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample14.aspx)]

다음으로 만듭니다 `Click` 네 개의 단추에 대 한 이벤트 처리기입니다. 이러한 단추 중 하나를 클릭할 때 업데이트 해야는 `StartRowIndex` 데이터 반복에 다시 바인딩합니다. 첫 번째, 이전 및 다음 단추에 대 한 코드는 간단 하지만 마지막 단추에 대 한 확인 하려면 어떻게 해야에서는 데이터의 마지막 페이지에 대 한 시작 행 인덱스? 계산 총에서 레코드 수를 알고 있어야 다음 및 마지막 단추를 활성화할지 여부를 결정할 수 있다는 뿐만 아니라이 인덱스를 통해 호출이 전달 됩니다. 이 호출 하 여 확인할 수 있습니다는 `ProductsBLL` s 클래스 `TotalNumberOfProducts()` 메서드. Let s 이라는 읽기 전용, 페이지 수준 속성을 만들 `TotalRowCount` 의 결과 반환 하는 `TotalNumberOfProducts()` 메서드:


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample15.vb)]

이 속성을 통해 이제 마지막 페이지의 시작 행 인덱스를 확인할 수 있습니다. 특히, s 정수 결과의 `TotalRowCount` 로 나눈 값 1을 뺀 값 `MaximumRows`를 곱한 값으로 `MaximumRows`합니다. 작성할 수 있습니다는 `Click` 페이징 인터페이스 단추 4 개에 대 한 이벤트 처리기.


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample16.vb)]

마지막으로, 마지막 페이지를 볼 때 데이터와 다음 및 마지막 단추의 첫 번째 페이지를 볼 때 페이징 인터페이스에서 첫 번째 및 이전 단추를 사용 하지 않도록 설정 해야 합니다. 이를 위해 ObjectDataSource s에 다음 코드를 추가 `Selecting` 이벤트 처리기.


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample17.vb)]

이러한를 추가한 후 `Click` 이벤트 처리기와 현재 시작 행 인덱스를 기반으로 페이징 인터페이스 요소를 사용 하지 않도록 설정 하거나 설정 하려면 코드 브라우저에서 페이지를 테스트 합니다. 그림 15에서는 첫 번째 페이지를 처음 방문할 때 및 이전 단추는 사용할 수 없습니다. 마지막을 클릭 하면 마지막 페이지를 표시 하는 동안 데이터의 두 번째 페이지 다음을 클릭 하면 표시 (그림 16 및 17 참조). 데이터의 마지막 페이지를 볼 때 다음와 마지막 단추가 비활성화 됩니다.


[![첫 번째 제품 페이지를 볼 때 이전 및 마지막 단추가 비활성화 됩니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image42.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image41.png)

**그림 15**: 제품의 첫 번째 페이지를 볼 때 이전 및 마지막 단추가 비활성화 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image43.png))


[![두 번째 페이지의 제품은 표시](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image45.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image44.png)

**그림 16**:의 두 번째 페이지의 제품을 표시 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image46.png))


[![마지막 데이터의 마지막 페이지 표시를 클릭합니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image48.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image47.png)

**그림 17**: 마지막을 클릭 하면 마지막 페이지의 데이터 표시 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image49.png))


## <a name="step-7-including-sorting-support-with-the-custom-paged-repeater"></a>7 단계: 반복기 페이징 지원을 사용자 지정 정렬 포함

사용자 지정 페이징을 구현 했으므로 준비 된 정렬 포함 하도록 지원 합니다. `ProductsBLL` s 클래스 `GetProductsPagedAndSorted` 메서드에 동일한 *startRowIndex* 및 *maximumRows* 입력으로 매개 변수 `GetProductsPaged`, 추가 허용 하지만  *sortExpression* 입력된 매개 변수입니다. 사용 하는 `GetProductsPagedAndSorted` 메서드에서 `SortingWithCustomPaging.aspx`, 다음 단계를 수행 해야 합니다.

1. ObjectDataSource s 변경 `SelectMethod` 속성 `GetProductsPaged` 를 `GetProductsPagedAndSorted`합니다.
2. 추가 *sortExpression* `Parameter` ObjectDataSource s에 대 한 개체 `SelectParameters` 컬렉션입니다.
3. 페이지 수준은 private 만들기 `SortExpression`의 페이지 뷰 상태를 통해 다시 게시할 때마다 해당 값을 유지 하는 속성입니다.
4. ObjectDataSource s 업데이트 `Selecting` ObjectDataSource s 할당 하는 이벤트 처리기 *sortExpression* 매개 변수는 페이지 수준 값 `SortExpression` 속성입니다.
5. 정렬 인터페이스를 만듭니다.

ObjectDataSource s를 업데이트 하 여 시작 `SelectMethod` 속성과 추가 *sortExpression* `Parameter`합니다. 다음 사항을 확인는 *sortExpression* `Parameter` s `Type` 속성이 `String`합니다. 먼저 두 작업을 완료 한 후 ObjectDataSource s 선언 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample18.aspx)]

다음으로, 페이지 수준 필요 `SortExpression` 속성 값을 갖는 상태를 보려면 serialize 됩니다. 정렬 식 값에 설정한 경우 기본적으로 ProductName을 사용 합니다.


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample19.vb)]

ObjectDataSource는 호출 전에 `GetProductsPagedAndSorted` 하도록 설정 해야 하는 메서드는 *sortExpression* `Parameter` 의 값에는 `SortExpression` 속성입니다. 에 `Selecting` 이벤트 처리기 코드의 다음 줄 추가:


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample20.vb)]

이제 남은 것 정렬 인터페이스를 구현 합니다. 마지막 예제에서 수행한 것 처럼 s 정렬 인터페이스를 구현한 결과 정렬 하는 데 사용할 수 있는 세 개의 단추 웹 컨트롤을 사용 하 여 제품 이름, 범주 또는 공급 업체를 사용 합니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample21.aspx)]

만들 `Click` 이 세 가지 단추 컨트롤에 대 한 이벤트 처리기입니다. 이벤트 처리기를 다시 설정는 `StartRowIndex` 0으로 설정 된 `SortExpression` 적절 한 값과 데이터를 반복 rebind를:


[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample22.vb)]

모두 완료 s가입니다! 다양 한 사용자 지정 페이징 및 정렬을 구현 하기 위한 단계의 라인일 단계 기본 페이징에 필요한 것과 매우 유사한 했습니다. 그림 18 범주별으로 정렬 하는 경우 데이터의 마지막 페이지를 볼 때의 제품을 표시 합니다.


[![데이터의 마지막 페이지, Sorted, 범주별으로 표시 됩니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image51.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image50.png)

**그림 18**:의 마지막 페이지의 데이터, Sorted, 범주별으로 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image52.png))


> [!NOTE]
> 이전 예제에서는 공급자 공급 업체 이름 정렬 식으로 사용 하 여 정렬할 때 지정 합니다. 그러나 사용자 지정 페이징 구현에 대 한 해야 CompanyName을 사용 합니다. ¿¡´ 사용자 지정 페이징을 구현 해야 하는 저장된 프로시저 `GetProductsPagedAndSorted` 에 정렬 식을 전달는 `ROW_NUMBER()` 키워드는 `ROW_NUMBER()` 키워드 별칭 대신 실제 열 이름이 필요 합니다. 사용해선 따라서 `CompanyName` (의 열 이름에서 `Suppliers` 테이블)에 사용 되는 별칭 대신는 `SELECT` 쿼리 (`SupplierName`) 정렬 식에 대 한 합니다.


## <a name="summary"></a>요약

모두 DataList 또는 반복기 제공 기본 제공 정렬을 지원 하지만 약간 코드와 사용자 지정 정렬 인터페이스의 이러한 기능을 추가할 수 있습니다. 정렬 식을 통해 지정할 수 있습니다를 정렬 하지만 하지 페이징을 구현할 때는 `DataSourceSelectArguments` ObjectDataSource s에 전달 된 개체 `Select` 메서드. 이 `DataSourceSelectArguments` 개체 s `SortExpression` ObjectDataSource s에서 속성을 지정할 수 있습니다 `Selecting` 이벤트 처리기입니다.

DataList 또는 이미 페이징 지원을 제공 하는 반복기에 정렬 기능을 추가 하려면 정렬 식을 허용 하는 메서드를 포함 하도록 비즈니스 논리 계층을 사용자 지정 하는 가장 쉬운 방법이입니다. 이 정보 다음에 ObjectDataSource s에서 매개 변수를 통해 전달할 수 `SelectParameters`합니다.

이 자습서는 페이징 및 정렬과 DataList 및 반복기 컨트롤과 우리의 검사를 완료 합니다. 이 다음 및 최종 자습서 항목 단위 별로 일부 사용자 지정, 사용자가 시작한 기능을 제공 하기 위해 DataList 및 반복기 s 템플릿에 Button 웹 컨트롤을 추가 하는 방법을 검사 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 David Suru 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](paging-report-data-in-a-datalist-or-repeater-control-vb.md)
