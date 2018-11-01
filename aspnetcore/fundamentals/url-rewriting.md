---
title: ASP.NET Core에서 URL 재작성 미들웨어
author: guardrex
description: ASP.NET Core 응용 프로그램에서 URL 재작성 미들웨어로 URL 재작성 및 리디렉션 하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 08/17/2017
uid: fundamentals/url-rewriting
ms.openlocfilehash: 5a1891c838436467fb49ff6288587fab08201179
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207188"
---
# <a name="url-rewriting-middleware-in-aspnet-core"></a><span data-ttu-id="686c7-103">ASP.NET Core에서 URL 재작성 미들웨어</span><span class="sxs-lookup"><span data-stu-id="686c7-103">URL Rewriting Middleware in ASP.NET Core</span></span>

<span data-ttu-id="686c7-104">작성자: [Luke Latham](https://github.com/guardrex) 및 [Mikael Mengistu](https://github.com/mikaelm12)</span><span class="sxs-lookup"><span data-stu-id="686c7-104">By [Luke Latham](https://github.com/guardrex) and [Mikael Mengistu](https://github.com/mikaelm12)</span></span>

<span data-ttu-id="686c7-105">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/sample/)([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="686c7-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/sample/) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="686c7-106">URL 재작성은 하나 이상의 미리 정의된 규칙을 기반으로 하는 요청 URL을 수정하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-106">URL rewriting is the act of modifying request URLs based on one or more predefined rules.</span></span> <span data-ttu-id="686c7-107">URL 재작성은 위치 및 주소가 밀접하게 연결되지 않도록 리소스 위치와 해당 주소 간의 추상화를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-107">URL rewriting creates an abstraction between resource locations and their addresses so that the locations and addresses are not tightly linked.</span></span> <span data-ttu-id="686c7-108">URL 재작성이 중요한 몇 가지 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-108">There are several scenarios where URL rewriting is valuable:</span></span>

* <span data-ttu-id="686c7-109">서버 리소스에 대한 안정적인 로케이터를 유지하는 동시에 임시 또는 영구적으로 해당 리소스를 이동하거나 교체하기</span><span class="sxs-lookup"><span data-stu-id="686c7-109">Moving or replacing server resources temporarily or permanently while maintaining stable locators for those resources.</span></span>
* <span data-ttu-id="686c7-110">다른 응용 프로그램 간에 또는 한 응용 프로그램의 여러 영역 간에 요청 처리 분리하기</span><span class="sxs-lookup"><span data-stu-id="686c7-110">Splitting request processing across different apps or across areas of one app.</span></span>
* <span data-ttu-id="686c7-111">들어오는 요청의 URL 세그먼트를 제거, 추가, 또는 재구성하기</span><span class="sxs-lookup"><span data-stu-id="686c7-111">Removing, adding, or reorganizing URL segments on incoming requests.</span></span>
* <span data-ttu-id="686c7-112">검색 엔진 최적화(SEO, Search Engine Optimization)를 위해 공개 URL 최적화하기</span><span class="sxs-lookup"><span data-stu-id="686c7-112">Optimizing public URLs for Search Engine Optimization (SEO).</span></span>
* <span data-ttu-id="686c7-113">링크로 이동했을 때 제공되는 콘텐츠를 사용자가 예측할 수 있도록 친숙한 공개 URL 사용하기</span><span class="sxs-lookup"><span data-stu-id="686c7-113">Permitting the use of friendly public URLs to help people predict the content they will find by following a link.</span></span>
* <span data-ttu-id="686c7-114">안전하지 않은 요청을 보안 엔드포인트로 리디렉션하기</span><span class="sxs-lookup"><span data-stu-id="686c7-114">Redirecting insecure requests to secure endpoints.</span></span>
* <span data-ttu-id="686c7-115">이미지 핫링크 방지하기</span><span class="sxs-lookup"><span data-stu-id="686c7-115">Preventing image hotlinking.</span></span>

<span data-ttu-id="686c7-116">URL을 변경하기 위한 규칙은 Regex, Apache mod_rewrite 모듈 규칙, IIS 재작성 모듈 규칙 및 사용자 지정 규칙 로직 사용 등의 다양한 방법으로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-116">You can define rules for changing the URL in several ways, including Regex, Apache mod_rewrite module rules, IIS Rewrite Module rules, and using custom rule logic.</span></span> <span data-ttu-id="686c7-117">본문에서는 ASP.NET Core 응용 프로그램에서 URL 재작성 미들웨어를 사용하는 방법에 관한 지침과 URL 재작성에 관해서 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-117">This document introduces URL rewriting with instructions on how to use URL Rewriting Middleware in ASP.NET Core apps.</span></span>

> [!NOTE]
> <span data-ttu-id="686c7-118">URL 재작성은 응용 프로그램의 성능을 저하시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-118">URL rewriting can reduce the performance of an app.</span></span> <span data-ttu-id="686c7-119">가능한 한 규칙의 수와 복잡성을 제한해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-119">Where feasible, you should limit the number and complexity of rules.</span></span>

## <a name="url-redirect-and-url-rewrite"></a><span data-ttu-id="686c7-120">URL 리디렉션 및 URL 재작성</span><span class="sxs-lookup"><span data-stu-id="686c7-120">URL redirect and URL rewrite</span></span>

<span data-ttu-id="686c7-121">*URL 리디렉션*과 *URL 재작성* 간의 단어 차이는 언뜻 보기에는 대단한 것 같지 않지만, 클라이언트에게 리소스를 제공할 때 많은 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-121">The difference in wording between *URL redirect* and *URL rewrite* may seem subtle at first but has important implications for providing resources to clients.</span></span> <span data-ttu-id="686c7-122">ASP.NET Core의 URL 재작성 미들웨어는 두 가지 모두에 대한 요구를 만족합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-122">ASP.NET Core's URL Rewriting Middleware is capable of meeting the need for both.</span></span>

<span data-ttu-id="686c7-123">*URL 리디렉션*은 클라이언트 측 작업으로, 클라이언트는 다른 주소를 통해서 리소스에 접근하도록 지시받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-123">A *URL redirect* is a client-side operation, where the client is instructed to access a resource at another address.</span></span> <span data-ttu-id="686c7-124">이 방식은 서버를 한 번 더 왕복해야만 합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-124">This requires a round-trip to the server.</span></span> <span data-ttu-id="686c7-125">클라이언트로 반환된 리디렉션 URL은 클라이언트가 리소스에 대한 새로운 요청을 만들 때 브라우저의 주소 표시줄에 나타나게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-125">The redirect URL returned to the client appears in the browser's address bar when the client makes a new request for the resource.</span></span> 

<span data-ttu-id="686c7-126">`/resource`가 `/different-resource`로 리디렉션 된다고 가정하면, 먼저 클라이언트가 `/resource`를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-126">If `/resource` is *redirected* to `/different-resource`, the client requests `/resource`.</span></span> <span data-ttu-id="686c7-127">그러면 서버는 리디렉션이 임시 또는 영구적임을 나타내는 상태 코드와 함께 해당 리소스를 `/different-resource`에서 가져가야 한다고 클라이언트에게 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-127">The server responds that the client should obtain the resource at `/different-resource` with a status code indicating that the redirect is either temporary or permanent.</span></span> <span data-ttu-id="686c7-128">마지막으로 클라이언트는 리디렉션 URL로 리소스에 대한 새로운 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-128">The client executes a new request for the resource at the redirect URL.</span></span>

![WebAPI 서비스 엔드포인트는 서버 측에서 버전 1(v1)에서 버전 2(v2)로 임시 변경됩니다.](url-rewriting/_static/url_redirect.png)

<span data-ttu-id="686c7-134">요청을 다른 URL로 리디렉션 할 때 서버는 리디렉션이 영구적인지 또는 임시적인지 여부를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-134">When redirecting requests to a different URL, you indicate whether the redirect is permanent or temporary.</span></span> <span data-ttu-id="686c7-135">301 (영구 이동) 상태 코드는 클라이언트에게 리소스에 새로운 영구적인 URL이 존재하며 앞으로 이 리소스에 대한 모든 요청은 새로운 URL을 사용해야 한다고 지시하고자 하는 경우에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-135">The 301 (Moved Permanently) status code is used where the resource has a new, permanent URL and you wish to instruct the client that all future requests for the resource should use the new URL.</span></span> <span data-ttu-id="686c7-136">*이렇게 301 상태 코드가 수신되면 클라이언트는 응답을 캐시할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="686c7-136">*The client may cache the response when a 301 status code is received.*</span></span> <span data-ttu-id="686c7-137">반면 302 (임시 이동) 상태 코드는 리디렉션이 임시적이거나 일반적으로 변경될 수 있는 경우에 사용되므로, 클라이언트는 리디렉션 URL을 저장했다가 나중에 다시 사용하거나 해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-137">The 302 (Found) status code is used where the redirection is temporary or generally subject to change, such that the client shouldn't store and reuse the redirect URL in the future.</span></span> <span data-ttu-id="686c7-138">보다 자세한 정보는 [RFC 2616: 상태 코드 정의](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-138">For more information, see [RFC 2616: Status Code Definitions](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).</span></span>

<span data-ttu-id="686c7-139">*URL 재작성*은 요청받은 리소스를 다른 리소스 주소에서 제공하는 서버 측 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-139">A *URL rewrite* is a server-side operation to provide a resource from a different resource address.</span></span> <span data-ttu-id="686c7-140">URL 재작성 방식은 서버를 한 번 더 왕복할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-140">Rewriting a URL doesn't require a round-trip to the server.</span></span> <span data-ttu-id="686c7-141">재작성된 URL은 클라이언트로 반환되지 않고 브라우저의 주소 표시줄에 나타나지도 않습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-141">The rewritten URL isn't returned to the client and won't appear in the browser's address bar.</span></span> <span data-ttu-id="686c7-142">`/resource`가 `/different-resource`로 *재작성* 된다고 가정할 때, 클라이언트는 `/resource`를 요청하지만 서버는 *내부적으로* `/different-resource`에서 리소스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-142">When `/resource` is *rewritten* to `/different-resource`, the client requests `/resource`, and the server *internally* fetches the resource at `/different-resource`.</span></span> <span data-ttu-id="686c7-143">클라이언트는 재작성된 URL에서 리소스를 조회할 수는 있지만, 해당 요청을 만들고 응답을 받을 때 실제로는 리소스가 재작성된 URL에 존재한다는 정보는 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-143">Although the client might be able to retrieve the resource at the rewritten URL, the client won't be informed that the resource exists at the rewritten URL when it makes its request and receives the response.</span></span>

![WebAPI 서비스 엔드포인트는 서버 측에서 버전 1(v1)에서 버전 2(v2)로 변경됩니다.](url-rewriting/_static/url_rewrite.png)

## <a name="url-rewriting-sample-app"></a><span data-ttu-id="686c7-148">URL 재작성 예제 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="686c7-148">URL rewriting sample app</span></span>

<span data-ttu-id="686c7-149">[URL 재작성 예제 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/sample/)은 URL 재작성 미들웨어의 기능을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-149">You can explore the features of the URL Rewriting Middleware with the [URL rewriting sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/sample/).</span></span> <span data-ttu-id="686c7-150">예제 응용 프로그램은 재작성 및 리디렉션 규칙을 적용하고 재작성 또는 리디렉션된 URL을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-150">The app applies rewrite and redirect rules and shows the rewritten or redirected URL.</span></span>

## <a name="when-to-use-url-rewriting-middleware"></a><span data-ttu-id="686c7-151">URL 재작성 미들웨어를 사용해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="686c7-151">When to use URL Rewriting Middleware</span></span>

<span data-ttu-id="686c7-152">Windows Server에서 IIS의 [URL 재작성 모듈](https://www.iis.net/downloads/microsoft/url-rewrite)을 사용할 수 없거나, Apache Server에서 [Apache mod_rewrite 모듈](https://httpd.apache.org/docs/2.4/rewrite/)을 사용할 수 없거나, [Nginx에서 URL 재작성](https://www.nginx.com/blog/creating-nginx-rewrite-rules/)을 사용할 수 없거나, 또는 응용 프로그램이 [HTTP.sys 서버](xref:fundamentals/servers/httpsys)(기존의 [WebListener](xref:fundamentals/servers/weblistener))에서 호스팅 되는 경우에 URL 재작성 미들웨어를 사용해야 합니다. </span><span class="sxs-lookup"><span data-stu-id="686c7-152">Use URL Rewriting Middleware when you are unable to use the [URL Rewrite module](https://www.iis.net/downloads/microsoft/url-rewrite) with IIS on Windows Server, the [Apache mod_rewrite module](https://httpd.apache.org/docs/2.4/rewrite/) on Apache Server, [URL rewriting on Nginx](https://www.nginx.com/blog/creating-nginx-rewrite-rules/), or your app is hosted on [HTTP.sys server](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)).</span></span> <span data-ttu-id="686c7-153">IIS, Apache 또는 Nginx에서 서버 기반의 URL 재작성 기술을 사용하는 가장 큰 이유는 미들웨어가 이런 모듈들의 모든 기능을 지원하지 않고 대부분 미들웨어의 성능이 모듈의 성능을 따라가지 못하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-153">The main reasons to use the server-based URL rewriting technologies in IIS, Apache, or Nginx are that the middleware doesn't support the full features of these modules and the performance of the middleware probably won't match that of the modules.</span></span> <span data-ttu-id="686c7-154">그러나 IIS 재작성 모듈의 `IsFile` 및 `IsDirectory` 제약 조건 같이 ASP.NET Core 프로젝트에서 동작하지 않는 일부 서버 모듈 기능도 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-154">However, there are some features of the server modules that don't work with ASP.NET Core projects, such as the `IsFile` and `IsDirectory` constraints of the IIS Rewrite module.</span></span> <span data-ttu-id="686c7-155">바로 이런 시나리오에서 대신 미들웨어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-155">In these scenarios, use the middleware instead.</span></span>

## <a name="package"></a><span data-ttu-id="686c7-156">패키지</span><span class="sxs-lookup"><span data-stu-id="686c7-156">Package</span></span>

<span data-ttu-id="686c7-157">프로젝트에 URL 재작성 미들웨어를 추가하려면 [`Microsoft.AspNetCore.Rewrite`](https://www.nuget.org/packages/Microsoft.AspNetCore.Rewrite/) 패키지를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-157">To include the middleware in your project, add a reference to the [`Microsoft.AspNetCore.Rewrite`](https://www.nuget.org/packages/Microsoft.AspNetCore.Rewrite/) package.</span></span> <span data-ttu-id="686c7-158">미들웨어의 기능은 ASP.NET Core 1.1 이상을 대상으로 하는 응용 프로그램에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-158">This feature is available for apps that target ASP.NET Core 1.1 or later.</span></span>

## <a name="extension-and-options"></a><span data-ttu-id="686c7-159">확장 및 옵션</span><span class="sxs-lookup"><span data-stu-id="686c7-159">Extension and options</span></span>

<span data-ttu-id="686c7-160">URL 재작성 및 리디렉션 규칙은 각 규칙에 대한 확장 메서드를 이용해서 [RewriteOptions](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptions) 클래스의 인스턴스를 생성하는 방식으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-160">Establish your URL rewrite and redirect rules by creating an instance of the [RewriteOptions](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptions) class with extension methods for each of your rules.</span></span> <span data-ttu-id="686c7-161">처리하고자 하는 순서대로 여러 규칙을 연결하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-161">Chain multiple rules in the order that you would like them processed.</span></span> <span data-ttu-id="686c7-162">그리고 `RewriteOptions`는 URL 재작성 미들웨어가 `app.UseRewriter(options);`으로 요청 파이프라인에 추가될 때 URL 재작성 미들웨어에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-162">The `RewriteOptions` are passed into the URL Rewriting Middleware as it's added to the request pipeline with `app.UseRewriter(options);`.</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    var options = new RewriteOptions()
        .AddRedirect("redirect-rule/(.*)", "redirected/$1")
        .AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", 
            skipRemainingRules: true)
        .AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt")
        .AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml")
        .Add(RedirectXMLRequests)
        .Add(new RedirectImageRequests(".png", "/png-images"))
        .Add(new RedirectImageRequests(".jpg", "/jpg-images"));

    app.UseRewriter(options);
}
```

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

### <a name="redirect-non-www-to-www"></a><span data-ttu-id="686c7-163">www 이외 요청을 www로 리디렉션</span><span class="sxs-lookup"><span data-stu-id="686c7-163">Redirect non-www to www</span></span>

<span data-ttu-id="686c7-164">이러한 옵션은 앱이 `www` 이외 요청을 `www`로 리디렉션하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-164">Three options permit the app to redirect non-`www` requests to `www`:</span></span>

* <span data-ttu-id="686c7-165">[AddRedirectToWwwPermanent(RewriteOptions)](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptionsextensions.addredirecttowwwpermanent) &ndash; `www` 이외 요청을 `www` 하위 도메인으로 영구적으로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-165">[AddRedirectToWwwPermanent(RewriteOptions)](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptionsextensions.addredirecttowwwpermanent) &ndash; Permanently redirect the request to the `www` subdomain if the request is non-`www`.</span></span> <span data-ttu-id="686c7-166">[Status308PermanentRedirect](/dotnet/api/microsoft.aspnetcore.http.statuscodes.status308permanentredirect) 상태 코드를 사용하여 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-166">Redirects with a [Status308PermanentRedirect](/dotnet/api/microsoft.aspnetcore.http.statuscodes.status308permanentredirect) status code.</span></span>
* <span data-ttu-id="686c7-167">[AddRedirectToWww(RewriteOptions)](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptionsextensions.addredirecttowww) &ndash; 들어오는 요청이 `www` 요청이 아닐 경우 `www` 하위 도메인으로 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-167">[AddRedirectToWww(RewriteOptions)](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptionsextensions.addredirecttowww) &ndash; Redirect the request to the `www` subdomain if the incoming request is non-`www`.</span></span> <span data-ttu-id="686c7-168">[Status307TemporaryRedirect](/dotnet/api/microsoft.aspnetcore.http.statuscodes.status307temporaryredirect) 상태 코드를 사용하여 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-168">Redirects with a [Status307TemporaryRedirect](/dotnet/api/microsoft.aspnetcore.http.statuscodes.status307temporaryredirect) status code.</span></span>
* <span data-ttu-id="686c7-169">[AddRedirectToWww(RewriteOptions, Int32)](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptionsextensions.addredirecttowww) &ndash; 들어오는 요청이 `www` 요청이 아닐 경우 `www` 하위 도메인으로 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-169">[AddRedirectToWww(RewriteOptions, Int32)](/dotnet/api/microsoft.aspnetcore.rewrite.rewriteoptionsextensions.addredirecttowww) &ndash; Redirect the request to the `www` subdomain if the incoming request is non-`www`.</span></span> <span data-ttu-id="686c7-170">응답 상태 코드를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-170">Allows you to provide the status code for the response.</span></span> <span data-ttu-id="686c7-171">`AddRedirectToWww`에 할당하는 경우 [StatusCodes](/dotnet/api/microsoft.aspnetcore.http.statuscodes) 클래스의 필드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="686c7-171">Use the fields of the [StatusCodes](/dotnet/api/microsoft.aspnetcore.http.statuscodes) class for assignments to `AddRedirectToWww`.</span></span>

::: moniker-end

### <a name="url-redirect"></a><span data-ttu-id="686c7-172">URL 리디렉션</span><span class="sxs-lookup"><span data-stu-id="686c7-172">URL redirect</span></span>

<span data-ttu-id="686c7-173">요청을 리디렉션하려면 `AddRedirect`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-173">Use `AddRedirect` to redirect requests.</span></span> <span data-ttu-id="686c7-174">첫 번째 매개 변수에는 들어오는 URL의 경로와 일치하는 부분을 찾기 위한 정규식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-174">The first parameter contains your regex for matching on the path of the incoming URL.</span></span> <span data-ttu-id="686c7-175">두 번째 매개 변수는 대체 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-175">The second parameter is the replacement string.</span></span> <span data-ttu-id="686c7-176">필요한 경우 세 번째 매개 변수로 상태 코드를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-176">The third parameter, if present, specifies the status code.</span></span> <span data-ttu-id="686c7-177">상태 코드를 지정하지 않는 경우 기본값을 리소스가 일시적으로 이동 또는 대체되었음을 나타내는 302(있음)로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-177">If you don't specify the status code, it defaults to 302 (Found), which indicates that the resource is temporarily moved or replaced.</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=9)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRedirect("redirect-rule/(.*)", "redirected/$1");

    app.UseRewriter(options);
}
```

::: moniker-end

<span data-ttu-id="686c7-178">개발자 도구가 활성화된 브라우저에서 `/redirect-rule/1234/5678` 경로로 샘플 앱에 대한 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-178">In a browser with developer tools enabled, make a request to the sample app with the path `/redirect-rule/1234/5678`.</span></span> <span data-ttu-id="686c7-179">그러면 정규식이 `redirect-rule/(.*)`의 요청 경로와 일치하므로 `/redirected/1234/5678`로 경로가 치환됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-179">The regex matches the request path on `redirect-rule/(.*)`, and the path is replaced with `/redirected/1234/5678`.</span></span> <span data-ttu-id="686c7-180">이 리디렉션 URL은 302 (임시 이동) 상태 코드와 함께 클라이언트로 재전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-180">The redirect URL is sent back to the client with a 302 (Found) status code.</span></span> <span data-ttu-id="686c7-181">브라우저는 리디렉션 URL에 대한 새로운 요청을 만들고 이 주소는 브라우저의 주소 표시줄에 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-181">The browser makes a new request at the redirect URL, which appears in the browser's address bar.</span></span> <span data-ttu-id="686c7-182">리디렉션 URL과 일치하는 예제 응용 프로그램의 규칙은 존재하지 않기 때문에 두 번째 요청은 응용 프로그램에서 200 (정상) 응답을 수신하고 응답 본문은 리디렉션 URL을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-182">Since no rules in the sample app match on the redirect URL, the second request receives a 200 (OK) response from the app and the body of the response shows the redirect URL.</span></span> <span data-ttu-id="686c7-183">URL이 *리디렉션* 될 때 서버에 대한 왕복이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-183">A roundtrip is made to the server when a URL is *redirected*.</span></span>

> [!WARNING]
> <span data-ttu-id="686c7-184">리디렉션 규칙을 설정할 때 주의하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-184">Be cautious when establishing your redirect rules.</span></span> <span data-ttu-id="686c7-185">리디렉션 규칙은 리디렉션 된 후를 비롯해서 응용 프로그램에 대한 각각의 요청을 대상으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-185">Your redirect rules are evaluated on each request to the app, including after a redirect.</span></span> <span data-ttu-id="686c7-186">따라서 실수로 무한히 리디렉션 되는 루프를 만들기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-186">It's easy to accidently create a loop of infinite redirects.</span></span>

<span data-ttu-id="686c7-187">원본 요청: `/redirect-rule/1234/5678`</span><span class="sxs-lookup"><span data-stu-id="686c7-187">Original Request: `/redirect-rule/1234/5678`</span></span>

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect.png)

<span data-ttu-id="686c7-189">표현식에서 괄호로 둘러쌓인 부분을 *캡처 그룹(Capture Group)* 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-189">The part of the expression contained within parentheses is called a *capture group*.</span></span> <span data-ttu-id="686c7-190">그리고 표현식에서 마침표(`.`)는 모든 문자와 일치함을 뜻합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-190">The dot (`.`) of the expression means *match any character*.</span></span> <span data-ttu-id="686c7-191">마지막으로 별표(`*`)는 앞의 문자와 0번 이상 일치함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-191">The asterisk (`*`) indicates *match the preceding character zero or more times*.</span></span> <span data-ttu-id="686c7-192">따라서 URL의 마지막 두 세그먼트, `1234/5678`은 캡쳐 그룹 `(.*)`에 의해 캡쳐됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-192">Therefore, the last two path segments of the URL, `1234/5678`, are captured by capture group `(.*)`.</span></span> <span data-ttu-id="686c7-193">즉 요청 URL에서 `redirect-rule/` 이후에 제공하는 모든 값이 이 단일 캡처 그룹에 의해서 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-193">Any value you provide in the request URL after `redirect-rule/` is captured by this single capture group.</span></span>

<span data-ttu-id="686c7-194">대체 문자열에서, 캡처된 그룹은 캡처의 일련번호가 뒤에 붙는 달러 기호(`$`)를 통해서 문자열에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-194">In the replacement string, captured groups are injected into the string with the dollar sign (`$`) followed by the sequence number of the capture.</span></span> <span data-ttu-id="686c7-195">첫 번째 캡처 그룹 값은 `$1`로 얻을 수 있고, 두 번째 캡처 그룹 값은 `$2`로 얻을 수 있으며, 이는 정규식에 포함된 캡처 그룹에 대해 순차적으로 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-195">The first capture group value is obtained with `$1`, the second with `$2`, and they continue in sequence for the capture groups in your regex.</span></span> <span data-ttu-id="686c7-196">예제 응용 프로그램에서 리디렉션 규칙의 정규식에 캡처된 그룹은 단 하나뿐이므로 대체 문자열에 삽입되는 그룹도 `$1` 하나뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-196">There's only one captured group in the redirect rule regex in the sample app, so there's only one injected group in the replacement string, which is `$1`.</span></span> <span data-ttu-id="686c7-197">규칙이 적용되고 나면 URL은 `/redirected/1234/5678`로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-197">When the rule is applied, the URL becomes `/redirected/1234/5678`.</span></span>

### <a name="url-redirect-to-a-secure-endpoint"></a><span data-ttu-id="686c7-198">보안 엔드포인트에 대한 URL 리디렉션</span><span class="sxs-lookup"><span data-stu-id="686c7-198">URL redirect to a secure endpoint</span></span>

<span data-ttu-id="686c7-199">`AddRedirectToHttps`를 사용하면 HTTP 요청을 HTTPS(`https://`)를 사용하는 동일한 호스트 및 경로로 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-199">Use `AddRedirectToHttps` to redirect HTTP requests to the same host and path using HTTPS (`https://`).</span></span> <span data-ttu-id="686c7-200">상태 코드를 지정하지 않으면 미들웨어가 기본값인 302(임시 이동)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-200">If the status code isn't supplied, the middleware defaults to 302 (Found).</span></span> <span data-ttu-id="686c7-201">그리고 포트를 지정하지 않으면 미들웨어가 기본값인 `null`을 설정하는데, 이는 프로토콜이 `https://`로 변경되고 클라이언트가 포트 443을 통해서 리소스에 접근함을 뜻합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-201">If the port isn't supplied, the middleware defaults to `null`, which means the protocol changes to `https://` and the client accesses the resource on port 443.</span></span> <span data-ttu-id="686c7-202">예제에서는 상태 코드를 301(영구 이동)로 설정하고 포트를 5001로 변경하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-202">The example shows how to set the status code to 301 (Moved Permanently) and change the port to 5001.</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRedirectToHttps(301, 5001);

    app.UseRewriter(options);
}
```

<span data-ttu-id="686c7-203">`AddRedirectToHttpsPermanent`를 사용하면 안전하지 않은 요청을 HTTPS 프로토콜을 사용하는 (포트 443에서 `https://`를 사용하는) 동일한 호스트 및 경로로 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-203">Use `AddRedirectToHttpsPermanent` to redirect insecure requests to the same host and path with secure HTTPS protocol (`https://` on port 443).</span></span> <span data-ttu-id="686c7-204">미들웨어는 상태 코드를 301(영구 이동)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-204">The middleware sets the status code to 301 (Moved Permanently).</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRedirectToHttpsPermanent();

    app.UseRewriter(options);
}
```

> [!NOTE]
> <span data-ttu-id="686c7-205">추가 리디렉션 규칙에 대한 요구 사항 없이 HTTPS로 리디렉션하는 경우에 HTTPS 리디렉션 미들웨어를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-205">When redirecting to HTTPS without the requirement for additional redirect rules, we recommend using HTTPS Redirection Middleware.</span></span> <span data-ttu-id="686c7-206">자세한 내용은 [HTTPS 적용](xref:security/enforcing-ssl#require-https) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="686c7-206">For more information, see the [Enforce HTTPS](xref:security/enforcing-ssl#require-https) topic.</span></span>

<span data-ttu-id="686c7-207">예제 응용 프로그램을 통해서 `AddRedirectToHttps` 또는 `AddRedirectToHttpsPermanent`의 사용 방법을 확인해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-207">The sample app is capable of demonstrating how to use `AddRedirectToHttps` or `AddRedirectToHttpsPermanent`.</span></span> <span data-ttu-id="686c7-208">먼저 `RewriteOptions`에 이 확장 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-208">Add the extension method to the `RewriteOptions`.</span></span> <span data-ttu-id="686c7-209">모든 URL에서 앱에 대한 안전하지 않은 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-209">Make an insecure request to the app at any URL.</span></span> <span data-ttu-id="686c7-210">자체 서명된 인증서를 신뢰할 수 없다는 브라우저 보안 경고는 무시하면 됩니다. 또는 인증서를 신뢰할 예외를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-210">Dismiss the browser security warning that the self-signed certificate is untrusted or create an exception to trust the certificate.</span></span>

<span data-ttu-id="686c7-211">`AddRedirectToHttps(301, 5001)`에 대한 원본 요청: `http://localhost:5000/secure`</span><span class="sxs-lookup"><span data-stu-id="686c7-211">Original Request using `AddRedirectToHttps(301, 5001)`: `http://localhost:5000/secure`</span></span>

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_to_https.png)

<span data-ttu-id="686c7-213">`AddRedirectToHttpsPermanent`에 대한 원본 요청: `http://localhost:5000/secure`</span><span class="sxs-lookup"><span data-stu-id="686c7-213">Original Request using `AddRedirectToHttpsPermanent`: `http://localhost:5000/secure`</span></span>

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_to_https_permanent.png)

### <a name="url-rewrite"></a><span data-ttu-id="686c7-215">URL 재작성</span><span class="sxs-lookup"><span data-stu-id="686c7-215">URL rewrite</span></span>

<span data-ttu-id="686c7-216">URL을 재작성하는 규칙을 만들려면 `AddRewrite`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-216">Use `AddRewrite` to create a rule for rewriting URLs.</span></span> <span data-ttu-id="686c7-217">첫 번째 매개 변수에는 들어오는 URL의 경로와 일치하는 부분을 찾기 위한 정규식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-217">The first parameter contains your regex for matching on the incoming URL path.</span></span> <span data-ttu-id="686c7-218">두 번째 매개 변수는 대체 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-218">The second parameter is the replacement string.</span></span> <span data-ttu-id="686c7-219">세 번째 매개 변수, `skipRemainingRules: {true|false}`는 현재 규칙이 적용되는 경우에 추가 재작성 규칙을 건너뛸 것인지 여부를 미들웨어에 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-219">The third parameter, `skipRemainingRules: {true|false}`, indicates to the middleware whether or not to skip additional rewrite rules if the current rule is applied.</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=10-11)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", 
            skipRemainingRules: true);

    app.UseRewriter(options);
}
```

::: moniker-end

<span data-ttu-id="686c7-220">원래 요청: `/rewrite-rule/1234/5678`</span><span class="sxs-lookup"><span data-stu-id="686c7-220">Original Request: `/rewrite-rule/1234/5678`</span></span>

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_rewrite.png)

<span data-ttu-id="686c7-222">이 정규식에서 가장 먼저 주목해야 할 부분은 식의 가장 첫 문자인 캐럿(`^`)입니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-222">The first thing you notice in the regex is the carat (`^`) at the beginning of the expression.</span></span> <span data-ttu-id="686c7-223">이는 URL 경로의 시작 부분에서부터 일치가 시작된다는 것을 의미합니다. </span><span class="sxs-lookup"><span data-stu-id="686c7-223">This means that matching starts at the beginning of the URL path.</span></span>

<span data-ttu-id="686c7-224">`redirect-rule/(.*)`리디렉션 규칙에 대한 이전 예제에서는 정규식 시작 부분에 캐럿이 없기 때문에, 경로의 `redirect-rule/` 앞부분에 어떤 문자가 나타나더라도 정상적으로 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-224">In the earlier example with the redirect rule, `redirect-rule/(.*)`, there's no carat at the start of the regex; therefore, any characters may precede `redirect-rule/` in the path for a successful match.</span></span>

| <span data-ttu-id="686c7-225">Path</span><span class="sxs-lookup"><span data-stu-id="686c7-225">Path</span></span>                               | <span data-ttu-id="686c7-226">일치</span><span class="sxs-lookup"><span data-stu-id="686c7-226">Match</span></span> |
| ---------------------------------- | :---: |
| `/redirect-rule/1234/5678`         | <span data-ttu-id="686c7-227">예</span><span class="sxs-lookup"><span data-stu-id="686c7-227">Yes</span></span>   |
| `/my-cool-redirect-rule/1234/5678` | <span data-ttu-id="686c7-228">예</span><span class="sxs-lookup"><span data-stu-id="686c7-228">Yes</span></span>   |
| `/anotherredirect-rule/1234/5678`  | <span data-ttu-id="686c7-229">예</span><span class="sxs-lookup"><span data-stu-id="686c7-229">Yes</span></span>   |

<span data-ttu-id="686c7-230">반면 `^rewrite-rule/(\d+)/(\d+)` 재작성 규칙의 경우에는 오로지 `rewrite-rule/`로 시작하는 경로만 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-230">The rewrite rule, `^rewrite-rule/(\d+)/(\d+)`, only matches paths if they start with `rewrite-rule/`.</span></span> <span data-ttu-id="686c7-231">위의 리디렉션 규칙과 다음 재작성 규칙 간의 일치 여부의 차이를 비교해보시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-231">Notice the difference in matching between the rewrite rule below and the redirect rule above.</span></span>

| <span data-ttu-id="686c7-232">Path</span><span class="sxs-lookup"><span data-stu-id="686c7-232">Path</span></span>                              | <span data-ttu-id="686c7-233">일치</span><span class="sxs-lookup"><span data-stu-id="686c7-233">Match</span></span> |
| --------------------------------- | :---: |
| `/rewrite-rule/1234/5678`         | <span data-ttu-id="686c7-234">예</span><span class="sxs-lookup"><span data-stu-id="686c7-234">Yes</span></span>   |
| `/my-cool-rewrite-rule/1234/5678` | <span data-ttu-id="686c7-235">아니요</span><span class="sxs-lookup"><span data-stu-id="686c7-235">No</span></span>    |
| `/anotherrewrite-rule/1234/5678`  | <span data-ttu-id="686c7-236">아니요</span><span class="sxs-lookup"><span data-stu-id="686c7-236">No</span></span>    |

<span data-ttu-id="686c7-237">표현식의 `^rewrite-rule/` 부분 뒤에는 계속해서 두 개의 캡처 그룹, `(\d+)/(\d+)`이 위치해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-237">Following the `^rewrite-rule/` portion of the expression, there are two capture groups, `(\d+)/(\d+)`.</span></span> <span data-ttu-id="686c7-238">여기서 `\d`는 *숫자 하나와 일치*함을 뜻합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-238">The `\d` signifies *match a digit (number)*.</span></span> <span data-ttu-id="686c7-239">그리고 더하기 기호(`+`)는 *앞의 문자와 한 번 이상 일치*함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-239">The plus sign (`+`) means *match one or more of the preceding character*.</span></span> <span data-ttu-id="686c7-240">따라서 URL은 반드시 숫자 뒤에 슬래시와 다른 숫자가 연이어 나타나는 부분을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-240">Therefore, the URL must contain a number followed by a forward-slash followed by another number.</span></span> <span data-ttu-id="686c7-241">이 캡쳐 그룹들은 `$1` 및 `$2`를 통해서 재작성 URL에 삽입됩니다. </span><span class="sxs-lookup"><span data-stu-id="686c7-241">These capture groups are injected into the rewritten URL as `$1` and `$2`.</span></span> <span data-ttu-id="686c7-242">이 재작성 규칙의 대체 문자열은 캡처된 그룹을 쿼리 문자열에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-242">The rewrite rule replacement string places the captured groups into the querystring.</span></span> <span data-ttu-id="686c7-243">즉, 요청 경로 `/rewrite-rule/1234/5678`은 `/rewritten?var1=1234&var2=5678`에서 리소스를 가져오도록 재작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-243">The requested path of `/rewrite-rule/1234/5678` is rewritten to obtain the resource at `/rewritten?var1=1234&var2=5678`.</span></span> <span data-ttu-id="686c7-244">원본 요청에 쿼리 문자열이 존재할 경우 URL이 재작성될 때 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-244">If a querystring is present on the original request, it's preserved when the URL is rewritten.</span></span>

<span data-ttu-id="686c7-245">이때 리소스를 가져오기 위해서 서버를 왕복하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-245">There's no roundtrip to the server to obtain the resource.</span></span> <span data-ttu-id="686c7-246">리소스가 존재할 경우 가져온 다음 200 (정상) 상태 코드와 함께 클라이언트에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-246">If the resource exists, it's fetched and returned to the client with a 200 (OK) status code.</span></span> <span data-ttu-id="686c7-247">클라이언트는 리디렉션 되지 않기 때문에 브라우저 주소 표시줄의 URL은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-247">Because the client isn't redirected, the URL in the browser address bar doesn't change.</span></span> <span data-ttu-id="686c7-248">클라이언트와 관련된 URL 재작성 작업은 전혀 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-248">As far as the client is concerned, the URL rewrite operation never occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="686c7-249">일치 규칙은 비용이 많이 드는 작업이며 응용 프로그램의 응답 속도를 늦추므로 가능하면 항상 `skipRemainingRules: true`를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-249">Use `skipRemainingRules: true` whenever possible, because matching rules is an expensive process and reduces app response time.</span></span> <span data-ttu-id="686c7-250">최대한 빠른 응용 프로그램 응답을 위해서는:</span><span class="sxs-lookup"><span data-stu-id="686c7-250">For the fastest app response:</span></span>
> * <span data-ttu-id="686c7-251">가장 자주 일치하는 규칙부터 가장 적게 일치하는 규칙 순으로 재작성 규칙을 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-251">Order your rewrite rules from the most frequently matched rule to the least frequently matched rule.</span></span>
> * <span data-ttu-id="686c7-252">일치가 발생하고 추가적인 규칙 처리가 필요하지 않다면 나머지 규칙의 처리를 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-252">Skip the processing of the remaining rules when a match occurs and no additional rule processing is required.</span></span>

### <a name="apache-modrewrite"></a><span data-ttu-id="686c7-253">Apache mod_rewrite</span><span class="sxs-lookup"><span data-stu-id="686c7-253">Apache mod_rewrite</span></span>

<span data-ttu-id="686c7-254">`AddApacheModRewrite`를 사용하면 Apache mod_rewrite 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-254">Apply Apache mod_rewrite rules with `AddApacheModRewrite`.</span></span> <span data-ttu-id="686c7-255">규칙 파일이 응용 프로그램과 함께 배포되고 있는지 확인하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-255">Make sure that the rules file is deployed with the app.</span></span> <span data-ttu-id="686c7-256">mod_rewrite 규칙에 대한 자세한 내용 및 예제는 [Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="686c7-256">For more information and examples of mod_rewrite rules, see [Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/).</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="686c7-257">`StreamReader`는 *ApacheModRewrite.txt* 규칙 파일에서 규칙을 읽는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-257">A `StreamReader` is used to read the rules from the *ApacheModRewrite.txt* rules file.</span></span>

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=3-4,12)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="686c7-258">첫 번째 매개 변수는 [종속성 주입](dependency-injection.md)을 통해 제공되는 `IFileProvider`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-258">The first parameter takes an `IFileProvider`, which is provided via [Dependency Injection](dependency-injection.md).</span></span> <span data-ttu-id="686c7-259">`IHostingEnvironment`는 `ContentRootFileProvider`를 제공하기 위해서 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-259">The `IHostingEnvironment` is injected to provide the `ContentRootFileProvider`.</span></span> <span data-ttu-id="686c7-260">두 번째 매개 변수는 규칙 파일, 즉 예제 응용 프로그램의 경우 *ApacheModRewrite.txt*에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-260">The second parameter is the path to your rules file, which is *ApacheModRewrite.txt* in the sample app.</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    var options = new RewriteOptions()
        .AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt");

    app.UseRewriter(options);
}
```

::: moniker-end

<span data-ttu-id="686c7-261">예제 응용 프로그램은 `/apache-mod-rules-redirect/(.\*)`에서 `/redirected?id=$1`로 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-261">The sample app redirects requests from `/apache-mod-rules-redirect/(.\*)` to `/redirected?id=$1`.</span></span> <span data-ttu-id="686c7-262">그리고 응답 상태 코드는 302 (임시 이동)입니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-262">The response status code is 302 (Found).</span></span>

[!code[](url-rewriting/sample/ApacheModRewrite.txt)]

<span data-ttu-id="686c7-263">원본 요청: `/apache-mod-rules-redirect/1234`</span><span class="sxs-lookup"><span data-stu-id="686c7-263">Original Request: `/apache-mod-rules-redirect/1234`</span></span>

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_apache_mod_redirect.png)

<span data-ttu-id="686c7-265">미들웨어는 다음과 같은 Apache mod_rewrite 서버 변수를 지원합니다:</span><span class="sxs-lookup"><span data-stu-id="686c7-265">The middleware supports the following Apache mod_rewrite server variables:</span></span>

* <span data-ttu-id="686c7-266">CONN_REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="686c7-266">CONN_REMOTE_ADDR</span></span>
* <span data-ttu-id="686c7-267">HTTP_ACCEPT</span><span class="sxs-lookup"><span data-stu-id="686c7-267">HTTP_ACCEPT</span></span>
* <span data-ttu-id="686c7-268">HTTP_CONNECTION</span><span class="sxs-lookup"><span data-stu-id="686c7-268">HTTP_CONNECTION</span></span>
* <span data-ttu-id="686c7-269">HTTP_COOKIE</span><span class="sxs-lookup"><span data-stu-id="686c7-269">HTTP_COOKIE</span></span>
* <span data-ttu-id="686c7-270">HTTP_FORWARDED</span><span class="sxs-lookup"><span data-stu-id="686c7-270">HTTP_FORWARDED</span></span>
* <span data-ttu-id="686c7-271">HTTP_HOST</span><span class="sxs-lookup"><span data-stu-id="686c7-271">HTTP_HOST</span></span>
* <span data-ttu-id="686c7-272">HTTP_REFERER</span><span class="sxs-lookup"><span data-stu-id="686c7-272">HTTP_REFERER</span></span>
* <span data-ttu-id="686c7-273">HTTP_USER_AGENT</span><span class="sxs-lookup"><span data-stu-id="686c7-273">HTTP_USER_AGENT</span></span>
* <span data-ttu-id="686c7-274">HTTPS</span><span class="sxs-lookup"><span data-stu-id="686c7-274">HTTPS</span></span>
* <span data-ttu-id="686c7-275">IPV6</span><span class="sxs-lookup"><span data-stu-id="686c7-275">IPV6</span></span>
* <span data-ttu-id="686c7-276">QUERY_STRING</span><span class="sxs-lookup"><span data-stu-id="686c7-276">QUERY_STRING</span></span>
* <span data-ttu-id="686c7-277">REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="686c7-277">REMOTE_ADDR</span></span>
* <span data-ttu-id="686c7-278">REMOTE_PORT</span><span class="sxs-lookup"><span data-stu-id="686c7-278">REMOTE_PORT</span></span>
* <span data-ttu-id="686c7-279">REQUEST_FILENAME</span><span class="sxs-lookup"><span data-stu-id="686c7-279">REQUEST_FILENAME</span></span>
* <span data-ttu-id="686c7-280">REQUEST_METHOD</span><span class="sxs-lookup"><span data-stu-id="686c7-280">REQUEST_METHOD</span></span>
* <span data-ttu-id="686c7-281">REQUEST_SCHEME</span><span class="sxs-lookup"><span data-stu-id="686c7-281">REQUEST_SCHEME</span></span>
* <span data-ttu-id="686c7-282">REQUEST_URI</span><span class="sxs-lookup"><span data-stu-id="686c7-282">REQUEST_URI</span></span>
* <span data-ttu-id="686c7-283">SCRIPT_FILENAME</span><span class="sxs-lookup"><span data-stu-id="686c7-283">SCRIPT_FILENAME</span></span>
* <span data-ttu-id="686c7-284">SERVER_ADDR</span><span class="sxs-lookup"><span data-stu-id="686c7-284">SERVER_ADDR</span></span>
* <span data-ttu-id="686c7-285">SERVER_PORT</span><span class="sxs-lookup"><span data-stu-id="686c7-285">SERVER_PORT</span></span>
* <span data-ttu-id="686c7-286">SERVER_PROTOCOL</span><span class="sxs-lookup"><span data-stu-id="686c7-286">SERVER_PROTOCOL</span></span>
* <span data-ttu-id="686c7-287">TIME</span><span class="sxs-lookup"><span data-stu-id="686c7-287">TIME</span></span>
* <span data-ttu-id="686c7-288">TIME_DAY</span><span class="sxs-lookup"><span data-stu-id="686c7-288">TIME_DAY</span></span>
* <span data-ttu-id="686c7-289">TIME_HOUR</span><span class="sxs-lookup"><span data-stu-id="686c7-289">TIME_HOUR</span></span>
* <span data-ttu-id="686c7-290">TIME_MIN</span><span class="sxs-lookup"><span data-stu-id="686c7-290">TIME_MIN</span></span>
* <span data-ttu-id="686c7-291">TIME_MON</span><span class="sxs-lookup"><span data-stu-id="686c7-291">TIME_MON</span></span>
* <span data-ttu-id="686c7-292">TIME_SEC</span><span class="sxs-lookup"><span data-stu-id="686c7-292">TIME_SEC</span></span>
* <span data-ttu-id="686c7-293">TIME_WDAY</span><span class="sxs-lookup"><span data-stu-id="686c7-293">TIME_WDAY</span></span>
* <span data-ttu-id="686c7-294">TIME_YEAR</span><span class="sxs-lookup"><span data-stu-id="686c7-294">TIME_YEAR</span></span>

### <a name="iis-url-rewrite-module-rules"></a><span data-ttu-id="686c7-295">IIS URL 재작성 모듈 규칙</span><span class="sxs-lookup"><span data-stu-id="686c7-295">IIS URL Rewrite Module rules</span></span>

<span data-ttu-id="686c7-296">`AddIISUrlRewrite`를 사용하면 IIS URL 재작성 모듈에 적용되는 규칙을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-296">To use rules that apply to the IIS URL Rewrite Module, use `AddIISUrlRewrite`.</span></span> <span data-ttu-id="686c7-297">규칙 파일이 응용 프로그램과 함께 배포되고 있는지 확인하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-297">Make sure that the rules file is deployed with the app.</span></span> <span data-ttu-id="686c7-298">응용 프로그램을 Windows Server의 IIS에서 실행하고 있다면 미들웨어가 *web.config* 파일을 사용하도록 지정하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="686c7-298">Don't direct the middleware to use your *web.config* file when running on Windows Server IIS.</span></span> <span data-ttu-id="686c7-299">IIS를 사용할 경우, IIS 재작성 모듈과 충돌을 피할 수 있도록 규칙을 *web.config* 외부에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-299">With IIS, these rules should be stored outside of your *web.config* to avoid conflicts with the IIS Rewrite module.</span></span> <span data-ttu-id="686c7-300">IIS URL 재작성 모듈 규칙에 대한 자세한 내용 및 예제는 [Url 재작성 모듈 2.0 사용](/iis/extensions/url-rewrite-module/using-url-rewrite-module-20) 및 [URL 재작성 모듈 구성 참조](/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="686c7-300">For more information and examples of IIS URL Rewrite Module rules, see [Using Url Rewrite Module 2.0](/iis/extensions/url-rewrite-module/using-url-rewrite-module-20) and [URL Rewrite Module Configuration Reference](/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference).</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="686c7-301">`StreamReader`는 *IISUrlRewrite.xml* 규칙 파일에서 규칙을 읽는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-301">A `StreamReader` is used to read the rules from the *IISUrlRewrite.xml* rules file.</span></span>

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=5-6,13)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="686c7-302">첫 번째 매개 변수는 `IFileProvider`를 사용하는 반면 두 번째 매개 변수는 XML 규칙 파일에 대한 경로입니다. 이는 샘플 앱에서 *IISUrlRewrite.xml*입니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-302">The first parameter takes an `IFileProvider`, while the second parameter is the path to your XML rules file, which is *IISUrlRewrite.xml* in the sample app.</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    var options = new RewriteOptions()
        .AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml");

    app.UseRewriter(options);
}
```

::: moniker-end

<span data-ttu-id="686c7-303">예제 응용 프로그램은 `/iis-rules-rewrite/(.*)`에서 `/rewritten?id=$1`로 요청을 재작성합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-303">The sample app rewrites requests from `/iis-rules-rewrite/(.*)` to `/rewritten?id=$1`.</span></span> <span data-ttu-id="686c7-304">그리고 응답은 200 (정상) 상태 코드로 클라이언트에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-304">The response is sent to the client with a 200 (OK) status code.</span></span>

[!code-xml[](url-rewriting/sample/IISUrlRewrite.xml)]

<span data-ttu-id="686c7-305">원본 요청: `/iis-rules-rewrite/1234`</span><span class="sxs-lookup"><span data-stu-id="686c7-305">Original Request: `/iis-rules-rewrite/1234`</span></span>

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_iis_url_rewrite.png)

<span data-ttu-id="686c7-307">원하지 않는 방식으로 응용 프로그램에 영향을 주는 서버 수준 규칙이 구성된 활성 IIS 재작성 모듈이 존재할 경우 응용 프로그램에 대한 IIS 재작성 모듈을 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-307">If you have an active IIS Rewrite Module with server-level rules configured that would impact your app in undesirable ways, you can disable the IIS Rewrite Module for an app.</span></span> <span data-ttu-id="686c7-308">보다 자세한 내용은 [IIS 모듈 비활성화](xref:host-and-deploy/iis/modules#disabling-iis-modules)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-308">For more information, see [Disabling IIS modules](xref:host-and-deploy/iis/modules#disabling-iis-modules).</span></span>

#### <a name="unsupported-features"></a><span data-ttu-id="686c7-309">지원되지 않는 기능</span><span class="sxs-lookup"><span data-stu-id="686c7-309">Unsupported features</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="686c7-310">ASP.NET Core 2.x로 출시된 미들웨어는 다음과 같은 IIS URL 재작성 모듈 기능을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-310">The middleware released with ASP.NET Core 2.x doesn't support the following IIS URL Rewrite Module features:</span></span>

* <span data-ttu-id="686c7-311">아웃바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="686c7-311">Outbound Rules</span></span>
* <span data-ttu-id="686c7-312">사용자 지정 서버 변수</span><span class="sxs-lookup"><span data-stu-id="686c7-312">Custom Server Variables</span></span>
* <span data-ttu-id="686c7-313">와일드카드</span><span class="sxs-lookup"><span data-stu-id="686c7-313">Wildcards</span></span>
* <span data-ttu-id="686c7-314">LogRewrittenUrl</span><span class="sxs-lookup"><span data-stu-id="686c7-314">LogRewrittenUrl</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="686c7-315">ASP.NET Core 1.x로 출시된 미들웨어는 다음과 같은 IIS URL 재작성 모듈 기능을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-315">The middleware released with ASP.NET Core 1.x doesn't support the following IIS URL Rewrite Module features:</span></span>

* <span data-ttu-id="686c7-316">전역 규칙</span><span class="sxs-lookup"><span data-stu-id="686c7-316">Global Rules</span></span>
* <span data-ttu-id="686c7-317">아웃바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="686c7-317">Outbound Rules</span></span>
* <span data-ttu-id="686c7-318">재작성 맵</span><span class="sxs-lookup"><span data-stu-id="686c7-318">Rewrite Maps</span></span>
* <span data-ttu-id="686c7-319">CustomResponse 작업</span><span class="sxs-lookup"><span data-stu-id="686c7-319">CustomResponse Action</span></span>
* <span data-ttu-id="686c7-320">사용자 지정 서버 변수</span><span class="sxs-lookup"><span data-stu-id="686c7-320">Custom Server Variables</span></span>
* <span data-ttu-id="686c7-321">와일드카드</span><span class="sxs-lookup"><span data-stu-id="686c7-321">Wildcards</span></span>
* <span data-ttu-id="686c7-322">Action:CustomResponse</span><span class="sxs-lookup"><span data-stu-id="686c7-322">Action:CustomResponse</span></span>
* <span data-ttu-id="686c7-323">LogRewrittenUrl</span><span class="sxs-lookup"><span data-stu-id="686c7-323">LogRewrittenUrl</span></span>

::: moniker-end

#### <a name="supported-server-variables"></a><span data-ttu-id="686c7-324">지원되는 서버 변수</span><span class="sxs-lookup"><span data-stu-id="686c7-324">Supported server variables</span></span>

<span data-ttu-id="686c7-325">미들웨어는 다음과 같은 IIS URL 재작성 모듈 서버 변수를 지원합니다:</span><span class="sxs-lookup"><span data-stu-id="686c7-325">The middleware supports the following IIS URL Rewrite Module server variables:</span></span>

* <span data-ttu-id="686c7-326">CONTENT_LENGTH</span><span class="sxs-lookup"><span data-stu-id="686c7-326">CONTENT_LENGTH</span></span>
* <span data-ttu-id="686c7-327">CONTENT_TYPE</span><span class="sxs-lookup"><span data-stu-id="686c7-327">CONTENT_TYPE</span></span>
* <span data-ttu-id="686c7-328">HTTP_ACCEPT</span><span class="sxs-lookup"><span data-stu-id="686c7-328">HTTP_ACCEPT</span></span>
* <span data-ttu-id="686c7-329">HTTP_CONNECTION</span><span class="sxs-lookup"><span data-stu-id="686c7-329">HTTP_CONNECTION</span></span>
* <span data-ttu-id="686c7-330">HTTP_COOKIE</span><span class="sxs-lookup"><span data-stu-id="686c7-330">HTTP_COOKIE</span></span>
* <span data-ttu-id="686c7-331">HTTP_HOST</span><span class="sxs-lookup"><span data-stu-id="686c7-331">HTTP_HOST</span></span>
* <span data-ttu-id="686c7-332">HTTP_REFERER</span><span class="sxs-lookup"><span data-stu-id="686c7-332">HTTP_REFERER</span></span>
* <span data-ttu-id="686c7-333">HTTP_URL</span><span class="sxs-lookup"><span data-stu-id="686c7-333">HTTP_URL</span></span>
* <span data-ttu-id="686c7-334">HTTP_USER_AGENT</span><span class="sxs-lookup"><span data-stu-id="686c7-334">HTTP_USER_AGENT</span></span>
* <span data-ttu-id="686c7-335">HTTPS</span><span class="sxs-lookup"><span data-stu-id="686c7-335">HTTPS</span></span>
* <span data-ttu-id="686c7-336">LOCAL_ADDR</span><span class="sxs-lookup"><span data-stu-id="686c7-336">LOCAL_ADDR</span></span>
* <span data-ttu-id="686c7-337">QUERY_STRING</span><span class="sxs-lookup"><span data-stu-id="686c7-337">QUERY_STRING</span></span>
* <span data-ttu-id="686c7-338">REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="686c7-338">REMOTE_ADDR</span></span>
* <span data-ttu-id="686c7-339">REMOTE_PORT</span><span class="sxs-lookup"><span data-stu-id="686c7-339">REMOTE_PORT</span></span>
* <span data-ttu-id="686c7-340">REQUEST_FILENAME</span><span class="sxs-lookup"><span data-stu-id="686c7-340">REQUEST_FILENAME</span></span>
* <span data-ttu-id="686c7-341">REQUEST_URI</span><span class="sxs-lookup"><span data-stu-id="686c7-341">REQUEST_URI</span></span>

> [!NOTE]
> <span data-ttu-id="686c7-342">`PhysicalFileProvider`를 이용해서 `IFileProvider`를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-342">You can also obtain an `IFileProvider` via a `PhysicalFileProvider`.</span></span> <span data-ttu-id="686c7-343">이 방식이 재작성 규칙 파일의 위치에 대해 더 많은 유연성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-343">This approach may provide greater flexibility for the location of your rewrite rules files.</span></span> <span data-ttu-id="686c7-344">재작성 규칙 파일이 서버의 지정한 경로에 배포되는지 확인하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-344">Make sure that your rewrite rules files are deployed to the server at the path you provide.</span></span>
> ```csharp
> PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
> ```

### <a name="method-based-rule"></a><span data-ttu-id="686c7-345">메서드 기반 규칙</span><span class="sxs-lookup"><span data-stu-id="686c7-345">Method-based rule</span></span>

<span data-ttu-id="686c7-346">메서드를 이용해서 직접 규칙 로직을 구현하고 싶다면 `Add(Action<RewriteContext> applyRule)`를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-346">Use `Add(Action<RewriteContext> applyRule)` to implement your own rule logic in a method.</span></span> <span data-ttu-id="686c7-347">`RewriteContext`는 메서드에서 사용할 수 있는 `HttpContext`를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-347">The `RewriteContext` exposes the `HttpContext` for use in your method.</span></span> <span data-ttu-id="686c7-348">`RewriteContext.Result`는 추가적인 파이프라인 처리가 수행되는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-348">The `RewriteContext.Result` determines how additional pipeline processing is handled.</span></span>

| `RewriteContext.Result`              | <span data-ttu-id="686c7-349">작업</span><span class="sxs-lookup"><span data-stu-id="686c7-349">Action</span></span>                                                          |
| ------------------------------------ | --------------------------------------------------------------- |
| <span data-ttu-id="686c7-350">`RuleResult.ContinueRules`(기본값)</span><span class="sxs-lookup"><span data-stu-id="686c7-350">`RuleResult.ContinueRules` (default)</span></span> | <span data-ttu-id="686c7-351">계속 규칙 적용</span><span class="sxs-lookup"><span data-stu-id="686c7-351">Continue applying rules</span></span>                                         |
| `RuleResult.EndResponse`             | <span data-ttu-id="686c7-352">규칙 적용을 중지하고 응답 전송</span><span class="sxs-lookup"><span data-stu-id="686c7-352">Stop applying rules and send the response</span></span>                       |
| `RuleResult.SkipRemainingRules`      | <span data-ttu-id="686c7-353">규칙 적용을 중지하고 다음 미들웨어에 컨텍스트 보내기</span><span class="sxs-lookup"><span data-stu-id="686c7-353">Stop applying rules and send the context to the next middleware</span></span> |

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=14)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .Add(RedirectXMLRequests);

    app.UseRewriter(options);
}
```

::: moniker-end

<span data-ttu-id="686c7-354">샘플 앱은 *.xml*로 끝나는 경로에 대한 요청을 리디렉션하는 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-354">The sample app demonstrates a method that redirects requests for paths that end with *.xml*.</span></span> <span data-ttu-id="686c7-355">가령 `/file.xml`을 요청할 경우 `/xmlfiles/file.xml`로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-355">If you make a request for `/file.xml`, it's redirected to `/xmlfiles/file.xml`.</span></span> <span data-ttu-id="686c7-356">상태 코드는 301 (영구 이동)으로 설정하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-356">The status code is set to 301 (Moved Permanently).</span></span> <span data-ttu-id="686c7-357">리디렉션의 경우 명시적으로 응답의 상태 코드를 설정해야 하며, 그렇지 않으면 200 (정상) 상태 코드가 반환되고 클라이언트에서 리디렉션이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-357">For a redirect, you must explicitly set the status code of the response; otherwise, a 200 (OK) status code is returned and the redirect won't occur on the client.</span></span>

[!code-csharp[](url-rewriting/sample/RewriteRules.cs?name=snippet1)]

<span data-ttu-id="686c7-358">원본 요청: `/file.xml`</span><span class="sxs-lookup"><span data-stu-id="686c7-358">Original Request: `/file.xml`</span></span>

![file.xml에 대한 요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_xml_requests.png)

### <a name="irule-based-rule"></a><span data-ttu-id="686c7-360">IRule 기반 규칙</span><span class="sxs-lookup"><span data-stu-id="686c7-360">IRule-based rule</span></span>

<span data-ttu-id="686c7-361">`Add(IRule)`를 사용하여 `IRule` 인터페이스를 구현하는 클래스에서 사용자 고유의 규칙 논리를 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-361">Use `Add(IRule)` to encapsulate your own rule logic in a class that implements the `IRule` interface.</span></span> <span data-ttu-id="686c7-362">`IRule`을 사용하면 메서드 기반 규칙 방식을 사용하는 것보다 더 많은 유연성을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-362">Using an `IRule` provides greater flexibility over using the method-based rule approach.</span></span> <span data-ttu-id="686c7-363">구현 클래스에는 `ApplyRule` 메서드에 대한 매개 변수를 전달할 수 있는 생성자가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-363">Your implementaion class may include a constructor, where you can pass in parameters for the `ApplyRule` method.</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=15-16)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .Add(new RedirectImageRequests(".png", "/png-images"))
        .Add(new RedirectImageRequests(".jpg", "/jpg-images"));

    app.UseRewriter(options);
}
```

::: moniker-end

<span data-ttu-id="686c7-364">예제 응용 프로그램은 `extension` 및 `newPath` 매개 변수 값들이 다양한 조건을 만족하는지 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-364">The values of the parameters in the sample app for the `extension` and the `newPath` are checked to meet several conditions.</span></span> <span data-ttu-id="686c7-365">`extension`매개 변수는 값을 포함하고 있어야 하고, 그 값은 *.png*, *.jpg*, 또는 *.gif* 중 하나이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-365">The `extension` must contain a value, and the value must be *.png*, *.jpg*, or *.gif*.</span></span> <span data-ttu-id="686c7-366">만약 `newPath`가 유효하지 않으면 `ArgumentException`이 던져집니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-366">If the `newPath` isn't valid, an `ArgumentException` is thrown.</span></span> <span data-ttu-id="686c7-367">*image.png*를 요청하면 `/png-images/image.png`로 요청이 리디렉션 됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-367">If you make a request for *image.png*, it's redirected to `/png-images/image.png`.</span></span> <span data-ttu-id="686c7-368">그리고 *image.jpg*를 요청하면 `/jpg-images/image.jpg`로 요청이 리디렉션 됩니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-368">If you make a request for *image.jpg*, it's redirected to `/jpg-images/image.jpg`.</span></span> <span data-ttu-id="686c7-369">상태 코드는 301 (영구 이동)으로 설정하고 규칙 처리를 중지하고 응답을 전송하도록 `context.Result`를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="686c7-369">The status code is set to 301 (Moved Permanently), and the `context.Result` is set to stop processing rules and send the response.</span></span>

[!code-csharp[](url-rewriting/sample/RewriteRules.cs?name=snippet2)]

<span data-ttu-id="686c7-370">원본 요청: `/image.png`</span><span class="sxs-lookup"><span data-stu-id="686c7-370">Original Request: `/image.png`</span></span>

![image.png에 대한 요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_png_requests.png)

<span data-ttu-id="686c7-372">원본 요청: `/image.jpg`</span><span class="sxs-lookup"><span data-stu-id="686c7-372">Original Request: `/image.jpg`</span></span>

![image.jpg에 대한 요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_jpg_requests.png)

## <a name="regex-examples"></a><span data-ttu-id="686c7-374">정규식 예제</span><span class="sxs-lookup"><span data-stu-id="686c7-374">Regex examples</span></span>

| <span data-ttu-id="686c7-375">Goal</span><span class="sxs-lookup"><span data-stu-id="686c7-375">Goal</span></span> | <span data-ttu-id="686c7-376">정규식 문자열 및</span><span class="sxs-lookup"><span data-stu-id="686c7-376">Regex String &</span></span><br><span data-ttu-id="686c7-377">일치 예제</span><span class="sxs-lookup"><span data-stu-id="686c7-377">Match Example</span></span> | <span data-ttu-id="686c7-378">대체 문자열 및</span><span class="sxs-lookup"><span data-stu-id="686c7-378">Replacement String &</span></span><br><span data-ttu-id="686c7-379">출력 예제</span><span class="sxs-lookup"><span data-stu-id="686c7-379">Output Example</span></span> |
| ---- | :-----------------------------: | :------------------------------------: |
| <span data-ttu-id="686c7-380">경로를 쿼리 문자열로 재작성</span><span class="sxs-lookup"><span data-stu-id="686c7-380">Rewrite path into querystring</span></span> | `^path/(.*)/(.*)`<br>`/path/abc/123` | `path?var1=$1&var2=$2`<br>`/path?var1=abc&var2=123` |
| <span data-ttu-id="686c7-381">후행 슬래시 제거</span><span class="sxs-lookup"><span data-stu-id="686c7-381">Strip trailing slash</span></span> | `(.*)/$`<br>`/path/` | `$1`<br>`/path` |
| <span data-ttu-id="686c7-382">후행 슬래시 적용</span><span class="sxs-lookup"><span data-stu-id="686c7-382">Enforce trailing slash</span></span> | `(.*[^/])$`<br>`/path` | `$1/`<br>`/path/` |
| <span data-ttu-id="686c7-383">특정 요청 재작성 방지</span><span class="sxs-lookup"><span data-stu-id="686c7-383">Avoid rewriting specific requests</span></span> | <span data-ttu-id="686c7-384">`^(.*)(?<!\.axd)$` 또는 `^(?!.*\.axd$)(.*)$`</span><span class="sxs-lookup"><span data-stu-id="686c7-384">`^(.*)(?<!\.axd)$` or `^(?!.*\.axd$)(.*)$`</span></span><br><span data-ttu-id="686c7-385">예: `/resource.htm`</span><span class="sxs-lookup"><span data-stu-id="686c7-385">Yes: `/resource.htm`</span></span><br><span data-ttu-id="686c7-386">아니요: `/resource.axd`</span><span class="sxs-lookup"><span data-stu-id="686c7-386">No: `/resource.axd`</span></span> | `rewritten/$1`<br>`/rewritten/resource.htm`<br>`/resource.axd` |
| <span data-ttu-id="686c7-387">URL 세그먼트 재정렬</span><span class="sxs-lookup"><span data-stu-id="686c7-387">Rearrange URL segments</span></span> | `path/(.*)/(.*)/(.*)`<br>`path/1/2/3` | `path/$3/$2/$1`<br>`path/3/2/1` |
| <span data-ttu-id="686c7-388">URL 세그먼트 대체</span><span class="sxs-lookup"><span data-stu-id="686c7-388">Replace a URL segment</span></span> | `^(.*)/segment2/(.*)`<br>`/segment1/segment2/segment3` | `$1/replaced/$2`<br>`/segment1/replaced/segment3` |

## <a name="additional-resources"></a><span data-ttu-id="686c7-389">추가 자료</span><span class="sxs-lookup"><span data-stu-id="686c7-389">Additional resources</span></span>

* [<span data-ttu-id="686c7-390">응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="686c7-390">Application Startup</span></span>](startup.md)
* [<span data-ttu-id="686c7-391">미들웨어</span><span class="sxs-lookup"><span data-stu-id="686c7-391">Middleware</span></span>](xref:fundamentals/middleware/index)
* [<span data-ttu-id="686c7-392">.NET에서의 정규식</span><span class="sxs-lookup"><span data-stu-id="686c7-392">Regular expressions in .NET</span></span>](/dotnet/articles/standard/base-types/regular-expressions)
* [<span data-ttu-id="686c7-393">정규식 언어 - 빠른 참조</span><span class="sxs-lookup"><span data-stu-id="686c7-393">Regular expression language - quick reference</span></span>](/dotnet/articles/standard/base-types/quick-ref)
* [<span data-ttu-id="686c7-394">Apache mod_rewrite</span><span class="sxs-lookup"><span data-stu-id="686c7-394">Apache mod_rewrite</span></span>](https://httpd.apache.org/docs/2.4/rewrite/)
* [<span data-ttu-id="686c7-395">Url 재작성 모듈 2.0 사용(IIS용)</span><span class="sxs-lookup"><span data-stu-id="686c7-395">Using Url Rewrite Module 2.0 (for IIS)</span></span>](/iis/extensions/url-rewrite-module/using-url-rewrite-module-20)
* [<span data-ttu-id="686c7-396">URL 재작성 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="686c7-396">URL Rewrite Module Configuration Reference</span></span>](/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference)
* [<span data-ttu-id="686c7-397">IIS URL 재작성 모듈 포럼</span><span class="sxs-lookup"><span data-stu-id="686c7-397">IIS URL Rewrite Module Forum</span></span>](https://forums.iis.net/1152.aspx)
* [<span data-ttu-id="686c7-398">간단한 URL 구조 유지</span><span class="sxs-lookup"><span data-stu-id="686c7-398">Keep a simple URL structure</span></span>](https://support.google.com/webmasters/answer/76329?hl=en)
* [<span data-ttu-id="686c7-399">10가지 URL 재작성 팁과 요령</span><span class="sxs-lookup"><span data-stu-id="686c7-399">10 URL Rewriting Tips and Tricks</span></span>](http://ruslany.net/2009/04/10-url-rewriting-tips-and-tricks/)
* [<span data-ttu-id="686c7-400">슬래시 여부</span><span class="sxs-lookup"><span data-stu-id="686c7-400">To slash or not to slash</span></span>](https://webmasters.googleblog.com/2010/04/to-slash-or-not-to-slash.html)
