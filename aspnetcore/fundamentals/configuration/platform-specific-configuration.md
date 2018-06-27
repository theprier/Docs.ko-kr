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
ms.openlocfilehash: 47d3a64ce0cc543162a066eeeaa0aaaf7dc96a5f
ms.sourcegitcommit: 0d6f151e69c159d776ed0142773279e645edbc0a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/13/2018
ms.locfileid: "35415010"
---
# <a name="enhance-an-app-from-an-external-assembly-in-aspnet-core-with-ihostingstartup"></a>IHostingStartup을 사용하여 ASP.NET Core의 외부 어셈블리에서 앱 강화

[Luke Latham](https://github.com/guardrex)으로

[IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) 구현에서는 시작 시 앱의 `Startup` 클래스 외부에 있는 외부 어셈블리에서 앱에 향상된 기능을 추가할 수 있습니다. 예를 들어 외부 도구 라이브러리는 `IHostingStartup` 구현을 사용하여 앱에 추가 구성 공급자 또는 서비스를 제공할 수 있습니다. `IHostingStartup` *는 ASP.NET Core 2.0 이상에서 지원됩니다.*

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/platform-specific-configuration/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="discover-loaded-hosting-startup-assemblies"></a>로드된 호스팅 시작 어셈블리 검색

앱 또는 라이브러리에서 로드한 호스팅 시작 어셈블리를 검색하려면 로깅을 사용하도록 설정하고 응용 프로그램 로그를 확인합니다. 어셈블리를 로드할 때 발생하는 오류가 기록됩니다. 로드된 호스팅 시작 어셈블리는 디버그 수준에서 기록되고 모든 오류가 기록됩니다.

샘플 앱은 [HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey)를 `string` 배열로 읽고 앱의 인덱스 페이지에 결과를 표시합니다.

[!code-csharp[](platform-specific-configuration/sample/HostingStartupSample/Pages/Index.cshtml.cs?name=snippet1&highlight=14-16)]

## <a name="disable-automatic-loading-of-hosting-startup-assemblies"></a>호스팅 시작 어셈블리의 자동 로드 사용 안 함

호스팅 시작 어셈블리의 자동 로드를 사용하지 않도록 설정하는 두 가지 방법이 있습니다.

* [호스팅 스타트업 방지](xref:fundamentals/host/web-host#prevent-hosting-startup) 호스트 구성 설정을 설정합니다.
* `ASPNETCORE_PREVENTHOSTINGSTARTUP` 환경 변수를 설정합니다.

호스트 설정 또는 환경 변수를 `true` 또는 `1`로 설정한 경우 호스팅 시작 어셈블리를 자동으로 로드하지 않습니다. 모두 설정하는 경우 호스트 설정은 동작을 제어합니다.

호스트 설정 및 환경 변수를 사용하여 호스팅 시작 어셈블리를 사용하지 않도록 설정하면 전역적으로 해제되고 앱의 여러 특징을 해제할 수 있습니다. 현재 라이브러리가 고유한 구성 옵션을 제공하지 않으면 라이브러리에서 추가한 호스팅 시작 어셈블리를 선택적으로 해제할 수 없습니다. 이후 릴리스에서는 호스팅 시작 어셈블리를 선택적으로 해제하는 기능을 제공할 예정입니다([GitHub 문제 aspnet/호스팅 #1243](https://github.com/aspnet/Hosting/pull/1243) 참조).

## <a name="implement-ihostingstartup"></a>IHostingStartup 구현

### <a name="create-the-assembly"></a>어셈블리 만들기

`IHostingStartup` 향상 기능은 진입점 없이 콘솔 앱에 따라 어셈블리로 배포됩니다. 어셈블리는 [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) 패키지를 참조합니다.

[!code-xml[](platform-specific-configuration/snapshot_sample/StartupEnhancement.csproj)]

[HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 특성은 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost)를 빌드할 때 로드 및 실행을 위해 `IHostingStartup`의 구현으로 클래스를 식별합니다. 다음 예제에서 네임스페이스는 `StartupEnhancement`이고 클래스는 `StartupEnhancementHostingStartup`입니다.

[!code-csharp[](platform-specific-configuration/snapshot_sample/StartupEnhancement.cs?name=snippet1)]

클래스는 `IHostingStartup`을 구현합니다. 클래스의 [구성](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 메서드는 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)를 사용하여 앱에 향상된 기능을 추가합니다. 호스팅 시작 어셈블리의 `IHostingStartup.Configure`는 사용자 코드로 `Startup.Configure` 전에 런타임에서 호출됩니다. 그러면 사용자 코드가 호스팅 시작 어셈블리에서 제공하는 모든 구성을 덮어쓸 수 있습니다.

[!code-csharp[](platform-specific-configuration/snapshot_sample/StartupEnhancement.cs?name=snippet2&highlight=3,5)]

`IHostingStartup` 프로젝트를 빌드할 때 종속성 파일(*\*.deps.json*)은 어셈블리의 `runtime` 위치를 *bin* 폴더로 설정합니다.

[!code-json[](platform-specific-configuration/snapshot_sample/StartupEnhancement1.deps.json?range=2-13&highlight=8)]

파일의 일부만 표시됩니다. 이 예제의 어셈블리 이름은 `StartupEnhancement`입니다.

### <a name="update-the-dependencies-file"></a>종속성 파일 업데이트

런타임 위치는 *\*.deps.json* 파일에 지정됩니다. 향상된 기능을 활성화하려면 `runtime` 요소가 해당 기능 런타임 어셈블리의 위치를 지정해야 합니다. `runtime` 위치의 접두사를 `lib/<TARGET_FRAMEWORK_MONIKER>/`로 지정합니다.

[!code-json[](platform-specific-configuration/snapshot_sample/StartupEnhancement2.deps.json?range=2-13&highlight=8)]

샘플 앱에서 *\*.deps.json* 파일은 [PowerShell](/powershell/scripting/powershell-scripting) 스크립트에 의해 수정됩니다. PowerShell 스크립트는 프로젝트 파일의 빌드 대상에서 자동으로 트리거합니다.

### <a name="enhancement-activation"></a>향상된 기능 활성화

**어셈블리 파일 배치**

`IHostingStartup` 구현의 어셈블리 파일은 앱에 배포되거나 [런타임 저장소](/dotnet/core/deploying/runtime-store)에 배치된 *bin*이어야 합니다.

사용자 단위 사용의 경우 어셈블리를 사용자 프로필의 런타임 저장소에 배치합니다.

```
<DRIVE>\Users\<USER>\.dotnet\store\x64\<TARGET_FRAMEWORK_MONIKER>\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\<TARGET_FRAMEWORK_MONIKER>\
```

전역 사용의 경우 어셈블리를 .NET Core 설치의 런타임 저장소에 배치합니다.

```
<DRIVE>\Program Files\dotnet\store\x64\<TARGET_FRAMEWORK_MONIKER>\<ENHANCEMENT_ASSEMBLY_NAME>\<ENHANCEMENT_VERSION>\lib\<TARGET_FRAMEWORK_MONIKER>\
```

런타임 저장소에 어셈블리를 배포할 때 기호 파일도 배포될 수 있지만 향상된 기능이 작동하는 데 필수 조건은 아닙니다.

**종속성 파일 배치**

이제 구현의 *\*.deps.json* 파일은 액세스할 수 있는 위치에 있어야 합니다.

사용자 단위 사용의 경우 파일을 사용자 프로필 `.dotnet` 설정의 `additonalDeps` 폴더에 배치합니다.

```
<DRIVE>\Users\<USER>\.dotnet\x64\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\
```

전역 사용의 경우 파일을 .NET Core 설치의 `additonalDeps` 폴더에 배치합니다.

```
<DRIVE>\Program Files\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\
```

공유 프레임워크 버전은 대상 앱이 사용하는 공유 런타임 버전을 반영합니다. 공유 런타임은 *\*.runtimeconfig.json* 파일에 표시됩니다. 샘플 앱에서 공유 런타임은 *HostingStartupSample.runtimeconfig.json* 파일에 지정됩니다.

**환경 변수 설정**

향상된 기능을 사용하는 앱의 컨텍스트에서 다음 환경 변수를 설정합니다.

ASPNETCORE_HOSTINGSTARTUPASSEMBLIES

호스팅 시작 어셈블리만이 `HostingStartupAttribute`을 검사합니다. 구현의 어셈블리 이름은 이 환경 변수에서 제공됩니다. 샘플 앱은 이 값을 `StartupDiagnostics`로 설정합니다.

[호스팅 스타트업 어셈블리](xref:fundamentals/host/web-host#hosting-startup-assemblies) 호스트 구성 설정을 사용하여 값을 설정할 수도 있습니다.

여러 개의 호스팅 시작 어셈블이 표시되어 있는 경우 해당 [구성](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 메서드가 어셈블리가 나열되는 순서대로 실행됩니다.

DOTNET_ADDITIONAL_DEPS

구현 *\*.deps.json* 파일의 위치입니다.

사용자 단위 사용에서 파일이 사용자 프로필의 *.dotnet* 폴더에 배치되는 경우:

```
<DRIVE>\Users\<USER>\.dotnet\x64\additionalDeps\
```

전역 사용에서 파일을 .NET Core 설치에 배치하는 경우 파일에 전체 경로를 제공합니다.

```
<DRIVE>\Program Files\dotnet\additionalDeps\<ENHANCEMENT_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\<SHARED_FRAMEWORK_VERSION>\<ENHANCEMENT_ASSEMBLY_NAME>.deps.json
```

샘플 앱은 이 값을 다음으로 설정합니다.

```
%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\
```

다양한 운영 체제에 대한 환경 변수를 설정하는 방법의 예제는 [여러 환경 사용](xref:fundamentals/environments)을 참조하세요.

## <a name="sample-app"></a>샘플 앱

[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/platform-specific-configuration/sample/)([다운로드하는 방법](xref:tutorials/index#how-to-download-a-sample))은 `IHostingStartup`를 사용하여 진단 도구를 만듭니다. 도구는 시작 시 앱에 진단 정보를 제공하는 두 개의 미들웨어를 추가합니다.

* 등록된 서비스
* 주소: 구성표, 호스트, 기본 경로, 경로, 쿼리 문자열
* 연결: 원격 IP, 원격 포트, 로컬 IP, 로컬 포트, 클라이언트 인증서
* 요청 헤더
* 환경 변수

샘플을 실행하려면:

1. 스타트업 진단 프로젝트는 [PowerShell](/powershell/scripting/powershell-scripting)을 사용하여 해당 *StartupDiagnostics.deps.json* 파일을 수정합니다. PowerShell은 Windows 7 SP1 및 Windows Server 2008 R2 SP1부터 Windows OS에서 기본적으로 설치됩니다. 다른 플랫폼에서 PowerShell을 가져오려면 [Windows PowerShell 설치](/powershell/scripting/setup/installing-windows-powershell)를 참조하세요.
2. 스타트업 진단 프로젝트를 빌드합니다. 프로젝트 파일의 빌드 대상:
   * 어셈블리 및 기호 파일을 사용자 프로필의 런타임 저장소로 이동합니다.
   * PowerShell 스크립트를 트리거하여 *StartupDiagnostics.deps.json* 파일을 수정합니다.
   * *StartupDiagnostics.deps.json* 파일을 사용자 프로필의 `additionalDeps` 폴더로 이동합니다.
3. 환경 변수를 설정합니다.
    * `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`: `StartupDiagnostics`
    * `DOTNET_ADDITIONAL_DEPS`: `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`
4. 샘플 앱을 실행합니다.
5. `/services` 엔드포인트가 앱의 등록된 서비스를 확인하도록 요청합니다. `/diag` 엔드포인트가 진단 정보를 확인하도록 요청합니다.
