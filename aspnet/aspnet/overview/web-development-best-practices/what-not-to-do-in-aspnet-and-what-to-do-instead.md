---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: ASP.NET에서 안 되 고 대신 | Microsoft Docs
author: Rick-Anderson
description: 이 항목에서는 ASP.NET 웹 프로젝트 내에서 사용자를 확인 하는 몇 가지 일반적인 실수를 설명 합니다. 무엇을 해야 이러한 공용을 방지 하기 위한 권장 사항을 제공 하는 중...
ms.author: riande
ms.date: 05/08/2014
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 69040ca6a1ddeaf029062da45475dd2171b1afa6
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021445"
---
<a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a>ASP.NET에서 안 되 고 대신
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 항목에서는 ASP.NET 웹 프로젝트 내에서 사용자를 확인 하는 몇 가지 일반적인 실수를 설명 합니다. 이러한 일반적인 실수를 방지 하려면 수행 해야 하는 것에 대 한 권장 사항을 제공 합니다. 기반이 되는 [프레젠테이션](http://vimeo.com/68390507) 하 여 **Damian Edwards** 노르웨이 개발자 회의에서.


## <a name="disclaimer"></a>고지 사항

이 항목에서는 없습니다 완전 한 가이드로 안전 하 고 효율적인 응용 프로그램을 확인 합니다. 이 항목에서 설명 하지는 보안 및 성능에 대 한 모범 사례를 수행 해야 합니다. 만.NET 클래스 및 프로세스와 관련 된 일반적인 실수를 방지 하는 방법을 제안 합니다.

## <a name="overview"></a>개요

이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [표준 준수](#standards)

    - [컨트롤 어댑터](#adapters)
    - [컨트롤의 스타일 속성](#styleprop)
    - [페이지 및 컨트롤 콜백을](#callback)
    - [브라우저 기능 검색](#browsercap)
- [보안](#security)

    - [요청 유효성 검사](#validation)
    - [쿠키 없는 폼 인증 및 세션](#cookieless)
    - [EnableViewStateMac](#viewstatemac)
    - [보통 신뢰](#medium)
    - [&lt;appSettings&gt;](#appsettings)
    - [UrlPathEncode](#urlpathencode)
- [안정성 및 성능](#performance)

    - [PreSendRequestHeaders 및 PreSendRequestContent](#presend)
    - [Web Forms 사용 하 여 비동기 페이지 이벤트](#asyncevents)
    - [실행 후 제거 작업](#fire)
    - [요청 엔터티 본문](#requestentity)
    - [Response.Redirect 및 Response.End](#redirect)
    - [EnableViewState 및 ViewStateMode](#viewstatemode)
    - [SqlMembershipProvider](#sqlprovider)
    - [긴 실행 요청 (> 110 초)](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a>표준 준수

<a id="adapters"></a>

### <a name="control-adapters"></a>컨트롤 어댑터

권장 사항: 적응형 렌더링에 대 한 컨트롤 어댑터를 사용 하 여 중지 하 고 대신 표준 규격 HTML 및 CSS 미디어 쿼리를 사용 하 여 키를 누릅니다.

컨트롤 어댑터는 다양 한 장치 및 환경에 대 한 사용자 지정 된 프레젠테이션 코드를 렌더링 하는.NET 2.0에서 도입 되었습니다. 이제이 적응형 렌더링 CSS 및 HTML을 사용 하 여 수행할 수 있습니다. 컨트롤 어댑터 사용을 중지 하 고 기존 어댑터를 모두 CSS 및 HTML을 변환 해야 합니다.

자세한 내용은 [미디어 쿼리](http://www.w3.org/TR/css3-mediaqueries/) 하 고 [How To: Your ASP.NET Web Forms에 모바일 페이지 추가 / MVC 응용 프로그램](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md)합니다.

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a>컨트롤의 스타일 속성

권장 사항: 중지 컨트롤 태그에 스타일 값을 설정 하 고 대신 CSS 스타일 시트에서 형식 지정 값을 설정 키를 누릅니다.

웹 서버 컨트롤에는 수십 개의 인라인 스타일 속성을 설정 하는 속성이 포함 됩니다. 예를 들어, ForeColor 속성을 컨트롤에 대 한 텍스트의 색을 설정합니다. CSS 스타일 시트를 통해 더 효율적으로이 동일한 효과 수행할 수 있습니다. 스타일 시트를 사용 하 여 스타일 값을 중앙 집중화 하 고 응용 프로그램 전체에서 이러한 값을 설정 하지 마십시오 수 있습니다.

다음 예제에서는 빨간색 집합 텍스트 CSS 클래스를 보여 줍니다.

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

다음 예제에는 CSS 클래스를 동적으로 적용 하는 방법을 보여 줍니다.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a>페이지 및 컨트롤 콜백을

권장 사항: 페이지 및 컨트롤 콜백을 사용을 중지 하 고 대신 다음 중 하나를 사용 하 여: AJAX, UpdatePanel, MVC 동작 메서드, 웹 API 또는 SignalR 합니다.

이전 버전의 ASP.NET 페이지 및 컨트롤의 콜백 메서드를 사용 전체 페이지를 새로 고치지 않고 웹 페이지의 일부를 업데이트할 수 있습니다. 이제을 통해 부분 페이지 업데이트를 수행할 수 있습니다 [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx)합니다 [MVC](../../../mvc/index.md)를 [Web API](../../../web-api/index.md) 또는 [SignalR](../../../signalr/index.md). 라우팅 및 친숙 한 Url을 사용 하 여 문제가 발생할 수 있으므로 콜백 메서드를 사용 하 여 중지 해야 합니다. 기본적으로 컨트롤에 콜백 메서드를 사용 하지 마십시오 있지만 컨트롤에서이 기능을 사용 하도록 설정한 경우에 해제 해야 합니다.

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a>브라우저 기능 검색

권장 사항: 정적 브라우저 기능 감지를 사용 하 여 중지 하 고 대신 동적 기능 감지를 사용 하 여 키를 누릅니다.

이전 버전의 ASP.NET에서는 각 브라우저에 대해 지원 되는 기능의 XML 파일에 저장 되었습니다. 정적 조회를 통해 검색 기능이 가장 좋은 방법은 아닙니다. 이제 검색할 수 있습니다 동적으로 브라우저에서 같은 기능 검색 프레임 워크를 사용 하 여 지 원하는 기능 [Modernizr](http://modernizr.com/)합니다. 기능 검색 메서드 또는 속성을 사용 하려고 하 고 브라우저에 원하는 결과 생성 하는 경우 참조를 확인 하 여 지원을 결정 합니다. 기본적으로 Modernizr 웹 응용 프로그램 템플릿에 포함 됩니다.

<a id="security"></a>

## <a name="security"></a>보안

<a id="validation"></a>

### <a name="request-validation"></a>요청 유효성 검사

권장 사항: 사용자 입력의 유효성을 검사 하 고 사용자의 출력을 인코딩하십시오.

요청 유효성 검사에는 각 요청을 검사 하 고 인식 된 위협이 발견 된 경우 요청을 중지 하는 ASP.NET의 기능입니다. 사이트 간 스크립팅 공격 으로부터 응용 프로그램을 보호 하는 것에 대 한 요청 유효성 검사에 종속 되지 않습니다. 대신, 사용자의 모든 입력의 유효성을 검사 하 고 출력을 인코딩하십시오. 일부 제한 된 경우에 정규식을 사용 하 여 입력의 유효성을 검사 하지만 유효성을 검사 해야 하는 더 복잡 한 경우에서 사용자 입력 값과 일치 하는 경우를 결정 하는.NET 클래스를 사용 하 여 허용 되는 값입니다.

다음 예제에서는 Uri 클래스의 정적 메서드를 사용 하 여 사용자가 제공 된 Uri의 유효한 지 여부를 결정 하는 방법을 보여 줍니다.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

그러나 Uri를 충분히 확인 하는 경우에 확인 해야 지정 되도록 `http` 또는 `https`합니다. 다음 예제에서는 인스턴스 메서드를 사용 하 여 Uri가 유효한 지 확인 합니다.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

사용자 입력을 포함 하 여 SQL 쿼리에서 또는 HTML로 사용자 입력을 렌더링 하기 전에 악성 코드가 포함 되지 않도록 하려면 값을 인코딩하십시오.

HTML을 수 있습니다 사용 하 여 태그의 값을 인코딩하는 &lt;%: %&gt; 아래와 같이 구문입니다.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

HTML Razor 구문에서를 사용 하 여 인코딩하 @ 아래 표시 된 것 처럼.

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

다음 예제에 나와 있는 어떻게 HTML로 인코딩 코드 숨김에 있는 값입니다.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

SQL 명령에 대 한 값을 안전 하 게 인코딩 명령 매개 변수 같은 사용 합니다 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)합니다. <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a>쿠키 없는 폼 인증 및 세션

권장 사항: 쿠키 필요 합니다.

쿼리 문자열의 인증 정보를 전달 안전 하지 않습니다. 따라서 응용 프로그램 인증을 포함 하는 경우에 쿠키를 필요 합니다. 중요 한 정보를 저장 하는 쿠키가, 경우에 쿠키에 SSL을 필요로 하는 것이 좋습니다.

다음 예제에서는 폼 인증에서는 SSL을 통해 전송 되는 쿠키를 해야 하는 Web.config 파일에서 지정 하는 방법을 보여 줍니다.

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a>EnableViewStateMac

권장 사항: 되지 false로 설정 합니다.

기본적으로 EnbableViewStateMac 설정을 true로 합니다. 응용 프로그램 뷰 상태에 사용 하지 않는 경우에 EnableViewStateMac를 false로 설정 하지 마십시오. 이 값을 false로 설정 하 게 응용 프로그램 사이트 간 스크립팅에 취약 합니다.

ASP.NET 4.5.2부터 런타임에서 적용 **EnableViewStateMac = true**합니다. False로 설정 하는 경우에 런타임은이 값을 무시 하 고 true로 설정 된 값으로 진행 됩니다. 자세한 내용은 [ASP.NET 4.5.2 및 EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx)합니다.

다음 예제에서는 EnableViewStateMac true로 설정 하는 방법을 보여 줍니다. 실제로이 값을 기본적으로 true 이기 때문에 true로 설정할 필요가 없습니다. 그러나 설정한 경우이 false로 아무 페이지에서 응용 프로그램에서이 값을 즉시 수정 해야 합니다.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a>보통 신뢰

권장 사항: 보안 경계로 서 보통 신뢰 (또는 다른 신뢰 수준)에 종속 되지 않습니다.

부분 신뢰 응용 프로그램을 적절 하 게 보호 하지 않습니다 하 고 사용할 수 없습니다. 대신 완전 신뢰를 사용 하 고 별도 응용 프로그램 풀에서 신뢰할 수 없는 응용 프로그램을 격리 합니다. 또한 각 응용 프로그램 풀을 고유 id를 실행 합니다. 자세한 내용은 [부분 신뢰 ASP.NET 응용 프로그램 격리를 보장 하지 않습니다](https://support.microsoft.com/kb/2698981)합니다.

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a>&lt;appSettings&gt;

권장 사항:의 보안 설정 안 &lt;appSettings&gt; 요소입니다.

AppSettings 요소는 보안 업데이트에 필요한 많은 값을 포함 합니다. 하지 변경 하거나 이러한 값을 사용 하지 않도록 설정 해야 합니다. 업데이트를 배포할 때 이러한 값을 사용 하지 않도록 해야, 즉시 다시 사용 하도록 설정 배포를 완료 합니다.

자세한 내용은 참조 하세요 [ASP.NET appSettings 요소](https://msdn.microsoft.com/library/hh975440.aspx)합니다.

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a>UrlPathEncode

권장 사항: 사용 [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) 대신 합니다.

UrlPathEncode 메서드는 매우 구체적인 브라우저 호환성 문제를 해결 하려면.NET Framework에 추가 되었습니다. URL을 적절 하 게 암호화 하지 않습니다 하 고 응용 프로그램에서 사이트 간 스크립팅 보호 하지 않습니다. 되지 응용 프로그램에서 사용 해야 합니다. 대신 [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx)합니다.

다음 예제에서는 인코딩된 URL 하이퍼링크 컨트롤에 대 한 쿼리 문자열 매개 변수로 전달 하는 방법을 보여 줍니다.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a>안정성 및 성능

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a>PreSendRequestHeaders 및 PreSendRequestContent

권장 사항: 관리 되는 모듈을 사용 하 여 이러한 이벤트를 사용 하지 마십시오. 대신, 필요한 작업을 수행 하는 네이티브 IIS 모듈을 작성 합니다. 참조 [네이티브 코드 HTTP 모듈을 만드는](https://msdn.microsoft.com/library/ms693629.aspx)합니다.

사용할 수는 [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) 하 고 [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) 네이티브 IIS 모듈을 사용 하 여 이벤트입니다.
> [!WARNING]
> 사용 하지 마세요 `PreSendRequestHeaders` 하 고 `PreSendRequestContent` 구현 하는 관리 되는 모듈을 사용 하 여 `IHttpModule`입니다. 이러한 속성을 설정 하면 비동기 요청을 사용 하 여 문제가 발생할 수 있습니다. 응용 프로그램 요청 라우팅 (ARR) 및 websocket의 조합을 w3wp 충돌을 일으킬 수 있는 액세스 위반 예외가 발생할 수 있습니다. 예를 들어 iiscore! W3_CONTEXT_BASE::GetIsLastNotification + 68 iiscore.dll에서 액세스 위반 예외 (0xC0000005) 발생 했습니다.

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a>Web Forms 사용 하 여 비동기 페이지 이벤트

권장 사항: Web Forms에서 페이지 수명 주기 이벤트에 대 한 void 메서드 비동기 쓰기를 방지 하 고 대신 [Page.RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) 비동기 코드에 대 한 합니다.

페이지 이벤트를 표시 하는 시점 **비동기** 하 고 **void**, 비동기 코드는 완료 된 시기를 확인할 수 없습니다. 완료를 추적할 수 있는 방식으로 비동기 코드를 실행 하려면 Page.RegisterAsyncTask를 대신 사용 합니다.

단추는 다음 예제에서는 비동기 코드를 포함 하는 처리기를 클릭 합니다. 이 예에서는 권장 아닌 비동기 작업의 간단한 예제로만 제공 하는 문자열 값을 비동기적으로 읽는 포함 됩니다.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

비동기 작업을 사용 하는 경우는 Web.config 파일에서 4.5로 Http 런타임 대상 프레임 워크를 설정 합니다. 대상 프레임 워크를 설정을 4.5으로 설정 하면 새 동기화 컨텍스트에서.NET 4.5에 추가 되었습니다. 이 값은 기본적으로 Visual Studio 2012의 새 프로젝트에서 설정 되지만 되지 설정 기존 프로젝트를 사용 하 여 작업 하는 경우.

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a>실행 후 제거 작업

권장 사항: asp.net 요청을 처리할 때 시작 하지 않고 실행 후 제거 작업 (이러한 ThreadPool.QueueUserWorkItem 메서드 호출 또는 반복적으로 대리자를 호출 하는 타이머를 만드는).

응용 프로그램에 ASP.NET에서 실행 되는 실행 후 제거 작업을 하는 경우 응용 프로그램 동기화를 가져올 수 있습니다. 언제 든 지 응용 프로그램 도메인을 제거할 수 없습니다. 즉, 진행 중인 프로세스는 더 이상 응용 프로그램의 현재 상태를 일치 시킬 수 없습니다.

이 유형의 ASP.NET 외부에서 작업을 이동 해야 합니다. 진행 중인 작업을 수행 하는 데 Azure의 웹 작업, Windows 서비스 또는 작업자 역할을 사용 하 고 다른 프로세스에서 해당 코드를 실행할 수 있습니다.

Asp.net이 작업을 수행 해야 하는 경우 라는 Nuget 패키지를 추가할 수 있습니다 [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) 코드를 실행 합니다.

<a id="requestentity"></a>

### <a name="request-entity-body"></a>요청 엔터티 본문

권장 사항: 처리기의 이벤트를 실행 하기 전에 Request.Form 또는 Request.InputStream 읽기를 방지 합니다.

가능한 한 빨리 Request.Form 또는 Request.InputStream에서 읽는 것은 동안 처리기의 실행 이벤트. Mvc에서 컨트롤러는 처리기 이며 실행 이벤트 동작 메서드를 실행 하는 경우. Web Forms 페이지 처리기 이며 Page.Init 이벤트가 발생할 때 실행 이벤트입니다. 이전 실행 이벤트 요청 엔터티 본문을 읽는 경우 요청을 처리 하는 방해 합니다.

를 실행 하기 전에 요청 엔터티 본문을 읽는 해야 하는 경우 하나를 사용 [Request.GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) 하거나 [Request.GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx)합니다. GetBufferlessInputStream를 사용 하는 경우 요청에서 원시는 스트림을 가져오려면 하 고 전체 요청을 처리 하는 것에 대 한 책임을 가정 합니다. GetBufferlessInputStream를 호출한 후 Request.Form 및 Request.InputStream은 사용할 수 없습니다 ASP.NET에서 채우지 않은 것입니다. GetBufferedInputStream를 사용 하는 경우 요청에서 스트림의 복사본을 가져옵니다. ASP.NET 다른 복사본을 채우므로 Request.Form 및 Request.InputStream 요청에서 나중에 사용할 수 있습니다.

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a>Response.Redirect 및 Response.End

권장 사항: 호출한 후 스레드가 처리 하는 방법을의 차이점에 유의 [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx)합니다.

합니다 [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) 메서드 Response.End 메서드를 호출 합니다. 동기 프로세스에서 Request.Redirect를 호출 하면 현재 스레드가 즉시 중단 합니다. 그러나 비동기 프로세스에서 Response.Redirect를 호출를 중단 하지 않습니다 현재 스레드에서 코드 실행 요청에 대해 계속 됩니다. 비동기 프로세스에서 코드 실행을 중지 하려면 메서드에서 작업을 반환 해야 합니다.

MVC 프로젝트에서 Response.Redirect를 호출 하지 않아야 합니다. 된 RedirectResult 대신 반환 합니다.

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a>EnableViewState 및 ViewStateMode

컨트롤 보기 상태를 사용 하는 세부적인 제어를 제공할 EnableViewState 대신의 권장 사항: 사용 하 여 ViewStateMode

EnableViewState Page 지시문에서 false로 설정한 경우 뷰 상태 페이지 내에서 모든 컨트롤에 대해 비활성화 되 고 사용할 수 없습니다. 페이지에만 특정 컨트롤에 대 한 뷰 상태를 사용 하려는 경우 페이지에 대 한 ViewStateMode 사용 안 함으로 설정 합니다.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

그런 다음 실제로 뷰 상태를 해야 하는 컨트롤만에 ViewStateMode Enabled로 설정 합니다.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

만 필요로 하는 컨트롤의 뷰 상태를 사용 하 여 웹 페이지에 대 한 보기 상태의 크기를 축소할 수 있습니다.

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a>SqlMembershipProvider

권장 사항: 범용 공급자를 사용 합니다.

현재 프로젝트 템플릿에서 SqlMembershipProvider 바뀌었습니다 [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers)를 NuGet 패키지로 사용할 수 있는 합니다. SqlMembershipProvider 템플릿의 이전 버전을 사용 하 여 빌드된 프로젝트를 사용 하는 경우 Universal Providers를 전환 해야 합니다. Universal Providers Entity Framework에서 지원 되는 모든 데이터베이스를 사용 하 여 작동 합니다.

자세한 내용은 [Introducing ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)합니다.

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a>장기 실행 요청 (> 110 초)

권장 사항: 사용 [Websocket](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) 하거나 [SignalR](../../../signalr/index.md) 연결 된 클라이언트 및 사용 하 여 비동기 I/O 작업에 대 한 합니다.

장기 실행 요청 웹 응용 프로그램에서 예기치 않은 결과 및 성능 저하를 발생할 수 있습니다. 요청에 대 한 기본 제한 시간 설정은 110 초입니다. 를 사용 하는 장기 실행 요청을 사용 하 여 세션 상태를 사용 하는 경우 ASP.NET 세션 개체에 대 한 잠금을 110 초 후에 출시 됩니다. 그러나 잠금이 해제 되 고 작업을 성공적으로 완료 되지 않을 수 하는 경우 세션 개체에 대 한 작업 중 응용 프로그램 수 있습니다. 첫 번째 요청이 실행 되는 동안 사용자의 두 번째 요청을 차단 된 경우 두 번째 요청 일관성이 없는 상태에서 세션 개체를 액세스할 수 있습니다.

응용 프로그램 차단 (또는 동기) I/O 작업에 포함 된 경우 응용 프로그램 응답 수 없습니다.

성능 향상을 위해.NET Framework의 비동기 I/O 작업을 사용 합니다. 또한 서버에 연결 하는 클라이언트에 대 한 Websocket 또는 SignalR를 사용 합니다. 이러한 기능은 효율적으로 장기 실행 요청을 처리 하도록 설계 되었습니다.
