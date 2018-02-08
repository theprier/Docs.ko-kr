---
title: "ASP.NET Core에서 Kestrel 웹 서버 구현"
author: tdykstra
description: "libuv 기반 ASP.NET Core에 대한 플랫폼 간 웹 서버인 Kestrel을 소개합니다."
manager: wpickett
ms.author: tdykstra
ms.custom: H1Hack27Feb2017
ms.date: 08/02/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/kestrel
ms.openlocfilehash: bfe7644891296c7c3485c9a870d90951ba87e9e8
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-kestrel-web-server-implementation-in-aspnet-core"></a>ASP.NET Core에서 Kestrel 웹 서버 구현에 대한 소개

작성자: [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher) 및 [Stephen Halter](https://twitter.com/halter73)

Kestrel은 플랫폼 간 비동기 I/O 라이브러리인 [libuv](https://github.com/libuv/libuv)를 기반으로 하는 [ASP.NET Core용 플랫폼 간 웹 서버](index.md)입니다. Kestrel은 기본적으로 ASP.NET Core 프로젝트 템플릿에 포함된 웹 서버입니다. 

Kestrel은 다음과 같은 기능을 지원합니다.

  * HTTPS
  * [Websocket](https://github.com/aspnet/websockets)을 활성화하는 데 사용되는 불투명 업그레이드
  * Nginx 뒤의 고성능을 위한 Unix 소켓 

Kestrel은 .NET Core에서 지원하는 모든 플랫폼 및 버전에서 지원됩니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[2.x용 샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample2)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[1.x용 샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample1)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

---

## <a name="when-to-use-kestrel-with-a-reverse-proxy"></a>Kestrel을 역방향 프록시와 함께 사용하는 경우

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

Kestrel을 단독으로 사용하거나 IIS, Nginx 또는 Apache 같은 *역방향 프록시 서버*와 함께 사용할 수 있습니다. 역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.

![Kestrel은 역방향 프록시 서버 없이 직접 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet2.png)

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

Kestrel이 내부 네트워크에만 노출되는 경우 역방향 프록시 서버를 사용하거나 사용하지 않는 구성을 사용할 수도 있습니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

응용 프로그램이 내부 네트워크의 요청만 허용할 경우 Kestrel을 단독으로 사용할 수 있습니다.

![Kestrel은 내부 네트워크와 직접 통신합니다.](kestrel/_static/kestrel-to-internal.png)

응용 프로그램을 인터넷에 노출할 경우 IIS, Nginx 또는 Apache를 *역방향 프록시 서버*로 사용해야 합니다. 역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

역방향 프록시는 보안 이유로 인터넷에서 트래픽에 노출되는 에지 배포에 필요합니다. Kestrel 1.x 버전에는 공격에 대한 전체 방어 기능이 포함되어 있지 않습니다. 이 방어 기능에는 적절한 시간 제한, 크기 제한, 동시 연결 제한이 포함되지만 이것으로 제한되지 않습니다.

---

역방향 프록시를 필요로 하는 시나리오는 동일한 IP 및 단일 서버에서 실행되는 포트를 공유하는 여러 응용 프로그램이 있는 경우입니다. Kestrel은 여러 프로세스 간에 동일한 IP 및 포트 공유를 지원하지 않으므로 Kestrel과 직접 작동하지 않습니다. 포트에서 수신 대기하도록 Kestrel을 구성할 때 호스트 헤더에 관계 없이 해당 포트에 대한 모든 트래픽을 처리합니다. 포트를 공유할 수 있는 역방향 프록시는 고유 IP 및 포트에서 Kestrel에 전달해야 합니다.

역방향 프록시 서버가 필요하지 않은 경우에도 하나를 사용하는 것은 다른 이유로 적합한 선택일 수 있습니다.

* 공개된 노출 영역을 제한할 수 있습니다.
* 구성 및 방어의 선택적 추가 계층을 제공합니다.
* 기존 인프라와 잘 통합될 수 있습니다.
* 부하 분산 및 SSL 설정을 간소화합니다. 역방향 프록시 서버에 SSL 인증서가 필요한 경우에만 해당 서버는 일반 HTTP를 사용하여 내부 네트워크의 응용 프로그램 서버와 통신할 수 있습니다.

## <a name="how-to-use-kestrel-in-aspnet-core-apps"></a>ASP.NET Core 앱에서 Kestrel을 사용하는 방법

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) 패키지는 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)에 포함되어 있습니다.

ASP.NET Core 프로젝트 템플릿은 기본적으로 Kestrel을 사용합니다. *Program.cs*에서 템플릿 코드는 [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 숨은 기능을 호출하는 `CreateDefaultBuilder`를 호출합니다.

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=7)]

Kestrel 옵션을 구성해야 하는 경우 다음 예제와 같이 *Program.cs*에서 `UseKestrel`을 호출합니다.

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=9-16)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet 패키지를 설치합니다.

다음 섹션과 같이 필요한 [Kestrel 옵션](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions)을 지정하여 `Main` 메서드에서 `WebHostBuilder`의 [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 확장 메서드를 호출합니다.

[!code-csharp[](kestrel/sample1/Program.cs?name=snippet_Main&highlight=13-19)]

---

### <a name="kestrel-options"></a>Kestrel 옵션

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

Kestrel 웹 서버에는 인터넷 연결 배포에 특히 유용한 제약 조건 구성 옵션이 있습니다. 다음은 설정할 수 있는 몇 가지 제한입니다.

- 최대 클라이언트 연결
- 최대 요청 본문 크기
- 최소 요청 본문 데이터 속도

[KestrelServerOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerOptions.cs) 클래스의 `Limits` 속성에서 이러한 제약 조건 및 그 외 항목을 설정합니다. `Limits` 속성은 [KestrelServerLimits](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerLimits.cs) 클래스의 인스턴스를 보유합니다. 

**최대 클라이언트 연결**

다음 코드를 사용하여 전체 응용 프로그램에 대한 동시 개방 TCP 연결의 최대 수를 설정할 수 있습니다.

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=3-4)]

HTTP 또는 HTTPS에서 다른 프로토콜(예: WebSocket 요청에서)로 업그레이드된 연결에 대한 별도 제한이 있습니다. 연결이 업그레이드된 후 `MaxConcurrentConnections` 제한에 대해 계산되지 않습니다. 

연결의 최대 수는 기본적으로 무제한(null)입니다.

**최대 요청 본문 크기**

기본 최대 요청 본문 크기는 약 28.6MB인 30,000,000바이트입니다. 

ASP.NET Core MVC 앱에서 한도를 재정의할 때는 작업 메서드에서 [RequestSizeLimit](https://github.com/aspnet/Mvc/blob/rel/2.0.0/src/Microsoft.AspNetCore.Mvc.Core/RequestSizeLimitAttribute.cs) 특성을 사용하는 방법이 좋습니다.

```csharp
[RequestSizeLimit(100000000)]
public IActionResult MyActionMethod()
```

다음 예제는 전체 응용 프로그램, 모든 요청에 대한 제약 조건을 구성하는 방법을 보여 줍니다.

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=5)]

미들웨어에서 특정 요청에 대한 설정을 재정의할 수 있습니다.

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Limits&highlight=3-4)]
 
응용 프로그램에서 요청을 읽기 시작한 후 요청에 대한 제한을 구성하려고 하면 예외가 throw됩니다. `MaxRequestBodySize` 속성이 제한을 구성하기에 너무 늦은, 읽기 전용 상태인지를 알려주는 `IsReadOnly` 속성이 있습니다.

**최소 요청 본문 데이터 속도**

Kestrel은 데이터가 지정된 속도(바이트/초)로 들어오는지 1초마다 확인합니다. 속도가 최소 아래로 떨어지면 연결이 시간 초과됩니다. 유예 기간은 Kestrel에서 해당 전송 속도를 최소로 높이기 위해 클라이언트에 제공하는 총 시간입니다. 이 시간 동안 속도는 확인되지 않습니다. 유예 기간은 TCP 느린 시작으로 인해 느린 속도로 처음에 데이터를 보내는 연결 중단을 방지하는 데 도움이 됩니다.

기본 최소 속도는 5초의 유예 기간으로 240바이트/초입니다.

최소 속도는 응답에도 적용됩니다. 요청 제한 및 응답 제한을 설정하는 코드는 속성 및 인터페이스 이름에 `RequestBody` 또는 `Response`를 갖는 것을 제외하고 동일합니다. 

*Program.cs*에서 최소 데이터 속도를 구성하는 방법을 보여 주는 예제는 다음과 같습니다.

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=6-9)]

미들웨어에서 요청별 속도를 구성할 수 있습니다.

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Limits&highlight=5-8)]

다른 Kestrel 옵션에 대한 내용은 다음 클래스를 참조하세요.

* [KestrelServerOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerOptions.cs)
* [KestrelServerLimits](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerLimits.cs)
* [ListenOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/ListenOptions.cs)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

Kestrel 옵션에 대한 정보는 [KestrelServerOptions 클래스](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions)를 참조하세요.

---

### <a name="endpoint-configuration"></a>엔드포인트 구성

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

기본적으로 ASP.NET Core는 `http://localhost:5000`으로 바인딩합니다. `KestrelServerOptions`의 `Listen` 또는 `ListenUnixSocket` 메서드를 호출하여 수신 대기하도록 Kestrel에 대한 URL 접두사 및 포트를 구성합니다. (`UseUrls`, `urls` 명령줄 인수 및 ASPNETCORE_URLS 환경 변수도 작동하지만 [이 문서의 뒷부분](#useurls-limitations)에 명시된 제한 사항이 있습니다.)

**TCP 소켓에 바인딩**

`Listen` 메서드는 TCP 소켓에 바인딩하고 옵션 람다를 통해 SSL 인증서를 구성할 수 있습니다.

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=9-16)]

[ListenOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/ListenOptions.cs)를 사용하여 이 예에서 특정 엔드포인트에 대한 SSL을 구성하는 방법을 확인합니다. 동일한 API를 사용하여 특정 엔드포인트에 대한 다른 Kestrel 설정을 구성할 수 있습니다.

[!INCLUDE[How to make an SSL cert](../../includes/make-ssl-cert.md)]

**Unix 소켓에 바인딩**

이 예제에 나와 있는 것처럼 Nginx를 사용하여 향상된 성능을 위해 Unix 소켓을 수신 대기할 수 있습니다.

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_UnixSocket)]

**포트 0**

포트 번호 0을 지정하는 경우 Kestrel은 동적으로 사용 가능한 포트에 바인딩합니다. 다음 예제에서는 Kestrel이 실제로 런타임에 바인딩한 포트를 확인하는 방법을 보여 줍니다.

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Configure&highlight=3,13,16-17)]

<a id="useurls-limitations"></a>

**UseUrls 제한 사항**

`UseUrls` 메서드를 호출하거나 `urls` 명령줄 인수 또는 ASPNETCORE_URLS 환경 변수를 사용하여 엔드포인트를 구성할 수 있습니다. 이러한 메서드는 코드를 Kestrel이 아닌 서버와 작동하도록 하려는 경우 유용합니다. 그러나 이러한 제한 사항을 고려해야 합니다.

* 이러한 메서드로 SSL을 사용할 수 없습니다.
* `Listen` 메서드 및 `UseUrls` 모두를 사용하는 경우 `Listen` 엔드포인트는 `UseUrls` 엔드포인트를 재정의합니다.

**IIS에 대한 엔드포인트 구성**

IIS를 사용하는 경우 IIS에 대한 URL 바인딩은 `Listen` 또는 `UseUrls`를 호출하여 설정하는 모든 바인딩을 재정의합니다. 자세한 내용은 [ASP.NET Core 모듈 소개](aspnet-core-module.md)를 참조하세요.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

기본적으로 ASP.NET Core는 `http://localhost:5000`으로 바인딩합니다. `UseUrls` 확장 메서드, `urls` 명령줄 인수 또는 ASP.NET Core 구성 시스템을 사용하여 수신하도록 Kestrel에 대한 URL 접두사와 포트를 구성할 수 있습니다. 이러한 메서드에 대한 자세한 내용은 [호스팅](../../fundamentals/hosting.md)을 참조하세요. 역방향 프록시로 IIS를 사용하는 경우 URL 바인딩이 작동하는 방법에 대한 자세한 내용은 [ASP.NET Core 모듈](aspnet-core-module.md)을 참조하세요. 

---

### <a name="url-prefixes"></a>URL 접두사

`UseUrls`를 호출하거나 `urls` 명령줄 인수 또는 ASPNETCORE_URLS 환경 변수를 사용하는 경우 URL 접두사는 다음 형식 중 하나일 수 있습니다. 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

HTTP URL 접두사만 유효합니다. Kestrel은 `UseUrls`를 사용하여 URL 바인딩을 구성하는 경우 SSL을 지원하지 않습니다.

* 포트 번호가 있는 IPv4 주소

  ```
  http://65.55.39.10:80/
  ```

  0.0.0.0은 모든 IPv4 주소에 바인딩하는 특별한 경우입니다.


* 포트 번호가 있는 IPv6 주소

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/ 
  ```

  [:]는 IPv4 0.0.0.0에 해당하는 IPv6입니다.


* 포트 번호가 있는 호스트 이름

  ```
  http://contoso.com:80/
  http://*:80/
  ```

  호스트 이름, * 및 +는 특별하지 않습니다. 인식되는 IP 주소 또는 "localhost"가 아닌 모든 항목은 모든 IPv4 및 IPv6 IP에 바인딩합니다. 서로 다른 호스트 이름을 같은 포트에서 서로 다른 ASP.NET Core 응용 프로그램에 바인딩해야 하는 경우 [HTTP.sys](httpsys.md) 또는 IIS, Nginx 또는 Apache와 같은 역방향 프록시 서버를 사용합니다.

* 포트 번호가 있는 "Localhost" 이름 또는 포트 번호가 있는 루프백 IP

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  `localhost`가 지정되면 Kestrel은 IPv4 및 IPv6 루프백 인터페이스 모두에 바인딩하려고 합니다. 요청된 포트가 루프백 인터페이스 중 하나의 다른 서비스에서 사용 중인 경우 Kestrel은 시작에 실패합니다. 루프백 인터페이스 중 하나를 다른 이유(일반적으로 IPv6이 지원되지 않으므로)로 사용할 수 없는 경우 Kestrel은 경고를 기록합니다. 

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

* 포트 번호가 있는 IPv4 주소

  ```
  http://65.55.39.10:80/
  https://65.55.39.10:443/
  ```

  0.0.0.0은 모든 IPv4 주소에 바인딩하는 특별한 경우입니다.


* 포트 번호가 있는 IPv6 주소

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/ 
  https://[0:0:0:0:0:ffff:4137:270a]:443/ 
  ```

  [:]는 IPv4 0.0.0.0에 해당하는 IPv6입니다.


* 포트 번호가 있는 호스트 이름

  ```
  http://contoso.com:80/
  http://*:80/
  https://contoso.com:443/
  https://*:443/
  ```

  호스트 이름, \* 및 +는 특별하지 않습니다. 인식되는 IP 주소 또는 "localhost"가 아닌 모든 항목은 모든 IPv4 및 IPv6 IP에 바인딩합니다. 서로 다른 호스트 이름을 같은 포트에서 서로 다른 ASP.NET Core 응용 프로그램에 바인딩해야 하는 경우 [WebListener](weblistener.md) 또는 IIS, Nginx 또는 Apache와 같은 역방향 프록시 서버를 사용합니다.

* 포트 번호가 있는 "Localhost" 이름 또는 포트 번호가 있는 루프백 IP

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

포트 번호 0을 지정하는 경우 Kestrel은 동적으로 사용 가능한 포트에 바인딩합니다. 포트 0에 바인딩은 `localhost` 이름을 제외하고 모든 호스트 이름 또는 IP에 허용됩니다.

다음 예제에서는 Kestrel이 실제로 런타임에 바인딩한 포트를 확인하는 방법을 보여 줍니다.

[!code-csharp[](kestrel/sample1/Startup.cs?name=snippet_Configure)]

**SSL에 대한 URL 접두사**

다음과 같이 `UseHttps` 확장 메서드를 호출하는 경우 `https:`로 URL 접두사를 포함해야 합니다.

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

[!INCLUDE[How to make an SSL cert](../../includes/make-ssl-cert.md)]

---
## <a name="next-steps"></a>다음 단계

자세한 내용은 다음 리소스를 참조하세요.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

* [2.x용 샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample2)
* [Kestrel 소스 코드](https://github.com/aspnet/KestrelHttpServer)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

* [1.x용 샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample1)
* [Kestrel 소스 코드](https://github.com/aspnet/KestrelHttpServer)

---
