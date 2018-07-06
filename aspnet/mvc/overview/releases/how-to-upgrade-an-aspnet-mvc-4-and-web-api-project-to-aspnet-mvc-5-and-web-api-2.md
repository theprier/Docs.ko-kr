---
uid: mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2
title: 웹 API 프로젝트를 ASP.NET MVC 5 및 Web API 2 및 ASP.NET MVC 4를 업그레이드 하는 방법 | Microsoft Docs
author: Rick-Anderson
description: ASP.NET MVC 5 및 Web API 2 호스트 특성 라우팅, 인증 필터 및 등을 포함 하 여 새 기능을 제공 합니다.
ms.author: aspnetcontent
ms.date: 10/17/2013
ms.assetid: db0d02d9-58e8-4a0b-8d7d-b8df8ea97b88
msc.legacyurl: /mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 8a50c188a2283af46789739e710be69159799695
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37826746"
---
<a name="how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2"></a>ASP.NET MVC 5 및 Web API 2에는 ASP.NET MVC 4 및 Web API 프로젝트를 업그레이드 하는 방법
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> ASP.NET MVC 5 및 Web API 2 호스트 특성 라우팅, 인증 필터 및 등을 포함 하 여 새 기능을 제공 합니다. 참조 [ https://www.asp.net/vnext ](https://www.asp.net/core) 대 한 자세한 내용은 합니다.
> 
> 이 연습에서는 최신 버전으로 응용 프로그램을 업그레이드 하는 데 필요한 단계를 안내 합니다.  
> 
> > [!NOTE]
> > 참조 하세요 [ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보](../../../visual-studio/overview/2013/release-notes.md) 주요 MVC 4 및 Web API에서 다음 버전의 변경 내용에 대 한 정보에 대 한 합니다.
> 
>   
> 
> 이 문서는 Youngjune 홍콩 및 Rick Anderson으로 작성 되었습니다 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )


## <a name="upgrade-steps"></a>업그레이드 단계

1. 프로젝트를 백업 합니다. 이 연습에서는 프로젝트 파일, 패키지 구성 및 web.config 파일에 변경 가능 해야 합니다.
2. Global.asax의 Web API에서 Web API 2로 업그레이드를 변경 합니다.

    [!code-csharp[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample1.cs)]

   다음으로 변경:

    [!code-csharp[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample2.cs)]
3. 프로젝트를 사용 하는 모든 패키지 MVC 5 및 Web API 2와 호환 되는지 확인 합니다. 다음 테이블에서는 MVC 4 및 Web API를 변경 해야 하는 보다 패키지와 관련 된 합니다. 아래에 나열 된 패키지 중 하나에 종속 된 패키지에 있는 MVC 5 및 Web API 2와 호환 되는 최신 버전을 가져오는 게시자에 게 문의 하십시오. 해당 패키지에 대 한 소스 코드가 있는 MVC 5 및 Web API 2의 새로운 어셈블리와 함께 다시 컴파일합니다 해야 있습니다.   

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
    | Microsoft.AspNet.Mvc.FixedDisplayModes | < 된 >< / 된 > | 제거됨 |
    | Microsoft.AspNet.WebPages.Administration | < 된 >< / 된 > | 제거됨 |
    | Microsoft-Web-Helpers | < 된 >< / 된 > | Microsoft.AspNet.WebHelpers |

    > [!NOTE]
    > Microsoft-웹-도우미 Microsoft.AspNet.WebHelpers 바뀌었습니다. 이전 패키지를 먼저 제거 하 고 최신 패키지를 설치 해야 합니다.   
    >   
    > 주요 ASP.NET 패키지 간에 교차 버전 모드가 있습니다. 예를 들어 MVC 5와 호환 되만 3 Razor, Razor 2 없습니다.
4. Visual Studio 2013에서 프로젝트를 엽니다.
5. 설치 된 다음 ASP.NET NuGet 패키지를 제거 합니다. (PMC (패키지 관리자 콘솔)를 사용 하 여 제거 합니다. PMC를 열려면 선택 합니다 **도구** 메뉴를 선택 합니다 **라이브러리 패키지 관리자** 선택한 **패키지 관리자 콘솔**합니다. 프로젝트가이 모두를 포함할 수 있습니다.

    1. `Microsoft.AspNet.WebPages.Administration`  
   이 패키지는 MVC 3에서 MVC 4로 업그레이드 하는 경우에 일반적으로 추가 됩니다. 를 제거 하려면 PMC에서 다음 명령을 실행 합니다.  
        `Uninstall-Package -Id Microsoft.AspNet.WebPages.Administration`
    2. `Microsoft-Web-Helpers`   
   으로이 패키지의 브랜드가 `Microsoft.AspNet.WebHelpers`합니다. 를 제거 하려면 PMC에서 다음 명령을 실행 합니다.  
        `Uninstall-Package -Id Microsoft-Web-Helpers`
    3. `Microsoft.AspNet.Mvc.FixedDisplayMode`  
   이 패키지는 MVC 5에서 해결 되었으며 MVC 4의 버그 해결을 포함 합니다. 를 제거 하려면 PMC에서 다음 명령을 실행 합니다.  
        `Uninstall-Package -Id Microsoft.AspNet.Mvc.FixedDisplayModes`
6. PMC를 사용 하 여 모든 ASP.NET NuGet 패키지를 업그레이드 합니다. PMC에서 다음 명령을 실행 합니다.  
    `Update-Package`  
   `Update-Package` 명령을 매개 변수는 모든 패키지를 업데이트 합니다. ID 인수를 사용 하 여 패키지를 개별적으로 업데이트할 수 있습니다. 업데이트 명령에 대 한 자세한 내용은 실행 `get-help update-package` 합니다.

## <a name="update-the-application-webconfig-file"></a>응용 프로그램을 업데이트 *web.config* 파일

앱에서 이러한 변경을 수행 해야 *web.config* 파일을 하지는 *web.config* 파일을 *뷰* 폴더.

찾을 `<runtime>/<assemblyBinding>` 섹션을 다음과 같이 변경 합니다.

1. 이름 특성이 "System.Web.Mvc" 요소를 "5.0.0.0"를 "4.0.0.0"에서 버전 번호를 변경 합니다. (해당 요소에서 두 가지 변경 합니다.)
2. 요소의 name 특성을 사용 하 여 &quot;System.Web.Helpers "하 고 &quot;System.Web.WebPages&quot; "3.0.0.0 "를"2.0.0.0"에서 버전 번호를 변경 합니다. 4 개의 변경 내용 발생의 각 요소에 두.

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample3.xml?highlight=6,10,14)]
3. 찾을 `<appSettings>` 섹션 하 고 아래와 같이 3.0.0.0 2.0.0.0.0에서 webpages:version 업데이트:

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample4.xml?highlight=2)]
4. 전체 이외의 모든 신뢰 수준을 제거 합니다. 예를 들어:

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample5.xml?highlight=2)]

## <a name="update-the-webconfig-files-under-the-views-folder"></a>업데이트를 *web.config* Views 폴더 아래에 있는 파일

응용 프로그램 영역을 사용 하는 경우에 각 업데이트 해야 수도 *web.config* 파일을 *뷰* 각 Area 폴더의 하위 폴더입니다.

1. 버전 "5.0.0.0" 버전 "4.0.0.0"에서 "System.Web.Mvc"를 포함 하는 모든 요소를 업데이트 합니다.  

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample6.xml?highlight=2)]

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample7.xml?highlight=4-6,8)]
2. 버전 "3.0.0.0" 버전 "2.0.0.0"에서 "system.web.webpages.razor"를 포함을 포함 하는 모든 요소를 업데이트 합니다. 이 섹션에서는 "System.Web.WebPages"를 포함 하는 경우 업데이트 버전 "3.0.0.0" 버전 "2.0.0.0"에서 이러한 요소  

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample8.xml?highlight=3-5)]
3. 제거한 경우 합니다 `Microsoft-Web-Helpers` 이전 단계에서 NuGet 패키지 설치 `Microsoft.AspNet.WebHelpers` PMC에서 다음 명령을 사용 하 여:  
    `Install-Package -Id Microsoft.AspNet.WebHelpers`
4. 앱에서 사용 하는 경우는 [User.IsInRole()](https://msdn.microsoft.com/en-us/library/system.web.security.roleprincipal.isinrole(v=vs.110).aspx) 메서드를 다음을 추가 합니다 *Web.config* 파일.

    [!code-xml[Main](how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2/samples/sample9.xml)]

## <a name="final-steps"></a>최종 단계

빌드 및 응용 프로그램을 테스트 합니다.

프로젝트 파일에서 MVC 4 프로젝트 형식 GUID를 제거 합니다.

1. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 선택한 **프로젝트 언로드**합니다.
2. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 편집 ProjectName.csproj를 선택 합니다.
3. 찾을 합니다 `ProjectTypeGuids` 요소를 선택한 다음 제거 MVC 4 프로젝트 GUID `{E3E379DF-F4C6-4180-9B81-6769533ABE47}`합니다.
4. 저장 하 고 열려 있는 프로젝트 파일을 닫습니다.
5. 프로젝트를 마우스 오른쪽 단추로 누르고 **프로젝트 다시 로드**합니다.
