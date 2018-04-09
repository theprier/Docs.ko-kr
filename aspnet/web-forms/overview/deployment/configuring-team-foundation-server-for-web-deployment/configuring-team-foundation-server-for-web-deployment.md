---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
title: 웹 배포에 대 한 Team Foundation Server 구성 | Microsoft Docs
author: jrjlee
description: 이 자습서에서는 Team Foundation Server (TFS) 2010 솔루션을 구축 하 다양 한 대상 환경에 웹 콘텐츠를 배포를 구성 하는 방법을 보여줍니다. 이 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: ff55233a-e795-4007-a4fc-861fe1bb590b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: c4cfac333c9400d9ee613ba88520b0b0439873f5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="configuring-team-foundation-server-for-web-deployment"></a>웹 배포에 대 한 Team Foundation Server 구성
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 자습서에서는 Team Foundation Server (TFS) 2010 솔루션을 구축 하 다양 한 대상 환경에 웹 콘텐츠를 배포를 구성 하는 방법을 보여줍니다. 여기서 콘텐츠를 배포 하면 자동으로 개발자가 변경 될 때마다 CI (연속 통합) 시나리오 포함 됩니다. 수동 트리거 있는 시나리오는, 관리자 수를 빌드 확인 되 고 테스트 환경에서 유효성이 검사 되 면 특정 빌드를 스테이징 환경으로 배포를 트리거하는 포함할 수도 있습니다. 이 자습서의 항목에서는 안내할 전체 구성 프로세스를 포함 하 여:
> 
> - TFS에서 새 팀 프로젝트를 만드는 방법.
> - 소스 제어에 콘텐츠를 추가 하는 방법.
> - CI 및 배포를 지원 하도록 빌드 서버를 구성 하는 방법입니다.
> - 배포 논리를 포함 하는 빌드 정의 만드는 방법.
> - 자동화 된 배포에 대 한 사용 권한을 구성 하는 방법.
> 
> 다음 자습서는 이탈리아어로 번역에 대 한 방문 [ http://www.lucamorelli.it ](http://www.lucamorelli.it)합니다.


이 자습서에서는 TFS 2010을 설치 하 고 초기 구성 프로세스의 일부로 팀 프로젝트 컬렉션을 만든 했는지를 가정 합니다. [for Visual Studio 2010 Team Foundation 설치 가이드](https://go.microsoft.com/?linkid=9805132) 이러한 작업에 대 한 포괄적인 지침을 제공 합니다.

## <a name="context"></a>컨텍스트

이 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 자습서 시리즈의 일부를 형성 샘플 솔루션을 사용 하는 자습서 시리즈가&#x2014;는 [않아](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 솔루션&#x2014;현실적인 수준의 복잡성, Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 WCF (foundation) 서비스 및 데이터베이스 프로젝트.

이 자습서의 핵심에는 배포 방법에 설명 된 분할 프로젝트 파일 접근 방식에 따라 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md), 두 개의 프로젝트 파일에 빌드 프로세스에 의해 제어 되는&#x2014;포함 환경 관련 빌드 및 배포 설정을 포함 하는 하나 및 모든 대상 환경에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 구성 하기 위해 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="scenario-overview"></a>시나리오 개요

이 자습서에 대 한 높은 수준의 시나리오에서 설명 [엔터프라이즈 웹 배포: 시나리오 개요](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)합니다. 이 자습서를 시작 하기 전에이 항목을 검토 하는 것이 좋습니다.

## <a name="how-to-use-this-tutorial"></a>이 자습서를 사용하는 방법

이 자습서에 설명 된 작업을 수행 했 고 처음으로 하는 경우 또는 순서로 자습서 항목 통해 작업 해야 샘플 솔루션을 사용 하 여 예제를 실행 하려는 경우. 또는 특정 작업에 대 한 지침으로 개별 항목을 사용할 수 있습니다. 이 자습서는 이러한 항목을 다룹니다.

- [TFS에서 팀 프로젝트를 만들면](creating-a-team-project-in-tfs.md)합니다. 팀 프로젝트에 소스 제어, 관리 프로세스 및 TFS에서 빌드에 대 한 핵심 단위입니다. 소스 제어 하거나 빌드 정의 만들 콘텐츠를 추가 하려면 먼저 팀 프로젝트를 만드는 데 필요 합니다.
- [소스 제어에 콘텐츠 추가](adding-content-to-source-control.md)합니다. 팀 프로젝트를 만든 후 소스 제어에 콘텐츠 추가 시작할 수 있습니다. 빌드를 구성 하기 전에 프로젝트 및 솔루션은 외부 종속성과 함께 추가 해야 합니다.
- [웹 배포에 대 한 TFS 구성 빌드 서버](configuring-a-tfs-build-server-for-web-deployment.md)합니다. 팀 프로젝트의 콘텐츠를 작성 하려면 빌드 서버를 구성 해야 합니다. 대부분의 경우가 TFS 설치에서 별도 컴퓨터에 있어야 합니다. 설치 하 고 TFS 빌드 서비스를 구성, Visual Studio 2010을 설치, 빌드 컨트롤러를 만들와 빌드 에이전트, 모든 제품 또는 코드를 빌드 및 설치 하는 데 필요한 구성 요소를 설치 해야 하는 빌드 서버를 구성 하려면는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포).
- [배포를 지원 하는 빌드 정의 만드는](creating-a-build-definition-that-supports-deployment.md)합니다. 큐 또는 TFS에서 빌드를 트리거를 시작 하려면 먼저 팀 프로젝트에 대 한 하나 이상의 빌드 정의를 만듭니다. 빌드 정의의 어느 부분이 빌드에 포함 되어야 합니다 빌드를 트리거할 기능 하 고 팀 빌드 보내야 위치 빌드 출력을 포함 하는 빌드 모든 측면을 정의 합니다. 자동화 된 빌드에 배포 논리를 포함할 수 있는 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 실행 하는 빌드 정의 구성할 수 있습니다.
- [특정 빌드를 배포](deploying-a-specific-build.md)합니다. 많은 시나리오를 대상 환경에 최신 빌드를 사용 하지 않고 특정 빌드를 배포 합니다. 이 경우 특정 드롭 폴더의 콘텐츠를 배포 하는 빌드 정의 구성할 수 있습니다.
- [팀에 대 한 구성 권한 빌드 배포](configuring-permissions-for-team-build-deployment.md)합니다. 빌드 서비스가 자동화 된 빌드 프로세스의 일부로 콘텐츠를 배포 하는 경우 모든 대상 웹 서버와 데이터베이스 서버에 빌드 서비스 계정에 다양 한 사용 권한을 부여 해야 합니다.

## <a name="key-technologies"></a>핵심 기술

이 자습서는 자동화 된 빌드 및 웹 배포를 지원 하기 위해 이러한 제품 및 기술을 사용 하는 방법에 중점을 둡니다.

- Visual Studio Team Foundation Server 2010
- 팀 빌드 및 MSBuild
- 웹 배포

이 자습서는 Windows Server 2008 R2, IIS 7.5, SQL Server 2008 R2, ASP.NET 4.0 및 ASP.NET MVC 3의 사용에는 대해서도 설명 합니다.

## <a name="other-tutorials-in-this-series"></a>이 시리즈의 다른 자습서

이 엔터프라이즈급 웹 배포에는 일련의 5 개 자습서의 일부를 형성합니다. 다른 자습서 시리즈에는 다음과 같습니다.

- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)합니다. 이 소개 콘텐츠는 자습서 시리즈에 대 한 상황에 맞는 배경 정보를 제공 합니다. 자습서 시나리오를 설명 하 고 작업 및 계열 전체에서 설명 하는 연습 광범위 한 관리 ALM (Application Lifecycle) 프로세스에 배치 하는 방법에 대해 설명 합니다.
- [웹 배포는 기업에서](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)합니다. 이 자습서에는 MSBuild 프로젝트 파일에 대 한 개념 소개, 웹 게시 파이프라인 (WPP), 웹 배포 및 기타 관련된 기술을 제공합니다. 방법을 함께 사용할 수 있습니다 이러한 도구 복잡 한 배포 프로세스를 관리 하에 대해 설명 합니다.
- [웹 배포를 위한 서버 환경을 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다. 이 자습서에서는 웹 배포 에이전트 서비스 (원격 에이전트) 또는 웹 배포 처리기 및 원격 데이터베이스 배포를 사용 하 여 원격 웹 패키지 배포를 비롯 한 다양 한 배포 시나리오를 지원 하기 위해 Windows 서버를 구성 하는 방법을 설명 합니다. 사용자 환경에 대 한 적절 한 배포 방법 선택에 지침을 제공 하 고 서버 팜의 모든 웹 서버에서 배포 된 웹 응용 프로그램을 복제 하기 위해 웹 팜 프레임 워크 (WFF)를 사용 하는 방법을 설명 합니다.
- [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)합니다. 이 자습서에서는 사용자 지정 된 여러 환경에 대 한 데이터베이스 배포, 배포에서 파일 및 폴더를 제외 하 고 배포 프로세스 중 웹 응용 프로그램을 오프 라인 등의 다양 한 고급 배포 작업을 수행 하는 방법을 설명합니다 .

> [!div class="step-by-step"]
> [다음](creating-a-team-project-in-tfs.md)
