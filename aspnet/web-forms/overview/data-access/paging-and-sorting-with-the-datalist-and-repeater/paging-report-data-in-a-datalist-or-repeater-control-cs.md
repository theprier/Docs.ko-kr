---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-cs
title: "DataList 반복기 컨트롤 (C#)에서 보고서 데이터를 페이징 | Microsoft Docs"
author: rick-anderson
description: "DataList 아니고 반복기 제안 자동 페이징 또는 정렬을 지원 하는 동안이 자습서에서는 DataList 또는 반복기, 페이징 지원을 추가 하는 방법..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/13/2006
ms.topic: article
ms.assetid: e8e0809b-25c4-4c3b-8d12-9a17048148ae
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 4952adff752ec834b8be5f190181be98a034ccfd
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="paging-report-data-in-a-datalist-or-repeater-control-c"></a>반복기 컨트롤 (C#) 또는 DataList에서 보고서 데이터를 페이징
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_44_CS.exe) 또는 [PDF 다운로드](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/datatutorial44cs1.pdf)

> DataList 아니고 반복기 제안을 자동 페이징 또는 지원,이 자습서를 정렬할 DataList 또는 훨씬 더 유연한 페이징 및 데이터에 대 한 디스플레이 인터페이스 수 있는 반복기를 페이징 지원을 추가 하는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

페이징 및 정렬과 온라인 응용 프로그램에서 데이터를 표시할 때 두 매우 공통적인 기능이 있습니다. 예를 들어 온라인 서 점에서에서 ASP.NET 설명서를 검색할 때는 이러한 책의 수백 있을 수 있습니다 하지만 검색 결과 나열 하는 보고서 페이지 당 10 번만 일치 항목을 나열 합니다. 또한, 제목, 가격, 페이지 수, 만든이 이름으로 결과 정렬할 수 있습니다. 설명한 것 처럼는 [페이징 및 보고서 데이터 정렬](../paging-and-sorting/paging-and-sorting-report-data-cs.md) 자습서는 GridView, DetailsView, FormView 컨트롤 모두 checkbox의 눈금에 사용할 수 있는 기본 제공 페이징 지원을 제공 합니다. GridView에도 정렬 지원을 포함 됩니다.

그러나 DataList 아니고 반복기 자동 페이징 또는 정렬 기능을 제공 합니다. 이 자습서에서는 DataList 또는 반복기를 페이징 지원을 추가 하는 방법을 검토 합니다. 해야 수동으로 만든 페이징 인터페이스, 적절 한 페이지의 레코드를 표시 하 게시할 방문 페이지를 기억 합니다. 이 시간이 더 길어지고 GridView, DetailsView, 또는 FormView 보다 코드에 수행 하는 동안 DataList와 반복기 허용 훨씬 더 유연한 페이징 및 데이터에 대 한 표시 인터페이스입니다.

> [!NOTE]
> 이 자습서는 페이징에만 중점을 둡니다. 다음 자습서에는 정렬 기능 추가 살펴보겠습니다.


## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>1 단계: 추가 페이징 및 자습서 웹 페이지를 정렬 합니다.

이 자습서를 시작 하기 전에 먼저이 자습서와 다음에 대 한 사용 해야 하는 ASP.NET 페이지를 추가 하려면 잠시 s를 사용 합니다. 시작 이라는 프로젝트에 새 폴더를 만들어서 `PagingSortingDataListRepeater`합니다. 다음으로 마스터 페이지를 사용 하도록 구성 된 모두이 폴더에 다음과 같은 5 개의 ASP.NET 페이지를 추가 `Site.master`:

- `Default.aspx`
- `Paging.aspx`
- `Sorting.aspx`
- `SortingWithDefaultPaging.aspx`
- `SortingWithCustomPaging.aspx`


![PagingSortingDataListRepeater 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image1.png)

**그림 1**: 만들기는 `PagingSortingDataListRepeater` 폴더 자습서 ASP.NET 페이지를 추가 합니다.


을 열고는 `Default.aspx` 끌어서 페이지는 `SectionLevelTutorialListing.ascx` 에서 사용자 정의 컨트롤의 `UserControls` 디자인 화면으로 폴더입니다. 만든이 사용자 정의 컨트롤의 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-cs.md) 자습서에서는 사이트 맵을 열거 하 고 글머리 기호 목록에서 현재 섹션의 해당 자습서를 표시 합니다.


[![Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image3.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image2.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image4.png))


페이징 및 정렬 자습서에서는 만들게 됩니다 표시 글머리 기호 목록을 가지려면 사이트 맵을 추가 해야 합니다. 열기는 `Web.sitemap` 파일을 편집 및 삭제 한 후 DataList 사이트 맵 노드 태그와 함께 다음 태그를 추가 합니다.


[!code-xml[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample1.xml)]


![새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image5.png)

**그림 3**: 새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트


## <a name="a-review-of-paging"></a>페이징 검토

이전 자습서에서 GridView, DetailsView, FormView 컨트롤의 데이터를 페이징 하는 방법을 살펴보았습니다. 이러한 세 가지 컨트롤 페이징 호출의 간단한 형태에서는 *기본 페이징* 단순히 컨트롤 s 스마트 태그에서 페이징 사용 옵션을 확인 하 여 구현할 수 있습니다. 기본 페이징을 사용 하 여 데이터 페이지 요청 될 때마다에서 첫 번째 페이지를 방문 또는 때 사용자가 데이터 GridView DetailsView의 다른 페이지를 탐색할 또는 FormView 컨트롤 다시 요청 *모든* 의 데이터는 ObjectDataSource 합니다. 그 다음 캡처가 표시할 레코드의 특정 집합 요청한 페이지 인덱스 및 한 페이지에 표시할 레코드 수입니다. 기본 페이징에서 자세히 설명한는 [페이징 및 보고서 데이터 정렬](../paging-and-sorting/paging-and-sorting-report-data-cs.md) 자습서입니다.

기본 페이징 각 페이지에 대 한 모든 레코드를 다시 요청 이후 것 불가능 충분히 많은 양의 데이터를 페이징할 때는 합니다. 예를 들어 10의 페이지 크기 50, 000 레코드에 페이징을 한다고 가정 합니다. 사용자가 새 페이지로 이동할 때마다 그중에서 10 표시 되는 경우에 모든 50, 000 레코드 검색, 데이터베이스에서 해야 합니다.

*사용자 지정 페이징* 요청된 된 페이지에 표시할 레코드의 하위 집합에 정확한 밖으로 기본 페이징의 성능 문제를 해결 합니다. 사용자 지정 페이징을 구현할 때 효율적으로 레코드의 올바른 집합에만 반환 하는 SQL 쿼리를 작성 해야 합니다. 새 SQL Server 2005 s를 사용 하 여 이러한 쿼리를 만드는 방법에 살펴보았습니다 [ `ROW_NUMBER()` 키워드](http://www.4guysfromrolla.com/webtech/010406-1.shtml) 다시는 [효율적으로 페이징 통해 많은 양의의 데이터](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md) 자습서입니다.

DataList 또는 반복기 컨트롤에서 기본 페이징을 구현 하려면 사용할 수는 [ `PagedDataSource` 클래스](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.aspx) 주위에서 래퍼로 `ProductsDataTable` 내용이 호출이 전달 됩니다. `PagedDataSource` 클래스에는 `DataSource` 열거 가능한 개체에 할당할 수 있는 속성 및 [ `PageSize` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.pagesize.aspx) 및 [ `CurrentPageIndex` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.currentpageindex.aspx) 레코드 수를 나타내는 속성 페이지당 표시 및 현재 페이지 인덱스입니다. 이러한 속성을 설정는 `PagedDataSource` 모든 데이터 웹 컨트롤의 데이터 원본으로 사용할 수 있습니다. `PagedDataSource`열거 하는 경우 해당 내부 레코드의 적절 한 하위 집합만 반환 됩니다 `DataSource` 기반는 `PageSize` 및 `CurrentPageIndex` 속성입니다. 그림 4의 기능을 보여주고는 `PagedDataSource` 클래스입니다.


![PagedDataSource 페이징할 수 있는 인터페이스를 열거 가능한 개체를 래핑합니다.](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image6.png)

**그림 4**:는 `PagedDataSource` 페이징할 수 있는 인터페이스를 열거 가능한 개체를 래핑합니다.


`PagedDataSource` 개체 일 수 생성 및 비즈니스 논리 계층에서 직접 구성 하 고 DataList 또는 ObjectDataSource 통해 반복기에 바인딩된 또는 만들고 사용할 수 있는 ASP.NET 페이지의 코드 숨김 클래스에서 직접 구성 합니다. 후자의 방법을 사용할 경우 사용 되는 경우는 ObjectDataSource를 사용 하지 말고 하 고 대신 페이징된 데이터 DataList 또는 반복기를 프로그래밍 방식으로 바인딩할 해야 했습니다.

`PagedDataSource` 개체에는 속성을 사용자 지정 페이징을 지원 합니다. 그러나에서는를 사용 하 여 무시할 수 있습니다는 `PagedDataSource` BLL 메서드에 이미 있는 때문에 사용자 지정 페이징 하는 데는 `ProductsBLL` 표시할 정확한 레코드를 반환 하는 사용자 지정 페이징 하기 위한 클래스입니다.

이 자습서에서는 새로운 메서드를 추가 하 여 DataList의 기본 페이징을 구현 살펴보겠습니다는 `ProductsBLL` 적절 하 게 구성 된 반환 하는 클래스 `PagedDataSource` 개체입니다. 다음 자습서에서는 사용자 지정 페이징을 사용 하는 방법을 살펴보겠습니다.

## <a name="step-2-adding-a-default-paging-method-in-the-business-logic-layer"></a>2 단계: 비즈니스 논리 계층에 기본 페이징 메서드 추가

`ProductsBLL` 클래스에는 모든 제품 정보를 반환 하기 위한 메서드가 현재 `GetProducts()` 시작 인덱스에서 제품의 특정 하위 집합을 반환 하는 것에 대 한 하나 `GetProductsPaged(startRowIndex, maximumRows)`합니다. 기본 페이징을 사용 하 여 GridView, DetailsView, 및 FormView 사용을 제어 모든는 `GetProducts()` 메서드를 사용 하 여 으로만 모든 제품을 검색 한 `PagedDataSource` 레코드의 하위 집합에 올바른 표시를 내부적으로 합니다. DataList 및 반복기 컨트롤과 함께이 기능을 복제 하려면이 동작을 모방 하 BLL에 새 메서드를 만들 수 했습니다.

메서드를 추가 `ProductsBLL` 라는 클래스 `GetProductsAsPagedDataSource` 두 정수 입력된 매개 변수를 사용 하 합니다.

- `pageIndex`을 표시 하려면 페이지의 인덱스 0에 인덱싱된 및
- `pageSize`한 페이지에 표시할 레코드 수를 지정 합니다.

`GetProductsAsPagedDataSource`검색 하 여 시작 *모든* 에서 레코드 `GetProducts()`합니다. 그런 다음 만듭니다는 `PagedDataSource` 설정 개체를 해당 `CurrentPageIndex` 및 `PageSize` 속성 값의 전달 기능을 `pageIndex` 및 `pageSize` 매개 변수입니다. 메서드가이 구성이 반환 하 여 마지막 `PagedDataSource`:


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample2.cs)]

## <a name="step-3-displaying-product-information-in-a-datalist-using-default-paging"></a>3 단계: 기본 페이징을 사용 하 여 DataList의 제품 정보 표시

와 `GetProductsAsPagedDataSource` 에 추가 하는 메서드는 `ProductsBLL` 클래스를 만들 수 있습니다 이제 DataList 또는 기본 페이징 제공 하는 반복기입니다. 열어 시작는 `Paging.aspx` 페이지에 `PagingSortingDataListRepeater` 폴더 및 s DataList 설정 디자이너 도구 상자에서 끌어서 DataList `ID` 속성을 `ProductsDefaultPaging`합니다. DataList s 스마트 태그를 만들고 라는 새 ObjectDataSource `ProductsDefaultPagingDataSource` 사용 하 여 데이터를 검색할 수 있도록 구성 하 고는 `GetProductsAsPagedDataSource` 메서드.


[![ObjectDataSource 만들고 GetProductsAsPagedDataSource () 메서드를 사용 하도록 구성](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image8.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image7.png)

**그림 5**:는 ObjectDataSource를 만들고 사용 하도록 구성 된 `GetProductsAsPagedDataSource` `()` 메서드 ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image9.png))


삽입, 업데이트에서 드롭 다운 목록을 설정 하 고 각 탭 (없음)을 삭제 합니다.


[![UPDATE, INSERT에에서 드롭다운 목록이 설정 하 고 각 탭 (없음)을 삭제 합니다.](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image11.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image10.png)

**그림 6**: 삽입, 업데이트에서 드롭 다운 목록를 설정 하 고 각 탭 (없음)을 삭제 ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image12.png))


이후는 `GetProductsAsPagedDataSource` 만들라는 주세요. 이러한 매개 변수 값의 출처, 메서드는 두 개의 입력된 매개 변수가 있습니다.

페이지 인덱스 및 페이지 크기 값 게시할 저장 해야 합니다. 이러한 뷰 상태에 저장할 수, 쿼리 문자열에 유지, 세션 변수에 저장 된 또는 다른 기술을 사용 하 여 저장 합니다. 이 자습서에 대 한 쿼리 문자열에는 특정 데이터 페이지를 책갈피가 표시 될 수 있는 이점이 사용 합니다.

Querystring 필드 pageIndex와 pageSize를 사용 하 여 특히는 `pageIndex` 및 `pageSize` 매개 변수를 각각 (그림 7 참조). 잠시 이러한 매개 변수에 대 한 기본 값을 설정 하려면 t 성공한 querystring 값 사용자가이 페이지를 처음 방문할 때 제공 되어야 하는 대로. 에 대 한 `pageIndex`, 기본값 0으로 설정 (데이터의 첫 페이지에 표시 됩니다) 및 `pageSize`의 기본값 4입니다.


[![PageIndex와 pageSize 매개 변수에 대 한 원본으로 쿼리 문자열을 사용 하 여](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image14.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image13.png)

**그림 7**:에 대 한 원본으로 쿼리 문자열을 사용 하 여 `pageIndex` 및 `pageSize` 매개 변수 ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image15.png))


ObjectDataSource를 구성한 후 Visual Studio 자동으로 만듭니다는 `ItemTemplate` DataList에 대 한 합니다. 사용자 지정의 `ItemTemplate`의 제품 이름, 범주 및 공급자만 표시 되도록 합니다. DataList s 설정 `RepeatColumns` 속성을 2, 해당 `Width` 100%로 및 해당 `ItemStyle` s `Width` 를 50%입니다. 이 너비 설정은 두 개의 열에 같은 간격을 제공 합니다.

다음과 같이 변경한 후 DataList 및 ObjectDataSource의 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample3.aspx)]

> [!NOTE]
> 이후 우리는 업데이트를 수행 하지 않으며 또는이 자습서에서 삭제 기능을 렌더링 된 페이지 크기를 줄이는 DataList의 뷰 상태를 해제할 수 있습니다.


도 브라우저를 통해이 페이지를 처음 방문할 때는 `pageIndex` 나 `pageSize` querystring 매개 변수가 제공 됩니다. 따라서 0에서 4의 기본 값이 사용 됩니다. 그림 8 에서처럼 따라서 처음 네 개의 제품을 표시 하는 DataList 됩니다.


[![첫 번째 4 개 제품 나와](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image17.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image16.png)

**그림 8**:의 첫 번째 4 개 제품 나와 ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image18.png))


없이 사용자 데이터의 두 번째 페이지를 탐색할 수에 대 한 s 현재 더 간단 하 게 여기 페이징 인터페이스를 의미 합니다. 4 단계에서 페이징 인터페이스를 만들어 보겠습니다. 지금은 하지만 페이징을 하려면 직접 쿼리 문자열에서 페이징 조건을 지정 하 여 합니다. 예를 들어 두 번째 페이지를 보려면에서 s 브라우저 주소 표시줄에서 URL을 변경 `Paging.aspx` 를 `Paging.aspx?pageIndex=2` Enter 키를 누릅니다. 이 인해 데이터를 표시할 수의 두 번째 페이지 (그림 9 참조).


[![두 번째 페이지의 데이터 표시](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image20.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image19.png)

**그림 9**: 두 번째 페이지의 데이터가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image21.png))


## <a name="step-4-creating-the-paging-interface"></a>4 단계: 페이징 인터페이스 만들기

구현 될 수 있는 다른 페이징 인터페이스의 여러 가지가 있습니다. GridView, DetailsView, 및 FormView 컨트롤 중에서 선택할 수 있는 네 개의 서로 다른 인터페이스를 제공 합니다.

- **다음, 이전** 사용자 다음 또는 이전 쿼리와 한 번에 한 페이지를 이동할 수 있습니다.
- **다음, 이전, 첫 번째, 마지막** 다음 및 이전 단추 외에도이 인터페이스는 첫 번째 또는 마지막 페이지로 이동 하기 위한 첫 번째 및 마지막 단추가 포함 합니다.
- **숫자** 사용자가 신속 하 게 특정 페이지로 이동할 페이징 인터페이스의 페이지 번호를 나열 합니다.
- **숫자, 먼저 마지막** 숫자 페이지 번호 외에도 첫 번째 또는 마지막 페이지로 이동 단추가 포함 되어 있습니다.

DataList 및 반복기에 대 한 결정을 내리기 페이징 인터페이스를 구현 하는 합니다. 이 페이지에서 필요한 웹 컨트롤을 만들고 특정 페이징 인터페이스 단추를 클릭할 때 요청된 된 페이지를 표시 해야 합니다. 또한 특정 페이징 인터페이스 컨트롤 사용 하지 않도록 설정할 할 수 있습니다. 예를 들어, 다음을 사용 하 여 데이터의 첫 번째 페이지를 볼 때 이전 먼저 마지막 인터페이스를 첫 번째 및 이전 단추가 비활성화 됩니다.

이 자습서에서는 다음을 할 수 있도록된 s 사용에 대 한 이전 먼저 마지막 인터페이스입니다. 네 개의 단추 웹 컨트롤이 페이지에 추가 하 고 설정의 `ID` s를 `FirstPage`, `PrevPage`, `NextPage`, 및 `LastPage`합니다. 설정의 `Text` 속성을 &lt; &lt; 먼저 &lt; Prev, 다음 &gt;, 및 마지막 &gt; &gt; 합니다.


[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample4.aspx)]

다음으로 만듭니다는 `Click` 이러한 각 단추에 대 한 이벤트 처리기입니다. 잠시 후에 요청 된 페이지를 표시 하는 데 필요한 코드를 추가 합니다.

## <a name="remembering-the-total-number-of-records-being-paged-through"></a>통해 호출이 전달 하는 레코드의 총 수를 기억 합니다.

선택 된 페이징 인터페이스에 관계 없이 계산 하 여 통해 호출이 전달 하는 레코드의 총 수를 저장 해야 합니다. 페이징 인터페이스 컨트롤 추가 되거나 사용할 수를 결정 하는 통해 데이터의 총 페이지 수를 호출이 전달 됩니다 (페이지 크기와 함께)의 총 행 수를 결정 합니다. 다음, 이전, 첫 번째에서 마지막 인터페이스를 작성 하는 페이지 수는 두 가지 방법으로 사용 됩니다.

- 이 경우 마지막 페이지를 있는지 여부를 보고 있는 것을 확인 하려면 다음 및 마지막 단추가 비활성화 됩니다.
- 마지막으로 whisk 해야 마지막 단추를 클릭할 경우 페이지 보다 작은 인 인덱스 페이지 수입니다.

총 행 수의 최대 페이지 크기를 나눈 페이지 수 계산 됩니다. 예를 들어 페이지당 4 개의 레코드가 있는 79 레코드를 통해 페이징, 하는 경우 다음 페이지 수는 20 (79의 최대 / 4). 숫자 페이징 인터페이스를 사용 하는 경우이 정보 있다는 메시지가; 표시할 숫자 페이지 단추 수에 대 한 우리는 페이징 인터페이스 다음 또는 마지막 단추가 포함 된 페이지 수 다음 또는 마지막 단추를 사용 하지 않도록 설정 하는 시기를 결정 하 ´ ù.

페이징 인터페이스 마지막 단추를 포함 하는 경우에 게시할에 마지막 단추를 클릭할 때 마지막 페이지 색인을 확인할 수 있습니다 되도록 통해 호출이 전달 하는 레코드의 총 수를 저장 하는 매우 중요 합니다. 이 작업을 위해 만들는 `TotalRowCount` 뷰 상태에 해당 값을 유지 하 고 ASP.NET 페이지의 코드 숨김 클래스 속성에에서:


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample5.cs)]

외에 `TotalRowCount`만드는 쉽게 페이지 인덱스, 페이지 크기에 액세스 하기 위한 읽기 전용 페이지 수준 속성을 하 고 페이지 수:


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample6.cs)]

## <a name="determining-the-total-number-of-records-being-paged-through"></a>통해 호출이 전달 하는 레코드의 총 수를 결정 합니다.

`PagedDataSource` ObjectDataSource s에서 반환 된 개체 `Select()` 메서드에 그 안에 *모든* 제품 레코드의 경우에만 이들의 하위 집합에에서 표시 됩니다 DataList 합니다. `PagedDataSource` s [ `Count` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.count.aspx) DataList;에 표시 되는 항목의 수만 반환는 [ `DataSourceCount` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.datasourcecount.aspx) 내에서 항목의 총 수를 반환 합니다.는 `PagedDataSource`. 따라서 ASP.NET의 페이지를 할당 해야 `TotalRowCount` 속성 값의는 `PagedDataSource` s `DataSourceCount` 속성입니다.

ObjectDataSource s에 대 한 이벤트 처리기를 만들고이를 위해 `Selected` 이벤트입니다. 에 `Selected` ObjectDataSource s의 반환 값에 액세스할 수 있는 이벤트 처리기 `Select()` 이 경우 메서드는 `PagedDataSource`합니다.


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample7.cs)]

## <a name="displaying-the-requested-page-of-data"></a>요청 된 데이터 페이지를 표시합니다.

사용자가 페이징 인터페이스에서 단추 중 하나를 클릭 하면 데이터의 요청 된 페이지를 표시 해야 합니다. 페이징 매개 변수는 데이터 사용의 요청 된 페이지를 표시 하는 쿼리 문자열을 통해 지정 된 이후 `Response.Redirect(url)` 는 s 사용자 브라우저 다시 요청 하려면는 `Paging.aspx` 페이지 적절 한 페이징 매개 변수를 사용 합니다. 예를 들어 데이터의 두 번째 페이지를 표시 하려면 우리는 사용자를 리디렉션하 `Paging.aspx?pageIndex=1`합니다.

이 작업을 위해 만들는 `RedirectUser(sendUserToPageIndex)` 메서드 사용자를 리디렉션하는 `Paging.aspx?pageIndex=sendUserToPageIndex`합니다. 그런 다음 네 명의 단추에서이 메서드를 호출 `Click` 이벤트 처리기입니다. 에 `FirstPage` `Click` 이벤트 처리기, 호출 `RedirectUser(0)`, 첫 페이지에;에서 보낼는 `PrevPage` `Click` 이벤트 처리기를 사용 하 여 `PageIndex - 1` 페이지 인덱스로 등입니다.


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample8.cs)]

와 `Click` 완료 하는 이벤트 처리기, 단추를 클릭 하 여 DataList의 레코드를 통해 페이징 될 수 있습니다. 기능 직접 사용해 보십시오!

## <a name="disabling-paging-interface-controls"></a>인터페이스 컨트롤 페이징 사용 하지 않도록 설정

현재 표시 되는 페이지에 관계 없이 모든 네 개의 단추가 활성화 됩니다. 그러나 마지막 페이지를 표시할 때 다음 및 마지막 단추, 데이터의 첫 번째 페이지를 표시 하는 경우 첫 번째 및 이전 단추를 사용 하지 않도록 설정 하려고 합니다. `PagedDataSource` ObjectDataSource s에 의해 반환 된 개체 `Select()` 메서드 속성이 [ `IsFirstPage` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.isfirstpage.aspx) 및 [ `IsLastPage` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.islastpage.aspx) 여기서 보고 있는 결정을 조사할 수 있습니다는 데이터의 첫 번째 또는 마지막 페이지입니다.

ObjectDataSource s에 다음 추가 `Selected` 이벤트 처리기.


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample9.cs)]

이 추가 된 마지막 페이지를 볼 때 다음 및 마지막 단추가 비활성화 됩니다 하는 동안 첫 번째 페이지를 볼 때 첫 번째 및 이전 단추를 비활성화 됩니다.

Let s 페이징 인터페이스를 완료 하 여 사용자에 게 알리는 대상 페이지은 다시 현재 보고 하 고 존재 하는 총 페이지 수입니다. 페이지에 레이블 웹 컨트롤을 추가 하 고 설정의 `ID` 속성을 `CurrentPageNumber`합니다. 설정의 `Text` ObjectDataSource 선택한 이벤트 처리기에서 이러한 속성을 표시 되는 현재 페이지에 포함 되도록 (`PageIndex + 1`) 및 총 페이지 수 (`PageCount`).


[!code-csharp[Main](paging-report-data-in-a-datalist-or-repeater-control-cs/samples/sample10.cs)]

그림 10은 `Paging.aspx` 처음 방문 합니다. DataList 처음 네 개의 제품; 표시 기본값으로 querystring 비어 있으므로 첫 번째 및 이전 단추 비활성화 됩니다. (그림 11 참조)는 다음 네 개의 레코드;을 다음을 클릭 하면 표시 됩니다. 이제 첫 번째 및 이전 단추를 활성화 합니다.


[![첫 번째 페이지의 데이터 표시](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image23.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image22.png)

**그림 10**: 첫 번째 페이지의 데이터가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image24.png))


[![두 번째 페이지의 데이터 표시](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image26.png)](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image25.png)

**그림 11**: 두 번째 페이지의 데이터가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-cs/_static/image27.png))


> [!NOTE]
> 사용자가 페이지당 보려면 페이지를 지정할 수 있도록 하 여 페이징 인터페이스를 추가로 향상 될 수 있습니다. 예를 들어 5, 10, 25, 50, 및 모든 같은 목록 페이지 크기 옵션 DropDownList에 추가할 수 없습니다. 페이지 크기를 선택할 때의 사용자가 다시 리디렉션할 수 있어야 `Paging.aspx?pageIndex=0&pageSize=selectedPageSize`합니다. 판독기에 대 한 연습으로이 향상 된이 기능을 구현 하려면을 둡니다.


## <a name="using-custom-paging"></a>사용자 지정 페이징 사용

비효율적인 기본 페이징 기술을 사용 하 여 해당 데이터를 통해 DataList 페이지입니다. 충분히 많은 양의 데이터를 페이징 하는 경우 반드시 사용자 지정 페이징을 사용할 수 있습니다. 약간 다를 구현 세부 정보, 하지만 기본 페이징을 사용 하 여 동일 DataList에서 사용자 지정 페이징을 구현 개념 않습니다. 사용자 지정 페이징을 사용 하 여 사용 하 여는 `ProductBLL` s 클래스 `GetProductsPaged` 메서드 (대신 `GetProductsAsPagedDataSource`). 에 설명 된 대로 [효율적으로 페이징 통해 많은 양의의 데이터](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md) 자습서 `GetProductsPaged` 반환할 행의 시작 행 인덱스 및 최대 수를 전달 해야 합니다. 이러한 매개 변수 querystring 마찬가지로 통해 유지 관리할 수 있습니다는 `pageIndex` 및 `pageSize` 사용 하는 매개 변수에 기본 페이징 합니다.

없어 s 이후 없는 `PagedDataSource` 사용자 지정 페이징을 사용 하 여 대체 기술을 통해 그리고 호출이 전달 하는 레코드의 총 수를 결정 하 사용 해야 다시 데이터의 첫 번째 또는 마지막 페이지를 표시 했습니다. `TotalNumberOfProducts()` 에서 메서드는 `ProductsBLL` 클래스를 통해 페이징 되는 제품의 총 수를 반환 합니다. 데이터의 첫 번째 페이지를 보고 하는 경우를 확인 하려면 검사 시작 행 인덱스가 0 인 경우 첫 번째 페이지를 보고 합니다. 시작 행 인덱스 및 반환할 최대 행을 통해 호출이 전달 하는 레코드의 총 수와 같거나 보다 큰 경우 마지막 페이지를 보고 합니다.

다음 자습서에서를 더 자세히 사용자 지정 페이징을 구현 살펴보겠습니다.

## <a name="summary"></a>요약

DataList 아니고 반복기 제공 아웃오브 상자 페이징 지원을 DetailsView, GridView에 있는 및 FormView 제어, 최소한의 노력으로 이러한 기능을 추가할 수 있습니다. 내 제품의 전체 집합을 래핑하는 기본 페이징 구현 하는 가장 쉬운 방법은 `PagedDataSource` 다음 바인딩합니다는 `PagedDataSource` DataList 또는 반복기입니다. 이 자습서에서는 추가 `GetProductsAsPagedDataSource` 메서드를는 `ProductsBLL` 반환 하는 클래스는 `PagedDataSource`합니다. `ProductsBLL` 클래스 사용자 지정 페이징에 필요한 메서드를 이미 포함 되어 `GetProductsPaged` 및 `TotalNumberOfProducts`합니다.

함께 사용자 지정 페이징에 표시할 레코드의 정확한 집합 또는 레코드를 모두 검색 하는 `PagedDataSource` 기본 페이징에도 추가 해야 한다고 수동으로 페이징 인터페이스입니다. 이 자습서에 대 한 만든 다음, 이전, 먼저 마지막 네 개의 단추 웹 컨트롤 인터페이스입니다. 또한 현재 페이지 번호와 총 페이지 수를 표시 하는 레이블 컨트롤 추가 되었습니다.

다음 자습서 DataList와 반복기에 정렬 지원을 추가 하는 방법을 살펴보겠습니다. 만들 수 있는 모두 페이징 (기본 및 사용자 지정 페이징을 사용 하 여 예제)으로 정렬 DataList 하는 방법 또한 살펴보겠습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가 Liz Shulok, Ken Pespisa 및 박 광 준 Leigh 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[다음](sorting-data-in-a-datalist-or-repeater-control-cs.md)
