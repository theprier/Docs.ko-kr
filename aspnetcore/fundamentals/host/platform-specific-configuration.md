---
title: IHostingStartup을 사용하여 ASP.NET Core의 외부 어셈블리에서 앱 강화
author: guardrex
description: IHostingStartup 구현을 사용하여 외부 어셈블리에서 ASP.NET Core 앱을 강화하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 08/13/2018
uid: fundamentals/configuration/platform-specific-configuration
ms.openlocfilehash: a06c2da04c1631f5811a535c891ca5190b0d8864
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207565"
---
# <a name="enhance-an-app-from-an-external-assembly-in-aspnet-core-with-ihostingstartup"></a><span data-ttu-id="bba60-103">IHostingStartup을 사용하여 ASP.NET Core의 외부 어셈블리에서 앱 강화</span><span class="sxs-lookup"><span data-stu-id="bba60-103">Enhance an app from an external assembly in ASP.NET Core with IHostingStartup</span></span>

<span data-ttu-id="bba60-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="bba60-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="bba60-105">[IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup)(호스팅 시작) 구현에서는 외부 어셈블리에서 시작할 때 앱에 향상된 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-105">An [IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) (hosting startup) implementation adds enhancements to an app at startup from an external assembly.</span></span> <span data-ttu-id="bba60-106">예를 들어 외부 라이브러리는 호스팅 시작 구현을 사용하여 앱에 추가 구성 공급자 또는 서비스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-106">For example, an external library can use a hosting startup implementation to provide additional configuration providers or services to an app.</span></span> <span data-ttu-id="bba60-107">`IHostingStartup` *는 ASP.NET Core 2.0 이상에서 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="bba60-107">`IHostingStartup` *is available in ASP.NET Core 2.0 or later.*</span></span>

<span data-ttu-id="bba60-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="bba60-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="hostingstartup-attribute"></a><span data-ttu-id="bba60-109">HostingStartup 특성</span><span class="sxs-lookup"><span data-stu-id="bba60-109">HostingStartup attribute</span></span>

<span data-ttu-id="bba60-110">[HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 특성은 런타임에 활성화할 호스팅 시작 어셈블리의 현재 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-110">A [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) attribute indicates the presence of a hosting startup assembly to activate at runtime.</span></span>

<span data-ttu-id="bba60-111">항목 어셈블리 또는 `Startup` 클래스가 포함된 어셈블리에서는 `HostingStartup` 특성을 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-111">The entry assembly or the assembly containing the `Startup` class is automatically scanned for the `HostingStartup` attribute.</span></span> <span data-ttu-id="bba60-112">`HostingStartup` 특성을 검색할 어셈블리 목록은 [WebHostDefaults.HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey)의 구성에서 런타임에 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-112">The list of assemblies to search for `HostingStartup` attributes is loaded at runtime from configuration in the [WebHostDefaults.HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey).</span></span> <span data-ttu-id="bba60-113">검색에서 제외할 어셈블리 목록은 [WebHostDefaults.HostingStartupExcludeAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupexcludeassemblieskey)에서 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-113">The list of assemblies to exclude from discovery is loaded from the [WebHostDefaults.HostingStartupExcludeAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupexcludeassemblieskey).</span></span> <span data-ttu-id="bba60-114">자세한 내용은 [웹 호스트: 호스팅 시작 어셈블리](xref:fundamentals/host/web-host#hosting-startup-assemblies) 및 [웹 호스트: 호스팅 시작 어셈블리 제외](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bba60-114">For more information, see [Web Host: Hosting Startup Assemblies](xref:fundamentals/host/web-host#hosting-startup-assemblies) and [Web Host: Hosting Startup Exclude Assemblies](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies).</span></span>

<span data-ttu-id="bba60-115">다음 예제에서는 호스팅 시작 어셈블리의 네임스페이스가 `StartupEnhancement`입니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-115">In the following example, the namespace of the hosting startup assembly is `StartupEnhancement`.</span></span> <span data-ttu-id="bba60-116">호스팅 시작 코드를 포함하는 클래스는 `StartupEnhancementHostingStartup`입니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-116">The class containing the hosting startup code is `StartupEnhancementHostingStartup`:</span></span>

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet1)]

<span data-ttu-id="bba60-117">`HostingStartup` 특성은 일반적으로 호스팅 시작 어셈블리의 `IHostingStartup` 구현 클래스 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-117">The `HostingStartup` attribute is typically located in the hosting startup assembly's `IHostingStartup` implementation class file.</span></span>

## <a name="discover-loaded-hosting-startup-assemblies"></a><span data-ttu-id="bba60-118">로드된 호스팅 시작 어셈블리 검색</span><span class="sxs-lookup"><span data-stu-id="bba60-118">Discover loaded hosting startup assemblies</span></span>

<span data-ttu-id="bba60-119">로드된 호스팅 시작 어셈블리를 검색하려면 로깅을 사용하도록 설정하고 앱의 로그를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-119">To discover loaded hosting startup assemblies, enable logging and check the app's logs.</span></span> <span data-ttu-id="bba60-120">어셈블리를 로드할 때 발생하는 오류가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-120">Errors that occur when loading assemblies are logged.</span></span> <span data-ttu-id="bba60-121">로드된 호스팅 시작 어셈블리는 디버그 수준에서 기록되고 모든 오류가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-121">Loaded hosting startup assemblies are logged at the Debug level, and all errors are logged.</span></span>

## <a name="disable-automatic-loading-of-hosting-startup-assemblies"></a><span data-ttu-id="bba60-122">호스팅 시작 어셈블리의 자동 로드 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="bba60-122">Disable automatic loading of hosting startup assemblies</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="bba60-123">호스팅 시작 어셈블리의 자동 로딩을 사용하지 않으려면 다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-123">To disable automatic loading of hosting startup assemblies, use one of the following approaches:</span></span>

* <span data-ttu-id="bba60-124">모든 호스팅 시작 어셈블리가 로드되지 않도록 하려면 다음 중 하나를 `true` 또는 `1`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-124">To prevent all hosting startup assemblies from loading, set one of the following to `true` or `1`:</span></span>
  * <span data-ttu-id="bba60-125">[호스팅 시작 방지](xref:fundamentals/host/web-host#prevent-hosting-startup) 호스트 구성 설정.</span><span class="sxs-lookup"><span data-stu-id="bba60-125">[Prevent Hosting Startup](xref:fundamentals/host/web-host#prevent-hosting-startup) host configuration setting.</span></span>
  * <span data-ttu-id="bba60-126">`ASPNETCORE_PREVENTHOSTINGSTARTUP` 환경 변수.</span><span class="sxs-lookup"><span data-stu-id="bba60-126">`ASPNETCORE_PREVENTHOSTINGSTARTUP` environment variable.</span></span>
* <span data-ttu-id="bba60-127">특정 호스팅 시작 어셈블리가 로드되지 않도록 하려면 시작 시 제외할 호스팅 시작 어셈블리의 세미콜론으로 구분된 문자열로 다음 중 하나를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-127">To prevent specific hosting startup assemblies from loading, set one of the following to a semicolon-delimited string of hosting startup assemblies to exclude at startup:</span></span>
  * <span data-ttu-id="bba60-128">[호스팅 시작 어셈블리 제외](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies) 호스트 구성 설정.</span><span class="sxs-lookup"><span data-stu-id="bba60-128">[Hosting Startup Exclude Assemblies](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies) host configuration setting.</span></span>
  * <span data-ttu-id="bba60-129">`ASPNETCORE_HOSTINGSTARTUPEXCLUDEASSEMBLIES` 환경 변수.</span><span class="sxs-lookup"><span data-stu-id="bba60-129">`ASPNETCORE_HOSTINGSTARTUPEXCLUDEASSEMBLIES` environment variable.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="bba60-130">호스팅 시작 어셈블리의 자동 로딩을 사용하지 않으려면 다음 방법 중 하나를 `true` 또는 `1`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-130">To disable automatic loading of hosting startup assemblies, set one of the following to `true` or `1`:</span></span>

* <span data-ttu-id="bba60-131">[호스팅 시작 방지](xref:fundamentals/host/web-host#prevent-hosting-startup) 호스트 구성 설정.</span><span class="sxs-lookup"><span data-stu-id="bba60-131">[Prevent Hosting Startup](xref:fundamentals/host/web-host#prevent-hosting-startup) host configuration setting.</span></span>
* <span data-ttu-id="bba60-132">`ASPNETCORE_PREVENTHOSTINGSTARTUP` 환경 변수.</span><span class="sxs-lookup"><span data-stu-id="bba60-132">`ASPNETCORE_PREVENTHOSTINGSTARTUP` environment variable.</span></span>

::: moniker-end

<span data-ttu-id="bba60-133">호스트 구성 설정과 환경 변수가 모두 설정되면 호스트 설정이 동작을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-133">If both the host configuration setting and the environment variable are set, the host setting controls the behavior.</span></span>

<span data-ttu-id="bba60-134">호스트 설정 또는 환경 변수를 사용하여 호스팅 시작 어셈블리를 사용하지 않도록 설정하면 어셈블리가 전역적으로 해제되고 앱의 여러 특징을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-134">Disabling hosting startup assemblies using the host setting or environment variable disables the assembly globally and may disable several characteristics of an app.</span></span>

## <a name="project"></a><span data-ttu-id="bba60-135">프로젝트</span><span class="sxs-lookup"><span data-stu-id="bba60-135">Project</span></span>

<span data-ttu-id="bba60-136">다음 프로젝트 형식 중 하나를 사용하여 호스팅 시작을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-136">Create a hosting startup with either of the following project types:</span></span>

* [<span data-ttu-id="bba60-137">클래스 라이브러리</span><span class="sxs-lookup"><span data-stu-id="bba60-137">Class library</span></span>](#class-library)
* [<span data-ttu-id="bba60-138">진입점 없는 콘솔 앱</span><span class="sxs-lookup"><span data-stu-id="bba60-138">Console app without an entry point</span></span>](#console-app-without-an-entry-point)

### <a name="class-library"></a><span data-ttu-id="bba60-139">클래스 라이브러리</span><span class="sxs-lookup"><span data-stu-id="bba60-139">Class library</span></span>

<span data-ttu-id="bba60-140">클래스 라이브러리에서 호스팅 시작 기능 향상을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-140">A hosting startup enhancement can be provided in a class library.</span></span> <span data-ttu-id="bba60-141">라이브러리에는 `HostingStartup` 특성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-141">The library contains a `HostingStartup` attribute.</span></span>

<span data-ttu-id="bba60-142">[샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)에는 Razor 페이지 앱, *HostingStartupApp* 및 클래스 라이브러리, *HostingStartupLibrary*가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-142">The [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/) includes a Razor Pages app, *HostingStartupApp*, and a class library, *HostingStartupLibrary*.</span></span> <span data-ttu-id="bba60-143">클래스 라이브러리:</span><span class="sxs-lookup"><span data-stu-id="bba60-143">The class library:</span></span>

* <span data-ttu-id="bba60-144">`IHostingStartup`을 구현하는 호스트 시작 클래스(`ServiceKeyInjection`)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-144">Contains a hosting startup class, `ServiceKeyInjection`, which implements `IHostingStartup`.</span></span> <span data-ttu-id="bba60-145">`ServiceKeyInjection`은 메모리 내 구성 공급자([AddInMemoryCollection](/dotnet/api/microsoft.extensions.configuration.memoryconfigurationbuilderextensions.addinmemorycollection))를 사용하여 앱의 구성에 서비스 문자열 쌍을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-145">`ServiceKeyInjection` adds a pair of service strings to the app's configuration using the in-memory configuration provider ([AddInMemoryCollection](/dotnet/api/microsoft.extensions.configuration.memoryconfigurationbuilderextensions.addinmemorycollection)).</span></span>
* <span data-ttu-id="bba60-146">호스팅 시작의 네임스페이스 및 클래스를 식별하는 `HostingStartup` 특성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-146">Includes a `HostingStartup` attribute that identifies the hosting startup's namespace and class.</span></span>

<span data-ttu-id="bba60-147">`ServiceKeyInjection` 클래스의 [구성](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 메서드는 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)를 사용하여 앱에 향상된 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-147">The `ServiceKeyInjection` class's [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) method uses an [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) to add enhancements to an app.</span></span> <span data-ttu-id="bba60-148">호스팅 시작 어셈블리의 `IHostingStartup.Configure`는 사용자 코드로 `Startup.Configure` 전에 런타임에서 호출됩니다. 그러면 사용자 코드가 호스팅 시작 어셈블리에서 제공하는 모든 구성을 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-148">`IHostingStartup.Configure` in the hosting startup assembly is called by the runtime before `Startup.Configure` in user code, which allows user code to overwrite any configuration provided by the hosting startup assembly.</span></span>

<span data-ttu-id="bba60-149">*HostingStartupLibrary/ServiceKeyInjection.cs*:</span><span class="sxs-lookup"><span data-stu-id="bba60-149">*HostingStartupLibrary/ServiceKeyInjection.cs*:</span></span>

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupLibrary/ServiceKeyInjection.cs?name=snippet1)]

<span data-ttu-id="bba60-150">앱의 인덱스 페이지는 클래스 라이브러리의 호스팅 시작 어셈블리에 의해 설정된 두 키에 대한 구성 값을 읽고 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-150">The app's Index page reads and renders the configuration values for the two keys set by the class library's hosting startup assembly:</span></span>

<span data-ttu-id="bba60-151">*HostingStartupApp/Pages/Index.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="bba60-151">*HostingStartupApp/Pages/Index.cshtml.cs*:</span></span>

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupApp/Pages/Index.cshtml.cs?name=snippet1&highlight=5-6,11-12)]

<span data-ttu-id="bba60-152">[샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)에는 별도의 호스팅 시작인 *HostingStartupPackage*를 제공하는 NuGet 패키지 프로젝트도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-152">The [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/) also includes a NuGet package project that provides a separate hosting startup, *HostingStartupPackage*.</span></span> <span data-ttu-id="bba60-153">패키지는 앞에서 설명한 클래스 라이브러리와 같은 특징이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-153">The package has the same characteristics of the class library described earlier.</span></span> <span data-ttu-id="bba60-154">패키지:</span><span class="sxs-lookup"><span data-stu-id="bba60-154">The package:</span></span>

* <span data-ttu-id="bba60-155">`IHostingStartup`을 구현하는 호스트 시작 클래스(`ServiceKeyInjection`)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-155">Contains a hosting startup class, `ServiceKeyInjection`, which implements `IHostingStartup`.</span></span> <span data-ttu-id="bba60-156">`ServiceKeyInjection`은 앱의 구성에 서비스 문자열 쌍을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-156">`ServiceKeyInjection` adds a pair of service strings to the app's configuration.</span></span>
* <span data-ttu-id="bba60-157">`HostingStartup` 특성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-157">Includes a `HostingStartup` attribute.</span></span>

<span data-ttu-id="bba60-158">*HostingStartupPackage/ServiceKeyInjection.cs*:</span><span class="sxs-lookup"><span data-stu-id="bba60-158">*HostingStartupPackage/ServiceKeyInjection.cs*:</span></span>

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupPackage/ServiceKeyInjection.cs?name=snippet1)]

<span data-ttu-id="bba60-159">앱의 인덱스 페이지는 패키지의 호스팅 시작 어셈블리에 의해 설정된 두 키에 대한 구성 값을 읽고 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-159">The app's Index page reads and renders the configuration values for the two keys set by the package's hosting startup assembly:</span></span>

<span data-ttu-id="bba60-160">*HostingStartupApp/Pages/Index.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="bba60-160">*HostingStartupApp/Pages/Index.cshtml.cs*:</span></span>

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupApp/Pages/Index.cshtml.cs?name=snippet1&highlight=7-8,13-14)]

### <a name="console-app-without-an-entry-point"></a><span data-ttu-id="bba60-161">진입점 없는 콘솔 앱</span><span class="sxs-lookup"><span data-stu-id="bba60-161">Console app without an entry point</span></span>

<span data-ttu-id="bba60-162">*이 방법은 .NET Framework가 아닌 .NET Core 앱에서만 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="bba60-162">*This approach is only available for .NET Core apps, not .NET Framework.*</span></span>

<span data-ttu-id="bba60-163">활성화에 대한 컴파일 시간 참조가 필요하지 않은 동적 호스팅 시작 기능 향상은 진입점 없이 콘솔 앱에서 제공될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-163">A dynamic hosting startup enhancement that doesn't require a compile-time reference for activation can be provided in a console app without an entry point.</span></span> <span data-ttu-id="bba60-164">앱에는 `HostingStartup` 특성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-164">The app contains a `HostingStartup` attribute.</span></span> <span data-ttu-id="bba60-165">동적 호스팅 시작을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="bba60-165">To create a dynamic hosting startup:</span></span>

1. <span data-ttu-id="bba60-166">구현 라이브러리는 `IHostingStartup` 구현을 포함하는 클래스에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-166">An implementation library is created from the class that contains the `IHostingStartup` implementation.</span></span> <span data-ttu-id="bba60-167">구현 라이브러리는 기본 패키지로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-167">The implementation library is treated as a normal package.</span></span>
1. <span data-ttu-id="bba60-168">진입점이 없는 콘솔 앱은 구현 라이브러리 패키지를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-168">A console app without an entry point references the implementation library package.</span></span> <span data-ttu-id="bba60-169">콘솔 앱은 다음과 같은 이유로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-169">A console app is used because:</span></span>
   * <span data-ttu-id="bba60-170">종속성 파일은 실행 가능한 앱 자산이므로 라이브러리는 종속성 파일을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-170">A dependencies file is a runnable app asset, so a library can't furnish a dependencies file.</span></span>
   * <span data-ttu-id="bba60-171">라이브러리를 [런타임 패키지 저장소](/dotnet/core/deploying/runtime-store)에 직접 추가할 수 없습니다. 이 저장소에는 공유 런타임을 대상으로 하는 실행 가능한 프로젝트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-171">A library can't be added directly to the [runtime package store](/dotnet/core/deploying/runtime-store), which requires a runnable project that targets the shared runtime.</span></span>
1. <span data-ttu-id="bba60-172">콘솔 앱은 호스팅 시작의 종속성을 얻기 위해 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-172">The console app is published to obtain the hosting startup's dependencies.</span></span> <span data-ttu-id="bba60-173">콘솔 앱을 게시하면 사용되지 않는 종속성이 종속성 파일에서 트리밍됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-173">A consequence of publishing the console app is that unused dependencies are trimmed from the dependencies file.</span></span>
1. <span data-ttu-id="bba60-174">앱 및 해당 종속성 파일이 런타임 패키지 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-174">The app and its dependencies file is placed into the runtime package store.</span></span> <span data-ttu-id="bba60-175">호스팅 시작 어셈블리 및 해당 종속성 파일을 검색하기 위해 한 쌍의 환경 변수에서 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-175">To discover the hosting startup assembly and its dependencies file, they're referenced in a pair of environment variables.</span></span>

<span data-ttu-id="bba60-176">콘솔 앱은 [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) 패키지를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-176">The console app references the [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) package:</span></span>

[!code-xml[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.csproj)]

<span data-ttu-id="bba60-177">[HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 특성은 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost)를 빌드할 때 로드 및 실행을 위해 `IHostingStartup`의 구현으로 클래스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-177">A [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) attribute identifies a class as an implementation of `IHostingStartup` for loading and execution when building the [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost).</span></span> <span data-ttu-id="bba60-178">다음 예제에서 네임스페이스는 `StartupEnhancement`이고 클래스는 `StartupEnhancementHostingStartup`입니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-178">In the following example, the namespace is `StartupEnhancement`, and the class is `StartupEnhancementHostingStartup`:</span></span>

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet1)]

<span data-ttu-id="bba60-179">클래스는 `IHostingStartup`을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-179">A class implements `IHostingStartup`.</span></span> <span data-ttu-id="bba60-180">클래스의 [구성](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 메서드는 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)를 사용하여 앱에 향상된 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-180">The class's [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) method uses an [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) to add enhancements to an app.</span></span> <span data-ttu-id="bba60-181">호스팅 시작 어셈블리의 `IHostingStartup.Configure`는 사용자 코드로 `Startup.Configure` 전에 런타임에서 호출됩니다. 그러면 사용자 코드가 호스팅 시작 어셈블리에서 제공하는 모든 구성을 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-181">`IHostingStartup.Configure` in the hosting startup assembly is called by the runtime before `Startup.Configure` in user code, which allows user code to overwrite any configuration provided by the hosting startup assembly.</span></span>

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet2&highlight=3,5)]

<span data-ttu-id="bba60-182">`IHostingStartup` 프로젝트를 빌드할 때 종속성 파일(*\*.deps.json*)은 어셈블리의 `runtime` 위치를 *bin* 폴더로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-182">When building an `IHostingStartup` project, the dependencies file (*\*.deps.json*) sets the `runtime` location of the assembly to the *bin* folder:</span></span>

[!code-json[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement1.deps.json?range=2-13&highlight=8)]

<span data-ttu-id="bba60-183">파일의 일부만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-183">Only part of the file is shown.</span></span> <span data-ttu-id="bba60-184">이 예제의 어셈블리 이름은 `StartupEnhancement`입니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-184">The assembly name in the example is `StartupEnhancement`.</span></span>

## <a name="specify-the-hosting-startup-assembly"></a><span data-ttu-id="bba60-185">호스팅 시작 어셈블리 지정</span><span class="sxs-lookup"><span data-stu-id="bba60-185">Specify the hosting startup assembly</span></span>

<span data-ttu-id="bba60-186">클래스 라이브러리 또는 콘솔 앱 제공 호스팅 시작의 경우 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 환경 변수에 호스팅 시작 어셈블리 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-186">For either a class library- or console app-supplied hosting startup, specify the hosting startup assembly's name in the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` environment variable.</span></span> <span data-ttu-id="bba60-187">환경 변수는 세미콜론으로 구분된 어셈블리 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-187">The environment variable is a semicolon-delimited list of assemblies.</span></span>

<span data-ttu-id="bba60-188">호스팅 시작 어셈블리만 `HostingStartup` 특성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-188">Only hosting startup assemblies are scanned for the `HostingStartup` attribute.</span></span> <span data-ttu-id="bba60-189">샘플 앱(*HostingStartupApp*)의 경우 앞에서 설명한 호스팅 시작을 검색하기 위해 환경 변수가 다음 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-189">For the sample app, *HostingStartupApp*, to discover the hosting startups described earlier, the environment variable is set to the following value:</span></span>

```
HostingStartupLibrary;HostingStartupPackage;StartupDiagnostics
```

<span data-ttu-id="bba60-190">호스팅 시작 어셈블리는 [호스팅 시작 어셈블리](xref:fundamentals/host/web-host#hosting-startup-assemblies) 호스트 구성 설정을 사용하여 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-190">A hosting startup assembly can also be set using the [Hosting Startup Assemblies](xref:fundamentals/host/web-host#hosting-startup-assemblies) host configuration setting.</span></span>

<span data-ttu-id="bba60-191">여러 개의 호스팅 시작 어셈블이 표시되어 있는 경우 해당 [구성](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 메서드가 어셈블리가 나열되는 순서대로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-191">When multiple hosting startup assembles are present, their [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) methods are executed in the order that the assemblies are listed.</span></span>

## <a name="activation"></a><span data-ttu-id="bba60-192">활성화</span><span class="sxs-lookup"><span data-stu-id="bba60-192">Activation</span></span>

<span data-ttu-id="bba60-193">호스팅 시작 활성화 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-193">Options for hosting startup activation are:</span></span>

* <span data-ttu-id="bba60-194">[런타임 저장소](#runtime-store) &ndash; 활성화에는 활성화를 위한 컴파일 시간 참조가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-194">[Runtime store](#runtime-store) &ndash; Activation doesn't require a compile-time reference for activation.</span></span> <span data-ttu-id="bba60-195">샘플 앱은 호스팅 시작 어셈블리 및 종속성 파일을 *배포* 폴더 안에 배치하여 다중 머신 환경에서 호스팅 시작의 배포를 용이하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-195">The sample app places the hosting startup assembly and dependencies files into a folder, *deployment*, to facilitate deployment of the hosting startup in a multimachine environment.</span></span> <span data-ttu-id="bba60-196">*배포* 폴더에는 호스팅 시작을 사용하도록 배포 시스템에 환경 변수를 만들거나 수정하는 PowerShell 스크립트도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-196">The *deployment* folder also includes a PowerShell script that creates or modifies environment variables on the deployment system to enable the hosting startup.</span></span>
* <span data-ttu-id="bba60-197">활성화에 필요한 컴파일 시간 참조</span><span class="sxs-lookup"><span data-stu-id="bba60-197">Compile-time reference required for activation</span></span>
  * [<span data-ttu-id="bba60-198">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="bba60-198">NuGet package</span></span>](#nuget-package)
  * [<span data-ttu-id="bba60-199">프로젝트 bin 폴더</span><span class="sxs-lookup"><span data-stu-id="bba60-199">Project bin folder</span></span>](#project-bin-folder)

### <a name="runtime-store"></a><span data-ttu-id="bba60-200">런타임 저장소</span><span class="sxs-lookup"><span data-stu-id="bba60-200">Runtime store</span></span>

<span data-ttu-id="bba60-201">호스팅 시작 구현은 [런타임 저장소](/dotnet/core/deploying/runtime-store)에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-201">The hosting startup implementation is placed in the [runtime store](/dotnet/core/deploying/runtime-store).</span></span> <span data-ttu-id="bba60-202">향상된 앱에서는 어셈블리에 대한 컴파일 시간 참조가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-202">A compile-time reference to the assembly isn't required by the enhanced app.</span></span>

<span data-ttu-id="bba60-203">호스팅 시작이 빌드된 후 호스팅 시작의 프로젝트 파일은 [dotnet store](/dotnet/core/tools/dotnet-store) 명령의 매니페스트 파일로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-203">After the hosting startup is built, the hosting startup's project file serves as the manifest file for the [dotnet store](/dotnet/core/tools/dotnet-store) command.</span></span>

```console
dotnet store --manifest <PROJECT_FILE> --runtime <RUNTIME_IDENTIFIER>
```

<span data-ttu-id="bba60-204">이 명령은 사용자 프로필의 런타임 저장소에 공유 프레임워크에 속하지 않는 호스팅 시작 어셈블리 및 기타 종속성을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-204">This command places the hosting startup assembly and other dependencies that aren't part of the shared framework in the user profile's runtime store at:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="bba60-205">Windows</span><span class="sxs-lookup"><span data-stu-id="bba60-205">Windows</span></span>](#tab/windows)

```
%USERPROFILE%\.dotnet\store\x64\<TARGET_FRAMEWORK_MONIKER>\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\<TARGET_FRAMEWORK_MONIKER>\
```

# <a name="macostabmacos"></a>[<span data-ttu-id="bba60-206">macOS</span><span class="sxs-lookup"><span data-stu-id="bba60-206">macOS</span></span>](#tab/macos)

```
/Users/<USER>/.dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

# <a name="linuxtablinux"></a>[<span data-ttu-id="bba60-207">Linux</span><span class="sxs-lookup"><span data-stu-id="bba60-207">Linux</span></span>](#tab/linux)

```
/Users/<USER>/.dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

---

<span data-ttu-id="bba60-208">글로벌 사용을 위한 어셈블리 및 종속성을 배치하려면 다음 경로를 사용하여 `-o|--output` 옵션을 `dotnet store` 명령에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-208">If you desire to place the assembly and dependencies for global use, add the `-o|--output` option to the `dotnet store` command with the following path:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="bba60-209">Windows</span><span class="sxs-lookup"><span data-stu-id="bba60-209">Windows</span></span>](#tab/windows)

```
%PROGRAMFILES%\dotnet\store\x64\<TARGET_FRAMEWORK_MONIKER>\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\<TARGET_FRAMEWORK_MONIKER>\
```

# <a name="macostabmacos"></a>[<span data-ttu-id="bba60-210">macOS</span><span class="sxs-lookup"><span data-stu-id="bba60-210">macOS</span></span>](#tab/macos)

```
/usr/local/share/dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

# <a name="linuxtablinux"></a>[<span data-ttu-id="bba60-211">Linux</span><span class="sxs-lookup"><span data-stu-id="bba60-211">Linux</span></span>](#tab/linux)

```
/usr/local/share/dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

---

<span data-ttu-id="bba60-212">**호스팅 시작의 종속성 파일 수정 및 배치**</span><span class="sxs-lookup"><span data-stu-id="bba60-212">**Modify and place the hosting startup's dependencies file**</span></span>

<span data-ttu-id="bba60-213">런타임 위치는 *\*.deps.json* 파일에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-213">The runtime location is specified in the *\*.deps.json* file.</span></span> <span data-ttu-id="bba60-214">향상된 기능을 활성화하려면 `runtime` 요소가 해당 기능 런타임 어셈블리의 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-214">To activate the enhancement, the `runtime` element must specify the location of the enhancement's runtime assembly.</span></span> <span data-ttu-id="bba60-215">`runtime` 위치의 접두사를 `lib/<TARGET_FRAMEWORK_MONIKER>/`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-215">Prefix the `runtime` location with `lib/<TARGET_FRAMEWORK_MONIKER>/`:</span></span>

[!code-json[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement2.deps.json?range=2-13&highlight=8)]

<span data-ttu-id="bba60-216">샘플 코드(*StartupDiagnostics* 프로젝트)에서 *\*.deps.json*파일의 수정은 [PowerShell](/powershell/scripting/powershell-scripting) 스크립트에 의해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-216">In the sample code (*StartupDiagnostics* project), modification of the *\*.deps.json* file is performed by a [PowerShell](/powershell/scripting/powershell-scripting) script.</span></span> <span data-ttu-id="bba60-217">PowerShell 스크립트는 프로젝트 파일의 빌드 대상에서 자동으로 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-217">The PowerShell script is automatically triggered by a build target in the project file.</span></span>

<span data-ttu-id="bba60-218">이제 구현의 *\*.deps.json* 파일은 액세스할 수 있는 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-218">The implementation's *\*.deps.json* file must be in an accessible location.</span></span>

<span data-ttu-id="bba60-219">사용자별 사용의 경우 파일을 사용자 프로필 `.dotnet` 설정의 *additonalDeps* 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-219">For per-user use, place the file in the *additonalDeps* folder of the user profile's `.dotnet` settings:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="bba60-220">Windows</span><span class="sxs-lookup"><span data-stu-id="bba60-220">Windows</span></span>](#tab/windows)

```
%USERPROFILE%\.dotnet\x64\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\
```

# <a name="macostabmacos"></a>[<span data-ttu-id="bba60-221">macOS</span><span class="sxs-lookup"><span data-stu-id="bba60-221">macOS</span></span>](#tab/macos)

```
/Users/<USER>/.dotnet/x64/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

# <a name="linuxtablinux"></a>[<span data-ttu-id="bba60-222">Linux</span><span class="sxs-lookup"><span data-stu-id="bba60-222">Linux</span></span>](#tab/linux)

```
/Users/<USER>/.dotnet/x64/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

---

<span data-ttu-id="bba60-223">글로벌 사용의 경우 파일을 .NET Core 설치의 *additonalDeps* 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-223">For global use, place the file in the *additonalDeps* folder of the .NET Core installation:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="bba60-224">Windows</span><span class="sxs-lookup"><span data-stu-id="bba60-224">Windows</span></span>](#tab/windows)

```
%PROGRAMFILES%\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\
```

# <a name="macostabmacos"></a>[<span data-ttu-id="bba60-225">macOS</span><span class="sxs-lookup"><span data-stu-id="bba60-225">macOS</span></span>](#tab/macos)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

# <a name="linuxtablinux"></a>[<span data-ttu-id="bba60-226">Linux</span><span class="sxs-lookup"><span data-stu-id="bba60-226">Linux</span></span>](#tab/linux)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

---

<span data-ttu-id="bba60-227">공유 프레임워크 버전은 대상 앱이 사용하는 공유 런타임 버전을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-227">The shared framework version reflects the version of the shared runtime that the target app uses.</span></span> <span data-ttu-id="bba60-228">공유 런타임은 *\*.runtimeconfig.json* 파일에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-228">The shared runtime is shown in the *\*.runtimeconfig.json* file.</span></span> <span data-ttu-id="bba60-229">샘플 앱(*HostingStartupApp*)에서 공유 런타임은 *HostingStartupApp.runtimeconfig.json* 파일에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-229">In the sample app (*HostingStartupApp*), the shared runtime is specified in the *HostingStartupApp.runtimeconfig.json* file.</span></span>

<span data-ttu-id="bba60-230">**호스팅 시작의 종속성 파일 목록**</span><span class="sxs-lookup"><span data-stu-id="bba60-230">**List the hosting startup's dependencies file**</span></span>

<span data-ttu-id="bba60-231">구현의 *\*.deps.json* 파일 위치가 `DOTNET_ADDITIONAL_DEPS` 환경 변수에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-231">The location of the implementation's *\*.deps.json* file is listed in the `DOTNET_ADDITIONAL_DEPS` environment variable.</span></span>

<span data-ttu-id="bba60-232">파일이 사용자 프로필의 *.dotnet* 폴더에 있는 경우 환경 변수의 값을 다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-232">If the file is placed in the user profile's *.dotnet* folder, set the environment variable's value to:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="bba60-233">Windows</span><span class="sxs-lookup"><span data-stu-id="bba60-233">Windows</span></span>](#tab/windows)

```
%USERPROFILE%\.dotnet\x64\additionalDeps\
```

# <a name="macostabmacos"></a>[<span data-ttu-id="bba60-234">macOS</span><span class="sxs-lookup"><span data-stu-id="bba60-234">macOS</span></span>](#tab/macos)

```
/Users/<USER>/.dotnet/x64/additionalDeps/
```

# <a name="linuxtablinux"></a>[<span data-ttu-id="bba60-235">Linux</span><span class="sxs-lookup"><span data-stu-id="bba60-235">Linux</span></span>](#tab/linux)

```
/Users/<USER>/.dotnet/x64/additionalDeps/
```

---

<span data-ttu-id="bba60-236">전역 사용에서 파일을 .NET Core 설치에 배치하는 경우 파일에 전체 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-236">If the file is placed in the .NET Core installation for global use, provide the full path to the file:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="bba60-237">Windows</span><span class="sxs-lookup"><span data-stu-id="bba60-237">Windows</span></span>](#tab/windows)

```
%PROGRAMFILES%\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

# <a name="macostabmacos"></a>[<span data-ttu-id="bba60-238">macOS</span><span class="sxs-lookup"><span data-stu-id="bba60-238">macOS</span></span>](#tab/macos)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

# <a name="linuxtablinux"></a>[<span data-ttu-id="bba60-239">Linux</span><span class="sxs-lookup"><span data-stu-id="bba60-239">Linux</span></span>](#tab/linux)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

---

<span data-ttu-id="bba60-240">샘플 앱(*HostingStartupApp*)이 종속성 파일(*HostingStartupApp.runtimeconfig.json*)을 찾는 경우 종속성 파일은 사용자의 프로필에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-240">For the sample app (*HostingStartupApp*) to find the dependencies file (*HostingStartupApp.runtimeconfig.json*), the dependencies file is placed in the user's profile.</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="bba60-241">Windows</span><span class="sxs-lookup"><span data-stu-id="bba60-241">Windows</span></span>](#tab/windows)

<span data-ttu-id="bba60-242">`DOTNET_ADDITIONAL_DEPS` 환경 변수를 다음 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-242">Set the `DOTNET_ADDITIONAL_DEPS` environment variable to the following value:</span></span>

```
%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\
```

# <a name="macostabmacos"></a>[<span data-ttu-id="bba60-243">macOS</span><span class="sxs-lookup"><span data-stu-id="bba60-243">macOS</span></span>](#tab/macos)

<span data-ttu-id="bba60-244">`DOTNET_ADDITIONAL_DEPS` 환경 변수를 다음 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-244">Set the `DOTNET_ADDITIONAL_DEPS` environment variable to the following value:</span></span>

```
/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/
```

# <a name="linuxtablinux"></a>[<span data-ttu-id="bba60-245">Linux</span><span class="sxs-lookup"><span data-stu-id="bba60-245">Linux</span></span>](#tab/linux)

<span data-ttu-id="bba60-246">`DOTNET_ADDITIONAL_DEPS` 환경 변수를 다음 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-246">Set the `DOTNET_ADDITIONAL_DEPS` environment variable to the following value:</span></span>

```
/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/
```

---

<span data-ttu-id="bba60-247">다양한 운영 체제에 대한 환경 변수를 설정하는 방법의 예제는 [여러 환경 사용](xref:fundamentals/environments)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bba60-247">For examples of how to set environment variables for various operating systems, see [Use multiple environments](xref:fundamentals/environments).</span></span>

<span data-ttu-id="bba60-248">**배포**</span><span class="sxs-lookup"><span data-stu-id="bba60-248">**Deployment**</span></span>

<span data-ttu-id="bba60-249">다중 머신 환경에서 호스팅 시작의 배포를 용이하게 하기 위해 샘플 앱은 다음을 포함하는 게시된 출력에 *배포* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-249">To facilitate the deployment of a hosting startup in a multimachine environment, the sample app creates a *deployment* folder in published output that contains:</span></span>

* <span data-ttu-id="bba60-250">호스팅 시작 어셈블리.</span><span class="sxs-lookup"><span data-stu-id="bba60-250">The hosting startup assembly.</span></span>
* <span data-ttu-id="bba60-251">호스팅 시작 종속성 파일.</span><span class="sxs-lookup"><span data-stu-id="bba60-251">The hosting startup dependencies file.</span></span>
* <span data-ttu-id="bba60-252">호스팅 시작 활성화를 지원하기 위해 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 및 `DOTNET_ADDITIONAL_DEPS`를 만들거나 수정하는 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-252">A PowerShell script that creates or modifies the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` and `DOTNET_ADDITIONAL_DEPS` to support the activation of the hosting startup.</span></span> <span data-ttu-id="bba60-253">배포 시스템의 관리 PowerShell 명령 프롬프트에서 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-253">Run the script from an administrative PowerShell command prompt on the deployment system.</span></span>

### <a name="nuget-package"></a><span data-ttu-id="bba60-254">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="bba60-254">NuGet package</span></span>

<span data-ttu-id="bba60-255">NuGet 패키지에서 호스팅 시작 기능 향상을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-255">A hosting startup enhancement can be provided in a NuGet package.</span></span> <span data-ttu-id="bba60-256">패키지에 `HostingStartup` 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-256">The package has a `HostingStartup` attribute.</span></span> <span data-ttu-id="bba60-257">패키지에서 제공하는 호스팅 시작 형식은 다음 방법 중 하나를 통해 앱에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-257">The hosting startup types provided by the package are made available to the app using either of the following approaches:</span></span>

* <span data-ttu-id="bba60-258">향상된 앱의 프로젝트 파일은 앱의 프로젝트 파일(컴파일 시간 참조)에서 호스팅 시작을 위한 패키지 참조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-258">The enhanced app's project file makes a package reference for the hosting startup in the app's project file (a compile-time reference).</span></span> <span data-ttu-id="bba60-259">이 곳에서 컴파일 시간 참조를 사용하면 호스팅 시작 어셈블리 및 모든 종속성이 앱의 종속성 파일(*\*.deps.json*)에 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-259">With the compile-time reference in place, the hosting startup assembly and all of its dependencies are incorporated into the app's dependency file (*\*.deps.json*).</span></span> <span data-ttu-id="bba60-260">이 방식은 [nuget.org](https://www.nuget.org/)에 게시된 호스팅 시작 어셈블리 패키지에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-260">This approach applies to a hosting startup assembly package published to [nuget.org](https://www.nuget.org/).</span></span>
* <span data-ttu-id="bba60-261">호스팅 시작 종속성 파일은 [런타임 저장소](#runtime-store) 섹션에 설명된 대로 향상된 앱에서 사용할 수 있습니다(컴파일 시간 참조 없이).</span><span class="sxs-lookup"><span data-stu-id="bba60-261">The hosting startup's dependencies file is made available to the enhanced app as described in the [Runtime store](#runtime-store) section (without a compile-time reference).</span></span>

<span data-ttu-id="bba60-262">NuGet 패키지 및 런타임 저장소에 대한 자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bba60-262">For more information on NuGet packages and the runtime store, see the following topics:</span></span>

* [<span data-ttu-id="bba60-263">플랫폼 간 도구로 NuGet 패키지를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="bba60-263">How to Create a NuGet Package with Cross Platform Tools</span></span>](/dotnet/core/deploying/creating-nuget-packages)
* [<span data-ttu-id="bba60-264">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="bba60-264">Publishing packages</span></span>](/nuget/create-packages/publish-a-package)
* [<span data-ttu-id="bba60-265">런타임 패키지 저장소</span><span class="sxs-lookup"><span data-stu-id="bba60-265">Runtime package store</span></span>](/dotnet/core/deploying/runtime-store)

### <a name="project-bin-folder"></a><span data-ttu-id="bba60-266">프로젝트 bin 폴더</span><span class="sxs-lookup"><span data-stu-id="bba60-266">Project bin folder</span></span>

<span data-ttu-id="bba60-267">호스팅 시작 향상 기능은 향상된 앱의 *bin* 배포 어셈블리에 의해 제공될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-267">A hosting startup enhancement can be provided by a *bin*-deployed assembly in the enhanced app.</span></span> <span data-ttu-id="bba60-268">어셈블리에서 제공하는 호스팅 시작 형식은 다음 방법 중 하나를 통해 앱에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-268">The hosting startup types provided by the assembly are made available to the app using either of the following approaches:</span></span>

* <span data-ttu-id="bba60-269">향상된 앱의 프로젝트 파일은 호스팅 시작에 대한 어셈블리 참조를 만듭니다(컴파일 시간 참조).</span><span class="sxs-lookup"><span data-stu-id="bba60-269">The enhanced app's project file makes an assembly reference to the hosting startup (a compile-time reference).</span></span> <span data-ttu-id="bba60-270">이 곳에서 컴파일 시간 참조를 사용하면 호스팅 시작 어셈블리 및 모든 종속성이 앱의 종속성 파일(*\*.deps.json*)에 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-270">With the compile-time reference in place, the hosting startup assembly and all of its dependencies are incorporated into the app's dependency file (*\*.deps.json*).</span></span> <span data-ttu-id="bba60-271">이 방법은 배포 시나리오에서 컴파일된 호스팅 시작 라이브러리의 어셈블리(DLL 파일)를 소비 프로젝트 또는 소비 프로젝트에서 액세스할 수 있는 위치로 이동하도록 요청하고 컴파일 시간 참조가 호스팅 시작 어셈블리에 필요한 경우에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-271">This approach applies when the deployment scenario calls for moving the compiled hosting startup library's assembly (DLL file) to the consuming project or to a location accessible by the consuming project and a compile-time reference is made to the hosting startup's assembly.</span></span>
* <span data-ttu-id="bba60-272">호스팅 시작 종속성 파일은 [런타임 저장소](#runtime-store) 섹션에 설명된 대로 향상된 앱에서 사용할 수 있습니다(컴파일 시간 참조 없이).</span><span class="sxs-lookup"><span data-stu-id="bba60-272">The hosting startup's dependencies file is made available to the enhanced app as described in the [Runtime store](#runtime-store) section (without a compile-time reference).</span></span>

## <a name="sample-code"></a><span data-ttu-id="bba60-273">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="bba60-273">Sample code</span></span>

<span data-ttu-id="bba60-274">[샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)([다운로드 방법](xref:index#how-to-download-a-sample))는 호스팅 시작 구현 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-274">The [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/) ([how to download](xref:index#how-to-download-a-sample)) demonstrates hosting startup implementation scenarios:</span></span>

* <span data-ttu-id="bba60-275">두 개의 호스팅 시작 어셈블리(클래스 라이브러리)는 각각 한 쌍의 메모리 내 구성 키-값 쌍을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-275">Two hosting startup assemblies (class libraries) set a pair of in-memory configuration key-value pairs each:</span></span>
  * <span data-ttu-id="bba60-276">NuGet 패키지(*HostingStartupPackage*)</span><span class="sxs-lookup"><span data-stu-id="bba60-276">NuGet package (*HostingStartupPackage*)</span></span>
  * <span data-ttu-id="bba60-277">클래스 라이브러리(*HostingStartupLibrary*)</span><span class="sxs-lookup"><span data-stu-id="bba60-277">Class library (*HostingStartupLibrary*)</span></span>
* <span data-ttu-id="bba60-278">호스팅 시작은 런타임 저장소 배포 어셈블리에서 활성화됩니다(*StartupDiagnostics*).</span><span class="sxs-lookup"><span data-stu-id="bba60-278">A hosting startup is activated from a runtime store-deployed assembly (*StartupDiagnostics*).</span></span> <span data-ttu-id="bba60-279">어셈블리는 시작 시 다음과 같은 진단 정보를 제공하는 두 개의 미들웨어를 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-279">The assembly adds two middlewares to the app at startup that provide diagnostic information on:</span></span>
  * <span data-ttu-id="bba60-280">등록된 서비스</span><span class="sxs-lookup"><span data-stu-id="bba60-280">Registered services</span></span>
  * <span data-ttu-id="bba60-281">주소(구성표, 호스트, 기본 경로, 경로, 쿼리 문자열)</span><span class="sxs-lookup"><span data-stu-id="bba60-281">Address (scheme, host, path base, path, query string)</span></span>
  * <span data-ttu-id="bba60-282">연결(원격 IP, 원격 포트, 로컬 IP, 로컬 포트, 클라이언트 인증서)</span><span class="sxs-lookup"><span data-stu-id="bba60-282">Connection (remote IP, remote port, local IP, local port, client certificate)</span></span>
  * <span data-ttu-id="bba60-283">요청 헤더</span><span class="sxs-lookup"><span data-stu-id="bba60-283">Request headers</span></span>
  * <span data-ttu-id="bba60-284">환경 변수</span><span class="sxs-lookup"><span data-stu-id="bba60-284">Environment variables</span></span>

<span data-ttu-id="bba60-285">샘플을 실행하려면:</span><span class="sxs-lookup"><span data-stu-id="bba60-285">To run the sample:</span></span>

<span data-ttu-id="bba60-286">**NuGet 패키지에서 활성화**</span><span class="sxs-lookup"><span data-stu-id="bba60-286">**Activation from a NuGet package**</span></span>

1. <span data-ttu-id="bba60-287">[dotnet pack](/dotnet/core/tools/dotnet-pack) 명령을 사용하여 *HostingStartupPackage* 패키지를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-287">Compile the *HostingStartupPackage* package with the [dotnet pack](/dotnet/core/tools/dotnet-pack) command.</span></span>
1. <span data-ttu-id="bba60-288">*HostingStartupPackage* 패키지의 어셈블리 이름을 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 환경 변수에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-288">Add the package's assembly name of the *HostingStartupPackage* to the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` environment variable.</span></span>
1. <span data-ttu-id="bba60-289">앱을 컴파일하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-289">Compile and run the app.</span></span> <span data-ttu-id="bba60-290">패키지 참조가 향상된 앱(컴파일 시간 참조)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-290">A package reference is present in the enhanced app (a compile-time reference).</span></span> <span data-ttu-id="bba60-291">앱의 프로젝트 파일에 있는 `<PropertyGroup>`에서는 패키지 프로젝트의 출력(*../HostingStartupPackage/bin/Debug*)을 패키지 원본으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-291">A `<PropertyGroup>` in the app's project file specifies the package project's output (*../HostingStartupPackage/bin/Debug*) as a package source.</span></span> <span data-ttu-id="bba60-292">이렇게 하면 [nuget.org](https://www.nuget.org/)에 패키지를 업로드하지 않고 패키지를 사용할 수 있습니다. 자세한 내용은 HostingStartupApp의 프로젝트 파일에 있는 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bba60-292">This allows the app to use the package without uploading the package to [nuget.org](https://www.nuget.org/). For more information, see the notes in the HostingStartupApp's project file.</span></span>

   ```xml
   <PropertyGroup>
     <RestoreSources>$(RestoreSources);https://api.nuget.org/v3/index.json;../HostingStartupPackage/bin/Debug</RestoreSources>
   </PropertyGroup>
   ```
1. <span data-ttu-id="bba60-293">인덱스 페이지에 의해 렌더링된 서비스 구성 키 값이 패키지의 `ServiceKeyInjection.Configure` 메서드에서 설정된 값과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-293">Observe that the service configuration key values rendered by the Index page match the values set by the package's `ServiceKeyInjection.Configure` method.</span></span>

<span data-ttu-id="bba60-294">*HostingStartupPackage* 프로젝트를 변경하고 다시 컴파일하는 경우, 로컬 NuGet 패키지 캐시의 선택을 취소하여 *HostingStartupApp*이 로컬 캐시에서 부실 패키지가 아닌 업데이트된 패키지를 수신하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-294">If you make changes to the *HostingStartupPackage* project and recompile it, clear the local NuGet package caches to ensure that the *HostingStartupApp* receives the updated package and not a stale package from the local cache.</span></span> <span data-ttu-id="bba60-295">로컬 NuGet 캐시를 지우려면 다음 [dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-295">To clear the local NuGet caches, execute the following [dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals) command:</span></span>

```console
dotnet nuget locals all --clear
```

<span data-ttu-id="bba60-296">**클래스 라이브러리에서 활성화**</span><span class="sxs-lookup"><span data-stu-id="bba60-296">**Activation from a class library**</span></span>

1. <span data-ttu-id="bba60-297">[dotnet build](/dotnet/core/tools/dotnet-build) 명령을 사용하여 *HostingStartupLibrary* 클래스 라이브러리를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-297">Compile the *HostingStartupLibrary* class library with the [dotnet build](/dotnet/core/tools/dotnet-build) command.</span></span>
1. <span data-ttu-id="bba60-298">*HostingStartupLibrary* 클래스 라이브러리의 어셈블리 이름을 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 환경 변수에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-298">Add the class library's assembly name of *HostingStartupLibrary* to the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` environment variable.</span></span>
1. <span data-ttu-id="bba60-299">*bin* - *HostingStartupLibrary.dll* 파일을 클래스 라이브러리의 컴파일된 출력에서 앱의 *bin/Debug* 폴더로 복사하여 클래스 라이브러리의 어셈블리를 앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-299">*bin*-deploy the class library's assembly to the app by copying the *HostingStartupLibrary.dll* file from the class library's compiled output to the app's *bin/Debug* folder.</span></span>
1. <span data-ttu-id="bba60-300">앱을 컴파일하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-300">Compile and run the app.</span></span> <span data-ttu-id="bba60-301">앱의 프로젝트 파일에 있는 `<ItemGroup>`는 클래스 라이브러리의 어셈블리(*.\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll*) (컴파일 시간 참조)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bba60-301">An `<ItemGroup>` in the app's project file references the class library's assembly (*.\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll*) (a compile-time reference).</span></span> <span data-ttu-id="bba60-302">자세한 내용은 HostingStartupApp의 프로젝트 파일에 있는 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bba60-302">For more information, see the notes in the HostingStartupApp's project file.</span></span>

   ```xml
   <ItemGroup>
     <Reference Include=".\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll">
       <HintPath>.\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll</HintPath>
       <SpecificVersion>False</SpecificVersion>
     </Reference>
   </ItemGroup>
   ```
1. <span data-ttu-id="bba60-303">인덱스 페이지에 의해 렌더링된 서비스 구성 키 값이 클래스 라이브러리의 `ServiceKeyInjection.Configure` 메서드에서 설정된 값과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-303">Observe that the service configuration key values rendered by the Index page match the values set by the class library's `ServiceKeyInjection.Configure` method.</span></span>

<span data-ttu-id="bba60-304">**런타임 저장소 배포 어셈블리에서 활성화**</span><span class="sxs-lookup"><span data-stu-id="bba60-304">**Activation from a runtime store-deployed assembly**</span></span>

1. <span data-ttu-id="bba60-305">*StartupDiagnostics* 프로젝트는 [PowerShell](/powershell/scripting/powershell-scripting)을 사용하여 해당 *StartupDiagnostics.deps.json* 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-305">The *StartupDiagnostics* project uses [PowerShell](/powershell/scripting/powershell-scripting) to modify its *StartupDiagnostics.deps.json* file.</span></span> <span data-ttu-id="bba60-306">PowerShell은 Windows 7 SP1 및 Windows Server 2008 R2 SP1부터 Windows에서 기본적으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-306">PowerShell is installed by default on Windows starting with Windows 7 SP1 and Windows Server 2008 R2 SP1.</span></span> <span data-ttu-id="bba60-307">다른 플랫폼에서 PowerShell을 가져오려면 [Windows PowerShell 설치](/powershell/scripting/setup/installing-powershell#powershell-core)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bba60-307">To obtain PowerShell on other platforms, see [Installing Windows PowerShell](/powershell/scripting/setup/installing-powershell#powershell-core).</span></span>
1. <span data-ttu-id="bba60-308">*StartupDiagnostics* 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-308">Build the *StartupDiagnostics* project.</span></span> <span data-ttu-id="bba60-309">프로젝트를 빌드한 후 프로젝트 파일의 빌드 대상이 자동으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-309">After the project is built, a build target in the project file automatically:</span></span>
   * <span data-ttu-id="bba60-310">PowerShell 스크립트를 트리거하여 *StartupDiagnostics.deps.json* 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-310">Triggers the PowerShell script to modify the *StartupDiagnostics.deps.json* file.</span></span>
   * <span data-ttu-id="bba60-311">*StartupDiagnostics.deps.json* 파일을 사용자 프로필의 *additionalDeps* 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-311">Moves the *StartupDiagnostics.deps.json* file to the user profile's *additionalDeps* folder.</span></span>
1. <span data-ttu-id="bba60-312">호스팅 시작 디렉터리의 명령 프롬프트에서 `dotnet store` 명령을 실행하여 어셈블리 및 해당 종속성을 사용자 프로필의 런타임 저장소에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-312">Execute the `dotnet store` command at a command prompt in the hosting startup's directory to store the assembly and its dependencies in the user profile's runtime store:</span></span>

   ```console
   dotnet store --manifest StartupDiagnostics.csproj --runtime <RID>
   ```
   <span data-ttu-id="bba60-313">Windows의 경우 명령은 `win7-x64` [RID(런타임 식별자)](/dotnet/core/rid-catalog)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-313">For Windows, the command uses the `win7-x64` [runtime identifier (RID)](/dotnet/core/rid-catalog).</span></span> <span data-ttu-id="bba60-314">다른 런타임에 호스팅 시작을 제공할 때 올바른 RID로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-314">When providing the hosting startup for a different runtime, substitute the correct RID.</span></span>
1. <span data-ttu-id="bba60-315">환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-315">Set the environment variables:</span></span>
   * <span data-ttu-id="bba60-316">*StartupDiagnostics*의 어셈블리 이름을 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 환경 변수에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-316">Add the assembly name of *StartupDiagnostics* to the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` environment variable.</span></span>
   * <span data-ttu-id="bba60-317">Windows의 경우 `DOTNET_ADDITIONAL_DEPS` 환경 변수를 `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-317">On Windows, set the `DOTNET_ADDITIONAL_DEPS` environment variable to `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`.</span></span> <span data-ttu-id="bba60-318">Linux/macOS에서는 `DOTNET_ADDITIONAL_DEPS` 환경 변수를 `/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/`로 설정합니다. 여기서 `<USER>`는 호스팅 시작을 포함하는 사용자 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-318">On macOS/Linux, set the `DOTNET_ADDITIONAL_DEPS` environment variable to `/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/`, where `<USER>` is the user profile that contains the hosting startup.</span></span>
1. <span data-ttu-id="bba60-319">샘플 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-319">Run the sample app.</span></span>
1. <span data-ttu-id="bba60-320">`/services` 엔드포인트가 앱의 등록된 서비스를 확인하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-320">Request the `/services` endpoint to see the app's registered services.</span></span> <span data-ttu-id="bba60-321">`/diag` 엔드포인트가 진단 정보를 확인하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="bba60-321">Request the `/diag` endpoint to see the diagnostic information.</span></span>
