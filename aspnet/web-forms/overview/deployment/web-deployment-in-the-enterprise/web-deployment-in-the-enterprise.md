---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
title: 엔터프라이즈 배포에서에서 웹 | Microsoft Docs
author: jrjlee
description: 이 자습서에서는 많은 개발자에 엔터프라이즈급 웹 응용 프로그램 배포를 관리 하는 경우 접할 수 과제를 충족 하는 방법을 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: b8283698-7b82-42a8-8d83-3aeb18ca7fcc
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
msc.type: authoredcontent
ms.openlocfilehash: 07c1ea9728c0130b860c0e0a64eb0751245ff840
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371144"
---
<a name="web-deployment-in-the-enterprise"></a>기업에서 웹 배포
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 자습서에는 많은 개발, 테스트, 스테이징 및 프로덕션 환경에 엔터프라이즈급 웹 응용 프로그램 배포를 관리할 때 발생 하는 과제를 충족 하는 방법을 설명 합니다. 자습서에는 다양 한 일반 작업 및 절차를 안내 하는 개념 및 작업 기반 콘텐츠 혼합 함께 참조 솔루션을 포함 합니다.
> 
> 이 자습서의 번역을 이탈리아어를 방문 [ http://www.lucamorelli.it ](http://www.lucamorelli.it)합니다.


## <a name="enterprise-deployment-challenges"></a>엔터프라이즈 배포 과제

조직에서는 복잡 한 엔터프라이즈급 솔루션의 배포를 관리 하는 경우 이러한 문제를 자주 발견:

- 해야 있으려면 개발자와 같은 여러 환경에 프로젝트를 배포 또는 테스트 환경, 플랫폼 및 프로덕션 서버를 준비 합니다. 각 환경에 대 한 다른 구성 설정을 사용 하 여 배포 해야 하는 솔루션입니다.
- 단일 단계 또는 자동화 된 빌드 및 배포 프로세스의 일환으로 동시에 여러 종속 프로젝트를 배포 해야 합니다.
- 자동화 된 프로세스에서 드라이브 배포 수 있게 해야 합니다. 예를 들어, 새 코드를 체크 인할 때 웹 응용 프로그램 테스트 환경에 배포 하는 CI (지속적인 통합) 프로세스를 사용 하려면.
- 모든 대상 환경에 필요한 자격 증명 또는 잘못 구성 설정이 않을 것으로 배포 프로세스를 제어 하 고 Visual Studio 외부에서 배포 변수를 설정 하는 일을 할 수 해야 합니다.
- 데이터베이스 스키마 기반 프로젝트를 배포 하 고 후속 배포에서 기존 데이터를 유지 해야 합니다.
- 사용자 계정 데이터를 배포 하지 않고 임시 단위로 멤버 자격 데이터베이스를 배포 해야 합니다. 기존 사용자 계정 데이터 손실 없이 배포 된 멤버 자격 데이터베이스의 스키마를 업데이트 해야 합니다.
- 다양 한 대상 환경에 콘텐츠를 배포할 때 특정 파일 또는 폴더를 제외 해야 합니다.

## <a name="overview-of-approach"></a>접근 방법의 개요

이 시리즈의 다른 자습서와 함께이 자습서에서는이 고급 방법을 사용 하 여 위에 설명 된 과제를 충족 합니다.

- **전체 빌드 및 배포 프로세스를 제어 하려면 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 합니다.**
- 이렇게 하면 빌드 및 스크립트 가능한 단일 작업의 일부분으로 솔루션의 모든 프로젝트를 배포할 수 있습니다.
- 환경 관련 설정 간단한 환경별 프로젝트 파일을 사용 하 여 구성 됩니다. 솔루션 구성을 사용 하 여 Visual Studio – 중심 방식을 달리 다른 환경에 대 한 배포를 구성 하기 위해 게시 프로필을이 이렇게 구성 하 고 Visual Studio 외부에서 배포 프로세스를 관리할 수 있습니다. 즉, 개발자가 없는 연결 문자열, 서비스 끝점, 서버 자격 증명 및 기타 배포 변수에 대상 환경에 대 한 지식이 이동 해야 합니다.
- Team Foundation Server (TFS) 워크플로의 일부로 팀 빌드에서 사용자 지정 프로젝트 파일을 호출할 수 있습니다. 이 CI 시나리오에 대 한 자동화 된 배포를 구성할 수 있습니다.

**인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 패키지 및 웹 응용 프로그램 프로젝트를 배포 합니다.**

- 웹 배포 패키지 및 종속성, 구성 설정, 보안 설정 및 기타 요구 사항 함께 대상 IIS 웹 서버에 웹 응용 프로그램 콘텐츠를 배포할 수 있는 프레임 워크를 제공 합니다.
- 사용자 지정 MSBuild 프로젝트 파일 내에서 전체 패키징 및 배포 프로세스를 제어할 수 있습니다. 또한 IIS 대상 세부 정보, 연결 문자열 및 서비스 끝점 등 웹 배포 패키지와 함께 제공 되는 구성 파일을 조작할 수 있습니다.
- 웹 게시 파이프라인을 함께 웹 배포는 다양 한 배포를 사용자 지정할 수 있는 확장성 지점 제공 합니다. 예를 들어, 웹 배포 패키지에서 원하지 않는 파일 및 폴더를 제외 하기 쉽습니다.

**VSDBCMD.exe 유틸리티를 사용 하 여 배포 하 여 데이터베이스 스키마를 업데이트 합니다.**

- VSDBCMD을 사용 하면 Visual Studio 데이터베이스 프로젝트를 빌드할 때 생성 되는 데이터베이스 스키마 파일 (.dbschema)에서 데이터베이스를 배포할 수 있습니다. 반면, 웹 배포에 포함 된 데이터베이스 배포 기능은 로컬 SQL Server 인스턴스에서 기존 데이터베이스를 배포 하는 데 더 적합 합니다.
- 데이터베이스 프로젝트를 배포 하기 위한 Visual Studio의 기능을 달리 VSDBCMD 기존 대상 데이터베이스에 차등 업데이트를 배포할 수 있습니다. 이 옵션을 사용 하면 데이터베이스 스키마를 업그레이드 하는 동안 모든 기존 데이터를 유지할 수 있습니다.
- 사용자 지정 MSBuild 프로젝트 파일 내에서 VSDBCMD 명령을 실행할 수 있습니다.

## <a name="content-map"></a>콘텐츠 맵

이 자습서에는 네 가지 주요 영역에 부합 하는 항목이 포함 되어 있습니다.

이러한 항목을 참조 솔루션 소개&#x2014;Contact Manager 솔루션&#x2014;다운로드 하 여 로컬 컴퓨터에 구성 하는 방법을 설명 합니다.

- [Contact Manager 솔루션](the-contact-manager-solution.md)
- [Contact Manager 솔루션 설정](setting-up-the-contact-manager-solution.md)

이러한 항목 MSBuild 프로젝트 파일을 소개, 만들기 및 사용자 지정 프로젝트 파일을 사용 하는 방법 Contact Manager 솔루션에 대 한 배포 프로세스를 단계별로 설명 합니다.

- [프로젝트 파일 이해](understanding-the-project-file.md)
- [빌드 프로세스 이해](understanding-the-build-process.md)

빌드 및 패키징 프로세스 작동 방식, 웹 게시 파이프라인을 사용 하 여 빌드 프로세스를 통합 하는 방법, 배포 매개 변수를 수정 하는 방법 및 대상 웹 패키지를 배포 하는 방법을 포함 하 여 웹 응용 프로그램 배포에 설명 환경:

- [웹 응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md)
- [웹 패키지 배포용 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)
- [웹 패키지 배포](deploying-web-packages.md)

- [데이터베이스 프로젝트 배포](deploying-database-projects.md) 장점과 각 접근 방식의 단점와 함께 Visual Studio 데이터베이스 프로젝트를 배포 하 여 다양 한 기법에 설명 합니다. [만들기 및 배포 명령 파일을 실행](creating-and-running-a-deployment-command-file.md) 배포 논리를 캡슐화 하 고 단일 단계 프로세스로 복잡 한 솔루션을 배포할 수 있습니다 하는 간단한 명령 파일을 만드는 방법을 설명 합니다.
- 마지막으로, [수동으로 웹 패키지 설치](manually-installing-web-packages.md) 으로 IIS 웹 패키지를 가져올 수를 표시 하 여 자습서를 마칩니다.

## <a name="key-technologies"></a>핵심 기술

이 자습서의 항목에서는 주로이 기술을 사용 하 여 이러한 빌드 및 배포를 관리 합니다.

- Visual Studio 2010
- MSBuild
- IIS 7.5
- 웹 배포 2.0
- VSDBCMD.exe 데이터베이스 배포 유틸리티

## <a name="other-tutorials-in-this-series"></a>이 시리즈의 다른 자습서

이 엔터프라이즈급 웹 배포에서 다섯 개의 자습서 시리즈의 일부를 형성합니다. 다른 자습서 시리즈의은 다음과 같습니다.

- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)합니다. 이 소개 콘텐츠 자습서 시리즈에 대 한 상황에 맞는 배경 정보를 제공 합니다. 자습서 시나리오를 설명 하 고 작업 및 연습 시리즈 전반에 설명 되어 광범위 한 응용 프로그램 수명 주기 관리 (ALM) 프로세스에 적합 하는 방법을 보여 줍니다.
- [웹 배포용 서버 환경 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다. 이 자습서에는 웹 배포 에이전트 서비스 (원격 에이전트) 또는 웹 배포 처리기 및 원격 데이터베이스 배포를 사용 하 여 원격 웹 패키지 배포를 비롯 한 다양 한 배포 시나리오를 지원 하도록 Windows 서버를 구성 하는 방법을 설명 합니다. 사용자 고유의 환경에 대 한 적절 한 배포 방법 선택에 지침을 제공 하 고 웹 팜 프레임 워크 (WFF)를 사용 하 여 서버 팜의 모든 웹 서버에서 배포 된 웹 응용 프로그램을 복제 하는 방법을 설명 합니다.
- [웹 배포용 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다. 이 자습서에서는 수동으로 트리거된 배포 특정 빌드의 및 CI 프로세스의 일부로 자동화 된 배포를 포함 하 여 다양 한 배포 시나리오를 지원 하도록 TFS를 구성 하는 방법을 설명 합니다.
- [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)합니다. 이 자습서에서는 사용자 지정 된 여러 환경에 대 한 데이터베이스 배포, 배포에서 파일 및 폴더 제외 하 고, 배포 프로세스 중 웹 응용 프로그램을 오프 라인 등 다양 한 고급 배포 작업을 수행 하는 방법 설명 .

> [!div class="step-by-step"]
> [다음](the-contact-manager-solution.md)
