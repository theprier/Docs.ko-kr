---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: "Visual Studio를 사용 하 여 ASP.NET 웹 배포: 테스트 배포 | Microsoft Docs"
author: tdykstra
description: "이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) 실행 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/23/2015
ms.topic: article
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: 01f72e0240e84944f8ffece9a2dbc5802be4646b
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 테스트에 배포
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자입니다. 계열에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](introduction.md)합니다.


## <a name="overview"></a>개요

이 자습서에서는 로컬 컴퓨터에서 IIS에 ASP.NET 웹 응용 프로그램을 배포 하는 방법을 보여 줍니다.

응용 프로그램을 개발 하는 경우 일반적으로 Visual Studio에서 실행 하 여 테스트 합니다. 웹 응용 프로그램 프로젝트를 Visual Studio 2012에서 기본적으로 개발 웹 서버와 IIS Express를 사용 합니다. IIS Express는 기본적으로 Visual Studio 2010을 사용 하는 Visual Studio 개발 서버 (Cassini 라고도), 보다 전체 IIS 처럼 더 동작 합니다. 하지만 두 개발 웹 서버 IIS와 동일 하 게 작동 합니다. 결과적으로, 것 Visual Studio에서 테스트 하지만 IIS에 배포 될 때 실패 하는 경우 응용 프로그램은 제대로 실행 가능 합니다.

다음과 같은이 방법으로 응용 프로그램을 더욱 안정적으로 테스트할 수 있습니다.

1. 동일한 프로세스를 사용 하 여 나중에 프로덕션 환경에 배포를 사용 하 여 개발 컴퓨터에서 IIS에 응용 프로그램을 배포 합니다. Visual Studio 웹 프로젝트를 실행할 때 수행 하는 배포 프로세스를 테스트 하지는 IIS를 사용 하도록 구성할 수 있습니다. 이 메서드는 IIS에서 응용 프로그램이 올바르게 실행 하는 유효성 검사와 함께 배포 프로세스의 유효성을 검사 합니다.
2. 프로덕션 환경으로 거의 동일 하 게 테스트 환경에 응용 프로그램을 배포 합니다. 이 자습서에 대 한 프로덕션 환경에 Azure 앱 서비스의 웹 응용 프로그램 이므로 이상적인 테스트 환경은 Azure 앱 서비스에서 만든 추가 웹 앱입니다. 이 두 번째 웹 응용 프로그램을 테스트할 경우에 사용 하지만 프로덕션 웹 앱과 동일한 방식으로 설정 됩니다.

옵션 2를 테스트 하는 가장 안정적인 방법은 이며 그럴 경우 반드시 없으면 옵션 1을 수행 합니다. 그러나에 배포 하는 경우 타사 호스팅 공급자 옵션을 2 못할 수도 있습니다 또는 수 비용이 많이 들며, 있으므로이 자습서 시리즈 두 메서드를 보여 줍니다. 옵션 2에 대 한 지침에 제공 되는 [프로덕션 환경에 배포](deploying-to-production.md) 자습서입니다.

Visual Studio에서 웹 서버를 사용 하는 방법에 대 한 자세한 내용은 참조 [ASP.NET 웹 프로젝트에 대 한 Visual Studio의 웹 서버](https://msdn.microsoft.com/library/58wxa9w5.aspx)합니다.

미리 알림: 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 반드시 확인는 [문제 해결 페이지](troubleshooting.md)합니다.

## <a name="install-iis"></a>IIS 설치

개발 컴퓨터에서 IIS에 배포 하려면 IIS 있어야 하 고 웹 배포 설치 합니다. 웹 배포는 Visual Studio와 함께 기본적으로 설치 하지만 IIS 기본 Windows 8 또는 Windows 7 구성에 포함 되지 않습니다. IIS를 이미 설치한 경우 기본 응용 프로그램 풀.NET 4에 이미 설정 되어 있으면를 건너뜁니다 [절로](#sqlexpress)합니다.

1. 사용 하는 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx) 를 사용 하 여 웹 플랫폼 설치 관리자는 IIS에 대 한 권장된 구성이 설치 하 고 IIS 및 웹에 대 한 필수 구성 요소를 자동으로 설치 하기 때문에 IIS 및 웹 배포를 설치 하려면 필요한 경우 배포 합니다.

    IIS 및 웹 배포를 설치 하려면 웹 플랫폼 설치 관리자를 실행 하려면 다음 링크를 사용 합니다. 웹 플랫폼 설치 관리자를 이미 설치한 경우 IIS, 웹 배포 또는 해당 필수 구성 요소 중 하나를 누락 된 것만 설치 합니다.

    - [IIS 및 WebPI를 사용 하 여 웹 배포 설치](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

    IIS 7을 설치할 나타내는 메시지가 표시 됩니다. Windows 8, IIS 8 용 하지만 Windows 8에 대 한 링크 works 다음 단계를 수행 하 여 ASP.NET 4.5가 설치 되어 있는지 확인 합니다.

    1. 열기 **제어판**, **프로그램 및 기능**, **Windows 기능 설정 또는 해제**합니다.
    2. 확장 **인터넷 정보 서비스**, **World Wide Web 서비스**, 및 **응용 프로그램 개발 기능**합니다.
    3. 다음 사항을 확인 **ASP.NET 4.5** 을 선택 합니다.

        ![ASP.NET 4.5를 선택 합니다.](deploying-to-iis/_static/image1.png)

IIS를 설치한 후 실행 **IIS 관리자** 를.NET Framework 버전 4 기본 응용 프로그램 풀에 할당 되어 있는지 확인 합니다.

1. 열려는 WINDOWS + r의 **실행** 대화 상자.

    (또는 Windows 8에서 입력 "run"는 **시작** 페이지 또는 Windows 7에서 선택 **실행** 에서 **시작** 메뉴. 경우 **실행** 에 없는 **시작** 메뉴 작업 표시줄을 마우스 오른쪽 단추로 클릭 합니다. **속성**을 선택는 **시작 메뉴** 탭에서 **사용자 지정**를 선택 하 고 **명령을 실행**.)
2. "Inetmgr"를 입력 한 다음 클릭 **확인**합니다.
3. 에 **연결** 창에서 서버 노드를 확장 하 고 선택 **응용 프로그램 풀**합니다. 에 **응용 프로그램 풀** 창 경우 **DefaultAppPool** 은 다음 섹션으로 건너뛰십시오.NET framework 버전 4는 다음 그림과 같이 할당 합니다.

    [![Inetmgr_showing_4.0_app_pools](deploying-to-iis/_static/image3.png)](deploying-to-iis/_static/image2.png)
4. 두 개의 응용 프로그램 풀을 참조 하는 경우.NET Framework 2.0으로 설정 되어 두 값을 함께 IIS에서 ASP.NET 4를 설치 해야 합니다.

    Windows 8 되도록 ASP.NET 4.5를 설치 하면 섹션 또는 참조 이전 지침을 참조 하십시오. [이 KB 문서](https://support.microsoft.com/kb/2736284)합니다. Windows 7을 마우스 오른쪽 단추로 클릭 하 여 명령 프롬프트 창을 열고 **명령 프롬프트** windows에서 **시작** 메뉴에서 **관리자 권한으로 실행**합니다. 그러고 나 서 [aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) 다음 명령을 사용 하 여 IIS에서 ASP.NET 4를 설치 합니다. (32 비트 시스템 "프레임 워크"와 "Framework64"를 대체 합니다.)

    [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

    이 명령은.NET Framework 4에 대 한 새 응용 프로그램 풀을 만듭니다. 하지만 기본 응용 프로그램 풀은 계속 2.0으로 설정 됩니다. 배포 하는 응용 프로그램.NET 4를 대상으로 하는 해당 응용 프로그램 풀에 이므로.NET 4로 응용 프로그램 풀을 변경 해야 합니다.
5. 작업창을 닫은 경우 **IIS 관리자**, 다시 실행, 서버 노드를 확장 하 고 클릭 **응용 프로그램 풀** 표시 하는 **응용 프로그램 풀** 다시 창.
6. 에 **응용 프로그램 풀** 창에서 클릭 **DefaultAppPool**, 한 다음는 **동작** 창 클릭 **기본 설정**합니다.

    [![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image5.png)](deploying-to-iis/_static/image4.png)
7. 에 **응용 프로그램 풀 편집** 대화 상자에서 변경 **.NET Framework 버전** 를 **.NET Framework v4.0.30319** 클릭 **확인**합니다.

    [![Selecting_.NET_4_for_DefaultAppPool](deploying-to-iis/_static/image7.png)](deploying-to-iis/_static/image6.png)

IIS, 웹 응용 프로그램을 게시할 준비가 되었습니다. 그러나 먼저 수행할 수 있는 테스트 환경에서 사용할 데이터베이스를 만들 수 있습니다.

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a>SQL Server Express 설치

LocalDB은 테스트 환경에 설치 된 SQL Server Express가 필요 하므로 IIS에서 작동 하도록 설계 되지 않았습니다. Visual Studio 2010 SQL Server Express를 사용 중인 경우 기본적으로 이미 설치 되었습니다. Visual Studio 2012를 사용 하는 경우 설치 해야 합니다.

SQL Server Express를 설치 하려면 설치에서 [다운로드 센터: Microsoft SQL Server 2012 Express](https://www.microsoft.com/download/details.aspx?id=29062) 클릭 하 여 [ENU\x64\SQLEXPR\_x64\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLEXPR_x64_ENU.exe) 또는 [ ENU\x86\SQLEXPR\_x86\_ENU.exe](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLEXPR_x86_ENU.exe)합니다. 잘못 선택 하면 시스템에 대 한 것을 설치 하지 하 고 다른 하나를 시도할 수 있습니다.

SQL Server 설치 센터의 첫 번째 페이지에서 클릭 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**, 기본 선택 항목을 수락 하 여 지침을 따릅니다. 설치 마법사에서 기본 설정을 적용 합니다. 설치 옵션에 대 한 자세한 내용은 참조 [(설치) 설치 마법사에서 SQL Server 2012 설치](https://msdn.microsoft.com/library/ms143219.aspx)합니다.

## <a name="create-sql-server-express-databases-for-the-test-environment"></a>테스트 환경에 대 한 SQL Server Express 데이터베이스 만들기

Contoso 대학교 응용 프로그램 데이터베이스가 두 개인: 멤버 자격 데이터베이스 및 응용 프로그램 데이터베이스입니다. 두 개의 서로 다른 데이터베이스 또는 단일 데이터베이스에 이러한 데이터베이스를 배포할 수 있습니다. 응용 프로그램 데이터베이스 및 멤버 자격 데이터베이스 간의 데이터베이스 조인을 수행 하기 위해 결합 할 수 있습니다. 제 3 자 호스팅 공급자에 게 배포 하는 경우 호스팅 계획 결합 하는 이유가 제공 합니다. 예를 들어, 호스팅 공급자는 여러 데이터베이스에 대 한 추가 요금을 청구할 수 또는 둘 이상의 데이터베이스도 허용 하지 않을 수 있습니다.

이 자습서에서는 테스트 환경에서 두 개의 데이터베이스를 준비 및 프로덕션 환경에서 하나의 데이터베이스를 배포 합니다.

**보기** 메뉴에서 Visual Studio 선택 **서버 탐색기** (**데이터베이스 탐색기** Visual Web Developer에서)를 마우스 오른쪽 단추로 클릭 한 다음 **데이터 연결**  선택 **새 SQL Server 데이터베이스 만들기**합니다.

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

에 **새 SQL Server 데이터베이스 만들기** 대화 상자에 입력 ". \SQLExpress"에 **서버 이름** 상자와 "aspnet ContosoUniversity"에 **새 데이터베이스 이름** 다음 상자 클릭 **확인**합니다.

![Aspnet ContosoUniversity 만들기](deploying-to-iis/_static/image9.png)

"ContosoUniversity" 라는 새 SQL Server Express School 데이터베이스를 만들려면 동일한 절차를 따릅니다.

**서버 탐색기** 이제 두 개의 새 데이터베이스를 표시 합니다.

![서버 탐색기에서 새 데이터베이스](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a>새 데이터베이스에 대 한 권한 부여 스크립트 만들기

응용 프로그램이 개발 컴퓨터에 IIS에서 실행, 응용 프로그램이 기본 응용 프로그램 풀 자격 증명을 사용 하 여 데이터베이스에 액세스 합니다. 그러나 기본적으로 응용 프로그램 풀 id 없는 데이터베이스를 열 수 있는 권한이 있습니다. 따라서 해당 권한을 부여 하는 스크립트를 실행 해야 할 수도 있습니다. 이 섹션의 수를 실행 하는 IIS에서 실행 될 때 응용 프로그램 데이터베이스를 열 수 있는지 확인 하려면 이후 스크립트를 만듭니다.

(하지 프로젝트 중 하나), 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **새 항목 추가**, 새을 만들려면 **SQL 파일** 라는 *Grant.sql*합니다. 파일에 다음 SQL 명령을 복사 하 고 저장 하 고 파일을 닫습니다.

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

> [!NOTE]
> 이 스크립트는이 자습서에서는 지정 된 대로 SQL Server Express 2012와 Windows 8 또는 Windows 7에서 IIS 설정을 사용 하 여 작동 하도록 설계 되었습니다. Windows 또는 SQL Server의 다른 버전을 사용 하는 또는를 설정한 경우 IIS 컴퓨터에 다르게이 스크립트에 대 한 변경 해야 할 수 있습니다. SQL Server 스크립트에 대 한 자세한 내용은 참조 [SQL Server 온라인 설명서](https://go.microsoft.com/fwlink/?LinkId=132511)합니다.


> [!NOTE] 
> 
> **보안 정보** 이 스크립트는 db\_은 프로덕션 환경에 맞게 해야 런타임 시 데이터베이스에 액세스 하는 사용자에 게 사용 권한 소유자입니다. 일부 시나리오에서 배포에 대 한 사용 권한을 업데이트 하 고 실행된 시간에 대 한 데이터 읽기 및 쓰기에 권한이 있는 다른 사용자 지정의 전체 데이터베이스 스키마가 있는 사용자를 지정 하는 것이 좋습니다. 자세한 내용은 참조 [Code First 마이그레이션에 대 한 자동 Web.config 변경 내용 검토](#reviewingmigrations) 이 자습서의 뒷부분에 나오는 합니다.


<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a>응용 프로그램 데이터베이스의 권한 부여 스크립트를 실행 합니다.

스크립트를 실행 grant 멤버 자격 데이터베이스에 배포 하는 동안 해당 데이터베이스 배포 dbDacFx 공급자를 사용 하기 때문에 게시 프로필을 구성할 수 있습니다. 응용 프로그램 데이터베이스를 배포 하는 Code First 마이그레이션을 배포 하는 동안 스크립트를 실행할 수 없습니다. 따라서 응용 프로그램 데이터베이스에 배포 하기 전에 스크립트를 수동으로 실행 해야 합니다.

1. Visual Studio에서 열고는 *Grant.sql* 앞에서 만든 파일입니다.
2. **연결**을 클릭합니다. 

    ![연결 단추](deploying-to-iis/_static/image11.png)
3. 에 **서버에 연결** 대화 상자에 입력 *. \SQLExpress* 로 **서버 이름**, 클릭 하 고 **연결**합니다.
4. 데이터베이스 드롭 다운 목록에서 선택 **ContosoUniversity**, 클릭 하 고 **Execute**합니다. 

    ![](deploying-to-iis/_static/image12.png)

기본 응용 프로그램 풀 id는 데이터베이스 테이블을 만드는 응용 프로그램을 실행 하는 경우 Code First 마이그레이션에 대 한 응용 프로그램 데이터베이스에 충분 한 권한이 되었습니다.

## <a name="publish-to-iis"></a>IIS에 게시

여러 가지 방법으로 Visual Studio 및 웹 배포를 사용 하 여 IIS를 배포할 수 있습니다.

- One-click 게시 하는 Visual Studio를 사용 합니다.
- 명령줄에서 게시 합니다.
- 만들기는 *배포 패키지* 하 고 IIS 관리자 UI를 사용 하 여 설치 합니다. 배포 패키지를 구성 하는 *.zip* 모든 파일 및 IIS에서 사이트를 설치 하는 데 필요한 메타 데이터가 포함 된 파일입니다.
- 배포 패키지를 만들고 명령줄을 사용 하 여 설치 합니다.

프로세스 서 자동화 하려면 Visual Studio를 설정 하려면 이전 자습서에서 배포 작업은 이러한 모든 메서드에 적용 됩니다. 이 자습서를 사용 하 여 이러한 메서드의 처음 두 합니다. 배포 패키지를 사용 하는 방법에 대 한 정보를 참조 하십시오. [작성 및 웹 배포 패키지를 설치 하 여 웹 응용 프로그램을 배포](https://go.microsoft.com/fwlink/p/?LinkId=282413#package) Visual Studio 및 ASP.NET에 대해 웹 배포 콘텐츠 맵에 있습니다.

게시 하기 전에 Visual Studio를 관리자 모드로 실행 되 고 있는지를 확인 합니다. 표시 되지 않으면 **(관리자)** 제목 표시줄에 Visual Studio를 닫습니다. Windows 8에서 **시작** 페이지 또는 Windows 7 **시작** 메뉴에서 사용 중인 Visual Studio 버전에 대 한 아이콘을 마우스 오른쪽 단추로 클릭 하 고 선택 **관리자 권한으로 실행**합니다. 관리자 모드는만 경우 게시 하는 IIS에 로컬 컴퓨터에 게시 하기 위한 필요 합니다.

### <a name="create-the-publish-profile"></a>게시 프로필 만들기

1. **솔루션 탐색기**ContosoUniversity 프로젝트 (ContosoUniversity.DAL 프로젝트 제외)를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.

    **웹 게시** 마법사가 나타납니다.

    ![게시 웹 마법사 프로필 탭](deploying-to-iis/_static/image13.png)
2. 드롭다운 목록에서 선택  **&lt;새로 만들기... &gt;**. (설치 된 최신 Visual Studio 업데이트가 적용 된 드롭다운 목록이 없는 않으며 단추를 클릭 하 여 처음부터 새 프로필 만들기는 **사용자 지정**.)
3. 에 **새 프로필** 대화 상자에서 "Test"를 입력 한 다음 클릭 **확인**합니다.

    마법사가 자동으로 이동 된 **연결** 탭 합니다.
4. 에 **서비스 URL** 상자에 입력 *localhost*합니다.
5. 에 **사이트/응용 프로그램** 상자에 입력 *기본 웹 사이트/ContosoUniversity*
6. 에 **대상 URL** 상자에 입력 합니다`http://localhost/ContosoUniversity`

    **대상 URL** 설정이 필요 하지 않습니다. Visual Studio 응용 프로그램 배포 완료 되 면 자동으로이 URL에 기본 브라우저를 엽니다. 배포 후 자동으로 열 수 브라우저를 사용 하지 않으려는 경우에이 상자를 비워 둡니다.
7. 클릭 **연결 유효성 검사** 설정이 올바른지 하 고 로컬 컴퓨터의 IIS에 연결할 수 있는지 확인 합니다.

    녹색 확인 표시가 성공적으로 연결 되었는지 확인 합니다.

    ![게시 웹 마법사 연결 탭](deploying-to-iis/_static/image14.png)
8. 클릭 **다음** 으로 이동 하 여 **설정을** 탭 합니다.
9. **구성** 드롭다운 목록 상자에 배포 하려면 빌드 구성을 지정 합니다. 릴리스의 기본값으로 설정 둡니다. 이 자습서에서는 디버그 빌드를 배포 하지 않습니다.
10. 확장 **파일 게시 옵션**를 선택한 후 **응용 프로그램에서 파일을 제외\_데이터 폴더**합니다.

    응용 프로그램은 로컬 SQL Server Express 인스턴스에에서 만든 데이터베이스에 액세스 테스트 환경에서 하지.mdf 파일에 *앱\_데이터* 폴더입니다.
11. 둡니다는 **게시 하는 동안 Precompile** 및 **대상에서 추가 파일 제거** 확인란의 선택을 취소 합니다.

    ![설정 탭에서 파일 게시 옵션](deploying-to-iis/_static/image15.png)

    매우 큰 사이트;에 주로 유용 하는 옵션은 미리 컴파일 처음으로 사이트를 게시 한 후에 페이지를 요청에 대 한 페이지 시작 시간을 줄일 수 있습니다.

    이 첫 번째 배포 하 고 있을 수 없습니다 파일이 대상 폴더에 아직 추가 파일 제거 필요가 없습니다.

    > [!NOTE] 
    > 
    > [!CAUTION]
    > 선택 하는 경우 **추가 파일 제거** 같은 사이트로 후속 배포의 경우 어떤 파일이 삭제 됩니다. 배포 하기 전에 미리 볼 있는 미리 보기 기능을 사용 하는 있는지 확인 합니다. 예상 되는 동작은 웹 배포 프로젝트에서 삭제 된 대상 서버에서 파일 삭제 됩니다. 그러나 비교 원본 및 대상 폴더 아래에서 전체 폴더 구조, 있으며 일부 시나리오에서 웹 배포를 삭제할 수 있습니다 파일을 삭제 하려면.
    > 
    > 예를 들어 있는 경우 웹 응용 프로그램 서버에서 하위 폴더에 루트 폴더에 프로젝트를 배포 하는 경우, 하위 폴더 삭제 됩니다. Contoso.com에서 기본 사이트에 대 한 프로젝트 및 다른 프로젝트의 contoso.com/blog 블로그에 대 있을 수 있습니다. 블로그 응용 프로그램은 하위 폴더에 있습니다. 주 사이트를 배포할 때 대상에서 추가 파일 제거를 선택 하면 블로그 응용 프로그램이 삭제 됩니다.
    > 
    > 또 다른 예로, 응용 프로그램에 대 한\_데이터 폴더 예기치 않게 삭제 될 수 있습니다. 응용 프로그램에서 데이터베이스 파일을 저장 하는 SQL Server Compact와 같은 특정 데이터베이스\_데이터 폴더. 초기 배포 후 제외 앱을 선택 하므로 후속 배포 데이터베이스 파일을 복사 유지 않으려면\_웹 패키지 및 게시 탭에서 데이터입니다. 복사 하 고 나면, 선택한 대상에서 추가 파일 제거, 데이터베이스 파일 및 응용 프로그램을 설정한 경우\_자체 데이터 폴더에 게시 하면 다음에 삭제 됩니다.

### <a name="configure-deployment-for-the-membership-database"></a>멤버 자격 데이터베이스에 대 한 배포를 구성 합니다.

다음 단계에 적용 된 **DefaultConnection** 여기에 데이터베이스는 **데이터베이스** 대화 상자의 섹션.

1. 에 **원격 연결 문자열** 상자에 새 SQL Server Express 멤버 자격 데이터베이스를 가리키는 다음 연결 문자열을 입력 합니다.

    [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

    때문에 배포 프로세스 배포 된 Web.config 파일에서이 연결 문자열이 됩니다 **이 연결 문자열을 사용 하 여 런타임 시** 을 선택 합니다.

    연결 문자열을 얻을 수 있습니다 **서버 탐색기**합니다. **서버 탐색기**를 확장 하 고 **데이터 연결** 선택 하 고는  **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity** 데이터베이스에서 다음의 **속성** 창 복사는 **연결 문자열** 값입니다. 연결 문자열에 하나의 추가 설정을 삭제할 수 있는 해야: `Pooling=False`합니다.
2. 선택 **데이터베이스 업데이트**합니다.

    이렇게 하면 데이터베이스 스키마를 배포 하는 동안 대상 데이터베이스에서 만들 수 있습니다. 다음 단계를 실행 해야 하는 추가 스크립트를 지정: 기본 응용 프로그램 풀 및 데이터를 배포할 하나에 대 한 데이터베이스 액세스를 부여할 하나 있습니다.
3. 클릭 **데이터베이스 업데이트 구성**합니다.
4. 에 **데이터베이스 업데이트 구성** 대화 상자에서 클릭 **SQL 스크립트 추가** 이동한 후의 *Grant.sql* 솔루션 폴더에서 이전에 저장 하는 스크립트입니다.
5. 추가 하는 프로세스를 반복 하는 *aspnet-데이터-dev.sql* 스크립트입니다.

    ![멤버 자격 데이터베이스에 대 한 데이터베이스 업데이트를 구성 합니다.](deploying-to-iis/_static/image16.png)
6. **닫기**를 클릭합니다.

### <a name="configure-deployment-for-the-application-database"></a>응용 프로그램 데이터베이스에 대 한 배포를 구성 합니다.

Visual Studio에서 Entity Framework를 감지 하는 경우 `DbContext` 클래스에 항목을 만듭니다는 **데이터베이스** 포함 된 섹션에는 **Code First 마이그레이션 실행** 대신 확인란은  **데이터베이스를 업데이트** 확인란 합니다. 이 자습서에 대 한 Code First 마이그레이션을 배포를 지정 하려면 해당 확인란을 사용 합니다.

일부 시나리오에서 사용 중일 수 있습니다는 `DbContext` 데이터베이스 남기려는 마이그레이션 대신 dbDacFx 공급자를 사용 하 여 데이터베이스를 배포 합니다. 이 경우 참조 [마이그레이션 없이 코드 첫 번째 데이터베이스를 어떻게 배포 합니까?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) MSDN에서 ASP.NET 웹 배포 FAQ에 있습니다.

다음 단계에 적용 된 **SchoolContext** 여기에 데이터베이스는 **데이터베이스** 대화 상자의 섹션.

1. 에 **원격 연결 문자열** 상자에 새 SQL Server Express 응용 프로그램 데이터베이스를 가리키는 다음 연결 문자열을 입력 합니다.

    [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

    때문에 배포 프로세스 배포 된 Web.config 파일에서이 연결 문자열이 됩니다 **이 연결 문자열을 사용 하 여 런타임 시** 을 선택 합니다.

    응용 프로그램 데이터베이스 연결 문자열을 얻을 수 있습니다 **서버 탐색기** 멤버 자격을 받은 같은 방법으로 데이터베이스 연결 문자열이 있습니다.
2. 선택 **실행 Code First 마이그레이션을 (응용 프로그램 시작 시 실행)**합니다.

    이 옵션을 사용 하면 배포 프로세스를 지정 하도록 배포 된 Web.config 파일을 구성 하는 `MigrateDatabaseToLatestVersion` 이니셜라이저입니다. 자동으로이 이니셜라이저 응용 프로그램 배포 후 처음으로 데이터베이스에 액세스 하는 경우 데이터베이스에서 최신 버전에 게 업데이트 합니다.

### <a name="configure-publish-profile-transforms"></a>구성 프로필 변환 게시

1. 클릭 **닫기**, 클릭 하 고 **예** 물으면 변경 내용을 저장 하려는 경우.
2. **솔루션 탐색기**를 확장 하 고 **속성**를 확장 하 고 **PublishProfiles**합니다.
3. Rright 클릭 *Test.pubxml,* 클릭 하 고 **Config 변환 추가**합니다.

    ![추가 구성 변환 메뉴](deploying-to-iis/_static/image17.png)

    Visual Studio 만듭니다는 *Web.Test.config* 변환 파일을 엽니다.
4. 에 *Web.Test.config* 변환 파일을 여는 바로 뒤에 다음 코드를 삽입 구성 태그입니다.

    [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    테스트를 사용 하는 경우 게시 프로필,이 변환은 환경 표시기 "Test"를 설정 합니다. 배포 된 사이트에서 "Contoso 대학" H1 제목을 후 "(테스트)"를 표시 됩니다.
5. 파일을 저장한 후 닫습니다.
6. 마우스 오른쪽 단추로 클릭는 *Web.Test.config* 파일을 클릭 하 여 **미리 보기 변환** 코딩 변환 된 예상된 변경 내용이 생성 되도록 합니다.

    **Web.config 미리 보기** 창 모두에 적용 한 결과 표시는 *Web.Release.config* 변환 및 *Web.Test.config* 변환 합니다.

### <a name="preview-the-deployment-updates"></a>배포 업데이트를 미리 봅니다.

1. 열기는 **웹 게시** 마법사를 다시 (ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**).
2. **미리 보기** 탭에서 다음 사항을 확인는 **테스트** 프로필을 선택 된 상태 이며 클릭 한 다음 **미리 보기 시작** 복사 될 파일 목록을 볼 수 있습니다.

    ![미리 보기 단추](deploying-to-iis/_static/image18.png)

    ![게시 미리 보기](deploying-to-iis/_static/image19.png)

    클릭할 수도 있습니다는 **미리 보기 데이터베이스** 멤버 자격 데이터베이스에서 실행 될 스크립트를 보려면이 링크를 합니다. (스크립트가 실행 됩니다 Code First 마이그레이션을 배포에 대 한 응용 프로그램 데이터베이스에 대 한 미리 보려면 할 것이 없습니다.)
3. **게시**를 클릭합니다.

    Visual Studio 관리자 모드에 없는 경우 사용 권한 오류를 나타내는 오류 메시지가 표시 될 수 있습니다. 이 경우 Visual Studio를 닫습니다 관리자 모드에서 연 하 고 다시 게시 하려고 합니다.

    관리자 모드에서 Visual Studio는 경우는 **출력** 성공 창 보고서를 작성 및 게시 합니다.

    ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

    URL을 입력 한 경우는 **대상 URL** 게시 프로필에 상자 **연결** 탭 브라우저는 로컬 컴퓨터에 IIS에서 실행 되는 Contoso 대학 홈 페이지로 자동으로 열립니다.

## <a name="test-in-the-test-environment"></a>테스트 환경에서 테스트

환경 표시기 "(테스트)"가 표시 "(Dev)" 대신 보여 주는 하는 *Web.config* 환경 표시기에 대 한 변환을 성공적으로 수행 합니다.

실행 된 **강사** 페이지 Code First 있는지 instructor 데이터로 데이터베이스 시 딩을 확인 합니다. 이 페이지를 선택 하면 Code First는 데이터베이스를 만들고 다음을 실행 하기 때문에 로드 하는 데 몇 분 정도 걸릴 수 있습니다는 `Seed` 메서드. (것 하지 않은 응용 프로그램 데이터베이스에 아직 액세스 시도 하지 않은 하기 때문에 홈 페이지에 했을 때 만듭니다.)

클릭는 **학생** 배포 된 데이터베이스에 없는 학생을 확인 하는 탭 합니다.

선택 **추가 학생** 에서 **학생** 메뉴는 학생을 추가 하 고 다음에 새 학생을 볼는 **학생** 페이지는 데이터베이스에 성공적으로 쓸 수 있는지 확인 합니다. .

**Courses** 메뉴 선택 **업데이트 크레딧**합니다. **업데이트 크레딧** 페이지에는 관리자 권한이 필요 하므로 **로그인** 페이지가 표시 됩니다. 이전 버전 ("admin" 및 "devpwd")를 만든 관리자 계정 자격 증명을 입력 합니다. **업데이트 크레딧** 이전 자습서에서 만든 관리자 계정을 테스트 환경에 잘못 배포 된 검증 페이지가 표시 됩니다.

되어 있는지 확인 한 *Elmah* 폴더에 존재는 *c:\inetpub\wwwroot\ContosoUniversity* 자리 표시자 파일에 있는 폴더입니다.

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a>Code First 마이그레이션에 대 한 자동 Web.config 변경 내용 검토

열기는 *Web.config* 파일에서 배포 응용 프로그램에서 *C:\inetpub\wwwroot\ContosoUniversity* 여기서 배포 프로세스를 Code First 마이그레이션이 자동으로 구성 하면 확인할 수 있습니다 최신 버전으로 데이터베이스를 업데이트 합니다.

![](deploying-to-iis/_static/image21.png)

배포 프로세스는 데이터베이스 스키마 업데이트에 대 한 단독으로 사용 하려면 Code First 마이그레이션에 대 한 새 연결 문자열도 생성 됩니다.

![Database_Publish 연결 문자열](deploying-to-iis/_static/image22.png)

이 추가 연결 문자열을 사용 하면 데이터베이스 스키마 업데이트에 대 한 하나의 사용자 계정 및 데이터 액세스 응용 프로그램에 대 한 다른 사용자 계정을 지정할 수 있습니다. 예를 들어 할당할 수 있습니다는 **db\_소유자** Code First 마이그레이션을에 역할 및 **db\_datareader** 및 **db\_datawriter**응용 프로그램에는 역할입니다. 데이터베이스 스키마 변경에서 응용 프로그램의 잠재적 악성 코드를 방지 하는 일반적인 심층 방어 패턴입니다. (예를 들어이 발생할 수 있습니다에 SQL 주입 공격에 성공 합니다.) 이 패턴은이 자습서에서 사용 되지 않습니다. 시나리오에이 패턴을 구현 하려면 다음 단계를 수행 하 여 수행할 수 있습니다.

1. 에 **설정** 탭은 **웹 게시** 마법사에서 전체 데이터베이스 스키마 업데이트 권한이 있는 사용자를 지정 하는 연결 문자열을 입력 한 선택을 취소는 **이 연결 문자열 사용 런타임 시** 확인란 합니다. 이 배포 된 Web.config 파일에는 `DatabasePublish` 연결 문자열입니다.
2. 응용 프로그램 실행 시 사용 하는 연결 문자열에 대 한 Web.config 파일 변환을 만듭니다.

## <a name="summary"></a>요약

이제 개발 컴퓨터에서 IIS에 응용 프로그램을 배포 하 고 있는 테스트 보았습니다.

![테스트에 홈 페이지](deploying-to-iis/_static/image23.png)

배포 프로세스 올바른 위치로 (배포 원하지 파일 제외), 응용 프로그램의 콘텐츠를 복사 하 고도 해당 웹 배포 구성 IIS 올바르게 배포 하는 동안 확인 합니다. 다음 자습서에서는 아직 수행 하지 않은 배포 작업을 발견 하는 한 더 많은 테스트 실행:에 폴더 사용 권한을 설정의 *Elmah* 폴더입니다.

## <a name="more-information"></a>추가 정보

Visual Studio에서 IIS 또는 IIS Express를 실행 하는 방법에 대 한 내용은 다음 리소스를 참조 합니다.

- [IIS Express 개요](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) IIS.net 사이트에 있습니다.
- [IIS Express 소개](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) Scott Guthrie의 블로그입니다.
- [ASP.NET 웹 프로젝트에 Visual Studio의 서버를 웹](https://msdn.microsoft.com/library/58wxa9w5.aspx)합니다.
- [주요 차이점 간의 IIS 및 ASP.NET 개발 서버](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) ASP.NET 사이트의 합니다.

어떤 문제에 대 한 정보는 보통 신뢰 수준에서 응용 프로그램이 실행 될 때 발생할 수 있습니다, 참조 [보통 신뢰에서 ASP.NET 응용 프로그램 호스팅](http://www.4guysfromrolla.com/articles/100307-1.aspx) Rolla 사이트에서 4 Guy에 있습니다.

>[!div class="step-by-step"]
[이전](project-properties.md)
[다음](setting-folder-permissions.md)
