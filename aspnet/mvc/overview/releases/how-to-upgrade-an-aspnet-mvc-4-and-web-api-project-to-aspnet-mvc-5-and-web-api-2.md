---
uid: mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2
title: 웹 API 프로젝트를 ASP.NET MVC 5 및 Web API 2 및 ASP.NET MVC 4를 업그레이드 하는 방법 | Microsoft Docs
author: Rick-Anderson
description: ASP.NET MVC 5 및 Web API 2의 새로운 기능을 특성이 라우팅, 인증 필터 및 등을 포함 하 여 호스트를 가져옵니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: db0d02d9-58e8-4a0b-8d7d-b8df8ea97b88
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: f61502933a5ba92896ee97cef9cff915fe23831d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2"></a>ASP.NET MVC 5 및 Web API 2에는 ASP.NET MVC 4 및 Web API 프로젝트를 업그레이드 하는 방법
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> ASP.NET MVC 5 및 Web API 2의 새로운 기능을 특성이 라우팅, 인증 필터 및 등을 포함 하 여 호스트를 가져옵니다. 참조 [ https://www.asp.net/vnext ](https://www.asp.net/core) 내용을 확인 합니다.
> 
> 이 연습에서는 응용 프로그램에서 최신 버전을 업그레이드 하는 데 필요한 단계를 안내 합니다.  
> 
> > [!NOTE]
> > 참조 하십시오 [ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보](../../../visual-studio/overview/2013/release-notes.md) 주요 다음 버전으로 MVC 4 및 Web API에서 변경 내용에 대 한 내용은 합니다.
> 
>   
> 
> 이 문서 Youngjune 홍콩 및 Rick Anderson 썼습니다 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )


## <a name="upgrade-steps"></a>업그레이드 단계

1. 프로젝트를 백업 합니다. 이 연습에서는 프로젝트 파일, 패키지 구성 및 web.config 파일에 변경 해야 합니다.
2. Global.asax의 웹 API에서 Web API 2로 업그레이드 하는 것에 대 한 변경:

    [!code-csharp[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample1.cs)]

   다음으로 변경:

    [!code-csharp[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample2.cs)]
3. 프로젝트를 사용 하는 모든 패키지 MVC 5 및 Web API 2와 호환 되는지 확인 합니다. 다음 표에서 MVC 4 및 Web API 관련 변경 해야 할 보다 패키지 합니다. 아래에 나열 된 패키지 중 하나에 종속 되어 있는 패키지를 사용 하는 경우 MVC 5와 Web API 2와 호환 되는 최신 버전을 가져올 게시자에 게 문의 하십시오. 이러한 패키지에 대 한 소스 코드를 있는 MVC 5와 Web API 2의 새로운 어셈블리와 함께 다시 컴파일합니다 해야 있습니다.   

    | **패키지 Id** | **이전 버전** | **새 버전** |
    | --- | --- | --- |
    | Microsoft.AspNet.Razor | 2.0.x.x | 3.0.0 |
    | Microsoft.AspNet.WebPages | 2.0.x.x | 3.0.0 |
    | Microsoft.AspNet.WebPages.WebData | 2.0.x.x | 3.0.0 |
    | Microsoft.AspNet.WebPages.OAuth | 2.0.x.x | 3.0.0 |
    | Microsoft.AspNet.Mvc | 4.0.x.x | 5.0.0 |
    | Microsoft.AspNet.Mvc.Facebook | 4.0.x.x | 5.0.0 |
    | Microsoft.AspNet.WebApi.Core | 4.0.x.x | 5.0.0 |
    | Microsoft.AspNet.WebApi.SelfHost | 4.0.x.x | 5.0.0 |
    | Microsoft.AspNet.WebApi.Client | 4.0.x.x | 5.0.0 |
    | Microsoft.AspNet.WebApi.OData | 4.0.x.x | 5.0.0 |
    | Microsoft.AspNet.WebApi | 4.0.x.x | 5.0.0 |
    | Microsoft.AspNet.WebApi.WebHost | 4.0.x.x | 5.0.0 |
    | Microsoft.AspNet.WebApi.Tracing | 4.0.x.x | 5.0.0 |
    | Microsoft.AspNet.WebApi.HelpPage | 4.0.x.x | 5.0.0 |
    | Microsoft.net.http | 2.0.x. | 2.2.x. |
    | Microsoft.Data.OData | 5.2.x | 5.6.x |
    | System.Spatial | 5.2.x | 5.6.x |
    | Microsoft.Data.Edm | 5.2.x | 5.6.x |
    | Microsoft.AspNet.Mvc.FixedDisplayModes | <o:p> </o:p> | 제거됨 |
    | Microsoft.AspNet.WebPages.Administration | <o:p> </o:p> | 제거됨 |
    | Microsoft-Web-Helpers | <o:p> </o:p> | Microsoft.AspNet.WebHelpers |

    > [!NOTE]
    > Microsoft 웹-도우미 Microsoft.AspNet.WebHelpers로 바뀌었습니다. 먼저, 이전 패키지를 제거 하 여 다음 최신 패키지를 설치 해야 합니다.   
    >   
    > ASP.NET의 주요 패키지 간에 교차 버전 호환성이 되지는 않습니다. 예를 들어 MVC 5는 Razor 3 및 Razor 2 하지 호환 됩니다.
4. Visual Studio 2013에서 프로젝트를 엽니다.
5. 설치 된 다음 ASP.NET NuGet 패키지를 제거 합니다. 패키지 관리자 콘솔 (PMC)를 사용 하 여이 제거 합니다. PMC를 열려면 선택 된 **도구** 메뉴를 선택 합니다 **라이브러리 패키지 관리자** 다음 선택 **패키지 관리자 콘솔**합니다. 프로젝트가이 모두 포함 되지 않을 수 있습니다.

    1. `Microsoft.AspNet.WebPages.Administration`  
   이 패키지는 MVC 3에서 MVC 4로 업그레이드 하는 경우에 일반적으로 추가 됩니다. 를 제거 하려면의 PMC에서 다음 명령을 실행:  
        `Uninstall-Package -Id Microsoft.AspNet.WebPages.Administration`
    2. `Microsoft-Web-Helpers`   
   이 패키지의으로 브랜드가 `Microsoft.AspNet.WebHelpers`합니다. 를 제거 하려면의 PMC에서 다음 명령을 실행:  
        `Uninstall-Package -Id Microsoft-Web-Helpers`
    3. `Microsoft.AspNet.Mvc.FixedDisplayMode`  
   이 패키지의 MVC 4 MVC 5에서 수정 된 버그에 대 한 해결을 포함 합니다. 를 제거 하려면의 PMC에서 다음 명령을 실행:  
        `Uninstall-Package -Id Microsoft.AspNet.Mvc.FixedDisplayModes`
6. PMC를 사용 하 여 모든 ASP.NET NuGet 패키지를 업그레이드 합니다. PMC에서 다음 명령을 실행 합니다.  
    `Update-Package`  
   `Update-Package` 명령 없이 매개 변수는 모든 패키지를 업데이트 합니다. 패키지 ID 인수를 사용 하 여 개별적으로 업데이트할 수 있습니다. 업데이트 명령에 대 한 자세한 내용은 실행 `get-help update-package` 합니다.

## <a name="update-the-application-webconfig-file"></a>응용 프로그램을 업데이트 *web.config* 파일

응용 프로그램에서 이러한 변경을 수행 해야 *web.config* 파일 없습니다는 *web.config* 파일에 *뷰* 폴더입니다.

찾은 `<runtime>/<assemblyBinding>` 섹션 및 다음과 같이 변경 합니다.

1. 이름 특성이 "System.Web.Mvc" 요소에서 "5.0.0.0"를 "4.0.0.0"에서 버전 번호를 변경 합니다. (해당 요소에서 두 변경 됩니다.)
2. Name 특성을 사용 하 여 요소에서 &quot;System.Web.Helpers "및 &quot;System.Web.WebPages&quot; "3.0.0.0 "를"2.0.0.0"에서 버전 번호를 변경 합니다. 4 개의 변경 내용은 적용 되며의 각 요소에 두 대.

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample3.xml?highlight=6,10,14)]
3. 찾은 `<appSettings>` 섹션 및 다음과 같이 3.0.0.0에 대 한 2.0.0.0.0 webpages:version 업데이트:

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample4.xml?highlight=2)]
4. 전체 이외의 모든 신뢰 수준을 제거 합니다. 예를 들어:

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample5.xml?highlight=2)]

## <a name="update-the-webconfig-files-under-the-views-folder"></a>업데이트는 *web.config* Views 폴더 아래에 있는 파일

응용 프로그램 영역을 사용 하는 경우 각 업데이트 해야 합니다 *web.config* 파일에 *뷰* 각 영역 폴더의 하위 폴더입니다.

1. 버전 "5.0.0.0" 버전 "4.0.0.0"에서 "System.Web.Mvc"를 포함 하는 모든 요소를 업데이트 합니다.  

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample6.xml?highlight=2)]

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample7.xml?highlight=4-6,8)]
2. 버전 "3.0.0.0" 버전 "2.0.0.0"에서 "system.web.webpages.razor"를 포함을 포함 하는 모든 요소를 업데이트 합니다. 이 섹션에 "System.Web.WebPages"이 있으면 해당 요소에서 버전 "2.0.0.0" 버전 "3.0.0.0"를 업데이트  

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample8.xml?highlight=3-5)]
3. 제거한 경우는 `Microsoft-Web-Helpers` 이전 단계에서 NuGet 패키지 설치 `Microsoft.AspNet.WebHelpers` 의 PMC에서 다음 명령을 사용 합니다.  
    `Install-Package -Id Microsoft.AspNet.WebHelpers`
4. 앱에서 사용 하는 경우는 [User.IsInRole()](https://msdn.microsoft.com/en-us/library/system.web.security.roleprincipal.isinrole(v=vs.110).aspx) 메서드를 추가 하려면 다음을는 *Web.config* 파일입니다.

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample9.xml)]

## <a name="final-steps"></a>마지막 단계는

빌드하고 응용 프로그램을 테스트 합니다.

프로젝트 파일에서 MVC 4 프로젝트 형식 GUID를 제거 합니다.

1. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 선택 **프로젝트 언로드**합니다.
2. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 편집 ProjectName.csproj를 선택 합니다.
3. 찾을 `ProjectTypeGuids` 요소를 선택한 다음 제거 MVC 4 프로젝트 GUID, `{E3E379DF-F4C6-4180-9B81-6769533ABE47}`합니다.
4. 저장 하 고 현재 열려 있는 프로젝트 파일을 닫습니다.
5. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **프로젝트 다시 로드**합니다.
