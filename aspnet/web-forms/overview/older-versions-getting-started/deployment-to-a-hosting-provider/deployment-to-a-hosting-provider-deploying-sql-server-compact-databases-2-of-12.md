---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
title: 'SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 배포 SQL Server Compact 데이터베이스-12 2 | Microsoft Docs'
author: tdykstra
description: 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹 응용 프로그램 프로젝트 Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 중...
ms.author: aspnetcontent
ms.date: 11/17/2011
ms.assetid: c3c76516-4c48-4153-bd03-d70e3a3edbb0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
msc.type: authoredcontent
ms.openlocfilehash: dc094211df77e6d3ff5eacb878be901e3552fd13
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803060"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-sql-server-compact-databases---2-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 배포 SQL Server Compact 데이터베이스-2/12
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹용 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. Visual Studio 2010 웹 게시 업데이트를 설치 하는 경우에 사용할 수 있습니다. 계열에 대 한 소개를 참조 하세요 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 출시 이후 도입 된 배포 기능을 보여 줍니다, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다 및 Azure App Service Web Apps를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하세요 [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)입니다.


## <a name="overview"></a>개요

이 자습서에는 두 SQL Server Compact 데이터베이스 및 배포에 대 한 데이터베이스 엔진을 설정 하는 방법을 보여 줍니다.

데이터베이스 액세스를 위한 Contoso University 응용 프로그램에.NET Framework에 포함 되어 있지 않으므로 응용 프로그램을 사용 하 여 배포 해야 하는 다음 소프트웨어가 필요 합니다.

- [SQL Server Compact](https://www.microsoft.com/sqlserver/en/us/editions/compact.aspx) (데이터베이스 엔진).
- [ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) (하는 SQL Server Compact를 사용 하는 ASP.NET 멤버 자격 사용)
- [Entity Framework 5.0](https://msdn.microsoft.com/library/gg696172(d=lightweight,v=vs.103).aspx)(Code First 마이그레이션 사용 하 여).

데이터베이스의 구조와 일부 (모두는 아님) 응용 프로그램의 두 데이터의 데이터베이스를 배포 해야 합니다. 일반적으로 응용 프로그램을 개발할 때는 테스트 데이터는 라이브 사이트에 배포 하지 않으려는 데이터베이스를 입력 합니다. 그러나 배포 하려는 일부 프로덕션 데이터를 입력할 수 있습니다. 이 자습서에는 필요한 소프트웨어 및 올바른 데이터가 포함 된 배포 하는 경우 Contoso University 프로젝트를 구성 합니다.

미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.

## <a name="sql-server-compact-versus-sql-server-express"></a>SQL Server Express 및 SQL Server Compact

샘플 응용 프로그램에서는 SQL Server Compact 4.0을 사용합니다. 이 데이터베이스 엔진은 웹 사이트에 대 한 비교적 새로운 옵션 이전 버전의 SQL Server Compact는 웹 호스팅 환경에서에서 작동 하지 않습니다. SQL Server Compact는 SQL Server Express를 사용 하 여 개발 하 고 전체 SQL Server에 배포 하는 더 일반적인 시나리오에 비해 몇 가지 이점을 제공 합니다. 선택한 호스팅 공급자에 따라 SQL Server Compact 때문일 수 있습니다를 배포 하려면 저렴 한 일부 공급자는 전체 SQL Server 데이터베이스를 지원 하도록 추가 요금이 부과 됩니다. 데이터베이스 엔진 자체 웹 응용 프로그램의 일부로 배포할 수 있으므로 SQL Server Compact에 대 한 추가 요금 없이 있습니다.

그러나 제한 사항을 알아야도 합니다. SQL Server Compact 지원 하지 않습니다 저장된 프로시저, 트리거, 뷰 또는 복제. (SQL Server Compact에서 지원 되지 않는 SQL Server 기능의 전체 목록은 참조 하세요 [차이점 간에 SQL Server Compact 및 SQL Server](https://msdn.microsoft.com/library/bb896140.aspx).) 또한 SQL Server Express 및 SQL Server 데이터베이스의 스키마 및 데이터를 조작 하는 데 사용할 수 있는 도구 중 일부를 작동 하지 않습니다 SQL Server Compact를 사용 하 여. 예를 들어 사용할 수 없습니다 SQL Server Management Studio 또는 SQL Server Data Tools Visual Studio에서 SQL Server Compact 데이터베이스를 사용 합니다. SQL Server Compact 데이터베이스를 사용 하 여 작업에 대 한 다른 옵션을 수행 해야 합니다.

- SQL Server Compact에 대 한 제한 된 데이터베이스 조작 기능을 제공 하는 Visual Studio에서 서버 탐색기를 사용할 수 있습니다.
- 데이터베이스 조작 기능을 사용할 수 있습니다 [WebMatrix](https://www.microsoft.com/web/webmatrix/), 서버 탐색기 보다 더 많은 기능이 있는 합니다.
- 비교적 완전 한 제 3 자 사용 하거나 오픈 소스 도구를 같은 합니다 [SQL Server Compact 도구 상자](https://github.com/ErikEJ/SqlCeToolbox) 하 고 [SQL Compact 데이터 및 스키마 스크립트 유틸리티](https://github.com/ErikEJ/SqlCeToolbox)합니다.
- 작성 하 고 데이터베이스 스키마를 조작 하는 고유한 DDL (데이터 정의 언어) 스크립트를 실행할 수 있습니다.

SQL Server Compact를 사용 하 여 시작 하 고 요구 사항을 진화 함에 따라 나중에 업그레이드할 수 있습니다. 이 시리즈의 뒷부분에 나오는 자습서 SQL Server Express를 SQL Server를 SQL Server Compact에서 마이그레이션하는 방법을 보여 줍니다. 그러나 새 응용 프로그램을 만드는 하 고 나중에 SQL Server 필요 하고자 하는 경우 SQL Server 또는 SQL Server Express를 시작 하는 것이 좋습니다.

## <a name="configuring-the-sql-server-compact-database-engine-for-deployment"></a>배포에 대 한 SQL Server Compact 데이터베이스 엔진 구성

Contoso University 응용 프로그램의 데이터 액세스에 필요한 소프트웨어는 다음 NuGet 패키지를 설치 하 여 추가 되었습니다.

- [SqlServerCompact](http://nuget.org/List/Packages/SqlServerCompact)
- [System.Web.Providers](http://nuget.org/List/Packages/System.Web.Providers) (ASP.NET 유니버설 공급자)
- [EntityFramework](http://nuget.org/List/Packages/EntityFramework)
- [EntityFramework.SqlServerCompact](http://nuget.org/List/Packages/EntityFramework.sqlservercompact)

링크는이 자습서에 대 한 다운로드 한 시작 프로젝트에 설치 된 것 보다 최신일 수 있는 이러한 패키지의 현재 버전을 가리킵니다. 호스팅 공급자에 대 한 배포에 대 한 Entity Framework 5.0 이상을 사용 하는지 확인 합니다. Code First 마이그레이션을의 이전 버전에서는 완전 신뢰 하 고 여러 호스팅 공급자에서 응용 프로그램은 보통 신뢰에서 실행 됩니다. 보통 신뢰 하는 방법에 대 한 자세한 내용은 참조는 [IIS 테스트 환경으로 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) 자습서입니다.

일반적으로 NuGet 패키지 설치 응용 프로그램을 사용 하 여이 소프트웨어를 배포 하는 데 필요한 모든 담당 합니다. 경우에 따라 Web.config 파일을 변경 하 고 솔루션을 빌드할 때마다 실행 되는 PowerShell 스크립트를 추가 하는 등의 작업 해야 합니다. **NuGet을 사용 하지 않고 이러한 기능 (예: SQL Server Compact 및 Entity Framework)에 대 한 지원을 추가 하려는 경우는 NuGet 패키지 설치 용도 동일한 작업을 수동으로 수행할 수 있도록 알고 있는지 확인 해야 합니다.**

한 가지 예외가 없는 NuGet 하지 주의 모든 성공적인 배포를 확인 하기 위해 수행 해야 합니다. 네이티브 어셈블리를 복사 하는 프로젝트에는 빌드 후 스크립트를 추가 하는 SqlServerCompact NuGet 패키지 *x86* 하 고 *amd64* 프로젝트 아래의 하위 폴더 *bin* 폴더에 있지만 스크립트 프로젝트에서 해당 폴더를 포함 되지 않습니다. 결과적으로, 웹 배포 복사 되지 않습니다 하는 대상 웹 사이트에 프로젝트에 수동으로 포함 하지 않으면. (기본 배포 구성에서이 동작으로 인해; 이러한 자습서에서 사용 하지 않는, 다른 옵션을이 동작을 제어 하는 설정을 변경 하는 것입니다. 변경할 수 있는 설정이 **응용 프로그램을 실행 하는 데 필요한 파일만** 아래 **배포할 항목** 에 **웹 패키지 및 게시** 탭은 **프로젝트 속성** 창입니다. 이 설정을 변경는 일반적으로 권장 되지 있습니다 필요 프로덕션 환경에 더 많은 파일이 배포 시에서 발생할 수 있기 때문입니다. 대안에 대 한 자세한 내용은 참조는 [프로젝트 속성 구성](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md) 자습서입니다.)

프로젝트를 선택한 다음 **솔루션 탐색기** 클릭 **모든 파일 표시** 이미 수행 하지 않은 경우. 클릭 해야 할 수도 있습니다 **새로 고침**합니다.

![Solution_Explorer_Show_All_Files](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image1.png)

확장을 **bin** 폴더를 합니다 **amd64** 하 고 **x86** 폴더를 선택한 다음 해당 폴더를 마우스 오른쪽 단추를 선택 **프로젝트에포함**.

![amd64_and_x86_in_Solution_Explorer.png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image2.png)

폴더 아이콘 변경 폴더를 프로젝트에 포함 되어 있는지 표시 됩니다.

![Solution_Explorer_amd64_included.png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image3.png)

## <a name="configuring-code-first-migrations-for-application-database-deployment"></a>응용 프로그램 데이터베이스 배포에 대 한 Code First 마이그레이션을 구성

응용 프로그램 데이터베이스를 배포할 때 일반적으로 하지 단순히에 데이터를 모두 사용 하 여 개발 데이터베이스를 프로덕션에 배포할 이므로 대부분의 데이터에 있는 아마도 테스트용 으로만 합니다. 예를 들어, 학생 이름을 테스트 데이터베이스에는 가상입니다. 반면, 자주 배포할 수 없습니다에 데이터가 없는 데이터베이스 구조만 전혀 합니다. 테스트 데이터베이스에 있는 데이터의 일부 실제 데이터를 사용할 수 있으며 사용자가 응용 프로그램을 사용 하기 시작 하는 경우 있습니다 여야 합니다. 예를 들어 데이터베이스 유효한 등급 값 또는 실제 부서 이름을 포함 하는 테이블이 있다고 가정 합니다.

이 일반적인 시나리오를 시뮬레이션 하려면 데이터베이스에 있는 프로덕션 환경에서 원하는 데이터만 삽입 하는 코드의 첫 번째 마이그레이션을 시드 메서드를 구성 합니다. 프로덕션 환경에서 Code First는 데이터베이스를 만든 후 프로덕션 환경에서 실행 되므로이 Seed 메서드 테스트 데이터를 삽입 하지 않습니다.

이전 버전의 Code First 마이그레이션을 릴리스되기 전에 것이 일반적 이었습니다 또한 테스트 데이터를 삽입 하는 시드 메서드 했으므로 개발 하는 동안 모델 바뀔 때마다 데이터베이스 완전히 삭제 하 고 처음부터 다시 만들어야 합니다. Code First 마이그레이션을 사용 하 여 테스트 데이터는 필요 없는 Seed 메서드에 테스트 데이터를 포함 하므로 데이터베이스 변경 된 후 보존 됩니다. 다운로드 한 프로젝트 초기값 메서드에서 이니셜라이저 클래스의 모든 데이터를 포함 하 여 사전 마이그레이션 방법을 사용 합니다. 이 자습서에서는 이니셜라이저 클래스를 사용 하지 않도록 설정 하 고 마이그레이션을 사용 하도록 설정 합니다. 그런 다음 데이터를 프로덕션에 삽입할 삽입 되도록 마이그레이션 구성 클래스의 시드 메서드를 업데이트 하겠습니다.

다음 다이어그램에서는 응용 프로그램 데이터베이스의 스키마를 보여 줍니다.

[![School_database_diagram](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image4.png)

이 자습서에서는 라고 가정 하는 `Student` 및 `Enrollment` 사이트를 처음 배포할 때 테이블이 비어 있어야 합니다. 다른 테이블을 때 응용 프로그램이 라이브 미리 로드 해야 하는 데이터를 포함 합니다.

Code First 마이그레이션을 사용 하 고는, 더 이상 사용 해야 합니다 **DropCreateDatabaseIfModelChanges** Code First 이니셜라이저입니다. 이 이니셜라이저에 대 한 코드는 ContosoUniversity.DAL 프로젝트에서 SchoolInitializer.cs 파일입니다. 설정 된 **appSettings** Web.config 파일의 요소를 응용 프로그램을 처음으로 데이터베이스에 액세스 하려고 하는 때마다 실행 되도록이 이니셜라이저 사용 하면:

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample1.xml?highlight=3)]

응용 프로그램 Web.config 파일을 열고 appSettings 요소에서 Code First 이니셜라이저 클래스를 지정 하는 요소를 제거 합니다. AppSettings 요소는 이제 다음과 같이 표시 됩니다.

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample2.xml)]

> [!NOTE]
> 이니셜라이저 클래스를 지정 하는 또 다른 방법은 호출 하 여 수행 됩니다 `Database.SetInitializer` 에 `Application_Start` 에서 메서드는 *Global.asax* 파일입니다. 해당 메서드를 사용 하 여 이니셜라이저를 지정 하는 프로젝트에서 Migrations를 사용 하는 경우 해당 코드 줄을 제거 합니다.


다음으로 Code First 마이그레이션을 사용 하도록 설정 합니다.

첫 번째 단계 ContosoUniversity 프로젝트를 시작 프로젝트로 설정 되어 있는지 확인 하는 것입니다. **솔루션 탐색기**ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **시작 프로젝트로 설정**합니다. Code First 마이그레이션을 데이터베이스 연결 문자열을 찾을 시작 프로젝트에 표시 됩니다.

**도구** 메뉴에서 클릭 **라이브러리 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.

![Selecting_Package_Manager_Console](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image6.png)

맨 위에 있는 합니다 **패키지 관리자 콘솔** 창 선택 ContosoUniversity.DAL 그 다음으로 기본 프로젝트에 `PM>` 프롬프트 "enable-마이그레이션"을 입력 합니다.

![enable-migrations_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image7.png)

이 명령은 만듭니다는 *Configuration.cs* 새 파일 *마이그레이션을* ContosoUniversity.DAL 프로젝트의 폴더입니다.

![Migrations_folder_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image8.png)

Code First 컨텍스트 클래스를 포함 하는 프로젝트에서 "enable-마이그레이션" 명령을 실행 해야 하기 때문에 DAL 프로젝트를 선택 합니다. 해당 클래스는 클래스 라이브러리 프로젝트의 경우 Code First 마이그레이션 솔루션에 대 한 시작 프로젝트에서 데이터베이스 연결 문자열을 찾습니다. ContosoUniversity 솔루션에서 웹 프로젝트를 시작 프로젝트로 설정한 합니다. (Visual Studio에서 시작 프로젝트와 연결 문자열을 포함 하는 프로젝트를 지정 하지 않은 경우 지정할 수 있습니다 시작 프로젝트에서 PowerShell 명령입니다. 마이그레이션을 사용 하도록 설정 명령에 대 한 명령 구문을 보려면를 입력할 수 있습니다 명령은 "get-도움말 사용-마이그레이션이".)

에 있는 메모를 바꾸고 Configuration.cs 파일을 엽니다는 `Seed` 메서드를 다음 코드로:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample3.cs)]

에 대 한 참조 `List` 필요가 없기 때문에 그 아래에 있는 빨간색의 구불구불한 선이는 `using` 아직 문을 해당 네임 스페이스에 대 한 합니다. 인스턴스 중 하나를 마우스 오른쪽 단추로 클릭 `List` 을 클릭 **해결**를 클릭 하 고 **System.Collections.Generic를 사용 하 여**입니다.

![문을 사용 하 여 해결](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image9.png)

다음 코드를 추가 하는이 메뉴를 선택 합니다 `using` 문을 파일의 맨 위 근처 합니다.

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample4.cs)]

> [!NOTE]
> 코드를 추가 합니다 `Seed` 메서드는 데이터베이스에 고정된 데이터를 삽입할 수 있는 여러 가지 방법 중 하나입니다. 대안은 코드를 추가 하는 `Up` 고 `Down` 각 마이그레이션 클래스의 메서드. 합니다 `Up` 고 `Down` 메서드는 데이터베이스 변경 내용을 구현 하는 코드를 포함 합니다. 예제에 표시 합니다 [데이터베이스 업데이트 배포](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) 자습서입니다.
> 
> 사용 하 여 SQL 문을 실행 하는 코드를 작성할 수도 있습니다는 `Sql` 메서드. 예를 들어, 예산 열 Department 테이블을 추가 했습니다 하는 마이그레이션의 일환으로 모든 부서 예산을 $ 1, 000.00를 초기화 하려는 경우 다음 줄의 코드를 추가할 수는 `Up` 마이그레이션에 대 한 메서드:
> 
> `Sql("UPDATE Department SET Budget = 1000");`
> 
> 이 자습서에서는 사용에 대해 표시 된이 예제는 `AddOrUpdate` 의 메서드를 `Seed` Code First 마이그레이션을 메서드의 `Configuration` 클래스입니다. 첫 번째 마이그레이션을 호출 코드는 `Seed` 모든 마이그레이션 후 메서드와이 메서드가 이미 삽입 되었거나 아직 없는 경우 삽입 된 행을 업데이트 합니다. `AddOrUpdate` 메서드 시나리오에 가장 적합 한 되지 않을 수 있습니다. 자세한 내용은 [EF 4.3 AddOrUpdate 메서드를 사용 하 여 주의](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) Julie Lerman의 블로그입니다.


프로젝트를 빌드하려면 CTRL-SHIFT-B를 누릅니다.

다음 단계를 만드는 것을 `DbMigration` 초기 마이그레이션에 대 한 클래스입니다. 원하는이 마이그레이션이 새 데이터베이스를 만들어 이미 존재 하는 데이터베이스를 삭제 해야 합니다. SQL Server Compact 데이터베이스에 포함 된 *.sdf* 파일을 *앱\_데이터* 폴더입니다. **솔루션 탐색기**를 확장 하 고 *앱\_데이터* 나타내는 두 SQL Server Compact 데이터베이스를 보려면 ContosoUniversity 프로젝트에서 *.sdf*파일입니다.

마우스 오른쪽 단추로 클릭 합니다 *School.sdf* 파일과 클릭 **삭제**합니다.

![sdf_files_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image10.png)

에 **패키지 관리자 콘솔** 창 "add-migration Initial" 명령을 입력 초기 마이그레이션을 만들고 "초기" 라는 이름을 지정 합니다.

![add-migration_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image11.png)

Code First 마이그레이션을에 다른 클래스 파일을 만듭니다는 *마이그레이션을* 폴더 및이 클래스는 데이터베이스 스키마를 만드는 코드를 포함 합니다.

에 **패키지 관리자 콘솔**, 명령 "업데이트-데이터베이스" 데이터베이스를 만들고 실행 하는 **초기값** 메서드.

![update-database_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image12.png)

(테이블에서 이미 존재 하 고 만들 수 없습니다를 나타내는 오류를 받게 되 면 것 및 실행 하기 전에 데이터베이스를 삭제 한 후 응용 프로그램을 실행 했으므로 `update-database`합니다. 이전과 삭제 합니다 *School.sdf* 파일을 다시 시도 `update-database` 명령입니다.)

응용 프로그램을 실행합니다. 이제 학생 페이지가 비어 있지만 강사 페이지는 강사를 포함 합니다. 새로운 하면 프로덕션 환경에서 응용 프로그램을 배포한 후입니다.

![Empty_Students_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image13.png)

![Instructors_page_after_initial_migration](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image14.png)

이제 프로젝트를 배포할 준비가 된 *학교* 데이터베이스입니다.

## <a name="creating-a-membership-database-for-deployment"></a>배포에 대 한 멤버 자격 데이터베이스 만들기

Contoso University 응용 프로그램 인증 및 사용자 권한 부여는 ASP.NET 멤버 자격 시스템 및 폼 인증을 사용 합니다. 해당 페이지 중 하나는 관리자만 액세스할 수 있습니다. 이 페이지를 보려면 응용 프로그램을 실행 하 고 선택 **업데이트 크레딧** 플라이 아웃 메뉴 아래에서 **과정**합니다. 응용 프로그램 표시 합니다 **로그인** 관리자만 사용할 수 있으므로 페이지는 **업데이트 크레딧** 페이지.

[![Log_in_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image15.png)

"$W0rd Pa" 암호를 사용 하 여 "관리자로" ("w0rd"에서 "o" 문자 대신 숫자 0 확인). 로그인 한 후에 **업데이트 크레딧** 페이지가 표시 됩니다.

[![Update_Credits_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image17.png)

처음으로 사이트를 배포 하 때 대부분 또는 모든 테스트를 위해 만든 사용자 계정을 제외에 공통적으로 적용 합니다. 이 경우에 관리자 계정 및 사용자 계정이 없는 배포. 테스트 계정을 수동으로 삭제 하는 대신 프로덕션 환경에서 해야 하는 한 관리자 사용자 계정과 있는 새 멤버 자격 데이터베이스를 만들어야 합니다.

> [!NOTE]
> 멤버 자격 데이터베이스 계정 암호의 해시를 저장 합니다. 다른 컴퓨터에서 계정에 배포 하려면 원본 컴퓨터에서 수행할 때 보다 해시 루틴이 대상 서버의 다른 해시를 생성 하지 않도록 해야 합니다. 생성 동일한 해시 ASP.NET Universal Providers를 사용 하는 경우 기본 알고리즘을 변경 하지 않으면으로 합니다. 기본 알고리즘 HMACSHA256 이며에 지정 된를 **유효성 검사** 특성을 **[machineKey](https://msdn.microsoft.com/library/w8h3skw9.aspx)** Web.config 파일의 요소입니다.


멤버 자격 데이터베이스에서 Code First 마이그레이션을 유지 되지 않습니다 되며 (하므로 School 데이터베이스에 대 한) 테스트 계정 사용 하 여 데이터베이스를 시드하는 자동 이니셜라이저가 없습니다. 따라서 사용 가능한 테스트 데이터를 유지 하려면에서는 할 테스트 데이터베이스의 복사본을 새로 만들려면.

**솔루션 탐색기**, 이름 바꾸기는 *aspnet.sdf* 파일을 *앱\_데이터* 폴더 *aspnet Dev.sdf*합니다. (복사본, 이름이 없는-잠시 후에 새 데이터베이스를 만들어야 합니다.)

**솔루션 탐색기**, 웹 프로젝트 (ContosoUniversity, 없습니다 ContosoUniversity.DAL) 확인란이 선택 되어 있는지 확인 합니다. 그런 다음 합니다 **프로젝트** 메뉴에서 **ASP.NET 구성** 실행 하는 **웹 사이트 관리 도구**(WAT).

선택 된 **보안** 탭 합니다.

[![WAT_Security_tab](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image19.png)

클릭 **만들거나 역할 관리** 추가한는 **관리자** 역할입니다.

[![WAT_Create_New_Role](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image21.png)

로 다시 이동 합니다 **보안** 탭을 클릭 **Create User**, "admin" 사용자를 관리자로 추가 하 고 합니다. 클릭 하기 전에 **Create User** 단추를 **Create User** 페이지에서 선택 되었는지 확인 합니다 **관리자** 확인란 합니다. 이 자습서에서 사용한 암호를 "Pa$ w0rd" 이며 모든 전자 메일 주소를 입력할 수 있습니다.

[![WAT_Create_User](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image23.png)

브라우저를 닫습니다. **솔루션 탐색기**에 새로운 새로 고침 단추를 클릭 *aspnet.sdf* 파일입니다.

![New_aspnet.sdf_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image25.png)

마우스 오른쪽 단추로 클릭 **aspnet.sdf** 선택한 **프로젝트에 포함**합니다.

## <a name="distinguishing-development-from-production-databases"></a>프로덕션 데이터베이스에서 고유한 개발

이 섹션에서는 개발 버전 학교 Dev.sdf 하 고 aspnet Dev.sdf 및 프로덕션 버전은 학교 Prod.sdf 및 aspnet Prod.sdf 데이터베이스를 이름을 바꿀 것입니다. 이 필요는 없지만 이렇게 하면 되므로 유지할 수 있도록 테스트 및 프로덕션 버전의 데이터베이스에서 혼동 합니다.

**솔루션 탐색기**, 클릭 **새로 고침** 앱을 확장 하 고\_앞에서 만든 School 데이터베이스를 참조 하세요. 마우스 오른쪽 단추로 클릭 하 고 선택 하려면 데이터 폴더 **프로젝트에 포함** .

![Including_School.sdf_in_project](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image26.png)

이름 바꾸기 *aspnet.sdf* 하 *aspnet Prod.sdf*합니다.

이름 바꾸기 *School.sdf* 하 *학교 Dev.sdf*합니다.

사용 하지 않으려면 Visual Studio에서 응용 프로그램을 실행 하는 *-Prod* 데이터베이스 파일의 버전을 사용 하려면 *-Dev* 버전입니다. 따라서를 가리키도록 Web.config 파일에서 연결 문자열을 변경 해야 합니다 *-개발* 버전의 데이터베이스입니다. (학교 Prod.sdf 파일을 만들지 않지만 괜찮습니다 만들어지므로 Code First는 해당 데이터베이스에 있는 앱을 실행 하는 첫 번째 프로덕션 시간.)

응용 프로그램 Web.config 파일을 열고 연결 문자열을 찾습니다.

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample5.xml)]

"Aspnet.sdf" "aspnet-Dev.sdf"로 변경 하 고 변경 "School.sdf" "학교 Dev.sdf".

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample6.xml?highlight=4-5)]

SQL Server Compact 데이터베이스 엔진 및 두 데이터베이스를 배포할 준비가 됩니다. 다음 자습서에서 설정한 자동 *Web.config* 파일은 개발, 테스트 및 프로덕션 환경에서 서로 달라 야 하는 설정에 대 한 변환 합니다. (변경 해야 하는 설정 된 연결 문자열에는 있지만 설정 변경 내용을 나중에 게시 프로필을 만들 때.)

## <a name="more-information"></a>추가 정보

NuGet에 대 한 자세한 내용은 참조 하세요. [NuGet 사용 하 여 프로젝트 라이브러리 관리](https://msdn.microsoft.com/magazine/hh547106.aspx) 하 고 [NuGet 설명서](http://docs.nuget.org/docs/start-here/overview)합니다. NuGet을 사용 하지 않으려는 경우 설치 될 때 무엇을 확인 하는 NuGet 패키지를 분석 하는 방법을 알아보려면 해야 합니다. (예를 들어 구성할 수 있습니다 *Web.config* 변환 등 빌드 시간에 실행 하도록 PowerShell 스크립트를 구성 합니다.) NuGet의 작동 원리에 대 한 자세한 내용은 참조 특히 [는 패키지 만들기 및 게시](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package) 하 고 [구성 파일 및 소스 코드 변환](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations)합니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-introduction-1-of-12.md)
> [다음](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
