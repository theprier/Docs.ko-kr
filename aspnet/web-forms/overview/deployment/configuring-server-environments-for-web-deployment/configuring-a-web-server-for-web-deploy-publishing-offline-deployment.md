---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
title: 게시 (오프 라인 배포) 배포 웹에 대 한 웹 서버 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 오프 라인 웹 게시 및 배포를 지원 하기 위해 IIS 웹 서버를 구성 하는 방법을 설명 합니다. 인터넷 정보 서비스를 사용 하 여 작업할 때 (I....
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: ba92788f-9f03-44b1-b6b2-af8413e6a35d
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
msc.type: authoredcontent
ms.openlocfilehash: 555b4b3c79d8efc641b1c179482993371735dbe2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37397579"
---
<a name="configuring-a-web-server-for-web-deploy-publishing-offline-deployment"></a>웹 배포 게시용 (오프 라인 배포) 웹 서버 구성
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 오프 라인 웹 게시 및 배포를 지원 하기 위해 IIS 웹 서버를 구성 하는 방법을 설명 합니다.
> 
> 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 2.0 이상을 사용 하 여 작업할 때 세 가지 기본 방법을 응용 프로그램 또는 웹 서버에 사이트를 가져오는 데 사용할 수 있습니다. 다음과 같은 작업을 수행할 수 있습니다.
> 
> - 사용 된 *원격 에이전트 서비스를 배포 하는 웹*합니다. 이 접근 방식에서는 웹 서버의 구성이 줄어들기 하지만 아무 것도 서버에 배포 하기 위해 로컬 서버 관리자의 자격 증명을 제공 해야 합니다.
> - 사용 된 *웹 배포 처리기*합니다. 이 방법은 훨씬 더 복잡 한 이며 웹 서버를 설정 하려면 초기 더 많은 노력이 필요 합니다. 그러나이 방법을 사용 하는 경우에 관리자가 아닌 사용자가 배포를 수행할 수 있도록 IIS를 구성할 수 있습니다. 웹 배포 처리기만 IIS 7 이상 버전에서에서 제공 됩니다.
> - 사용 하 여 *오프 라인 배포*합니다. 이 방법은 웹 서버에 최소 구성이 필요 하지만 서버 관리자가 수동으로 서버로 웹 패키지를 복사 하 고 IIS 관리자를 통해 가져옵니다.
> 
> 주요 기능, 이점 및 이러한 접근 방식의 단점에 대 한 자세한 내용은 참조 하세요. [웹 배포에 오른쪽 접근 방식을 선택](choosing-the-right-approach-to-web-deployment.md)합니다.


예, 네트워크 인프라 또는 보안 제한 사항에 원격 배포가 진행 되지 않습니다. 이 웹 서버가 격리 되 인터넷 프로덕션 환경의 경우 일 가능성이 가장 큰&#x2014;하거나 물리적으로 또는 하 여 방화벽 및 서브넷&#x2014;서버 인프라의 나머지 부분에서.

물론이 방법은 그다지 웹 응용 프로그램을 정기적으로 업데이트 됩니다. 인프라에서 허용 하는 경우 하려는 원격 배포를 사용 하도록 설정 하는 것이 좋습니다. 웹 배포 처리기 또는 웹 배포 원격 에이전트 서비스를 사용 하 여 합니다.

## <a name="task-overview"></a>작업 개요

오프 라인 가져오기 및 웹 패키지 배포를 지원 하도록 웹 서버를 구성 하려면를 해야 합니다.

- IIS 7.5 및 IIS 7 권장 구성에 설치 합니다.
- 웹 배포 2.1 이상을 설치 합니다.
- 배포 된 콘텐츠를 호스팅하는 IIS 웹 사이트를 만듭니다.
- 웹 배포 에이전트 서비스를 사용 하지 않도록 설정 합니다.

샘플 솔루션, 특히 호스트도 해야 합니다.

- .NET Framework 4.0을 설치 합니다.
- ASP.NET MVC 3을 설치 합니다.

이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여줍니다. 작업은이 항목의 연습에서는 Windows Server 2008 R2를 실행 하는 새로운 서버 빌드를 사용 하 여 시작 하 고 있음을 가정 합니다. 계속 하기 전에 확인 합니다.

- Windows Server 2008 R2 서비스 팩 1 및 모든 사용 가능한 업데이트가 설치 됩니다.
- 서버가는 도메인에 가입 된입니다.
- 서버에 고정 IP가 있습니다.

> [!NOTE]
> 참조 컴퓨터를 도메인에 가입 하는 방법은 [도메인 및 로그온에 컴퓨터 가입](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)합니다. 고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [정적 IP 주소를 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)합니다.


## <a name="install-products-and-components"></a>제품 및 구성 요소를 설치 합니다.

이 섹션에서는 웹 서버에서 필요한 제품 및 구성 요소를 설치 하는 과정 안내 합니다. 시작 하기 전에 서버에 최신 인지 확인 하려면 Windows Update를 실행 하는 것이 좋습니다.

이 경우 이러한 작업을 설치 해야 합니다.

- **IIS 7 권장 구성**합니다. 이 통해는 **웹 서버 (IIS)** 웹 서버의 역할 IIS 모듈 및 ASP.NET 응용 프로그램을 호스트 하기 위해 필요한 구성 요소 집합을 설치 합니다.
- **.NET Framework 4.0**. 이 버전의.NET Framework에서 빌드된 응용 프로그램을 실행 해야 합니다.
- **웹 배포 도구 2.1 이상**합니다. 서버에 웹 배포 (및 해당 기본 실행 파일, MSDeploy.exe)를 설치합니다. 웹 배포는 IIS를 통합 하 고 웹 패키지 가져오기 및 내보내기 수 있습니다.
- **ASP.NET MVC 3**합니다. MVC 3 응용 프로그램을 실행 해야 하는 어셈블리를 설치 합니다.

> [!NOTE]
> 이 연습에서는 웹 플랫폼 설치 관리자를 설치 하 여 다양 한 구성 요소 사용을 설명 합니다. 웹 플랫폼 설치 관리자를 사용 하 여 필요가 있지만 자동으로 종속성을 검색 하 고 제품을 최신 버전 항상 얻을 수를 확인 하 여 설치 프로세스를 간소화 합니다. 자세한 내용은 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/?linkid=9805118)합니다.


**필요한 제품 및 구성 요소를 설치 하려면**

1. 다운로드 및 설치 합니다 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)합니다.
2. 설치가 완료 되 면 웹 플랫폼 설치 관리자를 자동으로 시작 됩니다.

    > [!NOTE]
    > 웹 플랫폼 설치 관리자에서 언제 든 지 시작할 수 있습니다 합니다 **시작** 메뉴. 이 작업을 수행 하는 **시작** 메뉴에서 클릭 **모든 프로그램**를 클릭 하 고 **Microsoft Web Platform Installer**합니다.
3. 맨 위에 있는 합니다 **웹 플랫폼 설치 관리자 3.0** 창에서 클릭 **제품**합니다.
4. 왼쪽 탐색 창에서 창에서 클릭 **프레임 워크**합니다.
5. 에 **Microsoft.NET Framework 4** 행을.NET Framework가 이미 설치 되어 있지 않으면 클릭 **추가**합니다.

    > [!NOTE]
    > 이미 설치한 Windows Update를 통해.NET Framework 4.0입니다. 제품 또는 구성 요소를 이미 설치 되어 웹 플랫폼 설치 관리자는이 표시할 대체 하 여 합니다 **추가** 텍스트가 있는 단추 **설치 된**합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image1.png)
6. 에 **ASP.NET MVC 3 (Visual Studio 2010)** 행을 클릭 **추가**합니다.
7. 탐색 창에서 클릭 **Server**합니다.
8. 에 **IIS 7 권장 구성** 행을 클릭 **추가**합니다.
9. 에 **웹 배포 도구 2.1** 행을 클릭 **추가**합니다.
10. **설치**를 클릭합니다. 웹 플랫폼 설치 관리자 제품의 목록이 표시 됩니다&#x2014;연결 된 종속성을와 함께&#x2014;를 설치 및 사용 조건에 동의 하 라는 메시지가 표시 됩니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image2.png)
11. 사용 조건을 검토 하 고 사용자가 약관에 동의 하면 클릭 **동의**합니다.
12. 설치가 완료 되 면 클릭 **완료**를 닫은 다음 합니다 **웹 플랫폼 설치 관리자 3.0** 창입니다.

실행 해야 IIS를 설치 하기 전에.NET Framework 4.0을 설치한 경우 합니다 [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) IIS를 사용 하 여 최신 버전의 ASP.NET 등록 합니다. 이렇게 하지 않으면, 문제 없이 IIS 정적 콘텐츠 (예: HTML 파일)에서 처리를 찾을 수 있지만 반환 **찾을 수 없음 HTTP 오류 404.0 –** ASP.NET 콘텐츠를 검색 하려고 할 때입니다. ASP.NET 4.0이 등록 되었는지 확인 하려면 다음 절차를 사용할 수 있습니다.

**IIS를 사용 하 여 ASP.NET 4.0을 등록 하려면**

1. 클릭 **시작**를 차례로 **명령 프롬프트**합니다.
2. 검색 결과에서 마우스 오른쪽 단추로 클릭 **명령 프롬프트**를 클릭 하 고 **관리자 권한으로 실행**합니다.
3. 명령 프롬프트 창에서로 이동 합니다 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** 디렉터리입니다.
4. 이 명령을 입력 한 다음 Enter를 누릅니다.

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample1.cmd)]
5. 언제 든 지 64 비트 웹 응용 프로그램을 호스트 하려는 경우 IIS를 사용 하 여 64 비트 버전의 ASP.NET도 등록 해야 합니다. 이렇게 하려면 명령 프롬프트 창에서로 이동 합니다 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 디렉터리입니다.
6. 이 명령을 입력 한 다음 Enter를 누릅니다.

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample2.cmd)]

좋은 방법은, Windows 업데이트 다시 사용이 시점에서 다운로드 하 고 새 제품 및 설치한 구성 요소에 대 한 사용 가능한 업데이트를 설치 합니다.

## <a name="configure-the-iis-website"></a>IIS 웹 사이트를 구성 합니다.

웹 콘텐츠 서버를 배포 하기 전에 만들고 콘텐츠를 호스팅하는 IIS 웹 사이트를 구성 해야 합니다. 웹 배포는 기존 IIS 웹 사이트에 웹 패키지를 배포만 웹 사이트를 만들 수 없습니다. 높은 수준에서 이러한 작업을 완료 해야 합니다.

- 따라서 콘텐츠 호스트 파일 시스템에 폴더를 만듭니다.
- 콘텐츠를 제공 하는 IIS 웹 사이트를 만들고 로컬 폴더를 사용 하 여 연결 합니다.
- 로컬 폴더에 응용 프로그램 풀 id에 대 한 읽기 권한 부여 합니다.

없지만 해도 전혀 IIS에서 기본 웹 사이트에 콘텐츠를 배포, 테스트 또는 데모 시나리오 외에이 방법은 권장 되지 않습니다. 프로덕션 환경을 시뮬레이트하기 위해 응용 프로그램의 요구 사항과 관련 된 설정을 사용 하 여 새 IIS 웹 사이트를 만들어야 합니다.

**만들기 및 IIS 웹 사이트를 구성 합니다.**

1. 로컬 파일 시스템에 콘텐츠를 저장할 폴더를 만듭니다 (예를 들어 **C:\DemoSite**).
2. 에 **시작** 메뉴에서 **관리 도구**를 클릭 하 고 **인터넷 정보 서비스 (IIS) 관리자**합니다.
3. IIS 관리자에서에서 **연결** 창에서 서버 노드를 확장 (예를 들어 **PROWEB1**).

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image3.png)
4. 마우스 오른쪽 단추로 클릭 합니다 **사이트** 노드를 차례로 클릭 한 다음 **웹 사이트 추가**합니다.
5. 에 **사이트 이름** 상자에 IIS 웹 사이트에 대 한 이름을 입력 (예를 들어 **DemoSite**).
6. 에 **실제 경로** 상자, 형식 (또는 이동) 로컬 폴더에 경로 (예를 들어 **C:\DemoSite**).
7. 에 **포트** 상자는 웹 사이트를 호스트 하려면 포트 번호를 입력 합니다 (예를 들어 **85**).

    > [!NOTE]
    > 표준 포트 번호로 HTTP 80 및 443 https 됩니다. 그러나 포트 80에서이 웹 사이트를 호스트 하는 경우에 사이트에 액세스 하려면 먼저 기본 웹 사이트를 중지 해야 합니다.
8. 유지 된 **호스트 이름** 빈 웹 사이트에 대 한 도메인 이름 시스템 (DNS) 레코드를 구성 하 고 클릭 하려는 경우가 아니면 상자 **확인**합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image4.png)

    > [!NOTE]
    > 프로덕션 환경에서는 포트 80에서 웹 사이트를 호스트 하 고 일치 하는 DNS 레코드와 함께 호스트 헤더를 구성 하 해야 가능성이 높습니다. IIS 7에서 호스트 헤더를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [웹 사이트 (IIS 7)에 대 한 호스트 헤더 구성](https://technet.microsoft.com/library/cc753195(WS.10).aspx)합니다. Windows Server 2008 R2에서 DNS 서버 역할에 대 한 자세한 내용은 참조 하세요. [DNS 서버 개요](https://technet.microsoft.com/en-gb/library/cc770392.aspx) 하 고 [DNS 서버](https://technet.microsoft.com/windowsserver/dd448607)합니다.
9. **작업** 창의 **사이트 편집**에서 **바인딩**을 클릭합니다.
10. 에 **사이트 바인딩을** 대화 상자, 클릭 **추가**합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image5.png)
11. 에 **사이트 바인딩 추가** 대화 상자에서를 **IP 주소** 하 고 **포트** 기존 사이트 구성과 일치 하도록 합니다.
12. 에 **호스트 이름** 상자 웹 서버의 이름을 입력 합니다 (예를 들어 **PROWEB1**)를 클릭 하 고 **확인**합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image6.png)

    > [!NOTE]
    > 첫 번째 사이트 바인딩을 사용 하면 IP 주소 및 포트를 사용 하 여 로컬 사이트에 액세스할 수 있습니다 또는 `http://localhost:85`합니다. 두 번째 사이트 바인딩을 사용 하면 컴퓨터 이름을 사용 하 여 도메인의 다른 컴퓨터에서 사이트에 액세스할 수 있습니다 (예를 들어 http://proweb1:85)합니다.
13. 에 **사이트 바인딩을** 대화 상자, 클릭 **닫기**합니다.
14. 에 **연결** 창 클릭 **응용 프로그램 풀**합니다.
15. 에 **응용 프로그램 풀** 창에 응용 프로그램 풀의 이름을 마우스 오른쪽 단추로 클릭 **기본 설정**합니다. 기본적으로 응용 프로그램 풀의 이름에는 웹 사이트의 이름과 일치 합니다 (예를 들어 **DemoSite**).
16. 에 **.NET Framework 버전** 목록에서 **.NET Framework v4.0.30319**를 클릭 하 고 **확인**합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image7.png)

    > [!NOTE]
    > 샘플 솔루션에는.NET Framework 4.0에 필요합니다. 이 요구 사항은 아닙니다 웹 배포에 대 한 일반적입니다.

콘텐츠를 제공 하도록 웹 사이트에 대 한 순서 대로 응용 프로그램 풀 id를 콘텐츠를 저장 하는 로컬 폴더에 대 한 권한이 읽기 있어야 합니다. IIS 7.5에서 응용 프로그램 풀을 고유한 응용 프로그램 풀 id를 사용 하 여 (이전 버전의 IIS에 응용 프로그램 풀은 일반적으로 실행할 네트워크 서비스 계정 사용)는 달리 기본적으로 실행 합니다. 응용 프로그램 풀 id는 실제 사용자 계정이 아니며 사용자 또는 그룹의 모든 목록에 표시 되지 않습니다&#x2014;대신 만들어집니다 동적으로 응용 프로그램 풀 시작 될 때입니다. 각 응용 프로그램 풀 id는 로컬에 추가할 **IIS\_IUSRS** 숨겨진된 항목으로 보안 그룹입니다.

파일 또는 폴더에 응용 프로그램 풀 id에 대 한 사용 권한을 부여 하는 두 가지 옵션이 있습니다.

- 사용 권한을 할당 하 고 응용 프로그램 풀 id를 직접 형식을 사용 하 여 <strong>IIS AppPool\</s o n ><em>[응용 프로그램 풀 이름]</em>(예를 들어 <strong>IIS AppPool\DemoSite</strong>).
- 사용 권한을 할당 합니다 **IIS\_IUSRS** 그룹입니다.

로컬에 사용 권한을 할당 하는 가장 일반적인 방법입니다 **IIS\_IUSRS** 그룹에 있으므로이 방법을 사용 하면 파일 시스템 사용 권한 다시 구성 하지 않고 응용 프로그램 풀을 변경할 수 있습니다. 다음 절차에는이 그룹 기반 접근 방식을 사용 합니다.

> [!NOTE]
> IIS 7.5에서 응용 프로그램 풀 id에 대 한 자세한 내용은 참조 하세요. [응용 프로그램 풀 Id](https://go.microsoft.com/?linkid=9805123)합니다.


**IIS 웹 사이트에 대 한 폴더 사용 권한을 구성 하려면**

1. Windows 탐색기에서 로컬 폴더의 위치로 이동 합니다.
2. 폴더를 마우스 오른쪽 단추로 누른 **속성**합니다.
3. 에 **보안** 탭을 클릭 **편집**를 클릭 하 고 **추가**합니다.
4. 클릭 **위치**합니다. 에 **위치** 대화 상자에서 로컬 서버를 선택 하 고 클릭 **확인**합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image8.png)
5. 에 **사용자 또는 그룹 선택** 대화 상자에서 **IIS\_IUSRS**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.
6. 에 <strong>에 대 한 권한을</strong><em>[폴더 이름]</em> 대화 상자, 새 그룹에 할당 된 합니다 <strong>읽기 &amp; 실행</strong>, <strong>폴더 나열 내용을</strong>, 및 <strong>읽기</strong> 기본적으로 사용 권한. 이 변경 되지 않은 상태로 두고 클릭 <strong>확인</strong>합니다.
7. 클릭 <strong>확인</strong> 닫으려면 합니다 <em>[폴더 이름]</em><strong>속성</strong> 대화 상자.

## <a name="disable-the-remote-agent-service"></a>원격 에이전트 서비스를 사용 하지 않도록 설정

웹 배포를 설치할 때 웹 배포 에이전트 서비스가 설치 되어 자동으로 시작 됩니다. 이 서비스를 사용 하면 배포 하 고 원격 위치에서 웹 패키지를 게시할 수 있습니다. 중지 하 고 서비스를 사용 하지 않도록 설정 해야 하므로이 시나리오에서는 원격 배포 기능을 사용 하지 않습니다.

> [!NOTE]
> 가져오기 및 웹 패키지를 수동으로 배포 하려면 원격 에이전트 서비스를 중지 하지 않아도 됩니다. 그러나 것을 중지 하 고 사용 하지 않으려는 경우 서비스를 사용 하지 않도록 설정 하는 것이 좋습니다.


중지 하 고 다양 한 명령줄 유틸리티 또는 Windows PowerShell cmdlet을 사용 하 여 여러 가지 방법으로 서비스를 비활성화 합니다. 이 절차는 간단 하 게 UI 기반 접근 방식을 설명합니다.

**중지 하 고 원격 에이전트 서비스를 사용 하지 않도록 설정**

1. **시작** 메뉴에서 **관리 도구**를 가리킨 다음 **서비스**를 클릭합니다.
2. 서비스 콘솔에서 찾습니다 합니다 **웹 배포 에이전트 서비스가** 행입니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image9.png)
3. 마우스 오른쪽 단추로 클릭 **웹 배포 에이전트 서비스가**를 클릭 하 고 **속성**합니다.
4. 에 **웹 배포 에이전트 서비스 속성** 대화 상자, 클릭 **중지**합니다.
5. 에 **시작 유형** 목록에서 **사용 안 함**를 클릭 하 고 **확인**합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image10.png)

## <a name="conclusion"></a>결론

이 시점에서 웹 서버는 오프 라인 웹 패키지 배포용으로 준비 합니다. IIS 웹 사이트 웹 패키지를 가져올 하려고 하기 전에 이러한 요점을 확인 하는 것이 좋습니다.

- IIS를 사용 하 여 ASP.NET 4.0을 등록 한?
- 응용 프로그램 풀 id를 웹 사이트의 소스 폴더에 읽기 액세스할을 수?
- 웹 배포 에이전트 서비스를 중지 하면?

> [!div class="step-by-step"]
> [이전](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
> [다음](configuring-a-database-server-for-web-deploy-publishing.md)
