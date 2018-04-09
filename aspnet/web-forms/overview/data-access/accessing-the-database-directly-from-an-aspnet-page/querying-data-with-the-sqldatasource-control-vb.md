---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb
title: SqlDataSource 컨트롤 (VB)를 사용 하 여 데이터를 쿼리 합니다. | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서 완벽 하 게 데이터 액세스 계층에서 프레젠테이션 계층을 구분 하려면 ObjectDataSource 컨트롤을 사용 했습니다. 이 안내가으로 시작 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2007
ms.topic: article
ms.assetid: b12f752d-3502-40a4-b695-fc7b7d08cfd3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 6f886ca85a2a4dea5daeff109370bedc1a3f7265
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="querying-data-with-the-sqldatasource-control-vb"></a>SqlDataSource 컨트롤 (VB)를 사용 하 여 데이터를 쿼리합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_47_VB.exe) 또는 [PDF 다운로드](querying-data-with-the-sqldatasource-control-vb/_static/datatutorial47vb1.pdf)

> 이전 자습서에서 완벽 하 게 데이터 액세스 계층에서 프레젠테이션 계층을 구분 하려면 ObjectDataSource 컨트롤을 사용 했습니다. 프레젠테이션 및 데이터 액세스 엄격 하 게 분리 필요 하지 않은 간단한 응용 프로그램에 대 한 SqlDataSource 컨트롤을 사용할 수 있는 방법을 배울이 자습서를 시작 합니다.


## <a name="introduction"></a>소개

이 자습서의 모든에서는 지금까지 검사 했습니다 프레젠테이션, 비즈니스 논리 및 데이터 액세스 계층의 계층화 된 아키텍처를 사용 했습니다. 첫 번째 자습서에서 (DAL (데이터 액세스 계층) 트 되었습니다 ([데이터 액세스 계층을 만들려면](../introduction/creating-a-data-access-layer-vb.md)) 및 두 번째에서 비즈니스 논리 계층 ([는 비즈니스 논리 계층을 만드는](../introduction/creating-a-business-logic-layer-vb.md)). 부터는 [the ObjectDataSource와 데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) 자습서, ASP.NET 2.0 s 새 ObjectDataSource 컨트롤 선언적으로 프레젠테이션 계층에서 아키텍처와 인터페이스 하는 데 사용 하는 방법에 살펴보았습니다.

아키텍처 사용해본 지금까지 자습서의 모든 데이터로 작업 하는 것도 액세스, 삽입, 업데이트 및 아키텍처를 우회 하는 ASP.NET 페이지에서 직접 데이터베이스 데이터를 삭제할 수 있습니다. 이 위치는 특정 데이터베이스 쿼리 및 비즈니스 논리는 웹 페이지에 직접 합니다. 충분히 크거나 복잡 한 응용 프로그램 디자인, 구현 및 계층 구성된 구조를 사용 하는 성공, 업데이트 가능성 및 응용 프로그램의 유지 관리에 대 한 매우 중요 합니다. 하지만 강력한 아키텍처를 개발 할 수 있습니다 하지 매우 간단 하 고 일회용 응용 프로그램을 만들 때.

ASP.NET 2.0에서는 5 개의 기본 제공 데이터 소스 컨트롤을 제공 [SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx), [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx), [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx), [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx), 및 [SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx)합니다. SqlDataSource 액세스 하 고 Microsoft SQL Server, Microsoft Access, Oracle, MySQL 및 다른 사용자를 포함 하 여 관계형 데이터베이스에서 직접 데이터를 수정할 데 사용할 수 있습니다. 이 자습서에는 다음 세 SqlDataSource 컨트롤 작업, 삽입, 업데이트 및 데이터 삭제를 SqlDataSource를 사용 하는 방법 뿐만 아니라 쿼리 하는 방법을 필터 데이터베이스 데이터를 탐색 하는 방법을 검토 합니다.


![ASP.NET 2.0 5 개의 기본 제공 데이터 소스 제어를 포함합니다.](querying-data-with-the-sqldatasource-control-vb/_static/image1.gif)

**그림 1**: ASP.NET 2.0에 5 개의 기본 제공 데이터 소스 컨트롤이 포함 됩니다.


## <a name="comparing-the-objectdatasource-and-sqldatasource"></a>ObjectDataSource 및 SqlDataSource 비교

개념적으로 ObjectDataSource와 SqlDataSource 컨트롤은 데이터를 단순히 프록시입니다. 에 설명 된 대로 [the ObjectDataSource와 데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) 자습서는 ObjectDataSource 제공을 선택 하기 위해 호출할 메서드와 데이터 삽입, 업데이트 및 데이터를 삭제 하는 개체 유형을 나타내는 속성에는 기본 개체 형식입니다. ObjectDataSource s를 사용 하 여 컨트롤에 데이터 GridView, DetailsView, 또는 DataList 같은 웹 컨트롤을 바인딩할 수 ObjectDataSource의 속성을 구성한 후 `Select()`, `Insert()`, `Delete()`, 및 `Update()` 하는 메서드 기본 아키텍처와 상호 작용 합니다.

SqlDataSource 동일한 기능을 제공 하지만 개체 라이브러리 보다는 관계형 데이터베이스에 대해 작동 합니다. SqlDataSource를 사용 데이터베이스 연결 문자열 및 임시 SQL 쿼리를 지정 해야 우리 또는 저장 프로시저를 삽입, 업데이트, 삭제 및 데이터 검색을 실행 합니다. SqlDataSource s `Select()`, `Insert()`, `Update()`, 및 `Delete()` 메서드를 호출 하면 지정된 된 데이터베이스에 연결 하 고 적절 한 SQL 쿼리를 실행 합니다. 다이어그램에서 같이 다음, 이러한 방법이 데이터베이스에 연결 하는 쿼리를 실행 하 고 결과 반환 하는 힘든 작업을 수행 합니다.


![데이터베이스에 프록시로 사용 되어 SqlDataSource](querying-data-with-the-sqldatasource-control-vb/_static/image2.gif)

**그림 2**: 데이터베이스에 프록시로 사용 되어 SqlDataSource


> [!NOTE]
> 이 자습서에서는 집중적으로 살펴봅니다 데이터베이스에서 데이터를 검색 합니다. 에 [삽입, 업데이트 및 SqlDataSource 컨트롤을 사용 하 여 삭제 데이터](inserting-updating-and-deleting-data-with-the-sqldatasource-vb.md) 자습서, 삽입, 업데이트 및 삭제를 지원 하기 위해 SqlDataSource를 구성 하는 방법을 살펴보겠습니다.


## <a name="the-sqldatasource-and-accessdatasource-controls"></a>SqlDataSource 및 AccessDataSource 컨트롤

SqlDataSource 컨트롤 외에 ASP.NET 2.0 AccessDataSource 컨트롤에 포함 됩니다. 이러한 두 가지 다른 컨트롤 많은 개발자에 게 AccessDataSource 컨트롤 Microsoft SQL Server에 단독으로 사용할 수 있는 Microsoft Access 에서만 작동 하도록 설계 되었습니다 떨어지면 ASP.NET 2.0에 새로 될 있습니다. SqlDataSource 컨트롤 연동는 AccessDataSource Microsoft Access로 작동 하도록 설계 된, 반면 *모든* .NET을 통해 액세스할 수 있는 관계형 데이터베이스입니다. 모든 OleDb 또는 ODBC 규격 같은 데이터 저장소를 Microsoft SQL Server, Microsoft Access, Oracle, Informix, MySQL 및 PostgreSQL, 다양 한 기타 포함 됩니다.

AccessDataSource과 SqlDataSource 컨트롤 간의 유일한 차이점은 데이터베이스 연결 정보를 지정 하는 방법을 합니다. AccessDataSource 컨트롤 Access 데이터베이스 파일에 파일 경로만 필요합니다. 반면에, SqlDataSource 전체 연결 문자열을 필요합니다.

## <a name="step-1-creating-the-sqldatasource-web-pages"></a>1 단계: SqlDataSource 웹 페이지 만들기

SqlDataSource 컨트롤을 사용 하 여 데이터베이스 데이터와 직접 작업 하는 방법을 탐색을 시작 하기 전에 s를 먼저 잠시이 자습서와 다음 3에 대 한 사용 해야 하는 웹 사이트 프로젝트에 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `SqlDataSource`합니다. 다음에 해당 폴더에 있는 각 페이지에 연결할 수 있도록 다음 ASP.NET 페이지 추가 `Site.master` 마스터 페이지:

- `Default.aspx`
- `Querying.aspx`
- `ParameterizedQueries.aspx`
- `InsertUpdateDelete.aspx`
- `OptimisticConcurrency.aspx`


![SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가](querying-data-with-the-sqldatasource-control-vb/_static/image3.gif)

**그림 3**: SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더에서와 같이 `Default.aspx` 에 `SqlDataSource` 폴더는 해당 섹션의 자습서를 나열 합니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 이 기능을 제공 하는 사용자 정의 컨트롤입니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지 하려면 솔루션 탐색기에서 끌어서 합니다.


[![Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](querying-data-with-the-sqldatasource-control-vb/_static/image5.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image4.gif)

**그림 4**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](querying-data-with-the-sqldatasource-control-vb/_static/image6.gif))


마지막으로, 이러한 4 개 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히, 추가 사용자 지정 단추 다음 DataList 및 반복기에 다음 태그를 추가 `<siteMapNode>`:


[!code-sql[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample1.sql)]

업데이트 한 후 `Web.sitemap`, 브라우저를 통해 자습서 웹 사이트를 보려면 보십시오. 왼쪽 메뉴에는 이제 편집, 삽입 및 삭제 자습서에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 SqlDataSource 자습서에 대 한 항목을 포함](querying-data-with-the-sqldatasource-control-vb/_static/image7.gif)

**그림 5**: 이제 사이트 맵 SqlDataSource 자습서에 대 한 항목을 포함


## <a name="step-2-adding-and-configuring-the-sqldatasource-control"></a>2 단계: 추가 및 SqlDataSource 컨트롤 구성

열어 시작는 `Querying.aspx` 페이지에 `SqlDataSource` 폴더와 디자인 뷰로 전환 합니다. SqlDataSource 컨트롤을 도구 상자에서 디자이너와 세트가으로 끌어 해당 `ID` 를 `ProductsDataSource`합니다. ObjectDataSource를와 마찬가지로 SqlDataSource는 렌더링 된 출력을 생성 하지 않는 하 고 디자인 화면에서 회색 상자로 따라서 나타납니다. SqlDataSource를 구성 하려면 SqlDataSource s 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다.


![클릭는 SqlDataSource s 스마트 태그에서 데이터 원본 링크를 구성 합니다.](querying-data-with-the-sqldatasource-control-vb/_static/image8.gif)

**그림 6**: 클릭는 SqlDataSource s 스마트 태그에서 데이터 원본 링크를 구성 합니다.


SqlDataSource 컨트롤의 데이터 소스 구성 마법사가 표시 됩니다. ObjectDataSource 컨트롤 s에서에서 s 마법사의 단계 다르지만, 최종 목표는 동일한 작업을 검색, 삽입, 업데이트 및 데이터 소스를 통해 데이터를 삭제 하는 방법에 세부 정보를 제공 합니다. SqlDataSource에 대 한이 수반 사용할 기본 데이터베이스를 지정 하 고 임시 SQL 문 또는 저장된 프로시저를 제공 합니다.

첫 번째 마법사 단계 라는 데이터베이스에 대 한 메시지가 나타납니다. 웹 응용 프로그램 s에 해당 데이터베이스를 포함 하는 드롭 다운 목록 `App_Data` 폴더 및 서버 탐색기에서 데이터 연결 노드를 추가 합니다. 에서는 이후 했습니다 이미 추가 대 한 연결 문자열은 `NORTHWIND.MDF` 여기에 데이터베이스는 `App_Data` s 우리의 프로젝트 폴더 `Web.config` 파일 드롭 다운 목록에는 해당 연결 문자열에 대 한 참조가 포함 됩니다 `NORTHWINDConnectionString`합니다. 드롭다운 목록에서이 항목을 선택 하 고 클릭 합니다.


![위해 드롭 다운 목록에서 선택](querying-data-with-the-sqldatasource-control-vb/_static/image9.gif)

**그림 7**: 선택 된 `NORTHWINDConnectionString` 드롭 다운 목록에서


데이터베이스를 선택한 후 마법사는 데이터를 반환 하도록 쿼리를 요청 합니다. 테이블 또는 뷰를 반환 하거나 사용자 지정 SQL 문을 입력 하거나 지정할 수는 저장된 프로시저의 열 지정할 수 있습니다. 사용자 지정 SQL 문 또는 저장된 프로시저와 테이블 열 지정 지정을 통해이 선택 항목 사이 전환 하거나 라디오 단추를 볼 수 있습니다.

> [!NOTE]
> 이 첫 번째 예제에 대 한 열 지정 테이블 또는 뷰 옵션을 사용 하 여 s를 사용 합니다. 이 자습서의 뒷부분에 나오는 마법사로 돌아가서 알아보고 사용자 지정 SQL 문 또는 저장된 프로시저 옵션 지정 탐색 하겠습니다.


그림 8 화면은 다음 구성 Select 문 열 지정 테이블 또는 뷰 라디오 단추를 선택 합니다. 드롭 다운 목록에는 선택한 테이블 또는 뷰의 열 아래의 확인란을 선택 목록에 표시 된 Northwind 데이터베이스의 테이블 및 뷰 집합이 포함 됩니다. 예를 들어 s let 반환는 `ProductID`, `ProductName`, 및 `UnitPrice` 열을는 `Products` 테이블입니다. 볼 수 있듯이 그림 8 결과 SQL 문은 표시 마법사 이러한 선택 항목을 만드는 후 `SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`합니다.


![Products 테이블에서 데이터를 반환 합니다.](querying-data-with-the-sqldatasource-control-vb/_static/image10.gif)

**그림 8**:에서 데이터를 반환 된 `Products` 테이블


마법사를 구성 했으면는 `ProductID`, `ProductName`, 및 `UnitPrice` 열을는 `Products` 테이블에서 다음 단추를 클릭 합니다. 이 마지막 화면 이전 단계에서 구성 된 쿼리의 결과 검사를 제공 합니다. 쿼리 테스트 단추를 클릭 하면 구성 된 실행 `SELECT` 문과 결과 표로 표시 합니다.


![선택 쿼리를 검토 하려면 테스트 쿼리 단추를 클릭](querying-data-with-the-sqldatasource-control-vb/_static/image11.gif)

**그림 9**: 검토 하려면 테스트 쿼리 단추를 클릭 하면 `SELECT` 쿼리


마법사를 완료 하려면 마침을 클릭 합니다.

ObjectDataSource를와 SqlDataSource의 마법사 단순히 값을 할당 컨트롤의 속성 즉 처럼는 [ `ConnectionString` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.connectionstring.aspx) 및 [ `SelectCommand` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommand.aspx) 속성입니다. 마법사를 완료 한 후 SqlDataSource 컨트롤 s 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample2.aspx)]

`ConnectionString` 속성 데이터베이스에 연결 하는 방법에 대해 설명 합니다. 이 속성 완료 하드 코드 된 연결 문자열 값을 할당 하거나에서 연결 문자열을를 가리킬 수 `Web.config`합니다. Web.config의 연결 문자열 값을 참조 하려면 구문을 사용 하 여 `<%$ expressionPrefix:expressionValue %>`합니다. 일반적으로 *expressionPrefix* ConnectionStrings은 및 *expressionValue* 에서 연결 문자열의 이름인는 `Web.config` [ `<connectionStrings>` 섹션](https://msdn.microsoft.com/library/bf7sd233.aspx)합니다. 하지만 구문을 사용 참조에 `<appSettings>` 요소 또는 리소스 파일에서 콘텐츠입니다. 참조 [ASP.NET 식 개요](https://msdn.microsoft.com/library/d5bd1tad.aspx) 이 구문에 대 한 자세한 합니다.

`SelectCommand` 속성 임시 SQL 문 또는 저장된 프로시저 실행 데이터를 반환할 수를 지정 합니다.

## <a name="step-3-adding-a-data-web-control-and-binding-it-to-the-sqldatasource"></a>3 단계: 데이터 웹 컨트롤을 추가 하 고 SqlDataSource에 바인딩

SqlDataSource를 구성한 후 데이터 GridView 또는 DetailsView 같은 웹 컨트롤을 바인딩할 수 있습니다. 이 자습서에 대 한 s는 GridView에 데이터를 표시 하도록 합니다. 도구 상자에서는 GridView를 페이지로 끌어서에 바인딩할는 `ProductsDataSource` SqlDataSource GridView s 스마트 태그에서 드롭 다운 목록에서 데이터 원본을 선택 하 여 합니다.


[![GridView를 추가 하 고 SqlDataSource 컨트롤에 바인딩](querying-data-with-the-sqldatasource-control-vb/_static/image13.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image12.gif)

**그림 10**:는 GridView를 추가 하 고 SqlDataSource 컨트롤에 바인딩할 ([전체 크기 이미지를 보려면 클릭](querying-data-with-the-sqldatasource-control-vb/_static/image14.gif))


적 GridView s 스마트 태그에서 드롭 다운 목록에서 SqlDataSource 컨트롤을 선택 하면 Visual Studio는 자동으로 추가 BoundField 또는 CheckBoxField GridView 각 데이터 소스 컨트롤에 의해 반환 되는 열에 대 한. SqlDataSource 3 개 데이터베이스 열을 반환 하므로 `ProductID`, `ProductName`, 및 `UnitPrice` GridView에 세 개의 필드가 있다고 합니다.

GridView의 3을 구성을 BoundFields 합니다. 변경 된 `ProductName` 필드 s `HeaderText` 속성을 제품 이름 및 `UnitPrice` 필드의 가격을 합니다. 형식을 지정할 수도 `UnitPrice` 통화로 필드입니다. 이러한 수정에 확인 한 후 GridView s 선언 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample3.aspx)]

브라우저를 통해이 페이지를 방문 합니다. GridView 각 제품 s 나열 그림 11에서 볼 수 있듯이 `ProductID`, `ProductName`, 및 `UnitPrice` 값입니다.


[![각 제품의 ProductID, ProductName, 및 UnitPrice 값을 표시 하는 GridView](querying-data-with-the-sqldatasource-control-vb/_static/image16.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image15.gif)

**그림 11**: GridView 표시 각 제품의 s `ProductID`, `ProductName`, 및 `UnitPrice` 값 ([전체 크기 이미지를 보려면 클릭](querying-data-with-the-sqldatasource-control-vb/_static/image17.gif))


해당 페이지를 방문 GridView가 해당 데이터 소스 제어 s 호출 `Select()` 메서드. ObjectDataSource 컨트롤을 사용할 때는이 호출의 `ProductsBLL` s 클래스 `GetProducts()` 메서드. 그러나 SqlDataSource와는 `Select()` 지정한 데이터베이스 및 문제에 대 한 연결을 설정 하는 메서드는 `SelectCommand` (`SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`,이 예에서). SqlDataSource 열거 하는 GridView 다음을 반환 하는 각 데이터베이스 레코드에 대 한 GridView에서 행을 만드는 해당 결과 반환 합니다.

## <a name="the-built-in-data-web-control-features-and-the-sqldatasource-control"></a>기본 제공 데이터 웹 제어 기능 및 SqlDataSource 컨트롤

일반적으로 웹 컨트롤 페이징, 정렬, 편집, 데이터에 내재 된 기능을 삭제, 삽입 및 등은 데이터 웹 컨트롤에 관련 되며 사용 되는 데이터 소스 제어에 종속 되지 않습니다. 즉, GridView에는 해당 기본 제공 페이징, 정렬, 편집 및 삭제는 ObjectDataSource 또는 SqlDataSource에 바인딩되어 있는지 여부를 활용할 수 있습니다. 그러나 특정 데이터 제어 기능 웹은 사용 중인 데이터 소스 제어에 또는 데이터 소스 제어의 구성에 민감합니다.

예를 들어는 [효율적으로 통해 큰 크기의 데이터를 페이징](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md) 자습서, 기본적으로 웹 데이터에 대 한 페이징 논리 제어 하는 방법을 아무렇게나 반환 설명한 *모든* 내부에서 레코드 데이터 원본 및 현재 페이지 인덱스 및 한 페이지에 표시할 레코드 수가 지정 된 레코드의 하위 집합에 적절 한를 표시 합니다. 충분히 큰 결과 집합을 페이징 하는 경우이 모델은 매우 효율적으로 하지 않습니다. 다행히는 ObjectDataSource 정확 하 게 표시할 레코드의 하위 집합만 반환 하는 사용자 지정 페이징을 지원 하도록 구성할 수 있습니다. 그러나 SqlDataSource 컨트롤에는 사용자 지정 페이징을 구현에 대 한 속성에 부족 합니다.

SqlDataSource 발생 페이징 및 정렬 된 또 다른 주의 해야 합니다. 기본적으로는 SqlDataSource에서 반환 된 데이터 페이징 또는 GridView를 통해 정렬할 수 있습니다. 이 증명 하려면 GridView s 스마트 태그에서 페이징 사용 및 정렬 사용 옵션을 확인 `Querying.aspx` 이 예상 대로 작동 하는지 확인 합니다.

정렬 및 페이징을 SqlDataSource 자유로운 형식의 데이터 집합에는 데이터베이스 데이터를 검색 하기 때문에 작동 합니다. 데이터 집합에서 쿼리에 의해 반환 되는 필수적인 측면 페이징을 구현 하는 레코드의 총 수를 조사할 수 있습니다. 또한 데이터 집합의 결과 DataView를 통해 정렬할 수 있습니다. 이러한 기능은 GridView 요청 페이징 또는 데이터를 정렬 하는 경우에 자동으로 SqlDataSource에서 사용 됩니다.

SqlDataSource 변경 하 여 데이터 집합 대신 DataReader를 반환 하도록 구성할 수 있습니다는 [ `DataSourceMode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx) 에서 `DataSet` (기본값)를 `DataReader`합니다. SqlDataSource의 결과 DataReader를 필요로 하는 기존 코드를 전달할 때 상황에서 DataReader를 사용 하 여을 선호 될 수 있습니다. 또한 DataReaders는 데이터 집합 보다 훨씬 단순한 개체, 이므로 더 나은 성능을 제공 합니다. 그러나, 이렇게 변경 하는 경우 데이터 웹 컨트롤도 ַ ׂ 하거나 SqlDataSource 레코드 수는 쿼리에 의해 반환 된 확인할 수 없는 하지도 않습니다 DataReader 이후 페이지에 반환된 된 데이터 정렬에 대 한 모든 기술을 제공 합니다.

## <a name="step-4-using-a-custom-sql-statement-or-stored-procedure"></a>4 단계:를 사용 하 여 사용자 지정 SQL 문 또는 저장 프로시저

SqlDataSource 컨트롤을 구성할 때 사용자 지정 SQL 문 또는 저장된 프로시저 또는 기존 테이블 또는 뷰의 열 데이터를 반환 하는 데 쿼리 두 가지 방법 중 하나에 지정할 수 있습니다. 검사 했습니다 2 단계에서에서에서 열을 선택 하 고 `Products` 테이블입니다. S 사용자 지정 SQL 문을 사용 하 여 살펴볼 수 있도록 합니다.

다른 GridView 컨트롤을 추가 `Querying.aspx` 페이지 하 고 스마트 태그에서 드롭 다운 목록에서 새 데이터 원본을 만들려면 선택 합니다. 다음으로 표시 하는 데이터를 끌어올 데이터베이스에서이 새 SqlDataSource 컨트롤을 만듭니다. 컨트롤의 이름을 `ProductsWithCategoryInfoDataSource`합니다.


![ProductsWithCategoryInfoDataSource 라는 새 SqlDataSource 컨트롤 만들기](querying-data-with-the-sqldatasource-control-vb/_static/image18.gif)

**그림 12**: 라는 새 SqlDataSource 컨트롤 만들기 `ProductsWithCategoryInfoDataSource`


다음 화면에서는 데이터베이스를 지정할 수 있습니다. 그림 7에 다시 했던 것 처럼 선택은 `NORTHWINDConnectionString` 드롭다운 목록에서 나열 하 고 다음을 클릭 합니다. Select 문 화면 구성에서 사용자 지정 SQL 문 또는 저장된 프로시저 라디오 단추 지정을 선택 하 고 클릭 합니다. 그러면 SELECT, UPDATE, INSERT 및 DELETE 레이블이 지정 된 탭을 제공 하는 사용자 지정 문 또는 저장 프로시저 정의 화면으로 표시 됩니다. 각 탭에서 상자에 붙여넣습니다는 사용자 지정 SQL 문을 입력 하거나 드롭 다운 목록에서 저장된 프로시저를 선택할 수 있습니다. 이 자습서에서는 사용자 지정 SQL 문; 입력 살펴보겠습니다. 다음 자습서는 저장된 프로시저를 사용 하는 예제를 포함 합니다.


![사용자 지정 SQL 문을 입력 하거나 저장된 프로시저를 선택 합니다.](querying-data-with-the-sqldatasource-control-vb/_static/image19.gif)

**그림 13**: 사용자 지정 SQL 문을 입력 하거나 저장된 프로시저를 선택 합니다.


사용자 지정 SQL 문 텍스트 상자에 직접 입력할 수 또는 쿼리 작성기 단추를 클릭 하 여 그래픽으로 생성할 수 있습니다. 쿼리 작성기 또는 텍스트 상자에서 반환할 다음 쿼리를 사용는 `ProductID` 및 `ProductName` 에서 필드는 `Products` 를 사용 하 여 테이블을 `JOIN` s 제품을 검색 하 `CategoryName` 에서 `Categories` 테이블:


[!code-sql[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample4.sql)]


![생성할 수 있습니다 그래픽으로 사용 하 여 쿼리는 쿼리 작성기](querying-data-with-the-sqldatasource-control-vb/_static/image20.gif)

**그림 14**: 할 수 있습니다 생성 그래픽 쿼리 작성기를 사용 하 여 쿼리


쿼리를 지정한 후 쿼리 테스트 화면으로 이동 하려면 다음을 클릭 합니다. SqlDataSource 마법사를 완료 하려면 마침을 클릭 합니다.

마법사를 완료 한 후 GridView 세 BoundFields 표시에 추가 해야 합니다는 `ProductID`, `ProductName`, 및 `CategoryName` 쿼리에서 반환 되 고 다음 선언적 태그에서 결과 열:


[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample5.aspx)]


[![GridView에서는 각 s 제품 ID, 이름 및 연결 된 범주 이름을 보여 줍니다.](querying-data-with-the-sqldatasource-control-vb/_static/image22.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image21.gif)

**그림 15**: GridView 표시 각 제품의 ID, 이름 및 연결 된 범주 이름 ([전체 크기 이미지를 보려면 클릭](querying-data-with-the-sqldatasource-control-vb/_static/image23.gif))


## <a name="summary"></a>요약

이 자습서에서는 쿼리하고 SqlDataSource 컨트롤을 사용 하 여 데이터를 표시 하는 방법에 살펴보았습니다. SqlDataSource는 ObjectDataSource를 같은 데이터에 액세스 하는 선언적 접근 방법을 제공 하는 프록시 역할을 합니다. 해당 속성에 연결 하는 데이터베이스 및 SQL 지정 `SELECT` 실행 하려면 쿼리할 속성 창을 통해 또는 데이터 소스 구성 마법사를 사용 하 여 지정할 수 있습니다.

`SELECT` 이 자습서에서는 검사 했습니다 쿼리 예제 레코드를 모두 지정 된 쿼리에서 반환 합니다. 그러나 SqlDataSource 컨트롤을 포함할 수는 `WHERE` 절 매개 변수 값을 가진 프로그래밍 방식으로 할당 되었는지 또는 지정 된 소스에서 자동으로 끌어 오지 않습니다. 만들고 다음 자습서에서 매개 변수가 있는 쿼리를 사용 하는 방법을 검토 합니다!

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [관계형 데이터베이스 데이터에 액세스](http://aspnet.4guysfromrolla.com/articles/022206-1.aspx)
- [SqlDataSource 컨트롤 개요](https://msdn.microsoft.com/library/dz12d98w.aspx)
- [ASP.NET 빠른 시작 자습서: SqlDataSource 컨트롤](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/sqldatasource.aspx)
- [Web.config `<connectionStrings>` 요소](https://msdn.microsoft.com/library/bf7sd233.aspx)
- [데이터베이스 연결 문자열 참조](http://www.connectionstrings.com/)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가 Susan Connery, 박 광 준 Leigh 및 David Suru 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](implementing-optimistic-concurrency-with-the-sqldatasource-cs.md)
> [다음](using-parameterized-queries-with-the-sqldatasource-vb.md)
