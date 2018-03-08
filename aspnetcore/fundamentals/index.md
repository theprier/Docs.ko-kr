---
title: "ASP.NET Core 기본 사항"
author: rick-anderson
description: "ASP.NET Core 응용 프로그램을 구축하기 위한 기본적인 개념을 알아봅니다."
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 09/30/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: fundamentals/index
ms.openlocfilehash: be37df7789354ac4ce8e373a1560366be157ffa5
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="aspnet-core-fundamentals"></a>ASP.NET Core 기본 사항

ASP.NET Core 응용 프로그램은 `Main` 메서드에서 웹 서버를 생성하는 콘솔 앱입니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[!code-csharp[](../getting-started/sample/aspnetcoreapp/Program2x.cs)]

`Main` 메서드는 빌드 패턴에 따라 웹 응용 프로그램 호스트를 생성하는 `WebHost.CreateDefaultBuilder` 를 호출합니다. 이 빌더는 웹 서버를 정의하거나 (예: `UseKestrel`) 시작 클래스를 정의하는 (`UseStartup`) 메서드들을 제공합니다. 위의 예제에서는 기본적으로 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버가 할당되며. 가능하다면 ASP.NET Core의 웹 호스트는 IIS에서 실행하려고 시도합니다. 그러나 적절한 확장 메서드를 호출해서 [HTTP.sys](xref:fundamentals/servers/httpsys) 같은 다른 웹 서버를 사용할 수도 있습니다. `UseStartup` 에 관해서는 다음 섹션에서 더 자세히 살펴봅니다.

`WebHost.CreateDefaultBuilder` 호출로부터 반환되는 `IWebHostBuilder`형식은 다양한 선택적 메서드를 제공합니다. 이 메서드들 중에는 HTTP.sys에서 앱을 호스트하기 위한 `UseHttpSys` 및 루트 콘텐츠 디렉터리를 지정하기 위한 `UseContentRoot`도 포함되어 있습니다. `Build` 및 `Run` 메서드는 앱을 호스트하고 HTTP 요청의 수신 대기를 시작하는 `IWebHost` 개체를 빌드합니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[!code-csharp[](../getting-started/sample/aspnetcoreapp/Program.cs)]

`Main` 메서드는 빌드 패턴에 따라 웹 응용 프로그램 호스트를 만드는 `WebHostBuilder`를 사용합니다. 이 빌더는 웹 서버를 정의하거나 (예: `UseKestrel`) 시작 클래스를 정의하는(`UseStartup`)메서드들을 제공합니다. 위의 예제에서는 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버를 사용하고 있습니다. [WebListener](xref:fundamentals/servers/weblistener) 같은 다른 웹 서버를 사용할 수도 있습니다. `UseStartup`에 관해서는 다음 섹션에서 더 자세히 살펴봅니다.

`WebHostBuilder`는 IIS 및 IIS Express에서 호스팅하기 위한 `UseIISIntegration` 확장 메서드 및 루트 콘텐츠 디렉터리를 지정하기 위한 `UseContentRoot`확장 메서드를 비롯한 다양한 선택적 메서드를 제공합니다. `Build` 및 `Run` 메서드는 앱을 호스트하고 HTTP 요청의 수신 대기를 시작하는 `IWebHost` 개체를 빌드합니다.

---

## <a name="startup"></a>Startup 클래스

`WebHostBuilder`의 `UseStartup` 메서드는 앱의 `Startup` 클래스를 지정합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[!code-csharp[](../getting-started/sample/aspnetcoreapp/Program2x.cs?highlight=10&range=6-17)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[!code-csharp[](../getting-started/sample/aspnetcoreapp/Program.cs?highlight=7&range=6-17)]

---

`Startup` 클래스는 요청 처리 파이프라인을 정의하고 앱에 필요한 모든 서비스를 구성하는 곳입니다. `Startup` 클래스는 public으로 지정해야 하며 다음과 같은 메서드들을 제공해야 합니다.

```csharp
public class Startup
{
    // This method gets called by the runtime. Use this method
    // to add services to the container.
    public void ConfigureServices(IServiceCollection services)
    {
    }

    // This method gets called by the runtime. Use this method
    // to configure the HTTP request pipeline.
    public void Configure(IApplicationBuilder app)
    {
    }
}
```

`ConfigureServices`는 앱에서 사용되는 [서비스](#dependency-injection-services)를 정의합니다 (예, ASP.NET MVC Core MVC, Entity Framework Core, Identity). 그리고`Configure`는 요청 파이프라인의 [미들웨어](xref:fundamentals/middleware/index)를 정의.

자세한 내용은 [응용 프로그램 시작](xref:fundamentals/startup)을 참고하시기 바랍니다.

## <a name="content-root"></a>콘텐츠 루트

콘텐츠 루트는 앱에서 사용되는 뷰, [Razor 페이지](xref:mvc/razor-pages/index) 및 정적 자산 같은 모든 콘텐츠의 기본 경로입니다. 기본적으로 콘텐츠 루트는 앱을 호스팅하는 실행 파일의 응용 프로그램 기본 경로와 동일합니다. 

## <a name="web-root"></a>웹 루트

앱의 웹 루트는 CSS, JavaScript 및 이미지 파일 같은 공용 정적 리소스가 위치하는 프로젝트의 디렉터리입니다.

## <a name="dependency-injection-services"></a>종속성 주입(서비스)

서비스는 앱에서 공통으로 사용하기 위해 설계된 구성 요소입니다. 서비스는 DI([종속성 주입](xref:fundamentals/dependency-injection))를 통해서 사용됩니다. ASP.NET Core에는 기본적으로 [생성자 주입](xref:mvc/controllers/dependency-injection#constructor-injection)을 지원하는 네이티브 IoC(**I**nversion **o**f **C**) 컨테이너가 포함되어 있습니다. 만약 원한다면 기본 네이티브 컨테이너를 교체할 수도 있습니다. DI를 사용하면 느슨한 결합의 이점을 얻을 수 있을 뿐만 아니라, 앱 전체에서 서비스를 사용할 수 있습니다(예: [로깅](xref:fundamentals/logging/index)).

자세한 내용은 [종속성 주입](xref:fundamentals/dependency-injection)을 참고하시기 바랍니다.

## <a name="middleware"></a>미들웨어

ASP.NET Core는 [미들웨어](xref:fundamentals/middleware/index)를 사용해서 요청 파이프라인을 구성합니다. ASP.NET Core의 미들웨어는 `HttpContext` 상에서 비동기 논리를 수행한 다음, 시퀀스 상의 다음 미들웨어를 호출하거나 그대로 요청을 종료합니다. 일반적으로 "XYZ"라는 미들웨어 구성 요소는 `Configure` 메서드에서 `UseXYZ` 확장 메서드를 호출하는 방식으로 추가됩니다.

ASP.NET Core는 다양한 기본 제공 미들웨어들을 함께 제공합니다.

* [정적 파일](xref:fundamentals/static-files)
* [라우팅](xref:fundamentals/routing)
* [인증](xref:security/authentication/index)
* [응답 압축 미들웨어](xref:performance/response-compression)
* [URL 재작성 미들웨어](xref:fundamentals/url-rewriting)

ASP.NET Core 앱에서 [OWIN](http://owin.org) 기반 미들웨어를 사용할 수 있으며, 직접 자신의 사용자 지정 미들웨어를 작성할 수도 있습니다.

자세한 내용은 [미들웨어](xref:fundamentals/middleware/index) 및 [OWIN(Open Web Interface for .NET)](xref:fundamentals/owin)을 참고하시기 바랍니다.

## <a name="environments"></a>환경

"Development" 및 "Production" 같은 환경은 ASP.NET Core의 일급 개념으로, 환경 변수를 통해서 설정할 수 있습니다.

자세한 내용은 [다양한 환경에서 작업하기](xref:fundamentals/environments)를 참고하시기 바랍니다.

## <a name="configuration"></a>구성

ASP.NET Core는 이름 값 쌍에 기반을 둔 구성 모델을 사용합니다.  이 구성 모델은 `System.Configuration` 이나 *web.config*를 기반으로 하지 않습니다. 구성은 정렬된 구성 공급자 집합에서 설정을 가져옵니다. 기본으로 제공되는 구성 공급자는 환경 기반 구성을 가능하게 해주는 다양한 파일 형식(XML, JSON, INI)과 환경 변수를 지원합니다. 또는 직접 자신의 사용자 지정 구성 공급자를 작성할 수도 있습니다.

자세한 내용은 [구성](xref:fundamentals/configuration/index)을 참고하시기 바랍니다.

## <a name="logging"></a>로깅

ASP.NET Core는 다양한 로깅 공급자를 사용하는 로깅 API를 지원합니다. 기본으로 제공되는 공급자는 하나 이상의 대상에 로그를 전송할 수 있습니다. 타사의 로깅 프레임워크를 사용할 수도 있습니다.

자세한 내용은[로깅](xref:fundamentals/logging/index)을 참고하시기 바랍니다.

## <a name="error-handling"></a>오류 처리

ASP.NET Core는 앱에서 오류를 처리하기 위한 개발자 예외 페이지, 사용자 지정 오류 페이지, 정적 상태 코드 페이지 및 시작 예외 처리 등의 기본 제공 기능을 지원합니다.

자세한 내용은 [오류 처리](xref:fundamentals/error-handling)를 참고하시기 바랍니다.

## <a name="routing"></a>라우팅

ASP.NET Core는 응용 프로그램 요청을 경로 처리기로 라우팅하는 기능을 제공합니다.

자세한 내용은 [라우팅](xref:fundamentals/routing)을 참조하세요.

## <a name="file-providers"></a>파일 공급자

ASP.NET Core는 파일 공급자를 사용하여 파일 시스템 액세스를 추상화하고 플랫폼에서 파일을 사용하기 위한 공통 인터페이스를 제공합니다.

자세한 내용은 [파일 공급자](xref:fundamentals/file-providers)를 참고하시기 바랍니다.

## <a name="static-files"></a>정적 파일

정적 파일 미들웨어는 HTML, CSS, 이미지, JavaScript 등의 정적 파일을 제공합니다.

자세한 내용은 [고정 파일 작업](xref:fundamentals/static-files)을 참고하시기 바랍니다.

## <a name="hosting"></a>호스팅

ASP.NET Core 앱은 앱의 시작과 수명 관리를 담당하는 *호스트*를 구성하고 실행합니다.

자세한 내용은 [호스팅](xref:fundamentals/hosting)을 참조하세요.

## <a name="session-and-application-state"></a>세션 및 응용 프로그램 상태

세션 상태는 사용자가 웹앱을 탐색하는 동안 사용자 데이터를 저장하는 데 사용할 수 있는 ASP.NET Core의 기능입니다.

자세한 내용은 [세션 및 응용 프로그램 상태](xref:fundamentals/app-state)를 참고하시기 바랍니다.

## <a name="servers"></a>서버

ASP.NET Core의 호스팅 모델은 요청을 직접 수신하지 않습니다.  대신 호스팅 모델은 HTTP 서버 구현에 의존해서 요청을 앱에 전달합니다. 전달된 요청은 인터페이스를 통해서 접근할 수 있는 기능 개체 집합으로 래핑됩니다. ASP.NET Core에는 [Kestrel](xref:fundamentals/servers/kestrel)이라는 관리되는 크로스 플랫폼 웹 서버가 포함되어 있습니다. 일반적으로 Kestrel은 [IIS](https://www.iis.net/) 또는 [Nginx](http://nginx.org)같은 프로덕션 웹 서버의 뒤에서 실행됩니다. Kestrel은 에지 서버로 실행될 수 있습니다.

자세한 내용은 [서버](xref:fundamentals/servers/index) 및 다음 항목을 참고하시기 바랍니다.

* [Kestrel](xref:fundamentals/servers/kestrel)
* [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)
* [HTTP.sys](xref:fundamentals/servers/httpsys)(구 [WebListener](xref:fundamentals/servers/weblistener))

## <a name="globalization-and-localization"></a>전역화 및 지역화

ASP.NET Core를 사용해서 다국어 웹 사이트를 만들면 더 광범위한 사용자가 사이트를 사용할 수 있습니다. ASP.NET Core는 다른 언어 및 문화권의 지역화를 위한 서비스 및 미들웨어를 제공합니다.

자세한 내용은 [전역화 및 지역화](xref:fundamentals/localization)를 참조하세요.

## <a name="request-features"></a>요청 기능

웹 서버 구현은 HTTP 요청과 관련하여 설명되고 응답은 인터페이스에서 정의됩니다. 이 인터페이스들은 서버 구현 및 미들웨어에서 앱의 호스팅 파이프라인을 만들고 수정하기 위해 사용됩니다.

자세한 내용은 [요청 기능](xref:fundamentals/request-features)을 참고하시기 바랍니다.

## <a name="background-tasks"></a>백그라운드 작업

백그라운드 작업은 *호스티드 서비스*로 구현됩니다. 호스티드 서비스는 [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 인터페이스를 구현하는 백그라운드 작업 논리가 있는 클래스입니다.

자세한 내용은 [호스티드 서비스를 사용하는 백그라운드 작업](xref:fundamentals/hosted-services)을 참조하세요.

## <a name="open-web-interface-for-net-owin"></a>OWIN(Open Web Interface for .NET)

ASP.NET Core는 OWIN(Open Web Interface for .NET)을 지원합니다. OWIN을 사용하면 웹 앱을 웹 서버에서 분리할 수 있습니다.

자세한 내용은 [OWIN(Open Web Interface for .NET)](xref:fundamentals/owin)을 참조하세요.

## <a name="websockets"></a>WebSocket

[WebSocket](https://wikipedia.org/wiki/WebSocket)은 TCP 연결을 통한 영구 양방향 통신 채널을 사용하도록 설정하는 프로토콜이며 WebSocket은 채팅, 주식 시세, 게임 등 웹 앱에서 실시간 기능이 필요한 모든 곳에 사용됩니다. ASP.NET Core는 WebSocket 기능을 지원합니다.

자세한 내용은 [WebSocket](xref:fundamentals/websockets)을 참조하세요.

## <a name="microsoftaspnetcoreall-metapackage"></a>Microsoft.AspNetCore.All 메타패키지

ASP.NET Core에 대한 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 메타패키지는 다음을 포함합니다.

* ASP.NET Core 팀에서 지원되는 모든 패키지
* Entity Framework Core에서 지원되는 모든 패키지 
* ASP.NET Core 및 Entity Framework Core에서 사용하는 내부 및 타사 종속성

자세한 내용은 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)를 참고하시기 바랍니다.

## <a name="net-core-vs-net-framework-runtime"></a>.NET Core 및 .NET Framework 런타임

ASP.NET Core 앱은 .NET Core 또는 .NET Framework 런타임을 대상으로 할 수 있습니다.

자세한 내용은 [.NET Core와 .NET Framework  중에 선택하기](/dotnet/articles/standard/choosing-core-framework-server)을 참고하시기 바랍니다.

## <a name="choose-between-aspnet-core-and-aspnet"></a>ASP.NET Core와 ASP.NET 중에서 선택하기

ASP.NET Core와 ASP.NET 중에서 선택하는 방법에 대한 자세한 내용은 [ASP.NET Core 및 ASP.NET 중에서 선택하기](xref:fundamentals/choose-between-aspnet-and-aspnetcore)를 참고하시기 바랍니다.
