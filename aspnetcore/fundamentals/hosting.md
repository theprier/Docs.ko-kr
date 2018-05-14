---
title: ASP.NET Core에서 호스팅
author: guardrex
description: 앱 시작 및 수명 관리를 담당하는 ASP.NET Core에서의 웹 호스트에 대해 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 09/21/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/hosting
ms.openlocfilehash: 344bf5f0917f4c33d67eeb14176ff2aae3ae75da
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="hosting-in-aspnet-core"></a>ASP.NET Core에서 호스팅

[Luke Latham](https://github.com/guardrex)으로

ASP.NET Core 앱은 *호스트*를 구성 및 실행합니다. 호스트는 앱 시작 및 수명 관리를 담당합니다. 최소한으로 호스트는 서버 및 요청 처리 파이프라인을 구성합니다.

## <a name="setting-up-a-host"></a>호스트 설정

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)의 인스턴스를 사용하여 호스트를 만듭니다. 이는 일반적으로 앱의 진입점에서 수행되는 `Main` 메서드입니다. 프로젝트 템플릿에서 `Main`은 *Program.cs*에 있습니다. 일반적인 *Program.cs*는 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)를 호출하여 호스트 설정을 시작합니다.

[!code-csharp[](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main)]

`CreateDefaultBuilder`는 다음 작업을 수행합니다.

* [Kestrel](servers/kestrel.md)을 웹 서버로 구성합니다. Kestrel 기본 옵션의 경우 [ASP.NET Core에서 Kestrel 웹 서버 구현의 Kestrel 옵션 섹션](xref:fundamentals/servers/kestrel#kestrel-options)을 참조하세요.
* 콘텐츠 루트를 [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory)에서 반환된 경로로 설정합니다.
* 다음에서 선택적인 구성을 로드합니다.
  * *appsettings.json*.
  * *appsettings.{Environment}.json*.
  * [사용자 비밀](xref:security/app-secrets) - 앱이 `Development` 환경에서 실행되는 경우.
  * 환경 변수.
  * 명령줄 인수.
* 콘솔 및 디버그 출력에 대한 [로깅](xref:fundamentals/logging/index)을 구성합니다. 로깅은 *appsettings.json* 또는 *appsettings.{Environment}.json* 파일의 로깅 구성 섹션에 지정된 [로그 필터링](xref:fundamentals/logging/index#log-filtering) 규칙을 포함합니다.
* IIS 뒤에서 실행하는 경우 [IIS 통합](xref:host-and-deploy/iis/index)을 활성화합니다. [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 사용하는 경우 서버가 수신 대기할 기본 경로 및 포트를 구성합니다. 모듈은 IIS와 Kestrel 간에 역방향 프록시를 만듭니다. 또한 [시작 오류를 캡처](#capture-startup-errors)하도록 앱을 구성합니다. IIS 기본 옵션의 경우 [IIS가 있는 Windows에서 ASP.NET Core 호스팅의 IIS 옵션 섹션](xref:host-and-deploy/iis/index#iis-options)을 참조하세요.
* 앱의 환경이 개발인 경우 [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes)을 `true`으로 설정합니다. 자세한 내용은 [범위 유효성 검사](#scope-validation)를 참조하세요.

*콘텐츠 루트*는 호스트가 MVC 뷰 파일과 같은 콘텐츠 파일을 검색하는 위치를 결정합니다. 앱이 프로젝트의 루트 폴더에서 시작되면 프로젝트의 루트 폴더가 콘텐츠 루트로 사용됩니다. 이것이 [Visual Studio](https://www.visualstudio.com/) 및 [dotnet 새 템플릿](/dotnet/core/tools/dotnet-new)에서 사용되는 기본값입니다.

앱 구성에 대한 자세한 내용은 [ASP.NET Core의 구성](xref:fundamentals/configuration/index)을 참조하세요.

> [!NOTE]
> ASP.NET Core 2.x에서는 정적 `CreateDefaultBuilder` 메서드 사용에 대한 대안으로 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)에서 호스트를 만들 수 있도록 지원합니다. 자세한 내용은 ASP.NET Core 1.x 탭을 참조하세요.

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)의 인스턴스를 사용하여 호스트를 만듭니다. 호스트 만들기는 일반적으로 앱의 진입점에서 수행되는 `Main` 메서드입니다. 프로젝트 템플릿에서 `Main`은 *Program.cs*에 있습니다.

[!code-csharp[](../common/samples/WebApplication1/Program.cs)]

`WebHostBuilder`에는 [IServer를 구현하는 서버](servers/index.md)가 필요합니다. 기본 제공 서버는 [Kestrel](servers/kestrel.md) 및 [HTTP.sys](servers/httpsys.md)(ASP.NET Core 2.0 출시 전에 HTTP.sys는 [WebListener](xref:fundamentals/servers/weblistener)로 불림)입니다. 이 예제에서는 [UseKestrel 확장 메서드](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)가 Kestrel 서버를 지정합니다.

*콘텐츠 루트*는 호스트가 MVC 뷰 파일과 같은 콘텐츠 파일을 검색하는 위치를 결정합니다. [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1)에서 `UseContentRoot`에 대한 기본 콘텐츠 루트를 가져옵니다. 앱이 프로젝트의 루트 폴더에서 시작되면 프로젝트의 루트 폴더가 콘텐츠 루트로 사용됩니다. 이것이 [Visual Studio](https://www.visualstudio.com/) 및 [dotnet 새 템플릿](/dotnet/core/tools/dotnet-new)에서 사용되는 기본값입니다.

IIS를 역방향 프록시로 사용하려면 호스트 빌드 과정 중 일환으로 [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions)을 호출합니다. `UseIISIntegration`은 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)과 달리 *서버*를 구성하지 않습니다. `UseIISIntegration`은 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 사용하여 Kestrel과 IIS 간 역방향 프록시를 만드는 경우 서버가 수신 대기할 기본 경로 및 포트를 구성합니다. ASP.NET Core와 함께 IIS를 사용하려면 `UseKestrel` 및 `UseIISIntegration`을 지정해야 합니다. `UseIISIntegration`은 IIS 또는 IIS Express 뒤에서 실행하는 경우에만 활성화됩니다. 자세한 내용은 [ASP.NET Core 모듈 소개](xref:fundamentals/servers/aspnet-core-module) 및 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.

호스트(및 ASP.NET Core 앱)를 구성하는 최소 구현에는 서버와 앱의 요청 파이프라인의 구성을 지정하는 작업이 포함됩니다.

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .Configure(app =>
    {
        app.Run(context => context.Response.WriteAsync("Hello World!"));
    })
    .Build();

host.Run();
```

* * *
호스트를 설정할 때 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) 및 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) 메서드가 제공됩니다. `Startup` 클래스가 지정된 경우 `Configure` 메서드를 정의해야 합니다. 자세한 내용은 [ASP.NET Core에서 응용 프로그램 시작](startup.md)을 참조하세요. `ConfigureServices`에 대한 여러 호출은 서로 추가합니다. `WebHostBuilder`에서 `Configure` 또는 `UseStartup`에 대한 여러 호출은 이전 설정을 대체합니다.

## <a name="host-configuration-values"></a>호스트 구성 값

[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)는 호스트 구성 값을 설정하기 위해 다음 방법을 사용합니다.

* `ASPNETCORE_{configurationKey}` 형식의 환경 변수를 포함하는 호스트 빌더 구성. 예를 들어, `ASPNETCORE_URLS`을 입력합니다.
* `CaptureStartupErrors`와 같은 명시적 메서드.
* [UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) 및 연결된 키. `UseSetting`을 사용하여 값을 설정할 때 값은 형식에 관계 없이 문자열로 설정됩니다.

호스트는 마지막에 값을 설정한 옵션을 사용합니다. 자세한 내용은 다음 섹션의 [구성 재정의](#overriding-configuration)를 참조하세요.

### <a name="capture-startup-errors"></a>시작 오류 캡처

이 설정은 시작 오류의 캡처를 제어합니다.

**키**: captureStartupErrors  
**형식**: *bool*(`true` 또는 `1`)  
**기본값**: 기본값이 `true`인 IIS 뒤에 있는 Kestrel로 앱이 실행하지 않는 한 기본값은 `false`로 지정됩니다.  
**설정 방법**: `CaptureStartupErrors`  
**환경 변수**: `ASPNETCORE_CAPTURESTARTUPERRORS`

`false`인 경우 시작 시 오류가 발생하면 호스트가 종료됩니다. `true`이면 호스트가 시작 시 예외를 캡처하고 서버 시작을 시도합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .CaptureStartupErrors(true)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .CaptureStartupErrors(true)
    ...
```

---

### <a name="content-root"></a>콘텐츠 루트

이 설정은 ASP.NET Core가 MVC 뷰와 같은 콘텐츠 파일을 검색하기 시작하는 지점을 결정합니다. 

**키**: contentRoot  
**형식**: *string*  
**기본값**: 앱 어셈블리가 있는 폴더가 기본값으로 지정됩니다.  
**설정 방법**: `UseContentRoot`  
**환경 변수**: `ASPNETCORE_CONTENTROOT`

콘텐츠 루트는 또한 [웹 루트 설정](#web-root)에 대한 기본 경로로 사용됩니다. 경로가 존재하지 않는 경우 호스트가 시작되지 않습니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseContentRoot("c:\\mywebsite")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseContentRoot("c:\\mywebsite")
    ...
```

---

### <a name="detailed-errors"></a>자세한 오류

자세한 오류를 캡처해야 하는지를 결정합니다.

**키**: detailedErrors  
**형식**: *bool*(`true` 또는 `1`)  
**기본값**: false  
**설정 방법**: `UseSetting`  
**환경 변수**: `ASPNETCORE_DETAILEDERRORS`

사용하는 경우(또는 <a href="#environment">환경</a>이 `Development`로 설정된 경우) 앱은 자세한 예외를 캡처합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

---

### <a name="environment"></a>환경

앱의 환경을 설정합니다.

**키**: environment  
**형식**: *string*  
**기본값**: Production  
**설정 방법**: `UseEnvironment`  
**환경 변수**: `ASPNETCORE_ENVIRONMENT`

환경은 어떠한 값으로도 설정할 수 있습니다. 프레임워크에서 정의된 값은 `Development`, `Staging` 및 `Production`을 포함합니다. 값은 대/소문자를 구분하지 않습니다. 기본적으로 *환경*은 `ASPNETCORE_ENVIRONMENT` 환경 변수에서 읽습니다. [Visual Studio](https://www.visualstudio.com/)를 사용하는 경우 환경 변수는 *launchSettings.json* 파일에서 설정할 수 있습니다. 자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)를 참고하시기 바랍니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseEnvironment("Development")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseEnvironment("Development")
    ...
```

---

### <a name="hosting-startup-assemblies"></a>호스팅 시작 어셈블리

앱의 호스팅 시작 어셈블리를 설정합니다.

**키**: hostingStartupAssemblies  
**형식**: *string*  
**기본값**: 빈 문자열  
**설정 방법**: `UseSetting`  
**환경 변수**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`

시작 시 로드할 호스팅 시작 어셈블리의 세미콜론으로 구분된 문자열입니다. 이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.

구성 값의 기본값이 빈 문자열이지만, 호스팅 시작 어셈블리는 항상 앱의 어셈블리를 포함합니다. 호스팅 시작 어셈블리가 제공되는 경우, 시작 시 앱이 일반적인 서비스를 빌드할 때 로드를 위해 앱의 어셈블리에 추가됩니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupAssembliesKey, "assembly1;assembly2")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.

---

### <a name="prefer-hosting-urls"></a>호스팅 URL 선호

호스트가 `IServer` 구현으로 구성된 URL 대신에 `WebHostBuilder`로 구성된 URL에서 수신 대기할지 여부를 나타냅니다.

**키**: preferHostingUrls  
**형식**: *bool*(`true` 또는 `1`)  
**기본값**: true  
**설정 방법**: `PreferHostingUrls`  
**환경 변수**: `ASPNETCORE_PREFERHOSTINGURLS`

이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .PreferHostingUrls(false)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.

---

### <a name="prevent-hosting-startup"></a>호스팅 시작 방지

앱의 어셈블리에 의해 구성된 호스팅 시작 어셈블리를 포함한 호스팅 시작 어셈블리의 자동 로딩을 방지합니다. 자세한 내용은 [플랫폼별 구성을 사용하여 앱 기능 추가](xref:host-and-deploy/platform-specific-configuration)를 참조하세요.

**키**: preventHostingStartup  
**형식**: *bool*(`true` 또는 `1`)  
**기본값**: false  
**설정 방법**: `UseSetting`  
**환경 변수**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`

이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.PreventHostingStartupKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.

---

### <a name="server-urls"></a>서버 URL

서버에서 요청을 수신해야 하는 포트와 프로토콜이 있는 IP 주소 또는 호스트 주소를 나타냅니다.

**키**: urls  
**형식**: *string*  
**기본**: http://localhost:5000  
**설정 방법**: `UseUrls`  
**환경 변수**: `ASPNETCORE_URLS`

서버가 응답해야 하는 세미콜론으로 구분된(;) URL 접두사의 목록으로 설정합니다. 예를 들어, `http://localhost:123`을 입력합니다. “\*”를 사용하여 서버가 지정된 포트 및 프로토콜을 사용하는 IP 주소 또는 호스트 이름에서 요청을 수신해야 함을 나타냅니다(예: `http://*:5000`). 프로토콜(`http://` 또는 `https://`)은 각 URL에 포함되어 있어야 합니다. 지원되는 형식은 서버마다 다릅니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

Kestrel에는 자체 엔드포인트 구성 API가 있습니다. 자세한 내용은 [ASP.NET Core의 Kestrel 웹 서버 구현](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration)을 참조하세요.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

---

### <a name="shutdown-timeout"></a>시스템 종료 제한 시간

웹 호스트가 종료될 때까지 기다리는 시간을 지정합니다.

**키**: shutdownTimeoutSeconds  
**형식**: *int*  
**기본값**: 5  
**설정 방법**: `UseShutdownTimeout`  
**환경 변수**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`

키가 `UseSetting`을 통해 *int*를 허용하더라도(예: `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`) [UseShutdownTimeout](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useshutdowntimeout) 확장 메서드는 [TimeSpan](/dotnet/api/system.timespan)을 사용합니다. 이 기능은 ASP.NET Core 2.0의 새로운 기능입니다.

시간 제한 기간 동안 호스팅:

* [IApplicationLifetime.ApplicationStopping](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstopping)을 트리거합니다.
* 중지하지 못한 서비스에 대한 모든 오류를 기록하면서 호스팅된 서비스 중지를 시도합니다.

모든 호스팅된 서비스가 중지하기 전에 시간 제한 기간이 만료되면 앱이 종료될 때 모든 활성화된 나머지 서비스가 중지됩니다. 처리를 완료하지 않은 경우에도 서비스가 중지됩니다. 서비스를 중지하는 데 시간이 더 필요한 경우 시간 제한을 늘립니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

이 기능은 ASP.NET Core 1.x에서 사용할 수 없습니다.

---

### <a name="startup-assembly"></a>시작 어셈블리

`Startup` 클래스를 검색할 어셈블리를 결정합니다.

**키**: startupAssembly  
**형식**: *string*  
**기본값**: 앱의 어셈블리  
**설정 방법**: `UseStartup`  
**환경 변수**: `ASPNETCORE_STARTUPASSEMBLY`

이름(`string`) 또는 형식(`TStartup`)별 어셈블리를 참조할 수 있습니다. `UseStartup` 메서드가 여러 개 호출된 경우 마지막 메서드가 우선 적용됩니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup("StartupAssemblyName")
    ...
```

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup<TStartup>()
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseStartup("StartupAssemblyName")
    ...
```

```csharp
var host = new WebHostBuilder()
    .UseStartup<TStartup>()
    ...
```

---

### <a name="web-root"></a>웹 루트

앱의 정적 자산에 대한 상대 경로를 설정합니다.

**키**: webroot  
**형식**: *string*  
**기본값**: 기본값이 지정되지 않은 경우 기본값은 “(Content Root)/wwwroot”입니다(경로가 존재하는 경우). 경로가 존재하지 않다면 no-op 파일 공급자가 사용됩니다.  
**설정 방법**: `UseWebRoot`  
**환경 변수**: `ASPNETCORE_WEBROOT`

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseWebRoot("public")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseWebRoot("public")
    ...
```

---

## <a name="overriding-configuration"></a>구성 재정의 중

[구성](xref:fundamentals/configuration/index)을 사용하여 호스트를 구성합니다. 다음 예제에서는 호스트 구성이 필요에 따라 *hosting.json* 파일에 지정됩니다. *hosting.json* 파일에서 로드된 모든 구성은 명령줄 인수에 의해 재정의될 수도 있습니다. 기본 제공된 구성(`config`에 있음)은 `UseConfiguration`을 통해 호스트를 구성하는 데 사용됩니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

*hosting.json*:

```json
{
    urls: "http://*:5005"
}
```

먼저 *hosting.json* 구성으로 `UseUrls`에 의해 제공되는 구성을 재정의하고, 두 번째로 명령줄 인수 구성을 재정의합니다.

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        BuildWebHost(args).Run();
    }

    public static IWebHost BuildWebHost(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hosting.json", optional: true)
            .AddCommandLine(args)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseUrls("http://*:5000")
            .UseConfiguration(config)
            .Configure(app =>
            {
                app.Run(context => 
                    context.Response.WriteAsync("Hello, World!"));
            })
            .Build();
    }
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

*hosting.json*:

```json
{
    urls: "http://*:5005"
}
```

먼저 *hosting.json* 구성으로 `UseUrls`에 의해 제공되는 구성을 재정의하고, 두 번째로 명령줄 인수 구성을 재정의합니다.

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hosting.json", optional: true)
            .AddCommandLine(args)
            .Build();

        var host = new WebHostBuilder()
            .UseUrls("http://*:5000")
            .UseConfiguration(config)
            .UseKestrel()
            .Configure(app =>
            {
                app.Run(context => 
                    context.Response.WriteAsync("Hello, World!"));
            })
            .Build();

        host.Run();
    }
}
```

---

> [!NOTE]
> [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 확장 메서드는 현재 `GetSection`에서 반환되는 구성 섹션을 구문 분석할 수 없습니다(예: `.UseConfiguration(Configuration.GetSection("section"))`). `GetSection` 메서드는 요청된 섹션에 대한 구성 키를 필터링하지만 키에 있는 섹션 이름을 그대로 둡니다(예: `section:urls`, `section:environment`). `UseConfiguration` 메서드에서는 키가 `WebHostBuilder` 키와 일치해야 합니다(예: `urls`, `environment`). 키에서 섹션 이름의 존재는 섹션 값으로 호스트를 구성할 수 없도록 합니다. 이 문제는 향후 릴리스에서 해결될 예정입니다. 자세한 내용 및 해결 방법은 [전체 키를 사용하여 WebHostBuilder.UseConfiguration에 구성 섹션을 전달](https://github.com/aspnet/Hosting/issues/839)을 참조하세요.

특정 URL에서 실행하는 호스트를 지정하려면 [dotnet run](/dotnet/core/tools/dotnet-run) 실행 시 원하는 값을 명령 프롬프트에서 전달할 수 있습니다. 명령줄 인수는 *hosting.json* 파일의 `urls` 값을 재정의하고, 서버는 포트 8080에서 수신합니다.

```console
dotnet run --urls "http://*:8080"
```

## <a name="starting-the-host"></a>호스트 시작 중

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

**실행**

`Run` 메서드는 웹앱을 시작하고 호스트가 종료될 때까지 호출 스레드를 차단합니다.

```csharp
host.Run();
```

**Start**

해당 `Start` 메서드를 호출하여 비차단 방식으로 호스트를 실행합니다.

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

URL 목록이 `Start` 메서드에 전달되면 지정된 URL에서 수신합니다.

```csharp
var urls = new List<string>()
{
    "http://*:5000",
    "http://localhost:5001"
};

var host = new WebHostBuilder()
    .UseKestrel()
    .UseStartup<Startup>()
    .Start(urls.ToArray());

using (host)
{
    Console.ReadLine();
}
```

앱은 정적 편의 메서드를 사용하여 `CreateDefaultBuilder`의 미리 구성된 기본 값을 사용하는 새 호스트를 초기화하고 시작합니다. 이러한 메서드는 콘솔 출력 없이 서버를 시작하고 [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown)으로 중단(Ctrl-C/SIGINT 또는 SIGTERM)될 때까지 대기합니다.

**Start(RequestDelegate app)**

`RequestDelegate`로 시작합니다.

```csharp
using (var host = WebHost.Start(app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

`http://localhost:5000`에 대한 브라우저에서 요청을 수행하여 “Hello World!” 응답을 수신합니다. `WaitForShutdown`은 중단(Ctrl-C/SIGINT 또는 SIGTERM)이 발생할 때까지 차단합니다. 앱은 `Console.WriteLine` 메시지를 표시하고 keypress가 종료될 때까지 대기합니다.

**Start(string url, RequestDelegate app)**

URL 및 `RequestDelegate`로 시작합니다.

```csharp
using (var host = WebHost.Start("http://localhost:8080", app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

앱이 `http://localhost:8080`에서 응답한다는 점을 제외하고 **Start(RequestDelegate app)** 와 동일한 결과가 생성됩니다.

**Start(Action<IRouteBuilder> routeBuilder)**

`IRouteBuilder`의 인스턴스([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/))를 사용하여 라우팅 미들웨어를 사용합니다.

```csharp
using (var host = WebHost.Start(router => router
    .MapGet("hello/{name}", (req, res, data) => 
        res.WriteAsync($"Hello, {data.Values["name"]}!"))
    .MapGet("buenosdias/{name}", (req, res, data) => 
        res.WriteAsync($"Buenos dias, {data.Values["name"]}!"))
    .MapGet("throw/{message?}", (req, res, data) => 
        throw new Exception((string)data.Values["message"] ?? "Uh oh!"))
    .MapGet("{greeting}/{name}", (req, res, data) => 
        res.WriteAsync($"{data.Values["greeting"]}, {data.Values["name"]}!"))
    .MapGet("", (req, res, data) => res.WriteAsync("Hello, World!"))))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

예제에서는 다음 브라우저 요청을 사용합니다.

| 요청                                    | 응답                                 |
| ------------------------------------------ | ---------------------------------------- |
| `http://localhost:5000/hello/Martin`       | Hello, Martin!                           |
| `http://localhost:5000/buenosdias/Catrina` | Buenos dias, Catrina!                    |
| `http://localhost:5000/throw/ooops!`       | “ooops!” 문자열을 사용하여 예외를 throw합니다. |
| `http://localhost:5000/throw`              | “Uh oh!” 문자열을 사용하여 예외를 throw합니다. |
| `http://localhost:5000/Sante/Kevin`        | Sante, Kevin!                            |
| `http://localhost:5000`                    | Hello World!                             |

`WaitForShutdown`은 중단(Ctrl-C/SIGINT 또는 SIGTERM)이 발생할 때까지 차단합니다. 앱은 `Console.WriteLine` 메시지를 표시하고 keypress가 종료될 때까지 대기합니다.

**Start(string url, Action<IRouteBuilder> routeBuilder)**

URL 및 `IRouteBuilder`의 인스턴스를 사용합니다.

```csharp
using (var host = WebHost.Start("http://localhost:8080", router => router
    .MapGet("hello/{name}", (req, res, data) => 
        res.WriteAsync($"Hello, {data.Values["name"]}!"))
    .MapGet("buenosdias/{name}", (req, res, data) => 
        res.WriteAsync($"Buenos dias, {data.Values["name"]}!"))
    .MapGet("throw/{message?}", (req, res, data) => 
        throw new Exception((string)data.Values["message"] ?? "Uh oh!"))
    .MapGet("{greeting}/{name}", (req, res, data) => 
        res.WriteAsync($"{data.Values["greeting"]}, {data.Values["name"]}!"))
    .MapGet("", (req, res, data) => res.WriteAsync("Hello, World!"))))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

앱이 `http://localhost:8080`에서 응답한다는 점을 제외하고 **Start(Action<IRouteBuilder> routeBuilder)** 와 동일한 결과가 생성됩니다.

**StartWith(Action<IApplicationBuilder> app)**

대리자를 제공하여 `IApplicationBuilder`를 구성합니다.

```csharp
using (var host = WebHost.StartWith(app => 
    app.Use(next => 
    {
        return async context => 
        {
            await context.Response.WriteAsync("Hello World!");
        };
    })))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

`http://localhost:5000`에 대한 브라우저에서 요청을 수행하여 “Hello World!” 응답을 수신합니다. `WaitForShutdown`은 중단(Ctrl-C/SIGINT 또는 SIGTERM)이 발생할 때까지 차단합니다. 앱은 `Console.WriteLine` 메시지를 표시하고 keypress가 종료될 때까지 대기합니다.

**StartWith(string url, Action<IApplicationBuilder> app)**

URL 및 대리자를 제공하여 `IApplicationBuilder`를 구성합니다.

```csharp
using (var host = WebHost.StartWith("http://localhost:8080", app => 
    app.Use(next => 
    {
        return async context => 
        {
            await context.Response.WriteAsync("Hello World!");
        };
    })))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

앱이 `http://localhost:8080`에서 응답한다는 점을 제외하고 **StartWith(Action<IApplicationBuilder> app)** 와 동일한 결과가 생성됩니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

**실행**

`Run` 메서드는 웹앱을 시작하고 호스트가 종료될 때까지 호출 스레드를 차단합니다.

```csharp
host.Run();
```

**Start**

해당 `Start` 메서드를 호출하여 비차단 방식으로 호스트를 실행합니다.

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

URL 목록이 `Start` 메서드에 전달되면 지정된 URL에서 수신합니다.


```csharp
var urls = new List<string>()
{
    "http://*:5000",
    "http://localhost:5001"
};

var host = new WebHostBuilder()
    .UseKestrel()
    .UseStartup<Startup>()
    .Start(urls.ToArray());

using (host)
{
    Console.ReadLine();
}
```

---

## <a name="ihostingenvironment-interface"></a>IHostingEnvironment 인터페이스

[IHostingEnvironment 인터페이스](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment)는 앱의 웹 호스팅 환경에 대한 정보를 제공합니다. 해당 속성 및 확장 메서드를 사용하기 위해 [생성자 주입](xref:fundamentals/dependency-injection)을 사용하여 `IHostingEnvironment`를 가져옵니다.

```csharp
public class CustomFileReader
{
    private readonly IHostingEnvironment _env;

    public CustomFileReader(IHostingEnvironment env)
    {
        _env = env;
    }

    public string ReadFile(string filePath)
    {
        var fileProvider = _env.WebRootFileProvider;
        // Process the file here
    }
}
```

[규칙 기반 접근 방식](xref:fundamentals/environments#startup-conventions)은 시작할 때 환경에 따라 앱을 구성하는 데 사용할 수 있습니다. 또는 `ConfigureServices`에서 사용할 수 있도록 `IHostingEnvironment`를 `Startup` 생성자에 주입합니다.

```csharp
public class Startup
{
    public Startup(IHostingEnvironment env)
    {
        HostingEnvironment = env;
    }

    public IHostingEnvironment HostingEnvironment { get; }

    public void ConfigureServices(IServiceCollection services)
    {
        if (HostingEnvironment.IsDevelopment())
        {
            // Development configuration
        }
        else
        {
            // Staging/Production configuration
        }

        var contentRootPath = HostingEnvironment.ContentRootPath;
    }
}
```

> [!NOTE]
> `IsDevelopment` 확장 메서드 외에 `IHostingEnvironment`는 `IsStaging`, `IsProduction` 및 `IsEnvironment(string environmentName)` 메서드를 제공합니다. 자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)을 참조하세요.

또한 `IHostingEnvironment` 서비스를 파이프라인 처리를 설정하기 위한 `Configure` 메서드에 직접 주입할 수 있습니다.

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        // In Development, use the developer exception page
        app.UseDeveloperExceptionPage();
    }
    else
    {
        // In Staging/Production, route exceptions to /error
        app.UseExceptionHandler("/error");
    }

    var contentRootPath = env.ContentRootPath;
}
```

사용자 지정 [미들웨어](xref:fundamentals/middleware/index#writing-middleware)를 만들 때 `IHostingEnvironment`를 `Invoke` 메서드에 주입할 수 있습니다.

```csharp
public async Task Invoke(HttpContext context, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        // Configure middleware for Development
    }
    else
    {
        // Configure middleware for Staging/Production
    }

    var contentRootPath = env.ContentRootPath;
}
```

## <a name="iapplicationlifetime-interface"></a>IApplicationLifetime 인터페이스

[IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime)은 사후 시작 및 종료 작업을 고려합니다. 인터페이스에서 세 가지 속성은 취소 토큰으로, 시작 및 종료 이벤트를 정의하는 `Action` 메서드를 등록하는 데 사용됩니다.

| 취소 토큰    | 트리거되는 경우: |
| --------------------- | --------------------- |
| `ApplicationStarted`  | 호스트가 완벽하게 시작되었습니다. |
| `ApplicationStopping` | 호스트가 정상적으로 종료되고 있습니다. 요청은 계속 처리할 수 있습니다. 종료는 이 이벤트가 완료될 때까지 차단합니다. |
| `ApplicationStopped`  | 호스트가 정상적으로 종료되었습니다. 모든 요청이 처리되어야 합니다. 종료는 이 이벤트가 완료될 때까지 차단합니다. |

```csharp
public class Startup 
{
    public void Configure(IApplicationBuilder app, IApplicationLifetime appLifetime) 
    {
        appLifetime.ApplicationStarted.Register(OnStarted);
        appLifetime.ApplicationStopping.Register(OnStopping);
        appLifetime.ApplicationStopped.Register(OnStopped);

        Console.CancelKeyPress += (sender, eventArgs) =>
        {
            appLifetime.StopApplication();
            // Don't terminate the process immediately, wait for the Main thread to exit gracefully.
            eventArgs.Cancel = true;
        };
    }

    private void OnStarted()
    {
        // Perform post-startup activities here
    }

    private void OnStopping()
    {
        // Perform on-stopping activities here
    }

    private void OnStopped()
    {
        // Perform post-stopped activities here
    }
}
```

[StopApplication](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.stopapplication)은 앱의 종료를 요청합니다. 다음 클래스에서는 `StopApplication`을 사용하여 해당 클래스의 `Shutdown` 메서드를 호출하는 경우 앱을 정상 종료합니다.

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

## <a name="scope-validation"></a>범위 유효성 검사

ASP.NET Core 2.0 이상에서 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)은 앱의 환경이 개발인 경우 [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes)를 `true`로 설정합니다.

`ValidateScopes`이 `true`로 설정된 경우 기본 서비스 공급자는 다음을 확인하기 위해 검사를 수행합니다.

* 범위가 지정된 서비스는 직접 또는 간접적으로 루트 서비스 공급자에서 해결되지 않습니다.
* 범위가 지정된 서비스는 직접 또는 간접적으로 싱글톤에 삽입되지 않습니다.

루트 서비스 공급자는 [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider)를 호출할 때 만들어집니다. 루트 서비스 공급자의 수명은 공급자가 앱으로 시작하고 앱이 종료될 때 삭제되는 경우의 앱/서버의 수명에 해당합니다.

범위가 지정된 서비스는 서비스를 만든 컨테이너에 의해 삭제됩니다. 범위가 지정된 서비스가 루트 컨테이터에서 만들어지는 경우 서비스의 수명은 효과적으로 싱글톤으로 승격됩니다. 해당 서비스는 앱/서버가 종료될 때 루트 컨테이너에 의해서만 삭제되기 때문입니다. 서비스 범위의 유효성 검사는 `BuildServiceProvider`이 호출될 경우 이러한 상황을 catch합니다.

프로덕션 환경을 포함하여 범위의 유효성을 검사하려면 호스트 작성기에서 [ServiceProviderOptions](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions)을 [UseDefaultServiceProvider](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usedefaultserviceprovider)로 구성합니다.

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseDefaultServiceProvider((context, options) => {
        options.ValidateScopes = true;
    })
```

## <a name="troubleshooting-systemargumentexception"></a>System.ArgumentException 문제 해결

**ASP.NET Core 2.0에만 적용**

호스트는 `UseStartup` 또는 `Configure`를 호출하는 대신 종속성 주입 컨테이너에 `IStartup`을 직접 주입하여 빌드할 수 있습니다.

```csharp
services.AddSingleton<IStartup, Startup>();
```

호스트가 이러한 방식으로 빌드되면 다음과 같은 오류가 발생할 수 있습니다.

```
Unhandled Exception: System.ArgumentException: A valid non-empty application name must be provided.
```

이는 `HostingStartupAttributes`를 검색하는 데 [applicationName(ApplicationKey)](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey)(현재 어셈블리)이 필요하기 때문에 발생합니다. 앱이 `IStartup`을 종속성 주입 컨테이너에 수동으로 주입하는 경우 다음 호출을 지정된 어셈블리 이름으로 `WebHostBuilder`에 추가합니다.

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("applicationName", "<Assembly Name>")
    ...
```

또는 dummy `Configure`를 `WebHostBuilder`에 추가합니다. 이는 `applicationName`(`ApplicationKey`)을 자동으로 설정합니다.

```csharp
WebHost.CreateDefaultBuilder(args)
    .Configure(_ => { })
    ...
```

**참고**: 이는 ASP.NET Core 2.0 릴리스와 `UseStartup` 또는 `Configure`를 호출하지 않는 경우에만 필요합니다.

자세한 내용은 [알림: Microsoft.Extensions.PlatformAbstractions가 제거되었습니다(주석)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) 및 [StartupInjection 샘플](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs)을 참조하세요.

## <a name="additional-resources"></a>추가 자료

* [IIS를 사용하여 Windows에서 호스트](xref:host-and-deploy/iis/index)
* [Nginx를 사용하여 Linux에서 호스트](xref:host-and-deploy/linux-nginx)
* [Apache를 사용하여 Linux에서 호스트](xref:host-and-deploy/linux-apache)
* [Windows 서비스에서 호스트](xref:host-and-deploy/windows-service)
