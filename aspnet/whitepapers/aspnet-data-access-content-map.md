---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET 데이터 액세스-권장 리소스 | Microsoft Docs
author: rick-anderson
description: 이 항목에서는 Entity Framework 및 SQL Se를 사용 하 여 기본적으로 ASP.NET 웹 응용 프로그램의 데이터에 액세스 하는 방법에 대 한 설명서 리소스에 대 한 링크를 제공...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/25/2013
ms.topic: article
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 16364951544dff33c9cdb8c8e330cc93de192c47
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28048261"
---
<a name="aspnet-data-access---recommended-resources"></a>ASP.NET 데이터 액세스-권장 리소스
====================
> 이 항목에서는 Entity Framework 및 SQL Server를 사용 하 여 기본적으로 ASP.NET 웹 응용 프로그램의 데이터에 액세스 하는 방법에 대 한 설명서 리소스에 대 한 링크를 제공 합니다.
> 
> 훌륭한 블로그 게시물을 알고 있는 경우 [stackoverflow](http://stackoverflow.com) 스레드나 다른 링크는 것이 유용한 [전자 메일을 보내](mailto:aspnetue@microsoft.com?subject=Data Access Content Map) 링크와 합니다.
> 
> 마지막 업데이트 4/3/2014


이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [Asp.net에서 데이터 액세스 시작](#gettingstarted)
- [Entity Framework를 사용 하 여](#ef)

    - [먼저 Entity Framework 코드를 사용 하 여](#cf)
    - [Entity Framework Code First 마이그레이션을 사용 하 여](#efcfmigrations)
    - [먼저 Entity Framework 데이터베이스를 사용 하 여 또는 모델 첫 번째 (EF 디자이너)](#efdbf)
    - [Entity Framework (지연 로드, 신속 하 게 로드 하 고 명시적으로 로드)에 있는 관련된 데이터를 로드합니다.](#efrelateddata)
    - [Entity Framework 성능 최적화](#optimizingef)
    - [Entity Framework 응용 프로그램에서 동시성 처리](#efconcurrency)
    - [Entity Framework에 대 한 설명서](#efbooks)
    - [추가 Entity Framework 리소스](#otherefresources)
- [ASP.NET 웹에서 데이터 바인딩 Forms 응용 프로그램](#wfdatabinding)

    - [모델 바인딩 Forms 웹 사용](#wfmodelbinding)
    - [데이터 소스 제어 Forms 웹 사용](#wfdsc)
    - [데이터 바인딩된 컨트롤 및 데이터 바인딩 식 Forms 웹 사용](#wfdbc)
- [SQL Server 데이터베이스 작업](#sqlserver)

    - [SQL Server Express LocalDB 데이터베이스 작업](#sslocaldb)
    - [SQL Server Express 데이터베이스 작업](#sse)
    - [Windows Azure SQL 데이터베이스 사용](#ssdb)
    - [SQL Server 및 Windows Azure SQL 데이터베이스 중에서 선택](#ssdbchoosing)
- [NoSQL 데이터베이스 관리 시스템으로 작업](#nosql)
- [LINQ 쿼리를 사용 하 여 ASP.NET 응용 프로그램](#linq)
- [동적 데이터 스 캐 폴딩을 사용](#dd)
- [데이터 액세스 보안](#securing)
- [데이터 액세스 성능 최적화](#optimizingdataaccess)
- [데이터베이스 배포](#deploying)
- [웹 서비스를 통해 데이터 액세스](#webservice)
- [추가 리소스](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>Asp.net에서 데이터 액세스 시작

- [데이터 저장소 옵션 (Windows Azure로 응용 프로그램 빌딩 실제 클라우드)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md)합니다. 클라우드에 대 한 개발에 대 한 전자책 장 합니다. 관계형 데이터베이스에 익숙한 대부분의 개발자 간과 하는 대신 NoSQL 데이터베이스를 소개 합니다. 관계형 선택할 때 고려해 야 할 사항 또는 NoSQL, 또는 특정 플랫폼에 대 한 지침을 제공 합니다.
- [ASP.NET 데이터 액세스 옵션](https://msdn.microsoft.com/library/ms178359.aspx) (MSDN). ASP.NET에 대 한 관계형 데이터베이스에 대 한 데이터 액세스 옵션와 플랫폼을 선택 하 고 사용 중인 시나리오에 적합 한 메서드에 액세스 하는 방법에 대 한 지침을 소개 합니다.
- [관계형 데이터베이스](http://en.wikipedia.org/wiki/Relational_database)합니다. Wikipedia)입니다. 관계형 데이터베이스와, 적이 없는 경우이 페이지를 관계형 데이터베이스 용어 및 개념에 대 한 소개를 참조 하십시오. SQL Server에 대 한 소개 특히 참조 [SQL Server 데이터베이스 작업](#sqlserver) 이 항목의 뒷부분에 나오는 합니다.

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>Entity Framework를 사용 하 여

- [Entity Framework 개발 방법](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf) (MSDN). Entity Framework 개발 방법 Database First Model First 또는 Code First를 선택 하는 방법에 대 한 지침입니다.

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>먼저 Entity Framework 코드를 사용 하 여
  

다음 자습서 다운로드 가능한 샘플 응용 프로그램을 제공합니다.

- [MVC 5를 사용 하 여 EF 6 시작](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다. 비동기 연결 복원 력, 명령 가로채기 등 다양 한 Entity Framework Code First 시나리오, 마이그레이션 및 EF 6를 비롯 한 기능을 다룹니다. 합니다. 이 업데이트 된 버전의는 [EF 5 / MVC 4 시리즈](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다. 이전 시리즈 리포지토리 및 새 계열에 포함 되지 않은 작업 단위 패턴에 대 한 자습서를 포함 합니다.
- [ASP.NET MVC 5 소개](../mvc/overview/getting-started/introduction/getting-started.md)합니다. 적은 엔터티 프레임 워크 코드 범위 첫 번째 시나리오에 설명 하지만의 MVC 기능을 소개 하는 더 포괄적인 유용 합니다.
- [모델 바인딩 및 Web Forms](https://go.microsoft.com/fwlink/?LinkId=286117)합니다. Web Forms 응용 프로그램에서 Code First를 사용합니다.
- [ASP.NET 4.5 Web Forms 시작](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)합니다. 소개 Web Forms 일부 검사가 포함 된 첫 번째 코드의 합니다. 사용 하 여 모델 바인딩.
- [MVC Music Store](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md)합니다. 또한 구성원 자격 및 권한 부여를 구현 하는 전자 상거래 MVC 3 응용 프로그램에서 Code First를 사용 합니다. MVC 버전과 ASP.NET 멤버 자격 (인증 및 권한 부여) 시스템 여기에가 너무 오래 되었습니다. ASP.NET 멤버 자격에 최신 정보를 참조 하십시오. [https://asp.net/identity](https://asp.net/identity)합니다.

다른 리소스:

- [Entity Framework-기존 데이터베이스에 먼저 코드](https://msdn.microsoft.com/data/jj200620)합니다. MSDN. 비디오 및 기존 데이터베이스와 함께 Code First를 사용 하는 방법을 보여 주는 연습입니다.
- [데이터 개발자 센터-Entity Framework](https://msdn.microsoft.com/data/ef)합니다. MSDN. 생성 되 고 Entity Framework 팀에서 유지 관리 하는 Entity Framework 설명서에 대 한 지침을 참조 하십시오.는 [시작](https://msdn.microsoft.com/data/ee712907) 링크 합니다.

참고 항목 [Entity Framework에 대 한 설명서](#efbooks) 및 [추가 Entity Framework 리소스](#otherefresources) 이 항목의 뒷부분에 나오는 합니다.

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>Entity Framework Code First 마이그레이션을 사용 하 여
  

대부분의 커버 마이그레이션 위에 나열 된 코드 첫 번째 자습서입니다. 다음 리소스를 참조 하십시오.

- [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)합니다. 데이터베이스를 배포 하려면 Code First 마이그레이션을 사용 하는 방법을 보여 주는 자습서 시리즈 두 부분으로 구성 합니다.
- [Windows Azure 웹 사이트에 멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET MVC 5 앱을 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. Microsoft Azure). 멤버 자격 및 응용 프로그램 데이터를 Azure에 배포할 마이그레이션을 사용 하는 방법.
- [Visual Studio 및 ASP.NET에 대 한 웹 배포 개요](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment)합니다. 참조는 **Visual Studio에서 데이터베이스 배포 구성** Code First 마이그레이션을 Visual Studio 웹 배포 기능에 통합 하는 방법에 대 한 설명은 섹션.
- [데이터 개발자 센터 Code First 마이그레이션](https://msdn.microsoft.com/data/jj591621) (MSDN). Entity Framework 팀의 마이그레이션 설명서입니다.
- [마이그레이션 동영상 가이드 시리즈](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)합니다. EF 블로그)입니다. Code First 마이그레이션을에서 고급 항목에 3 개의 비디오.
- [Code First 마이그레이션이 ASP.NET 웹 페이지 사이트와](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites)합니다. Mikesdotnetting 블로그)입니다. Visual Studio 클래스 라이브러리 프로젝트에서 데이터 컨텍스트를 배치 하 여 ASP.NET 웹 페이지 사이트와 함께 Code First 마이그레이션을 사용 하는 방법을 보여 줍니다.

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>먼저 Entity Framework 데이터베이스를 사용 하 여 또는 모델 첫 번째 (EF 디자이너)

- [Entity Framework 6 Database First MVC 5를 사용 하 여 시작](../mvc/overview/getting-started/database-first-development/setting-up-database.md)합니다. 데이터베이스를 만들려면 서버 탐색기에서 스크립트를 실행 하 고 데이터 모델을 만드는 Entity Framework 디자이너를 사용 합니다. 만드는 간단한 CRUD 웹 페이지, 방법 및 다른 데이터 처리 모든 EF 워크플로 DbContext와 동일한 API를 사용 하므로 코드 첫 번째 자습서 중 하나에 따라 수 함수에 대 한 표시 됩니다.

다음 리소스는 이전 버전입니다. Entity Framework의 버전 4.0을 사용 하 고 Web Forms 응용 프로그램의 데이터 바인딩에 대 한 데이터 소스 제어를 사용 하려는 경우 유용 합니다.

- [Entity Framework 4.0 시작](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)합니다. 사용 하는 방법을 보여 줍니다.는 **EntityDataSource** 제어 합니다.
- [Entity Framework와 함께 계속](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)(사용 하는 방법을 보여 줍니다.는 **ObjectDataSource** 제어 합니다. 동시성 처리, EF 성능에 대 한 자습서 및 EF 4.0의 새로운 기능에 대 한 자습서에 대 한 자습서에 포함 되어 있습니다.

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>처리의에서 관련 데이터 (지연 로드, 신속 하 게 로드 하 고 명시적으로 로드) Entity Framework

- [ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여 관련된 데이터를 읽는](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)합니다. Code First, MVC 샘플 응용 프로그램입니다. 표시 된 메서드는 Web Forms 모델 바인딩 및 Database First 워크플로에 적용 됩니다.
- [데이터 개발자 센터-관련된 엔터티 로드](https://msdn.microsoft.com/data/jj574232) (MSDN). 로드에 대 한 설명서는 Entity Framework 팀의 관련 데이터를 사용 합니다.

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>Entity Framework 성능 최적화

- [엔터티 프레임 워크 시나리오 ASP.NET 응용 프로그램에 대 한 고급](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)합니다. 직접 SQL 문을 실행 하거나 사용자 고유의 저장된 프로시저를 호출 하는 방법, 변경 내용 검색을 사용 하지 않도록 설정 하는 방법 및 변경 내용을 저장할 때 유효성 검사를 해제 하는 방법을 보여 줍니다.
- [Entity Framework 5에 대 한 성능 고려 사항](https://msdn.microsoft.com/data/hh949853) (MSDN).
- [성능 고려 사항 (Entity Framework)](https://msdn.microsoft.com/library/cc853327) (MSDN).
- [ASP.NET 웹 응용 프로그램에서 Entity Framework와 함께 성능 최대화](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)합니다. Entity Framework 4.0에 적용 됩니다.
- 참고 항목 [최적화 ASP.NET 데이터 액세스](#optimizingdataaccess) 이 항목의 뒷부분에 나오는 합니다.

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>Entity Framework 응용 프로그램에서 동시성 처리

- [ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여 동시성 처리](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)합니다. 코드 먼저 DbContext API를 MVC 샘플 응용 프로그램을 사용 합니다.
- [데이터 개발자 센터 – 낙관적 동시성 패턴](https://msdn.microsoft.cus/data/jj592904) (MSDN). Entity Framework 팀의 동시성 설명서입니다.
- [ASP.NET 웹 응용 프로그램에서 Entity Framework 사용 하 여 동시성 처리](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)합니다. Entity Framework 4.0에 적용 됩니다. 데이터베이스는 Web Forms 예제 응용 프로그램을 사용 하 여 ObjectContext API를 먼저 합니다.

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>Entity Framework에 대 한 설명서

- [프로그래밍 Entity Framework: DbContext](http://shop.oreilly.com/product/0636920022237.do) Julie Lerman 및 Rowan Miller 합니다.
- [프로그래밍 엔터티 프레임 워크: Code First](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman 및 Rowan Miller 합니다.

이러한도 모두 최신 버전 현재 몇 가지 권장된 기법으로 유지 합니다. 인터넷에서 사용할 수 있는 것 보다는 Entity Framework에 대 한 보다 포괄적인 아직 따라 하기 쉬운 소개를 제공합니다. 다른 책 [Entity Framework 프로그래밍](http://shop.oreilly.com/product/9780596807252.do) 으로 Julie Lerman 크고 복잡 하지만 오래 된 이며 적용 되는 기술 중 상당수는 더 이상 없으며 Entity Framework를 사용 하는 것이 좋습니다. 참고 항목에서 Entity Framework 팀에서 권장 하는 책 목록을 [데이터 개발자 센터 설명서](https://msdn.microsoft.com/data/aa937716) MSDN 사이트입니다.

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>다른 Entity Framework 리소스

- [Entity Framework (ADO.NET) 팀 블로그](https://blogs.msdn.com/b/adonet/)합니다. 최신 정보와 공지 향상 된 새로운 기능에 대 한 최상의 리소스 중 하나입니다. 다른 EF 관련 블로그 참조에서 Blogroll [Entity Framework와 함께 시작](https://msdn.microsoft.com/data/ee712907)합니다.
- [MSDN Magazine](https://msdn.microsoft.com/magazine/default.aspx)합니다. 참조는 **데이터 요소** 열은 Entity Framework와 관련 된 항목에 대 한 경우가 많습니다.

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>ASP.NET 웹에서 데이터 바인딩 Forms 응용 프로그램

- [ASP.NET Web Forms 데이터 액세스 옵션](https://msdn.microsoft.com/library/jj822927.aspx) (MSDN)<a id="wfmodelbinding"></a>합니다.

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>모델 바인딩 Forms 웹 사용

- [모델 바인딩 및 Web Forms](https://go.microsoft.com/fwlink/?LinkId=286117)합니다. EF Code First를 사용 하는 자습서 시리즈 합니다.
- [Web Forms 모델 바인딩 1 부: 데이터 선택](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx) (Scott Guthrie의 블로그). 이러한 이전 블로그 게시물에서 ItemType 라는 현재 속성의 이름이 ModelType을 하지만 그 외에 포함 된 정보 유효 합니다.
- [Web Forms 모델 바인딩 2 부: 데이터 필터링](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx) (Scott Guthrie의 블로그).
- [Web Forms 모델 바인딩 3 부: 업데이트 및 유효성 검사](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx) (Scott Guthrie의 블로그).
- [ASP.NET 4.5 Web Forms 모델 바인딩](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md)합니다. (비디오)입니다.
- [바인딩 파트 1-을 선택 하면 데이터 모델링](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md) (비디오).
- [모델 바인딩 파트 2-필터링](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md) (비디오).
- [가져오는 데이터를 표시 ASP.NET 4.5 Web Forms-시작 항목 및 세부 사항](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)합니다.

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>데이터 소스 제어 Forms 웹 사용

- [데이터 소스 웹 서버 컨트롤](https://msdn.microsoft.com/library/ms247258.aspx) (MSDN).
- [Entity Framework 6에 대 한 동적 데이터 공급자 및 EntityDataSource 컨트롤의 릴리스를 발표](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx) (Microsoft 웹 개발 블로그).

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>데이터 바인딩된 컨트롤 및 데이터 바인딩 식 Forms 웹 사용

- [모델 바인딩 및 Web Forms](https://go.microsoft.com/fwlink/?LinkId=286117)합니다. EF Code First를 사용 하는 자습서 시리즈
- [가져오는 데이터를 표시 ASP.NET 4.5 Web Forms-시작 항목 및 세부 사항](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)합니다.
- [데이터 컨트롤 강력한 형식의](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx) (Scott Guthrie의 블로그).
- [데이터 컨트롤 강력한 형식의](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (비디오).
- [ASP.NET 4.5 Web Forms 강력한 형식의 데이터 컨트롤](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (비디오).
- [데이터 바인딩된 컨트롤을 웹 서버 컨트롤](https://msdn.microsoft.com/library/ms228214.aspx) (MSDN).
- [데이터 바인딩 식 개요](https://msdn.microsoft.com/library/ms178366.aspx) (MSDN). 이 페이지를 포함 **Eval** 및 **바인딩할**; 포함 하도록 업데이트 되지 않은 **항목** 및 **BindItem**합니다.

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>SQL Server 데이터베이스 작업

- [SQL Server 데이터베이스 기능](https://msdn.microsoft.com/library/hh230827.aspx) (MSDN). 다양 한 SQL Server 항목에 대 한 일반 소개, 목차에서 아래 항목을 참조 하세요.
- [SQL Server 버전](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver) (MSDN). 요약에 각각에 대 한 자세한 정보 링크를 사용할 수 있는 SQL Server 버전의.)
- [ASP.NET 웹 응용 프로그램에 대 한 SQL Server 연결 문자열](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램에 대 한](https://msdn.microsoft.com/library/ms247257.aspx) (MSDN).
- [Microsoft SQL Server: 데이터베이스 제품 예제](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)합니다. 샘플 AdventureWorks 데이터베이스입니다.
- [예제 데이터베이스 설치](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)합니다. 여기에 표시 된 메서드 외에도 다운로드할 수도 있습니다 예제.mdf 파일 중 하나는 응용 프로그램에\_웹 프로젝트의 데이터 폴더, LocalDB에 데이터베이스를 변환 하 고 LocalDB 연결 문자열을 만듭니다. 작업을 수행 하는 방법에 대 한 정보를 참조 하십시오. [하는 방법: LocalDB로 업그레이드](https://msdn.microsoft.com/library/hh873188.aspx)합니다.

다음 섹션에서는 SQL Server 및 SQL 데이터베이스 중에서 선택 하 고 SQL Server Express LocalDB와 작업에 참조 합니다.

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>SQL Server Express LocalDB 데이터베이스 작업

- [SQL Server Express 2012 LocalDB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) (MSDN). LocalDB에 공식 MSDN 소개 합니다.
- [ASP.NET 웹 응용 프로그램에 대 한 SQL Server 연결 문자열](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [방법: LocalDB로 업그레이드](https://msdn.microsoft.com/library/hh873188.aspx) (MSDN). LocalDB에 이전 버전의 SQL Server Express.mdf 파일을 마이그레이션하는 방법입니다. 중 하나를 다운로드 하는 경우에이 프로세스를 진행할 수 있습니다는 [SQL Server 2012 예제 데이터베이스](https://go.microsoft.com/fwlink/?linkid=117483)합니다.
- [향상 된 SQL Express LocalDB 소개](https://go.microsoft.com/fwlink/?LinkId=234375) (SQL Server Express 블로그). MSDN에 포함 된 보다 LocalDB 만들어진 이유를 자세한 배경을 알고 싶으면을 있습니다.
- [LocalDB: 내 데이터베이스는 어디 입니까?](https://go.microsoft.com/fwlink/?LinkId=234376) (SQL Server Express 블로그)입니다. LocalDB 데이터베이스 파일 생성 되는 위치에 대 한 정보입니다.
- [LocalDB를 사용 하 여 전체 iis에서 1 부: 사용자 프로필](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx) (SQL Server Express 블로그). LocalDB가 IIS와 함께 작동 하도록 설계 되지 않았습니다. 이 일련의 블로그 게시물 문제 및 해결을 설명합니다.

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>SQL Server Express 데이터베이스 작업

- [ASP.NET 웹 응용 프로그램에 대 한 SQL Server 연결 문자열](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN). AttachDBFileName 연결 문자열 설정을 SQL Server express를 사용 하면 특히이 페이지의 사용자 인스턴스 섹션을 참조 합니다.
- [사용자 로컬 SQL Server Express 2008의 소유권을 가져오는 방법](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx) (SQL Server Express 블로그). 일반적인 문제는 SQL Server Express 인스턴스의 관리자 모르겠으면 때문에 SQL Server Express 데이터베이스에서 작동할 수 되 고 있지 않습니다. 기본적으로 SQL Server Express를 설치한 사용자만 관리자 이지만, 이 블로그 하는 방법을 사용자가 직접 SQL Server Express 관리자 컴퓨터에서 관리자 인 경우에 대해 설명 합니다.
- [내 ASP.NET 웹 응용 프로그램 프로덕션 환경에서 SQL Server Express 데이터베이스를 사용할 수 있습니까?](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN)입니다.

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>Windows Azure SQL 데이터베이스 사용

- [Windows Azure 웹 사이트 멤버 자격, OAuth, SQL 데이터베이스와 Secure ASP.NET MVC 응용 프로그램 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) (Microsoft Azure 사이트).
- [SQL 데이터베이스](https://docs.microsoft.com/azure/sql-database/) (Microsoft Azure 사이트). 시작된 자습서 및 방법 가이드를 가져오는 중입니다.
- [Windows Azure SQL 데이터베이스](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx) (MSDN). MSDN의 SQL 데이터베이스에 대 한 목차의 최상위 노드.
- [Windows Azure SQL 데이터베이스 TechNet Wiki 문서 인덱스](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx) (Microsoft TechNet 사이트).
- [일시적인 오류 처리 응용 프로그램 블록](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx)합니다. 수 있는 일시적인 네트워크 오류와 연결 오류 처리 제한에서 해당 결과 프레임 워크입니다. NuGet 패키지에서 사용할 수 있는: [Enterprise Library 5.0-일시적인 오류 처리 응용 프로그램 블록](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling)합니다.
- [SQL 데이터베이스 및 Entity Framework 시작](https://msdn.microsoft.com/data/jj556244) (MSDN).
- [Windows Azure 트레이닝 키트](https://www.microsoft.com/download/details.aspx?id=8396) (Microsoft 다운로드 센터). SQL 데이터베이스에 대 한 실습 랩을 포함합니다.
- [Windows Azure SQL 데이터베이스 커뮤니티 포럼](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads)합니다.
- [Windows Azure SQL 데이터베이스를 이동](https://msdn.microsoft.com/library/ff803375.aspx) (MSDN). Microsoft Patterns and Practices 팀에서 포괄적인 종단 간 시나리오의 한 장 합니다. 마이그레이션하는 이유 표지와 SQL 데이터베이스에 SQL Server에서 마이그레이션하는 방법입니다.
- [Windows Azure SQL 데이터베이스로 SQL Server 데이터베이스 마이그레이션](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN).
- [SQL 데이터베이스 마이그레이션 마법사](http://sqlazuremw.codeplex.com/)합니다. 마이그레이션에 대 한 오픈 소스 도구와 SQL 데이터베이스의 데이터베이스합니다.

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>SQL Server 및 Windows Azure SQL 데이터베이스 중에서 선택

- [Windows Azure SQL 데이터베이스와 SQL Server 비교](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) (Microsoft TechNet 사이트).
- [Windows Azure SQL 데이터베이스로 데이터 마이그레이션: 도구와 기술을](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx) (MSDN). SQL 데이터베이스에 SQL Server를 비교 하 고 SQL 데이터베이스에 SQL Server에서 마이그레이션하는 경우에 대 한 지침을 제공 하는 섹션이 포함 됩니다.
- [Windows Azure SQL 데이터베이스 배달 가이드](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx) (Microsoft TechNet 사이트).
- [SQL Server 기능 제한 (Windows Azure SQL 데이터베이스)](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) (MSDN).
- [Windows Azure 테이블 저장소 및 Windows Azure SQL 데이터베이스-비교 및 대조](https://msdn.microsoft.com/library/jj553018.aspx) (MSDN). Windows Azure에 배포 하는 응용 프로그램에 대 한 Windows Azure 테이블 저장소는 Windows Azure SQL 데이터베이스에 대 한 대안을 수 있습니다. 이 항목에는 이러한 대체 방법 중에서 결정할 수 있습니다.
- [Windows Azure SQL 데이터베이스](https://msdn.microsoft.com/library/windowsazure/ee336279) (MSDN).
- [지침 및 제한 사항 (Windows Azure SQL 데이터베이스)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>NoSQL 데이터베이스 관리 시스템으로 작업

- [Windows Azure 데이터 서비스](https://www.windowsazure.com/develop/net/data/) (Microsoft Azure 사이트). 참조는 [테이블 서비스 기능 가이드](https://docs.microsoft.com/azure/) 및 **빅 데이터** 페이지의 섹션입니다.
- [ASP.NET 다중 계층 응용 프로그램 사용 하 여 저장소 테이블, 큐 및 Blob](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) (Microsoft Azure 사이트). Windows Azure 저장소 NoSQL 테이블을 사용 하는 다운로드 가능한 샘플 응용 프로그램과 종단 간 자습서입니다.

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>LINQ 쿼리를 사용 하 여 ASP.NET 응용 프로그램

- [ASP.NET 데이터 액세스 옵션](https://msdn.microsoft.com/library/ms178359.aspx#linq) (MSDN). LINQ 소개에 포함 되어 있습니다.
- [LINQ 학습 비디오](http://www.misfitgeek.com/windows-client-linq-training-videos-20/) (Joe Stagner 블로그).
- [동적 LINQ 리소스 링크를 ASP.NET 포럼 스레드](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq)합니다.

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>동적 데이터 스 캐 폴딩을 사용

- [동적 데이터 프로젝트 템플릿](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata) (MSDN). 동적 데이터 프로젝트를 사용 하는 경우에 대 한 지침입니다.
- [ASP.NET Dynamic Data](https://msdn.microsoft.com/library/ee845452.aspx) (MSDN).

<a id="securing"></a>

## <a name="securing-data-access"></a>데이터 액세스 보안

- [ASP.NET 데이터 액세스 보안](https://msdn.microsoft.com/library/ms178375.aspx) (MSDN).
- [보안 고려 사항 (Entity Framework)](https://msdn.microsoft.com/library/cc716760.aspx) (MSDN).
- [방법: 데이터 소스 제어를 사용 하는 경우 연결 문자열을 보호](https://msdn.microsoft.com/library/ms178372.aspx) (MSDN).

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>데이터 액세스 성능 최적화

- [ASP.NET 성능 개요](https://msdn.microsoft.com/library/cc668225.aspx) (MSDN).
- [ASP.NET 캐싱](https://msdn.microsoft.com/library/xsbfdd8c.aspx) (MSDN).
- [ASP.NET 성능 향상](https://msdn.microsoft.com/library/ff647787) (MSDN). 이 페이지 맨 위에 있는 "콘텐츠 사용 되지 않음" 경고 하지만 대부분의 정보는도 적용 되며 업데이트 된 리소스가 없으면 비교할 수 있습니다.
- [SQL Server 성능 향상](https://msdn.microsoft.com/library/ff647793) (MSDN). 이전 링크와 같은 설명 합니다.

참고 항목 [최적화 Entity Framework 성능](#optimizingef) 이 항목의에서 앞부분입니다.

<a id="deploying"></a>

## <a name="deploying-a-database"></a>데이터베이스 배포

- [ASP.NET 웹 배포-권장 리소스](aspnet-web-deployment-content-map.md) (MSDN).

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>웹 서비스를 통해 데이터 액세스

- [웹 서비스를 통해 데이터 액세스](https://msdn.microsoft.com/library/ms178359.aspx#webservice) (MSDN). WCF 또는 웹 API를 사용 하는 경우에 대 한 지침입니다.
- [ASP.NET Web API 시작](../web-api/index.md)합니다.
- [WCF Data Services](https://msdn.microsoft.com/data/bb931106) (MSDN).

<a id="additional"></a>

## <a name="additional-resources"></a>추가 리소스

- [ASP.NET 데이터 액세스 FAQ](https://msdn.microsoft.com/library/jj653753.aspx) (MSDN).
- [ASP.NET Web Forms 자습서-데이터](../web-forms/overview/data-access/index.md)합니다. 이 자습서의 대부분은 상대적으로 이전; 읽어보십시오 [ASP.NET 데이터 액세스 옵션](https://msdn.microsoft.com/library/ms178359.aspx) 및 [데이터 저장소 옵션 (실제 클라우드로 응용 프로그램 빌딩 Windows Azure)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) 첫 번째 오른쪽 없는 데이터 액세스 방법에 너무 큰를 얻지 있도록 시나리오입니다.
- [ASP.NET MVC 콘텐츠 맵](../mvc/overview/getting-started/recommended-resources-for-mvc.md)합니다.
- [ASP.NET 웹 페이지 자습서-데이터](../web-pages/overview/data/index.md)합니다.
- [Visual Studio에서 데이터 액세스](https://msdn.microsoft.com/library/wzabh8c4.aspx) (MSDN). 새 링크 목록을 제공이 콘텐츠 맵은 있지만 ASP.NET 보다는 Visual Studio에 중점을 두고 있습니다.
