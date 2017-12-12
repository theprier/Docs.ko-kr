---
title: "ASP.NET Core에서는 변경 토큰으로 변경 내용을 검색합니다"
author: guardrex
description: "변경 내용을 추적 하기 변경 토큰을 사용 하는 방법에 알아봅니다."
manager: wpickett
ms.author: riande
ms.date: 11/10/2017
ms.devlang: csharp
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/primitives/change-tokens
ms.openlocfilehash: a9479e3d676ed4dc880996a4a77de30d82b84cd5
ms.sourcegitcommit: 216dfac27542f10a79274a9ce60dc449e888ed20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/29/2017
---
# <a name="detect-changes-with-change-tokens-in-aspnet-core"></a><span data-ttu-id="8a044-103">ASP.NET Core에서는 변경 토큰으로 변경 내용을 검색합니다</span><span class="sxs-lookup"><span data-stu-id="8a044-103">Detect changes with change tokens in ASP.NET Core</span></span>

<span data-ttu-id="8a044-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="8a044-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="8a044-105">A *토큰 변경* 는 변경 내용을 추적 하는 데 사용 하는 범용, 하위 수준 빌딩 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-105">A *change token* is a general-purpose, low-level building block used to track changes.</span></span>

<span data-ttu-id="8a044-106">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/primitives/change-tokens/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="8a044-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/primitives/change-tokens/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="ichangetoken-interface"></a><span data-ttu-id="8a044-107">IChangeToken 인터페이스</span><span class="sxs-lookup"><span data-stu-id="8a044-107">IChangeToken interface</span></span>

<span data-ttu-id="8a044-108">[IChangeToken](/dotnet/api/microsoft.extensions.primitives.ichangetoken) 변경 내용이 발생 하는 알림을 전파 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-108">[IChangeToken](/dotnet/api/microsoft.extensions.primitives.ichangetoken) propagates notifications that a change has occurred.</span></span> <span data-ttu-id="8a044-109">`IChangeToken`에 [Microsoft.Extensions.Primitives](/dotnet/api/microsoft.extensions.primitives) 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-109">`IChangeToken` resides in the [Microsoft.Extensions.Primitives](/dotnet/api/microsoft.extensions.primitives) namespace.</span></span> <span data-ttu-id="8a044-110">사용 하지 않는 앱에 대 한는 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) metapackage, 참조는 [Microsoft.Extensions.Primitives](https://www.nuget.org/packages/Microsoft.Extensions.Primitives/) 프로젝트 파일에서 NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-110">For apps that don't use the [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) metapackage, reference the [Microsoft.Extensions.Primitives](https://www.nuget.org/packages/Microsoft.Extensions.Primitives/) NuGet package in the project file.</span></span>

<span data-ttu-id="8a044-111">`IChangeToken`에 두 개의 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-111">`IChangeToken` has two properties:</span></span>

* <span data-ttu-id="8a044-112">[ActiveChangedCallbacks](/dotnet/api/microsoft.extensions.primitives.ichangetoken.activechangecallbacks) 토큰 사전 콜백이 발생을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-112">[ActiveChangedCallbacks](/dotnet/api/microsoft.extensions.primitives.ichangetoken.activechangecallbacks) indicate if the token proactively raises callbacks.</span></span> <span data-ttu-id="8a044-113">경우 `ActiveChangedCallbacks` 로 설정 된 `false`, 콜백을 호출 되지 않는 및 앱 폴링해야 `HasChanged` 변경에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-113">If `ActiveChangedCallbacks` is set to `false`, a callback is never called, and the app must poll `HasChanged` for changes.</span></span> <span data-ttu-id="8a044-114">또한 변경 되지 않습니다 또는 기본 변경 수신기를 삭제 하거나 사용 하지 않도록 설정 하는 경우 취소 되지 하는 토큰에 대 한도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-114">It's also possible for a token to never be cancelled if no changes occur or the underlying change listener is disposed or disabled.</span></span>
* <span data-ttu-id="8a044-115">[HasChanged](/dotnet/api/microsoft.extensions.primitives.ichangetoken.haschanged) 변경 내용이 발생 하는 경우를 나타내는 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-115">[HasChanged](/dotnet/api/microsoft.extensions.primitives.ichangetoken.haschanged) gets a value that indicates if a change has occurred.</span></span>

<span data-ttu-id="8a044-116">인터페이스에는 하나의 메서드 [RegisterChangeCallback (동작&lt;개체&gt;, 개체)](/dotnet/api/microsoft.extensions.primitives.ichangetoken.registerchangecallback)를 토큰 변경 될 때 호출 되는 콜백을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-116">The interface has one method, [RegisterChangeCallback(Action&lt;Object&gt;, Object)](/dotnet/api/microsoft.extensions.primitives.ichangetoken.registerchangecallback), which registers a callback that's invoked when the token has changed.</span></span> <span data-ttu-id="8a044-117">`HasChanged`콜백이 호출 되기 전에 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-117">`HasChanged` must be set before the callback is invoked.</span></span>

## <a name="changetoken-class"></a><span data-ttu-id="8a044-118">ChangeToken 클래스</span><span class="sxs-lookup"><span data-stu-id="8a044-118">ChangeToken class</span></span>

<span data-ttu-id="8a044-119">`ChangeToken`정적 클래스 변경 내용이 발생 하는 알림을 전파 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-119">`ChangeToken` is a static class used to propagate notifications that a change has occurred.</span></span> <span data-ttu-id="8a044-120">`ChangeToken`에 [Microsoft.Extensions.Primitives](/dotnet/api/microsoft.extensions.primitives) 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-120">`ChangeToken` resides in the [Microsoft.Extensions.Primitives](/dotnet/api/microsoft.extensions.primitives) namespace.</span></span> <span data-ttu-id="8a044-121">사용 하지 않는 앱에 대 한는 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) metapackage, 참조는 [Microsoft.Extensions.Primitives](https://www.nuget.org/packages/Microsoft.Extensions.Primitives/) 프로젝트 파일에서 NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-121">For apps that don't use the [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) metapackage, reference the [Microsoft.Extensions.Primitives](https://www.nuget.org/packages/Microsoft.Extensions.Primitives/) NuGet package in the project file.</span></span>

<span data-ttu-id="8a044-122">`ChangeToken` [OnChange (Func&lt;IChangeToken&gt;, 동작)](/dotnet/api/microsoft.extensions.primitives.changetoken.onchange?view=aspnetcore-2.0#Microsoft_Extensions_Primitives_ChangeToken_OnChange_System_Func_Microsoft_Extensions_Primitives_IChangeToken__System_Action_) 메서드 레지스터는 `Action` 토큰 변경 될 때마다 호출 하려면:</span><span class="sxs-lookup"><span data-stu-id="8a044-122">The `ChangeToken` [OnChange(Func&lt;IChangeToken&gt;, Action)](/dotnet/api/microsoft.extensions.primitives.changetoken.onchange?view=aspnetcore-2.0#Microsoft_Extensions_Primitives_ChangeToken_OnChange_System_Func_Microsoft_Extensions_Primitives_IChangeToken__System_Action_) method registers an `Action` to call whenever the token changes:</span></span>
* <span data-ttu-id="8a044-123">`Func<IChangeToken>`토큰을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-123">`Func<IChangeToken>` produces the token.</span></span>
* <span data-ttu-id="8a044-124">`Action`토큰 변경 될 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-124">`Action` is called when the token changes.</span></span>

<span data-ttu-id="8a044-125">`ChangeToken`에 [OnChange&lt;TState&gt;(Func&lt;IChangeToken&gt;, 동작&lt;TState&gt;, TState)](/dotnet/api/microsoft.extensions.primitives.changetoken.onchange?view=aspnetcore-2.0#Microsoft_Extensions_Primitives_ChangeToken_OnChange__1_System_Func_Microsoft_Extensions_Primitives_IChangeToken__System_Action___0____0_) 오버 로드를 추가 `TState`토큰 소비자에 전달 되는 매개 변수 `Action`합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-125">`ChangeToken` has an [OnChange&lt;TState&gt;(Func&lt;IChangeToken&gt;, Action&lt;TState&gt;, TState)](/dotnet/api/microsoft.extensions.primitives.changetoken.onchange?view=aspnetcore-2.0#Microsoft_Extensions_Primitives_ChangeToken_OnChange__1_System_Func_Microsoft_Extensions_Primitives_IChangeToken__System_Action___0____0_) overload that takes an additional `TState` parameter that's passed into the token consumer `Action`.</span></span>

<span data-ttu-id="8a044-126">`OnChange`반환 된 [IDisposable](/dotnet/api/system.idisposable)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-126">`OnChange` returns an [IDisposable](/dotnet/api/system.idisposable).</span></span> <span data-ttu-id="8a044-127">호출 [Dispose](/dotnet/api/system.idisposable.dispose) 에서 추가 변경을 위해 수신 토큰을 중지 하 고 토큰의 리소스를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-127">Calling [Dispose](/dotnet/api/system.idisposable.dispose) stops the token from listening for further changes and releases the token's resources.</span></span>

## <a name="example-uses-of-change-tokens-in-aspnet-core"></a><span data-ttu-id="8a044-128">ASP.NET Core에서 변경 토큰의 사용 하 여 예제</span><span class="sxs-lookup"><span data-stu-id="8a044-128">Example uses of change tokens in ASP.NET Core</span></span>

<span data-ttu-id="8a044-129">변경 토큰 개체의 변경 내용을 모니터링 하는 ASP.NET Core의 주요 영역에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-129">Change tokens are used in prominent areas of ASP.NET Core monitoring changes to objects:</span></span>

* <span data-ttu-id="8a044-130">파일의 변경 내용을 모니터링에 대 한 [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider)의 [조사식](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.watch) 메서드 만듭니다는 `IChangeToken` 지정 된 파일 또는 폴더를 시청 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-130">For monitoring changes to files, [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider)'s [Watch](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.watch) method creates an `IChangeToken` for the specified files or folder to watch.</span></span>
* <span data-ttu-id="8a044-131">`IChangeToken`토큰 캐시를 변경 시 캐시 제거를 트리거하는 항목에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-131">`IChangeToken` tokens can be added to cache entries to trigger cache evictions on change.</span></span>
* <span data-ttu-id="8a044-132">에 대 한 `TOptions` 하면 기본 변경 [OptionsMonitor](/dotnet/api/microsoft.extensions.options.optionsmonitor-1) 구현의 [IOptionsMonitor](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) 하나 이상의 허용 하는 오버 로드가 [IOptionsChangeTokenSource](/dotnet/api/microsoft.extensions.options.ioptionschangetokensource-1)인스턴스.</span><span class="sxs-lookup"><span data-stu-id="8a044-132">For `TOptions` changes, the default [OptionsMonitor](/dotnet/api/microsoft.extensions.options.optionsmonitor-1) implementation of [IOptionsMonitor](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) has an overload that accepts one or more [IOptionsChangeTokenSource](/dotnet/api/microsoft.extensions.options.ioptionschangetokensource-1) instances.</span></span> <span data-ttu-id="8a044-133">각 인스턴스를 반환 된 `IChangeToken` 추적 옵션 변경 내용에 대 한 변경 알림 콜백을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-133">Each instance returns an `IChangeToken` to register a change notification callback for tracking options changes.</span></span>

## <a name="monitoring-for-configuration-changes"></a><span data-ttu-id="8a044-134">구성 변경에 대 한 모니터링</span><span class="sxs-lookup"><span data-stu-id="8a044-134">Monitoring for configuration changes</span></span>

<span data-ttu-id="8a044-135">ASP.NET Core 템플릿은 기본적으로 사용 하 여 [JSON 구성 파일](xref:fundamentals/configuration/index#json-configuration) (*appsettings.json*, *appsettings 합니다. Development.json*, 및 *appsettings 합니다. Production.json*) 응용 프로그램 구성 설정을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-135">By default, ASP.NET Core templates use [JSON configuration files](xref:fundamentals/configuration/index#json-configuration) (*appsettings.json*, *appsettings.Development.json*, and *appsettings.Production.json*) to load app configuration settings.</span></span>

<span data-ttu-id="8a044-136">사용 하 여 이러한 파일은 구성에서 [AddJsonFile (IConfigurationBuilder, String, Boolean, Boolean)](/dotnet/api/microsoft.extensions.configuration.jsonconfigurationextensions.addjsonfile?view=aspnetcore-2.0#Microsoft_Extensions_Configuration_JsonConfigurationExtensions_AddJsonFile_Microsoft_Extensions_Configuration_IConfigurationBuilder_System_String_System_Boolean_System_Boolean_) 확장 메서드를 [ConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.configurationbuilder) 수락 하는 `reloadOnChange` 매개 변수 (ASP.NET 코어 1.1 이상)입니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-136">These files are configured using the [AddJsonFile(IConfigurationBuilder, String, Boolean, Boolean)](/dotnet/api/microsoft.extensions.configuration.jsonconfigurationextensions.addjsonfile?view=aspnetcore-2.0#Microsoft_Extensions_Configuration_JsonConfigurationExtensions_AddJsonFile_Microsoft_Extensions_Configuration_IConfigurationBuilder_System_String_System_Boolean_System_Boolean_) extension method on [ConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.configurationbuilder) that accepts a `reloadOnChange` parameter (ASP.NET Core 1.1 and later).</span></span> <span data-ttu-id="8a044-137">`reloadOnChange`파일 변경 내용에 대 한 구성이 다시 로드 해야 하는 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-137">`reloadOnChange` indicates if configuration should be reloaded on file changes.</span></span> <span data-ttu-id="8a044-138">이 설정을 참조는 [WebHost](/dotnet/api/microsoft.aspnetcore.webhost) 편리 하 게 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) ([참조 소스](https://github.com/aspnet/MetaPackages/blob/rel/2.0.3/src/Microsoft.AspNetCore/WebHost.cs#L152-L193)):</span><span class="sxs-lookup"><span data-stu-id="8a044-138">See this setting in the [WebHost](/dotnet/api/microsoft.aspnetcore.webhost) convenience method [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) ([reference source](https://github.com/aspnet/MetaPackages/blob/rel/2.0.3/src/Microsoft.AspNetCore/WebHost.cs#L152-L193)):</span></span>

```csharp
config.AddJsonFile("appsettings.json", optional: true, reloadOnChange: true)
      .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true, reloadOnChange: true);
```

<span data-ttu-id="8a044-139">파일 기반 구성을 나타내는 [FileConfigurationSource](/dotnet/api/microsoft.extensions.configuration.fileconfigurationsource)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-139">File-based configuration is represented by [FileConfigurationSource](/dotnet/api/microsoft.extensions.configuration.fileconfigurationsource).</span></span> <span data-ttu-id="8a044-140">`FileConfigurationSource`사용 하 여 [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider) ([참조 소스](https://github.com/aspnet/FileSystem/blob/patch/2.0.1/src/Microsoft.Extensions.FileProviders.Abstractions/IFileProvider.cs)) 파일을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-140">`FileConfigurationSource` uses [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider) ([reference source](https://github.com/aspnet/FileSystem/blob/patch/2.0.1/src/Microsoft.Extensions.FileProviders.Abstractions/IFileProvider.cs)) to monitor files.</span></span>

<span data-ttu-id="8a044-141">기본적으로는 `IFileMonitor` 에서 제공는 [PhysicalFileProvider](/dotnet/api/microsoft.extensions.fileproviders.physicalfileprovider) ([참조 소스](https://github.com/aspnet/Configuration/blob/patch/2.0.1/src/Microsoft.Extensions.Configuration.FileExtensions/FileConfigurationSource.cs#L82)), 사용 하 여 [FileSystemWatcher](/dotnet/api/system.io.filesystemwatcher) 구성 파일에 대 한 모니터링 하려면 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-141">By default, the `IFileMonitor` is provided by a [PhysicalFileProvider](/dotnet/api/microsoft.extensions.fileproviders.physicalfileprovider) ([reference source](https://github.com/aspnet/Configuration/blob/patch/2.0.1/src/Microsoft.Extensions.Configuration.FileExtensions/FileConfigurationSource.cs#L82)), which uses [FileSystemWatcher](/dotnet/api/system.io.filesystemwatcher) to monitor for configuration file changes.</span></span>

<span data-ttu-id="8a044-142">샘플 응용 프로그램 구성 변경 내용을 모니터링 하기 위한 두 가지 구현 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-142">The sample app demonstrates two implementations for monitoring configuration changes.</span></span> <span data-ttu-id="8a044-143">경우는 *appsettings.json* 환경 버전의 파일 또는 파일 변경, 각 구현은 사용자 지정 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-143">If either the *appsettings.json* file changes or the Environment version of the file changes, each implementation executes custom code.</span></span> <span data-ttu-id="8a044-144">샘플 응용 프로그램을 콘솔에 메시지를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-144">The sample app writes a message to the console.</span></span>

<span data-ttu-id="8a044-145">구성 파일의 `FileSystemWatcher` 단일 구성 파일 변경에 대 한 여러 토큰 콜백을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-145">A configuration file's `FileSystemWatcher` can trigger multiple token callbacks for a single configuration file change.</span></span> <span data-ttu-id="8a044-146">이 문제에 대 한 구성 파일에 파일 해시를 확인 하 여 샘플의 구현을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-146">The sample's implementation guards against this problem by checking file hashes on the configuration files.</span></span> <span data-ttu-id="8a044-147">파일 해시를 확인 하는 중 사용자 지정 코드를 실행 하기 전에 구성 파일 중 하나 이상이 변경 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-147">Checking file hashes ensures that at least one of the configuration files has changed before running the custom code.</span></span> <span data-ttu-id="8a044-148">이 샘플에서는 SHA1 파일 해시를 사용 (*Utilities/Utilities.cs*):</span><span class="sxs-lookup"><span data-stu-id="8a044-148">The sample uses SHA1 file hashing (*Utilities/Utilities.cs*):</span></span>

   [!code-csharp[Main](change-tokens/sample/Utilities/Utilities.cs?name=snippet1)]

   <span data-ttu-id="8a044-149">다시 시도 하 여는 지 수 백오프으로 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-149">A retry is implemented with an exponential back-off.</span></span> <span data-ttu-id="8a044-150">다시 시도 파일 잠금을 임시로 파일 중 하나에서 새 해시를 계산 하지 못하게 하는 발생할 수 있으므로.</span><span class="sxs-lookup"><span data-stu-id="8a044-150">The re-try is present because file locking may occur that temporarily prevents computing a new hash on one of the files.</span></span>

### <a name="simple-startup-change-token"></a><span data-ttu-id="8a044-151">Simple 시작 변경 토큰</span><span class="sxs-lookup"><span data-stu-id="8a044-151">Simple startup change token</span></span>

<span data-ttu-id="8a044-152">토큰 소비자 등록 `Action` 구성 다시 로드 토큰에 콜백에 대 한 변경 알림을 (*Startup.cs*):</span><span class="sxs-lookup"><span data-stu-id="8a044-152">Register a token consumer `Action` callback for change notifications to the configuration reload token (*Startup.cs*):</span></span>

[!code-csharp[Main](change-tokens/sample/Startup.cs?name=snippet2)]

<span data-ttu-id="8a044-153">`config.GetReloadToken()`토큰을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-153">`config.GetReloadToken()` provides the token.</span></span> <span data-ttu-id="8a044-154">콜백을 `InvokeChanged` 메서드:</span><span class="sxs-lookup"><span data-stu-id="8a044-154">The callback is the `InvokeChanged` method:</span></span>

[!code-csharp[Main](change-tokens/sample/Startup.cs?name=snippet3)]

<span data-ttu-id="8a044-155">`state` 콜백은 전달 하는 데에 `IHostingEnvironment`합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-155">The `state` of the callback is used to pass in the `IHostingEnvironment`.</span></span> <span data-ttu-id="8a044-156">이 올바른 결정 하는 데 유용 *appsettings* 구성 JSON 파일을 모니터링 하려면 *appsettings.&lt; 환경&gt;.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-156">This is useful to determine the correct *appsettings* configuration JSON file to monitor, *appsettings.&lt;Environment&gt;.json*.</span></span> <span data-ttu-id="8a044-157">파일 해시는 방지 하는 데 사용 되는 `WriteConsole` 문은 구성 파일에 한 번만 변경 하는 경우 여러 개의 토큰 콜백 인해 여러 번 실행에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-157">File hashes are used to prevent the `WriteConsole` statement from running multiple times due to multiple token callbacks when the configuration file has only changed once.</span></span>

<span data-ttu-id="8a044-158">이 시스템 있으면 디버거가 실행 응용 프로그램 실행 되 고 있고 사용자가 해제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-158">This system runs as long as the app is running and can't be disabled by the user.</span></span>

### <a name="monitoring-configuration-changes-as-a-service"></a><span data-ttu-id="8a044-159">서비스 구성 변경 사항 모니터링</span><span class="sxs-lookup"><span data-stu-id="8a044-159">Monitoring configuration changes as a service</span></span>

<span data-ttu-id="8a044-160">이 샘플을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-160">The sample implements:</span></span>

* <span data-ttu-id="8a044-161">기본 시작 토큰을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-161">Basic startup token monitoring.</span></span>
* <span data-ttu-id="8a044-162">서비스를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-162">Monitoring as a service.</span></span>
* <span data-ttu-id="8a044-163">설정 및 모니터링을 해제 하는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-163">A mechanism to enable and disable monitoring.</span></span>

<span data-ttu-id="8a044-164">이 샘플은 설정 된 `IConfigurationMonitor` 인터페이스 (*Extensions/ConfigurationMonitor.cs*):</span><span class="sxs-lookup"><span data-stu-id="8a044-164">The sample establishes an `IConfigurationMonitor` interface (*Extensions/ConfigurationMonitor.cs*):</span></span>

[!code-csharp[Main](change-tokens/sample/Extensions/ConfigurationMonitor.cs?name=snippet1)]

<span data-ttu-id="8a044-165">구현 된 클래스의 생성자 `ConfigurationMonitor`, 변경 알림에 대 한 콜백을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-165">The constructor of the implemented class, `ConfigurationMonitor`, registers a callback for change notifications:</span></span>

[!code-csharp[Main](change-tokens/sample/Extensions/ConfigurationMonitor.cs?name=snippet2)]

<span data-ttu-id="8a044-166">`config.GetReloadToken()`토큰을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-166">`config.GetReloadToken()` supplies the token.</span></span> <span data-ttu-id="8a044-167">`InvokeChanged`콜백 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-167">`InvokeChanged` is the callback method.</span></span> <span data-ttu-id="8a044-168">`state` 이 인스턴스에서 모니터링 상태를 설명 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-168">The `state` in this instance is a string that describes the monitoring state.</span></span> <span data-ttu-id="8a044-169">두 개의 속성이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-169">Two properties are used:</span></span>

* <span data-ttu-id="8a044-170">`MonitoringEnabled`콜백은 사용자 지정 코드를 실행 해야 하는 경우 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-170">`MonitoringEnabled` indicates if the callback should run its custom code.</span></span>
* <span data-ttu-id="8a044-171">`CurrentState`UI에서 사용 하기 위해 현재 모니터링 상태를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-171">`CurrentState` describes the current monitoring state for use in the UI.</span></span>

<span data-ttu-id="8a044-172">`InvokeChanged` 한다는 점 제외 하면 이전 방식을 사용 하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-172">The `InvokeChanged` method is similar to the earlier approach, except that it:</span></span>

* <span data-ttu-id="8a044-173">하지 않는 한 해당 코드가 실행 되지 않으므로 `MonitoringEnabled` 은 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-173">Doesn't run its code unless `MonitoringEnabled` is `true`.</span></span>
* <span data-ttu-id="8a044-174">설정의 `CurrentState` 코드가 실행 된 시간을 기록 하는 설명 메시지 속성 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-174">Sets the `CurrentState` property string to a descriptive message that records the time that the code ran.</span></span>
* <span data-ttu-id="8a044-175">현재 정보 `state` 에 해당 `WriteConsole` 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-175">Notes the current `state` in its `WriteConsole` output.</span></span>

[!code-csharp[Main](change-tokens/sample/Extensions/ConfigurationMonitor.cs?name=snippet3)]

<span data-ttu-id="8a044-176">인스턴스 `ConfigurationMonitor` 에서 서비스로 등록 `ConfigureServices` 의 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="8a044-176">An instance `ConfigurationMonitor` is registered as a service in `ConfigureServices` of *Startup.cs*:</span></span>

[!code-csharp[Main](change-tokens/sample/Startup.cs?name=snippet1)]

<span data-ttu-id="8a044-177">인덱스 페이지에서는 구성 모니터링을 통해 사용자 정의 컨트롤을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-177">The Index page offers the user control over configuration monitoring.</span></span> <span data-ttu-id="8a044-178">인스턴스 `IConfigurationMonitor` 에 삽입 된 `IndexModel`:</span><span class="sxs-lookup"><span data-stu-id="8a044-178">The instance of `IConfigurationMonitor` is injected into the `IndexModel`:</span></span>

[!code-csharp[Main](change-tokens/sample/Pages/Index.cshtml.cs?name=snippet1)]

<span data-ttu-id="8a044-179">단추를 사용 하도록 설정 및 모니터링을 사용 하지 않도록 설정:</span><span class="sxs-lookup"><span data-stu-id="8a044-179">A button enables and disables monitoring:</span></span>

[!code-cshtml[Main](change-tokens/sample/Pages/Index.cshtml?range=35)]

[!code-csharp[Main](change-tokens/sample/Pages/Index.cshtml.cs?name=snippet2)]

<span data-ttu-id="8a044-180">때 `OnPostStartMonitoring` 은 트리거된 모니터링을 사용할 수 및 현재 상태가 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-180">When `OnPostStartMonitoring` is triggered, monitoring is enabled, and the current state is cleared.</span></span> <span data-ttu-id="8a044-181">때 `OnPostStopMonitoring` 은 트리거된 모니터링 하지 않는 경우 및 상태 모니터링은 발생 하지 반영 하도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-181">When `OnPostStopMonitoring` is triggered, monitoring is disabled, and the state is set to reflect that monitoring is not occurring.</span></span>

## <a name="monitoring-cached-file-changes"></a><span data-ttu-id="8a044-182">캐시 된 파일 변경 사항 모니터링</span><span class="sxs-lookup"><span data-stu-id="8a044-182">Monitoring cached file changes</span></span>

<span data-ttu-id="8a044-183">캐시 된 메모리를 사용 하 여 파일 내용을 수 [IMemoryCache](/dotnet/api/microsoft.extensions.caching.memory.imemorycache)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-183">File content can be cached in-memory using [IMemoryCache](/dotnet/api/microsoft.extensions.caching.memory.imemorycache).</span></span> <span data-ttu-id="8a044-184">에 설명 된 메모리 내 캐시는 [메모리에 캐시할](xref:performance/caching/memory) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-184">In-memory caching is described in the [In-memory caching](xref:performance/caching/memory) topic.</span></span> <span data-ttu-id="8a044-185">아래에 설명 된 구현 등의 추가 단계를 수행 하지 않고 *부실* (오래 된) 데이터 원본 데이터가 변경 되 면 캐시에서 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-185">Without taking additional steps, such as the implementation described below, *stale* (outdated) data is returned from a cache if the source data changes.</span></span>

<span data-ttu-id="8a044-186">하지 고려 된 캐시 된 원본 파일의 상태를 갱신할는 [상대 만료](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryoptions.slidingexpiration) 기간에 따라 캐시 데이터를 부실 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-186">Not taking into account the status of a cached source file when renewing a [sliding expiration](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryoptions.slidingexpiration) period leads to stale cache data.</span></span> <span data-ttu-id="8a044-187">슬라이딩 만료 기간을 갱신 하는 데이터에 대 한 각 요청 하지만 파일 캐시로 다시 로드 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-187">Each request for the data renews the sliding expiration period, but the file is never reloaded into the cache.</span></span> <span data-ttu-id="8a044-188">파일의 캐시 된 콘텐츠를 사용 하는 모든 앱 기능을 수 있는 불완전 한 콘텐츠를 받는 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-188">Any app features that use the file's cached content are subject to possibly receiving stale content.</span></span>

<span data-ttu-id="8a044-189">파일 캐싱 시나리오에서에서 변경 토큰을 사용 하 여 캐시에 유효 하지 않은 파일 콘텐츠를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-189">Using change tokens in a file caching scenario prevents stale file content in the cache.</span></span> <span data-ttu-id="8a044-190">샘플 앱 방법의 구현을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-190">The sample app demonstrates an implementation of the approach.</span></span>

<span data-ttu-id="8a044-191">이 샘플에서는 사용 `GetFileContent` 에:</span><span class="sxs-lookup"><span data-stu-id="8a044-191">The sample uses `GetFileContent` to:</span></span>

* <span data-ttu-id="8a044-192">파일 콘텐츠를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-192">Return file content.</span></span>
* <span data-ttu-id="8a044-193">지 수 백오프 여기서 파일 잠금을 일시적으로 때문에 파일을 읽지 못하게 하는 커버 사례에 있는 다시 시도 알고리즘을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-193">Implement a retry algorithm with exponential back-off to cover cases where a file lock is temporarily preventing a file from being read.</span></span>

<span data-ttu-id="8a044-194">*Utilities/Utilities.cs*:</span><span class="sxs-lookup"><span data-stu-id="8a044-194">*Utilities/Utilities.cs*:</span></span>

[!code-csharp[Main](change-tokens/sample/Utilities/Utilities.cs?name=snippet2)]

<span data-ttu-id="8a044-195">A `FileService` 조회 캐시 된 파일을 처리 하기 위해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-195">A `FileService` is created to handle cached file lookups.</span></span> <span data-ttu-id="8a044-196">`GetFileContent` 메서드 호출 서비스의 메모리 내 캐시에서 파일 콘텐츠를 가져올을 호출자에 게 반환 시도 (*Services/FileService.cs*).</span><span class="sxs-lookup"><span data-stu-id="8a044-196">The `GetFileContent` method call of the service attempts to obtain file content from the in-memory cache and return it to the caller (*Services/FileService.cs*).</span></span>

<span data-ttu-id="8a044-197">캐시 된 콘텐츠 찾을 수 없으면 캐시 키를 사용 하 여 다음 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-197">If cached content isn't found using the cache key, the following actions are taken:</span></span>

1. <span data-ttu-id="8a044-198">파일 콘텐츠를 사용 하 여 가져온 `GetFileContent`합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-198">The file content is obtained using `GetFileContent`.</span></span>
1. <span data-ttu-id="8a044-199">변경 토큰을 사용 하 여 파일 공급자에서 가져온 [IFileProviders.Watch](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.watch)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-199">A change token is obtained from the file provider with [IFileProviders.Watch](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.watch).</span></span> <span data-ttu-id="8a044-200">토큰의 콜백 파일 수정 될 때 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-200">The token's callback is triggered when the file is modified.</span></span>
1. <span data-ttu-id="8a044-201">파일 내용을 함께 캐시를 [상대 만료](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryoptions.slidingexpiration) 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-201">The file content is cached with a [sliding expiration](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryoptions.slidingexpiration) period.</span></span> <span data-ttu-id="8a044-202">와 연결 된 변경 토큰이 [MemoryCacheEntryExtensions.AddExpirationToken](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryextensions.addexpirationtoken) 캐시 되어 있는 동안 파일이 변경 되 면 캐시 엔트리를 제거 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-202">The change token is attached with [MemoryCacheEntryExtensions.AddExpirationToken](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryextensions.addexpirationtoken) to evict the cache entry if the file changes while it's cached.</span></span>

[!code-csharp[Main](change-tokens/sample/Services/FileService.cs?name=snippet1)]

<span data-ttu-id="8a044-203">`FileService` 서비스 캐싱 메모리와 함께 서비스 컨테이너에 등록 된 (*Startup.cs*):</span><span class="sxs-lookup"><span data-stu-id="8a044-203">The `FileService` is registered in the service container along with the memory caching service (*Startup.cs*):</span></span>

[!code-csharp[Main](change-tokens/sample/Startup.cs?name=snippet4)]

<span data-ttu-id="8a044-204">서비스를 사용 하 여 파일의 콘텐츠를 로드 하는 페이지 모델 (*Pages/Index.cshtml.cs*):</span><span class="sxs-lookup"><span data-stu-id="8a044-204">The page model loads the file's content using the service (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[Main](change-tokens/sample/Pages/Index.cshtml.cs?name=snippet3)]

## <a name="compositechangetoken-class"></a><span data-ttu-id="8a044-205">CompositeChangeToken 클래스</span><span class="sxs-lookup"><span data-stu-id="8a044-205">CompositeChangeToken class</span></span>

<span data-ttu-id="8a044-206">하나 이상의 나타내기 위한 `IChangeToken` 인스턴스는 단일 개체에 사용 하 여는 [CompositeChangeToken](/dotnet/api/microsoft.extensions.primitives.compositechangetoken) 클래스 ([참조 소스](https://github.com/aspnet/Common/blob/patch/2.0.1/src/Microsoft.Extensions.Primitives/CompositeChangeToken.cs)).</span><span class="sxs-lookup"><span data-stu-id="8a044-206">For representing one or more `IChangeToken` instances in a single object, use the [CompositeChangeToken](/dotnet/api/microsoft.extensions.primitives.compositechangetoken) class ([reference source](https://github.com/aspnet/Common/blob/patch/2.0.1/src/Microsoft.Extensions.Primitives/CompositeChangeToken.cs)).</span></span>

```csharp
var firstCancellationTokenSource = new CancellationTokenSource();
var secondCancellationTokenSource = new CancellationTokenSource();

var firstCancellationToken = firstCancellationTokenSource.Token;
var secondCancellationToken = secondCancellationTokenSource.Token;

var firstCancellationChangeToken = new CancellationChangeToken(firstCancellationToken);
var secondCancellationChangeToken = new CancellationChangeToken(secondCancellationToken);

var compositeChangeToken = 
    new CompositeChangeToken(
        new List<IChangeToken> 
        { 
            firstCancellationChangeToken, 
            secondCancellationChangeToken
        });
```

<span data-ttu-id="8a044-207">`HasChanged`복합 토큰 보고서 `true` 토큰을 나타내는 모든 `HasChanged` 은 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-207">`HasChanged` on the composite token reports `true` if any represented token `HasChanged` is `true`.</span></span> <span data-ttu-id="8a044-208">`ActiveChangeCallbacks`복합 토큰 보고서 `true` 토큰을 나타내는 모든 `ActiveChangeCallbacks` 은 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-208">`ActiveChangeCallbacks` on the composite token reports `true` if any represented token `ActiveChangeCallbacks` is `true`.</span></span> <span data-ttu-id="8a044-209">여러 동시 변경 이벤트가 발생할 경우 복합 변경 콜백이는 정확히 한 번 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a044-209">If multiple concurrent change events occur, the composite change callback is invoked exactly one time.</span></span>

## <a name="see-also"></a><span data-ttu-id="8a044-210">참고 항목</span><span class="sxs-lookup"><span data-stu-id="8a044-210">See also</span></span>

* [<span data-ttu-id="8a044-211">메모리 내 캐싱</span><span class="sxs-lookup"><span data-stu-id="8a044-211">In-memory caching</span></span>](xref:performance/caching/memory)
* [<span data-ttu-id="8a044-212">분산된 캐시 사용</span><span class="sxs-lookup"><span data-stu-id="8a044-212">Working with a distributed cache</span></span>](xref:performance/caching/distributed)
* [<span data-ttu-id="8a044-213">변경 내용을 변경 토큰으로 검색</span><span class="sxs-lookup"><span data-stu-id="8a044-213">Detect changes with change tokens</span></span>](xref:fundamentals/primitives/change-tokens)
* [<span data-ttu-id="8a044-214">응답 캐싱</span><span class="sxs-lookup"><span data-stu-id="8a044-214">Response caching</span></span>](xref:performance/caching/response)
* [<span data-ttu-id="8a044-215">응답 캐싱 미들웨어</span><span class="sxs-lookup"><span data-stu-id="8a044-215">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
* [<span data-ttu-id="8a044-216">캐시 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="8a044-216">Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [<span data-ttu-id="8a044-217">분산된 캐시 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="8a044-217">Distributed Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
