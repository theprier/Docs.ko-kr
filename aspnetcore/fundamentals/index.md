---
title: ASP.NET Core 기본 사항
author: rick-anderson
description: ASP.NET Core 앱을 구축하기 위한 기본적인 개념을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 10/25/2018
uid: fundamentals/index
ms.openlocfilehash: 56344315acc59003248ffaf1e61455b94a93a545
ms.sourcegitcommit: 4d74644f11e0dac52b4510048490ae731c691496
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50090721"
---
# <a name="aspnet-core-fundamentals"></a><span data-ttu-id="59d8f-103">ASP.NET Core 기본 사항</span><span class="sxs-lookup"><span data-stu-id="59d8f-103">ASP.NET Core fundamentals</span></span>

<span data-ttu-id="59d8f-104">ASP.NET Core 앱은 `Program.Main` 메서드에서 웹 서버를 생성하는 콘솔 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-104">An ASP.NET Core app is a console app that creates a web server in its `Program.Main` method.</span></span> <span data-ttu-id="59d8f-105">`Main` 메서드는 앱의 *관리 진입점*입니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-105">The `Main` method is the app's *managed entry point*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/snapshots/2.x/Program.cs)]

<span data-ttu-id="59d8f-106">.NET Core 호스트:</span><span class="sxs-lookup"><span data-stu-id="59d8f-106">The .NET Core Host:</span></span>

* <span data-ttu-id="59d8f-107">[.NET Core 런타임](https://github.com/dotnet/coreclr)을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-107">Loads the [.NET Core runtime](https://github.com/dotnet/coreclr).</span></span>
* <span data-ttu-id="59d8f-108">첫 번째 명령줄 인수를 진입점(`Main`)을 포함하는 관리되는 이진 경로로 사용하고 코드 실행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-108">Uses the first command-line argument as the path to the managed binary that contains the entry point (`Main`) and begins code execution.</span></span>

<span data-ttu-id="59d8f-109">`Main` 메서드는 [빌드 패턴](https://wikipedia.org/wiki/Builder_pattern)에 따라 웹 응용 프로그램 호스트를 생성하는 [WebHost.CreateDefaultBuilder](xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-109">The `Main` method invokes [WebHost.CreateDefaultBuilder](xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*), which follows the [builder pattern](https://wikipedia.org/wiki/Builder_pattern) to create a web host.</span></span> <span data-ttu-id="59d8f-110">이 빌더는 웹 서버를 정의하거나 (예: <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*>) 시작 클래스를 정의하는 (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*>) 메서드들을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-110">The builder has methods that define the web server (for example, <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*>) and the startup class (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*>).</span></span> <span data-ttu-id="59d8f-111">위의 예제에서는 기본적으로 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버가 할당되며.</span><span class="sxs-lookup"><span data-stu-id="59d8f-111">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is automatically allocated.</span></span> <span data-ttu-id="59d8f-112">가능하다면 ASP.NET Core의 웹 호스트는 IIS에서 실행하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-112">ASP.NET Core's web host attempts to run on IIS, if available.</span></span> <span data-ttu-id="59d8f-113">그러나 적절한 확장 메서드를 호출해서 [HTTP.sys](xref:fundamentals/servers/httpsys) 같은 다른 웹 서버를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-113">Other web servers, such as [HTTP.sys](xref:fundamentals/servers/httpsys), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="59d8f-114">`UseStartup` 에 관해서는 다음 섹션에서 더 자세히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-114">`UseStartup` is explained further in the next section.</span></span>

<span data-ttu-id="59d8f-115">`WebHost.CreateDefaultBuilder` 호출로부터 반환되는 <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder>형식은 다양한 선택적 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-115"><xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder>, the return type of the `WebHost.CreateDefaultBuilder` invocation, provides many optional methods.</span></span> <span data-ttu-id="59d8f-116">이 메서드들 중에는 HTTP.sys에서 앱을 호스트하기 위한 `UseHttpSys` 및 루트 콘텐츠 디렉터리를 지정하기 위한 <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseContentRoot*>도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-116">Some of these methods include `UseHttpSys` for hosting the app in HTTP.sys and <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseContentRoot*> for specifying the root content directory.</span></span> <span data-ttu-id="59d8f-117"><xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.Build*> 및 <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> 메서드는 앱을 호스트하고 HTTP 요청의 수신 대기를 시작하는 <xref:Microsoft.AspNetCore.Hosting.IWebHost> 개체를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-117">The <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.Build*> and <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> methods build the <xref:Microsoft.AspNetCore.Hosting.IWebHost> object that hosts the app and begins listening for HTTP requests.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/snapshots/1.x/Program.cs)]

<span data-ttu-id="59d8f-118">.NET Core 호스트:</span><span class="sxs-lookup"><span data-stu-id="59d8f-118">The .NET Core Host:</span></span>

* <span data-ttu-id="59d8f-119">[.NET Core 런타임](https://github.com/dotnet/coreclr)을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-119">Loads the [.NET Core runtime](https://github.com/dotnet/coreclr).</span></span>
* <span data-ttu-id="59d8f-120">첫 번째 명령줄 인수를 진입점(`Main`)을 포함하는 관리되는 이진 경로로 사용하고 코드 실행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-120">Uses the first command-line argument as the path to the managed binary that contains the entry point (`Main`) and begins code execution.</span></span>

<span data-ttu-id="59d8f-121">`Main` 메서드는 [빌드 패턴](https://wikipedia.org/wiki/Builder_pattern)에 따라 웹앱 호스트를 만드는 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-121">The `Main` method uses <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>, which follows the [builder pattern](https://wikipedia.org/wiki/Builder_pattern) to create a web app host.</span></span> <span data-ttu-id="59d8f-122">이 빌더는 웹 서버를 정의하거나 (예: <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*>) 시작 클래스를 정의하는 (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*>) 메서드들을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-122">The builder has methods that define the web server (for example, <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*>) and the startup class (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*>).</span></span> <span data-ttu-id="59d8f-123">위의 예제에서는 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버를 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-123">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is used.</span></span> <span data-ttu-id="59d8f-124">[WebListener](xref:fundamentals/servers/weblistener) 같은 다른 웹 서버를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-124">Other web servers, such as [WebListener](xref:fundamentals/servers/weblistener), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="59d8f-125">`UseStartup`에 관해서는 다음 섹션에서 더 자세히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-125">`UseStartup` is explained further in the next section.</span></span>

<span data-ttu-id="59d8f-126">`WebHostBuilder`는 IIS 및 IIS Express에서 호스팅하기 위한 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> 확장 메서드 및 루트 콘텐츠 디렉터리를 지정하기 위한 <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseContentRoot*>확장 메서드를 비롯한 다양한 선택적 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-126">`WebHostBuilder` provides many optional methods, including <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> for hosting in IIS and IIS Express and <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseContentRoot*> for specifying the root content directory.</span></span> <span data-ttu-id="59d8f-127"><xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.Build*> 및 <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> 메서드는 앱을 호스트하고 HTTP 요청의 수신 대기를 시작하는 <xref:Microsoft.AspNetCore.Hosting.IWebHost> 개체를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-127">The <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.Build*> and <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> methods build the <xref:Microsoft.AspNetCore.Hosting.IWebHost> object that hosts the app and begins listening for HTTP requests.</span></span>

::: moniker-end

## <a name="startup"></a><span data-ttu-id="59d8f-128">Startup 클래스</span><span class="sxs-lookup"><span data-stu-id="59d8f-128">Startup</span></span>

<span data-ttu-id="59d8f-129">`WebHostBuilder`의 `UseStartup` 메서드는 앱의 `Startup` 클래스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-129">The `UseStartup` method on `WebHostBuilder` specifies the `Startup` class for your app:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/snapshots/2.x/Program.cs?highlight=10)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/snapshots/1.x/Program.cs?highlight=7)]

::: moniker-end

<span data-ttu-id="59d8f-130">`Startup` 클래스는 요청 처리 파이프라인을 정의하고 앱에 필요한 모든 서비스를 구성하는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-130">The `Startup` class is where you define the request handling pipeline and where any services needed by the app are configured.</span></span> <span data-ttu-id="59d8f-131">`Startup` 클래스는 public으로 지정해야 하며 다음과 같은 메서드들을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-131">The `Startup` class must be public and contain the following methods:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/snapshots/2.x/Startup.cs)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/snapshots/1.x/Startup.cs)]

::: moniker-end

<span data-ttu-id="59d8f-132"><xref:Microsoft.AspNetCore.Hosting.IStartup.ConfigureServices*>는 앱에서 사용되는 [서비스](#dependency-injection-services)를 정의합니다 (예, ASP.NET MVC Core MVC, Entity Framework Core, Identity).</span><span class="sxs-lookup"><span data-stu-id="59d8f-132"><xref:Microsoft.AspNetCore.Hosting.IStartup.ConfigureServices*> defines the [Services](#dependency-injection-services) used by your app (for example, ASP.NET Core MVC, Entity Framework Core, Identity).</span></span> <span data-ttu-id="59d8f-133"><xref:Microsoft.AspNetCore.Hosting.IStartup.Configure*>는 요청 파이프라인에서 호출되는 [미들웨어](xref:fundamentals/middleware/index)를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-133"><xref:Microsoft.AspNetCore.Hosting.IStartup.Configure*> defines the [middleware](xref:fundamentals/middleware/index) called in the request pipeline.</span></span>

<span data-ttu-id="59d8f-134">자세한 내용은 <xref:fundamentals/startup>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-134">For more information, see <xref:fundamentals/startup>.</span></span>

## <a name="content-root"></a><span data-ttu-id="59d8f-135">콘텐츠 루트</span><span class="sxs-lookup"><span data-stu-id="59d8f-135">Content root</span></span>

<span data-ttu-id="59d8f-136">콘텐츠 루트는 앱에서 사용되는 [Razor Pages](xref:razor-pages/index), MVC 보기, 정적 자산 같은 콘텐츠의 기본 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-136">The content root is the base path to any content used by the app, such as [Razor Pages](xref:razor-pages/index), MVC views, and static assets.</span></span> <span data-ttu-id="59d8f-137">기본적으로 콘텐츠 루트는 앱을 호스팅하는 실행 파일의 앱 기본 경로와 동일한 위치입니다. </span><span class="sxs-lookup"><span data-stu-id="59d8f-137">By default, the content root is the same location as the app base path for the executable hosting the app.</span></span>

## <a name="web-root-webroot"></a><span data-ttu-id="59d8f-138">웹 루트(webroot)</span><span class="sxs-lookup"><span data-stu-id="59d8f-138">Web root (webroot)</span></span>

<span data-ttu-id="59d8f-139">앱의 웹 루트는 CSS, JavaScript 및 이미지 파일과 같은 공용, 정적 리소스를 포함하는 프로젝트의 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-139">The webroot of an app is the directory in the project containing public, static resources, such as CSS, JavaScript, and image files.</span></span> <span data-ttu-id="59d8f-140">기본적으로 *wwwroot*는 웹 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-140">By default, *wwwroot* is the webroot.</span></span>

<span data-ttu-id="59d8f-141">Razor(*.cshtml*) 파일의 경우 물결표 슬래시 `~/`가 웹 루트를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-141">For Razor (*.cshtml*) files, the tilde-slash  `~/` points to the webroot.</span></span> <span data-ttu-id="59d8f-142">`~/`에서 시작하는 경로를 가상 경로라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-142">Paths beginning with `~/` are referred to as virtual paths.</span></span>

## <a name="dependency-injection-services"></a><span data-ttu-id="59d8f-143">종속성 주입(서비스)</span><span class="sxs-lookup"><span data-stu-id="59d8f-143">Dependency injection (services)</span></span>

<span data-ttu-id="59d8f-144">*서비스*는 앱에서 공통으로 사용하기 위한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-144">A *service* is a component that's intended for common consumption in an app.</span></span> <span data-ttu-id="59d8f-145">서비스는 DI([종속성 주입](xref:fundamentals/dependency-injection))를 통해서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-145">Services are made available through [dependency injection (DI)](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="59d8f-146">ASP.NET Core에는 기본적으로 [생성자 주입](xref:mvc/controllers/dependency-injection#constructor-injection)을 지원하는 네이티브 IoC(Inversion of Control) 컨테이너가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-146">ASP.NET Core includes a native Inversion of Control (IoC) container that supports [constructor injection](xref:mvc/controllers/dependency-injection#constructor-injection) by default.</span></span> <span data-ttu-id="59d8f-147">만약 원한다면 기본 컨테이너를 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-147">You can replace the default container if you wish.</span></span> <span data-ttu-id="59d8f-148">DI를 사용하면 [느슨한 결합의 이점](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#encapsulation)을 얻을 수 있을 뿐만 아니라, 앱 전체에서 [로깅](xref:fundamentals/logging/index) 같은 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-148">In addition to its [loose coupling benefit](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#encapsulation), DI makes services, such as [logging](xref:fundamentals/logging/index), available throughout your app.</span></span>

<span data-ttu-id="59d8f-149">자세한 내용은 <xref:fundamentals/dependency-injection>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-149">For more information, see <xref:fundamentals/dependency-injection>.</span></span>

## <a name="middleware"></a><span data-ttu-id="59d8f-150">미들웨어</span><span class="sxs-lookup"><span data-stu-id="59d8f-150">Middleware</span></span>

<span data-ttu-id="59d8f-151">ASP.NET Core는 [미들웨어](xref:fundamentals/middleware/index)를 사용해서 요청 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-151">In ASP.NET Core, you compose your request pipeline using [middleware](xref:fundamentals/middleware/index).</span></span> <span data-ttu-id="59d8f-152">ASP.NET Core 미들웨어는 `HttpContext` 상에서 비동기 작업을 수행한 다음, 파이프라인의 다음 미들웨어를 호출하거나 요청을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-152">ASP.NET Core middleware performs asynchronous operations on an `HttpContext` and then either invokes the next middleware in the pipeline or terminates the request.</span></span>

<span data-ttu-id="59d8f-153">규칙에 따라, "XYZ"라는 미들웨어 구성 요소는 `Configure` 메서드에서 `UseXYZ` 확장 메서드를 호출하여 파이프라인에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-153">By convention, a middleware component called "XYZ" is added to the pipeline by invoking a `UseXYZ` extension method in the `Configure` method.</span></span>

<span data-ttu-id="59d8f-154">ASP.NET Core는 풍부한 기본 미들웨어 집합을 포함하고 있으며, 자신만의 사용자 지정 미들웨어를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-154">ASP.NET Core includes a rich set of built-in middleware, and you can write your own custom middleware.</span></span> <span data-ttu-id="59d8f-155">웹 서버에서 웹앱을 분리할 수 있게 해주는 [OWIN(Open Web Interface for .NET)](xref:fundamentals/owin)은 ASP.NET Core 앱에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-155">[Open Web Interface for .NET (OWIN)](xref:fundamentals/owin), which allows web apps to be decoupled from web servers, is supported in ASP.NET Core apps.</span></span>

<span data-ttu-id="59d8f-156">자세한 내용은 <xref:fundamentals/middleware/index> 및 <xref:fundamentals/owin>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-156">For more information, see <xref:fundamentals/middleware/index> and <xref:fundamentals/owin>.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="initiate-http-requests"></a><span data-ttu-id="59d8f-157">HTTP 요청 시작</span><span class="sxs-lookup"><span data-stu-id="59d8f-157">Initiate HTTP requests</span></span>

<span data-ttu-id="59d8f-158"><xref:System.Net.Http.IHttpClientFactory>를 사용하여 HTTP 요청을 만드는 <xref:System.Net.Http.HttpClient> 인스턴스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-158"><xref:System.Net.Http.IHttpClientFactory> is available to access <xref:System.Net.Http.HttpClient> instances to make HTTP requests.</span></span>

<span data-ttu-id="59d8f-159">자세한 내용은 <xref:fundamentals/http-requests>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-159">For more information, see <xref:fundamentals/http-requests>.</span></span>

::: moniker-end

## <a name="environments"></a><span data-ttu-id="59d8f-160">환경</span><span class="sxs-lookup"><span data-stu-id="59d8f-160">Environments</span></span>

<span data-ttu-id="59d8f-161">*개발* 및 *프로덕션* 같은 환경은 ASP.NET Core의 일급 개념이며 환경 변수, 설정 파일, 명령줄 인수를 사용하여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-161">Environments, such as *Development* and *Production*, are a first-class notion in ASP.NET Core and can be set using an environment variable, settings file, and command-line argument.</span></span>

<span data-ttu-id="59d8f-162">자세한 내용은 <xref:fundamentals/environments>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-162">For more information, see <xref:fundamentals/environments>.</span></span>

## <a name="hosting"></a><span data-ttu-id="59d8f-163">호스팅</span><span class="sxs-lookup"><span data-stu-id="59d8f-163">Hosting</span></span>

<span data-ttu-id="59d8f-164">ASP.NET Core 앱은 앱의 시작과 수명 관리를 담당하는 *호스트*를 구성하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-164">ASP.NET Core apps configure and launch a *host*, which is responsible for app startup and lifetime management.</span></span>

<span data-ttu-id="59d8f-165">자세한 내용은 <xref:fundamentals/host/index>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-165">For more information, see <xref:fundamentals/host/index>.</span></span>

## <a name="servers"></a><span data-ttu-id="59d8f-166">서버</span><span class="sxs-lookup"><span data-stu-id="59d8f-166">Servers</span></span>

<span data-ttu-id="59d8f-167">ASP.NET Core의 호스팅 모델은 요청을 직접 수신하지 않습니다. </span><span class="sxs-lookup"><span data-stu-id="59d8f-167">The ASP.NET Core hosting model doesn't directly listen for requests.</span></span> <span data-ttu-id="59d8f-168">대신 호스팅 모델은 HTTP 서버 구현에 의존해서 요청을 앱에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-168">The hosting model relies on an HTTP server implementation to forward the request to the app.</span></span> <span data-ttu-id="59d8f-169">전달된 요청은 인터페이스를 통해서 접근할 수 있는 기능 개체 집합으로 래핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-169">The forwarded request is wrapped as a set of feature objects that can be accessed through interfaces.</span></span> <span data-ttu-id="59d8f-170">ASP.NET Core에는 [Kestrel](xref:fundamentals/servers/kestrel)이라는 관리되는 크로스 플랫폼 웹 서버가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-170">ASP.NET Core includes a managed, cross-platform web server, called [Kestrel](xref:fundamentals/servers/kestrel).</span></span> <span data-ttu-id="59d8f-171">Kestrel은 일반적으로 역방향 프록시 구성의 [IIS](https://www.iis.net/) 또는 [Nginx](http://nginx.org) 같은 프로덕션 웹 서버 뒤에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-171">Kestrel is commonly run behind a production web server, such as [IIS](https://www.iis.net/) or [Nginx](http://nginx.org) in a reverse proxy configuration.</span></span> <span data-ttu-id="59d8f-172">kestrel은 ASP.NET Core 2.0 이상에서 인터넷에 직접 공개되는 공용 에지 서버로 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-172">Kestrel can also be run as a public-facing edge server exposed directly to the Internet in ASP.NET Core 2.0 or later.</span></span>

<span data-ttu-id="59d8f-173">자세한 내용은 <xref:fundamentals/servers/index>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-173">For more information, see <xref:fundamentals/servers/index>.</span></span>

## <a name="configuration"></a><span data-ttu-id="59d8f-174">구성</span><span class="sxs-lookup"><span data-stu-id="59d8f-174">Configuration</span></span>

<span data-ttu-id="59d8f-175">ASP.NET Core는 이름 값 쌍에 기반을 둔 구성 모델을 사용합니다. </span><span class="sxs-lookup"><span data-stu-id="59d8f-175">ASP.NET Core uses a configuration model based on name-value pairs.</span></span> <span data-ttu-id="59d8f-176">이 구성 모델은 <xref:System.Configuration> 이나 *web.config*를 기반으로 하지 않습니다. 구성은 정렬된 구성 공급자 집합에서 설정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-176">The configuration model isn't based on <xref:System.Configuration> or *web.config*. Configuration obtains settings from an ordered set of configuration providers.</span></span> <span data-ttu-id="59d8f-177">기본적으로 제공되는 구성 공급자는 다양한 파일 형식(XML, JSON, INI), 환경 변수 및 명령줄 인수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-177">The built-in configuration providers support a variety of file formats (XML, JSON, INI), environment variables, and command-line arguments.</span></span> <span data-ttu-id="59d8f-178">또는 직접 자신의 사용자 지정 구성 공급자를 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-178">You can also write your own custom configuration providers.</span></span>

<span data-ttu-id="59d8f-179">자세한 내용은 <xref:fundamentals/configuration/index>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-179">For more information, see <xref:fundamentals/configuration/index>.</span></span>

## <a name="logging"></a><span data-ttu-id="59d8f-180">로깅</span><span class="sxs-lookup"><span data-stu-id="59d8f-180">Logging</span></span>

<span data-ttu-id="59d8f-181">ASP.NET Core는 다양한 로깅 공급자를 사용하는 로깅 API를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-181">ASP.NET Core supports a Logging API that works with a variety of logging providers.</span></span> <span data-ttu-id="59d8f-182">기본으로 제공되는 공급자는 하나 이상의 대상에 로그를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-182">Built-in providers support sending logs to one or more destinations.</span></span> <span data-ttu-id="59d8f-183">타사의 로깅 프레임워크를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-183">Third-party logging frameworks can be used.</span></span>

<span data-ttu-id="59d8f-184">자세한 내용은 <xref:fundamentals/logging/index>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-184">For more information, see <xref:fundamentals/logging/index>.</span></span>

## <a name="error-handling"></a><span data-ttu-id="59d8f-185">오류 처리</span><span class="sxs-lookup"><span data-stu-id="59d8f-185">Error handling</span></span>

<span data-ttu-id="59d8f-186">ASP.NET Core는 앱에서 오류를 처리하기 위한 개발자 예외 페이지, 사용자 지정 오류 페이지, 정적 상태 코드 페이지 및 시작 예외 처리 등의 기본 시나리오를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-186">ASP.NET Core has built-in scenarios for handling errors in apps, including a developer exception page, custom error pages, static status code pages, and startup exception handling.</span></span>

<span data-ttu-id="59d8f-187">자세한 내용은 <xref:fundamentals/error-handling>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-187">For more information, see <xref:fundamentals/error-handling>.</span></span>

## <a name="routing"></a><span data-ttu-id="59d8f-188">라우팅</span><span class="sxs-lookup"><span data-stu-id="59d8f-188">Routing</span></span>

<span data-ttu-id="59d8f-189">ASP.NET Core는 응용 프로그램 요청을 경로 처리기로 라우팅하는 시나리오를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-189">ASP.NET Core offers scenarios for routing of app requests to route handlers.</span></span>

<span data-ttu-id="59d8f-190">자세한 내용은 <xref:fundamentals/routing>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-190">For more information, see <xref:fundamentals/routing>.</span></span>

## <a name="file-providers"></a><span data-ttu-id="59d8f-191">파일 공급자</span><span class="sxs-lookup"><span data-stu-id="59d8f-191">File Providers</span></span>

<span data-ttu-id="59d8f-192">ASP.NET Core는 파일 공급자를 사용하여 파일 시스템 액세스를 추상화하고 플랫폼에서 파일을 사용하기 위한 공통 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-192">ASP.NET Core abstracts file system access through the use of File Providers, which offers a common interface for working with files across platforms.</span></span>

<span data-ttu-id="59d8f-193">자세한 내용은 <xref:fundamentals/file-providers>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-193">For more information, see <xref:fundamentals/file-providers>.</span></span>

## <a name="static-files"></a><span data-ttu-id="59d8f-194">정적 파일</span><span class="sxs-lookup"><span data-stu-id="59d8f-194">Static files</span></span>

<span data-ttu-id="59d8f-195">정적 파일 미들웨어는 HTML, CSS, 이미지, JavaScript 파일 등의 정적 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-195">Static Files Middleware serves static files, such as HTML, CSS, image, and JavaScript files.</span></span>

<span data-ttu-id="59d8f-196">자세한 내용은 <xref:fundamentals/static-files>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-196">For more information, see <xref:fundamentals/static-files>.</span></span>

## <a name="session-and-app-state"></a><span data-ttu-id="59d8f-197">세션 및 앱 상태</span><span class="sxs-lookup"><span data-stu-id="59d8f-197">Session and app state</span></span>

<span data-ttu-id="59d8f-198">ASP.NET Core는 사용자가 웹앱을 탐색하는 동안 세션 및 앱 상태를 유지할 수 있는 여러 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-198">ASP.NET Core offers several approaches to preserve session and app state while a user browses a web app.</span></span>

<span data-ttu-id="59d8f-199">자세한 내용은 <xref:fundamentals/app-state>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-199">For more information, see <xref:fundamentals/app-state>.</span></span>

## <a name="globalization-and-localization"></a><span data-ttu-id="59d8f-200">전역화 및 지역화</span><span class="sxs-lookup"><span data-stu-id="59d8f-200">Globalization and localization</span></span>

<span data-ttu-id="59d8f-201">ASP.NET Core를 사용해서 다국어 웹 사이트를 만들면 더 광범위한 사용자가 사이트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-201">Creating a multilingual website with ASP.NET Core allows your site to reach a wider audience.</span></span> <span data-ttu-id="59d8f-202">ASP.NET Core는 콘텐츠를 다른 언어와 문화권에 맞게 지역화하기 위한 서비스 및 미들웨어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-202">ASP.NET Core provides services and middleware for localizing content into different languages and cultures.</span></span>

<span data-ttu-id="59d8f-203">자세한 내용은 <xref:fundamentals/localization>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-203">For more information, see <xref:fundamentals/localization>.</span></span>

## <a name="request-features"></a><span data-ttu-id="59d8f-204">요청 기능</span><span class="sxs-lookup"><span data-stu-id="59d8f-204">Request features</span></span>

<span data-ttu-id="59d8f-205">웹 서버 구현은 HTTP 요청과 관련하여 설명되고 응답은 인터페이스에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-205">Web server implementation details related to HTTP requests and responses are defined in interfaces.</span></span> <span data-ttu-id="59d8f-206">이 인터페이스들은 서버 구현 및 미들웨어에서 앱의 호스팅 파이프라인을 만들고 수정하기 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-206">These interfaces are used by server implementations and middleware to create and modify the app's hosting pipeline.</span></span>

<span data-ttu-id="59d8f-207">자세한 내용은 <xref:fundamentals/request-features>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-207">For more information, see <xref:fundamentals/request-features>.</span></span>

## <a name="background-tasks"></a><span data-ttu-id="59d8f-208">백그라운드 작업</span><span class="sxs-lookup"><span data-stu-id="59d8f-208">Background tasks</span></span>

<span data-ttu-id="59d8f-209">백그라운드 작업은 *호스티드 서비스*로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-209">Background tasks are implemented as *hosted services*.</span></span> <span data-ttu-id="59d8f-210">호스티드 서비스는 <xref:Microsoft.Extensions.Hosting.IHostedService> 인터페이스를 구현하는 백그라운드 작업 논리가 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-210">A hosted service is a class with background task logic that implements the <xref:Microsoft.Extensions.Hosting.IHostedService> interface.</span></span>

<span data-ttu-id="59d8f-211">자세한 내용은 <xref:fundamentals/host/hosted-services>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-211">For more information, see <xref:fundamentals/host/hosted-services>.</span></span>

## <a name="access-httpcontext"></a><span data-ttu-id="59d8f-212">HttpContext에 액세스</span><span class="sxs-lookup"><span data-stu-id="59d8f-212">Access HttpContext</span></span>

<span data-ttu-id="59d8f-213">`HttpContext`는 Razor Pages 및 MVC를 사용하여 요청을 처리할 때 자동으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-213">`HttpContext` is automatically available when processing requests with Razor Pages and MVC.</span></span> <span data-ttu-id="59d8f-214">`HttpContext`를 즉시 사용할 수 없는 경우에는 <xref:Microsoft.AspNetCore.Http.IHttpContextAccessor> 인터페이스 및 기본 구현 <xref:Microsoft.AspNetCore.Http.HttpContextAccessor>를 통해 `HttpContext`에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-214">In circumstances where `HttpContext` isn't readily available, you can access the `HttpContext` through the <xref:Microsoft.AspNetCore.Http.IHttpContextAccessor> interface and its default implementation, <xref:Microsoft.AspNetCore.Http.HttpContextAccessor>.</span></span>

<span data-ttu-id="59d8f-215">자세한 내용은 <xref:fundamentals/httpcontext>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-215">For more information, see <xref:fundamentals/httpcontext>.</span></span>

## <a name="websockets"></a><span data-ttu-id="59d8f-216">WebSocket</span><span class="sxs-lookup"><span data-stu-id="59d8f-216">WebSockets</span></span>

<span data-ttu-id="59d8f-217">[WebSocket](https://wikipedia.org/wiki/WebSocket)은 TCP 연결을 통한 영구 양방향 통신 채널을 사용하도록 설정하는 프로토콜이며</span><span class="sxs-lookup"><span data-stu-id="59d8f-217">[WebSocket](https://wikipedia.org/wiki/WebSocket) is a protocol that enables two-way persistent communication channels over TCP connections.</span></span> <span data-ttu-id="59d8f-218">WebSocket은 채팅, 주식 시세, 게임 등 웹 앱에서 실시간 기능이 필요한 모든 곳에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-218">It's used for apps such as chat, stock tickers, games, and anywhere you desire real-time functionality in a web app.</span></span> <span data-ttu-id="59d8f-219">ASP.NET Core는 웹 소켓 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-219">ASP.NET Core supports web socket scenarios.</span></span>

<span data-ttu-id="59d8f-220">자세한 내용은 <xref:fundamentals/websockets>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-220">For more information, see <xref:fundamentals/websockets>.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="microsoftaspnetcoreapp-metapackage"></a><span data-ttu-id="59d8f-221">Microsoft.AspNetCore.App 메타패키지</span><span class="sxs-lookup"><span data-stu-id="59d8f-221">Microsoft.AspNetCore.App metapackage</span></span>

<span data-ttu-id="59d8f-222">[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) 메타패키지는 패키지 관리를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-222">The [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) metapackage simplifies package management.</span></span>

<span data-ttu-id="59d8f-223">자세한 내용은 <xref:fundamentals/metapackage-app>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-223">For more information, see <xref:fundamentals/metapackage-app>.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

## <a name="microsoftaspnetcoreall-metapackage"></a><span data-ttu-id="59d8f-224">Microsoft.AspNetCore.All 메타패키지</span><span class="sxs-lookup"><span data-stu-id="59d8f-224">Microsoft.AspNetCore.All metapackage</span></span>

<span data-ttu-id="59d8f-225">ASP.NET Core에 대한 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 메타패키지는 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-225">The [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage for ASP.NET Core includes:</span></span>

* <span data-ttu-id="59d8f-226">ASP.NET Core 팀에서 지원되는 모든 패키지</span><span class="sxs-lookup"><span data-stu-id="59d8f-226">All supported packages by the ASP.NET Core team.</span></span>
* <span data-ttu-id="59d8f-227">Entity Framework Core에서 지원되는 모든 패키지</span><span class="sxs-lookup"><span data-stu-id="59d8f-227">All supported packages by Entity Framework Core.</span></span>
* <span data-ttu-id="59d8f-228">ASP.NET Core 및 Entity Framework Core에서 사용되는 내부 및 타사 종속성</span><span class="sxs-lookup"><span data-stu-id="59d8f-228">Internal and 3rd-party dependencies used by ASP.NET Core and Entity Framework Core.</span></span>

<span data-ttu-id="59d8f-229">자세한 내용은 <xref:fundamentals/metapackage>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-229">For more information, see <xref:fundamentals/metapackage>.</span></span>

::: moniker-end

## <a name="net-core-vs-net-framework-runtime"></a><span data-ttu-id="59d8f-230">.NET Core 및 .NET Framework 런타임</span><span class="sxs-lookup"><span data-stu-id="59d8f-230">.NET Core vs. .NET Framework runtime</span></span>

<span data-ttu-id="59d8f-231">ASP.NET Core 앱은 .NET Core 또는 .NET Framework 런타임을 대상으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-231">An ASP.NET Core app can target the .NET Core or .NET Framework runtime.</span></span>

<span data-ttu-id="59d8f-232">자세한 내용은 [.NET Core와 .NET Framework  중에 선택하기](/dotnet/articles/standard/choosing-core-framework-server)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="59d8f-232">For more information, see [Choosing between .NET Core and .NET Framework](/dotnet/articles/standard/choosing-core-framework-server).</span></span>

## <a name="choose-between-aspnet-core-and-aspnet"></a><span data-ttu-id="59d8f-233">ASP.NET Core와 ASP.NET 중에서 선택하기</span><span class="sxs-lookup"><span data-stu-id="59d8f-233">Choose between ASP.NET Core and ASP.NET</span></span>

<span data-ttu-id="59d8f-234">ASP.NET Core와 ASP.NET 중에서 선택하는 방법에 대한 자세한 내용은 <xref:fundamentals/choose-between-aspnet-and-aspnetcore>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d8f-234">For more information on choosing between ASP.NET Core and ASP.NET, see <xref:fundamentals/choose-between-aspnet-and-aspnetcore>.</span></span>
