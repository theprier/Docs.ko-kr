---
title: "ASP.NET Core 기본 사항"
author: rick-anderson
description: "ASP.NET Core 응용 프로그램을 빌드하기 위한 기본적인 개념을 검색합니다."
keywords: "ASP.NET Core, 기본 사항, 개요"
ms.author: riande
manager: wpickett
ms.date: 09/30/2017
ms.topic: get-started-article
ms.assetid: a19b7836-63e4-44e8-8250-50d426dd1070
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/index
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 83bed4676be3ca752442da3fe560f1f2a4d728a1
ms.sourcegitcommit: 8f42ab93402c1b8044815e1e48d0bb84c81f8b59
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/29/2017
---
# <a name="aspnet-core-fundamentals"></a><span data-ttu-id="c514b-104">ASP.NET Core 기본 사항</span><span class="sxs-lookup"><span data-stu-id="c514b-104">ASP.NET Core fundamentals</span></span>

<span data-ttu-id="c514b-105">ASP.NET Core 응용 프로그램은 `Main` 메서드에서 웹 서버를 만드는 콘솔 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-105">An ASP.NET Core application is a console app that creates a web server in its `Main` method:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="c514b-106">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="c514b-106">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program2x.cs)]

<span data-ttu-id="c514b-107">`Main` 메서드는 빌드 패턴에 따라 웹 응용 프로그램 호스트를 만드는 `WebHost.CreateDefaultBuilder`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-107">The `Main` method invokes `WebHost.CreateDefaultBuilder`, which follows the builder pattern to create a web application host.</span></span> <span data-ttu-id="c514b-108">빌더에는 웹 서버(예: `UseKestrel`) 및 시작 클래스(`UseStartup`)를 정의하는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-108">The builder has methods that define the web server (for example, `UseKestrel`) and the startup class (`UseStartup`).</span></span> <span data-ttu-id="c514b-109">이전 예제에서 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버가 자동으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-109">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is automatically allocated.</span></span> <span data-ttu-id="c514b-110">사용 가능한 경우 ASP.NET Core의 웹 호스트는 IIS에서 실행하도록 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-110">ASP.NET Core's web host attempts to run on IIS, if available.</span></span> <span data-ttu-id="c514b-111">[HTTP.sys](xref:fundamentals/servers/httpsys) 같은 다른 웹 서버는 해당하는 확장 메서드를 호출하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-111">Other web servers, such as [HTTP.sys](xref:fundamentals/servers/httpsys), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="c514b-112">`UseStartup`은 다음 섹션에서 추가로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-112">`UseStartup` is explained further in the next section.</span></span>

<span data-ttu-id="c514b-113">`WebHost.CreateDefaultBuilder` 호출의 반환 형식인 `IWebHostBuilder`는 다양한 선택적 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-113">`IWebHostBuilder`, the return type of the `WebHost.CreateDefaultBuilder` invocation, provides many optional methods.</span></span> <span data-ttu-id="c514b-114">이러한 일부 메서드에는 앱을 HTTP.sys에서 호스트하기 위한 `UseHttpSys` 및 루트 콘텐츠 디렉터리를 지정하기 위한 `UseContentRoot`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-114">Some of these methods include `UseHttpSys` for hosting the app in HTTP.sys and `UseContentRoot` for specifying the root content directory.</span></span> <span data-ttu-id="c514b-115">`Build` 및 `Run` 메서드는 앱을 호스트하고 HTTP 요청을 수신하기 시작하는 `IWebHost` 개체를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-115">The `Build` and `Run` methods build the `IWebHost` object that hosts the app and begins listening for HTTP requests.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="c514b-116">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="c514b-116">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program.cs)]

<span data-ttu-id="c514b-117">`Main` 메서드는 빌드 패턴에 따라 웹 응용 프로그램 호스트를 만드는 `WebHostBuilder`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-117">The `Main` method uses `WebHostBuilder`, which follows the builder pattern to create a web application host.</span></span> <span data-ttu-id="c514b-118">빌더에는 웹 서버(예: `UseKestrel`) 및 시작 클래스(`UseStartup`)를 정의하는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-118">The builder has methods that define the web server (for example, `UseKestrel`) and the startup class (`UseStartup`).</span></span> <span data-ttu-id="c514b-119">이전 예제에서는 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-119">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is used.</span></span> <span data-ttu-id="c514b-120">[WebListener](xref:fundamentals/servers/weblistener) 같은 다른 웹 서버는 해당하는 확장 메서드를 호출하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-120">Other web servers, such as [WebListener](xref:fundamentals/servers/weblistener), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="c514b-121">`UseStartup`은 다음 섹션에서 추가로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-121">`UseStartup` is explained further in the next section.</span></span>

<span data-ttu-id="c514b-122">`WebHostBuilder`는 IIS 및 IIS Express에서 호스트하기 위한 `UseIISIntegration` 및 루트 콘텐츠 디렉터리를 지정하기 위한 `UseContentRoot`를 포함한 다양한 선택적 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-122">`WebHostBuilder` provides many optional methods, including `UseIISIntegration` for hosting in IIS and IIS Express and `UseContentRoot` for specifying the root content directory.</span></span> <span data-ttu-id="c514b-123">`Build` 및 `Run` 메서드는 앱을 호스트하고 HTTP 요청을 수신하기 시작하는 `IWebHost` 개체를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-123">The `Build` and `Run` methods build the `IWebHost` object that hosts the app and begins listening for HTTP requests.</span></span>

---

## <a name="startup"></a><span data-ttu-id="c514b-124">시작</span><span class="sxs-lookup"><span data-stu-id="c514b-124">Startup</span></span>

<span data-ttu-id="c514b-125">`WebHostBuilder`의 `UseStartup` 메서드는 앱에 대한 `Startup` 클래스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-125">The `UseStartup` method on `WebHostBuilder` specifies the `Startup` class for your app:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="c514b-126">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="c514b-126">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program2x.cs?highlight=10&range=6-17)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="c514b-127">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="c514b-127">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program.cs?highlight=7&range=6-17)]

---

<span data-ttu-id="c514b-128">`Startup` 클래스는 요청 처리 파이프라인을 정의하고 앱에 필요한 서비스를 구성하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-128">The `Startup` class is where you define the request handling pipeline and where any services needed by the app are configured.</span></span> <span data-ttu-id="c514b-129">`Startup` 클래스는 공용이어야 하고 다음 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-129">The `Startup` class must be public and contain the following methods:</span></span>

```csharp
public class Startup
{
    // This method gets called by the runtime. Use this method
    // to add services to the container.
    public void ConfigureServices(IServiceCollection services)
    {
    }

    // This method gets called by the runtime. Use this method
    // to configure the HTTP request pipeline.
    public void Configure(IApplicationBuilder app)
    {
    }
}
```

<span data-ttu-id="c514b-130">`ConfigureServices`는 앱에서 사용되는 [서비스](#dependency-injection-services)를 정의합니다(예: ASP.NET Core MVC, Entity Framework Core, ID).</span><span class="sxs-lookup"><span data-stu-id="c514b-130">`ConfigureServices` defines the [Services](#dependency-injection-services) used by your app (for example, ASP.NET Core MVC, Entity Framework Core, Identity).</span></span> <span data-ttu-id="c514b-131">`Configure`는 요청 파이프라인의 [미들웨어](xref:fundamentals/middleware)를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-131">`Configure` defines the [middleware](xref:fundamentals/middleware) for the request pipeline.</span></span>

<span data-ttu-id="c514b-132">자세한 내용은 [응용 프로그램 시작](xref:fundamentals/startup)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-132">For more information, see [Application startup](xref:fundamentals/startup).</span></span>

## <a name="content-root"></a><span data-ttu-id="c514b-133">콘텐츠 루트</span><span class="sxs-lookup"><span data-stu-id="c514b-133">Content root</span></span>

<span data-ttu-id="c514b-134">콘텐츠 루트는 앱에서 사용되는 뷰, [Razor 페이지](xref:mvc/razor-pages/index) 및 정적 자산 같은 콘텐츠의 기본 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-134">The content root is the base path to any content used by the app, such as views, [Razor Pages](xref:mvc/razor-pages/index), and static assets.</span></span> <span data-ttu-id="c514b-135">기본적으로 콘텐츠 루트는 앱을 호스트하는 실행 파일의 응용 프로그램 기본 경로와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-135">By default, the content root is the same as application base path for the executable hosting the app.</span></span>

## <a name="web-root"></a><span data-ttu-id="c514b-136">웹 루트</span><span class="sxs-lookup"><span data-stu-id="c514b-136">Web root</span></span>

<span data-ttu-id="c514b-137">앱의 웹 루트는 CSS, JavaScript 및 이미지 파일과 같은 공용 정적 리소스를 포함하는 프로젝트의 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-137">The web root of an app is the directory in the project containing public, static resources, such as CSS, JavaScript, and image files.</span></span>

## <a name="dependency-injection-services"></a><span data-ttu-id="c514b-138">종속성 주입(서비스)</span><span class="sxs-lookup"><span data-stu-id="c514b-138">Dependency Injection (Services)</span></span>

<span data-ttu-id="c514b-139">서비스는 앱에서 공통으로 사용하기 위해 설계된 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-139">A service is a component that's intended for common consumption in an app.</span></span> <span data-ttu-id="c514b-140">서비스는 DI([종속성 주입](xref:fundamentals/dependency-injection))를 통해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-140">Services are made available through [dependency injection (DI)](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="c514b-141">ASP.NET Core에는 기본적으로 [생성자 주입](xref:mvc/controllers/dependency-injection#constructor-injection)을 지원하는 네이티브 IoC(**I**nversion **o**f **C**) 컨테이너가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-141">ASP.NET Core includes a native **I**nversion **o**f **C**ontrol (IoC) container that supports [constructor injection](xref:mvc/controllers/dependency-injection#constructor-injection) by default.</span></span> <span data-ttu-id="c514b-142">원하는 경우 기본 네이티브 컨테이너를 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-142">You can replace the default native container if you wish.</span></span> <span data-ttu-id="c514b-143">느슨한 결합의 이점 이외에 DI를 통해 앱 전체에서 서비스를 사용할 수 있습니다(예: [로깅](xref:fundamentals/logging/index)).</span><span class="sxs-lookup"><span data-stu-id="c514b-143">In addition to its loose coupling benefit, DI makes services available throughout your app (for example, [logging](xref:fundamentals/logging/index)).</span></span>

<span data-ttu-id="c514b-144">자세한 내용은 [종속성 주입](xref:fundamentals/dependency-injection)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-144">For more information, see [Dependency injection](xref:fundamentals/dependency-injection).</span></span>

## <a name="middleware"></a><span data-ttu-id="c514b-145">미들웨어</span><span class="sxs-lookup"><span data-stu-id="c514b-145">Middleware</span></span>

<span data-ttu-id="c514b-146">ASP.NET Core에서 [미들웨어](xref:fundamentals/middleware)를 사용하여 요청 파이프라인을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-146">In ASP.NET Core, you compose your request pipeline using [middleware](xref:fundamentals/middleware).</span></span> <span data-ttu-id="c514b-147">ASP.NET Core 미들웨어는 `HttpContext`에서 비동기 논리를 수행하고 나서 시퀀스에서 다음 미들웨어를 호출하거나 요청을 직접 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-147">ASP.NET Core middleware performs asynchronous logic on an `HttpContext` and then either invokes the next middleware in the sequence or terminates the request directly.</span></span> <span data-ttu-id="c514b-148">"XYZ"라는 미들웨어 구성 요소는 `Configure` 메서드에서 `UseXYZ` 확장 메서드를 호출하여 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-148">A middleware component called "XYZ" is added by invoking an `UseXYZ` extension method in the `Configure` method.</span></span>

<span data-ttu-id="c514b-149">ASP.NET Core는 다양한 기본 제공 미들웨어 집합이 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-149">ASP.NET Core comes with a rich set of built-in middleware:</span></span>

* [<span data-ttu-id="c514b-150">정적 파일</span><span class="sxs-lookup"><span data-stu-id="c514b-150">Static files</span></span>](xref:fundamentals/static-files)
* [<span data-ttu-id="c514b-151">라우팅</span><span class="sxs-lookup"><span data-stu-id="c514b-151">Routing</span></span>](xref:fundamentals/routing)
* [<span data-ttu-id="c514b-152">인증</span><span class="sxs-lookup"><span data-stu-id="c514b-152">Authentication</span></span>](xref:security/authentication/index)
* [<span data-ttu-id="c514b-153">응답 압축 미들웨어</span><span class="sxs-lookup"><span data-stu-id="c514b-153">Response Compression Middleware</span></span>](xref:performance/response-compression)
* [<span data-ttu-id="c514b-154">URL 재작성 미들웨어</span><span class="sxs-lookup"><span data-stu-id="c514b-154">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)

<span data-ttu-id="c514b-155">ASP.NET Core 앱에서 [OWIN](http://owin.org) 기반 미들웨어를 사용할 수 있고 고유한 사용자 지정 미들웨어를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-155">[OWIN](http://owin.org)-based middleware is available for ASP.NET Core apps, and you can write your own custom middleware.</span></span>

<span data-ttu-id="c514b-156">자세한 내용은 [미들웨어](xref:fundamentals/middleware) 및 [OWIN(Open Web Interface for .NET)](xref:fundamentals/owin)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-156">For more information, see [Middleware](xref:fundamentals/middleware) and [Open Web Interface for .NET (OWIN)](xref:fundamentals/owin).</span></span>

## <a name="environments"></a><span data-ttu-id="c514b-157">환경</span><span class="sxs-lookup"><span data-stu-id="c514b-157">Environments</span></span>

<span data-ttu-id="c514b-158">"개발" 및 "프로덕션"과 같은 환경은 ASP.NET Core의 고급 개념이고 환경 변수를 사용하여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-158">Environments, such as "Development" and "Production", are a first-class notion in ASP.NET Core and can be set using environment variables.</span></span>

<span data-ttu-id="c514b-159">자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-159">For more information, see [Working with Multiple Environments](xref:fundamentals/environments).</span></span>

## <a name="configuration"></a><span data-ttu-id="c514b-160">구성</span><span class="sxs-lookup"><span data-stu-id="c514b-160">Configuration</span></span>

<span data-ttu-id="c514b-161">ASP.NET Core는 이름 값 쌍에 기반한 구성 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-161">ASP.NET Core uses a configuration model based on name-value pairs.</span></span> <span data-ttu-id="c514b-162">구성 모델은 `System.Configuration` 또는 *web.config*를 기반으로 하지 않습니다. 구성은 구성 공급자의 정렬된 집합에서 설정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-162">The configuration model isn't based on `System.Configuration` or *web.config*. Configuration obtains settings from an ordered set of configuration providers.</span></span> <span data-ttu-id="c514b-163">기본 제공 구성 공급자는 환경 기반 구성을 가능하게 하는 다양한 파일 형식(XML, JSON, INI) 및 환경 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-163">The built-in configuration providers support a variety of file formats (XML, JSON, INI) and environment variables to enable environment-based configuration.</span></span> <span data-ttu-id="c514b-164">자체 사용자 지정 구성 공급자를 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-164">You can also write your own custom configuration providers.</span></span>

<span data-ttu-id="c514b-165">자세한 내용은 [구성](xref:fundamentals/configuration/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-165">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

## <a name="logging"></a><span data-ttu-id="c514b-166">로깅</span><span class="sxs-lookup"><span data-stu-id="c514b-166">Logging</span></span>

<span data-ttu-id="c514b-167">ASP.NET Core는 다양한 로깅 공급자를 사용하는 로깅 API를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-167">ASP.NET Core supports a logging API that works with a variety of logging providers.</span></span> <span data-ttu-id="c514b-168">기본 제공 공급자는 로그를 하나 이상의 대상으로 보내도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-168">Built-in providers support sending logs to one or more destinations.</span></span> <span data-ttu-id="c514b-169">타사 로깅 프레임워크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-169">Third-party logging frameworks can be used.</span></span>

[<span data-ttu-id="c514b-170">로깅</span><span class="sxs-lookup"><span data-stu-id="c514b-170">Logging</span></span>](xref:fundamentals/logging/index)

## <a name="error-handling"></a><span data-ttu-id="c514b-171">오류 처리</span><span class="sxs-lookup"><span data-stu-id="c514b-171">Error handling</span></span>

<span data-ttu-id="c514b-172">ASP.NET Core에는 앱에서 개발자 예외 페이지, 사용자 지정 오류 페이지, 고정 상태 코드 페이지 및 시작 예외 처리를 포함하여 오류 처리에 대한 기본 제공 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-172">ASP.NET Core has built-in features for handling errors in apps, including a developer exception page, custom error pages, static status code pages, and startup exception handling.</span></span>

<span data-ttu-id="c514b-173">자세한 내용은 [오류 처리](xref:fundamentals/error-handling)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-173">For more information, see [Error Handling](xref:fundamentals/error-handling).</span></span>

## <a name="routing"></a><span data-ttu-id="c514b-174">라우팅</span><span class="sxs-lookup"><span data-stu-id="c514b-174">Routing</span></span>

<span data-ttu-id="c514b-175">ASP.NET Core는 경로 처리기에 앱 요청을 라우팅하기 위한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-175">ASP.NET Core offers features for routing of app requests to route handlers.</span></span>

<span data-ttu-id="c514b-176">자세한 내용은 [라우팅](xref:fundamentals/routing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-176">For more information, see [Routing](xref:fundamentals/routing).</span></span>

## <a name="file-providers"></a><span data-ttu-id="c514b-177">파일 공급자</span><span class="sxs-lookup"><span data-stu-id="c514b-177">File providers</span></span>

<span data-ttu-id="c514b-178">ASP.NET Core는 파일 공급자를 사용하여 파일 시스템 액세스를 추상화하고 플랫폼에서 파일을 사용하기 위한 공통 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-178">ASP.NET Core abstracts file system access through the use of File Providers, which offers a common interface for working with files across platforms.</span></span>

<span data-ttu-id="c514b-179">자세한 내용은 [파일 공급자](xref:fundamentals/file-providers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-179">For more information, see [File Providers](xref:fundamentals/file-providers).</span></span>

## <a name="static-files"></a><span data-ttu-id="c514b-180">정적 파일</span><span class="sxs-lookup"><span data-stu-id="c514b-180">Static files</span></span>

<span data-ttu-id="c514b-181">고정 파일 미들웨어는 HTML, CSS, 이미지, JavaScript 등의 고정 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-181">Static files middleware serves static files, such as HTML, CSS, image, and JavaScript.</span></span>

<span data-ttu-id="c514b-182">자세한 내용은 [고정 파일 작업](xref:fundamentals/static-files)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-182">For more information, see [Working with static files](xref:fundamentals/static-files).</span></span>

## <a name="hosting"></a><span data-ttu-id="c514b-183">호스팅</span><span class="sxs-lookup"><span data-stu-id="c514b-183">Hosting</span></span>

<span data-ttu-id="c514b-184">ASP.NET Core 앱은 앱 시작 및 수명 관리를 담당하는 *호스트*를 구성하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-184">ASP.NET Core apps configure and launch a *host*, which is responsible for app startup and lifetime management.</span></span>

<span data-ttu-id="c514b-185">자세한 내용은 [호스팅](xref:fundamentals/hosting)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-185">For more information, see [Hosting](xref:fundamentals/hosting).</span></span>

## <a name="session-and-application-state"></a><span data-ttu-id="c514b-186">세션 및 응용 프로그램 상태</span><span class="sxs-lookup"><span data-stu-id="c514b-186">Session and application state</span></span>

<span data-ttu-id="c514b-187">세션 상태는 사용자가 웹앱을 탐색하는 동안 사용자 데이터를 저장하는 데 사용할 수 있는 ASP.NET Core의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-187">Session state is a feature in ASP.NET Core that you can use to save and store user data while the user browses your web app.</span></span>

<span data-ttu-id="c514b-188">자세한 내용은 [세션 및 응용 프로그램 상태](xref:fundamentals/app-state)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-188">For more information, see [Session and application state](xref:fundamentals/app-state).</span></span>

## <a name="servers"></a><span data-ttu-id="c514b-189">서버</span><span class="sxs-lookup"><span data-stu-id="c514b-189">Servers</span></span>

<span data-ttu-id="c514b-190">ASP.NET Core 호스팅 모델은 요청을 직접 수신하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-190">The ASP.NET Core hosting model doesn't directly listen for requests.</span></span> <span data-ttu-id="c514b-191">호스팅 모델은 HTTP 서버 구현을 사용하여 앱에 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-191">The hosting model relies on an HTTP server implementation to forward the request to the app.</span></span> <span data-ttu-id="c514b-192">전달된 요청은 인터페이스를 통해 액세스할 수 있는 기능 개체 집합으로 래핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-192">The forwarded request is wrapped as a set of feature objects that can be accessed through interfaces.</span></span> <span data-ttu-id="c514b-193">ASP.NET Core에는 [Kestrel](xref:fundamentals/servers/kestrel)이라는 관리되는 플랫폼 간 웹 서버가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-193">ASP.NET Core includes a managed, cross-platform web server, called [Kestrel](xref:fundamentals/servers/kestrel).</span></span> <span data-ttu-id="c514b-194">Kestrel은 주로 [IIS](https://www.iis.net/) 또는 [nginx](http://nginx.org)와 같은 프로덕션 웹 서버의 백그라운드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-194">Kestrel is often run behind a production web server, such as [IIS](https://www.iis.net/) or [nginx](http://nginx.org).</span></span> <span data-ttu-id="c514b-195">Kestrel은 에지 서버로 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-195">Kestrel can be run as an edge server.</span></span>

<span data-ttu-id="c514b-196">자세한 내용은 [서버](xref:fundamentals/servers/index) 및 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-196">For more information, see [Servers](xref:fundamentals/servers/index) and the following topics:</span></span>

* [<span data-ttu-id="c514b-197">Kestrel</span><span class="sxs-lookup"><span data-stu-id="c514b-197">Kestrel</span></span>](xref:fundamentals/servers/kestrel)
* [<span data-ttu-id="c514b-198">ASP.NET Core 모듈</span><span class="sxs-lookup"><span data-stu-id="c514b-198">ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* <span data-ttu-id="c514b-199">[HTTP.sys](xref:fundamentals/servers/httpsys)(이전의 [WebListener](xref:fundamentals/servers/weblistener))</span><span class="sxs-lookup"><span data-stu-id="c514b-199">[HTTP.sys](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener))</span></span>

## <a name="globalization-and-localization"></a><span data-ttu-id="c514b-200">전역화 및 지역화</span><span class="sxs-lookup"><span data-stu-id="c514b-200">Globalization and localization</span></span>

<span data-ttu-id="c514b-201">ASP.NET Core를 사용하여 다국어 웹 사이트를 만들면 더 광범위한 사용자가 사이트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-201">Creating a multilingual website with ASP.NET Core allows your site to reach a wider audience.</span></span> <span data-ttu-id="c514b-202">ASP.NET Core는 다른 언어와 문화권으로의 지역화를 위한 서비스 및 미들웨어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-202">ASP.NET Core provides services and middleware for localizing into different languages and cultures.</span></span>

<span data-ttu-id="c514b-203">자세한 내용은 [전역화 및 지역화](xref:fundamentals/localization)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-203">For more information, see [Globalization and localization](xref:fundamentals/localization).</span></span>

## <a name="request-features"></a><span data-ttu-id="c514b-204">요청 기능</span><span class="sxs-lookup"><span data-stu-id="c514b-204">Request features</span></span>

<span data-ttu-id="c514b-205">웹 서버 구현은 HTTP 요청과 관련하여 설명되고 응답은 인터페이스에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-205">Web server implementation details related to HTTP requests and responses are defined in interfaces.</span></span> <span data-ttu-id="c514b-206">서버 구현 및 미들웨어에서 이러한 인터페이스를 사용하여 앱의 호스팅 파이프라인을 만들고 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-206">These interfaces are used by server implementations and middleware to create and modify the app's hosting pipeline.</span></span>

<span data-ttu-id="c514b-207">자세한 내용은 [요청 기능](xref:fundamentals/request-features)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-207">For more information, see [Request Features](xref:fundamentals/request-features).</span></span>

## <a name="open-web-interface-for-net-owin"></a><span data-ttu-id="c514b-208">OWIN(Open Web Interface for .NET)</span><span class="sxs-lookup"><span data-stu-id="c514b-208">Open Web Interface for .NET (OWIN)</span></span>

<span data-ttu-id="c514b-209">ASP.NET Core는 OWIN(Open Web Interface for .NET)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-209">ASP.NET Core supports the Open Web Interface for .NET (OWIN).</span></span> <span data-ttu-id="c514b-210">OWIN을 사용하면 웹앱을 웹 서버에서 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-210">OWIN allows web apps to be decoupled from web servers.</span></span>

<span data-ttu-id="c514b-211">자세한 내용은 [OWIN(Open Web Interface for .NET)](xref:fundamentals/owin)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-211">For more information, see [Open Web Interface for .NET (OWIN)](xref:fundamentals/owin).</span></span>

## <a name="websockets"></a><span data-ttu-id="c514b-212">WebSocket</span><span class="sxs-lookup"><span data-stu-id="c514b-212">WebSockets</span></span>

<span data-ttu-id="c514b-213">[WebSocket](https://wikipedia.org/wiki/WebSocket)은 TCP 연결을 통한 영구 양방향 통신 채널을 사용하도록 설정하는 프로토콜이며</span><span class="sxs-lookup"><span data-stu-id="c514b-213">[WebSocket](https://wikipedia.org/wiki/WebSocket) is a protocol that enables two-way persistent communication channels over TCP connections.</span></span> <span data-ttu-id="c514b-214">채팅, 주식 종목, 게임 및 웹앱의 실시간 기능을 사용하려는 곳 등 앱에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-214">It's used for apps such as chat, stock tickers, games, and anywhere you desire real-time functionality in a web app.</span></span> <span data-ttu-id="c514b-215">ASP.NET Core는 WebSocket 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-215">ASP.NET Core supports web socket features.</span></span>

<span data-ttu-id="c514b-216">자세한 내용은 [WebSocket](xref:fundamentals/websockets)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-216">For more information, see [WebSockets](xref:fundamentals/websockets).</span></span>

## <a name="microsoftaspnetcoreall-metapackage"></a><span data-ttu-id="c514b-217">Microsoft.AspNetCore.All 메타패키지</span><span class="sxs-lookup"><span data-stu-id="c514b-217">Microsoft.AspNetCore.All metapackage</span></span>

<span data-ttu-id="c514b-218">ASP.NET Core에 대한 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 메타패키지는 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-218">The [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage for ASP.NET Core includes:</span></span>

* <span data-ttu-id="c514b-219">ASP.NET Core 팀에서 지원되는 모든 패키지</span><span class="sxs-lookup"><span data-stu-id="c514b-219">All supported packages by the ASP.NET Core team.</span></span>
* <span data-ttu-id="c514b-220">Entity Framework Core에서 지원되는 모든 패키지</span><span class="sxs-lookup"><span data-stu-id="c514b-220">All supported packages by the Entity Framework Core.</span></span> 
* <span data-ttu-id="c514b-221">ASP.NET Core 및 Entity Framework Core에서 사용하는 내부 및 타사 종속성</span><span class="sxs-lookup"><span data-stu-id="c514b-221">Internal and 3rd-party dependencies used by ASP.NET Core and Entity Framework Core.</span></span>

<span data-ttu-id="c514b-222">자세한 내용은 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-222">For more information, see [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

## <a name="net-core-vs-net-framework-runtime"></a><span data-ttu-id="c514b-223">.NET Core 및 .NET Framework 런타임</span><span class="sxs-lookup"><span data-stu-id="c514b-223">.NET Core vs. .NET Framework runtime</span></span>

<span data-ttu-id="c514b-224">ASP.NET Core 앱은 .NET Core 또는 .NET Framework 런타임을 대상으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c514b-224">An ASP.NET Core app can target the .NET Core or .NET Framework runtime.</span></span>

<span data-ttu-id="c514b-225">자세한 내용은 [.NET Core와 .NET Framework 중에 선택](/dotnet/articles/standard/choosing-core-framework-server)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-225">For more information, see [Choosing between .NET Core and .NET Framework](/dotnet/articles/standard/choosing-core-framework-server).</span></span>

## <a name="choose-between-aspnet-core-and-aspnet"></a><span data-ttu-id="c514b-226">ASP.NET Core와 ASP.NET 중에서 선택</span><span class="sxs-lookup"><span data-stu-id="c514b-226">Choose between ASP.NET Core and ASP.NET</span></span>

<span data-ttu-id="c514b-227">ASP.NET Core 및 ASP.NET 중에서 선택하는 방법 자세한 내용은 [ASP.NET Core 및 ASP.NET 중에서 선택](xref:fundamentals/choose-between-aspnet-and-aspnetcore)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c514b-227">For more information on choosing between ASP.NET Core and ASP.NET, see [Choose between ASP.NET Core and ASP.NET](xref:fundamentals/choose-between-aspnet-and-aspnetcore).</span></span>
