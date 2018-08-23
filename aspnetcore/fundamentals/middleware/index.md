---
title: ASP.NET Core 미들웨어 기본 사항
author: rick-anderson
description: ASP.NET Core 미들웨어 및 요청 파이프라인에 대해 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 08/21/2018
uid: fundamentals/middleware/index
ms.openlocfilehash: 9ba77561ab4f6a8668c480d6e81f2ce7e0193c73
ms.sourcegitcommit: 5a2456cbf429069dc48aaa2823cde14100e4c438
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2018
ms.locfileid: "41870949"
---
# <a name="aspnet-core-middleware"></a><span data-ttu-id="13b89-103">ASP.NET Core 미들웨어</span><span class="sxs-lookup"><span data-stu-id="13b89-103">ASP.NET Core Middleware</span></span>

<span data-ttu-id="13b89-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="13b89-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="13b89-105">미들웨어는 요청 및 응답을 처리하는 앱 파이프라인으로 어셈블리되는 소프트웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-105">Middleware is software that's assembled into an app pipeline to handle requests and responses.</span></span> <span data-ttu-id="13b89-106">각 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="13b89-106">Each component:</span></span>

* <span data-ttu-id="13b89-107">요청을 파이프라인의 다음 구성 요소로 전달할지 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-107">Chooses whether to pass the request to the next component in the pipeline.</span></span>
* <span data-ttu-id="13b89-108">파이프라인의 다음 구성 요소가 호출되기 전과 후에 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-108">Can perform work before and after the next component in the pipeline is invoked.</span></span>

<span data-ttu-id="13b89-109">요청 대리자는 요청 파이프라인을 빌드하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-109">Request delegates are used to build the request pipeline.</span></span> <span data-ttu-id="13b89-110">요청 대리자는 각 HTTP 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-110">The request delegates handle each HTTP request.</span></span>

<span data-ttu-id="13b89-111">요청 대리자는 <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*>, <xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> 및 <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> 확장 메서드를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-111">Request delegates are configured using <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*>, <xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*>, and <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> extension methods.</span></span> <span data-ttu-id="13b89-112">개별 요청 대리자는 무명 메서드(인라인 미들웨어라고 함)로 인라인에서 지정되거나 다시 사용할 수 있는 클래스에서 정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-112">An individual request delegate can be specified in-line as an anonymous method (called in-line middleware), or it can be defined in a reusable class.</span></span> <span data-ttu-id="13b89-113">이러한 다시 사용할 수 있는 클래스 및 인라인 무명 메서드는 *미들웨어*이며, *미들웨어 구성 요소*라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-113">These reusable classes and in-line anonymous methods are *middleware*, also called *middleware components*.</span></span> <span data-ttu-id="13b89-114">요청 파이프라인의 각 미들웨어 구성 요소는 파이프라인의 그 다음 구성 요소를 호출하거나 파이프라인을 단락(short-circuiting)하는 역할을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-114">Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline or short-circuiting the pipeline.</span></span>

<span data-ttu-id="13b89-115"><xref:migration/http-modules>은 ASP.NET Core와 ASP.NET 4.x의 요청 파이프라인 간의 차이점을 설명하고 더 많은 미들웨어 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-115"><xref:migration/http-modules> explains the difference between request pipelines in ASP.NET Core and ASP.NET 4.x and provides more middleware samples.</span></span>

## <a name="create-a-middleware-pipeline-with-iapplicationbuilder"></a><span data-ttu-id="13b89-116">IApplicationBuilder로 미들웨어 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="13b89-116">Create a middleware pipeline with IApplicationBuilder</span></span>

<span data-ttu-id="13b89-117">ASP.NET Core 요청 파이프라인은 하나씩 차례로 호출되는 요청 대리자 시퀀스로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-117">The ASP.NET Core request pipeline consists of a sequence of request delegates, called one after the other.</span></span> <span data-ttu-id="13b89-118">다음 다이어그램은 개념을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-118">The following diagram demonstrates the concept.</span></span> <span data-ttu-id="13b89-119">실행 스레드는 검은색 화살표를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-119">The thread of execution follows the black arrows.</span></span>

![요청이 도착하고, 세 가지 미들웨어를 처리하고, 응답이 앱에서 나가는 것을 보여주는 요청 처리 패턴입니다.](index/_static/request-delegate-pipeline.png)

<span data-ttu-id="13b89-123">각 대리자는 다음 대리자 전과 후에 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-123">Each delegate can perform operations before and after the next delegate.</span></span> <span data-ttu-id="13b89-124">또한 대리자는 다음 대리자에 요청을 전달하지 않도록 결정할 수 있습니다. 이를 *요청 파이프라인을 단락(short-circuiting)* 한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-124">A delegate can also decide to not pass a request to the next delegate, which is called *short-circuiting the request pipeline*.</span></span> <span data-ttu-id="13b89-125">단락(short-circuiting)은 불필요한 작업을 방지하기 때문에 보통 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-125">Short-circuiting is often desirable because it avoids unnecessary work.</span></span> <span data-ttu-id="13b89-126">예를 들어 정적 파일 미들웨어는 정적 파일에 대한 요청을 반환하고 나머지 파이프라인을 단락(short-circuit)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-126">For example, Static Files Middleware can return a request for a static file and short-circuit the rest of the pipeline.</span></span> <span data-ttu-id="13b89-127">예외 처리 대리자는 파이프라인의 이후 단계에서 발생하는 예외를 catch할 수 있도록 파이프라인의 초기에 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-127">Exception-handling delegates are called early in the pipeline, so they can catch exceptions that occur in later stages of the pipeline.</span></span>

<span data-ttu-id="13b89-128">가장 간단한 가능한 ASP.NET Core 앱은 모든 요청을 처리하는 단일 요청 대리자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-128">The simplest possible ASP.NET Core app sets up a single request delegate that handles all requests.</span></span> <span data-ttu-id="13b89-129">이 경우 실제 요청 파이프라인은 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-129">This case doesn't include an actual request pipeline.</span></span> <span data-ttu-id="13b89-130">대신, 단일 익명 함수가 모든 HTTP 요청에 대한 응답에 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-130">Instead, a single anonymous function is called in response to every HTTP request.</span></span>

[!code-csharp[](index/snapshot/Middleware/Startup.cs?name=snippet1)]

<span data-ttu-id="13b89-131">첫 번째 <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*> 대리자는 파이프라인을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-131">The first <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*> delegate terminates the pipeline.</span></span>

<span data-ttu-id="13b89-132"><xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*>를 사용하여 여러 요청 대리자를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-132">Chain multiple request delegates together with <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*>.</span></span> <span data-ttu-id="13b89-133">`next` 매개 변수는 파이프라인의 다음 대리자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-133">The `next` parameter represents the next delegate in the pipeline.</span></span> <span data-ttu-id="13b89-134">*next* 매개 변수를 호출하지 *않고* 파이프라인을 단락(short-circuit)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-134">You can short-circuit the pipeline by *not* calling the *next* parameter.</span></span> <span data-ttu-id="13b89-135">다음 예제의 설명처럼, 일반적으로 다음 대리자 전과 후 모두에서 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-135">You can typically perform actions both before and after the next delegate, as the following example demonstrates:</span></span>

[!code-csharp[](index/snapshot/Chain/Startup.cs?name=snippet1)]

> [!WARNING]
> <span data-ttu-id="13b89-136">클라이언트에 응답을 전송한 후에 `next.Invoke`를 호출하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="13b89-136">Don't call `next.Invoke` after the response has been sent to the client.</span></span> <span data-ttu-id="13b89-137">응답이 시작된 후 <xref:Microsoft.AspNetCore.Http.HttpResponse>로 변경하면 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-137">Changes to <xref:Microsoft.AspNetCore.Http.HttpResponse> after the response has started throw an exception.</span></span> <span data-ttu-id="13b89-138">예를 들어 헤더 및 상태 코드를 설정하는 변경 작업은 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-138">For example, changes such as setting headers and a status code throw an exception.</span></span> <span data-ttu-id="13b89-139">`next`를 호출한 후 응답 본문에 작성하기:</span><span class="sxs-lookup"><span data-stu-id="13b89-139">Writing to the response body after calling `next`:</span></span>
>
> * <span data-ttu-id="13b89-140">프로토콜 위반이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-140">May cause a protocol violation.</span></span> <span data-ttu-id="13b89-141">예를 들어, 명시된 `Content-Length`보다 긴 내용이 작성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-141">For example, writing more than the stated `Content-Length`.</span></span>
> * <span data-ttu-id="13b89-142">본문 형식을 손상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-142">May corrupt the body format.</span></span> <span data-ttu-id="13b89-143">예를 들어 CSS 파일에 HTML 바닥글 작성하기.</span><span class="sxs-lookup"><span data-stu-id="13b89-143">For example, writing an HTML footer to a CSS file.</span></span>
>
> <span data-ttu-id="13b89-144"><xref:Microsoft.AspNetCore.Http.HttpResponse.HasStarted*>는 헤더가 이미 전송됐는지 또는 본문이 이미 작성됐는지 여부를 나타내는 유용한 힌트를 제공해줍니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-144"><xref:Microsoft.AspNetCore.Http.HttpResponse.HasStarted*> is a useful hint to indicate if headers have been sent or the body has been written to.</span></span>

## <a name="order"></a><span data-ttu-id="13b89-145">순서</span><span class="sxs-lookup"><span data-stu-id="13b89-145">Order</span></span>

<span data-ttu-id="13b89-146">미들웨어 구성 요소가 `Startup.Configure` 메서드에 추가되는 순서는 요청에서 미들웨어 구성 요소가 호출되는 순서와 응답에 대한 역순서를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-146">The order that middleware components are added in the `Startup.Configure` method defines the order in which the middleware components are invoked on requests and the reverse order for the response.</span></span> <span data-ttu-id="13b89-147">순서는 보안, 성능 및 기능에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-147">The order is critical for security, performance, and functionality.</span></span>

<span data-ttu-id="13b89-148">다음 `Configure` 메서드는 다음 미들웨어 구성 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-148">The following `Configure` method adds the following middleware components:</span></span>

1. <span data-ttu-id="13b89-149">예외/오류 처리</span><span class="sxs-lookup"><span data-stu-id="13b89-149">Exception/error handling</span></span>
2. <span data-ttu-id="13b89-150">정적 파일 서버</span><span class="sxs-lookup"><span data-stu-id="13b89-150">Static file server</span></span>
3. <span data-ttu-id="13b89-151">인증</span><span class="sxs-lookup"><span data-stu-id="13b89-151">Authentication</span></span>
4. <span data-ttu-id="13b89-152">MVC</span><span class="sxs-lookup"><span data-stu-id="13b89-152">MVC</span></span>

::: moniker range=">= aspnetcore-2.0"

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
    //   Protection Regulation (GDPR) regulations.
    app.UseCookiePolicy();

    // Authenticate before the user accesses secure resources.
    app.UseAuthentication();

    // Add MVC to the request pipeline.
    app.UseMvc();
}
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

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

    // Add MVC to the request pipeline.
    app.UseMvcWithDefaultRoute();
}
```

::: moniker-end

<span data-ttu-id="13b89-153">위의 코드에서 <xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*>는 파이프라인에 처음으로 추가된 미들웨어 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-153">In the code above, <xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> is the first middleware component added to the pipeline.</span></span> <span data-ttu-id="13b89-154">따라서 예외 처리기 미들웨어는 후속 호출에서 발생하는 모든 예외를 catch 합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-154">Therefore, the Exception Handler Middleware catches any exceptions that occur in later calls.</span></span>

<span data-ttu-id="13b89-155">정적 파일 미들웨어는 파이프라인 초기에 호출되므로 요청을 처리하고 나머지 구성 요소를 통과하지 않고 단락(short-circuit)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-155">Static Files Middleware is called early in the pipeline so that it can handle requests and short-circuit without going through the remaining components.</span></span> <span data-ttu-id="13b89-156">정적 파일 미들웨어는 권한 부여 검사를 제공하지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="13b89-156">The Static Files Middleware provides **no** authorization checks.</span></span> <span data-ttu-id="13b89-157">*wwwroot* 아래의 항목을 비롯한 제공되는 모든 파일은 공개적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-157">Any files served by it, including those under *wwwroot*, are publicly available.</span></span> <span data-ttu-id="13b89-158">정적 파일을 보호하는 방법은 <xref:fundamentals/static-files>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13b89-158">For an approach to secure static files, see <xref:fundamentals/static-files>.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="13b89-159">요청이 정적 파일 미들웨어에서 처리되지 않는 경우 인증을 수행하는 인증 미들웨어(<xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*>)로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-159">If the request isn't handled by the Static Files Middleware, it's passed on to the Authentication Middleware (<xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*>), which performs authentication.</span></span> <span data-ttu-id="13b89-160">인증은 인증되지 않은 요청을 단락(short-circuit)하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-160">Authentication doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="13b89-161">인증 미들웨어가 요청을 인증하지만, MVC가 특정 Razor Page 또는 컨트롤러 및 작업을 선택한 후에만 권한 부여(및 거부)가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-161">Although Authentication Middleware authenticates requests, authorization (and rejection) occurs only after MVC selects a specific Razor Page or MVC controller and action.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="13b89-162">요청이 정적 파일 미들웨어에서 처리되지 않는 경우 인증을 수행하는 ID 미들웨어(<xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*>)로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-162">If the request isn't handled by Static Files Middleware, it's passed on to the Identity Middleware (<xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*>), which performs authentication.</span></span> <span data-ttu-id="13b89-163">ID는 인증되지 않은 요청을 단락(short-circuit)하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-163">Identity doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="13b89-164">ID가 요청을 인증하지만 MVC가 특정 컨트롤러 및 작업을 선택한 후에만 권한 부여(및 거부)가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-164">Although Identity authenticates requests, authorization (and rejection) occurs only after MVC selects a specific controller and action.</span></span>

::: moniker-end

<span data-ttu-id="13b89-165">다음 예제는 정적 파일에 대한 요청이 응답 압축 미들웨어 전에 정적 파일 미들웨어에서 처리되는 미들웨어 순서를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-165">The following example demonstrates a middleware order where requests for static files are handled by Static Files Middleware before Response Compression Middleware.</span></span> <span data-ttu-id="13b89-166">정적 파일은 이 미들웨어 순서를 사용하여 압축되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-166">Static files aren't compressed with this middleware order.</span></span> <span data-ttu-id="13b89-167"><xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*>의 MVC 응답은 압축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-167">The MVC responses from <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> can be compressed.</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    // Static files not compressed by Static Files Middleware.
    app.UseStaticFiles();
    app.UseResponseCompression();
    app.UseMvcWithDefaultRoute();
}
```

### <a name="use-run-and-map"></a><span data-ttu-id="13b89-168">Use, Run 및 Map</span><span class="sxs-lookup"><span data-stu-id="13b89-168">Use, Run, and Map</span></span>

<span data-ttu-id="13b89-169">`Use`, `Run` 및 `Map`을 사용하여 HTTP 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-169">Configure the HTTP pipeline using `Use`, `Run`, and `Map`.</span></span> <span data-ttu-id="13b89-170">`Use` 메서드는 파이프라인을 단락(short-circuit)할 수 있습니다(즉, `next` 요청 대리자를 호출하지 않는 경우).</span><span class="sxs-lookup"><span data-stu-id="13b89-170">The `Use` method can short-circuit the pipeline (that is, if it doesn't call a `next` request delegate).</span></span> <span data-ttu-id="13b89-171">`Run`은 규칙이며 일부 미들웨어 구성 요소는 파이프라인의 끝에서 실행되는 `Run[Middleware]` 메서드를 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-171">`Run` is a convention, and some middleware components may expose `Run[Middleware]` methods that run at the end of the pipeline.</span></span>

<span data-ttu-id="13b89-172"><xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> 확장은 파이프라인 분기에 규칙으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-172"><xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> extensions are used as a convention for branching the pipeline.</span></span> <span data-ttu-id="13b89-173">`Map*`은 지정된 요청 경로의 일치를 기반으로 요청 파이프라인을 분기합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-173">`Map*` branches the request pipeline based on matches of the given request path.</span></span> <span data-ttu-id="13b89-174">요청 경로가 지정된 경로로 시작하는 경우 분기가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-174">If the request path starts with the given path, the branch is executed.</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMap.cs?name=snippet1)]

<span data-ttu-id="13b89-175">다음 표는 앞의 코드를 사용하여 `http://localhost:1234`의 요청 및 응답을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-175">The following table shows the requests and responses from `http://localhost:1234` using the previous code.</span></span>

| <span data-ttu-id="13b89-176">요청</span><span class="sxs-lookup"><span data-stu-id="13b89-176">Request</span></span>             | <span data-ttu-id="13b89-177">응답</span><span class="sxs-lookup"><span data-stu-id="13b89-177">Response</span></span>                     |
| ------------------- | ---------------------------- |
| <span data-ttu-id="13b89-178">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="13b89-178">localhost:1234</span></span>      | <span data-ttu-id="13b89-179">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="13b89-179">Hello from non-Map delegate.</span></span> |
| <span data-ttu-id="13b89-180">localhost:1234/map1</span><span class="sxs-lookup"><span data-stu-id="13b89-180">localhost:1234/map1</span></span> | <span data-ttu-id="13b89-181">Map Test 1</span><span class="sxs-lookup"><span data-stu-id="13b89-181">Map Test 1</span></span>                   |
| <span data-ttu-id="13b89-182">localhost:1234/map2</span><span class="sxs-lookup"><span data-stu-id="13b89-182">localhost:1234/map2</span></span> | <span data-ttu-id="13b89-183">Map Test 2</span><span class="sxs-lookup"><span data-stu-id="13b89-183">Map Test 2</span></span>                   |
| <span data-ttu-id="13b89-184">localhost:1234/map3</span><span class="sxs-lookup"><span data-stu-id="13b89-184">localhost:1234/map3</span></span> | <span data-ttu-id="13b89-185">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="13b89-185">Hello from non-Map delegate.</span></span> |

<span data-ttu-id="13b89-186">`Map`이 사용되는 경우 일치하는 경로 세그먼트는 `HttpRequest.Path`에서 제거되고 각 요청에 대해 `HttpRequest.PathBase`에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-186">When `Map` is used, the matched path segment(s) are removed from `HttpRequest.Path` and appended to `HttpRequest.PathBase` for each request.</span></span>

<span data-ttu-id="13b89-187">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions)은 지정된 조건자의 결과를 기반으로 요청 파이프라인을 분기합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-187">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions) branches the request pipeline based on the result of the given predicate.</span></span> <span data-ttu-id="13b89-188">`Func<HttpContext, bool>` 형식의 조건자는 파이프라인의 새 분기에 요청을 매핑하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-188">Any predicate of type `Func<HttpContext, bool>` can be used to map requests to a new branch of the pipeline.</span></span> <span data-ttu-id="13b89-189">다음 예제에서 조건자는 쿼리 문자열 변수 `branch`의 존재를 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-189">In the following example, a predicate is used to detect the presence of a query string variable `branch`:</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMapWhen.cs?name=snippet1)]

<span data-ttu-id="13b89-190">다음 표는 앞의 코드를 사용하여 `http://localhost:1234`의 요청 및 응답을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-190">The following table shows the requests and responses from `http://localhost:1234` using the previous code.</span></span>

| <span data-ttu-id="13b89-191">요청</span><span class="sxs-lookup"><span data-stu-id="13b89-191">Request</span></span>                       | <span data-ttu-id="13b89-192">응답</span><span class="sxs-lookup"><span data-stu-id="13b89-192">Response</span></span>                     |
| ----------------------------- | ---------------------------- |
| <span data-ttu-id="13b89-193">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="13b89-193">localhost:1234</span></span>                | <span data-ttu-id="13b89-194">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="13b89-194">Hello from non-Map delegate.</span></span> |
| <span data-ttu-id="13b89-195">localhost:1234/?branch=master</span><span class="sxs-lookup"><span data-stu-id="13b89-195">localhost:1234/?branch=master</span></span> | <span data-ttu-id="13b89-196">Branch used = master</span><span class="sxs-lookup"><span data-stu-id="13b89-196">Branch used = master</span></span>         |

<span data-ttu-id="13b89-197">`Map`은 중첩을 지원합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-197">`Map` supports nesting, for example:</span></span>

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

<span data-ttu-id="13b89-198">`Map`은 여러 세그먼트를 한 번에 일치시킬 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-198">`Map` can also match multiple segments at once:</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMultiSeg.cs?name=snippet1&highlight=13)]

## <a name="built-in-middleware"></a><span data-ttu-id="13b89-199">기본 제공 미들웨어</span><span class="sxs-lookup"><span data-stu-id="13b89-199">Built-in middleware</span></span>

<span data-ttu-id="13b89-200">ASP.NET Core는 다음과 같은 미들웨어 구성 요소가 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-200">ASP.NET Core ships with the following middleware components.</span></span> <span data-ttu-id="13b89-201">*순서* 열은 요청 파이프라인에서 미들웨어의 배치, 미들웨어가 요청을 종료하고 다른 미들웨어가 요청을 처리하지 못하게 차단하는 조건에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-201">The *Order* column provides notes on the middleware's placement in the request pipeline and under what conditions the middleware may terminate the request and prevent other middleware from processing a request.</span></span>

| <span data-ttu-id="13b89-202">미들웨어</span><span class="sxs-lookup"><span data-stu-id="13b89-202">Middleware</span></span> | <span data-ttu-id="13b89-203">설명</span><span class="sxs-lookup"><span data-stu-id="13b89-203">Description</span></span> | <span data-ttu-id="13b89-204">순서</span><span class="sxs-lookup"><span data-stu-id="13b89-204">Order</span></span> |
| ---------- | ----------- | ----- |
| [<span data-ttu-id="13b89-205">인증</span><span class="sxs-lookup"><span data-stu-id="13b89-205">Authentication</span></span>](xref:security/authentication/identity) | <span data-ttu-id="13b89-206">인증 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-206">Provides authentication support.</span></span> | <span data-ttu-id="13b89-207">`HttpContext.User`가 필요하기 전에.</span><span class="sxs-lookup"><span data-stu-id="13b89-207">Before `HttpContext.User` is needed.</span></span> <span data-ttu-id="13b89-208">OAuth 콜백에 대한 터미널.</span><span class="sxs-lookup"><span data-stu-id="13b89-208">Terminal for OAuth callbacks.</span></span> |
| [<span data-ttu-id="13b89-209">CORS</span><span class="sxs-lookup"><span data-stu-id="13b89-209">CORS</span></span>](xref:security/cors) | <span data-ttu-id="13b89-210">원본 간 리소스 공유를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-210">Configures Cross-Origin Resource Sharing.</span></span> | <span data-ttu-id="13b89-211">CORS를 사용하는 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="13b89-211">Before components that use CORS.</span></span> |
| [<span data-ttu-id="13b89-212">진단</span><span class="sxs-lookup"><span data-stu-id="13b89-212">Diagnostics</span></span>](xref:fundamentals/error-handling) | <span data-ttu-id="13b89-213">진단을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-213">Configures diagnostics.</span></span> | <span data-ttu-id="13b89-214">오류를 생성하는 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="13b89-214">Before components that generate errors.</span></span> |
| [<span data-ttu-id="13b89-215">전달된 헤더</span><span class="sxs-lookup"><span data-stu-id="13b89-215">Forwarded Headers</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions) | <span data-ttu-id="13b89-216">프록시된 헤더를 현재 요청에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-216">Forwards proxied headers onto the current request.</span></span> | <span data-ttu-id="13b89-217">구성 요소가 업데이트된 필드를 사용하기 이전입니다(예: 체계, 호스트, 클라이언트 IP, 메서드).</span><span class="sxs-lookup"><span data-stu-id="13b89-217">Before components that consume the updated fields (examples: scheme, host, client IP, method).</span></span> |
| [<span data-ttu-id="13b89-218">HTTP 메서드 재정의</span><span class="sxs-lookup"><span data-stu-id="13b89-218">HTTP Method Override</span></span>](/dotnet/api/microsoft.aspnetcore.builder.httpmethodoverrideextensions) | <span data-ttu-id="13b89-219">들어오는 POST 요청이 메서드를 재정의하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-219">Allows an incoming POST request to override the method.</span></span> | <span data-ttu-id="13b89-220">업데이트된 메서드를 사용하는 구성 요소 앞입니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-220">Before components that consume the updated method.</span></span> |
| [<span data-ttu-id="13b89-221">HTTPS 리디렉션</span><span class="sxs-lookup"><span data-stu-id="13b89-221">HTTPS Redirection</span></span>](xref:security/enforcing-ssl#require-https) | <span data-ttu-id="13b89-222">HTTPS로 모든 HTTP 요청을 리디렉션합니다(ASP.NET Core 2.1 이상).</span><span class="sxs-lookup"><span data-stu-id="13b89-222">Redirect all HTTP requests to HTTPS (ASP.NET Core 2.1 or later).</span></span> | <span data-ttu-id="13b89-223">URL을 사용하는 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="13b89-223">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="13b89-224">HSTS(HTTP 엄격한 전송 보안)</span><span class="sxs-lookup"><span data-stu-id="13b89-224">HTTP Strict Transport Security (HSTS)</span></span>](xref:security/enforcing-ssl#http-strict-transport-security-protocol-hsts) | <span data-ttu-id="13b89-225">특별한 응답 헤더를 추가하는 보안 향상 미들웨어입니다(ASP.NET Core 2.1 이상).</span><span class="sxs-lookup"><span data-stu-id="13b89-225">Security enhancement middleware that adds a special response header (ASP.NET Core 2.1 or later).</span></span> | <span data-ttu-id="13b89-226">응답이 보내지기 이전 및 구성 요소가 요청을 수정한 이후입니다(예: 전달된 헤더, URL 다시 쓰기).</span><span class="sxs-lookup"><span data-stu-id="13b89-226">Before responses are sent and after components that modify requests (for example, Forwarded Headers, URL Rewriting).</span></span> |
| [<span data-ttu-id="13b89-227">MVC</span><span class="sxs-lookup"><span data-stu-id="13b89-227">MVC</span></span>](xref:mvc/overview) | <span data-ttu-id="13b89-228">MVC/Razor Pages(ASP.NET Core 2.0 이상)를 사용하여 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-228">Processes requests with MVC/Razor Pages (ASP.NET Core 2.0 or later).</span></span> | <span data-ttu-id="13b89-229">요청이 경로와 일치하는 경우 터미널입니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-229">Terminal if a request matches a route.</span></span> |
| [<span data-ttu-id="13b89-230">OWIN</span><span class="sxs-lookup"><span data-stu-id="13b89-230">OWIN</span></span>](xref:fundamentals/owin) | <span data-ttu-id="13b89-231">OWIN 기반 앱, 서버 및 미들웨어와 상호 운용됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-231">Interop with OWIN-based apps, servers, and middleware.</span></span> | <span data-ttu-id="13b89-232">OWIN 미들웨어가 요청을 완벽하게 처리하는 경우 터미널입니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-232">Terminal if the OWIN Middleware fully processes the request.</span></span> |
| [<span data-ttu-id="13b89-233">응답 캐싱</span><span class="sxs-lookup"><span data-stu-id="13b89-233">Response Caching</span></span>](xref:performance/caching/middleware) | <span data-ttu-id="13b89-234">응답 캐시에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-234">Provides support for caching responses.</span></span> | <span data-ttu-id="13b89-235">캐싱이 필요한 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="13b89-235">Before components that require caching.</span></span> |
| [<span data-ttu-id="13b89-236">응답 압축</span><span class="sxs-lookup"><span data-stu-id="13b89-236">Response Compression</span></span>](xref:performance/response-compression) | <span data-ttu-id="13b89-237">응답 압축에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-237">Provides support for compressing responses.</span></span> | <span data-ttu-id="13b89-238">압축이 필요한 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="13b89-238">Before components that require compression.</span></span> |
| [<span data-ttu-id="13b89-239">요청 지역화</span><span class="sxs-lookup"><span data-stu-id="13b89-239">Request Localization</span></span>](xref:fundamentals/localization) | <span data-ttu-id="13b89-240">지역화 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-240">Provides localization support.</span></span> | <span data-ttu-id="13b89-241">지역화 구분 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="13b89-241">Before localization sensitive components.</span></span> |
| [<span data-ttu-id="13b89-242">라우팅</span><span class="sxs-lookup"><span data-stu-id="13b89-242">Routing</span></span>](xref:fundamentals/routing) | <span data-ttu-id="13b89-243">요청 경로를 정의하고 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-243">Defines and constrains request routes.</span></span> | <span data-ttu-id="13b89-244">경로 일치에 대한 터미널.</span><span class="sxs-lookup"><span data-stu-id="13b89-244">Terminal for matching routes.</span></span> |
| [<span data-ttu-id="13b89-245">세션</span><span class="sxs-lookup"><span data-stu-id="13b89-245">Session</span></span>](xref:fundamentals/app-state) | <span data-ttu-id="13b89-246">사용자 세션 관리에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-246">Provides support for managing user sessions.</span></span> | <span data-ttu-id="13b89-247">세션이 필요한 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="13b89-247">Before components that require Session.</span></span> |
| [<span data-ttu-id="13b89-248">정적 파일</span><span class="sxs-lookup"><span data-stu-id="13b89-248">Static Files</span></span>](xref:fundamentals/static-files) | <span data-ttu-id="13b89-249">정적 파일 및 디렉터리 검색 처리에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-249">Provides support for serving static files and directory browsing.</span></span> | <span data-ttu-id="13b89-250">요청이 파일과 일치하는 경우 터미널입니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-250">Terminal if a request matches a file.</span></span> |
| [<span data-ttu-id="13b89-251">URL 재작성</span><span class="sxs-lookup"><span data-stu-id="13b89-251">URL Rewriting</span></span>](xref:fundamentals/url-rewriting) | <span data-ttu-id="13b89-252">URL 재작성 및 요청 리디렉션에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-252">Provides support for rewriting URLs and redirecting requests.</span></span> | <span data-ttu-id="13b89-253">URL을 사용하는 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="13b89-253">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="13b89-254">WebSockets</span><span class="sxs-lookup"><span data-stu-id="13b89-254">WebSockets</span></span>](xref:fundamentals/websockets) | <span data-ttu-id="13b89-255">WebSocket 프로토콜을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-255">Enables the WebSockets protocol.</span></span> | <span data-ttu-id="13b89-256">WebSocket 요청을 수락하는 데 필요한 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="13b89-256">Before components that are required to accept WebSocket requests.</span></span> |

## <a name="write-middleware"></a><span data-ttu-id="13b89-257">쓰기 미들웨어</span><span class="sxs-lookup"><span data-stu-id="13b89-257">Write middleware</span></span>

<span data-ttu-id="13b89-258">미들웨어는 일반적으로 클래스에서 캡슐화되고 확장 메서드로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-258">Middleware is generally encapsulated in a class and exposed with an extension method.</span></span> <span data-ttu-id="13b89-259">쿼리 문자열에서 현재 요청에 대한 문화권을 설정하는 다음 미들웨어를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-259">Consider the following middleware, which sets the culture for the current request from a query string:</span></span>

[!code-csharp[](index/snapshot/Culture/StartupCulture.cs?name=snippet1)]

<span data-ttu-id="13b89-260">위의 샘플 코드는 미들웨어 구성 요소를 만드는 방법을 보여주는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-260">The preceding sample code is used to demonstrate creating a middleware component.</span></span> <span data-ttu-id="13b89-261">ASP.NET Core의 기본 제공 지역화 지원은 <xref:fundamentals/localization>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13b89-261">For ASP.NET Core's built-in localization support, see <xref:fundamentals/localization>.</span></span>

<span data-ttu-id="13b89-262">문화권을 전달하여 미들웨어를 테스트할 수 있습니다(예: `http://localhost:7997/?culture=no`).</span><span class="sxs-lookup"><span data-stu-id="13b89-262">You can test the middleware by passing in the culture, for example `http://localhost:7997/?culture=no`.</span></span>

<span data-ttu-id="13b89-263">다음 코드는 미들웨어 대리자를 클래스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-263">The following code moves the middleware delegate to a class:</span></span>

[!code-csharp[](index/snapshot/Culture/RequestCultureMiddleware.cs)]

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="13b89-264">미들웨어 `Task` 메서드의 이름은 `Invoke`여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-264">The middleware `Task` method's name must be `Invoke`.</span></span> <span data-ttu-id="13b89-265">ASP.NET 코어 2.0 이상에서는 이름이 `Invoke` 또는 `InvokeAsync`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-265">In ASP.NET Core 2.0 or later, the name can be either `Invoke` or `InvokeAsync`.</span></span>

::: moniker-end

<span data-ttu-id="13b89-266">다음 확장 메서드는 <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder>를 통해 미들웨어를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-266">The following extension method exposes the middleware through <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder>:</span></span>

[!code-csharp[](index/snapshot/Culture/RequestCultureMiddlewareExtensions.cs)]

<span data-ttu-id="13b89-267">다음 코드는 `Startup.Configure`에서 미들웨어를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-267">The following code calls the middleware from `Startup.Configure`:</span></span>

[!code-csharp[](index/snapshot/Culture/Startup.cs?name=snippet1&highlight=5)]

<span data-ttu-id="13b89-268">미들웨어는 해당 생성자에서 해당 종속성을 노출하여 [명시적 종속성 원칙](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies)을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-268">Middleware should follow the [Explicit Dependencies Principle](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies) by exposing its dependencies in its constructor.</span></span> <span data-ttu-id="13b89-269">미들웨어는 *응용 프로그램 수명*당 한 번 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-269">Middleware is constructed once per *application lifetime*.</span></span> <span data-ttu-id="13b89-270">요청 내에서 서비스를 미들웨어와 공유해야 하는 경우 [요청당 종속성](#per-request-dependencies) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13b89-270">See the [Per-request dependencies](#per-request-dependencies) section if you need to share services with middleware within a request.</span></span>

<span data-ttu-id="13b89-271">미들웨어 구성 요소는 생성자 매개 변수를 통해 [DI(종속성 주입)](xref:fundamentals/dependency-injection)에서 해당 종속성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-271">Middleware components can resolve their dependencies from [dependency injection (DI)](xref:fundamentals/dependency-injection) through constructor parameters.</span></span> <span data-ttu-id="13b89-272">[UseMiddleware&lt;T&gt;](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions.usemiddleware#Microsoft_AspNetCore_Builder_UseMiddlewareExtensions_UseMiddleware_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Type_System_Object___)는 추가 매개 변수를 직접 수락할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-272">[UseMiddleware&lt;T&gt;](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions.usemiddleware#Microsoft_AspNetCore_Builder_UseMiddlewareExtensions_UseMiddleware_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Type_System_Object___) can also accept additional parameters directly.</span></span>

### <a name="per-request-dependencies"></a><span data-ttu-id="13b89-273">요청당 종속성</span><span class="sxs-lookup"><span data-stu-id="13b89-273">Per-request dependencies</span></span>

<span data-ttu-id="13b89-274">미들웨어는 요청당이 아닌 앱 시작 시 생성되므로 미들웨어 생성자에 의해 사용되는 *범위가 지정된* 수명 서비스는 각 요청 중에 다른 종속성 주입된 형식과 공유되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-274">Because middleware is constructed at app startup, not per-request, *scoped* lifetime services used by middleware constructors aren't shared with other dependency-injected types during each request.</span></span> <span data-ttu-id="13b89-275">*범위가 지정된* 서비스를 미들웨어와 다른 형식 간에 공유해야 하는 경우 이러한 서비스를 `Invoke` 메서드의 서명에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-275">If you must share a *scoped* service between your middleware and other types, add these services to the `Invoke` method's signature.</span></span> <span data-ttu-id="13b89-276">`Invoke` 메서드는 DI로 채워지는 추가 매개 변수를 수락할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13b89-276">The `Invoke` method can accept additional parameters that are populated by DI:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="13b89-277">추가 자료</span><span class="sxs-lookup"><span data-stu-id="13b89-277">Additional resources</span></span>

* <xref:migration/http-modules>
* <xref:fundamentals/startup>
* <xref:fundamentals/request-features>
* <xref:fundamentals/middleware/extensibility>
* <xref:fundamentals/middleware/extensibility-third-party-container>
