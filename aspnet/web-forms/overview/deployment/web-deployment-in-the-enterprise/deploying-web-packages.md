---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
title: "웹 패키지 배포 | Microsoft Docs"
author: jrjlee
description: "이 항목에서는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹...를 사용 하 여 원격 서버에 웹 배포 패키지를 게시할 수는 어떻게 설명"
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: a5c5eed2-8683-40a5-a2e1-35c9f8d17c29
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
msc.type: authoredcontent
ms.openlocfilehash: cd2bfa07262155b68ac4605fc7e9748d276d3193
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="deploying-web-packages"></a>웹 패키지 배포
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 원격 서버에 웹 배포 패키지를 게시할 수는 어떻게 설명 2.0.
> 
> 원격 서버에 웹 패키지를 배포할 수 있는 다음 두 가지가 있습니다.
> 
> - MSDeploy.exe 명령줄 유틸리티를 직접 사용할 수 있습니다.
> - 실행할 수는 *[프로젝트 이름].deploy.cmd* 빌드 프로세스에서 생성 하는 파일입니다.
> 
> 최종 결과 사용 방법에 관계 없이 같습니다. 기본적으로, 모든는 *. deploy.cmd* 파일이 없습니다. 패키지를 배포 하는 데 많은 정보를 제공 하지 않아도 되도록 일부 미리 결정 된 값이 있는 MSDeploy.exe를 실행 하는 것입니다. 배포 프로세스를 간소화 합니다. 반면에 MSDeploy.exe를 직접 사용 하 여 제공 더 많은 유연성을 통해 패키지의 배포 방법을 정확 하 게 합니다.
> 
> 사용 하는 방법 다양 한 요인에 따라 달라 집니다 어느 정도 제어할 비롯 하 여 배포 프로세스를 통해 필요한 및 웹 배포 원격 에이전트 서비스 또는 웹 배포 처리기 대상으로 하 여부입니다. 이 항목에서는 각 접근 방식을 사용 하는 방법에 설명 하 고 각 접근 방식은 식별 합니다.
> 
> 작업 및이 항목의 연습 하는 가정합니다.
> 
> - 작성 되었으며에 설명 된 대로 웹 응용 프로그램 패키지 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.
> - 수정한는 *SetParameters.xml* 파일에 설명 된 대로 대상 환경에 대 한 올바른 매개 변수 값을 제공 하도록 [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)합니다.


실행 되는 [*프로젝트 이름*]*. deploy.cmd* 파일은 웹 패키지를 배포 하는 가장 간단한 방법입니다. 특히 사용 하 여는 *. deploy.cmd* 파일 MSDeploy.exe를 직접 사용 하 여에 비해 이러한 이점을 제공 합니다.

- 웹 배포 패키지 & #x 2014;의 위치를 지정할 필요가 없습니다는 *. deploy.cmd* 파일이 이미 알고 있습니다.
- 위치를 지정할 필요가 없습니다는 *SetParameters.xml* 파일 & #x 2014;는 *. deploy.cmd* 파일이 이미 알고 있습니다.
- 원본 및 대상 MSDeploy 공급자 & #x 2014; 지정할 필요가 없습니다는 *. deploy.cmd* 파일을 이미 알고 있는 값을 사용 합니다.
- MSDeploy 운영 설정 & #x 2014;를 지정 하지 않아도 *. deploy.cmd* 파일 MSDeploy.exe 명령에 자동으로 일반적으로 필요한 값을 추가 합니다.

사용 하기 전에 *. deploy.cmd* 웹 패키지를 배포 하는 파일 인지 확인 해야 합니다.

- *. deploy.cmd* 파일의 [*프로젝트 이름*]. *SetParameters.xml* 파일과 웹 패키지 ([*프로젝트 이름*]. *zip*) 같은 폴더에 있습니다.
- Web Deploy (MSDeploy.exe) 실행 하는 컴퓨터에 설치 되어는 *. deploy.cmd* 파일입니다.

*. deploy.cmd* 파일은 다양 한 명령줄 옵션을 지원 합니다. 명령 프롬프트에서 파일을 실행 하는 경우 이것은 기본 구문입니다.


[!code-console[Main](deploying-web-packages/samples/sample1.cmd)]


중 하나를 지정 해야 합니다는 **/T** 플래그 또는 **/Y** 한 평가 실행 또는 실시간 배포를 각각 수행 것인지 여부를 나타내는 플래그 (동일한 명령에 두 플래그를 사용 하지 않습니다). 이 표에서 이러한 플래그의 용도 설명합니다.

| 플래그 | 설명 |
| --- | --- |
| **/T** | MSDeploy.exe를 호출는 **– whatif** 평가 실행 있음을 나타내는 플래그입니다. 패키지를 배포 하지 않고 패키지를 배포할 않은 경우의 보고서가 생성 합니다. |
| **/Y** | 없이 MSDeploy.exe를 호출 하 여 **– whatif** 플래그입니다. 이 로컬 컴퓨터 또는 지정 된 대상 서버에 패키지를 배포 합니다. |
| **/M** | 대상 서버를 지정 합니다. 이름을 지정 하거나 서비스 URL입니다. 여기에 제공 하는 값에 대 한 자세한 내용은 참조는 **끝점 고려 사항** 이 항목의 섹션입니다. 생략 하면는 **/M** 패키지 플래그를 로컬 컴퓨터에 배포 됩니다. |
| **/A** | MSDeploy.exe 배포를 수행 하는 데 사용 해야 하는 인증 유형을 지정 합니다. 가능한 값은 **NTLM** 및 **기본**합니다. 생략 하면는 **/A** 인증 유형을 기본적으로 플래그를 **NTLM** 웹 배포 원격 에이전트 서비스 및 배포에 대 한 **기본** 웹 배포 배포 처리기입니다. |
| **/U** | 사용자 이름을 지정합니다. 기본 인증을 사용 하는 경우에 적용 됩니다. |
| **/P** | 암호를 지정합니다. 기본 인증을 사용 하는 경우에 적용 됩니다. |
| **/L** | 로컬 IIS Express 인스턴스에 패키지를 배포 해야 나타냅니다. |
| **/G** | 패키지를 사용 하 여 배포 된 지정 된 [tempAgent 공급자 설정을](https://technet.microsoft.com/library/ee517345(WS.10).aspx)합니다. 생략 하면는 **/G** 플래그를 기본값인 **false**합니다. |

> [!NOTE]
> 명명 된 파일도 만듭니다 빌드 프로세스 웹 패키지를 만들 때마다 *[프로젝트 이름].deploy readme.txt* 하는 이러한 배포 옵션에 설명 합니다.


이러한 플래그 외에도 웹 배포 작업 설정을 추가으로 지정할 수 있습니다 *. deploy.cmd* 매개 변수입니다. 추가 설정은 지정 하면 단순히 기본 MSDeploy.exe 명령에 통과 됩니다. 이러한 설정에 대 한 자세한 내용은 참조 하십시오. [웹 배포 작업이 설정](https://technet.microsoft.com/library/dd569089(WS.10).aspx)합니다.

ContactManager.Mvc 웹 응용 프로그램 프로젝트를 실행 하 여 테스트 환경에 배포 하려는 경우 다음과 같이 *. deploy.cmd* 파일입니다. 에 설명 된 대로 테스트 환경이 웹 배포 원격 에이전트 서비스를 사용 하도록 구성 된 [웹 배포 게시 (원격 에이전트)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)합니다. 웹 응용 프로그램을 배포 하려면 다음 단계를 완료 해야 합니다.

**사용 하 여 웹 응용 프로그램을 배포 하는..deploy.cmd 파일**

1. 빌드하고에 설명 된 대로 웹 응용 프로그램 프로젝트를 패키지 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.
2. 수정 된 *ContactManager.Mvc.SetParameters.xml* 에 설명 된 대로 테스트 환경에 대 한 올바른 매개 변수 값을 포함 하는 파일 [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)합니다.
3. 명령 프롬프트 창을 열고의 위치로 이동 하는 *ContactManager.Mvc.deploy.cmd* 파일입니다.
4. 이 명령을 입력 한 다음 Enter 키를 누릅니다.

    [!code-console[Main](deploying-web-packages/samples/sample2.cmd)]

이 예제에 대한 설명:

- **/Y** 플래그는 실제로 패키지를 배포 하려면 실행 하지 않고 평가판을 수행 하는 나타냅니다.
- **/M** 플래그 TESTWEB1 이라는 서버에 패키지를 배포할 것인지를 나타냅니다. 이 값을 통해 MSDeploy.exe http://TESTWEB1/MSDeployAgentService에 웹 배포 원격 에이전트 서비스에 패키지를 배포 하려고 합니다.
- **/A** 플래그 NTLM 인증을 사용할 것인지를 나타냅니다. 따라서 사용자 이름과 암호를 지정할 필요가 없습니다.

설명 하기 위해 방법을 사용 하 여는 *. deploy.cmd* 배포 프로세스를 간소화 하는 파일, 가져옵니다의 생성 및 실행 하는 경우를 실행 하는 MSDeploy.exe 명령은 살펴보세요 *ContactManager.Mvc.deploy.cmd* 위에 표시 된 옵션을 사용 합니다.


[!code-console[Main](deploying-web-packages/samples/sample3.cmd)]


사용 하 여 대 한 자세한 내용은 *. deploy.cmd* 웹 패키지를 배포, 참조 파일을 [하는 방법: 설치 된 배포 패키지를 사용 하 여 파일 deploy.cmd](https://msdn.microsoft.com/library/ff356104.aspx)합니다.

## <a name="using-msdeployexe"></a>MSDeploy.exe를 사용 하 여

사용 하더라도 *. deploy.cmd* 파일은 일반적으로 배포 프로세스를 간소화, 몇 가지 경우가 있습니다 MSDeploy.exe를 직접 사용 하는 것이 좋습니다. 예:

- 관리자가 아닌 사용자로 웹 배포 처리기를 배포 하려는 경우 사용할 수 없습니다는 *. deploy.cmd* 파일입니다. 아래 설명 된 대로 웹 배포 2.0의 버그 때문에 이것이 **끝점 고려 사항**합니다.
- 수동으로 다른 사이 전환 하려면 *SetParameters.xml* 서로 다른 위치에 파일을 수도 있습니다 MSDeploy.exe를 직접 사용 합니다.
- 여러 MSDeploy.exe 명령줄 인수를 재정의 하려는 경우에 MSDeploy.exe를 직접 사용 하는 것이 좋습니다.

MSDeploy.exe를 사용 하면 세 가지 주요 정보를 제공 해야 합니다.

- A **– 소스** 데이터에서 온 것인지를 나타내는 매개 변수입니다.
- A **-dest** 데이터 하려는 위치를 나타내는 매개 변수입니다.
- A **– 동사** 나타내는 매개 변수는 [작업](https://technet.microsoft.com/library/dd568989(WS.10).aspx) 수행 하려는 합니다.

MSDeploy.exe 의존 [웹 배포 공급자](https://technet.microsoft.com/library/dd569040(WS.10).aspx) 원본 및 대상 데이터를 처리 하 합니다. 웹 배포를 사용 하려면 응용 프로그램 및 데이터 원본 & #x 2014의 범위를 나타내는 공급자 많이 포함 됩니다. 예를 들어 SQL Server 데이터베이스, IIS 웹 서버, 인증서, 전역 어셈블리 캐시 (GAC) 어셈블리에 대 한 공급자가 다양 한 다른 구성 파일 및 다른 종류의 데이터를 많이 합니다. 두는 **– 소스** 매개 변수 및 **-dest** 형태로 매개 변수는 공급자를 지정 해야 **– 소스**: [*providerName*] [=*위치*]. IIS 웹 사이트에 웹 패키지를 배포할 때 이러한 값을 사용 해야 합니다.

- **– 소스** 공급자는 항상 [패키지](https://technet.microsoft.com/library/dd569019(WS.10).aspx)합니다. 예:

    [!code-console[Main](deploying-web-packages/samples/sample4.cmd)]
- **-dest** 공급자는 항상 [자동](https://technet.microsoft.com/library/dd569016(WS.10).aspx)합니다. 예:

    [!code-console[Main](deploying-web-packages/samples/sample5.cmd)]
- **– 동사** 항상 **동기화**합니다.

    [!code-console[Main](deploying-web-packages/samples/sample6.cmd)]

또한 사용자 지정 해야 다양 한 다른 [공급자별 설정](https://technet.microsoft.com/library/dd569001(WS.10).aspx) 하 고 일반적인 [운영 설정](https://technet.microsoft.com/library/dd569089(WS.10).aspx)합니다. 예를 들어 ContactManager.Mvc 웹 응용 프로그램을 스테이징 환경에 배포 한다고 가정 합니다. 배포를 대상 웹 배포 처리기 및 기본 인증을 사용 해야 합니다. 웹 응용 프로그램을 배포 하려면 다음 단계를 완료 해야 합니다.

**MSDeploy.exe를 사용 하 여 웹 응용 프로그램을 배포 하려면**

1. 빌드하고에 설명 된 대로 웹 응용 프로그램 프로젝트를 패키지 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.
2. 수정 된 *ContactManager.Mvc.SetParameters.xml* 에 설명 된 대로 스테이징 환경에 대 한 올바른 매개 변수 값을 포함 하는 파일 [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)합니다.
3. 명령 프롬프트 창을 열고 MSDeploy.exe의 위치로 이동 합니다. 이 일반적으로 웹 배포 V2\msdeploy.exe %PROGRAMFILES%\IIS\Microsoft에 있습니다.
4. 이 명령을 입력 한 다음 Enter 키를 누릅니다 (줄 바꿈 무시):

    [!code-console[Main](deploying-web-packages/samples/sample7.cmd)]

이 예제에 대한 설명:

- **– 소스** 매개 변수를 지정 된 **패키지** 공급자 웹 패키지의 위치를 나타냅니다.
- **-dest** 매개 변수는 지정 된 **자동** 공급자입니다. **computerName** 설정은 대상 서버에 웹 배포 처리기의 서비스 URL을 제공 합니다. **인증 유형** 설정은 기본 인증을 사용 하려면와 같이 제공 해야 나타냅니다는 **username** 및 **암호**합니다. 마지막으로 **includeAcls = "False"** 설정은 대상 서버에 소스 웹 응용 프로그램에서 파일의 액세스 제어 목록 (Acl)을 복사 하려는 하지 나타냅니다.
- **– 동사: 동기화** 인수 대상 서버에서 원본 콘텐츠를 복제할 것인지를 나타냅니다.
- **– disableLink** 인수 응용 프로그램 풀, 가상 디렉터리 구성 또는 대상 서버에서 Secure Sockets Layer (SSL) 인증서를 복제 하 고 않은 있는지를 나타냅니다. 자세한 내용은 참조 [링크 확장을 배포 하는 웹](https://technet.microsoft.com/library/dd569028(WS.10).aspx)합니다.
- **– setParamFile** 의 위치를 제공 하는 매개 변수는 *SetParameters.xml* 파일입니다.
- **– allowUntrusted** 스위치 나타냅니다 웹 배포 SSL 인증서를 신뢰할 수 있는 인증 기관에서 발급 되지 않은 허용 해야 합니다. 웹 배포 처리기에 배포 하는 서비스 URL을 보호 하는 자체 서명 된 인증서를 사용한 경우이 스위치를 포함 해야 합니다.

## <a name="automating-web-package-deployment"></a>웹 패키지 배포 자동화

많은 엔터프라이즈 시나리오를 더 큰 단일 단계 또는 자동화 된 배포의 일부로 웹 패키지를 배포 합니다. 웹 패키지를 실행 하 여 배포 하려는 여부에 관계 없이 *. deploy.cmd* 파일 또는 MSDeploy.exe를 직접 사용 하 여 명령을 매개 변수화 및에 Microsoft Build Engine (MSBuild) 대상에서 호출할 수 있습니다 프로젝트 파일입니다.

Contact Manager 샘플 솔루션에 검토할는 **PublishWebPackages** 대상에 *Publish.proj* 파일입니다. 이 대상 마다 한 번씩 실행 *. deploy.cmd* 항목 목록이에 의해 식별 된 파일 **PublishPackages**합니다. 대상 속성 및 항목 메타 데이터를 사용 하 여 각각에 대 한 인수 값의 전체 집합을 만들려는 *. deploy.cmd* 파일을 사용 하 여 선택한 다음는 **Exec** 명령을 실행 하는 작업입니다.


[!code-xml[Main](deploying-web-packages/samples/sample8.xml)]


> [!NOTE]
> 일반적으로 사용자 지정 프로젝트 파일에 대 한 소개와 샘플 솔루션에서 프로젝트 파일 모델의 광범위 한 개요를 참조 하십시오. [프로젝트 파일 이해](understanding-the-project-file.md) 및 [빌드 프로세스를 이해](understanding-the-build-process.md)합니다.


## <a name="endpoint-considerations"></a>끝점 고려 사항

웹 패키지를 실행 하 여 배포 되는 여부에 관계 없이 *. deploy.cmd* 파일 또는 MSDeploy.exe를 직접 사용 하 여 컴퓨터 이름 또는 배포에 대 한 서비스 끝점을 지정 해야 합니다.

대상 웹 서버를 원격 에이전트 웹 배포 서비스를 사용 하 여 배포에 대 한 구성 경우 대상으로 대상 서비스 URL을 지정 합니다.


[!code-console[Main](deploying-web-packages/samples/sample9.cmd)]


또는 서버 이름만을 대상으로 지정할 수 있습니다 하 고 웹 배포에서 원격 에이전트 서비스 URL을 유추 합니다.


[!code-console[Main](deploying-web-packages/samples/sample10.cmd)]


대상 웹 서버 웹 배포 처리기를 사용 하 여 배포를 구성 하는 경우 IIS 웹 관리 서비스 (WMSvc)의 끝점 주소를 대상으로 지정 해야 합니다. 기본적으로이 형식을 사용 합니다.


[!code-console[Main](deploying-web-packages/samples/sample11.cmd)]


이러한 끝점 중 하나를 사용 하 여 대상을 지정할 수 있습니다는 *. deploy.cmd* 파일이 나 직접 MSDeploy.exe 합니다. 그러나에 설명 된 대로 관리자가 아닌 사용자로 웹 배포 처리기를 배포 하려는 경우 [웹 배포 게시 (웹 배포 처리기)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md), 서비스 끝점 주소에 쿼리 문자열을 추가 해야 합니다.


[!code-console[Main](deploying-web-packages/samples/sample12.cmd)]


관리자가 아닌 사용자; IIS 서버 수준 액세스 권한이 없기 때문에 이것이 자신이 특정 IIS 웹 사이트에 대 한 액세스를가지고 있습니다. 문서 작성에 웹 게시 파이프라인 (WPP)을 버그 때문에 실행할 수 없습니다는 *. deploy.cmd* 쿼리 문자열을 포함 하는 끝점 주소를 사용 하 여 파일입니다. 이 시나리오에서는 MSDeploy.exe를 직접 사용 하 여 웹 패키지를 배포 해야 합니다.

> [!NOTE]
> 웹 배포 원격 에이전트 서비스 및 웹 배포 처리기에 대 한 자세한 내용은 참조 하십시오. [웹 배포에 대 한 오른쪽 접근 방식을 선택](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)합니다. 이러한 끝점을 배포 하려면 환경 관련 프로젝트 파일을 구성 하는 방법에 대 한 지침을 참조 하십시오. [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)합니다.


## <a name="authentication-considerations"></a>인증 고려 사항

웹 패키지를 실행 하 여 배포 되는 여부에 관계 없이 *. deploy.cmd* 파일 또는 MSDeploy.exe를 직접 사용 하 여 인증 유형을 지정 해야 합니다. 두 개의 가능한 값을 허용 하는 웹 배포: **NTLM** 또는 **기본**합니다. 기본 인증을 지정 하면도 사용자 이름 및 암호를 제공 해야 합니다. 인증 유형을 선택 하는 경우 주의 해야 할 필요는 다양 한 요인이 있습니다.

- 웹 배포 원격 에이전트 서비스를 배포 하는 경우 NTLM 인증을 사용 해야 합니다. 원격 에이전트 서비스가 기본 인증 자격 증명을 허용 하지 않습니다.
- 웹 배포 처리기를 배포 하는 경우 NTLM 또는 기본 인증을 사용할 수 있습니다. 기본 설정은 기본 인증입니다. 기본 인증은 사용자 이름 및 암호를 일반 텍스트로 전송를 사용 하지만 자격 증명은 웹 배포 처리기 항상 SSL 암호화를 사용 하 게 보호 됩니다.
- 웹 패키지는 데이터베이스를 포함 하는 경우 웹 서버와 데이터베이스 서버는 별도 컴퓨터에로 인해 NTLM 인증을 사용 하 여 데이터베이스를 배포할 수 없습니다는 [NTLM "이중 홉" 제한](https://go.microsoft.com/?linkid=9805120)합니다. 배포 연결 문자열에 SQL Server 자격 증명을 사용 하거나 웹 배포를 기본 인증 자격 증명을 제공 해야 합니다. 이 문제에 자세히 설명 되어 [엔터프라이즈 환경에 배포 멤버 자격 데이터베이스](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)합니다.

## <a name="conclusion"></a>결론

이 항목을 배포 하 웹 패키지를 실행 하거나 설명의 *. deploy.cmd* 파일 또는 MSDeploy.exe를 직접 사용 하 여 합니다. 각 접근 방식의 적합할 시점과 매개 변수화 더 큰 단일 단계 또는 자동화 된 빌드 프로세스의 일부로 배포 명령을 실행 하는 방법을 설명 하는 것를 설명 합니다.

## <a name="further-reading"></a>추가 정보

만들기 및 웹 배포 패키지를 매개 변수화 하는 방법에 대 한 지침을 참조 하십시오. [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md) 및 [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)합니다. 빌드 및 인스턴스를 Team Foundation Server (TFS)에서 웹 패키지를 배포 하는 방법에 대 한 지침을 참조 하십시오. [자동화 된 웹 배포를 위해 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다. 사용자 지정 하 고 배포 프로세스 문제를 해결 하는 방법에 대 한 정보를 참조 하십시오. [배포에서 제외 하 고 파일 및 폴더](../advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment.md)합니다.

>[!div class="step-by-step"]
[이전](configuring-parameters-for-web-package-deployment.md)
[다음](deploying-database-projects.md)
