---
title: ASP.NET Core 기본 사항
author: rick-anderson
description: ASP.NET Core 응용 프로그램을 구축하기 위한 기본적인 개념을 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 09/30/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: fundamentals/index
ms.openlocfilehash: d5b74e213828d1a1f7e09810e5cc72773a821dab
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="aspnet-core-fundamentals"></a><span data-ttu-id="587a5-103">ASP.NET Core 기본 사항</span><span class="sxs-lookup"><span data-stu-id="587a5-103">ASP.NET Core fundamentals</span></span>

<span data-ttu-id="587a5-104">ASP.NET Core 응용 프로그램은 `Main` 메서드에서 웹 서버를 생성하는 콘솔 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-104">An ASP.NET Core application is a console app that creates a web server in its `Main` method:</span></span>

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="587a5-105">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="587a5-105">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)
[!code-csharp[](../getting-started/sample/aspnetcoreapp/Program2x.cs)]

<span data-ttu-id="587a5-106">`Main` 메서드는 빌드 패턴에 따라 웹 응용 프로그램 호스트를 만드는 `WebHost.CreateDefaultBuilder`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-106">The `Main` method invokes `WebHost.CreateDefaultBuilder`, which follows the builder pattern to create a web application host.</span></span> <span data-ttu-id="587a5-107">이 빌더는 웹 서버를 정의하거나 (예: `UseKestrel`) 시작 클래스를 정의하는 (`UseStartup`) 메서드들을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-107">The builder has methods that define the web server (for example, `UseKestrel`) and the startup class (`UseStartup`).</span></span> <span data-ttu-id="587a5-108">위의 예제에서는 기본적으로 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버가 할당되며.</span><span class="sxs-lookup"><span data-stu-id="587a5-108">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is automatically allocated.</span></span> <span data-ttu-id="587a5-109">가능하다면 ASP.NET Core의 웹 호스트는 IIS에서 실행하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-109">ASP.NET Core's web host attempts to run on IIS, if available.</span></span> <span data-ttu-id="587a5-110">그러나 적절한 확장 메서드를 호출해서 [HTTP.sys](xref:fundamentals/servers/httpsys) 같은 다른 웹 서버를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-110">Other web servers, such as [HTTP.sys](xref:fundamentals/servers/httpsys), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="587a5-111">`UseStartup` 에 관해서는 다음 섹션에서 더 자세히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-111">`UseStartup` is explained further in the next section.</span></span>

<span data-ttu-id="587a5-112">`WebHost.CreateDefaultBuilder` 호출로부터 반환되는 `IWebHostBuilder`형식은 다양한 선택적 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-112">`IWebHostBuilder`, the return type of the `WebHost.CreateDefaultBuilder` invocation, provides many optional methods.</span></span> <span data-ttu-id="587a5-113">이 메서드들 중에는 HTTP.sys에서 앱을 호스트하기 위한 `UseHttpSys` 및 루트 콘텐츠 디렉터리를 지정하기 위한 `UseContentRoot`도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-113">Some of these methods include `UseHttpSys` for hosting the app in HTTP.sys and `UseContentRoot` for specifying the root content directory.</span></span> <span data-ttu-id="587a5-114">`Build` 및 `Run` 메서드는 앱을 호스트하고 HTTP 요청의 수신 대기를 시작하는 `IWebHost` 개체를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-114">The `Build` and `Run` methods build the `IWebHost` object that hosts the app and begins listening for HTTP requests.</span></span>

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="587a5-115">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="587a5-115">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)
[!code-csharp[](../getting-started/sample/aspnetcoreapp/Program.cs)]

<span data-ttu-id="587a5-116">`Main` 메서드는 빌드 패턴에 따라 웹 응용 프로그램 호스트를 만드는 `WebHostBuilder`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-116">The `Main` method uses `WebHostBuilder`, which follows the builder pattern to create a web application host.</span></span> <span data-ttu-id="587a5-117">이 빌더는 웹 서버를 정의하거나 (예: `UseKestrel`) 시작 클래스를 정의하는(`UseStartup`)메서드들을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-117">The builder has methods that define the web server (for example, `UseKestrel`) and the startup class (`UseStartup`).</span></span> <span data-ttu-id="587a5-118">위의 예제에서는 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버를 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-118">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is used.</span></span> <span data-ttu-id="587a5-119">[WebListener](xref:fundamentals/servers/weblistener) 같은 다른 웹 서버를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-119">Other web servers, such as [WebListener](xref:fundamentals/servers/weblistener), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="587a5-120">`UseStartup`에 관해서는 다음 섹션에서 더 자세히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-120">`UseStartup` is explained further in the next section.</span></span>

<span data-ttu-id="587a5-121">`WebHostBuilder`는 IIS 및 IIS Express에서 호스팅하기 위한 `UseIISIntegration` 확장 메서드 및 루트 콘텐츠 디렉터리를 지정하기 위한 `UseContentRoot`확장 메서드를 비롯한 다양한 선택적 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-121">`WebHostBuilder` provides many optional methods, including `UseIISIntegration` for hosting in IIS and IIS Express and `UseContentRoot` for specifying the root content directory.</span></span> <span data-ttu-id="587a5-122">`Build` 및 `Run` 메서드는 앱을 호스트하고 HTTP 요청의 수신 대기를 시작하는 `IWebHost` 개체를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-122">The `Build` and `Run` methods build the `IWebHost` object that hosts the app and begins listening for HTTP requests.</span></span>

* * *
## <a name="startup"></a><span data-ttu-id="587a5-123">Startup 클래스</span><span class="sxs-lookup"><span data-stu-id="587a5-123">Startup</span></span>

<span data-ttu-id="587a5-124">`WebHostBuilder`의 `UseStartup` 메서드는 앱의 `Startup` 클래스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-124">The `UseStartup` method on `WebHostBuilder` specifies the `Startup` class for your app:</span></span>

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="587a5-125">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="587a5-125">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)
[!code-csharp[](../getting-started/sample/aspnetcoreapp/Program2x.cs?highlight=10&range=6-17)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="587a5-126">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="587a5-126">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)
[!code-csharp[](../getting-started/sample/aspnetcoreapp/Program.cs?highlight=7&range=6-17)]

* * *
<span data-ttu-id="587a5-127">`Startup` 클래스는 요청 처리 파이프라인을 정의하고 앱에 필요한 모든 서비스를 구성하는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-127">The `Startup` class is where you define the request handling pipeline and where any services needed by the app are configured.</span></span> <span data-ttu-id="587a5-128">`Startup` 클래스는 public으로 지정해야 하며 다음과 같은 메서드들을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-128">The `Startup` class must be public and contain the following methods:</span></span>

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

<span data-ttu-id="587a5-129">`ConfigureServices`는 앱에서 사용되는 [서비스](#dependency-injection-services)를 정의합니다 (예, ASP.NET MVC Core MVC, Entity Framework Core, Identity).</span><span class="sxs-lookup"><span data-stu-id="587a5-129">`ConfigureServices` defines the [Services](#dependency-injection-services) used by your app (for example, ASP.NET Core MVC, Entity Framework Core, Identity).</span></span> <span data-ttu-id="587a5-130">그리고`Configure`는 요청 파이프라인의 [미들웨어](xref:fundamentals/middleware/index)를 정의.</span><span class="sxs-lookup"><span data-stu-id="587a5-130">`Configure` defines the [middleware](xref:fundamentals/middleware/index) for the request pipeline.</span></span>

<span data-ttu-id="587a5-131">자세한 내용은 [응용 프로그램 시작](xref:fundamentals/startup)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-131">For more information, see [Application startup](xref:fundamentals/startup).</span></span>

## <a name="content-root"></a><span data-ttu-id="587a5-132">콘텐츠 루트</span><span class="sxs-lookup"><span data-stu-id="587a5-132">Content root</span></span>

<span data-ttu-id="587a5-133">콘텐츠 루트는 앱에서 사용되는 뷰, [Razor 페이지](xref:mvc/razor-pages/index) 및 정적 자산 같은 모든 콘텐츠의 기본 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-133">The content root is the base path to any content used by the app, such as views, [Razor Pages](xref:mvc/razor-pages/index), and static assets.</span></span> <span data-ttu-id="587a5-134">기본적으로 콘텐츠 루트는 앱을 호스팅하는 실행 파일의 응용 프로그램 기본 경로와 동일합니다. </span><span class="sxs-lookup"><span data-stu-id="587a5-134">By default, the content root is the same as application base path for the executable hosting the app.</span></span>

## <a name="web-root"></a><span data-ttu-id="587a5-135">웹 루트</span><span class="sxs-lookup"><span data-stu-id="587a5-135">Web root</span></span>

<span data-ttu-id="587a5-136">앱의 웹 루트는 CSS, JavaScript 및 이미지 파일 같은 공용 정적 리소스가 위치하는 프로젝트의 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-136">The web root of an app is the directory in the project containing public, static resources, such as CSS, JavaScript, and image files.</span></span>

## <a name="dependency-injection-services"></a><span data-ttu-id="587a5-137">종속성 주입(서비스)</span><span class="sxs-lookup"><span data-stu-id="587a5-137">Dependency injection (services)</span></span>

<span data-ttu-id="587a5-138">서비스는 앱에서 공통으로 사용하기 위한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-138">A service is a component that's intended for common consumption in an app.</span></span> <span data-ttu-id="587a5-139">서비스는 DI([종속성 주입](xref:fundamentals/dependency-injection))를 통해서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-139">Services are made available through [dependency injection (DI)](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="587a5-140">ASP.NET Core에는 기본적으로 [생성자 주입](xref:mvc/controllers/dependency-injection#constructor-injection)을 지원하는 네이티브 IoC(**I**nversion **o**f **C**) 컨테이너가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-140">ASP.NET Core includes a native **I**nversion **o**f **C**ontrol (IoC) container that supports [constructor injection](xref:mvc/controllers/dependency-injection#constructor-injection) by default.</span></span> <span data-ttu-id="587a5-141">만약 원한다면 기본 네이티브 컨테이너를 교체할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-141">You can replace the default native container if you wish.</span></span> <span data-ttu-id="587a5-142">DI를 사용하면 느슨한 결합의 이점을 얻을 수 있을 뿐만 아니라, 앱 전체에서 서비스를 사용할 수 있습니다(예: [로깅](xref:fundamentals/logging/index)).</span><span class="sxs-lookup"><span data-stu-id="587a5-142">In addition to its loose coupling benefit, DI makes services available throughout your app (for example, [logging](xref:fundamentals/logging/index)).</span></span>

<span data-ttu-id="587a5-143">자세한 내용은 [종속성 주입](xref:fundamentals/dependency-injection)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-143">For more information, see [Dependency injection](xref:fundamentals/dependency-injection).</span></span>

## <a name="middleware"></a><span data-ttu-id="587a5-144">미들웨어</span><span class="sxs-lookup"><span data-stu-id="587a5-144">Middleware</span></span>

<span data-ttu-id="587a5-145">ASP.NET Core는 [미들웨어](xref:fundamentals/middleware/index)를 사용해서 요청 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-145">In ASP.NET Core, you compose your request pipeline using [middleware](xref:fundamentals/middleware/index).</span></span> <span data-ttu-id="587a5-146">ASP.NET Core의 미들웨어는 `HttpContext` 상에서 비동기 논리를 수행한 다음, 시퀀스 상의 다음 미들웨어를 호출하거나 그대로 요청을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-146">ASP.NET Core middleware performs asynchronous logic on an `HttpContext` and then either invokes the next middleware in the sequence or terminates the request directly.</span></span> <span data-ttu-id="587a5-147">일반적으로 "XYZ"라는 미들웨어 구성 요소는 `Configure` 메서드에서 `UseXYZ` 확장 메서드를 호출하는 방식으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-147">A middleware component called "XYZ" is added by invoking an `UseXYZ` extension method in the `Configure` method.</span></span>

<span data-ttu-id="587a5-148">ASP.NET Core는 다양한 기본 제공 미들웨어들을 함께 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-148">ASP.NET Core includes a rich set of built-in middleware:</span></span>

* [<span data-ttu-id="587a5-149">정적 파일</span><span class="sxs-lookup"><span data-stu-id="587a5-149">Static files</span></span>](xref:fundamentals/static-files)
* [<span data-ttu-id="587a5-150">라우팅</span><span class="sxs-lookup"><span data-stu-id="587a5-150">Routing</span></span>](xref:fundamentals/routing)
* [<span data-ttu-id="587a5-151">인증</span><span class="sxs-lookup"><span data-stu-id="587a5-151">Authentication</span></span>](xref:security/authentication/index)
* [<span data-ttu-id="587a5-152">응답 압축 미들웨어</span><span class="sxs-lookup"><span data-stu-id="587a5-152">Response Compression Middleware</span></span>](xref:performance/response-compression)
* [<span data-ttu-id="587a5-153">URL 재작성 미들웨어</span><span class="sxs-lookup"><span data-stu-id="587a5-153">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)

<span data-ttu-id="587a5-154">ASP.NET Core 앱에서 [OWIN](http://owin.org) 기반 미들웨어를 사용할 수 있으며, 직접 자신의 사용자 지정 미들웨어를 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-154">[OWIN](http://owin.org)-based middleware is available for ASP.NET Core apps, and you can write your own custom middleware.</span></span>

<span data-ttu-id="587a5-155">자세한 내용은 [미들웨어](xref:fundamentals/middleware/index) 및 [OWIN(Open Web Interface for .NET)](xref:fundamentals/owin)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-155">For more information, see [Middleware](xref:fundamentals/middleware/index) and [Open Web Interface for .NET (OWIN)](xref:fundamentals/owin).</span></span>

## <a name="initiate-http-requests"></a><span data-ttu-id="587a5-156">HTTP 요청 시작</span><span class="sxs-lookup"><span data-stu-id="587a5-156">Initiate HTTP requests</span></span>

<span data-ttu-id="587a5-157">`IHttpClientFactory`를 사용하여 `HttpClient` 인스턴스에 액세스하고 HTTP 요청을 만드는 방법은 [HTTP 요청 시작](xref:fundamentals/http-requests)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="587a5-157">For information about using `IHttpClientFactory` to access `HttpClient` instances to make HTTP requests, see [Initiate HTTP requests](xref:fundamentals/http-requests).</span></span>

## <a name="environments"></a><span data-ttu-id="587a5-158">환경</span><span class="sxs-lookup"><span data-stu-id="587a5-158">Environments</span></span>

<span data-ttu-id="587a5-159">"Development" 및 "Production" 같은 환경은 ASP.NET Core의 일급 개념으로, 환경 변수를 통해서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-159">Environments, such as "Development" and "Production", are a first-class notion in ASP.NET Core and can be set using environment variables.</span></span>

<span data-ttu-id="587a5-160">자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-160">For more information, see [Work with multiple environments](xref:fundamentals/environments).</span></span>

## <a name="configuration"></a><span data-ttu-id="587a5-161">구성</span><span class="sxs-lookup"><span data-stu-id="587a5-161">Configuration</span></span>

<span data-ttu-id="587a5-162">ASP.NET Core는 이름 값 쌍에 기반을 둔 구성 모델을 사용합니다. </span><span class="sxs-lookup"><span data-stu-id="587a5-162">ASP.NET Core uses a configuration model based on name-value pairs.</span></span> <span data-ttu-id="587a5-163">이 구성 모델은 `System.Configuration` 이나 *web.config*를 기반으로 하지 않습니다. 구성은 정렬된 구성 공급자 집합에서 설정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-163">The configuration model isn't based on `System.Configuration` or *web.config*. Configuration obtains settings from an ordered set of configuration providers.</span></span> <span data-ttu-id="587a5-164">기본으로 제공되는 구성 공급자는 환경 기반 구성을 가능하게 해주는 다양한 파일 형식(XML, JSON, INI)과 환경 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-164">The built-in configuration providers support a variety of file formats (XML, JSON, INI) and environment variables to enable environment-based configuration.</span></span> <span data-ttu-id="587a5-165">또는 직접 자신의 사용자 지정 구성 공급자를 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-165">You can also write your own custom configuration providers.</span></span>

<span data-ttu-id="587a5-166">자세한 내용은 [구성](xref:fundamentals/configuration/index)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-166">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

## <a name="logging"></a><span data-ttu-id="587a5-167">로깅</span><span class="sxs-lookup"><span data-stu-id="587a5-167">Logging</span></span>

<span data-ttu-id="587a5-168">ASP.NET Core는 다양한 로깅 공급자를 사용하는 로깅 API를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-168">ASP.NET Core supports a logging API that works with a variety of logging providers.</span></span> <span data-ttu-id="587a5-169">기본으로 제공되는 공급자는 하나 이상의 대상에 로그를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-169">Built-in providers support sending logs to one or more destinations.</span></span> <span data-ttu-id="587a5-170">타사의 로깅 프레임워크를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-170">Third-party logging frameworks can be used.</span></span>

[<span data-ttu-id="587a5-171">로깅</span><span class="sxs-lookup"><span data-stu-id="587a5-171">Logging</span></span>](xref:fundamentals/logging/index)

## <a name="error-handling"></a><span data-ttu-id="587a5-172">오류 처리</span><span class="sxs-lookup"><span data-stu-id="587a5-172">Error handling</span></span>

<span data-ttu-id="587a5-173">ASP.NET Core는 앱에서 오류를 처리하기 위한 개발자 예외 페이지, 사용자 지정 오류 페이지, 정적 상태 코드 페이지 및 시작 예외 처리 등의 기본 제공 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-173">ASP.NET Core has built-in features for handling errors in apps, including a developer exception page, custom error pages, static status code pages, and startup exception handling.</span></span>

<span data-ttu-id="587a5-174">자세한 내용은 [오류를 처리하는 방법](xref:fundamentals/error-handling)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="587a5-174">For more information, see [how to handle errors](xref:fundamentals/error-handling).</span></span>

## <a name="routing"></a><span data-ttu-id="587a5-175">라우팅</span><span class="sxs-lookup"><span data-stu-id="587a5-175">Routing</span></span>

<span data-ttu-id="587a5-176">ASP.NET Core는 응용 프로그램 요청을 경로 처리기로 라우팅하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-176">ASP.NET Core offers features for routing of app requests to route handlers.</span></span>

<span data-ttu-id="587a5-177">자세한 내용은 [라우팅](xref:fundamentals/routing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="587a5-177">For more information, see [Routing](xref:fundamentals/routing).</span></span>

## <a name="file-providers"></a><span data-ttu-id="587a5-178">파일 공급자</span><span class="sxs-lookup"><span data-stu-id="587a5-178">File providers</span></span>

<span data-ttu-id="587a5-179">ASP.NET Core는 파일 공급자를 사용하여 파일 시스템 액세스를 추상화하고 플랫폼에서 파일을 사용하기 위한 공통 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-179">ASP.NET Core abstracts file system access through the use of File Providers, which offers a common interface for working with files across platforms.</span></span>

<span data-ttu-id="587a5-180">자세한 내용은 [파일 공급자](xref:fundamentals/file-providers)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-180">For more information, see [File Providers](xref:fundamentals/file-providers).</span></span>

## <a name="static-files"></a><span data-ttu-id="587a5-181">정적 파일</span><span class="sxs-lookup"><span data-stu-id="587a5-181">Static files</span></span>

<span data-ttu-id="587a5-182">정적 파일 미들웨어는 HTML, CSS, 이미지, JavaScript 등의 정적 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-182">Static files middleware serves static files, such as HTML, CSS, image, and JavaScript.</span></span>

<span data-ttu-id="587a5-183">자세한 내용은 [고정 파일 작업](xref:fundamentals/static-files)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="587a5-183">For more information, see [Work with static files](xref:fundamentals/static-files).</span></span>

## <a name="hosting"></a><span data-ttu-id="587a5-184">호스팅</span><span class="sxs-lookup"><span data-stu-id="587a5-184">Hosting</span></span>

<span data-ttu-id="587a5-185">ASP.NET Core 앱은 앱의 시작과 수명 관리를 담당하는 *호스트*를 구성하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-185">ASP.NET Core apps configure and launch a *host*, which is responsible for app startup and lifetime management.</span></span>

<span data-ttu-id="587a5-186">자세한 내용은 [호스팅](xref:fundamentals/hosting)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="587a5-186">For more information, see [Hosting](xref:fundamentals/hosting).</span></span>

## <a name="session-and-application-state"></a><span data-ttu-id="587a5-187">세션 및 응용 프로그램 상태</span><span class="sxs-lookup"><span data-stu-id="587a5-187">Session and application state</span></span>

<span data-ttu-id="587a5-188">세션 상태는 사용자가 웹앱을 탐색하는 동안 사용자 데이터를 저장하는 데 사용할 수 있는 ASP.NET Core의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-188">Session state is a feature in ASP.NET Core that you can use to save and store user data while the user browses your web app.</span></span>

<span data-ttu-id="587a5-189">자세한 내용은 [세션 및 응용 프로그램 상태](xref:fundamentals/app-state)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-189">For more information, see [Session and application state](xref:fundamentals/app-state).</span></span>

## <a name="servers"></a><span data-ttu-id="587a5-190">서버</span><span class="sxs-lookup"><span data-stu-id="587a5-190">Servers</span></span>

<span data-ttu-id="587a5-191">ASP.NET Core의 호스팅 모델은 요청을 직접 수신하지 않습니다. </span><span class="sxs-lookup"><span data-stu-id="587a5-191">The ASP.NET Core hosting model doesn't directly listen for requests.</span></span> <span data-ttu-id="587a5-192">대신 호스팅 모델은 HTTP 서버 구현에 의존해서 요청을 앱에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-192">The hosting model relies on an HTTP server implementation to forward the request to the app.</span></span> <span data-ttu-id="587a5-193">전달된 요청은 인터페이스를 통해서 접근할 수 있는 기능 개체 집합으로 래핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-193">The forwarded request is wrapped as a set of feature objects that can be accessed through interfaces.</span></span> <span data-ttu-id="587a5-194">ASP.NET Core에는 [Kestrel](xref:fundamentals/servers/kestrel)이라는 관리되는 크로스 플랫폼 웹 서버가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-194">ASP.NET Core includes a managed, cross-platform web server, called [Kestrel](xref:fundamentals/servers/kestrel).</span></span> <span data-ttu-id="587a5-195">일반적으로 Kestrel은 [IIS](https://www.iis.net/) 또는 [Nginx](http://nginx.org)같은 프로덕션 웹 서버의 뒤에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-195">Kestrel is often run behind a production web server, such as [IIS](https://www.iis.net/) or [Nginx](http://nginx.org).</span></span> <span data-ttu-id="587a5-196">Kestrel은 에지 서버로 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-196">Kestrel can be run as an edge server.</span></span>

<span data-ttu-id="587a5-197">자세한 내용은 [서버](xref:fundamentals/servers/index) 및 다음 항목을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-197">For more information, see [Servers](xref:fundamentals/servers/index) and the following topics:</span></span>

* [<span data-ttu-id="587a5-198">Kestrel</span><span class="sxs-lookup"><span data-stu-id="587a5-198">Kestrel</span></span>](xref:fundamentals/servers/kestrel)
* [<span data-ttu-id="587a5-199">ASP.NET Core 모듈</span><span class="sxs-lookup"><span data-stu-id="587a5-199">ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* <span data-ttu-id="587a5-200">[HTTP.sys](xref:fundamentals/servers/httpsys)(구 [WebListener](xref:fundamentals/servers/weblistener))</span><span class="sxs-lookup"><span data-stu-id="587a5-200">[HTTP.sys](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener))</span></span>

## <a name="globalization-and-localization"></a><span data-ttu-id="587a5-201">전역화 및 지역화</span><span class="sxs-lookup"><span data-stu-id="587a5-201">Globalization and localization</span></span>

<span data-ttu-id="587a5-202">ASP.NET Core를 사용해서 다국어 웹 사이트를 만들면 더 광범위한 사용자가 사이트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-202">Creating a multilingual website with ASP.NET Core allows your site to reach a wider audience.</span></span> <span data-ttu-id="587a5-203">ASP.NET Core는 다른 언어 및 문화권의 지역화를 위한 서비스 및 미들웨어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-203">ASP.NET Core provides services and middleware for localizing into different languages and cultures.</span></span>

<span data-ttu-id="587a5-204">자세한 내용은 [전역화 및 지역화](xref:fundamentals/localization)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="587a5-204">For more information, see [Globalization and localization](xref:fundamentals/localization).</span></span>

## <a name="request-features"></a><span data-ttu-id="587a5-205">요청 기능</span><span class="sxs-lookup"><span data-stu-id="587a5-205">Request features</span></span>

<span data-ttu-id="587a5-206">웹 서버 구현은 HTTP 요청과 관련하여 설명되고 응답은 인터페이스에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-206">Web server implementation details related to HTTP requests and responses are defined in interfaces.</span></span> <span data-ttu-id="587a5-207">이 인터페이스들은 서버 구현 및 미들웨어에서 앱의 호스팅 파이프라인을 만들고 수정하기 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-207">These interfaces are used by server implementations and middleware to create and modify the app's hosting pipeline.</span></span>

<span data-ttu-id="587a5-208">자세한 내용은 [요청 기능](xref:fundamentals/request-features)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-208">For more information, see [Request Features](xref:fundamentals/request-features).</span></span>

## <a name="background-tasks"></a><span data-ttu-id="587a5-209">백그라운드 작업</span><span class="sxs-lookup"><span data-stu-id="587a5-209">Background tasks</span></span>

<span data-ttu-id="587a5-210">백그라운드 작업은 *호스티드 서비스*로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-210">Background tasks are implemented as *hosted services*.</span></span> <span data-ttu-id="587a5-211">호스티드 서비스는 [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 인터페이스를 구현하는 백그라운드 작업 논리가 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-211">A hosted service is a class with background task logic that implements the [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) interface.</span></span>

<span data-ttu-id="587a5-212">자세한 내용은 [호스티드 서비스를 사용하는 백그라운드 작업](xref:fundamentals/hosted-services)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="587a5-212">For more information, see [Background tasks with hosted services](xref:fundamentals/hosted-services).</span></span>

## <a name="open-web-interface-for-net-owin"></a><span data-ttu-id="587a5-213">OWIN(Open Web Interface for .NET)</span><span class="sxs-lookup"><span data-stu-id="587a5-213">Open Web Interface for .NET (OWIN)</span></span>

<span data-ttu-id="587a5-214">ASP.NET Core는 OWIN(Open Web Interface for .NET)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-214">ASP.NET Core supports the Open Web Interface for .NET (OWIN).</span></span> <span data-ttu-id="587a5-215">OWIN을 사용하면 웹 앱을 웹 서버에서 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-215">OWIN allows web apps to be decoupled from web servers.</span></span>

<span data-ttu-id="587a5-216">자세한 내용은 [OWIN(Open Web Interface for .NET)](xref:fundamentals/owin)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="587a5-216">For more information, see [Open Web Interface for .NET (OWIN)](xref:fundamentals/owin).</span></span>

## <a name="websockets"></a><span data-ttu-id="587a5-217">WebSocket</span><span class="sxs-lookup"><span data-stu-id="587a5-217">WebSockets</span></span>

<span data-ttu-id="587a5-218">[WebSocket](https://wikipedia.org/wiki/WebSocket)은 TCP 연결을 통한 영구 양방향 통신 채널을 사용하도록 설정하는 프로토콜이며</span><span class="sxs-lookup"><span data-stu-id="587a5-218">[WebSocket](https://wikipedia.org/wiki/WebSocket) is a protocol that enables two-way persistent communication channels over TCP connections.</span></span> <span data-ttu-id="587a5-219">WebSocket은 채팅, 주식 시세, 게임 등 웹 앱에서 실시간 기능이 필요한 모든 곳에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-219">It's used for apps such as chat, stock tickers, games, and anywhere you desire real-time functionality in a web app.</span></span> <span data-ttu-id="587a5-220">ASP.NET Core는 WebSocket 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-220">ASP.NET Core supports web socket features.</span></span>

<span data-ttu-id="587a5-221">자세한 내용은 [WebSocket](xref:fundamentals/websockets)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="587a5-221">For more information, see [WebSockets](xref:fundamentals/websockets).</span></span>

## <a name="microsoftaspnetcoreall-metapackage"></a><span data-ttu-id="587a5-222">Microsoft.AspNetCore.All 메타패키지</span><span class="sxs-lookup"><span data-stu-id="587a5-222">Microsoft.AspNetCore.All metapackage</span></span>

<span data-ttu-id="587a5-223">ASP.NET Core에 대한 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 메타패키지는 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-223">The [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage for ASP.NET Core includes:</span></span>

* <span data-ttu-id="587a5-224">ASP.NET Core 팀에서 지원되는 모든 패키지</span><span class="sxs-lookup"><span data-stu-id="587a5-224">All supported packages by the ASP.NET Core team.</span></span>
* <span data-ttu-id="587a5-225">Entity Framework Core에서 지원되는 모든 패키지</span><span class="sxs-lookup"><span data-stu-id="587a5-225">All supported packages by the Entity Framework Core.</span></span> 
* <span data-ttu-id="587a5-226">ASP.NET Core 및 Entity Framework Core에서 사용하는 내부 및 타사 종속성</span><span class="sxs-lookup"><span data-stu-id="587a5-226">Internal and 3rd-party dependencies used by ASP.NET Core and Entity Framework Core.</span></span>

<span data-ttu-id="587a5-227">자세한 내용은 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-227">For more information, see [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

## <a name="net-core-vs-net-framework-runtime"></a><span data-ttu-id="587a5-228">.NET Core 및 .NET Framework 런타임</span><span class="sxs-lookup"><span data-stu-id="587a5-228">.NET Core vs. .NET Framework runtime</span></span>

<span data-ttu-id="587a5-229">ASP.NET Core 앱은 .NET Core 또는 .NET Framework 런타임을 대상으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-229">An ASP.NET Core app can target the .NET Core or .NET Framework runtime.</span></span>

<span data-ttu-id="587a5-230">자세한 내용은 [.NET Core와 .NET Framework  중에 선택하기](/dotnet/articles/standard/choosing-core-framework-server)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-230">For more information, see [Choosing between .NET Core and .NET Framework](/dotnet/articles/standard/choosing-core-framework-server).</span></span>

## <a name="choose-between-aspnet-core-and-aspnet"></a><span data-ttu-id="587a5-231">ASP.NET Core와 ASP.NET 중에서 선택하기</span><span class="sxs-lookup"><span data-stu-id="587a5-231">Choose between ASP.NET Core and ASP.NET</span></span>

<span data-ttu-id="587a5-232">ASP.NET Core와 ASP.NET 중에서 선택하는 방법에 대한 자세한 내용은 [ASP.NET Core 및 ASP.NET 중에서 선택하기](xref:fundamentals/choose-between-aspnet-and-aspnetcore)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="587a5-232">For more information on choosing between ASP.NET Core and ASP.NET, see [Choose between ASP.NET Core and ASP.NET](xref:fundamentals/choose-between-aspnet-and-aspnetcore).</span></span>
