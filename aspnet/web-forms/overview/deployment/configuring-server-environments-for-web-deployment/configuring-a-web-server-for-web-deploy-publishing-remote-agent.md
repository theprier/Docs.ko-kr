---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
title: 게시 (원격 에이전트)를 배포할 웹에 대 한 웹 서버를 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 웹 게시 및 IIS 웹 배포를 사용 하 여 배포를 지원 하기 위해 인터넷 정보 서비스 (IIS) 웹 서버를 구성 하는 방법을 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 239c7aa8-d09a-4d02-9c0e-6bd52be5f0d5
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
msc.type: authoredcontent
ms.openlocfilehash: 9f3a55c5e68e61a2d7907c765209d3786e05a485
ms.sourcegitcommit: 1b94305cc79843e2b0866dae811dab61c21980ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2018
ms.locfileid: "34473209"
---
<a name="configuring-a-web-server-for-web-deploy-publishing-remote-agent"></a>웹 배포 게시 (원격 에이전트)에 대 한 웹 서버를 구성 합니다.
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 웹 게시 및 IIS 웹 배포 도구 (웹 배포) 원격 에이전트 서비스를 사용 하 여 배포를 지원 하기 위해 인터넷 정보 서비스 (IIS) 웹 서버를 구성 하는 방법을 설명 합니다.
> 
> 웹 배포 2.0 이상으로 작업할 때 다음 3 가지 주요 방법 응용 프로그램이 나 웹 서버에 사이트를 가져오는 데 사용할 수 있습니다. 다음과 같은 작업을 수행할 수 있습니다.
> 
> - 사용 하 여는 *원격 에이전트 서비스를 배포 하는 웹*합니다. 이 방법은 웹 서버의 적게 구성 해야 하지만 아무 것도 서버에 배포 하기 위해 로컬 서버 관리자의 자격 증명을 제공 해야 합니다.
> - 사용 하 여는 *웹 배포 처리기*합니다. 이 방법은 훨씬 더 복잡 한 고 웹 서버를 설정 하려면 초기 더 많은 노력이 필요 합니다. 그러나이 방법을 사용 하면 관리자가 아닌 사용자가 배포를 수행할 수 있도록 IIS를 구성할 수 있습니다. 웹 배포 처리기가 IIS 7 이상 버전에서에서 사용할 수만 있습니다.
> - 사용 하 여 *오프 라인 배포*합니다. 이 방법은 웹 서버의 최소 구성 하는데 수동으로 서버에 웹 패키지를 복사 하 고 IIS 관리자를 통해 가져올 해야 서버 관리자입니다.
> 
> 주요 기능, 이점 및 이러한 방법의 단점에 대 한 자세한 내용은 참조 하십시오. [웹 배포에 대 한 오른쪽 접근 방식을 선택](choosing-the-right-approach-to-web-deployment.md)합니다.


## <a name="is-the-web-deploy-remote-agent-the-right-approach-for-you"></a>사용자에 대 한 적합 한 접근 방식을 원격 에이전트를 배포 하는 웹 인가요?

예, 콘텐츠를 배포 하는 사용자는 대상 서버에서 관리자의 자격 증명을 제공할 수 있는 경우. 이 방법은 이러한 유형의 시나리오에서는 유용 합니다.

- 개발 또는 테스트 환경, 여기서 개발자가 대상 웹 서버와 데이터베이스 서버에 대 한 모든 권한을입니다.
- 소규모 조직 사용자 한 명 또는 소규모 사용자 그룹이 전체 응용 프로그램 수명 주기에 대 한 제어 합니다.

대규모 조직 및 스테이징 또는 프로덕션 환경에 대 한 특히 많은에서 떨어질 때가 많습니다 비현실적 웹 서버에서 사용자가 관리자 권한을 부여 합니다. 호스트 된 웹 서버의 경우 이것이 특히 가능성이 아닙니다. 또한 빌드 서버에서 배포를 자동화할 계획인 경우 있습니다 하지 않을 배포 프로세스에 대 한 관리자 자격 증명을 사용 합니다. 이러한 시나리오에서 사용 하 여 배포를 지원 하도록 웹 서버 구성에서 [웹 배포 처리기](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md) 보다 만족 스러운 선택 항목을 제공할 수 있습니다.

## <a name="task-overview"></a>작업 개요

이 항목에서는 인터넷 정보 서비스 (IIS) 7.5 웹 서버를 사용 하 여 허용 및 웹 배포 원격 에이전트 방식을 사용 하 여 원격 컴퓨터에서 웹 패키지 배포를 구성 하는 방법을 설명 합니다. 에 필요 합니다.

- IIS 7.5 및 IIS 7 권장 구성에 설치 합니다.
- 2.1 이상에 웹 배포를 설치 합니다.
- 배포 된 콘텐츠를 호스팅하는 IIS 웹 사이트를 만듭니다.
- 웹 배포 에이전트 서비스가 실행 되 고 있는지 확인 합니다.

샘플 솔루션을 구체적으로 호스트 하려면 또한 해야 합니다.

- .NET Framework 4.0을 설치 합니다.
- ASP.NET MVC 3을 설치 합니다.

이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여줍니다. 작업은이 항목의 연습에서는 Windows Server 2008 r 2를 실행 하는 새로운 서버 빌드도 시작 하는 가정 합니다. 계속 하기 전에 다음 사항을 확인.

- Windows Server 2008 R2 서비스 팩 1 및 가능한 모든 업데이트가 설치 됩니다.
- 서버가 도메인에 가입 합니다.
- 서버에 고정 IP 주소입니다.

> [!NOTE]
> 참조 컴퓨터는 도메인에 가입에 대 한 자세한 내용은 [도메인 및 로그온에 컴퓨터 가입](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)합니다. 고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [고정 IP 주소 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)합니다. 원격 에이전트 서비스가 IIS 6에서부터 지원 않으며 하지 않아도 도메인에 가입 될 수 있습니다. 그러나이 자습서의 단계 개발 되 고 IIS 7.5에서 테스트를 다른 버전에 대 한 절차에 따라 달라질 수 있습니다.


## <a name="install-products-and-components"></a>제품 및 구성 요소 설치

이 섹션에서는 웹 서버에서 필요한 제품 및 구성 요소를 설치 하는 과정을 안내 합니다. 시작 하기 전에 서버에 최신 인지 확인 하려면 Windows Update를 실행 하는 것이 좋습니다.

이 경우 이러한 것 들을 설치 해야 할 수도 있습니다.

- **IIS 7 권장 구성**합니다. 이 통해는 **웹 서버 (IIS)** 웹 서버에서 역할 및 IIS 모듈 및 ASP.NET 응용 프로그램을 호스트 하는 데 필요한 구성 요소 집합을 설치 합니다.
- **.NET Framework 4.0**. 이 버전의.NET Framework에 작성 된 응용 프로그램을 실행 해야 합니다.
- **웹 배포 도구 2.1 이상**합니다. 서버에 웹 배포 (및 해당 기본 실행 파일, MSDeploy.exe)를 설치합니다. 이 과정의 일환으로, 설치 및 웹 배포 에이전트 서비스를 시작 합니다. 이 서비스는 원격 컴퓨터에서 웹 패키지를 배포할 수 있습니다.
- **ASP.NET MVC 3**합니다. MVC 3 응용 프로그램을 실행 해야 하는 어셈블리를 설치 합니다.

> [!NOTE]
> 이 연습에서는 설치 및 필수 구성 요소를 구성 하는 웹 플랫폼 설치 관리자의 사용을 설명 합니다. 웹 플랫폼 설치 관리자를 사용할 필요가 없습니다, 있지만 자동으로 종속성을 검색 하 고 최신 제품 버전을 항상 얻을 수 있도록 설치 프로세스를 간소화 합니다. 자세한 내용은 참조 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/?linkid=9805118)합니다.


**필요한 제품 및 구성 요소를 설치 하려면**

1. 다운로드 및 설치는 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)합니다.
2. 설치가 완료 되 면 웹 플랫폼 설치 관리자는 자동으로 시작 됩니다.

    > [!NOTE]
    > 웹 플랫폼 설치 관리자에서 언제 든 지 시작할 수 있습니다는 **시작** 메뉴. 이 작업을 수행 하는 **시작** 메뉴를 클릭 **모든 프로그램**, 클릭 하 고 **Microsoft 웹 플랫폼 설치 관리자**합니다.
3. 맨 위에 있는 **웹 플랫폼 설치 관리자 3.0** 창 클릭 **제품**합니다.
4. 왼쪽 탐색 창에서 창에서 클릭 **프레임 워크**합니다.
5. 에 **Microsoft.NET Framework 4** 행을.NET Framework가 이미 설치 되어 있지 않으면 클릭 **추가**합니다.

    > [!NOTE]
    > 이미 설치한 Windows Update를 통해.NET Framework 4.0입니다. 제품 또는 구성 요소가 이미 설치 되어 웹 플랫폼 설치 관리자는이 표시할 대체 하 여는 **추가** 단추 텍스트와 함께 **설치 됨**합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image1.png)
6. 에 **ASP.NET MVC 3 (Visual Studio 2010)** 행에서 클릭 **추가**합니다.
7. 탐색 창에서 클릭 **서버**합니다.
8. 에 **IIS 7 권장 구성** 행에서 클릭 **추가**합니다.
9. 에 **웹 배포 도구 2.1** 행에서 클릭 **추가**합니다.
10. **설치**를 클릭합니다. 웹 플랫폼 설치 관리자는 제품의 목록을 표시&#x2014;하 나와 함께 연결 된 종속성&#x2014;를 설치 및 사용 조건에 동의 하 라는 메시지가 나타납니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image2.png)
11. 라이선스 조건을 검토 하 고 사용자가 약관에 동의 하는 경우 클릭 **동의**합니다.
12. 설치가 완료 되 면 클릭 **마침**, 한 다음 닫습니다는 **웹 플랫폼 설치 관리자 3.0** 창.

IIS를 설치 하기 전에.NET Framework 4.0을 설치한 경우 실행 해야 합니다는 [ASP.NET IIS 등록 도구](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe)를 IIS와 함께 최신 버전의 ASP.NET 등록 합니다. 이렇게 하지 않으면, 아무 문제 없이 IIS 정적 콘텐츠 (예: HTML 파일)에서 처리를 찾을 수 있지만 반환 됩니다 **찾을 수 없음 – HTTP 오류 404.0** ASP.NET 콘텐츠를 검색 하려고 하면 합니다. ASP.NET 4.0이 등록 되었는지 확인 하려면이 절차를 사용할 수 있습니다.

**IIS와 ASP.NET 4.0을 등록 하려면**

1. 클릭 **시작**, 한 다음 입력 **명령 프롬프트**합니다.
2. 검색 결과에서 마우스 오른쪽 단추로 클릭 **명령 프롬프트**, 클릭 하 고 **관리자 권한으로 실행**합니다.
3. 명령 프롬프트 창에서 디렉터리로 이동 된 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** 디렉터리입니다.
4. 이 명령을 입력 한 다음 Enter 키를 누릅니다.

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample1.cmd)]
5. 언제 든 지 64 비트 웹 응용 프로그램을 호스트 하려는 경우 IIS와 함께 64 비트 버전의 ASP.NET도 등록 해야 합니다. 명령 프롬프트 창에서이 작업을 수행 하려면 탐색 하 고 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 디렉터리입니다.
6. 이 명령을 입력 한 다음 Enter 키를 누릅니다.

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample2.cmd)]

것이 좋습니다도 다시 사용 하 여 Windows Update이 시점에서 다운로드 하 고 새로운 제품 및 이전에 설치한 구성 요소에 대 한 사용 가능한 업데이트를 설치 합니다.

## <a name="configure-the-iis-website"></a>IIS 웹 사이트 구성

웹 콘텐츠 서버를 배포 하기 전에 만들고 콘텐츠를 호스팅하는 IIS 웹 사이트를 구성 해야 합니다. 웹 배포가 웹 패키지에서 기존 IIS 웹 사이트;에 배포할 수 있습니다. 웹 사이트를 만들 것 있습니다 수 없습니다. 상위 수준에서 이러한 작업을 완료 해야 합니다.

- 콘텐츠를 호스트 하는 파일 시스템에 폴더를 만듭니다.
- 콘텐츠를 제공 하도록 IIS 웹 사이트를 만들고 로컬 폴더에 연결 합니다.
- 로컬 폴더에 응용 프로그램 풀 id에 대 한 읽기 권한을 부여 합니다.

를 없지만 아무 IIS에서 기본 웹 사이트에 콘텐츠 배포에서 테스트 또는 데모 시나리오 외에이 방법은 권장 되지 않습니다. 프로덕션 환경을 시뮬레이트하기 위해 새 IIS 웹 사이트 응용 프로그램의 요구 사항과 관련 된 설정을 사용 하 여 만들어야 합니다.

**만들고 IIS 웹 사이트를 구성 하려면**

1. 로컬 파일 시스템에서 콘텐츠를 저장할 폴더를 만듭니다 (예를 들어 **C:\DemoSite**).
2. 에 **시작** 메뉴에서 **관리 도구**, 클릭 하 고 **인터넷 정보 서비스 (IIS) 관리자**합니다.
3. IIS 관리자에서에서 **연결** 창에서 서버 노드를 확장 (예를 들어 **TESTWEB1**).

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image3.png)
4. 마우스 오른쪽 단추로 클릭는 **사이트** 노드를 차례로 클릭 한 다음 **웹 사이트 추가**합니다.
5. 에 **사이트 이름** 상자에 IIS 웹 사이트에 대 한 이름을 입력 합니다 (예를 들어 **DemoSite**).
6. 에 **실제 경로** 상자, (찾거나 입력)의 경로를 로컬 폴더 (예를 들어 **C:\DemoSite**).
7. 에 **포트** 상자에 웹 사이트를 호스트 하려는 포트 번호를 입력 합니다 (예를 들어 **85**).

    > [!NOTE]
    > 표준 포트 번호는 80 HTTP 및 HTTPS의 경우 443입니다. 그러나 포트 80에서이 웹 사이트를 호스트 하는 경우에 사이트에 액세스 하려면 먼저 기본 웹 사이트를 중지 해야 합니다.
8. 둡니다는 **호스트 이름** 상자를 비워는 웹 사이트에 대 한 도메인 이름 (DNS System) 레코드를 구성 하 고 클릭 하려는 경우가 아니면 **확인**합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image4.png)

    > [!NOTE]
    > 프로덕션 환경에서 가능성이 싶어하는 포트 80에서 웹 사이트를 호스트 하 고 일치 하는 DNS 레코드와 함께 호스트 헤더를 구성 합니다. IIS 7에서 호스트 헤더를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [웹 사이트 (IIS 7)에 대 한 호스트 헤더 구성](https://technet.microsoft.com/library/cc753195(WS.10).aspx)합니다. Windows Server 2008 r 2에서 DNS 서버 역할에 대 한 자세한 내용은 참조 하십시오. [DNS 서버 개요](https://technet.microsoft.com/en-gb/library/cc770392.aspx) 및 [DNS 서버](https://technet.microsoft.com/windowsserver/dd448607)합니다.
9. **작업** 창의 **사이트 편집**에서 **바인딩**을 클릭합니다.
10. 에 **사이트 바인딩** 대화 상자를 클릭 **추가**합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image5.png)
11. 에 **사이트 바인딩 추가** 대화 상자, 설정 된 **IP 주소** 및 **포트** 기존 사이트 구성과 일치 하도록 합니다.
12. 에 **호스트 이름** 웹 서버의 이름을 입력 합니다 (예를 들어 **TESTWEB1**)를 클릭 하 고 **확인**합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image6.png)

    > [!NOTE]
    > 첫 번째 사이트 바인딩을 사용 하면 IP 주소와 포트를 사용 하 여 로컬로 사이트에 액세스할 수 있습니다 또는 `http://localhost:85`합니다. 두 번째 사이트 바인딩을 사용 하면 컴퓨터 이름을 사용 하 여 도메인의 다른 컴퓨터에서 사이트에 액세스할 수 있습니다 (예를 들어 http://testweb1:85)합니다.
13. 에 **사이트 바인딩** 대화 상자를 클릭 **닫기**합니다.
14. 에 **연결** 창에서 클릭 **응용 프로그램 풀**합니다.
15. 에 **응용 프로그램 풀** 창, 응용 프로그램 풀의 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **기본 설정**합니다. 기본적으로 응용 프로그램 풀의 이름에는 웹 사이트의 이름과 일치 합니다 (예를 들어 **DemoSite**).
16. 에 **.NET Framework 버전** 목록에서 **.NET Framework v4.0.30319**, 클릭 하 고 **확인**합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image7.png)

    > [!NOTE]
    > 샘플 솔루션에는.NET Framework 4.0 필요합니다. 이것이 웹 배포에 대 한 요구 사항은 일반적입니다.

콘텐츠를 제공 하도록 웹 사이트를 응용 프로그램 풀 id는 콘텐츠를 저장 하는 로컬 폴더에 대 한 권한이 읽기 있어야 합니다. IIS 7.5에서 응용 프로그램 풀은 일반적으로 실행 위치는 네트워크 서비스 계정을 사용 하 여 IIS의 이전 버전) (달리 기본적으로 응용 프로그램 풀 고유한 응용 프로그램 풀 id로 실행 합니다. 응용 프로그램 풀 id 실제 사용자 계정이 고 사용자 또는 그룹의 모든 목록에 표시 되지 않는&#x2014;대신 만들어졌을 동적으로 응용 프로그램 풀을 시작할 때입니다. 각 응용 프로그램 풀 id는 로컬에 추가 됩니다 **IIS\_IUSRS** 숨겨진된 항목으로 보안 그룹입니다.

를 파일이 나 폴더에 응용 프로그램 풀 id에 대 한 권한을 부여 하는 두 가지 옵션이 있습니다.

- 에 사용 권한을 할당 응용 프로그램 풀 id를 직접 형식을 사용 하 여 <strong>IIS AppPool\<강력한 / ><em>[응용 프로그램 풀 이름]</em>(예를 들어 <strong>IIS AppPool\DemoSite</strong>).
- 권한 할당의 **IIS\_IUSRS** 그룹입니다.

가장 일반적인 방법은 로컬에 권한을 할당 하려면 **IIS\_IUSRS** 이 방법은 파일 시스템 사용 권한 다시 구성 하지 않고 응용 프로그램 풀을 변경 하면 있기 때문에 그룹화 합니다. 다음 절차에는이 그룹 기반 접근 방식을 사용 합니다.

> [!NOTE]
> IIS 7.5에서 응용 프로그램 풀 id에 대 한 자세한 내용은 참조 하십시오. [응용 프로그램 풀 Id](https://go.microsoft.com/?linkid=9805123)합니다.


**IIS 웹 사이트에 대 한 폴더 사용 권한을 구성 하려면**

1. Windows 탐색기에서 로컬 폴더의 위치를 찾습니다.
2. 폴더를 마우스 오른쪽 단추로 누른 **속성**합니다.
3. 에 **보안** 탭을 클릭 **편집**, 클릭 하 고 **추가**합니다.
4. 클릭 **위치**합니다. 에 **위치** 대화 상자에서 로컬 서버를 선택 하 고 클릭 **확인**합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image8.png)
5. 에 **사용자 또는 그룹 선택** 대화 상자에서 **IIS\_IUSRS**, 클릭 **이름 확인**, 클릭 하 고 **확인**합니다.
6. 에 <strong>에 대 한 권한을</strong><em>[폴더 이름]</em>대화 상자, 새 그룹에 할당 된 통지는 <strong>읽기 &amp; 실행</strong>, <strong>폴더 목록 내용을</strong>, 및 <strong>읽기</strong> 권한은 기본적으로 합니다. 이 변경 되지 않은 상태로 두고 클릭 <strong>확인</strong>합니다.
7. 클릭 <strong>확인</strong> 를 닫으려면는 <em>[폴더 이름]</em><strong>속성</strong> 대화 상자.

마지막 작업으로 서버에 모든 웹 패키지를 배포 하기 전에 확인 해야 웹 배포 에이전트 서비스가 실행 되 고 있는지 합니다. 원격 컴퓨터에서 패키지를 배포 하는 경우에 웹 배포 에이전트 서비스는 추출 및 패키지의 콘텐츠를 설치 하는 일을 담당 합니다. 서비스는 웹 배포 도구를 설치할 때 기본적으로 시작 되 고 Network Service id로 실행 합니다.

확인할 수 있습니다는 서비스가 여러 다른 방법으로 실행 되 고 있는지 여부를 다양 한 명령줄 유틸리티 또는 Windows PowerShell cmdlet을 사용 합니다. 이 절차에서는 간단한 UI 기반 접근 방식을 설명 합니다.

**웹 배포 에이전트 서비스가 실행 되 고 있는지 확인 하려면**

1. **시작** 메뉴에서 **관리 도구**를 가리킨 다음 **서비스**를 클릭합니다.
2. 찾을 **웹 배포 에이전트 서비스가** 되어 있는지 확인 하 고 행을 **상태** 로 설정 된 **시작 됨**합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image9.png)
3. 서비스가 아직 시작 되지 않은 경우 클릭 **시작**합니다.

## <a name="configure-firewall-exceptions"></a>방화벽 예외 구성

기본적으로 원격 에이전트 서비스는이 URL에서 TCP 포트 80에서 수신:

<http://servername.com/MSDEPLOYAGENTSERVICE>

대부분의 경우에서 웹 서버는 일반적으로 포트 80에서 HTTP 요청에 대 한 수신 대기 하기 때문에 원격 에이전트 서비스에 대 한 모든 추가 방화벽 규칙을 구성할 필요가 없습니다. 비표준 포트에서 수신 하도록 설치를 사용자 지정한 경우에 필요에 따라 방화벽 예외를 구성 해야 합니다.

## <a name="conclusion"></a>결론

이 시점에서 웹 서버에 동의 하 고 원격 컴퓨터에서 웹 패키지를 설치 하는 일을 준비가 되었습니다. 서버에 웹 응용 프로그램을 배포 하려고 하기 전에 이러한 주요 사항을 확인 하는 것이 좋습니다.

- IIS와 ASP.NET 4.0을 등록 한?
- 응용 프로그램 풀 id가 읽기 권한을 웹 사이트에 대 한 원본 폴더에 있습니까?
- 웹 배포 에이전트 서비스가 실행 중 입니까?

## <a name="further-reading"></a>추가 정보

웹 패키지에서 원격 에이전트 서비스를 배포 하려면 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 구성 하는 방법에 대 한 지침을 참조 하십시오. [대상 환경에 대 한 배포 속성 구성](configuring-deployment-properties-for-a-target-environment.md)합니다.

> [!div class="step-by-step"]
> [이전](scenario-configuring-a-production-environment-for-web-deployment.md)
> [다음](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
