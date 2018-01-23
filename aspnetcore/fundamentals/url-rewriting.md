---
title: "URL의 ASP.NET Core 미들웨어를 다시 작성"
author: guardrex
description: "다시 작성 및 ASP.NET Core 응용 프로그램의 URL 재작성 미들웨어와 리디렉션 URL에 알아봅니다."
ms.author: riande
manager: wpickett
ms.date: 08/17/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/url-rewriting
ms.openlocfilehash: 99f8d1cc73fdcbd99cffe595ae89f3c61a6f9a53
ms.sourcegitcommit: 3d512ea991ac36dfd4c800b7d1f8a27bfc50635e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2018
---
# <a name="url-rewriting-middleware-in-aspnet-core"></a><span data-ttu-id="74794-103">URL의 ASP.NET Core 미들웨어를 다시 작성</span><span class="sxs-lookup"><span data-stu-id="74794-103">URL Rewriting Middleware in ASP.NET Core</span></span>

<span data-ttu-id="74794-104">여 [Luke Latham](https://github.com/guardrex) 및 [Mikael Mengistu](https://github.com/mikaelm12)</span><span class="sxs-lookup"><span data-stu-id="74794-104">By [Luke Latham](https://github.com/guardrex) and [Mikael Mengistu](https://github.com/mikaelm12)</span></span>

<span data-ttu-id="74794-105">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="74794-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="74794-106">URL 다시 쓰기는 하나 이상의 미리 정의 된 규칙을 기반으로 하는 Url 요청을 수정 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-106">URL rewriting is the act of modifying request URLs based on one or more predefined rules.</span></span> <span data-ttu-id="74794-107">URL 다시 작성 하는 위치 및 주소 밀접 하 게 연결 되지 않은 리소스 위치 및 해당 주소 간의 추상화를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74794-107">URL rewriting creates an abstraction between resource locations and their addresses so that the locations and addresses are not tightly linked.</span></span> <span data-ttu-id="74794-108">URL 다시 쓰기는 중요 한 몇 가지 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-108">There are several scenarios where URL rewriting is valuable:</span></span>
* <span data-ttu-id="74794-109">이동 또는 이러한 리소스에 대 한 안정적인 로케이터를 유지 관리 하는 동안 서버 리소스를 일시적 또는 영구적으로 대체</span><span class="sxs-lookup"><span data-stu-id="74794-109">Moving or replacing server resources temporarily or permanently while maintaining stable locators for those resources</span></span>
* <span data-ttu-id="74794-110">하나의 응용 프로그램의 영역에서 또는 다른 앱에서 처리 중인 요청과 분</span><span class="sxs-lookup"><span data-stu-id="74794-110">Splitting request processing across different apps or across areas of one app</span></span>
* <span data-ttu-id="74794-111">제거, 추가 또는 들어오는 요청에 URL 세그먼트를 다시 구성</span><span class="sxs-lookup"><span data-stu-id="74794-111">Removing, adding, or reorganizing URL segments on incoming requests</span></span>
* <span data-ttu-id="74794-112">공용 Url에 대 한 검색 엔진 최적화 SEO () 최적화</span><span class="sxs-lookup"><span data-stu-id="74794-112">Optimizing public URLs for Search Engine Optimization (SEO)</span></span>
* <span data-ttu-id="74794-113">링크를 클릭 하면 경우가 콘텐츠를 예측 하는 데 도움이 공용 친화적 Url의 사용 허용</span><span class="sxs-lookup"><span data-stu-id="74794-113">Permitting the use of friendly public URLs to help people predict the content they will find by following a link</span></span>
* <span data-ttu-id="74794-114">끝점을 보호 하는 안전 하지 않은 요청 리디렉션</span><span class="sxs-lookup"><span data-stu-id="74794-114">Redirecting insecure requests to secure endpoints</span></span>
* <span data-ttu-id="74794-115">이미지 hotlinking 방지</span><span class="sxs-lookup"><span data-stu-id="74794-115">Preventing image hotlinking</span></span>

<span data-ttu-id="74794-116">여러 가지 방법으로 URL을 변경 하 고, regex, Apache mod_rewrite 모듈 규칙, IIS를 다시 작성 모듈 규칙을 포함 하 고, 사용자 지정 규칙 논리를 사용 하 여에 대 한 규칙을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-116">You can define rules for changing the URL in several ways, including regex, Apache mod_rewrite module rules, IIS Rewrite Module rules, and using custom rule logic.</span></span> <span data-ttu-id="74794-117">이 문서는 ASP.NET Core 응용 프로그램에서 URL 다시 쓰기 미들웨어를 사용 하는 방법에 대 한 지침이 포함 된 URL 다시 쓰기를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-117">This document introduces URL rewriting with instructions on how to use URL Rewriting Middleware in ASP.NET Core apps.</span></span>

> [!NOTE]
> <span data-ttu-id="74794-118">URL 다시 쓰기 응용 프로그램의 성능이 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-118">URL rewriting can reduce the performance of an app.</span></span> <span data-ttu-id="74794-119">가능한 경우 규칙의 복잡성와 수를 제한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-119">Where feasible, you should limit the number and complexity of rules.</span></span>

## <a name="url-redirect-and-url-rewrite"></a><span data-ttu-id="74794-120">URL 리디렉션 및 URL 다시 쓰기</span><span class="sxs-lookup"><span data-stu-id="74794-120">URL redirect and URL rewrite</span></span>
<span data-ttu-id="74794-121">단어 사이의 차이 *URL 리디렉션* 및 *URL 재작성* 에 미묘한 보일 수 있지만 첫 번째 요소가 있 클라이언트에 리소스를 제공 하는 데 중요 한 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-121">The difference in wording between *URL redirect* and *URL rewrite* may seem subtle at first but has important implications for providing resources to clients.</span></span> <span data-ttu-id="74794-122">ASP.NET Core URL 다시 쓰기 미들웨어는 모두에 대 한 필요성을 충족 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-122">ASP.NET Core's URL Rewriting Middleware is capable of meeting the need for both.</span></span>

<span data-ttu-id="74794-123">A *URL 리디렉션* 는 클라이언트 쪽 작업으로, 다른 주소에서 리소스에 액세스 하려면 클라이언트에 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-123">A *URL redirect* is a client-side operation, where the client is instructed to access a resource at another address.</span></span> <span data-ttu-id="74794-124">이 서버에 왕복을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-124">This requires a round-trip to the server.</span></span> <span data-ttu-id="74794-125">클라이언트는 리소스에 대 한 새 요청을 클라이언트로 반환 된 리디렉션 URL이 브라우저의 주소 표시줄에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74794-125">The redirect URL returned to the client appears in the browser's address bar when the client makes a new request for the resource.</span></span> 

<span data-ttu-id="74794-126">경우 `/resource` 은 *리디렉션* 를 `/different-resource`, 클라이언트 요청 `/resource`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-126">If `/resource` is *redirected* to `/different-resource`, the client requests `/resource`.</span></span> <span data-ttu-id="74794-127">서버가 응답 하는 클라이언트에서 리소스를 가져올 해야 `/different-resource` 임시 또는 영구 리디렉션 임을 나타내는 상태 코드와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-127">The server responds that the client should obtain the resource at `/different-resource` with a status code indicating that the redirect is either temporary or permanent.</span></span> <span data-ttu-id="74794-128">클라이언트에 리디렉션 URL에 대 한 리소스에 대 한 새 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-128">The client executes a new request for the resource at the redirect URL.</span></span>

![WebAPI 서비스 끝점 v2 (버전 2) 서버를 일시적으로 변경 버전 (v1) 1에서에서 되었습니다.](url-rewriting/_static/url_redirect.png)

<span data-ttu-id="74794-134">를 다른 URL로 요청을 리디렉션하는 경우 리디렉션 영구 또는 임시 인지 여부를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-134">When redirecting requests to a different URL, you indicate whether the redirect is permanent or temporary.</span></span> <span data-ttu-id="74794-135">301 (영구적 이동) 상태 코드는 리소스에 대 한 모든 향후 요청 새 URL을 사용 하도록 클라이언트에 게 지시 하 시겠습니까 고 있는 리소스에 영구 새 URL 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74794-135">The 301 (Moved Permanently) status code is used where the resource has a new, permanent URL and you wish to instruct the client that all future requests for the resource should use the new URL.</span></span> <span data-ttu-id="74794-136">*301 상태 코드를 받을 때 클라이언트는 응답을 캐시할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="74794-136">*The client may cache the response when a 301 status code is received.*</span></span> <span data-ttu-id="74794-137">302 (있음) 상태 코드 변경, 클라이언트를 저장 하 고 리디렉션 URL을 나중에 다시 사용 하지 않아야 하 여기서 리디렉션은 임시 또는 제목 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74794-137">The 302 (Found) status code is used where the redirection is temporary or generally subject to change, such that the client shouldn't store and reuse the redirect URL in the future.</span></span> <span data-ttu-id="74794-138">자세한 내용은 참조 [RFC 2616: 상태 코드 정의](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-138">For more information, see [RFC 2616: Status Code Definitions](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).</span></span>

<span data-ttu-id="74794-139">A *URL 재작성* 다른 리소스 주소에서 리소스를 제공 하는 서버 쪽 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-139">A *URL rewrite* is a server-side operation to provide a resource from a different resource address.</span></span> <span data-ttu-id="74794-140">URL 다시 쓰기 서버에 대 한 라운드트립이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-140">Rewriting a URL doesn't require a round-trip to the server.</span></span> <span data-ttu-id="74794-141">다시 쓴된 URL 클라이언트에 반환 되지 않습니다 및 브라우저의 주소 표시줄에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-141">The rewritten URL isn't returned to the client and won't appear in the browser's address bar.</span></span> <span data-ttu-id="74794-142">때 `/resource` 은 *다시 작성* 를 `/different-resource`, 클라이언트 요청 `/resource`와 서버 *내부적으로* 인출에서 리소스 `/different-resource`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-142">When `/resource` is *rewritten* to `/different-resource`, the client requests `/resource`, and the server *internally* fetches the resource at `/different-resource`.</span></span> <span data-ttu-id="74794-143">클라이언트를 다시 작성된 URL에 리소스를 검색할 수 있지만 해당 요청을 수행 하 고 응답을 받는 리소스 다시 작성된 URL에 있는지 클라이언트 정보 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-143">Although the client might be able to retrieve the resource at the rewritten URL, the client won't be informed that the resource exists at the rewritten URL when it makes its request and receives the response.</span></span>

![WebAPI 서비스 끝점 (v1) 버전 1에서에서 v2 (버전 2) 서버에서 변경 되었습니다.](url-rewriting/_static/url_rewrite.png)

## <a name="url-rewriting-sample-app"></a><span data-ttu-id="74794-148">URL 다시 쓰기 샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="74794-148">URL rewriting sample app</span></span>
<span data-ttu-id="74794-149">URL 다시 쓰기 사용 하 여 미들웨어의 기능을 탐색할 수 있습니다는 [URL 다시 쓰기 샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/)합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-149">You can explore the features of the URL Rewriting Middleware with the [URL rewriting sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/).</span></span> <span data-ttu-id="74794-150">응용 프로그램 다시 쓰기를 적용 하 고 리디렉션 규칙 및 다시 작성 또는 리디렉션 URL을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="74794-150">The app applies rewrite and redirect rules and shows the rewritten or redirected URL.</span></span>

## <a name="when-to-use-url-rewriting-middleware"></a><span data-ttu-id="74794-151">URL 다시 쓰기 미들웨어를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="74794-151">When to use URL Rewriting Middleware</span></span>
<span data-ttu-id="74794-152">URL 다시 쓰기 미들웨어를 사용 하 여 사용할 수 없는 경우는 [URL 재작성 모듈](https://www.iis.net/downloads/microsoft/url-rewrite) Windows 서버에서 iis는 [Apache mod_rewrite 모듈](https://httpd.apache.org/docs/2.4/rewrite/) Apache 서버의 [Nginx에URL다시쓰기](https://www.nginx.com/blog/creating-nginx-rewrite-rules/), 응용 프로그램에서 호스팅되는 또는 [HTTP.sys 서버](xref:fundamentals/servers/httpsys) (이전의 [WebListener](xref:fundamentals/servers/weblistener)).</span><span class="sxs-lookup"><span data-stu-id="74794-152">Use URL Rewriting Middleware when you are unable to use the [URL Rewrite module](https://www.iis.net/downloads/microsoft/url-rewrite) with IIS on Windows Server, the [Apache mod_rewrite module](https://httpd.apache.org/docs/2.4/rewrite/) on Apache Server, [URL rewriting on Nginx](https://www.nginx.com/blog/creating-nginx-rewrite-rules/), or your app is hosted on [HTTP.sys server](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)).</span></span> <span data-ttu-id="74794-153">기술을 사용 하는 서버 기반 URL 다시 쓰기 IIS, Apache 또는 Nginx 주된 이유는 있는지 미들웨어 이러한 모듈의 전체 기능을 지원 하지 않습니다 및 미들웨어의 성능을 때문일 수와 일치 하지 않습니다는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-153">The main reasons to use the server-based URL rewriting technologies in IIS, Apache, or Nginx are that the middleware doesn't support the full features of these modules and the performance of the middleware probably won't match that of the modules.</span></span> <span data-ttu-id="74794-154">그러나 일부의 기능은 사용 하지 않는 ASP.NET Core 프로젝트와 같은 서버 모듈의 `IsFile` 및 `IsDirectory` IIS 재작성 모듈의 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-154">However, there are some features of the server modules that don't work with ASP.NET Core projects, such as the `IsFile` and `IsDirectory` constraints of the IIS Rewrite module.</span></span> <span data-ttu-id="74794-155">이러한 시나리오에서 미들웨어를 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-155">In these scenarios, use the middleware instead.</span></span>

## <a name="package"></a><span data-ttu-id="74794-156">패키지</span><span class="sxs-lookup"><span data-stu-id="74794-156">Package</span></span>
<span data-ttu-id="74794-157">미들웨어를 프로젝트에 포함 하려면 추가에 대 한 참조는 [ `Microsoft.AspNetCore.Rewrite` ](https://www.nuget.org/packages/Microsoft.AspNetCore.Rewrite/) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-157">To include the middleware in your project, add a reference to the [`Microsoft.AspNetCore.Rewrite`](https://www.nuget.org/packages/Microsoft.AspNetCore.Rewrite/) package.</span></span> <span data-ttu-id="74794-158">이 기능은 이상 ASP.NET Core 1.1을 대상으로 하는 응용 프로그램에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-158">This feature is available for apps that target ASP.NET Core 1.1 or later.</span></span>

## <a name="extension-and-options"></a><span data-ttu-id="74794-159">확장 및 옵션</span><span class="sxs-lookup"><span data-stu-id="74794-159">Extension and options</span></span>
<span data-ttu-id="74794-160">URL 재작성을 설정 하 고 규칙의 인스턴스를 만들어 리디렉션하는 `RewriteOptions` 각 규칙에 대 한 확장 메서드를 사용 하 여 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-160">Establish your URL rewrite and redirect rules by creating an instance of the `RewriteOptions` class with extension methods for each of your rules.</span></span> <span data-ttu-id="74794-161">여러 규칙 싶다는 의사를 처리 하는 순서를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-161">Chain multiple rules in the order that you would like them processed.</span></span> <span data-ttu-id="74794-162">`RewriteOptions` 으로 요청 파이프라인에 추가 되는 URL 다시 쓰기 미들웨어로 전달 되 `app.UseRewriter(options);`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-162">The `RewriteOptions` are passed into the URL Rewriting Middleware as it's added to the request pipeline with `app.UseRewriter(options);`.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="74794-163">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="74794-163">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="74794-164">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="74794-164">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1)]

---

### <a name="url-redirect"></a><span data-ttu-id="74794-165">URL 리디렉션</span><span class="sxs-lookup"><span data-stu-id="74794-165">URL redirect</span></span>
<span data-ttu-id="74794-166">사용 하 여 `AddRedirect` 요청을 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-166">Use `AddRedirect` to redirect requests.</span></span> <span data-ttu-id="74794-167">첫 번째 매개 변수는 받는 URL의 경로에 일치 하는 regex의 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-167">The first parameter contains your regex for matching on the path of the incoming URL.</span></span> <span data-ttu-id="74794-168">두 번째 매개 변수 대체 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-168">The second parameter is the replacement string.</span></span> <span data-ttu-id="74794-169">세 번째 매개 변수가 있는 경우 상태 코드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-169">The third parameter, if present, specifies the status code.</span></span> <span data-ttu-id="74794-170">상태 코드를 지정 하지 않으면 기본값으로 302 (있음)을 나타내는 리소스는 일시적으로 이동 또는 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-170">If you don't specify the status code, it defaults to 302 (Found), which indicates that the resource is temporarily moved or replaced.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="74794-171">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="74794-171">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=5)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="74794-172">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="74794-172">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=2)]

---

<span data-ttu-id="74794-173">개발자 도구를 사용 하도록 설정 된 브라우저에서 요청 경로로 샘플 응용 프로그램을 할 `/redirect-rule/1234/5678`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-173">In a browser with developer tools enabled, make a request to the sample app with the path `/redirect-rule/1234/5678`.</span></span> <span data-ttu-id="74794-174">요청 경로 일치 하는 regex `redirect-rule/(.*)`, 및 경로 아래 템플릿으로 바뀝니다 `/redirected/1234/5678`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-174">The regex matches the request path on `redirect-rule/(.*)`, and the path is replaced with `/redirected/1234/5678`.</span></span> <span data-ttu-id="74794-175">리디렉션 URL 302 (있음) 상태 코드를 사용 하 여 클라이언트에 다시 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74794-175">The redirect URL is sent back to the client with a 302 (Found) status code.</span></span> <span data-ttu-id="74794-176">브라우저에서 브라우저의 주소 표시줄에 표시 되는 리디렉션 URL에서 새 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-176">The browser makes a new request at the redirect URL, which appears in the browser's address bar.</span></span> <span data-ttu-id="74794-177">리디렉션 URL에 일치 하는 샘플 앱에 없는 규칙이, 하므로 두 번째 요청 응용 프로그램에서 보낸 200 (정상) 응답을 수신 및 응답의 본문으로 리디렉션 URL을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-177">Since no rules in the sample app match on the redirect URL, the second request receives a 200 (OK) response from the app and the body of the response shows the redirect URL.</span></span> <span data-ttu-id="74794-178">URL은 서버로 왕복이 수행 됩니다 *리디렉션*합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-178">A roundtrip is made to the server when a URL is *redirected*.</span></span>

> [!WARNING]
> <span data-ttu-id="74794-179">리디렉션 규칙을 설정할 때 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-179">Be cautious when establishing your redirect rules.</span></span> <span data-ttu-id="74794-180">리디렉션 규칙 리디렉션 이후에 포함 하 여 응용 프로그램에 각 요청에 대해 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74794-180">Your redirect rules are evaluated on each request to the app, including after a redirect.</span></span> <span data-ttu-id="74794-181">가 실수로 쉽게 무한 리디렉션 루프가 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-181">It's easy to accidently create a loop of infinite redirects.</span></span>

<span data-ttu-id="74794-182">원래 요청:`/redirect-rule/1234/5678`</span><span class="sxs-lookup"><span data-stu-id="74794-182">Original Request: `/redirect-rule/1234/5678`</span></span>

![브라우저 창을 요청 및 응답을 추적 하는 개발자 도구](url-rewriting/_static/add_redirect.png)

<span data-ttu-id="74794-184">괄호 안에 포함 된 식의 일부 라고는 *캡처 그룹*합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-184">The part of the expression contained within parentheses is called a *capture group*.</span></span> <span data-ttu-id="74794-185">점 (`.`) 식의 의미 *임의의 문자*합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-185">The dot (`.`) of the expression means *match any character*.</span></span> <span data-ttu-id="74794-186">별표 (`*`) 나타냅니다 *앞에 오는 문자 0 회 이상 일치*합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-186">The asterisk (`*`) indicates *match the preceding character zero or more times*.</span></span> <span data-ttu-id="74794-187">따라서 URL의 마지막 두 개의 경로 세그먼트 `1234/5678`, 캡처 그룹에 의해 캡처된 `(.*)`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-187">Therefore, the last two path segments of the URL, `1234/5678`, are captured by capture group `(.*)`.</span></span> <span data-ttu-id="74794-188">후 요청 URL에서 제공한 값 `redirect-rule/` 이 단일 캡처 그룹에 의해 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="74794-188">Any value you provide in the request URL after `redirect-rule/` is captured by this single capture group.</span></span>

<span data-ttu-id="74794-189">대체 문자열에 캡처된 그룹은 달러 기호를 사용 하 여 문자열에 삽입 (`$`) 다음 캡처의 시퀀스 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-189">In the replacement string, captured groups are injected into the string with the dollar sign (`$`) followed by the sequence number of the capture.</span></span> <span data-ttu-id="74794-190">첫 번째 캡처 그룹 값에 따라 획득 된은 `$1`, 두 번째 `$2`, 하며 프로그램 정규식에서 캡처 그룹에 대 한 시퀀스에서 지속 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-190">The first capture group value is obtained with `$1`, the second with `$2`, and they continue in sequence for the capture groups in your regex.</span></span> <span data-ttu-id="74794-191">캡처된 그룹이 하나만 있는에서 경우 리디렉션 규칙 regex 샘플 응용 프로그램을 인 대체 문자열에 삽입 된 그룹이 하나만 있으므로 `$1`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-191">There's only one captured group in the redirect rule regex in the sample app, so there's only one injected group in the replacement string, which is `$1`.</span></span> <span data-ttu-id="74794-192">URL은 규칙을 적용 하면 `/redirected/1234/5678`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-192">When the rule is applied, the URL becomes `/redirected/1234/5678`.</span></span>

<a name="url-redirect-to-secure-endpoint"></a>
### <a name="url-redirect-to-a-secure-endpoint"></a><span data-ttu-id="74794-193">보안 끝점을 URL 리디렉션</span><span class="sxs-lookup"><span data-stu-id="74794-193">URL redirect to a secure endpoint</span></span>
<span data-ttu-id="74794-194">사용 하 여 `AddRedirectToHttps` 동일한 호스트 및 HTTPS를 사용 하 여 경로에 HTTP 요청을 리디렉션할 수 (`https://`).</span><span class="sxs-lookup"><span data-stu-id="74794-194">Use `AddRedirectToHttps` to redirect HTTP requests to the same host and path using HTTPS (`https://`).</span></span> <span data-ttu-id="74794-195">상태 코드는 제공 되지 않는 경우 미들웨어 302 (있음) 기본값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74794-195">If the status code isn't supplied, the middleware defaults to 302 (Found).</span></span> <span data-ttu-id="74794-196">포트를 제공 하지 않으면, 미들웨어 기본적으로 `null`를로 변경 하는 프로토콜을 의미 하는 `https://` 클라이언트 포트 443에서 리소스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-196">If the port isn't supplied, the middleware defaults to `null`, which means the protocol changes to `https://` and the client accesses the resource on port 443.</span></span> <span data-ttu-id="74794-197">상태 코드 301 (영구적 이동)로 설정 하 고 5001이 고 다른 포트로 변경 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="74794-197">The example shows how to set the status code to 301 (Moved Permanently) and change the port to 5001.</span></span>
```csharp
var options = new RewriteOptions()
    .AddRedirectToHttps(301, 5001);

app.UseRewriter(options);
```
<span data-ttu-id="74794-198">사용 하 여 `AddRedirectToHttpsPermanent` 안전 하지 않은 요청을 동일한 호스트와 보안 HTTPS 프로토콜을 사용 하 여 경로 리디렉션하도록 (`https://` 포트 443).</span><span class="sxs-lookup"><span data-stu-id="74794-198">Use `AddRedirectToHttpsPermanent` to redirect insecure requests to the same host and path with secure HTTPS protocol (`https://` on port 443).</span></span> <span data-ttu-id="74794-199">상태 코드 301 (영구적 이동)를 설정 하는 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-199">The middleware sets the status code to 301 (Moved Permanently).</span></span>

<span data-ttu-id="74794-200">샘플 응용 프로그램은 사용 하는 방법을 보여 주는 수 `AddRedirectToHttps` 또는 `AddRedirectToHttpsPermanent`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-200">The sample app is capable of demonstrating how to use `AddRedirectToHttps` or `AddRedirectToHttpsPermanent`.</span></span> <span data-ttu-id="74794-201">확장 메서드를 추가 `RewriteOptions`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-201">Add the extension method to the `RewriteOptions`.</span></span> <span data-ttu-id="74794-202">모든 URL에서 응용 프로그램에 안전 하지 않은 요청을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-202">Make an insecure request to the app at any URL.</span></span> <span data-ttu-id="74794-203">자체 서명 된 인증서를 신뢰할 수 있는지 경고 브라우저 보안을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-203">Dismiss the browser security warning that the self-signed certificate is untrusted.</span></span>

<span data-ttu-id="74794-204">사용 하 여 원래 요청 `AddRedirectToHttps(301, 5001)`:`/secure`</span><span class="sxs-lookup"><span data-stu-id="74794-204">Original Request using `AddRedirectToHttps(301, 5001)`: `/secure`</span></span>

![브라우저 창을 요청 및 응답을 추적 하는 개발자 도구](url-rewriting/_static/add_redirect_to_https.png)

<span data-ttu-id="74794-206">사용 하 여 원래 요청 `AddRedirectToHttpsPermanent`:`/secure`</span><span class="sxs-lookup"><span data-stu-id="74794-206">Original Request using `AddRedirectToHttpsPermanent`: `/secure`</span></span>

![브라우저 창을 요청 및 응답을 추적 하는 개발자 도구](url-rewriting/_static/add_redirect_to_https_permanent.png)

### <a name="url-rewrite"></a><span data-ttu-id="74794-208">URL 다시 쓰기</span><span class="sxs-lookup"><span data-stu-id="74794-208">URL rewrite</span></span>
<span data-ttu-id="74794-209">사용 하 여 `AddRewrite` Url을 다시 작성 하기 위한 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74794-209">Use `AddRewrite` to create a rule for rewriting URLs.</span></span> <span data-ttu-id="74794-210">첫 번째 매개 변수는 들어오는 URL 경로에 일치 하는 regex의 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-210">The first parameter contains your regex for matching on the incoming URL path.</span></span> <span data-ttu-id="74794-211">두 번째 매개 변수 대체 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-211">The second parameter is the replacement string.</span></span> <span data-ttu-id="74794-212">세 번째 매개 변수 `skipRemainingRules: {true|false}`, 현재 규칙이 적용 되는 경우에 추가 재작성 규칙 건너뛸 것인지 여부는 미들웨어를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="74794-212">The third parameter, `skipRemainingRules: {true|false}`, indicates to the middleware whether or not to skip additional rewrite rules if the current rule is applied.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="74794-213">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="74794-213">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=6)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="74794-214">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="74794-214">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=3)]

---

<span data-ttu-id="74794-215">원래 요청:`/rewrite-rule/1234/5678`</span><span class="sxs-lookup"><span data-stu-id="74794-215">Original Request: `/rewrite-rule/1234/5678`</span></span>

![브라우저 창을 요청 및 응답을 추적 하는 개발자 도구](url-rewriting/_static/add_rewrite.png)

<span data-ttu-id="74794-217">정규식에서 첫 번째 점은 캐럿 (`^`) 식의 시작 부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-217">The first thing you notice in the regex is the carat (`^`) at the beginning of the expression.</span></span> <span data-ttu-id="74794-218">이 URL 경로의 시작 부분에서 일치 하는 시작 됨을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-218">This means that matching starts at the beginning of the URL path.</span></span>

<span data-ttu-id="74794-219">리디렉션 규칙을 사용 하면 앞의 예제에서 `redirect-rule/(.*)`, 정규식의 시작 부분에 없는 캐럿; 따라서 모든 수 앞에 있는 문자 `redirect-rule/` 성공한 일치에 대 한 경로에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-219">In the earlier example with the redirect rule, `redirect-rule/(.*)`, there's no carat at the start of the regex; therefore, any characters may precede `redirect-rule/` in the path for a successful match.</span></span>

| <span data-ttu-id="74794-220">Path</span><span class="sxs-lookup"><span data-stu-id="74794-220">Path</span></span>                               | <span data-ttu-id="74794-221">일치</span><span class="sxs-lookup"><span data-stu-id="74794-221">Match</span></span> |
| ---------------------------------- | :---: |
| `/redirect-rule/1234/5678`         | <span data-ttu-id="74794-222">예</span><span class="sxs-lookup"><span data-stu-id="74794-222">Yes</span></span>   |
| `/my-cool-redirect-rule/1234/5678` | <span data-ttu-id="74794-223">예</span><span class="sxs-lookup"><span data-stu-id="74794-223">Yes</span></span>   |
| `/anotherredirect-rule/1234/5678`  | <span data-ttu-id="74794-224">예</span><span class="sxs-lookup"><span data-stu-id="74794-224">Yes</span></span>   |

<span data-ttu-id="74794-225">다시 쓰기 규칙 `^rewrite-rule/(\d+)/(\d+)`, 경로로 시작 하는 경우에 일치 `rewrite-rule/`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-225">The rewrite rule, `^rewrite-rule/(\d+)/(\d+)`, only matches paths if they start with `rewrite-rule/`.</span></span> <span data-ttu-id="74794-226">다시 쓰기 규칙와 위의 리디렉션 규칙 간에 일치 하는 차이 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-226">Notice the difference in matching between the rewrite rule below and the redirect rule above.</span></span>

| <span data-ttu-id="74794-227">Path</span><span class="sxs-lookup"><span data-stu-id="74794-227">Path</span></span>                              | <span data-ttu-id="74794-228">일치</span><span class="sxs-lookup"><span data-stu-id="74794-228">Match</span></span> |
| --------------------------------- | :---: |
| `/rewrite-rule/1234/5678`         | <span data-ttu-id="74794-229">예</span><span class="sxs-lookup"><span data-stu-id="74794-229">Yes</span></span>   |
| `/my-cool-rewrite-rule/1234/5678` | <span data-ttu-id="74794-230">아니요</span><span class="sxs-lookup"><span data-stu-id="74794-230">No</span></span>    |
| `/anotherrewrite-rule/1234/5678`  | <span data-ttu-id="74794-231">아니요</span><span class="sxs-lookup"><span data-stu-id="74794-231">No</span></span>    |

<span data-ttu-id="74794-232">다음은 `^rewrite-rule/` 부분 식의은 두 개의 캡처 그룹 `(\d+)/(\d+)`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-232">Following the `^rewrite-rule/` portion of the expression, there are two capture groups, `(\d+)/(\d+)`.</span></span> <span data-ttu-id="74794-233">`\d` 의미 *숫자 (number)*합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-233">The `\d` signifies *match a digit (number)*.</span></span> <span data-ttu-id="74794-234">더하기 기호 (`+`) 의미 *앞에 오는 문자를 하나 이상의 일치*합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-234">The plus sign (`+`) means *match one or more of the preceding character*.</span></span> <span data-ttu-id="74794-235">따라서 URL에는 슬래시 다음에 다른 숫자와 앞에 숫자가 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-235">Therefore, the URL must contain a number followed by a forward-slash followed by another number.</span></span> <span data-ttu-id="74794-236">그룹은 다시 작성된 URL에 삽입이 캡처 `$1` 및 `$2`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-236">These capture groups are injected into the rewritten URL as `$1` and `$2`.</span></span> <span data-ttu-id="74794-237">다시 쓰기 규칙 대체 문자열은 문자열에 캡처된 그룹을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-237">The rewrite rule replacement string places the captured groups into the querystring.</span></span> <span data-ttu-id="74794-238">요청 된 경로 `/rewrite-rule/1234/5678` 에서 리소스를 가져올 수는 다시 작성 `/rewritten?var1=1234&var2=5678`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-238">The requested path of `/rewrite-rule/1234/5678` is rewritten to obtain the resource at `/rewritten?var1=1234&var2=5678`.</span></span> <span data-ttu-id="74794-239">쿼리 문자열은 원래 요청에 있는 경우 해당 데이터가 보존 됩니다 때 URL을 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-239">If a querystring is present on the original request, it's preserved when the URL is rewritten.</span></span>

<span data-ttu-id="74794-240">서버 리소스를 가져올 수 없는 왕복이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-240">There's no roundtrip to the server to obtain the resource.</span></span> <span data-ttu-id="74794-241">리소스가 존재 인출 개이고 200 (OK) 상태 코드를 사용 하 여 클라이언트에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-241">If the resource exists, it's fetched and returned to the client with a 200 (OK) status code.</span></span> <span data-ttu-id="74794-242">클라이언트가 리디렉션 없는 때문에 브라우저 주소 표시줄에 URL이 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-242">Because the client isn't redirected, the URL in the browser address bar doesn't change.</span></span> <span data-ttu-id="74794-243">클라이언트의 경우, 관련해 서 URL 다시 쓰기 작업을 하지 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-243">As far as the client is concerned, the URL rewrite operation never occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="74794-244">사용 하 여 `skipRemainingRules: true` 가능 하면 항상, 비용이 많이 드는 프로세스 일치 규칙을 사용 하면 응용 프로그램 응답 시간이 단축 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-244">Use `skipRemainingRules: true` whenever possible, because matching rules is an expensive process and reduces app response time.</span></span> <span data-ttu-id="74794-245">가장 빠른 응용 프로그램 응답:</span><span class="sxs-lookup"><span data-stu-id="74794-245">For the fastest app response:</span></span>
> * <span data-ttu-id="74794-246">가장 자주 일치 하는 규칙에 가장 자주 일치 하는 규칙에서 다시 쓰기 규칙을 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-246">Order your rewrite rules from the most frequently matched rule to the least frequently matched rule.</span></span>
> * <span data-ttu-id="74794-247">일치 하는 항목이 없는 추가 규칙 처리가 필요한 경우 나머지 규칙의 처리를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="74794-247">Skip the processing of the remaining rules when a match occurs and no additional rule processing is required.</span></span>

### <a name="apache-modrewrite"></a><span data-ttu-id="74794-248">Apache mod_rewrite</span><span class="sxs-lookup"><span data-stu-id="74794-248">Apache mod_rewrite</span></span>
<span data-ttu-id="74794-249">사용 하 여 Apache mod_rewrite 규칙 적용 `AddApacheModRewrite`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-249">Apply Apache mod_rewrite rules with `AddApacheModRewrite`.</span></span> <span data-ttu-id="74794-250">규칙 파일 앱 배포 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-250">Make sure that the rules file is deployed with the app.</span></span> <span data-ttu-id="74794-251">자세한 내용과 mod_rewrite 규칙의 예에 대 한 참조 [Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/)합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-251">For more information and examples of mod_rewrite rules, see [Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="74794-252">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="74794-252">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="74794-253">A `StreamReader` 에서 규칙을 읽는 데 사용 되는 *ApacheModRewrite.txt* 규칙 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-253">A `StreamReader` is used to read the rules from the *ApacheModRewrite.txt* rules file.</span></span>

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=1,7)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="74794-254">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="74794-254">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="74794-255">첫 번째 매개 변수를 사용는 `IFileProvider`를 통해 제공 하는 [종속성 주입](dependency-injection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-255">The first parameter takes an `IFileProvider`, which is provided via [Dependency Injection](dependency-injection.md).</span></span> <span data-ttu-id="74794-256">`IHostingEnvironment` 제공 하는 삽입 된 여 `ContentRootFileProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-256">The `IHostingEnvironment` is injected to provide the `ContentRootFileProvider`.</span></span> <span data-ttu-id="74794-257">두 번째 매개 변수는이 규칙 파일을 경로 *ApacheModRewrite.txt* 샘플 응용 프로그램에서입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-257">The second parameter is the path to your rules file, which is *ApacheModRewrite.txt* in the sample app.</span></span>

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=4)]

---

<span data-ttu-id="74794-258">샘플 응용 프로그램에서 요청을 리디렉션합니다 `/apache-mod-rules-redirect/(.\*)` 를 `/redirected?id=$1`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-258">The sample app redirects requests from `/apache-mod-rules-redirect/(.\*)` to `/redirected?id=$1`.</span></span> <span data-ttu-id="74794-259">응답 상태 코드 302 (있음)입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-259">The response status code is 302 (Found).</span></span>

[!code[Main](url-rewriting/samples/2.x/ApacheModRewrite.txt)]

<span data-ttu-id="74794-260">원래 요청:`/apache-mod-rules-redirect/1234`</span><span class="sxs-lookup"><span data-stu-id="74794-260">Original Request: `/apache-mod-rules-redirect/1234`</span></span>

![브라우저 창을 요청 및 응답을 추적 하는 개발자 도구](url-rewriting/_static/add_apache_mod_redirect.png)

##### <a name="supported-server-variables"></a><span data-ttu-id="74794-262">지원 되는 서버 변수</span><span class="sxs-lookup"><span data-stu-id="74794-262">Supported server variables</span></span>
<span data-ttu-id="74794-263">미들웨어는 다음 Apache mod_rewrite 서버 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-263">The middleware supports the following Apache mod_rewrite server variables:</span></span>
* <span data-ttu-id="74794-264">CONN_REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="74794-264">CONN_REMOTE_ADDR</span></span>
* <span data-ttu-id="74794-265">HTTP_ACCEPT</span><span class="sxs-lookup"><span data-stu-id="74794-265">HTTP_ACCEPT</span></span>
* <span data-ttu-id="74794-266">HTTP_CONNECTION</span><span class="sxs-lookup"><span data-stu-id="74794-266">HTTP_CONNECTION</span></span>
* <span data-ttu-id="74794-267">HTTP_COOKIE</span><span class="sxs-lookup"><span data-stu-id="74794-267">HTTP_COOKIE</span></span>
* <span data-ttu-id="74794-268">HTTP_FORWARDED</span><span class="sxs-lookup"><span data-stu-id="74794-268">HTTP_FORWARDED</span></span>
* <span data-ttu-id="74794-269">HTTP_HOST</span><span class="sxs-lookup"><span data-stu-id="74794-269">HTTP_HOST</span></span>
* <span data-ttu-id="74794-270">HTTP_REFERER</span><span class="sxs-lookup"><span data-stu-id="74794-270">HTTP_REFERER</span></span>
* <span data-ttu-id="74794-271">HTTP_USER_AGENT</span><span class="sxs-lookup"><span data-stu-id="74794-271">HTTP_USER_AGENT</span></span>
* <span data-ttu-id="74794-272">HTTPS</span><span class="sxs-lookup"><span data-stu-id="74794-272">HTTPS</span></span>
* <span data-ttu-id="74794-273">IPV6</span><span class="sxs-lookup"><span data-stu-id="74794-273">IPV6</span></span>
* <span data-ttu-id="74794-274">QUERY_STRING</span><span class="sxs-lookup"><span data-stu-id="74794-274">QUERY_STRING</span></span>
* <span data-ttu-id="74794-275">REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="74794-275">REMOTE_ADDR</span></span>
* <span data-ttu-id="74794-276">REMOTE_PORT</span><span class="sxs-lookup"><span data-stu-id="74794-276">REMOTE_PORT</span></span>
* <span data-ttu-id="74794-277">REQUEST_FILENAME</span><span class="sxs-lookup"><span data-stu-id="74794-277">REQUEST_FILENAME</span></span>
* <span data-ttu-id="74794-278">REQUEST_METHOD</span><span class="sxs-lookup"><span data-stu-id="74794-278">REQUEST_METHOD</span></span>
* <span data-ttu-id="74794-279">REQUEST_SCHEME</span><span class="sxs-lookup"><span data-stu-id="74794-279">REQUEST_SCHEME</span></span>
* <span data-ttu-id="74794-280">REQUEST_URI</span><span class="sxs-lookup"><span data-stu-id="74794-280">REQUEST_URI</span></span>
* <span data-ttu-id="74794-281">SCRIPT_FILENAME</span><span class="sxs-lookup"><span data-stu-id="74794-281">SCRIPT_FILENAME</span></span>
* <span data-ttu-id="74794-282">SERVER_ADDR</span><span class="sxs-lookup"><span data-stu-id="74794-282">SERVER_ADDR</span></span>
* <span data-ttu-id="74794-283">SERVER_PORT</span><span class="sxs-lookup"><span data-stu-id="74794-283">SERVER_PORT</span></span>
* <span data-ttu-id="74794-284">SERVER_PROTOCOL</span><span class="sxs-lookup"><span data-stu-id="74794-284">SERVER_PROTOCOL</span></span>
* <span data-ttu-id="74794-285">시간</span><span class="sxs-lookup"><span data-stu-id="74794-285">TIME</span></span>
* <span data-ttu-id="74794-286">TIME_DAY</span><span class="sxs-lookup"><span data-stu-id="74794-286">TIME_DAY</span></span>
* <span data-ttu-id="74794-287">TIME_HOUR</span><span class="sxs-lookup"><span data-stu-id="74794-287">TIME_HOUR</span></span>
* <span data-ttu-id="74794-288">TIME_MIN</span><span class="sxs-lookup"><span data-stu-id="74794-288">TIME_MIN</span></span>
* <span data-ttu-id="74794-289">TIME_MON</span><span class="sxs-lookup"><span data-stu-id="74794-289">TIME_MON</span></span>
* <span data-ttu-id="74794-290">TIME_SEC</span><span class="sxs-lookup"><span data-stu-id="74794-290">TIME_SEC</span></span>
* <span data-ttu-id="74794-291">TIME_WDAY</span><span class="sxs-lookup"><span data-stu-id="74794-291">TIME_WDAY</span></span>
* <span data-ttu-id="74794-292">TIME_YEAR</span><span class="sxs-lookup"><span data-stu-id="74794-292">TIME_YEAR</span></span>

### <a name="iis-url-rewrite-module-rules"></a><span data-ttu-id="74794-293">IIS URL 재작성 모듈 규칙</span><span class="sxs-lookup"><span data-stu-id="74794-293">IIS URL Rewrite Module rules</span></span>
<span data-ttu-id="74794-294">IIS URL 재작성 모듈에 적용 되는 규칙을 사용 하려면 사용 `AddIISUrlRewrite`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-294">To use rules that apply to the IIS URL Rewrite Module, use `AddIISUrlRewrite`.</span></span> <span data-ttu-id="74794-295">규칙 파일 앱 배포 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-295">Make sure that the rules file is deployed with the app.</span></span> <span data-ttu-id="74794-296">사용할 미들웨어 지시 하지 않는 프로그램 *web.config* 파일을 Windows Server IIS에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-296">Don't direct the middleware to use your *web.config* file when running on Windows Server IIS.</span></span> <span data-ttu-id="74794-297">Iis에서 이러한 규칙 외부에 저장 해야 하면 *web.config* IIS 재작성 모듈와 충돌 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-297">With IIS, these rules should be stored outside of your *web.config* to avoid conflicts with the IIS Rewrite module.</span></span> <span data-ttu-id="74794-298">자세한 내용과 예는 IIS URL 재작성 모듈 규칙에 대 한 참조 [를 사용 하 여 Url 재작성 모듈 2.0](https://docs.microsoft.com/iis/extensions/url-rewrite-module/using-url-rewrite-module-20) 및 [URL 재작성 모듈 구성 참조](https://docs.microsoft.com/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference)합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-298">For more information and examples of IIS URL Rewrite Module rules, see [Using Url Rewrite Module 2.0](https://docs.microsoft.com/iis/extensions/url-rewrite-module/using-url-rewrite-module-20) and [URL Rewrite Module Configuration Reference](https://docs.microsoft.com/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="74794-299">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="74794-299">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="74794-300">A `StreamReader` 에서 규칙을 읽는 데 사용 되는 *IISUrlRewrite.xml* 규칙 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-300">A `StreamReader` is used to read the rules from the *IISUrlRewrite.xml* rules file.</span></span>

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=2,8)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="74794-301">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="74794-301">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="74794-302">첫 번째 매개 변수를 사용는 `IFileProvider`, 두 번째 매개 변수, 즉 XML 규칙 파일에 경로 반면, *IISUrlRewrite.xml* 샘플 응용 프로그램에서입니다.</span><span class="sxs-lookup"><span data-stu-id="74794-302">The first parameter takes an `IFileProvider`, while the second parameter is the path to your XML rules file, which is *IISUrlRewrite.xml* in the sample app.</span></span>

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=5)]

---

<span data-ttu-id="74794-303">샘플 응용 프로그램의 요청을 다시 작성 `/iis-rules-rewrite/(.*)` 를 `/rewritten?id=$1`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-303">The sample app rewrites requests from `/iis-rules-rewrite/(.*)` to `/rewritten?id=$1`.</span></span> <span data-ttu-id="74794-304">응답은 200 (정상)이 상태 코드를 사용 하 여 클라이언트에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74794-304">The response is sent to the client with a 200 (OK) status code.</span></span>

[!code-xml[Main](url-rewriting/samples/2.x/IISUrlRewrite.xml)]

<span data-ttu-id="74794-305">원래 요청:`/iis-rules-rewrite/1234`</span><span class="sxs-lookup"><span data-stu-id="74794-305">Original Request: `/iis-rules-rewrite/1234`</span></span>

![브라우저 창을 요청 및 응답을 추적 하는 개발자 도구](url-rewriting/_static/add_iis_url_rewrite.png)

<span data-ttu-id="74794-307">영향을 미치는 방식 앱 바람직하지 않은 방법으로 구성 된 서버 수준 규칙 활성 IIS를 다시 작성 모듈 있는 경우 응용 프로그램에 대 한 IIS 재작성 모듈을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-307">If you have an active IIS Rewrite Module with server-level rules configured that would impact your app in undesirable ways, you can disable the IIS Rewrite Module for an app.</span></span> <span data-ttu-id="74794-308">자세한 내용은 참조 [비활성화 IIS 모듈](xref:host-and-deploy/iis/modules#disabling-iis-modules)합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-308">For more information, see [Disabling IIS modules](xref:host-and-deploy/iis/modules#disabling-iis-modules).</span></span>

#### <a name="unsupported-features"></a><span data-ttu-id="74794-309">지원 되지 않는 기능</span><span class="sxs-lookup"><span data-stu-id="74794-309">Unsupported features</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="74794-310">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="74794-310">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="74794-311">출시 미들웨어 2.x ASP.NET 코어는 다음과 같은 IIS URL 재작성 모듈 기능을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-311">The middleware released with ASP.NET Core 2.x doesn't support the following IIS URL Rewrite Module features:</span></span>
* <span data-ttu-id="74794-312">아웃 바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="74794-312">Outbound Rules</span></span>
* <span data-ttu-id="74794-313">사용자 지정 서버 변수</span><span class="sxs-lookup"><span data-stu-id="74794-313">Custom Server Variables</span></span>
* <span data-ttu-id="74794-314">와일드카드</span><span class="sxs-lookup"><span data-stu-id="74794-314">Wildcards</span></span>
* <span data-ttu-id="74794-315">LogRewrittenUrl</span><span class="sxs-lookup"><span data-stu-id="74794-315">LogRewrittenUrl</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="74794-316">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="74794-316">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="74794-317">출시 미들웨어 1.x ASP.NET 코어는 다음과 같은 IIS URL 재작성 모듈 기능을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-317">The middleware released with ASP.NET Core 1.x doesn't support the following IIS URL Rewrite Module features:</span></span>
* <span data-ttu-id="74794-318">전역 규칙</span><span class="sxs-lookup"><span data-stu-id="74794-318">Global Rules</span></span>
* <span data-ttu-id="74794-319">아웃 바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="74794-319">Outbound Rules</span></span>
* <span data-ttu-id="74794-320">지도 다시 작성</span><span class="sxs-lookup"><span data-stu-id="74794-320">Rewrite Maps</span></span>
* <span data-ttu-id="74794-321">CustomResponse 동작</span><span class="sxs-lookup"><span data-stu-id="74794-321">CustomResponse Action</span></span>
* <span data-ttu-id="74794-322">사용자 지정 서버 변수</span><span class="sxs-lookup"><span data-stu-id="74794-322">Custom Server Variables</span></span>
* <span data-ttu-id="74794-323">와일드카드</span><span class="sxs-lookup"><span data-stu-id="74794-323">Wildcards</span></span>
* <span data-ttu-id="74794-324">Action:CustomResponse</span><span class="sxs-lookup"><span data-stu-id="74794-324">Action:CustomResponse</span></span>
* <span data-ttu-id="74794-325">LogRewrittenUrl</span><span class="sxs-lookup"><span data-stu-id="74794-325">LogRewrittenUrl</span></span>

---

#### <a name="supported-server-variables"></a><span data-ttu-id="74794-326">지원 되는 서버 변수</span><span class="sxs-lookup"><span data-stu-id="74794-326">Supported server variables</span></span>
<span data-ttu-id="74794-327">미들웨어는 다음 IIS URL 재작성 모듈 서버 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-327">The middleware supports the following IIS URL Rewrite Module server variables:</span></span>
* <span data-ttu-id="74794-328">CONTENT_LENGTH</span><span class="sxs-lookup"><span data-stu-id="74794-328">CONTENT_LENGTH</span></span>
* <span data-ttu-id="74794-329">CONTENT_TYPE</span><span class="sxs-lookup"><span data-stu-id="74794-329">CONTENT_TYPE</span></span>
* <span data-ttu-id="74794-330">HTTP_ACCEPT</span><span class="sxs-lookup"><span data-stu-id="74794-330">HTTP_ACCEPT</span></span>
* <span data-ttu-id="74794-331">HTTP_CONNECTION</span><span class="sxs-lookup"><span data-stu-id="74794-331">HTTP_CONNECTION</span></span>
* <span data-ttu-id="74794-332">HTTP_COOKIE</span><span class="sxs-lookup"><span data-stu-id="74794-332">HTTP_COOKIE</span></span>
* <span data-ttu-id="74794-333">HTTP_HOST</span><span class="sxs-lookup"><span data-stu-id="74794-333">HTTP_HOST</span></span>
* <span data-ttu-id="74794-334">HTTP_REFERER</span><span class="sxs-lookup"><span data-stu-id="74794-334">HTTP_REFERER</span></span>
* <span data-ttu-id="74794-335">HTTP_URL</span><span class="sxs-lookup"><span data-stu-id="74794-335">HTTP_URL</span></span>
* <span data-ttu-id="74794-336">HTTP_USER_AGENT</span><span class="sxs-lookup"><span data-stu-id="74794-336">HTTP_USER_AGENT</span></span>
* <span data-ttu-id="74794-337">HTTPS</span><span class="sxs-lookup"><span data-stu-id="74794-337">HTTPS</span></span>
* <span data-ttu-id="74794-338">LOCAL_ADDR</span><span class="sxs-lookup"><span data-stu-id="74794-338">LOCAL_ADDR</span></span>
* <span data-ttu-id="74794-339">QUERY_STRING</span><span class="sxs-lookup"><span data-stu-id="74794-339">QUERY_STRING</span></span>
* <span data-ttu-id="74794-340">REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="74794-340">REMOTE_ADDR</span></span>
* <span data-ttu-id="74794-341">REMOTE_PORT</span><span class="sxs-lookup"><span data-stu-id="74794-341">REMOTE_PORT</span></span>
* <span data-ttu-id="74794-342">REQUEST_FILENAME</span><span class="sxs-lookup"><span data-stu-id="74794-342">REQUEST_FILENAME</span></span>
* <span data-ttu-id="74794-343">REQUEST_URI</span><span class="sxs-lookup"><span data-stu-id="74794-343">REQUEST_URI</span></span>

> [!NOTE]
> <span data-ttu-id="74794-344">가져올 수도 있습니다는 `IFileProvider` 통해는 `PhysicalFileProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-344">You can also obtain an `IFileProvider` via a `PhysicalFileProvider`.</span></span> <span data-ttu-id="74794-345">이 방법은 규칙 파일 프로그램 재작성의 위치에 대 한 유연성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-345">This approach may provide greater flexibility for the location of your rewrite rules files.</span></span> <span data-ttu-id="74794-346">다시 쓰기 규칙 파일 제공 된 경로에서 서버에 배포 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-346">Make sure that your rewrite rules files are deployed to the server at the path you provide.</span></span>
> ```csharp
> PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
> ```

### <a name="method-based-rule"></a><span data-ttu-id="74794-347">메서드 기반 규칙</span><span class="sxs-lookup"><span data-stu-id="74794-347">Method-based rule</span></span>
<span data-ttu-id="74794-348">사용 하 여 `Add(Action<RewriteContext> applyRule)` 메서드에서 사용자 고유의 규칙 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-348">Use `Add(Action<RewriteContext> applyRule)` to implement your own rule logic in a method.</span></span> <span data-ttu-id="74794-349">`RewriteContext` 노출는 `HttpContext` 메서드에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-349">The `RewriteContext` exposes the `HttpContext` for use in your method.</span></span> <span data-ttu-id="74794-350">`context.Result` 확인 방법을 추가 파이프라인 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74794-350">The `context.Result` determines how additional pipeline processing is handled.</span></span>

| <span data-ttu-id="74794-351">context.Result</span><span class="sxs-lookup"><span data-stu-id="74794-351">context.Result</span></span>                       | <span data-ttu-id="74794-352">작업</span><span class="sxs-lookup"><span data-stu-id="74794-352">Action</span></span>                                                          |
| ------------------------------------ | --------------------------------------------------------------- |
| <span data-ttu-id="74794-353">`RuleResult.ContinueRules`(기본값)</span><span class="sxs-lookup"><span data-stu-id="74794-353">`RuleResult.ContinueRules` (default)</span></span> | <span data-ttu-id="74794-354">계속 규칙 적용</span><span class="sxs-lookup"><span data-stu-id="74794-354">Continue applying rules</span></span>                                         |
| `RuleResult.EndResponse`             | <span data-ttu-id="74794-355">규칙 적용을 중지 하 고 응답 보내기</span><span class="sxs-lookup"><span data-stu-id="74794-355">Stop applying rules and send the response</span></span>                       |
| `RuleResult.SkipRemainingRules`      | <span data-ttu-id="74794-356">규칙 적용을 중지 하 고 미들웨어 컨텍스트 보내기</span><span class="sxs-lookup"><span data-stu-id="74794-356">Stop applying rules and send the context to the next middleware</span></span> |

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="74794-357">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="74794-357">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=9)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="74794-358">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="74794-358">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=6)]

---

<span data-ttu-id="74794-359">샘플 응용 프로그램으로 끝나는 경로 대 한 요청을 리디렉션하는 방법을 보여 줍니다. *.xml*합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-359">The sample app demonstrates a method that redirects requests for paths that end with *.xml*.</span></span> <span data-ttu-id="74794-360">에 대 한 요청을 수행 하는 경우 `/file.xml`로 리디렉션되도록 `/xmlfiles/file.xml`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-360">If you make a request for `/file.xml`, it's redirected to `/xmlfiles/file.xml`.</span></span> <span data-ttu-id="74794-361">상태 코드 301 (영구적 이동)로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74794-361">The status code is set to 301 (Moved Permanently).</span></span> <span data-ttu-id="74794-362">리디렉션에 대 한 명시적으로 설정 해야 응답;의 상태 코드 그렇지 않은 경우 200 (OK) 상태 코드가 반환 되 고 클라이언트에 리디렉션도 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74794-362">For a redirect, you must explicitly set the status code of the response; otherwise, a 200 (OK) status code is returned and the redirect won't occur on the client.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="74794-363">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="74794-363">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/RewriteRules.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="74794-364">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="74794-364">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet2)]

---

<span data-ttu-id="74794-365">원래 요청:`/file.xml`</span><span class="sxs-lookup"><span data-stu-id="74794-365">Original Request: `/file.xml`</span></span>

![브라우저 창을 요청 및 file.xml에 대 한 응답을 추적 하는 개발자 도구](url-rewriting/_static/add_redirect_xml_requests.png)

### <a name="irule-based-rule"></a><span data-ttu-id="74794-367">IRule 기반 규칙</span><span class="sxs-lookup"><span data-stu-id="74794-367">IRule-based rule</span></span>
<span data-ttu-id="74794-368">사용 하 여 `Add(IRule)` 에서 파생 된 클래스에서 사용자 고유의 규칙 논리를 구현 하려면 `IRule`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-368">Use `Add(IRule)` to implement your own rule logic in a class that derives from `IRule`.</span></span> <span data-ttu-id="74794-369">사용 하는 `IRule` 규칙 메서드 기반 방식을 사용 하 여 보다 큰 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-369">Using an `IRule` provides greater flexibility over using the method-based rule approach.</span></span> <span data-ttu-id="74794-370">파생 된 클래스에 대 한 매개 변수에서 전달 될 수 있는 생성자를 포함 될 수 있습니다는 `ApplyRule` 메서드.</span><span class="sxs-lookup"><span data-stu-id="74794-370">Your derived class may include a constructor, where you can pass in parameters for the `ApplyRule` method.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="74794-371">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="74794-371">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=10-11)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="74794-372">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="74794-372">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=7-8)]

---

<span data-ttu-id="74794-373">샘플 응용 프로그램에 대 한 매개 변수 값의 `extension` 및 `newPath` 여러 조건을 모두 충족 하도록 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-373">The values of the parameters in the sample app for the `extension` and the `newPath` are checked to meet several conditions.</span></span> <span data-ttu-id="74794-374">`extension` 값을 포함 해야 하며 값 이어야 합니다 *.png*, *.jpg*, 또는 *.gif*합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-374">The `extension` must contain a value, and the value must be *.png*, *.jpg*, or *.gif*.</span></span> <span data-ttu-id="74794-375">경우는 `newPath` 유효 하지는 `ArgumentException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74794-375">If the `newPath` isn't valid, an `ArgumentException` is thrown.</span></span> <span data-ttu-id="74794-376">에 대 한 요청을 수행 하는 경우 *image.png*로 리디렉션되도록 `/png-images/image.png`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-376">If you make a request for *image.png*, it's redirected to `/png-images/image.png`.</span></span> <span data-ttu-id="74794-377">에 대 한 요청을 수행 하는 경우 *image.jpg*로 리디렉션되도록 `/jpg-images/image.jpg`합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-377">If you make a request for *image.jpg*, it's redirected to `/jpg-images/image.jpg`.</span></span> <span data-ttu-id="74794-378">상태 코드가 301 (영구적 이동)을으로 설정 되어 및 `context.Result` 처리 규칙을 중지 하 고 응답을 보내기로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74794-378">The status code is set to 301 (Moved Permanently), and the `context.Result` is set to stop processing rules and send the response.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="74794-379">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="74794-379">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/RewriteRules.cs?name=snippet2)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="74794-380">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="74794-380">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/RewriteRule.cs?name=snippet1)]

---

<span data-ttu-id="74794-381">원래 요청:`/image.png`</span><span class="sxs-lookup"><span data-stu-id="74794-381">Original Request: `/image.png`</span></span>

![브라우저 창을 요청 및 image.png에 대 한 응답을 추적 하는 개발자 도구](url-rewriting/_static/add_redirect_png_requests.png)

<span data-ttu-id="74794-383">원래 요청:`/image.jpg`</span><span class="sxs-lookup"><span data-stu-id="74794-383">Original Request: `/image.jpg`</span></span>

![브라우저 창을 요청 및 image.jpg에 대 한 응답을 추적 하는 개발자 도구](url-rewriting/_static/add_redirect_jpg_requests.png)

## <a name="regex-examples"></a><span data-ttu-id="74794-385">정규식 예제</span><span class="sxs-lookup"><span data-stu-id="74794-385">Regex examples</span></span>

| <span data-ttu-id="74794-386">Goal</span><span class="sxs-lookup"><span data-stu-id="74794-386">Goal</span></span> | <span data-ttu-id="74794-387">Regex 문자열 &</span><span class="sxs-lookup"><span data-stu-id="74794-387">Regex String &</span></span><br><span data-ttu-id="74794-388">일치 예</span><span class="sxs-lookup"><span data-stu-id="74794-388">Match Example</span></span> | <span data-ttu-id="74794-389">대체 문자열 &</span><span class="sxs-lookup"><span data-stu-id="74794-389">Replacement String &</span></span><br><span data-ttu-id="74794-390">출력 예</span><span class="sxs-lookup"><span data-stu-id="74794-390">Output Example</span></span> |
| ---- | :-----------------------------: | :------------------------------------: |
| <span data-ttu-id="74794-391">쿼리 문자열에 경로 다시 작성</span><span class="sxs-lookup"><span data-stu-id="74794-391">Rewrite path into querystring</span></span> | `^path/(.*)/(.*)`<br>`/path/abc/123` | `path?var1=$1&var2=$2`<br>`/path?var1=abc&var2=123` |
| <span data-ttu-id="74794-392">후행 슬래시를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-392">Strip trailing slash</span></span> | `(.*)/$`<br>`/path/` | `$1`<br>`/path` |
| <span data-ttu-id="74794-393">후행 슬래시를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-393">Enforce trailing slash</span></span> | `(.*[^/])$`<br>`/path` | `$1/`<br>`/path/` |
| <span data-ttu-id="74794-394">특정 요청을 다시 작성 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="74794-394">Avoid rewriting specific requests</span></span> | <span data-ttu-id="74794-395">`^(.*)(?<!\.axd)$` 또는 `^(?!.*\.axd$)(.*)$`</span><span class="sxs-lookup"><span data-stu-id="74794-395">`^(.*)(?<!\.axd)$` or `^(?!.*\.axd$)(.*)$`</span></span><br><span data-ttu-id="74794-396">예:`/resource.htm`</span><span class="sxs-lookup"><span data-stu-id="74794-396">Yes: `/resource.htm`</span></span><br><span data-ttu-id="74794-397">아니요:`/resource.axd`</span><span class="sxs-lookup"><span data-stu-id="74794-397">No: `/resource.axd`</span></span> | `rewritten/$1`<br>`/rewritten/resource.htm`<br>`/resource.axd` |
| <span data-ttu-id="74794-398">URL 세그먼트를 다시 정렬</span><span class="sxs-lookup"><span data-stu-id="74794-398">Rearrange URL segments</span></span> | `path/(.*)/(.*)/(.*)`<br>`path/1/2/3` | `path/$3/$2/$1`<br>`path/3/2/1` |
| <span data-ttu-id="74794-399">URL 세그먼트를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-399">Replace a URL segment</span></span> | `^(.*)/segment2/(.*)`<br>`/segment1/segment2/segment3` | `$1/replaced/$2`<br>`/segment1/replaced/segment3` |

## <a name="additional-resources"></a><span data-ttu-id="74794-400">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="74794-400">Additional resources</span></span>
* [<span data-ttu-id="74794-401">응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="74794-401">Application Startup</span></span>](startup.md)
* [<span data-ttu-id="74794-402">미들웨어</span><span class="sxs-lookup"><span data-stu-id="74794-402">Middleware</span></span>](middleware.md)
* [<span data-ttu-id="74794-403">.NET에서의 정규식</span><span class="sxs-lookup"><span data-stu-id="74794-403">Regular expressions in .NET</span></span>](/dotnet/articles/standard/base-types/regular-expressions)
* [<span data-ttu-id="74794-404">정규식 언어 - 빠른 참조</span><span class="sxs-lookup"><span data-stu-id="74794-404">Regular expression language - quick reference</span></span>](/dotnet/articles/standard/base-types/quick-ref)
* [<span data-ttu-id="74794-405">Apache mod_rewrite</span><span class="sxs-lookup"><span data-stu-id="74794-405">Apache mod_rewrite</span></span>](https://httpd.apache.org/docs/2.4/rewrite/)
* [<span data-ttu-id="74794-406">(IIS) 용 Url 재작성 모듈 2.0을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="74794-406">Using Url Rewrite Module 2.0 (for IIS)</span></span>](https://docs.microsoft.com/iis/extensions/url-rewrite-module/using-url-rewrite-module-20)
* [<span data-ttu-id="74794-407">URL 재작성 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="74794-407">URL Rewrite Module Configuration Reference</span></span>](https://docs.microsoft.com/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference)
* [<span data-ttu-id="74794-408">IIS URL 재작성 모듈 포럼</span><span class="sxs-lookup"><span data-stu-id="74794-408">IIS URL Rewrite Module Forum</span></span>](https://forums.iis.net/1152.aspx)
* [<span data-ttu-id="74794-409">간단한 URL 구조를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="74794-409">Keep a simple URL structure</span></span>](https://support.google.com/webmasters/answer/76329?hl=en)
* [<span data-ttu-id="74794-410">팁과 트릭 10 URL 다시 쓰기</span><span class="sxs-lookup"><span data-stu-id="74794-410">10 URL Rewriting Tips and Tricks</span></span>](http://ruslany.net/2009/04/10-url-rewriting-tips-and-tricks/)
* [<span data-ttu-id="74794-411">슬래시 또는 슬래시</span><span class="sxs-lookup"><span data-stu-id="74794-411">To slash or not to slash</span></span>](https://webmasters.googleblog.com/2010/04/to-slash-or-not-to-slash.html)
