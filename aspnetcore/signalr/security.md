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
# <a name="security-considerations-in-aspnet-core-signalr"></a><span data-ttu-id="66af6-103">ASP.NET Core SignalR의 보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="66af6-103">Security considerations in ASP.NET Core SignalR</span></span>

<span data-ttu-id="66af6-104">[Andrew Stanton-nurse](https://twitter.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="66af6-104">By [Andrew Stanton-Nurse](https://twitter.com/anurse)</span></span>

## <a name="overview"></a><span data-ttu-id="66af6-105">개요</span><span class="sxs-lookup"><span data-stu-id="66af6-105">Overview</span></span>

<span data-ttu-id="66af6-106">SignalR은 기본적으로 다양 한 보안 보호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-106">SignalR provides a number of security protections by default.</span></span> <span data-ttu-id="66af6-107">이러한 보호를 구성 하는 방법을 이해 하는 것이 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-107">It's important to understand how to configure these protections.</span></span>

### <a name="cross-origin-resource-sharing"></a><span data-ttu-id="66af6-108">크로스-원본 자원 공유</span><span class="sxs-lookup"><span data-stu-id="66af6-108">Cross-origin resource sharing</span></span>

<span data-ttu-id="66af6-109">[크로스-원본 자원 공유 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) 브라우저에서 크로스-원본 SignalR 연결을 허용 하도록 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-109">[Cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) can be used to allow cross-origin SignalR connections in the browser.</span></span> <span data-ttu-id="66af6-110">사용 하도록 설정 해야 하는 JavaScript 코드, SignalR 앱에서 다른 도메인 이름에서 호스팅되는 경우는 [ASP.NET Core CORS 미들웨어](xref:security/cors) 연결을 허용 하려면.</span><span class="sxs-lookup"><span data-stu-id="66af6-110">If your JavaScript code is hosted on a different domain name from your SignalR app, you have to enable the [ASP.NET Core CORS middleware](xref:security/cors) in order to allow the connection.</span></span> <span data-ttu-id="66af6-111">일반적으로 제어 하는 도메인에서 원본 간 요청을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-111">In general, allow cross-origin requests only from domains you control.</span></span> <span data-ttu-id="66af6-112">예를 들어 사이트에서 호스팅되는 경우 `http://www.example.com` SignalR 앱에서 호스트 될 `http://signalr.example.com`, 원본만 사용할 수 있도록 SignalR 앱에서 CORS를 구성 해야 `www.example.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-112">For example, if your site is hosted on `http://www.example.com` and your SignalR app is hosted on `http://signalr.example.com`, you should configure CORS in your SignalR app to only allow the origin `www.example.com`.</span></span>

<span data-ttu-id="66af6-113">CORS를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [ASP.NET Core CORS에 대 한 설명서](xref:security/cors)합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-113">For more information on configuring CORS, see [the documentation on ASP.NET Core CORS](xref:security/cors).</span></span> <span data-ttu-id="66af6-114">SignalR에서 제대로 작동 하기 위해 다음 CORS 정책이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-114">SignalR requires the following CORS policies in order to operate correctly:</span></span>

* <span data-ttu-id="66af6-115">정책에는 예상 또는 (권장 하지 않음) 모든 원본을 허용 하 고 특정 원본을 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-115">The policy must allow the specific origins you expect, or allow any origin (not recommended).</span></span>
* <span data-ttu-id="66af6-116">HTTP 메서드 `GET` 고 `POST` 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-116">HTTP methods `GET` and `POST` must be allowed.</span></span>
* <span data-ttu-id="66af6-117">자격 증명 인증을 사용 하지 않는 경우에 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-117">Credentials must be enabled, even when you aren't using authentication.</span></span>

<span data-ttu-id="66af6-118">다음 CORS 정책에서 SignalR 브라우저 클라이언트에서 호스트를 허용 하는 예를 들어 `http://example.com` SignalR 앱에 액세스 하려면:</span><span class="sxs-lookup"><span data-stu-id="66af6-118">For example, the following CORS policy allows a SignalR browser client hosted on `http://example.com` to access your SignalR app:</span></span>

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
> <span data-ttu-id="66af6-119">SignalR은 Azure App Service의 기본 제공 CORS 기능을 사용 하 여 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-119">SignalR is not compatible with the built-in CORS feature in Azure App Service.</span></span>

### <a name="websocket-origin-restriction"></a><span data-ttu-id="66af6-120">WebSocket 원본 제한</span><span class="sxs-lookup"><span data-stu-id="66af6-120">WebSocket Origin Restriction</span></span>

<span data-ttu-id="66af6-121">CORS에서 제공 하는 보호 websocket 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-121">The protections provided by CORS do not apply to WebSockets.</span></span> <span data-ttu-id="66af6-122">브라우저 사전 CORS 요청을 수행 하지 않습니다 또는에 지정 된 제한 사항을 고려 않는 `Access-Control` WebSocket 요청을 생성할 때 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-122">Browsers do not perform CORS pre-flight requests, nor do they respect the restrictions specified in `Access-Control` headers when making WebSocket requests.</span></span> <span data-ttu-id="66af6-123">그러나 브라우저를 보낼 수행을 `Origin` WebSocket 요청을 발급 하는 경우 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-123">However, browsers do send the `Origin` header when issuing WebSocket requests.</span></span> <span data-ttu-id="66af6-124">이러한 헤더는 허용 되는 것이 원하는 원본에서 가져온만 Websocket을 보장 하기 위해 유효성을 검사 하는 응용 프로그램을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-124">You should configure your application to validate these headers in order to ensure that only WebSockets coming from the origins you expect are allowed.</span></span>

<span data-ttu-id="66af6-125">ASP.NET Core 2.1에서 수행할 수 있습니다 배치할 수 있습니다 하는 사용자 지정 미들웨어를 사용 하 여 **위에 `UseSignalR`, 및 모든 인증 미들웨어** 에서 프로그램 `Configure` 메서드:</span><span class="sxs-lookup"><span data-stu-id="66af6-125">In ASP.NET Core 2.1, this can be achieved using a custom middleware you can place **above `UseSignalR`, and any authentication middleware** in your `Configure` method:</span></span>

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
> <span data-ttu-id="66af6-126">합니다 `Origin` 클라이언트에서 그리고 헤더 완전히 제어는 `Referer` 헤더 가짜일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-126">The `Origin` header is completely controlled by the client and, like the `Referer` header, can be faked.</span></span> <span data-ttu-id="66af6-127">이러한 헤더는 인증 메커니즘으로 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-127">These headers should never be used as an authentication mechanism.</span></span>

### <a name="access-token-logging"></a><span data-ttu-id="66af6-128">액세스 토큰 로깅</span><span class="sxs-lookup"><span data-stu-id="66af6-128">Access token logging</span></span>

<span data-ttu-id="66af6-129">Websocket 또는 Server-Sent 이벤트를 사용 하면 브라우저 클라이언트가 쿼리 문자열에 액세스 토큰을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-129">When using WebSockets or Server-Sent Events, the browser client sends the access token in the query string.</span></span> <span data-ttu-id="66af6-130">하지만이 일반적으로 표준을 사용 하는 것 만큼 안전 `Authorization` 헤더를 여러 웹 서버에서 각 요청에 대 한 URL를 기록 쿼리 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-130">This is generally as secure as using the standard `Authorization` header, however many web servers log the URL for each request, including the query string.</span></span> <span data-ttu-id="66af6-131">즉, 액세스 토큰을 로그에 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-131">This means the access token may be included in logs.</span></span> <span data-ttu-id="66af6-132">이 정보를 기록 하지 않으려면 웹 서버 로깅 설정을 검토 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-132">Consider reviewing the web server's logging settings to avoid logging this information.</span></span>

### <a name="exceptions"></a><span data-ttu-id="66af6-133">예외</span><span class="sxs-lookup"><span data-stu-id="66af6-133">Exceptions</span></span>

<span data-ttu-id="66af6-134">예외 메시지는 일반적으로 클라이언트에 게 공개 하지 않아야 하는 중요 한 데이터를 간주 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-134">Exception messages are generally considered sensitive data that shouldn't be revealed to a client.</span></span> <span data-ttu-id="66af6-135">기본적으로 SignalR 클라이언트에 허브 메서드에서 throw 된 예외 세부 정보를 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-135">By default, SignalR doesn't send the details of an exception thrown by a hub method to the client.</span></span> <span data-ttu-id="66af6-136">대신 클라이언트에는 오류가 발생 했음을 나타내는 일반 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-136">Instead, the client receives a generic message indicating an error occurred.</span></span> <span data-ttu-id="66af6-137">설정 하 여이 동작을 재정의할 수는 [ `EnableDetailedErrors` ](xref:signalr/configuration#configure-server-options) 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-137">You can override this behavior by setting the [`EnableDetailedErrors`](xref:signalr/configuration#configure-server-options) setting.</span></span>

### <a name="buffer-management"></a><span data-ttu-id="66af6-138">버퍼 관리</span><span class="sxs-lookup"><span data-stu-id="66af6-138">Buffer management</span></span>

<span data-ttu-id="66af6-139">SignalR 들어오고 나가는 메시지를 관리 하기 위해 연결당 버퍼를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-139">SignalR uses per-connection buffers in order to manage incoming and outgoing messages.</span></span> <span data-ttu-id="66af6-140">기본적으로 SignalR 32KB로 이러한 버퍼를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-140">By default, SignalR limits these buffers to 32KB.</span></span> <span data-ttu-id="66af6-141">즉, 클라이언트 또는 서버 보낼 수 있는 가장 큰 가능한 메시지는 32KB입니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-141">This means the largest possible message a client or server can send is 32KB.</span></span> <span data-ttu-id="66af6-142">즉, 메시지에 대 한 연결에 사용 된 메모리의 최대 크기는 32KB입니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-142">This also means the maximum amount of memory consumed by a connection for messages is 32KB.</span></span> <span data-ttu-id="66af6-143">메시지는이 제한 보다 작은 항상 알고 있는 경우에 클라이언트가 큰 메시지를 보내고 수락 하도록 메모리를 할당 하도록 서버에 적용 되지 않도록 방지 하기 위해이 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-143">If you know your messages are always smaller than this limit, you can reduce this size to prevent a client from being able to send a larger message and force the server to allocate memory to accept it.</span></span> <span data-ttu-id="66af6-144">마찬가지로, 메시지는이 제한 보다 큰를 알고 있으면 해당 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-144">Similarly, if you know your messages are larger than this limit, you can increase it.</span></span> <span data-ttu-id="66af6-145">그러나 주의 하십시오이 제한을 늘리면 의미 클라이언트 추가 메모리를 할당 하도록 서버를 발생 시킬 수 이며 앱이 처리할 수 있는 동시 연결 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-145">However, be aware that increasing this limit means that the client is able to cause the server to allocate additional memory and may reduce the number of concurrent connections your app can handle.</span></span>

<span data-ttu-id="66af6-146">들어오고 나가는 메시지에 대 한 별도 제한은, 둘 다에서 구성할 수 있습니다 합니다 [ `HttpConnectionDispatcherOptions` ](xref:signalr/configuration#configure-server-options) 개체에 구성 된 `MapHub`:</span><span class="sxs-lookup"><span data-stu-id="66af6-146">There are separate limits for incoming and outgoing messages, both can be configured on the [`HttpConnectionDispatcherOptions`](xref:signalr/configuration#configure-server-options) object configured in `MapHub`:</span></span>

* <span data-ttu-id="66af6-147">`ApplicationMaxBufferSize` 클라이언트에서 바이트의 최대 수를 나타냅니다는 서버 버퍼입니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-147">`ApplicationMaxBufferSize` represents the maximum number of bytes from the client that the server buffers.</span></span> <span data-ttu-id="66af6-148">클라이언트를이 제한 보다 큰 메시지를 전송 하려고 하는 경우 연결이 닫힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-148">If the client attempts to send a message larger than this limit, the connection may be closed.</span></span>
* <span data-ttu-id="66af6-149">`TransportMaxBufferSize` 바이트를 보낼 수의 최대 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-149">`TransportMaxBufferSize` represents the maximum number of bytes the server can send.</span></span> <span data-ttu-id="66af6-150">서버 메시지를 보내려고 시도 하는 경우 (허브 메서드의 반환 값 포함)이이 제한 보다 큰 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-150">If the server attempts to send a message (includes return values from hub methods) larger than this limit, an exception will be thrown.</span></span>

<span data-ttu-id="66af6-151">제한 설정을 `0` 한계를 완전히 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-151">Setting the limit to `0` disables the limit entirely.</span></span> <span data-ttu-id="66af6-152">그러나이 주의 사용 하 여 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-152">However, this should be done with extreme caution.</span></span> <span data-ttu-id="66af6-153">도 제거 하면 모든 규모의 메시지를 보내는 클라이언트 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-153">Removing the limit allows a client to send a message of any size.</span></span> <span data-ttu-id="66af6-154">이 앱에서 지원할 수 있습니다 동시 연결 수를 크게 줄일 수 있습니다 하는 악의적인 클라이언트가 과도 한 메모리를 할당할 수를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66af6-154">This could be used by a malicious client to cause excess memory to be allocated, which could dramatically reduce the number of concurrent connections your app can support.</span></span>
