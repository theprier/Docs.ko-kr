---
title: "ASP.NET Core에서 응용 프로그램 시작"
author: ardalis
description: "ASP.NET Core의 시작 클래스에서 서비스 및 앱의 요청 파이프라인을 구성하는 방법을 알아봅니다."
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 12/08/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/startup
ms.openlocfilehash: c324918b33af82b619bb2251f32308e4a57c27e5
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="application-startup-in-aspnet-core"></a>ASP.NET Core에서 응용 프로그램 시작

작성자: [Steve Smith](https://ardalis.com), [Tom Dykstra](https://github.com/tdykstra) 및 [Luke Latham](https://github.com/guardrex)

`Startup` 클래스는 서비스와 응용 프로그램의 요청 파이프라인을 구성합니다.

## <a name="the-startup-class"></a>Startup 클래스

ASP.NET Core 앱은 규칙에 따라 `Startup`으로 이름이 지정된 `Startup` 클래스를 사용합니다. `Startup` 클래스:

* 선택적으로 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 메서드를 포함하여 앱의 서비스를 구성할 수 있습니다.
* [Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 메서드를 포함하여 앱의 요청 처리 파이프라인을 만들어야 합니다.

`ConfigureServices` 및 `Configure`는 앱 시작 시 런타임에 의해 호출됩니다.

[!code-csharp[Main](startup/snapshot_sample/Startup1.cs)]

[WebHostBuilderExtensions](/dotnet/api/Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions) [UseStartup&lt;TStartup&gt;](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 메서드로 `Startup` 클래스를 지정합니다.

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main&highlight=10)]

`Startup` 클래스 생성자는 호스트에 의해 정의된 종속성을 허용합니다. `Startup` 클래스에 대한 [종속성 주입](xref:fundamentals/dependency-injection)의 일반적인 용도는 다음을 삽입하는 것입니다.

* 환경에서 서비스를 구성하는 [IHostingEnvironment](/dotnet/api/Microsoft.AspNetCore.Hosting.IHostingEnvironment)
* 시작하는 동안 앱을 구성하는 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)

[!code-csharp[Main](startup/snapshot_sample/Startup2.cs)]

`IHostingEnvironment` 삽입의 대안은 규칙 기반 접근 방식을 사용하는 것입니다. 앱은 다양한 환경(예: `StartupDevelopment`)에 대한 별도의 `Startup` 클래스를 정의할 수 있으며 적절한 시작 클래스는 런타임에 선택됩니다. 해당 이름 접미사가 현재 환경과 일치하는 클래스에 우선 순위가 부여됩니다. 앱이 개발 환경에서 실행되고 `Startup` 클래스 및 `StartupDevelopment` 클래스 모두를 포함하는 경우 `StartupDevelopment` 클래스가 사용됩니다. 자세한 내용은 [여러 환경 사용](xref:fundamentals/environments#startup-conventions)을 참조하세요.

`WebHostBuilder`에 대한 자세한 내용은 [호스팅](xref:fundamentals/hosting) 항목을 참조하세요. 시작하는 동안 오류를 처리하는 방법은 [시작 예외 처리](xref:fundamentals/error-handling#startup-exception-handling)를 참조하세요.

## <a name="the-configureservices-method"></a>ConfigureServices 메서드

[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 메서드는

* 선택 사항입니다.
* `Configure` 메서드 전에 웹 호스트에 의해 호출되어 앱의 서비스를 구성합니다.
* 여기서 [구성 옵션](xref:fundamentals/configuration/index)은 규칙에 의해 설정됩니다.

서비스 컨테이너에 서비스를 추가하면 앱 내 및 `Configure` 메서드에서 사용할 수 있습니다. 서비스는 [종속성 주입](xref:fundamentals/dependency-injection)을 통해 또는 [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices)에서 확인됩니다.

웹 호스트는 `Startup` 메서드가 호출되기 전에 일부 서비스를 구성할 수 있습니다. 세부 정보는 [호스팅](xref:fundamentals/hosting) 항목에서 제공됩니다. 

대부분의 설치가 필요한 기능의 경우 [IServiceCollection](/dotnet/api/Microsoft.Extensions.DependencyInjection.IServiceCollection)에 `Add[Service]` 확장 메서드가 있습니다. 일반적인 웹앱은 Entity Framework, ID 및 MVC에 대한 서비스를 등록합니다.

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?highlight=4,7,11&start=40&end=55)]

## <a name="services-available-in-startup"></a>시작 시 사용할 수 있는 서비스

웹 호스트는 `Startup` 클래스 생성자에 사용할 수 있는 몇 가지 서비스를 제공합니다. 앱은 `ConfigureServices`를 통해 추가 서비스를 추가합니다. 그러면 호스트와 앱 서비스 모두는 `Configure` 및 응용 프로그램 전체에서 사용할 수 있습니다.

## <a name="the-configure-method"></a>Configure 메서드

[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 메서드는 앱이 HTTP 요청에 응답하는 방식을 지정하는 데 사용됩니다. 요청 파이프라인은 [미들웨어](xref:fundamentals/middleware/index) 구성 요소를 [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) 인스턴스에 추가하여 구성됩니다. `IApplicationBuilder`는 `Configure` 메서드에 사용할 수 있지만 서비스 컨테이너에 등록되지 않습니다. 호스팅은 `IApplicationBuilder`를 만들고 `Configure`에 직접 전달합니다([참조 원본](https://github.com/aspnet/Hosting/blob/release/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/WebHost.cs#L179-L192)).

[ASP.NET Core 템플릿](/dotnet/core/tools/dotnet-new)은 개발자 예외 페이지, [BrowserLink](http://vswebessentials.com/features/browserlink), 오류 페이지, 정적 파일 및 ASP.NET MVC에 대한 지원으로 파이프라인을 구성합니다.

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Startup.cs?range=28-48&highlight=5,6,10,13,15)]

각 `Use` 확장 메서드는 요청 파이프라인에 미들웨어 구성 요소를 추가합니다. 예를 들어 `UseMvc` 확장 메서드는 [라우팅 미들웨어](xref:fundamentals/routing)를 요청 파이프라인에 추가하고 기본 처리기로 [MVC](xref:mvc/overview)를 구성합니다.

`IHostingEnvironment` 및 `ILoggerFactory`와 같은 추가 서비스는 메서드 서명에서 지정될 수도 있습니다. 지정되면 사용 가능한 경우 추가 서비스가 삽입됩니다.

`IApplicationBuilder`를 사용하는 방법에 대한 자세한 내용은 [미들웨어](xref:fundamentals/middleware/index)를 참조하세요.

## <a name="convenience-methods"></a>편리한 메서드

[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder.configureservices) 및 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure) 편의 메서드는 `Startup` 클래스 지정 대신 사용될 수 있습니다. `ConfigureServices`에 대한 여러 호출은 다른 것에 추가됩니다. `Configure`에 대한 여러 호출은 마지막 메서드 호출을 사용합니다.

[!code-csharp[Main](startup/snapshot_sample/Program.cs?highlight=18,22)]

## <a name="startup-filters"></a>시작 필터

[IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter)를 사용하여 앱의 [구성](#the-configure-method) 미들웨어 파이프라인의 시작 또는 끝에 미들웨어를 구성합니다. `IStartupFilter`는 미들웨어가 앱의 요청 처리 파이프라인의 시작 또는 끝에 라이브러리에 의해 추가되는 미들웨어 전이나 후에 실행되도록 하는데 유용합니다.

`IStartupFilter`는 `Action<IApplicationBuilder>`를 받고 반환하는 단일 메서드, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter.configure)를 구성합니다. [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder)는 앱의 요청 파이프라인을 구성하는 클래스를 정의합니다. 자세한 내용은 [IApplicationBuilder로 미들웨어 파이프라인 만들기](xref:fundamentals/middleware/index#creating-a-middleware-pipeline-with-iapplicationbuilder)를 참조하세요.

각 `IStartupFilter`는 요청 파이프라인에서 하나 이상의 미들웨어를 구현합니다. 필터는 서비스 컨테이너에 추가된 순서 대로 호출됩니다. 필터는 다음 필터에 컨트롤을 전달하기 전이나 후에 미들웨어를 추가할 수 있으므로 앱 파이프라인의 시작 또는 끝에 추가합니다.

[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/startup/sample/)([다운로드하는 방법](xref:tutorials/index#how-to-download-a-sample))은 `IStartupFilter`를 사용하여 미들웨어를 등록하는 방법을 보여 줍니다. 샘플 앱은 쿼리 문자열 매개 변수에서 옵션 값을 설정하는 미들웨어를 포함합니다.

[!code-csharp[Main](startup/sample/RequestSetOptionsMiddleware.cs?name=snippet1)]

`RequestSetOptionsMiddleware`는 `RequestSetOptionsStartupFilter` 클래스에서 구성됩니다.

[!code-csharp[Main](startup/sample/RequestSetOptionsStartupFilter.cs?name=snippet1&highlight=7)]

`IStartupFilter`는 `ConfigureServices`의 서비스 컨테이너에 등록됩니다.

[!code-csharp[Main](startup/sample/Startup.cs?name=snippet1&highlight=3)]

`option`에 대한 쿼리 문자열 매개 변수가 제공되는 경우 미들웨어는 MVC 미들웨어가 응답을 렌더링하기 전에 값 할당을 처리합니다.

![렌더링된 인덱스 페이지를 표시하는 브라우저 창 옵션의 값은 쿼리 문자열 매개 변수 및 'From Middleware'로 설정된 옵션의 값으로 페이지 요청에 따라 'From Middleware'로 렌더링됩니다.](startup/_static/index.png)

미들웨어 실행 순서는 `IStartupFilter` 등록 순서로 설정됩니다.

* 여러 `IStartupFilter` 구현은 동일한 개체와 상호 작용할 수 있습니다. 순서 지정이 중요한 경우 해당 미들웨어가 실행해야 하는 순서와 일치하도록 해당 `IStartupFilter` 서비스 등록의 순서를 지정합니다.
* 라이브러리는 `IStartupFilter`로 등록된 다른 앱 미들웨어 전이나 후에 실행하는 하나 이상의 `IStartupFilter` 구현으로 미들웨어를 추가할 수 있습니다. 라이브러리의 `IStartupFilter`에 의해 추가되는 미들웨어 전에 `IStartupFilter` 미들웨어를 호출하려면 라이브러리가 서비스 컨테이너에 추가되기 전에 서비스 등록의 위치를 지정합니다. 나중에 호출하려면 라이브러리가 추가된 후에 서비스 등록의 위치를 지정합니다.

## <a name="additional-resources"></a>추가 리소스

* [호스팅](xref:fundamentals/hosting)
* [여러 환경 사용](xref:fundamentals/environments)
* [미들웨어](xref:fundamentals/middleware/index)
* [로깅](xref:fundamentals/logging/index)
* [구성](xref:fundamentals/configuration/index)
* [StartupLoader 클래스: FindStartupType 메서드(참조 원본)](https://github.com/aspnet/Hosting/blob/rel/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/StartupLoader.cs#L66-L116)
