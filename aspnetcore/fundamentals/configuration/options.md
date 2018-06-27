---
title: ASP.NET Core의 옵션 패턴
author: guardrex
description: 옵션 패턴을 사용하여 ASP.NET Core 앱에서 관련된 설정 그룹을 나타내는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 11/28/2017
uid: fundamentals/configuration/options
ms.openlocfilehash: 1fe05fbc5035ffa2d01bc6be55436146f1434d17
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36278546"
---
# <a name="options-pattern-in-aspnet-core"></a><span data-ttu-id="b6a1b-103">ASP.NET Core의 옵션 패턴</span><span class="sxs-lookup"><span data-stu-id="b6a1b-103">Options pattern in ASP.NET Core</span></span>

<span data-ttu-id="b6a1b-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="b6a1b-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="b6a1b-105">옵션 패턴은 클래스를 사용하여 관련 설정 그룹을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-105">The options pattern uses classes to represent groups of related settings.</span></span> <span data-ttu-id="b6a1b-106">구성 설정이 기능에 따라 별도 클래스로 격리된 경우 앱은 두 가지 중요한 소프트웨어 엔지니어링 원칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-106">When configuration settings are isolated by feature into separate classes, the app adheres to two important software engineering principles:</span></span>

* <span data-ttu-id="b6a1b-107">[ISP(Interface Segregation Principle, 인터페이스 분리 원칙)](http://deviq.com/interface-segregation-principle/): 구성 설정에 의해 결정되는 기능(클래스)은 사용하는 구성 설정에 의해서만 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-107">The [Interface Segregation Principle (ISP)](http://deviq.com/interface-segregation-principle/): Features (classes) that depend on configuration settings depend only on the configuration settings that they use.</span></span>
* <span data-ttu-id="b6a1b-108">[관심사의 분리](http://deviq.com/separation-of-concerns/): 앱의 다른 부분에 대한 설정은 다른 설정에 종속되거나 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-108">[Separation of Concerns](http://deviq.com/separation-of-concerns/): Settings for different parts of the app aren't dependent or coupled to one another.</span></span>

<span data-ttu-id="b6a1b-109">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)([다운로드 하는 방법](xref:tutorials/index#how-to-download-a-sample)) 이 문서는 샘플 앱으로 따라하기 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)) This article is easier to follow with the sample app.</span></span>

## <a name="basic-options-configuration"></a><span data-ttu-id="b6a1b-110">기본 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="b6a1b-110">Basic options configuration</span></span>

<span data-ttu-id="b6a1b-111">기본 옵션 구성은 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)에 예제 &num;1로 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-111">Basic options configuration is demonstrated as Example &num;1 in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="b6a1b-112">옵션 클래스는 매개 변수가 없는 public 생성자를 사용하는 비추상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-112">An options class must be non-abstract with a public parameterless constructor.</span></span> <span data-ttu-id="b6a1b-113">다음 클래스 `MyOptions`에는 `Option1` 및 `Option2`의 두 가지 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-113">The following class, `MyOptions`, has two properties, `Option1` and `Option2`.</span></span> <span data-ttu-id="b6a1b-114">기본 값 설정은 선택 사항이지만, 다음 예제의 클래스 생성자는 `Option1`의 기본값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-114">Setting default values is optional, but the class constructor in the following example sets the default value of `Option1`.</span></span> <span data-ttu-id="b6a1b-115">`Option2`에는 직접 속성을 초기화하여 설정된 기본값이 있습니다(*Models/MyOptions.cs*).</span><span class="sxs-lookup"><span data-stu-id="b6a1b-115">`Option2` has a default value set by initializing the property directly (*Models/MyOptions.cs*):</span></span>

[!code-csharp[](options/sample/Models/MyOptions.cs?name=snippet1)]

<span data-ttu-id="b6a1b-116">`MyOptions` 클래스가 [Configure&lt;TOptions&gt;(IServiceCollection, IConfiguration)](/dotnet/api/microsoft.extensions.dependencyinjection.optionsconfigurationservicecollectionextensions.configure#Microsoft_Extensions_DependencyInjection_OptionsConfigurationServiceCollectionExtensions_Configure__1_Microsoft_Extensions_DependencyInjection_IServiceCollection_Microsoft_Extensions_Configuration_IConfiguration_)를 통해 서비스 컨테이너에 추가되고 구성에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-116">The `MyOptions` class is added to the service container with [Configure&lt;TOptions&gt;(IServiceCollection, IConfiguration)](/dotnet/api/microsoft.extensions.dependencyinjection.optionsconfigurationservicecollectionextensions.configure#Microsoft_Extensions_DependencyInjection_OptionsConfigurationServiceCollectionExtensions_Configure__1_Microsoft_Extensions_DependencyInjection_IServiceCollection_Microsoft_Extensions_Configuration_IConfiguration_) and bound to configuration:</span></span>

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example1)]

<span data-ttu-id="b6a1b-117">다음 페이지 모델은 [IOptions&lt;TOptions&gt;](/dotnet/api/Microsoft.Extensions.Options.IOptions-1)를 통해 [생성자 종속성 주입](xref:fundamentals/dependency-injection#what-is-dependency-injection)을 사용하여 설정에 액세스합니다(*Pages/Index.cshtml.cs*).</span><span class="sxs-lookup"><span data-stu-id="b6a1b-117">The following page model uses [constructor dependency injection](xref:fundamentals/dependency-injection#what-is-dependency-injection) with [IOptions&lt;TOptions&gt;](/dotnet/api/Microsoft.Extensions.Options.IOptions-1) to access the settings (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example1)]

<span data-ttu-id="b6a1b-118">샘플의 *appsettings.json* 파일은 `option1` 및 `option2`에 대한 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-118">The sample's *appsettings.json* file specifies values for `option1` and `option2`:</span></span>

[!code-json[](options/sample/appsettings.json?highlight=2-3)]

<span data-ttu-id="b6a1b-119">앱을 실행할 때 페이지 모델의 `OnGet` 메서드는 옵션 클래스 값을 표시하는 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-119">When the app is run, the page model's `OnGet` method returns a string showing the option class values:</span></span>

```html
option1 = value1_from_json, option2 = -1
```

## <a name="configure-simple-options-with-a-delegate"></a><span data-ttu-id="b6a1b-120">대리자로 간단한 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="b6a1b-120">Configure simple options with a delegate</span></span>

<span data-ttu-id="b6a1b-121">대리자를 사용한 간단한 옵션 구성은 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)에 예제 &num;2로 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-121">Configuring simple options with a delegate is demonstrated as Example &num;2 in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="b6a1b-122">대리자를 사용하여 옵션 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-122">Use a delegate to set options values.</span></span> <span data-ttu-id="b6a1b-123">샘플 앱에서는 `MyOptionsWithDelegateConfig` 클래스(*Models/MyOptionsWithDelegateConfig.cs*)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-123">The sample app uses the `MyOptionsWithDelegateConfig` class (*Models/MyOptionsWithDelegateConfig.cs*):</span></span>

[!code-csharp[](options/sample/Models/MyOptionsWithDelegateConfig.cs?name=snippet1)]

<span data-ttu-id="b6a1b-124">다음 코드에서 두 번째 `IConfigureOptions<TOptions>` 서비스가 서비스 컨테이너에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-124">In the following code, a second `IConfigureOptions<TOptions>` service is added to the service container.</span></span> <span data-ttu-id="b6a1b-125">`MyOptionsWithDelegateConfig`를 통해 바인딩을 구성하는 데 대리자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-125">It uses a delegate to configure the binding with `MyOptionsWithDelegateConfig`:</span></span>

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example2)]

<span data-ttu-id="b6a1b-126">*Index.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="b6a1b-126">*Index.cshtml.cs*:</span></span>

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=10)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3,9)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example2)]

<span data-ttu-id="b6a1b-127">여러 구성 공급자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-127">You can add multiple configuration providers.</span></span> <span data-ttu-id="b6a1b-128">구성 공급자는 NuGet 패키지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-128">Configuration providers are available in NuGet packages.</span></span> <span data-ttu-id="b6a1b-129">등록한 순서대로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-129">They're applied in order that they're registered.</span></span>

<span data-ttu-id="b6a1b-130">[Configure&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1.configure)에 대한 각 호출은 `IConfigureOptions<TOptions>` 서비스를 서비스 컨테이너에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-130">Each call to [Configure&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1.configure) adds an `IConfigureOptions<TOptions>` service to the service container.</span></span> <span data-ttu-id="b6a1b-131">위의 예제에서는 `Option1` 및 `Option2`의 값은 모두 *appsettings.json*에서 지정되지만, `Option1` 및 `Option2`의 값은 구성된 대리자에 의해 재정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-131">In the preceding example, the values of `Option1` and `Option2` are both specified in *appsettings.json*, but the values of `Option1` and `Option2` are overridden by the configured delegate.</span></span>

<span data-ttu-id="b6a1b-132">둘 이상의 구성 서비스를 활성화한 경우 마지막 지정된 구성 소스가 *wins*를 지정했으며 구성 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-132">When more than one configuration service is enabled, the last configuration source specified *wins* and sets the configuration value.</span></span> <span data-ttu-id="b6a1b-133">앱을 실행할 때 페이지 모델의 `OnGet` 메서드는 옵션 클래스 값을 표시하는 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-133">When the app is run, the page model's `OnGet` method returns a string showing the option class values:</span></span>

```html
delegate_option1 = value1_configured_by_delgate, delegate_option2 = 500
```

## <a name="suboptions-configuration"></a><span data-ttu-id="b6a1b-134">하위 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="b6a1b-134">Suboptions configuration</span></span>

<span data-ttu-id="b6a1b-135">하위 옵션 구성은 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)에 예제 &num;3으로 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-135">Suboptions configuration is demonstrated as Example &num;3 in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="b6a1b-136">앱은 앱의 특정 기능 그룹(클래스)과 관련된 옵션 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-136">Apps should create options classes that pertain to specific feature groups (classes) in the app.</span></span> <span data-ttu-id="b6a1b-137">구성 값을 필요로 하는 앱의 일부는 사용하는 구성 값에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-137">Parts of the app that require configuration values should only have access to the configuration values that they use.</span></span>

<span data-ttu-id="b6a1b-138">옵션을 구성에 바인딩하는 경우 옵션 형식의 각 속성은 `property[:sub-property:]` 양식의 구성 키에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-138">When binding options to configuration, each property in the options type is bound to a configuration key of the form `property[:sub-property:]`.</span></span> <span data-ttu-id="b6a1b-139">예를 들어 `MyOptions.Option1` 속성은 키 `Option1`에 바인딩되어 *appsettings.json*의 `option1` 속성에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-139">For example, the `MyOptions.Option1` property is bound to the key `Option1`, which is read from the `option1` property in *appsettings.json*.</span></span>

<span data-ttu-id="b6a1b-140">다음 코드에서 세 번째 `IConfigureOptions<TOptions>` 서비스가 서비스 컨테이너에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-140">In the following code, a third `IConfigureOptions<TOptions>` service is added to the service container.</span></span> <span data-ttu-id="b6a1b-141">이 코드는 `MySubOptions`를 *appsettings.json* 파일의 `subsection` 섹션에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-141">It binds `MySubOptions` to the section `subsection` of the *appsettings.json* file:</span></span>

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example3)]

<span data-ttu-id="b6a1b-142">`GetSection` 확장 메서드에는 [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/) NuGet 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-142">The `GetSection` extension method requires the [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/) NuGet package.</span></span> <span data-ttu-id="b6a1b-143">앱이 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)(ASP.NET Core 2.1 이상)를 사용하는 경우 패키지가 자동으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-143">If the app uses the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) (ASP.NET Core 2.1 or later), the package is automatically included.</span></span>

<span data-ttu-id="b6a1b-144">샘플의 *appsettings.json* 파일은 `suboption1` 및 `suboption2`에 대한 키로 `subsection` 멤버를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-144">The sample's *appsettings.json* file defines a `subsection` member with keys for `suboption1` and `suboption2`:</span></span>

[!code-json[](options/sample/appsettings.json?highlight=4-7)]

<span data-ttu-id="b6a1b-145">`MySubOptions` 클래스는 `SubOption1` 및 `SubOption2` 속성을 정의하여 하위 옵션 값을 유지합니다(*Models/MySubOptions.cs*).</span><span class="sxs-lookup"><span data-stu-id="b6a1b-145">The `MySubOptions` class defines properties, `SubOption1` and `SubOption2`, to hold the sub-option values (*Models/MySubOptions.cs*):</span></span>

[!code-csharp[](options/sample/Models/MySubOptions.cs?name=snippet1)]

<span data-ttu-id="b6a1b-146">페이지 모델의 `OnGet` 메서드는 하위 옵션 값을 포함한 문자열을 반환합니다(*Pages/Index.cshtml.cs*).</span><span class="sxs-lookup"><span data-stu-id="b6a1b-146">The page model's `OnGet` method returns a string with the sub-option values (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=11)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=4,10)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example3)]

<span data-ttu-id="b6a1b-147">앱을 실행할 때 `OnGet` 메서드는 하위 옵션 클래스 값을 표시하는 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-147">When the app is run, the `OnGet` method returns a string showing the sub-option class values:</span></span>

```html
subOption1 = subvalue1_from_json, subOption2 = 200
```

## <a name="options-provided-by-a-view-model-or-with-direct-view-injection"></a><span data-ttu-id="b6a1b-148">직접 보기 주입 또는 보기 모델에 의해 제공되는 옵션</span><span class="sxs-lookup"><span data-stu-id="b6a1b-148">Options provided by a view model or with direct view injection</span></span>

<span data-ttu-id="b6a1b-149">직접 보기 주입 또는 보기 모델에 의해 제공되는 옵션은 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)에서 예제 &num;4로 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-149">Options provided by a view model or with direct view injection is demonstrated as Example &num;4 in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="b6a1b-150">옵션은 뷰 모델 또는 `IOptions<TOptions>`를 보기에 직접 주입하여 제공할 수 있습니다(*Pages/Index.cshtml.cs*).</span><span class="sxs-lookup"><span data-stu-id="b6a1b-150">Options can be supplied in a view model or by injecting `IOptions<TOptions>` directly into a view (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example4)]

<span data-ttu-id="b6a1b-151">직접 주입의 경우 `@inject` 지시문을 사용하여 `IOptions<MyOptions>`를 주입합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-151">For direct injection, inject `IOptions<MyOptions>` with an `@inject` directive:</span></span>

[!code-cshtml[](options/sample/Pages/Index.cshtml?range=1-10&highlight=5)]

<span data-ttu-id="b6a1b-152">앱을 실행하는 경우 옵션 값은 렌더링된 페이지에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-152">When the app is run, the option values are shown in the rendered page:</span></span>

![옵션 값 옵션 1: value1_from_json 및 옵션 2: -1은 모델에서 로드되며 보기에 주입됩니다.](options/_static/view.png)

## <a name="reload-configuration-data-with-ioptionssnapshot"></a><span data-ttu-id="b6a1b-154">IOptionsSnapshot을 사용하여 구성 데이터 다시 로드</span><span class="sxs-lookup"><span data-stu-id="b6a1b-154">Reload configuration data with IOptionsSnapshot</span></span>

<span data-ttu-id="b6a1b-155">`IOptionsSnapshot`을 사용하여 구성 데이터를 다시 로드하는 것은 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)에서 예제 &num;5에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-155">Reloading configuration data with `IOptionsSnapshot` is demonstrated in Example &num;5 in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="b6a1b-156">*ASP.NET Core 1.1 이상이 필요합니다.*</span><span class="sxs-lookup"><span data-stu-id="b6a1b-156">*Requires ASP.NET Core 1.1 or later.*</span></span>

<span data-ttu-id="b6a1b-157">[IOptionsSnapshot](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1)은 최소한의 처리 오버헤드로 옵션의 다시 로드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-157">[IOptionsSnapshot](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1) supports reloading options with minimal processing overhead.</span></span> <span data-ttu-id="b6a1b-158">ASP.NET Core 1.1에서 `IOptionsSnapshot`은 [IOptionsMonitor&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1)의 스냅샷으로, 모니터 트리거가 데이터 원본 변경에 따라 변경될 때마다 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-158">In ASP.NET Core 1.1, `IOptionsSnapshot` is a snapshot of [IOptionsMonitor&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) and updates automatically whenever the monitor triggers changes based on the data source changing.</span></span> <span data-ttu-id="b6a1b-159">ASP.NET Core 2.0 이상에서 옵션은 요청의 수명 동안 액세스되고 캐시될 때 요청당 한 번 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-159">In ASP.NET Core 2.0 and later, options are computed once per request when accessed and cached for the lifetime of the request.</span></span>

<span data-ttu-id="b6a1b-160">다음 예제에는 *appsettings.json*이 변경된 후 새 `IOptionsSnapshot`을 만드는 방법이 설명되어 있습니다(*Pages/Index.cshtml.cs*).</span><span class="sxs-lookup"><span data-stu-id="b6a1b-160">The following example demonstrates how a new `IOptionsSnapshot` is created after *appsettings.json* changes (*Pages/Index.cshtml.cs*).</span></span> <span data-ttu-id="b6a1b-161">서버에 대한 여러 요청은 파일이 변경되고 구성이 다시 로드될 때까지 *appsettings.json* 파일에서 제공하는 상수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-161">Multiple requests to the server return constant values provided by the *appsettings.json* file until the file is changed and configuration reloads.</span></span>

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=12)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=5,11)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example5)]

<span data-ttu-id="b6a1b-162">다음 이미지에는 *appsettings.json* 파일에서 로드된 초기 `option1` 및 `option2` 값이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-162">The following image shows the initial `option1` and `option2` values loaded from the *appsettings.json* file:</span></span>

```html
snapshot option1 = value1_from_json, snapshot option2 = -1
```

<span data-ttu-id="b6a1b-163">*appsettings.json* 파일의 값을 `value1_from_json UPDATED` 및 `200`으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-163">Change the values in the *appsettings.json* file to `value1_from_json UPDATED` and `200`.</span></span> <span data-ttu-id="b6a1b-164">*appsettings.json* 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-164">Save the *appsettings.json* file.</span></span> <span data-ttu-id="b6a1b-165">옵션 값이 업데이트되었음을 확인하려면 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-165">Refresh the browser to see that the options values are updated:</span></span>

```html
snapshot option1 = value1_from_json UPDATED, snapshot option2 = 200
```

## <a name="named-options-support-with-iconfigurenamedoptions"></a><span data-ttu-id="b6a1b-166">IConfigureNamedOptions로 명명된 옵션 지원</span><span class="sxs-lookup"><span data-stu-id="b6a1b-166">Named options support with IConfigureNamedOptions</span></span>

<span data-ttu-id="b6a1b-167">[IConfigureNamedOptions](/dotnet/api/microsoft.extensions.options.iconfigurenamedoptions-1)로 명명된 옵션 지원은 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)에서 예제 &num;6으로 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-167">Named options support with [IConfigureNamedOptions](/dotnet/api/microsoft.extensions.options.iconfigurenamedoptions-1) is demonstrated as Example &num;6 in the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="b6a1b-168">*ASP.NET Core 2.0 이상이 필요합니다.*</span><span class="sxs-lookup"><span data-stu-id="b6a1b-168">*Requires ASP.NET Core 2.0 or later.*</span></span>

<span data-ttu-id="b6a1b-169">앱은 *명명된 옵션* 지원을 통해 명명된 옵션 구성들을 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-169">*Named options* support allows the app to distinguish between named options configurations.</span></span> <span data-ttu-id="b6a1b-170">샘플 앱에서 명명된 옵션은 [OptionsServiceCollectionExtensions.Configure&lt;TOptions&gt;(IServiceCollection, String, Action&lt;TOptions&gt;)](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configure)로 선언되었습니다. 그러면 확장명 메서드 [ConfigureNamedOptions&lt;TOptions&gt;.Configure](/dotnet/api/microsoft.extensions.options.configurenamedoptions-1.configure) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-170">In the sample app, named options are declared with the [OptionsServiceCollectionExtensions.Configure&lt;TOptions&gt;(IServiceCollection, String, Action&lt;TOptions&gt;)](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configure) which in turn calls the extension method [ConfigureNamedOptions&lt;TOptions&gt;.Configure](/dotnet/api/microsoft.extensions.options.configurenamedoptions-1.configure) method:</span></span>

[!code-csharp[](options/sample/Startup.cs?name=snippet_Example6)]

<span data-ttu-id="b6a1b-171">샘플 앱은 [IOptionsSnapshot&lt;TOptions&gt;.Get](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1.get)을 사용하여 명명된 옵션에 액세스합니다(*Pages/Index.cshtml.cs*).</span><span class="sxs-lookup"><span data-stu-id="b6a1b-171">The sample app accesses the named options with [IOptionsSnapshot&lt;TOptions&gt;.Get](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1.get) (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?range=13-14)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=6,12-13)]

[!code-csharp[](options/sample/Pages/Index.cshtml.cs?name=snippet_Example6)]

<span data-ttu-id="b6a1b-172">샘플 앱을 실행하면 명명된 옵션이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-172">Running the sample app, the named options are returned:</span></span>

```html
named_options_1: option1 = value1_from_json, option2 = -1
named_options_2: option1 = named_options_2_value1_from_action, option2 = 5
```

<span data-ttu-id="b6a1b-173">`named_options_1` 값은 *appsettings.json* 파일에서 로드되는 구성에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-173">`named_options_1` values are provided from configuration, which are loaded from the *appsettings.json* file.</span></span> <span data-ttu-id="b6a1b-174">`named_options_2` 값은 다음에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-174">`named_options_2` values are provided by:</span></span>

* <span data-ttu-id="b6a1b-175">`Option1`에 대한 `ConfigureServices`의 `named_options_2` 대리자.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-175">The `named_options_2` delegate in `ConfigureServices` for `Option1`.</span></span>
* <span data-ttu-id="b6a1b-176">`MyOptions` 클래스에서 제공되는 `Option2`에 대한 기본값.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-176">The default value for `Option2` provided by the `MyOptions` class.</span></span>

<span data-ttu-id="b6a1b-177">모든 명명된 옵션 인스턴스를 [OptionsServiceCollectionExtensions.ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) 메서드를 사용하여 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-177">Configure all named options instances with the [OptionsServiceCollectionExtensions.ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) method.</span></span> <span data-ttu-id="b6a1b-178">다음 코드는 공통 값을 사용하는 명명된 모든 구성 인스턴스에 대해 `Option1`을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-178">The following code configures `Option1` for all named configuration instances with a common value.</span></span> <span data-ttu-id="b6a1b-179">다음 코드를 `Configure` 메서드에 직접 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-179">Add the following code manually to the `Configure` method:</span></span>

```csharp
services.ConfigureAll<MyOptions>(myOptions => 
{
    myOptions.Option1 = "ConfigureAll replacement value";
});
```

<span data-ttu-id="b6a1b-180">코드를 추가한 후 샘플 앱을 실행하면 다음과 같은 결과가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-180">Running the sample app after adding the code produces the following result:</span></span>

```html
named_options_1: option1 = ConfigureAll replacement value, option2 = -1
named_options_2: option1 = ConfigureAll replacement value, option2 = 5
```

> [!NOTE]
> <span data-ttu-id="b6a1b-181">ASP.NET Core 2.0 이상에서는 모든 옵션이 명명된 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-181">In ASP.NET Core 2.0 and later, all options are named instances.</span></span> <span data-ttu-id="b6a1b-182">기존 `IConfigureOption` 인스턴스는 `Options.DefaultName` 인스턴스를 대상 지정하는 것으로 처리됩니다(즉, `string.Empty`).</span><span class="sxs-lookup"><span data-stu-id="b6a1b-182">Existing `IConfigureOption` instances are treated as targeting the `Options.DefaultName` instance, which is `string.Empty`.</span></span> <span data-ttu-id="b6a1b-183">또한 `IConfigureNamedOptions`는 `IConfigureOptions`를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-183">`IConfigureNamedOptions` also implements `IConfigureOptions`.</span></span> <span data-ttu-id="b6a1b-184">[IOptionsFactory&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1)의 기본 구현([참조 소스](https://github.com/aspnet/Options/blob/release/2.0/src/Microsoft.Extensions.Options/IOptionsFactory.cs)에는 각각 적절하게 사용하기 위한 논리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-184">The default implementation of the [IOptionsFactory&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1) ([reference source](https://github.com/aspnet/Options/blob/release/2.0/src/Microsoft.Extensions.Options/IOptionsFactory.cs) has logic to use each appropriately.</span></span> <span data-ttu-id="b6a1b-185">`null` 명명된 옵션은 특정 명명된 인스턴스 대신 모든 명명된 인스턴스를 대상 지정하는 데 사용됩니다([ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) 및 [PostConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall)에서 이 규칙을 사용).</span><span class="sxs-lookup"><span data-stu-id="b6a1b-185">The `null` named option is used to target all of the named instances instead of a specific named instance ([ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) and [PostConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall) use this convention).</span></span>

## <a name="ipostconfigureoptions"></a><span data-ttu-id="b6a1b-186">IPostConfigureOptions</span><span class="sxs-lookup"><span data-stu-id="b6a1b-186">IPostConfigureOptions</span></span>

<span data-ttu-id="b6a1b-187">*ASP.NET Core 2.0 이상이 필요합니다.*</span><span class="sxs-lookup"><span data-stu-id="b6a1b-187">*Requires ASP.NET Core 2.0 or later.*</span></span>

<span data-ttu-id="b6a1b-188">[IPostConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1)로 사후 구성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-188">Set postconfiguration with [IPostConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1).</span></span> <span data-ttu-id="b6a1b-189">사후 구성은 [IConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) 구성이 발생한 후에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-189">Postconfiguration runs after all [IConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) configuration occurs:</span></span>

```csharp
services.PostConfigure<MyOptions>(myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

<span data-ttu-id="b6a1b-190">[PostConfigure&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1.postconfigure)는 명명된 옵션을 사후 구성하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-190">[PostConfigure&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1.postconfigure) is available to post-configure named options:</span></span>

```csharp
services.PostConfigure<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

<span data-ttu-id="b6a1b-191">[PostConfigureAll&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall)를 사용하여 명명된 모든 구성 인스턴스를 사후 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-191">Use [PostConfigureAll&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall) to post-configure all named configuration instances:</span></span>

```csharp
services.PostConfigureAll<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

## <a name="options-factory-monitoring-and-cache"></a><span data-ttu-id="b6a1b-192">옵션 팩터리, 모니터링 및 캐시</span><span class="sxs-lookup"><span data-stu-id="b6a1b-192">Options factory, monitoring, and cache</span></span>

<span data-ttu-id="b6a1b-193">[IOptionsMonitor](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1)는 `TOptions` 인스턴스가 변경될 때 알림에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-193">[IOptionsMonitor](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) is used for notifications when `TOptions` instances change.</span></span> <span data-ttu-id="b6a1b-194">`IOptionsMonitor`는 다시 로드할 수 있는 옵션, 변경 알림 및 `IPostConfigureOptions`를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-194">`IOptionsMonitor` supports reloadable options, change notifications, and `IPostConfigureOptions`.</span></span>

<span data-ttu-id="b6a1b-195">[IOptionsFactory&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1)(ASP.NET Core 2.0 이상)는 새로운 옵션 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-195">[IOptionsFactory&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1) (ASP.NET Core 2.0 or later) is responsible for creating new options instances.</span></span> <span data-ttu-id="b6a1b-196">단일 [Create](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1.create) 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-196">It has a single [Create](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1.create) method.</span></span> <span data-ttu-id="b6a1b-197">기본 구현에서는 등록된 모든 `IConfigureOptions` 및 `IPostConfigureOptions`를 사용하며 먼저 구성을 모두 실행한 다음, 사후 구성을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-197">The default implementation takes all registered `IConfigureOptions` and `IPostConfigureOptions` and runs all the configures first, followed by the post-configures.</span></span> <span data-ttu-id="b6a1b-198">`IConfigureNamedOptions`와 `IConfigureOptions`를 구별하며 적절한 인터페이스만 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-198">It distinguishes between `IConfigureNamedOptions` and `IConfigureOptions` and only calls the appropriate interface.</span></span>

<span data-ttu-id="b6a1b-199">[IOptionsMonitorCache&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1)(ASP.NET Core 2.0 이상)는 `IOptionsMonitor`에서 `TOptions` 인스턴스를 캐시하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-199">[IOptionsMonitorCache&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1) (ASP.NET Core 2.0 or later) is used by `IOptionsMonitor` to cache `TOptions` instances.</span></span> <span data-ttu-id="b6a1b-200">`IOptionsMonitorCache`는 모니터에서 옵션 인스턴스를 무효화하므로 값이 다시 계산됩니다([TryRemove](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryremove)).</span><span class="sxs-lookup"><span data-stu-id="b6a1b-200">The `IOptionsMonitorCache` invalidates options instances in the monitor so that the value is recomputed ([TryRemove](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryremove)).</span></span> <span data-ttu-id="b6a1b-201">또한 [TryAdd](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryadd)로 값을 수동으로 도입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-201">Values can be manually introduced as well with [TryAdd](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryadd).</span></span> <span data-ttu-id="b6a1b-202">모든 명명된 인스턴스를 필요에 따라 다시 생성해야 하는 경우 [Clear](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.clear) 메서드가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-202">The [Clear](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.clear) method is used when all named instances should be recreated on demand.</span></span>

## <a name="accessing-options-during-startup"></a><span data-ttu-id="b6a1b-203">시작하는 동안 옵션 액세스</span><span class="sxs-lookup"><span data-stu-id="b6a1b-203">Accessing options during startup</span></span>

<span data-ttu-id="b6a1b-204">서비스는 `Configure` 메서드가 실행되기 전에 빌드되므로 `IOptions`를 `Configure`에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-204">`IOptions` can be used in `Configure`, since services are built before the `Configure` method executes.</span></span> <span data-ttu-id="b6a1b-205">옵션에 액세스하기 위해 서비스 공급자가 `ConfigureServices`에서 기본 제공되는 경우 서비스 공급자가 빌드된 후 제공되는 옵션 구성을 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-205">If a service provider is built in `ConfigureServices` to access options, it wouldn't contain any options configurations provided after the service provider is built.</span></span> <span data-ttu-id="b6a1b-206">따라서 서비스 등록의 순서 지정으로 인해 일관성 없는 옵션 상태가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-206">Therefore, an inconsistent options state may exist due to the ordering of service registrations.</span></span>

<span data-ttu-id="b6a1b-207">옵션은 일반적으로 구성에서 로드되므로 구성은 `Configure` 및 `ConfigureServices` 모두에서 시작에 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-207">Since options are typically loaded from configuration, configuration can be used in startup in both `Configure` and `ConfigureServices`.</span></span> <span data-ttu-id="b6a1b-208">시작하는 동안 구성 사용에 관한 예제는 [응용 프로그램 시작](xref:fundamentals/startup) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6a1b-208">For examples of using configuration during startup, see the [Application startup](xref:fundamentals/startup) topic.</span></span>

## <a name="see-also"></a><span data-ttu-id="b6a1b-209">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b6a1b-209">See also</span></span>

* [<span data-ttu-id="b6a1b-210">구성</span><span class="sxs-lookup"><span data-stu-id="b6a1b-210">Configuration</span></span>](xref:fundamentals/configuration/index)
