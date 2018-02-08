---
title: "ASP.NET Core에서 호스팅"
author: guardrex
description: "앱 시작 및 수명 관리를 담당하는 ASP.NET Core에서의 웹 호스트에 대해 알아봅니다."
manager: wpickett
ms.author: riande
ms.date: 09/21/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/hosting
ms.openlocfilehash: 004487aebe5262a515e2375c30ccd2a84844dff6
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="hosting-in-aspnet-core"></a><span data-ttu-id="81b33-103">ASP.NET Core에서 호스팅</span><span class="sxs-lookup"><span data-stu-id="81b33-103">Hosting in ASP.NET Core</span></span>

<span data-ttu-id="81b33-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="81b33-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="81b33-105">ASP.NET Core 앱은 *호스트*를 구성 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-105">ASP.NET Core apps configure and launch a *host*.</span></span> <span data-ttu-id="81b33-106">호스트는 앱 시작 및 수명 관리를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-106">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="81b33-107">최소한으로 호스트는 서버 및 요청 처리 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-107">At a minimum, the host configures a server and a request processing pipeline.</span></span>

## <a name="setting-up-a-host"></a><span data-ttu-id="81b33-108">호스트 설정</span><span class="sxs-lookup"><span data-stu-id="81b33-108">Setting up a host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="81b33-109">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="81b33-109">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="81b33-110">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)의 인스턴스를 사용하여 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-110">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="81b33-111">이는 일반적으로 앱의 진입점에서 수행되는 `Main` 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-111">This is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="81b33-112">프로젝트 템플릿에서 `Main`은 *Program.cs*에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-112">In the project templates, `Main` is located in *Program.cs*.</span></span> <span data-ttu-id="81b33-113">일반적인 *Program.cs*는 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)를 호출하여 호스트 설정을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-113">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to start setting up a host:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main)]

<span data-ttu-id="81b33-114">`CreateDefaultBuilder`는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-114">`CreateDefaultBuilder` performs the following tasks:</span></span>

* <span data-ttu-id="81b33-115">[Kestrel](servers/kestrel.md)을 웹 서버로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-115">Configures [Kestrel](servers/kestrel.md) as the web server.</span></span> <span data-ttu-id="81b33-116">Kestrel 기본 옵션의 경우 [ASP.NET Core에서 Kestrel 웹 서버 구현의 Kestrel 옵션 섹션](xref:fundamentals/servers/kestrel#kestrel-options)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b33-116">For the Kestrel default options, see [the Kestrel options section of Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel#kestrel-options).</span></span>
* <span data-ttu-id="81b33-117">콘텐츠 루트를 [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory)에서 반환된 경로로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-117">Sets the content root to the path returned by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).</span></span>
* <span data-ttu-id="81b33-118">다음에서 선택적인 구성을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-118">Loads optional configuration from:</span></span>
  * <span data-ttu-id="81b33-119">*appsettings.json*.</span><span class="sxs-lookup"><span data-stu-id="81b33-119">*appsettings.json*.</span></span>
  * <span data-ttu-id="81b33-120">*appsettings.{Environment}.json*.</span><span class="sxs-lookup"><span data-stu-id="81b33-120">*appsettings.{Environment}.json*.</span></span>
  * <span data-ttu-id="81b33-121">[사용자 비밀](xref:security/app-secrets) - 앱이 `Development` 환경에서 실행되는 경우.</span><span class="sxs-lookup"><span data-stu-id="81b33-121">[User secrets](xref:security/app-secrets) when the app runs in the `Development` environment.</span></span>
  * <span data-ttu-id="81b33-122">환경 변수.</span><span class="sxs-lookup"><span data-stu-id="81b33-122">Environment variables.</span></span>
  * <span data-ttu-id="81b33-123">명령줄 인수.</span><span class="sxs-lookup"><span data-stu-id="81b33-123">Command-line arguments.</span></span>
* <span data-ttu-id="81b33-124">콘솔 및 디버그 출력에 대한 [로깅](xref:fundamentals/logging/index)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-124">Configures [logging](xref:fundamentals/logging/index) for console and debug output.</span></span> <span data-ttu-id="81b33-125">로깅은 *appsettings.json* 또는 *appsettings.{Environment}.json* 파일의 로깅 구성 섹션에 지정된 [로그 필터링](xref:fundamentals/logging/index#log-filtering) 규칙을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-125">Logging includes [log filtering](xref:fundamentals/logging/index#log-filtering) rules specified in a Logging configuration section of an *appsettings.json* or *appsettings.{Environment}.json* file.</span></span>
* <span data-ttu-id="81b33-126">IIS 뒤에서 실행하는 경우 [IIS 통합](xref:host-and-deploy/iis/index)을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-126">When running behind IIS, enables [IIS integration](xref:host-and-deploy/iis/index).</span></span> <span data-ttu-id="81b33-127">[ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 사용하는 경우 서버가 수신 대기할 기본 경로 및 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-127">Configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="81b33-128">모듈은 IIS와 Kestrel 간에 역방향 프록시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-128">The module creates a reverse proxy between IIS and Kestrel.</span></span> <span data-ttu-id="81b33-129">또한 [시작 오류를 캡처](#capture-startup-errors)하도록 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-129">Also configures the app to [capture startup errors](#capture-startup-errors).</span></span> <span data-ttu-id="81b33-130">IIS 기본 옵션의 경우 [IIS가 있는 Windows에서 ASP.NET Core 호스팅의 IIS 옵션 섹션](xref:host-and-deploy/iis/index#iis-options)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b33-130">For the IIS default options, see [the IIS options section of Host ASP.NET Core on Windows with IIS](xref:host-and-deploy/iis/index#iis-options).</span></span>

<span data-ttu-id="81b33-131">*콘텐츠 루트*는 호스트가 MVC 뷰 파일과 같은 콘텐츠 파일을 검색하는 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-131">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="81b33-132">앱이 프로젝트의 루트 폴더에서 시작되면 프로젝트의 루트 폴더가 콘텐츠 루트로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-132">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="81b33-133">이것이 [Visual Studio](https://www.visualstudio.com/) 및 [dotnet 새 템플릿](/dotnet/core/tools/dotnet-new)에서 사용되는 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-133">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="81b33-134">앱 구성에 대한 자세한 내용은 [ASP.NET Core의 구성](xref:fundamentals/configuration/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b33-134">For more information on app configuration, see [Configuration in ASP.NET Core](xref:fundamentals/configuration/index).</span></span>

> [!NOTE]
> <span data-ttu-id="81b33-135">ASP.NET Core 2.x에서는 정적 `CreateDefaultBuilder` 메서드 사용에 대한 대안으로 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)에서 호스트를 만들 수 있도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-135">As an alternative to using the static `CreateDefaultBuilder` method, creating a host from [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) is a supported approach with ASP.NET Core 2.x.</span></span> <span data-ttu-id="81b33-136">자세한 내용은 ASP.NET Core 1.x 탭을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b33-136">For more information, see the ASP.NET Core 1.x tab.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="81b33-137">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="81b33-137">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="81b33-138">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)의 인스턴스를 사용하여 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-138">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="81b33-139">호스트 만들기는 일반적으로 앱의 진입점에서 수행되는 `Main` 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-139">Creating a host is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="81b33-140">프로젝트 템플릿에서 `Main`은 *Program.cs*에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-140">In the project templates, `Main` is located in *Program.cs*:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1/Program.cs)]

<span data-ttu-id="81b33-141">`WebHostBuilder`에는 [IServer를 구현하는 서버](servers/index.md)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-141">`WebHostBuilder` requires a [server that implements IServer](servers/index.md).</span></span> <span data-ttu-id="81b33-142">기본 제공 서버는 [Kestrel](servers/kestrel.md) 및 [HTTP.sys](servers/httpsys.md)(ASP.NET Core 2.0 출시 전에 HTTP.sys는 [WebListener](xref:fundamentals/servers/weblistener)로 불림)입니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-142">The built-in servers are [Kestrel](servers/kestrel.md) and [HTTP.sys](servers/httpsys.md) (prior to the release of ASP.NET Core 2.0, HTTP.sys was called [WebListener](xref:fundamentals/servers/weblistener)).</span></span> <span data-ttu-id="81b33-143">이 예제에서는 [UseKestrel 확장 메서드](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)가 Kestrel 서버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-143">In this example, the [UseKestrel extension method](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) specifies the Kestrel server.</span></span>

<span data-ttu-id="81b33-144">*콘텐츠 루트*는 호스트가 MVC 뷰 파일과 같은 콘텐츠 파일을 검색하는 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-144">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="81b33-145">[Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1)에서 `UseContentRoot`에 대한 기본 콘텐츠 루트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-145">The default content root is obtained for `UseContentRoot` by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1).</span></span> <span data-ttu-id="81b33-146">앱이 프로젝트의 루트 폴더에서 시작되면 프로젝트의 루트 폴더가 콘텐츠 루트로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-146">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="81b33-147">이것이 [Visual Studio](https://www.visualstudio.com/) 및 [dotnet 새 템플릿](/dotnet/core/tools/dotnet-new)에서 사용되는 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-147">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="81b33-148">IIS를 역방향 프록시로 사용하려면 호스트 빌드 과정 중 일환으로 [UseIISIntegration](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions)을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-148">To use IIS as a reverse proxy, call [UseIISIntegration](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions) as part of building the host.</span></span> <span data-ttu-id="81b33-149">`UseIISIntegration`은 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)과 달리 *서버*를 구성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-149">`UseIISIntegration` doesn't configure a *server*, like [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) does.</span></span> <span data-ttu-id="81b33-150">`UseIISIntegration`은 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 사용하여 Kestrel과 IIS 간 역방향 프록시를 만드는 경우 서버가 수신 대기할 기본 경로 및 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-150">`UseIISIntegration` configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) to create a reverse proxy between Kestrel and IIS.</span></span> <span data-ttu-id="81b33-151">ASP.NET Core와 함께 IIS를 사용하려면 `UseKestrel` 및 `UseIISIntegration`을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-151">To use IIS with ASP.NET Core, `UseKestrel` and `UseIISIntegration` must be specified.</span></span> <span data-ttu-id="81b33-152">`UseIISIntegration`은 IIS 또는 IIS Express 뒤에서 실행하는 경우에만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-152">`UseIISIntegration` only activates when running behind IIS or IIS Express.</span></span> <span data-ttu-id="81b33-153">자세한 내용은 [ASP.NET Core 모듈 소개](xref:fundamentals/servers/aspnet-core-module) 및 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b33-153">For more information, see [Introduction to ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

<span data-ttu-id="81b33-154">호스트(및 ASP.NET Core 앱)를 구성하는 최소 구현에는 서버와 앱의 요청 파이프라인의 구성을 지정하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-154">A minimal implementation that configures a host (and an ASP.NET Core app) includes specifying a server and configuration of the app's request pipeline:</span></span>

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .Configure(app =>
    {
        app.Run(context => context.Response.WriteAsync("Hello World!"));
    })
    .Build();

host.Run();
```

---

<span data-ttu-id="81b33-155">호스트를 설정할 때 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) 및 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) 메서드가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-155">When setting up a host, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) and [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) methods can be provided.</span></span> <span data-ttu-id="81b33-156">`Startup` 클래스가 지정된 경우 `Configure` 메서드를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-156">If a `Startup` class is specified, it must define a `Configure` method.</span></span> <span data-ttu-id="81b33-157">자세한 내용은 [ASP.NET Core에서 응용 프로그램 시작](startup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b33-157">For more information, see [Application Startup in ASP.NET Core](startup.md).</span></span> <span data-ttu-id="81b33-158">`ConfigureServices`에 대한 여러 호출은 서로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-158">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="81b33-159">`WebHostBuilder`에서 `Configure` 또는 `UseStartup`에 대한 여러 호출은 이전 설정을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-159">Multiple calls to `Configure` or `UseStartup` on the `WebHostBuilder` replace previous settings.</span></span>

## <a name="host-configuration-values"></a><span data-ttu-id="81b33-160">호스트 구성 값</span><span class="sxs-lookup"><span data-stu-id="81b33-160">Host configuration values</span></span>

<span data-ttu-id="81b33-161">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)는 호스트 구성 값을 설정하기 위해 다음 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-161">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) relies on the following approaches to set the host configuration values:</span></span>

* <span data-ttu-id="81b33-162">`ASPNETCORE_{configurationKey}` 형식의 환경 변수를 포함하는 호스트 빌더 구성.</span><span class="sxs-lookup"><span data-stu-id="81b33-162">Host builder configuration, which includes environment variables with the format `ASPNETCORE_{configurationKey}`.</span></span> <span data-ttu-id="81b33-163">예를 들어, `ASPNETCORE_URLS`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-163">For example, `ASPNETCORE_URLS`.</span></span>
* <span data-ttu-id="81b33-164">`CaptureStartupErrors`와 같은 명시적 메서드.</span><span class="sxs-lookup"><span data-stu-id="81b33-164">Explicit methods, such as `CaptureStartupErrors`.</span></span>
* <span data-ttu-id="81b33-165">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) 및 연결된 키.</span><span class="sxs-lookup"><span data-stu-id="81b33-165">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) and the associated key.</span></span> <span data-ttu-id="81b33-166">`UseSetting`을 사용하여 값을 설정할 때 값은 형식에 관계 없이 문자열로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-166">When setting a value with `UseSetting`, the value is set as a string regardless of the type.</span></span>

<span data-ttu-id="81b33-167">호스트는 마지막에 값을 설정한 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-167">The host uses whichever option sets a value last.</span></span> <span data-ttu-id="81b33-168">자세한 내용은 다음 섹션의 [구성 재정의](#overriding-configuration)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b33-168">For more information, see [Overriding configuration](#overriding-configuration) in the next section.</span></span>

### <a name="capture-startup-errors"></a><span data-ttu-id="81b33-169">시작 오류 캡처</span><span class="sxs-lookup"><span data-stu-id="81b33-169">Capture Startup Errors</span></span>

<span data-ttu-id="81b33-170">이 설정은 시작 오류의 캡처를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-170">This setting controls the capture of startup errors.</span></span>

<span data-ttu-id="81b33-171">**키**: captureStartupErrors</span><span class="sxs-lookup"><span data-stu-id="81b33-171">**Key**: captureStartupErrors</span></span>  
<span data-ttu-id="81b33-172">**형식**: *bool*(`true` 또는 `1`)</span><span class="sxs-lookup"><span data-stu-id="81b33-172">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="81b33-173">**기본값**: 기본값이 `true`인 IIS 뒤에 있는 Kestrel로 앱이 실행하지 않는 한 기본값은 `false`로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-173">**Default**: Defaults to `false` unless the app runs with Kestrel behind IIS, where the default is `true`.</span></span>  
<span data-ttu-id="81b33-174">**설정 방법**: `CaptureStartupErrors`</span><span class="sxs-lookup"><span data-stu-id="81b33-174">**Set using**: `CaptureStartupErrors`</span></span>  
<span data-ttu-id="81b33-175">**환경 변수**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span><span class="sxs-lookup"><span data-stu-id="81b33-175">**Environment variable**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span></span>

<span data-ttu-id="81b33-176">`false`인 경우 시작 시 오류가 발생하면 호스트가 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-176">When `false`, errors during startup result in the host exiting.</span></span> <span data-ttu-id="81b33-177">`true`이면 호스트가 시작 시 예외를 캡처하고 서버 시작을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-177">When `true`, the host captures exceptions during startup and attempts to start the server.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="81b33-178">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="81b33-178">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .CaptureStartupErrors(true)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="81b33-179">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="81b33-179">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .CaptureStartupErrors(true)
    ...
```

---

### <a name="content-root"></a><span data-ttu-id="81b33-180">콘텐츠 루트</span><span class="sxs-lookup"><span data-stu-id="81b33-180">Content Root</span></span>

<span data-ttu-id="81b33-181">이 설정은 ASP.NET Core가 MVC 뷰와 같은 콘텐츠 파일을 검색하기 시작하는 지점을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-181">This setting determines where ASP.NET Core begins searching for content files, such as MVC views.</span></span> 

<span data-ttu-id="81b33-182">**키**: contentRoot</span><span class="sxs-lookup"><span data-stu-id="81b33-182">**Key**: contentRoot</span></span>  
<span data-ttu-id="81b33-183">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="81b33-183">**Type**: *string*</span></span>  
<span data-ttu-id="81b33-184">**기본값**: 앱 어셈블리가 있는 폴더가 기본값으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-184">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="81b33-185">**설정 방법**: `UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="81b33-185">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="81b33-186">**환경 변수**: `ASPNETCORE_CONTENTROOT`</span><span class="sxs-lookup"><span data-stu-id="81b33-186">**Environment variable**: `ASPNETCORE_CONTENTROOT`</span></span>

<span data-ttu-id="81b33-187">콘텐츠 루트는 또한 [웹 루트 설정](#web-root)에 대한 기본 경로로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-187">The content root is also used as the base path for the [Web Root setting](#web-root).</span></span> <span data-ttu-id="81b33-188">경로가 존재하지 않는 경우 호스트가 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-188">If the path doesn't exist, the host fails to start.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="81b33-189">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="81b33-189">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseContentRoot("c:\\mywebsite")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="81b33-190">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="81b33-190">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseContentRoot("c:\\mywebsite")
    ...
```

---

### <a name="detailed-errors"></a><span data-ttu-id="81b33-191">자세한 오류</span><span class="sxs-lookup"><span data-stu-id="81b33-191">Detailed Errors</span></span>

<span data-ttu-id="81b33-192">자세한 오류를 캡처해야 하는지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-192">Determines if detailed errors should be captured.</span></span>

<span data-ttu-id="81b33-193">**키**: detailedErrors</span><span class="sxs-lookup"><span data-stu-id="81b33-193">**Key**: detailedErrors</span></span>  
<span data-ttu-id="81b33-194">**형식**: *bool*(`true` 또는 `1`)</span><span class="sxs-lookup"><span data-stu-id="81b33-194">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="81b33-195">**기본값**: false</span><span class="sxs-lookup"><span data-stu-id="81b33-195">**Default**: false</span></span>  
<span data-ttu-id="81b33-196">**설정 방법**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="81b33-196">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="81b33-197">**환경 변수**: `ASPNETCORE_DETAILEDERRORS`</span><span class="sxs-lookup"><span data-stu-id="81b33-197">**Environment variable**: `ASPNETCORE_DETAILEDERRORS`</span></span>

<span data-ttu-id="81b33-198">사용하는 경우(또는 <a href="#environment">환경</a>이 `Development`로 설정된 경우) 앱은 자세한 예외를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-198">When enabled (or when the <a href="#environment">Environment</a> is set to `Development`), the app captures detailed exceptions.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="81b33-199">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="81b33-199">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="81b33-200">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="81b33-200">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

---

### <a name="environment"></a><span data-ttu-id="81b33-201">환경</span><span class="sxs-lookup"><span data-stu-id="81b33-201">Environment</span></span>

<span data-ttu-id="81b33-202">앱의 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-202">Sets the app's environment.</span></span>

<span data-ttu-id="81b33-203">**키**: environment</span><span class="sxs-lookup"><span data-stu-id="81b33-203">**Key**: environment</span></span>  
<span data-ttu-id="81b33-204">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="81b33-204">**Type**: *string*</span></span>  
<span data-ttu-id="81b33-205">**기본값**: Production</span><span class="sxs-lookup"><span data-stu-id="81b33-205">**Default**: Production</span></span>  
<span data-ttu-id="81b33-206">**설정 방법**: `UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="81b33-206">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="81b33-207">**환경 변수**: `ASPNETCORE_ENVIRONMENT`</span><span class="sxs-lookup"><span data-stu-id="81b33-207">**Environment variable**: `ASPNETCORE_ENVIRONMENT`</span></span>

<span data-ttu-id="81b33-208">환경은 어떠한 값으로도 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-208">The environment can be set to any value.</span></span> <span data-ttu-id="81b33-209">프레임워크에서 정의된 값은 `Development`, `Staging` 및 `Production`을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-209">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="81b33-210">값은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-210">Values aren't case sensitive.</span></span> <span data-ttu-id="81b33-211">기본적으로 *환경*은 `ASPNETCORE_ENVIRONMENT` 환경 변수에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-211">By default, the *Environment* is read from the `ASPNETCORE_ENVIRONMENT` environment variable.</span></span> <span data-ttu-id="81b33-212">[Visual Studio](https://www.visualstudio.com/)를 사용하는 경우 환경 변수는 *launchSettings.json* 파일에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-212">When using [Visual Studio](https://www.visualstudio.com/), environment variables may be set in the *launchSettings.json* file.</span></span> <span data-ttu-id="81b33-213">자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b33-213">For more information, see [Working with Multiple Environments](xref:fundamentals/environments).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="81b33-214">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="81b33-214">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseEnvironment("Development")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="81b33-215">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="81b33-215">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseEnvironment("Development")
    ...
```

---

### <a name="hosting-startup-assemblies"></a><span data-ttu-id="81b33-216">호스팅 시작 어셈블리</span><span class="sxs-lookup"><span data-stu-id="81b33-216">Hosting Startup Assemblies</span></span>

<span data-ttu-id="81b33-217">앱의 호스팅 시작 어셈블리를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-217">Sets the app's hosting startup assemblies.</span></span>

<span data-ttu-id="81b33-218">**키**: hostingStartupAssemblies</span><span class="sxs-lookup"><span data-stu-id="81b33-218">**Key**: hostingStartupAssemblies</span></span>  
<span data-ttu-id="81b33-219">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="81b33-219">**Type**: *string*</span></span>  
<span data-ttu-id="81b33-220">**기본값**: 빈 문자열</span><span class="sxs-lookup"><span data-stu-id="81b33-220">**Default**: Empty string</span></span>  
<span data-ttu-id="81b33-221">**설정 방법**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="81b33-221">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="81b33-222">**환경 변수**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span><span class="sxs-lookup"><span data-stu-id="81b33-222">**Environment variable**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span></span>

<span data-ttu-id="81b33-223">시작 시 로드할 호스팅 시작 어셈블리의 세미콜론으로 구분된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-223">A semicolon-delimited string of hosting startup assemblies to load on startup.</span></span> <span data-ttu-id="81b33-224">이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-224">This feature is new in ASP.NET Core 2.0.</span></span>

<span data-ttu-id="81b33-225">구성 값의 기본값이 빈 문자열이지만, 호스팅 시작 어셈블리는 항상 앱의 어셈블리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-225">Although the configuration value defaults to an empty string, the hosting startup assemblies always include the app's assembly.</span></span> <span data-ttu-id="81b33-226">호스팅 시작 어셈블리가 제공되는 경우, 시작 시 앱이 일반적인 서비스를 빌드할 때 로드를 위해 앱의 어셈블리에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-226">When hosting startup assemblies are provided, they're added to the app's assembly for loading when the app builds its common services during startup.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="81b33-227">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="81b33-227">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupAssembliesKey, "assembly1;assembly2")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="81b33-228">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="81b33-228">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="81b33-229">이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-229">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prefer-hosting-urls"></a><span data-ttu-id="81b33-230">호스팅 URL 선호</span><span class="sxs-lookup"><span data-stu-id="81b33-230">Prefer Hosting URLs</span></span>

<span data-ttu-id="81b33-231">호스트가 `IServer` 구현으로 구성된 URL 대신에 `WebHostBuilder`로 구성된 URL에서 수신 대기할지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-231">Indicates whether the host should listen on the URLs configured with the `WebHostBuilder` instead of those configured with the `IServer` implementation.</span></span>

<span data-ttu-id="81b33-232">**키**: preferHostingUrls</span><span class="sxs-lookup"><span data-stu-id="81b33-232">**Key**: preferHostingUrls</span></span>  
<span data-ttu-id="81b33-233">**형식**: *bool*(`true` 또는 `1`)</span><span class="sxs-lookup"><span data-stu-id="81b33-233">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="81b33-234">**기본값**: true</span><span class="sxs-lookup"><span data-stu-id="81b33-234">**Default**: true</span></span>  
<span data-ttu-id="81b33-235">**설정 방법**: `PreferHostingUrls`</span><span class="sxs-lookup"><span data-stu-id="81b33-235">**Set using**: `PreferHostingUrls`</span></span>  
<span data-ttu-id="81b33-236">**환경 변수**: `ASPNETCORE_PREFERHOSTINGURLS`</span><span class="sxs-lookup"><span data-stu-id="81b33-236">**Environment variable**: `ASPNETCORE_PREFERHOSTINGURLS`</span></span>

<span data-ttu-id="81b33-237">이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-237">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="81b33-238">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="81b33-238">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .PreferHostingUrls(false)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="81b33-239">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="81b33-239">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="81b33-240">이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-240">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prevent-hosting-startup"></a><span data-ttu-id="81b33-241">호스팅 시작 방지</span><span class="sxs-lookup"><span data-stu-id="81b33-241">Prevent Hosting Startup</span></span>

<span data-ttu-id="81b33-242">앱의 어셈블리에 의해 구성된 호스팅 시작 어셈블리를 포함한 호스팅 시작 어셈블리의 자동 로딩을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-242">Prevents the automatic loading of hosting startup assemblies, including hosting startup assemblies configured by the app's assembly.</span></span> <span data-ttu-id="81b33-243">자세한 내용은 [IHostingStartup을 사용하여 외부 어셈블리의 앱 기능 추가](xref:host-and-deploy/ihostingstartup)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b33-243">See [Add app features from an external assembly using IHostingStartup](xref:host-and-deploy/ihostingstartup) for more information.</span></span>

<span data-ttu-id="81b33-244">**키**: preventHostingStartup</span><span class="sxs-lookup"><span data-stu-id="81b33-244">**Key**: preventHostingStartup</span></span>  
<span data-ttu-id="81b33-245">**형식**: *bool*(`true` 또는 `1`)</span><span class="sxs-lookup"><span data-stu-id="81b33-245">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="81b33-246">**기본값**: false</span><span class="sxs-lookup"><span data-stu-id="81b33-246">**Default**: false</span></span>  
<span data-ttu-id="81b33-247">**설정 방법**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="81b33-247">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="81b33-248">**환경 변수**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span><span class="sxs-lookup"><span data-stu-id="81b33-248">**Environment variable**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span></span>

<span data-ttu-id="81b33-249">이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-249">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="81b33-250">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="81b33-250">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.PreventHostingStartupKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="81b33-251">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="81b33-251">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="81b33-252">이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-252">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="server-urls"></a><span data-ttu-id="81b33-253">서버 URL</span><span class="sxs-lookup"><span data-stu-id="81b33-253">Server URLs</span></span>

<span data-ttu-id="81b33-254">서버에서 요청을 수신해야 하는 포트와 프로토콜이 있는 IP 주소 또는 호스트 주소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-254">Indicates the IP addresses or host addresses with ports and protocols that the server should listen on for requests.</span></span>

<span data-ttu-id="81b33-255">**키**: urls</span><span class="sxs-lookup"><span data-stu-id="81b33-255">**Key**: urls</span></span>  
<span data-ttu-id="81b33-256">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="81b33-256">**Type**: *string*</span></span>  
<span data-ttu-id="81b33-257">**기본값**: http://localhost:5000</span><span class="sxs-lookup"><span data-stu-id="81b33-257">**Default**: http://localhost:5000</span></span>  
<span data-ttu-id="81b33-258">**설정 방법**: `UseUrls`</span><span class="sxs-lookup"><span data-stu-id="81b33-258">**Set using**: `UseUrls`</span></span>  
<span data-ttu-id="81b33-259">**환경 변수**: `ASPNETCORE_URLS`</span><span class="sxs-lookup"><span data-stu-id="81b33-259">**Environment variable**: `ASPNETCORE_URLS`</span></span>

<span data-ttu-id="81b33-260">서버가 응답해야 하는 세미콜론으로 구분된(;) URL 접두사의 목록으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-260">Set to a semicolon-separated (;) list of URL prefixes to which the server should respond.</span></span> <span data-ttu-id="81b33-261">예를 들어, `http://localhost:123`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-261">For example, `http://localhost:123`.</span></span> <span data-ttu-id="81b33-262">“\*”를 사용하여 서버가 지정된 포트 및 프로토콜을 사용하는 IP 주소 또는 호스트 이름에서 요청을 수신해야 함을 나타냅니다(예: `http://*:5000`).</span><span class="sxs-lookup"><span data-stu-id="81b33-262">Use "\*" to indicate that the server should listen for requests on any IP address or hostname using the specified port and protocol (for example, `http://*:5000`).</span></span> <span data-ttu-id="81b33-263">프로토콜(`http://` 또는 `https://`)은 각 URL에 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-263">The protocol (`http://` or `https://`) must be included with each URL.</span></span> <span data-ttu-id="81b33-264">지원되는 형식은 서버마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-264">Supported formats vary between servers.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="81b33-265">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="81b33-265">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

<span data-ttu-id="81b33-266">Kestrel에는 자체 엔드포인트 구성 API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-266">Kestrel has its own endpoint configuration API.</span></span> <span data-ttu-id="81b33-267">자세한 내용은 [ASP.NET Core의 Kestrel 웹 서버 구현](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b33-267">For more information, see [Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="81b33-268">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="81b33-268">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

---

### <a name="shutdown-timeout"></a><span data-ttu-id="81b33-269">시스템 종료 제한 시간</span><span class="sxs-lookup"><span data-stu-id="81b33-269">Shutdown Timeout</span></span>

<span data-ttu-id="81b33-270">웹 호스트가 종료될 때까지 기다리는 시간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-270">Specifies the amount of time to wait for the web host to shutdown.</span></span>

<span data-ttu-id="81b33-271">**키**: shutdownTimeoutSeconds</span><span class="sxs-lookup"><span data-stu-id="81b33-271">**Key**: shutdownTimeoutSeconds</span></span>  
<span data-ttu-id="81b33-272">**형식**: *int*</span><span class="sxs-lookup"><span data-stu-id="81b33-272">**Type**: *int*</span></span>  
<span data-ttu-id="81b33-273">**기본값**: 5</span><span class="sxs-lookup"><span data-stu-id="81b33-273">**Default**: 5</span></span>  
<span data-ttu-id="81b33-274">**설정 방법**: `UseShutdownTimeout`</span><span class="sxs-lookup"><span data-stu-id="81b33-274">**Set using**: `UseShutdownTimeout`</span></span>  
<span data-ttu-id="81b33-275">**환경 변수**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span><span class="sxs-lookup"><span data-stu-id="81b33-275">**Environment variable**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span></span>

<span data-ttu-id="81b33-276">키가 `UseSetting`을 통해 *int*를 허용하더라도(예: `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`) `UseShutdownTimeout` 확장 메서드는 `TimeSpan`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-276">Although the key accepts an *int* with `UseSetting` (for example, `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), the `UseShutdownTimeout` extension method takes a `TimeSpan`.</span></span> <span data-ttu-id="81b33-277">이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-277">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="81b33-278">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="81b33-278">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="81b33-279">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="81b33-279">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="81b33-280">이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-280">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="startup-assembly"></a><span data-ttu-id="81b33-281">시작 어셈블리</span><span class="sxs-lookup"><span data-stu-id="81b33-281">Startup Assembly</span></span>

<span data-ttu-id="81b33-282">`Startup` 클래스를 검색할 어셈블리를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-282">Determines the assembly to search for the `Startup` class.</span></span>

<span data-ttu-id="81b33-283">**키**: startupAssembly</span><span class="sxs-lookup"><span data-stu-id="81b33-283">**Key**: startupAssembly</span></span>  
<span data-ttu-id="81b33-284">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="81b33-284">**Type**: *string*</span></span>  
<span data-ttu-id="81b33-285">**기본값**: 앱의 어셈블리</span><span class="sxs-lookup"><span data-stu-id="81b33-285">**Default**: The app's assembly</span></span>  
<span data-ttu-id="81b33-286">**설정 방법**: `UseStartup`</span><span class="sxs-lookup"><span data-stu-id="81b33-286">**Set using**: `UseStartup`</span></span>  
<span data-ttu-id="81b33-287">**환경 변수**: `ASPNETCORE_STARTUPASSEMBLY`</span><span class="sxs-lookup"><span data-stu-id="81b33-287">**Environment variable**: `ASPNETCORE_STARTUPASSEMBLY`</span></span>

<span data-ttu-id="81b33-288">이름(`string`) 또는 형식(`TStartup`)별 어셈블리를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-288">The assembly by name (`string`) or type (`TStartup`) can be referenced.</span></span> <span data-ttu-id="81b33-289">`UseStartup` 메서드가 여러 개 호출된 경우 마지막 메서드가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-289">If multiple `UseStartup` methods are called, the last one takes precedence.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="81b33-290">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="81b33-290">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup("StartupAssemblyName")
    ...
```

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup<TStartup>()
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="81b33-291">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="81b33-291">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseStartup("StartupAssemblyName")
    ...
```

```csharp
var host = new WebHostBuilder()
    .UseStartup<TStartup>()
    ...
```

---

### <a name="web-root"></a><span data-ttu-id="81b33-292">웹 루트</span><span class="sxs-lookup"><span data-stu-id="81b33-292">Web Root</span></span>

<span data-ttu-id="81b33-293">앱의 정적 자산에 대한 상대 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-293">Sets the relative path to the app's static assets.</span></span>

<span data-ttu-id="81b33-294">**키**: webroot</span><span class="sxs-lookup"><span data-stu-id="81b33-294">**Key**: webroot</span></span>  
<span data-ttu-id="81b33-295">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="81b33-295">**Type**: *string*</span></span>  
<span data-ttu-id="81b33-296">**기본값**: 기본값이 지정되지 않은 경우 기본값은 “(Content Root)/wwwroot”입니다(경로가 존재하는 경우).</span><span class="sxs-lookup"><span data-stu-id="81b33-296">**Default**: If not specified, the default is "(Content Root)/wwwroot", if the path exists.</span></span> <span data-ttu-id="81b33-297">경로가 존재하지 않다면 no-op 파일 공급자가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-297">If the path doesn't exist, then a no-op file provider is used.</span></span>  
<span data-ttu-id="81b33-298">**설정 방법**: `UseWebRoot`</span><span class="sxs-lookup"><span data-stu-id="81b33-298">**Set using**: `UseWebRoot`</span></span>  
<span data-ttu-id="81b33-299">**환경 변수**: `ASPNETCORE_WEBROOT`</span><span class="sxs-lookup"><span data-stu-id="81b33-299">**Environment variable**: `ASPNETCORE_WEBROOT`</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="81b33-300">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="81b33-300">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseWebRoot("public")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="81b33-301">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="81b33-301">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseWebRoot("public")
    ...
```

---

## <a name="overriding-configuration"></a><span data-ttu-id="81b33-302">구성 재정의 중</span><span class="sxs-lookup"><span data-stu-id="81b33-302">Overriding configuration</span></span>

<span data-ttu-id="81b33-303">[구성](xref:fundamentals/configuration/index)을 사용하여 호스트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-303">Use [Configuration](xref:fundamentals/configuration/index) to configure the host.</span></span> <span data-ttu-id="81b33-304">다음 예제에서는 호스트 구성이 필요에 따라 *hosting.json* 파일에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-304">In the following example, host configuration is optionally specified in a *hosting.json* file.</span></span> <span data-ttu-id="81b33-305">*hosting.json* 파일에서 로드된 모든 구성은 명령줄 인수에 의해 재정의될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-305">Any configuration loaded from the *hosting.json* file may be overridden by command-line arguments.</span></span> <span data-ttu-id="81b33-306">기본 제공된 구성(`config`에 있음)은 `UseConfiguration`을 통해 호스트를 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-306">The built configuration (in `config`) is used to configure the host with `UseConfiguration`.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="81b33-307">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="81b33-307">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="81b33-308">*hosting.json*:</span><span class="sxs-lookup"><span data-stu-id="81b33-308">*hosting.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

<span data-ttu-id="81b33-309">먼저 *hosting.json* 구성으로 `UseUrls`에 의해 제공되는 구성을 재정의하고, 두 번째로 명령줄 인수 구성을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-309">Overriding the configuration provided by `UseUrls` with *hosting.json* config first, command-line argument config second:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        BuildWebHost(args).Run();
    }

    public static IWebHost BuildWebHost(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hosting.json", optional: true)
            .AddCommandLine(args)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseUrls("http://*:5000")
            .UseConfiguration(config)
            .Configure(app =>
            {
                app.Run(context => 
                    context.Response.WriteAsync("Hello, World!"));
            })
            .Build();
    }
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="81b33-310">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="81b33-310">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="81b33-311">*hosting.json*:</span><span class="sxs-lookup"><span data-stu-id="81b33-311">*hosting.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

<span data-ttu-id="81b33-312">먼저 *hosting.json* 구성으로 `UseUrls`에 의해 제공되는 구성을 재정의하고, 두 번째로 명령줄 인수 구성을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-312">Overriding the configuration provided by `UseUrls` with *hosting.json* config first, command-line argument config second:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hosting.json", optional: true)
            .AddCommandLine(args)
            .Build();

        var host = new WebHostBuilder()
            .UseUrls("http://*:5000")
            .UseConfiguration(config)
            .UseKestrel()
            .Configure(app =>
            {
                app.Run(context => 
                    context.Response.WriteAsync("Hello, World!"));
            })
            .Build();

        host.Run();
    }
}
```

---

> [!NOTE]
> <span data-ttu-id="81b33-313">[UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 확장 메서드는 현재 `GetSection`에서 반환되는 구성 섹션을 구문 분석할 수 없습니다(예: `.UseConfiguration(Configuration.GetSection("section"))`).</span><span class="sxs-lookup"><span data-stu-id="81b33-313">The [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) extension method isn't currently capable of parsing a configuration section returned by `GetSection` (for example, `.UseConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="81b33-314">`GetSection` 메서드는 요청된 섹션에 대한 구성 키를 필터링하지만 키에 있는 섹션 이름을 그대로 둡니다(예: `section:urls`, `section:environment`).</span><span class="sxs-lookup"><span data-stu-id="81b33-314">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:urls`, `section:environment`).</span></span> <span data-ttu-id="81b33-315">`UseConfiguration` 메서드에서는 키가 `WebHostBuilder` 키와 일치해야 합니다(예: `urls`, `environment`).</span><span class="sxs-lookup"><span data-stu-id="81b33-315">The `UseConfiguration` method expects the keys to match the `WebHostBuilder` keys (for example, `urls`, `environment`).</span></span> <span data-ttu-id="81b33-316">키에서 섹션 이름의 존재는 섹션 값으로 호스트를 구성할 수 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-316">The presence of the section name on the keys prevents the section's values from configuring the host.</span></span> <span data-ttu-id="81b33-317">이 문제는 향후 릴리스에서 해결될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-317">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="81b33-318">자세한 내용 및 해결 방법은 [전체 키를 사용하여 WebHostBuilder.UseConfiguration에 구성 섹션을 전달](https://github.com/aspnet/Hosting/issues/839)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b33-318">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>

<span data-ttu-id="81b33-319">특정 URL에서 실행하는 호스트를 지정하려면 `dotnet run` 실행 시 원하는 값을 명령 프롬프트에서 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-319">To specify the host run on a particular URL, the desired value can be passed in from a command prompt when executing `dotnet run`.</span></span> <span data-ttu-id="81b33-320">명령줄 인수는 *hosting.json* 파일의 `urls` 값을 재정의하고, 서버는 포트 8080에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-320">The command-line argument overrides the `urls` value from the *hosting.json* file, and the server listens on port 8080:</span></span>

```console
dotnet run --urls "http://*:8080"
```

## <a name="starting-the-host"></a><span data-ttu-id="81b33-321">호스트 시작 중</span><span class="sxs-lookup"><span data-stu-id="81b33-321">Starting the host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="81b33-322">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="81b33-322">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="81b33-323">**실행**</span><span class="sxs-lookup"><span data-stu-id="81b33-323">**Run**</span></span>

<span data-ttu-id="81b33-324">`Run` 메서드는 웹앱을 시작하고 호스트가 종료될 때까지 호출 스레드를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-324">The `Run` method starts the web app and blocks the calling thread until the host is shutdown:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="81b33-325">**Start**</span><span class="sxs-lookup"><span data-stu-id="81b33-325">**Start**</span></span>

<span data-ttu-id="81b33-326">해당 `Start` 메서드를 호출하여 비차단 방식으로 호스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-326">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="81b33-327">URL 목록이 `Start` 메서드에 전달되면 지정된 URL에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-327">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>

```csharp
var urls = new List<string>()
{
    "http://*:5000",
    "http://localhost:5001"
};

var host = new WebHostBuilder()
    .UseKestrel()
    .UseStartup<Startup>()
    .Start(urls.ToArray());

using (host)
{
    Console.ReadLine();
}
```

<span data-ttu-id="81b33-328">앱은 정적 편의 메서드를 사용하여 `CreateDefaultBuilder`의 미리 구성된 기본 값을 사용하는 새 호스트를 초기화하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-328">The app can initialize and start a new host using the pre-configured defaults of `CreateDefaultBuilder` using a static convenience method.</span></span> <span data-ttu-id="81b33-329">이러한 메서드는 콘솔 출력 없이 서버를 시작하고 [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown)으로 중단(Ctrl-C/SIGINT 또는 SIGTERM)될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-329">These methods start the server without console output and with [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) wait for a break (Ctrl-C/SIGINT or SIGTERM):</span></span>

<span data-ttu-id="81b33-330">**Start(RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="81b33-330">**Start(RequestDelegate app)**</span></span>

<span data-ttu-id="81b33-331">`RequestDelegate`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-331">Start with a `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start(app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="81b33-332">`http://localhost:5000`에 대한 브라우저에서 요청을 수행하여 “Hello World!” 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-332">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="81b33-333">`WaitForShutdown`은 중단(Ctrl-C/SIGINT 또는 SIGTERM)이 발생할 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-333">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="81b33-334">앱은 `Console.WriteLine` 메시지를 표시하고 keypress가 종료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-334">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="81b33-335">**Start(string url, RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="81b33-335">**Start(string url, RequestDelegate app)**</span></span>

<span data-ttu-id="81b33-336">URL 및 `RequestDelegate`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-336">Start with a URL and `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start("http://localhost:8080", app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="81b33-337">앱이 `http://localhost:8080`에서 응답한다는 점을 제외하고 **Start(RequestDelegate app)**와 동일한 결과가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-337">Produces the same result as **Start(RequestDelegate app)**, except the app responds on `http://localhost:8080`.</span></span>

<span data-ttu-id="81b33-338">**Start(Action<IRouteBuilder> routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="81b33-338">**Start(Action<IRouteBuilder> routeBuilder)**</span></span>

<span data-ttu-id="81b33-339">`IRouteBuilder`의 인스턴스([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/))를 사용하여 라우팅 미들웨어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-339">Use an instance of `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) to use routing middleware:</span></span>

```csharp
using (var host = WebHost.Start(router => router
    .MapGet("hello/{name}", (req, res, data) => 
        res.WriteAsync($"Hello, {data.Values["name"]}!"))
    .MapGet("buenosdias/{name}", (req, res, data) => 
        res.WriteAsync($"Buenos dias, {data.Values["name"]}!"))
    .MapGet("throw/{message?}", (req, res, data) => 
        throw new Exception((string)data.Values["message"] ?? "Uh oh!"))
    .MapGet("{greeting}/{name}", (req, res, data) => 
        res.WriteAsync($"{data.Values["greeting"]}, {data.Values["name"]}!"))
    .MapGet("", (req, res, data) => res.WriteAsync("Hello, World!"))))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="81b33-340">예제에서는 다음 브라우저 요청을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-340">Use the following browser requests with the example:</span></span>

| <span data-ttu-id="81b33-341">요청</span><span class="sxs-lookup"><span data-stu-id="81b33-341">Request</span></span>                                    | <span data-ttu-id="81b33-342">응답</span><span class="sxs-lookup"><span data-stu-id="81b33-342">Response</span></span>                                 |
| ------------------------------------------ | ---------------------------------------- |
| `http://localhost:5000/hello/Martin`       | <span data-ttu-id="81b33-343">Hello, Martin!</span><span class="sxs-lookup"><span data-stu-id="81b33-343">Hello, Martin!</span></span>                           |
| `http://localhost:5000/buenosdias/Catrina` | <span data-ttu-id="81b33-344">Buenos dias, Catrina!</span><span class="sxs-lookup"><span data-stu-id="81b33-344">Buenos dias, Catrina!</span></span>                    |
| `http://localhost:5000/throw/ooops!`       | <span data-ttu-id="81b33-345">“ooops!” 문자열을 사용하여 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-345">Throws an exception with string "ooops!"</span></span> |
| `http://localhost:5000/throw`              | <span data-ttu-id="81b33-346">“Uh oh!” 문자열을 사용하여 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-346">Throws an exception with string "Uh oh!"</span></span> |
| `http://localhost:5000/Sante/Kevin`        | <span data-ttu-id="81b33-347">Sante, Kevin!</span><span class="sxs-lookup"><span data-stu-id="81b33-347">Sante, Kevin!</span></span>                            |
| `http://localhost:5000`                    | <span data-ttu-id="81b33-348">Hello World!</span><span class="sxs-lookup"><span data-stu-id="81b33-348">Hello World!</span></span>                             |

<span data-ttu-id="81b33-349">`WaitForShutdown`은 중단(Ctrl-C/SIGINT 또는 SIGTERM)이 발생할 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-349">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="81b33-350">앱은 `Console.WriteLine` 메시지를 표시하고 keypress가 종료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-350">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="81b33-351">**Start(string url, Action<IRouteBuilder> routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="81b33-351">**Start(string url, Action<IRouteBuilder> routeBuilder)**</span></span>

<span data-ttu-id="81b33-352">URL 및 `IRouteBuilder`의 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-352">Use a URL and an instance of `IRouteBuilder`:</span></span>

```csharp
using (var host = WebHost.Start("http://localhost:8080", router => router
    .MapGet("hello/{name}", (req, res, data) => 
        res.WriteAsync($"Hello, {data.Values["name"]}!"))
    .MapGet("buenosdias/{name}", (req, res, data) => 
        res.WriteAsync($"Buenos dias, {data.Values["name"]}!"))
    .MapGet("throw/{message?}", (req, res, data) => 
        throw new Exception((string)data.Values["message"] ?? "Uh oh!"))
    .MapGet("{greeting}/{name}", (req, res, data) => 
        res.WriteAsync($"{data.Values["greeting"]}, {data.Values["name"]}!"))
    .MapGet("", (req, res, data) => res.WriteAsync("Hello, World!"))))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="81b33-353">앱이 `http://localhost:8080`에서 응답한다는 점을 제외하고 **Start(Action<IRouteBuilder> routeBuilder)**와 동일한 결과가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-353">Produces the same result as **Start(Action<IRouteBuilder> routeBuilder)**, except the app responds at `http://localhost:8080`.</span></span>

<span data-ttu-id="81b33-354">**StartWith(Action<IApplicationBuilder> app)**</span><span class="sxs-lookup"><span data-stu-id="81b33-354">**StartWith(Action<IApplicationBuilder> app)**</span></span>

<span data-ttu-id="81b33-355">대리자를 제공하여 `IApplicationBuilder`를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-355">Provide a delegate to configure an `IApplicationBuilder`:</span></span>

```csharp
using (var host = WebHost.StartWith(app => 
    app.Use(next => 
    {
        return async context => 
        {
            await context.Response.WriteAsync("Hello World!");
        };
    })))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="81b33-356">`http://localhost:5000`에 대한 브라우저에서 요청을 수행하여 “Hello World!” 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-356">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="81b33-357">`WaitForShutdown`은 중단(Ctrl-C/SIGINT 또는 SIGTERM)이 발생할 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-357">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="81b33-358">앱은 `Console.WriteLine` 메시지를 표시하고 keypress가 종료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-358">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="81b33-359">**StartWith(string url, Action<IApplicationBuilder> app)**</span><span class="sxs-lookup"><span data-stu-id="81b33-359">**StartWith(string url, Action<IApplicationBuilder> app)**</span></span>

<span data-ttu-id="81b33-360">URL 및 대리자를 제공하여 `IApplicationBuilder`를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-360">Provide a URL and a delegate to configure an `IApplicationBuilder`:</span></span>

```csharp
using (var host = WebHost.StartWith("http://localhost:8080", app => 
    app.Use(next => 
    {
        return async context => 
        {
            await context.Response.WriteAsync("Hello World!");
        };
    })))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="81b33-361">앱이 `http://localhost:8080`에서 응답한다는 점을 제외하고 **StartWith(Action<IApplicationBuilder> app)**와 동일한 결과가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-361">Produces the same result as **StartWith(Action<IApplicationBuilder> app)**, except the app responds on `http://localhost:8080`.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="81b33-362">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="81b33-362">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="81b33-363">**실행**</span><span class="sxs-lookup"><span data-stu-id="81b33-363">**Run**</span></span>

<span data-ttu-id="81b33-364">`Run` 메서드는 웹앱을 시작하고 호스트가 종료될 때까지 호출 스레드를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-364">The `Run` method starts the web app and blocks the calling thread until the host is shut down:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="81b33-365">**Start**</span><span class="sxs-lookup"><span data-stu-id="81b33-365">**Start**</span></span>

<span data-ttu-id="81b33-366">해당 `Start` 메서드를 호출하여 비차단 방식으로 호스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-366">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="81b33-367">URL 목록이 `Start` 메서드에 전달되면 지정된 URL에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-367">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>


```csharp
var urls = new List<string>()
{
    "http://*:5000",
    "http://localhost:5001"
};

var host = new WebHostBuilder()
    .UseKestrel()
    .UseStartup<Startup>()
    .Start(urls.ToArray());

using (host)
{
    Console.ReadLine();
}
```

---

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="81b33-368">IHostingEnvironment 인터페이스</span><span class="sxs-lookup"><span data-stu-id="81b33-368">IHostingEnvironment interface</span></span>

<span data-ttu-id="81b33-369">[IHostingEnvironment 인터페이스](/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment)는 앱의 웹 호스팅 환경에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-369">The [IHostingEnvironment interface](/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment) provides information about the app's web hosting environment.</span></span> <span data-ttu-id="81b33-370">해당 속성 및 확장 메서드를 사용하기 위해 [생성자 주입](xref:fundamentals/dependency-injection)을 사용하여 `IHostingEnvironment`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-370">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

```csharp
public class CustomFileReader
{
    private readonly IHostingEnvironment _env;

    public CustomFileReader(IHostingEnvironment env)
    {
        _env = env;
    }

    public string ReadFile(string filePath)
    {
        var fileProvider = _env.WebRootFileProvider;
        // Process the file here
    }
}
```

<span data-ttu-id="81b33-371">[규칙 기반 접근 방식](xref:fundamentals/environments#startup-conventions)은 시작할 때 환경에 따라 앱을 구성하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-371">A [convention-based approach](xref:fundamentals/environments#startup-conventions) can be used to configure the app at startup based on the environment.</span></span> <span data-ttu-id="81b33-372">또는 `ConfigureServices`에서 사용할 수 있도록 `IHostingEnvironment`를 `Startup` 생성자에 주입합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-372">Alternatively, inject the `IHostingEnvironment` into the `Startup` constructor for use in `ConfigureServices`:</span></span>

```csharp
public class Startup
{
    public Startup(IHostingEnvironment env)
    {
        HostingEnvironment = env;
    }

    public IHostingEnvironment HostingEnvironment { get; }

    public void ConfigureServices(IServiceCollection services)
    {
        if (HostingEnvironment.IsDevelopment())
        {
            // Development configuration
        }
        else
        {
            // Staging/Production configuration
        }

        var contentRootPath = HostingEnvironment.ContentRootPath;
    }
}
```

> [!NOTE]
> <span data-ttu-id="81b33-373">`IsDevelopment` 확장 메서드 외에 `IHostingEnvironment`는 `IsStaging`, `IsProduction` 및 `IsEnvironment(string environmentName)` 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-373">In addition to the `IsDevelopment` extension method, `IHostingEnvironment` offers `IsStaging`, `IsProduction`, and `IsEnvironment(string environmentName)` methods.</span></span> <span data-ttu-id="81b33-374">자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b33-374">See [Working with multiple environments](xref:fundamentals/environments) for details.</span></span>

<span data-ttu-id="81b33-375">또한 `IHostingEnvironment` 서비스를 파이프라인 처리를 설정하기 위한 `Configure` 메서드에 직접 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-375">The `IHostingEnvironment` service can also be injected directly into the `Configure` method for setting up the processing pipeline:</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        // In Development, use the developer exception page
        app.UseDeveloperExceptionPage();
    }
    else
    {
        // In Staging/Production, route exceptions to /error
        app.UseExceptionHandler("/error");
    }

    var contentRootPath = env.ContentRootPath;
}
```

<span data-ttu-id="81b33-376">사용자 지정 [미들웨어](xref:fundamentals/middleware/index#writing-middleware)를 만들 때 `IHostingEnvironment`를 `Invoke` 메서드에 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-376">`IHostingEnvironment` can be injected into the `Invoke` method when creating custom [middleware](xref:fundamentals/middleware/index#writing-middleware):</span></span>

```csharp
public async Task Invoke(HttpContext context, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        // Configure middleware for Development
    }
    else
    {
        // Configure middleware for Staging/Production
    }

    var contentRootPath = env.ContentRootPath;
}
```

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="81b33-377">IApplicationLifetime 인터페이스</span><span class="sxs-lookup"><span data-stu-id="81b33-377">IApplicationLifetime interface</span></span>

<span data-ttu-id="81b33-378">[IApplicationLifetime](/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime)은 사후 시작 및 종료 작업을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-378">[IApplicationLifetime](/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime) allows for post-startup and shutdown activities.</span></span> <span data-ttu-id="81b33-379">인터페이스에서 세 가지 속성은 취소 토큰으로, 시작 및 종료 이벤트를 정의하는 `Action` 메서드를 등록하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-379">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span> <span data-ttu-id="81b33-380">또한 `StopApplication` 메서드도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-380">There's also a `StopApplication` method.</span></span>

| <span data-ttu-id="81b33-381">취소 토큰</span><span class="sxs-lookup"><span data-stu-id="81b33-381">Cancellation Token</span></span>    | <span data-ttu-id="81b33-382">트리거되는 경우:</span><span class="sxs-lookup"><span data-stu-id="81b33-382">Triggered when&#8230;</span></span> |
| --------------------- | --------------------- |
| `ApplicationStarted`  | <span data-ttu-id="81b33-383">호스트가 완벽하게 시작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-383">The host has fully started.</span></span> |
| `ApplicationStopping` | <span data-ttu-id="81b33-384">호스트가 정상적으로 종료되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-384">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="81b33-385">요청은 계속 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-385">Requests may still be processing.</span></span> <span data-ttu-id="81b33-386">종료는 이 이벤트가 완료될 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-386">Shutdown blocks until this event completes.</span></span> |
| `ApplicationStopped`  | <span data-ttu-id="81b33-387">호스트가 정상적으로 종료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-387">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="81b33-388">모든 요청이 처리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-388">All requests should be processed.</span></span> <span data-ttu-id="81b33-389">종료는 이 이벤트가 완료될 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-389">Shutdown blocks until this event completes.</span></span> |

| <span data-ttu-id="81b33-390">메서드</span><span class="sxs-lookup"><span data-stu-id="81b33-390">Method</span></span>            | <span data-ttu-id="81b33-391">작업</span><span class="sxs-lookup"><span data-stu-id="81b33-391">Action</span></span>                                           |
| ----------------- | ------------------------------------------------ |
| `StopApplication` | <span data-ttu-id="81b33-392">현재 응용 프로그램의 종료를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-392">Requests termination of the current application.</span></span> |

```csharp
public class Startup 
{
    public void Configure(IApplicationBuilder app, IApplicationLifetime appLifetime) 
    {
        appLifetime.ApplicationStarted.Register(OnStarted);
        appLifetime.ApplicationStopping.Register(OnStopping);
        appLifetime.ApplicationStopped.Register(OnStopped);

        Console.CancelKeyPress += (sender, eventArgs) =>
        {
            appLifetime.StopApplication();
            // Don't terminate the process immediately, wait for the Main thread to exit gracefully.
            eventArgs.Cancel = true;
        };
    }

    private void OnStarted()
    {
        // Perform post-startup activities here
    }

    private void OnStopping()
    {
        // Perform on-stopping activities here
    }

    private void OnStopped()
    {
        // Perform post-stopped activities here
    }
}
```

## <a name="troubleshooting-systemargumentexception"></a><span data-ttu-id="81b33-393">System.ArgumentException 문제 해결</span><span class="sxs-lookup"><span data-stu-id="81b33-393">Troubleshooting System.ArgumentException</span></span>

<span data-ttu-id="81b33-394">**ASP.NET Core 2.0에만 적용**</span><span class="sxs-lookup"><span data-stu-id="81b33-394">**Applies to ASP.NET Core 2.0 Only**</span></span>

<span data-ttu-id="81b33-395">호스트는 `UseStartup` 또는 `Configure`를 호출하는 대신 종속성 주입 컨테이너에 `IStartup`을 직접 주입하여 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-395">A host may be built by injecting `IStartup` directly into the dependency injection container rather than calling `UseStartup` or `Configure`:</span></span>

```csharp
services.AddSingleton<IStartup, Startup>();
```

<span data-ttu-id="81b33-396">호스트가 이러한 방식으로 빌드되면 다음과 같은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-396">If the host is built this way, the following error may occur:</span></span>

```
Unhandled Exception: System.ArgumentException: A valid non-empty application name must be provided.
```

<span data-ttu-id="81b33-397">이는 `HostingStartupAttributes`를 검색하는 데 [applicationName(ApplicationKey)](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey)(현재 어셈블리)이 필요하기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-397">This occurs because the [applicationName(ApplicationKey)](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey) (the current assembly) is required to scan for `HostingStartupAttributes`.</span></span> <span data-ttu-id="81b33-398">앱이 `IStartup`을 종속성 주입 컨테이너에 수동으로 주입하는 경우 다음 호출을 지정된 어셈블리 이름으로 `WebHostBuilder`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-398">If the app manually injects `IStartup` into the dependency injection container, add the following call to `WebHostBuilder` with the assembly name specified:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("applicationName", "<Assembly Name>")
    ...
```

<span data-ttu-id="81b33-399">또는 dummy `Configure`를 `WebHostBuilder`에 추가합니다. 이는 `applicationName`(`ApplicationKey`)을 자동으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-399">Alternatively, add a dummy `Configure` to the `WebHostBuilder`, which sets the `applicationName`(`ApplicationKey`) automatically:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .Configure(_ => { })
    ...
```

<span data-ttu-id="81b33-400">**참고**: 이는 ASP.NET Core 2.0 릴리스와 `UseStartup` 또는 `Configure`를 호출하지 않는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="81b33-400">**NOTE**: This is only required with the ASP.NET Core 2.0 release and only when the app doesn't call `UseStartup` or `Configure`.</span></span>

<span data-ttu-id="81b33-401">자세한 내용은 [알림: Microsoft.Extensions.PlatformAbstractions가 제거되었습니다(주석)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) 및 [StartupInjection 샘플](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81b33-401">For more information, see [Announcements: Microsoft.Extensions.PlatformAbstractions has been removed (comment)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) and the [StartupInjection sample](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81b33-402">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="81b33-402">Additional resources</span></span>

* [<span data-ttu-id="81b33-403">IIS를 사용하여 Windows에서 호스트</span><span class="sxs-lookup"><span data-stu-id="81b33-403">Host on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="81b33-404">Nginx를 사용하여 Linux에서 호스트</span><span class="sxs-lookup"><span data-stu-id="81b33-404">Host on Linux with Nginx</span></span>](xref:host-and-deploy/linux-nginx)
* [<span data-ttu-id="81b33-405">Apache를 사용하여 Linux에서 호스트</span><span class="sxs-lookup"><span data-stu-id="81b33-405">Host on Linux with Apache</span></span>](xref:host-and-deploy/linux-apache)
* [<span data-ttu-id="81b33-406">Windows 서비스에서 호스트</span><span class="sxs-lookup"><span data-stu-id="81b33-406">Host in a Windows Service</span></span>](xref:host-and-deploy/windows-service)
