---
title: .NET 일반 호스트
author: guardrex
description: 앱 시작 및 수명 관리를 담당하는 .NET의 일반 호스트에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 05/16/2018
uid: fundamentals/host/generic-host
ms.openlocfilehash: 40d297257895a4defeb89cef9c5ec6deea64a985
ms.sourcegitcommit: 7003d27b607e529642ded0400aa48ae692a0e666
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2018
ms.locfileid: "37033357"
---
# <a name="net-generic-host"></a>.NET 일반 호스트

[Luke Latham](https://github.com/guardrex)으로

.NET 앱은 *호스트*를 구성 및 실행합니다. 호스트는 앱 시작 및 수명 관리를 담당합니다. 이 항목에서는 HTTP 요청을 처리하지 않는 앱을 호스팅하는 데 유용한 ASP.NET Core 일반 호스트([HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder))를 다룹니다. 웹 호스트([WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder))에 대한 자세한 내용은 [웹 호스트](xref:fundamentals/host/web-host) 항목을 참조하세요.

일반 호스트의 목표는 웹 호스트 API에서 HTTP 파이프라인을 분리하여 호스트 시나리오의 더 광범위한 배열을 구현하는 것입니다. 일반 호스트에 기반을 둔 메시징, 백그라운드 작업 및 기타 HTTP 이외 워크로드는 구성, 종속성 주입(DI) 및 로깅과 같은 교차 편집 기능에서 이점을 얻습니다.

일반 호스트는 ASP.NET Core 2.1의 새로운 기능이며 웹 호스팅 시나리오에 적합하지 않습니다. 웹 호스팅 시나리오의 경우 [웹 호스트](xref:fundamentals/host/web-host)를 사용하세요. 일반 호스트는 향후 릴리스에서 웹 호스트를 대체하기 위해 개발 중이며, HTTP 및 HTTP 이외 시나리오에서 기본 호스트 API 역할을 합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

[Visual Studio Code](https://code.visualstudio.com/)에서 샘플 앱을 실행할 때는 *외부 또는 통합 터미널*을 사용하세요. `internalConsole`에서는 샘플을 실행하지 마세요.

Visual Studio Code에서 콘솔을 설정하려면:

1. *.vscode/launch.json* 파일을 엽니다.
1. **.NET Core 시작(콘솔)** 구성에서 **콘솔** 항목을 찾습니다. 값을 `externalTerminal` 또는 `integratedTerminal` 중 하나로 설정합니다.

## <a name="introduction"></a>소개

일반 호스트 라이브러리는 [Microsoft.Extensions.Hosting 네임스페이스](/dotnet/api/microsoft.extensions.hosting)에서 사용할 수 있으며, [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting/)에서 제공합니다. `Microsoft.Extensions.Hosting` 패키지는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)(ASP.NET Core 2.1 이상)에 포함되어 있습니다.

[IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice)는 코드 실행 진입점입니다. 각 `IHostedService` 구현은 [ConfigureServices의 서비스 등록](#configureservices) 순서대로 실행됩니다. [StartAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.startasync)는 호스트가 시작될 때 각 `IHostedService`에서 호출되고, [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.stopasync)는 호스트가 점진적으로 종료될 때 등록 순서의 역순으로 호출됩니다.

## <a name="set-up-a-host"></a>호스트 설정

[IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder)는 라이브러리 및 앱이 호스트를 초기화, 빌드 및 실행 하는 데 사용하는 주 구성 요소입니다.

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_HostBuilder)]

## <a name="host-configuration"></a>호스트 구성

[HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder)는 호스트 구성 값을 설정하기 위해 다음 방법을 사용합니다.

* 구성 작성기
* 확장 메서드 구성

### <a name="configuration-builder"></a>구성 작성기

호스트 작성기 구성은 [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) 구현에서 [ConfigureHostConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configurehostconfiguration)을 호출하여 생성됩니다. `ConfigureHostConfiguration`은 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder)를 사용하여 호스트의 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)을 만듭니다. 구성 작성기는 앱의 빌드 프로세스에서 사용할 [IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment)를 초기화합니다.

환경 변수 구성은 기본적으로 추가되지 않습니다. 호스트 빌더에서 [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables)를 호출하여 환경 변수의 호스트를 구성합니다. `AddEnvironmentVariables`는 선택적 사용자 정의 접두사를 허용합니다. 샘플 앱은 `PREFIX_` 접두사를 사용합니다. 접두사는 환경 변수를 읽을 때 제거됩니다. 샘플 앱의 호스트가 구성되면 `PREFIX_ENVIRONMENT`의 환경 변수 값이 `environment` 키에 대한 호스트 구성 값이 됩니다.

[Visual Studio](https://www.visualstudio.com/)를 사용하거나 `dotnet run`을 통해 앱을 실행할 때 개발하는 동안에 환경 변수는 *Properties/launchSettings.json* 파일에 설정될 수 있습니다. [Visual Studio Code](https://code.visualstudio.com/)에서 환경 변수는 개발하는 동안에 *.vscode/launch.json* 파일에 설정될 수 있습니다. 자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)를 참조하세요.

`ConfigureHostConfiguration` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다. 호스트는 마지막에 값을 설정한 옵션을 사용합니다.

*hostsettings.json*:

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/hostsettings.json)]

`ConfigureHostConfiguration`을 사용한 `HostBuilder` 구성 예:

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureHostConfiguration)]

> [!NOTE]
> [AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) 확장 메서드는 현재 [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection)에서 반환되는 구성 섹션을 구문 분석할 수 없습니다(예: `.AddConfiguration(Configuration.GetSection("section"))`). `GetSection` 메서드는 요청된 섹션에 대한 구성 키를 필터링하지만 키에 있는 섹션 이름을 그대로 둡니다(예: `section:environment`). `AddConfiguration` 메서드에서는 키가 `HostBuilder` 키와 일치해야 합니다(예: `environment`). 키에서 섹션 이름의 존재는 섹션 값으로 호스트를 구성할 수 없도록 합니다. 이 문제는 향후 릴리스에서 해결될 예정입니다. 자세한 내용 및 해결 방법은 [전체 키를 사용하여 WebHostBuilder.UseConfiguration에 구성 섹션을 전달](https://github.com/aspnet/Hosting/issues/839)을 참조하세요.

### <a name="extension-method-configuration"></a>확장 메서드 구성

확장 메서드는 콘텐츠 루트 및 환경을 구성하기 위해 `IHostBuilder` 구현에서 호출됩니다.

#### <a name="content-root"></a>콘텐츠 루트

이 설정은 호스트가 콘텐츠 파일을 검색하기 시작하는 지점을 결정합니다.

**키**: contentRoot  
**형식**: *string*  
**기본값**: 앱 어셈블리가 있는 폴더가 기본값으로 지정됩니다.  
**설정 방법**: `UseContentRoot`  
**환경 변수**: `<PREFIX_>CONTENTROOT`(`<PREFIX_>`는 [선택적이고 사용자 정의됨](#configuration-builder))

경로가 존재하지 않는 경우 호스트가 시작되지 않습니다.

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseContentRoot)]

#### <a name="environment"></a>환경

앱의 [환경](xref:fundamentals/environments)을 설정합니다.

**키**: environment  
**형식**: *string*  
**기본값**: Production  
**설정 방법**: `UseEnvironment`  
**환경 변수**: `<PREFIX_>ENVIRONMENT`(`<PREFIX_>`는 [선택적이고 사용자 정의됨](#configuration-builder))

환경은 어떠한 값으로도 설정할 수 있습니다. 프레임워크에서 정의된 값은 `Development`, `Staging` 및 `Production`을 포함합니다. 값은 대/소문자를 구분하지 않습니다.

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseEnvironment)]

## <a name="configureappconfiguration"></a>ConfigureAppConfiguration

앱 작성기 구성은 [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) 구현에서 [ConfigureAppConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configureappconfiguration)을 호출하여 생성됩니다. `ConfigureAppConfiguration`은 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder)를 사용하여 앱의 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)을 만듭니다. `ConfigureAppConfiguration` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다. 앱은 마지막에 값을 설정한 옵션을 사용합니다. `ConfigureAppConfiguration`을 사용하여 만든 구성은 다음 작업에 대한 [HostBuilderContext.Configuration](/dotnet/api/microsoft.extensions.hosting.hostbuildercontext.configuration)과 [Services](/dotnet/api/microsoft.extensions.hosting.ihost.services)에서 사용할 수 있습니다.

`ConfigureAppConfiguration`을 사용한 앱 구성 예:

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureAppConfiguration)]

*appsettings.json*:

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.json)]

*appsettings.Development.json*:

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.Development.json)]

*appsettings.Production.json*:

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.Production.json)]

> [!NOTE]
> [AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) 확장 메서드는 현재 [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection)에서 반환되는 구성 섹션을 구문 분석할 수 없습니다(예: `.AddConfiguration(Configuration.GetSection("section"))`). `GetSection` 메서드는 요청된 섹션에 대한 구성 키를 필터링하지만 키에 있는 섹션 이름을 그대로 둡니다(예: `section:Logging:LogLevel:Default`). `AddConfiguration` 메서드는 구성 키에 대한 정확한 일치를 예상합니다(예: `Logging:LogLevel:Default`). 키에서 섹션 이름의 존재는 섹션 값으로 앱을 구성할 수 없도록 합니다. 이 문제는 향후 릴리스에서 해결될 예정입니다. 자세한 내용 및 해결 방법은 [전체 키를 사용하여 WebHostBuilder.UseConfiguration에 구성 섹션을 전달](https://github.com/aspnet/Hosting/issues/839)을 참조하세요.

## <a name="configureservices"></a>ConfigureServices

[ConfigureServices](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configureservices)는 앱의 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에 서비스를 추가합니다. `ConfigureServices` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.

호스티드 서비스는 [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 인터페이스를 구현하는 백그라운드 작업 논리가 있는 클래스입니다. 자세한 내용은 [호스티드 서비스를 사용하는 백그라운드 작업](xref:fundamentals/host/hosted-services) 항목을 참조하세요.

[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)은 `AddHostedService` 확장 메서드를 사용하여 수명 이벤트, `LifetimeEventsHostedService` 및 시간 제한 백그라운드 작업에 대한 서비스 `TimedHostedService`를 앱에 추가합니다.

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureServices)]

## <a name="configurelogging"></a>ConfigureLogging

[ConfigureLogging](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configurelogging)은 제공된 [ILoggingBuilder](/dotnet/api/microsoft.extensions.logging.iloggingbuilder) 구성을 위한 대리자를 추가합니다. `ConfigureLogging` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureLogging)]

### <a name="useconsolelifetime"></a>UseConsoleLifetime

[UseConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.useconsolelifetime)은 `Ctrl+C`/SIGINT 또는 SIGTERM을 수신 대기하고 [StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication)을 호출하여 종료 프로세스를 시작합니다. `UseConsoleLifetime`은 [RunAsync](#runasync) 및 [WaitForShutdownAsync](#waitforshutdownasync)와 같은 확장의 차단을 해제합니다. [ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime)은 기본 수명 구현으로 미리 등록됩니다. 등록된 마지막 수명이 사용됩니다.

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseConsoleLifetime)]

## <a name="container-configuration"></a>컨테이너 구성

호스트는 다른 컨테이너 연결을 지원하기 위해 [IServiceProviderFactory](/dotnet/api/microsoft.extensions.dependencyinjection.iserviceproviderfactory-1)를 사용할 수 있습니다. 팩터리 제공은 DI 컨테이너 등록의 일부가 아니지만 구체적 DI 컨테이너를 만드는 데 사용되는 내장 호스트입니다. [UseServiceProviderFactory(IServiceProviderFactory&lt;TContainerBuilder&gt;)](/dotnet/api/microsoft.extensions.hosting.hostbuilder.useserviceproviderfactory)는 앱의 서비스 공급자를 만드는 데 사용되는 기본 팩터리를 재정의합니다.

사용자 지정 컨테이너 구성은 [ConfigureContainer](/dotnet/api/microsoft.extensions.hosting.hostbuilder.configurecontainer) 메서드로 관리됩니다. `ConfigureContainer`는 기본 호스트 API 위에 컨테이너를 구성하기 위한 강력한 형식의 환경입니다. `ConfigureContainer` 항목은 부가적 결과와 함께 여러 번 호출할 수 있습니다.

앱에 대한 서비스 컨테이너를 만듭니다.

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/ServiceContainer.cs)]

서비스 컨테이너 팩터리를 제공합니다.

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/ServiceContainerFactory.cs)]

팩터리를 사용하고 앱에 대 한 사용자 지정 서비스 컨테이너를 구성 합니다.

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ContainerConfiguration)]

## <a name="extensibility"></a>확장성

`IHostBuilder`에서 확장 메서드를 사용하여 호스트 확장성이 수행됩니다. 다음 예에서는 확장 메서드가 [RabbitMQ](https://www.rabbitmq.com/)를 사용하여 `IHostBuilder` 구현을 확장하는 방법을 보여줍니다. 확장 메서드(앱의 다른 곳)는 RabbitMQ `IHostedService`를 등록합니다.

```csharp
// UseRabbitMq is an extension method that sets up RabbitMQ to handle incoming
// messages.
var host = new HostBuilder()
    .UseRabbitMq<MyMessageHandler>()
    .Build();

await host.StartAsync();
```

## <a name="manage-the-host"></a>호스트 관리

[IHost](/dotnet/api/microsoft.extensions.hosting.ihost) 구현은 서비스 컨테이너에 등록된 `IHostedService` 구현의 시작 및 중지를 담당합니다.

### <a name="run"></a>실행

[Run](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.run)은 앱을 시작하고 호스트가 종료될 때까지 호출 스레드를 차단합니다.

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

### <a name="runasync"></a>RunAsync

[RunAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.runasync)는 앱을 실행하고 취소 토큰 또는 종료가 트리거될 때 완료되는 `Task`를 반환합니다.

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

### <a name="runconsoleasync"></a>RunConsoleAsync

[RunConsoleAsync](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.runconsoleasync)는 콘솔 지원을 구현하고, 호스트를 빌드 및 시작하며, `Ctrl+C`/SIGINT 또는 SIGTERM이 종료될 때까지 기다립니다.

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

### <a name="start-and-stopasync"></a>Start 및 StopAsync

[Start](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.start)는 호스트를 동기적으로 시작합니다.

[StopAsync(TimeSpan)](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.stopasync)는 지정된 시간 제한 내에서 호스트를 중지하려고 합니다.

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

### <a name="startasync-and-stopasync"></a>StartAsync 및 StopAsync

[StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync)는 앱을 시작합니다.

[StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync)는 앱을 중지합니다.

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

### <a name="waitforshutdown"></a>WaitForShutdown

[WaitForShutdown](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdown)은 [ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime)(`Ctrl+C`/SIGINT 또는 SIGTERM 수신 대기)과 같은 [IHostLifetime](/dotnet/api/microsoft.extensions.hosting.ihostlifetime)을 통해 트리거됩니다. `WaitForShutdown`은 [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync)를 호출합니다.

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

### <a name="waitforshutdownasync"></a>WaitForShutdownAsync

[WaitForShutdownAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdownasync)는 지정된 토큰을 통해 종료가 트리거될 때 완료되는 `Task`를 반환하고 [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync)를 호출합니다.

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

### <a name="external-control"></a>외부 제어

외부에서 호출할 수 있는 메서드를 사용하여 호스트의 외부 제어를 구현할 수 있습니다.

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

[IHostLifetime.WaitForStartAsync](/dotnet/api/microsoft.extensions.hosting.ihostlifetime.waitforstartasync)는 [StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync) 시작 시 호출되고, 완료될 때까지 기다린 후 계속합니다. 이는 외부 이벤트에서 신호를 보낼 때까지 시작을 지연시키는 데 사용할 수 있습니다.

## <a name="ihostingenvironment-interface"></a>IHostingEnvironment 인터페이스

[IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment)는 앱의 호스팅 환경에 대한 정보를 제공합니다. 해당 속성 및 확장 메서드를 사용하기 위해 [생성자 주입](xref:fundamentals/dependency-injection)을 사용하여 `IHostingEnvironment`를 가져옵니다.

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

자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)를 참조하세요.

## <a name="iapplicationlifetime-interface"></a>IApplicationLifetime 인터페이스

[IApplicationLifetime](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime)은 점진적인 종료 요청을 비롯한 사후 시작 및 종료 작업을 고려합니다. 인터페이스에서 세 가지 속성은 취소 토큰으로, 시작 및 종료 이벤트를 정의하는 `Action` 메서드를 등록하는 데 사용됩니다.

| 취소 토큰 | 트리거되는 경우: |
| ------------------ | --------------------- |
| [ApplicationStarted](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstarted) | 호스트가 완벽하게 시작되었습니다. |
| [ApplicationStopped](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopped) | 호스트가 정상적으로 종료되었습니다. 모든 요청이 처리되어야 합니다. 종료는 이 이벤트가 완료될 때까지 차단합니다. |
| [ApplicationStopping](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopping) | 호스트가 정상적으로 종료되고 있습니다. 요청은 계속 처리할 수 있습니다. 종료는 이 이벤트가 완료될 때까지 차단합니다. |

클래스에 대한 `IApplicationLifetime` 서비스 생성자 주입을 수행합니다. [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)은 `LifetimeEventsHostedService` 클래스(`IHostedService` 구현)에 대한 생성자 주입을 사용하여 이벤트를 등록합니다.

*LifetimeEventsHostedService.cs*:

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/LifetimeEventsHostedService.cs?name=snippet1)]

[StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication)은 앱의 종료를 요청합니다. 다음 클래스에서는 `StopApplication`을 사용하여 해당 클래스의 `Shutdown` 메서드를 호출하는 경우 앱을 정상 종료합니다.

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

## <a name="additional-resources"></a>추가 자료

* [호스티드 서비스를 사용하는 백그라운드 작업](xref:fundamentals/host/hosted-services)
* [GitHub의 호스팅 리포지토리 샘플](https://github.com/aspnet/Hosting/tree/release/2.1/samples)
