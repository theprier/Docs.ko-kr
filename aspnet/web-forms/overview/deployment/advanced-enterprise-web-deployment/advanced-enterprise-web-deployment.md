---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
title: 고급 엔터프라이즈 웹 배포 | Microsoft Docs
author: jrjlee
description: 이 자습서에서는 필요 없거나 에이전트 설치가 바람직하지 많은 엔터프라이즈 배포 시나리오는 다양 한 작업을 수행 하는 방법을 보여줍니다. 이탈리아어 translati에 대 한...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 7dcaba80-f2ec-4db3-ad98-daadc3afdb49
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 892e494b6fde994c4d04952382e4d618d73cad5c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879935"
---
<a name="advanced-enterprise-web-deployment"></a>고급 엔터프라이즈 웹 배포
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 자습서에서는 필요 없거나 에이전트 설치가 바람직하지 많은 엔터프라이즈 배포 시나리오는 다양 한 작업을 수행 하는 방법을 보여줍니다.
> 
> 다음 자습서는 이탈리아어로 번역에 대 한 방문 [ http://www.lucamorelli.it ](http://www.lucamorelli.it)합니다.


이 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 샘플 솔루션을 사용 하는 자습서 시리즈가&#x2014;는 [않아](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 솔루션&#x2014;현실적인 수준의 복잡성, Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 WCF (foundation) 서비스 및 데이터베이스 프로젝트.

이 자습서의 핵심에는 배포 방법에 설명 된 분할 프로젝트 파일 접근 방식에 따라 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md), 두 개의 프로젝트 파일에 빌드 프로세스에 의해 제어 되는&#x2014;포함 환경 관련 빌드 및 배포 설정을 포함 하는 하나 및 모든 대상 환경에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 구성 하기 위해 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="scenario-overview"></a>시나리오 개요

이 자습서에 대 한 높은 수준의 시나리오에서 설명 [엔터프라이즈 웹 배포: 시나리오 개요](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)합니다. 이 자습서를 시작 하기 전에이 항목을 검토 하는 것이 좋습니다.

## <a name="how-to-use-this-tutorial"></a>이 자습서를 사용하는 방법

- 각이 자습서의 항목은 독립적 이며 특정 챌린지 또는 엔터프라이즈 배포 시나리오에서 발생 하는 문제를 해결 합니다. 특정 한 순서로 이러한 항목을 통해 작동 필요가 없습니다. 그러나이 자습서에서는 몇 가지 고급 작업에 설명 합니다. 따라서 개념 및 기술을 잘 이해 해야 하는 [기업에서 웹 배포](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md) 이 콘텐츠는 최대한 활용 하기 위해 자습서에 설명 합니다.
- 이 자습서는 이러한 항목을 다룹니다.
- ["경우 어떻게" 배포](performing-a-what-if-deployment.md)합니다. 많은 시나리오를 실제로 변경 하기 전에 대상 환경 또는 기존 내용을에 제안 된 배포의 영향을 확인 합니다. 이 항목에서는 실제로 변경 하지 않고 대상 환경에 콘텐츠를 배포 했을 경우 처럼 로그 파일 및 데이터베이스 업데이트 스크립트를 생성 하는 "경우 어떻게" 배포를 실행 하는 방법을 설명 합니다. 이러한 리소스를 분석 하는 데 도움이 라이브 배포 하기 전에 잠재적인 문제를 식별 합니다.
- [사용자 지정 된 여러 환경에 대 한 데이터베이스 배포](customizing-database-deployments-for-multiple-environments.md)합니다. 여러 대상에 데이터베이스 프로젝트를 배포할 때 각 대상 환경에 대 한 배포 속성을 사용자 지정 하고자 합니다. 예를 들어 테스트 환경에서 일반적으로 다시 만드는 것 모든 배포에 있는 데이터베이스 반면 스테이징 또는 프로덕션 환경에서 수 더 많은 데이터를 보존 하도록 증분 업데이트를 수행 합니다. 이 항목에서는 각 대상 환경에 대 한 환경 관련 배포 (.sqldeployment) 구성 파일을 만들어 배포 논리에 이러한 속성이 변경을 포함 하는 방법을 설명 합니다.
- 데이터베이스 역할 멤버 자격이 테스트 환경에 배포 합니다. 모든 배포에 데이터베이스를 다시 만들&#x2014;예를 들어 연속 통합 (CI)의 일환으로 빌드 및 테스트 환경에 배포&#x2014;일반적으로 될 때마다 데이터베이스 역할 멤버 자격을 구성 해야 합니다. 예를 들어 웹 응용 프로그램과 연결 된 응용 프로그램 풀 id에 사용 권한을 부여 해야 일반적으로 합니다. 이 항목에서는 배포 후 SQL 스크립트를 배포 논리를 추가 하 여이 프로세스를 자동화 하는 방법을 설명 합니다.
- [멤버 자격 데이터베이스 엔터프라이즈 환경에 배포](deploying-membership-databases-to-enterprise-environments.md)합니다. ASP.NET 멤버 자격 데이터베이스의 경우 배포 프로세스 작업이 복잡 해질 수 있는 다양 한 특성입니다. 예를 들어 스키마 전용 배포 비작동 상태로 데이터베이스를 유지 됩니다. 대부분의 시나리오에서 각 대상 환경에 직접 멤버 자격 데이터베이스를 만드는 것이 좋습니다. 그러나 멤버 자격 데이터베이스를 배포할 필요가 있는 경우이 항목 내재 된 과제를 충족 하는 데 사용할 수는 방법 중 일부 설명 합니다.
- [배포에서 파일 및 폴더 제외](excluding-files-and-folders-from-deployment.md)합니다. 일부 시나리오에서는 특정 대상 환경에 웹 패키지의 내용에 맞게 합니다. 예를 들어, 다음 클라이언트 쪽 디버깅을 지원 하 되는 스테이징 또는 프로덕션 환경에 배포 하는 경우 축소 된 버전의 라이브러리를 사용 하 여 테스트 환경에 배포할 때 전체 버전의 JavaScript 라이브러리를 포함 하는 것이 좋습니다. 이 항목에서는 패키지 생성 프로세스에서 특정 파일 및 폴더를 제외할 수는 방법에 대해 설명 합니다.
- [기록 사용 웹 응용 프로그램 오프 라인 웹 배포](taking-web-applications-offline-with-web-deploy.md)합니다. 스테이징 또는 프로덕션 환경에 솔루션을 배포할 때 배포 프로세스 중에 웹 응용 프로그램 오프 라인으로 수행 해야 경우가 많습니다. 이 항목에서는 추가 하는 방법을 설명는 *앱\_offline.htm* 배포 프로세스의 시작 부분에 웹 응용 프로그램에 파일을 끝에서 제거 합니다. 반면는 *앱\_offline.htm* 파일 위치에 있으면 탐색 웹 응용 프로그램 하는 모든 사용자는 자동으로 리디렉션됩니다는 *앱\_offline.htm* 파일입니다.
- [MSBuild에서 Windows PowerShell 스크립트를 실행](running-windows-powershell-scripts-from-msbuild-project-files.md)합니다. 다양 한 배포 시나리오를 레지스트리에 사용자 지정 이벤트 소스를 추가 하거나 SQL Server 인스턴스 간 복제 구성 등의 더 복잡 한 배포 후 작업을 필요 합니다. 이러한 작업은 종종 Windows PowerShell 스크립트를 통해 수행 됩니다. 이 항목에서는 Microsoft Build Engine (MSBuild) 프로젝트 파일에서 빌드 및 배포 프로세스의 일환으로 Windows PowerShell 스크립트를 실행 하는 방법을 설명 합니다.
- [패키징 프로세스 문제 해결](troubleshooting-the-packaging-process.md)합니다. 웹 게시 파이프라인 (WPP) MSBuild 속성 이름이 정의 **EnablePackageProcessLoggingAndAssert** 웹 응용 프로그램 프로젝트에 대 한 패키징 프로세스에 대 한 자세한 정보를 생성 하는 데 사용할 수 있는 합니다. 이 항목에는 속성의 용도 및 사용 하는 방법을 설명 합니다.

## <a name="key-technologies"></a>핵심 기술

이 자습서는 자동화 된 빌드 및 웹 배포를 지원 하기 위해 이러한 제품 및 기술을 사용 하는 방법에 중점을 둡니다.

- Visual Studio 2010 및 Team Foundation Server (TFS) 2010
- MSBuild 및 TFS 팀 빌드
- 인터넷 정보 서비스 (IIS) 7.5
- IIS 웹 배포 도구 (웹 배포) 2.1
- VSDBCMD.exe 데이터베이스 배포 유틸리티

## <a name="other-tutorials-in-this-series"></a>이 시리즈의 다른 자습서

이 엔터프라이즈급 웹 배포에는 일련의 5 개 자습서의 일부를 형성합니다. 다른 자습서 시리즈에는 다음과 같습니다.

- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)합니다. 이 소개 콘텐츠는 자습서 시리즈에 대 한 상황에 맞는 배경 정보를 제공 합니다. 자습서 시나리오를 설명 하 고 작업 및 계열 전체에서 설명 하는 연습 광범위 한 관리 ALM (Application Lifecycle) 프로세스에 배치 하는 방법에 대해 설명 합니다.
- [웹 배포는 기업에서](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)합니다. 이 자습서에는 MSBuild 프로젝트 파일에 대 한 개념 소개, WPP, 웹 배포 및 기타 관련된 기술을 제공합니다. 방법을 함께 사용할 수 있습니다 이러한 도구 복잡 한 배포 프로세스를 관리 하에 대해 설명 합니다.
- [웹 배포를 위한 서버 환경을 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다. 이 자습서에서는 웹 배포 에이전트 서비스 (원격 에이전트) 또는 웹 배포 처리기 및 원격 데이터베이스 배포를 사용 하 여 원격 웹 패키지 배포를 비롯 한 다양 한 배포 시나리오를 지원 하기 위해 Windows 서버를 구성 하는 방법을 설명 합니다. 사용자 환경에 대 한 적절 한 배포 방법 선택에 지침을 제공 하 고 서버 팜의 모든 웹 서버에서 배포 된 웹 응용 프로그램을 복제 하기 위해 웹 팜 프레임 워크 (WFF)를 사용 하는 방법을 설명 합니다.
- [웹 배포에 대 한 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다. 이 자습서에서는 수동으로 배포의 특정 빌드를 트리거 및 CI 프로세스의 일부로 자동화 된 배포를 비롯 한 다양 한 배포 시나리오를 지원 하도록 TFS를 구성 하는 방법을 설명 합니다.

> [!div class="step-by-step"]
> [다음](performing-a-what-if-deployment.md)
