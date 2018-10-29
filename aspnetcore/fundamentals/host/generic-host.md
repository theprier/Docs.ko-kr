---
title: .NET 일반 호스트
author: guardrex
description: 앱 시작 및 수명 관리를 담당하는 .NET의 일반 호스트에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 05/16/2018
uid: fundamentals/host/generic-host
ms.openlocfilehash: e5f91ed64b7f8402dfe938f0fa8a0d94755d15c6
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207721"
---
# <a name="net-generic-host"></a><span data-ttu-id="b194f-103">.NET 일반 호스트</span><span class="sxs-lookup"><span data-stu-id="b194f-103">.NET Generic Host</span></span>

<span data-ttu-id="b194f-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="b194f-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="b194f-105">.NET Core 앱은 *호스트*를 구성 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-105">.NET Core apps configure and launch a *host*.</span></span> <span data-ttu-id="b194f-106">호스트는 앱 시작 및 수명 관리를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-106">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="b194f-107">이 항목에서는 HTTP 요청을 처리하지 않는 앱을 호스팅하는 데 유용한 ASP.NET Core 일반 호스트([HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder))를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-107">This topic covers the ASP.NET Core Generic Host ([HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder)), which is useful for hosting apps that don't process HTTP requests.</span></span> <span data-ttu-id="b194f-108">웹 호스트([WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder))에 대한 자세한 내용은 <xref:fundamentals/host/web-host>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b194f-108">For coverage of the Web Host ([WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)), see <xref:fundamentals/host/web-host>.</span></span>

<span data-ttu-id="b194f-109">일반 호스트의 목표는 웹 호스트 API에서 HTTP 파이프라인을 분리하여 호스트 시나리오의 더 광범위한 배열을 구현하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-109">The goal of the Generic Host is to decouple the HTTP pipeline from the Web Host API to enable a wider array of host scenarios.</span></span> <span data-ttu-id="b194f-110">일반 호스트에 기반을 둔 메시징, 백그라운드 작업 및 기타 HTTP 이외 워크로드는 구성, 종속성 주입(DI) 및 로깅과 같은 교차 편집 기능에서 이점을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-110">Messaging, background tasks, and other non-HTTP workloads based on the Generic Host benefit from cross-cutting capabilities, such as configuration, dependency injection (DI), and logging.</span></span>

<span data-ttu-id="b194f-111">일반 호스트는 ASP.NET Core 2.1의 새로운 기능이며 웹 호스팅 시나리오에 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-111">The Generic Host is new in ASP.NET Core 2.1 and isn't suitable for web hosting scenarios.</span></span> <span data-ttu-id="b194f-112">웹 호스팅 시나리오의 경우 [웹 호스트](xref:fundamentals/host/web-host)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b194f-112">For web hosting scenarios, use the [Web Host](xref:fundamentals/host/web-host).</span></span> <span data-ttu-id="b194f-113">일반 호스트는 향후 릴리스에서 웹 호스트를 대체하기 위해 개발 중이며, HTTP 및 HTTP 이외 시나리오에서 기본 호스트 API 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-113">The Generic Host is under development to replace the Web Host in a future release and act as the primary host API in both HTTP and non-HTTP scenarios.</span></span>

<span data-ttu-id="b194f-114">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="b194f-114">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="b194f-115">[Visual Studio Code](https://code.visualstudio.com/)에서 샘플 앱을 실행할 때는 *외부 또는 통합 터미널*을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b194f-115">When running the sample app in [Visual Studio Code](https://code.visualstudio.com/), use an *external or integrated terminal*.</span></span> <span data-ttu-id="b194f-116">`internalConsole`에서는 샘플을 실행하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b194f-116">Don't run the sample in an `internalConsole`.</span></span>

<span data-ttu-id="b194f-117">Visual Studio Code에서 콘솔을 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="b194f-117">To set the console in Visual Studio Code:</span></span>

1. <span data-ttu-id="b194f-118">*.vscode/launch.json* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-118">Open the *.vscode/launch.json* file.</span></span>
1. <span data-ttu-id="b194f-119">**.NET Core 시작(콘솔)** 구성에서 **콘솔** 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-119">In the **.NET Core Launch (console)** configuration, locate the **console** entry.</span></span> <span data-ttu-id="b194f-120">값을 `externalTerminal` 또는 `integratedTerminal` 중 하나로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-120">Set the value to either `externalTerminal` or `integratedTerminal`.</span></span>

## <a name="introduction"></a><span data-ttu-id="b194f-121">소개</span><span class="sxs-lookup"><span data-stu-id="b194f-121">Introduction</span></span>

<span data-ttu-id="b194f-122">일반 호스트 라이브러리는 [Microsoft.Extensions.Hosting 네임스페이스](/dotnet/api/microsoft.extensions.hosting)에서 사용할 수 있으며, [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting/)에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-122">The Generic Host library is available in the [Microsoft.Extensions.Hosting namespace](/dotnet/api/microsoft.extensions.hosting) and provided by the [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting/) package.</span></span> <span data-ttu-id="b194f-123">`Microsoft.Extensions.Hosting` 패키지는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)(ASP.NET Core 2.1 이상)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-123">The `Microsoft.Extensions.Hosting` package is included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) (ASP.NET Core 2.1 or later).</span></span>

<span data-ttu-id="b194f-124">[IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice)는 코드 실행 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-124">[IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) is the entry point to code execution.</span></span> <span data-ttu-id="b194f-125">각 `IHostedService` 구현은 [ConfigureServices의 서비스 등록](#configureservices) 순서대로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-125">Each `IHostedService` implementation is executed in the order of [service registration in ConfigureServices](#configureservices).</span></span> <span data-ttu-id="b194f-126">[StartAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.startasync)는 호스트가 시작될 때 각 `IHostedService`에서 호출되고, [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.stopasync)는 호스트가 점진적으로 종료될 때 등록 순서의 역순으로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-126">[StartAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.startasync) is called on each `IHostedService` when the host starts, and [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.stopasync) is called in reverse registration order when the host shuts down gracefully.</span></span>

## <a name="set-up-a-host"></a><span data-ttu-id="b194f-127">호스트 설정</span><span class="sxs-lookup"><span data-stu-id="b194f-127">Set up a host</span></span>

<span data-ttu-id="b194f-128">[IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder)는 라이브러리 및 앱이 호스트를 초기화, 빌드 및 실행 하는 데 사용하는 주 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-128">[IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) is the main component that libraries and apps use to initialize, build, and run the host:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_HostBuilder)]

## <a name="default-services"></a><span data-ttu-id="b194f-129">기본 서비스</span><span class="sxs-lookup"><span data-stu-id="b194f-129">Default services</span></span>

<span data-ttu-id="b194f-130">호스트 초기화 중에 다음 서비스가 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-130">The following services are registered during host initialization:</span></span>

* <span data-ttu-id="b194f-131">[환경](xref:fundamentals/environments)(<xref:Microsoft.Extensions.Hosting.IHostingEnvironment>)</span><span class="sxs-lookup"><span data-stu-id="b194f-131">[Environment](xref:fundamentals/environments) (<xref:Microsoft.Extensions.Hosting.IHostingEnvironment>)</span></span>
* <xref:Microsoft.Extensions.Hosting.HostBuilderContext>
* <span data-ttu-id="b194f-132">[구성](xref:fundamentals/configuration/index)(<xref:Microsoft.Extensions.Configuration.IConfiguration>)</span><span class="sxs-lookup"><span data-stu-id="b194f-132">[Configuration](xref:fundamentals/configuration/index) (<xref:Microsoft.Extensions.Configuration.IConfiguration>)</span></span>
* <span data-ttu-id="b194f-133"><xref:Microsoft.Extensions.Hosting.IApplicationLifetime> (<xref:Microsoft.Extensions.Hosting.Internal.ApplicationLifetime>)</span><span class="sxs-lookup"><span data-stu-id="b194f-133"><xref:Microsoft.Extensions.Hosting.IApplicationLifetime> (<xref:Microsoft.Extensions.Hosting.Internal.ApplicationLifetime>)</span></span>
* <span data-ttu-id="b194f-134"><xref:Microsoft.Extensions.Hosting.IHostLifetime> (<xref:Microsoft.Extensions.Hosting.Internal.ConsoleLifetime>)</span><span class="sxs-lookup"><span data-stu-id="b194f-134"><xref:Microsoft.Extensions.Hosting.IHostLifetime> (<xref:Microsoft.Extensions.Hosting.Internal.ConsoleLifetime>)</span></span>
* <xref:Microsoft.Extensions.Hosting.IHost>
* <span data-ttu-id="b194f-135">[옵션](xref:fundamentals/configuration/options)(<xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptions*>)</span><span class="sxs-lookup"><span data-stu-id="b194f-135">[Options](xref:fundamentals/configuration/options) (<xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptions*>)</span></span>
* <span data-ttu-id="b194f-136">[로깅](xref:fundamentals/logging/index)(<xref:Microsoft.Extensions.DependencyInjection.LoggingServiceCollectionExtensions.AddLogging*>)</span><span class="sxs-lookup"><span data-stu-id="b194f-136">[Logging](xref:fundamentals/logging/index) (<xref:Microsoft.Extensions.DependencyInjection.LoggingServiceCollectionExtensions.AddLogging*>)</span></span>

## <a name="host-configuration"></a><span data-ttu-id="b194f-137">호스트 구성</span><span class="sxs-lookup"><span data-stu-id="b194f-137">Host configuration</span></span>

<span data-ttu-id="b194f-138">[HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder)는 호스트 구성 값을 설정하기 위해 다음 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-138">[HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder) relies on the following approaches to set the host configuration values:</span></span>

* <span data-ttu-id="b194f-139">구성 작성기</span><span class="sxs-lookup"><span data-stu-id="b194f-139">Configuration builder</span></span>
* <span data-ttu-id="b194f-140">확장 메서드 구성</span><span class="sxs-lookup"><span data-stu-id="b194f-140">Extension method configuration</span></span>

### <a name="configuration-builder"></a><span data-ttu-id="b194f-141">구성 작성기</span><span class="sxs-lookup"><span data-stu-id="b194f-141">Configuration builder</span></span>

<span data-ttu-id="b194f-142">호스트 작성기 구성은 [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) 구현에서 [ConfigureHostConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configurehostconfiguration)을 호출하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-142">Host builder configuration is created by calling [ConfigureHostConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configurehostconfiguration) on the [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) implementation.</span></span> <span data-ttu-id="b194f-143">`ConfigureHostConfiguration`은 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder)를 사용하여 호스트의 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-143">`ConfigureHostConfiguration` uses an [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder) to create an [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) for the host.</span></span> <span data-ttu-id="b194f-144">구성 작성기는 앱의 빌드 프로세스에서 사용할 [IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment)를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-144">The configuration builder initializes the [IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment) for use in the app's build process.</span></span>

<span data-ttu-id="b194f-145">환경 변수 구성은 기본적으로 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-145">Environment variable configuration isn't added by default.</span></span> <span data-ttu-id="b194f-146">호스트 빌더에서 [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables)를 호출하여 환경 변수의 호스트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-146">Call [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables) on the host builder to configure the host from environment variables.</span></span> <span data-ttu-id="b194f-147">`AddEnvironmentVariables`는 선택적 사용자 정의 접두사를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-147">`AddEnvironmentVariables` accepts an optional user-defined prefix.</span></span> <span data-ttu-id="b194f-148">샘플 앱은 `PREFIX_` 접두사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-148">The sample app uses a prefix of `PREFIX_`.</span></span> <span data-ttu-id="b194f-149">접두사는 환경 변수를 읽을 때 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-149">The prefix is removed when the environment variables are read.</span></span> <span data-ttu-id="b194f-150">샘플 앱의 호스트가 구성되면 `PREFIX_ENVIRONMENT`의 환경 변수 값이 `environment` 키에 대한 호스트 구성 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-150">When the sample app's host is configured, the environment variable value for `PREFIX_ENVIRONMENT` becomes the host configuration value for the `environment` key.</span></span>

<span data-ttu-id="b194f-151">[Visual Studio](https://www.visualstudio.com/)를 사용하거나 `dotnet run`을 통해 앱을 실행할 때 개발하는 동안에 환경 변수는 *Properties/launchSettings.json* 파일에 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-151">During development when using [Visual Studio](https://www.visualstudio.com/) or running an app with `dotnet run`, environment variables may be set in the *Properties/launchSettings.json* file.</span></span> <span data-ttu-id="b194f-152">[Visual Studio Code](https://code.visualstudio.com/)에서 환경 변수는 개발하는 동안에 *.vscode/launch.json* 파일에 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-152">In [Visual Studio Code](https://code.visualstudio.com/), environment variables may be set in the *.vscode/launch.json* file during development.</span></span> <span data-ttu-id="b194f-153">자세한 내용은 <xref:fundamentals/environments>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b194f-153">For more information, see <xref:fundamentals/environments>.</span></span>

<span data-ttu-id="b194f-154">`ConfigureHostConfiguration` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-154">`ConfigureHostConfiguration` can be called multiple times with additive results.</span></span> <span data-ttu-id="b194f-155">호스트는 마지막에 값을 설정한 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-155">The host uses whichever option sets a value last.</span></span>

<span data-ttu-id="b194f-156">*hostsettings.json*:</span><span class="sxs-lookup"><span data-stu-id="b194f-156">*hostsettings.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/hostsettings.json)]

<span data-ttu-id="b194f-157">`ConfigureHostConfiguration`을 사용한 `HostBuilder` 구성 예:</span><span class="sxs-lookup"><span data-stu-id="b194f-157">Example `HostBuilder` configuration using `ConfigureHostConfiguration`:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureHostConfiguration)]

> [!NOTE]
> <span data-ttu-id="b194f-158">[AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) 확장 메서드는 현재 [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection)에서 반환되는 구성 섹션을 구문 분석할 수 없습니다(예: `.AddConfiguration(Configuration.GetSection("section"))`).</span><span class="sxs-lookup"><span data-stu-id="b194f-158">The [AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) extension method isn't currently capable of parsing a configuration section returned by [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection) (for example, `.AddConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="b194f-159">`GetSection` 메서드는 요청된 섹션에 대한 구성 키를 필터링하지만 키에 있는 섹션 이름을 그대로 둡니다(예: `section:environment`).</span><span class="sxs-lookup"><span data-stu-id="b194f-159">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:environment`).</span></span> <span data-ttu-id="b194f-160">`AddConfiguration` 메서드에서는 키가 `HostBuilder` 키와 일치해야 합니다(예: `environment`).</span><span class="sxs-lookup"><span data-stu-id="b194f-160">The `AddConfiguration` method expects the keys to match the `HostBuilder` keys (for example, `environment`).</span></span> <span data-ttu-id="b194f-161">키에서 섹션 이름의 존재는 섹션 값으로 호스트를 구성할 수 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-161">The presence of the section name on the keys prevents the section's values from configuring the host.</span></span> <span data-ttu-id="b194f-162">이 문제는 향후 릴리스에서 해결될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-162">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="b194f-163">자세한 내용 및 해결 방법은 [전체 키를 사용하여 WebHostBuilder.UseConfiguration에 구성 섹션을 전달](https://github.com/aspnet/Hosting/issues/839)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b194f-163">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>

### <a name="extension-method-configuration"></a><span data-ttu-id="b194f-164">확장 메서드 구성</span><span class="sxs-lookup"><span data-stu-id="b194f-164">Extension method configuration</span></span>

<span data-ttu-id="b194f-165">확장 메서드는 콘텐츠 루트 및 환경을 구성하기 위해 `IHostBuilder` 구현에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-165">Extension methods are called on the `IHostBuilder` implementation to configure the content root and the environment.</span></span>

#### <a name="application-key-name"></a><span data-ttu-id="b194f-166">응용 프로그램 키(이름)</span><span class="sxs-lookup"><span data-stu-id="b194f-166">Application Key (Name)</span></span>

<span data-ttu-id="b194f-167">호스트를 생성하는 동안 호스트 구성에서 [IHostingEnvironment.ApplicationName](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment.applicationname) 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-167">The [IHostingEnvironment.ApplicationName](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment.applicationname) property is set from host configuration during host construction.</span></span> <span data-ttu-id="b194f-168">값을 명시적으로 설정하려면 [HostDefaults.ApplicationKey](/dotnet/api/microsoft.extensions.hosting.hostdefaults.applicationkey)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-168">To set the value explicitly, use the [HostDefaults.ApplicationKey](/dotnet/api/microsoft.extensions.hosting.hostdefaults.applicationkey):</span></span>

<span data-ttu-id="b194f-169">**키**: applicationName</span><span class="sxs-lookup"><span data-stu-id="b194f-169">**Key**: applicationName</span></span>  
<span data-ttu-id="b194f-170">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="b194f-170">**Type**: *string*</span></span>  
<span data-ttu-id="b194f-171">**기본값**: 앱의 진입점을 포함하는 어셈블리의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-171">**Default**: The name of the assembly containing the app's entry point.</span></span>  
<span data-ttu-id="b194f-172">**설정 방법**: `HostBuilderContext.HostingEnvironment.ApplicationName`</span><span class="sxs-lookup"><span data-stu-id="b194f-172">**Set using**: `HostBuilderContext.HostingEnvironment.ApplicationName`</span></span>  
<span data-ttu-id="b194f-173">**환경 변수**: `<PREFIX_>APPLICATIONNAME`(`<PREFIX_>`는 [선택적이고 사용자 정의됨](#configuration-builder))</span><span class="sxs-lookup"><span data-stu-id="b194f-173">**Environment variable**: `<PREFIX_>APPLICATIONNAME` (`<PREFIX_>` is [optional and user-defined](#configuration-builder))</span></span>

```csharp
var host = new HostBuilder()
    .ConfigureAppConfiguration((hostContext, configApp) =>
    {
        hostContext.HostingEnvironment.ApplicationName = "CustomApplicationName";
    })
```

#### <a name="content-root"></a><span data-ttu-id="b194f-174">콘텐츠 루트</span><span class="sxs-lookup"><span data-stu-id="b194f-174">Content Root</span></span>

<span data-ttu-id="b194f-175">이 설정은 호스트가 콘텐츠 파일을 검색하기 시작하는 지점을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-175">This setting determines where the host begins searching for content files.</span></span>

<span data-ttu-id="b194f-176">**키**: contentRoot</span><span class="sxs-lookup"><span data-stu-id="b194f-176">**Key**: contentRoot</span></span>  
<span data-ttu-id="b194f-177">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="b194f-177">**Type**: *string*</span></span>  
<span data-ttu-id="b194f-178">**기본값**: 앱 어셈블리가 있는 폴더가 기본값으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-178">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="b194f-179">**설정 방법**: `UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="b194f-179">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="b194f-180">**환경 변수**: `<PREFIX_>CONTENTROOT`(`<PREFIX_>`는 [선택적이고 사용자 정의됨](#configuration-builder))</span><span class="sxs-lookup"><span data-stu-id="b194f-180">**Environment variable**: `<PREFIX_>CONTENTROOT` (`<PREFIX_>` is [optional and user-defined](#configuration-builder))</span></span>

<span data-ttu-id="b194f-181">경로가 존재하지 않는 경우 호스트가 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-181">If the path doesn't exist, the host fails to start.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseContentRoot)]

#### <a name="environment"></a><span data-ttu-id="b194f-182">환경</span><span class="sxs-lookup"><span data-stu-id="b194f-182">Environment</span></span>

<span data-ttu-id="b194f-183">앱의 [환경](xref:fundamentals/environments)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-183">Sets the app's [environment](xref:fundamentals/environments).</span></span>

<span data-ttu-id="b194f-184">**키**: environment</span><span class="sxs-lookup"><span data-stu-id="b194f-184">**Key**: environment</span></span>  
<span data-ttu-id="b194f-185">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="b194f-185">**Type**: *string*</span></span>  
<span data-ttu-id="b194f-186">**기본값**: Production</span><span class="sxs-lookup"><span data-stu-id="b194f-186">**Default**: Production</span></span>  
<span data-ttu-id="b194f-187">**설정 방법**: `UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="b194f-187">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="b194f-188">**환경 변수**: `<PREFIX_>ENVIRONMENT`(`<PREFIX_>`는 [선택적이고 사용자 정의됨](#configuration-builder))</span><span class="sxs-lookup"><span data-stu-id="b194f-188">**Environment variable**: `<PREFIX_>ENVIRONMENT` (`<PREFIX_>` is [optional and user-defined](#configuration-builder))</span></span>

<span data-ttu-id="b194f-189">환경은 어떠한 값으로도 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-189">The environment can be set to any value.</span></span> <span data-ttu-id="b194f-190">프레임워크에서 정의된 값은 `Development`, `Staging` 및 `Production`을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-190">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="b194f-191">값은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-191">Values aren't case sensitive.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseEnvironment)]

## <a name="configureappconfiguration"></a><span data-ttu-id="b194f-192">ConfigureAppConfiguration</span><span class="sxs-lookup"><span data-stu-id="b194f-192">ConfigureAppConfiguration</span></span>

<span data-ttu-id="b194f-193">앱 작성기 구성은 [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) 구현에서 [ConfigureAppConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configureappconfiguration)을 호출하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-193">App builder configuration is created by calling [ConfigureAppConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configureappconfiguration) on the [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) implementation.</span></span> <span data-ttu-id="b194f-194">`ConfigureAppConfiguration`은 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder)를 사용하여 앱의 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-194">`ConfigureAppConfiguration` uses an [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder) to create an [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) for the app.</span></span> <span data-ttu-id="b194f-195">`ConfigureAppConfiguration` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-195">`ConfigureAppConfiguration` can be called multiple times with additive results.</span></span> <span data-ttu-id="b194f-196">앱은 마지막에 값을 설정한 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-196">The app uses whichever option sets a value last.</span></span> <span data-ttu-id="b194f-197">`ConfigureAppConfiguration`을 사용하여 만든 구성은 다음 작업에 대한 [HostBuilderContext.Configuration](/dotnet/api/microsoft.extensions.hosting.hostbuildercontext.configuration)과 [Services](/dotnet/api/microsoft.extensions.hosting.ihost.services)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-197">The configuration created by `ConfigureAppConfiguration` is available at [HostBuilderContext.Configuration](/dotnet/api/microsoft.extensions.hosting.hostbuildercontext.configuration) for subsequent operations and in [Services](/dotnet/api/microsoft.extensions.hosting.ihost.services).</span></span>

<span data-ttu-id="b194f-198">`ConfigureAppConfiguration`을 사용한 앱 구성 예:</span><span class="sxs-lookup"><span data-stu-id="b194f-198">Example app configuration using `ConfigureAppConfiguration`:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureAppConfiguration)]

<span data-ttu-id="b194f-199">*appsettings.json*:</span><span class="sxs-lookup"><span data-stu-id="b194f-199">*appsettings.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.json)]

<span data-ttu-id="b194f-200">*appsettings.Development.json*:</span><span class="sxs-lookup"><span data-stu-id="b194f-200">*appsettings.Development.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.Development.json)]

<span data-ttu-id="b194f-201">*appsettings.Production.json*:</span><span class="sxs-lookup"><span data-stu-id="b194f-201">*appsettings.Production.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.Production.json)]

> [!NOTE]
> <span data-ttu-id="b194f-202">[AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) 확장 메서드는 현재 [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection)에서 반환되는 구성 섹션을 구문 분석할 수 없습니다(예: `.AddConfiguration(Configuration.GetSection("section"))`).</span><span class="sxs-lookup"><span data-stu-id="b194f-202">The [AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) extension method isn't currently capable of parsing a configuration section returned by [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection) (for example, `.AddConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="b194f-203">`GetSection` 메서드는 요청된 섹션에 대한 구성 키를 필터링하지만 키에 있는 섹션 이름을 그대로 둡니다(예: `section:Logging:LogLevel:Default`).</span><span class="sxs-lookup"><span data-stu-id="b194f-203">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:Logging:LogLevel:Default`).</span></span> <span data-ttu-id="b194f-204">`AddConfiguration` 메서드는 구성 키에 대한 정확한 일치를 예상합니다(예: `Logging:LogLevel:Default`).</span><span class="sxs-lookup"><span data-stu-id="b194f-204">The `AddConfiguration` method expects an exact match to configuration keys (for example, `Logging:LogLevel:Default`).</span></span> <span data-ttu-id="b194f-205">키에서 섹션 이름의 존재는 섹션 값으로 앱을 구성할 수 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-205">The presence of the section name on the keys prevents the section's values from configuring the app.</span></span> <span data-ttu-id="b194f-206">이 문제는 향후 릴리스에서 해결될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-206">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="b194f-207">자세한 내용 및 해결 방법은 [전체 키를 사용하여 WebHostBuilder.UseConfiguration에 구성 섹션을 전달](https://github.com/aspnet/Hosting/issues/839)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b194f-207">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>

<span data-ttu-id="b194f-208">출력 디렉터리로 설정 파일을 이동하려면, 설정 파일을 프로젝트 파일 내 [MSBuild 프로젝트 항목](/visualstudio/msbuild/common-msbuild-project-items)으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-208">To move settings files to the output directory, specify the settings files as [MSBuild project items](/visualstudio/msbuild/common-msbuild-project-items) in the project file.</span></span> <span data-ttu-id="b194f-209">샘플 앱은 다음 **&lt;콘텐츠, &gt;** 항목과 함께 JSON 앱 설정 파일과 *hostsettings.json*을 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-209">The sample app moves its JSON app settings files and *hostsettings.json* with the following **&lt;Content:&gt;** item:</span></span>

```xml
<ItemGroup>
  <Content Include="**\*.json" CopyToOutputDirectory="PreserveNewest" />
</ItemGroup>
```

## <a name="configureservices"></a><span data-ttu-id="b194f-210">ConfigureServices</span><span class="sxs-lookup"><span data-stu-id="b194f-210">ConfigureServices</span></span>

<span data-ttu-id="b194f-211">[ConfigureServices](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configureservices)는 앱의 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에 서비스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-211">[ConfigureServices](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configureservices) adds services to the app's [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> <span data-ttu-id="b194f-212">`ConfigureServices` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-212">`ConfigureServices` can be called multiple times with additive results.</span></span>

<span data-ttu-id="b194f-213">호스티드 서비스는 [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 인터페이스를 구현하는 백그라운드 작업 논리가 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-213">A hosted service is a class with background task logic that implements the [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) interface.</span></span> <span data-ttu-id="b194f-214">자세한 내용은 <xref:fundamentals/host/hosted-services>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b194f-214">For more information, see <xref:fundamentals/host/hosted-services>.</span></span>

<span data-ttu-id="b194f-215">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)은 `AddHostedService` 확장 메서드를 사용하여 수명 이벤트, `LifetimeEventsHostedService` 및 시간 제한 백그라운드 작업에 대한 서비스 `TimedHostedService`를 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-215">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) uses the `AddHostedService` extension method to add a service for lifetime events, `LifetimeEventsHostedService`, and a timed background task, `TimedHostedService`, to the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureServices)]

## <a name="configurelogging"></a><span data-ttu-id="b194f-216">ConfigureLogging</span><span class="sxs-lookup"><span data-stu-id="b194f-216">ConfigureLogging</span></span>

<span data-ttu-id="b194f-217">[ConfigureLogging](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configurelogging)은 제공된 [ILoggingBuilder](/dotnet/api/microsoft.extensions.logging.iloggingbuilder) 구성을 위한 대리자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-217">[ConfigureLogging](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configurelogging) adds a delegate for configuring the provided [ILoggingBuilder](/dotnet/api/microsoft.extensions.logging.iloggingbuilder).</span></span> <span data-ttu-id="b194f-218">`ConfigureLogging` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-218">`ConfigureLogging` may be called multiple times with additive results.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureLogging)]

### <a name="useconsolelifetime"></a><span data-ttu-id="b194f-219">UseConsoleLifetime</span><span class="sxs-lookup"><span data-stu-id="b194f-219">UseConsoleLifetime</span></span>

<span data-ttu-id="b194f-220">[UseConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.useconsolelifetime)은 `Ctrl+C`/SIGINT 또는 SIGTERM을 수신 대기하고 [StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication)을 호출하여 종료 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-220">[UseConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.useconsolelifetime) listens for `Ctrl+C`/SIGINT or SIGTERM and calls [StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication) to start the shutdown process.</span></span> <span data-ttu-id="b194f-221">`UseConsoleLifetime`은 [RunAsync](#runasync) 및 [WaitForShutdownAsync](#waitforshutdownasync)와 같은 확장의 차단을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-221">`UseConsoleLifetime` unblocks extensions such as [RunAsync](#runasync) and [WaitForShutdownAsync](#waitforshutdownasync).</span></span> <span data-ttu-id="b194f-222">[ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime)은 기본 수명 구현으로 미리 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-222">[ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime) is pre-registered as the default lifetime implementation.</span></span> <span data-ttu-id="b194f-223">등록된 마지막 수명이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-223">The last lifetime registered is used.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseConsoleLifetime)]

## <a name="container-configuration"></a><span data-ttu-id="b194f-224">컨테이너 구성</span><span class="sxs-lookup"><span data-stu-id="b194f-224">Container configuration</span></span>

<span data-ttu-id="b194f-225">호스트는 다른 컨테이너 연결을 지원하기 위해 [IServiceProviderFactory](/dotnet/api/microsoft.extensions.dependencyinjection.iserviceproviderfactory-1)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-225">To support plugging in other containers, the host can accept an [IServiceProviderFactory](/dotnet/api/microsoft.extensions.dependencyinjection.iserviceproviderfactory-1).</span></span> <span data-ttu-id="b194f-226">팩터리 제공은 DI 컨테이너 등록의 일부가 아니지만 구체적 DI 컨테이너를 만드는 데 사용되는 내장 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-226">Providing a factory isn't part of the DI container registration but is instead a host intrinsic used to create the concrete DI container.</span></span> <span data-ttu-id="b194f-227">[UseServiceProviderFactory(IServiceProviderFactory&lt;TContainerBuilder&gt;)](/dotnet/api/microsoft.extensions.hosting.hostbuilder.useserviceproviderfactory)는 앱의 서비스 공급자를 만드는 데 사용되는 기본 팩터리를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-227">[UseServiceProviderFactory(IServiceProviderFactory&lt;TContainerBuilder&gt;)](/dotnet/api/microsoft.extensions.hosting.hostbuilder.useserviceproviderfactory) overrides the default factory used to create the app's service provider.</span></span>

<span data-ttu-id="b194f-228">사용자 지정 컨테이너 구성은 [ConfigureContainer](/dotnet/api/microsoft.extensions.hosting.hostbuilder.configurecontainer) 메서드로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-228">Custom container configuration is managed by the [ConfigureContainer](/dotnet/api/microsoft.extensions.hosting.hostbuilder.configurecontainer) method.</span></span> <span data-ttu-id="b194f-229">`ConfigureContainer`는 기본 호스트 API 위에 컨테이너를 구성하기 위한 강력한 형식의 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-229">`ConfigureContainer` provides a strongly-typed experience for configuring the container on top of the underlying host API.</span></span> <span data-ttu-id="b194f-230">`ConfigureContainer` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-230">`ConfigureContainer` can be called multiple times with additive results.</span></span>

<span data-ttu-id="b194f-231">앱에 대한 서비스 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-231">Create a service container for the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/ServiceContainer.cs)]

<span data-ttu-id="b194f-232">서비스 컨테이너 팩터리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-232">Provide a service container factory:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/ServiceContainerFactory.cs)]

<span data-ttu-id="b194f-233">팩터리를 사용하고 앱에 대 한 사용자 지정 서비스 컨테이너를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-233">Use the factory and configure the custom service container for the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ContainerConfiguration)]

## <a name="extensibility"></a><span data-ttu-id="b194f-234">확장성</span><span class="sxs-lookup"><span data-stu-id="b194f-234">Extensibility</span></span>

<span data-ttu-id="b194f-235">`IHostBuilder`에서 확장 메서드를 사용하여 호스트 확장성이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-235">Host extensibility is performed with extension methods on `IHostBuilder`.</span></span> <span data-ttu-id="b194f-236">다음 예제는 <xref:fundamentals/host/hosted-services>에 설명된 [TimedHostedService](xref:fundamentals/host/hosted-services#timed-background-tasks) 예제를 사용하여 확장 메서드가 `IHostBuilder` 구현을 확장하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-236">The following example shows how an extension method extends an `IHostBuilder` implementation with the [TimedHostedService](xref:fundamentals/host/hosted-services#timed-background-tasks) example demonstrated in <xref:fundamentals/host/hosted-services>.</span></span>

```csharp
var host = new HostBuilder()
    .UseHostedService<TimedHostedService>()
    .Build();

await host.StartAsync();
```

<span data-ttu-id="b194f-237">앱은 `UseHostedService` 확장 메서드를 설정하여 `T`에서 전달되는 호스티드 서비스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-237">An app establishes the `UseHostedService` extension method to register the hosted service passed in `T`:</span></span>

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

## <a name="manage-the-host"></a><span data-ttu-id="b194f-238">호스트 관리</span><span class="sxs-lookup"><span data-stu-id="b194f-238">Manage the host</span></span>

<span data-ttu-id="b194f-239">[IHost](/dotnet/api/microsoft.extensions.hosting.ihost) 구현은 서비스 컨테이너에 등록된 `IHostedService` 구현의 시작 및 중지를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-239">The [IHost](/dotnet/api/microsoft.extensions.hosting.ihost) implementation is responsible for starting and stopping the `IHostedService` implementations that are registered in the service container.</span></span>

### <a name="run"></a><span data-ttu-id="b194f-240">실행</span><span class="sxs-lookup"><span data-stu-id="b194f-240">Run</span></span>

<span data-ttu-id="b194f-241">[Run](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.run)은 앱을 시작하고 호스트가 종료될 때까지 호출 스레드를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-241">[Run](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.run) runs the app and blocks the calling thread until the host is shut down:</span></span>

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

### <a name="runasync"></a><span data-ttu-id="b194f-242">RunAsync</span><span class="sxs-lookup"><span data-stu-id="b194f-242">RunAsync</span></span>

<span data-ttu-id="b194f-243">[RunAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.runasync)는 앱을 실행하고 취소 토큰 또는 종료가 트리거될 때 완료되는 `Task`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-243">[RunAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.runasync) runs the app and returns a `Task` that completes when the cancellation token or shutdown is triggered:</span></span>

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

### <a name="runconsoleasync"></a><span data-ttu-id="b194f-244">RunConsoleAsync</span><span class="sxs-lookup"><span data-stu-id="b194f-244">RunConsoleAsync</span></span>

<span data-ttu-id="b194f-245">[RunConsoleAsync](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.runconsoleasync)는 콘솔 지원을 구현하고, 호스트를 빌드 및 시작하며, `Ctrl+C`/SIGINT 또는 SIGTERM이 종료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-245">[RunConsoleAsync](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.runconsoleasync) enables console support, builds and starts the host, and waits for `Ctrl+C`/SIGINT or SIGTERM to shut down.</span></span>

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

### <a name="start-and-stopasync"></a><span data-ttu-id="b194f-246">Start 및 StopAsync</span><span class="sxs-lookup"><span data-stu-id="b194f-246">Start and StopAsync</span></span>

<span data-ttu-id="b194f-247">[Start](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.start)는 호스트를 동기적으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-247">[Start](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.start) starts the host synchronously.</span></span>

<span data-ttu-id="b194f-248">[StopAsync(TimeSpan)](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.stopasync)는 지정된 시간 제한 내에서 호스트를 중지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-248">[StopAsync(TimeSpan)](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.stopasync) attempts to stop the host within the provided timeout.</span></span>

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

### <a name="startasync-and-stopasync"></a><span data-ttu-id="b194f-249">StartAsync 및 StopAsync</span><span class="sxs-lookup"><span data-stu-id="b194f-249">StartAsync and StopAsync</span></span>

<span data-ttu-id="b194f-250">[StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync)는 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-250">[StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync) starts the app.</span></span>

<span data-ttu-id="b194f-251">[StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync)는 앱을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-251">[StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync) stops the app.</span></span>

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

### <a name="waitforshutdown"></a><span data-ttu-id="b194f-252">WaitForShutdown</span><span class="sxs-lookup"><span data-stu-id="b194f-252">WaitForShutdown</span></span>

<span data-ttu-id="b194f-253">[WaitForShutdown](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdown)은 [ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime)(`Ctrl+C`/SIGINT 또는 SIGTERM 수신 대기)과 같은 [IHostLifetime](/dotnet/api/microsoft.extensions.hosting.ihostlifetime)을 통해 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-253">[WaitForShutdown](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdown) is triggered via the [IHostLifetime](/dotnet/api/microsoft.extensions.hosting.ihostlifetime), such as [ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime) (listens for `Ctrl+C`/SIGINT or SIGTERM).</span></span> <span data-ttu-id="b194f-254">`WaitForShutdown`은 [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-254">`WaitForShutdown` calls [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync).</span></span>

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

### <a name="waitforshutdownasync"></a><span data-ttu-id="b194f-255">WaitForShutdownAsync</span><span class="sxs-lookup"><span data-stu-id="b194f-255">WaitForShutdownAsync</span></span>

<span data-ttu-id="b194f-256">[WaitForShutdownAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdownasync)는 지정된 토큰을 통해 종료가 트리거될 때 완료되는 `Task`를 반환하고 [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-256">[WaitForShutdownAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdownasync) returns a `Task` that completes when shutdown is triggered via the given token and calls [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync).</span></span>

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

### <a name="external-control"></a><span data-ttu-id="b194f-257">외부 제어</span><span class="sxs-lookup"><span data-stu-id="b194f-257">External control</span></span>

<span data-ttu-id="b194f-258">외부에서 호출할 수 있는 메서드를 사용하여 호스트의 외부 제어를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-258">External control of the host can be achieved using methods that can be called externally:</span></span>

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

<span data-ttu-id="b194f-259">[IHostLifetime.WaitForStartAsync](/dotnet/api/microsoft.extensions.hosting.ihostlifetime.waitforstartasync)는 [StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync) 시작 시 호출되고, 완료될 때까지 기다린 후 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-259">[IHostLifetime.WaitForStartAsync](/dotnet/api/microsoft.extensions.hosting.ihostlifetime.waitforstartasync) is called at the start of [StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync), which waits until it's complete before continuing.</span></span> <span data-ttu-id="b194f-260">이는 외부 이벤트에서 신호를 보낼 때까지 시작을 지연시키는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-260">This can be used to delay startup until signaled by an external event.</span></span>

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="b194f-261">IHostingEnvironment 인터페이스</span><span class="sxs-lookup"><span data-stu-id="b194f-261">IHostingEnvironment interface</span></span>

<span data-ttu-id="b194f-262">[IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment)는 앱의 호스팅 환경에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-262">[IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment) provides information about the app's hosting environment.</span></span> <span data-ttu-id="b194f-263">해당 속성 및 확장 메서드를 사용하기 위해 [생성자 주입](xref:fundamentals/dependency-injection)을 사용하여 `IHostingEnvironment`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-263">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

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

<span data-ttu-id="b194f-264">자세한 내용은 <xref:fundamentals/environments>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b194f-264">For more information, see <xref:fundamentals/environments>.</span></span>

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="b194f-265">IApplicationLifetime 인터페이스</span><span class="sxs-lookup"><span data-stu-id="b194f-265">IApplicationLifetime interface</span></span>

<span data-ttu-id="b194f-266">[IApplicationLifetime](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime)은 점진적인 종료 요청을 비롯한 사후 시작 및 종료 작업을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-266">[IApplicationLifetime](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime) allows for post-startup and shutdown activities, including graceful shutdown requests.</span></span> <span data-ttu-id="b194f-267">인터페이스에서 세 가지 속성은 취소 토큰으로, 시작 및 종료 이벤트를 정의하는 `Action` 메서드를 등록하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-267">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span>

| <span data-ttu-id="b194f-268">취소 토큰</span><span class="sxs-lookup"><span data-stu-id="b194f-268">Cancellation Token</span></span> | <span data-ttu-id="b194f-269">트리거되는 경우:</span><span class="sxs-lookup"><span data-stu-id="b194f-269">Triggered when&#8230;</span></span> |
| ------------------ | --------------------- |
| [<span data-ttu-id="b194f-270">ApplicationStarted</span><span class="sxs-lookup"><span data-stu-id="b194f-270">ApplicationStarted</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstarted) | <span data-ttu-id="b194f-271">호스트가 완벽하게 시작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-271">The host has fully started.</span></span> |
| [<span data-ttu-id="b194f-272">ApplicationStopped</span><span class="sxs-lookup"><span data-stu-id="b194f-272">ApplicationStopped</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopped) | <span data-ttu-id="b194f-273">호스트가 정상적으로 종료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-273">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="b194f-274">모든 요청이 처리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-274">All requests should be processed.</span></span> <span data-ttu-id="b194f-275">종료는 이 이벤트가 완료될 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-275">Shutdown blocks until this event completes.</span></span> |
| [<span data-ttu-id="b194f-276">ApplicationStopping</span><span class="sxs-lookup"><span data-stu-id="b194f-276">ApplicationStopping</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopping) | <span data-ttu-id="b194f-277">호스트가 정상적으로 종료되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-277">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="b194f-278">요청은 계속 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-278">Requests may still be processing.</span></span> <span data-ttu-id="b194f-279">종료는 이 이벤트가 완료될 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-279">Shutdown blocks until this event completes.</span></span> |

<span data-ttu-id="b194f-280">클래스에 대한 `IApplicationLifetime` 서비스 생성자 주입을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-280">Constructor-inject the `IApplicationLifetime` service into any class.</span></span> <span data-ttu-id="b194f-281">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)은 `LifetimeEventsHostedService` 클래스(`IHostedService` 구현)에 대한 생성자 주입을 사용하여 이벤트를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-281">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) uses constructor injection into a `LifetimeEventsHostedService` class (an `IHostedService` implementation) to register the events.</span></span>

<span data-ttu-id="b194f-282">*LifetimeEventsHostedService.cs*:</span><span class="sxs-lookup"><span data-stu-id="b194f-282">*LifetimeEventsHostedService.cs*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/LifetimeEventsHostedService.cs?name=snippet1)]

<span data-ttu-id="b194f-283">[StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication)은 앱의 종료를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-283">[StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication) requests termination of the app.</span></span> <span data-ttu-id="b194f-284">다음 클래스에서는 `StopApplication`을 사용하여 해당 클래스의 `Shutdown` 메서드를 호출하는 경우 앱을 정상 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="b194f-284">The following class uses `StopApplication` to gracefully shut down an app when the class's `Shutdown` method is called:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="b194f-285">추가 자료</span><span class="sxs-lookup"><span data-stu-id="b194f-285">Additional resources</span></span>

* <xref:fundamentals/host/hosted-services>
* [<span data-ttu-id="b194f-286">GitHub의 호스팅 리포지토리 샘플</span><span class="sxs-lookup"><span data-stu-id="b194f-286">Hosting repo samples on GitHub</span></span>](https://github.com/aspnet/Hosting/tree/release/2.1/samples)
