---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: "경우에 기능을 수행 배포 | Microsoft Docs"
author: jrjlee
description: "이 항목 ' 경우 어떻게 ' 수행 하는 방법에 설명 등의 시뮬레이션 된 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 및 V를 사용 하 여 배포..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: 62be7c9636fb74c40bec812e9ac76b360995da50
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="performing-a-what-if-deployment"></a>"경우 어떻게" 배포
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목 "경우 어떻게" 수행 하는 방법에 설명 등의 시뮬레이션 된 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 및 VSDBCMD를 사용 하 여 배포 합니다. 이렇게 하면 실제로 응용 프로그램을 배포 하기 전에 배포 논리는 특정 대상 환경에 미치는 영향을 확인할 수 있습니다.


이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 이 자습서 시리즈 샘플 솔루션 & #x 2014;을 사용 하는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& #x 2014; 현실적인 수준의 복잡성을 Windows ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 제공 합니다.

이 자습서의 핵심에는 배포 방법에 설명 된 분할 프로젝트 파일 접근 방식에 따라 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 빌드 및 배포 프로세스는 두 개의 프로젝트 파일 & #x 2014로 제어 되; o 환경 관련 빌드 및 배포 설정을 포함 하는 하나 및 모든 대상 환경에 적용 되는 빌드 명령이 포함 된 ne 합니다. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 구성 하기 위해 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="performing-a-what-if-deployment-for-web-packages"></a>웹 패키지에 대 한 "경우 어떻게" 배포를 수행합니다.

"경우 어떻게"의 배포를 수행할 수 있는 기능 (또는 평가판)를 포함 하는 웹 배포 모드입니다. "경우 어떻게" 모드에서 아티팩트를 배포할 때 배포를 끝낸 있지만 대상 서버에 아무 것도 실제로 변경 되지 않은 로그 파일을 생성 웹 배포 합니다. 로그 파일을 검토 배포 갖습니다 대상 서버에 특히 어떤 영향을 이해할 수 있습니다.

- 기능 추가 됩니다.
- 어떤 업데이트 됩니다.
- 어떤 삭제 됩니다.

"경우 어떻게" 배포 수행할 항상 수 없는 작업 대상 서버에 아무 것도 변경 실제로 되지 않으므로 배포는 성공 여부를 예측 합니다.

에 설명 된 대로 [웹 패키지 배포](../web-deployment-in-the-enterprise/deploying-web-packages.md), 두 가지 방법 & #x 2014에서; MSDeploy.exe 명령줄 유틸리티 직접 사용 하 여 또는 실행 하 여 웹 배포를 사용 하 여 웹 패키지를 배포할 수 있습니다는 *. deploy.cmd* 빌드 프로세스를 생성 하는 파일입니다.

MSDeploy.exe를 직접 사용 중인 경우 추가 하 여 "경우 어떻게" 배포를 실행할 수 있습니다는 **– whatif** 플래그를 명령입니다. 예를 들어 스테이징 환경에 ContactManager.Mvc.zip 패키지를 배포 하는 경우 어떻게 되는지 평가 수행 하려면 MSDeploy 명령은 다음과 같습니다.


[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]


"경우 어떻게" 배포 결과를 만족 하는 경우 제거할 수 있습니다는 **– whatif** 라이브 배포를 실행 하는 플래그입니다.

> [!NOTE]
> MSDeploy.exe에 대 한 명령줄 옵션에 대 한 자세한 내용은 참조 하십시오. [웹 배포 작업이 설정](https://technet.microsoft.com/en-us/library/dd569089(WS.10).aspx)합니다.


사용 중인 경우는 *. deploy.cmd* 파일을 포함 하 여 "경우 어떻게" 배포를 실행할 수 있습니다는 **/t** 대신 플래그 (평가판 모드) 플래그는 **/y** 의 플래그 ("yes" 또는 업데이트 모드) 명령입니다. 예를 들어, ContactManager.Mvc.zip 패키지를 실행 하 여 배포한 경우 어떻게 될 지를 평가 하는 *. deploy.cmd* 파일인 명령 다음과 유사 합니다:


[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]


"평가 모드" 배포 결과를 만족 하는 경우 대체할 수 있습니다는 **/t** 와 플래그는 **/y** 라이브 배포를 실행 하는 플래그:


[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]


> [!NOTE]
> 명령줄 옵션에 대 한 자세한 내용은 *. deploy.cmd* 파일, 참조 [하는 방법: 설치는 배포 패키지를 사용 하 여 파일 deploy.cmd](https://msdn.microsoft.com/en-us/library/ff356104.aspx)합니다. 실행 하는 경우는 *. deploy.cmd* 파일 플래그를 지정 하지 않고 명령 프롬프트에는 사용 가능한 플래그의 목록이 표시 됩니다.


## <a name="performing-a-what-if-deployment-for-databases"></a>데이터베이스에 대 한 "경우 어떻게" 배포를 수행합니다.

이 섹션에서는 데이터베이스, 스키마 기반 증분 배포를 수행 하려면 VSDBCMD 유틸리티를 사용 하는 가정 합니다. 이 방법은에서 더 자세하게 설명 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)합니다. 잘 이해 하는이 항목을 여기에 설명 된 개념을 적용 하기 전에 것이 좋습니다.

VSDBCMD에서 사용 하는 경우 **배포** 사용할 수 있습니다 모드는 **d d** (또는 **/DeployToDatabase**) VSDBCMD 실제로 데이터베이스를 배포 하거나만 생성 하는지 여부를 제어 하는 플래그는 배포 스크립트입니다. .Dbschema 파일을 배포 하는 경우 이것은 동작:

- 지정 하는 경우 **/dd+** 또는 **d d**, VSDBCMD 배포 스크립트를 생성 하 고 데이터베이스를 배포 합니다.
- 지정 하는 경우 **/dd-** 이 스위치를 생략 하거나, VSDBCMD만 배포 스크립트를 생성 합니다.

> [!NOTE]
> 동작은.dbschema 파일 대신.deploymanifest 파일을 배포할 경우에 **d d** 스위치는 훨씬 더 복잡 합니다. VSDBCMD의 값을 무시 합니다, 기본적으로 **d d** .deploymanifest 파일에 포함 된 경우 스위치는 **DeployToDatabase** 의 값을 가진 요소가 **True**합니다. [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md) 전체에서이 동작에 설명 합니다.


예를 들어에 대 한 배포 스크립트를 생성 하는 **ContactManager** 실제로 VSDBCMD 명령을 데이터베이스를 배포 하지 않고 데이터베이스는 다음과 유사 합니다.


[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]


VSDBCMD, 차등 데이터베이스 배포 도구 이며 따라서 배포 스크립트를 동적으로 지정된 된 스키마에 있는 경우 현재 데이터베이스를 업데이트 하는 데 필요한 모든 SQL 명령이 포함 하도록 생성 합니다. 배포에 어떤 영향을 결정 하는 유용한 방법은 했을 경우에 현재 데이터베이스와 포함 된 데이터는 배포 스크립트를 검토 합니다. 예를 들어 확인 하려는 될 수 있습니다.

- 기존 테이블 없어지고 데이터 손실이 발생 하 있는지 여부.
- 여부 연산이 수행 하는 경우 데이터 손실의 위험 예를 들어 분할 하거나 테이블을 병합 하는 경우.

배포 스크립트에 만족 하는 경우와 VSDBCMD 반복할 수 있습니다는 **/dd+** 플래그를 변경 합니다. 또는 요구 사항에 맞게 선택한 다음 데이터베이스 서버에서 수동으로 실행 하는 배포 스크립트를 편집할 수 있습니다.

## <a name="integrating-what-if-functionality-into-custom-project-files"></a>사용자 지정 프로젝트 파일에 "경우 어떻게" 기능 통합

더 복잡 한 배포 시나리오에서 사용 하 여 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 빌드 및 배포 논리를 캡슐화 하에 설명 된 대로 해야 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다. 예를 들어는 [않아](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 솔루션을는 *Publish.proj* 파일:

- 솔루션을 빌드합니다.
- 패키징 및 ContactManager.Mvc 응용 프로그램을 배포 하는 웹 배포를 사용 합니다.
- 패키징 및 ContactManager.Service 응용 프로그램을 배포 하는 웹 배포를 사용 합니다.
- 배포는 **ContactManager** 데이터베이스입니다.

이러한 방식으로 단일 단계 프로세스에 여러 웹 패키지 및/또는 데이터베이스의 배포를 통합 하는 경우 "경우 어떻게" 모드에서 전체 배포를 수행 하는 옵션이 할 수 있습니다.

*Publish.proj* 파일이를 수행할 수는 방법을 보여 줍니다. 먼저 "경우 어떻게" 값을 저장할 속성을 만들려면:


[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]


이 경우 라는 속성이 만든 **WhatIf** 의 기본값은 **false**합니다. 사용자가 속성을 설정 하 여이 값을 재정의할 수 **true** 명령줄 매개 변수, 살펴보겠지만 곧 합니다.

다음 단계는 모든 웹 배포 매개 변수화 하는 및 VSDBCMD 명령 플래그를 나타내도록는 **WhatIf** 속성 값입니다. 예를 들어 다음 대상 (에서 가져온는 *Publish.proj* 파일 및 간소화 된) 실행 되는 *. deploy.cmd* 웹 패키지를 배포 하는 파일입니다. 명령에 포함 된 기본적으로는 **/Y** 스위치 ("yes" 또는 업데이트 모드). 경우 **WhatIf** 로 설정 된 **true**,이으로 대체 되는 **/T** 스위치 (평가판, 또는 "경우 어떻게" 모드).


[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]


마찬가지로, 다음 대상 VSDBCMD 유틸리티를 사용 하 여 데이터베이스를 배포 합니다. 기본적으로는 **d d** 스위치는 포함 되지 않습니다. 즉, VSDBCMD 배포 스크립트를 생성 하는 있지만 데이터베이스 & #x 2014; 배포 되지 것입니다 즉, "what-if" 시나리오입니다. 경우는 **WhatIf** 속성으로 설정 되지 않은 **true**, **d d** 스위치 추가 되 고 VSDBCMD 데이터베이스를 배포 합니다.


[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]


프로젝트 파일의 모든 관련 명령을 매개 변수화 하 같은 방법을 사용할 수 있습니다. "경우 어떻게" 배포를 실행 하려는 경우 수 다음 제공 하기만 하면는 **WhatIf** 명령줄에서 속성 값:


[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]


이러한 방식으로 한 번에 모든 프로젝트 구성 요소에 대 한 "경우 어떻게" 배포를 실행할 수 있습니다.

## <a name="conclusion"></a>결론

이 항목에는 웹 배포, VSDBCMD, 및 MSBuild를 사용 하 여 배포 "경우 어떻게"를 실행 하는 방법을 설명 합니다. "경우 어떻게" 배포를 사용 하면 대상 환경에 실제로 변경을 수행 하기 전에 제안 된 배포의 영향을 평가 수 있습니다.

## <a name="further-reading"></a>추가 정보

웹 배포 명령줄 구문에 대 한 자세한 내용은 참조 하십시오. [웹 배포 작업이 설정](https://technet.microsoft.com/en-us/library/dd569089(WS.10).aspx)합니다. 사용 하는 경우 명령줄 옵션에 대 한 지침은 *. deploy.cmd* 파일에서 참조 [하는 방법: 설치는 배포 패키지를 사용 하 여 파일 deploy.cmd](https://msdn.microsoft.com/en-us/library/ff356104.aspx)합니다. VSDBCMD 명령줄 구문에 대 한 지침을 참조 하십시오. [VSDBCMD에 대 한 명령줄 참조 합니다. EXE (배포 및 스키마 가져오기)](https://msdn.microsoft.com/en-us/library/dd193283.aspx)합니다.

>[!div class="step-by-step"]
[이전](advanced-enterprise-web-deployment.md)
[다음](customizing-database-deployments-for-multiple-environments.md)
