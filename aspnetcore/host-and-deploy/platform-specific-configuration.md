---
title: "ASP.NET Core에서 플랫폼 관련 구성을 사용 하 여 앱 기능 추가"
author: guardrex
description: "IHostingStartup 구현을 사용 하 여 외부 어셈블리의 기능을 ASP.NET Core 응용 프로그램을 추가 하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 12/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/platform-specific-configuration
ms.openlocfilehash: 2663cd1e05be9e8695966df959082e6e574d0b4a
ms.sourcegitcommit: 809ee4baf8bf7b4cae9e366ecae29de1037d2bbb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="add-app-features-using-a-platform-specific-configuration-in-aspnet-core"></a><span data-ttu-id="cf67c-103">ASP.NET Core에서 플랫폼 관련 구성을 사용 하 여 앱 기능 추가</span><span class="sxs-lookup"><span data-stu-id="cf67c-103">Add app features using a platform-specific configuration in ASP.NET Core</span></span>

<span data-ttu-id="cf67c-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="cf67c-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="cf67c-105">[IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) 구현 하면 응용 프로그램의 외부 어셈블리 외부에서 시작 시 응용 프로그램에 기능 추가 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-105">An [IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) implementation allows adding features to an app at startup from an external assembly outside of the app's `Startup` class.</span></span> <span data-ttu-id="cf67c-106">예를 들어 외부 도구 라이브러리 사용할 수는 `IHostingStartup` 구현을 추가 하는 구성 공급자 또는 응용 프로그램 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-106">For example, an external tooling library can use an `IHostingStartup` implementation to provide additional configuration providers or services to an app.</span></span> <span data-ttu-id="cf67c-107">`IHostingStartup` *이상에서 ASP.NET Core 2.0에서 사용할 수는 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="cf67c-107">`IHostingStartup` *is available in ASP.NET Core 2.0 and later.*</span></span>

<span data-ttu-id="cf67c-108">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/platform-specific-configuration/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="cf67c-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/platform-specific-configuration/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="discover-loaded-hosting-startup-assemblies"></a><span data-ttu-id="cf67c-109">로드 된 호스팅 시작 어셈블리를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-109">Discover loaded hosting startup assemblies</span></span>

<span data-ttu-id="cf67c-110">응용 프로그램에서 또는 라이브러리를 통해 로드 호스팅 시작 어셈블리를 검색 하려면 로깅을 사용 하도록 설정 하 고 응용 프로그램 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-110">To discover hosting startup assemblies loaded by the app or by libraries, enable logging and check the application logs.</span></span> <span data-ttu-id="cf67c-111">어셈블리를 로드할 때 발생 하는 오류가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-111">Errors that occur when loading assemblies are logged.</span></span> <span data-ttu-id="cf67c-112">로드 된 호스팅 시작 어셈블리 디버그 수준에서 로깅됩니다 및 모든 오류가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-112">Loaded hosting startup assemblies are logged at the Debug level, and all errors are logged.</span></span>

<span data-ttu-id="cf67c-113">샘플 응용 프로그램 읽기는 [HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey) 에 `string` 배열 하 고 응용 프로그램의 인덱스 페이지에 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-113">The sample app reads the [HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey) into a `string` array and displays the result in the app's Index page:</span></span>

[!code-csharp[Main](platform-specific-configuration/sample/HostingStartupSample/Pages/Index.cshtml.cs?name=snippet1&highlight=14-16)]

## <a name="disable-automatic-loading-of-hosting-startup-assemblies"></a><span data-ttu-id="cf67c-114">호스팅 시작 어셈블리의 자동 로드 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="cf67c-114">Disable automatic loading of hosting startup assemblies</span></span>

<span data-ttu-id="cf67c-115">호스팅 시작 어셈블리의 자동 로드를 사용 하지 않도록 설정 하는 두 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-115">There are two ways to disable the automatic loading of hosting startup assemblies:</span></span>

* <span data-ttu-id="cf67c-116">설정의 [호스팅 시작 방지](xref:fundamentals/hosting#prevent-hosting-startup) 호스트 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-116">Set the [Prevent Hosting Startup](xref:fundamentals/hosting#prevent-hosting-startup) host configuration setting.</span></span>
* <span data-ttu-id="cf67c-117">설정의 `ASPNETCORE_preventHostingStartup` 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-117">Set the `ASPNETCORE_preventHostingStartup` environment variable.</span></span>

<span data-ttu-id="cf67c-118">호스트 설정 또는 환경 변수로 설정 된 경우 `true` 또는 `1`호스팅, 시작 어셈블리를 자동으로 로드 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-118">When either the host setting or the environment variable is set to `true` or `1`, hosting startup assemblies aren't automatically loaded.</span></span> <span data-ttu-id="cf67c-119">모두 설정 하는 경우 호스트 설정 동작을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-119">If both are set, the host setting controls the behavior.</span></span>

<span data-ttu-id="cf67c-120">호스트 설정 및 환경 변수를 사용 하 여 호스팅 시작 어셈블리를 사용 하지 않도록 설정에 전체적으로 비활성화 하 고 응용 프로그램의 몇 가지 기능을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-120">Disabling hosting startup assemblies using the host setting or environment variable disables them globally and may disable several features of an app.</span></span> <span data-ttu-id="cf67c-121">현재 라이브러리 자체 구성 옵션에서 제공 하지 않으면 라이브러리에서 추가 호스팅 시작 어셈블리를 선택적으로 해제 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-121">It isn't currently possible to selectively disable a hosting startup assembly added by a library unless the library offers its own configuration option.</span></span> <span data-ttu-id="cf67c-122">이후 릴리스에서 호스팅 시작 어셈블리를 선택적으로 해제 하는 기능을 제공할 (참조 [GitHub 발급 aspnet/호스팅 #1243](https://github.com/aspnet/Hosting/pull/1243)).</span><span class="sxs-lookup"><span data-stu-id="cf67c-122">A future release will offer the ability to selectively disable hosting startup assemblies (see [GitHub issue aspnet/Hosting #1243](https://github.com/aspnet/Hosting/pull/1243)).</span></span>

## <a name="implement-ihostingstartup-features"></a><span data-ttu-id="cf67c-123">IHostingStartup 기능 구현</span><span class="sxs-lookup"><span data-stu-id="cf67c-123">Implement IHostingStartup features</span></span>

### <a name="create-the-assembly"></a><span data-ttu-id="cf67c-124">어셈블리 만들기</span><span class="sxs-lookup"><span data-stu-id="cf67c-124">Create the assembly</span></span>

<span data-ttu-id="cf67c-125">`IHostingStartup` 기능은 진입점 하지 않고 콘솔 응용 프로그램에 따라 어셈블리도 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-125">An `IHostingStartup` feature is deployed as an assembly based on a console app without an entry point.</span></span> <span data-ttu-id="cf67c-126">어셈블리 참조는 [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) 패키지:</span><span class="sxs-lookup"><span data-stu-id="cf67c-126">The assembly references the [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) package:</span></span>

[!code-xml[Main](platform-specific-configuration/snapshot_sample/StartupFeature.csproj)]

<span data-ttu-id="cf67c-127">A [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 의 구현으로 클래스를 식별 하는 특성 `IHostingStartup` 로드 및 빌드할 때 실행을 위한는 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost)합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-127">A [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) attribute identifies a class as an implementation of `IHostingStartup` for loading and execution when building the [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost).</span></span> <span data-ttu-id="cf67c-128">다음 예제에서는 네임 스페이스는 `StartupFeature`, 고 클래스는 `StartupFeatureHostingStartup`:</span><span class="sxs-lookup"><span data-stu-id="cf67c-128">In the following example, the namespace is `StartupFeature`, and the class is `StartupFeatureHostingStartup`:</span></span>

[!code-csharp[Main](platform-specific-configuration/snapshot_sample/StartupFeature.cs?name=snippet1)]

<span data-ttu-id="cf67c-129">클래스가 구현 하는 `IHostingStartup`합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-129">A class implements `IHostingStartup`.</span></span> <span data-ttu-id="cf67c-130">클래스의 [구성](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 메서드는 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 기능 응용 프로그램을 추가 하려면:</span><span class="sxs-lookup"><span data-stu-id="cf67c-130">The class's [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) method uses an [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) to add features to an app:</span></span>

[!code-csharp[Main](platform-specific-configuration/snapshot_sample/StartupFeature.cs?name=snippet2&highlight=3,5)]

<span data-ttu-id="cf67c-131">빌드할 때는 `IHostingStartup` 프로젝트, 종속성 파일 (*\*. deps.json*) 설정 하는 `runtime` 어셈블리의 위치는 *bin* 폴더:</span><span class="sxs-lookup"><span data-stu-id="cf67c-131">When building an `IHostingStartup` project, the dependencies file (*\*.deps.json*) sets the `runtime` location of the assembly to the *bin* folder:</span></span>

[!code-json[Main](platform-specific-configuration/snapshot_sample/StartupFeature1.deps.json?range=2-13&highlight=8)]

<span data-ttu-id="cf67c-132">파일의 일부만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-132">Only part of the file is shown.</span></span> <span data-ttu-id="cf67c-133">이 예제에 어셈블리 이름이 `StartupFeature`합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-133">The assembly name in the example is `StartupFeature`.</span></span>

### <a name="update-the-dependencies-file"></a><span data-ttu-id="cf67c-134">종속성 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="cf67c-134">Update the dependencies file</span></span>

<span data-ttu-id="cf67c-135">에 지정 된 런타임 위치는  *\*. deps.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-135">The runtime location is specified in the *\*.deps.json* file.</span></span> <span data-ttu-id="cf67c-136">기능을 활성는 `runtime` 요소 기능의 런타임 어셈블리의 위치를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-136">To active the feature, the `runtime` element must specify the location of the feature's runtime assembly.</span></span> <span data-ttu-id="cf67c-137">접두사는 `runtime` 위치 `lib/netcoreapp2.0/`:</span><span class="sxs-lookup"><span data-stu-id="cf67c-137">Prefix the `runtime` location with `lib/netcoreapp2.0/`:</span></span>

[!code-json[Main](platform-specific-configuration/snapshot_sample/StartupFeature2.deps.json?range=2-13&highlight=8)]

<span data-ttu-id="cf67c-138">샘플 응용 프로그램의 수정 된  *\*. deps.json* 파일에 의해 수행 됩니다는 [PowerShell](/powershell/scripting/powershell-scripting) 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-138">In the sample app, modification of the *\*.deps.json* file is performed by a [PowerShell](/powershell/scripting/powershell-scripting) script.</span></span> <span data-ttu-id="cf67c-139">PowerShell 스크립트는 프로젝트 파일의 빌드 대상에서 자동으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-139">The PowerShell script is automatically triggered by a build target in the project file.</span></span>

### <a name="feature-activation"></a><span data-ttu-id="cf67c-140">기능 활성화</span><span class="sxs-lookup"><span data-stu-id="cf67c-140">Feature activation</span></span>

<span data-ttu-id="cf67c-141">**어셈블리 파일을 배치**</span><span class="sxs-lookup"><span data-stu-id="cf67c-141">**Place the assembly file**</span></span>

<span data-ttu-id="cf67c-142">`IHostingStartup` 구현의 어셈블리 파일이 있어야 *bin*-응용 프로그램에 배포 또는에 [런타임 저장소](/dotnet/core/deploying/runtime-store):</span><span class="sxs-lookup"><span data-stu-id="cf67c-142">The `IHostingStartup` implementation's assembly file must be *bin*-deployed in the app or placed in the [runtime store](/dotnet/core/deploying/runtime-store):</span></span>

<span data-ttu-id="cf67c-143">사용자 단위 사용에 대 한 어셈블리에서 사용자 프로필의 런타임 저장소에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-143">For per-user use, place the assembly in the user profile's runtime store at:</span></span>

```
<DRIVE>\Users\<USER>\.dotnet\store\x64\netcoreapp2.0\<FEATURE_ASSEMBLY_NAME>\<FEATURE_VERSION>\lib\netcoreapp2.0\
```

<span data-ttu-id="cf67c-144">전역 사용에 대 한 어셈블리의.NET Core 설치 런타임 저장소에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-144">For global use, place the assembly in the .NET Core installation's runtime store:</span></span>

```
<DRIVE>\Program Files\dotnet\store\x64\netcoreapp2.0\<FEATURE_ASSEMBLY_NAME>\<FEATURE_VERSION>\lib\netcoreapp2.0\
```

<span data-ttu-id="cf67c-145">런타임 저장소에 어셈블리를 배포 하는 경우 기호 파일도 배포 될 수 있지만 기능이 작동 하려면 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-145">When deploying the assembly to the runtime store, the symbols file may be deployed as well but isn't required for the feature to work.</span></span>

<span data-ttu-id="cf67c-146">**종속성 파일 배치**</span><span class="sxs-lookup"><span data-stu-id="cf67c-146">**Place the dependencies file**</span></span>

<span data-ttu-id="cf67c-147">이제 구현의  *\*. deps.json* 파일 액세스할 수 있는 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-147">The implementation's *\*.deps.json* file must be in an accessible location.</span></span>

<span data-ttu-id="cf67c-148">사용자별으로 사용 하기 위해에서 파일을 배치는 `additonalDeps` 사용자 프로필의 폴더 `.dotnet` 설정:</span><span class="sxs-lookup"><span data-stu-id="cf67c-148">For per-user use, place the file in the `additonalDeps` folder of the user profile's `.dotnet` settings:</span></span> 

```
<DRIVE>\Users\<USER>\.dotnet\x64\additionalDeps\<FEATURE_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\2.0.0\
```

<span data-ttu-id="cf67c-149">전역 사용에 대 한 배치 파일에는 `additonalDeps` .NET Core 설치의 폴더:</span><span class="sxs-lookup"><span data-stu-id="cf67c-149">For global use, place the file in the `additonalDeps` folder of the .NET Core installation:</span></span>

```
<DRIVE>\Program Files\dotnet\additionalDeps\<FEATURE_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\2.0.0\
```

<span data-ttu-id="cf67c-150">버전을 기록 `2.0.0`에서 대상 응용 프로그램을 사용 하는 공유 런타임 버전을 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-150">Note the version, `2.0.0`, reflects the version of the shared runtime that the target app uses.</span></span> <span data-ttu-id="cf67c-151">공유 런타임에 표시 되는  *\*. runtimeconfig.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-151">The shared runtime is shown in the *\*.runtimeconfig.json* file.</span></span> <span data-ttu-id="cf67c-152">에 지정 된 공유 런타임 샘플 앱에는 *HostingStartupSample.runtimeconfig.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-152">In the sample app, the shared runtime is specified in the *HostingStartupSample.runtimeconfig.json* file.</span></span>

<span data-ttu-id="cf67c-153">**환경 변수 설정**</span><span class="sxs-lookup"><span data-stu-id="cf67c-153">**Set environment variables**</span></span>

<span data-ttu-id="cf67c-154">기능을 사용 하는 앱의 컨텍스트에서 다음과 같은 환경 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-154">Set the following environment variables in the context of the app that uses the feature.</span></span>

<span data-ttu-id="cf67c-155">ASPNETCORE\_HOSTINGSTARTUPASSEMBLIES</span><span class="sxs-lookup"><span data-stu-id="cf67c-155">ASPNETCORE\_HOSTINGSTARTUPASSEMBLIES</span></span>

<span data-ttu-id="cf67c-156">호스팅 시작 어셈블리만 검색는 `HostingStartupAttribute`합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-156">Only hosting startup assemblies are scanned for the `HostingStartupAttribute`.</span></span> <span data-ttu-id="cf67c-157">구현 어셈블리 이름은이 환경 변수에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-157">The assembly name of the implementation is provided in this environment variable.</span></span> <span data-ttu-id="cf67c-158">이 값을 설정 하는 샘플 응용 프로그램 `StartupDiagnostics`합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-158">The sample app sets this value to `StartupDiagnostics`.</span></span>

<span data-ttu-id="cf67c-159">사용 하 여 값 설정할 수도 있습니다는 [호스팅 시작 어셈블리가](xref:fundamentals/hosting#hosting-startup-assemblies) 호스트 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-159">The value can also be set using the [Hosting Startup Assemblies](xref:fundamentals/hosting#hosting-startup-assemblies) host configuration setting.</span></span>

<span data-ttu-id="cf67c-160">DOTNET\_추가\_DEPS</span><span class="sxs-lookup"><span data-stu-id="cf67c-160">DOTNET\_ADDITIONAL\_DEPS</span></span>

<span data-ttu-id="cf67c-161">구현 위치  *\*. deps.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-161">The location of the implementation's *\*.deps.json* file.</span></span>

<span data-ttu-id="cf67c-162">파일은 사용자 프로필에 저장 하는 경우 *.dotnet* 사용자 단위 사용에 대 한 폴더:</span><span class="sxs-lookup"><span data-stu-id="cf67c-162">If the file is placed in the user profile's *.dotnet* folder for per-user use:</span></span>

```
<DRIVE>\Users\<USER>\.dotnet\x64\additionalDeps\
```

<span data-ttu-id="cf67c-163">파일을 전역 사용에 대 한.NET Core 설치에 배치 하는 경우 파일에 전체 경로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-163">If the file is placed in the .NET Core installation for global use, provide the full path to the file:</span></span>

```
<DRIVE>\Program Files\dotnet\additionalDeps\<FEATURE_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\2.0.0\<FEATURE_ASSEMBLY_NAME>.deps.json
```

<span data-ttu-id="cf67c-164">이 값을 설정 하는 샘플 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="cf67c-164">The sample app sets this value to:</span></span>

```
%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\
```

<span data-ttu-id="cf67c-165">다양 한 운영 체제에 대 한 환경 변수를 설정 하는 방법의 예 참조 [여러 환경 작업](xref:fundamentals/environments)합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-165">For examples of how to set environment variables for various operating systems, see [Working with multiple environments](xref:fundamentals/environments).</span></span>

## <a name="sample-app"></a><span data-ttu-id="cf67c-166">샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="cf67c-166">Sample app</span></span>

<span data-ttu-id="cf67c-167">[샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/platform-specific-configuration/sample/) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample)) 사용 하 여 `IHostingStartup` 진단 도구를 만드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-167">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/platform-specific-configuration/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)) uses `IHostingStartup` to create a diagnostics tool.</span></span> <span data-ttu-id="cf67c-168">두 middlewares 진단 정보를 제공 하는 시작 시 응용 프로그램에 추가 하는 도구:</span><span class="sxs-lookup"><span data-stu-id="cf67c-168">The tool adds two middlewares to the app at startup that provide diagnostic information:</span></span>

* <span data-ttu-id="cf67c-169">등록 된 서비스</span><span class="sxs-lookup"><span data-stu-id="cf67c-169">Registered services</span></span>
* <span data-ttu-id="cf67c-170">주소: 구성표, 호스트, 기본 경로, 경로, 쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="cf67c-170">Address: scheme, host, path base, path, query string</span></span>
* <span data-ttu-id="cf67c-171">연결: 원격 IP, 원격 포트, 로컬 IP 로컬 포트를 클라이언트 인증서</span><span class="sxs-lookup"><span data-stu-id="cf67c-171">Connection: remote IP, remote port, local IP, local port, client certificate</span></span>
* <span data-ttu-id="cf67c-172">요청 헤더</span><span class="sxs-lookup"><span data-stu-id="cf67c-172">Request headers</span></span>
* <span data-ttu-id="cf67c-173">환경 변수</span><span class="sxs-lookup"><span data-stu-id="cf67c-173">Environment variables</span></span>

<span data-ttu-id="cf67c-174">샘플을 실행 하려면</span><span class="sxs-lookup"><span data-stu-id="cf67c-174">To run the sample:</span></span>

1. <span data-ttu-id="cf67c-175">진단 시작 프로젝트를 사용 하 여 [PowerShell](/powershell/scripting/powershell-scripting) 수정 하려면 해당 *StartupDiagnostics.deps.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-175">The Startup Diagnostic project uses [PowerShell](/powershell/scripting/powershell-scripting) to modify its *StartupDiagnostics.deps.json* file.</span></span> <span data-ttu-id="cf67c-176">PowerShell은 Windows 7 SP1 및 Windows Server 2008 R2 s p 1 부터는 Windows 운영 체제에서 기본적으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-176">PowerShell is installed by default on Windows OS starting with Windows 7 SP1 and Windows Server 2008 R2 SP1.</span></span> <span data-ttu-id="cf67c-177">다른 플랫폼에서 PowerShell을 얻으려고 참조 [Windows PowerShell 설치](/powershell/scripting/setup/installing-windows-powershell)합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-177">To obtain PowerShell on other platforms, see [Installing Windows PowerShell](/powershell/scripting/setup/installing-windows-powershell).</span></span>
2. <span data-ttu-id="cf67c-178">진단 시작 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="cf67c-178">Build the Startup Diagnostic project.</span></span> <span data-ttu-id="cf67c-179">프로젝트 파일에 빌드 대상:</span><span class="sxs-lookup"><span data-stu-id="cf67c-179">A build target in the project file:</span></span>
   * <span data-ttu-id="cf67c-180">어셈블리를 이동 하 고 기호 파일에서 사용자 프로필의 런타임 저장소에 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-180">Moves the assembly and symbols files to the user profile's runtime store.</span></span>
   * <span data-ttu-id="cf67c-181">수정 하는 PowerShell 스크립트를 트리거하는 *StartupDiagnostics.deps.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-181">Triggers the PowerShell script to modify the *StartupDiagnostics.deps.json* file.</span></span>
   * <span data-ttu-id="cf67c-182">이동 된 *StartupDiagnostics.deps.json* 사용자 프로필에 대 한 파일 `additionalDeps` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-182">Moves the *StartupDiagnostics.deps.json* file to the user profile's `additionalDeps` folder.</span></span>
3. <span data-ttu-id="cf67c-183">환경 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-183">Set the environment variables:</span></span>
    * <span data-ttu-id="cf67c-184">`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`: `StartupDiagnostics`</span><span class="sxs-lookup"><span data-stu-id="cf67c-184">`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`: `StartupDiagnostics`</span></span>
    * <span data-ttu-id="cf67c-185">`DOTNET_ADDITIONAL_DEPS`: `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`</span><span class="sxs-lookup"><span data-stu-id="cf67c-185">`DOTNET_ADDITIONAL_DEPS`: `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`</span></span>
4. <span data-ttu-id="cf67c-186">샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-186">Run the sample app.</span></span>
5. <span data-ttu-id="cf67c-187">요청 된 `/services` 응용 프로그램의를 참조 하는 끝점 서비스를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-187">Request the `/services` endpoint to see the app's registered services.</span></span> <span data-ttu-id="cf67c-188">요청 된 `/diag` 진단 정보를 확인 하는 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="cf67c-188">Request the `/diag` endpoint to see the diagnostic information.</span></span>
