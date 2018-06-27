---
title: ASP.NET Core 웹 호스트
author: guardrex
description: 앱 시작 및 수명 관리를 담당하는 ASP.NET Core에서의 웹 호스트에 대해 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/16/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/host/web-host
ms.openlocfilehash: ce95599ec8e940635ca63c3bf9a3c28784a3f371
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34687492"
---
# <a name="aspnet-core-web-host"></a><span data-ttu-id="1b9a8-103">ASP.NET Core 웹 호스트</span><span class="sxs-lookup"><span data-stu-id="1b9a8-103">ASP.NET Core Web Host</span></span>

<span data-ttu-id="1b9a8-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="1b9a8-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="1b9a8-105">ASP.NET Core 앱은 *호스트*를 구성 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-105">ASP.NET Core apps configure and launch a *host*.</span></span> <span data-ttu-id="1b9a8-106">호스트는 앱 시작 및 수명 관리를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-106">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="1b9a8-107">최소한으로 호스트는 서버 및 요청 처리 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-107">At a minimum, the host configures a server and a request processing pipeline.</span></span> <span data-ttu-id="1b9a8-108">이 항목에서는 웹 호스팅에 유용한 ASP.NET Core 웹 호스트([IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder))를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-108">This topic covers the ASP.NET Core Web Host ([IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)), which is useful for hosting web apps.</span></span> <span data-ttu-id="1b9a8-109">.NET 일반 호스트([IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder))에 대한 자세한 내용은 [일반 호스트](xref:fundamentals/host/generic-host) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-109">For coverage of the .NET Generic Host ([IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder)), see the [Generic Host](xref:fundamentals/host/generic-host) topic.</span></span>

## <a name="set-up-a-host"></a><span data-ttu-id="1b9a8-110">호스트 설정</span><span class="sxs-lookup"><span data-stu-id="1b9a8-110">Set up a host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1b9a8-111">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-111">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="1b9a8-112">[IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)의 인스턴스를 사용하여 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-112">Create a host using an instance of [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder).</span></span> <span data-ttu-id="1b9a8-113">이는 일반적으로 앱의 진입점에서 수행되는 `Main` 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-113">This is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="1b9a8-114">프로젝트 템플릿에서 `Main`은 *Program.cs*에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-114">In the project templates, `Main` is located in *Program.cs*.</span></span> <span data-ttu-id="1b9a8-115">일반적인 *Program.cs*는 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)를 호출하여 호스트 설정을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-115">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to start setting up a host:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .UseStartup<Startup>();
}
```

<span data-ttu-id="1b9a8-116">`CreateDefaultBuilder`는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-116">`CreateDefaultBuilder` performs the following tasks:</span></span>

* <span data-ttu-id="1b9a8-117">[Kestrel](xref:fundamentals/servers/kestrel)을 웹 서버로 구성하고 앱의 호스팅 구성 공급자를 사용하여 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-117">Configures [Kestrel](xref:fundamentals/servers/kestrel) as the web server and configures the server using the app's hosting configuration providers.</span></span> <span data-ttu-id="1b9a8-118">Kestrel 기본 옵션의 경우 [ASP.NET Core에서 Kestrel 웹 서버 구현의 Kestrel 옵션 섹션](xref:fundamentals/servers/kestrel#kestrel-options)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-118">For the Kestrel default options, see [the Kestrel options section of Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel#kestrel-options).</span></span>
* <span data-ttu-id="1b9a8-119">콘텐츠 루트를 [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory)에서 반환된 경로로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-119">Sets the content root to the path returned by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).</span></span>
* <span data-ttu-id="1b9a8-120">다음에서 선택적인 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-120">Loads optional [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) from:</span></span>
  * <span data-ttu-id="1b9a8-121">*appsettings.json*.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-121">*appsettings.json*.</span></span>
  * <span data-ttu-id="1b9a8-122">*appsettings.{Environment}.json*.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-122">*appsettings.{Environment}.json*.</span></span>
  * <span data-ttu-id="1b9a8-123">앱이 항목 어셈블리를 사용하여 `Development` 환경에서 실행되는 경우 [사용자 암호](xref:security/app-secrets)입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-123">[User secrets](xref:security/app-secrets) when the app runs in the `Development` environment using the entry assembly.</span></span>
  * <span data-ttu-id="1b9a8-124">환경 변수.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-124">Environment variables.</span></span>
  * <span data-ttu-id="1b9a8-125">명령줄 인수.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-125">Command-line arguments.</span></span>
* <span data-ttu-id="1b9a8-126">콘솔 및 디버그 출력에 대한 [로깅](xref:fundamentals/logging/index)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-126">Configures [logging](xref:fundamentals/logging/index) for console and debug output.</span></span> <span data-ttu-id="1b9a8-127">로깅은 *appsettings.json* 또는 *appsettings.{Environment}.json* 파일의 로깅 구성 섹션에 지정된 [로그 필터링](xref:fundamentals/logging/index#log-filtering) 규칙을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-127">Logging includes [log filtering](xref:fundamentals/logging/index#log-filtering) rules specified in a Logging configuration section of an *appsettings.json* or *appsettings.{Environment}.json* file.</span></span>
* <span data-ttu-id="1b9a8-128">IIS 뒤에서 실행하는 경우 [IIS 통합](xref:host-and-deploy/iis/index)을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-128">When running behind IIS, enables [IIS integration](xref:host-and-deploy/iis/index).</span></span> <span data-ttu-id="1b9a8-129">[ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 사용하는 경우 서버가 수신 대기할 기본 경로 및 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-129">Configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="1b9a8-130">모듈은 IIS와 Kestrel 간에 역방향 프록시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-130">The module creates a reverse proxy between IIS and Kestrel.</span></span> <span data-ttu-id="1b9a8-131">또한 [시작 오류를 캡처](#capture-startup-errors)하도록 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-131">Also configures the app to [capture startup errors](#capture-startup-errors).</span></span> <span data-ttu-id="1b9a8-132">IIS 기본 옵션의 경우 [IIS가 있는 Windows에서 ASP.NET Core 호스팅의 IIS 옵션 섹션](xref:host-and-deploy/iis/index#iis-options)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-132">For the IIS default options, see [the IIS options section of Host ASP.NET Core on Windows with IIS](xref:host-and-deploy/iis/index#iis-options).</span></span>
* <span data-ttu-id="1b9a8-133">앱의 환경이 개발인 경우 [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes)을 `true`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-133">Sets [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) to `true` if the app's environment is Development.</span></span> <span data-ttu-id="1b9a8-134">자세한 내용은 [범위 유효성 검사](#scope-validation)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-134">For more information, see [Scope validation](#scope-validation).</span></span>

<span data-ttu-id="1b9a8-135">*콘텐츠 루트*는 호스트가 MVC 뷰 파일과 같은 콘텐츠 파일을 검색하는 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-135">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="1b9a8-136">앱이 프로젝트의 루트 폴더에서 시작되면 프로젝트의 루트 폴더가 콘텐츠 루트로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-136">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="1b9a8-137">이것이 [Visual Studio](https://www.visualstudio.com/) 및 [dotnet 새 템플릿](/dotnet/core/tools/dotnet-new)에서 사용되는 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-137">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="1b9a8-138">앱 구성에 대한 자세한 내용은 [ASP.NET Core의 구성](xref:fundamentals/configuration/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-138">For more information on app configuration, see [Configuration in ASP.NET Core](xref:fundamentals/configuration/index).</span></span>

> [!NOTE]
> <span data-ttu-id="1b9a8-139">ASP.NET Core 2.x에서는 정적 `CreateDefaultBuilder` 메서드 사용에 대한 대안으로 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)에서 호스트를 만들 수 있도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-139">As an alternative to using the static `CreateDefaultBuilder` method, creating a host from [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) is a supported approach with ASP.NET Core 2.x.</span></span> <span data-ttu-id="1b9a8-140">자세한 내용은 ASP.NET Core 1.x 탭을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-140">For more information, see the ASP.NET Core 1.x tab.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1b9a8-141">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-141">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="1b9a8-142">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)의 인스턴스를 사용하여 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-142">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="1b9a8-143">호스트 만들기는 일반적으로 앱의 진입점에서 수행되는 `Main` 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-143">Creating a host is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="1b9a8-144">프로젝트 템플릿에서 `Main`은 *Program.cs*에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-144">In the project templates, `Main` is located in *Program.cs*:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        BuildWebHost(args).Run();
    }

    public static IWebHost BuildWebHost(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .UseStartup<Startup>()
            .Build();
}
```

<span data-ttu-id="1b9a8-145">`WebHostBuilder`에는 [IServer를 구현하는 서버](xref:fundamentals/servers/index)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-145">`WebHostBuilder` requires a [server that implements IServer](xref:fundamentals/servers/index).</span></span> <span data-ttu-id="1b9a8-146">기본 제공 서버는 [Kestrel](xref:fundamentals/servers/kestrel) 및 [HTTP.sys](xref:fundamentals/servers/httpsys)(ASP.NET Core 2.0 출시 전에 HTTP.sys는 [WebListener](xref:fundamentals/servers/weblistener)로 불림)입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-146">The built-in servers are [Kestrel](xref:fundamentals/servers/kestrel) and [HTTP.sys](xref:fundamentals/servers/httpsys) (prior to the release of ASP.NET Core 2.0, HTTP.sys was called [WebListener](xref:fundamentals/servers/weblistener)).</span></span> <span data-ttu-id="1b9a8-147">이 예제에서는 [UseKestrel 확장 메서드](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)가 Kestrel 서버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-147">In this example, the [UseKestrel extension method](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) specifies the Kestrel server.</span></span>

<span data-ttu-id="1b9a8-148">*콘텐츠 루트*는 호스트가 MVC 뷰 파일과 같은 콘텐츠 파일을 검색하는 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-148">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="1b9a8-149">[Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1)에서 `UseContentRoot`에 대한 기본 콘텐츠 루트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-149">The default content root is obtained for `UseContentRoot` by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1).</span></span> <span data-ttu-id="1b9a8-150">앱이 프로젝트의 루트 폴더에서 시작되면 프로젝트의 루트 폴더가 콘텐츠 루트로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-150">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="1b9a8-151">이것이 [Visual Studio](https://www.visualstudio.com/) 및 [dotnet 새 템플릿](/dotnet/core/tools/dotnet-new)에서 사용되는 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-151">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="1b9a8-152">IIS를 역방향 프록시로 사용하려면 호스트 빌드 과정 중 일환으로 [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions)을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-152">To use IIS as a reverse proxy, call [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions) as part of building the host.</span></span> <span data-ttu-id="1b9a8-153">`UseIISIntegration`은 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)과 달리 *서버*를 구성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-153">`UseIISIntegration` doesn't configure a *server*, like [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) does.</span></span> <span data-ttu-id="1b9a8-154">`UseIISIntegration`은 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 사용하여 Kestrel과 IIS 간 역방향 프록시를 만드는 경우 서버가 수신 대기할 기본 경로 및 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-154">`UseIISIntegration` configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) to create a reverse proxy between Kestrel and IIS.</span></span> <span data-ttu-id="1b9a8-155">ASP.NET Core와 함께 IIS를 사용하려면 `UseKestrel` 및 `UseIISIntegration`을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-155">To use IIS with ASP.NET Core, `UseKestrel` and `UseIISIntegration` must be specified.</span></span> <span data-ttu-id="1b9a8-156">`UseIISIntegration`은 IIS 또는 IIS Express 뒤에서 실행하는 경우에만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-156">`UseIISIntegration` only activates when running behind IIS or IIS Express.</span></span> <span data-ttu-id="1b9a8-157">자세한 내용은 [ASP.NET Core 모듈 소개](xref:fundamentals/servers/aspnet-core-module) 및 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-157">For more information, see [Introduction to ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

<span data-ttu-id="1b9a8-158">호스트(및 ASP.NET Core 앱)를 구성하는 최소 구현에는 서버와 앱의 요청 파이프라인의 구성을 지정하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-158">A minimal implementation that configures a host (and an ASP.NET Core app) includes specifying a server and configuration of the app's request pipeline:</span></span>

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

<span data-ttu-id="1b9a8-159">호스트를 설정할 때 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) 및 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) 메서드가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-159">When setting up a host, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) and [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) methods can be provided.</span></span> <span data-ttu-id="1b9a8-160">`Startup` 클래스가 지정된 경우 `Configure` 메서드를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-160">If a `Startup` class is specified, it must define a `Configure` method.</span></span> <span data-ttu-id="1b9a8-161">자세한 내용은 [ASP.NET Core에서 응용 프로그램 시작](xref:fundamentals/startup)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-161">For more information, see [Application Startup in ASP.NET Core](xref:fundamentals/startup).</span></span> <span data-ttu-id="1b9a8-162">`ConfigureServices`에 대한 여러 호출은 서로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-162">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="1b9a8-163">`WebHostBuilder`에서 `Configure` 또는 `UseStartup`에 대한 여러 호출은 이전 설정을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-163">Multiple calls to `Configure` or `UseStartup` on the `WebHostBuilder` replace previous settings.</span></span>

## <a name="host-configuration-values"></a><span data-ttu-id="1b9a8-164">호스트 구성 값</span><span class="sxs-lookup"><span data-stu-id="1b9a8-164">Host configuration values</span></span>

<span data-ttu-id="1b9a8-165">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)는 호스트 구성 값을 설정하기 위해 다음 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-165">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) relies on the following approaches to set the host configuration values:</span></span>

* <span data-ttu-id="1b9a8-166">`ASPNETCORE_{configurationKey}` 형식의 환경 변수를 포함하는 호스트 빌더 구성.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-166">Host builder configuration, which includes environment variables with the format `ASPNETCORE_{configurationKey}`.</span></span> <span data-ttu-id="1b9a8-167">예를 들어, `ASPNETCORE_ENVIRONMENT`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-167">For example, `ASPNETCORE_ENVIRONMENT`.</span></span>
* <span data-ttu-id="1b9a8-168">[HostingAbstractionsWebHostBuilderExtensions.UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot)와 같은 명시적 메서드.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-168">Explicit methods, such as [HostingAbstractionsWebHostBuilderExtensions.UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot).</span></span>
* <span data-ttu-id="1b9a8-169">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) 및 연결된 키.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-169">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) and the associated key.</span></span> <span data-ttu-id="1b9a8-170">`UseSetting`을 사용하여 값을 설정할 때 값은 형식에 관계 없이 문자열로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-170">When setting a value with `UseSetting`, the value is set as a string regardless of the type.</span></span>

<span data-ttu-id="1b9a8-171">호스트는 마지막에 값을 설정한 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-171">The host uses whichever option sets a value last.</span></span> <span data-ttu-id="1b9a8-172">자세한 내용은 다음 섹션의 [구성 재정의](#override-configuration)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-172">For more information, see [Override configuration](#override-configuration) in the next section.</span></span>

### <a name="capture-startup-errors"></a><span data-ttu-id="1b9a8-173">시작 오류 캡처</span><span class="sxs-lookup"><span data-stu-id="1b9a8-173">Capture Startup Errors</span></span>

<span data-ttu-id="1b9a8-174">이 설정은 시작 오류의 캡처를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-174">This setting controls the capture of startup errors.</span></span>

<span data-ttu-id="1b9a8-175">**키**: captureStartupErrors</span><span class="sxs-lookup"><span data-stu-id="1b9a8-175">**Key**: captureStartupErrors</span></span>  
<span data-ttu-id="1b9a8-176">**형식**: *bool*(`true` 또는 `1`)</span><span class="sxs-lookup"><span data-stu-id="1b9a8-176">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="1b9a8-177">**기본값**: 기본값이 `true`인 IIS 뒤에 있는 Kestrel로 앱이 실행하지 않는 한 기본값은 `false`로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-177">**Default**: Defaults to `false` unless the app runs with Kestrel behind IIS, where the default is `true`.</span></span>  
<span data-ttu-id="1b9a8-178">**설정 방법**: `CaptureStartupErrors`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-178">**Set using**: `CaptureStartupErrors`</span></span>  
<span data-ttu-id="1b9a8-179">**환경 변수**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-179">**Environment variable**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span></span>

<span data-ttu-id="1b9a8-180">`false`인 경우 시작 시 오류가 발생하면 호스트가 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-180">When `false`, errors during startup result in the host exiting.</span></span> <span data-ttu-id="1b9a8-181">`true`이면 호스트가 시작 시 예외를 캡처하고 서버 시작을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-181">When `true`, the host captures exceptions during startup and attempts to start the server.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1b9a8-182">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-182">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .CaptureStartupErrors(true)
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1b9a8-183">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-183">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .CaptureStartupErrors(true)
```

---

### <a name="content-root"></a><span data-ttu-id="1b9a8-184">콘텐츠 루트</span><span class="sxs-lookup"><span data-stu-id="1b9a8-184">Content Root</span></span>

<span data-ttu-id="1b9a8-185">이 설정은 ASP.NET Core가 MVC 뷰와 같은 콘텐츠 파일을 검색하기 시작하는 지점을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-185">This setting determines where ASP.NET Core begins searching for content files, such as MVC views.</span></span> 

<span data-ttu-id="1b9a8-186">**키**: contentRoot</span><span class="sxs-lookup"><span data-stu-id="1b9a8-186">**Key**: contentRoot</span></span>  
<span data-ttu-id="1b9a8-187">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="1b9a8-187">**Type**: *string*</span></span>  
<span data-ttu-id="1b9a8-188">**기본값**: 앱 어셈블리가 있는 폴더가 기본값으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-188">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="1b9a8-189">**설정 방법**: `UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-189">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="1b9a8-190">**환경 변수**: `ASPNETCORE_CONTENTROOT`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-190">**Environment variable**: `ASPNETCORE_CONTENTROOT`</span></span>

<span data-ttu-id="1b9a8-191">콘텐츠 루트는 또한 [웹 루트 설정](#web-root)에 대한 기본 경로로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-191">The content root is also used as the base path for the [Web Root setting](#web-root).</span></span> <span data-ttu-id="1b9a8-192">경로가 존재하지 않는 경우 호스트가 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-192">If the path doesn't exist, the host fails to start.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1b9a8-193">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-193">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseContentRoot("c:\\<content-root>")
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1b9a8-194">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-194">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseContentRoot("c:\\<content-root>")
```

---

### <a name="detailed-errors"></a><span data-ttu-id="1b9a8-195">자세한 오류</span><span class="sxs-lookup"><span data-stu-id="1b9a8-195">Detailed Errors</span></span>

<span data-ttu-id="1b9a8-196">자세한 오류를 캡처해야 하는지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-196">Determines if detailed errors should be captured.</span></span>

<span data-ttu-id="1b9a8-197">**키**: detailedErrors</span><span class="sxs-lookup"><span data-stu-id="1b9a8-197">**Key**: detailedErrors</span></span>  
<span data-ttu-id="1b9a8-198">**형식**: *bool*(`true` 또는 `1`)</span><span class="sxs-lookup"><span data-stu-id="1b9a8-198">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="1b9a8-199">**기본값**: false</span><span class="sxs-lookup"><span data-stu-id="1b9a8-199">**Default**: false</span></span>  
<span data-ttu-id="1b9a8-200">**설정 방법**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-200">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="1b9a8-201">**환경 변수**: `ASPNETCORE_DETAILEDERRORS`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-201">**Environment variable**: `ASPNETCORE_DETAILEDERRORS`</span></span>

<span data-ttu-id="1b9a8-202">사용하는 경우(또는 <a href="#environment">환경</a>이 `Development`로 설정된 경우) 앱은 자세한 예외를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-202">When enabled (or when the <a href="#environment">Environment</a> is set to `Development`), the app captures detailed exceptions.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1b9a8-203">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-203">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1b9a8-204">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-204">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
```

---

### <a name="environment"></a><span data-ttu-id="1b9a8-205">환경</span><span class="sxs-lookup"><span data-stu-id="1b9a8-205">Environment</span></span>

<span data-ttu-id="1b9a8-206">앱의 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-206">Sets the app's environment.</span></span>

<span data-ttu-id="1b9a8-207">**키**: environment</span><span class="sxs-lookup"><span data-stu-id="1b9a8-207">**Key**: environment</span></span>  
<span data-ttu-id="1b9a8-208">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="1b9a8-208">**Type**: *string*</span></span>  
<span data-ttu-id="1b9a8-209">**기본값**: Production</span><span class="sxs-lookup"><span data-stu-id="1b9a8-209">**Default**: Production</span></span>  
<span data-ttu-id="1b9a8-210">**설정 방법**: `UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-210">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="1b9a8-211">**환경 변수**: `ASPNETCORE_ENVIRONMENT`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-211">**Environment variable**: `ASPNETCORE_ENVIRONMENT`</span></span>

<span data-ttu-id="1b9a8-212">환경은 어떠한 값으로도 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-212">The environment can be set to any value.</span></span> <span data-ttu-id="1b9a8-213">프레임워크에서 정의된 값은 `Development`, `Staging` 및 `Production`을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-213">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="1b9a8-214">값은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-214">Values aren't case sensitive.</span></span> <span data-ttu-id="1b9a8-215">기본적으로 *환경*은 `ASPNETCORE_ENVIRONMENT` 환경 변수에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-215">By default, the *Environment* is read from the `ASPNETCORE_ENVIRONMENT` environment variable.</span></span> <span data-ttu-id="1b9a8-216">[Visual Studio](https://www.visualstudio.com/)를 사용하는 경우 환경 변수는 *launchSettings.json* 파일에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-216">When using [Visual Studio](https://www.visualstudio.com/), environment variables may be set in the *launchSettings.json* file.</span></span> <span data-ttu-id="1b9a8-217">자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-217">For more information, see [Use multiple environments](xref:fundamentals/environments).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1b9a8-218">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-218">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseEnvironment(EnvironmentName.Development)
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1b9a8-219">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-219">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseEnvironment(EnvironmentName.Development)
```

---

### <a name="hosting-startup-assemblies"></a><span data-ttu-id="1b9a8-220">호스팅 시작 어셈블리</span><span class="sxs-lookup"><span data-stu-id="1b9a8-220">Hosting Startup Assemblies</span></span>

<span data-ttu-id="1b9a8-221">앱의 호스팅 시작 어셈블리를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-221">Sets the app's hosting startup assemblies.</span></span>

<span data-ttu-id="1b9a8-222">**키**: hostingStartupAssemblies</span><span class="sxs-lookup"><span data-stu-id="1b9a8-222">**Key**: hostingStartupAssemblies</span></span>  
<span data-ttu-id="1b9a8-223">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="1b9a8-223">**Type**: *string*</span></span>  
<span data-ttu-id="1b9a8-224">**기본값**: 빈 문자열</span><span class="sxs-lookup"><span data-stu-id="1b9a8-224">**Default**: Empty string</span></span>  
<span data-ttu-id="1b9a8-225">**설정 방법**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-225">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="1b9a8-226">**환경 변수**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-226">**Environment variable**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span></span>

<span data-ttu-id="1b9a8-227">시작 시 로드할 호스팅 시작 어셈블리의 세미콜론으로 구분된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-227">A semicolon-delimited string of hosting startup assemblies to load on startup.</span></span> <span data-ttu-id="1b9a8-228">이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-228">This feature is new in ASP.NET Core 2.0.</span></span>

<span data-ttu-id="1b9a8-229">구성 값의 기본값이 빈 문자열이지만, 호스팅 시작 어셈블리는 항상 앱의 어셈블리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-229">Although the configuration value defaults to an empty string, the hosting startup assemblies always include the app's assembly.</span></span> <span data-ttu-id="1b9a8-230">호스팅 시작 어셈블리가 제공되는 경우, 시작 시 앱이 일반적인 서비스를 빌드할 때 로드를 위해 앱의 어셈블리에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-230">When hosting startup assemblies are provided, they're added to the app's assembly for loading when the app builds its common services during startup.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1b9a8-231">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-231">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupAssembliesKey, "assembly1;assembly2")
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1b9a8-232">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-232">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="1b9a8-233">이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-233">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prefer-hosting-urls"></a><span data-ttu-id="1b9a8-234">호스팅 URL 선호</span><span class="sxs-lookup"><span data-stu-id="1b9a8-234">Prefer Hosting URLs</span></span>

<span data-ttu-id="1b9a8-235">호스트가 `IServer` 구현으로 구성된 URL 대신에 `WebHostBuilder`로 구성된 URL에서 수신 대기할지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-235">Indicates whether the host should listen on the URLs configured with the `WebHostBuilder` instead of those configured with the `IServer` implementation.</span></span>

<span data-ttu-id="1b9a8-236">**키**: preferHostingUrls</span><span class="sxs-lookup"><span data-stu-id="1b9a8-236">**Key**: preferHostingUrls</span></span>  
<span data-ttu-id="1b9a8-237">**형식**: *bool*(`true` 또는 `1`)</span><span class="sxs-lookup"><span data-stu-id="1b9a8-237">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="1b9a8-238">**기본값**: true</span><span class="sxs-lookup"><span data-stu-id="1b9a8-238">**Default**: true</span></span>  
<span data-ttu-id="1b9a8-239">**설정 방법**: `PreferHostingUrls`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-239">**Set using**: `PreferHostingUrls`</span></span>  
<span data-ttu-id="1b9a8-240">**환경 변수**: `ASPNETCORE_PREFERHOSTINGURLS`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-240">**Environment variable**: `ASPNETCORE_PREFERHOSTINGURLS`</span></span>

<span data-ttu-id="1b9a8-241">이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-241">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1b9a8-242">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-242">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .PreferHostingUrls(false)
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1b9a8-243">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-243">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="1b9a8-244">이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-244">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prevent-hosting-startup"></a><span data-ttu-id="1b9a8-245">호스팅 시작 방지</span><span class="sxs-lookup"><span data-stu-id="1b9a8-245">Prevent Hosting Startup</span></span>

<span data-ttu-id="1b9a8-246">앱의 어셈블리에 의해 구성된 호스팅 시작 어셈블리를 포함한 호스팅 시작 어셈블리의 자동 로딩을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-246">Prevents the automatic loading of hosting startup assemblies, including hosting startup assemblies configured by the app's assembly.</span></span> <span data-ttu-id="1b9a8-247">자세한 내용은 [IHostingStartup을 사용하여 외부 어셈블리에서 앱 강화](xref:fundamentals/configuration/platform-specific-configuration)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-247">See [Enhance an app from an external assembly with IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration) for more information.</span></span>

<span data-ttu-id="1b9a8-248">**키**: preventHostingStartup</span><span class="sxs-lookup"><span data-stu-id="1b9a8-248">**Key**: preventHostingStartup</span></span>  
<span data-ttu-id="1b9a8-249">**형식**: *bool*(`true` 또는 `1`)</span><span class="sxs-lookup"><span data-stu-id="1b9a8-249">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="1b9a8-250">**기본값**: false</span><span class="sxs-lookup"><span data-stu-id="1b9a8-250">**Default**: false</span></span>  
<span data-ttu-id="1b9a8-251">**설정 방법**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-251">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="1b9a8-252">**환경 변수**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-252">**Environment variable**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span></span>

<span data-ttu-id="1b9a8-253">이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-253">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1b9a8-254">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-254">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.PreventHostingStartupKey, "true")
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1b9a8-255">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-255">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="1b9a8-256">이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-256">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="server-urls"></a><span data-ttu-id="1b9a8-257">서버 URL</span><span class="sxs-lookup"><span data-stu-id="1b9a8-257">Server URLs</span></span>

<span data-ttu-id="1b9a8-258">서버에서 요청을 수신해야 하는 포트와 프로토콜이 있는 IP 주소 또는 호스트 주소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-258">Indicates the IP addresses or host addresses with ports and protocols that the server should listen on for requests.</span></span>

<span data-ttu-id="1b9a8-259">**키**: urls</span><span class="sxs-lookup"><span data-stu-id="1b9a8-259">**Key**: urls</span></span>  
<span data-ttu-id="1b9a8-260">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="1b9a8-260">**Type**: *string*</span></span>  
<span data-ttu-id="1b9a8-261">**기본**: http://localhost:5000</span><span class="sxs-lookup"><span data-stu-id="1b9a8-261">**Default**: http://localhost:5000</span></span>  
<span data-ttu-id="1b9a8-262">**설정 방법**: `UseUrls`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-262">**Set using**: `UseUrls`</span></span>  
<span data-ttu-id="1b9a8-263">**환경 변수**: `ASPNETCORE_URLS`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-263">**Environment variable**: `ASPNETCORE_URLS`</span></span>

<span data-ttu-id="1b9a8-264">서버가 응답해야 하는 세미콜론으로 구분된(;) URL 접두사의 목록으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-264">Set to a semicolon-separated (;) list of URL prefixes to which the server should respond.</span></span> <span data-ttu-id="1b9a8-265">예를 들어, `http://localhost:123`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-265">For example, `http://localhost:123`.</span></span> <span data-ttu-id="1b9a8-266">“\*”를 사용하여 서버가 지정된 포트 및 프로토콜을 사용하는 IP 주소 또는 호스트 이름에서 요청을 수신해야 함을 나타냅니다(예: `http://*:5000`).</span><span class="sxs-lookup"><span data-stu-id="1b9a8-266">Use "\*" to indicate that the server should listen for requests on any IP address or hostname using the specified port and protocol (for example, `http://*:5000`).</span></span> <span data-ttu-id="1b9a8-267">프로토콜(`http://` 또는 `https://`)은 각 URL에 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-267">The protocol (`http://` or `https://`) must be included with each URL.</span></span> <span data-ttu-id="1b9a8-268">지원되는 형식은 서버마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-268">Supported formats vary between servers.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1b9a8-269">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-269">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
```

<span data-ttu-id="1b9a8-270">Kestrel에는 자체 엔드포인트 구성 API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-270">Kestrel has its own endpoint configuration API.</span></span> <span data-ttu-id="1b9a8-271">자세한 내용은 [ASP.NET Core의 Kestrel 웹 서버 구현](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-271">For more information, see [Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1b9a8-272">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-272">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
```

---

### <a name="shutdown-timeout"></a><span data-ttu-id="1b9a8-273">시스템 종료 제한 시간</span><span class="sxs-lookup"><span data-stu-id="1b9a8-273">Shutdown Timeout</span></span>

<span data-ttu-id="1b9a8-274">웹 호스트가 종료될 때까지 기다리는 시간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-274">Specifies the amount of time to wait for the web host to shut down.</span></span>

<span data-ttu-id="1b9a8-275">**키**: shutdownTimeoutSeconds</span><span class="sxs-lookup"><span data-stu-id="1b9a8-275">**Key**: shutdownTimeoutSeconds</span></span>  
<span data-ttu-id="1b9a8-276">**형식**: *int*</span><span class="sxs-lookup"><span data-stu-id="1b9a8-276">**Type**: *int*</span></span>  
<span data-ttu-id="1b9a8-277">**기본값**: 5</span><span class="sxs-lookup"><span data-stu-id="1b9a8-277">**Default**: 5</span></span>  
<span data-ttu-id="1b9a8-278">**설정 방법**: `UseShutdownTimeout`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-278">**Set using**: `UseShutdownTimeout`</span></span>  
<span data-ttu-id="1b9a8-279">**환경 변수**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-279">**Environment variable**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span></span>

<span data-ttu-id="1b9a8-280">키가 `UseSetting`을 통해 *int*를 허용하더라도(예: `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`) [UseShutdownTimeout](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useshutdowntimeout) 확장 메서드는 [TimeSpan](/dotnet/api/system.timespan)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-280">Although the key accepts an *int* with `UseSetting` (for example, `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), the [UseShutdownTimeout](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useshutdowntimeout) extension method takes a [TimeSpan](/dotnet/api/system.timespan).</span></span> <span data-ttu-id="1b9a8-281">이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-281">This feature is new in ASP.NET Core 2.0.</span></span>

<span data-ttu-id="1b9a8-282">시간 제한 기간 동안 호스팅:</span><span class="sxs-lookup"><span data-stu-id="1b9a8-282">During the timeout period, hosting:</span></span>

* <span data-ttu-id="1b9a8-283">[IApplicationLifetime.ApplicationStopping](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstopping)을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-283">Triggers [IApplicationLifetime.ApplicationStopping](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstopping).</span></span>
* <span data-ttu-id="1b9a8-284">중지하지 못한 서비스에 대한 모든 오류를 기록하면서 호스팅된 서비스 중지를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-284">Attempts to stop hosted services, logging any errors for services that fail to stop.</span></span>

<span data-ttu-id="1b9a8-285">모든 호스팅된 서비스가 중지하기 전에 시간 제한 기간이 만료되면 앱이 종료될 때 모든 활성화된 나머지 서비스가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-285">If the timeout period expires before all of the hosted services stop, any remaining active services are stopped when the app shuts down.</span></span> <span data-ttu-id="1b9a8-286">처리를 완료하지 않은 경우에도 서비스가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-286">The services stop even if they haven't finished processing.</span></span> <span data-ttu-id="1b9a8-287">서비스를 중지하는 데 시간이 더 필요한 경우 시간 제한을 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-287">If services require additional time to stop, increase the timeout.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1b9a8-288">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-288">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1b9a8-289">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-289">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="1b9a8-290">이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-290">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="startup-assembly"></a><span data-ttu-id="1b9a8-291">시작 어셈블리</span><span class="sxs-lookup"><span data-stu-id="1b9a8-291">Startup Assembly</span></span>

<span data-ttu-id="1b9a8-292">`Startup` 클래스를 검색할 어셈블리를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-292">Determines the assembly to search for the `Startup` class.</span></span>

<span data-ttu-id="1b9a8-293">**키**: startupAssembly</span><span class="sxs-lookup"><span data-stu-id="1b9a8-293">**Key**: startupAssembly</span></span>  
<span data-ttu-id="1b9a8-294">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="1b9a8-294">**Type**: *string*</span></span>  
<span data-ttu-id="1b9a8-295">**기본값**: 앱의 어셈블리</span><span class="sxs-lookup"><span data-stu-id="1b9a8-295">**Default**: The app's assembly</span></span>  
<span data-ttu-id="1b9a8-296">**설정 방법**: `UseStartup`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-296">**Set using**: `UseStartup`</span></span>  
<span data-ttu-id="1b9a8-297">**환경 변수**: `ASPNETCORE_STARTUPASSEMBLY`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-297">**Environment variable**: `ASPNETCORE_STARTUPASSEMBLY`</span></span>

<span data-ttu-id="1b9a8-298">이름(`string`) 또는 형식(`TStartup`)별 어셈블리를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-298">The assembly by name (`string`) or type (`TStartup`) can be referenced.</span></span> <span data-ttu-id="1b9a8-299">`UseStartup` 메서드가 여러 개 호출된 경우 마지막 메서드가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-299">If multiple `UseStartup` methods are called, the last one takes precedence.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1b9a8-300">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-300">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup("StartupAssemblyName")
```

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup<TStartup>()
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1b9a8-301">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-301">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseStartup("StartupAssemblyName")
```

```csharp
var host = new WebHostBuilder()
    .UseStartup<TStartup>()
```

---

### <a name="web-root"></a><span data-ttu-id="1b9a8-302">웹 루트</span><span class="sxs-lookup"><span data-stu-id="1b9a8-302">Web Root</span></span>

<span data-ttu-id="1b9a8-303">앱의 정적 자산에 대한 상대 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-303">Sets the relative path to the app's static assets.</span></span>

<span data-ttu-id="1b9a8-304">**키**: webroot</span><span class="sxs-lookup"><span data-stu-id="1b9a8-304">**Key**: webroot</span></span>  
<span data-ttu-id="1b9a8-305">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="1b9a8-305">**Type**: *string*</span></span>  
<span data-ttu-id="1b9a8-306">**기본값**: 기본값이 지정되지 않은 경우 기본값은 “(Content Root)/wwwroot”입니다(경로가 존재하는 경우).</span><span class="sxs-lookup"><span data-stu-id="1b9a8-306">**Default**: If not specified, the default is "(Content Root)/wwwroot", if the path exists.</span></span> <span data-ttu-id="1b9a8-307">경로가 존재하지 않다면 no-op 파일 공급자가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-307">If the path doesn't exist, then a no-op file provider is used.</span></span>  
<span data-ttu-id="1b9a8-308">**설정 방법**: `UseWebRoot`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-308">**Set using**: `UseWebRoot`</span></span>  
<span data-ttu-id="1b9a8-309">**환경 변수**: `ASPNETCORE_WEBROOT`</span><span class="sxs-lookup"><span data-stu-id="1b9a8-309">**Environment variable**: `ASPNETCORE_WEBROOT`</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1b9a8-310">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-310">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseWebRoot("public")
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1b9a8-311">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-311">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseWebRoot("public")
```

---

## <a name="override-configuration"></a><span data-ttu-id="1b9a8-312">구성 재정의</span><span class="sxs-lookup"><span data-stu-id="1b9a8-312">Override configuration</span></span>

<span data-ttu-id="1b9a8-313">[구성](xref:fundamentals/configuration/index)을 사용하여 호스트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-313">Use [Configuration](xref:fundamentals/configuration/index) to configure the host.</span></span> <span data-ttu-id="1b9a8-314">다음 예제에서는 호스트 구성이 필요에 따라 *hosting.json* 파일에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-314">In the following example, host configuration is optionally specified in a *hosting.json* file.</span></span> <span data-ttu-id="1b9a8-315">*hosting.json* 파일에서 로드된 모든 구성은 명령줄 인수에 의해 재정의될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-315">Any configuration loaded from the *hosting.json* file may be overridden by command-line arguments.</span></span> <span data-ttu-id="1b9a8-316">기본 제공된 구성(`config`에 있음)은 `UseConfiguration`을 통해 호스트를 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-316">The built configuration (in `config`) is used to configure the host with `UseConfiguration`.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1b9a8-317">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-317">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="1b9a8-318">*hosting.json*:</span><span class="sxs-lookup"><span data-stu-id="1b9a8-318">*hosting.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

<span data-ttu-id="1b9a8-319">먼저 *hosting.json* 구성으로 `UseUrls`에 의해 제공되는 구성을 재정의하고, 두 번째로 명령줄 인수 구성을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-319">Overriding the configuration provided by `UseUrls` with *hosting.json* config first, command-line argument config second:</span></span>

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

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1b9a8-320">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-320">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="1b9a8-321">*hosting.json*:</span><span class="sxs-lookup"><span data-stu-id="1b9a8-321">*hosting.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

<span data-ttu-id="1b9a8-322">먼저 *hosting.json* 구성으로 `UseUrls`에 의해 제공되는 구성을 재정의하고, 두 번째로 명령줄 인수 구성을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-322">Overriding the configuration provided by `UseUrls` with *hosting.json* config first, command-line argument config second:</span></span>

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
> <span data-ttu-id="1b9a8-323">[UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 확장 메서드는 현재 `GetSection`에서 반환되는 구성 섹션을 구문 분석할 수 없습니다(예: `.UseConfiguration(Configuration.GetSection("section"))`).</span><span class="sxs-lookup"><span data-stu-id="1b9a8-323">The [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) extension method isn't currently capable of parsing a configuration section returned by `GetSection` (for example, `.UseConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="1b9a8-324">`GetSection` 메서드는 요청된 섹션에 대한 구성 키를 필터링하지만 키에 있는 섹션 이름을 그대로 둡니다(예: `section:urls`, `section:environment`).</span><span class="sxs-lookup"><span data-stu-id="1b9a8-324">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:urls`, `section:environment`).</span></span> <span data-ttu-id="1b9a8-325">`UseConfiguration` 메서드에서는 키가 `WebHostBuilder` 키와 일치해야 합니다(예: `urls`, `environment`).</span><span class="sxs-lookup"><span data-stu-id="1b9a8-325">The `UseConfiguration` method expects the keys to match the `WebHostBuilder` keys (for example, `urls`, `environment`).</span></span> <span data-ttu-id="1b9a8-326">키에서 섹션 이름의 존재는 섹션 값으로 호스트를 구성할 수 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-326">The presence of the section name on the keys prevents the section's values from configuring the host.</span></span> <span data-ttu-id="1b9a8-327">이 문제는 향후 릴리스에서 해결될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-327">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="1b9a8-328">자세한 내용 및 해결 방법은 [전체 키를 사용하여 WebHostBuilder.UseConfiguration에 구성 섹션을 전달](https://github.com/aspnet/Hosting/issues/839)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-328">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>

<span data-ttu-id="1b9a8-329">특정 URL에서 실행하는 호스트를 지정하려면 [dotnet run](/dotnet/core/tools/dotnet-run) 실행 시 원하는 값을 명령 프롬프트에서 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-329">To specify the host run on a particular URL, the desired value can be passed in from a command prompt when executing [dotnet run](/dotnet/core/tools/dotnet-run).</span></span> <span data-ttu-id="1b9a8-330">명령줄 인수는 *hosting.json* 파일의 `urls` 값을 재정의하고, 서버는 포트 8080에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-330">The command-line argument overrides the `urls` value from the *hosting.json* file, and the server listens on port 8080:</span></span>

```console
dotnet run --urls "http://*:8080"
```

## <a name="manage-the-host"></a><span data-ttu-id="1b9a8-331">호스트 관리</span><span class="sxs-lookup"><span data-stu-id="1b9a8-331">Manage the host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1b9a8-332">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-332">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="1b9a8-333">**실행**</span><span class="sxs-lookup"><span data-stu-id="1b9a8-333">**Run**</span></span>

<span data-ttu-id="1b9a8-334">`Run` 메서드는 웹앱을 시작하고 호스트가 종료될 때까지 호출 스레드를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-334">The `Run` method starts the web app and blocks the calling thread until the host is shut down:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="1b9a8-335">**Start**</span><span class="sxs-lookup"><span data-stu-id="1b9a8-335">**Start**</span></span>

<span data-ttu-id="1b9a8-336">해당 `Start` 메서드를 호출하여 비차단 방식으로 호스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-336">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="1b9a8-337">URL 목록이 `Start` 메서드에 전달되면 지정된 URL에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-337">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>

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

<span data-ttu-id="1b9a8-338">앱은 정적 편의 메서드를 사용하여 `CreateDefaultBuilder`의 미리 구성된 기본 값을 사용하는 새 호스트를 초기화하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-338">The app can initialize and start a new host using the pre-configured defaults of `CreateDefaultBuilder` using a static convenience method.</span></span> <span data-ttu-id="1b9a8-339">이러한 메서드는 콘솔 출력 없이 서버를 시작하고 [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown)으로 중단(Ctrl-C/SIGINT 또는 SIGTERM)될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-339">These methods start the server without console output and with [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) wait for a break (Ctrl-C/SIGINT or SIGTERM):</span></span>

<span data-ttu-id="1b9a8-340">**Start(RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="1b9a8-340">**Start(RequestDelegate app)**</span></span>

<span data-ttu-id="1b9a8-341">`RequestDelegate`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-341">Start with a `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start(app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="1b9a8-342">`http://localhost:5000`에 대한 브라우저에서 요청을 수행하여 “Hello World!” 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-342">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="1b9a8-343">`WaitForShutdown`은 중단(Ctrl-C/SIGINT 또는 SIGTERM)이 발생할 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-343">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="1b9a8-344">앱은 `Console.WriteLine` 메시지를 표시하고 keypress가 종료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-344">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="1b9a8-345">**Start(string url, RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="1b9a8-345">**Start(string url, RequestDelegate app)**</span></span>

<span data-ttu-id="1b9a8-346">URL 및 `RequestDelegate`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-346">Start with a URL and `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start("http://localhost:8080", app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="1b9a8-347">앱이 `http://localhost:8080`에서 응답한다는 점을 제외하고 **Start(RequestDelegate app)** 와 동일한 결과가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-347">Produces the same result as **Start(RequestDelegate app)**, except the app responds on `http://localhost:8080`.</span></span>

<span data-ttu-id="1b9a8-348">**Start(Action&lt;IRouteBuilder&gt; routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="1b9a8-348">**Start(Action&lt;IRouteBuilder&gt; routeBuilder)**</span></span>

<span data-ttu-id="1b9a8-349">`IRouteBuilder`의 인스턴스([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/))를 사용하여 라우팅 미들웨어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-349">Use an instance of `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) to use routing middleware:</span></span>

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

<span data-ttu-id="1b9a8-350">예제에서는 다음 브라우저 요청을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-350">Use the following browser requests with the example:</span></span>

| <span data-ttu-id="1b9a8-351">요청</span><span class="sxs-lookup"><span data-stu-id="1b9a8-351">Request</span></span>                                    | <span data-ttu-id="1b9a8-352">응답</span><span class="sxs-lookup"><span data-stu-id="1b9a8-352">Response</span></span>                                 |
| ------------------------------------------ | ---------------------------------------- |
| `http://localhost:5000/hello/Martin`       | <span data-ttu-id="1b9a8-353">Hello, Martin!</span><span class="sxs-lookup"><span data-stu-id="1b9a8-353">Hello, Martin!</span></span>                           |
| `http://localhost:5000/buenosdias/Catrina` | <span data-ttu-id="1b9a8-354">Buenos dias, Catrina!</span><span class="sxs-lookup"><span data-stu-id="1b9a8-354">Buenos dias, Catrina!</span></span>                    |
| `http://localhost:5000/throw/ooops!`       | <span data-ttu-id="1b9a8-355">“ooops!” 문자열을 사용하여 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-355">Throws an exception with string "ooops!"</span></span> |
| `http://localhost:5000/throw`              | <span data-ttu-id="1b9a8-356">“Uh oh!” 문자열을 사용하여 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-356">Throws an exception with string "Uh oh!"</span></span> |
| `http://localhost:5000/Sante/Kevin`        | <span data-ttu-id="1b9a8-357">Sante, Kevin!</span><span class="sxs-lookup"><span data-stu-id="1b9a8-357">Sante, Kevin!</span></span>                            |
| `http://localhost:5000`                    | <span data-ttu-id="1b9a8-358">Hello World!</span><span class="sxs-lookup"><span data-stu-id="1b9a8-358">Hello World!</span></span>                             |

<span data-ttu-id="1b9a8-359">`WaitForShutdown`은 중단(Ctrl-C/SIGINT 또는 SIGTERM)이 발생할 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-359">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="1b9a8-360">앱은 `Console.WriteLine` 메시지를 표시하고 keypress가 종료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-360">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="1b9a8-361">**Start(string url, Action&lt;IRouteBuilder&gt; routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="1b9a8-361">**Start(string url, Action&lt;IRouteBuilder&gt; routeBuilder)**</span></span>

<span data-ttu-id="1b9a8-362">URL 및 `IRouteBuilder`의 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-362">Use a URL and an instance of `IRouteBuilder`:</span></span>

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
    Console.WriteLine("Use Ctrl-C to shut down the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="1b9a8-363">앱이 `http://localhost:8080`에서 응답한다는 점을 제외하고 **Start(Action&lt;IRouteBuilder&gt; routeBuilder)** 와 동일한 결과가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-363">Produces the same result as **Start(Action&lt;IRouteBuilder&gt; routeBuilder)**, except the app responds at `http://localhost:8080`.</span></span>

<span data-ttu-id="1b9a8-364">**StartWith(Action&lt;IApplicationBuilder&gt; app)**</span><span class="sxs-lookup"><span data-stu-id="1b9a8-364">**StartWith(Action&lt;IApplicationBuilder&gt; app)**</span></span>

<span data-ttu-id="1b9a8-365">대리자를 제공하여 `IApplicationBuilder`를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-365">Provide a delegate to configure an `IApplicationBuilder`:</span></span>

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
    Console.WriteLine("Use Ctrl-C to shut down the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="1b9a8-366">`http://localhost:5000`에 대한 브라우저에서 요청을 수행하여 “Hello World!” 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-366">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="1b9a8-367">`WaitForShutdown`은 중단(Ctrl-C/SIGINT 또는 SIGTERM)이 발생할 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-367">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="1b9a8-368">앱은 `Console.WriteLine` 메시지를 표시하고 keypress가 종료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-368">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="1b9a8-369">**StartWith(string url, Action&lt;IApplicationBuilder&gt; app)**</span><span class="sxs-lookup"><span data-stu-id="1b9a8-369">**StartWith(string url, Action&lt;IApplicationBuilder&gt; app)**</span></span>

<span data-ttu-id="1b9a8-370">URL 및 대리자를 제공하여 `IApplicationBuilder`를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-370">Provide a URL and a delegate to configure an `IApplicationBuilder`:</span></span>

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
    Console.WriteLine("Use Ctrl-C to shut down the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="1b9a8-371">앱이 `http://localhost:8080`에서 응답한다는 점을 제외하고 **StartWith(Action&lt;IApplicationBuilder&gt; app)** 와 동일한 결과가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-371">Produces the same result as **StartWith(Action&lt;IApplicationBuilder&gt; app)**, except the app responds on `http://localhost:8080`.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1b9a8-372">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1b9a8-372">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="1b9a8-373">**실행**</span><span class="sxs-lookup"><span data-stu-id="1b9a8-373">**Run**</span></span>

<span data-ttu-id="1b9a8-374">`Run` 메서드는 웹앱을 시작하고 호스트가 종료될 때까지 호출 스레드를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-374">The `Run` method starts the web app and blocks the calling thread until the host is shut down:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="1b9a8-375">**Start**</span><span class="sxs-lookup"><span data-stu-id="1b9a8-375">**Start**</span></span>

<span data-ttu-id="1b9a8-376">해당 `Start` 메서드를 호출하여 비차단 방식으로 호스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-376">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="1b9a8-377">URL 목록이 `Start` 메서드에 전달되면 지정된 URL에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-377">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>

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

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="1b9a8-378">IHostingEnvironment 인터페이스</span><span class="sxs-lookup"><span data-stu-id="1b9a8-378">IHostingEnvironment interface</span></span>

<span data-ttu-id="1b9a8-379">[IHostingEnvironment 인터페이스](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment)는 앱의 웹 호스팅 환경에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-379">The [IHostingEnvironment interface](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) provides information about the app's web hosting environment.</span></span> <span data-ttu-id="1b9a8-380">해당 속성 및 확장 메서드를 사용하기 위해 [생성자 주입](xref:fundamentals/dependency-injection)을 사용하여 `IHostingEnvironment`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-380">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

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

<span data-ttu-id="1b9a8-381">[규칙 기반 접근 방식](xref:fundamentals/environments#startup-conventions)은 시작할 때 환경에 따라 앱을 구성하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-381">A [convention-based approach](xref:fundamentals/environments#startup-conventions) can be used to configure the app at startup based on the environment.</span></span> <span data-ttu-id="1b9a8-382">또는 `ConfigureServices`에서 사용할 수 있도록 `IHostingEnvironment`를 `Startup` 생성자에 주입합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-382">Alternatively, inject the `IHostingEnvironment` into the `Startup` constructor for use in `ConfigureServices`:</span></span>

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
> <span data-ttu-id="1b9a8-383">`IsDevelopment` 확장 메서드 외에 `IHostingEnvironment`는 `IsStaging`, `IsProduction` 및 `IsEnvironment(string environmentName)` 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-383">In addition to the `IsDevelopment` extension method, `IHostingEnvironment` offers `IsStaging`, `IsProduction`, and `IsEnvironment(string environmentName)` methods.</span></span> <span data-ttu-id="1b9a8-384">자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-384">See [Use multiple environments](xref:fundamentals/environments) for details.</span></span>

<span data-ttu-id="1b9a8-385">또한 `IHostingEnvironment` 서비스를 파이프라인 처리를 설정하기 위한 `Configure` 메서드에 직접 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-385">The `IHostingEnvironment` service can also be injected directly into the `Configure` method for setting up the processing pipeline:</span></span>

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

<span data-ttu-id="1b9a8-386">사용자 지정 [미들웨어](xref:fundamentals/middleware/index#writing-middleware)를 만들 때 `IHostingEnvironment`를 `Invoke` 메서드에 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-386">`IHostingEnvironment` can be injected into the `Invoke` method when creating custom [middleware](xref:fundamentals/middleware/index#writing-middleware):</span></span>

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

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="1b9a8-387">IApplicationLifetime 인터페이스</span><span class="sxs-lookup"><span data-stu-id="1b9a8-387">IApplicationLifetime interface</span></span>

<span data-ttu-id="1b9a8-388">[IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime)은 사후 시작 및 종료 작업을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-388">[IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) allows for post-startup and shutdown activities.</span></span> <span data-ttu-id="1b9a8-389">인터페이스에서 세 가지 속성은 취소 토큰으로, 시작 및 종료 이벤트를 정의하는 `Action` 메서드를 등록하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-389">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span>

| <span data-ttu-id="1b9a8-390">취소 토큰</span><span class="sxs-lookup"><span data-stu-id="1b9a8-390">Cancellation Token</span></span>    | <span data-ttu-id="1b9a8-391">트리거되는 경우:</span><span class="sxs-lookup"><span data-stu-id="1b9a8-391">Triggered when&#8230;</span></span> |
| --------------------- | --------------------- |
| [<span data-ttu-id="1b9a8-392">ApplicationStarted</span><span class="sxs-lookup"><span data-stu-id="1b9a8-392">ApplicationStarted</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstarted) | <span data-ttu-id="1b9a8-393">호스트가 완벽하게 시작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-393">The host has fully started.</span></span> |
| [<span data-ttu-id="1b9a8-394">ApplicationStopped</span><span class="sxs-lookup"><span data-stu-id="1b9a8-394">ApplicationStopped</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopped) | <span data-ttu-id="1b9a8-395">호스트가 정상적으로 종료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-395">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="1b9a8-396">모든 요청이 처리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-396">All requests should be processed.</span></span> <span data-ttu-id="1b9a8-397">종료는 이 이벤트가 완료될 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-397">Shutdown blocks until this event completes.</span></span> |
| [<span data-ttu-id="1b9a8-398">ApplicationStopping</span><span class="sxs-lookup"><span data-stu-id="1b9a8-398">ApplicationStopping</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopping) | <span data-ttu-id="1b9a8-399">호스트가 정상적으로 종료되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-399">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="1b9a8-400">요청은 계속 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-400">Requests may still be processing.</span></span> <span data-ttu-id="1b9a8-401">종료는 이 이벤트가 완료될 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-401">Shutdown blocks until this event completes.</span></span> |

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

<span data-ttu-id="1b9a8-402">[StopApplication](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.stopapplication)은 앱의 종료를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-402">[StopApplication](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.stopapplication) requests termination of the app.</span></span> <span data-ttu-id="1b9a8-403">다음 클래스에서는 `StopApplication`을 사용하여 해당 클래스의 `Shutdown` 메서드를 호출하는 경우 앱을 정상 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-403">The following class uses `StopApplication` to gracefully shut down an app when the class's `Shutdown` method is called:</span></span>

```csharp
public class MyClass
{
    private readonly IApplicationLifetime _appLifetime;

    public MyClass(IApplicationLifetime appLifetime)
    {
        _appLifetime = appLifetime;
    }

    public void Shutdown()
    {
        _appLifetime.StopApplication();
    }
}
```

## <a name="scope-validation"></a><span data-ttu-id="1b9a8-404">범위 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="1b9a8-404">Scope validation</span></span>

<span data-ttu-id="1b9a8-405">ASP.NET Core 2.0 이상에서 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)은 앱의 환경이 개발인 경우 [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes)를 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-405">In ASP.NET Core 2.0 or later, [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) sets [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) to `true` if the app's environment is Development.</span></span>

<span data-ttu-id="1b9a8-406">`ValidateScopes`이 `true`로 설정된 경우 기본 서비스 공급자는 다음을 확인하기 위해 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-406">When `ValidateScopes` is set to `true`, the default service provider performs checks to verify that:</span></span>

* <span data-ttu-id="1b9a8-407">범위가 지정된 서비스는 직접 또는 간접적으로 루트 서비스 공급자에서 해결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-407">Scoped services aren't directly or indirectly resolved from the root service provider.</span></span>
* <span data-ttu-id="1b9a8-408">범위가 지정된 서비스는 직접 또는 간접적으로 싱글톤에 삽입되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-408">Scoped services aren't directly or indirectly injected into singletons.</span></span>

<span data-ttu-id="1b9a8-409">루트 서비스 공급자는 [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider)를 호출할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-409">The root service provider is created when [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider) is called.</span></span> <span data-ttu-id="1b9a8-410">루트 서비스 공급자의 수명은 공급자가 앱과 함께 시작되고 앱이 종료될 때 삭제되는 앱/서버의 수명에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-410">The root service provider's lifetime corresponds to the app/server's lifetime when the provider starts with the app and is disposed when the app shuts down.</span></span>

<span data-ttu-id="1b9a8-411">범위가 지정된 서비스는 서비스를 만든 컨테이너에 의해 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-411">Scoped services are disposed by the container that created them.</span></span> <span data-ttu-id="1b9a8-412">범위가 지정된 서비스가 루트 컨테이너에서 만들어지는 경우 서비스의 수명은 효과적으로 싱글톤으로 승격됩니다. 해당 서비스는 앱/서버가 종료될 때 루트 컨테이너에 의해서만 삭제되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-412">If a scoped service is created in the root container, the service's lifetime is effectively promoted to singleton because it's only disposed by the root container when app/server is shut down.</span></span> <span data-ttu-id="1b9a8-413">서비스 범위의 유효성 검사는 `BuildServiceProvider`이 호출될 경우 이러한 상황을 catch합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-413">Validating service scopes catches these situations when `BuildServiceProvider` is called.</span></span>

<span data-ttu-id="1b9a8-414">프로덕션 환경을 포함하여 범위의 유효성을 검사하려면 호스트 작성기에서 [ServiceProviderOptions](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions)을 [UseDefaultServiceProvider](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usedefaultserviceprovider)로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-414">To always validate scopes, including in the Production environment, configure the [ServiceProviderOptions](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions) with [UseDefaultServiceProvider](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usedefaultserviceprovider) on the host builder:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseDefaultServiceProvider((context, options) => {
        options.ValidateScopes = true;
    })
```

## <a name="troubleshooting-systemargumentexception"></a><span data-ttu-id="1b9a8-415">System.ArgumentException 문제 해결</span><span class="sxs-lookup"><span data-stu-id="1b9a8-415">Troubleshooting System.ArgumentException</span></span>

<span data-ttu-id="1b9a8-416">**ASP.NET Core 2.0에만 적용**</span><span class="sxs-lookup"><span data-stu-id="1b9a8-416">**Applies to ASP.NET Core 2.0 Only**</span></span>

<span data-ttu-id="1b9a8-417">호스트는 `UseStartup` 또는 `Configure`를 호출하는 대신 종속성 주입 컨테이너에 `IStartup`을 직접 주입하여 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-417">A host may be built by injecting `IStartup` directly into the dependency injection container rather than calling `UseStartup` or `Configure`:</span></span>

```csharp
services.AddSingleton<IStartup, Startup>();
```

<span data-ttu-id="1b9a8-418">호스트가 이러한 방식으로 빌드되면 다음과 같은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-418">If the host is built this way, the following error may occur:</span></span>

```
Unhandled Exception: System.ArgumentException: A valid non-empty application name must be provided.
```

<span data-ttu-id="1b9a8-419">이는 `HostingStartupAttributes`를 검색하는 데 [applicationName(ApplicationKey)](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey)(현재 어셈블리)이 필요하기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-419">This occurs because the [applicationName(ApplicationKey)](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey) (the current assembly) is required to scan for `HostingStartupAttributes`.</span></span> <span data-ttu-id="1b9a8-420">앱이 `IStartup`을 종속성 주입 컨테이너에 수동으로 주입하는 경우 다음 호출을 지정된 어셈블리 이름으로 `WebHostBuilder`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-420">If the app manually injects `IStartup` into the dependency injection container, add the following call to `WebHostBuilder` with the assembly name specified:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("applicationName", "<Assembly Name>")
    ...
```

<span data-ttu-id="1b9a8-421">또는 dummy `Configure`를 `WebHostBuilder`에 추가합니다. 이는 `applicationName`(`ApplicationKey`)을 자동으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-421">Alternatively, add a dummy `Configure` to the `WebHostBuilder`, which sets the `applicationName`(`ApplicationKey`) automatically:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .Configure(_ => { })
    ...
```

<span data-ttu-id="1b9a8-422">**참고**: 이는 ASP.NET Core 2.0 릴리스와 `UseStartup` 또는 `Configure`를 호출하지 않는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-422">**NOTE**: This is only required with the ASP.NET Core 2.0 release and only when the app doesn't call `UseStartup` or `Configure`.</span></span>

<span data-ttu-id="1b9a8-423">자세한 내용은 [알림: Microsoft.Extensions.PlatformAbstractions가 제거되었습니다(주석)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) 및 [StartupInjection 샘플](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9a8-423">For more information, see [Announcements: Microsoft.Extensions.PlatformAbstractions has been removed (comment)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) and the [StartupInjection sample](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b9a8-424">추가 자료</span><span class="sxs-lookup"><span data-stu-id="1b9a8-424">Additional resources</span></span>

* [<span data-ttu-id="1b9a8-425">IIS를 사용하여 Windows에서 호스트</span><span class="sxs-lookup"><span data-stu-id="1b9a8-425">Host on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="1b9a8-426">Nginx를 사용하여 Linux에서 호스트</span><span class="sxs-lookup"><span data-stu-id="1b9a8-426">Host on Linux with Nginx</span></span>](xref:host-and-deploy/linux-nginx)
* [<span data-ttu-id="1b9a8-427">Apache를 사용하여 Linux에서 호스트</span><span class="sxs-lookup"><span data-stu-id="1b9a8-427">Host on Linux with Apache</span></span>](xref:host-and-deploy/linux-apache)
* [<span data-ttu-id="1b9a8-428">Windows 서비스에서 호스트</span><span class="sxs-lookup"><span data-stu-id="1b9a8-428">Host in a Windows Service</span></span>](xref:host-and-deploy/windows-service)
