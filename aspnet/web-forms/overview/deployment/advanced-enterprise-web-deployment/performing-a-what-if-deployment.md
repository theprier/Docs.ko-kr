---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: What를 수행 하는 경우 배포 | Microsoft Docs
author: jrjlee
description: "' 경우 ' 수행 하는 방법에 설명 합니다 (또는 시뮬레이션)이 항목이에서는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 및 V를 사용 하 여 배포 하는 중..."
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: f54a4d91ea0f735d3cd5b99c0dda5d83cbb5e5d4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830651"
---
<a name="performing-a-what-if-deployment"></a>"What If" 배포 수행
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 "what if"를 수행 하는 방법에 설명 합니다 (또는 시뮬레이션) VSDBCMD 고 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 배포 합니다. 이렇게 하면 실제로 응용 프로그램을 배포 하기 전에 배포 논리를 특정 대상 환경에 미치는 영향을 확인할 수 있습니다.


이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.

이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 및 배포 프로세스에 의해 제어 되는&#x2014;하나 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 빌드 명령이 들어 있는입니다. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="performing-a-what-if-deployment-for-web-packages"></a>웹 패키지에 대 한 "What If" 배포 수행

"What if"에서 배포를 수행할 수 있는 기능 (또는 평가판)를 포함 하는 웹 배포 모드입니다. "What if" 모드에서 아티팩트를 배포 하면 배포를 수행 해야 하지만 대상 서버에서 아무 것도 실제로 변경 되지 않은 것 처럼 로그 파일을 생성 웹 배포 합니다. 로그 파일 검토 도움이 배포 해야 대상 서버에서 특히 어떤 영향을 이해할 수 있습니다.

- 새로운 추가 됩니다.
- 새로운 업데이트 됩니다.
- 항목 삭제 됩니다.

"What if" 배포를 실제로 바뀌지 수행할 항상 수 없습니다. 작업 대상 서버에 있는 모든 것 이므로 배포 성공 여부를 예측 합니다.

에 설명 된 대로 [웹 배포 패키지](../web-deployment-in-the-enterprise/deploying-web-packages.md), 두 가지 방법으로 웹 배포를 사용 하는 웹 패키지를 배포할 수 있습니다&#x2014;직접 또는 실행 하 여 MSDeploy.exe 명령줄 유틸리티를 사용 하 여는 *. deploy.cmd* 파일 빌드 프로세스를 생성 합니다.

MSDeploy.exe를 직접 사용 하는 경우 추가 하 여 "what if" 배포를 실행할 수 있습니다 합니다 **– whatif** 플래그 명령입니다. 예를 들어 스테이징 환경에 ContactManager.Mvc.zip 패키지를 배포 하는 경우에 상황을 평가 하려면 MSDeploy 명령을 다음과 비슷합니다.


[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]


"What if" 배포의 결과 만족 하는 경우 제거할 수 있습니다 합니다 **– whatif** 라이브 배포를 실행 하는 플래그입니다.

> [!NOTE]
> MSDeploy.exe에 대 한 명령줄 옵션에 대 한 자세한 내용은 참조 하세요. [웹 배포 작업 설정](https://technet.microsoft.com/library/dd569089(WS.10).aspx)합니다.


사용 중인 경우는 *. deploy.cmd* 파일을 포함 하 여 "what if" 배포를 실행할 수 있습니다 합니다 **/t** 플래그 대신 (평가판 모드) 플래그를 **/y** 플래그 ("yes" 또는 업데이트 모드)에서 사용자 명령입니다. 예를 들어, 실행 하 여 ContactManager.Mvc.zip 패키지를 배포 하는 경우에 상황을 평가 하는 *. deploy.cmd* 파일인 명령은 다음과 유사 합니다:


[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]


바꿀 수 있습니다 "평가판 모드" 배포의 결과 만족 하면 합니다 **/t** 사용 하 여 플래그를 **/y** 라이브 배포를 실행 하는 플래그:


[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]


> [!NOTE]
> 명령줄 옵션에 대 한 자세한 내용은 *. deploy.cmd* 파일을 참조 하세요 [방법: 설치 된 배포 패키지를 사용 하 여 deploy.cmd 파일](https://msdn.microsoft.com/library/ff356104.aspx). 실행 하는 경우는 *. deploy.cmd* 파일 플래그를 지정 하지 않고 명령 프롬프트에는 사용 가능한 플래그의 목록이 표시 됩니다.


## <a name="performing-a-what-if-deployment-for-databases"></a>데이터베이스에 대 한 "What If" 배포 수행

이 섹션에서는 증분, 스키마 기반 데이터베이스를 배포 하는 데 VSDBCMD 유틸리티를 사용 하는 것을 가정 합니다. 이 방법은에서 더 자세히 설명 되어 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)합니다. 잘 이해 하는이 항목에서는 사용 하 여 여기에 설명 된 개념을 적용 하기 전에 유지 하는 것이 좋습니다.

VSDBCMD를 사용 하는 경우 **배포** 모드를 사용할 수는 **/dd** (또는 **/DeployToDatabase**) VSDBCMD 실제로 데이터베이스를 배포 하거나만 생성 하는지 여부를 제어 하는 플래그를 배포 스크립트입니다. .Dbschema 파일에 배포 하는 경우이 동작은:

- 지정 하는 경우 **/dd+** 하거나 **/dd**, VSDBCMD 배포 스크립트를 생성 되며 데이터베이스를 배포 합니다.
- 지정 하는 경우 **/dd-** 스위치를 생략 하거나, VSDBCMD만 배포 스크립트를 생성 합니다.

> [!NOTE]
> 동작을.dbschema 파일이 아닌.deploymanifest 파일을 배포 하는 경우는 **/dd** 스위치는 훨씬 더 복잡 합니다. VSDBCMD는 값을 무시 하는 기본적으로 **/dd** .deploymanifest 파일에 포함 된 경우 스위치를 **DeployToDatabase** 의 값을 가진 요소가 **True**. [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md) 전체에서이 동작을 설명 합니다.


예를 들어에 대 한 배포 스크립트를 생성 하는 **ContactManager** VSDBCMD 명령을 데이터베이스에 실제로 배포 하지 않고 데이터베이스는 다음과 유사 합니다.


[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]


VSDBCMD 차등 데이터베이스 배포 도구를 이며 따라서 배포 스크립트를 동적으로 생성 지정한 스키마에 있는 경우 현재 데이터베이스를 업데이트 하는 데 필요한 모든 SQL 명령이 포함 합니다. 배포 스크립트를 검토는 배포에 영향을 줄 내용을 결정 하는 유용한 방법을 현재 데이터베이스에 포함 된 데이터입니다. 예를 들어, 다음 확인 하는 것이 좋습니다.

- 기존 테이블 없어지고 여부는 결과를 데이터 손실 여부.
- 작업 순서 예를 들어 데이터 손실의 위험을 전달 하는지 여부를, 테이블을 병합 하거나 분할 하는 경우.

배포 스크립트에 만족할 경우 사용 하 여 VSDBCMD 반복할 수 있습니다는 **/dd+** 플래그 변경 내용을 적용 합니다. 또는 요구 사항을 충족 하 고 데이터베이스 서버에서 수동으로 실행 하려면 배포 스크립트를 편집할 수 있습니다.

## <a name="integrating-what-if-functionality-into-custom-project-files"></a>사용자 지정 프로젝트 파일에서 "What If" 기능 통합

더 복잡 한 배포 시나리오에서 사용 하 여 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 빌드 및 배포 논리를 캡슐화 하에 설명 된 대로 해야 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다. 예를 들어, 합니다 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 솔루션에는 *Publish.proj* 파일:

- 솔루션을 빌드합니다.
- 패키지 ContactManager.Mvc 응용 프로그램을 배포 하는 웹 배포를 사용 합니다.
- 패키지 ContactManager.Service 응용 프로그램을 배포 하는 웹 배포를 사용 합니다.
- 배포 된 **ContactManager** 데이터베이스입니다.

이러한 방식으로 단일 단계 프로세스를 여러 웹 패키지 및/또는 데이터베이스의 배포를 통합 하면 "what if" 모드에서 전체 배포를 수행 하는 옵션을 수도 있습니다.

합니다 *Publish.proj* 파일이를 수행할 수는 방법을 보여 줍니다. 첫째, "what-if" 값을 저장 하는 속성을 만드는 해야 합니다.


[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]


이 경우 명명 된 속성을 만들었습니다 **WhatIf** 이며 기본값은 **false**합니다. 사용자 속성을 설정 하 여이 값을 재정의할 수 있습니다 **true** 명령줄 매개 변수에서 살펴보겠지만 곧 합니다.

다음 단계는 모든 웹 배포 매개 변수화 및 VSDBCMD 명령 플래그를 나타내도록 합니다 **WhatIf** 속성 값입니다. 예를 들어, 다음 대상 (에서 가져온를 *Publish.proj* 파일 및 간소화 된) 실행 합니다 *. deploy.cmd* 웹 패키지를 배포 하는 파일입니다. 기본적으로 명령에 포함 된 **/Y** ("yes" 또는 업데이트 모드) 스위치. 경우 **WhatIf** 로 설정 된 **true**, 바뀝니다이 **/T** 스위치 (평가판 또는 "what if" 모드).


[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]


마찬가지로, 다음 대상 데이터베이스를 배포 하는 VSDBCMD 유틸리티를 사용 합니다. 기본적으로 **/dd** 스위치 포함 되지 않습니다. 즉, VSDBCMD 배포 스크립트를 생성 하는 있지만 데이터베이스를 배포 하지 것입니다&#x2014;즉, "what-if" 시나리오입니다. 경우는 **WhatIf** 속성으로 설정 되지 않은 **true**, **/dd** 스위치 추가 되 고 VSDBCMD 데이터베이스를 배포 합니다.


[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]


프로젝트 파일의 모든 관련 명령을 매개 변수화 하려면 동일한 접근 방식을 사용할 수 있습니다. "What if" 배포를 실행 하려는 경우 단순히 제공할 수는 **WhatIf** 명령줄에서 속성 값:


[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]


이러한 방식으로 한 단계로 모든 프로젝트 구성 요소에 대 한 "what if" 배포를 실행할 수 있습니다.

## <a name="conclusion"></a>결론

이 항목에서는 웹 배포, VSDBCMD, 및 MSBuild를 사용 하 여 배포 "what if"를 실행 하는 방법을 설명 합니다. "What if" 배포를 사용 하면 대상 환경에 변경 내용을 실제로 만들기 전에 제안 된 배포의 영향을 평가 수 있습니다.

## <a name="further-reading"></a>추가 정보

웹 배포 명령줄 구문에 대 한 자세한 내용은 참조 하세요. [웹 배포 작업 설정](https://technet.microsoft.com/library/dd569089(WS.10).aspx)합니다. 사용 하는 경우 명령줄 옵션에 대 한 지침은 합니다 *. deploy.cmd* 파일을 참조 하세요 [방법:는 배포 패키지를 사용 하 여 deploy.cmd 파일 설치](https://msdn.microsoft.com/library/ff356104.aspx). VSDBCMD 명령줄 구문에 대 한 지침을 참조 하세요. [VSDBCMD에 대 한 명령줄 참조 합니다. EXE (배포 및 스키마 가져오기)](https://msdn.microsoft.com/library/dd193283.aspx)합니다.

> [!div class="step-by-step"]
> [이전](advanced-enterprise-web-deployment.md)
> [다음](customizing-database-deployments-for-multiple-environments.md)
