---
title: "ASP.NET Core 응용 프로그램 시작"
author: ardalis
description: "ASP.NET Core 시작 클래스에서 서비스 및 응용 프로그램의 요청 파이프라인을 구성 하는 방법을 검색 합니다."
ms.author: tdykstra
manager: wpickett
ms.custom: mvc
ms.date: 12/08/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/startup
ms.openlocfilehash: 8adb96c7261a2e7b1556f0daddcf6f135862b53a
ms.sourcegitcommit: 198fb0488e961048bfa376cf58cb853ef1d1cb91
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="application-startup-in-aspnet-core"></a><span data-ttu-id="8dc96-103">ASP.NET Core 응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="8dc96-103">Application startup in ASP.NET Core</span></span>

<span data-ttu-id="8dc96-104">여 [Steve Smith](https://ardalis.com), [Tom Dykstra](https://github.com/tdykstra), 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="8dc96-104">By [Steve Smith](https://ardalis.com), [Tom Dykstra](https://github.com/tdykstra), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="8dc96-105">`Startup` 클래스 서비스 및 응용 프로그램의 요청 파이프라인을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-105">The `Startup` class configures services and the app's request pipeline.</span></span>

## <a name="the-startup-class"></a><span data-ttu-id="8dc96-106">시작 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-106">The Startup class</span></span>

<span data-ttu-id="8dc96-107">ASP.NET Core 응용 프로그램 사용을 `Startup` 클래스 이름으로 지정 된 `Startup` 규칙에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-107">ASP.NET Core apps use a `Startup` class, which is named `Startup` by convention.</span></span> <span data-ttu-id="8dc96-108">`Startup` 클래스:</span><span class="sxs-lookup"><span data-stu-id="8dc96-108">The `Startup` class:</span></span>

* <span data-ttu-id="8dc96-109">선택적으로 포함할 수는 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 응용 프로그램의 서비스를 구성 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="8dc96-109">Can optionally include a [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) method to configure the app's services.</span></span>
* <span data-ttu-id="8dc96-110">포함 되어야 합니다는 [구성](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 방법을 응용 프로그램의 요청 처리 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-110">Must include a [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) method to create the app's request processing pipeline.</span></span>

<span data-ttu-id="8dc96-111">`ConfigureServices`및 `Configure` 앱 시작 시 런타임에 의해 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-111">`ConfigureServices` and `Configure` are called by the runtime when the app starts:</span></span>

[!code-csharp[Main](startup/snapshot_sample/Startup1.cs)]

<span data-ttu-id="8dc96-112">지정 된 `Startup` 클래스와 [WebHostBuilderExtensions](/dotnet/api/Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions) [UseStartup&lt;TStartup&gt; ](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 메서드:</span><span class="sxs-lookup"><span data-stu-id="8dc96-112">Specify the `Startup` class with the [WebHostBuilderExtensions](/dotnet/api/Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions) [UseStartup&lt;TStartup&gt;](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) method:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main&highlight=10)]

<span data-ttu-id="8dc96-113">`Startup` 클래스 생성자는 호스트에 의해 정의 된 종속성을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-113">The `Startup` class constructor accepts dependencies defined by the host.</span></span> <span data-ttu-id="8dc96-114">일반적인 용도 [종속성 주입](xref:fundamentals/dependency-injection) 에 `Startup` 클래스를 삽입 하는 [IHostingEnvironment](/dotnet/api/Microsoft.AspNetCore.Hosting.IHostingEnvironment) 환경에서 서비스를 구성 하려면:</span><span class="sxs-lookup"><span data-stu-id="8dc96-114">A common use of [dependency injection](xref:fundamentals/dependency-injection) into the `Startup` class is to inject [IHostingEnvironment](/dotnet/api/Microsoft.AspNetCore.Hosting.IHostingEnvironment) to configure services by environment:</span></span>

[!code-csharp[Main](startup/snapshot_sample/Startup2.cs)]

<span data-ttu-id="8dc96-115">삽입 하는 대신 `IHostingStartup` 규칙 기반 접근 방식을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-115">An alternative to injecting `IHostingStartup` is to use a conventions-based approach.</span></span> <span data-ttu-id="8dc96-116">응용 프로그램을 별도 정의할 수 `Startup` 다양 한 환경에 대 한 클래스 (예를 들어 `StartupDevelopment`), 적절 한 시작 클래스는 런타임에 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-116">The app can define separate `Startup` classes for different environments (for example, `StartupDevelopment`), and the appropriate startup class is selected at runtime.</span></span> <span data-ttu-id="8dc96-117">해당 이름 접미사는 현재 환경에 적합 한 클래스 우선 순위가 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-117">The class whose name suffix matches the current environment is prioritized.</span></span> <span data-ttu-id="8dc96-118">응용 프로그램 개발 환경에서 실행 되 고 모두를 포함 하는 경우는 `Startup` 클래스 및 `StartupDevelopment` 클래스는 `StartupDevelopment` 클래스가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-118">If the app is run in the Development environment and includes both a `Startup` class and a `StartupDevelopment` class, the `StartupDevelopment` class is used.</span></span> <span data-ttu-id="8dc96-119">자세한 내용은 참조 [여러 환경 작업](xref:fundamentals/environments#startup-conventions)합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-119">For more information see [Working with multiple environments](xref:fundamentals/environments#startup-conventions).</span></span>

<span data-ttu-id="8dc96-120">에 대 한 자세한 내용은 `WebHostBuilder`, 참조는 [호스팅](xref:fundamentals/hosting) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-120">To learn more about `WebHostBuilder`, see the [Hosting](xref:fundamentals/hosting) topic.</span></span> <span data-ttu-id="8dc96-121">시작 하는 동안 오류를 처리 하는 방법은 참조 하십시오. [시작 예외 처리](xref:fundamentals/error-handling#startup-exception-handling)합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-121">For information on handling errors during startup, see [Startup exception handling](xref:fundamentals/error-handling#startup-exception-handling).</span></span>

## <a name="the-configureservices-method"></a><span data-ttu-id="8dc96-122">ConfigureServices 메서드</span><span class="sxs-lookup"><span data-stu-id="8dc96-122">The ConfigureServices method</span></span>

<span data-ttu-id="8dc96-123">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 방법은:</span><span class="sxs-lookup"><span data-stu-id="8dc96-123">The [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) method is:</span></span>

* <span data-ttu-id="8dc96-124">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-124">Optional.</span></span>
* <span data-ttu-id="8dc96-125">하기 전에 웹 호스트에 의해 호출 된 `Configure` 응용 프로그램의 서비스를 구성 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="8dc96-125">Called by the web host before the `Configure` method to configure the app's services.</span></span>
* <span data-ttu-id="8dc96-126">여기서 [구성 옵션](xref:fundamentals/configuration/index) 규칙에 의해 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-126">Where [configuration options](xref:fundamentals/configuration/index) are set by convention.</span></span>

<span data-ttu-id="8dc96-127">서비스 컨테이너에 서비스 추가 사용할 수 있도록 응용 프로그램 내에서 `Configure` 메서드.</span><span class="sxs-lookup"><span data-stu-id="8dc96-127">Adding services to the service container makes them available within the app and in the `Configure` method.</span></span> <span data-ttu-id="8dc96-128">서비스는를 통해 확인 [종속성 주입](xref:fundamentals/dependency-injection) 또는 [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices)합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-128">The services are resolved via [dependency injection](xref:fundamentals/dependency-injection) or from [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices).</span></span>

<span data-ttu-id="8dc96-129">웹 호스트 되기 전에 일부 서비스를 구성할 수 있습니다 `Startup` 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-129">The web host may configure some services before `Startup` methods are called.</span></span> <span data-ttu-id="8dc96-130">사용할 수 있는 세부 정보는 [호스팅](xref:fundamentals/hosting) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-130">Details are available in the [Hosting](xref:fundamentals/hosting) topic.</span></span> 

<span data-ttu-id="8dc96-131">상당한 설치 해야 하는 기능을 위해 가지 `Add[Service]` 에 확장 메서드 [IServiceCollection](/dotnet/api/Microsoft.Extensions.DependencyInjection.IServiceCollection)합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-131">For features that require substantial setup, there are `Add[Service]` extension methods on [IServiceCollection](/dotnet/api/Microsoft.Extensions.DependencyInjection.IServiceCollection).</span></span> <span data-ttu-id="8dc96-132">Entity Framework, Id 및 MVC에 대 한 서비스를 등록 하는 일반적인 웹 앱:</span><span class="sxs-lookup"><span data-stu-id="8dc96-132">A typical web app registers services for Entity Framework, Identity, and MVC:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?highlight=4,7,11&start=40&end=55)]

## <a name="services-available-in-startup"></a><span data-ttu-id="8dc96-133">시작에 사용할 수 있는 서비스</span><span class="sxs-lookup"><span data-stu-id="8dc96-133">Services available in Startup</span></span>

<span data-ttu-id="8dc96-134">에 사용할 수 있는 몇 가지 서비스를 제공 하는 웹 호스트는 `Startup` 클래스 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-134">The web host provides some services that are available to the `Startup` class constructor.</span></span> <span data-ttu-id="8dc96-135">응용 프로그램을 통해 추가 서비스를 추가 합니다. `ConfigureServices`합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-135">The app adds additional services via `ConfigureServices`.</span></span> <span data-ttu-id="8dc96-136">호스트와 응용 프로그램 서비스에서 사용할 수 있는 다음 `Configure` 및 응용 프로그램에 걸쳐 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-136">Both the host and app services are then available in `Configure` and throughout the application.</span></span>

## <a name="the-configure-method"></a><span data-ttu-id="8dc96-137">Configure 메서드</span><span class="sxs-lookup"><span data-stu-id="8dc96-137">The Configure method</span></span>

<span data-ttu-id="8dc96-138">[구성](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 메서드를 사용 하는 응용 프로그램 HTTP 요청에 응답 하는 방식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-138">The [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) method is used to specify how the app responds to HTTP requests.</span></span> <span data-ttu-id="8dc96-139">요청 파이프라인을 추가 하 여 구성할 [미들웨어](xref:fundamentals/middleware) 구성 요소는 [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="8dc96-139">The request pipeline is configured by adding [middleware](xref:fundamentals/middleware) components to an [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) instance.</span></span> <span data-ttu-id="8dc96-140">`IApplicationBuilder`사용할 수는 `Configure` 하지만 메서드를 서비스 컨테이너에 등록 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-140">`IApplicationBuilder` is available to the `Configure` method, but it isn't registered in the service container.</span></span> <span data-ttu-id="8dc96-141">호스팅 만듭니다는 `IApplicationBuilder` 에 직접 전달 `Configure` ([참조 소스](https://github.com/aspnet/Hosting/blob/release/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/WebHost.cs#L179-L192)).</span><span class="sxs-lookup"><span data-stu-id="8dc96-141">Hosting creates an `IApplicationBuilder` and passes it directly to `Configure` ([reference source](https://github.com/aspnet/Hosting/blob/release/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/WebHost.cs#L179-L192)).</span></span>

<span data-ttu-id="8dc96-142">[ASP.NET Core 템플릿](/dotnet/core/tools/dotnet-new) 개발자 예외 페이지를 지 원하는 파이프라인을 구성 [BrowserLink](http://vswebessentials.com/features/browserlink), 오류 페이지, 정적 파일 및 ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="8dc96-142">The [ASP.NET Core templates](/dotnet/core/tools/dotnet-new) configure the pipeline with support for a developer exception page, [BrowserLink](http://vswebessentials.com/features/browserlink), error pages, static files, and ASP.NET MVC:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Startup.cs?range=28-48&highlight=5,6,10,13,15)]

<span data-ttu-id="8dc96-143">각 `Use` 확장 메서드는 요청 파이프라인에 미들웨어 구성 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-143">Each `Use` extension method adds a middleware component to the request pipeline.</span></span> <span data-ttu-id="8dc96-144">예를 들어,는 `UseMvc` 추가 하는 확장 메서드는 [라우팅 미들웨어](xref:fundamentals/routing) 요청 파이프라인을 구성 및 [MVC](xref:mvc/overview) 기본 처리기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-144">For instance, the `UseMvc` extension method adds the [routing middleware](xref:fundamentals/routing) to the request pipeline and configures [MVC](xref:mvc/overview) as the default handler.</span></span>

<span data-ttu-id="8dc96-145">추가 서비스와 같은 `IHostingEnvironment` 및 `ILoggerFactory`, 메서드 서명에서 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-145">Additional services, such as `IHostingEnvironment` and `ILoggerFactory`, may also be specified in the method signature.</span></span> <span data-ttu-id="8dc96-146">을 지정 하면 사용 가능한 경우 추가 서비스는 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-146">When specified, additional services are injected if they're available.</span></span>

<span data-ttu-id="8dc96-147">사용 하는 방법에 대 한 자세한 내용은 `IApplicationBuilder`, 참조 [미들웨어](xref:fundamentals/middleware)합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-147">For more information on how to use `IApplicationBuilder`, see [Middleware](xref:fundamentals/middleware).</span></span>

## <a name="convenience-methods"></a><span data-ttu-id="8dc96-148">편리한 메서드</span><span class="sxs-lookup"><span data-stu-id="8dc96-148">Convenience methods</span></span>

<span data-ttu-id="8dc96-149">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder.configureservices) 및 [구성](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure) 편의 메서드를 지정 하는 대신 사용할 수는 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-149">[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder.configureservices) and [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure) convenience methods can be used instead of specifying a `Startup` class.</span></span> <span data-ttu-id="8dc96-150">여러 번 호출 `ConfigureServices` 서로에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-150">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="8dc96-151">여러 번 호출 `Configure` 마지막 메서드 호출을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-151">Multiple calls to `Configure` use the last method call.</span></span>

[!code-csharp[Main](startup/snapshot_sample/Program.cs?highlight=16,20)]

## <a name="startup-filters"></a><span data-ttu-id="8dc96-152">시작 필터</span><span class="sxs-lookup"><span data-stu-id="8dc96-152">Startup filters</span></span>

<span data-ttu-id="8dc96-153">사용 하 여 [IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter) 미들웨어를 구성 하는 시작 이나 끝 응용 프로그램의 [구성](#the-configure-method) 미들웨어 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="8dc96-153">Use [IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter) to configure middleware at the beginning or end of an app's [Configure](#the-configure-method) middleware pipeline.</span></span> <span data-ttu-id="8dc96-154">`IStartupFilter`미들웨어 실행 전이나 후 라이브러리 시작 부분이 나 끝의 응용 프로그램의 요청 처리 파이프라인에 의해 추가 되는 미들웨어 되도록 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-154">`IStartupFilter` is useful to ensure that a middleware runs before or after middleware added by libraries at the start or end of the app's request processing pipeline.</span></span>

<span data-ttu-id="8dc96-155">`IStartupFilter`단일 메서드를 구현 [구성](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter.configure)를 받아서 반환 하는 프로그램 `Action<IApplicationBuilder>`합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-155">`IStartupFilter` implements a single method, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter.configure), which receives and returns an `Action<IApplicationBuilder>`.</span></span> <span data-ttu-id="8dc96-156">[IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) 는 응용 프로그램의 요청 파이프라인을 구성 하는 클래스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-156">An [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) defines a class to configure an app's request pipeline.</span></span> <span data-ttu-id="8dc96-157">자세한 내용은 참조 [IApplicationBuilder 미들웨어 파이프라인 만들기](xref:fundamentals/middleware#creating-a-middleware-pipeline-with-iapplicationbuilder)합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-157">For more information, see [Creating a middleware pipeline with IApplicationBuilder](xref:fundamentals/middleware#creating-a-middleware-pipeline-with-iapplicationbuilder).</span></span>

<span data-ttu-id="8dc96-158">각 `IStartupFilter` 요청 파이프라인에서 하나 이상의 middlewares를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-158">Each `IStartupFilter` implements one or more middlewares in the request pipeline.</span></span> <span data-ttu-id="8dc96-159">필터는 서비스 컨테이너에 추가 된 순서 대로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-159">The filters are invoked in the order they were added to the service container.</span></span> <span data-ttu-id="8dc96-160">미들웨어 하기 전에 행 필터를 추가할 수 있습니다 또는 제어 하 여 다음 필터를 통과 했으면 따라서은 추가 시작 또는 응용 프로그램 파이프라인의 끝에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-160">Filters may add middleware before or after passing control to the next filter, thus they append to the beginning or end of the app pipeline.</span></span>

<span data-ttu-id="8dc96-161">[샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/startup/sample/) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample)) 사용 하 여 미들웨어를 등록 하는 방법을 보여 줍니다. `IStartupFilter`합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-161">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/startup/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)) demonstrates how to register a middleware with `IStartupFilter`.</span></span> <span data-ttu-id="8dc96-162">샘플 응용 프로그램에서 쿼리 문자열 매개 변수 옵션 값을 설정 하는 미들웨어를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-162">The sample app includes a middleware that sets an options value from a query string parameter:</span></span>

[!code-csharp[Main](startup/sample/RequestSetOptionsMiddleware.cs?name=snippet1)]

<span data-ttu-id="8dc96-163">`RequestSetOptionsMiddleware` 에 구성 된 `RequestSetOptionsStartupFilter` 클래스:</span><span class="sxs-lookup"><span data-stu-id="8dc96-163">The `RequestSetOptionsMiddleware` is configured in the `RequestSetOptionsStartupFilter` class:</span></span>

[!code-csharp[Main](startup/sample/RequestSetOptionsStartupFilter.cs?name=snippet1&highlight=7)]

<span data-ttu-id="8dc96-164">`IStartupFilter` 서비스 컨테이너에에 등록 되어 `ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="8dc96-164">The `IStartupFilter` is registered in the service container in `ConfigureServices`:</span></span>

[!code-csharp[Main](startup/sample/Startup.cs?name=snippet1&highlight=3)]

<span data-ttu-id="8dc96-165">경우에 대 한 쿼리 문자열 매개 변수 `option` MVC 미들웨어의 응답을 렌더링 하기 전에 값 할당을 처리 하는 미들웨어 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-165">When a query string parameter for `option` is provided, the middleware processes the value assignment before the MVC middleware renders the response:</span></span>

![브라우저 창에 렌더링된 된 인덱스 페이지를 표시 합니다.](startup/_static/index.png)

<span data-ttu-id="8dc96-168">순서 여 미들웨어 실행 순서 설정 되어 `IStartupFilter` 등록:</span><span class="sxs-lookup"><span data-stu-id="8dc96-168">Middleware execution order is set by the order of `IStartupFilter` registrations:</span></span>

* <span data-ttu-id="8dc96-169">여러 `IStartupFilter` 구현을 동일한 개체를 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-169">Multiple `IStartupFilter` implementations may interact with the same objects.</span></span> <span data-ttu-id="8dc96-170">정렬 순서가 중요 한 경우 해당 `IStartupFilter` 서비스 자신의 middlewares 실행 해야 하는 순서와 일치 하도록 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-170">If ordering is important, order their `IStartupFilter` service registrations to match the order that their middlewares should run.</span></span>
* <span data-ttu-id="8dc96-171">라이브러리에서 하나 이상의 미들웨어를 추가할 수 있습니다. `IStartupFilter` 전 또는 다른 응용 프로그램 미들웨어에 등록 한 후에 실행 하는 구현 `IStartupFilter`합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-171">Libraries may add middleware with one or more `IStartupFilter` implementations that run before or after other app middleware registered with `IStartupFilter`.</span></span> <span data-ttu-id="8dc96-172">호출 하는 `IStartupFilter` 미들웨어는 라이브러리에 의해 추가 하기 전에 미들웨어 `IStartupFilter`, 라이브러리 서비스 컨테이너에 추가 되기 전에 서비스 등록 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-172">To invoke an `IStartupFilter` middleware before a middleware added by a library's `IStartupFilter`, position the service registration before the library is added to the service container.</span></span> <span data-ttu-id="8dc96-173">라이브러리를 추가한 후 나중에 호출할 서비스 등록을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dc96-173">To invoke it afterward, position the service registration after the library is added.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8dc96-174">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8dc96-174">Additional resources</span></span>

* [<span data-ttu-id="8dc96-175">호스팅</span><span class="sxs-lookup"><span data-stu-id="8dc96-175">Hosting</span></span>](xref:fundamentals/hosting)
* [<span data-ttu-id="8dc96-176">여러 환경 사용</span><span class="sxs-lookup"><span data-stu-id="8dc96-176">Working with Multiple Environments</span></span>](xref:fundamentals/environments)
* [<span data-ttu-id="8dc96-177">미들웨어</span><span class="sxs-lookup"><span data-stu-id="8dc96-177">Middleware</span></span>](xref:fundamentals/middleware)
* [<span data-ttu-id="8dc96-178">로깅</span><span class="sxs-lookup"><span data-stu-id="8dc96-178">Logging</span></span>](xref:fundamentals/logging/index)
* [<span data-ttu-id="8dc96-179">구성</span><span class="sxs-lookup"><span data-stu-id="8dc96-179">Configuration</span></span>](xref:fundamentals/configuration/index)
* <span data-ttu-id="8dc96-180">[StartupLoader 클래스: FindStartupType 메서드 (참조 소스)](https://github.com/aspnet/Hosting/blob/rel/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/StartupLoader.cs#L66-L116))</span><span class="sxs-lookup"><span data-stu-id="8dc96-180">[StartupLoader class: FindStartupType method (reference source)](https://github.com/aspnet/Hosting/blob/rel/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/StartupLoader.cs#L66-L116))</span></span>
