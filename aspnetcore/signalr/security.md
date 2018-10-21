---
title: ASP.NET Core SignalR의 보안 고려 사항
author: tdykstra
description: ASP.NET Core SignalR의 인증 및 권한 부여를 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: anurse
ms.custom: mvc
ms.date: 10/17/2018
uid: signalr/security
ms.openlocfilehash: 1adf762cd6de4f0cf62e31c0ec6e595a32ed56f8
ms.sourcegitcommit: f5d403004f3550e8c46585fdbb16c49e75f495f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2018
ms.locfileid: "49477542"
---
# <a name="security-considerations-in-aspnet-core-signalr"></a><span data-ttu-id="0066e-103">ASP.NET Core SignalR의 보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="0066e-103">Security considerations in ASP.NET Core SignalR</span></span>

<span data-ttu-id="0066e-104">[Andrew Stanton-nurse](https://twitter.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="0066e-104">By [Andrew Stanton-Nurse](https://twitter.com/anurse)</span></span>

<span data-ttu-id="0066e-105">이 문서에서 SignalR 보안 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-105">This article provides information on securing SignalR.</span></span>

## <a name="cross-origin-resource-sharing"></a><span data-ttu-id="0066e-106">크로스-원본 자원 공유</span><span class="sxs-lookup"><span data-stu-id="0066e-106">Cross-origin resource sharing</span></span>

<span data-ttu-id="0066e-107">[크로스-원본 자원 공유 (CORS)](https://www.w3.org/TR/cors/) 브라우저에서 크로스-원본 SignalR 연결을 허용 하도록 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-107">[Cross-origin resource sharing (CORS)](https://www.w3.org/TR/cors/) can be used to allow cross-origin SignalR connections in the browser.</span></span> <span data-ttu-id="0066e-108">JavaScript 코드는 SignalR 앱에서 다른 도메인에서 호스팅되는 경우 [CORS 미들웨어](xref:security/cors) SignalR 앱에 연결 하는 JavaScript를 허용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-108">If JavaScript code is hosted on a different domain from the SignalR app, [CORS middleware](xref:security/cors) must be enabled to allow the JavaScript to connect to the SignalR app.</span></span> <span data-ttu-id="0066e-109">신뢰 하는 도메인 또는 컨트롤 에서만 크로스-원본 요청을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-109">Allow cross-origin requests only from domains you trust or control.</span></span> <span data-ttu-id="0066e-110">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="0066e-110">For example:</span></span>

* <span data-ttu-id="0066e-111">사이트에서 호스팅됩니다. `http://www.example.com`</span><span class="sxs-lookup"><span data-stu-id="0066e-111">Your site is hosted on `http://www.example.com`</span></span>
* <span data-ttu-id="0066e-112">SignalR 앱에서 호스팅됩니다. `http://signalr.example.com`</span><span class="sxs-lookup"><span data-stu-id="0066e-112">Your SignalR app is hosted on `http://signalr.example.com`</span></span>

<span data-ttu-id="0066e-113">원본만 사용할 수 있도록 SignalR 앱에서 CORS를 구성 해야 `www.example.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-113">CORS should be configured in the SignalR app to only allow the origin `www.example.com`.</span></span>

<span data-ttu-id="0066e-114">CORS를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [크로스-원본 요청 (CORS)](xref:security/cors)합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-114">For more information on configuring CORS, see [Enable Cross-Origin Requests (CORS)](xref:security/cors).</span></span> <span data-ttu-id="0066e-115">SignalR **필요** 다음 CORS 정책:</span><span class="sxs-lookup"><span data-stu-id="0066e-115">SignalR **requires** the following CORS policies:</span></span>

* <span data-ttu-id="0066e-116">특정 예상된 원본을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-116">Allow the specific expected origins.</span></span> <span data-ttu-id="0066e-117">모든 원본을 허용 수 있지만 **되지** 보안 또는 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-117">Allowing any origin is possible but is **not** secure or recommended.</span></span>
* <span data-ttu-id="0066e-118">HTTP 메서드 `GET` 고 `POST` 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-118">HTTP methods `GET` and `POST` must be allowed.</span></span>
* <span data-ttu-id="0066e-119">자격 증명 인증 사용 되지 않는 경우에 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-119">Credentials must be enabled, even when authentication is not used.</span></span>

<span data-ttu-id="0066e-120">다음 CORS 정책에서 SignalR 브라우저 클라이언트에서 호스트를 허용 하는 예를 들어 `http://example.com` 에 호스트 된 SignalR 앱에 액세스 하도록 `http://signalr.example.com`:</span><span class="sxs-lookup"><span data-stu-id="0066e-120">For example, the following CORS policy allows a SignalR browser client hosted on `http://example.com` to access the SignalR app hosted on `http://signalr.example.com`:</span></span>

[!code-csharp[Main](security/sample/Startup.cs?name=snippet1)]

> [!NOTE]
> <span data-ttu-id="0066e-121">SignalR은 Azure App Service의 기본 제공 CORS 기능을 사용 하 여 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-121">SignalR is not compatible with the built-in CORS feature in Azure App Service.</span></span>

## <a name="websocket-origin-restriction"></a><span data-ttu-id="0066e-122">WebSocket 원본 제한</span><span class="sxs-lookup"><span data-stu-id="0066e-122">WebSocket Origin Restriction</span></span>

<span data-ttu-id="0066e-123">CORS에서 제공 하는 보호는 websocket 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-123">The protections provided by CORS don't apply to WebSockets.</span></span> <span data-ttu-id="0066e-124">브라우저 수행 **되지**:</span><span class="sxs-lookup"><span data-stu-id="0066e-124">Browsers do **not**:</span></span>

* <span data-ttu-id="0066e-125">사전 CORS 요청을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-125">Perform CORS pre-flight requests.</span></span>
* <span data-ttu-id="0066e-126">에 지정 된 제한 사항을 준수 `Access-Control` WebSocket 요청을 생성할 때 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-126">Respect the restrictions specified in `Access-Control` headers when making WebSocket requests.</span></span>

<span data-ttu-id="0066e-127">그러나 브라우저를 보낼 수행을 `Origin` WebSocket 요청을 발급 하는 경우 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-127">However, browsers do send the `Origin` header when issuing WebSocket requests.</span></span> <span data-ttu-id="0066e-128">응용 프로그램을 예상된 원본에서 제공 하는 Websocket만 허용 되는지 확인 하려면 이러한 헤더를 검사할 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-128">Applications should be configured to validate these headers to ensure that only WebSockets coming from the expected origins are allowed.</span></span>

<span data-ttu-id="0066e-129">배치 하는 사용자 지정 미들웨어를 사용 하 여 헤더 유효성 검사 가능 ASP.NET Core 2.1 이상 버전에서는 **하기 전에 `UseSignalR`, 및 인증 미들웨어** 에서 `Configure`:</span><span class="sxs-lookup"><span data-stu-id="0066e-129">In ASP.NET Core 2.1 and later, header validation can be achieved using a custom middleware placed **before `UseSignalR`, and authentication middleware** in `Configure`:</span></span>

[!code-csharp[Main](security/sample/Startup.cs?name=snippet2)]

> [!NOTE]
> <span data-ttu-id="0066e-130">합니다 `Origin` 헤더는 클라이언트에서 그리고 제어 되는 `Referer` 헤더 가짜일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-130">The `Origin` header is controlled by the client and, like the `Referer` header, can be faked.</span></span> <span data-ttu-id="0066e-131">이러한 헤더 해야 **되지** 인증 메커니즘으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-131">These headers should **not** be used as an authentication mechanism.</span></span>

## <a name="access-token-logging"></a><span data-ttu-id="0066e-132">액세스 토큰 로깅</span><span class="sxs-lookup"><span data-stu-id="0066e-132">Access token logging</span></span>

<span data-ttu-id="0066e-133">Websocket 또는 Server-Sent 이벤트를 사용 하면 브라우저 클라이언트가 쿼리 문자열에 액세스 토큰을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-133">When using WebSockets or Server-Sent Events, the browser client sends the access token in the query string.</span></span> <span data-ttu-id="0066e-134">쿼리 문자열을 통해 액세스 토큰을 수신 하는 것은 일반적으로 표준을 사용 하는 것 만큼 안전 `Authorization` 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-134">Receiving the access token via query string is generally as secure as using the standard `Authorization` header.</span></span> <span data-ttu-id="0066e-135">그러나 여러 웹 서버 로그 쿼리 문자열을 포함 하 여 각 요청에 대 한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-135">However, many web servers log the URL for each request, including the query string.</span></span> <span data-ttu-id="0066e-136">로그인 Url 액세스 토큰을 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-136">Logging the URLs may log the access token.</span></span> <span data-ttu-id="0066e-137">웹 서버 로깅 설정을 로깅 액세스 토큰을 방지 하기 위해 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-137">A best practice is to set the web server's logging settings to prevent logging access tokens.</span></span>

## <a name="exceptions"></a><span data-ttu-id="0066e-138">예외</span><span class="sxs-lookup"><span data-stu-id="0066e-138">Exceptions</span></span>

<span data-ttu-id="0066e-139">예외 메시지는 일반적으로 클라이언트에 게 공개 하지 않아야 하는 중요 한 데이터를 간주 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-139">Exception messages are generally considered sensitive data that shouldn't be revealed to a client.</span></span> <span data-ttu-id="0066e-140">기본적으로 SignalR 클라이언트에 허브 메서드에서 throw 된 예외 세부 정보를 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-140">By default, SignalR doesn't send the details of an exception thrown by a hub method to the client.</span></span> <span data-ttu-id="0066e-141">대신 클라이언트에는 오류가 발생 했음을 나타내는 일반 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-141">Instead, the client receives a generic message indicating an error occurred.</span></span> <span data-ttu-id="0066e-142">클라이언트에 예외 메시지 배달을 사용 하 여 (예: 개발 또는 테스트) 재정의할 수 있습니다 [ `EnableDetailedErrors` ](xref:signalr/configuration#configure-server-options)합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-142">Exception message delivery to the client can be overridden (for example in development or test) with [`EnableDetailedErrors`](xref:signalr/configuration#configure-server-options).</span></span> <span data-ttu-id="0066e-143">예외 메시지를 프로덕션 앱에서 클라이언트에 노출 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-143">Exception messages should not be exposed to the client in production apps.</span></span>

## <a name="buffer-management"></a><span data-ttu-id="0066e-144">버퍼 관리</span><span class="sxs-lookup"><span data-stu-id="0066e-144">Buffer management</span></span>

<span data-ttu-id="0066e-145">SignalR은 연결당 버퍼를 사용 하 여 들어오고 나가는 메시지를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-145">SignalR uses per-connection buffers to manage incoming and outgoing messages.</span></span> <span data-ttu-id="0066e-146">기본적으로 SignalR 32KB로 이러한 버퍼를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-146">By default, SignalR limits these buffers to 32 KB.</span></span> <span data-ttu-id="0066e-147">클라이언트 또는 서버 보낼 수 있는 가장 큰 메시지는 32KB입니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-147">The largest message a client or server can send is 32 KB.</span></span> <span data-ttu-id="0066e-148">메시지에 대 한 연결에서 사용 하는 최대 메모리는 32KB입니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-148">The maximum memory consumed by a connection for messages is 32 KB.</span></span> <span data-ttu-id="0066e-149">32KB 보다 작은 항상 메시지 경우 제한을 줄일 수 있습니다는.</span><span class="sxs-lookup"><span data-stu-id="0066e-149">If your messages are always smaller than 32 KB, you can reduce the limit, which:</span></span>

* <span data-ttu-id="0066e-150">클라이언트가 큰 메시지를 보낼 수 없도록 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-150">Prevents a client from being able to send a larger message.</span></span>
* <span data-ttu-id="0066e-151">서버는 메시지를 받을 큰 버퍼를 할당할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-151">The server will never need to allocate large buffers to accept messages.</span></span>

<span data-ttu-id="0066e-152">메시지 32KB 보다 큰 경우에 한도 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-152">If your messages are larger than 32 KB, you can increase the limit.</span></span> <span data-ttu-id="0066e-153">이 제한을 늘리면 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-153">Increasing this limit means:</span></span>

* <span data-ttu-id="0066e-154">클라이언트는 대용량 메모리 버퍼를 할당 하도록 서버에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-154">The client can cause the server to allocate large memory buffers.</span></span>
* <span data-ttu-id="0066e-155">대용량 버퍼 server 할당 동시 연결 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-155">Server allocation of large buffers may reduce the number of concurrent connections.</span></span>

<span data-ttu-id="0066e-156">들어오고 나가는 메시지에 대 한 제한은, 둘 다에서 구성할 수 있습니다 합니다 [ `HttpConnectionDispatcherOptions` ](xref:signalr/configuration#configure-server-options) 개체에 구성 된 `MapHub`:</span><span class="sxs-lookup"><span data-stu-id="0066e-156">There are limits for incoming and outgoing messages, both can be configured on the [`HttpConnectionDispatcherOptions`](xref:signalr/configuration#configure-server-options) object configured in `MapHub`:</span></span>

* <span data-ttu-id="0066e-157">`ApplicationMaxBufferSize` 클라이언트에서 바이트의 최대 수를 나타냅니다는 서버 버퍼입니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-157">`ApplicationMaxBufferSize` represents the maximum number of bytes from the client that the server buffers.</span></span> <span data-ttu-id="0066e-158">클라이언트를이 제한 보다 큰 메시지를 전송 하려고 하는 경우 연결이 닫힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-158">If the client attempts to send a message larger than this limit, the connection may be closed.</span></span>
* <span data-ttu-id="0066e-159">`TransportMaxBufferSize` 바이트를 보낼 수의 최대 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-159">`TransportMaxBufferSize` represents the maximum number of bytes the server can send.</span></span> <span data-ttu-id="0066e-160">서버를이 제한 보다 큰 메시지 (허브 메서드의 반환 값 포함)를 전송 하려고 하는 경우 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-160">If the server attempts to send a message (including return values from hub methods) larger than this limit, an exception will be thrown.</span></span>

<span data-ttu-id="0066e-161">제한 설정을 `0` 제한을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-161">Setting the limit to `0` disables the limit.</span></span> <span data-ttu-id="0066e-162">도 제거 하면 모든 규모의 메시지를 보내는 클라이언트 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-162">Removing the limit allows a client to send a message of any size.</span></span> <span data-ttu-id="0066e-163">큰 메시지를 전송 하는 악의적인 클라이언트가 과도 한 메모리 할당 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-163">Malicious clients sending large messages can cause excess memory to be allocated.</span></span> <span data-ttu-id="0066e-164">과도 한 메모리 사용량 동시 연결 수를 크게 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0066e-164">Excess memory usage can significantly reduce the number of concurrent connections.</span></span>
