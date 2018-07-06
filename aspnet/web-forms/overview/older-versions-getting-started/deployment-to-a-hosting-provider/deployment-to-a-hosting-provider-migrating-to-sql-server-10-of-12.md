---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
title: 'SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포 합니다: SQL Server-10 / 12로 마이그레이션 | Microsoft Docs'
author: tdykstra
description: 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹 응용 프로그램 프로젝트 Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 중...
ms.author: aspnetcontent
ms.date: 11/17/2011
ms.assetid: a89d6f32-b71b-4036-8ff7-5f8ac2a6eca8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
msc.type: authoredcontent
ms.openlocfilehash: bc0bca18d2f6e4cdbb527ab75952e9a50eb49b20
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37827364"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-migrating-to-sql-server---10-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포 합니다: SQL Server-10 / 12로 마이그레이션
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹용 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. Visual Studio 2010 웹 게시 업데이트를 설치 하는 경우에 사용할 수 있습니다. 계열에 대 한 소개를 참조 하세요 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 출시 이후 도입 된 배포 기능을 보여 줍니다, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다 및 Azure App Service Web Apps를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하세요 [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)입니다.


## <a name="overview"></a>개요

이 자습서에서는 SQL Server Compact에서 SQL Server로 마이그레이션하는 방법을 보여 줍니다. SQL Server Compact를 지원 하지 않는, 저장된 프로시저, 트리거, 뷰, 복제 등 SQL Server 기능을 활용 하는 작업을 수행 하는 것이 좋습니다 하는 이유 중 하나입니다. SQL Server Compact 및 SQL Server 간의 차이점에 대 한 자세한 내용은 참조는 [SQL Server Compact 배포](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) 자습서입니다.

### <a name="sql-server-express-versus-full-sql-server-for-development"></a>개발에 대 한 전체 SQL Server와 SQL Server Express

SQL Server로 업그레이드 하기로 한 후에 개발 및 테스트 환경에서 SQL Server 또는 SQL Server Express를 사용 하는 것이 좋습니다. 데이터베이스 엔진 기능 및 도구 지원에서 차이 외에도 공급자 구현 SQL Server Compact와 다른 버전의 SQL Server 간에 차이가 있습니다. 이러한 차이 다른 결과 생성 하는 동일한 코드를 발생할 수 있습니다. 따라서 개발 데이터베이스로 SQL Server Compact 유지 하려는 경우 철저히 테스트 해야 사이트 SQL Server 또는 SQL Server Express에서 프로덕션에 각 배포 하기 전에 테스트 환경에서.

SQL Server Compact는 달리 SQL Server Express는 기본적으로 동일한 데이터베이스 엔진 및 전체 SQL Server와 같은.NET 공급자를 사용 합니다. SQL Server express를 테스트 하는 경우 SQL Server를 사용 하 여 수로 동일한 결과 얻는 것 이라는 것을 확신할 수 있습니다. 대부분의 동일한 데이터베이스 도구를 사용 하 여 SQL Server를 사용 하 여 사용할 수 있는 SQL Server express (되는 주목할 만한 예외 [SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)), 저장된 프로시저, 뷰, 트리거, SQL Server의 다른 기능을 지원 하 고 및 복제 합니다. 하지만 (일반적으로 해야 프로덕션 웹 사이트에서는 전체 SQL Server를 사용 합니다. SQL Server Express는 공유 호스팅 환경에서 실행할 수 있지만를 위해 설계 되지 않았습니다 및 여러 호스팅 공급자에서 지원 하지 않습니다.)

Visual Studio 2012를 사용 하는 경우 일반적으로 개발 환경에 대 한 SQL Server Express LocalDB를 선택할 Visual Studio를 사용 하 여 기본적으로 설치 된 기능 이므로. 그러나 LocalDB 테스트 환경에 대 한 SQL Server 또는 SQL Server Express를 사용 해야 하므로 IIS에서 작동 하지 않습니다.

### <a name="combining-databases-versus-keeping-them-separate"></a>데이터베이스를 별도 유지 및 결합

Contoso University 응용 프로그램에 두 SQL Server Compact 데이터베이스: 멤버 자격 데이터베이스 (*aspnet.sdf*) 및 응용 프로그램 데이터베이스 (*School.sdf*). 를 마이그레이션하는 경우에 2 개의 개별 데이터베이스 또는 단일 데이터베이스에 이러한 데이터베이스를 마이그레이션할 수 있습니다. 응용 프로그램 데이터베이스 및 멤버 자격 데이터베이스 간의 데이터베이스 조인을 수행 하기 위해 결합 하려는 경우. 호스팅 계획 결합 하는 이유를 제공할 수도 있습니다. 예를 들어, 호스팅 공급자는 여러 데이터베이스에 대 한 추가 요금을 청구할 수 또는 둘 이상의 데이터베이스도 허용 하지 않을 수 있습니다. Cytanium Lite 호스팅만 단일 SQL Server 데이터베이스를 허용 하는이 자습서에 사용 되는 계정에 사용 하는 경우입니다.

이 자습서에서는 이러한 방식으로 두 데이터베이스를 마이그레이션할 수 있습니다.

- 개발 환경에서 두 LocalDB 데이터베이스를 마이그레이션하십시오.
- 테스트 환경에서 두 SQL Server Express 데이터베이스를 마이그레이션하십시오.
- 결합 된 프로덕션 환경에서 완전 한 SQL Server 데이터베이스를 마이그레이션하십시오.

미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.

## <a name="installing-sql-server-express"></a>SQL Server Express 설치

SQL Server Express는 Visual Studio 2010을 사용 하 여 기본적으로 자동으로 설치 됩니다 있지만 기본적으로 설치 되지 않은 Visual Studio 2012를 사용 하 여 합니다. SQL Server 2012 Express를 설치 하려면 다음 링크를 클릭 합니다.

- [SQL Server Express 2012](https://www.microsoft.com/download/details.aspx?id=29062)

선택 *한국어/x64/SQLEXPR\_x64\_ENU.exe* 하거나 *한국어/x86/SQLEXPR\_x86\_ENU.exe*, 설치 마법사에서 기본값을 적용 하 고 설정. 설치 옵션에 대 한 자세한 내용은 참조 하세요. [설치 마법사 (설치)에서 SQL Server 2012 설치](https://msdn.microsoft.com/library/ms143219.aspx)합니다.

## <a name="creating-sql-server-express-databases-for-the-test-environment"></a>테스트 환경에 대 한 SQL Server Express 데이터베이스 만들기

다음 단계는 ASP.NET 멤버 자격 및 School 데이터베이스를 만드는 것입니다.

**뷰** 메뉴 선택 **서버 탐색기** (**데이터베이스 탐색기** Visual Web developer에서)를 마우스 오른쪽 단추로 클릭 **데이터 연결**선택한 **새 SQL Server 데이터베이스 만들기**합니다.

![Selecting_Create_New_SQL_Server_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image1.png)

에 **새 SQL Server 데이터베이스 만들기** 대화 상자에 입력 합니다 ". \SQLExpress"에 **서버 이름** 상자 및 "aspnet 테스트"에서 **새 데이터베이스 이름** 상자를클릭**확인**합니다.

![Create_New_SQL_Server_Database_aspnet](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image2.png)

"학교-Test" 라는 새 SQL Server Express School 데이터베이스를 만들려면 동일한 절차를 따릅니다.

(에 추가할 때는 "Test" 이러한 데이터베이스 이름은 나중에 개발 환경에 대 한 각 데이터베이스의 추가 인스턴스를 만들어야 하 고 데이터베이스의 두 집합을 구분할 수 해야 합니다.)

**서버 탐색기** 이제 두 새 데이터베이스를 표시 합니다.

![New_databases_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image3.png)

## <a name="creating-a-grant-script-for-the-new-databases"></a>새 데이터베이스에 대 한 권한 부여 스크립트 만들기

응용 프로그램 개발 컴퓨터에 IIS에서 실행 하는 경우 응용 프로그램에 기본 응용 프로그램 풀 자격 증명을 사용 하 여 데이터베이스에 액세스 합니다. 그러나 기본적으로 응용 프로그램 풀 id 없는 데이터베이스를 열 수 있는 권한이 있습니다. 따라서 해당 권한을 부여 하는 스크립트를 실행 해야 합니다. 이 섹션에서는 실행 하는 IIS에서 실행 될 때 응용 프로그램에서 데이터베이스를 열 수 있도록 되도록 이상 스크립트를 만듭니다.

솔루션의 *SolutionFiles* 에서 만든 폴더를 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서에서는 명명 된 새 SQL 파일을 만듭니다 *Grant.sql*합니다. 파일에 다음 SQL 명령을 복사 하 고 저장 한 다음 파일을 닫습니다.

[!code-sql[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample1.sql)]

> [!NOTE]
> 이 스크립트는이 자습서에서는 지정 된 SQL Server 2008 및 Windows 7에서 IIS 설정을 사용 하 여 작동 하도록 설계 되었습니다. Windows, 또는 SQL Server의 다른 버전을 사용 하는 경우 또는 설정한 경우 IIS 컴퓨터에 다르게이 스크립트를 변경 해야 할 수 있습니다. SQL Server 스크립트에 대 한 자세한 내용은 참조 하세요. [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511)합니다.


> [!NOTE] 
> 
> **보안 참고** 이 스크립트는 db 제공\_프로덕션 환경에 맞게 해야는 런타임 시 데이터베이스를 액세스 하는 사용자에 게 소유자 권한. 일부 시나리오에서는 전체 데이터베이스 스키마 배포에 대해서만 사용 권한을 업데이트 하 고 실행된 시간에 대 한 데이터 읽기 및 쓰기에 권한이 있는 다른 사용자 지정 된 사용자를 지정 하는 것이 좋습니다. 자세한 내용은 **Code First 마이그레이션에 대 한 자동 Web.config 변경 내용 검토** 에 [IIS 테스트 환경으로 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)합니다.


## <a name="configuring-database-deployment-for-the-test-environment"></a>테스트 환경에 대 한 데이터베이스 배포를 구성합니다.

다음으로, 각 데이터베이스에 대해 다음 태스크를 수행 합니다 하는 Visual Studio를 구성 합니다.

- 대상 데이터베이스에서 원본 데이터베이스의 구조 (테이블, 열, 제약 조건 등)을 만드는 SQL 스크립트를 생성 합니다.
- 대상 데이터베이스의 테이블에 원본 데이터베이스의 데이터를 삽입 하는 SQL 스크립트를 생성 합니다.
- 생성된 된 스크립트 및 대상 데이터베이스에서 만든 권한 부여 스크립트를 실행 합니다.

엽니다는 **프로젝트 속성** 창과 선택 합니다 **SQL 패키지 및 게시** 탭.

했는지 **활성 (릴리스)** 또는 **릴리스** 가 선택 합니다 **구성** 드롭 다운 목록.

클릭 **이 페이지를 사용 하도록 설정**합니다.

![Package_Publish_SQL_tab_Enable_This_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image4.png)

합니다 **패키지 및 게시 SQL** 탭 일반적으로 레거시 배포 메서드를 지정 하기 때문에 사용할 수 없습니다. 대부분의 시나리오에서 데이터베이스 배포를 구성 해야 합니다 **웹 게시** 마법사. SQL Server Compact에서 SQL Server 또는 SQL Server Express로 마이그레이션하는 특수가 방법이 적합 합니다.

클릭 **Web.config에서 가져오기**합니다.

![Selecting_Import_from_Web.config](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image5.png)

Visual Studio에서 연결 문자열을 찾습니다 합니다 *Web.config* 파일인 멤버 자격 데이터베이스에 대 한 하나 및 School 데이터베이스를 찾아서 각 연결 문자열에 해당 하는 행을 추가 합니다 **데이터베이스 항목**  테이블입니다. 찾으면 연결 문자열은 기존 SQL Server Compact 데이터베이스의 경우 및 다음 단계 방법 및 위치를 구성 해야 합니다. 이러한 데이터베이스를 배포 합니다.

에 데이터베이스 배포 설정을 입력 합니다 **데이터베이스 항목 세부 정보** 아래 섹션의 **데이터베이스 항목** 테이블. 에 나와 있는 설정을 **데이터베이스 항목 세부 정보** 섹션의 행 중 관련이 **데이터베이스 항목** 다음 그림에 표시 된 대로 테이블을 선택 합니다.

![Database_Entry_Details_section_of_Package_Publish_SQL_tab](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image6.png)

### <a name="configuring-deployment-settings-for-the-membership-database"></a>멤버 자격 데이터베이스에 대 한 배포 설정을 구성합니다.

선택 합니다 **DefaultConnection 배포** 행에 **데이터베이스 항목** 멤버 자격 데이터베이스에 적용 되는 설정을 구성 하기 위해 테이블.

**대상 데이터베이스에 대 한 연결 문자열**를 새 SQL Server Express 멤버 자격 데이터베이스를 가리키는 연결 문자열을 입력 합니다. 필요한 연결 문자열을 가져올 수 있습니다 **서버 탐색기**합니다. **서버 탐색기**, 확장 **데이터 연결** 선택한를 **aspnetTest** 데이터베이스에서 다음을 **속성** 창 복사는 **연결 문자열** 값입니다.

![aspnet_connection_string_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image7.png)

여기에 재현 되어 동일한 연결 문자열:

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample2.cmd)]

복사 하 고이 연결 문자열을 붙여 넣습니다 **대상 데이터베이스에 대 한 연결 문자열** 에 **SQL 패키지 및 게시** 탭 합니다.

했는지 **데이터 및/또는 기존 데이터베이스에서 스키마 가져오기** 을 선택 합니다. 이 인해 SQL 스크립트를 자동으로 생성 하 고 대상 데이터베이스에서 실행 합니다.

합니다 **원본 데이터베이스에 대 한 연결 문자열** 값에서 추출 되는 *Web.config* 파일과 개발 SQL Server Compact 데이터베이스를 가리킵니다. 이 나중에 대상 데이터베이스에서에서 실행 될 스크립트를 생성 하는 데 사용할 원본 데이터베이스입니다. 데이터베이스의 프로덕션 버전을 배포 하려면 "aspnet Dev.sdf" "aspnet Prod.sdf"를 변경 합니다.

변경 **데이터베이스 스크립팅 옵션** 에서 **스키마만** 하 **스키마 및 데이터**데이터베이스 구조와 데이터 (사용자 계정 및 역할)을 복사 하려는 때문입니다.

이전에 만든 권한 부여 스크립트를 실행 하는 배포를 구성 하려면 추가 해야 합니다 **데이터베이스 스크립트** 섹션입니다. 클릭 **스크립트 추가**, 및를 **SQL 스크립트 추가** 대화 상자에서 권한 부여 스크립트를 저장할 폴더를 탐색 합니다 (이 솔루션 파일에 포함 된 폴더). 라는 파일을 선택 *Grant.sql*, 클릭 **오픈**합니다.

[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)

에 대 한 설정 합니다 **DefaultConnection 배포** 행 **데이터베이스 항목** 이제 다음 그림과 같이 표시:

![Database_Entry_Details_for_DefaultConnection_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image10.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>School 데이터베이스에 대 한 배포 설정을 구성합니다.

다음으로, 선택는 **SchoolContext 배포** 행에 **데이터베이스 항목** School 데이터베이스에 대 한 배포 설정을 구성 하기 위해 테이블.

새 SQL Server Express 데이터베이스에 대 한 연결 문자열을 가져오려면 이전에 사용한 동일한 방법을 사용할 수 있습니다. 이 연결 문자열을 복사 **대상 데이터베이스에 대 한 연결 문자열** 에 **SQL 패키지 및 게시** 탭 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample3.cmd)]

했는지 **데이터 및/또는 기존 데이터베이스에서 스키마 가져오기** 을 선택 합니다.

합니다 **원본 데이터베이스에 대 한 연결 문자열** 값에서 추출 되는 *Web.config* 파일과 개발 SQL Server Compact 데이터베이스를 가리킵니다. "학교 Dev.sdf" "학교 Prod.sdf" 배포 데이터베이스의 프로덕션 버전을 변경 합니다. (앱에서 학교 Prod.sdf 파일 만들어지지\_데이터 폴더를 앱에 테스트 환경에서 해당 파일을 복사할 수 있습니다\_ContosoUniversity 프로젝트 폴더를 나중에 데이터 폴더.)

변경 **데이터베이스 스크립팅 옵션** 하 **스키마와 데이터**입니다.

읽기 권한을 부여 하 고 응용 프로그램 풀 id를 쓸 수 있는 권한이이 데이터베이스에 대 한 추가 스크립트를 실행 하려는 합니다 *Grant.sql* 멤버 자격 데이터베이스에 대해 수행한 것 처럼 스크립트 파일입니다.

완료 되 면, 설정에 대 한 합니다 **SchoolContext 배포** 행 **데이터베이스 항목** 다음 그림과 같이 표시 합니다.

![Database_Entry_Details_for_SchoolContext_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image11.png)

변경 내용을 저장 합니다 **패키지 및 게시 SQL** 탭 합니다.

복사를 *학교 Prod.sdf* 에서 파일을 *c:\inetpub\wwwroot\ContosoUniversity\App\_데이터* 폴더를 *앱\_데이터* 폴더에서 ContosoUniversity 프로젝트입니다.

### <a name="specifying-transacted-mode-for-the-grant-script"></a>권한 부여 스크립트에 대 한 트랜잭션된 모드를 지정합니다.

배포 프로세스는 데이터베이스 스키마 및 데이터를 배포 하는 스크립트를 생성 합니다. 기본적으로 이러한 스크립트를 트랜잭션에서 실행 합니다. 그러나 기본적으로 (예: 권한 부여 스크립트) 사용자 지정 스크립트를 트랜잭션에서 실행 되지 않습니다. 트랜잭션 모드를 혼합 하는 배포 프로세스를 배포 하는 동안 스크립트를 실행 하는 경우 시간 초과 오류를 얻게 됩니다. 이 섹션에서는 사용자 지정 스크립트를 트랜잭션에서 실행할 구성 하기 위해 프로젝트 파일을 편집 합니다.

**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **ContosoUniversity** 프로젝트를 마우스 **프로젝트 언로드**합니다.

![Unload_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image12.png)

그런 다음 프로젝트를 다시 마우스 오른쪽 단추로 클릭 하 고 선택 **ContosoUniversity.csproj 편집**합니다.

![Edit_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image13.png)

Visual Studio 편집기 프로젝트 파일의 XML 콘텐츠를 보여 줍니다. 몇 가지는 `PropertyGroup` 요소입니다. (이미지의 내용에는 `PropertyGroup` 요소가 생략 되었습니다.)

![프로젝트 파일 편집기 창](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image15.png)

아니요 있는 첫 번째 `Condition` 특성, 설정에 관계 없이 적용 되는 빌드 구성입니다. 하나의 `PropertyGroup` 요소는 디버그 빌드 구성에만 적용 됩니다 (참고는 `Condition` 특성), 릴리스 빌드 구성에만 적용 됩니다 하나 및 하나 테스트 빌드 구성에만 적용 됩니다. 내 합니다 `PropertyGroup` 릴리스 빌드 구성에 대 한 요소를 볼 수는 `PublishDatabaseSettings` 에 입력 한 설정을 포함 하는 요소는 **SQL 패키지 및 게시** 탭. `Object` 권한 부여 스크립트를 각각에 해당 하는 요소 ("Grant.sql"의 두 알림 인스턴스)를 지정 합니다. 기본적으로 `Transacted` 특성을 `Source` 각 권한 부여 스크립트에 대 한 요소가 `False`합니다.

![Transacted_false](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image16.png)

값을 변경 합니다 `Transacted` 특성을 `Source` 요소를 `True`합니다.

![Transacted_true](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image17.png)

저장 하 고 프로젝트 파일을 닫고 다음에 프로젝트를 마우스 오른쪽 단추로 **솔루션 탐색기** 선택한 **프로젝트 다시 로드**합니다.

![Reload_project](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image18.png)

## <a name="setting-up-webconfig-transformations-for-the-connection-strings"></a>연결 문자열에 대 한 Web.Config 변환 설정

입력 데이터베이스를 새 SQL Express에 대 한 연결 문자열을 **SQL 패키지 및 게시** 탭에서 사용 하는 웹 배포 배포 중 대상 데이터베이스를 업데이트 하는 중에 합니다. 도 설정 해야 *Web.config* 변환 연결 문자열에 배포 되도록 *Web.config* 파일 새 SQL Server Express 데이터베이스를 가리킵니다. (사용 하는 경우는 **패키지 및 게시 SQL** 탭 게시 프로필의 연결 문자열을 구성할 수 없습니다.)

열기 *Web.Test.config* 바꾸고 합니다 `connectionStrings` 요소는 `connectionStrings` 다음 예제에서는 요소입니다. (ConnectionStrings 요소는 다음과 같습니다 컨텍스트를 제공 하는 주변 코드가 아니라 복사할 수 있는지 확인 합니다.)

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample4.xml?highlight=2-11)]

이 코드는 `connectionString` 및 `providerName` 각 특성 `add` 대체할 요소의 배포에서 *Web.config* 파일입니다. 이러한 연결 문자열에 입력 한 것과 동일 하지 않습니다.는 **패키지 및 게시 SQL** 탭 합니다. 설정 "MultipleActiveResultSets = True" Entity Framework 및 범용 공급자에 대 한 필요 하므로에 추가 되었습니다.

## <a name="installing-sql-server-compact"></a>SQL Server Compact를 설치합니다.

SqlServerCompact NuGet 패키지는 Contoso University 응용 프로그램에 대 한 엔진 어셈블리를 SQL Server Compact 데이터베이스를 제공합니다. 하지만 이제 없는 응용 프로그램 이지만 웹 배포를 SQL Server 데이터베이스에서 실행 하는 스크립트를 만들기 위해 SQL Server Compact 데이터베이스를 읽을 수 있어야 합니다. 을 사용 하려면 SQL Server Compact 데이터베이스를 읽기에 웹 배포 설치 SQL Server Compact 개발 컴퓨터의 다음 링크를 사용 하 여: [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6)합니다.

## <a name="deploying-to-the-test-environment"></a>테스트 환경에 배포

테스트 환경에 게시 하기 위해 사용 하도록 구성 되어 있는 게시 프로필을 만들 필요가 합니다 **SQL 패키지 및 게시** 게시 프로필 데이터베이스 설정 하는 대신 게시 데이터베이스에 대 한 탭 합니다.

먼저 기존 테스트 프로필을 삭제 합니다.

**솔루션 탐색기**ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.

선택 된 **프로필** 탭 합니다.

클릭 **프로필을 관리**합니다.

선택 **테스트**, 클릭 **제거**를 클릭 하 고 **닫기**합니다.

닫기 합니다 **웹 게시** 마법사가 변경이 내용을 저장 합니다.

다음으로, 새 테스트 프로필을 만들고 프로젝트를 게시 하는 데 사용할 합니다.

**솔루션 탐색기**ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.

선택 된 **프로필** 탭 합니다.

선택 **&lt;새로 만들기... &gt;** 드롭다운 목록에서 목록에서 선택한 프로필 이름으로 "Test"를 입력 합니다.

에 **서비스 URL** 상자에 입력 합니다 *localhost*합니다.

에 **사이트 및 응용 프로그램** 상자에 입력 합니다 *기본 웹 사이트/ContosoUniversity*합니다.

에 **대상 URL** 상자에 입력 `http://localhost/ContosoUniversity/`합니다.

**다음**을 클릭합니다.

**설정을** 탭에서 경고는 합니다 **SQL 패키지 및 게시** 탭에 구성 된 새 데이터베이스 게시 개선 사항 사용을 클릭 하 여 덮어쓸 수 있는 기회를 제공 하 합니다. 이 배포에 대 한 재정의 않으려는 합니다 **SQL 패키지 및 게시** 설정 탭에서 그러 **다음**합니다.

![Publish_Web_wizard_Settings_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image19.png)

메시지를 **미리 보기** 탭을 사용 함을 **데이터베이스가 선택 되지 않음 게시할**, 하지만 게시 프로필에서 데이터베이스 게시가 구성 되지 않았습니다.

**게시**를 클릭합니다.

![Publish_Web_wizard_Preview_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image20.png)

Visual Studio 응용 프로그램을 배포 하 고 테스트 환경에서 사이트의 홈 페이지로 브라우저를 엽니다. 앞서 살펴본 있는 동일한 데이터를 표시 하려면 강사 페이지를 실행 합니다. 실행 합니다 **추가 학생** 페이지에서 새 학생을 추가 하 고 다음에 새 학생을 봅니다 합니다 **학생** 페이지. 이 데이터베이스를 업데이트할 수 있습니다 것을 확인 합니다. 선택 된 **업데이트 크레딧** 페이지 (로그인) 멤버 자격 데이터베이스가 배포 된 고에 액세스할 수 있는지 확인 합니다.

## <a name="creating-a-sql-server-database-for-the-production-environment"></a>프로덕션 환경에 대 한 SQL Server 데이터베이스 만들기

테스트 환경에 배포한 했으므로 프로덕션 배포를 설정할 준비가 되었습니다. 먼저, 데이터베이스에 배포를 만들어 테스트 환경에 대해 수행한 것 처럼. 개요에서 기억 하듯이, 두 개가 아닌 하나만 데이터베이스를 설정 하므로 Cytanium Lite 호스팅 계획에 단일 SQL Server 데이터베이스를 허용 합니다. 모든 테이블과 멤버 자격 및 학교 SQL Server Compact 데이터베이스에서 데이터를 프로덕션 환경에서 하나의 SQL Server 데이터베이스에 배포 됩니다.

Cytanium 제어판으로 이동 [ http://panel.cytanium.com ](http://panel.cytanium.com)합니다. 위로 마우스를 가져가면 **데이터베이스** 을 클릭 한 다음 **SQL Server 2008**합니다.

[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)

에 **SQL Server 2008** 페이지에서 클릭 **Create Database**합니다.

[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)

School 데이터베이스 이름을 지정 하 고 클릭 **저장할**합니다. (페이지 자동으로 추가 "contosou"를 접두사 효과적인 이름을 "contosouSchool" 되도록 합니다.)

[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)

같은 페이지에서 클릭 **Create User**합니다. Cytanium의 서버에 보다는 통합된 Windows 보안을 사용 하 여 데이터베이스를 열고 응용 프로그램 풀 id 수 있도록, 데이터베이스를 열 권한이 있는 사용자를 만들어야 합니다. 프로덕션에서 이동 하는 연결 문자열에 사용자의 자격 증명을 추가할 *Web.config* 파일입니다. 이 단계에서는 해당 자격 증명을 만들 수 있습니다.

[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)

필수 필드를 입력 합니다 **SQL 사용자 속성** 페이지:

- 이름으로 "ContosoUniversityUser"를 입력 합니다.
- 암호를 입력 합니다.
- 선택 **contosouSchool** 를 기본 데이터베이스입니다.
- 선택 된 **contosouSchool** 확인란 합니다.

[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)

## <a name="configuring-database-deployment-for-the-production-environment"></a>프로덕션 환경에 대 한 데이터베이스 배포를 구성합니다.

데이터베이스 배포 설정을 설정할 준비가 되었습니다. 이제는 **SQL 패키지 및 게시** 이전 테스트 환경에 대해 수행한 것 처럼 탭 합니다.

열기는 **프로젝트 속성** 창에서를 **SQL 패키지 및 게시** 탭을 했는지 **활성 (릴리스)** 또는 **릴리스** 는 선택 합니다 **구성** 드롭 다운 목록.

각 데이터베이스에 대 한 배포 설정을 구성한 경우 연결 문자열을 구성 하는 방법에 프로덕션 환경과 테스트 환경에 대 한 여러분의 주요 차이점은입니다. 다른 대상 데이터베이스 연결 문자열을 입력 한 테스트 환경에 대 한 하지만 프로덕션 환경에 대 한 대상 연결 문자열은 동일 데이터베이스 모두에 대 한 합니다. 두 데이터베이스를 배포 하는 프로덕션 환경에서 하나의 데이터베이스로 때문입니다.

### <a name="configuring-deployment-settings-for-the-membership-database"></a>멤버 자격 데이터베이스에 대 한 배포 설정을 구성합니다.

멤버 자격 데이터베이스에 적용 되는 설정을 구성 하려면 선택 합니다 **DefaultConnection 배포** 행에 **데이터베이스 항목** 테이블입니다.

**대상 데이터베이스에 대 한 연결 문자열**, 방금 만든 새 프로덕션 SQL Server 데이터베이스를 가리키는 연결 문자열을 입력 합니다. 환영 전자 메일에서 연결 문자열을 가져올 수 있습니다. 다음 샘플 연결 문자열을 포함 하는 전자 메일의 관련 부분:

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample5.cmd)]

세 개의 변수를 대체 한 후 필요한 연결 문자열을이 예제와 비슷합니다.

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample6.cmd)]

복사 하 고이 연결 문자열을 붙여 넣습니다 **대상 데이터베이스에 대 한 연결 문자열** 에 **SQL 패키지 및 게시** 탭 합니다.

했는지 **데이터 및/또는 기존 데이터베이스에서 스키마 가져오기** 하 고 선택 계속 됩니다 **데이터베이스 스크립팅 옵션** 여전히 **스키마 및 데이터**입니다.

에 **데이터베이스 스크립트** 상자 Grant.sql 스크립트 옆의 확인란의 선택을 취소 합니다.

![Disable_Grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image31.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>School 데이터베이스에 대 한 배포 설정을 구성합니다.

다음으로, 선택는 **SchoolContext 배포** 행을 **데이터베이스 항목** School 데이터베이스 설정을 구성 하기 위해 테이블.

동일한 연결 문자열을 복사 **대상 데이터베이스에 대 한 연결 문자열** 멤버 자격 데이터베이스에 대 한 해당 필드에 복사 합니다.

했는지 **데이터 및/또는 기존 데이터베이스에서 스키마 가져오기** 하 고 선택 계속 됩니다 **데이터베이스 스크립팅 옵션** 여전히 **스키마 및 데이터**입니다.

에 **데이터베이스 스크립트** 상자 Grant.sql 스크립트 옆의 확인란의 선택을 취소 합니다.

변경 내용을 저장 합니다 **패키지 및 게시 SQL** 탭 합니다.

## <a name="setting-up-webconfig-transforms-for-the-connection-strings-to-production-databases"></a>프로덕션 데이터베이스에 대 한 연결 문자열에 대 한 Web.Config 설정 변환

다음으로 설정 합니다 *Web.config* 변환을 연결 문자열에 배포 되도록 *Web.config* 새 프로덕션 데이터베이스를 가리키도록 파일입니다. 에 입력 한 연결 문자열을 **SQL 패키지 및 게시** 탭을 사용 하 여 웹 배포에 대 한 응용 프로그램 추가 제외 하 고 사용 해야 하는 것 같습니다는 `MultipleResultSets` 옵션입니다.

열기 *Web.Production.config* 바꾸고 합니다 `connectionStrings` 요소를 `connectionStrings` 요소는 다음 예제와 같습니다. (만 복사는 `connectionStrings` 요소, 컨텍스트를 표시 하도록 제공 되는 주변 태그가 없습니다.)

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample7.xml?highlight=2-11)]

경우에 따라 항상의 연결 문자열을 암호화 하도록 알려주는 통지를 표시 합니다 *Web.config* 파일입니다. 이 여러분의 회사 네트워크에서 서버를 배포 하는 경우에 적절할 수 있습니다. 그러나 공유 호스팅 환경에 배포 하는 경우 호스팅 공급자의 보안 사례를 신뢰 하는 및 것은 불필요 하거나 연결 문자열을 암호화 하는 데 적합 합니다.

## <a name="deploying-to-the-production-environment"></a>프로덕션 환경에 배포

이제 프로덕션 환경에 배포할 준비가 되었습니다. 웹 배포 프로젝트의 SQL Server Compact 데이터베이스를 읽어들일 *앱\_데이터* 폴더 하 고 다시 모든 테이블 및 프로덕션 SQL Server 데이터베이스의 데이터를 만듭니다. 사용 하 여 게시 하려면 합니다 **웹 패키지 및 게시** 프로덕션에 대 한 새 게시 프로필을 만들 필요가 탭 설정 합니다.

테스트 프로필을 앞서 수행한 것 처럼 기존 프로덕션 프로필을 먼저 삭제 합니다.

**솔루션 탐색기**ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.

선택 된 **프로필** 탭 합니다.

클릭 **프로필을 관리**합니다.

선택 **프로덕션**, 클릭 **제거**를 클릭 하 고 **닫기**합니다.

닫기 합니다 **웹 게시** 마법사가 변경이 내용을 저장 합니다.

다음으로, 새 프로덕션 프로필을 만들고 프로젝트를 게시 하는 데 사용할 합니다.

**솔루션 탐색기**ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.

선택 된 **프로필** 탭 합니다.

클릭 **가져오기**, 이전에 다운로드 한.publishsettings 파일을 선택 합니다.

에 **연결** 탭으로 변경 합니다 **대상 URL** 은이 예제에서는 임시 올바른 URL로 http://contosouniversity.com.vserver01.cytanium.com.

프로덕션 프로필을 이름을 바꿉니다. (선택 된 **프로필** 탭을 클릭 **프로필 관리** 를 위해).

닫기 합니다 **웹 게시** 변경 내용을 저장 하는 마법사입니다.

데이터베이스를 프로덕션 환경에서 업데이트 되는 실제 응용 프로그램에서 수행한 두 가지 추가 단계가 이제 게시 하기 전에:

1. 업로드 *앱\_offline.htm*에 나와 있는 것 처럼 합니다 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서입니다.
2. 사용 합니다 **파일 관리자** 복사할 Cytanium 제어판의 기능을 *aspnet Prod.sdf* 및 *학교 Prod.sdf* 프로덕션 사이트에서 파일을 *앱\_데이터* ContosoUniversity 프로젝트의 폴더입니다. 이렇게 하면 새 SQL Server 데이터베이스에 배포 하는 데이터를 프로덕션 웹 사이트에서 수행 된 최신 업데이트에 포함 합니다.

에 **한 번 클릭으로 웹 게시** 도구 모음 있는지 확인 합니다 **프로덕션** 프로필을 선택한 다음 클릭 **게시**.

업로드 한 경우 <em>앱\_offline.htm</em> 게시 하기 전에 사용 해야 합니다 <strong>파일 관리자</strong> Cytanium 제어판 삭제 유틸리티 <em>앱\_오프 라인.</em> htm 테스트 하기 전에 합니다. 동시에 삭제할 수도 합니다 <em>.sdf</em> 에서 파일을 <em>앱\_데이터</em> 폴더.

이제 브라우저를 열고 하 수는 응용 프로그램 테스트 환경에 배포한 후 수행한 동일한 방식으로 테스트 공개 사이트의 URL로 이동 합니다.

## <a name="switching-to-sql-server-express-localdb-in-development"></a>SQL Server Express LocalDB 개발에서로 전환

개요에서 설명한 것 처럼 개발 테스트 및 프로덕션에서 사용 하는 동일한 데이터베이스 엔진을 사용 하는 것이 좋습니다. (개발에서 SQL Server Express를 사용 하는 이점은 데이터베이스를 동일 하 게 작동 개발, 테스트 및 프로덕션 환경에서 인지 해야 합니다.) 이 섹션에서 Visual Studio에서 응용 프로그램을 실행 하는 경우 SQL Server Express LocalDB를 사용 하도록 ContosoUniversity 프로젝트를 설정 하는 것이 됩니다.

이 마이그레이션을 수행 하는 가장 간단한 방법은 되도록 두는 Code First 및 멤버 자격 시스템을 모두 새 개발 데이터베이스를 만듭니다. 이 메서드를 사용 하 여 마이그레이션하려면 세 단계가 필요 합니다.

1. 새 SQL Express LocalDB 데이터베이스를 지정 하도록 연결 문자열을 변경 합니다.
2. 관리자 사용자를 만들려면 웹 사이트 관리 도구를 실행 합니다. 이 멤버 자격 데이터베이스를 만듭니다.
3. Code First 마이그레이션을 update-database 명령은 사용 하 여 만들고 응용 프로그램 데이터베이스를 시드합니다.

### <a name="updating-connection-strings-in-the-webconfig-file"></a>Web.config 파일에서 연결 문자열 업데이트

엽니다는 *Web.config* 바꾸고 파일을 `connectionStrings` 요소를 다음 코드로:

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample8.xml)]

### <a name="creating-the-membership-database"></a>멤버 자격 데이터베이스를 만드는 중

**솔루션 탐색기**ContosoUniversity 프로젝트를 선택한 다음 클릭 **ASP.NET 구성** 에 **프로젝트** 메뉴.

보안 탭을 선택 합니다.

클릭 **만들거나 역할 관리**을 만든 다음는 **관리자** 역할입니다.

보안 탭으로 돌아갑니다.

클릭 **사용자 만들기**를 선택한 후 합니다 **관리자** 관리자 라는 사용자를 만들고 확인란

닫기 합니다 **웹 사이트 관리 도구**합니다.

### <a name="creating-the-school-database"></a>School 데이터베이스 만들기

패키지 관리자 콘솔 창을 엽니다.

에 **기본 프로젝트** 드롭 다운 목록 ContosoUniversity.DAL 프로젝트를 선택 합니다.

다음 명령을 입력합니다.

[!code-powershell[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample9.ps1)]

데이터베이스를 만드는 AddBirthDate 마이그레이션을 적용 하는 초기 마이그레이션을 적용 하는 code First 마이그레이션을 다음 Seed 메서드를 실행 합니다.

사이트 컨트롤 F5 키를 눌러 실행 합니다. 테스트 및 프로덕션 환경에 대해 수행한 것 처럼 실행 합니다 **추가 학생** 페이지에서 새 학생을 추가 하 고 다음에 새 학생을 봅니다 합니다 **학생** 페이지. School 데이터베이스 생성 및 초기화 된 그리고 읽기 및 쓰기 액세스 있는지 확인 합니다.

선택 된 **업데이트 크레딧** 페이지 및 멤버 자격 데이터베이스가 배포 된 고에 액세스할 수 있는지 확인 하려면 로그인 합니다. 사용자 계정을 마이그레이션하지 않은 경우 관리자 계정을 만들고 다음을 선택 합니다 **업데이트 크레딧** 페이지 작동 하는지 확인 합니다.

## <a name="cleaning-up-sql-server-compact-files"></a>SQL Server Compact 파일 정리

파일 및 SQL Server Compact를 지원 하기 위해 포함 된 NuGet 패키지가 더 이상 필요 합니다. 원하는 경우 (이 단계가 필요 하지 않습니다), 불필요 한 파일 및 참조를 정리할 수 있습니다.

**솔루션 탐색기**, 삭제 합니다 *.sdf* 에서 파일을 *앱\_데이터* 폴더 및 *amd64* 및 *x86* 폴더를 *bin* 폴더입니다.

**솔루션 탐색기**(없습니다 프로젝트 중 하나), 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **솔루션용 NuGet 패키지 관리**합니다.

왼쪽된 창에는 **NuGet 패키지 관리** 대화 상자에서 **설치 된 패키지**합니다.

선택 된 **EntityFramework.SqlServerCompact** 패키징하고 클릭 **관리**합니다.

에 **프로젝트 선택** 대화 상자에서 두 프로젝트를 선택 합니다. 두 프로젝트에서 패키지를 제거 하려면 두 확인란의 선택을 취소 한 다음 클릭 **확인**합니다.

또한 종속성 패키지를 제거 하려는 경우 요청 하는 대화 상자에서 클릭 아니요. 다음 중 하나를 유지 해야 하는 Entity Framework 패키지입니다.

제거 하려면 동일한 절차에 따라 합니다 **SqlServerCompact** 패키지 있습니다. (때문에이 순서 대로 패키지를 제거 해야 합니다는 **EntityFramework.SqlServerCompact** 패키지에 따라 달라 집니다 합니다 **SqlServerCompact** 패키지 있습니다.)

이제 성공적으로 마이그레이션한 SQL Server Express와 전체 SQL Server입니다. 다음 자습서를 다른 데이터베이스 변경 및 해야 SQL Server Express 및 SQL Server 전체 테스트 및 프로덕션 데이터베이스를 사용 하는 경우 데이터베이스 변경 내용을 배포 하는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
