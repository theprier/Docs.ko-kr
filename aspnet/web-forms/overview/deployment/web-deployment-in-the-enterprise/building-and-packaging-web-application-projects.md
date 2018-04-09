---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
title: 빌드 및 웹 응용 프로그램 프로젝트를 패키지 | Microsoft Docs
author: jrjlee
description: 원격 서버 환경에는 웹 응용 프로그램 프로젝트를 배포 하려는 경우 첫 번째 작업 프로젝트를 빌드하고 웹 배포 팩을 생성 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 94e92f80-a7e3-4d18-9375-ff8be5d666ac
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
msc.type: authoredcontent
ms.openlocfilehash: d630e1776607bd0bd7c61e1f0f7234ef58c7533b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="building-and-packaging-web-application-projects"></a>빌드 및 웹 응용 프로그램 프로젝트를 패키지
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 원격 서버 환경에는 웹 응용 프로그램 프로젝트를 배포 하려는 경우 첫 번째 작업 프로젝트를 빌드하고 웹 배포 패키지를 생성 됩니다. 이 항목에서는 웹 응용 프로그램 프로젝트에 대 한 빌드 프로세스의 작동 방식에 대해 설명 합니다. 특히, 설명:
> 
> - 웹 게시 파이프라인 (WPP) 어떻게 배포 기능을 포함 하도록 빌드 프로세스를 확장 합니다.
> - 어떻게 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 배포 패키지에 웹 응용 프로그램을 설정 합니다.
> - 빌드 및 패키징 프로세스 작동 방식 및 어떤 파일이 만들어집니다.


Visual Studio 2010에서 웹 응용 프로그램 프로젝트 빌드 및 배포 프로세스는 WPP에서 지원 됩니다. WPP은 MSBuild의 기능을 확장 하 고 웹 배포와 통합할 수 있도록 하는 Microsoft Build Engine (MSBuild) 대상 집합을 제공 합니다. Visual Studio 내에서 웹 응용 프로그램 프로젝트에 대 한 속성 페이지에서이 확장 된 기능을 볼 수 있습니다. **웹 패키지 및 게시** 함께 페이지는 **SQL 패키지 및 게시** 페이지 빌드 프로세스가 완료 되 면 웹 응용 프로그램 프로젝트 배포를 위해 패키지 하는 방법을 구성할 수 있습니다.

![](building-and-packaging-web-application-projects/_static/image1.png)

## <a name="how-does-the-wpp-work"></a>WPP 어떻게 작동 합니까?

C#에 대 한 프로젝트 파일에서 확인을 수행한-기반된 웹 응용 프로그램 프로젝트에서는 두 개의.targets 파일을 가져오는 것을 볼 수 있습니다.


[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample1.xml)]


첫 번째 **가져오기** 문이 모든 Visual C# 프로젝트에 공통적으로 적용 됩니다. 이 파일을 *Microsoft.CSharp.targets*, 대상 및 Visual C#에 관련 된 작업을 포함 합니다. 예를 들어 C# 컴파일러 (**Csc**) 여기에 작업을 호출 합니다. *Microsoft.CSharp.targets* 가져오기 파일에 *Microsoft.Common.targets* 파일입니다. 마찬가지로 모든 프로젝트에 공통 된 대상을 정의 합니다. **빌드**, **다시 작성**, **실행**, **컴파일**, 및 **정리** . 두 번째 **가져오기** 문을 웹 응용 프로그램 프로젝트와 관련이 있습니다. *Microsoft.WebApplication.targets* 가져오기 파일에 *Microsoft.Web.Publishing.targets* 파일입니다. *Microsoft.Web.Publishing.targets* 기본적으로 파일 *은* WPP 합니다. 대상에 같은 정의 **패키지** 및 **MSDeployPublish**, 다양 한 배포 작업을 완료 하기 위해 Web Deploy를 호출 하는 합니다.

열고 않아 샘플 솔루션에 이러한 추가 대상을 사용 하는 방식을 이해 하는 *Publish.proj* 파일을 살펴보세요는 **BuildProjects** 대상입니다.


[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample2.xml)]


이 대상을 사용 하 여는 **MSBuild** 다양 한 프로젝트를 빌드하는 작업입니다. 공지는 **DeployOnBuild** 및 **DeployTarget** 속성:

- **DeployOnBuild = true** 속성을 의미 "빌드가 성공적으로 완료 될 때 추가 대상 실행 하고자 합니다."
- **DeployTarget** 속성을 실행할 때 대상의 이름을 식별 하는 **DeployOnBuild** 속성이 **true**합니다. MSBuild에서 실행 되도록 지정 하는 경우에 **패키지** 프로젝트를 빌드한 후 대상입니다.

**패키지** 대상이에 정의 된 *Microsoft.Web.Publishing.targets* 파일입니다. 기본적으로,이 대상 웹 응용 프로그램 프로젝트의 빌드 출력 걸리며 IIS 웹 서버에 게시할 수 있는 웹 배포 패키지를로 변환 합니다.

> [!NOTE]
> 프로젝트 파일을 보려면 (예를 들어 <em>ContactManager.Mvc.csproj</em>) Visual Studio 2010에서 먼저 솔루션에서 프로젝트를 언로드합니다. 에 <strong>솔루션 탐색기</strong> 창에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭 <strong>프로젝트 언로드</strong>합니다. 다시 프로젝트 노드를 마우스 오른쪽 단추로 누른 <strong>편집</strong><em>[프로젝트 파일]</em>). 프로젝트 파일은 원시 XML 형식으로 열립니다. 완료 되 면 프로젝트를 다시 로드 해야 합니다.  
> MSBuild 대상, 작업에 대 한 자세한 내용은 및 <strong>가져오기</strong> 참조 [프로젝트 파일 이해](understanding-the-project-file.md)합니다. 프로젝트 파일 및 WPP에 대 한 자세한 소개를 참조 하십시오. [Microsoft Build Engine 안에: MSBuild를 사용 하 여 및 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi 및 William Bartholomew, ISBN: 978-0-7356-4524-0입니다.


## <a name="what-is-a-web-deployment-package"></a>웹 배포 패키지는 무엇입니까?

최종 결과 일반적으로 빌드하고 Visual Studio 2010을 사용 하거나 직접 MSBuild를 사용 하 여 웹 응용 프로그램 프로젝트를 배포 하는 경우는 *웹 배포 패키지*합니다. 웹 배포 패키지는.zip 파일. 포함 된 모든 IIS 웹 응용 프로그램을 다시 만드는 데 필요한 웹 배포 및 포함 하 여:

- 콘텐츠, 리소스 파일, 구성 파일, JavaScript 및 연계 스타일 시트 (CSS) 리소스 및 등을 포함 하 여 웹 응용 프로그램의 컴파일된 출력 합니다.
- 웹 응용 프로그램 프로젝트 및에 대 한 어셈블리 참조 솔루션 내의 프로젝트.
- 웹 응용 프로그램으로 배포 하는 모든 데이터베이스를 생성 하는 SQL 스크립트.

웹 배포 패키지 생성 되 면 다양 한 방법으로 IIS 웹 서버에 게시할 수 있습니다. 예를 들어, 웹 배포 원격 에이전트 서비스 또는 웹 배포 처리기 대상 웹 서버에서 대상으로 하 여 원격으로 배포할 수 있습니다 또는 IIS 관리자를 사용 하 여 대상 웹 서버에 패키지를 수동으로 가져올 수 있습니다. 배포에 이러한 방법에 대 한 자세한 내용은 참조 하십시오. [웹 배포에 대 한 오른쪽 접근 방식을 선택](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)합니다.

## <a name="how-does-the-build-process-work"></a>빌드 프로세스는 어떻게 작동 합니까?

이 패키지는 웹 응용 프로그램 프로젝트를 빌드할 때 동작을 보여 줍니다.

![](building-and-packaging-web-application-projects/_static/image2.png)

웹 응용 프로그램 프로젝트를 빌드할 때 빌드 프로세스 라는 파일이 생성 *[프로젝트 name]. SourceManifest.xml*합니다. 프로젝트 파일 및 빌드 출력과 함께이 *합니다. SourceManifest.xml* 파일을 통해 알 Web Deploy 웹 배포 패키지에 포함 해야 합니다. 이러한 입력을 사용 하 여, 라는 웹 배포 패키지를 생성 웹 배포 *[프로젝트 이름].zip*합니다.

웹 배포 패키지와 함께 빌드 프로세스에서는 패키지를 사용 하는 데 도움이 되는 두 개의 파일을 생성 합니다.

- *. deploy.cmd* 파일에 원격 IIS 웹 서버에 웹 배포 패키지를 게시 하는 매개 변수가 있는 Web Deploy (MSDeploy.exe) 명령 집합이 포함 되어 있습니다. 실행 된 *. deploy.cmd* 파일을 적절 한 매개 변수 일반적으로 더 빠르게 제공 및 쉽게 대체는 MSDeploy.exe를 수동으로 만들고 명령을 직접 합니다.
- *SetParameters.xml* 파일 MSDeploy.exe 명령에 매개 변수 값의 집합을 제공 합니다. IIS 웹 응용 프로그램을 배포할 패키지를 모든 서비스 끝점의 값 및 연결 문자열에 정의 된 이름과 같은 속성을 포함 하는 이러한 값은 *web.config* 파일 및 배포 속성 프로젝트 속성 페이지에 정의 된 값입니다.

*SetParameters.xml* 파일은 배포 프로세스를 관리 하는 키입니다. 이 파일은 웹 응용 프로그램 프로젝트의 내용에 따라 동적으로 생성 됩니다. 예를 들어, 연결 문자열을 추가 하는 경우 프로그램 *web.config* 파일, 빌드 프로세스는 자동으로 연결 문자열을 검색, 배포를 그에 따라 매개 변수화 및에서 항목을 만들는  *SetParameters.xml* 파일을 배포 프로세스의 일환으로 연결 문자열을 수정할 수 있습니다. 다음 항목인 [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)자세히이 파일의 역할에 설명 하 고는 수정할 수 있습니다 빌드 및 배포 하는 동안 여러 가지 방법을 설명 합니다.

> [!NOTE]
> Visual Studio 2010에서 WPP가 패키징 전에 웹 응용 프로그램 페이지 미리 컴파일으로 지원 하지 않습니다. 다음 버전의 Visual Studio 및 WPP 웹 응용 프로그램 패키징 옵션으로 미리 컴파일할 수 있는 권한이 포함 됩니다.


## <a name="conclusion"></a>결론

이 항목에서 Visual Studio 2010 웹 응용 프로그램 프로젝트 빌드 및 패키징 프로세스의 개요를 제공합니다. WPP MSBuild에서 웹 배포 명령을 호출할 수 있습니다 어떻게 설명 된 것 하 고 빌드 및 패키징 프로세스 작동 방식 설명 된 것입니다.

웹 배포 패키지를 만든 다음 단계는를 배포 합니다. 이 대 한 자세한 내용은 참조 하십시오. [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md) 및 [웹 패키지 배포](deploying-web-packages.md)합니다.

## <a name="further-reading"></a>추가 정보

이 자습서의 다음 항목에서는 [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md) 및 [웹 패키지 배포](deploying-web-packages.md)를 만든 후 웹 패키지를 사용 하는 방법에 지침을 제공 합니다. 이 시리즈의 최종 자습서 [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md), 사용자 지정 및 패키징 프로세스의 문제를 해결 하는 방법에 대 한 지침을 제공 합니다.

프로젝트 파일 및 WPP에 대 한 자세한 소개를 참조 하십시오. [Microsoft Build Engine 안에: MSBuild를 사용 하 여 및 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi 및 William Bartholomew, ISBN: 978-0-7356-4524-0입니다.

> [!div class="step-by-step"]
> [이전](understanding-the-build-process.md)
> [다음](configuring-parameters-for-web-package-deployment.md)
