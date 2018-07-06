---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: ASP.NET MVC 4 모바일 기능 | Microsoft Docs
author: Rick-Anderson
description: 이제 ASP.NET MVC 5 모바일 웹 응용 프로그램에서 Azure 웹 사이트 배포에서 코드 샘플을 사용 하 여이 자습서는 MVC 5 버전이입니다.
ms.author: aspnetcontent
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: c852f4a853d14badb6c9a1c2c1ddb7b069bc3441
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37806589"
---
<a name="aspnet-mvc-4-mobile-features"></a>ASP.NET MVC 4 모바일 기능
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> 이제는 MVC 5의 버전이이 자습서에서 샘플 코드 [ASP.NET MVC 5 모바일 웹 응용 프로그램이 Azure 웹 사이트에서 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)합니다.


이 자습서는 ASP.NET MVC 4 웹 응용 프로그램에서 모바일 기능을 사용 하는 방법의 기본 사항을 설명 합니다. 이 자습서에서는 사용할 수 있습니다 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) 또는 Visual Web Developer 2010 Express 서비스 팩 1 (&quot;VWD 또는 Visual Web Developer&quot;). 이미 있는 경우 Visual Studio professional 버전을 사용할 수 있습니다.

시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다.

- [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (권장) 또는 Visual Studio Web Developer Express SP1. Visual Studio 2012에 ASP.NET MVC 4 포함 되어 있습니다. Visual Web Developer 2010를 사용 하는 경우 설치 해야 [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)합니다.

모바일 브라우저 에뮬레이터를 해야 합니다. 다음 중 하나라도 작동 합니다.

- [Windows 7 Phone 에뮬레이터](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)합니다. (이 자습서에서는 대부분의 스크린 샷 사용 되는 에뮬레이터입니다.)
- IPhone을 에뮬레이트하는 데 사용자 에이전트 문자열을 변경 합니다. 참조 [이](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) 블로그 항목입니다.
- [Opera Mobile 에뮬레이터](http://www.opera.com/developer/tools/mobile/)
- [Apple Safari](http://www.apple.com/safari/download/) iPhone로 사용자 에이전트를 사용 하 여 합니다. Safari에서 사용자 에이전트를 "iPhone"로 하는 방법에 대 한 지침을 참조 하세요 [하도록 Safari IE 것으로 가정 하는 방법을](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) David Alison 블로그.

C# 소스 코드를 사용 하 여 visual Studio 프로젝트는 다음이 항목과 함께 사용할 수 있습니다.

- [시작 프로젝트 다운로드](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [완성 된 프로젝트 다운로드](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a>만들 내용

이 자습서에서는 추가 모바일 기능에 제공 된 간단한 회의 목록 응용 프로그램에는 [시작 프로젝트](https://go.microsoft.com/fwlink/?LinkId=228307)합니다. 다음 스크린샷은 완성된 된 응용 프로그램의 태그 페이지에서 볼 수 있듯이 합니다 [Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)합니다. 참조 [키보드 매핑에 대 한 Windows Phone 에뮬레이터](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) 키보드 입력을 단순화 하기 위해.

[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)

Internet Explorer 9 또는 10, FireFox 또는 Chrome을 설정 하 여 모바일 응용 프로그램을 개발 하는 버전을 사용할 수는 [사용자 에이전트 문자열](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)합니다. 다음 이미지에서는 iPhone을 에뮬레이션 하는 Internet Explorer를 사용 하 여 완성된 된 자습서를 보여 줍니다. Internet Explorer F-12 개발자 도구를 사용할 수 있습니다 및 [Fiddler 도구](http://www.fiddler2.com/fiddler2/) 응용 프로그램을 디버깅할 수 있도록 합니다.

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a>학습할 기술

학습할 다음과 같습니다.

- ASP.NET MVC 4 템플릿인 HTML5를 사용 하는 방법을 `viewport` 특성 및 개선 하기 위해 적응형 렌더링 모바일 장치를 표시 합니다.
- 모바일 전용 뷰를 만드는 방법입니다.
- 모바일 보기 및 응용 프로그램의 데스크톱 보기 사이 해당 사용 사용자 전환 뷰 전환기를 만드는 방법입니다.

### <a name="getting-started"></a>시작

다음 링크를 사용 하 여 시작 프로젝트에 대 한 회의 목록 응용 프로그램을 다운로드 합니다. [다운로드](https://go.microsoft.com/fwlink/?LinkId=228307)합니다. 그런 다음 Windows 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 *MvcMobile.zip* 파일을 선택 **속성**합니다. 에 **MvcMobile.zip 속성** 대화 상자를 선택 합니다 **차단 해제** 단추입니다. (사용 하려고 할 때 발생 하는 보안 경고를 방지 차단 해제 된 *.zip* 웹에서 다운로드 한 파일입니다.)

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

마우스 오른쪽 단추로 클릭 합니다 *MvcMobile.zip* 파일을 선택 **풀기** 파일 압축을 풀 합니다. Visual Studio에서 엽니다는 *MvcMobile.sln* 파일입니다.

데스크톱 브라우저에서 표시 하는 응용 프로그램을 실행 하려면 CTRL + F5 키를 누릅니다. 모바일 브라우저 에뮬레이터를 시작 회의 응용 프로그램에 대 한 URL을 에뮬레이터에 복사한 다음를 클릭 합니다 **태그로 찾아보기** 링크 합니다. Windows Phone 에뮬레이터를 사용 하는 경우 URL 표시줄에서 클릭 하 고 키보드 액세스를 일시 중지 키를 누릅니다. 아래 이미지는 *AllTags* 보기 (선택 **태그로 찾아보기**).

[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)

이 화면은 모바일 장치에서 가독성이 뛰어납니다. ASP.NET 링크를 선택 합니다.

[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)

ASP.NET 태그 뷰는 매우 복잡 합니다. 예를 들어 합니다 **날짜** 열 읽기 하기가 매우 어렵습니다. 자습서 뒷부분에서의 버전을 만든 합니다 *AllTags* 모바일 브라우저에 맞게 이며 하 게 되 면 표시를 읽을 수 있는 보기입니다.

참고: 현재 버그 모바일 캐싱 엔진 존재 합니다. 프로덕션 응용 프로그램을 설치 해야 합니다 [고정 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget 패키지 있습니다. 참조 [ASP.NET MVC 4 모바일 캐싱 버그 고정](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 수정 세부 정보에 대 한 합니다.

## <a name="css-media-queries"></a>CSS 미디어 쿼리

[CSS 미디어 쿼리](http://www.w3.org/TR/css3-mediaqueries/) 는 미디어 형식에 대 한 CSS 확장 합니다. 그러면 특정 브라우저 (사용자 에이전트)에 대 한 기본 CSS 규칙을 재정의 하는 규칙을 만들 수 있습니다. 모바일 브라우저를 대상으로 하는 CSS에 대 한 일반적인 규칙은 최대 화면 크기를 정의 합니다. 합니다 *Content\Site.css* 다음 미디어 쿼리를 포함 하는 새 ASP.NET MVC 4 인터넷 프로젝트를 만들 때 생성 되는 파일:

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

브라우저 창의 픽셀 이하로 850 픽셀 인 경우이 미디어 블록 내에서 CSS 규칙을 사용 합니다. 데스크톱 브라우저의 광범위 한 디스플레이 대 한 설계 된 기본 CSS 규칙 보다 작은 브라우저 (예: 모바일 브라우저)에서 HTML 콘텐츠를 더 나은 표시를 위해 다음과 같은 CSS 미디어 쿼리를 사용할 수 있습니다.

## <a name="the-viewport-meta-tag"></a>뷰포트 메타 태그

가상 브라우저 창 너비를 정의 하는 대부분의 모바일 브라우저 (합니다 *뷰포트*) 모바일 장치의 실제 너비 보다 훨씬 큰 합니다. 따라서 가상 표시 내의 전체 웹 페이지에 맞게 모바일 브라우저. 흥미로운 콘텐츠 사용자 확대 다음 수 있습니다. 그러나 실제 장치 너비 뷰포트 너비를 설정 하는 경우 없습니다 확대/축소 되므로 필요한 경우 모바일 브라우저에서 적합 한 콘텐츠 합니다.

뷰포트 `<meta>` ASP.NET MVC 4 레이아웃 파일에서 태그를 장치 너비로 뷰포트를 설정 합니다. 다음 줄은 뷰포트를 보여 줍니다. `<meta>` ASP.NET MVC 4 레이아웃 파일의 태그입니다.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a>CSS 미디어 쿼리 및 뷰포트 Meta 태그의 효과 검사합니다.

엽니다는 *Views\Shared\\_Layout.cshtml* 뷰포트 주석 편집기에서 파일 `<meta>` 태그입니다. 다음 태그 주석 줄을 보여 줍니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

엽니다는 *MvcMobile\Content\Site.css* 편집기에서 파일 및 미디어 쿼리에서 최대 너비를 0 픽셀로 변경 합니다. 이렇게 하면 모바일 브라우저에서 사용 되는 CSS 규칙 되지 것입니다. 다음 줄에서는 수정 된 미디어 쿼리를 보여 줍니다.

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

변경 내용을 저장 하 고 모바일 브라우저 에뮬레이터에서 회의 응용 프로그램으로 이동 합니다. 다음 이미지에 작은 텍스트는 뷰포트를 제거한 결과 `<meta>` 태그입니다. 하지 뷰포트를 사용 하 여 `<meta>` 태그 브라우저 축소 되어 기본 뷰포트 너비 (850 픽셀 또는 대부분의 모바일 브라우저에 대 한 광범위 한 있습니다.)

[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)

변경 내용을 실행 취소-뷰포트를 주석 처리 제거 `<meta>` 레이아웃 파일에서 태그 및 850 픽셀을 미디어 쿼리를 복원 합니다 *Site.css* 파일입니다. 변경 내용을 저장 하 고 모바일 친화적인 디스플레이가 복원 되었는지 확인 하려면 모바일 브라우저를 새로 고칩니다.

뷰포트 `<meta>` 태그와 CSS 미디어 쿼리 관련이 없는 ASP.NET MVC 4 및 모든 웹 응용 프로그램에서 이러한 기능을 수행할 수 있는 합니다. 하지만 이제 새 ASP.NET MVC 4 프로젝트를 만들 때 생성 되는 파일로 빌드됩니다.

뷰포트에 대 한 자세한 내용은 `<meta>` 태그를 참조 하십시오 [의 두 개의 뷰포트 A tale-2 부](http://www.quirksmode.org/mobile/viewports2.html)합니다.

다음 섹션에서는 모바일 브라우저 전용 뷰를 제공 하는 방법을 배웁니다.

## <a name="overriding-views-layouts-and-partial-views"></a>뷰, 레이아웃 및 부분 뷰 재정의

ASP.NET MVC 4의 중요 한 새로운 기능에는 모바일 브라우저는 개별 모바일 브라우저에 대 한 일반적으로 또는 특정 브라우저용 뷰 (레이아웃 및 부분 뷰 포함)를 재정의할 수 있도록 간단한 메커니즘입니다. 모바일 전용 뷰를 제공 하려면 뷰 파일을 복사한 추가 *합니다. 모바일* 파일 이름입니다. 예를 들어 모바일을 만들려는 *인덱스* 보기, 복사 *Views\Home\Index.cshtml* 하 *Views\Home\Index.Mobile.cshtml*합니다.

이 섹션에서는 모바일 전용 레이아웃 파일을 만들어야 합니다.

복사를 시작 하려면 *Views\Shared\\_Layout.cshtml* 하려면 *Views\Shared\\_Layout.Mobile.cshtml*합니다. 오픈  *\_Layout.Mobile.cshtml* 에서 제목을 변경 하 고 **MVC4 회의** 하 **회의 (모바일)** 합니다.

각 `Html.ActionLink` 호출에서 "Browse by" 각 링크를 제거 *ActionLink*합니다. 다음 코드는 모바일 레이아웃 파일의 전체 본문 섹션을 보여줍니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

복사 합니다 *Views\Home\AllTags.cshtml* 파일을 *Views\Home\AllTags.Mobile.cshtml*합니다. 새 파일을 열고 변경 된 `<h2>` 요소를 "Tags"를 "Tags (M)".

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

데스크톱 브라우저 및 모바일 브라우저 에뮬레이터를 사용 하 여 태그 페이지로 이동 합니다. 모바일 브라우저 에뮬레이터에는 두 가지 변경 내용을 보여 줍니다.

[![p2m_layoutTags.mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)

반대로 데스크톱 화면은 변경 되지 않았습니다.

[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)

## <a name="browser-specific-views"></a>브라우저 전용 뷰

모바일 및 데스크톱 전용 뷰 외에도 개별 브라우저에 대 한 보기를 만들 수 있습니다. 예를 들어 iPhone 브라우저에만 사용 되는 뷰를 만들 수 있습니다. 이 섹션에서는 iPhone 브라우저와의 iPhone 버전에 대 한 레이아웃을 만든 합니다 *AllTags* 보기.

엽니다는 *Global.asax* 파일과 다음 코드를 추가 합니다 `Application_Start` 메서드.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

이 코드는 들어오는 각 요청에 맞출 "iPhone" 이라는 새로운 디스플레이 모드를 정의 합니다. 들어오는 요청 (즉, 하는 경우 사용자 에이전트가 "iPhone" 문자열을 포함)를 정의한 조건과 일치 하는 경우 ASP.NET MVC는 이름에 "iPhone" 접미사가 포함 된 뷰를 찾습니다.

코드에서 마우스 오른쪽 단추로 클릭 `DefaultDisplayMode`, 선택 **해결**를 선택한 후 `using System.Web.WebPages;`합니다. 에 대 한 참조를 추가 하는이 `System.Web.WebPages` 네임 스페이스에 위치를 `DisplayModes` 및 `DefaultDisplayMode` 유형이 정의 됩니다.

[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)

또는 다음 줄을 직접 추가할 수는 `using` 파일의 섹션입니다.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

전체 콘텐츠를 *Global.asax* 파일은 다음과 같습니다.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

변경 내용을 저장합니다. 복사 합니다 *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* 파일을 *MvcMobile\Views\Shared\\_Layout.iPhone.cshtml*합니다. 새 파일을 열고 변경 합니다 `h1` 에서 제목 `Conference (Mobile)` 에 `Conference (iPhone)`입니다.

복사 합니다 *MvcMobile\Views\Home\AllTags.Mobile.cshtml* 파일을 *MvcMobile\Views\Home\AllTags.iPhone.cshtml*합니다. 새 파일에서 변경 된 `<h2>` 요소에서 "Tags (M)" "Tags (iPhone)"를 합니다.

응용 프로그램을 실행합니다. 모바일 브라우저 에뮬레이터를 실행, 사용자 에이전트가 "iPhone"으로 설정 되어 있는지 확인 및 이동 합니다 *AllTags* 보기. 다음 스크린 샷에 표시 된 *AllTags* 보기에서 렌더링 합니다 [Safari](http://www.apple.com/safari/download/) 브라우저. Safari에 대 한 Windows를 다운로드할 수 있습니다 [여기](https://support.apple.com/kb/DL1531)합니다.

[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)

이 섹션에서는 모바일 레이아웃 및 뷰를 만드는 방법 및 레이아웃과 iPhone과 같은 특정 장치에 대 한 보기를 만드는 방법을 살펴보았습니다. 다음 섹션에서 더 많은 매력적인 모바일 보기에 대 한 jQuery Mobile을 활용 하는 방법을 배웁니다.

## <a name="using-jquery-mobile"></a>JQuery Mobile을 사용 하 여

합니다 [jQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) 라이브러리 모바일 브라우저는 모든 주요에서 작동 하는 사용자 인터페이스 프레임 워크를 제공 합니다. jQuery Mobile 적용 *점진적인 기능 향상* CSS 및 JavaScript를 지 원하는 모바일 브라우저에 있습니다. 점진적인 기능 향상에 모든 브라우저가 더 강력한 브라우저 및 장치를 다양 한 표시를 허용 하는 동안 웹 페이지의 기본 콘텐츠를 표시할 수 있습니다. JQuery Mobile 사용 하 여 포함 된 JavaScript 및 CSS 파일에 태그를 변경 하지 않고 모바일 브라우저에 맞게 여러 요소 스타일입니다.

이 섹션에서는 설치를 *jQuery.Mobile.MVC* 뷰 전환기 위젯 및 jQuery Mobile을 설치 하는 NuGet 패키지.

삭제를 시작 하려면 합니다 *공유\\_Layout.Mobile.cshtml* 하 고 *공유\\_Layout.iPhone.cshtml* 이전에 만든 파일입니다.

이름 바꾸기 *Views\Home\AllTags.Mobile.cshtml* 하 고 *Views\Home\AllTags.iPhone.cshtml* 파일을 *Views\Home\AllTags.iPhone.cshtml.hide* 고  *Views\Home\AllTags.Mobile.cshtml.hide*합니다. 파일이 더 이상 없으므로 *.cshtml* 확장을 렌더링 하는 ASP.NET MVC 런타임에서 사용 되지 않으므로 합니다 *AllTags* 보기.

설치 합니다 *jQuery.Mobile.MVC* 이 수행 하 여 NuGet 패키지:

1. **도구** 메뉴에서 **라이브러리 패키지 관리자**를 선택한 후 **패키지 관리자 콘솔**합니다.

    [![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)
2. 에 **패키지 관리자 콘솔**, 입력 `Install-Package jQuery.Mobile.MVC -version 1.0.0`

다음 이미지는 추가 및 MvcMobile 프로젝트에 NuGet jQuery.Mobile.MVC 패키지에서 변경 된 파일을 보여줍니다. 파일 이름 뒤에 오는 추가 [추가]가 추가 된 파일입니다. 이미지 GIF를 표시 하지 않습니다 하 고 PNG 파일을 추가 합니다 *Content\images* 폴더입니다.

![](aspnet-mvc-4-mobile-features/_static/image21.png)

다음 jQuery.Mobile.MVC NuGet 패키지를 설치합니다.

- 합니다 *앱\_Start\BundleMobileConfig.cs* 추가 jQuery JavaScript 및 CSS 파일을 참조 하는 데 필요한 파일입니다. 아래 지침에 따라를이 파일에 정의 된 모바일 번들을 참조 해야 합니다.
- jQuery Mobile CSS 파일입니다.
- A `ViewSwitcher` 컨트롤러 위젯 (*Controllers\ViewSwitcherController.cs*).
- jQuery Mobile JavaScript 파일입니다.
- JQuery Mobile 스타일 레이아웃 파일 (*Views\Shared\\_Layout.Mobile.cshtml*).
- 뷰 전환기 부분 뷰 *(MvcMobile\Views\Shared\\_ViewSwitcher.cshtml*) 모바일 뷰로 이동 하 고 그 반대의 경우 바탕 화면 보기에서 전환 하려면 각 페이지의 맨 위에 있는 링크를 제공 합니다.
- 여러<em>.png</em> 하 고 <em>.gif</em> 이미지 파일을 <em>Content\images</em> 폴더입니다.

엽니다는 *Global.asax* 파일과 다음 코드의 마지막 줄으로 추가 `Application_Start` 메서드.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

다음 코드에서는 전체 *Global.asax* 파일입니다.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> Internet Explorer 9를 사용 하 고 표시 되지 않는 경우는 `BundleMobileConfig` 줄 위에 노란색 강조 표시를 클릭 합니다 [호환성 보기 단추](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![(해제) 호환성 뷰 단추 그림] (http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg " (해제) 호환성 뷰 단추 그림") 개요에서 변경 아이콘을 ie ![(해제) 호환성 뷰 단추 그림](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "(해제) 호환성 뷰 단추 그림 ") 단색 ![(켜기) 호환성 뷰 단추 그림](http://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "(on) 호환성 뷰 단추 그림")합니다. 또는 FireFox 또는 Chrome에서이 자습서를 볼 수 있습니다.


엽니다는 *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* 파일과 후 직접 다음 태그를 추가 합니다 `Html.Partial` 호출:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

전체 *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* 파일은 다음과 같습니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

응용 프로그램을 빌드하고 모바일 브라우저 에뮬레이터에서로 이동 합니다 *AllTags* 보기. 다음 표시 됩니다.

[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)

> [!NOTE]
> 특정 모바일 코드를 디버깅할 수 있습니다 [사용자 에이전트 문자열을 설정](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) IE 또는 iPhone 및 다음 F-12 개발자 도구를 사용 하 여 Chrome에 대 한 합니다. 모바일 브라우저가 표시 되지 않는 경우는 **홈**를 **발표자**를 **태그**, 및 **날짜** 단추 링크로, jQuery Mobile에 대 한 참조 스크립트 및 CSS 파일은 올바른 되지 않을 수 있습니다.


표시 스타일이 변경 하는 것 외에도 **모바일 보기 표시** 및 모바일 보기에서 데스크톱 보기로 전환할 수 있는 링크입니다. 선택 된 **바탕 화면 보기** 링크 및 바탕 화면 보기에 표시 됩니다.

[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)

바탕 화면 보기에는 모바일 보기로 직접 이동 하는 방법을 제공 하지 않습니다. 이제 수정 됩니다. 엽니다는 *Views\Shared\\_Layout.cshtml* 파일입니다. 페이지에서 방금 `body` 요소인 뷰 전환기 위젯을 렌더링 하는 다음 코드를 추가 합니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

새로 고침 합니다 *AllTags* 모바일 브라우저에서 보기. 이제 데스크톱 및 모바일 뷰 간에 탐색할 수 있습니다.

[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)

> [!NOTE]
> 참고 디버그:는 Views\Shared의 끝에 다음 코드를 추가할 수 있습니다\\_ViewSwitcher.cshtml 브라우저 사용자 에이전트 문자열을 사용 하 여 모바일 장치를 설정 하는 경우 뷰를 디버깅할 수 있도록 합니다.
> 
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
> 
>  다음 머리글을 추가 합니다 *Views\Shared\\_Layout.cshtml* 파일입니다.  
> 
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]


로 이동 합니다 *AllTags* 데스크톱 브라우저에서 페이지입니다. 뷰 전환기 위젯 모바일 레이아웃 페이지에만 추가 되므로 데스크톱 브라우저에 표시 되지 않습니다. 이 자습서의 뒷부분에 나오는 데스크톱 뷰로 뷰 전환기 위젯을 추가 하는 방법을 볼 수 있습니다.

[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)

## <a name="improving-the-speakers-list"></a>발표자 목록 개선

모바일 브라우저에서 선택 합니다 **발표자** 링크 합니다. 모바일 뷰가 있기 때문에 (*AllSpeakers.Mobile.cshtml*), 기본 발표자 표시 (*AllSpeakers.cshtml*) 모바일 레이아웃 뷰를 사용 하 여 렌더링 됩니다 ( *\_ Layout.Mobile.cshtml*).

[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)

렌더링 모바일 레이아웃 내에서 기본 (모바일 아님) 뷰를 설정 하 여 전역적으로 비활성화할 수 있습니다 `RequireConsistentDisplayMode` 에 `true` 에 *뷰\\_ViewStart.cshtml* 같이 파일:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

때 `RequireConsistentDisplayMode` 로 설정 된 `true`, 모바일 레이아웃 (<em>\_Layout.Mobile.cshtml</em>) 모바일 뷰에 대해서만 사용 됩니다. (뷰 파일 즉, 양식의 <em>* * ViewName</em><em>합니다. Mobile.cshtml</em>.) 설정 하려는 `RequireConsistentDisplayMode` 에 `true` 모바일 레이아웃이 비모바일 보기에서 잘 작동 하지 않는 경우. 아래 스크린샷에서 하는 방법을 <em>발표자</em> 페이지를 렌더링 하는 경우 `RequireConsistentDisplayMode` 로 설정 된 `true`합니다.

[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)

보기에서 일관 된 표시 모드가 설정 하 여 비활성화할 수 있습니다 `RequireConsistentDisplayMode` 에 `false` 뷰 파일에서 합니다. 다음 태그는 *Views\Home\AllSpeakers.cshtml* 파일 집합 `RequireConsistentDisplayMode` 하려면 `false`:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a>모바일 발표자 뷰 만들기

방금 본 것 처럼 합니다 *발표자* 뷰도 가독성은 있지만 링크가 작은 되며 모바일 장치에서 누르기 어렵습니다. 이 섹션에서는 모바일 전용을 만든 *발표자* 다음과 같은 최신 모바일 응용 프로그램 보기-큰 표시, 누르기 쉬운 링크 및 스피커를 신속 하 게 찾을 수 있는 검색 상자가 포함 됩니다.

복사본 *AllSpeakers.cshtml* 하 *AllSpeakers.Mobile.cshtml*합니다. 엽니다는 *AllSpeakers.Mobile.cshtml* 파일을 제거는 `<h2>` 제목 요소입니다.

에 `<ul>` 태그를 추가 합니다 `data-role` 특성 및 해당 값을 설정 `listview`합니다. 와 같은 다른 [ `data-*` 특성](http://html5doctor.com/html5-custom-data-attributes/), `data-role="listview"` 큰 목록 항목을 쉽게 탭에 게 합니다. 완료 된 태그의 모양은 다음과 같습니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

모바일 브라우저를 새로 고칩니다. 업데이트 된 뷰는 다음과 같습니다.

[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)

모바일 뷰를 향상 되어 있지만 긴 발표자 목록을 탐색 하기가 어렵습니다. 이 문제를 해결 하는 `<ul>` 태그를 추가 합니다 `data-filter` 특성 및 설정 `true`합니다. 아래 코드는 `ul` 태그입니다.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

다음 이미지는 결과로 생성 되는 페이지의 맨 위에 있는 검색 필터 상자를 표시 합니다 `data-filter` 특성입니다.

[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)

검색 상자에 각 문자를 입력할 jQuery Mobile 아래 그림과에서 같이 표시 된 목록을 필터링 합니다.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)

## <a name="improving-the-tags-list"></a>태그 목록 개선

기본값이 마음 *스피커* 뷰를 *태그* 뷰도 가독성은 있지만 링크가 작고 모바일 장치에서 누르기 어렵습니다. 수정이 섹션에서는 합니다 *태그* 수정한 동일한 방식으로 보기를 *발표자* 보기.

제거는 &quot;숨기기&quot; 접미사는 *Views\Home\AllTags.Mobile.cshtml.hide* 파일 이름 이므로 *Views\Home\AllTags.Mobile.cshtml*합니다. 이름이 바뀐된 파일을 열고 제거는 `<h2>` 요소입니다.

추가 된 `data-role` 하 고 `data-filter` 특성을 `<ul>` 태그를 다음과 같이:

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

아래 이미지에서 문자 필터링 태그 페이지를 보여 줍니다. `J`합니다.

[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)

## <a name="improving-the-dates-list"></a>날짜 목록 개선

향상 시킬 수 있습니다는 *날짜* 향상 같은 보기를 *발표자* 및 *태그* 뷰를 쉽게 모바일 장치에서 사용할 수 있도록 합니다.

복사 합니다 *Views\Home\AllDates.cshtml* 파일을 *Views\Home\AllDates.Mobile.cshtml*합니다. 새 파일을 열고 제거는 `<h2>` 요소입니다.

추가 `data-role="listview"` 에 `<ul>` 다음과 같은 태그:

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

아래 이미지 보여 줍니다 합니다 **날짜** 사용 하 여 페이지는 다음과 같은 `data-role` 진행에서 특성.

[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) 의 내용을 대체 합니다 *Views\Home\AllDates.Mobile.cshtml* 를 다음 코드로 파일:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

이 코드는 일까 지 모든 세션을 그룹화합니다. 각 날마다 목록 구분선을 생성 및 구분선 아래에서 각 날짜에 대 한 모든 세션을 나열 합니다. 모양이 코드를 실행할 때 다음과 같습니다.

[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)

## <a name="improving-the-sessionstable-view"></a>SessionsTable 뷰 개선

이 섹션에서는 세션의 모바일 전용 뷰를 만들어야 합니다. 우리가 변경 내용을 만들었습니다 다른 보기에서는 보다 더 광범위 한 됩니다.

모바일 브라우저에서 탭의 **스피커** 단추를 선택한 다음 입력 `Sc` 검색 상자에 합니다.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)

탭의 **Scott hanselman이** 링크 합니다.

[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)

알 수 있듯이 표시를 모바일 브라우저에서는 읽기가 어렵습니다. 날짜 열이 읽기 어려운 및 태그 열 뷰를 벗어났습니다. 이 문제를 해결 하려면 복사 *Views\Home\SessionsTable.cshtml* 하 *Views\Home\SessionsTable.Mobile.cshtml*, 파일의 내용을 다음 코드로 바꿉니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

코드 열 태그 및이 모든 정보를 모바일 브라우저에서 읽을 수 있도록 제목, 강연자 및 날짜를 세로로 형식 대화방을 제거 합니다. 아래 이미지에 코드 변경 내용을 반영합니다.

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)

## <a name="improving-the-sessionbycode-view"></a>SessionByCode 뷰 개선

모바일 전용 뷰를 마지막으로 만들어야 합니다 *SessionByCode* 보기. 모바일 브라우저에서 탭의 **스피커** 단추를 선택한 다음 입력 `Sc` 검색 상자에 합니다.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)

탭의 **Scott hanselman이** 링크 합니다. Scott Hanselman의 세션이 표시 됩니다.

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)

선택 된 **MS 웹 Love 스택의 개요** 링크 합니다.

[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)

기본 바탕 화면 보기 정상 이지만 향상 시킬 수 있습니다.

복사 합니다 *Views\Home\SessionByCode.cshtml* 에 *Views\Home\SessionByCode.Mobile.cshtml* 의 내용을 바꾸고는 *Views\Home\SessionByCode.Mobile.cshtml*파일에 다음 태그를 사용 하 여:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

새 태그를 사용 하는 `data-role` 특성 뷰의 레이아웃을 개선 합니다.

모바일 브라우저를 새로 고칩니다. 다음 이미지는 방금 만든 코드 변경 내용을 반영 합니다.

[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)

## <a name="wrapup-and-review"></a>Wrapup 및 검토

이 자습서는 ASP.NET MVC 4 Developer Preview의 새로운 모바일 기능을 도입 했습니다. 모바일 기능에는 다음이 포함 됩니다.

- 전역적으로 그리고 개별 뷰에 대해 레이아웃, 뷰 및 부분 뷰를 재정의할 수 있습니다.
- 레이아웃 및 부분 재정의 하 여에 대 한 제어를 `RequireConsistentDisplayMode` 속성입니다.
- 모바일 뷰 전환기 위젯 데스크톱 보기에 표시할 수 있는 보기입니다.
- IPhone 브라우저 등 특정 브라우저를 지원 하기 위한 지원 합니다.

## <a name="see-also"></a>참고 항목

- [jQuery Mobile](http://jquerymobile.com) 사이트입니다.
- [jQuery Mobile 개요](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [W3C 권장 사항 모바일 웹 응용 프로그램 모범 사례](http://www.w3.org/TR/mwabp/)
- [미디어 쿼리에 대 한 W3C 후보 권장 사항](http://www.w3.org/TR/css3-mediaqueries/)
