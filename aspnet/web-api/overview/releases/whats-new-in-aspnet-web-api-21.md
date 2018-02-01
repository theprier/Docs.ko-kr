---
uid: web-api/overview/releases/whats-new-in-aspnet-web-api-21
title: "ASP.NET Web API 2.1의에서 새로운 기능 | Microsoft Docs"
author: microsoft
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2014
ms.topic: article
ms.assetid: b6721bba-38c8-48c4-acbf-274c1a34e817
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/releases/whats-new-in-aspnet-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: cc5dc111d88cc7dae6a4a93203317fa0769d5427
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="whats-new-in-aspnet-web-api-21"></a>ASP.NET Web API 2.1의에서 새로운 기능
====================
여 [Microsoft](https://github.com/microsoft)

이 항목에서는 ASP.NET 웹 API 2.1에 대 한 새로운 기능을 설명 합니다.

- [다운로드](#download)
- [문서](#documentation)
- [ASP.NET Web API 2.1의에서 새로운 기능](#new-features)

    - [전역 오류 처리](#global-error)
    - [라우팅 향상 된 기능 특성](#attribute-routing)
    - [도움말 페이지 기능 향상](#help-page)
    - [IgnoreRoute 지원](#ignoreroute)
    - [BSON 미디어 유형 포맷터입니다.](#bson)
    - [비동기 필터에 대 한 지원 향상](#async-filters)
    - [형식 라이브러리를 지정 하는 클라이언트에 대 한 구문 분석 하는 쿼리](#query-parsing)
- [알려진된 문제 및 주요 변경 내용](#known-issues)
- [버그 수정](#bug-fixes)

<a id="download"></a>
## <a name="download"></a>다운로드

런타임 기능은 NuGet 갤러리에서 NuGet 패키지로 해제 됩니다. 모든 런타임 패키지에 따라는 [의미 체계 버전 관리](http://semver.org/) 사양입니다. ASP.NET Web API 2.1 RTM 최신 패키지에는 다음 버전: "5.1.2"입니다. 설치 또는 업데이트를 통해 이러한 패키지 [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/)합니다. 릴리스에 NuGet에 해당 지역화 된 패키지도 포함 됩니다.

설치 하거나 NuGet 패키지 관리자 콘솔을 사용 하 여 출시 된 NuGet 패키지를 업데이트할 수 있습니다.

[!code-console[Main](whats-new-in-aspnet-web-api-21/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a>설명서

ASP.NET 웹 사이트에서 사용할 수 있는 자습서 및 ASP.NET Web API 2.1 RTM에 대 한 기타 정보 ([https://www.asp.net/web-api](../../index.md)).

<a id="new-features"></a>
## <a name="new-features-in-aspnet-web-api-21"></a>ASP.NET Web API 2.1의에서 새로운 기능

<a id="global-error"></a>
### <a name="global-error-handling"></a>전역 오류 처리

하나의 중앙 메커니즘을 통해 모든 처리 되지 않은 예외 기록 이제 수 및 처리 되지 않은 예외에 대 한 동작을 사용자 지정할 수 있습니다.

프레임 워크는 모두 처리 되지 않은 예외 및 되었지만, 동시에 처리 중인 요청과 같은 컨텍스트에 대 한 정보를 참조 하십시오. 여러 예외로 거를 지원 합니다.

예를 들어 다음 코드를 사용 하 여 System.Diagnostics.TraceSource 모든 처리 되지 않은 예외를 기록:

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample2.cs)]

기본 예외 처리기로 바꿀 수도, 발생 하는 경우 처리 되지 않은 예외가 전송 되는 HTTP 응답 메시지를 완전히 사용자 지정할 수 있습니다.

제공 된 [샘플](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/Elmah/ReadMe.txt) 인기 있는 ELMAH 프레임 워크를 통해 처리 되지 않은 모든 예외를 기록 하는 합니다.

<a id="attribute-routing"></a>
### <a name="attribute-routing-improvements"></a>라우팅 향상 된 기능 특성

특성 라우팅을 이제 제약 조건, 버전 관리 및 머리글 기반 경로 선택을 활성화를 지원 합니다. 또한 특성 경로의 여러 측면을 통해 사용자 지정 가능한 이제는 **IDirectRouteFactory** 인터페이스 및 **RouteFactoryAttribute** 클래스입니다. 경로 접두사를 통해 확장 가능한는 이제는 **IRoutePrefix** 인터페이스 및 **RoutePrefixAttribute** 클래스입니다.

제공 된 [샘플](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/RoutingConstraintsSample/ReadMe.txt) 제약 조건 ' api-version ' HTTP 헤더에 따라 컨트롤러를 동적으로 필터링을 사용 하 여 합니다.

<a id="help-page"></a>
### <a name="help-page-improvements"></a>도움말 페이지 기능 향상

Web API 2.1에는 다음과 같은 향상 기능이 포함 되어 [API 도움말 페이지](../getting-started-with-aspnet-web-api/creating-api-help-pages.md):

- 매개 변수 또는 반환 형식에 대해 작업의 각 속성의 설명서입니다.
- 데이터 모델 주석의 설명서입니다.

이러한 변경 내용을 수용 하도록 도움말 페이지의 UI 디자인도, 업데이트 되었습니다.

<a id="ignoreroute"></a>
### <a name="ignoreroute-support"></a>IgnoreRoute 지원

집합을 통해 Web API 라우팅에 대 한 URL 패턴을 무시 하는 API 2.1 지원 웹 **IgnoreRoute** 에 확장 메서드 **HttpRouteCollection**합니다. 이러한 메서드는 지정된 된 서식 파일을 일치 하는 모든 Url을 무시 하도록 Web API를 발생 하 고 호스트가 해당 되는 경우 추가 처리를 적용할 수 있도록 합니다.

다음 예제에서는 무시로 시작 하는 Uri는 &quot;콘텐츠&quot; 세그먼트:

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample3.cs)]

<a id="bson"></a>
### <a name="bson-media-type-formatter"></a>BSON 미디어 유형 포맷터입니다.

API에서 지 원하는 웹는 [BSON](http://bsonspec.org/) 통신 형식으로 클라이언트와 서버에 모두 있습니다.

BSON 서버 쪽을 사용 하려면 추가 **BsonMediaTypeFormatter** 포맷터 컬렉션에:

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample4.cs)]

.NET 클라이언트 BSON 형식을 소비할 수 있는 방법을 다음과 같습니다.

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample5.cs)]

제공 된 [샘플](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/ReadMe.txt) 클라이언트와 서버 쪽을 보여 주는 합니다.

자세한 내용은 참조 [웹 API 2.1에서 BSON 지원](../formats-and-model-binding/bson-support-in-web-api-21.md)

<a id="async-filters"></a>
### <a name="better-support-for-async-filters"></a>비동기 필터에 대 한 지원 향상

Web API는 이제 쉽게 비동기적으로 실행 하는 필터를 만들 수 있는 방법을 지원 합니다. 이 기능은 유용 필터 데이터베이스 액세스와 같은 비동기 동작을 수행 해야 하는 합니다. 이전에 비동기 필터를 만들려면 사용 했던 인터페이스를 구현 하는 필터를 직접 필터 기본 클래스가 동기 메서드를 노출만 합니다. 이제 가상 문자인 `On*Async` 메서드는 필터의 기본 클래스입니다.

예:

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample6.cs)]

**AuthorizationFilterAttribute**, **ActionFilterAttribute**, 및 **ExceptionFilterAttribute** 클래스 모두 웹 API 2.1에서 비동기를 지원 합니다.

<a id="query-parsing"></a>
### <a name="query-parsing-for-the-client-formatting-library"></a>형식 라이브러리를 지정 하는 클라이언트에 대 한 구문 분석 하는 쿼리

이전에 **System.Net.Http.Formatting** 지원 되는 구문 분석 및 서버 쪽 코드에 대 한 URI 쿼리를 업데이트 하지만 해당 하는 이식 가능한 라이브러리가 없기 때문에이 기능입니다. 웹 API 2.1에는 클라이언트 응용 프로그램 이제 쉽게 구문 분석 하 고 업데이트할 수는 쿼리 문자열입니다.

다음 예에서는 구문 분석, 수정 및 URI 쿼리를 생성 하는 방법을 보여 줍니다. (예제에서는 간단한 설명을 위해 콘솔 응용 프로그램)

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample7.cs)]

<a id="known-issues"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진된 문제 및 주요 변경 내용

이 섹션에서는 알려진된 문제 및 ASP.NET Web API 2.1 RTM의 주요 변경 내용에 설명 합니다.

### <a name="attribute-routing"></a>특성 라우팅

이제 특성에서 일치 하는 라우팅 항목에 모호성이 첫 번째 일치 항목을 선택 하지 않고 오류를 보고 합니다.

특성 경로 사용 하 여에서 금지 됩니다는 *{컨트롤러}* 매개 변수를 사용 하 여 간에 *{action}* 경로에 매개 변수가 작업에 배치 합니다. 이러한 매개 변수 모호성이 발생할 가능성이 것입니다.

### <a name="scaffolding-mvcweb-api-into-a-project-with-51-packages-results-in-50-packages-for-ones-that-dont-already-exist-in-the-project"></a>5.1 패키지 결과 프로젝트에 이미 존재 하지 않는 것에 대 한 5.0 패키지를 사용 하는 프로젝트에 스 캐 폴딩 MVC/웹 API

ASP.NET Web API 2.1 RTM에 대 한 NuGet 패키지를 업데이트 해도 Visual Studio tools ASP.NET 스 캐 폴딩 같은 또는 ASP.NET 웹 응용 프로그램 프로젝트 템플릿을 업데이트 되지 않습니다. 이전 버전의 ASP.NET 런타임 패키지 (5.0.0.0) 사용합니다. 결과적으로, ASP.NET 스 캐 폴딩은 이미 프로젝트에서 사용할 수 없는 경우에 필요한 패키지의 이전 버전 (5.0.0.0)으로 설치 됩니다. 그러나 Visual Studio 2013 RTM 또는 업데이트 1에서 ASP.NET 스 캐 폴딩을 프로젝트에서 최신 패키지를 덮어쓰지 않습니다.

ASP.NET 웹 API 2.1 또는 ASP.NET MVC 5.1에는 패키지를 업데이트 한 후에 스 캐 폴딩을 사용 하는 경우에 버전의 웹 API 및 MVC 일치 하는지 확인 합니다.

### <a name="type-renames"></a>형식 이름 바꾸기

라우팅 확장 특성에 사용 되는 형식 중 일부를 2.1 RTM rc에서 변경 되었습니다.

| 이전 형식 이름 (2.1 RC) | 새 형식 이름을 (2.1 RTM) |
| --- | --- |
| IDirectRouteProvider | IDirectRouteFactory |
| RouteProviderAttribute | RouteFactoryAttribute |
| DirectRouteProviderContext | DirectRouteFactoryContext |

### <a name="exception-filters-do-not-unwrap-aggregate-exceptions-thrown-in-async-actions"></a>예외 필터 비동기 작업에서 발생 한 예외를 집계 래핑을 해제 하지 않습니다.

이전에 비동기 작업에서는 **AggregateException**, 예외 필터에서 예외를 래핑 해제는 및 **OnException** 기본 예외를 얻을 수도 있습니다. 2.1에서 예외 필터는 래핑을 해제 하지 않습니다, 및 **OnException** 원래 가져옵니다 **AggregateException**합니다.

<a id="bug-fixes"></a>
## <a name="bug-fixes"></a>버그 수정

이 버전에는 다양 한 버그 수정 사항이 포함 되어 있습니다. 전체 목록은 여기를 찾을 수 있습니다.

- [5.1.0 패키지](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.1%20Preview|v5.1%20RTM&amp;assignedTo=All&amp;component=Web%20API|Web%20API%20OData&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)
- [5.1.1 패키지](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=v5.1.1%20RTM&assignedTo=All&component=Web%20API&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

5.1.2 없는 버그 수정 하지만 IntelliSense 업데이트 패키지에 포함 되어 있습니다.
