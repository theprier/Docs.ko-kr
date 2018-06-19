---
uid: web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-vb
title: SQL 캐시 종속성 (VB)를 사용 하 여 | Microsoft Docs
author: rick-anderson
description: 가장 간단한 캐싱 전략 지정 된 기간 후에 만료 되도록 캐시 된 데이터입니다. 하지만이 간단한 방법은 즉 캐시 된 데이터 maintai...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/30/2007
ms.topic: article
ms.assetid: bd347d93-4251-4532-801c-a36f2dfa7f96
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-vb
msc.type: authoredcontent
ms.openlocfilehash: 452d856fe352ef2eb7dfcc3f3acd6aa5bcb5ae41
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30878375"
---
<a name="using-sql-cache-dependencies-vb"></a>SQL 캐시 종속성 (VB)를 사용 하 여
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_61_VB.zip) 또는 [PDF 다운로드](using-sql-cache-dependencies-vb/_static/datatutorial61vb1.pdf)

> 가장 간단한 캐싱 전략 지정 된 기간 후에 만료 되도록 캐시 된 데이터입니다. 하지만이 간단한 방법은 캐시 된 데이터 부실 데이터를 너무 길게 유지 되 나 현재 데이터를 너무 일찍 만료 생성은 내부 데이터 소스의 유지 함을 의미 합니다. 데이터 원본 데이터에 SQL 데이터베이스에서 수정한 때까지 캐시 된 남아 있도록 SqlCacheDependency 클래스를 사용 하는 것이 좋습니다. 이 자습서에서는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

캐싱 기술을 검사는 [는 ObjectDataSource 사용 하 여 데이터 캐싱을](caching-data-with-the-objectdatasource-vb.md) 및 [아키텍처에서 데이터 캐싱](caching-data-in-the-architecture-vb.md) 지정 된 후 캐시에서 데이터를 제거 하도록 시간 기반 만료를 사용 하는 자습서 기간입니다. 이 방법은 캐싱을 부실 데이터에 대 한 성능 향상 균형을 조정 하는 가장 간단한 방법은 설명 합니다. 시간 만료를 선택 하 여 *x* 시간 (초), 페이지 개발자 concedes에 대 한 캐싱 전용의 성능 이점을 *x* 초, 하지만 쉽게 재설정할 수 그녀의 데이터가 될 것 이라는 되지 부실는 최대 길이 보다 더 이상 *x* 초입니다. 물론, 정적 데이터에 대 한 *x* 에서 검사 된 대로 웹 응용 프로그램의 수명에 확장할 수는 [응용 프로그램 시작 시 데이터 캐싱](caching-data-at-application-startup-vb.md) 자습서입니다.

데이터베이스 데이터 캐싱, 시간 기반 만료 종종 해당 사용 편의성을 위해 선택한 되지만 자주 부적절 한 솔루션입니다. 이상적으로 데이터베이스 데이터는 데이터베이스;에서 내부 데이터가 수정 될 때까지 캐시 된 유지 만 후 캐시를 제거 합니다. 이 방법은 캐싱의 성능 이점을 극대화 하 고 오래 된 데이터의 기간을 최소화 합니다. 그러나 다음과 같은이 이점을 활용 하려면 기본 데이터베이스 데이터 수정 되었습니다 하 고 캐시에서 해당 항목을 제거 하는 경우 알 수 있는 일부 시스템 되어야 합니다. ASP.NET 2.0 이전 페이지 개발자가이 시스템을 구현 해야 했습니다.

ASP.NET 2.0에서는 제공 된 [ `SqlCacheDependency` 클래스](https://msdn.microsoft.com/library/system.web.caching.sqlcachedependency.aspx) 및 캐시 된 항목을 해당 하는 데이터베이스에서 변경이 발생 했을 때 결정 하는 데 필요한 인프라를 제거할 수 있습니다. 기본 데이터가 변경 되었을 때 확인 하기 위한 두 가지 방법이: 알림 및 폴링 합니다. 알림 및 폴링 간의 차이점에 논의 후 만들겠습니다 인프라 폴링을 지원 한 다음 사용 하는 방법을 탐색 하는 데 필요한는 `SqlCacheDependency` 선언에서 클래스 및 프로그래밍 방식으로 시나리오입니다.

## <a name="understanding-notification-and-polling"></a>이해 알림 및 폴링

데이터베이스의 데이터 수정 되었는지 시기를 확인 하는 데 사용할 수 있는 두 가지 방법이: 알림 및 폴링 합니다. 알림을 사용 하 여 쿼리가 마지막 실행 이후 변경 했을 특정 쿼리 결과를 할 때 자동으로 ASP.NET 런타임이 경고 데이터베이스, 이때 쿼리에 연결 된 캐시 된 항목 보다 먼저 삭제 됩니다. 데이터베이스 서버, 폴링을 통해 때 특정 테이블이 마지막으로 업데이트 된에 대 한 정보를 유지 합니다. ASP.NET 런타임 테이블이 변경 내용을 확인 하려면 데이터베이스를 주기적으로 폴링하여 캐시에 입력 된 이후입니다. 해당 데이터가 수정 된 포함가 연결 된 캐시 항목을 제거 합니다.

알림 옵션 폴링 보다 적은 설정이 필요 하며 테이블 수준에서가 아니라 쿼리 수준에서 변경 내용을 추적 하므로 보다 세부적인 있습니다. 그러나 알림은 Microsoft SQL Server 2005 (즉, Express 이외의 버전)의 전체 버전에서 사용할 수 있습니다. 그러나 7.0의 Microsoft SQL Server 2005로의 모든 버전에 대 한 폴링 옵션을 사용할 수 있습니다. SQL Server 2005 Express edition을 사용 하는이 자습서의 설정 및 폴링 옵션을 사용 하 여 살펴볼 것입니다. SQL Server 2005의 알림 기능에 추가 리소스에 대 한이 자습서의 끝에 추가 읽기 섹션을 참조 하십시오.

폴링을 통해 데이터베이스 라는 테이블을 포함 하도록 구성 해야 `AspNet_SqlCacheTablesForChangeNotification` 세 개의 열이 있는 `tableName`, `notificationCreated`, 및 `changeId`합니다. 이 테이블에는 웹 응용 프로그램에서 SQL 캐시 종속성에 사용할 수 해야 할 수 있는 데이터가 있는 각 테이블에 대 한 행을 포함 합니다. `tableName` 열 하는 동안 테이블의 이름을 지정 `notificationCreated` 테이블에 행이 추가 시간과 날짜를 나타냅니다. `changeId` 형식의 열이 `int` 와 초기 값은 0입니다. 해당 값으로 테이블을 수정할 때마다 증가 합니다.

이외에 `AspNet_SqlCacheTablesForChangeNotification` 테이블, 데이터베이스에서는 SQL 캐시 종속성에 나타날 수 있는 테이블의 각 트리거를 포함 합니다. 이 트리거는 행 삽입, 업데이트 또는 삭제 될 때마다 실행 되 고 s 테이블 증가 `changeId` 값 `AspNet_SqlCacheTablesForChangeNotification`합니다.

ASP.NET 런타임 추적 현재 `changeId` 사용 하 여 데이터를 캐시할 때 테이블에 대 한는 `SqlCacheDependency` 개체입니다. 데이터베이스를 정기적으로 검사 하는 임의의 `SqlCacheDependency` 개체 `changeId` 데이터베이스의 값에서 다른는 다른 이후 제거 되는 `changeId` 발생 하는 테이블에 대 한 변경 데이터가 캐시 된 이후 값을 나타냅니다.

## <a name="step-1-exploring-theaspnetregsqlexecommand-line-program"></a>1 단계: 탐색는`aspnet_regsql.exe`명령줄 프로그램

폴링 접근 방식으로 데이터베이스에는 위에서 설명한 인프라를 포함 하도록 설정 되어 있어야: 미리 정의 된 테이블 (`AspNet_SqlCacheTablesForChangeNotification`), 저장된 프로시저 및 기본 테이블의 각 웹의 SQL 캐시 종속성에 사용할 수 있는 테이블의 트리거는 소수의 응용 프로그램입니다. 명령줄 프로그램을 통해 이러한 테이블, 저장된 프로시저 및 트리거를 만들 수 있습니다 `aspnet_regsql.exe`에 있는 `$WINDOWS$\Microsoft.NET\Framework\version` 폴더입니다. 만들려는 `AspNet_SqlCacheTablesForChangeNotification` 테이블과 명령줄에서 다음을 실행 하는 연결 된 저장된 프로시저:


[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample1.cmd)]

> [!NOTE]
> 지정 된 데이터베이스 로그인에 있어야 합니다. 이러한 명령을 실행 하는 [ `db_securityadmin` ](https://msdn.microsoft.com/library/ms188685.aspx) 및 [ `db_ddladmin` ](https://msdn.microsoft.com/library/ms190667.aspx) 역할입니다. 검사 하 여 데이터베이스에 전송 하는 T-SQL은 `aspnet_regsql.exe` 줄 프로그램 명령에서 참조 [이 블로그 항목](http://scottonwriting.net/sowblog/posts/10709.aspx)합니다.


예를 들어 라는 폴링에 대 한 인프라는 Microsoft SQL Server 데이터베이스를 추가 하려면 `pubs` 이라는 데이터베이스 서버에 `ScottsServer` Windows 인증을 사용 하 고 해당 디렉터리 이동한, 명령줄에서 다음을 입력 합니다.


[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample2.cmd)]

데이터베이스 수준 인프라를 추가한 후 SQL 캐시 종속성에 사용할 수 있는 이러한 테이블에 트리거를 추가 해야 합니다. 사용 하 여는 `aspnet_regsql.exe` 명령줄 프로그램을 다시, 하지만 사용 하 여 테이블 이름을 지정는 `-t` 전환 하 고 사용 하는 대신는 `-ed` 사용 전환 `-et`, 같이:


[!code-html[Main](using-sql-cache-dependencies-vb/samples/sample3.html)]

트리거를 추가 하는 `authors` 및 `titles` 테이블에 `pubs` 데이터베이스에 `ScottsServer`를 사용 하 여:


[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample4.cmd)]

이 자습서에 대 한 추가 트리거를 트리거는 `Products`, `Categories`, 및 `Suppliers` 테이블입니다. 3 단계에서에서 특정 명령줄 구문 살펴보겠습니다.

## <a name="step-2-referencing-a-microsoft-sql-server-2005-express-edition-database-inappdata"></a>2 단계: 참조에서 Microsoft SQL Server 2005 Express Edition 데이터베이스`App_Data`

`aspnet_regsql.exe` 명령줄 프로그램 필요한 폴링 인프라를 추가 하려면 데이터베이스 및 서버 이름을 입력 해야 합니다. 에 있는 Microsoft SQL Server 2005 Express 데이터베이스에 대 한 데이터베이스 및 서버 이름을 하지만 `App_Data` 폴더? 데이터베이스 및 서버 이름이 이란를 검색 하는 것이 아니라 I 했습니다 않음을 발견 가장 간단한 방법은 데이터베이스를 연결 하는 `localhost\SQLExpress` 데이터베이스 인스턴스 및 사용 하 여 데이터의 이름을 바꿀 [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)합니다. 컴퓨터에 설치 된 SQL Server 2005의 전체 버전 중 하나를 해야 하는 경우 다음 가능성이 이미 컴퓨터에 설치 된 SQL Server Management Studio 합니다. Express edition만 있는 경우 무료 다운로드할 수 [Microsoft SQL Server Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)합니다.

Visual Studio를 닫고 시작 합니다. 다음으로, SQL Server Management Studio를 연에 연결 하도록 선택 된 `localhost\SQLExpress` Windows 인증을 사용 하 여 서버입니다.


![Localhost\SQLExpress 서버에 연결](using-sql-cache-dependencies-vb/_static/image1.gif)

**그림 1**:에 연결 된 `localhost\SQLExpress` 서버


Management Studio에는 서버를 연결한 후 서버 나타나며이 데이터베이스, 보안 등에 대 한 하위 폴더. 데이터베이스 폴더 단추로 클릭 하 고 연결 옵션을 선택 합니다. 나타납니다 데이터베이스 연결 대화 상자 (그림 2 참조). 추가 단추를 클릭 하 고 선택 된 `NORTHWND.MDF` 웹 응용 프로그램 s에 데이터베이스 폴더 `App_Data` 폴더입니다.


[![NORTHWND를 연결 합니다. App_Data 폴더에서 MDF 데이터베이스](using-sql-cache-dependencies-vb/_static/image2.gif)](using-sql-cache-dependencies-vb/_static/image1.png)

**그림 2**: 연결에서 `NORTHWND.MDF` 에서 데이터베이스는 `App_Data` 폴더 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-vb/_static/image2.png))


이렇게 하면 데이터베이스에서 데이터베이스 폴더에 추가 됩니다. 데이터베이스 이름이 데이터베이스 파일에 전체 경로 되었거나 붙습니다. 전체 경로 [GUID](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)합니다. Aspnet를 사용 하는 경우이 긴 데이터베이스 이름을 입력 하지 않으려면\_regsql.exe 명령줄 도구, 마우스 오른쪽 단추로 클릭 데이터베이스에서 방금 사람이 더 친숙 한 이름으로 데이터베이스는 연결 이름 바꾸기 및 선택의 이름을 변경 합니다. I DataTutorials 내 데이터베이스로 변경 했습니다.


![사람이 더 친숙 한 이름으로 연결된 되는 데이터베이스 이름 바꾸기](using-sql-cache-dependencies-vb/_static/image3.gif)

**그림 3**: 사람이 더 친숙 한 이름으로 연결된 되는 데이터베이스 이름 바꾸기


## <a name="step-3-adding-the-polling-infrastructure-to-the-northwind-database"></a>Northwind 데이터베이스에는 폴링 인프라를 추가 하는 3 단계:

첨부 한 म 했으므로 `NORTHWND.MDF` 에서 데이터베이스는 `App_Data` 폴더 폴링 인프라를 추가 하려면 준비 된 것입니다. 적 DataTutorials에 데이터베이스 이름이 바뀌었거나, 있다고 가정할 경우 다음 4 개 명령은 실행 합니다.


[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample5.cmd)]

이러한 4 개 명령은 실행 한 후 Management Studio에서 데이터베이스 이름을 마우스 오른쪽 단추로 클릭 작업 하위 메뉴도 이동한 후 분리를 선택 합니다. 그런 다음 Management Studio를 닫습니다 하 고 Visual Studio를 다시 여세요.

Visual Studio가 다시 후 서버 탐색기를 통해 데이터베이스에 드릴 합니다. 새 테이블을 확인 (`AspNet_SqlCacheTablesForChangeNotification`), 새에 저장 된 프로시저 및 트리거는 `Products`, `Categories`, 및 `Suppliers` 테이블입니다.


![이제는 데이터베이스에 필요한 폴링 인프라를 포함 됩니다.](using-sql-cache-dependencies-vb/_static/image4.gif)

**그림 4**: 이제는 데이터베이스에 필요한 폴링 인프라 포함 됩니다


## <a name="step-4-configuring-the-polling-service"></a>폴링 서비스를 구성 하는 4 단계:

필요한 테이블, 트리거 및 저장된 프로시저에서 데이터베이스를 만든 후 마지막 단계를 통해 이루어집니다 폴링 서비스를 구성 하는 `Web.config` 데이터베이스 사용 및 폴링 빈도를 밀리초 단위로 지정 하 여 합니다. 다음 태그는 매 초 마다 Northwind 데이터베이스를 폴링합니다.


[!code-xml[Main](using-sql-cache-dependencies-vb/samples/sample6.xml)]

`name` 값에 `<add>` 요소 (NorthwindDB) 이해 하기 쉬운 이름을 특정 데이터베이스와 연결 합니다. SQL 캐시 종속성을 사용할 때 캐시 된 데이터는 기반으로 하는 테이블 뿐만 아니라 여기에 정의 된 데이터베이스 이름을 참조 하도록 해야 합니다. 사용 하는 방법을 살펴보려는 `SqlCacheDependency` 와 SQL 캐시 종속성을 프로그래밍 방식으로 연결 하는 데 6 단계에서에서 데이터를 캐시 합니다.

폴링 시스템에 정의 된 데이터베이스에 연결 되는 SQL 캐시 종속성, 설정 되 면는 `<databases>` 요소 모든 `pollTime` 시간 (밀리초)을 실행 하 고는 `AspNet_SqlCachePollingStoredProcedure` 저장 프로시저. 추가 된이 저장된 프로시저를 사용 하 여 3 단계에서 다시는 `aspnet_regsql.exe` 명령줄 도구-반환 된 `tableName` 및 `changeId` 의 각 레코드에 대 한 값 `AspNet_SqlCacheTablesForChangeNotification`합니다. SQL 캐시 종속성을 오래 된 캐시에서 제거 됩니다.

`pollTime` 설정은 성능 및 데이터 부실 간의 균형을 소개 합니다. 작은 `pollTime` 값에는 데이터베이스에 대 한 요청 수가 증가 하지만 더 신속 하 게 캐시에서 오래 된 데이터를 제거 합니다. 더 큰 `pollTime` 값 데이터베이스 요청 수를 줄일 수 있지만 백 엔드 데이터가 변경 될 때 및 관련된 캐시 항목이 제거 되는 시간 사이의 지연이 증가 합니다. 다행히는 데이터베이스 요청이 실행 하 고 간단한 저장된 프로시저를 s 작고 간단한 테이블에서 몇 개의 행을 반환 합니다. 다른 테스트 수행 하지만 `pollTime` 값 이상적인 균형점을 찾아야을 데이터베이스 응용 프로그램에 대 한 액세스 및 데이터 부실 합니다. 가장 작은 `pollTime` 허용 된 값은 500입니다.

> [!NOTE]
> 위의 예제에서는 단일 제공 `pollTime` 값는 `<sqlCacheDependency>` 있지만 요소를 선택적으로 지정할 수는 `pollTime` 값에 `<add>` 요소입니다. 지정 된 데이터베이스가 여러 개 있 및 데이터베이스당 폴링 빈도 사용자 지정 하려는 경우에 유용 합니다.


## <a name="step-5-declaratively-working-with-sql-cache-dependencies"></a>5 단계: SQL 캐시 종속성 선언적으로 사용

1 ~ 4 단계에서에서 필요한 데이터베이스 인프라를 설정 하 고 폴링 시스템을 구성 하는 방법을 찾았습니다. 위치에이 인프라를 프로그래밍 방식으로 또는 선언적 기술을 사용 하 여 연결 된 SQL 캐시 종속성으로 데이터 캐시를 항목을 이제 추가할 수 있습니다. 이 단계에서는 SQL 캐시 종속성을 선언적으로 사용 하는 방법을 검토 합니다. 6 단계 프로그래밍 방식을 살펴보겠습니다.

[는 ObjectDataSource 사용 하 여 데이터 캐싱을](caching-data-with-the-objectdatasource-vb.md) 자습서는 ObjectDataSource의 선언적 캐싱 기능을 탐색 합니다. 설정 하면는 `EnableCaching` 속성을 `True` 및 `CacheDuration` 속성을 몇 시간 간격으로는 ObjectDataSource 지정된 된 간격에 대 한 해당 내부 개체에서 반환 된 데이터를 캐시 자동으로 됩니다. ObjectDataSource는 하나 이상의 SQL 캐시 종속성 사용할 수도 있습니다.

SQL 캐시 종속성을 선언적으로 사용 하 여 작업을 보여 주기 위해 열고는 `SqlCacheDependencies.aspx` 페이지에 `Caching` 폴더와 디자이너 도구 상자에서 끌어서는 GridView입니다. GridView s 설정 `ID` 를 `ProductsDeclarative` 하 고 스마트 태그를 라는 새 ObjectDataSource 바인딩할 선택 `ProductsDataSourceDeclarative`합니다.


[![ProductsDataSourceDeclarative 라는 새 ObjectDataSource 만들기](using-sql-cache-dependencies-vb/_static/image5.gif)](using-sql-cache-dependencies-vb/_static/image3.png)

**그림 5**: 명명 된 새 ObjectDataSource 만드는 `ProductsDataSourceDeclarative` ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-vb/_static/image4.png))


ObjectDataSource 사용 하도록 구성 된 `ProductsBLL` 클래스 및 드롭 다운 목록에 선택 탭에서 설정할 `GetProducts()`합니다. 업데이트 탭에서 선택 된 `UpdateProduct` 세 개의 입력된 매개 변수-오버 로드 `productName`, `unitPrice`, 및 `productID`합니다. INSERT 및 DELETE 탭에 있는 드롭 다운 목록을를 (없음)을 설정 합니다.


[![세 개의 입력된 매개 변수가 있는 UpdateProduct 오버 로드를 사용 합니다.](using-sql-cache-dependencies-vb/_static/image6.gif)](using-sql-cache-dependencies-vb/_static/image5.png)

**그림 6**: 세 개의 입력 매개 변수가 있는 UpdateProduct 오버 로드를 사용 하 여 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-vb/_static/image6.png))


[![INSERT 및 DELETE 탭에 대 한 드롭다운 목록 (없음)으로 설정](using-sql-cache-dependencies-vb/_static/image7.gif)](using-sql-cache-dependencies-vb/_static/image7.png)

**그림 7**: (None) 드롭 다운 목록을 삽입 및 삭제 탭에 대 한 설정 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-vb/_static/image8.png))


데이터 소스 구성 마법사를 완료 한 후 Visual Studio는 만듭니다 BoundFields 및 CheckBoxFields GridView에서 각 데이터 필드에 대 한 합니다. 모든 필드를 제거 하지만 `ProductName`, `CategoryName`, 및 `UnitPrice`, 나타나며이 필드의 서식을 지정 하 고 있습니다. GridView s 스마트 태그에서의 페이징 사용, 사용 하도록 설정 및 편집 사용 확인란을 선택 합니다. Visual Studio는 ObjectDataSource s 설정 `OldValuesParameterFormatString` 속성을 `original_{0}`합니다. 이 속성 선언적 구문 또는 해당 기본값으로 다시 설정에서 완전히 제거 하거나 제대로 작동 하려면 GridView의 편집 기능에 대 한 순서로 `{0}`합니다.

마지막으로, 위에 집합과 GridView Label 웹 컨트롤을 추가 해당 `ID` 속성을 `ODSEvents` 및 해당 `EnableViewState` 속성을 `False`합니다. 다음과 같이 변경한 후 페이지 s 선언적 태그 다음과 비슷해야 합니다. 참고를 했습니다의 미적인 사용자 지정 SQL 캐시 종속성 기능을 설명 하기 위해 필요 하지 않은 GridView 필드에 적용 합니다.


[!code-aspx[Main](using-sql-cache-dependencies-vb/samples/sample7.aspx)]

다음으로, ObjectDataSource s에 대 한 이벤트 처리기를 만들고 `Selecting` 이벤트에 다음 코드를 추가 합니다.


[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample8.vb)]

이전에 설명한 대로 ObjectDataSource의 `Selecting` 개체는 기본 개체 로부터 데이터를 검색 하는 경우에이 이벤트가 발생 합니다. ObjectDataSource에서 고유한 캐시에서 데이터를 액세스할 경우이 이벤트는 발생 하지 않습니다.

이제는 브라우저를 통해이 페이지를 참조 하세요. 에서는 이후 아직 캐싱을 구현 하는, 페이지, 정렬 또는 그리드 페이지를 편집할 때마다 했습니다로 표시 되어야 텍스트, Selecting 이벤트 발생 그림 8 보여 줍니다.


[![각 GridView 페이징된 편집, 시간 또는 Sorted ObjectDataSource의 Selecting 이벤트 발생](using-sql-cache-dependencies-vb/_static/image8.gif)](using-sql-cache-dependencies-vb/_static/image9.png)

**그림 8**: The ObjectDataSource s `Selecting` 페이징 되는 GridView 이벤트 발생 합니다. 각 시간, 편집, 또는 Sorted ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-vb/_static/image10.png))


설명한 것 처럼는 [는 ObjectDataSource 사용 하 여 데이터 캐싱을](caching-data-with-the-objectdatasource-vb.md) 설정 자습서는 `EnableCaching` 속성을 `True` 로 지정 된 기간에 대 한 해당 데이터를 캐시 하도록 ObjectDataSource 하면 해당 `CacheDuration` 속성입니다. ObjectDataSource 역시는 [ `SqlCacheDependency` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sqlcachedependency.aspx), 캐시 된 데이터의 패턴을 사용 하 여 하나 이상의 SQL 캐시 종속성을 추가:


[!code-css[Main](using-sql-cache-dependencies-vb/samples/sample9.css)]

여기서 *databaseName* 에 지정 된 데이터베이스의 이름는 `name` 특성에는 `<add>` 요소에 `Web.config`, 및 *tableName* 데이터베이스 테이블의 이름입니다. 예를 들어 데이터를 무기한으로 캐시 하는 ObjectDataSource를 만들려는 Northwind s에 대해 SQL 캐시 종속성에 따라 `Products` 테이블, ObjectDataSource s 설정 `EnableCaching` 속성을 `True` 및 해당 `SqlCacheDependency` 속성을 NorthwindDB:Products 합니다.

> [!NOTE]
> SQL 캐시 종속성을 사용할 수 있습니다 *및* 설정 하 여 시간 기반 만료 `EnableCaching` 를 `True`, `CacheDuration` 시간 간격 및 `SqlCacheDependency` 데이터베이스 및 테이블 이름에 있습니다. ObjectDataSource 때나 폴링 시스템 정보 중 발생 하는 먼저 기본 데이터베이스 데이터가 변경 된 시간 기반 만료에 도달 하면 해당 데이터를 제거 하 합니다.


GridView에서 `SqlCacheDependencies.aspx` -두 테이블의 데이터를 표시 `Products` 및 `Categories` (제품 s `CategoryName` 필드를 통해 검색 되는 `JOIN` 에 `Categories`). 따라서 두 개의 SQL 캐시 종속성을 지정 하려는: NorthwindDB:Products; NorthwindDB:Categories 합니다.


[![ObjectDataSource SQL 캐시 종속성을 사용 하 여 제품 및 범주에 캐싱 지원 하도록 구성](using-sql-cache-dependencies-vb/_static/image9.gif)](using-sql-cache-dependencies-vb/_static/image11.png)

**그림 9**: 구성 지원 캐싱을 사용 하 여 SQL 캐시 종속성을 ObjectDataSource에서 `Products` 및 `Categories` ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-vb/_static/image12.png))


캐싱 지원 하기 위해 ObjectDataSource를 구성한 후 브라우저를 통해 페이지를 다시 확인 합니다. 또한 텍스트 Selecting 이벤트를 발생 합니다. 첫 번째 페이지 방문에 표시 되어야 하지만 더 이상 나타나지 페이징, 정렬 또는 편집 취소 단추를 클릭 하는 경우. 이 데이터를 ObjectDataSource의 캐시에 로드 된 후 남아 있기 때문에 있을 때까지 `Products` 또는 `Categories` 테이블을 수정 하거나 데이터가 GridView을 통해 업데이트 됩니다.

표를 통해 페이징 및 Selecting 이벤트 부족 주목할 발생 합니다. 후 텍스트를 새 브라우저 창을 열고의 편집, 삽입 및 삭제 섹션의에서 기본 사항 자습서로 이동 (`~/EditInsertDelete/Basics.aspx`). 이름이 나 제품의 가격을 업데이트 합니다. 그런 다음에서 첫 번째 브라우저 창으로 데이터의 다른 페이지, 모눈 정렬 보거나 행의 편집 단추를 클릭 합니다. (그림 10 참조)를 수정 된 데이터는 기본 데이터베이스 Selecting 이벤트를 발생 합니다.이 시간에 더 이상 표시 합니다. 텍스트 표시 되지 않으면 몇 분 정도 기다렸다가 다시 시도 하십시오. 폴링 서비스 변경 내용을 체크 인하는 기억는 `Products` 테이블 마다 `pollTime` 밀리초 이므로 기본 데이터를 업데이트 하는 경우과 캐시 된 데이터를 제거 합니다.


[![캐시 된 제품 데이터를 제거 하 여 Products 테이블을 수정](using-sql-cache-dependencies-vb/_static/image10.gif)](using-sql-cache-dependencies-vb/_static/image13.png)

**그림 10**: 캐시 제품 데이터를 제거 하 여 Products 테이블을 수정 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-vb/_static/image14.png))


## <a name="step-6-programmatically-working-with-thesqlcachedependencyclass"></a>6 단계: 프로그래밍 방식으로 사용 하 여`SqlCacheDependency`클래스

[아키텍처에서 데이터 캐싱](caching-data-in-the-architecture-vb.md) 자습서는 ObjectDataSource 캐싱을 긴밀 하 게 연결 하는 대신 아키텍처에서 별도 캐싱 레이어를 사용 하는 이점에 검토 합니다. 해당 자습서에서 만든는 `ProductsCL` 클래스를 프로그래밍 방식으로 데이터 캐시 사용을 보여 줍니다. 캐싱 계층에서 SQL 캐시 종속성을 사용 하려면 사용 된 `SqlCacheDependency` 클래스입니다.

폴링 시스템과 `SqlCacheDependency` 개체는 특정 데이터베이스와 테이블 쌍으로 연결 되어야 합니다. 다음 코드 예를 들어 만듭니다는 `SqlCacheDependency` s Northwind 데이터베이스를 기반으로 개체 `Products` 테이블:


[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample10.vb)]

두 입력 매개 변수는 `SqlCacheDependency`의 생성자는 데이터베이스 및 테이블 이름을 각각. ObjectDataSource s와 함께 `SqlCacheDependency` 속성, 사용 되는 데이터베이스 이름은에 지정 된 값과 같으면는 `name` 특성에는 `<add>` 요소에 `Web.config`합니다. 테이블 이름은 데이터베이스 테이블의 실제 이름이입니다.

연결 하는 `SqlCacheDependency` 데이터 캐시에 추가 된 항목을 사용 하 여 중 하나는 `Insert` 종속성을 허용 하는 메서드 오버 로드 합니다. 다음 코드에서는 추가 *값* 정해 지지 않은 기간에 대 한 데이터 캐시에 있지만 변수와 연결는 `SqlCacheDependency` 에 `Products` 테이블입니다. 즉, *값* 폴링 시스템이 검색 하기 때문에 메모리 제약 때문에 제거 될 때까지 또는 캐시에 유지 됩니다는 `Products` 테이블은 캐시 된 이후 변경 되었습니다.


[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample11.vb)]

캐싱 계층 s `ProductsCL` 클래스에는 현재 데이터를 캐시는 `Products` 60 초의 시간 기반 만료를 사용 하 여 테이블입니다. S를 SQL 캐시 종속성을 대신 사용 하도록이 클래스를 업데이트 하도록 합니다. `ProductsCL` 클래스의 `AddCacheItem` 에 데이터를 캐시에 추가 된 메서드를 현재 다음 코드를 포함 합니다.


[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample12.vb)]

이 코드를 사용 하 여 업데이트를 `SqlCacheDependency` 개체가 아니라는 `MasterCacheKeyArray` 캐시 종속성:


[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample13.vb)]

이 기능을 테스트 하려면 기존 아래에 있는 페이지에는 GridView 추가 `ProductsDeclarative` GridView입니다. 이 새 GridView s 설정 `ID` 를 `ProductsProgrammatic` 고 라는 새 ObjectDataSource에 바인딩하는 스마트 태그를 통해 `ProductsDataSourceProgrammatic`합니다. ObjectDataSource 사용 하도록 구성 된 `ProductsCL` 드롭 다운 목록에서 선택 및 업데이트 탭 설정 클래스 `GetProducts` 및 `UpdateProduct`각각 합니다.


[![ObjectDataSource ProductsCL 클래스를 사용 하도록 구성](using-sql-cache-dependencies-vb/_static/image11.gif)](using-sql-cache-dependencies-vb/_static/image15.png)

**그림 11**: 구성에 사용 하 여 ObjectDataSource는 `ProductsCL` 클래스 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-vb/_static/image16.png))


[![GetProducts 메서드 선택 탭의 드롭 다운 목록에서 선택](using-sql-cache-dependencies-vb/_static/image12.gif)](using-sql-cache-dependencies-vb/_static/image17.png)

**그림 12**: 선택 된 `GetProducts` 탭 선택 s 드롭 다운 목록에서에서 메서드 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-vb/_static/image18.png))


[![UpdateProduct 메서드 업데이트 탭의 드롭 다운 목록에서 선택](using-sql-cache-dependencies-vb/_static/image13.gif)](using-sql-cache-dependencies-vb/_static/image19.png)

**그림 13**: UpdateProduct 메서드 업데이트 탭의 드롭 다운 목록에서에서 선택 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-vb/_static/image20.png))


데이터 소스 구성 마법사를 완료 한 후 Visual Studio는 만듭니다 BoundFields 및 CheckBoxFields GridView에서 각 데이터 필드에 대 한 합니다. 마찬가지로 첫 번째 GridView이이 페이지에 추가 된 모든 필드를 제거 하지만 `ProductName`, `CategoryName`, 및 `UnitPrice`, 나타나며이 필드의 서식을 지정 하 고 있습니다. GridView s 스마트 태그에서의 페이징 사용, 사용 하도록 설정 및 편집 사용 확인란을 선택 합니다. 과 마찬가지로 `ProductsDataSourceDeclarative` ObjectDataSource, Visual Studio는 설정의 `ProductsDataSourceProgrammatic` ObjectDataSource s `OldValuesParameterFormatString` 속성을 `original_{0}`합니다. 제대로 작동,이 속성을 설정 하는 GridView의 편집 기능에 대 한 순서 대로 다시 `{0}` (또는 선언적 구문에서 속성 할당을 함께 제거).

이러한 작업을 완료 한 후 결과 GridView 및 ObjectDataSource 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](using-sql-cache-dependencies-vb/samples/sample14.aspx)]

SQL 테스트 하려면 캐싱 계층에서 캐시 종속성에 중단점을 설정는 `ProductCL` s 클래스 `AddCacheItem` 메서드와 다음 디버깅을 시작 합니다. 처음 방문 `SqlCacheDependencies.aspx`, 데이터를 처음으로 요청 하 고 캐시에 배치 된 대로 중단점이 적중 됩니다. 다음으로 GridView에서 다른 페이지로 이동 하거나 열 중 하나를 정렬 합니다. 이렇게 하면 해당 데이터를 GridView 하지만 후 캐시에서 발견 되어야 데이터의 `Products` 데이터베이스 테이블 수정 되지 않았습니다. 데이터는 캐시에서 찾을 수 없습니다 반복 해 서, 메모리가 충분 한 사용 가능한 컴퓨터에 있는지 확인 하 고 다시 시도 하십시오.

GridView의 몇 가지 페이지를 통해 페이징, 후 두 번째 브라우저 창을 열고 다음을 편집, 삽입 및 삭제 섹션의에서 기본 사항 자습서로 이동 (`~/EditInsertDelete/Basics.aspx`). Products 테이블에서 레코드를 업데이트 하 고 그런 다음 첫 번째 브라우저 창에서 새 페이지를 보거나 정렬 헤더 중 하나를 클릭 합니다.

이 시나리오에서는 나타납니다 다음 두 가지 중 하나: 중 하나는 중단점이 적중지 것입니다를 나타내는 캐시 된 데이터는 데이터베이스의 변경으로 인해 제거 되었습니다 또는, 중단점이 적중 되지 것입니다, 즉 `SqlCacheDependencies.aspx` 가 이제 유효 하지 않은 데이터를 표시 합니다. 중단점이 적중 되지 않습니다 경우 가능성이 폴링 서비스 데이터가 변경 된 후 아직 실행 되지 않습니다는 때문에입니다. 폴링 서비스 변경 내용을 체크 인하는 기억는 `Products` 테이블 마다 `pollTime` 밀리초 이므로 기본 데이터를 업데이트 하는 경우과 캐시 된 데이터를 제거 합니다.

> [!NOTE]
> 이 지연 시간은에 GridView 통해 제품 중 하나를 편집할 때 나타날 가능성이 더 `SqlCacheDependencies.aspx`합니다. 에 [아키텍처에서 데이터 캐싱](caching-data-in-the-architecture-vb.md) 추가 자습서는 `MasterCacheKeyArray` 캐시 종속성을 통해 편집 중인 데이터를 확인 하는 `ProductsCL` s 클래스 `UpdateProduct` 메서드는 캐시에서 제거 되었습니다. 그러나 수정 하는 경우이 캐시 종속성 교체는 `AddCacheItem` 이 단계에서 메서드 따라서 및는 `ProductsCL` 클래스 계속 폴링 시스템 정보에 대 한 변경 될 때까지 캐시 된 데이터를 표시 됩니다는 `Products` 테이블입니다. 다시 삽입 하는 방법을 살펴보려는 `MasterCacheKeyArray` 7 단계에서에서 종속성을 캐시 합니다.


## <a name="step-7-associating-multiple-dependencies-with-a-cached-item"></a>7 단계: 캐시 된 항목을 여러 종속성 연결

이전에 설명한 대로 `MasterCacheKeyArray` 캐시 종속성은 있는지 확인 하는 데 사용 되 *모든* 내에서 연결 된 모든 단일 항목을 업데이트할 때는 제품 관련 데이터를 캐시에서 제거 합니다. 예를 들어는 `GetProductsByCategoryID(categoryID)` 메서드 캐시 `ProductsDataTables` 인스턴스 각각에 대해 고유한 *categoryID* 값입니다. 이러한 개체 중 하나를 제거 하는 경우는 `MasterCacheKeyArray` 캐시 종속성 확인 하는 다른 사용자도 제거 됩니다. 이 캐시 종속성 없이 캐시 된 데이터를 변경할 때 가능성이 있습니다 다른 캐시 제품 데이터가 만료 될 수 있습니다. 따라서 그 유지할 있습니다 중요 s는 `MasterCacheKeyArray` SQL 캐시 종속성을 사용 하는 경우 종속성을 캐시 합니다. 그러나 데이터 캐시 s `Insert` 메서드는 단일 종속성 개체에 대 한 허용 합니다.

또한 SQL 캐시 종속성을 작업할 때 종속성으로 여러 데이터베이스 테이블을 연결 해야 할 수도 있습니다. 예를 들어는 `ProductsDataTable` 에서 캐시 된는 `ProductsCL` 클래스에는 각 제품에 대 한 범주 및 공급자 이름이 포함 되지만 `AddCacheItem` 메서드 종속성에 대해서만 사용 `Products`합니다. 이 상황에서 사용자 범주 또는 공급 업체의 이름을 업데이트 하는 경우 캐시 된 제품 데이터 캐시에 유지 되며 기간이 만료 합니다. 따라서 캐시 제품 데이터에 종속 되 게 하려고 뿐만 아니라는 `Products` 테이블에서 `Categories` 및 `Suppliers` 테이블도 합니다.

[ `AggregateCacheDependency` 클래스](https://msdn.microsoft.com/library/system.web.caching.aggregatecachedependency.aspx) 캐시 항목이 여러 개이면 종속성 연결에 대 한는 수단을 제공 합니다. 만들어 시작 프로그램 `AggregateCacheDependency` 인스턴스. 다음으로 사용 하 여 종속성 집합을 추가 `AggregateCacheDependency` s `Add` 메서드. 데이터 캐시에 항목을 이후 삽입할 때 전달 된 `AggregateCacheDependency` 인스턴스. 때 *모든* 의 `AggregateCacheDependency` 인스턴스의 종속성이 변경, 캐시 된 항목이 제거 됩니다.

다음 테이블에 대 한 업데이트 된 코드에 나와 `ProductsCL` s 클래스 `AddCacheItem` 메서드. 메서드는 `MasterCacheKeyArray` 종속성과 함께 캐시 `SqlCacheDependency` 에 대 한 개체는 `Products`, `Categories`, 및 `Suppliers` 테이블. 모든 결합 되 하나로 `AggregateCacheDependency` 라는 개체 `aggregateDependencies`에 전달 되는 `Insert` 메서드.


[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample15.vb)]

이 새 코드를 테스트 합니다. 이제 변경는 `Products`, `Categories`, 또는 `Suppliers` 테이블 입력 될 캐시 된 데이터를 발생 합니다. 또한는 `ProductsCL` s 클래스 `UpdateProduct` GridView 통해 제품을 편집할 때 호출 되는 메서드를 제거는 `MasterCacheKeyArray` 캐시는 캐시 된 종속성 `ProductsDataTable` 제거할와 다음 다시 검색할 데이터 요청입니다.

> [!NOTE]
> SQL 캐시 종속성으로 사용할 수도 있습니다 [출력 캐싱을](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/output.aspx)합니다. 이 기능의 데모를 보려면 참조: [SQL Server에 ASP.NET 출력 캐싱을 사용 하 여](https://msdn.microsoft.com/library/e3w8402y(VS.80).aspx)합니다.


## <a name="summary"></a>요약

데이터베이스 데이터 캐싱, 데이터는 데이터베이스에서 수정 될 때까지 캐시에 이상적으로 유지 됩니다. ASP.NET 2.0과 함께 SQL 캐시 종속성 만들고 사용할 수 있는 선언적 방법과 프로그래밍 시나리오에 사용 됩니다. 데이터를 수정 하는 경우를 검색 중인 과제 중 하나는이 방법을 사용 합니다. 전체 버전의 Microsoft SQL Server 2005 쿼리 결과가 변경 될 때 응용 프로그램에 알릴 수 있는 알림 기능을 제공 합니다. Express Edition of SQL Server 2005 및 이전 버전의 SQL Server의 경우 폴링 시스템을 대신 사용 해야 합니다. 다행히 필요한 폴링 인프라 설정은 매우 간단 합니다.

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Microsoft SQL Server 2005에서에서 쿼리 알림 사용](https://msdn.microsoft.com/library/ms175110.aspx)
- [쿼리 알림 생성](https://msdn.microsoft.com/library/ms188669.aspx)
- [에 `SqlCacheDependency` 클래스](https://msdn.microsoft.com/library/ms178604(VS.80).aspx)
- [ASP.NET SQL Server 등록 도구 (`aspnet_regsql.exe`)](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)
- [개요 `SqlCacheDependency`](http://www.aspnetresources.com/blog/sql_cache_depedency_overview.aspx)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가 Marko Rangel, Teresa 머피 및 Hilton Giesenow 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](caching-data-at-application-startup-vb.md)
