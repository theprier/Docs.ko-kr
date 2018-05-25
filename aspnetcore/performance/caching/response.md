---
title: ASP.NET Core의 응답 캐싱
author: rick-anderson
description: 낮은 대역폭 요구 사항에 대응하고 ASP.NET Core 응용 프로그램의 성능을 향상시키기 위해 응답 캐싱을 사용하는 방법을 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 09/20/2017
ms.prod: asp.net-core
ms.topic: article
uid: performance/caching/response
ms.openlocfilehash: cc1ec50155398ba4143a2bf697ca26435c228c49
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="response-caching-in-aspnet-core"></a><span data-ttu-id="e1c14-103">ASP.NET Core의 응답 캐싱</span><span class="sxs-lookup"><span data-stu-id="e1c14-103">Response caching in ASP.NET Core</span></span>

<span data-ttu-id="e1c14-104">작성자: [John Luo](https://github.com/JunTaoLuo), [Rick Anderson](https://twitter.com/RickAndMSFT), [Steve Smith](https://ardalis.com/), 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="e1c14-104">By [John Luo](https://github.com/JunTaoLuo), [Rick Anderson](https://twitter.com/RickAndMSFT), [Steve Smith](https://ardalis.com/), and [Luke Latham](https://github.com/guardrex)</span></span>

> [!NOTE]
> <span data-ttu-id="e1c14-105">응답 캐싱은 [ASP.NET Core 2.0을 사용하는 Razor 페이지에서는 지원되지 않습니다.](https://github.com/aspnet/Mvc/issues/6437)</span><span class="sxs-lookup"><span data-stu-id="e1c14-105">Response caching [isn't supported in Razor Pages with ASP.NET Core 2.0](https://github.com/aspnet/Mvc/issues/6437).</span></span> <span data-ttu-id="e1c14-106">이 기능은 [ASP.NET Core 2.1 릴리스](https://github.com/aspnet/Home/wiki/Roadmap)부터 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-106">This feature will be supported in the [ASP.NET Core 2.1 release](https://github.com/aspnet/Home/wiki/Roadmap).</span></span>
  
<span data-ttu-id="e1c14-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/response/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="e1c14-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/response/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="e1c14-108">응답 캐싱은 클라이언트나 프록시가 웹 서버에 요청하는 회수를 줄여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-108">Response caching reduces the number of requests a client or proxy makes to a web server.</span></span> <span data-ttu-id="e1c14-109">또한 응답 캐싱은 웹 서버가 응답을 생성하기 위해 수행해야 하는 작업의 총량도 줄여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-109">Response caching also reduces the amount of work the web server performs to generate a response.</span></span> <span data-ttu-id="e1c14-110">응답 캐싱은 클라이언트, 프록시, 및 미들웨어가 응답을 캐싱해야 하는 방식을 지시하는 헤더에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-110">Response caching is controlled by headers that specify how you want client, proxy, and middleware to cache responses.</span></span>

<span data-ttu-id="e1c14-111">[응답 캐싱 미들웨어](xref:performance/caching/middleware)를 추가하면 웹 서버가 응답을 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-111">The web server can cache responses when you add [Response Caching Middleware](xref:performance/caching/middleware).</span></span>

## <a name="http-based-response-caching"></a><span data-ttu-id="e1c14-112">HTTP 기반 응답 캐싱</span><span class="sxs-lookup"><span data-stu-id="e1c14-112">HTTP-based response caching</span></span>

<span data-ttu-id="e1c14-113">[HTTP 1.1 캐싱 사양](https://tools.ietf.org/html/rfc7234)은 인터넷 캐시가 동작해야 하는 방식을 기술합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-113">The [HTTP 1.1 Caching specification](https://tools.ietf.org/html/rfc7234) describes how Internet caches should behave.</span></span> <span data-ttu-id="e1c14-114">캐싱에 사용되는 가장 기본적인 HTTP 헤더는 [Cache-Control](https://tools.ietf.org/html/rfc7234#section-5.2)로 캐시 *지시문*을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-114">The primary HTTP header used for caching is [Cache-Control](https://tools.ietf.org/html/rfc7234#section-5.2), which is used to specify cache *directives*.</span></span> <span data-ttu-id="e1c14-115">지시문은 요청이 클라이언트에서 서버로 전달될 때의 캐싱 동작과 응답이 서버에서 클라이언트로 되돌아올 때의 캐싱 동작을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-115">The directives control caching behavior as requests make their way from clients to servers and as reponses make their way from servers back to clients.</span></span> <span data-ttu-id="e1c14-116">프록시 서버를 통해서 이동하는 요청 및 응답, 그리고 프록시 서버 역시 HTTP 1.1 캐싱 사양을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-116">Requests and responses move through proxy servers, and proxy servers must also conform to the HTTP 1.1 Caching specification.</span></span>

<span data-ttu-id="e1c14-117">기본적인 `Cache-Control` 지시문은 다음 표와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-117">Common `Cache-Control` directives are shown in the following table.</span></span>

| <span data-ttu-id="e1c14-118">지시문</span><span class="sxs-lookup"><span data-stu-id="e1c14-118">Directive</span></span>                                                       | <span data-ttu-id="e1c14-119">작업</span><span class="sxs-lookup"><span data-stu-id="e1c14-119">Action</span></span> |
| --------------------------------------------------------------- | ------ |
| [<span data-ttu-id="e1c14-120">public</span><span class="sxs-lookup"><span data-stu-id="e1c14-120">public</span></span>](https://tools.ietf.org/html/rfc7234#section-5.2.2.5)   | <span data-ttu-id="e1c14-121">캐시에 응답을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-121">A cache may store the response.</span></span> |
| [<span data-ttu-id="e1c14-122">private</span><span class="sxs-lookup"><span data-stu-id="e1c14-122">private</span></span>](https://tools.ietf.org/html/rfc7234#section-5.2.2.6)  | <span data-ttu-id="e1c14-123">공유 캐시는 응답을 저장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-123">The response must not be stored by a shared cache.</span></span> <span data-ttu-id="e1c14-124">사설 캐시는 응답을 저장하고 재사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-124">A private cache may store and reuse the response.</span></span> |
| [<span data-ttu-id="e1c14-125">max-age</span><span class="sxs-lookup"><span data-stu-id="e1c14-125">max-age</span></span>](https://tools.ietf.org/html/rfc7234#section-5.2.1.1)  | <span data-ttu-id="e1c14-126">클라이언트는 지정된 초 수보다 오래된 응답을 수락하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-126">The client won't accept a response whose age is greater than the specified number of seconds.</span></span> <span data-ttu-id="e1c14-127">예: `max-age=60` (60초), `max-age=2592000` (1개월)</span><span class="sxs-lookup"><span data-stu-id="e1c14-127">Examples: `max-age=60` (60 seconds), `max-age=2592000` (1 month)</span></span> |
| [<span data-ttu-id="e1c14-128">no-cache</span><span class="sxs-lookup"><span data-stu-id="e1c14-128">no-cache</span></span>](https://tools.ietf.org/html/rfc7234#section-5.2.1.4) | <span data-ttu-id="e1c14-129">**요청 시**: 캐시는 저장된 응답을 사용해서 요청에 대응하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-129">**On requests**: A cache must not use a stored response to satisfy the request.</span></span> <span data-ttu-id="e1c14-130">주의: 원본 서버는 클라이언트에 대한 응답을 다시 생성하고 미들웨어는 캐시에 저장된 응답을 갱신해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-130">Note: The origin server re-generates the response for the client, and the middleware updates the stored response in its cache.</span></span><br><br><span data-ttu-id="e1c14-131">**응답 시**: 원본 서버에서 유효성을 검사받지 않은 응답을 후속 요청에 사용하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-131">**On responses**: The response must not be used for a subsequent request without validation on the origin server.</span></span> |
| [<span data-ttu-id="e1c14-132">no-store</span><span class="sxs-lookup"><span data-stu-id="e1c14-132">no-store</span></span>](https://tools.ietf.org/html/rfc7234#section-5.2.1.5) | <span data-ttu-id="e1c14-133">**요청 시**: 캐시가 요청을 저장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-133">**On requests**: A cache must not store the request.</span></span><br><br><span data-ttu-id="e1c14-134">**응답 시**: 캐시가 응답의 모든 부분에서 응답을 저장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-134">**On responses**: A cache must not store any part of the response.</span></span> |

<span data-ttu-id="e1c14-135">캐싱 역할을 수행하는 다른 캐시 헤더는 다음 표와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-135">Other cache headers that play a role in caching are shown in the following table.</span></span>

| <span data-ttu-id="e1c14-136">헤더</span><span class="sxs-lookup"><span data-stu-id="e1c14-136">Header</span></span>                                                     | <span data-ttu-id="e1c14-137">기능</span><span class="sxs-lookup"><span data-stu-id="e1c14-137">Function</span></span> |
| ---------------------------------------------------------- | -------- |
| [<span data-ttu-id="e1c14-138">Age</span><span class="sxs-lookup"><span data-stu-id="e1c14-138">Age</span></span>](https://tools.ietf.org/html/rfc7234#section-5.1)     | <span data-ttu-id="e1c14-139">응답이 생성되거나 원본 서버에서 정상적으로 검증된 이후로부터 지난 초 단위의 총 추정 시간.</span><span class="sxs-lookup"><span data-stu-id="e1c14-139">An estimate of the amount of time in seconds since the response was generated or successfully validated at the origin server.</span></span> |
| [<span data-ttu-id="e1c14-140">Expires</span><span class="sxs-lookup"><span data-stu-id="e1c14-140">Expires</span></span>](https://tools.ietf.org/html/rfc7234#section-5.3) | <span data-ttu-id="e1c14-141">응답이 만료된 것으로 간주되는 날짜/시간.</span><span class="sxs-lookup"><span data-stu-id="e1c14-141">The date/time after which the response is considered stale.</span></span> |
| [<span data-ttu-id="e1c14-142">Pragma</span><span class="sxs-lookup"><span data-stu-id="e1c14-142">Pragma</span></span>](https://tools.ietf.org/html/rfc7234#section-5.4)  | <span data-ttu-id="e1c14-143">`no-cache` 동작 설정에 대한 HTTP/1.0 캐시와의 하위 호환성을 지원하기 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-143">Exists for backwards compatibility with HTTP/1.0 caches for setting `no-cache` behavior.</span></span> <span data-ttu-id="e1c14-144">`Cache-Control` 헤더가 존재할 경우 `Pragma` 헤더는 무시됩니다. </span><span class="sxs-lookup"><span data-stu-id="e1c14-144">If the `Cache-Control` header is present, the `Pragma` header is ignored.</span></span> |
| [<span data-ttu-id="e1c14-145">Vary</span><span class="sxs-lookup"><span data-stu-id="e1c14-145">Vary</span></span>](https://tools.ietf.org/html/rfc7231#section-7.1.4)  | <span data-ttu-id="e1c14-146">모든 `Vary` 헤더 필드가 캐시된 응답의 원본 요청 및 새 요청 모두와 일치하지 않는 한 캐시된 응답이 전송되지 않도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-146">Specifies that a cached response must not be sent unless all of the `Vary` header fields match in both the cached response's original request and the new request.</span></span> |

## <a name="http-based-caching-respects-request-cache-control-directives"></a><span data-ttu-id="e1c14-147">HTTP 기반 캐싱은 Cache-Control 지시문을 준수합니다</span><span class="sxs-lookup"><span data-stu-id="e1c14-147">HTTP-based caching respects request Cache-Control directives</span></span>

<span data-ttu-id="e1c14-148">[Cache-Control 헤더에 대한 HTTP 1.1 캐싱 사양](https://tools.ietf.org/html/rfc7234#section-5.2)은 캐시에게 클라이언트가 전송하는 유효한 `Cache-Control` 헤더를 준수할 것을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-148">The [HTTP 1.1 Caching specification for the Cache-Control header](https://tools.ietf.org/html/rfc7234#section-5.2) requires a cache to honor a valid `Cache-Control` header sent by the client.</span></span> <span data-ttu-id="e1c14-149">클라이언트는 `no-cache` 헤더 값을 설정한 요청을 전송함으로써 모든 요청에 대해 서버가 새로운 응답을 생성하도록 강제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-149">A client can make requests with a `no-cache` header value and force the server to generate a new response for every request.</span></span>

<span data-ttu-id="e1c14-150">HTTP 캐싱의 목적을 고려했을 때 항상 클라이언트의 `Cache-Control` 요청 헤더를 준수하는 것이 이치에 맞습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-150">Always honoring client `Cache-Control` request headers makes sense if you consider the goal of HTTP caching.</span></span> <span data-ttu-id="e1c14-151">공식 사양에서 캐싱은 클라이언트, 프록시 및 서버 간의 네트워크에서 요청의 대기 시간 및 네트워크 오버헤드를 만족스럽게 줄이기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-151">Under the official specification, caching is meant to reduce the latency and network overhead of satisfying requests across a network of clients, proxies, and servers.</span></span> <span data-ttu-id="e1c14-152">원본 서버에서 부하를 제어하기 위한 방법이 필수적인 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-152">It isn't necessarily a way to control the load on an origin server.</span></span>

<span data-ttu-id="e1c14-153">[응답 캐싱 미들웨어](xref:performance/caching/middleware)를 사용할 때 캐싱 동작에 관해서 개발자가 제어할 수 있는 부분은 현재 존재하지 않으며, 그 이유는 미들웨어가 공식 캐싱 사양을 따르고 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-153">There's no current developer control over this caching behavior when using the [Response Caching Middleware](xref:performance/caching/middleware) because the middleware adheres to the official caching specification.</span></span> <span data-ttu-id="e1c14-154">캐시된 응답을 제공하기로 결정할 경우 미들웨어가 요청의 \`Cache-Control\`\` 헤더를 무시하게 구성할 수 있도록 [향후에는 미들웨어를 개선](https://github.com/aspnet/ResponseCaching/issues/96)할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-154">[Future enhancements to the middleware](https://github.com/aspnet/ResponseCaching/issues/96) will permit configuring the middleware to ignore a request's `Cache-Control` header when deciding to serve a cached response.</span></span> <span data-ttu-id="e1c14-155">이렇게 하면 미들웨어를 사용할 때 서버의 부하를 보다 세밀하게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-155">This will offer you an opportunity to better control the load on your server when you use the middleware.</span></span>

## <a name="other-caching-technology-in-aspnet-core"></a><span data-ttu-id="e1c14-156">ASP.NET Core의 다른 캐싱 기술</span><span class="sxs-lookup"><span data-stu-id="e1c14-156">Other caching technology in ASP.NET Core</span></span>

### <a name="in-memory-caching"></a><span data-ttu-id="e1c14-157">메모리 내 캐싱</span><span class="sxs-lookup"><span data-stu-id="e1c14-157">In-memory caching</span></span>

<span data-ttu-id="e1c14-158">메모리 내 캐싱은 서버의 메모리를 이용해서 캐시된 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-158">In-memory caching uses server memory to store cached data.</span></span> <span data-ttu-id="e1c14-159">이 방식의 캐싱은 단일 서버나 *고정 세션*을 사용하는 복수의 서버에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-159">This type of caching is suitable for a single server or multiple servers using *sticky sessions*.</span></span> <span data-ttu-id="e1c14-160">고정 세션은 클라이언트의 요청이 처리를 위해 항상 동일한 서버로 라우트된다는 것을 뜻합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-160">Sticky sessions means that the requests from a client are always routed to the same server for processing.</span></span>

<span data-ttu-id="e1c14-161">자세한 내용은 [메모리 내 캐시](xref:performance/caching/memory)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-161">For more information, see [Cache in-memory](xref:performance/caching/memory).</span></span>

### <a name="distributed-cache"></a><span data-ttu-id="e1c14-162">분산 캐시</span><span class="sxs-lookup"><span data-stu-id="e1c14-162">Distributed Cache</span></span>

<span data-ttu-id="e1c14-163">응용 프로그램이 클라우드나 서버 팜에서 호스팅될 때 메모리에 데이터를 저장하려면 분산 캐시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-163">Use a distributed cache to store data in memory when the app is hosted in a cloud or server farm.</span></span> <span data-ttu-id="e1c14-164">이 캐시는 요청을 처리하는 서버들 간에 서로 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-164">The cache is shared across the servers that process requests.</span></span> <span data-ttu-id="e1c14-165">클라이언트에 대한 캐시 데이터를 사용할 수 있는 경우 클라이언트는 그룹의 어떤 서버에서나 처리할 수 있는 요청을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-165">A client can submit a request that's handled by any server in the group if cached data for the client is available.</span></span> <span data-ttu-id="e1c14-166">ASP.NET Core는 SQL Server 및 Redis 분산 캐시를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-166">ASP.NET Core offers SQL Server and Redis distributed caches.</span></span>

<span data-ttu-id="e1c14-167">자세한 내용은 [분산 캐시 사용하기](xref:performance/caching/distributed)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-167">For more information, see [Work with a distributed cache](xref:performance/caching/distributed).</span></span>

### <a name="cache-tag-helper"></a><span data-ttu-id="e1c14-168">캐시 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="e1c14-168">Cache Tag Helper</span></span>

<span data-ttu-id="e1c14-169">캐시 태그 도우미를 사용하면 MVC 뷰 또는 Razor 페이지의 콘텐츠를 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-169">You can cache the content from an MVC view or Razor Page with the Cache Tag Helper.</span></span> <span data-ttu-id="e1c14-170">캐시 태그 도우미는 메모리 내 캐시에 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-170">The Cache Tag Helper uses in-memory caching to store data.</span></span>

<span data-ttu-id="e1c14-171">자세한 내용은 [ASP.NET Core MVC와 캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-171">For more information, see [Cache Tag Helper in ASP.NET Core MVC](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper).</span></span>

### <a name="distributed-cache-tag-helper"></a><span data-ttu-id="e1c14-172">분산 캐시 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="e1c14-172">Distributed Cache Tag Helper</span></span>

<span data-ttu-id="e1c14-173">분산 캐시 태그 도우미를 사용하면 분산 클라우드 또는 웹 팜 시나리오에서 MVC 뷰 또는 Razor 페이지의 콘텐츠를 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-173">You can cache the content from an MVC view or Razor Page in distributed cloud or web farm scenarios with the Distributed Cache Tag Helper.</span></span> <span data-ttu-id="e1c14-174">분산 캐시 태그 도우미는 SQL Server 또는 Redis에 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-174">The Distributed Cache Tag Helper uses SQL Server or Redis to store data.</span></span>

<span data-ttu-id="e1c14-175">자세한 내용은 [분산 캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-175">For more information, see [Distributed Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper).</span></span>

## <a name="responsecache-attribute"></a><span data-ttu-id="e1c14-176">ResponseCache 특성</span><span class="sxs-lookup"><span data-stu-id="e1c14-176">ResponseCache attribute</span></span>

<span data-ttu-id="e1c14-177">[ResponseCacheAttribute](/dotnet/api/Microsoft.AspNetCore.Mvc.ResponseCacheAttribute) 는 응답 캐싱이 적절한 헤더를 설정하기 위해서 필요한 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-177">The [ResponseCacheAttribute](/dotnet/api/Microsoft.AspNetCore.Mvc.ResponseCacheAttribute) specifies the parameters necessary for setting appropriate headers in response caching.</span></span>

> [!WARNING]
> <span data-ttu-id="e1c14-178">인증된 클라이언트의 정보를 포함하는 콘텐츠는 캐싱하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-178">Disable caching for content that contains information for authenticated clients.</span></span> <span data-ttu-id="e1c14-179">사용자 ID 또는 사용자 로그인 여부와 무관하게 변경되지 않는 콘텐츠만 캐싱해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-179">Caching should only be enabled for content that doesn't change based on a user's identity or whether a user is signed in.</span></span>

<span data-ttu-id="e1c14-180">[VaryByQueryKeys](/dotnet/api/microsoft.aspnetcore.mvc.responsecacheattribute.varybyquerykeys) 속성은 지정한 쿼리 키 목록의 값에 따라 저장된 응답을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-180">[VaryByQueryKeys](/dotnet/api/microsoft.aspnetcore.mvc.responsecacheattribute.varybyquerykeys) varies the stored response by the values of the given list of query keys.</span></span> <span data-ttu-id="e1c14-181">단일 값으로 `*`를 지정하면 모든 쿼리 문자열 매개 변수별로 미들웨어의 응답이 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-181">When a single value of `*` is provided, the middleware varies responses by all request query string parameters.</span></span> <span data-ttu-id="e1c14-182">`VaryByQueryKeys` 를 사용하려면 ASP.NET Core 1.1 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-182">`VaryByQueryKeys` requires ASP.NET Core 1.1 or later.</span></span>

<span data-ttu-id="e1c14-183">응답 캐싱 미들웨어는 반드시 `VaryByQueryKeys` 속성을 설정할 수 있어야 합니다. 그렇지 않을 경우 런타임 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-183">The Response Caching Middleware must be enabled to set the `VaryByQueryKeys` property; otherwise, a runtime exception is thrown.</span></span> <span data-ttu-id="e1c14-184">`VaryByQueryKeys` 속성에 대응하는 HTTP 헤더는 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-184">There isn't a corresponding HTTP header for the `VaryByQueryKeys` property.</span></span> <span data-ttu-id="e1c14-185">이 속성은 응답 캐싱 미들웨어에 의해서 처리되는 HTTP 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-185">The property is an HTTP feature handled by the Response Caching Middleware.</span></span> <span data-ttu-id="e1c14-186">미들웨어가 캐시된 응답을 제공하려면 쿼리 문자열 및 쿼리 문자열 값이 이전 요청과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-186">For the middleware to serve a cached response, the query string and query string value must match a previous request.</span></span> <span data-ttu-id="e1c14-187">예를 들어, 다음 표는 요청 순서에 따른 결과를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-187">For example, consider the sequence of requests and results shown in the following table.</span></span>

| <span data-ttu-id="e1c14-188">요청</span><span class="sxs-lookup"><span data-stu-id="e1c14-188">Request</span></span>                          | <span data-ttu-id="e1c14-189">결과</span><span class="sxs-lookup"><span data-stu-id="e1c14-189">Result</span></span>                   |
| -------------------------------- | ------------------------ |
| `http://example.com?key1=value1` | <span data-ttu-id="e1c14-190">서버에서 반환됨</span><span class="sxs-lookup"><span data-stu-id="e1c14-190">Returned from server</span></span>     |
| `http://example.com?key1=value1` | <span data-ttu-id="e1c14-191">미들웨어에서 반환됨</span><span class="sxs-lookup"><span data-stu-id="e1c14-191">Returned from middleware</span></span> |
| `http://example.com?key1=value2` | <span data-ttu-id="e1c14-192">서버에서 반환됨</span><span class="sxs-lookup"><span data-stu-id="e1c14-192">Returned from server</span></span>     |

<span data-ttu-id="e1c14-193">첫 번째 요청은 서버에서 반환되고 미들웨어에 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-193">The first request is returned by the server and cached in middleware.</span></span> <span data-ttu-id="e1c14-194">두 번째 요청은 쿼리 문자열이 이전 요청과 일치하기 때문에 미들웨어에서 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-194">The second request is returned by middleware because the query string matches the previous request.</span></span> <span data-ttu-id="e1c14-195">세 번째 요청은 쿼리 문자열 값이 이전 요청과 일치하지 않기 때문에 미들웨어 캐시에 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-195">The third request isn't in the middleware cache because the query string value doesn't match a previous request.</span></span> 

<span data-ttu-id="e1c14-196">`ResponseCacheAttribute` 는 [ResponseCacheFilter](/dotnet/api/microsoft.aspnetcore.mvc.internal.responsecachefilter)를 구성하고 생성하기 위해서 (`IFilterFactory`를 통해서) 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-196">The `ResponseCacheAttribute` is used to configure and create (via `IFilterFactory`) a [ResponseCacheFilter](/dotnet/api/microsoft.aspnetcore.mvc.internal.responsecachefilter).</span></span> <span data-ttu-id="e1c14-197">`ResponseCacheFilter` 적절 한 HTTP 헤더 및 응답의 기능을 업데이트 하는 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-197">The `ResponseCacheFilter` performs the work of updating the appropriate HTTP headers and features of the response.</span></span> <span data-ttu-id="e1c14-198">필터:</span><span class="sxs-lookup"><span data-stu-id="e1c14-198">The filter:</span></span>

* <span data-ttu-id="e1c14-199">기존에 존재하는 `Vary`, `Cache-Control` 및 `Pragma` 헤더를 모두 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-199">Removes any existing headers for `Vary`, `Cache-Control`, and `Pragma`.</span></span> 
* <span data-ttu-id="e1c14-200">`ResponseCacheAttribute`에 설정된 속성을 기반으로 적절한 헤더를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-200">Writes out the appropriate headers based on the properties set in the `ResponseCacheAttribute`.</span></span> 
* <span data-ttu-id="e1c14-201">`VaryByQueryKeys` 속성이 설정된 경우 응답 캐싱 HTTP 기능을 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-201">Updates the response caching HTTP feature if `VaryByQueryKeys` is set.</span></span>

### <a name="vary"></a><span data-ttu-id="e1c14-202">Vary</span><span class="sxs-lookup"><span data-stu-id="e1c14-202">Vary</span></span>

<span data-ttu-id="e1c14-203">이 헤더는 `VaryByHeader` 속성이 설정된 경우에만 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-203">This header is only written when the `VaryByHeader` property is set.</span></span> <span data-ttu-id="e1c14-204">이 속성은 `Vary` 헤더의 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-204">It's set to the `Vary` property's value.</span></span> <span data-ttu-id="e1c14-205">다음 예제는 `VaryByHeader` 속성을 사용합니다:</span><span class="sxs-lookup"><span data-stu-id="e1c14-205">The following sample uses the `VaryByHeader` property:</span></span>

[!code-csharp[](response/sample/Controllers/HomeController.cs?name=snippet_VaryByHeader&highlight=1)]

<span data-ttu-id="e1c14-206">브라우저의 네트워크 도구를 사용하면 응답 헤더를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-206">You can view the response headers with your browser's network tools.</span></span> <span data-ttu-id="e1c14-207">다음 그림은 `About2` 액션 메서드를 갱신했을 때 Edge F12 개발자 도구의 **네트워크** 탭의 출력을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-207">The following image shows the Edge F12 output on the **Network** tab when the `About2` action method is refreshed:</span></span>

![About2 액션 메서드 호출 시 Edge F12 개발자 도구의 네트워크 탭의 출력](response/_static/vary.png)

### <a name="nostore-and-locationnone"></a><span data-ttu-id="e1c14-209">NoStore 및 Location.None</span><span class="sxs-lookup"><span data-stu-id="e1c14-209">NoStore and Location.None</span></span>

<span data-ttu-id="e1c14-210">`NoStore` 속성은 다른 대부분의 속성을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-210">`NoStore` overrides most of the other properties.</span></span> <span data-ttu-id="e1c14-211">이 속성이 `true`로 설정되면 `Cache-Control` 헤더가 `no-store`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-211">When this property is set to `true`, the `Cache-Control` header is set to `no-store`.</span></span> <span data-ttu-id="e1c14-212">만약 `Location`이 `None`으로 설정되면:</span><span class="sxs-lookup"><span data-stu-id="e1c14-212">If `Location` is set to `None`:</span></span>

* <span data-ttu-id="e1c14-213">`Cache-Control`이 `no-store,no-cache`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-213">`Cache-Control` is set to `no-store,no-cache`.</span></span>
* <span data-ttu-id="e1c14-214">`Pragma`가 `no-cache`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-214">`Pragma` is set to `no-cache`.</span></span>

<span data-ttu-id="e1c14-215">`NoStore`가 `false`로 그리고 `Location`이 `None`으로 설정되면, `Cache-Control` 및 `Pragma`가 `no-cache`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-215">If `NoStore` is `false` and `Location` is `None`, `Cache-Control` and `Pragma` are set to `no-cache`.</span></span>

<span data-ttu-id="e1c14-216">일반적으로 오류 페이지에서 `NoStore`를 `true`로 설정하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-216">You typically set `NoStore` to `true` on error pages.</span></span> <span data-ttu-id="e1c14-217">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="e1c14-217">For example:</span></span>

[!code-csharp[](response/sample/Controllers/HomeController.cs?name=snippet1&highlight=1)]

<span data-ttu-id="e1c14-218">그 결과 다음과 같은 헤더가 만들어집니다:</span><span class="sxs-lookup"><span data-stu-id="e1c14-218">This results in the following headers:</span></span>

```
Cache-Control: no-store,no-cache
Pragma: no-cache
```

### <a name="location-and-duration"></a><span data-ttu-id="e1c14-219">Location 및 Duration</span><span class="sxs-lookup"><span data-stu-id="e1c14-219">Location and Duration</span></span>

<span data-ttu-id="e1c14-220">캐싱을 사용하기 위해서는 `Duration`을 양수 값으로 설정하고 `Location`이 `Any` (기본값) 또는 `Client`이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-220">To enable caching, `Duration` must be set to a positive value and `Location` must be either `Any` (the default) or `Client`.</span></span> <span data-ttu-id="e1c14-221">이 경우 `Cache-Control` 헤더는 응답의 `max-age`가 뒤에 추가된 위치 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-221">In this case, the `Cache-Control` header is set to the location value followed by the `max-age` of the response.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c14-222">`Location` 옵션의 `Any`와 `Client`는 각각 `Cache-Control` 헤더의 값, `public`과 `private`로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-222">`Location`'s options of `Any` and `Client` translate into `Cache-Control` header values of `public` and `private`, respectively.</span></span> <span data-ttu-id="e1c14-223">앞에서 설명한 것처럼 `Location`을 `None`으로 설정하면 `Cache-Control` 및 `Pragma` 헤더가 모두 `no-cache`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-223">As noted previously, setting `Location` to `None` sets both `Cache-Control` and `Pragma` headers to `no-cache`.</span></span>

<span data-ttu-id="e1c14-224">다음은 `Duration`을 설정하고 `Location`을 기본 값 그대로 변경하지 않고 생성하는 헤더를 보여주는 예제입니다:</span><span class="sxs-lookup"><span data-stu-id="e1c14-224">Below is an example showing the headers produced by setting `Duration` and leaving the default `Location` value:</span></span>

[!code-csharp[](response/sample/Controllers/HomeController.cs?name=snippet_duration&highlight=1)]

<span data-ttu-id="e1c14-225">이 코드는 다음과 같은 헤더를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-225">This produces the following header:</span></span>

```
Cache-Control: public,max-age=60
```

### <a name="cache-profiles"></a><span data-ttu-id="e1c14-226">캐시 프로필</span><span class="sxs-lookup"><span data-stu-id="e1c14-226">Cache profiles</span></span>

<span data-ttu-id="e1c14-227">수 많은 컨트롤러 액션 속성마다 `ResponseCache` 설정을 반복하는 대신, `Startup`의 `ConfigureServices` 메서드에서 MVC를 설정할 때 캐시 프로필을 옵션으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-227">Instead of duplicating `ResponseCache` settings on many controller action attributes, cache profiles can be configured as options when setting up MVC in the `ConfigureServices` method in `Startup`.</span></span> <span data-ttu-id="e1c14-228">참조된 캐시 프로필에 지정된 값은 `ResponseCache` 특성에 의해 기본값으로 사용되며 특성에 지정된 모든 속성에 의해 덮어써집니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-228">Values found in a referenced cache profile are used as the defaults by the `ResponseCache` attribute and are overridden by any properties specified on the attribute.</span></span>

<span data-ttu-id="e1c14-229">먼저 캐시 프로필을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-229">Setting up a cache profile:</span></span>

[!code-csharp[](response/sample/Startup.cs?name=snippet1)] 

<span data-ttu-id="e1c14-230">그리고 캐시 프로필을 참조합니다:</span><span class="sxs-lookup"><span data-stu-id="e1c14-230">Referencing a cache profile:</span></span>

[!code-csharp[](response/sample/Controllers/HomeController.cs?name=snippet_controller&highlight=1,4)]

<span data-ttu-id="e1c14-231">`ResponseCache` 특성은 액션(메서드) 및 컨트롤러(클래스) 모두에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-231">The `ResponseCache` attribute can be applied both to actions (methods) and controllers (classes).</span></span> <span data-ttu-id="e1c14-232">메서드 수준 특성은 클래스 수준 특성에 지정된 설정을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-232">Method-level attributes override the settings specified in class-level attributes.</span></span>

<span data-ttu-id="e1c14-233">위의 예제에서는 클래스 수준 특성이 30초의 지속 시간을 지정하는 반면, 메서드 수준 특성은 지속 시간이 60초로 설정된 캐시 프로필을 참조하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1c14-233">In the above example, a class-level attribute specifies a duration of 30 seconds, while a method-level attribute references a cache profile with a duration set to 60 seconds.</span></span>

<span data-ttu-id="e1c14-234">결과 헤더:</span><span class="sxs-lookup"><span data-stu-id="e1c14-234">The resulting header:</span></span>

```
Cache-Control: public,max-age=60
```

## <a name="additional-resources"></a><span data-ttu-id="e1c14-235">추가 자료</span><span class="sxs-lookup"><span data-stu-id="e1c14-235">Additional resources</span></span>

* [<span data-ttu-id="e1c14-236">캐시에 응답 저장하기</span><span class="sxs-lookup"><span data-stu-id="e1c14-236">Storing Responses in Caches</span></span>](https://tools.ietf.org/html/rfc7234#section-3)
* [<span data-ttu-id="e1c14-237">Cache-Control</span><span class="sxs-lookup"><span data-stu-id="e1c14-237">Cache-Control</span></span>](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="e1c14-238">메모리 내 캐시</span><span class="sxs-lookup"><span data-stu-id="e1c14-238">Cache in-memory</span></span>](xref:performance/caching/memory)
* [<span data-ttu-id="e1c14-239">분산 캐시 사용하기</span><span class="sxs-lookup"><span data-stu-id="e1c14-239">Work with a distributed cache</span></span>](xref:performance/caching/distributed)
* [<span data-ttu-id="e1c14-240">변경 토큰을 이용해서 변경 감지하기</span><span class="sxs-lookup"><span data-stu-id="e1c14-240">Detect changes with change tokens</span></span>](xref:fundamentals/primitives/change-tokens)
* [<span data-ttu-id="e1c14-241">응답 캐싱 미들웨어</span><span class="sxs-lookup"><span data-stu-id="e1c14-241">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
* [<span data-ttu-id="e1c14-242">캐시 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="e1c14-242">Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [<span data-ttu-id="e1c14-243">분산 캐시 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="e1c14-243">Distributed Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
