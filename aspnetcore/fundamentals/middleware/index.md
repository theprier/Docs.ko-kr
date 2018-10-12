---
title: ASP.NET Core 미들웨어 기본 사항
author: rick-anderson
description: ASP.NET Core 미들웨어 및 요청 파이프라인에 대해 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 08/21/2018
uid: fundamentals/middleware/index
ms.openlocfilehash: 84e79df7fcf5790e658a20c80f21d73cdc76c054
ms.sourcegitcommit: 8bf4dff3069e62972c1b0839a93fb444e502afe7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2018
ms.locfileid: "46483011"
---
# <a name="aspnet-core-middleware"></a><span data-ttu-id="af801-103">ASP.NET Core 미들웨어</span><span class="sxs-lookup"><span data-stu-id="af801-103">ASP.NET Core Middleware</span></span>

<span data-ttu-id="af801-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="af801-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="af801-105">미들웨어는 요청 및 응답을 처리하는 앱 파이프라인으로 어셈블리되는 소프트웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="af801-105">Middleware is software that's assembled into an app pipeline to handle requests and responses.</span></span> <span data-ttu-id="af801-106">각 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="af801-106">Each component:</span></span>

* <span data-ttu-id="af801-107">요청을 파이프라인의 다음 구성 요소로 전달할지 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-107">Chooses whether to pass the request to the next component in the pipeline.</span></span>
* <span data-ttu-id="af801-108">파이프라인의 다음 구성 요소가 호출되기 전과 후에 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-108">Can perform work before and after the next component in the pipeline is invoked.</span></span>

<span data-ttu-id="af801-109">요청 대리자는 요청 파이프라인을 빌드하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-109">Request delegates are used to build the request pipeline.</span></span> <span data-ttu-id="af801-110">요청 대리자는 각 HTTP 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-110">The request delegates handle each HTTP request.</span></span>

<span data-ttu-id="af801-111">요청 대리자는 <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*>, <xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> 및 <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> 확장 메서드를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-111">Request delegates are configured using <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*>, <xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*>, and <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> extension methods.</span></span> <span data-ttu-id="af801-112">개별 요청 대리자는 무명 메서드(인라인 미들웨어라고 함)로 인라인에서 지정되거나 다시 사용할 수 있는 클래스에서 정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-112">An individual request delegate can be specified in-line as an anonymous method (called in-line middleware), or it can be defined in a reusable class.</span></span> <span data-ttu-id="af801-113">이러한 다시 사용할 수 있는 클래스 및 인라인 무명 메서드는 *미들웨어*이며, *미들웨어 구성 요소*라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-113">These reusable classes and in-line anonymous methods are *middleware*, also called *middleware components*.</span></span> <span data-ttu-id="af801-114">요청 파이프라인의 각 미들웨어 구성 요소는 파이프라인의 그 다음 구성 요소를 호출하거나 파이프라인을 단락(short-circuiting)하는 역할을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-114">Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline or short-circuiting the pipeline.</span></span>

<span data-ttu-id="af801-115"><xref:migration/http-modules>은 ASP.NET Core와 ASP.NET 4.x의 요청 파이프라인 간의 차이점을 설명하고 더 많은 미들웨어 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-115"><xref:migration/http-modules> explains the difference between request pipelines in ASP.NET Core and ASP.NET 4.x and provides more middleware samples.</span></span>

## <a name="create-a-middleware-pipeline-with-iapplicationbuilder"></a><span data-ttu-id="af801-116">IApplicationBuilder로 미들웨어 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="af801-116">Create a middleware pipeline with IApplicationBuilder</span></span>

<span data-ttu-id="af801-117">ASP.NET Core 요청 파이프라인은 하나씩 차례로 호출되는 요청 대리자 시퀀스로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-117">The ASP.NET Core request pipeline consists of a sequence of request delegates, called one after the other.</span></span> <span data-ttu-id="af801-118">다음 다이어그램은 개념을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="af801-118">The following diagram demonstrates the concept.</span></span> <span data-ttu-id="af801-119">실행 스레드는 검은색 화살표를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="af801-119">The thread of execution follows the black arrows.</span></span>

![요청이 도착하고, 세 가지 미들웨어를 처리하고, 응답이 앱에서 나가는 것을 보여주는 요청 처리 패턴입니다.](index/_static/request-delegate-pipeline.png)

<span data-ttu-id="af801-123">각 대리자는 다음 대리자 전과 후에 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-123">Each delegate can perform operations before and after the next delegate.</span></span> <span data-ttu-id="af801-124">또한 대리자는 다음 대리자에 요청을 전달하지 않도록 결정할 수 있습니다. 이를 *요청 파이프라인을 단락(short-circuiting)* 한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-124">A delegate can also decide to not pass a request to the next delegate, which is called *short-circuiting the request pipeline*.</span></span> <span data-ttu-id="af801-125">단락(short-circuiting)은 불필요한 작업을 방지하기 때문에 보통 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-125">Short-circuiting is often desirable because it avoids unnecessary work.</span></span> <span data-ttu-id="af801-126">예를 들어 정적 파일 미들웨어는 정적 파일에 대한 요청을 반환하고 나머지 파이프라인을 단락(short-circuit)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-126">For example, Static Files Middleware can return a request for a static file and short-circuit the rest of the pipeline.</span></span> <span data-ttu-id="af801-127">예외 처리 대리자는 파이프라인의 이후 단계에서 발생하는 예외를 catch할 수 있도록 파이프라인의 초기에 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-127">Exception-handling delegates are called early in the pipeline, so they can catch exceptions that occur in later stages of the pipeline.</span></span>

<span data-ttu-id="af801-128">가장 간단한 가능한 ASP.NET Core 앱은 모든 요청을 처리하는 단일 요청 대리자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-128">The simplest possible ASP.NET Core app sets up a single request delegate that handles all requests.</span></span> <span data-ttu-id="af801-129">이 경우 실제 요청 파이프라인은 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-129">This case doesn't include an actual request pipeline.</span></span> <span data-ttu-id="af801-130">대신, 단일 익명 함수가 모든 HTTP 요청에 대한 응답에 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-130">Instead, a single anonymous function is called in response to every HTTP request.</span></span>

[!code-csharp[](index/snapshot/Middleware/Startup.cs?name=snippet1)]

<span data-ttu-id="af801-131">첫 번째 <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*> 대리자는 파이프라인을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-131">The first <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*> delegate terminates the pipeline.</span></span>

<span data-ttu-id="af801-132"><xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*>를 사용하여 여러 요청 대리자를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-132">Chain multiple request delegates together with <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*>.</span></span> <span data-ttu-id="af801-133">`next` 매개 변수는 파이프라인의 다음 대리자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="af801-133">The `next` parameter represents the next delegate in the pipeline.</span></span> <span data-ttu-id="af801-134">*next* 매개 변수를 호출하지 *않고* 파이프라인을 단락(short-circuit)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-134">You can short-circuit the pipeline by *not* calling the *next* parameter.</span></span> <span data-ttu-id="af801-135">다음 예제의 설명처럼, 일반적으로 다음 대리자 전과 후 모두에서 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-135">You can typically perform actions both before and after the next delegate, as the following example demonstrates:</span></span>

[!code-csharp[](index/snapshot/Chain/Startup.cs?name=snippet1)]

> [!WARNING]
> <span data-ttu-id="af801-136">클라이언트에 응답을 전송한 후에 `next.Invoke`를 호출하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="af801-136">Don't call `next.Invoke` after the response has been sent to the client.</span></span> <span data-ttu-id="af801-137">응답이 시작된 후 <xref:Microsoft.AspNetCore.Http.HttpResponse>로 변경하면 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-137">Changes to <xref:Microsoft.AspNetCore.Http.HttpResponse> after the response has started throw an exception.</span></span> <span data-ttu-id="af801-138">예를 들어 헤더 및 상태 코드를 설정하는 변경 작업은 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-138">For example, changes such as setting headers and a status code throw an exception.</span></span> <span data-ttu-id="af801-139">`next`를 호출한 후 응답 본문에 작성하기:</span><span class="sxs-lookup"><span data-stu-id="af801-139">Writing to the response body after calling `next`:</span></span>
>
> * <span data-ttu-id="af801-140">프로토콜 위반이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-140">May cause a protocol violation.</span></span> <span data-ttu-id="af801-141">예를 들어, 명시된 `Content-Length`보다 긴 내용이 작성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-141">For example, writing more than the stated `Content-Length`.</span></span>
> * <span data-ttu-id="af801-142">본문 형식을 손상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-142">May corrupt the body format.</span></span> <span data-ttu-id="af801-143">예를 들어 CSS 파일에 HTML 바닥글 작성하기.</span><span class="sxs-lookup"><span data-stu-id="af801-143">For example, writing an HTML footer to a CSS file.</span></span>
>
> <span data-ttu-id="af801-144"><xref:Microsoft.AspNetCore.Http.HttpResponse.HasStarted*>는 헤더가 이미 전송됐는지 또는 본문이 이미 작성됐는지 여부를 나타내는 유용한 힌트를 제공해줍니다.</span><span class="sxs-lookup"><span data-stu-id="af801-144"><xref:Microsoft.AspNetCore.Http.HttpResponse.HasStarted*> is a useful hint to indicate if headers have been sent or the body has been written to.</span></span>

## <a name="order"></a><span data-ttu-id="af801-145">순서</span><span class="sxs-lookup"><span data-stu-id="af801-145">Order</span></span>

<span data-ttu-id="af801-146">미들웨어 구성 요소가 `Startup.Configure` 메서드에 추가되는 순서는 요청에서 미들웨어 구성 요소가 호출되는 순서와 응답에 대한 역순서를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-146">The order that middleware components are added in the `Startup.Configure` method defines the order in which the middleware components are invoked on requests and the reverse order for the response.</span></span> <span data-ttu-id="af801-147">순서는 보안, 성능 및 기능에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-147">The order is critical for security, performance, and functionality.</span></span>

<span data-ttu-id="af801-148">다음 `Startup.Configure` 메서드는 공통 앱 시나리오를 위한 미들웨어 구성 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-148">The following `Startup.Configure` method adds middleware components for common app scenarios:</span></span>

::: moniker range=">= aspnetcore-2.0"

1. <span data-ttu-id="af801-149">예외/오류 처리</span><span class="sxs-lookup"><span data-stu-id="af801-149">Exception/error handling</span></span>
1. <span data-ttu-id="af801-150">HTTP 엄격한 전송 보안 프로토콜</span><span class="sxs-lookup"><span data-stu-id="af801-150">HTTP Strict Transport Security Protocol</span></span>
1. <span data-ttu-id="af801-151">HTTPS 리디렉션</span><span class="sxs-lookup"><span data-stu-id="af801-151">HTTPS redirection</span></span>
1. <span data-ttu-id="af801-152">정적 파일 서버</span><span class="sxs-lookup"><span data-stu-id="af801-152">Static file server</span></span>
1. <span data-ttu-id="af801-153">쿠키 정책 적용</span><span class="sxs-lookup"><span data-stu-id="af801-153">Cookie policy enforcement</span></span>
1. <span data-ttu-id="af801-154">인증</span><span class="sxs-lookup"><span data-stu-id="af801-154">Authentication</span></span>
1. <span data-ttu-id="af801-155">세션</span><span class="sxs-lookup"><span data-stu-id="af801-155">Session</span></span>
1. <span data-ttu-id="af801-156">MVC</span><span class="sxs-lookup"><span data-stu-id="af801-156">MVC</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    if (env.IsDevelopment())
    {
        // When the app runs in the Development environment:
        //   Use the Developer Exception Page to report app runtime errors.
        //   Use the Database Error Page to report database runtime errors.
        app.UseDeveloperExceptionPage();
        app.UseDatabaseErrorPage();
    }
    else
    {
        // When the app doesn't run in the Development environment:
        //   Enable the Exception Handler Middleware to catch exceptions
        //     thrown in the following middlewares.
        //   Use the HTTP Strict Transport Security Protocol (HSTS)
        //     Middleware.
        app.UseExceptionHandler("/Error");
        app.UseHsts();
    }

    // Use HTTPS Redirection Middleware to redirect HTTP requests to HTTPS.
    app.UseHttpsRedirection();

    // Return static files and end the pipeline.
    app.UseStaticFiles();

    // Use Cookie Policy Middleware to conform to EU General Data 
    // Protection Regulation (GDPR) regulations.
    app.UseCookiePolicy();

    // Authenticate before the user accesses secure resources.
    app.UseAuthentication();

    // If the app uses session state, call Session Middleware after Cookie 
    // Policy Middleware and before MVC Middleware.
    app.UseSession();

    // Add MVC to the request pipeline.
    app.UseMvc();
}
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

1. <span data-ttu-id="af801-157">예외/오류 처리</span><span class="sxs-lookup"><span data-stu-id="af801-157">Exception/error handling</span></span>
1. <span data-ttu-id="af801-158">정적 파일</span><span class="sxs-lookup"><span data-stu-id="af801-158">Static files</span></span>
1. <span data-ttu-id="af801-159">인증</span><span class="sxs-lookup"><span data-stu-id="af801-159">Authentication</span></span>
1. <span data-ttu-id="af801-160">세션</span><span class="sxs-lookup"><span data-stu-id="af801-160">Session</span></span>
1. <span data-ttu-id="af801-161">MVC</span><span class="sxs-lookup"><span data-stu-id="af801-161">MVC</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    // Enable the Exception Handler Middleware to catch exceptions
    //   thrown in the following middlewares.
    app.UseExceptionHandler("/Home/Error");

    // Return static files and end the pipeline.
    app.UseStaticFiles();

    // Authenticate before you access secure resources.
    app.UseIdentity();

    // If the app uses session state, call UseSession before 
    // MVC Middleware.
    app.UseSession();

    // Add MVC to the request pipeline.
    app.UseMvcWithDefaultRoute();
}
```

::: moniker-end

<span data-ttu-id="af801-162">앞의 예제 코드에서 각 미들웨어 확장 메서드는 <xref:Microsoft.AspNetCore.Builder?displayProperty=fullName> 네임스페이스를 통해 <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder>에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-162">In the preceding example code, each middleware extension method is exposed on <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> through the <xref:Microsoft.AspNetCore.Builder?displayProperty=fullName> namespace.</span></span>

<span data-ttu-id="af801-163"><xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*>는 파이프라인에 처음으로 추가된 미들웨어 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="af801-163"><xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> is the first middleware component added to the pipeline.</span></span> <span data-ttu-id="af801-164">따라서 예외 처리기 미들웨어는 후속 호출에서 발생하는 모든 예외를 catch 합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-164">Therefore, the Exception Handler Middleware catches any exceptions that occur in later calls.</span></span>

<span data-ttu-id="af801-165">정적 파일 미들웨어는 파이프라인 초기에 호출되므로 요청을 처리하고 나머지 구성 요소를 통과하지 않고 단락(short-circuit)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-165">Static Files Middleware is called early in the pipeline so that it can handle requests and short-circuit without going through the remaining components.</span></span> <span data-ttu-id="af801-166">정적 파일 미들웨어는 권한 부여 검사를 제공하지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="af801-166">The Static Files Middleware provides **no** authorization checks.</span></span> <span data-ttu-id="af801-167">*wwwroot* 아래의 항목을 비롯한 제공되는 모든 파일은 공개적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-167">Any files served by it, including those under *wwwroot*, are publicly available.</span></span> <span data-ttu-id="af801-168">정적 파일을 보호하는 방법은 <xref:fundamentals/static-files>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af801-168">For an approach to secure static files, see <xref:fundamentals/static-files>.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="af801-169">요청이 정적 파일 미들웨어에서 처리되지 않는 경우 인증을 수행하는 인증 미들웨어(<xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*>)로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-169">If the request isn't handled by the Static Files Middleware, it's passed on to the Authentication Middleware (<xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*>), which performs authentication.</span></span> <span data-ttu-id="af801-170">인증은 인증되지 않은 요청을 단락(short-circuit)하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-170">Authentication doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="af801-171">인증 미들웨어가 요청을 인증하지만, MVC가 특정 Razor Page 또는 컨트롤러 및 작업을 선택한 후에만 권한 부여(및 거부)가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-171">Although Authentication Middleware authenticates requests, authorization (and rejection) occurs only after MVC selects a specific Razor Page or MVC controller and action.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="af801-172">요청이 정적 파일 미들웨어에서 처리되지 않는 경우 인증을 수행하는 ID 미들웨어(<xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*>)로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-172">If the request isn't handled by Static Files Middleware, it's passed on to the Identity Middleware (<xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*>), which performs authentication.</span></span> <span data-ttu-id="af801-173">ID는 인증되지 않은 요청을 단락(short-circuit)하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-173">Identity doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="af801-174">ID가 요청을 인증하지만 MVC가 특정 컨트롤러 및 작업을 선택한 후에만 권한 부여(및 거부)가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-174">Although Identity authenticates requests, authorization (and rejection) occurs only after MVC selects a specific controller and action.</span></span>

::: moniker-end

<span data-ttu-id="af801-175">다음 예제는 정적 파일에 대한 요청이 응답 압축 미들웨어 전에 정적 파일 미들웨어에서 처리되는 미들웨어 순서를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-175">The following example demonstrates a middleware order where requests for static files are handled by Static Files Middleware before Response Compression Middleware.</span></span> <span data-ttu-id="af801-176">정적 파일은 이 미들웨어 순서를 사용하여 압축되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-176">Static files aren't compressed with this middleware order.</span></span> <span data-ttu-id="af801-177"><xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*>의 MVC 응답은 압축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-177">The MVC responses from <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> can be compressed.</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    // Static files not compressed by Static Files Middleware.
    app.UseStaticFiles();
    app.UseResponseCompression();
    app.UseMvcWithDefaultRoute();
}
```

### <a name="use-run-and-map"></a><span data-ttu-id="af801-178">Use, Run 및 Map</span><span class="sxs-lookup"><span data-stu-id="af801-178">Use, Run, and Map</span></span>

<span data-ttu-id="af801-179">`Use`, `Run` 및 `Map`을 사용하여 HTTP 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-179">Configure the HTTP pipeline using `Use`, `Run`, and `Map`.</span></span> <span data-ttu-id="af801-180">`Use` 메서드는 파이프라인을 단락(short-circuit)할 수 있습니다(즉, `next` 요청 대리자를 호출하지 않는 경우).</span><span class="sxs-lookup"><span data-stu-id="af801-180">The `Use` method can short-circuit the pipeline (that is, if it doesn't call a `next` request delegate).</span></span> <span data-ttu-id="af801-181">`Run`은 규칙이며 일부 미들웨어 구성 요소는 파이프라인의 끝에서 실행되는 `Run[Middleware]` 메서드를 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-181">`Run` is a convention, and some middleware components may expose `Run[Middleware]` methods that run at the end of the pipeline.</span></span>

<span data-ttu-id="af801-182"><xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> 확장은 파이프라인 분기에 규칙으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-182"><xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> extensions are used as a convention for branching the pipeline.</span></span> <span data-ttu-id="af801-183">`Map*`은 지정된 요청 경로의 일치를 기반으로 요청 파이프라인을 분기합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-183">`Map*` branches the request pipeline based on matches of the given request path.</span></span> <span data-ttu-id="af801-184">요청 경로가 지정된 경로로 시작하는 경우 분기가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-184">If the request path starts with the given path, the branch is executed.</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMap.cs?name=snippet1)]

<span data-ttu-id="af801-185">다음 표는 앞의 코드를 사용하여 `http://localhost:1234`의 요청 및 응답을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="af801-185">The following table shows the requests and responses from `http://localhost:1234` using the previous code.</span></span>

| <span data-ttu-id="af801-186">요청</span><span class="sxs-lookup"><span data-stu-id="af801-186">Request</span></span>             | <span data-ttu-id="af801-187">응답</span><span class="sxs-lookup"><span data-stu-id="af801-187">Response</span></span>                     |
| ------------------- | ---------------------------- |
| <span data-ttu-id="af801-188">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="af801-188">localhost:1234</span></span>      | <span data-ttu-id="af801-189">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="af801-189">Hello from non-Map delegate.</span></span> |
| <span data-ttu-id="af801-190">localhost:1234/map1</span><span class="sxs-lookup"><span data-stu-id="af801-190">localhost:1234/map1</span></span> | <span data-ttu-id="af801-191">Map Test 1</span><span class="sxs-lookup"><span data-stu-id="af801-191">Map Test 1</span></span>                   |
| <span data-ttu-id="af801-192">localhost:1234/map2</span><span class="sxs-lookup"><span data-stu-id="af801-192">localhost:1234/map2</span></span> | <span data-ttu-id="af801-193">Map Test 2</span><span class="sxs-lookup"><span data-stu-id="af801-193">Map Test 2</span></span>                   |
| <span data-ttu-id="af801-194">localhost:1234/map3</span><span class="sxs-lookup"><span data-stu-id="af801-194">localhost:1234/map3</span></span> | <span data-ttu-id="af801-195">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="af801-195">Hello from non-Map delegate.</span></span> |

<span data-ttu-id="af801-196">`Map`이 사용되는 경우 일치하는 경로 세그먼트는 `HttpRequest.Path`에서 제거되고 각 요청에 대해 `HttpRequest.PathBase`에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-196">When `Map` is used, the matched path segment(s) are removed from `HttpRequest.Path` and appended to `HttpRequest.PathBase` for each request.</span></span>

<span data-ttu-id="af801-197">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions)은 지정된 조건자의 결과를 기반으로 요청 파이프라인을 분기합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-197">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions) branches the request pipeline based on the result of the given predicate.</span></span> <span data-ttu-id="af801-198">`Func<HttpContext, bool>` 형식의 조건자는 파이프라인의 새 분기에 요청을 매핑하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-198">Any predicate of type `Func<HttpContext, bool>` can be used to map requests to a new branch of the pipeline.</span></span> <span data-ttu-id="af801-199">다음 예제에서 조건자는 쿼리 문자열 변수 `branch`의 존재를 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-199">In the following example, a predicate is used to detect the presence of a query string variable `branch`:</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMapWhen.cs?name=snippet1)]

<span data-ttu-id="af801-200">다음 표는 앞의 코드를 사용하여 `http://localhost:1234`의 요청 및 응답을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="af801-200">The following table shows the requests and responses from `http://localhost:1234` using the previous code.</span></span>

| <span data-ttu-id="af801-201">요청</span><span class="sxs-lookup"><span data-stu-id="af801-201">Request</span></span>                       | <span data-ttu-id="af801-202">응답</span><span class="sxs-lookup"><span data-stu-id="af801-202">Response</span></span>                     |
| ----------------------------- | ---------------------------- |
| <span data-ttu-id="af801-203">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="af801-203">localhost:1234</span></span>                | <span data-ttu-id="af801-204">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="af801-204">Hello from non-Map delegate.</span></span> |
| <span data-ttu-id="af801-205">localhost:1234/?branch=master</span><span class="sxs-lookup"><span data-stu-id="af801-205">localhost:1234/?branch=master</span></span> | <span data-ttu-id="af801-206">Branch used = master</span><span class="sxs-lookup"><span data-stu-id="af801-206">Branch used = master</span></span>         |

<span data-ttu-id="af801-207">`Map`은 중첩을 지원합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-207">`Map` supports nesting, for example:</span></span>

```csharp
app.Map("/level1", level1App => {
    level1App.Map("/level2a", level2AApp => {
        // "/level1/level2a" processing
    });
    level1App.Map("/level2b", level2BApp => {
        // "/level1/level2b" processing
    });
});
   ```

<span data-ttu-id="af801-208">`Map`은 여러 세그먼트를 한 번에 일치시킬 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-208">`Map` can also match multiple segments at once:</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMultiSeg.cs?name=snippet1&highlight=13)]

## <a name="built-in-middleware"></a><span data-ttu-id="af801-209">기본 제공 미들웨어</span><span class="sxs-lookup"><span data-stu-id="af801-209">Built-in middleware</span></span>

<span data-ttu-id="af801-210">ASP.NET Core는 다음과 같은 미들웨어 구성 요소가 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-210">ASP.NET Core ships with the following middleware components.</span></span> <span data-ttu-id="af801-211">*순서* 열은 요청 파이프라인에서 미들웨어의 배치, 미들웨어가 요청을 종료하고 다른 미들웨어가 요청을 처리하지 못하게 차단하는 조건에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-211">The *Order* column provides notes on the middleware's placement in the request pipeline and under what conditions the middleware may terminate the request and prevent other middleware from processing a request.</span></span>

| <span data-ttu-id="af801-212">미들웨어</span><span class="sxs-lookup"><span data-stu-id="af801-212">Middleware</span></span> | <span data-ttu-id="af801-213">설명</span><span class="sxs-lookup"><span data-stu-id="af801-213">Description</span></span> | <span data-ttu-id="af801-214">순서</span><span class="sxs-lookup"><span data-stu-id="af801-214">Order</span></span> |
| ---------- | ----------- | ----- |
| [<span data-ttu-id="af801-215">인증</span><span class="sxs-lookup"><span data-stu-id="af801-215">Authentication</span></span>](xref:security/authentication/identity) | <span data-ttu-id="af801-216">인증 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-216">Provides authentication support.</span></span> | <span data-ttu-id="af801-217">`HttpContext.User`가 필요하기 전에.</span><span class="sxs-lookup"><span data-stu-id="af801-217">Before `HttpContext.User` is needed.</span></span> <span data-ttu-id="af801-218">OAuth 콜백에 대한 터미널.</span><span class="sxs-lookup"><span data-stu-id="af801-218">Terminal for OAuth callbacks.</span></span> |
| [<span data-ttu-id="af801-219">쿠키 정책</span><span class="sxs-lookup"><span data-stu-id="af801-219">Cookie Policy</span></span>](xref:security/gdpr) | <span data-ttu-id="af801-220">개인 정보 저장과 관련한 사용자의 동의를 추적하고 쿠키 필드(예: `secure` 및 `SameSite`)에 대해 최소한의 표준을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-220">Tracks consent from users for storing personal information and enforces minimum standards for cookie fields, such as `secure` and `SameSite`.</span></span> | <span data-ttu-id="af801-221">쿠키를 발행하는 미들웨어 전에.</span><span class="sxs-lookup"><span data-stu-id="af801-221">Before middleware that issues cookies.</span></span> <span data-ttu-id="af801-222">예: 인증, 세션, MVC(TempData).</span><span class="sxs-lookup"><span data-stu-id="af801-222">Examples: Authentication, Session, MVC (TempData).</span></span> |
| [<span data-ttu-id="af801-223">CORS</span><span class="sxs-lookup"><span data-stu-id="af801-223">CORS</span></span>](xref:security/cors) | <span data-ttu-id="af801-224">원본 간 리소스 공유를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-224">Configures Cross-Origin Resource Sharing.</span></span> | <span data-ttu-id="af801-225">CORS를 사용하는 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="af801-225">Before components that use CORS.</span></span> |
| [<span data-ttu-id="af801-226">진단</span><span class="sxs-lookup"><span data-stu-id="af801-226">Diagnostics</span></span>](xref:fundamentals/error-handling) | <span data-ttu-id="af801-227">진단을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-227">Configures diagnostics.</span></span> | <span data-ttu-id="af801-228">오류를 생성하는 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="af801-228">Before components that generate errors.</span></span> |
| [<span data-ttu-id="af801-229">전달된 헤더</span><span class="sxs-lookup"><span data-stu-id="af801-229">Forwarded Headers</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions) | <span data-ttu-id="af801-230">프록시된 헤더를 현재 요청에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-230">Forwards proxied headers onto the current request.</span></span> | <span data-ttu-id="af801-231">업데이트된 필드를 사용하는 구성 요소 전에.</span><span class="sxs-lookup"><span data-stu-id="af801-231">Before components that consume the updated fields.</span></span> <span data-ttu-id="af801-232">예: 체계, 호스트, 클라이언트 IP, 메서드.</span><span class="sxs-lookup"><span data-stu-id="af801-232">Examples: scheme, host, client IP, method.</span></span> |
| [<span data-ttu-id="af801-233">HTTP 메서드 재정의</span><span class="sxs-lookup"><span data-stu-id="af801-233">HTTP Method Override</span></span>](/dotnet/api/microsoft.aspnetcore.builder.httpmethodoverrideextensions) | <span data-ttu-id="af801-234">들어오는 POST 요청이 메서드를 재정의하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-234">Allows an incoming POST request to override the method.</span></span> | <span data-ttu-id="af801-235">업데이트된 메서드를 사용하는 구성 요소 앞입니다.</span><span class="sxs-lookup"><span data-stu-id="af801-235">Before components that consume the updated method.</span></span> |
| [<span data-ttu-id="af801-236">HTTPS 리디렉션</span><span class="sxs-lookup"><span data-stu-id="af801-236">HTTPS Redirection</span></span>](xref:security/enforcing-ssl#require-https) | <span data-ttu-id="af801-237">HTTPS로 모든 HTTP 요청을 리디렉션합니다(ASP.NET Core 2.1 이상).</span><span class="sxs-lookup"><span data-stu-id="af801-237">Redirect all HTTP requests to HTTPS (ASP.NET Core 2.1 or later).</span></span> | <span data-ttu-id="af801-238">URL을 사용하는 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="af801-238">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="af801-239">HSTS(HTTP 엄격한 전송 보안)</span><span class="sxs-lookup"><span data-stu-id="af801-239">HTTP Strict Transport Security (HSTS)</span></span>](xref:security/enforcing-ssl#http-strict-transport-security-protocol-hsts) | <span data-ttu-id="af801-240">특별한 응답 헤더를 추가하는 보안 향상 미들웨어입니다(ASP.NET Core 2.1 이상).</span><span class="sxs-lookup"><span data-stu-id="af801-240">Security enhancement middleware that adds a special response header (ASP.NET Core 2.1 or later).</span></span> | <span data-ttu-id="af801-241">응답이 전송되기 이전, 요청을 수정하는 구성 요소 이후에.</span><span class="sxs-lookup"><span data-stu-id="af801-241">Before responses are sent and after components that modify requests.</span></span> <span data-ttu-id="af801-242">예: 전달된 헤더, URL 재작성.</span><span class="sxs-lookup"><span data-stu-id="af801-242">Examples: Forwarded Headers, URL Rewriting.</span></span> |
| [<span data-ttu-id="af801-243">MVC</span><span class="sxs-lookup"><span data-stu-id="af801-243">MVC</span></span>](xref:mvc/overview) | <span data-ttu-id="af801-244">MVC/Razor Pages(ASP.NET Core 2.0 이상)를 사용하여 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-244">Processes requests with MVC/Razor Pages (ASP.NET Core 2.0 or later).</span></span> | <span data-ttu-id="af801-245">요청이 경로와 일치하는 경우 터미널입니다.</span><span class="sxs-lookup"><span data-stu-id="af801-245">Terminal if a request matches a route.</span></span> |
| [<span data-ttu-id="af801-246">OWIN</span><span class="sxs-lookup"><span data-stu-id="af801-246">OWIN</span></span>](xref:fundamentals/owin) | <span data-ttu-id="af801-247">OWIN 기반 앱, 서버 및 미들웨어와 상호 운용됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-247">Interop with OWIN-based apps, servers, and middleware.</span></span> | <span data-ttu-id="af801-248">OWIN 미들웨어가 요청을 완벽하게 처리하는 경우 터미널입니다.</span><span class="sxs-lookup"><span data-stu-id="af801-248">Terminal if the OWIN Middleware fully processes the request.</span></span> |
| [<span data-ttu-id="af801-249">응답 캐싱</span><span class="sxs-lookup"><span data-stu-id="af801-249">Response Caching</span></span>](xref:performance/caching/middleware) | <span data-ttu-id="af801-250">응답 캐시에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-250">Provides support for caching responses.</span></span> | <span data-ttu-id="af801-251">캐싱이 필요한 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="af801-251">Before components that require caching.</span></span> |
| [<span data-ttu-id="af801-252">응답 압축</span><span class="sxs-lookup"><span data-stu-id="af801-252">Response Compression</span></span>](xref:performance/response-compression) | <span data-ttu-id="af801-253">응답 압축에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-253">Provides support for compressing responses.</span></span> | <span data-ttu-id="af801-254">압축이 필요한 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="af801-254">Before components that require compression.</span></span> |
| [<span data-ttu-id="af801-255">요청 지역화</span><span class="sxs-lookup"><span data-stu-id="af801-255">Request Localization</span></span>](xref:fundamentals/localization) | <span data-ttu-id="af801-256">지역화 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-256">Provides localization support.</span></span> | <span data-ttu-id="af801-257">지역화 구분 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="af801-257">Before localization sensitive components.</span></span> |
| [<span data-ttu-id="af801-258">라우팅</span><span class="sxs-lookup"><span data-stu-id="af801-258">Routing</span></span>](xref:fundamentals/routing) | <span data-ttu-id="af801-259">요청 경로를 정의하고 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-259">Defines and constrains request routes.</span></span> | <span data-ttu-id="af801-260">경로 일치에 대한 터미널.</span><span class="sxs-lookup"><span data-stu-id="af801-260">Terminal for matching routes.</span></span> |
| [<span data-ttu-id="af801-261">세션</span><span class="sxs-lookup"><span data-stu-id="af801-261">Session</span></span>](xref:fundamentals/app-state) | <span data-ttu-id="af801-262">사용자 세션 관리에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-262">Provides support for managing user sessions.</span></span> | <span data-ttu-id="af801-263">세션이 필요한 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="af801-263">Before components that require Session.</span></span> |
| [<span data-ttu-id="af801-264">정적 파일</span><span class="sxs-lookup"><span data-stu-id="af801-264">Static Files</span></span>](xref:fundamentals/static-files) | <span data-ttu-id="af801-265">정적 파일 및 디렉터리 검색 처리에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-265">Provides support for serving static files and directory browsing.</span></span> | <span data-ttu-id="af801-266">요청이 파일과 일치하는 경우 터미널입니다.</span><span class="sxs-lookup"><span data-stu-id="af801-266">Terminal if a request matches a file.</span></span> |
| [<span data-ttu-id="af801-267">URL 재작성</span><span class="sxs-lookup"><span data-stu-id="af801-267">URL Rewriting</span></span>](xref:fundamentals/url-rewriting) | <span data-ttu-id="af801-268">URL 재작성 및 요청 리디렉션에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-268">Provides support for rewriting URLs and redirecting requests.</span></span> | <span data-ttu-id="af801-269">URL을 사용하는 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="af801-269">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="af801-270">WebSockets</span><span class="sxs-lookup"><span data-stu-id="af801-270">WebSockets</span></span>](xref:fundamentals/websockets) | <span data-ttu-id="af801-271">WebSocket 프로토콜을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-271">Enables the WebSockets protocol.</span></span> | <span data-ttu-id="af801-272">WebSocket 요청을 수락하는 데 필요한 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="af801-272">Before components that are required to accept WebSocket requests.</span></span> |

## <a name="write-middleware"></a><span data-ttu-id="af801-273">쓰기 미들웨어</span><span class="sxs-lookup"><span data-stu-id="af801-273">Write middleware</span></span>

<span data-ttu-id="af801-274">미들웨어는 일반적으로 클래스에서 캡슐화되고 확장 메서드로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-274">Middleware is generally encapsulated in a class and exposed with an extension method.</span></span> <span data-ttu-id="af801-275">쿼리 문자열에서 현재 요청에 대한 문화권을 설정하는 다음 미들웨어를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-275">Consider the following middleware, which sets the culture for the current request from a query string:</span></span>

[!code-csharp[](index/snapshot/Culture/StartupCulture.cs?name=snippet1)]

<span data-ttu-id="af801-276">위의 샘플 코드는 미들웨어 구성 요소를 만드는 방법을 보여주는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-276">The preceding sample code is used to demonstrate creating a middleware component.</span></span> <span data-ttu-id="af801-277">ASP.NET Core의 기본 제공 지역화 지원은 <xref:fundamentals/localization>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af801-277">For ASP.NET Core's built-in localization support, see <xref:fundamentals/localization>.</span></span>

<span data-ttu-id="af801-278">문화권을 전달하여 미들웨어를 테스트할 수 있습니다(예: `http://localhost:7997/?culture=no`).</span><span class="sxs-lookup"><span data-stu-id="af801-278">You can test the middleware by passing in the culture, for example `http://localhost:7997/?culture=no`.</span></span>

<span data-ttu-id="af801-279">다음 코드는 미들웨어 대리자를 클래스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-279">The following code moves the middleware delegate to a class:</span></span>

[!code-csharp[](index/snapshot/Culture/RequestCultureMiddleware.cs)]

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="af801-280">미들웨어 `Task` 메서드의 이름은 `Invoke`여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-280">The middleware `Task` method's name must be `Invoke`.</span></span> <span data-ttu-id="af801-281">ASP.NET 코어 2.0 이상에서는 이름이 `Invoke` 또는 `InvokeAsync`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-281">In ASP.NET Core 2.0 or later, the name can be either `Invoke` or `InvokeAsync`.</span></span>

::: moniker-end

<span data-ttu-id="af801-282">다음 확장 메서드는 <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder>를 통해 미들웨어를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-282">The following extension method exposes the middleware through <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder>:</span></span>

[!code-csharp[](index/snapshot/Culture/RequestCultureMiddlewareExtensions.cs)]

<span data-ttu-id="af801-283">다음 코드는 `Startup.Configure`에서 미들웨어를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-283">The following code calls the middleware from `Startup.Configure`:</span></span>

[!code-csharp[](index/snapshot/Culture/Startup.cs?name=snippet1&highlight=5)]

<span data-ttu-id="af801-284">미들웨어는 해당 생성자에서 해당 종속성을 노출하여 [명시적 종속성 원칙](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies)을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-284">Middleware should follow the [Explicit Dependencies Principle](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies) by exposing its dependencies in its constructor.</span></span> <span data-ttu-id="af801-285">미들웨어는 *응용 프로그램 수명*당 한 번 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="af801-285">Middleware is constructed once per *application lifetime*.</span></span> <span data-ttu-id="af801-286">요청 내에서 서비스를 미들웨어와 공유해야 하는 경우 [요청당 종속성](#per-request-dependencies) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af801-286">See the [Per-request dependencies](#per-request-dependencies) section if you need to share services with middleware within a request.</span></span>

<span data-ttu-id="af801-287">미들웨어 구성 요소는 생성자 매개 변수를 통해 [DI(종속성 주입)](xref:fundamentals/dependency-injection)에서 해당 종속성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-287">Middleware components can resolve their dependencies from [dependency injection (DI)](xref:fundamentals/dependency-injection) through constructor parameters.</span></span> <span data-ttu-id="af801-288">[UseMiddleware&lt;T&gt;](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions.usemiddleware#Microsoft_AspNetCore_Builder_UseMiddlewareExtensions_UseMiddleware_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Type_System_Object___)는 추가 매개 변수를 직접 수락할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-288">[UseMiddleware&lt;T&gt;](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions.usemiddleware#Microsoft_AspNetCore_Builder_UseMiddlewareExtensions_UseMiddleware_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Type_System_Object___) can also accept additional parameters directly.</span></span>

### <a name="per-request-dependencies"></a><span data-ttu-id="af801-289">요청당 종속성</span><span class="sxs-lookup"><span data-stu-id="af801-289">Per-request dependencies</span></span>

<span data-ttu-id="af801-290">미들웨어는 요청당이 아닌 앱 시작 시 생성되므로 미들웨어 생성자에 의해 사용되는 *범위가 지정된* 수명 서비스는 각 요청 중에 다른 종속성 주입된 형식과 공유되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-290">Because middleware is constructed at app startup, not per-request, *scoped* lifetime services used by middleware constructors aren't shared with other dependency-injected types during each request.</span></span> <span data-ttu-id="af801-291">*범위가 지정된* 서비스를 미들웨어와 다른 형식 간에 공유해야 하는 경우 이러한 서비스를 `Invoke` 메서드의 서명에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af801-291">If you must share a *scoped* service between your middleware and other types, add these services to the `Invoke` method's signature.</span></span> <span data-ttu-id="af801-292">`Invoke` 메서드는 DI로 채워지는 추가 매개 변수를 수락할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af801-292">The `Invoke` method can accept additional parameters that are populated by DI:</span></span>

```csharp
public class CustomMiddleware
{
    private readonly RequestDelegate _next;

    public CustomMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    // IMyScopedService is injected into Invoke
    public async Task Invoke(HttpContext httpContext, IMyScopedService svc)
    {
        svc.MyProperty = 1000;
        await _next(httpContext);
    }
}
```

## <a name="additional-resources"></a><span data-ttu-id="af801-293">추가 자료</span><span class="sxs-lookup"><span data-stu-id="af801-293">Additional resources</span></span>

* <xref:migration/http-modules>
* <xref:fundamentals/startup>
* <xref:fundamentals/request-features>
* <xref:fundamentals/middleware/extensibility>
* <xref:fundamentals/middleware/extensibility-third-party-container>
