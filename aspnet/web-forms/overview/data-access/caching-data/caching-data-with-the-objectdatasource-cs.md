---
uid: web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-cs
title: ObjectDataSource (C#)를 사용 하 여 데이터 캐싱 | Microsoft Docs
author: rick-anderson
description: 캐싱은 느린와 웹 응용 프로그램의 속도 차이 의미할 수 있습니다. 이 자습서는 ASP.NET에서 캐싱를 자세히 보기를 사용 하는 4 개 중 첫 번째는 중...
ms.author: aspnetcontent
ms.date: 05/30/2007
ms.assetid: bd87413c-8160-4520-a8a2-43b555c4183a
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: f6ca84dc11eb8ecd03aee91198e74b723cfdce7c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803047"
---
<a name="caching-data-with-the-objectdatasource-c"></a>ObjectDataSource (C#)를 사용 하 여 데이터 캐싱
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_58_CS.exe) 또는 [PDF 다운로드](caching-data-with-the-objectdatasource-cs/_static/datatutorial58cs1.pdf)

> 캐싱은 느린와 웹 응용 프로그램의 속도 차이 의미할 수 있습니다. 이 자습서는 ASP.NET에서 캐싱를 자세히 보기를 사용 하는 4 개 중 첫 번째입니다. 캐시의 주요 개념 및 ObjectDataSource 컨트롤을 통해 프레젠테이션 계층에 캐싱을 적용 하는 방법에 알아봅니다.


## <a name="introduction"></a>소개

전산학 석사 학위에서 *캐싱* 프로세스를 가져오는 데 비용이 많이 드는 정보나 데이터를 가져와 복사본을 빠르게 액세스할 수 있는 위치에 저장 됩니다. 데이터 기반 응용 프로그램에 대 한 대규모 또는 복잡 한 쿼리는 s 응용 프로그램 실행 시간의 대부분 일반적으로 사용합니다. 이러한 응용 프로그램의 성능, 그런 다음 응용 프로그램의 메모리에 비용이 많이 드는 데이터베이스 쿼리의 결과 저장 하 여 종종 향상 될 수 있습니다.

ASP.NET 2.0은 다양 한 캐싱 옵션을 제공 합니다. 전체 웹 페이지 또는 사용자 정의 컨트롤 렌더링 s 태그를 통해 캐시 될 수 있습니다 *출력 캐싱을*합니다. ObjectDataSource, SqlDataSource 컨트롤 제어 수준에 캐시할 캐싱 기능에도 수 있도록 데이터를 제공 합니다. 및 ASP.NET *데이터 캐시* 페이지 개발자가 프로그래밍 방식으로 캐시 개체 수 있는 다양 한 캐싱 API를 제공 합니다. 이 자습서에서 살펴봅니다 ObjectDataSource s를 사용 하 여 다음 세 기능 뿐만 아니라 데이터 캐시를 캐시 합니다. 시작 시 응용 프로그램 수준 데이터를 캐시 하는 방법 및 캐시 된 데이터를 SQL 캐시 종속성 사용 하 여 최신 상태로 유지 하는 방법을 대해서도 살펴보겠습니다. 이러한 자습서에서 출력 캐싱을 살펴봅니다 하지 않습니다. 출력 캐싱을 자세히 살펴보고, 대해서 [Output Caching in ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)합니다.

캐싱을 적용할 수 아키텍처에서는 어디서 든 데이터 액세스 계층에서 위로 프레젠테이션 레이어를 통해. 이 자습서는 ObjectDataSource 컨트롤을 통해 프레젠테이션 계층으로 캐시를 적용 하는 방법을 살펴보겠습니다. 살펴보겠습니다 다음 자습서에서 비즈니스 논리 계층에서 데이터를 캐시 합니다.

## <a name="key-caching-concepts"></a>캐싱 개념 키

캐싱 응용 프로그램 s 크게 높일 수 있습니다 전반적인 성능 및 확장성 데이터를 생성 하는 데 비용이 많이 드는 서 보다 효율적으로 액세스할 수 있는 위치에 복사본을 저장 합니다. 캐시는 실제 기본 데이터의 복사본이 보관 하므로 오래 될 수 있습니다 또는 *부실*기본 데이터가 변경 된 경우. 이 대처 하기 위해 페이지 개발자 캐시 항목 될 조건을 나타낼 수 있습니다 *제거* 캐시에서 사용 하 여:

- **시간 기반 조건을** 절대 또는 슬라이딩 기간에 대 한 캐시에 항목을 추가할 수 있습니다. 예를 들어 페이지 개발자는 기간을 60 초를 나타낼 수 있습니다. 절대 기간을 사용 하 여 캐시 된 항목에는 60 초 액세스 된 빈도 관계 없이 캐시에 추가 된 후 제거 됩니다. 슬라이딩 기간을 사용 하 여 캐시 된 항목에는 마지막 액세스 이후 60 초 동안 제거 됩니다.
- **조건 종속성 기반** 종속성 캐시에 추가 하는 경우 항목에 연결할 수 있습니다. S 항목 종속성 변경 될 때 캐시에서 제거 됩니다. 종속성 파일, 다른 캐시 항목 또는 둘의 조합 수 있습니다. 또한 ASP.NET 2.0에는 개발자가 캐시에 항목을 추가 하 고 기본 데이터베이스 데이터 변경 될 때 제거 되 게 사용 하도록 설정 하는 SQL 캐시 종속성을 수 있습니다. SQL 캐시 종속성을 검토해 보겠습니다 [를 사용 하 여 SQL 캐시 종속성](using-sql-cache-dependencies-cs.md) 자습서입니다.

지정 된 제거 조건에 관계 없이 캐시에서 항목 수 *청소* 시간 기반 또는 종속성 기반 조건에 도달 하기 전에 합니다. 캐시 용량에 도달 하는 경우에 새로 추가 하려면 먼저 기존 항목 제거 해야 합니다. 결과적으로 작업 하는 경우 프로그래밍 방식으로 캐시 된 데이터를 사용 하 여 해당 s 항상 가정 하는 중요 한 캐시 된 데이터가 없을 수도 있습니다. 다음 자습서에서 프로그래밍 방식으로 캐시에서 데이터를 액세스할 때 사용할 패턴을 살펴보겠습니다 *아키텍처에서 데이터 캐싱*합니다.

캐싱 응용 프로그램에서 더 많은 성능이 빼내는 경제적인 방법을 제공 합니다. 로 [Steven Smith](http://aspadvice.com/blogs/ssmith/) 그의 기사에서 위협의 [ASP.NET 캐싱: 기술 및 모범 사례](https://msdn.microsoft.com/library/aa478965.aspx):

캐싱 좋은 성능을 얻기 위해 좋은 충분 한 시간과 분석 많지 않아도 될 수 있습니다. 메모리가 저렴, 하루 또는 일주일에 프로그램 코드 또는 데이터베이스를 최적화 하는 동안 소비 하는 대신 30 초 동안 출력을 캐시 하 여 필요한 성능을 얻을 수 있는, 경우 그렇게 캐싱 솔루션 (확인은 두 번째 이전-30 데이터 가정) 이동 합니다. 결국 서투른 디자인은 아마도 캐치 업, 물론 응용 프로그램을 제대로 디자인 하려고 해야 하므로 합니다. 하지만 현재 충분 한 성능이 좋은 가져오기 해야 하는 경우 캐싱 수 매우 좋은 [방법], 리팩터링 작업을 수행 하는 시간을 설치한 경우 나중에 응용 프로그램 시간을 구입 합니다.

캐싱 이점은 성능 향상을 제공할 수, 적용 되지 않는 모든 경우에서와 같은 응용 프로그램 데이터를 실시간으로 자주 업데이트를 사용 하는 또는 오래 된 데이터도 곧-수명이 허용 되지 됩니다. 하지만 대부분의 응용 프로그램에서 캐싱 사용 해야 합니다. ASP.NET 2.0의 캐싱 자세한 배경 정보를 참조를 [성능에 대 한 캐싱](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/default.aspx) 섹션을 [ASP.NET 2.0 퀵 스타트 자습서](https://quickstarts.asp.net/QuickStartv20/aspnet/)합니다.

## <a name="step-1-creating-the-caching-web-pages"></a>1 단계: 캐싱 웹 페이지 만들기

ObjectDataSource s 캐싱 기능 탐색을 시작 하기 전에 s를 먼저 시간을 내어이 자습서에는 다음 세 할 웹 사이트 프로젝트에서 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `Caching`합니다. 다음에 있는 각 페이지에 연결할 수 있도록 해당 폴더에 다음 ASP.NET 페이지를 추가 합니다 `Site.master` 마스터 페이지:

- `Default.aspx`
- `ObjectDataSource.aspx`
- `FromTheArchitecture.aspx`
- `AtApplicationStartup.aspx`
- `SqlCacheDependencies.aspx`


![캐싱 관련 자습서에 대 한 ASP.NET 페이지 추가](caching-data-with-the-objectdatasource-cs/_static/image1.png)

**그림 1**: 캐싱 관련 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더와 같이 `Default.aspx` 에 `Caching` 폴더 섹션의 자습서를 나열 됩니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 사용자 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지의 솔루션 탐색기에서 끌어 합니다.


[![그림 2: Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가](caching-data-with-the-objectdatasource-cs/_static/image3.png)](caching-data-with-the-objectdatasource-cs/_static/image2.png)

**그림 2**: 그림 2: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 `Default.aspx` ([클릭 하 여 큰 이미지 보기](caching-data-with-the-objectdatasource-cs/_static/image4.png))


마지막으로, 이러한 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히 다음 태그를 이진 데이터로 작업 후 추가 `<siteMapNode>`:


[!code-xml[Main](caching-data-with-the-objectdatasource-cs/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 잠시 브라우저를 통해 자습서 웹 사이트를 확인 합니다. 이제는 왼쪽 메뉴에서 캐싱 자습서에 대 한 항목이 포함 됩니다.


![사이트 맵 항목이 포함 되어 있습니다 캐싱 자습서](caching-data-with-the-objectdatasource-cs/_static/image5.png)

**그림 3**: 이제 사이트 맵 캐싱 자습서에 대 한 항목을 포함


## <a name="step-2-displaying-a-list-of-products-in-a-web-page"></a>2 단계: 웹 페이지에서 제품 목록을 표시

이 자습서는 ObjectDataSource 컨트롤 기본 캐싱 기능을 사용 하는 방법을 살펴봅니다. 이러한 기능을 살펴보면 그러나 먼저 해야 페이지에서 작동 하도록 합니다. Let s ObjectDataSource에서 검색 되는 제품 정보 목록에는 GridView를 사용 하는 웹 페이지 만들기를 `ProductsBLL` 클래스입니다.

열어서 시작 합니다 `ObjectDataSource.aspx` 페이지에 `Caching` 폴더입니다. 디자이너 도구 상자에서 GridView를 끌거나, 설정 해당 `ID` 속성을 `Products`, 선택한, 스마트 태그, 라는 새 ObjectDataSource 컨트롤을 바인딩할 `ProductsDataSource`합니다. ObjectDataSource를 사용 하려면 구성 된 `ProductsBLL` 클래스입니다.


[![ProductsBLL 클래스를 사용 하는 ObjectDataSource 구성](caching-data-with-the-objectdatasource-cs/_static/image7.png)](caching-data-with-the-objectdatasource-cs/_static/image6.png)

**그림 4**: ObjectDataSource 사용 하도록 구성 된 `ProductsBLL` 클래스 ([클릭 하 여 큰 이미지 보기](caching-data-with-the-objectdatasource-cs/_static/image8.png))


이 페이지에 대 한 s를 ObjectDataSource에 캐시 된 데이터는 GridView가의 인터페이스를 통해 수정 되 면 어떻게 될까요 살펴볼 수 있도록 편집할 수는 GridView를 만들 수 있습니다. 드롭다운 목록에 기본값을 설정 하 고 선택 탭 유지 `GetProducts()`, [업데이트] 탭에서 선택한 항목을 변경 하지만 `UpdateProduct` 받아들이는 오버 로드가 `productName`, `unitPrice`, 및 `productID` 입력된 매개 변수로.


[![적절 한 UpdateProduct 오버 로드로 업데이트 탭의 드롭 다운 목록 설정](caching-data-with-the-objectdatasource-cs/_static/image10.png)](caching-data-with-the-objectdatasource-cs/_static/image9.png)

**그림 5**: 드롭다운 목록에서 업데이트 탭 s는 적절으로 `UpdateProduct` 오버 로드 ([클릭 하 여 큰 이미지 보기](caching-data-with-the-objectdatasource-cs/_static/image11.png))


마지막으로, INSERT 및 DELETE 탭 (없음)을에서 드롭 다운 목록을 설정 하 고 마침을 클릭 합니다. 데이터 소스 구성 마법사를 완료 하면 Visual Studio 설정 ObjectDataSource s `OldValuesParameterFormatString` 속성을 `original_{0}`입니다. 에 설명 된 대로 합니다 [An 개요의 삽입, 업데이트 및 데이터 삭제](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) 자습서에서는이 속성에 선언적 구문에서 제거 되거나 해당 기본값으로 다시 설정 하려면 필요 `{0}`, 업데이트 워크플로를 위해 오류 없이 진행 합니다.

또한 마법사를 완료할 때 Visual Studio에 필드를 추가 GridView 각 제품 데이터 필드에 대 한 합니다. 제거를 제외한 모든 `ProductName`, `CategoryName`, 및 `UnitPrice` BoundFields 합니다. 다음으로 업데이트 하는 `HeaderText` 각 제품, Category 및 Price를 이러한 BoundFields 속성 각각. 있으므로 합니다 `ProductName` 필드는 필수는 BoundField templatefield로 변환 하 고를 RequiredFieldValidator 추가 `EditItemTemplate`. 마찬가지로, 변환는 `UnitPrice` 를 TemplateField로 BoundField 되도록 사용자가 입력 한 값을 유효한 통화 값 0 보다 크거나 s CompareValidator를 추가 합니다. 이러한 수정 하는 것 외에도 자유롭게 오른쪽 맞춤 등의 모든 시각적인 변경을 수행 하는 `UnitPrice` 값의 서식을 지정 하거나는 `UnitPrice` 해당 읽기 전용 및 편집 인터페이스의 텍스트가 있습니다.

GridView가 스마트 태그 편집 사용 확인란을 선택 하 여 GridView를 편집할 수 있도록 합니다. 또한 사용 페이징 및 정렬 사용 확인란을 선택 합니다.

> [!NOTE]
> GridView s 편집 인터페이스 사용자 지정 하는 방법에 대 한 검토 필요 하십니까? 그렇다면 다시 참조를 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) 자습서입니다.


[![지원할 GridView 편집, 정렬 및 페이징](caching-data-with-the-objectdatasource-cs/_static/image13.png)](caching-data-with-the-objectdatasource-cs/_static/image12.png)

**그림 6**: 편집, 정렬 및 페이징 GridView 지원을 사용 하도록 설정 ([큰 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image14.png))


이러한 GridView 수정을 마치면 GridView 및 ObjectDataSource가 선언적 태그 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](caching-data-with-the-objectdatasource-cs/samples/sample2.aspx)]

그림 7에서 알 수 있듯이, 편집 가능한 GridView 이름, 범주 및 각 데이터베이스에서 제품의 가격을 나열 합니다. 잠시 s 페이지 기능 정렬, 페이징 결과 테스트 하 고 레코드를 편집 합니다.


[![각 제품의의 이름이, Category 및 Price 정렬 가능, Pageable 편집 가능한 GridView에 나열 됩니다.](caching-data-with-the-objectdatasource-cs/_static/image16.png)](caching-data-with-the-objectdatasource-cs/_static/image15.png)

**그림 7**: 각 제품의 이름이, Category 및 Price 정렬 가능, Pageable 편집 가능한 GridView에 나열 됩니다 ([큰 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image17.png))


## <a name="step-3-examining-when-the-objectdatasource-is-requesting-data"></a>3 단계: 때 the ObjectDataSource 검사 데이터가 요청

`Products` GridView를 호출 하 여 표시할 데이터를 검색할 합니다 `Select` 메서드는 `ProductsDataSource` ObjectDataSource 합니다. 이 ObjectDataSource의 비즈니스 논리 레이어의 인스턴스를 만듭니다 `ProductsBLL` 클래스 및 호출 해당 `GetProducts()` 메서드를 호출 하는 데이터 액세스 계층 s `ProductsTableAdapter` s `GetProducts()` 메서드. DAL 메서드는 Northwind 데이터베이스에 연결 하 고 구성 된 발급 `SELECT` 쿼리 합니다. 이 데이터 DAL에서 등록 패키지는 다음을 `NorthwindDataTable`입니다. DataTable 개체를 GridView에 반환 하는 ObjectDataSource가 반환 하는 BLL에 반환 됩니다. GridView 만듭니다는 `GridViewRow` 각각에 대 한 개체 `DataRow` datatable을 이동 하 고 각 `GridViewRow` 결과적으로 클라이언트에 반환 되어 방문자가의 브라우저에 표시 되는 HTML로 렌더링 됩니다.

이 이벤트 순서는 GridView가 해당 기본 데이터에 바인딩할 해야 하는 각 시간에 발생 합니다. GridView를 정렬 하는 경우 또는 해당 기본 제공을 편집 하거나 삭제 인터페이스를 통해 GridView가의 데이터를 수정 하는 경우 다른 데이터 한 페이지에서 이동 하는 경우 페이지를 처음 방문할 때 발생 합니다. GridView가의 뷰 상태를 사용 하지 않으면 GridView도 모든 포스트백에 다시 바인딩할 수 됩니다. GridView도 명시적으로 다시 바인딩할 수 데이터를 호출 하 여 해당 `DataBind()` 메서드.

완벽 하 게 파악할 있는 데이터를 데이터베이스에서 검색 하는 빈도, 데이터를 다시 검색 될 때 메시지가 표시 되는 s 수 있습니다. 명명 된 GridView 위에 레이블을 웹 컨트롤을 추가 `ODSEvents`합니다. 지웁니다 해당 `Text` 속성 집합과 해당 `EnableViewState` 속성을 `false`입니다. 레이블 아래에 있는 단추 웹 컨트롤을 추가 하 고 설정 해당 `Text` 속성을 다시 게시 합니다.


[![GridView 위에 있는 페이지에 레이블 및 단추 추가](caching-data-with-the-objectdatasource-cs/_static/image19.png)](caching-data-with-the-objectdatasource-cs/_static/image18.png)

**그림 8**: GridView는 위의 페이지에 레이블 및 단추를 추가 ([큰 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image20.png))


데이터 액세스 워크플로 ObjectDataSource가 중 `Selecting` 기본 개체가 만들어지기 전에 이벤트가 발생 하 고 해당 구성된 메서드를 호출 합니다. 이 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.


[!code-csharp[Main](caching-data-with-the-objectdatasource-cs/samples/sample3.cs)]

ObjectDataSource 데이터에 대 한 아키텍처에 요청 될 때마다 레이블을 발생 하는 텍스트 선택 하면 이벤트를 표시 합니다.

브라우저에서이 페이지를 방문 합니다. 페이지가 처음 방문할 때 발생 하는 이벤트에 텍스트 선택이 표시 됩니다. 다시 게시 단추를 클릭 하 고 텍스트가 사라집니다 있는지 확인 (가정 GridView s `EnableViewState` 속성이 `true`, 기본값). 포스트백에서 GridView를 해당 뷰 상태를 재구성 및 해당 데이터에 대 한 ObjectDataSource 만들어지고 t 전환 하 고 따라서 때문입니다. 하지만 정렬, 페이징 또는 데이터를 편집 해당 데이터 원본에 바인딩할 GridView 시키고 따라서 선택 하면 이벤트가 텍스트 다시 나타납니다.


[![해당 데이터 원본에 GridView는 차츰 회복 되면서 때마다 선택 하면 이벤트 발생 표시 됩니다.](caching-data-with-the-objectdatasource-cs/_static/image22.png)](caching-data-with-the-objectdatasource-cs/_static/image21.png)

**그림 9**: 해당 데이터 원본에 다시 바인딩되 때마다 GridView, 발생 한 이벤트를 선택 하면 표시 됩니다 ([큰 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image23.png))


[![클릭 하면 포스트백 단추를 클릭 하면 GridView 보기 상태에서 다시 구성](caching-data-with-the-objectdatasource-cs/_static/image25.png)](caching-data-with-the-objectdatasource-cs/_static/image24.png)

**그림 10**: 다시 게시 단추를 클릭 하면 GridView 보기 상태에서 다시 구성 ([큰 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image26.png))


데이터를 통해 페이징 하거나 정렬 될 때마다 데이터베이스 데이터를 검색할 필요가 없습니다 보일 수 있습니다. 결국 기본 페이징을 사용 하 여 다시 우리 이후로 ObjectDataSource가 검색 레코드를 모두 첫 번째 페이지를 표시 하는 경우. GridView에는 정렬 및 페이징 지원을 제공 하지 않습니다, 경우에 데이터를 검색 해야 데이터베이스에서 페이지가 모든 사용자 (및 상태 보기를 사용 하지 않도록 설정 하는 경우 모든 포스트백에서)에 처음 방문할 때마다 합니다. 하지만 이러한 추가 데이터베이스 요청은 불필요 한 GridView는 모든 사용자에 게 동일한 데이터를 표시 하는 경우. 반환 된 결과 캐시 하지 않는 이유는 `GetProducts()` 메서드 및 bind를 GridView가 캐시 된 결과?

## <a name="step-4-caching-the-data-using-the-objectdatasource"></a>4 단계: 데이터를 캐싱하는 ObjectDataSource를 사용 하 여

단순히 몇 가지 속성을 설정 하 여 ObjectDataSource ASP.NET 데이터 캐시에서 검색된 데이터를 자동으로 캐시를 구성할 수 있습니다. ObjectDataSource의 캐시와 관련 된 속성을 다음과 같습니다.

- [EnableCaching](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.enablecaching.aspx) 으로 설정 되어 있어야 `true` 캐싱을 사용 하도록 설정 합니다. 기본값은 `false`입니다.
- [CacheDuration](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheduration.aspx) 시간 (초) 데이터가 캐시 되는 양입니다. 기본값은 0입니다. ObjectDataSource가 경우에 데이터를 캐시 `EnableCaching` 됩니다 `true` 고 `CacheDuration` 0 보다 큰 값으로 설정 됩니다.
- [CacheExpirationPolicy](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheexpirationpolicy.aspx) 로 설정할 수 있습니다 `Absolute` 또는 `Sliding`합니다. 하는 경우 `Absolute`, ObjectDataSource에 대 한 검색된 데이터를 캐시 `CacheDuration` 초; 경우 `Sliding`에 대 한 액세스 하지 않은 후에 데이터가 만료 되 `CacheDuration` 시간 (초)입니다. 기본값은 `Absolute`입니다.
- [CacheKeyDependency](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cachekeydependency.aspx) 이 속성을 사용 하 여 기존 캐시 종속성을 사용 하 여 ObjectDataSource가의 캐시 항목을 연결 합니다. ObjectDataSource의 데이터 항목을 제거할 수 있습니다 중간 캐시에서 만료 관련 시켜 `CacheKeyDependency`합니다. SQL 캐시 종속성을 ObjectDataSource가의 캐시를 사용 하 여 연결 하려면이 속성은 가장 많이 사용, 항목을 살펴보겠습니다 향후 [를 사용 하 여 SQL 캐시 종속성](using-sql-cache-dependencies-cs.md) 자습서입니다.

구성 s는 `ProductsDataSource` ObjectDataSource 절대 확장에서 30 초 동안 해당 데이터를 캐시 합니다. 집합 ObjectDataSource s `EnableCaching` 속성을 `true` 고 `CacheDuration` 30 속성입니다. 유지 된 `CacheExpirationPolicy` 속성이 해당 기본값으로 설정 `Absolute`합니다.


[![30 초 동안 해당 데이터를 캐시 하는 ObjectDataSource 구성](caching-data-with-the-objectdatasource-cs/_static/image28.png)](caching-data-with-the-objectdatasource-cs/_static/image27.png)

**그림 11**: 30 초 동안 해당 데이터를 캐시 하는 ObjectDataSource 구성 ([큰 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image29.png))


변경 내용을 저장 하 고 브라우저에서이 페이지를 다시 확인 합니다. 해제 되는 처음에 데이터를 캐시에서 발생 하는 이벤트 텍스트 선택 페이지를 처음 방문 하면 표시 됩니다. 않지만 후속 포스트백 정렬 하 고 다시 게시 단추를 클릭 하 여 트리거할 페이징 또는 편집 취소 단추를 클릭 하는 *되지* 텍스트 발생 합니다. 다시 선택 하면 이벤트를 표시 합니다. 왜냐하면 합니다 `Selecting` ObjectDataSource 해당 기본 개체에서 해당 데이터를 가져오는 경우에 이벤트가 발생 합니다 `Selecting` 데이터 데이터 캐시에서 끌어온 구성 인 경우 이벤트가 발생 하지 않습니다.

30 초 후 데이터를 캐시에서 제거 됩니다. 하는 경우 데이터 캐시에서 제거 될 수도 ObjectDataSource s `Insert`, `Update`, 또는 `Delete` 메서드가 호출 됩니다. 따라서 30 초가 경과 또는 업데이트 단추를 클릭 정렬, 페이징, 편집 또는 취소 단추를 클릭 하면 해당 기본 개체에서 해당 데이터를 가져오기 위해 ObjectDataSource를 선택 하면 이벤트를 표시 합니다. 발생 텍스트 경우는 `Selecting` 이벤트가 발생 합니다. 반환 된 결과 데이터 캐시에 다시 배치 됩니다.

> [!NOTE]
> 선택 하면 발생 하는 이벤트 텍스트를 자주 표시 되 면 캐시 된 데이터를 사용 하 여 작동 하는 ObjectDataSource를 예상 하는 경우에 것 메모리 제약 조건으로 인해. 사용 가능한 메모리가 없는 경우 ObjectDataSource 하 여 캐시에 추가 된 데이터 청소 되었습니다 수 있습니다. ObjectDataSource 만들어지고 t만 캐시를 데이터를 올바르게 캐시 수를 표시 하는 경우 데이터는 산발적으로 일부 응용 프로그램의 사용 가능한 메모리 닫고 다시 시도 하십시오.


그림 12에서는 워크플로 캐싱 ObjectDataSource가 보여 줍니다. 선택 하면 이벤트가 발생할 때 화면에 표시 되는 텍스트, 하므로 데이터 캐시에 없었으며 내부 개체에서 검색 해야 합니다. 이 텍스트는 사용할 수 없는 경우에 있지만 해당 s 캐시에서 데이터를 사용할 수 있으므로 합니다. 캐시에서 데이터가 반환 되는 경우 여기서 s는 내부 개체에 대 한 호출이 및 따라서 데이터베이스 쿼리가 실행 됩니다.


![ObjectDataSource 저장소 및 데이터 캐시에서 해당 데이터를 검색 합니다](caching-data-with-the-objectdatasource-cs/_static/image30.png)

**그림 12**: ObjectDataSource를 저장 하 고 데이터 캐시에서 해당 데이터를 검색 합니다.


각 ASP.NET 응용 프로그램에는 s의 모든 페이지와 방문자 공유 인스턴스는 자체 데이터 캐시가 있습니다. 즉, ObjectDataSource에서 데이터 캐시에 저장 된 데이터 페이지를 방문 하는 모든 사용자에 대해 마찬가지로 공유 되도록 합니다. 이 확인 하려면 엽니다는 `ObjectDataSource.aspx` 브라우저에서 페이지입니다. 먼저 페이지를 방문 하 고, (가정 이전 테스트 하 여 캐시에 추가 된 데이터를 지금 제거 되었습니다.) 선택 하면 발생 하는 이벤트 텍스트가 표시 됩니다. 복사본을 두 번째 브라우저 인스턴스를 열고 두 번째 첫 번째 브라우저 인스턴스의 URL을 붙여 넣습니다. 두 번째 브라우저 인스턴스에서 발생 하는 이벤트 텍스트 선택 표시 되지 것 s 동일한를 사용 하 여 첫 번째 데이터를 캐시 합니다.

ObjectDataSource를 포함 하는 캐시 키 값을 사용 하 여 해당 검색된 데이터를 캐시에 삽입 하는 경우: 합니다 `CacheDuration` 고 `CacheExpirationPolicy` 속성 값, 지정 된 ObjectDataSource를 사용 하 고 기본 비즈니스 개체의 형식 통해는 [ `TypeName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.typename.aspx) (`ProductsBLL`,이 예제의);의 값을 `SelectMethod` 속성 이름 및 매개 변수 값을 `SelectParameters` 컬렉션 및 해당 값`StartRowIndex`하 고 `MaximumRows` 속성을 구현 하는 경우 사용 되는 [사용자 지정 페이징 합니다.](../paging-and-sorting/paging-and-sorting-report-data-cs.md)

이러한 값이 변경 될 고유 캐시 엔트리를 통해 이러한 속성의 조합으로 캐시 키 값을 작성 합니다. 이전 자습서에서 예를 들어에서는 ve를 사용 하 여 살펴보았습니다 합니다 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)`, 지정된 된 범주에 대 한 모든 제품을 반환 하는 합니다. 한 명의 사용자가 페이지와 보기 음료를 가져올 수 있습니다는 `CategoryID` 1입니다. ObjectDataSource에 관계 없이 결과 캐시 하는 경우는 `SelectParameters` 값, 다른 사용자 페이지에 제공 하는 경우 캐시에 있던 음료 제품 하는 동안 입력 하면 조미료 보려는 d 보는 입력 하면 조미료 대신 캐시 된 음료 제품입니다. 값을 포함 하는 캐시 키를 다양 한 이러한 속성을 여는 `SelectParameters`, ObjectDataSource beverages 및 입력 하면 조미료에 대 한 별도 캐시 항목을 유지 관리 합니다.

## <a name="stale-data-concerns"></a>오래 된 데이터 문제

ObjectDataSource 되 면 캐시 중 하나에서 해당 항목을 자동으로 제거 해당 `Insert`, `Update`, 또는 `Delete` 메서드가 호출 됩니다. 이 페이지를 통해 데이터가 수정 될 때 캐시 항목을 지우는 오래 된 데이터에 대해 보호할 수 있습니다. 그러나 캐싱을 사용 하 여 오래 된 데이터를 여전히 표시할 ObjectDataSource에 대 한 가능한 것입니다. 가장 간단한 경우에는 데이터의 데이터베이스 내에서 직접 변경으로 인해 수 있습니다. 아마도 데이터베이스 관리자만 데이터베이스에 있는 레코드의 일부를 수정 하는 스크립트를 실행 합니다.

이 시나리오 보다 미묘 하 게에서 펼치려면 수도 없습니다. ObjectDataSource의 데이터 수정 메서드 중 하나를 호출 하면 캐시에서 해당 항목을 제거, 속성 값의 ObjectDataSource가 특정 조합에 대해 캐시 된 항목이 제거는 (`CacheDuration`하십시오 `TypeName`, `SelectMethod`, 등에)입니다. 다른 사용 하는 두 가지 경우, ObjectDataSources 있다면 `SelectMethods` 또는 `SelectParameters`, 아니지만 여전히 업데이트할 수 동일한 데이터를 하나의 ObjectDataSource 행을 업데이트 하 고 두 번째 ObjectDataSource에 대 한 고유한 캐시 항목, 하지만 해당 행을 무효화 될 수 있습니다 제공 될 여전히 캐시에서. 이 기능을 노출 하는 페이지를 만드는 하시기 바랍니다. 캐싱을 사용 하 여 데이터를 가져올 구성 하는 ObjectDataSource에서 해당 데이터를 풀링 하는 편집 가능한 GridView를 표시 하는 페이지를 만들려면 합니다 `ProductsBLL` s 클래스 `GetProducts()` 메서드. 다른 추가 사용 하 여 GridView 및이 페이지 (또는 다른) 하지만이 두 번째 ObjectDataSource ObjectDataSource를 편집할 수 있습니다는 `GetProductsByCategoryID(categoryID)` 메서드. 두 가지 경우, ObjectDataSources 이후 `SelectMethod` 속성 다는 ll 각 고유한 캐시 된 값이 있는 합니다. (페이징, 정렬 및 등)에서 다른 눈금으로 데이터를 바인딩 다음에, 그리드, 제품을 편집 하는 경우 여전히 오래 되 고 캐시 된 데이터를 제공 하 고 다른 그리드에서 수행한 변경을 반영 하지 합니다.

즉,만 사용 하 여 시간 기반 expiries 부실 데이터 가능성 있고 여기서 데이터의 새로 고침은 중요 한 시나리오에 대 한 짧은 expiries를 사용 하려는 경우. 부실 데이터를 수용할 수 없으면 캐싱 말고 또는 SQL 캐시 종속성 사용 (데이터베이스 데이터 가정 캐싱 다시 있습니다). 이후 자습서에서 SQL 캐시 종속성을 살펴보겠습니다.

## <a name="summary"></a>요약

이 자습서에서는 ObjectDataSource가 기본 제공 캐싱 기능을 검사 했습니다. 단순히 몇 가지 속성을 설정 하 여 지정 된 위치에서 반환 된 결과 캐시 하는 ObjectDataSource에 지시할 수에서는 `SelectMethod` ASP.NET 데이터 캐시에 있습니다. 합니다 `CacheDuration` 고 `CacheExpirationPolicy` 속성 항목은 캐시 기간과 절대 또는 상대 만료 인지를 나타냅니다. `CacheKeyDependency` 속성 ObjectDataSource가의 캐시 항목의 모든 기존 캐시 종속성을 사용 하 여 연결 합니다. 이 항목을 제거 하는 ObjectDataSource가의 캐시에서 시간 기반 만료에 도달 하 고 SQL 캐시 종속성을 사용 하 여 일반적으로 수입니다.

ObjectDataSource는 단순히 데이터 캐시에 해당 값을 캐시 하므로 ObjectDataSource가 기본 제공 기능을 프로그래밍 방식으로 복제할 수 것입니다. 해당 대상이 t ObjectDataSource 기본적으로이 기능을 제공 하지만 아키텍처의 별도 계층에 캐싱 기능을 구현할 수 것 이므로 프레젠테이션 계층에서이 수행 하는 것이 확인 합니다. 이렇게 하려면 ObjectDataSource에서 사용 되는 동일한 논리를 반복 해야 합니다. 다음 자습서에서 아키텍처 내에서 데이터 캐시를 사용 하 여 프로그래밍 방식으로 작동 하는 방법을 살펴봅니다.

즐거운 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 캐싱: 기술 및 모범 사례](https://msdn.microsoft.com/library/aa478965.aspx)
- [.NET Framework 응용 프로그램에 대 한 캐싱 아키텍처 가이드](https://msdn.microsoft.com/library/ee817645.aspx)
- [ASP.NET 2.0의에서 출력 캐싱](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Teresa Murphy 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](caching-data-in-the-architecture-cs.md)
