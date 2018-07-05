---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-cs
title: DataList 또는 Repeater 컨트롤 (C#)에서 보고서 데이터 페이징 | Microsoft Docs
author: rick-anderson
description: DataList 또는 Repeater 모두 제품 자동 페이징 또는 정렬 지원을 하는 동안이 자습서에서는 DataList 또는 Repeater를 페이징 지원을 추가 하는 방법을 보여 줍니다...
ms.author: aspnetcontent
ms.date: 11/13/2006
ms.assetid: e8e0809b-25c4-4c3b-8d12-9a17048148ae
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 90df9c096b5411201da35b7076fdd3cd9b1f86d1
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37842321"
---
<a name="paging-report-data-in-a-datalist-or-repeater-control-c"></a>DataList 또는 Repeater 컨트롤 (C#)에서 보고서 데이터 페이징
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_44_CS.exe) 또는 [PDF 다운로드](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/datatutorial44cs1.pdf)

> DataList 또는 Repeater를 모두 제공 페이징 또는 정렬 지원,이 자습서에는 자동 DataList 또는 Repeater 표시 인터페이스를 훨씬 더 유연한 페이징 및 데이터에 대 한 허용 하는 페이징 지원을 추가 하는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

페이징 및 정렬 기능이 두 가지 매우 일반적인 온라인 응용 프로그램에서 데이터를 표시 하는 경우입니다. 예를 들어, 온라인 서 점에서에서 ASP.NET 설명서를 검색할 때 등의 서적 수백 있을 수 있지만 검색 결과 나열 하는 보고서 페이지당 10 번만 일치 항목을 나열 합니다. 또한 제목, 가격, 페이지 수, 저자 이름으로 결과 정렬할 수 있습니다. 설명한 대로 합니다 [페이징 및 정렬 보고서 데이터](../paging-and-sorting/paging-and-sorting-report-data-cs.md) 자습서, 모든 확인란의 눈금에 사용할 수 있는 기본 제공 페이징 지원을 제공 하는 GridView, DetailsView 및 FormView 컨트롤입니다. GridView에는 정렬 지원을 포함 됩니다.

아쉽게도 DataList 또는 Repeater를 모두 자동 페이징 또는 정렬 지원을 제공 합니다. 이 자습서는 DataList 또는 Repeater 페이징 지원을 추가 하는 방법을 살펴봅니다. 해야 수동으로 페이징 인터페이스를 만듭니다, 그리고 레코드의 해당 페이지를 표시 하 고 다시 게시할 때마다 방문 페이지를 기억 합니다. 이 더 많은 시간과 GridView, DetailsView 또는 FormView 보다 코드에 수행 하는 동안 DataList 및 반복기를 훨씬 더 유연한 페이징 및 허용 데이터 표시 인터페이스입니다.

> [!NOTE]
> 이 자습서는 단독으로 페이징에 중점을 둡니다. 다음 자습서에서는 정렬 기능 추가 살펴보겠습니다.


## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>1 단계: 페이징 추가 및 자습서 웹 페이지를 정렬 합니다.

이 자습서를 시작 하기 전에 먼저 시간을 내어이 자습서에서 다음에 해야 ASP.NET 페이지를 추가 하는 s 수 있습니다. 이라는 프로젝트에 새 폴더를 만들어 시작 `PagingSortingDataListRepeater`합니다. 다음으로 마스터 페이지를 사용 하도록 구성 된 모든 것이 폴더에 다음 5 개의 ASP.NET 페이지를 추가 `Site.master`:

- `Default.aspx`
- `Paging.aspx`
- `Sorting.aspx`
- `SortingWithDefaultPaging.aspx`
- `SortingWithCustomPaging.aspx`


![PagingSortingDataListRepeater 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image1.png)

**그림 1**: 만들기는 `PagingSortingDataListRepeater` 폴더 및 자습서 ASP.NET 페이지 추가


을 엽니다는 `Default.aspx` 끌어서 페이지를 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `UserControls` 디자인 화면으로 폴더입니다. 만든이 사용자 정의 컨트롤을 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-cs.md) 자습서에서는 사이트 맵을 열거 하 고 글머리 기호 목록에 현재 섹션에서 이러한 자습서를 표시 합니다.


[![Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image3.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image2.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 `Default.aspx` ([클릭 하 여 큰 이미지 보기](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image4.png))


글머리 기호 목록에 표시할 페이징 및 자습서를 만들 것을 정렬 하려면 사이트 맵을 추가 해야 합니다. 열기는 `Web.sitemap` 파일과 DataList 사이트 맵 노드 태그를 사용 하 여 편집 및 삭제 한 후 다음 태그를 추가 합니다.


[!code-xml[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample1.xml)]


![사이트 맵을 업데이트 하 여 새 ASP.NET 페이지를 포함 합니다.](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image5.png)

**그림 3**: 사이트 맵을 업데이트 하 여 새 ASP.NET 페이지를 포함 합니다.


## <a name="a-review-of-paging"></a>페이징에 대 한 검토

이전 자습서에서 GridView, FormView DetailsView 컨트롤에서 데이터를 페이징 하는 방법에 살펴보았습니다. 이러한 세 가지 컨트롤에서는 간단한 형태의 호출 페이징 *기본 페이징은* s control 스마트 태그의 페이징 사용 옵션을 선택 하면 구현할 수 있습니다. 기본 페이징을 사용 하 여 데이터 페이지를 요청할 때마다 첫 번째 페이지에 방문 하면 사용자 페이지로 이동 하는 다른 데이터 GridView DetailsView 또는 FormView 컨트롤이 다시 요청 *모든* 에서 데이터를 ObjectDataSource 합니다. 그 다음 캡처 표시할 레코드의 특정 집합 요청한 페이지 인덱스 및 한 페이지에 표시할 레코드 수를 지정 합니다. 기본 페이징은에서 자세히 설명한 합니다 [페이징 및 정렬 보고서 데이터](../paging-and-sorting/paging-and-sorting-report-data-cs.md) 자습서입니다.

기본 페이징은 각 페이지에 대 한 모든 레코드를 다시 요청 하므로 하기가 어려운 충분히 많은 양의 데이터를 페이징 하는 경우입니다. 예를 들어, 페이지 크기가 10 인 50,000 개의 레코드를 통해 페이징 한다고 가정 합니다. 새 페이지로 이동할 때마다의 유일한 10 표시 되는 경우에 모든 50,000 개의 레코드 검색 데이터베이스에서 해야 합니다.

*사용자 지정 페이징을* 요청된 된 페이지에 표시할 레코드의 하위 집합에 정확 하 게를 통해 기본 페이징의 성능 문제를 해결 합니다. 사용자 지정 페이징을 구현할 때 반환 하는 레코드의 올바른 집합에만 효율적으로 SQL 쿼리를 작성 해야 했습니다. 새 SQL Server 2005 s를 사용 하 여 이러한 쿼리를 만드는 방법에 살펴보았습니다 [ `ROW_NUMBER()` 키워드](http://www.4guysfromrolla.com/webtech/010406-1.shtml) 년대 합니다 [효율적으로 페이징를 통해 많은 양의 데이터](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md) 자습서입니다.

DataList 또는 Repeater 컨트롤의 기본 페이징을 구현 하려면를 사용 하면 합니다 [ `PagedDataSource` 클래스](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.aspx) 주위에서 래퍼로 `ProductsDataTable` 내용이 페이징 하는 합니다. 합니다 `PagedDataSource` 클래스에는 `DataSource` 열거 가능한 개체에 할당할 수 있는 속성 및 [ `PageSize` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.pagesize.aspx) 하 고 [ `CurrentPageIndex` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.currentpageindex.aspx) 레코드 수를 나타내는 속성 페이지당 표시 및 현재 페이지 인덱스입니다. 이러한 속성을 설정 합니다 `PagedDataSource` 데이터 웹 컨트롤의 데이터 원본으로 사용할 수 있습니다. `PagedDataSource`열거 하는 경우 해당 내부 레코드의 적절 한 하위 집합만 반환 됩니다 `DataSource` 기반으로 합니다 `PageSize` 및 `CurrentPageIndex` 속성입니다. 그림 4의 기능을 보여 주며는 `PagedDataSource` 클래스입니다.


![PagedDataSource 페이징할 수 있는 인터페이스를 사용 하 여 열거 가능한 개체를 래핑합니다.](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image6.png)

**그림 4**:는 `PagedDataSource` 페이징할 수 있는 인터페이스를 사용 하 여 열거 가능한 개체를 래핑합니다.


`PagedDataSource` 개체 일 수 있습니다 생성 및 비즈니스 논리 계층에서 직접 구성 하 고 DataList 또는 Repeater ObjectDataSource 통해 바인딩할 또는 수 만들어지고 ASP.NET의 페이지 코드 숨김 클래스에 직접 구성 합니다. 후자의 방법을 사용 하는 경우 해야 ObjectDataSource를 사용 하 여 포기 하 고 대신 페이징된 데이터 DataList 또는 Repeater에 프로그래밍 방식으로 바인딩.

`PagedDataSource` 개체에는 속성을 사용자 지정 페이징을 지원 합니다. 그러나에서는를 사용 하 여 무시할 수는 `PagedDataSource` 사용자 지정 페이징 BLL 메서드에 이미 있기 때문에 대 한는 `ProductsBLL` 표시할 정확한 레코드를 반환 하는 사용자 지정 페이징을 위한 클래스입니다.

이 자습서에서는 새 메서드를 추가 하 여 DataList에서 기본 페이징을 구현 살펴보겠습니다 합니다 `ProductsBLL` 반환을 적절 하 게 구성 하는 클래스 `PagedDataSource` 개체입니다. 다음 자습서에서는 사용자 지정 페이징을 사용 하는 방법을 살펴보겠습니다.

## <a name="step-2-adding-a-default-paging-method-in-the-business-logic-layer"></a>2 단계: 비즈니스 논리 계층에서 기본 페이징 메서드 추가

합니다 `ProductsBLL` 클래스에는 현재 모든 제품 정보를 반환 하는 방법에 `GetProducts()` 시작 인덱스에 있는 제품의 특정 하위 집합을 반환 하는 것에 대 한 개와 `GetProductsPaged(startRowIndex, maximumRows)`합니다. 기본 페이징을 사용 하 여 GridView, DetailsView 및 FormView 사용을 제어 모든 합니다 `GetProducts()` 모든 제품을 검색 하지만 사용 하 여 메서드를 `PagedDataSource` 올바른 레코드의 하위 집합만 표시할 내부적으로 합니다. DataList 및 반복기 컨트롤을 사용 하 여이 기능을 복제,이 동작을 모방 하는 BLL에 새 메서드를 만들 수 있습니다.

메서드를 추가 합니다 `ProductsBLL` 라는 클래스 `GetProductsAsPagedDataSource` 두 정수 입력 매개 변수에서 사용:

- `pageIndex` 표시할 페이지의 인덱스 0부터 인덱싱된 및
- `pageSize` 페이지당 표시할 레코드의 수입니다.

`GetProductsAsPagedDataSource` 검색 하 여 시작 *모든* 에 있는 레코드가 `GetProducts()`합니다. 그런 다음 만듭니다는 `PagedDataSource` 설정 개체를 해당 `CurrentPageIndex` 및 `PageSize` 속성 값의 전달 기능을 `pageIndex` 및 `pageSize` 매개 변수입니다. 구성 된이 반환 하 여 메서드 완료 `PagedDataSource`:


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample2.cs)]

## <a name="step-3-displaying-product-information-in-a-datalist-using-default-paging"></a>3 단계: 기본 페이징을 사용 하 여 DataList에서 제품 정보를 표시 합니다.

사용 하 여 합니다 `GetProductsAsPagedDataSource` 에 추가 하는 메서드를 `ProductsBLL` 클래스를 만들 수 있습니다 이제 DataList 또는 Repeater 기본 페이징을 제공 하는 합니다. 열어서 시작 합니다 `Paging.aspx` 페이지를 `PagingSortingDataListRepeater` 폴더 및 s DataList 설정 디자이너 도구 상자에서 끌어서 DataList `ID` 속성을 `ProductsDefaultPaging`. DataList s 스마트 태그를 만들 라는 한 새 ObjectDataSource `ProductsDefaultPagingDataSource` 사용 하 여 데이터를 검색할 수 있도록 구성 하 고는 `GetProductsAsPagedDataSource` 메서드.


[![ObjectDataSource를 만들고 GetProductsAsPagedDataSource () 메서드를 사용 하도록 구성](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image8.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image7.png)

**그림 5**: ObjectDataSource를 만들고 사용 하도록 구성 된 `GetProductsAsPagedDataSource` `()` 메서드 ([클릭 하 여 큰 이미지 보기](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image9.png))


UPDATE, INSERT에서에서 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제 합니다.


[![UPDATE, INSERT에에서 드롭다운 목록이 설정 하 고 탭 (없음)을 삭제 합니다.](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image11.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image10.png)

**그림 6**: UPDATE, INSERT에에서 드롭다운 목록이 설정 하 고 탭 (없음)을 삭제 ([큰 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image12.png))


있으므로 `GetProductsAsPagedDataSource` 마법사 이러한 매개 변수 값의 원본에 대 한 요청, 메서드는 두 개의 입력된 매개 변수가 필요 합니다.

다시 게시할 때마다 페이지 인덱스 및 페이지 크기 값을 저장 해야 합니다. 이러한 뷰 상태에 저장할 수 있습니다, 쿼리 문자열에 유지, 세션 변수에 저장 또는 다른 기술을 사용 하 여 저장 합니다. 이 자습서에 대 한 특정 페이지 수를 책갈피에 데이터의 장점이 있는 쿼리 문자열을 사용 하겠습니다.

특히 쿼리 문자열 필드 pageIndex 및에 대 한 pageSize를 사용 합니다 `pageIndex` 및 `pageSize` 매개 변수를 각각 (그림 7 참조). 시간을 내어 이러한 매개 변수에 대 한 기본값을 설정으로 t-이득 querystring 값을 사용자가이 페이지를 처음 방문할 때 제공 되어야 합니다. 에 대 한 `pageIndex`을 기본값 0으로 설정 (데이터의 첫 페이지에 표시 됩니다) 및 `pageSize` 4가 기본값입니다.


[![PageIndex 및 pageSize 매개 변수에 대 한 원본으로 쿼리 문자열 사용](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image14.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image13.png)

**그림 7**: 쿼리 문자열에 대 한 원본으로 사용 합니다 `pageIndex` 및 `pageSize` 매개 변수 ([클릭 하 여 큰 이미지 보기](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image15.png))


ObjectDataSource를 구성한 후 자동으로 만들어지고는 `ItemTemplate` DataList에 대 한 합니다. 사용자 지정을 `ItemTemplate`의 제품 이름, 범주 및 공급자만 표시 되도록 합니다. DataList s를 설정할 수도 `RepeatColumns` 속성을 2, 해당 `Width` 100% 및 해당 `ItemStyle` s `Width` 50%로 합니다. 이러한 너비 설정을 두 개의 열에 같은 간격을 제공 합니다.

다음과 같이 변경한 후 DataList 및 ObjectDataSource의 태그 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample3.aspx)]

> [!NOTE]
> 에서는 모든 업데이트를 수행 하지 않으며,이 자습서에서 삭제 기능 이므로 렌더링 된 페이지 크기를 줄이기 위해 DataList의 뷰 상태를 비활성화할 수 있습니다.


처음에 브라우저를 통해이 페이지를 방문 하는 경우는 `pageIndex` 나 `pageSize` querystring 매개 변수가 제공 됩니다. 따라서 0에서 4의 기본값을 사용 됩니다. 그림 8에서 알 수 있듯이,이 인해 처음 네 개 제품을 표시 하는 DataList 합니다.


[![첫 번째는 네 가지 제품 나와 있습니다.](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image17.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image16.png)

**그림 8**: 첫 번째는 네 가지 제품 나열 됩니다 ([큰 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image18.png))


없이 데이터의 두 번째 페이지로 이동 하는 사용자가 현재 더 간단 하 게 여기 페이징 인터페이스를 의미 합니다. 4 단계에서 페이징 인터페이스를 만들겠습니다. 지금은 그러나 페이징을 수행할 수 있습니다 직접 querystring 페이징 조건을 지정 하 여 합니다. 예를 들어, 두 번째 페이지를 보려면에서 s 브라우저 주소 표시줄에서 URL을 변경 `Paging.aspx` 에 `Paging.aspx?pageIndex=2` Enter를 누릅니다. 이렇게 하면 표시 되는 데이터의 두 번째 페이지 (그림 9 참조).


[![두 번째 페이지의 데이터가 표시 됩니다.](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image20.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image19.png)

**그림 9**:의 두 번째 페이지의 데이터가 표시 됩니다 ([큰 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image21.png))


## <a name="step-4-creating-the-paging-interface"></a>4 단계: 페이징 인터페이스를 만드는 방법

구현 될 수 있는 다른 페이징 인터페이스의 여러 가지가 있습니다. GridView, DetailsView 및 FormView 컨트롤 중에서 선택 하는 네 가지 다른 인터페이스를 제공 합니다.

- **다음으로 이전** 사용자는 다음 또는 이전 하나를 한 번에 한 페이지를 이동할 수 있습니다.
- **다음, 이전, 첫 번째, 마지막** 다음 및 이전 단추 외에도이 인터페이스는 첫 번째 또는 마지막 페이지로 이동 하는 것에 대 한 첫 번째 및 마지막 단추를 포함 합니다.
- **숫자** 사용자가 특정 페이지에 신속 하 게 이동할 수 있도록 페이징 인터페이스의 페이지 번호를 나열 합니다.
- **숫자, 처음, 마지막** 숫자 페이지 번호를 하는 것 외에도 첫 번째 또는 마지막 페이지로 이동 하는 단추를 포함 합니다.

DataList 및 반복기의 경우는에서는 페이징 인터페이스를 결정 하 고 구현 하는 일을 담당 합니다. 페이지에서 필요한 웹 컨트롤을 만들고 특정 페이징 인터페이스 단추를 클릭할 때 요청된 된 페이지를 표시 해야 합니다. 또한 특정 페이징 인터페이스 컨트롤을 사용할 수 없게 해야 합니다. 예를 들어, 다음을 사용 하 여 데이터의 첫 페이지를 볼 때 이전, 처음, 마지막으로 인터페이스를 첫 번째 및 이전 단추를 사용할 수 없게 됩니다.

이 자습서에서는 let가 사용 하 여 다음에 대 한 이전, 먼저 마지막 인터페이스입니다. 네 개의 단추 웹 컨트롤이 페이지에 추가 하 고 설정 해당 `ID` s `FirstPage`를 `PrevPage`, `NextPage`, 및 `LastPage`합니다. 설정 된 `Text` 속성을 &lt; &lt; 먼저 &lt; Prev, 다음 &gt;, 및 마지막 &gt; &gt; 합니다.


[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample4.aspx)]

그런 다음 만들기를 `Click` 이러한 각 단추에 대 한 이벤트 처리기입니다. 잠시 후에 요청된 된 페이지를 표시 하는 데 필요한 코드를 추가 합니다.

## <a name="remembering-the-total-number-of-records-being-paged-through"></a>통해 페이징 되 고 레코드의 총 수를 기억 합니다.

선택 된 페이징 인터페이스에 관계 없이 계산 하 여를 통해 페이징 되 고 레코드의 총 수를 저장 해야 합니다. 페이징 인터페이스 컨트롤 추가 되거나 사용 하도록 설정 된 결정, 데이터의 총 페이지 수를 페이징 되는 (페이지 크기와 함께)의 총 행 수를 결정 합니다. 다음, 이전, 첫 번째, 마지막 인터페이스를 빌드하는 우리는 페이지 수는 두 가지 방법으로 사용 됩니다.

- 여부를 우리는 마지막 페이지를 보고 다음 및 마지막 단추를 사용 하지 않는 경우를 결정 합니다.
- 마지막으로 whisk 해야 마지막 단추를 클릭할 경우 페이지 보다 작은 해당 인덱스는 페이지 수입니다.

총 행 수의 최대 페이지 크기로 나눈 페이지 수를 계산 됩니다. 예를 들어 페이지당 네 개의 레코드를 사용 하 여 79 레코드를 통해 페이징, 다음 페이지 수 인지 20 (79의 한계 / 4). 숫자 페이징 인터페이스를 사용 하는 경우이 정보가 알립니다; 표시할 숫자 페이지 단추의 수에 대 한 페이징 인터페이스 다음 또는 마지막 단추를 포함 하는 경우 페이지 수를 결정할 다음 또는 마지막 단추를 사용 하지 않도록 설정 하는 경우 사용 됩니다.

페이징 인터페이스 마지막 단추를 포함 하는 경우 반드시 다시 게시할 때마다에 마지막 페이지 인덱스 마지막 단추를 클릭할 때 확인할 수 있습니다 있도록 통해 페이징 되 고 레코드의 총을 기억 합니다. 이 용이 하 게 만들려면를 `TotalRowCount` 뷰 상태에 해당 값을 유지 하는 ASP.NET 페이지가 코드 숨김 클래스의 속성:


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample5.cs)]

외에 `TotalRowCount`, 잠시 페이지 인덱스, 페이지 크기를 쉽게 액세스 하는 것에 대 한 페이지 수준 속성을 읽기 전용으로 만들 수 및 페이지 수:


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample6.cs)]

## <a name="determining-the-total-number-of-records-being-paged-through"></a>통해 페이징 되 고 레코드의 총 수를 결정 합니다.

합니다 `PagedDataSource` ObjectDataSource s에서 반환 된 개체 `Select()` 메서드가 그 *모든* 제품 레코드의 경우에 하의 하위 집합만 표시 됩니다 DataList 합니다. `PagedDataSource` s [ `Count` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.count.aspx) DataList;에 표시 되는 항목의 수만 반환 합니다 [ `DataSourceCount` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.datasourcecount.aspx) 내 항목의 총 수를 반환 합니다 `PagedDataSource`. 따라서 ASP.NET의 페이지를 할당 해야 `TotalRowCount` 속성 값의 합니다 `PagedDataSource` s `DataSourceCount` 속성입니다.

이를 위해 ObjectDataSource s에 대 한 이벤트 처리기를 만들고 `Selected` 이벤트입니다. 에 `Selected` ObjectDataSource s의 반환 값에 액세스할 수는 이벤트 처리기 `Select()` 이 경우 메서드는 `PagedDataSource`합니다.


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample7.cs)]

## <a name="displaying-the-requested-page-of-data"></a>데이터의 요청된 된 페이지를 표시합니다.

사용자가 페이징 인터페이스에서 단추 중 하나를 클릭 하면 데이터의 요청 된 페이지를 표시 해야 합니다. 쿼리 문자열을 통해 데이터 사용의 요청 된 페이지를 표시 하는 페이징 매개 변수를 지정 하므로 `Response.Redirect(url)` 사용자가의 브라우저 다시 요청을 할는 `Paging.aspx` 적절 한 페이징 매개 변수를 사용 하 여 페이지입니다. 예를 들어, 데이터의 두 번째 페이지를 표시 하려면 것은 사용자를 리디렉션할 `Paging.aspx?pageIndex=1`합니다.

이 용이 하 게 만들려면를 `RedirectUser(sendUserToPageIndex)` 메서드는 사용자를 리디렉션하는 `Paging.aspx?pageIndex=sendUserToPageIndex`합니다. 그런 다음 4 명의 단추에서이 메서드를 호출 `Click` 이벤트 처리기입니다. 에 `FirstPage` `Click` 이벤트 처리기를 호출 `RedirectUser(0)`에서 첫 번째 페이지에 보낼 합니다 `PrevPage` `Click` 이벤트 처리기를 사용 하 여 `PageIndex - 1` 페이지 인덱스로; 등입니다.


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample8.cs)]

사용 하 여는 `Click` 단추를 클릭 하면 DataList가의 레코드를 통해 페이징할 수, 이벤트 처리기를 완료 합니다. 잠시 사용해 보세요!

## <a name="disabling-paging-interface-controls"></a>페이징 인터페이스 컨트롤을 사용 하지 않도록 설정

현재 표시 되는 페이지에 관계 없이 모든 네 개의 단추가 활성화 됩니다. 그러나 마지막 페이지를 표시할 때 데이터 및 다음 및 마지막 단추를 첫 번째 페이지를 표시 하는 경우 첫 번째 및 이전 단추를 사용 하지 않도록 설정 하려고 합니다. 합니다 `PagedDataSource` ObjectDataSource s에 의해 반환 된 개체 `Select()` 메서드가 속성 [ `IsFirstPage` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.isfirstpage.aspx) 하 고 [ `IsLastPage` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.islastpage.aspx) 우리가 보고 있는 결정을 살펴볼 수 있는 데이터의 첫 번째 또는 마지막 페이지입니다.

ObjectDataSource가의 다음 추가할 `Selected` 이벤트 처리기:


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample9.cs)]

이 또한이를 사용 하 여 마지막 페이지를 볼 때 다음 마지막 단추 수 없게 하는 동안 첫 번째 페이지를 볼 때 첫 번째 및 이전 단추를 비활성화 됩니다.

Let s 페이징 인터페이스를 완료 하 여 사용자에 게 알리는 새로운 페이지는 다시 존재 하는 총 페이지 수 및 현재 보고 합니다. 페이지에 레이블 웹 컨트롤을 추가 하 고 설정 해당 `ID` 속성을 `CurrentPageNumber`입니다. 설정 해당 `Text` 표시 되는 현재 페이지를 포함 하는 ObjectDataSource 선택한 이벤트 처리기에서 이러한 속성 (`PageIndex + 1`) 및 페이지의 총 수 (`PageCount`).


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample10.cs)]

그림 10은 `Paging.aspx` 처음 방문할 때. 쿼리 문자열 이므로 빈, DataList 기본값으로 처음 네 개 제품;를 표시 합니다. 첫 번째 및 이전 단추를 사용할 수 없습니다. (그림 11 참조)에서 다음 네 개의 레코드가;을 다음을 클릭 하면 표시 됩니다. 첫 번째 및 이전 단추를 지금 활성화 됩니다.


[![데이터의 첫 번째 페이지 표시](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image23.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image22.png)

**그림 10**:의 첫 번째 페이지의 데이터가 표시 됩니다 ([큰 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image24.png))


[![두 번째 페이지의 데이터가 표시 됩니다.](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image26.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image25.png)

**그림 11**:의 두 번째 페이지의 데이터가 표시 됩니다 ([큰 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image27.png))


> [!NOTE]
> 페이징 인터페이스 페이지당 보기 페이지를 지정할 수 있도록 하 여 더욱 향상 시킬 수 있습니다. 예를 들어, DropDownList 5, 10, 25, 50, 및 모든 같은 목록 페이지 크기 옵션을 추가할 수 있었습니다. 페이지 크기를 선택 하면 사용자 해야 다시 리디렉션됩니다 `Paging.aspx?pageIndex=0&pageSize=selectedPageSize`합니다. I 유지 판독기에 대 한 연습으로이 향상 된이 기능을 구현 합니다.


## <a name="using-custom-paging"></a>사용자 지정 페이징을 사용 하 여

비효율적인 기본 페이징 기술을 사용 하 여 해당 데이터를 통해 DataList 페이지입니다. 충분히 많은 양의 데이터를 페이징할 때는 반드시 사용자 지정 페이징을 사용할 수 있습니다. 구현 세부 정보는 약간 다를 있지만 DataList에서 사용자 지정 페이징을 구현 개념 기본 페이징은와 동일 하 게 됩니다. 사용자 지정 페이징을 사용 합니다 `ProductBLL` s 클래스 `GetProductsPaged` 메서드 (대신 `GetProductsAsPagedDataSource`). 에 설명 된 대로 합니다 [효율적으로 페이징를 통해 많은 양의 데이터](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md) 자습서에서는 `GetProductsPaged` 반환할 행의 시작 행 인덱스 및 최대 수를 전달 해야 합니다. 이러한 매개 변수 querystring 마찬가지로 통해 유지 관리할 수 있습니다는 `pageIndex` 및 `pageSize` 사용 하는 매개 변수에 기본 페이징 합니다.

있는 s 이후 없습니다 `PagedDataSource` 사용자 지정 페이징을 사용 하 여 대체 기술을 사용할지 여부와 통해 페이징 되 고 레코드의 총 수를 확인 하려면 사용 해야 다시 데이터의 첫 번째 또는 마지막 페이지를 표시 했습니다. `TotalNumberOfProducts()` 의 메서드는 `ProductsBLL` 클래스를 통해 페이징 되 고 제품의 총 수를 반환 합니다. 데이터의 첫 페이지를 보는 경우를 확인 하려면 검사 시작 행 인덱스 0 인 경우 첫 번째 페이지를 보고 합니다. 시작 하는 행 인덱스 및 반환할 최대 행 수를 통해 페이징 되 고 레코드의 총 보다 크거나 경우 마지막 페이지를 보고 합니다.

다음 자습서에서 자세히 사용자 지정 페이징을 구현 살펴보겠습니다.

## <a name="summary"></a>요약

DataList 또는 Repeater를 모두 제공을 페이징 지원의 찾을 DetailsView gridview에서 및 FormView 컨트롤, 최소한의 노력으로 이러한 기능을 추가할 수 있습니다. 내 제품의 전체 집합을 래핑하는 기본 페이징을 구현 하기가 가장 쉬운을 `PagedDataSource` 바인딩하고 및는 `PagedDataSource` DataList 또는 반복기입니다. 이 자습서에서는 추가 합니다 `GetProductsAsPagedDataSource` 메서드를를 `ProductsBLL` 반환 하는 클래스는 `PagedDataSource`합니다. 합니다 `ProductsBLL` 사용자 지정 페이징에 필요한 메서드를 이미 포함 하는 클래스 `GetProductsPaged` 및 `TotalNumberOfProducts`합니다.

함께 사용자 지정 페이징에 표시할 레코드의 정확한 집합 또는 모든 레코드를 검색 하는 `PagedDataSource` 기본 페이징, 해야 수동으로 페이징 인터페이스를 추가 합니다. 이 자습서를 위해 만든 다음, 이전, 처음, 마지막으로 네 개의 단추 웹 컨트롤이 있는 인터페이스입니다. 또한 현재 페이지 번호와 총 페이지 수를 표시 하는 레이블 컨트롤 추가 되었습니다.

다음 자습서에서 정렬 지원을 DataList 및 반복기를 추가 하는 방법을 살펴보겠습니다. 또한 수 모두 페이징 및 정렬 (기본 및 사용자 지정 페이징을 사용 하 여 예제) 수는 DataList를 만드는 방법을 알아봅니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Liz Shulok, Ken Pespisa 및 박 광 준 Leigh 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](sorting-data-in-a-datalist-or-repeater-control-cs.md)
