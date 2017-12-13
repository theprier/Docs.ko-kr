---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
title: "SignalR 1.x 허브 API 가이드-JavaScript 클라이언트 | Microsoft Docs"
author: pfletcher
description: "이 문서에서는 허브 API를 사용 하 여 SignalR JavaScript 클라이언트 브라우저 및 Windows 스토어 (WinJS) applic 등의 버전 1.1에 대 한 소개를 제공..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/17/2013
ms.topic: article
ms.assetid: dcd4593b-1118-418a-af71-d12ff33fb36d
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 56931827a1a1edf003d2662b2d36964b9b6f3761
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="signalr-1x-hubs-api-guide---javascript-client"></a><span data-ttu-id="95c53-103">SignalR 1.x 허브 API 가이드-JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="95c53-103">SignalR 1.x Hubs API Guide - JavaScript Client</span></span>
====================
<span data-ttu-id="95c53-104">여 [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="95c53-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="95c53-105">이 문서에서는 허브 API를 사용 하 여 SignalR JavaScript 클라이언트 브라우저 및 Windows 스토어 (WinJS) 응용 프로그램 등의 버전 1.1에 대 한 소개를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-105">This document provides an introduction to using the Hubs API for SignalR version 1.1 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
> 
> <span data-ttu-id="95c53-106">SignalR 허브 API를 사용 하면 클라이언트가 서버와 연결 된 클라이언트에는 서버에서 원격 프로시저 호출 (Rpc)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="95c53-107">서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="95c53-108">클라이언트 코드에서 서버에서 호출 될 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="95c53-109">SignalR은 클라이언트와 서버 작업을 처리의 모든 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="95c53-110">또한 SignalR 영구 연결을 호출 하는 하위 수준 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="95c53-111">SignalR, 허브 및 영구 연결에 대 한 소개 또는 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서에 대 한 참조 [SignalR-시작](../getting-started/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>


## <a name="overview"></a><span data-ttu-id="95c53-112">개요</span><span class="sxs-lookup"><span data-stu-id="95c53-112">Overview</span></span>

<span data-ttu-id="95c53-113">이 문서는 다음 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="95c53-114">생성 된 프록시 및 수에 대 한 역</span><span class="sxs-lookup"><span data-stu-id="95c53-114">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="95c53-115">생성 된 프록시를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="95c53-115">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="95c53-116">클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="95c53-116">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="95c53-117">동적으로 생성 된 프록시를 참조 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-117">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="95c53-118">SignalR에 대 한 실제 파일을 만드는 방법에는 프록시 생성</span><span class="sxs-lookup"><span data-stu-id="95c53-118">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="95c53-119">연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-119">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="95c53-120">$. connection.hub 같습니다. 해당 $.hubConnection() 만듭니다 개체</span><span class="sxs-lookup"><span data-stu-id="95c53-120">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="95c53-121">Start 메서드의 비동기 실행</span><span class="sxs-lookup"><span data-stu-id="95c53-121">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="95c53-122">도메인 간 연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-122">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="95c53-123">연결을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-123">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="95c53-124">쿼리 문자열 매개 변수를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-124">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="95c53-125">전송 메서드를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-125">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="95c53-126">허브 클래스에 대 한 프록시를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-126">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="95c53-127">서버를 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-127">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="95c53-128">클라이언트에서 서버 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-128">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="95c53-129">연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-129">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="95c53-130">오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-130">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="95c53-131">클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-131">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="95c53-132">프로그래밍 하는 방법에 대 한 설명서는 서버 또는.NET 클라이언트는 다음 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-132">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="95c53-133">SignalR 허브 API 가이드-서버</span><span class="sxs-lookup"><span data-stu-id="95c53-133">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="95c53-134">SignalR 허브 API 가이드-.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="95c53-134">SignalR Hubs API Guide - .NET Client</span></span>](../guide-to-the-api/hubs-api-guide-net-client.md)

<span data-ttu-id="95c53-135">API 참조 항목의 링크를.NET 4.5 버전의 API 되도록합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-135">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="95c53-136">.NET 4를 사용 하 여 참조 [.NET 4 버전의 API 항목](https://msdn.microsoft.com/en-us/library/jj891075(v=vs.100).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-136">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/en-us/library/jj891075(v=vs.100).aspx).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="95c53-137">생성 된 프록시 및 수에 대 한 역</span><span class="sxs-lookup"><span data-stu-id="95c53-137">The generated proxy and what it does for you</span></span>

<span data-ttu-id="95c53-138">프록시를 위해 생성 한 SignalR 유무 SignalR 서비스와 통신 하는 JavaScript 클라이언트를 프로그래밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-138">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="95c53-139">연결, 서버를 호출 하는 쓰기 메서드를 사용 하 여 서버에서 메서드를 호출 하는 코드의 구문을 간소화은 프록시에서는을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-139">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="95c53-140">생성 된 프록시는 로컬 함수를 실행 중 이었던 것 처럼 보이는 구문을 사용할 수 있습니다를 사용 하면 서버 메서드를 호출 하는 코드를 작성할 때는: 작성할 수 있습니다 `serverMethod(arg1, arg2)` 대신 `invoke('serverMethod', arg1, arg2)`합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-140">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="95c53-141">생성 된 프록시 구문을 서버 메서드 이름을 잘못 입력 하면 즉각적이 고 읽을 클라이언트 쪽 오류가 또한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-141">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="95c53-142">및 프록시를 정의 하는 파일을 수동으로 만들면 가져올 수도 있습니다 IntelliSense 지원을 서버 메서드를 호출 하는 코드를 작성 하기 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-142">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="95c53-143">예를 들어 서버에서 다음 허브 클래스를 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-143">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="95c53-144">다음 코드 예제는 JavaScript 코드의 모양은 호출에 대 한 표시는 `NewContosoChatMessage` 서버 끝점 및 수신의 호출에서 메서드는 `addContosoChatMessageToPage` 서버에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="95c53-144">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="95c53-145">**생성 된 프록시 사용**</span><span class="sxs-lookup"><span data-stu-id="95c53-145">**With the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="95c53-146">**생성 된 프록시 없이**</span><span class="sxs-lookup"><span data-stu-id="95c53-146">**Without the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="95c53-147">생성 된 프록시를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="95c53-147">When to use the generated proxy</span></span>

<span data-ttu-id="95c53-148">서버를 호출 하는 클라이언트 메서드에 대 한 여러 이벤트 처리기를 등록 하려는 경우 생성 된 프록시를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-148">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="95c53-149">그렇지 않은 경우 생성 된 프록시를 사용 하도록 선택할 수 있습니다 또는 코딩 기본 설정을 기반으로 하지 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-149">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="95c53-150">사용 하지 않도록 선택 "signalr /" URL에서 참조할 필요가 없습니다는 `script` 클라이언트 코드에서 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-150">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="95c53-151">클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="95c53-151">Client setup</span></span>

<span data-ttu-id="95c53-152">JavaScript 클라이언트는 jQuery 및 SignalR core JavaScript 파일에 대 한 참조가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-152">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="95c53-153">JQuery 버전 1.6.4 또는 1.7.2, 1.8.2, 또는 1.9.1 같은 주요 이상 버전 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-153">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="95c53-154">생성 된 프록시를 사용 하려는 경우 생성 된 SignalR 프록시 JavaScript 파일에 대 한 참조를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-154">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="95c53-155">다음 예제에서는 생성 된 프록시를 사용 하는 HTML 페이지에 대 한 참조의 모양을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-155">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="95c53-156">이러한 참조를이 순서에 포함 되어야 합니다: jQuery 그 후 SignalR core 및 SignalR 프록시 이름, 성입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-156">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="95c53-157">동적으로 생성 된 프록시를 참조 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-157">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="95c53-158">앞의 예에서 생성 하는 SignalR 프록시에 대 한 참조 하지는 실제 파일에 JavaScript 코드를 동적으로 생성 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-158">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="95c53-159">SignalR은 JavaScript 코드를 만들고 신속 하 게 프록시에 대 한 "/ signalr/허브" URL에 대 한 응답에서 클라이언트로 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-159">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="95c53-160">서버에서 SignalR 연결에 대 한 다른 기본 URL을 지정 하는 경우 프로그램 `MapHubs` 메서드를 동적으로 생성 된 프록시 파일에 대 한 URL은와 사용자 지정 URL "/ 허브"를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-160">If you specified a different base URL for SignalR connections on the server in your `MapHubs` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="95c53-161">Windows 8 (Windows 스토어) JavaScript 클라이언트에 대 한 동적으로 생성 된 것 대신 실제 프록시 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-161">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="95c53-162">자세한 내용은 참조 [는 SignalR에 대 한 실제 파일을 만드는 방법에는 프록시 생성](#manualproxy) 이 항목의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-162">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>


<span data-ttu-id="95c53-163">ASP.NET MVC 4 Razor 뷰에서 프록시 파일 참조의 응용 프로그램 루트를 가리키는 물결표를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-163">In an ASP.NET MVC 4 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="95c53-164">MVC 4의 SignalR을 사용 하는 방법에 대 한 자세한 내용은 참조 [SignalR 및 MVC 4 시작](tutorial-getting-started-with-signalr-and-mvc-4.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-164">For more information about using SignalR in MVC 4, see [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="95c53-165">ASP.NET MVC 3 Razor 뷰에서 사용 하 여 `Url.Content` 프록시 파일 참조에 대 한:</span><span class="sxs-lookup"><span data-stu-id="95c53-165">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="95c53-166">ASP.NET Web Forms 응용 프로그램에서 사용 하 여 `ResolveClientUrl` 프록시 파일 참조가 또는 (물결표부터 시작) 응용 프로그램 루트 상대 경로 사용 하 여 ScriptManager을 통해 등록:</span><span class="sxs-lookup"><span data-stu-id="95c53-166">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="95c53-167">일반적으로 CSS 또는 JavaScript 파일에 대 한 사용 하는 "/ signalr/허브" URL을 지정 하는 데 동일한 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-167">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="95c53-168">물결표를 사용 하지 않고 URL을 지정 하는 경우 일부 시나리오에서는 응용 프로그램은 제대로 경우 작동 IIS Express를 사용 하 여 Visual Studio에서 테스트 되었지만 전체 IIS를 배포할 때 404 오류와 함께 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-168">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="95c53-169">자세한 내용은 참조 **루트 수준 리소스에 대 한 참조를 확인** 에 [ASP.NET 웹 프로젝트에 대 한 Visual Studio의 웹 서버](https://msdn.microsoft.com/en-us/library/58wxa9w5.aspx) MSDN 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-169">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/en-us/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="95c53-170">디버그 모드에서 Visual Studio 2012에서 웹 프로젝트를 실행 하 고 Internet Explorer를 사용 하 여 브라우저로 프록시 파일에서 확인할 수 있습니다 때 **솔루션 탐색기** 아래 **스크립트 문서**에 나타난 것 처럼는 다음 그림입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-170">When you run a web project in Visual Studio 2012 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Script Documents**, as shown in the following illustration.</span></span>

![솔루션 탐색기에서 JavaScript 생성 된 프록시 파일](signalr-1x-hubs-api-guide-javascript-client/_static/image1.png)

<span data-ttu-id="95c53-172">파일의 콘텐츠를 보려면 두 번 클릭 **허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-172">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="95c53-173">Visual Studio 2012 및 Internet Explorer를 사용 하지 않는 또는 디버그 모드에 거주 하지 않는 경우 "/ signalR/허브" URL로 이동 하 여 파일의 내용을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-173">If you are not using Visual Studio 2012 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="95c53-174">예를 들어, 사이트에서 실행 중인 경우 `http://localhost:56699`로 이동 `http://localhost:56699/SignalR/hubs` 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-174">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="95c53-175">SignalR에 대 한 실제 파일을 만드는 방법에는 프록시 생성</span><span class="sxs-lookup"><span data-stu-id="95c53-175">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="95c53-176">동적으로 생성 된 프록시 하는 대신, 프록시 코드를 있는 물리적 파일 만들고 해당 파일을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-176">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="95c53-177">캐싱 또는 동작을 번들로 대 한 제어에 대 한 그렇게 하려면 또는 서버 메서드 호출을 코딩 하는 경우 IntelliSense를 얻을 수를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-177">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="95c53-178">프록시 파일을 만들려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-178">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="95c53-179">설치는 [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-179">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="95c53-180">명령 프롬프트를 열고를 찾습니다는 *도구* SignalR.exe 파일이 있는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-180">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="95c53-181">다음 위치에서 도구 폴더는입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-181">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.1.0.1\tools`
3. <span data-ttu-id="95c53-182">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-182">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="95c53-183">에 대 한 경로 *.dll* 는 일반적으로 *bin* 프로젝트 폴더에 있는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-183">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="95c53-184">이 명령은 명명 된 파일을 만듭니다 *server.js* 와 같은 폴더에 *signalr.exe*합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-184">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="95c53-185">배치는 *server.js* 프로젝트에 적절 한 폴더에 파일, 응용 프로그램에 따라 이름 바꾸기 및 / "signalr" 참조 대신에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-185">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="95c53-186">연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-186">How to establish a connection</span></span>

<span data-ttu-id="95c53-187">연결을 설정할 수 있습니다, 전에 연결 개체를 만들 프록시를 만들고 서버에서 호출 될 수 있는 방법에 대 한 이벤트 처리기를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-187">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="95c53-188">프록시 및 이벤트 처리기를 설정 하면 연결을 호출 하 여 설정 된 `start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="95c53-188">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="95c53-189">생성 된 프록시를 사용 하는 경우에 생성된 된 프록시 코드에서는을 수행 하기 때문에 사용자 코드에서 연결 개체를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-189">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="95c53-190">**(생성 된 프록시)와 연결**</span><span class="sxs-lookup"><span data-stu-id="95c53-190">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="95c53-191">**(없이 생성 된 프록시) 연결 설정**</span><span class="sxs-lookup"><span data-stu-id="95c53-191">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="95c53-192">기본값을 사용 하 여 샘플 코드는 "/ signalr" SignalR 서비스에 연결 하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-192">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="95c53-193">다른 기본 URL을 지정 하는 방법에 대 한 정보를 참조 하십시오. [ASP.NET SignalR 허브 API 가이드-서버-/signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-193">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

> [!NOTE]
> <span data-ttu-id="95c53-194">호출 하기 전에 이벤트 처리기를 등록 하는 일반적으로 `start` 메서드 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-194">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="95c53-195">연결을 설정한 후 일부 이벤트 처리기를 등록 하려면, 할 수 있지만 호출 하기 전에 사용자 이벤트 처리기 중 하나 이상 등록 해야 하는 경우는 `start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="95c53-195">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="95c53-196">이 대 한 한 가지 이유는 응용 프로그램에서 하는 대부분의 허브 있을 수 있지만 트리거할 원하지는 `OnConnected` 둘 중 하나를 사용 하 여만 하려는 경우 모든 허브에 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-196">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="95c53-197">연결 되 면는 허브 프록시에 대 한 클라이언트 메서드를 어떤 지시 SignalR을 트리거하는 `OnConnected` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-197">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="95c53-198">호출 하기 전에 모든 이벤트 처리기를 등록 하지 않는 경우는 `start` 허브에 있지만 허브의 메서드를 호출할 수 있는 메서드를 `OnConnected` 메서드를 호출할 수 없습니다 및 서버에서 클라이언트 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-198">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>


<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="95c53-199">$. connection.hub 같습니다. 해당 $.hubConnection() 만듭니다 개체</span><span class="sxs-lookup"><span data-stu-id="95c53-199">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="95c53-200">생성 된 프록시를 사용 하는 경우의 예제에서 볼 수 있듯이 `$.connection.hub` 연결 개체를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-200">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="95c53-201">이 동일한 개체를 호출 하 여 얻을 수 있는 `$.hubConnection()` 생성 된 프록시를 사용 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="95c53-201">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="95c53-202">생성 된 프록시 코드는 다음 문을 실행 하 여 사용자에 대 한 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-202">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![생성 된 프록시 파일에 대 한 연결 만들기](signalr-1x-hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="95c53-204">생성 된 프록시를 사용 하는 작업을 수행할 수 있습니다 `$.connection.hub` 생성 된 프록시를 사용 하지 않을 때 연결 개체와 함께 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-204">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="95c53-205">Start 메서드의 비동기 실행</span><span class="sxs-lookup"><span data-stu-id="95c53-205">Asynchronous execution of the start method</span></span>

<span data-ttu-id="95c53-206">`start` 메서드가 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-206">The `start` method executes asynchronously.</span></span> <span data-ttu-id="95c53-207">반환 된 [jQuery 지연 된 개체](http://api.jquery.com/category/deferred-object/)와 같은 메서드를 호출 하 여 콜백 함수를 추가할 수 있다는 의미입니다 `pipe`, `done`, 및 `fail`합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-207">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="95c53-208">연결이 설정 된 후 실행할 코드가 있는 경우에 서버 메서드 호출과 같은 콜백 함수에 해당 코드를 입력 하거나 콜백 함수에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-208">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="95c53-209">`.done` 연결, 고 하는 모든 코드 후 후 콜백 메서드를 실행 하면 `OnConnected` 실행이 완료 되는 서버에서 이벤트 처리기 메서드.</span><span class="sxs-lookup"><span data-stu-id="95c53-209">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="95c53-210">뒤에 코드의 다음 줄으로 앞의 예제에서 "연결" 문을 배치 하는 경우는 `start` 메서드 호출 (에 없는 한 `.done` 콜백), `console.log` 다음에 표시 된 것 처럼 줄 연결을 설정 하기 전에 실행 됩니다 예:</span><span class="sxs-lookup"><span data-stu-id="95c53-210">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![연결이 설정 된 후 실행 되는 코드를 작성 하는 잘못 된 방법](signalr-1x-hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="95c53-212">도메인 간 연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-212">How to establish a cross-domain connection</span></span>

<span data-ttu-id="95c53-213">일반적으로 브라우저에서 페이지를 로드 하는 경우 `http://contoso.com`, SignalR 연결에 동일한 도메인에는 `http://contoso.com/signalr`합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-213">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="95c53-214">경우에서 페이지 `http://contoso.com` 에 대 한 연결을 사용 하면 `http://fabrikam.com/signalr`, 도메인 간 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-214">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="95c53-215">보안상의 이유로 도메인 간 연결이 기본적으로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-215">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="95c53-216">도메인 간 연결을 설정 하려면 서버에서 도메인 간 연결이 설정 되어 있는지 확인 하 고 연결 개체를 만들 때 연결 URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-216">To establish a cross-domain connection, make sure that cross-domain connections are enabled on the server, and specify the connection URL when you create the connection object.</span></span> <span data-ttu-id="95c53-217">SignalR과 같은 적합 한 기술을 도메인 간 연결에 사용 됩니다 [JSONP](http://en.wikipedia.org/wiki/JSONP) 또는 [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing)합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-217">SignalR will use the appropriate technology for cross-domain connections, such as [JSONP](http://en.wikipedia.org/wiki/JSONP) or [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span>

<span data-ttu-id="95c53-218">서버에서 호출 하는 경우 해당 옵션을 선택 하 여 도메인 간 연결을 설정는 `MapHubs` 메서드.</span><span class="sxs-lookup"><span data-stu-id="95c53-218">On the server, enable cross-domain connections by selecting that option when you call the `MapHubs` method.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample10.cs?highlight=2)]

<span data-ttu-id="95c53-219">클라이언트에서 생성 된 프록시) (없이 연결 개체를 만들 때나 (으로 생성 된 프록시) 시작 메서드를 호출 하기 전에 URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-219">On the client, specify the URL when you create the connection object (without the generated proxy) or before you call the start method (with the generated proxy).</span></span>

<span data-ttu-id="95c53-220">**도메인 간 연결 (생성 된 프록시)을 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-220">**Client code that specifies a cross-domain connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample11.js?highlight=1)]

<span data-ttu-id="95c53-221">**도메인 간 연결 (없이 생성 된 프록시)를 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-221">**Client code that specifies a cross-domain connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="95c53-222">사용 하는 경우는 `$.hubConnection` 포함 하지 않아도 생성자 `signalr` URL에 자동으로 추가 되기 때문에 (지정 하지 않으면 `useDefaultUrl` 으로 `false`).</span><span class="sxs-lookup"><span data-stu-id="95c53-222">When you use the `$.hubConnection` constructor, you don't have to include `signalr` in the URL because it is added automatically (unless you specify `useDefaultUrl` as `false`).</span></span>

<span data-ttu-id="95c53-223">서로 다른 끝점에 대 한 여러 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-223">You can create multiple connections to different endpoints.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample13.js)]

> [!NOTE] 
> 
> - <span data-ttu-id="95c53-224">설정 하지 않으면 `jQuery.support.cors` 코드에서 true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-224">Don't set `jQuery.support.cors` to true in your code.</span></span>
> 
>     ![JQuery.support.cors true로 설정 하지 마십시오](signalr-1x-hubs-api-guide-javascript-client/_static/image7.png)
> 
>     <span data-ttu-id="95c53-226">SignalR 처리 JSONP 또는 CORS를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-226">SignalR handles the use of JSONP or CORS.</span></span> <span data-ttu-id="95c53-227">설정 `jQuery.support.cors` true 브라우저에서 CORS를 가정 하는 SignalR 발생 하기 때문에 JSONP 사용 하지 않도록 설정 하려면.</span><span class="sxs-lookup"><span data-stu-id="95c53-227">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="95c53-228">Localhost URL에 연결할 때 Internet Explorer 10 않습니다 고려 도메인 간 연결을 응용 프로그램이 작동 하도록 로컬로 IE 10으로 서버에서 도메인 간 연결을 활성화 하지 않은 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-228">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="95c53-229">Internet Explorer 9와 함께 도메인 간 연결을 사용 하는 방법에 대 한 정보를 참조 하십시오. [이 StackOverflow 스레드](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-229">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="95c53-230">Chrome에서 도메인 간 연결을 사용 하는 방법에 대 한 정보를 참조 하십시오. [이 StackOverflow 스레드](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-230">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="95c53-231">기본값을 사용 하 여 샘플 코드는 "/ signalr" SignalR 서비스에 연결 하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-231">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="95c53-232">다른 기본 URL을 지정 하는 방법에 대 한 정보를 참조 하십시오. [ASP.NET SignalR 허브 API 가이드-서버-/signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-232">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>


<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="95c53-233">연결을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-233">How to configure the connection</span></span>

<span data-ttu-id="95c53-234">연결을 설정 하기 전에 쿼리 문자열 매개 변수를 지정 하거나 전송 방법을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-234">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="95c53-235">쿼리 문자열 매개 변수를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-235">How to specify query string parameters</span></span>

<span data-ttu-id="95c53-236">클라이언트가 연결할 때 서버에 데이터를 전송 하려는 경우에 연결 개체에 쿼리 문자열 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-236">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="95c53-237">다음 예제에서는 클라이언트 코드에서 쿼리 문자열 매개 변수를 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-237">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="95c53-238">**쿼리 문자열 값 (으로 생성 된 프록시) 시작 메서드를 호출 하기 전에 설정**</span><span class="sxs-lookup"><span data-stu-id="95c53-238">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample14.js?highlight=1)]

<span data-ttu-id="95c53-239">**(없이 생성 된 프록시) 시작 메서드를 호출 하기 전에 쿼리 문자열 값 설정**</span><span class="sxs-lookup"><span data-stu-id="95c53-239">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample15.js?highlight=2)]

<span data-ttu-id="95c53-240">다음 예제에는 서버 코드에서 쿼리 문자열 매개 변수를 읽는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-240">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample16.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="95c53-241">전송 메서드를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-241">How to specify the transport method</span></span>

<span data-ttu-id="95c53-242">연결 하는 과정의 일환으로, SignalR 클라이언트는 일반적으로 서버와 클라이언트 모두에서 지원 되는 가장 좋은 전송을 결정할 서버와 협상 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-242">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="95c53-243">어떤 전송을 사용 하려는 이미 알고 있는 경우 호출 하는 경우에 전송 메서드를 지정 하 여이 협상 프로세스를 무시할 수 있습니다는 `start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="95c53-243">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="95c53-244">**생성 된 프록시) (사용 하 여 전송 메서드를 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-244">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="95c53-245">**전송 메서드 (없이 생성 된 프록시)를 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-245">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="95c53-246">대신 바랍니다 SignalR 원하는 순서로 전송 메서드가 여러 개 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-246">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="95c53-247">**(생성 된 프록시)를 대체 사용자 지정 전송 체계를 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-247">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample19.js?highlight=1)]

<span data-ttu-id="95c53-248">**(없이 생성 된 프록시) 대체 사용자 지정 전송 체계를 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-248">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample20.js?highlight=2)]

<span data-ttu-id="95c53-249">전송 메서드를 지정 하기 위한 다음 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-249">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="95c53-250">"Websocket"</span><span class="sxs-lookup"><span data-stu-id="95c53-250">"webSockets"</span></span>
- <span data-ttu-id="95c53-251">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="95c53-251">"foreverFrame"</span></span>
- <span data-ttu-id="95c53-252">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="95c53-252">"serverSentEvents"</span></span>
- <span data-ttu-id="95c53-253">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="95c53-253">"longPolling"</span></span>

<span data-ttu-id="95c53-254">다음 예제는 연결에서 사용 되 고 전송 방법을 확인 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-254">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="95c53-255">**(생성 된 프록시)와 연결을 사용 하는 전송 방법 표시 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-255">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample21.js?highlight=2)]

<span data-ttu-id="95c53-256">**(없이 생성 된 프록시) 연결에서 사용 되는 전송 메서드를 표시 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-256">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample22.js?highlight=3)]

<span data-ttu-id="95c53-257">서버 코드에서 전송 방법을 확인 하는 방법에 대 한 정보를 참조 하십시오. [ASP.NET SignalR 허브 API 가이드-서버-컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-257">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="95c53-258">전송 및 대체 하는 방법에 대 한 자세한 내용은 참조 [SignalR-전송 및 대체 소개](../getting-started/introduction-to-signalr.md#transports)합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-258">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="95c53-259">허브 클래스에 대 한 프록시를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-259">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="95c53-260">만드는 각 연결 개체는 하나 이상의 허브 클래스를 포함 하는 SignalR 서비스에 연결 하는 방법에 대 한 정보를 캡슐화 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-260">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="95c53-261">을 허브 클래스와 통신 하도록 하 여 만든 사용자가 직접 (생성 된 프록시를 사용 하지 않는) 하는 경우 또는 사용자에 대해 생성 되는 프록시 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-261">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="95c53-262">클라이언트에서 프록시 이름을 카멜식 대/소문자의 버전이 허브 클래스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-262">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="95c53-263">SignalR 자동으로 이러한 변경 때문 JavaScript 코드는 JavaScript 규칙을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-263">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="95c53-264">**서버 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="95c53-264">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="95c53-265">**허브에 대 한 생성 된 클라이언트 프록시에 대 한 참조를 가져오려면**</span><span class="sxs-lookup"><span data-stu-id="95c53-265">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample24.js?highlight=1)]

<span data-ttu-id="95c53-266">**(없이 생성 된 프록시) 허브 클래스에 대 한 클라이언트 프록시 만들기**</span><span class="sxs-lookup"><span data-stu-id="95c53-266">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="95c53-267">하면 허브 클래스를 추가 하는 경우는 `HubName` 특성을 대/소문자를 변경 하지 않고 정확한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-267">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="95c53-268">**HubName 특성을 가진 서버 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="95c53-268">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="95c53-269">**허브에 대 한 생성 된 클라이언트 프록시에 대 한 참조를 가져오려면**</span><span class="sxs-lookup"><span data-stu-id="95c53-269">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample27.js?highlight=1)]

<span data-ttu-id="95c53-270">**(없이 생성 된 프록시) 허브 클래스에 대 한 클라이언트 프록시 만들기**</span><span class="sxs-lookup"><span data-stu-id="95c53-270">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample28.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="95c53-271">서버를 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-271">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="95c53-272">허브에서 서버를 호출할 수 있는 메서드를 정의 하려면 이벤트 처리기 허브 프록시를 사용 하 여 추가 `client` 생성 된 프록시 또는 호출의 속성은 `on` 메서드는 생성 된 프록시를 사용 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="95c53-272">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="95c53-273">매개 변수는 복잡 한 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-273">The parameters can be complex objects.</span></span>

<span data-ttu-id="95c53-274">이벤트 처리기를 호출 하기 전에 추가 `start` 메서드 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-274">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="95c53-275">(호출한 후 이벤트 처리기를 추가 하려는 경우는 `start` 메서드를에 나와 있는 참고를 참조 하십시오. [연결을 설정 하는 방법](#establishconnection) 앞부분에 나오는이 문서화 하 고 생성 된 프록시를 사용 하지 않고 메서드를 정의 하는 것에 대 한 표시 된 구문을 사용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="95c53-275">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="95c53-276">메서드 이름 일치는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-276">Method name matching is case-insensitive.</span></span> <span data-ttu-id="95c53-277">예를 들어 `Clients.All.addContosoChatMessageToPage` 서버에서 실행 됩니다 `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, 또는 `addcontosochatmessagetopage` 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="95c53-277">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="95c53-278">**(사용 하 여 생성 된 프록시) 클라이언트에서 메서드를 정의 합니다.**</span><span class="sxs-lookup"><span data-stu-id="95c53-278">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample29.js?highlight=2)]

<span data-ttu-id="95c53-279">**(사용 하 여 생성 된 프록시) 클라이언트에서 메서드를 정의 하는 다른 방법**</span><span class="sxs-lookup"><span data-stu-id="95c53-279">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample30.js?highlight=1-2)]

<span data-ttu-id="95c53-280">**생성 된 프록시 없이 이동해 왔거나 start 메서드를 호출한 후 추가 하는 경우 클라이언트에서 메서드를 정의 합니다.**</span><span class="sxs-lookup"><span data-stu-id="95c53-280">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample31.js?highlight=3)]

<span data-ttu-id="95c53-281">**클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-281">**Server code that calls the client method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample32.cs?highlight=5)]

<span data-ttu-id="95c53-282">다음 예제에서는 메서드 매개 변수로 복잡 한 개체를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-282">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="95c53-283">**생성 된 프록시) (포함 하는 복잡 한 개체를 사용 하는 클라이언트에서 메서드를 정의 합니다.**</span><span class="sxs-lookup"><span data-stu-id="95c53-283">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample33.js?highlight=2-3)]

<span data-ttu-id="95c53-284">**(없이 생성 된 프록시)는 복잡 한 개체를 사용 하는 클라이언트에서 메서드를 정의 합니다.**</span><span class="sxs-lookup"><span data-stu-id="95c53-284">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample34.js?highlight=3-4)]

<span data-ttu-id="95c53-285">**복잡 한 개체를 정의 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-285">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="95c53-286">**복잡 한 개체를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-286">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample36.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="95c53-287">클라이언트에서 서버 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-287">How to call server methods from the client</span></span>

<span data-ttu-id="95c53-288">메서드를 호출 하는 서버는 클라이언트에서를 사용 하 여는 `server` 생성 된 프록시의 속성 또는 `invoke` Hub 프록시 생성 된 프록시를 사용 하지 않는 경우에 메서드.</span><span class="sxs-lookup"><span data-stu-id="95c53-288">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="95c53-289">반환 값 또는 매개 변수는 복잡 한 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-289">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="95c53-290">허브에서 메서드 이름의 카멜식 대 / 소문자 버전에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-290">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="95c53-291">SignalR 자동으로 이러한 변경 때문 JavaScript 코드는 JavaScript 규칙을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-291">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="95c53-292">다음 예제에서는 반환 값에는 서버 메서드를 호출 하는 방법 및 반환 값이 없는 서버 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-292">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="95c53-293">**서버 HubMethodName 특성이 없는 메서드**</span><span class="sxs-lookup"><span data-stu-id="95c53-293">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample37.cs?highlight=3)]

<span data-ttu-id="95c53-294">**매개 변수에 전달 하는 복잡 한 개체를 정의 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-294">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample38.cs)]

<span data-ttu-id="95c53-295">**생성 된 프록시) (사용 하 여 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-295">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample39.js?highlight=1)]

<span data-ttu-id="95c53-296">**생성 된 프록시) (없이 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-296">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="95c53-297">허브 메서드를 데코 레이트 된 경우는 `HubMethodName` 특성을 대/소문자를 변경 하지 않고이 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-297">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="95c53-298">**서버 메서드에서** HubMethodName 특성</span><span class="sxs-lookup"><span data-stu-id="95c53-298">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample41.cs?highlight=3)]

<span data-ttu-id="95c53-299">**생성 된 프록시) (사용 하 여 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-299">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample42.js?highlight=1)]

<span data-ttu-id="95c53-300">**생성 된 프록시) (없이 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-300">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample43.js?highlight=1)]

<span data-ttu-id="95c53-301">앞의 예제에서는 반환 값이 없는 서버 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-301">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="95c53-302">다음 예제에서는 반환 값이 있는 서버 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-302">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="95c53-303">**반환 값을 포함 하는 방법에 대 한 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-303">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample44.cs?highlight=3)]

<span data-ttu-id="95c53-304">**에 사용 되는 Stock 클래스는** 반환 값</span><span class="sxs-lookup"><span data-stu-id="95c53-304">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample45.cs?highlight=1)]

<span data-ttu-id="95c53-305">**생성 된 프록시) (사용 하 여 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-305">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample46.js?highlight=2,4-5)]

<span data-ttu-id="95c53-306">**생성 된 프록시) (없이 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="95c53-306">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample47.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="95c53-307">연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-307">How to handle connection lifetime events</span></span>

<span data-ttu-id="95c53-308">SignalR 다음 연결을 처리할 수 있는 수명 이벤트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-308">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="95c53-309">`starting`: 연결을 통해 모든 데이터를 보내기 전에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-309">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="95c53-310">`received`: 연결에서 모든 데이터를 수신할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-310">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="95c53-311">수신된 된 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-311">Provides the received data.</span></span>
- <span data-ttu-id="95c53-312">`connectionSlow`: 클라이언트 느리거나 자주 삭제 연결을 검색 하는 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-312">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="95c53-313">`reconnecting`: 기본 전송 다시 시작 될 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-313">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="95c53-314">`reconnected`: 기본 전송에 다시 연결 되 면 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-314">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="95c53-315">`stateChanged`: 연결 상태가 변경 될 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-315">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="95c53-316">이전 상태와 (연결, 연결 됨, 다시 연결, 또는 연결 끊김) 새 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-316">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="95c53-317">`disconnected`: 연결을 끊을 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-317">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="95c53-318">예를 들어, 상당한 지연을 발생 시킬 수 있는 연결 문제가 있을 때 경고 메시지를 표시 하려는 경우 처리는 `connectionSlow` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-318">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="95c53-319">**생성 된 프록시) (포함 connectionSlow 이벤트를 처리 합니다.**</span><span class="sxs-lookup"><span data-stu-id="95c53-319">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample48.js?highlight=1)]

<span data-ttu-id="95c53-320">**생성 된 프록시) (없이 connectionSlow 이벤트 처리**</span><span class="sxs-lookup"><span data-stu-id="95c53-320">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample49.js?highlight=2)]

<span data-ttu-id="95c53-321">자세한 내용은 참조 [이해 하 고 SignalR에서 연결 수명 이벤트를 처리](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-321">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="95c53-322">오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-322">How to handle errors</span></span>

<span data-ttu-id="95c53-323">SignalR JavaScript 클라이언트는 제공 된 `error` 에 대 한 처리기를 추가할 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-323">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="95c53-324">또한 서버 메서드 호출에서 발생 하는 오류에 대 한 처리기를 추가 하려면 fail 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-324">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="95c53-325">서버에 대 한 자세한 오류 메시지를 명시적으로 활성화 하지 않는 경우 오류가 발생 한 후 SignalR 반환 하는 예외 개체는 오류에 대 한 최소한의 정보만을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-325">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="95c53-326">예를 들어, 호출 하는 경우 `newContosoChatMessage` 실패, 오류 개체에서 오류 메시지에 "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" 보내는 프로덕션의 클라이언트에 자세한 오류 메시지에 대 한 자세한 오류 메시지를 사용 하도록 설정 하려면 보안상의 이유로 적합 하지 않습니다 문제 해결을 위해 서버에서 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-326">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample50.cs?highlight=2)]

<span data-ttu-id="95c53-327">다음 예제에서는 오류 이벤트에 대 한 처리기를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-327">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="95c53-328">**오류 처리기 (생성 된 프록시)에 추가**</span><span class="sxs-lookup"><span data-stu-id="95c53-328">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample51.js?highlight=1)]

<span data-ttu-id="95c53-329">**오류 처리기 (없이 생성 된 프록시)를 추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="95c53-329">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="95c53-330">다음 예제에서는 메서드 호출에서 오류를 처리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-330">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="95c53-331">**생성 된 프록시) (포함 된 메서드 호출에서 오류를 처리 합니다**</span><span class="sxs-lookup"><span data-stu-id="95c53-331">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample53.js?highlight=2)]

<span data-ttu-id="95c53-332">**(없이 생성 된 프록시) 메서드 호출에서 오류를 처리 합니다**</span><span class="sxs-lookup"><span data-stu-id="95c53-332">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="95c53-333">메서드 호출에 실패 하면는 `error` 이벤트도 발생 하므로 코드에는 `error` 메서드 처리기 및는 `.fail` 콜백 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-333">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="95c53-334">클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="95c53-334">How to enable client-side logging</span></span>

<span data-ttu-id="95c53-335">클라이언트 쪽 로깅에 대 한 연결을 사용 하려면 설정는 `logging` 호출 하기 전에 연결 개체에 `start` 연결을 설정 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="95c53-335">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="95c53-336">**(생성 된 프록시)에 대 한 로깅을 사용 하도록 설정**</span><span class="sxs-lookup"><span data-stu-id="95c53-336">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample55.js?highlight=1)]

<span data-ttu-id="95c53-337">**(없이 생성 된 프록시) 로깅을 사용 하도록 설정**</span><span class="sxs-lookup"><span data-stu-id="95c53-337">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample56.js?highlight=2)]

<span data-ttu-id="95c53-338">로그를 확인 하려면 브라우저의 개발자 도구를 열고 콘솔 탭으로 이동 합니다. 이 작업을 수행 하는 방법을 보여 주는 샷 단계별 지침 및 화면을 보여 주는 자습서를 참조 하십시오. [서버 로깅 사용-ASP.NET Signalr과 브로드캐스트](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95c53-338">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](index.md).</span></span>
