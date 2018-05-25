---
title: IHostingStartup을 사용하여 ASP.NET Core의 외부 어셈블리에서 앱 강화
author: guardrex
description: IHostingStartup 구현을 사용하여 외부 어셈블리에서 ASP.NET Core 앱을 강화하는 방법을 알아봅니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 12/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/configuration/platform-specific-configuration
ms.openlocfilehash: 793169b491596cd7326d747a3f19d7fdaf7e2b65
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
# <a name="enhance-an-app-from-an-external-assembly-in-aspnet-core-with-ihostingstartup"></a><span data-ttu-id="2d2b9-103">IHostingStartup을 사용하여 ASP.NET Core의 외부 어셈블리에서 앱 강화</span><span class="sxs-lookup"><span data-stu-id="2d2b9-103">Enhance an app from an external assembly in ASP.NET Core with IHostingStartup</span></span>

<span data-ttu-id="2d2b9-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="2d2b9-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="2d2b9-105">[IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) 구현에서는 시작 시 앱의 `Startup` 클래스 외부에 있는 외부 어셈블리에서 앱에 향상된 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-105">An [IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) implementation allows adding enhancements to an app at startup from an external assembly outside of the app's `Startup` class.</span></span> <span data-ttu-id="2d2b9-106">예를 들어 외부 도구 라이브러리는 `IHostingStartup` 구현을 사용하여 앱에 추가 구성 공급자 또는 서비스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-106">For example, an external tooling library can use an `IHostingStartup` implementation to provide additional configuration providers or services to an app.</span></span> <span data-ttu-id="2d2b9-107">`IHostingStartup` *는 ASP.NET Core 2.0 이상에서 지원됩니다.*</span><span class="sxs-lookup"><span data-stu-id="2d2b9-107">`IHostingStartup` *is available in ASP.NET Core 2.0 and later.*</span></span>

<span data-ttu-id="2d2b9-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/platform-specific-configuration/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="2d2b9-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/platform-specific-configuration/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="discover-loaded-hosting-startup-assemblies"></a><span data-ttu-id="2d2b9-109">로드된 호스팅 시작 어셈블리 검색</span><span class="sxs-lookup"><span data-stu-id="2d2b9-109">Discover loaded hosting startup assemblies</span></span>

<span data-ttu-id="2d2b9-110">앱 또는 라이브러리에서 로드한 호스팅 시작 어셈블리를 검색하려면 로깅을 사용하도록 설정하고 응용 프로그램 로그를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-110">To discover hosting startup assemblies loaded by the app or by libraries, enable logging and check the application logs.</span></span> <span data-ttu-id="2d2b9-111">어셈블리를 로드할 때 발생하는 오류가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-111">Errors that occur when loading assemblies are logged.</span></span> <span data-ttu-id="2d2b9-112">로드된 호스팅 시작 어셈블리는 디버그 수준에서 기록되고 모든 오류가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-112">Loaded hosting startup assemblies are logged at the Debug level, and all errors are logged.</span></span>

<span data-ttu-id="2d2b9-113">샘플 앱은 [HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey)를 `string` 배열로 읽고 앱의 인덱스 페이지에 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-113">The sample app reads the [HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey) into a `string` array and displays the result in the app's Index page:</span></span>

[!code-csharp[](platform-specific-configuration/sample/HostingStartupSample/Pages/Index.cshtml.cs?name=snippet1&highlight=14-16)]

## <a name="disable-automatic-loading-of-hosting-startup-assemblies"></a><span data-ttu-id="2d2b9-114">호스팅 시작 어셈블리의 자동 로드 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="2d2b9-114">Disable automatic loading of hosting startup assemblies</span></span>

<span data-ttu-id="2d2b9-115">호스팅 시작 어셈블리의 자동 로드를 사용하지 않도록 설정하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-115">There are two ways to disable the automatic loading of hosting startup assemblies:</span></span>

* <span data-ttu-id="2d2b9-116">[호스팅 스타트업 방지](xref:fundamentals/host/web-host#prevent-hosting-startup) 호스트 구성 설정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-116">Set the [Prevent Hosting Startup](xref:fundamentals/host/web-host#prevent-hosting-startup) host configuration setting.</span></span>
* <span data-ttu-id="2d2b9-117">`ASPNETCORE_PREVENTHOSTINGSTARTUP` 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-117">Set the `ASPNETCORE_PREVENTHOSTINGSTARTUP` environment variable.</span></span>

<span data-ttu-id="2d2b9-118">호스트 설정 또는 환경 변수를 `true` 또는 `1`로 설정한 경우 호스팅 시작 어셈블리를 자동으로 로드하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-118">When either the host setting or the environment variable is set to `true` or `1`, hosting startup assemblies aren't automatically loaded.</span></span> <span data-ttu-id="2d2b9-119">모두 설정하는 경우 호스트 설정은 동작을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-119">If both are set, the host setting controls the behavior.</span></span>

<span data-ttu-id="2d2b9-120">호스트 설정 및 환경 변수를 사용하여 호스팅 시작 어셈블리를 사용하지 않도록 설정하면 전역적으로 해제되고 앱의 여러 특징을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-120">Disabling hosting startup assemblies using the host setting or environment variable disables them globally and may disable several characteristics of an app.</span></span> <span data-ttu-id="2d2b9-121">현재 라이브러리가 고유한 구성 옵션을 제공하지 않으면 라이브러리에서 추가한 호스팅 시작 어셈블리를 선택적으로 해제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-121">It isn't currently possible to selectively disable a hosting startup assembly added by a library unless the library offers its own configuration option.</span></span> <span data-ttu-id="2d2b9-122">이후 릴리스에서는 호스팅 시작 어셈블리를 선택적으로 해제하는 기능을 제공할 예정입니다([GitHub 문제 aspnet/호스팅 #1243](https://github.com/aspnet/Hosting/pull/1243) 참조).</span><span class="sxs-lookup"><span data-stu-id="2d2b9-122">A future release will offer the ability to selectively disable hosting startup assemblies (see [GitHub issue aspnet/Hosting #1243](https://github.com/aspnet/Hosting/pull/1243)).</span></span>

## <a name="implement-ihostingstartup"></a><span data-ttu-id="2d2b9-123">IHostingStartup 구현</span><span class="sxs-lookup"><span data-stu-id="2d2b9-123">Implement IHostingStartup</span></span>

### <a name="create-the-assembly"></a><span data-ttu-id="2d2b9-124">어셈블리 만들기</span><span class="sxs-lookup"><span data-stu-id="2d2b9-124">Create the assembly</span></span>

<span data-ttu-id="2d2b9-125">`IHostingStartup` 향상 기능은 진입점 없이 콘솔 앱에 따라 어셈블리로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-125">An `IHostingStartup` enhancement is deployed as an assembly based on a console app without an entry point.</span></span> <span data-ttu-id="2d2b9-126">어셈블리는 [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) 패키지를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-126">The assembly references the [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) package:</span></span>

[!code-xml[](platform-specific-configuration/snapshot_sample/StartupEnhancement.csproj)]

<span data-ttu-id="2d2b9-127">[HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 특성은 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost)를 빌드할 때 로드 및 실행을 위해 `IHostingStartup`의 구현으로 클래스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-127">A [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) attribute identifies a class as an implementation of `IHostingStartup` for loading and execution when building the [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost).</span></span> <span data-ttu-id="2d2b9-128">다음 예제에서 네임스페이스는 `StartupEnhancement`이고 클래스는 `StartupEnhancementHostingStartup`입니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-128">In the following example, the namespace is `StartupEnhancement`, and the class is `StartupEnhancementHostingStartup`:</span></span>

[!code-csharp[](platform-specific-configuration/snapshot_sample/StartupEnhancement.cs?name=snippet1)]

<span data-ttu-id="2d2b9-129">클래스는 `IHostingStartup`을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-129">A class implements `IHostingStartup`.</span></span> <span data-ttu-id="2d2b9-130">클래스의 [구성](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 메서드는 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)를 사용하여 앱에 향상된 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-130">The class's [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) method uses an [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) to add enhancements to an app:</span></span>

[!code-csharp[](platform-specific-configuration/snapshot_sample/StartupEnhancement.cs?name=snippet2&highlight=3,5)]

<span data-ttu-id="2d2b9-131">`IHostingStartup` 프로젝트를 빌드할 때 종속성 파일(*\*.deps.json*)은 어셈블리의 `runtime` 위치를 *bin* 폴더로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-131">When building an `IHostingStartup` project, the dependencies file (*\*.deps.json*) sets the `runtime` location of the assembly to the *bin* folder:</span></span>

[!code-json[](platform-specific-configuration/snapshot_sample/StartupEnhancement1.deps.json?range=2-13&highlight=8)]

<span data-ttu-id="2d2b9-132">파일의 일부만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-132">Only part of the file is shown.</span></span> <span data-ttu-id="2d2b9-133">이 예제의 어셈블리 이름은 `StartupEnhancement`입니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-133">The assembly name in the example is `StartupEnhancement`.</span></span>

### <a name="update-the-dependencies-file"></a><span data-ttu-id="2d2b9-134">종속성 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="2d2b9-134">Update the dependencies file</span></span>

<span data-ttu-id="2d2b9-135">런타임 위치는 *\*.deps.json* 파일에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-135">The runtime location is specified in the *\*.deps.json* file.</span></span> <span data-ttu-id="2d2b9-136">향상된 기능을 활성화하려면 `runtime` 요소가 해당 기능 런타임 어셈블리의 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-136">To active the enhancement, the `runtime` element must specify the location of the enhancement's runtime assembly.</span></span> <span data-ttu-id="2d2b9-137">`runtime` 위치의 접두사를 `lib/netcoreapp2.0/`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-137">Prefix the `runtime` location with `lib/netcoreapp2.0/`:</span></span>

[!code-json[](platform-specific-configuration/snapshot_sample/StartupEnhancement2.deps.json?range=2-13&highlight=8)]

<span data-ttu-id="2d2b9-138">샘플 앱에서 *\*.deps.json* 파일은 [PowerShell](/powershell/scripting/powershell-scripting) 스크립트에 의해 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-138">In the sample app, modification of the *\*.deps.json* file is performed by a [PowerShell](/powershell/scripting/powershell-scripting) script.</span></span> <span data-ttu-id="2d2b9-139">PowerShell 스크립트는 프로젝트 파일의 빌드 대상에서 자동으로 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-139">The PowerShell script is automatically triggered by a build target in the project file.</span></span>

### <a name="enhancement-activation"></a><span data-ttu-id="2d2b9-140">향상된 기능 활성화</span><span class="sxs-lookup"><span data-stu-id="2d2b9-140">Enhancement activation</span></span>

<span data-ttu-id="2d2b9-141">**어셈블리 파일 배치**</span><span class="sxs-lookup"><span data-stu-id="2d2b9-141">**Place the assembly file**</span></span>

<span data-ttu-id="2d2b9-142">`IHostingStartup` 구현의 어셈블리 파일은 앱에 배포되거나 [런타임 저장소](/dotnet/core/deploying/runtime-store)에 배치된 *bin*이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-142">The `IHostingStartup` implementation's assembly file must be *bin*-deployed in the app or placed in the [runtime store](/dotnet/core/deploying/runtime-store):</span></span>

<span data-ttu-id="2d2b9-143">사용자 단위 사용의 경우 어셈블리를 사용자 프로필의 런타임 저장소에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-143">For per-user use, place the assembly in the user profile's runtime store at:</span></span>

```
<DRIVE>\Users\<USER>\.dotnet\store\x64\netcoreapp2.0\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\netcoreapp2.0\
```

<span data-ttu-id="2d2b9-144">전역 사용의 경우 어셈블리를 .NET Core 설치의 런타임 저장소에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-144">For global use, place the assembly in the .NET Core installation's runtime store:</span></span>

```
<DRIVE>\Program Files\dotnet\store\x64\netcoreapp2.0\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\netcoreapp2.0\
```

<span data-ttu-id="2d2b9-145">런타임 저장소에 어셈블리를 배포할 때 기호 파일도 배포될 수 있지만 향상된 기능이 작동하는 데 필수 조건은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-145">When deploying the assembly to the runtime store, the symbols file may be deployed as well but isn't required for the enhancement to work.</span></span>

<span data-ttu-id="2d2b9-146">**종속성 파일 배치**</span><span class="sxs-lookup"><span data-stu-id="2d2b9-146">**Place the dependencies file**</span></span>

<span data-ttu-id="2d2b9-147">이제 구현의 *\*.deps.json* 파일은 액세스할 수 있는 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-147">The implementation's *\*.deps.json* file must be in an accessible location.</span></span>

<span data-ttu-id="2d2b9-148">사용자 단위 사용의 경우 파일을 사용자 프로필 `.dotnet` 설정의 `additonalDeps` 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-148">For per-user use, place the file in the `additonalDeps` folder of the user profile's `.dotnet` settings:</span></span> 

```
<DRIVE>\Users\<USER>\.dotnet\x64\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\2.0.0\
```

<span data-ttu-id="2d2b9-149">전역 사용의 경우 파일을 .NET Core 설치의 `additonalDeps` 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-149">For global use, place the file in the `additonalDeps` folder of the .NET Core installation:</span></span>

```
<DRIVE>\Program Files\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\2.0.0\
```

<span data-ttu-id="2d2b9-150">버전(`2.0.0`)을 적어두고, 대상 앱이 사용하는 공유 런타임 버전을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-150">Note the version, `2.0.0`, reflects the version of the shared runtime that the target app uses.</span></span> <span data-ttu-id="2d2b9-151">공유 런타임은 *\*.runtimeconfig.json* 파일에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-151">The shared runtime is shown in the *\*.runtimeconfig.json* file.</span></span> <span data-ttu-id="2d2b9-152">샘플 앱에서 공유 런타임은 *HostingStartupSample.runtimeconfig.json* 파일에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-152">In the sample app, the shared runtime is specified in the *HostingStartupSample.runtimeconfig.json* file.</span></span>

<span data-ttu-id="2d2b9-153">**환경 변수 설정**</span><span class="sxs-lookup"><span data-stu-id="2d2b9-153">**Set environment variables**</span></span>

<span data-ttu-id="2d2b9-154">향상된 기능을 사용하는 앱의 컨텍스트에서 다음 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-154">Set the following environment variables in the context of the app that uses the enhancement.</span></span>

<span data-ttu-id="2d2b9-155">ASPNETCORE\_HOSTINGSTARTUPASSEMBLIES</span><span class="sxs-lookup"><span data-stu-id="2d2b9-155">ASPNETCORE\_HOSTINGSTARTUPASSEMBLIES</span></span>

<span data-ttu-id="2d2b9-156">호스팅 시작 어셈블리만이 `HostingStartupAttribute`을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-156">Only hosting startup assemblies are scanned for the `HostingStartupAttribute`.</span></span> <span data-ttu-id="2d2b9-157">구현의 어셈블리 이름은 이 환경 변수에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-157">The assembly name of the implementation is provided in this environment variable.</span></span> <span data-ttu-id="2d2b9-158">샘플 앱은 이 값을 `StartupDiagnostics`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-158">The sample app sets this value to `StartupDiagnostics`.</span></span>

<span data-ttu-id="2d2b9-159">[호스팅 스타트업 어셈블리](xref:fundamentals/host/web-host#hosting-startup-assemblies) 호스트 구성 설정을 사용하여 값을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-159">The value can also be set using the [Hosting Startup Assemblies](xref:fundamentals/host/web-host#hosting-startup-assemblies) host configuration setting.</span></span>

<span data-ttu-id="2d2b9-160">DOTNET\_ADDITIONAL\_DEPS</span><span class="sxs-lookup"><span data-stu-id="2d2b9-160">DOTNET\_ADDITIONAL\_DEPS</span></span>

<span data-ttu-id="2d2b9-161">구현 *\*.deps.json* 파일의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-161">The location of the implementation's *\*.deps.json* file.</span></span>

<span data-ttu-id="2d2b9-162">사용자 단위 사용에서 파일이 사용자 프로필의 *.dotnet* 폴더에 배치되는 경우:</span><span class="sxs-lookup"><span data-stu-id="2d2b9-162">If the file is placed in the user profile's *.dotnet* folder for per-user use:</span></span>

```
<DRIVE>\Users\<USER>\.dotnet\x64\additionalDeps\
```

<span data-ttu-id="2d2b9-163">전역 사용에서 파일을 .NET Core 설치에 배치하는 경우 파일에 전체 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-163">If the file is placed in the .NET Core installation for global use, provide the full path to the file:</span></span>

```
<DRIVE>\Program Files\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\2.0.0\<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

<span data-ttu-id="2d2b9-164">샘플 앱은 이 값을 다음으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-164">The sample app sets this value to:</span></span>

```
%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\
```

<span data-ttu-id="2d2b9-165">다양한 운영 체제에 대한 환경 변수를 설정하는 방법의 예제는 [여러 환경 사용](xref:fundamentals/environments)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-165">For examples of how to set environment variables for various operating systems, see [Use multiple environments](xref:fundamentals/environments).</span></span>

## <a name="sample-app"></a><span data-ttu-id="2d2b9-166">샘플 앱</span><span class="sxs-lookup"><span data-stu-id="2d2b9-166">Sample app</span></span>

<span data-ttu-id="2d2b9-167">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/platform-specific-configuration/sample/)([다운로드하는 방법](xref:tutorials/index#how-to-download-a-sample))은 `IHostingStartup`를 사용하여 진단 도구를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-167">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/platform-specific-configuration/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)) uses `IHostingStartup` to create a diagnostics tool.</span></span> <span data-ttu-id="2d2b9-168">도구는 시작 시 앱에 진단 정보를 제공하는 두 개의 미들웨어를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-168">The tool adds two middlewares to the app at startup that provide diagnostic information:</span></span>

* <span data-ttu-id="2d2b9-169">등록된 서비스</span><span class="sxs-lookup"><span data-stu-id="2d2b9-169">Registered services</span></span>
* <span data-ttu-id="2d2b9-170">주소: 구성표, 호스트, 기본 경로, 경로, 쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="2d2b9-170">Address: scheme, host, path base, path, query string</span></span>
* <span data-ttu-id="2d2b9-171">연결: 원격 IP, 원격 포트, 로컬 IP, 로컬 포트, 클라이언트 인증서</span><span class="sxs-lookup"><span data-stu-id="2d2b9-171">Connection: remote IP, remote port, local IP, local port, client certificate</span></span>
* <span data-ttu-id="2d2b9-172">요청 헤더</span><span class="sxs-lookup"><span data-stu-id="2d2b9-172">Request headers</span></span>
* <span data-ttu-id="2d2b9-173">환경 변수</span><span class="sxs-lookup"><span data-stu-id="2d2b9-173">Environment variables</span></span>

<span data-ttu-id="2d2b9-174">샘플을 실행하려면:</span><span class="sxs-lookup"><span data-stu-id="2d2b9-174">To run the sample:</span></span>

1. <span data-ttu-id="2d2b9-175">스타트업 진단 프로젝트는 [PowerShell](/powershell/scripting/powershell-scripting)을 사용하여 해당 *StartupDiagnostics.deps.json* 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-175">The Startup Diagnostic project uses [PowerShell](/powershell/scripting/powershell-scripting) to modify its *StartupDiagnostics.deps.json* file.</span></span> <span data-ttu-id="2d2b9-176">PowerShell은 Windows 7 SP1 및 Windows Server 2008 R2 SP1부터 Windows OS에서 기본적으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-176">PowerShell is installed by default on Windows OS starting with Windows 7 SP1 and Windows Server 2008 R2 SP1.</span></span> <span data-ttu-id="2d2b9-177">다른 플랫폼에서 PowerShell을 가져오려면 [Windows PowerShell 설치](/powershell/scripting/setup/installing-windows-powershell)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-177">To obtain PowerShell on other platforms, see [Installing Windows PowerShell](/powershell/scripting/setup/installing-windows-powershell).</span></span>
2. <span data-ttu-id="2d2b9-178">스타트업 진단 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-178">Build the Startup Diagnostic project.</span></span> <span data-ttu-id="2d2b9-179">프로젝트 파일의 빌드 대상:</span><span class="sxs-lookup"><span data-stu-id="2d2b9-179">A build target in the project file:</span></span>
   * <span data-ttu-id="2d2b9-180">어셈블리 및 기호 파일을 사용자 프로필의 런타임 저장소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-180">Moves the assembly and symbols files to the user profile's runtime store.</span></span>
   * <span data-ttu-id="2d2b9-181">PowerShell 스크립트를 트리거하여 *StartupDiagnostics.deps.json* 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-181">Triggers the PowerShell script to modify the *StartupDiagnostics.deps.json* file.</span></span>
   * <span data-ttu-id="2d2b9-182">*StartupDiagnostics.deps.json* 파일을 사용자 프로필의 `additionalDeps` 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-182">Moves the *StartupDiagnostics.deps.json* file to the user profile's `additionalDeps` folder.</span></span>
3. <span data-ttu-id="2d2b9-183">환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-183">Set the environment variables:</span></span>
    * <span data-ttu-id="2d2b9-184">`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`: `StartupDiagnostics`</span><span class="sxs-lookup"><span data-stu-id="2d2b9-184">`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`: `StartupDiagnostics`</span></span>
    * <span data-ttu-id="2d2b9-185">`DOTNET_ADDITIONAL_DEPS`: `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`</span><span class="sxs-lookup"><span data-stu-id="2d2b9-185">`DOTNET_ADDITIONAL_DEPS`: `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`</span></span>
4. <span data-ttu-id="2d2b9-186">샘플 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-186">Run the sample app.</span></span>
5. <span data-ttu-id="2d2b9-187">`/services` 엔드포인트가 앱의 등록된 서비스를 확인하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-187">Request the `/services` endpoint to see the app's registered services.</span></span> <span data-ttu-id="2d2b9-188">`/diag` 엔드포인트가 진단 정보를 확인하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2b9-188">Request the `/diag` endpoint to see the diagnostic information.</span></span>
