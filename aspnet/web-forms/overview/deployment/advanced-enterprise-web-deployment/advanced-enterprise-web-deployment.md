---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
title: 고급 엔터프라이즈 웹 배포 | Microsoft Docs
author: jrjlee
description: 이 자습서에서는 필수 또는 다양 한 엔터프라이즈 배포 시나리오에서에서 적합할 수 있는 다양 한 작업을 수행 하는 방법을 보여줍니다. 이탈리아어 translati는에 대 한 중...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 7dcaba80-f2ec-4db3-ad98-daadc3afdb49
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 34f1bf3bc2c37afc66f458a60a29fe5ce8f6c018
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838780"
---
<a name="advanced-enterprise-web-deployment"></a>고급 엔터프라이즈 웹 배포
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 자습서에서는 필수 또는 다양 한 엔터프라이즈 배포 시나리오에서에서 적합할 수 있는 다양 한 작업을 수행 하는 방법을 보여줍니다.
> 
> 이 자습서의 번역을 이탈리아어를 방문 [ http://www.lucamorelli.it ](http://www.lucamorelli.it)합니다.


이 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 솔루션&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.

이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="scenario-overview"></a>시나리오 개요

이 자습서에 대 한 상위 수준 시나리오에서 설명한 [엔터프라이즈 웹 배포: 시나리오 개요](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)합니다. 이 자습서를 시작 하기 전에이 항목을 검토 하는 것이 좋습니다.

## <a name="how-to-use-this-tutorial"></a>이 자습서를 사용하는 방법

- 이 자습서의 항목에서는 각 자체 포함 되어 있으며 특정 문제 또는 엔터프라이즈 배포 시나리오에서 발생 하는 문제를 해결 합니다. 특정 한 순서로 이러한 항목을 진행할 필요가 없습니다. 그러나이 자습서에서는 몇 가지 고급 작업을 설명합니다. 이와 같이 개념 및 기술을 사용 하 여 잘 이해 해야 하는 합니다 [기업에서 웹 배포](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md) 이 콘텐츠에서 최대한 활용 하기 위해 자습서에서 다루는 합니다.
- 이 자습서는 이러한 항목이 포함 되어 있습니다.
- ["What If" 배포 수행](performing-a-what-if-deployment.md)합니다. 많은 시나리오에서 실제로 변경 하기 전에 대상 환경에 기존 내용을 제안 된 배포의 영향을 확인 해야 합니다. 이 항목에서는 실제로 변경 하지 않고 대상 환경으로 콘텐츠를 배포 했을 경우 처럼 로그 파일 및 데이터베이스 업데이트 스크립트를 생성 하는 "what if" 배포를 실행 하는 방법을 설명 합니다. 이러한 리소스를 분석에 도움 라이브 배포 하기 전에 잠재적인 문제를 식별 합니다.
- [여러 환경에 대 한 데이터베이스 배포를 사용자 지정](customizing-database-deployments-for-multiple-environments.md)합니다. 여러 대상에 데이터베이스 프로젝트를 배포할 때 각 대상 환경에 대 한 배포 속성을 사용자 지정 하려는 경우가 많습니다 됩니다. 예를 들어 테스트 환경에서 일반적으로 다시 만드는 모든 배포에서 데이터베이스 반면 스테이징 또는 프로덕션 환경에서 데이터를 유지 하기 위해 증분 업데이트를 수행할 가능성이 훨씬 더 됩니다. 이 항목에서는 각 대상 환경에 대 한 환경 관련 배포 구성 (.sqldeployment) 파일을 만들어 배포 논리를 이러한 속성 변경을 포함 하는 방법을 설명 합니다.
- 데이터베이스 역할 멤버 자격 테스트 환경에 배포 합니다. 모든 배포에서 데이터베이스를 다시 만들 때&#x2014;예를 들어, 연속 통합 (CI)의 일부로 빌드 및 테스트 환경에 배포&#x2014;일반적으로 때마다 데이터베이스 역할 멤버 자격을 구성 해야 합니다. 예를 들어, 웹 응용 프로그램과 연결 된 응용 프로그램 풀 id에 권한 부여 일반적으로 해야 합니다. 이 항목에서는 배포 후 SQL 스크립트를 배포 논리를 추가 하 여이 프로세스를 자동화 하는 방법을 설명 합니다.
- [엔터프라이즈 환경에 멤버 자격 데이터베이스 배포](deploying-membership-databases-to-enterprise-environments.md)합니다. ASP.NET 멤버 자격 데이터베이스에 배포 프로세스에 작업이 복잡 해질 수 있는 다양 한 특징이 있습니다. 예를 들어 스키마 전용 배포가 작동 하지 않는 상태의 데이터베이스가 종료 됩니다. 대부분의 시나리오에서는 각 대상 환경에서 직접 멤버 자격 데이터베이스를 만드는 것이 좋습니다. 그러나 멤버 자격 데이터베이스를 배포할 필요가 있는 경우이 항목에서는 몇 가지 고유한 과제를 충족 하는 데 사용할 수 방법 설명.
- [배포에서 파일 및 폴더 제외](excluding-files-and-folders-from-deployment.md)합니다. 일부 시나리오에서는 특정 대상 환경에 웹 패키지의 내용에 맞게 싶을 것입니다. 예를 들어, 다음 클라이언트 쪽 디버깅을 지원 하지만 스테이징 또는 프로덕션 환경에 배포 하는 경우에 축소 된 버전의 라이브러리를 사용 하 여 테스트 환경에 배포할 때 전체 버전의 JavaScript 라이브러리를 포함 하는 것이 좋습니다. 이 항목에서는 패키지 생성 프로세스에서 특정 파일 및 폴더를 제외할 수는 방법을 설명 합니다.
- [관련 웹 응용 프로그램은 오프 라인 웹 배포](taking-web-applications-offline-with-web-deploy.md)합니다. 스테이징 또는 프로덕션 환경에 솔루션을 배포할 때 배포 프로세스의 기간에 대 한 웹 응용 프로그램 오프 라인으로 수행 하려는 경우가 많습니다 됩니다. 이 항목에서는 추가 하는 방법에 대해 설명 합니다.는 *앱\_offline.htm* 배포 프로세스의 시작 시 웹 응용 프로그램에 파일을 끝에서 제거 합니다. 동안 합니다 *앱\_offline.htm* 파일 위치에 있으면 모든 사용자가 웹 응용 프로그램으로 이동 하는 자동으로 리디렉션됩니다 합니다 *앱\_offline.htm* 파일입니다.
- [MSBuild에서 Windows PowerShell 스크립트를 실행](running-windows-powershell-scripts-from-msbuild-project-files.md)합니다. 다양 한 배포 시나리오에는 레지스트리를 사용자 지정 이벤트 소스를 추가 하거나 SQL Server 인스턴스 간에 복제를 구성 같은 더 복잡 한 배포 후 작업을 필요 합니다. 이러한 작업은 Windows PowerShell 스크립트를 통해 수행 되기도 합니다. 이 항목에서는 빌드 및 배포 프로세스의 일환으로 Microsoft Build Engine (MSBuild) 프로젝트 파일에서 Windows PowerShell 스크립트를 실행 하는 방법을 설명 합니다.
- [패키징 프로세스 문제 해결](troubleshooting-the-packaging-process.md)합니다. 웹 게시 파이프라인 (WPP) 이라는 MSBuild 속성을 정의 **EnablePackageProcessLoggingAndAssert** 웹 응용 프로그램 프로젝트에 대 한 패키징 프로세스에 대 한 자세한 정보를 생성 하려면 사용할 수 있습니다. 이 항목에서는 속성의 용도 및 사용 하는 방법을 설명 합니다.

## <a name="key-technologies"></a>핵심 기술

이 자습서는 자동화 된 빌드 및 웹 배포를 지원 하기 위해 이러한 제품과 기술을 사용 하는 방법에 중점을 둡니다.

- Visual Studio 2010 및 TFS (Team Foundation Server) 2010
- MSBuild 및 TFS 팀 빌드
- 인터넷 정보 서비스 (IIS) 7.5
- IIS 웹 배포 도구 (웹 배포) 2.1
- VSDBCMD.exe 데이터베이스 배포 유틸리티

## <a name="other-tutorials-in-this-series"></a>이 시리즈의 다른 자습서

이 엔터프라이즈급 웹 배포에서 다섯 개의 자습서 시리즈의 일부를 형성합니다. 다른 자습서 시리즈의은 다음과 같습니다.

- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)합니다. 이 소개 콘텐츠 자습서 시리즈에 대 한 상황에 맞는 배경 정보를 제공 합니다. 자습서 시나리오를 설명 하 고 작업 및 연습 시리즈 전반에 설명 되어 광범위 한 응용 프로그램 수명 주기 관리 (ALM) 프로세스에 적합 하는 방법을 보여 줍니다.
- [엔터프라이즈 배포에서에서 웹](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)합니다. 이 자습서에서는 MSBuild 프로젝트 파일에 대 한 개념 소개, WPP, 웹 배포 및 기타 관련된 기술을 제공 합니다. 사용 하는 방법을 이러한 도구 함께 복잡 한 배포 프로세스를 관리 하려면 설명 합니다.
- [웹 배포용 서버 환경 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다. 이 자습서에는 웹 배포 에이전트 서비스 (원격 에이전트) 또는 웹 배포 처리기 및 원격 데이터베이스 배포를 사용 하 여 원격 웹 패키지 배포를 비롯 한 다양 한 배포 시나리오를 지원 하도록 Windows 서버를 구성 하는 방법을 설명 합니다. 사용자 고유의 환경에 대 한 적절 한 배포 방법 선택에 지침을 제공 하 고 웹 팜 프레임 워크 (WFF)를 사용 하 여 서버 팜의 모든 웹 서버에서 배포 된 웹 응용 프로그램을 복제 하는 방법을 설명 합니다.
- [웹 배포용 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다. 이 자습서에서는 수동으로 트리거된 배포 특정 빌드의 및 CI 프로세스의 일부로 자동화 된 배포를 포함 하 여 다양 한 배포 시나리오를 지원 하도록 TFS를 구성 하는 방법을 설명 합니다.

> [!div class="step-by-step"]
> [다음](performing-a-what-if-deployment.md)
