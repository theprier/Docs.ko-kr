---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
title: "엔터프라이즈 웹 배포: 시나리오 개요 | Microsoft Docs"
author: jrjlee
description: "이 집합의 자습서를 사용 하 여 샘플 솔루션 현실적인 수준의 복잡성 가상의 엔터프라이즈 배포 시나리오와 함께 ref 제공..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/03/2012
ms.topic: article
ms.assetid: aa862153-4cd8-4e33-beeb-abf502c6664f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
msc.type: authoredcontent
ms.openlocfilehash: f90db22bf98456661c530e728e854ce109aec6fd
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="enterprise-web-deployment-scenario-overview"></a>엔터프라이즈 웹 배포: 시나리오 개요
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 자습서의이 집합 참조 구현을 제공 하 고 작업 및 연습 일반적인 컨텍스트를 제공 하는 가상의 엔터프라이즈 배포 시나리오와 함께 복잡성 현실적인 수준으로 샘플 솔루션을 사용 합니다. 이 항목 자습서 시나리오를 설명 하 고 샘플 솔루션을 소개 합니다.


## <a name="scenario-description"></a>시나리오 설명

Fabrikam, Inc., 회사인 원격 영업 팀 저장 하 고 웹 인터페이스에서 연락처 정보를 검색할 수 있는 솔루션을 만드는 것입니다.

관리 ALM (Application Lifecycle) 프로세스에서 Fabrikam, Inc. 소프트웨어 개발 프로세스의 여러 단계에서 3 개의 서버 환경에 배포할 솔루션이 필요 합니다.

- 개발자의 테스트 또는 "샌드박스" 환경입니다.
- 인트라넷 기반 스테이징 환경입니다.
- 인터넷 연결 프로덕션 환경입니다.

이러한 각각의이 환경에 서로 다른 구성 및 보안 요구 사항 및 각 되지만 고유한 배포 문제가 발생 합니다.

### <a name="the-fabrikam-inc-server-infrastructure"></a>Fabrikam, inc. 서버 인프라

이 Fabrikam, inc.의 고급 개발 및 배포 인프라

![](enterprise-web-deployment-scenario-overview/_static/image1.png)

개발자 워크스테이션, 소스 제어 인프라, 개발자 테스트 환경 및 스테이징 환경 모두 Fabrikam.net 도메인 내의 인트라넷 네트워크에 상주 합니다. 프로덕션 환경에서 방화벽으로 인트라넷 네트워크 격리 된 경계 네트워크 (라고도 DMZ, 완충 지역 및 스크린 된 서브넷)에 상주 합니다. 이것은 일반적인 배포 시나리오: 일반적으로 방화벽 또는 게이트웨이 서버를 사용 하 여 내부 서버 인프라에서 인터넷 연결 웹 서버를 격리 합니다.

이 예제에 대한 설명:

- 별도 빌드 서버를 사용 하 여 Team Foundation Server (TFS) 2010 서버는 소스 제어 및 CI (연속 통합) 기능을 제공 합니다.
- 인터넷 정보 서비스 (IIS) 7.5 웹 서버와 SQL Server 2008 R2 데이터베이스 서버 개발자 테스트 환경에 포함 되어 있습니다.
- 프로덕션 환경에 SQL Server 2008 R2 데이터베이스 서버와 함께 wff (웹 팜 프레임 워크) 컨트롤러 서버에 의해 동기화 된 여러 IIS 7.5 웹 서버에 포함 됩니다. 실제로, 데이터베이스 서버가 클러스터링 또는 미러링을 확장성 및 가용성을 개선 하기 위해 사용할 수 있습니다.
- 스테이징 환경은 프로덕션 환경의 구성을 최대한 비슷하게 복제 하도록 설계 되었습니다.
- 방화벽 및 네트워크 격리 정책을 인트라넷 경계 네트워크 직접적으로 자동화 된 배포를 허용 하지 않습니다.

이러한 환경 중 각 구성 두 번째 자습서에서 자세히 설명 [웹 배포에 대 한 서버 환경을 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다.

### <a name="team-roles-for-alm"></a>ALM에 대 한 팀 역할

이러한 사용자 만들기, 관리, 빌드 및 게시 않아 솔루션에 관련 된:

- Matt Hink는 Fabrikam, inc.에서 웹 응용 프로그램 개발자 그는 Visual Studio 2010을 사용 하 여 Contact Manager 솔루션을 개발 하는 팀의 일부입니다. Matt에을 사용 하 여 자신의 요구에 맞게 환경을 구성 하는 개발자 테스트 환경에 있는 서버에 대 한 전체 관리자 권한이 있습니다. 그 사용자 인스턴스에 대 한 액세스는 Visual Studio 2010 TFS 그 않아 솔루션에 대 한 소스 코드는 저장 위치에 있습니다.
- Rob 받는 Fabrikam, Inc. 개발 팀에 대 한 서버 관리자입니다. Rob에 대 한 관리 액세스는 TFS 서버에서 있으므로 TFS 및 팀 빌드에서의 모든 측면을 구성할 수 있습니다. 또한 Rob 테스트 및 스테이징 웹 서버에 관리 액세스 권한을 보유 하 고 테스트와 스테이징 환경에 데이터베이스 서버에 대 한 역할을 데이터베이스 관리자 (DBA) 합니다. Rob 이러한 작업을 수행 하는 TFS 서버에서 팀 빌드 구성 했습니다.

    - 빌드 및 TFS에 파일에 사용자 체크 때마다 응용 프로그램에서 단위 테스트를 실행 합니다. 이 CI 이라고 합니다.
    - 응용 프로그램 단위 테스트를 통과 되 면 테스트 환경에 않아 응용 프로그램을 자동으로 배포 합니다. 여기에 초기 배포 및 데이터베이스에 대 한 업데이트에 테스트 서버에 초기 배포 이후에 데이터베이스를 게시 합니다.
    - 단일 단계 프로세스에서 스테이징 환경에 않아 응용 프로그램을 배포 합니다.
    - 웹 서버 관리자와 DBA가 프로덕션 환경에 응용 프로그램을 게시 하는 데 사용할 수 있는 웹 패키지를 만듭니다.
- 리사 Andrews Fabrikam, inc. 프로덕션 서버에 응용 프로그램 배포를 담당 하는 서버 관리자입니다. 그녀는 TFS 팀 빌드 저장 위치 웹 배포 패키지 않아 응용 프로그램을 작성 한 후 공유에 대 한 읽기 권한이 있습니다. 그녀는 또한 그녀 프로덕션 환경에 응용 프로그램을 배포할 수 있도록 프로덕션 웹 서버에 대 한 관리 액세스를에 있습니다. 또한 영업 관리자 역할을 프로덕션 환경에서 데이터베이스 서버에 데이터베이스 및 데이터베이스 업데이트를 배포 하는 DBA 합니다.

<a id="_The_Contact_Manager"></a>

### <a name="the-contact-manager-solution"></a>Contact Manager 솔루션

관리자에 게 문의 솔루션은 등록, 로그인 사용자가 추가 하 고 웹 인터페이스를 통해 연락처 정보를 편집할 수 있도록 설계 되었습니다. Contact Manager 솔루션 4 개의 개별 프로젝트가 이루어져 있습니다.

![](enterprise-web-deployment-scenario-overview/_static/image2.png)

- **ContactManager.Mvc**합니다. 이 ASP.NET MVC3 웹 응용 프로그램 프로젝트를 솔루션에 대 한 진입점을 나타냅니다. 만들고 연락처 세부 정보를 볼 수 있는 사용자가 제공 하는 등 몇 가지 기본 웹 응용 프로그램 기능을 제공 합니다. 응용 프로그램 연락처와 인증 및 권한 부여를 관리 하는 ASP.NET 응용 프로그램 서비스 데이터베이스를 관리 하려면 Windows Communication Foundation (WCF) 서비스를 사용 합니다.
- **ContactManager.Database**합니다. 이것이 Visual Studio 2010 데이터베이스 프로젝트입니다. 프로젝트는 저장소 연락처 세부 정보는 데이터베이스에 대 한 스키마를 정의 합니다.
- **ContactManager.Service**합니다. 이 WCF 웹 서비스 프로젝트입니다. 수행 하는 호출자를 허용 하는 끝점을 만들려면 WCF 노출 검색, 업데이트 및 삭제 (CRUD) 작업 Contact Manager 데이터베이스에 있습니다. 서비스는 연락처 Manager 데이터베이스 및 ContactManager.Common.dll 어셈블리에 의존합니다.
- **ContactManager.Common**합니다. 이 클래스 라이브러리 프로젝트입니다. WCF 서비스는이 어셈블리에 정의 된 형식을 사용 합니다.

솔루션 및 해당 배포 요구 사항을 면밀히 검토 한이 시리즈의 첫 번째 자습서에서 제공 됩니다 [기업에서 웹 배포](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)합니다.

<a id="_Deployment_Tasks"></a>

## <a name="deployment-tasks"></a>배포 작업

대규모 조직에서 다른 환경에 응용 프로그램 배포에 관련 된 몇 가지 고유한 작업 있습니다. 다음은 자습서를 포괄 하는 주요 작업입니다.

![](enterprise-web-deployment-scenario-overview/_static/image3.png)

이 문서의 앞부분에 설명 된 사용자의 관점에서 배포 프로세스의 각 단계 목록은 다음과 같습니다.

1. 팀의 모든 멤버는 주요 배포 요구 사항 및 문제를 확인 하려면 Visual Studio 2010에서 않아 솔루션을 검토 합니다.
2. Matt Hink 개발자 테스트 환경에 배포 논리의 초기 테스트를 수행 하 고 개발자 워크스테이션에서 직접 않아 솔루션을 배포할 수 있습니다.
3. Matt Hink TFS에서 소스 제어에 응용 프로그램을 추가합니다.
4. Rob 받는 팀 빌드에서 않아 솔루션에 대 한 다양 한 빌드 정의 만듭니다. 새 코드에 사용자 체크 때마다 개발자 테스트 환경에 솔루션을 배포 하려면 CI를 사용 하는 한 빌드 정의 합니다. 또 다른 빌드 정의 사용 하면 필요에 따라 스테이징 환경에 대 한 사용자가 트리거 배포가 있습니다.
5. 될 때마다 새 코드에서는 사용자가 체크 팀 빌드 자동으로 솔루션 구성 요소, 단위 테스트 실행 도중 빌드되고 배포 솔루션 빌드에 성공 하면 개발자 테스트 환경 및 단위 테스트 통과 됩니다.
6. 사용자는 스테이징 환경에 배포를 트리거하는 경우 솔루션 패키지를 업데이트 하 고 프로세스는 단일 단계에서 배포 된 됩니다. 이 프로세스는 또한 수동 배포를 프로덕션 환경에 대 한 패키지를 생성합니다.
7. 리사 Andrews 6 단계에서 만든 웹 패키지를 수동으로 가져오는 하 여 프로덕션 환경에 응용 프로그램을 배포 합니다.

### <a name="key-deployment-issues"></a>주요 배포 문제

Contact Manager 솔루션 및 Fabrikam, Inc. 시나리오에는 다양 한 일반적인 문제 및 문제 복잡 하거나 엔터프라이즈 규모 솔루션을 배포할 때 발생할 수 있는 강조 표시 합니다. 예:

- 해야 개발자와 같은 여러 환경에 프로젝트를 배포 하거나 테스트 환경에서는 수 플랫폼 및 프로덕션 서버를 준비 합니다. 솔루션은 각 환경에 대해 서로 다른 구성 설정을 사용 하 여 배포 해야 합니다.
- 단일 단계 또는 자동화 된 빌드 및 배포 프로세스의 일환으로 동시에 여러 종속 프로젝트를 배포 해야 합니다.
- 자동화 된 프로세스에서 드라이브 배포를 실행할 수 있도록 해야 합니다. 예를 들어 CI 프로세스를 사용 하 여 새 코드를 체크 인할 때 웹 응용 프로그램을 스테이징 환경에 배포 하려면.
- 올바른 구성 설정 또는 모든 대상 환경에 대 한 필요한 자격 증명을 않을 것 처럼 하 배포 프로세스를 제어 하 고 Visual Studio 외부에서 배포 변수를 설정 해야 합니다.
- 데이터베이스 스키마 기반 프로젝트를 배포 하 고 후속 배포에서 기존 데이터를 유지 해야 합니다.
- 사용자 계정 데이터를 배포 하지 않고 멤버 자격 데이터베이스 임시로에 배포 해야 합니다. 또한 기존 사용자 계정 데이터 손실 없이 배포 된 멤버 자격 데이터베이스의 스키마를 업데이트 해야 할 수 있습니다.
- 다양 한 대상 환경에 콘텐츠를 배포할 때 특정 파일 또는 폴더를 제외 해야 합니다.

또한 일반적이 고 증분 업데이트 되 면 배포를 관리 하는 몇 가지 추가 과제를 throw 합니다. 예:

- 개발자는 새 코드에 체크 인하 때마다 단위 테스트를 실행 합니다. 코드 단위 테스트를 통과 하는 경우 솔루션을 배포 하려고 합니다.
- 사용자가을 리디렉션하려고 할 스테이징 또는 프로덕션 환경에 웹 응용 프로그램을 배포 하는 경우는 *앱\_offline.htm* 배포 프로세스 중에 파일입니다.
- 배포 작업을 기록 하려면. 지정 된 받는 사람에 게 배포 프로세스에 성공 또는 실패 한 배포의 전자 메일 알림을 보내야 합니다.
- 자동화 된 배포에 실패 하는 경우 배포 프로세스는 현재 배포를 다시 시도 하거나 대신 이전 웹 패키지를 배포 해야 합니다.

>[!div class="step-by-step"]
[이전](deploying-web-applications-in-enterprise-scenarios.md)
[다음](application-lifecycle-management-from-development-to-production.md)
