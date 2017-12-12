---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
title: "SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: iis 5 / 12-테스트 환경으로 배포 | Microsoft Docs"
author: tdykstra
description: "이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시) ASP.NET Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: 493b2a66-816c-485c-8315-952ed1085ccc
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
msc.type: authoredcontent
ms.openlocfilehash: a5538744dfaff76f28c5f17d8f5d782ef3f6c118
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-iis-as-a-test-environment---5-of-12"></a>SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: iis 5 / 12-테스트 환경으로 배포
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시)는 ASP.NET 웹에 대 한 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다. 웹 게시 업데이트를 설치 하는 경우에 Visual Studio 2010을 사용할 수 있습니다. 계열에 대 한 소개를 참조 하십시오. [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.
> 
> Visual Studio 2012 RC 릴리스 이후 도입 된 배포 기능을 표시, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다. 및 Azure 앱 서비스 웹 앱을 배포 하는 방법을 보여 줍니다. 하는 자습서를 참조 하십시오. [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)합니다.


## <a name="overview"></a>개요

이 자습서에서는 로컬 컴퓨터에서 IIS에 ASP.NET 웹 응용 프로그램을 배포 하는 방법을 보여 줍니다.

응용 프로그램을 개발 하는 경우 일반적으로 Visual Studio에서 실행 하 여 테스트 합니다. 기본적으로 Visual Studio 개발 서버 (Cassini 라고도 함)를 사용 하는이 의미 합니다. Visual Studio 개발 서버를 사용 하면 Visual Studio에서 개발 하는 동안 테스트를 쉽게 하지만 IIS와 동일 하 게 작동 하지 않습니다. 결과적으로, 것 Visual Studio에서 테스트 해야 하지만 호스팅 환경에서 IIS에 배포 될 때 실패 하는 경우 응용 프로그램은 제대로 실행 가능 합니다.

다음과 같은이 방법으로 응용 프로그램을 더욱 안정적으로 테스트할 수 있습니다.

1. Visual Studio에서 개발 하는 동안 테스트할 때 Visual Studio 개발 서버 대신 IIS Express 또는 전체 IIS를 사용 합니다. 이 메서드가 일반적으로 에뮬레이션 더 정확 하 게 IIS에서 사이트를 실행할 방법을 합니다. 그러나이 메서드는 테스트 배포 프로세스 하거나 확인 배포 프로세스의 결과 제대로 실행 됩니다.
2. 동일한 프로세스를 사용 하 여 나중에 프로덕션 환경에 배포를 사용 하 여 개발 컴퓨터에서 IIS에 응용 프로그램을 배포 합니다. 이 메서드는 IIS에서 응용 프로그램이 올바르게 실행 하는 유효성 검사와 함께 배포 프로세스의 유효성을 검사 합니다.
3. 최대한 가까운 프로덕션 환경과 테스트 환경에 응용 프로그램을 배포 합니다. 이 자습서에 대 한 프로덕션 환경에서 타사 호스팅 공급자 이므로 이상적인 테스트 환경 호스팅 공급자와 두 번째 계정을 것입니다. 테스트에이 두 번째 계정을 사용 합니다 하지만 프로덕션 계정으로는 동일한 방식으로 설정 됩니다.

이 자습서 2 옵션에 대 한 단계를 보여 줍니다. 옵션 3에 대 한 지침의 끝에서 제공 되는 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서에서는이 자습서의 끝에 있다면 옵션 1에 대 한 리소스에 대 한 링크입니다.

미리 알림: 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 반드시 확인는 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.

## <a name="configuring-the-application-to-run-in-medium-trust"></a>보통 신뢰 수준에서 실행 하도록 응용 프로그램 구성

IIS를 설치 하 고를 배포 하기 전에 실행 되 게 사이트 더 일반적인 공유 호스팅 환경에서와 같은 하기 위해 Web.config 파일 설정을 변경 합니다.

호스팅 공급자는 일반적으로 웹 사이트에서 실행 *보통 신뢰*, 즉, 몇 가지 할 수 없습니다. 예를 들어 응용 프로그램 코드 없습니다 Windows 레지스트리에 액세스할 및 수 없는 읽기 또는 쓰기 응용 프로그램의 폴더 계층 구조 외부 파일. 기본적으로 응용 프로그램에서 실행 *높은 신뢰* 로컬 컴퓨터에 의미 하는 응용 프로그램을 프로덕션에 배포할 때 실패 하 게 하는 것을 수행할 수 있습니다. 따라서 더 정확 하 게 반영 테스트 환경에서 프로덕션 환경을 하려면 보통 신뢰 수준에서 실행 되도록 응용 프로그램을 구성 합니다.

응용 프로그램 Web.config 파일에 추가 **신뢰** 요소에는 **system.web** 요소를이 예제에 나와 있는 것 처럼 합니다.

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample1.xml?highlight=4)]

응용 프로그램이 이제 로컬 컴퓨터에도 IIS에서 보통 신뢰에서 실행 됩니다. 이 설정을 사용 하면 프로덕션 환경에서 실패 하 게 작업을 수행할 응용 프로그램 코드에서 가능한 한 빨리 모든 시도 catch 하 있습니다.

> [!NOTE]
> Entity Framework Code First 마이그레이션을 사용 하는 경우 버전 5.0 나중에 설치 되어 있는지 확인 합니다. Entity Framework 버전 4.3에서에서 마이그레이션 데이터베이스 스키마를 업데이트 하려면 완전 신뢰가 필요 합니다.


## <a name="installing-iis-and-web-deploy"></a>설치할 IIS 및 웹 배포

개발 컴퓨터에서 IIS에 배포 하려면 IIS 있어야 하 고 웹 배포 설치 합니다. 기본 구성으로 Windows 7이 포함 되지 않습니다. IIS 및 웹 배포를 설치한 경우 다음 섹션으로 건너뜁니다.

사용 하는 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx) 를 사용 하 여 웹 플랫폼 설치 관리자는 IIS에 대 한 권장된 구성이 설치 하 고 IIS 및 웹에 대 한 필수 구성 요소를 자동으로 설치 하기 때문에 IIS 및 웹 배포를 설치 하려면 필요한 경우 배포 합니다.

IIS 및 웹 배포를 설치 하려면 웹 플랫폼 설치 관리자를 실행 하려면 다음 링크를 사용 합니다. 웹 플랫폼 설치 관리자를 이미 설치한 경우 IIS, 웹 배포 또는 해당 필수 구성 요소 중 하나를 누락 된 것만 설치 합니다.

- [IIS 및 WebPI를 사용 하 여 웹 배포 설치](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

## <a name="setting-the-default-application-pool-to-net-4"></a>.NET 4에 기본 응용 프로그램 풀을 설정합니다.

IIS를 설치한 후 실행 **IIS 관리자** 를.NET Framework 버전 4 기본 응용 프로그램 풀에 할당 되어 있는지 확인 합니다.

Windows에서 **시작** 메뉴 선택 **실행**"inetmgr"를 입력 한 다음 클릭 **확인**합니다. (하는 경우는 **실행** 명령에 속하지 않는 사용자 **시작** 메뉴에서 Windows 키와 R 열려는 눌러 수 있습니다. 또는 작업 표시줄을 마우스 오른쪽 단추로 클릭 합니다 **속성**, 선택는 **시작 메뉴** 탭을 클릭 **사용자 지정**, 선택 하 고 **명령을 실행**.)

에 **연결** 창에서 서버 노드를 확장 하 고 선택 **응용 프로그램 풀**합니다. 에 **응용 프로그램 풀** 창 경우 **DefaultAppPool** 은 다음 섹션으로 건너뛰십시오.NET framework 버전 4는 다음 그림과 같이 할당 합니다.

[![Inetmgr_showing_4.0_app_pools](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image1.png)

두 개의 응용 프로그램 풀을 참조 하는 경우.NET Framework 2.0으로 설정 되어 둘 모두 IIS에서 ASP.NET 4를 설치 해야 합니다.

- 마우스 오른쪽 단추로 클릭 하 여 명령 프롬프트 창을 열고 **명령 프롬프트** windows에서 **시작** 메뉴에서 **관리자 권한으로 실행**합니다. 그러고 나 서 [aspnet\_regiis.exe](https://msdn.microsoft.com/en-us/library/k6h9cz8h.aspx) 다음 명령을 사용 하 여 IIS에서 ASP.NET 4를 설치 합니다. (64 비트 시스템 "Framework64"와 "프레임 워크"를 대체 합니다.)

    [!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample2.cmd)]

    [![aspnet_regiis_installing_ASP.NET_4](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image3.png)

    이 명령은.NET Framework 4에 대 한 새 응용 프로그램 풀을 만듭니다. 하지만 기본 응용 프로그램 풀은 계속 2.0으로 설정 됩니다. 배포 하는 응용 프로그램.NET 4를 대상으로 하는 해당 응용 프로그램 풀에 이므로.NET 4로 응용 프로그램 풀을 변경 해야 합니다.

작업창을 닫은 경우 **IIS 관리자**, 다시 실행, 서버 노드를 확장 하 고 클릭 **응용 프로그램 풀** 표시 하는 **응용 프로그램 풀** 다시 창.

에 **응용 프로그램 풀** 창에서 클릭 **DefaultAppPool**, 한 다음는 **동작** 창 클릭 **기본 설정**합니다.

[![Inetmgr_selecting_Basic_Settings_for_app_pool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image5.png)

에 **응용 프로그램 풀 편집** 대화 상자에서 변경 **.NET Framework 버전** 를 **.NET Framework v4.0.30319** 클릭 **확인**합니다.

[![Selecting_.NET_4_for_DefaultAppPool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image7.png)

이제 IIS에 게시할 준비가 되었습니다.

## <a name="publishing-to-iis"></a>IIS에 게시

여러 가지 방법으로 Visual Studio 2010 및 웹 배포를 사용 하 여 배포할 수 있습니다.

- One-click 게시 하는 Visual Studio를 사용 합니다.
- 만들기는 *배포 패키지* 하 고 IIS 관리자 UI를 사용 하 여 설치 합니다. 배포 패키지를 구성 하는 *.zip* 모든 파일 및 IIS에서 사이트를 설치 하는 데 필요한 메타 데이터가 포함 된 파일입니다.
- 배포 패키지를 만들고 명령줄을 사용 하 여 설치 합니다.

서 자동화 하려면 Visual Studio를 설정 하려면 이전 자습서의 다음 세 가지 방법의 모든 배포 작업 적용 프로세스입니다. 이 자습서를 사용 하 여 이러한 메서드의 첫 번째입니다. 배포 패키지를 사용 하는 방법에 대 한 정보를 참조 하십시오. [ASP.NET 배포 콘텐츠 맵](https://msdn.microsoft.com/en-us/library/bb386521.aspx)합니다.

게시 하기 전에 Visual Studio를 관리자 모드로 실행 되 고 있는지를 확인 합니다. (Windows 7에서 **시작** 메뉴에서 사용 중인 Visual Studio 버전에 대 한 아이콘을 마우스 오른쪽 단추로 클릭 하 고 선택 **관리자 권한으로 실행**.) 관리자 모드는만 경우 게시 하는 IIS에 로컬 컴퓨터에 게시 하기 위한 필요 합니다.

**솔루션 탐색기**ContosoUniversity 프로젝트 (ContosoUniversity.DAL 프로젝트 제외)를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.

**웹 게시** 마법사가 나타납니다.

![Publish_Web_wizard_Profile_tab](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image9.png)

드롭다운 목록에서 선택  **&lt;새로 만들기... &gt;**.

에 **새 프로필** 대화 상자에서 "Test"를 입력 한 다음 클릭 **확인**합니다.

![New_Profile_dialog_box](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image10.png)

이 이름은 Web.Test.config의 중간 노드와 동일 변환 앞에서 만든 파일입니다. 이 관계는이 프로필을 사용 하 여 게시할 때 적용할 Web.Test.config 변환을 놓이게 되어 합니다.

마법사가 자동으로 이동 된 **연결** 탭 합니다.

에 **서비스 URL** 상자에 입력 *localhost*합니다.

에 **사이트/응용 프로그램** 상자에 입력 *기본 웹 사이트/ContosoUniversity*합니다.

에 **대상 URL** 상자에 입력 `http://localhost/ContosoUniversity`합니다.

**대상 URL** 설정이 필요 하지 않습니다. Visual Studio 응용 프로그램 배포 완료 되 면 자동으로이 URL에 기본 브라우저를 엽니다. 배포 후 자동으로 열 수 브라우저를 사용 하지 않으려는 경우에이 상자를 비워 둡니다.

![Publish_Web_wizard_Connection_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image11.png)

클릭 **연결 유효성 검사** 설정이 올바른지 하 고 로컬 컴퓨터의 IIS에 연결할 수 있는지 확인 합니다.

녹색 확인 표시가 성공적으로 연결 되었는지 확인 합니다.

![Publish_Web_wizard_Connection_tab_validated](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image12.png)

클릭 **다음** 으로 이동 하 여 **설정을** 탭 합니다.

**구성** 드롭다운 목록 상자에 배포 하려면 빌드 구성을 지정 합니다. 기본값은 원하는 대로 인 릴리스 합니다.

유지 된 **대상에서 추가 파일 제거** 확인란의 선택을 취소 합니다. 첫 번째 배포 이므로, 않습니다 있을 파일이 대상 폴더에 아직.

에 **데이터베이스** 섹션에서 다음 값에 대 한 연결 문자열 상자 입력 **SchoolContext**:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample3.cmd)]

때문에 배포 프로세스 배포 된 Web.config 파일에서이 연결 문자열이 됩니다 **이 연결 문자열을 사용 하 여 런타임 시** 을 선택 합니다.

또한 아래에서 **SchoolContext**선택, **Code First 마이그레이션을 적용**합니다. 이 옵션을 사용 하면 배포 프로세스를 지정 하도록 배포 된 Web.config 파일을 구성 하는 `MigrateDatabaseToLatestVersion` 이니셜라이저입니다. 자동으로이 이니셜라이저 응용 프로그램 배포 후 처음으로 데이터베이스에 액세스 하는 경우 데이터베이스에서 최신 버전에 게 업데이트 합니다.

에 대 한 연결 문자열 상자에서 **DefaultConnection**를 다음 값을 입력 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample4.cmd)]

둡니다 **데이터베이스 업데이트** 의 선택을 취소 합니다. 응용 프로그램에서.sdf 파일을 복사 하 여 멤버 자격 데이터베이스가 배포 될\_데이터를 숨기려면이 데이터베이스와 다른 작업을 수행 하는 배포 프로세스입니다.

![Publish_Web_wizard_Settings_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image13.png)

클릭 **다음** 으로 이동 하 여 **미리 보기** 탭 합니다.

에 **미리 보기** 탭을 클릭 **미리 보기 시작** 복사 될 파일 목록을 볼 수 있습니다.

![Publish_Web_wizard_Preview_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image14.png)

![Publish_Web_wizard_Preview_tab_Test_with_file_list](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image15.png)

**게시**를 클릭합니다.

Visual Studio 관리자 모드에 없는 경우 사용 권한 오류를 나타내는 오류 메시지가 표시 될 수 있습니다. 이 경우 Visual Studio를 닫습니다 관리자 모드에서 연 하 고 다시 게시 하려고 합니다.

관리자 모드에서 Visual Studio는 경우는 **출력** 성공 창 보고서를 작성 및 게시 합니다.

![Output_window_publish_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image16.png)

브라우저는 로컬 컴퓨터에 IIS에서 실행 되는 Contoso 대학 홈 페이지로 자동으로 열립니다.

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image17.png)

## <a name="testing-in-the-test-environment"></a>테스트 환경에서 테스트

환경 표시기 "(테스트)"가 표시 "(Dev)" 대신 보여 주는 하는 *Web.config* 환경 표시기에 대 한 변환을 성공적으로 수행 합니다.

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image19.png)

실행 된 **학생** 페이지는 배포 된 데이터베이스에 없는 학생에 있는지 확인 합니다. 이 페이지를 선택 하는 경우 Code First는 데이터베이스를 만들고 다음을 실행 하기 때문에 로드 하는 데 몇 분 정도 걸릴 수 있습니다는 `Seed` 메서드. (것 하지 않은 응용 프로그램 데이터베이스에 아직 액세스 시도 하지 않은 하기 때문에 홈 페이지에 했을 때 만듭니다.)

[![Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image21.png)

실행 된 **강사** 페이지 Code First 있는지 instructor 데이터로 데이터베이스 시드 된 확인:

[![Instructors_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image23.png)

선택 **추가 학생** 에서 **학생** 메뉴는 학생을 추가 하 고 다음에 새 학생을 볼는 **학생** 페이지는 데이터베이스에 성공적으로 쓸 수 있는지 확인 합니다. :

[![Add_Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image26.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image25.png)

[![Students_page_with_new_student_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image28.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image27.png)

**Courses** 메뉴 선택 **업데이트 크레딧**합니다. **업데이트 크레딧** 페이지에는 관리자 권한이 필요 하므로 **로그인** 페이지가 표시 됩니다. 이전 버전 ("admin" 및 "Pa$ w0rd")를 만든 관리자 계정 자격 증명을 입력 합니다. **업데이트 크레딧** 이전 자습서에서 만든 관리자 계정을 테스트 환경에 잘못 배포 된 검증 페이지가 표시 됩니다.

[![Log_In_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image30.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image29.png)

[![Update_Credits_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image32.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image31.png)

되어 있는지 확인 한 *Elmah* 폴더가 자리 표시자 파일에 있습니다.

[![Elmah_folder_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image34.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image33.png)

<a id="efcfmigrations"></a>

## <a name="reviewing-the-automatic-webconfig-changes-for-code-first-migrations"></a>Code First 마이그레이션에 대 한 자동 Web.config 변경 내용 검토

열기는 *Web.config* 파일에서 배포 응용 프로그램에서 *C:\inetpub\wwwroot\ContosoUniversity* 여기서 배포 프로세스를 Code First 마이그레이션이 자동으로 구성 하면 확인할 수 있습니다 최신 버전으로 데이터베이스를 업데이트 합니다.

![](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image35.png)

배포 프로세스는 데이터베이스 스키마 업데이트에 대 한 단독으로 사용 하려면 Code First 마이그레이션에 대 한 새 연결 문자열도 생성 됩니다.

![DatabasePublish_connection_string](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image36.png)

이 추가 연결 문자열을 사용 하면 데이터베이스 스키마 업데이트에 대 한 하나의 사용자 계정 및 데이터 액세스 응용 프로그램에 대 한 다른 사용자 계정을 지정할 수 있습니다. 예를 들어 db를 할당할 수 있습니다\_소유자 역할의 Code First 마이그레이션 및 db\_datareader 및 db\_응용 프로그램에 datawriter 역할입니다. 데이터베이스 스키마 변경에서 응용 프로그램의 잠재적 악성 코드를 방지 하는 일반적인 심층 방어 패턴입니다. (예를 들어이 발생할 수 있습니다에 SQL 주입 공격에 성공 합니다.) 이 패턴은이 자습서에서 사용 되지 않습니다. SQL Server Compact에 적용 되지 않습니다 하 한이 시리즈의 자습서의 뒷부분에서 SQL Server로 마이그레이션할 때는 적용 되지 않습니다. Cytanium 사이트 Cytanium에서 만드는 SQL Server 데이터베이스에 액세스 하기 위한 하나의 사용자 계정을 제공 합니다. 시나리오에이 패턴을 구현할 수 있다면 다음 단계를 수행 하 여 수행할 수 있습니다.

1. 에 **설정** 탭은 **웹 게시** 마법사에서 전체 데이터베이스 스키마 업데이트 권한이 있는 사용자를 지정 하는 연결 문자열을 입력 한 선택을 취소는 **이 연결 문자열 사용 런타임 시** 확인란 합니다. 이 배포 된 Web.config 파일에는 `DatabasePublish` 연결 문자열입니다.
2. 응용 프로그램 실행 시 사용 하는 연결 문자열에 대 한 Web.config 파일 변환을 만듭니다.

이제 개발 컴퓨터에서 IIS에 응용 프로그램을 배포 하 고 있는 테스트 보았습니다. 배포 프로세스 올바른 위치로 (배포 원하지 파일 제외), 응용 프로그램의 콘텐츠를 복사 하 고도 해당 웹 배포 구성 IIS 올바르게 배포 하는 동안 확인 합니다. 다음 자습서에서는 아직 수행 하지 않은 배포 작업을 발견 하는 한 더 많은 테스트 실행:에 폴더 사용 권한을 설정의 *Elmah* 폴더입니다.

## <a name="more-information"></a>추가 정보

Visual Studio에서 IIS 또는 IIS Express를 실행 하는 방법에 대 한 내용은 다음 리소스를 참조 합니다.

- [IIS Express 개요](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) IIS.net 사이트에 있습니다.
- [IIS Express 소개](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) Scott Guthrie의 블로그입니다.
- [방법: Visual Studio에서 웹 프로젝트에 대 한 웹 서버를 지정](https://msdn.microsoft.com/en-us/library/ms178108.aspx)합니다.
- [주요 차이점 간의 IIS 및 ASP.NET 개발 서버](../deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) ASP.NET 사이트의 합니다.
- [ASP.NET MVC 또는 Web Forms 응용 프로그램 IIS 7에서 30 초 내에 테스트](https://blogs.msdn.com/b/rickandy/archive/2011/04/22/test-you-asp-net-mvc-or-webforms-application-on-iis-7-in-30-seconds.aspx) Rick Anderson의 블로그에서 합니다. 이 항목의 예제 이유 (Cassini) Visual Studio 개발 서버를 사용 하 여 안정적이 지 않습니다 IIS Express에서 테스트와 IIS Express에서 테스트 된 이유 IIS에서 테스트 하는 것 만큼 안정적를 제공 합니다.

어떤 문제에 대 한 정보는 보통 신뢰 수준에서 응용 프로그램이 실행 될 때 발생할 수 있습니다, 참조 [보통 신뢰에서 ASP.NET 응용 프로그램 호스팅](http://www.4guysfromrolla.com/articles/100307-1.aspx) Rolla 사이트에서 4 Guy에 있습니다.

>[!div class="step-by-step"]
[이전](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
[다음](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
