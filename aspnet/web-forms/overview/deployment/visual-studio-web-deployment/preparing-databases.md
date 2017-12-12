---
uid: web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
title: "Visual Studio를 사용 하 여 ASP.NET 웹 배포: 배포 데이터베이스에 대 한 준비 | Microsoft Docs"
author: tdykstra
description: "이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) 실행 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: ae4def81-fa37-4883-a13e-d9896cbf6c36
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
msc.type: authoredcontent
ms.openlocfilehash: 1f19d54a5f2679f790575d520b28472d4ff3233f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-web-deployment-using-visual-studio-preparing-for-database-deployment"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 데이터베이스 배포 준비
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자입니다. 계열에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](introduction.md)합니다.


## <a name="overview"></a>개요

이 자습서에서는 프로젝트를 가져오는 방법을 데이터베이스 배포에 대해 준비 합니다. 데이터베이스의 구조와 일부 (모두는 아님) 응용 프로그램의 두에 있는 데이터의 데이터베이스 테스트, 스테이징 및 프로덕션 환경에 배포 해야 합니다.

일반적으로 응용 프로그램을 개발할 때 테스트 데이터 라이브 사이트에 배포 하지 않으려는 데이터베이스를 입력 합니다. 그러나 프로덕션 데이터를 배포 하려는 할 수 있습니다. 이 자습서에서는 Contoso 대학 프로젝트를 구성 하 고 배포할 때 올바른 데이터가 포함 되도록 SQL 스크립트를 준비 합니다.

미리 알림: 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 반드시 확인는 [문제 해결 페이지](troubleshooting.md)합니다.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

샘플 응용 프로그램이 SQL Server Express LocalDB를 사용 합니다. SQL Server Express는 SQL Server의 무료 버전입니다. 전체 버전의 SQL Server로 동일한 데이터베이스 엔진을 기반으로 하므로 일반적으로 개발 하는 동안 사용 됩니다. SQL Server Express와 함께 테스트할 수 있으며, 응용 프로그램이 SQL Server 버전 간에 달라 지는 기능에 대 한 몇 가지 예외 프로덕션 환경에서 동일 하 게 동작 합니다을 보장할 수 있습니다.

LocalDB는 SQL Server express 데이터베이스도 작업할 수 있도록 하는 특별 한 실행 모드가 *.mdf* 파일입니다. LocalDB 데이터베이스 파일에 보관 되는 일반적으로 *앱\_데이터* 웹 프로젝트의 폴더입니다. SQL Server express 사용자 인스턴스 기능 또한 작업할 수 있습니다 *.mdf* 은 사용자 인스턴스 기능은 사용 되지 않습니다; 따라서 LocalDB를 사용 하기 위한 좋습니다 *.mdf* 파일입니다.

일반적으로 SQL Server Express 프로덕션 웹 응용 프로그램에 대 한 사용 되지 않습니다. LocalDB 특히 권장 되지 않습니다 웹 응용 프로그램의 프로덕션 사용을 위해 하므로 IIS와 함께 작동 하도록 설계 되지 않았습니다.

Visual Studio 2012에서 LocalDB는 Visual Studio를 사용 하 여 기본적으로 설치 됩니다. Visual Studio 2010 및 이전 버전 Visual Studio;와 함께 기본적으로 설치 됩니다 (LocalDB) 없이 SQL Server Express 필수 구성 요소 중 하나로 설치 이유 즉 [이 시리즈의 첫 번째 자습서](introduction.md)합니다.

SQL Server 버전에 대 한 자세한 내용은 다음 리소스를 참조 LocalDB를 포함 하 여 [SQL Server 데이터베이스 작업](../../../../whitepapers/aspnet-data-access-content-map.md#sqlserver)합니다.

## <a name="entity-framework-and-universal-providers"></a>Entity Framework와 유니버설 공급자

데이터베이스 액세스를 위해 Contoso 대학교 응용 프로그램에.NET Framework에 포함 되어 있지 않으므로 응용 프로그램과 함께 배포 해야 하는 다음 소프트웨어가 필요:

- [ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) (Azure SQL 데이터베이스를 사용 하도록 ASP.NET 멤버 자격 시스템 수 있음)
- [Entity Framework](https://msdn.microsoft.com/en-us/library/gg696172.aspx)

이 소프트웨어를 NuGet 패키지에 포함 되므로 프로젝트 이미 설정 되어 필요한 어셈블리를 프로젝트와 함께 배포 되도록 합니다. (링크는이 자습서에 대 한 다운로드 한 시작 프로젝트에 설치 된 것 보다 최신일 수 있습니다 이러한 패키지의 현재 버전을 가리킵니다.)

Azure 대신 제 3 자 호스팅 공급자에 게 배포 하는 경우 Entity Framework 5.0 이상을 사용 하 고 있는지 확인 합니다. 이전 버전의 Code First 마이그레이션을 완전 신뢰 필요 하 고 대부분의 호스팅 공급자 보통 신뢰 응용 프로그램을 실행 됩니다. 보통 신뢰 하는 방법에 대 한 자세한 내용은 참조는 [iis 테스트 환경으로 배포](deploying-to-iis.md) 자습서입니다.

## <a name="configure-code-first-migrations-for-application-database-deployment"></a>응용 프로그램 데이터베이스 배포에 대 한 Code First 마이그레이션을 구성합니다

Code First에서 관리 하는 Contoso 대학 응용 프로그램 데이터베이스 및 Code First 마이그레이션을 사용 하 여 배포 합니다. Code First 마이그레이션을 사용 하 여 데이터베이스 배포의 개요를 참조 하십시오. [이 시리즈의 첫 번째 자습서](introduction.md)합니다.

응용 프로그램 데이터베이스를 배포 하면 일반적으로 배포 하지는 않습니다 단순히 그 안의 데이터가 모든 개발 데이터베이스를 프로덕션에 대부분의 데이터에가 있기 때문에 아마도 테스트용 으로만 사용 합니다. 예를 들어 테스트 데이터베이스에 있는 학생 이름을 가상의 합니다. 반면에 자주 배포할 수는 없습니다 것에 데이터가 없는 데이터베이스 구조만 전혀 합니다. 테스트 데이터베이스에 있는 데이터의 일부 실제 데이터 일 수 있습니다 하며 사용자가 응용 프로그램을 사용 하기 시작 하는 경우 있습니다 이어야 합니다. 예를 들어 데이터베이스 유효한 등급 값 또는 실제 부서 이름을 포함 하는 테이블이 있다고 가정 합니다.

이 일반적인 시나리오를 시뮬레이트하는 Code First 마이그레이션을 구성 합니다 `Seed` 프로덕션 환경에서 있습니다 수 있도록 하려는 데이터를 데이터베이스에 삽입 하는 메서드입니다. 이 `Seed` 메서드는 프로덕션 환경에서 코드 첫 번째 데이터베이스를 만든 후 프로덕션 환경에서 실행 되므로 테스트 데이터를 삽입 하지 않아야 합니다.

이전 버전의 Code First 마이그레이션 전에 이었습니다 `Seed` 삽입 하는 메서드를 테스트 데이터 또한 모든 모델을 개발 하는 동안 변경 데이터베이스 완전히 삭제 하 고 처음부터 다시 생성 했습니다. Code First 마이그레이션을, 데이터베이스 변경 된 후 데이터는 유지 하는 테스트의 테스트 데이터를 포함 하므로 `Seed` 메서드는 필요 없습니다. 다운로드 한 프로젝트의 모든 데이터를 포함 하는 메서드를 사용 하 여는 `Seed` 이니셜라이저 클래스의 메서드. 이 자습서에서는 해당 이니셜라이저 클래스를 해제 합니다 및 `enable Migrations. Then you'll update the `초기값 ' 메서드 마이그레이션 구성에서 클래스 삽입만 데이터를 프로덕션 환경에 삽입할 수 있도록 합니다.

다음 다이어그램에서는 응용 프로그램 데이터베이스의 스키마를 보여 줍니다.

[![School_database_diagram](preparing-databases/_static/image2.png)](preparing-databases/_static/image1.png)

이 자습서에 대 한 라고 가정 하 고 `Student` 및 `Enrollment` 사이트를 처음 배포할 때 테이블이 비어 있어야 합니다. 다른 테이블 때 응용 프로그램 문제를 미리 로드 하는 데이터를 포함 합니다.

### <a name="disable-the-initializer"></a>이니셜라이저를 사용 하지 않도록 설정

Code First 마이그레이션을 사용 하 고는, 이후 필요가 없습니다 사용 하 여 `DropCreateDatabaseIfModelChanges` Code First 이니셜라이저입니다. 이 이니셜라이저에 대 한 코드는는 *SchoolInitializer.cs* ContosoUniversity.DAL 프로젝트 파일에에서 있습니다. 설정에는 `appSettings` 의 요소는 *Web.config* 응용 프로그램 데이터베이스에 처음으로 액세스 하려고 시도 될 때마다 실행 되도록이 이니셜라이저 발생:

[!code-xml[Main](preparing-databases/samples/sample1.xml?highlight=3)]

응용 프로그램을 열고 *Web.config* 파일 제거 하거나 주석으로 처리는 `add` Code First 이니셜라이저 클래스를 지정 하는 요소입니다. `appSettings` 요소는 이제 다음과 같이 표시:

[!code-xml[Main](preparing-databases/samples/sample2.xml)]

> [!NOTE]
> 또 다른 방법은 이니셜라이저 클래스를 지정 하는 호출 하 여 수행 `Database.SetInitializer` 에 `Application_Start` 에서 메서드는 *Global.asax* 파일입니다. 해당 메서드를 사용 하 여 이니셜라이저를 지정 하는 프로젝트에서 마이그레이션이 설정 하는 경우 해당 코드 줄을 제거 합니다.


> [!NOTE]
> Visual Studio 2013을 사용 하는 경우 추가 단계 2와 3 간의 다음 단계: (a)의 PMC 입력 "업데이트 패키지 entityframework-버전 6.1.1" EF의 현재 버전을 가져오려면 합니다. 다음 (b) 빌드 오류 목록을 가져오고 패키지를 수정 하는 프로젝트를 빌드합니다. 문을 사용 하 여 더 이상 존재 마우스 오른쪽 단추로 클릭 하 고, 필요한 장소로 문을 사용 하 여 추가 하는 해결을 클릭 하는 네임 스페이스에 대 한 삭제 하 고 System.Data.Entity.EntityState로 System.Data.EntityState 나타나는 횟수를 변경 합니다.


### <a name="enable-code-first-migrations"></a>Code First 마이그레이션을 사용 하도록 설정

1. ContosoUniversity 프로젝트 (하지 ContosoUniversity.DAL)를 시작 프로젝트로 설정 되어 있는지 확인 합니다. **솔루션 탐색기**ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **시작 프로젝트로 설정**합니다. Code First 마이그레이션을 데이터베이스 연결 문자열을 찾을 시작 프로젝트에 표시 됩니다.
2. **도구** 메뉴를 클릭 하 여 **라이브러리 패키지 관리자** (또는 **NuGet 패키지 관리자**) 한 다음 **패키지 관리자 콘솔**합니다.

    ![Selecting_Package_Manager_Console](preparing-databases/_static/image3.png)
3. 맨 위에 있는 **패키지 관리자 콘솔** 창으로 기본 프로젝트 선택한 다음 at ContosoUniversity.DAL 선택은 `PM>` 프롬프트 "마이그레이션 사용"을 입력 합니다.

    ![enable-migrations 명령](preparing-databases/_static/image4.png)

    (라는 오류가 발생 하는 경우는 *사용 마이그레이션* 명령을 인식할 수 없습니다, 명령을 입력 *업데이트 패키지 EntityFramework-다시 설치* 하 고 다시 시도 하십시오.)

    이 명령은 만듭니다는 *마이그레이션* 폴더 ContosoUniversity.DAL 프로젝트에 두 개의 파일을 해당 폴더에 배치:는 *Configuration.cs* 마이그레이션 및는 를구성하는데사용할수있는파일*InitialCreate.cs* 데이터베이스를 만드는 첫 번째 마이그레이션에 대 한 파일입니다.

    ![Migrations 폴더](preparing-databases/_static/image5.png)

    DAL 프로젝트를 선택는 **기본 프로젝트** 드롭 다운 목록에서 **패키지 관리자 콘솔** 때문에 `enable-migrations` Code First를 포함 하는 프로젝트에서 명령을 실행 해야 합니다 컨텍스트 클래스입니다. 해당 클래스는 클래스 라이브러리 프로젝트에 포함 된 경우 Code First 마이그레이션을 솔루션에 대 한 시작 프로젝트에 데이터베이스 연결 문자열을 찾습니다. ContosoUniversity 솔루션의 웹 프로젝트를 시작 프로젝트로 설정한 합니다. Visual Studio의 시작 프로젝트로 연결 문자열을 포함 된 프로젝트를 지정 하지 않으려면 경우 PowerShell 명령에서 시작 프로젝트를 지정할 수 있습니다. 명령 구문을 보려면 명령 입력 `get-help enable-migrations`합니다.

    `enable-migrations` 데이터베이스가 이미 있기 때문에 자동으로 첫 번째 마이그레이션을 만든 명령입니다. 대신은 데이터베이스를 만들 마이그레이션입니다. 이 위해 사용 하 여 **서버 탐색기** 또는 **SQL Server 개체 탐색기** 마이그레이션을 사용 하도록 설정 하기 전에 ContosoUniversity 데이터베이스를 삭제 하 합니다. 마이그레이션을 사용 하도록 설정 하면 첫 번째 마이그레이션 수동으로 입력 하 여 만듭니다 "추가 마이그레이션 InitialCreate" 명령입니다. 다음 명령은 "-데이터베이스 업데이트"를 입력 하 여 데이터베이스를 만들 수 있습니다.

### <a name="set-up-the-seed-method"></a>Seed 메서드 설정

이 자습서에 대 한 코드를 추가 하 여 고정된 데이터를 추가 합니다는 `Seed` Code First 마이그레이션을 방식의 `Configuration` 클래스입니다. 첫 번째 마이그레이션 호출 코드에서 `Seed` 모든 마이그레이션 후 메서드.

이후는 `Seed` 데이터가 이미 테이블에 첫 번째 마이그레이션 후, 모든 마이그레이션 후 메서드를 실행 합니다. 사용 하 여이 상황을 처리 하는 `AddOrUpdate` 메서드를 이미 삽입 되었거나 아직 없는 경우 삽입 된 행을 업데이트 합니다. `AddOrUpdate` 메서드 시나리오에 대 한 최상의 선택이 아닐 수 있습니다. 자세한 내용은 참조 [EF 4.3 AddOrUpdate 메서드로 주의](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) Julie Lerman 블로그.

1. 열기는 *Configuration.cs* 에 있는 설명은 코드를 바꾸고 파일은 `Seed` 메서드를 다음 코드로:

    [!code-csharp[Main](preparing-databases/samples/sample3.cs)]
2. 에 대 한 참조 `List` 없기 때문에 그 아래 빨간색의 구불구불한 선이는 `using` 아직 문을 네임 스페이스에 대 한 합니다. 인스턴스 중 하나를 마우스 오른쪽 단추로 클릭 `List` 클릭 **해결**, 클릭 하 고 **System.Collections.Generic 사용**합니다.

    ![문을 사용 하 여 사용 하 여 확인](preparing-databases/_static/image6.png)

    다음 코드를 추가 하는이 메뉴를 선택은 `using` 문을 파일의 맨 위 근처 합니다.

    [!code-csharp[Main](preparing-databases/samples/sample4.cs)]
3. CTRL-SHIFT-B를 눌러 프로젝트를 빌드합니다.

이제 프로젝트를 배포할 준비가 된 *ContosoUniversity* 데이터베이스입니다. 배포 응용 프로그램을 처음 실행 하 고 데이터베이스에 액세스 하는 페이지로 이동 하 고 나면 코드 첫 번째 데이터베이스를 만들고 실행이 `Seed` 메서드.

> [!NOTE]
> 코드를 추가 하는 `Seed` 메서드는 데이터베이스에 고정된 데이터를 삽입할 수 있는 여러 가지 방법 중 하나입니다. 다른 방법은 코드를 추가 하는 것은 `Up` 및 `Down` 각 마이그레이션 클래스의 메서드. `Up` 및 `Down` 메서드는 데이터베이스 변경 내용을 구현 하는 코드를 포함 합니다. 예제를 볼 수는 [데이터베이스 업데이트를 배포](deploying-a-database-update.md) 자습서입니다.
> 
> 사용 하 여 SQL 문을 실행 하는 코드를 작성할 수도 있습니다는 `Sql` 메서드. 예를 들어 예산 열에서 Department 테이블을 추가 하는 마이그레이션의 일환으로 $ 1, 000.00에 모든 부서 예산 초기화 하려고 하는 경우 다음 줄의 코드를 추가할 수는 `Up` 해당 마이그레이션에 대 한 메서드:
> 
> `Sql("UPDATE Department SET Budget = 1000");`


## <a name="create-scripts-for-membership-database-deployment"></a>멤버 자격 데이터베이스 배포에 대 한 스크립트 만들기

Contoso 대학교 응용 프로그램 ASP.NET 멤버 자격 시스템 및 폼 인증을 사용 하 여 인증 하 고 사용자 권한을 부여 합니다. **업데이트 크레딧** 페이지는 관리자 역할에 속한 사용자만 액세스할 수 있습니다.

응용 프로그램을 실행 하 고 클릭 **Courses**, 클릭 하 고 **업데이트 크레딧**합니다.

![업데이트 크레딧을 클릭 합니다.](preparing-databases/_static/image7.png)

**로그인** 때문에 페이지가 표시 됩니다는 **업데이트 크레딧** 페이지 관리 권한이 필요 합니다.

입력 *admin* 사용자 이름 및 *devpwd* 클릭와 암호 **로그인**합니다.

![로그인 페이지](preparing-databases/_static/image8.png)

**업데이트 크레딧** 페이지가 나타납니다.

![크레딧 페이지를 업데이트 합니다.](preparing-databases/_static/image9.png)

사용자 및 역할 정보에는 *aspnet ContosoUniversity* 변수로 지정 된 데이터베이스는 **DefaultConnection** 에서 연결 문자열은 *Web.config* 파일입니다.

마이그레이션 배포를 사용할 수 없습니다 Entity Framework Code First 하 여이 데이터베이스를 관리 되지 않습니다. 사용 하 여 dbDacFx 공급자가 데이터베이스 스키마를 배포 하 고 초기 데이터를 데이터베이스 테이블에 삽입 하는 스크립트를 실행 하려면 게시 프로필을 구성 합니다.

> [!NOTE]
> Visual Studio 2013 (이제 ASP.NET Identity 라고 함) 새 ASP.NET 멤버 자격 시스템 도입 되었습니다. 새 시스템을 사용 하면 동일한 데이터베이스에 응용 프로그램 및 멤버 자격 테이블을 모두 유지할 수 있습니다 및 둘 다를 배포 하려면 Code First 마이그레이션을 사용할 수 있습니다. 샘플 응용 프로그램 Code First 마이그레이션을 사용 하 여 배포할 수 없습니다는 이전 ASP.NET 멤버 자격 시스템을 사용 합니다. 이 멤버 자격 데이터베이스를 배포 하기 위한 절차는 응용 프로그램에서 Entity Framework Code First 만들어지지 않으므로 SQL Server 데이터베이스를 배포 해야 하는 다른 모든 시나리오에도 적용 됩니다.


여기서도 일반적으로 원하지 개발에서 사용 하는 프로덕션 환경에서 동일한 데이터 합니다. 처음으로 사이트를 배포 하는 경우에 테스트를 위해 생성 하는 사용자 계정의 전체 또는 대부분을 제외 하려면 일반적입니다. 따라서 다운로드 한 프로젝트에 두 개의 멤버 자격 데이터베이스: *aspnet ContosoUniversity.mdf* 개발 사용자와 및 *aspnet-ContosoUniversity-Prod.mdf* 프로덕션 사용자와 합니다. 이 자습서에 대 한 사용자 이름이 두 데이터베이스 모두에 동일한 지: *admin* 및 *nonadmin*합니다. 모든 사용자가 암호 *devpwd* 개발 데이터베이스에서 및 *prodpwd* 프로덕션 데이터베이스에 있습니다.

개발 사용자 테스트 환경을 스테이징 및 프로덕션에 프로덕션 사용자에 게 배포 합니다. 이렇게 하기 위해이 자습서에서 개발 및 프로덕션 환경에 대 한 두 개의 SQL 스크립트를 만들어야 하 고 이후의 자습서으로 실행 하도록 게시 프로세스를 구성 합니다.

> [!NOTE]
> 멤버 자격 데이터베이스 계정 암호의 해시를 저장 합니다. 한 컴퓨터에서 계정을 배포 하려면 원본 컴퓨터에서 보다 해시 루틴이 대상 서버에서 다른 해시를 생성 하지 않아도 되어 있는지 확인 해야 합니다. 생성 합니다 동일한 해시 ASP.NET Universal Providers를 사용 하는 경우 기본 알고리즘을 변경 하지 않는 상태로 있습니다. 기본 알고리즘 HMACSHA256 이며에 지정 된는 **유효성 검사** 특성에는  **[machineKey](https://msdn.microsoft.com/en-us/library/system.web.configuration.machinekeysection.aspx)**  Web.config 파일의 요소입니다.


SQL Server Management Studio (SSMS)를 사용 하 여 또는 타사 도구를 사용 하 여 데이터 배포 스크립트를 수동으로 만들 수 있습니다. 이 자습서의 나머지 부분이에서는이 SSMS에서 수행 하는 방법을 표시 되지만 설치 하 고 SSMS를 사용 하지 않으려는 경우에 프로젝트의 완성된 된 버전에서 스크립트를 가져올 고 노트가 저장은 솔루션 폴더에서 섹션으로 건너뛸 수 있습니다.

SSMS를 설치 하려면 설치에서 [다운로드 센터: Microsoft SQL Server 2012 Express](https://www.microsoft.com/en-us/download/details.aspx?id=29062) 클릭 하 여 [ENU\x64\SQLManagementStudio\_x64\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLManagementStudio_x64_ENU.exe) 또는 [ ENU\x86\SQLManagementStudio\_x86\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLManagementStudio_x86_ENU.exe)합니다. 잘못 선택 하면 시스템에 대 한 것을 설치 하지 하 고 다른 하나를 시도할 수 있습니다.

(이것은 600mb 다운로드 note 합니다. 데 시간이 오래 걸릴 수 있습니다 설치 하 고 컴퓨터를 다시 부팅 해야 합니다.)

SQL Server 설치 센터의 첫 번째 페이지에서 클릭 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**, 기본 선택 항목을 수락 하 여 지침을 따릅니다.

### <a name="create-the-development-database-script"></a>개발 데이터베이스 스크립트 만들기

1. SSMS를 실행 합니다.
2. 에 **서버에 연결** 대화 상자에 입력 *(localdb) \v11.0* 로 **서버 이름**, 둡니다 **인증** 로설정**Windows 인증**, 클릭 하 고 **연결**합니다.

    ![SSMS는 서버에 연결](preparing-databases/_static/image10.png)
3. 에 **개체 탐색기** 창 확장 **데이터베이스**를 마우스 오른쪽 단추로 클릭 **aspnet ContosoUniversity**, 클릭 **작업**, 클릭 하 고 **스크립트 생성**합니다.

    ![SSMS 스크립트 생성](preparing-databases/_static/image11.png)
4. 에 **스크립트 생성 및 게시** 대화 상자를 클릭 **스크립팅 옵션 설정**합니다.

    건너뛸 수 있습니다는 **개체 선택** 기본값 이므로 단계 **전체 데이터베이스 및 모든 데이터베이스 개체 스크립팅** 대상입니다.
5. **고급**을 클릭합니다.

    ![SSMS 스크립팅 옵션](preparing-databases/_static/image12.png)
6. 에 **고급 스크립팅 옵션** 대화 상자, 아래로 스크롤하여 **스크립팅할 데이터 형식**를 클릭 하 고는 **데이터만** 드롭 다운 목록에서 옵션입니다.
7. 변경 **USE DATABASE 스크립팅** 를 **False**합니다. 문 사용 Azure SQL 데이터베이스에 대해 유효 하지 및 테스트 환경에서 SQL Server Express에 배포에 필요한 되지 않습니다.

    ![SSMS 스크립트 데이터 전용, USE 문이 없는](preparing-databases/_static/image13.png)
8. **확인**을 클릭합니다.
9. 에 **스크립트 생성 및 게시** 대화 상자는 **파일 이름** 상자 스크립트를 만들 위치를 지정 합니다. 경로 파일 이름 및 솔루션 폴더 (ContosoUniversity.sln 파일이 있는 폴더)를 변경 *aspnet-데이터-dev.sql*합니다.
10. 클릭 **다음** 로 이동 하는 **요약** 탭을 클릭 한 다음 **다음** 스크립트를 다시 합니다.

    ![SSMS 스크립트 생성](preparing-databases/_static/image14.png)
11. **마침**을 클릭합니다.

### <a name="create-the-production-database-script"></a>프로덕션 데이터베이스 스크립트 만들기

프로덕션 데이터베이스와 프로젝트를 실행 하지 않은 LocalDB 인스턴스를 아직 연결 되지 않았습니다. 따라서 먼저 데이터베이스를 연결 해야 합니다.

1. SSMS에서 **개체 탐색기**를 마우스 오른쪽 단추로 클릭 **데이터베이스** 클릭 **연결**합니다.

    ![SSMS에서 연결](preparing-databases/_static/image15.png)
- 에 **데이터베이스 연결** 대화 상자에서 클릭 **추가** 이동한 후는 *aspnet-ContosoUniversity-Prod.mdf* 파일에 *앱\_ 데이터* 폴더입니다.

    ![연결할 SSMS 추가.mdf 파일](preparing-databases/_static/image16.png)
- **확인**을 클릭합니다.
- 이전 프로덕션 파일에 대 한 스크립트를 만드는 데 사용한 동일한 절차를 따릅니다. 스크립트 파일의 이름을 *aspnet-데이터-prod.sql*합니다.

## <a name="summary"></a>요약

두 데이터베이스는 이제 배포 될 준비가 및 솔루션 폴더에 있는 두 개의 데이터 배포 스크립트도 합니다.

![데이터 배포 스크립트](preparing-databases/_static/image17.png)

다음 자습서에서는 배포에 영향을 주는 프로젝트 설정을 구성 하 고 자동 설정 *Web.config* 배포 응용 프로그램에서 달라 야 하는 설정에 대 한 변환 파일입니다.

## <a name="more-information"></a>추가 정보

NuGet에 대 한 자세한 내용은 참조 하십시오. [NuGet이 포함 된 프로젝트 라이브러리가 관리](https://msdn.microsoft.com/en-us/magazine/hh547106.aspx) 및 [NuGet 설명서](http://docs.nuget.org/docs/start-here/overview)합니다. NuGet을 사용 하지 않으려면 설치 될 때 역할을 결정 하는 NuGet 패키지를 분석 하는 방법에 알아보려면 해야 합니다. (구성할 수는 예를 들어 *Web.config* 변환 등 빌드 시간에 실행 되도록 PowerShell 스크립트를 구성 합니다.) NuGet의 작동 방식에 대 한 자세한 참조 [만들기 및 게시 패키지](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package) 및 [구성 파일 및 소스 코드 변환](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations)합니다.

>[!div class="step-by-step"]
[이전](introduction.md)
[다음](web-config-transformations.md)
