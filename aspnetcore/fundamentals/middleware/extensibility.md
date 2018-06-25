---
title: ASP.NET Core의 팩터리 기반 미들웨어 활성화
author: guardrex
description: ASP.NET Core에서 팩터리 기반 활성화 구현으로 강력한 형식의 미들웨어를 사용하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2018
uid: fundamentals/middleware/extensibility
ms.openlocfilehash: 44987dbc20b0419865a23e64b60a5dc3f436743a
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277074"
---
# <a name="factory-based-middleware-activation-in-aspnet-core"></a><span data-ttu-id="5bcca-103">ASP.NET Core의 팩터리 기반 미들웨어 활성화</span><span class="sxs-lookup"><span data-stu-id="5bcca-103">Factory-based middleware activation in ASP.NET Core</span></span>

<span data-ttu-id="5bcca-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="5bcca-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="5bcca-105">[IMiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory)/[IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware)는 [미들웨어](xref:fundamentals/middleware/index) 활성화에 대한 확장성 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-105">[IMiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory)/[IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) is an extensibility point for [middleware](xref:fundamentals/middleware/index) activation.</span></span>

<span data-ttu-id="5bcca-106">`UseMiddleware` 확장 메서드는 미들웨어의 등록된 형식이 `IMiddleware`를 구현하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-106">`UseMiddleware` extension methods check if a middleware's registered type implements `IMiddleware`.</span></span> <span data-ttu-id="5bcca-107">구현하는 경우 컨테이너에 등록된 `IMiddlewareFactory` 인스턴스는 규칙 기반 미들웨어 활성화 논리를 사용하는 대신 `IMiddleware` 구현을 확인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-107">If it does, the `IMiddlewareFactory` instance registered in the container is used to resolve the `IMiddleware` implementation instead of using the convention-based middleware activation logic.</span></span> <span data-ttu-id="5bcca-108">미들웨어는 앱의 서비스 컨테이너의 범위가 지정된 서비스 또는 일시적인 서비스로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-108">The middleware is registered as a scoped or transient service in the app's service container.</span></span>

<span data-ttu-id="5bcca-109">혜택:</span><span class="sxs-lookup"><span data-stu-id="5bcca-109">Benefits:</span></span>

* <span data-ttu-id="5bcca-110">요청당 활성화(범위가 지정된 서비스의 주입)</span><span class="sxs-lookup"><span data-stu-id="5bcca-110">Activation per request (injection of scoped services)</span></span>
* <span data-ttu-id="5bcca-111">미들웨어의 강력한 형식 지정</span><span class="sxs-lookup"><span data-stu-id="5bcca-111">Strong typing of middleware</span></span>

<span data-ttu-id="5bcca-112">`IMiddleware`는 요청당 활성화되므로 범위가 지정된 서비스는 미들웨어의 생성자에 주입될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-112">`IMiddleware` is activated per request, so scoped services can be injected into the middleware's constructor.</span></span>

<span data-ttu-id="5bcca-113">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/extensibility/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="5bcca-113">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/extensibility/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="5bcca-114">샘플 앱은 다음에 의해 활성화되는 미들웨어를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-114">The sample app demonstrates middleware activated by:</span></span>

* <span data-ttu-id="5bcca-115">규칙.</span><span class="sxs-lookup"><span data-stu-id="5bcca-115">Convention.</span></span> <span data-ttu-id="5bcca-116">규칙에 따른 미들웨어 활성화에 대한 자세한 내용은 [미들웨어](xref:fundamentals/middleware/index) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5bcca-116">For more information on conventional middleware activation, see the [Middleware](xref:fundamentals/middleware/index) topic.</span></span>
* <span data-ttu-id="5bcca-117">[IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-117">An [IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) implementation.</span></span> <span data-ttu-id="5bcca-118">기본 [MiddlewareFactory 클래스](/dotnet/api/microsoft.aspnetcore.http.middlewarefactory)가 미들웨어를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-118">The default [MiddlewareFactory class](/dotnet/api/microsoft.aspnetcore.http.middlewarefactory) activates the middleware.</span></span>

<span data-ttu-id="5bcca-119">미들웨어 구현은 동일하게 작동하며, 쿼리 문자열 매개 변수(`key`)에서 제공한 값을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-119">The middleware implementations function identically and record the value provided by a query string parameter (`key`).</span></span> <span data-ttu-id="5bcca-120">미들웨어는 주입된 데이터베이스 컨텍스트(범위가 지정된 서비스)를 사용하여 메모리 내 데이터베이스에 쿼리 문자열 값을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-120">The middlewares use an injected database context (a scoped service) to record the query string value in an in-memory database.</span></span>

## <a name="imiddleware"></a><span data-ttu-id="5bcca-121">IMiddleware</span><span class="sxs-lookup"><span data-stu-id="5bcca-121">IMiddleware</span></span>

<span data-ttu-id="5bcca-122">[IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware)는 앱의 요청 파이프라인에 대한 미들웨어를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-122">[IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) defines middleware for the app's request pipeline.</span></span> <span data-ttu-id="5bcca-123">[InvokeAsync(HttpContext, RequestDelegate)](/dotnet/api/microsoft.aspnetcore.http.imiddleware.invokeasync#Microsoft_AspNetCore_Http_IMiddleware_InvokeAsync_Microsoft_AspNetCore_Http_HttpContext_Microsoft_AspNetCore_Http_RequestDelegate_) 메서드는 요청을 처리하고 미들웨어의 실행을 나타내는 `Task`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-123">The [InvokeAsync(HttpContext, RequestDelegate)](/dotnet/api/microsoft.aspnetcore.http.imiddleware.invokeasync#Microsoft_AspNetCore_Http_IMiddleware_InvokeAsync_Microsoft_AspNetCore_Http_HttpContext_Microsoft_AspNetCore_Http_RequestDelegate_) method handles requests and returns a `Task` that represents the execution of the middleware.</span></span>

<span data-ttu-id="5bcca-124">규칙에 따라 미들웨어 활성화:</span><span class="sxs-lookup"><span data-stu-id="5bcca-124">Middleware activated by convention:</span></span>

[!code-csharp[](extensibility/sample/Middleware/ConventionalMiddleware.cs?name=snippet1)]

<span data-ttu-id="5bcca-125">`MiddlewareFactory`에 따라 미들웨어 활성화:</span><span class="sxs-lookup"><span data-stu-id="5bcca-125">Middleware activated by `MiddlewareFactory`:</span></span>

[!code-csharp[](extensibility/sample/Middleware/IMiddlewareMiddleware.cs?name=snippet1)]

<span data-ttu-id="5bcca-126">확장은 미들웨어에 대해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-126">Extensions are created for the middlewares:</span></span>

[!code-csharp[](extensibility/sample/Middleware/MiddlewareExtensions.cs?name=snippet1)]

<span data-ttu-id="5bcca-127">개체를 `UseMiddleware`를 사용하여 팩터리 활성화된 미들웨어에 전달할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-127">It isn't possible to pass objects to the factory-activated middleware with `UseMiddleware`:</span></span>

```csharp
public static IApplicationBuilder UseIMiddlewareMiddleware(
    this IApplicationBuilder builder, bool option)
{
    // Passing 'option' as an argument throws a NotSupportedException at runtime.
    return builder.UseMiddleware<IMiddlewareMiddleware>(option);
}
```

<span data-ttu-id="5bcca-128">팩터리 활성화된 미들웨어는 *Startup.cs*의 기본 제공 컨테이너에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-128">The factory-activated middleware is added to the built-in container in *Startup.cs*:</span></span>

[!code-csharp[](extensibility/sample/Startup.cs?name=snippet1&highlight=12)]

<span data-ttu-id="5bcca-129">두 미들웨어는 모두 `Configure`의 요청 처리 파이프라인에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-129">Both middlewares are registered in the request processing pipeline in `Configure`:</span></span>

[!code-csharp[](extensibility/sample/Startup.cs?name=snippet2&highlight=13-14)]

## <a name="imiddlewarefactory"></a><span data-ttu-id="5bcca-130">IMiddlewareFactory</span><span class="sxs-lookup"><span data-stu-id="5bcca-130">IMiddlewareFactory</span></span>

<span data-ttu-id="5bcca-131">[IMiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory)는 미들웨어를 만드는 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-131">[IMiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) provides methods to create middleware.</span></span> <span data-ttu-id="5bcca-132">미들웨어 팩터리 구현은 범위가 지정된 서비스로 컨테이너에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bcca-132">The middleware factory implementation is registered in the container as a scoped service.</span></span>

<span data-ttu-id="5bcca-133">기본 `IMiddlewareFactory` 구현인 [MiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.middlewarefactory)는 [Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/) 패키지에 있습니다([참조 소스](https://github.com/aspnet/HttpAbstractions/blob/release/2.0/src/Microsoft.AspNetCore.Http/MiddlewareFactory.cs)).</span><span class="sxs-lookup"><span data-stu-id="5bcca-133">The default `IMiddlewareFactory` implementation, [MiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.middlewarefactory), is found in the [Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/) package ([reference source](https://github.com/aspnet/HttpAbstractions/blob/release/2.0/src/Microsoft.AspNetCore.Http/MiddlewareFactory.cs)).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5bcca-134">추가 자료</span><span class="sxs-lookup"><span data-stu-id="5bcca-134">Additional resources</span></span>

* [<span data-ttu-id="5bcca-135">미들웨어</span><span class="sxs-lookup"><span data-stu-id="5bcca-135">Middleware</span></span>](xref:fundamentals/middleware/index)
* [<span data-ttu-id="5bcca-136">타사 컨테이너를 사용하여 미들웨어 활성화</span><span class="sxs-lookup"><span data-stu-id="5bcca-136">Middleware activation with a third-party container</span></span>](xref:fundamentals/middleware/extensibility-third-party-container)
