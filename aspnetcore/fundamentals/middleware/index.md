---
title: ASP.NET Core 미들웨어 기본 사항
author: rick-anderson
description: ASP.NET Core 미들웨어 및 요청 파이프라인에 대해 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 01/22/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/middleware/index
ms.openlocfilehash: c6d362cf15b5d4611f0e544c5092a18f32ed7dfc
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34819047"
---
# <a name="aspnet-core-middleware"></a><span data-ttu-id="5bd9e-103">ASP.NET Core 미들웨어</span><span class="sxs-lookup"><span data-stu-id="5bd9e-103">ASP.NET Core Middleware</span></span>

<span data-ttu-id="5bd9e-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="5bd9e-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="5bd9e-105">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/index/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="5bd9e-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/index/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="what-is-middleware"></a><span data-ttu-id="5bd9e-106">미들웨어란?</span><span class="sxs-lookup"><span data-stu-id="5bd9e-106">What is middleware?</span></span>

<span data-ttu-id="5bd9e-107">미들웨어는 요청 및 응답을 처리하는 응용 프로그램 파이프라인으로 어셈블리되는 소프트웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-107">Middleware is software that's assembled into an application pipeline to handle requests and responses.</span></span> <span data-ttu-id="5bd9e-108">각 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="5bd9e-108">Each component:</span></span>

* <span data-ttu-id="5bd9e-109">요청을 파이프라인의 다음 구성 요소로 전달할지 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-109">Chooses whether to pass the request to the next component in the pipeline.</span></span>
* <span data-ttu-id="5bd9e-110">파이프라인의 다음 구성 요소가 호출되기 전과 후에 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-110">Can perform work before and after the next component in the pipeline is invoked.</span></span> 

<span data-ttu-id="5bd9e-111">요청 대리자는 요청 파이프라인을 빌드하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-111">Request delegates are used to build the request pipeline.</span></span> <span data-ttu-id="5bd9e-112">요청 대리자는 각 HTTP 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-112">The request delegates handle each HTTP request.</span></span>

<span data-ttu-id="5bd9e-113">요청 대리자는 [Run](/dotnet/api/microsoft.aspnetcore.builder.runextensions), [Map](/dotnet/api/microsoft.aspnetcore.builder.mapextensions) 및 [Use](/dotnet/api/microsoft.aspnetcore.builder.useextensions) 확장 메서드를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-113">Request delegates are configured using [Run](/dotnet/api/microsoft.aspnetcore.builder.runextensions), [Map](/dotnet/api/microsoft.aspnetcore.builder.mapextensions), and [Use](/dotnet/api/microsoft.aspnetcore.builder.useextensions) extension methods.</span></span> <span data-ttu-id="5bd9e-114">개별 요청 대리자는 무명 메서드(인라인 미들웨어라고 함)로 인라인에서 지정되거나 다시 사용할 수 있는 클래스에서 정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-114">An individual request delegate can be specified in-line as an anonymous method (called in-line middleware), or it can be defined in a reusable class.</span></span> <span data-ttu-id="5bd9e-115">이러한 다시 사용할 수 있는 클래스 및 인라인 무명 메서드는 *미들웨어* 또는 *미들웨어 구성 요소*입니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-115">These reusable classes and in-line anonymous methods are *middleware*, or *middleware components*.</span></span> <span data-ttu-id="5bd9e-116">요청 파이프라인의 각 미들웨어 구성 요소는 파이프라인의 다음 구성 요소를 호출하거나 적절한 경우 체인을 단락(short-circuiting)하는 일을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-116">Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline, or short-circuiting the chain if appropriate.</span></span>

<span data-ttu-id="5bd9e-117">[HTTP 모듈을 미들웨어로 마이그레이션](xref:migration/http-modules)은 ASP.NET Core와 ASP.NET 4.x의 요청 파이프라인 간의 차이점을 설명하고 더 많은 미들웨어 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-117">[Migrate HTTP Modules to Middleware](xref:migration/http-modules) explains the difference between request pipelines in ASP.NET Core and ASP.NET 4.x and provides more middleware samples.</span></span>

## <a name="creating-a-middleware-pipeline-with-iapplicationbuilder"></a><span data-ttu-id="5bd9e-118">IApplicationBuilder로 미들웨어 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="5bd9e-118">Creating a middleware pipeline with IApplicationBuilder</span></span>

<span data-ttu-id="5bd9e-119">ASP.NET Core 요청 파이프라인은 이 다이어그램이 보여 주는 것과 같이 차례로 호출되는 요청 대리자의 시퀀스로 구성됩니다(실행의 스레드는 검은색 화살표를 따름).</span><span class="sxs-lookup"><span data-stu-id="5bd9e-119">The ASP.NET Core request pipeline consists of a sequence of request delegates, called one after the other, as this diagram shows (the thread of execution follows the black arrows):</span></span>

![요청 수신을 표시하고, 세 가지 미들웨어를 통해 처리하는 요청 처리 패턴 및 응용 프로그램을 나가는 응답](index/_static/request-delegate-pipeline.png)

<span data-ttu-id="5bd9e-123">각 대리자는 다음 대리자 전과 후에 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-123">Each delegate can perform operations before and after the next delegate.</span></span> <span data-ttu-id="5bd9e-124">또한 대리자는 다음 대리자에 요청을 전달하지 않도록 결정할 수 있습니다. 이를 요청 파이프라인을 단락(short-circuiting)한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-124">A delegate can also decide to not pass a request to the next delegate, which is called short-circuiting the request pipeline.</span></span> <span data-ttu-id="5bd9e-125">단락(short-circuiting)은 불필요한 작업을 방지하기 때문에 보통 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-125">Short-circuiting is often desirable because it avoids unnecessary work.</span></span> <span data-ttu-id="5bd9e-126">예를 들어 정적 파일 미들웨어는 정적 파일에 대한 요청을 반환하고 나머지 파이프라인을 단락(short-circuit)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-126">For example, the static file middleware can return a request for a static file and short-circuit the rest of the pipeline.</span></span> <span data-ttu-id="5bd9e-127">예외 처리 대리자는 파이프라인의 이후 단계에서 발생하는 예외를 catch할 수 있도록 파이프라인의 초기에 호출되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-127">Exception-handling delegates need to be called early in the pipeline, so they can catch exceptions that occur in later stages of the pipeline.</span></span>

<span data-ttu-id="5bd9e-128">가장 간단한 가능한 ASP.NET Core 앱은 모든 요청을 처리하는 단일 요청 대리자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-128">The simplest possible ASP.NET Core app sets up a single request delegate that handles all requests.</span></span> <span data-ttu-id="5bd9e-129">이 경우 실제 요청 파이프라인은 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-129">This case doesn't include an actual request pipeline.</span></span> <span data-ttu-id="5bd9e-130">대신, 단일 익명 함수가 모든 HTTP 요청에 대한 응답에 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-130">Instead, a single anonymous function is called in response to every HTTP request.</span></span>

[!code-csharp[](index/sample/Middleware/Startup.cs)]

<span data-ttu-id="5bd9e-131">첫 번째 [app.Run](/dotnet/api/microsoft.aspnetcore.builder.runextensions) 대리자는 파이프라인을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-131">The first [app.Run](/dotnet/api/microsoft.aspnetcore.builder.runextensions) delegate terminates the pipeline.</span></span>

<span data-ttu-id="5bd9e-132">[app.Use](/dotnet/api/microsoft.aspnetcore.builder.useextensions)를 사용하여 여러 요청 대리자를 함께 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-132">You can chain multiple request delegates together with [app.Use](/dotnet/api/microsoft.aspnetcore.builder.useextensions).</span></span> <span data-ttu-id="5bd9e-133">`next` 매개 변수는 파이프라인의 다음 대리자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-133">The `next` parameter represents the next delegate in the pipeline.</span></span> <span data-ttu-id="5bd9e-134">(*next* 매개 변수를 호출하지 *않고* 파이프라인을 단락(short-circuit)할 수 있습니다.) 이 예제에서 설명하듯이 일반적으로 다음 대리자 전과 후 모두에서 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-134">(Remember that you can short-circuit the pipeline by *not* calling the *next* parameter.) You can typically perform actions both before and after the next delegate, as this example demonstrates:</span></span>

[!code-csharp[](index/sample/Chain/Startup.cs?name=snippet1)]

>[!WARNING]
> <span data-ttu-id="5bd9e-135">클라이언트에 응답을 전송한 후에 `next.Invoke`를 호출하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-135">Don't call `next.Invoke` after the response has been sent to the client.</span></span> <span data-ttu-id="5bd9e-136">응답이 시작된 후 `HttpResponse`로 변경하면 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-136">Changes to `HttpResponse` after the response has started will throw an exception.</span></span> <span data-ttu-id="5bd9e-137">예를 들어 헤더, 상태 코드 등을 설정하는 것 같은 변경은 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-137">For example, changes such as setting headers, status code, etc,  will throw an exception.</span></span> <span data-ttu-id="5bd9e-138">`next`를 호출한 후 응답 본문에 작성하기:</span><span class="sxs-lookup"><span data-stu-id="5bd9e-138">Writing to the response body after calling `next`:</span></span>
> - <span data-ttu-id="5bd9e-139">프로토콜 위반이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-139">May cause a protocol violation.</span></span> <span data-ttu-id="5bd9e-140">예를 들어, 명시된 `content-length`보다 긴 내용이 작성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-140">For example, writing more than the stated `content-length`.</span></span>
> - <span data-ttu-id="5bd9e-141">본문 형식을 손상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-141">May corrupt the body format.</span></span> <span data-ttu-id="5bd9e-142">예를 들어 CSS 파일에 HTML 바닥글 작성하기.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-142">For example, writing an HTML footer to a CSS file.</span></span>
>
> <span data-ttu-id="5bd9e-143">[HttpResponse.HasStarted](/dotnet/api/microsoft.aspnetcore.http.features.httpresponsefeature#Microsoft_AspNetCore_Http_Features_HttpResponseFeature_HasStarted)는 헤더가 이미 전송됐는지 또는 본문이 이미 작성됐는지 여부를 나타내는 유용한 힌트를 제공해줍니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-143">[HttpResponse.HasStarted](/dotnet/api/microsoft.aspnetcore.http.features.httpresponsefeature#Microsoft_AspNetCore_Http_Features_HttpResponseFeature_HasStarted) is a useful hint to indicate if headers have been sent and/or the body has been written to.</span></span>

## <a name="ordering"></a><span data-ttu-id="5bd9e-144">순서</span><span class="sxs-lookup"><span data-stu-id="5bd9e-144">Ordering</span></span>

<span data-ttu-id="5bd9e-145">미들웨어 구성 요소가 `Configure` 메서드에 추가되는 순서는 요청에서 호출되는 순서와 응답에 대한 역순서를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-145">The order that middleware components are added in the `Configure` method defines the order in which they're invoked on requests, and the reverse order for the response.</span></span> <span data-ttu-id="5bd9e-146">이 순서 지정은 보안, 성능 및 기능에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-146">This ordering is critical for security, performance, and functionality.</span></span>

<span data-ttu-id="5bd9e-147">Configure 메서드(아래 참조)는 다음 미들웨어 구성 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-147">The Configure method (shown below) adds the following middleware components:</span></span>

1. <span data-ttu-id="5bd9e-148">예외/오류 처리</span><span class="sxs-lookup"><span data-stu-id="5bd9e-148">Exception/error handling</span></span>
2. <span data-ttu-id="5bd9e-149">정적 파일 서버</span><span class="sxs-lookup"><span data-stu-id="5bd9e-149">Static file server</span></span>
3. <span data-ttu-id="5bd9e-150">인증</span><span class="sxs-lookup"><span data-stu-id="5bd9e-150">Authentication</span></span>
4. <span data-ttu-id="5bd9e-151">MVC</span><span class="sxs-lookup"><span data-stu-id="5bd9e-151">MVC</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="5bd9e-152">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="5bd9e-152">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)


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

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="5bd9e-153">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="5bd9e-153">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

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

<span data-ttu-id="5bd9e-154">위의 코드에서 `UseExceptionHandler`는 파이프라인에 추가된 첫 번째 미들웨어 구성 요소이므로 후속 호출에서 발생하는 모든 예외를 catch합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-154">In the code above, `UseExceptionHandler` is the first middleware component added to the pipeline—therefore, it catches any exceptions that occur in later calls.</span></span>

<span data-ttu-id="5bd9e-155">정적 파일 미들웨어는 파이프라인 초기에 호출되므로 요청을 처리하고 나머지 구성 요소를 통과하지 않고 단락(short-circuit)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-155">The static file middleware is called early in the pipeline so it can handle requests and short-circuit without going through the remaining components.</span></span> <span data-ttu-id="5bd9e-156">정적 파일 미들웨어는 권한 부여 검사를 제공하지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-156">The static file middleware provides **no** authorization checks.</span></span> <span data-ttu-id="5bd9e-157">*wwwroot* 아래의 항목을 비롯한 제공되는 모든 파일은 공개적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-157">Any files served by it, including those under *wwwroot*, are publicly available.</span></span> <span data-ttu-id="5bd9e-158">정적 파일을 보호하는 방법은 [정정 파일](xref:fundamentals/static-files)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-158">See [Static files](xref:fundamentals/static-files) for an approach to secure static files.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="5bd9e-159">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="5bd9e-159">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)


<span data-ttu-id="5bd9e-160">요청이 정적 파일 미들웨어에서 처리되지 않는 경우 인증을 수행하는 ID 미들웨어(`app.UseAuthentication`)로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-160">If the request isn't handled by the static file middleware, it's passed on to the Identity middleware (`app.UseAuthentication`), which performs authentication.</span></span> <span data-ttu-id="5bd9e-161">ID는 인증되지 않은 요청을 단락(short-circuit)하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-161">Identity doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="5bd9e-162">ID가 요청을 인증하지만 MVC가 특정 Razor 페이지 또는 컨트롤러 및 작업을 선택한 후에만 권한 부여(및 거부)가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-162">Although Identity authenticates requests,  authorization (and rejection) occurs only after MVC selects a specific Razor Page or controller and action.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="5bd9e-163">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="5bd9e-163">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="5bd9e-164">요청이 정적 파일 미들웨어에서 처리되지 않는 경우 인증을 수행하는 ID 미들웨어(`app.UseIdentity`)로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-164">If the request isn't handled by the static file middleware, it's passed on to the Identity middleware (`app.UseIdentity`), which performs authentication.</span></span> <span data-ttu-id="5bd9e-165">ID는 인증되지 않은 요청을 단락(short-circuit)하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-165">Identity doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="5bd9e-166">ID가 요청을 인증하지만 MVC가 특정 컨트롤러 및 작업을 선택한 후에만 권한 부여(및 거부)가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-166">Although Identity authenticates requests,  authorization (and rejection) occurs only after MVC selects a specific controller and action.</span></span>

-----------

<span data-ttu-id="5bd9e-167">다음 예제는 정적 파일에 대한 요청이 응답 압축 미들웨어 전에 정적 파일 미들웨어에서 처리되는 미들웨어 순서를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-167">The following example demonstrates a middleware ordering where requests for static files are handled by the static file middleware before the response compression middleware.</span></span> <span data-ttu-id="5bd9e-168">정적 파일은 이 미들웨어의 순서로 압축되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-168">Static files are not compressed with this ordering of the middleware.</span></span> <span data-ttu-id="5bd9e-169">[UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_)의 MVC 응답은 압축될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-169">The MVC responses from [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) can be compressed.</span></span>

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

### <a name="use-run-and-map"></a><span data-ttu-id="5bd9e-170">Use, Run 및 Map</span><span class="sxs-lookup"><span data-stu-id="5bd9e-170">Use, Run, and Map</span></span>

<span data-ttu-id="5bd9e-171">`Use`, `Run` 및 `Map`을 사용하여 HTTP 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-171">You configure the HTTP pipeline using `Use`, `Run`, and `Map`.</span></span> <span data-ttu-id="5bd9e-172">`Use` 메서드는 파이프라인을 단락(short-circuit)할 수 있습니다(즉, `next` 요청 대리자를 호출하지 않는 경우).</span><span class="sxs-lookup"><span data-stu-id="5bd9e-172">The `Use` method can short-circuit the pipeline (that is, if it doesn't call a `next` request delegate).</span></span> <span data-ttu-id="5bd9e-173">`Run`은 규칙이며 일부 미들웨어 구성 요소는 파이프라인의 끝에서 실행되는 `Run[Middleware]` 메서드를 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-173">`Run` is a convention, and some middleware components may expose `Run[Middleware]` methods that run at the end of the pipeline.</span></span>

<span data-ttu-id="5bd9e-174">`Map*` 확장은 파이프라인 분기에 규칙으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-174">`Map*` extensions are used as a convention for branching the pipeline.</span></span> <span data-ttu-id="5bd9e-175">[Map](/dotnet/api/microsoft.aspnetcore.builder.mapextensions)은 지정된 요청 경로의 일치를 기반으로 요청 파이프라인을 분기합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-175">[Map](/dotnet/api/microsoft.aspnetcore.builder.mapextensions) branches the request pipeline based on matches of the given request path.</span></span> <span data-ttu-id="5bd9e-176">요청 경로가 지정된 경로로 시작하는 경우 분기가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-176">If the request path starts with the given path, the branch is executed.</span></span>

[!code-csharp[](index/sample/Chain/StartupMap.cs?name=snippet1)]

<span data-ttu-id="5bd9e-177">다음 표는 앞의 코드를 사용하여 `http://localhost:1234`의 요청 및 응답을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-177">The following table shows the requests and responses from `http://localhost:1234` using the previous code:</span></span>

| <span data-ttu-id="5bd9e-178">요청</span><span class="sxs-lookup"><span data-stu-id="5bd9e-178">Request</span></span> | <span data-ttu-id="5bd9e-179">응답</span><span class="sxs-lookup"><span data-stu-id="5bd9e-179">Response</span></span> |
| --- | --- |
| <span data-ttu-id="5bd9e-180">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="5bd9e-180">localhost:1234</span></span> | <span data-ttu-id="5bd9e-181">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-181">Hello from non-Map delegate.</span></span>  |
| <span data-ttu-id="5bd9e-182">localhost:1234/map1</span><span class="sxs-lookup"><span data-stu-id="5bd9e-182">localhost:1234/map1</span></span> | <span data-ttu-id="5bd9e-183">Map Test 1</span><span class="sxs-lookup"><span data-stu-id="5bd9e-183">Map Test 1</span></span> |
| <span data-ttu-id="5bd9e-184">localhost:1234/map2</span><span class="sxs-lookup"><span data-stu-id="5bd9e-184">localhost:1234/map2</span></span> | <span data-ttu-id="5bd9e-185">Map Test 2</span><span class="sxs-lookup"><span data-stu-id="5bd9e-185">Map Test 2</span></span> |
| <span data-ttu-id="5bd9e-186">localhost:1234/map3</span><span class="sxs-lookup"><span data-stu-id="5bd9e-186">localhost:1234/map3</span></span> | <span data-ttu-id="5bd9e-187">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-187">Hello from non-Map delegate.</span></span>  |

<span data-ttu-id="5bd9e-188">`Map`이 사용되는 경우 일치하는 경로 세그먼트는 `HttpRequest.Path`에서 제거되고 각 요청에 대해 `HttpRequest.PathBase`에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-188">When `Map` is used, the matched path segment(s) are removed from `HttpRequest.Path` and appended to `HttpRequest.PathBase` for each request.</span></span>

<span data-ttu-id="5bd9e-189">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions)은 지정된 조건자의 결과를 기반으로 요청 파이프라인을 분기합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-189">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions) branches the request pipeline based on the result of the given predicate.</span></span> <span data-ttu-id="5bd9e-190">`Func<HttpContext, bool>` 형식의 조건자는 파이프라인의 새 분기에 요청을 매핑하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-190">Any predicate of type `Func<HttpContext, bool>` can be used to map requests to a new branch of the pipeline.</span></span> <span data-ttu-id="5bd9e-191">다음 예제에서 조건자는 쿼리 문자열 변수 `branch`의 존재를 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-191">In the following example, a predicate is used to detect the presence of a query string variable `branch`:</span></span>

[!code-csharp[](index/sample/Chain/StartupMapWhen.cs?name=snippet1)]

<span data-ttu-id="5bd9e-192">다음 표는 앞의 코드를 사용하여 `http://localhost:1234`의 요청 및 응답을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-192">The following table shows the requests and responses from `http://localhost:1234` using the previous code:</span></span>

| <span data-ttu-id="5bd9e-193">요청</span><span class="sxs-lookup"><span data-stu-id="5bd9e-193">Request</span></span> | <span data-ttu-id="5bd9e-194">응답</span><span class="sxs-lookup"><span data-stu-id="5bd9e-194">Response</span></span> |
| --- | --- |
| <span data-ttu-id="5bd9e-195">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="5bd9e-195">localhost:1234</span></span> | <span data-ttu-id="5bd9e-196">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-196">Hello from non-Map delegate.</span></span>  |
| <span data-ttu-id="5bd9e-197">localhost:1234/?branch=master</span><span class="sxs-lookup"><span data-stu-id="5bd9e-197">localhost:1234/?branch=master</span></span> | <span data-ttu-id="5bd9e-198">Branch used = master</span><span class="sxs-lookup"><span data-stu-id="5bd9e-198">Branch used = master</span></span>|

<span data-ttu-id="5bd9e-199">`Map`은 중첩을 지원합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-199">`Map` supports nesting, for example:</span></span>

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

<span data-ttu-id="5bd9e-200">`Map`은 여러 세그먼트를 한 번에 일치시킬 수도 있습니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-200">`Map` can also match multiple segments at once, for example:</span></span>

 ```csharp
app.Map("/level1/level2", HandleMultiSeg);
```

## <a name="built-in-middleware"></a><span data-ttu-id="5bd9e-201">기본 제공 미들웨어</span><span class="sxs-lookup"><span data-stu-id="5bd9e-201">Built-in middleware</span></span>

<span data-ttu-id="5bd9e-202">ASP.NET Core는 다음 미들웨어 구성 요소 및 추가되어야 하는 순서에 대한 설명과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-202">ASP.NET Core ships with the following middleware components, as well as a description of the order in which they should be added:</span></span>

| <span data-ttu-id="5bd9e-203">미들웨어</span><span class="sxs-lookup"><span data-stu-id="5bd9e-203">Middleware</span></span> | <span data-ttu-id="5bd9e-204">설명</span><span class="sxs-lookup"><span data-stu-id="5bd9e-204">Description</span></span> | <span data-ttu-id="5bd9e-205">순서</span><span class="sxs-lookup"><span data-stu-id="5bd9e-205">Order</span></span> |
| ---------- | ----------- | ----- |
| [<span data-ttu-id="5bd9e-206">인증</span><span class="sxs-lookup"><span data-stu-id="5bd9e-206">Authentication</span></span>](xref:security/authentication/identity) | <span data-ttu-id="5bd9e-207">인증 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-207">Provides authentication support.</span></span> | <span data-ttu-id="5bd9e-208">`HttpContext.User`가 필요하기 전에.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-208">Before `HttpContext.User` is needed.</span></span> <span data-ttu-id="5bd9e-209">OAuth 콜백에 대한 터미널.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-209">Terminal for OAuth callbacks.</span></span> |
| [<span data-ttu-id="5bd9e-210">CORS</span><span class="sxs-lookup"><span data-stu-id="5bd9e-210">CORS</span></span>](xref:security/cors) | <span data-ttu-id="5bd9e-211">원본 간 리소스 공유를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-211">Configures Cross-Origin Resource Sharing.</span></span> | <span data-ttu-id="5bd9e-212">CORS를 사용하는 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-212">Before components that use CORS.</span></span> |
| [<span data-ttu-id="5bd9e-213">진단</span><span class="sxs-lookup"><span data-stu-id="5bd9e-213">Diagnostics</span></span>](xref:fundamentals/error-handling) | <span data-ttu-id="5bd9e-214">진단을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-214">Configures diagnostics.</span></span> | <span data-ttu-id="5bd9e-215">오류를 생성하는 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-215">Before components that generate errors.</span></span> |
| [<span data-ttu-id="5bd9e-216">전달된 헤더</span><span class="sxs-lookup"><span data-stu-id="5bd9e-216">Forwarded Headers</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions) | <span data-ttu-id="5bd9e-217">프록시된 헤더를 현재 요청에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-217">Forwards proxied headers onto the current request.</span></span> | <span data-ttu-id="5bd9e-218">구성 요소가 업데이트된 필드를 사용하기 이전입니다(예: 체계, 호스트, 클라이언트 IP, 메서드).</span><span class="sxs-lookup"><span data-stu-id="5bd9e-218">Before components that consume the updated fields (examples: scheme, host, client IP, method).</span></span> |
| [<span data-ttu-id="5bd9e-219">HTTP 메서드 재정의</span><span class="sxs-lookup"><span data-stu-id="5bd9e-219">HTTP Method Override</span></span>](/dotnet/api/microsoft.aspnetcore.builder.httpmethodoverrideextensions) | <span data-ttu-id="5bd9e-220">들어오는 POST 요청이 메서드를 재정의하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-220">Allows an incoming POST request to override the method.</span></span> | <span data-ttu-id="5bd9e-221">업데이트된 메서드를 사용하는 구성 요소 앞입니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-221">Before components that consume the updated method.</span></span> |
| [<span data-ttu-id="5bd9e-222">HTTPS 리디렉션</span><span class="sxs-lookup"><span data-stu-id="5bd9e-222">HTTPS Redirection</span></span>](xref:security/enforcing-ssl#require-https) | <span data-ttu-id="5bd9e-223">HTTPS로 모든 HTTP 요청을 리디렉션합니다(ASP.NET Core 2.1 이상).</span><span class="sxs-lookup"><span data-stu-id="5bd9e-223">Redirect all HTTP requests to HTTPS (ASP.NET Core 2.1 or later).</span></span> | <span data-ttu-id="5bd9e-224">URL을 사용하는 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-224">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="5bd9e-225">HSTS(HTTP 엄격한 전송 보안)</span><span class="sxs-lookup"><span data-stu-id="5bd9e-225">HTTP Strict Transport Security (HSTS)</span></span>](xref:security/enforcing-ssl#http-strict-transport-security-protocol-hsts) | <span data-ttu-id="5bd9e-226">특별한 응답 헤더를 추가하는 보안 향상 미들웨어입니다(ASP.NET Core 2.1 이상).</span><span class="sxs-lookup"><span data-stu-id="5bd9e-226">Security enhancement middleware that adds a special response header (ASP.NET Core 2.1 or later).</span></span> | <span data-ttu-id="5bd9e-227">응답이 보내지기 이전 및 구성 요소가 요청을 수정한 이후입니다(예: 전달된 헤더, URL 다시 쓰기).</span><span class="sxs-lookup"><span data-stu-id="5bd9e-227">Before responses are sent and after components that modify requests (for example, Forwarded Headers, URL Rewriting).</span></span> |
| [<span data-ttu-id="5bd9e-228">응답 캐싱</span><span class="sxs-lookup"><span data-stu-id="5bd9e-228">Response Caching</span></span>](xref:performance/caching/middleware) | <span data-ttu-id="5bd9e-229">응답 캐시에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-229">Provides support for caching responses.</span></span> | <span data-ttu-id="5bd9e-230">캐싱이 필요한 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-230">Before components that require caching.</span></span> |
| [<span data-ttu-id="5bd9e-231">응답 압축</span><span class="sxs-lookup"><span data-stu-id="5bd9e-231">Response Compression</span></span>](xref:performance/response-compression) | <span data-ttu-id="5bd9e-232">응답 압축에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-232">Provides support for compressing responses.</span></span> | <span data-ttu-id="5bd9e-233">압축이 필요한 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-233">Before components that require compression.</span></span> |
| [<span data-ttu-id="5bd9e-234">요청 지역화</span><span class="sxs-lookup"><span data-stu-id="5bd9e-234">Request Localization</span></span>](xref:fundamentals/localization) | <span data-ttu-id="5bd9e-235">지역화 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-235">Provides localization support.</span></span> | <span data-ttu-id="5bd9e-236">지역화 구분 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-236">Before localization sensitive components.</span></span> |
| [<span data-ttu-id="5bd9e-237">라우팅</span><span class="sxs-lookup"><span data-stu-id="5bd9e-237">Routing</span></span>](xref:fundamentals/routing) | <span data-ttu-id="5bd9e-238">요청 경로를 정의하고 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-238">Defines and constrains request routes.</span></span> | <span data-ttu-id="5bd9e-239">경로 일치에 대한 터미널.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-239">Terminal for matching routes.</span></span> |
| [<span data-ttu-id="5bd9e-240">세션</span><span class="sxs-lookup"><span data-stu-id="5bd9e-240">Session</span></span>](xref:fundamentals/app-state) | <span data-ttu-id="5bd9e-241">사용자 세션 관리에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-241">Provides support for managing user sessions.</span></span> | <span data-ttu-id="5bd9e-242">세션이 필요한 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-242">Before components that require Session.</span></span> |
| [<span data-ttu-id="5bd9e-243">정적 파일</span><span class="sxs-lookup"><span data-stu-id="5bd9e-243">Static Files</span></span>](xref:fundamentals/static-files) | <span data-ttu-id="5bd9e-244">정적 파일 및 디렉터리 검색 처리에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-244">Provides support for serving static files and directory browsing.</span></span> | <span data-ttu-id="5bd9e-245">요청이 파일과 일치하는 경우 터미널.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-245">Terminal if a request matches files.</span></span> |
| [<span data-ttu-id="5bd9e-246">URL 재작성</span><span class="sxs-lookup"><span data-stu-id="5bd9e-246">URL Rewriting</span></span>](xref:fundamentals/url-rewriting) | <span data-ttu-id="5bd9e-247">URL 재작성 및 요청 리디렉션에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-247">Provides support for rewriting URLs and redirecting requests.</span></span> | <span data-ttu-id="5bd9e-248">URL을 사용하는 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-248">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="5bd9e-249">WebSockets</span><span class="sxs-lookup"><span data-stu-id="5bd9e-249">WebSockets</span></span>](xref:fundamentals/websockets) | <span data-ttu-id="5bd9e-250">WebSocket 프로토콜을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-250">Enables the WebSockets protocol.</span></span> | <span data-ttu-id="5bd9e-251">WebSocket 요청을 수락하는 데 필요한 구성 요소 이전.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-251">Before components that are required to accept WebSocket requests.</span></span> |

<a name="middleware-writing-middleware"></a>

## <a name="writing-middleware"></a><span data-ttu-id="5bd9e-252">미들웨어 작성</span><span class="sxs-lookup"><span data-stu-id="5bd9e-252">Writing middleware</span></span>

<span data-ttu-id="5bd9e-253">미들웨어는 일반적으로 클래스에서 캡슐화되고 확장 메서드로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-253">Middleware is generally encapsulated in a class and exposed with an extension method.</span></span> <span data-ttu-id="5bd9e-254">쿼리 문자열에서 현재 요청에 대한 문화권을 설정하는 다음 미들웨어를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-254">Consider the following middleware, which sets the culture for the current request from the query string:</span></span>

[!code-csharp[](index/sample/Culture/StartupCulture.cs?name=snippet1)]

<span data-ttu-id="5bd9e-255">참고: 위의 샘플 코드는 미들웨어 구성 요소 만들기를 보여 주는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-255">Note: The sample code above is used to demonstrate creating a middleware component.</span></span> <span data-ttu-id="5bd9e-256">ASP.NET Core의 기본 제공 지역화 지원은 [전역화 및 지역화](xref:fundamentals/localization)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-256">See [ Globalization and localization](xref:fundamentals/localization) for ASP.NET Core's built-in localization support.</span></span>

<span data-ttu-id="5bd9e-257">문화권을 전달하여 미들웨어를 테스트할 수 있습니다(예: `http://localhost:7997/?culture=no`).</span><span class="sxs-lookup"><span data-stu-id="5bd9e-257">You can test the middleware by passing in the culture, for example `http://localhost:7997/?culture=no`.</span></span>

<span data-ttu-id="5bd9e-258">다음 코드는 미들웨어 대리자를 클래스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-258">The following code moves the middleware delegate to a class:</span></span>

[!code-csharp[](index/sample/Culture/RequestCultureMiddleware.cs)]

> [!NOTE]
> <span data-ttu-id="5bd9e-259">ASP.NET Core 1.x에서 미들웨어 `Task` 메서드의 이름은 `Invoke`이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-259">In ASP.NET Core 1.x, the middleware `Task` method's name must be `Invoke`.</span></span> <span data-ttu-id="5bd9e-260">ASP.NET 코어 2.0 이상에서는 이름이 `Invoke` 또는 `InvokeAsync`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-260">In ASP.NET Core 2.0 or later, the name can be either `Invoke` or `InvokeAsync`.</span></span>

<span data-ttu-id="5bd9e-261">다음 확장 메서드는 [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder)를 통해 미들웨어를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-261">The following extension method exposes the middleware through [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder):</span></span>

[!code-csharp[](index/sample/Culture/RequestCultureMiddlewareExtensions.cs)]

<span data-ttu-id="5bd9e-262">다음 코드는 `Configure`에서 미들웨어를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-262">The following code calls the middleware from `Configure`:</span></span>

[!code-csharp[](index/sample/Culture/Startup.cs?name=snippet1&highlight=5)]

<span data-ttu-id="5bd9e-263">미들웨어는 해당 생성자에서 해당 종속성을 노출하여 [명시적 종속성 원칙](http://deviq.com/explicit-dependencies-principle/)을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-263">Middleware should follow the [Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/) by exposing its dependencies in its constructor.</span></span> <span data-ttu-id="5bd9e-264">미들웨어는 *응용 프로그램 수명*당 한 번 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-264">Middleware is constructed once per *application lifetime*.</span></span> <span data-ttu-id="5bd9e-265">서비스를 요청 내의 미들웨어와 공유해야 하는 경우 아래 *요청당 종속성*을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-265">See *Per-request dependencies* below if you need to share services with middleware within a request.</span></span>

<span data-ttu-id="5bd9e-266">미들웨어 구성 요소는 생성자 매개 변수를 통해 종속성 주입에서 해당 종속성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-266">Middleware components can resolve their dependencies from dependency injection through constructor parameters.</span></span> <span data-ttu-id="5bd9e-267">[`UseMiddleware<T>`](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions#methods_summary)는 추가 매개 변수를 직접 수락할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-267">[`UseMiddleware<T>`](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions#methods_summary) can also accept additional parameters directly.</span></span>

### <a name="per-request-dependencies"></a><span data-ttu-id="5bd9e-268">요청당 종속성</span><span class="sxs-lookup"><span data-stu-id="5bd9e-268">Per-request dependencies</span></span>

<span data-ttu-id="5bd9e-269">미들웨어는 요청당이 아닌 앱 시작 시 생성되므로 미들웨어 생성자에 의해 사용되는 *범위가 지정된* 수명 서비스는 각 요청 중에 다른 종속성 주입된 형식과 공유되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-269">Because middleware is constructed at app startup, not per-request, *scoped* lifetime services used by middleware constructors are not  shared with other dependency-injected types during each request.</span></span> <span data-ttu-id="5bd9e-270">*범위가 지정된* 서비스를 미들웨어와 다른 형식 간에 공유해야 하는 경우 이러한 서비스를 `Invoke` 메서드의 서명에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-270">If you must share a *scoped* service between your middleware and other types, add these services to the `Invoke` method's signature.</span></span> <span data-ttu-id="5bd9e-271">`Invoke` 메서드는 종속성 주입으로 채워지는 추가 매개 변수를 수락할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bd9e-271">The `Invoke` method can accept additional parameters that are populated by dependency injection.</span></span> <span data-ttu-id="5bd9e-272">예:</span><span class="sxs-lookup"><span data-stu-id="5bd9e-272">For example:</span></span>

```csharp
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

## <a name="additional-resources"></a><span data-ttu-id="5bd9e-273">추가 자료</span><span class="sxs-lookup"><span data-stu-id="5bd9e-273">Additional resources</span></span>

* [<span data-ttu-id="5bd9e-274">HTTP 모듈을 미들웨어로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="5bd9e-274">Migrate HTTP Modules to Middleware</span></span>](xref:migration/http-modules)
* [<span data-ttu-id="5bd9e-275">응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="5bd9e-275">Application Startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="5bd9e-276">요청 기능</span><span class="sxs-lookup"><span data-stu-id="5bd9e-276">Request Features</span></span>](xref:fundamentals/request-features)
* [<span data-ttu-id="5bd9e-277">팩터리 기반 미들웨어 활성화</span><span class="sxs-lookup"><span data-stu-id="5bd9e-277">Factory-based middleware activation</span></span>](xref:fundamentals/middleware/extensibility)
* [<span data-ttu-id="5bd9e-278">타사 컨테이너를 사용하여 미들웨어 활성화</span><span class="sxs-lookup"><span data-stu-id="5bd9e-278">Middleware activation with a third-party container</span></span>](xref:fundamentals/middleware/extensibility-third-party-container)
