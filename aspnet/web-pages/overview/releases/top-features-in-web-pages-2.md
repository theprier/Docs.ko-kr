---
uid: web-pages/overview/releases/top-features-in-web-pages-2
title: ASP.NET 웹 페이지 2의에서 주요 기능 | Microsoft Docs
author: microsoft
description: 이 항목에서는 ASP.NET 웹 페이지 2는 WebMatr와 함께 포함 되는 경량 웹 프로그래밍 프레임 워크의 상위 새로운 기능의 개요를 제공...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/13/2012
ms.topic: article
ms.assetid: cc712e72-c3d0-4e43-bc2d-28cc09cd8f71
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/releases/top-features-in-web-pages-2
msc.type: authoredcontent
ms.openlocfilehash: f0d32edd3ab54c55aa06c803cd91e01cbbb8f08a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="the-top-features-in-aspnet-web-pages-2"></a>ASP.NET 웹 페이지 2에서에서 최상위 기능
====================
by [Microsoft](https://github.com/microsoft)

> 이 문서에서는 ASP.NET 웹 페이지 2 RC와 함께 포함 되는 경량 웹 프로그래밍 프레임 워크의에서 상위 새로운 기능의 개요를 제공 [Microsoft WebMatrix 2 RC](https://www.microsoft.com/web/)합니다.
> 
> **포함 된 내용:** 
> 
> - [WebMatrix를 설치합니다.](#install)
> - [새로운 기능과 향상 된 기능](#New_and_Enhanced_Features)
> 
>     - [RC 릴리스에 대 한 변경 내용](#Changes_for_the_RC_Version)
>     - [베타 릴리스 버전에 대 한 변경](#Changes_for_the_Beta_Version)
>     - [새로운 또는 업데이트 된 사이트 서식 파일 사용](#templates)
>     - [사용자 입력 유효성 검사](#validation)
>     - [Facebook 및 OAuth 및 OpenID를 사용 하 여 다른 사이트에서의 로그인을 사용 하도록 설정](#oauthsetup)
>     - [지도 도우미를 사용 하 여 맵 추가](#maphelper)
>     - [웹 페이지 응용 프로그램 Side-by-side 실행](#sidebyside)
>     - [모바일 장치에 대 한 페이지 렌더링](#mobile)
> - [추가 리소스](#resources)
> 
> > [!NOTE]
> > 이 항목에서는 ASP.NET 웹 페이지 2 코드로 작업 하려면 WebMatrix를 사용 한다고 가정 합니다. 그러나 웹 페이지 1도 Visual Studio를 사용 하 여 웹 페이지 2 웹 사이트를 만들 수 있으므로, 제공 하는 향상 된 IntelliSense 기능 및 디버깅 합니다. Visual Studio에서 웹 페이지를 사용 하려면 먼저 Visual Studio 2010 SP1, Visual Web Developer Express 2010 SP1, 또는 Visual Studio 11 베타를 설치 해야 합니다. Visual Studio에서 ASP.NET MVC 4 및 웹 페이지 2 응용 프로그램을 만들기 위한 템플릿과 도구를 포함 하는 ASP.NET MVC 4 베타를 설치 합니다.
> 
> 
> *마지막 업데이트: 2012 년 6 월 18*


<a id="install"></a>
## <a name="installing-webmatrix"></a>WebMatrix를 설치합니다.

웹 페이지를 설치 하려면 Microsoft 웹 플랫폼 설치 관리자를 설치 하 고 구성할 웹 관련 기술을 활용할 수 있는 무료 응용 프로그램에는 사용할 수 있습니다. 웹 페이지 2 베타를 포함 하는 WebMatrix 2 베타를 설치 합니다.

1. 웹 플랫폼 설치 관리자의 최신 버전에 대 한 설치 페이지로 이동 합니다.

    [https://go.microsoft.com/fwlink/?LinkId=226883](https://go.microsoft.com/fwlink/?LinkId=226883)

    > [!NOTE]
    > 이미 WebMatrix 1이 설치 되어 있으면이 설치 WebMatrix 2 베타로 업데이트 됩니다. 동일한 컴퓨터에서 버전 1 또는 2를 사용 하 여 만든 웹 사이트를 실행할 수 있습니다. 자세한 내용은 섹션을 참조 [실행 웹 페이지 응용 프로그램 나란히](#sidebyside)합니다.
2. 선택 **지금 설치**합니다. 

    Internet Explorer를 사용 하는 경우 다음 단계로 이동 합니다. Google Chrome 또는 Mozilla Firefox와 같은 다른 브라우저를 사용 하는 메시지가 저장 된 *Webmatrix.exe* 파일을 컴퓨터입니다. 파일 저장 한 다음 설치 관리자를 시작 하려면 클릭 합니다.
3. 설치 프로그램을 실행 하 고 선택 된 **설치** 단추입니다. WebMatrix 및 웹 페이지를 설치합니다.

## <a id="New_and_Enhanced_Features"></a>  새로운 기능과 향상 된 기능

### <a id="Changes_for_the_RC_Version"></a>  (2012 년 6 월) RC 버전에 대 한 변경 내용

2012 년 6 월의에서 RC 버전에는 2012 년 3 월에에서 출시 된 베타 버전 새로 고침에서 몇 가지 변경 되었습니다. 이러한 변경은 다음과 같습니다.

- A `Validation.AddFormError` 에 추가 된 메서드는 `Validation` 도우미입니다. 유효성 검사를 수동으로 수행 하는 경우에 유용 (예를 들어 하면 유효성 검사 쿼리 문자열에 전달 되는 값)으로 표시 되는 오류 메시지를 추가 하려면는 `Html.ValidationSummary` 메서드. 자세한 내용은 섹션을 참조 하십시오. [유효성 검사 데이터는 하지 않습니다 제공 직접에서 사용자](https://go.microsoft.com/fwlink/?LinkId=253002#Validating_Data_That_Doesnt_Come_Directly_from_Users) 에 [ASP.NET 웹 페이지 (Razor) 사이트의 사용자 입력 유효성 검사](https://go.microsoft.com/fwlink/?LinkId=253002)합니다.
- 묶음 및 축소의 기능이 핵심 ASP.NET 웹 페이지 2 어셈블리에서 제거 되었습니다. 결과적으로 `Assets` 이 문서의 뒷부분에 나열 된 도우미를 사용할 수 없습니다. 대신 설치 해야는 [ASP.NET 최적화](http://nuget.org/packages/Microsoft.Web.Optimization/0.1) NuGet 패키지 합니다. 자세한 내용은 참조 [묶음 및 축소 자산 ASP.NET 웹 페이지 (Razor) 사이트의](https://go.microsoft.com/fwlink/?LinkId=255373)합니다.
- ASP.NET 웹 페이지 2를 지원 하기 위해 추가 어셈블리 추가 되었습니다. 이러한 변경의만 두드러지는 효과 사이트에서 더 많은 어셈블리를 표시 될 수 있습니다는 *bin* 폴더 후에 사이트를 만들거나를 호스팅 공급자는 사이트를 배포 합니다.

<a id="Changes_for_the_Beta_Version"></a>
### <a name="changes-for-the-beta-version-february-2012"></a>베타 버전 (2012 년 2 월)에 대 한 변경

2012 년 2 월에에서 릴리스된 베타 버전은 2011 년 12 월에에서 발표 되었지만 베타 버전에서 몇 가지 변경 내용만 있습니다. 이러한 변경은 다음과 같습니다.

- 이제 razor 조건부 특성을 지원합니다. Html에서 요소를 값으로 특성 설정 하는 경우에 서버 코드에서 해결 `false` 또는 `null`, ASP.NET 특성을 전혀 렌더링 하지 않습니다. 예를 들어, 확인란에 대 한 다음 태그를 있다고 가정해 보겠습니다.

    [!code-html[Main](top-features-in-web-pages-2/samples/sample1.html)]

    하는 경우의 값 `checked1` 확인 `false` 또는 `null`, `checked` 특성은 렌더링 되지 않습니다. 주요 변경 내용입니다.
- `Validation.GetHtml` 메서드 이름이 `Validation.For`합니다. 이 주요 변경 내용. `Validation.GetHtml` 베타 릴리스 버전에서 작동 하지 것입니다.
- 이제 포함할 수 있습니다는 `~` 사이트 루트를 사용 하지 않고 참조 하려면 태그에서 연산자는 `Href` 함수입니다. (즉, Razor 파서가 이제 찾을 하 고 확인할 수는 `~` 연산자에 대 한 명시적 메서드 호출을 요구 하지 않고 `Href`.) `Href` 여전히 사용할 수 있는 방법, 그럼, 이것은 주요 변경 내용입니다.

    예를 들어, 다음과 같은 태그를 이전에 설치한 경우:

    `<a href="@Href("~/Default.cshtml")">Home</a>`

    이제 다음과 같은 태그를 사용할 수 있습니다.

    `<a href="~/Default.cshtml">Home</a>`
- `Scripts` 으로 대체 되었습니다 (리소스) 자산 관리를 위한 도우미는 `Assets` 도우미에는 다음과 같이 약간 다른 방법을:

  - 에 대 한 `Scripts.Add`를 사용 하 여 `Assets.AddScript`
  - 에 대 한 `Scripts.GetScriptTags`를 사용 하 여 `Assets.GetScripts`

    이 주요 변경 내용. `Scripts` 클래스는 베타 릴리스 버전에서 사용할 수 없습니다. 자산 관리를 사용 하는이 문서의 코드 예제는 이러한 변경으로 인해 업데이트 되었습니다.

<a id="templates"></a>
### <a name="using-the-new-and-updated-site-templates"></a>새로운 또는 업데이트 된 사이트 서식 파일 사용

**시작 사이트** 에 템플릿이 업데이트 된 웹 페이지 2에서 실행 되도록 기본적으로 합니다. 다음과 같은 새로운 기능이 포함 됩니다.

- 모바일에서 잘 작동 페이지 렌더링 합니다. CSS 스타일 사용 하 여 및 `@media` 선택기는 **시작 사이트** 모바일 장치 화면을 포함 하는 보다 작은 화면에 페이지의 향상 된 렌더링을 제공 합니다.
- 향상 된 멤버 자격 및 인증 옵션입니다. Twitter, Facebook, 및 Windows Live와 같은 다른 소셜 네트워킹 사이트에서 자신의 계정을 사용 하 여 사이트에 사용자가 로그인 하도록 할 수 있습니다. 자세한 내용은 참조는 [Facebook 및 OAuth 및 OpenID를 사용 하 여 다른 사이트에서의 로그인을 사용 하도록 설정](#oauthsetup) 섹션.
- HTML5 요소입니다.

새 **개인 사이트** 템플릿을 사용 하는 개인 블로그, 사진 페이지 및 Twitter 페이지를 포함 하는 웹 사이트를 만들 수 있습니다. 에 따라 사이트를 사용자 지정할 수는 **개인 사이트** 서식 파일에서 다음을 수행 하 여:

- 레이아웃 파일을 편집 하 여 사이트의 모양을 변경 (*\_SiteLayout.cshtml*)와 스타일 파일 (*Site.css*).
- 사이트에 기능을 추가 하는 NuGet 패키지를 설치 합니다. 에 대 한 자습서 참조 ASP.NET Web Helpers Library를 포함 하 여 패키지를 설치 하는 방법에 대 한 내용은 [설치 도우미](https://go.microsoft.com/fwlink/?LinkId=202889#webhelpers)합니다.

액세스는 **개인 사이트** 서식 파일을 선택 **템플릿** 는 WebMatrix에서 **빠른 시작** 화면입니다.

[![topseven-personalsite-1](top-features-in-web-pages-2/_static/image2.png)](top-features-in-web-pages-2/_static/image1.png)

에 **템플릿** 대화 상자에서 선택 하는 **개인 사이트** 템플릿.

[![topseven-personalsite-2](top-features-in-web-pages-2/_static/image4.png)](top-features-in-web-pages-2/_static/image3.png)

방문 페이지는 **개인 사이트** 페이지 및 사진 페이지 Twitter 템플릿을 사용 하면 블로그의 설정에 대 한 링크를 수행 합니다.

[![topseven-personalsite-3](top-features-in-web-pages-2/_static/image6.png)](top-features-in-web-pages-2/_static/image5.png)

<a id="validation"></a>
### <a name="validating-user-input"></a>사용자 입력 유효성 검사

웹 페이지 1, 제출 된 양식에 사용자 입력 유효성 검사를 사용 하 여는 `System.Web.WebPages.Html.ModelState` 클래스입니다. (코드 샘플 중 몇 개에 라는 웹 페이지 1 자습서에 설명 되어 [데이터로 작업](../data/5-working-with-data.md).) 웹 페이지 2에이 방법을 계속 사용할 수 있습니다. 그러나 웹 페이지 2는 또한 사용자 입력 유효성 검사에 대 한 향상 된 도구를 제공 합니다.

- 새로운 유효성 검사 클래스를 포함 하 여 `System.Web.WebPages.ValidationHelper` 및 `System.Web.WebPages.Validator`, 몇 줄의 코드로 강력한 유효성 검사 작업을 수행할 수 있도록 합니다.
- 필요에 따라 유효성 검사 오류를 확인 하려면 서버에 왕복을 요구 하는 대신 사용자에 대 한 즉각적인 피드백을 제공 하는 클라이언트 쪽 유효성 검사 합니다. (보안상의 이유로 유효성 검사는 수행 서버에서 미리 클라이언트에서 수행 된 검사 하는 경우에.)

새 유효성 검사 기능을 사용 하려면 다음을 수행 합니다.

페이지의 코드에서 메서드를 사용 하 여 유효성을 검사 하려면 요소를 등록 하는 `Validation` 도우미: `Validation.RequireField`, `Validation.RequireFields` (필요한 것으로 여러 요소를 등록)을, 또는 `Validation.Add`합니다. `Add` 메서드 다른 종류의 데이터 형식 검사, 여러 필드 문자열 길이 검사에서에서 항목을 비교와 같은 유효성 검사를 지정할 수 있습니다 및 (정규식을 사용 하 여) 패턴. 다음은 몇 가지 예입니다.

[!code-html[Main](top-features-in-web-pages-2/samples/sample2.html)]

필드 관련 오류를 표시 하려면 호출 `Html.ValidationMessage` 유효성을 검사할 각 요소에 대 한 태그에:

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample3.cshtml)]

요약 정보를 표시 하려면 (`<ul>` 목록)의 페이지에서 모든 오류 `Html.ValidationSummary` 태그에서:

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample4.cshtml)]

이러한 단계는 서버 쪽 유효성 검사를 구현 하기에 충분 합니다. 클라이언트 쪽 유효성 검사를 추가 하려는 경우 또한 다음 수행 합니다.

내부 다음 스크립트 파일 참조를 추가할는 `<head>` 웹 페이지의 섹션입니다. 처음 두 개의 스크립트 참조 콘텐츠 배달 네트워크 (CDN) 서버에 원격 파일을 가리킵니다. 세 번째 참조가 로컬 스크립트 파일을 가리킵니다. CDN을 사용할 수 없는 경우 프로덕션 응용 프로그램에 대체를 구현 해야 합니다. 대체 (fallback)를 테스트 합니다.

[!code-html[Main](top-features-in-web-pages-2/samples/sample5.html)]

로컬 복사본을 가져오는 가장 쉬운 방법은 *jquery.validate.unobtrusive.min.js* 라이브러리 (예: 시작 사이트) 사이트 템플릿 중 하나를 기반으로 새 웹 페이지 사이트를 만드는 것입니다. 템플릿에서 만든 사이트에 포함 되어 *jquery.validate.unobtrusive.js* 파일을 복사할 수 있습니다 프로그램 사이트로 스크립트 폴더에 있습니다.

웹 사이트를 사용 하는 경우는<em>\_SiteLayout</em> 페이지 레이아웃을 제어 하려면 페이지에서 유효성 검사는 모든 콘텐츠 페이지를 사용할 수 있도록 해당 페이지에서 다음 스크립트 참조를 포함할 수 있습니다. 특정 페이지에 대해서만 유효성 검사를 수행 하려는 경우에 해당 페이지에 스크립트 등록 자산 관리자를 사용할 수 있습니다. 이 작업을 수행 하려면 호출 `Assets.AddScript(path)` 유효성을 검사 하 여 각 스크립트 파일을 참조 하는 페이지에 있습니다. 다음에 대 한 호출을 추가 `Assets.GetScripts` 에  <em>\_SiteLayout</em> 등록 된 렌더링 하는 데는 페이지 `<script>` 태그입니다. 자세한 내용은 섹션을 참조 하십시오. [자산 관리자를 사용 하 여 스크립트 등록](#resmanagement)합니다.

개별 요소에 대 한 태그를 호출 하 여 `Validation.For` 메서드. 이 메서드는 특성에서 해당 jQuery 클라이언트 쪽 유효성 검사를 제공 하기 위해 연결할 수 있습니다. 예를 들어:

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample6.cshtml)]

다음 예제에서는 양식에서 사용자 입력의 유효성을 검사 하는 페이지를 보여 줍니다. 이 유효성 검사 코드를 실행 하 고 테스트를이 작업을 수행 합니다.

1. 포함 된 WebMatrix 2 사이트 템플릿 중 하나를 사용 하 여 새 웹 사이트 만들기는 *스크립트* 폴더와 같은 **시작 사이트** 템플릿.
2. 새 사이트에서 만드는 새 *.cshtml* 페이지 및 페이지의 내용을 다음 코드로 바꿉니다.
3. 브라우저에서 페이지를 실행 합니다. 유효성 검사에 미치는 영향을 확인 하기 위해 유효 하지 않은 값을 입력 합니다. 예를 들어 필수 필드 지정 하지 않거나에 문자를 입력 하 고 **크레딧** 필드입니다.


[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample7.cshtml)]

사용자가 유효한 입력을 제출할 때 페이지는 다음과 같습니다.

[![topSeven-valid-1](top-features-in-web-pages-2/_static/image8.png)](top-features-in-web-pages-2/_static/image7.png)

비워 두는 필수 필드와 사용자가 전송 하는 경우 페이지는 다음과 같습니다.

[![topSeven-valid-2](top-features-in-web-pages-2/_static/image10.png)](top-features-in-web-pages-2/_static/image9.png)

사용자가 아닌 다른 정수 제출 페이지가 표시 되어는 **크레딧** 필드:

[![topSeven-valid-3](top-features-in-web-pages-2/_static/image12.png)](top-features-in-web-pages-2/_static/image11.png)

자세한 내용은 다음 블로그 게시물을 참조 하십시오.

- [웹 페이지 v 2에서 유효성 검사를 업데이트](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2344) 을 유효성 검사를 사용 하 여 추가 기본적인은 `Validation` 도우미 (서버 쪽에만 해당)
- [웹 페이지 v2, 2 부에서에서 유효성 검사를 업데이트](http://www.mikepope.com/blog/DisplayBlog.aspx?permalink=2347) 클라이언트 쪽 유효성 검사를 추가 합니다.
- [웹 페이지 v 2, 3 부에서에서 유효성 검사를 업데이트](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2351) 서식 유효성 검사 오류입니다.

<a id="resmanagement"></a>
### <a name="registering-scripts-using-the-assets-manager"></a>자산 관리자를 사용 하 여 스크립트를 등록 하는 중

자산 관리자에 등록 하 고 클라이언트 스크립트를 렌더링 서버 코드에서 사용할 수 있는 새로운 기능입니다. 이 기능은 런타임에 단일 페이지에 결합 된 여러 개의 파일 (예: 레이아웃 페이지, 콘텐츠 페이지, 도우미 등)에서 코드를 사용 하 여 작업할 때 유용 합니다. 자산 관리자도 스크립트 파일을 올바르게 참조 하 고 효율적으로 렌더링된 된 페이지에서 호출 되는 코드 파일에 관계 없이 또는 몇 번 호출 되었는지 확인 하는 소스 파일을 조정 합니다. 자산 관리자 렌더링 `<script>` 적절 한 위치에 태그를 신속 하 게 (다운로드 하지 않고 렌더링 하는 동안 스크립트) 페이지 로드할 수 있으며 스크립트 렌더링 되기 전에 호출 된 경우 발생할 수 있는 오류를 방지 하기 위해 완료 된 되도록 합니다.

예를 들어 JavaScript 파일을 호출 하는 사용자 지정 도우미를 만들어야 하 고 콘텐츠 페이지 코드에서 세 가지 다른 곳에서이 도우미를 호출 합니다. 스크립트 호출 세 가지 도우미에서 등록 하는 자산 관리자를 사용 하지 않으면 `<script>` 모든 지점에서 동일한 스크립트 파일에 렌더링 된 페이지에 표시 되는 태그입니다. 또한을 계산한는 `<script>` 렌더링된 된 페이지에 태그를 삽입, 스크립트를 페이지가 완전히 로드 하기 전에 특정 페이지 요소에 액세스 하려고 하는 경우 오류가 발생할 수 있습니다. 자산 관리자를 사용 하 여 해당 스크립트를 등록 하는 경우 이러한 문제를 방지 합니다.

자산 관리자와이 수행 하 여 스크립트를 등록할 수 있습니다.

- 스크립트를 참조 해야 하는 코드를 호출 하 여 `Assets.AddScript` 메서드.
- 에  *\_SiteLayout* 페이지에서 호출는 `Assets.GetScripts` 렌더링 하는 메서드는 `<script>` 태그입니다. 

    > [!NOTE]
    > 에 대 한 호출을 배치 `Assets.GetScripts` 의 마지막 항목으로는 `<body>` 의 요소는  *\_SiteLayout* 페이지. 이 페이지를 통해 더 빠르게 로드 하 고 스크립트 오류를 방지할 수 있습니다.

다음 예제 자산 관리자의 작동 방법을 보여 줍니다. 코드는 다음 항목이 포함 되어 있습니다.

- 명명 된 사용자 지정 도우미 `MakeNote`합니다. 이 도우미를 묶어서 상자 내의 문자열을 렌더링 한 `div` 요소로 둘러싼 있는 스타일이 지정 테두리가 있는 만들고 추가 하 여 &quot;참고:&quot; 를 합니다. 도우미는 또한 메모에 런타임 동작을 추가 하는 JavaScript 파일을 호출 합니다. 포함 하는 스크립트를 참조 하지 않고는 `<script>` 호출 하 여 스크립트를 등록 하는 태그 도우미 `Assets.AddScript` 합니다.
- JavaScript 파일입니다. 이것은 도우미에 의해 호출 되는 파일이 고 일시적으로 증가 하는 동안 메모 항목의 글꼴 크기는 `mouseover` 이벤트입니다.
- 참조 하는 콘텐츠 페이지는<em>\_SiteLayout</em> 페이지 본문의 일부 콘텐츠를 렌더링 한 다음 호출에서 `MakeNote` 도우미입니다.
- A  *\_SiteLayout* 페이지. 이 페이지는 공통 헤더 및 페이지 레이아웃 구조를 제공합니다. 에 대 한 호출도 `Assets.GetScripts`, 페이지에서 호출 되, 자산 관리자 스크립트를 렌더링 하는 방법입니다.

샘플을 실행 하려면

1. 빈 웹 페이지 2 웹 사이트를 만듭니다. WebMatrix는 사용할 수 있습니다 **빈 사이트** 이 서식 파일입니다.
2. 라는 폴더를 만듭니다 *스크립트* 사이트에 있습니다.
3. 에 *스크립트* 폴더를 라는 파일을 만들어 *Test.js*, 복사는 *Test.js* 예제에서에 콘텐츠 파일을 저장...
4. 라는 폴더를 만듭니다 *앱\_코드* 사이트에 있습니다.
5. 에 *앱\_코드* 폴더를 라는 파일을 만들어 *Helpers.cshtml*, 예제 코드를 복사 하 고 명명 된 폴더에 저장 *앱\_코드*루트 폴더에 있습니다.
6. 사이트의 루트 폴더에는 파일을 만듭니다  *\_SiteLayout.cshtml,* 예를 복사 하 고 파일을 저장 합니다.
7. 사이트 루트에서 라는 파일을 만들어 *ContentPage.cshtml*, 예제 코드를 추가 하 고 저장 합니다.
8. 실행 *ContentPage* 브라우저에서 합니다. 에 전달 된 문자열의 `MakeNote` 도우미 boxed 참고로 렌더링 됩니다.
9. 주석 위로 마우스 포인터를 전달 합니다. 스크립트는 일시적으로 메모의 글꼴 크기를 늘립니다.
10. 렌더링된 된 페이지의 원본을 봅니다. 에 대 한 호출을 배치 하는 위치 때문에 `Assets.GetScripts`, 렌더링 된 `<script>` 호출 하는 태그 *Test.js* 페이지의 본문에 있는 매우 마지막 항목입니다.

*Test.js*

[!code-javascript[Main](top-features-in-web-pages-2/samples/sample8.js)]

*Helpers.cshtml*

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample9.cshtml)]

*\_SiteLayout.cshtml*

[!code-html[Main](top-features-in-web-pages-2/samples/sample10.html)]

*ContentPage.cshtml*

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample11.cshtml)]

다음 스크린 샷에 표시 *ContentPage.cshtml* 주석 위로 마우스 포인터를 놓을 때 브라우저에서:

[![topSeven-resmgr-1](top-features-in-web-pages-2/_static/image14.png)](top-features-in-web-pages-2/_static/image13.png)

<a id="oauthsetup"></a>
### <a name="enabling-logins-from-facebook-and-other-sites-using-oauth-and-openid"></a>Facebook 및 OAuth 및 OpenID를 사용 하 여 다른 사이트에서의 로그인을 사용 하도록 설정

웹 페이지 2는 멤버 자격 및 인증에 대 한 향상 된 옵션을 제공합니다. 주요 기능 향상은 새 않는다는 [OAuth](http://oauth.net/) 및 [OpenID](http://openid.net/) 공급자입니다. 이러한 공급자를 사용 하 여 사용자가 로그인 하도록 하 할 Facebook, Twitter, Windows Live, Google, Yahoo에서 기존 자격 증명을 사용 하 여 사이트에 있습니다. 예를 들어 Facebook 계정을 사용 하 여 로그인, 사용자가 선택 하기만 Facebook 아이콘을 사용자 정보를 입력할 있습니다 Facebook 로그인 페이지로 리디렉션합니다. 그런 다음 사이트에서 자신의 계정으로 Facebook 로그인을 연결할 수 있습니다. 웹 페이지 멤버 자격 기능에도 사용자가 여러 로그인 (소셜 네트워킹 사이트에서의 로그인 포함)를 연결할 수 웹 사이트에서 단일 계정을 사용 하 여 합니다.

이 이미지에서 로그인 페이지를 보여 줍니다.는 **시작 사이트** 사용자 외부 계정으로 로그인을 사용 하도록 설정 하려면 Facebook, Twitter, 또는 Windows Live 아이콘을 선택할 수 있는 템플릿:

[![topSeven-oauth-1](top-features-in-web-pages-2/_static/image16.png)](top-features-in-web-pages-2/_static/image15.png)

코드 몇 줄을 사용 하 여 OAuth 및 OpenID 멤버 자격을 사용할 수 있습니다. OAuth를 사용 하는 사용 하 여는 메서드 및 속성이 있으며 OpenID 공급자에서는 `WebMatrix.Security.OAuthWebSecurity` 클래스입니다.

그러나, 다른 사이트에서의 로그인을 사용 하도록 설정 하려면 코드를 사용 하는 대신 새 공급자와 함께 시작 하는 권장된 방법을 사용 하는 새 **시작 사이트** WebMatrix 2 베타와 함께 포함 되는 서식 파일입니다. **시작 사이트** 완전 한 구성원 인프라를 포함 하는 서식 파일, 로그인 페이지, 멤버 자격 데이터베이스 및 모든 코드와 함께 완료 해야 사용자가 로그인 로컬 자격 증명 또는 다른 사이트에서 사용 하 여 사이트에 .

#### <a name="how-to-enable-logins-using-the-oauth-and-openid-providers"></a>OAuth 및 OpenID 공급자를 사용 하 여 로그인을 활성화 하는 방법

이 섹션에서는 사용자가 외부 사이트 (Facebook, Twitter, Windows Live, Google 또는 Yahoo)에서 로그인을 사용 하는 방법의 예를 기반으로 하는 사이트에 제공 된 **시작 사이트** 서식 파일. 시작 사이트를 만든 후 (세부 정보 수행)를 수행 합니다.

- OAuth 공급자 (Facebook, Twitter, 및 Windows Live)를 사용 하는 사이트에 대해 외부 사이트에서 응용 프로그램을 만듭니다. 이렇게 하면 응용 프로그램 키를 해당 사이트에 대 한 로그인 기능을 호출 하기 위해 필요 합니다. OpenID 공급자 (Google, Yahoo)를 사용 하는 사이트, 응용 프로그램을 만들 필요가 없습니다. 모든 이러한 사이트에 로그인 하 고를 개발자 응용 프로그램을 만들 수 계정이 있어야 합니다. 

    > [!NOTE]
    > Windows Live 응용 프로그램 로그인을 테스트 하기 위한 로컬 웹 사이트 URL을 사용할 수 없습니다 작업 중인 웹 사이트에 대 한 라이브 URL만 허용 합니다.
- 사용 하려는 사이트에 대 한 로그인을 전송 하 고 적절 한 인증 공급자를 지정 하기 위해 웹 사이트의 몇 개의 파일을 편집 합니다.

**Google, Yahoo 로그인을 사용 하도록 설정 하려면**:

1. 웹 사이트에서 편집 된  *\_AppStart.cshtml* 페이지 Razor 코드 블록에 다음 두 줄의 코드에 대 한 호출 뒤에 추가 하 고는 `WebSecurity.InitializeDatabaseConnection` 메서드. 이 코드에는 Google과 Yahoo OpenID 공급자 수 있습니다. 

    [!code-css[Main](top-features-in-web-pages-2/samples/sample12.css)]
2. 에 *~/Account/Login.cshtml* 페이지에서 다음에서 주석을 제거 `<fieldset>` 블록 끝에서 페이지의 태그입니다. 코드에 주석 처리를 제거 하려면 제거의 `@*` 앞과 뒤에 있는 문자는 `<fieldset>` 블록입니다. 결과 코드 블록은 다음과 같습니다.

    [!code-html[Main](top-features-in-web-pages-2/samples/sample13.html)]
3. 추가 `<input>` 에 Google 또는 Yahoo 공급자에 대 한 요소는 `<fieldset>` 그룹에 *~/Account/Login.cshtml* 페이지. 업데이트 된 `<fieldset>` 그룹에 `<input>` Google, Yahoo 모두 검색에 대 한 요소에는 다음 예제와 같은: 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample14.html)]
4. 에 *~/Account/AssociateServiceAccount.cshtml* 페이지에서 추가 `<input>` Google 또는 Yahoo에 대 한 요소는 `<fieldset>` 파일의 끝 부분에서 그룹입니다. 동일한 복사할 수는 있지만 `<input>` 에 방금 추가한 요소는 `<fieldset>` 섹션는 *~/Account/Login.cshtml* 페이지. 

    *~/Account/AssociateServiceAccount.cshtml* 에 연결할 수 있음 다른 사이트에서 여러 로그인 웹 사이트에서 단일 계정을 사용 하 여 페이지를 만들려고 할 경우는 시작 사이트 템플릿의에서 페이지를 사용할 수 있습니다.

이제 Google, Yahoo 로그인을 테스트할 수 있습니다.

1. 실행의 *default.cshtml* 사이트의 페이지를 선택 하 고는 **로그인** 단추입니다.
2. 에 *로그인* 페이지는 **다른 서비스를 사용 하 여 로그인 할** 섹션 중 하나를 선택는 **Google** 또는 **Yahoo** 전송 단추입니다. 이 예제에서는 Google 로그인을 사용 합니다. 

    웹 페이지 요청을 Google 로그인 페이지로 리디렉션합니다.

    [![topSeven-oauth-6](top-features-in-web-pages-2/_static/image18.png)](top-features-in-web-pages-2/_static/image17.png)
3. 기존 Google 계정 자격 증명을 입력 합니다.
4. Google 요청 하면 계정에서 정보를 클릭 합니다. Localhost를 허용할 것인지 여부 **허용**합니다.

    코드는 사용자를 인증 하 고 Google 토큰을 사용 하 고 웹 사이트에이 페이지를 반환 합니다. 이 페이지에서는 사용자가 자신의 Google 로그인에 웹 사이트에서 기존 계정을 연결 또는 외부 로그인으로 연결 하려면 사이트에서 새 계정을 등록할 수 있습니다.

    [![topSeven-oauth-5](top-features-in-web-pages-2/_static/image20.png)](top-features-in-web-pages-2/_static/image19.png)
5. 선택 된 **연결** 단추입니다. 브라우저 응용 프로그램의 홈 페이지를 반환합니다.

    [![topSeven-oauth-3](top-features-in-web-pages-2/_static/image22.png)](top-features-in-web-pages-2/_static/image21.png)

    [![topSeven-oauth-3](top-features-in-web-pages-2/_static/image24.png)](top-features-in-web-pages-2/_static/image23.png)

**Facebook 로그인을 사용 하도록 설정 하려면**:

1. 이동 하 여 [Facebook 개발자 사이트](https://developers.facebook.com/apps) (로그인 아직 로그인 하는 경우).
2. 선택 된 **Create New App** 단추를 클릭 한 다음 지시에 따라 이름을 지정 하 고 새 응용 프로그램을 만듭니다.
3. 섹션에서 **앱은 Facebook과 통합 하는 방법을 선택**, 선택는 **웹 사이트** 섹션.
4. 입력은 **사이트 URL** 필드와 사이트의 URL (예를 들어 [ `http://www.example.com` ](http://www.example.com)). **도메인** 필드는 선택 사항 이지만 전체 도메인 인증을 제공 하는 데 사용할 수 있습니다 (예: *example.com*). 

    > [!NOTE]
    > 다음과 같은 URL 사용 하 여 로컬 컴퓨터에서 사이트를 실행 하는 경우 `http://localhost:12345` (여기서 번호는 로컬 포트 번호는)이이 값을 추가할 수 있습니다는 **사이트 URL** 사이트 테스트에 대 한 필드입니다. 그러나 언제 든 지 변경 내용을 로컬 사이트의 포트 번호를 업데이트 해야 합니다는 **사이트 URL** 응용 프로그램의 필드입니다.
5. 선택 된 **변경 내용 저장** 단추입니다.
6. 선택 된 **앱** 다시 탭 한 다음 응용 프로그램에 대 한 시작 페이지를 표시 합니다.
7. 복사는 **앱 ID** 및 **응용 프로그램 암호** 응용 프로그램에 대 한 값 임시 텍스트 파일에 붙여 넣습니다. Facebook 공급자에 코드를 웹 사이트에서 이러한 값을 전달 합니다.
8. Facebook 개발자 사이트를 종료 합니다.

이제 변경 하 두 페이지 웹 사이트에서의 사용자에 게 있도록 자신의 Facebook 계정을 사용 하는 사이트에 로그인 할 수 있습니다.

1. 웹 사이트에서 편집 된  *\_AppStart.cshtml* 페이지 및 Facebook OAuth 공급자에 대 한 코드 주석 처리를 제거 합니다. 주석 처리가 제거 코드 블록은 다음과 같습니다. 

    [!code-xml[Main](top-features-in-web-pages-2/samples/sample15.xml)]
2. 복사는 **앱 ID** 의 값으로 Facebook 응용 프로그램에서 값의 `consumerKey` (인용 부호 제외) 내 매개 변수입니다.
3. 복사 **응용 프로그램 암호** 으로 Facebook 응용 프로그램에서 값의 `consumerSecret` 매개 변수 값입니다.
4. 파일을 저장한 후 닫습니다.
5. 편집 된 *~/Account/Login.cshtml* 페이지에서 메모를 제거 하 고는 `<fieldset>` 블록 끝에서 페이지의 합니다. 코드에 주석 처리를 제거 하려면 제거의 `@*` 앞과 뒤에 있는 문자는 `<fieldset>` 블록입니다. 주석 사용 하 여 코드 블록 제거 하면 다음과 같이 표시 합니다. 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample16.html)]
6. 파일을 저장한 후 닫습니다.

이제 Facebook 로그인을 테스트할 수 있습니다.

1. 사이트의 실행 *default.cshtml* 페이지를 선택 하 고는 **로그인** 단추입니다.
2. 에 *로그인* 페이지는 **다른 서비스를 사용 하 여 로그인 할** 섹션에서 **Facebook** 아이콘입니다. 

    웹 페이지는 Facebook 로그인 페이지에 요청을 리디렉션합니다.

    [![topSeven-oauth-2](top-features-in-web-pages-2/_static/image26.png)](top-features-in-web-pages-2/_static/image25.png)
3. Facebook 계정에 로그인 합니다. 

    코드는 Facebook 토큰을 사용 하 여 사용자를 인증 하 고 페이지를 반환 합니다 사이트의 로그인을 사용 하 여 Facebook 로그인을 연결할 수 있습니다. 사용자 이름이 나 전자 메일 주소에 채워지는 **전자 메일** 폼에 필드입니다.

    [![topSeven-oauth-5](top-features-in-web-pages-2/_static/image28.png)](top-features-in-web-pages-2/_static/image27.png)
4. 선택 된 **연결** 단추입니다. 

    브라우저 홈 페이지로 돌아가고에 기록 됩니다.

    [![topSeven-oauth-3](top-features-in-web-pages-2/_static/image30.png)](top-features-in-web-pages-2/_static/image29.png)

**Twitter 로그인 사용 하도록 설정 하려면:** 

1. 찾아는 [Twitter 개발자 사이트](https://dev.twitter.com/)합니다.
2. 선택 된 **응용 프로그램을 만들** 에 연결 하 고 사이트에 로그인 합니다.
3. 에 **응용 프로그램을 만들** 양식에서 입력의 **이름** 및 **설명** 필드입니다.
4. 에 **웹 사이트** 필드 사이트의 URL을 입력 합니다 (예를 들어 [ `http://www.example.com` ](http://www.example.com)). 

    > [!NOTE]
    > 로컬 사이트를 테스트 하는 경우 (같은 URL을 사용 하 여 `http://localhost:12345`), Twitter URL을 허용 하지 않을 합니다. 그러나 로컬 루프백 IP 주소를 사용할 수 있습니다 (예를 들어 `http://127.0.0.1:12345`). 이 응용 프로그램을 로컬로 테스트 하는 과정이 간단해 집니다. 그러나 로컬 사이트의 포트 번호 변경 될 때마다 해야 업데이트는 **웹 사이트** 응용 프로그램의 필드입니다.
5. 에 **콜백 URL** 필드에, 사용자가 Twitter로 로그인 한 후에 반환 하는 웹 사이트의 페이지에 대 한 URL을 입력 합니다. 예를 들어 사용자 (로그인 상태를 인식 하)는 시작 사이트의 홈 페이지를 보내려면에 입력 된 동일한 URL을 입력에서 **웹 사이트** 필드입니다.
6. 조건에 동의 하 고 선택 된 **Twitter 응용 프로그램을 만드는** 단추입니다.
7. 에 **내 응용 프로그램** 방문 페이지를 만든 응용 프로그램을 선택 합니다.
8. 에 **세부 정보** 탭, 아래로 스크롤하여 선택한는 **내 액세스 토큰 만들기** 단추입니다.
9. 에 **세부 정보** 탭에서 복사 된 **소비자 키** 및 **소비자 암호** 응용 프로그램에 대 한 값 임시 텍스트 파일에 붙여 넣습니다. Twitter 공급자에 코드를 웹 사이트에서 이러한 값을 전달 합니다.
10. Twitter 사이트를 종료 합니다.

이제 변경 하면 두 페이지에 웹 사이트의 사용자가 Twitter 계정을 사용 하 여 사이트에 로그인 할 수 있도록 합니다.

1. 웹 사이트에서 편집 된  *\_AppStart.cshtml* 페이지 하 고 Twitter OAuth 공급자에 대 한 코드 주석 처리를 제거 합니다. 주석 처리가 제거 코드 블록은 다음과 같습니다. 

    [!code-csharp[Main](top-features-in-web-pages-2/samples/sample17.cs)]
2. 복사는 **소비자 키** 의 값으로 Twitter 응용 프로그램에서 값의 `consumerKey` (인용 부호 제외) 내 매개 변수입니다.
3. 복사는 **소비자 암호** 의 값으로 Twitter 응용 프로그램에서 값의 `consumerSecret` 매개 변수입니다.
4. 파일을 저장한 후 닫습니다.
5. 편집 된 *~/Account/Login.cshtml* 페이지에서 메모를 제거 하 고는 `<fieldset>` 블록 끝에서 페이지의 합니다. 코드에 주석 처리를 제거 하려면 제거의 `@*` 앞과 뒤에 있는 문자는 `<fieldset>` 블록입니다. 주석 사용 하 여 코드 블록 제거 하면 다음과 같이 표시 합니다. 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample18.html)]
6. 파일을 저장한 후 닫습니다.

이제 Twitter 로그인을 테스트할 수 있습니다.

1. 실행의 *default.cshtml* 사이트의 페이지를 선택 하 고는 **로그인** 단추입니다.
2. 에 *로그인* 페이지는 **다른 서비스를 사용 하 여 로그인 할** 섹션에서 **Twitter** 아이콘입니다. 

    웹 페이지 요청을 만든 응용 프로그램에 대 한 Twitter 로그인 페이지로 리디렉션합니다.

    [![topSeven-oauth-4](top-features-in-web-pages-2/_static/image32.png)](top-features-in-web-pages-2/_static/image31.png)
3. Twitter 계정에 로그인 합니다.
4. 코드는 Twitter 토큰을 사용 하 여 사용자를 인증 하 고 돌아갑니다 페이지에 연결할 수 있습니다 웹 사이트 계정으로 로그인 합니다. 사용자 이름 또는 전자 메일 주소에 채워지는 **전자 메일** 폼에 필드입니다.

    [![topSeven-oauth-5](top-features-in-web-pages-2/_static/image34.png)](top-features-in-web-pages-2/_static/image33.png)
5. 선택 된 **연결** 단추입니다. 

    브라우저 홈 페이지로 돌아가고에 기록 됩니다.

    [![topSeven-oauth-3](top-features-in-web-pages-2/_static/image36.png)](top-features-in-web-pages-2/_static/image35.png)

<a id="maphelper"></a>
### <a name="adding-maps-using-the-maps-helper"></a>지도 도우미를 사용 하 여 맵 추가

웹 페이지 2는 웹 페이지 사이트에 대 한 추가 기능 패키지는 ASP.NET Web Helpers Library에 대 한 추가 포함 됩니다. 다음 중 하나는에서 제공 하는 매핑 구성 요소는 `Microsoft.Web.Helpers.Maps` 클래스입니다. 사용할 수는 `Maps` 주소 또는 경도 및 위도 좌표 집합을 기반으로 하는 맵을 생성 하는 클래스입니다. `Maps` 클래스 Bing, Google, 지도 보기, Yahoo 등 널리 사용 되 지도 엔진으로 직접 호출할 수 있습니다.

새 사용 하려면 `Maps` 클래스에서 웹 사이트를 먼저 설치 해야 Web Helpers Library의 버전 2입니다. 이 작업을 수행 하려면 현재 정식된 버전의 설치를 위한 지침으로 이동 된 [ASP.NET Web Helpers Library](https://go.microsoft.com/fwlink/?LinkId=202889#webhelpers) 버전 2를 설치 합니다.

페이지에 매핑을 추가 하는 단계는 호출 지도 엔진에 관계 없이 동일 합니다. 매핑 페이지에 대 한 JavaScript 파일 참조를 추가 하 고 렌더링 하는 호출을 추가 합니다는 `<script>` 페이지에 태그를 삽입 합니다. 다음 매핑 페이지에서 사용 하려는 지도 엔진을 호출 합니다.

다음 예제에는 주소에 기반 하는 구조를 렌더링 하는 페이지 및 경도 및 위도 좌표에 따라 지도 렌더링 하는 다른 페이지를 만드는 방법을 보여 줍니다. Google 맵을 사용 하 여 주소 매핑 예제 및 좌표 매핑 예제에서는 Bing 지도 사용 합니다. 코드에서 다음과 같은 요소가 note:

- 에 대 한 호출 `Assets.AddScript` 두 매핑 페이지 맨 위에 있는 합니다. 에 대 한 참조를 추가 하는이 메서드는 *jquery 1.6.2.min.js* 에 포함 된 파일의 **시작 사이트** 서식 파일에 필요 하 고는 `Maps` 클래스입니다.
- 에 대 한 호출에서 `Assets.GetScripts` 레이아웃 파일에서 메서드. 이 메서드를 렌더링는 `<script>` 두 매핑 페이지에 태그를 지정 합니다.
- 에 대 한 호출에서 `@Maps.GetGoogleHtml` 및 `@Maps.GetBingHtml` 매핑 페이지의 메서드. 주소를 매핑하려면 주소 문자열을 전달 해야 합니다. 지도 좌표에 경도 및 위도 통과 해야 좌표입니다. Bing 지도 엔진에 대 한 전달 해야 키 (에서 등록 하 여 무료로 얻을 [Bing Maps 개발자 사이트](https://www.microsoft.com/maps/developers/web.aspx)). 비슷한 방법으로 다른 맵 엔진에 대 한 메서드는 작동 (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).

매핑 페이지를 만들려면:

1. 에 따라 웹 사이트 만들기는 **시작 사이트** 템플릿.
2. 라는 파일을 만들어 *MapAddress.cshtml* 사이트의 루트에 있습니다. 이 페이지는 지도를 전달 하는 주소에 따라 생성 됩니다.
3. 다음 코드를 파일에 복사 기존 내용을 덮어씁니다. 

    [!code-cshtml[Main](top-features-in-web-pages-2/samples/sample19.cshtml)]
4. 라는 파일을 만들어  *\_MapLayout.cshtml* 사이트의 루트에 있습니다. 이 페이지에는 두 개의 매핑 페이지에 대 한 레이아웃 페이지 수 있습니다.
5. 다음 코드를 파일에 복사 기존 내용을 덮어씁니다. 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample20.html)]
6. 라는 파일을 만들어 *MapCoordinates.cshtml* 사이트의 루트에 있습니다. 이 페이지는 지도를 전달 하는 좌표 집합에 따라 생성 됩니다.
7. 다음 코드를 파일에 복사 기존 내용을 덮어씁니다. 

    [!code-cshtml[Main](top-features-in-web-pages-2/samples/sample21.cshtml)]

매핑 페이지를 테스트:

1. 페이지 실행 *MapAddress.cshtml* 파일입니다.
2. 주소, 상태 또는 및 우편 번호를 포함 하 여 전체 주소 문자열을 입력 한 다음 선택에서 **Map It** 단추입니다. 페이지는 Google 지도에서 지도 렌더링합니다. 

    [![topseven-maphelper-1](top-features-in-web-pages-2/_static/image38.png)](top-features-in-web-pages-2/_static/image37.png)
3. 특정 위치에 대 한 위도 및 경도 좌표의 집합을 찾습니다.
4. 페이지 실행 *MapCoordinates.cshtml*합니다. 좌표를 입력 한 다음 선택에서 **Map It** 단추입니다. 페이지는 Bing 지도에서 지도 렌더링합니다. 

    [![topseven-maphelper-2](top-features-in-web-pages-2/_static/image40.png)](top-features-in-web-pages-2/_static/image39.png)

<a id="sidebyside"></a>
### <a name="running-web-pages-applications-side-by-side"></a>웹 페이지 응용 프로그램 Side-by-side 실행

웹 페이지 2 함께 응용 프로그램을 실행 하는 기능을 추가 합니다. 이렇게 하면 웹 페이지 1 응용 프로그램을 실행 하 고 새 웹 페이지 2 응용 프로그램을 빌드할 모두 동일한 컴퓨터에서 실행을 계속할 수 있습니다.

WebMatrix로 웹 페이지 2 베타를 설치할 때 고려해 야 할 몇 가지 사항 다음과 같습니다.

- 기본적으로 컴퓨터에 기존 웹 페이지 응용 프로그램 버전 2 응용 프로그램으로 실행 됩니다. (버전 2에 대 한 어셈블리 GAC에 설치 되 고 자동으로 사용 됩니다.)
- 웹 페이지 버전 1 (이전 시점에서와 같이 기본값) 대신 사용 하 여 사이트를 실행 하려는 경우에 작업을 수행 하는 사이트를 구성할 수 있습니다. 사이트에 지문이 아직 없으면는 *web.config* 사이트의 루트에서 파일을 새로 만들고 메서드를 다음과 같은 XML을 복사 기존 내용을 덮어씁니다. 사이트에 이미 포함 되어 있는 경우는 *web.config* 파일에서 추가 `<appSettings>` 에 다음과 같은 요소는 `<configuration>` 섹션.

    [!code-xml[Main](top-features-in-web-pages-2/samples/sample22.xml)]
  '-의 버전을 지정 하지 않으면는 *web.config* 파일을 사이트 버전 2 사이트도 배포 됩니다. (버전 2 어셈블리에 복사 되 고 *bin* 배포 된 사이트의 폴더입니다.)
- 사이트의 웹 페이지 버전 2 어셈블리를 포함 하는 2 베타 웹 매트릭스 버전에서 사이트 템플릿을 사용 하 여 만든 새 응용 프로그램 *bin* 폴더입니다.

버전은 사이트에 적절 한 어셈블리를 설치 하려면 NuGet을 사용 하 여 사이트와 함께 사용할 웹 페이지에 항상 제어할 수는 일반적으로 *bin* 폴더입니다. 패키지를 찾으려고 방문 [NuGet.org](http://NuGet.org)합니다.

<a id="mobile"></a>
### <a name="rendering-pages-for-mobile-devices"></a>모바일 장치에 대 한 페이지 렌더링

웹 페이지 2를 사용 하면 모바일 또는 다른 장치에 대 한 콘텐츠 렌더링 방식을 사용자 지정할 수 있습니다.

`System.Web.WebPages` 디스플레이 모드를 사용 하도록 하는 다음 클래스를 포함 하는 네임 스페이스: `DefaultDisplayMode`, `DisplayInfo`, 및 `DisplayModes`합니다. 이러한 클래스를 직접 사용할 수 있으며 특정 장치에 대 한 오른쪽 출력을 렌더링 하는 코드를 작성할 수 있습니다.

또는 다음과 같이 파일 명명 패턴을 사용 하 여 장치 관련 페이지를 만들 수 있습니다: <em>파일 이름.</em> <em>모바일</em><em>.cshtml</em>합니다. 예를 들어 이름이 하나는 페이지의 두 버전을 만들 수 있습니다 <em>MyFile.cshtml</em> 및 이름이 각각 <em>MyFile.Mobile.cshtml</em>합니다. 런타임 시 모바일 장치를 요청할 때 <em>MyFile.cshtml</em>, 웹 페이지에서 콘텐츠를 렌더링 <em>MyFile.Mobile.cshtml</em>합니다. 그렇지 않으면 <em>MyFile.cshtml</em> 렌더링 됩니다.

다음 예제에서는 모바일 장치에 대 한 콘텐츠 페이지를 추가 하 여 모바일 렌더링을 활성화 하는 방법을 보여 줍니다. *Page1.cshtml* 콘텐츠 및 탐색 세로 막대를 포함 합니다. *Page1.Mobile.cshtml* 동일한 콘텐츠를 포함 하지만 세로 막대를 생략 합니다.

작성 하 고 실행 코드 샘플:

1. 웹 페이지 사이트에서는 라는 파일을 만들어 *Page1.cshtml* 복사는 *Page1.cshtml* 예제에서 콘텐츠를 합니다.
2. 라는 파일을 만들어 *Page1.Mobile.cshtml* 복사는 *Page1.Mobile.cshtml* 예제의 콘텐츠입니다. 확인 페이지의 모바일 버전이 더 작은 화면에 보다 나은 렌더링에 대 한 탐색 절을 생략 합니다.
3. 데스크톱 브라우저를 실행 하 고 *Page1.cshtml*합니다.
4. 모바일 브라우저 (또는 모바일 장치 에뮬레이터)를 실행 하 고 *Page1.cshtml*합니다. 이 현재 웹 페이지 렌더링 하는 페이지의 모바일 버전을 확인 합니다. 

    > [!NOTE]
    > 모바일 페이지를 테스트 하려면 데스크톱 컴퓨터에서 실행 되는 모바일 장치 시뮬레이터에서 앱을 사용할 수 있습니다. 이 도구를 사용 하면 모바일 장치에서 유사할 것 처럼 웹 페이지를 테스트할 수 있습니다 (즉, 일반적으로 훨씬 더 작은와 표시 영역). 시뮬레이터에서 앱의 한 가지 예는 [사용자 에이전트 전환기 추가 기능](http://addons.mozilla.org/en-us/firefox/addon/user-agent-switcher/) Mozilla Firefox에 대 한 수 있는 데스크톱 버전의 Firefox에서 다양 한 모바일 브라우저 에뮬레이션 합니다.

*Page1.cshtml*

[!code-html[Main](top-features-in-web-pages-2/samples/sample23.html)]

*Page1.Mobile.cshtml*

[!code-html[Main](top-features-in-web-pages-2/samples/sample24.html)]

*Page1.cshtml* 데스크톱 브라우저에 렌더링 합니다.

[![topseven-displaymodes-1](top-features-in-web-pages-2/_static/image42.png)](top-features-in-web-pages-2/_static/image41.png)

*Page1.Mobile.cshtml* Firefox 브라우저에 Apple iPhone 시뮬레이터 보기에 표시 합니다. 요청 하는 것도 *Page1.cshtml*, 응용 프로그램 렌더링 *Page1.Mobile.cshtml*합니다.

[![topseven-displaymodes-2](top-features-in-web-pages-2/_static/image44.png)](top-features-in-web-pages-2/_static/image43.png)

<a id="resources"></a>
## <a name="additional-resources"></a>추가 자료

### <a name="aspnet-web-pages-1-resources"></a>ASP.NET 웹 페이지 1 리소스

> [!NOTE]
> 대부분의 웹 페이지 1 프로그래밍 및 API 리소스 웹 페이지 2에 계속 적용 합니다.

- [ASP.NET 웹 페이지 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkId=202890)

### <a name="webmatrix-resources"></a>WebMatrix 리소스

- [WebMatrix 2는 새로운 기능](http://webmatrix.com/next)
- [Microsoft WebMatrix Site](https://go.microsoft.com/fwlink/?LinkID=195076)
- [Microsoft WebMatrix로 웹 개발 시작](https://msdn.microsoft.com/en-us/library/hh145669(v=VS.99).aspx)(전체 길이 샘플 웹 페이지 응용 프로그램 포함)
