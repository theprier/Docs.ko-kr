---
title: "ASP.NET Core의 구성"
author: rick-anderson
description: "구성 API를 사용하여 여러 가지 방법으로 ASP.NET Core 앱을 구성합니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/11/2018
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/configuration/index
ms.openlocfilehash: c4f57d1e02ad5f4e235039999af9df9d236756a7
ms.sourcegitcommit: 3d512ea991ac36dfd4c800b7d1f8a27bfc50635e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2018
---
# <a name="configure-an-aspnet-core-app"></a>ASP.NET Core 앱 구성

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [Mark Michaelis](http://intellitect.com/author/mark-michaelis/), [Steve Smith](https://ardalis.com/), [Daniel Roth](https://github.com/danroth27), [Luke Latham](https://github.com/guardrex)

구성 API는 이름-값 쌍 목록을 기반으로 ASP.NET Core 웹앱을 구성하는 방법을 제공합니다. 구성은 여러 소스에서 런타임에 읽힙니다. 이러한 이름-값 쌍을 다중 수준 계층으로 그룹화할 수 있습니다.

다음에 대한 구성 공급자가 있습니다.

* 파일 형식(INI, JSON 및 XML)
* 명령줄 인수
* 환경 변수
* 메모리 내 .NET 개체
* 암호화된 사용자 저장소
* [Azure Key Vault](xref:security/key-vault-configuration)
* 사용자 지정 공급자(설치 또는 생성된)

각 구성 값은 문자열 키에 매핑됩니다. 설정을 사용자 지정 [POCO](https://wikipedia.org/wiki/Plain_Old_CLR_Object) 개체(속성이 있는 간단한 .NET 클래스)로 deserialize하는 바인딩 지원이 기본적으로 제공됩니다.

옵션 패턴은 옵션 클래스를 사용하여 관련 설정 그룹을 나타냅니다. 옵션 패턴 사용에 대한 자세한 내용은 [옵션](xref:fundamentals/configuration/options) 항목을 참조하세요.

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/index/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="json-configuration"></a>JSON 구성

다음 콘솔 앱은 JSON 구성 공급자를 사용합니다.

[!code-csharp[Main](index/sample/ConfigJson/Program.cs)]

앱은 다음 구성 설정을 읽고 표시합니다.

[!code-json[Main](index/sample/ConfigJson/appsettings.json)]

구성은 콜론으로 노드를 구분하는 이름-값 쌍의 계층적 목록으로 이루어집니다. 값을 검색하려면 해당 항목의 키를 사용하여 `Configuration` 인덱서에 액세스합니다.

[!code-csharp[Main](index/sample/ConfigJson/Program.cs?range=21-22)]

JSON 형식 구성 소스의 배열을 작업하려면 배열 인덱스를 콜론으로 구분된 문자열의 일부로 사용합니다. 다음 예제는 앞에서 나온 `wizards` 배열의 첫 번째 항목 이름을 가져옵니다.

```csharp
Console.Write($"{Configuration["wizards:0:Name"]}");
// Output: Gandalf
```

기본 제공 [구성](/dotnet/api/microsoft.extensions.configuration) 공급자에 기록된 이름-값 쌍은 유지되지 **않습니다**. 그러나 값을 저장하는 사용자 지정 공급자를 만들 수 있습니다. [사용자 지정 구성 공급자](xref:fundamentals/configuration/index#custom-config-providers)를 참조하세요.

이전 샘플은 구성 인덱서를 사용하여 값을 읽습니다. `Startup` 외부에서 구성에 액세스하려면 *옵션 패턴*을 사용합니다. 자세한 내용은 [옵션](xref:fundamentals/configuration/options) 항목을 참조하세요.


## <a name="configuration-by-environment"></a>환경별 구성

개발, 테스트, 프로덕션 등 환경마다 다른 구성 설정을 사용하는 것이 일반적입니다. ASP.NET Core 2.x 앱의 `CreateDefaultBuilder` 확장 메서드(또는 ASP.NET Core 1.x 앱에서 바로 `AddJsonFile` 및 `AddEnvironmentVariables` 사용)는 JSON 파일 및 시스템 구성 소스를 읽기 위한 구성 공급자를 추가합니다.

* *appsettings.json*
* *appsettings.\<EnvironmentName>.json*
* 환경 변수

ASP.NET Core 1.x 앱은 `AddJsonFile` 및 [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables#Microsoft_Extensions_Configuration_EnvironmentVariablesExtensions_AddEnvironmentVariables_Microsoft_Extensions_Configuration_IConfigurationBuilder_System_String_)를 호출해야 합니다.

매개 변수에 대한 설명은 [AddJsonFile](/dotnet/api/microsoft.extensions.configuration.jsonconfigurationextensions)을 참조하세요. `reloadOnChange`는 ASP.NET Core 1.1 이상에서만 지원됩니다.

구성 소스는 지정된 순서대로 읽힙니다. 이전 코드에서 환경 변수는 마지막에 읽힙니다. 환경을 통해 설정된 구성 값은 두 이전 공급자에서 설정된 구성 값을 대체합니다.

다음 *appsettings.Staging.json* 파일을 고려해 보세요.

[!code-json[Main](index/sample/appsettings.Staging.json)]

환경이 `Staging`으로 설정되면 다음 `Configure` 메서드가 `MyConfig` 값을 읽습니다.

[!code-csharp[Main](index/sample/StartupConfig.cs?name=snippet&highlight=3,4)]


환경은 일반적으로 `Development`, `Staging` 또는 `Production`으로 설정됩니다. 자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)을 참조하세요.

구성 고려 사항:

* `IOptionsSnapshot`은 구성 데이터가 변경되면 구성 데이터를 다시 로드할 수 있습니다. 자세한 내용은 [IOptionsSnapshot](xref:fundamentals/configuration/options#reload-configuration-data-with-ioptionssnapshot)을 참조하세요.
* 구성 키는 대/소문자를 구분하지 **않습니다**.
* 구성 공급자 코드 또는 일반 텍스트 구성 파일에 암호 또는 기타 중요한 데이터를 **절대 저장하지 마세요**. 개발 또는 테스트 환경에서 프로덕션 비밀을 사용하지 마세요. 의도치 않게 리포지토리에 커밋되는 일이 없도록 프로젝트 외부에서 비밀을 지정하세요. [여러 환경 사용](xref:fundamentals/environments) 및 [개발 중 안전한 앱 비밀 저장소](xref:security/app-secrets) 관리에 대해 자세히 알아보세요.
* 시스템의 환경 변수에서 콜론(`:`)을 사용할 수 없으면 콜론(`:`)을 이중 밑줄(`__`)로 바꾸세요.

## <a name="in-memory-provider-and-binding-to-a-poco-class"></a>메모리 내 공급자 및 POCO 클래스에 바인딩

다음 샘플은 메모리 내 공급자를 사용하고 클래스에 바인딩하는 방법을 보여 줍니다.

[!code-csharp[Main](index/sample/InMemory/Program.cs)]

구성 값이 문자열로 반환되지만, 바인딩을 통해 개체를 생성할 수 있게 됩니다. 바인딩을 사용하면 POCO 개체 또는 심지어 전체 개체 그래프를 검색할 수 있습니다.

### <a name="getvalue"></a>GetValue

다음 샘플은 [GetValue&lt;T&gt;](/dotnet/api/microsoft.extensions.configuration.configurationbinder.get?view=aspnetcore-2.0#Microsoft_Extensions_Configuration_ConfigurationBinder_Get__1_Microsoft_Extensions_Configuration_IConfiguration_) 확장 메서드를 보여줍니다.

[!code-csharp[Main](index/sample/InMemoryGetValue/Program.cs?highlight=31)]

ConfigurationBinder의 `GetValue<T>` 메서드를 사용하여 기본값을 지정할 수 있습니다(이 샘플에서는 80). `GetValue<T>`는 간단한 시나리오에 사용되며 전체 섹션에 바인딩되지 않습니다. `GetValue<T>`는 특정 형식으로 변환된 `GetSection(key).Value`에서 스칼라 값을 가져옵니다.

## <a name="bind-to-an-object-graph"></a>개체 그래프에 바인딩

클래스의 각 개체에 재귀적으로 바인딩할 수 있습니다. 다음 `AppSettings` 클래스를 살펴보세요.

[!code-csharp[Main](index/sample/ObjectGraph/AppSettings.cs)]

다음 샘플은 `AppSettings` 클래스에 바인딩합니다.

[!code-csharp[Main](index/sample/ObjectGraph/Program.cs?highlight=15-16)]

**ASP.NET Core 1.1** 이상은 전체 섹션에서 작동하는 `Get<T>`를 사용할 수 있습니다. `Get<T>`가 `Bind`을 사용하는 것보다 편리할 수 있습니다. 다음 코드는 이전 샘플에 `Get<T>`를 사용하는 방법을 보여 줍니다.

```csharp
var appConfig = config.GetSection("App").Get<AppSettings>();
```

다음 *appsettings.json* 파일 사용:

[!code-json[Main](index/sample/ObjectGraph/appsettings.json)]

프로그램에서는 `Height 11`을 표시합니다.

다음 코드를 구성 단위 테스트에 사용할 수 있습니다.

```csharp
[Fact]
public void CanBindObjectTree()
{
    var dict = new Dictionary<string, string>
        {
            {"App:Profile:Machine", "Rick"},
            {"App:Connection:Value", "connectionstring"},
            {"App:Window:Height", "11"},
            {"App:Window:Width", "11"}
        };
    var builder = new ConfigurationBuilder();
    builder.AddInMemoryCollection(dict);
    var config = builder.Build();

    var settings = new AppSettings();
    config.GetSection("App").Bind(settings);

    Assert.Equal("Rick", settings.Profile.Machine);
    Assert.Equal(11, settings.Window.Height);
    Assert.Equal(11, settings.Window.Width);
    Assert.Equal("connectionstring", settings.Connection.Value);
}
```

<a name="custom-config-providers"></a>

## <a name="create-an-entity-framework-custom-provider"></a>Entity Framework 사용자 지정 공급자 만들기

이 섹션에서는 EF를 사용하여 데이터베이스에서 이름-값 쌍을 읽는 기본 구성 공급자가 생성됩니다.

데이터베이스에 구성 값을 저장하는 `ConfigurationValue` 엔터티를 정의합니다.

[!code-csharp[Main](index/sample/CustomConfigurationProvider/ConfigurationValue.cs)]

구성된 값을 저장 및 액세스하는 `ConfigurationContext`를 추가합니다.

[!code-csharp[Main](index/sample/CustomConfigurationProvider/ConfigurationContext.cs?name=snippet1)]

[IConfigurationSource](/dotnet/api/Microsoft.Extensions.Configuration.IConfigurationSource)를 구현하는 클래스를 만듭니다.

[!code-csharp[Main](index/sample/CustomConfigurationProvider/EntityFrameworkConfigurationSource.cs?highlight=7)]

[ConfigurationProvider](/dotnet/api/Microsoft.Extensions.Configuration.ConfigurationProvider)에서 상속하여 사용자 지정 구성 공급자를 만듭니다. 구성 공급자는 비어 있는 데이터베이스를 초기화합니다.

[!code-csharp[Main](index/sample/CustomConfigurationProvider/EntityFrameworkConfigurationProvider.cs?highlight=9,18-31,38-39)]

샘플이 실행되면 데이터베이스의 강조 표시된 값("value_from_ef_1" 및 "value_from_ef_2")이 표시됩니다.

구성 소스를 추가하기 위한 `EFConfigSource` 확장 메서드를 추가할 수 있습니다.

[!code-csharp[Main](index/sample/CustomConfigurationProvider/EntityFrameworkExtensions.cs?highlight=12)]

다음 코드는 사용자 지정 `EFConfigProvider`를 사용하는 방법을 보여 줍니다.

[!code-csharp[Main](index/sample/CustomConfigurationProvider/Program.cs?highlight=21-26)]

이 샘플은 JSON 공급자 뒤에 사용자 지정 `EFConfigProvider`를 추가하므로 데이터베이스의 모든 설정이 *appsettings.json* 파일의 설정을 재정의합니다.

다음 *appsettings.json* 파일 사용:

[!code-json[Main](index/sample/CustomConfigurationProvider/appsettings.json)]

다음 출력이 표시됩니다.

```console
key1=value_from_ef_1
key2=value_from_ef_2
key3=value_from_json_3
```

## <a name="commandline-configuration-provider"></a>CommandLine 구성 공급자

[CommandLine 구성 공급자](/aspnet/core/api/microsoft.extensions.configuration.commandline.commandlineconfigurationprovider)는 런타임에 구성에 대한 명령줄 인수 키-값 쌍을 받습니다.

[CommandLine 구성 샘플 살펴보기 또는 다운로드](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/index/sample/CommandLine)

### <a name="setup-and-use-the-commandline-configuration-provider"></a>CommandLine 구성 공급자 설정 및 사용

# <a name="basic-configurationtabbasicconfiguration"></a>[기본 구성](#tab/basicconfiguration)

명령줄 구성을 활성화하려면 [ConfigurationBuilder](/api/microsoft.extensions.configuration.configurationbuilder) 인스턴스에서 `AddCommandLine` 확장 메서드를 호출합니다.

[!code-csharp[Main](index/sample_snapshot//CommandLine/Program.cs?highlight=18,21)]

코드를 실행하면 다음 출력이 표시됩니다.

```console
MachineName: MairaPC
Left: 1980
```

명령줄에서 인수 키-값 쌍을 전달하면 `Profile:MachineName` 및 `App:MainWindow:Left` 값이 변경됩니다.

```console
dotnet run Profile:MachineName=BartPC App:MainWindow:Left=1979
```

콘솔 창에 다음 항목이 표시됩니다.

```console
MachineName: BartPC
Left: 1979
```

다른 구성 공급자가 제공한 구성을 명령줄 구성으로 재정의하려면 `ConfigurationBuilder`의 마지막에서 `AddCommandLine`을 호출합니다.

[!code-csharp[Main](index/sample_snapshot//CommandLine/Program2.cs?range=11-16&highlight=1,5)]

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

일반적인 ASP.NET Core 2.x 앱은 고정적인 편의 메서드를 사용하여 `CreateDefaultBuilder`를 빌드합니다.

[!code-csharp[Main](index/sample_snapshot//Program.cs?highlight=12)]

`CreateDefaultBuilder`는 *appsettings.json*, *appsettings.{Environment}.json*, [사용자 비밀](xref:security/app-secrets)(`Development` 환경의 경우), 환경 변수 및 명령줄 인수에서 선택적 구성을 로드합니다. CommandLine 구성 공급자는 마지막에 호출됩니다. 공급자가 마지막에 호출되기 때문에 다른 구성 공급자가 이전에 설정한 구성을 런타임에 전달되는 명령줄 인수가 재정의할 수 있습니다.

*appsettings* 파일에는

* `reloadOnChange`가 활성화됩니다.
* 명령줄 인수와 *appsettings* 파일에 동일한 설정을 포함하세요.
* 일치하는 명령줄 인수가 포함된 *appsettings* 파일은 앱이 시작된 후 변경됩니다.

이전 조건이 모두 참인 경우 명령줄 인수가 무시됩니다.

ASP.NET Core 2.x 앱은 [ConfigurationBuilder](/api/microsoft.extensions.configuration.configurationbuilder)를 사용하여 수동으로 설정된 구성인 ``CreateDefaultBuilder`. When using `WebHostBuilder` 대신 WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)를 사용할 수 있습니다. 자세한 내용은 ASP.NET Core 1.x 탭을 참조하세요.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[ConfigurationBuilder](/api/microsoft.extensions.configuration.configurationbuilder)를 만들고 `AddCommandLine` 메서드를 호출하여 CommandLine 구성 공급자를 사용합니다. 공급자가 마지막에 호출되기 때문에 다른 구성 공급자가 이전에 설정한 구성을 런타임에 전달되는 명령줄 인수가 재정의할 수 있습니다. `UseConfiguration` 메서드를 사용하여 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)에 구성을 적용합니다.

[!code-csharp[Main](index/sample_snapshot//CommandLine/Program2.cs?highlight=11,15,19)]

---

### <a name="arguments"></a>인수

명령줄에 전달된 인수는 다음 표에 표시된 두 형식 중 하나를 따라야 합니다.

| 인수 형식                                                     | 예        |
| ------------------------------------------------------------------- | :------------: |
| 단일 인수: 등호로 구분되는 키-값 쌍(`=`) | `key1=value`   |
| 두 인수 시퀀스: 공백으로 구분되는 키-값 쌍    | `/key1 value1` |

**단일 인수**

값이 등호를 따라야 합니다(`=`). 값이 null일 수 있습니다(예: `mykey=`).

키에 접두사가 붙을 수 있습니다.

| 키 접두사               | 예         |
| ------------------------ | :-------------: |
| 접두사 없음                | `key1=value1`   |
| 단일 대시(`-`)&#8224; | `-key2=value2`  |
| 대시 2개(`--`)        | `--key3=value3` |
| 슬래시(`/`)      | `/key4=value4`  |

&#8224;단일 대시 접두사(`-`)가 붙은 키는 아래에 설명된 [스위치 매핑](#switch-mappings)에 제공해야 합니다.

예제 명령:

```console
dotnet run key1=value1 -key2=value2 --key3=value3 /key4=value4
```

참고: 구성 공급자에게 제공된 [스위치 매핑](#switch-mappings)에 `-key1`가 없으면 `FormatException`이 throw됩니다.

**두 인수 시퀀스**

값이 null일 수 없으며 공백으로 구분되는 키를 따라야 합니다.

키에 접두사가 있어야 합니다.

| 키 접두사               | 예         |
| ------------------------ | :-------------: |
| 단일 대시(`-`)&#8224; | `-key1 value1`  |
| 대시 2개(`--`)        | `--key2 value2` |
| 슬래시(`/`)      | `/key3 value3`  |

&#8224;단일 대시 접두사(`-`)가 붙은 키는 아래에 설명된 [스위치 매핑](#switch-mappings)에 제공해야 합니다.

예제 명령:

```console
dotnet run -key1 value1 --key2 value2 /key3 value3
```

참고: 구성 공급자에게 제공된 [스위치 매핑](#switch-mappings)에 `-key1`가 없으면 `FormatException`이 throw됩니다.

### <a name="duplicate-keys"></a>중복 키

중복 키를 제공하면 마지막 키-값 쌍이 사용됩니다.

### <a name="switch-mappings"></a>스위치 매핑

`ConfigurationBuilder`를 사용하여 수동으로 구성을 빌드하는 경우 선택적으로 `AddCommandLine` 메서드에 스위치 매핑 사전을 제공할 수 있습니다. 스위치 매핑을 통해 키 이름 교체 논리를 제공할 수 있습니다.

스위치 매핑 사전을 사용하면 명령줄 인수를 통해 제공된 키와 일치하는 키에 대해 사전을 검사합니다. 사전에서 명령줄 키가 발견되면 사전 값(키 교체)이 다시 구성으로 전달됩니다. 단일 대시(`-`) 접두사가 붙은 명령줄 키에는 스위치 매핑이 필수입니다.

스위치 매핑 사전 키 규칙:

* 스위치는 단일 대시(`-`) 또는 이중 대시(`--`)로 시작해야 합니다.
* 스위치 매핑 사전이 중복 키를 포함하면 안 됩니다.

다음 예제의 `GetSwitchMappings` 메서드는 명령줄 인수가 단일 대시(`-`) 키 접두사를 사용하고 선행 하위 키 접두사를 사용하지 않는 것을 허용합니다.

[!code-csharp[Main](index/sample/CommandLine/Program.cs?highlight=10-19,32)]

`AddInMemoryCollection`에 제공된 사전은 명령줄 인수를 제공하지 않고 구성 값을 설정합니다. 다음 명령을 사용하여 앱을 실행합니다.

```console
dotnet run
```

콘솔 창에 다음 항목이 표시됩니다.

```console
MachineName: RickPC
Left: 1980
```

다음 명령을 사용하여 구성 설정을 전달합니다.

```console
dotnet run /Profile:MachineName=DahliaPC /App:MainWindow:Left=1984
```

콘솔 창에 다음 항목이 표시됩니다.

```console
MachineName: DahliaPC
Left: 1984
```

생성된 스위치 매핑 사전은 다음 표의 데이터를 포함합니다.

| Key            | 값                 |
| -------------- | --------------------- |
| `-MachineName` | `Profile:MachineName` |
| `-Left`        | `App:MainWindow:Left` |

사전을 사용하여 키 전환을 보여 주려면 다음 명령을 실행합니다.

```console
dotnet run -MachineName=ChadPC -Left=1988
```

명령줄 키가 교환됩니다. 콘솔 창에 `Profile:MachineName` 및 `App:MainWindow:Left`의 구성 값이 표시됩니다.

```console
MachineName: ChadPC
Left: 1988
```

## <a name="the-webconfig-file"></a>web.config 파일

IIS 또는 IIS Express에서 앱을 호스트하는 경우 *web.config* 파일이 필요합니다. *web.config*의 설정은 IIS의 [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module)이 앱을 시작하고 다른 IIS 설정 및 모듈을 구성할 수 있게 합니다. *web.config* 파일이 없고 프로젝트 파일에 `<Project Sdk="Microsoft.NET.Sdk.Web">`이 포함되어 있는 경우 프로젝트를 게시하면 게시된 출력에 *web.config* 파일이 만들어집니다(*게시* 폴더). 자세한 내용은 [IIS가 있는 Windows에서 ASP.NET Core 호스팅](xref:host-and-deploy/iis/index#webconfig)을 참조하세요.

## <a name="additional-notes"></a>추가 참고 사항

* `ConfigureServices`가 호출되기 전에는 DI(종속성 주입)가 설정되지 않습니다.
* 구성 시스템에서 DI를 인식하지 못합니다.
* `IConfiguration`에는 두 가지 특수화가 있습니다.
  * `IConfigurationRoot`는 루트 노드에 사용됩니다. 다시 로드를 트리거할 수 있습니다.
  * `IConfigurationSection`은 구성 값의 섹션을 나타냅니다. `GetSection` 및 `GetChildren` 메서드는 `IConfigurationSection`을 반환합니다.
  * 구성을 다시 로드하는 경우 또는 각 공급자에 액세스해야 하는 경우 [IConfigurationRoot](/dotnet/api/microsoft.extensions.configuration.iconfigurationroot)를 사용하세요. 이러한 상황은 일반적이지 않습니다.

## <a name="additional-resources"></a>추가 리소스

* [옵션](xref:fundamentals/configuration/options)
* [여러 환경 사용](xref:fundamentals/environments)
* [개발 중 안전한 앱 비밀 저장소](xref:security/app-secrets)
* [ASP.NET Core에서 호스팅](xref:fundamentals/hosting)
* [종속성 주입](xref:fundamentals/dependency-injection)
* [Azure Key Vault 구성 공급자](xref:security/key-vault-configuration)
