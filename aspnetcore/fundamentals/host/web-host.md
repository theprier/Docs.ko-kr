---
title: ASP.NET Core 웹 호스트
author: guardrex
description: 앱 시작 및 수명 관리를 담당하는 ASP.NET Core에서의 웹 호스트에 대해 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 06/19/2018
uid: fundamentals/host/web-host
ms.openlocfilehash: 98070f49c98919e7ebff41ecc69c953249977dcc
ms.sourcegitcommit: e22097b84d26a812cd1380a6b2d12c93e522c125
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36314151"
---
# <a name="aspnet-core-web-host"></a><span data-ttu-id="b0dcb-103">ASP.NET Core 웹 호스트</span><span class="sxs-lookup"><span data-stu-id="b0dcb-103">ASP.NET Core Web Host</span></span>

<span data-ttu-id="b0dcb-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="b0dcb-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="b0dcb-105">ASP.NET Core 앱은 *호스트*를 구성 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-105">ASP.NET Core apps configure and launch a *host*.</span></span> <span data-ttu-id="b0dcb-106">호스트는 앱 시작 및 수명 관리를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-106">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="b0dcb-107">최소한으로 호스트는 서버 및 요청 처리 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-107">At a minimum, the host configures a server and a request processing pipeline.</span></span> <span data-ttu-id="b0dcb-108">이 항목에서는 웹 호스팅에 유용한 ASP.NET Core 웹 호스트([IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder))를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-108">This topic covers the ASP.NET Core Web Host ([IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)), which is useful for hosting web apps.</span></span> <span data-ttu-id="b0dcb-109">.NET 일반 호스트([IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder))에 대한 자세한 내용은 [일반 호스트](xref:fundamentals/host/generic-host) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-109">For coverage of the .NET Generic Host ([IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder)), see the [Generic Host](xref:fundamentals/host/generic-host) topic.</span></span>

## <a name="set-up-a-host"></a><span data-ttu-id="b0dcb-110">호스트 설정</span><span class="sxs-lookup"><span data-stu-id="b0dcb-110">Set up a host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b0dcb-111">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-111">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="b0dcb-112">[IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)의 인스턴스를 사용하여 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-112">Create a host using an instance of [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder).</span></span> <span data-ttu-id="b0dcb-113">이는 일반적으로 앱의 진입점에서 수행되는 `Main` 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-113">This is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="b0dcb-114">프로젝트 템플릿에서 `Main`은 *Program.cs*에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-114">In the project templates, `Main` is located in *Program.cs*.</span></span> <span data-ttu-id="b0dcb-115">일반적인 *Program.cs*는 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)를 호출하여 호스트 설정을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-115">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to start setting up a host:</span></span>

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

<span data-ttu-id="b0dcb-116">`CreateDefaultBuilder`는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-116">`CreateDefaultBuilder` performs the following tasks:</span></span>

* <span data-ttu-id="b0dcb-117">[Kestrel](xref:fundamentals/servers/kestrel)을 웹 서버로 구성하고 앱의 호스팅 구성 공급자를 사용하여 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-117">Configures [Kestrel](xref:fundamentals/servers/kestrel) as the web server and configures the server using the app's hosting configuration providers.</span></span> <span data-ttu-id="b0dcb-118">Kestrel 기본 옵션의 경우 [ASP.NET Core에서 Kestrel 웹 서버 구현의 Kestrel 옵션 섹션](xref:fundamentals/servers/kestrel#kestrel-options)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-118">For the Kestrel default options, see [the Kestrel options section of Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel#kestrel-options).</span></span>
* <span data-ttu-id="b0dcb-119">콘텐츠 루트를 [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory)에서 반환된 경로로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-119">Sets the content root to the path returned by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).</span></span>
* <span data-ttu-id="b0dcb-120">다음에서 [호스트 구성](#host-configuration-values)을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-120">Loads [host configuration](#host-configuration-values) from:</span></span>
  * <span data-ttu-id="b0dcb-121">접두사가 `ASPNETCORE_`인 환경 변수(예: `ASPNETCORE_ENVIRONMENT`)입니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-121">Environment variables prefixed with `ASPNETCORE_` (for example, `ASPNETCORE_ENVIRONMENT`).</span></span>
  * <span data-ttu-id="b0dcb-122">명령줄 인수.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-122">Command-line arguments.</span></span>
* <span data-ttu-id="b0dcb-123">다음에서 앱 구성을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-123">Loads app configuration from:</span></span>
  * <span data-ttu-id="b0dcb-124">*appsettings.json*.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-124">*appsettings.json*.</span></span>
  * <span data-ttu-id="b0dcb-125">*appsettings.{Environment}.json*.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-125">*appsettings.{Environment}.json*.</span></span>
  * <span data-ttu-id="b0dcb-126">앱이 항목 어셈블리를 사용하여 `Development` 환경에서 실행되는 경우 [사용자 암호](xref:security/app-secrets)입니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-126">[User secrets](xref:security/app-secrets) when the app runs in the `Development` environment using the entry assembly.</span></span>
  * <span data-ttu-id="b0dcb-127">환경 변수.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-127">Environment variables.</span></span>
  * <span data-ttu-id="b0dcb-128">명령줄 인수.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-128">Command-line arguments.</span></span>
* <span data-ttu-id="b0dcb-129">콘솔 및 디버그 출력에 대한 [로깅](xref:fundamentals/logging/index)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-129">Configures [logging](xref:fundamentals/logging/index) for console and debug output.</span></span> <span data-ttu-id="b0dcb-130">로깅은 *appsettings.json* 또는 *appsettings.{Environment}.json* 파일의 로깅 구성 섹션에 지정된 [로그 필터링](xref:fundamentals/logging/index#log-filtering) 규칙을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-130">Logging includes [log filtering](xref:fundamentals/logging/index#log-filtering) rules specified in a Logging configuration section of an *appsettings.json* or *appsettings.{Environment}.json* file.</span></span>
* <span data-ttu-id="b0dcb-131">IIS 뒤에서 실행하는 경우 [IIS 통합](xref:host-and-deploy/iis/index)을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-131">When running behind IIS, enables [IIS integration](xref:host-and-deploy/iis/index).</span></span> <span data-ttu-id="b0dcb-132">[ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 사용하는 경우 서버가 수신 대기할 기본 경로 및 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-132">Configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="b0dcb-133">모듈은 IIS와 Kestrel 간에 역방향 프록시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-133">The module creates a reverse proxy between IIS and Kestrel.</span></span> <span data-ttu-id="b0dcb-134">또한 [시작 오류를 캡처](#capture-startup-errors)하도록 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-134">Also configures the app to [capture startup errors](#capture-startup-errors).</span></span> <span data-ttu-id="b0dcb-135">IIS 기본 옵션의 경우 [IIS가 있는 Windows에서 ASP.NET Core 호스팅의 IIS 옵션 섹션](xref:host-and-deploy/iis/index#iis-options)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-135">For the IIS default options, see [the IIS options section of Host ASP.NET Core on Windows with IIS](xref:host-and-deploy/iis/index#iis-options).</span></span>
* <span data-ttu-id="b0dcb-136">앱의 환경이 개발인 경우 [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes)을 `true`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-136">Sets [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) to `true` if the app's environment is Development.</span></span> <span data-ttu-id="b0dcb-137">자세한 내용은 [범위 유효성 검사](#scope-validation)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-137">For more information, see [Scope validation](#scope-validation).</span></span>

<span data-ttu-id="b0dcb-138">`CreateDefaultBuilder`에 의해 정의된 구성은 [ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration), [ConfigureLogging](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configurelogging), 기타 메서드 및 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)의 확장 메서드로 재정의되고 확대될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-138">The configuration defined by `CreateDefaultBuilder` can be overridden and augmented by [ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration), [ConfigureLogging](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configurelogging), and other methods and extension methods of [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder).</span></span> <span data-ttu-id="b0dcb-139">몇 가지 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-139">A few examples follow:</span></span>

* <span data-ttu-id="b0dcb-140">[ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration)은 앱에 대한 추가 `IConfiguration`을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-140">[ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration) is used to specify additional `IConfiguration` for the app.</span></span> <span data-ttu-id="b0dcb-141">다음 `ConfigureAppConfiguration` 호출은 *appsettings.xml* 파일에 앱 구성을 포함하는 대리자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-141">The following `ConfigureAppConfiguration` call adds a delegate to include app configuration in the *appsettings.xml* file.</span></span> <span data-ttu-id="b0dcb-142">`ConfigureAppConfiguration`이 여러 번 호출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-142">`ConfigureAppConfiguration` may be called multiple times.</span></span> <span data-ttu-id="b0dcb-143">이 구성은 호스트(예: 서버 URL 또는 환경)에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-143">Note that this configuration doesn't apply to the host (for example, server URLs or environment).</span></span> <span data-ttu-id="b0dcb-144">[호스트 구성 값](#host-configuration-values) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-144">See the [Host configuration values](#host-configuration-values) section.</span></span>

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .ConfigureAppConfiguration((hostingContext, config) =>
        {
            config.AddXmlFile("appsettings.xml", optional: true, reloadOnChange: true);
        })
        ...
    ```

* <span data-ttu-id="b0dcb-145">다음 `ConfigureLogging` 호출은 최소 로깅 수준([SetMinimumLevel](/dotnet/api/microsoft.extensions.logging.loggingbuilderextensions.setminimumlevel))을 [LogLevel.Warning](/dotnet/api/microsoft.extensions.logging.loglevel)으로 구성하는 대리자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-145">The following `ConfigureLogging` call adds a delegate to configure the minimum logging level ([SetMinimumLevel](/dotnet/api/microsoft.extensions.logging.loggingbuilderextensions.setminimumlevel)) to [LogLevel.Warning](/dotnet/api/microsoft.extensions.logging.loglevel).</span></span> <span data-ttu-id="b0dcb-146">이 설정은 `CreateDefaultBuilder`에 의해 구성된 *appsettings.Development.json*(`LogLevel.Debug`) 및 *appsettings.Production.json*(`LogLevel.Error`)의 설정을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-146">This setting overrides the settings in *appsettings.Development.json* (`LogLevel.Debug`) and *appsettings.Production.json* (`LogLevel.Error`) configured by `CreateDefaultBuilder`.</span></span> <span data-ttu-id="b0dcb-147">`ConfigureLogging`이 여러 번 호출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-147">`ConfigureLogging` may be called multiple times.</span></span>

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .ConfigureLogging(logging => 
        {
            logging.SetMinimumLevel(LogLevel.Warning);
        })
        ...
    ```

* <span data-ttu-id="b0dcb-148">[UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel)에 대한 다음 호출은 Kestrel이 `CreateDefaultBuilder`에 의해 구성될 때 설정된 30,000,000바이트의 기본 [Limits.MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize)를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-148">The following call to [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) overrides the default [Limits.MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize) of 30,000,000 bytes established when Kestrel was configured by `CreateDefaultBuilder`:</span></span>

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .UseKestrel(options =>
        {
            options.Limits.MaxRequestBodySize = 20000000;
        });
        ...
    ```

<span data-ttu-id="b0dcb-149">*콘텐츠 루트*는 호스트가 MVC 뷰 파일과 같은 콘텐츠 파일을 검색하는 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-149">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="b0dcb-150">앱이 프로젝트의 루트 폴더에서 시작되면 프로젝트의 루트 폴더가 콘텐츠 루트로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-150">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="b0dcb-151">이것이 [Visual Studio](https://www.visualstudio.com/) 및 [dotnet 새 템플릿](/dotnet/core/tools/dotnet-new)에서 사용되는 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-151">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="b0dcb-152">앱 구성에 대한 자세한 내용은 [ASP.NET Core의 구성](xref:fundamentals/configuration/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-152">For more information on app configuration, see [Configuration in ASP.NET Core](xref:fundamentals/configuration/index).</span></span>

> [!NOTE]
> <span data-ttu-id="b0dcb-153">ASP.NET Core 2.x에서는 정적 `CreateDefaultBuilder` 메서드 사용에 대한 대안으로 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)에서 호스트를 만들 수 있도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-153">As an alternative to using the static `CreateDefaultBuilder` method, creating a host from [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) is a supported approach with ASP.NET Core 2.x.</span></span> <span data-ttu-id="b0dcb-154">자세한 내용은 ASP.NET Core 1.x 탭을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-154">For more information, see the ASP.NET Core 1.x tab.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b0dcb-155">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-155">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="b0dcb-156">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)의 인스턴스를 사용하여 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-156">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="b0dcb-157">호스트 만들기는 일반적으로 앱의 진입점에서 수행되는 `Main` 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-157">Creating a host is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="b0dcb-158">프로젝트 템플릿에서 `Main`은 *Program.cs*에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-158">In the project templates, `Main` is located in *Program.cs*:</span></span>

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

<span data-ttu-id="b0dcb-159">`WebHostBuilder`에는 [IServer를 구현하는 서버](xref:fundamentals/servers/index)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-159">`WebHostBuilder` requires a [server that implements IServer](xref:fundamentals/servers/index).</span></span> <span data-ttu-id="b0dcb-160">기본 제공 서버는 [Kestrel](xref:fundamentals/servers/kestrel) 및 [HTTP.sys](xref:fundamentals/servers/httpsys)(ASP.NET Core 2.0 출시 전에 HTTP.sys는 [WebListener](xref:fundamentals/servers/weblistener)로 불림)입니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-160">The built-in servers are [Kestrel](xref:fundamentals/servers/kestrel) and [HTTP.sys](xref:fundamentals/servers/httpsys) (prior to the release of ASP.NET Core 2.0, HTTP.sys was called [WebListener](xref:fundamentals/servers/weblistener)).</span></span> <span data-ttu-id="b0dcb-161">이 예제에서는 [UseKestrel 확장 메서드](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)가 Kestrel 서버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-161">In this example, the [UseKestrel extension method](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) specifies the Kestrel server.</span></span>

<span data-ttu-id="b0dcb-162">*콘텐츠 루트*는 호스트가 MVC 뷰 파일과 같은 콘텐츠 파일을 검색하는 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-162">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="b0dcb-163">[Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1)에서 `UseContentRoot`에 대한 기본 콘텐츠 루트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-163">The default content root is obtained for `UseContentRoot` by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1).</span></span> <span data-ttu-id="b0dcb-164">앱이 프로젝트의 루트 폴더에서 시작되면 프로젝트의 루트 폴더가 콘텐츠 루트로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-164">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="b0dcb-165">이것이 [Visual Studio](https://www.visualstudio.com/) 및 [dotnet 새 템플릿](/dotnet/core/tools/dotnet-new)에서 사용되는 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-165">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="b0dcb-166">IIS를 역방향 프록시로 사용하려면 호스트 빌드 과정 중 일환으로 [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions)을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-166">To use IIS as a reverse proxy, call [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions) as part of building the host.</span></span> <span data-ttu-id="b0dcb-167">`UseIISIntegration`은 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)과 달리 *서버*를 구성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-167">`UseIISIntegration` doesn't configure a *server*, like [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) does.</span></span> <span data-ttu-id="b0dcb-168">`UseIISIntegration`은 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 사용하여 Kestrel과 IIS 간 역방향 프록시를 만드는 경우 서버가 수신 대기할 기본 경로 및 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-168">`UseIISIntegration` configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) to create a reverse proxy between Kestrel and IIS.</span></span> <span data-ttu-id="b0dcb-169">ASP.NET Core와 함께 IIS를 사용하려면 `UseKestrel` 및 `UseIISIntegration`을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-169">To use IIS with ASP.NET Core, `UseKestrel` and `UseIISIntegration` must be specified.</span></span> <span data-ttu-id="b0dcb-170">`UseIISIntegration`은 IIS 또는 IIS Express 뒤에서 실행하는 경우에만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-170">`UseIISIntegration` only activates when running behind IIS or IIS Express.</span></span> <span data-ttu-id="b0dcb-171">자세한 내용은 [ASP.NET Core 모듈 소개](xref:fundamentals/servers/aspnet-core-module) 및 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-171">For more information, see [Introduction to ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

<span data-ttu-id="b0dcb-172">호스트(및 ASP.NET Core 앱)를 구성하는 최소 구현에는 서버와 앱의 요청 파이프라인의 구성을 지정하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-172">A minimal implementation that configures a host (and an ASP.NET Core app) includes specifying a server and configuration of the app's request pipeline:</span></span>

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

<span data-ttu-id="b0dcb-173">호스트를 설정할 때 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) 및 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) 메서드가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-173">When setting up a host, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) and [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) methods can be provided.</span></span> <span data-ttu-id="b0dcb-174">`Startup` 클래스가 지정된 경우 `Configure` 메서드를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-174">If a `Startup` class is specified, it must define a `Configure` method.</span></span> <span data-ttu-id="b0dcb-175">자세한 내용은 [ASP.NET Core에서 응용 프로그램 시작](xref:fundamentals/startup)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-175">For more information, see [Application Startup in ASP.NET Core](xref:fundamentals/startup).</span></span> <span data-ttu-id="b0dcb-176">`ConfigureServices`에 대한 여러 호출은 서로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-176">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="b0dcb-177">`WebHostBuilder`에서 `Configure` 또는 `UseStartup`에 대한 여러 호출은 이전 설정을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-177">Multiple calls to `Configure` or `UseStartup` on the `WebHostBuilder` replace previous settings.</span></span>

## <a name="host-configuration-values"></a><span data-ttu-id="b0dcb-178">호스트 구성 값</span><span class="sxs-lookup"><span data-stu-id="b0dcb-178">Host configuration values</span></span>

<span data-ttu-id="b0dcb-179">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)는 호스트 구성 값을 설정하기 위해 다음 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-179">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) relies on the following approaches to set the host configuration values:</span></span>

* <span data-ttu-id="b0dcb-180">`ASPNETCORE_{configurationKey}` 형식의 환경 변수를 포함하는 호스트 빌더 구성.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-180">Host builder configuration, which includes environment variables with the format `ASPNETCORE_{configurationKey}`.</span></span> <span data-ttu-id="b0dcb-181">예를 들어, `ASPNETCORE_ENVIRONMENT`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-181">For example, `ASPNETCORE_ENVIRONMENT`.</span></span>
* <span data-ttu-id="b0dcb-182">[UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot) 및 [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 같은 확장입니다([구성 재정의](#override-configuration) 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-182">Extensions such as [UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot) and [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) (see the [Override configuration](#override-configuration) section).</span></span>
* <span data-ttu-id="b0dcb-183">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) 및 연결된 키.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-183">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) and the associated key.</span></span> <span data-ttu-id="b0dcb-184">`UseSetting`을 사용하여 값을 설정할 때 값은 형식에 관계 없이 문자열로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-184">When setting a value with `UseSetting`, the value is set as a string regardless of the type.</span></span>

<span data-ttu-id="b0dcb-185">호스트는 마지막에 값을 설정한 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-185">The host uses whichever option sets a value last.</span></span> <span data-ttu-id="b0dcb-186">자세한 내용은 다음 섹션의 [구성 재정의](#override-configuration)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-186">For more information, see [Override configuration](#override-configuration) in the next section.</span></span>

### <a name="capture-startup-errors"></a><span data-ttu-id="b0dcb-187">시작 오류 캡처</span><span class="sxs-lookup"><span data-stu-id="b0dcb-187">Capture Startup Errors</span></span>

<span data-ttu-id="b0dcb-188">이 설정은 시작 오류의 캡처를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-188">This setting controls the capture of startup errors.</span></span>

<span data-ttu-id="b0dcb-189">**키**: captureStartupErrors</span><span class="sxs-lookup"><span data-stu-id="b0dcb-189">**Key**: captureStartupErrors</span></span>  
<span data-ttu-id="b0dcb-190">**형식**: *bool*(`true` 또는 `1`)</span><span class="sxs-lookup"><span data-stu-id="b0dcb-190">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="b0dcb-191">**기본값**: 기본값이 `true`인 IIS 뒤에 있는 Kestrel로 앱이 실행하지 않는 한 기본값은 `false`로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-191">**Default**: Defaults to `false` unless the app runs with Kestrel behind IIS, where the default is `true`.</span></span>  
<span data-ttu-id="b0dcb-192">**설정 방법**: `CaptureStartupErrors`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-192">**Set using**: `CaptureStartupErrors`</span></span>  
<span data-ttu-id="b0dcb-193">**환경 변수**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-193">**Environment variable**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span></span>

<span data-ttu-id="b0dcb-194">`false`인 경우 시작 시 오류가 발생하면 호스트가 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-194">When `false`, errors during startup result in the host exiting.</span></span> <span data-ttu-id="b0dcb-195">`true`이면 호스트가 시작 시 예외를 캡처하고 서버 시작을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-195">When `true`, the host captures exceptions during startup and attempts to start the server.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b0dcb-196">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-196">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .CaptureStartupErrors(true)
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b0dcb-197">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-197">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .CaptureStartupErrors(true)
```

---

### <a name="content-root"></a><span data-ttu-id="b0dcb-198">콘텐츠 루트</span><span class="sxs-lookup"><span data-stu-id="b0dcb-198">Content Root</span></span>

<span data-ttu-id="b0dcb-199">이 설정은 ASP.NET Core가 MVC 뷰와 같은 콘텐츠 파일을 검색하기 시작하는 지점을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-199">This setting determines where ASP.NET Core begins searching for content files, such as MVC views.</span></span> 

<span data-ttu-id="b0dcb-200">**키**: contentRoot</span><span class="sxs-lookup"><span data-stu-id="b0dcb-200">**Key**: contentRoot</span></span>  
<span data-ttu-id="b0dcb-201">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="b0dcb-201">**Type**: *string*</span></span>  
<span data-ttu-id="b0dcb-202">**기본값**: 앱 어셈블리가 있는 폴더가 기본값으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-202">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="b0dcb-203">**설정 방법**: `UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-203">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="b0dcb-204">**환경 변수**: `ASPNETCORE_CONTENTROOT`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-204">**Environment variable**: `ASPNETCORE_CONTENTROOT`</span></span>

<span data-ttu-id="b0dcb-205">콘텐츠 루트는 또한 [웹 루트 설정](#web-root)에 대한 기본 경로로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-205">The content root is also used as the base path for the [Web Root setting](#web-root).</span></span> <span data-ttu-id="b0dcb-206">경로가 존재하지 않는 경우 호스트가 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-206">If the path doesn't exist, the host fails to start.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b0dcb-207">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-207">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseContentRoot("c:\\<content-root>")
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b0dcb-208">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-208">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseContentRoot("c:\\<content-root>")
```

---

### <a name="detailed-errors"></a><span data-ttu-id="b0dcb-209">자세한 오류</span><span class="sxs-lookup"><span data-stu-id="b0dcb-209">Detailed Errors</span></span>

<span data-ttu-id="b0dcb-210">자세한 오류를 캡처해야 하는지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-210">Determines if detailed errors should be captured.</span></span>

<span data-ttu-id="b0dcb-211">**키**: detailedErrors</span><span class="sxs-lookup"><span data-stu-id="b0dcb-211">**Key**: detailedErrors</span></span>  
<span data-ttu-id="b0dcb-212">**형식**: *bool*(`true` 또는 `1`)</span><span class="sxs-lookup"><span data-stu-id="b0dcb-212">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="b0dcb-213">**기본값**: false</span><span class="sxs-lookup"><span data-stu-id="b0dcb-213">**Default**: false</span></span>  
<span data-ttu-id="b0dcb-214">**설정 방법**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-214">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="b0dcb-215">**환경 변수**: `ASPNETCORE_DETAILEDERRORS`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-215">**Environment variable**: `ASPNETCORE_DETAILEDERRORS`</span></span>

<span data-ttu-id="b0dcb-216">사용하는 경우(또는 <a href="#environment">환경</a>이 `Development`로 설정된 경우) 앱은 자세한 예외를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-216">When enabled (or when the <a href="#environment">Environment</a> is set to `Development`), the app captures detailed exceptions.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b0dcb-217">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-217">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b0dcb-218">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-218">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
```

---

### <a name="environment"></a><span data-ttu-id="b0dcb-219">환경</span><span class="sxs-lookup"><span data-stu-id="b0dcb-219">Environment</span></span>

<span data-ttu-id="b0dcb-220">앱의 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-220">Sets the app's environment.</span></span>

<span data-ttu-id="b0dcb-221">**키**: environment</span><span class="sxs-lookup"><span data-stu-id="b0dcb-221">**Key**: environment</span></span>  
<span data-ttu-id="b0dcb-222">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="b0dcb-222">**Type**: *string*</span></span>  
<span data-ttu-id="b0dcb-223">**기본값**: Production</span><span class="sxs-lookup"><span data-stu-id="b0dcb-223">**Default**: Production</span></span>  
<span data-ttu-id="b0dcb-224">**설정 방법**: `UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-224">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="b0dcb-225">**환경 변수**: `ASPNETCORE_ENVIRONMENT`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-225">**Environment variable**: `ASPNETCORE_ENVIRONMENT`</span></span>

<span data-ttu-id="b0dcb-226">환경은 어떠한 값으로도 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-226">The environment can be set to any value.</span></span> <span data-ttu-id="b0dcb-227">프레임워크에서 정의된 값은 `Development`, `Staging` 및 `Production`을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-227">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="b0dcb-228">값은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-228">Values aren't case sensitive.</span></span> <span data-ttu-id="b0dcb-229">기본적으로 *환경*은 `ASPNETCORE_ENVIRONMENT` 환경 변수에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-229">By default, the *Environment* is read from the `ASPNETCORE_ENVIRONMENT` environment variable.</span></span> <span data-ttu-id="b0dcb-230">[Visual Studio](https://www.visualstudio.com/)를 사용하는 경우 환경 변수는 *launchSettings.json* 파일에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-230">When using [Visual Studio](https://www.visualstudio.com/), environment variables may be set in the *launchSettings.json* file.</span></span> <span data-ttu-id="b0dcb-231">자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-231">For more information, see [Use multiple environments](xref:fundamentals/environments).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b0dcb-232">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-232">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseEnvironment(EnvironmentName.Development)
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b0dcb-233">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-233">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseEnvironment(EnvironmentName.Development)
```

---

### <a name="hosting-startup-assemblies"></a><span data-ttu-id="b0dcb-234">호스팅 시작 어셈블리</span><span class="sxs-lookup"><span data-stu-id="b0dcb-234">Hosting Startup Assemblies</span></span>

<span data-ttu-id="b0dcb-235">앱의 호스팅 시작 어셈블리를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-235">Sets the app's hosting startup assemblies.</span></span>

<span data-ttu-id="b0dcb-236">**키**: hostingStartupAssemblies</span><span class="sxs-lookup"><span data-stu-id="b0dcb-236">**Key**: hostingStartupAssemblies</span></span>  
<span data-ttu-id="b0dcb-237">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="b0dcb-237">**Type**: *string*</span></span>  
<span data-ttu-id="b0dcb-238">**기본값**: 빈 문자열</span><span class="sxs-lookup"><span data-stu-id="b0dcb-238">**Default**: Empty string</span></span>  
<span data-ttu-id="b0dcb-239">**설정 방법**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-239">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="b0dcb-240">**환경 변수**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-240">**Environment variable**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span></span>

<span data-ttu-id="b0dcb-241">시작 시 로드할 호스팅 시작 어셈블리의 세미콜론으로 구분된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-241">A semicolon-delimited string of hosting startup assemblies to load on startup.</span></span> <span data-ttu-id="b0dcb-242">이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-242">This feature is new in ASP.NET Core 2.0.</span></span>

<span data-ttu-id="b0dcb-243">구성 값의 기본값이 빈 문자열이지만, 호스팅 시작 어셈블리는 항상 앱의 어셈블리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-243">Although the configuration value defaults to an empty string, the hosting startup assemblies always include the app's assembly.</span></span> <span data-ttu-id="b0dcb-244">호스팅 시작 어셈블리가 제공되는 경우, 시작 시 앱이 일반적인 서비스를 빌드할 때 로드를 위해 앱의 어셈블리에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-244">When hosting startup assemblies are provided, they're added to the app's assembly for loading when the app builds its common services during startup.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b0dcb-245">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-245">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupAssembliesKey, "assembly1;assembly2")
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b0dcb-246">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-246">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b0dcb-247">이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-247">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prefer-hosting-urls"></a><span data-ttu-id="b0dcb-248">호스팅 URL 선호</span><span class="sxs-lookup"><span data-stu-id="b0dcb-248">Prefer Hosting URLs</span></span>

<span data-ttu-id="b0dcb-249">호스트가 `IServer` 구현으로 구성된 URL 대신에 `WebHostBuilder`로 구성된 URL에서 수신 대기할지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-249">Indicates whether the host should listen on the URLs configured with the `WebHostBuilder` instead of those configured with the `IServer` implementation.</span></span>

<span data-ttu-id="b0dcb-250">**키**: preferHostingUrls</span><span class="sxs-lookup"><span data-stu-id="b0dcb-250">**Key**: preferHostingUrls</span></span>  
<span data-ttu-id="b0dcb-251">**형식**: *bool*(`true` 또는 `1`)</span><span class="sxs-lookup"><span data-stu-id="b0dcb-251">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="b0dcb-252">**기본값**: true</span><span class="sxs-lookup"><span data-stu-id="b0dcb-252">**Default**: true</span></span>  
<span data-ttu-id="b0dcb-253">**설정 방법**: `PreferHostingUrls`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-253">**Set using**: `PreferHostingUrls`</span></span>  
<span data-ttu-id="b0dcb-254">**환경 변수**: `ASPNETCORE_PREFERHOSTINGURLS`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-254">**Environment variable**: `ASPNETCORE_PREFERHOSTINGURLS`</span></span>

<span data-ttu-id="b0dcb-255">이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-255">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b0dcb-256">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-256">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .PreferHostingUrls(false)
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b0dcb-257">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-257">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b0dcb-258">이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-258">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prevent-hosting-startup"></a><span data-ttu-id="b0dcb-259">호스팅 시작 방지</span><span class="sxs-lookup"><span data-stu-id="b0dcb-259">Prevent Hosting Startup</span></span>

<span data-ttu-id="b0dcb-260">앱의 어셈블리에 의해 구성된 호스팅 시작 어셈블리를 포함한 호스팅 시작 어셈블리의 자동 로딩을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-260">Prevents the automatic loading of hosting startup assemblies, including hosting startup assemblies configured by the app's assembly.</span></span> <span data-ttu-id="b0dcb-261">자세한 내용은 [IHostingStartup을 사용하여 외부 어셈블리에서 앱 강화](xref:fundamentals/configuration/platform-specific-configuration)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-261">See [Enhance an app from an external assembly with IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration) for more information.</span></span>

<span data-ttu-id="b0dcb-262">**키**: preventHostingStartup</span><span class="sxs-lookup"><span data-stu-id="b0dcb-262">**Key**: preventHostingStartup</span></span>  
<span data-ttu-id="b0dcb-263">**형식**: *bool*(`true` 또는 `1`)</span><span class="sxs-lookup"><span data-stu-id="b0dcb-263">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="b0dcb-264">**기본값**: false</span><span class="sxs-lookup"><span data-stu-id="b0dcb-264">**Default**: false</span></span>  
<span data-ttu-id="b0dcb-265">**설정 방법**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-265">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="b0dcb-266">**환경 변수**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-266">**Environment variable**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span></span>

<span data-ttu-id="b0dcb-267">이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-267">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b0dcb-268">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-268">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.PreventHostingStartupKey, "true")
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b0dcb-269">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-269">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b0dcb-270">이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-270">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="server-urls"></a><span data-ttu-id="b0dcb-271">서버 URL</span><span class="sxs-lookup"><span data-stu-id="b0dcb-271">Server URLs</span></span>

<span data-ttu-id="b0dcb-272">서버에서 요청을 수신해야 하는 포트와 프로토콜이 있는 IP 주소 또는 호스트 주소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-272">Indicates the IP addresses or host addresses with ports and protocols that the server should listen on for requests.</span></span>

<span data-ttu-id="b0dcb-273">**키**: urls</span><span class="sxs-lookup"><span data-stu-id="b0dcb-273">**Key**: urls</span></span>  
<span data-ttu-id="b0dcb-274">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="b0dcb-274">**Type**: *string*</span></span>  
<span data-ttu-id="b0dcb-275">**기본**: http://localhost:5000</span><span class="sxs-lookup"><span data-stu-id="b0dcb-275">**Default**: http://localhost:5000</span></span>  
<span data-ttu-id="b0dcb-276">**설정 방법**: `UseUrls`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-276">**Set using**: `UseUrls`</span></span>  
<span data-ttu-id="b0dcb-277">**환경 변수**: `ASPNETCORE_URLS`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-277">**Environment variable**: `ASPNETCORE_URLS`</span></span>

<span data-ttu-id="b0dcb-278">서버가 응답해야 하는 세미콜론으로 구분된(;) URL 접두사의 목록으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-278">Set to a semicolon-separated (;) list of URL prefixes to which the server should respond.</span></span> <span data-ttu-id="b0dcb-279">예를 들어, `http://localhost:123`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-279">For example, `http://localhost:123`.</span></span> <span data-ttu-id="b0dcb-280">“\*”를 사용하여 서버가 지정된 포트 및 프로토콜을 사용하는 IP 주소 또는 호스트 이름에서 요청을 수신해야 함을 나타냅니다(예: `http://*:5000`).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-280">Use "\*" to indicate that the server should listen for requests on any IP address or hostname using the specified port and protocol (for example, `http://*:5000`).</span></span> <span data-ttu-id="b0dcb-281">프로토콜(`http://` 또는 `https://`)은 각 URL에 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-281">The protocol (`http://` or `https://`) must be included with each URL.</span></span> <span data-ttu-id="b0dcb-282">지원되는 형식은 서버마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-282">Supported formats vary between servers.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b0dcb-283">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-283">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
```

<span data-ttu-id="b0dcb-284">Kestrel에는 자체 엔드포인트 구성 API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-284">Kestrel has its own endpoint configuration API.</span></span> <span data-ttu-id="b0dcb-285">자세한 내용은 [ASP.NET Core의 Kestrel 웹 서버 구현](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-285">For more information, see [Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b0dcb-286">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-286">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
```

---

### <a name="shutdown-timeout"></a><span data-ttu-id="b0dcb-287">시스템 종료 제한 시간</span><span class="sxs-lookup"><span data-stu-id="b0dcb-287">Shutdown Timeout</span></span>

<span data-ttu-id="b0dcb-288">웹 호스트가 종료될 때까지 기다리는 시간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-288">Specifies the amount of time to wait for the web host to shut down.</span></span>

<span data-ttu-id="b0dcb-289">**키**: shutdownTimeoutSeconds</span><span class="sxs-lookup"><span data-stu-id="b0dcb-289">**Key**: shutdownTimeoutSeconds</span></span>  
<span data-ttu-id="b0dcb-290">**형식**: *int*</span><span class="sxs-lookup"><span data-stu-id="b0dcb-290">**Type**: *int*</span></span>  
<span data-ttu-id="b0dcb-291">**기본값**: 5</span><span class="sxs-lookup"><span data-stu-id="b0dcb-291">**Default**: 5</span></span>  
<span data-ttu-id="b0dcb-292">**설정 방법**: `UseShutdownTimeout`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-292">**Set using**: `UseShutdownTimeout`</span></span>  
<span data-ttu-id="b0dcb-293">**환경 변수**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-293">**Environment variable**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span></span>

<span data-ttu-id="b0dcb-294">키가 `UseSetting`을 통해 *int*를 허용하더라도(예: `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`) [UseShutdownTimeout](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useshutdowntimeout) 확장 메서드는 [TimeSpan](/dotnet/api/system.timespan)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-294">Although the key accepts an *int* with `UseSetting` (for example, `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), the [UseShutdownTimeout](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useshutdowntimeout) extension method takes a [TimeSpan](/dotnet/api/system.timespan).</span></span> <span data-ttu-id="b0dcb-295">이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-295">This feature is new in ASP.NET Core 2.0.</span></span>

<span data-ttu-id="b0dcb-296">시간 제한 기간 동안 호스팅:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-296">During the timeout period, hosting:</span></span>

* <span data-ttu-id="b0dcb-297">[IApplicationLifetime.ApplicationStopping](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstopping)을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-297">Triggers [IApplicationLifetime.ApplicationStopping](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstopping).</span></span>
* <span data-ttu-id="b0dcb-298">중지하지 못한 서비스에 대한 모든 오류를 기록하면서 호스팅된 서비스 중지를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-298">Attempts to stop hosted services, logging any errors for services that fail to stop.</span></span>

<span data-ttu-id="b0dcb-299">모든 호스팅된 서비스가 중지하기 전에 시간 제한 기간이 만료되면 앱이 종료될 때 모든 활성화된 나머지 서비스가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-299">If the timeout period expires before all of the hosted services stop, any remaining active services are stopped when the app shuts down.</span></span> <span data-ttu-id="b0dcb-300">처리를 완료하지 않은 경우에도 서비스가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-300">The services stop even if they haven't finished processing.</span></span> <span data-ttu-id="b0dcb-301">서비스를 중지하는 데 시간이 더 필요한 경우 시간 제한을 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-301">If services require additional time to stop, increase the timeout.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b0dcb-302">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-302">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b0dcb-303">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-303">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b0dcb-304">이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-304">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="startup-assembly"></a><span data-ttu-id="b0dcb-305">시작 어셈블리</span><span class="sxs-lookup"><span data-stu-id="b0dcb-305">Startup Assembly</span></span>

<span data-ttu-id="b0dcb-306">`Startup` 클래스를 검색할 어셈블리를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-306">Determines the assembly to search for the `Startup` class.</span></span>

<span data-ttu-id="b0dcb-307">**키**: startupAssembly</span><span class="sxs-lookup"><span data-stu-id="b0dcb-307">**Key**: startupAssembly</span></span>  
<span data-ttu-id="b0dcb-308">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="b0dcb-308">**Type**: *string*</span></span>  
<span data-ttu-id="b0dcb-309">**기본값**: 앱의 어셈블리</span><span class="sxs-lookup"><span data-stu-id="b0dcb-309">**Default**: The app's assembly</span></span>  
<span data-ttu-id="b0dcb-310">**설정 방법**: `UseStartup`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-310">**Set using**: `UseStartup`</span></span>  
<span data-ttu-id="b0dcb-311">**환경 변수**: `ASPNETCORE_STARTUPASSEMBLY`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-311">**Environment variable**: `ASPNETCORE_STARTUPASSEMBLY`</span></span>

<span data-ttu-id="b0dcb-312">이름(`string`) 또는 형식(`TStartup`)별 어셈블리를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-312">The assembly by name (`string`) or type (`TStartup`) can be referenced.</span></span> <span data-ttu-id="b0dcb-313">`UseStartup` 메서드가 여러 개 호출된 경우 마지막 메서드가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-313">If multiple `UseStartup` methods are called, the last one takes precedence.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b0dcb-314">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-314">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup("StartupAssemblyName")
```

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup<TStartup>()
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b0dcb-315">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-315">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseStartup("StartupAssemblyName")
```

```csharp
var host = new WebHostBuilder()
    .UseStartup<TStartup>()
```

---

### <a name="web-root"></a><span data-ttu-id="b0dcb-316">웹 루트</span><span class="sxs-lookup"><span data-stu-id="b0dcb-316">Web Root</span></span>

<span data-ttu-id="b0dcb-317">앱의 정적 자산에 대한 상대 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-317">Sets the relative path to the app's static assets.</span></span>

<span data-ttu-id="b0dcb-318">**키**: webroot</span><span class="sxs-lookup"><span data-stu-id="b0dcb-318">**Key**: webroot</span></span>  
<span data-ttu-id="b0dcb-319">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="b0dcb-319">**Type**: *string*</span></span>  
<span data-ttu-id="b0dcb-320">**기본값**: 기본값이 지정되지 않은 경우 기본값은 “(Content Root)/wwwroot”입니다(경로가 존재하는 경우).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-320">**Default**: If not specified, the default is "(Content Root)/wwwroot", if the path exists.</span></span> <span data-ttu-id="b0dcb-321">경로가 존재하지 않다면 no-op 파일 공급자가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-321">If the path doesn't exist, then a no-op file provider is used.</span></span>  
<span data-ttu-id="b0dcb-322">**설정 방법**: `UseWebRoot`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-322">**Set using**: `UseWebRoot`</span></span>  
<span data-ttu-id="b0dcb-323">**환경 변수**: `ASPNETCORE_WEBROOT`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-323">**Environment variable**: `ASPNETCORE_WEBROOT`</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b0dcb-324">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-324">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseWebRoot("public")
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b0dcb-325">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-325">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseWebRoot("public")
```

---

## <a name="override-configuration"></a><span data-ttu-id="b0dcb-326">구성 재정의</span><span class="sxs-lookup"><span data-stu-id="b0dcb-326">Override configuration</span></span>

<span data-ttu-id="b0dcb-327">[구성](xref:fundamentals/configuration/index)을 사용하여 웹 호스트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-327">Use [Configuration](xref:fundamentals/configuration/index) to configure the web host.</span></span> <span data-ttu-id="b0dcb-328">다음 예제에서는 호스트 구성이 필요에 따라 *hostsettings.json* 파일에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-328">In the following example, host configuration is optionally specified in a *hostsettings.json* file.</span></span> <span data-ttu-id="b0dcb-329">*hostsettings.json* 파일에서 로드된 모든 구성은 명령줄 인수에 의해 재정의될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-329">Any configuration loaded from the *hostsettings.json* file may be overridden by command-line arguments.</span></span> <span data-ttu-id="b0dcb-330">빌드된 구성(`config`에 있음)은 [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration)을 통해 호스트를 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-330">The built configuration (in `config`) is used to configure the host with [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration).</span></span> <span data-ttu-id="b0dcb-331">`IWebHostBuilder` 구성이 앱의 구성에 추가되지만 반대의 경우에는 true가 아닙니다. &mdash;`ConfigureAppConfiguration`은 `IWebHostBuilder` 구성에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-331">`IWebHostBuilder` configuration is added to the app's configuration, but the converse isn't true&mdash;`ConfigureAppConfiguration` doesn't affect the `IWebHostBuilder` configuration.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b0dcb-332">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-332">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="b0dcb-333">먼저 *hostsettings.json* 구성으로 `UseUrls`에 의해 제공되는 구성을 재정의하고, 두 번째로 명령줄 인수 구성을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-333">Overriding the configuration provided by `UseUrls` with *hostsettings.json* config first, command-line argument config second:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hostsettings.json", optional: true)
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

<span data-ttu-id="b0dcb-334">*hostsettings.json*:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-334">*hostsettings.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b0dcb-335">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-335">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b0dcb-336">먼저 *hostsettings.json* 구성으로 `UseUrls`에 의해 제공되는 구성을 재정의하고, 두 번째로 명령줄 인수 구성을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-336">Overriding the configuration provided by `UseUrls` with *hostsettings.json* config first, command-line argument config second:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hostsettings.json", optional: true)
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

<span data-ttu-id="b0dcb-337">*hostsettings.json*:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-337">*hostsettings.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

---

> [!NOTE]
> <span data-ttu-id="b0dcb-338">[UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 확장 메서드는 현재 `GetSection`에서 반환되는 구성 섹션을 구문 분석할 수 없습니다(예: `.UseConfiguration(Configuration.GetSection("section"))`).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-338">The [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) extension method isn't currently capable of parsing a configuration section returned by `GetSection` (for example, `.UseConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="b0dcb-339">`GetSection` 메서드는 요청된 섹션에 대한 구성 키를 필터링하지만 키에 있는 섹션 이름을 그대로 둡니다(예: `section:urls`, `section:environment`).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-339">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:urls`, `section:environment`).</span></span> <span data-ttu-id="b0dcb-340">`UseConfiguration` 메서드에서는 키가 `WebHostBuilder` 키와 일치해야 합니다(예: `urls`, `environment`).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-340">The `UseConfiguration` method expects the keys to match the `WebHostBuilder` keys (for example, `urls`, `environment`).</span></span> <span data-ttu-id="b0dcb-341">키에서 섹션 이름의 존재는 섹션 값으로 호스트를 구성할 수 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-341">The presence of the section name on the keys prevents the section's values from configuring the host.</span></span> <span data-ttu-id="b0dcb-342">이 문제는 향후 릴리스에서 해결될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-342">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="b0dcb-343">자세한 내용 및 해결 방법은 [전체 키를 사용하여 WebHostBuilder.UseConfiguration에 구성 섹션을 전달](https://github.com/aspnet/Hosting/issues/839)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-343">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>
>
> <span data-ttu-id="b0dcb-344">`UseConfiguration`은 제공된 `IConfiguration`의 키만 호스트 빌더 구성으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-344">`UseConfiguration` only copies keys from the provided `IConfiguration` to the host builder configuration.</span></span> <span data-ttu-id="b0dcb-345">따라서 JSON, INI 및 XML 설정 파일에 대해 `reloadOnChange: true`를 설정해도 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-345">Therefore, setting `reloadOnChange: true` for JSON, INI, and XML settings files has no effect.</span></span>

<span data-ttu-id="b0dcb-346">특정 URL에서 실행하는 호스트를 지정하려면 [dotnet run](/dotnet/core/tools/dotnet-run) 실행 시 원하는 값을 명령 프롬프트에서 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-346">To specify the host run on a particular URL, the desired value can be passed in from a command prompt when executing [dotnet run](/dotnet/core/tools/dotnet-run).</span></span> <span data-ttu-id="b0dcb-347">명령줄 인수는 *hostsettings.json* 파일의 `urls` 값을 재정의하고, 서버는 포트 8080에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-347">The command-line argument overrides the `urls` value from the *hostsettings.json* file, and the server listens on port 8080:</span></span>

```console
dotnet run --urls "http://*:8080"
```

## <a name="manage-the-host"></a><span data-ttu-id="b0dcb-348">호스트 관리</span><span class="sxs-lookup"><span data-stu-id="b0dcb-348">Manage the host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b0dcb-349">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-349">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="b0dcb-350">**실행**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-350">**Run**</span></span>

<span data-ttu-id="b0dcb-351">`Run` 메서드는 웹앱을 시작하고 호스트가 종료될 때까지 호출 스레드를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-351">The `Run` method starts the web app and blocks the calling thread until the host is shut down:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="b0dcb-352">**Start**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-352">**Start**</span></span>

<span data-ttu-id="b0dcb-353">해당 `Start` 메서드를 호출하여 비차단 방식으로 호스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-353">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="b0dcb-354">URL 목록이 `Start` 메서드에 전달되면 지정된 URL에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-354">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>

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

<span data-ttu-id="b0dcb-355">앱은 정적 편의 메서드를 사용하여 `CreateDefaultBuilder`의 미리 구성된 기본 값을 사용하는 새 호스트를 초기화하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-355">The app can initialize and start a new host using the pre-configured defaults of `CreateDefaultBuilder` using a static convenience method.</span></span> <span data-ttu-id="b0dcb-356">이러한 메서드는 콘솔 출력 없이 서버를 시작하고 [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown)으로 중단(Ctrl-C/SIGINT 또는 SIGTERM)될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-356">These methods start the server without console output and with [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) wait for a break (Ctrl-C/SIGINT or SIGTERM):</span></span>

<span data-ttu-id="b0dcb-357">**Start(RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-357">**Start(RequestDelegate app)**</span></span>

<span data-ttu-id="b0dcb-358">`RequestDelegate`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-358">Start with a `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start(app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="b0dcb-359">`http://localhost:5000`에 대한 브라우저에서 요청을 수행하여 “Hello World!” 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-359">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="b0dcb-360">`WaitForShutdown`은 중단(Ctrl-C/SIGINT 또는 SIGTERM)이 발생할 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-360">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="b0dcb-361">앱은 `Console.WriteLine` 메시지를 표시하고 keypress가 종료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-361">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="b0dcb-362">**Start(string url, RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-362">**Start(string url, RequestDelegate app)**</span></span>

<span data-ttu-id="b0dcb-363">URL 및 `RequestDelegate`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-363">Start with a URL and `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start("http://localhost:8080", app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="b0dcb-364">앱이 `http://localhost:8080`에서 응답한다는 점을 제외하고 **Start(RequestDelegate app)** 와 동일한 결과가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-364">Produces the same result as **Start(RequestDelegate app)**, except the app responds on `http://localhost:8080`.</span></span>

<span data-ttu-id="b0dcb-365">**Start(Action&lt;IRouteBuilder&gt; routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-365">**Start(Action&lt;IRouteBuilder&gt; routeBuilder)**</span></span>

<span data-ttu-id="b0dcb-366">`IRouteBuilder`의 인스턴스([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/))를 사용하여 라우팅 미들웨어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-366">Use an instance of `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) to use routing middleware:</span></span>

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

<span data-ttu-id="b0dcb-367">예제에서는 다음 브라우저 요청을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-367">Use the following browser requests with the example:</span></span>

| <span data-ttu-id="b0dcb-368">요청</span><span class="sxs-lookup"><span data-stu-id="b0dcb-368">Request</span></span>                                    | <span data-ttu-id="b0dcb-369">응답</span><span class="sxs-lookup"><span data-stu-id="b0dcb-369">Response</span></span>                                 |
| ------------------------------------------ | ---------------------------------------- |
| `http://localhost:5000/hello/Martin`       | <span data-ttu-id="b0dcb-370">Hello, Martin!</span><span class="sxs-lookup"><span data-stu-id="b0dcb-370">Hello, Martin!</span></span>                           |
| `http://localhost:5000/buenosdias/Catrina` | <span data-ttu-id="b0dcb-371">Buenos dias, Catrina!</span><span class="sxs-lookup"><span data-stu-id="b0dcb-371">Buenos dias, Catrina!</span></span>                    |
| `http://localhost:5000/throw/ooops!`       | <span data-ttu-id="b0dcb-372">“ooops!” 문자열을 사용하여 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-372">Throws an exception with string "ooops!"</span></span> |
| `http://localhost:5000/throw`              | <span data-ttu-id="b0dcb-373">“Uh oh!” 문자열을 사용하여 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-373">Throws an exception with string "Uh oh!"</span></span> |
| `http://localhost:5000/Sante/Kevin`        | <span data-ttu-id="b0dcb-374">Sante, Kevin!</span><span class="sxs-lookup"><span data-stu-id="b0dcb-374">Sante, Kevin!</span></span>                            |
| `http://localhost:5000`                    | <span data-ttu-id="b0dcb-375">Hello World!</span><span class="sxs-lookup"><span data-stu-id="b0dcb-375">Hello World!</span></span>                             |

<span data-ttu-id="b0dcb-376">`WaitForShutdown`은 중단(Ctrl-C/SIGINT 또는 SIGTERM)이 발생할 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-376">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="b0dcb-377">앱은 `Console.WriteLine` 메시지를 표시하고 keypress가 종료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-377">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="b0dcb-378">**Start(string url, Action&lt;IRouteBuilder&gt; routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-378">**Start(string url, Action&lt;IRouteBuilder&gt; routeBuilder)**</span></span>

<span data-ttu-id="b0dcb-379">URL 및 `IRouteBuilder`의 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-379">Use a URL and an instance of `IRouteBuilder`:</span></span>

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

<span data-ttu-id="b0dcb-380">앱이 `http://localhost:8080`에서 응답한다는 점을 제외하고 **Start(Action&lt;IRouteBuilder&gt; routeBuilder)** 와 동일한 결과가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-380">Produces the same result as **Start(Action&lt;IRouteBuilder&gt; routeBuilder)**, except the app responds at `http://localhost:8080`.</span></span>

<span data-ttu-id="b0dcb-381">**StartWith(Action&lt;IApplicationBuilder&gt; app)**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-381">**StartWith(Action&lt;IApplicationBuilder&gt; app)**</span></span>

<span data-ttu-id="b0dcb-382">대리자를 제공하여 `IApplicationBuilder`를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-382">Provide a delegate to configure an `IApplicationBuilder`:</span></span>

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

<span data-ttu-id="b0dcb-383">`http://localhost:5000`에 대한 브라우저에서 요청을 수행하여 “Hello World!” 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-383">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="b0dcb-384">`WaitForShutdown`은 중단(Ctrl-C/SIGINT 또는 SIGTERM)이 발생할 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-384">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="b0dcb-385">앱은 `Console.WriteLine` 메시지를 표시하고 keypress가 종료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-385">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="b0dcb-386">**StartWith(string url, Action&lt;IApplicationBuilder&gt; app)**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-386">**StartWith(string url, Action&lt;IApplicationBuilder&gt; app)**</span></span>

<span data-ttu-id="b0dcb-387">URL 및 대리자를 제공하여 `IApplicationBuilder`를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-387">Provide a URL and a delegate to configure an `IApplicationBuilder`:</span></span>

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

<span data-ttu-id="b0dcb-388">앱이 `http://localhost:8080`에서 응답한다는 점을 제외하고 **StartWith(Action&lt;IApplicationBuilder&gt; app)** 와 동일한 결과가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-388">Produces the same result as **StartWith(Action&lt;IApplicationBuilder&gt; app)**, except the app responds on `http://localhost:8080`.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b0dcb-389">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b0dcb-389">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b0dcb-390">**실행**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-390">**Run**</span></span>

<span data-ttu-id="b0dcb-391">`Run` 메서드는 웹앱을 시작하고 호스트가 종료될 때까지 호출 스레드를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-391">The `Run` method starts the web app and blocks the calling thread until the host is shut down:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="b0dcb-392">**Start**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-392">**Start**</span></span>

<span data-ttu-id="b0dcb-393">해당 `Start` 메서드를 호출하여 비차단 방식으로 호스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-393">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="b0dcb-394">URL 목록이 `Start` 메서드에 전달되면 지정된 URL에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-394">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>

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

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="b0dcb-395">IHostingEnvironment 인터페이스</span><span class="sxs-lookup"><span data-stu-id="b0dcb-395">IHostingEnvironment interface</span></span>

<span data-ttu-id="b0dcb-396">[IHostingEnvironment 인터페이스](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment)는 앱의 웹 호스팅 환경에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-396">The [IHostingEnvironment interface](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) provides information about the app's web hosting environment.</span></span> <span data-ttu-id="b0dcb-397">해당 속성 및 확장 메서드를 사용하기 위해 [생성자 주입](xref:fundamentals/dependency-injection)을 사용하여 `IHostingEnvironment`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-397">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

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

<span data-ttu-id="b0dcb-398">[규칙 기반 접근 방식](xref:fundamentals/environments#environment-based-startup-class-and-methods)은 시작할 때 환경에 따라 앱을 구성하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-398">A [convention-based approach](xref:fundamentals/environments#environment-based-startup-class-and-methods) can be used to configure the app at startup based on the environment.</span></span> <span data-ttu-id="b0dcb-399">또는 `ConfigureServices`에서 사용할 수 있도록 `IHostingEnvironment`를 `Startup` 생성자에 주입합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-399">Alternatively, inject the `IHostingEnvironment` into the `Startup` constructor for use in `ConfigureServices`:</span></span>

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
> <span data-ttu-id="b0dcb-400">`IsDevelopment` 확장 메서드 외에 `IHostingEnvironment`는 `IsStaging`, `IsProduction` 및 `IsEnvironment(string environmentName)` 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-400">In addition to the `IsDevelopment` extension method, `IHostingEnvironment` offers `IsStaging`, `IsProduction`, and `IsEnvironment(string environmentName)` methods.</span></span> <span data-ttu-id="b0dcb-401">자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-401">See [Use multiple environments](xref:fundamentals/environments) for details.</span></span>

<span data-ttu-id="b0dcb-402">또한 `IHostingEnvironment` 서비스를 파이프라인 처리를 설정하기 위한 `Configure` 메서드에 직접 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-402">The `IHostingEnvironment` service can also be injected directly into the `Configure` method for setting up the processing pipeline:</span></span>

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

<span data-ttu-id="b0dcb-403">사용자 지정 [미들웨어](xref:fundamentals/middleware/index#writing-middleware)를 만들 때 `IHostingEnvironment`를 `Invoke` 메서드에 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-403">`IHostingEnvironment` can be injected into the `Invoke` method when creating custom [middleware](xref:fundamentals/middleware/index#writing-middleware):</span></span>

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

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="b0dcb-404">IApplicationLifetime 인터페이스</span><span class="sxs-lookup"><span data-stu-id="b0dcb-404">IApplicationLifetime interface</span></span>

<span data-ttu-id="b0dcb-405">[IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime)은 사후 시작 및 종료 작업을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-405">[IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) allows for post-startup and shutdown activities.</span></span> <span data-ttu-id="b0dcb-406">인터페이스에서 세 가지 속성은 취소 토큰으로, 시작 및 종료 이벤트를 정의하는 `Action` 메서드를 등록하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-406">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span>

| <span data-ttu-id="b0dcb-407">취소 토큰</span><span class="sxs-lookup"><span data-stu-id="b0dcb-407">Cancellation Token</span></span>    | <span data-ttu-id="b0dcb-408">트리거되는 경우:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-408">Triggered when&#8230;</span></span> |
| --------------------- | --------------------- |
| [<span data-ttu-id="b0dcb-409">ApplicationStarted</span><span class="sxs-lookup"><span data-stu-id="b0dcb-409">ApplicationStarted</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstarted) | <span data-ttu-id="b0dcb-410">호스트가 완벽하게 시작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-410">The host has fully started.</span></span> |
| [<span data-ttu-id="b0dcb-411">ApplicationStopped</span><span class="sxs-lookup"><span data-stu-id="b0dcb-411">ApplicationStopped</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopped) | <span data-ttu-id="b0dcb-412">호스트가 정상적으로 종료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-412">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="b0dcb-413">모든 요청이 처리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-413">All requests should be processed.</span></span> <span data-ttu-id="b0dcb-414">종료는 이 이벤트가 완료될 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-414">Shutdown blocks until this event completes.</span></span> |
| [<span data-ttu-id="b0dcb-415">ApplicationStopping</span><span class="sxs-lookup"><span data-stu-id="b0dcb-415">ApplicationStopping</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopping) | <span data-ttu-id="b0dcb-416">호스트가 정상적으로 종료되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-416">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="b0dcb-417">요청은 계속 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-417">Requests may still be processing.</span></span> <span data-ttu-id="b0dcb-418">종료는 이 이벤트가 완료될 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-418">Shutdown blocks until this event completes.</span></span> |

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

<span data-ttu-id="b0dcb-419">[StopApplication](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.stopapplication)은 앱의 종료를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-419">[StopApplication](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.stopapplication) requests termination of the app.</span></span> <span data-ttu-id="b0dcb-420">다음 클래스에서는 `StopApplication`을 사용하여 해당 클래스의 `Shutdown` 메서드를 호출하는 경우 앱을 정상 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-420">The following class uses `StopApplication` to gracefully shut down an app when the class's `Shutdown` method is called:</span></span>

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

## <a name="scope-validation"></a><span data-ttu-id="b0dcb-421">범위 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="b0dcb-421">Scope validation</span></span>

<span data-ttu-id="b0dcb-422">ASP.NET Core 2.0 이상에서 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)은 앱의 환경이 개발인 경우 [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes)를 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-422">In ASP.NET Core 2.0 or later, [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) sets [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) to `true` if the app's environment is Development.</span></span>

<span data-ttu-id="b0dcb-423">`ValidateScopes`이 `true`로 설정된 경우 기본 서비스 공급자는 다음을 확인하기 위해 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-423">When `ValidateScopes` is set to `true`, the default service provider performs checks to verify that:</span></span>

* <span data-ttu-id="b0dcb-424">범위가 지정된 서비스는 직접 또는 간접적으로 루트 서비스 공급자에서 해결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-424">Scoped services aren't directly or indirectly resolved from the root service provider.</span></span>
* <span data-ttu-id="b0dcb-425">범위가 지정된 서비스는 직접 또는 간접적으로 싱글톤에 삽입되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-425">Scoped services aren't directly or indirectly injected into singletons.</span></span>

<span data-ttu-id="b0dcb-426">루트 서비스 공급자는 [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider)를 호출할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-426">The root service provider is created when [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider) is called.</span></span> <span data-ttu-id="b0dcb-427">루트 서비스 공급자의 수명은 공급자가 앱과 함께 시작되고 앱이 종료될 때 삭제되는 앱/서버의 수명에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-427">The root service provider's lifetime corresponds to the app/server's lifetime when the provider starts with the app and is disposed when the app shuts down.</span></span>

<span data-ttu-id="b0dcb-428">범위가 지정된 서비스는 서비스를 만든 컨테이너에 의해 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-428">Scoped services are disposed by the container that created them.</span></span> <span data-ttu-id="b0dcb-429">범위가 지정된 서비스가 루트 컨테이너에서 만들어지는 경우 서비스의 수명은 효과적으로 싱글톤으로 승격됩니다. 해당 서비스는 앱/서버가 종료될 때 루트 컨테이너에 의해서만 삭제되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-429">If a scoped service is created in the root container, the service's lifetime is effectively promoted to singleton because it's only disposed by the root container when app/server is shut down.</span></span> <span data-ttu-id="b0dcb-430">서비스 범위의 유효성 검사는 `BuildServiceProvider`이 호출될 경우 이러한 상황을 catch합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-430">Validating service scopes catches these situations when `BuildServiceProvider` is called.</span></span>

<span data-ttu-id="b0dcb-431">프로덕션 환경을 포함하여 범위의 유효성을 검사하려면 호스트 작성기에서 [ServiceProviderOptions](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions)을 [UseDefaultServiceProvider](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usedefaultserviceprovider)로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-431">To always validate scopes, including in the Production environment, configure the [ServiceProviderOptions](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions) with [UseDefaultServiceProvider](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usedefaultserviceprovider) on the host builder:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseDefaultServiceProvider((context, options) => {
        options.ValidateScopes = true;
    })
```

## <a name="troubleshooting-systemargumentexception"></a><span data-ttu-id="b0dcb-432">System.ArgumentException 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b0dcb-432">Troubleshooting System.ArgumentException</span></span>

<span data-ttu-id="b0dcb-433">**ASP.NET Core 2.0에만 적용**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-433">**Applies to ASP.NET Core 2.0 Only**</span></span>

<span data-ttu-id="b0dcb-434">호스트는 `UseStartup` 또는 `Configure`를 호출하는 대신 종속성 주입 컨테이너에 `IStartup`을 직접 주입하여 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-434">A host may be built by injecting `IStartup` directly into the dependency injection container rather than calling `UseStartup` or `Configure`:</span></span>

```csharp
services.AddSingleton<IStartup, Startup>();
```

<span data-ttu-id="b0dcb-435">호스트가 이러한 방식으로 빌드되면 다음과 같은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-435">If the host is built this way, the following error may occur:</span></span>

```
Unhandled Exception: System.ArgumentException: A valid non-empty application name must be provided.
```

<span data-ttu-id="b0dcb-436">이는 `HostingStartupAttributes`를 검색하는 데 [applicationName(ApplicationKey)](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey)(현재 어셈블리)이 필요하기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-436">This occurs because the [applicationName(ApplicationKey)](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey) (the current assembly) is required to scan for `HostingStartupAttributes`.</span></span> <span data-ttu-id="b0dcb-437">앱이 `IStartup`을 종속성 주입 컨테이너에 수동으로 주입하는 경우 다음 호출을 지정된 어셈블리 이름으로 `WebHostBuilder`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-437">If the app manually injects `IStartup` into the dependency injection container, add the following call to `WebHostBuilder` with the assembly name specified:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("applicationName", "<Assembly Name>")
    ...
```

<span data-ttu-id="b0dcb-438">또는 dummy `Configure`를 `WebHostBuilder`에 추가합니다. 이는 `applicationName`(`ApplicationKey`)을 자동으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-438">Alternatively, add a dummy `Configure` to the `WebHostBuilder`, which sets the `applicationName`(`ApplicationKey`) automatically:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .Configure(_ => { })
    ...
```

<span data-ttu-id="b0dcb-439">**참고**: 이는 ASP.NET Core 2.0 릴리스와 `UseStartup` 또는 `Configure`를 호출하지 않는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-439">**NOTE**: This is only required with the ASP.NET Core 2.0 release and only when the app doesn't call `UseStartup` or `Configure`.</span></span>

<span data-ttu-id="b0dcb-440">자세한 내용은 [알림: Microsoft.Extensions.PlatformAbstractions가 제거되었습니다(주석)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) 및 [StartupInjection 샘플](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-440">For more information, see [Announcements: Microsoft.Extensions.PlatformAbstractions has been removed (comment)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) and the [StartupInjection sample](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0dcb-441">추가 자료</span><span class="sxs-lookup"><span data-stu-id="b0dcb-441">Additional resources</span></span>

* [<span data-ttu-id="b0dcb-442">IIS를 사용하여 Windows에서 호스트</span><span class="sxs-lookup"><span data-stu-id="b0dcb-442">Host on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="b0dcb-443">Nginx를 사용하여 Linux에서 호스트</span><span class="sxs-lookup"><span data-stu-id="b0dcb-443">Host on Linux with Nginx</span></span>](xref:host-and-deploy/linux-nginx)
* [<span data-ttu-id="b0dcb-444">Apache를 사용하여 Linux에서 호스트</span><span class="sxs-lookup"><span data-stu-id="b0dcb-444">Host on Linux with Apache</span></span>](xref:host-and-deploy/linux-apache)
* [<span data-ttu-id="b0dcb-445">Windows 서비스에서 호스트</span><span class="sxs-lookup"><span data-stu-id="b0dcb-445">Host in a Windows Service</span></span>](xref:host-and-deploy/windows-service)
