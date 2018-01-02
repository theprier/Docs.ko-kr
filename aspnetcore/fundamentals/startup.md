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
ms.openlocfilehash: dd2eb3d3996bc0bf277c8d5e772c8568ef9f147e
ms.sourcegitcommit: f5a7f0198628f0d152257d90dba6c3a0747a355a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2017
---
# <a name="application-startup-in-aspnet-core"></a>ASP.NET Core 응용 프로그램 시작

여 [Steve Smith](https://ardalis.com), [Tom Dykstra](https://github.com/tdykstra), 및 [Luke Latham](https://github.com/guardrex)

`Startup` 클래스 서비스 및 응용 프로그램의 요청 파이프라인을 구성 합니다.

## <a name="the-startup-class"></a>시작 클래스입니다.

ASP.NET Core 응용 프로그램 사용을 `Startup` 클래스 이름으로 지정 된 `Startup` 규칙에 따라 합니다. `Startup` 클래스:

* 선택적으로 포함할 수는 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 응용 프로그램의 서비스를 구성 하는 메서드.
* 포함 되어야 합니다는 [구성](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 방법을 응용 프로그램의 요청 처리 파이프라인을 만들 수 있습니다.

`ConfigureServices`및 `Configure` 앱 시작 시 런타임에 의해 호출 됩니다.

[!code-csharp[Main](startup/snapshot_sample/Startup1.cs)]

지정 된 `Startup` 클래스와 [WebHostBuilderExtensions](/dotnet/api/Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions) [UseStartup&lt;TStartup&gt; ](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 메서드:

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main&highlight=10)]

`Startup` 클래스 생성자는 호스트에 의해 정의 된 종속성을 허용 합니다. 일반적인 용도 [종속성 주입](xref:fundamentals/dependency-injection) 에 `Startup` 클래스를 삽입 하는 [IHostingEnvironment](/dotnet/api/Microsoft.AspNetCore.Hosting.IHostingEnvironment) 환경에서 서비스를 구성 하려면:

[!code-csharp[Main](startup/snapshot_sample/Startup2.cs)]

삽입 하는 대신 `IHostingStartup` 규칙 기반 접근 방식을 사용 하는 것입니다. 응용 프로그램을 별도 정의할 수 `Startup` 다양 한 환경에 대 한 클래스 (예를 들어 `StartupDevelopment`), 적절 한 시작 클래스는 런타임에 선택 됩니다. 해당 이름 접미사는 현재 환경에 적합 한 클래스 우선 순위가 부여 됩니다. 응용 프로그램 개발 환경에서 실행 되 고 모두를 포함 하는 경우는 `Startup` 클래스 및 `StartupDevelopment` 클래스는 `StartupDevelopment` 클래스가 사용 됩니다. 자세한 내용은 참조 [여러 환경 작업](xref:fundamentals/environments#startup-conventions)합니다.

에 대 한 자세한 내용은 `WebHostBuilder`, 참조는 [호스팅](xref:fundamentals/hosting) 항목입니다. 시작 하는 동안 오류를 처리 하는 방법은 참조 하십시오. [시작 예외 처리](xref:fundamentals/error-handling#startup-exception-handling)합니다.

## <a name="the-configureservices-method"></a>ConfigureServices 메서드

[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 방법은:

* 선택 사항입니다.
* 하기 전에 웹 호스트에 의해 호출 된 `Configure` 응용 프로그램의 서비스를 구성 하는 메서드.
* 여기서 [구성 옵션](xref:fundamentals/configuration/index) 규칙에 의해 설정 됩니다.

서비스 컨테이너에 서비스 추가 사용할 수 있도록 응용 프로그램 내에서 `Configure` 메서드. 서비스는를 통해 확인 [종속성 주입](xref:fundamentals/dependency-injection) 또는 [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices)합니다.

웹 호스트 되기 전에 일부 서비스를 구성할 수 있습니다 `Startup` 메서드가 호출 됩니다. 사용할 수 있는 세부 정보는 [호스팅](xref:fundamentals/hosting) 항목입니다. 

상당한 설치 해야 하는 기능을 위해 가지 `Add[Service]` 에 확장 메서드 [IServiceCollection](/dotnet/api/Microsoft.Extensions.DependencyInjection.IServiceCollection)합니다. Entity Framework, Id 및 MVC에 대 한 서비스를 등록 하는 일반적인 웹 앱:

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?highlight=4,7,11&start=40&end=55)]

## <a name="services-available-in-startup"></a>시작에 사용할 수 있는 서비스

에 사용할 수 있는 몇 가지 서비스를 제공 하는 웹 호스트는 `Startup` 클래스 생성자입니다. 응용 프로그램을 통해 추가 서비스를 추가 합니다. `ConfigureServices`합니다. 호스트와 응용 프로그램 서비스에서 사용할 수 있는 다음 `Configure` 및 응용 프로그램에 걸쳐 있습니다.

## <a name="the-configure-method"></a>Configure 메서드

[구성](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 메서드를 사용 하는 응용 프로그램 HTTP 요청에 응답 하는 방식을 지정 합니다. 요청 파이프라인을 추가 하 여 구성할 [미들웨어](xref:fundamentals/middleware) 구성 요소는 [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) 인스턴스. `IApplicationBuilder`사용할 수는 `Configure` 하지만 메서드를 서비스 컨테이너에 등록 되지 않았습니다. 호스팅 만듭니다는 `IApplicationBuilder` 에 직접 전달 `Configure` ([참조 소스](https://github.com/aspnet/Hosting/blob/release/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/WebHost.cs#L179-L192)).

[ASP.NET Core 템플릿](/dotnet/core/tools/dotnet-new) 개발자 예외 페이지를 지 원하는 파이프라인을 구성 [BrowserLink](http://vswebessentials.com/features/browserlink), 오류 페이지, 정적 파일 및 ASP.NET MVC:

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Startup.cs?range=28-48&highlight=5,6,10,13,15)]

각 `Use` 확장 메서드는 요청 파이프라인에 미들웨어 구성 요소를 추가 합니다. 예를 들어,는 `UseMvc` 추가 하는 확장 메서드는 [라우팅 미들웨어](xref:fundamentals/routing) 요청 파이프라인을 구성 및 [MVC](xref:mvc/overview) 기본 처리기로 합니다.

추가 서비스와 같은 `IHostingEnvironment` 및 `ILoggerFactory`, 메서드 서명에서 지정할 수도 있습니다. 을 지정 하면 사용 가능한 경우 추가 서비스는 삽입 합니다.

사용 하는 방법에 대 한 자세한 내용은 `IApplicationBuilder`, 참조 [미들웨어](xref:fundamentals/middleware)합니다.

## <a name="convenience-methods"></a>편리한 메서드

[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder.configureservices) 및 [구성](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure) 편의 메서드를 지정 하는 대신 사용할 수는 `Startup` 클래스입니다. 여러 번 호출 `ConfigureServices` 서로에 추가 합니다. 여러 번 호출 `Configure` 마지막 메서드 호출을 사용 합니다.

[!code-csharp[Main](startup/snapshot_sample/Program.cs?highlight=16,20)]

## <a name="startup-filters"></a>시작 필터

사용 하 여 [IStartupFilter](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter) 미들웨어를 구성 하는 시작 이나 끝 응용 프로그램의 [구성](#the-configure-method) 미들웨어 파이프라인. `IStartupFilter`미들웨어 실행 전이나 후 라이브러리 시작 부분이 나 끝의 응용 프로그램의 요청 처리 파이프라인에 의해 추가 되는 미들웨어 되도록 유용 합니다.

`IStartupFilter`단일 메서드를 구현 [구성](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter.configure)를 받아서 반환 하는 프로그램 `Action<IApplicationBuilder>`합니다. [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) 는 응용 프로그램의 요청 파이프라인을 구성 하는 클래스를 정의 합니다. 자세한 내용은 참조 [IApplicationBuilder 미들웨어 파이프라인 만들기](xref:fundamentals/middleware#creating-a-middleware-pipeline-with-iapplicationbuilder)합니다.

각 `IStartupFilter` 요청 파이프라인에서 하나 이상의 middlewares를 구현 합니다. 필터는 서비스 컨테이너에 추가 된 순서 대로 호출 됩니다. 미들웨어 하기 전에 행 필터를 추가할 수 있습니다 또는 제어 하 여 다음 필터를 통과 했으면 따라서은 추가 시작 또는 응용 프로그램 파이프라인의 끝에 있습니다.

[샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/startup/sample/) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample)) 사용 하 여 미들웨어를 등록 하는 방법을 보여 줍니다. `IStartupFilter`합니다. 샘플 응용 프로그램에서 쿼리 문자열 매개 변수 옵션 값을 설정 하는 미들웨어를 포함 되어 있습니다.

[!code-csharp[Main](startup/sample/RequestSetOptionsMiddleware.cs?name=snippet1)]

`RequestSetOptionsMiddleware` 에 구성 된 `RequestSetOptionsStartupFilter` 클래스:

[!code-csharp[Main](startup/sample/RequestSetOptionsStartupFilter.cs?name=snippet1&highlight=7)]

`IStartupFilter` 서비스 컨테이너에에 등록 되어 `ConfigureServices`:

[!code-csharp[Main](startup/sample/Startup.cs?name=snippet1&highlight=3)]

경우에 대 한 쿼리 문자열 매개 변수 `option` MVC 미들웨어의 응답을 렌더링 하기 전에 값 할당을 처리 하는 미들웨어 제공 됩니다.

![브라우저 창에 렌더링된 된 인덱스 페이지를 표시 합니다. 옵션의 값으로 ' 미들웨어에서 ' 요청 쿼리 문자열 매개 변수 및 값 ' 미들웨어에서 '로 설정 된 옵션을 사용 하 여 페이지에 따라 렌더링 됩니다.](startup/_static/index.png)

순서 여 미들웨어 실행 순서 설정 되어 `IStartupFilter` 등록:

* 여러 `IStartupFilter` 구현을 동일한 개체를 조작할 수 있습니다. 정렬 순서가 중요 한 경우 해당 `IStartupFilter` 서비스 자신의 middlewares 실행 해야 하는 순서와 일치 하도록 등록 합니다.
* 라이브러리에서 하나 이상의 미들웨어를 추가할 수 있습니다. `IStartupFilter` 전 또는 다른 응용 프로그램 미들웨어에 등록 한 후에 실행 하는 구현 `IStartupFilter`합니다. 호출 하는 `IStartupFilter` 미들웨어는 라이브러리에 의해 추가 하기 전에 미들웨어 `IStartupFilter`, 라이브러리 서비스 컨테이너에 추가 되기 전에 서비스 등록 위치를 지정 합니다. 라이브러리를 추가한 후 나중에 호출할 서비스 등록을 배치 합니다.

## <a name="additional-resources"></a>추가 리소스

* [호스팅](xref:fundamentals/hosting)
* [여러 환경 사용](xref:fundamentals/environments)
* [미들웨어](xref:fundamentals/middleware)
* [로깅](xref:fundamentals/logging/index)
* [구성](xref:fundamentals/configuration/index)
* [StartupLoader 클래스: FindStartupType 메서드 (참조 소스)](https://github.com/aspnet/Hosting/blob/rel/2.0.0/src/Microsoft.AspNetCore.Hosting/Internal/StartupLoader.cs#L66-L116)
