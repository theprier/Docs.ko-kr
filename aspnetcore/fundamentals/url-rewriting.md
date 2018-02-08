---
title: "ASP.NET Core에서 URL 재작성 미들웨어"
author: guardrex
description: "ASP.NET Core 응용 프로그램에서 URL 재작성 미들웨어로 URL 재작성 및 리디렉션에 대해 알아봅니다."
manager: wpickett
ms.author: riande
ms.date: 08/17/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/url-rewriting
ms.openlocfilehash: ca1f2f366bcf12cd3df83c3cdefa460cb9a68e2a
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="url-rewriting-middleware-in-aspnet-core"></a><span data-ttu-id="b652a-103">ASP.NET Core에서 URL 재작성 미들웨어</span><span class="sxs-lookup"><span data-stu-id="b652a-103">URL Rewriting Middleware in ASP.NET Core</span></span>

<span data-ttu-id="b652a-104">작성자: [Luke Latham](https://github.com/guardrex) 및 [Mikael Mengistu](https://github.com/mikaelm12)</span><span class="sxs-lookup"><span data-stu-id="b652a-104">By [Luke Latham](https://github.com/guardrex) and [Mikael Mengistu](https://github.com/mikaelm12)</span></span>

<span data-ttu-id="b652a-105">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="b652a-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="b652a-106">URL 재작성은 하나 이상의 미리 정의된 규칙을 기반으로 하는 요청 URL을 수정하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-106">URL rewriting is the act of modifying request URLs based on one or more predefined rules.</span></span> <span data-ttu-id="b652a-107">URL 재작성은 위치 및 주소가 밀접하게 연결되지 않도록 리소스 위치와 해당 주소 간의 추상화를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-107">URL rewriting creates an abstraction between resource locations and their addresses so that the locations and addresses are not tightly linked.</span></span> <span data-ttu-id="b652a-108">URL 재작성이 중요한 몇 가지 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-108">There are several scenarios where URL rewriting is valuable:</span></span>
* <span data-ttu-id="b652a-109">이러한 리소스에 대한 안정적인 로케이터를 유지 관리하는 동안 서버 리소스를 일시적 또는 영구적으로 이동 또는 대체</span><span class="sxs-lookup"><span data-stu-id="b652a-109">Moving or replacing server resources temporarily or permanently while maintaining stable locators for those resources</span></span>
* <span data-ttu-id="b652a-110">서로 다른 앱 또는 하나의 앱 영역에서 처리 중인 요청 분리</span><span class="sxs-lookup"><span data-stu-id="b652a-110">Splitting request processing across different apps or across areas of one app</span></span>
* <span data-ttu-id="b652a-111">들어오는 요청에서 URL 세그먼트 제거, 추가 또는 다시 구성</span><span class="sxs-lookup"><span data-stu-id="b652a-111">Removing, adding, or reorganizing URL segments on incoming requests</span></span>
* <span data-ttu-id="b652a-112">SEO(검색 엔진 최적화)에 대한 공용 URL 최적화</span><span class="sxs-lookup"><span data-stu-id="b652a-112">Optimizing public URLs for Search Engine Optimization (SEO)</span></span>
* <span data-ttu-id="b652a-113">사용자가 링크를 따라 찾는 콘텐츠를 예측하는 데 도움이 되도록 친숙한 공용 URL의 사용을 허용</span><span class="sxs-lookup"><span data-stu-id="b652a-113">Permitting the use of friendly public URLs to help people predict the content they will find by following a link</span></span>
* <span data-ttu-id="b652a-114">엔드포인트를 보호하도록 안전하지 않은 요청 리디렉션</span><span class="sxs-lookup"><span data-stu-id="b652a-114">Redirecting insecure requests to secure endpoints</span></span>
* <span data-ttu-id="b652a-115">이미지 핫링크 방지</span><span class="sxs-lookup"><span data-stu-id="b652a-115">Preventing image hotlinking</span></span>

<span data-ttu-id="b652a-116">정규식, Apache mod_rewrite 모듈 규칙, IIS 다시 쓰기 모듈 규칙 및 사용자 지정 규칙 논리를 사용하는 등의 여러 가지 방법으로 URL 변경을 위한 규칙을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-116">You can define rules for changing the URL in several ways, including regex, Apache mod_rewrite module rules, IIS Rewrite Module rules, and using custom rule logic.</span></span> <span data-ttu-id="b652a-117">이 문서는 ASP.NET Core 앱에서 URL 재작성 미들웨어를 사용하는 방법에 대한 지침이 포함된 URL 재작성을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-117">This document introduces URL rewriting with instructions on how to use URL Rewriting Middleware in ASP.NET Core apps.</span></span>

> [!NOTE]
> <span data-ttu-id="b652a-118">URL 재작성은 앱의 성능을 저하시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-118">URL rewriting can reduce the performance of an app.</span></span> <span data-ttu-id="b652a-119">가능한 경우 규칙의 수와 복잡성을 제한해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-119">Where feasible, you should limit the number and complexity of rules.</span></span>

## <a name="url-redirect-and-url-rewrite"></a><span data-ttu-id="b652a-120">URL 리디렉션 및 URL 재작성</span><span class="sxs-lookup"><span data-stu-id="b652a-120">URL redirect and URL rewrite</span></span>
<span data-ttu-id="b652a-121">*URL 리디렉션* 및 *URL 재작성* 간 단어의 차이점은 처음에는 미묘해 보일 수 있지만 클라이언트에 리소스를 제공하는 데 중요한 의미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-121">The difference in wording between *URL redirect* and *URL rewrite* may seem subtle at first but has important implications for providing resources to clients.</span></span> <span data-ttu-id="b652a-122">ASP.NET Core의 URL 재작성 미들웨어는 모두에 대한 필요성을 충족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-122">ASP.NET Core's URL Rewriting Middleware is capable of meeting the need for both.</span></span>

<span data-ttu-id="b652a-123">*URL 리디렉션*은 클라이언트 쪽 작업으로, 클라이언트는 다른 주소에서 리소스에 액세스하도록 지시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-123">A *URL redirect* is a client-side operation, where the client is instructed to access a resource at another address.</span></span> <span data-ttu-id="b652a-124">서버에 대한 왕복 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-124">This requires a round-trip to the server.</span></span> <span data-ttu-id="b652a-125">클라이언트로 반환된 리디렉션 URL은 클라이언트가 리소스에 대한 새 요청을 만들 때 브라우저의 주소 표시줄에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-125">The redirect URL returned to the client appears in the browser's address bar when the client makes a new request for the resource.</span></span> 

<span data-ttu-id="b652a-126">`/resource`가 `/different-resource`로 *리디렉션*된 경우 클라이언트는 `/resource`를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-126">If `/resource` is *redirected* to `/different-resource`, the client requests `/resource`.</span></span> <span data-ttu-id="b652a-127">서버는 클라이언트가 리디렉션이 임시 또는 영구임을 나타내는 상태 코드와 함께 `/different-resource`에서 리소스를 가져와야 한다고 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-127">The server responds that the client should obtain the resource at `/different-resource` with a status code indicating that the redirect is either temporary or permanent.</span></span> <span data-ttu-id="b652a-128">클라이언트는 리디렉션 URL에서 리소스에 대한 새 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-128">The client executes a new request for the resource at the redirect URL.</span></span>

![WebAPI 서비스 엔드포인트는 서버에서 버전 1(v1)에서 버전 2(v2)로 임시적으로 변경되었습니다.](url-rewriting/_static/url_redirect.png)

<span data-ttu-id="b652a-134">요청을 다른 URL로 리디렉션하는 경우 리디렉션이 영구 또는 임시인지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-134">When redirecting requests to a different URL, you indicate whether the redirect is permanent or temporary.</span></span> <span data-ttu-id="b652a-135">301(영구적 이동) 상태 코드는 리소스에 새, 영구 URL이 있고 리소스에 대한 모든 향후 요청이 새 URL을 사용해야 함을 클라이언트에게 지시하려는 경우에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-135">The 301 (Moved Permanently) status code is used where the resource has a new, permanent URL and you wish to instruct the client that all future requests for the resource should use the new URL.</span></span> <span data-ttu-id="b652a-136">*클라이언트는 301 상태 코드를 받을 때 응답을 캐시할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="b652a-136">*The client may cache the response when a 301 status code is received.*</span></span> <span data-ttu-id="b652a-137">302(있음) 상태 코드는 리디렉션이 임시이거나 일반적으로 변경될 수 있는 경우에 사용됩니다. 클라이언트는 향후에 리디렉션 URL을 저장 및 다시 사용하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-137">The 302 (Found) status code is used where the redirection is temporary or generally subject to change, such that the client shouldn't store and reuse the redirect URL in the future.</span></span> <span data-ttu-id="b652a-138">자세한 내용은 [RFC 2616: 상태 코드 정의](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b652a-138">For more information, see [RFC 2616: Status Code Definitions](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).</span></span>

<span data-ttu-id="b652a-139">*URL 재작성*은 다른 리소스 주소에서 리소스를 제공하는 서버 쪽 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-139">A *URL rewrite* is a server-side operation to provide a resource from a different resource address.</span></span> <span data-ttu-id="b652a-140">URL 재작성은 서버에 대한 왕복 작업이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-140">Rewriting a URL doesn't require a round-trip to the server.</span></span> <span data-ttu-id="b652a-141">재작성된 URL은 클라이언트에 반환되지 않으며 브라우저의 주소 표시줄에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-141">The rewritten URL isn't returned to the client and won't appear in the browser's address bar.</span></span> <span data-ttu-id="b652a-142">`/resource`가 `/different-resource`로 *재작성*되는 경우 클라이언트는 `/resource`를 요청하고, 서버는 *내부적으로* `/different-resource`에서 리소스를 페치합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-142">When `/resource` is *rewritten* to `/different-resource`, the client requests `/resource`, and the server *internally* fetches the resource at `/different-resource`.</span></span> <span data-ttu-id="b652a-143">클라이언트는 재작성된 URL에서 리소스를 검색할 수 있지만 클라이언트는 해당 요청을 만들고 응답을 받을 때 리소스가 재작성된 URL에 있다는 것을 알림 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-143">Although the client might be able to retrieve the resource at the rewritten URL, the client won't be informed that the resource exists at the rewritten URL when it makes its request and receives the response.</span></span>

![WebAPI 서비스 엔드포인트는 서버에서 버전 1(v1)에서 버전 2(v2)로 변경되었습니다.](url-rewriting/_static/url_rewrite.png)

## <a name="url-rewriting-sample-app"></a><span data-ttu-id="b652a-148">URL 재작성 샘플 앱</span><span class="sxs-lookup"><span data-stu-id="b652a-148">URL rewriting sample app</span></span>
<span data-ttu-id="b652a-149">[URL 재작성 샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/)을 사용하여 URL 재작성 미들웨어의 기능을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-149">You can explore the features of the URL Rewriting Middleware with the [URL rewriting sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/).</span></span> <span data-ttu-id="b652a-150">앱은 재작성 및 리디렉션 규칙을 적용하고 재작성 또는 리디렉션된 URL을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-150">The app applies rewrite and redirect rules and shows the rewritten or redirected URL.</span></span>

## <a name="when-to-use-url-rewriting-middleware"></a><span data-ttu-id="b652a-151">URL 재작성 미들웨어를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="b652a-151">When to use URL Rewriting Middleware</span></span>
<span data-ttu-id="b652a-152">Windows Server에서 IIS, Apache Server에서 [Apache mod_rewrite 모듈](https://httpd.apache.org/docs/2.4/rewrite/), [Nginx에서 URL 재작성](https://www.nginx.com/blog/creating-nginx-rewrite-rules/)으로 [URL 재작성 모듈](https://www.iis.net/downloads/microsoft/url-rewrite)을 사용할 수 없거나 앱이 [HTTP.sys 서버](xref:fundamentals/servers/httpsys)(이전에 [WebListener](xref:fundamentals/servers/weblistener)라고 함)에서 호스팅되는 경우 URL 재작성 미들웨어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-152">Use URL Rewriting Middleware when you are unable to use the [URL Rewrite module](https://www.iis.net/downloads/microsoft/url-rewrite) with IIS on Windows Server, the [Apache mod_rewrite module](https://httpd.apache.org/docs/2.4/rewrite/) on Apache Server, [URL rewriting on Nginx](https://www.nginx.com/blog/creating-nginx-rewrite-rules/), or your app is hosted on [HTTP.sys server](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)).</span></span> <span data-ttu-id="b652a-153">IIS, Apache 또는 Nginx에서 서버 기반 URL 재작성 기술을 사용하는 주된 이유는 미들웨어가 이러한 모듈의 전체 기능을 지원하지 않고 미들웨어의 성능이 아마도 모듈의 성능과 일치하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-153">The main reasons to use the server-based URL rewriting technologies in IIS, Apache, or Nginx are that the middleware doesn't support the full features of these modules and the performance of the middleware probably won't match that of the modules.</span></span> <span data-ttu-id="b652a-154">그러나 IIS 재작성 모듈의 `IsFile` 및 `IsDirectory` 제약 조건과 같은 ASP.NET Core 프로젝트를 사용하지 않는 서버 모듈의 일부 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-154">However, there are some features of the server modules that don't work with ASP.NET Core projects, such as the `IsFile` and `IsDirectory` constraints of the IIS Rewrite module.</span></span> <span data-ttu-id="b652a-155">이러한 시나리오에서 미들웨어를 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-155">In these scenarios, use the middleware instead.</span></span>

## <a name="package"></a><span data-ttu-id="b652a-156">패키지</span><span class="sxs-lookup"><span data-stu-id="b652a-156">Package</span></span>
<span data-ttu-id="b652a-157">미들웨어를 프로젝트에 포함하려면 [`Microsoft.AspNetCore.Rewrite`](https://www.nuget.org/packages/Microsoft.AspNetCore.Rewrite/) 패키지에 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-157">To include the middleware in your project, add a reference to the [`Microsoft.AspNetCore.Rewrite`](https://www.nuget.org/packages/Microsoft.AspNetCore.Rewrite/) package.</span></span> <span data-ttu-id="b652a-158">이 기능은 ASP.NET Core 1.1 이상을 대상으로 하는 앱에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-158">This feature is available for apps that target ASP.NET Core 1.1 or later.</span></span>

## <a name="extension-and-options"></a><span data-ttu-id="b652a-159">확장 및 옵션</span><span class="sxs-lookup"><span data-stu-id="b652a-159">Extension and options</span></span>
<span data-ttu-id="b652a-160">각 규칙에 대한 확장 메서드로 `RewriteOptions` 클래스의 인스턴스를 만들어 URL 재작성을 설정하고 규칙을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-160">Establish your URL rewrite and redirect rules by creating an instance of the `RewriteOptions` class with extension methods for each of your rules.</span></span> <span data-ttu-id="b652a-161">처리하려는 순서로 여러 규칙을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-161">Chain multiple rules in the order that you would like them processed.</span></span> <span data-ttu-id="b652a-162">`RewriteOptions`는 `app.UseRewriter(options);`로 요청 파이프라인에 추가되므로 URL 재작성 미들웨어로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-162">The `RewriteOptions` are passed into the URL Rewriting Middleware as it's added to the request pipeline with `app.UseRewriter(options);`.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b652a-163">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b652a-163">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b652a-164">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b652a-164">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1)]

---

### <a name="url-redirect"></a><span data-ttu-id="b652a-165">URL 리디렉션</span><span class="sxs-lookup"><span data-stu-id="b652a-165">URL redirect</span></span>
<span data-ttu-id="b652a-166">`AddRedirect`를 사용하여 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-166">Use `AddRedirect` to redirect requests.</span></span> <span data-ttu-id="b652a-167">첫 번째 매개 변수는 들어오는 URL의 경로에서 일치를 위해 정규식을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-167">The first parameter contains your regex for matching on the path of the incoming URL.</span></span> <span data-ttu-id="b652a-168">두 번째 매개 변수는 대체 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-168">The second parameter is the replacement string.</span></span> <span data-ttu-id="b652a-169">세 번째 매개 변수는 있는 경우 상태 코드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-169">The third parameter, if present, specifies the status code.</span></span> <span data-ttu-id="b652a-170">상태 코드를 지정하지 않는 경우 기본값을 리소스가 일시적으로 이동 또는 대체되었음을 나타내는 302(있음)로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-170">If you don't specify the status code, it defaults to 302 (Found), which indicates that the resource is temporarily moved or replaced.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b652a-171">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b652a-171">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=5)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b652a-172">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b652a-172">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=2)]

---

<span data-ttu-id="b652a-173">개발자 도구가 활성화된 브라우저에서 `/redirect-rule/1234/5678` 경로로 샘플 앱에 대한 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-173">In a browser with developer tools enabled, make a request to the sample app with the path `/redirect-rule/1234/5678`.</span></span> <span data-ttu-id="b652a-174">정규식은 `redirect-rule/(.*)`에서 요청 경로와 일치하고 경로는 `/redirected/1234/5678`로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-174">The regex matches the request path on `redirect-rule/(.*)`, and the path is replaced with `/redirected/1234/5678`.</span></span> <span data-ttu-id="b652a-175">리디렉션 URL은 302(있음) 상태 코드로 클라이언트에 다시 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-175">The redirect URL is sent back to the client with a 302 (Found) status code.</span></span> <span data-ttu-id="b652a-176">브라우저에서 브라우저의 주소 표시줄에 표시되는 리디렉션 URL에서 새 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-176">The browser makes a new request at the redirect URL, which appears in the browser's address bar.</span></span> <span data-ttu-id="b652a-177">샘플 앱의 규칙은 리디렉션 URL에서 일치하지 않으므로 두 번째 요청은 앱에서 200(정상) 응답을 수신하고 응답의 본문은 리디렉션 URL을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-177">Since no rules in the sample app match on the redirect URL, the second request receives a 200 (OK) response from the app and the body of the response shows the redirect URL.</span></span> <span data-ttu-id="b652a-178">URL이 *리디렉션*될 때 서버에 대한 왕복 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-178">A roundtrip is made to the server when a URL is *redirected*.</span></span>

> [!WARNING]
> <span data-ttu-id="b652a-179">리디렉션 규칙을 설정할 때 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-179">Be cautious when establishing your redirect rules.</span></span> <span data-ttu-id="b652a-180">리디렉션 규칙은 리디렉션 후를 포함하여 앱에 대한 각 요청에서 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-180">Your redirect rules are evaluated on each request to the app, including after a redirect.</span></span> <span data-ttu-id="b652a-181">실수로 무한 리디렉션의 루프를 생성하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-181">It's easy to accidently create a loop of infinite redirects.</span></span>

<span data-ttu-id="b652a-182">원래 요청: `/redirect-rule/1234/5678`</span><span class="sxs-lookup"><span data-stu-id="b652a-182">Original Request: `/redirect-rule/1234/5678`</span></span>

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect.png)

<span data-ttu-id="b652a-184">괄호 안에 포함된 식의 일부는 *캡처 그룹*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-184">The part of the expression contained within parentheses is called a *capture group*.</span></span> <span data-ttu-id="b652a-185">식의 점(`.`)은 *모든 문자 일치*를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-185">The dot (`.`) of the expression means *match any character*.</span></span> <span data-ttu-id="b652a-186">별표(`*`)는 *0회 이상 이전 문자와 일치*를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-186">The asterisk (`*`) indicates *match the preceding character zero or more times*.</span></span> <span data-ttu-id="b652a-187">따라서 URL, `1234/5678`의 마지막 두 경로 세그먼트는 캡처 그룹 `(.*)`에 의해 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-187">Therefore, the last two path segments of the URL, `1234/5678`, are captured by capture group `(.*)`.</span></span> <span data-ttu-id="b652a-188">`redirect-rule/` 후 요청 URL에서 제공하는 값은 이 단일 캡처 그룹에 의해 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-188">Any value you provide in the request URL after `redirect-rule/` is captured by this single capture group.</span></span>

<span data-ttu-id="b652a-189">대체 문자열에서 캡처된 그룹은 캡처의 시퀀스 번호가 뒤에 오는 달러 기호(`$`)를 사용하여 문자열에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-189">In the replacement string, captured groups are injected into the string with the dollar sign (`$`) followed by the sequence number of the capture.</span></span> <span data-ttu-id="b652a-190">첫 번째 캡처 그룹 값은 `$1`로 획득되고, 두 번째는 `$2`로 획득되며, 정규식의 캡처 그룹에 대한 시퀀스에서 지속합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-190">The first capture group value is obtained with `$1`, the second with `$2`, and they continue in sequence for the capture groups in your regex.</span></span> <span data-ttu-id="b652a-191">샘플 앱의 리디렉션 규칙 정규식에 캡처된 그룹이 하나만 있으므로 대체 문자열에 삽입된 그룹은 하나입니다. 이는 `$1`입니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-191">There's only one captured group in the redirect rule regex in the sample app, so there's only one injected group in the replacement string, which is `$1`.</span></span> <span data-ttu-id="b652a-192">규칙이 적용되면 URL은 `/redirected/1234/5678`이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-192">When the rule is applied, the URL becomes `/redirected/1234/5678`.</span></span>

<a name="url-redirect-to-secure-endpoint"></a>
### <a name="url-redirect-to-a-secure-endpoint"></a><span data-ttu-id="b652a-193">보안 엔드포인트에 대한 URL 리디렉션</span><span class="sxs-lookup"><span data-stu-id="b652a-193">URL redirect to a secure endpoint</span></span>
<span data-ttu-id="b652a-194">`AddRedirectToHttps`를 사용하여 HTTP 요청을 동일한 호스트 및 HTTPS(`https://`)를 사용하는 경로에 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-194">Use `AddRedirectToHttps` to redirect HTTP requests to the same host and path using HTTPS (`https://`).</span></span> <span data-ttu-id="b652a-195">상태 코드가 제공되지 않는 경우 미들웨어는 302(있음)로 기본값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-195">If the status code isn't supplied, the middleware defaults to 302 (Found).</span></span> <span data-ttu-id="b652a-196">포트가 제공되지 않는 경우 미들웨어는 기본값을 `null`로 설정합니다. 이는 프로토콜이 `https://`로 변경되고 클라이언트가 포트 443에서 리소스에 액세스하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-196">If the port isn't supplied, the middleware defaults to `null`, which means the protocol changes to `https://` and the client accesses the resource on port 443.</span></span> <span data-ttu-id="b652a-197">예제는 상태 코드를 301(영구적 이동)로 설정하고 포트를 5001로 변경하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-197">The example shows how to set the status code to 301 (Moved Permanently) and change the port to 5001.</span></span>
```csharp
var options = new RewriteOptions()
    .AddRedirectToHttps(301, 5001);

app.UseRewriter(options);
```
<span data-ttu-id="b652a-198">`AddRedirectToHttpsPermanent`를 사용하여 안전하지 않은 요청을 동일한 호스트와 보안 HTTPS 프로토콜(포트 443의 `https://`)이 있는 경로로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-198">Use `AddRedirectToHttpsPermanent` to redirect insecure requests to the same host and path with secure HTTPS protocol (`https://` on port 443).</span></span> <span data-ttu-id="b652a-199">미들웨어는 상태 코드를 301(영구적 이동)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-199">The middleware sets the status code to 301 (Moved Permanently).</span></span>

<span data-ttu-id="b652a-200">샘플 앱은 `AddRedirectToHttps` 또는 `AddRedirectToHttpsPermanent`를 사용하는 방법을 보여 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-200">The sample app is capable of demonstrating how to use `AddRedirectToHttps` or `AddRedirectToHttpsPermanent`.</span></span> <span data-ttu-id="b652a-201">확장 메서드를 `RewriteOptions`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-201">Add the extension method to the `RewriteOptions`.</span></span> <span data-ttu-id="b652a-202">모든 URL에서 앱에 대한 안전하지 않은 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-202">Make an insecure request to the app at any URL.</span></span> <span data-ttu-id="b652a-203">자체 서명된 인증서를 신뢰할 수 없다는 브라우저 보안 경고를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-203">Dismiss the browser security warning that the self-signed certificate is untrusted.</span></span>

<span data-ttu-id="b652a-204">`AddRedirectToHttps(301, 5001)`를 사용하는 원래 요청: `/secure`</span><span class="sxs-lookup"><span data-stu-id="b652a-204">Original Request using `AddRedirectToHttps(301, 5001)`: `/secure`</span></span>

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_to_https.png)

<span data-ttu-id="b652a-206">`AddRedirectToHttpsPermanent`를 사용하는 원래 요청: `/secure`</span><span class="sxs-lookup"><span data-stu-id="b652a-206">Original Request using `AddRedirectToHttpsPermanent`: `/secure`</span></span>

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_to_https_permanent.png)

### <a name="url-rewrite"></a><span data-ttu-id="b652a-208">URL 재작성</span><span class="sxs-lookup"><span data-stu-id="b652a-208">URL rewrite</span></span>
<span data-ttu-id="b652a-209">`AddRewrite`를 사용하여 URL을 재작성하기 위한 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-209">Use `AddRewrite` to create a rule for rewriting URLs.</span></span> <span data-ttu-id="b652a-210">첫 번째 매개 변수는 들어오는 URL 경로에서 일치를 위한 정규식을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-210">The first parameter contains your regex for matching on the incoming URL path.</span></span> <span data-ttu-id="b652a-211">두 번째 매개 변수는 대체 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-211">The second parameter is the replacement string.</span></span> <span data-ttu-id="b652a-212">세 번째 매개 변수, `skipRemainingRules: {true|false}`는 현재 규칙이 적용되는 경우에 추가 재작성 규칙을 건너뛸 것인지 여부를 미들웨어에 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-212">The third parameter, `skipRemainingRules: {true|false}`, indicates to the middleware whether or not to skip additional rewrite rules if the current rule is applied.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b652a-213">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b652a-213">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=6)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b652a-214">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b652a-214">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=3)]

---

<span data-ttu-id="b652a-215">원래 요청: `/rewrite-rule/1234/5678`</span><span class="sxs-lookup"><span data-stu-id="b652a-215">Original Request: `/rewrite-rule/1234/5678`</span></span>

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_rewrite.png)

<span data-ttu-id="b652a-217">정규식에서 발견한 첫 번째 사항은 식 시작 부분에 있는 캐럿(`^`)입니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-217">The first thing you notice in the regex is the carat (`^`) at the beginning of the expression.</span></span> <span data-ttu-id="b652a-218">이는 URL 경로의 시작 부분에서 일치하는 시작을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-218">This means that matching starts at the beginning of the URL path.</span></span>

<span data-ttu-id="b652a-219">리디렉션 규칙, `redirect-rule/(.*)`이 있는 앞의 예제에서 정규식의 시작 부분에 캐럿이 없으므로 모든 문자는 성공한 일치에 대한 경로에서 `redirect-rule/`을 앞설 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-219">In the earlier example with the redirect rule, `redirect-rule/(.*)`, there's no carat at the start of the regex; therefore, any characters may precede `redirect-rule/` in the path for a successful match.</span></span>

| <span data-ttu-id="b652a-220">Path</span><span class="sxs-lookup"><span data-stu-id="b652a-220">Path</span></span>                               | <span data-ttu-id="b652a-221">일치</span><span class="sxs-lookup"><span data-stu-id="b652a-221">Match</span></span> |
| ---------------------------------- | :---: |
| `/redirect-rule/1234/5678`         | <span data-ttu-id="b652a-222">예</span><span class="sxs-lookup"><span data-stu-id="b652a-222">Yes</span></span>   |
| `/my-cool-redirect-rule/1234/5678` | <span data-ttu-id="b652a-223">예</span><span class="sxs-lookup"><span data-stu-id="b652a-223">Yes</span></span>   |
| `/anotherredirect-rule/1234/5678`  | <span data-ttu-id="b652a-224">예</span><span class="sxs-lookup"><span data-stu-id="b652a-224">Yes</span></span>   |

<span data-ttu-id="b652a-225">재작성 규칙, `^rewrite-rule/(\d+)/(\d+)`는 `rewrite-rule/`로 시작하는 경우에 경로와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-225">The rewrite rule, `^rewrite-rule/(\d+)/(\d+)`, only matches paths if they start with `rewrite-rule/`.</span></span> <span data-ttu-id="b652a-226">아래 재작성 규칙과 위의 리디렉션 규칙 간 일치에서 차이점을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-226">Notice the difference in matching between the rewrite rule below and the redirect rule above.</span></span>

| <span data-ttu-id="b652a-227">Path</span><span class="sxs-lookup"><span data-stu-id="b652a-227">Path</span></span>                              | <span data-ttu-id="b652a-228">일치</span><span class="sxs-lookup"><span data-stu-id="b652a-228">Match</span></span> |
| --------------------------------- | :---: |
| `/rewrite-rule/1234/5678`         | <span data-ttu-id="b652a-229">예</span><span class="sxs-lookup"><span data-stu-id="b652a-229">Yes</span></span>   |
| `/my-cool-rewrite-rule/1234/5678` | <span data-ttu-id="b652a-230">아니요</span><span class="sxs-lookup"><span data-stu-id="b652a-230">No</span></span>    |
| `/anotherrewrite-rule/1234/5678`  | <span data-ttu-id="b652a-231">아니요</span><span class="sxs-lookup"><span data-stu-id="b652a-231">No</span></span>    |

<span data-ttu-id="b652a-232">식의 `^rewrite-rule/` 부분을 따릅니다. 두 개의 캡처 그룹, `(\d+)/(\d+)`가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-232">Following the `^rewrite-rule/` portion of the expression, there are two capture groups, `(\d+)/(\d+)`.</span></span> <span data-ttu-id="b652a-233">`\d`는 *숫자 일치*를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-233">The `\d` signifies *match a digit (number)*.</span></span> <span data-ttu-id="b652a-234">더하기 기호(`+`)는 *하나 이상의 앞에 오는 문자와 일치*를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-234">The plus sign (`+`) means *match one or more of the preceding character*.</span></span> <span data-ttu-id="b652a-235">따라서 URL은 슬래시와 다른 숫자가 잇따라 뒤에 오는 숫자를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-235">Therefore, the URL must contain a number followed by a forward-slash followed by another number.</span></span> <span data-ttu-id="b652a-236">이러한 캡처 그룹은 `$1` 및 `$2`로 재작성 URL에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-236">These capture groups are injected into the rewritten URL as `$1` and `$2`.</span></span> <span data-ttu-id="b652a-237">재작성 규칙 대체 문자열은 캡처된 그룹을 쿼리 문자열에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-237">The rewrite rule replacement string places the captured groups into the querystring.</span></span> <span data-ttu-id="b652a-238">`/rewrite-rule/1234/5678`의 요청된 경로는 `/rewritten?var1=1234&var2=5678`에서 리소스를 가져오도록 재작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-238">The requested path of `/rewrite-rule/1234/5678` is rewritten to obtain the resource at `/rewritten?var1=1234&var2=5678`.</span></span> <span data-ttu-id="b652a-239">쿼리 문자열이 원래 요청에 있는 경우 URL이 재작성될 때 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-239">If a querystring is present on the original request, it's preserved when the URL is rewritten.</span></span>

<span data-ttu-id="b652a-240">리소스를 가져오는 서버에 대한 왕복 작업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-240">There's no roundtrip to the server to obtain the resource.</span></span> <span data-ttu-id="b652a-241">리소스가 있는 경우 200(OK) 상태 코드로 클라이언트에 페치 및 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-241">If the resource exists, it's fetched and returned to the client with a 200 (OK) status code.</span></span> <span data-ttu-id="b652a-242">클라이언트는 리디렉션되지 않기 때문에 브라우저 주소 표시줄의 URL은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-242">Because the client isn't redirected, the URL in the browser address bar doesn't change.</span></span> <span data-ttu-id="b652a-243">클라이언트가 관련되어 있는 한 URL 재작성 작업은 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-243">As far as the client is concerned, the URL rewrite operation never occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="b652a-244">일치 규칙은 비용이 많이 드는 프로세스이며 앱 응답 시간을 단축시키므로 가능하면 항상 `skipRemainingRules: true`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-244">Use `skipRemainingRules: true` whenever possible, because matching rules is an expensive process and reduces app response time.</span></span> <span data-ttu-id="b652a-245">가장 빠른 앱 응답의 경우:</span><span class="sxs-lookup"><span data-stu-id="b652a-245">For the fastest app response:</span></span>
> * <span data-ttu-id="b652a-246">가장 자주 일치하는 규칙에서 가장 적게 일치하는 규칙으로 재작성 규칙을 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-246">Order your rewrite rules from the most frequently matched rule to the least frequently matched rule.</span></span>
> * <span data-ttu-id="b652a-247">일치가 발생하고 추가 규칙 처리가 필요하지 않은 경우 나머지 규칙의 처리를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-247">Skip the processing of the remaining rules when a match occurs and no additional rule processing is required.</span></span>

### <a name="apache-modrewrite"></a><span data-ttu-id="b652a-248">Apache mod_rewrite</span><span class="sxs-lookup"><span data-stu-id="b652a-248">Apache mod_rewrite</span></span>
<span data-ttu-id="b652a-249">`AddApacheModRewrite`를 사용하여 Apache mod_rewrite 규칙을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-249">Apply Apache mod_rewrite rules with `AddApacheModRewrite`.</span></span> <span data-ttu-id="b652a-250">규칙 파일이 앱으로 배포되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-250">Make sure that the rules file is deployed with the app.</span></span> <span data-ttu-id="b652a-251">mod_rewrite 규칙에 대한 자세한 내용 및 예제는 [Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b652a-251">For more information and examples of mod_rewrite rules, see [Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b652a-252">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b652a-252">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="b652a-253">`StreamReader`는 *ApacheModRewrite.txt* 규칙 파일에서 규칙을 읽는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-253">A `StreamReader` is used to read the rules from the *ApacheModRewrite.txt* rules file.</span></span>

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=1,7)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b652a-254">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b652a-254">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b652a-255">첫 번째 매개 변수는 [종속성 주입](dependency-injection.md)을 통해 제공되는 `IFileProvider`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-255">The first parameter takes an `IFileProvider`, which is provided via [Dependency Injection](dependency-injection.md).</span></span> <span data-ttu-id="b652a-256">`IHostingEnvironment`는 `ContentRootFileProvider`를 제공하도록 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-256">The `IHostingEnvironment` is injected to provide the `ContentRootFileProvider`.</span></span> <span data-ttu-id="b652a-257">두 번째 매개 변수는 샘플 앱에서 *ApacheModRewrite.txt*인 규칙 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-257">The second parameter is the path to your rules file, which is *ApacheModRewrite.txt* in the sample app.</span></span>

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=4)]

---

<span data-ttu-id="b652a-258">샘플 앱은 `/apache-mod-rules-redirect/(.\*)`에서 `/redirected?id=$1`로 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-258">The sample app redirects requests from `/apache-mod-rules-redirect/(.\*)` to `/redirected?id=$1`.</span></span> <span data-ttu-id="b652a-259">응답 상태 코드는 302(있음)입니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-259">The response status code is 302 (Found).</span></span>

[!code[Main](url-rewriting/samples/2.x/ApacheModRewrite.txt)]

<span data-ttu-id="b652a-260">원래 요청: `/apache-mod-rules-redirect/1234`</span><span class="sxs-lookup"><span data-stu-id="b652a-260">Original Request: `/apache-mod-rules-redirect/1234`</span></span>

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_apache_mod_redirect.png)

##### <a name="supported-server-variables"></a><span data-ttu-id="b652a-262">지원되는 서버 변수</span><span class="sxs-lookup"><span data-stu-id="b652a-262">Supported server variables</span></span>
<span data-ttu-id="b652a-263">미들웨어는 다음 Apache mod_rewrite 서버 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-263">The middleware supports the following Apache mod_rewrite server variables:</span></span>
* <span data-ttu-id="b652a-264">CONN_REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="b652a-264">CONN_REMOTE_ADDR</span></span>
* <span data-ttu-id="b652a-265">HTTP_ACCEPT</span><span class="sxs-lookup"><span data-stu-id="b652a-265">HTTP_ACCEPT</span></span>
* <span data-ttu-id="b652a-266">HTTP_CONNECTION</span><span class="sxs-lookup"><span data-stu-id="b652a-266">HTTP_CONNECTION</span></span>
* <span data-ttu-id="b652a-267">HTTP_COOKIE</span><span class="sxs-lookup"><span data-stu-id="b652a-267">HTTP_COOKIE</span></span>
* <span data-ttu-id="b652a-268">HTTP_FORWARDED</span><span class="sxs-lookup"><span data-stu-id="b652a-268">HTTP_FORWARDED</span></span>
* <span data-ttu-id="b652a-269">HTTP_HOST</span><span class="sxs-lookup"><span data-stu-id="b652a-269">HTTP_HOST</span></span>
* <span data-ttu-id="b652a-270">HTTP_REFERER</span><span class="sxs-lookup"><span data-stu-id="b652a-270">HTTP_REFERER</span></span>
* <span data-ttu-id="b652a-271">HTTP_USER_AGENT</span><span class="sxs-lookup"><span data-stu-id="b652a-271">HTTP_USER_AGENT</span></span>
* <span data-ttu-id="b652a-272">HTTPS</span><span class="sxs-lookup"><span data-stu-id="b652a-272">HTTPS</span></span>
* <span data-ttu-id="b652a-273">IPV6</span><span class="sxs-lookup"><span data-stu-id="b652a-273">IPV6</span></span>
* <span data-ttu-id="b652a-274">QUERY_STRING</span><span class="sxs-lookup"><span data-stu-id="b652a-274">QUERY_STRING</span></span>
* <span data-ttu-id="b652a-275">REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="b652a-275">REMOTE_ADDR</span></span>
* <span data-ttu-id="b652a-276">REMOTE_PORT</span><span class="sxs-lookup"><span data-stu-id="b652a-276">REMOTE_PORT</span></span>
* <span data-ttu-id="b652a-277">REQUEST_FILENAME</span><span class="sxs-lookup"><span data-stu-id="b652a-277">REQUEST_FILENAME</span></span>
* <span data-ttu-id="b652a-278">REQUEST_METHOD</span><span class="sxs-lookup"><span data-stu-id="b652a-278">REQUEST_METHOD</span></span>
* <span data-ttu-id="b652a-279">REQUEST_SCHEME</span><span class="sxs-lookup"><span data-stu-id="b652a-279">REQUEST_SCHEME</span></span>
* <span data-ttu-id="b652a-280">REQUEST_URI</span><span class="sxs-lookup"><span data-stu-id="b652a-280">REQUEST_URI</span></span>
* <span data-ttu-id="b652a-281">SCRIPT_FILENAME</span><span class="sxs-lookup"><span data-stu-id="b652a-281">SCRIPT_FILENAME</span></span>
* <span data-ttu-id="b652a-282">SERVER_ADDR</span><span class="sxs-lookup"><span data-stu-id="b652a-282">SERVER_ADDR</span></span>
* <span data-ttu-id="b652a-283">SERVER_PORT</span><span class="sxs-lookup"><span data-stu-id="b652a-283">SERVER_PORT</span></span>
* <span data-ttu-id="b652a-284">SERVER_PROTOCOL</span><span class="sxs-lookup"><span data-stu-id="b652a-284">SERVER_PROTOCOL</span></span>
* <span data-ttu-id="b652a-285">TIME</span><span class="sxs-lookup"><span data-stu-id="b652a-285">TIME</span></span>
* <span data-ttu-id="b652a-286">TIME_DAY</span><span class="sxs-lookup"><span data-stu-id="b652a-286">TIME_DAY</span></span>
* <span data-ttu-id="b652a-287">TIME_HOUR</span><span class="sxs-lookup"><span data-stu-id="b652a-287">TIME_HOUR</span></span>
* <span data-ttu-id="b652a-288">TIME_MIN</span><span class="sxs-lookup"><span data-stu-id="b652a-288">TIME_MIN</span></span>
* <span data-ttu-id="b652a-289">TIME_MON</span><span class="sxs-lookup"><span data-stu-id="b652a-289">TIME_MON</span></span>
* <span data-ttu-id="b652a-290">TIME_SEC</span><span class="sxs-lookup"><span data-stu-id="b652a-290">TIME_SEC</span></span>
* <span data-ttu-id="b652a-291">TIME_WDAY</span><span class="sxs-lookup"><span data-stu-id="b652a-291">TIME_WDAY</span></span>
* <span data-ttu-id="b652a-292">TIME_YEAR</span><span class="sxs-lookup"><span data-stu-id="b652a-292">TIME_YEAR</span></span>

### <a name="iis-url-rewrite-module-rules"></a><span data-ttu-id="b652a-293">IIS URL 재작성 모듈 규칙</span><span class="sxs-lookup"><span data-stu-id="b652a-293">IIS URL Rewrite Module rules</span></span>
<span data-ttu-id="b652a-294">IIS URL 재작성 모듈에 적용되는 규칙을 사용하려면 `AddIISUrlRewrite`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-294">To use rules that apply to the IIS URL Rewrite Module, use `AddIISUrlRewrite`.</span></span> <span data-ttu-id="b652a-295">규칙 파일이 앱으로 배포되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-295">Make sure that the rules file is deployed with the app.</span></span> <span data-ttu-id="b652a-296">Windows Server IIS에서 실행할 때 *web.config* 파일을 사용하도록 미들웨어에 지시하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b652a-296">Don't direct the middleware to use your *web.config* file when running on Windows Server IIS.</span></span> <span data-ttu-id="b652a-297">IIS를 사용하는 경우 이러한 규칙은 IIS 재작성 모듈과 충돌을 피하도록 *web.config* 외부에 저장되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-297">With IIS, these rules should be stored outside of your *web.config* to avoid conflicts with the IIS Rewrite module.</span></span> <span data-ttu-id="b652a-298">IIS URL 재작성 모듈 규칙에 대한 자세한 내용 및 예제는 [Url 재작성 모듈 2.0 사용](https://docs.microsoft.com/iis/extensions/url-rewrite-module/using-url-rewrite-module-20) 및 [URL 재작성 모듈 구성 참조](https://docs.microsoft.com/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b652a-298">For more information and examples of IIS URL Rewrite Module rules, see [Using Url Rewrite Module 2.0](https://docs.microsoft.com/iis/extensions/url-rewrite-module/using-url-rewrite-module-20) and [URL Rewrite Module Configuration Reference](https://docs.microsoft.com/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b652a-299">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b652a-299">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="b652a-300">`StreamReader`는 *IISUrlRewrite.xml* 규칙 파일에서 규칙을 읽는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-300">A `StreamReader` is used to read the rules from the *IISUrlRewrite.xml* rules file.</span></span>

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=2,8)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b652a-301">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b652a-301">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b652a-302">첫 번째 매개 변수는 `IFileProvider`를 사용하는 반면 두 번째 매개 변수는 XML 규칙 파일에 대한 경로입니다. 이는 샘플 앱에서 *IISUrlRewrite.xml*입니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-302">The first parameter takes an `IFileProvider`, while the second parameter is the path to your XML rules file, which is *IISUrlRewrite.xml* in the sample app.</span></span>

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=5)]

---

<span data-ttu-id="b652a-303">샘플 앱은 `/iis-rules-rewrite/(.*)`에서 `/rewritten?id=$1`로 요청을 재작성합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-303">The sample app rewrites requests from `/iis-rules-rewrite/(.*)` to `/rewritten?id=$1`.</span></span> <span data-ttu-id="b652a-304">응답은 200(정상) 상태 코드로 클라이언트에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-304">The response is sent to the client with a 200 (OK) status code.</span></span>

[!code-xml[Main](url-rewriting/samples/2.x/IISUrlRewrite.xml)]

<span data-ttu-id="b652a-305">원래 요청: `/iis-rules-rewrite/1234`</span><span class="sxs-lookup"><span data-stu-id="b652a-305">Original Request: `/iis-rules-rewrite/1234`</span></span>

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_iis_url_rewrite.png)

<span data-ttu-id="b652a-307">바람직하지 않은 방법으로 앱에 영향을 미치는 서버 수준 규칙으로 구성된 활성 IIS 재작성 모듈이 있는 경우 앱에 대해 IIS 재작성 모듈을 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-307">If you have an active IIS Rewrite Module with server-level rules configured that would impact your app in undesirable ways, you can disable the IIS Rewrite Module for an app.</span></span> <span data-ttu-id="b652a-308">자세한 내용은 [IIS 모듈 비활성화](xref:host-and-deploy/iis/modules#disabling-iis-modules)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b652a-308">For more information, see [Disabling IIS modules](xref:host-and-deploy/iis/modules#disabling-iis-modules).</span></span>

#### <a name="unsupported-features"></a><span data-ttu-id="b652a-309">지원되지 않는 기능</span><span class="sxs-lookup"><span data-stu-id="b652a-309">Unsupported features</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b652a-310">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b652a-310">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="b652a-311">ASP.NET Core 2.x로 출시된 미들웨어는 다음과 같은 IIS URL 재작성 모듈 기능을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-311">The middleware released with ASP.NET Core 2.x doesn't support the following IIS URL Rewrite Module features:</span></span>
* <span data-ttu-id="b652a-312">아웃바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="b652a-312">Outbound Rules</span></span>
* <span data-ttu-id="b652a-313">사용자 지정 서버 변수</span><span class="sxs-lookup"><span data-stu-id="b652a-313">Custom Server Variables</span></span>
* <span data-ttu-id="b652a-314">와일드카드</span><span class="sxs-lookup"><span data-stu-id="b652a-314">Wildcards</span></span>
* <span data-ttu-id="b652a-315">LogRewrittenUrl</span><span class="sxs-lookup"><span data-stu-id="b652a-315">LogRewrittenUrl</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b652a-316">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b652a-316">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b652a-317">ASP.NET Core 1.x로 출시된 미들웨어는 다음과 같은 IIS URL 재작성 모듈 기능을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-317">The middleware released with ASP.NET Core 1.x doesn't support the following IIS URL Rewrite Module features:</span></span>
* <span data-ttu-id="b652a-318">전역 규칙</span><span class="sxs-lookup"><span data-stu-id="b652a-318">Global Rules</span></span>
* <span data-ttu-id="b652a-319">아웃바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="b652a-319">Outbound Rules</span></span>
* <span data-ttu-id="b652a-320">재작성 맵</span><span class="sxs-lookup"><span data-stu-id="b652a-320">Rewrite Maps</span></span>
* <span data-ttu-id="b652a-321">CustomResponse 작업</span><span class="sxs-lookup"><span data-stu-id="b652a-321">CustomResponse Action</span></span>
* <span data-ttu-id="b652a-322">사용자 지정 서버 변수</span><span class="sxs-lookup"><span data-stu-id="b652a-322">Custom Server Variables</span></span>
* <span data-ttu-id="b652a-323">와일드카드</span><span class="sxs-lookup"><span data-stu-id="b652a-323">Wildcards</span></span>
* <span data-ttu-id="b652a-324">Action:CustomResponse</span><span class="sxs-lookup"><span data-stu-id="b652a-324">Action:CustomResponse</span></span>
* <span data-ttu-id="b652a-325">LogRewrittenUrl</span><span class="sxs-lookup"><span data-stu-id="b652a-325">LogRewrittenUrl</span></span>

---

#### <a name="supported-server-variables"></a><span data-ttu-id="b652a-326">지원되는 서버 변수</span><span class="sxs-lookup"><span data-stu-id="b652a-326">Supported server variables</span></span>
<span data-ttu-id="b652a-327">미들웨어는 다음 IIS URL 재작성 모듈 서버 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-327">The middleware supports the following IIS URL Rewrite Module server variables:</span></span>
* <span data-ttu-id="b652a-328">CONTENT_LENGTH</span><span class="sxs-lookup"><span data-stu-id="b652a-328">CONTENT_LENGTH</span></span>
* <span data-ttu-id="b652a-329">CONTENT_TYPE</span><span class="sxs-lookup"><span data-stu-id="b652a-329">CONTENT_TYPE</span></span>
* <span data-ttu-id="b652a-330">HTTP_ACCEPT</span><span class="sxs-lookup"><span data-stu-id="b652a-330">HTTP_ACCEPT</span></span>
* <span data-ttu-id="b652a-331">HTTP_CONNECTION</span><span class="sxs-lookup"><span data-stu-id="b652a-331">HTTP_CONNECTION</span></span>
* <span data-ttu-id="b652a-332">HTTP_COOKIE</span><span class="sxs-lookup"><span data-stu-id="b652a-332">HTTP_COOKIE</span></span>
* <span data-ttu-id="b652a-333">HTTP_HOST</span><span class="sxs-lookup"><span data-stu-id="b652a-333">HTTP_HOST</span></span>
* <span data-ttu-id="b652a-334">HTTP_REFERER</span><span class="sxs-lookup"><span data-stu-id="b652a-334">HTTP_REFERER</span></span>
* <span data-ttu-id="b652a-335">HTTP_URL</span><span class="sxs-lookup"><span data-stu-id="b652a-335">HTTP_URL</span></span>
* <span data-ttu-id="b652a-336">HTTP_USER_AGENT</span><span class="sxs-lookup"><span data-stu-id="b652a-336">HTTP_USER_AGENT</span></span>
* <span data-ttu-id="b652a-337">HTTPS</span><span class="sxs-lookup"><span data-stu-id="b652a-337">HTTPS</span></span>
* <span data-ttu-id="b652a-338">LOCAL_ADDR</span><span class="sxs-lookup"><span data-stu-id="b652a-338">LOCAL_ADDR</span></span>
* <span data-ttu-id="b652a-339">QUERY_STRING</span><span class="sxs-lookup"><span data-stu-id="b652a-339">QUERY_STRING</span></span>
* <span data-ttu-id="b652a-340">REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="b652a-340">REMOTE_ADDR</span></span>
* <span data-ttu-id="b652a-341">REMOTE_PORT</span><span class="sxs-lookup"><span data-stu-id="b652a-341">REMOTE_PORT</span></span>
* <span data-ttu-id="b652a-342">REQUEST_FILENAME</span><span class="sxs-lookup"><span data-stu-id="b652a-342">REQUEST_FILENAME</span></span>
* <span data-ttu-id="b652a-343">REQUEST_URI</span><span class="sxs-lookup"><span data-stu-id="b652a-343">REQUEST_URI</span></span>

> [!NOTE]
> <span data-ttu-id="b652a-344">`PhysicalFileProvider`를 통해 `IFileProvider`를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-344">You can also obtain an `IFileProvider` via a `PhysicalFileProvider`.</span></span> <span data-ttu-id="b652a-345">이 방법은 재작성 규칙 파일의 위치에 대해 더 큰 유연성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-345">This approach may provide greater flexibility for the location of your rewrite rules files.</span></span> <span data-ttu-id="b652a-346">재작성 규칙 파일이 제공한 경로에서 서버에 배포되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-346">Make sure that your rewrite rules files are deployed to the server at the path you provide.</span></span>
> ```csharp
> PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
> ```

### <a name="method-based-rule"></a><span data-ttu-id="b652a-347">메서드 기반 규칙</span><span class="sxs-lookup"><span data-stu-id="b652a-347">Method-based rule</span></span>
<span data-ttu-id="b652a-348">`Add(Action<RewriteContext> applyRule)`를 사용하여 메서드에서 사용자 고유의 규칙 논리를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-348">Use `Add(Action<RewriteContext> applyRule)` to implement your own rule logic in a method.</span></span> <span data-ttu-id="b652a-349">`RewriteContext`는 메서드에서 사용하기 위해 `HttpContext`를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-349">The `RewriteContext` exposes the `HttpContext` for use in your method.</span></span> <span data-ttu-id="b652a-350">`context.Result`는 추가 파이프라인 처리가 처리되는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-350">The `context.Result` determines how additional pipeline processing is handled.</span></span>

| <span data-ttu-id="b652a-351">context.Result</span><span class="sxs-lookup"><span data-stu-id="b652a-351">context.Result</span></span>                       | <span data-ttu-id="b652a-352">작업</span><span class="sxs-lookup"><span data-stu-id="b652a-352">Action</span></span>                                                          |
| ------------------------------------ | --------------------------------------------------------------- |
| <span data-ttu-id="b652a-353">`RuleResult.ContinueRules`(기본값)</span><span class="sxs-lookup"><span data-stu-id="b652a-353">`RuleResult.ContinueRules` (default)</span></span> | <span data-ttu-id="b652a-354">계속 규칙 적용</span><span class="sxs-lookup"><span data-stu-id="b652a-354">Continue applying rules</span></span>                                         |
| `RuleResult.EndResponse`             | <span data-ttu-id="b652a-355">규칙 적용을 중지하고 응답 보내기</span><span class="sxs-lookup"><span data-stu-id="b652a-355">Stop applying rules and send the response</span></span>                       |
| `RuleResult.SkipRemainingRules`      | <span data-ttu-id="b652a-356">규칙 적용을 중지하고 다음 미들웨어에 컨텍스트 보내기</span><span class="sxs-lookup"><span data-stu-id="b652a-356">Stop applying rules and send the context to the next middleware</span></span> |

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b652a-357">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b652a-357">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=9)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b652a-358">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b652a-358">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=6)]

---

<span data-ttu-id="b652a-359">샘플 앱은 *.xml*로 끝나는 경로에 대한 요청을 리디렉션하는 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-359">The sample app demonstrates a method that redirects requests for paths that end with *.xml*.</span></span> <span data-ttu-id="b652a-360">`/file.xml`에 대한 요청을 만드는 경우 `/xmlfiles/file.xml`로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-360">If you make a request for `/file.xml`, it's redirected to `/xmlfiles/file.xml`.</span></span> <span data-ttu-id="b652a-361">상태 코드는 301(영구적 이동)로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-361">The status code is set to 301 (Moved Permanently).</span></span> <span data-ttu-id="b652a-362">리디렉션의 경우 응답의 상태 코드를 명시적으로 설정해야 합니다. 그렇지 않으면 200(정상) 상태 코드가 반환되고 클라이언트에서 리디렉션이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-362">For a redirect, you must explicitly set the status code of the response; otherwise, a 200 (OK) status code is returned and the redirect won't occur on the client.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b652a-363">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b652a-363">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/RewriteRules.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b652a-364">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b652a-364">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet2)]

---

<span data-ttu-id="b652a-365">원래 요청: `/file.xml`</span><span class="sxs-lookup"><span data-stu-id="b652a-365">Original Request: `/file.xml`</span></span>

![file.xml에 대한 요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_xml_requests.png)

### <a name="irule-based-rule"></a><span data-ttu-id="b652a-367">IRule 기반 규칙</span><span class="sxs-lookup"><span data-stu-id="b652a-367">IRule-based rule</span></span>
<span data-ttu-id="b652a-368">`Add(IRule)`를 사용하여 `IRule`에서 파생되는 클래스에서 사용자 고유의 규칙 논리를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-368">Use `Add(IRule)` to implement your own rule logic in a class that derives from `IRule`.</span></span> <span data-ttu-id="b652a-369">`IRule`을 사용하면 메서드 기반 규칙 방식을 사용하는 것보다 큰 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-369">Using an `IRule` provides greater flexibility over using the method-based rule approach.</span></span> <span data-ttu-id="b652a-370">파생된 클래스는 `ApplyRule` 메서드에 대한 매개 변수를 전달할 수 있는 생성자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-370">Your derived class may include a constructor, where you can pass in parameters for the `ApplyRule` method.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b652a-371">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b652a-371">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=10-11)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b652a-372">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b652a-372">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=7-8)]

---

<span data-ttu-id="b652a-373">여러 조건을 충족하도록 `extension` 및 `newPath`에 대한 샘플 앱의 매개 변수 값이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-373">The values of the parameters in the sample app for the `extension` and the `newPath` are checked to meet several conditions.</span></span> <span data-ttu-id="b652a-374">`extension`은 값을 포함해야 하며 값은 *.png*, *.jpg* 또는 *.gif*여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-374">The `extension` must contain a value, and the value must be *.png*, *.jpg*, or *.gif*.</span></span> <span data-ttu-id="b652a-375">`newPath`가 유효하지 않은 경우 `ArgumentException`이 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-375">If the `newPath` isn't valid, an `ArgumentException` is thrown.</span></span> <span data-ttu-id="b652a-376">*image.png*에 대한 요청을 만드는 경우 `/png-images/image.png`로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-376">If you make a request for *image.png*, it's redirected to `/png-images/image.png`.</span></span> <span data-ttu-id="b652a-377">*image.jpg*에 대한 요청을 만드는 경우 `/jpg-images/image.jpg`로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-377">If you make a request for *image.jpg*, it's redirected to `/jpg-images/image.jpg`.</span></span> <span data-ttu-id="b652a-378">상태 코드가 301(영구적 이동)로 설정되어 있고 `context.Result`가 규칙 처리를 중지하고 응답을 보내도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b652a-378">The status code is set to 301 (Moved Permanently), and the `context.Result` is set to stop processing rules and send the response.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b652a-379">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b652a-379">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/RewriteRules.cs?name=snippet2)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b652a-380">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b652a-380">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/RewriteRule.cs?name=snippet1)]

---

<span data-ttu-id="b652a-381">원래 요청: `/image.png`</span><span class="sxs-lookup"><span data-stu-id="b652a-381">Original Request: `/image.png`</span></span>

![image.png에 대한 요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_png_requests.png)

<span data-ttu-id="b652a-383">원래 요청: `/image.jpg`</span><span class="sxs-lookup"><span data-stu-id="b652a-383">Original Request: `/image.jpg`</span></span>

![image.jpg에 대한 요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_jpg_requests.png)

## <a name="regex-examples"></a><span data-ttu-id="b652a-385">정규식 예제</span><span class="sxs-lookup"><span data-stu-id="b652a-385">Regex examples</span></span>

| <span data-ttu-id="b652a-386">Goal</span><span class="sxs-lookup"><span data-stu-id="b652a-386">Goal</span></span> | <span data-ttu-id="b652a-387">정규식 문자열 및</span><span class="sxs-lookup"><span data-stu-id="b652a-387">Regex String &</span></span><br><span data-ttu-id="b652a-388">일치 예제</span><span class="sxs-lookup"><span data-stu-id="b652a-388">Match Example</span></span> | <span data-ttu-id="b652a-389">대체 문자열 및</span><span class="sxs-lookup"><span data-stu-id="b652a-389">Replacement String &</span></span><br><span data-ttu-id="b652a-390">출력 예제</span><span class="sxs-lookup"><span data-stu-id="b652a-390">Output Example</span></span> |
| ---- | :-----------------------------: | :------------------------------------: |
| <span data-ttu-id="b652a-391">쿼리 문자열로 경로 재작성</span><span class="sxs-lookup"><span data-stu-id="b652a-391">Rewrite path into querystring</span></span> | `^path/(.*)/(.*)`<br>`/path/abc/123` | `path?var1=$1&var2=$2`<br>`/path?var1=abc&var2=123` |
| <span data-ttu-id="b652a-392">후행 슬래시 제거</span><span class="sxs-lookup"><span data-stu-id="b652a-392">Strip trailing slash</span></span> | `(.*)/$`<br>`/path/` | `$1`<br>`/path` |
| <span data-ttu-id="b652a-393">후행 슬래시 적용</span><span class="sxs-lookup"><span data-stu-id="b652a-393">Enforce trailing slash</span></span> | `(.*[^/])$`<br>`/path` | `$1/`<br>`/path/` |
| <span data-ttu-id="b652a-394">특정 요청 재작성 방지</span><span class="sxs-lookup"><span data-stu-id="b652a-394">Avoid rewriting specific requests</span></span> | <span data-ttu-id="b652a-395">`^(.*)(?<!\.axd)$` 또는 `^(?!.*\.axd$)(.*)$`</span><span class="sxs-lookup"><span data-stu-id="b652a-395">`^(.*)(?<!\.axd)$` or `^(?!.*\.axd$)(.*)$`</span></span><br><span data-ttu-id="b652a-396">예: `/resource.htm`</span><span class="sxs-lookup"><span data-stu-id="b652a-396">Yes: `/resource.htm`</span></span><br><span data-ttu-id="b652a-397">아니요: `/resource.axd`</span><span class="sxs-lookup"><span data-stu-id="b652a-397">No: `/resource.axd`</span></span> | `rewritten/$1`<br>`/rewritten/resource.htm`<br>`/resource.axd` |
| <span data-ttu-id="b652a-398">URL 세그먼트 다시 정렬</span><span class="sxs-lookup"><span data-stu-id="b652a-398">Rearrange URL segments</span></span> | `path/(.*)/(.*)/(.*)`<br>`path/1/2/3` | `path/$3/$2/$1`<br>`path/3/2/1` |
| <span data-ttu-id="b652a-399">URL 세그먼트 대체</span><span class="sxs-lookup"><span data-stu-id="b652a-399">Replace a URL segment</span></span> | `^(.*)/segment2/(.*)`<br>`/segment1/segment2/segment3` | `$1/replaced/$2`<br>`/segment1/replaced/segment3` |

## <a name="additional-resources"></a><span data-ttu-id="b652a-400">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b652a-400">Additional resources</span></span>
* [<span data-ttu-id="b652a-401">응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="b652a-401">Application Startup</span></span>](startup.md)
* [<span data-ttu-id="b652a-402">미들웨어</span><span class="sxs-lookup"><span data-stu-id="b652a-402">Middleware</span></span>](xref:fundamentals/middleware/index)
* [<span data-ttu-id="b652a-403">.NET에서의 정규식</span><span class="sxs-lookup"><span data-stu-id="b652a-403">Regular expressions in .NET</span></span>](/dotnet/articles/standard/base-types/regular-expressions)
* [<span data-ttu-id="b652a-404">정규식 언어 - 빠른 참조</span><span class="sxs-lookup"><span data-stu-id="b652a-404">Regular expression language - quick reference</span></span>](/dotnet/articles/standard/base-types/quick-ref)
* [<span data-ttu-id="b652a-405">Apache mod_rewrite</span><span class="sxs-lookup"><span data-stu-id="b652a-405">Apache mod_rewrite</span></span>](https://httpd.apache.org/docs/2.4/rewrite/)
* [<span data-ttu-id="b652a-406">Url 재작성 모듈 2.0 사용(IIS용)</span><span class="sxs-lookup"><span data-stu-id="b652a-406">Using Url Rewrite Module 2.0 (for IIS)</span></span>](https://docs.microsoft.com/iis/extensions/url-rewrite-module/using-url-rewrite-module-20)
* [<span data-ttu-id="b652a-407">URL 재작성 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="b652a-407">URL Rewrite Module Configuration Reference</span></span>](https://docs.microsoft.com/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference)
* [<span data-ttu-id="b652a-408">IIS URL 재작성 모듈 포럼</span><span class="sxs-lookup"><span data-stu-id="b652a-408">IIS URL Rewrite Module Forum</span></span>](https://forums.iis.net/1152.aspx)
* [<span data-ttu-id="b652a-409">간단한 URL 구조 유지</span><span class="sxs-lookup"><span data-stu-id="b652a-409">Keep a simple URL structure</span></span>](https://support.google.com/webmasters/answer/76329?hl=en)
* [<span data-ttu-id="b652a-410">10가지 URL 재작성 팁과 요령</span><span class="sxs-lookup"><span data-stu-id="b652a-410">10 URL Rewriting Tips and Tricks</span></span>](http://ruslany.net/2009/04/10-url-rewriting-tips-and-tricks/)
* [<span data-ttu-id="b652a-411">슬래시 여부</span><span class="sxs-lookup"><span data-stu-id="b652a-411">To slash or not to slash</span></span>](https://webmasters.googleblog.com/2010/04/to-slash-or-not-to-slash.html)
