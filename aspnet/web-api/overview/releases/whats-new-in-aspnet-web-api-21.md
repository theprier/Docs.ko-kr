---
uid: web-api/overview/releases/whats-new-in-aspnet-web-api-21
title: ASP.NET Web API 2.1의에서 새로운 기능 | Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
ms.date: 01/20/2014
ms.assetid: b6721bba-38c8-48c4-acbf-274c1a34e817
msc.legacyurl: /web-api/overview/releases/whats-new-in-aspnet-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: 7952614456b1de24e4c618b9e7ba8448b2a01741
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37838405"
---
<a name="whats-new-in-aspnet-web-api-21"></a>ASP.NET Web API 2.1의에서 새로운 기능
====================
[Microsoft](https://github.com/microsoft)

이 항목에서는 ASP.NET Web API 2.1의 새로운 기능을 설명 합니다.

- [다운로드](#download)
- [문서](#documentation)
- [ASP.NET Web API 2.1의에서 새로운 기능](#new-features)

    - [전역 오류 처리](#global-error)
    - [특성 라우팅 기능 향상](#attribute-routing)
    - [도움말 페이지 개선](#help-page)
    - [IgnoreRoute 지원](#ignoreroute)
    - [BSON 미디어 유형 포맷터입니다.](#bson)
    - [비동기 필터에 대 한 지원 향상](#async-filters)
    - [클라이언트 라이브러리를 서식 지정에 대 한 구문 분석 하는 쿼리](#query-parsing)
- [알려진된 문제 및 주요 변경 내용](#known-issues)
- [버그 수정](#bug-fixes)

<a id="download"></a>
## <a name="download"></a>다운로드

NuGet 갤러리에서 NuGet 패키지로 런타임 기능 해제 됩니다. 모든 런타임 패키지를 수행 합니다 [유의 적 버전](http://semver.org/) 사양입니다. 다음 버전이 최신 ASP.NET Web API 2.1 RTM 패키지: "5.1.2"입니다. 설치 하거나 이러한 패키지를 통해 업데이트할 수 있습니다 [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/)합니다. 릴리스에 NuGet의 해당 지역화 된 패키지도 포함 됩니다.

설치 하거나 NuGet 패키지 관리자 콘솔을 사용 하 여 릴리스된 NuGet 패키지를 업데이트할 수 있습니다.

[!code-console[Main](whats-new-in-aspnet-web-api-21/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a>설명서

자습서 및 ASP.NET Web API 2.1 RTM에 대 한 다른 정보는 ASP.NET 웹 사이트에서 사용할 수 있습니다 ([https://www.asp.net/web-api](../../index.md)).

<a id="new-features"></a>
## <a name="new-features-in-aspnet-web-api-21"></a>ASP.NET Web API 2.1의에서 새로운 기능

<a id="global-error"></a>
### <a name="global-error-handling"></a>전역 오류 처리

모든 처리 되지 않은 예외는 하나의 중앙 메커니즘을 통해 이제 로깅될 수 있습니다 하 고 처리 되지 않은 예외에 대 한 동작을 사용자 지정할 수 있습니다.

프레임 워크는 모두 있는 것 같은 발생 시 처리 되는 요청 컨텍스트에 대 한 정보와 처리 되지 않은 예외를 참조 하세요. 여러 예외로 거를 지원 합니다.

예를 들어, 다음 코드는 모든 처리 되지 않은 예외를 기록할 System.Diagnostics.TraceSource를 사용 합니다.

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample2.cs)]

기본 예외 처리기를 바꿀 수도 있습니다를 완전히 처리 되지 않은 예외가 때 전송 되는 HTTP 응답 메시지를 사용자 지정할 수 있도록 발생 하 합니다.

제공 된 [샘플](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/Elmah/ReadMe.txt) 인기 있는 ELMAH 프레임 워크를 통해 모든 처리 되지 않은 예외를 기록 하는 합니다.

<a id="attribute-routing"></a>
### <a name="attribute-routing-improvements"></a>특성 라우팅 기능 향상

특성 라우팅은 이제 제약 조건, 버전 관리 및 헤더 기반 경로 선택을 사용할 수 있도록 지원 합니다. 여러 가지 특성 경로 통해 사용자 지정 가능한 됩니다 또한 합니다 **IDirectRouteFactory** 인터페이스와 **RouteFactoryAttribute** 클래스입니다. 경로 접두사를 통해 확장 되었습니다 합니다 **IRoutePrefix** 인터페이스와 **RoutePrefixAttribute** 클래스입니다.

제공 된 [샘플](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/RoutingConstraintsSample/ReadMe.txt) 제약 조건 ' api-version은 ' HTTP 헤더에서 컨트롤러를 동적으로 필터링을 사용 하 여 합니다.

<a id="help-page"></a>
### <a name="help-page-improvements"></a>도움말 페이지 개선

Web API 2.1에서 다음과 같은 향상 기능이 포함 되어 있습니다 [API 도움말 페이지](../getting-started-with-aspnet-web-api/creating-api-help-pages.md):

- 매개 변수 또는 반환 형식에 대해 작업의 개별 속성 설명서입니다.
- 데이터 모델에 대 한 주석의 설명서입니다.

이러한 변경 내용을 수용 하도록 도움말 페이지의 UI 디자인에도, 업데이트 되었습니다.

<a id="ignoreroute"></a>
### <a name="ignoreroute-support"></a>IgnoreRoute 지원

Web API 2.1은 URL 패턴의 집합을 통해 Web API 라우팅에 무시 **IgnoreRoute** 대 한 확장 메서드 **HttpRouteCollection**합니다. 이러한 메서드를 지정된 된 템플릿을 일치 하는 모든 Url을 무시 하려면 Web API를 발생 하 고 해당 하는 경우 추가 처리를 적용 하려면 호스트를 허용 합니다.

다음 예제에서는 무시로 시작 하는 Uri를 &quot;콘텐츠&quot; 세그먼트:

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample3.cs)]

<a id="bson"></a>
### <a name="bson-media-type-formatter"></a>BSON 미디어 유형 포맷터입니다.

웹 API에서 지 원하는 합니다 [BSON](http://bsonspec.org/) 클라이언트와 서버의 통신 형식입니다.

서버 쪽에서 BSON을 활성화 하려면 합니다 **BsonMediaTypeFormatter** 포맷터 컬렉션:

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample4.cs)]

.NET 클라이언트 BSON 형식을 사용 하는 방법 다음과 같습니다.

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample5.cs)]

제공 된 [샘플](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/ReadMe.txt) 클라이언트와 서버 쪽을 보여 주는 합니다.

자세한 내용은 참조 하세요. [Web API 2.1에서 BSON 지원](../formats-and-model-binding/bson-support-in-web-api-21.md)

<a id="async-filters"></a>
### <a name="better-support-for-async-filters"></a>비동기 필터에 대 한 지원 향상

웹 API는 이제 비동기적으로 실행 되는 필터를 만드는 쉬운을 지원 합니다. 이 기능은 유용 필터 데이터베이스 액세스와 같은 비동기 작업을 수행 해야 됩니다. 이전에 비동기 필터를 만들려면 했습니다 인터페이스를 구현 하는 필터를 직접 필터 기본 클래스 에서만 동기 메서드를 노출 합니다. 이제 가상 재정의할 수 있습니다 `On*Async` 메서드 필터의 기본 클래스입니다.

예를 들어:

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample6.cs)]

합니다 **AuthorizationFilterAttribute**를 **ActionFilterAttribute**, 및 **ExceptionFilterAttribute** 클래스는 모두 Web API 2.1에서 비동기를 지원 합니다.

<a id="query-parsing"></a>
### <a name="query-parsing-for-the-client-formatting-library"></a>클라이언트 라이브러리를 서식 지정에 대 한 구문 분석 하는 쿼리

이전에 **System.Net.Http.Formatting** 구문 분석 하 고 업데이트 서버 쪽 코드에 대 한 URI 쿼리를 지원 하지만 해당 하는 이식 가능한 라이브러리에는이 기능은 없습니다. Web API 2.1에서 클라이언트 응용 프로그램을 이제 쉽게 구문 분석 하 고 업데이트할 수는 쿼리 문자열입니다.

다음 예제에서는 구문 분석, 수정 및 URI 쿼리를 생성 하는 방법을 보여 줍니다. (예제에서는 편의상 콘솔 응용 프로그램을 표시 합니다.)

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample7.cs)]

<a id="known-issues"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진된 문제 및 주요 변경 내용

이 섹션에서는 알려진된 문제 및 ASP.NET Web API 2.1 RTM의 주요 변경 내용에 설명합니다.

### <a name="attribute-routing"></a>특성 라우팅

특성 라우팅 일치 항목이 모호성은 이제 첫 번째 일치 항목을 선택 하는 것이 아니라 오류를 보고 합니다.

특성 경로를 사용할 수 없습니다는 *{컨트롤러}* 매개 변수를 사용 하는 *{action}* 경로에 매개 변수 작업에 배치 합니다. 이러한 매개 변수 하면 모호성이 발생할 가능성이 됩니다.

### <a name="scaffolding-mvcweb-api-into-a-project-with-51-packages-results-in-50-packages-for-ones-that-dont-already-exist-in-the-project"></a>프로젝트에 이미 존재 하지 않는 것에 대 한 패키지를 5.0에서 5.1 패키지 결과 사용 하 여 프로젝트에 스 캐 폴딩 MVC/웹 API

ASP.NET 웹 응용 프로그램 프로젝트 템플릿이나 ASP.NET 스 캐 폴딩와 같은 Visual Studio 도구, ASP.NET Web API 2.1 RTM에 대 한 NuGet 패키지를 업데이트 하는 중 업데이트 되지 않습니다. 이전 버전의 ASP.NET 런타임 패키지 (5.0.0.0)를 사용합니다. 결과적으로, ASP.NET 스 캐 폴딩은 이미 프로젝트에서 사용할 수 없는 경우에 필요한 패키지의 이전 버전 (5.0.0.0)으로 설치 됩니다. 그러나 Visual Studio 2013 RTM 또는 업데이트 1에서 ASP.NET 스 캐 폴딩 프로젝트에서 최신 패키지를 덮어쓰지 않습니다.

ASP.NET Web API 2.1 또는 ASP.NET MVC 5.1에는 패키지를 업데이트 한 후에 스 캐 폴딩을 사용 하는 경우 Web API 및 MVC의 버전이 일치 하는지 확인 합니다.

### <a name="type-renames"></a>형식 이름 바꾸기

특성 라우팅 확장성에 사용 되는 형식 중 일부를 2.1 RTM RC에서 변경 되었습니다.

| 이전 형식 이름 (2.1 RC) | 새 형식 이름을 (2.1 RTM) |
| --- | --- |
| IDirectRouteProvider | IDirectRouteFactory |
| RouteProviderAttribute | RouteFactoryAttribute |
| DirectRouteProviderContext | DirectRouteFactoryContext |

### <a name="exception-filters-do-not-unwrap-aggregate-exceptions-thrown-in-async-actions"></a>예외 필터 수행할 비동기 작업에서 throw 하는 집계 예외 래핑을 해제 하지 않습니다.

이전에 비동기 작업에서 하는 경우는 **AggregateException**, 예외 필터에서 예외를 래핑 해제 됩니다 및 **OnException** 기본 예외만 얻게입니다. 2.1에서 예외 필터는 래핑을 해제 하지 않습니다, 및 **OnException** 원래 가져옵니다 **AggregateException**합니다.

<a id="bug-fixes"></a>
## <a name="bug-fixes"></a>버그 수정

이 이번에는 여러 버그 수정도 포함 됩니다. 여기서 전체 목록을 찾을 수 있습니다.

- [5.1.0 패키지](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.1%20Preview|v5.1%20RTM&amp;assignedTo=All&amp;component=Web%20API|Web%20API%20OData&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)
- [5.1.1 패키지](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=v5.1.1%20RTM&assignedTo=All&component=Web%20API&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

5.1.2 없습니다 버그 수정 하지만 IntelliSense 업데이트 패키지에 포함 되어 있습니다.
