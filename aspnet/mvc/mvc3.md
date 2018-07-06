---
uid: mvc/mvc3
title: ASP.NET MVC 3 | Microsoft Docs
author: rick-anderson
description: (2011 년 4 월 포함 Tools 업데이트) ASP.NET MVC 3 체계적인 디자인 패턴을 사용 하 여 확장성이 뛰어난 표준 기반 웹 응용 프로그램을 빌드하기 위한 프레임 워크는...
ms.author: aspnetcontent
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 2c2d53734cd62e59ee4f550713b0576a73b0e32b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37834772"
---
<a name="aspnet-mvc-3"></a>ASP.NET MVC 3
====================
> *(2011 년 4 월 포함 Tools 업데이트)*
> 
> ASP.NET MVC 3은 ASP.NET 및.NET Framework의 기능과 체계적인 디자인 패턴을 사용 하 여 확장성이 뛰어난 표준 기반 웹 응용 프로그램을 빌드하기 위한 프레임 워크입니다.
> 
> ASP.NET MVC 2를 지금 시작 하므로-나란히 설치!
> 
> 다운로드는 [여기에서 설치 관리자](https://go.microsoft.com/fwlink/?LinkID=208140)


## <a name="top-features"></a>주요 기능

- NuGet을 통해 확장 가능한 통합된 스 캐 폴딩 시스템
- HTML 5 설정 된 프로젝트 템플릿
- 새 Razor 보기 엔진을 비롯 한 표현 보기
- 종속성 주입 및 전역 작업 필터를 사용 하 여 강력한 후크
- JSON 바인딩, 비 가시적인 JavaScript 및 jQuery 유효성 검사와 다양 한 JavaScript 지원
- *전체 기능 목록의 읽을 [아래](#overview)*

## <a name="top-links"></a>맨 위 링크

ASP.NET MVC 3의에서 새로운 기능

- Phil Haack: [ASP.NET MVC 3 출시](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- Scott Hanselman: [ASP.NET MVC3, WebMatrix, NuGet, IIS Express 및 Orchard 출시-The Microsoft 웹 월 컨텍스트에서](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- Scott Guthrie: [ASP.NET MVC 3, IIS Express, SQL CE 4, 웹 팜 프레임 워크, Orchard, WebMatrix의 릴리스를 발표](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [ASP.NET MVC 3에 대 한 릴리스 정보](../whitepapers/mvc3-release-notes.md)

설치 및 도움말

- ASP.NET MVC 3 사용 하 여 설치를 [웹 플랫폼 설치 관리자 (권장)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)
- ASP.NET MVC 3 사용 하 여 설치를 [설치 관리자 실행](https://go.microsoft.com/fwlink/?LinkID=208140)
- 설치 [ASP.NET MVC 3 Visual Studio 11 개발자 미리 보기](https://go.microsoft.com/fwlink/?LinkID=208140)
- 읽기는 [ASP.NET MVC 3 자습서 소개](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)
- 도움말 및 ASP.NET MVC 3에 설명 된 [포럼](https://forums.asp.net/1146.aspx)

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>ASP.NET MVC 3 개요

ASP.NET MVC 3 기반으로 ASP.NET MVC 1과 2를 둘 다 코드를 단순화 및 심층적인 확장성을 허용 하는 훌륭한 기능을 추가 합니다. 이 항목에서는 다양 한이 릴리스의 경우 다음 섹션으로 구성에 포함 된 새 기능에 대 한 개요를 제공:

- [확장할 수 있는 스 캐 폴딩 MvcScaffold 통합](#BM_MvcScaffolding)
- [HTML 5 설정 된 프로젝트 템플릿](#BM_HTML5)
- [Razor 보기 엔진](#BM_TheRazorViewEngine)
- [여러 뷰 엔진에 대 한 지원](#BM_Support_for_Multiple_View_Engines)
- [컨트롤러의 향상 된 기능](#BM_Controller_Improvements)
- [JavaScript 및 Ajax](#BM_JavaScript_and_Ajax_Improvements)
- [모델 유효성 검사 향상](#BM_Model_Validation_Improvements)
- [종속성 주입 기능 향상](#BM_Dependency_Injection_Improvements)
- [기타 새로운 기능](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>확장할 수 있는 스 캐 폴딩 MvcScaffold 통합

새 스 캐 폴딩 시스템 쉽게 선택 하 고 사용 하 여 생산적으로 완전히 새로운 프레임 워크로 인 경우 시작 하 고을 경험이 있는 경우 일반적인 개발 작업을 자동화 하 고 작업을 잘 알고 있습니다.

새 NuGet에서 지원 됩니다 *스 캐 폴딩* 라는 패키지 **MvcScaffolding**합니다. 용어 "스 캐 폴딩" 하는 데 많은 소프트웨어 기술 "신속 하 게 수 있는 소프트웨어의 기본 구조를 생성 한 다음 편집 및 사용자 지정"을 의미 합니다. ASP.NET MVC에 대해 만드는 중입니다. 스 캐 폴딩 패키지는 여러 시나리오에서 매우 유용 합니다.

- **ASP.NET MVC를 처음 배우는 경우**이므로 다음 편집 하 고 필요에 따라 조정할 수 있는 몇 가지 유용한 작업 코드를 가져오기 하는 빠른 방법을 제공 합니다. 줄일 수에서 빈 페이지를 살펴보고 시작 위치를 알 수 없습니다 것의 충격!
- **ASP.NET MVC를 잘 알고 있고 이제 새 추가 기능 기술을 탐색 하는 경우** 테스트 라이브러리에는 개체 관계형 매퍼, 뷰 엔진 등 등, 해당 기술의 창조 또한 만들었을 스 캐 폴딩 패키지에 대 한 때문입니다.
- **회사에서는 반복적으로 유사한 클래스 또는 일종의 파일을 만듭니다 경우**이므로 테스트 픽스 쳐, 배포 스크립트 또는 다른 원하는 출력 하는 사용자 지정 스 캐 폴더를 만들 수 있습니다. 팀의 누구나에 사용자 지정 스 캐 폴더가 너무 사용할 수 있습니다.

MvcScaffolding의 다른 기능은 다음과 같습니다.

- C# 및 VB 프로젝트에 대 한 지원
- ASPX 고 Razor 보기 엔진에 대 한 지원
- ASP.NET MVC 영역으로 스 캐 폴딩 및 사용자 지정 보기 레이아웃/마스터를 사용 하 여 지원.
- T4 템플릿을 편집 하 여 출력 사용자 쉽게 지정할 수 있습니다.
- 사용자 지정 PowerShell 논리 및 사용자 지정 T4 템플릿을 사용 하 여 완전히 새로운 스 캐 폴더를 추가할 수 있습니다. 이러한 (및 사용자에 게 제공한 사용자 지정 매개 변수) 콘솔 탭 완성 기능 목록에 자동으로 표시 합니다.
- 다른 기술에 대 한 추가 스 캐 폴더를 포함 하는 NuGet 패키지를 가져올 수 있습니다 (예를 들어 만들어집니다는의 개념 증명 하나 linq to SQL) 조합 하 고 함께 일치

ASP.NET MVC 3 도구 업데이트와 같은이 스 캐 폴딩 시스템에 대 한 유용한 Visual Studio 지원에 포함 합니다.

- Controller 대화 상자에 이제 해당 뷰와 컨트롤러 작업 만들기, 읽기, 업데이트 및 삭제의 전체 자동 스 캐 폴딩을 추가 합니다. 기본적으로이 스 캐 폴딩 EF Code First를 사용 하 여 데이터 액세스 코드입니다.
- 컨트롤러 대화 지원 추가 *확장할 수 있는 스 캐 폴드* NuGet을 통해 패키지와 같은 *MvcScaffolding*합니다. 이렇게 하면 필요한 경우 ODBCDirect 통해 NHibernate 등도 JET 다른 데이터 액세스 기술에 대 한 스 캐 폴드를 만드는 데 허용 하는 대화 상자에 사용자 지정 스 캐 폴드에 플러그 인!

ASP.NET MVC 3에서 스 캐 폴딩에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- Steve Sanderson의 게시물 시리즈는: 

    1. [소개: MvcScaffolding 패키지를 사용 하 여 ASP.NET MVC 3 프로젝트를 스 캐 폴드](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [표준 사용: 일반적인 사용 사례 및 옵션](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [1 대 다 관계](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [스 캐 폴딩 작업 및 단위 테스트](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [T4 템플릿 재정의](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [이 게시물: 사용자 지정 스 캐 폴더 만들기](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- PDC 2010 세션의 Scott Hanselman의 게시물 [빌드 "웹 선호를의 명명 되지 않은 패키지" microsoft 블로그](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)
- [MVC 3 릴리스 정보](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>HTML 5 프로젝트 템플릿

새 프로젝트 대화 상자 프로젝트 템플릿의 확인란 사용 HTML 5 버전을 포함합니다. 이러한 템플릿을 활용 Modernizr 1.7 하위 브라우저에서 html5 및 CSS 3에 대 한 호환성 지원을 제공 합니다.

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>Razor 보기 엔진

ASP.NET MVC 3 Razor 다음과 같은 이점을 제공 하는 명명 된 새 뷰 엔진을 함께 제공 됩니다.

- Razor 구문은 깔끔하고 간결 최소 키 입력을 요구 합니다.
- Razor는 C# 및 Visual Basic과 같은 기존 언어를 기반으로 하기 때문에 일부 배우기 쉽습니다.
- Visual Studio Razor 구문에 대 한 IntelliSense 및 코드 색 지정을 포함합니다.
- Razor 뷰 단위 응용 프로그램을 실행 또는 웹 서버를 시작 하는 없이 테스트할 수 있습니다.

새 Razor 기능 중 일부는 다음과 같습니다.

- `@model` 보기에 전달 되는 유형을 지정 하는 구문입니다.
- `@* *@` 주석 구문입니다.
- 기본값을 지정 하는 기능 (같은 `layoutpage`) 전체 사이트에 한 번씩입니다.
- `Html.Raw` 메서드 HTML 인코딩하지 않고 텍스트를 표시 하기 위한 것입니다.
- 여러 뷰 간에 코드 공유에 대 한 지원 (*\_viewstart.cshtml* 하거나  *\_viewstart.vbhtml* 파일).

Razor에는 다음과 같은 새 HTML 도우미도 포함 됩니다.

- `Chart`. ASP.NET 4의 차트 컨트롤과 같은 기능을 제공 하는 차트를 렌더링 합니다.
- `WebGrid`. 페이징 및 정렬 기능을 사용 하 여 전체 데이터 표를 렌더링합니다.
- `Crypto`. 솔트된 하 및 암호를 해시 하는 해시를 제대로 만드는 알고리즘 사용 합니다.
- `WebImage`. 이미지를 렌더링합니다.
- `WebMail`. 이메일 메시지를 보냅니다.

Razor에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Razor 소개 하는 Scott Guthrie의 블로그 게시물](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [Scott Guthrie의 블로그 게시물 소개를 @model 키워드](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [Scott Guthrie의 블로그 게시물 소개 Razor 레이아웃](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [Razor API 빠른 참조](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [MVC 3 릴리스 정보](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>여러 뷰 엔진에 대 한 지원

합니다 **뷰 추가** ASP.NET MVC 3의 대화 상자를 사용 하면 작업 하려는 뷰 엔진을 선택 하며 **새 프로젝트** 대화 상자는 프로젝트에 대 한 기본 뷰 엔진을 지정할 수 있습니다. Web Forms 뷰 엔진 (ASPX), Razor, 또는 오픈 소스 뷰 엔진을 같은 선택할 수 있습니다 [Spark](http://sparkviewengine.com/)하십시오 [NHaml](https://code.google.com/p/nhaml/), 또는 [NDjango](http://ndjango.org/)합니다.

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>컨트롤러의 향상 된 기능

### <a name="global-action-filters"></a>전역 작업 필터

동작 메서드가 실행 되기 전에 또는 작업 메서드가 실행 된 이후에 논리를 수행 하려는 경우가 있습니다. 이 지 원하는 ASP.NET MVC 2 작업 필터를 제공 합니다. 작업 필터는 특정 컨트롤러 작업 메서드에 사전 작업 및 작업 이후의 동작을 추가 하는 선언적 수단을 제공 하는 사용자 지정 특성입니다. 그러나 일부 경우에서 하려는 모든 작업 메서드에 적용 되는 사전 작업 또는 작업 후 동작을 지정 합니다. MVC 3을 사용 하면 추가 하 여 전역 필터를 지정할 수는 `GlobalFilters` 컬렉션입니다. 전역 작업 필터에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [MVC 3 Preview에 대 한 Scott Guthrie의 블로그](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [ASP.NET MVC의 필터링](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>새 "ViewBag" 속성

MVC 2 컨트롤러 지원은 `ViewData` 속성 보기 템플릿에 바인딩된 사전 API를 사용 하 여 데이터를 전달할 수 있도록 합니다. MVC 3에서 사용할 수도 있습니다와 다소 더 간단한 구문은 `ViewBag` 동일한 목적을 수행 하는 속성입니다. 예를 들어, 작성 하는 대신 `ViewData["Message"]="text"`를 작성할 수 있습니다 `ViewBag.Message="text"`합니다. 사용 하는 모든 강력한 형식의 클래스를 정의할 필요가 없습니다를 `ViewBag` 속성입니다. 동적 속성 이기 때문에 가져올 수 있습니다만 또는 속성을 설정 하며 확인 되 고 동적으로 런타임 시. 내부적으로 `ViewBag` 속성의 이름/값 쌍으로 저장 됩니다는 `ViewData` 사전입니다. (참고: MVC 3의 대부분의 시험판 버전에는 `ViewBag` 속성 이름이 `ViewModel` 속성입니다.)

### <a name="new-actionresult-types"></a>새 "ActionResult" 형식

다음 `ActionResult` 형식 및 해당 도우미 메서드는 새 또는 MVC 3에서 기능이 향상 되었습니다.

- [HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx). 404 HTTP 상태 코드를 클라이언트에 반환합니다.
- [된 RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx)합니다. 임시 리디렉션 (HTTP 302 상태 코드) 또는 부울 매개 변수에 따라 영구 리디렉션 (HTTP 301 상태 코드)를 반환합니다. 이렇게이 변경 하면 함께에서 합니다 [컨트롤러](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) 클래스에는 이제 영구 리디렉션을 수행 하는 것에 대 한 세 가지 방법에: `RedirectPermanent`, `RedirectToRoutePermanent`, 및 `RedirectToActionPermanent`합니다. 이러한 메서드는 인스턴스를 반환 `RedirectResult` 사용 하 여 합니다 `Permanent` 속성으로 설정 `true`합니다.
- [HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx). 사용자 지정 HTTP 상태 코드를 반환합니다.

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>JavaScript 및 Ajax 향상 된 기능

기본적으로 MVC 3에서 Ajax 및 유효성 검사 도우미 눈에 띄지 않는 JavaScript 접근 방식을 사용 합니다. 비간섭 JavaScript 인라인 JavaScript를 HTML 삽입을 방지 합니다. HTML 작고 덜 혼잡을 있고 쉽게 교체 하거나 JavaScript 라이브러리를 사용자 지정 됩니다. MVC 3에서 유효성 검사 도우미도 사용 하 여는 `jQueryValidate` 기본적으로 플러그 인입니다. MVC 2 동작을 원하는 경우 비간섭 JavaScript를 사용 하 여 비활성화할 수 있습니다는 *web.config* 파일 설정 합니다. JavaScript 및 Ajax 향상에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Wikipedia 사이트에서 비간섭 JavaScript에 대 한 기본적인 내용을 소개](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [Brad Wilson의 눈에 띄지 않는 JavaScript 게시물](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [Brad Wilson의 비간섭 JavaScript 유효성 검사 게시](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [Razor 및 비간섭 JavaScript를 사용 하 여 MVC 3 응용 프로그램을 만드는](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (ASP.NET 사이트의 자습서)
- [MVC 3 릴리스 정보](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>기본적으로 사용 하도록 설정 하는 클라이언트 쪽 유효성 검사

MVC의 이전 버전에서 명시적으로 호출 해야 합니다 `Html.EnableClientValidation` 클라이언트 쪽 유효성 검사를 사용 하도록 설정 하려면 뷰에서 메서드. MVC 3에서 더 이상 때문에 이것이 필요 클라이언트 쪽 유효성 검사는 기본적으로 사용 합니다. (의 설정을 사용 하 여 비활성화할 수 있습니다 합니다 *web.config* 파일입니다.)

클라이언트 쪽 유효성 검사 작업에 대 한 순서 대로 적절 한 jQuery 및 사이트에서 jQuery 유효성 검사 라이브러리를 참조 해야 합니다. 사용자 고유의 서버에서 해당 라이브러리를 호스트할 수도 있고 Microsoft 또는 Google의 Cdn 같은 content delivery network (CDN)에서 참조할 수 있습니다.

### <a name="remote-validator"></a>원격 유효성 검사기

ASP.NET MVC 3 새 지원 [RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) 플러그 jQuery 유효성 검사를 활용할 수 있는 클래스의 원격 유효성 검사기 지원 합니다. 이 자동으로 서버 쪽만 수행할 수 있는 유효성 검사 논리를 수행 하기 위해 서버에서 정의한 사용자 지정 메서드를 호출 하려면 클라이언트 쪽 유효성 검사 라이브러리를 사용 하도록 설정 합니다.

다음 예제에서는 `Remote` 특성 지정 클라이언트 유효성 검사 라는 작업을 호출 합니다 `UserNameAvailable` 에 `UsersController` 의 유효성을 검사 하기 위해 클래스는 `UserName` 필드.

[!code-csharp[Main](mvc3/samples/sample1.cs)]

다음 예제에서는 해당 컨트롤러를 보여 줍니다.

[!code-csharp[Main](mvc3/samples/sample2.cs)]

사용 하는 방법에 대 한 자세한를 `Remote` 특성을 참조 하십시오 [방법: ASP.NET MVC에서 원격 유효성 검사 구현](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) MSDN library에서.

### <a name="json-binding-support"></a>JSON의 바인딩 지원

ASP.NET MVC 3 JSON으로 인코딩된 데이터를 수신 하 고 모델에 바인딩할 수 고 동작 메서드 매개 변수를 작업 메서드를 사용 하도록 설정 하는 기본 제공 JSON 바인딩 지원을 포함 합니다. 이 기능은 클라이언트 템플릿 및 데이터 바인딩을 포함 하는 시나리오에서 유용 합니다. (클라이언트 템플릿을 사용 하면 서식을 지정 하 고 클라이언트에서 실행 되는 템플릿을 사용 하 여 단일 데이터 항목 또는 데이터 항목 집합을 표시 합니다.) MVC 3 JSON 데이터를 송수신 하는 서버에서 작업 메서드를 사용 하 여 클라이언트 템플릿을 쉽게 연결할 수 있습니다. JSON의 바인딩 지원에 대 한 자세한 내용은 참조 하세요. 합니다 **JavaScript 및 AJAX 향상** 부분 [Scott Guthrie의 MVC 3 Preview 블로그 게시물](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)합니다.

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>모델 유효성 검사 향상

### <a name="dataannotations-metadata-attributes"></a>"DataAnnotations" 메타 데이터 특성

ASP.NET MVC 3을 지 원하는 `DataAnnotations` 메타 데이터와 같은 특성 `DisplayAttribute`합니다.

### <a name="validationattribute-class"></a>"ValidationAttribute" 클래스

합니다 `ValidationAttribute` 새 지원 하기 위해.NET Framework 4에서 클래스 개선 되었습니다 `IsValid` 같은 개체에 따라 유효성 검사 중인 현재 유효성 검사 컨텍스트에 대 한 자세한 정보를 제공 하는 오버 로드 합니다. 이 통해 다양 한 시나리오는 모델의 다른 속성에 따라 현재 값을 확인할 수 있습니다. 예를 들어 새 `CompareAttribute` 특성을 사용 하면 모델의 두 속성의 값을 비교 합니다. 다음 예제에서는 `ComparePassword` 속성과 일치 해야는 `Password` 유효 하기 위해 필드입니다.

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>유효성 검사 인터페이스

합니다 [IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) 인터페이스를 사용 하면 모델 수준 유효성 검사를 수행할 수 있습니다 및 유효성 검사 또는 모델 내에서 두 속성 간의 전체 모델의 상태에 관련 된 오류 메시지를 제공할 수 있습니다 . MVC 3에는 이제 오류를 검색 합니다 `IValidatableObject` 모델 바인딩 및 자동으로 플래그 또는 주요 기본 제공 HTML 양식 도우미를 사용 하 여 뷰 내에서 필드를 받는 경우 인터페이스.

합니다 [IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) 인터페이스에서 ASP.NET MVC 유효성 검사기가 클라이언트 유효성 검사를 지원 하는지 여부를 런타임에 검색할 수 있습니다. 이 인터페이스는 다양 한 유효성 검사 프레임 워크와 통합 될 수 있도록 설계 되었습니다.

유효성 검사 인터페이스에 대 한 자세한 내용은 참조는 **모델 유효성 검사 향상** 부분 [Scott Guthrie의 MVC 3 Preview 블로그 게시물](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)합니다. 그러나 (note 블로그의 "IValidateObject"에 대 한 참조 "IValidatableObject" 되도록 합니다.)

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>종속성 주입 기능 향상

ASP.NET MVC 3 DI (종속성 주입)를 적용 하 고 종속성 주입 또는 제어 반전 (IOC) 컨테이너를 사용 하 여 통합 하기 위한 더 나은 지원을 제공 합니다. 다음 영역에서 DI에 대 한 지원이 추가 되었습니다.

- 컨트롤러 (등록 및 컨트롤러 팩터리, 컨트롤러 삽입 삽입).
- 뷰 (등록 하 고 뷰 엔진, 페이지 보기에 종속성 주입을 주입).
- 작업 필터 (찾기 및 필터를 주입)입니다.
- 모델 바인더 (등록 및 삽입)입니다.
- 모델 유효성 검사 공급자 (등록 및 삽입)입니다.
- 모델 메타 데이터 공급자 (등록 및 삽입)입니다.
- 값 공급자 (등록 및 삽입)입니다.

MVC 3을 지원 합니다 [공통 서비스 로케이터](https://github.com/unitycontainer/commonservicelocator) 라이브러리 및 해당 라이브러리를 지 원하는 DI 컨테이너 `IServiceLocator` 인터페이스입니다. 또한 새 지원 `IDependencyResolver` 쉽게 DI 프레임 워크를 통합 하는 인터페이스입니다.

MVC 3에서 DI에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Brad Wilson의 일련의 서비스 위치에 대 한 블로그 게시물](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [MVC 3 릴리스 정보](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>기타 새로운 기능

### <a name="nuget-integration"></a>NuGet 통합

ASP.NET MVC 3는 자동으로 설치 하 고 해당 설정의 일부분으로 NuGet을 사용 하도록 설정 합니다. NuGet은 쉽게 찾고, 설치, 프로젝트에서.NET 라이브러리 및 도구를 사용 하는 무료 오픈 소스 패키지 관리자입니다. 모든 Visual Studio 프로젝트 형식 (ASP.NET Web Forms 및 ASP.NET MVC 포함)를 사용 하 여 작동 합니다.

NuGet 패키지는 라이브러리 및 온라인 갤러리에 등록 합니다 오픈 소스 프로젝트 (예를 들어, Moq, NHibernate, Ninject, StructureMap, NUnit, Windsor, RhinoMocks, Elmah 등)를 유지 관리 하는 개발자를 수 있습니다. 그런 다음 이러한 라이브러리 중 하나를 사용 하 여 패키지를 검색 하 여 작업 중인 프로젝트에 설치 하려는.NET 개발자는 것이 쉽습니다.

ASP.NET 3 도구 업데이트를 사용 하 여 프로젝트 템플릿에 JavaScript 라이브러리가 사전 설치 된 NuGet 패키지를 포함 하는 NuGet을 통해 업데이트할 수 있도록. Entity Framework Code First는 미리 설치 된 NuGet 패키지로 합니다.

NuGet에 대한 자세한 내용은 [NuGet 설명서](https://docs.microsoft.com/nuget/)를 참조하세요.

### <a name="partial-page-output-caching"></a>부분 페이지 출력 캐싱

ASP.NET MVC 버전 1의 전체 페이지 응답 출력 캐싱을 지원 해 왔습니다. MVC 3 부분 페이지 출력 캐싱도 지원, 쉽게 캐시 지역 또는 응답의 조각에 있습니다. 캐싱에 대 한 자세한 내용은 참조는 **부분 페이지 출력 캐싱** 부분 [MVC 3 release candidate Scott Guthrie의 블로그 게시물](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) 및 **자식 작업 출력 캐싱을** 의 섹션을 [MVC 3 릴리스 정보](../whitepapers/mvc3-release-notes.md)합니다.

### <a name="granular-control-over-request-validation"></a>요청 유효성 검사에 대 한 세부적인 제어

ASP.NET MVC에 자동으로 XSS 및 HTML 삽입 공격 으로부터 보호 하는 기본 제공 요청 유효성 검사 합니다. 그러나 명시적으로 사용 하지 않도록 설정 요청 유효성 검사 하려는 경우가 있습니다 경우와 같이 하려는 HTML 콘텐츠 (예를 들어, 블로그 또는 CMS 콘텐츠) 게시할 수 있습니다. 이제 추가할 수 있습니다는 [AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) 특성을 모델 또는 모델 바인딩 중 속성별 별로 요청 유효성 검사를 사용 하지 않도록 설정 하는 모델을 확인 합니다. 요청 유효성 검사에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- **비 가시적인 JavaScript 및 유효성 검사** 단원의 [Scott Guthrie의 블로그 게시물에서 MVC 3 release candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)합니다.
- [MVC 3 릴리스 정보](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>확장 가능한 "새 프로젝트" 대화 상자

ASP.NET MVC 3에서 프로젝트 템플릿, 뷰 엔진을 추가할 수 있습니다 및 단위 테스트 프레임 워크가 프로젝트의 **새 프로젝트** 대화 상자.

### <a name="template-scaffolding-improvements"></a>템플릿 스 캐 폴딩 개선 사항

모델에서 기본 키 속성을 식별 하 고 처리 보다 적절 하 게 하는 이전 버전의 MVC 더 나은 작업을 수행 하는 ASP.NET MVC 3 스 캐 폴딩 템플릿이 있습니다. (예를 들어, 스 캐 폴딩 템플릿이 있어야는 기본 키가 없습니다 스 캐 폴드 된 편집 가능한 폼 필드와.)

기본적으로 만들기 및 편집 스 캐 폴드 이제 사용 합니다 `Html.EditorFor` 대신 도우미는 `Html.TextBoxFor` 도우미입니다. 이렇게 하면 데이터의 형태로 모델에 대 한 메타 데이터에 대 한 지원이 향상 됩니다. 때 주석 특성을 **뷰 추가** 대화 상자는 뷰가 생성 됩니다.

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>"Html.LabelFor" 및 "Html.LabelForModel"에 대 한 새 오버 로드

에 대 한 새 메서드 오버 로드가 추가 되어는 `LabelFor` 고 `LabelForModel` 도우미 메서드. 새 오버 로드를 사용 하면 지정 또는 레이블 텍스트를 재정의할 수 있습니다.

### <a name="sessionless-controller-support"></a>Sessionless 컨트롤러 지원

그렇다면 및 세션 상태를 사용 하는 컨트롤러 클래스를 할지 여부를 지정할 수 있습니다 ASP.NET MVC 3에서 여야 하는지 여부 세션 상태가 읽기/쓰기 또는 읽기 전용입니다. Sessionless 컨트롤러 지원에 대 한 자세한 내용은 참조 하십시오 [MVC 3 릴리스 정보](../whitepapers/mvc3-release-notes.md)합니다.

### <a name="new-additionalmetadataattribute-class"></a>새 "AdditionalMetadataAttribute" 클래스

사용할 수는 [AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) 특성을 채우는 `ModelMetadata.AdditionalValues` 모델 속성에 대 한 사전입니다. 예를 들어, 보기 모델 관리자 에게만 표시 해야 하는 속성에는 다음 예와 같이 해당 속성을 주석을 지정할 수 있습니다.

[!code-csharp[Main](mvc3/samples/sample4.cs)]

제품 보기 모델 렌더링 될 때이 메타 데이터 표시 또는 편집기 템플릿에 제공 됩니다. 메타 데이터 정보를 해석 하는 것입니다.

### <a name="accountcontroller-improvements"></a>AccountController 개선 사항

인터넷 프로젝트 템플릿에서 AccountController 크게 향상 되었습니다.

### <a name="new-intranet-project-template"></a>새 인트라넷 프로젝트 템플릿

새 인트라넷 프로젝트 템플릿이 포함 되어는 Windows 인증을 사용 하도록 설정 하 고는 AccountController를 제거 합니다.
