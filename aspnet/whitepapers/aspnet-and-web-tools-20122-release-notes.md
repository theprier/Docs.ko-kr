---
uid: whitepapers/aspnet-and-web-tools-20122-release-notes
title: "ASP.NET 및 웹 도구 2012.2 릴리스 정보 | Microsoft Docs"
author: rick-anderson
description: "ASP.NET 및 웹 도구 2012.2에 대 한 릴리스 정보입니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/14/2013
ms.topic: article
ms.assetid: bdb18d02-9f61-4676-836d-6fdea94f9282
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /whitepapers/aspnet-and-web-tools-20122-release-notes
msc.type: content
ms.openlocfilehash: e6c940aa507d72928d71019070ded5197458a763
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-and-web-tools-20122-release-notes"></a>릴리스 정보에 ASP.NET 및 Web Tools 2012.2
====================
> 이 문서는 ASP.NET 및 웹 도구 2012.2의 릴리스에 대해 설명합니다. Visual Studio Web Tooling 및 ASP.NET에 대 한 업데이트는


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

ASP.NET 및 Visual Studio 2012 용 웹 도구 2012.2를 사용해 설치 가능 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)합니다. 이것이 Visual Studio 2012 또는 Visual Studio Express 2012 for Web 필요 함에 대 한 업데이트입니다. 설치 된 Visual Studio가 Visual Studio Express 2012 for Web이 설치 됩니다.

또한 수동으로 설치할 수 있습니다 ASP.NET 및 웹 도구 2012.2 합니다. Visual Studio 2012 또는 Visual Studio Express 2012 for Web 설치 되어 있어야 합니다. 그런 다음 다음 지침을 따르세요. 

1. 다운로드 [ASP.NET 및 Frameworks 2012.2 웹](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) 다운로드 센터에서 설치 관리자입니다.
2. 경우 입력 정보를 요청 실행을 클릭 합니다. 또한 나중에 실행 파일을 저장할 수 있습니다.
3. 업데이트 하 여 Visual Studio의 버전을 확인 합니다. 이렇게 하려면을 업데이트 하려면 Visual Studio를 실행 합니다. 도움말 메뉴 항목을 클릭 합니다.   
    ![](aspnet-and-web-tools-20122-release-notes/_static/image1.jpg)
4. 메뉴 항목 표시 되 면 &quot;에 대 한 Microsoft Visual Studio 2012 for Web&quot; 다음 다운로드 [웹 개발자 도구 2012.2-Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkID=282228)합니다. 그렇지 않은 경우 다운로드 [웹 개발자 도구 2012.2-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)합니다.
5. 경우 입력 정보를 요청 실행을 클릭 합니다. 또한 나중에 실행 파일을 저장할 수 있습니다.

> [!NOTE]
> ASP.NET 및 웹 도구 2012.2 릴리스는 SQL Server Data Tools를 포함 하지 않습니다. SQL Server와 Windows Azure SQL 데이터베이스에는 다양 한 데이터베이스 프로젝트 기반 오프 라인으로 개발, 스키마 비교 및 향상 된 데이터베이스 배포 기능을 포함 하 여 도구를 제공 합니다. 자세한 내용을 보거나 SQL Server Data Tools를 설치 하려면 방문 [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)합니다.

<a id="_Documentation"></a>
## <a name="documentation"></a>설명서

자습서 및 ASP.NET 및 웹 도구 2012.2 하는 방법에 대 한 기타 정보는 ASP.NET 웹 사이트 (https://www.asp.net)에서 사용할 수 있습니다.

<a id="_Support"></a>
## <a name="support"></a>지원

ASP.NET 및 웹 도구 2012.2는 공식적으로 출시 되어 지원 합니다. 일반적인 지원 채널을 사용할 수 있습니다. ASP.NET 포럼에 질문을 게시할 수도 있습니다 ([https://forums.asp.net/](https://forums.asp.net/))에서 ASP.NET 커뮤니티의 회원과 비공식적인 지원을 제공할 수 있는 경우가 많습니다.

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

ASP.NET 및 웹 도구 2012.2 Visual Studio 2012 또는 Visual Studio Express 2012 for Web 필요 합니다.

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>ASP.NET 및 Web Tools 2012.2의 새로운 기능

이 섹션에는 ASP.NET 및 웹 도구 2012.2 릴리스에서 도입 된 기능에 설명 합니다.

<a id="_Tooling"></a>
### <a name="tooling"></a>도구

- 페이지 검사기 

    - 페이지 검사기를 페이지에 해당 하는 JavaScript 코드에 동적으로 추가 된 항목에 매핑할 수 있도록 하는 JavaScript 선택 매핑을 지원 합니다.
    - CSS를 볼 수 있는 기능을 실시간으로 업데이트 합니다.
    - 자세한 내용은 [CSS 자동 동기화 및 JavaScript 페이지 검사기의 매핑 선택](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)합니다.
- 편집기 

    - CoffeeScript, Mustache, 핸들, 및 JsRender에 대 한 구문 강조 표시를 지원 합니다.
    - HTML 편집기 Knockout 바인딩에 대 한 Intellisense를 제공합니다.
    - 덜 편집 및 컴파일러 작은 사용 하 여 동적 CSS 빌드 수 있도록 지원 합니다.
    - JSON.NET 클래스로 붙여넣기 합니다. 이 특수 붙여넣기 명령을에 붙여넣은 다음 JSON C# 또는 VB.NET 코드 파일을 Visual Studio를 사용 하 여 JSON에서 유추 하는.NET 클래스를 자동으로 생성 됩니다.
- VSIX로 제 3 자 에뮬레이터를 설치할 수 있도록 확장성 후크를 추가 하는 모바일 에뮬레이터 지원 합니다. 설치 된 에뮬레이터에에서 표시 됩니다 F5 드롭다운 개발자가 다양 한 모바일 장치에서 웹 사이트를 미리 볼 수 있습니다. Scott Hanselman의 블로그 항목에서이 기능에 대해 자세히 읽어보세요 [Visual Studio와 함께 새 BrowserStack 통합](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)합니다.

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>웹 게시

- 웹 사이트 프로젝트는 이제 Windows Azure 웹 사이트에 게시를 포함 하 여 웹 응용 프로그램 프로젝트와 동일한 게시 환경을가지고 있습니다.
- 선택적 게시 &#8211; 하나 이상의 파일에 대 한 (웹 배포 끝점에 게시) 한 후 다음 작업을 수행할 수 있습니다. 

    - 선택한 파일을 게시 합니다.
    - 로컬 파일 및 원격 파일 간의 차이 참조 하십시오.
    - 로컬 파일 원격 파일을 업데이트 하거나 원격 파일 로컬 파일을 업데이트 합니다.

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET MVC 템플릿

- 새로운 Facebook 응용 프로그램 템플릿 덕분에 Facebook Canvas 쉽게 응용 프로그램을 작성 합니다. 몇 가지 간단한 단계에서에서 로그인된 한 사용자 데이터를 가져오고 자신의 친구와 통합 하는 Facebook 응용 프로그램을 만들 수 있습니다. 서식 파일에는 인증, 사용 권한, Facebook 데이터 액세스를 포함 하 여 Facebook 응용 프로그램 작성과 관련 된 모든 배관을 처리 하기 위한 새 라이브러리가 포함 됩니다. Facebook 응용 프로그램 템플릿을 사용 하 여 대 한 자세한 내용은 참조 [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)합니다.
- 새로운 단일 페이지 응용 프로그램 MVC 템플릿을 HTML 5, CSS 3 Knockout 및 jQuery JavaScript 라이브러리를 ASP.NET Web API를 사용 하 여 대화형 클라이언트 쪽 웹 앱을 만들 수가 있습니다. 서식 파일에 RESTful 서버 API를 사용 하는 JavaScript HTML5 응용 프로그램을 작성 하기 위한 일반적인 방법을 보여 주는 "todo" 목록 응용 프로그램에 포함 됩니다. 자세히 알아볼 수 있습니다 [https://www.asp.net/single-page-application](../single-page-application/index.md)합니다.
- 이제 ASP.NET MVC 새 프로젝트 대화 상자에 새 템플릿을 추가 하는 VSIX를 만들 수 있습니다. 자세한 내용은: [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- FixedDisplayModes 패키지 &#8211; MVC 프로젝트 템플릿은 MVC 4의 버그에 대 한 해결책을 포함 하는 새 'FixedDisplayModes' NuGet 패키지를 포함 하도록 업데이트 되었습니다. 패키지에 포함 된 수정에 관한 자세한 내용은이 블로그 게시물을 참조 ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) MVC 팀에서.

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET Web API와 여러 가지 새로운 기능이 향상 되었습니다.

- ASP.NET Web API OData
- ASP.NET Web API 추적
- ASP.NET Web API 도움말 페이지

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

ASP.NET Web API OData 모든 데이터 소스를 통해 다양 한 비즈니스 논리를 사용 하 여 OData 끝점을 만들어야 하는 유연성을 제공 합니다. ASP.NET Web API OData와 OData 의미 체계를 노출 하려는 양을 제어할 수 있습니다. ASP.NET Web API OData ASP.NET MVC 4 프로젝트 템플릿이 함께 제공 포함 되며 NuGet에서 제공 됩니다 ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)).

ASP.NET Web API OData는 현재 다음과 같은 기능을 지원합니다.

- [Queryable] 특성을 적용 하 여 OData 쿼리 의미 체계를 사용 합니다.
- 쉽게 OData 쿼리의 유효성을 검사 하 고 지원 되는 쿼리 옵션, 연산자 및 함수는 집합을 제한 합니다.
- 매개 변수는 다음 검증 하 고 IQueryable 또는 IEnumerable에 적용 하는 쿼리의 추상 구문 트리 표현을 가져오는에 직접 ODataQueryOptions에 바인딩합니다.
- [Queryable] 특성에서 결과 한도 지정 하 여 서비스 기반 페이징 및 다음 페이지 링크 생성을 설정 합니다.
- $Inlinecount을 사용 하 여 일치 하는 리소스의 총 수에 대 한 인라인된 카운트를 요청 합니다.
- Null 전파를 제어 합니다.
- $Filter의 일부/모든 연산자입니다.
- 규칙에 따라 엔터티 데이터 모델을 유추 하거나 명시적으로 유사한를 Entity Framework 코드 중심 방식으로 모델을 사용자 지정 합니다.
- 노출 엔터티 EntitySetController에서 파생 하 여 설정 합니다.
- 탐색 속성을 노출, 링크를 조작할 OData 작업을 구현 하기 위한 간단 하 고 사용자 지정 가능한 규칙입니다.
- MapODataRoute 확장 메서드를 사용 하 여 라우팅을 간소화 합니다.
- 여러 개의 EDM 모델을 노출 하 여 버전 관리를 지원 합니다.
- 서비스 문서와 표시 $metadata 클라이언트 (.NET, Windows Phone, Windows 스토어 등)를 생성할 수 있도록 웹 API에 대 한 됩니다.
- 자세한 정보 표시 형식을 OData Atom, JSON 및 JSON에 대 한 지원 합니다.
- 만들기, 업데이트, 부분적으로 업데이트 (PATCH) 및 엔터티를 삭제 합니다.
- 쿼리하고 엔터티 간의 관계를 조작 합니다.
- 경로 연결 하는 관계 링크를 만듭니다.
- 복합 형식
- 엔터티 형식 상속 합니다.
- 컬렉션 속성입니다.
- 열거형입니다.
- OData 작업입니다.
- WCF Data Services, 즉 ODataLib와 동일한 기반을 기반으로 구축 ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)).

ASP.NET Web API OData에 대 한 자세한 내용은 참조 [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)합니다.

#### <a name="aspnet-web-api-tracing"></a>ASP.NET Web API 추적

ASP.NET Web API 추적.NET 추적 웹 Api에서에서 추적 데이터를 통합합니다. 이제 Web API 프로젝트 템플릿에 기본적으로 설정 됩니다. 웹에 대 한 데이터 추적 Api 출력 창에 전송 및 IntelliTrace를 통해 사용할 수 있습니다. ASP.NET Web API Tracing 하면 Web API와의 통합을 통해 Windows Azure에서 호스팅되는 경우에 대 한 추적 정보 [Windows Azure 진단](https://msdn.microsoft.com/en-us/library/windowsazure/hh411529.aspx)합니다. 또한 설치 하 고 ASP.NET 웹 API 추적 NuGet 패키지를 사용 하 여 모든 응용 프로그램에서 ASP.NET 웹 API 추적 기능을 활성화 수 ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)).

구성 및 ASP.NET Web API Tracing 사용에 대 한 자세한 내용은 참조 [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)합니다.

#### <a name="aspnet-web-api-help-page"></a>ASP.NET Web API 도움말 페이지

이제 ASP.NET Web API 도움말 페이지는 웹 API 프로젝트 템플릿에 기본적으로 포함 됩니다. ASP.NET 웹 API 도움말 페이지는 웹 HTTP 끝점, 지원 되는 HTTP 방법, 매개 변수 및 예제 요청 및 응답 메시지 페이로드를 포함 하 여 Api에 대 한 설명서를 자동으로 생성 합니다. 문서는 자동으로 코드의 주석에서 찾아볼 수 있습니다. ASP.NET 웹 API 도움말 페이지 NuGet 패키지를 사용 하 여 응용 프로그램에 ASP.NET 웹 API 도움말 페이지를 추가할 수도 있습니다 ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)).

설정 및 ASP.NET 웹 API 도움말 페이지 참조를 사용자 지정에 대 한 자세한 내용은 [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)합니다.

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR 쉽게 실시간 웹 기능 ASP.NET 응용 프로그램을 추가할 수 있는 경우 Websocket을 사용 하 고 자동으로 대체 하기 명시 된 기타 기술을 그렇지 않을 경우 있습니다.

ASP.NET SignalR을 사용 하 여 대 한 자세한 내용은 참조 [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)합니다.

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>Asp.net Url

ASP.NET FriendlyURLs를 사용 하면 수행 되는 클리너 (.aspx 확장명 없음) Url을 찾고 생성 하려면 web forms 개발자가 매우 쉬워집니다. No로 적은 구성이 필요로 하며 기존 ASP.NET v4.0 응용 프로그램과 함께 사용할 수 있습니다. 또한 FriendlyURLs 기능을 사용 하면 보다 쉽게 지원 데스크톱 및 모바일 뷰 간을 전환 하 여 해당 응용 프로그램에 모바일 지원을 추가 하는 개발자를 위한 합니다.

설치 및 ASP.NET Url 사용에 대 한 자세한 내용은 참조 [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)합니다.

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진된 문제 및 주요 변경 내용

이 섹션에는 알려진된 문제 및 ASP.NET 및 웹 도구 2012.2 릴리스에 주요 변경 내용을 설명 합니다.

### <a name="installation-issues"></a>설치 문제

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>Visual Studio 2012의 순서가 설치

복구 작업에서는 ASP.NET 및 웹 도구 2012.2 설치 후에 추가 SKU의 Visual Studio 2012를 설치 합니다. 다음 순서를 고려 합니다.

1. Visual Studio 2012 Express for Web을 설치
2. ASP.NET 및 Web Tools 2012.2 설치
3. Visual Studio 2012 Professional, Premium 또는 Ultimate를 설치 합니다.

2 단계 Express for Web 용 업데이트 설치만 발생 합니다. 3 단계 중에 설치 하는 SKU 업데이트가 포함 되어 있는지 확인 하려면 설치 된 마지막 SKU에 대 한 업데이트를 설치 하려면 ASP.NET 및 웹 도구 2012.2 복구 해야 합니다. 또한 1 단계에서에서 Sku 및 3이 반대로 하는 경우이 적용 됩니다.

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Visual Studio를 열면 Microsoft ASP.NET 및 웹 도구 2012.2 설치

Microsoft ASP.NET 및 웹 도구 2012.2 설치 하는 동안 VS 열려 있으면 Visual Studio이 잘못 된 상태에 생길 수 있습니다. 사용자가 설치를 계속 하기 전에 Visual Studio의 모든 인스턴스를 닫고는 것이 좋습니다.

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>설치 도중에 ASP.NET 및 웹 도구 2012.2 설치 취소

ASP.NET 및 웹 도구 2012.2 취소 설치 도중에 설치는 Visual Studio 잘못 된 상태에서 종료 됩니다. 다음이 단계에 따라가 문제를 해결: 

- 프로그램 추가/제거로 이동
- Microsoft ASP.NET 및 웹 도구 2012.2 제거 있는 경우.
- Microsoft ASP.NET 및 Web Tools 2012.2 다시 설치

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>ASP.NET 및 웹 도구 2012.2 ASP.NET MVC 4를 제거한 후 템플릿과 Razor v2 웹 사이트 서식 파일은 누락

ASP.NET 및 웹 도구 2012.2 제거도 제거 됩니다 ASP.NET MVC 4 및 Razor v2 웹 사이트 서식 파일 모두 Visual Studio 2012에서.

ASP.NET MVC 4 및 Razor v2 웹 사이트 서식 파일을 다시 설치 하려면 Visual Studio 2012 설치를 복구 해야이 문제를 해결 합니다.

### <a name="tooling-issues"></a>도구 문제

#### <a name="nuget-error-reported-during-project-creation"></a>프로젝트를 만드는 동안 보고 된 NuGet 오류

ASP.NET 및 웹 도구 2012.2 설치 후 표시 될 수 있는 MVC 4 프로젝트를 만들 때 다음 오류

![](aspnet-and-web-tools-20122-release-notes/_static/image1.png)

ASP.NET 및 웹 도구 2012.2 NuGet 2.1을 함께 제공 하 고 Visual Studio 2012에서 확장을 업그레이드 합니다. 경우에 따라 VSIX 설치 VSIX를 올바르게 업데이트 되지 것입니다. 다음 단계를 사용 하면이 문제를 해결할 수 있습니다.

1. 관리자 권한으로 Visual Studio 2012 시작
2. 도구-이동&gt;확장명 및 업데이트 NuGet을 제거 합니다.
3. Visual Studio를 닫습니다.
4. ASP.NET 및 웹 도구 2012.2 설치 폴더로 이동 합니다.

    1. Visual Studio 2012: **Files\Microsoft ASP.NET\ASP.NET 웹 Stack\Visual Studio 2012 프로그램**
    2. Visual Studio 2012 Express for Web 용: **Program Files\Microsoft ASP.NET\ASP.NET 웹 Stack\Visual Studio Express 2012 for Web**
5. NuGet을 다시 설치 하려면 NuGet.Tools.vsix을 두 번 클릭

### <a name="web-api-issues"></a>Web API 문제

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>날짜/시간 리터럴 $filter의 문제를 구문 분석

OData URI 파서에서 부분 datetime 리터럴이 올바르게 구문 분석 되지 않습니다. 예를 들어 $filter = 시작 eq 날짜/시간 ' 2012-12-31T12:00' 제대로 구문 분석에 실패 합니다. 해결 방법이 전체 리터럴 $filter를 사용 하는 것 = 시작 eq 날짜/시간 ' 2012-12-31T12:00:00'.

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData는 대/소문자 속성 이름을 지원 하지 않습니다.

OData는 OData 쿼리 및 odata 경로에 대/소문자 속성 이름을 지원 하지 않습니다. 작업 항목을 참조 하십시오.

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

사용자가 javascript 클라이언트 쪽 및 서버 쪽에 서로 다른 대/소문자가이 문제 때문일 수 도달할 됩니다. 이 문제는 odata 프로토콜에 의도적입니다. 그러나 많은 사용자가이 문제를 보고 합니다. 이 해결 하려면 사용자의 경우 URL에 해결 해야 합니다.

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>기본 OData 라우팅 규칙 탐색 속성에 대해 POST/PUT을 지원 하지 않습니다.

기본 OData 라우팅 규칙 탐색 속성에 대해 POST/PUT을 지원 하지 않습니다. 작업 항목을 참조 [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)합니다. 기본 규칙에서이 자주 사용 되는 규칙을 누락 됩니다.

이 해결 하려면 사용자를 지원 하기 위한 새 경로 규칙을 확장 해야 합니다.

### <a name="facebook-template-issues"></a>Facebook 템플릿 문제

#### <a name="facebook-application-template-only-works-using-net-45"></a>.NET 4.5를 사용 하 여 Facebook 응용 프로그램 템플릿만 작동

ASP.NET MVC 4에 Facebook 응용 프로그램 템플릿이 새 프로젝트 대화 상자에 프레임 워크 드롭다운 목록에서.NET 4.5를 선택 해야 합니다.

#### <a name="real-time-update-controller"></a>컨트롤러 실시간 업데이트

Facebook 응용 프로그램 템플릿은 사용자를 쉽게 있습니다 facebook에서 실시간 업데이트를 처리 하도록 Web API 컨트롤러를 만듭니다. 개발 컴퓨터 NAT 뒤에 있는 포함 된 경우 컨트롤러 추가 네트워크 구성 없이도 작동 하지 않습니다. 자세한 내용은 여기를 참조 하십시오.: [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>Facebook OAuth 매개 변수가 있는 문자열 값이 충돌 하는 쿼리

Facebook OAuth 대화 호출와 충돌 하는 다음 필드가 URL을 백업 합니다. 다음과 같은 이름의 사용자 고유의 쿼리 문자열 값을 추가 하지 마십시오: 코드, 오류, 오류\_설명, 오류\_이유입니다.

#### <a name="using-page-inspector-with-facebook-template"></a>페이지 검사기를 사용 하 여 Facebook 템플릿을 사용 하 여

Facebook 응용 프로그램을 디버깅 하는 동안 Visual Studio 2012에서 페이지 검사기 기능을 사용할 수 없습니다. 페이지 검사기 iframe 현재 지원 되지 않습니다.

### <a name="single-page-application-template-issues"></a>단일 페이지 응용 프로그램 템플릿 문제

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>JQuery 1.9/Knockout 2.2.1 업데이트를 기본 MVC SPA 프로젝트에 새 할 일 항목 편집을 실행할 때 입력 된 포커스 이벤트가 올바르게 처리 되지 않습니다.

JQuery 1.9/Knockout 2.2.1 업데이트을 기본 MVC SPA 프로젝트를 실행할 때 새 할 일 항목 편집 입력 더 이상 포커스 새 할 일 항목 편집 상자에 다시 할 일 목록에 새 할 일 항목을 입력 한 후 합니다.

해결 방법 참조 [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html), 다음 샘플 코드에 비슷한 수정 확인:

파일 todo.model.js  
 todolist(data) 함수, 추가 다음:  
 **self.isSelected ko.observable(false); =**

todoList.prototype.addTodo 함수 blacked 다음 텍스트를 추가 합니다.  
 **self.isSelected(true);**  
 self.newTodoTitle (&quot;&quot;);

Index.cshtml 파일 blacked 다음 텍스트를 추가 합니다.  
 &lt;데이터 바인딩 폼 =&quot;제출: addTodo&quot;&gt;  
 &lt;클래스를 입력 =&quot;addTodo&quot; 유형 =&quot;텍스트&quot; 데이터 바인딩 =&quot;값: newTodoTitle, 자리 표시자: '여기에 형식을 추가 하려면', blurOnEnter: true 이면 **hasfocus: isSelected**, 이벤트: {흐림: addTodo}&quot; /&gt;  
 &lt;/form&gt;
