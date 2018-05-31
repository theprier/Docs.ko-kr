---
title: ASP.NET Core에서 Kestrel 웹 서버 구현
author: rick-anderson
description: ASP.NET Core의 플랫폼 간 웹 서버인 Kestrel에 대해 알아봅니다.
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 05/02/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/kestrel
ms.openlocfilehash: 1c5d229614e6d6ca6889d19a5f3dc145da01bc04
ms.sourcegitcommit: 466300d32f8c33e64ee1b419a2cbffe702863cdf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/27/2018
ms.locfileid: "34555328"
---
# <a name="kestrel-web-server-implementation-in-aspnet-core"></a>ASP.NET Core에서 Kestrel 웹 서버 구현

작성자: [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher) 및 [Stephen Halter](https://twitter.com/halter73)

Kestrel은 [ASP.NET Core의 플랫폼 간 웹 서버](xref:fundamentals/servers/index)입니다. Kestrel은 기본적으로 ASP.NET Core 프로젝트 템플릿에 포함된 웹 서버입니다.

Kestrel은 다음과 같은 기능을 지원합니다.

* HTTPS
* [Websocket](https://github.com/aspnet/websockets)을 활성화하는 데 사용되는 불투명 업그레이드
* Nginx 뒤의 고성능을 위한 Unix 소켓

Kestrel은 .NET Core에서 지원하는 모든 플랫폼 및 버전에서 지원됩니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="when-to-use-kestrel-with-a-reverse-proxy"></a>Kestrel을 역방향 프록시와 함께 사용하는 경우

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

Kestrel을 단독으로 사용하거나 IIS, Nginx 또는 Apache 같은 *역방향 프록시 서버*와 함께 사용할 수 있습니다. 역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.

![Kestrel은 역방향 프록시 서버 없이 직접 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet2.png)

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

&mdash;역방향 프록시 서버의 유무에 상관없이&mdash; ASP.NET Core 2.0 이상 앱에 대해 지원되는 유효한 호스팅 구성입니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

앱이 내부 네트워크에서만 요청을 수락하는 경우 Kestrel을 앱 서버로 직접 사용할 수 있습니다.

![Kestrel은 내부 네트워크와 직접 통신합니다.](kestrel/_static/kestrel-to-internal.png)

앱을 인터넷에 노출할 경우 IIS, Nginx 또는 Apache를 *역방향 프록시 서버*로 사용합니다. 역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

역방향 프록시는 보안 이유로 인터넷에서 트래픽에 노출되는 에지 배포에 필요합니다. Kestrel의 1.x 버전은 적절한 시간 제한, 크기 제한 및 동시 연결 제한 등의 공격에 대한 완벽한 방어 능력은 없습니다.

---

역방향 프록시 시나리오는 동일한 IP 및 단일 서버에서 실행되는 포트를 공유하는 여러 앱이 있는 경우에 존재합니다. Kestrel은 여러 프로세스 간에 동일한 IP 및 포트 공유를 지원하지 않으므로 이 시나리오를 지원하지 않습니다. Kestrel이 포트에서 수신 대기하도록 구성된 경우 Kestrel은 요청의 호스트 헤더에 관계 없이 해당 포트에 대한 모든 트래픽을 처리합니다. 포트를 공유할 수 있는 역방향 프록시는 고유 IP 및 포트에서 Kestrel에 요청을 전달할 수 있습니다.

역방향 프록시 서버가 필요하지 않은 경우에도 역방향 프록시 서버를 사용하는 것은 적합한 선택일 수 있습니다.

* 호스트하는 앱의 공개된 공용 노출 영역을 제한할 수 있습니다.
* 구성 및 방어의 추가 계층을 제공합니다.
* 기존 인프라와 잘 통합될 수 있습니다.
* 부하 분산 및 SSL 구성을 간소화합니다. 역방향 프록시 서버에 SSL 인증서가 필요한 경우에만 해당 서버는 일반 HTTP를 사용하여 내부 네트워크에서 앱 서버와 통신할 수 있습니다.

> [!WARNING]
> 호스트 필터링을 사용하도록 설정된 역방향 프록시를 사용하지 않는 경우 [호스트 필터링](#host-filtering)을 사용하도록 설정해야 합니다.

## <a name="how-to-use-kestrel-in-aspnet-core-apps"></a>ASP.NET Core 앱에서 Kestrel을 사용하는 방법

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) 패키지는 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)에 포함되어 있습니다.

ASP.NET Core 프로젝트 템플릿은 기본적으로 Kestrel을 사용합니다. *Program.cs*에서 템플릿 코드는 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) 숨은 기능을 호출하는 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)를 호출합니다.

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_DefaultBuilder&highlight=7)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet 패키지를 설치합니다.

다음 섹션과 같이 필요한 [Kestrel 옵션](/dotnet/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions?view=aspnetcore-1.1)을 지정하여 `Main` 메서드에서 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder?view=aspnetcore-1.1)의 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) 확장 메서드를 호출합니다.

[!code-csharp[](kestrel/samples/1.x/Program.cs?name=snippet_Main&highlight=13-19)]

---

### <a name="kestrel-options"></a>Kestrel 옵션

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

Kestrel 웹 서버에는 인터넷 연결 배포에 특히 유용한 제약 조건 구성 옵션이 있습니다. 사용자 지정될 수 있는 몇 가지 중요 한 제한입니다.

* 최대 클라이언트 연결
* 최대 요청 본문 크기
* 최소 요청 본문 데이터 속도

[KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions) 클래스의 [한도](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.limits) 속성에서 이러한 제약 조건 및 기타 제약 조건을 설정합니다. `Limits` 속성은 [KestrelServerLimits](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits) 클래스의 인스턴스를 보유합니다.

**최대 클라이언트 연결**

[MaxConcurrentConnections](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxconcurrentconnections)  
[MaxConcurrentUpgradedConnections](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxconcurrentupgradedconnections)

다음 코드를 사용하여 전체 앱에 대한 동시 개방 TCP 연결의 최대 수를 설정할 수 있습니다.

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_Limits&highlight=3)]

HTTP 또는 HTTPS에서 다른 프로토콜(예: WebSocket 요청에서)로 업그레이드된 연결에 대한 별도 제한이 있습니다. 연결이 업그레이드된 후 `MaxConcurrentConnections` 제한에 대해 계산되지 않습니다.

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_Limits&highlight=4)]

연결의 최대 수는 기본적으로 무제한(null)입니다.

**최대 요청 본문 크기**

[MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize)

기본 최대 요청 본문 크기는 약 28.6MB인 30,000,000바이트입니다.

ASP.NET Core MVC 앱에서 한도를 재정의할 때는 작업 메서드에서 [RequestSizeLimit](/dotnet/api/microsoft.aspnetcore.mvc.requestsizelimitattribute) 특성을 사용하는 방법이 좋습니다.

```csharp
[RequestSizeLimit(100000000)]
public IActionResult MyActionMethod()
```

다음 예제는 모든 요청에서 앱에 대한 제약 조건을 구성하는 방법을 보여 줍니다.

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_Limits&highlight=5)]

미들웨어에서 특정 요청에 대한 설정을 재정의할 수 있습니다.

[!code-csharp[](kestrel/samples/2.x/Startup.cs?name=snippet_Limits&highlight=3-4)]

앱에서 요청을 읽기 시작한 후 요청에 대한 제한을 구성하려고 하면 예외가 throw됩니다. `MaxRequestBodySize` 속성이 제한을 구성하기에 너무 늦은, 읽기 전용 상태인지를 알려주는 `IsReadOnly` 속성이 있습니다.

**최소 요청 본문 데이터 속도**

[MinRequestBodyDataRate](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.minrequestbodydatarate)  
[MinResponseDataRate](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.minresponsedatarate)

Kestrel은 데이터가 지정된 속도(바이트/초)로 도착하는지 1초마다 확인합니다. 속도가 최소 아래로 떨어지면 연결이 시간 초과됩니다. 유예 기간은 Kestrel에서 해당 전송 속도를 최소로 높이기 위해 클라이언트에 제공하는 총 시간입니다. 이 시간 동안 속도는 확인되지 않습니다. 유예 기간은 TCP 느린 시작으로 인해 느린 속도로 처음에 데이터를 보내는 연결 중단을 방지하는 데 도움이 됩니다.

기본 최소 속도는 5초의 유예 기간으로 240바이트/초입니다.

최소 속도는 응답에도 적용됩니다. 요청 제한 및 응답 제한을 설정하는 코드는 속성 및 인터페이스 이름에 `RequestBody` 또는 `Response`를 갖는 것을 제외하고 동일합니다.

*Program.cs*에서 최소 데이터 속도를 구성하는 방법을 보여 주는 예제는 다음과 같습니다.

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_Limits&highlight=6-7)]

미들웨어에서 요청별 속도를 구성할 수 있습니다.

[!code-csharp[](kestrel/samples/2.x/Startup.cs?name=snippet_Limits&highlight=5-8)]

다른 Kestrel 옵션 및 제한에 대한 내용은 다음을 참조하세요.

* [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions)
* [KestrelServerLimits](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits)
* [ListenOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.listenoptions)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

Kestrel 옵션 및 제한에 대한 내용은 다음을 참조하세요.

* [KestrelServerOptions class](/dotnet/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions?view=aspnetcore-1.1)
* [KestrelServerLimits](/dotnet/api/microsoft.aspnetcore.server.kestrel.kestrelserverlimits?view=aspnetcore-1.1)

---

### <a name="endpoint-configuration"></a>엔드포인트 구성

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

::: moniker range="= aspnetcore-2.0"
기본적으로 ASP.NET Core는 `http://localhost:5000`으로 바인딩합니다. Kestrel에 대한 URL 접두사 및 포트를 구성하려면 [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions)에 대한 [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) 메서드 또는 [수신 대기](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen)를 호출합니다. `UseUrls`, `--urls` 명령줄 인수 `urls` 호스트 구성 키 및 `ASPNETCORE_URLS` 환경 변수도 작동하지만 이 섹션의 뒷부분에 명시된 제한 사항이 있습니다.

`urls` 호스트 구성 키는 앱 구성이 아닌 호스트 구성에서 와야 합니다. `urls` 키와 값을 *appsettings.json*에 추가하는 것은 구성 파일에서 구성을 읽을 때면 호스트가 완전히 초기화되기 때문에 호스트 구성에 영향을 주지 않습니다. 그러나 호스트를 구성하려면 호스트 작성기에서 [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration)을 통해 *appsettings.json*에서 `urls` 키를 사용할 수 있습니다.

```csharp
var config = new ConfigurationBuilder()
    .SetBasePath(Directory.GetCurrentDirectory())
    .AddJsonFile("appSettings.json", optional: true, reloadOnChange: true)
    .Build();

var host = new WebHostBuilder()
    .UseKestrel()
    .UseConfiguration(config)
    .UseContentRoot(Directory.GetCurrentDirectory())
    .UseStartup<Startup>()
    .Build();
```

::: moniker-end
::: moniker range=">= aspnetcore-2.1"

기본적으로 ASP.NET Core는 다음으로 바인딩합니다.

* `http://localhost:5000`
* `https://localhost:5001` (로컬 개발 인증서가 제공되는 경우)

개발 인증서를 만듭니다.

* [.NET Core SDK](/dotnet/core/sdk)가 설치되는 경우.
* [dev-certs 도구](https://github.com/aspnet/DotNetTools/tree/dev/src/dotnet-dev-certs)가 인증서를 만드는 데 사용됩니다.

일부 브라우저에서 로컬 개발 인증서를 신뢰하도록 브라우저에 명시적 사용 권한을 부여할 것을 요구합니다.

ASP.NET Core 2.1 이상 프로젝트 템플릿은 기본적으로 HTTPS에서 실행할 앱을 구성하고 [HTTPS 리디렉션 및 HSTS 지원](xref:security/enforcing-ssl)을 포함합니다.

Kestrel에 대한 URL 접두사 및 포트를 구성하려면 [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions)에 대한 [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) 메서드 또는 [수신 대기](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen)를 호출합니다.

`UseUrls`, `--urls` 명령줄 인수 `urls` 호스트 구성 키 및 `ASPNETCORE_URLS` 환경 변수도 작동하지만 이 섹션의 뒷부분에 명시된 제한 사항이 있습니다(HTTPS 엔드포인트 구성에 대해 기본 인증서를 사용할 수 있어야 합니다).

ASP.NET Core 2.1 `KestrelServerOptions` 구성:

**ConfigureEndpointDefaults(Action&lt;ListenOptions&gt;)**  
지정된 각 엔드포인트에 대해 실행할 구성 `Action`을 지정합니다. `ConfigureEndpointDefaults`의 여러 차례 호출은 `Action`에 앞서 마지막으로 지정된 `Action`으로 바꿉니다.

**ConfigureHttpsDefaults(Action&lt;HttpsConnectionAdapterOptions&gt;)**  
각 HTTPS 엔드포인트에 대해 실행할 구성 `Action`을 지정합니다. `ConfigureHttpsDefaults`의 여러 차례 호출은 `Action`에 앞서 마지막으로 지정된 `Action`으로 바꿉니다.

**Configure(IConfiguration)**  
입력으로 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)을 받아들이는 Kestrel를 설정하기 위한 구성 로더를 만듭니다. 구성은 Kestrel용 구성 섹션에 대해 범위를 지정해야 합니다.

**ListenOptions.UseHttps**  
HTTPS를 사용하려면 Kestrel을 구성합니다.

`ListenOptions.UseHttps` 확장:

* `UseHttps` &ndash; 기본 인증서를 통해 HTTPS를 사용하려면 Kestrel 구성합니다. 기본 인증서가 구성되지 않은 경우 예외를 throw합니다.
* `UseHttps(string fileName)`
* `UseHttps(string fileName, string password)`
* `UseHttps(string fileName, string password, Action<HttpsConnectionAdapterOptions> configureOptions)`
* `UseHttps(StoreName storeName, string subject)`
* `UseHttps(StoreName storeName, string subject, bool allowInvalid)`
* `UseHttps(StoreName storeName, string subject, bool allowInvalid, StoreLocation location)`
* `UseHttps(StoreName storeName, string subject, bool allowInvalid, StoreLocation location, Action<HttpsConnectionAdapterOptions> configureOptions)`
* `UseHttps(X509Certificate2 serverCertificate)`
* `UseHttps(X509Certificate2 serverCertificate, Action<HttpsConnectionAdapterOptions> configureOptions)`
* `UseHttps(Action<HttpsConnectionAdapterOptions> configureOptions)`

`ListenOptions.UseHttps` 매개 변수:

* `filename`은 앱의 콘텐츠 파일을 포함하는 디렉터리와 관련된 인증서 파일의 경로 및 파일 이름입니다.
* `password`은 X.509 인증서 데이터에 액세스하는 데 필요한 암호입니다.
* `configureOptions`은 `HttpsConnectionAdapterOptions`를 구성하는 `Action`입니다. `ListenOptions`를 반환합니다.
* `storeName`은 인증서를 로드할 수 있는 인증서 저장소입니다.
* `subject`은 인증서의 주체 이름입니다.
* `allowInvalid`은 자체 서명된 인증서와 같이 잘못된 인증서를 고려해야 할 경우를 나타냅니다.
* `location`은 인증서를 로드할 수 있는 저장소 위치입니다.
* `serverCertificate`은 X.509 인증서입니다.

프로덕션 내에 HTTPS가 명시적으로 구성되어야 합니다. 최소한 기본 인증서를 제공해야 합니다.

다음에 설명된 지원되는 구성입니다.

* 구성 없음
* 구성에서 기본 인증서를 바꿈
* 코드에서 기본값 변경

*구성 없음*

Kestrel은 `http://localhost:5000` 및 `https://localhost:5001`에서 수신 대기합니다(기본 인증서가 사용 가능한 경우).

다음을 사용하여 URL을 지정합니다.

* `ASPNETCORE_URLS` 환경 변수.
* `--urls` 명령줄 인수.
* `urls` 호스트 구성 키.
* `UseUrls` 확장명 메서드.

자세한 내용은 [서버 URL](xref:fundamentals/host/web-host#server-urls) 및 [구성 재정의](xref:fundamentals/host/web-host#override-configuration)를 참조합니다.

이러한 접근 방식을 사용하여 제공된 값은 하나 이상의 HTTP 및 HTTPS 엔드포인트(기본 인증서가 사용 가능한 경우의 HTTPS)일 수 있습니다. 값을 세미콜론으로 구분된 목록으로 구성합니다(예를 들어, `"Urls": "http://localhost:8000;http://localhost:8001"`).

*구성에서 기본 인증서를 바꿈*

[WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)는 Kestrel 구성을 로드하려면 기본적으로 `serverOptions.Configure(context.Configuration.GetSection("Kestrel"))`을 호출합니다. 기본 HTTPS 앱 설정 구성 스키마는 Kestrel에 대해 사용 가능합니다. 디스크 상의 파일에서 또는 인증서 저장소에서 사용할 인증서 및 URL을 포함하여 여러 엔드포인트를 구성합니다.

다음 *appsettings.json* 예제에서:

* 잘못된 인증서 사용을 허가하려면 **AllowInvalid**를 `true`으로 설정합니다(예를 들어, 자체 서명된 인증서).
* 인증서를 지정하지 않는 모든 HTTPS 엔드포인트(다음 예제에서 **HttpsDefaultCert**)는 **인증서** > **기본**에서 정의된 인증서 또는 개발 인증서로 대체합니다.

```json
{
"Kestrel": {
  "EndPoints": {
    "Http": {
      "Url": "http://localhost:5000"
    },

    "HttpsInlineCertFile": {
      "Url": "https://localhost:5001",
      "Certificate": {
        "Path": "<path to .pfx file>",
        "Password": "<certificate password>"
      }
    },

    "HttpsInlineCertStore": {
      "Url": "https://localhost:5002",
      "Certificate": {
        "Subject": "<subject; required>",
        "Store": "<certificate store; defaults to My>",
        "Location": "<location; defaults to CurrentUser>",
        "AllowInvalid": "<true or false; defaults to false>"
      }
    },

    "HttpsDefaultCert": {
      "Url": "https://localhost:5003"
    },

    "Https": {
      "Url": "https://*:5004",
      "Certificate": {
      "Path": "<path to .pfx file>",
      "Password": "<certificate password>"
      }
    }
    },
    "Certificates": {
      "Default": {
        "Path": "<path to .pfx file>",
        "Password": "<certificate password>"
      }
    }
  }
}
```

모든 인증서 노드에 대해 **경로** 및 **암호**를 사용하는 대신 인증서 저장소 필드를 지정합니다. 예를 들어, **인증서** > **기본** 인증서는 다음과 같이 지정될 수 있습니다.

```json
"Default": {
  "Subject": "<subject; required>",
  "Store": "<cert store; defaults to My>",
  "Location": "<location; defaults to CurrentUser>",
  "AllowInvalid": "<true or false; defaults to false>"
}
```

스키마 참고 사항:

* 엔드포인트 이름은 대/소문자를 구분하지 않습니다. 예를 들어, `HTTPS` 및 `Https`는 유효합니다.
* `Url` 매개 변수는 각 엔드포인트에 대해 필요합니다. 이 매개 변수에 대한 형식은 단일 값으로 제한된 경우를 제외하고 최상위 `Urls` 구성 매개 변수와 동일합니다.
* 이러한 엔드포인트는 추가하기보다는 최상위 `Urls` 구성에서 정의된 엔드포인트를 바꿉니다. `Listen`을 통해 코드에서 정의된 엔드포인트는 구성 섹션에서 정의된 엔드포인트로 누적됩니다.
* `Certificate` 섹션은 선택 사항입니다. `Certificate` 섹션이 지정되지 않은 경우 이전 시나리오에서 정의된 기본값이 사용됩니다. 기본값이 사용 가능하지 않은 경우 서버는 예외를 throw하고 시작되지 않습니다.
* `Certificate` 섹션은 **경로**&ndash;**암호** 및 **주체**&ndash;**저장소** 인증서 모두를 지원합니다.
* 많은 엔드포인트가 포트 충돌을 일으키지 않는 한 이런 방식으로 정의될 수 있습니다.
* `serverOptions.Configure(context.Configuration.GetSection("Kestrel"))`은 구성된 엔드포인트의 설정을 보완하는 데 사용될 수 있는 `.Endpoint(string name, options => { })` 메서드를 통해 `KestrelConfigurationLoader`를 반환합니다.

  ```csharp
  serverOptions.Configure(context.Configuration.GetSection("Kestrel"))
      .Endpoint("HTTPS", opt =>
      {
          opt.HttpsOptions.SslProtocols = SslProtocols.Tls12;
      });
  ```

  또한 `KestrelServerOptions.ConfigurationLoader`에 직접 액세스하여 `WebHost.CreatedDeafaultBuilder`에서 제공한 로더와 같이 기존 로더에서 반복을 유지할 수 있습니다.

* 각 엔드포인트에 대한 구성 섹션은 `Endpoint` 메서드의 옵션에서 사용 가능하므로 사용자 지정 설정을 읽을 수 있습니다.
* 여러 구성은 다른 섹션을 통해 다시 `serverOptions.Configure(context.Configuration.GetSection("Kestrel"))`을 호출하여 로드할 수 있습니다. `Load`은 이전 인스턴스에서 명시적으로 호출되지 않는 한 마지막 구성만 사용됩니다. 메타패키지는 `Load`을 호출하지 않으므로 기본 구성 섹션을 바꿀 수 있습니다.
* `KestrelConfigurationLoader`은 `KestrelServerOptions`에서 `Endpoint` 오버로드로 `Listen` API 제품군을 미러링하므로 코드 및 구성 엔드포인트를 동일 장소에서 구성할 수 있습니다. 이러한 오버로드는 이름을 사용하지 않고 구성에서 기본 설정만 사용합니다.

*코드에서 기본값 변경*

`ConfigureEndpointDefaults` 및 `ConfigureHttpsDefaults`는 이전 시나리오에서 지정된 기본 인증서 재정의를 포함한 `ListenOptions` 및 `HttpsConnectionAdapterOptions`에 대해 기본 설정을 변경하는 데 사용될 수 있습니다. `ConfigureEndpointDefaults` 및 `ConfigureHttpsDefaults`는 모든 엔드포인트가 구성되기 전에 호출해야 합니다.

```csharp
options.ConfigureEndpointDefaults(opt =>
{
    opt.NoDelay = true;
});

options.ConfigureHttpsDefaults(httpsOptions =>
{
    httpsOptions.SslProtocols = SslProtocols.Tls12;
});
```

*SNI에 대한 Kestrel 지원*

[서버 이름 표시(SNI)](https://tools.ietf.org/html/rfc6066#section-3)는 동일한 IP 주소 및 포트에서 여러 도메인을 호스트하는 데 사용될 수 있습니다. 함수에 대한 SNI의 경우 클라이언트는 TLS 핸드셰이크 동안 보안 세션에 대한 호스트 이름을 서버로 보내므로 서버에서 올바른 인증서를 제공할 수 있습니다. TLS 핸드셰이크 다음에 오는 보안 세션 동안 클라이언트는 서버와 암호화된 통신을 위해 제공된 인증서를 사용합니다.

Kestrel은 `ServerCertificateSelector` 콜백을 통해 SNI를 지원합니다. 앱이 호스트 이름을 검사하고 적절한 인증서를 선택하도록 허용하려면 연결당 한 번씩 콜백이 호출됩니다.

SNI 지원은 대상 프레임워크 `netcoreapp2.1`에서 실행할 것을 요구합니다. `netcoreapp2.0` 및 `net461`에서 콜백이 호출되지만 `name` 은 항상 `null`입니다. 클라이언트가 TLS 핸드셰이크에서 호스트 이름 매개 변수를 제공하지 않는 경우 `name`은 또한 `null`입니다.

```csharp
WebHost.CreateDefaultBuilder()
    .UseKestrel((context, options) =>
    {
        options.ListenAnyIP(5005, listenOptions =>
        {
            listenOptions.UseHttps(httpsOptions =>
            {
                var localhostCert = CertificateLoader.LoadFromStoreCert(
                    "localhost", "My", StoreLocation.CurrentUser, 
                    allowInvalid: true);
                var exampleCert = CertificateLoader.LoadFromStoreCert(
                    "example.com", "My", StoreLocation.CurrentUser, 
                    allowInvalid: true);
                var subExampleCert = CertificateLoader.LoadFromStoreCert(
                    "sub.example.com", "My", StoreLocation.CurrentUser, 
                    allowInvalid: true);
                var certs = new Dictionary(StringComparer.OrdinalIgnoreCase);
                certs["localhost"] = localhostCert;
                certs["example.com"] = exampleCert;
                certs["sub.example.com"] = subExampleCert;

                httpsOptions.ServerCertificateSelector = (connectionContext, name) =>
                {
                    if (name != null && certs.TryGetValue(name, out var cert))
                    {
                        return cert;
                    }

                    return exampleCert;
                };
            });
        });
    });
```

::: moniker-end

**TCP 소켓에 바인딩**

[수신 대기](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen) 메서드는 TCP 소켓에 바인딩하고 옵션 람다는 SSL 인증서 구성을 허용합니다.

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_TCPSocket&highlight=9-16)]

예제에서는 [ListenOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.listenoptions)를 사용하여 끝점에 대한 SSL을 구성합니다. 동일한 API를 사용하여 특정 엔드포인트에 대한 다른 Kestrel 설정을 구성합니다.

[!INCLUDE [How to make an X.509 cert](~/includes/make-x509-cert.md)]

**Unix 소켓에 바인딩**

이 예제에 나와 있는 것처럼 Nginx를 사용하여 향상된 성능을 위해 [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket)을 통해 Unix 소켓을 수신 대기합니다.

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_UnixSocket)]

**포트 0**

포트 번호 `0`가 지정되는 경우 Kestrel은 동적으로 사용 가능한 포트에 바인딩합니다. 다음 예제에서는 Kestrel이 실제로 런타임에 바인딩한 포트를 확인하는 방법을 보여 줍니다.

[!code-csharp[](kestrel/samples/2.x/Startup.cs?name=snippet_Port0&highlight=3)]

앱이 실행되는 경우 콘솔 창 출력은 앱이 연결될 수 있는 동적 포트를 나타냅니다.

```console
Now listening on: http://127.0.0.1:48508
```

**UseUrls, --urls 명령 줄 인수, urls 호스트 구성 키 및 ASPNETCORE_URLS 환경 변수 제한 사항**

다음 방법으로 엔트포인트를 구성합니다.

* [UseUrls](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useurls)
* `--urls` 명령줄 인수
* `urls` 호스트 구성 키
* `ASPNETCORE_URLS`환경 변수

이러한 메서드는 코드를 Kestrel이 아닌 서버와 작동하도록 하려는 경우 유용합니다. 그러나 이러한 제한 사항을 고려해야 합니다.

* HTTPS 끝점 구성에서 기본 인증서를 제공하지 않는 한 이러한 방법으로는 SSL을 사용할 수 없습니다(예: 이 항목의 앞부분에 표시된 것처럼 `KestrelServerOptions` 구성 또는 구성 파일 사용).
* `Listen` 및 `UseUrls` 방식 모두를 동시에 사용할 경우 `Listen` 엔드포인트는 `UseUrls` 엔드포인트를 재정의합니다.

**IIS 엔드포인트 구성**

IIS를 사용하는 경우 IIS 재정의 바인딩에 대한 URL 바인딩은 `Listen` 또는 `UseUrls`에 의해 설정됩니다. 자세한 내용은 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module) 항목을 참조하세요.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

기본적으로 ASP.NET Core는 `http://localhost:5000`으로 바인딩합니다. Kestrel 사용에 대한 URL 접두사 및 포트를 구성합니다.

* [UseUrls](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useurls?view=aspnetcore-1.1) 확장 메서드
* `--urls` 명령줄 인수
* `urls` 호스트 구성 키
* `ASPNETCORE_URLS` 환경 변수를 포함한 ASP.NET Core 구성 시스템

이러한 메서드에 대한 자세한 내용은 [호스팅](xref:fundamentals/host/index)을 참조하세요.

**IIS 엔드포인트 구성**

IIS를 사용하는 경우 IIS 재정의 바인딩에 대한 URL 바인딩은 `UseUrls`에 의해 설정됩니다. 자세한 내용은 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module) 항목을 참조하세요.

---

::: moniker range=">= aspnetcore-2.1"

## <a name="transport-configuration"></a>전송 구성

ASP.NET Core 2.1 릴리스에서 Kestrel의 기본 전송은 더 이상 Libuv에 기반하지 않으며 대신 관리 소켓에 기반합니다. [WebHostBuilderLibuvExtensions.UseLibuv](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderlibuvextensions.uselibuv)를 호출하고 다음 패키지 중 하나를 사용하는 2.1로 업그레이드된 ASP.NET Core 2.0 앱의 주요 변경 내용입니다.

* [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/)(직접 패키지 참조)
* [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/)

ASP.NET Core 2.1 이상의 경우 `Microsoft.AspNetCore.App` 메타패키지를 사용하는 프로젝트는 Libuv를 사용해야 합니다.

* [Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv/) 패키지에 대한 종속성을 앱의 프로젝트 파일에 추가합니다.

    ```xml
    <PackageReference Include="Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv" 
                    Version="2.1.0" />
    ```

* [WebHostBuilderLibuvExtensions.UseLibuv](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderlibuvextensions.uselibuv)를 호출합니다.

    ```csharp
    public class Program
    {
        public static void Main(string[] args)
        {
            CreateWebHostBuilder(args).Build().Run();
        }

        public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .UseLibuv()
                .UseStartup<Startup>();
    }
    ```

::: moniker-end

### <a name="url-prefixes"></a>URL 접두사

`UseUrls`, `--urls` 명령줄 인수, `urls` 호스트 구성 키 또는 `ASPNETCORE_URLS` 환경 변수를 사용하는 경우 URL 접두사는 다음 형식 중 하나일 수 있습니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

HTTP URL 접두사만 유효합니다. Kestrel은 `UseUrls`을 사용하여 URL 바인딩을 구성하는 경우 SSL을 지원하지 않습니다.

* 포트 번호가 있는 IPv4 주소

  ```
  http://65.55.39.10:80/
  ```

  `0.0.0.0`은 모든 IPv4 주소에 바인딩하는 특별한 경우입니다.

* 포트 번호가 있는 IPv6 주소

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/
  ```

  `[::]`는 IPv4 `0.0.0.0`에 해당하는 IPv6입니다.

* 포트 번호가 있는 호스트 이름

  ```
  http://contoso.com:80/
  http://*:80/
  ```

  호스트 이름, `*` 및 `+`는 특별하지 않습니다. 유효한 IP 주소 또는 `localhost`로 인식하지 않는 모든 항목은 모든 IPv4 및 IPv6 IP에 바인딩합니다. 서로 다른 호스트 이름을 같은 포트에서 서로 다른 ASP.NET Core 앱에 바인딩하려면 IIS, Nginx 또는 Apache와 같은 역방향 프록시 서버 또는 [HTTP.sys](xref:fundamentals/servers/httpsys)를 사용합니다.

  > [!WARNING]
  > 호스트 필터링을 사용하도록 설정된 역방향 프록시를 사용하지 않는 경우 [호스트 필터링](#host-filtering)을 사용하도록 설정합니다.

* 포트 번호가 있는 호스트 `localhost` 이름 또는 포트 번호가 있는 루프백 IP

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  `localhost`가 지정되면 Kestrel은 IPv4 및 IPv6 루프백 인터페이스 모두에 바인딩하려고 합니다. 요청된 포트가 루프백 인터페이스 중 하나의 다른 서비스에서 사용 중인 경우 Kestrel은 시작에 실패합니다. 루프백 인터페이스 중 하나를 다른 이유(일반적으로 IPv6이 지원되지 않으므로)로 사용할 수 없는 경우 Kestrel은 경고를 기록합니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

* 포트 번호가 있는 IPv4 주소

  ```
  http://65.55.39.10:80/
  https://65.55.39.10:443/
  ```

  `0.0.0.0`은 모든 IPv4 주소에 바인딩하는 특별한 경우입니다.

* 포트 번호가 있는 IPv6 주소

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/
  https://[0:0:0:0:0:ffff:4137:270a]:443/
  ```

  `[::]`는 IPv4 `0.0.0.0`에 해당하는 IPv6입니다.

* 포트 번호가 있는 호스트 이름

  ```
  http://contoso.com:80/
  http://*:80/
  https://contoso.com:443/
  https://*:443/
  ```

  호스트 이름, `*` 및 `+`는 특별하지 않습니다. 인식된 IP 주소 또는 `localhost`가 아닌 모든 항목은 모든 IPv4 및 IPv6 IP에 바인딩합니다. 서로 다른 호스트 이름을 같은 포트에서 서로 다른 ASP.NET Core 앱에 바인딩하려면 IIS, Nginx 또는 Apache와 같은 역방향 프록시 서버 또는 [WebListener](xref:fundamentals/servers/weblistener)를 사용합니다.

* 포트 번호가 있는 호스트 `localhost` 이름 또는 포트 번호가 있는 루프백 IP

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  `localhost`가 지정되면 Kestrel은 IPv4 및 IPv6 루프백 인터페이스 모두에 바인딩하려고 합니다. 요청된 포트가 루프백 인터페이스 중 하나의 다른 서비스에서 사용 중인 경우 Kestrel은 시작에 실패합니다. 루프백 인터페이스 중 하나를 다른 이유(일반적으로 IPv6이 지원되지 않으므로)로 사용할 수 없는 경우 Kestrel은 경고를 기록합니다.

* Unix 소켓

  ```
  http://unix:/run/dan-live.sock
  ```

**포트 0**

포트 번호 `0`가 지정되는 경우 Kestrel은 동적으로 사용 가능한 포트에 바인딩합니다. 포트 `0`에 바인딩은 `localhost`를 제외하고 모든 호스트 이름 또는 IP에 대해 허용됩니다.

앱이 실행되는 경우 콘솔 창 출력은 앱이 연결될 수 있는 동적 포트를 나타냅니다.

```console
Now listening on: http://127.0.0.1:48508
```

**SSL에 대한 URL 접두사**

`UseHttps` 확장 메서드를 호출하는 경우 `https:`에 URL 접두사를 포함해야 합니다.

```csharp
var host = new WebHostBuilder()
    .UseKestrel(options =>
    {
        options.UseHttps("testCert.pfx", "testPassword");
    })
   .UseUrls("http://localhost:5000", "https://localhost:5001")
   .UseContentRoot(Directory.GetCurrentDirectory())
   .UseStartup<Startup>()
   .Build();
```

> [!NOTE]
> HTTPS 및 HTTP는 동일한 포트에서 호스팅될 수 없습니다.

[!INCLUDE [How to make an X.509 cert](~/includes/make-x509-cert.md)]

---

## <a name="host-filtering"></a>호스트 필터링

Kestrel은 `http://example.com:5000`과 같은 접두사에 따라 구성을 지원하지만 일반적으로 호스트 이름을 무시합니다. 호스트 `localhost`은 루프백 주소에 바인딩하는 데 사용된 특별한 경우입니다. 명시적 IP 주소를 제외한 모든 호스트는 모든 공용 IP 주소에 바인딩합니다. 이 정보 중 어느 것도 요청 `Host` 헤더의 유효성을 검사하는 데 사용됩니다.

두 가지 해결 방법이 있습니다.

* 호스트 헤더 필터링을 사용한 역방향 프록시 뒤의 호스트입니다. ASP.NET Core 1.x에서 Kestrel에 대한 유일한 지원 시나리오입니다.
* 미들웨어를 사용하여 `Host` 헤더로 요청을 필터링합니다. 샘플 미들웨어는 다음과 같습니다.

```csharp
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Logging;
using Microsoft.Extensions.Primitives;
using Microsoft.Net.Http.Headers;
using System;
using System.Collections.Generic;
using System.Threading.Tasks;

// A normal middleware would provide an options type, config binding, extension methods, etc..
// This intentionally does all of the work inside of the middleware so it can be
// easily copy-pasted into docs and other projects.
public class HostFilteringMiddleware
{
    private readonly RequestDelegate _next;
    private readonly IList<string> _hosts;
    private readonly ILogger<HostFilteringMiddleware> _logger;

    public HostFilteringMiddleware(RequestDelegate next, IConfiguration config, ILogger<HostFilteringMiddleware> logger)
    {
        if (config == null)
        {
            throw new ArgumentNullException(nameof(config));
        }

        _next = next ?? throw new ArgumentNullException(nameof(next));
        _logger = logger ?? throw new ArgumentNullException(nameof(logger));

        // A semicolon separated list of host names without the port numbers.
        // IPv6 addresses must use the bounding brackets and be in their normalized form.
        _hosts = config["AllowedHosts"]?.Split(new[] { ';' }, StringSplitOptions.RemoveEmptyEntries);
        if (_hosts == null || _hosts.Count == 0)
        {
            throw new InvalidOperationException("No configuration entry found for AllowedHosts.");
        }
    }

    public Task Invoke(HttpContext context)
    {
        if (!ValidateHost(context))
        {
            context.Response.StatusCode = 400;
            _logger.LogDebug("Request rejected due to incorrect Host header.");
            return Task.CompletedTask;
        }

        return _next(context);
    }

    // This does not duplicate format validations that are expected to be performed by the host.
    private bool ValidateHost(HttpContext context)
    {
        StringSegment host = context.Request.Headers[HeaderNames.Host].ToString().Trim();

        if (StringSegment.IsNullOrEmpty(host))
        {
            // Http/1.0 does not require the Host header.
            // Http/1.1 requires the header but the value may be empty.
            return true;
        }

        // Drop the port

        var colonIndex = host.LastIndexOf(':');

        // IPv6 special case
        if (host.StartsWith("[", StringComparison.Ordinal))
        {
            var endBracketIndex = host.IndexOf(']');
            if (endBracketIndex < 0)
            {
                // Invalid format
                return false;
            }
            if (colonIndex < endBracketIndex)
            {
                // No port, just the IPv6 Host
                colonIndex = -1;
            }
        }

        if (colonIndex > 0)
        {
            host = host.Subsegment(0, colonIndex);
        }

        foreach (var allowedHost in _hosts)
        {
            if (StringSegment.Equals(allowedHost, host, StringComparison.OrdinalIgnoreCase))
            {
                return true;
            }

            // Sub-domain wildcards: *.example.com
            if (allowedHost.StartsWith("*.", StringComparison.Ordinal) && host.Length >= allowedHost.Length)
            {
                // .example.com
                var allowedRoot = new StringSegment(allowedHost, 1, allowedHost.Length - 1);

                var hostRoot = host.Subsegment(host.Length - allowedRoot.Length, allowedRoot.Length);
                if (hostRoot.Equals(allowedRoot, StringComparison.OrdinalIgnoreCase))
                {
                    return true;
                }
            }
        }

        return false;
    }
}
```

`Startup.Configure`에 위의 `HostFilteringMiddleware`을 등록합니다. [미들웨어 등록 순서](xref:fundamentals/middleware/index#ordering)가 중요합니다. 등록은 진단 미들웨어 등록 후 즉시 이뤄져야 합니다(예: `app.UseExceptionHandler`).

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
        app.UseBrowserLink();
    }
    else
    {
        app.UseExceptionHandler("/Home/Error");
    }

    app.UseMiddleware<HostFilteringMiddleware>();

    app.UseMvcWithDefaultRoute();
}
```

위의 미들웨어는 *appsettings.\< EnvironmentName>.json*에서 `AllowedHosts` 키를 예상합니다. 이 키의 값은 세미콜론으로 구분된 포트 번호 없는 호스트 이름 목록입니다. *appsettings.Production.json*에 `AllowedHosts` 키-값 쌍을 포함합니다.

```json
{
  "AllowedHosts": "example.com"
}
```

*appsettings.Development.json* (로컬 호스트 구성 파일):

```json
{
  "AllowedHosts": "localhost"
}
```

## <a name="additional-resources"></a>추가 자료

* [HTTPS 적용](xref:security/enforcing-ssl)
* [Kestrel 소스 코드](https://github.com/aspnet/KestrelHttpServer)
