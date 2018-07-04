---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET 및 Web Tools 2012.2 릴리스 정보 | Microsoft Docs
author: rick-anderson
description: ASP.NET 및 웹 도구 2012.2 릴리스 정보입니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/14/2013
ms.topic: article
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
ms.technology: ''
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: fe26f1f312415d97d71d2ab75d04877dc4a9cfbb
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37362400"
---
<a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET 및 Web Tools 2012.2 릴리스 정보
====================
> 이 문서에서는 ASP.NET 및 웹 도구 2012.2 릴리스를 설명 합니다. Visual Studio Web Tooling 및 ASP.NET에 대 한 업데이트는 것입니다.


- [설치 참고 사항](#_Installation)
- [문서](#_Documentation)
- [지원](#_Support)
- [소프트웨어 요구 사항](#_Software_Requirements)
- [ASP.NET 및 Web Tools 2012.2의 새로운 기능](#_New_Features_in)

    - [도구](#_Tooling)
    - [웹 게시](#_Web_Publishing)
    - [ASP.NET MVC 템플릿](#_Templates)
    - [ASP.NET Web API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [Asp.net Url](#_ASP.NET_Friendly_URLs)
- [알려진된 문제 및 주요 변경 내용](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>설치 참고 사항

ASP.NET 및 Visual Studio 2012 용 웹 도구 2012.2를 사용해 설치 가능 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)합니다. 이것이 Visual Studio 2012 또는 Visual Studio Express 2012 for Web, 필요한 업데이트입니다. 설치 된 Visual Studio가 없는 경우 Visual Studio Express 2012 for Web이 설치 됩니다.

또한 수동으로 설치할 수 있습니다 ASP.NET 및 웹 도구 2012.2 합니다. Visual Studio 2012 또는 Visual Studio Express 2012 for Web 설치 해야 합니다. 다음 지침을 따르세요. 

1. 다운로드 [ASP.NET 및 Frameworks 2012.2 웹](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) 다운로드 센터에서 설치 관리자입니다.
2. 경우 입력 정보를 요청 실행을 클릭 합니다. 또한 나중에 실행 파일을 저장할 수 있습니다.
3. 업데이트는 Visual Studio의 버전을 확인 합니다. 업데이트 하려는 Visual Studio를 시작 하 여이 수행할 수 있습니다. 도움말 메뉴 항목을 클릭 합니다.   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. 메뉴 항목을 표시 하는 경우 &quot;에 대 한 Microsoft Visual Studio 2012 for Web&quot; 다운로드 한 다음 [Visual Studio Express 2012 for Web-웹 개발자 도구 2012.2](https://go.microsoft.com/fwlink/?LinkID=282228)합니다. 그렇지 않은 경우 다운로드할 [웹 개발자 도구 2012.2-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)합니다.
5. 경우 입력 정보를 요청 실행을 클릭 합니다. 또한 나중에 실행 파일을 저장할 수 있습니다.

> [!NOTE]
> ASP.NET 및 웹 도구 2012.2 릴리스는 SQL Server Data Tools를 포함 하지 않습니다. SQL Server 및 Windows Azure SQL Database는 다양 한 데이터베이스 오프 라인 프로젝트 기반의 개발, 스키마 비교 및 향상 된 데이터베이스 배포 기능을 포함 하 여 도구를 제공 합니다. 자세한 내용을 보거나 SQL Server Data Tools 설치를 방문 [ https://go.microsoft.com/fwlink/?LinkID=237127 ](https://go.microsoft.com/fwlink/?LinkID=237127)합니다.

<a id="_Documentation"></a>
## <a name="documentation"></a>설명서

ASP.NET 및 웹 도구 2012.2 정보 및 자습서는 ASP.NET 웹 사이트에서 사용할 수 있습니다 ( https://www.asp.net)합니다.

<a id="_Support"></a>
## <a name="support"></a>Support(지원)

ASP.NET 및 웹 도구 2012.2 릴리스 공식적으로 이며 지원 합니다. 일반적인 지원 채널을 사용할 수 있습니다. ASP.NET 포럼에 질문을 게시할 수도 있습니다 ([https://forums.asp.net/](https://forums.asp.net/)) ASP.NET 커뮤니티 회원이 비공식적인 지원을 제공 하기 위해 자주 수 있는, 합니다.

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

ASP.NET 및 웹 도구 2012.2 Visual Studio 2012 또는 Visual Studio Express 2012 for Web 필요 합니다.

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>ASP.NET 및 Web Tools 2012.2의 새로운 기능

이 섹션에서는 ASP.NET 및 웹 도구 2012.2 릴리스에서 도입 된 기능을 설명 합니다.

<a id="_Tooling"></a>
### <a name="tooling"></a>도구

- 페이지 검사기 

    - 페이지 검사기에 페이지를 다시 해당 JavaScript 코드에 동적으로 추가 된 항목을 매핑할 수 있도록 하는 JavaScript 선택 매핑을 지원 합니다.
    - 실시간 CSS 업데이트를 확인할 수 있습니다.
    - 자세한 내용은 [CSS 자동 동기화 및 페이지 검사기에서 JavaScript 선택 매핑](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)합니다.
- 편집기 

    - CoffeeScript, Mustache, Handlebars, 및 JsRender에 대 한 구문 강조 표시를 지원 합니다.
    - HTML 편집기 Knockout 바인딩에 대 한 Intellisense를 제공합니다.
    - 작은 편집 및 컴파일러 작은 사용 하 여 동적 CSS를 빌드할 수 있도록 지원 합니다.
    - .NET 클래스로 JSON 붙여 넣습니다. 이 특수 붙여넣기 명령을 사용 하 여 C# 또는 VB.NET 코드 파일을 Visual Studio에 JSON를 붙여 넣습니다. JSON에서 유추 하는.NET 클래스를 자동으로 생성 됩니다.
- VSIX로 타사 에뮬레이터를 설치할 수 있도록 확장성 후크를 추가 하는 모바일 에뮬레이터 지원 합니다. 설치 된 에뮬레이터 나타납니다 F5 드롭다운 목록에서 개발자는 다양 한 모바일 장치에서 웹 사이트를 미리 볼 수 있도록 합니다. Scott Hanselman의 블로그 항목을이 기능에 대해 자세히 알아보세요 [Visual Studio를 사용 하 여 새 BrowserStack 통합](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)합니다.

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>웹 게시

- 웹 사이트 프로젝트는 이제 Windows Azure 웹 사이트에 게시를 포함 하 여 웹 응용 프로그램 프로젝트와 동일한 게시 환경을 있습니다.
- 선택적 게시 &#8211; 하나 이상의 파일 (웹 배포 끝점에 게시) 한 후 다음 작업을 수행할 수 있습니다. 

    - 선택한 파일을 게시 합니다.
    - 로컬 파일 및 원격 파일 간의 차이 참조 하세요.
    - 원격 파일을 사용 하 여 로컬 파일을 업데이트 하거나 로컬 파일을 사용 하 여 원격 파일을 업데이트 합니다.

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET MVC 템플릿

- 새 Facebook 응용 프로그램 템플릿 Facebook Canvas 응용 프로그램을 쉽게 작성할 수 있습니다. 몇 가지 간단한 단계에서 로그인된 한 사용자에서 데이터를 가져와서 해당 친구와 통합 되는 Facebook 응용 프로그램을 만들 수 있습니다. 템플릿에 인증, 사용 권한, Facebook 데이터 액세스를 포함 하 여 Facebook 응용 프로그램 작성과 관련 된 모든 배관을 처리 하기 위한 새 라이브러리가 포함 되어 있습니다. Facebook 응용 프로그램 템플릿을 사용 하 여 대 한 자세한 내용은 참조 하세요 [ https://go.microsoft.com/fwlink/?LinkID=269921 ](https://go.microsoft.com/fwlink/?LinkID=269921)합니다.
- 새 단일 페이지 응용 프로그램 MVC 템플릿을 HTML 5, CSS 3 및 Knockout 및 jQuery JavaScript 라이브러리를 ASP.NET Web API를 사용 하 여 대화형 클라이언트 쪽 웹 앱을 빌드하는 개발자를 수 있습니다. 템플릿은 RESTful 서버 API를 사용 하는 JavaScript HTML5 응용 프로그램을 작성 하기 위한 일반적인 방법을 보여 주는 "todo" 목록 응용 프로그램을 포함 합니다. 자세히 알아볼 수 있습니다 [ https://www.asp.net/single-page-application ](../../../single-page-application/index.md)합니다.
- 이제 ASP.NET MVC 새 프로젝트 대화 상자에 새 템플릿을 추가 하는 VSIX를 만들 수 있습니다. 여기에서 방법을 알아보세요. [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- FixedDisplayModes 패키지 &#8211; MVC 프로젝트 템플릿은 MVC 4의 버그 해결을 포함 하는 새 'FixedDisplayModes' NuGet 패키지를 포함 하도록 업데이트 되었습니다. 패키지에 포함 된 수정에 대 한 자세한 내용은이 블로그 게시물을 참조 하세요 ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) MVC 팀에서.

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET Web API 몇 가지 새로운 기능을 사용 하 여 향상 되었습니다.

- ASP.NET Web API OData
- ASP.NET Web API 추적
- ASP.NET Web API 도움말 페이지

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

ASP.NET Web API OData는 모든 데이터 원본에 대해 다양 한 비즈니스 논리를 사용 하 여 OData 끝점을 작성 하는 데 필요한 유연성을 제공 합니다. ASP.NET Web API OData를 사용 하 여 OData 의미 체계를 노출 하려는 양을 제어할 수 있습니다. ASP.NET Web API OData는 ASP.NET MVC 4 프로젝트 템플릿이 포함 되어 있으며 NuGet에서 사용할 수 있습니다 ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)).

ASP.NET Web API OData는 현재 다음과 같은 기능을 지원합니다.

- [Queryable] 특성을 적용 하 여 OData 쿼리 의미 체계를 사용 합니다.
- 쉽게 OData 쿼리의 유효성을 검사 하 고 지원 되는 쿼리 옵션, 연산자 및 함수는 집합을 제한 합니다.
- 매개 변수 다음의 유효성을 검사 하 고 수 IEnumerable 또는 IQueryable에 적용 하는 쿼리의 추상 구문 트리 표현을 가져오는에 직접 ODataQueryOptions에 바인딩합니다.
- [Queryable] 특성에서 결과 한도 지정 하 여 서비스 기반 페이징 및 다음 페이지 링크 생성을 활성화 합니다.
- 총 $inlinecount을 사용 하 여 일치 하는 리소스에 대 한 인라인된 카운트를 요청 합니다.
- Null 전파를 제어 합니다.
- $Filter에서 일부/모든 연산자입니다.
- 규칙에 따라 엔터티 데이터 모델을 유추 하거나 명시적으로 유사한를 Entity Framework 코드 중심 방식으로 모델을 사용자 지정 합니다.
- EntitySetController에서 파생 하 여 노출 엔터티 집합입니다.
- 탐색 속성을 노출 하 고 링크를 조작할 OData 작업 구현에 대 한 간단 하 고 사용자 지정 가능한 규칙입니다.
- MapODataRoute 확장 메서드를 사용 하 여 라우팅 간소화 합니다.
- 여러 EDM 모델을 노출 하 여 버전 관리를 지원 합니다.
- 서비스 문서 및 노출 $metadata 클라이언트 (.NET, Windows Phone, Windows 스토어 등)를 생성할 수 있습니다 웹 API에 대 한 합니다.
- OData Atom, JSON 및 JSON 자세한 정보 표시 형식에 대해 지원 합니다.
- 만들기, 업데이트, 부분적으로 업데이트 (PATCH) 및 엔터티를 삭제 합니다.
- 쿼리하고 엔터티 간의 관계를 조작 합니다.
- 연결 하 여 경로 관계 링크를 만듭니다.
- 복합 형식
- 엔터티 형식 상속 합니다.
- 컬렉션 속성입니다.
- 열거형입니다.
- OData 작업입니다.
- 동일한 기반 WCF Data Services, 즉 ODataLib 기반으로 ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)).

ASP.NET Web API OData에 대 한 자세한 내용은 참조 하세요 [ https://go.microsoft.com/fwlink/?LinkId=271141 ](https://go.microsoft.com/fwlink/?LinkId=271141)합니다.

#### <a name="aspnet-web-api-tracing"></a>ASP.NET Web API 추적

.NET 추적을 사용 하 여 web Api에서에서 추적 데이터를 통합 하는 ASP.NET Web API 추적 합니다. 이제 Web API 프로젝트 템플릿에 기본적으로 활성화 됩니다. 웹에 대 한 데이터를 추적 Api 출력 창에 전송 되 고 IntelliTrace를 통해 사용할 수 있습니다. 통합을 통해 Windows Azure에서 호스트 되는 경우 Web API에 대 한 정보를 추적 하면 ASP.NET 웹 API 추적 [Windows Azure 진단](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)합니다. 또한 설치 하 고 ASP.NET 웹 API 추적 NuGet 패키지를 사용 하 여 모든 응용 프로그램에서 ASP.NET 웹 API 추적을 사용 수 있습니다 ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)).

구성 및 ASP.NET Web API 추적 사용에 대 한 자세한 내용은 참조 하세요 [ https://go.microsoft.com/fwlink/?LinkID=269874 ](https://go.microsoft.com/fwlink/?LinkID=269874)합니다.

#### <a name="aspnet-web-api-help-page"></a>ASP.NET Web API 도움말 페이지

이제 ASP.NET Web API 도움말 페이지는 Web API 프로젝트 템플릿에 기본적으로 포함 됩니다. ASP.NET Web API 도움말 페이지는 자동으로 웹 HTTP 끝점, 지원 되는 HTTP 메서드, 매개 변수 및 예제 요청 및 응답 메시지 페이로드를 포함 하 여 Api에 대 한 설명서를 생성 합니다. 문서를 자동으로 코드의 주석에서 가져옵니다. ASP.NET Web API 도움말 페이지 NuGet 패키지를 사용 하 여 모든 응용 프로그램에 ASP.NET Web API 도움말 페이지를 추가할 수도 있습니다 ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)).

설정 및 ASP.NET Web API 도움말 페이지 참조를 사용자 지정에 대 한 자세한 내용은 [ https://go.microsoft.com/fwlink/?LinkId=271140 ](https://go.microsoft.com/fwlink/?LinkId=271140)합니다.

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR을 간단히 ASP.NET 응용 프로그램에 실시간 웹 기능을 추가 및 가능 하면 Websocket을 사용 하 여 자동으로 대체 다른 기술 하지 않은 경우.

ASP.NET SignalR을 사용 하 여 대 한 자세한 내용은 참조 하세요 [ https://go.microsoft.com/fwlink/?LinkId=271271 ](https://go.microsoft.com/fwlink/?LinkId=271271)합니다.

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>Asp.net Url

ASP.NET FriendlyURLs 매우 쉽게 웹 개발자에 게 forms (.aspx 확장명 없음) Url을 찾고 수행 되는 클리너를 생성 합니다. No로 적은 구성이 필요로 하 고 기존 ASP.NET v4.0 응용 프로그램과 함께 사용할 수 있습니다. FriendlyURLs 기능 또한 쉽게 지원 데스크톱 및 모바일 보기 간에 전환 하 여 해당 응용 프로그램에 모바일 지원을 추가 하는 개발자를 위한 있습니다.

설치 및 ASP.NET Url 사용에 대 한 자세한 내용은 참조 하세요 [ http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx ](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)합니다.

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진된 문제 및 주요 변경 내용

이 섹션에는 알려진된 문제 및 ASP.NET 및 웹 도구 2012.2 릴리스에 주요 변경 내용을 설명 합니다.

### <a name="installation-issues"></a>설치 문제

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>Visual Studio 2012의 순서가 설치

복구 작업을 해야 ASP.NET 및 웹 도구 2012.2 설치 후는 추가 SKU의 Visual Studio 2012를 설치 합니다. 다음 시퀀스를 고려해 야 합니다.

1. 웹용 Visual Studio 2012 Express 설치
2. ASP.NET 및 Web Tools 2012.2 설치
3. Visual Studio 2012 Professional, Premium 또는 Ultimate를 설치 합니다.

2 단계 Express for Web 용 업데이트 설치만 반환 됩니다. 3 단계 중에 설치 하는 추가 SKU 업데이트를 포함 하도록 설치 하는 마지막 SKU에 대 한 업데이트를 설치 하려면 ASP.NET 및 웹 도구 2012.2 복구 해야 합니다. 또한 1 단계에서에서 Sku 및 3 반대 하는 경우이 적용 됩니다.

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Visual Studio에 열려 있을 때 Microsoft ASP.NET 및 웹 도구 2012.2 설치

Microsoft ASP.NET 및 웹 도구 2012.2 설치 하는 동안 VS가 열려 있으면 Visual Studio는 잘못 된 상태로 종료 될 수 있습니다. 사용자 설치를 계속 하기 전에 Visual Studio의 모든 인스턴스를 닫고는 것이 좋습니다.

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>설치 도중 ASP.NET 및 웹 도구 2012.2 설치 취소

ASP.NET 및 웹 도구 2012.2 취소 설치 도중 설치는 Visual Studio 잘못 된 상태에서 종료 됩니다. 다음이 단계에 따라가 문제를 해결를: 

- 프로그램 추가/제거로 이동
- 있는 경우 Microsoft ASP.NET 및 웹 도구 2012.2를 제거 합니다.
- Microsoft ASP.NET 및 Web Tools 2012.2 다시 설치

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>ASP.NET 및 웹 도구 2012.2 ASP.NET MVC 4를 제거한 후 템플릿 및 Razor v2 웹 사이트 템플릿이 없는

ASP.NET 및 웹 도구 2012.2 제거 해도 Visual Studio 2012에서는 모든 ASP.NET MVC 4 및 Razor v2 웹 사이트 템플릿을 제거도 됩니다.

ASP.NET MVC 4 및 Razor v2 웹 사이트 템플릿 다시 설치 하려면 Visual Studio 2012 설치를 복구 하려면이 문제를 해결 합니다.

### <a name="tooling-issues"></a>도구 문제

#### <a name="nuget-error-reported-during-project-creation"></a>프로젝트를 만드는 동안 오류가 NuGet

ASP.NET 및 웹 도구 2012.2를 설치한 후 표시 될 수 있는 MVC 4 프로젝트를 만들 때 다음 오류

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

ASP.NET 및 웹 도구 2012.2 NuGet 2.1을 함께 제공 되 고 Visual Studio 2012에서 확장을 업그레이드 합니다. 일부 경우에 VSIX 설치 관리자 VSIX를 올바르게 업데이트 되지 것입니다. 다음 단계를 사용 하면이 문제를 해결할 수 있습니다.

1. 관리자 권한으로 Visual Studio 2012 시작
2. 이동 도구-&gt;확장 및 업데이트 하 고 NuGet을 제거 합니다.
3. Visual Studio를 닫습니다.
4. ASP.NET 및 웹 도구 2012.2 설치 폴더로 이동 합니다.

    1. Visual Studio 2012: **Files\Microsoft ASP.NET\ASP.NET 웹 Stack\Visual Studio 2012 프로그램**
    2. Visual Studio 2012 Express for Web에 대 한: **Program Files\Microsoft ASP.NET\ASP.NET 웹 Stack\Visual Studio Express 2012 for Web**
5. NuGet을 다시 설치 하려면 NuGet.Tools.vsix를 두 번 클릭

### <a name="web-api-issues"></a>웹 API 문제

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>구문 분석 문제 $filter 및 날짜/시간 리터럴

OData URI 파서에서 부분 날짜/시간 리터럴을 올바르게 구문 분석 하지 못했습니다. 예를 들어 $filter 시작 ' 2012 eq 날짜/시간 =-12-31T12:00' 올바르게 구문 분석 하지 못했습니다. 전체 리터럴 $filter를 사용 하는 해결 방법을 시작 ' 2012 eq 날짜/시간 =-12-31T12:00:00'.

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData는 대/소문자 속성 이름을 지원 하지 않습니다.

OData는 OData 쿼리 및 odata 경로에서 대/소문자 속성 이름을 지원 하지 않습니다. 작업 항목을 참조 하세요.

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

사용자가 javascript 클라이언트 쪽 및 서버 쪽에서 대/소문자가는 것은이 문제가 발생 합니다. 이 문제는 odata 프로토콜의 의도적입니다. 그러나 많은 사용자가이 문제를 보고 합니다. 이 해결 하려면 사용자의 경우 url에서을 수정 해야 합니다.

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>기본 OData 라우팅 규칙은 탐색 속성에 대해 POST/PUT를 지원 하지 않습니다.

기본 OData 라우팅 규칙은 탐색 속성에 대해 POST/PUT를 지원 하지 않습니다. 작업 항목을 참조 하세요 [ http://aspnetwebstack.codeplex.com/workitem/366 ](http://aspnetwebstack.codeplex.com/workitem/366)합니다. 자주 사용 되는이 규칙이 기본 규칙에 누락 된 것입니다.

이 해결 하려면 사용자를 지원 하도록 새 라우팅 규칙을 확장 해야 합니다.

### <a name="facebook-template-issues"></a>Facebook 템플릿 문제

#### <a name="facebook-application-template-only-works-using-net-45"></a>.NET 4.5를 사용 하 여 Facebook 응용 프로그램 템플릿을 에서만 작동

ASP.NET MVC 4에서 Facebook 응용 프로그램 템플릿을 참조 하는 새 프로젝트 대화 상자의 framework 드롭다운 목록에서.NET 4.5를 선택 해야 합니다.

#### <a name="real-time-update-controller"></a>컨트롤러 실시간 업데이트

Facebook 응용 프로그램 템플릿을 쉽게 사용자 수 있도록 Facebook의 실시간 업데이트를 처리 하는 웹 API 컨트롤러를 만듭니다. NAT 뒤에 개발 컴퓨터 이면 컨트롤러 추가 네트워크 구성 없이 작동 하지 않습니다. 자세한 내용은 여기를 참조 하십시오. [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>Facebook OAuth 매개 변수를 사용 하 여 문자열 값이 충돌 하는 쿼리

다음 필드를 Facebook OAuth 대화의 호출을 사용 하 여 충돌 URL을 백업 합니다. 같은 이름의 고유한 쿼리 문자열 값을 추가 하지 마십시오: 코드, 오류, 오류\_설명, 오류\_이유입니다.

#### <a name="using-page-inspector-with-facebook-template"></a>Facebook 템플릿을 사용 하 여 페이지 검사기 사용

Facebook 응용 프로그램을 디버깅 하는 동안 Visual Studio 2012에서 페이지 검사기 기능을 사용할 수 없습니다. 페이지 검사기는 iframes를 현재 지원 하지 않습니다.

### <a name="single-page-application-template-issues"></a>단일 페이지 응용 프로그램 템플릿 문제

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>1.9/Knockout 2.2.1 업데이트, 기본 MVC SPA 프로젝트에 새 할 일 항목 편집을 실행 하는 경우 입력 JQuery를 사용 하 여 포커스 이벤트가 올바르게 처리 되지 않습니다.

JQuery 1.9/Knockout 2.2.1 사용 하 여 업데이트를 기본 MVC SPA 프로젝트를 실행 하는 경우 새 todo 항목 편집 입력 더 이상 포커스 새 todo 항목 편집 상자에 다시 할 일 목록에 새 할 일 항목을 입력 한 후.

해결 방법 참조 [ http://knockoutjs.com/documentation/hasfocus-binding.html ](http://knockoutjs.com/documentation/hasfocus-binding.html), 다음 샘플 코드와 유사한 수정 하 고:

Todo.model.js 파일  
 todolist(data) 함수를 추가 합니다. 다음:  
 **self.isSelected = ko.observable(false);**

todoList.prototype.addTodo 함수, 다음 blacked 텍스트를 추가 합니다.  
 **self.isSelected(true);**  
 self.newTodoTitle(&quot;&quot;);

Index.cshtml 파일 blacked 다음 텍스트를 추가 합니다.  
 &lt;데이터 바인딩 폼 =&quot;제출: addTodo&quot;&gt;  
 &lt;input class=&quot;addTodo&quot; type=&quot;text&quot; data-bind=&quot;value: newTodoTitle, placeholder: 'Type here to add', blurOnEnter: true, **hasfocus: isSelected**, event: { blur: addTodo }&quot; /&gt;  
 &lt;/form&gt;
