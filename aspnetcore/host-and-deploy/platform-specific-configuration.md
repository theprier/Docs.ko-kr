---
title: IHostingStartup와 ASP.NET Core에서 플랫폼 관련 구성 사용 하 여 앱 기능을 추가 합니다.
author: guardrex
description: IHostingStartup 구현을 사용 하 여 외부 어셈블리의 기능을 ASP.NET Core 응용 프로그램을 추가 하는 방법을 알아봅니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 12/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/platform-specific-configuration
ms.openlocfilehash: 1b899e3d510be83cbd4c03368e5c2d6226706a66
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="add-app-features-with-a-platform-specific-configuration-in-aspnet-core"></a>ASP.NET Core에서 플랫폼 관련 구성 사용 하 여 앱 기능을 추가 합니다.

[Luke Latham](https://github.com/guardrex)으로

[IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) 구현 하면 응용 프로그램의 외부 어셈블리 외부에서 시작 시 응용 프로그램에 기능 추가 `Startup` 클래스입니다. 예를 들어 외부 도구 라이브러리 사용할 수는 `IHostingStartup` 구현을 추가 하는 구성 공급자 또는 응용 프로그램 서비스를 제공 합니다. `IHostingStartup` *이상에서 ASP.NET Core 2.0에서 사용할 수는 있습니다.*

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/platform-specific-configuration/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="discover-loaded-hosting-startup-assemblies"></a>로드 된 호스팅 시작 어셈블리를 검색 합니다.

응용 프로그램에서 또는 라이브러리를 통해 로드 호스팅 시작 어셈블리를 검색 하려면 로깅을 사용 하도록 설정 하 고 응용 프로그램 로그를 확인 합니다. 어셈블리를 로드할 때 발생 하는 오류가 기록 됩니다. 로드 된 호스팅 시작 어셈블리 디버그 수준에서 로깅됩니다 및 모든 오류가 기록 됩니다.

샘플 응용 프로그램 읽기는 [HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey) 에 `string` 배열 하 고 응용 프로그램의 인덱스 페이지에 결과 표시 합니다.

[!code-csharp[](platform-specific-configuration/sample/HostingStartupSample/Pages/Index.cshtml.cs?name=snippet1&highlight=14-16)]

## <a name="disable-automatic-loading-of-hosting-startup-assemblies"></a>호스팅 시작 어셈블리의 자동 로드 사용 안 함

호스팅 시작 어셈블리의 자동 로드를 사용 하지 않도록 설정 하는 두 가지 있습니다.

* 설정의 [호스팅 시작 방지](xref:fundamentals/hosting#prevent-hosting-startup) 호스트 구성 설정입니다.
* 설정의 `ASPNETCORE_preventHostingStartup` 환경 변수입니다.

호스트 설정 또는 환경 변수로 설정 된 경우 `true` 또는 `1`호스팅, 시작 어셈블리를 자동으로 로드 되지 않습니다. 모두 설정 하는 경우 호스트 설정 동작을 제어 합니다.

호스트 설정 및 환경 변수를 사용 하 여 호스팅 시작 어셈블리를 사용 하지 않도록 설정에 전체적으로 비활성화 하 고 응용 프로그램의 몇 가지 기능을 해제할 수 있습니다. 현재 라이브러리 자체 구성 옵션에서 제공 하지 않으면 라이브러리에서 추가 호스팅 시작 어셈블리를 선택적으로 해제 하는 것이 불가능 합니다. 이후 릴리스에서 호스팅 시작 어셈블리를 선택적으로 해제 하는 기능을 제공할 (참조 [GitHub 발급 aspnet/호스팅 #1243](https://github.com/aspnet/Hosting/pull/1243)).

## <a name="implement-ihostingstartup-features"></a>IHostingStartup 기능 구현

### <a name="create-the-assembly"></a>어셈블리 만들기

`IHostingStartup` 기능은 진입점 하지 않고 콘솔 응용 프로그램에 따라 어셈블리도 배포 합니다. 어셈블리 참조는 [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) 패키지:

[!code-xml[](platform-specific-configuration/snapshot_sample/StartupFeature.csproj)]

A [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 의 구현으로 클래스를 식별 하는 특성 `IHostingStartup` 로드 및 빌드할 때 실행을 위한는 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost)합니다. 다음 예제에서는 네임 스페이스는 `StartupFeature`, 고 클래스는 `StartupFeatureHostingStartup`:

[!code-csharp[](platform-specific-configuration/snapshot_sample/StartupFeature.cs?name=snippet1)]

클래스가 구현 하는 `IHostingStartup`합니다. 클래스의 [구성](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 메서드는 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 기능 응용 프로그램을 추가 하려면:

[!code-csharp[](platform-specific-configuration/snapshot_sample/StartupFeature.cs?name=snippet2&highlight=3,5)]

빌드할 때는 `IHostingStartup` 프로젝트, 종속성 파일 (*\*. deps.json*) 설정 하는 `runtime` 어셈블리의 위치는 *bin* 폴더:

[!code-json[](platform-specific-configuration/snapshot_sample/StartupFeature1.deps.json?range=2-13&highlight=8)]

파일의 일부만 표시 됩니다. 이 예제에 어셈블리 이름이 `StartupFeature`합니다.

### <a name="update-the-dependencies-file"></a>종속성 파일 업데이트

에 지정 된 런타임 위치는  *\*. deps.json* 파일입니다. 기능을 활성는 `runtime` 요소 기능의 런타임 어셈블리의 위치를 지정 해야 합니다. 접두사는 `runtime` 위치 `lib/netcoreapp2.0/`:

[!code-json[](platform-specific-configuration/snapshot_sample/StartupFeature2.deps.json?range=2-13&highlight=8)]

샘플 응용 프로그램의 수정 된  *\*. deps.json* 파일에 의해 수행 됩니다는 [PowerShell](/powershell/scripting/powershell-scripting) 스크립트입니다. PowerShell 스크립트는 프로젝트 파일의 빌드 대상에서 자동으로 트리거됩니다.

### <a name="feature-activation"></a>기능 활성화

**어셈블리 파일을 배치**

`IHostingStartup` 구현의 어셈블리 파일이 있어야 *bin*-응용 프로그램에 배포 또는에 [런타임 저장소](/dotnet/core/deploying/runtime-store):

사용자 단위 사용에 대 한 어셈블리에서 사용자 프로필의 런타임 저장소에 배치 합니다.

```
<DRIVE>\Users\<USER>\.dotnet\store\x64\netcoreapp2.0\<FEATURE_ASSEMBLY_NAME>\<FEATURE_VERSION>\lib\netcoreapp2.0\
```

전역 사용에 대 한 어셈블리의.NET Core 설치 런타임 저장소에 배치 합니다.

```
<DRIVE>\Program Files\dotnet\store\x64\netcoreapp2.0\<FEATURE_ASSEMBLY_NAME>\<FEATURE_VERSION>\lib\netcoreapp2.0\
```

런타임 저장소에 어셈블리를 배포 하는 경우 기호 파일도 배포 될 수 있지만 기능이 작동 하려면 필요 하지 않습니다.

**종속성 파일 배치**

이제 구현의  *\*. deps.json* 파일 액세스할 수 있는 위치에 있어야 합니다.

사용자별으로 사용 하기 위해에서 파일을 배치는 `additonalDeps` 사용자 프로필의 폴더 `.dotnet` 설정: 

```
<DRIVE>\Users\<USER>\.dotnet\x64\additionalDeps\<FEATURE_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\2.0.0\
```

전역 사용에 대 한 배치 파일에는 `additonalDeps` .NET Core 설치의 폴더:

```
<DRIVE>\Program Files\dotnet\additionalDeps\<FEATURE_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\2.0.0\
```

버전을 기록 `2.0.0`에서 대상 응용 프로그램을 사용 하는 공유 런타임 버전을 반영 합니다. 공유 런타임에 표시 되는  *\*. runtimeconfig.json* 파일입니다. 에 지정 된 공유 런타임 샘플 앱에는 *HostingStartupSample.runtimeconfig.json* 파일입니다.

**환경 변수 설정**

기능을 사용 하는 앱의 컨텍스트에서 다음과 같은 환경 변수를 설정 합니다.

ASPNETCORE\_HOSTINGSTARTUPASSEMBLIES

호스팅 시작 어셈블리만 검색는 `HostingStartupAttribute`합니다. 구현 어셈블리 이름은이 환경 변수에서 제공 됩니다. 이 값을 설정 하는 샘플 응용 프로그램 `StartupDiagnostics`합니다.

사용 하 여 값 설정할 수도 있습니다는 [호스팅 시작 어셈블리가](xref:fundamentals/hosting#hosting-startup-assemblies) 호스트 구성 설정입니다.

DOTNET\_추가\_DEPS

구현 위치  *\*. deps.json* 파일입니다.

파일은 사용자 프로필에 저장 하는 경우 *.dotnet* 사용자 단위 사용에 대 한 폴더:

```
<DRIVE>\Users\<USER>\.dotnet\x64\additionalDeps\
```

파일을 전역 사용에 대 한.NET Core 설치에 배치 하는 경우 파일에 전체 경로 제공 합니다.

```
<DRIVE>\Program Files\dotnet\additionalDeps\<FEATURE_ASSEMBLY_NAME>\shared\Microsoft.NETCore.App\2.0.0\<FEATURE_ASSEMBLY_NAME>.deps.json
```

이 값을 설정 하는 샘플 응용 프로그램:

```
%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\
```

다양 한 운영 체제에 대 한 환경 변수를 설정 하는 방법의 예 참조 [여러 환경 작업할](xref:fundamentals/environments)합니다.

## <a name="sample-app"></a>샘플 응용 프로그램

[샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/platform-specific-configuration/sample/) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample)) 사용 하 여 `IHostingStartup` 진단 도구를 만드는 합니다. 두 middlewares 진단 정보를 제공 하는 시작 시 응용 프로그램에 추가 하는 도구:

* 등록 된 서비스
* 주소: 구성표, 호스트, 기본 경로, 경로, 쿼리 문자열
* 연결: 원격 IP, 원격 포트, 로컬 IP 로컬 포트를 클라이언트 인증서
* 요청 헤더
* 환경 변수

샘플을 실행 하려면

1. 진단 시작 프로젝트를 사용 하 여 [PowerShell](/powershell/scripting/powershell-scripting) 수정 하려면 해당 *StartupDiagnostics.deps.json* 파일입니다. PowerShell은 Windows 7 SP1 및 Windows Server 2008 R2 s p 1 부터는 Windows 운영 체제에서 기본적으로 설치 됩니다. 다른 플랫폼에서 PowerShell을 얻으려고 참조 [Windows PowerShell 설치](/powershell/scripting/setup/installing-windows-powershell)합니다.
2. 진단 시작 프로젝트를 빌드하십시오. 프로젝트 파일에 빌드 대상:
   * 어셈블리를 이동 하 고 기호 파일에서 사용자 프로필의 런타임 저장소에 키를 누릅니다.
   * 수정 하는 PowerShell 스크립트를 트리거하는 *StartupDiagnostics.deps.json* 파일입니다.
   * 이동 된 *StartupDiagnostics.deps.json* 사용자 프로필에 대 한 파일 `additionalDeps` 폴더입니다.
3. 환경 변수를 설정 합니다.
    * `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`: `StartupDiagnostics`
    * `DOTNET_ADDITIONAL_DEPS`: `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`
4. 샘플 응용 프로그램을 실행 합니다.
5. 요청 된 `/services` 응용 프로그램의를 참조 하는 끝점 서비스를 등록 합니다. 요청 된 `/diag` 진단 정보를 확인 하는 끝점입니다.
