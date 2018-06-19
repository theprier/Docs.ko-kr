---
uid: web-api/overview/releases/whats-new-in-aspnet-web-api-21
title: ASP.NET Web API 2.1의에서 새로운 기능 | Microsoft Docs
author: microsoft
description: ''
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
ms.locfileid: "26508172"
---
<a name="whats-new-in-aspnet-web-api-21"></a><span data-ttu-id="a124f-102">ASP.NET Web API 2.1의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="a124f-102">What's New in ASP.NET Web API 2.1</span></span>
====================
<span data-ttu-id="a124f-103">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a124f-103">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="a124f-104">이 항목에서는 ASP.NET 웹 API 2.1에 대 한 새로운 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-104">This topic describes what's new for ASP.NET Web API 2.1.</span></span>

- [<span data-ttu-id="a124f-105">다운로드</span><span class="sxs-lookup"><span data-stu-id="a124f-105">Download</span></span>](#download)
- [<span data-ttu-id="a124f-106">문서</span><span class="sxs-lookup"><span data-stu-id="a124f-106">Documentation</span></span>](#documentation)
- [<span data-ttu-id="a124f-107">ASP.NET Web API 2.1의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="a124f-107">New Features in ASP.NET Web API 2.1</span></span>](#new-features)

    - [<span data-ttu-id="a124f-108">전역 오류 처리</span><span class="sxs-lookup"><span data-stu-id="a124f-108">Global Error Handling</span></span>](#global-error)
    - [<span data-ttu-id="a124f-109">라우팅 향상 된 기능 특성</span><span class="sxs-lookup"><span data-stu-id="a124f-109">Attribute Routing Improvements</span></span>](#attribute-routing)
    - [<span data-ttu-id="a124f-110">도움말 페이지 기능 향상</span><span class="sxs-lookup"><span data-stu-id="a124f-110">Help Page Improvements</span></span>](#help-page)
    - [<span data-ttu-id="a124f-111">IgnoreRoute 지원</span><span class="sxs-lookup"><span data-stu-id="a124f-111">IgnoreRoute Support</span></span>](#ignoreroute)
    - [<span data-ttu-id="a124f-112">BSON 미디어 유형 포맷터입니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-112">BSON Media-Type Formatter</span></span>](#bson)
    - [<span data-ttu-id="a124f-113">비동기 필터에 대 한 지원 향상</span><span class="sxs-lookup"><span data-stu-id="a124f-113">Better Support for Async Filters</span></span>](#async-filters)
    - [<span data-ttu-id="a124f-114">형식 라이브러리를 지정 하는 클라이언트에 대 한 구문 분석 하는 쿼리</span><span class="sxs-lookup"><span data-stu-id="a124f-114">Query Parsing for the Client Formatting Library</span></span>](#query-parsing)
- [<span data-ttu-id="a124f-115">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="a124f-115">Known Issues and Breaking Changes</span></span>](#known-issues)
- [<span data-ttu-id="a124f-116">버그 수정</span><span class="sxs-lookup"><span data-stu-id="a124f-116">Bug Fixes</span></span>](#bug-fixes)

<a id="download"></a>
## <a name="download"></a><span data-ttu-id="a124f-117">다운로드</span><span class="sxs-lookup"><span data-stu-id="a124f-117">Download</span></span>

<span data-ttu-id="a124f-118">런타임 기능은 NuGet 갤러리에서 NuGet 패키지로 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-118">The runtime features are released as NuGet packages on the NuGet gallery.</span></span> <span data-ttu-id="a124f-119">모든 런타임 패키지에 따라는 [의미 체계 버전 관리](http://semver.org/) 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-119">All the runtime packages follow the [Semantic Versioning](http://semver.org/) specification.</span></span> <span data-ttu-id="a124f-120">ASP.NET Web API 2.1 RTM 최신 패키지에는 다음 버전: "5.1.2"입니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-120">The latest ASP.NET Web API 2.1 RTM package has the following version: "5.1.2".</span></span> <span data-ttu-id="a124f-121">설치 또는 업데이트를 통해 이러한 패키지 [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-121">You can install or update these packages through [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/).</span></span> <span data-ttu-id="a124f-122">릴리스에 NuGet에 해당 지역화 된 패키지도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-122">The release also includes corresponding localized packages on NuGet.</span></span>

<span data-ttu-id="a124f-123">설치 하거나 NuGet 패키지 관리자 콘솔을 사용 하 여 출시 된 NuGet 패키지를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-123">You can install or update to the released NuGet packages by using the NuGet Package Manager Console:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-21/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="a124f-124">설명서</span><span class="sxs-lookup"><span data-stu-id="a124f-124">Documentation</span></span>

<span data-ttu-id="a124f-125">ASP.NET 웹 사이트에서 사용할 수 있는 자습서 및 ASP.NET Web API 2.1 RTM에 대 한 기타 정보 ([https://www.asp.net/web-api](../../index.md)).</span><span class="sxs-lookup"><span data-stu-id="a124f-125">Tutorials and other information about ASP.NET Web API 2.1 RTM are available from the ASP.NET web site ([https://www.asp.net/web-api](../../index.md)).</span></span>

<a id="new-features"></a>
## <a name="new-features-in-aspnet-web-api-21"></a><span data-ttu-id="a124f-126">ASP.NET Web API 2.1의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="a124f-126">New Features in ASP.NET Web API 2.1</span></span>

<a id="global-error"></a>
### <a name="global-error-handling"></a><span data-ttu-id="a124f-127">전역 오류 처리</span><span class="sxs-lookup"><span data-stu-id="a124f-127">Global Error Handling</span></span>

<span data-ttu-id="a124f-128">하나의 중앙 메커니즘을 통해 모든 처리 되지 않은 예외 기록 이제 수 및 처리 되지 않은 예외에 대 한 동작을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-128">All unhandled exceptions can now be logged through one central mechanism, and the behavior for unhandled exceptions can be customized.</span></span>

<span data-ttu-id="a124f-129">프레임 워크는 모두 처리 되지 않은 예외 및 되었지만, 동시에 처리 중인 요청과 같은 컨텍스트에 대 한 정보를 참조 하십시오. 여러 예외로 거를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-129">The framework supports multiple exception loggers, which all see the unhandled exception and information about the context in which it occurred, such as the request being processed at the time.</span></span>

<span data-ttu-id="a124f-130">예를 들어 다음 코드를 사용 하 여 System.Diagnostics.TraceSource 모든 처리 되지 않은 예외를 기록:</span><span class="sxs-lookup"><span data-stu-id="a124f-130">For example, the following code uses System.Diagnostics.TraceSource to log all unhandled exceptions:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample2.cs)]

<span data-ttu-id="a124f-131">기본 예외 처리기로 바꿀 수도, 발생 하는 경우 처리 되지 않은 예외가 전송 되는 HTTP 응답 메시지를 완전히 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-131">You can also replace the default exception handler, so that you can fully customize the HTTP response message that is sent when an unhandled exception occurs.</span></span>

<span data-ttu-id="a124f-132">제공 된 [샘플](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/Elmah/ReadMe.txt) 인기 있는 ELMAH 프레임 워크를 통해 처리 되지 않은 모든 예외를 기록 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-132">We have provided a [sample](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/Elmah/ReadMe.txt) that logs all unhandled exceptions via the popular ELMAH framework.</span></span>

<a id="attribute-routing"></a>
### <a name="attribute-routing-improvements"></a><span data-ttu-id="a124f-133">라우팅 향상 된 기능 특성</span><span class="sxs-lookup"><span data-stu-id="a124f-133">Attribute Routing Improvements</span></span>

<span data-ttu-id="a124f-134">특성 라우팅을 이제 제약 조건, 버전 관리 및 머리글 기반 경로 선택을 활성화를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-134">Attribute routing now supports constraints, enabling versioning and header-based route selection.</span></span> <span data-ttu-id="a124f-135">또한 특성 경로의 여러 측면을 통해 사용자 지정 가능한 이제는 **IDirectRouteFactory** 인터페이스 및 **RouteFactoryAttribute** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-135">Also, many aspects of attribute routes are now customizable via the **IDirectRouteFactory** interface and **RouteFactoryAttribute** class.</span></span> <span data-ttu-id="a124f-136">경로 접두사를 통해 확장 가능한는 이제는 **IRoutePrefix** 인터페이스 및 **RoutePrefixAttribute** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-136">The route prefix is now extensible via the **IRoutePrefix** interface and **RoutePrefixAttribute** class.</span></span>

<span data-ttu-id="a124f-137">제공 된 [샘플](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/RoutingConstraintsSample/ReadMe.txt) 제약 조건 ' api-version ' HTTP 헤더에 따라 컨트롤러를 동적으로 필터링을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-137">We have provided a [sample](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/RoutingConstraintsSample/ReadMe.txt) that uses constraints to dynamically filter controllers by an 'api-version' HTTP header.</span></span>

<a id="help-page"></a>
### <a name="help-page-improvements"></a><span data-ttu-id="a124f-138">도움말 페이지 기능 향상</span><span class="sxs-lookup"><span data-stu-id="a124f-138">Help Page Improvements</span></span>

<span data-ttu-id="a124f-139">Web API 2.1에는 다음과 같은 향상 기능이 포함 되어 [API 도움말 페이지](../getting-started-with-aspnet-web-api/creating-api-help-pages.md):</span><span class="sxs-lookup"><span data-stu-id="a124f-139">Web API 2.1 includes the following enhancements to [API Help Pages](../getting-started-with-aspnet-web-api/creating-api-help-pages.md):</span></span>

- <span data-ttu-id="a124f-140">매개 변수 또는 반환 형식에 대해 작업의 각 속성의 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-140">Documentation of individual properties of parameters or return types of actions.</span></span>
- <span data-ttu-id="a124f-141">데이터 모델 주석의 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-141">Documentation of data model annotations.</span></span>

<span data-ttu-id="a124f-142">이러한 변경 내용을 수용 하도록 도움말 페이지의 UI 디자인도, 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-142">The UI design of the help pages was also updated, to accomodate these changes.</span></span>

<a id="ignoreroute"></a>
### <a name="ignoreroute-support"></a><span data-ttu-id="a124f-143">IgnoreRoute 지원</span><span class="sxs-lookup"><span data-stu-id="a124f-143">IgnoreRoute Support</span></span>

<span data-ttu-id="a124f-144">집합을 통해 Web API 라우팅에 대 한 URL 패턴을 무시 하는 API 2.1 지원 웹 **IgnoreRoute** 에 확장 메서드 **HttpRouteCollection**합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-144">Web API 2.1 supports ignoring URL patterns in Web API routing, through a set of **IgnoreRoute** extension methods on **HttpRouteCollection**.</span></span> <span data-ttu-id="a124f-145">이러한 메서드는 지정된 된 서식 파일을 일치 하는 모든 Url을 무시 하도록 Web API를 발생 하 고 호스트가 해당 되는 경우 추가 처리를 적용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-145">These methods cause Web API to ignore any URLs that match a specified template, and allow the host to apply additional processing if appropriate.</span></span>

<span data-ttu-id="a124f-146">다음 예제에서는 무시로 시작 하는 Uri는 &quot;콘텐츠&quot; 세그먼트:</span><span class="sxs-lookup"><span data-stu-id="a124f-146">The following example ignores URIs that start with a &quot;content&quot; segment:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample3.cs)]

<a id="bson"></a>
### <a name="bson-media-type-formatter"></a><span data-ttu-id="a124f-147">BSON 미디어 유형 포맷터입니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-147">BSON Media-Type Formatter</span></span>

<span data-ttu-id="a124f-148">API에서 지 원하는 웹는 [BSON](http://bsonspec.org/) 통신 형식으로 클라이언트와 서버에 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-148">Web API now supports the [BSON](http://bsonspec.org/) wire format, both on the client and on the server.</span></span>

<span data-ttu-id="a124f-149">BSON 서버 쪽을 사용 하려면 추가 **BsonMediaTypeFormatter** 포맷터 컬렉션에:</span><span class="sxs-lookup"><span data-stu-id="a124f-149">To enable BSON on the server side, add the **BsonMediaTypeFormatter** to the formatters collection:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample4.cs)]

<span data-ttu-id="a124f-150">.NET 클라이언트 BSON 형식을 소비할 수 있는 방법을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-150">Here is how a .NET client can consume BSON format:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample5.cs)]

<span data-ttu-id="a124f-151">제공 된 [샘플](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/ReadMe.txt) 클라이언트와 서버 쪽을 보여 주는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-151">We have provided a [sample](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/ReadMe.txt) that shows both the client and server side.</span></span>

<span data-ttu-id="a124f-152">자세한 내용은 참조 [웹 API 2.1에서 BSON 지원](../formats-and-model-binding/bson-support-in-web-api-21.md)</span><span class="sxs-lookup"><span data-stu-id="a124f-152">For more information, see [BSON Support in Web API 2.1](../formats-and-model-binding/bson-support-in-web-api-21.md)</span></span>

<a id="async-filters"></a>
### <a name="better-support-for-async-filters"></a><span data-ttu-id="a124f-153">비동기 필터에 대 한 지원 향상</span><span class="sxs-lookup"><span data-stu-id="a124f-153">Better Support for Async Filters</span></span>

<span data-ttu-id="a124f-154">Web API는 이제 쉽게 비동기적으로 실행 하는 필터를 만들 수 있는 방법을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-154">Web API now supports an easy way to create filters that execute asynchronously.</span></span> <span data-ttu-id="a124f-155">이 기능은 유용 필터 데이터베이스 액세스와 같은 비동기 동작을 수행 해야 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-155">This feature is useful is your filter needs to perform an async action, such as access a database.</span></span> <span data-ttu-id="a124f-156">이전에 비동기 필터를 만들려면 사용 했던 인터페이스를 구현 하는 필터를 직접 필터 기본 클래스가 동기 메서드를 노출만 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-156">Previously, to create an async filter, you had to implement the filter interface yourself, because the filter base classes only exposed synchronous methods.</span></span> <span data-ttu-id="a124f-157">이제 가상 문자인 `On*Async` 메서드는 필터의 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-157">Now you can override the virtual `On*Async` methods of the filter base class.</span></span>

<span data-ttu-id="a124f-158">예:</span><span class="sxs-lookup"><span data-stu-id="a124f-158">For example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample6.cs)]

<span data-ttu-id="a124f-159">**AuthorizationFilterAttribute**, **ActionFilterAttribute**, 및 **ExceptionFilterAttribute** 클래스 모두 웹 API 2.1에서 비동기를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-159">The **AuthorizationFilterAttribute**, **ActionFilterAttribute**, and **ExceptionFilterAttribute** classes all support async in Web API 2.1.</span></span>

<a id="query-parsing"></a>
### <a name="query-parsing-for-the-client-formatting-library"></a><span data-ttu-id="a124f-160">형식 라이브러리를 지정 하는 클라이언트에 대 한 구문 분석 하는 쿼리</span><span class="sxs-lookup"><span data-stu-id="a124f-160">Query Parsing for the Client Formatting Library</span></span>

<span data-ttu-id="a124f-161">이전에 **System.Net.Http.Formatting** 지원 되는 구문 분석 및 서버 쪽 코드에 대 한 URI 쿼리를 업데이트 하지만 해당 하는 이식 가능한 라이브러리가 없기 때문에이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-161">Previously, **System.Net.Http.Formatting** supported parsing and updating URI queries for server-side code, but the equivalent portable library was missing this feature.</span></span> <span data-ttu-id="a124f-162">웹 API 2.1에는 클라이언트 응용 프로그램 이제 쉽게 구문 분석 하 고 업데이트할 수는 쿼리 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-162">In Web API 2.1, a client application can now easily parse and update a query string.</span></span>

<span data-ttu-id="a124f-163">다음 예에서는 구문 분석, 수정 및 URI 쿼리를 생성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-163">The following examples show how to parse, modify, and generate URI queries.</span></span> <span data-ttu-id="a124f-164">(예제에서는 간단한 설명을 위해 콘솔 응용 프로그램)</span><span class="sxs-lookup"><span data-stu-id="a124f-164">(The examples show a console application for simplicity.)</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample7.cs)]

<a id="known-issues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="a124f-165">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="a124f-165">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="a124f-166">이 섹션에서는 알려진된 문제 및 ASP.NET Web API 2.1 RTM의 주요 변경 내용에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-166">This section describes known issues and breaking changes in the ASP.NET Web API 2.1 RTM.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="a124f-167">특성 라우팅</span><span class="sxs-lookup"><span data-stu-id="a124f-167">Attribute Routing</span></span>

<span data-ttu-id="a124f-168">이제 특성에서 일치 하는 라우팅 항목에 모호성이 첫 번째 일치 항목을 선택 하지 않고 오류를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-168">Ambiguities in attribute routing matches now report an error rather than choosing the first match.</span></span>

<span data-ttu-id="a124f-169">특성 경로 사용 하 여에서 금지 됩니다는 *{컨트롤러}* 매개 변수를 사용 하 여 간에 *{action}* 경로에 매개 변수가 작업에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-169">Attribute routes are prohibited from using the *{controller}* parameter, and from using the *{action}* parameter on routes placed on actions.</span></span> <span data-ttu-id="a124f-170">이러한 매개 변수 모호성이 발생할 가능성이 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-170">These parameters would very likely cause ambiguities.</span></span>

### <a name="scaffolding-mvcweb-api-into-a-project-with-51-packages-results-in-50-packages-for-ones-that-dont-already-exist-in-the-project"></a><span data-ttu-id="a124f-171">5.1 패키지 결과 프로젝트에 이미 존재 하지 않는 것에 대 한 5.0 패키지를 사용 하는 프로젝트에 스 캐 폴딩 MVC/웹 API</span><span class="sxs-lookup"><span data-stu-id="a124f-171">Scaffolding MVC/Web API into a project with 5.1 packages results in 5.0 packages for ones that don't already exist in the project</span></span>

<span data-ttu-id="a124f-172">ASP.NET Web API 2.1 RTM에 대 한 NuGet 패키지를 업데이트 해도 Visual Studio tools ASP.NET 스 캐 폴딩 같은 또는 ASP.NET 웹 응용 프로그램 프로젝트 템플릿을 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-172">Updating NuGet packages for ASP.NET Web API 2.1 RTM does not update the Visual Studio tools, such as ASP.NET scaffolding or the ASP.NET Web Application project template.</span></span> <span data-ttu-id="a124f-173">이전 버전의 ASP.NET 런타임 패키지 (5.0.0.0) 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-173">They use the previous version of the ASP.NET runtime packages (5.0.0.0).</span></span> <span data-ttu-id="a124f-174">결과적으로, ASP.NET 스 캐 폴딩은 이미 프로젝트에서 사용할 수 없는 경우에 필요한 패키지의 이전 버전 (5.0.0.0)으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-174">As a result, the ASP.NET scaffolding will install the previous version (5.0.0.0) of the required packages, if they are not already available in your projects.</span></span> <span data-ttu-id="a124f-175">그러나 Visual Studio 2013 RTM 또는 업데이트 1에서 ASP.NET 스 캐 폴딩을 프로젝트에서 최신 패키지를 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-175">However, the ASP.NET scaffolding in Visual Studio 2013 RTM or Update 1 does not overwrite the latest packages in your projects.</span></span>

<span data-ttu-id="a124f-176">ASP.NET 웹 API 2.1 또는 ASP.NET MVC 5.1에는 패키지를 업데이트 한 후에 스 캐 폴딩을 사용 하는 경우에 버전의 웹 API 및 MVC 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-176">If you use ASP.NET scaffolding after updating the packages to Web API 2.1 or ASP.NET MVC 5.1, make sure the versions of Web API and MVC are consistent.</span></span>

### <a name="type-renames"></a><span data-ttu-id="a124f-177">형식 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="a124f-177">Type Renames</span></span>

<span data-ttu-id="a124f-178">라우팅 확장 특성에 사용 되는 형식 중 일부를 2.1 RTM rc에서 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-178">Some of the types used for attribute routing extensibility were renamed from the RC to the 2.1 RTM.</span></span>

| <span data-ttu-id="a124f-179">이전 형식 이름 (2.1 RC)</span><span class="sxs-lookup"><span data-stu-id="a124f-179">Old type name (2.1 RC)</span></span> | <span data-ttu-id="a124f-180">새 형식 이름을 (2.1 RTM)</span><span class="sxs-lookup"><span data-stu-id="a124f-180">New Type Name (2.1 RTM)</span></span> |
| --- | --- |
| <span data-ttu-id="a124f-181">IDirectRouteProvider</span><span class="sxs-lookup"><span data-stu-id="a124f-181">IDirectRouteProvider</span></span> | <span data-ttu-id="a124f-182">IDirectRouteFactory</span><span class="sxs-lookup"><span data-stu-id="a124f-182">IDirectRouteFactory</span></span> |
| <span data-ttu-id="a124f-183">RouteProviderAttribute</span><span class="sxs-lookup"><span data-stu-id="a124f-183">RouteProviderAttribute</span></span> | <span data-ttu-id="a124f-184">RouteFactoryAttribute</span><span class="sxs-lookup"><span data-stu-id="a124f-184">RouteFactoryAttribute</span></span> |
| <span data-ttu-id="a124f-185">DirectRouteProviderContext</span><span class="sxs-lookup"><span data-stu-id="a124f-185">DirectRouteProviderContext</span></span> | <span data-ttu-id="a124f-186">DirectRouteFactoryContext</span><span class="sxs-lookup"><span data-stu-id="a124f-186">DirectRouteFactoryContext</span></span> |

### <a name="exception-filters-do-not-unwrap-aggregate-exceptions-thrown-in-async-actions"></a><span data-ttu-id="a124f-187">예외 필터 비동기 작업에서 발생 한 예외를 집계 래핑을 해제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-187">Exception filters do not unwrap aggregate exceptions thrown in async actions</span></span>

<span data-ttu-id="a124f-188">이전에 비동기 작업에서는 **AggregateException**, 예외 필터에서 예외를 래핑 해제는 및 **OnException** 기본 예외를 얻을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-188">Previously, if an async action threw an **AggregateException**, an exception filter would unwrap the exception, and **OnException** would get the base exception.</span></span> <span data-ttu-id="a124f-189">2.1에서 예외 필터는 래핑을 해제 하지 않습니다, 및 **OnException** 원래 가져옵니다 **AggregateException**합니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-189">In 2.1, the exception filter does not unwrap it, and **OnException** gets the original **AggregateException**.</span></span>

<a id="bug-fixes"></a>
## <a name="bug-fixes"></a><span data-ttu-id="a124f-190">버그 수정</span><span class="sxs-lookup"><span data-stu-id="a124f-190">Bug Fixes</span></span>

<span data-ttu-id="a124f-191">이 버전에는 다양 한 버그 수정 사항이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-191">This release also includes several bug fixes.</span></span> <span data-ttu-id="a124f-192">전체 목록은 여기를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-192">You can find the complete list here:</span></span>

- [<span data-ttu-id="a124f-193">5.1.0 패키지</span><span class="sxs-lookup"><span data-stu-id="a124f-193">5.1.0 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.1%20Preview|v5.1%20RTM&amp;assignedTo=All&amp;component=Web%20API|Web%20API%20OData&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)
- [<span data-ttu-id="a124f-194">5.1.1 패키지</span><span class="sxs-lookup"><span data-stu-id="a124f-194">5.1.1 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=v5.1.1%20RTM&assignedTo=All&component=Web%20API&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<span data-ttu-id="a124f-195">5.1.2 없는 버그 수정 하지만 IntelliSense 업데이트 패키지에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a124f-195">The 5.1.2 package contains IntelliSense updates but no bug fixes.</span></span>
