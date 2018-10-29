---
title: ASP.NET Core 기본 사항
author: rick-anderson
description: ASP.NET Core 앱을 구축하기 위한 기본적인 개념을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 10/25/2018
uid: fundamentals/index
ms.openlocfilehash: ab140051648c1640b3c4f382bfd8201c5c0c2039
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207474"
---
# <a name="aspnet-core-fundamentals"></a>ASP.NET Core 기본 사항

ASP.NET Core 앱은 `Program.Main` 메서드에서 웹 서버를 생성하는 콘솔 앱입니다. `Main` 메서드는 앱의 *관리 진입점*입니다.

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/snapshots/2.x/Program.cs)]

.NET Core 호스트:

* [.NET Core 런타임](https://github.com/dotnet/coreclr)을 로드합니다.
* 첫 번째 명령줄 인수를 진입점(`Main`)을 포함하는 관리되는 이진 경로로 사용하고 코드 실행을 시작합니다.

`Main` 메서드는 [빌드 패턴](https://wikipedia.org/wiki/Builder_pattern)에 따라 웹 응용 프로그램 호스트를 생성하는 [WebHost.CreateDefaultBuilder](xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*)를 호출합니다. 이 빌더는 웹 서버를 정의하거나 (예: <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*>) 시작 클래스를 정의하는 (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*>) 메서드들을 제공합니다. 위의 예제에서는 기본적으로 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버가 할당되며. 가능하다면 ASP.NET Core의 웹 호스트는 IIS에서 실행하려고 시도합니다. 그러나 적절한 확장 메서드를 호출해서 [HTTP.sys](xref:fundamentals/servers/httpsys) 같은 다른 웹 서버를 사용할 수도 있습니다. `UseStartup` 에 관해서는 다음 섹션에서 더 자세히 살펴봅니다.

`WebHost.CreateDefaultBuilder` 호출로부터 반환되는 <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder>형식은 다양한 선택적 메서드를 제공합니다. 이 메서드들 중에는 HTTP.sys에서 앱을 호스트하기 위한 `UseHttpSys` 및 루트 콘텐츠 디렉터리를 지정하기 위한 <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseContentRoot*>도 포함되어 있습니다. <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.Build*> 및 <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> 메서드는 앱을 호스트하고 HTTP 요청의 수신 대기를 시작하는 <xref:Microsoft.AspNetCore.Hosting.IWebHost> 개체를 빌드합니다.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/snapshots/1.x/Program.cs)]

.NET Core 호스트:

* [.NET Core 런타임](https://github.com/dotnet/coreclr)을 로드합니다.
* 첫 번째 명령줄 인수를 진입점(`Main`)을 포함하는 관리되는 이진 경로로 사용하고 코드 실행을 시작합니다.

`Main` 메서드는 [빌드 패턴](https://wikipedia.org/wiki/Builder_pattern)에 따라 웹앱 호스트를 만드는 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>를 사용합니다. 이 빌더는 웹 서버를 정의하거나 (예: <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*>) 시작 클래스를 정의하는 (<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*>) 메서드들을 제공합니다. 위의 예제에서는 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버를 사용하고 있습니다. [WebListener](xref:fundamentals/servers/weblistener) 같은 다른 웹 서버를 사용할 수도 있습니다. `UseStartup`에 관해서는 다음 섹션에서 더 자세히 살펴봅니다.

`WebHostBuilder`는 IIS 및 IIS Express에서 호스팅하기 위한 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> 확장 메서드 및 루트 콘텐츠 디렉터리를 지정하기 위한 <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseContentRoot*>확장 메서드를 비롯한 다양한 선택적 메서드를 제공합니다. <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder.Build*> 및 <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*> 메서드는 앱을 호스트하고 HTTP 요청의 수신 대기를 시작하는 <xref:Microsoft.AspNetCore.Hosting.IWebHost> 개체를 빌드합니다.

::: moniker-end

## <a name="startup"></a>Startup 클래스

`WebHostBuilder`의 `UseStartup` 메서드는 앱의 `Startup` 클래스를 지정합니다.

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/snapshots/2.x/Program.cs?highlight=10)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/snapshots/1.x/Program.cs?highlight=7)]

::: moniker-end

`Startup` 클래스는 요청 처리 파이프라인을 정의하고 앱에 필요한 모든 서비스를 구성하는 곳입니다. `Startup` 클래스는 public으로 지정해야 하며 다음과 같은 메서드들을 제공해야 합니다.

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/snapshots/2.x/Startup.cs)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/snapshots/1.x/Startup.cs)]

::: moniker-end

<xref:Microsoft.AspNetCore.Hosting.IStartup.ConfigureServices*>는 앱에서 사용되는 [서비스](#dependency-injection-services)를 정의합니다 (예, ASP.NET MVC Core MVC, Entity Framework Core, Identity). <xref:Microsoft.AspNetCore.Hosting.IStartup.Configure*>는 요청 파이프라인에서 호출되는 [미들웨어](xref:fundamentals/middleware/index)를 정의합니다.

자세한 내용은 <xref:fundamentals/startup>을 참조하세요.

## <a name="content-root"></a>콘텐츠 루트

콘텐츠 루트는 앱에서 사용되는 [Razor Pages](xref:razor-pages/index), MVC 보기, 정적 자산 같은 콘텐츠의 기본 경로입니다. 기본적으로 콘텐츠 루트는 앱을 호스팅하는 실행 파일의 앱 기본 경로와 동일한 위치입니다. 

## <a name="web-root-webroot"></a>웹 루트(webroot)

앱의 웹 루트는 CSS, JavaScript 및 이미지 파일과 같은 공용, 정적 리소스를 포함하는 프로젝트의 디렉터리입니다. 기본적으로 *wwwroot*는 웹 루트입니다.

Razor(*.cshtml*) 파일의 경우 물결표 슬래시 `~/`가 웹 루트를 가리킵니다. `~/`에서 시작하는 경로를 가상 경로라고 합니다.

## <a name="dependency-injection-services"></a>종속성 주입(서비스)

*서비스*는 앱에서 공통으로 사용하기 위한 구성 요소입니다. 서비스는 DI([종속성 주입](xref:fundamentals/dependency-injection))를 통해서 사용됩니다. ASP.NET Core에는 기본적으로 [생성자 주입](xref:mvc/controllers/dependency-injection#constructor-injection)을 지원하는 네이티브 IoC(Inversion of Control) 컨테이너가 포함되어 있습니다. 만약 원한다면 기본 컨테이너를 교체할 수 있습니다. DI를 사용하면 [느슨한 결합의 이점](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#encapsulation)을 얻을 수 있을 뿐만 아니라, 앱 전체에서 [로깅](xref:fundamentals/logging/index) 같은 서비스를 사용할 수 있습니다.

자세한 내용은 <xref:fundamentals/dependency-injection>을 참조하세요.

## <a name="middleware"></a>미들웨어

ASP.NET Core는 [미들웨어](xref:fundamentals/middleware/index)를 사용해서 요청 파이프라인을 구성합니다. ASP.NET Core 미들웨어는 `HttpContext` 상에서 비동기 작업을 수행한 다음, 파이프라인의 다음 미들웨어를 호출하거나 요청을 종료합니다.

규칙에 따라, "XYZ"라는 미들웨어 구성 요소는 `Configure` 메서드에서 `UseXYZ` 확장 메서드를 호출하여 파이프라인에 추가됩니다.

ASP.NET Core는 풍부한 기본 미들웨어 집합을 포함하고 있으며, 자신만의 사용자 지정 미들웨어를 작성할 수 있습니다. 웹 서버에서 웹앱을 분리할 수 있게 해주는 [OWIN(Open Web Interface for .NET)](xref:fundamentals/owin)은 ASP.NET Core 앱에서 지원됩니다.

자세한 내용은 <xref:fundamentals/middleware/index> 및 <xref:fundamentals/owin>를 참조하세요.

::: moniker range=">= aspnetcore-2.1"

## <a name="initiate-http-requests"></a>HTTP 요청 시작

<xref:System.Net.Http.IHttpClientFactory>를 사용하여 HTTP 요청을 만드는 <xref:System.Net.Http.HttpClient> 인스턴스에 액세스할 수 있습니다.

자세한 내용은 <xref:fundamentals/http-requests>을 참조하세요.

::: moniker-end

## <a name="environments"></a>환경

*개발* 및 *프로덕션* 같은 환경은 ASP.NET Core의 일급 개념이며 환경 변수, 설정 파일, 명령줄 인수를 사용하여 설정할 수 있습니다.

자세한 내용은 <xref:fundamentals/environments>을 참조하세요.

## <a name="hosting"></a>호스팅

ASP.NET Core 앱은 앱의 시작과 수명 관리를 담당하는 *호스트*를 구성하고 실행합니다.

자세한 내용은 <xref:fundamentals/host/index>을 참조하세요.

## <a name="servers"></a>서버

ASP.NET Core의 호스팅 모델은 요청을 직접 수신하지 않습니다.  대신 호스팅 모델은 HTTP 서버 구현에 의존해서 요청을 앱에 전달합니다. 전달된 요청은 인터페이스를 통해서 접근할 수 있는 기능 개체 집합으로 래핑됩니다. ASP.NET Core에는 [Kestrel](xref:fundamentals/servers/kestrel)이라는 관리되는 크로스 플랫폼 웹 서버가 포함되어 있습니다. Kestrel은 일반적으로 역방향 프록시 구성의 [IIS](https://www.iis.net/) 또는 [Nginx](http://nginx.org) 같은 프로덕션 웹 서버 뒤에서 실행됩니다. kestrel은 ASP.NET Core 2.0 이상에서 인터넷에 직접 공개되는 공용 에지 서버로 실행할 수도 있습니다.

자세한 내용은 <xref:fundamentals/servers/index>을 참조하세요.

## <a name="configuration"></a>구성

ASP.NET Core는 이름 값 쌍에 기반을 둔 구성 모델을 사용합니다.  이 구성 모델은 <xref:System.Configuration> 이나 *web.config*를 기반으로 하지 않습니다. 구성은 정렬된 구성 공급자 집합에서 설정을 가져옵니다. 기본적으로 제공되는 구성 공급자는 다양한 파일 형식(XML, JSON, INI), 환경 변수 및 명령줄 인수를 지원합니다. 또는 직접 자신의 사용자 지정 구성 공급자를 작성할 수도 있습니다.

자세한 내용은 <xref:fundamentals/configuration/index>을 참조하세요.

## <a name="logging"></a>로깅

ASP.NET Core는 다양한 로깅 공급자를 사용하는 로깅 API를 지원합니다. 기본으로 제공되는 공급자는 하나 이상의 대상에 로그를 전송할 수 있습니다. 타사의 로깅 프레임워크를 사용할 수도 있습니다.

자세한 내용은 <xref:fundamentals/logging/index>을 참조하세요.

## <a name="error-handling"></a>오류 처리

ASP.NET Core는 앱에서 오류를 처리하기 위한 개발자 예외 페이지, 사용자 지정 오류 페이지, 정적 상태 코드 페이지 및 시작 예외 처리 등의 기본 시나리오를 제공합니다.

자세한 내용은 <xref:fundamentals/error-handling>을 참조하세요.

## <a name="routing"></a>라우팅

ASP.NET Core는 응용 프로그램 요청을 경로 처리기로 라우팅하는 시나리오를 제공합니다.

자세한 내용은 <xref:fundamentals/routing>을 참조하세요.

## <a name="background-tasks"></a>백그라운드 작업

백그라운드 작업은 *호스티드 서비스*로 구현됩니다. 호스티드 서비스는 <xref:Microsoft.Extensions.Hosting.IHostedService> 인터페이스를 구현하는 백그라운드 작업 논리가 있는 클래스입니다.

자세한 내용은 <xref:fundamentals/host/hosted-services>을 참조하세요.

## <a name="access-httpcontext"></a>HttpContext에 액세스

`HttpContext`는 Razor Pages 및 MVC를 사용하여 요청을 처리할 때 자동으로 제공됩니다. `HttpContext`를 즉시 사용할 수 없는 경우에는 <xref:Microsoft.AspNetCore.Http.IHttpContextAccessor> 인터페이스 및 기본 구현 <xref:Microsoft.AspNetCore.Http.HttpContextAccessor>를 통해 `HttpContext`에 액세스할 수 있습니다.

자세한 내용은 <xref:fundamentals/httpcontext>을 참조하세요.
