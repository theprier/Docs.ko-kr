---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: "ASP.NET MVC 4 모바일 기능 | Microsoft Docs"
author: Rick-Anderson
description: "이 자습서에서는 ASP.NET MVC 5 모바일 웹 응용 프로그램에서 Azure 웹 사이트 배포에서 샘플 코드는 MVC 5 버전이 되었습니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/15/2012
ms.topic: article
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: f4e0e4eb558e0c7b9e94fc83ede986fa4c666739
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
<a name="aspnet-mvc-4-mobile-features"></a>ASP.NET MVC 4 모바일 기능
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 이제이 자습서에서 샘플 코드의 MVC 5 버전 [ASP.NET MVC 5 모바일 웹 응용 프로그램 배포 Azure 웹 사이트에](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)합니다.


이 자습서에서는 모바일 ASP.NET MVC 4 웹 응용 프로그램 기능을 사용 하는 방법의 기본 사항 설명 합니다. 이 자습서에서는 사용할 수 있습니다 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) 또는 Visual Web Developer 2010 Express 서비스 팩 1 (&quot;Visual Web Developer 또는 VWD&quot;). 이미 있는 경우 Visual studio professional 버전을 사용할 수 있습니다.

시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다.

- [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (권장) 또는 Visual Studio Web Developer Express SP1. Visual Studio 2012에 ASP.NET MVC 4 포함 되어 있습니다. Visual Web Developer 2010를 사용 하는 경우 설치 해야 [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)합니다.

모바일 브라우저 에뮬레이터에서 앱을 해야 합니다. 다음 중 하나를 작동 합니다.

- [Windows 7 Phone 에뮬레이터](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)합니다. (이 자습서에서는 대부분의 스크린 샷에 사용 되는 에뮬레이터입니다.)
- IPhone을 에뮬레이션 하기 위해 사용자 에이전트 문자열을 변경 합니다. 참조 [이](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) 블로그 항목입니다.
- [Opera Mobile Emulator](http://www.opera.com/developer/tools/mobile/)
- [Apple Safari](http://www.apple.com/safari/download/) iPhone로 설정 하 고 사용자 에이전트와 합니다. Safari에서 "iPhone"로 사용자 에이전트를 설정 하는 방법에 지침은 [Safari 있다고 생각 IE 되 게 하는 방법](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) David Alison 블로그.

C# 소스 코드를 visual Studio 프로젝트는이 항목을 함께 사용할 수 있습니다.

- [시작 프로젝트 다운로드](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [프로젝트 다운로드를 완료합니다.](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a>만들 것인지

이 자습서에서는 모바일 기능에 추가할 간단한 회의 목록 응용 프로그램에 제공 되는 [시작 프로젝트](https://go.microsoft.com/fwlink/?LinkId=228307)합니다. 다음 스크린 샷에서 같이 완성된 된 응용 프로그램 태그 페이지가 나와 [Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)합니다. 참조 [키보드 매핑에 대 한 Windows Phone 에뮬레이터](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) 키보드 입력을 간소화 하기 위해 합니다.

[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)

Internet Explorer 버전 9, 10, FireFox 또는 Chrome을 설정 하 여 모바일 응용 프로그램을 개발 하는 데는 [사용자 에이전트 문자열](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)합니다. 다음 그림에서는 iPhone을 에뮬레이션 하는 Internet Explorer를 사용 하 여 완성 된 자습서를 보여 줍니다. Internet Explorer F-12 개발자 도구를 사용할 수 있습니다 및 [Fiddler 도구](http://www.fiddler2.com/fiddler2/) 응용 프로그램을 디버깅할 수 있도록 합니다.

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a>기술을 알아봅니다

학습할 다음과 같습니다.

- ASP.NET MVC 4 템플릿에 HTML5를 사용 하는 방법 `viewport` 모바일 장치에 특성 및 개선 하기 위해 자동 선택 렌더링을 표시 합니다.
- 모바일 전용 뷰를 만드는 방법.
- 만들기 뷰 전환기 모바일 보기와 응용 프로그램의 바탕 화면 보기 간에 사용 하면 사용자가 토글 해당 하는 방법.

### <a name="getting-started"></a>시작

다음 링크를 사용 하 여 시작 프로젝트에 대 한 목록 회의 응용 프로그램을 다운로드: [다운로드](https://go.microsoft.com/fwlink/?LinkId=228307)합니다. 다음 Windows 탐색기에서 마우스 오른쪽 단추로 클릭는 *MvcMobile.zip* 파일을 선택 **속성**합니다. 에 **MvcMobile.zip 속성** 대화 상자에서 선택 하는 **차단 해제** 단추입니다. (사용 하려고 할 때 발생 하는 보안 경고가 표시 되지 않도록 차단 해제는 *.zip* 웹에서 다운로드 한 파일입니다.)

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

마우스 오른쪽 단추로 클릭는 *MvcMobile.zip* 파일을 선택 **압축 풀기** 에 파일 압축을 풉니다. Visual Studio에서 열고는 *MvcMobile.sln* 파일입니다.

데스크톱 브라우저에 표시 하는 응용 프로그램을 실행 하려면 CTRL + f 5를 누릅니다. 모바일 브라우저 에뮬레이터 시작 회의 응용 프로그램에 대 한 URL의 에뮬레이터에 복사한 다음 클릭는 **태그에 의해 찾아보기** 링크 합니다. Windows Phone 에뮬레이터를 사용 하는 경우 URL 표시줄에서 클릭를 키보드 액세스를 일시 중지 키를 누르십시오. 다음 이미지는 *AllTags* 보기 (선택 **태그에 의해 찾아보기**).

[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)

디스플레이가 모바일 장치에서 읽을 수 있는 매우입니다. ASP.NET 링크를 선택 합니다.

[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)

ASP.NET 태그 보기는 매우 복잡 합니다. 예를 들어는 **날짜** 열 읽기 하기 매우 어렵습니다. 이 자습서의 뒷부분에 나오는 버전을 만듭니다는 *AllTags* 모바일 브라우저에 맞게 이며 하 게 되는 디스플레이 읽을 수 있는 보기입니다.

참고: 현재는 버그가 있습니다 모바일 캐싱 엔진입니다. 프로덕션 응용 프로그램을 설치 해야는 [고정 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) 덩어리 패키지 합니다. 참조 [ASP.NET MVC 4 모바일 캐싱 버그 고정](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 수정 프로그램에 대 한 자세한 내용은 합니다.

## <a name="css-media-queries"></a>CSS 미디어 쿼리

[CSS 미디어 쿼리](http://www.w3.org/TR/css3-mediaqueries/) 미디어 형식에 대 한 CSS에 대 한 확장입니다. 특정 브라우저 (사용자 에이전트)에 대 한 기본 CSS 규칙을 재정의 하는 규칙을 만들 수 수 있습니다. 모바일 브라우저를 대상으로 하는 CSS에 대 한 일반적인 규칙은 최대 화면 크기를 정의 합니다. *Content\Site.css* 다음 미디어 쿼리를 포함 하는 새 ASP.NET MVC 4 인터넷 프로젝트를 만들 때 만들어지는 파일입니다.

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

브라우저 창을 850 픽셀 줄이거나 경우이 미디어 블록 CSS 규칙을 사용 합니다. 에 제공 하기 위해 HTML 콘텐츠의 표시를 더 나은 설계 된 기본 CSS 규칙 보다 작은 브라우저 (예: 모바일 브라우저) 데스크톱 브라우저의 넓은 디스플레이 대 한 다음과 같은 CSS 미디어 쿼리를 사용할 수 있습니다.

## <a name="the-viewport-meta-tag"></a>뷰포트 메타 태그

가상 브라우저 창의 너비를 정의 하는 대부분의 모바일 브라우저 (의 *뷰포트*) 하는 모바일 장치에서의 실제 너비 보다 훨씬 큰 합니다. 따라서 가상 디스플레이로 내 전체 웹 페이지에 맞게 모바일 브라우저 수 있습니다. 사용자가 다음 확대할 수 흥미로운 내용입니다. 그러나 실제 장치 너비로 뷰포트 너비를 설정 하는 경우 없습니다 확대/축소는 필요한 경우 모바일 브라우저에는 콘텐츠를 맞추는 때문에.

뷰포트 `<meta>` ASP.NET MVC 4 레이아웃 파일의 태그에에서 장치 너비에 뷰포트를 설정 합니다. 다음 줄 뷰포트를 보여 줍니다. `<meta>` ASP.NET MVC 4 레이아웃 파일의 태그에에서 있습니다.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a>CSS 미디어 쿼리 및 뷰포트 메타 태그의 효과 검토합니다.

열기는 *Views\Shared\\_Layout.cshtml* 뷰포트 주석 고 편집기에서 파일 `<meta>` 태그입니다. 다음 태그 주석 줄을 보여 줍니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

열기는 *MvcMobile\Content\Site.css* 편집기에서 파일을 미디어 쿼리의 최대 너비를 0 픽셀로 변경 합니다. 이렇게 하면 모바일 브라우저에서 사용 되는 CSS 규칙이 방지 됩니다. 다음 줄에서는 수정 된 미디어 쿼리를 보여 줍니다.

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

변경 내용을 저장 하 고 모바일 브라우저 에뮬레이터에서 회의 응용 프로그램을 찾습니다. 다음 그림에는 작은 텍스트 뷰포트를 제거할 경우의 결과 `<meta>` 태그입니다. 없는 뷰포트와 `<meta>` 태그 브라우저 축소 되어 표시 기본 뷰포트 너비에 (850 픽셀 대부분의 모바일 브라우저에 대 한 광범위 한 또는.)

[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)

변경 내용을 실행 취소-뷰포트를 주석 처리 제거 `<meta>` 레이아웃 파일에 태그 및 850 픽셀에 미디어 쿼리 복원는 *Site.css* 파일입니다. 변경 내용을 저장 모바일에서 잘 작동 디스플레이 복원 되었는지 확인 하려면 모바일 브라우저를 새로 고 치세요.

뷰포트 `<meta>` 태그와 CSS 미디어 쿼리 ASP.NET MVC 4 관련 되어 있으며 웹 응용 프로그램에서 이러한 기능을 활용을 취할 수 있습니다. 하지만 이제 새 ASP.NET MVC 4 프로젝트를 만들 때 생성 되는 파일에 만들어집니다.

뷰포트에 대 한 자세한 내용은 `<meta>` 태그, 참조 [두 개의 뷰포트 이야기-2 부](http://www.quirksmode.org/mobile/viewports2.html)합니다.

다음 섹션에서 모바일 브라우저 특정 보기를 제공 하는 방법을 배웁니다.

## <a name="overriding-views-layouts-and-partial-views"></a>뷰, 레이아웃 및 부분 뷰를 재정의합니다.

ASP.NET MVC 4의 중요 한 새로운 기능은 개별 모바일 브라우저에 대 한 일반적으로 또는 모든 특정 브라우저에 대 한 모바일 브라우저에 대 한 모든 보기 (레이아웃 및 부분 뷰 포함)를 재정의할 수 있습니다 하는 간단한 메커니즘입니다. 모바일 전용 보기를 제공 하려면 보기 파일 복사 추가 하는 *합니다. 모바일* 을 파일 이름입니다. 예를 들어, 모바일 만들려는 *인덱스* 보기, 복사 *Views\Home\Index.cshtml* 를 *Views\Home\Index.Mobile.cshtml*합니다.

이 섹션에서는 모바일 전용 레이아웃 파일을 만들어야 합니다.

복사를 시작 하려면 *Views\Shared\\_Layout.cshtml* 를 *Views\Shared\\_Layout.Mobile.cshtml*합니다. 열기  *\_Layout.Mobile.cshtml* 에서 제목을 변경 하 고 **MVC4 회의** 를 **회의 (모바일)**합니다.

각 `Html.ActionLink` 호출, "찾아보기 기준" 각 링크에 제거 *ActionLink*합니다. 다음 코드는 모바일 레이아웃 파일의 완료 된 본문 섹션을 보여 줍니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

복사는 *Views\Home\AllTags.cshtml* 파일을 *Views\Home\AllTags.Mobile.cshtml*합니다. 새 파일을 열고 변경는 `<h2>` "Tags"에서 요소를 "태그 (M)":

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

데스크톱 브라우저 및 모바일 브라우저 에뮬레이터를 사용 하 여 태그 페이지로 이동 합니다. 모바일 브라우저 에뮬레이터에는 두 개의 변경 내용을 보여 줍니다.

[![p2m_layoutTags.mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)

반면, 바탕 화면 변경 되지 않았습니다.

[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)

## <a name="browser-specific-views"></a>브라우저의 뷰

모바일 및 데스크톱 관련 뷰 외에도 개별 브라우저에 대 한 보기를 만들 수 있습니다. 예를 들어, iPhone 브라우저에만 사용 되는 뷰를 만들 수 있습니다. 이 섹션에서는 iPhone 버전과 iPhone 브라우저에 대 한 레이아웃 만듭니다는 *AllTags* 보기.

열기는 *Global.asax* 파일을 다음 코드를 추가 하는 `Application_Start` 메서드.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

이 코드는 들어오는 각 요청에 대해 일치 시킬 "iPhone" 라는 새 디스플레이 모드를 정의 합니다. (즉, 포함 되 면 사용자 에이전트는 "iPhone")를 정의 된 조건과 일치 하는 들어오는 요청을 하면 ASP.NET MVC는 이름이 "iPhone" 접미사를 포함 하는 뷰를 찾습니다.

코드에서 마우스 오른쪽 단추로 클릭 `DefaultDisplayMode`, 선택 **해결**를 선택한 후 `using System.Web.WebPages;`합니다. 에 대 한 참조를 추가 하는이 `System.Web.WebPages` 에 네임 스페이스는 `DisplayModes` 및 `DefaultDisplayMode` 형식은 정의 됩니다.

[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)

또는 다음 줄을 방금 수동으로 추가할 수는 `using` 파일의 섹션입니다.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

전체 내용을 *Global.asax* 파일은 다음과 같습니다.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

변경 내용을 저장 합니다. 복사는 *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* 파일을 *MvcMobile\Views\Shared\\_Layout.iPhone.cshtml*합니다. 새 파일을 열고 변경 하는 `h1` 에서 머리글 `Conference (Mobile)` 를 `Conference (iPhone)`합니다.

복사는 *MvcMobile\Views\Home\AllTags.Mobile.cshtml* 파일을 *MvcMobile\Views\Home\AllTags.iPhone.cshtml*합니다. 새 파일에서 변경 된 `<h2>` 요소에서 "태그 (M)"을 "태그 (iPhone)"입니다.

응용 프로그램을 실행합니다. 모바일 브라우저 에뮬레이터에서 앱 실행에서 사용자 에이전트를 "iPhone"로 설정 되어 있는지 확인 한를 찾습니다는 *AllTags* 보기. 다음 스크린 샷에 표시는 *AllTags* 보기에서 렌더링 된 [Safari](http://www.apple.com/safari/download/) 브라우저. Windows 용 Safari를 다운로드할 수 있습니다 [여기](https://support.apple.com/kb/DL1531)합니다.

[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)

이 섹션에서는 모바일 레이아웃, 보기를 만드는 방법과 레이아웃, iPhone 등 특정 장치에 대 한 보기를 만드는 방법을 살펴보았습니다. 다음 섹션에서 더 많은 매력적인 모바일 보기에 대 한 jQuery Mobile을 활용 하는 방법을 배웁니다.

## <a name="using-jquery-mobile"></a>JQuery Mobile을 사용 하 여

[jQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) 라이브러리에서 작동 하는 모든 주요 모바일 브라우저는 사용자 인터페이스 프레임 워크를 제공 합니다. jQuery Mobile 적용 *점진적인 기능 향상* CSS 및 JavaScript를 지 원하는 모바일 브라우저에 있습니다. 점진적인 기능 향상에 보다 강력한 브라우저와 장치를 보다 다양 한 표시를 허용 하는 동안 웹 페이지의 기본 콘텐츠를 표시 하는 모든 브라우저 수 있습니다. JQuery Mobile에 포함 된 JavaScript 및 CSS 파일에 태그를 변경 하지 않고 모바일 브라우저에 맞게 많은 요소 스타일 지정 합니다.

이 섹션의 설치는 *jQuery.Mobile.MVC* 뷰 전환기 위젯 및 jQuery Mobile을 설치 하는 NuGet 패키지 합니다.

삭제를 시작 하려면는 *Shared\\_Layout.Mobile.cshtml* 및 *Shared\\_Layout.iPhone.cshtml* 앞에서 만든 파일입니다.

이름 바꾸기 *Views\Home\AllTags.Mobile.cshtml* 및 *Views\Home\AllTags.iPhone.cshtml* 파일을 *Views\Home\AllTags.iPhone.cshtml.hide* 및  *Views\Home\AllTags.Mobile.cshtml.hide*합니다. 파일이 더 이상 없으므로 *.cshtml* 확장, 렌더링 하는 ASP.NET MVC 런타임에서 사용 되지 않습니다는 *AllTags* 보기.

설치는 *jQuery.Mobile.MVC* 이 수행 하 여 NuGet 패키지:

1. **도구** 메뉴 선택 **라이브러리 패키지 관리자**를 선택한 후 **패키지 관리자 콘솔**합니다.

    [![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)
2. 에 **패키지 관리자 콘솔**, 입력`Install-Package jQuery.Mobile.MVC -version 1.0.0`

다음 이미지는 추가 및 MvcMobile 프로젝트에 NuGet jQuery.Mobile.MVC 패키지에서 변경 된 파일을 표시 합니다. 파일 이름 뒤에 추가 [추가]가 추가 되는 파일입니다. GIF 이미지는 표시 되지 않습니다 및 PNG 파일에 추가 된 *Content\images* 폴더입니다.

![](aspnet-mvc-4-mobile-features/_static/image21.png)

다음 jQuery.Mobile.MVC NuGet 패키지를 설치합니다.

- *앱\_Start\BundleMobileConfig.cs* 추가 jQuery JavaScript 및 CSS 파일을 참조 하는 데 필요한 파일입니다. 아래 지침에 따라 해야 하며이 파일에 정의 된 모바일 번들 참조 해야 합니다.
- jQuery Mobile CSS 파일입니다.
- A `ViewSwitcher` 컨트롤러 위젯 (*Controllers\ViewSwitcherController.cs*).
- jQuery Mobile JavaScript 파일입니다.
- JQuery Mobile 스타일의 레이아웃 파일 (*Views\Shared\\_Layout.Mobile.cshtml*).
- 뷰 전환기 부분 뷰 *(MvcMobile\Views\Shared\\_ViewSwitcher.cshtml*) 하는 모바일 보기로 그리고 반대로 바탕 화면 보기에서 전환 하려면 각 페이지의 위쪽에 대 한 링크를 제공 합니다.
- 여러*.png* 및 *.gif* 이미지 파일의 *Content\images* 폴더입니다.

열기는 *Global.asax* 파일의 마지막 줄으로 다음 코드를 추가 하 고는 `Application_Start` 메서드.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

다음 코드에서는 전체 *Global.asax* 파일입니다.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> Internet Explorer 9를 사용 하 고 표시 되지 않는 경우는 `BundleMobileConfig` 노란색 강조 표시에 위의 줄, 클릭는 [호환성 보기 단추](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![(off) 호환성 보기 단추 그림] (http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg " (Off) 호환성 보기 단추 그림") 개요에서 변경 아이콘을 확인 하는 IE의 ![(off) 호환성 보기 단추 그림](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "(해제) 호환성 보기 단추 그림 ") 단색 ![(on) 호환성 보기 단추 그림](http://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "(on) 호환성 보기 단추 그림")합니다. 또는 FireFox 또는 Chrome에서이 자습서를 확인할 수 있습니다.


열기는 *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* 파일을 다음 태그 바로 뒤에 추가 된 `Html.Partial` 호출:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

전체 *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* 파일은 다음과 같습니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

응용 프로그램을 빌드 및 모바일 브라우저 에뮬레이터에서 찾은 *AllTags* 보기. 다음 화면이 나타납니다.

[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)

> [!NOTE]
> 모바일 특정 코드를 디버깅할 수 [사용자 에이전트 문자열을 설정](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) IE 또는 iPhone 및 다음 F-12 개발자 도구를 사용 하 여 Chrome에 대 한 합니다. 모바일 브라우저에 표시 되지 않는 경우는 **홈**, **스피커**, **태그**, 및 **날짜** 단추로 링크, jQuery Mobile에 대 한 참조 스크립트 및 CSS 파일 아마도 올바르지 않습니다.


참조 스타일 변경 내용 외에 **모바일 보기 표시** 및 바탕 화면 보기 모바일 보기에서 전환할 수 있는 링크입니다. 선택 된 **바탕 화면 보기** 링크 및 바탕 화면 보기에 표시 됩니다.

[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)

바탕 화면 보기에는 직접 모바일 보기로 다시 이동 하는 방법을 제공 하지 않습니다. 지금 수정 합니다. 열기는 *Views\Shared\\_Layout.cshtml* 파일입니다. 페이지 아래에서 방금 `body` 요소를 뷰 전환기 위젯 렌더링 하는 다음 코드를 추가 합니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

새로 고침의 *AllTags* 모바일 브라우저에서 보기. 데스크톱 및 모바일 뷰 간에 탐색할 수 있습니다.

[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)

> [!NOTE]
> 디버깅 참고:는 Views\Shared의 끝에 다음 코드를 추가할 수 있습니다\\_ViewSwitcher.cshtml 브라우저 사용자 에이전트 문자열을 사용 하 여 모바일 장치를 설정 하는 경우 뷰를 디버깅할 수 있도록 합니다.
> 
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
> 
>  다음과 같은 머리글을 추가 하 고는 *Views\Shared\\_Layout.cshtml* 파일입니다.  
> 
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]


찾아는 *AllTags* 데스크톱 브라우저에서 페이지입니다. 뷰 전환기 위젯 모바일 레이아웃 페이지에만 추가 되므로 데스크톱 브라우저에 표시 되지 않습니다. 자습서의 뒷부분에 나오는 추가 하는 방법을 뷰 전환기 위젯 바탕 화면 보기에 표시 됩니다.

[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)

## <a name="improving-the-speakers-list"></a>스피커 목록 개선

모바일 브라우저에서 선택 된 **스피커** 링크 합니다. 모바일 뷰가 있기 때문에 (*AllSpeakers.Mobile.cshtml*), 기본 스피커 표시 (*AllSpeakers.cshtml*) 모바일 레이아웃 보기를 사용 하 여 렌더링 됩니다 ( *\_ Layout.Mobile.cshtml*).

[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)

전역으로 설정 하 여 렌더링 모바일 레이아웃 내에서 기본 (비모바일) 뷰를 비활성화할 수 있습니다 `RequireConsistentDisplayMode` 를 `true` 에 *뷰\\_viewstart.vbhtml* 다음과 같이 파일:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

때 `RequireConsistentDisplayMode` 로 설정 된 `true`, 모바일 레이아웃 (*\_Layout.Mobile.cshtml*) 모바일 보기에만 사용 됩니다. (즉, 파일 보기 된 형식인 ***ViewName**합니다. Mobile.cshtml*입니다.) 설정 하려는 경우 `RequireConsistentDisplayMode` 를 `true` 모바일 레이아웃 비모바일 보기와 잘 작동 하지 않는 경우. 다음 스크린샷에서 방법을 *스피커* 페이지를 렌더링 하는 경우 `RequireConsistentDisplayMode` 로 설정 된 `true`합니다.

[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)

설정 하 여 보기에 일관 된 표시 모드를 해제할 수 `RequireConsistentDisplayMode` 를 `false` 보기 파일에 있습니다. 에 다음 태그는 *Views\Home\AllSpeakers.cshtml* 파일 집합 `RequireConsistentDisplayMode` 를 `false`:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a>모바일 스피커 보기를 만드는 방법

본 것 처럼는 *스피커* 보기 사용자가 읽을 수 있지만 링크는 작은 이며 모바일 장치를 탭 하기 어렵습니다. 이 섹션에서는 모바일 전용 만듭니다 *스피커* 최신 모바일 응용 프로그램 같은 보기-큰 표시, tap 쉽게 연결 하 고 스피커를 빠르게 찾기 위해 검색 상자를 포함 합니다.

복사 *AllSpeakers.cshtml* 를 *AllSpeakers.Mobile.cshtml*합니다. 열기는 *AllSpeakers.Mobile.cshtml* 파일을 제거는 `<h2>` 제목 요소입니다.

에 `<ul>` 태그, 추가 된 `data-role` 특성 및 값을 설정 `listview`합니다. 와 같은 다른 [ `data-*` 특성](http://html5doctor.com/html5-custom-data-attributes/), `data-role="listview"` 을 탭 하 큰 목록 항목을 더 쉽게 만듭니다. 다음은 완성 된 태그의 모양을입니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

모바일 브라우저를 새로 고칩니다. 업데이트 된 보기는 다음과 같습니다.

[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)

모바일 보기 기능이 향상 되기는 하지만 스피커의 긴 목록을 탐색 하 어렵습니다. 이 해결 하려면는 `<ul>` 태그, 추가 `data-filter` 로 설정 하 고 특성 `true`합니다. 다음 코드는 `ul` 태그입니다.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

다음 이미지는 검색 필터 상자의 결과로 생성 되는 페이지의 위쪽에 표시 된 `data-filter` 특성입니다.

[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)

검색 상자에 각 문자를 입력할 때 jQuery Mobile 아래 이미지에 나와 있는 것 처럼 표시 된 목록을 필터링 합니다.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)

## <a name="improving-the-tags-list"></a>태그 목록 개선

기본값이 마음에 *스피커* 보기는 *태그* 보기 사용자가 읽을 수 있지만 링크는 작은 모바일 장치를 탭 하기가 어렵습니다. 이 섹션에서는 수정 합니다는 *태그* 고정 여부에 관계 없이 동일한 방식으로 볼는 *스피커* 보기.

제거는 &quot;숨기기&quot; 에 접미사는 *Views\Home\AllTags.Mobile.cshtml.hide* 하므로 이름이 파일 *Views\Home\AllTags.Mobile.cshtml*합니다. 이름이 바뀐된 파일을 열고 제거는 `<h2>` 요소입니다.

추가 `data-role` 및 `data-filter` 특성에 `<ul>` 태그를 다음과 같이 합니다.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

아래 이미지에서 문자 필터링 태그 페이지를 보여 줍니다. `J`합니다.

[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)

## <a name="improving-the-dates-list"></a>날짜 목록 개선

향상 시킬 수 있습니다는 *날짜* 향상 된 처럼 볼는 *스피커* 및 *태그* 뷰를 보다 쉽게 모바일 장치에서 사용할 수 있도록 합니다.

복사는 *Views\Home\AllDates.cshtml* 파일을 *Views\Home\AllDates.Mobile.cshtml*합니다. 새 파일을 열고 제거는 `<h2>` 요소입니다.

추가 `data-role="listview"` 에 `<ul>` 다음과 같은 태그:

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

아래 이미지에서는 **날짜** 와 같이 페이지는 `data-role` 위치에 대 한 특성입니다.

[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) 의 내용을 대체는 *Views\Home\AllDates.Mobile.cshtml* 를 다음 코드로 파일:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

이 코드는 일별로 모든 세션을 그룹화합니다. 새로운 각 날에 대 한 목록 구분선을 만들므로 목록과 구분선 아래에서 각 날짜에 대 한 모든 세션. 이 코드를 실행할 때 모양 다음과 같습니다.

[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)

## <a name="improving-the-sessionstable-view"></a>SessionsTable 보기 향상

이 섹션에서는 세션 모바일 전용 보기를 만듭니다. 변경 하도록 준비 되어 다른 보기에서 보다 더욱 광범위 한 됩니다.

모바일 브라우저 탭에서 **스피커** 입력 한 다음 단추를 `Sc` 검색 상자에 있습니다.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)

탭의 **Scott Hanselman** 링크 합니다.

[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)

볼 수 있듯이 디스플레이가 모바일 브라우저를 읽기가 어렵습니다. 날짜 열이 읽기 어려운 및은 보기에서 태그 열이 있습니다. 이 문제를 해결 하려면 복사 *Views\Home\SessionsTable.cshtml* 를 *Views\Home\SessionsTable.Mobile.cshtml*, 파일의 내용을 다음 코드로 바꿉니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

코드 태그 열, 및이 모든 정보는 모바일 브라우저에서 읽을 수 있도록 제목과 스피커, 날짜를 세로로 서식을 대화방을 제거 합니다. 아래 이미지에는 코드 변경 내용을 반영합니다.

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)

## <a name="improving-the-sessionbycode-view"></a>SessionByCode 보기 향상

모바일 전용 보기를 만듭니다 마지막으로 *SessionByCode* 보기. 모바일 브라우저 탭에서 **스피커** 입력 한 다음 단추를 `Sc` 검색 상자에 있습니다.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)

탭의 **Scott Hanselman** 링크 합니다. Scott Hanselman 세션이 표시 됩니다.

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)

선택 된 **An MS 웹 Love 스택 개요** 링크 합니다.

[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)

기본 바탕 화면 보기 하지만,이 향상 시킬 수 있습니다.

복사는 *Views\Home\SessionByCode.cshtml* 를 *Views\Home\SessionByCode.Mobile.cshtml* 의 내용을 대체 하 고는 *Views\Home\SessionByCode.Mobile.cshtml*다음 태그로 파일:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

새 태그를 사용 하 여는 `data-role` 특성 보기의 레이아웃을 개선 합니다.

모바일 브라우저를 새로 고칩니다. 다음 그림에는 방금 만든 코드 변경 내용을 반영 합니다.

[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)

## <a name="wrapup-and-review"></a>Wrapup 및 검토

이 자습서에 ASP.NET MVC 4 Developer Preview의 새로운 모바일 기능을 도입 되었습니다. 모바일 기능은 다음과 같습니다.

- 전역 및 개별 보기에 대 한 레이아웃, 뷰 및 부분 뷰를 재정의 하는 기능입니다.
- 레이아웃 및 사용 하 여 부분 재정의 적용에 대 한 제어는 `RequireConsistentDisplayMode` 속성입니다.
- 모바일 앱을 위해 뷰 전환기 위젯 데스크톱 보기에 표시할 수 있는 뷰.
- IPhone 브라우저와 같은 특정 브라우저 지원에 대 한 지원.

## <a name="see-also"></a>참고 항목

- [jQuery Mobile](http://jquerymobile.com) 사이트입니다.
- [jQuery Mobile 개요](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [W3C 권장 사항 모바일 웹 응용 프로그램 모범 사례](http://www.w3.org/TR/mwabp/)
- [미디어 쿼리에 대 한 W3C Candidate Recommendation](http://www.w3.org/TR/css3-mediaqueries/)
