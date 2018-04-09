---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
title: 배포를 지원 하는 빌드 정의 만드는 | Microsoft Docs
author: jrjlee
description: Team Foundation Server (TFS) 2010에서 모든 종류의 빌드를 수행 하려면 팀 프로젝트 내에서 빌드 정의 만드는 데 필요 합니다. 이 항목 des 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: fe47a018-f6d0-4979-80e7-5b1fa75a5865
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
msc.type: authoredcontent
ms.openlocfilehash: c5ea0bd9f01bb57b96abd349741f304c0093d887
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="creating-a-build-definition-that-supports-deployment"></a>배포를 지원 하는 빌드 정의 만들기
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Team Foundation Server (TFS) 2010에서 모든 종류의 빌드를 수행 하려면 팀 프로젝트 내에서 빌드 정의 만드는 데 필요 합니다. 이 항목에서는 TFS에서 새 빌드 정의 만드는 방법과 팀 빌드의 빌드 프로세스의 일부로 웹 배포를 제어 하는 방법을 설명 합니다.


이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하는 자습서 시리즈가&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성, Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 WCF (foundation) 서비스 및 데이터베이스 프로젝트.

이 자습서의 핵심에는 배포 방법에 설명 된 분할 프로젝트 파일 접근 방식에 따라 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에 빌드 및 배포 프로세스에 의해 제어 되는&#x2014;하나 환경 관련 빌드 및 배포 설정을 포함 하는 하나 및 모든 대상 환경에 적용 되는 빌드 명령이 포함 된입니다. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 구성 하기 위해 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="task-overview"></a>작업 개요

빌드 정의는 TFS의 팀 프로젝트에 대 한 빌드가 수행 방식 및 시기를 제어 하는 메커니즘입니다. 각 빌드 정의 지정합니다.

- 예: Visual Studio 솔루션 파일 또는 Microsoft Build Engine (MSBuild) 프로젝트 파일 사용자 지정 빌드 하려는 것입니다.
- 빌드를 수행 해야 하는 경우를 결정 하는 기준을 CI (연속 통합), 수동 트리거와 마찬가지로 배치 또는 제어 된 체크 인 합니다.
- 팀 빌드 보내야 하 웹 패키지 및 데이터베이스 스크립트와 같은 배포 아티팩트를 포함 하 여 빌드 출력 위치입니다.
- 각 빌드를 유지 해야 하는 시간의 양입니다.
- 다양 한 기타 매개 변수는 빌드 프로세스입니다.

> [!NOTE]
> 빌드 정의 대 한 자세한 내용은 참조 하십시오. [빌드 프로세스 정의](https://msdn.microsoft.com/library/ms181715.aspx)합니다.


이 항목은 빌드는 개발자가 새 내용에서 체크 인하는 경우에 트리거됩니다 CI를 사용 하는 빌드 정의 만드는 방법을 보여 줍니다. 빌드가 성공한 경우 빌드 서비스를 테스트 환경에 솔루션을 배포 하는 사용자 지정 프로젝트 파일을 실행 합니다.

빌드를 트리거 이러한 작업에서 발생 해야 합니다.

- 첫째, 팀 빌드 솔루션을 구축 해야 합니다. 이 프로세스의 일부로 팀 빌드 웹 게시 파이프라인 (WPP) 각 솔루션의 웹 응용 프로그램 프로젝트에 대 한 웹 배포 패키지를 생성 하려면 호출 합니다. 팀 빌드 솔루션과 관련 된 모든 단위 테스트도 실행 됩니다.
- 솔루션 빌드 오류가 발생 하면 팀 빌드 추가 작업이 없으므로 수행 해야 합니다. 단위 테스트 실패를 빌드 오류로 취급 되어야 합니다.
- 솔루션 빌드에 성공 하면 팀 빌드 솔루션의 배포를 제어 하는 사용자 지정 프로젝트 파일을 실행 해야 합니다. 이 프로세스의 일부로 팀 빌드 (웹 배포)를 대상 웹 서버에서 패키지에 포함 된 웹 응용 프로그램을 설치 하려면 인터넷 정보 서비스 (IIS) 웹 배포 도구는 호출 하 고 데이터베이스 생성을 실행할 VSDBCMD.exe 유틸리티를 호출 합니다. 대상 데이터베이스 서버에 대 한 스크립트입니다.

프로세스를 들 수 있습니다.

![](creating-a-build-definition-that-supports-deployment/_static/image1.png)

[않아](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 솔루션에는 사용자 지정 MSBuild 프로젝트 파일 *Publish.proj*, MSBuild 또는 팀 빌드를 실행할 수 있는 합니다. 에 설명 된 대로 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md),이 프로젝트 파일을 대상 환경에 웹 패키지 및 데이터베이스를 배포 하는 논리를 정의 합니다. 파일에서 팀 빌드만 배포 작업이 실행 되도록 그대로 두고 실행 중인 경우 빌드 및 패키징 프로세스를 생략 하는 논리를 포함 합니다. 하므로 이러한 방식으로 배포를 자동화 하는 경우 일반적으로 솔루션을 성공적으로 빌드되도록 이며 배포 프로세스를 시작 하기 전에 모든 단위 테스트를 통과 합니다.

다음 섹션에는 새 빌드 정의 만들어이 프로세스를 구현 하는 방법을 설명 합니다.

> [!NOTE]
> 이 절차&#x2014;단일 자동화 된 프로세스를 작성, 테스트 하 고, 및에서 솔루션을 배포&#x2014;배포를 테스트 환경에 가장 적합 한 수입니다. 스테이징 및 프로덕션 환경에 대 한 있습니다 가능성이 훨씬 더 이전 버전 으로부터 이미 확인 및 테스트 환경에서 유효성을 검사 하는 콘텐츠를 배포 합니다. 이 방법은 다음 항목에서 설명 [는 특정 빌드 배포](deploying-a-specific-build.md)합니다.


### <a name="who-performs-this-procedure"></a>이 절차를 수행 하는 사람?

일반적으로 TFS 관리자가이 절차를 수행합니다. 경우에 따라 개발자 팀 리더는 TFS에서 팀 프로젝트 컬렉션에 대 한 책임을 걸릴 수 있습니다. 멤버는 새 빌드 정의 만들기 위해 필요는 **프로젝트 컬렉션 빌드 관리자** 솔루션을 포함 하는 팀 프로젝트 컬렉션에 대 한 그룹입니다.

## <a name="create-a-build-definition-for-ci-and-deployment"></a>CI 및 배포에 대 한 빌드 정의 만들기

다음 절차를 CI 트리거하는 빌드 정의 만드는 방법을 설명 합니다. 빌드가 성공 하면 사용자 지정 MSBuild 프로젝트 파일에는 논리를 사용 하 여 솔루션 배포 됩니다.

**CI 및 배포에 대 한 빌드 정의 만들려면**

1. Visual Studio 2010에서에 **팀 탐색기** 창, 팀 프로젝트 노드를 마우스 오른쪽 단추로 클릭 **빌드**, 클릭 하 고 **새 빌드 정의**합니다.

    ![](creating-a-build-definition-that-supports-deployment/_static/image2.png)
2. 에 **일반** 탭에서 빌드 정의 이름을 지정 (예를 들어 **DeployToTest**) 및 선택적 설명을 합니다.
3. 에 **트리거** 탭에서 새 빌드 하려는 조건을 선택 합니다. 예를 들어, 솔루션 빌드 및 개발자가 새 코드에 체크 인하 될 때마다 테스트 환경에 배포 하려는 경우 선택 **연속 통합**합니다.
4. 에 **빌드 기본값** 탭에 **다음 저장 폴더에 빌드 출력 복사** 저장 폴더의 범용 명명 규칙 (UNC) 경로 입력 합니다 (예를 들어  **\\TFSBUILD\Drops**).

    ![](creating-a-build-definition-that-supports-deployment/_static/image3.png)

    > [!NOTE]
    > 이 저장 위치를 구성한 보존 정책에 따라 여러 개의 빌드를 저장 합니다. 특정 빌드에서 배포 아티팩트를 스테이징 또는 프로덕션 환경에 게시 하려는 경우 찾을 수 있는입니다.
5. 에 **프로세스** 탭에 **빌드 프로세스 파일** 드롭다운 목록에서 leave **DefaultTemplate.xaml** 선택한 합니다. 모든 새 팀 프로젝트에 추가 하면 기본 빌드 프로세스 템플릿 중 하나입니다.
6. 에 **빌드 프로세스 매개 변수** 테이블에서 클릭는 **빌드할 항목** 행을 클릭 하 고는 **줄임표** 단추입니다.

    ![](creating-a-build-definition-that-supports-deployment/_static/image4.png)
7. 에 **빌드할 항목** 대화 상자를 클릭 **추가**합니다.
8. 솔루션 파일의 위치를 찾은 다음 클릭 **확인**합니다.

    ![](creating-a-build-definition-that-supports-deployment/_static/image5.png)
9. 에 **빌드할 항목** 대화 상자를 클릭 **추가**합니다.
10. 에 **형식의 항목** 드롭다운 목록에서 선택 **MSBuild 프로젝트 파일**합니다.
11. 배포 프로세스를 제어, 파일을 선택한 다음를 클릭 하 여 사용자 지정 프로젝트 파일의 위치를 찾아 **확인**합니다.

    ![](creating-a-build-definition-that-supports-deployment/_static/image6.png)
12. **빌드할 항목** 대화 상자가 두 개의 항목이 표시 됩니다. **확인**을 클릭합니다.

    ![](creating-a-build-definition-that-supports-deployment/_static/image7.png)
13. 에 **프로세스** 탭에 **빌드 프로세스 매개 변수** 테이블을 확장 하 고는 **고급** 섹션.
14. 에 **MSBuild 인수** 행에서 MSBuild 명령줄 인수를 추가 하는 *어느* 빌드할 항목의 필요 합니다. Contact Manager 솔루션 시나리오에서 이러한 인수가 필요 합니다.

    [!code-console[Main](creating-a-build-definition-that-supports-deployment/samples/sample1.cmd)]

    ![](creating-a-build-definition-that-supports-deployment/_static/image8.png)
15. 이 예제에 대한 설명:

    1. **DeployOnBuild = true** 및 **DeployTarget 패키지 =** Contact Manager 솔루션을 빌드할 때의 인수가 필요 합니다. 이렇게 하면 MSBuild에서 웹 배포 패키지를 만들 각 웹 응용 프로그램 프로젝트를 빌드한 후에 설명 된 대로 [빌드 및 패키징 웹 응용 프로그램 프로젝트](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)합니다.
    2. **TargetEnvPropsFile** 빌드할 때 인수는 필수는 *Publish.proj* 파일입니다. 이 속성에 설명 된 대로 환경 관련 구성 파일의 위치를 나타내는 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다.
16. 에 **보존 정책** 탭에서 필요에 따라 유지 하려면 각 유형의 한 빌드의 수를 구성 합니다.
17. **저장**을 클릭합니다.

## <a name="queue-a-build"></a>큐에 빌드 대기시키기

이 시점에서 새 빌드 정을 하나 이상 만들었습니다. 빌드 프로세스 정의 빌드 정의에 지정 된 트리거 따라 이제 실행 됩니다.

CI를 사용 하 여 빌드 정의 구성한 경우에 두 가지 방법으로 빌드 정의 테스트할 수 있습니다.

- 자동 빌드를 트리거할 팀 프로젝트에 일부 콘텐츠를 확인 합니다.
- 수동으로 빌드를 큐에 대기 합니다.

**빌드를 큐에 수동으로**

1. 에 **팀 탐색기** 창에서 빌드 정의 마우스 오른쪽 단추로 클릭 **새 빌드 큐 대기**합니다.

    ![](creating-a-build-definition-that-supports-deployment/_static/image9.png)
2. 에 **빌드 큐 대기** 대화 상자, 빌드 속성을 검토 한 다음 클릭 **큐**합니다.

    ![](creating-a-build-definition-that-supports-deployment/_static/image10.png)

진행률 및 빌드 결과 검토 하려면&#x2014;수동 또는 자동으로 트리거 여부에 관계 없이&#x2014;에서 빌드 정의 두 번 클릭은 **팀 탐색기** 창. 열립니다는 **빌드 탐색기** 탭 합니다.

![](creating-a-build-definition-that-supports-deployment/_static/image11.png)

여기에서는 빌드 실패를 해결할 수 있습니다. 각 빌드를 두 번 클릭 하면 요약 정보를 볼 수 있으며 클릭 하 여 자세한 로그 파일을.

![](creating-a-build-definition-that-supports-deployment/_static/image12.png)

실패 한 빌드 문제를 해결 하 고 다른 빌드를 시도 하기 전에 문제를 해결 하려면이 정보를 사용할 수 있습니다.

> [!NOTE]
> 배포 논리를 실행 하는 빌드는 빌드 서버 대상 환경에 필요한 모든 권한을 부여 될 때까지 실패할 수 있습니다. 자세한 내용은 참조 [팀 빌드 배포에 대 한 사용 권한 구성](configuring-permissions-for-team-build-deployment.md)합니다.


## <a name="monitor-the-build-process"></a>빌드 프로세스를 모니터링 합니다.

TFS 광범위 한 빌드 프로세스를 모니터링 하는 기능을 제공 합니다. 예를 들어 TFS 전자 메일을 보낼 수 또는 빌드 완료 되었을 때 작업 표시줄 알림 영역에서 경고를 표시 합니다. 자세한 내용은 참조 [실행 및 빌드 모니터링](https://msdn.microsoft.com/library/ms181721.aspx)합니다.

## <a name="conclusion"></a>결론

이 항목을 TFS에서 빌드 정의 만드는 방법을 설명 합니다. 개발자가 팀 프로젝트에 내용에서 체크 인하 때마다 빌드 프로세스에서 실행 되도록 빌드 정의 CI에 대 한 구성 됩니다. 빌드 정의 대상 서버 환경에 웹 패키지 및 데이터베이스 스크립트를 배포 하는 사용자 지정 MSBuild 프로젝트 파일을 실행 합니다.

빌드 프로세스의 일부로 성공 하는 자동화 된 배포 순서, 대상 웹 서버와 대상 데이터베이스 서버에 빌드 서비스 계정에 적절 한 권한을 부여 해야 합니다. 이 자습서의 최종 항목 [팀 빌드 배포에 대 한 사용 권한 구성](configuring-permissions-for-team-build-deployment.md)를 식별 하 고 팀 빌드 서버에서 자동화 된 배포에 필요한 사용 권한을 구성 하는 방법을 설명 합니다.

## <a name="further-reading"></a>추가 정보

빌드 정의 만드는 방법에 대 한 자세한 내용은 참조 하십시오. [기본 빌드 정의 만들기](https://msdn.microsoft.com/library/ms181716.aspx) 및 [빌드 프로세스 정의](https://msdn.microsoft.com/library/ms181715.aspx)합니다. 빌드를 큐에 대 한 자세한 지침을 참조 하십시오. [빌드 큐에 대기](https://msdn.microsoft.com/library/ms181722.aspx)합니다.

> [!div class="step-by-step"]
> [이전](configuring-a-tfs-build-server-for-web-deployment.md)
> [다음](deploying-a-specific-build.md)
