---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
title: 빌드 프로세스 이해 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 빌드 및 배포 프로세스를 엔터프라이즈 규모의 연습을 제공 합니다. 이 항목에서 설명 하는 방식은 사용자 지정 Microsoft 빌드 Engin를 사용 하는 중...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 5b982451-547b-4a2f-a5dc-79bc64d84d40
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
msc.type: authoredcontent
ms.openlocfilehash: 581b7e996bf5aa4c76a6bf3d55a758677c0bf897
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37804318"
---
<a name="understanding-the-build-process"></a>빌드 프로세스 이해
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 빌드 및 배포 프로세스를 엔터프라이즈 규모의 연습을 제공 합니다. 이 항목에서 설명 하는 방식은 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 하 여 프로세스의 모든 측면을 세부적으로 제어할 수 있도록 합니다. 프로젝트 파일 내에서 사용자 지정 MSBuild 대상 인터넷 정보 서비스 (IIS) 웹 배포 도구 (MSDeploy.exe)와 같은 배포 유틸리티 및 VSDBCMD.exe 데이터베이스 배포 유틸리티를 실행 하는 데 사용 됩니다.
> 
> > [!NOTE]
> > 이전 항목인 [프로젝트 파일 이해](understanding-the-project-file.md), MSBuild 프로젝트 파일의 주요 구성 요소를 설명 및 여러 대상 환경에 배포를 지원 하기 위해 분할 프로젝트 파일의 개념이 도입 되었습니다. 아직 수행 하지 않은 이러한 개념을 잘 알고, 경우 검토해 [프로젝트 파일 이해](understanding-the-project-file.md) 작업 수행 하기 전에이 항목입니다.


이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.

이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="build-and-deployment-overview"></a>빌드 및 배포 개요

에 [Contact Manager 솔루션](the-contact-manager-solution.md), 빌드 및 배포 프로세스를 제어 하는 세 개의 파일:

- A *유니버설 프로젝트 파일* (*Publish.proj*). 이 대상 환경 간에 변경 되지 않는 빌드 및 배포 지침을 포함 합니다.
- *환경별 프로젝트 파일* (*Env Dev.proj*). 특정 대상 환경에 관련 된 빌드 및 배포 설정을 포함 합니다. 예를 들어 사용할 수 있습니다 합니다 *Env Dev.proj* 파일을 개발자나 테스트 환경에 대 한 설정을 제공 하 라는 대체 파일을 만듭니다 *Env Stage.proj* 스테이징에 대 한 설정을 제공 하려면 환경입니다.
- A *명령 파일* (*게시 Dev.cmd*). 프로젝트 파일을 지정 하는 명령을 실행 하려고 하는 MSBuild.exe 포함 합니다. 각 파일을 다른 환경 관련 프로젝트 파일을 지정 하는 MSBuild.exe 명령에 포함 된 모든 대상 환경에 대 한 명령에 대 한 파일을 만들 수 있습니다. 따라서 개발자를 적절 한 명령 파일을 실행 하면 서로 다른 환경에 배포할 수 있습니다.

샘플 솔루션에서는 이러한 세 파일 게시 솔루션 폴더에서 찾을 수 있습니다.

![](understanding-the-build-process/_static/image1.png)

이러한 파일을 자세히 살펴보기 전에이 방법을 사용 하면 전반적인 빌드 프로세스의 작동 방식에 대해를 살펴보겠습니다. 높은 수준에서 빌드 및 배포 프로세스는 다음과 같이 나타납니다.

![](understanding-the-build-process/_static/image2.png)

가장 먼저 발생 하는 두 프로젝트 파일은&#x2014;유니버설 빌드 및 배포 지침이 포함 된 생성자와 환경 관련 설정이 포함 된&#x2014;단일 프로젝트 파일에 병합 됩니다. 그런 다음 MSBuild 프로젝트 파일의 지침을 통해 작동합니다. 각 프로젝트 파일을 사용 하 여 각 프로젝트에 대 한 솔루션에서 프로젝트를 작성 합니다. 그런 다음 Web Deploy (MSDeploy.exe)와 같은 다른 도구 및 대상 환경에 웹 콘텐츠 및 데이터베이스를 배포 하려면 VSDBCMD 유틸리티 호출 합니다.

처음부터 끝까지, 빌드 및 배포 프로세스는 이러한 작업을 수행 합니다.

1. 최신 빌드에 대 한 준비에서 출력 디렉터리의 내용을 삭제합니다.
2. 솔루션의 각 프로젝트를 빌드할:

    1. 웹 프로젝트에 대 한&#x2014;이 경우 ASP.NET MVC 웹 응용 프로그램 및 WCF 웹 서비스&#x2014;빌드 프로세스는 각 프로젝트에 대해 웹 배포 패키지를 만듭니다.
    2. 데이터베이스 프로젝트에 대 한 빌드 프로세스는 각 프로젝트에 대 한 배포 매니페스트 (.deploymanifest 파일)를 만듭니다.
3. VSDBCMD.exe 유틸리티를 사용 하 여 프로젝트 파일에서 다양 한 속성을 사용 하 여 솔루션의 각 데이터베이스 프로젝트를 배포 하려면&#x2014;는 대상 연결 문자열 및 데이터베이스 이름&#x2014;.deploymanifest 파일과 함께 합니다.
4. MSDeploy.exe 유틸리티를 사용 하 여 프로젝트 파일에서 다양 한 속성을 사용 하 여 배포 프로세스를 제어 하는 솔루션의 각 웹 프로젝트 배포.

이 과정을 자세히 추적 하는 샘플 솔루션을 사용할 수 있습니다.

> [!NOTE]
> 사용자 고유의 서버 환경에 대 한 환경 관련 프로젝트 파일 사용자 지정 하는 방법에 대 한 지침을 참조 하세요 [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)합니다.


## <a name="invoking-the-build-and-deployment-process"></a>빌드 및 배포 프로세스를 호출합니다.

Contact Manager 솔루션 개발자 테스트 환경에 배포 하려면 개발자는 다음과 같이 실행 됩니다. 합니다 *게시 Dev.cmd* 명령 파일입니다. MSBuild.exe를 호출 하는이 지정 *Publish.proj* 실행 하려면 프로젝트 파일 및 *Env Dev.proj* 매개 변수 값으로.


[!code-console[Main](understanding-the-build-process/samples/sample1.cmd)]


> [!NOTE]
> 합니다 **/fl** 전환 (짧은 **/fileLogger**) 라는 파일에 빌드 출력을 기록 *msbuild.log* 현재 디렉터리에 있습니다. 자세한 내용은 참조는 [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311.aspx)합니다.


이 시점에서 MSBuild 실행을 시작 로드 된 *Publish.proj* 파일 및 그 안에 있는 지침을 처리 하기 시작 합니다. 첫 번째 명령은 프로젝트는 MSBuild 지시 파일을 **TargetEnvPropsFile** 매개 변수를 지정 합니다.


[!code-xml[Main](understanding-the-build-process/samples/sample2.xml)]


**TargetEnvPropsFile** 매개 변수를 지정 합니다 *Env Dev.proj* 파일 이기 때문에 MSBuild의 콘텐츠를 병합 합니다 *Env Dev.proj* 파일를  *Publish.proj* 파일입니다.

MSBuild에서 병합 된 프로젝트 파일에서 발생 하는 다음 요소는 속성 그룹입니다. 속성 파일에 나타나는 순서 대로 처리 됩니다. MSBuild는 지정 된 조건을 충족 제공 각 속성에 대 한 키-값 쌍을 만듭니다. 나중에 파일에 정의 된 속성 파일에 앞에서 정의한 동일한 이름의 속성을 덮어씁니다. 예를 들어 합니다 **OutputRoot** 속성입니다.


[!code-xml[Main](understanding-the-build-process/samples/sample3.xml)]


MSBuild에서 첫 번째를 처리 하는 경우 **OutputRoot** 요소인 마찬가지로 명명 된 매개 변수를 제공 하지 않았습니다의 값을 설정 합니다 **OutputRoot** 속성을 **... \Publish\Out**합니다. 두 번째 있을 경우 **OutputRoot** 요소를 조건이 **true**의 값을 덮어씁니다를 **OutputRoot** 속성의 값으로는 **OutDir** 매개 변수입니다.

MSBuild에서 발생 하는 다음 요소는 라는 항목이 포함 된 단일 항목 그룹을 **ProjectsToBuild**합니다.


[!code-xml[Main](understanding-the-build-process/samples/sample4.xml)]


명명 된 항목 목록을 작성 하 여이 명령을 처리 하는 MSBuild **ProjectsToBuild**합니다. 항목 목록에 단일 값을 포함 하는 예제의 경우&#x2014;의 경로 및 솔루션 파일의 파일 이름입니다.

이 시점에서 나머지 요소는 대상이 됩니다. 대상 속성 및 항목에서 다르게 처리 됩니다&#x2014;기본적으로, 대상으로 처리 되지 않는 되거나 되지 않는 하거나 명시적으로 사용자가 지정한 프로젝트 파일 내에서 다른 구문에 의해 호출 됩니다. 이전에 설명한 대로 열기 **프로젝트** 태그를 포함 한 **DefaultTargets** 특성입니다.


[!code-xml[Main](understanding-the-build-process/samples/sample5.xml)]


이렇게 하면 MSBuild를 호출 하는 **FullPublish** 대상이 대상 MSBuild.exe가 호출 될 때 지정 합니다. 합니다 **FullPublish** 대상 작업을 포함 하지 않으면 대신 종속성 목록을 간단히 지정 합니다.


[!code-xml[Main](understanding-the-build-process/samples/sample6.xml)]


이 종속성 MSBuild를 실행 하려면 지시 합니다 **FullPublish** 이 순서 대로 대상이 목록을 호출 할 대상:

1. 호출 해야 합니다 **정리** 대상입니다.
2. 호출 해야 합니다 **BuildProjects** 대상입니다.
3. 호출 해야 합니다 **GatherPackagesForPublishing** 대상입니다.
4. 호출 해야 합니다 **PublishDbPackages** 대상입니다.
5. 호출 해야 합니다 **PublishWebPackages** 대상입니다.

### <a name="the-clean-target"></a>Clean 대상

합니다 **정리** 대상 기본적으로 삭제 합니다. 출력 디렉터리 및 모든 해당 콘텐츠는 최신 빌드에 대 한 준비로 합니다.


[!code-xml[Main](understanding-the-build-process/samples/sample7.xml)]


대상이 포함 된 **ItemGroup** 요소입니다. 속성 또는 내의 항목을 정의 하는 경우는 **대상** 요소를 만들 *동적* 속성 및 항목입니다. 즉, 속성 또는 항목 대상을 실행 될 때까지 처리 되지 않습니다. 출력 디렉터리 없거나 빌드할 수 있도록 빌드 프로세스가 시작 될 때까지 파일을 포함 하지 수는 **\_FilesToDelete** 정적 항목으로 나열; 실행이 진행 될 때까지 기다려야 합니다. 따라서 대상 내의 항목을 동적으로 목록을 작성 합니다.

> [!NOTE]
> 이 경우 때문에 합니다 **정리** 대상이 실행할 첫 번째는 실제 동적 항목 그룹을 사용할 필요가 없습니다. 그러나 것이 좋습니다 동적 속성 및 항목을 사용 하 여 이러한 유형의 시나리오를 시점에서 다른 순서로 대상을 실행 하려는 수도 있습니다.  
> 사용 하지 않을 항목을 선언 하지 않는 것을 목표로 정해야 하 합니다. 특정 대상에만 사용할 수 있는 항목에 있는 경우에 빌드 프로세스에서 모든 불필요 한 오버 헤드를 제거 하려면 대상 내에 배치 하는 것이 좋습니다.


항목을 제외 하 고, 동적 합니다 **정리** 대상은 매우 간단 하 고 기본 제공 활용 **메시지**, **삭제**, 및 **RemoveDir**작업:

1. 로 거로 메시지를 보냅니다.
2. 삭제할 파일의 목록을 작성 합니다.
3. 파일을 삭제 합니다.
4. 출력 디렉터리를 제거 합니다.

### <a name="the-buildprojects-target"></a>BuildProjects 대상

합니다 **BuildProjects** 대상에는 기본적으로 샘플 솔루션의 모든 프로젝트를 빌드합니다.


[!code-xml[Main](understanding-the-build-process/samples/sample8.xml)]


이 대상 이전 항목에서 자세히 설명한 [프로젝트 파일 이해](understanding-the-project-file.md), 작업 및 대상 속성 및 항목 참조 하는 방법을 보여 줍니다. 이 시점에서 관심이 주로 합니다 **MSBuild** 작업 합니다. 여러 프로젝트를 빌드하기 위해이 작업을 사용할 수 있습니다. 작업에 MSBuild.exe;의 새 인스턴스를 만들지 않습니다. 현재 실행 중인 인스턴스를 사용 하 여 각 프로젝트를 빌드합니다. 이 예제에 대 한 관심의 핵심 포인트는 배포 속성:

- 합니다 **DeployOnBuild** 속성 각 프로젝트의 빌드를 완료 되 면 프로젝트 설정의 모든 배포 명령을 실행 하는 MSBuild에 지시 합니다.
- 합니다 **DeployTarget** 속성 프로젝트를 빌드한 후 호출 하려는 대상을 식별 합니다. 이 경우에 **패키지** 대상 배포 가능한 웹 패키지에 프로젝트 출력을 빌드합니다.

> [!NOTE]
> 합니다 **패키지** 대상 웹 게시 파이프라인 (WPP), MSBuild 및 웹 배포 간의 통합을 제공 하는 호출 합니다. 기본 제공 대상 WPP이 제공 하는 검토를 확인 하려는 경우는 *Microsoft.Web.Publishing.targets* %PROGRAMFILES (x86) %\MSBuild\Microsoft\VisualStudio\v10.0\Web 폴더의 파일입니다.


### <a name="the-gatherpackagesforpublishing-target"></a>GatherPackagesForPublishing 대상

연구 하는 경우는 **GatherPackagesForPublishing** 대상 보면 모든 작업을 실제로 포함 되지 않습니다. 대신 동적 세 가지 항목을 정의 하는 단일 항목 그룹을 포함 합니다.


[!code-xml[Main](understanding-the-build-process/samples/sample9.xml)]


이러한 항목은 때 생성 된 배포 패키지를 참조 합니다 **BuildProjects** 대상이 실행 합니다. 있습니다 수 없습니다 이러한 항목을 정의 정적으로 프로젝트 파일에서 항목을 참조 하는 파일까지 존재 하지 때문에 합니다 **BuildProjects** 대상이 실행 됩니다. 대신 항목을 정의 해야 동적으로 될 때까지 호출 되지 않는 대상 내의 후 합니다 **BuildProjects** 대상이 실행 됩니다.

이 대상 내의 항목은 사용 되지 않습니다&#x2014;이 대상 항목 및 각 항목 값과 연결 된 메타 데이터를 간단히 작성 합니다. 이러한 요소를 처리 한 후의 **PublishPackages** 항목의 경로를 두 개의 값이 포함 됩니다는 *ContactManager.Mvc.deploy.cmd* 파일 및 경로를 *ContactManager.Service.deploy.cmd* 파일입니다. 웹 배포 각 프로젝트에 대 한 웹 패키지의 일부로 이러한 파일을 만들고을 호출 해야 하는 파일 패키지를 배포 하기 위해 대상 서버에서. 이러한 파일 중 하나를 열면 기본적으로 MSDeploy.exe 명령은 다양 한 빌드 관련 매개 변수 값으로 표시 됩니다.

합니다 **DbPublishPackages** 항목의 경로를 단일 값을 포함 합니다 합니다 *ContactManager.Database.deploymanifest* 파일입니다.

> [!NOTE]
> 데이터베이스 프로젝트를 빌드하고 동일한 스키마를 사용 하 여 MSBuild 프로젝트 파일로.deploymanifest 파일로 생성 됩니다. 데이터베이스 스키마 (.dbschema)의 위치 및 모든 배포 전 및 배포 후 스크립트의 세부 정보를 포함 하 여 데이터베이스를 배포 하는 데 필요한 모든 정보를 포함 합니다. 자세한 내용은 [의 개요 데이터베이스 빌드 및 배포](https://msdn.microsoft.com/library/aa833165.aspx)합니다.


배포 패키지 및 데이터베이스 배포 매니페스트 생성 및 사용 하는 방법을 자세히 알아봅니다 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md) 하 고 [데이터베이스 프로젝트 배포](deploying-database-projects.md)합니다.

### <a name="the-publishdbpackages-target"></a>PublishDbPackages 대상

간단 하 게 말하자면를 **PublishDbPackages** 배포 VSDBCMD 유틸리티를 호출 하는 대상 합니다 **ContactManager** 대상 환경에는 데이터베이스입니다. 결정과 미묘한 차이 많이 포함 데이터베이스 배포를 구성 하 고이에 대 한 자세히 알아봅니다 [데이터베이스 프로젝트 배포](deploying-database-projects.md) 고 [여러환경에대한데이터베이스배포사용자지정](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md). 이 항목에서는이 대상 실제로 작동 하는 방법을 집중적으로 다루겠습니다.

첫째, 여는 태그에 포함 되어 있는지 확인할 수 있습니다는 **출력** 특성입니다.


[!code-xml[Main](understanding-the-build-process/samples/sample10.xml)]


이 예가 *대상 일괄 처리*합니다. MSBuild 프로젝트 파일에서 일괄 처리는 컬렉션을 반복 하기 위한 기술입니다. 값은 **출력** 특성 **"% (DbPublishPackages.Identity)"**, 참조 하는 **Identity** 의 메타 데이터 속성은 **DbPublishPackages** 항목 목록입니다. 이 표기법 **Outputs=%***(ItemList.ItemMetadataName)*,으로 변환 됩니다.

- 항목 분할 **DbPublishPackages** 같은 포함 된 항목의 일괄 처리로 **Identity** 메타 데이터 값입니다.
- 대상 일괄 처리 마다 한 번씩 실행 합니다.

> [!NOTE]
> **Identity** 중 하나인 합니다 [기본 제공 메타 데이터 값](https://msdn.microsoft.com/library/ms164313.aspx) 만들기의 모든 항목에 할당 된 합니다. 값을 가리킵니다 합니다 **포함** 특성을 **항목** 요소&#x2014;즉, 경로 및 항목의 파일 이름입니다.


이 경우 동일한 경로 및 파일 이름을 사용 하 여 둘 이상의 항목 없어야, 때문에 기본적으로 협력 하 고 하나의 일괄 처리 크기입니다. 대상은 데이터베이스 패키지 마다 한 번씩 실행 됩니다.

비슷한 표기법을 볼 수는 **\_Cmd** 속성을 적절 한 스위치도 VSDBCMD 명령을 작성 합니다.


[!code-xml[Main](understanding-the-build-process/samples/sample11.xml)]


이 예에서 **%(DbPublishPackages.DatabaseConnectionString)** 를 **%(DbPublishPackages.TargetDatabase)**, 및 **%(DbPublishPackages.FullPath)** 모든 참조 메타 데이터 값을 **DbPublishPackages** 항목 컬렉션입니다. **\_Cmd** 속성을 사용 합니다 **Exec** 명령을 호출 하는 작업을 합니다.


[!code-xml[Main](understanding-the-build-process/samples/sample12.xml)]


이 표기법의 결과로 합니다 **Exec** 작업 일괄 처리의 고유한 조합에 따라 만들어집니다 합니다 **DatabaseConnectionString**를 **TargetDatabase**, 및 **FullPath** 메타 데이터 값 및 작업 일괄 처리 마다 한 번 실행 됩니다. 이 예가 *작업 일괄 처리*합니다. 그러나 이므로 단일 항목 일괄 처리로 항목 컬렉션이 이미 분할 대상 수준 일괄 처리를 **Exec** 작업은 대상의 각 반복에 대해 한 번만 실행 됩니다. 즉,이 작업은 솔루션의 각 데이터베이스 패키지에 한 번씩 VSDBCMD 유틸리티를 호출합니다.

> [!NOTE]
> MSBuild 대상 및 작업 일괄 처리에 대 한 자세한 내용은 참조 [일괄 처리](https://msdn.microsoft.com/library/ms171473.aspx)하십시오 [대상 일괄 처리의 항목 메타 데이터](https://msdn.microsoft.com/library/ms228229.aspx), 및 [작업 일괄 처리의 항목 메타 데이터](https://msdn.microsoft.com/library/ms171474.aspx)합니다.


### <a name="the-publishwebpackages-target"></a>PublishWebPackages 대상

호출 했으므로 이제는 **BuildProjects** 샘플 솔루션의 각 프로젝트에 대해 웹 배포 패키지를 생성 하는 대상으로 합니다. 각 패키지와 함께 제공 되는 *deploy.cmd* 대상 환경에 패키지를 배포 하는 데 필요한 MSDeploy.exe 명령이 들어 있는 파일 및 *SetParameters.xml* 파일을 지정 하는 합니다 필요한 대상 환경의 세부 정보입니다. 또한 호출 되는 **GatherPackagesForPublishing** 포함 하는 항목 컬렉션을 생성 하는 대상을 *deploy.cmd* 관심이 파일. 기본적으로 **PublishWebPackages** 대상 이러한 기능을 수행 합니다.

- 여기에서 조작 합니다 *SetParameters.xml* 대상 환경에 대 한 올바른 정보를 포함 시킬 각 패키지에 대 한 파일 사용 하 여 합니다 **XmlPoke** 작업 합니다.
- 호출 된 *deploy.cmd* 적절 한 스위치를 사용 하 여 각 패키지에 대 한 파일입니다.

마찬가지로 합니다 **PublishDbPackages** 대상에는 **PublishWebPackages** 대상을 사용 하 여 대상 일괄 처리 되도록 대상이 각 웹 패키지에 대해 한 번 실행 됩니다.


[!code-xml[Main](understanding-the-build-process/samples/sample13.xml)]


대상 내에서 **Exec** 작업은 실행 하는 데 사용 되는 *deploy.cmd* 각 웹 패키지에 대 한 파일입니다.


[!code-xml[Main](understanding-the-build-process/samples/sample14.xml)]


웹 패키지의 배포를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.

## <a name="conclusion"></a>결론

이 항목에서는 분할 프로젝트 파일 Contact Manager 샘플 솔루션에 대 한 처음부터 빌드 및 배포 프로세스를 제어를 사용 하는 방법의 연습을 제공 합니다. 이 방법을 사용 하 여 실행 하면 복잡 한을 반복 가능한 단일 단계에서 엔터프라이즈 규모 배포 환경별 명령 파일을 실행 하면 수 있습니다.

## <a name="further-reading"></a>추가 정보

WPP 및 프로젝트 파일에 대 한 자세한 소개를 참조 하세요. [Microsoft 빌드 엔진 내:를 사용 하 여 MSBuild 및 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi William Bartholomew, ISBN: 978-0-7356-4524-0입니다.

> [!div class="step-by-step"]
> [이전](understanding-the-project-file.md)
> [다음](building-and-packaging-web-application-projects.md)
