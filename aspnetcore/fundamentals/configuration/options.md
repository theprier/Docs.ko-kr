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
ms.openlocfilehash: 7d89416626433bf737b63eda4b17e65b089ae142
ms.sourcegitcommit: 8f42ab93402c1b8044815e1e48d0bb84c81f8b59
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/29/2017
---
# <a name="options-pattern-in-aspnet-core"></a><span data-ttu-id="e4bb7-103">ASP.NET Core에서 옵션 패턴</span><span class="sxs-lookup"><span data-stu-id="e4bb7-103">Options pattern in ASP.NET Core</span></span>

<span data-ttu-id="e4bb7-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="e4bb7-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="e4bb7-105">옵션 패턴 옵션 클래스를 사용 하 여 관련된 설정의 그룹을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-105">The options pattern uses options classes to represent groups of related settings.</span></span> <span data-ttu-id="e4bb7-106">구성 설정은 별도 옵션 클래스에 기능에 의해 격리 됩니다, 있을 때 응용 프로그램 두 가지 중요 한 소프트웨어 엔지니어링 원칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-106">When configuration settings are isolated by feature into separate options classes, the app adheres to two important software engineering principles:</span></span>

* <span data-ttu-id="e4bb7-107">[인터페이스 분리 원칙 (ISP)](http://deviq.com/interface-segregation-principle/): 구성 설정에 종속 된 기능 (클래스)만 사용 하는 구성 설정에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-107">The [Interface Segregation Principle (ISP)](http://deviq.com/interface-segregation-principle/): Features (classes) that depend on configuration settings depend only on the configuration settings that they use.</span></span>
* <span data-ttu-id="e4bb7-108">[문제의 분리](http://deviq.com/separation-of-concerns/): 종속 또는 서로 결합 된 응용 프로그램의 다른 부분에 대 한 설정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-108">[Separation of Concerns](http://deviq.com/separation-of-concerns/): Settings for different parts of the app aren't dependent or coupled to one another.</span></span>

<span data-ttu-id="e4bb7-109">[보거나 다운로드 샘플 코드](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample))이이 문서 샘플 응용 프로그램에 대 한 따라 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-109">[View or download sample code](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)) This article is easier to follow with the sample app.</span></span>

## <a name="basic-options-configuration"></a><span data-ttu-id="e4bb7-110">기본 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="e4bb7-110">Basic options configuration</span></span>

<span data-ttu-id="e4bb7-111">기본 옵션 구성 예제로 나와 &num;1에는 [샘플 응용 프로그램](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-111">Basic options configuration is demonstrated as Example &num;1 in the [sample app](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="e4bb7-112">옵션 클래스에 추상이 아닌 여야 합니다. 매개 변수가 없는 public 생성자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-112">An options class must be non-abstract with a public parameterless constructor.</span></span> <span data-ttu-id="e4bb7-113">다음 클래스 `MyOptions`, 다음 두 가지 속성이 `Option1` 및 `Option2`합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-113">The following class, `MyOptions`, has two properties, `Option1` and `Option2`.</span></span> <span data-ttu-id="e4bb7-114">기본 값을 설정 하는 것은 선택적 이지만의 기본값을 설정 하는 다음 예제에서 클래스 생성자 `Option1`합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-114">Setting default values is optional, but the class constructor in the following example sets the default value of `Option1`.</span></span> <span data-ttu-id="e4bb7-115">`Option2`직접 속성을 초기화 하 여 설정의 기본값이 (*Models/MyOptions.cs*):</span><span class="sxs-lookup"><span data-stu-id="e4bb7-115">`Option2` has a default value set by initializing the property directly (*Models/MyOptions.cs*):</span></span>

[!code-csharp[Main](options/sample/Models/MyOptions.cs?name=snippet1)]

<span data-ttu-id="e4bb7-116">`MyOptions` 클래스에는 서비스 컨테이너에 추가 됩니다 [IConfigureOptions&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) 구성에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-116">The `MyOptions` class is added to the service container with [IConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) and bound to configuration:</span></span>

[!code-csharp[Main](options/sample/Startup.cs?name=snippet_Example1)]

<span data-ttu-id="e4bb7-117">다음 페이지는 모델 [생성자 종속성 주입](xref:fundamentals/dependency-injection#what-is-dependency-injection) 와 [IOptions&lt;TOptions&gt; ](/dotnet/api/Microsoft.Extensions.Options.IOptions-1) 는 설정에 액세스 하려면 (*Pages/Index.cshtml.cs*):</span><span class="sxs-lookup"><span data-stu-id="e4bb7-117">The following page model uses [constructor dependency injection](xref:fundamentals/dependency-injection#what-is-dependency-injection) with [IOptions&lt;TOptions&gt;](/dotnet/api/Microsoft.Extensions.Options.IOptions-1) to access the settings (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet_Example1)]

<span data-ttu-id="e4bb7-118">샘플의 *appsettings.json* 파일에 대 한 값을 지정 `option1` 및 `option2`:</span><span class="sxs-lookup"><span data-stu-id="e4bb7-118">The sample's *appsettings.json* file specifies values for `option1` and `option2`:</span></span>

[!code-json[Main](options/sample/appsettings.json)]

<span data-ttu-id="e4bb7-119">응용 프로그램을 실행할 때 페이지 모델 `OnGet` 메서드 옵션 클래스 값을 표시 하는 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-119">When the app is run, the page model's `OnGet` method returns a string showing the option class values:</span></span>

```html
option1 = value1_from_json, option2 = -1
```

## <a name="configure-simple-options-with-a-delegate"></a><span data-ttu-id="e4bb7-120">대리자에 간단한 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="e4bb7-120">Configure simple options with a delegate</span></span>

<span data-ttu-id="e4bb7-121">예제로 나와 대리자를 사용 하 여 간단한 옵션 구성 &num;에서 값 2는 [샘플 응용 프로그램](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-121">Configuring simple options with a delegate is demonstrated as Example &num;2 in the [sample app](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="e4bb7-122">대리자를 사용 하 여 옵션 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-122">Use a delegate to set options values.</span></span> <span data-ttu-id="e4bb7-123">샘플 앱에서는 `MyOptionsWithDelegateConfig` 클래스 (*Models/MyOptionsWithDelegateConfig.cs*):</span><span class="sxs-lookup"><span data-stu-id="e4bb7-123">The sample app uses the `MyOptionsWithDelegateConfig` class (*Models/MyOptionsWithDelegateConfig.cs*):</span></span>

[!code-csharp[Main](options/sample/Models/MyOptionsWithDelegateConfig.cs?name=snippet1)]

<span data-ttu-id="e4bb7-124">다음 코드에서 두 번째 `IConfigureOptions<TOptions>` 서비스를 서비스 컨테이너에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-124">In the following code, a second `IConfigureOptions<TOptions>` service is added to the service container.</span></span> <span data-ttu-id="e4bb7-125">대리자를 사용 하 여 바인딩을 구성 `MyOptionsWithDelegateConfig`:</span><span class="sxs-lookup"><span data-stu-id="e4bb7-125">It uses a delegate to configure the binding with `MyOptionsWithDelegateConfig`:</span></span>

[!code-csharp[Main](options/sample/Startup.cs?name=snippet_Example2)]

<span data-ttu-id="e4bb7-126">*Index.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="e4bb7-126">*Index.cshtml.cs*:</span></span>

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?range=10)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3,9)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet_Example2)]

<span data-ttu-id="e4bb7-127">여러 구성 공급자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-127">You can add multiple configuration providers.</span></span> <span data-ttu-id="e4bb7-128">구성 공급자는 NuGet 패키지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-128">Configuration providers are available in NuGet packages.</span></span> <span data-ttu-id="e4bb7-129">등록 하는 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-129">They're applied in order that they're registered.</span></span>

<span data-ttu-id="e4bb7-130">호출할 때마다 [구성&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1.configure) 추가 `IConfigureOptions<TOptions>` 서비스를 서비스 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-130">Each call to [Configure&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1.configure) adds an `IConfigureOptions<TOptions>` service to the service container.</span></span> <span data-ttu-id="e4bb7-131">위의 예제에서는 값 `Option1` 및 `Option2` 에 지정 된 *appsettings.json*, 하지만 값의 `Option1` 및 `Option2` 구성 된 대리자에 의해 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-131">In the preceding example, the values of `Option1` and `Option2` are both specified in *appsettings.json*, but the values of `Option1` and `Option2` are overridden by the configured delegate.</span></span>

<span data-ttu-id="e4bb7-132">둘 이상의 구성 서비스를 사용 하는 경우 마지막 구성 소스 지정 *wins* 구성 값을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-132">When more than one configuration service is enabled, the last configuration source specified *wins* and sets the configuration value.</span></span> <span data-ttu-id="e4bb7-133">응용 프로그램을 실행할 때 페이지 모델 `OnGet` 메서드 옵션 클래스 값을 표시 하는 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-133">When the app is run, the page model's `OnGet` method returns a string showing the option class values:</span></span>

```html
delegate_option1 = value1_configured_by_delgate, delegate_option2 = 500
```

## <a name="suboptions-configuration"></a><span data-ttu-id="e4bb7-134">하위 옵션이 구성</span><span class="sxs-lookup"><span data-stu-id="e4bb7-134">Suboptions configuration</span></span>

<span data-ttu-id="e4bb7-135">하위 옵션이 구성 예제로 나와 &num;3에는 [샘플 응용 프로그램](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-135">Suboptions configuration is demonstrated as Example &num;3 in the [sample app](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="e4bb7-136">앱은 앱의 특정 기능 그룹 (클래스)와 관련 된 옵션 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-136">Apps should create options classes that pertain to specific feature groups (classes) in the app.</span></span> <span data-ttu-id="e4bb7-137">구성 값을 필요로 하는 응용 프로그램의 일부를 사용 하는 구성 값에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-137">Parts of the app that require configuration values should only have access to the configuration values that they use.</span></span>

<span data-ttu-id="e4bb7-138">각 속성에 옵션의 유형 폼의 구성 키에 바인딩된 옵션을 구성을 바인딩하는 경우 `property[:sub-property:]`합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-138">When binding options to configuration, each property in the options type is bound to a configuration key of the form `property[:sub-property:]`.</span></span> <span data-ttu-id="e4bb7-139">예를 들어는 `MyOptions.Option1` 속성의 키에 바인딩된 `Option1`에서 읽음는 `option1` 속성 *appsettings.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-139">For example, the `MyOptions.Option1` property is bound to the key `Option1`, which is read from the `option1` property in *appsettings.json*.</span></span>

<span data-ttu-id="e4bb7-140">다음 코드에서는 세 번째 `IConfigureOptions<TOptions>` 서비스를 서비스 컨테이너에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-140">In the following code, a third `IConfigureOptions<TOptions>` service is added to the service container.</span></span> <span data-ttu-id="e4bb7-141">바인딩할 `MySubOptions` 섹션 `subsection` 의 *appsettings.json* 파일:</span><span class="sxs-lookup"><span data-stu-id="e4bb7-141">It binds `MySubOptions` to the section `subsection` of the *appsettings.json* file:</span></span>

[!code-csharp[Main](options/sample/Startup.cs?name=snippet_Example3)]

<span data-ttu-id="e4bb7-142">`GetSection` 확장 메서드를 사용 하려면는 [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/) NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-142">The `GetSection` extension method requires the [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/) NuGet package.</span></span> <span data-ttu-id="e4bb7-143">응용 프로그램을 사용 하는 경우는 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) metapackage, 패키지를 자동으로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-143">If the app uses the [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) metapackage, the package is automatically included.</span></span>

<span data-ttu-id="e4bb7-144">샘플의 *appsettings.json* 파일 정의 `subsection` 멤버에 대 한 키를 가진 `suboption1` 및 `suboption2`:</span><span class="sxs-lookup"><span data-stu-id="e4bb7-144">The sample's *appsettings.json* file defines a `subsection` member with keys for `suboption1` and `suboption2`:</span></span>

[!code-json[Main](options/sample/appsettings.json?highlight=4-7)]

<span data-ttu-id="e4bb7-145">`MySubOptions` 클래스 속성을 정의 `SubOption1` 및 `SubOption2`하위 옵션 값을 유지 합니다 (*Models/MySubOptions.cs*):</span><span class="sxs-lookup"><span data-stu-id="e4bb7-145">The `MySubOptions` class defines properties, `SubOption1` and `SubOption2`, to hold the sub-option values (*Models/MySubOptions.cs*):</span></span>

[!code-csharp[Main](options/sample/Models/MySubOptions.cs?name=snippet1)]

<span data-ttu-id="e4bb7-146">페이지 모델 `OnGet` 하위 옵션 값이 포함 된 문자열을 반환 하는 메서드 (*Pages/Index.cshtml.cs*):</span><span class="sxs-lookup"><span data-stu-id="e4bb7-146">The page model's `OnGet` method returns a string with the sub-option values (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?range=11)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=4,10)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet_Example3)]

<span data-ttu-id="e4bb7-147">앱이 실행 되는 경우는 `OnGet` 메서드 하위 옵션 클래스 값을 표시 하는 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-147">When the app is run, the `OnGet` method returns a string showing the sub-option class values:</span></span>

```html
subOption1 = subvalue1_from_json, subOption2 = 200
```

## <a name="options-provided-by-a-view-model-or-with-direct-view-injection"></a><span data-ttu-id="e4bb7-148">직접 보기 주입 또는 보기 모델에 의해 제공 되는 옵션</span><span class="sxs-lookup"><span data-stu-id="e4bb7-148">Options provided by a view model or with direct view injection</span></span>

<span data-ttu-id="e4bb7-149">예제로 직접 보기 주입 또는 보기 모델에 의해 제공 되는 옵션에 대해서는 설명 &num;4에는 [샘플 응용 프로그램](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-149">Options provided by a view model or with direct view injection is demonstrated as Example &num;4 in the [sample app](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="e4bb7-150">뷰 모델 또는 삽입 하 여 옵션을 제공할 수 있습니다 `IOptions<TOptions>` 보기에 직접 (*Pages/Index.cshtml.cs*):</span><span class="sxs-lookup"><span data-stu-id="e4bb7-150">Options can be supplied in a view model or by injecting `IOptions<TOptions>` directly into a view (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet_Example4)]

<span data-ttu-id="e4bb7-151">직접 삽입에 대 한 삽입 `IOptions<MyOptions>` 와 `@inject` 지시문:</span><span class="sxs-lookup"><span data-stu-id="e4bb7-151">For direct injection, inject `IOptions<MyOptions>` with an `@inject` directive:</span></span>

[!code-cshtml[Main](options/sample/Pages/Index.cshtml?range=1-10&highlight=5)]

<span data-ttu-id="e4bb7-152">앱이 실행 되는 경우 옵션 값은 렌더링된 된 페이지에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-152">When the app is run, the option values are shown in the rendered page:</span></span>

![옵션 값 옵션 1: value1_from_json 및 옵션 2:-1 로드 모델에서 보기에 삽입 합니다.](options/_static/view.png)

## <a name="reload-configuration-data-with-ioptionssnapshot"></a><span data-ttu-id="e4bb7-154">IOptionsSnapshot 사용 하 여 구성 데이터를 다시 로드</span><span class="sxs-lookup"><span data-stu-id="e4bb7-154">Reload configuration data with IOptionsSnapshot</span></span>

<span data-ttu-id="e4bb7-155">구성 데이터를 다시 로드 `IOptionsSnapshot` 예제에 나와 &num;5는 [샘플 응용 프로그램](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-155">Reloading configuration data with `IOptionsSnapshot` is demonstrated in Example &num;5 in the [sample app](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="e4bb7-156">*ASP.NET Core 1.1 이상 필요합니다.*</span><span class="sxs-lookup"><span data-stu-id="e4bb7-156">*Requires ASP.NET Core 1.1 or later.*</span></span>

<span data-ttu-id="e4bb7-157">[IOptionsSnapshot](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1) 최소한의 처리 오버 헤드 및 옵션을 다시 로드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-157">[IOptionsSnapshot](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1) supports reloading options with minimal processing overhead.</span></span> <span data-ttu-id="e4bb7-158">ASP.NET Core 1.1에서 `IOptionsSnapshot` 계획 [IOptionsMonitor&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) 트리거와 업데이트가 자동으로 때마다 모니터 데이터 원본 변경에 따라 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-158">In ASP.NET Core 1.1, `IOptionsSnapshot` is a snapshot of [IOptionsMonitor&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) and updates automatically whenever the monitor triggers changes based on the data source changing.</span></span> <span data-ttu-id="e4bb7-159">ASP.NET Core 2.0 이상 버전에서는 옵션 고 요청의 수명 동안 캐시에 액세스할 때 요청당 한 번 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-159">In ASP.NET Core 2.0 and later, options are computed once per request when accessed and cached for the lifetime of the request.</span></span>

<span data-ttu-id="e4bb7-160">다음 예제에서는 새 방법을 `IOptionsSnapshot` 후에 만들어진 *appsettings.json* 변경 (*Pages/Index.cshtml.cs*).</span><span class="sxs-lookup"><span data-stu-id="e4bb7-160">The following example demonstrates how a new `IOptionsSnapshot` is created after *appsettings.json* changes (*Pages/Index.cshtml.cs*).</span></span> <span data-ttu-id="e4bb7-161">서버에 대 한 여러 요청에서 제공 하는 상수 값을 반환 된 *appsettings.json* 파일이 변경 되 고 구성 다시 로드 될 때까지 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-161">Multiple requests to the server return constant values provided by the *appsettings.json* file until the file is changed and configuration reloads.</span></span>

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?range=12)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=5,11)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet_Example5)]

<span data-ttu-id="e4bb7-162">다음 이미지는 초기 표시 `option1` 및 `option2` 값에서 로드 된 *appsettings.json* 파일:</span><span class="sxs-lookup"><span data-stu-id="e4bb7-162">The following image shows the initial `option1` and `option2` values loaded from the *appsettings.json* file:</span></span>

```html
snapshot option1 = value1_from_json, snapshot option2 = -1
```

<span data-ttu-id="e4bb7-163">값을 변경는 *appsettings.json* 파일을 `value1_from_json UPDATED` 및 `200`합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-163">Change the values in the *appsettings.json* file to `value1_from_json UPDATED` and `200`.</span></span> <span data-ttu-id="e4bb7-164">저장 된 *appsettings.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-164">Save the *appsettings.json* file.</span></span> <span data-ttu-id="e4bb7-165">옵션 값이 업데이트를 확인 하려면 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-165">Refresh the browser to see that the options values are updated:</span></span>

```html
snapshot option1 = value1_from_json UPDATED, snapshot option2 = 200
```

## <a name="named-options-support-with-iconfigurenamedoptions"></a><span data-ttu-id="e4bb7-166">라는 IConfigureNamedOptions 옵션 지원</span><span class="sxs-lookup"><span data-stu-id="e4bb7-166">Named options support with IConfigureNamedOptions</span></span>

<span data-ttu-id="e4bb7-167">관련 옵션 지원을 라는 [IConfigureNamedOptions](/dotnet/api/microsoft.extensions.options.iconfigurenamedoptions-1) 예제로 나와 &num;에서 6는 [샘플 응용 프로그램](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-167">Named options support with [IConfigureNamedOptions](/dotnet/api/microsoft.extensions.options.iconfigurenamedoptions-1) is demonstrated as Example &num;6 in the [sample app](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/options/sample).</span></span>

<span data-ttu-id="e4bb7-168">*ASP.NET Core 2.0 이상이 필요합니다.*</span><span class="sxs-lookup"><span data-stu-id="e4bb7-168">*Requires ASP.NET Core 2.0 or later.*</span></span>

<span data-ttu-id="e4bb7-169">*옵션 라는* 지원을 통해 응용 프로그램에서 명명 된 옵션을 구성을 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-169">*Named options* support allows the app to distinguish between named options configurations.</span></span> <span data-ttu-id="e4bb7-170">샘플 응용 프로그램을 명명 된 옵션으로 선언 되는 [ConfigureNamedOptions&lt;TOptions&gt;합니다. 구성](/dotnet/api/microsoft.extensions.options.configurenamedoptions-1.configure) 메서드:</span><span class="sxs-lookup"><span data-stu-id="e4bb7-170">In the sample app, named options are declared with the [ConfigureNamedOptions&lt;TOptions&gt;.Configure](/dotnet/api/microsoft.extensions.options.configurenamedoptions-1.configure) method:</span></span>

[!code-csharp[Main](options/sample/Startup.cs?name=snippet_Example6)]

<span data-ttu-id="e4bb7-171">샘플 앱에서 사용 하 여 명명 된 옵션에 액세스 [IOptionsSnapshot&lt;TOptions&gt;합니다. 가져오기](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1.get) (*Pages/Index.cshtml.cs*):</span><span class="sxs-lookup"><span data-stu-id="e4bb7-171">The sample app accesses the named options with [IOptionsSnapshot&lt;TOptions&gt;.Get](/dotnet/api/microsoft.extensions.options.ioptionssnapshot-1.get) (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?range=13-14)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=6,12-13)]

[!code-csharp[Main](options/sample/Pages/Index.cshtml.cs?name=snippet_Example6)]

<span data-ttu-id="e4bb7-172">샘플 응용 프로그램을 실행, 명명 된 옵션은이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-172">Running the sample app, the named options are returned:</span></span>

```html
named_options_1: option1 = value1_from_json, option2 = -1
named_options_2: option1 = named_options_2_value1_from_action, option2 = 5
```

<span data-ttu-id="e4bb7-173">`named_options_1`로드 되는, 구성에서 값을 제공 된 *appsettings.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-173">`named_options_1` values are provided from configuration, which are loaded from the *appsettings.json* file.</span></span> <span data-ttu-id="e4bb7-174">`named_options_2`값으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-174">`named_options_2` values are provided by:</span></span>

* <span data-ttu-id="e4bb7-175">`named_options_2` 에 위임 `ConfigureServices` 에 대 한 `Option1`합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-175">The `named_options_2` delegate in `ConfigureServices` for `Option1`.</span></span>
* <span data-ttu-id="e4bb7-176">에 대 한 기본값 `Option2` 에서 제공 되는 `MyOptions` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-176">The default value for `Option2` provided by the `MyOptions` class.</span></span>

<span data-ttu-id="e4bb7-177">구성 된 모든 옵션을 명명 된 인스턴스는 [OptionsServiceCollectionExtensions.ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) 메서드.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-177">Configure all named options instances with the [OptionsServiceCollectionExtensions.ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) method.</span></span> <span data-ttu-id="e4bb7-178">다음 코드를 구성 `Option1` 명명 된 공통 값을 사용 하는 구성 인스턴스 모두에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-178">The following code configures `Option1` for all named configuration instances with a common value.</span></span> <span data-ttu-id="e4bb7-179">다음 코드에 수동으로 추가 하는 `Configure` 메서드:</span><span class="sxs-lookup"><span data-stu-id="e4bb7-179">Add the following code manually to the `Configure` method:</span></span>

```csharp
services.ConfigureAll<MyOptions>(myOptions => 
{
    myOptions.Option1 = "ConfigureAll replacement value";
});
```

<span data-ttu-id="e4bb7-180">샘플 응용 프로그램 코드를 추가한 후에 실행 결과 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-180">Running the sample app after adding the code produces the following result:</span></span>

```html
named_options_1: option1 = ConfigureAll replacement value, option2 = -1
named_options_2: option1 = ConfigureAll replacement value, option2 = 5
```

> [!NOTE]
> <span data-ttu-id="e4bb7-181">ASP.NET Core 2.0 이상에서는 모든 옵션은 명명 된 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-181">In ASP.NET Core 2.0 and later, all options are named instances.</span></span> <span data-ttu-id="e4bb7-182">기존 `IConfigureOption` 인스턴스 대상으로 처리 되는 `Options.DefaultName` 인스턴스에 `string.Empty`합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-182">Existing `IConfigureOption` instances are treated as targeting the `Options.DefaultName` instance, which is `string.Empty`.</span></span> <span data-ttu-id="e4bb7-183">`IConfigureNamedOptions`또한 구현 `IConfigureOptions`합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-183">`IConfigureNamedOptions` also implements `IConfigureOptions`.</span></span> <span data-ttu-id="e4bb7-184">기본 구현은 [IOptionsFactory&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1) ([참조 소스](https://github.com/aspnet/Options/blob/release/2.0.0/src/Microsoft.Extensions.Options/OptionsFactory.cs)) 각 적절 하 게 사용 하는 논리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-184">The default implementation of the [IOptionsFactory&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1) ([reference source](https://github.com/aspnet/Options/blob/release/2.0.0/src/Microsoft.Extensions.Options/OptionsFactory.cs)) has logic to use each appropriately.</span></span> <span data-ttu-id="e4bb7-185">`null` 명명 된 옵션을 사용 하는 특정 명명 된 인스턴스 대신 명명 된 인스턴스는 모두 대상 ([ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) 및 [PostConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall) 이 규칙을 사용).</span><span class="sxs-lookup"><span data-stu-id="e4bb7-185">The `null` named option is used to target all of the named instances instead of a specific named instance ([ConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.configureall) and [PostConfigureAll](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall) use this convention).</span></span>

## <a name="ipostconfigureoptions"></a><span data-ttu-id="e4bb7-186">IPostConfigureOptions</span><span class="sxs-lookup"><span data-stu-id="e4bb7-186">IPostConfigureOptions</span></span>

<span data-ttu-id="e4bb7-187">*ASP.NET Core 2.0 이상이 필요합니다.*</span><span class="sxs-lookup"><span data-stu-id="e4bb7-187">*Requires ASP.NET Core 2.0 or later.*</span></span>

<span data-ttu-id="e4bb7-188">설정 된 postconfiguration [IPostConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-188">Set postconfiguration with [IPostConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1).</span></span> <span data-ttu-id="e4bb7-189">Postconfiguration 결국 실행 [IConfigureOptions&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) 구성 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-189">Postconfiguration runs after all [IConfigureOptions&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) configuration occurs:</span></span>

```csharp
services.PostConfigure<MyOptions>(myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

<span data-ttu-id="e4bb7-190">[PostConfigure&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1.postconfigure) 를 사후 명명 된 옵션을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-190">[PostConfigure&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ipostconfigureoptions-1.postconfigure) is available to post-configure named options:</span></span>

```csharp
services.PostConfigure<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

<span data-ttu-id="e4bb7-191">사용 하 여 [PostConfigureAll&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall) 후 모든를 구성 하 라는 구성 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="e4bb7-191">Use [PostConfigureAll&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.dependencyinjection.optionsservicecollectionextensions.postconfigureall) to post-configure all named configuration instances:</span></span>

```csharp
services.PostConfigureAll<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

## <a name="options-factory-monitoring-and-cache"></a><span data-ttu-id="e4bb7-192">공장 옵션, 모니터링 및 캐시</span><span class="sxs-lookup"><span data-stu-id="e4bb7-192">Options factory, monitoring, and cache</span></span>

<span data-ttu-id="e4bb7-193">[IOptionsMonitor](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) 알림에 사용 되는 경우 `TOptions` 인스턴스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-193">[IOptionsMonitor](/dotnet/api/microsoft.extensions.options.ioptionsmonitor-1) is used for notifications when `TOptions` instances change.</span></span> <span data-ttu-id="e4bb7-194">`IOptionsMonitor`지원 reloadable 옵션, 알림, 변경 및 `IPostConfigureOptions`합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-194">`IOptionsMonitor` supports reloadable options, change notifications, and `IPostConfigureOptions`.</span></span>

<span data-ttu-id="e4bb7-195">[IOptionsFactory&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1) (ASP.NET 코어 2.0 이상)는 인스턴스 옵션 새로 만들기에 대해 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-195">[IOptionsFactory&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1) (ASP.NET Core 2.0 or later) is responsible for creating new options instances.</span></span> <span data-ttu-id="e4bb7-196">에 단일 [만들기](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1.create) 메서드.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-196">It has a single [Create](/dotnet/api/microsoft.extensions.options.ioptionsfactory-1.create) method.</span></span> <span data-ttu-id="e4bb7-197">기본 구현에서는 등록 된 모든 `IConfigureOptions` 및 `IPostConfigureOptions` 모두 실행 하 고는 먼저 구성 하며, 그는 후 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-197">The default implementation takes all registered `IConfigureOptions` and `IPostConfigureOptions` and runs all the configures first, followed by the post-configures.</span></span> <span data-ttu-id="e4bb7-198">구별해 `IConfigureNamedOptions` 및 `IConfigureOptions` 만 적절 한 인터페이스를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-198">It distinguishes between `IConfigureNamedOptions` and `IConfigureOptions` and only calls the appropriate interface.</span></span>

<span data-ttu-id="e4bb7-199">[IOptionsMonitorCache&lt;TOptions&gt; ](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1) (ASP.NET 코어 2.0 이상) ´ â `IOptionsMonitor` 캐시에 `TOptions` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-199">[IOptionsMonitorCache&lt;TOptions&gt;](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1) (ASP.NET Core 2.0 or later) is used by `IOptionsMonitor` to cache `TOptions` instances.</span></span> <span data-ttu-id="e4bb7-200">`IOptionsMonitorCache` 모니터에서 인스턴스 옵션을 무효화 하는 값을 다시 계산 됩니다 ([TryRemove](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryremove)).</span><span class="sxs-lookup"><span data-stu-id="e4bb7-200">The `IOptionsMonitorCache` invalidates options instances in the monitor so that the value is recomputed ([TryRemove](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryremove)).</span></span> <span data-ttu-id="e4bb7-201">값 수동으로 쿼리도 [TryAdd](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryadd)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-201">Values can be manually introduced as well with [TryAdd](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.tryadd).</span></span> <span data-ttu-id="e4bb7-202">[지우기](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.clear) 메서드는 필요에 따라 모든 명명 된 인스턴스를 다시 만들어야 하는 경우 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bb7-202">The [Clear](/dotnet/api/microsoft.extensions.options.ioptionsmonitorcache-1.clear) method is used when all named instances should be recreated on demand.</span></span>

## <a name="see-also"></a><span data-ttu-id="e4bb7-203">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e4bb7-203">See also</span></span>

* [<span data-ttu-id="e4bb7-204">구성</span><span class="sxs-lookup"><span data-stu-id="e4bb7-204">Configuration</span></span>](xref:fundamentals/configuration/index)
