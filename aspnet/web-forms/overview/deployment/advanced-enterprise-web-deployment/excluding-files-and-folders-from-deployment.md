---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
title: 배포에서 파일 및 폴더 제외 | Microsoft Docs
author: jrjlee
description: 이 설명 하는 방법에서 제외할 수 있습니다 파일 및 폴더 웹 배포 패키지를 빌드하고 웹 응용 프로그램 프로젝트를 패키지 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: f4cc2d40-6a78-429b-b06f-07d000d4caad
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
msc.type: authoredcontent
ms.openlocfilehash: c50352d423f41f84677dbf048e74088214340f3a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37382584"
---
<a name="excluding-files-and-folders-from-deployment"></a>배포에서 파일 및 폴더 제외
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 설명 하는 방법에서 제외할 수 있습니다 파일 및 폴더 웹 배포 패키지를 빌드하고 웹 응용 프로그램 프로젝트를 패키지 합니다.


이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.

이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="overview"></a>개요

Visual Studio 2010에서 웹 응용 프로그램 프로젝트를 빌드할 때 웹 게시 파이프라인 (WPP) 대 한 웹 배포 가능한 패키지로 컴파일된 웹 응용 프로그램 패키지를 빌드 프로세스를 확장할 수 있습니다. 원격 IIS 웹 서버에이 웹 패키지를 배포 하려면 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하거나 수동으로 IIS 관리자를 통해 웹 패키지를 가져올 수 있습니다. 이 패키징 프로세스는 설명 [빌드 및 패키징 웹 응용 프로그램 프로젝트](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)합니다.

그렇다면 어떻게 웹에 포함 된 항목을 가져옵니다 제어 하려면 패키지? 많은 시나리오에 대 한 충분 한 제어를 제공 하는 기본 프로젝트 파일을 통해 Visual Studio에서 프로젝트 설정 합니다. 그러나 일부 경우 특정 대상 환경에 웹 패키지의 콘텐츠를 조정 하려는 합니다. 예를 들어, 다음 응용 프로그램 테스트 환경에 배포 해도 스테이징 또는 프로덕션 환경에 응용 프로그램을 배포 하는 경우 폴더를 제외 하는 경우 로그 파일에 대 한 폴더를 포함 하는 것이 좋습니다. 이 항목에서는이 작업을 수행 하는 방법을 보여줍니다.

## <a name="what-gets-included-by-default"></a>기본적으로 포함 가져옵니다 무엇입니까?

Visual Studio에서 웹 응용 프로그램 프로젝트 속성을 구성한 경우는 **배포할 항목** 목록에 **웹 패키지 및 게시** 페이지에서는 웹 배포에 포함 하도록 지정할 수 있습니다 패키지입니다. 기본적으로이 설정은 **이 응용 프로그램을 실행 하는 데 필요한 파일만**합니다.

![](excluding-files-and-folders-from-deployment/_static/image1.png)

선택 하는 경우 **이 응용 프로그램을 실행 하는 데 필요한 파일만**, WPP 웹 패키지에 추가할 파일을 확인 하려고 합니다. 여기에는 다음이 포함됩니다.

- 프로젝트에 대 한 모든 빌드 출력 합니다.
- 빌드 작업을 사용 하 여 모든 파일 표시 **콘텐츠**합니다.

> [!NOTE]
> 포함할 파일을 결정 하는 논리는이 파일에 포함 되어 있습니다.   
> *%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ Microsoft.Web.Publishing.OnlyFilesToRunTheApp.targets*


## <a name="excluding-specific-files-and-folders"></a>특정 파일 및 폴더 제외

일부 경우에는 파일 및 폴더는 배포 보다 세부적으로 제어를 해야 합니다. 앞 제외 하려는 파일 시간을 알고 있고 제외를 모든 대상 환경에 적용 됩니다, 설정 하기만 하면 됩니다 합니다 **빌드 작업** 각 파일의 **None**합니다.

**배포에서 특정 파일을 제외 하려면**

1. 에 **솔루션 탐색기** 창에서 파일을 마우스 오른쪽 단추로 클릭 **속성**합니다.
2. 에 **속성** 창에서를 **빌드 작업** 행을 선택 **None**합니다.

그러나이 방법은 항상 편리한 것은 아닙니다. 예를 들어 파일을 변경 하는 것이 좋습니다 및 폴더는 대상 환경에 따라 Visual Studio 외부에서 포함 합니다. 예를 들어 Contact Manager 샘플 솔루션에서 ContactManager.Mvc 프로젝트의 내용 살펴봅니다를 수행 합니다.

![](excluding-files-and-folders-from-deployment/_static/image2.png)

- 내부 폴더 만들기, 삭제 및 개발을 위해 로컬 데이터베이스를 채우는 데 사용 하는 개발자는 몇 가지 SQL 스크립트를 포함 합니다. 이 폴더의 경우 nothing 스테이징 또는 프로덕션 환경에 배포 되어야 합니다.
- 스크립트 폴더에는 몇 가지 JavaScript 파일이 있습니다. 이러한 파일이 많이 디버깅을 지원 하거나 Visual Studio에서 IntelliSense 제공 순수 하 게 포함 되어 있습니다. 이러한 파일 중 일부를 스테이징 또는 프로덕션 환경에 배포 하지 말아야 합니다. 그러나 다음 문제 해결 용이 하 게 하는 개발자 테스트 환경에 배포 하는 것이 좋습니다.

특정 파일 및 폴더 제외 하려면 프로젝트 파일을 조작할 수 있습니다, 있지만 쉬운 방법이 있습니다. WPP 라는 항목 목록을 작성 하 여 파일 및 폴더를 제외 하는 메커니즘을 포함 **ExcludeFromPackageFolders** 하 고 **ExcludeFromPackageFiles**합니다. 이러한 목록에 고유한 항목을 추가 하 여이 메커니즘을 확장할 수 있습니다. 이렇게 하려면 다음 대략적인 단계를 완료 해야 합니다.

1. 라는 사용자 지정 프로젝트 파일을 만듭니다 *[프로젝트 이름].wpp.targets* 프로젝트 파일과 동일한 폴더에 있습니다.

    > [!NOTE]
    > 합니다 *. wpp.targets* 파일을 웹 응용 프로그램 프로젝트 파일과 동일한 폴더에 이동 해야&#x2014;예를 들어 *ContactManager.Mvc.csproj*&#x2014;아닌 같은 사용자 지정 폴더 프로젝트 파일을 사용 하면 빌드 및 배포 프로세스를 제어할 수 있습니다.
2. 에 *. wpp.targets* 파일을 추가 **ItemGroup** 요소입니다.
3. 에 **ItemGroup** 요소를 추가 **ExcludeFromPackageFolders** 하 고 **ExcludeFromPackageFiles** 특정 파일 및 필요에 따라 폴더를 제외할 항목을 합니다.

이 기본 구조가 *. wpp.targets* 파일:


[!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample1.xml)]


각 항목 라는 항목 메타 데이터 요소를 포함 하는 참고 **FromTarget**합니다. 이 값은 빌드 프로세스를 영향을 주지는 선택적 값 단순히 특정 파일 또는 폴더 생략 된 이유를 나타내는 데 사용 되 빌드 로그를 검토 하는 사용자가 하는 경우.

## <a name="excluding-files-and-folders-from-a-web-package"></a>웹 패키지에서 파일 및 폴더 제외

다음 절차는 추가 하는 방법을 보여 줍니다.는 *. wpp.targets* 파일 웹 응용 프로그램 프로젝트 및 파일을 사용 하 여 프로젝트를 빌드할 때 웹 패키지에서 특정 파일 및 폴더를 제외 하는 방법입니다.

**웹 배포 패키지에서 파일 및 폴더를 제외 하려면**

1. Visual Studio 2010에서 솔루션을 엽니다.
2. 에 **솔루션 탐색기** 창에서 웹 응용 프로그램 프로젝트 노드를 마우스 오른쪽 단추로 클릭 (예를 들어 **ContactManager.Mvc**), 가리킵니다 **추가**, 클릭하고**새 항목**합니다.
3. 에 **새 항목 추가** 대화 상자를 선택 합니다 **XML 파일** 템플릿.
4. 에 **이름** 상자에 입력 *[프로젝트 이름] * * *.wpp.targets** (예를 들어 **ContactManager.Mvc.wpp.targets**)를 클릭 하 고 **추가**.

    ![](excluding-files-and-folders-from-deployment/_static/image3.png)

    > [!NOTE]
    > 새 항목을 프로젝트의 루트 노드로 추가 하는 경우 파일은 프로젝트 파일과 동일한 폴더에 생성 됩니다. Windows 탐색기에서 폴더를 열어이 확인할 수 있습니다.
5. 파일에 추가 된 **프로젝트** 요소와 **ItemGroup** 요소:

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample2.xml)]
6. 웹 패키지에서 폴더를 제외 하려는 경우 추가 된 **ExcludeFromPackageFolders** 요소를 **ItemGroup** 요소:

   1. 에 **Include** 특성을 제외 하려는 폴더의 세미콜론으로 구분 된 목록을 제공 합니다.
   2. 에 **FromTarget** 메타 데이터 요소를 의미 있는 이름와 같은 폴더 되 제외 이유를 나타내는 값을 제공 합니다 *. wpp.targets* 파일입니다.

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample3.xml)]
7. 웹 패키지에서 파일을 제외 하려는 경우 추가 된 **ExcludeFromPackageFiles** 요소를 **ItemGroup** 요소:

   1. 에 **Include** 특성을 제외 하려는 파일의 세미콜론으로 구분 된 목록을 제공 합니다.
   2. 에 **FromTarget** 메타 데이터 요소를 의미 있는 이름와 같은 파일 되 제외 이유를 나타내는 값을 제공 합니다 *. wpp.targets* 파일입니다.

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample4.xml)]
8. 합니다 *[프로젝트 이름].wpp.targets* 파일 이제는 다음과 유사 합니다.

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample5.xml)]
9. 저장 후 닫기 합니다 *[프로젝트 이름].wpp.targets* 파일입니다.

다음에 웹 응용 프로그램 프로젝트 빌드 및 패키지 있습니다, WPP가 자동으로 감지 합니다 *. wpp.targets* 파일입니다. 모든 파일 및 폴더를 지정한 웹 패키지에 포함 되지 않습니다.

## <a name="conclusion"></a>결론

이 항목에서는 사용자 지정을 만들어 웹 패키지를 빌드할 때 특정 파일 및 폴더를 제외 하는 방법 설명 *. wpp.targets* 웹 응용 프로그램 프로젝트 파일과 동일한 폴더에는 파일입니다.

## <a name="further-reading"></a>추가 정보

사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하에 대 한 자세한 내용은 참조 하세요. [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 하 고 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다. 패키징 및 배포 프로세스에 대 한 자세한 내용은 참조 하세요. [빌드 및 패키징 웹 응용 프로그램 프로젝트](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)하십시오 [웹 패키지 배포용 매개 변수 구성](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md), 및 [ 웹 패키지 배포](../web-deployment-in-the-enterprise/deploying-web-packages.md)합니다.

> [!div class="step-by-step"]
> [이전](deploying-membership-databases-to-enterprise-environments.md)
> [다음](taking-web-applications-offline-with-web-deploy.md)
