---
uid: web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 배포 데이터베이스에 대 한 준비 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: ae4def81-fa37-4883-a13e-d9896cbf6c36
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
msc.type: authoredcontent
ms.openlocfilehash: 21b4a924115daff6ee79ce045330c748b58246ee
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388542"
---
<a name="aspnet-web-deployment-using-visual-studio-preparing-for-database-deployment"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 배포 데이터베이스에 대 한 준비
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다. 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.


## <a name="overview"></a>개요

이 자습서 데이터베이스 배포용으로 준비 프로젝트를 가져오는 방법을 보여줍니다. 데이터베이스의 구조와 일부 (모두는 아님) 응용 프로그램의 두 데이터의 데이터베이스 테스트, 스테이징 및 프로덕션 환경에 배포 되어야 합니다.

일반적으로 응용 프로그램을 개발할 때는 테스트 데이터는 라이브 사이트에 배포 하지 않으려는 데이터베이스를 입력 합니다. 그러나 수도 있습니다는 배포 하려는 일부 프로덕션 데이터입니다. 이 자습서에서는 Contoso University 프로젝트를 구성 하 고 배포 하는 경우 올바른 데이터가 포함 되도록 SQL 스크립트를 준비 합니다.

미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](troubleshooting.md)합니다.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

샘플 응용 프로그램에서는 SQL Server Express LocalDB를 사용합니다. SQL Server Express는 SQL Server의 무료 버전입니다. SQL Server의 전체 버전으로 같은 데이터베이스 엔진을 기반으로 하므로 일반적으로 개발 하는 동안 사용 됩니다. SQL Server express 테스트할 수 있으며, SQL Server 버전 간에 달라 지는 기능에 대 한 몇 가지 예외를 사용 하 여 프로덕션 환경에서 동일한 응용 프로그램 동작는 보장할 수 있습니다.

LocalDB 데이터베이스를 사용 하 여 작업할 수 있도록 하는 SQL Server Express의 특수 하 게 실행 모드가 *.mdf* 파일입니다. 일반적으로, LocalDB 데이터베이스 파일에 보관 되는 *앱\_데이터* 웹 프로젝트의 폴더입니다. SQL Server express 사용자 인스턴스 기능 또한 작업할 수 있습니다 *.mdf* 파일을 하지만 사용자 인스턴스 기능 사용 되지 않으면 따라서 LocalDB가 사용 하기 위한 권장 *.mdf* 파일입니다.

일반적으로 SQL Server Express 프로덕션 웹 응용 프로그램에 대 한 사용 되지 않습니다. LocalDB 특히 권장 되지 않습니다 프로덕션 웹 응용 프로그램을 사용 하므로 IIS와 함께 작동 하도록 설계 되지는 않았습니다.

Visual Studio 2012의 Visual Studio를 사용 하 여 기본적으로 LocalDB는 설치 됩니다. Visual Studio 2010 및 이전 버전의 Visual Studio를 사용 하 여 기본적으로 설치 됩니다 (LocalDB) 없이 SQL Server Express 필수 구성 요소 중 하나로 설치 이유 즉 [이 시리즈의 첫 번째 자습서](introduction.md)합니다.

LocalDB를 비롯 한 SQL Server 버전에 대 한 자세한 내용은 다음 리소스를 참조 [SQL Server 데이터베이스를 사용 하 여 작업](../../../../whitepapers/aspnet-data-access-content-map.md#sqlserver)합니다.

## <a name="entity-framework-and-universal-providers"></a>Entity Framework 및 범용 공급자

데이터베이스 액세스를 위한 Contoso University 응용 프로그램에.NET Framework에 포함 되어 있지 않으므로 응용 프로그램을 사용 하 여 배포 해야 하는 다음 소프트웨어가 필요 합니다.

- [ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) (Azure SQL Database를 사용 하는 ASP.NET 멤버 자격 수 있음)
- [Entity Framework](https://msdn.microsoft.com/library/gg696172.aspx)

이 소프트웨어는 NuGet 패키지에 포함 되므로, 프로젝트가 이미 설정 되어 필요한 어셈블리 프로젝트를 사용 하 여 배포 됩니다. (링크는이 자습서에 대 한 다운로드 한 시작 프로젝트에 설치 된 것 보다 새로운 버전일 수 있습니다 이러한 패키지의 현재 버전을 가리킵니다.)

Azure가 아닌 타사 호스팅 공급자에 배포 하는 경우 Entity Framework 5.0 이상을 사용 하는 있는지 확인 합니다. 이전 버전의 Code First 마이그레이션을 완전 신뢰 하며 대부분의 호스팅 공급자는 보통 신뢰 응용 프로그램을 실행 합니다. 보통 신뢰 하는 방법에 대 한 자세한 내용은 참조는 [iis 테스트 환경으로 배포](deploying-to-iis.md) 자습서입니다.

## <a name="configure-code-first-migrations-for-application-database-deployment"></a>응용 프로그램 데이터베이스 배포에 대 한 Code First 마이그레이션을 구성합니다

Code First 마이그레이션을 사용 하 여 배포한와 Contoso University 응용 프로그램 데이터베이스는 Code First에서 관리 됩니다. Code First 마이그레이션을 사용 하 여 데이터베이스 배포의 개요를 보려면 [이 시리즈의 첫 번째 자습서](introduction.md)합니다.

응용 프로그램 데이터베이스를 배포할 때 일반적으로 하지 단순히에 데이터를 모두 사용 하 여 개발 데이터베이스를 프로덕션에 배포할 이므로 대부분의 데이터에 있는 아마도 테스트용 으로만 합니다. 예를 들어, 학생 이름을 테스트 데이터베이스에는 가상입니다. 반면, 자주 배포할 수 없습니다에 데이터가 없는 데이터베이스 구조만 전혀 합니다. 테스트 데이터베이스에 있는 데이터의 일부 실제 데이터를 사용할 수 있으며 사용자가 응용 프로그램을 사용 하기 시작 하는 경우 있습니다 여야 합니다. 예를 들어 데이터베이스 유효한 등급 값 또는 실제 부서 이름을 포함 하는 테이블이 있다고 가정 합니다.

이 일반적인 시나리오를 시뮬레이션 하려면 Code First 마이그레이션을 구성 `Seed` 데이터베이스에 있는 프로덕션 환경에서 원하는 데이터만 삽입 하는 메서드. DAL 프로젝트를 선택 합니다 `Seed`기본 프로젝트 드롭 다운 목록을 합니다 패키지 관리자 콘솔 때문에  Code First를 포함 하는 프로젝트에서 명령을 실행 해야 컨텍스트 클래스입니다.

해당 클래스는 클래스 라이브러리 프로젝트의 경우 Code First 마이그레이션 솔루션에 대 한 시작 프로젝트에서 데이터베이스 연결 문자열을 찾습니다. ContosoUniversity 솔루션에서 웹 프로젝트를 시작 프로젝트로 설정한 합니다. Visual Studio에서 시작 프로젝트와 연결 문자열을 포함 하는 프로젝트를 지정 하지 않으려는 경우에 PowerShell 명령에서 시작 프로젝트를 지정할 수 있습니다. 명령 구문을 보려면에서 명령을 입력 `enable Migrations. Then you'll update the `합니다.

데이터베이스가 이미 있기 때문에 자동으로 명령을 첫 번째 마이그레이션을 생성 합니다.

[![School_database_diagram](preparing-databases/_static/image2.png)](preparing-databases/_static/image1.png)

대 안으로 마이그레이션 데이터베이스를 만듭니다. 이렇게 하려면 사용 하 여 서버 탐색기 하거나 SQL Server 개체 탐색기 마이그레이션을 사용 하기 전에 ContosoUniversity 데이터베이스를 삭제 하려면.

### <a name="disable-the-initializer"></a>마이그레이션을 사용 하도록 설정 하면 첫 번째 마이그레이션 수동으로 만들 "추가 마이그레이션 InitialCreate" 명령을 입력 하 여.

다음 명령은 "-데이터베이스 업데이트"를 입력 하 여 데이터베이스를 만들 수 있습니다. Seed 메서드 설정 이 자습서에 대 한 코드를 추가 하 여 고정된 데이터가 추가 됩니다는 `appSettings` Code First 마이그레이션을 메서드의 * 클래스입니다.

[!code-xml[Main](preparing-databases/samples/sample1.xml?highlight=3)]

첫 번째 마이그레이션을 호출 코드는 * 모든 마이그레이션 후 메서드. 이후는 `appSettings` 모든 마이그레이션 후 실행 되는 메서드, 데이터가 이미 테이블의 첫 번째 마이그레이션 후 합니다.

[!code-xml[Main](preparing-databases/samples/sample2.xml)]

> [!NOTE]
> 사용 하 여이 상황을 처리 하는 `Database.SetInitializer` 아직 없는 경우 삽입 하거나 이미 삽입 된 행을 업데이트 하는 방법입니다. 메서드 시나리오에 가장 적합 한 되지 않을 수 있습니다.


> [!NOTE]
> 자세한 내용은 EF 4.3 AddOrUpdate 메서드를 사용 하 여 주의 Julie Lerman의 블로그입니다. 엽니다는 Configuration.cs 에 있는 메모를 바꾸고 파일을  메서드를 다음 코드로: 에 대 한 참조  필요가 없기 때문에 그 아래에 있는 빨간색의 구불구불한 선이는  아직 문을 해당 네임 스페이스에 대 한 합니다.


### <a name="enable-code-first-migrations"></a>인스턴스 중 하나를 마우스 오른쪽 단추로 클릭  을 클릭 해결를 클릭 하 고 System.Collections.Generic를 사용 하 여입니다.

1. 문을 사용 하 여 해결 다음 코드를 추가 하는이 메뉴를 선택 합니다 ** 문을 파일의 맨 위 근처 합니다. 프로젝트를 빌드하려면 CTRL-SHIFT-B를 누릅니다.
2. 이제 프로젝트를 배포할 준비가 된 **ContosoUniversity** 데이터베이스입니다.

    ![Selecting_Package_Manager_Console](preparing-databases/_static/image3.png)
3. 배포 응용 프로그램을 처음 실행 하 고 데이터베이스에 액세스 하는 페이지로 이동 하 고 나면 Code First는 데이터베이스를 만들고 실행 ** 메서드.

    ![코드를 추가 합니다  메서드는 데이터베이스에 고정된 데이터를 삽입할 수 있는 여러 가지 방법 중 하나입니다.](preparing-databases/_static/image4.png)

    대안은 코드를 추가 하는 *고* 각 마이그레이션 클래스의 메서드.

    합니다 *고* 메서드는 데이터베이스 변경 내용을 구현 하는 코드를 포함 합니다.

    ![예제에 표시 합니다 데이터베이스 업데이트 배포 자습서입니다.](preparing-databases/_static/image5.png)

    사용 하 여 SQL 문을 실행 하는 코드를 작성할 수도 있습니다는 ** 메서드. 예를 들어, 예산 열 Department 테이블을 추가 했습니다 하는 마이그레이션의 일환으로 모든 부서 예산을 $ 1, 000.00를 초기화 하려는 경우 다음 줄의 코드를 추가할 수는  마이그레이션에 대 한 메서드: 멤버 자격 데이터베이스 배포를 위한 스크립트 만들기 Contoso University 응용 프로그램 인증 및 사용자 권한 부여는 ASP.NET 멤버 자격 시스템 및 폼 인증을 사용 합니다. 합니다 `get-help enable-migrations`업데이트 크레딧 페이지는 관리자 역할이 있는 사용자만 액세스할 수 있습니다.

    응용 프로그램을 실행 하 고 클릭 `enable-migrations`코스를 클릭 하 고 업데이트 크레딧합니다. 업데이트 크레딧을 클릭 합니다. **에 로그인** 때문에 페이지가 표시 됩니다는 **업데이트 크레딧** 페이지 관리 권한이 필요 합니다. 입력 admin 사용자 이름으로 및 devpwd 암호와 클릭 로그인합니다. 로그인 페이지

### <a name="set-up-the-seed-method"></a>합니다 업데이트 크레딧 페이지가 나타납니다.

크레딧 페이지 업데이트 사용자 및 역할 정보를 `Seed`aspnet ContosoUniversity 하 여 지정 된 데이터베이스에는 DefaultConnection 에서 연결 문자열을 Web.config 파일.

이 데이터베이스는 Entity Framework Code First에서 관리 되지 배포 마이그레이션을 사용할 수 없습니다. 데이터베이스 스키마를 배포 하려면 dbDacFx 공급자 사용 및 데이터베이스 테이블에 초기 데이터를 삽입 하는 스크립트를 실행 하려면 게시 프로필을 구성 합니다. 새 ASP.NET 멤버 자격 시스템 (이제 ASP.NET Id 라고 함)는 Visual Studio 2013을 사용 하 여 도입 되었습니다. 새 시스템을 사용 하면 응용 프로그램 및 멤버 자격 테이블을 모두 동일한 데이터베이스에 유지 하 고 Code First 마이그레이션을 사용 하 여 모두를 배포 하 합니다.

1. Code First 마이그레이션을 사용 하 여 배포할 수 없습니다는 이전 ASP.NET 멤버 자격 시스템을 사용 하는 샘플 응용 프로그램입니다.

    [!code-csharp[Main](preparing-databases/samples/sample3.cs)]
2. 이 멤버 자격 데이터베이스를 배포 하는 절차는 응용 프로그램이 Entity Framework Code First에서 만들어지지 있는 SQL Server 데이터베이스를 배포 해야 하는 다른 모든 시나리오에도 적용 됩니다. 여기도 일반적으로 원하지 개발에서 해야 하는 프로덕션 환경에서 동일한 데이터입니다.

    ![처음으로 사이트를 배포 하 때 대부분 또는 모든 테스트를 위해 만든 사용자 계정을 제외에 공통적으로 적용 합니다.](preparing-databases/_static/image6.png)

    따라서 다운로드 한 프로젝트에 두 개의 멤버 자격 데이터베이스: `using`aspnet ContosoUniversity.mdf 개발 사용자를 사용 하 여 및 aspnet-ContosoUniversity-Prod.mdf 프로덕션 사용자를 사용 하 여 합니다.

    [!code-csharp[Main](preparing-databases/samples/sample4.cs)]
3. 이 자습서에 대 한 사용자 이름을 동일 두 데이터베이스 모두에: admin 하 고 nonadmin합니다.

두 명의 암호 *devpwd* 개발 데이터베이스에서 및 prodpwd 프로덕션 데이터베이스에 있습니다. 개발 사용자 테스트 환경 및 사용자에 게는 프로덕션 스테이징 및 프로덕션에 배포 합니다.

> [!NOTE]
> 이렇게 하려면이 자습서에서 개발 및 프로덕션 환경에 대해 하나씩 두 개의 SQL 스크립트를 만들어야 하 고 나중에 자습서에서 실행 하는 게시 프로세스를 구성 합니다. 멤버 자격 데이터베이스 계정 암호의 해시를 저장 합니다. 다른 컴퓨터에서 계정에 배포 하려면 원본 컴퓨터에서 수행할 때 보다 해시 루틴이 대상 서버의 다른 해시를 생성 하지 않도록 해야 합니다. 생성 동일한 해시 ASP.NET Universal Providers를 사용 하는 경우 기본 알고리즘을 변경 하지 않으면으로 합니다.
> 
> 기본 알고리즘 HMACSHA256 이며에 지정 된를 `Sql`유효성 검사 특성을  machineKey  Web.config 파일의 요소입니다. SQL Server Management Studio (SSMS)를 사용 하 여 또는 타사 도구를 사용 하 여 데이터 배포 스크립트를 수동으로 만들 수 있습니다.
> 
> `Sql("UPDATE Department SET Budget = 1000");`


## <a name="create-scripts-for-membership-database-deployment"></a>이 자습서의 나머지이 부분은 SSMS에서 수행 하는 방법을 표시 되지만 설치 하 고 SSMS를 사용 하지 않을 경우에 프로젝트의 완성된 된 버전에서 스크립트를 가져올 고 저장할 해당 솔루션 폴더에서 섹션을 건너뛸 수 있습니다.

에 데이터베이스 연결 대화 상자에서 클릭 추가 로 이동한 다음를 aspnet-ContosoUniversity-Prod.mdf 파일을 앱 데이터 폴더입니다. .Mdf 파일 연결을 추가 하는 SSMS

프로덕션 파일에 대 한 스크립트를 만들려면 이전에 사용한 동일한 절차를 따릅니다.

![스크립트 파일의 이름을 aspnet-데이터-prod.sql합니다.](preparing-databases/_static/image7.png)

두 데이터베이스를 배포할 준비가 됩니다 하 고 솔루션 폴더에 두 개의 데이터 배포 스크립트를 해야 합니다.

데이터 배포 스크립트

![다음 자습서에서는 배포에 영향을 주는 프로젝트 설정을 구성 하 고 자동 설정한 Web.config 파일은 배포 된 응용 프로그램에서 서로 달라 야 하는 설정에 대 한 변환 합니다.](preparing-databases/_static/image8.png)

NuGet에 대 한 자세한 내용은 참조 하세요. **NuGet 사용 하 여 프로젝트 라이브러리 관리** 하 고 NuGet 설명서합니다.

![NuGet을 사용 하지 않으려는 경우 설치 될 때 무엇을 확인 하는 NuGet 패키지를 분석 하는 방법을 알아보려면 해야 합니다.](preparing-databases/_static/image9.png)

(예를 들어 구성할 수 있습니다 *Web.config* 변환 등 빌드 시간에 실행 하도록 PowerShell 스크립트를 구성 합니다.)

NuGet의 작동 원리에 대 한 자세한 내용은를 참조 하세요. 는 패키지 만들기 및 게시 하 고 구성 파일 및 소스 코드 변환합니다. 데이터베이스 스키마를 배포 하려면 dbDacFx 공급자 사용 및 데이터베이스 테이블에 초기 데이터를 삽입 하는 스크립트를 실행 하려면 게시 프로필을 구성 합니다.

> [!NOTE]
> 새 ASP.NET 멤버 자격 시스템 (이제 ASP.NET Id 라고 함)는 Visual Studio 2013을 사용 하 여 도입 되었습니다. 새 시스템을 사용 하면 응용 프로그램 및 멤버 자격 테이블을 모두 동일한 데이터베이스에 유지 하 고 Code First 마이그레이션을 사용 하 여 모두를 배포 하 합니다. Code First 마이그레이션을 사용 하 여 배포할 수 없습니다는 이전 ASP.NET 멤버 자격 시스템을 사용 하는 샘플 응용 프로그램입니다. 이 멤버 자격 데이터베이스를 배포 하는 절차는 응용 프로그램이 Entity Framework Code First에서 만들어지지 있는 SQL Server 데이터베이스를 배포 해야 하는 다른 모든 시나리오에도 적용 됩니다.


여기도 일반적으로 원하지 개발에서 해야 하는 프로덕션 환경에서 동일한 데이터입니다. 처음으로 사이트를 배포 하 때 대부분 또는 모든 테스트를 위해 만든 사용자 계정을 제외에 공통적으로 적용 합니다. 따라서 다운로드 한 프로젝트에 두 개의 멤버 자격 데이터베이스: *aspnet ContosoUniversity.mdf* 개발 사용자를 사용 하 여 및 *aspnet-ContosoUniversity-Prod.mdf* 프로덕션 사용자를 사용 하 여 합니다. 이 자습서에 대 한 사용자 이름을 동일 두 데이터베이스 모두에: *admin* 하 고 *nonadmin*합니다. 두 명의 암호 *devpwd* 개발 데이터베이스에서 및 *prodpwd* 프로덕션 데이터베이스에 있습니다.

개발 사용자 테스트 환경 및 사용자에 게는 프로덕션 스테이징 및 프로덕션에 배포 합니다. 이렇게 하려면이 자습서에서 개발 및 프로덕션 환경에 대해 하나씩 두 개의 SQL 스크립트를 만들어야 하 고 나중에 자습서에서 실행 하는 게시 프로세스를 구성 합니다.

> [!NOTE]
> 멤버 자격 데이터베이스 계정 암호의 해시를 저장 합니다. 다른 컴퓨터에서 계정에 배포 하려면 원본 컴퓨터에서 수행할 때 보다 해시 루틴이 대상 서버의 다른 해시를 생성 하지 않도록 해야 합니다. 생성 동일한 해시 ASP.NET Universal Providers를 사용 하는 경우 기본 알고리즘을 변경 하지 않으면으로 합니다. 기본 알고리즘 HMACSHA256 이며에 지정 된를 **유효성 검사** 특성을 **[machineKey](https://msdn.microsoft.com/library/system.web.configuration.machinekeysection.aspx)** Web.config 파일의 요소입니다.


SQL Server Management Studio (SSMS)를 사용 하 여 또는 타사 도구를 사용 하 여 데이터 배포 스크립트를 수동으로 만들 수 있습니다. 이 자습서의 나머지이 부분은 SSMS에서 수행 하는 방법을 표시 되지만 설치 하 고 SSMS를 사용 하지 않을 경우에 프로젝트의 완성된 된 버전에서 스크립트를 가져올 고 저장할 해당 솔루션 폴더에서 섹션을 건너뛸 수 있습니다.

SSMS를 설치 하려면에서 설치할 [다운로드 센터: Microsoft SQL Server 2012 Express](https://www.microsoft.com/download/details.aspx?id=29062) 를 클릭 하 여 [ENU\x64\SQLManagementStudio\_x64\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLManagementStudio_x64_ENU.exe) 또는 [ ENU\x86\SQLManagementStudio\_x86\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLManagementStudio_x86_ENU.exe)합니다. 잘못 된 것을 선택 하면 시스템에 대 한 설치에 실패 합니다 하 고 다른 하나를 시도할 수 있습니다.

(이 600 메가바이트 다운로드 note 합니다. 시간이 오래 걸릴 수 있습니다를 설치 하 고 컴퓨터를 다시 부팅 해야 합니다.)

SQL Server 설치 센터의 첫 번째 페이지에서 클릭 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**, 기본 선택 항목을 수락 하는 지침을 따릅니다.

### <a name="create-the-development-database-script"></a>개발 데이터베이스 스크립트를 만들려면

1. SSMS를 실행 합니다.
2. 에 **서버에 연결** 대화 상자에 입력 합니다 *(localdb) \v11.0* 으로 **서버 이름**, 둡니다 **인증** 로**Windows 인증**를 클릭 하 고 **Connect**합니다.

    ![SSMS는 서버에 연결](preparing-databases/_static/image10.png)
3. 에 **개체 탐색기** 창 확장 **데이터베이스**를 마우스 오른쪽 단추로 클릭 **aspnet ContosoUniversity**, 클릭 **작업**를 클릭 하 고 **스크립트 생성**합니다.

    ![SSMS 스크립트 생성](preparing-databases/_static/image11.png)
4. 에 **스크립트 생성 및 게시** 대화 상자, 클릭 **스크립팅 옵션 설정**합니다.

    건너뛸 수 있습니다 합니다 **개체 선택** 기본값 이므로 단계 **전체 데이터베이스 및 모든 데이터베이스 개체 스크립팅** 원하는 것입니다.
5. **고급**을 클릭합니다.

    ![SSMS 스크립팅 옵션](preparing-databases/_static/image12.png)
6. 에 **고급 스크립팅 옵션** 대화 상자에서 아래쪽으로 스크롤하여 **스크립팅할 데이터 형식**, 클릭 하 고는 **데이터만** 드롭 다운 목록에서 옵션.
7. 변경 **USE DATABASE 스크립팅** 하 **False**합니다. 사용 하 여 Azure SQL Database에 대 한 유효 하지 문과 테스트 환경에서 SQL Server Express에 대 한 배포에 대 한 필요 하지 않습니다.

    ![SSMS 스크립트 데이터만 사용 하 여 문이 없는](preparing-databases/_static/image13.png)
8. **확인**을 클릭합니다.
9. 에 **스크립트 생성 및 게시** 대화 상자를 **파일 이름** 상자 스크립트를 생성 하는 위치를 지정 합니다. 솔루션 폴더 (ContosoUniversity.sln 파일에 있는 폴더)를 파일 이름에 경로 변경 *aspnet-데이터-dev.sql*합니다.
10. 클릭 **다음** 로 이동 하는 **요약** 탭을 클릭 한 다음 **다음** 스크립트를 만들려면 다시 합니다.

    ![SSMS 스크립트 생성](preparing-databases/_static/image14.png)
11. **마침**을 클릭합니다.

### <a name="create-the-production-database-script"></a>프로덕션 데이터베이스 스크립트를 만들려면

프로덕션 데이터베이스를 사용 하 여 프로젝트를 실행 하지 않은 이므로 LocalDB 인스턴스에 아직 연결 되지 않았습니다. 따라서 데이터베이스를 먼저 연결 해야 합니다.

1. Ssms에서 **개체 탐색기**를 마우스 오른쪽 단추로 클릭 **데이터베이스** 누릅니다 **연결**합니다.

    ![SSMS 연결](preparing-databases/_static/image15.png)
2. 에 **데이터베이스 연결** 대화 상자에서 클릭 **추가** 로 이동한 다음를 *aspnet-ContosoUniversity-Prod.mdf* 파일을 *앱\_ 데이터* 폴더입니다.

     ![.Mdf 파일 연결을 추가 하는 SSMS](preparing-databases/_static/image16.png)
3. **확인**을 클릭합니다.
4. 프로덕션 파일에 대 한 스크립트를 만들려면 이전에 사용한 동일한 절차를 따릅니다. 스크립트 파일의 이름을 *aspnet-데이터-prod.sql*합니다.

## <a name="summary"></a>요약

두 데이터베이스를 배포할 준비가 됩니다 하 고 솔루션 폴더에 두 개의 데이터 배포 스크립트를 해야 합니다.

![데이터 배포 스크립트](preparing-databases/_static/image17.png)

다음 자습서에서는 배포에 영향을 주는 프로젝트 설정을 구성 하 고 자동 설정한 *Web.config* 파일은 배포 된 응용 프로그램에서 서로 달라 야 하는 설정에 대 한 변환 합니다.

## <a name="more-information"></a>추가 정보

NuGet에 대 한 자세한 내용은 참조 하세요. [NuGet 사용 하 여 프로젝트 라이브러리 관리](https://msdn.microsoft.com/magazine/hh547106.aspx) 하 고 [NuGet 설명서](http://docs.nuget.org/docs/start-here/overview)합니다. NuGet을 사용 하지 않으려는 경우 설치 될 때 무엇을 확인 하는 NuGet 패키지를 분석 하는 방법을 알아보려면 해야 합니다. (예를 들어 구성할 수 있습니다 *Web.config* 변환 등 빌드 시간에 실행 하도록 PowerShell 스크립트를 구성 합니다.) NuGet의 작동 원리에 대 한 자세한 내용은를 참조 하세요. [는 패키지 만들기 및 게시](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package) 하 고 [구성 파일 및 소스 코드 변환](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations)합니다.

> [!div class="step-by-step"]
> [이전](introduction.md)
> [다음](web-config-transformations.md)
