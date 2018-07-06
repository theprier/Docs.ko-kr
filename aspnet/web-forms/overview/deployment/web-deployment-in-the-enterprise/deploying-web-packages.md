---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
title: 웹 패키지 배포 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹...를 사용 하 여 원격 서버에 웹 배포 패키지를 게시할 수는 방법에 대해 설명 합니다.
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: a5c5eed2-8683-40a5-a2e1-35c9f8d17c29
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
msc.type: authoredcontent
ms.openlocfilehash: 44c3772263cbebaf03e1393542fda32467a97cd8
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825267"
---
<a name="deploying-web-packages"></a>웹 패키지 배포
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 원격 서버에 웹 배포 패키지를 게시할 수는 방법에 대해 설명 합니다. 2.0.
> 
> 두 가지 주요는 원격 서버에 웹 패키지를 배포할 수 있습니다.
> 
> - MSDeploy.exe 명령줄 유틸리티를 직접 사용할 수 있습니다.
> - 실행할 수 있습니다 합니다 *[프로젝트 이름].deploy.cmd* 빌드 프로세스를 생성 하는 파일입니다.
> 
> 최종 결과 사용 하는 방법에 관계 없이 동일 합니다. 기본적으로 모든 합니다 *. deploy.cmd* 파일이 없습니다. 패키지를 배포 하기 위해 많은 정보를 제공 하지 않아도 되도록 일부 미리 결정 된 값을 사용 하 여 MSDeploy.exe를 실행 하는 것입니다. 이 배포 프로세스를 간소화 합니다. 반면에 MSDeploy.exe를 직접 사용 하 여 융통성 있게 많은 패키지 배포 되는 방식을 정확히 위에 있습니다.
> 
> 어떤 방법을 사용 하면 다양 한 요인에 따라 달라 집니다 얼마나 많이 제어 비롯 하 여 배포 프로세스를 통해 필요한 및 웹 배포 원격 에이전트 서비스 또는 웹 배포 처리기를 대상으로 하는지 여부입니다. 이 항목에서는 각 방법을 사용 하는 방법에 설명 하 고 적합 한 각 방법을 식별 합니다.
> 
> 작업은이 문서의 연습 있다고 가정 합니다.
> 
> - 에 설명 된 대로 웹 응용 프로그램 패키지를 빌드하고 했으므로 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.
> - 수정한 합니다 *SetParameters.xml* 에 설명 된 대로 대상 환경의 오른쪽 매개 변수 값을 제공 하는 파일 [웹 패키지 배포용 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)합니다.


실행 되는 [*프로젝트 이름*]*. deploy.cmd* 파일이 웹 패키지를 배포 하는 가장 간단한 방법은 합니다. 특히 사용 하는 *. deploy.cmd* 파일 MSDeploy.exe를 직접 사용 하는 동안 다음과 같은이 이점을 제공:

- 웹 배포 패키지의 위치를 지정할 필요가 없습니다&#x2014;는 *. deploy.cmd* 파일 위치를 알고 있다면 합니다.
- 위치를 지정할 필요가 없습니다 합니다 *SetParameters.xml* 파일&#x2014;합니다 *. deploy.cmd* 파일 위치를 알고 있다면 합니다.
- 원본 및 대상 MSDeploy 공급자를 지정할 필요가 없습니다&#x2014;는 *. deploy.cmd* 파일을 이미 알고 있는 값을 사용 합니다.
- MSDeploy 작업 설정을 지정할 필요가 없습니다&#x2014;는 *. deploy.cmd* 파일 MSDeploy.exe 명령에 자동으로 일반적으로 필요한 값을 추가 합니다.

사용 하기 전에 합니다 *. deploy.cmd* 웹 패키지를 배포 하는 파일 인지 확인 해야 합니다.

- 합니다 *. deploy.cmd* 파일을 [*프로젝트 이름*]. *SetParameters.xml* 파일 및 웹 패키지 ([*프로젝트 이름*]. *zip*) 같은 폴더에 있습니다.
- 웹 배포 (MSDeploy.exe)를 실행 하는 컴퓨터에 설치 되는 *. deploy.cmd* 파일입니다.

합니다 *. deploy.cmd* 파일은 다양 한 명령줄 옵션을 지원 합니다. 명령 프롬프트에서 파일을 실행 하는 경우이 기본 구문은 다음과 같습니다.


[!code-console[Main](deploying-web-packages/samples/sample1.cmd)]


중 하나를 지정 해야 합니다는 **/T** 플래그 또는 **/Y** 각각 평가판 실행 또는 라이브 배포를 수행할 것인지 여부를 나타내는 플래그 (동일한 명령에 두 플래그를 사용 안 함). 이 표에서 이러한 플래그는 각각의 용도 설명합니다.

| 플래그 | 설명 |
| --- | --- |
| **/T** | 사용 하 여 MSDeploy.exe를 호출 합니다 **– whatif** 평가판 실행을 나타내는 플래그를 합니다. 패키지를 배포 하는 대신 패키지를 배포할 않았습니다 않는다면 어떤 상황이 대 한 보고서를 만듭니다. |
| **/Y** | 없이 MSDeploy.exe를 호출 합니다 **– whatif** 플래그입니다. 이 로컬 컴퓨터 또는 지정 된 대상 서버에 패키지를 배포합니다. |
| **/M** | 대상 서버를 지정 합니다. 이름을 지정 하거나 서비스 URL입니다. 여기에 제공 하는 값에 대 한 자세한 내용은 참조는 **끝점 고려 사항** 섹션을이 참조 합니다. 생략 하면 합니다 **/M** 패키지 플래그를 로컬 컴퓨터에 배포 됩니다. |
| **/A** | MSDeploy.exe를 배포 하는 데 사용 해야 하는 인증 유형을 지정 합니다. 가능한 값은 **NTLM** 하 고 **기본**입니다. 생략 하면 합니다 **/A** 인증 형식의 기본값은 플래그 **NTLM** 웹 배포 원격 에이전트 서비스를 배포에 대 한 **기본** 웹 배포에 배포 처리기입니다. |
| **/U** | 사용자 이름을 지정합니다. 기본 인증을 사용 하는 경우에 적용 됩니다. |
| **/P** | 암호를 지정합니다. 기본 인증을 사용 하는 경우에 적용 됩니다. |
| **/L** | 로컬 IIS Express 인스턴스에 패키지를 배포 해야 나타냅니다. |
| **/G** | 패키지를 사용 하 여 배포 된 지정 된 [tempAgent 공급자 설정을](https://technet.microsoft.com/library/ee517345(WS.10).aspx)합니다. 생략 하면 합니다 **/G** 플래그를 기본값인 **false**합니다. |

> [!NOTE]
> 또한 라는 파일이 생성 될 때마다 웹 패키지를 만드는 빌드 프로세스를 *[프로젝트 이름].deploy readme.txt* 는 이러한 배포 옵션에 설명 합니다.


이러한 플래그 외에도 웹 배포 작업 설정 추가으로 지정할 수 있습니다 *. deploy.cmd* 매개 변수입니다. 추가 설정은 지정 하는 단순히 기본 MSDeploy.exe 명령은를 통해 전달 됩니다. 이러한 설정에 대 한 자세한 내용은 참조 하세요. [웹 배포 작업 설정](https://technet.microsoft.com/library/dd569089(WS.10).aspx)합니다.

ContactManager.Mvc 웹 응용 프로그램 프로젝트를 실행 하 여 테스트 환경에 배포 하기를 원한다고 가정 합니다 *. deploy.cmd* 파일입니다. 에 설명 된 대로 웹 배포 원격 에이전트 서비스를 사용 하 여 테스트 환경이 구성 된 [웹 배포 게시 (원격 에이전트)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)합니다. 웹 응용 프로그램을 배포 하려면 다음 단계를 완료 해야 합니다.

**사용 하 여 웹 응용 프로그램을 배포 하는. deploy.cmd 파일**

1. 빌드 및에 설명 된 대로 웹 응용 프로그램 프로젝트를 패키지 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.
2. 수정 된 *ContactManager.Mvc.SetParameters.xml* 에 설명 된 대로 테스트 환경에 대 한 올바른 매개 변수 값을 포함 하는 파일 [웹 패키지 배포용 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)합니다.
3. 명령 프롬프트 창을 열고의 위치로 이동 합니다 *ContactManager.Mvc.deploy.cmd* 파일입니다.
4. 이 명령을 입력 한 다음 Enter를 누릅니다.

    [!code-console[Main](deploying-web-packages/samples/sample2.cmd)]

이 예제에 대한 설명:

- 합니다 **/Y** 플래그 나타냅니다는 실제로 패키지를 배포 하려는 것이 아니라 실행 평가판을 수행 합니다.
- 합니다 **/M** 플래그 TESTWEB1 이라는 서버에 패키지를 배포할 것인지를 나타냅니다. 이 값에서 원격 에이전트 웹 배포에서 서비스에 패키지를 배포 하려면 MSDeploy.exe 시도가 http://TESTWEB1/MSDeployAgentService합니다.
- 합니다 **/A** NTLM 인증을 사용 하려는 플래그를 나타냅니다. 따라서 사용자 이름과 암호를 지정할 필요가 없습니다.

설명 하기 위해 어떻게 사용 하 여 합니다 *. deploy.cmd* 배포 프로세스를 간소화 하는 파일, 생성 및 실행 하는 경우 실행 가져옵니다 MSDeploy.exe 명령은 살펴보겠습니다 *ContactManager.Mvc.deploy.cmd* 위에 표시 된 옵션을 사용 합니다.


[!code-console[Main](deploying-web-packages/samples/sample3.cmd)]


사용 하 여 대 한 자세한 내용은 합니다 *. deploy.cmd* 내용은 웹 패키지를 배포 하는 파일 [방법:는 배포 패키지를 사용 하 여 deploy.cmd 파일을 설치](https://msdn.microsoft.com/library/ff356104.aspx).

## <a name="using-msdeployexe"></a>MSDeploy.exe를 사용 하 여

사용 된 *. deploy.cmd* 파일은 일반적으로 배포 프로세스를 간소화, 경우에 일부 MSDeploy.exe를 직접 사용 하는 것이 좋습니다. 예를 들어:

- 관리자가 아닌 사용자로 웹 배포 처리기에 배포 하려는 경우 사용할 수 없습니다는 *. deploy.cmd* 파일입니다. 아래 설명 된 대로 웹 배포 2.0의 버그 때문에 이것이 **끝점 고려 사항**합니다.
- 수동으로 다른 사이 전환 하려는 경우 *SetParameters.xml* 서로 다른 위치에 파일을 좋습니다 MSDeploy.exe를 직접 사용 합니다.
- 몇 개의 MSDeploy.exe 명령줄 인수를 재정의 하려는 경우에 MSDeploy.exe를 직접 사용 하는 것이 좋습니다.

MSDeploy.exe를 사용 하는 경우에 세 가지 중요 정보를 제공 해야 합니다.

- A **-원본** 데이터에서 제공 되는 위치를 나타내는 매개 변수입니다.
- A **– dest** 데이터 하려는 위치를 나타내는 매개 변수입니다.
- A **– 동사** 나타내는 매개 변수를 [작업](https://technet.microsoft.com/library/dd568989(WS.10).aspx) 수행 하려는 합니다.

MSDeploy.exe 의존 [웹 배포 공급자](https://technet.microsoft.com/library/dd569040(WS.10).aspx) 원본 및 대상 데이터를 처리 하 합니다. 웹 배포 공급자에서 작동 하는 응용 프로그램 및 데이터 원본의 범위를 나타내는 많이 포함&#x2014;예를 들어, SQL Server 데이터베이스, IIS 웹 서버, 인증서, 전역 어셈블리 캐시 (GAC) 어셈블리에 대 한 공급자가 다양 한 다른 구성 파일 및 많은 다른 유형의 데이터입니다. 모두를 **– 원본** 매개 변수 및 **– dest** 매개 변수 형식에서 공급자를 지정 해야 **– 원본**: [*providerName*] [=*위치*]. 웹 패키지를 IIS 웹 사이트에 배포 하는 경우에 이러한 값을 사용 하면 됩니다.

- 합니다 **-원본** 공급자는 항상 [패키지](https://technet.microsoft.com/library/dd569019(WS.10).aspx)합니다. 예를 들어:

    [!code-console[Main](deploying-web-packages/samples/sample4.cmd)]
- 합니다 **– dest** 공급자는 항상 [자동](https://technet.microsoft.com/library/dd569016(WS.10).aspx)합니다. 예를 들어:

    [!code-console[Main](deploying-web-packages/samples/sample5.cmd)]
- 합니다 **– 동사** 은 항상 **동기화**합니다.

    [!code-console[Main](deploying-web-packages/samples/sample6.cmd)]

또한 해야 지정 하는 다양 한 다른 [공급자별 설정](https://technet.microsoft.com/library/dd569001(WS.10).aspx) 일반적인 [작업 설정을](https://technet.microsoft.com/library/dd569089(WS.10).aspx)합니다. 예를 들어, 스테이징 환경에 ContactManager.Mvc 웹 응용 프로그램을 배포 한다고 가정 합니다. 배포를 대상으로 웹 배포 처리기 및 기본 인증을 사용 해야 합니다. 웹 응용 프로그램을 배포 하려면 다음 단계를 완료 해야 합니다.

**MSDeploy.exe를 사용 하 여 웹 응용 프로그램을 배포 하려면**

1. 빌드 및에 설명 된 대로 웹 응용 프로그램 프로젝트를 패키지 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.
2. 수정 된 *ContactManager.Mvc.SetParameters.xml* 에 설명 된 대로, 스테이징 환경에 대 한 올바른 매개 변수 값을 포함 하는 파일 [웹 패키지 배포용 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)합니다.
3. 명령 프롬프트 창을 열고 MSDeploy.exe의 위치로 이동 합니다. 이 일반적으로 웹 배포 V2\msdeploy.exe %PROGRAMFILES%\IIS\Microsoft에서.
4. 이 명령을 입력 한 다음 Enter를 누릅니다 (줄 바꿈은 무시).

    [!code-console[Main](deploying-web-packages/samples/sample7.cmd)]

이 예제에 대한 설명:

- 합니다 **– 원본** 매개 변수를 지정 합니다 **패키지** 공급자 웹 패키지의 위치를 나타냅니다.
- 합니다 **– dest** 매개 변수를 지정 합니다 **자동** 공급자입니다. 합니다 **computerName** 설정을 대상 서버에서 웹 배포 처리기의 서비스 URL을 제공 합니다. 합니다 **authtype** 설정 되었음을 나타내고 기본 인증을 사용 하려는 제공 해야 하는 같이 **username** 및 **암호**합니다. 마지막으로, 합니다 **includeAcls = "False"** 설정은 대상 서버로 소스 웹 응용 프로그램에서 파일의 액세스 제어 목록 (Acl)을 복사 하려는 없습니다 나타냅니다.
- 합니다 **– 동사: 동기화** 인수 대상 서버에서 원본 콘텐츠를 복제할 것인지를 나타냅니다.
- 합니다 **-disableLink** 인수 응용 프로그램 풀, 가상 디렉터리 구성 또는 대상 서버에서 Secure Sockets Layer (SSL) 인증서를 복제 하려는 없습니다 나타냅니다. 자세한 내용은 [링크 확장을 배포 하는 웹](https://technet.microsoft.com/library/dd569028(WS.10).aspx)합니다.
- 합니다 **– setParamFile** 매개 변수 위치를 제공 합니다 *SetParameters.xml* 파일.
- 합니다 **– allowUntrusted** 스위치 나타냅니다 웹 배포 하지는 신뢰할 수 있는 인증 기관에서 발급 된 SSL 인증서 수락 해야 합니다. 웹 배포 처리기에 배포 하는 서비스 URL을 보호 하는 자체 서명 된 인증서를 사용한 경우이 스위치를 포함 해야 합니다.

## <a name="automating-web-package-deployment"></a>웹 패키지 배포 자동화

엔터프라이즈 시나리오 많은, 더 큰 단일 단계 또는 자동화 된 배포의 일부로 웹 패키지를 배포 합니다. 웹 패키지를 실행 하 여 배포 하도록 선택 했는지 여부에 관계 없이 합니다 *. deploy.cmd* 파일 또는 MSDeploy.exe를 직접 사용 하 여 명령을 매개 변수화 하는 Microsoft Build Engine (MSBuild) 대상에서 호출 프로젝트 파일입니다.

Contact Manager 샘플 솔루션에 살펴보겠습니다 합니다 **PublishWebPackages** 에서 대상으로 지정 합니다 *Publish.proj* 파일. 이 대상 마다 한 번 실행 *. deploy.cmd* 이라는 항목 목록에서 식별 된 파일 **PublishPackages**합니다. 대상 속성 및 항목 메타 데이터를 사용 하 여 각각에 대 한 인수 값의 전체 집합을 작성 하 *. deploy.cmd* 파일을 선택한 다음 사용 합니다 **Exec** 명령을 실행 하는 작업입니다.


[!code-xml[Main](deploying-web-packages/samples/sample8.xml)]


> [!NOTE]
> 일반적으로 사용자 지정 프로젝트 파일에 대 한 소개와 샘플 솔루션에서 프로젝트 파일 모델의 광범위 한 개요를 참조 하세요 [프로젝트 파일 이해](understanding-the-project-file.md) 하 고 [빌드 프로세스를 이해](understanding-the-build-process.md)합니다.


## <a name="endpoint-considerations"></a>끝점 고려 사항

웹 패키지를 실행 하 여 배포 되는 여부에 관계 없이 합니다 *. deploy.cmd* 파일 또는 MSDeploy.exe를 직접 사용 하 여 컴퓨터 이름 또는 배포에 대 한 서비스 끝점을 지정 해야 합니다.

대상 웹 서버는 웹 배포 원격 에이전트 서비스를 사용 하 여 배포, 구성 된 경우 대상으로 대상 서비스 URL을 지정 합니다.


[!code-console[Main](deploying-web-packages/samples/sample9.cmd)]


또는 서버 이름만 대상으로 지정할 수 있습니다 하 고 웹 배포에 원격 에이전트 서비스 URL을 유추 합니다.


[!code-console[Main](deploying-web-packages/samples/sample10.cmd)]


대상 웹 서버는 웹 배포 처리기를 사용 하 여 배포, 구성 된 경우에 IIS 웹 관리 서비스 (WMSvc)의 끝점 주소를 대상으로 지정 해야 합니다. 기본적으로이 형식을 사용 합니다.


[!code-console[Main](deploying-web-packages/samples/sample11.cmd)]


대상 중 하나를 사용 하 여 이러한 끝점 중 하나는 *. deploy.cmd* 파일 또는 MSDeploy.exe 직접. 그러나에 설명 된 대로 관리자가 아닌 사용자로 웹 배포 처리기에 배포 하려는 경우 [웹 배포 게시 (웹 배포 처리기)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md), 서비스 끝점 주소에 대 한 쿼리 문자열을 추가 해야 합니다.


[!code-console[Main](deploying-web-packages/samples/sample12.cmd)]


관리자가 아닌 사용자에 게 IIS;에 대 한 서버 수준 액세스 이므로 자신이 특정 IIS 웹 사이트에 액세스할 수 있습니다. 웹 게시 파이프라인 (WPP), 버그로 인해 작성 시 실행할 수 없습니다는 *. deploy.cmd* 쿼리 문자열을 포함 하는 끝점 주소를 사용 하는 파일입니다. 이 시나리오에서는 MSDeploy.exe를 직접 사용 하 여 웹 패키지를 배포 해야 합니다.

> [!NOTE]
> 웹 배포 원격 에이전트 서비스 및 웹 배포 처리기에 대 한 자세한 내용은 참조 하세요. [웹 배포에 오른쪽 접근 방식을 선택](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)합니다. 이러한 끝점을 배포 하려면 환경 관련 프로젝트 파일을 구성 하는 방법에 대 한 지침을 참조 하세요 [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)합니다.


## <a name="authentication-considerations"></a>인증 고려 사항

웹 패키지를 실행 하 여 배포 되는 여부에 관계 없이 합니다 *. deploy.cmd* 파일 또는 MSDeploy.exe를 직접 사용 하 여 인증 형식을 지정 해야 합니다. 두 개의 가능한 값을 허용 하는 웹 배포: **NTLM** 하거나 **기본**입니다. 기본 인증을 지정 하는 경우 또한 사용자 이름 및 암호를 제공 해야 합니다. 가지 인증 유형을 선택 하는 경우 주의 해야 하는 다양 한 요인이 있습니다.

- 웹 배포 원격 에이전트 서비스를 배포 하는 경우 NTLM 인증을 사용 해야 합니다. 원격 에이전트 서비스를 기본 인증 자격 증명을 허용 하지 않습니다.
- 웹 배포 처리기를 배포 하는 경우에 NTLM 또는 기본 인증을 사용할 수 있습니다. 기본값은 기본 인증입니다. 기본 인증은 사용자 이름과 암호를 일반 텍스트로 전송를 사용 하지만 자격 증명으로 보호 하는 웹 배포 처리기를 항상 SSL 암호화를 사용 합니다.
- 웹 패키지 데이터베이스를 포함 하는 경우 웹 서버와 데이터베이스 서버를 별도 컴퓨터에로 인해 NTLM 인증을 사용 하 여 데이터베이스를 배포할 수 없습니다는 [NTLM "이중 홉" 제한](https://go.microsoft.com/?linkid=9805120)합니다. 배포 연결 문자열에 SQL Server 자격 증명을 사용 하거나 웹 배포를 기본 인증 자격 증명을 제공 해야 합니다. 이 문제에 자세히 설명 되어 [엔터프라이즈 환경에 멤버 자격 데이터베이스 배포](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)합니다.

## <a name="conclusion"></a>결론

이 항목에서는 배포 하는 방법을 웹 패키지를 실행 하 여 하나를 설명 합니다 *. deploy.cmd* 파일 또는 MSDeploy.exe를 직접 사용 하 여 합니다. 각 접근 방식은 적합할 시점과 매개 변수화 대규모 단일 단계 또는 자동화 된 빌드 프로세스의 일부로 배포 명령을 실행 하는 방법 설명 설명 했습니다.

## <a name="further-reading"></a>추가 정보

만들기 및 웹 배포 패키지를 매개 변수화 하는 방법에 대 한 지침을 참조 하세요 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md) 하 고 [웹 패키지 배포용 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)합니다. 빌드 및 Team Foundation Server (TFS) 인스턴스에서 웹 패키지를 배포 하는 방법에 대 한 지침을 참조 하세요 [자동화 된 웹 배포용 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다. 사용자 지정 및 배포 프로세스의 문제를 해결 하는 방법에 대 한 자세한 내용은 [배포에서 제외 하 고 파일 및 폴더](../advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment.md)합니다.

> [!div class="step-by-step"]
> [이전](configuring-parameters-for-web-package-deployment.md)
> [다음](deploying-database-projects.md)
