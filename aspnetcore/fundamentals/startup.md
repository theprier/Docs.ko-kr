---
title: ASP.NET Core에서 응용 프로그램 시작
author: ardalis
description: ASP.NET Core의 시작 클래스에서 서비스 및 앱의 요청 파이프라인을 구성하는 방법을 설명합니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 4/13/2018
uid: fundamentals/startup
ms.openlocfilehash: 392dc83666bc6b9012adc6c32169ae7bdc7ed8d7
ms.sourcegitcommit: f43f430a166a7ec137fcad12ded0372747227498
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49391117"
---
# <a name="application-startup-in-aspnet-core"></a><span data-ttu-id="6694f-103">ASP.NET Core에서 응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="6694f-103">Application startup in ASP.NET Core</span></span>

<span data-ttu-id="6694f-104">작성자: [Steve Smith](https://ardalis.com), [Tom Dykstra](https://github.com/tdykstra) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="6694f-104">By [Steve Smith](https://ardalis.com), [Tom Dykstra](https://github.com/tdykstra), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="6694f-105">`Startup` 클래스는 서비스 및 앱의 요청 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-105">The `Startup` class configures services and the app's request pipeline.</span></span>

## <a name="the-startup-class"></a><span data-ttu-id="6694f-106">시작 클래스</span><span class="sxs-lookup"><span data-stu-id="6694f-106">The Startup class</span></span>

<span data-ttu-id="6694f-107">ASP.NET Core 앱은 규칙에 따라 `Startup`으로 이름이 지정된 `Startup` 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-107">ASP.NET Core apps use a `Startup` class, which is named `Startup` by convention.</span></span> <span data-ttu-id="6694f-108">`Startup` 클래스:</span><span class="sxs-lookup"><span data-stu-id="6694f-108">The `Startup` class:</span></span>

* <span data-ttu-id="6694f-109">선택적으로 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 메서드를 포함하여 앱의 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-109">Can optionally include a [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) method to configure the app's services.</span></span>
* <span data-ttu-id="6694f-110">[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 메서드를 포함하여 앱의 요청 처리 파이프라인을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-110">Must include a [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) method to create the app's request processing pipeline.</span></span>

<span data-ttu-id="6694f-111">`ConfigureServices` 및 `Configure`는 앱 시작 시 런타임에 의해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-111">`ConfigureServices` and `Configure` are called by the runtime when the app starts:</span></span>

[!code-csharp[](startup/snapshot_sample/Startup1.cs)]

<span data-ttu-id="6694f-112">[WebHostBuilderExtensions](/dotnet/api/Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions) [UseStartup&lt;TStartup&gt;](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 메서드로 `Startup` 클래스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-112">Specify the `Startup` class with the [WebHostBuilderExtensions](/dotnet/api/Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions) [UseStartup&lt;TStartup&gt;](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) method:</span></span>

[!code-csharp[](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main&highlight=10)]

<span data-ttu-id="6694f-113">웹 호스트는 `Startup` 클래스 생성자에 사용할 수 있는 몇 가지 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-113">The web host provides some services that are available to the `Startup` class constructor.</span></span> <span data-ttu-id="6694f-114">앱은 `ConfigureServices`를 통해 추가 서비스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-114">The app adds additional services via `ConfigureServices`.</span></span> <span data-ttu-id="6694f-115">그러면 호스트 및 앱 서비스 모두를 `Configure` 및 앱 전체에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-115">Both the host and app services are then available in `Configure` and throughout the app.</span></span>

<span data-ttu-id="6694f-116">`Startup` 클래스에 대한 [종속성 주입](xref:fundamentals/dependency-injection)의 일반적인 용도는 다음을 삽입하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-116">A common use of [dependency injection](xref:fundamentals/dependency-injection) into the `Startup` class is to inject:</span></span>

* <span data-ttu-id="6694f-117">환경에서 서비스를 구성하는 [IHostingEnvironment](/dotnet/api/Microsoft.AspNetCore.Hosting.IHostingEnvironment)</span><span class="sxs-lookup"><span data-stu-id="6694f-117">[IHostingEnvironment](/dotnet/api/Microsoft.AspNetCore.Hosting.IHostingEnvironment) to configure services by environment.</span></span>
* <span data-ttu-id="6694f-118">구성을 읽는 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)</span><span class="sxs-lookup"><span data-stu-id="6694f-118">[IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) to read configuration.</span></span>
* <span data-ttu-id="6694f-119">`Startup.ConfigureServices`에서 로거를 만드는 [ILoggerFactory](/dotnet/api/microsoft.extensions.logging.iloggerfactory)</span><span class="sxs-lookup"><span data-stu-id="6694f-119">[ILoggerFactory](/dotnet/api/microsoft.extensions.logging.iloggerfactory) to create a logger in `Startup.ConfigureServices`.</span></span>

[!code-csharp[](startup/snapshot_sample/Startup2.cs)]

<span data-ttu-id="6694f-120">`IHostingEnvironment` 삽입의 대안은 규칙 기반 접근 방식을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-120">An alternative to injecting `IHostingEnvironment` is to use a conventions-based approach.</span></span> <span data-ttu-id="6694f-121">앱은 다양한 환경(예: `StartupDevelopment`)에 대한 별도의 `Startup` 클래스를 정의할 수 있으며 적절한 `Startup` 클래스는 런타임에 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-121">The app can define separate `Startup` classes for different environments (for example, `StartupDevelopment`), and the appropriate `Startup` class is selected at runtime.</span></span> <span data-ttu-id="6694f-122">해당 이름 접미사가 현재 환경과 일치하는 클래스에 우선 순위가 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-122">The class whose name suffix matches the current environment is prioritized.</span></span> <span data-ttu-id="6694f-123">앱이 개발 환경에서 실행되고 `Startup` 클래스 및 `StartupDevelopment` 클래스 모두를 포함하는 경우 `StartupDevelopment` 클래스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-123">If the app is run in the Development environment and includes both a `Startup` class and a `StartupDevelopment` class, the `StartupDevelopment` class is used.</span></span> <span data-ttu-id="6694f-124">자세한 내용은 [여러 환경 사용](xref:fundamentals/environments#environment-based-startup-class-and-methods)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6694f-124">For more information, see [Use multiple environments](xref:fundamentals/environments#environment-based-startup-class-and-methods).</span></span>

<span data-ttu-id="6694f-125">`WebHostBuilder`에 대한 자세한 내용은 [호스팅](xref:fundamentals/host/index) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6694f-125">To learn more about `WebHostBuilder`, see the [Hosting](xref:fundamentals/host/index) topic.</span></span> <span data-ttu-id="6694f-126">시작하는 동안 오류를 처리하는 방법은 [시작 예외 처리](xref:fundamentals/error-handling#startup-exception-handling)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6694f-126">For information on handling errors during startup, see [Startup exception handling](xref:fundamentals/error-handling#startup-exception-handling).</span></span>

## <a name="the-configureservices-method"></a><span data-ttu-id="6694f-127">ConfigureServices 메서드</span><span class="sxs-lookup"><span data-stu-id="6694f-127">The ConfigureServices method</span></span>

<span data-ttu-id="6694f-128">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 메서드는</span><span class="sxs-lookup"><span data-stu-id="6694f-128">The [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) method is:</span></span>

* <span data-ttu-id="6694f-129">Optional</span><span class="sxs-lookup"><span data-stu-id="6694f-129">Optional</span></span>
* <span data-ttu-id="6694f-130">`Configure` 메서드 전에 웹 호스트에 의해 호출되어 앱의 서비스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-130">Called by the web host before the `Configure` method to configure the app's services.</span></span>
* <span data-ttu-id="6694f-131">여기서 [구성 옵션](xref:fundamentals/configuration/index)은 규칙에 의해 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-131">Where [configuration options](xref:fundamentals/configuration/index) are set by convention.</span></span>

<span data-ttu-id="6694f-132">일반적인 패턴은 모든 `Add{Service}` 메서드를 호출한 후 모든 `services.Configure{Service}` 메서드를 호출하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-132">The typical pattern is to call all the `Add{Service}` methods, and then call all the `services.Configure{Service}` methods.</span></span> <span data-ttu-id="6694f-133">예는 [ID 서비스 구성](xref:security/authentication/identity#pw)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6694f-133">For example, see [Configure Identity services](xref:security/authentication/identity#pw).</span></span>

<span data-ttu-id="6694f-134">서비스 컨테이너에 서비스를 추가하면 앱 내 및 `Configure` 메서드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-134">Adding services to the service container makes them available within the app and in the `Configure` method.</span></span> <span data-ttu-id="6694f-135">서비스는 [종속성 주입](xref:fundamentals/dependency-injection)을 통해 또는 [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices)에서 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-135">The services are resolved via [dependency injection](xref:fundamentals/dependency-injection) or from [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices).</span></span>

<span data-ttu-id="6694f-136">웹 호스트는 `Startup` 메서드가 호출되기 전에 일부 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-136">The web host may configure some services before `Startup` methods are called.</span></span> <span data-ttu-id="6694f-137">세부 정보는 [ASP.NET Core의 호스트](xref:fundamentals/host/index) 항목에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-137">Details are available in the [Host in ASP.NET Core](xref:fundamentals/host/index) topic.</span></span>

<span data-ttu-id="6694f-138">대부분의 설치가 필요한 기능의 경우 [IServiceCollection](/dotnet/api/Microsoft.Extensions.DependencyInjection.IServiceCollection)에 `Add[Service]` 확장 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-138">For features that require substantial setup, there are `Add[Service]` extension methods on [IServiceCollection](/dotnet/api/Microsoft.Extensions.DependencyInjection.IServiceCollection).</span></span> <span data-ttu-id="6694f-139">일반적인 ASP.NET Core 앱은 Entity Framework, ID 및 MVC에 대한 서비스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-139">A typical ASP.NET Core app registers services for Entity Framework, Identity, and MVC:</span></span>

[!code-csharp[](../common/samples/WebApplication1/Startup.cs?highlight=4,7,11&start=40&end=55)]

## <a name="the-configure-method"></a><span data-ttu-id="6694f-140">Configure 메서드</span><span class="sxs-lookup"><span data-stu-id="6694f-140">The Configure method</span></span>

<span data-ttu-id="6694f-141">[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 메서드는 앱이 HTTP 요청에 응답하는 방식을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-141">The [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) method is used to specify how the app responds to HTTP requests.</span></span> <span data-ttu-id="6694f-142">요청 파이프라인은 [미들웨어](xref:fundamentals/middleware/index) 구성 요소를 [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) 인스턴스에 추가하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-142">The request pipeline is configured by adding [middleware](xref:fundamentals/middleware/index) components to an [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) instance.</span></span> <span data-ttu-id="6694f-143">`IApplicationBuilder`는 `Configure` 메서드에 사용할 수 있지만 서비스 컨테이너에 등록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-143">`IApplicationBuilder` is available to the `Configure` method, but it isn't registered in the service container.</span></span> <span data-ttu-id="6694f-144">호스팅은 `IApplicationBuilder`를 만들고 `Configure`에 직접 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-144">Hosting creates an `IApplicationBuilder` and passes it directly to `Configure`.</span></span>

<span data-ttu-id="6694f-145">[ASP.NET Core 템플릿](/dotnet/core/tools/dotnet-new)은 개발자 예외 페이지, [BrowserLink](http://vswebessentials.com/features/browserlink), 오류 페이지, 정적 파일 및 ASP.NET Core MVC에 대한 지원으로 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-145">The [ASP.NET Core templates](/dotnet/core/tools/dotnet-new) configure the pipeline with support for a developer exception page, [BrowserLink](http://vswebessentials.com/features/browserlink), error pages, static files, and ASP.NET Core MVC:</span></span>

[!code-csharp[](../common/samples/WebApplication1DotNetCore2.0App/Startup.cs?range=28-48&highlight=5,6,10,13,15)]

<span data-ttu-id="6694f-146">각 `Use` 확장 메서드는 요청 파이프라인에 미들웨어 구성 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-146">Each `Use` extension method adds a middleware component to the request pipeline.</span></span> <span data-ttu-id="6694f-147">예를 들어 `UseMvc` 확장 메서드는 [라우팅 미들웨어](xref:fundamentals/routing)를 요청 파이프라인에 추가하고 기본 처리기로 [MVC](xref:mvc/overview)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-147">For instance, the `UseMvc` extension method adds the [Routing Middleware](xref:fundamentals/routing) to the request pipeline and configures [MVC](xref:mvc/overview) as the default handler.</span></span>

<span data-ttu-id="6694f-148">요청 파이프라인의 각 미들웨어 구성 요소는 파이프라인의 다음 구성 요소를 호출하거나 적절한 경우 체인을 단락(short-circuiting)하는 일을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-148">Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline or short-circuiting the chain, if appropriate.</span></span> <span data-ttu-id="6694f-149">미들웨어 체인을 따라 단락(short-circuiting)이 발생하지 않으면, 각 미들웨어는 클라이언트에 전송되기 전에 요청을 처리할 수 있는 두 번째 기회를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-149">If short-circuiting doesn't occur along the middleware chain, each middleware has a second chance to process the request before it's sent to the client.</span></span>

<span data-ttu-id="6694f-150">`IHostingEnvironment` 및 `ILoggerFactory`와 같은 추가 서비스는 메서드 서명에서 지정될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-150">Additional services, such as `IHostingEnvironment` and `ILoggerFactory`, may also be specified in the method signature.</span></span> <span data-ttu-id="6694f-151">지정되면 사용 가능한 경우 추가 서비스가 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-151">When specified, additional services are injected if they're available.</span></span>

<span data-ttu-id="6694f-152">`IApplicationBuilder`를 사용하는 방법 및 미들웨어 처리 순서에 대한 자세한 내용은 [미들웨어](xref:fundamentals/middleware/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6694f-152">For more information on how to use `IApplicationBuilder` and the order of middleware processing, see [Middleware](xref:fundamentals/middleware/index).</span></span>

## <a name="convenience-methods"></a><span data-ttu-id="6694f-153">편리한 메서드</span><span class="sxs-lookup"><span data-stu-id="6694f-153">Convenience methods</span></span>

<span data-ttu-id="6694f-154">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder.configureservices) 및 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure) 편의 메서드는 `Startup` 클래스 지정 대신 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-154">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder.configureservices) and [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure) convenience methods can be used instead of specifying a `Startup` class.</span></span> <span data-ttu-id="6694f-155">`ConfigureServices`에 대한 여러 호출은 다른 것에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-155">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="6694f-156">`Configure`에 대한 여러 호출은 마지막 메서드 호출을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-156">Multiple calls to `Configure` use the last method call.</span></span>

[!code-csharp[](startup/snapshot_sample/Program.cs?highlight=18,22)]

## <a name="extend-startup-with-startup-filters"></a><span data-ttu-id="6694f-157">시작 필터로 시작 확장</span><span class="sxs-lookup"><span data-stu-id="6694f-157">Extend Startup with startup filters</span></span>

<span data-ttu-id="6694f-158">[IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter)를 사용하여 앱의 [구성](#the-configure-method) 미들웨어 파이프라인의 시작 또는 끝에 미들웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-158">Use [IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter) to configure middleware at the beginning or end of an app's [Configure](#the-configure-method) middleware pipeline.</span></span> <span data-ttu-id="6694f-159">`IStartupFilter`는 미들웨어가 앱의 요청 처리 파이프라인의 시작 또는 끝에 라이브러리에 의해 추가되는 미들웨어 전이나 후에 실행되도록 하는데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-159">`IStartupFilter` is useful to ensure that a middleware runs before or after middleware added by libraries at the start or end of the app's request processing pipeline.</span></span>

<span data-ttu-id="6694f-160">`IStartupFilter`는 `Action<IApplicationBuilder>`를 받고 반환하는 단일 메서드, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter.configure)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-160">`IStartupFilter` implements a single method, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter.configure), which receives and returns an `Action<IApplicationBuilder>`.</span></span> <span data-ttu-id="6694f-161">[IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder)는 앱의 요청 파이프라인을 구성하는 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-161">An [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) defines a class to configure an app's request pipeline.</span></span> <span data-ttu-id="6694f-162">자세한 내용은 [IApplicationBuilder로 미들웨어 파이프라인 만들기](xref:fundamentals/middleware/index#create-a-middleware-pipeline-with-iapplicationbuilder)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6694f-162">For more information, see [Create a middleware pipeline with IApplicationBuilder](xref:fundamentals/middleware/index#create-a-middleware-pipeline-with-iapplicationbuilder).</span></span>

<span data-ttu-id="6694f-163">각 `IStartupFilter`는 요청 파이프라인에서 하나 이상의 미들웨어를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-163">Each `IStartupFilter` implements one or more middlewares in the request pipeline.</span></span> <span data-ttu-id="6694f-164">필터는 서비스 컨테이너에 추가된 순서 대로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-164">The filters are invoked in the order they were added to the service container.</span></span> <span data-ttu-id="6694f-165">필터는 다음 필터에 컨트롤을 전달하기 전이나 후에 미들웨어를 추가할 수 있으므로 앱 파이프라인의 시작 또는 끝에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-165">Filters may add middleware before or after passing control to the next filter, thus they append to the beginning or end of the app pipeline.</span></span>

<span data-ttu-id="6694f-166">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/startup/sample/)([다운로드하는 방법](xref:tutorials/index#how-to-download-a-sample))은 `IStartupFilter`를 사용하여 미들웨어를 등록하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-166">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/startup/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)) demonstrates how to register a middleware with `IStartupFilter`.</span></span> <span data-ttu-id="6694f-167">샘플 앱은 쿼리 문자열 매개 변수에서 옵션 값을 설정하는 미들웨어를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-167">The sample app includes a middleware that sets an options value from a query string parameter:</span></span>

[!code-csharp[](startup/sample/RequestSetOptionsMiddleware.cs?name=snippet1)]

<span data-ttu-id="6694f-168">`RequestSetOptionsMiddleware`는 `RequestSetOptionsStartupFilter` 클래스에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-168">The `RequestSetOptionsMiddleware` is configured in the `RequestSetOptionsStartupFilter` class:</span></span>

[!code-csharp[](startup/sample/RequestSetOptionsStartupFilter.cs?name=snippet1&highlight=7)]

<span data-ttu-id="6694f-169">`IStartupFilter`는 [IWebHostBuilder.ConfigureServices](xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.ConfigureServices*)의 서비스 컨테이너에 등록되어 시작 필터가 `Startup` 클래스 외부에서 `Startup`을 확대하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-169">The `IStartupFilter` is registered in the service container in [IWebHostBuilder.ConfigureServices](xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.ConfigureServices*) to demonstrate how the startup filter augments `Startup` from outside of the `Startup` class:</span></span>

[!code-csharp[](startup/sample/Program.cs?name=snippet1&highlight=4-5)]

<span data-ttu-id="6694f-170">`option`에 대한 쿼리 문자열 매개 변수가 제공되는 경우 미들웨어는 MVC 미들웨어가 응답을 렌더링하기 전에 값 할당을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-170">When a query string parameter for `option` is provided, the middleware processes the value assignment before the MVC middleware renders the response:</span></span>

![렌더링된 인덱스 페이지를 표시하는 브라우저 창](startup/_static/index.png)

<span data-ttu-id="6694f-173">미들웨어 실행 순서는 `IStartupFilter` 등록 순서로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-173">Middleware execution order is set by the order of `IStartupFilter` registrations:</span></span>

* <span data-ttu-id="6694f-174">여러 `IStartupFilter` 구현은 동일한 개체와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-174">Multiple `IStartupFilter` implementations may interact with the same objects.</span></span> <span data-ttu-id="6694f-175">순서 지정이 중요한 경우 해당 미들웨어가 실행해야 하는 순서와 일치하도록 해당 `IStartupFilter` 서비스 등록의 순서를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-175">If ordering is important, order their `IStartupFilter` service registrations to match the order that their middlewares should run.</span></span>
* <span data-ttu-id="6694f-176">라이브러리는 `IStartupFilter`로 등록된 다른 앱 미들웨어 전이나 후에 실행하는 하나 이상의 `IStartupFilter` 구현으로 미들웨어를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-176">Libraries may add middleware with one or more `IStartupFilter` implementations that run before or after other app middleware registered with `IStartupFilter`.</span></span> <span data-ttu-id="6694f-177">라이브러리의 `IStartupFilter`에 의해 추가되는 미들웨어 전에 `IStartupFilter` 미들웨어를 호출하려면 라이브러리가 서비스 컨테이너에 추가되기 전에 서비스 등록의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-177">To invoke an `IStartupFilter` middleware before a middleware added by a library's `IStartupFilter`, position the service registration before the library is added to the service container.</span></span> <span data-ttu-id="6694f-178">나중에 호출하려면 라이브러리가 추가된 후에 서비스 등록의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-178">To invoke it afterward, position the service registration after the library is added.</span></span>

## <a name="add-configuration-at-startup-from-an-external-assembly"></a><span data-ttu-id="6694f-179">외부 어셈블리의 시작 시 구성 추가</span><span class="sxs-lookup"><span data-stu-id="6694f-179">Add configuration at startup from an external assembly</span></span>

<span data-ttu-id="6694f-180">[IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) 구현에서는 시작 시 앱의 `Startup` 클래스 외부에 있는 외부 어셈블리에서 앱에 향상된 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6694f-180">An [IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) implementation allows adding enhancements to an app at startup from an external assembly outside of the app's `Startup` class.</span></span> <span data-ttu-id="6694f-181">자세한 내용은 [외부 어셈블리에서 앱 강화](xref:fundamentals/configuration/platform-specific-configuration)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6694f-181">For more information, see [Enhance an app from an external assembly](xref:fundamentals/configuration/platform-specific-configuration).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6694f-182">추가 자료</span><span class="sxs-lookup"><span data-stu-id="6694f-182">Additional resources</span></span>

* <xref:fundamentals/host/index>
* <xref:fundamentals/environments>
* <xref:fundamentals/middleware/index>
* <xref:fundamentals/logging/index>
* <xref:fundamentals/configuration/index>
