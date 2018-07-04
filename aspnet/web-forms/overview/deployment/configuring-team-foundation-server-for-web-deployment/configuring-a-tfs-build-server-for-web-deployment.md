---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
title: 웹 배포에 대 한 빌드 서버를 TFS 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 빌드 및 팀 빌드 및 인터넷 Informat를 사용 하 여 솔루션을 배포 하는 Team Foundation Server (TFS) 빌드 서버를 준비 하는 방법을 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: f8400241-4f4b-4bbd-9994-54fb64909e6e
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 12a18f601a75b607c97c46ecb7f68947ca3a342b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37382535"
---
<a name="configuring-a-tfs-build-server-for-web-deployment"></a>웹 배포용 TFS 빌드 서버 구성
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 빌드 및 팀 빌드 및 배포 (웹 배포)는 인터넷 정보 서비스 (IIS) 웹 배포 도구를 사용 하 여 솔루션을 배포 하는 Team Foundation Server (TFS) 빌드 서버를 준비 하는 방법을 설명 합니다.


이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.

이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="task-overview"></a>작업 개요

빌드 및 배포 솔루션을 빌드 서버를 준비 하려면를 해야 합니다.

- 설치 하 고 TFS 빌드 서비스를 구성 합니다.
- Visual Studio 2010을 설치 합니다.
- 모든 제품 또는 버전의.NET Framework 또는 ASP.NET MVC와 같은 솔루션을 빌드하는 데 필요한 구성 요소를 설치 합니다.
- 웹 배포 2.0 이상을 설치 합니다.

이 항목에서는 이러한 절차를 수행 하거나 이들이 존재 하는 다른 리소스를 가리키도록 하는 방법을 보여줍니다. 작업은이 문서의 연습 있다고 가정 합니다.

- Windows Server 2008 R2 서비스 팩 1을 실행 하는 새로운 서버 빌드를 사용 하 여 시작 합니다.
- 서버는 고정 IP 주소를 사용 하 여 도메인에 가입 된 경우
- 에 설명 된 대로 TFS 응용 프로그램 계층을 별도 서버를 설치 했습니다 [엔터프라이즈 웹 배포: 시나리오 개요](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)합니다.

### <a name="who-performs-these-procedures"></a>이러한 절차를 수행 하는 사람?

대부분의 경우에서 TFS 관리자가 빌드 서버를 구성 해야 합니다. 경우에 따라 개발자 팀 특정 빌드 서버의 소유권을 가져올 수 있습니다.

## <a name="install-and-configure-the-tfs-build-service"></a>TFS 빌드 서비스 설치 및 구성

빌드 서버를 구성할 때 먼저 TFS 빌드 서비스 설치 및 구성 방법은입니다. 이 프로세스의 일부로 해야 합니다.

- TFS 빌드 서비스를 설치 하 고 서비스 계정을 구성 합니다. 배포를 비롯 한 모든 빌드 작업, 빌드 서비스 계정의 id를 사용 하 여 실행 됩니다.
- 만들기는 *빌드 컨트롤러* 와 하나 이상의 *빌드 에이전트*합니다. 각 빌드 컨트롤러는 빌드 에이전트 집합을 관리합니다. 빌드를 큐에 대기 하는 경우 빌드 컨트롤러 사용 가능한 빌드 에이전트에 빌드 작업을 할당 합니다. TFS에서 각 팀 프로젝트 컬렉션을 단일 빌드 컨트롤러에 매핑됩니다.
- 빌드 출력에 대 한 drop 폴더를 구성 합니다. 네트워크 공유입니다. 모든 웹 배포 패키지와 같은 출력을 빌드, 드롭 폴더로 전송 됩니다.

합니다 [Team Foundation Build 관리](https://msdn.microsoft.com/library/ms252495.aspx) 장에서 MSDN의 이러한 작업을 수행 하는 데 필요한 모든 리소스를 포함 합니다.

- Team Foundation Build의 개념적인 개요를 비롯 한 빌드 서비스를 빌드 컨트롤러와 빌드 에이전트 참조 [Team Foundation Build 시스템 이해](https://msdn.microsoft.com/library/dd793166.aspx)합니다.
- 빌드 서비스 설치 및 구성에 대 한 내용은 참조 하세요 [빌드 컴퓨터를 구성](https://msdn.microsoft.com/library/ms181712.aspx)합니다.
- 빌드 컨트롤러를 만드는 방법에 대 한 정보를 참조 하세요 [작업 만들기 및 빌드 컨트롤러 사용](https://msdn.microsoft.com/library/ee330987.aspx)합니다.
- 빌드 에이전트 만들기에 대 한 내용은 참조 하세요 [만들기 및 빌드 에이전트를 사용 하 여 작업](https://msdn.microsoft.com/library/bb399135.aspx)합니다.
- 만들기 및 저장 폴더를 구성에 대 한 내용은 참조 하세요 [저장 폴더 설정](https://msdn.microsoft.com/library/bb778394.aspx)합니다.

## <a name="install-required-products-and-components"></a>필요한 제품 및 구성 요소를 설치 합니다.

솔루션을 빌드하려면 빌드 서버를 사용 하려면 모든 제품, 구성 요소 또는 솔루션에 필요한 어셈블리를 설치 해야 합니다. 모든 웹 플랫폼 구성 요소를 설치 하기 전에 Visual Studio 2010 (모든 버전) 빌드 서버에 설치 해야 합니다. 이렇게 하면 핵심 Microsoft Build Engine (MSBuild) 대상 파일 및 웹 게시 파이프라인 (WPP) 대상 파일은 빌드 서비스를 사용할 수 있습니다. Visual Studio 설치 관리자 빌드 프로세스의 일부로 웹 패키지를 배포 하려는 경우 필요한 웹 배포 설치 해야 합니다.

일반적인 웹 플랫폼 구성 요소를 설치 하는 가장 좋은 방법은 사용 하는 것은 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)합니다. 이렇게 하면 각 제품의 최신 버전을 설치 하는 자동으로 감지 하 고 각 제품에 대 한 모든 필수 구성 요소를 설치 합니다. 경우에 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 솔루션에서는 이러한 제품 및 구성 요소를 설치 하려면 웹 플랫폼 설치 관리자를 사용 해야 합니다.

- **.NET Framework 4.0**. 이 버전의.NET Framework에서 빌드된 응용 프로그램을 실행 해야 합니다.
- **웹 배포 도구 2.1 이상**합니다. 서버에 웹 배포 (및 해당 기본 실행 파일, MSDeploy.exe)를 설치합니다. 이 프로세스의 일부로 설치 하 고 웹 배포 에이전트 서비스를 시작 합니다. 이 서비스를 사용 하면 원격 컴퓨터에서 웹 패키지를 배포할 수 있습니다.
- **ASP.NET MVC 3**합니다. ASP.NET MVC 3 응용 프로그램을 실행 해야 하는 어셈블리를 설치 합니다.

**필요한 제품 및 구성 요소를 설치 하려면**

1. Visual Studio 2010을 설치 합니다. 를 설치할 기능 선택 하 라는 메시지가 포함 해야 합니다.

    1. 컴파일하는 데 필요한 모든 프로그래밍 언어입니다.
    2. Visual Web Developer입니다. 이렇게 하면 WPP 대상 빌드 서버에 추가 된 것입니다.

        ![](configuring-a-tfs-build-server-for-web-deployment/_static/image1.png)
2. Visual Studio 2010의 설치가 완료 되 면 다운로드 및 설치 [Visual Studio 2010 서비스 팩 1](https://go.microsoft.com/?linkid=9805133) (하는 경우이 아직 포함 되지 않은 설치 미디어에서).

    > [!NOTE]
    > Visual Studio 2010 서비스 팩 1 실행 MSDeploy 찾기에서 MSBuild를 방해할 수 있는 버그를 확인 합니다.
3. 다운로드 하 고 시작 합니다 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)합니다.
4. 맨 위에 있는 합니다 **웹 플랫폼 설치 관리자 3.0** 창에서 클릭 **제품**합니다.
5. 왼쪽 탐색 창에서 창에서 클릭 **프레임 워크**합니다.
6. 에 **Microsoft.NET Framework 4** 행을.NET Framework가 이미 설치 되어 있지 않으면 클릭 **추가**합니다.

    > [!NOTE]
    > 이미 설치한 Windows Update를 통해.NET Framework 4.0입니다. 제품 또는 구성 요소를 이미 설치 되어 웹 플랫폼 설치 관리자는이 표시할 대체 하 여 합니다 **추가** 텍스트가 있는 단추 **설치 된**합니다.

    ![](configuring-a-tfs-build-server-for-web-deployment/_static/image2.png)
7. 에 **ASP.NET MVC 3 (Visual Studio 2010)** 행을 클릭 **추가**합니다.
8. 탐색 창에서 클릭 **Server**합니다.
9. 에 **웹 배포 도구 2.1** 행을 클릭 **추가**합니다.
10. **설치**를 클릭합니다. 웹 플랫폼 설치 관리자 제품의 목록이 표시 됩니다&#x2014;연결 된 종속성을와 함께&#x2014;를 설치 및 사용 조건에 동의 하 라는 메시지가 표시 됩니다.
11. 사용 조건을 검토 하 고 사용자가 약관에 동의 하면 클릭 **동의**합니다.
12. 설치가 완료 되 면 클릭 **완료**를 닫은 다음 합니다 **웹 플랫폼 설치 관리자 3.0** 창입니다.

> [!NOTE]
> 배포 프로세스 VSDBCMD.exe 또는 SQLCMD.exe와 같은 도구 사용에 포함 된 경우에 이러한 빌드 서버에 설치 되어 있는지 확인 해야 합니다. VSDBCMD.exe는 Visual Studio 도구 및 Team Foundation Build를 설치할 때 서버에 일반적으로 추가 됩니다. SQLCMD.exe는 SQL Server 도구입니다. 독립 실행형 버전에서 sqlcmd.exe를 다운로드할 수 있습니다 합니다 [Microsoft SQL Server 2008 R2 기능 팩](https://go.microsoft.com/?linkid=9805134) 페이지입니다.


## <a name="conclusion"></a>결론

이 시점에서 빌드 서버를 빌드 및 웹 응용 프로그램 프로젝트 배포를 시작할 준비가 됩니다. 다음 항목인 [배포를 만드는 빌드 정의 지원](creating-a-build-definition-that-supports-deployment.md), 만들기 및 시기를 제어 하는 빌드 정의 구성 하는 방법 및 프로젝트 빌드 및 배포 하는 방법에 대해 설명 합니다.

## <a name="further-reading"></a>추가 정보

팀 빌드와 작업에 대 한 보다 일반적인 지침을 참조 하세요 [Team Foundation Build 관리](https://msdn.microsoft.com/library/ms252495.aspx)합니다.

> [!div class="step-by-step"]
> [이전](adding-content-to-source-control.md)
> [다음](creating-a-build-definition-that-supports-deployment.md)
