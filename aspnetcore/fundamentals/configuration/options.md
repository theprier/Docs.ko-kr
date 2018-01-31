---
title: "ASP.NET Core에서 옵션 패턴"
author: guardrex
description: "ASP.NET Core 응용 프로그램에서 관련된 설정 그룹을 나타내는 옵션 패턴을 사용 하는 방법을 알아봅니다."
ms.author: riande
manager: wpickett
ms.custom: mvc
ms.date: 11/28/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/configuration/options
ms.openlocfilehash: aab96b5313a8632950e51f5586612c1d0d3d176e
ms.sourcegitcommit: 83b5a4715fd25e4eb6f7c8427c0ef03850a7fa07
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="options-pattern-in-aspnet-core"></a>ASP.NET Core에서 옵션 패턴

[Luke Latham](https://github.com/guardrex)으로

옵션 패턴은 옵션 클래스를 사용하여 관련 설정 그룹을 나타냅니다. 구성 설정은 별도 옵션 클래스에 기능에 의해 격리 됩니다, 있을 때 응용 프로그램 두 가지 중요 한 소프트웨어 엔지니어링 원칙을 따릅니다.

* [인터페이스 분리 원칙 (ISP)](http://deviq.com/interface-segregation-principle/): 구성 설정에 종속 된 기능 (클래스)만 사용 하는 구성 설정에 따라 달라 집니다.
* [문제의 분리](http://deviq.com/separation-of-concerns/): 종속 또는 서로 결합 된 응용 프로그램의 다른 부분에 대 한 설정 되지 않습니다.

[보거나 다운로드 샘플 코드](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample))이이 문서 샘플 응용 프로그램에 대 한 따라 하기 쉽습니다.

## <a name="basic-options-configuration"></a>기본 옵션 구성

기본 옵션 구성 예제로 나와 &num;1에는 [샘플 응용 프로그램](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)합니다.

옵션 클래스에 추상이 아닌 여야 합니다. 매개 변수가 없는 public 생성자를 사용 합니다. 다음 클래스 `MyOptions`, 다음 두 가지 속성이 `Option1` 및 `Option2`합니다. 기본 값을 설정 하는 것은 선택적 이지만의 기본값을 설정 하는 다음 예제에서 클래스 생성자 `Option1`합니다. `Option2`직접 속성을 초기화 하 여 설정의 기본값이 (*Models/MyOptions.cs*):

[!code-csharp[Main](options/sample/Models/MyOptions.cs?name=snippet1)]

`MyOptions` 클래스에는 서비스 컨테이너에 추가 됩니다 [IConfigureOptions&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) 구성에 바인딩됩니다.

[!code-csharp[Main](options/sample/Startup.cs?name=snippet_Example1)]

다음 페이지는 모델 [생성자 종속성 주입](xref:fundamentals/dependency-injection#what-is-dependency-injection) 와 [IOptions&lt;TOptions&gt; ](/dotnet/api/Microsoft.Extensions.Options.IOptions-1) 는 설정에 액세스 하려면 (*Pages/Index.cshtml.cs*):

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet_Example1)]

샘플의 *appsettings.json* 파일에 대 한 값을 지정 `option1` 및 `option2`:

[!code-json[Main](options/sample/appsettings.json)]

응용 프로그램을 실행할 때 페이지 모델 `OnGet` 메서드 옵션 클래스 값을 표시 하는 문자열을 반환 합니다.

```html
option1 = value1_from_json, option2 = -1
```

## <a name="configure-simple-options-with-a-delegate"></a>대리자에 간단한 옵션 구성

예제로 나와 대리자를 사용 하 여 간단한 옵션 구성 &num;에서 값 2는 [샘플 응용 프로그램](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)합니다.

대리자를 사용 하 여 옵션 값을 설정 합니다. 샘플 앱에서는 `MyOptionsWithDelegateConfig` 클래스 (*Models/MyOptionsWithDelegateConfig.cs*):

[!code-csharp[Main](options/sample/Models/MyOptionsWithDelegateConfig.cs?name=snippet1)]

다음 코드에서 두 번째 `IConfigureOptions<TOptions>` 서비스를 서비스 컨테이너에 추가 합니다. 대리자를 사용 하 여 바인딩을 구성 `MyOptionsWithDelegateConfig`:

[!code-csharp[Main](options/sample/Startup.cs?name=snippet_Example2)]

*Index.cshtml.cs*:

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?range=10)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3,9)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet_Example2)]

여러 구성 공급자를 추가할 수 있습니다. 구성 공급자는 NuGet 패키지에서 사용할 수 있습니다. 등록 하는 적용 합니다.

호출할 때마다 [구성&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1.configure) 추가 `IConfigureOptions<TOptions>` 서비스를 서비스 컨테이너입니다. 위의 예제에서는 값 `Option1` 및 `Option2` 에 지정 된 *appsettings.json*, 하지만 값의 `Option1` 및 `Option2` 구성 된 대리자에 의해 무시 됩니다.

둘 이상의 구성 서비스를 사용 하는 경우 마지막 구성 소스 지정 *wins* 구성 값을 가져오거나 설정 합니다. 응용 프로그램을 실행할 때 페이지 모델 `OnGet` 메서드 옵션 클래스 값을 표시 하는 문자열을 반환 합니다.

```html
delegate_option1 = value1_configured_by_delgate, delegate_option2 = 500
```

## <a name="suboptions-configuration"></a>하위 옵션이 구성

하위 옵션이 구성 예제로 나와 &num;3에는 [샘플 응용 프로그램](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)합니다.

앱은 앱의 특정 기능 그룹 (클래스)와 관련 된 옵션 클래스를 만들어야 합니다. 구성 값을 필요로 하는 응용 프로그램의 일부를 사용 하는 구성 값에 액세스할 수 있어야 합니다.

각 속성에 옵션의 유형 폼의 구성 키에 바인딩된 옵션을 구성을 바인딩하는 경우 `property[:sub-property:]`합니다. 예를 들어는 `MyOptions.Option1` 속성의 키에 바인딩된 `Option1`에서 읽음는 `option1` 속성 *appsettings.json*합니다.

다음 코드에서는 세 번째 `IConfigureOptions<TOptions>` 서비스를 서비스 컨테이너에 추가 합니다. 바인딩할 `MySubOptions` 섹션 `subsection` 의 *appsettings.json* 파일:

[!code-csharp[Main](options/sample/Startup.cs?name=snippet_Example3)]

`GetSection` 확장 메서드를 사용 하려면는 [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/) NuGet 패키지 합니다. 응용 프로그램을 사용 하는 경우는 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) metapackage, 패키지를 자동으로 포함 합니다.

샘플의 *appsettings.json* 파일 정의 `subsection` 멤버에 대 한 키를 가진 `suboption1` 및 `suboption2`:

[!code-json[Main](options/sample/appsettings.json?highlight=4-7)]

`MySubOptions` 클래스 속성을 정의 `SubOption1` 및 `SubOption2`하위 옵션 값을 유지 합니다 (*Models/MySubOptions.cs*):

[!code-csharp[Main](options/sample/Models/MySubOptions.cs?name=snippet1)]

페이지 모델 `OnGet` 하위 옵션 값이 포함 된 문자열을 반환 하는 메서드 (*Pages/Index.cshtml.cs*):

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?range=11)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=4,10)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet_Example3)]

앱이 실행 되는 경우는 `OnGet` 메서드 하위 옵션 클래스 값을 표시 하는 문자열을 반환 합니다.

```html
subOption1 = subvalue1_from_json, subOption2 = 200
```

## <a name="options-provided-by-a-view-model-or-with-direct-view-injection"></a>직접 보기 주입 또는 보기 모델에 의해 제공 되는 옵션

예제로 직접 보기 주입 또는 보기 모델에 의해 제공 되는 옵션에 대해서는 설명 &num;4에는 [샘플 응용 프로그램](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)합니다.

뷰 모델 또는 삽입 하 여 옵션을 제공할 수 있습니다 `IOptions<TOptions>` 보기에 직접 (*Pages/Index.cshtml.cs*):

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet_Example4)]

직접 삽입에 대 한 삽입 `IOptions<MyOptions>` 와 `@inject` 지시문:

[!code-cshtml[Main](options/sample/Pages/Index.cshtml?range=1-10&highlight=5)]

앱이 실행 되는 경우 옵션 값은 렌더링된 된 페이지에 나와 있습니다.

![옵션 값 옵션 1: value1_from_json 및 옵션 2:-1 로드 모델에서 보기에 삽입 합니다.](options/_static/view.png)

## <a name="reload-configuration-data-with-ioptionssnapshot"></a>IOptionsSnapshot 사용 하 여 구성 데이터를 다시 로드

구성 데이터를 다시 로드 `IOptionsSnapshot` 예제에 나와 &num;5는 [샘플 응용 프로그램](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)합니다.

*ASP.NET Core 1.1 이상 필요합니다.*

[IOptionsSnapshot](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1) 최소한의 처리 오버 헤드 및 옵션을 다시 로드를 지원 합니다. ASP.NET Core 1.1에서 `IOptionsSnapshot` 계획 [IOptionsMonitor&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) 트리거와 업데이트가 자동으로 때마다 모니터 데이터 원본 변경에 따라 변경 합니다. ASP.NET Core 2.0 이상 버전에서는 옵션 고 요청의 수명 동안 캐시에 액세스할 때 요청당 한 번 계산 됩니다.

다음 예제에서는 새 방법을 `IOptionsSnapshot` 후에 만들어진 *appsettings.json* 변경 (*Pages/Index.cshtml.cs*). 서버에 대 한 여러 요청에서 제공 하는 상수 값을 반환 된 *appsettings.json* 파일이 변경 되 고 구성 다시 로드 될 때까지 파일입니다.

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?range=12)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=5,11)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet_Example5)]

다음 이미지는 초기 표시 `option1` 및 `option2` 값에서 로드 된 *appsettings.json* 파일:

```html
snapshot option1 = value1_from_json, snapshot option2 = -1
```

값을 변경는 *appsettings.json* 파일을 `value1_from_json UPDATED` 및 `200`합니다. 저장 된 *appsettings.json* 파일입니다. 옵션 값이 업데이트를 확인 하려면 브라우저를 새로 고칩니다.

```html
snapshot option1 = value1_from_json UPDATED, snapshot option2 = 200
```

## <a name="named-options-support-with-iconfigurenamedoptions"></a>라는 IConfigureNamedOptions 옵션 지원

관련 옵션 지원을 라는 [IConfigureNamedOptions](/dotnet/api/microsoft.extensions.options.iconfigurenamedoptions-1) 예제로 나와 &num;에서 6는 [샘플 응용 프로그램](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)합니다.

*ASP.NET Core 2.0 이상이 필요합니다.*

*옵션 라는* 지원을 통해 응용 프로그램에서 명명 된 옵션을 구성을 구분할 수 있습니다. 샘플 응용 프로그램을 명명 된 옵션으로 선언 되는 [ConfigureNamedOptions&lt;TOptions&gt;합니다. 구성](/dotnet/api/microsoft.extensions.options.configurenamedoptions-1.configure) 메서드:

[!code-csharp[Main](options/sample/Startup.cs?name=snippet_Example6)]

샘플 앱에서 사용 하 여 명명 된 옵션에 액세스 [IOptionsSnapshot&lt;TOptions&gt;합니다. 가져오기](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1.get) (*Pages/Index.cshtml.cs*):

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?range=13-14)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=6,12-13)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet_Example6)]

샘플 응용 프로그램을 실행, 명명 된 옵션은이 반환 됩니다.

```html
named_options_1: option1 = value1_from_json, option2 = -1
named_options_2: option1 = named_options_2_value1_from_action, option2 = 5
```

`named_options_1`로드 되는, 구성에서 값을 제공 된 *appsettings.json* 파일입니다. `named_options_2`값으로 제공 됩니다.

* `named_options_2` 에 위임 `ConfigureServices` 에 대 한 `Option1`합니다.
* 에 대 한 기본값 `Option2` 에서 제공 되는 `MyOptions` 클래스입니다.

구성 된 모든 옵션을 명명 된 인스턴스는 [OptionsServiceCollectionExtensions.ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) 메서드. 다음 코드를 구성 `Option1` 명명 된 공통 값을 사용 하는 구성 인스턴스 모두에 대 한 합니다. 다음 코드에 수동으로 추가 하는 `Configure` 메서드:

```csharp
services.ConfigureAll<MyOptions>(myOptions => 
{
    myOptions.Option1 = "ConfigureAll replacement value";
});
```

샘플 응용 프로그램 코드를 추가한 후에 실행 결과 다음과 같습니다.

```html
named_options_1: option1 = ConfigureAll replacement value, option2 = -1
named_options_2: option1 = ConfigureAll replacement value, option2 = 5
```

> [!NOTE]
> ASP.NET Core 2.0 이상에서는 모든 옵션은 명명 된 인스턴스입니다. 기존 `IConfigureOption` 인스턴스 대상으로 처리 되는 `Options.DefaultName` 인스턴스에 `string.Empty`합니다. `IConfigureNamedOptions`또한 구현 `IConfigureOptions`합니다. 기본 구현은 [IOptionsFactory&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1) ([참조 소스](https://github.com/aspnet/Options/blob/release/2.0.0/src/Microsoft.Extensions.Options/OptionsFactory.cs)) 각 적절 하 게 사용 하는 논리가 있습니다. `null` 명명 된 옵션을 사용 하는 특정 명명 된 인스턴스 대신 명명 된 인스턴스는 모두 대상 ([ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) 및 [PostConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall) 이 규칙을 사용).

## <a name="ipostconfigureoptions"></a>IPostConfigureOptions

*ASP.NET Core 2.0 이상이 필요합니다.*

설정 된 postconfiguration [IPostConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1)합니다. Postconfiguration 결국 실행 [IConfigureOptions&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) 구성 발생 합니다.

```csharp
services.PostConfigure<MyOptions>(myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

[PostConfigure&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1.postconfigure) 를 사후 명명 된 옵션을 구성할 수 있습니다.

```csharp
services.PostConfigure<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

사용 하 여 [PostConfigureAll&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall) 후 모든를 구성 하 라는 구성 인스턴스:

```csharp
services.PostConfigureAll<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

## <a name="options-factory-monitoring-and-cache"></a>공장 옵션, 모니터링 및 캐시

[IOptionsMonitor](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) 알림에 사용 되는 경우 `TOptions` 인스턴스를 변경 합니다. `IOptionsMonitor`지원 reloadable 옵션, 알림, 변경 및 `IPostConfigureOptions`합니다.

[IOptionsFactory&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1) (ASP.NET 코어 2.0 이상)는 인스턴스 옵션 새로 만들기에 대해 책임이 있습니다. 에 단일 [만들기](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1.create) 메서드. 기본 구현에서는 등록 된 모든 `IConfigureOptions` 및 `IPostConfigureOptions` 모두 실행 하 고는 먼저 구성 하며, 그는 후 구성 합니다. 구별해 `IConfigureNamedOptions` 및 `IConfigureOptions` 만 적절 한 인터페이스를 호출 합니다.

[IOptionsMonitorCache&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1) (ASP.NET 코어 2.0 이상) ´ â `IOptionsMonitor` 캐시에 `TOptions` 인스턴스. `IOptionsMonitorCache` 모니터에서 인스턴스 옵션을 무효화 하는 값을 다시 계산 됩니다 ([TryRemove](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryremove)). 값 수동으로 쿼리도 [TryAdd](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryadd)합니다. [지우기](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.clear) 메서드는 필요에 따라 모든 명명 된 인스턴스를 다시 만들어야 하는 경우 사용 합니다.

## <a name="accessing-options-during-startup"></a>시작 하는 동안 액세스 옵션

`IOptions`사용할 수 있습니다 `Configure`이므로 서비스 이전에 작성 되는 `Configure` 메서드가 실행 합니다. 서비스 공급자에 기본 제공 되는 경우 `ConfigureServices` 옵션에 액세스 하려면 그가 사용할 서비스 공급자가 작성 한 후 제공 하는 구성을 옵션 합니다. 따라서 서비스 등록의 순서 지정으로 인해 일관성 없는 옵션 상태 있을 수 있습니다.

구성 옵션 구성에서 일반적으로 로드 되 면 때문에 둘 다 시작에 사용할 수 있습니다 `Configure` 및 `ConfigureServices`합니다. 구성을 시작 하는 동안 사용 하 여의 예 참조는 [응용 프로그램 시작](xref:fundamentals/startup) 항목입니다.

## <a name="see-also"></a>참고 항목

* [구성](xref:fundamentals/configuration/index)
