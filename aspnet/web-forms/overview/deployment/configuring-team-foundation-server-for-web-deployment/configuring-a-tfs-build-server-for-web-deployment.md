---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
title: "웹 배포에 대 한 빌드 서버 TFS 구성 | Microsoft Docs"
author: jrjlee
description: "이 항목에서는 빌드하고 팀 빌드 및 인터넷 Informat를 사용 하 여 솔루션을 배포 하는 Team Foundation Server (TFS) 빌드 서버를 준비 하는 방법에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: f8400241-4f4b-4bbd-9994-54fb64909e6e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: de31a9dffb95b863a4ec38b74fd2c6e03f287a7f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="configuring-a-tfs-build-server-for-web-deployment"></a>웹 배포를 위한 TFS 빌드 서버 구성
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 빌드하고 팀 빌드 및 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 솔루션을 배포 하는 Team Foundation Server (TFS) 빌드 서버를 준비 하는 방법을 설명 합니다.


이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 이 자습서 시리즈 샘플 솔루션 & #x 2014;을 사용 하는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& #x 2014; 현실적인 수준의 복잡성을 Windows ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 제공 합니다.

이 자습서의 핵심에는 배포 방법에 설명 된 분할 프로젝트 파일 접근 방식에 따라 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 빌드 프로세스에 의해 제어 되는 두 프로젝트에 파일 & #x 2014; 포함 환경 관련 빌드 및 배포 설정을 포함 하는 하나 및 모든 대상 환경에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 구성 하기 위해 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="task-overview"></a>작업 개요

빌드 및 배포 솔루션 빌드 서버를 준비 하려면 해야 합니다.

- 설치 하 고 TFS 빌드 서비스를 구성 합니다.
- Visual Studio 2010을 설치 합니다.
- 모든 제품 또는 같은 버전의.NET Framework 또는 ASP.NET MVC 솔루션을 빌드하는 데 필요한 구성 요소를 설치 합니다.
- 웹 배포 2.0 이상을 설치 합니다.

이 항목에서는 이러한 절차를 수행 하거나 이들이 존재 하는 다른 리소스를 가리킬 방법을 보여줍니다. 작업 및이 항목의 연습 하는 가정합니다.

- Windows Server 2008 R2 서비스 팩 1을 실행 하는 새로운 서버 빌드와 시작 합니다.
- 서버가 고정 IP 주소를 갖는 도메인에 가입 합니다.
- TFS 응용 프로그램 계층에 설치한 별도 서버에 설명 된 대로 [엔터프라이즈 웹 배포: 시나리오 개요](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)합니다.

### <a name="who-performs-these-procedures"></a>이러한 절차를 수행 하는 사람?

대부분의 경우에서 TFS 관리자에 빌드 서버 구성 됩니다. 경우에 따라 개발자 팀 특정 빌드 서버의 소유권을 가질 수 있습니다.

## <a name="install-and-configure-the-tfs-build-service"></a>TFS 빌드 서비스 설치 및 구성

빌드 서버를 구성할 때 첫 번째 작업은 설치 하 고 TFS 빌드 서비스를 구성 합니다. 이 과정의 일환으로,에 필요 합니다.

- TFS 빌드 서비스를 설치 하 고 서비스 계정을 구성 합니다. 빌드 서비스 계정의 id를 사용 하 여 배포를 비롯 한 모든 빌드 작업을 실행 됩니다.
- 만들기는 *빌드 컨트롤러* 와 하나 이상의 *빌드 에이전트*합니다. 각 빌드 컨트롤러는 빌드 에이전트 집합을 관리합니다. 한 빌드를 큐 빌드 컨트롤러의 빌드 작업은 사용 가능한 빌드 에이전트에 할당 합니다. TFS에서 각 팀 프로젝트 컬렉션을 단일 빌드 컨트롤러에 매핑됩니다.
- 빌드 출력에 대 한 드롭 폴더를 구성 합니다. 네트워크 공유입니다. 모든 빌드 출력이 웹 배포 패키지와 마찬가지로, 드롭 폴더로 전송 됩니다.

[Team Foundation Build 관리](https://msdn.microsoft.com/library/ms252495.aspx) 장 MSDN에서 이러한 작업을 수행 하는 데 필요한 모든 리소스가 포함 되어 있습니다.

- 빌드 서비스, 빌드 컨트롤러 및 빌드 에이전트 참조를 포함 하 여 Team Foundation Build의 개념적인 개요를 위한 [Team Foundation 빌드 시스템을 이해](https://msdn.microsoft.com/library/dd793166.aspx)합니다.
- 빌드 서비스 설치 및 구성에 대 한 정보를 참조 하십시오. [빌드 컴퓨터를 구성](https://msdn.microsoft.com/library/ms181712.aspx)합니다.
- 빌드 컨트롤러를 만드는 방법에 대 한 정보를 참조 하십시오. [작업 만들기 및 빌드 컨트롤러 사용](https://msdn.microsoft.com/library/ee330987.aspx)합니다.
- 빌드 에이전트를 만드는 방법에 대 한 정보를 참조 하십시오. [작업 만들기 및 빌드 에이전트 사용](https://msdn.microsoft.com/library/bb399135.aspx)합니다.
- 작성 및 구성 저장 폴더에 대 한 정보를 참조 하십시오. [저장 폴더 설정](https://msdn.microsoft.com/library/bb778394.aspx)합니다.

## <a name="install-required-products-and-components"></a>필요한 제품 및 구성 요소 설치

솔루션을 빌드하려면 빌드 서버를 사용 하려면 모든 제품, 구성 요소 또는 솔루션에 필요한 어셈블리를 설치 해야 합니다. 모든 웹 플랫폼 구성 요소를 설치 하기 전에 빌드 서버에서 Visual Studio 2010 (모든 버전)를 설치 해야 합니다. 이렇게 하면 핵심 Microsoft Build Engine (MSBuild) 대상 파일 및 웹 게시 파이프라인 (WPP) 대상 파일은 빌드 서비스를 사용할 수 있습니다. Visual Studio 설치 관리자는 웹 배포 빌드 프로세스의 일부로 웹 패키지를 배포 하려는 경우 필요 합니다는 설치도 해야 합니다.

사용 하는 일반적인 웹 플랫폼 구성 요소를 설치 하는 가장 좋은 방법은 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)합니다. 이렇게 하면 각 제품의 최신 버전을 설치 하 고 자동으로 감지 하 고 각 제품에 대 한 모든 필수 구성 요소를 설치 합니다. 경우에 [않아](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 솔루션을 이러한 제품 및 구성 요소를 설치 하려면 웹 플랫폼 설치 관리자를 사용 해야 합니다.

- **.NET Framework 4.0**. 이 버전의.NET Framework에 작성 된 응용 프로그램을 실행 해야 합니다.
- **웹 배포 도구 2.1 이상**합니다. 서버에 웹 배포 (및 해당 기본 실행 파일, MSDeploy.exe)를 설치합니다. 이 과정의 일환으로, 설치 및 웹 배포 에이전트 서비스를 시작 합니다. 이 서비스는 원격 컴퓨터에서 웹 패키지를 배포할 수 있습니다.
- **ASP.NET MVC 3**합니다. ASP.NET MVC 3 응용 프로그램을 실행 해야 하는 어셈블리를 설치 합니다.

**필요한 제품 및 구성 요소를 설치 하려면**

1. Visual Studio 2010을 설치 합니다. 를 설치할 기능을 선택 하 라는 메시지가 포함 되어야 합니다.

    1. 컴파일해야 하는 모든 프로그래밍 언어입니다.
    2. Visual Web Developer 합니다. 이렇게 하면 WPP 대상 빌드 서버에 추가 됩니다.

        ![](configuring-a-tfs-build-server-for-web-deployment/_static/image1.png)
2. Visual Studio 2010 설치가 완료 되 면 다운로드 및 설치 [Visual Studio 2010 서비스 팩 1](https://go.microsoft.com/?linkid=9805133) (경우 것은 아직 포함 되지 않은 설치 미디어에).

    > [!NOTE]
    > Visual Studio 2010 서비스 팩 1 않도록 할 수 있는 MSBuild 실행 MSDeploy 찾기는 버그를 해결 합니다.
3. 다운로드 하 여 시작 된 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)합니다.
4. 맨 위에 있는 **웹 플랫폼 설치 관리자 3.0** 창 클릭 **제품**합니다.
5. 왼쪽 탐색 창에서 창에서 클릭 **프레임 워크**합니다.
6. 에 **Microsoft.NET Framework 4** 행을.NET Framework가 이미 설치 되어 있지 않으면 클릭 **추가**합니다.

    > [!NOTE]
    > 이미 설치한 Windows Update를 통해.NET Framework 4.0입니다. 제품 또는 구성 요소가 이미 설치 되어 웹 플랫폼 설치 관리자는이 표시할 대체 하 여는 **추가** 단추 텍스트와 함께 **설치 됨**합니다.

    ![](configuring-a-tfs-build-server-for-web-deployment/_static/image2.png)
7. 에 **ASP.NET MVC 3 (Visual Studio 2010)** 행에서 클릭 **추가**합니다.
8. 탐색 창에서 클릭 **서버**합니다.
9. 에 **웹 배포 도구 2.1** 행에서 클릭 **추가**합니다.
10. **설치**를 클릭합니다. 웹 플랫폼 설치 관리자를 설치할 모든 관련 된 종속성 & #x 2014; 함께; 제품 & #x 2014의 목록이 표시 됩니다 및 사용 조건에 동의 하 라는 메시지가 나타납니다.
11. 라이선스 조건을 검토 하 고 사용자가 약관에 동의 하는 경우 클릭 **동의**합니다.
12. 설치가 완료 되 면 클릭 **마침**, 한 다음 닫습니다는 **웹 플랫폼 설치 관리자 3.0** 창.

> [!NOTE]
> 배포 프로세스의 VSDBCMD.exe 또는 SQLCMD.exe와 같은 도구를 사용할 경우, 이러한 빌드 서버에 설치 되어 있는지 확인 해야 합니다. VSDBCMD.exe Visual Studio 도구 이며 일반적으로 Team Foundation Build를 설치할 때 서버에 추가 됩니다. SQLCMD.exe는 SQL Server 도구입니다. SQLCMD.exe의 독립 실행형 버전을 다운로드할 수 있습니다는 [Microsoft SQL Server 2008 R2 기능 팩](https://go.microsoft.com/?linkid=9805134) 페이지.


## <a name="conclusion"></a>결론

이 시점에서 빌드 서버에 빌드 및 웹 응용 프로그램 프로젝트 배포를 시작할 준비가 되 합니다. 다음 항목인 [빌드 정의 지원 배포 만들려면](creating-a-build-definition-that-supports-deployment.md), 작성 및 시기를 제어 하는 빌드 정의 구성 하는 방법 및 프로젝트 빌드 및 배포 방법에 대해 설명 합니다.

## <a name="further-reading"></a>추가 정보

팀 빌드를 사용한 작업에는 보다 일반적인 지침을 참조 하십시오. [Team Foundation Build 관리](https://msdn.microsoft.com/library/ms252495.aspx)합니다.

>[!div class="step-by-step"]
[이전](adding-content-to-source-control.md)
[다음](creating-a-build-definition-that-supports-deployment.md)
