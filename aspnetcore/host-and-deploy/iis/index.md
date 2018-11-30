---
title: IIS가 있는 Windows에서 ASP.NET Core 호스팅
author: guardrex
description: Windows Server IIS(인터넷 정보 서비스)에서 ASP.NET Core 앱을 호스팅하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 11/26/2018
uid: host-and-deploy/iis/index
ms.openlocfilehash: 77fa6e1ef6a7fc707c2665826d3c1f4c2691979c
ms.sourcegitcommit: e9b99854b0a8021dafabee0db5e1338067f250a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52450803"
---
# <a name="host-aspnet-core-on-windows-with-iis"></a><span data-ttu-id="e6cc9-103">IIS가 있는 Windows에서 ASP.NET Core 호스팅</span><span class="sxs-lookup"><span data-stu-id="e6cc9-103">Host ASP.NET Core on Windows with IIS</span></span>

<span data-ttu-id="e6cc9-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="e6cc9-104">By [Luke Latham](https://github.com/guardrex)</span></span>

[<span data-ttu-id="e6cc9-105">.NET Core 호스팅 번들 설치</span><span class="sxs-lookup"><span data-stu-id="e6cc9-105">Install the .NET Core Hosting Bundle</span></span>](#install-the-net-core-hosting-bundle)

> [!NOTE]
> <span data-ttu-id="e6cc9-106">ASP.NET Core 목차에 대해 제안된 새 구조의 유용성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-106">We’re testing the usability of a proposed new structure for the ASP.NET Core table of contents.</span></span>  <span data-ttu-id="e6cc9-107">몇 분 동안 현재 또는 제안된 목차에서 다른 7개의 항목을 찾는 연습을 수행하는 경우 [여기를 클릭하여 연구에 참여하세요](https://dpk4xbh5.optimalworkshop.com/treejack/rps16hd5).</span><span class="sxs-lookup"><span data-stu-id="e6cc9-107">If you have a few minutes to try an exercise of finding 7 different topics in the current or proposed table of contents, please [click here to participate in the study](https://dpk4xbh5.optimalworkshop.com/treejack/rps16hd5).</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="e6cc9-108">지원되는 운영 체제</span><span class="sxs-lookup"><span data-stu-id="e6cc9-108">Supported operating systems</span></span>

<span data-ttu-id="e6cc9-109">지원되는 운영 체제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-109">The following operating systems are supported:</span></span>

* <span data-ttu-id="e6cc9-110">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="e6cc9-110">Windows 7 or later</span></span>
* <span data-ttu-id="e6cc9-111">Windows Server 2008 R2 이상</span><span class="sxs-lookup"><span data-stu-id="e6cc9-111">Windows Server 2008 R2 or later</span></span>

<span data-ttu-id="e6cc9-112">[HTTP.sys 서버](xref:fundamentals/servers/httpsys)(이전의 [WebListener](xref:fundamentals/servers/weblistener))는 IIS를 사용하는 역방향 프록시 구성에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-112">[HTTP.sys server](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)) doesn't work in a reverse proxy configuration with IIS.</span></span> <span data-ttu-id="e6cc9-113">[Kestrel 서버](xref:fundamentals/servers/kestrel)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-113">Use the [Kestrel server](xref:fundamentals/servers/kestrel).</span></span>

<span data-ttu-id="e6cc9-114">Azure에서 호스트하는 방법에 대한 자세한 내용은 <xref:host-and-deploy/azure-apps/index>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-114">For information on hosting in Azure, see <xref:host-and-deploy/azure-apps/index>.</span></span>

## <a name="application-configuration"></a><span data-ttu-id="e6cc9-115">응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="e6cc9-115">Application configuration</span></span>

### <a name="enable-the-iisintegration-components"></a><span data-ttu-id="e6cc9-116">IISIntegration 구성 요소 사용</span><span class="sxs-lookup"><span data-stu-id="e6cc9-116">Enable the IISIntegration components</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="e6cc9-117">일반적인 *Program.cs*는 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>를 호출하여 호스트 설정을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-117">A typical *Program.cs* calls <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> to begin setting up a host:</span></span>

```csharp
public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        ...
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="e6cc9-118">일반적인 *Program.cs*는 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>를 호출하여 호스트 설정을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-118">A typical *Program.cs* calls <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> to begin setting up a host:</span></span>

```csharp
public static IWebHost BuildWebHost(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        ...
```

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="e6cc9-119">**In-process 호스팅 모델**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-119">**In-process hosting model**</span></span>

<span data-ttu-id="e6cc9-120">`CreateDefaultBuilder`는 `UseIIS` 메서드를 호출하여 [CoreCLR](/dotnet/standard/glossary#coreclr)을 부팅하고 IIS 작업자 프로세스(*w3wp.exe* 또는 *iisexpress.exe*) 내에서 앱을 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-120">`CreateDefaultBuilder` calls the `UseIIS` method to boot the [CoreCLR](/dotnet/standard/glossary#coreclr) and host the app inside of the IIS worker process (*w3wp.exe* or *iisexpress.exe*).</span></span> <span data-ttu-id="e6cc9-121">성능 테스트의 결과 .NET Core 앱 In-process를 호스팅하는 것이 앱 out-of-process 및 [Kestrel](xref:fundamentals/servers/kestrel)에 대한 요청을 프록시하는 것보다 훨씬 높은 요청 처리량을 제공함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-121">Performance tests indicate that hosting a .NET Core app in-process delivers significantly higher request throughput compared to hosting the app out-of-process and proxying requests to [Kestrel](xref:fundamentals/servers/kestrel).</span></span>

<span data-ttu-id="e6cc9-122">**Out-of-process 호스팅 모델**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-122">**Out-of-process hosting model**</span></span>

<span data-ttu-id="e6cc9-123">IIS가 있는 out-of-process 호스팅의 경우 `CreateDefaultBuilder`는 [Kestrel](xref:fundamentals/servers/kestrel)을 웹 서버로 구성하고 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)의 기본 경로 및 포트를 구성하여 IIS 통합을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-123">For out-of-process hosting with IIS, `CreateDefaultBuilder` configures [Kestrel](xref:fundamentals/servers/kestrel) as the web server and enables IIS integration by configuring the base path and port for the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span>

<span data-ttu-id="e6cc9-124">ASP.NET Core 모듈은 동적 포트를 생성하여 백 엔드 프로세스에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-124">The ASP.NET Core Module generates a dynamic port to assign to the backend process.</span></span> <span data-ttu-id="e6cc9-125">`CreateDefaultBuilder`는 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-125">`CreateDefaultBuilder` calls the <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> method.</span></span> <span data-ttu-id="e6cc9-126">`UseIISIntegration`은 localhost IP 주소(`127.0.0.1`)의 동적 포트에서 수신 대기하도록 Kestrel을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-126">`UseIISIntegration` configures Kestrel to listen on the dynamic port at the localhost IP address (`127.0.0.1`).</span></span> <span data-ttu-id="e6cc9-127">동적 포트가 1234인 경우 Kestrel은 `127.0.0.1:1234`에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-127">If the dynamic port is 1234, Kestrel listens at `127.0.0.1:1234`.</span></span> <span data-ttu-id="e6cc9-128">이 구성은 다음에서 제공된 다른 URL 구성을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-128">This configuration replaces other URL configurations provided by:</span></span>

* `UseUrls`
* [<span data-ttu-id="e6cc9-129">Kestrel의 수신 대기 API</span><span class="sxs-lookup"><span data-stu-id="e6cc9-129">Kestrel's Listen API</span></span>](xref:fundamentals/servers/kestrel#endpoint-configuration)
* <span data-ttu-id="e6cc9-130">[구성](xref:fundamentals/configuration/index)(또는 [명령줄 --urls 옵션](xref:fundamentals/host/web-host#override-configuration))</span><span class="sxs-lookup"><span data-stu-id="e6cc9-130">[Configuration](xref:fundamentals/configuration/index) (or [command-line --urls option](xref:fundamentals/host/web-host#override-configuration))</span></span>

<span data-ttu-id="e6cc9-131">모듈을 사용하는 경우 `UseUrls` 호출 또는 Kestrel의 `Listen` API가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-131">Calls to `UseUrls` or Kestrel's `Listen` API aren't required when using the module.</span></span> <span data-ttu-id="e6cc9-132">`UseUrls` 또는 `Listen`을 호출하는 경우 Kestrel은 IIS 없이 앱을 실행할 때만 지정된 포트에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-132">If `UseUrls` or `Listen` is called, Kestrel listens on the ports specified only when running the app without IIS.</span></span>

<span data-ttu-id="e6cc9-133">In-process 및 out-of-process 호스팅 모델에 대한 자세한 내용은 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module) 및 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-133">For more information on the in-process and out-of-process hosting models, see [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.1"

<span data-ttu-id="e6cc9-134">`CreateDefaultBuilder`는 [Kestrel](xref:fundamentals/servers/kestrel)을 웹 서버로 구성하고 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)의 기본 경로 및 포트를 구성하여 IIS 통합을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-134">`CreateDefaultBuilder` configures [Kestrel](xref:fundamentals/servers/kestrel) as the web server and enables IIS integration by configuring the base path and port for the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span>

<span data-ttu-id="e6cc9-135">ASP.NET Core 모듈은 동적 포트를 생성하여 백 엔드 프로세스에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-135">The ASP.NET Core Module generates a dynamic port to assign to the backend process.</span></span> <span data-ttu-id="e6cc9-136">`CreateDefaultBuilder`는 [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-136">`CreateDefaultBuilder` calls the [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) method.</span></span> <span data-ttu-id="e6cc9-137">`UseIISIntegration`은 localhost IP 주소(`127.0.0.1`)의 동적 포트에서 수신 대기하도록 Kestrel을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-137">`UseIISIntegration` configures Kestrel to listen on the dynamic port at the localhost IP address (`127.0.0.1`).</span></span> <span data-ttu-id="e6cc9-138">동적 포트가 1234인 경우 Kestrel은 `127.0.0.1:1234`에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-138">If the dynamic port is 1234, Kestrel listens at `127.0.0.1:1234`.</span></span> <span data-ttu-id="e6cc9-139">이 구성은 다음에서 제공된 다른 URL 구성을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-139">This configuration replaces other URL configurations provided by:</span></span>

* `UseUrls`
* [<span data-ttu-id="e6cc9-140">Kestrel의 수신 대기 API</span><span class="sxs-lookup"><span data-stu-id="e6cc9-140">Kestrel's Listen API</span></span>](xref:fundamentals/servers/kestrel#endpoint-configuration)
* <span data-ttu-id="e6cc9-141">[구성](xref:fundamentals/configuration/index)(또는 [명령줄 --urls 옵션](xref:fundamentals/host/web-host#override-configuration))</span><span class="sxs-lookup"><span data-stu-id="e6cc9-141">[Configuration](xref:fundamentals/configuration/index) (or [command-line --urls option](xref:fundamentals/host/web-host#override-configuration))</span></span>

<span data-ttu-id="e6cc9-142">모듈을 사용하는 경우 `UseUrls` 호출 또는 Kestrel의 `Listen` API가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-142">Calls to `UseUrls` or Kestrel's `Listen` API aren't required when using the module.</span></span> <span data-ttu-id="e6cc9-143">`UseUrls` 또는 `Listen`을 호출하는 경우 Kestrel은 IIS 없이 앱을 실행할 때만 지정된 포트에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-143">If `UseUrls` or `Listen` is called, Kestrel listens on the port specified only when running the app without IIS.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="e6cc9-144">`CreateDefaultBuilder`는 [Kestrel](xref:fundamentals/servers/kestrel)을 웹 서버로 구성하고 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)의 기본 경로 및 포트를 구성하여 IIS 통합을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-144">`CreateDefaultBuilder` configures [Kestrel](xref:fundamentals/servers/kestrel) as the web server and enables IIS integration by configuring the base path and port for the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span>

<span data-ttu-id="e6cc9-145">ASP.NET Core 모듈은 동적 포트를 생성하여 백 엔드 프로세스에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-145">The ASP.NET Core Module generates a dynamic port to assign to the backend process.</span></span> <span data-ttu-id="e6cc9-146">`CreateDefaultBuilder`는 [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-146">`CreateDefaultBuilder` calls the [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) method.</span></span> <span data-ttu-id="e6cc9-147">`UseIISIntegration`은 localhost IP 주소(`localhost`)의 동적 포트에서 수신 대기하도록 Kestrel을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-147">`UseIISIntegration` configures Kestrel to listen on the dynamic port at the localhost IP address (`localhost`).</span></span> <span data-ttu-id="e6cc9-148">동적 포트가 1234인 경우 Kestrel은 `localhost:1234`에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-148">If the dynamic port is 1234, Kestrel listens at `localhost:1234`.</span></span> <span data-ttu-id="e6cc9-149">이 구성은 다음에서 제공된 다른 URL 구성을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-149">This configuration replaces other URL configurations provided by:</span></span>

* `UseUrls`
* [<span data-ttu-id="e6cc9-150">Kestrel의 수신 대기 API</span><span class="sxs-lookup"><span data-stu-id="e6cc9-150">Kestrel's Listen API</span></span>](xref:fundamentals/servers/kestrel#endpoint-configuration)
* <span data-ttu-id="e6cc9-151">[구성](xref:fundamentals/configuration/index)(또는 [명령줄 --urls 옵션](xref:fundamentals/host/web-host#override-configuration))</span><span class="sxs-lookup"><span data-stu-id="e6cc9-151">[Configuration](xref:fundamentals/configuration/index) (or [command-line --urls option](xref:fundamentals/host/web-host#override-configuration))</span></span>

<span data-ttu-id="e6cc9-152">모듈을 사용하는 경우 `UseUrls` 호출 또는 Kestrel의 `Listen` API가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-152">Calls to `UseUrls` or Kestrel's `Listen` API aren't required when using the module.</span></span> <span data-ttu-id="e6cc9-153">`UseUrls` 또는 `Listen`을 호출하는 경우 Kestrel은 IIS 없이 앱을 실행할 때만 지정된 포트에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-153">If `UseUrls` or `Listen` is called, Kestrel listens on the port specified only when running the app without IIS.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e6cc9-154">[Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) 패키지에 대한 종속성을 앱의 종속성에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-154">Include a dependency on the [Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) package in the app's dependencies.</span></span> <span data-ttu-id="e6cc9-155">[UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) 확장 메서드를 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)에 추가하여 IIS 통합 미들웨어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-155">Use IIS Integration middleware by adding the [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) extension method to [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder):</span></span>

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .UseIISIntegration()
    ...
```

<span data-ttu-id="e6cc9-156">[UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) 및 [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration)이 둘 다 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-156">Both [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) and [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) are required.</span></span> <span data-ttu-id="e6cc9-157">`UseIISIntegration`을 호출하는 코드는 코드 이식성에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-157">Code calling `UseIISIntegration` doesn't affect code portability.</span></span> <span data-ttu-id="e6cc9-158">앱이 IIS 배후에서 실행되지 않는 경우(예를 들어 앱이 Kestrel에서 바로 실행되는 경우)에는 `UseIISIntegration`이 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-158">If the app isn't run behind IIS (for example, the app is run directly on Kestrel), `UseIISIntegration` doesn't operate.</span></span>

<span data-ttu-id="e6cc9-159">ASP.NET Core 모듈은 동적 포트를 생성하여 백 엔드 프로세스에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-159">The ASP.NET Core Module generates a dynamic port to assign to the backend process.</span></span> <span data-ttu-id="e6cc9-160">`UseIISIntegration`은 localhost IP 주소(`localhost`)의 동적 포트에서 수신 대기하도록 Kestrel을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-160">`UseIISIntegration` configures Kestrel to listen on the dynamic port at the localhost IP address (`localhost`).</span></span> <span data-ttu-id="e6cc9-161">동적 포트가 1234인 경우 Kestrel은 `localhost:1234`에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-161">If the dynamic port is 1234, Kestrel listens at `localhost:1234`.</span></span> <span data-ttu-id="e6cc9-162">이 구성은 다음에서 제공된 다른 URL 구성을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-162">This configuration replaces other URL configurations provided by:</span></span>

* `UseUrls`
* <span data-ttu-id="e6cc9-163">[구성](xref:fundamentals/configuration/index)(또는 [명령줄 --urls 옵션](xref:fundamentals/host/web-host#override-configuration))</span><span class="sxs-lookup"><span data-stu-id="e6cc9-163">[Configuration](xref:fundamentals/configuration/index) (or [command-line --urls option](xref:fundamentals/host/web-host#override-configuration))</span></span>

<span data-ttu-id="e6cc9-164">모듈을 사용하는 경우 `UseUrls` 호출이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-164">A call to `UseUrls` isn't required when using the module.</span></span> <span data-ttu-id="e6cc9-165">`UseUrls`를 호출하는 경우 Kestrel은 IIS 없이 앱을 실행할 때만 지정된 포트에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-165">If `UseUrls` is called, Kestrel listens on the port specified only when running the app without IIS.</span></span>

<span data-ttu-id="e6cc9-166">`UseUrls`를 ASP.NET Core 1.0 앱에서 호출하는 경우 모듈 구성 포트를 덮어 쓰지 않도록 `UseIISIntegration`을 호출하기 **전에** 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-166">If `UseUrls` is called in an ASP.NET Core 1.0 app, call it **before** calling `UseIISIntegration` so that the module-configured port isn't overwritten.</span></span> <span data-ttu-id="e6cc9-167">모듈 설정이 `UseUrls`를 재정의하기 때문에 이 호출 순서는 ASP.NET Core 1.1에서 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-167">This calling order isn't required with ASP.NET Core 1.1 because the module setting overrides `UseUrls`.</span></span>

::: moniker-end

<span data-ttu-id="e6cc9-168">호스팅에 대한 자세한 내용은 [ASP.NET Core의 호스트](xref:fundamentals/host/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-168">For more information on hosting, see [Host in ASP.NET Core](xref:fundamentals/host/index).</span></span>

### <a name="iis-options"></a><span data-ttu-id="e6cc9-169">IIS 옵션</span><span class="sxs-lookup"><span data-stu-id="e6cc9-169">IIS options</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="e6cc9-170">**In-process 호스팅 모델**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-170">**In-process hosting model**</span></span>

<span data-ttu-id="e6cc9-171">IIS 서버 옵션을 구성하려면 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices)에 [IISServerOptions](/dotnet/api/microsoft.aspnetcore.builder.iisserveroptions)에 대한 서비스 구성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-171">To configure IIS Server options, include a service configuration for [IISServerOptions](/dotnet/api/microsoft.aspnetcore.builder.iisserveroptions) in [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices).</span></span> <span data-ttu-id="e6cc9-172">다음 예제에서는 AutomaticAuthentication을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-172">The following example disables AutomaticAuthentication:</span></span>

```csharp
services.Configure<IISServerOptions>(options => 
{
    options.AutomaticAuthentication = false;
});
```

| <span data-ttu-id="e6cc9-173">옵션</span><span class="sxs-lookup"><span data-stu-id="e6cc9-173">Option</span></span>                         | <span data-ttu-id="e6cc9-174">기본</span><span class="sxs-lookup"><span data-stu-id="e6cc9-174">Default</span></span> | <span data-ttu-id="e6cc9-175">설정</span><span class="sxs-lookup"><span data-stu-id="e6cc9-175">Setting</span></span> |
| ------------------------------ | :-----: | ------- |
| `AutomaticAuthentication`      | `true`  | <span data-ttu-id="e6cc9-176">`true`인 경우 IIS 서버는 [Windows 인증](xref:security/authentication/windowsauth)에 의해 인증된 `HttpContext.User`를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-176">If `true`, IIS Server sets the `HttpContext.User` authenticated by [Windows Authentication](xref:security/authentication/windowsauth).</span></span> <span data-ttu-id="e6cc9-177">`false`인 경우 서버는 `HttpContext.User`에 대한 ID만 제공하고, `AuthenticationScheme`에서 명시적으로 요청될 때 챌린지에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-177">If `false`, the server only provides an identity for `HttpContext.User` and responds to challenges when explicitly requested by the `AuthenticationScheme`.</span></span> <span data-ttu-id="e6cc9-178">IIS에서 Windows 인증은 `AutomaticAuthentication`이 작동하기 위해 사용하도록 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-178">Windows Authentication must be enabled in IIS for `AutomaticAuthentication` to function.</span></span> <span data-ttu-id="e6cc9-179">자세한 내용은 [Windows 인증](xref:security/authentication/windowsauth)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-179">For more information, see [Windows Authentication](xref:security/authentication/windowsauth).</span></span> |
| `AuthenticationDisplayName`    | `null`  | <span data-ttu-id="e6cc9-180">로그인 페이지에서 사용자에게 나타나는 표시 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-180">Sets the display name shown to users on login pages.</span></span> |

<span data-ttu-id="e6cc9-181">**Out-of-process 호스팅 모델**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-181">**Out-of-process hosting model**</span></span>

::: moniker-end

<span data-ttu-id="e6cc9-182">IIS 옵션을 구성하려면 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices)에 [IISOptions](/dotnet/api/microsoft.aspnetcore.builder.iisoptions)에 대한 서비스 구성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-182">To configure IIS options, include a service configuration for [IISOptions](/dotnet/api/microsoft.aspnetcore.builder.iisoptions) in [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices).</span></span> <span data-ttu-id="e6cc9-183">다음 예에서는 앱이 `HttpContext.Connection.ClientCertificate`를 채우는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-183">The following example prevents the app from populating `HttpContext.Connection.ClientCertificate`:</span></span>

```csharp
services.Configure<IISOptions>(options => 
{
    options.ForwardClientCertificate = false;
});
```

| <span data-ttu-id="e6cc9-184">옵션</span><span class="sxs-lookup"><span data-stu-id="e6cc9-184">Option</span></span>                         | <span data-ttu-id="e6cc9-185">기본</span><span class="sxs-lookup"><span data-stu-id="e6cc9-185">Default</span></span> | <span data-ttu-id="e6cc9-186">설정</span><span class="sxs-lookup"><span data-stu-id="e6cc9-186">Setting</span></span> |
| ------------------------------ | :-----: | ------- |
| `AutomaticAuthentication`      | `true`  | <span data-ttu-id="e6cc9-187">`true`이면 IIS 통합 미들웨어가 [Windows 인증](xref:security/authentication/windowsauth)에 의해 인증된 `HttpContext.User`를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-187">If `true`, IIS Integration Middleware sets the `HttpContext.User` authenticated by [Windows Authentication](xref:security/authentication/windowsauth).</span></span> <span data-ttu-id="e6cc9-188">`false`이면 미들웨어가 `HttpContext.User`에게 ID만 제공하고, `AuthenticationScheme`에서 명시적으로 요청될 때 챌린지에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-188">If `false`, the middleware only provides an identity for `HttpContext.User` and responds to challenges when explicitly requested by the `AuthenticationScheme`.</span></span> <span data-ttu-id="e6cc9-189">IIS에서 Windows 인증은 `AutomaticAuthentication`이 작동하기 위해 사용하도록 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-189">Windows Authentication must be enabled in IIS for `AutomaticAuthentication` to function.</span></span> <span data-ttu-id="e6cc9-190">자세한 내용은 [Windows 인증](xref:security/authentication/windowsauth) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-190">For more information, see the [Windows Authentication](xref:security/authentication/windowsauth) topic.</span></span> |
| `AuthenticationDisplayName`    | `null`  | <span data-ttu-id="e6cc9-191">로그인 페이지에서 사용자에게 나타나는 표시 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-191">Sets the display name shown to users on login pages.</span></span> |
| `ForwardClientCertificate`     | `true`  | <span data-ttu-id="e6cc9-192">`true`면서 `MS-ASPNETCORE-CLIENTCERT` 요청 헤더가 있는 경우 `HttpContext.Connection.ClientCertificate`가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-192">If `true` and the `MS-ASPNETCORE-CLIENTCERT` request header is present, the `HttpContext.Connection.ClientCertificate` is populated.</span></span> |

### <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="e6cc9-193">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="e6cc9-193">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="e6cc9-194">체계(HTTP/HTTPS) 및 요청이 시작된 원격 IP 주소를 전달하도록 전달된 헤더 미들웨어를 구성하는 IIS 통합 미들웨어 및 ASP.NET Core 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-194">The IIS Integration Middleware, which configures Forwarded Headers Middleware, and the ASP.NET Core Module are configured to forward the scheme (HTTP/HTTPS) and the remote IP address where the request originated.</span></span> <span data-ttu-id="e6cc9-195">추가 프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-195">Additional configuration might be required for apps hosted behind additional proxy servers and load balancers.</span></span> <span data-ttu-id="e6cc9-196">자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-196">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

### <a name="webconfig-file"></a><span data-ttu-id="e6cc9-197">web.config 파일</span><span class="sxs-lookup"><span data-stu-id="e6cc9-197">web.config file</span></span>

<span data-ttu-id="e6cc9-198">*web.config* 파일은 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-198">The *web.config* file configures the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="e6cc9-199">*web.config* 파일을 만들고, 변하고, 게시하는 작업은 프로젝트를 게시할 때 MSBuild 대상(`_TransformWebConfig`)에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-199">Creating, transforming, and publishing the *web.config* file is handled by an MSBuild target (`_TransformWebConfig`) when the project is published.</span></span> <span data-ttu-id="e6cc9-200">이 대상은 웹 SDK 대상(`Microsoft.NET.Sdk.Web`)에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-200">This target is present in the Web SDK targets (`Microsoft.NET.Sdk.Web`).</span></span> <span data-ttu-id="e6cc9-201">SDK는 프로젝트 파일을 기반으로 해서 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-201">The SDK is set at the top of the project file:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
```

<span data-ttu-id="e6cc9-202">프로젝트에 *web.config* 파일이 없는 경우, [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 구성하기 위해 올바른 *processPath* 및 *인수*로 파일이 생성되어 [게시된 출력](xref:host-and-deploy/directory-structure)으로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-202">If a *web.config* file isn't present in the project, the file is created with the correct *processPath* and *arguments* to configure the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and moved to [published output](xref:host-and-deploy/directory-structure).</span></span>

<span data-ttu-id="e6cc9-203">프로젝트에 *web.config* 파일이 있는 경우, ASP.NET Core 모듈을 구성하기 위해 올바른 *processPath* 및 *인수*로 파일이 변환되어 게시된 출력으로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-203">If a *web.config* file is present in the project, the file is transformed with the correct *processPath* and *arguments* to configure the ASP.NET Core Module and moved to published output.</span></span> <span data-ttu-id="e6cc9-204">변환은 이 파일의 IIS 구성 설정을 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-204">The transformation doesn't modify IIS configuration settings in the file.</span></span>

<span data-ttu-id="e6cc9-205">*web.config* 파일은 활성 IIS 모듈을 제어하는 추가 IIS 구성 설정을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-205">The *web.config* file may provide additional IIS configuration settings that control active IIS modules.</span></span> <span data-ttu-id="e6cc9-206">ASP.NET Core 앱을 사용하여 요청을 처리할 수 있는 IIS 모듈에 대한 자세한 내용은 [IIS 모듈](xref:host-and-deploy/iis/modules) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-206">For information on IIS modules that are capable of processing requests with ASP.NET Core apps, see the [IIS modules](xref:host-and-deploy/iis/modules) topic.</span></span>

<span data-ttu-id="e6cc9-207">웹 SDK가 *web.config* 파일을 변환하지 못하게 하려면 프로젝트 파일의 **\<IsTransformWebConfigDisabled>** 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-207">To prevent the Web SDK from transforming the *web.config* file, use the **\<IsTransformWebConfigDisabled>** property in the project file:</span></span>

```xml
<PropertyGroup>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

<span data-ttu-id="e6cc9-208">웹 SDK가 파일을 변환하지 않도록 설정하는 경우 개발자가 *processPath* 및 *인수*를 수동으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-208">When disabling the Web SDK from transforming the file, the *processPath* and *arguments* should be manually set by the developer.</span></span> <span data-ttu-id="e6cc9-209">자세한 내용은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-209">For more information, see the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

### <a name="webconfig-file-location"></a><span data-ttu-id="e6cc9-210">web.config 파일 위치</span><span class="sxs-lookup"><span data-stu-id="e6cc9-210">web.config file location</span></span>

<span data-ttu-id="e6cc9-211">[ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module)을 올바르게 설정하려면 배포된 앱의 콘텐츠 루트 경로(일반적으로 앱 기본 경로)에 *web.config* 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-211">In order to set up the [ASP.NET Core Module](xref:host-and-deploy/aspnet-core-module) correctly, the *web.config* file must be present at the content root path (typically the app base path) of the deployed app.</span></span> <span data-ttu-id="e6cc9-212">IIS에 제공되는 웹 사이트 실제 경로와 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-212">This is the same location as the website physical path provided to IIS.</span></span> <span data-ttu-id="e6cc9-213">웹 배포를 사용하여 여러 앱을 게시하도록 설정하려면 앱의 루트에 *web.config* 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-213">The *web.config* file is required at the root of the app to enable the publishing of multiple apps using Web Deploy.</span></span>

<span data-ttu-id="e6cc9-214">중요한 파일은 *\<assembly>.runtimeconfig.json*, *\<assembly>.xml*(XML 문서 주석) 및 *\<assembly>.deps.json*과 같은 앱의 실제 경로에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-214">Sensitive files exist on the app's physical path, such as *\<assembly>.runtimeconfig.json*, *\<assembly>.xml* (XML Documentation comments), and *\<assembly>.deps.json*.</span></span> <span data-ttu-id="e6cc9-215">*web.config* 파일이 있고 사이트가 정상적으로 시작되면 IIS는 이러한 중요한 파일이 요청되어도 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-215">When the *web.config* file is present and and the site starts normally, IIS doesn't serve these sensitive files if they're requested.</span></span> <span data-ttu-id="e6cc9-216">*web.config* 파일이 없거나, 이름이 잘못 지정되었거나, 정상적으로 시작되도록 사이트를 구성할 수 없는 경우 IIS에서 중요한 파일을 공개적으로 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-216">If the *web.config* file is missing, incorrectly named, or unable to configure the site for normal startup, IIS may serve sensitive files publicly.</span></span>

<span data-ttu-id="e6cc9-217">***web.config* 파일이 항상 배포에 있어야 하며, 올바르게 이름이 지정되고, 정상적으로 시작되도록 사이트를 구성할 수 있어야 합니다. 프로덕션 배포에서 *web.config* 파일을 제거하지 마세요.**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-217">**The *web.config* file must be present in the deployment at all times, correctly named, and able to configure the site for normal start up. Never remove the *web.config* file from a production deployment.**</span></span>

## <a name="iis-configuration"></a><span data-ttu-id="e6cc9-218">IIS 구성</span><span class="sxs-lookup"><span data-stu-id="e6cc9-218">IIS configuration</span></span>

<span data-ttu-id="e6cc9-219">**Windows Server 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-219">**Windows Server operating systems**</span></span>

<span data-ttu-id="e6cc9-220">**웹 서버(IIS)** 서버 역할을 사용하도록 설정하고 역할 서비스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-220">Enable the **Web Server (IIS)** server role and establish role services.</span></span>

1. <span data-ttu-id="e6cc9-221">**관리** 메뉴 또는 **서버 관리자**의 링크를 통해 **역할 및 기능 추가** 마법사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-221">Use the **Add Roles and Features** wizard from the **Manage** menu or the link in **Server Manager**.</span></span> <span data-ttu-id="e6cc9-222">**서버 역할** 단계에서 **웹 서버(IIS)** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-222">On the **Server Roles** step, check the box for **Web Server (IIS)**.</span></span>

   ![서버 역할 선택 단계에서 선택된 웹 서버 IIS 역할](index/_static/server-roles-ws2016.png)

1. <span data-ttu-id="e6cc9-224">**기능** 단계 후에는 웹 서버(IIS)에 대한 **역할 서비스** 단계가 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-224">After the **Features** step, the **Role services** step loads for Web Server (IIS).</span></span> <span data-ttu-id="e6cc9-225">원하는 IIS 역할 서비스를 선택하거나 제공된 기본 역할 서비스를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-225">Select the IIS role services desired or accept the default role services provided.</span></span>

   ![역할 서비스 선택 단계에서 선택된 기본 역할 서비스](index/_static/role-services-ws2016.png)

   <span data-ttu-id="e6cc9-227">**Windows 인증(선택 사항)**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-227">**Windows Authentication (Optional)**</span></span>  
   <span data-ttu-id="e6cc9-228">Windows 인증을 사용하도록 설정하려면 **웹 서버** > **보안** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-228">To enable Windows Authentication, expand the following nodes: **Web Server** > **Security**.</span></span> <span data-ttu-id="e6cc9-229">**Windows 인증** 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-229">Select the **Windows Authentication** feature.</span></span> <span data-ttu-id="e6cc9-230">자세한 내용은 [Windows 인증 \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) 및 [Windows 인증 구성](xref:security/authentication/windowsauth)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-230">For more information, see [Windows Authentication \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) and [Configure Windows authentication](xref:security/authentication/windowsauth).</span></span>

   <span data-ttu-id="e6cc9-231">**WebSockets(선택 사항)**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-231">**WebSockets (Optional)**</span></span>  
   <span data-ttu-id="e6cc9-232">WebSockets는 ASP.NET Core 1.1 이상에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-232">WebSockets is supported with ASP.NET Core 1.1 or later.</span></span> <span data-ttu-id="e6cc9-233">WebSockets를 사용하도록 설정하려면 **웹 서버** > **응용 프로그램 개발** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-233">To enable WebSockets, expand the following nodes: **Web Server** > **Application Development**.</span></span> <span data-ttu-id="e6cc9-234">**WebSocket 프로토콜** 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-234">Select the **WebSocket Protocol** feature.</span></span> <span data-ttu-id="e6cc9-235">자세한 내용은 [WebSocket](xref:fundamentals/websockets)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-235">For more information, see [WebSockets](xref:fundamentals/websockets).</span></span>

1. <span data-ttu-id="e6cc9-236">**확인** 단계를 진행하여 웹 서버 역할 및 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-236">Proceed through the **Confirmation** step to install the web server role and services.</span></span> <span data-ttu-id="e6cc9-237">**웹 서버(IIS)** 역할을 설치한 후에 서버/IIS를 다시 시작할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-237">A server/IIS restart isn't required after installing the **Web Server (IIS)** role.</span></span>

<span data-ttu-id="e6cc9-238">**Windows 데스크톱 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-238">**Windows desktop operating systems**</span></span>

<span data-ttu-id="e6cc9-239">**IIS 관리 콘솔** 및 **World Wide Web 서비스**를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-239">Enable the **IIS Management Console** and **World Wide Web Services**.</span></span>

1. <span data-ttu-id="e6cc9-240">**제어판** > **프로그램** > **프로그램 및 기능** > **Windows 기능 Windows 기능 사용/사용 안 함**(화면 왼쪽)으로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-240">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span>

1. <span data-ttu-id="e6cc9-241">**인터넷 정보 서비스** 노드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-241">Open the **Internet Information Services** node.</span></span> <span data-ttu-id="e6cc9-242">**웹 관리 도구** 노드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-242">Open the **Web Management Tools** node.</span></span>

1. <span data-ttu-id="e6cc9-243">**IIS 관리 콘솔** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-243">Check the box for **IIS Management Console**.</span></span>

1. <span data-ttu-id="e6cc9-244">**World Wide Web 서비스** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-244">Check the box for **World Wide Web Services**.</span></span>

1. <span data-ttu-id="e6cc9-245">**World Wide Web 서비스**의 기본 기능을 그대로 사용하거나 IIS 기능을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-245">Accept the default features for **World Wide Web Services** or customize the IIS features.</span></span>

   <span data-ttu-id="e6cc9-246">**Windows 인증(선택 사항)**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-246">**Windows Authentication (Optional)**</span></span>  
   <span data-ttu-id="e6cc9-247">Windows 인증을 사용하도록 설정하려면 **World Wide Web 서비스** > **보안** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-247">To enable Windows Authentication, expand the following nodes: **World Wide Web Services** > **Security**.</span></span> <span data-ttu-id="e6cc9-248">**Windows 인증** 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-248">Select the **Windows Authentication** feature.</span></span> <span data-ttu-id="e6cc9-249">자세한 내용은 [Windows 인증 \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) 및 [Windows 인증 구성](xref:security/authentication/windowsauth)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-249">For more information, see [Windows Authentication \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) and [Configure Windows authentication](xref:security/authentication/windowsauth).</span></span>

   <span data-ttu-id="e6cc9-250">**WebSockets(선택 사항)**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-250">**WebSockets (Optional)**</span></span>  
   <span data-ttu-id="e6cc9-251">WebSockets는 ASP.NET Core 1.1 이상에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-251">WebSockets is supported with ASP.NET Core 1.1 or later.</span></span> <span data-ttu-id="e6cc9-252">WebSockets를 사용하도록 설정하려면 **World Wide Web 서비스** > **응용 프로그램 개발 기능** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-252">To enable WebSockets, expand the following nodes: **World Wide Web Services** > **Application Development Features**.</span></span> <span data-ttu-id="e6cc9-253">**WebSocket 프로토콜** 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-253">Select the **WebSocket Protocol** feature.</span></span> <span data-ttu-id="e6cc9-254">자세한 내용은 [WebSocket](xref:fundamentals/websockets)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-254">For more information, see [WebSockets](xref:fundamentals/websockets).</span></span>

1. <span data-ttu-id="e6cc9-255">IIS 설치 시 다시 시작해야 하는 경우 시스템을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-255">If the IIS installation requires a restart, restart the system.</span></span>

![Windows 기능에서 선택된 IIS 관리 콘솔 및 World Wide Web 서비스](index/_static/windows-features-win10.png)

## <a name="install-the-net-core-hosting-bundle"></a><span data-ttu-id="e6cc9-257">.NET Core 호스팅 번들 설치</span><span class="sxs-lookup"><span data-stu-id="e6cc9-257">Install the .NET Core Hosting Bundle</span></span>

<span data-ttu-id="e6cc9-258">호스팅 시스템에 *.NET Core 호스팅 번들*을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-258">Install the *.NET Core Hosting Bundle* on the hosting system.</span></span> <span data-ttu-id="e6cc9-259">번들은 .NET Core 런타임, .NET Core 라이브러리 및 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-259">The bundle installs the .NET Core Runtime, .NET Core Library, and the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="e6cc9-260">이 모듈을 통해 ASP.NET Core 앱을 IIS 배후에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-260">The module allows ASP.NET Core apps to run behind IIS.</span></span> <span data-ttu-id="e6cc9-261">시스템이 인터넷에 연결되지 않은 경우 [Microsoft Visual C++ 2015 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=53840)를 설치한 후에 .NET Core 호스팅 번들을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-261">If the system doesn't have an Internet connection, obtain and install the [Microsoft Visual C++ 2015 Redistributable](https://www.microsoft.com/download/details.aspx?id=53840) before installing the .NET Core Hosting Bundle.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6cc9-262">IIS 이전에 호스팅 번들이 설치된 경우 번들 설치를 복구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-262">If the Hosting Bundle is installed before IIS, the bundle installation must be repaired.</span></span> <span data-ttu-id="e6cc9-263">IIS를 설치한 후 호스팅 번들 설치 프로그램을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-263">Run the Hosting Bundle installer again after installing IIS.</span></span>

### <a name="direct-download-current-version"></a><span data-ttu-id="e6cc9-264">직접 다운로드(현재 버전)</span><span class="sxs-lookup"><span data-stu-id="e6cc9-264">Direct download (current version)</span></span>

<span data-ttu-id="e6cc9-265">다음 링크를 사용하여 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-265">Download the installer using the following link:</span></span>

[<span data-ttu-id="e6cc9-266">현재 .NET Core 호스팅 번들 설치 관리자(직접 다운로드)</span><span class="sxs-lookup"><span data-stu-id="e6cc9-266">Current .NET Core Hosting Bundle installer (direct download)</span></span>](https://www.microsoft.com/net/permalink/dotnetcore-current-windows-runtime-bundle-installer)

### <a name="earlier-versions-of-the-installer"></a><span data-ttu-id="e6cc9-267">이전 버전의 설치 관리자</span><span class="sxs-lookup"><span data-stu-id="e6cc9-267">Earlier versions of the installer</span></span>

<span data-ttu-id="e6cc9-268">이전 버전의 설치 관리자를 가져오려면:</span><span class="sxs-lookup"><span data-stu-id="e6cc9-268">To obtain an earlier version of the installer:</span></span>

1. <span data-ttu-id="e6cc9-269">[.NET 다운로드 보관](https://www.microsoft.com/net/download/archives)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-269">Navigate to the [.NET download archives](https://www.microsoft.com/net/download/archives).</span></span>
1. <span data-ttu-id="e6cc9-270">**.NET Core**에서 .NET Core 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-270">Under **.NET Core**, select the .NET Core version.</span></span>
1. <span data-ttu-id="e6cc9-271">**앱 실행 - 런타임** 열에서 원하는 .NET Core 런타임 버전의 행을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-271">In the **Run apps - Runtime** column, find the row of the .NET Core runtime version desired.</span></span>
1. <span data-ttu-id="e6cc9-272">**런타임 및 호스팅 번들** 링크를 사용하여 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-272">Download the installer using the **Runtime & Hosting Bundle** link.</span></span>

> [!WARNING]
> <span data-ttu-id="e6cc9-273">일부 설치 관리자는 EOL(수명 종료)에 도달한 릴리스 버전을 포함하고 Microsoft에서 더 이상 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-273">Some installers contain release versions that have reached their end of life (EOL) and are no longer supported by Microsoft.</span></span> <span data-ttu-id="e6cc9-274">자세한 내용은 [지원 정책](https://www.microsoft.com/net/download/dotnet-core/2.0)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-274">For more information, see the [support policy](https://www.microsoft.com/net/download/dotnet-core/2.0).</span></span>

### <a name="install-the-hosting-bundle"></a><span data-ttu-id="e6cc9-275">호스팅 번들 설치</span><span class="sxs-lookup"><span data-stu-id="e6cc9-275">Install the Hosting Bundle</span></span>

1. <span data-ttu-id="e6cc9-276">서버에서 설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-276">Run the installer on the server.</span></span> <span data-ttu-id="e6cc9-277">관리자 명령 프롬프트에서 설치 관리자를 실행할 때 다음 스위치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-277">The following switches are available when running the installer from an administrator command prompt:</span></span>

   * <span data-ttu-id="e6cc9-278">`OPT_NO_ANCM=1` &ndash; ASP.NET Core 모듈 설치를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-278">`OPT_NO_ANCM=1` &ndash; Skip installing the ASP.NET Core Module.</span></span>
   * <span data-ttu-id="e6cc9-279">`OPT_NO_RUNTIME=1` &ndash; .NET Core 런타임 설치를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-279">`OPT_NO_RUNTIME=1` &ndash; Skip installing the .NET Core runtime.</span></span>
   * <span data-ttu-id="e6cc9-280">`OPT_NO_SHAREDFX=1` &ndash; ASP.NET 공유 프레임워크(ASP.NET 런타임) 설치를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-280">`OPT_NO_SHAREDFX=1` &ndash; Skip installing the ASP.NET Shared Framework (ASP.NET runtime).</span></span>
   * <span data-ttu-id="e6cc9-281">`OPT_NO_X86=1` &ndash; x86 런타임 설치를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-281">`OPT_NO_X86=1` &ndash; Skip installing x86 runtimes.</span></span> <span data-ttu-id="e6cc9-282">32비트 앱을 호스팅하지 않음을 아는 경우 이 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-282">Use this switch when you know that you won't be hosting 32-bit apps.</span></span> <span data-ttu-id="e6cc9-283">향후 32비트와 64비트 앱을 모두 호스트할 수 있는 기회가 있는 경우 이 스위치를 사용하지 않고 두 런타임을 모두 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-283">If there's any chance that you will host both 32-bit and 64-bit apps in the future, don't use this switch and install both runtimes.</span></span>
1. <span data-ttu-id="e6cc9-284">시스템을 다시 시작하거나 명령 프롬프트에서 **net stop was /y**, **net start w3svc**를 차례로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-284">Restart the system or execute **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span> <span data-ttu-id="e6cc9-285">IIS를 다시 시작하면 설치 관리자에서 변경된 시스템 PATH(환경 변수)의 내용이 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-285">Restarting IIS picks up a change to the system PATH, which is an environment variable, made by the installer.</span></span>

<span data-ttu-id="e6cc9-286">Windows 호스팅 번들 설치 관리자는 설치를 완료하기 위해 IIS를 다시 설정해야 함을 발견하면 IIS를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-286">If the Windows Hosting Bundle installer detects that IIS requires a reset in order to complete installation, the installer resets IIS.</span></span> <span data-ttu-id="e6cc9-287">설치 관리자가 IIS 다시 설정을 트리거하면 모든 IIS 앱 풀 및 웹 사이트가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-287">If the installer triggers an IIS reset, all of the IIS app pools and websites are restarted.</span></span>

> [!NOTE]
> <span data-ttu-id="e6cc9-288">IIS 공유 구성에 대한 자세한 내용은 [IIS 공유 구성을 사용하는 ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-288">For information on IIS Shared Configuration, see [ASP.NET Core Module with IIS Shared Configuration](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration).</span></span>

## <a name="install-web-deploy-when-publishing-with-visual-studio"></a><span data-ttu-id="e6cc9-289">Visual Studio을 사용하여 게시할 때 웹 배포 설치</span><span class="sxs-lookup"><span data-stu-id="e6cc9-289">Install Web Deploy when publishing with Visual Studio</span></span>

<span data-ttu-id="e6cc9-290">[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)를 사용하여 앱을 서버에 배포하는 경우 최신 버전의 웹 배포를 서버에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-290">When deploying apps to servers with [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy), install the latest version of Web Deploy on the server.</span></span> <span data-ttu-id="e6cc9-291">웹 배포를 설치하려면 [WebPI(웹 플랫폼 설치 관리자)](https://www.microsoft.com/web/downloads/platform.aspx)를 사용하거나 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=43717)에서 직접 설치 관리자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-291">To install Web Deploy, use the [Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx) or obtain an installer directly from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=43717).</span></span> <span data-ttu-id="e6cc9-292">WebPI를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-292">The preferred method is to use WebPI.</span></span> <span data-ttu-id="e6cc9-293">WebPI는 호스팅 공급자에 대한 독립 실행형 설치 및 구성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-293">WebPI offers a standalone setup and a configuration for hosting providers.</span></span>

## <a name="create-the-iis-site"></a><span data-ttu-id="e6cc9-294">IIS 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="e6cc9-294">Create the IIS site</span></span>

1. <span data-ttu-id="e6cc9-295">호스팅 시스템에서 앱의 게시된 폴더 및 파일을 포함할 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-295">On the hosting system, create a folder to contain the app's published folders and files.</span></span> <span data-ttu-id="e6cc9-296">앱의 배포 레이아웃은 [디렉터리 구조](xref:host-and-deploy/directory-structure) 항목에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-296">An app's deployment layout is described in the [Directory Structure](xref:host-and-deploy/directory-structure) topic.</span></span>

1. <span data-ttu-id="e6cc9-297">stdout 로깅을 사용하도록 설정할 경우 ASP.NET Core 모듈 stdout 로그를 보관할 *logs* 폴더를 새 폴더 안에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-297">Within the new folder, create a *logs* folder to hold ASP.NET Core Module stdout logs when stdout logging is enabled.</span></span> <span data-ttu-id="e6cc9-298">앱이 페이로드에서 *logs* 폴더로 배포되는 경우 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-298">If the app is deployed with a *logs* folder in the payload, skip this step.</span></span> <span data-ttu-id="e6cc9-299">로컬에서 프로젝트가 빌드될 때 MSBuild에서 *logs* 폴더를 자동으로 만들도록 설정하는 방법에 대한 지침은 [디렉터리 구조](xref:host-and-deploy/directory-structure) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-299">For instructions on how to enable MSBuild to create the *logs* folder automatically when the project is built locally, see the [Directory structure](xref:host-and-deploy/directory-structure) topic.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="e6cc9-300">stdout 로그는 앱 시작 오류의 문제 해결 용도로만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-300">Only use the stdout log to troubleshoot app startup failures.</span></span> <span data-ttu-id="e6cc9-301">일상적인 앱 로깅에는 stdout 로깅을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-301">Never use stdout logging for routine app logging.</span></span> <span data-ttu-id="e6cc9-302">로그 파일 크기 또는 생성되는 로그 파일 수에 대한 제한은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-302">There's no limit on log file size or the number of log files created.</span></span> <span data-ttu-id="e6cc9-303">앱 풀에는 로그가 기록될 위치에 쓰기 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-303">The app pool must have write access to the location where the logs are written.</span></span> <span data-ttu-id="e6cc9-304">로그 위치에 대한 해당 경로에 있는 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-304">All of the folders on the path to the log location must exist.</span></span> <span data-ttu-id="e6cc9-305">stdout 로그에 대한 자세한 내용은 [로그 생성 및 리디렉션](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-305">For more information on the stdout log, see [Log creation and redirection](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection).</span></span> <span data-ttu-id="e6cc9-306">ASP.NET Core 앱의 로깅에 대한 자세한 내용은 [로깅](xref:fundamentals/logging/index) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-306">For information on logging in an ASP.NET Core app, see the [Logging](xref:fundamentals/logging/index) topic.</span></span>

1. <span data-ttu-id="e6cc9-307">**IIS 관리자**의 **연결** 패널에서 서버 노드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-307">In **IIS Manager**, open the server's node in the **Connections** panel.</span></span> <span data-ttu-id="e6cc9-308">**사이트** 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-308">Right-click the **Sites** folder.</span></span> <span data-ttu-id="e6cc9-309">상황에 맞는 메뉴에서 **웹 사이트 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-309">Select **Add Website** from the contextual menu.</span></span>

1. <span data-ttu-id="e6cc9-310">**사이트 이름**을 제공하고 **실제 경로**를 앱의 배포 폴더로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-310">Provide a **Site name** and set the **Physical path** to the app's deployment folder.</span></span> <span data-ttu-id="e6cc9-311">**바인딩** 구성을 제공하고 **확인**을 선택하여 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-311">Provide the **Binding** configuration and create the website by selecting **OK**:</span></span>

   ![[웹 사이트 추가] 단계에서 사이트 이름, 실제 경로 및 호스트 이름을 제공합니다.](index/_static/add-website-ws2016.png)

   > [!WARNING]
   > <span data-ttu-id="e6cc9-313">최상위 와일드카드 바인딩(`http://*:80/` 및 `http://+:80`)을 사용하지 **않아야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-313">Top-level wildcard bindings (`http://*:80/` and `http://+:80`) should **not** be used.</span></span> <span data-ttu-id="e6cc9-314">최상위 와일드카드 바인딩은 보안 취약점에 앱을 노출시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-314">Top-level wildcard bindings can open up your app to security vulnerabilities.</span></span> <span data-ttu-id="e6cc9-315">강력한 와일드카드와 약한 와일드카드 모두에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-315">This applies to both strong and weak wildcards.</span></span> <span data-ttu-id="e6cc9-316">와일드카드보다는 명시적 호스트 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-316">Use explicit host names rather than wildcards.</span></span> <span data-ttu-id="e6cc9-317">전체 부모 도메인을 제어하는 경우 하위 도메인 와일드카드 바인딩(예: `*.mysub.com`)에는 이러한 보안 위험이 없습니다(취약한 `*.com`과 반대임).</span><span class="sxs-lookup"><span data-stu-id="e6cc9-317">Subdomain wildcard binding (for example, `*.mysub.com`) doesn't have this security risk if you control the entire parent domain (as opposed to `*.com`, which is vulnerable).</span></span> <span data-ttu-id="e6cc9-318">자세한 내용은 [rfc7230 섹션-5.4](https://tools.ietf.org/html/rfc7230#section-5.4)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-318">See [rfc7230 section-5.4](https://tools.ietf.org/html/rfc7230#section-5.4) for more information.</span></span>

1. <span data-ttu-id="e6cc9-319">서버 노드에서 **응용 프로그램 풀**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-319">Under the server's node, select **Application Pools**.</span></span>

1. <span data-ttu-id="e6cc9-320">사이트의 앱 풀을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **기본 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-320">Right-click the site's app pool and select **Basic Settings** from the contextual menu.</span></span>

1. <span data-ttu-id="e6cc9-321">**응용 프로그램 풀 편집** 창에서 **.NET CLR 버전**을 **관리 코드 없음**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-321">In the **Edit Application Pool** window, set the **.NET CLR version** to **No Managed Code**:</span></span>

   ![.NET CLR 버전에 대해 관리 코드 없음 설정](index/_static/edit-apppool-ws2016.png)

    <span data-ttu-id="e6cc9-323">ASP.NET Core는 별도의 프로세스에서 실행되며 런타임을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-323">ASP.NET Core runs in a separate process and manages the runtime.</span></span> <span data-ttu-id="e6cc9-324">ASP.NET Core에서는 데스크톱 CLR을 로드할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-324">ASP.NET Core doesn't rely on loading the desktop CLR.</span></span> <span data-ttu-id="e6cc9-325">**.NET CLR 버전**을 **관리 코드 없음**으로 설정하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-325">Setting the **.NET CLR version** to **No Managed Code** is optional.</span></span>

1. <span data-ttu-id="e6cc9-326">프로세스 모델 ID에 적절한 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-326">Confirm the process model identity has the proper permissions.</span></span>

   <span data-ttu-id="e6cc9-327">응용 프로그램 풀의 기본 ID(**프로세스 모델** > **ID**)가 **ApplicationPoolIdentity**에서 다른 ID로 변경되면, 새 ID에 앱의 폴더, 데이터베이스 및 기타 필요한 리소스에 액세스하는 데 필요한 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-327">If the default identity of the app pool (**Process Model** > **Identity**) is changed from **ApplicationPoolIdentity** to another identity, verify that the new identity has the required permissions to access the app's folder, database, and other required resources.</span></span> <span data-ttu-id="e6cc9-328">예를 들어 앱 풀에는 앱이 파일을 읽고 쓰는 폴더에 대한 읽기 및 쓰기 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-328">For example, the app pool requires read and write access to folders where the app reads and writes files.</span></span>

<span data-ttu-id="e6cc9-329">**Windows 인증 구성(선택 사항)**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-329">**Windows Authentication configuration (Optional)**</span></span>  
<span data-ttu-id="e6cc9-330">자세한 내용은 [Windows 인증 구성](xref:security/authentication/windowsauth)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-330">For more information, see [Configure Windows authentication](xref:security/authentication/windowsauth).</span></span>

## <a name="deploy-the-app"></a><span data-ttu-id="e6cc9-331">앱 배포</span><span class="sxs-lookup"><span data-stu-id="e6cc9-331">Deploy the app</span></span>

<span data-ttu-id="e6cc9-332">호스팅 시스템에 만든 폴더에 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-332">Deploy the app to the folder created on the hosting system.</span></span> <span data-ttu-id="e6cc9-333">[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)는 배포에 권장되는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-333">[Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) is the recommended mechanism for deployment.</span></span>

### <a name="web-deploy-with-visual-studio"></a><span data-ttu-id="e6cc9-334">Visual Studio를 사용한 웹 배포</span><span class="sxs-lookup"><span data-stu-id="e6cc9-334">Web Deploy with Visual Studio</span></span>

<span data-ttu-id="e6cc9-335">웹 배포에서 사용할 게시 프로필을 만드는 방법은 [ASP.NET Core 앱 배포용 Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-335">See the [Visual Studio publish profiles for ASP.NET Core app deployment](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles) topic to learn how to create a publish profile for use with Web Deploy.</span></span> <span data-ttu-id="e6cc9-336">호스팅 공급자가 게시 프로필을 제공하거나 게시 프로필을 만들 수 있도록 지원하는 경우 해당 프로필을 다운로드하고 Visual Studio **게시** 대화 상자를 사용하여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-336">If the hosting provider provides a Publish Profile or support for creating one, download their profile and import it using the Visual Studio **Publish** dialog.</span></span>

![게시 대화 상자 페이지](index/_static/pub-dialog.png)

### <a name="web-deploy-outside-of-visual-studio"></a><span data-ttu-id="e6cc9-338">Visual Studio 외부에서 웹 배포</span><span class="sxs-lookup"><span data-stu-id="e6cc9-338">Web Deploy outside of Visual Studio</span></span>

<span data-ttu-id="e6cc9-339">[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)는 Visual Studio 외부에서 명령줄을 통해 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-339">[Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) can also be used outside of Visual Studio from the command line.</span></span> <span data-ttu-id="e6cc9-340">자세한 내용은 [웹 배포 도구](/iis/publish/using-web-deploy/use-the-web-deployment-tool)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-340">For more information, see [Web Deployment Tool](/iis/publish/using-web-deploy/use-the-web-deployment-tool).</span></span>

### <a name="alternatives-to-web-deploy"></a><span data-ttu-id="e6cc9-341">웹 배포에 대한 대안</span><span class="sxs-lookup"><span data-stu-id="e6cc9-341">Alternatives to Web Deploy</span></span>

<span data-ttu-id="e6cc9-342">수동 복사, Xcopy, Robocopy, PowerShell 등의 여러 방법 중 하나를 사용하여 앱을 호스팅 시스템으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-342">Use any of several methods to move the app to the hosting system, such as manual copy, Xcopy, Robocopy, or PowerShell.</span></span>

<span data-ttu-id="e6cc9-343">IIS에 ASP.NET Core 배포에 대한 자세한 내용은 [IIS 관리자를 위한 배포 리소스](#deployment-resources-for-iis-administrators) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-343">For more information on ASP.NET Core deployment to IIS, see the [Deployment resources for IIS administrators](#deployment-resources-for-iis-administrators) section.</span></span>

## <a name="browse-the-website"></a><span data-ttu-id="e6cc9-344">웹 사이트 찾아보기</span><span class="sxs-lookup"><span data-stu-id="e6cc9-344">Browse the website</span></span>

![IIS 시작 페이지가 로드된 Microsoft Edge 브라우저](index/_static/browsewebsite.png)

## <a name="locked-deployment-files"></a><span data-ttu-id="e6cc9-346">배포 파일이 잠겨 있음</span><span class="sxs-lookup"><span data-stu-id="e6cc9-346">Locked deployment files</span></span>

<span data-ttu-id="e6cc9-347">앱이 실행 중이면 배포 폴더의 파일이 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-347">Files in the deployment folder are locked when the app is running.</span></span> <span data-ttu-id="e6cc9-348">잠긴 파일은 배포 중에 덮어쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-348">Locked files can't be overwritten during deployment.</span></span> <span data-ttu-id="e6cc9-349">배포에서 잠긴 파일을 해제하려면 다음 방법 중 **하나**를 사용하여 앱 풀을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-349">To release locked files in a deployment, stop the app pool using **one** of the following approaches:</span></span>

* <span data-ttu-id="e6cc9-350">웹 배포를 사용하고 프로젝트 파일에서 `Microsoft.NET.Sdk.Web`을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-350">Use Web Deploy and reference `Microsoft.NET.Sdk.Web` in the project file.</span></span> <span data-ttu-id="e6cc9-351">*app_offline.htm* 파일은 웹앱 디렉터리의 루트에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-351">An *app_offline.htm* file is placed at the root of the web app directory.</span></span> <span data-ttu-id="e6cc9-352">파일이 있는 경우 ASP.NET Core 모듈은 앱을 정상적으로 종료하고, 배포하는 동안 *app_offline.htm* 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-352">When the file is present, the ASP.NET Core Module gracefully shuts down the app and serves the *app_offline.htm* file during the deployment.</span></span> <span data-ttu-id="e6cc9-353">자세한 내용은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module#app_offlinehtm)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-353">For more information, see the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module#app_offlinehtm).</span></span>
* <span data-ttu-id="e6cc9-354">서버의 IIS 관리자에서 앱 풀을 수동으로 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-354">Manually stop the app pool in the IIS Manager on the server.</span></span>
* <span data-ttu-id="e6cc9-355">PowerShell을 사용하여 *app_offline.html*을 삭제합니다(PowerShell 5 이상 필요).</span><span class="sxs-lookup"><span data-stu-id="e6cc9-355">Use PowerShell to drop *app_offline.html* (requires PowerShell 5 or later):</span></span>

  ```PowerShell
  $pathToApp = 'PATH_TO_APP'

  # Stop the AppPool
  New-Item -Path $pathToApp app_offline.htm

  # Provide script commands here to deploy the app

  # Restart the AppPool
  Remove-Item -Path $pathToApp app_offline.htm

  ```

## <a name="data-protection"></a><span data-ttu-id="e6cc9-356">데이터 보호</span><span class="sxs-lookup"><span data-stu-id="e6cc9-356">Data protection</span></span>

<span data-ttu-id="e6cc9-357">[ASP.NET Core 데이터 보호 스택](xref:security/data-protection/introduction)은 인증에 사용되는 미들웨어를 포함하여 여러 ASP.NET Core [미들웨어](xref:fundamentals/middleware/index)에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-357">The [ASP.NET Core Data Protection stack](xref:security/data-protection/introduction) is used by several ASP.NET Core [middlewares](xref:fundamentals/middleware/index), including middleware used in authentication.</span></span> <span data-ttu-id="e6cc9-358">사용자 코드에서 데이터 보호 API가 호출되지 않더라도 배포 스크립트 또는 사용자 코드를 통해 영구적 암호화 [키 저장소](xref:security/data-protection/implementation/key-management)를 만들도록 데이터 보호를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-358">Even if Data Protection APIs aren't called by user code, data protection should be configured with a deployment script or in user code to create a persistent cryptographic [key store](xref:security/data-protection/implementation/key-management).</span></span> <span data-ttu-id="e6cc9-359">데이터 보호를 구성하지 않으면 키는 메모리에 보관되고 앱이 다시 시작되면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-359">If data protection isn't configured, the keys are held in memory and discarded when the app restarts.</span></span>

<span data-ttu-id="e6cc9-360">키 링이 메모리에 저장된 경우 앱을 다시 시작하면 다음과 같이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-360">If the key ring is stored in memory when the app restarts:</span></span>

* <span data-ttu-id="e6cc9-361">모든 쿠키 기반 인증 토큰이 무효화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-361">All cookie-based authentication tokens are invalidated.</span></span> 
* <span data-ttu-id="e6cc9-362">사용자는 다음 요청에서 다시 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-362">Users are required to sign in again on their next request.</span></span> 
* <span data-ttu-id="e6cc9-363">키 링으로 보호된 데이터의 암호를 더 이상 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-363">Any data protected with the key ring can no longer be decrypted.</span></span> <span data-ttu-id="e6cc9-364">여기에는 [CSRF 토큰](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) 및 [ASP.NET Core MVC TempData 쿠키](xref:fundamentals/app-state#tempdata)가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-364">This may include [CSRF tokens](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) and [ASP.NET Core MVC TempData cookies](xref:fundamentals/app-state#tempdata).</span></span>

<span data-ttu-id="e6cc9-365">IIS에서 키 링을 저장하도록 데이터 보호를 구성하려면 다음 방법 중 **하나**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-365">To configure data protection under IIS to persist the key ring, use **one** of the following approaches:</span></span>

* <span data-ttu-id="e6cc9-366">**데이터 보호 레지스트리키 만들기**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-366">**Create Data Protection Registry Keys**</span></span>

  <span data-ttu-id="e6cc9-367">ASP.NET 앱에서 사용되는 데이터 보호 키는 앱 외부의 레지스트리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-367">Data protection keys used by ASP.NET Core apps are stored in the registry external to the apps.</span></span> <span data-ttu-id="e6cc9-368">지정된 앱의 키를 저장하려면 앱 풀에 대한 레지스트리 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-368">To persist the keys for a given app, create registry keys for the app pool.</span></span>

  <span data-ttu-id="e6cc9-369">WebFarm이 아닌 독립 실행형 IIS 설치의 경우 [Data Protection Provision-AutoGenKeys.ps1 PowerShell 스크립트](https://github.com/aspnet/AspNetCore/blob/master/src/DataProtection/Provision-AutoGenKeys.ps1)를 ASP.NET Core 앱과 함께 사용되는 각 응용 프로그램 풀에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-369">For standalone, non-webfarm IIS installations, the [Data Protection Provision-AutoGenKeys.ps1 PowerShell script](https://github.com/aspnet/AspNetCore/blob/master/src/DataProtection/Provision-AutoGenKeys.ps1) can be used for each app pool used with an ASP.NET Core app.</span></span> <span data-ttu-id="e6cc9-370">이 스크립트는 앱의 앱 풀 작업자 프로세스 계정만 액세스할 수 있는 HKLM 레지스트리에 레지스트리 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-370">This script creates a registry key in the HKLM registry that's accessible only to the worker process account of the app's app pool.</span></span> <span data-ttu-id="e6cc9-371">미사용 키는 컴퓨터 전체 키가 있는 DPAPI를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-371">Keys are encrypted at rest using DPAPI with a machine-wide key.</span></span>

  <span data-ttu-id="e6cc9-372">웹 팜 시나리오에서는 UNC 경로를 사용하여 데이터 보호 키 링을 저장하도록 앱을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-372">In web farm scenarios, an app can be configured to use a UNC path to store its data protection key ring.</span></span> <span data-ttu-id="e6cc9-373">기본적으로 데이터 보호 키는 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-373">By default, the data protection keys aren't encrypted.</span></span> <span data-ttu-id="e6cc9-374">네트워크 공유에 대한 파일 권한은 앱 실행에 사용되는 Windows 계정으로 제한되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-374">Ensure that the file permissions for the network share are limited to the Windows account the app runs under.</span></span> <span data-ttu-id="e6cc9-375">X509 인증서를 사용하여 미사용 키를 보호할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-375">An X509 certificate can be used to protect keys at rest.</span></span> <span data-ttu-id="e6cc9-376">사용자가 인증서를 업로드할 수 있는 메커니즘을 사용하는 것이 좋습니다. 즉 사용자의 신뢰할 수 있는 인증서 저장소에 인증서를 배치하고, 사용자의 앱이 실행되는 모든 컴퓨터에서 이 인증서를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-376">Consider a mechanism to allow users to upload certificates: Place certificates into the user's trusted certificate store and ensure they're available on all machines where the user's app runs.</span></span> <span data-ttu-id="e6cc9-377">자세한 내용은 [ASP.NET Core 데이터 보호 구성](xref:security/data-protection/configuration/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-377">See [Configure ASP.NET Core Data Protection](xref:security/data-protection/configuration/overview) for details.</span></span>

* <span data-ttu-id="e6cc9-378">**사용자 프로필을 로드하도록 IIS 응용 프로그램 풀 구성**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-378">**Configure the IIS Application Pool to load the user profile**</span></span>

  <span data-ttu-id="e6cc9-379">이 설정은 앱 풀에 대한 **고급 설정** 아래의 **프로세스 모델** 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-379">This setting is in the **Process Model** section under the **Advanced Settings** for the app pool.</span></span> <span data-ttu-id="e6cc9-380">사용자 프로필 로드를 `True`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-380">Set Load User Profile to `True`.</span></span> <span data-ttu-id="e6cc9-381">이렇게 하면 사용자 프로필 디렉터리 아래에 키가 저장되고, 앱 풀에서 사용되는 사용자 계정과 관련된 키로 DPAPI를 사용하여 키가 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-381">This stores keys under the user profile directory and protects them using DPAPI with a key specific to the user account used by the app pool.</span></span>

* <span data-ttu-id="e6cc9-382">**파일 시스템을 키 링 저장소로 사용**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-382">**Use the file system as a key ring store**</span></span>

  <span data-ttu-id="e6cc9-383">[파일 시스템을 키 링 저장소로 사용](xref:security/data-protection/configuration/overview)하도록 앱 코드를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-383">Adjust the app code to [use the file system as a key ring store](xref:security/data-protection/configuration/overview).</span></span> <span data-ttu-id="e6cc9-384">X509 인증서를 사용하여 키 링을 보호하고 신뢰할 수 있는 인증서인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-384">Use an X509 certificate to protect the key ring and ensure the certificate is a trusted certificate.</span></span> <span data-ttu-id="e6cc9-385">자체 서명된 인증서인 경우 신뢰할 수 있는 루트 저장소에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-385">If the certificate is self-signed, place the certificate in the Trusted Root store.</span></span>

  <span data-ttu-id="e6cc9-386">웹 팜에서 IIS를 사용하는 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-386">When using IIS in a web farm:</span></span>

  * <span data-ttu-id="e6cc9-387">모든 컴퓨터에서 액세스할 수 있는 파일 공유를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-387">Use a file share that all machines can access.</span></span>
  * <span data-ttu-id="e6cc9-388">각 시스템에 X509 인증서를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-388">Deploy an X509 certificate to each machine.</span></span> <span data-ttu-id="e6cc9-389">[코드에 데이터 보호](xref:security/data-protection/configuration/overview)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-389">Configure [data protection in code](xref:security/data-protection/configuration/overview).</span></span>

* <span data-ttu-id="e6cc9-390">**데이터 보호에 대한 컴퓨터 수준 정책 설정**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-390">**Set a machine-wide policy for data protection**</span></span>

  <span data-ttu-id="e6cc9-391">데이터 보호 시스템은 데이터 보호 API를 사용하는 모든 앱에 대한 기본 [컴퓨터 수준 정책](xref:security/data-protection/configuration/machine-wide-policy) 설정을 제한적으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-391">The data protection system has limited support for setting a default [machine-wide policy](xref:security/data-protection/configuration/machine-wide-policy) for all apps that consume the Data Protection APIs.</span></span> <span data-ttu-id="e6cc9-392">자세한 내용은 <xref:security/data-protection/introduction>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-392">For more information, see <xref:security/data-protection/introduction>.</span></span>

## <a name="virtual-directories"></a><span data-ttu-id="e6cc9-393">가상 디렉터리</span><span class="sxs-lookup"><span data-stu-id="e6cc9-393">Virtual Directories</span></span>

<span data-ttu-id="e6cc9-394">[IIS 가상 디렉터리](/iis/get-started/planning-your-iis-architecture/understanding-sites-applications-and-virtual-directories-on-iis#virtual-directories)는 ASP.NET Core 앱에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-394">[IIS Virtual Directories](/iis/get-started/planning-your-iis-architecture/understanding-sites-applications-and-virtual-directories-on-iis#virtual-directories) aren't supported with ASP.NET Core apps.</span></span> <span data-ttu-id="e6cc9-395">앱은 [하위 애플리케이션](#sub-applications)으로 호스팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-395">An app can be hosted as a [sub-application](#sub-applications).</span></span>

## <a name="sub-applications"></a><span data-ttu-id="e6cc9-396">하위 애플리케이션</span><span class="sxs-lookup"><span data-stu-id="e6cc9-396">Sub-applications</span></span>

<span data-ttu-id="e6cc9-397">ASP.NET Core 앱은 [IIS 하위 애플리케이션(하위 앱)](/iis/get-started/planning-your-iis-architecture/understanding-sites-applications-and-virtual-directories-on-iis#applications)으로 호스팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-397">An ASP.NET Core app can be hosted as an [IIS sub-application (sub-app)](/iis/get-started/planning-your-iis-architecture/understanding-sites-applications-and-virtual-directories-on-iis#applications).</span></span> <span data-ttu-id="e6cc9-398">하위 앱의 경로는 루트 앱 URL의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-398">The sub-app's path becomes part of the root app's URL.</span></span>

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="e6cc9-399">하위 앱에는 ASP.NET Core 모듈이 처리기로 포함되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-399">A sub-app shouldn't include the ASP.NET Core Module as a handler.</span></span> <span data-ttu-id="e6cc9-400">하위 앱의 *web.config* 파일에 모듈이 처리기로 추가되면, 하위 앱을 찾으려고 할 때 잘못된 구성 파일을 참조하는 *500.19 내부 서버 오류*가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-400">If the module is added as a handler in a sub-app's *web.config* file, a *500.19 Internal Server Error* referencing the faulty config file is received when attempting to browse the sub-app.</span></span>

<span data-ttu-id="e6cc9-401">다음 예제에서는 ASP.NET Core 하위 앱에 대해 게시된 *web.config* 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-401">The following example shows a published *web.config* file for an ASP.NET Core sub-app:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <aspNetCore processPath="dotnet" 
      arguments=".\MyApp.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

<span data-ttu-id="e6cc9-402">ASP.NET Core 앱 아래에 비ASP .NET Core 하위 앱을 호스팅하는 경우, 하위 앱의 *web.config* 파일에서 상속된 처리기를 명시적으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-402">When hosting a non-ASP.NET Core sub-app underneath an ASP.NET Core app, explicitly remove the inherited handler in the sub-app's *web.config* file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <remove name="aspNetCore" />
    </handlers>
    <aspNetCore processPath="dotnet" 
      arguments=".\MyApp.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

::: moniker-end

<span data-ttu-id="e6cc9-403">하위 앱 내의 정적 자산 링크는 물결표-슬래시(`~/`) 표기법을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-403">Static asset links within the sub-app should use tilde-slash (`~/`) notation.</span></span> <span data-ttu-id="e6cc9-404">물결표-슬래시 표기법은 [태그 도우미](xref:mvc/views/tag-helpers/intro)를 트리거하여 하위 앱의 PathBase를 렌더링된 상대 링크 앞에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-404">Tilde-slash notation triggers a [Tag Helper](xref:mvc/views/tag-helpers/intro) to prepend the sub-app's pathbase to the rendered relative link.</span></span> <span data-ttu-id="e6cc9-405">`/subapp_path`에서 하위 앱의 경우, `src="~/image.png"`와 연결된 이미지가 `src="/subapp_path/image.png"`으로 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-405">For a sub-app at `/subapp_path`, an image linked with `src="~/image.png"` is rendered as `src="/subapp_path/image.png"`.</span></span> <span data-ttu-id="e6cc9-406">루트 앱의 정적 파일 미들웨어는 정적 파일 요청을 처리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-406">The root app's Static File Middleware doesn't process the static file request.</span></span> <span data-ttu-id="e6cc9-407">요청은 하위 앱의 정적 파일 미들웨어에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-407">The request is processed by the sub-app's Static File Middleware.</span></span>

<span data-ttu-id="e6cc9-408">정적 자산의 `src` 특성이 절대 경로(예: `src="/image.png"`)로 설정된 경우 링크는 하위 앱의 PathBase 없이 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-408">If a static asset's `src` attribute is set to an absolute path (for example, `src="/image.png"`), the link is rendered without the sub-app's pathbase.</span></span> <span data-ttu-id="e6cc9-409">루트 앱의 정적 파일 미들웨어는 루트 앱의 [webroot](xref:fundamentals/index#web-root-webroot)에서 자산을 제공하려고 시도하며 그 결과 루트 앱에서 정적 자산을 사용할 수 있지 않으면 ‘404 - 찾을 수 없음’이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-409">The root app's Static File Middleware attempts to serve the asset from the root app's [webroot](xref:fundamentals/index#web-root-webroot), which results in a *404 - Not Found* response unless the static asset is available from the root app.</span></span>

<span data-ttu-id="e6cc9-410">ASP.NET Core 앱을 다른 ASP.NET Core 앱에서 하위 앱으로 호스팅하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-410">To host an ASP.NET Core app as a sub-app under another ASP.NET Core app:</span></span>

1. <span data-ttu-id="e6cc9-411">하위 앱에 대한 앱 풀을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-411">Establish an app pool for the sub-app.</span></span> <span data-ttu-id="e6cc9-412">**.NET CLR 버전**을 **관리 코드 없음**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-412">Set the **.NET CLR Version** to **No Managed Code**.</span></span>

1. <span data-ttu-id="e6cc9-413">루트 사이트 아래의 폴더에 하위 앱을 사용하여 IIS 관리자에 루트 사이트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-413">Add the root site in IIS Manager with the sub-app in a folder under the root site.</span></span>

1. <span data-ttu-id="e6cc9-414">IIS 관리자에서 하위 앱 폴더를 마우스 오른쪽 단추로 클릭하고 **Convert to Application**(애플리케이션으로 변환)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-414">Right-click the sub-app folder in IIS Manager and select **Convert to Application**.</span></span>

1. <span data-ttu-id="e6cc9-415">**Add Application**(애플리케이션 추가) 대화 상자에서 **애플리케이션 풀**에 대한 **선택** 단추를 사용하여 하위 앱에 대해 만든 앱 풀을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-415">In the **Add Application** dialog, use the **Select** button for the **Application Pool** to assign the app pool that you created for the sub-app.</span></span> <span data-ttu-id="e6cc9-416">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-416">Select **OK**.</span></span>

<span data-ttu-id="e6cc9-417">하위 앱에 대한 별도의 앱 풀 할당은 In-process 호스팅 모델을 사용할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-417">The assignment of a separate app pool to the sub-app is a requirement when using the in-process hosting model.</span></span>

<span data-ttu-id="e6cc9-418">In-process 호스팅 모델 및 ASP.NET Core 모듈 구성에 대한 자세한 내용은 <xref:fundamentals/servers/aspnet-core-module> 및 <xref:host-and-deploy/aspnet-core-module>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-418">For more information on the in-process hosting model and configuring the ASP.NET Core Module, see <xref:fundamentals/servers/aspnet-core-module> and <xref:host-and-deploy/aspnet-core-module>.</span></span>

## <a name="configuration-of-iis-with-webconfig"></a><span data-ttu-id="e6cc9-419">web.config를 사용하여 IIS 구성</span><span class="sxs-lookup"><span data-stu-id="e6cc9-419">Configuration of IIS with web.config</span></span>

<span data-ttu-id="e6cc9-420">IIS 구성은 역방향 프록시 구성에 적용되는 IIS 기능에 대한 *web.config*에 포함된 **\<system.webServer>** 섹션의 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-420">IIS configuration is influenced by the **\<system.webServer>** section of *web.config* for those IIS features that apply to a reverse proxy configuration.</span></span> <span data-ttu-id="e6cc9-421">IIS가 서버 수준에서 동적 압축을 사용하도록 구성된 경우 앱의 *web.config* 파일에 있는 **\<urlCompression>** 요소를 통해 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-421">If IIS is configured at the server level to use dynamic compression, the **\<urlCompression>** element in the app's *web.config* file can disable it.</span></span>

<span data-ttu-id="e6cc9-422">자세한 내용은 [\<system.webServer>에 대한 구성 참조](/iis/configuration/system.webServer/), [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module) 및 [ASP.NET Core와 IIS 모듈](xref:host-and-deploy/iis/modules)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-422">For more information, see the [configuration reference for \<system.webServer>](/iis/configuration/system.webServer/), [ASP.NET Core Module Configuration Reference](xref:host-and-deploy/aspnet-core-module), and [IIS Modules with ASP.NET Core](xref:host-and-deploy/iis/modules).</span></span> <span data-ttu-id="e6cc9-423">격리된 앱 풀에서 실행되는 개별 앱에 대해 환경 변수를 설정하려면(IIS 10.0 이상에서 지원됨), IIS 참조 문서에서 [환경 변수 \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 항목의 *AppCmd.exe 명령* 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-423">To set environment variables for individual apps running in isolated app pools (supported for IIS 10.0 or later), see the *AppCmd.exe command* section of the [Environment Variables \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) topic in the IIS reference documentation.</span></span>

## <a name="configuration-sections-of-webconfig"></a><span data-ttu-id="e6cc9-424">web.config 구성 섹션</span><span class="sxs-lookup"><span data-stu-id="e6cc9-424">Configuration sections of web.config</span></span>

<span data-ttu-id="e6cc9-425">*web.config*에 있는 ASP.NET 4.x 앱의 구성 섹션은 ASP.NET Core 앱의 구성에 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-425">Configuration sections of ASP.NET 4.x apps in *web.config* aren't used by ASP.NET Core apps for configuration:</span></span>

* <span data-ttu-id="e6cc9-426">**\<system.web>**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-426">**\<system.web>**</span></span>
* <span data-ttu-id="e6cc9-427">**\<appSettings>**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-427">**\<appSettings>**</span></span>
* <span data-ttu-id="e6cc9-428">**\<connectionStrings>**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-428">**\<connectionStrings>**</span></span>
* <span data-ttu-id="e6cc9-429">**\<location>**</span><span class="sxs-lookup"><span data-stu-id="e6cc9-429">**\<location>**</span></span>

<span data-ttu-id="e6cc9-430">ASP.NET Core 앱은 다른 구성 공급자를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-430">ASP.NET Core apps are configured using other configuration providers.</span></span> <span data-ttu-id="e6cc9-431">자세한 내용은 [구성](xref:fundamentals/configuration/index)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-431">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

## <a name="application-pools"></a><span data-ttu-id="e6cc9-432">응용 프로그램 풀</span><span class="sxs-lookup"><span data-stu-id="e6cc9-432">Application Pools</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="e6cc9-433">앱 풀 격리는 호스팅 모델에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-433">App pool isolation is determined by the hosting model:</span></span>

* <span data-ttu-id="e6cc9-434">In-process 호스팅 &ndash; 앱은 별도의 앱 풀에서 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-434">In-process hosting &ndash; Apps are required to run in separate app pools.</span></span>
* <span data-ttu-id="e6cc9-435">Out-of-process 호스팅 &ndash; 각 앱을 자체 앱 풀에서 실행하여 앱을 서로 격리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-435">Out-of-process hosting &ndash; We recommend isolating the apps from each other by running each app in its own app pool.</span></span>

<span data-ttu-id="e6cc9-436">IIS **웹 사이트 추가** 대화 상자는 기본적으로 앱당 단일 앱 풀로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-436">The IIS **Add Website** dialog defaults to a single app pool per app.</span></span> <span data-ttu-id="e6cc9-437">**사이트 이름**을 제공하면 텍스트가 자동으로 **응용 프로그램 풀** 텍스트 상자로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-437">When a **Site name** is provided, the text is automatically transferred to the **Application pool** textbox.</span></span> <span data-ttu-id="e6cc9-438">사이트를 추가할 때 이 사이트 이름을 사용하여 새로운 앱 풀이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-438">A new app pool is created using the site name when the site is added.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="e6cc9-439">서버에서 여러 웹 사이트를 호스트하는 경우 각 앱을 해당 앱 풀에서 실행하여 서로 격리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-439">When hosting multiple websites on a server, we recommend isolating the apps from each other by running each app in its own app pool.</span></span> <span data-ttu-id="e6cc9-440">이 구성은 IIS **웹 사이트 추가** 대화 상자의 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-440">The IIS **Add Website** dialog defaults to this configuration.</span></span> <span data-ttu-id="e6cc9-441">**사이트 이름**을 제공하면 텍스트가 자동으로 **응용 프로그램 풀** 텍스트 상자로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-441">When a **Site name** is provided, the text is automatically transferred to the **Application pool** textbox.</span></span> <span data-ttu-id="e6cc9-442">사이트를 추가할 때 이 사이트 이름을 사용하여 새로운 앱 풀이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-442">A new app pool is created using the site name when the site is added.</span></span>

::: moniker-end

## <a name="application-pool-identity"></a><span data-ttu-id="e6cc9-443">응용 프로그램 풀 ID</span><span class="sxs-lookup"><span data-stu-id="e6cc9-443">Application Pool Identity</span></span>

<span data-ttu-id="e6cc9-444">응용 프로그램 풀 ID 계정을 사용하면 도메인 또는 로컬 계정을 만들고 관리할 필요 없이 고유한 계정으로 앱을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-444">An app pool identity account allows an app to run under a unique account without having to create and manage domains or local accounts.</span></span> <span data-ttu-id="e6cc9-445">IIS 8.0 이상에서 IIS WAS(관리 작업자 프로세스)는 새로운 앱 풀의 이름으로 가상 계정을 만들고, 기본적으로 이 계정으로 앱 풀의 작업자 프로세스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-445">On IIS 8.0 or later, the IIS Admin Worker Process (WAS) creates a virtual account with the name of the new app pool and runs the app pool's worker processes under this account by default.</span></span> <span data-ttu-id="e6cc9-446">IIS 관리 콘솔의 응용 프로그램 풀에 대한 **고급 설정** 아래에서 **ID**가 **ApplicationPoolIdentity**를 사용하도록 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-446">In the IIS Management Console under **Advanced Settings** for the app pool, ensure that the **Identity** is set to use **ApplicationPoolIdentity**:</span></span>

![응용 프로그램 풀 고급 설정 대화 상자](index/_static/apppool-identity.png)

<span data-ttu-id="e6cc9-448">IIS 관리 프로세스는 Windows 보안 시스템에 앱 풀 이름이 포함된 보안 식별자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-448">The IIS management process creates a secure identifier with the name of the app pool in the Windows Security System.</span></span> <span data-ttu-id="e6cc9-449">리소스는 이 ID를 사용하여 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-449">Resources can be secured using this identity.</span></span> <span data-ttu-id="e6cc9-450">그러나 이 ID는 실제 사용자 계정이 아니며 Windows 사용자 관리 콘솔에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-450">However, this identity isn't a real user account and doesn't show up in the Windows User Management Console.</span></span>

<span data-ttu-id="e6cc9-451">IIS 작업자 프로세스에서 앱에 대한 높은 액세스 권한이 필요한 경우 앱이 포함된 디렉터리에 대한 ACL(액세스 제어 목록)을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-451">If the IIS worker process requires elevated access to the app, modify the Access Control List (ACL) for the directory containing the app:</span></span>

1. <span data-ttu-id="e6cc9-452">[Windows 탐색기]를 열고 해당 하위 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-452">Open Windows Explorer and navigate to the directory.</span></span>

1. <span data-ttu-id="e6cc9-453">디렉터리를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-453">Right-click on the directory and select **Properties**.</span></span>

1. <span data-ttu-id="e6cc9-454">**보안** 탭 아래에서 **편집** 단추, **추가** 단추를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-454">Under the **Security** tab, select the **Edit** button and then the **Add** button.</span></span>

1. <span data-ttu-id="e6cc9-455">**위치** 단추를 선택하고 시스템이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-455">Select the **Locations** button and make sure the system is selected.</span></span>

1. <span data-ttu-id="e6cc9-456">**선택할 개체 이름 입력** 영역에 **IIS AppPool\\<app_pool_name>** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-456">Enter **IIS AppPool\\<app_pool_name>** in **Enter the object names to select** area.</span></span> <span data-ttu-id="e6cc9-457">**이름 확인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-457">Select the **Check Names** button.</span></span> <span data-ttu-id="e6cc9-458">*DefaultAppPool*의 경우 **IIS AppPool\DefaultAppPool**을 사용하는 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-458">For the *DefaultAppPool* check the names using **IIS AppPool\DefaultAppPool**.</span></span> <span data-ttu-id="e6cc9-459">**이름 확인** 단추를 선택하면 개체 이름 영역에 **DefaultAppPool** 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-459">When the **Check Names** button is selected, a value of **DefaultAppPool** is indicated in the object names area.</span></span> <span data-ttu-id="e6cc9-460">개체 이름 영역에 앱 풀 이름을 직접 입력할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-460">It isn't possible to enter the app pool name directly into the object names area.</span></span> <span data-ttu-id="e6cc9-461">개체 이름을 확인할 때는 **IIS AppPool\\<app_pool_name>** 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-461">Use the **IIS AppPool\\<app_pool_name>** format when checking for the object name.</span></span>

   ![앱 폴더에 대한 사용자 또는 그룹 대화 상자 선택: “이름 확인”을 선택하기 전에 개체 이름 영역의 “IIS AppPool\"에 앱 풀 이름 “DefaultAppPool”이 추가됩니다.](index/_static/select-users-or-groups-1.png)

1. <span data-ttu-id="e6cc9-463">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-463">Select **OK**.</span></span>

   ![앱 폴더에 대한 사용자 또는 그룹 대화 상자 선택: “이름 확인”을 선택하면 개체 이름 영역에 개체 이름 “DefaultAppPool”이 표시됩니다.](index/_static/select-users-or-groups-2.png)

1. <span data-ttu-id="e6cc9-465">읽기 및 실행 권한은 기본적으로 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-465">Read &amp; execute permissions should be granted by default.</span></span> <span data-ttu-id="e6cc9-466">필요에 따라 추가 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-466">Provide additional permissions as needed.</span></span>

<span data-ttu-id="e6cc9-467">**ICACLS** 도구를 사용하여 명령 프롬프트에서 액세스 권한을 부여할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-467">Access can also be granted at a command prompt using the **ICACLS** tool.</span></span> <span data-ttu-id="e6cc9-468">*DefaultAppPool*을 예로 들면, 다음 명령이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-468">Using the *DefaultAppPool* as an example, the following command is used:</span></span>

```console
ICACLS C:\sites\MyWebApp /grant "IIS AppPool\DefaultAppPool":F
```

<span data-ttu-id="e6cc9-469">자세한 내용은 [icacls](/windows-server/administration/windows-commands/icacls) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-469">For more information, see the [icacls](/windows-server/administration/windows-commands/icacls) topic.</span></span>

## <a name="http2-support"></a><span data-ttu-id="e6cc9-470">HTTP/2 지원</span><span class="sxs-lookup"><span data-stu-id="e6cc9-470">HTTP/2 support</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="e6cc9-471">[HTTP/2](https://httpwg.org/specs/rfc7540.html)는 다음과 같은 IIS 배포 시나리오에서 ASP.NET Core를 통해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-471">[HTTP/2](https://httpwg.org/specs/rfc7540.html) is supported with ASP.NET Core in the following IIS deployment scenarios:</span></span>

* <span data-ttu-id="e6cc9-472">In-Process</span><span class="sxs-lookup"><span data-stu-id="e6cc9-472">In-process</span></span>
  * <span data-ttu-id="e6cc9-473">Windows Server 2016/Windows 10 이상, IIS 10 이상</span><span class="sxs-lookup"><span data-stu-id="e6cc9-473">Windows Server 2016/Windows 10 or later; IIS 10 or later</span></span>
  * <span data-ttu-id="e6cc9-474">TLS 1.2 이상 연결</span><span class="sxs-lookup"><span data-stu-id="e6cc9-474">TLS 1.2 or later connection</span></span>
* <span data-ttu-id="e6cc9-475">Out of Process</span><span class="sxs-lookup"><span data-stu-id="e6cc9-475">Out-of-process</span></span>
  * <span data-ttu-id="e6cc9-476">Windows Server 2016/Windows 10 이상, IIS 10 이상</span><span class="sxs-lookup"><span data-stu-id="e6cc9-476">Windows Server 2016/Windows 10 or later; IIS 10 or later</span></span>
  * <span data-ttu-id="e6cc9-477">공용 에지 서버 연결은 HTTP/2를 사용하지만 [Kestrel 서버](xref:fundamentals/servers/kestrel)에 대한 역방향 프록시 연결은 HTTP/1.1을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-477">Public-facing edge server connections use HTTP/2, but the reverse proxy connection to the [Kestrel server](xref:fundamentals/servers/kestrel) uses HTTP/1.1.</span></span>
  * <span data-ttu-id="e6cc9-478">TLS 1.2 이상 연결</span><span class="sxs-lookup"><span data-stu-id="e6cc9-478">TLS 1.2 or later connection</span></span>

<span data-ttu-id="e6cc9-479">In-Process 배포에서 HTTP/2 연결이 설정된 경우 [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*)에서 `HTTP/2`를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-479">For an in-process deployment when an HTTP/2 connection is established, [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) reports `HTTP/2`.</span></span> <span data-ttu-id="e6cc9-480">Out of Process 배포에서 HTTP/2 연결이 설정된 경우 [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*)에서 `HTTP/1.1`을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-480">For an out-of-process deployment when an HTTP/2 connection is established, [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) reports `HTTP/1.1`.</span></span>

<span data-ttu-id="e6cc9-481">In-process 및 out-of-process 호스팅 모델에 대한 자세한 내용은 <xref:fundamentals/servers/aspnet-core-module> 항목 및 <xref:host-and-deploy/aspnet-core-module> 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-481">For more information on the in-process and out-of-process hosting models, see the <xref:fundamentals/servers/aspnet-core-module> topic and the <xref:host-and-deploy/aspnet-core-module>.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="e6cc9-482">[HTTP/2](https://httpwg.org/specs/rfc7540.html)는 다음 기본 요구 사항을 충족하는 Out of Process 배포에 대해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-482">[HTTP/2](https://httpwg.org/specs/rfc7540.html) is supported for out-of-process deployments that meet the following base requirements:</span></span>

* <span data-ttu-id="e6cc9-483">Windows Server 2016/Windows 10 이상, IIS 10 이상</span><span class="sxs-lookup"><span data-stu-id="e6cc9-483">Windows Server 2016/Windows 10 or later; IIS 10 or later</span></span>
* <span data-ttu-id="e6cc9-484">공용 에지 서버 연결은 HTTP/2를 사용하지만 [Kestrel 서버](xref:fundamentals/servers/kestrel)에 대한 역방향 프록시 연결은 HTTP/1.1을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-484">Public-facing edge server connections use HTTP/2, but the reverse proxy connection to the [Kestrel server](xref:fundamentals/servers/kestrel) uses HTTP/1.1.</span></span>
* <span data-ttu-id="e6cc9-485">대상 프레임워크: HTTP/2 연결은 IIS에 의해 완전히 처리되므로 Out of Process 배포에는 해당하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-485">Target framework: Not applicable to out-of-process deployments, since the HTTP/2 connection is handled entirely by IIS.</span></span>
* <span data-ttu-id="e6cc9-486">TLS 1.2 이상 연결</span><span class="sxs-lookup"><span data-stu-id="e6cc9-486">TLS 1.2 or later connection</span></span>

<span data-ttu-id="e6cc9-487">HTTP/2 연결이 설정된 경우 [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*)에서 `HTTP/1.1`을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-487">If an HTTP/2 connection is established, [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) reports `HTTP/1.1`.</span></span>

::: moniker-end

<span data-ttu-id="e6cc9-488">HTTP/2는 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-488">HTTP/2 is enabled by default.</span></span> <span data-ttu-id="e6cc9-489">HTTP/2 연결이 설정되지 않은 경우 연결이 HTTP/1.1로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-489">Connections fall back to HTTP/1.1 if an HTTP/2 connection isn't established.</span></span> <span data-ttu-id="e6cc9-490">IIS 배포가 포함된 HTTP/2 구성에 대한 자세한 내용은 [IIS의 HTTP/2](/iis/get-started/whats-new-in-iis-10/http2-on-iis)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-490">For more information on HTTP/2 configuration with IIS deployments, see [HTTP/2 on IIS](/iis/get-started/whats-new-in-iis-10/http2-on-iis).</span></span>

## <a name="deployment-resources-for-iis-administrators"></a><span data-ttu-id="e6cc9-491">IIS 관리자를 위한 배포 리소스</span><span class="sxs-lookup"><span data-stu-id="e6cc9-491">Deployment resources for IIS administrators</span></span>

<span data-ttu-id="e6cc9-492">IIS 설명서에서 IIS에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-492">Learn about IIS in-depth in the IIS documentation.</span></span>  
[<span data-ttu-id="e6cc9-493">IIS 설명서</span><span class="sxs-lookup"><span data-stu-id="e6cc9-493">IIS documentation</span></span>](/iis)

<span data-ttu-id="e6cc9-494">.NET Core 앱 배포 모델에 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-494">Learn about .NET Core app deployment models.</span></span>  
[<span data-ttu-id="e6cc9-495">.NET Core 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="e6cc9-495">.NET Core application deployment</span></span>](/dotnet/core/deploying/)

<span data-ttu-id="e6cc9-496">ASP.NET Core 모듈이 Kestrel 웹 서버에서 역방향 프록시 서버로 IIS 또는 IIS Express를 어떻게 사용하도록 허용하는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-496">Learn how the ASP.NET Core Module allows the Kestrel web server to use IIS or IIS Express as a reverse proxy server.</span></span>  
[<span data-ttu-id="e6cc9-497">ASP.NET Core 모듈</span><span class="sxs-lookup"><span data-stu-id="e6cc9-497">ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)

<span data-ttu-id="e6cc9-498">ASP.NET Core 앱을 호스팅하기 위해 ASP.NET Core 모듈을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-498">Learn how to configure the ASP.NET Core Module for hosting ASP.NET Core apps.</span></span>  
[<span data-ttu-id="e6cc9-499">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="e6cc9-499">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)

<span data-ttu-id="e6cc9-500">게시된 ASP.NET Core 앱의 디렉터리 구조에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-500">Learn about the directory structure of published ASP.NET Core apps.</span></span>  
[<span data-ttu-id="e6cc9-501">디렉터리 구조</span><span class="sxs-lookup"><span data-stu-id="e6cc9-501">Directory structure</span></span>](xref:host-and-deploy/directory-structure)

<span data-ttu-id="e6cc9-502">ASP.NET Core 앱용 활성 및 비활성 IIS 모듈과 IIS 모듈을 관리하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-502">Discover active and inactive IIS modules for ASP.NET Core apps and how to manage IIS modules.</span></span>  
[<span data-ttu-id="e6cc9-503">IIS 모듈</span><span class="sxs-lookup"><span data-stu-id="e6cc9-503">IIS modules</span></span>](xref:host-and-deploy/iis/troubleshoot)

<span data-ttu-id="e6cc9-504">ASP.NET Core 앱의 IIS 배포에 대한 문제 진단 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-504">Learn how to diagnose problems with IIS deployments of ASP.NET Core apps.</span></span>  
[<span data-ttu-id="e6cc9-505">문제 해결</span><span class="sxs-lookup"><span data-stu-id="e6cc9-505">Troubleshoot</span></span>](xref:host-and-deploy/iis/troubleshoot)

<span data-ttu-id="e6cc9-506">IIS에서 ASP.NET Core 앱을 호스팅할 때 일반적인 오류를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cc9-506">Distinguish common errors when hosting ASP.NET Core apps on IIS.</span></span>  
[<span data-ttu-id="e6cc9-507">Azure App Service 및 IIS에 대한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="e6cc9-507">Common errors reference for Azure App Service and IIS</span></span>](xref:host-and-deploy/azure-iis-errors-reference)

## <a name="additional-resources"></a><span data-ttu-id="e6cc9-508">추가 자료</span><span class="sxs-lookup"><span data-stu-id="e6cc9-508">Additional resources</span></span>

* <xref:test/troubleshoot>
* [<span data-ttu-id="e6cc9-509">ASP.NET Core 소개</span><span class="sxs-lookup"><span data-stu-id="e6cc9-509">Introduction to ASP.NET Core</span></span>](xref:index)
* [<span data-ttu-id="e6cc9-510">공식 Microsoft IIS 사이트</span><span class="sxs-lookup"><span data-stu-id="e6cc9-510">The Official Microsoft IIS Site</span></span>](https://www.iis.net/)
* [<span data-ttu-id="e6cc9-511">Windows Server 기술 콘텐츠 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e6cc9-511">Windows Server technical content library</span></span>](/windows-server/windows-server)
* [<span data-ttu-id="e6cc9-512">IIS의 HTTP/2</span><span class="sxs-lookup"><span data-stu-id="e6cc9-512">HTTP/2 on IIS</span></span>](/iis/get-started/whats-new-in-iis-10/http2-on-iis)
