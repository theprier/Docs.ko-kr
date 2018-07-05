---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment
title: 대상 환경에 대 한 배포 속성 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 특정 대상 환경에 샘플 Contact Manager 솔루션을 배포 하기 위해 환경 관련 속성을 구성 하는 방법을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: b5b86e03-b8ed-46e6-90fa-e1da88ef34e9
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment
msc.type: authoredcontent
ms.openlocfilehash: 205a60ee8695f84054bf2139baa3eeb88728d28a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37817767"
---
<a name="configuring-deployment-properties-for-a-target-environment"></a>대상 환경에 대 한 배포 속성 구성
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에는 특정 대상 환경에 샘플 Contact Manager 솔루션을 배포 하기 위해 환경 관련 속성을 구성 하는 방법을 설명 합니다.


이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 솔루션&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.

이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="process-overview"></a>프로세스 개요

Contact Manager 솔루션 빌드 및 배포를 사용 하는 프로젝트 파일은 두 개의 실제 파일로 분할 됩니다.

- Universal를 포함 하는 빌드 설정 및 지침 (합니다 *Publish.proj* 파일).
- 환경별을 포함 하는 빌드 설정 (*Env Dev.proj*를 *Env Stage.proj*등).

빌드 시간에 적절 한 환경 관련 프로젝트 파일은 병합할 범용 *Publish.proj* 빌드 지침의 전체 집합을 형성 하는 파일입니다. 만들거나 사용자 고유의 배포 시나리오를 설명 하는 설정 사용 하 여 환경 관련 프로젝트 파일을 사용자 지정 하 여 특정 대상 환경에 배포를 구성할 수 있습니다.

이러한 값의 많은 대상 환경을 구성 하는 방법에 따라 결정 됩니다&#x2014;대상 웹 서버는 웹 배포 에이전트 서비스 (원격 에이전트) 또는 웹 배포 처리기를 사용 하 여 구성 되어 있는지 여부에 특히 합니다. 이러한 방법에 대 한 자세한 내용은 및 고유한 환경에 대 한 적절 한 방식을 선택에 대 한 지침은 [웹 배포에 오른쪽 접근 방식을 선택](choosing-the-right-approach-to-web-deployment.md)합니다.

합니다 [Contact Manager 시나리오](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md) 두 환경별 프로젝트 파일이 필요 합니다.

- 개발자 테스트 환경에 배포 (*Env Dev.proj*). 개발자 테스트 환경에 설명 된 대로 원격 에이전트를 사용 하 여 원격 배포를 허용 하도록 구성 된 [시나리오: 웹 배포용 테스트 환경 구성](scenario-configuring-a-test-environment-for-web-deployment.md)합니다. 이 파일 연결 문자열에서 서비스 끝점 등의 특정 위치 설정 뿐만 아니라 끝점 주소에 원격 에이전트를 제공 해야 합니다.
- 스테이징 환경에 배포 (*Env Stage.proj*). 스테이징 환경에 설명 된 대로 웹 배포 처리기를 사용 하 여 원격 배포를 허용 하도록 구성 된 [시나리오: 웹 배포용 스테이징 환경 구성](scenario-configuring-a-staging-environment-for-web-deployment.md)합니다. 이 파일 서비스 끝점 및 웹 배포 처리기 끝점 주소 뿐만 아니라 연결 문자열 같은 특정 위치 설정을 제공 해야 합니다.

환경별 프로젝트 파일에서 구성 설정을 자체 웹 패키지의 내용에 영향을 주지 명심 해야 것&#x2014;대신 제어 하는 패키지 배포 방법 및 패키지 때 어떤 매개 변수 값을 제공 합니다. 추출 합니다. 프로덕션 환경에 웹 패키지에 설명 된 대로 수동으로 가져오는 [시나리오: 웹 배포용 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md) 하 고 [수동으로 웹 패키지 설치](../web-deployment-in-the-enterprise/manually-installing-web-packages.md), 설정을 중요 하지 않습니다 사용한 환경 관련 프로젝트 파일에서 패키지를 생성 하는 경우. 인터넷 정보 서비스 (IIS) 관리자 묻는 연결 문자열 및 서비스 끝점에서 모든 매개 변수가 있는 값에 대 한 패키지를 가져올 때입니다.

Contact Manager 솔루션에 고유한 대상 환경에 배포 하려면 하거나이 파일을 사용자 지정 또는 템플릿으로 사용할를 사용자 고유의 파일을 만듭니다.

**Contact Manager 솔루션에 대 한 환경 관련 배포 설정을 구성 하려면**

1. Visual Studio 2010에서 ContactManager WCF 솔루션을 엽니다.
2. 에 **솔루션 탐색기** 창 확장를 **게시** 폴더를 확장 합니다 **EnvConfig** 폴더를 마우스 두 번 클릭 **Env-Dev.proj**.

    ![](configuring-deployment-properties-for-a-target-environment/_static/image1.png)
3. 속성 값을 대체 합니다 *Env Dev.proj* 자신의 테스트 환경에 대 한 올바른 값을 사용 하 여 파일입니다.

    > [!NOTE]
    > 이 절차 뒤에 나오는 표에서 이러한 각 속성에 자세한 정보를 제공 합니다.
4. 작업을 저장 한 다음 닫습니다 합니다 *Env Dev.proj* 파일입니다.

## <a name="choosing-the-right-deployment-properties"></a>올바른 배포 속성을 선택합니다.

샘플 환경 관련 프로젝트 파일의 각 속성의 용도 설명 하는이 테이블 *Env Dev.proj*를 제공 해야 하는 값에 몇 가지 지침을 제공 합니다.


|                                                        속성 이름                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              <strong>MSDeployComputerName</strong> 대상 웹 서버 또는 서비스 끝점의 이름입니다.               |                                                                                                                                                                                                                                              대상 웹 서버에서 원격 에이전트 서비스를 배포 하는 경우 대상 컴퓨터 이름을 지정할 수 있습니다 (예를 들어 <strong>TESTWEB1</strong> 하거나 <strong>TESTWEB1.fabrikam.net</strong>), 원격을 지정할 수 있습니다 에이전트 끝점 (예를 들어 `http://TESTWEB1/MSDEPLOYAGENTSERVICE`). 배포는 각각의 경우에서 동일한 방식으로 작동합니다. 서비스 끝점을 지정 하 고 쿼리 문자열 매개 변수로 IIS 웹 사이트의 이름을 포함 해야 대상 웹 서버에서 웹 배포 처리기를 배포 하는 경우 (예를 들어 `https://STAGEWEB1:8172/MSDeploy.axd?site=DemoSite`).                                                                                                                                                                                                                                              |
|         <strong>MSDeployAuth</strong> 웹 배포에서 원격 컴퓨터에 인증 하는 데 사용 해야 하는 메서드.          |                                                                                                                                                                                                                          이 설정 해야 <strong>NTLM</strong> 하거나 <strong>기본</strong>입니다. 일반적으로 사용 하 여 <strong>NTLM</strong> 원격 에이전트 서비스를 배포 하는 경우와 <strong>기본</strong> 웹 배포 처리기를 배포 하는 경우. 기본 인증을 사용 하는 경우 또한 사용자 이름 및 배포를 수행 하기 위해 IIS 웹 배포 도구 (웹 배포)를 가장 해야 하는 암호를 지정 해야 합니다. 이 예제에서는 이러한 값을 통해 제공 합니다 <strong>MSDeployUsername</strong> 하 고 <strong>MSDeployPassword</strong> 속성입니다. NTLM 인증을 사용 하는 경우에 이러한 속성을 생략 하거나 빈 그대로 수 있습니다.                                                                                                                                                                                                                          |
| <strong>MSDeployUsername</strong> 웹 배포 기본 인증을 사용 하는 경우이 계정은 원격 컴퓨터에서 사용 됩니다.  |                                                                                                                                                                                                                                                                                                                                                                                                                       이 형식 이어야 <em>도메인</em>\*username * (예를 들어 <strong>FABRIKAM\matt</strong>). 기본 인증을 지정 하는 경우에이 값이 사용 됩니다. NTLM 인증을 사용 하는 경우에 속성을 생략할 수 있습니다. 값을 제공 하는 경우 무시 됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                        |
| <strong>MSDeployPassword</strong> 웹 배포 기본 인증을 사용 하는 경우이 암호 원격 컴퓨터에서 사용 됩니다. |                                                                                                                                                                                                                                                                                                                                                                                                                    지정한 사용자 계정의 암호를 <strong>MSDeployUsername</strong> 속성입니다. 기본 인증을 지정 하는 경우에이 값이 사용 됩니다. NTLM 인증을 사용 하는 경우에 속성을 생략할 수 있습니다. 값을 제공 하는 경우 무시 됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                    |
|     <strong>ContactManagerIisPath</strong> Contact Manager MVC 응용 프로그램을 배포 하려는 IIS 경로입니다.     |                                                                                                                                                                                                                                                                                                                                                                        IIS 관리자에서 폼에 표시 되는 경로 여야 합니다 [<em>IIS 웹 사이트 이름</em>] / [<em>web</em><em>응용 프로그램 이름</em>]. IIS 웹 사이트 응용 프로그램을 배포 하기 전에 존재 해야 함을 기억 합니다. 예를 들어 DemoSite 라는 IIS 웹 사이트를 만든 경우 DemoSite/ContactManager로 MVC 응용 프로그램에 대 한 IIS 경로 지정할 수 있습니다.                                                                                                                                                                                                                                                                                                                                                                        |
|   <strong>ContactManagerServiceIisPath</strong> Contact Manager WCF 서비스를 배포 하려는 IIS 경로입니다.    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                          예를 들어 DemoSite 라는 IIS 웹 사이트를 만든 경우 WCF 서비스 IIS 경로도 지정할 수 <strong>DemoSite/ContactManagerService</strong>합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                  <strong>ContactManagerTargetUrl</strong> URL는 WCF 서비스에 연결할 수 있습니다.                   |                                                                                                                                                     폼 이렇게 [<em>IIS 웹 사이트 루트 URL</em>] / [<em>서비스 응용 프로그램 이름</em>] / [<em>끝점이</em>]. 예를 들어 포트 85에서 IIS 웹 사이트를 만든 경우 URL은 형태가 `http://localhost:85/ContactManagerService/ContactService.svc`합니다. MVC 응용 프로그램 및 WCF 서비스를 동일한 서버에 배포 해야 합니다. 결과적으로이 URL만 설치 된 컴퓨터에서 액세스 합니다. 이 때문에 URL의 localhost IP 주소 대신 컴퓨터 이름 또는 호스트 헤더를 사용 하는 것이 좋습니다. 컴퓨터 이름 또는 호스트 헤더를 사용 하는 경우는 [루프백 확인](https://go.microsoft.com/?linkid=9805131) IIS의 보안 기능 URL을 차단 하 고 반환할 수 있습니다는 <strong>HTTP 401.1-권한이 없음</strong> 오류입니다.                                                                                                                                                     |
|                  <strong>CmDatabaseConnectionString</strong> 데이터베이스 서버에 대 한 연결 문자열입니다.                  | 연결 문자열 모두 자격 증명이 VSDBCMD 데이터베이스 서버에 연결할 데이터베이스를 만들고 웹 서버 응용 프로그램 풀 하는 데이터베이스 서버 및 데이터베이스와 상호 작용 하는 데 사용할 자격 증명을 사용할지를 결정 합니다. 기본적으로 두 가지 옵션이 있습니다 여기 있습니다. 지정할 수 있습니다 <strong>Integrated Security = true</strong>, 통합된 Windows 인증을 사용 하는 경우: <strong>데이터 원본 TESTDB1; = Integrated Security = true</strong> 이 경우 데이터베이스를 사용 하 여 만들어집니다 실행 파일, VSDBCMD를 실행 하는 사용자 및 응용 프로그램의 자격 증명을 웹 서버 컴퓨터 계정의 id를 사용 하 여 데이터베이스에 액세스 합니다. 또는 사용자 이름 및 SQL Server 계정의 암호를 지정할 수 있습니다. 이 경우 SQL Server 자격 증명 되는 데이터베이스와 상호 작용 하는 응용 프로그램 풀 및 데이터베이스를 만들려고 VSDBCMD가 모두: <strong>데이터 원본 = TESTDB1; 사용자 Id = ASqlUser; 암호 = Pa$$w0rd</strong> 이 항목의 연습에서는 통합된 Windows 인증 사용 하는 것을 가정 합니다. |
|        <strong>CmTargetDatabase</strong> 을 데이터베이스 서버에서 만든 데이터베이스에 지정할 이름입니다.        |                                                                                                                                                                                                                                                                                                                                                                                                                                                     여기에 제공 하는 값은 매개 변수로 VSDBCMD 명령에 추가 됩니다. 또한 웹 서버의 응용 프로그램 풀의 데이터베이스와 상호 작용 하는 데 사용할 수 있는 전체 연결 문자열을 작성 하는 것이 됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

이러한 예제는 특정 배포 시나리오에 대 한 이러한 속성을 구성할 수 있습니다 하는 방법을 보여 줍니다.

### <a name="example-1x2014deployment-to-the-remote-agent-service"></a>예제 1&#x2014;원격 에이전트 서비스에 배포

이 예제에 대한 설명:

- TESTWEB1에서 원격 에이전트 서비스를 배포 하는 합니다.
- NTLM 인증을 사용 하려면 웹 배포 하도록 합니다. 웹 배포는 Microsoft Build Engine (MSBuild)을 호출 하는 데 자격 증명을 사용 하 여 실행 됩니다.
- 통합된 인증을 사용 하는 배포 하는 **ContactManager** 데이터베이스 TESTDB1 합니다. 데이터베이스는 MSBuild를 호출 하는 데 자격 증명을 사용 하 여 배포 됩니다.


[!code-xml[Main](configuring-deployment-properties-for-a-target-environment/samples/sample1.xml)]


### <a name="example-2x2014deployment-to-the-web-deploy-handler-endpoint"></a>예제 2&#x2014;웹 배포 처리기 끝점 배포

이 예제에 대한 설명:

- 웹 배포 처리기 서비스 끝점 STAGEWEB1에 배포 하는 합니다.
- 웹 배포를 기본 인증을 사용 하도록 합니다.
- 웹 배포 원격 컴퓨터의 FABRIKAM\stagingdeployer 계정을 가장 해야 하는 지정 하는 합니다.
- SQL Server 인증을 사용 하는 배포 하는 **ContactManager** STAGEDB1 데이터베이스입니다.


[!code-xml[Main](configuring-deployment-properties-for-a-target-environment/samples/sample2.xml)]


## <a name="conclusion"></a>결론

이 시점에서 프로젝트 파일을 빌드하고 Contact Manager 솔루션 하나 이상의 대상 환경에 배포할 구성 완벽 하 게 됩니다.

단일 단계 및 반복 가능한 배포 프로세스의 일부로 이러한 프로젝트 파일을 사용 하려면 실행 해야 합니다 *Publish.proj* MSBuild를 사용 하 여 파일 및 환경 관련 프로젝트 파일의 위치를 매개 변수로 전달 합니다. 다양 한 방법으로이 수행할 수 있습니다.

- 사용자 지정 프로젝트 파일에 대 한 소개와 MSBuild의 개요를 보려면 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다.
- 사용자 지정 프로젝트 파일을 실행 하는 MSBuild 명령을 작성 하는 방법에 대 한 자세한 내용은 [웹 배포 패키지](../web-deployment-in-the-enterprise/deploying-web-packages.md)합니다.
- 단일 단계 및 반복 가능한 배포에 대 한 명령 파일에 MSBuild 명령을 통합 하는 방법에 대 한 자세한 내용은 [만들기 및 배포 명령 파일을 실행](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)합니다.
- Team Build에서 사용자 지정 프로젝트 파일을 실행 하는 방법에 대 한 자세한 내용은 [는 지원 배포 빌드 정의 만들려면](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)합니다.

> [!div class="step-by-step"]
> [이전](creating-a-server-farm-with-the-web-farm-framework.md)
