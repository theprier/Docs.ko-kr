---
title: "ASP.NET Core 미들웨어"
author: rick-anderson
description: "ASP.NET Core 미들웨어 및 요청 파이프라인에 대해 알아봅니다."
manager: wpickett
ms.author: riande
ms.date: 01/22/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/middleware/index
ms.openlocfilehash: 887ba1a4742821226a7ebecfd238c97627d6c5f7
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="aspnet-core-middleware"></a><span data-ttu-id="b7b0a-103">ASP.NET Core 미들웨어</span><span class="sxs-lookup"><span data-stu-id="b7b0a-103">ASP.NET Core Middleware</span></span>

<span data-ttu-id="b7b0a-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="b7b0a-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="b7b0a-105">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/index/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="b7b0a-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/index/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="what-is-middleware"></a><span data-ttu-id="b7b0a-106">미들웨어는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b7b0a-106">What is middleware?</span></span>

<span data-ttu-id="b7b0a-107">미들웨어는 요청 및 응답을 처리하는 응용 프로그램 파이프라인으로 어셈블되는 소프트웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-107">Middleware is software that's assembled into an application pipeline to handle requests and responses.</span></span> <span data-ttu-id="b7b0a-108">각 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="b7b0a-108">Each component:</span></span>

* <span data-ttu-id="b7b0a-109">요청을 파이프라인의 다음 구성 요소로 전달할지 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-109">Chooses whether to pass the request to the next component in the pipeline.</span></span>
* <span data-ttu-id="b7b0a-110">파이프라인의 다음 구성 요소가 호출되기 전과 후에 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-110">Can perform work before and after the next component in the pipeline is invoked.</span></span> 

<span data-ttu-id="b7b0a-111">요청 대리자는 요청 파이프라인을 빌드하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-111">Request delegates are used to build the request pipeline.</span></span> <span data-ttu-id="b7b0a-112">요청 대리자는 각 HTTP 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-112">The request delegates handle each HTTP request.</span></span>

<span data-ttu-id="b7b0a-113">요청 대리자는 [Run](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.runextensions), [Map](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapextensions) 및 [Use](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.useextensions) 확장 메서드를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-113">Request delegates are configured using [Run](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.runextensions), [Map](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapextensions), and [Use](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.useextensions) extension methods.</span></span> <span data-ttu-id="b7b0a-114">개별 요청 대리자는 무명 메서드(인라인 미들웨어라고 함)로 인라인에서 지정되거나 다시 사용할 수 있는 클래스에서 정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-114">An individual request delegate can be specified in-line as an anonymous method (called in-line middleware), or it can be defined in a reusable class.</span></span> <span data-ttu-id="b7b0a-115">이러한 다시 사용할 수 있는 클래스 및 인라인 무명 메서드는 *미들웨어* 또는 *미들웨어 구성 요소*입니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-115">These reusable classes and in-line anonymous methods are *middleware*, or *middleware components*.</span></span> <span data-ttu-id="b7b0a-116">요청 파이프라인의 각 미들웨어 구성 요소는 파이프라인의 다음 구성 요소를 호출하거나 해당하는 경우 체인을 단락(short-circuiting)하는 일을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-116">Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline, or short-circuiting the chain if appropriate.</span></span>

<span data-ttu-id="b7b0a-117">[HTTP 모듈을 미들웨어로 마이그레이션](xref:migration/http-modules)은 ASP.NET Core와 ASP.NET 4.x의 요청 파이프라인 간의 차이점을 설명하고 더 많은 미들웨어 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-117">[Migrating HTTP Modules to Middleware](xref:migration/http-modules) explains the difference between request pipelines in ASP.NET Core and ASP.NET 4.x and provides more middleware samples.</span></span>

## <a name="creating-a-middleware-pipeline-with-iapplicationbuilder"></a><span data-ttu-id="b7b0a-118">IApplicationBuilder로 미들웨어 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="b7b0a-118">Creating a middleware pipeline with IApplicationBuilder</span></span>

<span data-ttu-id="b7b0a-119">ASP.NET Core 요청 파이프라인은 이 다이어그램이 보여 주는 것과 같이 차례로 호출되어 요청 대리자의 시퀀스로 구성됩니다(실행의 스레드는 검은색 화살표를 따름).</span><span class="sxs-lookup"><span data-stu-id="b7b0a-119">The ASP.NET Core request pipeline consists of a sequence of request delegates, called one after the other, as this diagram shows (the thread of execution follows the black arrows):</span></span>

![요청 도착을 표시하고, 세 가지 미들웨어를 통해 처리하는 요청 처리 패턴 및 응용 프로그램을 떠나는 응답](index/_static/request-delegate-pipeline.png)

<span data-ttu-id="b7b0a-123">각 대리자는 다음 대리자 전과 후에 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-123">Each delegate can perform operations before and after the next delegate.</span></span> <span data-ttu-id="b7b0a-124">대리자는 요청 파이프라인 단락(short-circuiting)이라고 하는 다음 대리자에 요청을 전달하지 않도록 결정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-124">A delegate can also decide to not pass a request to the next delegate, which is called short-circuiting the request pipeline.</span></span> <span data-ttu-id="b7b0a-125">단락(short-circuiting)은 불필요한 작업을 방지하기 때문에 종종 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-125">Short-circuiting is often desirable because it avoids unnecessary work.</span></span> <span data-ttu-id="b7b0a-126">예를 들어 정적 파일 미들웨어는 정적 파일에 대한 요청을 반환하고 나머지 파이프라인을 단락(short-circuit)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-126">For example, the static file middleware can return a request for a static file and short-circuit the rest of the pipeline.</span></span> <span data-ttu-id="b7b0a-127">예외 처리 대리자는 파이프라인의 이후 단계에서 발생하는 예외를 catch할 수 있도록 파이프라인의 초기에 호출되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-127">Exception-handling delegates need to be called early in the pipeline, so they can catch exceptions that occur in later stages of the pipeline.</span></span>

<span data-ttu-id="b7b0a-128">가장 간단한 가능한 ASP.NET Core 앱은 모든 요청을 처리하는 단일 요청 대리자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-128">The simplest possible ASP.NET Core app sets up a single request delegate that handles all requests.</span></span> <span data-ttu-id="b7b0a-129">이 사례는 실제 요청 파이프라인을 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-129">This case doesn't include an actual request pipeline.</span></span> <span data-ttu-id="b7b0a-130">대신, 단일 익명 함수는 모든 HTTP 요청에 대한 응답에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-130">Instead, a single anonymous function is called in response to every HTTP request.</span></span>

[!code-csharp[Main](index/sample/Middleware/Startup.cs)]

<span data-ttu-id="b7b0a-131">첫 번째 [app.Run](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.runextensions) 대리자는 파이프라인을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-131">The first [app.Run](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.runextensions) delegate terminates the pipeline.</span></span>

<span data-ttu-id="b7b0a-132">[app.Use](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.useextensions)를 사용하여 여러 요청 대리자를 함께 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-132">You can chain multiple request delegates together with [app.Use](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.useextensions).</span></span> <span data-ttu-id="b7b0a-133">`next` 매개 변수는 파이프라인의 다음 대리자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-133">The `next` parameter represents the next delegate in the pipeline.</span></span> <span data-ttu-id="b7b0a-134">(*next* 매개 변수를 호출하지 *않고* 파이프라인을 단락(short-circuit)할 수 있습니다.) 이 예제에서 설명하듯이 일반적으로 다음 대리자 전과 후 모두에서 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-134">(Remember that you can short-circuit the pipeline by *not* calling the *next* parameter.) You can typically perform actions both before and after the next delegate, as this example demonstrates:</span></span>

[!code-csharp[Main](index/sample/Chain/Startup.cs?name=snippet1)]

>[!WARNING]
> <span data-ttu-id="b7b0a-135">클라이언트에 응답을 전송한 후에 `next.Invoke`를 호출하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-135">Don't call `next.Invoke` after the response has been sent to the client.</span></span> <span data-ttu-id="b7b0a-136">응답이 시작된 후 `HttpResponse`로 변경하면 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-136">Changes to `HttpResponse` after the response has started will throw an exception.</span></span> <span data-ttu-id="b7b0a-137">예를 들어 헤더, 상태 코드 등을 설정하는 것과 같은 변경은 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-137">For example, changes such as setting headers, status code, etc,  will throw an exception.</span></span> <span data-ttu-id="b7b0a-138">`next`를 호출한 후 응답 본문에 작성:</span><span class="sxs-lookup"><span data-stu-id="b7b0a-138">Writing to the response body after calling `next`:</span></span>
> - <span data-ttu-id="b7b0a-139">프로토콜 위반이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-139">May cause a protocol violation.</span></span> <span data-ttu-id="b7b0a-140">예를 들어 언급된 `content-length`보다 더 많은 작성</span><span class="sxs-lookup"><span data-stu-id="b7b0a-140">For example, writing more than the stated `content-length`.</span></span>
> - <span data-ttu-id="b7b0a-141">본문 형식을 손상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-141">May corrupt the body format.</span></span> <span data-ttu-id="b7b0a-142">예를 들어 CSS 파일에 HTML 바닥글 작성</span><span class="sxs-lookup"><span data-stu-id="b7b0a-142">For example, writing an HTML footer to a CSS file.</span></span>
>
> <span data-ttu-id="b7b0a-143">[HttpResponse.HasStarted](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.features.httpresponsefeature#Microsoft_AspNetCore_Http_Features_HttpResponseFeature_HasStarted)는 헤더가 전송되고 또는 본문이 작성되었는지 나타내는 데 유용한 힌트입니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-143">[HttpResponse.HasStarted](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.features.httpresponsefeature#Microsoft_AspNetCore_Http_Features_HttpResponseFeature_HasStarted) is a useful hint to indicate if headers have been sent and/or the body has been written to.</span></span>

## <a name="ordering"></a><span data-ttu-id="b7b0a-144">정렬</span><span class="sxs-lookup"><span data-stu-id="b7b0a-144">Ordering</span></span>

<span data-ttu-id="b7b0a-145">미들웨어 구성 요소가 `Configure` 메서드에 추가되는 순서는 요청에서 호출되는 순서와 응답에 대한 역순서를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-145">The order that middleware components are added in the `Configure` method defines the order in which they're invoked on requests, and the reverse order for the response.</span></span> <span data-ttu-id="b7b0a-146">이 순서 지정은 보안, 성능 및 기능에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-146">This ordering is critical for security, performance, and functionality.</span></span>

<span data-ttu-id="b7b0a-147">Configure 메서드(아래 참조)는 다음 미들웨어 구성 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-147">The Configure method (shown below) adds the following middleware components:</span></span>

1. <span data-ttu-id="b7b0a-148">예외/오류 처리</span><span class="sxs-lookup"><span data-stu-id="b7b0a-148">Exception/error handling</span></span>
2. <span data-ttu-id="b7b0a-149">정적 파일 서버</span><span class="sxs-lookup"><span data-stu-id="b7b0a-149">Static file server</span></span>
3. <span data-ttu-id="b7b0a-150">인증</span><span class="sxs-lookup"><span data-stu-id="b7b0a-150">Authentication</span></span>
4. <span data-ttu-id="b7b0a-151">MVC</span><span class="sxs-lookup"><span data-stu-id="b7b0a-151">MVC</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b7b0a-152">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b7b0a-152">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)


```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseExceptionHandler("/Home/Error"); // Call first to catch exceptions
                                            // thrown in the following middleware.

    app.UseStaticFiles();                   // Return static files and end pipeline.

    app.UseAuthentication();               // Authenticate before you access
                                           // secure resources.

    app.UseMvcWithDefaultRoute();          // Add MVC to the request pipeline.
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b7b0a-153">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b7b0a-153">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseExceptionHandler("/Home/Error"); // Call first to catch exceptions
                                            // thrown in the following middleware.

    app.UseStaticFiles();                   // Return static files and end pipeline.

    app.UseIdentity();                     // Authenticate before you access
                                           // secure resources.

    app.UseMvcWithDefaultRoute();          // Add MVC to the request pipeline.
}
```

-----------

<span data-ttu-id="b7b0a-154">위의 코드에서 `UseExceptionHandler`는 파이프라인에 추가된 첫 번째 미들웨어 구성 요소이므로 후속 호출에서 발생하는 모든 예외를 catch합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-154">In the code above, `UseExceptionHandler` is the first middleware component added to the pipeline—therefore, it catches any exceptions that occur in later calls.</span></span>

<span data-ttu-id="b7b0a-155">정적 파일 미들웨어는 파이프라인 초기에 호출되므로 요청을 처리하고 나머지 구성 요소를 통과하지 않고 단락(short-circuit)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-155">The static file middleware is called early in the pipeline so it can handle requests and short-circuit without going through the remaining components.</span></span> <span data-ttu-id="b7b0a-156">정적 파일 미들웨어는 권한 부여 검사를 제공하지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-156">The static file middleware provides **no** authorization checks.</span></span> <span data-ttu-id="b7b0a-157">*wwwroot* 아래의 항목을 비롯한 제공되는 모든 파일은 공개적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-157">Any files served by it, including those under *wwwroot*, are publicly available.</span></span> <span data-ttu-id="b7b0a-158">정적 파일을 보호하는 방법은 [정적 파일 작업](xref:fundamentals/static-files)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-158">See [Working with static files](xref:fundamentals/static-files) for an approach to secure static files.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b7b0a-159">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b7b0a-159">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)


<span data-ttu-id="b7b0a-160">요청이 정적 파일 미들웨어에서 처리되지 않는 경우 인증을 수행하는 ID 미들웨어(`app.UseAuthentication`)로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-160">If the request isn't handled by the static file middleware, it's passed on to the Identity middleware (`app.UseAuthentication`), which performs authentication.</span></span> <span data-ttu-id="b7b0a-161">ID는 인증되지 않은 요청을 단락(short-circuit)하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-161">Identity doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="b7b0a-162">ID가 요청을 인증하지만 MVC가 특정 Razor 페이지 또는 컨트롤러 및 작업을 선택한 후에만 권한 부여(및 거부)가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-162">Although Identity authenticates requests,  authorization (and rejection) occurs only after MVC selects a specific Razor Page or controller and action.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b7b0a-163">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b7b0a-163">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b7b0a-164">요청이 정적 파일 미들웨어에서 처리되지 않는 경우 인증을 수행하는 ID 미들웨어(`app.UseIdentity`)로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-164">If the request isn't handled by the static file middleware, it's passed on to the Identity middleware (`app.UseIdentity`), which performs authentication.</span></span> <span data-ttu-id="b7b0a-165">ID는 인증되지 않은 요청을 단락(short-circuit)하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-165">Identity doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="b7b0a-166">ID가 요청을 인증하지만 MVC가 특정 컨트롤러 및 작업을 선택한 후에만 권한 부여(및 거부)가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-166">Although Identity authenticates requests,  authorization (and rejection) occurs only after MVC selects a specific controller and action.</span></span>

-----------

<span data-ttu-id="b7b0a-167">다음 예제는 정적 파일에 대한 요청이 응답 압축 미들웨어 전에 정적 파일 미들웨어에서 처리되는 미들웨어 순서를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-167">The following example demonstrates a middleware ordering where requests for static files are handled by the static file middleware before the response compression middleware.</span></span> <span data-ttu-id="b7b0a-168">정적 파일은 이 미들웨어의 순서로 압축되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-168">Static files are not compressed with this ordering of the middleware.</span></span> <span data-ttu-id="b7b0a-169">[UseMvcWithDefaultRoute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_)의 MVC 응답은 압축될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-169">The MVC responses from [UseMvcWithDefaultRoute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) can be compressed.</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseStaticFiles();         // Static files not compressed
                                  // by middleware.
    app.UseResponseCompression();
    app.UseMvcWithDefaultRoute();
}
```

<a name="middleware-run-map-use"></a>

### <a name="use-run-and-map"></a><span data-ttu-id="b7b0a-170">Use, Run 및 Map</span><span class="sxs-lookup"><span data-stu-id="b7b0a-170">Use, Run, and Map</span></span>

<span data-ttu-id="b7b0a-171">`Use`, `Run` 및 `Map`을 사용하여 HTTP 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-171">You configure the HTTP pipeline using `Use`, `Run`, and `Map`.</span></span> <span data-ttu-id="b7b0a-172">`Use` 메서드는 파이프라인을 단락(short-circuit)할 수 있습니다(즉, `next` 요청 대리자를 호출하지 않는 경우).</span><span class="sxs-lookup"><span data-stu-id="b7b0a-172">The `Use` method can short-circuit the pipeline (that is, if it doesn't call a `next` request delegate).</span></span> <span data-ttu-id="b7b0a-173">`Run`은 규칙이며 일부 미들웨어 구성 요소는 파이프라인의 끝에서 실행되는 `Run[Middleware]` 메서드를 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-173">`Run` is a convention, and some middleware components may expose `Run[Middleware]` methods that run at the end of the pipeline.</span></span>

<span data-ttu-id="b7b0a-174">`Map*` 확장은 파이프라인 분기에 규칙으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-174">`Map*` extensions are used as a convention for branching the pipeline.</span></span> <span data-ttu-id="b7b0a-175">[Map](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapextensions)은 지정된 요청 경로의 일치를 기반으로 요청 파이프라인을 분기합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-175">[Map](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapextensions) branches the request pipeline based on matches of the given request path.</span></span> <span data-ttu-id="b7b0a-176">요청 경로가 지정된 경로로 시작하는 경우 분기가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-176">If the request path starts with the given path, the branch is executed.</span></span>

[!code-csharp[Main](index/sample/Chain/StartupMap.cs?name=snippet1)]

<span data-ttu-id="b7b0a-177">다음 표는 앞의 코드를 사용하여 `http://localhost:1234`의 요청 및 응답을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-177">The following table shows the requests and responses from `http://localhost:1234` using the previous code:</span></span>

| <span data-ttu-id="b7b0a-178">요청</span><span class="sxs-lookup"><span data-stu-id="b7b0a-178">Request</span></span> | <span data-ttu-id="b7b0a-179">응답</span><span class="sxs-lookup"><span data-stu-id="b7b0a-179">Response</span></span> |
| --- | --- |
| <span data-ttu-id="b7b0a-180">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="b7b0a-180">localhost:1234</span></span> | <span data-ttu-id="b7b0a-181">비 Map 대리자에서 Hello</span><span class="sxs-lookup"><span data-stu-id="b7b0a-181">Hello from non-Map delegate.</span></span>  |
| <span data-ttu-id="b7b0a-182">localhost:1234/map1</span><span class="sxs-lookup"><span data-stu-id="b7b0a-182">localhost:1234/map1</span></span> | <span data-ttu-id="b7b0a-183">맵 테스트 1</span><span class="sxs-lookup"><span data-stu-id="b7b0a-183">Map Test 1</span></span> |
| <span data-ttu-id="b7b0a-184">localhost:1234/map2</span><span class="sxs-lookup"><span data-stu-id="b7b0a-184">localhost:1234/map2</span></span> | <span data-ttu-id="b7b0a-185">맵 테스트 2</span><span class="sxs-lookup"><span data-stu-id="b7b0a-185">Map Test 2</span></span> |
| <span data-ttu-id="b7b0a-186">localhost:1234/map3</span><span class="sxs-lookup"><span data-stu-id="b7b0a-186">localhost:1234/map3</span></span> | <span data-ttu-id="b7b0a-187">비 Map 대리자에서 Hello</span><span class="sxs-lookup"><span data-stu-id="b7b0a-187">Hello from non-Map delegate.</span></span>  |

<span data-ttu-id="b7b0a-188">`Map`이 사용되는 경우 일치하는 경로 세그먼트는 `HttpRequest.Path`에서 제거되고 각 요청에 대해 `HttpRequest.PathBase`에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-188">When `Map` is used, the matched path segment(s) are removed from `HttpRequest.Path` and appended to `HttpRequest.PathBase` for each request.</span></span>

<span data-ttu-id="b7b0a-189">[MapWhen](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapwhenextensions)은 지정된 조건자의 결과를 기반으로 요청 파이프라인을 분기합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-189">[MapWhen](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapwhenextensions) branches the request pipeline based on the result of the given predicate.</span></span> <span data-ttu-id="b7b0a-190">`Func<HttpContext, bool>` 형식의 조건자는 파이프라인의 새 분기에 요청을 매핑하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-190">Any predicate of type `Func<HttpContext, bool>` can be used to map requests to a new branch of the pipeline.</span></span> <span data-ttu-id="b7b0a-191">다음 예제에서 조건자는 쿼리 문자열 변수 `branch`의 존재를 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-191">In the following example, a predicate is used to detect the presence of a query string variable `branch`:</span></span>

[!code-csharp[Main](index/sample/Chain/StartupMapWhen.cs?name=snippet1)]

<span data-ttu-id="b7b0a-192">다음 표는 앞의 코드를 사용하여 `http://localhost:1234`의 요청 및 응답을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-192">The following table shows the requests and responses from `http://localhost:1234` using the previous code:</span></span>

| <span data-ttu-id="b7b0a-193">요청</span><span class="sxs-lookup"><span data-stu-id="b7b0a-193">Request</span></span> | <span data-ttu-id="b7b0a-194">응답</span><span class="sxs-lookup"><span data-stu-id="b7b0a-194">Response</span></span> |
| --- | --- |
| <span data-ttu-id="b7b0a-195">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="b7b0a-195">localhost:1234</span></span> | <span data-ttu-id="b7b0a-196">비 Map 대리자에서 Hello</span><span class="sxs-lookup"><span data-stu-id="b7b0a-196">Hello from non-Map delegate.</span></span>  |
| <span data-ttu-id="b7b0a-197">localhost:1234/?branch=master</span><span class="sxs-lookup"><span data-stu-id="b7b0a-197">localhost:1234/?branch=master</span></span> | <span data-ttu-id="b7b0a-198">사용되는 분기 = 마스터</span><span class="sxs-lookup"><span data-stu-id="b7b0a-198">Branch used = master</span></span>|

<span data-ttu-id="b7b0a-199">`Map`은 중첩을 지원합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-199">`Map` supports nesting, for example:</span></span>

```csharp
app.Map("/level1", level1App => {
       level1App.Map("/level2a", level2AApp => {
           // "/level1/level2a"
           //...
       });
       level1App.Map("/level2b", level2BApp => {
           // "/level1/level2b"
           //...
       });
   });
   ```

<span data-ttu-id="b7b0a-200">`Map`은 여러 세그먼트를 한 번에 일치시킬 수도 있습니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-200">`Map` can also match multiple segments at once, for example:</span></span>

 ```csharp
app.Map("/level1/level2", HandleMultiSeg);
```

## <a name="built-in-middleware"></a><span data-ttu-id="b7b0a-201">기본 제공 미들웨어</span><span class="sxs-lookup"><span data-stu-id="b7b0a-201">Built-in middleware</span></span>

<span data-ttu-id="b7b0a-202">ASP.NET Core는 다음 미들웨어 구성 요소 및 추가되어야 하는 순서에 대한 설명과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-202">ASP.NET Core ships with the following middleware components, as well as a description of the order in which they should be added:</span></span>

| <span data-ttu-id="b7b0a-203">미들웨어</span><span class="sxs-lookup"><span data-stu-id="b7b0a-203">Middleware</span></span> | <span data-ttu-id="b7b0a-204">설명</span><span class="sxs-lookup"><span data-stu-id="b7b0a-204">Description</span></span> | <span data-ttu-id="b7b0a-205">순서</span><span class="sxs-lookup"><span data-stu-id="b7b0a-205">Order</span></span> |
| ---------- | ----------- | ----- |
| [<span data-ttu-id="b7b0a-206">인증</span><span class="sxs-lookup"><span data-stu-id="b7b0a-206">Authentication</span></span>](xref:security/authentication/identity) | <span data-ttu-id="b7b0a-207">인증 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-207">Provides authentication support.</span></span> | <span data-ttu-id="b7b0a-208">이전에 `HttpContext.User`가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-208">Before `HttpContext.User` is needed.</span></span> <span data-ttu-id="b7b0a-209">OAuth에 대한 터미널이 콜백합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-209">Terminal for OAuth callbacks.</span></span> |
| [<span data-ttu-id="b7b0a-210">CORS</span><span class="sxs-lookup"><span data-stu-id="b7b0a-210">CORS</span></span>](xref:security/cors) | <span data-ttu-id="b7b0a-211">원본 간 리소스 공유를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-211">Configures Cross-Origin Resource Sharing.</span></span> | <span data-ttu-id="b7b0a-212">CORS를 사용하는 구성 요소 이전</span><span class="sxs-lookup"><span data-stu-id="b7b0a-212">Before components that use CORS.</span></span> |
| [<span data-ttu-id="b7b0a-213">진단</span><span class="sxs-lookup"><span data-stu-id="b7b0a-213">Diagnostics</span></span>](xref:fundamentals/error-handling) | <span data-ttu-id="b7b0a-214">진단을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-214">Configures diagnostics.</span></span> | <span data-ttu-id="b7b0a-215">오류를 생성하는 구성 요소 이전</span><span class="sxs-lookup"><span data-stu-id="b7b0a-215">Before components that generate errors.</span></span> |
| [<span data-ttu-id="b7b0a-216">ForwardedHeaders/HttpOverrides</span><span class="sxs-lookup"><span data-stu-id="b7b0a-216">ForwardedHeaders/HttpOverrides</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions) | <span data-ttu-id="b7b0a-217">프록시된 헤더를 현재 요청에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-217">Forwards proxied headers onto the current request.</span></span> | <span data-ttu-id="b7b0a-218">업데이트된 필드를 사용하는 구성 요소 이전(예: 체계, 호스트, ClientIP, 메서드)</span><span class="sxs-lookup"><span data-stu-id="b7b0a-218">Before components that consume the updated fields (examples: Scheme, Host, ClientIP, Method).</span></span> |
| [<span data-ttu-id="b7b0a-219">응답 캐싱</span><span class="sxs-lookup"><span data-stu-id="b7b0a-219">Response Caching</span></span>](xref:performance/caching/middleware) | <span data-ttu-id="b7b0a-220">응답 캐시에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-220">Provides support for caching responses.</span></span> | <span data-ttu-id="b7b0a-221">캐싱이 필요한 구성 요소 이전</span><span class="sxs-lookup"><span data-stu-id="b7b0a-221">Before components that require caching.</span></span> |
| [<span data-ttu-id="b7b0a-222">응답 압축</span><span class="sxs-lookup"><span data-stu-id="b7b0a-222">Response Compression</span></span>](xref:performance/response-compression) | <span data-ttu-id="b7b0a-223">응답 압축에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-223">Provides support for compressing responses.</span></span> | <span data-ttu-id="b7b0a-224">압축이 필요한 구성 요소 이전</span><span class="sxs-lookup"><span data-stu-id="b7b0a-224">Before components that require compression.</span></span> |
| [<span data-ttu-id="b7b0a-225">RequestLocalization</span><span class="sxs-lookup"><span data-stu-id="b7b0a-225">RequestLocalization</span></span>](xref:fundamentals/localization) | <span data-ttu-id="b7b0a-226">지역화 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-226">Provides localization support.</span></span> | <span data-ttu-id="b7b0a-227">지역화 구분 구성 요소 이전</span><span class="sxs-lookup"><span data-stu-id="b7b0a-227">Before localization sensitive components.</span></span> |
| [<span data-ttu-id="b7b0a-228">라우팅</span><span class="sxs-lookup"><span data-stu-id="b7b0a-228">Routing</span></span>](xref:fundamentals/routing) | <span data-ttu-id="b7b0a-229">요청 경로를 정의하고 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-229">Defines and constrains request routes.</span></span> | <span data-ttu-id="b7b0a-230">경로 일치에 대한 터미널</span><span class="sxs-lookup"><span data-stu-id="b7b0a-230">Terminal for matching routes.</span></span> |
| [<span data-ttu-id="b7b0a-231">세션</span><span class="sxs-lookup"><span data-stu-id="b7b0a-231">Session</span></span>](xref:fundamentals/app-state) | <span data-ttu-id="b7b0a-232">사용자 세션 관리에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-232">Provides support for managing user sessions.</span></span> | <span data-ttu-id="b7b0a-233">세션이 필요한 구성 요소 이전</span><span class="sxs-lookup"><span data-stu-id="b7b0a-233">Before components that require Session.</span></span> |
| [<span data-ttu-id="b7b0a-234">정적 파일</span><span class="sxs-lookup"><span data-stu-id="b7b0a-234">Static Files</span></span>](xref:fundamentals/static-files) | <span data-ttu-id="b7b0a-235">정적 파일 및 디렉터리 검색 처리에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-235">Provides support for serving static files and directory browsing.</span></span> | <span data-ttu-id="b7b0a-236">요청이 파일과 일치하는 경우 터미널</span><span class="sxs-lookup"><span data-stu-id="b7b0a-236">Terminal if a request matches files.</span></span> |
| [<span data-ttu-id="b7b0a-237">URL 재작성</span><span class="sxs-lookup"><span data-stu-id="b7b0a-237">URL Rewriting </span></span>](xref:fundamentals/url-rewriting) | <span data-ttu-id="b7b0a-238">URL 재작성 및 요청 리디렉션에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-238">Provides support for rewriting URLs and redirecting requests.</span></span> | <span data-ttu-id="b7b0a-239">URL을 사용하는 구성 요소 이전</span><span class="sxs-lookup"><span data-stu-id="b7b0a-239">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="b7b0a-240">WebSockets</span><span class="sxs-lookup"><span data-stu-id="b7b0a-240">WebSockets</span></span>](xref:fundamentals/websockets) | <span data-ttu-id="b7b0a-241">WebSocket 프로토콜을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-241">Enables the WebSockets protocol.</span></span> | <span data-ttu-id="b7b0a-242">WebSocket 요청을 수락하는 데 필요한 구성 요소 이전</span><span class="sxs-lookup"><span data-stu-id="b7b0a-242">Before components that are required to accept WebSocket requests.</span></span> |

<a name="middleware-writing-middleware"></a>

## <a name="writing-middleware"></a><span data-ttu-id="b7b0a-243">미들웨어 작성</span><span class="sxs-lookup"><span data-stu-id="b7b0a-243">Writing middleware</span></span>

<span data-ttu-id="b7b0a-244">미들웨어는 일반적으로 클래스에서 캡슐화되고 확장 메서드로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-244">Middleware is generally encapsulated in a class and exposed with an extension method.</span></span> <span data-ttu-id="b7b0a-245">쿼리 문자열에서 현재 요청에 대한 문화권을 설정하는 다음 미들웨어를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-245">Consider the following middleware, which sets the culture for the current request from the query string:</span></span>

[!code-csharp[Main](index/sample/Culture/StartupCulture.cs?name=snippet1)]

<span data-ttu-id="b7b0a-246">참고: 위의 샘플 코드는 미들웨어 구성 요소 만들기를 보여 주는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-246">Note: The sample code above is used to demonstrate creating a middleware component.</span></span> <span data-ttu-id="b7b0a-247">ASP.NET Core의 기본 제공 지역화 지원은 [전역화 및 지역화](xref:fundamentals/localization)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-247">See [ Globalization and localization](xref:fundamentals/localization) for ASP.NET Core's built-in localization support.</span></span>

<span data-ttu-id="b7b0a-248">문화권을 전달하여 미들웨어를 테스트할 수 있습니다(예: `http://localhost:7997/?culture=no`).</span><span class="sxs-lookup"><span data-stu-id="b7b0a-248">You can test the middleware by passing in the culture, for example `http://localhost:7997/?culture=no`.</span></span>

<span data-ttu-id="b7b0a-249">다음 코드는 미들웨어 대리자를 클래스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-249">The following code moves the middleware delegate to a class:</span></span>

[!code-csharp[Main](index/sample/Culture/RequestCultureMiddleware.cs)]

<span data-ttu-id="b7b0a-250">다음 확장 메서드는 [IApplicationBuilder](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.iapplicationbuilder)를 통해 미들웨어를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-250">The following extension method exposes the middleware through [IApplicationBuilder](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.iapplicationbuilder):</span></span>

[!code-csharp[Main](index/sample/Culture/RequestCultureMiddlewareExtensions.cs)]

<span data-ttu-id="b7b0a-251">다음 코드는 `Configure`에서 미들웨어를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-251">The following code calls the middleware from `Configure`:</span></span>

[!code-csharp[Main](index/sample/Culture/Startup.cs?name=snippet1&highlight=5)]

<span data-ttu-id="b7b0a-252">미들웨어는 해당 생성자에서 해당 종속성을 노출하여 [명시적 종속성 원칙](http://deviq.com/explicit-dependencies-principle/)을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-252">Middleware should follow the [Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/) by exposing its dependencies in its constructor.</span></span> <span data-ttu-id="b7b0a-253">미들웨어는 *응용 프로그램 수명*당 한 번 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-253">Middleware is constructed once per *application lifetime*.</span></span> <span data-ttu-id="b7b0a-254">서비스를 요청 내의 미들웨어와 공유해야 하는 경우 아래 *요청당 종속성*을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-254">See *Per-request dependencies* below if you need to share services with middleware within a request.</span></span>

<span data-ttu-id="b7b0a-255">미들웨어 구성 요소는 생성자 매개 변수를 통해 종속성 주입에서 해당 종속성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-255">Middleware components can resolve their dependencies from dependency injection through constructor parameters.</span></span> <span data-ttu-id="b7b0a-256">[`UseMiddleware<T>`](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.usemiddlewareextensions#methods_summary)는 추가 매개 변수를 직접 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-256">[`UseMiddleware<T>`](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.usemiddlewareextensions#methods_summary) can also accept additional parameters directly.</span></span>

### <a name="per-request-dependencies"></a><span data-ttu-id="b7b0a-257">요청당 종속성</span><span class="sxs-lookup"><span data-stu-id="b7b0a-257">Per-request dependencies</span></span>

<span data-ttu-id="b7b0a-258">미들웨어는 요청당이 아닌 앱 시작 시 생성되므로 미들웨어 생성자에 의해 사용되는 *범위가 지정된* 수명 서비스는 각 요청 동안 다른 종속성 주입된 형식과 공유되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-258">Because middleware is constructed at app startup, not per-request, *scoped* lifetime services used by middleware constructors are not  shared with other dependency-injected types during each request.</span></span> <span data-ttu-id="b7b0a-259">*범위가 지정된* 서비스를 미들웨어와 다른 형식 간에 공유해야 하는 경우 이러한 서비스를 `Invoke` 메서드의 서명에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-259">If you must share a *scoped* service between your middleware and other types, add these services to the `Invoke` method's signature.</span></span> <span data-ttu-id="b7b0a-260">`Invoke` 메서드는 종속성 주입으로 채워지는 추가 매개 변수를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7b0a-260">The `Invoke` method can accept additional parameters that are populated by dependency injection.</span></span> <span data-ttu-id="b7b0a-261">예:</span><span class="sxs-lookup"><span data-stu-id="b7b0a-261">For example:</span></span>

```c#
public class MyMiddleware
{
    private readonly RequestDelegate _next;

    public MyMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task Invoke(HttpContext httpContext, IMyScopedService svc)
    {
        svc.MyProperty = 1000;
        await _next(httpContext);
    }
}
```

## <a name="additional-resources"></a><span data-ttu-id="b7b0a-262">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b7b0a-262">Additional resources</span></span>

* [<span data-ttu-id="b7b0a-263">HTTP 모듈을 미들웨어로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="b7b0a-263">Migrating HTTP Modules to Middleware</span></span>](xref:migration/http-modules)
* [<span data-ttu-id="b7b0a-264">응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="b7b0a-264">Application Startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="b7b0a-265">기능 요청</span><span class="sxs-lookup"><span data-stu-id="b7b0a-265">Request Features</span></span>](xref:fundamentals/request-features)
* [<span data-ttu-id="b7b0a-266">팩터리 기반 미들웨어 활성화</span><span class="sxs-lookup"><span data-stu-id="b7b0a-266">Factory-based middleware activation</span></span>](xref:fundamentals/middleware/extensibility)
