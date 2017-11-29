---
title: "ASP.NET Core 응용 프로그램의 Startup 클래스"
author: ardalis
description: "ASP.NET Core 시작 클래스에서 서비스 및 응용 프로그램의 요청 파이프라인을 구성 하는 방법을 검색 합니다."
keywords: "ASP.NET Core, 시작, 구성 메서드, ConfigureServices 메서드"
ms.author: tdykstra
manager: wpickett
ms.date: 02/29/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/startup
ms.openlocfilehash: bba0eafe3917fa850b3a07df8df6448409f4062d
ms.sourcegitcommit: 732cd2684246e49e796836596643a8d37e20c46d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2017
---
# <a name="application-startup-in-aspnet-core"></a>ASP.NET Core 응용 프로그램의 Startup 클래스

작성자: [Steve Smith](https://ardalis.com/) 및 [Tom Dykstra](https://github.com/tdykstra/)

`Startup` 클래스는 서비스와 응용 프로그램의 요청 파이프라인을 구성합니다.

## <a name="the-startup-class"></a>Startup 클래스

ASP.NET Core 응용 프로그램에는 반드시 시작 클래스가 존재해야 하며, 이 클래스는 관례상 `Startup`이라는 이름을 사용합니다. `Main` 프로그램에서 [WebHostBuilderExtensions](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderextensions)의 [`UseStartup<TStartup>`](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_)을 호출할 때, 다른 시작 클래스 이름을 지정할 수도 있습니다. `WebHostBuilder`는 `Startup`보다 먼저 실행되는데, 보다 자세한 내용은 [호스팅](xref:fundamentals/hosting)을 참고하시기 바랍니다.

각 환경마다 별도의 `Startup` 클래스를 정의할 수 있으며, 그 경우 런타임에 적절한 클래스가 선택됩니다. [WebHost 구성](https://docs.microsoft.com/aspnet/core/fundamentals/hosting?tabs=aspnetcore2x#configuring-a-host)이나 옵션에서 `startupAssembly`를 지정하면, 호스팅이 지정한 시작 어셈블리를 로드한 다음, `Startup` 또는 `Startup[Environment]` 형식을 찾습니다. 이때, 클래스 이름의 접미사와 현재 환경이 일치하는 클래스의 우선 순위가 높기 때문에, 만약 응용 프로그램이 *Development* 환경에서 실행되고 있고 시작 어셈블리에 `Startup` 클래스와 `StartupDevelopment` 클래스가 모두 존재한다면, `StartupDevelopment` 클래스가 사용됩니다. 더 자세한 정보는 `StartupLoader`의 [FindStartupType](https://github.com/aspnet/Hosting/blob/rel/1.1.0/src/Microsoft.AspNetCore.Hosting/Internal/StartupLoader.cs)와 [다양한 환경에서 작업하기](environments.md#startup-conventions)를 참고하시기 바랍니다. 

또는, `UseStartup<TStartup>`를 호출해서 환경과 무관하게 사용되는 고정 `Startup` 클래스를 정의할 수도 있으며, 이 방식을 권장합니다.

`Startup` 클래스의 생성자는 [종속성 주입](xref:fundamentals/dependency-injection)을 통해서 제공되는 종속성을 전달받을 수 있습니다. 일반적인 방식은 `IHostingEnvironment`를 이용해서 [구성](xref:fundamentals/configuration) 원본을 설정하는 것입니다.

`Startup` 클래스에는 반드시 `Configure` 메서드가 존재해야 하며, 필요에 따라 `ConfigureServices` 메서드가 포함될 수도 있는데, 이 두 메서드 모두 응용 프로그램이 구동될 때 호출됩니다. 또한 Startup 클래스에는 [이 메서드들의 환경별 버전](xref:fundamentals/environments#startup-conventions)이 포함될 수도 있습니다. `ConfigureServices` 메서드가 존재할 경우, `Configure` 메서드보다 먼저 호출됩니다.

[응용 프로그램이 시작되는 동안 발생하는 예외를 처리](xref:fundamentals/error-handling#startup-exception-handling)하는 방법에 관해서도 살펴보시기 바랍니다.

## <a name="the-configureservices-method"></a>ConfigureServices 메서드

[ConfigureServices](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.startupbase#Microsoft_AspNetCore_Hosting_StartupBase_ConfigureServices_Microsoft_Extensions_DependencyInjection_IServiceCollection_) 메서드는 선택 사항이지만, 존재할 경우 웹 호스트에 의해 `Configure` 메서드보다 먼저 호출됩니다. 웹 호스트는 `Startup`의 메서드들이 호출되기 전에 일부 서비스들을 구성할 수도 있습니다 ([호스팅 참고](xref:fundamentals/hosting)). 규약에 따라 [구성 옵션](xref:fundamentals/configuration)은 이 메서드에서 설정됩니다.

각 기능들에 필요한 실질적인 설정은 [IServiceCollection](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.dependencyinjection.iservicecollection)의 `Add[Service]` 확장 메서드를 통해서 수행됩니다. 기본 웹 사이트 템플릿에서 가져온 다음 예제는 응용 프로그램에서 Entity Framework, Identity 및 MVC 서비스를 사용하도록 구성합니:

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?highlight=4,7,11&start=40&end=55)]

이 메서드에서 서비스들을 서비스 컨테이너에 추가하면 [종속성 주입](xref:fundamentals/dependency-injection)을 이용해서 응용 프로그램에서 해당 서비스들을 사용할 수 있습니다.

## <a name="services-available-in-startup"></a>Startup에서 사용할 수 있는 서비스

ASP.NET Core의 종속성 주입은 응용 프로그램이 구동되는 동안에도 서비스를 제공합니다. 따라서 `Startup` 클래스의 생성자나 `Configure` 메서드의 매개 변수로 적절한 인터페이스를 지정해서 서비스를 요청할 수 있습니다. `ConfigureServices` 메서드는 `IServiceCollection` 매개 변수만 전달받습니다 (그러나 이 컬렉션에 등록된 모든 서비스를 가져올 수 있기 때문에, 추가적인 매개 변수는 필요 없습니다.).

다음은 일반적으로 `Startup`의 메서드에서 요청하는 서비스입니다:

* 생성자: `IHostingEnvironment`, `ILogger<Startup>`
* `ConfigureServices` 메서드: `IServiceCollection`
* `Configure` 메서드: `IApplicationBuilder`, `IHostingEnvironment`, `ILoggerFactory`

`WebHostBuilder`의 `ConfigureServices`로 추가된 모든 서비스들은 `Startup` 클래스의 생성자나 `Configure` 메서드에서 요청할 수 있습니다. `WebHostBuilder`를 사용해서 `Startup`의 메서드에서 필요한 서비스들을 제공할 수 있습니다.

## <a name="the-configure-method"></a>Configure 메서드

`Configure` 메서드는 ASP.NET Core 응용 프로그램이 HTTP 요청에 응답하는 방식을 지정합니다. 요청 파이프라인은 종속성 주입으로 제공된 `IApplicationBuilder`의 인스턴스에 [미들웨어](middleware.md) 구성 요소들을 추가함으로써 구성됩니다.

기본 웹 사이트 템플릿에서 가져온 다음 예제는, 몇 가지 확장 메서드를 이용해서 [BrowserLink](http://vswebessentials.com/features/browserlink), 오류 페이지, 정적 파일, ASP.NET MVC 및 Identity를 지원하는 파이프라인을 구성합니다:

[!code-csharp[Main](../common/samples/WebApplication1/Startup.cs?highlight=8,9,10,14,17,19,21&start=58&end=84)]

각각의 `Use` 확장 메서드는 요청 파이프라인에 [미들웨어](xref:fundamentals/middleware) 구성 요소를 추가합니다. 예를 들어서, `UseMvc` 확장 메서드는 요청 파이프라인에 [라우팅](routing.md) 미들웨어를 추가하고 [MVC](xref:mvc/overview)를 기본 처리기로 구성합니다.

`IApplicationBuilder`를 사용하는 자세한 방법은 [미들웨어](xref:fundamentals/middleware)를 참고하시기 바랍니다.

또한 `IHostingEnvironment`나 `ILoggerFactory` 같은 추가적인 서비스들을 메서드 시그니처에 지정할 수도 있으며, 해당 서비스를 사용할 수 있는 경우 지정한 서비스가 [주입](dependency-injection.md)됩니다.

## <a name="additional-resources"></a>추가 자료

* [다양한 환경에서 작업하기](xref:fundamentals/environments)
* [미들웨어](xref:fundamentals/middleware)
* [로깅](xref:fundamentals/logging)
* [구성](xref:fundamentals/configuration)
