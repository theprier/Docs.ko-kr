---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
title: '엔터프라이즈 웹 배포: 시나리오 개요 | Microsoft Docs'
author: jrjlee
description: 이 자습서 집합 현실적인 수준의 복잡성을 가상의 엔터프라이즈 배포 시나리오와 함께 샘플 솔루션을를 사용 하 여 ref를 제공 하는 중...
ms.author: riande
ms.date: 05/03/2012
ms.assetid: aa862153-4cd8-4e33-beeb-abf502c6664f
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
msc.type: authoredcontent
ms.openlocfilehash: ec5b62f3991fa256bc8efe7abe9b953d61d1a515
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829380"
---
<a name="enterprise-web-deployment-scenario-overview"></a>엔터프라이즈 웹 배포: 시나리오 개요
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 자습서 집합 참조 구현을 제공 하 고 작업 및 연습 일반적인 컨텍스트를 제공 하기 현실적인 수준의 복잡성을 가상의 엔터프라이즈 배포 시나리오와 함께 샘플 솔루션을 사용 합니다. 이 항목에서는 자습서 시나리오를 설명 하 고 샘플 솔루션을 소개 합니다.


## <a name="scenario-description"></a>시나리오 설명

가상의 회사인 Fabrikam, Inc., 원격 영업 팀 저장 하 고 웹 인터페이스에서 연락처 정보를 검색할 수 있는 솔루션을 만드는 것입니다.

응용 프로그램 수명 주기 관리 (ALM) 프로세스에서 Fabrikam, Inc. 소프트웨어 개발 프로세스의 여러 단계에서 세 가지 서버 환경에 배포할 솔루션이 필요 합니다.

- 개발자 테스트 또는 "샌드박스" 환경입니다.
- 인트라넷 기반 준비 환경입니다.
- 인터넷 프로덕션 환경입니다.

이러한 각 환경에 다른 구성 및 보안 요구 사항 및 각 고유한 배포 문제를 제기 합니다.

### <a name="the-fabrikam-inc-server-infrastructure"></a>Fabrikam, inc. 서버 인프라

이 Fabrikam, Inc.의 고급 개발 및 배포 인프라

![](enterprise-web-deployment-scenario-overview/_static/image1.png)

개발자 워크스테이션, 원본 제어 인프라, 개발자 테스트 환경 및 Fabrikam.net 도메인 내의 인트라넷 네트워크에 있는 모든 스테이징 환경입니다. 프로덕션 환경 인트라넷 네트워크 방화벽으로 분리 되는 경계 네트워크 (라고도 DMZ, 완충 영역 및 스크린 된 서브넷)에 상주 합니다. 이 일반적인 배포 시나리오: 일반적으로 방화벽 또는 게이트웨이 서버를 사용 하 여 내부 서버 인프라에서 인터넷 연결 웹 서버를 격리 합니다.

이 예제에 대한 설명:

- 별도 빌드 서버를 사용 하 여 Team Foundation Server (TFS) 2010 서버 소스 제어 및 CI (지속적인 통합) 기능을 제공 합니다.
- 개발자 테스트 환경에는 인터넷 정보 서비스 (IIS) 7.5 웹 서버와 SQL Server 2008 R2 데이터베이스 서버를 포함합니다.
- 프로덕션 환경에 여러 IIS 7.5 웹 서버를 SQL Server 2008 R2 데이터베이스 서버와 함께 wff (웹 팜 프레임 워크) 컨트롤러 서버에서 동기화 합니다. 실제로 데이터베이스 서버가 클러스터링 또는 미러링을 확장성 및 가용성을 개선 하기 위해 사용할 수 있습니다.
- 스테이징 환경 프로덕션 환경의 구성을 최대한 근접 하 게 복제 하도록 설계 되었습니다.
- 방화벽 및 네트워크 격리 정책을 인트라넷 경계 네트워크 직접, 자동화 된 배포를 허용 하지 않습니다.

두 번째 자습서에서는 이러한 각각의이 환경 구성을 자세히 설명 [웹 배포용 서버 환경 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다.

### <a name="team-roles-for-alm"></a>ALM 용 팀 역할

이러한 사용자는 만들기, 관리, 빌드 및 게시 Contact Manager 솔루션에 관련 됩니다.

- Matt Hink는 Fabrikam, Inc.에서 웹 응용 프로그램 개발자 그는 Visual Studio 2010을 사용 하 여 Contact Manager 솔루션을 개발 팀의 일부입니다. Matt는을 사용 하 여 자신의 요구 사항을 충족 하도록 환경을 구성 하는 개발자 테스트 환경에 있는 서버의 모든 관리자 권한을 보유 합니다. Contact Manager 솔루션의 소스 코드는 그 저장 위치는 Visual Studio 2010 TFS 인스턴스에 대 한 사용자 액세스도를 있습니다.
- Rob Walters Fabrikam, Inc. 개발 팀에 대 한 서버 관리자를입니다. Rob 그 TFS 및 팀 빌드의 모든 측면을 구성할 수 있도록 TFS 서버에 관리자 액세스할 수 있습니다. 또한 Rob 테스트 및 스테이징 웹 서버에 대 한 관리 권한이 하 고 테스트 및 스테이징 환경에서 데이터베이스 서버에 대 한 데이터베이스 관리자 (DBA)으로 작동 합니다. Rob 이러한 작업을 수행 하려면 TFS 서버에 팀 빌드 구성에.

    - 빌드 및 사용자를 TFS에 파일을 체크 인할 때마다 응용 프로그램에서 단위 테스트를 실행 합니다. 이 CI 이라고 합니다.
    - 응용 프로그램 단위 테스트를 통과 되 면 테스트 환경에 연락처 관리자 응용 프로그램을 자동으로 배포 합니다. 여기에 초기 배포 후 초기 배포 및 데이터베이스에 대 한 업데이트에서 테스트 서버로 데이터베이스를 게시 합니다.
    - 단일 단계 프로세스에서 스테이징 환경에 연락처 관리자 응용 프로그램을 배포 합니다.
    - 웹 서버 관리자 및 dba가 프로덕션 환경에 응용 프로그램을 게시 하는 데 사용할 수 있는 웹 패키지를 만듭니다.
- Lisa Andrews Fabrikam, Inc. 프로덕션 서버에 응용 프로그램을 배포 하는 서버 관리자를입니다. 그녀는 TFS 팀 빌드 저장 위치는 웹 배포 패키지에 연락처 관리자 응용 프로그램이 빌드되면 공유에 대 한 읽기 권한이 있습니다. 또한가지고 프로덕션 웹 서버에 대 한 관리 액세스 그녀는 프로덕션 응용 프로그램을 배포할 수 있도록 합니다. 또한 그녀는 프로덕션 환경에서 데이터베이스 서버로 데이터베이스 및 데이터베이스 업데이트를 배포 하는 DBA 처럼 작동 합니다.

<a id="_The_Contact_Manager"></a>

### <a name="the-contact-manager-solution"></a>Contact Manager 솔루션

연락처 관리자 솔루션은 등록, 로그인 사용자 추가 및 웹 인터페이스를 통해 연락처 정보를 편집할 수 있도록 설계 되었습니다. Contact Manager 솔루션 4 개의 개별 프로젝트가 이루어져 있습니다.

![](enterprise-web-deployment-scenario-overview/_static/image2.png)

- **ContactManager.Mvc**. 솔루션에 대 한 진입점을 나타내는 ASP.NET MVC3 웹 응용 프로그램 프로젝트입니다. 생성 및 연락처 세부 정보를 확인 하는 기능을 사용 하 여 사용자를 제공 하는 등 몇 가지 기본 웹 응용 프로그램 기능을 제공 합니다. 응용 프로그램은 연락처 및 인증 및 권한 부여를 관리 하는 ASP.NET 응용 프로그램 서비스 데이터베이스를 관리 하는 Windows Communication Foundation (WCF) 서비스입니다.
- **ContactManager.Database**. Visual Studio 2010 데이터베이스 프로젝트입니다. 프로젝트는 저장소 연락처 세부 정보는 데이터베이스에 대 한 스키마를 정의 합니다.
- **ContactManager.Service**. WCF 웹 서비스 프로젝트입니다. 호출자가 수행 하도록 허용 하는 끝점을 만들려면 WCF 노출 검색, 업데이트 및 삭제 (CRUD) 작업 연락처 관리자 데이터베이스에 있습니다. Contact Manager 데이터베이스 및 ContactManager.Common.dll 어셈블리를 의존 하는 서비스입니다.
- **ContactManager.Common**. 클래스 라이브러리 프로젝트입니다. WCF 서비스는이 어셈블리에 정의 된 형식을 사용 합니다.

솔루션 및 해당 배포 요구 사항 등을 철저히 검토할이이 시리즈의 첫 번째 자습서에서 제공 됩니다 [기업에서 웹 배포](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)합니다.

<a id="_Deployment_Tasks"></a>

## <a name="deployment-tasks"></a>배포 작업

대규모 조직에서 다른 환경에 응용 프로그램 배포와 관련 된 몇 가지 고유한 작업 있습니다. 다음은 자습서에서 다루는 주요 작업입니다.

![](enterprise-web-deployment-scenario-overview/_static/image3.png)

이 문서의 앞부분에서 설명한 사용자의 관점에서 배포 프로세스의 각 단계 목록은 다음과 같습니다.

1. 팀의 모든 멤버는 키 배포 요구 사항 및 문제를 확인 하려면 Visual Studio 2010에서 Contact Manager 솔루션을 검토 합니다.
2. Matt Hink 개발자 테스트 환경에 배포 논리의 초기 테스트를 수행 하는 개발자 워크스테이션에서 직접 Contact Manager 솔루션을 배포할 수 있습니다.
3. Matt Hink TFS에서 소스 제어에 응용 프로그램을 추가합니다.
4. Rob Walters Team Build에서 Contact Manager 솔루션에 대 한 다양 한 빌드 정의 만듭니다. 새 코드에서는 사용자가 때마다 개발자 테스트 환경에 솔루션을 배포 하려면 CI를 사용 하는 하나의 빌드 정의 합니다. 다른 빌드 정의 사용 하면 필요에 따라 스테이징 환경에 대 한 사용자 트리거 배포가 있습니다.
5. 될 때마다 새 코드에서는 사용자가, 팀 빌드 자동으로 솔루션 구성 요소를 빌드합니다 단위 테스트를 실행 하며 빌드가 성공 하는 경우 개발자 테스트 환경에서 단위 테스트를 통과 하는 솔루션을 배포 합니다.
6. 사용자는 스테이징 환경에 배포를 트리거하는 경우 솔루션 패키지 이며 단일 단계 프로세스에서 배포 됩니다. 이 프로세스는 또한 프로덕션 환경에 수동 배포에 대 한 패키지를 생성합니다.
7. Lisa Andrews 수동으로 6 단계에서 만든 웹 패키지를 가져와 프로덕션 환경에 응용 프로그램을 배포 합니다.

### <a name="key-deployment-issues"></a>키 배포 문제

Contact Manager 솔루션 및 Fabrikam, Inc. 시나리오에는 다양 한 일반적인 문제 및 복잡 한 엔터프라이즈급 솔루션을 배포할 때 발생할 수 있는 문제 강조 표시 합니다. 예를 들어:

- 해야 있으려면 개발자와 같은 여러 환경에 프로젝트를 배포 또는 테스트 환경, 플랫폼 및 프로덕션 서버를 준비 합니다. 각 환경에 대 한 다른 구성 설정을 사용 하 여 배포 해야 하는 솔루션입니다.
- 단일 단계 또는 자동화 된 빌드 및 배포 프로세스의 일환으로 동시에 여러 종속 프로젝트를 배포 해야 합니다.
- 자동화 된 프로세스에서 드라이브 배포 수 있게 해야 합니다. 예를 들어, 새 코드를 체크 인할 때 스테이징 환경에 웹 응용 프로그램을 배포 하는 CI 프로세스를 사용 하려면.
- 모든 대상 환경에 필요한 자격 증명 또는 잘못 구성 설정이 않을 것으로 배포 프로세스를 제어 하 고 Visual Studio 외부에서 배포 변수를 설정 하는 일을 할 수 해야 합니다.
- 데이터베이스 스키마 기반 프로젝트를 배포 하 고 후속 배포에서 기존 데이터를 유지 해야 합니다.
- 사용자 계정 데이터를 배포 하지 않고 임시 단위로 멤버 자격 데이터베이스를 배포 해야 합니다. 기존 사용자 계정 데이터 손실 없이 배포 된 멤버 자격 데이터베이스의 스키마를 업데이트 해야 합니다.
- 다양 한 대상 환경에 콘텐츠를 배포할 때 특정 파일 또는 폴더를 제외 해야 합니다.

또한 자주 발생 하 고 증분 업데이트 되 면 배포 관리를 몇 가지 추가 과제가를 throw 합니다. 예를 들어:

- 새 코드에서는 개발자가 체크 인하면 때마다 단위 테스트를 실행 합니다. 코드 단위 테스트를 통과 하는 경우 솔루션을 배포 하려고 합니다.
- 사용자를 리디렉션하 하려는 스테이징 또는 프로덕션 환경에 웹 응용 프로그램을 배포 하는 경우는 *앱\_offline.htm* 배포 프로세스의 기간에 대 한 파일입니다.
- 배포 작업 기록 하려고 합니다. 배포 프로세스에는 지정 된 받는 사람에 게 성공 또는 실패 한 배포의 전자 메일 알림을 보내야 합니다.
- 자동화 된 배포가 실패할 경우 배포 프로세스를 현재 배포를 다시 시도 하거나 대신 이전 웹 패키지를 배포 해야 합니다.

> [!div class="step-by-step"]
> [이전](deploying-web-applications-in-enterprise-scenarios.md)
> [다음](application-lifecycle-management-from-development-to-production.md)
