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
ms.openlocfilehash: 94bf356fcbfab3930804485c1b65e4a0f4c52b8e
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="detect-changes-with-change-tokens-in-aspnet-core"></a>ASP.NET Core에서는 변경 토큰으로 변경 내용을 검색합니다

[Luke Latham](https://github.com/guardrex)으로

A *토큰 변경* 는 변경 내용을 추적 하는 데 사용 하는 범용, 하위 수준 빌딩 블록입니다.

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/primitives/change-tokens/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="ichangetoken-interface"></a>IChangeToken 인터페이스

[IChangeToken](/dotnet/api/microsoft.extensions.primitives.ichangetoken) 변경 내용이 발생 하는 알림을 전파 합니다. `IChangeToken`에 [Microsoft.Extensions.Primitives](/dotnet/api/microsoft.extensions.primitives) 네임 스페이스입니다. 사용 하지 않는 앱에 대 한는 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) metapackage, 참조는 [Microsoft.Extensions.Primitives](https://www.nuget.org/packages/Microsoft.Extensions.Primitives/) 프로젝트 파일에서 NuGet 패키지 합니다.

`IChangeToken`에 두 개의 속성이 있습니다.

* [ActiveChangedCallbacks](/dotnet/api/microsoft.extensions.primitives.ichangetoken.activechangecallbacks) 토큰 사전 콜백이 발생을 나타냅니다. 경우 `ActiveChangedCallbacks` 로 설정 된 `false`, 콜백을 호출 되지 않는 및 앱 폴링해야 `HasChanged` 변경에 대 한 합니다. 또한 변경 되지 않습니다 또는 기본 변경 수신기를 삭제 하거나 사용 하지 않도록 설정 하는 경우 취소 되지 하는 토큰에 대 한도 가능 합니다.
* [HasChanged](/dotnet/api/microsoft.extensions.primitives.ichangetoken.haschanged) 변경 내용이 발생 하는 경우를 나타내는 값을 가져옵니다.

인터페이스에는 하나의 메서드 [RegisterChangeCallback (동작&lt;개체&gt;, 개체)](/dotnet/api/microsoft.extensions.primitives.ichangetoken.registerchangecallback)를 토큰 변경 될 때 호출 되는 콜백을 등록 합니다. `HasChanged`콜백이 호출 되기 전에 설정 되어야 합니다.

## <a name="changetoken-class"></a>ChangeToken 클래스

`ChangeToken`정적 클래스 변경 내용이 발생 하는 알림을 전파 하는 데 사용 됩니다. `ChangeToken`에 [Microsoft.Extensions.Primitives](/dotnet/api/microsoft.extensions.primitives) 네임 스페이스입니다. 사용 하지 않는 앱에 대 한는 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) metapackage, 참조는 [Microsoft.Extensions.Primitives](https://www.nuget.org/packages/Microsoft.Extensions.Primitives/) 프로젝트 파일에서 NuGet 패키지 합니다.

`ChangeToken` [OnChange (Func&lt;IChangeToken&gt;, 동작)](/dotnet/api/microsoft.extensions.primitives.changetoken.onchange?view=aspnetcore-2.0#Microsoft_Extensions_Primitives_ChangeToken_OnChange_System_Func_Microsoft_Extensions_Primitives_IChangeToken__System_Action_) 메서드 레지스터는 `Action` 토큰 변경 될 때마다 호출 하려면:
* `Func<IChangeToken>`토큰을 생성합니다.
* `Action`토큰 변경 될 때 호출 됩니다.

`ChangeToken`에 [OnChange&lt;TState&gt;(Func&lt;IChangeToken&gt;, 동작&lt;TState&gt;, TState)](/dotnet/api/microsoft.extensions.primitives.changetoken.onchange?view=aspnetcore-2.0#Microsoft_Extensions_Primitives_ChangeToken_OnChange__1_System_Func_Microsoft_Extensions_Primitives_IChangeToken__System_Action___0____0_) 오버 로드를 추가 `TState`토큰 소비자에 전달 되는 매개 변수 `Action`합니다.

`OnChange`반환 된 [IDisposable](/dotnet/api/system.idisposable)합니다. 호출 [Dispose](/dotnet/api/system.idisposable.dispose) 에서 추가 변경을 위해 수신 토큰을 중지 하 고 토큰의 리소스를 해제 합니다.

## <a name="example-uses-of-change-tokens-in-aspnet-core"></a>ASP.NET Core에서 변경 토큰의 사용 하 여 예제

변경 토큰 개체의 변경 내용을 모니터링 하는 ASP.NET Core의 주요 영역에 사용 됩니다.

* 파일의 변경 내용을 모니터링에 대 한 [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider)의 [조사식](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.watch) 메서드 만듭니다는 `IChangeToken` 지정 된 파일 또는 폴더를 시청 합니다.
* `IChangeToken`토큰 캐시를 변경 시 캐시 제거를 트리거하는 항목에 추가할 수 있습니다.
* 에 대 한 `TOptions` 하면 기본 변경 [OptionsMonitor](/dotnet/api/microsoft.extensions.options.optionsmonitor-1) 구현의 [IOptionsMonitor](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) 하나 이상의 허용 하는 오버 로드가 [IOptionsChangeTokenSource](/dotnet/api/microsoft.extensions.options.ioptionschangetokensource-1)인스턴스. 각 인스턴스를 반환 된 `IChangeToken` 추적 옵션 변경 내용에 대 한 변경 알림 콜백을 등록 합니다.

## <a name="monitoring-for-configuration-changes"></a>구성 변경에 대 한 모니터링

ASP.NET Core 템플릿은 기본적으로 사용 하 여 [JSON 구성 파일](xref:fundamentals/configuration/index#json-configuration) (*appsettings.json*, *appsettings 합니다. Development.json*, 및 *appsettings 합니다. Production.json*) 응용 프로그램 구성 설정을 로드 합니다.

사용 하 여 이러한 파일은 구성에서 [AddJsonFile (IConfigurationBuilder, String, Boolean, Boolean)](/dotnet/api/microsoft.extensions.configuration.jsonconfigurationextensions.addjsonfile?view=aspnetcore-2.0#Microsoft_Extensions_Configuration_JsonConfigurationExtensions_AddJsonFile_Microsoft_Extensions_Configuration_IConfigurationBuilder_System_String_System_Boolean_System_Boolean_) 확장 메서드를 [ConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.configurationbuilder) 수락 하는 `reloadOnChange` 매개 변수 (ASP.NET 코어 1.1 이상)입니다. `reloadOnChange`파일 변경 내용에 대 한 구성이 다시 로드 해야 하는 경우를 나타냅니다. 이 설정을 참조는 [WebHost](/dotnet/api/microsoft.aspnetcore.webhost) 편리 하 게 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) ([참조 소스](https://github.com/aspnet/MetaPackages/blob/rel/2.0.3/src/Microsoft.AspNetCore/WebHost.cs#L152-L193)):

```csharp
config.AddJsonFile("appsettings.json", optional: true, reloadOnChange: true)
      .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true, reloadOnChange: true);
```

파일 기반 구성을 나타내는 [FileConfigurationSource](/dotnet/api/microsoft.extensions.configuration.fileconfigurationsource)합니다. `FileConfigurationSource`사용 하 여 [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider) ([참조 소스](https://github.com/aspnet/FileSystem/blob/patch/2.0.1/src/Microsoft.Extensions.FileProviders.Abstractions/IFileProvider.cs)) 파일을 모니터링 합니다.

기본적으로는 `IFileMonitor` 에서 제공는 [PhysicalFileProvider](/dotnet/api/microsoft.extensions.fileproviders.physicalfileprovider) ([참조 소스](https://github.com/aspnet/Configuration/blob/patch/2.0.1/src/Microsoft.Extensions.Configuration.FileExtensions/FileConfigurationSource.cs#L82)), 사용 하 여 [FileSystemWatcher](/dotnet/api/system.io.filesystemwatcher) 구성 파일에 대 한 모니터링 하려면 변경합니다.

샘플 응용 프로그램 구성 변경 내용을 모니터링 하기 위한 두 가지 구현 하는 방법을 보여 줍니다. 경우는 *appsettings.json* 환경 버전의 파일 또는 파일 변경, 각 구현은 사용자 지정 코드를 실행 합니다. 샘플 응용 프로그램을 콘솔에 메시지를 씁니다.

구성 파일의 `FileSystemWatcher` 단일 구성 파일 변경에 대 한 여러 토큰 콜백을 트리거할 수 있습니다. 이 문제에 대 한 구성 파일에 파일 해시를 확인 하 여 샘플의 구현을 보호 합니다. 파일 해시를 확인 하는 중 사용자 지정 코드를 실행 하기 전에 구성 파일 중 하나 이상이 변경 되었는지 확인 합니다. 이 샘플에서는 SHA1 파일 해시를 사용 (*Utilities/Utilities.cs*):

   [!code-csharp[Main](change-tokens/sample/Utilities/Utilities.cs?name=snippet1)]

   다시 시도 하 여는 지 수 백오프으로 구현 됩니다. 다시 시도 파일 잠금을 임시로 파일 중 하나에서 새 해시를 계산 하지 못하게 하는 발생할 수 있으므로.

### <a name="simple-startup-change-token"></a>Simple 시작 변경 토큰

토큰 소비자 등록 `Action` 구성 다시 로드 토큰에 콜백에 대 한 변경 알림을 (*Startup.cs*):

[!code-csharp[Main](change-tokens/sample/Startup.cs?name=snippet2)]

`config.GetReloadToken()`토큰을 제공합니다. 콜백을 `InvokeChanged` 메서드:

[!code-csharp[Main](change-tokens/sample/Startup.cs?name=snippet3)]

`state` 콜백은 전달 하는 데에 `IHostingEnvironment`합니다. 이 올바른 결정 하는 데 유용 *appsettings* 구성 JSON 파일을 모니터링 하려면 *appsettings.&lt; 환경&gt;.json*합니다. 파일 해시는 방지 하는 데 사용 되는 `WriteConsole` 문은 구성 파일에 한 번만 변경 하는 경우 여러 개의 토큰 콜백 인해 여러 번 실행에서 합니다.

이 시스템 있으면 디버거가 실행 응용 프로그램 실행 되 고 있고 사용자가 해제할 수 없습니다.

### <a name="monitoring-configuration-changes-as-a-service"></a>서비스 구성 변경 사항 모니터링

이 샘플을 구현합니다.

* 기본 시작 토큰을 모니터링 합니다.
* 서비스를 모니터링 합니다.
* 설정 및 모니터링을 해제 하는 메커니즘입니다.

이 샘플은 설정 된 `IConfigurationMonitor` 인터페이스 (*Extensions/ConfigurationMonitor.cs*):

[!code-csharp[Main](change-tokens/sample/Extensions/ConfigurationMonitor.cs?name=snippet1)]

구현 된 클래스의 생성자 `ConfigurationMonitor`, 변경 알림에 대 한 콜백을 등록 합니다.

[!code-csharp[Main](change-tokens/sample/Extensions/ConfigurationMonitor.cs?name=snippet2)]

`config.GetReloadToken()`토큰을 제공합니다. `InvokeChanged`콜백 메서드입니다. `state` 이 인스턴스에서 모니터링 상태를 설명 하는 문자열입니다. 두 개의 속성이 사용 됩니다.

* `MonitoringEnabled`콜백은 사용자 지정 코드를 실행 해야 하는 경우 나타냅니다.
* `CurrentState`UI에서 사용 하기 위해 현재 모니터링 상태를 설명합니다.

`InvokeChanged` 한다는 점 제외 하면 이전 방식을 사용 하는 것과 비슷합니다.

* 하지 않는 한 해당 코드가 실행 되지 않으므로 `MonitoringEnabled` 은 `true`합니다.
* 설정의 `CurrentState` 코드가 실행 된 시간을 기록 하는 설명 메시지 속성 문자열입니다.
* 현재 정보 `state` 에 해당 `WriteConsole` 출력 합니다.

[!code-csharp[Main](change-tokens/sample/Extensions/ConfigurationMonitor.cs?name=snippet3)]

인스턴스 `ConfigurationMonitor` 에서 서비스로 등록 `ConfigureServices` 의 *Startup.cs*:

[!code-csharp[Main](change-tokens/sample/Startup.cs?name=snippet1)]

인덱스 페이지에서는 구성 모니터링을 통해 사용자 정의 컨트롤을 제공 합니다. 인스턴스 `IConfigurationMonitor` 에 삽입 된 `IndexModel`:

[!code-csharp[Main](change-tokens/sample/Pages/Index.cshtml.cs?name=snippet1)]

단추를 사용 하도록 설정 및 모니터링을 사용 하지 않도록 설정:

[!code-cshtml[Main](change-tokens/sample/Pages/Index.cshtml?range=35)]

[!code-csharp[Main](change-tokens/sample/Pages/Index.cshtml.cs?name=snippet2)]

때 `OnPostStartMonitoring` 은 트리거된 모니터링을 사용할 수 및 현재 상태가 지워집니다. 때 `OnPostStopMonitoring` 은 트리거된 모니터링 하지 않는 경우 및 상태 모니터링 되지 않습니다 발생 하는지 반영 하도록 설정 됩니다.

## <a name="monitoring-cached-file-changes"></a>캐시 된 파일 변경 사항 모니터링

캐시 된 메모리를 사용 하 여 파일 내용을 수 [IMemoryCache](/dotnet/api/microsoft.extensions.caching.memory.imemorycache)합니다. 에 설명 된 메모리 내 캐시는 [메모리에 캐시할](xref:performance/caching/memory) 항목입니다. 아래에 설명 된 구현 등의 추가 단계를 수행 하지 않고 *부실* (오래 된) 데이터 원본 데이터가 변경 되 면 캐시에서 반환 됩니다.

하지 고려 된 캐시 된 원본 파일의 상태를 갱신할는 [상대 만료](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryoptions.slidingexpiration) 기간에 따라 캐시 데이터를 부실 합니다. 슬라이딩 만료 기간을 갱신 하는 데이터에 대 한 각 요청 하지만 파일 캐시로 다시 로드 되지 않습니다. 파일의 캐시 된 콘텐츠를 사용 하는 모든 앱 기능을 수 있는 불완전 한 콘텐츠를 받는 영향을 받습니다.

파일 캐싱 시나리오에서에서 변경 토큰을 사용 하 여 캐시에 유효 하지 않은 파일 콘텐츠를 방지 합니다. 샘플 앱 방법의 구현을 보여 줍니다.

이 샘플에서는 사용 `GetFileContent` 에:

* 파일 콘텐츠를 반환 합니다.
* 지 수 백오프 여기서 파일 잠금을 일시적으로 때문에 파일을 읽지 못하게 하는 커버 사례에 있는 다시 시도 알고리즘을 구현 합니다.

*Utilities/Utilities.cs*:

[!code-csharp[Main](change-tokens/sample/Utilities/Utilities.cs?name=snippet2)]

A `FileService` 조회 캐시 된 파일을 처리 하기 위해 만들어집니다. `GetFileContent` 메서드 호출 서비스의 메모리 내 캐시에서 파일 콘텐츠를 가져올을 호출자에 게 반환 시도 (*Services/FileService.cs*).

캐시 된 콘텐츠 찾을 수 없으면 캐시 키를 사용 하 여 다음 작업이 수행 됩니다.

1. 파일 콘텐츠를 사용 하 여 가져온 `GetFileContent`합니다.
1. 변경 토큰을 사용 하 여 파일 공급자에서 가져온 [IFileProviders.Watch](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.watch)합니다. 토큰의 콜백 파일 수정 될 때 트리거됩니다.
1. 파일 내용을 함께 캐시를 [상대 만료](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryoptions.slidingexpiration) 기간입니다. 와 연결 된 변경 토큰이 [MemoryCacheEntryExtensions.AddExpirationToken](/dotnet/api/microsoft.extensions.caching.memory.memorycacheentryextensions.addexpirationtoken) 캐시 되어 있는 동안 파일이 변경 되 면 캐시 엔트리를 제거 하 합니다.

[!code-csharp[Main](change-tokens/sample/Services/FileService.cs?name=snippet1)]

`FileService` 서비스 캐싱 메모리와 함께 서비스 컨테이너에 등록 된 (*Startup.cs*):

[!code-csharp[Main](change-tokens/sample/Startup.cs?name=snippet4)]

서비스를 사용 하 여 파일의 콘텐츠를 로드 하는 페이지 모델 (*Pages/Index.cshtml.cs*):

[!code-csharp[Main](change-tokens/sample/Pages/Index.cshtml.cs?name=snippet3)]

## <a name="compositechangetoken-class"></a>CompositeChangeToken 클래스

하나 이상의 나타내기 위한 `IChangeToken` 인스턴스는 단일 개체에 사용 하 여는 [CompositeChangeToken](/dotnet/api/microsoft.extensions.primitives.compositechangetoken) 클래스 ([참조 소스](https://github.com/aspnet/Common/blob/patch/2.0.1/src/Microsoft.Extensions.Primitives/CompositeChangeToken.cs)).

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

`HasChanged`복합 토큰 보고서 `true` 토큰을 나타내는 모든 `HasChanged` 은 `true`합니다. `ActiveChangeCallbacks`복합 토큰 보고서 `true` 토큰을 나타내는 모든 `ActiveChangeCallbacks` 은 `true`합니다. 여러 동시 변경 이벤트가 발생할 경우 복합 변경 콜백이는 정확히 한 번 호출 됩니다.

## <a name="see-also"></a>참고 항목

* [메모리 내 캐싱](xref:performance/caching/memory)
* [분산 캐시 사용](xref:performance/caching/distributed)
* [변경 토큰을 사용하여 변경 내용 검색](xref:fundamentals/primitives/change-tokens)
* [응답 캐싱](xref:performance/caching/response)
* [응답 캐싱 미들웨어](xref:performance/caching/middleware)
* [캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [분산 캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
