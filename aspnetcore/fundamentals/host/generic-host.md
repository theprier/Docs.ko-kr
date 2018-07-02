---
title: .NET 일반 호스트
author: guardrex
description: 앱 시작 및 수명 관리를 담당하는 .NET의 일반 호스트에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 05/16/2018
uid: fundamentals/host/generic-host
ms.openlocfilehash: 33e5829ce4a09e132743b4174a588cf232a44775
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276264"
---
# <a name="net-generic-host"></a><span data-ttu-id="e4388-103">.NET 일반 호스트</span><span class="sxs-lookup"><span data-stu-id="e4388-103">.NET Generic Host</span></span>

<span data-ttu-id="e4388-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="e4388-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="e4388-105">.NET 앱은 *호스트*를 구성 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-105">.NET apps configure and launch a *host*.</span></span> <span data-ttu-id="e4388-106">호스트는 앱 시작 및 수명 관리를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-106">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="e4388-107">이 항목에서는 HTTP 요청을 처리하지 않는 앱을 호스팅하는 데 유용한 ASP.NET Core 일반 호스트([HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder))를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-107">This topic covers the ASP.NET Core Generic Host ([HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder)), which is useful for hosting apps that don't process HTTP requests.</span></span> <span data-ttu-id="e4388-108">웹 호스트([WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder))에 대한 자세한 내용은 [웹 호스트](xref:fundamentals/host/web-host) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4388-108">For coverage of the Web Host ([WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)), see the [Web Host](xref:fundamentals/host/web-host) topic.</span></span>

<span data-ttu-id="e4388-109">일반 호스트의 목표는 웹 호스트 API에서 HTTP 파이프라인을 분리하여 호스트 시나리오의 더 광범위한 배열을 구현하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-109">The goal of the Generic Host is to decouple the HTTP pipeline from the Web Host API to enable a wider array of host scenarios.</span></span> <span data-ttu-id="e4388-110">일반 호스트에 기반을 둔 메시징, 백그라운드 작업 및 기타 HTTP 이외 워크로드는 구성, 종속성 주입(DI) 및 로깅과 같은 교차 편집 기능에서 이점을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-110">Messaging, background tasks, and other non-HTTP workloads based on the Generic Host benefit from cross-cutting capabilities, such as configuration, dependency injection (DI), and logging.</span></span>

<span data-ttu-id="e4388-111">일반 호스트는 ASP.NET Core 2.1의 새로운 기능이며 웹 호스팅 시나리오에 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-111">The Generic Host is new in ASP.NET Core 2.1 and isn't suitable for web hosting scenarios.</span></span> <span data-ttu-id="e4388-112">웹 호스팅 시나리오의 경우 [웹 호스트](xref:fundamentals/host/web-host)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="e4388-112">For web hosting scenarios, use the [Web Host](xref:fundamentals/host/web-host).</span></span> <span data-ttu-id="e4388-113">일반 호스트는 향후 릴리스에서 웹 호스트를 대체하기 위해 개발 중이며, HTTP 및 HTTP 이외 시나리오에서 기본 호스트 API 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-113">The Generic Host is under development to replace the Web Host in a future release and act as the primary host API in both HTTP and non-HTTP scenarios.</span></span>

<span data-ttu-id="e4388-114">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="e4388-114">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="e4388-115">[Visual Studio Code](https://code.visualstudio.com/)에서 샘플 앱을 실행할 때는 *외부 또는 통합 터미널*을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="e4388-115">When running the sample app in [Visual Studio Code](https://code.visualstudio.com/), use an *external or integrated terminal*.</span></span> <span data-ttu-id="e4388-116">`internalConsole`에서는 샘플을 실행하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e4388-116">Don't run the sample in an `internalConsole`.</span></span>

<span data-ttu-id="e4388-117">Visual Studio Code에서 콘솔을 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="e4388-117">To set the console in Visual Studio Code:</span></span>

1. <span data-ttu-id="e4388-118">*.vscode/launch.json* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-118">Open the *.vscode/launch.json* file.</span></span>
1. <span data-ttu-id="e4388-119">**.NET Core 시작(콘솔)** 구성에서 **콘솔** 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-119">In the **.NET Core Launch (console)** configuration, locate the **console** entry.</span></span> <span data-ttu-id="e4388-120">값을 `externalTerminal` 또는 `integratedTerminal` 중 하나로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-120">Set the value to either `externalTerminal` or `integratedTerminal`.</span></span>

## <a name="introduction"></a><span data-ttu-id="e4388-121">소개</span><span class="sxs-lookup"><span data-stu-id="e4388-121">Introduction</span></span>

<span data-ttu-id="e4388-122">일반 호스트 라이브러리는 [Microsoft.Extensions.Hosting 네임스페이스](/dotnet/api/microsoft.extensions.hosting)에서 사용할 수 있으며, [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting/)에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-122">The Generic Host library is available in the [Microsoft.Extensions.Hosting namespace](/dotnet/api/microsoft.extensions.hosting) and provided by the [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting/) package.</span></span> <span data-ttu-id="e4388-123">`Microsoft.Extensions.Hosting` 패키지는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)(ASP.NET Core 2.1 이상)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-123">The `Microsoft.Extensions.Hosting` package is included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) (ASP.NET Core 2.1 or later).</span></span>

<span data-ttu-id="e4388-124">[IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice)는 코드 실행 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-124">[IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) is the entry point to code execution.</span></span> <span data-ttu-id="e4388-125">각 `IHostedService` 구현은 [ConfigureServices의 서비스 등록](#configureservices) 순서대로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-125">Each `IHostedService` implementation is executed in the order of [service registration in ConfigureServices](#configureservices).</span></span> <span data-ttu-id="e4388-126">[StartAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.startasync)는 호스트가 시작될 때 각 `IHostedService`에서 호출되고, [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.stopasync)는 호스트가 점진적으로 종료될 때 등록 순서의 역순으로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-126">[StartAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.startasync) is called on each `IHostedService` when the host starts, and [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.stopasync) is called in reverse registration order when the host shuts down gracefully.</span></span>

## <a name="set-up-a-host"></a><span data-ttu-id="e4388-127">호스트 설정</span><span class="sxs-lookup"><span data-stu-id="e4388-127">Set up a host</span></span>

<span data-ttu-id="e4388-128">[IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder)는 라이브러리 및 앱이 호스트를 초기화, 빌드 및 실행 하는 데 사용하는 주 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-128">[IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) is the main component that libraries and apps use to initialize, build, and run the host:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_HostBuilder)]

## <a name="host-configuration"></a><span data-ttu-id="e4388-129">호스트 구성</span><span class="sxs-lookup"><span data-stu-id="e4388-129">Host configuration</span></span>

<span data-ttu-id="e4388-130">[HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder)는 호스트 구성 값을 설정하기 위해 다음 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-130">[HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder) relies on the following approaches to set the host configuration values:</span></span>

* <span data-ttu-id="e4388-131">구성 작성기</span><span class="sxs-lookup"><span data-stu-id="e4388-131">Configuration builder</span></span>
* <span data-ttu-id="e4388-132">확장 메서드 구성</span><span class="sxs-lookup"><span data-stu-id="e4388-132">Extension method configuration</span></span>

### <a name="configuration-builder"></a><span data-ttu-id="e4388-133">구성 작성기</span><span class="sxs-lookup"><span data-stu-id="e4388-133">Configuration builder</span></span>

<span data-ttu-id="e4388-134">호스트 작성기 구성은 [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) 구현에서 [ConfigureHostConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configurehostconfiguration)을 호출하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-134">Host builder configuration is created by calling [ConfigureHostConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configurehostconfiguration) on the [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) implementation.</span></span> <span data-ttu-id="e4388-135">`ConfigureHostConfiguration`은 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder)를 사용하여 호스트의 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-135">`ConfigureHostConfiguration` uses an [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder) to create an [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) for the host.</span></span> <span data-ttu-id="e4388-136">구성 작성기는 앱의 빌드 프로세스에서 사용할 [IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment)를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-136">The configuration builder initializes the [IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment) for use in the app's build process.</span></span>

<span data-ttu-id="e4388-137">환경 변수 구성은 기본적으로 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-137">Environment variable configuration isn't added by default.</span></span> <span data-ttu-id="e4388-138">호스트 빌더에서 [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables)를 호출하여 환경 변수의 호스트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-138">Call [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables) on the host builder to configure the host from environment variables.</span></span> <span data-ttu-id="e4388-139">`AddEnvironmentVariables`는 선택적 사용자 정의 접두사를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-139">`AddEnvironmentVariables` accepts an optional user-defined prefix.</span></span> <span data-ttu-id="e4388-140">샘플 앱은 `PREFIX_` 접두사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-140">The sample app uses a prefix of `PREFIX_`.</span></span> <span data-ttu-id="e4388-141">접두사는 환경 변수를 읽을 때 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-141">The prefix is removed when the environment variables are read.</span></span> <span data-ttu-id="e4388-142">샘플 앱의 호스트가 구성되면 `PREFIX_ENVIRONMENT`의 환경 변수 값이 `environment` 키에 대한 호스트 구성 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-142">When the sample app's host is configured, the environment variable value for `PREFIX_ENVIRONMENT` becomes the host configuration value for the `environment` key.</span></span>

<span data-ttu-id="e4388-143">[Visual Studio](https://www.visualstudio.com/)를 사용하거나 `dotnet run`을 통해 앱을 실행할 때 개발하는 동안에 환경 변수는 *Properties/launchSettings.json* 파일에 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-143">During development when using [Visual Studio](https://www.visualstudio.com/) or running an app with `dotnet run`, environment variables may be set in the *Properties/launchSettings.json* file.</span></span> <span data-ttu-id="e4388-144">[Visual Studio Code](https://code.visualstudio.com/)에서 환경 변수는 개발하는 동안에 *.vscode/launch.json* 파일에 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-144">In [Visual Studio Code](https://code.visualstudio.com/), environment variables may be set in the *.vscode/launch.json* file during development.</span></span> <span data-ttu-id="e4388-145">자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4388-145">For more information, see [Use multiple environments](xref:fundamentals/environments).</span></span>

<span data-ttu-id="e4388-146">`ConfigureHostConfiguration` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-146">`ConfigureHostConfiguration` can be called multiple times with additive results.</span></span> <span data-ttu-id="e4388-147">호스트는 마지막에 값을 설정한 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-147">The host uses whichever option sets a value last.</span></span>

<span data-ttu-id="e4388-148">*hostsettings.json*:</span><span class="sxs-lookup"><span data-stu-id="e4388-148">*hostsettings.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/hostsettings.json)]

<span data-ttu-id="e4388-149">`ConfigureHostConfiguration`을 사용한 `HostBuilder` 구성 예:</span><span class="sxs-lookup"><span data-stu-id="e4388-149">Example `HostBuilder` configuration using `ConfigureHostConfiguration`:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureHostConfiguration)]

> [!NOTE]
> <span data-ttu-id="e4388-150">[AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) 확장 메서드는 현재 [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection)에서 반환되는 구성 섹션을 구문 분석할 수 없습니다(예: `.AddConfiguration(Configuration.GetSection("section"))`).</span><span class="sxs-lookup"><span data-stu-id="e4388-150">The [AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) extension method isn't currently capable of parsing a configuration section returned by [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection) (for example, `.AddConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="e4388-151">`GetSection` 메서드는 요청된 섹션에 대한 구성 키를 필터링하지만 키에 있는 섹션 이름을 그대로 둡니다(예: `section:environment`).</span><span class="sxs-lookup"><span data-stu-id="e4388-151">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:environment`).</span></span> <span data-ttu-id="e4388-152">`AddConfiguration` 메서드에서는 키가 `HostBuilder` 키와 일치해야 합니다(예: `environment`).</span><span class="sxs-lookup"><span data-stu-id="e4388-152">The `AddConfiguration` method expects the keys to match the `HostBuilder` keys (for example, `environment`).</span></span> <span data-ttu-id="e4388-153">키에서 섹션 이름의 존재는 섹션 값으로 호스트를 구성할 수 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-153">The presence of the section name on the keys prevents the section's values from configuring the host.</span></span> <span data-ttu-id="e4388-154">이 문제는 향후 릴리스에서 해결될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-154">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="e4388-155">자세한 내용 및 해결 방법은 [전체 키를 사용하여 WebHostBuilder.UseConfiguration에 구성 섹션을 전달](https://github.com/aspnet/Hosting/issues/839)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4388-155">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>

### <a name="extension-method-configuration"></a><span data-ttu-id="e4388-156">확장 메서드 구성</span><span class="sxs-lookup"><span data-stu-id="e4388-156">Extension method configuration</span></span>

<span data-ttu-id="e4388-157">확장 메서드는 콘텐츠 루트 및 환경을 구성하기 위해 `IHostBuilder` 구현에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-157">Extension methods are called on the `IHostBuilder` implementation to configure the content root and the environment.</span></span>

#### <a name="content-root"></a><span data-ttu-id="e4388-158">콘텐츠 루트</span><span class="sxs-lookup"><span data-stu-id="e4388-158">Content Root</span></span>

<span data-ttu-id="e4388-159">이 설정은 호스트가 콘텐츠 파일을 검색하기 시작하는 지점을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-159">This setting determines where the host begins searching for content files.</span></span>

<span data-ttu-id="e4388-160">**키**: contentRoot</span><span class="sxs-lookup"><span data-stu-id="e4388-160">**Key**: contentRoot</span></span>  
<span data-ttu-id="e4388-161">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="e4388-161">**Type**: *string*</span></span>  
<span data-ttu-id="e4388-162">**기본값**: 앱 어셈블리가 있는 폴더가 기본값으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-162">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="e4388-163">**설정 방법**: `UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="e4388-163">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="e4388-164">**환경 변수**: `<PREFIX_>CONTENTROOT`(`<PREFIX_>`는 [선택적이고 사용자 정의됨](#configuration-builder))</span><span class="sxs-lookup"><span data-stu-id="e4388-164">**Environment variable**: `<PREFIX_>CONTENTROOT` (`<PREFIX_>` is [optional and user-defined](#configuration-builder))</span></span>

<span data-ttu-id="e4388-165">경로가 존재하지 않는 경우 호스트가 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-165">If the path doesn't exist, the host fails to start.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseContentRoot)]

#### <a name="environment"></a><span data-ttu-id="e4388-166">환경</span><span class="sxs-lookup"><span data-stu-id="e4388-166">Environment</span></span>

<span data-ttu-id="e4388-167">앱의 [환경](xref:fundamentals/environments)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-167">Sets the app's [environment](xref:fundamentals/environments).</span></span>

<span data-ttu-id="e4388-168">**키**: environment</span><span class="sxs-lookup"><span data-stu-id="e4388-168">**Key**: environment</span></span>  
<span data-ttu-id="e4388-169">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="e4388-169">**Type**: *string*</span></span>  
<span data-ttu-id="e4388-170">**기본값**: Production</span><span class="sxs-lookup"><span data-stu-id="e4388-170">**Default**: Production</span></span>  
<span data-ttu-id="e4388-171">**설정 방법**: `UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="e4388-171">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="e4388-172">**환경 변수**: `<PREFIX_>ENVIRONMENT`(`<PREFIX_>`는 [선택적이고 사용자 정의됨](#configuration-builder))</span><span class="sxs-lookup"><span data-stu-id="e4388-172">**Environment variable**: `<PREFIX_>ENVIRONMENT` (`<PREFIX_>` is [optional and user-defined](#configuration-builder))</span></span>

<span data-ttu-id="e4388-173">환경은 어떠한 값으로도 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-173">The environment can be set to any value.</span></span> <span data-ttu-id="e4388-174">프레임워크에서 정의된 값은 `Development`, `Staging` 및 `Production`을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-174">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="e4388-175">값은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-175">Values aren't case sensitive.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseEnvironment)]

## <a name="configureappconfiguration"></a><span data-ttu-id="e4388-176">ConfigureAppConfiguration</span><span class="sxs-lookup"><span data-stu-id="e4388-176">ConfigureAppConfiguration</span></span>

<span data-ttu-id="e4388-177">앱 작성기 구성은 [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) 구현에서 [ConfigureAppConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configureappconfiguration)을 호출하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-177">App builder configuration is created by calling [ConfigureAppConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configureappconfiguration) on the [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) implementation.</span></span> <span data-ttu-id="e4388-178">`ConfigureAppConfiguration`은 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder)를 사용하여 앱의 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-178">`ConfigureAppConfiguration` uses an [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder) to create an [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) for the app.</span></span> <span data-ttu-id="e4388-179">`ConfigureAppConfiguration` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-179">`ConfigureAppConfiguration` can be called multiple times with additive results.</span></span> <span data-ttu-id="e4388-180">앱은 마지막에 값을 설정한 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-180">The app uses whichever option sets a value last.</span></span> <span data-ttu-id="e4388-181">`ConfigureAppConfiguration`을 사용하여 만든 구성은 다음 작업에 대한 [HostBuilderContext.Configuration](/dotnet/api/microsoft.extensions.hosting.hostbuildercontext.configuration)과 [Services](/dotnet/api/microsoft.extensions.hosting.ihost.services)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-181">The configuration created by `ConfigureAppConfiguration` is available at [HostBuilderContext.Configuration](/dotnet/api/microsoft.extensions.hosting.hostbuildercontext.configuration) for subsequent operations and in [Services](/dotnet/api/microsoft.extensions.hosting.ihost.services).</span></span>

<span data-ttu-id="e4388-182">`ConfigureAppConfiguration`을 사용한 앱 구성 예:</span><span class="sxs-lookup"><span data-stu-id="e4388-182">Example app configuration using `ConfigureAppConfiguration`:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureAppConfiguration)]

<span data-ttu-id="e4388-183">*appsettings.json*:</span><span class="sxs-lookup"><span data-stu-id="e4388-183">*appsettings.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.json)]

<span data-ttu-id="e4388-184">*appsettings.Development.json*:</span><span class="sxs-lookup"><span data-stu-id="e4388-184">*appsettings.Development.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.Development.json)]

<span data-ttu-id="e4388-185">*appsettings.Production.json*:</span><span class="sxs-lookup"><span data-stu-id="e4388-185">*appsettings.Production.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.Production.json)]

> [!NOTE]
> <span data-ttu-id="e4388-186">[AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) 확장 메서드는 현재 [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection)에서 반환되는 구성 섹션을 구문 분석할 수 없습니다(예: `.AddConfiguration(Configuration.GetSection("section"))`).</span><span class="sxs-lookup"><span data-stu-id="e4388-186">The [AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) extension method isn't currently capable of parsing a configuration section returned by [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection) (for example, `.AddConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="e4388-187">`GetSection` 메서드는 요청된 섹션에 대한 구성 키를 필터링하지만 키에 있는 섹션 이름을 그대로 둡니다(예: `section:Logging:LogLevel:Default`).</span><span class="sxs-lookup"><span data-stu-id="e4388-187">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:Logging:LogLevel:Default`).</span></span> <span data-ttu-id="e4388-188">`AddConfiguration` 메서드는 구성 키에 대한 정확한 일치를 예상합니다(예: `Logging:LogLevel:Default`).</span><span class="sxs-lookup"><span data-stu-id="e4388-188">The `AddConfiguration` method expects an exact match to configuration keys (for example, `Logging:LogLevel:Default`).</span></span> <span data-ttu-id="e4388-189">키에서 섹션 이름의 존재는 섹션 값으로 앱을 구성할 수 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-189">The presence of the section name on the keys prevents the section's values from configuring the app.</span></span> <span data-ttu-id="e4388-190">이 문제는 향후 릴리스에서 해결될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-190">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="e4388-191">자세한 내용 및 해결 방법은 [전체 키를 사용하여 WebHostBuilder.UseConfiguration에 구성 섹션을 전달](https://github.com/aspnet/Hosting/issues/839)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4388-191">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>

## <a name="configureservices"></a><span data-ttu-id="e4388-192">ConfigureServices</span><span class="sxs-lookup"><span data-stu-id="e4388-192">ConfigureServices</span></span>

<span data-ttu-id="e4388-193">[ConfigureServices](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configureservices)는 앱의 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에 서비스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-193">[ConfigureServices](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configureservices) adds services to the app's [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> <span data-ttu-id="e4388-194">`ConfigureServices` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-194">`ConfigureServices` can be called multiple times with additive results.</span></span>

<span data-ttu-id="e4388-195">호스티드 서비스는 [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 인터페이스를 구현하는 백그라운드 작업 논리가 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-195">A hosted service is a class with background task logic that implements the [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) interface.</span></span> <span data-ttu-id="e4388-196">자세한 내용은 [호스티드 서비스를 사용하는 백그라운드 작업](xref:fundamentals/host/hosted-services) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4388-196">For more information, see the [Background tasks with hosted services](xref:fundamentals/host/hosted-services) topic.</span></span>

<span data-ttu-id="e4388-197">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)은 `AddHostedService` 확장 메서드를 사용하여 수명 이벤트, `LifetimeEventsHostedService` 및 시간 제한 백그라운드 작업에 대한 서비스 `TimedHostedService`를 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-197">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) uses the `AddHostedService` extension method to add a service for lifetime events, `LifetimeEventsHostedService`, and a timed background task, `TimedHostedService`, to the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureServices)]

## <a name="configurelogging"></a><span data-ttu-id="e4388-198">ConfigureLogging</span><span class="sxs-lookup"><span data-stu-id="e4388-198">ConfigureLogging</span></span>

<span data-ttu-id="e4388-199">[ConfigureLogging](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configurelogging)은 제공된 [ILoggingBuilder](/dotnet/api/microsoft.extensions.logging.iloggingbuilder) 구성을 위한 대리자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-199">[ConfigureLogging](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configurelogging) adds a delegate for configuring the provided [ILoggingBuilder](/dotnet/api/microsoft.extensions.logging.iloggingbuilder).</span></span> <span data-ttu-id="e4388-200">`ConfigureLogging` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-200">`ConfigureLogging` may be called multiple times with additive results.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureLogging)]

### <a name="useconsolelifetime"></a><span data-ttu-id="e4388-201">UseConsoleLifetime</span><span class="sxs-lookup"><span data-stu-id="e4388-201">UseConsoleLifetime</span></span>

<span data-ttu-id="e4388-202">[UseConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.useconsolelifetime)은 `Ctrl+C`/SIGINT 또는 SIGTERM을 수신 대기하고 [StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication)을 호출하여 종료 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-202">[UseConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.useconsolelifetime) listens for `Ctrl+C`/SIGINT or SIGTERM and calls [StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication) to start the shutdown process.</span></span> <span data-ttu-id="e4388-203">`UseConsoleLifetime`은 [RunAsync](#runasync) 및 [WaitForShutdownAsync](#waitforshutdownasync)와 같은 확장의 차단을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-203">`UseConsoleLifetime` unblocks extensions such as [RunAsync](#runasync) and [WaitForShutdownAsync](#waitforshutdownasync).</span></span> <span data-ttu-id="e4388-204">[ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime)은 기본 수명 구현으로 미리 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-204">[ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime) is pre-registered as the default lifetime implementation.</span></span> <span data-ttu-id="e4388-205">등록된 마지막 수명이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-205">The last lifetime registered is used.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseConsoleLifetime)]

## <a name="container-configuration"></a><span data-ttu-id="e4388-206">컨테이너 구성</span><span class="sxs-lookup"><span data-stu-id="e4388-206">Container configuration</span></span>

<span data-ttu-id="e4388-207">호스트는 다른 컨테이너 연결을 지원하기 위해 [IServiceProviderFactory](/dotnet/api/microsoft.extensions.dependencyinjection.iserviceproviderfactory-1)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-207">To support plugging in other containers, the host can accept an [IServiceProviderFactory](/dotnet/api/microsoft.extensions.dependencyinjection.iserviceproviderfactory-1).</span></span> <span data-ttu-id="e4388-208">팩터리 제공은 DI 컨테이너 등록의 일부가 아니지만 구체적 DI 컨테이너를 만드는 데 사용되는 내장 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-208">Providing a factory isn't part of the DI container registration but is instead a host intrinsic used to create the concrete DI container.</span></span> <span data-ttu-id="e4388-209">[UseServiceProviderFactory(IServiceProviderFactory&lt;TContainerBuilder&gt;)](/dotnet/api/microsoft.extensions.hosting.hostbuilder.useserviceproviderfactory)는 앱의 서비스 공급자를 만드는 데 사용되는 기본 팩터리를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-209">[UseServiceProviderFactory(IServiceProviderFactory&lt;TContainerBuilder&gt;)](/dotnet/api/microsoft.extensions.hosting.hostbuilder.useserviceproviderfactory) overrides the default factory used to create the app's service provider.</span></span>

<span data-ttu-id="e4388-210">사용자 지정 컨테이너 구성은 [ConfigureContainer](/dotnet/api/microsoft.extensions.hosting.hostbuilder.configurecontainer) 메서드로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-210">Custom container configuration is managed by the [ConfigureContainer](/dotnet/api/microsoft.extensions.hosting.hostbuilder.configurecontainer) method.</span></span> <span data-ttu-id="e4388-211">`ConfigureContainer`는 기본 호스트 API 위에 컨테이너를 구성하기 위한 강력한 형식의 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-211">`ConfigureContainer` provides a strongly-typed experience for configuring the container on top of the underlying host API.</span></span> <span data-ttu-id="e4388-212">`ConfigureContainer` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-212">`ConfigureContainer` can be called multiple times with additive results.</span></span>

<span data-ttu-id="e4388-213">앱에 대한 서비스 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-213">Create a service container for the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/ServiceContainer.cs)]

<span data-ttu-id="e4388-214">서비스 컨테이너 팩터리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-214">Provide a service container factory:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/ServiceContainerFactory.cs)]

<span data-ttu-id="e4388-215">팩터리를 사용하고 앱에 대 한 사용자 지정 서비스 컨테이너를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-215">Use the factory and configure the custom service container for the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ContainerConfiguration)]

## <a name="extensibility"></a><span data-ttu-id="e4388-216">확장성</span><span class="sxs-lookup"><span data-stu-id="e4388-216">Extensibility</span></span>

<span data-ttu-id="e4388-217">`IHostBuilder`에서 확장 메서드를 사용하여 호스트 확장성이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-217">Host extensibility is performed with extension methods on `IHostBuilder`.</span></span> <span data-ttu-id="e4388-218">다음 예에서는 확장 메서드가 [RabbitMQ](https://www.rabbitmq.com/)를 사용하여 `IHostBuilder` 구현을 확장하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-218">The following example shows how an extension method extends an `IHostBuilder` implementation with [RabbitMQ](https://www.rabbitmq.com/).</span></span> <span data-ttu-id="e4388-219">확장 메서드(앱의 다른 곳)는 RabbitMQ `IHostedService`를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-219">The extension method (elsewhere in the app) registers a RabbitMQ `IHostedService`:</span></span>

```csharp
// UseRabbitMq is an extension method that sets up RabbitMQ to handle incoming
// messages.
var host = new HostBuilder()
    .UseRabbitMq<MyMessageHandler>()
    .Build();

await host.StartAsync();
```

## <a name="manage-the-host"></a><span data-ttu-id="e4388-220">호스트 관리</span><span class="sxs-lookup"><span data-stu-id="e4388-220">Manage the host</span></span>

<span data-ttu-id="e4388-221">[IHost](/dotnet/api/microsoft.extensions.hosting.ihost) 구현은 서비스 컨테이너에 등록된 `IHostedService` 구현의 시작 및 중지를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-221">The [IHost](/dotnet/api/microsoft.extensions.hosting.ihost) implementation is responsible for starting and stopping the `IHostedService` implementations that are registered in the service container.</span></span>

### <a name="run"></a><span data-ttu-id="e4388-222">실행</span><span class="sxs-lookup"><span data-stu-id="e4388-222">Run</span></span>

<span data-ttu-id="e4388-223">[Run](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.run)은 앱을 시작하고 호스트가 종료될 때까지 호출 스레드를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-223">[Run](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.run) runs the app and blocks the calling thread until the host is shut down:</span></span>

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

### <a name="runasync"></a><span data-ttu-id="e4388-224">RunAsync</span><span class="sxs-lookup"><span data-stu-id="e4388-224">RunAsync</span></span>

<span data-ttu-id="e4388-225">[RunAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.runasync)는 앱을 실행하고 취소 토큰 또는 종료가 트리거될 때 완료되는 `Task`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-225">[RunAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.runasync) runs the app and returns a `Task` that completes when the cancellation token or shutdown is triggered:</span></span>

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

### <a name="runconsoleasync"></a><span data-ttu-id="e4388-226">RunConsoleAsync</span><span class="sxs-lookup"><span data-stu-id="e4388-226">RunConsoleAsync</span></span>

<span data-ttu-id="e4388-227">[RunConsoleAsync](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.runconsoleasync)는 콘솔 지원을 구현하고, 호스트를 빌드 및 시작하며, `Ctrl+C`/SIGINT 또는 SIGTERM이 종료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-227">[RunConsoleAsync](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.runconsoleasync) enables console support, builds and starts the host, and waits for `Ctrl+C`/SIGINT or SIGTERM to shut down.</span></span>

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

### <a name="start-and-stopasync"></a><span data-ttu-id="e4388-228">Start 및 StopAsync</span><span class="sxs-lookup"><span data-stu-id="e4388-228">Start and StopAsync</span></span>

<span data-ttu-id="e4388-229">[Start](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.start)는 호스트를 동기적으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-229">[Start](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.start) starts the host synchronously.</span></span>

<span data-ttu-id="e4388-230">[StopAsync(TimeSpan)](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.stopasync)는 지정된 시간 제한 내에서 호스트를 중지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-230">[StopAsync(TimeSpan)](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.stopasync) attempts to stop the host within the provided timeout.</span></span>

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

### <a name="startasync-and-stopasync"></a><span data-ttu-id="e4388-231">StartAsync 및 StopAsync</span><span class="sxs-lookup"><span data-stu-id="e4388-231">StartAsync and StopAsync</span></span>

<span data-ttu-id="e4388-232">[StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync)는 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-232">[StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync) starts the app.</span></span>

<span data-ttu-id="e4388-233">[StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync)는 앱을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-233">[StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync) stops the app.</span></span>

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

### <a name="waitforshutdown"></a><span data-ttu-id="e4388-234">WaitForShutdown</span><span class="sxs-lookup"><span data-stu-id="e4388-234">WaitForShutdown</span></span>

<span data-ttu-id="e4388-235">[WaitForShutdown](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdown)은 [ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime)(`Ctrl+C`/SIGINT 또는 SIGTERM 수신 대기)과 같은 [IHostLifetime](/dotnet/api/microsoft.extensions.hosting.ihostlifetime)을 통해 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-235">[WaitForShutdown](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdown) is triggered via the [IHostLifetime](/dotnet/api/microsoft.extensions.hosting.ihostlifetime), such as [ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime) (listens for `Ctrl+C`/SIGINT or SIGTERM).</span></span> <span data-ttu-id="e4388-236">`WaitForShutdown`은 [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-236">`WaitForShutdown` calls [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync).</span></span>

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

### <a name="waitforshutdownasync"></a><span data-ttu-id="e4388-237">WaitForShutdownAsync</span><span class="sxs-lookup"><span data-stu-id="e4388-237">WaitForShutdownAsync</span></span>

<span data-ttu-id="e4388-238">[WaitForShutdownAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdownasync)는 지정된 토큰을 통해 종료가 트리거될 때 완료되는 `Task`를 반환하고 [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-238">[WaitForShutdownAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdownasync) returns a `Task` that completes when shutdown is triggered via the given token and calls [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync).</span></span>

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

### <a name="external-control"></a><span data-ttu-id="e4388-239">외부 제어</span><span class="sxs-lookup"><span data-stu-id="e4388-239">External control</span></span>

<span data-ttu-id="e4388-240">외부에서 호출할 수 있는 메서드를 사용하여 호스트의 외부 제어를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-240">External control of the host can be achieved using methods that can be called externally:</span></span>

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

<span data-ttu-id="e4388-241">[IHostLifetime.WaitForStartAsync](/dotnet/api/microsoft.extensions.hosting.ihostlifetime.waitforstartasync)는 [StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync) 시작 시 호출되고, 완료될 때까지 기다린 후 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-241">[IHostLifetime.WaitForStartAsync](/dotnet/api/microsoft.extensions.hosting.ihostlifetime.waitforstartasync) is called at the start of [StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync), which waits until it's complete before continuing.</span></span> <span data-ttu-id="e4388-242">이는 외부 이벤트에서 신호를 보낼 때까지 시작을 지연시키는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-242">This can be used to delay startup until signaled by an external event.</span></span>

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="e4388-243">IHostingEnvironment 인터페이스</span><span class="sxs-lookup"><span data-stu-id="e4388-243">IHostingEnvironment interface</span></span>

<span data-ttu-id="e4388-244">[IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment)는 앱의 호스팅 환경에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-244">[IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment) provides information about the app's hosting environment.</span></span> <span data-ttu-id="e4388-245">해당 속성 및 확장 메서드를 사용하기 위해 [생성자 주입](xref:fundamentals/dependency-injection)을 사용하여 `IHostingEnvironment`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-245">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

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

<span data-ttu-id="e4388-246">자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4388-246">For more information, see [Use multiple environments](xref:fundamentals/environments).</span></span>

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="e4388-247">IApplicationLifetime 인터페이스</span><span class="sxs-lookup"><span data-stu-id="e4388-247">IApplicationLifetime interface</span></span>

<span data-ttu-id="e4388-248">[IApplicationLifetime](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime)은 점진적인 종료 요청을 비롯한 사후 시작 및 종료 작업을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-248">[IApplicationLifetime](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime) allows for post-startup and shutdown activities, including graceful shutdown requests.</span></span> <span data-ttu-id="e4388-249">인터페이스에서 세 가지 속성은 취소 토큰으로, 시작 및 종료 이벤트를 정의하는 `Action` 메서드를 등록하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-249">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span>

| <span data-ttu-id="e4388-250">취소 토큰</span><span class="sxs-lookup"><span data-stu-id="e4388-250">Cancellation Token</span></span> | <span data-ttu-id="e4388-251">트리거되는 경우:</span><span class="sxs-lookup"><span data-stu-id="e4388-251">Triggered when&#8230;</span></span> |
| ------------------ | --------------------- |
| [<span data-ttu-id="e4388-252">ApplicationStarted</span><span class="sxs-lookup"><span data-stu-id="e4388-252">ApplicationStarted</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstarted) | <span data-ttu-id="e4388-253">호스트가 완벽하게 시작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-253">The host has fully started.</span></span> |
| [<span data-ttu-id="e4388-254">ApplicationStopped</span><span class="sxs-lookup"><span data-stu-id="e4388-254">ApplicationStopped</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopped) | <span data-ttu-id="e4388-255">호스트가 정상적으로 종료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-255">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="e4388-256">모든 요청이 처리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-256">All requests should be processed.</span></span> <span data-ttu-id="e4388-257">종료는 이 이벤트가 완료될 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-257">Shutdown blocks until this event completes.</span></span> |
| [<span data-ttu-id="e4388-258">ApplicationStopping</span><span class="sxs-lookup"><span data-stu-id="e4388-258">ApplicationStopping</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopping) | <span data-ttu-id="e4388-259">호스트가 정상적으로 종료되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-259">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="e4388-260">요청은 계속 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-260">Requests may still be processing.</span></span> <span data-ttu-id="e4388-261">종료는 이 이벤트가 완료될 때까지 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-261">Shutdown blocks until this event completes.</span></span> |

<span data-ttu-id="e4388-262">클래스에 대한 `IApplicationLifetime` 서비스 생성자 주입을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-262">Constructor-inject the `IApplicationLifetime` service into any class.</span></span> <span data-ttu-id="e4388-263">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)은 `LifetimeEventsHostedService` 클래스(`IHostedService` 구현)에 대한 생성자 주입을 통해 이벤트를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-263">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) uses contructor injection into a `LifetimeEventsHostedService` class (an `IHostedService` implementation) to register the events.</span></span>

<span data-ttu-id="e4388-264">*LifetimeEventsHostedService.cs*:</span><span class="sxs-lookup"><span data-stu-id="e4388-264">*LifetimeEventsHostedService.cs*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/LifetimeEventsHostedService.cs?name=snippet1)]

<span data-ttu-id="e4388-265">[StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication)은 앱의 종료를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-265">[StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication) requests termination of the app.</span></span> <span data-ttu-id="e4388-266">다음 클래스에서는 `StopApplication`을 사용하여 해당 클래스의 `Shutdown` 메서드를 호출하는 경우 앱을 정상 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="e4388-266">The following class uses `StopApplication` to gracefully shut down an app when the class's `Shutdown` method is called:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="e4388-267">추가 자료</span><span class="sxs-lookup"><span data-stu-id="e4388-267">Additional resources</span></span>

* [<span data-ttu-id="e4388-268">호스티드 서비스를 사용하는 백그라운드 작업</span><span class="sxs-lookup"><span data-stu-id="e4388-268">Background tasks with hosted services</span></span>](xref:fundamentals/host/hosted-services)
* [<span data-ttu-id="e4388-269">GitHub의 호스팅 리포지토리 샘플</span><span class="sxs-lookup"><span data-stu-id="e4388-269">Hosting repo samples on GitHub</span></span>](https://github.com/aspnet/Hosting/tree/release/2.1/samples)
