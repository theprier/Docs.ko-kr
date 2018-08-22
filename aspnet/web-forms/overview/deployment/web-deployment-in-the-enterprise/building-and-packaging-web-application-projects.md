---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
title: 빌드 및 웹 응용 프로그램 프로젝트를 패키징 | Microsoft Docs
author: jrjlee
description: 원격 서버 환경에 웹 응용 프로그램 프로젝트를 배포 하려는 경우 첫 번째 작업 프로젝트를 빌드하고 웹 배포 팩을 생성 하는 중...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 94e92f80-a7e3-4d18-9375-ff8be5d666ac
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
msc.type: authoredcontent
ms.openlocfilehash: 406b8e6daf47196eb98700efe41e34c02d5682d3
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823736"
---
<a name="building-and-packaging-web-application-projects"></a>빌드 및 웹 응용 프로그램 프로젝트를 패키징
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 원격 서버 환경에 웹 응용 프로그램 프로젝트를 배포 하려는 경우 먼저 프로젝트를 빌드하고 웹 배포 패키지를 생성 하는 합니다. 이 항목에서는 웹 응용 프로그램 프로젝트에 대 한 빌드 프로세스의 작동 방식을 설명 합니다. 특히, 설명:
> 
> - 어떻게 웹 게시 파이프라인 (WPP) 배포 기능을 포함 하는 빌드 프로세스를 확장 합니다.
> - 어떻게 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 배포 패키지에 웹 응용 프로그램을 설정 합니다.
> - 빌드 및 패키징 프로세스 작동 방식 및 생성 되는 파일입니다.


Visual Studio 2010에서 웹 응용 프로그램 프로젝트 빌드 및 배포 프로세스는 WPP에서 지원 됩니다. WPP은 MSBuild의 기능을 확장 하 고 웹 배포를 통합할 수 있도록 하는 Microsoft Build Engine (MSBuild) 대상 집합을 제공 합니다. Visual Studio 내에서 웹 응용 프로그램 프로젝트에 대 한 속성 페이지에서이 확장된 기능을 볼 수 있습니다. 합니다 **웹 패키지 및 게시** 페이지와 함께 합니다 **SQL 패키지 및 게시** 페이지 빌드 프로세스가 완료 되 면 웹 응용 프로그램 프로젝트 배포를 위해 패키지 하는 방법을 구성할 수 있습니다.

![](building-and-packaging-web-application-projects/_static/image1.png)

## <a name="how-does-the-wpp-work"></a>WPP는 어떻게 작동 하나요?

C# 프로젝트 파일에서 확인을 수행한-기반된 웹 응용 프로그램 프로젝트를 두.targets 파일을 가져오는 것을 볼 수 있습니다.


[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample1.xml)]


첫 번째 **가져오기** 문은 모든 Visual C# 프로젝트에 공통적으로 적용 됩니다. 이 파일 *Microsoft.CSharp.targets*, Visual C#에 관련 된 작업 및 대상을 포함 합니다. 예를 들어 C# 컴파일러 (**Csc**) 여기에 작업을 호출 합니다. 합니다 *Microsoft.CSharp.targets* 가져오기 파일에 *Microsoft.Common.targets* 파일입니다. 같은 모든 프로젝트에 공통 되는 대상을 정의 합니다. **빌드**, **Rebuild**를 **실행**, **컴파일**, 및 **정리** . 두 번째 **가져오기** 문을 웹 응용 프로그램 프로젝트에 따라 다릅니다. 합니다 *Microsoft.WebApplication.targets* 가져오기 파일에 *Microsoft.Web.Publishing.targets* 파일입니다. 합니다 *Microsoft.Web.Publishing.targets* 기본적으로 파일 *는* WPP 합니다. 같은 대상 정의 **패키지** 하 고 **MSDeployPublish**, 다양 한 배포 작업을 완료 하려면 웹 배포를 호출 하는 합니다.

Contact Manager 샘플 솔루션에서는 이러한 추가 대상을 사용 하는 방법을 이해 하려면 엽니다는 *Publish.proj* 파일을 살펴보겠습니다를 **BuildProjects** 대상입니다.


[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample2.xml)]


이 대상을 사용 하 여 **MSBuild** 다양 한 프로젝트를 빌드하는 작업입니다. 표시 된 **DeployOnBuild** 하 고 **DeployTarget** 속성:

- 합니다 **DeployOnBuild = true** 속성이 기본적으로 "빌드가 성공적으로 완료 될 때 추가 된 대상을 실행 하려고 합니다."을 의미
- **DeployTarget** 를 실행할 때 대상의 이름을 식별 합니다 **DeployOnBuild** 속성이 **true**합니다. MSBuild를 실행 한다고 지정 하는 경우에 **패키지** 프로젝트를 빌드한 후 대상입니다.

**패키지** 대상이에 정의 된 *Microsoft.Web.Publishing.targets* 파일. 기본적으로,이 대상 웹 응용 프로그램 프로젝트의 빌드 출력 및 IIS 웹 서버에 게시할 수 있는 웹 배포 패키지를 변환 합니다.

> [!NOTE]
> 프로젝트 파일을 보려면 (예를 들어 <em>ContactManager.Mvc.csproj</em>) Visual Studio 2010에서는 먼저 솔루션에서 프로젝트를 언로드합니다. 에 <strong>솔루션 탐색기</strong> 창에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭 <strong>프로젝트 언로드</strong>합니다. 프로젝트 노드를 다시 마우스 오른쪽 단추로 누른 <strong>편집할</strong><em>[프로젝트 파일]</em>). 프로젝트 파일은 원시 XML 형식으로 열립니다. 완료 되 면 프로젝트를 다시 로드 해야 합니다.  
> MSBuild 대상 작업에 대 한 자세한 내용은 및 <strong>가져오기</strong> 문의 [프로젝트 파일 이해](understanding-the-project-file.md)합니다. WPP 및 프로젝트 파일에 대 한 자세한 소개를 참조 하세요. [Microsoft 빌드 엔진 내:를 사용 하 여 MSBuild 및 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi William Bartholomew, ISBN: 978-0-7356-4524-0입니다.


## <a name="what-is-a-web-deployment-package"></a>웹 배포 패키지란?

최종 결과 일반적으로 빌드하고 Visual Studio 2010을 사용 하 여 또는 MSBuild를 직접 사용 하 여 웹 응용 프로그램 프로젝트를 배포 하는 경우는 *웹 배포 패키지*합니다. 웹 배포 패키지는.zip 파일. IIS는 모든 포함 및 웹 응용 프로그램을 다시 만드는 데 필요한 웹 배포 포함:

- 콘텐츠, 리소스 파일, 구성 파일, JavaScript 및 연계 스타일 시트 (CSS) 리소스 및 등을 포함 하 여 웹 응용 프로그램의 컴파일된 출력입니다.
- 웹 응용 프로그램 프로젝트에 대 한 어셈블리에 대 한 솔루션 내의 프로젝트를 참조 합니다.
- 웹 응용 프로그램을 구축 하는 모든 데이터베이스를 생성 하는 SQL 스크립트입니다.

웹 배포 패키지를 생성 한 후에 다양 한 방법으로 IIS 웹 서버에 게시할 수 있습니다. 예를 들어, 웹 배포 원격 에이전트 서비스 또는 웹 배포 처리기는 대상 웹 서버를 대상으로 하 여 원격으로 배포할 수 있습니다 하거나 IIS 관리자를 사용 하 여 대상 웹 서버에서 패키지를 수동으로 가져올 수 있습니다. 배포에 이러한 방법에 대 한 자세한 내용은 참조 하세요. [웹 배포에 오른쪽 접근 방식을 선택](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)합니다.

## <a name="how-does-the-build-process-work"></a>빌드 프로세스는 어떻게 작동 하나요?

이 빌드 및 웹 응용 프로그램 프로젝트를 패키지 하는 경우 어떻게 되는지 보여 줍니다.

![](building-and-packaging-web-application-projects/_static/image2.png)

웹 응용 프로그램 프로젝트를 빌드할 때 빌드 프로세스 파일을 생성 *[프로젝트 이름]. SourceManifest.xml*합니다. 프로젝트 파일 및 빌드 출력을와 함께이 *합니다. SourceManifest.xml* 파일은 Web Deploy 웹 배포 패키지에 포함 해야 합니다. 이러한 입력을 사용 하 여, 라는 웹 배포 패키지 생성 Web Deploy *[프로젝트 이름].zip*합니다.

웹 배포 패키지와 함께 빌드 프로세스에서는 패키지를 사용 하는 데 도움이 되는 두 개의 파일을 생성 합니다.

- 합니다 *. deploy.cmd* 파일 원격 IIS 웹 서버에 웹 배포 패키지를 게시 하는 매개 변수가 있는 Web Deploy (MSDeploy.exe) 명령 집합을 포함 합니다. 실행 합니다 *. deploy.cmd* 적절 한 매개 변수를 사용 하 여 파일을 일반적으로 빠르게 제공 및 쉽게 대체는 MSDeploy.exe를 수동으로 생성 명령을 직접.
- 합니다 *SetParameters.xml* 파일 MSDeploy.exe 명령에 매개 변수 값 집합을 제공 합니다. 이러한 값은 IIS 웹 응용 프로그램을 배포할 패키지를 모든 서비스 끝점의 값 및 연결 문자열에 정의 된 이름 등의 속성을 *web.config* 파일 및 배포 속성 프로젝트 속성 페이지에 정의 된 값입니다.

합니다 *SetParameters.xml* 파일은 배포 프로세스를 관리 하는 키입니다. 이 파일은 웹 응용 프로그램 프로젝트의 내용에 따라 동적으로 생성 됩니다. 예를 들어, 연결 문자열을 추가 하는 경우에 *web.config* 파일을 빌드 프로세스는 자동으로 연결 문자열을 검색, 배포를 그에 따라 매개 변수화 및에 항목을 생성 합니다  *SetParameters.xml* 파일을 배포 프로세스의 일부로 연결 문자열을 수정할 수 있습니다. 다음 항목인 [웹 패키지 배포용 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)자세히이 파일의 역할에 설명 하 고는 수정할 수 있습니다 빌드 및 배포 하는 동안 다양 한 방법에 설명 합니다.

> [!NOTE]
> Visual Studio 2010에서는 WPP 지원 하지 않습니다 패키징 전에 웹 응용 프로그램 페이지 미리 컴파일. 다음 버전의 Visual Studio 및 WPP 패키징 옵션으로 웹 응용 프로그램을 미리 컴파일하는 기능이 포함 됩니다.


## <a name="conclusion"></a>결론

이 항목에서는 Visual Studio 2010에서 웹 응용 프로그램 프로젝트 빌드 및 패키징 프로세스의 개요를 제공 합니다. WPP MSBuild, 웹 배포 명령을 호출할 수 있습니다 하는 방법을 설명 하 고 빌드 및 패키징 프로세스 작동 방식 설명 했습니다.

웹 배포 패키지를 만든 후 다음 단계는 배포 하는입니다. 이 대 한 자세한 내용은 참조 하세요. [웹 패키지 배포용 매개 변수 구성](configuring-parameters-for-web-package-deployment.md) 하 고 [웹 패키지 배포](deploying-web-packages.md)합니다.

## <a name="further-reading"></a>추가 정보

이 자습서에서는 다음 항목 [웹 패키지 배포용 매개 변수 구성](configuring-parameters-for-web-package-deployment.md) 하 고 [웹 패키지 배포](deploying-web-packages.md), 만든 웹 패키지를 사용 하는 방법에 지침을 제공 합니다. 이 시리즈의 마지막 자습서 [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md), 사용자 지정 및 패키징 프로세스 문제를 해결 하는 방법에 대 한 지침을 제공 합니다.

WPP 및 프로젝트 파일에 대 한 자세한 소개를 참조 하세요. [Microsoft 빌드 엔진 내:를 사용 하 여 MSBuild 및 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi William Bartholomew, ISBN: 978-0-7356-4524-0입니다.

> [!div class="step-by-step"]
> [이전](understanding-the-build-process.md)
> [다음](configuring-parameters-for-web-package-deployment.md)
