---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-cs
title: DataList 또는 Repeater 컨트롤 (C#)에서 데이터 정렬 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 정렬 DataList 및 반복기를의 지원을 포함 하는 방법 뿐만 아니라 데이터 수 DataList 또는 반복기를 생성 하는 방법을 살펴보겠습니다...
ms.author: riande
ms.date: 11/13/2006
ms.assetid: f52c302a-1b7c-46fe-8a13-8412c95cbf6d
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 05fbc51d5341a4d3d634cbbc05c0e66a827b0394
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837847"
---
<a name="sorting-data-in-a-datalist-or-repeater-control-c"></a>DataList 또는 Repeater 컨트롤 (C#)에서 데이터 정렬
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_45_CS.exe) 또는 [PDF 다운로드](sorting-data-in-a-datalist-or-repeater-control-cs/_static/datatutorial45cs1.pdf)

> 이 자습서에서는 정렬 DataList 및 반복기를의 지원을 포함 하는 방법 뿐만 아니라 DataList 또는 Repeater 데이터 페이징 및 정렬 수를 생성 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

에 [이전 자습서](paging-report-data-in-a-datalist-or-repeater-control-cs.md) DataList 페이징 지원을 추가 하는 방법을 살펴보았습니다. 새 메서드를 만들었습니다 합니다 `ProductsBLL` 클래스 (`GetProductsAsPagedDataSource`) 반환을 `PagedDataSource` 개체입니다. DataList 또는 Repeater에 바인딩된 경우 데이터의 요청 된 페이지만 DataList 또는 반복기를 만들 표시 됩니다. 이 기술을 사용 되는 것 내부적으로 GridView, FormView DetailsView 컨트롤에서 해당 기본 제공 페이징 기능을 제공 하는 것과 비슷합니다.

페이징 지원을 제공 하는 것 외에도 GridView 정렬 지원을 즉시도 포함 됩니다. DataList 또는 Repeater 모두 기본 제공 정렬 기능이 있습니다. 그러나 정렬 기능을 약간의 코드를 사용 하 여 추가할 수 있습니다. 이 자습서에서는 정렬 DataList 및 반복기를의 지원을 포함 하는 방법 뿐만 아니라 DataList 또는 Repeater 데이터 페이징 및 정렬 수를 생성 하는 방법을 살펴보겠습니다.

## <a name="a-review-of-sorting"></a>정렬에 대 한 검토

설명한 것 처럼 합니다 [페이징 및 정렬 보고서 데이터](../paging-and-sorting/paging-and-sorting-report-data-cs.md) 자습서에서는 GridView 컨트롤 정렬 지원을 기본으로 제공 합니다. 각 GridView 필드 연결 되어 있을 수 있습니다 `SortExpression`, 데이터 정렬에 사용 되는 데이터 필드를 나타냅니다. 때 GridView s `AllowSorting` 속성이로 설정 되어 `true`,이 있는 각 GridView 필드는 `SortExpression` 속성 값에 해당 헤더는 LinkButton으로 렌더링 합니다. 사용자가 특정 GridView 필드의 헤더를 클릭 하면 포스트백이 발생할 및 s 클릭할된 필드에 따라 데이터를 정렬 `SortExpression`합니다.

GridView 컨트롤에는 `SortExpression` 속성을 저장 하는 `SortExpression` GridView 필드의 데이터를 정렬할 때. 또한는 `SortDirection` 속성 데이터를 오름차순 또는 내림차순 (경우 특정 GridView의 필드 헤더의에서 링크를 두 번 연속으로 정렬 순서 토글은 사용자가 클릭)에서 정렬 하는 여부를 나타냅니다.

핸드 오프 GridView 데이터 소스 컨트롤에 바인딩되면 해당 `SortExpression` 및 `SortDirection` 속성을 데이터 소스 제어 합니다. 데이터 소스 컨트롤이 데이터를 검색 한 다음에 따라 제공 된 정렬 `SortExpression` 고 `SortDirection` 속성입니다. 데이터 정렬 후 데이터 소스 컨트롤 GridView에 반환 합니다.

DataList 또는 Repeater 컨트롤을 사용 하 여이 기능을 복제 해야 합니다.

- 정렬 인터페이스 만들기
- 데이터 필드를 기준으로 정렬 및 오름차순 또는 내림차순으로 정렬할 것인지
- 특정 데이터 필드에 따라 데이터를 정렬 하는 ObjectDataSource를 지시 합니다.

에서는에서는 3 및 4 단계에서 이러한 세 가지 작업을 수행할 수 있습니다. 그런 다음, 페이징 및 정렬 DataList 또는 반복기에 대 한 지원을 포함 하는 방법을 살펴보겠습니다.

## <a name="step-2-displaying-the-products-in-a-repeater"></a>2 단계: Repeater에 제품 표시

정렬 관련 기능을 구현 하는 방법에 대 한 걱정 했습니다 전에 s를 반복기 컨트롤에서 제품을 나열 하 여 시작할 수 있습니다. 열어서 시작 합니다 `Sorting.aspx` 페이지에 `PagingSortingDataListRepeater` 폴더입니다. Repeater 컨트롤을 웹 페이지, 설정 추가 해당 `ID` 속성을 `SortableProducts`입니다. 반복기가 스마트 태그를 명명 된 새 ObjectDataSource를 만들 `ProductsDataSource` 에서 데이터를 검색 하도록 구성 하는 `ProductsBLL` s 클래스 `GetProducts()` 메서드. INSERT, UPDATE 및 DELETE 탭의 드롭다운 목록에서 옵션 (없음)을 선택 합니다.


[![ObjectDataSource를 만들고 GetProductsAsPagedDataSource() 메서드를 사용 하도록 구성](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image2.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image1.png)

**그림 1**: ObjectDataSource를 만들고 사용 하도록 구성 된 `GetProductsAsPagedDataSource()` 메서드 ([클릭 하 여 큰 이미지 보기](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image3.png))


[![UPDATE, INSERT에에서 드롭다운 목록이 설정 하 고 탭 (없음)을 삭제 합니다.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image5.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image4.png)

**그림 2**: UPDATE, INSERT에에서 드롭다운 목록이 설정 하 고 탭 (없음)을 삭제 ([큰 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image6.png))


와 달리, DataList를 사용 하 여 Visual Studio 자동으로 만들지 않으므로 `ItemTemplate` Repeater 컨트롤 데이터 소스에 바인딩한 후에 대 한 합니다. 이 추가 해야 합니다 또한 `ItemTemplate` Repeater 컨트롤 s 스마트 태그에 s DataList 있는 템플릿 편집 옵션으로 선언적으로 합니다. S let을 사용 하 여 동일한 `ItemTemplate` 이전 자습서에서 표시 되는 s 제품 이름, 공급자 및 범주입니다.

추가한 후는 `ItemTemplate`, 반복기 및 ObjectDataSource가 선언적 태그는 다음과 유사 합니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample1.aspx)]

그림 3에서는 브라우저를 통해 볼 때이 페이지를 보여 줍니다.


[![각 제품의의 이름이, 공급자 및 범주에 표시 됩니다.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image8.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image7.png)

**그림 3**: 각 제품의 이름이, 공급자 및 범주에 표시 됩니다 ([큰 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image9.png))


## <a name="step-3-instructing-the-objectdatasource-to-sort-the-data"></a>3 단계: 데이터를 정렬 하려면 ObjectDataSource 지시

Repeater에 표시 되는 데이터를 정렬 하려면 사용 되는 데이터를 정렬 해야 하는 정렬 식의 ObjectDataSource를 알리기 위해 필요 합니다. 먼저 발생 ObjectDataSource 해당 데이터를 검색 하기 전에 해당 [ `Selecting` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting.aspx)에 정렬 식을 지정 하는 기회를 제공 하는 합니다. 합니다 `Selecting` 이벤트 처리기가 형식의 개체를 전달 [ `ObjectDataSourceSelectingEventArgs` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.aspx)에 라는 속성이 있는 [ `Arguments` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.arguments.aspx) 형식의 [ `DataSourceSelectArguments` ](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)합니다. `DataSourceSelectArguments` 클래스는 데이터 소스 컨트롤에 데이터의 소비자에서 데이터 관련 요청을 전달 하도록 설계 되었습니다 및 포함 된 [ `SortExpression` 속성](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.sortexpression.aspx)합니다.

정렬 정보를 ASP.NET 페이지에서 ObjectDataSource에 전달 하려면에 대 한 이벤트 처리기를 만들고는 `Selecting` 이벤트 및 다음 코드를 사용 합니다.


[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample2.cs)]

합니다 *sortExpression* 값 (예: ProductName)로 데이터를 정렬 하려면 데이터 필드의 이름을 할당 해야 합니다. 정렬 방향 관련 속성이 없는, 데이터를 내림차순으로 정렬 하려는 경우 따라서 문자열 DESC를 추가 하는 *sortExpression* 값 (예: ProductName DESC).

계속 해 서 일부 다른 하드 코드 된 값에 대 한 *sortExpression* 및 브라우저에서 결과 테스트 합니다. 그림 4 에서처럼,으로 ProductName DESC를 사용 하는 경우는 *sortExpression*, 제품 이름 역방향 사전순에서으로 정렬 됩니다.


[![제품 이름 역방향 사전순에서으로 정렬 됩니다.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image11.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image10.png)

**그림 4**: The 제품 역방향 사전순에서 이름별으로 정렬 됩니다 ([큰 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image12.png))


## <a name="step-4-creating-the-sorting-interface-and-remembering-the-sort-expression-and-direction"></a>4 단계: 정렬 인터페이스를 만드는 방법 및 정렬 식과 방향을 기억

각 정렬 가능한 필드의 헤더 텍스트 LinkButton 변환 정렬 GridView에 지원을 설정를 클릭 하면 데이터를 적절 하 게 정렬 합니다. 해당 정렬 인터페이스 GridView, 여기서 데이터 깔끔하게에 배치 된 열이 적합 합니다. DataList 및 반복기 컨트롤에 대 한 반면 다른 정렬 인터페이스가 필요 합니다. 데이터 그리드), (반대로 데이터의 목록을 정렬 공용 인터페이스에 사용 되는 데이터를 정렬할 수 있습니다 필드를 제공 하는 드롭다운 목록입니다. 이 자습서에 대 한 이러한 인터페이스를 구현 하는 s 수 있습니다.

위의 DropDownList 웹 컨트롤을 추가 합니다 `SortableProducts` Repeater 집합과 해당 `ID` 속성을 `SortBy`입니다. 속성 창에서 줄임표를 클릭 합니다 `Items` ListItem 컬렉션 편집기를 표시 하는 속성입니다. 추가 `ListItem` s로 데이터를 정렬 하는 `ProductName`를 `CategoryName`, 및 `SupplierName` 필드입니다. 추가할 수도 `ListItem` 제품 역방향 사전순에서 이름별으로 정렬 합니다.

합니다 `ListItem` `Text` 속성 (예: 이름) 값으로 설정할 수 있지만 `Value` 속성 (예: ProductName) 데이터 필드의 이름으로 설정 해야 합니다. 내림차순으로 정렬 결과 정렬 하려면 데이터 필드 이름 ProductName DESC 같은 문자열 DESC를 추가 합니다.


![ListItem 정렬 가능한 데이터 필드의 각 추가](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image13.png)

**그림 5**: 추가 된 `ListItem` 정렬 가능한 데이터 필드에 대해


마지막으로, DropDownList의 오른쪽에 단추 웹 컨트롤을 추가 합니다. 설정 해당 `ID` 하 `RefreshRepeater` 고 `Text` 속성 새로 고침을 합니다.

만든 후의 `ListItem` s 및 새로 고침 단추를 추가, DropDownList 및 단추 s 선언적 구문을 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample3.aspx)]

전체 정렬 DropDownList를 사용 하 여 다음 업데이트 해야 ObjectDataSource s `Selecting` 이벤트 처리기를 사용 하 여 선택한 `SortBy``ListItem` s `Value` 속성과 반대로 하드 코드 된 정렬 식입니다.


[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample4.cs)]

먼저 페이지를 방문 하는 경우이 시점에서 제품을 처음에 따라 정렬 됩니다는 `ProductName` 데이터 필드, s 합니다 `SortBy` `ListItem` 기본적으로 선택 (그림 6 참조). 다른 범주와 같은 옵션 정렬 및 새로 고침을 클릭 하면 선택 포스트백을 발생 되며 그림 7 있듯이 범주 이름으로 데이터를 다시 정렬 합니다.


[![제품은 처음 이름별으로 정렬](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image15.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image14.png)

**그림 6**: The 제품은 처음 이름별으로 정렬 ([큰 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image16.png))


[![제품은 이제 범주별으로 정렬](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image18.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image17.png)

**그림 7**: The 제품은 이제 범주별으로 정렬 ([큰 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image19.png))


> [!NOTE]
> 새로 고침 단추를 클릭 하면 데이터를 자동으로 다시 정렬 된 반복기가의 뷰 상태를 사용 하지 않도록 설정 하므로 클라이언트별 포스트백이 발생할 때마다 해당 데이터 원본에 바인딩할 반복기입니다. 적 왼쪽 반복기가의 뷰 상태를 사용 하도록 설정 정렬 변경 드롭다운에 어떤 영향을 정렬 순서에 미치는 t-이득 목록입니다. 이 문제를 해결 하려면 새로 고침 단추에 대 한 이벤트 처리기를 만듭니다 `Click` 이벤트 및 해당 데이터 원본에 대 한 반복기 rebind (s 반복기를 호출 하 여 `DataBind()` 메서드).


## <a name="remembering-the-sort-expression-and-direction"></a>정렬 식과 방향을 기억

정렬 되지 않은 관련 포스트백이 발생할 수 있는 페이지에 정렬 가능한 DataList 또는 반복기를 만들 때 해당 s 명령적 정렬 식과 방향을 다시 게시할 때마다 기억 됩니다. 예를 들어 각 제품에 삭제 단추를 포함 하려면이 자습서에서는 반복기를 업데이트 했습니다 한다고 가정 합니다. 삭제 단추를 클릭할 때 d에서는 선택한 제품을 삭제 하 고 다음 데이터는 반복기를 다시 바인딩해야 하는 코드를 실행 합니다. 정렬 세부 정보를 다시 게시를 통해 유지 되지 경우 화면에 표시 되는 데이터를 원래 정렬 순서 되돌아갑니다.

이 자습서에서는 DropDownList 암시적으로 정렬 식과 방향에에서 저장 해당 뷰 상태의 한 합니다. 에서는 하나는 다른 정렬 인터페이스와 함께 다양 한 정렬 옵션을 제공 하는 예를 들어 Linkbutton의 연결을 사용한 경우 d 해야 다시 게시할 때마다 정렬 순서를 기억 하도록 주의 합니다. 이 쿼리 문자열에 또는 다른 상태 지 속성 기술을 통해 정렬 매개 변수를 포함 하 여 페이지의 보기 상태의 정렬 매개 변수를 저장 하 여 수행할 수 없습니다.

이 자습서의 이후 예제 페이지의 보기 상태의 정렬 세부 정보를 유지 하는 방법을 살펴봅니다.

## <a name="step-5-adding-sorting-support-to-a-datalist-that-uses-default-paging"></a>5 단계: 기본 페이징을 사용 하는 DataList 정렬을 지원 추가

에 [이전 자습서](paging-report-data-in-a-datalist-or-repeater-control-cs.md) DataList와 함께 기본 페이징을 구현 하는 방법을 살펴보았습니다. S가 페이징된 데이터 정렬 하는 기능을 포함 하도록이 이전 예제를 확장할 수 있습니다. 열어서 시작 합니다 `SortingWithDefaultPaging.aspx` 및 `Paging.aspx` 페이지에 `PagingSortingDataListRepeater` 폴더입니다. `Paging.aspx` 페이지, 페이지 s 선언적 태그를 보려면 원본 단추를 클릭 합니다. 선택한 텍스트 복사 합니다 (그림 8 참조)의 선언 태그에 붙여 넣습니다 `SortingWithDefaultPaging.aspx` 간에 `<asp:Content>` 태그.


[![에 있는 선언적 태그를 복제 합니다 &lt;asp: Content&gt; SortingWithDefaultPaging.aspx Paging.aspx에서 태그](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image21.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image20.png)

**그림 8**:에 있는 선언적 태그를 복제 합니다 `<asp:Content>` 에서 태그 `Paging.aspx` 하 `SortingWithDefaultPaging.aspx` ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image22.png))


선언적 태그를 복사한 후의 속성과 메서드를 복사 합니다 `Paging.aspx` s 코드 숨김 클래스에 대 한 코드 숨김 클래스 페이지 `SortingWithDefaultPaging.aspx`합니다. 다음으로, 시간을 내어 보기는 `SortingWithDefaultPaging.aspx` 브라우저에서 페이지입니다. 동일한 기능 및 모양으로 나타내야 `Paging.aspx`합니다.

## <a name="enhancing-productsbll-to-include-a-default-paging-and-sorting-method"></a>페이징 및 정렬 방법을 기본값을 포함 하도록 ProductsBLL 향상

이전 자습서에서 만든를 `GetProductsAsPagedDataSource(pageIndex, pageSize)` 의 메서드를 `ProductsBLL` 반환 되는 클래스를 `PagedDataSource` 개체입니다. 이 `PagedDataSource` 개체를 사용 하 여 채워진 *모든* 제품 (BLL s를 통해 `GetProducts()` 메서드)에 바인딩된 경우 DataList에 해당 하는 지정 된 레코드만 하지만 *pageIndex* 및 *pageSize* 입력된 매개 변수 표시 되었습니다.

이 자습서의 앞부분에서 추가한 정렬 지원 ObjectDataSource s에서 정렬 식을 지정 하 여 `Selecting` 이벤트 처리기입니다. ObjectDataSource 같은 정렬할 수 있습니다 하는 개체를 반환 될 때 잘 작동 합니다 `ProductsDataTable` 반환한는 `GetProducts()` 메서드. 그러나 합니다 `PagedDataSource` 에서 반환 된 개체는 `GetProductsAsPagedDataSource` 메서드는 내부 데이터 소스 정렬을 지원 하지 않습니다. 대신, 반환 된 결과 정렬 해야 합니다 `GetProducts()` 메서드 *하기 전에* 배치 했으므로 `PagedDataSource`합니다.

이렇게 하려면 새 메서드 만들기에 `ProductsBLL` 클래스 `GetProductsSortedAsPagedDataSource(sortExpression, pageIndex, pageSize)`합니다. 정렬 하는 `ProductsDataTable` 반환한를 `GetProducts()` 메서드를 지정 합니다 `Sort` 의 기본 속성 `DataTableView`:


[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample5.cs)]

합니다 `GetProductsSortedAsPagedDataSource` 메서드는 약간만 다릅니다에서 `GetProductsAsPagedDataSource` 이전 자습서에서 만든 메서드. 특히 `GetProductsSortedAsPagedDataSource` 추가 입력된 매개 변수를 허용 `sortExpression` 이 값을 할당 하 고는 `Sort` 의 속성을 `ProductDataTable` s `DefaultView`입니다. 나중에 코드 몇 줄을 `PagedDataSource` s 데이터 원본 개체를 할당 하는 `ProductDataTable` s `DefaultView`.

## <a name="calling-the-getproductssortedaspageddatasource-method-and-specifying-the-value-for-the-sortexpression-input-parameter"></a>GetProductsSortedAsPagedDataSource 메서드를 호출 하 고 SortExpression 입력 매개 변수 값 지정

사용 하 여는 `GetProductsSortedAsPagedDataSource` 메서드 완료를 다음 단계는이 매개 변수에 대 한 값을 제공 합니다. ObjectDataSource `SortingWithDefaultPaging.aspx` 호출 하도록 현재 구성 되어 합니다 `GetProductsAsPagedDataSource` 메서드 및 2를 통해 두 개의 입력된 매개 변수 전달 `QueryStringParameters`에서 지정 된는 `SelectParameters` 컬렉션입니다. 이러한 두 `QueryStringParameters` 나타내는 원본 합니다 `GetProductsAsPagedDataSource` 메서드 s *pageIndex* 및 *pageSize* querystring 필드에서 매개 변수를 가져오는 `pageIndex` 및 `pageSize`합니다.

ObjectDataSource s 업데이트 `SelectMethod` 속성을 새 호출 `GetProductsSortedAsPagedDataSource` 메서드. 그런 다음 새를 추가 `QueryStringParameter` 있도록 합니다 *sortExpression* querystring 필드에서 액세스 하는 입력된 매개 변수 `sortExpression`합니다. 설정 된 `QueryStringParameter` s `DefaultValue` productname 합니다.

이러한 변경 이후 ObjectDataSource가 선언적 태그 같이 표시 됩니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample6.aspx)]

이 시점에서 `SortingWithDefaultPaging.aspx` 페이지는 해당 결과 사전순 정렬 제품 이름별 (그림 9 참조). 이므로 기본적으로 ProductName 값은 변수로 전달 된 `GetProductsSortedAsPagedDataSource` s 메서드에 *sortExpression* 매개 변수입니다.


[![기본적으로 결과 제품 이름별으로 정렬](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image24.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image23.png)

**그림 9**: 기본적으로 결과 기준으로 정렬 됩니다 `ProductName` ([클릭 하 여 큰 이미지 보기](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image25.png))


수동으로 추가 하는 경우는 `sortExpression` querystring 필드와 같은 `SortingWithDefaultPaging.aspx?sortExpression=CategoryName` 결과 정렬에서 지정 된 `sortExpression`합니다. 그러나이 `sortExpression` 매개 변수 데이터의 다른 페이지로 이동할 때 쿼리 문자열에 포함 되지 않습니다. 사실, 다시 우리는 단추 다음 페이지나 마지막 페이지에서 클릭 `Paging.aspx`! 또한 있는 s 현재 정렬 없음 인터페이스입니다. 사용자의 페이징된 데이터 정렬 순서를 변경할 수는 유일한 방법은 쿼리 문자열을 직접 조작 하 여 됩니다.

## <a name="creating-the-sorting-interface"></a>정렬 인터페이스를 만드는 방법

먼저 업데이트 해야 합니다 `RedirectUser` 메서드를 사용자에 게 보낼지 `SortingWithDefaultPaging.aspx` (대신 `Paging.aspx`)를 포함 합니다 `sortExpression` 쿼리 문자열에서 값. 읽기 전용 페이지 수준 이라는 추가 해야 `SortExpression` 속성입니다. 이 속성을 비슷하게를 `PageIndex` 및 `PageSize` 이전 자습서에서 만든 속성의 값을 반환 합니다 `sortExpression` 존재 하는 경우 querystring 필드 및 기본 값 (ProductName)이 고, 그렇지 합니다.

현재는 `RedirectUser` 메서드는 단일 입력된 매개 변수만 표시 하려면 페이지의 인덱스를 허용 합니다. 그러나 쿼리 문자열에 지정 된 새로운 이외의 정렬 식을 사용 하 여 데이터의 특정 페이지에 사용자를 리디렉션할 하려는 경우 경우가 있을 수 있습니다. 잠시 후에 일련의 지정된 된 열에서 데이터를 정렬 하는 것에 대 한 단추 웹 컨트롤을 포함 하는이 페이지에 대 한 정렬 인터페이스를 만들겠습니다. 이러한 단추 중 하나를 클릭할 때 적절 한 정렬 식 값을 전달 하는 사용자를 리디렉션할 하고자 합니다. 이 기능을 제공 하려면 두 가지 버전의 만들기를 `RedirectUser` 메서드. 첫 번째 두 번째 페이지 인덱스와 정렬 식을 허용 하는 동안을 표시 하려면 페이지 인덱스만 동의 해야 합니다.


[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample7.cs)]

이 자습서의 첫 번째 예제에서는 DropDownList를 사용 하 여 정렬 인터페이스를 만들었습니다. 예를 들어 let s 사용을 기준으로 정렬 하는 것에 대 한 하나 DataList 위에 배치 하는 세 개의 단추 웹 컨트롤 `ProductName`하나씩에 대 한 `CategoryName`, 및 `SupplierName`합니다. 설정으로 3 개의 단추 웹 컨트롤 추가 자신의 `ID` 및 `Text` 속성 적절 하 게 합니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample8.aspx)]

그런 다음 만들기를 `Click` 각각에 대 한 이벤트 처리기입니다. 이벤트 처리기를 호출 해야 합니다 `RedirectUser` 메서드를 적절 한 정렬 식을 사용 하 여 첫 번째 페이지로 사용자를 반환 합니다.


[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample9.cs)]

데이터 제품 이름별 사전순으로 정렬는 페이지를 처음 방문 하는 경우 (그림 9 다시 참조). 범주 단추 종류를 클릭 하 고 데이터의 두 번째 페이지로 이동 하려면 다음 단추를 클릭 합니다. 범주 이름을 기준으로 정렬 하는 데이터의 첫 번째 페이지로 우리 반환 합니다 (그림 10 참조). 마찬가지로 정렬 Supplier 단추 클릭 데이터의 첫 번째 페이지에서 시작 하는 공급 업체에서 데이터를 정렬 합니다. 데이터를 통해 페이징 되는 대로 정렬 선택을 기억 됩니다. 그림 11 범주별으로 정렬 하 고 다음 데이터의 열 세 번째 페이지로 이동한 후 페이지를 보여 줍니다.


[![제품은 범주별으로 정렬](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image27.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image26.png)

**그림 10**: The 제품 범주별으로 정렬 됩니다 ([큰 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image28.png))


[![정렬 식은 기억 하면 페이징를 통해 데이터](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image30.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image29.png)

**그림 11**:의 정렬 식은 기억 하면 페이징를 통해 데이터 ([큰 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image31.png))


## <a name="step-6-custom-paging-through-records-in-a-repeater"></a>Repeater에 레코드를 통해 사용자 지정 페이징을 6 단계:

DataList 예제 단계에서 비효율적인 기본 페이징 기술을 사용 하 여 해당 데이터를 통해 5 페이지를 검사 합니다. 충분히 많은 양의 데이터를 페이징할 때는 반드시 사용자 지정 페이징을 사용할 수 있습니다. 다시 합니다 [효율적으로 페이징을 통해 많은 양의 데이터](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md) 하 고 [사용자 지정 페이징 데이터 정렬](../paging-and-sorting/sorting-custom-paged-data-cs.md) 자습서, 기본 및 사용자 지정 페이징 및 만든된 메서드 간의 차이점에 대 한 BLL에 검사할 사용자 지정 페이징 및 정렬 사용자 지정 페이징된 데이터를 활용할 수 있습니다. 특히, 이러한 두 이전 자습서에서 추가한 다음 세 가지 방법의 `ProductsBLL` 클래스:

- `GetProductsPaged(startRowIndex, maximumRows)` 시작 하는 레코드의 특정 하위 집합 반환 *startRowIndex* 초과 하지 않는 한 *maximumRows*합니다.
- `GetProductsPagedAndSorted(sortExpression, startRowIndex, maximumRows)` 지정 된 정렬 하는 레코드의 특정 하위 집합 반환 *sortExpression* 입력된 매개 변수입니다.
- `TotalNumberOfProducts()` 레코드의 총 수를 제공 합니다 `Products` 데이터베이스 테이블입니다.

이러한 메서드를 효율적으로 페이지 및 정렬 DataList 또는 Repeater 컨트롤을 사용 하 여 데이터를 통해 사용할 수 있습니다. 이 설명 하기 s 사용자 지정 페이징 지원을 사용 하 여 반복기 컨트롤을 만들어 시작 수 그런 다음 정렬 기능 추가 하겠습니다.

열기는 `SortingWithCustomPaging.aspx` 페이지에 `PagingSortingDataListRepeater` 폴더 설정 페이지로 Repeater를 추가 하 고 해당 `ID` 속성을 `Products`입니다. 반복기가 스마트 태그를 만들고 라는 새로운 ObjectDataSource는 `ProductsDataSource`합니다. 해당 데이터를 선택 하도록 구성 합니다 `ProductsBLL` s 클래스 `GetProductsPaged` 메서드.


[![S ProductsBLL 클래스 GetProductsPaged 메서드를 사용 하는 ObjectDataSource 구성](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image33.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image32.png)

**그림 12**: ObjectDataSource를 사용 하 여 구성 합니다 `ProductsBLL` s 클래스 `GetProductsPaged` 메서드 ([클릭 하 여 큰 이미지 보기](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image34.png))


UPDATE, INSERT에서에서 드롭 다운 목록을 설정 탭 (없음)을 삭제 하 고 단추를 클릭 합니다. 데이터 소스 구성 마법사에서 이제 소스를 요구 합니다 `GetProductsPaged` s 메서드에 *startRowIndex* 및 *maximumRows* 매개 변수를 입력 합니다. 실제로 이러한 입력된 매개 변수가 무시 됩니다. 대신 합니다 *startRowIndex* 및 *maximumRows* 값을 통해 전달 됩니다는 `Arguments` ObjectDataSource에서 속성 `Selecting` 지정 방법을 마찬가지로 이벤트 처리기를 *sortExpression* 이 자습서가 첫 번째 데모입니다. 따라서 매개 변수 소스를 None에서 설정 마법사에서 드롭 다운 목록을 유지 합니다.


[![매개 변수 원본 집합을 None으로 유지](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image36.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image35.png)

**그림 13**: 매개 변수 원본 집합을 None으로 유지 ([큰 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image37.png))


> [!NOTE]
> 수행할 *되지* 집합 ObjectDataSource s `EnablePaging` 속성을 `true`입니다. 이렇게 하면 자동으로 자체를 포함 하는 ObjectDataSource *startRowIndex* 및 *maximumRows* 매개 변수는 `SelectMethod` s 기존 매개 변수 목록입니다. 합니다 `EnablePaging` 속성은 이러한 컨트롤의 ObjectDataSource의 특정 동작을 예상 하기 때문에 바인딩 사용자 지정 GridView, FormView DetailsView 컨트롤에 데이터를 페이징 하는 경우 유용 경우에만 사용 가능 `EnablePaging` 속성은 `true`합니다. DataList 및 반복기에 대 한 페이징 지원을 수동으로 추가 하 고 있기 때문에이 속성을 설정 유지 `false` (기본값), ASP.NET 페이지 내에서 직접 필요한 기능에 적용 됩니다 것 처럼 합니다.


마지막으로 s 반복기를 정의 `ItemTemplate`의 제품 이름, 범주 및 공급자 표시 되도록 합니다. 이러한 변경 이후 Repeater 및 ObjectDataSource가 선언적 구문을 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample10.aspx)]

잠시 브라우저를 통해 페이지를 방문 하 여 레코드가 반환 됩니다. 때문에 이것이에서는 ve 지정 하는 *startRowIndex* 및 *maximumRows* 매개 변수 값이 있습니다; 따라서 0의 값은 전달 되 둘 다에 대 한 합니다. 이러한 값을 지정 하려면 ObjectDataSource s에 대 한 이벤트 처리기를 만들 `Selecting` 이벤트 및 이러한 매개 변수 값을 프로그래밍 방식으로 0에서 5의 하드 코드 된 값에 각각 설정 합니다.


[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample11.cs)]

이 변경으로 브라우저를 통해 볼 때 페이지 처음 5 개 제품을 보여 줍니다.


[![첫 번째 5 개 레코드가 표시 됩니다.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image39.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image38.png)

**그림 14**:의 첫 번째 5 개 레코드가 표시 됩니다 ([큰 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image40.png))


> [!NOTE]
> 그림 14에 나열 된 제품 때문에 제품 이름별으로 정렬할 오류가 발생 하는 `GetProductsPaged` 기준으로 결과 정렬 하는 효율적인 사용자 지정 페이징 쿼리를 수행 하는 저장된 프로시저 `ProductName`합니다.


페이지를 단계별로 실행 하려면 사용자를 허용 하기 위해 추적을 시작 하는 행 인덱스 및 최대 행 수 하 고 다시 게시할 때마다 이러한 값을 저장 해야 합니다. 기본 페이징 예제에서에서는 querystring 필드 지 속하는 데 이러한 값 이 데모에서는 s 페이지의 뷰 상태에서이 정보를 유지 하도록 합니다. 다음 두 속성을 만듭니다.


[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample12.cs)]

사용 하도록 선택 하면 이벤트 처리기에서 코드를 다음으로 업데이트 합니다 `StartRowIndex` 고 `MaximumRows` 0에서 5의 하드 코드 된 값 대신 속성:


[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample13.cs)]

이 시점에서 페이지는 여전히 처음 다섯 개의 레코드만 표시 됩니다. 그러나 이러한 속성이 있는 곳에서 준비 된 페이징 인터페이스를 만드는 것입니다.

## <a name="adding-the-paging-interface"></a>페이징 인터페이스를 추가합니다.

동일한 첫 번째, 이전 다음, 마지막으로 페이징 인터페이스 let 용도로 데이터 페이지를 표시 하는 컨트롤에 표시 되는 레이블 웹을 비롯 한 기본 페이징 예제에서는 및 존재 하는 총 페이지 수에 사용 합니다. 네 단추 웹 컨트롤 및 반복기 아래에 레이블을 추가 합니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample14.aspx)]

다음으로 만듭니다 `Click` 네 개의 단추에 대 한 이벤트 처리기입니다. 이러한 단추 중 하나를 클릭할 때 업데이트 해야 합니다 `StartRowIndex` Repeater 데이터 다시 바인딩합니다. 첫 번째, 이전 및 다음 단추에 대 한 코드는 충분히 간단 하지만 마지막 단추에 대 한 확인 하려면 어떻게 해야에서는 데이터의 마지막 페이지에 대 한 시작 행 인덱스? 계산에 총에서 레코드 수를 알아야 합니다 다음 및 마지막 단추를 사용할지 여부를 확인할 수 있게 뿐만 아니라이 인덱스를 통해 페이징 되 고 됩니다. 이 호출 하 여 확인할 수 있습니다 합니다 `ProductsBLL` s 클래스 `TotalNumberOfProducts()` 메서드. Let s 이라는 읽기 전용, 페이지 수준 속성을 만들 `TotalRowCount` 의 결과 반환 하는 `TotalNumberOfProducts()` 메서드:


[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample15.cs)]

이 속성을 사용 하 여 이제 마지막 페이지의 시작 행 인덱스를 확인할 수 있습니다. 특히, s 정수 결과의 합니다 `TotalRowCount` 로 나눈 값 1을 뺀 `MaximumRows`를 곱한 값으로 `MaximumRows`입니다. 작성할 수 있습니다는 `Click` 페이징 인터페이스 단추 4 개에 대 한 이벤트 처리기:


[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample16.cs)]

마지막으로, 마지막 페이지를 볼 때 데이터 및 다음 마지막 단추의 첫 페이지를 볼 때 페이징 인터페이스의 첫 번째 및 이전 단추를 사용 하지 않도록 설정 해야 합니다. 이렇게 하려면 다음 코드를 추가 합니다 ObjectDataSource의 `Selecting` 이벤트 처리기:


[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample17.cs)]

이 추가한 후 `Click` 이벤트 처리기 및 코드를 사용 하도록 설정 하거나 현재 시작 행 인덱스를 기준으로 페이징 인터페이스 요소를 사용 하지 않도록 브라우저에서 페이지를 테스트 합니다. 그림 15에서는 먼저 첫 번째 페이지를 방문할 때 및 이전 단추는 비활성화 됩니다. 마지막을 클릭 하면 마지막 페이지를 표시 하는 동안 데이터의 두 번째 페이지를 보여 줍니다 다음을 클릭 (그림 16과 17 참조). 데이터의 마지막 페이지를 볼 때 다음와 마지막 단추가 비활성화 됩니다.


[![첫 번째 제품 페이지를 볼 때 이전 및 마지막 단추를 비활성화 됩니다.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image42.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image41.png)

**그림 15**: 첫 번째 제품 페이지를 볼 때 비활성화 됩니다 Previous 및 마지막 단추 ([큰 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image43.png))


[![제품의 두 번째 페이지는 표시](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image45.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image44.png)

**그림 16**:의 두 번째 페이지의 제품에 표시 됩니다 ([큰 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image46.png))


[![마지막 표시를 클릭 하 고 있습니다. 데이터의 마지막 페이지](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image48.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image47.png)

**그림 17**: 마지막을 클릭 하면 마지막 페이지의 데이터 표시 ([큰 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image49.png))


## <a name="step-7-including-sorting-support-with-the-custom-paged-repeater"></a>7 단계: Repeater를 페이징 지원 사용자 지정을 사용 하 여 정렬 포함

이제는 사용자 지정 페이징을 구현 되었습니다 정렬 포함할 준비가 지원 합니다. `ProductsBLL` s 클래스 `GetProductsPagedAndSorted` 메서드가 동일 *startRowIndex* 하 고 *maximumRows* 매개 변수를 입력 `GetProductsPaged`, 추가 허용 하지만  *sortExpression* 입력된 매개 변수입니다. 사용 하는 `GetProductsPagedAndSorted` 메서드에서 `SortingWithCustomPaging.aspx`, 다음 단계를 수행 해야 합니다.

1. ObjectDataSource s 변경할 `SelectMethod` 속성을 `GetProductsPaged` 에 `GetProductsPagedAndSorted`입니다.
2. 추가 된 *sortExpression* `Parameter` ObjectDataSource의 개체 `SelectParameters` 컬렉션입니다.
3. 페이지 수준 개인 만들기 `SortExpression`의 페이지 뷰 상태를 통해 다시 게시할 때마다 해당 값을 유지 하는 속성입니다.
4. ObjectDataSource s 업데이트 `Selecting` ObjectDataSource s 할당할 이벤트 처리기 *sortExpression* 매개 변수 값 페이지 수준 `SortExpression` 속성입니다.
5. 정렬 인터페이스를 만듭니다.

ObjectDataSource가 업데이트 하 여 시작 `SelectMethod` 속성과 추가 된 *sortExpression* `Parameter`합니다. 있는지 확인 합니다 *sortExpression* `Parameter` s `Type` 속성이 `String`합니다. 이러한 처음 두 개의 태스크를 완료 한 후 ObjectDataSource가 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample18.aspx)]

다음으로 페이지 수준 해야 `SortExpression` 속성 값 뷰 상태에 serialize 됩니다. 정렬 식 값에 설정한 경우 ProductName을 기본값으로 사용 합니다.


[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample19.cs)]

ObjectDataSource를 호출 하기 전에 `GetProductsPagedAndSorted` 로 설정 해야 하는 메서드를 *sortExpression* `Parameter` 의 값에는 `SortExpression` 속성. 에 `Selecting` 이벤트 처리기 코드의 다음 줄을 추가 합니다.


[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample20.cs)]

에 정렬 인터페이스를 구현 합니다. 마지막 예제에서 수행한 것 처럼 s를 구현한 결과 정렬 하는 데 사용할 수 있는 세 개의 단추 웹 컨트롤을 사용 하 여 제품 이름, 범주 또는 공급 업체 정렬 인터페이스가 있습니다.


[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample21.aspx)]

만들 `Click` 이러한 3 개의 단추 컨트롤에 대 한 이벤트 처리기입니다. 이벤트 처리기를 다시 설정 합니다 `StartRowIndex` 0으로 설정 합니다 `SortExpression` rebind 데이터 Repeater 확인 하 고 적절 한 값에:


[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample22.cs)]

S 모두 완료 되었습니다! 다양 한 사용자 지정 페이징 및 정렬을 구현 하는 단계 동안 단계 기본 페이징에 필요한 것과 매우 유사한 되었습니다. 그림 18 범주별으로 정렬 하는 경우 데이터의 마지막 페이지를 볼 때 제품을 보여 줍니다.


[![데이터의 마지막 페이지, Sorted 범주별으로 표시 됩니다.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image51.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image50.png)

**그림 18**: 마지막 페이지의 데이터, Sorted 범주별으로 표시 됩니다 ([큰 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image52.png))


> [!NOTE]
> 이전 예제에서는 공급 업체 이름 정렬 식으로 사용 된 공급 업체에서 정렬 하는 경우. 그러나 사용자 지정 페이징 구현 CompanyName을 사용 해야 합니다. 때문에 이것이 저장된 프로시저를 사용자 지정 페이징을 구현할 책임이 `GetProductsPagedAndSorted` 에 정렬 식을 전달 합니다 `ROW_NUMBER()` 키워드를는 `ROW_NUMBER()` 키워드 별칭 대신 실제 열 이름이 필요 합니다. 따라서 사용 해야 합니다 `CompanyName` (의 열 이름을 `Suppliers` 테이블)에 사용 되는 별칭 대신 합니다 `SELECT` 쿼리 (`SupplierName`) 정렬 식에 대 한 합니다.


## <a name="summary"></a>요약

모두 DataList 또는 Repeater 기본 제공 정렬 지원을 제공 하지만 약간의 코드 및 사용자 지정 정렬 인터페이스를 사용 하 여 이러한 기능을 추가할 수 있습니다. 정렬 식을 통해 지정할 수 있습니다 정렬 하지만 하지 페이징를 구현할 때 합니다 `DataSourceSelectArguments` ObjectDataSource s에 전달 된 개체 `Select` 메서드. 이렇게 `DataSourceSelectArguments` s 개체 `SortExpression` ObjectDataSource에서 속성을 할당할 수 있습니다 `Selecting` 이벤트 처리기입니다.

DataList 또는 Repeater 이미 페이징 지원을 제공 하는 정렬 기능을 추가 하려면는 가장 쉬운 방법은 정렬 식을 허용 하는 메서드를 포함 하도록 비즈니스 논리 계층을 사용자 지정할 수 있습니다. 이 정보 다음에 ObjectDataSource에서 매개 변수를 통해 전달할 수 `SelectParameters`입니다.

이 자습서는 페이징 및 정렬 DataList 및 반복기 컨트롤을 사용 하 여이 검사를 완료 합니다. 다음 및 최종 자습서는 항목별로을 일부 사용자가 시작 되는 사용자 지정 기능을 제공 하기 위해 DataList 및 반복기가 템플릿에 단추 웹 컨트롤을 추가 하는 방법을 검사 합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 David Suru 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](paging-report-data-in-a-datalist-or-repeater-control-cs.md)
> [다음](paging-report-data-in-a-datalist-or-repeater-control-vb.md)
