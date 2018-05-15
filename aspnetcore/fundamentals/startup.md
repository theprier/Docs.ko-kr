---
title: ASP.NET Core에서 응용 프로그램 시작
author: ardalis
description: ASP.NET Core의 시작 클래스에서 서비스 및 앱의 요청 파이프라인을 구성하는 방법을 알아봅니다.
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 4/13/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/startup
ms.openlocfilehash: 8dd632a2c888e65c6420e0fed7acf6fa15173b3d
ms.sourcegitcommit: c4a31aaf902f2e84aaf4a9d882ca980fdf6488c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2018
---
# <a name="application-startup-in-aspnet-core"></a><span data-ttu-id="1ed4b-103">ASP.NET Core에서 응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="1ed4b-103">Application startup in ASP.NET Core</span></span>

<span data-ttu-id="1ed4b-104">작성자: [Steve Smith](https://ardalis.com), [Tom Dykstra](https://github.com/tdykstra) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="1ed4b-104">By [Steve Smith](https://ardalis.com), [Tom Dykstra](https://github.com/tdykstra), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="1ed4b-105">`Startup` 클래스는 서비스 및 앱의 요청 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-105">The `Startup` class configures services and the app's request pipeline.</span></span>

## <a name="the-startup-class"></a><span data-ttu-id="1ed4b-106">시작 클래스</span><span class="sxs-lookup"><span data-stu-id="1ed4b-106">The Startup class</span></span>

<span data-ttu-id="1ed4b-107">ASP.NET Core 앱은 규칙에 따라 `Startup`으로 이름이 지정된 `Startup` 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-107">ASP.NET Core apps use a `Startup` class, which is named `Startup` by convention.</span></span> <span data-ttu-id="1ed4b-108">`Startup` 클래스:</span><span class="sxs-lookup"><span data-stu-id="1ed4b-108">The `Startup` class:</span></span>

* <span data-ttu-id="1ed4b-109">선택적으로 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 메서드를 포함하여 앱의 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-109">Can optionally include a [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) method to configure the app's services.</span></span>
* <span data-ttu-id="1ed4b-110">[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 메서드를 포함하여 앱의 요청 처리 파이프라인을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-110">Must include a [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) method to create the app's request processing pipeline.</span></span>

<span data-ttu-id="1ed4b-111">`ConfigureServices` 및 `Configure`는 앱 시작 시 런타임에 의해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-111">`ConfigureServices` and `Configure` are called by the runtime when the app starts:</span></span>

[!code-csharp[](startup/snapshot_sample/Startup1.cs)]

<span data-ttu-id="1ed4b-112">[WebHostBuilderExtensions](/dotnet/api/Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions) [UseStartup&lt;TStartup&gt;](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 메서드로 `Startup` 클래스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-112">Specify the `Startup` class with the [WebHostBuilderExtensions](/dotnet/api/Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions) [UseStartup&lt;TStartup&gt;](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) method:</span></span>

[!code-csharp[](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main&highlight=10)]

<span data-ttu-id="1ed4b-113">`Startup` 클래스 생성자는 호스트에 의해 정의된 종속성을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-113">The `Startup` class constructor accepts dependencies defined by the host.</span></span> <span data-ttu-id="1ed4b-114">`Startup` 클래스에 대한 [종속성 주입](xref:fundamentals/dependency-injection)의 일반적인 용도는 다음을 삽입하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-114">A common use of [dependency injection](xref:fundamentals/dependency-injection) into the `Startup` class is to inject:</span></span>

* <span data-ttu-id="1ed4b-115">환경에서 서비스를 구성하는 [IHostingEnvironment](/dotnet/api/Microsoft.AspNetCore.Hosting.IHostingEnvironment)</span><span class="sxs-lookup"><span data-stu-id="1ed4b-115">[IHostingEnvironment](/dotnet/api/Microsoft.AspNetCore.Hosting.IHostingEnvironment) to configure services by environment.</span></span>
* <span data-ttu-id="1ed4b-116">시작하는 동안 앱을 구성하는 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)</span><span class="sxs-lookup"><span data-stu-id="1ed4b-116">[IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) to configure the app during startup.</span></span>

[!code-csharp[](startup/snapshot_sample/Startup2.cs)]

<span data-ttu-id="1ed4b-117">`IHostingEnvironment` 삽입의 대안은 규칙 기반 접근 방식을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-117">An alternative to injecting `IHostingEnvironment` is to use a conventions-based approach.</span></span> <span data-ttu-id="1ed4b-118">앱은 다양한 환경(예: `StartupDevelopment`)에 대한 별도의 `Startup` 클래스를 정의할 수 있으며 적절한 시작 클래스는 런타임에 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-118">The app can define separate `Startup` classes for different environments (for example, `StartupDevelopment`), and the appropriate startup class is selected at runtime.</span></span> <span data-ttu-id="1ed4b-119">해당 이름 접미사가 현재 환경과 일치하는 클래스에 우선 순위가 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-119">The class whose name suffix matches the current environment is prioritized.</span></span> <span data-ttu-id="1ed4b-120">앱이 개발 환경에서 실행되고 `Startup` 클래스 및 `StartupDevelopment` 클래스 모두를 포함하는 경우 `StartupDevelopment` 클래스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-120">If the app is run in the Development environment and includes both a `Startup` class and a `StartupDevelopment` class, the `StartupDevelopment` class is used.</span></span> <span data-ttu-id="1ed4b-121">자세한 내용은 [여러 환경 사용](xref:fundamentals/environments#startup-conventions)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-121">For more information, see [Work with multiple environments](xref:fundamentals/environments#startup-conventions).</span></span>

<span data-ttu-id="1ed4b-122">`WebHostBuilder`에 대한 자세한 내용은 [호스팅](xref:fundamentals/hosting) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-122">To learn more about `WebHostBuilder`, see the [Hosting](xref:fundamentals/hosting) topic.</span></span> <span data-ttu-id="1ed4b-123">시작하는 동안 오류를 처리하는 방법은 [시작 예외 처리](xref:fundamentals/error-handling#startup-exception-handling)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-123">For information on handling errors during startup, see [Startup exception handling](xref:fundamentals/error-handling#startup-exception-handling).</span></span>

## <a name="the-configureservices-method"></a><span data-ttu-id="1ed4b-124">ConfigureServices 메서드</span><span class="sxs-lookup"><span data-stu-id="1ed4b-124">The ConfigureServices method</span></span>

<span data-ttu-id="1ed4b-125">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 메서드는</span><span class="sxs-lookup"><span data-stu-id="1ed4b-125">The [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) method is:</span></span>

* <span data-ttu-id="1ed4b-126">Optional</span><span class="sxs-lookup"><span data-stu-id="1ed4b-126">Optional</span></span>
* <span data-ttu-id="1ed4b-127">`Configure` 메서드 전에 웹 호스트에 의해 호출되어 앱의 서비스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-127">Called by the web host before the `Configure` method to configure the app's services.</span></span>
* <span data-ttu-id="1ed4b-128">여기서 [구성 옵션](xref:fundamentals/configuration/index)은 규칙에 의해 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-128">Where [configuration options](xref:fundamentals/configuration/index) are set by convention.</span></span>

<span data-ttu-id="1ed4b-129">서비스 컨테이너에 서비스를 추가하면 앱 내 및 `Configure` 메서드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-129">Adding services to the service container makes them available within the app and in the `Configure` method.</span></span> <span data-ttu-id="1ed4b-130">서비스는 [종속성 주입](xref:fundamentals/dependency-injection)을 통해 또는 [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices)에서 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-130">The services are resolved via [dependency injection](xref:fundamentals/dependency-injection) or from [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices).</span></span>

<span data-ttu-id="1ed4b-131">웹 호스트는 `Startup` 메서드가 호출되기 전에 일부 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-131">The web host may configure some services before `Startup` methods are called.</span></span> <span data-ttu-id="1ed4b-132">세부 정보는 [호스팅](xref:fundamentals/hosting) 항목에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-132">Details are available in the [Hosting](xref:fundamentals/hosting) topic.</span></span>

<span data-ttu-id="1ed4b-133">대부분의 설치가 필요한 기능의 경우 [IServiceCollection](/dotnet/api/Microsoft.Extensions.DependencyInjection.IServiceCollection)에 `Add[Service]` 확장 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-133">For features that require substantial setup, there are `Add[Service]` extension methods on [IServiceCollection](/dotnet/api/Microsoft.Extensions.DependencyInjection.IServiceCollection).</span></span> <span data-ttu-id="1ed4b-134">일반적인 웹앱은 Entity Framework, ID 및 MVC에 대한 서비스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-134">A typical web app registers services for Entity Framework, Identity, and MVC:</span></span>

[!code-csharp[](../common/samples/WebApplication1/Startup.cs?highlight=4,7,11&start=40&end=55)]

::: moniker range=">= aspnetcore-2.1" 

<a name="setcompatibilityversion"></a>
### <a name="setcompatibilityversion-for-aspnet-core-mvc"></a><span data-ttu-id="1ed4b-135">ASP.NET Core MVC용 SetCompatibilityVersion</span><span class="sxs-lookup"><span data-stu-id="1ed4b-135">SetCompatibilityVersion for ASP.NET Core MVC</span></span> 

<span data-ttu-id="1ed4b-136">`SetCompatibilityVersion` 메서드를 사용하면 ASP.NET MVC Core 2.1+에서 도입된 주요 동작 변경 내용을 앱이 옵트인(opt-in) 또는 옵트아웃(opt-out)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-136">The `SetCompatibilityVersion` method allows an app to opt-in or opt-out of potentially breaking behavior changes introduced in ASP.NET MVC Core 2.1+.</span></span> <span data-ttu-id="1ed4b-137">이 주요 동작 변경 내용은 일반적으로 MVC 하위 시스템의 작동 방식과 런타임에서 **코드**를 호출하는 방법과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-137">These potentially breaking behavior changes are generally in how the MVC subsystem behaves and how **your code** is called by the runtime.</span></span> <span data-ttu-id="1ed4b-138">옵트인을 하면 ASP.NET Core의 최신 동작과 장기 동작을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-138">By opting in, you get the latest behavior, and the long-term behavior of ASP.NET Core.</span></span>

<span data-ttu-id="1ed4b-139">다음 코드는 호환성 모드를 ASP.NET Core 2.1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-139">The following code sets the compatibility mode to ASP.NET Core 2.1:</span></span>

<span data-ttu-id="1ed4b-140">[!code-csharp[Main](startup/sampleCompatibility/Startup.cs?name=snippet1)]</span><span class="sxs-lookup"><span data-stu-id="1ed4b-140">[!code-csharp[Main](startup/sampleCompatibility/Startup.cs?name=snippet1)]</span></span>

<span data-ttu-id="1ed4b-141">최신 버전(`CompatibilityVersion.Version_2_1`)을 사용하여 응용 프로그램을 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-141">We recommend you test your application using the latest version (`CompatibilityVersion.Version_2_1`).</span></span> <span data-ttu-id="1ed4b-142">대부분의 응용 프로그램은 최신 버전을 사용하여 주요 동작을 변경하지 않을 것으로 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-142">We anticipate that most applications will not have breaking behavior changes using the latest version.</span></span> 

<span data-ttu-id="1ed4b-143">`SetCompatibilityVersion(CompatibilityVersion.Version_2_0)`을 호출하는 응용 프로그램은 ASP.NET Core 2.1 MVC 및 이후의 2.x 버전에서 도입된 주요 동작 변경으로부터 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-143">Applications that call `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)` are protected from potentially breaking behavior changes introduced in the ASP.NET Core 2.1 MVC and later 2.x versions.</span></span> <span data-ttu-id="1ed4b-144">이 보호:</span><span class="sxs-lookup"><span data-stu-id="1ed4b-144">This protection:</span></span>

* <span data-ttu-id="1ed4b-145">2.1 이상의 모든 변경 내용에 적용되지는 않으며, MVC 하위 시스템의 주요 ASP.NET Core 런타임 동작 변경을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-145">Does not apply to all 2.1 and later changes, it's targeted to potentially breaking ASP.NET Core runtime behavior changes in the MVC subsystem.</span></span>
* <span data-ttu-id="1ed4b-146">다음의 주 버전으로 확장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-146">Does not extend to the next major version.</span></span>

<span data-ttu-id="1ed4b-147">`SetCompatibilityVersion`을 호출하지 **않는** ASP.NET Core 2.1 및 이후 2.x 응용 프로그램의 기본 호환성은 2.0 호환성입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-147">The default compatibility for ASP.NET Core 2.1 and later 2.x applications that do **not** call `SetCompatibilityVersion` is 2.0 compatibility.</span></span> <span data-ttu-id="1ed4b-148">즉, `SetCompatibilityVersion`을 호출하지 않는 것은 `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)`을 호출하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-148">That is, not calling `SetCompatibilityVersion` is the same as calling `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)`.</span></span>

<span data-ttu-id="1ed4b-149">다음 코드는 다음 동작을 제외하고, 호환성 모드를 ASP.NET Core 2.1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-149">The following code sets the compatibility mode to ASP.NET Core 2.1, except for the following behaviors:</span></span>

* [<span data-ttu-id="1ed4b-150">AllowCombiningAuthorizeFilters</span><span class="sxs-lookup"><span data-stu-id="1ed4b-150">AllowCombiningAuthorizeFilters</span></span>](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.Core/MvcOptions.cs)
* [<span data-ttu-id="1ed4b-151">InputFormatterExceptionPolicy</span><span class="sxs-lookup"><span data-stu-id="1ed4b-151">InputFormatterExceptionPolicy</span></span>](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.Core/MvcOptions.cs)

<span data-ttu-id="1ed4b-152">[!code-csharp[Main](startup/sampleCompatibility/Startup2.cs?name=snippet1)]</span><span class="sxs-lookup"><span data-stu-id="1ed4b-152">[!code-csharp[Main](startup/sampleCompatibility/Startup2.cs?name=snippet1)]</span></span>

<span data-ttu-id="1ed4b-153">적절한 호환성 스위치를 사용하여 주요 동작 변경 내용이 발생하는 앱의 경우:</span><span class="sxs-lookup"><span data-stu-id="1ed4b-153">For apps that encounter breaking behavior changes, using the appropriate compatibility switches:</span></span>

* <span data-ttu-id="1ed4b-154">최신 릴리스를 사용하고 특정 주요 동작 변경 내용을 옵트아웃(opt out)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-154">Allows you to use the latest release and opt out of specific breaking behavior changes.</span></span>
* <span data-ttu-id="1ed4b-155">최신 변경 내용과 함께 작동하도록 앱을 업데이트할 시간을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-155">Gives you time to update your app so it works with the latest changes.</span></span>

<span data-ttu-id="1ed4b-156">[MvcOptions](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.Core/MvcOptions.cs) 클래스 소스 주석에는 변경된 내용과 변경 내용이 대부분의 사용자에게 향상된 기능인 이유가 잘 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-156">The [MvcOptions](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.Core/MvcOptions.cs) class source comments have a good explanation of what changed and why the changes are an improvement for most users.</span></span>

<span data-ttu-id="1ed4b-157">이후에 [ASP.NET Core 3.0 버전](https://github.com/aspnet/Home/wiki/Roadmap)이 나올 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-157">At some future date, there will be an [ASP.NET Core 3.0 version](https://github.com/aspnet/Home/wiki/Roadmap).</span></span> <span data-ttu-id="1ed4b-158">호환성 스위치가 지원하는 이전 동작은 3.0 버전에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-158">Old behaviors supported by compatibility switches will be removed in the 3.0 version.</span></span> <span data-ttu-id="1ed4b-159">거의 모든 사용자에게 혜택을 주는 긍정적인 변화라고 생각합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-159">We feel these are positive changes benefitting nearly all users.</span></span> <span data-ttu-id="1ed4b-160">이제 이러한 변경 내용을 도입함으로써 대부분의 앱이 혜택을 받을 수 있으며, 다른 사람은 응용 프로그램을 업데이트할 시간을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-160">By introducing these changes now, most apps can benefit now, and the others will have time to update their applications.</span></span>

::: moniker-end

## <a name="services-available-in-startup"></a><span data-ttu-id="1ed4b-161">시작 시 사용할 수 있는 서비스</span><span class="sxs-lookup"><span data-stu-id="1ed4b-161">Services available in Startup</span></span>

<span data-ttu-id="1ed4b-162">웹 호스트는 `Startup` 클래스 생성자에 사용할 수 있는 몇 가지 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-162">The web host provides some services that are available to the `Startup` class constructor.</span></span> <span data-ttu-id="1ed4b-163">앱은 `ConfigureServices`를 통해 추가 서비스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-163">The app adds additional services via `ConfigureServices`.</span></span> <span data-ttu-id="1ed4b-164">그러면 호스트와 앱 서비스 모두는 `Configure` 및 응용 프로그램 전체에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-164">Both the host and app services are then available in `Configure` and throughout the application.</span></span>

## <a name="the-configure-method"></a><span data-ttu-id="1ed4b-165">Configure 메서드</span><span class="sxs-lookup"><span data-stu-id="1ed4b-165">The Configure method</span></span>

<span data-ttu-id="1ed4b-166">[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 메서드는 앱이 HTTP 요청에 응답하는 방식을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-166">The [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) method is used to specify how the app responds to HTTP requests.</span></span> <span data-ttu-id="1ed4b-167">요청 파이프라인은 [미들웨어](xref:fundamentals/middleware/index) 구성 요소를 [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) 인스턴스에 추가하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-167">The request pipeline is configured by adding [middleware](xref:fundamentals/middleware/index) components to an [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) instance.</span></span> <span data-ttu-id="1ed4b-168">`IApplicationBuilder`는 `Configure` 메서드에 사용할 수 있지만 서비스 컨테이너에 등록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-168">`IApplicationBuilder` is available to the `Configure` method, but it isn't registered in the service container.</span></span> <span data-ttu-id="1ed4b-169">호스팅은 `IApplicationBuilder`를 만들고 `Configure`에 직접 전달합니다([참조 원본](https://github.com/aspnet/Hosting/blob/release/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/WebHost.cs#L179-L192)).</span><span class="sxs-lookup"><span data-stu-id="1ed4b-169">Hosting creates an `IApplicationBuilder` and passes it directly to `Configure` ([reference source](https://github.com/aspnet/Hosting/blob/release/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/WebHost.cs#L179-L192)).</span></span>

<span data-ttu-id="1ed4b-170">[ASP.NET Core 템플릿](/dotnet/core/tools/dotnet-new)은 개발자 예외 페이지, [BrowserLink](http://vswebessentials.com/features/browserlink), 오류 페이지, 정적 파일 및 ASP.NET MVC에 대한 지원으로 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-170">The [ASP.NET Core templates](/dotnet/core/tools/dotnet-new) configure the pipeline with support for a developer exception page, [BrowserLink](http://vswebessentials.com/features/browserlink), error pages, static files, and ASP.NET MVC:</span></span>

[!code-csharp[](../common/samples/WebApplication1DotNetCore2.0App/Startup.cs?range=28-48&highlight=5,6,10,13,15)]

<span data-ttu-id="1ed4b-171">각 `Use` 확장 메서드는 요청 파이프라인에 미들웨어 구성 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-171">Each `Use` extension method adds a middleware component to the request pipeline.</span></span> <span data-ttu-id="1ed4b-172">예를 들어 `UseMvc` 확장 메서드는 [라우팅 미들웨어](xref:fundamentals/routing)를 요청 파이프라인에 추가하고 기본 처리기로 [MVC](xref:mvc/overview)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-172">For instance, the `UseMvc` extension method adds the [Routing Middleware](xref:fundamentals/routing) to the request pipeline and configures [MVC](xref:mvc/overview) as the default handler.</span></span>

<span data-ttu-id="1ed4b-173">요청 파이프라인의 각 미들웨어 구성 요소는 파이프라인의 다음 구성 요소를 호출하거나 적절한 경우 체인을 단락(short-circuiting)하는 일을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-173">Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline or short-circuiting the chain, if appropriate.</span></span> <span data-ttu-id="1ed4b-174">미들웨어 체인을 따라 단락(short-circuiting)이 발생하지 않으면, 각 미들웨어는 클라이언트에 전송되기 전에 요청을 처리할 수 있는 두 번째 기회를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-174">If short-circuiting doesn't occur along the middleware chain, each middleware has a second chance to process the request before it's sent to the client.</span></span>

<span data-ttu-id="1ed4b-175">`IHostingEnvironment` 및 `ILoggerFactory`와 같은 추가 서비스는 메서드 서명에서 지정될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-175">Additional services, such as `IHostingEnvironment` and `ILoggerFactory`, may also be specified in the method signature.</span></span> <span data-ttu-id="1ed4b-176">지정되면 사용 가능한 경우 추가 서비스가 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-176">When specified, additional services are injected if they're available.</span></span>

<span data-ttu-id="1ed4b-177">`IApplicationBuilder`를 사용하는 방법 및 미들웨어 처리 순서에 대한 자세한 내용은 [미들웨어](xref:fundamentals/middleware/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-177">For more information on how to use `IApplicationBuilder` and the order of middleware processing, see [Middleware](xref:fundamentals/middleware/index).</span></span>

## <a name="convenience-methods"></a><span data-ttu-id="1ed4b-178">편리한 메서드</span><span class="sxs-lookup"><span data-stu-id="1ed4b-178">Convenience methods</span></span>

<span data-ttu-id="1ed4b-179">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder.configureservices) 및 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure) 편의 메서드는 `Startup` 클래스 지정 대신 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-179">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder.configureservices) and [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure) convenience methods can be used instead of specifying a `Startup` class.</span></span> <span data-ttu-id="1ed4b-180">`ConfigureServices`에 대한 여러 호출은 다른 것에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-180">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="1ed4b-181">`Configure`에 대한 여러 호출은 마지막 메서드 호출을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-181">Multiple calls to `Configure` use the last method call.</span></span>

[!code-csharp[](startup/snapshot_sample/Program.cs?highlight=18,22)]

## <a name="startup-filters"></a><span data-ttu-id="1ed4b-182">시작 필터</span><span class="sxs-lookup"><span data-stu-id="1ed4b-182">Startup filters</span></span>

<span data-ttu-id="1ed4b-183">[IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter)를 사용하여 앱의 [구성](#the-configure-method) 미들웨어 파이프라인의 시작 또는 끝에 미들웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-183">Use [IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter) to configure middleware at the beginning or end of an app's [Configure](#the-configure-method) middleware pipeline.</span></span> <span data-ttu-id="1ed4b-184">`IStartupFilter`는 미들웨어가 앱의 요청 처리 파이프라인의 시작 또는 끝에 라이브러리에 의해 추가되는 미들웨어 전이나 후에 실행되도록 하는데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-184">`IStartupFilter` is useful to ensure that a middleware runs before or after middleware added by libraries at the start or end of the app's request processing pipeline.</span></span>

<span data-ttu-id="1ed4b-185">`IStartupFilter`는 `Action<IApplicationBuilder>`를 받고 반환하는 단일 메서드, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter.configure)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-185">`IStartupFilter` implements a single method, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter.configure), which receives and returns an `Action<IApplicationBuilder>`.</span></span> <span data-ttu-id="1ed4b-186">[IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder)는 앱의 요청 파이프라인을 구성하는 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-186">An [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) defines a class to configure an app's request pipeline.</span></span> <span data-ttu-id="1ed4b-187">자세한 내용은 [IApplicationBuilder로 미들웨어 파이프라인 만들기](xref:fundamentals/middleware/index#creating-a-middleware-pipeline-with-iapplicationbuilder)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-187">For more information, see [Create a middleware pipeline with IApplicationBuilder](xref:fundamentals/middleware/index#creating-a-middleware-pipeline-with-iapplicationbuilder).</span></span>

<span data-ttu-id="1ed4b-188">각 `IStartupFilter`는 요청 파이프라인에서 하나 이상의 미들웨어를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-188">Each `IStartupFilter` implements one or more middlewares in the request pipeline.</span></span> <span data-ttu-id="1ed4b-189">필터는 서비스 컨테이너에 추가된 순서 대로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-189">The filters are invoked in the order they were added to the service container.</span></span> <span data-ttu-id="1ed4b-190">필터는 다음 필터에 컨트롤을 전달하기 전이나 후에 미들웨어를 추가할 수 있으므로 앱 파이프라인의 시작 또는 끝에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-190">Filters may add middleware before or after passing control to the next filter, thus they append to the beginning or end of the app pipeline.</span></span>

<span data-ttu-id="1ed4b-191">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/startup/sample/)([다운로드하는 방법](xref:tutorials/index#how-to-download-a-sample))은 `IStartupFilter`를 사용하여 미들웨어를 등록하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-191">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/startup/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)) demonstrates how to register a middleware with `IStartupFilter`.</span></span> <span data-ttu-id="1ed4b-192">샘플 앱은 쿼리 문자열 매개 변수에서 옵션 값을 설정하는 미들웨어를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-192">The sample app includes a middleware that sets an options value from a query string parameter:</span></span>

[!code-csharp[](startup/sample/RequestSetOptionsMiddleware.cs?name=snippet1)]

<span data-ttu-id="1ed4b-193">`RequestSetOptionsMiddleware`는 `RequestSetOptionsStartupFilter` 클래스에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-193">The `RequestSetOptionsMiddleware` is configured in the `RequestSetOptionsStartupFilter` class:</span></span>

[!code-csharp[](startup/sample/RequestSetOptionsStartupFilter.cs?name=snippet1&highlight=7)]

<span data-ttu-id="1ed4b-194">`IStartupFilter`는 `ConfigureServices`의 서비스 컨테이너에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-194">The `IStartupFilter` is registered in the service container in `ConfigureServices`:</span></span>

[!code-csharp[](startup/sample/Startup.cs?name=snippet1&highlight=3)]

<span data-ttu-id="1ed4b-195">`option`에 대한 쿼리 문자열 매개 변수가 제공되는 경우 미들웨어는 MVC 미들웨어가 응답을 렌더링하기 전에 값 할당을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-195">When a query string parameter for `option` is provided, the middleware processes the value assignment before the MVC middleware renders the response:</span></span>

![렌더링된 인덱스 페이지를 표시하는 브라우저 창](startup/_static/index.png)

<span data-ttu-id="1ed4b-198">미들웨어 실행 순서는 `IStartupFilter` 등록 순서로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-198">Middleware execution order is set by the order of `IStartupFilter` registrations:</span></span>

* <span data-ttu-id="1ed4b-199">여러 `IStartupFilter` 구현은 동일한 개체와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-199">Multiple `IStartupFilter` implementations may interact with the same objects.</span></span> <span data-ttu-id="1ed4b-200">순서 지정이 중요한 경우 해당 미들웨어가 실행해야 하는 순서와 일치하도록 해당 `IStartupFilter` 서비스 등록의 순서를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-200">If ordering is important, order their `IStartupFilter` service registrations to match the order that their middlewares should run.</span></span>
* <span data-ttu-id="1ed4b-201">라이브러리는 `IStartupFilter`로 등록된 다른 앱 미들웨어 전이나 후에 실행하는 하나 이상의 `IStartupFilter` 구현으로 미들웨어를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-201">Libraries may add middleware with one or more `IStartupFilter` implementations that run before or after other app middleware registered with `IStartupFilter`.</span></span> <span data-ttu-id="1ed4b-202">라이브러리의 `IStartupFilter`에 의해 추가되는 미들웨어 전에 `IStartupFilter` 미들웨어를 호출하려면 라이브러리가 서비스 컨테이너에 추가되기 전에 서비스 등록의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-202">To invoke an `IStartupFilter` middleware before a middleware added by a library's `IStartupFilter`, position the service registration before the library is added to the service container.</span></span> <span data-ttu-id="1ed4b-203">나중에 호출하려면 라이브러리가 추가된 후에 서비스 등록의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-203">To invoke it afterward, position the service registration after the library is added.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1ed4b-204">추가 자료</span><span class="sxs-lookup"><span data-stu-id="1ed4b-204">Additional resources</span></span>

* [<span data-ttu-id="1ed4b-205">호스팅</span><span class="sxs-lookup"><span data-stu-id="1ed4b-205">Hosting</span></span>](xref:fundamentals/hosting)
* [<span data-ttu-id="1ed4b-206">여러 환경 사용</span><span class="sxs-lookup"><span data-stu-id="1ed4b-206">Work with multiple environments</span></span>](xref:fundamentals/environments)
* [<span data-ttu-id="1ed4b-207">미들웨어</span><span class="sxs-lookup"><span data-stu-id="1ed4b-207">Middleware</span></span>](xref:fundamentals/middleware/index)
* [<span data-ttu-id="1ed4b-208">로깅</span><span class="sxs-lookup"><span data-stu-id="1ed4b-208">Logging</span></span>](xref:fundamentals/logging/index)
* [<span data-ttu-id="1ed4b-209">구성</span><span class="sxs-lookup"><span data-stu-id="1ed4b-209">Configuration</span></span>](xref:fundamentals/configuration/index)
* [<span data-ttu-id="1ed4b-210">StartupLoader 클래스: FindStartupType 메서드(참조 원본)</span><span class="sxs-lookup"><span data-stu-id="1ed4b-210">StartupLoader class: FindStartupType method (reference source)</span></span>](https://github.com/aspnet/Hosting/blob/rel/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/StartupLoader.cs#L66-L116)
