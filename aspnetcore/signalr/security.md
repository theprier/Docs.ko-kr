---
title: ASP.NET Core SignalR의 보안 고려 사항
author: tdykstra
description: ASP.NET Core SignalR에서 인증 및 권한 부여를 사용하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: anurse
ms.custom: mvc
ms.date: 10/17/2018
uid: signalr/security
ms.openlocfilehash: 1adf762cd6de4f0cf62e31c0ec6e595a32ed56f8
ms.sourcegitcommit: f5d403004f3550e8c46585fdbb16c49e75f495f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2018
ms.locfileid: "49477542"
---
# <a name="security-considerations-in-aspnet-core-signalr"></a><span data-ttu-id="1b7d0-103">ASP.NET Core SignalR의 보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="1b7d0-103">Security considerations in ASP.NET Core SignalR</span></span>

<span data-ttu-id="1b7d0-104">작성자: [Andrew Stanton-Nurse](https://twitter.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="1b7d0-104">By [Andrew Stanton-Nurse](https://twitter.com/anurse)</span></span>

<span data-ttu-id="1b7d0-105">이 문서에서는 SignalR의 보안에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-105">This article provides information on securing SignalR.</span></span>

## <a name="cross-origin-resource-sharing"></a><span data-ttu-id="1b7d0-106">교차 원본 자원 공유</span><span class="sxs-lookup"><span data-stu-id="1b7d0-106">Cross-origin resource sharing</span></span>

<span data-ttu-id="1b7d0-107">[교차 원본 자원 공유(CORS)](https://www.w3.org/TR/cors/)를 사용해서 브라우저에서 교차 원본 SignalR 연결을 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-107">[Cross-origin resource sharing (CORS)](https://www.w3.org/TR/cors/) can be used to allow cross-origin SignalR connections in the browser.</span></span> <span data-ttu-id="1b7d0-108">JavaScript 코드가 SignalR 앱과 다른 도메인에서 호스팅 될 경우 JavaScript가 SignalR 앱에 연결할 수 있도록 반드시 [CORS 미들웨어](xref:security/cors)를 활성화시켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-108">If JavaScript code is hosted on a different domain from the SignalR app, [CORS middleware](xref:security/cors) must be enabled to allow the JavaScript to connect to the SignalR app.</span></span> <span data-ttu-id="1b7d0-109">신뢰하거나 제어할 수 있는 도메인의 교차 원본 요청만 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-109">Allow cross-origin requests only from domains you trust or control.</span></span> <span data-ttu-id="1b7d0-110">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="1b7d0-110">For example:</span></span>

* <span data-ttu-id="1b7d0-111">사이트에서 호스팅됩니다. `http://www.example.com`</span><span class="sxs-lookup"><span data-stu-id="1b7d0-111">Your site is hosted on `http://www.example.com`</span></span>
* <span data-ttu-id="1b7d0-112">SignalR 앱에서 호스팅됩니다. `http://signalr.example.com`</span><span class="sxs-lookup"><span data-stu-id="1b7d0-112">Your SignalR app is hosted on `http://signalr.example.com`</span></span>

<span data-ttu-id="1b7d0-113">SignalR 앱에서 `www.example.com` 원본만 허용하도록 CORS를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-113">CORS should be configured in the SignalR app to only allow the origin `www.example.com`.</span></span>

<span data-ttu-id="1b7d0-114">CORS를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [크로스-원본 요청 (CORS)](xref:security/cors)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-114">For more information on configuring CORS, see [Enable Cross-Origin Requests (CORS)](xref:security/cors).</span></span> <span data-ttu-id="1b7d0-115">SignalR **필요** 다음 CORS 정책:</span><span class="sxs-lookup"><span data-stu-id="1b7d0-115">SignalR **requires** the following CORS policies:</span></span>

* <span data-ttu-id="1b7d0-116">예상되는 특정 원본을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-116">Allow the specific expected origins.</span></span> <span data-ttu-id="1b7d0-117">모든 원본을 허용할 수는 있지만 안전하지 않거나 권장되지 **않습니다.**</span><span class="sxs-lookup"><span data-stu-id="1b7d0-117">Allowing any origin is possible but is **not** secure or recommended.</span></span>
* <span data-ttu-id="1b7d0-118">HTTP 메서드 `GET`과 `POST`를 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-118">HTTP methods `GET` and `POST` must be allowed.</span></span>
* <span data-ttu-id="1b7d0-119">인증이 사용되지 않는 경우에도 자격 증명이 활성화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-119">Credentials must be enabled, even when authentication is not used.</span></span>

<span data-ttu-id="1b7d0-120">예를 들어 다음 CORS 정책은 `http://example.com`에서 호스팅되는 SignalR 브라우저 클라이언트가 `http://signalr.example.com`에서 호스팅되는 SignalR 앱에 접근할 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-120">For example, the following CORS policy allows a SignalR browser client hosted on `http://example.com` to access the SignalR app hosted on `http://signalr.example.com`:</span></span>

[!code-csharp[Main](security/sample/Startup.cs?name=snippet1)]

> [!NOTE]
> <span data-ttu-id="1b7d0-121">SignalR은 Azure App Service가 기본 제공하는 CORS 기능과 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-121">SignalR is not compatible with the built-in CORS feature in Azure App Service.</span></span>

## <a name="websocket-origin-restriction"></a><span data-ttu-id="1b7d0-122">WebSocket 원본 제한</span><span class="sxs-lookup"><span data-stu-id="1b7d0-122">WebSocket Origin Restriction</span></span>

<span data-ttu-id="1b7d0-123">CORS가 제공하는 보호는 WebSocket에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-123">The protections provided by CORS don't apply to WebSockets.</span></span> <span data-ttu-id="1b7d0-124">브라우저는 다음을 수행하지 **않습니다.**</span><span class="sxs-lookup"><span data-stu-id="1b7d0-124">Browsers do **not**:</span></span>

* <span data-ttu-id="1b7d0-125">CORS 예비 요청을 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-125">Perform CORS pre-flight requests.</span></span>
* <span data-ttu-id="1b7d0-126">WebSocket 요청을 생성할 때 `Access-Control` 헤더에 지정된 제한 사항을 준수하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-126">Respect the restrictions specified in `Access-Control` headers when making WebSocket requests.</span></span>

<span data-ttu-id="1b7d0-127">그러나 브라우저는 WebSocket 요청을 만들때 `Origin` 헤더를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-127">However, browsers do send the `Origin` header when issuing WebSocket requests.</span></span> <span data-ttu-id="1b7d0-128">응용 프로그램은 예상된 원본으로부터 들어오는 WebSocket만 허용하도록 이런 헤더의 유효성을 검사하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-128">Applications should be configured to validate these headers to ensure that only WebSockets coming from the expected origins are allowed.</span></span>

<span data-ttu-id="1b7d0-129">ASP.NET Core 2.1 이상에서는 `Configure`에서 **`UseSignalR` 및 인증 미들웨어를 호출하기 전에** 사용자 지정 미들웨어를 배치해서 헤더 유효성 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-129">In ASP.NET Core 2.1 and later, header validation can be achieved using a custom middleware placed **before `UseSignalR`, and authentication middleware** in `Configure`:</span></span>

[!code-csharp[Main](security/sample/Startup.cs?name=snippet2)]

> [!NOTE]
> <span data-ttu-id="1b7d0-130">`Origin` 헤더는 클라이언트에 의해서 제어되며 `Referer` 헤더처럼 가짜일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-130">The `Origin` header is controlled by the client and, like the `Referer` header, can be faked.</span></span> <span data-ttu-id="1b7d0-131">이런 헤더들을 인증 메커니즘으로 사용하면 **안 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="1b7d0-131">These headers should **not** be used as an authentication mechanism.</span></span>

## <a name="access-token-logging"></a><span data-ttu-id="1b7d0-132">액세스 토큰 로깅</span><span class="sxs-lookup"><span data-stu-id="1b7d0-132">Access token logging</span></span>

<span data-ttu-id="1b7d0-133">WebSocket 또는 서버-전송 이벤트를 사용할 경우 브라우저 클라이언트는 쿼리 문자열을 통해서 액세스 토큰을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-133">When using WebSockets or Server-Sent Events, the browser client sends the access token in the query string.</span></span> <span data-ttu-id="1b7d0-134">쿼리 문자열을 통해서 액세스 토큰을 수신하는 방식은 일반적으로 표준 `Authorization` 헤더를 사용하는 방식만큼 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-134">Receiving the access token via query string is generally as secure as using the standard `Authorization` header.</span></span> <span data-ttu-id="1b7d0-135">그러나 많은 웹 서버가 쿼리 문자열을 포함한 각 요청의 URL을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-135">However, many web servers log the URL for each request, including the query string.</span></span> <span data-ttu-id="1b7d0-136">따라서 URL 로깅이 액세스 토큰까지 기록할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-136">Logging the URLs may log the access token.</span></span> <span data-ttu-id="1b7d0-137">가장 좋은 방법은 액세스 토큰을 기록하지 않도록 웹 서버의 로깅 설정을 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-137">A best practice is to set the web server's logging settings to prevent logging access tokens.</span></span>

## <a name="exceptions"></a><span data-ttu-id="1b7d0-138">예외</span><span class="sxs-lookup"><span data-stu-id="1b7d0-138">Exceptions</span></span>

<span data-ttu-id="1b7d0-139">일반적으로 예외 메시지는 민감한 데이터로 간주되어 클라이언트에게 노출되어서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-139">Exception messages are generally considered sensitive data that shouldn't be revealed to a client.</span></span> <span data-ttu-id="1b7d0-140">기본적으로 SignalR은 허브 메서드가 던진 예외의 세부 정보를 클라이언트로 전송하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-140">By default, SignalR doesn't send the details of an exception thrown by a hub method to the client.</span></span> <span data-ttu-id="1b7d0-141">대신 클라이언트는 오류가 발생했음을 나타내는 일반적인 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-141">Instead, the client receives a generic message indicating an error occurred.</span></span> <span data-ttu-id="1b7d0-142">클라이언트에 대한 예외 메시지 전달은 [`EnableDetailedErrors`](xref:signalr/configuration#configure-server-options)를 사용하여 재정의할 수 있습니다(예: 개발 또는 테스트 환경에서).</span><span class="sxs-lookup"><span data-stu-id="1b7d0-142">Exception message delivery to the client can be overridden (for example in development or test) with [`EnableDetailedErrors`](xref:signalr/configuration#configure-server-options).</span></span> <span data-ttu-id="1b7d0-143">운영 앱에서는 예외 메시지가 클라이언트에게 노출되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-143">Exception messages should not be exposed to the client in production apps.</span></span>

## <a name="buffer-management"></a><span data-ttu-id="1b7d0-144">버퍼 관리</span><span class="sxs-lookup"><span data-stu-id="1b7d0-144">Buffer management</span></span>

<span data-ttu-id="1b7d0-145">SignalR은 연결당 버퍼를 사용 하 여 들어오고 나가는 메시지를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-145">SignalR uses per-connection buffers to manage incoming and outgoing messages.</span></span> <span data-ttu-id="1b7d0-146">기본적으로 SignalR 32KB로 이러한 버퍼를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-146">By default, SignalR limits these buffers to 32 KB.</span></span> <span data-ttu-id="1b7d0-147">클라이언트 또는 서버 보낼 수 있는 가장 큰 메시지는 32KB입니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-147">The largest message a client or server can send is 32 KB.</span></span> <span data-ttu-id="1b7d0-148">메시지에 대 한 연결에서 사용 하는 최대 메모리는 32KB입니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-148">The maximum memory consumed by a connection for messages is 32 KB.</span></span> <span data-ttu-id="1b7d0-149">32KB 보다 작은 항상 메시지 경우 제한을 줄일 수 있습니다는.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-149">If your messages are always smaller than 32 KB, you can reduce the limit, which:</span></span>

* <span data-ttu-id="1b7d0-150">클라이언트가 더 큰 메시지를 전송하는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-150">Prevents a client from being able to send a larger message.</span></span>
* <span data-ttu-id="1b7d0-151">서버가 메시지를 받기 위해 큰 버퍼를 할당할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-151">The server will never need to allocate large buffers to accept messages.</span></span>

<span data-ttu-id="1b7d0-152">메시지가 32KB보다 크다면 제한을 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-152">If your messages are larger than 32 KB, you can increase the limit.</span></span> <span data-ttu-id="1b7d0-153">이 제한을 늘리는 것은 다음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-153">Increasing this limit means:</span></span>

* <span data-ttu-id="1b7d0-154">클라이언트는 서버가 큰 메모리 버퍼를 할당하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-154">The client can cause the server to allocate large memory buffers.</span></span>
* <span data-ttu-id="1b7d0-155">서버의 큰 버퍼 할당은 동시 연결 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-155">Server allocation of large buffers may reduce the number of concurrent connections.</span></span>

<span data-ttu-id="1b7d0-156">들어오는 메시지와 나가는 메시지에 대한 제한이 존재하며, 두 제한 모두 `MapHub`에 구성된 [`HttpConnectionDispatcherOptions`](xref:signalr/configuration#configure-server-options) 개체에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-156">There are limits for incoming and outgoing messages, both can be configured on the [`HttpConnectionDispatcherOptions`](xref:signalr/configuration#configure-server-options) object configured in `MapHub`:</span></span>

* <span data-ttu-id="1b7d0-157">`ApplicationMaxBufferSize`는 서버가 버퍼링하는 클라이언트의 최대 바이트 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-157">`ApplicationMaxBufferSize` represents the maximum number of bytes from the client that the server buffers.</span></span> <span data-ttu-id="1b7d0-158">클라이언트가 이 제한보다 큰 메시지를 전송하려고 시도하면 연결이 닫힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-158">If the client attempts to send a message larger than this limit, the connection may be closed.</span></span>
* <span data-ttu-id="1b7d0-159">`TransportMaxBufferSize`는 서버가 전송할 수 있는 최대 바이트 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-159">`TransportMaxBufferSize` represents the maximum number of bytes the server can send.</span></span> <span data-ttu-id="1b7d0-160">서버가 이 제한보다 큰 메시지(허브 메서드의 반환 값을 포함)를 전송하려고 시도하면 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-160">If the server attempts to send a message (including return values from hub methods) larger than this limit, an exception will be thrown.</span></span>

<span data-ttu-id="1b7d0-161">제한을 `0`으로 설정하면 제한이 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-161">Setting the limit to `0` disables the limit.</span></span> <span data-ttu-id="1b7d0-162">제한을 제거하면 클라이언트가 모든 크기의 메시지를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-162">Removing the limit allows a client to send a message of any size.</span></span> <span data-ttu-id="1b7d0-163">악의적인 클라이언트가 큰 메시지를 전송하여 과도한 메모리를 할당하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-163">Malicious clients sending large messages can cause excess memory to be allocated.</span></span> <span data-ttu-id="1b7d0-164">과도한 메모리의 사용은 동시 연결 수를 크게 감소시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b7d0-164">Excess memory usage can significantly reduce the number of concurrent connections.</span></span>
