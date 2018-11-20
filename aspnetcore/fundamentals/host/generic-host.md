---
title: .NET 일반 호스트
author: guardrex
description: 앱 시작 및 수명 관리를 담당하는 .NET의 일반 호스트에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 10/30/2018
uid: fundamentals/host/generic-host
ms.openlocfilehash: cac5ccdea7838d26b7468f9bf1ab8d317b444b46
ms.sourcegitcommit: 09bcda59a58019fdf47b2db5259fe87acf19dd38
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51708519"
---
# <a name="net-generic-host"></a><span data-ttu-id="efef6-103">.NET 일반 호스트</span><span class="sxs-lookup"><span data-stu-id="efef6-103">.NET Generic Host</span></span>

<span data-ttu-id="efef6-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="efef6-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="efef6-105">.NET Core 앱은 *호스트*를 구성 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-105">.NET Core apps configure and launch a *host*.</span></span> <span data-ttu-id="efef6-106">호스트는 앱 시작 및 수명 관리를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-106">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="efef6-107">이 항목에서는 HTTP 요청을 처리하지 않는 앱을 호스팅하는 데 유용한 ASP.NET Core 일반 호스트(<xref:Microsoft.Extensions.Hosting.HostBuilder>)를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-107">This topic covers the ASP.NET Core Generic Host (<xref:Microsoft.Extensions.Hosting.HostBuilder>), which is useful for hosting apps that don't process HTTP requests.</span></span> <span data-ttu-id="efef6-108">웹 호스트(<xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>)의 적용 범위는 <xref:fundamentals/host/web-host>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efef6-108">For coverage of the Web Host (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>), see <xref:fundamentals/host/web-host>.</span></span>

<span data-ttu-id="efef6-109">일반 호스트의 목표는 웹 호스트 API에서 HTTP 파이프라인을 분리하여 호스트 시나리오의 더 광범위한 배열을 구현하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-109">The goal of the Generic Host is to decouple the HTTP pipeline from the Web Host API to enable a wider array of host scenarios.</span></span> <span data-ttu-id="efef6-110">일반 호스트에 기반을 둔 메시징, 백그라운드 작업 및 기타 HTTP 이외 워크로드는 구성, 종속성 주입(DI) 및 로깅과 같은 교차 편집 기능에서 이점을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-110">Messaging, background tasks, and other non-HTTP workloads based on the Generic Host benefit from cross-cutting capabilities, such as configuration, dependency injection (DI), and logging.</span></span>

<span data-ttu-id="efef6-111">일반 호스트는 ASP.NET Core 2.1의 새로운 기능이며 웹 호스팅 시나리오에 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-111">The Generic Host is new in ASP.NET Core 2.1 and isn't suitable for web hosting scenarios.</span></span> <span data-ttu-id="efef6-112">웹 호스팅 시나리오의 경우 [웹 호스트](xref:fundamentals/host/web-host)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="efef6-112">For web hosting scenarios, use the [Web Host](xref:fundamentals/host/web-host).</span></span> <span data-ttu-id="efef6-113">일반 호스트는 향후 릴리스에서 웹 호스트를 대체하기 위해 개발 중이며, HTTP 및 HTTP 이외 시나리오에서 기본 호스트 API 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-113">The Generic Host is under development to replace the Web Host in a future release and act as the primary host API in both HTTP and non-HTTP scenarios.</span></span>

<span data-ttu-id="efef6-114">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="efef6-114">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="efef6-115">[Visual Studio Code](https://code.visualstudio.com/)에서 샘플 앱을 실행할 때는 *외부 또는 통합 터미널*을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="efef6-115">When running the sample app in [Visual Studio Code](https://code.visualstudio.com/), use an *external or integrated terminal*.</span></span> <span data-ttu-id="efef6-116">`internalConsole`에서는 샘플을 실행하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="efef6-116">Don't run the sample in an `internalConsole`.</span></span>

<span data-ttu-id="efef6-117">Visual Studio Code에서 콘솔을 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="efef6-117">To set the console in Visual Studio Code:</span></span>

1. <span data-ttu-id="efef6-118">*.vscode/launch.json* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-118">Open the *.vscode/launch.json* file.</span></span>
1. <span data-ttu-id="efef6-119">**.NET Core 시작(콘솔)** 구성에서 **콘솔** 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-119">In the **.NET Core Launch (console)** configuration, locate the **console** entry.</span></span> <span data-ttu-id="efef6-120">값을 `externalTerminal` 또는 `integratedTerminal` 중 하나로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-120">Set the value to either `externalTerminal` or `integratedTerminal`.</span></span>

## <a name="introduction"></a><span data-ttu-id="efef6-121">소개</span><span class="sxs-lookup"><span data-stu-id="efef6-121">Introduction</span></span>

<span data-ttu-id="efef6-122">일반 호스트 라이브러리는 <xref:Microsoft.Extensions.Hosting> 네임스페이스에서 사용할 수 있으며, [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting/) 패키지에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-122">The Generic Host library is available in the <xref:Microsoft.Extensions.Hosting> namespace and provided by the [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting/) package.</span></span> <span data-ttu-id="efef6-123">`Microsoft.Extensions.Hosting` 패키지는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)(ASP.NET Core 2.1 이상)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-123">The `Microsoft.Extensions.Hosting` package is included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) (ASP.NET Core 2.1 or later).</span></span>

<span data-ttu-id="efef6-124"><xref:Microsoft.Extensions.Hosting.IHostedService>는 코드 실행 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-124"><xref:Microsoft.Extensions.Hosting.IHostedService> is the entry point to code execution.</span></span> <span data-ttu-id="efef6-125">각 `IHostedService` 구현은 [ConfigureServices의 서비스 등록](#configureservices) 순서대로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-125">Each `IHostedService` implementation is executed in the order of [service registration in ConfigureServices](#configureservices).</span></span> <span data-ttu-id="efef6-126"><xref:Microsoft.Extensions.Hosting.IHostedService.StartAsync*>는 호스트가 시작될 때 각 `IHostedService`에서 호출되고, <xref:Microsoft.Extensions.Hosting.IHostedService.StopAsync*>는 호스트가 점진적으로 종료될 때 등록 순서의 역순으로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-126"><xref:Microsoft.Extensions.Hosting.IHostedService.StartAsync*> is called on each `IHostedService` when the host starts, and <xref:Microsoft.Extensions.Hosting.IHostedService.StopAsync*> is called in reverse registration order when the host shuts down gracefully.</span></span>

## <a name="set-up-a-host"></a><span data-ttu-id="efef6-127">호스트 설정</span><span class="sxs-lookup"><span data-stu-id="efef6-127">Set up a host</span></span>

<span data-ttu-id="efef6-128"><xref:Microsoft.Extensions.Hosting.IHostBuilder>는 라이브러리 및 앱이 호스트를 초기화, 빌드 및 실행하는 데 사용하는 주 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-128"><xref:Microsoft.Extensions.Hosting.IHostBuilder> is the main component that libraries and apps use to initialize, build, and run the host:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_HostBuilder)]

## <a name="default-services"></a><span data-ttu-id="efef6-129">기본 서비스</span><span class="sxs-lookup"><span data-stu-id="efef6-129">Default services</span></span>

<span data-ttu-id="efef6-130">호스트 초기화 중에 다음 서비스가 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-130">The following services are registered during host initialization:</span></span>

* <span data-ttu-id="efef6-131">[환경](xref:fundamentals/environments)(<xref:Microsoft.Extensions.Hosting.IHostingEnvironment>)</span><span class="sxs-lookup"><span data-stu-id="efef6-131">[Environment](xref:fundamentals/environments) (<xref:Microsoft.Extensions.Hosting.IHostingEnvironment>)</span></span>
* <xref:Microsoft.Extensions.Hosting.HostBuilderContext>
* <span data-ttu-id="efef6-132">[구성](xref:fundamentals/configuration/index)(<xref:Microsoft.Extensions.Configuration.IConfiguration>)</span><span class="sxs-lookup"><span data-stu-id="efef6-132">[Configuration](xref:fundamentals/configuration/index) (<xref:Microsoft.Extensions.Configuration.IConfiguration>)</span></span>
* <span data-ttu-id="efef6-133"><xref:Microsoft.Extensions.Hosting.IApplicationLifetime> (<xref:Microsoft.Extensions.Hosting.Internal.ApplicationLifetime>)</span><span class="sxs-lookup"><span data-stu-id="efef6-133"><xref:Microsoft.Extensions.Hosting.IApplicationLifetime> (<xref:Microsoft.Extensions.Hosting.Internal.ApplicationLifetime>)</span></span>
* <span data-ttu-id="efef6-134"><xref:Microsoft.Extensions.Hosting.IHostLifetime> (<xref:Microsoft.Extensions.Hosting.Internal.ConsoleLifetime>)</span><span class="sxs-lookup"><span data-stu-id="efef6-134"><xref:Microsoft.Extensions.Hosting.IHostLifetime> (<xref:Microsoft.Extensions.Hosting.Internal.ConsoleLifetime>)</span></span>
* <xref:Microsoft.Extensions.Hosting.IHost>
* <span data-ttu-id="efef6-135">[옵션](xref:fundamentals/configuration/options)(<xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptions*>)</span><span class="sxs-lookup"><span data-stu-id="efef6-135">[Options](xref:fundamentals/configuration/options) (<xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptions*>)</span></span>
* <span data-ttu-id="efef6-136">[로깅](xref:fundamentals/logging/index)(<xref:Microsoft.Extensions.DependencyInjection.LoggingServiceCollectionExtensions.AddLogging*>)</span><span class="sxs-lookup"><span data-stu-id="efef6-136">[Logging](xref:fundamentals/logging/index) (<xref:Microsoft.Extensions.DependencyInjection.LoggingServiceCollectionExtensions.AddLogging*>)</span></span>

## <a name="host-configuration"></a><span data-ttu-id="efef6-137">호스트 구성</span><span class="sxs-lookup"><span data-stu-id="efef6-137">Host configuration</span></span>

<span data-ttu-id="efef6-138">호스트 구성은 다음에 의해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-138">Host configuration is created by:</span></span>

* <span data-ttu-id="efef6-139"><xref:Microsoft.Extensions.Hosting.IHostBuilder>에서 확장 메서드를 호출하여 [콘텐츠 루트](#content-root) 및 [환경](#environment)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-139">Calling extension methods on <xref:Microsoft.Extensions.Hosting.IHostBuilder> to set the [content root](#content-root) and [environment](#environment).</span></span>
* <span data-ttu-id="efef6-140"><xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureHostConfiguration*>의 구성 공급자에서 구성을 읽는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-140">Reading configuration from configuration providers in <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureHostConfiguration*>.</span></span>

### <a name="extension-methods"></a><span data-ttu-id="efef6-141">확장 메서드</span><span class="sxs-lookup"><span data-stu-id="efef6-141">Extension methods</span></span>

### <a name="application-key-name"></a><span data-ttu-id="efef6-142">애플리케이션 키(이름)</span><span class="sxs-lookup"><span data-stu-id="efef6-142">Application key (name)</span></span>

<span data-ttu-id="efef6-143">호스트를 생성하는 동안 호스트 구성에서 [IHostingEnvironment.ApplicationName](xref:Microsoft.Extensions.Hosting.IHostingEnvironment.ApplicationName*) 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-143">The [IHostingEnvironment.ApplicationName](xref:Microsoft.Extensions.Hosting.IHostingEnvironment.ApplicationName*) property is set from host configuration during host construction.</span></span> <span data-ttu-id="efef6-144">값을 명시적으로 설정하려면 [HostDefaults.ApplicationKey](xref:Microsoft.Extensions.Hosting.HostDefaults.ApplicationKey)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-144">To set the value explicitly, use the [HostDefaults.ApplicationKey](xref:Microsoft.Extensions.Hosting.HostDefaults.ApplicationKey):</span></span>

<span data-ttu-id="efef6-145">**키**: applicationName</span><span class="sxs-lookup"><span data-stu-id="efef6-145">**Key**: applicationName</span></span>  
<span data-ttu-id="efef6-146">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="efef6-146">**Type**: *string*</span></span>  
<span data-ttu-id="efef6-147">**기본값**: 앱의 진입점을 포함하는 어셈블리의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-147">**Default**: The name of the assembly containing the app's entry point.</span></span>  
<span data-ttu-id="efef6-148">**설정 방법**: `HostBuilderContext.HostingEnvironment.ApplicationName`</span><span class="sxs-lookup"><span data-stu-id="efef6-148">**Set using**: `HostBuilderContext.HostingEnvironment.ApplicationName`</span></span>  
<span data-ttu-id="efef6-149">**환경 변수**: `<PREFIX_>APPLICATIONNAME`(`<PREFIX_>`는 [선택적이고 사용자 정의됨](#configurehostconfiguration))</span><span class="sxs-lookup"><span data-stu-id="efef6-149">**Environment variable**: `<PREFIX_>APPLICATIONNAME` (`<PREFIX_>` is [optional and user-defined](#configurehostconfiguration))</span></span>

### <a name="content-root"></a><span data-ttu-id="efef6-150">콘텐츠 루트</span><span class="sxs-lookup"><span data-stu-id="efef6-150">Content root</span></span>

<span data-ttu-id="efef6-151">이 설정은 호스트가 콘텐츠 파일을 검색하기 시작하는 지점을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-151">This setting determines where the host begins searching for content files.</span></span>

<span data-ttu-id="efef6-152">**키**: contentRoot</span><span class="sxs-lookup"><span data-stu-id="efef6-152">**Key**: contentRoot</span></span>  
<span data-ttu-id="efef6-153">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="efef6-153">**Type**: *string*</span></span>  
<span data-ttu-id="efef6-154">**기본값**: 앱 어셈블리가 있는 폴더가 기본값으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-154">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="efef6-155">**설정 방법**: `UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="efef6-155">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="efef6-156">**환경 변수**: `<PREFIX_>CONTENTROOT`(`<PREFIX_>`는 [선택적이고 사용자 정의됨](#configurehostconfiguration))</span><span class="sxs-lookup"><span data-stu-id="efef6-156">**Environment variable**: `<PREFIX_>CONTENTROOT` (`<PREFIX_>` is [optional and user-defined](#configurehostconfiguration))</span></span>

<span data-ttu-id="efef6-157">경로가 존재하지 않는 경우 호스트가 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-157">If the path doesn't exist, the host fails to start.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseContentRoot)]

### <a name="environment"></a><span data-ttu-id="efef6-158">환경</span><span class="sxs-lookup"><span data-stu-id="efef6-158">Environment</span></span>

<span data-ttu-id="efef6-159">앱의 [환경](xref:fundamentals/environments)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-159">Sets the app's [environment](xref:fundamentals/environments).</span></span>

<span data-ttu-id="efef6-160">**키**: environment</span><span class="sxs-lookup"><span data-stu-id="efef6-160">**Key**: environment</span></span>  
<span data-ttu-id="efef6-161">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="efef6-161">**Type**: *string*</span></span>  
<span data-ttu-id="efef6-162">**기본값**: Production</span><span class="sxs-lookup"><span data-stu-id="efef6-162">**Default**: Production</span></span>  
<span data-ttu-id="efef6-163">**설정 방법**: `UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="efef6-163">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="efef6-164">**환경 변수**: `<PREFIX_>ENVIRONMENT`(`<PREFIX_>`는 [선택적이고 사용자 정의됨](#configurehostconfiguration))</span><span class="sxs-lookup"><span data-stu-id="efef6-164">**Environment variable**: `<PREFIX_>ENVIRONMENT` (`<PREFIX_>` is [optional and user-defined](#configurehostconfiguration))</span></span>

<span data-ttu-id="efef6-165">환경은 어떠한 값으로도 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-165">The environment can be set to any value.</span></span> <span data-ttu-id="efef6-166">프레임워크에서 정의된 값은 `Development`, `Staging` 및 `Production`을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-166">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="efef6-167">값은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-167">Values aren't case sensitive.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseEnvironment)]

### <a name="configurehostconfiguration"></a><span data-ttu-id="efef6-168">ConfigureHostConfiguration</span><span class="sxs-lookup"><span data-stu-id="efef6-168">ConfigureHostConfiguration</span></span>

<span data-ttu-id="efef6-169">`ConfigureHostConfiguration`은 <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder>를 사용하여 호스트에 대한 <xref:Microsoft.Extensions.Configuration.IConfiguration>을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-169">`ConfigureHostConfiguration` uses an <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> to create an <xref:Microsoft.Extensions.Configuration.IConfiguration> for the host.</span></span> <span data-ttu-id="efef6-170">호스트 구성은 앱의 빌드 프로세스에 사용할 <xref:Microsoft.Extensions.Hosting.IHostingEnvironment>를 초기화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-170">The host configuration is used to initialize the <xref:Microsoft.Extensions.Hosting.IHostingEnvironment> for use in the app's build process.</span></span>

<span data-ttu-id="efef6-171">`ConfigureHostConfiguration` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-171">`ConfigureHostConfiguration` can be called multiple times with additive results.</span></span> <span data-ttu-id="efef6-172">호스트는 지정된 키에 마지막으로 값을 설정하는 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-172">The host uses whichever option sets a value last on a given key.</span></span>

<span data-ttu-id="efef6-173">호스트 구성이 자동으로 앱 구성([ConfigureAppConfiguration](#configureappconfiguration) 및 앱의 나머지 부분)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-173">Host configuration automatically flows to app configuration ([ConfigureAppConfiguration](#configureappconfiguration) and the rest of the app).</span></span>

<span data-ttu-id="efef6-174">기본적으로 공급자는 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-174">No providers are included by default.</span></span> <span data-ttu-id="efef6-175">다음을 포함하여 앱에 필요한 모든 구성 공급자를 `ConfigureHostConfiguration`에 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-175">You must explicitly specify whatever configuration providers the app requires in `ConfigureHostConfiguration`, including:</span></span>

* <span data-ttu-id="efef6-176">구성 파일(예: *hostsettings.json* 파일에서).</span><span class="sxs-lookup"><span data-stu-id="efef6-176">File configuration (for example, from a *hostsettings.json* file).</span></span>
* <span data-ttu-id="efef6-177">환경 변수 구성.</span><span class="sxs-lookup"><span data-stu-id="efef6-177">Environment variable configuration.</span></span>
* <span data-ttu-id="efef6-178">명령줄 인수 구성.</span><span class="sxs-lookup"><span data-stu-id="efef6-178">Command-line argument configuration.</span></span>
* <span data-ttu-id="efef6-179">기타 필수 구성 공급자.</span><span class="sxs-lookup"><span data-stu-id="efef6-179">Any other required configuration providers.</span></span>

<span data-ttu-id="efef6-180">호스트의 파일 구성은 `SetBasePath`를 사용하여 앱의 기본 경로를 지정한 후 [파일 구성 공급자](xref:fundamentals/configuration/index#file-configuration-provider) 중 하나를 호출하여 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-180">File configuration of the host is enabled by specifying the app's base path with `SetBasePath` followed by a call to one of the [file configuration providers](xref:fundamentals/configuration/index#file-configuration-provider).</span></span> <span data-ttu-id="efef6-181">샘플 앱은 JSON 파일인 *hostsettings.json*을 사용하고 <xref:Microsoft.Extensions.Configuration.JsonConfigurationExtensions.AddJsonFile*>을 호출하여 파일의 호스트 구성 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-181">The sample app uses a JSON file, *hostsettings.json*, and calls <xref:Microsoft.Extensions.Configuration.JsonConfigurationExtensions.AddJsonFile*> to consume the file's host configuration settings.</span></span>

<span data-ttu-id="efef6-182">[환경 변수 구성](xref:fundamentals/configuration/index#environment-variables-configuration-provider)을 추가하려면 호스트 작성기에서 <xref:Microsoft.Extensions.Configuration.EnvironmentVariablesExtensions.AddEnvironmentVariables*>를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-182">To add [environment variable configuration](xref:fundamentals/configuration/index#environment-variables-configuration-provider) of the host, call <xref:Microsoft.Extensions.Configuration.EnvironmentVariablesExtensions.AddEnvironmentVariables*> on the host builder.</span></span> <span data-ttu-id="efef6-183">`AddEnvironmentVariables`는 선택적 사용자 정의 접두사를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-183">`AddEnvironmentVariables` accepts an optional user-defined prefix.</span></span> <span data-ttu-id="efef6-184">샘플 앱은 `PREFIX_` 접두사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-184">The sample app uses a prefix of `PREFIX_`.</span></span> <span data-ttu-id="efef6-185">접두사는 환경 변수를 읽을 때 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-185">The prefix is removed when the environment variables are read.</span></span> <span data-ttu-id="efef6-186">샘플 앱의 호스트가 구성되면 `PREFIX_ENVIRONMENT`의 환경 변수 값이 `environment` 키에 대한 호스트 구성 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-186">When the sample app's host is configured, the environment variable value for `PREFIX_ENVIRONMENT` becomes the host configuration value for the `environment` key.</span></span>

<span data-ttu-id="efef6-187">[Visual Studio](https://www.visualstudio.com/)를 사용하거나 `dotnet run`을 통해 앱을 실행할 때 개발하는 동안에 환경 변수는 *Properties/launchSettings.json* 파일에 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-187">During development when using [Visual Studio](https://www.visualstudio.com/) or running an app with `dotnet run`, environment variables may be set in the *Properties/launchSettings.json* file.</span></span> <span data-ttu-id="efef6-188">[Visual Studio Code](https://code.visualstudio.com/)에서 환경 변수는 개발하는 동안에 *.vscode/launch.json* 파일에 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-188">In [Visual Studio Code](https://code.visualstudio.com/), environment variables may be set in the *.vscode/launch.json* file during development.</span></span> <span data-ttu-id="efef6-189">자세한 내용은 <xref:fundamentals/environments>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efef6-189">For more information, see <xref:fundamentals/environments>.</span></span>

<span data-ttu-id="efef6-190">[명령줄 구성](xref:fundamentals/configuration/index#command-line-configuration-provider)은 <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*>을 호출하여 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-190">[Command-line configuration](xref:fundamentals/configuration/index#command-line-configuration-provider) is added by calling <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*>.</span></span> <span data-ttu-id="efef6-191">명령줄 구성이 마지막으로 추가되어 명령줄 인수가 이전 구성 공급자가 제공한 구성을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-191">Command-line configuration is added last to permit command-line arguments to override configuration provided by the earlier configuration providers.</span></span>

<span data-ttu-id="efef6-192">*hostsettings.json*:</span><span class="sxs-lookup"><span data-stu-id="efef6-192">*hostsettings.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/hostsettings.json)]

<span data-ttu-id="efef6-193">[applicationName](#application-key-name) 및 [contentRoot](#content-root) 키를 사용하여 추가 구성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-193">Additional configuration can be provided with the [applicationName](#application-key-name) and [contentRoot](#content-root) keys.</span></span>

<span data-ttu-id="efef6-194">`ConfigureHostConfiguration`을 사용한 `HostBuilder` 구성 예:</span><span class="sxs-lookup"><span data-stu-id="efef6-194">Example `HostBuilder` configuration using `ConfigureHostConfiguration`:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureHostConfiguration)]

## <a name="configureappconfiguration"></a><span data-ttu-id="efef6-195">ConfigureAppConfiguration</span><span class="sxs-lookup"><span data-stu-id="efef6-195">ConfigureAppConfiguration</span></span>

<span data-ttu-id="efef6-196">앱 구성은 <xref:Microsoft.Extensions.Hosting.IHostBuilder> 구현에서 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>을 호출하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-196">App configuration is created by calling <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> on the <xref:Microsoft.Extensions.Hosting.IHostBuilder> implementation.</span></span> <span data-ttu-id="efef6-197">`ConfigureAppConfiguration`은 <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder>를 사용하여 앱에 대한 <xref:Microsoft.Extensions.Configuration.IConfiguration>을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-197">`ConfigureAppConfiguration` uses an <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> to create an <xref:Microsoft.Extensions.Configuration.IConfiguration> for the app.</span></span> <span data-ttu-id="efef6-198">`ConfigureAppConfiguration` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-198">`ConfigureAppConfiguration` can be called multiple times with additive results.</span></span> <span data-ttu-id="efef6-199">앱은 지정된 키에 마지막으로 값을 설정하는 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-199">The app uses whichever option sets a value last on a given key.</span></span> <span data-ttu-id="efef6-200">`ConfigureAppConfiguration`에 의해 생성된 구성은 다음 작업에 대한 [HostBuilderContext.Configuration](xref:Microsoft.Extensions.Hosting.HostBuilderContext.Configuration*) 및 <xref:Microsoft.Extensions.Hosting.IHost.Services*>에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-200">The configuration created by `ConfigureAppConfiguration` is available at [HostBuilderContext.Configuration](xref:Microsoft.Extensions.Hosting.HostBuilderContext.Configuration*) for subsequent operations and in <xref:Microsoft.Extensions.Hosting.IHost.Services*>.</span></span>

<span data-ttu-id="efef6-201">앱 구성은 [ConfigureHostConfiguration](#configurehostconfiguration)에서 제공하는 호스트 구성을 자동으로 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-201">App configuration automatically receives host configuration provided by [ConfigureHostConfiguration](#configurehostconfiguration).</span></span>

<span data-ttu-id="efef6-202">`ConfigureAppConfiguration`을 사용한 앱 구성 예:</span><span class="sxs-lookup"><span data-stu-id="efef6-202">Example app configuration using `ConfigureAppConfiguration`:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureAppConfiguration)]

<span data-ttu-id="efef6-203">*appsettings.json*:</span><span class="sxs-lookup"><span data-stu-id="efef6-203">*appsettings.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.json)]

<span data-ttu-id="efef6-204">*appsettings.Development.json*:</span><span class="sxs-lookup"><span data-stu-id="efef6-204">*appsettings.Development.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.Development.json)]

<span data-ttu-id="efef6-205">*appsettings.Production.json*:</span><span class="sxs-lookup"><span data-stu-id="efef6-205">*appsettings.Production.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.Production.json)]

<span data-ttu-id="efef6-206">출력 디렉터리로 설정 파일을 이동하려면, 설정 파일을 프로젝트 파일 내 [MSBuild 프로젝트 항목](/visualstudio/msbuild/common-msbuild-project-items)으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-206">To move settings files to the output directory, specify the settings files as [MSBuild project items](/visualstudio/msbuild/common-msbuild-project-items) in the project file.</span></span> <span data-ttu-id="efef6-207">샘플 앱은 다음 `<Content>` 항목과 함께 JSON 앱 설정 파일과 *hostsettings.json*을 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-207">The sample app moves its JSON app settings files and *hostsettings.json* with the following `<Content>` item:</span></span>

```xml
<ItemGroup>
  <Content Include="**\*.json" Exclude="bin\**\*;obj\**\*" CopyToOutputDirectory="PreserveNewest" />
</ItemGroup>
```

## <a name="configureservices"></a><span data-ttu-id="efef6-208">ConfigureServices</span><span class="sxs-lookup"><span data-stu-id="efef6-208">ConfigureServices</span></span>

<span data-ttu-id="efef6-209"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.ConfigureServices*>는 앱의 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에 서비스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-209"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.ConfigureServices*> adds services to the app's [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> <span data-ttu-id="efef6-210">`ConfigureServices` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-210">`ConfigureServices` can be called multiple times with additive results.</span></span>

<span data-ttu-id="efef6-211">호스티드 서비스는 <xref:Microsoft.Extensions.Hosting.IHostedService> 인터페이스를 구현하는 백그라운드 작업 논리가 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-211">A hosted service is a class with background task logic that implements the <xref:Microsoft.Extensions.Hosting.IHostedService> interface.</span></span> <span data-ttu-id="efef6-212">자세한 내용은 <xref:fundamentals/host/hosted-services>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efef6-212">For more information, see <xref:fundamentals/host/hosted-services>.</span></span>

<span data-ttu-id="efef6-213">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)은 `AddHostedService` 확장 메서드를 사용하여 수명 이벤트, `LifetimeEventsHostedService` 및 시간 제한 백그라운드 작업에 대한 서비스 `TimedHostedService`를 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-213">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) uses the `AddHostedService` extension method to add a service for lifetime events, `LifetimeEventsHostedService`, and a timed background task, `TimedHostedService`, to the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureServices)]

## <a name="configurelogging"></a><span data-ttu-id="efef6-214">ConfigureLogging</span><span class="sxs-lookup"><span data-stu-id="efef6-214">ConfigureLogging</span></span>

<span data-ttu-id="efef6-215"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.ConfigureLogging*>에는 제공된 <xref:Microsoft.Extensions.Logging.ILoggingBuilder>를 구성하는 대리자가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-215"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.ConfigureLogging*> adds a delegate for configuring the provided <xref:Microsoft.Extensions.Logging.ILoggingBuilder>.</span></span> <span data-ttu-id="efef6-216">`ConfigureLogging` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-216">`ConfigureLogging` may be called multiple times with additive results.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureLogging)]

### <a name="useconsolelifetime"></a><span data-ttu-id="efef6-217">UseConsoleLifetime</span><span class="sxs-lookup"><span data-stu-id="efef6-217">UseConsoleLifetime</span></span>

<span data-ttu-id="efef6-218"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseConsoleLifetime*>은 `Ctrl+C`/SIGINT 또는 SIGTERM을 수신 대기하고 <xref:Microsoft.Extensions.Hosting.IApplicationLifetime.StopApplication*>을 호출하여 종료 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-218"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseConsoleLifetime*> listens for `Ctrl+C`/SIGINT or SIGTERM and calls <xref:Microsoft.Extensions.Hosting.IApplicationLifetime.StopApplication*> to start the shutdown process.</span></span> <span data-ttu-id="efef6-219">`UseConsoleLifetime`은 [RunAsync](#runasync) 및 [WaitForShutdownAsync](#waitforshutdownasync)와 같은 확장의 차단을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-219">`UseConsoleLifetime` unblocks extensions such as [RunAsync](#runasync) and [WaitForShutdownAsync](#waitforshutdownasync).</span></span> <span data-ttu-id="efef6-220"><xref:Microsoft.Extensions.Hosting.Internal.ConsoleLifetime>은 기본 수명 구현으로 미리 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-220"><xref:Microsoft.Extensions.Hosting.Internal.ConsoleLifetime> is pre-registered as the default lifetime implementation.</span></span> <span data-ttu-id="efef6-221">등록된 마지막 수명이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-221">The last lifetime registered is used.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseConsoleLifetime)]

## <a name="container-configuration"></a><span data-ttu-id="efef6-222">컨테이너 구성</span><span class="sxs-lookup"><span data-stu-id="efef6-222">Container configuration</span></span>

<span data-ttu-id="efef6-223">호스트는 다른 컨테이너 연결을 지원하기 위해 <xref:Microsoft.Extensions.DependencyInjection.IServiceProviderFactory`1>를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-223">To support plugging in other containers, the host can accept an <xref:Microsoft.Extensions.DependencyInjection.IServiceProviderFactory`1>.</span></span> <span data-ttu-id="efef6-224">팩터리 제공은 DI 컨테이너 등록의 일부가 아니지만 구체적 DI 컨테이너를 만드는 데 사용되는 내장 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-224">Providing a factory isn't part of the DI container registration but is instead a host intrinsic used to create the concrete DI container.</span></span> <span data-ttu-id="efef6-225">[UseServiceProviderFactory(IServiceProviderFactory&lt;TContainerBuilder&gt;)](xref:Microsoft.Extensions.Hosting.HostBuilder.UseServiceProviderFactory*)는 앱의 서비스 공급자를 만드는 데 사용되는 기본 팩터리를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-225">[UseServiceProviderFactory(IServiceProviderFactory&lt;TContainerBuilder&gt;)](xref:Microsoft.Extensions.Hosting.HostBuilder.UseServiceProviderFactory*) overrides the default factory used to create the app's service provider.</span></span>

<span data-ttu-id="efef6-226">사용자 지정 컨테이너 구성은 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureContainer*> 메서드로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-226">Custom container configuration is managed by the <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureContainer*> method.</span></span> <span data-ttu-id="efef6-227">`ConfigureContainer`는 기본 호스트 API 위에 컨테이너를 구성하기 위한 강력한 형식의 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-227">`ConfigureContainer` provides a strongly-typed experience for configuring the container on top of the underlying host API.</span></span> <span data-ttu-id="efef6-228">`ConfigureContainer` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-228">`ConfigureContainer` can be called multiple times with additive results.</span></span>

<span data-ttu-id="efef6-229">앱에 대한 서비스 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-229">Create a service container for the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/ServiceContainer.cs)]

<span data-ttu-id="efef6-230">서비스 컨테이너 팩터리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-230">Provide a service container factory:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/ServiceContainerFactory.cs)]

<span data-ttu-id="efef6-231">팩터리를 사용하고 앱에 대 한 사용자 지정 서비스 컨테이너를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-231">Use the factory and configure the custom service container for the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ContainerConfiguration)]

## <a name="extensibility"></a><span data-ttu-id="efef6-232">확장성</span><span class="sxs-lookup"><span data-stu-id="efef6-232">Extensibility</span></span>

<span data-ttu-id="efef6-233">`IHostBuilder`에서 확장 메서드를 사용하여 호스트 확장성이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-233">Host extensibility is performed with extension methods on `IHostBuilder`.</span></span> <span data-ttu-id="efef6-234">다음 예제는 <xref:fundamentals/host/hosted-services>에 설명된 [TimedHostedService](xref:fundamentals/host/hosted-services#timed-background-tasks) 예제를 사용하여 확장 메서드가 `IHostBuilder` 구현을 확장하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-234">The following example shows how an extension method extends an `IHostBuilder` implementation with the [TimedHostedService](xref:fundamentals/host/hosted-services#timed-background-tasks) example demonstrated in <xref:fundamentals/host/hosted-services>.</span></span>

```csharp
var host = new HostBuilder()
    .UseHostedService<TimedHostedService>()
    .Build();

await host.StartAsync();
```

<span data-ttu-id="efef6-235">앱은 `UseHostedService` 확장 메서드를 설정하여 `T`에서 전달되는 호스티드 서비스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-235">An app establishes the `UseHostedService` extension method to register the hosted service passed in `T`:</span></span>

```csharp
using System;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;

public static class Extensions
{
    public static IHostBuilder UseHostedService<T>(this IHostBuilder hostBuilder)
        where T : class, IHostedService, IDisposable
    {
        return hostBuilder.ConfigureServices(services =>
            services.AddHostedService<T>());
    }
}
```

## <a name="manage-the-host"></a><span data-ttu-id="efef6-236">호스트 관리</span><span class="sxs-lookup"><span data-stu-id="efef6-236">Manage the host</span></span>

<span data-ttu-id="efef6-237"><xref:Microsoft.Extensions.Hosting.IHost> 구현은 서비스 컨테이너에 등록된 `IHostedService` 구현의 시작 및 중지를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-237">The <xref:Microsoft.Extensions.Hosting.IHost> implementation is responsible for starting and stopping the `IHostedService` implementations that are registered in the service container.</span></span>

### <a name="run"></a><span data-ttu-id="efef6-238">실행</span><span class="sxs-lookup"><span data-stu-id="efef6-238">Run</span></span>

<span data-ttu-id="efef6-239"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.Run*>은 앱을 시작하고 호스트가 종료될 때까지 호출 스레드를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-239"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.Run*> runs the app and blocks the calling thread until the host is shut down:</span></span>

```csharp
public class Program
{
    public void Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        host.Run();
    }
}
```

### <a name="runasync"></a><span data-ttu-id="efef6-240">RunAsync</span><span class="sxs-lookup"><span data-stu-id="efef6-240">RunAsync</span></span>

<span data-ttu-id="efef6-241"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.RunAsync*>는 앱을 실행하고 취소 토큰 또는 종료가 트리거될 때 완료되는 `Task`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-241"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.RunAsync*> runs the app and returns a `Task` that completes when the cancellation token or shutdown is triggered:</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        await host.RunAsync();
    }
}
```

### <a name="runconsoleasync"></a><span data-ttu-id="efef6-242">RunConsoleAsync</span><span class="sxs-lookup"><span data-stu-id="efef6-242">RunConsoleAsync</span></span>

<span data-ttu-id="efef6-243"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.RunConsoleAsync*>는 콘솔 지원을 구현하고, 호스트를 빌드 및 시작하며, `Ctrl+C`/SIGINT 또는 SIGTERM이 종료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-243"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.RunConsoleAsync*> enables console support, builds and starts the host, and waits for `Ctrl+C`/SIGINT or SIGTERM to shut down.</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var hostBuilder = new HostBuilder();

        await hostBuilder.RunConsoleAsync();
    }
}
```

### <a name="start-and-stopasync"></a><span data-ttu-id="efef6-244">Start 및 StopAsync</span><span class="sxs-lookup"><span data-stu-id="efef6-244">Start and StopAsync</span></span>

<span data-ttu-id="efef6-245"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.Start*>는 호스트를 동기적으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-245"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.Start*> starts the host synchronously.</span></span>

<span data-ttu-id="efef6-246"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.StopAsync*>는 지정된 시간 제한 내에서 호스트를 중지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-246"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.StopAsync*> attempts to stop the host within the provided timeout.</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            host.Start();

            await host.StopAsync(TimeSpan.FromSeconds(5));
        }
    }
}
```

### <a name="startasync-and-stopasync"></a><span data-ttu-id="efef6-247">StartAsync 및 StopAsync</span><span class="sxs-lookup"><span data-stu-id="efef6-247">StartAsync and StopAsync</span></span>

<span data-ttu-id="efef6-248"><xref:Microsoft.Extensions.Hosting.IHost.StartAsync*>가 서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-248"><xref:Microsoft.Extensions.Hosting.IHost.StartAsync*> starts the app.</span></span>

<span data-ttu-id="efef6-249"><xref:Microsoft.Extensions.Hosting.IHost.StopAsync*>가 서버를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-249"><xref:Microsoft.Extensions.Hosting.IHost.StopAsync*> stops the app.</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            await host.StartAsync();

            await host.StopAsync();
        }
    }
}
```

### <a name="waitforshutdown"></a><span data-ttu-id="efef6-250">WaitForShutdown</span><span class="sxs-lookup"><span data-stu-id="efef6-250">WaitForShutdown</span></span>

<span data-ttu-id="efef6-251"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.WaitForShutdown*>은 <xref:Microsoft.Extensions.Hosting.Internal.ConsoleLifetime>(`Ctrl+C`/SIGINT 또는 SIGTERM 수신 대기)과 같이 <xref:Microsoft.Extensions.Hosting.IHostLifetime>을 통해 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-251"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.WaitForShutdown*> is triggered via the <xref:Microsoft.Extensions.Hosting.IHostLifetime>, such as <xref:Microsoft.Extensions.Hosting.Internal.ConsoleLifetime> (listens for `Ctrl+C`/SIGINT or SIGTERM).</span></span> <span data-ttu-id="efef6-252">`WaitForShutdown`은 <xref:Microsoft.Extensions.Hosting.IHost.StopAsync*>을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-252">`WaitForShutdown` calls <xref:Microsoft.Extensions.Hosting.IHost.StopAsync*>.</span></span>

```csharp
public class Program
{
    public void Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            host.Start();

            host.WaitForShutdown();
        }
    }
}
```

### <a name="waitforshutdownasync"></a><span data-ttu-id="efef6-253">WaitForShutdownAsync</span><span class="sxs-lookup"><span data-stu-id="efef6-253">WaitForShutdownAsync</span></span>

<span data-ttu-id="efef6-254"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.WaitForShutdownAsync*>는 지정된 토큰을 통해 종료가 트리거될 때 완료되는 `Task`를 반환하고 <xref:Microsoft.Extensions.Hosting.IHost.StopAsync*>를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-254"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.WaitForShutdownAsync*> returns a `Task` that completes when shutdown is triggered via the given token and calls <xref:Microsoft.Extensions.Hosting.IHost.StopAsync*>.</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            await host.StartAsync();

            await host.WaitForShutdownAsync();
        }

    }
}
```

### <a name="external-control"></a><span data-ttu-id="efef6-255">외부 제어</span><span class="sxs-lookup"><span data-stu-id="efef6-255">External control</span></span>

<span data-ttu-id="efef6-256">외부에서 호출할 수 있는 메서드를 사용하여 호스트의 외부 제어를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-256">External control of the host can be achieved using methods that can be called externally:</span></span>

```csharp
public class Program
{
    private IHost _host;

    public Program()
    {
        _host = new HostBuilder()
            .Build();
    }

    public async Task StartAsync()
    {
        _host.StartAsync();
    }

    public async Task StopAsync()
    {
        using (_host)
        {
            await _host.StopAsync(TimeSpan.FromSeconds(5));
        }
    }
}
```

<span data-ttu-id="efef6-257"><xref:Microsoft.Extensions.Hosting.IHostLifetime.WaitForStartAsync*>는 <xref:Microsoft.Extensions.Hosting.IHost.StartAsync*>의 시작 시 호출되고, 완료될 때까지 기다린 후 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-257"><xref:Microsoft.Extensions.Hosting.IHostLifetime.WaitForStartAsync*> is called at the start of <xref:Microsoft.Extensions.Hosting.IHost.StartAsync*>, which waits until it's complete before continuing.</span></span> <span data-ttu-id="efef6-258">이는 외부 이벤트에서 신호를 보낼 때까지 시작을 지연시키는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-258">This can be used to delay startup until signaled by an external event.</span></span>

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="efef6-259">IHostingEnvironment 인터페이스</span><span class="sxs-lookup"><span data-stu-id="efef6-259">IHostingEnvironment interface</span></span>

<span data-ttu-id="efef6-260"><xref:Microsoft.Extensions.Hosting.IHostingEnvironment>는 앱의 호스팅 환경에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-260"><xref:Microsoft.Extensions.Hosting.IHostingEnvironment> provides information about the app's hosting environment.</span></span> <span data-ttu-id="efef6-261">해당 속성 및 확장 메서드를 사용하기 위해 [생성자 주입](xref:fundamentals/dependency-injection)을 사용하여 `IHostingEnvironment`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-261">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

```csharp
public class MyClass
{
    private readonly IHostingEnvironment _env;

    public MyClass(IHostingEnvironment env)
    {
        _env = env;
    }

    public void DoSomething()
    {
        var environmentName = _env.EnvironmentName;
    }
}
```

<span data-ttu-id="efef6-262">자세한 내용은 <xref:fundamentals/environments>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efef6-262">For more information, see <xref:fundamentals/environments>.</span></span>

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="efef6-263">IApplicationLifetime 인터페이스</span><span class="sxs-lookup"><span data-stu-id="efef6-263">IApplicationLifetime interface</span></span>

<span data-ttu-id="efef6-264"><xref:Microsoft.Extensions.Hosting.IApplicationLifetime>은 점진적인 종료 요청을 비롯한 사후 시작 및 종료 작업을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-264"><xref:Microsoft.Extensions.Hosting.IApplicationLifetime> allows for post-startup and shutdown activities, including graceful shutdown requests.</span></span> <span data-ttu-id="efef6-265">인터페이스에서 세 가지 속성은 취소 토큰으로, 시작 및 종료 이벤트를 정의하는 `Action` 메서드를 등록하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-265">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span>

| <span data-ttu-id="efef6-266">취소 토큰</span><span class="sxs-lookup"><span data-stu-id="efef6-266">Cancellation Token</span></span> | <span data-ttu-id="efef6-267">트리거되는 경우:</span><span class="sxs-lookup"><span data-stu-id="efef6-267">Triggered when&#8230;</span></span> |
| ------------------ | --------------------- |
| <xref:Microsoft.Extensions.Hosting.IApplicationLifetime.ApplicationStarted*> | <span data-ttu-id="efef6-268">호스트가 완벽하게 시작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-268">The host has fully started.</span></span> |
| <xref:Microsoft.Extensions.Hosting.IApplicationLifetime.ApplicationStopped*> | <span data-ttu-id="efef6-269">호스트가 정상적으로 종료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-269">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="efef6-270">모든 요청이 처리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-270">All requests should be processed.</span></span> <span data-ttu-id="efef6-271">종료는 이 이벤트가 완료될 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-271">Shutdown blocks until this event completes.</span></span> |
| <xref:Microsoft.Extensions.Hosting.IApplicationLifetime.ApplicationStopping*> | <span data-ttu-id="efef6-272">호스트가 정상적으로 종료되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-272">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="efef6-273">요청은 계속 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-273">Requests may still be processing.</span></span> <span data-ttu-id="efef6-274">종료는 이 이벤트가 완료될 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-274">Shutdown blocks until this event completes.</span></span> |

<span data-ttu-id="efef6-275">클래스에 대한 `IApplicationLifetime` 서비스 생성자 주입을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-275">Constructor-inject the `IApplicationLifetime` service into any class.</span></span> <span data-ttu-id="efef6-276">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)은 `LifetimeEventsHostedService` 클래스(`IHostedService` 구현)에 대한 생성자 주입을 사용하여 이벤트를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-276">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) uses constructor injection into a `LifetimeEventsHostedService` class (an `IHostedService` implementation) to register the events.</span></span>

<span data-ttu-id="efef6-277">*LifetimeEventsHostedService.cs*:</span><span class="sxs-lookup"><span data-stu-id="efef6-277">*LifetimeEventsHostedService.cs*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/LifetimeEventsHostedService.cs?name=snippet1)]

<span data-ttu-id="efef6-278"><xref:Microsoft.Extensions.Hosting.IApplicationLifetime.StopApplication*>은 앱의 종료를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-278"><xref:Microsoft.Extensions.Hosting.IApplicationLifetime.StopApplication*> requests termination of the app.</span></span> <span data-ttu-id="efef6-279">다음 클래스에서는 `StopApplication`을 사용하여 해당 클래스의 `Shutdown` 메서드를 호출하는 경우 앱을 정상 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="efef6-279">The following class uses `StopApplication` to gracefully shut down an app when the class's `Shutdown` method is called:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="efef6-280">추가 자료</span><span class="sxs-lookup"><span data-stu-id="efef6-280">Additional resources</span></span>

* <xref:fundamentals/host/hosted-services>
* [<span data-ttu-id="efef6-281">GitHub의 호스팅 리포지토리 샘플</span><span class="sxs-lookup"><span data-stu-id="efef6-281">Hosting repo samples on GitHub</span></span>](https://github.com/aspnet/Hosting/tree/release/2.1/samples)
