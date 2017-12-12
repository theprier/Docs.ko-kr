---
uid: whitepapers/mvc4-release-notes
title: ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: "이 문서는 ASP.NET MVC 4의 릴리스에 대해 설명합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/09/2011
ms.topic: article
ms.assetid: f014524f-25c0-4094-b8e1-886d99536f00
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /whitepapers/mvc4-release-notes
msc.type: content
ms.openlocfilehash: fb9d2eaa83fe7486279815c21aec204bdfdf122d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-mvc-4"></a>ASP.NET MVC 4
====================
> 이 문서는 ASP.NET MVC 4의 릴리스에 대해 설명합니다.


- [설치 참고 사항](#_Toc303253802)
- [문서](#_Toc303253803)
- [지원](#_Toc303253804)
- [소프트웨어 요구 사항](#_Toc303253805)
- [ASP.NET MVC 4의에서 새로운 기능](#_Toc303253807)

    - [ASP.NET Web API](#_Toc317096197)
    - [기본 프로젝트 템플릿의 향상 된 기능](#_Toc303253808)
    - [모바일 프로젝트 템플릿](#_Toc303253809)
    - [디스플레이 모드](#_Toc303253810)
    - [jQuery Mobile 뷰 전환기와 브라우저 재정의](#_Toc303253811)
    - [비동기 컨트롤러에 대 한 작업 지원](#_Toc303253813)
    - [Azure SDK](#_Toc303253814)
    - [데이터베이스 마이그레이션](#_Toc303253818)
    - [빈 프로젝트 템플릿](#_Toc303253819)
    - [모든 프로젝트 폴더에 컨트롤러 추가](#_Toc303253820)
    - [묶음 및 축소](#_Toc303253821)
    - [Facebook 및 OAuth 및 OpenID를 사용 하 여 다른 사이트에서의 로그인을 사용 하도록 설정](#_Toc303253822)
- [ASP.NET MVC 3 프로젝트를 ASP.NET MVC 4로 업그레이드](#_Toc303253806)
- [ASP.NET MVC 4 릴리스 후보에서 변경 내용](#_Toc303253817)
- [알려진된 문제 및 주요 변경 내용](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>설치 참고 사항

Visual Studio 2010 용 ASP.NET MVC 4에서 설치할 수 있습니다는 [ASP.NET MVC 4 홈 페이지](../mvc/mvc4.md) 웹 플랫폼 설치 관리자를 사용 하 여 합니다.

ASP.NET MVC 4를 설치 하기 전에 ASP.NET MVC 4의 모든 이전에 설치 된 미리 보기를 제거 하는 것이 좋습니다. ASP.NET MVC 4를 제거 하지 않고 ASP.NET MVC 4 베타 및 릴리스 후보를 업그레이드할 수 있습니다.

이 릴리스는.NET Framework 4.5의 미리 보기 버전을 모두와 호환 되지 않습니다. 개별적으로 ASP.NET MVC 4를 설치 하기 전에 최신 버전을.NET Framework 4.5의 모든 설치 된 미리 보기 버전을 업그레이드 해야 합니다.

ASP.NET MVC 4 설치 및 실행--와 함께 ASP.NET MVC 3을 수 있습니다.

<a id="_Toc303253803"></a>
## <a name="documentation"></a>설명서

ASP.NET MVC에 대 한 설명서는 다음 URL의 MSDN 웹 사이트에서 사용할 수 있습니다.

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

ASP.NET 웹 사이트의 MVC 4 페이지에서 사용할 수 있는 자습서 및 ASP.NET MVC에 대 한 기타 정보 ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)).

<a id="_Toc303253804"></a>
## <a name="support"></a>지원

ASP.NET MVC 4는 완전히 지원 됩니다. 이 릴리스에서 사용에 대 한 문의 사항이 있으면 게시할 수도 있습니다에 ASP.NET MVC 포럼 ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx))에서 ASP.NET 커뮤니티의 회원과 비공식적인 지원을 제공할 수 있는 경우가 많습니다.

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

Visual Studio에 대 한 ASP.NET MVC 4 구성 요소에는 PowerShell 2.0 및 Visual Studio 2010 서비스 팩 1 또는 Visual Web Developer Express 2010 서비스 팩 1에 필요 합니다.

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4"></a>ASP.NET MVC 4의에서 새로운 기능

이 섹션에 도입 된 기능에 설명 ASP.NET MVC 4 릴리스에서 합니다.

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET MVC 4는 새로운 프레임 워크 다양 한 브라우저 및 모바일 장치를 포함 하 여 클라이언트를 연결할 수 있는 HTTP 서비스를 만들기 위한 ASP.NET Web API를 포함 합니다. ASP.NET Web API는 RESTful 서비스를 구축 하기 위한 이상적인 플랫폼입니다.

ASP.NET Web API에는 다음과 같은 기능에 대 한 지원이 포함 됩니다.

- **최신 HTTP 프로그래밍 모델:** 직접 액세스 하 고 새, 강력한 형식의 HTTP 개체 모델을 사용 하 여 Web Api의 HTTP 요청 및 응답을 처리 합니다. 동일한 프로그래밍 모델 및 HTTP 파이프라인 대칭적으로 클라이언트를 사용할 수는 새로운 *HttpClient* 유형입니다.
- **전체 경로 대 한 지원:** ASP.NET Web API의 ASP.NET 라우팅 경로 매개 변수 및 제약 조건을 포함 경로 기능의 전체 집합을 지원 합니다. 또한 작업 HTTP 메서드 매핑할 간단한 규칙을 사용 하십시오.
- **콘텐츠 협상:** 클라이언트와 서버를 함께 사용 web API에서에서 반환 되는 데이터에 대 한 올바른 형식을 결정 합니다. ASP.NET Web API는 XML, JSON, 기본 지원 및 양식 URL로 인코딩된 형식 및 있습니다 직접 포맷터를 추가 하 여이 지원을 확장할 수 또는 기본 콘텐츠 협상 전략을 바꿀 수도 합니다.
- **모델 바인딩 및 유효성 검사:** 모델 바인더를 쉽게 HTTP 요청의 다양 한 부분에서 데이터를 추출 하 고 이러한 메시지 파트 웹 API 작업에 의해 사용할 수 있는.NET 개체로 변환할 수 있는 방법을 제공 합니다. 액션 매개 변수를 기반으로 데이터 주석 유효성 검사도 수행 됩니다.
- **필터:** ASP.NET Web API와 같은 잘 알려진 필터를 포함 하는 필터를 지 원하는 *[Authorize]* 특성입니다. 제작 하 고 작업, 권한 부여 및 예외 처리에 대 한 필터를 직접 연결할 수 있습니다.
- **쿼리 컴퍼지션:** 사용은 *[Queryable]* 반환 하는 동작에 대 한 필터 특성 *IQueryable* web API OData 쿼리 규칙을 통해 쿼리를 위한 지원을 사용 하도록 설정 합니다.
- **테스트 용이성 향상:** 정적 컨텍스트 개체에서 HTTP 정보를 설정 하는 대신 웹 API 작업 작업의 인스턴스와 *HttpRequestMessage* 및 *HttpResponseMessage*합니다. 웹 API 기능에 대 한 단위 테스트를 신속 하 게 작성을 시작 하려면 웹 API 프로젝트와 함께 단위 테스트 프로젝트를 만듭니다.
- **코드 기반 구성:** 파일 정리 config를 그대로 두고, ASP.NET Web API 구성을 전적으로 코드를 통해 수행 됩니다. 확장성 지점을 구성 하려면 제공 된 서비스 로케이터 패턴을 사용 합니다.
- **Inversion of Control (IoC) 컨테이너에 대 한 지원 향상:** 향상 된 종속성 확인자 추상화를 통해 IoC 컨테이너에 대 한 뛰어난 지원 기능을 제공 하는 ASP.NET Web API
- **자체 호스팅:** 경로의 모든 기능 및 Web API의 기타 기능을 계속 사용 하면서 IIS 외에도 사용자가 소유한 프로세스에서 Web Api를 호스팅할 수 있습니다.
- **사용자 지정 도움말을 만들고 테스트 페이지:** 이제 쉽게 사용자 지정 도움말을 작성 하 고 테스트할 수 페이지 웹 Api에 대 한 새 사용 하 여 *IApiExplorer* 웹 Api에 대 한 전체 런타임 설명을 가져오기 위해 서비스에 있습니다.
- **모니터링 및 진단:** ASP.NET Web API 이제 System.Diagnostics, ETW 및 제 3 자 로깅 프레임 워크와 같은 기존 로깅 솔루션와 쉽게 통합할 수 있도록 하는 경량 추적 인프라를 제공 합니다. 제공 하 여 추적을 설정할 수 있습니다는 *ITraceWriter* 구현 및 web API 구성에 추가 합니다.
- **링크 생성:** ASP.NET Web API를 사용 하 여 *UrlHelper* 동일한 응용 프로그램에서 관련된 리소스에 대 한 링크를 생성 하 합니다.
- **웹 API 프로젝트 템플릿을:** 선택 새 웹 API 프로젝트에서 새 MVC 4 프로젝트 마법사를 신속 하 게 시작 하 고 실행할 ASP.NET Web API를 선택 합니다.
- **스 캐 폴딩:** 사용은 **컨트롤러 추가** 신속 하 게 Entity Framework를 기반으로 하는 web API 컨트롤러를 스 캐 폴드 하려면 대화 상자에 모델 형식을 기반으로 합니다.

ASP.NET Web API에 대 한 자세한 내용은 링크 참조 [https://www.asp.net/web-api](../web-api/index.md)합니다.

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>기본 프로젝트 템플릿의 향상 된 기능

최신 수준의 웹 사이트를 만들려면 새 ASP.NET MVC 4 프로젝트를 만드는 사용 되는 템플릿을 업데이트 되었습니다.

![](mvc4-release-notes/_static/image1.png)

형식적 향상 된 기능 외에도 새 서식 파일의 기능을 향상 되었습니다. 서식 파일에서는 보기에 좋고 데스크톱 브라우저의 경우와 사용자 지정 하지 않고 모바일 브라우저에서 자동 선택 렌더링 기술을 사용 합니다.

![](mvc4-release-notes/_static/image2.png)

실행에서 자동 선택 렌더링을 보려면 모바일 에뮬레이터에서 앱을 사용할 수도 있고 작게 데스크톱 브라우저 창 크기를 조정 하면 키를 누릅니다. 브라우저 창 만큼 작지 않아서 가져오면 페이지의 레이아웃이 변경 됩니다.

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>모바일 프로젝트 템플릿

새 프로젝트를 시작 하 고 mobile에 대 한 사이트 및 태블릿에서 브라우저를 만들려고 할 경우에 새 모바일 응용 프로그램 프로젝트 템플릿을 사용할 수 있습니다. 이 필드는 jQuery Mobile, 터치에 최적화 된 UI 구축에 대 한 오픈 소스 라이브러리를 기반으로 계산입니다.

![](mvc4-release-notes/_static/image3.png)

이 서식 파일에는 인터넷 응용 프로그램 템플릿 동일한 응용 프로그램 구조 (및 컨트롤러 코드는 사실상 동일) 이지만 jQuery Mobile을 사용 하 여 제대로 표시 되 고 터치 기반 모바일 장치에서 제대로 동작 하도록 스타일이 지정 합니다. 모바일 UI 스타일 지정 및 구성 하는 방법에 대 한 자세한 내용은 참조는 [jQuery 모바일 프로젝트 웹 사이트](http://jquerymobile.com/)합니다.

데스크톱 지향 사이트, 모바일에 최적화 된 뷰를 추가 하려면 또는 데스크톱 및 모바일 브라우저에 다른 스타일된 보기 역할 하는 단일 사이트를 만들려고 할 경우 이미 있는 경우에 디스플레이 모드에서 새로운 기능을 사용할 수 있습니다. (다음 섹션 참조).

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>디스플레이 모드

새 디스플레이 모드 기능을 사용 하는 응용 프로그램은 요청을 수행 하는 브라우저에 따라 보기를 선택 합니다. 예를 들어 데스크톱 브라우저 홈 페이지를 요청 하는 경우 응용 프로그램 Views\Home\Index.cshtml 템플릿을 사용 될 수 있습니다. 모바일 브라우저 홈 페이지를 요청 하는 경우 응용 프로그램 Views\Home\Index.mobile.cshtml 서식 파일을 반환할 수 있습니다.

특정 브라우저 종류에 대 한 레이아웃 및 부분을 재정의할 수도 있습니다. 예:

- Views\Shared 폴더 모두에 포함 된 경우는 \_Layout.cshtml 및 \_Layout.mobile.cshtml 템플릿, 응용 프로그램 사용은 기본적으로 \_모바일 브라우저와 의요청을하는동안Layout.mobile.cshtml\_다른 요청 하는 동안 Layout.cshtml 합니다.
- 둘 다 포함 된 폴더 \_MyPartial.cshtml 및 \_MyPartial.mobile.cshtml, 명령 @Html.Partial("\_MyPartial")은 렌더링 \_MyPartial.mobile.cshtml 모바일에서 요청 하는 동안 브라우저 및 \_다른 요청 하는 동안 MyPartial.cshtml 합니다.

보다 구체적인 뷰, 레이아웃, 또는 다른 장치에 대 한 부분 뷰를 만들려는 경우 새 등록할 수 *DefaultDisplayMode* 인스턴스 요청을 특정 조건을 충족 하는 경우 검색할 수 있는 이름을 지정할 수 있습니다. 예를 들어 다음 코드를 추가할 수 있습니다는 *응용 프로그램\_시작* 메서드 문자열 "iPhone" Apple iPhone 브라우저 요청할 때 적용 되는 디스플레이 모드로 등록 하려면 Global.asax 파일에:

[!code-csharp[Main](mvc4-release-notes/samples/sample1.cs)]

이 코드를 실행 한 후 Apple iPhone 브라우저 요청을 수행 하는 경우, 응용 프로그램의 Views\Shared를 사용 합니다\\_Layout.iPhone.cshtml 레이아웃 (있는 경우). 디스플레이 모드에 대 한 자세한 내용은 참조 하십시오. [ASP.NET MVC 4 모바일 기능](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md)합니다. DisplayModeProvider를 사용 하 여 응용 프로그램을 설치 해야는 [고정 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet 패키지 합니다. [ASP.NET Fall 2012 업데이트](https://go.microsoft.com/fwlink/?LinkID=271322) 포함는 [고정 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet 패키지에 새 프로젝트 템플릿이 있습니다. 참조 [ASP.NET MVC 4 모바일 캐싱 버그 Fixedd](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 수정 프로그램에 대 한 자세한 내용은 합니다.

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-and-mobile-features"></a>jQuery Mobile 및 모바일 기능

자습서를 참조 jQuery Mobile을 사용 하 여 ASP.NET MVC 4 모바일 응용 프로그램에 대 한 내용은 [ASP.NET MVC 4 모바일 기능](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md)합니다.

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>비동기 컨트롤러에 대 한 작업 지원

작성할 수 있습니다 비동기 작업 메서드 형식의 개체를 반환 하는 단일 메서드 *작업* 또는 *작업&lt;ActionResult&gt;*합니다.

 자세한 내용은 참조 [ASP.NET MVC 4의 비동기 메서드를 사용 하 여](../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)합니다.

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4의 Windows Azure SDK 1.6 이상 버전을 지원합니다.

<a id="_Toc303253818"></a>
### <a name="database-migrations"></a>데이터베이스 마이그레이션

ASP.NET MVC 4 프로젝트는 이제 Entity Framework 5를 포함 합니다. 데이터베이스 마이그레이션에 대 한 지원은 Entity Framework 5의 유용한 기능 중 하나입니다. 이 기능을 사용 하면 쉽게 데이터베이스의 데이터를 유지 하는 동안 코드 중심 마이그레이션을 사용 하 여 데이터베이스 스키마를 개발할 수 있습니다. 데이터베이스 마이그레이션에 대 한 자세한 내용은 참조 하십시오. [영화 모델 및 테이블에 새 필드 추가](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table.md) 에 [ASP.NET MVC 4 자습서](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)합니다.

<a id="_Toc303253819"></a>
### <a name="empty-project-template"></a>빈 프로젝트 템플릿

빈 MVC 프로젝트 템플릿을 비어 이제 실제로 완전히 백지에서 시작할 수 있도록 합니다. 빈 프로젝트 템플릿의 이전 버전에서 기본 이름이 변경 되었습니다.

<a id="_Toc303253820"></a>
### <a name="add-controller-to-any-project-folder"></a>모든 프로젝트 폴더에 컨트롤러 추가

이제 마우스 오른쪽 단추로 클릭 하 고 선택할 수 있습니다 **컨트롤러 추가** MVC 프로젝트의 모든 폴더에서 합니다. 이 MVC 및 Web API 컨트롤러에 별도 폴더에 유지 하는 포함 하 여 원하는 컨트롤러를 구성 하기 더 많은 유연성을 제공 합니다.

<a id="_Toc303253821"></a>
### <a name="bundling-and-minification"></a>묶음 및 축소

묶음 및 축소 프레임 워크를 사용 하면 웹 페이지에서 개별 파일을 번들로 묶은 단일 파일 스크립트 및 CSS에 결합 하 여 확인 해야 하는 HTTP 요청 수를 줄일 수 있습니다. 그런 다음 이러한 요청의 전체 크기 번들의 내용을 축소 하 여 줄일 수 있습니다. 축소 단축 하는 해당 의미에 따라 CSS 선택기도 축소 변수 이름에 공백 제거 같은 작업을 포함할 수 있습니다. 번들 선언 되 고에서 구성 되며 코드 쉽게 뷰 중 하나를 생성할 수 있는 도우미 메서드를 통해 번들에 대 한 단일 링크 또는 참조, 디버깅, 여러 개별 번들의 내용에 연결 합니다. 자세한 내용은 참조 [묶음 및 축소](../mvc/overview/performance/bundling-and-minification.md)합니다.

<a id="_Toc303253822"></a>
### <a name="enabling-logins-from-facebook-and-other-sites-using-oauth-and-openid"></a>Facebook 및 OAuth 및 OpenID를 사용 하 여 다른 사이트에서의 로그인을 사용 하도록 설정

ASP.NET MVC 4 인터넷 프로젝트 템플릿의 기본 템플릿 DotNetOpenAuth 라이브러리를 사용 하 여 OAuth 및 OpenID 로그인에 대 한 지원이 포함 됩니다. OAuth 또는 OpenID 공급자 구성에 대 한 참조 [WebForms, MVC 및 웹 페이지에 대 한 OAuth/OpenID 지원](https://blogs.msdn.com/b/webdev/archive/2012/08/15/oauth-openid-support-for-webforms-mvc-and-webpages.aspx) 및 [OAuth 및 OpenID 기능 설명서 ASP.NET 웹 페이지에서](../web-pages/overview/releases/top-features-in-web-pages-2.md#oauthsetup)합니다.

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>ASP.NET MVC 3 프로젝트를 ASP.NET MVC 4로 업그레이드

ASP.NET MVC 4를 ASP.NET MVC 4 ASP.NET MVC 3 응용 프로그램을 업그레이드 하는 시기 선택에 유연성을 제공 하 여 동일한 컴퓨터에 ASP.NET MVC 3 나란히 설치할 수 있습니다.

업그레이드 하는 가장 간단한 방법은 새 ASP.NET MVC 4 프로젝트와 복사본을 만드는 모든 뷰, 컨트롤러, 코드 및 콘텐츠 파일에서 기존 MVC 3 프로젝트 새 프로젝트를 선택한 다음 어셈블리를 업데이트 아닌 MVC 템플릿에 일치 하도록 새 프로젝트에서 참조는 cluded 어셈블리를 사용 하는 합니다. MVC 3 프로젝트의 Web.config 파일을 변경한도 MVC 4 프로젝트에서 Web.config 파일에 이러한 변경 내용을 병합 해야 합니다.

기존 ASP.NET MVC 3 응용 프로그램 버전 4 수동으로 업그레이드 하려면 다음을 수행 합니다.

1. (에 프로젝트, Views 폴더와 프로젝트의 각 영역에 대 한 뷰 폴더에 각각 하나씩의 루트에 각각 하나씩) 프로젝트의에서 파일에 모든 Web.config에서 다음 텍스트의 모든 인스턴스를 바꿉니다 (참고: System.Web.WebPages, Version = 1.0.0.0를 찾을 수 없습니다 프로젝트의 경우 Visual Studio 2012를 사용 하 여 만든): 

    [!code-console[Main](mvc4-release-notes/samples/sample2.cmd)]

    해당 텍스트:

    [!code-console[Main](mvc4-release-notes/samples/sample3.cmd)]
2. 루트 Web.config 파일에서 업데이트는 *webPages:Version* "2.0.0.0"으로 요소를 새로 추가 *PreserveLoginUrl* "true" 값이 있는 키: 

    [!code-xml[Main](mvc4-release-notes/samples/sample4.xml)]
3. 솔루션 탐색기에서 참조를 마우스 오른쪽 단추로 클릭 하 고 NuGet 패키지 관리를 선택 합니다. 왼쪽된 창에서 선택 **Online\NuGet 공식 패키지 소스**, 다음을 업데이트 합니다.

    - ASP.NET MVC 4
    - (선택 사항) jQuery, jQuery 유효성 검사 및 jQuery UI
    - (선택 사항) Entity Framework
    - (Optonal) Modernizr
4. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 프로젝트 언로드를 선택 합니다. 그런 다음 이름을 다시 마우스 오른쪽 단추로 클릭 하 고 편집 선택 *ProjectName*.csproj 합니다.
5. 찾을 *ProjectTypeGuids* 요소 및 {E53F8FEA-EAE0-44A6-8774-FFD645390401} {E3E379DF-F4C6-4180-9B81-6769533ABE47}으로 대체 합니다.
6. 변경 내용을 저장, 편집 하 고 프로젝트 (.csproj) 파일을 닫습니다 하, 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 프로젝트 다시 로드를 선택 합니다.
7. 이전 버전의 ASP.NET MVC를 사용 하 여 컴파일되는 모든 타사 라이브러리를 프로젝트에서 참조 하는 경우 루트 Web.config 파일을 열고 다음 세 개의 추가 *bindingRedirect* 아래에는  *구성* 섹션: 

    [!code-xml[Main](mvc4-release-notes/samples/sample5.xml)]

<a id="_Toc303253817"></a>
## <a name="changes-from-aspnet-mvc-4-release-candidate"></a>ASP.NET MVC 4 릴리스 후보에서 변경 내용

ASP.NET MVC 4 릴리스 후보 릴리스 정보는 여기에서 확인할 수 있습니다.

이 릴리스의 ASP.NET MVC 4 릴리스 후보에서 주요 변경 내용 아래에 요약 되어 있습니다.

- **컨트롤러 구성 당:** ASP.NET Web API 컨트롤러를 구현 하는 사용자 지정 특성 발생 될 수 있는 *IControllerConfiguration* 자신의 포맷터, 작업 선택기 및 매개 변수 바인더를 설정 하려면 . *HttpControllerConfigurationAttribute* 제거 되었습니다.
- **경로의 메시지 처리기 당:** 지정된 된 경로 대 한 요청 체인에서 마지막 메시지 처리기를 지정할 수 있습니다. 이 통해 자신 들에 게 발송할 라우팅을 사용 하려면 안에서 따라 프레임에 대 한 지원 (비-*IHttpController*) 끝점입니다.
- **진행률 알림을:** 는 *ProgressMessageHandler* 업로드 되 고 요청 엔터티 및 다운로드할 응답 엔터티 둘 다에 대 한 진행률 알림을 생성 합니다. 이 처리기를 사용 하 여 있기 요청 본문을 업로드 또는 다운로드 하는 응답 본문 떨어져 있는 정도 추적할 수 있습니다.
- **콘텐츠 푸시:** 는 *PushStreamContent* 클래스 하려는 시나리오에서 데이터 공급자는 요청 또는 응답 (동기 또는 비동기)는 스트림을 사용 하 여에 직접 쓸 수 있도록 합니다. 경우는 *PushStreamContent* 출력 스트림 사용 하 여 action 대리자를 호출 하는 데이터를 받아들일 준비가 되었습니다. 스트림에 쓸 때 완료 하는 동안 필요한와 종가 대 한 개발자 스트림에 쓸 다음 수 있습니다. *PushStreamContent* 스트림의 닫는 검색 하 고 내부 비동기 완료 *작업* 콘텐츠 작성 하기 위한 합니다.
- **오류 응답을 만드는:** 사용은 *HttpError* 일관 되 게 오류 정보에서 유효성 검사 오류 및 예외와 같은 여전히 적용 하면서를 나타내는 형식을 *IncludeErrorDetailPolicy* . 새로운 *CreateErrorResponse* 확장 메서드를 쉽게와 오류 응답을 만들 *HttpError* 콘텐츠로 합니다. *HttpError* 콘텐츠 완벽 하 게 콘텐츠를 협상 합니다.
- **제거 MediaRangeMapping:** 미디어 형식 범위는 이제 기본 콘텐츠 협상 자에 의해 처리 됩니다.
- **단순 형식 매개 변수에 대 한 기본 매개 변수 바인딩에 이제 [FromUri]:** 모델 바인딩을 사용 하는 단순 형식 매개 변수가 기본 매개 변수 바인딩에 ASP.NET Web API의 이전 릴리스에서 합니다. 단순 형식 매개 변수에 대 한 기본 매개 변수 바인딩에 이제 *[FromUri]*합니다.
- **작업 선택에 필요한 매개 변수가 인식:** ASP.NET Web API에서 작업 선택은 이제 경우에 선택 동작 URI에서 제공 하는 모든 필수 매개 변수가 제공 됩니다. 동작 메서드 시그니처의 인수에 대 한 기본값을 제공 하 여 매개 변수를 선택적으로 지정할 수 있습니다.
- **HTTP 매개 변수 바인딩 사용자 지정:** 사용는 *ParameterBindingAttribute* 사용 또는 특정 작업 매개 변수에 대 한 매개 변수 바인딩을 사용자 지정할 수는 *ParameterBindingRules* 에 *HttpConfiguration* 매개 변수 바인딩에 사용자 지정 하려면 보다 광범위 하 게 합니다.
- **MediaTypeFormatter 개선:** 포맷터 액세스는 완전 하 게 *HttpContent* 인스턴스.
- **호스트 정책 선택 버퍼링:** 구현 및 구성의 *IHostBufferPolicySelector* 서비스 호스트는 데 사용할 때 버퍼링에 대 한 정책을 확인 하기 위해 사용할 수 있도록 ASP.NET Web API에 있습니다.
- **클라이언트 인증서는 호스트 알 수 없는 방식으로 액세스:** 사용은 *GetClientCertificate* 요청 메시지에서 제공 된 클라이언트 인증서를 가져올 확장 메서드를 합니다.
- **콘텐츠 협상 확장성:** 에서 파생 하 여 콘텐츠 협상을 사용자 지정의 *DefaultContentNegotiator* 원하는 콘텐츠 협상의 모든 요소를 재정의 합니다.
- **승인 금지 406 응답을 반환 하는 것에 대 한 지원:** 돌아올 수 승인 금지 406 응답 ASP.NET Web API에서 만들어 적합 한 포맷터를 찾을 수는 *DefaultContentNegotiator* 는 와*excludeMatchOnTypeOnly* 매개 변수 설정 *true*합니다.
- **양식 데이터 JToken 또는 NameValueCollection 읽기:** URI 쿼리 문자열에 또는으로 요청 본문에 양식 데이터를 읽을 수는 *NameValueCollection* 를 사용 하는 *ParseQueryString* 및  *ReadAsFormDataAsync* 확장 메서드 각각. 마찬가지로, URI 쿼리 문자열에 또는으로 요청 본문에 양식 데이터를 읽을 수 있습니다는 *JToken* 를 사용 하는 *TryReadQueryAsJson* 및 *ReadAsAsync*&lt;T&gt; 확장 메서드 각각.
- **다중 파트 기능 향상:** 쓸 수는 *MultipartStreamProvider* 완전히 MIME 다중 파트 데이터를 읽고 수를 최적의 방법 사용자에 게 표시 되는 결과의 형식에 맞게 조정 합니다. 선택할 수도 있습니다는 후 처리 단계에는 *MultipartStreamProvider* 어떤 후 MIME 다중 파트 본문 부분에 려를 처리 하는 구현을 수 있도록 합니다. 예를 들어는 *MultipartFormDataStreamProvider* 구현 읽고 HTML 폼 데이터 부분에 추가 합니다.는 *NameValueCollection* 쉽게 호출자에서에 가져올 수 있도록 합니다.
- **연결 생성 기능 향상:** 는 *UrlHelper* 더 이상 의존 *HttpControllerContext*합니다. 이제 액세스할 수 있습니다는 *UrlHelper* 어떤 컨텍스트에서 여기서는 *HttpRequestMessage* ´ ï ´ 합니다.
- **메시지 처리기 실행 순서 변경:** 메시지 처리기가 이제 대신 반대 순서로 구성 된 순서로 실행 됩니다.
- **메시지 처리기를 연결에 대 한 도우미:** 새 *HttpClientFactory* 를 연결할 수 있는 *DelegatingHandlers* 만듭니다는 *HttpClient* 으로 원하는 파이프라인 준비가 되었습니다. 처리 된 대체 내부 처리기를 연결에 대 한 기능을 제공 (기본값은 *HttpClientHandler*) 뿐만 아니라 사용 하는 경우를 고 배선 해야 하나요 *HttpMessageInvoker* 또는 다른  *DelegatingHandler* 대신 *HttpClient* 위쪽 호출자입니다.
- **ASP.NET 웹 최적화에서 Cdn에 대 한 지원:** 각각에 대해 지정할 수 있도록 하는 CDN 대체 경로가 번들 콘텐츠 배달 네트워크에 동일한 해당 리소스를 가리키는 추가 URL에 대 한 이제 ASP.NET 웹 최적화 지원을 제공 합니다. Cdn을 지 원하는 웹 응용 프로그램의 최종 소비자에 게 사용자 스크립트 및 스타일 번들 가깝게 지리적으로 가져올 수 있습니다.
- **구성 서버로 이동 하 고 ASP.NET Web API 라우팅합니다 *WebApiConfig.Register* resused 테스트 코드에서 일 수 있는 정적 메서드.** 이전에 ASP.NET Web API 경로에 추가 된 *RouteConfig.RegisterRoutes* 표준 MVC와 함께 라우팅합니다. 기본 ASP.NET Web API 라우트하 고 구성 하는 별도의 이제 처리 *WebApiConfig.Register* 을 쉽게 테스트할 메서드.

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진된 문제 및 주요 변경 내용

- **RC와 RTM 버전의 ASP.NET MVC 4 올바르게 반환 하지 캐시 된 데스크톱 뷰가 모바일 보기를 반환 합니다.**

    - 참조 [ASP.NET MVC 4 모바일 캐싱 버그 고정](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 수정 프로그램에 대 한 자세한 내용은 합니다. 수정 프로그램을 설치할 수 있습니다는 [고정 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet 패키지 합니다.
- **Razor 뷰 엔진의 주요 변경 내용**합니다. 다음 형식에서 제거 된 *System.Web.Mvc.Razor*: 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

 다음 방법도 제거 되었습니다. 

    - *MvcCSharpRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*
    - *MvcWebPageRazorHost.DecorateCodeGenerator(System.Web.Razor.Generator.RazorCodeGenerator)*
    - *MvcVBRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*
- **WebMatrix.WebData.dll에는 ASP.NET MVC 4 응용 프로그램의 /bin 디렉터리에 포함 되어 있으면, 폼 인증에 대 한 URL를 인계 받습니다.** / 계정/로그온에 대 한 인증 로그인 리디렉션을 무시 됩니다 (예를 들어 선택 하 여 "Razor 구문이 있는 ASP.NET 웹 페이지" 배포 가능 종속성 추가 대화 상자를 사용 하는 경우) 응용 프로그램에 WebMatrix.WebData.dll 어셈블리를 추가 하지 않고 / ASP.NET MVC 계정 컨트롤러 기본적으로 예상 대로 계정/로그인입니다. 이 문제를 방지 하 고 인증 섹션에서 web.config에 이미 지정 된 URL을 사용 하려면 PreserveLoginUrl를 호출 하는 appSetting을 추가 하 고 true로 설정: 

    [!code-xml[Main](mvc4-release-notes/samples/sample6.xml)]
- **NuGet 패키지 관리자 Visual Studio 2010 및 Visual Web Developer 2010의 병렬 설치에 대 한 ASP.NET MVC 4를 설치 하려고 하면 설치 되지 않습니다.** Visual Studio 2010과 Visual Web Developer 2010 ASP.NET MVC 4와 함께 실행 하려면 두 버전의 Visual Studio 설치 된 후 ASP.NET MVC 4를 설치 해야 합니다.
- **ASP.NET MVC 4를 제거 합니다. 필수 구성 요소가 이미 제거 된 경우 실패 합니다.** ASP.NET MVC를 완전히 제거 하려면 4you Visual Studio를 제거 하기 전에 ASP.NET MVC 4를 제거 해야 합니다.
- **ASP.NET MVC 3 RTM 응용 프로그램을 중단 ASP.NET MVC 4를 설치 합니다.** RTM을 사용 하 여 만든 ASP.NET MVC 3 응용 프로그램 릴리스 (아닌는 [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/en-us/download/details.aspx?id=1491) 릴리스) 나란히 ASP.NET MVC 4를 작동 하려면 다음과 같이 변경 해야 합니다. 컴파일 오류 수행 이러한 업데이트가 발생 하지 않고 프로젝트를 작성 합니다. 

    **필수 업데이트**

    1. 루트 Web.config 파일에는 새로운 추가  *&lt;appSettings&gt;*  항목 키와 *webPages:Version* 값 *1.0.0.0*합니다. 

        [!code-xml[Main](mvc4-release-notes/samples/sample7.xml)]
    2. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 프로젝트 언로드를 선택 합니다. 그런 다음 이름을 다시 마우스 오른쪽 단추로 클릭 하 고 편집 선택 *ProjectName*.csproj 합니다.
    3. 다음 어셈블리 참조를 찾습니다. 

        [!code-xml[Main](mvc4-release-notes/samples/sample8.xml)]

        다음으로 바꾸세요.

        [!code-xml[Main](mvc4-release-notes/samples/sample9.xml)]
    4. 변경 내용을 저장, 하면 편집 된 다음 마우스 오른쪽 단추로 클릭 프로젝트 다시 로드를 선택 하 고 프로젝트 (.csproj) 파일을 닫습니다.
- **4.5에서 ASP.NET MVC 4 프로젝트 대상 4.0로 변경 EntityFramework 어셈블리 참조를 업데이트 하지 않습니다:** 변경할 경우 ASP.NET MVC 4 프로젝트 대상 4.0 대상으로 하는 4.5 EntityFramework 어셈블리에 대 한 참조는 여전히 가리킵니다 후 4.5 버전입니다. 이 문제 제거를 수정 하 고 EntityFramework NuGet 패키지를 다시 설치 하십시오에.
- **4.0 대상 4.5에서 변경 된 후 Azure에서 ASP.NET MVC 4 응용 프로그램을 실행 하는 경우 403 사용할 수 없음:** 4.5 대상으로 한 후 대상 4.0에는 ASP.NET MVC 4 프로젝트를 변경 하 고 다음 Azure에 배포 런타임에 403 사용할 수 없음 오류가 표시 될 수 있습니다. 이 문제를 해결 하려면 web.config에 다음을 추가 합니다.`<modules runAllManagedModulesForAllRequests="true" />`
- **Visual Studio 2012를 입력 하는 경우 충돌을 '\' Razor 파일의 문자열 리터럴에서 합니다.** 실행 되도록 문제를 해결 리터럴 문자열의 닫는 따옴표를 먼저 입력 합니다.
- **찾아 &quot;계정/관리&quot; CHS, TRK 및 CHT 언어에 대 한 런타임 오류가 인터넷 템플릿 결과에 있습니다.** 문제를 해결 하려면 구분해 페이지를 수정  *@User.Identity.Name*  사용 하 여 내 유일한 콘텐츠로  *&lt;강력한&gt;*  태그입니다.
- **Google 및 LinkedIn 공급자는 Azure 웹 사이트 내에서 지원 되지 않습니다.** Azure 웹 사이트를 배포 하는 경우 다른 인증 공급자를 사용 합니다.
- **UriPathExtensionMapping IIS 8 Express/IIS와 함께 사용할 때 확장을 사용 하려고 할 때 404 찾을 수 없음 오류를 수신는 합니다.** 정적 파일 처리기를 사용 하는 web Api에 대 한 요청을 방해할 *UriPathExtensionMappings*합니다. 설정 *runAllManagedModulesForAllRequests = true* 문제를 해결 하려면 web.config에 있습니다.
- **Controller.Execute 방법은 더 이상 이라고 합니다.** 모든 MVC 컨트롤러는 이제 항상 비동기적으로 실행 합니다.
