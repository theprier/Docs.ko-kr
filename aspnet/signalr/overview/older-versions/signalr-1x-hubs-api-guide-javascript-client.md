---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
title: SignalR 1.x 허브 API 가이드-JavaScript 클라이언트 | Microsoft Docs
author: pfletcher
description: 이 문서에서는 허브 API를 사용 하 여 SignalR 브라우저 등 Windows 스토어 (WinJS) 합 JavaScript 클라이언트의 버전 1.1에 대 한 소개를 제공 하는 중...
ms.author: riande
ms.date: 04/17/2013
ms.assetid: dcd4593b-1118-418a-af71-d12ff33fb36d
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 993ad7924d8335f79aa2c3e41c00ddfa8bc26874
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836388"
---
<a name="signalr-1x-hubs-api-guide---javascript-client"></a><span data-ttu-id="4b680-103">SignalR 1.x 허브 API 가이드-JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="4b680-103">SignalR 1.x Hubs API Guide - JavaScript Client</span></span>
====================
<span data-ttu-id="4b680-104">하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="4b680-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="4b680-105">이 문서에서는 허브 API를 사용 하 여 SignalR 브라우저 (WinJS) Windows 스토어 응용 프로그램 등의 JavaScript 클라이언트의 버전 1.1에 대 한 소개를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-105">This document provides an introduction to using the Hubs API for SignalR version 1.1 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
> 
> <span data-ttu-id="4b680-106">SignalR 허브 API를 사용 하면 클라이언트가 서버에 연결 된 클라이언트에는 서버에서 원격 프로시저 호출 (Rpc)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="4b680-107">서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="4b680-108">클라이언트 코드에서 서버에서 호출할 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="4b680-109">SignalR은 모든 클라이언트-서버 연결 구조를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="4b680-110">또한 SignalR 영구 연결을 호출 하는 하위 수준 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="4b680-111">SignalR에서 허브 및 영구 연결에 대 한 소개, 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서에 대 한 참조 [SignalR-Getting Started](../getting-started/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>


## <a name="overview"></a><span data-ttu-id="4b680-112">개요</span><span class="sxs-lookup"><span data-stu-id="4b680-112">Overview</span></span>

<span data-ttu-id="4b680-113">이 문서는 다음 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="4b680-114">생성 된 프록시 및를 수행 하는 작업</span><span class="sxs-lookup"><span data-stu-id="4b680-114">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="4b680-115">생성 된 프록시를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="4b680-115">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="4b680-116">클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="4b680-116">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="4b680-117">동적으로 생성 된 프록시를 참조 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-117">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="4b680-118">SignalR에 대 한 실제 파일을 만드는 방법에는 프록시 생성</span><span class="sxs-lookup"><span data-stu-id="4b680-118">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="4b680-119">연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-119">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="4b680-120">$. connection.hub 동일 해당 $.hubConnection() 만듭니다 개체</span><span class="sxs-lookup"><span data-stu-id="4b680-120">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="4b680-121">비동기 시작 메서드 실행</span><span class="sxs-lookup"><span data-stu-id="4b680-121">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="4b680-122">도메인 간 연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-122">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="4b680-123">연결을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-123">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="4b680-124">쿼리 문자열 매개 변수를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-124">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="4b680-125">전송 메서드를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-125">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="4b680-126">허브 클래스에 대 한 프록시를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-126">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="4b680-127">서버를 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-127">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="4b680-128">클라이언트에서 서버 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-128">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="4b680-129">연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-129">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="4b680-130">오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-130">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="4b680-131">클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-131">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="4b680-132">프로그래밍 하는 방법에 대 한 설명서에 대 한 서버 또는.NET 클라이언트는 다음 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-132">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="4b680-133">SignalR 허브 API 가이드-서버</span><span class="sxs-lookup"><span data-stu-id="4b680-133">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="4b680-134">SignalR 허브 API 가이드-.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="4b680-134">SignalR Hubs API Guide - .NET Client</span></span>](../guide-to-the-api/hubs-api-guide-net-client.md)

<span data-ttu-id="4b680-135">.NET 4.5 버전의 API는 API 참조 항목에 대 한 링크.</span><span class="sxs-lookup"><span data-stu-id="4b680-135">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="4b680-136">.NET 4를 사용 하는 경우 참조 [항목에서는 API의.NET 4 버전](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-136">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="4b680-137">생성 된 프록시 및를 수행 하는 작업</span><span class="sxs-lookup"><span data-stu-id="4b680-137">The generated proxy and what it does for you</span></span>

<span data-ttu-id="4b680-138">SignalR를 생성 하는 프록시 없이 SignalR service와 통신 하는 JavaScript 클라이언트를 프로그래밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-138">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="4b680-139">용도 프록시에 연결 하 고 서버를 호출 하는 쓰기 메서드를 사용 하 여 서버에서 메서드를 호출 하는 코드의 구문을 간소화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-139">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="4b680-140">생성된 된 프록시의 로컬 함수를 실행 중 이었던 것 처럼 보이는 구문을 사용할 수 있도록 하는 서버 메서드를 호출 하는 코드를 작성 하는 경우: 작성할 수 있습니다 `serverMethod(arg1, arg2)` 대신 `invoke('serverMethod', arg1, arg2)`합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-140">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="4b680-141">생성 된 프록시 구문을 서버 메서드 이름을 잘못 입력 하면 즉각적이 고 알아보기 쉬운 클라이언트 쪽 오류가 또한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-141">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="4b680-142">및 서버 메서드를 호출 하는 코드를 작성 하기 위한 IntelliSense 지원의 가져올 수도 있습니다 프록시를 정의 하는 파일을 수동으로 만들어야 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="4b680-142">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="4b680-143">예를 들어 서버에서 다음 허브 클래스를 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-143">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="4b680-144">다음 코드 예제에서는 JavaScript 코드의 모양은 호출을 표시 합니다 `NewContosoChatMessage` 메서드 호출을 받는 서버에는 `addContosoChatMessageToPage` 서버에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="4b680-144">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="4b680-145">**생성 된 프록시를 사용 하 여**</span><span class="sxs-lookup"><span data-stu-id="4b680-145">**With the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="4b680-146">**생성 된 프록시 없이**</span><span class="sxs-lookup"><span data-stu-id="4b680-146">**Without the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="4b680-147">생성 된 프록시를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="4b680-147">When to use the generated proxy</span></span>

<span data-ttu-id="4b680-148">서버를 호출 하는 클라이언트 메서드에 대 한 여러 이벤트 처리기를 등록 하려는 경우 생성 된 프록시를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-148">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="4b680-149">그렇지 않은 경우 생성 된 프록시를 사용 하도록 선택할 수 또는 코딩 기본 설정을 기반으로 하지.</span><span class="sxs-lookup"><span data-stu-id="4b680-149">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="4b680-150">사용 하지 않으려는 경우 "signalr /" URL에서 참조할 필요가 없습니다를 `script` 클라이언트 코드에서 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-150">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="4b680-151">클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="4b680-151">Client setup</span></span>

<span data-ttu-id="4b680-152">JavaScript 클라이언트에 jQuery 및 SignalR core JavaScript 파일에 대 한 참조가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-152">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="4b680-153">JQuery 버전 1.6.4 또는 1.7.2, 1.8.2, 1.9.1 등 주요 이상 버전 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-153">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="4b680-154">생성 된 프록시를 사용 하려는 경우에 SignalR 생성 된 프록시 JavaScript 파일에 대 한 참조가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-154">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="4b680-155">다음 예제에서는 생성 된 프록시를 사용 하는 HTML 페이지에 표시 될 수 있습니다 참조를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-155">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="4b680-156">이러한 참조를이 순서 대로 포함 되어야 합니다: jQuery, 그 후 SignalR core 및 SignalR 프록시 성입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-156">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="4b680-157">동적으로 생성 된 프록시를 참조 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-157">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="4b680-158">앞의 예제에서는 SignalR 생성 된 프록시에 대 한 참조를 동적으로 생성 된 JavaScript 코드를 실제 파일에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-158">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="4b680-159">SignalR 즉석에서 프록시에 대 한 JavaScript 코드를 만들고 "/ signalr 허브" URL에 대 한 응답에서 클라이언트로 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-159">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="4b680-160">서버에서 SignalR 연결에 대 한 다양 한 기본 URL을 지정한 경우에 `MapHubs` 메서드를 동적으로 생성 된 프록시 파일의 URL을 사용 하 여 사용자 지정 URL은 "/ hubs"를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-160">If you specified a different base URL for SignalR connections on the server in your `MapHubs` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="4b680-161">Windows 8 (Windows 스토어) JavaScript 클라이언트에 대 한 동적으로 생성 된 것 대신 실제 프록시 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-161">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="4b680-162">자세한 내용은 [SignalR에 대 한 실제 파일을 만드는 방법에는 프록시 생성](#manualproxy) 이 항목의에서 뒷부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-162">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>


<span data-ttu-id="4b680-163">ASP.NET MVC 4 Razor 보기에서를 가리키는 데 프록시 파일 참조의 응용 프로그램 루트를 물결표를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-163">In an ASP.NET MVC 4 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="4b680-164">MVC 4에서 SignalR을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [SignalR 및 MVC 4 시작](tutorial-getting-started-with-signalr-and-mvc-4.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-164">For more information about using SignalR in MVC 4, see [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="4b680-165">ASP.NET MVC 3 Razor 보기에서 사용 하 여 `Url.Content` 프록시 파일 참조용:</span><span class="sxs-lookup"><span data-stu-id="4b680-165">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="4b680-166">ASP.NET Web Forms 응용 프로그램에서 사용 하 여 `ResolveClientUrl` 프록시 참조를 파일 또는 앱 루트 상대 경로 (물결표부터 시작)를 사용 하는 ScriptManager를 통해 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-166">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="4b680-167">일반적으로 CSS 또는 JavaScript 파일에 사용 하는 "/ signalr 허브" URL을 지정 하는 데 동일한 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-167">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="4b680-168">물결표를 사용 하지 않고 URL을 지정 하는 경우 일부 시나리오에서는 응용 프로그램은 제대로 작동 IIS Express를 사용 하 여 Visual Studio에서 테스트 해도 전체 IIS를 배포할 때 404 오류와 함께 실패 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="4b680-168">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="4b680-169">자세한 내용은 **루트 수준 리소스에 대 한 참조 해결** 에서 [ASP.NET 웹 프로젝트에 대 한 Visual Studio에서 웹 서버](https://msdn.microsoft.com/library/58wxa9w5.aspx) MSDN 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-169">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="4b680-170">디버그 모드에서 Visual Studio 2012에서 웹 프로젝트를 실행 하 고 브라우저를 Internet Explorer를 사용 하는 경우에 프록시 파일을 볼 수 있습니다 **솔루션 탐색기** 아래에서 **스크립트 문서**에서처럼 합니다 다음 그림에서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-170">When you run a web project in Visual Studio 2012 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Script Documents**, as shown in the following illustration.</span></span>

![솔루션 탐색기에서 JavaScript 생성 된 프록시 파일](signalr-1x-hubs-api-guide-javascript-client/_static/image1.png)

<span data-ttu-id="4b680-172">파일의 내용을 보려면, 두 번 클릭 **hubs**합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-172">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="4b680-173">Visual Studio 2012 및 Internet Explorer를 사용 하지 않는 경우, 디버그 모드에서 없는 경우에 "/ signalR 허브" URL로 이동 하 여 파일의 콘텐츠를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-173">If you are not using Visual Studio 2012 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="4b680-174">예를 들어 사이트에서 실행 중인 `http://localhost:56699`으로 이동 하 여 `http://localhost:56699/SignalR/hubs` 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-174">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="4b680-175">SignalR에 대 한 실제 파일을 만드는 방법에는 프록시 생성</span><span class="sxs-lookup"><span data-stu-id="4b680-175">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="4b680-176">동적으로 생성 된 프록시 또는 프록시 코드가 있는 물리적 파일을 만들 수 있으며 해당 파일을 참조할 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-176">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="4b680-177">에 대 한 캐싱 나 동작을 제어 하는 작업을 수행 하 또는 server 메서드 호출을 코딩 하는 경우 IntelliSense를 가져올 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-177">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="4b680-178">프록시 파일을 만들려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-178">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="4b680-179">설치 합니다 [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="4b680-179">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="4b680-180">명령 프롬프트를 열고 이동 합니다 *도구* SignalR.exe 파일이 있는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-180">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="4b680-181">다음 위치에서 도구 폴더는입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-181">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.1.0.1\tools`
3. <span data-ttu-id="4b680-182">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-182">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="4b680-183">에 대 한 경로 *.dll* 일반적으로 *bin* 프로젝트 폴더의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-183">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="4b680-184">이 명령은 라는 파일을 만듭니다 *server.js* 와 같은 폴더에 *signalr.exe*합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-184">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="4b680-185">배치 된 *server.js* 프로젝트에 적절 한 폴더에 파일, 응용 프로그램에 대해 적절 하 게 바꾸거나 및 "signalr /" 참조를 대신 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-185">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="4b680-186">연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-186">How to establish a connection</span></span>

<span data-ttu-id="4b680-187">연결을 설정 하기 전에 연결 개체를 만들고 프록시를 만들려면 서버에서 호출할 수 있는 방법에 대 한 이벤트 처리기를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-187">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="4b680-188">프록시 및 이벤트 처리기를 설정 하는 경우 호출 하 여 연결을 설정 합니다 `start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="4b680-188">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="4b680-189">생성 된 프록시를 사용 하는 경우에 생성된 된 프록시 코드를 수행 하기 때문에 사용자 고유의 코드에서 연결 개체를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-189">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="4b680-190">**연결 된 (생성된 된 프록시)**</span><span class="sxs-lookup"><span data-stu-id="4b680-190">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="4b680-191">**생성된 된 프록시) (없음 연결**</span><span class="sxs-lookup"><span data-stu-id="4b680-191">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="4b680-192">기본값을 사용 하 여 샘플 코드는 "/ signalr" SignalR 서비스에 연결 하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-192">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="4b680-193">다른 기본 URL을 지정 하는 방법에 대 한 정보를 참조 하세요 [ASP.NET SignalR 허브 API 가이드-서버-/signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-193">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

> [!NOTE]
> <span data-ttu-id="4b680-194">호출 하기 전에 이벤트 처리기를 등록 하는 일반적으로 `start` 연결을 설정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-194">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="4b680-195">연결을 설정한 후 몇 가지 이벤트 처리기를 등록 하려면를 수행할 수 있지만 호출 하기 전에 이벤트 처리기 중 하나 이상 등록 해야 하는 경우는 `start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="4b680-195">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="4b680-196">그 이유 중 하나는 응용 프로그램에서 하는 많은 허브 있을 수 있지만 트리거 하려고 하는 `OnConnected` 그 중 하나를 사용 하 여만 하려는 경우 모든 허브에 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-196">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="4b680-197">연결이 설정 되 면 클라이언트에 대 한 메서드는 허브 프록시는 어떤 지시를 트리거하는 SignalR을 `OnConnected` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-197">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="4b680-198">호출 하기 전에 이벤트 처리기를 등록 하지 않으면 합니다 `start` 허브에 있지만 허브의 메서드를 호출할 수 있는 메서드를 `OnConnected` 메서드를 호출할 수 없습니다 하 고 서버에서 클라이언트 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-198">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>


<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="4b680-199">$. connection.hub 동일 해당 $.hubConnection() 만듭니다 개체</span><span class="sxs-lookup"><span data-stu-id="4b680-199">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="4b680-200">알 수 있듯이 예제에서는에서 생성 된 프록시를 사용 하는 경우 `$.connection.hub` 연결 개체를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-200">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="4b680-201">이 동일한 개체를 호출 하 여 가져올 `$.hubConnection()` 생성 된 프록시를 사용 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="4b680-201">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="4b680-202">생성된 된 프록시 코드는 다음 문을 실행 하 여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-202">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![생성된 된 프록시 파일에서 연결 만들기](signalr-1x-hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="4b680-204">생성 된 프록시를 사용 하는 작업을 수행할 수 있습니다 `$.connection.hub` 생성 된 프록시를 사용 하지 않는 경우 연결 개체를 사용 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-204">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="4b680-205">비동기 시작 메서드 실행</span><span class="sxs-lookup"><span data-stu-id="4b680-205">Asynchronous execution of the start method</span></span>

<span data-ttu-id="4b680-206">`start` 메서드를 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-206">The `start` method executes asynchronously.</span></span> <span data-ttu-id="4b680-207">반환을 [jQuery 지연 된 개체](http://api.jquery.com/category/deferred-object/), 즉, 같은 메서드를 호출 하 여 콜백 함수를 추가할 수 있습니다 `pipe`를 `done`, 및 `fail`합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-207">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="4b680-208">연결이 설정 된 후에 실행 하려는 코드가 있는 경우에 서버 메서드 호출을 같은 콜백 함수에 해당 코드를 입력 하거나 콜백 함수에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-208">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="4b680-209">`.done` 연결을 설정한 후에 모든 코드가 후 콜백 메서드가 실행 되기에 `OnConnected` 서버의 이벤트 처리기 메서드 실행을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-209">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="4b680-210">뒤에 코드의 다음 줄으로 앞의 예제에서 "이제 연결" 문을 넣으면 합니다 `start` 메서드 호출 (아닌를 `.done` 콜백), `console.log` 다음과에서 같이 줄 연결 되기 전에 실행 합니다 예:</span><span class="sxs-lookup"><span data-stu-id="4b680-210">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![연결이 설정 된 후 실행 되는 코드를 작성 하는 잘못 된 방법](signalr-1x-hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="4b680-212">도메인 간 연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-212">How to establish a cross-domain connection</span></span>

<span data-ttu-id="4b680-213">일반적으로 브라우저에서 페이지를 로드 하는 경우 `http://contoso.com`, SignalR 연결에 동일한 도메인에 `http://contoso.com/signalr`입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-213">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="4b680-214">경우 페이지가 `http://contoso.com` 에 연결 `http://fabrikam.com/signalr`, 도메인 간 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-214">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="4b680-215">보안상의 이유로 기본적으로 도메인 간 연결을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-215">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="4b680-216">도메인 간 연결을 설정 하려면 서버에서 도메인 간 연결이 설정 되어 있는지 확인 하 고 연결 개체를 만들 때 연결 URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-216">To establish a cross-domain connection, make sure that cross-domain connections are enabled on the server, and specify the connection URL when you create the connection object.</span></span> <span data-ttu-id="4b680-217">SignalR과 같은 적절 한 기술을 도메인 간 연결에 대 한 사용 됩니다 [JSONP](http://en.wikipedia.org/wiki/JSONP) 하거나 [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-217">SignalR will use the appropriate technology for cross-domain connections, such as [JSONP](http://en.wikipedia.org/wiki/JSONP) or [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span>

<span data-ttu-id="4b680-218">서버에서 호출 하는 경우 해당 옵션을 선택 하 여 도메인 간 연결을 설정 합니다 `MapHubs` 메서드.</span><span class="sxs-lookup"><span data-stu-id="4b680-218">On the server, enable cross-domain connections by selecting that option when you call the `MapHubs` method.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample10.cs?highlight=2)]

<span data-ttu-id="4b680-219">클라이언트에서 생성된 된 프록시) (없음 연결 개체를 만들 때나 (사용 하 여 생성된 된 프록시) 시작 메서드를 호출 하기 전에 URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-219">On the client, specify the URL when you create the connection object (without the generated proxy) or before you call the start method (with the generated proxy).</span></span>

<span data-ttu-id="4b680-220">**도메인 간 연결 (사용 하 여 생성된 된 프록시)를 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-220">**Client code that specifies a cross-domain connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample11.js?highlight=1)]

<span data-ttu-id="4b680-221">**생성된 된 프록시) (없이 도메인 간 연결을 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-221">**Client code that specifies a cross-domain connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="4b680-222">사용 하는 경우는 `$.hubConnection` 포함할 필요가 생성자 `signalr` URL에 자동으로 추가 되므로 (지정 하지 않으면 `useDefaultUrl` 으로 `false`).</span><span class="sxs-lookup"><span data-stu-id="4b680-222">When you use the `$.hubConnection` constructor, you don't have to include `signalr` in the URL because it is added automatically (unless you specify `useDefaultUrl` as `false`).</span></span>

<span data-ttu-id="4b680-223">다른 끝점으로 여러 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-223">You can create multiple connections to different endpoints.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample13.js)]

> [!NOTE] 
> 
> - <span data-ttu-id="4b680-224">설정 하지 않은 `jQuery.support.cors` 코드에서 true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-224">Don't set `jQuery.support.cors` to true in your code.</span></span>
> 
>     ![JQuery.support.cors true로 설정 하지](signalr-1x-hubs-api-guide-javascript-client/_static/image7.png)
> 
>     <span data-ttu-id="4b680-226">SignalR 처리 JSONP 또는 CORS를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-226">SignalR handles the use of JSONP or CORS.</span></span> <span data-ttu-id="4b680-227">설정 `jQuery.support.cors` true SignalR를 브라우저에서 CORS를 지원 하면 되므로 JSONP 사용 하지 않도록 설정 하려면.</span><span class="sxs-lookup"><span data-stu-id="4b680-227">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="4b680-228">Localhost URL에 연결할 때 Internet Explorer 10 않습니다 고려 도메인 간 연결을 응용 프로그램은 작동 로컬로 IE 10을 사용 하 여 서버에서 도메인 간 연결을 설정 하지 않은 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-228">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="4b680-229">Internet Explorer 9를 사용 하 여 도메인 간 연결을 사용 하는 방법에 대 한 내용은 [이 StackOverflow 스레드](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-229">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="4b680-230">Chrome을 사용 하 여 도메인 간 연결을 사용 하는 방법에 대 한 내용은 [이 StackOverflow 스레드](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-230">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="4b680-231">기본값을 사용 하 여 샘플 코드는 "/ signalr" SignalR 서비스에 연결 하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-231">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="4b680-232">다른 기본 URL을 지정 하는 방법에 대 한 정보를 참조 하세요 [ASP.NET SignalR 허브 API 가이드-서버-/signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-232">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>


<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="4b680-233">연결을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-233">How to configure the connection</span></span>

<span data-ttu-id="4b680-234">연결을 설정 하기 전에 쿼리 문자열 매개 변수를 지정할 수도 있고 전송 방법을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-234">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="4b680-235">쿼리 문자열 매개 변수를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-235">How to specify query string parameters</span></span>

<span data-ttu-id="4b680-236">클라이언트가 연결할 때 서버에 데이터를 전송 하려는 경우에 연결 개체에 쿼리 문자열 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-236">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="4b680-237">다음 예제에서는 클라이언트 코드에서 쿼리 문자열 매개 변수를 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-237">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="4b680-238">**(사용 하 여 생성된 된 프록시) 시작 메서드를 호출 하기 전에 쿼리 문자열 값을 설정 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4b680-238">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample14.js?highlight=1)]

<span data-ttu-id="4b680-239">**(없이 생성된 된 프록시) 시작 메서드를 호출 하기 전에 쿼리 문자열 값을 설정 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4b680-239">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample15.js?highlight=2)]

<span data-ttu-id="4b680-240">다음 예에서는 서버 코드에서 쿼리 문자열 매개 변수를 읽는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-240">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample16.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="4b680-241">전송 메서드를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-241">How to specify the transport method</span></span>

<span data-ttu-id="4b680-242">연결 하는 프로세스의 일환으로, SignalR 클라이언트는 일반적으로 서버와 클라이언트 모두에서 지원 되는 최상의 전송을 확인 하도록 서버를 사용 하 여 협상 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-242">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="4b680-243">사용 하려는 하는 전송을 알고 있는 경우 호출 하는 경우에 전송 메서드를 지정 하 여이 협상 프로세스를 무시할 수 있습니다는 `start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="4b680-243">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="4b680-244">**생성된 된 프록시) (사용 하 여 전송 메서드를 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-244">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="4b680-245">**생성된 된 프록시) (없이 전송 메서드를 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-245">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="4b680-246">대신 시도 하는 SignalR 하려는 순서로 여러 전송 메서드를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-246">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="4b680-247">**(사용 하 여 생성된 된 프록시) 사용자 지정 전송 대체 (fallback) 체계를 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-247">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample19.js?highlight=1)]

<span data-ttu-id="4b680-248">**(하지 않는 생성된 된 프록시) 사용자 지정 전송 대체 (fallback) 스키마를 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-248">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample20.js?highlight=2)]

<span data-ttu-id="4b680-249">전송 메서드를 지정 하기 위한 다음 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-249">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="4b680-250">"webSockets"</span><span class="sxs-lookup"><span data-stu-id="4b680-250">"webSockets"</span></span>
- <span data-ttu-id="4b680-251">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="4b680-251">"foreverFrame"</span></span>
- <span data-ttu-id="4b680-252">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="4b680-252">"serverSentEvents"</span></span>
- <span data-ttu-id="4b680-253">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="4b680-253">"longPolling"</span></span>

<span data-ttu-id="4b680-254">다음 예제에서는 연결에서 사용 중인 전송 방법을 확인 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-254">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="4b680-255">**(생성된 된 프록시)와 연결을 사용한 전송 메서드를 표시 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-255">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample21.js?highlight=2)]

<span data-ttu-id="4b680-256">**(없이 생성된 된 프록시) 연결에서 사용 하는 전송 메서드를 표시 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-256">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample22.js?highlight=3)]

<span data-ttu-id="4b680-257">서버 코드에서 전송 메서드를 확인 하는 방법에 대 한 정보를 참조 하세요 [ASP.NET SignalR 허브 API 가이드-서버-컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법을](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-257">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="4b680-258">전송 및 대체에 대 한 자세한 내용은 참조 하세요. [SignalR-전송 및 대체 소개](../getting-started/introduction-to-signalr.md#transports)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-258">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="4b680-259">허브 클래스에 대 한 프록시를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-259">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="4b680-260">사용자가 만든 각 연결 개체는 하나 이상의 허브 클래스를 포함 하는 SignalR 서비스에 대 한 연결에 대 한 정보를 캡슐화 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-260">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="4b680-261">허브 클래스와 통신 하려면 사용자가 직접 만든 (생성 된 프록시를 사용 하지 않는) 하는 경우는 또는를 생성 되는 프록시 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-261">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="4b680-262">클라이언트에서 프록시 이름을 카멜식 대 / 소문자의 버전이 허브 클래스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-262">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="4b680-263">SignalR 자동으로이 변경 되므로 JavaScript 코드는 JavaScript 규칙을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-263">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="4b680-264">**서버의 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="4b680-264">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="4b680-265">**허브에 대 한 생성 된 클라이언트 프록시에 대 한 참조 가져오기**</span><span class="sxs-lookup"><span data-stu-id="4b680-265">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample24.js?highlight=1)]

<span data-ttu-id="4b680-266">**허브 클래스 (없이 생성 된 프록시)에 대 한 클라이언트 프록시 생성**</span><span class="sxs-lookup"><span data-stu-id="4b680-266">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="4b680-267">사용 하 여 허브 클래스를 데코 레이트 하는 경우는 `HubName` 특성, 대/소문자를 변경 하지 않고 이름을 정확 하 게 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-267">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="4b680-268">**HubName 특성을 사용 하 여 서버의 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="4b680-268">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="4b680-269">**허브에 대 한 생성 된 클라이언트 프록시에 대 한 참조 가져오기**</span><span class="sxs-lookup"><span data-stu-id="4b680-269">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample27.js?highlight=1)]

<span data-ttu-id="4b680-270">**허브 클래스 (없이 생성 된 프록시)에 대 한 클라이언트 프록시 생성**</span><span class="sxs-lookup"><span data-stu-id="4b680-270">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample28.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="4b680-271">서버를 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-271">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="4b680-272">허브에서 서버를 호출할 수 있는 메서드를 정의 하려면 이벤트 처리기 허브 프록시를 사용 하 여 추가 합니다 `client` 생성 된 프록시 또는 호출의 속성을 `on` 메서드 생성 된 프록시를 사용 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="4b680-272">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="4b680-273">매개 변수는 복잡 한 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-273">The parameters can be complex objects.</span></span>

<span data-ttu-id="4b680-274">호출 하기 전에 이벤트 처리기를 추가 합니다 `start` 연결을 설정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-274">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="4b680-275">(호출한 후 이벤트 처리기를 추가 하려는 경우를 `start` 메서드를 참조 하십시오 [연결을 설정 하는 방법](#establishconnection) 앞부분에 나오는이 문서화 및 생성 된 프록시를 사용 하지 않고 메서드를 정의 하는 것에 대 한 표시 된 구문을 사용 하 여.)</span><span class="sxs-lookup"><span data-stu-id="4b680-275">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="4b680-276">메서드 이름 일치는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-276">Method name matching is case-insensitive.</span></span> <span data-ttu-id="4b680-277">예를 들어 `Clients.All.addContosoChatMessageToPage` 서버에서 실행 됩니다 `AddContosoChatMessageToPage`를 `addContosoChatMessageToPage`, 또는 `addcontosochatmessagetopage` 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="4b680-277">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="4b680-278">**(사용 하 여 생성된 된 프록시) 클라이언트에서 메서드를 정의 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4b680-278">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample29.js?highlight=2)]

<span data-ttu-id="4b680-279">**(사용 하 여 생성된 된 프록시) 클라이언트에서 메서드를 정의 하는 대체 방법**</span><span class="sxs-lookup"><span data-stu-id="4b680-279">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample30.js?highlight=1-2)]

<span data-ttu-id="4b680-280">**생성된 된 프록시 없이 등의 start 메서드를 호출한 후 추가 하는 경우 클라이언트에서 메서드를 정의 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4b680-280">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample31.js?highlight=3)]

<span data-ttu-id="4b680-281">**클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-281">**Server code that calls the client method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample32.cs?highlight=5)]

<span data-ttu-id="4b680-282">다음 예제에서는 메서드 매개 변수로 복잡 한 개체를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-282">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="4b680-283">**복잡 한 개체 (사용 하 여 생성된 된 프록시)를 사용 하는 클라이언트에서 메서드를 정의 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4b680-283">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample33.js?highlight=2-3)]

<span data-ttu-id="4b680-284">**생성된 된 프록시) (없이 복잡 한 개체를 사용 하는 클라이언트에서 메서드를 정의 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4b680-284">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample34.js?highlight=3-4)]

<span data-ttu-id="4b680-285">**복합 개체를 정의 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-285">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="4b680-286">**복잡 한 개체를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-286">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample36.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="4b680-287">클라이언트에서 서버 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-287">How to call server methods from the client</span></span>

<span data-ttu-id="4b680-288">클라이언트에서 서버 메서드를 호출 하려면 사용 합니다 `server` 생성 된 프록시의 속성 또는 `invoke` 허브 프록시 생성 된 프록시를 사용 하지 않는 경우에 메서드.</span><span class="sxs-lookup"><span data-stu-id="4b680-288">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="4b680-289">반환 값 또는 매개 변수는 복잡 한 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-289">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="4b680-290">허브에서 카멜식 대 / 소문자 버전의 메서드 이름 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-290">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="4b680-291">SignalR 자동으로이 변경 되므로 JavaScript 코드는 JavaScript 규칙을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-291">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="4b680-292">다음 예제에서는 반환 값이 없는 서버 메서드를 호출 하는 방법 및 반환 값이 없는 서버 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-292">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="4b680-293">**HubMethodName 특성이 없는 사용 하 여 서버 메서드**</span><span class="sxs-lookup"><span data-stu-id="4b680-293">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample37.cs?highlight=3)]

<span data-ttu-id="4b680-294">**매개 변수에 전달 된 복합 개체를 정의 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-294">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample38.cs)]

<span data-ttu-id="4b680-295">**(사용 하 여 생성된 된 프록시) 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-295">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample39.js?highlight=1)]

<span data-ttu-id="4b680-296">**(없이 생성된 된 프록시) 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-296">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="4b680-297">사용 하 여 허브 메서드를 데코 레이트 하는 경우는 `HubMethodName` 특성, 대/소문자를 변경 하지 않고 해당 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-297">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="4b680-298">**서버 메서드에서** HubMethodName 특성을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4b680-298">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample41.cs?highlight=3)]

<span data-ttu-id="4b680-299">**(사용 하 여 생성된 된 프록시) 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-299">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample42.js?highlight=1)]

<span data-ttu-id="4b680-300">**(없이 생성된 된 프록시) 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-300">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample43.js?highlight=1)]

<span data-ttu-id="4b680-301">앞의 예제에는 반환 값이 없는 서버 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-301">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="4b680-302">다음 예제에서는 반환 값을 포함 하는 서버 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-302">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="4b680-303">**반환 값이 있는 메서드에 대 한 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-303">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample44.cs?highlight=3)]

<span data-ttu-id="4b680-304">**사용 되는 Stock 클래스는** 값 반환</span><span class="sxs-lookup"><span data-stu-id="4b680-304">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample45.cs?highlight=1)]

<span data-ttu-id="4b680-305">**(사용 하 여 생성된 된 프록시) 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-305">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample46.js?highlight=2,4-5)]

<span data-ttu-id="4b680-306">**(없이 생성된 된 프록시) 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="4b680-306">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample47.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="4b680-307">연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-307">How to handle connection lifetime events</span></span>

<span data-ttu-id="4b680-308">SignalR 처리할 수 있는 수명 이벤트 다음 연결을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-308">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="4b680-309">`starting`: 데이터 연결을 통해 전송 되기 전에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-309">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="4b680-310">`received`: 연결에서 모든 데이터를 수신할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-310">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="4b680-311">수신된 된 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-311">Provides the received data.</span></span>
- <span data-ttu-id="4b680-312">`connectionSlow`: 클라이언트 느리거나 자주 삭제 연결을 검색 하는 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-312">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="4b680-313">`reconnecting`: 기본 전송 다시 시작 될 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-313">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="4b680-314">`reconnected`: 기본 전송에 다시 연결 되 면 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-314">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="4b680-315">`stateChanged`: 연결 상태가 변경 될 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-315">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="4b680-316">이전 상태 및 새 상태 (연결, 연결 됨, 다시 연결, 또는 Disconnected)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-316">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="4b680-317">`disconnected`: 연결이 끊어지면 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-317">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="4b680-318">예를 들어, 상당한 지연을 일으킬 수 있는 연결 문제가 있는 경우 경고 메시지를 표시 하려는 경우를 처리 합니다 `connectionSlow` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-318">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="4b680-319">**(사용 하 여 생성된 된 프록시) connectionSlow 이벤트를 처리 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4b680-319">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample48.js?highlight=1)]

<span data-ttu-id="4b680-320">**생성된 된 프록시) (없이 connectionSlow 이벤트 처리**</span><span class="sxs-lookup"><span data-stu-id="4b680-320">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample49.js?highlight=2)]

<span data-ttu-id="4b680-321">자세한 내용은 [이해 및 SignalR의 연결 수명 이벤트 처리](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-321">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="4b680-322">오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-322">How to handle errors</span></span>

<span data-ttu-id="4b680-323">SignalR JavaScript 클라이언트 제공는 `error` 이벤트에 대 한 처리기를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-323">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="4b680-324">또한 server 메서드 호출에서 발생 하는 오류에 대 한 처리기를 추가 하려면 fail 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-324">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="4b680-325">서버에 대 한 자세한 오류 메시지를 명시적으로 사용 하지 않는 경우 SignalR 오류가 발생 한 후 반환 하는 예외 개체는 오류에 대 한 최소한의 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-325">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="4b680-326">예를 들어, 호출 하는 경우 `newContosoChatMessage` 실패 하면 오류 개체에 오류 메시지에 "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" 프로덕션에서 클라이언트에 자세한 오류 메시지에 대 한 자세한 오류 메시지를 사용 하도록 설정 하려는 경우 있지만 보안상의 이유로 적합 하지 않습니다 보내기 문제 해결을 위해 서버에서 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-326">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample50.cs?highlight=2)]

<span data-ttu-id="4b680-327">다음 예제에서는 오류 이벤트에 대 한 처리기를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-327">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="4b680-328">**(사용 하 여 생성된 된 프록시) 오류 처리기를 추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4b680-328">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample51.js?highlight=1)]

<span data-ttu-id="4b680-329">**오류 처리기 (없이 생성된 된 프록시)를 추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4b680-329">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="4b680-330">다음 예제에서는 메서드 호출에서 오류를 처리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-330">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="4b680-331">**(사용 하 여 생성된 된 프록시) 메서드 호출에서 오류 처리**</span><span class="sxs-lookup"><span data-stu-id="4b680-331">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample53.js?highlight=2)]

<span data-ttu-id="4b680-332">**생성된 된 프록시) (없이 메서드 호출에서 오류 처리**</span><span class="sxs-lookup"><span data-stu-id="4b680-332">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="4b680-333">메서드 호출에 실패 하면를 `error` 이벤트도 발생 하므로에서 코드를 `error` 메서드 처리기 및는 `.fail` 메서드 콜백이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-333">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="4b680-334">클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b680-334">How to enable client-side logging</span></span>

<span data-ttu-id="4b680-335">클라이언트 쪽에서 로깅을 사용 하도록 연결을 설정 합니다 `logging` 를 호출 하기 전에 연결 개체의 속성을 `start` 연결을 설정 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="4b680-335">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="4b680-336">**(사용 하 여 생성된 된 프록시) 로깅을 사용 하도록 설정**</span><span class="sxs-lookup"><span data-stu-id="4b680-336">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample55.js?highlight=1)]

<span data-ttu-id="4b680-337">**(없이 생성된 된 프록시) 로깅을 사용 하도록 설정**</span><span class="sxs-lookup"><span data-stu-id="4b680-337">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample56.js?highlight=2)]

<span data-ttu-id="4b680-338">로그를 확인 하려면 브라우저의 개발자 도구를 열고 콘솔 탭으로 이동 합니다. 이 작업을 수행 하는 방법을 보여주는 스크린샷 단계별 지침 및 화면을 보여 주는 자습서를 참조 하세요 [로깅을 사용 하도록 설정-ASP.NET Signalr을 사용 하 여 서버 브로드캐스트](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b680-338">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](index.md).</span></span>
