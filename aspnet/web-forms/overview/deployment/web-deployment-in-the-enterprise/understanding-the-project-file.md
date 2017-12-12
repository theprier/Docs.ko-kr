---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
title: "프로젝트 파일을 이해 | Microsoft Docs"
author: jrjlee
description: "Microsoft Build Engine (MSBuild) 프로젝트 파일은 빌드 및 배포 프로세스의 핵심 에합니다. 이 항목의 MSBuild에 대해 개념적으로 시작 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 07978d9d-341c-4524-bcba-62976f390f77
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
msc.type: authoredcontent
ms.openlocfilehash: 8d0f9604529db9cf4ee5d333450a551e46e6ba4f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="understanding-the-project-file"></a>프로젝트 파일 이해
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Microsoft Build Engine (MSBuild) 프로젝트 파일은 빌드 및 배포 프로세스의 핵심 에합니다. 이 항목에 대해 개념적으로 프로젝트 파일과 MSBuild로 시작합니다. 가로질러 예가 프로젝트 파일을 사용 하 여 실제 응용 프로그램을 배포 하는 방법을 통해 작동 하 고 프로젝트 파일을 사용 하 여 작업할 때 핵심 구성 요소를 설명 합니다.
> 
> 학습 내용:
> 
> - 어떻게 MSBuild는 프로젝트를 빌드하기 위해 MSBuild 프로젝트 파일을 사용 합니다.
> - 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)와 같은 배포 기술이, MSBuild 통합 방법
> - 프로젝트 파일의 주요 구성 요소를 이해 하는 방법입니다.
> - 어떻게 프로젝트 파일을 빌드 및 복잡 한 응용 프로그램 배포에 사용할 수 있습니다.


## <a name="msbuild-and-the-project-file"></a>MSBuild 및 프로젝트 파일

만들고 Visual Studio에서 솔루션을 빌드할 때 Visual Studio 솔루션의 각 프로젝트를 빌드하려면 MSBuild를 사용 합니다. 파일 확장명이 프로젝트 & #x 2014의 유형을 반영 하는 MSBuild 프로젝트 파일; 예를 들어 C# 프로젝트 (.csproj), Visual Basic.NET 프로젝트 (.vbproj) 또는 데이터베이스 프로젝트 (.dbproj) 모든 Visual Studio 프로젝트에 포함 되어 있습니다. MSBuild는 프로젝트를 빌드하려면 프로젝트와 연결 된 프로젝트 파일을 처리 해야 합니다. 프로젝트 파일은 모든 정보 및 MSBuild 플랫폼 요구 사항, 버전 관리 정보, 웹 서버 또는 데이터베이스 서버 설정을 포함 하도록 콘텐츠와 마찬가지로 프로젝트를 구축 하기 위해 필요한는 지침을 포함 하는 XML 문서 및 작업을 수행 해야 합니다.

MSBuild 프로젝트 파일 기반으로 [MSBuild XML 스키마](https://msdn.microsoft.com/en-us/library/5dy88c2e.aspx), 따라서 빌드 프로세스는 완전히 열리고 투명 하 고 있습니다. 또한 MSBuild 엔진 & #x 2014 사용 하려면 Visual Studio를 설치할 필요가 없습니다; MSBuild.exe 실행 파일은.NET Framework의 일부 및 명령 프롬프트에서 실행할 수 있습니다. 개발자의 경우 MSBuild XML 스키마를 사용 하 여 프로젝트 빌드 및 배포 정교 하 고 세분화 된 제어를 적용 하려면 사용자 고유의 MSBuild 프로젝트 파일을 만들 수 있습니다. 이러한 사용자 지정 프로젝트 파일이 Visual Studio를 자동으로 생성 되는 프로젝트 파일과 같은 방식에서 작동 합니다.

> [!NOTE]
> 팀 빌드 서비스에서 Team Foundation Server (TFS)와 MSBuild 프로젝트 파일을 사용할 수도 있습니다. 예를 들어 배포를 자동화 하는 테스트 환경에 새 코드를 체크 인할 때 CI (연속 통합) 시나리오에서 프로젝트 파일을 사용할 수 있습니다. 자세한 내용은 참조 [자동화 된 웹 배포를 위해 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다.


### <a name="project-file-naming-conventions"></a>프로젝트 파일 명명 규칙

사용자 고유의 프로젝트 파일을 만들 때 원하는 파일 확장명을 사용할 수 있습니다. 그러나 솔루션을 다른 사람이 이해 하기 간단 하 게 하려면 이러한 일반적인 규칙을 사용 해야 합니다.

- 프로젝트를 작성 하는 프로젝트 파일을 만들 때.proj 확장을 사용 합니다.
- 다른 프로젝트 파일로 가져올 다시 사용할 수 있는 프로젝트 파일을 만들 때.targets 확장을 사용 합니다. .Targets 확장명을 가진 파일 일반적으로 하지 않는 빌드 아무 것도 자체, 단순히 포함.proj 파일로 가져올 수 있는 지침입니다.

### <a name="integration-with-deployment-technologies"></a>배포 기술과 통합

ASP.NET 웹 응용 프로그램 및 ASP.NET MVC 웹 응용 프로그램과 같은 Visual Studio 2010에서 웹 응용 프로그램 프로젝트와 함께 사용한 경우 이러한 프로젝트 패키징 및 대상 환경에 웹 응용 프로그램 배포에 대 한 기본 제공 지원이 포함 되어 있는지 알 수 있습니다. **속성** 페이지에 이러한 프로젝트에 포함 되어 **웹 패키지 및 게시** 및 **SQL 패키지 및 게시** 탭을 구성 하는 데 사용할 수 있는 방법의 구성 요소 프로그램 응용 프로그램 패키지 되 고 배포 합니다. 이 표시는 **웹 패키지 및 게시** 탭:

![](understanding-the-project-file/_static/image1.png)

이러한 기능은 기본 기술으로 웹 게시 파이프라인 (WPP) 라고 합니다. WPP MSBuild를 기본적으로 제공 하 고 [웹 배포](https://go.microsoft.com/?linkid=9805122) 웹 응용 프로그램에 대 한 전체 빌드, 패키지 및 배포 프로세스를 제공 하기 위해 함께 합니다.

다행히도 WPP 웹 프로젝트에 대 한 사용자 지정 프로젝트 파일을 만들 때 제공 하는 통합 지점의 이용 수입니다. 프로젝트 웹 배포 패키지를 만들 빌드하고 단일 프로젝트 파일과 MSBuild 한 번 호출을 통해 원격 서버에 이러한 패키지를 설치할 수 있는 프로젝트 파일의 배포 지침을 포함할 수 있습니다. 또한 빌드 프로세스의 일부로 다른 실행 파일을 호출할 수 있습니다. 예를 들어 스키마 파일에서 데이터베이스를 배포 하려면 VSDBCMD.exe 명령줄 도구를 실행할 수 있습니다. 이 항목의 과정 동안 있습니다 사용할 수 있는 방법을 엔터프라이즈 배포 시나리오의 요구 사항을 충족 하기 위해 이러한 기능을 볼 수 있습니다.

> [!NOTE]
> 웹 응용 프로그램 배포 프로세스의 작동 방법에 대 한 자세한 내용은 참조 하십시오. [ASP.NET 웹 응용 프로그램 프로젝트 배포 개요](https://msdn.microsoft.com/en-us/library/dd394698.aspx)합니다.


## <a name="the-anatomy-of-a-project-file"></a>프로젝트 파일의 구조

빌드 프로세스의 자세한 보기 전에 MSBuild 프로젝트 파일의 기본 구조를 파악 하는 몇 분 정도 가치가 됩니다. 이 섹션에서는 검토, 편집 또는 프로젝트 파일을 만들 때 발생 하는 보다 일반적인 요소의 개요를 제공 합니다. 특히, 방법을 살펴봅니다.

- 사용 하는 방법 *속성* 빌드 프로세스에 대 한 변수를 관리할 수 있습니다.
- 사용 하는 방법 *항목* 다음과 같은 코드 파일을 빌드 프로세스에 대 한 입력을 식별 합니다.
- 사용 하는 방법 *대상* 및 *작업* MSBuild를 실행 지침을 제공 하기를 사용 하 여 *속성* 및 *항목* 다른 위치에서 정의 프로젝트 파일입니다.

MSBuild 프로젝트 파일의 주요 요소 간의 관계를 보여 줍니다.

![](understanding-the-project-file/_static/image2.png)

### <a name="the-project-element"></a>프로젝트 요소

[프로젝트](https://msdn.microsoft.com/en-us/library/bcxfsh87.aspx) 요소는 모든 프로젝트 파일의 루트 요소입니다. 프로젝트 파일에 대 한 XML 스키마를 식별 하는 것 외에도 **프로젝트** 요소 특성을 지정 하는 빌드 프로세스에 대 한 진입점을 포함할 수 있습니다. 예를 들어는 [않아 샘플 솔루션](the-contact-manager-solution.md), *Publish.proj* 파일 빌드 대상 명명 된를 호출 하 여 시작 해야 함을 지정 **FullPublish**합니다.


[!code-xml[Main](understanding-the-project-file/samples/sample1.xml)]


### <a name="properties-and-conditions"></a>속성 및 조건

일반적으로 프로젝트 파일을 성공적으로 빌드 및 프로젝트를 배포 하려면 정보의 다양 한 요소를 많이 제공 해야 합니다. 이러한 정보를이 바탕 서버 이름, 연결 문자열, 자격 증명, 빌드 구성, 원본 및 대상 파일 경로 및 사용자 지정을 지원 하기 위해 포함 시킬 다른 정보가 포함 될 수 있습니다. 프로젝트 파일에서 속성 내에서 정의 해야 합니다는 [PropertyGroup](https://msdn.microsoft.com/en-us/library/t4w159bs.aspx) 요소입니다. MSBuild 속성 키-값 쌍으로 구성 됩니다. 내에서 **PropertyGroup** 요소, 요소 이름 속성 키를 정의 하 고 요소의 콘텐츠 속성 값을 정의 합니다. 명명 된 속성을 정의할 수는 예를 들어 **ServerName** 및 **ConnectionString** 정적 서버 이름 및 연결 문자열을 저장 합니다.


[!code-xml[Main](understanding-the-project-file/samples/sample2.xml)]


형식을 사용 하면 속성 값을 검색 하려면 **$(***PropertyName***)***.* 예를 들어의 값을 검색 하는 **ServerName** 속성 입력:


[!code-powershell[Main](understanding-the-project-file/samples/sample3.ps1)]


> [!NOTE]
> 이 항목의 뒷부분에 나오는 속성 값을 사용 하는 시기와 방법의 예제에 표시 됩니다.


프로젝트 파일에 포함 하는 정적 속성으로 정보는 항상 빌드 프로세스를 관리 하는 데 이상적인 접근 방법. 많은 시나리오에서 다른 소스에서 정보를 얻거나 명령 프롬프트에서 정보를 제공 하도록 사용자 권한 부여 합니다. MSBuild를 사용 하면 명령줄 매개 변수가 모든 속성 값을 지정할 수 있습니다. 사용자에 대 한 값을 제공할 수는 예를 들어 **ServerName** 실행 될 때 자신이 MSBuild.exe 명령줄에서.


[!code-console[Main](understanding-the-project-file/samples/sample4.cmd)]


> [!NOTE]
> 인수 및 스위치 MSBuild.exe로 사용할 수 있습니다에 대 한 자세한 내용은 참조 하십시오. [MSBuild 명령줄 참조](https://msdn.microsoft.com/en-us/library/ms164311.aspx)합니다.


환경 변수 및 기본 제공 프로젝트 속성의 값을 가져오려면 동일한 속성 구문을 사용할 수 있습니다. 일반적으로 사용 되는 속성의 많은 사용자에 대해 정의 된 및 관련 매개 변수 이름을 포함 하 여 프로젝트 파일에서 사용할 수 있습니다. 예를 들어, 검색할 현재 프로젝트 플랫폼 & #x 2014; 예를 들어 **x86** 또는 **AnyCpu**& #x 2014; 포함할 수 있습니다는 **$(Platform)** 에서 속성 참조 프로젝트 파일입니다. 자세한 내용은 참조 [빌드 명령 및 속성 매크로](https://msdn.microsoft.com/en-us/library/c02as0cs.aspx), [일반적인 MSBuild 프로젝트 속성](https://msdn.microsoft.com/en-us/library/bb629394.aspx), 및 [예약 속성](https://msdn.microsoft.com/en-us/library/ms164309.aspx)합니다.

속성을 함께에서 사용 종종 *조건*합니다. MSBuild 요소는 대부분 지원는 **조건** 특성으로, MSBuild는 요소를 평가 해야 하는 조건을 지정할 수 있습니다. 예를 들어이 속성 정을 것이 좋습니다.


[!code-xml[Main](understanding-the-project-file/samples/sample5.xml)]


MSBuild 속성 정의이 처리할 때 먼저 확인 하 여부는 **$(OutputRoot)** 속성 값을 사용할 수 있습니다. 속성 값이 빈 값 & #x 2014; 즉, 사용자 하지 않은 지정 된 값이 속성 & #x 2014에 대 한; 조건이 **true** 속성 값으로 설정 되 고 **... \Publish\Out**합니다. 이 속성에 대 한 값을 입력 조건이 **false** 고 정적 속성 값이 사용 되지 않습니다.

조건을 지정할 수 있는 다양 한 방법에 대 한 자세한 내용은 참조 하십시오. [MSBuild 조건](https://msdn.microsoft.com/en-us/library/7szfhaft.aspx)합니다.

### <a name="items-and-item-groups"></a>항목 및 항목 그룹

프로젝트 파일의 중요 한 역할 중 하나는 빌드 프로세스에 대 한 입력을 정의 하는 것입니다. 일반적으로 이러한 입력 파일 & #x 2014; 코드 파일과 구성 파일, 명령 파일을 처리 하거나로 복사 해야 하는 다른 파일 부 빌드 프로세스의 합니다. MSBuild 프로젝트 스키마에서이 입력으로 표시 됩니다 [항목](https://msdn.microsoft.com/en-us/library/ms164283.aspx) 요소입니다. 프로젝트 파일 항목 내에서 정의 되어야 합니다는 [ItemGroup](https://msdn.microsoft.com/en-us/library/646dk05y.aspx) 요소입니다. 그러나 마찬가지로 **속성** 이름을 지정할 수 있습니다 요소는 **항목** 요소 원하는 합니다. 그러나 지정 해야 합니다는 **Include** 파일이 나 항목이 나타내는 와일드 카드를 식별 하는 특성입니다.


[!code-xml[Main](understanding-the-project-file/samples/sample6.xml)]


여러 번 지정 하 여 **항목** 동일한 이름 가진 요소를 효과적으로 만드는 리소스의 명명된 된 목록입니다. 이 방법이 작동 되는지 확인 하는 데는 Visual Studio에서 생성 하는 프로젝트 파일 중 하나에 대해 알아보겠습니다. 예를 들어는 *ContactManager.Mvc.csproj* 파일 샘플 솔루션에 동일한 이름의 여러 각 항목 그룹을 많이 포함 **항목** 요소입니다.


[!code-xml[Main](understanding-the-project-file/samples/sample7.xml)]


이러한 방식으로 프로젝트 파일에는 동일한 방식으로 & #x 2014; 처리 해야 하는 파일의 목록을 생성 하는 MSBuild 지시은 **참조** 목록에는 성공적인빌드용준비해야하는어셈블리**컴파일** 을 컴파일해야 하는 코드 파일을 포함 하는 목록 및 **콘텐츠** 변경 되지 않고 복사 해야 하는 리소스 목록에 포함 됩니다. 빌드 프로세스의 참조와 이러한 항목을 사용 하 여이 항목의 뒷부분에 나오는 방법을 살펴보겠습니다.

항목 요소를 포함할 수도 [ItemMetadata](https://msdn.microsoft.com/en-us/library/ms164284.aspx) 자식 요소입니다. 이러한 사용자 정의 키-값 쌍 이며 기본적으로 해당 항목에 관련 된 속성을 나타냅니다. 예를 들어 많은 **컴파일** 항목 요소는 프로젝트 파일에는 **DependentUpon** 자식 요소입니다.


[!code-xml[Main](understanding-the-project-file/samples/sample8.xml)]


> [!NOTE]
> 사용자가 만든 항목 메타 데이터 외에도 모든 항목 생성 시 다양 한 일반 메타 데이터를 할당 됩니다. 자세한 내용은 [잘 알려진 항목 메타데이터](https://msdn.microsoft.com/en-us/library/ms164313.aspx)를 참조하세요.


만들 수 있습니다 **ItemGroup** 루트 수준 내에서 요소 **프로젝트** 요소 또는 특정 내 **대상** 요소입니다. **ItemGroup** 요소도 지원 **조건** 특성 프로젝트 구성 또는 플랫폼와 같은 조건에 따라 빌드 프로세스에 대 한 입력을 조정할 수 있습니다.

### <a name="targets-and-tasks"></a>대상 및 작업

MSBuild 스키마에는 [작업](https://msdn.microsoft.com/en-us/library/77f2hx1s.aspx) 요소는 개별 빌드 명령 (또는 작업)을 나타냅니다. MSBuild는 다양 한 미리 정의 된 작업을 포함합니다. 예:

- **복사** 작업을 새 위치로 파일을 복사 합니다.
- **Csc** Visual C# 컴파일러를 호출 하는 작업입니다.
- **Vbc** Visual Basic 컴파일러를 호출 하는 작업입니다.
- **Exec** 작업이 지정된 된 프로그램을 실행 합니다.
- **메시지** 작업 메시지로 거를 씁니다.

> [!NOTE]
> 곧바로 사용할 수 있는 작업의 전체 정보를 참조 하십시오. [MSBuild 작업 참조](https://msdn.microsoft.com/en-us/library/7z253716.aspx)합니다. 작업을 사용자 지정 작업을 만드는 방법에 대 한 자세한 내용은 참조 [MSBuild 작업](https://msdn.microsoft.com/en-us/library/ms171466.aspx)합니다.


작업에 항상 포함 되어야 합니다 [대상](https://msdn.microsoft.com/en-us/library/t50z2hka.aspx) 요소입니다. A **대상** 요소는 일련의 순차적으로 실행 되는 하나 이상의 작업 및 프로젝트 파일에는 여러 대상이 포함 될 수 있습니다. 작업 또는 작업 집합을 실행 하려는 경우 포함 된 대상을 호출 합니다. 예를 들어 메시지를 기록 하는 간단한 프로젝트 파일을 있다고 가정 합니다.


[!code-xml[Main](understanding-the-project-file/samples/sample9.xml)]


명령줄에서 대상을 사용 하 여 호출할 수 있습니다는 **/t** 대상을 지정 하는 스위치입니다.


[!code-console[Main](understanding-the-project-file/samples/sample10.cmd)]


추가할 수 있습니다는 **DefaultTargets** 특성을 **프로젝트** 요소를 호출 하려면 대상을 지정 합니다.


[!code-xml[Main](understanding-the-project-file/samples/sample11.xml)]


이 경우 명령줄에서 대상을 지정할 필요가 없습니다. 프로젝트 파일을 간단히 지정할 수 있으며 MSBuild를 호출 합니다는 **FullPublish** 대상에 있습니다.


[!code-console[Main](understanding-the-project-file/samples/sample12.cmd)]


대상 및 작업을 모두 포함할 수 **조건** 특성입니다. 따라서 특정 조건이 충족 될 경우 전체 대상 또는 개별 작업을 생략할 수 있습니다.

일반적으로 유용한 작업 및 목표를 만들 때에 속성 및 프로젝트 파일에서 다른 곳에서 정의 된 항목을 참조 해야:

- 속성 값을 사용 하려면 입력 **$(***PropertyName***)**여기서 *PropertyName* 의 이름인는 **속성** 요소 또는 매개 변수의 이름입니다.
- 항목을 사용 하려면 입력 **@(***ItemName***)**여기서 *ItemName* 의 이름인는 **항목** 요소입니다.

> [!NOTE]
> 동일한 이름을 가진 여러 항목을 만들 목록을 작성 하 기억 합니다. 반면, 마지막 속성 값을 제공와 이름이 같은 & #x 2014 이전 속성을 덮어씁니다 동일한 이름을 가진 여러 속성을 만드는 경우; 속성에는 단일 값을 포함할 수 있습니다.


예를 들어는 *Publish.proj* 샘플 솔루션에 파일을 살펴보세요는 **BuildProjects** 대상입니다.


[!code-xml[Main](understanding-the-project-file/samples/sample13.xml)]


이 샘플에서는 이러한 핵심 사항을 확인할 수 있습니다.

- 경우는 **BuildingInTeamBuild** 매개 변수를 지정 하 고 값이 **true**, 어떤이 대상 내의 태스크 실행 되지 것입니다.
- 대상의 단일 인스턴스가 포함 된 [MSBuild](https://msdn.microsoft.com/en-us/library/z7f65y0d.aspx) 작업 합니다. 이 태스크를 사용 하면 다른 MSBuild 프로젝트를 빌드할 수 있습니다.
- **ProjectsToBuild** 항목 작업에 전달 됩니다. 이 항목에서 정의 된 모든 프로젝트 또는 솔루션 파일의 목록을 나타낼 수 **ProjectsToBuild** 항목 그룹 내에서 요소를 항목입니다. 이 경우에 **ProjectsToBuild** 항목에서 참조 하는 단일 솔루션 파일입니다.

    [!code-xml[Main](understanding-the-project-file/samples/sample14.xml)]
- 에 전달 된 속성 값은 **MSBuild** 명명 된 매개 변수를 포함 하는 작업 **OutputRoot** 및 **구성**합니다. 그렇지 않은 경우 이러한 값이 제공 되는 경우 매개 변수 값 또는 정적 속성 값으로 설정 됩니다.

    [!code-xml[Main](understanding-the-project-file/samples/sample15.xml)]

볼 수는 **MSBuild** 이라는 대상을 호출 하면 **빌드**합니다. 이 널리 사용 되는 Visual Studio 프로젝트 파일 및 사용자 지정 프로젝트 파일에서 사용할 수에서 같은 몇 가지 기본 제공 대상 중 하나 **빌드**, **Clean**, **다시작성**, 및 **게시**합니다. 대상 및 빌드 프로세스를 제어 하 고에 대 한 작업을 사용 하는 방법에 대 한 자세히 알아보세요는 **MSBuild** 특히,이 항목의 뒷부분에 나오는 작업 합니다.

> [!NOTE]
> 대상에 대 한 자세한 내용은 참조 하십시오. [MSBuild 대상](https://msdn.microsoft.com/en-us/library/ms171462.aspx)합니다.


## <a name="splitting-project-files-to-support-multiple-environments"></a>여러 환경을 지원 하기 위해 프로젝트 파일 분

솔루션을 테스트 서버, 준비 플랫폼 및 프로덕션 환경 같은 여러 환경을 배포할 수 있게 되기를 한다고 가정 합니다. 구성을 이러한 환경 & #x 2014 간에 크게 달라질 수 있습니다; 뿐만 아니라 서버 이름, 연결 문자열 및 등의 관점에서 뿐만 아니라 자격 증명, 보안 설정 및 기타 요인의 많은 측면에서 잠재적으로 합니다. 이 작업을 정기적으로 수행 해야 할 경우 대상 환경을 전환할 때마다 프로젝트 파일의 여러 속성을 편집 하려면 실제로 편리있지 않습니다. 무한 목록이 빌드 프로세스에 제공 되는 속성 값을 요구 하도록 이상적인 솔루션 것도 아닙니다.

다행히 대안이 있습니다. MSBuild를 사용 하면 여러 프로젝트 파일에서 빌드 구성을 분할할 수 있습니다. 어떻게 작동 하는지, 샘플 솔루션에 두 개의 사용자 지정 프로젝트 파일은을 확인 합니다.

- *Publish.proj*, 속성, 항목을 포함 하 고 모든 환경에 공통적으로 적용 되는 대상입니다.
- *Env Dev.proj*, 개발자 환경에 관련 된 속성을 포함 하 합니다.

이제 다음에 유의 *Publish.proj* 파일에 포함 되어는 [가져오기](https://msdn.microsoft.com/en-us/library/92x05xfs.aspx) 열기 바로 아래에 있는 요소 **프로젝트** 태그입니다.


[!code-xml[Main](understanding-the-project-file/samples/sample16.xml)]


**가져올** 요소가 현재 MSBuild 프로젝트 파일에 다른 MSBuild 프로젝트 파일의 내용을 가져오기 위해 사용 됩니다. 이 경우에 **TargetEnvPropsFile** 매개 변수를 가져올 프로젝트 파일의 파일 이름을 제공 합니다. MSBuild를 실행할 때이 매개 변수에 대 한 값을 제공할 수 있습니다.


[!code-console[Main](understanding-the-project-file/samples/sample17.cmd)]


이 두 파일의 내용을 단일 프로젝트 파일에 효과적으로 병합합니다. 이 방식에서는 유니버설 빌드 구성에 포함 된 하나의 프로젝트 파일 및 환경 관련 속성을 포함 하는 여러 보조 프로젝트 파일을 만들 수 있습니다. 결과적으로, 다른 매개 변수 값으로 명령을 실행 하기만 하면 다른 환경에 솔루션을 배포할 수 있습니다.

![](understanding-the-project-file/_static/image3.png)

이러한 방식으로 프로젝트 파일 분할은 따라야 하는 것이 좋습니다. 개발자가 여러 프로젝트 파일에서 유니버설 빌드 속성의 중복을 피하는 단일 명령을 실행 하 여 여러 환경에 배포할 수 있습니다.

> [!NOTE]
> 사용자 고유의 서버 환경에 대 한 환경 관련 프로젝트 파일 사용자 지정 하는 방법에 대 한 지침을 참조 하십시오. [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)합니다.


## <a name="conclusion"></a>결론

이 항목 MSBuild 프로젝트 파일에 대 한 일반 소개를 제공 하 고 빌드 프로세스 제어 기능을 해당 하는 사용자 지정 프로젝트 파일을 만드는 방법을 설명 합니다. 또한 프로젝트 파일에 유니버설 빌드 지침 및 환경별 빌드 속성을 쉽게 빌드하고 여러 대상에 프로젝트를 배포할 수 있도록 분할의 개념을 소개 합니다.

다음 항목인 [빌드 프로세스를 이해](understanding-the-build-process.md)를 볼 수 있게 현실적인 수준의 복잡 한 솔루션의 배포를 통해 제어 빌드 및 배포 프로젝트 파일을 사용 하는 방법을 제공 합니다.

## <a name="further-reading"></a>추가 정보

프로젝트 파일 및 WPP에 대 한 자세한 소개를 참조 하십시오. [Microsoft Build Engine 안에: MSBuild를 사용 하 여 및 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi 및 William Bartholomew, ISBN: 978-0-7356-4524-0입니다.

>[!div class="step-by-step"]
[이전](setting-up-the-contact-manager-solution.md)
[다음](understanding-the-build-process.md)
