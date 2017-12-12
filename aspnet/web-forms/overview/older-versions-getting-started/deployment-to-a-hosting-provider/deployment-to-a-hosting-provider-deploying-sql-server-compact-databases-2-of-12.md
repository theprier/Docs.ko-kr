---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
title: "SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 배포 SQL Server Compact 데이터베이스-2/12 | Microsoft Docs"
author: tdykstra
description: "이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시) ASP.NET Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: c3c76516-4c48-4153-bd03-d70e3a3edbb0
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
msc.type: authoredcontent
ms.openlocfilehash: d0b76c06495c51df3ed0f61cd318507a05240392
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-sql-server-compact-databases---2-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 배포 SQL Server Compact 데이터베이스-2/12
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시)는 ASP.NET 웹에 대 한 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. 웹 게시 업데이트를 설치 하는 경우에 Visual Studio 2010을 사용할 수 있습니다. 계열에 대 한 소개를 참조 하십시오. [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 릴리스 이후 도입 된 배포 기능을 표시, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다. 및 Azure 앱 서비스 웹 앱을 배포 하는 방법을 보여 줍니다. 하는 자습서를 참조 하십시오. [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)합니다.


## <a name="overview"></a>개요

이 자습서에는 두 개의 SQL Server Compact 데이터베이스 및 배포에 대 한 데이터베이스 엔진을 설정 하는 방법을 보여 줍니다.

데이터베이스 액세스를 위해 Contoso 대학교 응용 프로그램에.NET Framework에 포함 되어 있지 않으므로 응용 프로그램과 함께 배포 해야 하는 다음 소프트웨어가 필요:

- [SQL Server Compact](https://www.microsoft.com/sqlserver/en/us/editions/compact.aspx) (데이터베이스 엔진).
- [ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) (SQL Server Compact를 사용 하도록 ASP.NET 멤버 자격 시스템 있도록)
- [Entity Framework 5.0](https://msdn.microsoft.com/en-us/library/gg696172(d=lightweight,v=vs.103).aspx)(마이그레이션과 함께 첫 번째 코드).

데이터베이스의 구조와 일부 (모두는 아님)의 데이터를 응용 프로그램의 두 데이터베이스를 배포 해야 합니다. 일반적으로 응용 프로그램을 개발할 때 테스트 데이터 라이브 사이트에 배포 하지 않으려는 데이터베이스를 입력 합니다. 그러나 배포 하려는 일부 프로덕션 데이터를 입력할 수 있습니다. 이 자습서에서 필요한 소프트웨어와 되도록 올바른 데이터가 포함를 배포할 때 Contoso 대학 프로젝트를 구성 합니다.

미리 알림: 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 반드시 확인는 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.

## <a name="sql-server-compact-versus-sql-server-express"></a>SQL Server Express와 SQL Server Compact

예제 응용 프로그램에는 SQL Server Compact 4.0 사용 합니다. 이 데이터베이스 엔진은 웹 사이트;에 대해 비교적 새로운 옵션 이전 버전의 SQL Server Compact는 웹 호스팅 환경에서에서 작동 하지 않습니다. SQL Server Compact는 SQL Server Express를 사용 하 여 개발 하 고 전체 SQL Server에 배포의 일반적인 시나리오에 비해 몇 가지 이점을 제공 합니다. 선택한 호스팅 공급자에 따라 SQL Server Compact 때문일 수 있습니다를 배포 하기 쉽지만 일부 공급자는 전체 SQL Server 데이터베이스를 지원 하기 위해 추가 요금을 청구 합니다. 웹 응용 프로그램의 일부로 자체 데이터베이스 엔진으로 배포할 수에 SQL Server Compact에 대 한 무료 추가 합니다.

그러나 제한 사항을 알아야도 합니다. SQL Server Compact 지원 하지 않습니다 저장된 프로시저, 트리거, 뷰 또는 복제. (SQL Server Compact에서 지원 되지 않는 SQL Server 기능의 전체 목록은 참조 하십시오. [차이점 간의 SQL Server Compact 및 SQL Server](https://msdn.microsoft.com/en-us/library/bb896140.aspx).) 또한, 스키마 및 SQL Server Express 및 SQL Server 데이터베이스의 데이터를 조작 하는 데 사용할 수 있는 도구 중 일부를 작동 하지 않습니다 SQL Server Compact와. 예를 들어 있습니다 사용할 수 없습니다 SQL Server Management Studio 또는 SQL Server Data Tools Visual Studio에서 SQL Server Compact 데이터베이스. SQL Server Compact 데이터베이스 작업에 대 한 다른 옵션이지 않습니다.

- SQL Server Compact에 대 한 제한 된 데이터베이스 조작 기능을 제공 하는 Visual Studio에서 서버 탐색기를 사용할 수 있습니다.
- 데이터베이스 조작 기능을 사용할 수 [WebMatrix](https://www.microsoft.com/web/webmatrix/), 서버 탐색기에 비해 많은 기능이 있는 합니다.
- 상대적으로 모든 기능을 갖춘 공급 업체를 사용 하거나 같은 소스 도구를 열 수 있습니다는 [SQL Server Compact 도구 상자](https://github.com/ErikEJ/SqlCeToolbox) 및 [SQL Compact 데이터와 스키마 스크립트 유틸리티](https://github.com/ErikEJ/SqlCeToolbox)합니다.
- 작성 하 고 데이터베이스 스키마를 조작 하기 위한 DDL (데이터 정의 언어) 스크립트를 직접 실행할 수 있습니다.

SQL Server Compact와 시작을 다음 나중에 따라 진화 하는 사용자의 요구를 업그레이드할 수 있습니다. 이 시리즈의 이후의 자습서 SQL Server Express를 SQL Server를 SQL Server Compact에서 마이그레이션하는 방법을 보여 줍니다. 그러나 새 응용 프로그램을 만들려는 하 고 SQL Server를 나중에 필요 하 경우 SQL Server 또는 SQL Server Express로 시작 하는 것이 좋습니다.

## <a name="configuring-the-sql-server-compact-database-engine-for-deployment"></a>배포를 위한 SQL Server Compact 데이터베이스 엔진 구성

Contoso 대학교 응용 프로그램에서 데이터 액세스에 필요한 소프트웨어는 다음과 같은 NuGet 패키지를 설치 하 여 추가 되었습니다.

- [SqlServerCompact](http://nuget.org/List/Packages/SqlServerCompact)
- [System.Web.Providers](http://nuget.org/List/Packages/System.Web.Providers) (ASP.NET 유니버설 공급자)
- [EntityFramework](http://nuget.org/List/Packages/EntityFramework)
- [EntityFramework.SqlServerCompact](http://nuget.org/List/Packages/EntityFramework.sqlservercompact)

링크는이 자습서에 대 한 다운로드 한 시작 프로젝트에 설치 된 것 보다 최신일 수 있습니다 이러한 패키지의 현재 버전을 가리킵니다. 호스팅 공급자에 게 배포의 경우 Entity Framework 5.0 이상를 사용 해야 합니다. 이전 버전의 Code First 마이그레이션을 완전 신뢰 필요 하 고 보통 신뢰 호스팅 공급자는 대부분 응용 프로그램을 실행할 합니다. 보통 신뢰 하는 방법에 대 한 자세한 내용은 참조는 [iis 테스트 환경으로 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) 자습서입니다.

일반적으로 NuGet 패키지를 설치 하는 응용 프로그램에이 소프트웨어를 배포 하는 데 필요한 모든 처리 합니다. 이 경우에 따라 Web.config 파일을 변경 하 고 솔루션을 빌드할 때마다 실행 되는 PowerShell 스크립트를 추가 하는 등의 작업 해야 합니다. **NuGet을 사용 하지 않고 이러한 기능 (예: SQL Server Compact 및 Entity Framework)에 대 한 지원을 추가 하려면 NuGet 패키지 설치 용도 수동으로 동일한 작업을 수행할 수 있도록 알고 있는지 확인 합니다.**

한 가지 예외가 NuGet 성공적인 배포를 보장 하기 위해 수행 해야 하는 모든 항목의 주의 사용 하지 않습니다. 네이티브 어셈블리를 복사 하는 프로젝트에 빌드 후 스크립트를 추가 하는 SqlServerCompact NuGet 패키지 *x86* 및 *amd64* 프로젝트 아래의 하위 폴더도 *bin* 폴더, 하지만 스크립트 프로젝트에 해당 폴더를 포함 되지 않습니다. 결과적으로, 웹 배포 복사 되지 않습니다으로 대상 웹 사이트에는 프로젝트에 수동으로 포함 하지 않는 한 합니다. (기본 배포 구성에서이 동작으로 인해; 다른 옵션을이 자습서에 사용 하지 않으며,이 동작을 제어 하는 설정을 변경 하는 것입니다. 변경할 수 있는 설정은 **응용 프로그램을 실행 하는 데 필요한 파일만** 아래 **배포할 항목을** 에 **웹 패키지 및 게시** 탭은 **프로젝트 속성** 창. 이 설정을 변경 일반적으로 좋지 않습니다 수 있기 때문에 더 많은 파일이 배포에 있을 필요는 프로덕션 환경으로. 다음 방법에 대 한 자세한 내용은 참조는 [프로젝트 속성 구성](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md) 자습서입니다.)

프로젝트를 작성 한 다음 **솔루션 탐색기** 클릭 **모든 파일 표시** 아직 수행 하지 않은 경우. 클릭 해야 할 수 **새로 고침**합니다.

![Solution_Explorer_Show_All_Files](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image1.png)

확장 된 **bin** 폴더를는 **amd64** 및 **x86** 폴더를 선택한 후 해당 폴더를 마우스 오른쪽 단추로 클릭 및 선택 **프로젝트에포함**.

![amd64_and_x86_in_Solution_Explorer.png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image2.png)

폴더 아이콘 폴더가 프로젝트에 포함 되어 표시를 변경 합니다.

![Solution_Explorer_amd64_included.png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image3.png)

## <a name="configuring-code-first-migrations-for-application-database-deployment"></a>응용 프로그램 데이터베이스 배포에 대 한 Code First 마이그레이션을 구성합니다.

응용 프로그램 데이터베이스를 배포 하면 일반적으로 배포 하지는 않습니다 단순히 그 안의 데이터가 모든 개발 데이터베이스를 프로덕션에 대부분의 데이터에가 있기 때문에 아마도 테스트용 으로만 사용 합니다. 예를 들어 테스트 데이터베이스에 있는 학생 이름을 가상의 합니다. 반면에 자주 배포할 수는 없습니다 것에 데이터가 없는 데이터베이스 구조만 전혀 합니다. 테스트 데이터베이스에 있는 데이터의 일부 실제 데이터 일 수 있습니다 하며 사용자가 응용 프로그램을 사용 하기 시작 하는 경우 있습니다 이어야 합니다. 예를 들어 데이터베이스 유효한 등급 값 또는 실제 부서 이름을 포함 하는 테이블이 있다고 가정 합니다.

이 일반적인 시나리오를 시뮬레이션 하려면 프로덕션 환경에서 있습니다 수 있도록 하려는 데이터를 데이터베이스에 삽입 하는 코드 첫 번째 마이그레이션 시드 메서드를 구성 합니다. 프로덕션 환경에서 코드 첫 번째 데이터베이스를 만든 후 프로덕션 환경에서 실행 되므로이 초기값 메서드 테스트 데이터를 삽입 하지 않습니다.

이전 버전의 Code First 마이그레이션 전에 것이 일반적 시드 또한 테스트 데이터를 삽입 하는 방법에 대 한 해야 때문에 모든 모델을 개발 하는 동안 변경 된 데이터베이스 완전히 삭제 되 고 처음부터 다시 만들어집니다. Code First 마이그레이션을 사용 테스트 데이터는 유지 데이터베이스 변경 된 후 테스트 데이터를 포함 하 여 시드 메서드에서 필요 하지 않습니다. 다운로드 한 프로젝트 시드 메서드에 이니셜라이저 클래스의 모든 데이터를 포함 하 여의 사전 마이그레이션 메서드를 사용 합니다. 이 자습서의 이니셜라이저 클래스를 사용 하지 않도록 설정 하 고 마이그레이션을 사용 하도록 설정 합니다. 그런 다음 삽입만 원하는 데이터를 프로덕션에 삽입할 수 있도록 마이그레이션 구성 클래스에서 초기값 메서드를 업데이트 합니다.

다음 다이어그램에서는 응용 프로그램 데이터베이스의 스키마를 보여 줍니다.

[![School_database_diagram](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image4.png)

이 자습서에 대 한 라고 가정 하 고 `Student` 및 `Enrollment` 사이트를 처음 배포할 때 테이블이 비어 있어야 합니다. 다른 테이블 때 응용 프로그램 문제를 미리 로드 하는 데이터를 포함 합니다.

더 이상 사용 해야 하므로 Code First 마이그레이션을 사용 하 고는의 **DropCreateDatabaseIfModelChanges** Code First 이니셜라이저입니다. 이 이니셜라이저에 대 한 코드는 ContosoUniversity.DAL 프로젝트에서 SchoolInitializer.cs 파일입니다. 설정에는 **appSettings** Web.config 파일의 요소는 응용 프로그램 데이터베이스에 처음으로 액세스 하려고 시도 될 때마다 실행 되도록이 이니셜라이저 하면:

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample1.xml?highlight=3)]

응용 프로그램 Web.config 파일을 열고 appSettings 요소에서 Code First 이니셜라이저 클래스를 지정 하는 요소를 제거 합니다. AppSettings 요소는 이제 다음과 같이 보입니다.

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample2.xml)]

> [!NOTE]
> 또 다른 방법은 이니셜라이저 클래스를 지정 하는 호출 하 여 수행 `Database.SetInitializer` 에 `Application_Start` 에서 메서드는 *Global.asax* 파일입니다. 해당 메서드를 사용 하 여 이니셜라이저를 지정 하는 프로젝트에서 마이그레이션이 설정 하는 경우 해당 코드 줄을 제거 합니다.


다음으로 Code First 마이그레이션을 사용 하도록 설정 합니다.

ContosoUniversity 프로젝트를 시작 프로젝트로 설정 되어 있는지 확인 하는 첫 번째 단계가입니다. **솔루션 탐색기**ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **시작 프로젝트로 설정**합니다. Code First 마이그레이션을 데이터베이스 연결 문자열을 찾을 시작 프로젝트에 표시 됩니다.

**도구** 메뉴를 클릭 하 여 **라이브러리 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.

![Selecting_Package_Manager_Console](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image6.png)

맨 위에 있는 **패키지 관리자 콘솔** 창으로 기본 프로젝트 선택한 다음 at ContosoUniversity.DAL 선택은 `PM>` 프롬프트 "마이그레이션 사용"을 입력 합니다.

![enable migrations_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image7.png)

이 명령은 만듭니다는 *Configuration.cs* 를 새로운 파일 *마이그레이션* ContosoUniversity.DAL 프로젝트의 폴더에에서 있습니다.

![Migrations_folder_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image8.png)

Code First 컨텍스트 클래스를 포함 하는 프로젝트에서 "enable-migrations" 명령을 실행 해야 하기 때문에 DAL 프로젝트를 선택 합니다. 해당 클래스는 클래스 라이브러리 프로젝트에 포함 된 경우 Code First 마이그레이션을 솔루션에 대 한 시작 프로젝트에 데이터베이스 연결 문자열을 찾습니다. ContosoUniversity 솔루션의 웹 프로젝트를 시작 프로젝트로 설정한 합니다. (Visual Studio의 시작 프로젝트로 연결 문자열을 포함 된 프로젝트를 지정 하려면 원하지 않은 지정할 수 있습니다를 시작 프로젝트로 PowerShell 명령에서. Enable-migrations 명령을 위한 명령 구문은 보려면 입력할 수 있는 명령 "g e t-h 사용-마이그레이션"입니다.)

Configuration.cs 파일을 열고의 주석을 대체는 `Seed` 메서드를 다음 코드로:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample3.cs)]

에 대 한 참조 `List` 없기 때문에 그 아래 빨간색의 구불구불한 선이는 `using` 아직 문을 네임 스페이스에 대 한 합니다. 인스턴스 중 하나를 마우스 오른쪽 단추로 클릭 `List` 클릭 **해결**, 클릭 하 고 **System.Collections.Generic 사용**합니다.

![문을 사용 하 여 사용 하 여 확인](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image9.png)

다음 코드를 추가 하는이 메뉴를 선택은 `using` 문을 파일의 맨 위 근처 합니다.

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample4.cs)]

> [!NOTE]
> 코드를 추가 하는 `Seed` 메서드는 데이터베이스에 고정된 데이터를 삽입할 수 있는 여러 가지 방법 중 하나입니다. 다른 방법은 코드를 추가 하는 것은 `Up` 및 `Down` 각 마이그레이션 클래스의 메서드. `Up` 및 `Down` 메서드는 데이터베이스 변경 내용을 구현 하는 코드를 포함 합니다. 예제를 볼 수는 [데이터베이스 업데이트를 배포](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) 자습서입니다.
> 
> 사용 하 여 SQL 문을 실행 하는 코드를 작성할 수도 있습니다는 `Sql` 메서드. 예를 들어 예산 열에서 Department 테이블을 추가 하는 마이그레이션의 일환으로 $ 1, 000.00에 모든 부서 예산 초기화 하려고 하는 경우 다음 줄의 코드를 추가할 수는 `Up` 해당 마이그레이션에 대 한 메서드:
> 
> `Sql("UPDATE Department SET Budget = 1000");`
> 
> 이 자습서에서 사용 하 여 표시 된이 예제는 `AddOrUpdate` 에서 메서드는 `Seed` Code First 마이그레이션을 방식의 `Configuration` 클래스입니다. 첫 번째 마이그레이션 호출 코드에서 `Seed` 모든 마이그레이션 후 메서드와이 메서드는 이미 삽입 되었거나 아직 없는 경우 삽입 된 행을 업데이트 합니다. `AddOrUpdate` 메서드 시나리오에 대 한 최상의 선택이 아닐 수 있습니다. 자세한 내용은 참조 [EF 4.3 AddOrUpdate 메서드로 주의](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) Julie Lerman 블로그.


CTRL-SHIFT-B를 눌러 프로젝트를 빌드합니다.

다음 단계를 만드는 것을 `DbMigration` 초기 마이그레이션에 대 한 클래스입니다. 만드는 새 데이터베이스에 이미 존재 하는 데이터베이스를 삭제 해야이 마이그레이션을 사용 하는 것이 좋습니다. SQL Server Compact 데이터베이스에 포함 된 *.sdf* 파일에 *앱\_데이터* 폴더입니다. **솔루션 탐색기**를 확장 하 고 *앱\_데이터* 나타내는 두 개의 SQL Server Compact 데이터베이스를 보려면 ContosoUniversity 프로젝트에서 *.sdf*파일입니다.

마우스 오른쪽 단추로 클릭는 *School.sdf* 파일을 클릭 하 여 **삭제**합니다.

![sdf_files_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image10.png)

에 **패키지 관리자 콘솔** 창 "추가 마이그레이션 초기" 명령을 입력를 초기 마이그레이션 만들고 "초기" 라는 이름을 지정 합니다.

![추가 migration_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image11.png)

Code First 마이그레이션을에 다른 클래스 파일을 만듭니다는 *마이그레이션* 폴더에 있으며,이 클래스는 데이터베이스 스키마를 만드는 코드를 포함 합니다.

에 **패키지 관리자 콘솔**, 명령 "업데이트-데이터베이스 입력" 데이터베이스를 만들고 실행 하는 **시드** 메서드.

![업데이트 database_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image12.png)

(테이블 이미 있으며 만들 수를 나타내는 오류가 발생할 경우 때문일 것 데이터베이스 삭제 되 고 실행 하기 전에 응용 프로그램을 실행 `update-database`합니다. 그런, 삭제는 *School.sdf* 파일을 다시 시도 `update-database` 명령입니다.)

응용 프로그램을 실행합니다. 이제 학생 페이지가 비어 있지만 강사 페이지 강사를 포함 합니다. 이 생성 됩니다 프로덕션에서 응용 프로그램을 배포한 후입니다.

![Empty_Students_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image13.png)

![Instructors_page_after_initial_migration](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image14.png)

이제 프로젝트를 배포할 준비가 된 *학교* 데이터베이스입니다.

## <a name="creating-a-membership-database-for-deployment"></a>배포에 대 한 멤버 자격 데이터베이스 만들기

Contoso 대학교 응용 프로그램 ASP.NET 멤버 자격 시스템 및 폼 인증을 사용 하 여 인증 하 고 사용자 권한을 부여 합니다. 해당 페이지 중 하나는 관리자만 액세스할 수 있습니다. 이 페이지를 보려면 응용 프로그램을 실행 하 고 선택 **업데이트 크레딧** 플라이 아웃 메뉴 아래 **Courses**합니다. 표시 됩니다는 **로그인** 만 관리자가 사용할 수 있는 때문에 페이지는 **업데이트 크레딧** 페이지.

[![Log_in_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image15.png)

"Admin" 암호 "Pa$ w0rd"를 사용 하 여로 로그인 ("w0rd"에서 문자 "o" 대신 숫자 0 확인). 로그인 한 후는 **업데이트 크레딧** 페이지가 표시 됩니다.

[![Update_Credits_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image17.png)

처음으로 사이트를 배포 하는 경우에 테스트를 위해 생성 하는 사용자 계정의 전체 또는 대부분을 제외 하려면 일반적입니다. 이 경우 관리자 계정 및 사용자 계정이 배포할 수 있습니다. 테스트 계정을 수동으로 삭제 하는 대신 새 멤버 자격 데이터베이스를 프로덕션 환경에서 필요로 하는 한 명의 관리자 사용자 계정 으로만 만듭니다.

> [!NOTE]
> 멤버 자격 데이터베이스 계정 암호의 해시를 저장 합니다. 한 컴퓨터에서 계정을 배포 하려면 원본 컴퓨터에서 보다 해시 루틴이 대상 서버에서 다른 해시를 생성 하지 않아도 되어 있는지 확인 해야 합니다. 생성 합니다 동일한 해시 ASP.NET Universal Providers를 사용 하는 경우 기본 알고리즘을 변경 하지 않는 상태로 있습니다. 기본 알고리즘 HMACSHA256 이며에 지정 된는 **유효성 검사** 특성에는  **[machineKey](https://msdn.microsoft.com/en-us/library/w8h3skw9.aspx)**  Web.config 파일의 요소입니다.


멤버 자격 데이터베이스는 Code First 마이그레이션을 통해 유지 되지 않습니다 되며 (이므로 School 데이터베이스에 대 한) 테스트 계정 사용 하 여 데이터베이스를 시드하 자동 이니셜라이저 없습니다. 따라서 사용할 수 있는 테스트 데이터를 유지 하려면 지정 테스트 데이터베이스의 복사본을 새를 만들기 전에 합니다.

**솔루션 탐색기**, 이름 바꾸기는 *aspnet.sdf* 파일에 *앱\_데이터* 폴더를 *aspnet Dev.sdf*합니다. (복사 하지 않습니다, 방금 이름 바꾸기-잠시 후에 새 데이터베이스를 만듭니다.)

**솔루션 탐색기**, 웹 프로젝트 (ContosoUniversity, 하지 ContosoUniversity.DAL)이 선택 되어 있는지 확인 합니다. 그런 다음는 **프로젝트** 메뉴 선택 **ASP.NET 구성** 실행 하는 **웹 사이트 관리 도구**(WAT).

선택 된 **보안** 탭 합니다.

[![WAT_Security_tab](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image19.png)

클릭 **만들기 또는 역할 관리** 추가 **관리자** 역할입니다.

[![WAT_Create_New_Role](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image21.png)

로 돌아가 **보안** 탭을 클릭 **Create User**, "admin" 사용자를 관리자로 추가 합니다. 클릭 하기 전에 **Create User** 단추는 **사용자 만들기** 페이지에서 선택 해야는 **관리자** 확인란 합니다. 이 자습서에 사용 되는 암호 "Pa$ w0rd" 이며 모든 전자 메일 주소를 입력할 수 있습니다.

[![WAT_Create_User](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image23.png)

브라우저를 닫습니다. **솔루션 탐색기**, 새로 고침 단추를 클릭 새 볼 *aspnet.sdf* 파일입니다.

![New_aspnet.sdf_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image25.png)

마우스 오른쪽 단추로 클릭 **aspnet.sdf** 선택 **프로젝트에 포함**합니다.

## <a name="distinguishing-development-from-production-databases"></a>프로덕션 데이터베이스에서 개발 구별

이 섹션에서는 개발 버전 학교 Dev.sdf 있고 aspnet Dev.sdf 및 프로덕션 버전은 학교 Prod.sdf 및 aspnet Prod.sdf 않도록 데이터베이스를 이름을 바꿀 합니다. 이 필요는 없지만 이렇게 하면 지금 됩니다 유지할 수 있도록 테스트 및 프로덕션 버전의 데이터베이스에 혼란 수 없도록 합니다.

**솔루션 탐색기**, 클릭 **새로 고침** 응용 프로그램을 확장 하 고\_앞에서 만든 School 데이터베이스를 참조 하 고; 단추로 클릭 한 다음 선택 데이터 폴더 **프로젝트에 포함** .

![Including_School.sdf_in_project](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image26.png)

이름 바꾸기 *aspnet.sdf* 를 *aspnet Prod.sdf*합니다.

이름 바꾸기 *School.sdf* 를 *학교 Dev.sdf*합니다.

사용 하려면 Visual Studio에서 응용 프로그램을 실행 하는 *-Prod* 사용 하려는 버전의 데이터베이스 파일을 *-Dev* 버전입니다. 따라서를 가리키도록 Web.config 파일에서 연결 문자열을 변경 해야는 *-Dev* 버전의 데이터베이스입니다. (학교 Prod.sdf 파일을 만들지 않은 있지만 확인은 Code First 해당에 데이터베이스를 만드는 첫 번째 프로덕션 시간 있는 앱을 실행 하기 때문).

응용 프로그램 Web.config 파일을 열고 연결 문자열을 찾습니다.

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample5.xml)]

"Aspnet-Dev.sdf"를 "aspnet.sdf" 이동한 "School.sdf" "학교 Dev.sdf"로 변경 합니다.

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample6.xml?highlight=4-5)]

SQL Server Compact 데이터베이스 엔진 및 두 데이터베이스를 배포할 준비가 됩니다. 다음 자습서에서 설정한 자동 *Web.config* 개발, 테스트 및 프로덕션 환경에서 달라 야 하는 설정에 대 한 변환 파일입니다. (변경 해야 하는 설정 중 연결 문자열에는 있지만를 설정 변경 내용을 나중에 게시 프로필을 만들 때).

## <a name="more-information"></a>추가 정보

NuGet에 대 한 자세한 내용은 참조 하십시오. [NuGet이 포함 된 프로젝트 라이브러리가 관리](https://msdn.microsoft.com/en-us/magazine/hh547106.aspx) 및 [NuGet 설명서](http://docs.nuget.org/docs/start-here/overview)합니다. NuGet을 사용 하지 않으려면 설치 될 때 역할을 결정 하는 NuGet 패키지를 분석 하는 방법에 알아보려면 해야 합니다. (구성할 수는 예를 들어 *Web.config* 변환 등 빌드 시간에 실행 되도록 PowerShell 스크립트를 구성 합니다.) NuGet의 작동 방식에 대 한 자세한 내용은 참조 특히 [만들기 및 게시 패키지](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package) 및 [구성 파일 및 소스 코드 변환](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations)합니다.

>[!div class="step-by-step"]
[이전](deployment-to-a-hosting-provider-introduction-1-of-12.md)
[다음](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
