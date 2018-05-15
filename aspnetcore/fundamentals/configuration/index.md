---
title: ASP.NET Core의 구성
author: rick-anderson
description: 구성 API를 사용하여 여러 가지 방법으로 ASP.NET Core 앱을 구성합니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/11/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/configuration/index
ms.openlocfilehash: 4637ff6312f32f5887ff0f7a6e74d10f5beb0ca5
ms.sourcegitcommit: 477d38e33530a305405eaf19faa29c6d805273aa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="configuration-in-aspnet-core"></a><span data-ttu-id="a96fa-103">ASP.NET Core의 구성</span><span class="sxs-lookup"><span data-stu-id="a96fa-103">Configuration in ASP.NET Core</span></span>

<span data-ttu-id="a96fa-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [Mark Michaelis](http://intellitect.com/author/mark-michaelis/), [Steve Smith](https://ardalis.com/), [Daniel Roth](https://github.com/danroth27), [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="a96fa-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Mark Michaelis](http://intellitect.com/author/mark-michaelis/), [Steve Smith](https://ardalis.com/), [Daniel Roth](https://github.com/danroth27), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="a96fa-105">구성 API는 이름-값 쌍 목록을 기반으로 ASP.NET Core 웹앱을 구성하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-105">The Configuration API provides a way to configure an ASP.NET Core web app based on a list of name-value pairs.</span></span> <span data-ttu-id="a96fa-106">구성은 여러 소스에서 런타임에 읽힙니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-106">Configuration is read at runtime from multiple sources.</span></span> <span data-ttu-id="a96fa-107">이름-값 쌍을 다중 수준 계층으로 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-107">Name-value pairs can be grouped into a multi-level hierarchy.</span></span>

<span data-ttu-id="a96fa-108">다음에 대한 구성 공급자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-108">There are configuration providers for:</span></span>

* <span data-ttu-id="a96fa-109">파일 형식(INI, JSON 및 XML).</span><span class="sxs-lookup"><span data-stu-id="a96fa-109">File formats (INI, JSON, and XML).</span></span>
* <span data-ttu-id="a96fa-110">명령줄 인수.</span><span class="sxs-lookup"><span data-stu-id="a96fa-110">Command-line arguments.</span></span>
* <span data-ttu-id="a96fa-111">환경 변수.</span><span class="sxs-lookup"><span data-stu-id="a96fa-111">Environment variables.</span></span>
* <span data-ttu-id="a96fa-112">메모리 내 .NET 개체.</span><span class="sxs-lookup"><span data-stu-id="a96fa-112">In-memory .NET objects.</span></span>
* <span data-ttu-id="a96fa-113">암호화되지 않은 [암호 관리자](xref:security/app-secrets) 저장소.</span><span class="sxs-lookup"><span data-stu-id="a96fa-113">The unencrypted [Secret Manager](xref:security/app-secrets) storage.</span></span>
* <span data-ttu-id="a96fa-114">암호화된 사용자 저장소(예:[Azure Key Vault](xref:security/key-vault-configuration)).</span><span class="sxs-lookup"><span data-stu-id="a96fa-114">An encrypted user store, such as [Azure Key Vault](xref:security/key-vault-configuration).</span></span>
* <span data-ttu-id="a96fa-115">사용자 지정 공급자(설치 또는 생성된).</span><span class="sxs-lookup"><span data-stu-id="a96fa-115">Custom providers (installed or created).</span></span>

<span data-ttu-id="a96fa-116">각 구성 값은 문자열 키에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-116">Each configuration value maps to a string key.</span></span> <span data-ttu-id="a96fa-117">설정을 사용자 지정 [POCO](https://wikipedia.org/wiki/Plain_Old_CLR_Object) 개체(속성이 있는 간단한 .NET 클래스)로 deserialize하는 바인딩 지원이 기본적으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-117">There's built-in binding support to deserialize settings into a custom [POCO](https://wikipedia.org/wiki/Plain_Old_CLR_Object) object (a simple .NET class with properties).</span></span>

<span data-ttu-id="a96fa-118">옵션 패턴은 옵션 클래스를 사용하여 관련 설정 그룹을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-118">The options pattern uses options classes to represent groups of related settings.</span></span> <span data-ttu-id="a96fa-119">옵션 패턴 사용에 대한 자세한 내용은 [옵션](xref:fundamentals/configuration/options) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-119">For more information on using the options pattern, see the [Options](xref:fundamentals/configuration/options) topic.</span></span>

<span data-ttu-id="a96fa-120">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/index/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="a96fa-120">[View or download sample code](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/configuration/index/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="json-configuration"></a><span data-ttu-id="a96fa-121">JSON 구성</span><span class="sxs-lookup"><span data-stu-id="a96fa-121">JSON configuration</span></span>

<span data-ttu-id="a96fa-122">다음 콘솔 앱은 JSON 구성 공급자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-122">The following console app uses the JSON configuration provider:</span></span>

[!code-csharp[](index/sample/ConfigJson/Program.cs)]

<span data-ttu-id="a96fa-123">앱은 다음 구성 설정을 읽고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-123">The app reads and displays the following configuration settings:</span></span>

[!code-json[](index/sample/ConfigJson/appsettings.json)]

<span data-ttu-id="a96fa-124">구성은 콜론(`:`)으로 노드를 구분하는 이름-값 쌍의 계층적 목록으로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-124">Configuration consists of a hierarchical list of name-value pairs in which the nodes are separated by a colon (`:`).</span></span> <span data-ttu-id="a96fa-125">값을 검색하려면 해당 항목의 키를 사용하여 `Configuration` 인덱서에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-125">To retrieve a value, access the `Configuration` indexer with the corresponding item's key:</span></span>

[!code-csharp[](index/sample/ConfigJson/Program.cs?range=21-22)]

<span data-ttu-id="a96fa-126">JSON 형식 구성 소스의 배열을 작업하려면 배열 인덱스를 콜론으로 구분된 문자열의 일부로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-126">To work with arrays in JSON-formatted configuration sources, use an array index as part of the colon-separated string.</span></span> <span data-ttu-id="a96fa-127">다음 예제는 앞에서 나온 `wizards` 배열의 첫 번째 항목 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-127">The following example gets the name of the first item in the preceding `wizards` array:</span></span>

```csharp
Console.Write($"{Configuration["wizards:0:Name"]}");
// Output: Gandalf
```

<span data-ttu-id="a96fa-128">기본 제공 [구성](/dotnet/api/microsoft.extensions.configuration) 공급자에 기록된 이름-값 쌍은 유지되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="a96fa-128">Name-value pairs written to the built-in [Configuration](/dotnet/api/microsoft.extensions.configuration) providers are **not** persisted.</span></span> <span data-ttu-id="a96fa-129">그러나 값을 저장하는 사용자 지정 공급자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-129">However, a custom provider that saves values can be created.</span></span> <span data-ttu-id="a96fa-130">[사용자 지정 구성 공급자](xref:fundamentals/configuration/index#custom-config-providers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-130">See [custom configuration provider](xref:fundamentals/configuration/index#custom-config-providers).</span></span>

<span data-ttu-id="a96fa-131">이전 샘플은 구성 인덱서를 사용하여 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-131">The preceding sample uses the configuration indexer to read values.</span></span> <span data-ttu-id="a96fa-132">`Startup` 외부에서 구성에 액세스하려면 *옵션 패턴*을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-132">To access configuration outside of `Startup`, use the *options pattern*.</span></span> <span data-ttu-id="a96fa-133">자세한 내용은 [옵션](xref:fundamentals/configuration/options) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-133">For more information, see the [Options](xref:fundamentals/configuration/options) topic.</span></span>

## <a name="xml-configuration"></a><span data-ttu-id="a96fa-134">XML 구성 </span><span class="sxs-lookup"><span data-stu-id="a96fa-134">XML configuration</span></span>

<span data-ttu-id="a96fa-135">XML 형식 구성 소스의 배열을 작업하려면 각 요소에 `name` 인덱스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-135">To work with arrays in XML-formatted configuration sources, provide a `name` index to each element.</span></span> <span data-ttu-id="a96fa-136">인덱스를 사용하여 값에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-136">Use the index to access the values:</span></span>

```xml
<wizards>
  <wizard name="Gandalf">
    <age>1000</age>
  </wizard>
  <wizard name="Harry">
    <age>17</age>
  </wizard>
</wizards>
```

```csharp
Console.Write($"{Configuration["wizard:Harry:age"]}");
// Output: 17
```

## <a name="configuration-by-environment"></a><span data-ttu-id="a96fa-137">환경별 구성</span><span class="sxs-lookup"><span data-stu-id="a96fa-137">Configuration by environment</span></span>

<span data-ttu-id="a96fa-138">개발, 테스트, 프로덕션 등 환경마다 다른 구성 설정을 사용하는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-138">It's typical to have different configuration settings for different environments, for example, development, testing, and production.</span></span> <span data-ttu-id="a96fa-139">ASP.NET Core 2.x 앱의 `CreateDefaultBuilder` 확장 메서드(또는 ASP.NET Core 1.x 앱에서 바로 `AddJsonFile` 및 `AddEnvironmentVariables` 사용)는 JSON 파일 및 시스템 구성 소스를 읽기 위한 구성 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-139">The `CreateDefaultBuilder` extension method in an ASP.NET Core 2.x app (or using `AddJsonFile` and `AddEnvironmentVariables` directly in an ASP.NET Core 1.x app) adds configuration providers for reading JSON files and system configuration sources:</span></span>

* <span data-ttu-id="a96fa-140">*appsettings.json*</span><span class="sxs-lookup"><span data-stu-id="a96fa-140">*appsettings.json*</span></span>
* <span data-ttu-id="a96fa-141">*appsettings.\<EnvironmentName>.json*</span><span class="sxs-lookup"><span data-stu-id="a96fa-141">*appsettings.\<EnvironmentName>.json*</span></span>
* <span data-ttu-id="a96fa-142">환경 변수</span><span class="sxs-lookup"><span data-stu-id="a96fa-142">Environment variables</span></span>

<span data-ttu-id="a96fa-143">ASP.NET Core 1.x 앱은 `AddJsonFile` 및 [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables#Microsoft_Extensions_Configuration_EnvironmentVariablesExtensions_AddEnvironmentVariables_Microsoft_Extensions_Configuration_IConfigurationBuilder_System_String_)를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-143">ASP.NET Core 1.x apps need to call `AddJsonFile` and [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables#Microsoft_Extensions_Configuration_EnvironmentVariablesExtensions_AddEnvironmentVariables_Microsoft_Extensions_Configuration_IConfigurationBuilder_System_String_).</span></span>

<span data-ttu-id="a96fa-144">매개 변수에 대한 설명은 [AddJsonFile](/dotnet/api/microsoft.extensions.configuration.jsonconfigurationextensions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-144">See [AddJsonFile](/dotnet/api/microsoft.extensions.configuration.jsonconfigurationextensions) for an explanation of the parameters.</span></span> <span data-ttu-id="a96fa-145">`reloadOnChange`는 ASP.NET Core 1.1 이상에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-145">`reloadOnChange` is only supported in ASP.NET Core 1.1 and later.</span></span>

<span data-ttu-id="a96fa-146">구성 소스는 지정된 순서대로 읽힙니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-146">Configuration sources are read in the order that they're specified.</span></span> <span data-ttu-id="a96fa-147">이전 코드에서 환경 변수는 마지막에 읽힙니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-147">In the preceding code, the environment variables are read last.</span></span> <span data-ttu-id="a96fa-148">환경을 통해 설정된 구성 값은 두 이전 공급자에서 설정된 구성 값을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-148">Any configuration values set through the environment replace those set in the two previous providers.</span></span>

<span data-ttu-id="a96fa-149">다음 *appsettings.Staging.json* 파일을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-149">Consider the following *appsettings.Staging.json* file:</span></span>

[!code-json[](index/sample/appsettings.Staging.json)]

<span data-ttu-id="a96fa-150">환경이 `Staging`으로 설정되면 다음 `Configure` 메서드가 `MyConfig` 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-150">When the environment is set to `Staging`, the following `Configure` method reads the value of `MyConfig`:</span></span>

[!code-csharp[](index/sample/StartupConfig.cs?name=snippet&highlight=3,4)]

<span data-ttu-id="a96fa-151">환경은 일반적으로 `Development`, `Staging` 또는 `Production`으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-151">The environment is typically set to `Development`, `Staging`, or `Production`.</span></span> <span data-ttu-id="a96fa-152">자세한 내용은 [여러 환경 사용](xref:fundamentals/environments)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-152">For more information, see [Use multiple environments](xref:fundamentals/environments).</span></span>

<span data-ttu-id="a96fa-153">구성 고려 사항:</span><span class="sxs-lookup"><span data-stu-id="a96fa-153">Configuration considerations:</span></span>

* <span data-ttu-id="a96fa-154">[IOptionsSnapshot](xref:fundamentals/configuration/options#reload-configuration-data-with-ioptionssnapshot)은 구성 데이터가 변경되면 구성 데이터를 다시 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-154">[IOptionsSnapshot](xref:fundamentals/configuration/options#reload-configuration-data-with-ioptionssnapshot) can reload configuration data when it changes.</span></span>
* <span data-ttu-id="a96fa-155">구성 키는 대/소문자를 구분하지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="a96fa-155">Configuration keys are **not** case-sensitive.</span></span>
* <span data-ttu-id="a96fa-156">구성 공급자 코드 또는 일반 텍스트 구성 파일에 암호 또는 기타 중요한 데이터를 **절대 저장하지 마세요**.</span><span class="sxs-lookup"><span data-stu-id="a96fa-156">**Never** store passwords or other sensitive data in configuration provider code or in plain text configuration files.</span></span> <span data-ttu-id="a96fa-157">개발 또는 테스트 환경에서 프로덕션 비밀을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-157">Don't use production secrets in development or test environments.</span></span> <span data-ttu-id="a96fa-158">의도치 않게 소스 코드 리포지토리에 커밋되는 일이 없도록 프로젝트 외부에서 비밀을 지정하세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-158">Specify secrets outside of the project so that they can't be accidentally committed to a source code repository.</span></span> <span data-ttu-id="a96fa-159">[여러 환경을 사용하는 방법](xref:fundamentals/environments) 및 [개발 중 안전한 앱 비밀 저장소](xref:security/app-secrets) 관리에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-159">Learn more about [how to use multiple environments](xref:fundamentals/environments) and managing [safe storage of app secrets in development](xref:security/app-secrets).</span></span>
* <span data-ttu-id="a96fa-160">환경 변수에 지정된 계층적 구성 값의 경우 콜론(`:`)은 모든 플랫폼에서 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-160">For hierarchical config values specified in environment variables, a colon (`:`) may not work on all platforms.</span></span> <span data-ttu-id="a96fa-161">두 개의 밑줄(`__`)은 모든 플랫폼에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-161">Double underscore (`__`) is supported by all platforms.</span></span>
* <span data-ttu-id="a96fa-162">구성 API와 상호 작용하는 경우 콜론(`:`)은 모든 플랫폼에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-162">When interacting with the configuration API, a colon (`:`) works on all platforms.</span></span>

## <a name="in-memory-provider-and-binding-to-a-poco-class"></a><span data-ttu-id="a96fa-163">메모리 내 공급자 및 POCO 클래스에 바인딩</span><span class="sxs-lookup"><span data-stu-id="a96fa-163">In-memory provider and binding to a POCO class</span></span>

<span data-ttu-id="a96fa-164">다음 샘플은 메모리 내 공급자를 사용하고 클래스에 바인딩하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-164">The following sample shows how to use the in-memory provider and bind to a class:</span></span>

[!code-csharp[](index/sample/InMemory/Program.cs)]

<span data-ttu-id="a96fa-165">구성 값이 문자열로 반환되지만, 바인딩을 통해 개체를 생성할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-165">Configuration values are returned as strings, but binding enables the construction of objects.</span></span> <span data-ttu-id="a96fa-166">바인딩을 사용하면 POCO 개체 또는 심지어 전체 개체 그래프를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-166">Binding allows the retrieval of POCO objects or even entire object graphs.</span></span>

### <a name="getvalue"></a><span data-ttu-id="a96fa-167">GetValue</span><span class="sxs-lookup"><span data-stu-id="a96fa-167">GetValue</span></span>

<span data-ttu-id="a96fa-168">다음 샘플은 [GetValue&lt;T&gt;](/dotnet/api/microsoft.extensions.configuration.configurationbinder.get?view=aspnetcore-2.0#Microsoft_Extensions_Configuration_ConfigurationBinder_Get__1_Microsoft_Extensions_Configuration_IConfiguration_) 확장 메서드를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-168">The following sample demonstrates the [GetValue&lt;T&gt;](/dotnet/api/microsoft.extensions.configuration.configurationbinder.get?view=aspnetcore-2.0#Microsoft_Extensions_Configuration_ConfigurationBinder_Get__1_Microsoft_Extensions_Configuration_IConfiguration_) extension method:</span></span>

[!code-csharp[](index/sample/InMemoryGetValue/Program.cs?highlight=31)]

<span data-ttu-id="a96fa-169">ConfigurationBinder의 `GetValue<T>` 메서드를 사용하여 기본값을 지정할 수 있습니다(이 샘플에서는 80).</span><span class="sxs-lookup"><span data-stu-id="a96fa-169">The ConfigurationBinder's `GetValue<T>` method allows the specification of a default value (80 in the sample).</span></span> <span data-ttu-id="a96fa-170">`GetValue<T>`는 간단한 시나리오에 사용되며 전체 섹션에 바인딩되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-170">`GetValue<T>` is for simple scenarios and doesn't bind to entire sections.</span></span> <span data-ttu-id="a96fa-171">`GetValue<T>`는 특정 형식으로 변환된 `GetSection(key).Value`에서 스칼라 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-171">`GetValue<T>` obtains scalar values from `GetSection(key).Value` converted to a specific type.</span></span>

## <a name="bind-to-an-object-graph"></a><span data-ttu-id="a96fa-172">개체 그래프에 바인딩</span><span class="sxs-lookup"><span data-stu-id="a96fa-172">Bind to an object graph</span></span>

<span data-ttu-id="a96fa-173">클래스의 각 개체를 재귀적으로 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-173">Each object in a class can be recursively bound.</span></span> <span data-ttu-id="a96fa-174">다음 `AppSettings` 클래스를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-174">Consider the following `AppSettings` class:</span></span>

[!code-csharp[](index/sample/ObjectGraph/AppSettings.cs)]

<span data-ttu-id="a96fa-175">다음 샘플은 `AppSettings` 클래스에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-175">The following sample binds to the `AppSettings` class:</span></span>

[!code-csharp[](index/sample/ObjectGraph/Program.cs?highlight=15-16)]

<span data-ttu-id="a96fa-176">**ASP.NET Core 1.1** 이상은 전체 섹션에서 작동하는 `Get<T>`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-176">**ASP.NET Core 1.1** and higher can use `Get<T>`, which works with entire sections.</span></span> <span data-ttu-id="a96fa-177">`Get<T>`가 `Bind`을 사용하는 것보다 편리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-177">`Get<T>` can be more convenient than using `Bind`.</span></span> <span data-ttu-id="a96fa-178">다음 코드는 이전 샘플에 `Get<T>`를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-178">The following code shows how to use `Get<T>` with the preceding sample:</span></span>

```csharp
var appConfig = config.GetSection("App").Get<AppSettings>();
```

<span data-ttu-id="a96fa-179">다음 *appsettings.json* 파일 사용:</span><span class="sxs-lookup"><span data-stu-id="a96fa-179">Using the following *appsettings.json* file:</span></span>

[!code-json[](index/sample/ObjectGraph/appsettings.json)]

<span data-ttu-id="a96fa-180">프로그램에서는 `Height 11`을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-180">The program displays `Height 11`.</span></span>

<span data-ttu-id="a96fa-181">다음 코드를 구성 단위 테스트에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-181">The following code can be used to unit test the configuration:</span></span>

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

## <a name="create-an-entity-framework-custom-provider"></a><span data-ttu-id="a96fa-182">Entity Framework 사용자 지정 공급자 만들기</span><span class="sxs-lookup"><span data-stu-id="a96fa-182">Create an Entity Framework custom provider</span></span>

<span data-ttu-id="a96fa-183">이 섹션에서는 EF를 사용하여 데이터베이스에서 이름-값 쌍을 읽는 기본 구성 공급자가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-183">In this section, a basic configuration provider that reads name-value pairs from a database using EF is created.</span></span>

<span data-ttu-id="a96fa-184">데이터베이스에 구성 값을 저장하는 `ConfigurationValue` 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-184">Define a `ConfigurationValue` entity for storing configuration values in the database:</span></span>

[!code-csharp[](index/sample/CustomConfigurationProvider/ConfigurationValue.cs)]

<span data-ttu-id="a96fa-185">구성된 값을 저장 및 액세스하는 `ConfigurationContext`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-185">Add a `ConfigurationContext` to store and access the configured values:</span></span>

[!code-csharp[](index/sample/CustomConfigurationProvider/ConfigurationContext.cs?name=snippet1)]

<span data-ttu-id="a96fa-186">[IConfigurationSource](/dotnet/api/Microsoft.Extensions.Configuration.IConfigurationSource)를 구현하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-186">Create a class that implements [IConfigurationSource](/dotnet/api/Microsoft.Extensions.Configuration.IConfigurationSource):</span></span>

[!code-csharp[](index/sample/CustomConfigurationProvider/EntityFrameworkConfigurationSource.cs?highlight=7)]

<span data-ttu-id="a96fa-187">[ConfigurationProvider](/dotnet/api/Microsoft.Extensions.Configuration.ConfigurationProvider)에서 상속하여 사용자 지정 구성 공급자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-187">Create the custom configuration provider by inheriting from [ConfigurationProvider](/dotnet/api/Microsoft.Extensions.Configuration.ConfigurationProvider).</span></span> <span data-ttu-id="a96fa-188">구성 공급자는 비어 있는 데이터베이스를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-188">The configuration provider initializes the database when it's empty:</span></span>

[!code-csharp[](index/sample/CustomConfigurationProvider/EntityFrameworkConfigurationProvider.cs?highlight=9,18-31,38-39)]

<span data-ttu-id="a96fa-189">샘플이 실행되면 데이터베이스의 강조 표시된 값("value_from_ef_1" 및 "value_from_ef_2")이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-189">The highlighted values from the database ("value_from_ef_1" and "value_from_ef_2") are displayed when the sample is run.</span></span>

<span data-ttu-id="a96fa-190">구성 소스를 추가하기 위한 `EFConfigSource` 확장 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-190">An `EFConfigSource` extension method for adding the configuration source can be used:</span></span>

[!code-csharp[](index/sample/CustomConfigurationProvider/EntityFrameworkExtensions.cs?highlight=12)]

<span data-ttu-id="a96fa-191">다음 코드는 사용자 지정 `EFConfigProvider`를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-191">The following code shows how to use the custom `EFConfigProvider`:</span></span>

[!code-csharp[](index/sample/CustomConfigurationProvider/Program.cs?highlight=21-26)]

<span data-ttu-id="a96fa-192">이 샘플은 JSON 공급자 뒤에 사용자 지정 `EFConfigProvider`를 추가하므로 데이터베이스의 모든 설정이 *appsettings.json* 파일의 설정을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-192">Note the sample adds the custom `EFConfigProvider` after the JSON provider, so any settings from the database will override settings from the *appsettings.json* file.</span></span>

<span data-ttu-id="a96fa-193">다음 *appsettings.json* 파일 사용:</span><span class="sxs-lookup"><span data-stu-id="a96fa-193">Using the following *appsettings.json* file:</span></span>

[!code-json[](index/sample/CustomConfigurationProvider/appsettings.json)]

<span data-ttu-id="a96fa-194">다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-194">The following output is displayed:</span></span>

```console
key1=value_from_ef_1
key2=value_from_ef_2
key3=value_from_json_3
```

## <a name="commandline-configuration-provider"></a><span data-ttu-id="a96fa-195">CommandLine 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="a96fa-195">CommandLine configuration provider</span></span>

<span data-ttu-id="a96fa-196">[CommandLine 구성 공급자](/dotnet/api/microsoft.extensions.configuration.commandline.commandlineconfigurationprovider)는 런타임에 구성에 대한 명령줄 인수 키-값 쌍을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-196">The [CommandLine configuration provider](/dotnet/api/microsoft.extensions.configuration.commandline.commandlineconfigurationprovider) receives command-line argument key-value pairs for configuration at runtime.</span></span>

[<span data-ttu-id="a96fa-197">CommandLine 구성 샘플 살펴보기 또는 다운로드</span><span class="sxs-lookup"><span data-stu-id="a96fa-197">View or download the CommandLine configuration sample</span></span>](https://github.com/aspnet/docs/tree/master/aspnetcore/fundamentals/index/sample/CommandLine)

### <a name="setup-and-use-the-commandline-configuration-provider"></a><span data-ttu-id="a96fa-198">CommandLine 구성 공급자 설정 및 사용</span><span class="sxs-lookup"><span data-stu-id="a96fa-198">Setup and use the CommandLine configuration provider</span></span>

#### <a name="basic-configurationtabbasicconfiguration"></a>[<span data-ttu-id="a96fa-199">기본 구성</span><span class="sxs-lookup"><span data-stu-id="a96fa-199">Basic Configuration</span></span>](#tab/basicconfiguration/)
<span data-ttu-id="a96fa-200">명령줄 구성을 활성화하려면 [ConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.configurationbuilder) 인스턴스에서 `AddCommandLine` 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-200">To activate command-line configuration, call the `AddCommandLine` extension method on an instance of [ConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.configurationbuilder):</span></span>

[!code-csharp[](index/sample_snapshot//CommandLine/Program.cs?highlight=18,21)]

<span data-ttu-id="a96fa-201">코드를 실행하면 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-201">Running the code, the following output is displayed:</span></span>

```console
MachineName: MairaPC
Left: 1980
```

<span data-ttu-id="a96fa-202">명령줄에서 인수 키-값 쌍을 전달하면 `Profile:MachineName` 및 `App:MainWindow:Left` 값이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-202">Passing argument key-value pairs on the command line changes the values of `Profile:MachineName` and `App:MainWindow:Left`:</span></span>

```console
dotnet run Profile:MachineName=BartPC App:MainWindow:Left=1979
```

<span data-ttu-id="a96fa-203">콘솔 창에 다음 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-203">The console window displays:</span></span>

```console
MachineName: BartPC
Left: 1979
```

<span data-ttu-id="a96fa-204">다른 구성 공급자가 제공한 구성을 명령줄 구성으로 재정의하려면 `ConfigurationBuilder`의 마지막에서 `AddCommandLine`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-204">To override configuration provided by other configuration providers with command-line configuration, call `AddCommandLine` last on `ConfigurationBuilder`:</span></span>

[!code-csharp[](index/sample_snapshot//CommandLine/Program2.cs?range=11-16&highlight=1,5)]

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="a96fa-205">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="a96fa-205">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)
<span data-ttu-id="a96fa-206">일반적인 ASP.NET Core 2.x 앱은 고정적인 편의 메서드를 사용하여 `CreateDefaultBuilder`를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-206">Typical ASP.NET Core 2.x apps use the static convenience method `CreateDefaultBuilder` to build the host:</span></span>

[!code-csharp[](index/sample_snapshot//Program.cs?highlight=12)]

<span data-ttu-id="a96fa-207">`CreateDefaultBuilder`는 *appsettings.json*, *appsettings.{Environment}.json*, [사용자 비밀](xref:security/app-secrets)(`Development` 환경의 경우), 환경 변수 및 명령줄 인수에서 선택적 구성을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-207">`CreateDefaultBuilder` loads optional configuration from *appsettings.json*, *appsettings.{Environment}.json*, [user secrets](xref:security/app-secrets) (in the `Development` environment), environment variables, and command-line arguments.</span></span> <span data-ttu-id="a96fa-208">CommandLine 구성 공급자는 마지막에 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-208">The CommandLine configuration provider is called last.</span></span> <span data-ttu-id="a96fa-209">공급자가 마지막에 호출되기 때문에 다른 구성 공급자가 이전에 설정한 구성을 런타임에 전달되는 명령줄 인수가 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-209">Calling the provider last allows the command-line arguments passed at runtime to override configuration set by the other configuration providers called earlier.</span></span>

<span data-ttu-id="a96fa-210">*appsettings* 파일에는</span><span class="sxs-lookup"><span data-stu-id="a96fa-210">For *appsettings* files where:</span></span>

* <span data-ttu-id="a96fa-211">`reloadOnChange`가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-211">`reloadOnChange` is enabled.</span></span>
* <span data-ttu-id="a96fa-212">명령줄 인수와 *appsettings* 파일에 동일한 설정을 포함하세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-212">Contain the same setting in the command-line arguments and an *appsettings* file.</span></span>
* <span data-ttu-id="a96fa-213">일치하는 명령줄 인수가 포함된 *appsettings* 파일은 앱이 시작된 후 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-213">The *appsettings* file containing the matching command-line argument is changed after the app starts.</span></span>

<span data-ttu-id="a96fa-214">이전 조건이 모두 참인 경우 명령줄 인수가 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-214">If all the preceding conditions are true, the command-line arguments are overridden.</span></span>

<span data-ttu-id="a96fa-215">ASP.NET Core 2.x 앱은 `CreateDefaultBuilder` 대신 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-215">ASP.NET Core 2.x app can use [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) instead of `CreateDefaultBuilder`.</span></span> <span data-ttu-id="a96fa-216">`WebHostBuilder`를 사용하는 경우 [ConfigurationBuilder](/api/microsoft.extensions.configuration.configurationbuilder)를 사용하여 수동으로 구성을 설정하세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-216">When using `WebHostBuilder`, manually set configuration with [ConfigurationBuilder](/api/microsoft.extensions.configuration.configurationbuilder).</span></span> <span data-ttu-id="a96fa-217">자세한 내용은 ASP.NET Core 1.x 탭을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-217">See the ASP.NET Core 1.x tab for more information.</span></span>

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="a96fa-218">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="a96fa-218">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)
<span data-ttu-id="a96fa-219">[ConfigurationBuilder](/api/microsoft.extensions.configuration.configurationbuilder)를 만들고 `AddCommandLine` 메서드를 호출하여 CommandLine 구성 공급자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-219">Create a [ConfigurationBuilder](/api/microsoft.extensions.configuration.configurationbuilder) and call the `AddCommandLine` method to use the CommandLine configuration provider.</span></span> <span data-ttu-id="a96fa-220">공급자가 마지막에 호출되기 때문에 다른 구성 공급자가 이전에 설정한 구성을 런타임에 전달되는 명령줄 인수가 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-220">Calling the provider last allows the command-line arguments passed at runtime to override configuration set by the other configuration providers called earlier.</span></span> <span data-ttu-id="a96fa-221">`UseConfiguration` 메서드를 사용하여 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)에 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-221">Apply the configuration to [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) with the `UseConfiguration` method:</span></span>

[!code-csharp[](index/sample_snapshot//CommandLine/Program2.cs?highlight=11,15,19)]

* * *
### <a name="arguments"></a><span data-ttu-id="a96fa-222">인수</span><span class="sxs-lookup"><span data-stu-id="a96fa-222">Arguments</span></span>

<span data-ttu-id="a96fa-223">명령줄에 전달된 인수는 다음 표에 표시된 두 형식 중 하나를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-223">Arguments passed on the command line must conform to one of two formats shown in the following table:</span></span>

| <span data-ttu-id="a96fa-224">인수 형식</span><span class="sxs-lookup"><span data-stu-id="a96fa-224">Argument format</span></span>                                                     | <span data-ttu-id="a96fa-225">예</span><span class="sxs-lookup"><span data-stu-id="a96fa-225">Example</span></span>        |
| ------------------------------------------------------------------- | :------------: |
| <span data-ttu-id="a96fa-226">단일 인수: 등호로 구분되는 키-값 쌍(`=`)</span><span class="sxs-lookup"><span data-stu-id="a96fa-226">Single argument: a key-value pair separated by an equals sign (`=`)</span></span> | `key1=value`   |
| <span data-ttu-id="a96fa-227">두 인수 시퀀스: 공백으로 구분되는 키-값 쌍</span><span class="sxs-lookup"><span data-stu-id="a96fa-227">Sequence of two arguments: a key-value pair separated by a space</span></span>    | `/key1 value1` |

<span data-ttu-id="a96fa-228">**단일 인수**</span><span class="sxs-lookup"><span data-stu-id="a96fa-228">**Single argument**</span></span>

<span data-ttu-id="a96fa-229">값이 등호를 따라야 합니다(`=`).</span><span class="sxs-lookup"><span data-stu-id="a96fa-229">The value must follow an equals sign (`=`).</span></span> <span data-ttu-id="a96fa-230">값이 null일 수 있습니다(예: `mykey=`).</span><span class="sxs-lookup"><span data-stu-id="a96fa-230">The value can be null (for example, `mykey=`).</span></span>

<span data-ttu-id="a96fa-231">키에 접두사가 붙을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-231">The key may have a prefix.</span></span>

| <span data-ttu-id="a96fa-232">키 접두사</span><span class="sxs-lookup"><span data-stu-id="a96fa-232">Key prefix</span></span>               | <span data-ttu-id="a96fa-233">예</span><span class="sxs-lookup"><span data-stu-id="a96fa-233">Example</span></span>         |
| ------------------------ | :-------------: |
| <span data-ttu-id="a96fa-234">접두사 없음</span><span class="sxs-lookup"><span data-stu-id="a96fa-234">No prefix</span></span>                | `key1=value1`   |
| <span data-ttu-id="a96fa-235">단일 대시(`-`)&#8224;</span><span class="sxs-lookup"><span data-stu-id="a96fa-235">Single dash (`-`)&#8224;</span></span> | `-key2=value2`  |
| <span data-ttu-id="a96fa-236">대시 2개(`--`)</span><span class="sxs-lookup"><span data-stu-id="a96fa-236">Two dashes (`--`)</span></span>        | `--key3=value3` |
| <span data-ttu-id="a96fa-237">슬래시(`/`)</span><span class="sxs-lookup"><span data-stu-id="a96fa-237">Forward slash (`/`)</span></span>      | `/key4=value4`  |

<span data-ttu-id="a96fa-238">&#8224;단일 대시 접두사(`-`)가 붙은 키는 아래에 설명된 [스위치 매핑](#switch-mappings)에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-238">&#8224;A key with a single dash prefix (`-`) must be provided in [switch mappings](#switch-mappings), described below.</span></span>

<span data-ttu-id="a96fa-239">예제 명령:</span><span class="sxs-lookup"><span data-stu-id="a96fa-239">Example command:</span></span>

```console
dotnet run key1=value1 -key2=value2 --key3=value3 /key4=value4
```

<span data-ttu-id="a96fa-240">참고: 구성 공급자에게 제공된 [스위치 매핑](#switch-mappings)에 `-key2`가 없으면 `FormatException`이 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-240">Note: If `-key2` isn't present in the [switch mappings](#switch-mappings) given to the configuration provider, a `FormatException` is thrown.</span></span>

<span data-ttu-id="a96fa-241">**두 인수 시퀀스**</span><span class="sxs-lookup"><span data-stu-id="a96fa-241">**Sequence of two arguments**</span></span>

<span data-ttu-id="a96fa-242">값이 null일 수 없으며 공백으로 구분되는 키를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-242">The value can't be null and must follow the key separated by a space.</span></span>

<span data-ttu-id="a96fa-243">키에 접두사가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-243">The key must have a prefix.</span></span>

| <span data-ttu-id="a96fa-244">키 접두사</span><span class="sxs-lookup"><span data-stu-id="a96fa-244">Key prefix</span></span>               | <span data-ttu-id="a96fa-245">예</span><span class="sxs-lookup"><span data-stu-id="a96fa-245">Example</span></span>         |
| ------------------------ | :-------------: |
| <span data-ttu-id="a96fa-246">단일 대시(`-`)&#8224;</span><span class="sxs-lookup"><span data-stu-id="a96fa-246">Single dash (`-`)&#8224;</span></span> | `-key1 value1`  |
| <span data-ttu-id="a96fa-247">대시 2개(`--`)</span><span class="sxs-lookup"><span data-stu-id="a96fa-247">Two dashes (`--`)</span></span>        | `--key2 value2` |
| <span data-ttu-id="a96fa-248">슬래시(`/`)</span><span class="sxs-lookup"><span data-stu-id="a96fa-248">Forward slash (`/`)</span></span>      | `/key3 value3`  |

<span data-ttu-id="a96fa-249">&#8224;단일 대시 접두사(`-`)가 붙은 키는 아래에 설명된 [스위치 매핑](#switch-mappings)에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-249">&#8224;A key with a single dash prefix (`-`) must be provided in [switch mappings](#switch-mappings), described below.</span></span>

<span data-ttu-id="a96fa-250">예제 명령:</span><span class="sxs-lookup"><span data-stu-id="a96fa-250">Example command:</span></span>

```console
dotnet run -key1 value1 --key2 value2 /key3 value3
```

<span data-ttu-id="a96fa-251">참고: 구성 공급자에게 제공된 [스위치 매핑](#switch-mappings)에 `-key1`가 없으면 `FormatException`이 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-251">Note: If `-key1` isn't present in the [switch mappings](#switch-mappings) given to the configuration provider, a `FormatException` is thrown.</span></span>

### <a name="duplicate-keys"></a><span data-ttu-id="a96fa-252">중복 키</span><span class="sxs-lookup"><span data-stu-id="a96fa-252">Duplicate keys</span></span>

<span data-ttu-id="a96fa-253">중복 키를 제공하면 마지막 키-값 쌍이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-253">If duplicate keys are provided, the last key-value pair is used.</span></span>

### <a name="switch-mappings"></a><span data-ttu-id="a96fa-254">스위치 매핑</span><span class="sxs-lookup"><span data-stu-id="a96fa-254">Switch mappings</span></span>

<span data-ttu-id="a96fa-255">`ConfigurationBuilder`를 사용하여 수동으로 구성을 빌드하는 경우 `AddCommandLine` 메서드에 스위치 매핑 사전을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-255">When manually building configuration with `ConfigurationBuilder`, a switch mappings dictionary can be added to the `AddCommandLine` method.</span></span> <span data-ttu-id="a96fa-256">스위치 매핑은 키 이름 교체 논리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-256">Switch mappings allow key name replacement logic.</span></span>

<span data-ttu-id="a96fa-257">스위치 매핑 사전을 사용하면 명령줄 인수를 통해 제공된 키와 일치하는 키에 대해 사전을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-257">When the switch mappings dictionary is used, the dictionary is checked for a key that matches the key provided by a command-line argument.</span></span> <span data-ttu-id="a96fa-258">사전에서 명령줄 키가 발견되면 사전 값(키 교체)이 다시 구성으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-258">If the command-line key is found in the dictionary, the dictionary value (the key replacement) is passed back to set the configuration.</span></span> <span data-ttu-id="a96fa-259">단일 대시(`-`) 접두사가 붙은 명령줄 키에는 스위치 매핑이 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-259">A switch mapping is required for any command-line key prefixed with a single dash (`-`).</span></span>

<span data-ttu-id="a96fa-260">스위치 매핑 사전 키 규칙:</span><span class="sxs-lookup"><span data-stu-id="a96fa-260">Switch mappings dictionary key rules:</span></span>

* <span data-ttu-id="a96fa-261">스위치는 단일 대시(`-`) 또는 이중 대시(`--`)로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-261">Switches must start with a dash (`-`) or double-dash (`--`).</span></span>
* <span data-ttu-id="a96fa-262">스위치 매핑 사전이 중복 키를 포함하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-262">The switch mappings dictionary must not contain duplicate keys.</span></span>

<span data-ttu-id="a96fa-263">다음 예제의 `GetSwitchMappings` 메서드는 명령줄 인수가 단일 대시(`-`) 키 접두사를 사용하고 선행 하위 키 접두사를 사용하지 않는 것을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-263">In the following example, the `GetSwitchMappings` method allows command-line arguments to use a single dash (`-`) key prefix and avoid leading subkey prefixes.</span></span>

[!code-csharp[](index/sample/CommandLine/Program.cs?highlight=10-19,32)]

<span data-ttu-id="a96fa-264">`AddInMemoryCollection`에 제공된 사전은 명령줄 인수를 제공하지 않고 구성 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-264">Without providing command-line arguments, the dictionary provided to `AddInMemoryCollection` sets the configuration values.</span></span> <span data-ttu-id="a96fa-265">다음 명령을 사용하여 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-265">Run the app with the following command:</span></span>

```console
dotnet run
```

<span data-ttu-id="a96fa-266">콘솔 창에 다음 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-266">The console window displays:</span></span>

```console
MachineName: RickPC
Left: 1980
```

<span data-ttu-id="a96fa-267">다음 명령을 사용하여 구성 설정을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-267">Use the following to pass in configuration settings:</span></span>

```console
dotnet run /Profile:MachineName=DahliaPC /App:MainWindow:Left=1984
```

<span data-ttu-id="a96fa-268">콘솔 창에 다음 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-268">The console window displays:</span></span>

```console
MachineName: DahliaPC
Left: 1984
```

<span data-ttu-id="a96fa-269">생성된 스위치 매핑 사전은 다음 표의 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-269">After the switch mappings dictionary is created, it contains the data shown in the following table:</span></span>

| <span data-ttu-id="a96fa-270">Key</span><span class="sxs-lookup"><span data-stu-id="a96fa-270">Key</span></span>            | <span data-ttu-id="a96fa-271">값</span><span class="sxs-lookup"><span data-stu-id="a96fa-271">Value</span></span>                 |
| -------------- | --------------------- |
| `-MachineName` | `Profile:MachineName` |
| `-Left`        | `App:MainWindow:Left` |

<span data-ttu-id="a96fa-272">사전을 사용하여 키 전환을 보여 주려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-272">To demonstrate key switching using the dictionary, run the following command:</span></span>

```console
dotnet run -MachineName=ChadPC -Left=1988
```

<span data-ttu-id="a96fa-273">명령줄 키가 교환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-273">The command-line keys are swapped.</span></span> <span data-ttu-id="a96fa-274">콘솔 창에 `Profile:MachineName` 및 `App:MainWindow:Left`의 구성 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-274">The console window displays the configuration values for `Profile:MachineName` and `App:MainWindow:Left`:</span></span>

```console
MachineName: ChadPC
Left: 1988
```

## <a name="webconfig-file"></a><span data-ttu-id="a96fa-275">web.config 파일</span><span class="sxs-lookup"><span data-stu-id="a96fa-275">web.config file</span></span>

<span data-ttu-id="a96fa-276">IIS 또는 IIS Express에서 앱을 호스트하는 경우 *web.config* 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-276">A *web.config* file is required when hosting the app in IIS or IIS Express.</span></span> <span data-ttu-id="a96fa-277">*web.config*의 설정은 IIS의 [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module)이 앱을 시작하고 다른 IIS 설정 및 모듈을 구성할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-277">Settings in *web.config* enable the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) to launch the app and configure other IIS settings and modules.</span></span> <span data-ttu-id="a96fa-278">*web.config* 파일이 없고 프로젝트 파일에 `<Project Sdk="Microsoft.NET.Sdk.Web">`이 포함되어 있는 경우 프로젝트를 게시하면 게시된 출력에 *web.config* 파일이 만들어집니다(*게시* 폴더).</span><span class="sxs-lookup"><span data-stu-id="a96fa-278">If the *web.config* file isn't present and the project file includes `<Project Sdk="Microsoft.NET.Sdk.Web">`, publishing the project creates a *web.config* file in the published output (the *publish* folder).</span></span> <span data-ttu-id="a96fa-279">자세한 내용은 [IIS가 있는 Windows에서 ASP.NET Core 호스팅](xref:host-and-deploy/iis/index#webconfig-file)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-279">For more information, see [Host ASP.NET Core on Windows with IIS](xref:host-and-deploy/iis/index#webconfig-file).</span></span>

## <a name="access-configuration-during-startup"></a><span data-ttu-id="a96fa-280">시작하는 동안 구성에 액세스</span><span class="sxs-lookup"><span data-stu-id="a96fa-280">Access configuration during startup</span></span>

<span data-ttu-id="a96fa-281">시작하는 동안 `ConfigureServices` 또는 `Configure` 내에서 구성에 액세스하려면 [응용 프로그램 시작](xref:fundamentals/startup) 항목의 예를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-281">To access configuration within `ConfigureServices` or `Configure` during startup, see the examples in the [Application startup](xref:fundamentals/startup) topic.</span></span>

## <a name="adding-configuration-from-an-external-assembly"></a><span data-ttu-id="a96fa-282">외부 어셈블리의 구성 추가</span><span class="sxs-lookup"><span data-stu-id="a96fa-282">Adding configuration from an external assembly</span></span>

<span data-ttu-id="a96fa-283">[IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) 구현에서는 시작 시 앱의 `Startup` 클래스 외부에 있는 외부 어셈블리에서 앱에 향상된 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-283">An [IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) implementation allows adding enhancements to an app at startup from an external assembly outside of the app's `Startup` class.</span></span> <span data-ttu-id="a96fa-284">자세한 내용은 [외부 어셈블리에서 앱 강화](xref:fundamentals/configuration/platform-specific-configuration)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-284">For more information, see [Enhance an app from an external assembly](xref:fundamentals/configuration/platform-specific-configuration).</span></span>

## <a name="access-configuration-in-a-razor-page-or-mvc-view"></a><span data-ttu-id="a96fa-285">Razor 페이지 또는 MVC 뷰에서 구성에 액세스</span><span class="sxs-lookup"><span data-stu-id="a96fa-285">Access configuration in a Razor Page or MVC view</span></span>

<span data-ttu-id="a96fa-286">Razor 페이지나 MVC 뷰의 구성 설정에 액세스하려면 [Microsoft.Extensions.Configuration 네임스페이스](/dotnet/api/microsoft.extensions.configuration)에 [using 지시문](xref:mvc/views/razor#using)([C# 참조: using 지시문](/dotnet/csharp/language-reference/keywords/using-directive))을 추가하고 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)을 페이지 또는 뷰로 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-286">To access configuration settings in a Razor Pages page or an MVC view, add a [using directive](xref:mvc/views/razor#using) ([C# reference: using directive](/dotnet/csharp/language-reference/keywords/using-directive)) for the [Microsoft.Extensions.Configuration namespace](/dotnet/api/microsoft.extensions.configuration) and inject [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) into the page or view.</span></span>

<span data-ttu-id="a96fa-287">Razor 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="a96fa-287">In a Razor Pages page:</span></span>

```cshtml
@page
@model IndexModel

@using Microsoft.Extensions.Configuration
@inject IConfiguration Configuration

<!DOCTYPE html>
<html lang="en">
<head>
    <title>Index Page</title>
</head>
<body>
    <h1>Access configuration in a Razor Pages page</h1>
    <p>Configuration[&quot;key&quot;]: @Configuration["key"]</p>
</body>
</html>
```

<span data-ttu-id="a96fa-288">MVC 뷰에서:</span><span class="sxs-lookup"><span data-stu-id="a96fa-288">In an MVC view:</span></span>

```cshtml
@using Microsoft.Extensions.Configuration
@inject IConfiguration Configuration

<!DOCTYPE html>
<html lang="en">
<head>
    <title>Index View</title>
</head>
<body>
    <h1>Access configuration in an MVC view</h1>
    <p>Configuration[&quot;key&quot;]: @Configuration["key"]</p>
</body>
</html>
```

## <a name="additional-notes"></a><span data-ttu-id="a96fa-289">추가 참고 사항</span><span class="sxs-lookup"><span data-stu-id="a96fa-289">Additional notes</span></span>

* <span data-ttu-id="a96fa-290">`ConfigureServices`가 호출되기 전에는 DI(종속성 주입)가 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-290">Dependency Injection (DI) isn't set up until after `ConfigureServices` is invoked.</span></span>
* <span data-ttu-id="a96fa-291">구성 시스템에서 DI를 인식하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-291">The configuration system isn't DI aware.</span></span>
* <span data-ttu-id="a96fa-292">`IConfiguration`에는 두 가지 특수화가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-292">`IConfiguration` has two specializations:</span></span>
  * <span data-ttu-id="a96fa-293">`IConfigurationRoot`는 루트 노드에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-293">`IConfigurationRoot` Used for the root node.</span></span> <span data-ttu-id="a96fa-294">다시 로드를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-294">Can trigger a reload.</span></span>
  * <span data-ttu-id="a96fa-295">`IConfigurationSection`은 구성 값의 섹션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-295">`IConfigurationSection` Represents a section of configuration values.</span></span> <span data-ttu-id="a96fa-296">`GetSection` 및 `GetChildren` 메서드는 `IConfigurationSection`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-296">The `GetSection` and `GetChildren` methods return an `IConfigurationSection`.</span></span>
  * <span data-ttu-id="a96fa-297">구성을 다시 로드하는 경우 또는 각 공급자에 액세스하는 경우 [IConfigurationRoot](/dotnet/api/microsoft.extensions.configuration.iconfigurationroot)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="a96fa-297">Use [IConfigurationRoot](/dotnet/api/microsoft.extensions.configuration.iconfigurationroot) when reloading configuration or for access to each provider.</span></span> <span data-ttu-id="a96fa-298">이러한 상황은 일반적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a96fa-298">Neither of these situations are common.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a96fa-299">추가 자료</span><span class="sxs-lookup"><span data-stu-id="a96fa-299">Additional resources</span></span>

* [<span data-ttu-id="a96fa-300">옵션</span><span class="sxs-lookup"><span data-stu-id="a96fa-300">Options</span></span>](xref:fundamentals/configuration/options)
* [<span data-ttu-id="a96fa-301">여러 환경 사용</span><span class="sxs-lookup"><span data-stu-id="a96fa-301">Use multiple environments</span></span>](xref:fundamentals/environments)
* [<span data-ttu-id="a96fa-302">개발 중인 안전한 앱 비밀 저장소</span><span class="sxs-lookup"><span data-stu-id="a96fa-302">Safe storage of app secrets in development</span></span>](xref:security/app-secrets)
* [<span data-ttu-id="a96fa-303">ASP.NET Core에서 호스팅</span><span class="sxs-lookup"><span data-stu-id="a96fa-303">Hosting in ASP.NET Core</span></span>](xref:fundamentals/hosting)
* [<span data-ttu-id="a96fa-304">종속성 주입</span><span class="sxs-lookup"><span data-stu-id="a96fa-304">Dependency Injection</span></span>](xref:fundamentals/dependency-injection)
* [<span data-ttu-id="a96fa-305">Azure Key Vault 구성 공급자</span><span class="sxs-lookup"><span data-stu-id="a96fa-305">Azure Key Vault configuration provider</span></span>](xref:security/key-vault-configuration)
