---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
title: '응용 프로그램 수명 주기 관리: 프로덕션 개발에서 | Microsoft Docs'
author: jrjlee
description: 이 항목에서는 가상의 회사 par로 테스트, 스테이징 및 프로덕션 환경을 통해 ASP.NET 웹 응용 프로그램의 배포를 관리 하는 방법...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: f97a1145-6470-4bca-8f15-ccfb25fb903c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
msc.type: authoredcontent
ms.openlocfilehash: 8beeffb374df09c6695a1845199d30006ddcc1b7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="application-lifecycle-management-from-development-to-production"></a>응용 프로그램 수명 주기 관리: 프로덕션 개발에서
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 가상의 회사는 연속 개발 프로세스의 일부로 테스트, 스테이징 및 프로덕션 환경을 통해 ASP.NET 웹 응용 프로그램의 배포를 관리 하는 방법을 보여 줍니다. 항목을 통해 자세한 정보 및 특정 작업을 수행 하는 방법에 대 한 연습 링크가 제공 됩니다.
> 
> 이 항목에 대 한 높은 수준의 개요를 제공 하도록 설계는 [일련의 자습서](deploying-web-applications-in-enterprise-scenarios.md) 기업에서 웹 배포에 합니다. 여기에 설명 된 개념 중 일부에 대해 잘 알고 모르겠으면 걱정&#x2014;자습서를 수행 하는 모든 이러한 작업 및 기술에서 자세한 정보를 제공 합니다.
> 
> > [!NOTE]
> > 간단한 것에 대해 쉽도록이이 항목 배포 프로세스의 일부로 업데이트 데이터베이스를 설명 하지 않습니다. 그러나 데이터베이스 기능을 증분 업데이트를 하는 많은 엔터프라이즈 배포 시나리오의 요구 사항 및이 자습서 시리즈의 뒷부분에 나오는 이렇게 하는 방법에 지침을 찾을 수 있습니다. 자세한 내용은 참조 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)합니다.


## <a name="overview"></a>개요

여기에 설명 된 배포 프로세스에 설명 된 Fabrikam, Inc. 배포 시나리오에 따라은 [엔터프라이즈 웹 배포: 시나리오 개요](enterprise-web-deployment-scenario-overview.md)합니다. 이 항목을 검토 하기 전에 시나리오 개요를 읽어야 합니다. 시나리오 조직 비교적 복잡 한 웹 응용 프로그램의 배포를 관리 하는 방법을 검사, 기본적으로 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md), 일반적인 엔터프라이즈 환경에서 다양 한 단계가 수행 됩니다.

상위 수준 Contact Manager 솔루션 개발 및 배포 프로세스의 일부로 이러한 단계를 거칩니다.

1. 개발자는 Team Foundation Server (TFS) 2010에 일부 코드를 확인합니다.
2. TFS에서 코드를 작성 하 고 팀 프로젝트와 관련 된 모든 단위 테스트를 실행 합니다.
3. TFS는 테스트 환경에 솔루션을 배포합니다.
4. 개발자 팀 확인 하 고 테스트 환경에서 솔루션의 유효성을 검사 합니다.
5. 스테이징 환경 관리자가 배포 문제를 발생 되는지 여부를 설정 하려면 스테이징 환경에 "경우 어떻게" 배포를 수행 합니다.
6. 스테이징 환경 관리자는 스테이징 환경에 라이브 배포를 수행합니다.
7. 솔루션 스테이징 환경에서 테스트 사용자 수용을 거칩니다.
8. 웹 배포 패키지를 프로덕션 환경에 수동으로 가져올 않습니다.

이러한 단계는 연속 개발 주기의 일부를 구성 합니다.

![](application-lifecycle-management-from-development-to-production/_static/image1.png)

실제로, 프로세스는이 영역 보다 약간 더 복잡 한 각 단계를 자세히 살펴볼 때 확인할 수 있습니다. Fabrikam, Inc. 각 대상 환경에 배포 하는 다른 방법을 사용합니다.

![](application-lifecycle-management-from-development-to-production/_static/image2.png)

이 항목의 나머지 부분을이 배포 수명 주기의 주요 단계 이러한 검사:

- **필수 구성 요소**: 현재 위치에 배포 논리를 삽입 하기 전에 서버 인프라를 구성 해야 합니다.
- **초기 개발 및 배포**: 처음으로 솔루션을 배포 하기 전에 작업을 수행 해야 합니다.
- **배포 테스트를**: 패키지 및 콘텐츠 배포를 테스트 환경에 자동으로 새 코드에서는 개발자가 체크 하는 방법입니다.
- **스테이징 배포**: 특정 배포 하는 방법에 빌드를 스테이징 환경 및 "경우 어떻게" 수행 하는 방법을 배포 하려면 배포 문제를 발생 하지 않습니다.
- **프로덕션에 배포**: 네트워크 인프라에는 원격 배포 하지 못하게 하는 경우 프로덕션 환경에 웹 패키지를 가져오는 방법입니다.

## <a name="prerequisites"></a>전제 조건

모든 배포 시나리오에서 첫 번째 태스크 서버 인프라 배포 도구 및 기술의 요구 사항을 충족 하는지 확인 하는 것입니다. 이 경우 Fabrikam, Inc.가 다음과 같이 서버 인프라 구성:

- TFS 팀 프로젝트 컬렉션을 포함, 컨트롤러, 빌드 및 빌드 에이전트 하도록 구성 됩니다. 참조 [자동화 된 웹 배포를 위해 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) 자세한 정보에 대 한 합니다.
- 테스트 환경에 설명 된 대로 웹 배포 에이전트 서비스 ("원격 에이전트")를 사용 하 여 원격 배포를 허용 하도록 구성 된 [시나리오: 웹 배포를 위해 테스트 환경 구성](../configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment.md) 및 [ 웹 배포 게시 (원격 에이전트)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)합니다.
- 스테이징 환경에 설명 된 대로 웹 배포 처리기 끝점을 사용 하는 원격 배포를 허용 하도록 구성 된 [시나리오: 웹 배포를 위해 스테이징 환경 구성](../configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment.md) 및 [웹 서버 구성 웹 배포 게시 (웹 처리기를 배포 하는 데 사용)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)합니다.
- 프로덕션 환경에 설명 된 대로 관리자에 인터넷 정보 서비스 (IIS), 웹 배포 패키지를 수동으로 가져올 수를 허용 하도록 구성 된 [시나리오:웹배포를위해프로덕션환경구성](../configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment.md) 및 [웹 배포 게시 (오프 라인 배포의 경우)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)합니다.

## <a name="initial-development-and-deployment"></a>초기 개발 및 배포

Fabrikam, Inc. 개발 팀은 처음으로 Contact Manager 솔루션을 배포 하려면, 이러한 작업을 수행 해야 합니다.

- TFS에서 새 팀 프로젝트를 만듭니다.
- 배포 논리를 포함 하는 Microsoft Build Engine (MSBuild) 프로젝트 파일을 만듭니다.
- 배포 프로세스를 트리거하는 TFS 빌드 정의 만듭니다.

### <a name="create-a-new-team-project"></a>새 팀 프로젝트 만들기

- Rob 받는 TFS 관리자에 설명 된 대로 응용 프로그램에 대 한 새 팀 프로젝트를 만듭니다 [TFS에서 팀 프로젝트를 만드는](../configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs.md)합니다. 다음으로, Matt Hink 수석 개발자는 기본 솔루션을 만듭니다. 에 설명 된 대로 그의 파일을 TFS, 새 팀 프로젝트에 체크 [소스 제어에 콘텐츠 추가](../configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control.md)합니다.

### <a name="create-the-deployment-logic"></a>배포 논리를 만들기

Matt Hink 분할 프로젝트 파일 접근 방식에 설명 된를 사용 하 여 다양 한 사용자 지정 MSBuild 프로젝트 파일을 만들고 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다. Matt 만듭니다.

- 명명 된 프로젝트 파일 *Publish.proj* 배포 프로세스를 실행 하는 합니다. 이 파일에는 솔루션의 프로젝트 빌드하고 웹 패키지를 만드는 패키지는 대상 서버 환경에 배포 하는 MSBuild 대상을 포함 합니다.
- 환경 관련 프로젝트 파일 이름이 *Env Dev.proj* 및 *Env Stage.proj*합니다. 여기에 연결 문자열, 서비스 끝점 및 웹 패키지를 받을 원격 서비스의 세부 정보 같은 각각 테스트 환경과 스테이징 환경에 관련 된 설정을 포함 합니다. 특정 대상 환경에 대 한 올바른 설정을 선택에 대 한 지침을 참조 하십시오. [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)합니다.

배포를 실행 하려면 사용자는 다음과 같이 실행 됩니다.는 *Publish.proj* MSBuild 또는 팀 빌드를 사용 하 여 파일 및 관련 환경별 프로젝트 파일의 위치를 지정 합니다 (*Env Dev.proj* 또는 *Env Stage.proj*) 명령줄 인수입니다. *Publish.proj* 파일은 다음 각 대상 환경에 대 한 지침을 게시의 전체 집합을 만들 환경 관련 프로젝트 파일을 가져옵니다.

> [!NOTE]
> 이러한 사용자 지정 프로젝트 파일의 작업 방식은 독립적 MSBuild를 호출을 사용 하는 메커니즘입니다. 예를 들어 직접 사용할 수는 MSBuild 명령줄을에 설명 된 대로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다. 에 설명 된 대로 명령 파일에서 프로젝트 파일을 실행할 수 있습니다 [만들기 및 배포 명령 파일을 실행](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)합니다. 또는에서 실행할 수 있습니다 프로젝트 파일을 TFS, 빌드 정의에 설명 된 대로 [해당 지원 배포 빌드 정의 만들려면](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)합니다.  
> 각각의 경우 최종 결과 동일&#x2014;MSBuild 병합 된 프로젝트 파일을 실행 하 고 대상 환경에 솔루션을 배포 합니다. 이렇게 하면 많은 프로그램 게시 프로세스를 시작 하는 방법을 유연 하 게 됩니다.


사용자 지정 프로젝트 파일을 만든가 그 후 Matt 솔루션 폴더에 추가 하 고 소스 제어로 체크 합니다.

### <a name="create-build-definitions"></a>빌드 정의 만들기

최종 준비 작업으로 Matt와 Rob 협력 새 팀 프로젝트에 대 한 세 개의 빌드 정의를 만들려면:

- **DeployToTest**합니다. Contact Manager 솔루션 빌드하고 체크 인 발생할 때마다 테스트 환경에 배포 합니다.
- **DeployToStaging**합니다. 개발자 빌드 큐 대기 하는 경우에 지정 된 이전 빌드에서 리소스를 스테이징 환경에 배포 합니다.
- **DeployToStaging-whatif를 지원함**합니다. 이 개발자는 빌드 큐 대기 하는 경우 스테이징 환경에 "경우 어떻게" 배포를 수행 합니다.

다음 섹션에서는 이러한 각 항목에 대해 보다 자세히 빌드 정의 합니다.

## <a name="deployment-to-test"></a>테스트에는 배포

Fabrikam, Inc.의 개발 팀에는 다양 한 소프트웨어 테스트 인증 및 유효성 검사, 및와 같은 유용성 테스트, 호환성 테스트, 임시 또는 예비 테스트의 작업을 수행 하 고 테스트 환경을 유지 관리 합니다.

개발 팀에서 명명 된 TFS에 빌드 정의 만든 **DeployToTest**합니다. 이 빌드 정의 될 때마다 Fabrikam, Inc. 개발 팀의 구성원에 체크 인 수행을 실행 하는 빌드 프로세스를 의미 하는 연속 통합 트리거를 사용 합니다. 빌드 트리거될 때 빌드 정의 됩니다.

- ContactManager.sln 솔루션을 빌드하십시오. 이 솔루션 내에서 모든 프로젝트를 다시 작성합니다.
- (솔루션을 성공적으로 빌드하기) 하는 경우 솔루션 폴더 구조에서 모든 단위 테스트를 실행 합니다.
- (솔루션이 성공적으로 빌드되고 모든 단위 테스트를 통과) 경우 배포 프로세스를 제어 하는 사용자 지정 프로젝트 파일을 실행 합니다.

최종 결과 솔루션 빌드되면 하 단위 테스트를 통과 하는 경우 웹 패키지 및 기타 배포 리소스 테스트 환경에 배포 됩니다.

![](application-lifecycle-management-from-development-to-production/_static/image3.png)

### <a name="how-does-the-deployment-process-work"></a>배포 프로세스는 어떻게 작동 합니까?

**DeployToTest** 빌드 정의 제공 MSBuild에 이러한 인수:


[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample1.cmd)]


**DeployOnBuild = true** 및 **DeployTarget 패키지 =** 속성 팀 빌드 솔루션 내의 프로젝트를 빌드할 때 사용 됩니다. 웹 응용 프로그램 프로젝트를 프로젝트의 경우 MSBuild는 프로젝트에 대 한 웹 배포 패키지를 만들려면 이러한 속성에 지시 합니다. **TargetEnvPropsFile** 속성이 있으면는 *Publish.proj* 가져올 환경 관련 프로젝트 파일을 찾을 수 있는 위치를 파일입니다.

> [!NOTE]
> 다음과 같이 빌드 정의 만드는 방법에 자세한 연습을 참조 하십시오. [해당 지원 배포 빌드 정의 만들려면](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)합니다.


*Publish.proj* 솔루션의 각 프로젝트 빌드 대상 파일에 포함 되어 있습니다. 그러나 조건부 논리를 건너뛰고 다음의 빌드 대상 팀 빌드에서 파일을 실행 하는 경우도 있습니다. 이 제공 하는 팀 빌드, 단위 테스트를 실행 하는 기능과 같은 추가 빌드 기능을 사용할 수 있습니다. 솔루션 빌드 또는 단위 테스트 실패 하는 경우는 *Publish.proj* 파일 실행 되지 것입니다 및 응용 프로그램이 배포 되지 것입니다.

조건부 논리를 평가 하 여 수행 됩니다는 **BuildingInTeamBuild** 속성입니다. 이 속성은으로 자동으로 설정 된 MSBuild 속성 **true** 때 사용 하 여 팀 빌드 프로젝트입니다.

## <a name="deployment-to-staging"></a>스테이징 배포

빌드를 테스트 환경에서 개발자 팀의 요구 사항을 모두 충족, 팀을 스테이징 환경에 동일한 빌드를 배포 해야 할 수 있습니다. 스테이징 환경은 프로덕션 또는 "라이브" 환경에 밀접 하 게 최대한, 예를 들어 서버 사양, 운영 체제 및 소프트웨어 및 네트워크 구성의 관점에서 특성과 일치 하도록 일반적으로 구성 됩니다. 스테이징 환경은 부하 테스트, 사용자 수용 테스트 및 광범위 한 내부 검토 자주 사용 됩니다. 빌드는 빌드 서버에서 직접 스테이징 환경에 배포 됩니다.

![](application-lifecycle-management-from-development-to-production/_static/image4.png)

스테이징 환경에 솔루션을 배포 하는 데 사용 하는 빌드 정의 **DeployToStaging-whatif를 지원함** 및 **DeployToStaging**, 이러한 특성을 공유 합니다.

- 실제로 아무 것도 생성 하지 있습니다. Rob를 배포 하면 솔루션 스테이징 환경에 이미 확인 및 테스트 환경에서 유효성이 검사 된 특정, 기존 빌드를 배포 하려고 합니다. 빌드 정의 방금 배포 프로세스를 제어 하는 사용자 지정 프로젝트 파일을 실행 해야 합니다.
- Rob 빌드를 트리거하는 경우 그 사용 하 여 빌드 매개 변수 지정는 빌드 빌드 서버에서 배포 하 고 싶기 리소스가 포함 되어 있습니다.
- 빌드 정의 자동으로 트리거되지 않습니다. Rob 수동으로 솔루션 스테이징 환경에 배포 하려고 하는 경우 빌드를 큐 대기 시킵니다.

다음은 스테이징 환경에 배포 하기 위한 고급 프로세스입니다.

1. 스테이징 환경 관리자 Rob 받는 사용 하 여 빌드 큐 대기는 **DeployToStaging-whatif를 지원함** 빌드 정의 합니다. Rob 빌드 정의 매개 변수를 사용 하 여 배포 하고자 하는 빌드를 지정 합니다.
2. **DeployToStaging-whatif를 지원함** 빌드 정의 실행 "경우 어떻게" 모드에서 사용자 지정 프로젝트 파일입니다. 이 Rob 라이브 배포 수행 되 고 있던 있지만 대상 환경에 실제로 변경을 수행 하지 않는 것 로그 파일을 생성 합니다.
3. Rob 스테이징 환경에서 배포의 효과 확인 하려면 로그 파일을 검토 합니다. 특히, Rob 추가할 수 있는, 내용을 업데이트할지 및 삭제는 항목을 확인 하려고 합니다.
4. Rob 경우 사용 하 여 빌드 큐가 충족 하는 배포 하지 않습니다 바람직하지 않은 설정을 변경 하려면 기존 리소스 또는 데이터는 **DeployToStaging** 빌드 정의 합니다.
5. **DeployToStaging** 빌드 정의 실행 사용자 지정 프로젝트 파일입니다. 이러한 배포 리소스 스테이징 환경에서 주 웹 서버에 게시 합니다.
6. Wff (웹 팜 프레임 워크) 컨트롤러는 스테이징 환경에서 웹 서버를 동기화합니다. 이렇게 하면 서버 팜의 모든 웹 서버에서 사용할 수 있는 응용 프로그램.

### <a name="how-does-the-deployment-process-work"></a>배포 프로세스는 어떻게 작동 합니까?

**DeployToStaging** 빌드 정의 제공 MSBuild에 이러한 인수:


[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample2.cmd)]


**TargetEnvPropsFile** 속성이 있으면는 *Publish.proj* 가져올 환경 관련 프로젝트 파일을 찾을 수 있는 위치를 파일입니다. **OutputRoot** 속성 기본 제공 값을 재정의 하 고 배포할 리소스를 포함 하는 빌드 폴더의 위치를 나타냅니다. 사용 하 여 Rob 큐 빌드를 사용할 때의 **매개 변수** 탭에 대 한 업데이트 된 값을 제공 하는 **OutputRoot** 속성입니다.

![](application-lifecycle-management-from-development-to-production/_static/image5.png)

> [!NOTE]
> 다음과 같이 빌드 정의 만드는 방법에 대 한 자세한 내용은 참조 하십시오. [는 특정 빌드 배포](../configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build.md)합니다.


**DeployToStaging-whatif를 지원함** 와 같은 배포 논리를 포함 하는 빌드 정의 **DeployToStaging** 빌드 정의 합니다. 하지만 추가 인수를 포함 **WhatIf = true**:


[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample3.cmd)]


내에서 *Publish.proj* 파일인은 **WhatIf** 속성 나타냅니다 "경우 어떻게" 모드에서 배포의 모든 리소스를 게시 되어야 합니다. 즉, 배포, 미리 gone에 있지만 대상 환경에서 실제로 변경 아무 것도 로그 파일이 생성 됩니다. 이렇게 하면 제안 된 배포의 영향을 평가&#x2014;특히 추가 get 기능, 어떤 업데이트 됩니다, 및 어떤 삭제 됩니다&#x2014;실제로 변경 하기 전에 합니다.

> [!NOTE]
> "경우 어떻게" 배포를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. ["경우 어떻게" 배포](../advanced-enterprise-web-deployment/performing-a-what-if-deployment.md)합니다.


응용 프로그램을 스테이징 환경에서 주 웹 서버를 배포 하 고 나면는 WFF 서버 팜의 모든 서버 응용 프로그램을 자동으로 동기화 합니다.

> [!NOTE]
> 웹 서버를 동기화 할 WFF를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [웹 팜 프레임 워크와 서버 팜 만들기](../configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework.md)합니다.


## <a name="deployment-to-production"></a>프로덕션에 배포

스테이징 환경에서 빌드를 승인 되 면 Fabrikam, Inc. 팀 프로덕션 환경에 응용 프로그램을 게시할 수 있습니다. 프로덕션 환경은 위치는 응용 프로그램 "가동" 되기을 최종 사용자가 해당 대상에 도달 하면입니다.

프로덕션 환경은 인터넷 경계 네트워크에입니다. 이 빌드 서버를 포함 하는 내부 네트워크에서 격리 됩니다. 수동으로 프로덕션 환경 관리자 리사 Andrews 빌드 서버에서 웹 배포 패키지를 복사 하 고 기본 프로덕션 웹 서버에서 IIS로 가져올 해야 합니다.

![](application-lifecycle-management-from-development-to-production/_static/image6.png)

다음은 프로덕션 환경에 배포 하기 위한 고급 프로세스입니다.

1. 개발자 팀 빌드를 프로덕션 환경에 배포할 준비가 되었는지 리사 권고 합니다. 팀 빌드 서버에서 드롭 폴더 내에서 웹 배포 패키지의 위치는 리사 권고합니다.
2. 리사 빌드 서버에서 웹 패키지를 수집 하 고 프로덕션 환경에서 주 웹 서버에 복사 합니다.
3. IIS 관리자를 사용 하 여 가져온 주 웹 서버에 웹 패키지를 게시 하는 리사 합니다.
4. WFF 컨트롤러 프로덕션 환경에서 웹 서버를 동기화합니다. 이렇게 하면 서버 팜의 모든 웹 서버에서 사용할 수 있는 응용 프로그램.

### <a name="how-does-the-deployment-process-work"></a>배포 프로세스는 어떻게 작동 합니까?

IIS 관리자에서 IIS 웹 사이트에 웹 패키지를 게시할 수 용이 하 게 하는 가져오기 응용 프로그램 패키지 마법사를 포함 합니다. 이 절차를 수행 하는 방법은 연습을 참조 하십시오. [수동으로 웹 패키지 설치](../web-deployment-in-the-enterprise/manually-installing-web-packages.md)합니다.

## <a name="conclusion"></a>결론

이 항목 제공 일반적인 엔터프라이즈급 웹 응용 프로그램에 대 한 배포 수명 주기를 보여 줍니다.

이 항목의 웹 응용 프로그램 배포의 다양 한 측면에 지침을 제공 하는 자습서 시리즈의 일부를 형성 합니다. 실제로 배포 프로세스의 각 단계에는 많은 추가 작업 및 고려 사항 및 모두 단일 연습에서에서 설명 불가능 합니다. 자세한 내용은이 자습서를 참조 하십시오.

- [웹 배포는 기업에서](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)합니다. 이 자습서에는 MSBuild 및 IIS 웹 배포 도구 (웹 배포)를 사용 하 여 웹 배포 기술에 대 한 포괄적인 소개를 제공 합니다.
- [웹 배포를 위한 서버 환경을 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다. 이 자습서는 다양 한 배포 시나리오를 지원 하기 위해 Windows 서버 환경을 구성 하는 방법에 지침을 제공 합니다.
- [웹 배포를 자동화 된 구성에 대 한 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다. 이 자습서 배포 논리를 TFS 빌드 프로세스에 통합 하는 방법에 지침을 제공 합니다.
- [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)합니다. 이 자습서를 제공 지침 보다 복잡 한 배포 문제 중 일부를 만족 하는 방법에 조직 얼굴 합니다.

> [!div class="step-by-step"]
> [이전](enterprise-web-deployment-scenario-overview.md)
