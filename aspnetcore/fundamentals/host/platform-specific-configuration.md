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
# <a name="enhance-an-app-from-an-external-assembly-in-aspnet-core-with-ihostingstartup"></a>IHostingStartup을 사용하여 ASP.NET Core의 외부 어셈블리에서 앱 강화

[Luke Latham](https://github.com/guardrex)으로

[IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup)(호스팅 시작) 구현에서는 외부 어셈블리에서 시작할 때 앱에 향상된 기능을 추가할 수 있습니다. 예를 들어 외부 라이브러리는 호스팅 시작 구현을 사용하여 앱에 추가 구성 공급자 또는 서비스를 제공할 수 있습니다. `IHostingStartup` *는 ASP.NET Core 2.0 이상에서 사용할 수 있습니다.*

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="hostingstartup-attribute"></a>HostingStartup 특성

[HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 특성은 런타임에 활성화할 호스팅 시작 어셈블리의 현재 상태를 나타냅니다.

항목 어셈블리 또는 `Startup` 클래스가 포함된 어셈블리에서는 `HostingStartup` 특성을 자동으로 검색합니다. `HostingStartup` 특성을 검색할 어셈블리 목록은 [WebHostDefaults.HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey)의 구성에서 런타임에 로드됩니다. 검색에서 제외할 어셈블리 목록은 [WebHostDefaults.HostingStartupExcludeAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupexcludeassemblieskey)에서 로드됩니다. 자세한 내용은 [웹 호스트: 호스팅 시작 어셈블리](xref:fundamentals/host/web-host#hosting-startup-assemblies) 및 [웹 호스트: 호스팅 시작 어셈블리 제외](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies)를 참조하세요.

다음 예제에서는 호스팅 시작 어셈블리의 네임스페이스가 `StartupEnhancement`입니다. 호스팅 시작 코드를 포함하는 클래스는 `StartupEnhancementHostingStartup`입니다.

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet1)]

`HostingStartup` 특성은 일반적으로 호스팅 시작 어셈블리의 `IHostingStartup` 구현 클래스 파일에 있습니다.

## <a name="discover-loaded-hosting-startup-assemblies"></a>로드된 호스팅 시작 어셈블리 검색

로드된 호스팅 시작 어셈블리를 검색하려면 로깅을 사용하도록 설정하고 앱의 로그를 확인합니다. 어셈블리를 로드할 때 발생하는 오류가 기록됩니다. 로드된 호스팅 시작 어셈블리는 디버그 수준에서 기록되고 모든 오류가 기록됩니다.

## <a name="disable-automatic-loading-of-hosting-startup-assemblies"></a>호스팅 시작 어셈블리의 자동 로드 사용 안 함

::: moniker range=">= aspnetcore-2.1"

호스팅 시작 어셈블리의 자동 로딩을 사용하지 않으려면 다음 방법 중 하나를 사용합니다.

* 모든 호스팅 시작 어셈블리가 로드되지 않도록 하려면 다음 중 하나를 `true` 또는 `1`로 설정합니다.
  * [호스팅 시작 방지](xref:fundamentals/host/web-host#prevent-hosting-startup) 호스트 구성 설정.
  * `ASPNETCORE_PREVENTHOSTINGSTARTUP` 환경 변수.
* 특정 호스팅 시작 어셈블리가 로드되지 않도록 하려면 시작 시 제외할 호스팅 시작 어셈블리의 세미콜론으로 구분된 문자열로 다음 중 하나를 설정합니다.
  * [호스팅 시작 어셈블리 제외](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies) 호스트 구성 설정.
  * `ASPNETCORE_HOSTINGSTARTUPEXCLUDEASSEMBLIES` 환경 변수.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

호스팅 시작 어셈블리의 자동 로딩을 사용하지 않으려면 다음 방법 중 하나를 `true` 또는 `1`로 설정합니다.

* [호스팅 시작 방지](xref:fundamentals/host/web-host#prevent-hosting-startup) 호스트 구성 설정.
* `ASPNETCORE_PREVENTHOSTINGSTARTUP` 환경 변수.

::: moniker-end

호스트 구성 설정과 환경 변수가 모두 설정되면 호스트 설정이 동작을 제어합니다.

호스트 설정 또는 환경 변수를 사용하여 호스팅 시작 어셈블리를 사용하지 않도록 설정하면 어셈블리가 전역적으로 해제되고 앱의 여러 특징을 해제할 수 있습니다.

## <a name="project"></a>프로젝트

다음 프로젝트 형식 중 하나를 사용하여 호스팅 시작을 만듭니다.

* [클래스 라이브러리](#class-library)
* [진입점 없는 콘솔 앱](#console-app-without-an-entry-point)

### <a name="class-library"></a>클래스 라이브러리

클래스 라이브러리에서 호스팅 시작 기능 향상을 제공할 수 있습니다. 라이브러리에는 `HostingStartup` 특성이 포함되어 있습니다.

[샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)에는 Razor 페이지 앱, *HostingStartupApp* 및 클래스 라이브러리, *HostingStartupLibrary*가 포함되어 있습니다. 클래스 라이브러리:

* `IHostingStartup`을 구현하는 호스트 시작 클래스(`ServiceKeyInjection`)가 포함되어 있습니다. `ServiceKeyInjection`은 메모리 내 구성 공급자([AddInMemoryCollection](/dotnet/api/microsoft.extensions.configuration.memoryconfigurationbuilderextensions.addinmemorycollection))를 사용하여 앱의 구성에 서비스 문자열 쌍을 추가합니다.
* 호스팅 시작의 네임스페이스 및 클래스를 식별하는 `HostingStartup` 특성을 포함합니다.

`ServiceKeyInjection` 클래스의 [구성](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 메서드는 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)를 사용하여 앱에 향상된 기능을 추가합니다. 호스팅 시작 어셈블리의 `IHostingStartup.Configure`는 사용자 코드로 `Startup.Configure` 전에 런타임에서 호출됩니다. 그러면 사용자 코드가 호스팅 시작 어셈블리에서 제공하는 모든 구성을 덮어쓸 수 있습니다.

*HostingStartupLibrary/ServiceKeyInjection.cs*:

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupLibrary/ServiceKeyInjection.cs?name=snippet1)]

앱의 인덱스 페이지는 클래스 라이브러리의 호스팅 시작 어셈블리에 의해 설정된 두 키에 대한 구성 값을 읽고 렌더링합니다.

*HostingStartupApp/Pages/Index.cshtml.cs*:

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupApp/Pages/Index.cshtml.cs?name=snippet1&highlight=5-6,11-12)]

[샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)에는 별도의 호스팅 시작인 *HostingStartupPackage*를 제공하는 NuGet 패키지 프로젝트도 포함되어 있습니다. 패키지는 앞에서 설명한 클래스 라이브러리와 같은 특징이 있습니다. 패키지:

* `IHostingStartup`을 구현하는 호스트 시작 클래스(`ServiceKeyInjection`)가 포함되어 있습니다. `ServiceKeyInjection`은 앱의 구성에 서비스 문자열 쌍을 추가합니다.
* `HostingStartup` 특성을 포함합니다.

*HostingStartupPackage/ServiceKeyInjection.cs*:

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupPackage/ServiceKeyInjection.cs?name=snippet1)]

앱의 인덱스 페이지는 패키지의 호스팅 시작 어셈블리에 의해 설정된 두 키에 대한 구성 값을 읽고 렌더링합니다.

*HostingStartupApp/Pages/Index.cshtml.cs*:

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupApp/Pages/Index.cshtml.cs?name=snippet1&highlight=7-8,13-14)]

### <a name="console-app-without-an-entry-point"></a>진입점 없는 콘솔 앱

*이 방법은 .NET Framework가 아닌 .NET Core 앱에서만 사용할 수 있습니다.*

활성화에 대한 컴파일 시간 참조가 필요하지 않은 동적 호스팅 시작 기능 향상은 진입점 없이 콘솔 앱에서 제공될 수 있습니다. 앱에는 `HostingStartup` 특성이 포함되어 있습니다. 동적 호스팅 시작을 만들려면:

1. 구현 라이브러리는 `IHostingStartup` 구현을 포함하는 클래스에서 생성됩니다. 구현 라이브러리는 기본 패키지로 처리됩니다.
1. 진입점이 없는 콘솔 앱은 구현 라이브러리 패키지를 참조합니다. 콘솔 앱은 다음과 같은 이유로 사용됩니다.
   * 종속성 파일은 실행 가능한 앱 자산이므로 라이브러리는 종속성 파일을 제공할 수 없습니다.
   * 라이브러리를 [런타임 패키지 저장소](/dotnet/core/deploying/runtime-store)에 직접 추가할 수 없습니다. 이 저장소에는 공유 런타임을 대상으로 하는 실행 가능한 프로젝트가 필요합니다.
1. 콘솔 앱은 호스팅 시작의 종속성을 얻기 위해 게시됩니다. 콘솔 앱을 게시하면 사용되지 않는 종속성이 종속성 파일에서 트리밍됩니다.
1. 앱 및 해당 종속성 파일이 런타임 패키지 저장소에 저장됩니다. 호스팅 시작 어셈블리 및 해당 종속성 파일을 검색하기 위해 한 쌍의 환경 변수에서 참조됩니다.

콘솔 앱은 [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) 패키지를 참조합니다.

[!code-xml[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.csproj)]

[HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 특성은 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost)를 빌드할 때 로드 및 실행을 위해 `IHostingStartup`의 구현으로 클래스를 식별합니다. 다음 예제에서 네임스페이스는 `StartupEnhancement`이고 클래스는 `StartupEnhancementHostingStartup`입니다.

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet1)]

클래스는 `IHostingStartup`을 구현합니다. 클래스의 [구성](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 메서드는 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)를 사용하여 앱에 향상된 기능을 추가합니다. 호스팅 시작 어셈블리의 `IHostingStartup.Configure`는 사용자 코드로 `Startup.Configure` 전에 런타임에서 호출됩니다. 그러면 사용자 코드가 호스팅 시작 어셈블리에서 제공하는 모든 구성을 덮어쓸 수 있습니다.

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet2&highlight=3,5)]

`IHostingStartup` 프로젝트를 빌드할 때 종속성 파일(*\*.deps.json*)은 어셈블리의 `runtime` 위치를 *bin* 폴더로 설정합니다.

[!code-json[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement1.deps.json?range=2-13&highlight=8)]

파일의 일부만 표시됩니다. 이 예제의 어셈블리 이름은 `StartupEnhancement`입니다.

## <a name="specify-the-hosting-startup-assembly"></a>호스팅 시작 어셈블리 지정

클래스 라이브러리 또는 콘솔 앱 제공 호스팅 시작의 경우 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 환경 변수에 호스팅 시작 어셈블리 이름을 지정합니다. 환경 변수는 세미콜론으로 구분된 어셈블리 목록입니다.

호스팅 시작 어셈블리만 `HostingStartup` 특성을 검사합니다. 샘플 앱(*HostingStartupApp*)의 경우 앞에서 설명한 호스팅 시작을 검색하기 위해 환경 변수가 다음 값으로 설정됩니다.

```
HostingStartupLibrary;HostingStartupPackage;StartupDiagnostics
```

호스팅 시작 어셈블리는 [호스팅 시작 어셈블리](xref:fundamentals/host/web-host#hosting-startup-assemblies) 호스트 구성 설정을 사용하여 설정할 수도 있습니다.

여러 개의 호스팅 시작 어셈블이 표시되어 있는 경우 해당 [구성](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 메서드가 어셈블리가 나열되는 순서대로 실행됩니다.

## <a name="activation"></a>활성화

호스팅 시작 활성화 옵션은 다음과 같습니다.

* [런타임 저장소](#runtime-store) &ndash; 활성화에는 활성화를 위한 컴파일 시간 참조가 필요하지 않습니다. 샘플 앱은 호스팅 시작 어셈블리 및 종속성 파일을 *배포* 폴더 안에 배치하여 다중 머신 환경에서 호스팅 시작의 배포를 용이하게 합니다. *배포* 폴더에는 호스팅 시작을 사용하도록 배포 시스템에 환경 변수를 만들거나 수정하는 PowerShell 스크립트도 포함되어 있습니다.
* 활성화에 필요한 컴파일 시간 참조
  * [NuGet 패키지](#nuget-package)
  * [프로젝트 bin 폴더](#project-bin-folder)

### <a name="runtime-store"></a>런타임 저장소

호스팅 시작 구현은 [런타임 저장소](/dotnet/core/deploying/runtime-store)에 배치됩니다. 향상된 앱에서는 어셈블리에 대한 컴파일 시간 참조가 필요하지 않습니다.

호스팅 시작이 빌드된 후 호스팅 시작의 프로젝트 파일은 [dotnet store](/dotnet/core/tools/dotnet-store) 명령의 매니페스트 파일로 사용됩니다.

```console
dotnet store --manifest <PROJECT_FILE> --runtime <RUNTIME_IDENTIFIER>
```

이 명령은 사용자 프로필의 런타임 저장소에 공유 프레임워크에 속하지 않는 호스팅 시작 어셈블리 및 기타 종속성을 배치합니다.

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

```
%USERPROFILE%\.dotnet\store\x64\<TARGET_FRAMEWORK_MONIKER>\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\<TARGET_FRAMEWORK_MONIKER>\
```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

```
/Users/<USER>/.dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

```
/Users/<USER>/.dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

---

글로벌 사용을 위한 어셈블리 및 종속성을 배치하려면 다음 경로를 사용하여 `-o|--output` 옵션을 `dotnet store` 명령에 추가합니다.

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

```
%PROGRAMFILES%\dotnet\store\x64\<TARGET_FRAMEWORK_MONIKER>\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\<TARGET_FRAMEWORK_MONIKER>\
```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

```
/usr/local/share/dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

```
/usr/local/share/dotnet/store/x64/<TARGET_FRAMEWORK_MONIKER>/<ENHANCEMENT_ASSEMBLY_NAME>/<ENHANCEMENT_VERSION>/lib/<TARGET_FRAMEWORK_MONIKER>/
```

---

**호스팅 시작의 종속성 파일 수정 및 배치**

런타임 위치는 *\*.deps.json* 파일에 지정됩니다. 향상된 기능을 활성화하려면 `runtime` 요소가 해당 기능 런타임 어셈블리의 위치를 지정해야 합니다. `runtime` 위치의 접두사를 `lib/<TARGET_FRAMEWORK_MONIKER>/`로 지정합니다.

[!code-json[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement2.deps.json?range=2-13&highlight=8)]

샘플 코드(*StartupDiagnostics* 프로젝트)에서 *\*.deps.json*파일의 수정은 [PowerShell](/powershell/scripting/powershell-scripting) 스크립트에 의해 수행됩니다. PowerShell 스크립트는 프로젝트 파일의 빌드 대상에서 자동으로 트리거합니다.

이제 구현의 *\*.deps.json* 파일은 액세스할 수 있는 위치에 있어야 합니다.

사용자별 사용의 경우 파일을 사용자 프로필 `.dotnet` 설정의 *additonalDeps* 폴더에 배치합니다.

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

```
%USERPROFILE%\.dotnet\x64\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\
```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

```
/Users/<USER>/.dotnet/x64/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

```
/Users/<USER>/.dotnet/x64/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

---

글로벌 사용의 경우 파일을 .NET Core 설치의 *additonalDeps* 폴더에 배치합니다.

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

```
%PROGRAMFILES%\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\
```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/
```

---

공유 프레임워크 버전은 대상 앱이 사용하는 공유 런타임 버전을 반영합니다. 공유 런타임은 *\*.runtimeconfig.json* 파일에 표시됩니다. 샘플 앱(*HostingStartupApp*)에서 공유 런타임은 *HostingStartupApp.runtimeconfig.json* 파일에 지정됩니다.

**호스팅 시작의 종속성 파일 목록**

구현의 *\*.deps.json* 파일 위치가 `DOTNET_ADDITIONAL_DEPS` 환경 변수에 나열됩니다.

파일이 사용자 프로필의 *.dotnet* 폴더에 있는 경우 환경 변수의 값을 다음과 같이 설정합니다.

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

```
%USERPROFILE%\.dotnet\x64\additionalDeps\
```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

```
/Users/<USER>/.dotnet/x64/additionalDeps/
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

```
/Users/<USER>/.dotnet/x64/additionalDeps/
```

---

전역 사용에서 파일을 .NET Core 설치에 배치하는 경우 파일에 전체 경로를 제공합니다.

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

```
%PROGRAMFILES%\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

```
/usr/local/share/dotnet/additionalDeps/<ENHANCEMENT_ASSEMBLY_NAME>/shared/Microsoft.NETCore.App/<SHARED_FRAMEWORK_VERSION>/<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

---

샘플 앱(*HostingStartupApp*)이 종속성 파일(*HostingStartupApp.runtimeconfig.json*)을 찾는 경우 종속성 파일은 사용자의 프로필에 배치됩니다.

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

`DOTNET_ADDITIONAL_DEPS` 환경 변수를 다음 값으로 설정합니다.

```
%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\
```

# <a name="macostabmacos"></a>[macOS](#tab/macos)

`DOTNET_ADDITIONAL_DEPS` 환경 변수를 다음 값으로 설정합니다.

```
/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

`DOTNET_ADDITIONAL_DEPS` 환경 변수를 다음 값으로 설정합니다.

```
/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/
```

---

다양한 운영 체제에 대한 환경 변수를 설정하는 방법의 예제는 [여러 환경 사용](xref:fundamentals/environments)을 참조하세요.

**배포**

다중 머신 환경에서 호스팅 시작의 배포를 용이하게 하기 위해 샘플 앱은 다음을 포함하는 게시된 출력에 *배포* 폴더를 만듭니다.

* 호스팅 시작 어셈블리.
* 호스팅 시작 종속성 파일.
* 호스팅 시작 활성화를 지원하기 위해 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 및 `DOTNET_ADDITIONAL_DEPS`를 만들거나 수정하는 PowerShell 스크립트입니다. 배포 시스템의 관리 PowerShell 명령 프롬프트에서 스크립트를 실행합니다.

### <a name="nuget-package"></a>NuGet 패키지

NuGet 패키지에서 호스팅 시작 기능 향상을 제공할 수 있습니다. 패키지에 `HostingStartup` 특성이 있습니다. 패키지에서 제공하는 호스팅 시작 형식은 다음 방법 중 하나를 통해 앱에서 사용할 수 있습니다.

* 향상된 앱의 프로젝트 파일은 앱의 프로젝트 파일(컴파일 시간 참조)에서 호스팅 시작을 위한 패키지 참조를 만듭니다. 이 곳에서 컴파일 시간 참조를 사용하면 호스팅 시작 어셈블리 및 모든 종속성이 앱의 종속성 파일(*\*.deps.json*)에 통합됩니다. 이 방식은 [nuget.org](https://www.nuget.org/)에 게시된 호스팅 시작 어셈블리 패키지에 적용됩니다.
* 호스팅 시작 종속성 파일은 [런타임 저장소](#runtime-store) 섹션에 설명된 대로 향상된 앱에서 사용할 수 있습니다(컴파일 시간 참조 없이).

NuGet 패키지 및 런타임 저장소에 대한 자세한 내용은 다음 항목을 참조하세요.

* [플랫폼 간 도구로 NuGet 패키지를 만드는 방법](/dotnet/core/deploying/creating-nuget-packages)
* [패키지 게시](/nuget/create-packages/publish-a-package)
* [런타임 패키지 저장소](/dotnet/core/deploying/runtime-store)

### <a name="project-bin-folder"></a>프로젝트 bin 폴더

호스팅 시작 향상 기능은 향상된 앱의 *bin* 배포 어셈블리에 의해 제공될 수 있습니다. 어셈블리에서 제공하는 호스팅 시작 형식은 다음 방법 중 하나를 통해 앱에서 사용할 수 있습니다.

* 향상된 앱의 프로젝트 파일은 호스팅 시작에 대한 어셈블리 참조를 만듭니다(컴파일 시간 참조). 이 곳에서 컴파일 시간 참조를 사용하면 호스팅 시작 어셈블리 및 모든 종속성이 앱의 종속성 파일(*\*.deps.json*)에 통합됩니다. 이 방법은 배포 시나리오에서 컴파일된 호스팅 시작 라이브러리의 어셈블리(DLL 파일)를 소비 프로젝트 또는 소비 프로젝트에서 액세스할 수 있는 위치로 이동하도록 요청하고 컴파일 시간 참조가 호스팅 시작 어셈블리에 필요한 경우에 적용됩니다.
* 호스팅 시작 종속성 파일은 [런타임 저장소](#runtime-store) 섹션에 설명된 대로 향상된 앱에서 사용할 수 있습니다(컴파일 시간 참조 없이).

## <a name="sample-code"></a>샘플 코드

[샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)([다운로드 방법](xref:index#how-to-download-a-sample))는 호스팅 시작 구현 시나리오를 보여 줍니다.

* 두 개의 호스팅 시작 어셈블리(클래스 라이브러리)는 각각 한 쌍의 메모리 내 구성 키-값 쌍을 설정합니다.
  * NuGet 패키지(*HostingStartupPackage*)
  * 클래스 라이브러리(*HostingStartupLibrary*)
* 호스팅 시작은 런타임 저장소 배포 어셈블리에서 활성화됩니다(*StartupDiagnostics*). 어셈블리는 시작 시 다음과 같은 진단 정보를 제공하는 두 개의 미들웨어를 앱에 추가합니다.
  * 등록된 서비스
  * 주소(구성표, 호스트, 기본 경로, 경로, 쿼리 문자열)
  * 연결(원격 IP, 원격 포트, 로컬 IP, 로컬 포트, 클라이언트 인증서)
  * 요청 헤더
  * 환경 변수

샘플을 실행하려면:

**NuGet 패키지에서 활성화**

1. [dotnet pack](/dotnet/core/tools/dotnet-pack) 명령을 사용하여 *HostingStartupPackage* 패키지를 컴파일합니다.
1. *HostingStartupPackage* 패키지의 어셈블리 이름을 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 환경 변수에 추가합니다.
1. 앱을 컴파일하고 실행합니다. 패키지 참조가 향상된 앱(컴파일 시간 참조)에 있습니다. 앱의 프로젝트 파일에 있는 `<PropertyGroup>`에서는 패키지 프로젝트의 출력(*../HostingStartupPackage/bin/Debug*)을 패키지 원본으로 지정합니다. 이렇게 하면 [nuget.org](https://www.nuget.org/)에 패키지를 업로드하지 않고 패키지를 사용할 수 있습니다. 자세한 내용은 HostingStartupApp의 프로젝트 파일에 있는 정보를 참조하세요.

   ```xml
   <PropertyGroup>
     <RestoreSources>$(RestoreSources);https://api.nuget.org/v3/index.json;../HostingStartupPackage/bin/Debug</RestoreSources>
   </PropertyGroup>
   ```
1. 인덱스 페이지에 의해 렌더링된 서비스 구성 키 값이 패키지의 `ServiceKeyInjection.Configure` 메서드에서 설정된 값과 일치하는지 확인합니다.

*HostingStartupPackage* 프로젝트를 변경하고 다시 컴파일하는 경우, 로컬 NuGet 패키지 캐시의 선택을 취소하여 *HostingStartupApp*이 로컬 캐시에서 부실 패키지가 아닌 업데이트된 패키지를 수신하는지 확인합니다. 로컬 NuGet 캐시를 지우려면 다음 [dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals) 명령을 실행합니다.

```console
dotnet nuget locals all --clear
```

**클래스 라이브러리에서 활성화**

1. [dotnet build](/dotnet/core/tools/dotnet-build) 명령을 사용하여 *HostingStartupLibrary* 클래스 라이브러리를 컴파일합니다.
1. *HostingStartupLibrary* 클래스 라이브러리의 어셈블리 이름을 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 환경 변수에 추가합니다.
1. *bin* - *HostingStartupLibrary.dll* 파일을 클래스 라이브러리의 컴파일된 출력에서 앱의 *bin/Debug* 폴더로 복사하여 클래스 라이브러리의 어셈블리를 앱에 배포합니다.
1. 앱을 컴파일하고 실행합니다. 앱의 프로젝트 파일에 있는 `<ItemGroup>`는 클래스 라이브러리의 어셈블리(*.\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll*) (컴파일 시간 참조)를 참조하세요. 자세한 내용은 HostingStartupApp의 프로젝트 파일에 있는 정보를 참조하세요.

   ```xml
   <ItemGroup>
     <Reference Include=".\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll">
       <HintPath>.\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll</HintPath>
       <SpecificVersion>False</SpecificVersion>
     </Reference>
   </ItemGroup>
   ```
1. 인덱스 페이지에 의해 렌더링된 서비스 구성 키 값이 클래스 라이브러리의 `ServiceKeyInjection.Configure` 메서드에서 설정된 값과 일치하는지 확인합니다.

**런타임 저장소 배포 어셈블리에서 활성화**

1. *StartupDiagnostics* 프로젝트는 [PowerShell](/powershell/scripting/powershell-scripting)을 사용하여 해당 *StartupDiagnostics.deps.json* 파일을 수정합니다. PowerShell은 Windows 7 SP1 및 Windows Server 2008 R2 SP1부터 Windows에서 기본적으로 설치됩니다. 다른 플랫폼에서 PowerShell을 가져오려면 [Windows PowerShell 설치](/powershell/scripting/setup/installing-powershell#powershell-core)를 참조하세요.
1. *StartupDiagnostics* 프로젝트를 빌드합니다. 프로젝트를 빌드한 후 프로젝트 파일의 빌드 대상이 자동으로 다음과 같습니다.
   * PowerShell 스크립트를 트리거하여 *StartupDiagnostics.deps.json* 파일을 수정합니다.
   * *StartupDiagnostics.deps.json* 파일을 사용자 프로필의 *additionalDeps* 폴더로 이동합니다.
1. 호스팅 시작 디렉터리의 명령 프롬프트에서 `dotnet store` 명령을 실행하여 어셈블리 및 해당 종속성을 사용자 프로필의 런타임 저장소에 저장합니다.

   ```console
   dotnet store --manifest StartupDiagnostics.csproj --runtime <RID>
   ```
   Windows의 경우 명령은 `win7-x64` [RID(런타임 식별자)](/dotnet/core/rid-catalog)를 사용합니다. 다른 런타임에 호스팅 시작을 제공할 때 올바른 RID로 대체합니다.
1. 환경 변수를 설정합니다.
   * *StartupDiagnostics*의 어셈블리 이름을 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 환경 변수에 추가합니다.
   * Windows의 경우 `DOTNET_ADDITIONAL_DEPS` 환경 변수를 `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`로 설정합니다. Linux/macOS에서는 `DOTNET_ADDITIONAL_DEPS` 환경 변수를 `/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/`로 설정합니다. 여기서 `<USER>`는 호스팅 시작을 포함하는 사용자 프로필입니다.
1. 샘플 앱을 실행합니다.
1. `/services` 엔드포인트가 앱의 등록된 서비스를 확인하도록 요청합니다. `/diag` 엔드포인트가 진단 정보를 확인하도록 요청합니다.
