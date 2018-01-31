---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: "ASP.NET Web API에 대 한 도움말 페이지 만들기 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/01/2013
ms.topic: article
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 37fd26ebaea192cb540c443eff8a07343ab8c15b
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="creating-help-pages-for-aspnet-web-api"></a>ASP.NET Web API에 대 한 도움말 페이지 만들기
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

Web API를 만들 때 유용 도움말 페이지를 만들 되 고 다른 개발자가 API를 호출 하는 방법을 알게 됩니다. 모든 문서를 수동으로 만들 수 있지만 가능한 한 자동 생성 하는 것이 좋습니다.

이 작업을 간단 하 게 하려면 ASP.NET Web API 도움말 페이지 자동 생성에 대 한 라이브러리를 런타임에 제공 합니다.

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a>API 도움말 페이지 만들기

설치 [ASP.NET 및 웹 도구 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=282650)합니다. 도움말 페이지의 웹 API 프로젝트 템플릿을에 통합 하는이 업데이트 됩니다.

다음으로 새 ASP.NET MVC 4 프로젝트를 만들고 웹 API 프로젝트 템플릿을 선택 합니다. 프로젝트 템플릿은 만듭니다 라는 예제 API 컨트롤러는 `ValuesController`합니다. 또한이 템플릿은 API 도움말 페이지를 만듭니다. 도움말 페이지에 대 한 코드 파일의 모든 프로젝트의 영역 폴더에 배치 됩니다.

![](creating-api-help-pages/_static/image2.png)

응용 프로그램을 실행 하는 경우 홈 페이지의 API 도움말 페이지에 대 한 링크를 포함 합니다. 상대 경로 홈 페이지에서 /Help은 합니다.

![](creating-api-help-pages/_static/image3.png)

이 링크 API 요약 페이지에 제공 해야 합니다.

![](creating-api-help-pages/_static/image4.png)

이 페이지에 대 한 MVC 뷰 Areas/HelpPage/Views/Help/Index.cshtml에 정의 됩니다. 레이아웃, 소개, 제목, 스타일 및 등을 수정 하려면이 페이지를 편집할 수 있습니다.

페이지의 주요 부분에는 컨트롤러에 의해 그룹화, Api의 테이블입니다. 사용 하 여 테이블 항목으로 동적으로 생성 된 **IApiExplorer** 인터페이스입니다. (하겠습니다이 인터페이스에 대 한 자세한 나중.) 새 API 컨트롤러를 추가 하는 경우 테이블은 런타임에 자동으로 업데이트 됩니다.

"API" 열에는 HTTP 메서드 및 상대 URI 나열 됩니다. "Description" 열 각 API에 대 한 설명서를 포함합니다. 처음에 설명서에 자리 표시자 텍스트 뿐입니다. 다음 섹션에서 XML 주석에서 설명서를 추가 하는 방법을 살펴보겠습니다.

각 API에 있는 예제 요청 및 응답 본문을 포함 하 여 보다 자세한 정보를 페이지에 대 한 링크입니다.

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a>도움말 페이지를 기존 프로젝트 추가

기존 웹 API 프로젝트에 NuGet 패키지 관리자를 사용 하 여 도움말 페이지를 추가할 수 있습니다. 이 옵션은 "Web API" 템플릿보다 다른 프로젝트 템플릿에서 시작 하면 유용 합니다.

**도구** 메뉴 선택 **라이브러리 패키지 관리자**를 선택한 후 **패키지 관리자 콘솔**합니다. 에 [패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 창에서 다음 명령 중 하나를 입력 합니다.

에 대 한는 **C#** 응용 프로그램:`Install-Package Microsoft.AspNet.WebApi.HelpPage`

에 대 한는 **Visual Basic** 응용 프로그램:`Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`

두 개의 패키지, C# 및 Visual basic의 있습니다. 프로젝트와 일치 하는 것을 사용 하 고 있는지 확인 합니다.

이 명령은 필요한 어셈블리와 도움말 페이지 (영역/HelpPage 폴더에 있음)에 대 한 MVC 뷰를 추가 합니다. 도움말 페이지에 대 한 링크를 수동으로 추가 해야 합니다. URI는 /Help 합니다. Razor 보기에서 링크를 만들려면 다음을 추가 합니다.

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

또한 영역을 등록 해야 합니다. Global.asax 파일에 다음 코드를 추가 **응용 프로그램\_시작** 메서드를 사용할 수 있는 아직 없는 경우:

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a>API 설명서 추가

기본적으로 도움말 페이지는 설명서에 대 한 자리 표시자 문자열을 제공 합니다. 사용할 수 있습니다 [XML 문서 주석](https://msdn.microsoft.com/library/b2s063f7.aspx) 는 문서를 만들 수 있습니다. 이 기능을 사용 하려면 영역/HelpPage/응용 프로그램 파일을 열고\_Start/HelpPageConfig.cs 다음 줄에서 주석 처리 제거:

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

이제 XML 문서를 사용 합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다. 선택 된 **빌드** 페이지.

![](creating-api-help-pages/_static/image6.png)

아래 **출력**, 확인 **XML 문서 파일**합니다. 편집 상자에 입력 "앱\_Data/XmlDocument.xml"입니다.

![](creating-api-help-pages/_static/image7.png)

에 대 한 코드를 열고 다음으로 `ValuesController` /Controllers/ValuesControler.cs에 정의 된 API 컨트롤러입니다. 일부 문서 주석을 컨트롤러 메서드를 추가 합니다. 예:

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> 팁: 메서드 위의 줄에 캐럿을 배치 하 고 3 개의 슬래시를 입력 하는 경우 Visual Studio 자동으로 삽입 하는 XML 요소입니다. 다음에 있는 공백을 채울 수 있습니다.


이제 및 응용 프로그램을 다시 실행 빌드하고 도움말 페이지로 이동 합니다. 설명서 문자열 API 테이블에 표시 됩니다.

![](creating-api-help-pages/_static/image8.png)

도움말 페이지 런타임 시 XML 파일에서 문자열을 읽습니다. (응용 프로그램을 배포 하는 경우 확인 XML 파일을 배포 해야 합니다.)

## <a name="under-the-hood"></a>기본적인 이해

도움말 페이지의 맨 위에 빌드됩니다는 **ApiExplorer** 클래스는 Web API 프레임 워크의 일부입니다. **ApiExplorer** 클래스 도움말 페이지를 만들기 위한 raw 자료를 제공 합니다. 각 API에 대 한 **ApiExplorer** 포함 한 **ApiDescription** API를 설명 하는 합니다. 이 위해 "API"는 HTTP 메서드 및 상대 URI의 조합으로 정의 됩니다. 예를 들어 다음은 몇 가지 고유한 Api입니다.

- /Api/Products 가져오기
- 가져오기 /api/제품 / {id}
- / Api/제품 게시

컨트롤러 작업에서 여러 HTTP 메서드를 지 원하는 경우는 **ApiExplorer** 각 메서드는 별도 API로 처리 합니다.

API를 숨기려면는 **ApiExplorer**, 추가 된 **ApiExplorerSettings** 특성을 설정 하 고는 동작 *IgnoreApi* true로 합니다.

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

또한 전체 컨트롤러를 제외 하려면 컨트롤러에이 특성을 추가할 수 있습니다.

ApiExplorer 클래스 문자열의 설명서를 가져옵니다는 **IDocumentationProvider** 인터페이스입니다. 도움말 페이지 라이브러리에서 제공 하는 앞에서 살펴본 것 처럼는 **IDocumentationProvider** 하는 XML 문서 문자열에서 설명서를 가져옵니다. 코드는 /Areas/HelpPage/XmlDocumentationProvider.cs에 있습니다. 가져올 수 있습니다 설명서 다른 원본에서 작성 하 여 사용자 고유의 **IDocumentationProvider**합니다. 연결 하는 것을, 호출 된 **SetDocumentationProvider** 에 정의 된 확장 메서드 **HelpPageConfigurationExtensions**

**ApiExplorer** 를 자동으로 호출 된 **IDocumentationProvider** 각 API에 대 한 설명서 문자열을 얻을 수 있는 인터페이스입니다. 에 저장 된 **설명서** 속성의는 **ApiDescription** 및 **ApiParameterDescription** 개체입니다.

## <a name="next-steps"></a>다음 단계

여기에 표시 된 도움말 페이지에 제한 되지 않습니다. 사실, **ApiExplorer** 도움말 페이지를 만드는로 제한 되지 않습니다. 상자를 고려 하는 데 몇 가지 훌륭한 블로그 게시물 Yao Huang 연결 기록 했습니다.

- [ASP.NET 웹 API 도움말 페이지에는 간단한 테스트 클라이언트를 추가합니다.](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [자체 호스팅된 서비스에서 작동 하는 ASP.NET 웹 API 도움말 페이지 만들기](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [ASP.NET Web API에 대 한 도움말 페이지 (또는 클라이언트)의 디자인 타임 생성](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [고급 도움말 페이지 사용자 지정](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
