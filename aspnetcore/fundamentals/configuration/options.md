---
title: ASP.NET Core의 옵션 패턴
author: guardrex
description: 옵션 패턴을 사용하여 ASP.NET Core 앱에서 관련된 설정 그룹을 나타내는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 11/28/2017
uid: fundamentals/configuration/options
ms.openlocfilehash: 96d7d2956fa9bf72706cde0532ee7f4ff753b72c
ms.sourcegitcommit: 2941e24d7f3fd3d5e88d27e5f852aaedd564deda
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37126263"
---
# <a name="options-pattern-in-aspnet-core"></a>ASP.NET Core의 옵션 패턴

[Luke Latham](https://github.com/guardrex)으로

옵션 패턴은 클래스를 사용하여 관련 설정 그룹을 나타냅니다. 구성 설정이 기능에 따라 별도 클래스로 격리된 경우 앱은 두 가지 중요한 소프트웨어 엔지니어링 원칙을 따릅니다.

* [ISP(Interface Segregation Principle, 인터페이스 분리 원칙)](http://deviq.com/interface-segregation-principle/): 구성 설정에 의해 결정되는 기능(클래스)은 사용하는 구성 설정에 의해서만 결정됩니다.
* [관심사의 분리](http://deviq.com/separation-of-concerns/): 앱의 다른 부분에 대한 설정은 다른 설정에 종속되거나 연결되지 않습니다.

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)([다운로드 하는 방법](xref:tutorials/index#how-to-download-a-sample)) 이 문서는 샘플 앱으로 따라하기 더 쉽습니다.

## <a name="basic-options-configuration"></a>기본 옵션 구성

기본 옵션 구성은 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)에 예제 &num;1로 설명되어 있습니다.

옵션 클래스는 매개 변수가 없는 public 생성자를 사용하는 비추상이어야 합니다. 다음 클래스 `MyOptions`에는 `Option1` 및 `Option2`의 두 가지 속성이 있습니다. 기본 값 설정은 선택 사항이지만, 다음 예제의 클래스 생성자는 `Option1`의 기본값을 설정합니다. `Option2`에는 직접 속성을 초기화하여 설정된 기본값이 있습니다(*Models/MyOptions.cs*).

[!code-csharp[](options/sample/Models/MyOptions.cs?name=snippet1)]

`MyOptions` 클래스가 [Configure&lt;TOptions&gt;(IServiceCollection, IConfiguration)](/dotnet/api/microsoft.extensions.dependencyinjection.optionsconfigurationservicecollectionextensions.configure#Microsoft_Extensions_DependencyInjection_OptionsConfigurationServiceCollectionExtensions_Configure__1_Microsoft_Extensions_DependencyInjection_IServiceCollection_Microsoft_Extensions_Configuration_IConfiguration_)를 통해 서비스 컨테이너에 추가되고 구성에 바인딩됩니다.

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example1)]

다음 페이지 모델은 [IOptions&lt;TOptions&gt;](/dotnet/api/Microsoft.Extensions.Options.IOptions-1)를 통해 [생성자 종속성 주입](xref:fundamentals/dependency-injection#what-is-dependency-injection)을 사용하여 설정에 액세스합니다(*Pages/Index.cshtml.cs*).

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example1)]

샘플의 *appsettings.json* 파일은 `option1` 및 `option2`에 대한 값을 지정합니다.

[!code-json[](options/sample/appsettings.json?highlight=2-3)]

앱을 실행할 때 페이지 모델의 `OnGet` 메서드는 옵션 클래스 값을 표시하는 문자열을 반환합니다.

```html
option1 = value1_from_json, option2 = -1
```

> [!NOTE]
> 사용자 지정 [ConfigurationBuilder](/dotnet/api/system.configuration.configurationbuilder)를 사용하여 설정 파일에서 옵션 구성을 로드할 때 기본 경로가 정확히 설정되었는지 확인합니다.
>
> ```csharp
> var configBuilder = new ConfigurationBuilder()
>    .SetBasePath(Directory.GetCurrentDirectory())
>    .AddJsonFile("appsettings.json", optional: true);
> var config = configBuilder.Build();
>
> services.Configure<MyOptions>(config);
> ```
>
> [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)를 통해 설정 파일에서 옵션 구성을 로드할 때 명시적으로 기본 경로를 설정하는 작업은 필요하지 않습니다.

## <a name="configure-simple-options-with-a-delegate"></a>대리자로 간단한 옵션 구성

대리자를 사용한 간단한 옵션 구성은 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)에 예제 &num;2로 설명되어 있습니다.

대리자를 사용하여 옵션 값을 설정합니다. 샘플 앱에서는 `MyOptionsWithDelegateConfig` 클래스(*Models/MyOptionsWithDelegateConfig.cs*)를 사용합니다.

[!code-csharp[](options/sample/Models/MyOptionsWithDelegateConfig.cs?name=snippet1)]

다음 코드에서 두 번째 `IConfigureOptions<TOptions>` 서비스가 서비스 컨테이너에 추가됩니다. `MyOptionsWithDelegateConfig`를 통해 바인딩을 구성하는 데 대리자를 사용합니다.

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example2)]

*Index.cshtml.cs*:

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=10)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3,9)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example2)]

여러 구성 공급자를 추가할 수 있습니다. 구성 공급자는 NuGet 패키지에서 사용할 수 있습니다. 등록한 순서대로 적용됩니다.

[Configure&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1.configure)에 대한 각 호출은 `IConfigureOptions<TOptions>` 서비스를 서비스 컨테이너에 추가합니다. 위의 예제에서는 `Option1` 및 `Option2`의 값은 모두 *appsettings.json*에서 지정되지만, `Option1` 및 `Option2`의 값은 구성된 대리자에 의해 재정의됩니다.

둘 이상의 구성 서비스를 활성화한 경우 마지막 지정된 구성 소스가 *wins*를 지정했으며 구성 값을 설정합니다. 앱을 실행할 때 페이지 모델의 `OnGet` 메서드는 옵션 클래스 값을 표시하는 문자열을 반환합니다.

```html
delegate_option1 = value1_configured_by_delgate, delegate_option2 = 500
```

## <a name="suboptions-configuration"></a>하위 옵션 구성

하위 옵션 구성은 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)에 예제 &num;3으로 설명되어 있습니다.

앱은 앱의 특정 기능 그룹(클래스)과 관련된 옵션 클래스를 만들어야 합니다. 구성 값을 필요로 하는 앱의 일부는 사용하는 구성 값에 액세스할 수 있어야 합니다.

옵션을 구성에 바인딩하는 경우 옵션 형식의 각 속성은 `property[:sub-property:]` 양식의 구성 키에 바인딩됩니다. 예를 들어 `MyOptions.Option1` 속성은 키 `Option1`에 바인딩되어 *appsettings.json*의 `option1` 속성에서 읽습니다.

다음 코드에서 세 번째 `IConfigureOptions<TOptions>` 서비스가 서비스 컨테이너에 추가됩니다. 이 코드는 `MySubOptions`를 *appsettings.json* 파일의 `subsection` 섹션에 바인딩합니다.

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example3)]

`GetSection` 확장 메서드에는 [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/) NuGet 패키지가 필요합니다. 앱이 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)(ASP.NET Core 2.1 이상)를 사용하는 경우 패키지가 자동으로 포함됩니다.

샘플의 *appsettings.json* 파일은 `suboption1` 및 `suboption2`에 대한 키로 `subsection` 멤버를 정의합니다.

[!code-json[](options/sample/appsettings.json?highlight=4-7)]

`MySubOptions` 클래스는 `SubOption1` 및 `SubOption2` 속성을 정의하여 하위 옵션 값을 유지합니다(*Models/MySubOptions.cs*).

[!code-csharp[](options/sample/Models/MySubOptions.cs?name=snippet1)]

페이지 모델의 `OnGet` 메서드는 하위 옵션 값을 포함한 문자열을 반환합니다(*Pages/Index.cshtml.cs*).

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=11)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=4,10)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example3)]

앱을 실행할 때 `OnGet` 메서드는 하위 옵션 클래스 값을 표시하는 문자열을 반환합니다.

```html
subOption1 = subvalue1_from_json, subOption2 = 200
```

## <a name="options-provided-by-a-view-model-or-with-direct-view-injection"></a>직접 보기 주입 또는 보기 모델에 의해 제공되는 옵션

직접 보기 주입 또는 보기 모델에 의해 제공되는 옵션은 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)에서 예제 &num;4로 설명되어 있습니다.

옵션은 뷰 모델 또는 `IOptions<TOptions>`를 보기에 직접 주입하여 제공할 수 있습니다(*Pages/Index.cshtml.cs*).

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example4)]

직접 주입의 경우 `@inject` 지시문을 사용하여 `IOptions<MyOptions>`를 주입합니다.

[!code-cshtml[](options/sample/Pages/Index.cshtml?range=1-10&highlight=5)]

앱을 실행하는 경우 옵션 값은 렌더링된 페이지에 표시되어 있습니다.

![옵션 값 옵션 1: value1_from_json 및 옵션 2: -1은 모델에서 로드되며 보기에 주입됩니다.](options/_static/view.png)

## <a name="reload-configuration-data-with-ioptionssnapshot"></a>IOptionsSnapshot을 사용하여 구성 데이터 다시 로드

`IOptionsSnapshot`을 사용하여 구성 데이터를 다시 로드하는 것은 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)에서 예제 &num;5에 설명되어 있습니다.

*ASP.NET Core 1.1 이상이 필요합니다.*

[IOptionsSnapshot](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1)은 최소한의 처리 오버헤드로 옵션의 다시 로드를 지원합니다. ASP.NET Core 1.1에서 `IOptionsSnapshot`은 [IOptionsMonitor&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1)의 스냅샷으로, 모니터 트리거가 데이터 원본 변경에 따라 변경될 때마다 자동으로 업데이트됩니다. ASP.NET Core 2.0 이상에서 옵션은 요청의 수명 동안 액세스되고 캐시될 때 요청당 한 번 계산됩니다.

다음 예제에는 *appsettings.json*이 변경된 후 새 `IOptionsSnapshot`을 만드는 방법이 설명되어 있습니다(*Pages/Index.cshtml.cs*). 서버에 대한 여러 요청은 파일이 변경되고 구성이 다시 로드될 때까지 *appsettings.json* 파일에서 제공하는 상수 값을 반환합니다.

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=12)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=5,11)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example5)]

다음 이미지에는 *appsettings.json* 파일에서 로드된 초기 `option1` 및 `option2` 값이 나와 있습니다.

```html
snapshot option1 = value1_from_json, snapshot option2 = -1
```

*appsettings.json* 파일의 값을 `value1_from_json UPDATED` 및 `200`으로 변경합니다. *appsettings.json* 파일을 저장합니다. 옵션 값이 업데이트되었음을 확인하려면 브라우저를 새로 고칩니다.

```html
snapshot option1 = value1_from_json UPDATED, snapshot option2 = 200
```

## <a name="named-options-support-with-iconfigurenamedoptions"></a>IConfigureNamedOptions로 명명된 옵션 지원

[IConfigureNamedOptions](/dotnet/api/microsoft.extensions.options.iconfigurenamedoptions-1)로 명명된 옵션 지원은 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)에서 예제 &num;6으로 설명되어 있습니다.

*ASP.NET Core 2.0 이상이 필요합니다.*

앱은 *명명된 옵션* 지원을 통해 명명된 옵션 구성들을 구분할 수 있습니다. 샘플 앱에서 명명된 옵션은 [OptionsServiceCollectionExtensions.Configure&lt;TOptions&gt;(IServiceCollection, String, Action&lt;TOptions&gt;)](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configure)로 선언되었습니다. 그러면 확장명 메서드 [ConfigureNamedOptions&lt;TOptions&gt;.Configure](/dotnet/api/microsoft.extensions.options.configurenamedoptions-1.configure) 메서드를 호출합니다.

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example6)]

샘플 앱은 [IOptionsSnapshot&lt;TOptions&gt;.Get](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1.get)을 사용하여 명명된 옵션에 액세스합니다(*Pages/Index.cshtml.cs*).

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=13-14)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=6,12-13)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example6)]

샘플 앱을 실행하면 명명된 옵션이 반환됩니다.

```html
named_options_1: option1 = value1_from_json, option2 = -1
named_options_2: option1 = named_options_2_value1_from_action, option2 = 5
```

`named_options_1` 값은 *appsettings.json* 파일에서 로드되는 구성에서 제공됩니다. `named_options_2` 값은 다음에서 제공됩니다.

* `Option1`에 대한 `ConfigureServices`의 `named_options_2` 대리자.
* `MyOptions` 클래스에서 제공되는 `Option2`에 대한 기본값.

모든 명명된 옵션 인스턴스를 [OptionsServiceCollectionExtensions.ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) 메서드를 사용하여 구성합니다. 다음 코드는 공통 값을 사용하는 명명된 모든 구성 인스턴스에 대해 `Option1`을 구성합니다. 다음 코드를 `Configure` 메서드에 직접 추가합니다.

```csharp
services.ConfigureAll<MyOptions>(myOptions => 
{
    myOptions.Option1 = "ConfigureAll replacement value";
});
```

코드를 추가한 후 샘플 앱을 실행하면 다음과 같은 결과가 생성됩니다.

```html
named_options_1: option1 = ConfigureAll replacement value, option2 = -1
named_options_2: option1 = ConfigureAll replacement value, option2 = 5
```

> [!NOTE]
> ASP.NET Core 2.0 이상에서는 모든 옵션이 명명된 인스턴스입니다. 기존 `IConfigureOption` 인스턴스는 `Options.DefaultName` 인스턴스를 대상 지정하는 것으로 처리됩니다(즉, `string.Empty`). 또한 `IConfigureNamedOptions`는 `IConfigureOptions`를 구현합니다. [IOptionsFactory&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1)의 기본 구현([참조 소스](https://github.com/aspnet/Options/blob/release/2.0/src/Microsoft.Extensions.Options/IOptionsFactory.cs)에는 각각 적절하게 사용하기 위한 논리가 있습니다. `null` 명명된 옵션은 특정 명명된 인스턴스 대신 모든 명명된 인스턴스를 대상 지정하는 데 사용됩니다([ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) 및 [PostConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall)에서 이 규칙을 사용).

## <a name="ipostconfigureoptions"></a>IPostConfigureOptions

*ASP.NET Core 2.0 이상이 필요합니다.*

[IPostConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1)로 사후 구성을 설정합니다. 사후 구성은 [IConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) 구성이 발생한 후에 실행됩니다.

```csharp
services.PostConfigure<MyOptions>(myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

[PostConfigure&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1.postconfigure)는 명명된 옵션을 사후 구성하는 데 사용할 수 있습니다.

```csharp
services.PostConfigure<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

[PostConfigureAll&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall)를 사용하여 명명된 모든 구성 인스턴스를 사후 구성합니다.

```csharp
services.PostConfigureAll<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

## <a name="options-factory-monitoring-and-cache"></a>옵션 팩터리, 모니터링 및 캐시

[IOptionsMonitor](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1)는 `TOptions` 인스턴스가 변경될 때 알림에 사용됩니다. `IOptionsMonitor`는 다시 로드할 수 있는 옵션, 변경 알림 및 `IPostConfigureOptions`를 지원합니다.

[IOptionsFactory&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1)(ASP.NET Core 2.0 이상)는 새로운 옵션 인스턴스를 만듭니다. 단일 [Create](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1.create) 메서드가 있습니다. 기본 구현에서는 등록된 모든 `IConfigureOptions` 및 `IPostConfigureOptions`를 사용하며 먼저 구성을 모두 실행한 다음, 사후 구성을 수행합니다. `IConfigureNamedOptions`와 `IConfigureOptions`를 구별하며 적절한 인터페이스만 호출합니다.

[IOptionsMonitorCache&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1)(ASP.NET Core 2.0 이상)는 `IOptionsMonitor`에서 `TOptions` 인스턴스를 캐시하는 데 사용됩니다. `IOptionsMonitorCache`는 모니터에서 옵션 인스턴스를 무효화하므로 값이 다시 계산됩니다([TryRemove](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryremove)). 또한 [TryAdd](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryadd)로 값을 수동으로 도입할 수 있습니다. 모든 명명된 인스턴스를 필요에 따라 다시 생성해야 하는 경우 [Clear](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.clear) 메서드가 사용됩니다.

## <a name="accessing-options-during-startup"></a>시작하는 동안 옵션 액세스

서비스는 `Configure` 메서드가 실행되기 전에 빌드되므로 `IOptions`를 `Configure`에서 사용할 수 있습니다. 옵션에 액세스하기 위해 서비스 공급자가 `ConfigureServices`에서 기본 제공되는 경우 서비스 공급자가 빌드된 후 제공되는 옵션 구성을 포함하지 않습니다. 따라서 서비스 등록의 순서 지정으로 인해 일관성 없는 옵션 상태가 있을 수 있습니다.

옵션은 일반적으로 구성에서 로드되므로 구성은 `Configure` 및 `ConfigureServices` 모두에서 시작에 사용될 수 있습니다. 시작하는 동안 구성 사용에 관한 예제는 [응용 프로그램 시작](xref:fundamentals/startup) 항목을 참조하세요.

## <a name="see-also"></a>참고 항목

* [구성](xref:fundamentals/configuration/index)
