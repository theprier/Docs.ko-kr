---
title: ASP.NET Core SignalR의 보안 고려 사항
author: tdykstra
description: ASP.NET Core SignalR의 인증 및 권한 부여를 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: anurse
ms.custom: mvc
ms.date: 06/29/2018
uid: signalr/security
ms.openlocfilehash: 98b5eb7be87920aacf7a941f76ff652ae7905303
ms.sourcegitcommit: f43f430a166a7ec137fcad12ded0372747227498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49391260"
---
# <a name="security-considerations-in-aspnet-core-signalr"></a>ASP.NET Core SignalR의 보안 고려 사항

[Andrew Stanton-nurse](https://twitter.com/anurse)

## <a name="overview"></a>개요

SignalR은 기본적으로 다양 한 보안 보호를 제공합니다. 이러한 보호를 구성 하는 방법을 이해 하는 것이 반드시 합니다.

### <a name="cross-origin-resource-sharing"></a>크로스-원본 자원 공유

[크로스-원본 자원 공유 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) 브라우저에서 크로스-원본 SignalR 연결을 허용 하도록 사용할 수 있습니다. 사용 하도록 설정 해야 하는 JavaScript 코드, SignalR 앱에서 다른 도메인 이름에서 호스팅되는 경우는 [ASP.NET Core CORS 미들웨어](xref:security/cors) 연결을 허용 하려면. 일반적으로 제어 하는 도메인에서 원본 간 요청을 허용 합니다. 예를 들어 사이트에서 호스팅되는 경우 `http://www.example.com` SignalR 앱에서 호스트 될 `http://signalr.example.com`, 원본만 사용할 수 있도록 SignalR 앱에서 CORS를 구성 해야 `www.example.com`합니다.

CORS를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [ASP.NET Core CORS에 대 한 설명서](xref:security/cors)합니다. SignalR에서 제대로 작동 하기 위해 다음 CORS 정책이 필요 합니다.

* 정책에는 예상 또는 (권장 하지 않음) 모든 원본을 허용 하 고 특정 원본을 허용 해야 합니다.
* HTTP 메서드 `GET` 고 `POST` 허용 해야 합니다.
* 자격 증명 인증을 사용 하지 않는 경우에 사용할 수 있어야 합니다.

다음 CORS 정책에서 SignalR 브라우저 클라이언트에서 호스트를 허용 하는 예를 들어 `http://example.com` SignalR 앱에 액세스 하려면:

```csharp
public void Configure(IApplicationBuilder app)
{
    // ... other middleware ...

    // Make sure the CORS middleware is ahead of SignalR.
    app.UseCors(builder => {
        builder.WithOrigins("http://example.com")
            .AllowAnyHeader()
            .WithMethods("GET", "POST")
            .AllowCredentials();
    });

    // ... other middleware ...

    app.UseSignalR();

    // ... other middleware ...
}
```

> [!NOTE]
> SignalR은 Azure App Service의 기본 제공 CORS 기능을 사용 하 여 호환 되지 않습니다.

### <a name="websocket-origin-restriction"></a>WebSocket 원본 제한

CORS에서 제공 하는 보호 websocket 적용 되지 않습니다. 브라우저 사전 CORS 요청을 수행 하지 않습니다 또는에 지정 된 제한 사항을 고려 않는 `Access-Control` WebSocket 요청을 생성할 때 헤더입니다. 그러나 브라우저를 보낼 수행을 `Origin` WebSocket 요청을 발급 하는 경우 헤더입니다. 이러한 헤더는 허용 되는 것이 원하는 원본에서 가져온만 Websocket을 보장 하기 위해 유효성을 검사 하는 응용 프로그램을 구성 해야 합니다.

ASP.NET Core 2.1에서 수행할 수 있습니다 배치할 수 있습니다 하는 사용자 지정 미들웨어를 사용 하 여 **위에 `UseSignalR`, 및 모든 인증 미들웨어** 에서 프로그램 `Configure` 메서드:

```csharp
// In your Startup class, add a static field listing the allowed Origin values:
private static readonly HashSet<string> _allowedOrigins = new HashSet<string>()
{
    // Add allowed origins here. For example:
    "http://www.mysite.com",
    "http://mysite.com",
};

// In your Configure method:
public void Configure(IApplicationBuilder app)
{
    // ... other middleware ...

    // Validate Origin header on WebSocket requests to prevent unexpected cross-site WebSocket requests
    app.Use((context, next) =>
    {
        // Check for a WebSocket request.
        if(string.Equals(context.Request.Headers["Upgrade"], "websocket"))
        {
            var origin = context.Request.Headers["Origin"];

            // If there is no origin header, or if the origin header doesn't match an allowed value:
            if(string.IsNullOrEmpty(origin) && !_allowedOrigins.Contains(origin))
            {
                // The origin is not allowed, reject the request
                context.Response.StatusCode = StatusCodes.Status400BadRequest;
                return Task.CompletedTask;
            }
        }

        // The request is not a WebSocket request or is a valid Origin, so let it continue
        return next();
    });

    // ... other middleware ...

    app.UseSignalR();

    // ... other middleware ...
}
```

> [!NOTE]
> 합니다 `Origin` 클라이언트에서 그리고 헤더 완전히 제어는 `Referer` 헤더 가짜일 수 있습니다. 이러한 헤더는 인증 메커니즘으로 사용할 수는 없습니다.

### <a name="access-token-logging"></a>액세스 토큰 로깅

Websocket 또는 Server-Sent 이벤트를 사용 하면 브라우저 클라이언트가 쿼리 문자열에 액세스 토큰을 보냅니다. 하지만이 일반적으로 표준을 사용 하는 것 만큼 안전 `Authorization` 헤더를 여러 웹 서버에서 각 요청에 대 한 URL를 기록 쿼리 문자열을 포함 합니다. 즉, 액세스 토큰을 로그에 포함 될 수 있습니다. 이 정보를 기록 하지 않으려면 웹 서버 로깅 설정을 검토 하는 것이 좋습니다.

### <a name="exceptions"></a>예외

예외 메시지는 일반적으로 클라이언트에 게 공개 하지 않아야 하는 중요 한 데이터를 간주 해야 합니다. 기본적으로 SignalR 클라이언트에 허브 메서드에서 throw 된 예외 세부 정보를 보내지 않습니다. 대신 클라이언트에는 오류가 발생 했음을 나타내는 일반 메시지를 받습니다. 설정 하 여이 동작을 재정의할 수는 [ `EnableDetailedErrors` ](xref:signalr/configuration#configure-server-options) 설정 합니다.

### <a name="buffer-management"></a>버퍼 관리

SignalR 들어오고 나가는 메시지를 관리 하기 위해 연결당 버퍼를 사용 합니다. 기본적으로 SignalR 32KB로 이러한 버퍼를 제한합니다. 즉, 클라이언트 또는 서버 보낼 수 있는 가장 큰 가능한 메시지는 32KB입니다. 즉, 메시지에 대 한 연결에 사용 된 메모리의 최대 크기는 32KB입니다. 메시지는이 제한 보다 작은 항상 알고 있는 경우에 클라이언트가 큰 메시지를 보내고 수락 하도록 메모리를 할당 하도록 서버에 적용 되지 않도록 방지 하기 위해이 크기를 줄일 수 있습니다. 마찬가지로, 메시지는이 제한 보다 큰를 알고 있으면 해당 늘릴 수 있습니다. 그러나 주의 하십시오이 제한을 늘리면 의미 클라이언트 추가 메모리를 할당 하도록 서버를 발생 시킬 수 이며 앱이 처리할 수 있는 동시 연결 수를 줄일 수 있습니다.

들어오고 나가는 메시지에 대 한 별도 제한은, 둘 다에서 구성할 수 있습니다 합니다 [ `HttpConnectionDispatcherOptions` ](xref:signalr/configuration#configure-server-options) 개체에 구성 된 `MapHub`:

* `ApplicationMaxBufferSize` 클라이언트에서 바이트의 최대 수를 나타냅니다는 서버 버퍼입니다. 클라이언트를이 제한 보다 큰 메시지를 전송 하려고 하는 경우 연결이 닫힐 수 있습니다.
* `TransportMaxBufferSize` 바이트를 보낼 수의 최대 수를 나타냅니다. 서버 메시지를 보내려고 시도 하는 경우 (허브 메서드의 반환 값 포함)이이 제한 보다 큰 예외가 throw 됩니다.

제한 설정을 `0` 한계를 완전히 사용 하지 않도록 설정 합니다. 그러나이 주의 사용 하 여 수행 되어야 합니다. 도 제거 하면 모든 규모의 메시지를 보내는 클라이언트 있습니다. 이 앱에서 지원할 수 있습니다 동시 연결 수를 크게 줄일 수 있습니다 하는 악의적인 클라이언트가 과도 한 메모리를 할당할 수를 사용할 수 없습니다.
