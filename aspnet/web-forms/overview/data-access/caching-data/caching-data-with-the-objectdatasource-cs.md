---
uid: web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-cs
title: "ObjectDataSource (C#)를 사용 하 여 데이터를 캐시 | Microsoft Docs"
author: rick-anderson
description: "캐싱 저속 및 고속 웹 응용 프로그램 간의 차이 의미할 수 있습니다. 이 자습서에는 ASP.NET의 캐싱 기능에 대해 자세히를 사용 하는 4의 첫 번째는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/30/2007
ms.topic: article
ms.assetid: bd87413c-8160-4520-a8a2-43b555c4183a
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ce0bd1d3302ee68c9c65584686172a07143e4a4
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="caching-data-with-the-objectdatasource-c"></a>ObjectDataSource (C#)를 사용 하 여 데이터 캐싱
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_58_CS.exe) 또는 [PDF 다운로드](caching-data-with-the-objectdatasource-cs/_static/datatutorial58cs1.pdf)

> 캐싱 저속 및 고속 웹 응용 프로그램 간의 차이 의미할 수 있습니다. 이 자습서에는 ASP.NET의 캐싱 기능에 대해 자세히를 사용 하는 4 개 중 첫 번째 숫자입니다. Caching의 주요 개념 및 캐싱 ObjectDataSource 컨트롤을 통해 프레젠테이션 계층에 적용 하는 방법에 알아봅니다.


## <a name="introduction"></a>소개

컴퓨터 분야에서 *캐싱* 데이터 나 정보를 가져오는 데 비용이 많이 차지 하 고 신속 하 게 액세스할 수 있는 위치에는 해당 복사본을 저장 하는 프로세스입니다. 데이터 기반 응용 프로그램 크고 복잡 한 쿼리는 일반적으로 응용 프로그램의 실행 시간의 대부분을 사용합니다. 이러한 프로그램 응용 프로그램의 성능, 그런 다음 응용 프로그램의 메모리에 비용이 많이 드는 데이터베이스 쿼리 결과 저장 하 여 자주 향상 될 수 있습니다.

ASP.NET 2.0은 다양 한 캐싱 옵션을 제공 합니다. 전체 웹 페이지 또는 사용자 정의 컨트롤 렌더링 s 태그를 통해 캐시 될 수 *출력 캐싱을*합니다. ObjectDataSource 및 SqlDataSource 컨트롤 제어 수준에 캐시 될 수 있도록 데이터에도 캐싱 기능을 제공 합니다. 및 ASP.NET s *데이터 캐시* 페이지 개발자가 프로그래밍 방식으로 캐시 개체 수 있는 다양 한 캐싱 API를 제공 합니다. 이 자습서에는 다음 세 ObjectDataSource s를 사용 하 여 검토 합니다 기능 뿐만 아니라 데이터 캐시를 캐시 합니다. 또한 살펴보겠습니다 시작할 때 응용 프로그램 수준 데이터를 캐시 하는 방법 및 캐시 된 데이터를 SQL 캐시 종속성을 사용 하 여 최신 상태로 유지 하는 방법. 이 자습서를 출력 캐싱을 탐색 하지 않습니다. 출력 캐싱을 자세히 살펴보고, 참조 [ASP.NET 2.0에서 출력 캐시](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)합니다.

캐싱을 통해 적용할 수 있습니다 아키텍처의 모든 위치에서 데이터 액세스 계층에서 위로 프레젠테이션 계층입니다. 이 자습서에서는 캐싱 ObjectDataSource 컨트롤을 통해 프레젠테이션 계층에 적용 하는 방법을 살펴보겠습니다. 살펴봅니다 다음 자습서의 비즈니스 논리 계층에서 데이터를 캐시 합니다.

## <a name="key-caching-concepts"></a>키 캐싱 개념

캐싱 크게 향상 시킬 수는 응용 프로그램 s 전반적인 성능 및 확장성 데이터를 생성 하는 데 비용이 서 보다 효율적으로 액세스할 수 있는 위치에는 해당 복사본을 저장 합니다. 캐시가 보유 하는 실제 기본 데이터의 복사본이 고 이후 만료 될 수 있습니다 또는 *부실*기본 데이터가 변경 되 면, 합니다. 페이지 개발자 캐시 항목 됩니다 조건을 등을 나타낼 수 있습니다 *제거* 캐시에서 사용 하 여:

- **시간 기반 조건을** 절대 또는 슬라이딩 기간에 대 한 캐시에 항목을 추가할 수 있습니다. 예를 들어 페이지 개발자 지속 시간이, 예를 들어, 60 초를 나타낼 수 있습니다. 절대 기간이 캐시 된 항목이 60 초를 얼마나 자주 액세스 하는 것에 관계 없이 캐시에 추가 된 후 제거 됩니다. 슬라이딩 기간이 캐시 된 항목에는 마지막 액세스 이후 60 초 동안 제거 됩니다.
- **종속성 기반 조건을** 종속성 캐시에 추가 하는 경우 항목에 연결할 수 있습니다. 항목의 종속성이 변경 될 때 캐시에서 제거 됩니다. 종속성은 파일, 다른 캐시 항목 또는 둘의 조합 수 있습니다. ASP.NET 2.0에는 개발자가 캐시에 항목을 추가 하 고 기본 데이터베이스 데이터 변경 될 때 제거 되 게 수 있도록 하는 SQL 캐시 종속성을 수 있습니다. SQL 캐시 종속성에는 살펴보겠습니다 [를 사용 하 여 SQL 캐시 종속성](using-sql-cache-dependencies-cs.md) 자습서입니다.

지정 된 제거 조건에 관계 없이 캐시의 항목 수 *청소* 시간 기반 또는 종속성 기반 조건이 충족 되었지만 전에 합니다. 캐시가 용량에 도달 하면 새로 추가 하려면 먼저 기존 항목 제거 해야 합니다. 따라서 작업 하는 경우 프로그래밍 방식으로 캐시 된 데이터와 해당 s 항상 가정 하는 중요 한 캐시 된 데이터 표시 되지 않을 수 있습니다. 데이터에 액세스할 때 캐시에서 프로그래밍 방식으로 다음 자습서에서를 사용 하는 패턴에서 살펴보게 *아키텍처에서 데이터 캐싱*합니다.

캐싱은 응용 프로그램에서 성능이 더 빼내에 대 한 경제적이 고 하는 방법을 제공 합니다. 으로 [서 Smith](http://aspadvice.com/blogs/ssmith/) 가 작성 한 문서에서 articulates [ASP.NET 캐싱: 기법 및 모범 사례](https://msdn.microsoft.com/en-us/library/aa478965.aspx):

캐싱 좋은 충분 한 성능을 얻으려면 많은 시간과 분석 필요 없이 좋은 방법이 될 수 있습니다. 메모리는 부담이, 30 초는 하루 또는 한 코드 또는 데이터베이스를 최적화 하는 동안 주 소비 하는 대신 출력을 캐시 하 여 필요한 성능을 얻을 수 있는, 경우 마찬가지로 캐싱 솔루션 (확인는 30-1 초 동안 오래 된 데이터를 것으로 가정)를 이동 합니다. 결국 잘못 된 설계는 아마도 따라잡을 사용자에 게 과정의 응용 프로그램을 올바르게 디자인할 하려고 해야 하므로 합니다. 하지만 경우 성능을 하기 위해 좋은 충분 한 오늘 하기만 하면, 캐싱 방법이 될 수 있는 뛰어난 [], 리팩터링 작업을 수행 하는 시간을 보유 하는 경우 나중에 응용 프로그램 시간을 구입 합니다.

캐싱 수 있는 특별 성능 향상을 제공할 수 하는 동안 적용 되지 않는 모든 상황에서와 같은 데이터를 실시간으로 자주 업데이트를 사용 하는 또는 오래 된 데이터도 곧 지속 허용 되지 않는 응용 프로그램과 함께 합니다. 하지만 대부분의 응용 프로그램, 캐싱 사용 해야 합니다. ASP.NET 2.0의 캐싱에 대 자세한 배경을 알고 싶으면에 대 한 참조는 [성능에 대 한 캐싱을](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/default.aspx) 의 섹션은 [ASP.NET 2.0 빠른 시작 자습서](https://quickstarts.asp.net/QuickStartv20/aspnet/)합니다.

## <a name="step-1-creating-the-caching-web-pages"></a>1 단계: 캐싱 웹 페이지 만들기

ObjectDataSource s 캐싱 기능 탐색을 시작 하기 전에 s를 먼저 잠시이 자습서와 다음 3에 대 한 사용 해야 하는 웹 사이트 프로젝트에 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `Caching`합니다. 다음에 해당 폴더에 있는 각 페이지에 연결할 수 있도록 다음 ASP.NET 페이지 추가 `Site.master` 마스터 페이지:

- `Default.aspx`
- `ObjectDataSource.aspx`
- `FromTheArchitecture.aspx`
- `AtApplicationStartup.aspx`
- `SqlCacheDependencies.aspx`


![캐싱 관련 자습서에 대 한 ASP.NET 페이지 추가](caching-data-with-the-objectdatasource-cs/_static/image1.png)

**그림 1**: 캐싱 관련 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더에서와 같이 `Default.aspx` 에 `Caching` 폴더는 해당 섹션의 자습서를 나열 합니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 이 기능을 제공 하는 사용자 정의 컨트롤입니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지 하려면 솔루션 탐색기에서 끌어서 합니다.


[![그림 2: Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](caching-data-with-the-objectdatasource-cs/_static/image3.png)](caching-data-with-the-objectdatasource-cs/_static/image2.png)

**그림 2**: 그림 2: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image4.png))


마지막으로, 이러한 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히 다음 태그를 이진 데이터로 작업 후 추가 `<siteMapNode>`:


[!code-xml[Main](caching-data-with-the-objectdatasource-cs/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 브라우저를 통해 자습서 웹 사이트를 보려면 보십시오. 이제는 왼쪽 메뉴에서 캐싱 자습서에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 캐싱 자습서에 대 한 항목을 포함](caching-data-with-the-objectdatasource-cs/_static/image5.png)

**그림 3**: 이제 사이트 맵 캐싱 자습서에 대 한 항목을 포함


## <a name="step-2-displaying-a-list-of-products-in-a-web-page"></a>2 단계: 웹 페이지에서 제품의 목록을 표시

이 자습서 ObjectDataSource 컨트롤 s 기본 제공 캐싱 기능을 사용 하는 방법을 살펴봅니다. 이러한 기능을 볼 수 있지만, 먼저 해야 페이지에서 작업 합니다. Let s는 GridView 목록에서 ObjectDataSource에서 검색 한 제품 정보를 사용 하는 웹 페이지를 만들고는 `ProductsBLL` 클래스입니다.

열어 시작는 `ObjectDataSource.aspx` 페이지에 `Caching` 폴더입니다. 디자이너 도구 상자에서는 GridView 끌고, 설정 해당 `ID` 속성을 `Products`, 하 고 스마트 태그를 라는 새 ObjectDataSource 컨트롤에 바인딩할 선택 `ProductsDataSource`합니다. 구성에 맞게 ObjectDataSource는 `ProductsBLL` 클래스입니다.


[![ObjectDataSource ProductsBLL 클래스를 사용 하도록 구성](caching-data-with-the-objectdatasource-cs/_static/image7.png)](caching-data-with-the-objectdatasource-cs/_static/image6.png)

**그림 4**: 구성에 사용 하 여 ObjectDataSource는 `ProductsBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image8.png))


이 페이지에 대 한 s는 ObjectDataSource에 캐시 된 데이터가 GridView의 인터페이스를 통해 수정 될 때 수행 되는 작업을 검사할 수 있도록 편집 가능한 GridView를 만들 수 있도록 합니다. 드롭 다운 목록 선택 탭, 기본 설정으로 둡니다 `GetProducts()`, [업데이트] 탭에서 선택된 항목을 변경 하지만 `UpdateProduct` 를 받아들이는 오버 로드 `productName`, `unitPrice`, 및 `productID` 입력된 매개 변수로 합니다.


[![적절 한 UpdateProduct 오버 헤드로 업데이트 탭의 드롭 다운 목록을 설정합니다](caching-data-with-the-objectdatasource-cs/_static/image10.png)](caching-data-with-the-objectdatasource-cs/_static/image9.png)

**그림 5**: 드롭다운 목록에서 업데이트 탭 s는 적절 한 설정 `UpdateProduct` 오버 로드 ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image11.png))


마지막으로 삽입 및 삭제 탭 (없음)을에서 드롭 다운 목록을 설정 하 고 마침을 클릭 합니다. 데이터 소스 구성 마법사를 완료 될 때 Visual Studio 설정 ObjectDataSource s `OldValuesParameterFormatString` 속성을 `original_{0}`합니다. 에 설명 된 대로 [는 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) 자습서에서는이 속성은 선언적 구문에서 제거 되거나 해당 기본값으로 다시 설정 `{0}`, 우리의 업데이트 워크플로를 위해 오류 없이 진행 합니다.

또한 마법사 완료 시 Visual Studio 추가 필드 GridView에 각 제품 데이터 필드에 대 한 합니다. 제거 제외한 모두 `ProductName`, `CategoryName`, 및 `UnitPrice` BoundFields 합니다. 다음을 업데이트 하는 `HeaderText` 각 제품, 범주 및 가격을 이러한 BoundFields 각각. 이후는 `ProductName` 필드는 필수는 BoundField를 TemplateField로 변환한에 RequiredFieldValidator 추가 `EditItemTemplate`합니다. 마찬가지로, 변환 된 `UnitPrice` BoundField를 TemplateField로 되도록 사용자가 입력 한 값 올바른 통화 값을 0 보다 크거나 s CompareValidator 추가 합니다. 이러한 수정 외에도 계속 오른쪽 맞춤 하는 등의 미적인 변경 수행 하기 전에 `UnitPrice` 값 또는 대 한 서식을 지정 하는 `UnitPrice` 해당 읽기 전용 및 편집 인터페이스의 텍스트가 있습니다.

GridView s 스마트 태그 편집 사용 확인란을 선택 하 여 GridView를 편집할 수 있도록 합니다. 또한 페이징 사용 및 정렬 사용 확인란을 선택 합니다.

> [!NOTE]
> GridView s 편집 인터페이스를 사용자 지정 하는 방법에 대 한 검토 필요 하십니까? 이 경우 다시 참조는 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) 자습서입니다.


[![편집, 정렬 및 페이징을 대 한 GridView 지원을 사용 하도록 설정](caching-data-with-the-objectdatasource-cs/_static/image13.png)](caching-data-with-the-objectdatasource-cs/_static/image12.png)

**그림 6**: 편집, 정렬 및 페이징을 GridView 지원을 사용 하도록 설정 ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image14.png))


이러한 GridView 수정에 확인 한 후 GridView 및 ObjectDataSource s 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](caching-data-with-the-objectdatasource-cs/samples/sample2.aspx)]

그림 7에서 볼 수 있듯이 편집 가능한 GridView 이름, 범주 및 각 데이터베이스에 제품의 가격을 나열 합니다. 백업 세트를 통해 페이지 결과 페이지의 기능 정렬을 테스트 하려면 잠시 하 고 레코드를 편집 합니다.


[![각 제품의 이름, 범주 및 가격 Sortable, Pageable, 편집 가능한 GridView에 나열 됩니다.](caching-data-with-the-objectdatasource-cs/_static/image16.png)](caching-data-with-the-objectdatasource-cs/_static/image15.png)

**그림 7**: s 각 제품 이름, 범주 및 가격 Sortable, Pageable, 편집 가능한 GridView에 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image17.png))


## <a name="step-3-examining-when-the-objectdatasource-is-requesting-data"></a>3 단계: 때 the ObjectDataSource 검사가 데이터 요청

`Products` GridView를 호출 하 여 표시할 데이터를 검색할는 `Select` 의 메서드는 `ProductsDataSource` ObjectDataSource 합니다. 이 ObjectDataSource 비즈니스 논리 계층 s의 인스턴스를 만들고 `ProductsBLL` 클래스 및 호출 해당 `GetProducts()` 메서드를 호출 하 여 데이터 액세스 계층 s `ProductsTableAdapter` s `GetProducts()` 메서드. DAL 메서드 Northwind 데이터베이스에 연결 하 고 구성 된 발급 `SELECT` 쿼리 합니다. 이 데이터는 DAL에서를 패키지에 반환 됩니다는 `NorthwindDataTable`합니다. ObjectDataSource를 GridView에 반환 하 게 반환 하는 BLL에 DataTable 개체가 반환 됩니다. GridView 만듭니다는 `GridViewRow` 각각에 대 한 개체 `DataRow` DataTable 및 각 `GridViewRow` 결국 클라이언트에 반환 되며 방문자의 브라우저에 표시 된 HTML로 렌더링 됩니다.

이 이벤트 시퀀스를 GridView에 원본 데이터를 바인딩할 필요한 각 시간에 발생 합니다. 하 여 GridView를 정렬할 때 또는 해당 기본 제공을 편집 하거나 삭제 인터페이스를 통해 GridView의 데이터를 수정 하는 경우 다른 데이터 한 페이지에서 이동할 때 페이지를 처음 방문할 때 수행 됩니다. GridView의 뷰 상태를 사용 하지 않는 경우 GridView에도 각 포스트백 다시 바인딩할 수 됩니다. GridView도 명시적으로 다시 바인딩할 수의 데이터를 호출 하 여 해당 `DataBind()` 메서드.

데이터베이스에서 데이터가 검색 되는 빈도 완전히 이해 하려면 다시 검색 되는 데이터는 때를 나타내는 메시지를 표시 하는 s 사용 수 있습니다. 명명 된 GridView 위에 Label 웹 컨트롤을 추가 `ODSEvents`합니다. 삭제는 `Text` 속성 집합과 해당 `EnableViewState` 속성을 `false`합니다. 레이블 Button 웹 컨트롤을 추가 하 고 설정 해당 `Text` 속성을 다시 게시 합니다.


[![GridView 위에 있는 페이지에 레이블 및 단추 추가](caching-data-with-the-objectdatasource-cs/_static/image19.png)](caching-data-with-the-objectdatasource-cs/_static/image18.png)

**그림 8**: GridView 위에 페이지에 레이블 및 단추를 추가 ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image20.png))


데이터 액세스 워크플로 ObjectDataSource s 중 `Selecting` 내부 개체를 만들기 전에 이벤트 발생 및 해당 구성 된 메서드를 호출 합니다. 이 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.


[!code-csharp[Main](caching-data-with-the-objectdatasource-cs/samples/sample3.cs)]

데이터에 대 한 아키텍처에 요청 하는 ObjectDataSource 때마다 레이블이 텍스트 Selecting 이벤트 발생 표시 됩니다.

브라우저에서이 페이지를 방문 합니다. 해당 페이지를 방문 먼저 발생 합니다. 텍스트 Selecting 이벤트는 표시 됩니다. 다시 게시 단추를 클릭 하 고 텍스트가 사라집니다 있는지 확인 (있다고 가정할 경우 GridView s `EnableViewState` 속성이 `true`, 기본값). 다시 게시 될 GridView를 뷰 상태에서 다시 만들려면를 대상이 t에 해당 데이터에 대 한 ObjectDataSource 때문입니다. 하지만 정렬, 페이징, 또는 데이터를 편집 해당 데이터 원본에 다시 바인딩하려면 GridView 시키고 유효성 검사 따라서 Selecting 이벤트 발생 텍스트 다시 나타납니다.


[![Selecting 이벤트 발생이 표시 됩니다 때마다 데이터 원본에 GridView는 다시 바인딩](caching-data-with-the-objectdatasource-cs/_static/image22.png)](caching-data-with-the-objectdatasource-cs/_static/image21.png)

**그림 9**: 때마다 GridView가 데이터 원본에 리바운드, Selecting 이벤트 발생이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image23.png))


[![GridView에서 뷰 상태에서 다시 구성할 수를 다시 게시 단추를 클릭 하면 클릭](caching-data-with-the-objectdatasource-cs/_static/image25.png)](caching-data-with-the-objectdatasource-cs/_static/image24.png)

**그림 10**: 포스트백 단추를 클릭 하면 해당 뷰 상태에서 다시 구성할 수에 GridView ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image26.png))


데이터를 검색 하는 데이터베이스 데이터를 통해 페이징 하거나 정렬 될 때마다 불필요 해 보일 수 있습니다. 즉, 기본 페이징을 사용 하 여 다시 we, 이후에 ObjectDataSource를 읽어들일 수의 모든 레코드 첫 번째 페이지를 표시할 때. GridView 정렬 및 페이징 지원을 제공 하지 않는 경우에 데이터 검색 해야 데이터베이스에서 될 때마다 모든 사용자 (및 포스트백이 발생할 때마다, 뷰 상태를 비활성화 하는 경우)에 먼저 해당 페이지를 방문 합니다. 하지만 이러한 추가 데이터베이스 요청은 불필요 한 GridView 모든 사용자에 게 동일한 데이터를 표시 됩니다. 반환 된 결과 캐시 하지 않는 이유는 `GetProducts()` 메서드 및 bind를 GridView가 캐시 된 결과?

## <a name="step-4-caching-the-data-using-the-objectdatasource"></a>ObjectDataSource에서 사용 하 여 데이터를 캐시 하는 4 단계:

몇 가지 속성을 설정 하면, ObjectDataSource는 자동으로 ASP.NET 데이터 캐시에서 검색 된 데이터를 캐시 하도록 구성할 수 있습니다. ObjectDataSource의 캐시 관련 속성을 다음과 같습니다.

- [EnableCaching](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.objectdatasource.enablecaching.aspx) 으로 설정 되어 있어야 `true` 캐싱을 사용 하도록 설정 합니다. 기본값은 `false`입니다.
- [CacheDuration](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.objectdatasource.cacheduration.aspx) 시간 (초) 데이터가 캐시입니다. 기본값은 0입니다. ObjectDataSource는 경우에 데이터를 캐시 `EnableCaching` 은 `true` 및 `CacheDuration` 0 보다 큰 값으로 설정 됩니다.
- [CacheExpirationPolicy](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.objectdatasource.cacheexpirationpolicy.aspx) 로 설정할 수 있습니다 `Absolute` 또는 `Sliding`합니다. 경우 `Absolute`, ObjectDataSource에서 검색 된 데이터에 대 한 캐시 `CacheDuration` 초; 경우 `Sliding`에 대 한 액세스 하지 않은 후에 데이터가 만료 되 `CacheDuration` 초입니다. 기본값은 `Absolute`입니다.
- [CacheKeyDependency](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.objectdatasource.cachekeydependency.aspx) 는 기존 캐시 종속성 ObjectDataSource의 캐시 항목을 연결 하려면이 속성을 사용 합니다. ObjectDataSource의 데이터 항목 중간를 제거할 수 있습니다 캐시에서 만료 관련 시켜 `CacheKeyDependency`합니다. 이 속성은 SQL 캐시 종속성 ObjectDataSource의 캐시와 연결할 가장 일반적으로 사용, 항목을 살펴볼 것 이후에 [를 사용 하 여 SQL 캐시 종속성](using-sql-cache-dependencies-cs.md) 자습서입니다.

구성 s는 `ProductsDataSource` ObjectDataSource 절대 단위로에서 30 초 동안 데이터를 캐시할 수 있습니다. ObjectDataSource s 설정 `EnableCaching` 속성을 `true` 및 해당 `CacheDuration` 30 속성입니다. 둡니다는 `CacheExpirationPolicy` 속성이 해당 기본값으로 설정 `Absolute`합니다.


[![구성 데이터를 캐시 하는 30 초 동안 ObjectDataSource](caching-data-with-the-objectdatasource-cs/_static/image28.png)](caching-data-with-the-objectdatasource-cs/_static/image27.png)

**그림 11**: 구성 데이터를 캐시 하는 30 초 동안 ObjectDataSource ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-cs/_static/image29.png))


변경 내용을 저장 하 고 브라우저에서이 페이지를 다시 확인 합니다. 먼저 해당 페이지를 방문 하면 처음 데이터 아니므로 캐시에서 발생 한 이벤트 텍스트 선택 표시 됩니다. 하지만 후속 포스트백을 정렬 하 고 다시 게시 단추를 클릭 하 여 트리거할 페이징, 편집 또는 취소 단추를 클릭 하거나 않습니다 *하지* Selecting 이벤트를 다시 표시할 텍스트를 실행 합니다. ¿¡´는 `Selecting` 는 ObjectDataSource 개체는 기본 개체; 로부터 데이터를 가져오는 경우에 이벤트가 발생 된 `Selecting` 데이터 캐시에서 데이터를 끌어온 경우 이벤트가 발생 하지 않습니다.

30 초 후 데이터를 캐시에서 제거 됩니다. 하는 경우 데이터 캐시에서 제거 될 수도 ObjectDataSource s `Insert`, `Update`, 또는 `Delete` 메서드 호출 됩니다. 업데이트 단추를 클릭 했음을, 정렬, 페이징, 아니면 개체는 기본 개체 로부터 해당 데이터를 가져오기 위해 ObjectDataSource 편집 또는 취소 단추를 클릭 하면 30 초 경과한 후 텍스트를 발생 Selecting 이벤트를 표시 합니다. 따라서 때는 `Selecting` 이벤트 발생 합니다. 반환 된 결과 데이터 캐시에 다시 배치 됩니다.

> [!NOTE]
> Selecting 이벤트를 발생 합니다. 텍스트를 자주 표시 되 면 캐시 된 데이터에 작동 하 ObjectDataSource를 예상 하는 경우에 원인일 수 있습니다 메모리 제약 조건입니다. 메모리가 부족 없는 경우는 objectdatasource 캐시에 추가 된 데이터 청소 되었습니다 수 있습니다. ObjectDataSource 대상이 t 데이터 또는 유일한 캐시 캐싱하기 올바르게 표시 되 면 데이터는 산발적으로 일부 응용 프로그램의 사용 가능한 메모리가 닫고 다시 시도 하십시오.


그림 12 워크플로 캐싱 ObjectDataSource s를 보여 줍니다. 선택 하면 이벤트가 발생할 때 화면에 표시 되는 텍스트, 데이터 캐시에 없습니다. 내부 개체에서 검색 해야 할 때문에 더 합니다. 그러나이 텍스트는 사용할 수 없는 경우 것 s 데이터를 캐시에서 사용할 수 있습니다. 캐시에서 데이터가 반환 될 때 여기서 s는 기본 개체에 대 한 호출이 및 따라서 데이터베이스 쿼리가 실행 됩니다.


![ObjectDataSource 저장소 및 데이터 캐시에서 데이터 검색](caching-data-with-the-objectdatasource-cs/_static/image30.png)

**그림 12**:는 ObjectDataSource를 저장 하 고 데이터 캐시에서 해당 데이터를 검색 합니다.


각 ASP.NET 응용 프로그램에서 모든 페이지와 방문자 공유 s 인스턴스는 자체 데이터 캐시를 있습니다. 즉,는 objectdatasource 데이터 캐시에 저장 된 데이터 페이지를 방문 하는 모든 사용자가 공유 마찬가지로 됩니다. 이 확인 하려면 열고는 `ObjectDataSource.aspx` 브라우저에서 페이지입니다. 처음 방문 하 여 페이지 (있다고 가정 하면 이전 테스트 하 여 캐시에 추가 된 데이터를 지금까지 제거 된) 선택 하면 발생 한 이벤트 텍스트가 표시 됩니다. 두 번째 브라우저 인스턴스 및 복사 열고 두 번째 인스턴스에 대 한 첫 번째 브라우저 인스턴스 URL을 붙여 넣습니다. 두 번째 브라우저 인스턴스에서 발생 한 이벤트 텍스트 선택 표시 되지 않는 것 같은 사용 하 여 s 첫 데이터를 캐시 합니다.

ObjectDataSource는 포함 된 캐시 키 값을 사용 하 여 해당 검색된 데이터를 캐시에 삽입할 경우:는 `CacheDuration` 및 `CacheExpirationPolicy` 속성 값, 지정 된 ObjectDataSource에서 사용 하 고 기본 비즈니스 개체의 유형 통해는 [ `TypeName` 속성](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.objectdatasource.typename.aspx) (`ProductsBLL`,이 예에서);의 값은 `SelectMethod` 속성 이름 및 값 매개 변수는 `SelectParameters` 컬렉션의 및 값이 해당 `StartRowIndex`및 `MaximumRows` 구현할 때 사용 되는 속성 [사용자 지정 페이징 합니다.](../paging-and-sorting/paging-and-sorting-report-data-cs.md)

이러한 속성의 조합으로 캐시 키 값을 만들어 이러한 값이 변경으로 고유 캐시 엔트리를 보장 합니다. 예를 들어 지난 자습서에서에서 우리 했습니다를 사용 하 여에 검토는 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)`, 지정된 된 범주에 대 한 모든 제품을 반환 하는 합니다. 한 명의 사용자가 페이지 및 보기 음료를 수행할 수는 `CategoryID` 1입니다. ObjectDataSource에 관계 없이 결과 캐시 하는 경우는 `SelectParameters` 값, 다른 사용자 페이지에 제공 하는 경우 캐시에 있던 음료 제품 하는 동안 입력 하면 조미료 보려는 d 표시 조미료 보다는 캐시 된 음료 제품입니다. 이러한 속성에 의해 캐시 키를 변경 하 여의 값을 포함 하는 `SelectParameters`, ObjectDataSource는 beverages 및 조미료에 대 한 별도 캐시 항목을 유지 관리 합니다.

## <a name="stale-data-concerns"></a>오래 된 데이터 문제

ObjectDataSource 캐시 때 중 하나에서 해당 항목을 자동으로 제거 해당 `Insert`, `Update`, 또는 `Delete` 메서드 호출 됩니다. 이 페이지를 통해 데이터가 수정 될 때 캐시 항목 선택을 취소 하 여 오래 된 데이터에 대해 보호할 수 있습니다. 그러나 캐싱을 사용 하 여 여전히 유효 하지 않은 데이터를 표시 하는 objectdatasource 같습니다. 가장 간단한 경우 데이터는 데이터베이스 내에서 직접 변경으로 인해 수 있습니다. 아마도 데이터베이스 관리자는 데이터베이스의 레코드 중 일부를 수정 하는 스크립트 실행.

이 시나리오 보다 미묘 하 게에서 펼치려면 수도 없습니다. 데이터 수정 메서드 중 하나를 호출할 때 캐시에서 해당 항목을 제거 하는 고 ObjectDataSource, 속성 값의 ObjectDataSource s 특정 조합에 대해 캐시 된 항목이 제거는 (`CacheDuration`, `TypeName`, `SelectMethod`, 등에)입니다. 다른을 사용 하는 두 개의 ObjectDataSources 있으면 `SelectMethods` 또는 `SelectParameters`, 여전히 동일한 데이터를 업데이트할 수, 하나의 ObjectDataSource 행을 업데이트 하 고 두 번째 ObjectDataSource에 대 한 고유 캐시 항목을 하지만 해당 행을 무효화 될 수 있습니다 하지만 여전히 제공 될 캐시 된에서. 확인해 페이지에서는이 기능을 만들 수 있습니다. 에서는 캐시를 사용 하는 데이터를 가져올 구성 된 ObjectDataSource에서 해당 데이터를 가져오는 편집 가능한 GridView를 표시 하는 페이지 만들기는 `ProductsBLL` s 클래스 `GetProducts()` 메서드. 다른 항목 추가 편집 가능한 GridView 및 ObjectDataSource이이 페이지 (또는 다른) 이지만이 두 번째 ObjectDataSource에 게 사용 하 여는 `GetProductsByCategoryID(categoryID)` 메서드. 두 개의 ObjectDataSources 이후 `SelectMethod` 속성 다은 각 ll는 캐시 된 값입니다. 한 모눈의 제품 (페이징, 정렬, 등)에서 다른 모눈에 다시 데이터를 바인딩 다음에 편집할 경우 여전히 오래 되 고 캐시 된 데이터를 제공 하 고 다른 그리드에서 변경한 내용을 반영 하지 합니다.

즉, 경우에 사용 시간 기반 expiries 감수할지 부실 데이터 가능성이 있는 및 사용 하 여 더 짧은 expiries 시나리오에 대 한 데이터의 새로 고침이 중요 합니다. 유효 하지 않은 데이터를 수용할 수 없으면 캐시를 취소 하거나 SQL 캐시 종속성을 사용 하 여 (데이터베이스 데이터 간주 된 캐싱). 이후 자습서에서 SQL 캐시 종속성을 살펴보겠습니다.

## <a name="summary"></a>요약

이 자습서에서는 기본 제공 캐싱 기능의 ObjectDataSource 검사 했습니다. 몇 가지 속성을 설정 하면, ObjectDataSource 지정 된 위치에서 반환 된 결과 캐시 하도록 지시할 수 우리 `SelectMethod` ASP.NET 데이터 캐시에 있습니다. `CacheDuration` 및 `CacheExpirationPolicy` 속성 항목이 캐시 되는 기간과 절대 또는 상대 만료 인지를 나타냅니다. `CacheKeyDependency` 속성 ObjectDataSource의 캐시 항목을 모두는 기존 캐시 종속성과 연결 합니다. 시간 기반 만료에 도달 하 고 SQL 캐시 종속성 일반적으로 사용 하기 전에 캐시에서 ObjectDataSource의 항목을 제거 데 될 수 있습니다.

ObjectDataSource를 단순히 해당 값 데이터 캐시에 캐시를 하므로 프로그래밍 방식으로 ObjectDataSource s 기본 제공 기능을 복제할 수 있습니다. 해당 대상이 t는 ObjectDataSource 기본적으로이 기능을 제공 하므로 아키텍처의 별도 계층에 캐싱 기능을 구현할 프레젠테이션 계층에서는 이렇게 하는 데 맞지 않습니다. 이렇게 하려면는 ObjectDataSource에서 사용 하는 동일한 논리를 반복 해야 합니다. 프로그래밍 방식으로 다음이 자습서에서 아키텍처 내에서 데이터 캐시를 사용 하는 방법을 살펴보겠습니다.

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 캐싱: 기법 및 모범 사례](https://msdn.microsoft.com/en-us/library/aa478965.aspx)
- [.NET Framework 응용 프로그램에 대 한 캐싱 아키텍처 가이드](https://msdn.microsoft.com/en-us/library/ee817645.aspx)
- [ASP.NET 2.0의에서 출력 캐싱](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Teresa 머피의 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[다음](caching-data-in-the-architecture-cs.md)
