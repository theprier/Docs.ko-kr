---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
title: 프로젝트 파일 이해 | Microsoft Docs
author: jrjlee
description: Microsoft Build Engine (MSBuild) 프로젝트 파일은 빌드 및 배포 프로세스의 핵심입니다. 이 항목에서는 MSBuild에 대 한 개념적인 개요를 시작 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 07978d9d-341c-4524-bcba-62976f390f77
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
msc.type: authoredcontent
ms.openlocfilehash: 89c5c7906ccfc453195b788cbc6393dc74cda1fb
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37377206"
---
<a name="understanding-the-project-file"></a>프로젝트 파일 이해
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Microsoft Build Engine (MSBuild) 프로젝트 파일은 빌드 및 배포 프로세스의 핵심입니다. 이 항목에서는 프로젝트 파일과 MSBuild에 대 한 개념적인 개요를 시작합니다. 가로질러 프로젝트 파일을 사용 하 여 실제 응용 프로그램을 배포 하는 방법의 예제를 통해 작동 하 고 프로젝트 파일을 사용 하 여 작업할 때 주요 구성 요소를 설명 합니다.
> 
> 학습할 내용:
> 
> - 어떻게 MSBuild는 프로젝트를 빌드하려면 MSBuild 프로젝트 파일을 사용 합니다.
> - 어떻게 MSBuild는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)와 같은 배포 기술과 통합 됩니다.
> - 프로젝트 파일의 주요 구성 요소를 이해 하는 방법입니다.
> - 어떻게 빌드 및 복잡 한 응용 프로그램을 배포 하려면 프로젝트 파일을 사용할 수 있습니다.


## <a name="msbuild-and-the-project-file"></a>프로젝트 파일과 MSBuild

를 만들고 Visual Studio에서 솔루션을 빌드할 때 Visual Studio 솔루션의 각 프로젝트를 빌드하려면 MSBuild를 사용 합니다. 모든 Visual Studio 프로젝트에 프로젝트 형식에 반영 하는 파일 확장명을 사용 하 여 MSBuild 프로젝트 파일을&#x2014;예를 들어 C# 프로젝트 (.csproj), Visual Basic.NET 프로젝트 (.vbproj) 또는 데이터베이스 프로젝트 (.dbproj). 프로젝트를 구축 하기 위해 MSBuild는 프로젝트에 연결 된 프로젝트 파일을 처리 해야 합니다. 프로젝트 파일은 모든 정보 및 플랫폼 요구 사항, 버전 관리 정보, 웹 서버 또는 데이터베이스 서버 설정에 포함 하려면 콘텐츠와 마찬가지로 프로젝트를 빌드하려면 MSBuild 해야 한다는 지침을 포함 하는 XML 문서 및 수행 해야 하는 작업입니다.

MSBuild 프로젝트 파일에 기반한 합니다 [MSBuild XML 스키마](https://msdn.microsoft.com/library/5dy88c2e.aspx), 이며 결과적으로 빌드 프로세스 전적으로 열고 투명 합니다. 또한 MSBuild 엔진을 사용 하려면 Visual Studio를 설치할 필요가 없습니다&#x2014;.NET Framework의 일부인 MSBuild.exe 실행 파일 및 명령 프롬프트에서 실행할 수 있습니다. 개발자는 MSBuild XML 스키마를 사용 하 여 프로젝트 빌드 및 배포 하는 방법을 정교 하 고 세분화 된 제어를 적용 하려면 사용자 고유의 MSBuild 프로젝트 파일을 만들 수 있습니다. 이러한 사용자 지정 프로젝트 파일이 Visual Studio에서 자동으로 생성 되는 프로젝트 파일과 동일한 방식으로 작동 합니다.

> [!NOTE]
> 또한 Team Foundation Server (TFS)에서 팀 빌드 서비스를 사용 하 여 MSBuild 프로젝트 파일을 사용할 수 있습니다. 예를 들어, 새 코드를 체크 인할 때 테스트 환경에 배포를 자동화 하려면 CI (지속적인 통합) 시나리오에서 프로젝트 파일을 사용할 수 있습니다. 자세한 내용은 [자동화 된 웹 배포용 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다.


### <a name="project-file-naming-conventions"></a>프로젝트 파일 명명 규칙

사용자 고유의 프로젝트 파일을 만들면 원하는 파일 확장명을 사용할 수 있습니다. 그러나 솔루션을 더 쉽게 다른 사람이 이해 하기에 대 한 이러한 일반적인 규칙을 사용 해야 합니다.

- 프로젝트를 빌드하는 프로젝트 파일을 만들 때.proj 확장을 사용 합니다.
- 다른 프로젝트 파일로 가져올 다시 사용할 수 있는 프로젝트 파일을 만들 때.targets 확장명을 사용 합니다. .Targets 확장명을 사용 하 여 파일 일반적으로 없는 빌드 아무 것도 자체를.proj 파일에 가져올 수 있는 지침 포함 하기만 하면 됩니다.

### <a name="integration-with-deployment-technologies"></a>배포 기술과 통합

ASP.NET 웹 응용 프로그램 및 ASP.NET MVC 웹 응용 프로그램과 같은 Visual Studio 2010에서 웹 응용 프로그램 프로젝트를 사용 하 여 했었다면 이러한 프로젝트 패키징 및 배포 대상 환경에 웹 응용 프로그램에 대 한 기본 제공 지원을 포함 알 수 있습니다. **속성** 이러한 프로젝트에 대해 페이지 **웹 패키지 및 게시** 및 **SQL 패키지 및 게시** 탭 구성 하는 데 사용할 수 있는 방법의 구성 요소에 응용 프로그램 패키지 되 고 배포 합니다. 표시 된 **웹 패키지 및 게시** 탭:

![](understanding-the-project-file/_static/image1.png)

이러한 기능은 기본 기술으로 웹 게시 파이프라인 (WPP) 이라고 합니다. WPP MSBuild를 기본적으로 제공 하 고 [웹 배포](https://go.microsoft.com/?linkid=9805122) 웹 응용 프로그램에 대 한 전체 빌드, 패키지 및 배포 프로세스를 제공 하기 위해 협력 합니다.

좋은 소식은 WPP 웹 프로젝트에 대 한 사용자 지정 프로젝트 파일을 만들 때 제공 하는 통합 지점 활용을 수행할 수 있는 것입니다. 프로젝트 빌드, 웹 배포 패키지 만들기 및 단일 프로젝트 파일과 MSBuild에 대 한 단일 호출을 통해 원격 서버에서 이러한 패키지를 설치할 수 있는 프로젝트 파일에서 배포 지침을 포함할 수 있습니다. 또한 빌드 프로세스의 일부로 다른 실행 파일을 호출할 수 있습니다. 예를 들어 스키마 파일에서 데이터베이스를 배포 VSDBCMD.exe 명령줄 도구를 실행할 수 있습니다. 이 항목의 과정을 통해 엔터프라이즈 배포 시나리오의 요구 사항에 맞게 이러한 기능은 활용할 수는 어떻게 볼 수 있습니다.

> [!NOTE]
> 웹 응용 프로그램 배포 프로세스의 작동 방식에 대 한 자세한 내용은 참조 하세요. [ASP.NET 웹 응용 프로그램 프로젝트 배포 개요](https://msdn.microsoft.com/library/dd394698.aspx)합니다.


## <a name="the-anatomy-of-a-project-file"></a>프로젝트 파일의 분석

빌드 프로세스를 자세히 살펴보기 전에 MSBuild 프로젝트 파일의 기본 구조를 숙지 하는 데는 몇 분 정도 걸리는 가치가 있습니다. 이 섹션에서는 검토, 편집 또는 프로젝트 파일을 만들 때 발생 하는 보다 일반적인 요소의 개요를 제공 합니다. 특히 알아봅니다.

- 사용 하는 방법 *속성* 빌드 프로세스에 대 한 변수를 관리할 수 있습니다.
- 사용 하는 방법 *항목* 다음과 같은 코드 파일은 빌드 프로세스에 대 한 입력을 식별 합니다.
- 사용 하는 방법 *대상* 하 고 *작업* msbuild를 실행 지침을 제공 하를 사용 하 여 *속성* 및 *항목* 에서 다른 곳에서 정의 프로젝트 파일입니다.

MSBuild 프로젝트 파일의 주요 요소 간의 관계를 보여 줍니다.

![](understanding-the-project-file/_static/image2.png)

### <a name="the-project-element"></a>프로젝트 요소

합니다 [프로젝트](https://msdn.microsoft.com/library/bcxfsh87.aspx) 요소는 모든 프로젝트 파일의 루트 요소입니다. 프로젝트 파일에 대 한 XML 스키마를 식별 하는 것 외에도 합니다 **프로젝트** 요소는 빌드 프로세스에 대 한 진입점을 지정 하는 특성을 포함할 수 있습니다. 예를 들어, 합니다 [Contact Manager 샘플 솔루션](the-contact-manager-solution.md)의 *Publish.proj* 파일 이라는 대상을 호출 하 여 빌드를 시작 해야 함을 지정 **FullPublish**합니다.


[!code-xml[Main](understanding-the-project-file/samples/sample1.xml)]


### <a name="properties-and-conditions"></a>속성 및 조건

일반적으로 프로젝트 파일을 성공적으로 빌드 및 프로젝트를 배포 하기 위해 다양 한 정보를 많이 제공 해야 합니다. 이러한 정보에는 서버 이름, 연결 문자열, 자격 증명, 빌드 구성, 원본 및 대상 파일 경로 및 사용자 지정을 지원 하려면 포함 하려는 모든 기타 정보에 포함할 수 있습니다. 프로젝트 파일 속성 내에서 정의 되어야 합니다는 [PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx) 요소입니다. MSBuild 속성의 키-값 쌍으로 구성 됩니다. 내 합니다 **PropertyGroup** 속성 키를 정의 하는 요소, 요소 이름 및 속성 값을 정의 하는 요소의 콘텐츠입니다. 예를 들어, 명명 된 속성을 정의할 수 있습니다 **ServerName** 하 고 **ConnectionString** 정적 서버 이름 및 연결 문자열을 저장 합니다.


[!code-xml[Main](understanding-the-project-file/samples/sample2.xml)]


속성 값을 검색 하 형식을 사용 하면 <strong>$(</strong><em>PropertyName</em><strong>)</strong><em>.</em> 예를 들어의 값을 검색 하는 <strong>ServerName</strong> 속성 입력:


[!code-powershell[Main](understanding-the-project-file/samples/sample3.ps1)]


> [!NOTE]
> 방법의 예제 및이 항목의 뒷부분에 나오는 속성 값을 사용 하는 경우 볼 수 있습니다.


프로젝트 파일에서 정적 속성으로 정보를 포함 합니다. 아닌 경우 항상 빌드 프로세스를 관리 하는 이상적인 방법 많은 시나리오를 다른 원본에서 정보를 얻거나 궁극적인 목표는 사용자 명령 프롬프트에서 정보를 제공 합니다. MSBuild를 사용 하면 명령줄 매개 변수로 속성 값을 지정할 수 있습니다. 사용자 수에 대 한 값을 제공 하는 예를 들어 **ServerName** 실행 될 때 자신이 MSBuild.exe 명령줄에서.


[!code-console[Main](understanding-the-project-file/samples/sample4.cmd)]


> [!NOTE]
> MSBuild.exe를 사용 하 여 사용할 수 있습니다 스위치 인수에 대 한 자세한 내용은 참조 하세요. [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311.aspx)합니다.


환경 변수 및 기본 제공 프로젝트 속성의 값을 가져오려면 동일한 속성 구문을 사용할 수 있습니다. 일반적으로 사용 되는 속성에 많은 사용자에 대해 정의 된 및 관련 매개 변수 이름을 포함 하 여 프로젝트 파일에서 사용할 수 있습니다. 예를 들어, 현재 프로젝트 플랫폼을 검색할&#x2014;예를 들어 **x86** 또는 **AnyCpu**&#x2014;포함 될 수 있습니다 합니다 **$** 에서 속성 참조 프로젝트 파일입니다. 자세한 내용은 [빌드 명령 및 속성 매크로](https://msdn.microsoft.com/library/c02as0cs.aspx)를 [일반적인 MSBuild 프로젝트 속성](https://msdn.microsoft.com/library/bb629394.aspx), 및 [예약 된 속성](https://msdn.microsoft.com/library/ms164309.aspx)합니다.

속성은 종종 함께에서 사용 됩니다 *조건을*합니다. 대부분의 MSBuild 요소를 지원 합니다 **조건을** 기반이 MSBuild 요소를 평가 해야 하는 조건을 지정할 수 있는 특성입니다. 예를 들어이 속성 정을 것이 좋습니다.


[!code-xml[Main](understanding-the-project-file/samples/sample5.xml)]


MSBuild는이 속성 정의 처리할 때 먼저 확인 하 여부를 **$(OutputRoot)** 속성 값을 사용할 수 있습니다. 속성 값이 비어 있으면&#x2014;즉, 사용자 되지 않은이 속성에 제공 된 값이&#x2014;조건이 **true** 속성 값을로 설정 됩니다 **... \Publish\Out**합니다. 사용자에서는이 속성에 대 한 값을 제공 하는 경우 조건이 **false** 정적 속성 값이 사용 되지 않습니다.

다양 한 조건을 지정 하는 방법에 대 한 자세한 내용은 참조 하세요. [MSBuild 조건](https://msdn.microsoft.com/library/7szfhaft.aspx)합니다.

### <a name="items-and-item-groups"></a>항목 및 항목 그룹

프로젝트 파일의 중요 한 역할 중 하나는 빌드 프로세스에 대 한 입력을 정의 하는 것입니다. 일반적으로 이러한 입력 파일이&#x2014;코드 파일, 구성 파일에서 명령 파일 및 다른 파일을 처리 하거나로 복사 해야 하는 빌드 프로세스의 일부입니다. MSBuild 프로젝트 스키마를이 입력 하 여 표시 됩니다 [항목](https://msdn.microsoft.com/library/ms164283.aspx) 요소입니다. 프로젝트 파일에서 항목 내에서 정의 해야 합니다는 [ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx) 요소입니다. 마찬가지로 **속성** 요소에 이름을 지정할 수 있습니다는 **항목** 요소 원하는 대로 정할 수 있습니다. 그러나 지정 해야 합니다는 **Include** 파일 또는 항목을 나타내는 와일드 카드를 식별 하는 특성입니다.


[!code-xml[Main](understanding-the-project-file/samples/sample6.xml)]


여러 번 지정 하 여 **항목** 동일한 이름의 요소를 효과적으로 만드는 리소스의 명명된 된 목록입니다. 작업에서이 확인 하려면 Visual Studio에서 생성 하는 프로젝트 파일 중 하나에 대해 알아보겠습니다는 것이 좋습니다. 예를 들어 합니다 *ContactManager.Mvc.csproj* 샘플 솔루션의 파일에는 각각 동일한 이름의 여러 항목 그룹을 많이 포함 **항목** 요소입니다.


[!code-xml[Main](understanding-the-project-file/samples/sample7.xml)]


이러한 방식으로 프로젝트 파일을 동일한 방식으로 처리 해야 하는 파일 목록을 생성 하는 MSBuild 지시는&#x2014;는 **참조** 목록은 성공적인 빌드를 한 곳에 있어야 하는 어셈블리를  **컴파일** 컴파일해야 하는 코드 파일을 포함 하는 목록 및 **콘텐츠** 목록에는 변경 되지 않은 상태로 복사 되어야 하는 리소스가 포함 됩니다. 빌드 프로세스 참조 및이 항목 뒷부분의 해당이 항목을 사용 하는 방법을 살펴보겠습니다.

항목 요소를 포함할 수도 [ItemMetadata](https://msdn.microsoft.com/library/ms164284.aspx) 자식 요소입니다. 이러한 사용자 정의 키-값 쌍 이며 기본적으로 해당 항목에 관련 된 속성을 나타냅니다. 예를 들어, 많은 합니다 **컴파일** 프로젝트 파일의 항목 요소에 포함 되어 **DependentUpon** 자식 요소입니다.


[!code-xml[Main](understanding-the-project-file/samples/sample8.xml)]


> [!NOTE]
> 사용자가 만든 항목 메타 데이터 외에 모든 항목 생성 시 공용 다양 한 메타 데이터가 할당 됩니다. 자세한 내용은 [잘 알려진 항목 메타데이터](https://msdn.microsoft.com/library/ms164313.aspx)를 참조하세요.


만들 수 있습니다 **ItemGroup** 루트 수준 내의 요소 **프로젝트** 요소 또는 특정 내 **대상** 요소입니다. **ItemGroup** 요소 기능도 **조건** 프로젝트 구성 또는 플랫폼와 같은 조건에 따라 빌드 프로세스에 대 한 입력을 조정할 수 있는 특성입니다.

### <a name="targets-and-tasks"></a>대상 및 작업

MSBuild 스키마에는 [태스크](https://msdn.microsoft.com/library/77f2hx1s.aspx) 요소는 개별 빌드 명령 (또는 작업)을 나타냅니다. MSBuild는 다양 한 미리 정의 된 작업을 포함합니다. 예를 들어:

- 합니다 **복사** 태스크를 새 위치로 파일을 복사 합니다.
- 합니다 **Csc** Visual C# 컴파일러를 호출 하는 작업입니다.
- 합니다 **Vbc** Visual Basic 컴파일러를 호출 하는 작업입니다.
- 합니다 **Exec** 작업이 지정된 된 프로그램을 실행 합니다.
- 합니다 **메시지** 태스크로 거에 메시지를 씁니다.

> [!NOTE]
> 기본적으로 사용할 수 있는 작업의 전체 세부 정보를 참조 하세요 [MSBuild 작업 참조](https://msdn.microsoft.com/library/7z253716.aspx)합니다. 사용자 고유의 사용자 지정 작업을 만드는 방법을 비롯 한 태스크에 대 한 자세한 내용은 참조 하세요 [MSBuild 작업](https://msdn.microsoft.com/library/ms171466.aspx)합니다.


작업에 항상 포함 되어야 합니다 [대상](https://msdn.microsoft.com/library/t50z2hka.aspx) 요소입니다. A **대상** 요소는 순차적으로 실행 되는 하나 이상의 작업 집합이 며 프로젝트 파일에는 여러 대상이 포함 될 수 있습니다. 작업 또는 작업 집합을 실행 하려는 경우 포함 된 대상을 호출 합니다. 예를 들어, 메시지를 기록 하는 간단한 프로젝트 파일이 있다고 가정 합니다.


[!code-xml[Main](understanding-the-project-file/samples/sample9.xml)]


명령줄에서 대상을 사용 하 여 호출할 수 있습니다 합니다 **/t** 대상을 지정 하는 스위치입니다.


[!code-console[Main](understanding-the-project-file/samples/sample10.cmd)]


추가할 수 있습니다는 **DefaultTargets** 특성을 합니다 **프로젝트** 요소를 호출 하려는 대상을 지정 합니다.


[!code-xml[Main](understanding-the-project-file/samples/sample11.xml)]


이 경우 명령줄에서 대상을 지정할 필요가 없습니다. 프로젝트 파일을 간단히 지정할 수 있습니다 및 MSBuild를 호출 합니다 **FullPublish** 를 대상입니다.


[!code-console[Main](understanding-the-project-file/samples/sample12.cmd)]


대상 및 작업을 모두 포함 될 수 있습니다 **조건을** 특성입니다. 따라서 특정 조건이 충족 될 경우 전체 대상 또는 개별 태스크를 생략할 수 있습니다.

일반적으로 유용한 작업 및 목표를 만든 경우에 속성 및 프로젝트 파일의 다른 곳에서 정의 된 항목을 참조 해야 합니다.

- 속성 값을 사용 하려면 입력 <strong>$(</strong><em>PropertyName</em><strong>)</strong>여기서 <em>PropertyName</em> 이름인는 <strong>속성</strong> 요소 또는 매개 변수의 이름입니다.
- 항목을 사용 하려면 입력 <strong>@(</strong><em>ItemName</em><strong>)</strong>여기서 <em>ItemName</em> 이름인 합니다 <strong>항목</strong> 요소.

> [!NOTE]
> 동일한 이름의 여러 항목을 만드는 경우 목록 작성 하 고 기억 합니다. 반면, 동일한 이름의 여러 속성을 만드는 경우 마지막 속성 값을 입력 해야 이전 속성 덮어씁니다 동일한 이름을 가진&#x2014;속성을 단일 값을 포함할 수 있습니다.


예를 들어,를 *Publish.proj* 샘플 솔루션에서 파일을 살펴봅니다 합니다 **BuildProjects** 대상입니다.


[!code-xml[Main](understanding-the-project-file/samples/sample13.xml)]


이 샘플에서는 이러한 요점을 확인할 수 있습니다.

- 경우는 **BuildingInTeamBuild** 매개 변수를 지정 하 고 값이 **true**, 어떤이 대상 내의 작업이 실행 되지 것입니다.
- 대상의 단일 인스턴스가 포함 된 [MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx) 작업 합니다. 이 태스크를 사용 하면 다른 MSBuild 프로젝트를 빌드할 수 있습니다.
- 합니다 **ProjectsToBuild** 항목 작업에 전달 됩니다. 이 항목에서 정의 된 모든 프로젝트 또는 솔루션 파일의 목록을 나타낼 수 있습니다 **ProjectsToBuild** 항목 그룹 내에서 요소 항목입니다. 이 경우에 **ProjectsToBuild** 항목에서 참조 하는 단일 솔루션 파일입니다.

    [!code-xml[Main](understanding-the-project-file/samples/sample14.xml)]
- 에 전달 된 속성 값을 **MSBuild** 명명 된 매개 변수를 포함 하는 태스크 **OutputRoot** 및 **구성**합니다. 이러한 값은 하지 않은 경우 제공 되는 경우 매개 변수 값 또는 정적 속성 값으로 설정 됩니다.

    [!code-xml[Main](understanding-the-project-file/samples/sample15.xml)]

도 볼 수 있습니다 합니다 **MSBuild** 라는 대상이 호출 하는 태스크 **빌드**합니다. 널리 사용 되는 사용자 지정 프로젝트 파일에 제공 되며 Visual Studio 프로젝트 파일에서 같은 몇 가지 기본 제공 대상 중 하나인 **빌드**를 **정리**, **다시**, 및 **게시**합니다. 대상 및 작업에 대 한 빌드 프로세스 제어를 사용 하 여 자세히 알아봅니다 합니다 **MSBuild** 특히,이 항목의 뒷부분에 나오는 작업 합니다.

> [!NOTE]
> 대상에 대 한 자세한 내용은 참조 하세요. [MSBuild 대상](https://msdn.microsoft.com/library/ms171462.aspx)합니다.


## <a name="splitting-project-files-to-support-multiple-environments"></a>여러 환경을 지원 하도록 프로젝트 파일 분

프로덕션 환경, 테스트 서버 및 스테이징 플랫폼 등 여러 환경에 솔루션을 배포할 수 있게 되기를 한다고 가정 합니다. 구성을 이러한 환경 간에 크게 달라질 수 있습니다&#x2014;뿐만 아니라 서버 이름, 연결 문자열 및 등 측면에서 뿐만 아니라 자격 증명, 보안 설정 및 기타 요인의 많은 측면에서 잠재적으로 합니다. 이 작업을 정기적으로 수행 해야 할 경우 대상 환경 전환 될 때마다 프로젝트 파일의 여러 속성을 편집 하려면 실제로 합당 아닙니다. 속성 값은 빌드 프로세스에 제공 되는 무한 목록이 필요에 적합 한 솔루션을 것도 아닙니다.

다행히는 대안입니다. MSBuild를 사용 하면 빌드 구성에 여러 프로젝트 파일에 걸쳐 분할할 수 있습니다. 작동 방식을 보려면이, 샘플 솔루션에서는 두 개의 사용자 지정 프로젝트 파일이 있는지를 확인 합니다.

- *Publish.proj*속성, 항목을 포함 하는, 및 모든 환경에 공통적으로 적용 되는 대상입니다.
- *Env Dev.proj*, 개발자 환경에 관련 된 속성을 포함 하는 합니다.

이제 있음을 합니다 *Publish.proj* 파일에는 [가져오기](https://msdn.microsoft.com/library/92x05xfs.aspx) 여 바로 아래에 있는 요소를 **프로젝트** 태그.


[!code-xml[Main](understanding-the-project-file/samples/sample16.xml)]


**가져올** 다른 MSBuild 프로젝트 파일의 내용을 현재 MSBuild 프로젝트 파일을 가져올 요소를 사용 합니다. 이 경우에 **TargetEnvPropsFile** 매개 변수를 가져올 프로젝트 파일의 파일 이름을 제공 합니다. MSBuild를 실행할 때이 매개 변수에 대 한 값을 제공할 수 있습니다.


[!code-console[Main](understanding-the-project-file/samples/sample17.cmd)]


이 두 파일의 내용을 단일 프로젝트 파일에 효과적으로 병합합니다. 이 방법을 사용 하면 유니버설 빌드 구성에 포함 된 프로젝트 파일 및 환경 관련 속성을 포함 하는 여러 보조 프로젝트 파일을 만들 수 있습니다. 결과적으로, 다른 매개 변수 값을 사용 하 여 명령을 실행 하기만 하면 다른 환경으로 솔루션을 배포할 수 있습니다.

![](understanding-the-project-file/_static/image3.png)

이 방식으로 프로젝트 파일을 분할은 따라야 하는 것이 좋습니다. 개발자가 여러 프로젝트 파일에서 유니버설 빌드 속성의 중복을 방지 하는 동안 단일 명령을 실행 하 여 여러 환경에 배포할 수 있습니다.

> [!NOTE]
> 사용자 고유의 서버 환경에 대 한 환경 관련 프로젝트 파일 사용자 지정 하는 방법에 대 한 지침을 참조 하세요 [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)합니다.


## <a name="conclusion"></a>결론

이 항목에서는 MSBuild 프로젝트 파일에 대 한 일반 소개를 제공 하 고 빌드 프로세스를 제어 하려면 사용자 고유의 사용자 지정 프로젝트 파일을 만드는 방법을 설명 합니다. 또한 범용 빌드 지침 및 환경별 빌드 속성을 쉽게 빌드 및 여러 대상에 프로젝트를 배포 하려면 프로젝트 파일을 분할할 개념이 도입 되었습니다.

다음 항목인 [빌드 프로세스를 이해](understanding-the-build-process.md), 현실적인 수준의 복잡성을 사용 하 여 솔루션의 배포를 통해 컨트롤 빌드 및 배포 하기 위해 프로젝트 파일을 사용 하는 방법을에 대 한 자세한 정보를 제공 합니다.

## <a name="further-reading"></a>추가 정보

WPP 및 프로젝트 파일에 대 한 자세한 소개를 참조 하세요. [Microsoft 빌드 엔진 내:를 사용 하 여 MSBuild 및 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi William Bartholomew, ISBN: 978-0-7356-4524-0입니다.

> [!div class="step-by-step"]
> [이전](setting-up-the-contact-manager-solution.md)
> [다음](understanding-the-build-process.md)
