---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
title: 웹 배포용 Team Foundation Server 구성 | Microsoft Docs
author: jrjlee
description: 이 자습서에서는 Team Foundation Server (TFS) 2010 솔루션을 빌드하고 다양 한 대상 환경에 웹 콘텐츠를 배포할 수를 구성 하는 방법을 보여줍니다. 이 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: ff55233a-e795-4007-a4fc-861fe1bb590b
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 6430a96a8e430a8a30d062ec22868de829680806
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365343"
---
<a name="configuring-team-foundation-server-for-web-deployment"></a>웹 배포용 Team Foundation Server 구성
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 자습서에서는 Team Foundation Server (TFS) 2010 솔루션을 빌드하고 다양 한 대상 환경에 웹 콘텐츠를 배포할 수를 구성 하는 방법을 보여줍니다. 배포할 콘텐츠가 자동으로 개발자가 변경할 때마다 CI (지속적인 통합) 시나리오를 포함 합니다. 수동 트리거 시나리오에서 관리자 수 하려는 빌드 확인 되었으며 테스트 환경에서 유효성이 검사 되 면 스테이징 환경에 특정 빌드 배포를 트리거하는 포함할 수도 있습니다. 이 자습서의 항목에서는 안내 전체 구성 프로세스에 포함 합니다.
> 
> - TFS에서 새 팀 프로젝트를 만드는 방법입니다.
> - 소스 제어에 콘텐츠를 추가 하는 방법.
> - CI 및 배포를 지원 하려면 빌드 서버를 구성 하는 방법입니다.
> - 배포 논리를 포함 하는 빌드 정의 만드는 방법입니다.
> - 자동화 된 배포에 대 한 권한을 구성 하는 방법입니다.
> 
> 이 자습서의 번역을 이탈리아어를 방문 [ http://www.lucamorelli.it ](http://www.lucamorelli.it)합니다.


이 자습서에는 TFS 2010을 설치 및 초기 구성 프로세스의 일부로 팀 프로젝트 컬렉션을 만든가 가정 합니다. 합니다 [Visual Studio 2010에 대 한 Team Foundation 설치 가이드](https://go.microsoft.com/?linkid=9805132) 이러한 작업에 대 한 포괄적인 지침을 제공 합니다.

## <a name="context"></a>컨텍스트

이 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 자습서 시리즈의 일부를 형성 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 솔루션&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.

이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="scenario-overview"></a>시나리오 개요

이 자습서에 대 한 상위 수준 시나리오에서 설명한 [엔터프라이즈 웹 배포: 시나리오 개요](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)합니다. 이 자습서를 시작 하기 전에이 항목을 검토 하는 것이 좋습니다.

## <a name="how-to-use-this-tutorial"></a>이 자습서를 사용하는 방법

처음으로이 경우이 자습서에 설명 된 작업을 수행 하거나 샘플 솔루션을 사용 하 여 예제를 실행 하려는 경우 순서로 자습서 항목을 진행 해야 합니다. 또는 특정 작업에 대 한 지침으로 개별 항목을 사용할 수 있습니다. 이 자습서는 이러한 항목이 포함 되어 있습니다.

- [TFS에서 팀 프로젝트를 만들면](creating-a-team-project-in-tfs.md)합니다. 팀 프로젝트는 소스 제어, 프로세스 관리 및 TFS에서 빌드에 대 한 핵심 단위입니다. 콘텐츠 소스 제어 또는 빌드 정의 만들기를 추가 하기 전에 팀 프로젝트를 생성 해야 합니다.
- [소스 제어에 콘텐츠 추가](adding-content-to-source-control.md)합니다. 팀 프로젝트를 만든 후 소스 제어에 콘텐츠 추가 시작할 수 있습니다. 빌드를 구성 하기 전에 프로젝트 및 솔루션, 모든 외부 종속성과 함께 추가 해야 합니다.
- [웹 배포에 대 한 빌드 서버를 TFS 구성](configuring-a-tfs-build-server-for-web-deployment.md)합니다. 팀 프로젝트 내용을 빌드 하려는 경우에 빌드 서버를 구성 해야 합니다. 대부분의 경우이 별도 컴퓨터에서 TFS 설치 해야 합니다. 빌드 서버를 구성 하려면 설치 하 고 TFS build service 구성, Visual Studio 2010을 설치, 빌드 컨트롤러를 만들기 및 빌드 에이전트, 모든 제품 또는 성공적으로 빌드 및 설치 하기 위해 코드에 필요한 구성 요소를 설치 합니다 IIS (인터넷 정보 서비스) 웹 배포 도구 (웹 배포).
- [배포를 지 원하는 빌드 정의 만들기](creating-a-build-definition-that-supports-deployment.md)합니다. 큐 또는 TFS에서 빌드를 트리거하여을 시작 하기 전에 팀 프로젝트에 대 한 하나 이상의 빌드 정의 만들기 해야 합니다. 빌드 정의 야 할 빌드에 포함 되어야 합니다, 새로운 빌드를 트리거해야, 팀 빌드를 빌드 출력을 전송 해야는 위치 등 빌드의 모든 측면을 정의 합니다. 자동화 된 빌드에 배포 논리를 포함할 수 있는 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 실행 하는 빌드 정의 구성할 수 있습니다.
- [특정 빌드 배포](deploying-a-specific-build.md)합니다. 많은 시나리오에서 대상 환경에 최근 빌드 후 보다는 특정 빌드를 배포 합니다. 이 경우 특정 저장 폴더의 콘텐츠를 배포 하는 빌드 정의 구성할 수 있습니다.
- [팀에 대 한 권한 구성 빌드 배포](configuring-permissions-for-team-build-deployment.md)합니다. 빌드 서비스를 자동화 된 빌드 프로세스의 일부로 콘텐츠를 배포 하려면 모든 대상 웹 서버와 데이터베이스 서버에 빌드 서비스 계정에 다양 한 사용 권한을 부여 해야 합니다.

## <a name="key-technologies"></a>핵심 기술

이 자습서는 자동화 된 빌드 및 웹 배포를 지원 하기 위해 이러한 제품과 기술을 사용 하는 방법에 중점을 둡니다.

- Visual Studio Team Foundation Server 2010
- 팀 빌드 및 MSBuild
- 웹 배포

Windows Server 2008 R2, IIS 7.5, SQL Server 2008 R2, ASP.NET 4.0 및 ASP.NET MVC 3의 사용에 관한 자습서도 살펴봅니다.

## <a name="other-tutorials-in-this-series"></a>이 시리즈의 다른 자습서

이 엔터프라이즈급 웹 배포에서 다섯 개의 자습서 시리즈의 일부를 형성합니다. 다른 자습서 시리즈의은 다음과 같습니다.

- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)합니다. 이 소개 콘텐츠 자습서 시리즈에 대 한 상황에 맞는 배경 정보를 제공 합니다. 자습서 시나리오를 설명 하 고 작업 및 연습 시리즈 전반에 설명 되어 광범위 한 응용 프로그램 수명 주기 관리 (ALM) 프로세스에 적합 하는 방법을 보여 줍니다.
- [엔터프라이즈 배포에서에서 웹](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)합니다. 이 자습서에서는 MSBuild 프로젝트 파일에 대 한 개념 소개, 웹 게시 파이프라인 (WPP), 웹 배포 및 기타 관련된 기술을 제공 합니다. 사용 하는 방법을 이러한 도구 함께 복잡 한 배포 프로세스를 관리 하려면 설명 합니다.
- [웹 배포용 서버 환경 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다. 이 자습서에는 웹 배포 에이전트 서비스 (원격 에이전트) 또는 웹 배포 처리기 및 원격 데이터베이스 배포를 사용 하 여 원격 웹 패키지 배포를 비롯 한 다양 한 배포 시나리오를 지원 하도록 Windows 서버를 구성 하는 방법을 설명 합니다. 사용자 고유의 환경에 대 한 적절 한 배포 방법 선택에 지침을 제공 하 고 웹 팜 프레임 워크 (WFF)를 사용 하 여 서버 팜의 모든 웹 서버에서 배포 된 웹 응용 프로그램을 복제 하는 방법을 설명 합니다.
- [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)합니다. 이 자습서에서는 사용자 지정 된 여러 환경에 대 한 데이터베이스 배포, 배포에서 파일 및 폴더 제외 하 고, 배포 프로세스 중 웹 응용 프로그램을 오프 라인 등 다양 한 고급 배포 작업을 수행 하는 방법 설명 .

> [!div class="step-by-step"]
> [다음](creating-a-team-project-in-tfs.md)
