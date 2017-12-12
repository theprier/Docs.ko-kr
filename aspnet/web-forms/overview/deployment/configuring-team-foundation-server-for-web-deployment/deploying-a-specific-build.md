---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: "특정 빌드를 배포 | Microsoft Docs"
author: jrjlee
description: "이 항목에서는 웹 패키지 및 이전 버전 으로부터 특정 스테이징 또는 프로덕션 환경 같은 새 대상 데이터베이스 스크립트를 배포 하는 방법에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: afac083c96c1396ad60275fcb55a0ec9c4c0bd44
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="deploying-a-specific-build"></a>특정 빌드를 배포합니다.
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 웹 패키지 및 이전 버전 으로부터 특정 스테이징 또는 프로덕션 환경 같은 새 대상 데이터베이스 스크립트를 배포 하는 방법에 설명 합니다.


이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 이 자습서 시리즈 샘플 솔루션 & #x 2014;을 사용 하는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& #x 2014; 현실적인 수준의 복잡성을 Windows ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 제공 합니다.

이 자습서의 핵심에는 배포 방법에 설명 된 분할 프로젝트 파일 접근 방식에 따라 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 빌드 및 배포 프로세스는 두 개의 프로젝트 파일 & #x 2014로 제어 되; o 환경 관련 빌드 및 배포 설정을 포함 하는 하나 및 모든 대상 환경에 적용 되는 빌드 명령이 포함 된 ne 합니다. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 구성 하기 위해 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="task-overview"></a>작업 개요

지금까지이 자습서에서는 항목 빌드, 패키지 및 웹 응용 프로그램 및 데이터베이스를 단일 단계의 일부분으로 배포 하는 방법에 초점을 맞춘 했거나 프로세스를 자동화 합니다. 그러나 몇 가지 일반적인 시나리오의 빌드 저장 폴더에는 목록에서 배포 하는 리소스를 선택 해야 합니다. 즉, 최신 빌드를 배포 하려는 빌드 아닐 수 있습니다.

이전 항목에 설명 된 CI (연속 통합) 시나리오를 생각해 볼 [빌드 정의 지원 배포 만들려면](creating-a-build-definition-that-supports-deployment.md)합니다. 빌드 정을 Team Foundation Server (TFS) 2010에서 만들었습니다. TFS에 코드를 확인 하는 개발자, 때마다 팀 빌드 됩니다 코드를 작성, 빌드 프로세스의 일부로 웹 패키지 및 데이터베이스 스크립트를 만들, 모든 단위 테스트를 실행 및 리소스는 테스트 환경에 배포 합니다. 빌드 정의 만들 때 구성 된 보존 정책에 따라 TFS 특정 개수의 이전 빌드를 유지 합니다.

![](deploying-a-specific-build/_static/image1.png)

이제 테스트 환경에서 빌드 중 하나에 대해서도 테스트 하는 유효성 검사 및 응용 프로그램을 스테이징 환경에 배포할 준비가 되었습니다. 확인을 수행 했을 가정 합니다. 한편, 개발자가 새 코드에 체크 수 있습니다. 솔루션을 다시 작성 하 고 스테이징 환경에 배포 하지 않으려는 스테이징 환경에 최신 빌드를 배포 하려면. 대신, 확인 하 고 테스트 서버에서 유효성을 검사 하는 특정 빌드를 배포 하려고 합니다.

이를 위해 Microsoft Build Engine (MSBuild) 웹 패키지 및 특정 빌드를 생성 하는 데이터베이스 스크립트를 찾을 위치를 지시 해야 합니다.

## <a name="overriding-the-outputroot-property"></a>OutputRoot 속성을 재정의

에 [샘플 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md), *Publish.proj* 라는 속성을 선언 하는 파일 **OutputRoot**합니다. 이름에서 알 수 있듯이 빌드 프로세스를 생성 하는 모든 항목이 포함 된 루트 폴더입니다. 에 *Publish.proj* 파일을 볼 수 있습니다 하는 **OutputRoot** 속성은 모든 배포 리소스에 대 한 루트 위치를 참조 합니다.

> [!NOTE]
> **OutputRoot** 자주 사용 되는 속성 이름입니다. 또한 visual C# 및 Visual Basic 프로젝트 파일에 대 한 모든 빌드 출력이 루트 위치를 저장 하려면이 속성을 선언 합니다.


[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]


웹 패키지 및;는 이전 TFS 빌드 & #x 2014;의 출력을와 같은 다른 위치 & #x 2014에서 데이터베이스 스크립트를 배포 하기 위해 프로젝트 파일을 원하는 경우 단순히 재정의 해야는 **OutputRoot** 속성입니다. 팀 빌드 서버에서 관련 빌드 폴더에 속성 값을 설정 해야 합니다. 명령줄에서 MSBuild를 실행 했을 대 한 값을 지정할 수 있습니다 **OutputRoot** 명령줄 인수로:


[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]


그러나 실제로, 것도 건너 뛰 려는 **빌드** 대상 & #x 2014; 솔루션을 빌드할 때 빌드 출력을 사용 하지 않으려는 경우에 포인터가 없는 합니다. 명령줄에서 실행할 대상을 지정 하 여 수행할 수 있습니다.


[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]


그러나 대부분의 경우 TFS 빌드 정의를 배포 논리를 작성 해야 합니다. 이렇게 하면 사용자와는 **큐에 빌드 대기** TFS 서버에 연결 된 모든 Visual Studio 설치에서 배포를 트리거할 수 있는 권한이 있습니다.

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a>빌드를 배포 하는 빌드 정의 특정 만들기

다음 절차에는 사용자가 단일 명령으로 스테이징 환경에 대 한 트리거 배포가 수 있는 빌드 정의를 만드는 방법을 설명 합니다.

이 경우 빌드 정의를 실제로 생성 아무 것도 않을 & #x 2014; 사용자 지정 프로젝트 파일의 배포 논리를 실행 하 려 합니다. *Publish.proj* 건너뛴 조건부 논리를 포함 하는 파일의 **빌드** 파일 Team Build에서 실행 중인 경우를 대상으로 합니다. 기본 제공 계산 하 여 이렇게 **BuildingInTeamBuild** 속성으로 자동으로 설정 된 **true** Team Build에서 프로젝트 파일을 실행 하는 경우. 결과적으로, 빌드 프로세스를 건너뛸 수 있으며 기존 빌드를 배포 하려면 프로젝트 파일을 실행 하면 됩니다.

**배포를 수동으로 트리거할 빌드 정의를 만들려면**

1. Visual Studio 2010에서에 **팀 탐색기** 창, 팀 프로젝트 노드를 마우스 오른쪽 단추로 클릭 **빌드**, 클릭 하 고 **새 빌드 정의**합니다.

    ![](deploying-a-specific-build/_static/image2.png)
2. 에 **일반** 탭에서 빌드 정의 이름을 지정 (예를 들어 **DeployToStaging**) 및 선택적 설명을 합니다.
3. 에 **트리거** 탭에서 **수동-체크 인은 새 빌드를 트리거하지 않습니다**합니다.
4. 에 **빌드 기본값** 탭에 **다음 저장 폴더에 빌드 출력 복사** 저장 폴더의 범용 명명 규칙 (UNC) 경로 입력 합니다 (예를 들어  **\\TFSBUILD\Drops**).

    ![](deploying-a-specific-build/_static/image3.png)
5. 에 **프로세스** 탭에 **빌드 프로세스 파일** 드롭다운 목록에서 leave **DefaultTemplate.xaml** 선택한 합니다. 모든 새 팀 프로젝트에 추가 하면 기본 빌드 프로세스 템플릿 중 하나입니다.
6. 에 **빌드 프로세스 매개 변수** 테이블에서 클릭는 **빌드할 항목** 행을 클릭 하 고는 **줄임표** 단추입니다.

    ![](deploying-a-specific-build/_static/image4.png)
7. 에 **빌드할 항목** 대화 상자를 클릭 **추가**합니다.
8. 에 **형식의 항목** 드롭다운 목록에서 선택 **MSBuild 프로젝트 파일**합니다.
9. 배포 프로세스를 제어, 파일을 선택한 다음를 클릭 하 여 사용자 지정 프로젝트 파일의 위치를 찾아 **확인**합니다.

    ![](deploying-a-specific-build/_static/image5.png)
10. 에 **빌드할 항목** 대화 상자를 클릭 **확인**합니다.
11. 에 **빌드 프로세스 매개 변수** 테이블을 확장 하 고는 **고급** 섹션.
12. 에 **MSBuild 인수** 행 환경별 프로젝트 파일의 위치를 지정 하 고 빌드 폴더의 위치에 대 한 자리 표시자를 추가 합니다.

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > 재정의 할는 **OutputRoot** 빌드를 큐에 대기 될 때마다 값입니다. 이 내용은 다음 절차에서 설명 합니다.
13. **저장**을 클릭합니다.

업데이트 해야 하는 경우 빌드를 트리거는 **OutputRoot** 배포 하려면 빌드를 가리키도록 속성입니다.

**빌드 정의에서 특정 빌드를 배포 하려면**

1. 에 **팀 탐색기** 창에서 빌드 정의 마우스 오른쪽 단추로 클릭 **새 빌드 큐 대기**합니다.

    ![](deploying-a-specific-build/_static/image7.png)
2. 에 **빌드 큐 대기** 대화 상자의 **매개 변수** 탭을 확장 하 고는 **고급** 섹션.
3. 에 **MSBuild 인수** 행에서의 값을 대체는 **OutputRoot** 빌드 폴더의 위치를 사용 하 여 속성입니다. 예:

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > 빌드 폴더에 대 한 경로의 끝에 후행 슬래시를 포함 해야 합니다.
4. 클릭 **큐**합니다.

빌드를 큐 하 고 프로젝트 파일에서 데이터베이스 스크립트를 배포 합니다 빌드 저장 폴더에서 웹 패키지에서 지정한는 **OutputRoot** 속성입니다.

## <a name="conclusion"></a>결론

이 항목에는 분할 프로젝트 파일의 배포 모델을 사용 하 여 특정 이전 빌드에서 웹 패키지 및 데이터베이스 스크립트와 같은 배포 리소스를 게시 하는 방법을 설명 합니다. 재정의 하는 방법을 설명 하는 **OutputRoot** 속성 및 TFS에 배포 논리를 통합 하는 방법에 대 한 빌드 정의 합니다.

## <a name="further-reading"></a>추가 정보

빌드 정의 만드는 방법에 대 한 자세한 내용은 참조 하십시오. [기본 빌드 정의 만들기](https://msdn.microsoft.com/en-us/library/ms181716.aspx) 및 [빌드 프로세스 정의](https://msdn.microsoft.com/en-us/library/ms181715.aspx)합니다. 빌드를 큐에 대 한 자세한 지침을 참조 하십시오. [빌드 큐에 대기](https://msdn.microsoft.com/en-us/library/ms181722.aspx)합니다.

>[!div class="step-by-step"]
[이전](creating-a-build-definition-that-supports-deployment.md)
[다음](configuring-permissions-for-team-build-deployment.md)
