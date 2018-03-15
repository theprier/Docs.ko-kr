---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
title: "웹 배포는 기업에서 | Microsoft Docs"
author: jrjlee
description: "이 자습서에서는 다양 한 개발자의 엔터프라이즈급 웹 응용 프로그램의 배포를 관리 하는 경우 발생 하는 과제를 충족 하는 방법을 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: b8283698-7b82-42a8-8d83-3aeb18ca7fcc
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
msc.type: authoredcontent
ms.openlocfilehash: 6210d01f65bcadf8ae4209e372d5aac68861bd7a
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
<a name="web-deployment-in-the-enterprise"></a>기업에서 웹 배포
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 자습서에서는 다양 한 엔터프라이즈급 웹 응용 프로그램을 개발, 테스트, 스테이징 및 프로덕션 환경 배포를 관리 하는 경우 발생 하는 문제를 충족 하는 방법을 설명 합니다. 이 자습서의 개념 및 작업 기반 콘텐츠를 다양 한 일반 작업 및 절차를 안내 하는 혼합 함께 참조 솔루션에 포함 됩니다.
> 
> 다음 자습서는 이탈리아어로 번역에 대 한 방문 [ http://www.lucamorelli.it ](http://www.lucamorelli.it)합니다.


## <a name="enterprise-deployment-challenges"></a>엔터프라이즈 배포 문제

조직에서는 자주, 복잡 한 엔터프라이즈급 솔루션 배포를 관리 하는 경우 이러한 문제를 발생 합니다.

- 해야 개발자와 같은 여러 환경에 프로젝트를 배포 하거나 테스트 환경에서는 수 플랫폼 및 프로덕션 서버를 준비 합니다. 솔루션은 각 환경에 대해 서로 다른 구성 설정을 사용 하 여 배포 해야 합니다.
- 단일 단계 또는 자동화 된 빌드 및 배포 프로세스의 일환으로 동시에 여러 종속 프로젝트를 배포 해야 합니다.
- 자동화 된 프로세스에서 드라이브 배포를 실행할 수 있도록 해야 합니다. 예를 들어 새 코드를 체크 인할 때 웹 응용 프로그램을 테스트 환경에 배포 하려면 CI (연속 통합) 프로세스를 사용 하려면.
- 올바른 구성 설정 또는 모든 대상 환경에 대 한 필요한 자격 증명을 않을 것 처럼 하 배포 프로세스를 제어 하 고 Visual Studio 외부에서 배포 변수를 설정 해야 합니다.
- 데이터베이스 스키마 기반 프로젝트를 배포 하 고 후속 배포에서 기존 데이터를 유지 해야 합니다.
- 사용자 계정 데이터를 배포 하지 않고 멤버 자격 데이터베이스 임시로에 배포 해야 합니다. 또한 기존 사용자 계정 데이터 손실 없이 배포 된 멤버 자격 데이터베이스의 스키마를 업데이트 해야 할 수 있습니다.
- 다양 한 대상 환경에 콘텐츠를 배포할 때 특정 파일 또는 폴더를 제외 해야 합니다.

## <a name="overview-of-approach"></a>접근 방법의 개요

이 자습서에서는이 시리즈의 다른 자습서와 함께이 높은 수준의 방법을 사용 하 여 위에서 설명한 과제를 충족 합니다.

- **전체 빌드 및 배포 프로세스 제어 기능을 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 합니다.**
- 이렇게 하면 단일 하 고 스크립트 가능한 작업의 일환으로 솔루션의 모든 프로젝트를 배포 합니다.
- 환경 관련 설정이 간단한 환경별 프로젝트 파일을 사용 하 여 구성 됩니다. 솔루션 구성을 사용 하 여 Visual Studio-중심 방법은 반대 및 다양 한 환경에 대 한 배포를 구성 하기 위해 게시 프로필,이 방법 구성 하 고 Visual Studio 외부에서 배포 프로세스를 관리할 수 있습니다. 즉, 개발자 하지 않는 연결 문자열, 서비스 끝점, 서버 자격 증명 및 기타 배포 변수 대상 환경에 대 한 기술 이동 해야 합니다.
- Team Foundation Server (TFS) 워크플로의 일부로 팀 빌드 사용자 지정 프로젝트 파일을 호출할 수 있습니다. 이 CI 시나리오에 대 한 자동화 된 배포를 구성할 수 있습니다.

**인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 패키지 및 웹 응용 프로그램 프로젝트를 배포 합니다.**

- 웹 배포 패키지 및 종속성, 구성 설정, 보안 설정 및 기타 요구 사항을 함께 대상 IIS 웹 서버에 웹 응용 프로그램 콘텐츠를 배포할 수 있는 프레임 워크를 제공 합니다.
- 사용자 지정 MSBuild 프로젝트 파일 내에서 전체 패키징 및 배포 프로세스를 제어할 수 있습니다. 웹 배포 패키지, 같은 연결 문자열, 서비스 끝점 및 IIS 대상 세부 정보를 함께 사용 해야 하는 구성 설정은 조작할 수 있습니다.
- 웹 배포가 웹 게시 파이프라인 함께 다양 한 배포를 사용자 지정할 수 있는 확장 지점 제공 합니다. 예를 들어, 웹 배포 패키지에서 원치 않는 파일 및 폴더를 제외 하기 쉽습니다.

**VSDBCMD.exe 유틸리티를 사용 하 여 배포 및 데이터베이스 스키마를 업데이트 합니다.**

- VSDBCMD을 사용 하면 Visual Studio 데이터베이스 프로젝트를 빌드할 때 생성 되는 데이터베이스 스키마 파일 (.dbschema)에서 데이터베이스를 배포할 수 있습니다. 반면 웹 배포에 포함 된 데이터베이스 배포 기능을 로컬 SQL Server 인스턴스에서 기존 데이터베이스를 배포 하는 데 더 적합 합니다.
- 데이터베이스 프로젝트를 배포 하기 위한 Visual Studio의 기능, 달리 VSDBCMD 기존 대상 데이터베이스에 차등 업데이트를 배포할 수 있습니다. 이 옵션을 사용 하면 데이터베이스 스키마를 업그레이드 하는 동안 모든 기존 데이터를 유지할 수 있습니다.
- 사용자 지정 MSBuild 프로젝트 파일 내에서 VSDBCMD 명령을 실행할 수 있습니다.

## <a name="content-map"></a>콘텐츠 맵

이 자습서에는 네 가지 주요 영역에 해당 하는 항목이 포함 되어 있습니다.

이러한 항목 참조 솔루션 & #x 2014;는 Contact Manager 솔루션 & #x 2014; 소개 하 고 다운로드 한 로컬 컴퓨터에서 구성 하는 방법을 설명 합니다.

- [Contact Manager 솔루션](the-contact-manager-solution.md)
- [Contact Manager 솔루션 설정](setting-up-the-contact-manager-solution.md)

MSBuild 프로젝트 파일을 소개 하, 만들기 및 사용자 지정 프로젝트 파일을 사용 하는 방법을 않아 솔루션에 대 한 배포 프로세스를 안내를 설명 하는 다음이 항목:

- [프로젝트 파일 이해](understanding-the-project-file.md)
- [빌드 프로세스 이해](understanding-the-build-process.md)

이 항목에서는 웹 응용 프로그램 배포를 빌드 및 패키징 프로세스 작동 방식, 빌드 프로세스 웹 게시 파이프라인으로 통합 하는 방법, 배포 매개 변수를 수정 하는 방법 및 대상에 웹 패키지를 배포 하는 방법을 비롯 한 설명 환경:

- [웹 응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md)
- [웹 패키지 배포용 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)
- [웹 패키지 배포](deploying-web-packages.md)

- [데이터베이스 프로젝트 배포](deploying-database-projects.md) 각 방법의 장단점와 함께 Visual Studio 데이터베이스 프로젝트를 배포 하는 데 다양 한 기술을 설명 합니다. [만들기 및 배포 명령 파일을 실행](creating-and-running-a-deployment-command-file.md) 배포 논리를 캡슐화 하 고 단일 단계 프로세스로 복잡 한 솔루션을 배포할 수 있습니다 하는 간단한 명령 파일을 만드는 방법을 설명 합니다.
- 마지막으로, [수동으로 웹 패키지 설치](manually-installing-web-packages.md) 으로 IIS에 웹 패키지를 가져올 수를 표시 하 여 자습서를 마칩니다.

## <a name="key-technologies"></a>핵심 기술

이 자습서의 항목에서는 주로 이러한 기술을 사용 하 여 빌드 및 배포를 관리 하려면:

- Visual Studio 2010
- MSBuild
- IIS 7.5
- 웹 배포 2.0
- VSDBCMD.exe 데이터베이스 배포 유틸리티

## <a name="other-tutorials-in-this-series"></a>이 시리즈의 다른 자습서

이 엔터프라이즈급 웹 배포에는 일련의 5 개 자습서의 일부를 형성합니다. 다른 자습서 시리즈에는 다음과 같습니다.

- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)합니다. 이 소개 콘텐츠는 자습서 시리즈에 대 한 상황에 맞는 배경 정보를 제공 합니다. 자습서 시나리오를 설명 하 고 작업 및 계열 전체에서 설명 하는 연습 광범위 한 관리 ALM (Application Lifecycle) 프로세스에 배치 하는 방법에 대해 설명 합니다.
- [웹 배포를 위한 서버 환경을 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다. 이 자습서에서는 웹 배포 에이전트 서비스 (원격 에이전트) 또는 웹 배포 처리기 및 원격 데이터베이스 배포를 사용 하 여 원격 웹 패키지 배포를 비롯 한 다양 한 배포 시나리오를 지원 하기 위해 Windows 서버를 구성 하는 방법을 설명 합니다. 사용자 환경에 대 한 적절 한 배포 방법 선택에 지침을 제공 하 고 서버 팜의 모든 웹 서버에서 배포 된 웹 응용 프로그램을 복제 하기 위해 웹 팜 프레임 워크 (WFF)를 사용 하는 방법을 설명 합니다.
- [웹 배포에 대 한 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다. 이 자습서에서는 수동으로 배포의 특정 빌드를 트리거 및 CI 프로세스의 일부로 자동화 된 배포를 비롯 한 다양 한 배포 시나리오를 지원 하도록 TFS를 구성 하는 방법을 설명 합니다.
- [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)합니다. 이 자습서에서는 사용자 지정 된 여러 환경에 대 한 데이터베이스 배포, 배포에서 파일 및 폴더를 제외 하 고 배포 프로세스 중 웹 응용 프로그램을 오프 라인 등의 다양 한 고급 배포 작업을 수행 하는 방법을 설명합니다 .

>[!div class="step-by-step"]
[다음](the-contact-manager-solution.md)
