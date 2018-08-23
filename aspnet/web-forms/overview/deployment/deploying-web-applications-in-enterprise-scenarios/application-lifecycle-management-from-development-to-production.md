---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
title: '응용 프로그램 수명 주기 관리: 개발부터 프로덕션까지 | Microsoft Docs'
author: jrjlee
description: 이 항목에서는 가상의 회사 par로 테스트, 스테이징 및 프로덕션 환경을 통해 ASP.NET 웹 응용 프로그램의 배포를 관리 하는 방법을 보여 줍니다...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f97a1145-6470-4bca-8f15-ccfb25fb903c
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
msc.type: authoredcontent
ms.openlocfilehash: 7cb9c949936c3af73d4c904d401c36d4d83f3e18
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836687"
---
<a name="application-lifecycle-management-from-development-to-production"></a>응용 프로그램 수명 주기 관리: 개발부터 프로덕션까지
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 가상의 회사는 연속 개발 프로세스의 일부로 테스트, 스테이징 및 프로덕션 환경을 통해 ASP.NET 웹 응용 프로그램의 배포를 관리 하는 방법을 보여 줍니다. 항목 전체에서 추가 정보 및 특정 작업을 수행 하는 방법에 대 한 연습에는 링크가 제공 됩니다.
> 
> 항목에 대 한 대략적인 개요를 제공 하도록 설계 되었습니다를 [시리즈의 자습서](deploying-web-applications-in-enterprise-scenarios.md) 기업에서 웹 배포 합니다. 여기에 설명 된 개념 중 일부를 잘 모르는 경우 걱정 하지 마세요&#x2014;다음에 나오는 자습서에서 이러한 작업 및 기술 모두 자세한 정보를 제공 합니다.
> 
> > [!NOTE]
> > 단순성 만들기 쉽도록이 항목이에서는 배포 프로세스의 일부로 데이터베이스 업데이트를 설명 하지 않습니다. 그러나 많은 엔터프라이즈 배포 시나리오의 요구 사항에는 데이터베이스 기능을 사용 하 여 증분 업데이트 하기 및이 자습서 시리즈의 뒷부분에서이 작업을 수행 하는 방법에 지침을 찾을 수 있습니다. 자세한 내용은 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)합니다.


## <a name="overview"></a>개요

에 설명 된 Fabrikam, Inc. 배포 시나리오를 기반으로 하는 여기서 설명 하는 배포 프로세스 [엔터프라이즈 웹 배포: 시나리오 개요](enterprise-web-deployment-scenario-overview.md)합니다. 이 항목을 검토 하기 전에 시나리오 개요를 읽어야 합니다. 시나리오 조직 비교적 복잡 한 웹 응용 프로그램 배포를 관리 하는 방법을 검사 기본적 합니다 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md), 일반적인 엔터프라이즈 환경에서 다양 한 단계입니다.

높은 수준에서 Contact Manager 솔루션 개발 및 배포 프로세스의 일부로 이러한 단계를 거칩니다.

1. 개발자는 Team Foundation Server (TFS) 2010에 일부 코드를 확인합니다.
2. TFS에서 코드를 작성 하 고 팀 프로젝트와 연결 된 모든 단위 테스트를 실행 합니다.
3. TFS는 테스트 환경에 솔루션을 배포합니다.
4. 개발자 팀 확인 하 고 테스트 환경에서 솔루션의 유효성을 검사 합니다.
5. 스테이징 환경 관리자는 스테이징 환경에 배포 문제가 발생 되는지 여부를 설정 하려면 "what if" 배포를 수행 합니다.
6. 스테이징 환경 관리자는 스테이징 환경으로 라이브 배포를 수행합니다.
7. 솔루션은 사용자 수용을 스테이징 환경에서 테스트를 거칩니다.
8. 웹 배포 패키지를 프로덕션 환경에 수동으로 가져올 않습니다.

이러한 단계는 연속 개발 주기의 한 부분을 형성합니다.

![](application-lifecycle-management-from-development-to-production/_static/image1.png)

실제로 프로세스는 이보다 조금 더 복잡 한 자세히 각 단계에 살펴봅니다 때 표시 됩니다. Fabrikam, Inc. 각 대상 환경에 배포 하는 다른 방법을 사용합니다.

![](application-lifecycle-management-from-development-to-production/_static/image2.png)

이 항목의 나머지 부분에는이 배포 수명 주기의 주요 단계에 이러한 검사:

- **필수 구성 요소**: 현재 위치에서 배포 논리를 배치 하기 전에 서버 인프라를 구성 해야 하는 방법입니다.
- **초기 개발 및 배포**: 처음으로 솔루션을 배포 하기 전에 수행 해야 합니다.
- **테스트를 위해 배포**: 패키지 및 배포 방법 콘텐츠 테스트 환경에 자동으로 새 코드에서는 개발자가 체크 합니다.
- **스테이징 배포**: 특정 배포 하는 방법에 빌드를 스테이징 환경 및 "what if"를 수행 하는 방법을 배포 문제가 발생 하지는 되도록 배포 합니다.
- **배포를 프로덕션으로**: 네트워크 인프라에는 원격 배포 하지 못하게 하는 경우 프로덕션 환경에 웹 패키지를 가져오는 방법입니다.

## <a name="prerequisites"></a>전제 조건

모든 배포 시나리오에서 첫 번째 작업 서버 인프라의 배포 도구 및 기술 요구 사항을 충족 하는지 확인 하는 것입니다. 이 경우 Fabrikam, Inc.가 다음과 같이 해당 서버 인프라 구성:

- TFS 팀 프로젝트 컬렉션을 포함, 빌드 컨트롤러와 빌드 에이전트 구성 됩니다. 참조 [자동화 된 웹 배포용 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) 자세한 내용은 합니다.
- 테스트 환경에 설명 된 대로 웹 배포 에이전트 서비스 ("원격 에이전트")를 사용 하는 원격 배포를 허용 하도록 구성 된 [시나리오: 웹 배포용 테스트 환경 구성](../configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment.md) 고 [ 웹 배포 게시용 (원격 에이전트)에 대 한 웹 서버를 구성할](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)합니다.
- 스테이징 환경에 설명 된 대로 웹 배포 처리기 끝점을 사용 하는 원격 배포를 허용 하도록 구성 된 [시나리오: 웹 배포용 스테이징 환경 구성](../configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment.md) 고 [웹 서버 구성 웹 배포 게시 (웹 배포 처리기)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)합니다.
- 프로덕션 환경에 설명 된 대로 관리자에 인터넷 정보 서비스 (IIS), 웹 배포 패키지를 수동으로 가져올 수를 허용 하도록 구성 되어 [시나리오: 웹 배포용프로덕션환경구성](../configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment.md) 하 고 [웹 배포 게시용 (오프 라인 배포)에 대 한 웹 서버를 구성할](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)합니다.

## <a name="initial-development-and-deployment"></a>초기 개발 및 배포

Fabrikam, Inc. 개발 팀은 처음으로 Contact Manager 솔루션을 배포 하려면, 이러한 작업을 수행 해야 합니다.

- TFS에서 새 팀 프로젝트를 만듭니다.
- 배포 논리를 포함 하는 Microsoft Build Engine (MSBuild) 프로젝트 파일을 만듭니다.
- 배포 프로세스를 트리거하는 TFS 빌드 정의 만듭니다.

### <a name="create-a-new-team-project"></a>새 팀 프로젝트 만들기

- 에 설명 된 대로 TFS 관리자 Rob Walters, 응용 프로그램에 대 한 새 팀 프로젝트를 만듭니다 [TFS에서 팀 프로젝트를 만들면](../configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs.md)합니다. 다음으로, Matt Hink 수석 개발자는 스 켈 레 톤 솔루션을 만듭니다. 에 설명 된 대로 자신의 파일에 TFS에서 새 팀 프로젝트로 체크 [소스 제어에 콘텐츠 추가](../configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control.md)합니다.

### <a name="create-the-deployment-logic"></a>배포 논리를 만듭니다

Matt Hink에 설명 된 분할 프로젝트 파일 방법을 사용 하 여 다양 한 사용자 지정 MSBuild 프로젝트 파일을 만듭니다 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다. Matt 만듭니다.

- 프로젝트 파일인 *Publish.proj* 배포 프로세스를 실행 하는 합니다. 이 파일에는 솔루션에서 프로젝트를 빌드할 웹 패키지를 만들고 대상 서버 환경에 패키지를 배포 하는 MSBuild 대상으로 포함 되어 있습니다.
- 환경 관련 프로젝트 파일 *Env Dev.proj* 하 고 *Env Stage.proj*합니다. 연결 문자열, 서비스 끝점에서 웹 패키지 받을 원격 서비스의 세부 정보 등 각각 테스트 환경과 스테이징 환경에 관련 된 설정이 포함 됩니다. 특정 대상 환경에 대 한 올바른 설정을 선택에 대 한 지침을 참조 하세요 [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)합니다.

사용자가 배포를 실행 하려면 다음을 실행 합니다.는 *Publish.proj* Team Build 또는 MSBuild를 사용 하 여 파일 및 관련 환경 관련 프로젝트 파일의 위치를 지정 합니다 (*Env Dev.proj* 또는*Env Stage.proj*) 명령줄 인수입니다. 합니다 *Publish.proj* 파일은 다음 각 대상 환경에 대 한 지침을 게시 하는 전체 집합을 만드는 환경 관련 프로젝트 파일을 가져옵니다.

> [!NOTE]
> 이러한 사용자 지정 프로젝트 파일의 작동 방식은 독립적 MSBuild 호출을 사용 하는 메커니즘입니다. 예를 들어 사용할 수는 MSBuild 명령줄을 직접에 설명 된 대로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다. 에 설명 된 대로 프로젝트 파일에서 명령 파일을 실행할 수 있습니다 [만들기 및 배포 명령 파일을 실행](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)합니다. 또는에서 실행할 수 있습니다 프로젝트 파일은 TFS에서 빌드 정의에 설명 된 대로 [는 지원 배포 빌드 정의 만들려면](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)합니다.  
> 각각의 경우 최종 결과&#x2014;MSBuild 병합 된 프로젝트 파일을 실행 하 고 대상 환경에 솔루션을 배포 합니다. 이렇게 하면 상당한 수준의 유연성을 게시 하는 과정을 트리거하는 방법을 제공 합니다.


만들어지면 그에 사용자 지정 프로젝트 파일 Matt 솔루션 폴더에 추가 하 고 소스 제어로 체크 합니다.

### <a name="create-build-definitions"></a>빌드 정의 만들기

최종 준비 작업으로 Matt과 Rob 함께 새 팀 프로젝트에 대 한 세 개의 빌드 정의 만들려면:

- **DeployToTest**합니다. Contact Manager 솔루션 빌드되고 체크 인 발생할 때마다 테스트 환경에 배포 됩니다.
- **DeployToStaging**합니다. 이 개발자 빌드 큐 대기 하는 경우 스테이징 환경에 지정 된 이전 빌드에서 리소스를 배포 합니다.
- **DeployToStaging-WhatIf**합니다. 이 개발자 빌드 큐 대기 하는 경우 스테이징 환경에 "what if" 배포를 수행 합니다.

이러한 각 세부 정보를 제공 하는 다음 단원에서는 빌드 정의 합니다.

## <a name="deployment-to-test"></a>테스트 배포

Fabrikam, Inc.의 개발 팀에는 다양 한 소프트웨어 테스트 확인 및 유효성 검사, 사용 편의성 테스트, 호환성 테스트 및 임시 또는 예비 테스트와 같은 작업을 수행 하려면 테스트 환경을 유지 관리 합니다.

개발 팀에 이동한 TFS 인에 빌드 정의 만들었다고 **DeployToTest**합니다. 이 빌드 정의 빌드 프로세스에서 체크 인 Fabrikam, Inc. 개발 팀의 멤버가 수행 될 때마다 실행 됨을 의미 하는 연속 통합 트리거를 사용 합니다. 빌드가 트리거될 때 빌드 정의 됩니다.

- ContactManager.sln 솔루션을 빌드하십시오. 이 솔루션 내에서 모든 프로젝트를 다시 빌드합니다.
- (솔루션을 성공적으로 빌드되면) 하는 경우 솔루션 폴더 구조의 모든 단위 테스트를 실행 합니다.
- (솔루션이 성공적으로 빌드되고 모든 단위 테스트 통과) 경우 배포 프로세스를 제어 하는 사용자 지정 프로젝트 파일을 실행 합니다.

최종 결과 솔루션 성공적으로 빌드되면 고 단위 테스트를 통과 하는 경우 웹 패키지 및 기타 배포 리소스 테스트 환경에 배포 됩니다.

![](application-lifecycle-management-from-development-to-production/_static/image3.png)

### <a name="how-does-the-deployment-process-work"></a>배포 프로세스는 어떻게 작동 하나요?

합니다 **DeployToTest** 빌드 정의 제공 MSBuild에 이러한 인수:


[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample1.cmd)]


합니다 **DeployOnBuild = true** 하 고 **DeployTarget = 패키지** Team Build 솔루션 내의 프로젝트를 빌드할 때 속성을 사용 합니다. 프로젝트를 웹 응용 프로그램 프로젝트를 이러한 속성에 MSBuild 프로젝트에 대 한 웹 배포 패키지를 만드는 하도록 지시 합니다. 합니다 **TargetEnvPropsFile** 속성은 합니다 *Publish.proj* 가져오려면 환경별 프로젝트 파일을 찾을 수 있는 위치를 파일.

> [!NOTE]
> 다음과 같은 빌드 정의 만드는 방법에 자세한 연습을 참조 하세요 [는 지원 배포 빌드 정의 만들려면](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)합니다.


합니다 *Publish.proj* 파일 해당 솔루션의 각 프로젝트 빌드 대상이 포함 되어 있습니다. 그러나 조건부 논리를 건너뛰고 이러한 빌드 대상 Team Build에서 파일을 실행 하는 경우 또한 포함 합니다. 이렇게 하면 제공 하는 팀 빌드, 단위 테스트를 실행 하는 기능과 같은 추가 빌드 기능을 활용할 수 있습니다. 솔루션 빌드 또는 단위 테스트 실패 하는 경우는 *Publish.proj* 파일 실행 되지 것입니다 및 응용 프로그램 배포 되지 것입니다.

조건부 논리를 평가 하 여 수행 됩니다 합니다 **BuildingInTeamBuild** 속성입니다. MSBuild 속성을 자동으로 설정 된 **true** 사용 하는 경우 팀 빌드 프로젝트를 빌드할 수 있습니다.

## <a name="deployment-to-staging"></a>스테이징에 배포

빌드를 테스트 환경에서 개발자 팀의 요구 사항을 모두 충족을 하는 경우 팀 스테이징 환경에 동일한 빌드를 배포 하려고 합니다. 스테이징 환경은 일반적으로 프로덕션 또는 밀접 하 게 최대한, 예를 들어 서버 사양, 운영 체제 및 소프트웨어 및 네트워크 구성을 기준으로 "라이브" 환경으로의 특성에 맞게 구성 됩니다. 부하 테스트, 사용자 승인 테스트 및 광범위 한 내부 검토에 대 한 스테이징 환경 자주 사용 됩니다. 빌드는 빌드 서버에서 직접 스테이징 환경에 배포 됩니다.

![](application-lifecycle-management-from-development-to-production/_static/image4.png)

스테이징 환경에 솔루션을 배포 하는 데 사용 하는 빌드 정의 **DeployToStaging-WhatIf** 하 고 **DeployToStaging**, 이러한 특성을 공유:

- 실제로 아무 것도 작성 하지 않아도 해당 합니다. Rob 스테이징 환경에 솔루션을 배포 하는 경우에 이미 확인 및 테스트 환경에서 유효성을 검사 하는 특정 한 기존 빌드를 배포 하고자 합니다. 빌드 정의 배포 프로세스를 제어 하는 사용자 지정 프로젝트 파일을 실행 해야 합니다.
- Rob 빌드를 트리거하는 경우 빌드 서버에서 배포 하고자 하는 리소스를 포함 하는 빌드 지정 하려면 빌드 매개 변수를 사용 합니다.
- 빌드 정의 자동으로 트리거되지 않습니다. Rob 스테이징 환경에 솔루션을 배포 하고자 하는 경우 수동으로 빌드를 큐입니다.

스테이징 환경에 배포를 위한 고급 프로세스는 다음과 같습니다.

1. 스테이징 환경 관리자, Rob Walters, 사용 하 여 빌드 큐를 **DeployToStaging-WhatIf** 빌드 정의 합니다. Rob 배포 하고자 하는 빌드를 지정 하려면 빌드 정의 매개 변수를 사용 합니다.
2. 합니다 **DeployToStaging-WhatIf** 정의 실행 "what if" 모드에서 사용자 지정 프로젝트 파일을 작성 합니다. 이 처럼 Rob 라이브 배포를 수행 하지만 하지 실제로 변경 모든 대상 환경에 로그 파일을 생성 합니다.
3. Rob 스테이징 환경에서 배포의 효과 확인 하려면 로그 파일을 검토 합니다. 특히, Rob 추가 기능, 새로운 업데이트될지 및 삭제할 항목을 확인 하려고 합니다.
4. Rob 경우 사용 하 여 빌드 큐가 배포 되지 않습니다 게 변경 하는 모든 바람직하지 않은 기존 리소스나 데이터에 만족 하는 **DeployToStaging** 빌드 정의 합니다.
5. 합니다 **DeployToStaging** 정의 실행 사용자 지정 프로젝트 파일을 작성 합니다. 이러한 배포 리소스를 스테이징 환경에서 기본 웹 서버에 게시 합니다.
6. Wff (웹 팜 프레임 워크) 컨트롤러는 스테이징 환경에서 웹 서버를 동기화합니다. 이렇게 하면 서버 팜의 모든 웹 서버에서 사용할 수 있는 응용 프로그램.

### <a name="how-does-the-deployment-process-work"></a>배포 프로세스는 어떻게 작동 하나요?

합니다 **DeployToStaging** 빌드 정의 제공 MSBuild에 이러한 인수:


[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample2.cmd)]


합니다 **TargetEnvPropsFile** 속성은 합니다 *Publish.proj* 가져오려면 환경별 프로젝트 파일을 찾을 수 있는 위치를 파일. 합니다 **OutputRoot** 속성 기본 제공 값을 재정의 하 고 배포 하려는 리소스를 포함 하는 빌드 폴더의 위치를 나타냅니다. Rob 큐 빌드를 사용할 때 사용 합니다 **매개 변수** 탭에 대 한 업데이트 된 값을 제공 하는 **OutputRoot** 속성입니다.

![](application-lifecycle-management-from-development-to-production/_static/image5.png)

> [!NOTE]
> 다음과 같은 빌드 정의 만드는 방법에 대 한 자세한 내용은 참조 하세요. [특정 빌드를 배포](../configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build.md)합니다.


합니다 **DeployToStaging-WhatIf** 와 같은 배포 논리를 포함 하는 빌드 정의 **DeployToStaging** 빌드 정의 합니다. 그러나 여기에 추가 인수 **WhatIf = true**:


[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample3.cmd)]


내를 *Publish.proj* 파일을 **WhatIf** 속성 "what if" 모드에서 모든 배포 리소스를 게시할 나타냅니다. 즉, 배포를 계속 해 서 완료가 있지만 대상 환경에서 실제로 변경 된 사항이 없습니다 처럼 로그 파일이 생성 됩니다. 이렇게 하면 제안 된 배포의 영향을 평가할 수 있습니다&#x2014;특정, 어떤 추가 됩니다, 항목은 업데이트 및 삭제는 어떤&#x2014;실제로 변경 하기 전에 합니다.

> [!NOTE]
> "What if" 배포를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. ["What If" 배포 수행](../advanced-enterprise-web-deployment/performing-a-what-if-deployment.md)합니다.


스테이징 환경에서 기본 웹 서버에 응용 프로그램을 배포한 후의 WFF 서버 팜의 모든 서버에서 응용 프로그램을 자동으로 동기화 합니다.

> [!NOTE]
> 웹 서버를 동기화 할 WFF를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [웹 팜 프레임 워크를 사용 하 여 서버 팜 만들기](../configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework.md)합니다.


## <a name="deployment-to-production"></a>프로덕션에 배포

스테이징 환경에서 빌드를 승인 하는 경우 Fabrikam, Inc. 팀은 프로덕션 환경에 응용 프로그램을 게시할 수 있습니다. 프로덕션 환경 위치 이며 응용 프로그램 "라이브" 상태가 최종 사용자가 해당 대상에 도달 합니다.

프로덕션 환경은 인터넷 경계 네트워크에 있습니다. 이 빌드 서버를 포함 하는 내부 네트워크와에서 격리 됩니다. 수동으로 프로덕션 환경 관리자 인 Lisa Andrews 빌드 서버에서 웹 배포 패키지를 복사 하 고 기본 프로덕션 웹 서버에서 IIS로 가져올 해야 합니다.

![](application-lifecycle-management-from-development-to-production/_static/image6.png)

프로덕션 환경으로 배포를 위한 고급 프로세스는 다음과 같습니다.

1. 개발자 팀 빌드를 프로덕션 환경에 배포할 준비가 되었는지 Lisa 권고 합니다. 팀 빌드 서버의 저장 폴더 내에서 웹 배포 패키지의 위치는 Lisa을 권고합니다.
2. Lisa 빌드 서버에서 웹 패키지를 수집 하 고 프로덕션 환경에서 기본 웹 서버에 복사 합니다.
3. Lisa는 IIS 관리자를 사용 하 여 가져오기 및 기본 웹 서버에서 웹 패키지를 게시 합니다.
4. WFF 컨트롤러 프로덕션 환경에서 웹 서버를 동기화합니다. 이렇게 하면 서버 팜의 모든 웹 서버에서 사용할 수 있는 응용 프로그램.

### <a name="how-does-the-deployment-process-work"></a>배포 프로세스는 어떻게 작동 하나요?

IIS 관리자는 응용 프로그램 패키지 가져오기 마법사 쉽게 웹 패키지는 IIS 웹 사이트를 게시 하기를 포함 합니다. 이 절차를 수행 하는 방법에 대 한 연습은 대해서 [수동으로 웹 패키지 설치](../web-deployment-in-the-enterprise/manually-installing-web-packages.md)합니다.

## <a name="conclusion"></a>결론

이 항목에서는 일반적인 엔터프라이즈급 웹 응용 프로그램에 대 한 배포 수명 주기의 예시를 제공 합니다.

이 항목에서는의 웹 응용 프로그램 배포의 다양 한 측면에 지침을 제공 하는 자습서 시리즈의 일부를 형성 합니다. 실제로 배포 프로세스의 각 단계에서 추가 작업 및 고려 사항에 대 한 많은 되며 단일 연습의 모두 다룰 수 없는 있습니다. 자세한 내용은이 자습서를 참조 하세요.

- [엔터프라이즈 배포에서에서 웹](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)합니다. 이 자습서에서는 MSBuild 및 IIS 웹 배포 도구 (웹 배포)를 사용 하 여 웹 배포 기술에 대 한 포괄적인 소개를 제공 합니다.
- [웹 배포용 서버 환경 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다. 이 자습서는 다양 한 배포 시나리오를 지원 하기 위해 Windows server 환경을 구성 하는 방법에 지침을 제공 합니다.
- [웹 배포를 자동화 된 Team Foundation Server에 대 한 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다. 이 자습서는 TFS 빌드 프로세스로 배포 논리를 통합 하는 방법에 지침을 제공 합니다.
- [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)합니다. 이 자습서 지침 제공 몇 가지 더 복잡 한 배포 과제를 충족 하는 방법은 조직에서 직면 합니다.

> [!div class="step-by-step"]
> [이전](enterprise-web-deployment-scenario-overview.md)
