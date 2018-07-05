---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-cs
title: SqlDataSource 컨트롤 (C#)를 사용 하 여 데이터 쿼리 | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서 완벽 하 게 데이터 액세스 계층에서 프레젠테이션 계층을 분리 하 ObjectDataSource 컨트롤을 사용 했습니다. 이 안내가 사용 하 여 시작 하는 중...
ms.author: aspnetcontent
ms.date: 02/20/2007
ms.assetid: 60512d6a-b572-4b7a-beb3-3e44b4d2020c
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 6b9ca474b7a085302d287a223c08abe2fa5336b0
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815293"
---
<a name="querying-data-with-the-sqldatasource-control-c"></a>SqlDataSource 컨트롤 (C#)를 사용 하 여 데이터를 쿼리합니다.
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_47_CS.exe) 또는 [PDF 다운로드](querying-data-with-the-sqldatasource-control-cs/_static/datatutorial47cs1.pdf)

> 이전 자습서에서 완벽 하 게 데이터 액세스 계층에서 프레젠테이션 계층을 분리 하 ObjectDataSource 컨트롤을 사용 했습니다. 프레젠테이션 및 데이터 액세스 엄격 하 게 분리 하지 않아도 되는 간단한 응용 프로그램에 대 한 SqlDataSource 컨트롤을 사용할 수 있는 방법을 배울이 자습서를 시작 합니다.


## <a name="introduction"></a>소개

모든 자습서에서는 지금 검사 ve 프레젠테이션, 비즈니스 논리 및 데이터 액세스 계층으로 이루어진 계층화 된 아키텍처를 사용 합니다. (DAL (데이터 액세스 계층) 첫 번째 자습서에서 만들 되었습니다 ([데이터 액세스 레이어 만들기](../introduction/creating-a-data-access-layer-cs.md)) 및 두 번째에서 비즈니스 논리 계층 ([비즈니스 논리 레이어 만들기](../introduction/creating-a-business-logic-layer-cs.md)). 로 시작 합니다 [the ObjectDataSource 사용 하 여 데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) 자습서, ASP.NET 2.0 s 새 ObjectDataSource 컨트롤을 사용 하 여 선언적으로 프레젠테이션 계층에서 아키텍처와 인터페이스 하는 방법에 살펴보았습니다.

아키텍처를 사용 자습서를 지금의 모든 데이터로 작업을 하는 동안 액세스, 삽입, 업데이트 및 아키텍처를 우회 하는 ASP.NET 페이지에서 직접 데이터베이스 데이터를 삭제 하는 데 수 이기도 합니다. 이렇게 특정 데이터베이스 쿼리 및 비즈니스 논리는 웹 페이지에 직접 배치 합니다. 충분히 크고 복잡 한 응용 프로그램 디자인, 구현 및 계층화 된 아키텍처를 사용 하는 성공, 업데이트 가능성 및 유지 관리 응용 프로그램의 매우 중요 합니다. 그러나 강력한 아키텍처를 개발, 해야 할 수도 있습니다 하지 매우 간단 하 고 일회용 응용 프로그램을 만들 때.

ASP.NET 2.0은 5 개의 기본 제공 데이터 소스 컨트롤을 제공 [SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx)를 [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx)하십시오 [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx), [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx), 및 [SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx)합니다. Microsoft SQL Server, Microsoft Access, Oracle, MySQL 및 기타를 포함 하 여 관계형 데이터베이스에서 직접 데이터를 액세스 및 수정 SqlDataSource는 사용할 수 있습니다. 이 자습서에는 다음 세 SqlDataSource 컨트롤을 사용 하 여 작업, 삽입, 업데이트 및 데이터 삭제 SqlDataSource를 사용 하는 방법 뿐만 아니라 쿼리 하는 방법 및 필터 데이터베이스 데이터를 탐색 하는 방법을 살펴보겠습니다.


![ASP.NET 2.0에는 5 개의 기본 제공 데이터 소스 컨트롤이 포함 되어 있습니다.](querying-data-with-the-sqldatasource-control-cs/_static/image1.gif)

**그림 1**: ASP.NET 2.0에는 5 개의 기본 제공 데이터 소스 컨트롤이 포함 되어 있습니다.


## <a name="comparing-the-objectdatasource-and-sqldatasource"></a>ObjectDataSource, SqlDataSource 비교

개념적으로 SqlDataSource 및 ObjectDataSource 컨트롤은 데이터를 단순히 프록시입니다. 에 설명 된 대로 합니다 [the ObjectDataSource 사용 하 여 데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) 자습서에서는 ObjectDataSource에 속성을 선택 하기 위해 호출할 메서드와 데이터 삽입, 업데이트 및 데이터를 삭제 하는 개체 형식을 나타내는 기본 개체 형식입니다. 데이터 웹 컨트롤을 GridView, DetailsView 또는 DataList와 같은 ObjectDataSource s를 사용 하 여 컨트롤을 바인딩할 수는 ObjectDataSource 속성을 구성한 후 `Select()`, `Insert()`를 `Delete()`, 및 `Update()` 방법 기본 아키텍처와 상호 작용 합니다.

SqlDataSource 동일한 기능을 제공 하지만 개체 라이브러리 보다는 관계형 데이터베이스에 대해 작동 합니다. SqlDataSource를 사용 하 여 데이터베이스 연결 문자열 및 임시 SQL 쿼리를 지정 해야 했습니다 또는 저장 프로시저를 삽입, 업데이트, 삭제 및 데이터 검색을 실행 합니다. SqlDataSource s `Select()`, `Insert()`를 `Update()`, 및 `Delete()` 메서드를 호출 하는 경우 지정된 된 데이터베이스에 연결 하 고 적절 한 SQL 쿼리를 실행 합니다. 다음 다이어그램에서 볼 수 있듯이, 이러한 메서드는 데이터베이스에 연결, 쿼리를 실행 및 결과 반환 합니다. grunt 작업을 수행 합니다.


![SqlDataSource는 데이터베이스로 프록시로 사용](querying-data-with-the-sqldatasource-control-cs/_static/image2.gif)

**그림 2**: SqlDataSource는 데이터베이스로 프록시로 사용


> [!NOTE]
> 이 자습서에서는 데이터베이스에서 데이터를 검색할 집중적으로 다루겠습니다. 에 [삽입, 업데이트 및 SqlDataSource 컨트롤을 사용 하 여 데이터를 삭제 해도](inserting-updating-and-deleting-data-with-the-sqldatasource-cs.md) 자습서, SqlDataSource 삽입, 업데이트 및 삭제를 지원 하도록 구성 하는 방법을 살펴보겠습니다.


## <a name="the-sqldatasource-and-accessdatasource-controls"></a>SqlDataSource 및 AccessDataSource 컨트롤

SqlDataSource 컨트롤 외에도 ASP.NET 2.0은 또한 AccessDataSource 컨트롤에 연결 합니다. 이러한 두 가지 다른 컨트롤 발생할 대부분의 개발자 AccessDataSource 컨트롤은 Microsoft SQL Server에 단독으로 사용 하도록 디자인 된 SqlDataSource 컨트롤을 사용 하 여 Microsoft Access를 사용 하 여 단독으로 작동 하도록 설계 되었다는 주의 대상으로 ASP.NET 2.0에 있습니다. SqlDataSource 컨트롤을 사용 하 여 작동 합니다 AccessDataSource은 Microsoft Access를 사용 하 여 구체적으로 작동 되도록 설계 되었지만, *모든* .NET을 통해 액세스할 수 있는 관계형 데이터베이스입니다. 모든 OleDb 나 ODBC 호환 데이터 저장소, Microsoft SQL Server, Microsoft Access, Oracle, Informix, MySQL 및 PostgreSQL 등 다양 한 기타 포함 됩니다.

AccessDataSource, SqlDataSource 컨트롤 간의 유일한 차이점은 데이터베이스 연결 정보를 지정 하는 방법을 AccessDataSource 컨트롤에는 Access 데이터베이스 파일에 파일 경로만이 필요합니다. 반면에, SqlDataSource에는 전체 연결 문자열에 필요합니다.

## <a name="step-1-creating-the-sqldatasource-web-pages"></a>1 단계: SqlDataSource 웹 페이지 만들기

SqlDataSource 컨트롤을 사용 하 여 데이터베이스 데이터와 직접 작업 하는 방법을 탐색을 시작 하기 전에 s를 먼저 시간을 내어이 자습서에는 다음 세 할 웹 사이트 프로젝트에서 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `SqlDataSource`합니다. 다음에 있는 각 페이지에 연결할 수 있도록 해당 폴더에 다음 ASP.NET 페이지를 추가 합니다 `Site.master` 마스터 페이지:

- `Default.aspx`
- `Querying.aspx`
- `ParameterizedQueries.aspx`
- `InsertUpdateDelete.aspx`
- `OptimisticConcurrency.aspx`


![SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가](querying-data-with-the-sqldatasource-control-cs/_static/image3.gif)

**그림 3**: SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더와 같이 `Default.aspx` 에 `SqlDataSource` 폴더 섹션의 자습서를 나열 됩니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 사용자 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지의 솔루션 탐색기에서 끌어 합니다.


[![Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가](querying-data-with-the-sqldatasource-control-cs/_static/image5.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image4.gif)

**그림 4**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 `Default.aspx` ([클릭 하 여 큰 이미지 보기](querying-data-with-the-sqldatasource-control-cs/_static/image6.gif))


마지막으로, 이러한 네 가지 페이지 항목을 추가 합니다 `Web.sitemap` 파일입니다. 특히, DataList 및 반복기에 추가 사용자 지정 단추 후 다음 태그를 추가 `<siteMapNode>`:


[!code-sql[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample1.sql)]

업데이트 한 후 `Web.sitemap`, 잠시 브라우저를 통해 자습서 웹 사이트를 확인 합니다. 왼쪽 메뉴에는 이제 편집, 삽입 및 삭제 자습서에 대 한 항목이 포함 됩니다.


![사이트 맵 항목이 포함 되어 있습니다 SqlDataSource 자습서](querying-data-with-the-sqldatasource-control-cs/_static/image7.gif)

**그림 5**: 이제 사이트 맵 SqlDataSource 자습서에 대 한 항목을 포함


## <a name="step-2-adding-and-configuring-the-sqldatasource-control"></a>추가 하 고 SqlDataSource 컨트롤을 구성 하는 2 단계:

열어서 시작 합니다 `Querying.aspx` 페이지에 `SqlDataSource` 폴더 및 디자인 뷰로 전환 합니다. SqlDataSource 컨트롤 집합과 디자이너 도구 상자에서 끌어 해당 `ID` 에 `ProductsDataSource`입니다. ObjectDataSource가 마찬가지로 SqlDataSource 렌더링 된 출력을 생성 하지 않습니다 하 고 따라서 디자인 화면에서 회색 상자로 표시 됩니다. SqlDataSource를 구성 하려면 SqlDataSource s 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다.


![클릭 된 SqlDataSource s 스마트 태그에서 데이터 원본 연결 구성](querying-data-with-the-sqldatasource-control-cs/_static/image8.gif)

**그림 6**: 클릭을 SqlDataSource s 스마트 태그에서 데이터 원본 연결 구성


그러면 SqlDataSource 컨트롤의 데이터 소스 구성 마법사. S 마법사의 단계에 s ObjectDataSource 컨트롤에서 다를 있지만 최종 목표 동일 검색, 삽입, 업데이트 및 데이터 소스를 통해 데이터를 삭제 하는 방법에 세부 정보를 제공 합니다. SqlDataSource에 대 한이 수반 사용할 기본 데이터베이스를 지정 하 고 임시 SQL 문 또는 저장된 프로시저를 제공 합니다.

첫 번째 마법사 단계를 데이터베이스에 대 한 요청입니다. 드롭다운 목록에 포함 된 웹 응용 프로그램 s에 해당 데이터베이스 `App_Data` 폴더 및 서버 탐색기에서 데이터 연결 노드에 추가 되었습니다. 이후로 ve 이미 추가 대 한 연결 문자열을 `NORTHWIND.MDF` 데이터베이스에 `App_Data` s 프로젝트 폴더 `Web.config` 해당 연결 문자열에 대 한 참조를 포함 하는 파일을 드롭 다운 목록 `NORTHWINDConnectionString`합니다. 드롭다운 목록에서이 항목을 선택 하 고 클릭 합니다.


![위해 드롭다운 목록에서 선택](querying-data-with-the-sqldatasource-control-cs/_static/image9.gif)

**그림 7**: 선택 된 `NORTHWINDConnectionString` 드롭 다운 목록에서


데이터베이스를 선택한 후 마법사가 데이터를 반환 하도록 쿼리를 요청 합니다. 테이블 또는 뷰를 반환할 수는 사용자 지정 SQL 문 입력 또는 저장된 프로시저를 지정할 열 하거나 지정할 수 있습니다. 사용자 지정 SQL 문 또는 저장된 프로시저 및 테이블에서 열을 지정이이 선택한 지정을 통해 전환할 수도 있고 라디오 단추를 볼 수 있습니다.

> [!NOTE]
> 첫 번째 예를 들어 s를 테이블 또는 뷰 옵션에서 지정 열을 사용할 수 있습니다. 이 자습서의 뒷부분에서 설명 하 고 마법사로 돌아갑니다 하 고 사용자 지정 SQL 문 또는 저장된 프로시저 옵션을 지정을 탐색 합니다.


그림 8 화면은 구성 Select 문을 지정 라디오 단추를 테이블 또는 뷰 열을 선택 합니다. 드롭다운 목록에 선택한 테이블 또는 뷰의 열 아래 확인란을 선택 목록에 표시를 사용 하 여 Northwind 데이터베이스의 테이블 및 뷰 집합이 포함 합니다. 예를 들어 let s는 다음과 같이 반환 됩니다.는 `ProductID`, `ProductName`, 및 `UnitPrice` 의 열을 `Products` 테이블. 그림 8에 나와 것 처럼 결과 SQL 문은 표시 이러한 선택 항목 마법사 만들기 후 `SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`합니다.


![Products 테이블에서 데이터를 반환 합니다.](querying-data-with-the-sqldatasource-control-cs/_static/image10.gif)

**그림 8**: 데이터를 반환 합니다 `Products` 테이블


마법사를 구성한 후 합니다 `ProductID`, `ProductName`, 및 `UnitPrice` 열에서를 `Products` 테이블에서 다음 단추를 클릭 합니다. 이 최종 화면 이전 단계에서 구성 된 쿼리의 결과 검사할 수 있는 기회를 제공 합니다. 쿼리 테스트 단추를 클릭 하면 구성 된 실행 `SELECT` 문과 표에 결과 표시 합니다.


![선택 쿼리를 검토 하려면 테스트 쿼리 단추를 클릭](querying-data-with-the-sqldatasource-control-cs/_static/image11.gif)

**그림 9**: 검토에 대 한 테스트 쿼리 단추를 클릭 하 여 `SELECT` 쿼리


마법사를 완료 하려면 마침을 클릭 합니다.

ObjectDataSource를 사용 하 여 SqlDataSource의 마법사 단순히 값을 할당 s control 속성, 즉 같은 합니다 [ `ConnectionString` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.connectionstring.aspx) 하 고 [ `SelectCommand` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommand.aspx) 속성입니다. 마법사를 완료 한 후 SqlDataSource 컨트롤 s 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample2.aspx)]

`ConnectionString` 속성 데이터베이스에 연결 하는 방법에 대해 설명 합니다. 이 속성을 완전 하 고 하드 코드 된 연결 문자열 값을 할당할 수 있습니다 하거나 연결 문자열을 가리킬 수 있습니다 `Web.config`합니다. Web.config에서 연결 문자열 값을 참조 하려면 구문을 사용 하 여 `<%$ expressionPrefix:expressionValue %>`입니다. 일반적으로 *expressionPrefix* ConnectionStrings는 및 *expressionValue* 의 연결 문자열의 이름입니다 합니다 `Web.config` [ `<connectionStrings>` 섹션](https://msdn.microsoft.com/library/bf7sd233.aspx)합니다. 구문을 사용할 수 있지만 참조 `<appSettings>` 요소 또는 리소스 파일의 콘텐츠입니다. 참조 [ASP.NET 식 개요](https://msdn.microsoft.com/library/d5bd1tad.aspx) 이 구문에 대 한 자세한 내용은 합니다.

`SelectCommand` 임시 SQL 문이나 저장된 프로시저 실행 데이터를 반환 하도록 속성을 지정 합니다.

## <a name="step-3-adding-a-data-web-control-and-binding-it-to-the-sqldatasource"></a>3 단계: 데이터 웹 컨트롤을 추가 하 고 SqlDataSource에 바인딩

SqlDataSource를 구성한 후 데이터 GridView 또는 DetailsView와 같은 웹 컨트롤을 바인딩할 수 있습니다. 이 자습서에서는 s GridView에 데이터를 표시 하도록 합니다. 도구 상자에서 GridView를 페이지로 끌어서에 바인딩하는 `ProductsDataSource` SqlDataSource GridView가 스마트 태그의 드롭다운 목록에서 데이터 소스를 선택 하 여 합니다.


[![GridView를 추가 하 고 SqlDataSource 컨트롤에 바인딩](querying-data-with-the-sqldatasource-control-cs/_static/image13.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image12.gif)

**그림 10**: GridView를 추가 하 고 SqlDataSource 컨트롤에 바인딩합니다 ([큰 이미지를 보려면 클릭](querying-data-with-the-sqldatasource-control-cs/_static/image14.gif))


적 GridView가 스마트 태그의 드롭다운 목록에서 SqlDataSource 컨트롤을 선택 하면 Visual Studio는 자동으로 추가 BoundField 또는 CheckBoxField GridView에 각 데이터 소스 컨트롤에 의해 반환 되는 열에 대 한 합니다. SqlDataSource 세 가지 데이터베이스 열을 반환 하므로 `ProductID`, `ProductName`, 및 `UnitPrice` GridView에 세 개의 필드가 있습니다.

GridView가의 3을 구성 하려면 잠시 BoundFields입니다. 변경 된 `ProductName` 필드 s `HeaderText` 속성을 제품 이름 및 `UnitPrice` 가격 필드 s입니다. 형식을 지정할 수는 `UnitPrice` 통화 필드입니다. 이러한 수정을 마치면 GridView가 선언적 태그 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample3.aspx)]

브라우저를 통해이 페이지를 방문 합니다. GridView가 각 제품이 나열 그림 11에서 알 수 있듯이 `ProductID`, `ProductName`, 및 `UnitPrice` 값입니다.


[![각 제품의 ProductID, ProductName, 및 UnitPrice 값을 표시 하는 GridView](querying-data-with-the-sqldatasource-control-cs/_static/image16.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image15.gif)

**그림 11**: The GridView 표시 각 제품 s `ProductID`를 `ProductName`, 및 `UnitPrice` 값 ([클릭 하 여 큰 이미지 보기](querying-data-with-the-sqldatasource-control-cs/_static/image17.gif))


해당 페이지를 방문 하는 경우 GridView가 해당 데이터 소스 제어를 호출 하는 `Select()` 메서드. ObjectDataSource 컨트롤을 사용할 때는이 호출을 `ProductsBLL` s 클래스 `GetProducts()` 메서드. 그러나 SqlDataSource와 함께 합니다 `Select()` 메서드는 지정 된 데이터베이스 및 문제에 대 한 연결을 설정 하는 `SelectCommand` (`SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`,이 예제의). SqlDataSource는 GridView 열거를 반환 하는 각 데이터베이스 레코드에 대 한 gridview 행 만들기의 결과 반환 합니다.

## <a name="the-built-in-data-web-control-features-and-the-sqldatasource-control"></a>기본 제공 데이터 웹 제어 기능과 SqlDataSource 컨트롤

일반적으로 웹 컨트롤 페이징, 정렬, 편집, 데이터에 내재 된 기능 삭제, 삽입 및 등 데이터 웹 컨트롤에 특정 되며 사용 되는 데이터 소스 컨트롤에 종속 되지 않습니다. 즉, GridView에는 해당 기본 제공 페이징, 정렬, 편집 및 삭제는 ObjectDataSource 또는 SqlDataSource에 바인딩되어 있는지 여부를 활용할 수 있습니다. 그러나 특정 데이터 웹 제어 기능은 사용 중인 데이터 소스 컨트롤 또는 데이터 소스 컨트롤의 구성에 민감합니다.

예를 들어 합니다 [효율적으로 페이징을 통해 많은 양의 데이터](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md) 자습서를 기본적으로 웹 데이터에 대 한 페이징 논리 제어 잡이 반환 하는 것이 설명한 *모든* 기본 레코드 데이터 원본 및 다음 적절 한 현재 페이지 인덱스 및 한 페이지에 표시할 레코드 수를 지정 하는 레코드의 하위 집합만 표시 됩니다. 이 모델 충분히 큰 결과 집합을 페이징할 때는 매우 비효율적입니다. 다행 스럽게도 표시할 레코드의 하위 집합에 정확 하 게 반환 하는 사용자 지정 페이징을 지원 하기 위해 ObjectDataSource는 구성할 수 있습니다. 그러나 SqlDataSource 컨트롤에는 사용자 지정 페이징을 구현에 대 한 속성에 부족 합니다.

SqlDataSource를 사용 하 여 페이징 및 정렬를 사용 하 여 다른 미묘한 문제가 발생 합니다. 기본적으로 SqlDataSource에서 반환 되는 데이터 페이징 또는 GridView를 통해 정렬할 수 있습니다. 이 보여 주기 위해에 GridView s 스마트 태그가 사용 하도록 설정 페이징 및 정렬 사용 옵션을 선택 `Querying.aspx` 이 예상 대로 작동 하는지 확인 합니다.

정렬 및 페이징 SqlDataSource 느슨하게 형식화 된 데이터 집합으로 데이터베이스 데이터를 검색 하기 때문에 작동 합니다. 데이터 집합의 페이징을 구현 하는 데 핵심적인 부분을 쿼리에서 반환 하는 레코드의 총 수를 조사할 수 있습니다. 또한 DataView를 통해 데이터 집합의 결과 정렬할 수 있습니다. 이러한 기능은 GridView 요청 페이징 또는 정렬 된 데이터에 자동으로 SqlDataSource에서 사용 됩니다.

SqlDataSource를 변경 하 여 데이터 집합 대신 DataReader를 반환할 구성할 수 있습니다 해당 [ `DataSourceMode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx) 에서 `DataSet` (기본값)를 `DataReader`입니다. DataReader를 필요로 하는 기존 코드 SqlDataSource가의 결과 전달 하는 경우 상황에서 DataReader를 사용 하 여을 선호 될 수 있습니다. 또한 Datareader 데이터 집합 보다 훨씬 단순한 개체와 되므로 더 나은 성능을 제공 합니다. 그러나,이 변경을 수행 하는 경우 데이터 웹 컨트롤 모두 정렬할 수 있습니다 하거나 SqlDataSource 레코드 수는 쿼리에 의해 반환 됩니다 확인할 수 없습니다. 않으며 DataReader 이후 페이지에서 반환 된 데이터를 정렬 하는 모든 기술을 제공 합니다.

## <a name="step-4-using-a-custom-sql-statement-or-stored-procedure"></a>4 단계: 사용자 지정 SQL 문을 사용 하 여 또는 저장 프로시저

SqlDataSource 컨트롤을 구성할 때 또는 기존 테이블 또는 뷰 열 사용자 지정 SQL 문 또는 저장된 프로시저를로 데이터를 반환 하는 쿼리 두 가지 방법 중 하나로 지정할 수 있습니다. 우리는 2 단계에서에서에서 열을 선택 하 여 `Products` 테이블입니다. 가 사용자 지정 SQL 문을 사용 하 여 살펴볼 수 있습니다.

다른 GridView 컨트롤을 추가 합니다 `Querying.aspx` 페이지 및 스마트 태그의 드롭다운 목록에서 새 데이터 원본을 만들려면 선택 합니다. 다음으로 표시는 데이터를 가져와서 데이터베이스에서이 새 SqlDataSource 컨트롤을 만듭니다. 컨트롤의 이름을 `ProductsWithCategoryInfoDataSource`입니다.


![ProductsWithCategoryInfoDataSource 라는 새 SqlDataSource 컨트롤 만들기](querying-data-with-the-sqldatasource-control-cs/_static/image18.gif)

**그림 12**: 라는 새 SqlDataSource 컨트롤 만들기 `ProductsWithCategoryInfoDataSource`


다음 화면에서는 데이터베이스를 지정 합니다. 그림 7 년대에서 했던 것 처럼 선택 된 `NORTHWINDConnectionString` 드롭다운 목록에서 나열 하 고 다음을 클릭 합니다. Select 문 화면 구성 지정을 사용자 지정 SQL 문 또는 저장된 프로시저 라디오 단추를 선택 하 고 클릭 합니다. SELECT, UPDATE, INSERT 및 DELETE를 레이블이 지정 된 탭을 제공 하는 사용자 지정 문 또는 저장 프로시저 정의 화면으로 표시 됩니다. 각 탭에서 텍스트 상자에 사용자 지정 SQL 문을 입력 하 하거나 드롭다운 목록에서 저장된 프로시저를 선택할 수 있습니다. 이 자습서에서는 사용자 지정 SQL 문; 입력 살펴보겠습니다. 다음 자습서는 저장된 프로시저를 사용 하는 예제를 포함 합니다.


![사용자 지정 SQL 문을 입력 하거나 저장된 프로시저를 선택 합니다.](querying-data-with-the-sqldatasource-control-cs/_static/image19.gif)

**그림 13**: 사용자 지정 SQL 문을 입력 하거나 저장된 프로시저를 선택 합니다.


사용자 지정 SQL 문 텍스트 상자에 직접 입력할 수 있습니다 또는 쿼리 작성기 단추를 클릭 하 여 그래픽 방식으로 생성할 수 있습니다. 쿼리 작성기 또는 텍스트 상자에서 반환할 다음 쿼리를 사용 합니다 `ProductID` 및 `ProductName` 에서 필드를 `Products` 를 사용 하 여 테이블을 `JOIN` s 제품을 검색 하 `CategoryName` 에서 `Categories` 테이블:


[!code-sql[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample4.sql)]


![생성할 수 있습니다 그래픽 방식으로 쿼리를 통해 쿼리 작성기](querying-data-with-the-sqldatasource-control-cs/_static/image20.gif)

**그림 14**: 있습니다 생성 그래픽 쿼리 작성기를 사용 하 여 쿼리


쿼리를 지정한 후 쿼리 테스트 화면으로 이동 하려면 다음을 클릭 합니다. SqlDataSource 마법사를 완료 하려면 마침을 클릭 합니다.

마법사를 완료 한 후 GridView 세 BoundFields 표시에 추가 해야 합니다 `ProductID`, `ProductName`, 및 `CategoryName` 열 쿼리에서 반환 되 고 다음 선언적 태그에서 결과:


[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample5.aspx)]


[![GridView 각 s 제품 ID, 이름 및 연결 된 범주 이름을 보여 줍니다.](querying-data-with-the-sqldatasource-control-cs/_static/image22.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image21.gif)

**그림 15**: GridView를 보여 줍니다 각 제품 ID, 이름 및 연결 된 범주 이름 ([큰 이미지를 보려면 클릭](querying-data-with-the-sqldatasource-control-cs/_static/image23.gif))


## <a name="summary"></a>요약

이 자습서에서는 쿼리 SqlDataSource 컨트롤을 사용 하 여 데이터를 표시 하는 방법을 살펴보았습니다. 같은 ObjectDataSource, SqlDataSource 데이터에 액세스 하는 선언적 방법을 제공 하는 프록시 역할도 합니다. 속성과 연결할 데이터베이스 및 SQL 지정 `SELECT` 실행할 쿼리; 속성 창을 통해 또는 데이터 소스 구성 마법사를 사용 하 여 지정할 수 있습니다.

`SELECT` 이 자습서에서는 검사할 쿼리 예제 쿼리에서 반환 된 레코드를 모두 지정 합니다. 그러나 SqlDataSource 컨트롤을 포함할 수는 `WHERE` 값 프로그래밍 방식으로 할당 되거나 자동으로 지정된 된 소스에서 가져온 매개 변수를 사용 하 여 절. 만들고 다음 자습서에서 매개 변수가 있는 쿼리를 사용 하는 방법을 살펴보겠습니다.

즐거운 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [관계형 데이터베이스 데이터에 액세스](http://aspnet.4guysfromrolla.com/articles/022206-1.aspx)
- [SqlDataSource 컨트롤 개요](https://msdn.microsoft.com/library/dz12d98w.aspx)
- [ASP.NET 퀵 스타트 자습서: SqlDataSource 컨트롤](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/sqldatasource.aspx)
- [Web.config `<connectionStrings>` 요소](https://msdn.microsoft.com/library/bf7sd233.aspx)
- [데이터베이스 연결 문자열 참조](http://www.connectionstrings.com/)

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Susan Connery, 박 광 준 Leigh 및 David Suru 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](using-parameterized-queries-with-the-sqldatasource-cs.md)
