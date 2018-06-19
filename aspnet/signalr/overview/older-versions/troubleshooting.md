---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR 문제 해결 (SignalR 1.x) | Microsoft Docs
author: pfletcher
description: 이 문서에서는 SignalR 응용 프로그램을 개발 하는 일반적인 문제를 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/05/2013
ms.topic: article
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: eb739f806eb57d09008fa0bf04b5a40721dab73d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26505822"
---
<a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="30673-103">SignalR 문제 해결 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="30673-103">SignalR Troubleshooting (SignalR 1.x)</span></span>
====================
<span data-ttu-id="30673-104">으로 [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="30673-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="30673-105">이 문서는 SignalR과 일반적인 문제 해결을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-105">This document describes common troubleshooting issues with SignalR.</span></span>


<span data-ttu-id="30673-106">이 문서는 다음 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="30673-107">메서드를 호출 하는 클라이언트와 서버 간에 자동으로 실패</span><span class="sxs-lookup"><span data-stu-id="30673-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="30673-108">기타 연결 문제</span><span class="sxs-lookup"><span data-stu-id="30673-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="30673-109">컴파일 및 서버 쪽 오류</span><span class="sxs-lookup"><span data-stu-id="30673-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="30673-110">Visual Studio 문제</span><span class="sxs-lookup"><span data-stu-id="30673-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="30673-111">인터넷 정보 서비스 문제</span><span class="sxs-lookup"><span data-stu-id="30673-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="30673-112">Azure 문제</span><span class="sxs-lookup"><span data-stu-id="30673-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="30673-113">메서드를 호출 하는 클라이언트와 서버 간에 자동으로 실패</span><span class="sxs-lookup"><span data-stu-id="30673-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="30673-114">이 섹션에서는 의미 있는 오류 메시지가 표시 되지 않고 실패 하는 클라이언트와 서버 간의 메서드 호출에 대 한 가능한 원인을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="30673-115">SignalR 응용 프로그램에서 서버에 클라이언트 구현; 하는 방법에 대 한 정보가 없습니다. 서버 클라이언트 메서드를 호출 하면 메서드 이름과 매개 변수 데이터는 클라이언트에 전송 되 고 메서드는 서버를 지정 하는 형식에 있는 경우에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30673-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="30673-116">메서드가 아무 작업도 수행 클라이언트에서 발견 되는 서버에 오류 메시지가 발생 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="30673-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="30673-117">더 자세히 조사 하려면 클라이언트 메서드를 호출 하지, 서버에서 들어오는 어떤 호출을 표시 하도록 허브에서 start 메서드 호출 하기 전에 로깅을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-117">To further investigate client methods not getting called, you can turn on logging before the calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="30673-118">JavaScript 응용 프로그램에 로그인 할 참조 [클라이언트 쪽 로깅 (JavaScript 클라이언트 버전)를 사용 하도록 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="30673-119">.NET 클라이언트 응용 프로그램에 로그인 할 참조 [클라이언트 쪽 로깅 (.NET 클라이언트 버전)를 사용 하도록 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-net-client.md#logging)합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="30673-120">철자가 잘못 된 메서드, 잘못 된 메서드 서명 또는 잘못 된 허브 이름</span><span class="sxs-lookup"><span data-stu-id="30673-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="30673-121">이름 또는 호출 메서드의 시그니처가 정확히 일치 하지 않는 클라이언트에서 적절 한 메서드를 호출 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="30673-122">호출 하 여 메서드 이름을 클라이언트에 대 한 메서드의 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="30673-123">또한 SignalR 카멜식 대/소문자를 사용 하는 메서드를 사용 하 여 허브 프록시를 만들고 JavaScript에서 적절 한 그대로 따라서 메서드가 호출 `SendMessage` 서버에서 호출 되 `sendMessage` 클라이언트 프록시에 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="30673-124">사용 하는 경우는 `HubName` 서버 쪽 코드에 특성을 사용 하는 이름을 클라이언트에 허브를 만드는 데 이름 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="30673-125">사용 하지 않는 경우는 `HubName` 특성을 카멜식 대, ChatHub 대신 chatHub 같은 JavaScript 클라이언트에 허브의 이름 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="30673-126">클라이언트에서 중복 된 메서드 이름</span><span class="sxs-lookup"><span data-stu-id="30673-126">Duplicate method name on client</span></span>

<span data-ttu-id="30673-127">대/소문자만 다른 클라이언트에 중복 된 메서드를 되어 있지 않은 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="30673-128">클라이언트 응용 프로그램 라는 메서드가 경우 `sendMessage`, 메서드 호출 또한 없는지 확인 `SendMessage` 도 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="30673-129">클라이언트에서 누락 된 JSON 파서</span><span class="sxs-lookup"><span data-stu-id="30673-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="30673-130">SignalR의 서버와 클라이언트 간의 호출을 직렬화 하는 데 사용할 수는 JSON 파서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="30673-131">클라이언트는 기본 제공 JSON 파서 (예: Internet Explorer 7)가 없으면 응용 프로그램에서 종료자를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="30673-132">JSON 파서를 다운로드할 수 있습니다 [여기](http://nuget.org/packages/json2)합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="30673-133">허브 및 PersistentConnection 구문을 함께</span><span class="sxs-lookup"><span data-stu-id="30673-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="30673-134">두 개의 통신 모델을 사용 하 여 SignalR: 허브 및 PersistentConnections 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="30673-135">이러한 두 개의 통신 모델을 호출 하기 위한 구문이 클라이언트 코드에서 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="30673-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="30673-136">서버 코드에서 허브를 추가한 경우 모든 클라이언트 코드에서는 적절 한 허브 구문을 사용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="30673-137">**JavaScript 클라이언트에에서 만드는 코드를 한 PersistentConnection은 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="30673-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="30673-138">**JavaScript 클라이언트 코드는 Javascript 클라이언트의 허브 프록시를 생성 합니다.**</span><span class="sxs-lookup"><span data-stu-id="30673-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="30673-139">**C# 서버 코드 경로 PersistentConnection 매핑되는**</span><span class="sxs-lookup"><span data-stu-id="30673-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="30673-140">**C# 서버 코드 여러 응용 프로그램의 경우를 허브 또는 여러 허브에 대 한 경로 매핑하는**</span><span class="sxs-lookup"><span data-stu-id="30673-140">**C# server code that maps a route to a Hub, or to mulitple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="30673-141">구독 추가 되기 전에 시작 된 연결</span><span class="sxs-lookup"><span data-stu-id="30673-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="30673-142">연결 허브의 서버에서 호출 될 수 있는 메서드는 프록시에 추가 되기 전에 시작 되 면 메시지를 수신할 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="30673-143">다음 JavaScript 코드에서 허브를 제대로 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="30673-144">**허브 메시지를 받으려면 수 없는 잘못 된 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="30673-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="30673-145">대신, 시작을 호출 하기 전에 메서드 구독을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="30673-146">**올바르게 허브에 구독을 추가 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="30673-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="30673-147">허브 프록시에 누락 된 메서드 이름</span><span class="sxs-lookup"><span data-stu-id="30673-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="30673-148">클라이언트에서 서버에 정의 된 메서드는을 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="30673-149">서버는 메서드를 정의 하는 경우에 여전히 클라이언트 프록시에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="30673-150">메서드는 다음과 같은 방법으로 클라이언트 프록시에 추가할 수 있습니다 (에 메서드가 추가 되는 `client` 하지 허브 직접 허브 소속):</span><span class="sxs-lookup"><span data-stu-id="30673-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="30673-151">**허브 프록시에 메서드를 추가 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="30673-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="30673-152">허브 또는 허브 메서드를 Public로 선언 되지 않았습니다</span><span class="sxs-lookup"><span data-stu-id="30673-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="30673-153">클라이언트에 표시 되려면 허브 구현 및 메서드도 선언 해야 `public`합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="30673-154">다른 응용 프로그램에서 허브에 액세스</span><span class="sxs-lookup"><span data-stu-id="30673-154">Accessing hub from a different application</span></span>

<span data-ttu-id="30673-155">SignalR 허브 SignalR 클라이언트를 구현 하는 응용 프로그램을 통해 액세스할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="30673-156">SignalR 다른 통신 라이브러리 (예: SOAP 또는 WCF 웹 서비스입니다.)와 상호 작용할 수 없습니다. 대상 플랫폼에서 사용할 수 없는 SignalR 클라이언트 경우 서버의 끝점을 직접 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="30673-157">수동으로 데이터를 직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-157">Manually serializing data</span></span>

<span data-ttu-id="30673-158">SignalR 자동으로 사용 됩니다 JSON 메서드를 직렬화 하는 데 매개 변수-여기의 않아도 직접 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="30673-159">OnDisconnected 함수에는 클라이언트에서 실행 되지 않은 원격 허브 메서드</span><span class="sxs-lookup"><span data-stu-id="30673-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="30673-160">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-160">This behavior is by design.</span></span> <span data-ttu-id="30673-161">때 `OnDisconnected` 는 호출할 허브 이미 입력는 `Disconnected` 허브 호출 될 메서드를 더 이상 허용 하지 않는 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="30673-162">**C# 서버 코드 올바르게 OnDisconnected 이벤트의 코드를 실행 하는**</span><span class="sxs-lookup"><span data-stu-id="30673-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="30673-163">연결 제한에 도달</span><span class="sxs-lookup"><span data-stu-id="30673-163">Connection limit reached</span></span>

<span data-ttu-id="30673-164">Windows 7과 같은 클라이언트 운영 체제에서 IIS의 전체 버전을 사용할 경우 10 연결 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30673-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="30673-165">클라이언트 운영 체제를 사용 하는 경우 IIS Express 대신 사용이 제한을 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="30673-166">도메인 간 연결을 적절히 설정 되지</span><span class="sxs-lookup"><span data-stu-id="30673-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="30673-167">도메인 간 연결 하는 경우 (입니다 SignalR URL이 호스팅 페이지와 동일한 도메인에 연결)가 올바르게 설정 되지, 오류 메시지 없이 연결이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="30673-168">도메인 간 통신을 사용 하는 방법에 대 한 정보를 참조 하십시오. [도메인 간 연결을 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="30673-169">.NET 클라이언트에서 작동 하지 않을 NTLM (Active Directory)를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="30673-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="30673-170">도메인 보안을 사용 하는.NET 클라이언트 응용 프로그램에서 연결 연결이 제대로 구성 되지 않은 경우에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="30673-171">도메인 환경에서 SignalR을 사용 하려면 필요한 연결 속성을 다음과 같이 설정.</span><span class="sxs-lookup"><span data-stu-id="30673-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="30673-172">**C# 클라이언트 코드는 연결 자격 증명을 구현 합니다.**</span><span class="sxs-lookup"><span data-stu-id="30673-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="30673-173">기타 연결 문제</span><span class="sxs-lookup"><span data-stu-id="30673-173">Other connection issues</span></span>

<span data-ttu-id="30673-174">이 섹션에서는 원인과 그 해결 특정 증상 또는 연결 하는 동안 발생 하는 오류 메시지에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="30673-175">"시작 해야 데이터를 보내기 전에 호출 됨" 오류</span><span class="sxs-lookup"><span data-stu-id="30673-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="30673-176">이 오류는 일반적으로 연결을 시작 하기 전에 코드 SignalR 개체를 참조 하는 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30673-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="30673-177">처리기와 유사한에 대 한 연결이 메서드를 호출 하는 서버에 정의 된 추가 되어야 함을 연결이 완료 된 후입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="30673-178">에 대 한 호출 `Start` 비동기 이므로 호출 되기 전에 실행 될 수 후에 코드를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="30673-179">처리기를 추가 하려면 연결이 완전히 시작 된 후에 start 메서드를 매개 변수로 전달 되는 콜백 함수에 배치 하는 가장 좋은 방법은:</span><span class="sxs-lookup"><span data-stu-id="30673-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="30673-180">**올바르게 SignalR 개체를 참조 하는 이벤트 처리기를 추가 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="30673-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="30673-181">이 오류는 연결 하는 SignalR 개체가 여전히 참조 하는 동안 중지 하는 경우에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="30673-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="30673-182">"301 영구적으로 이동" 또는 "302 일시적으로 이동" 오류</span><span class="sxs-lookup"><span data-stu-id="30673-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="30673-183">이 오류는 프로젝트에 자동으로 만들어진 프록시에 방해가 됩니다는 SignalR 이라는 경우 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="30673-184">이 오류를 방지 하려면 라는 폴더를 사용 하지 않는 `SignalR` 응용 프로그램 또는 off 자동 프록시 생성 설정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="30673-185">참조 [은을 수행 하 고 생성 된 프록시](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) 자세한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="30673-186">.NET 또는 Silverlight 클라이언트에서 "403 사용할 수 없음" 오류</span><span class="sxs-lookup"><span data-stu-id="30673-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="30673-187">이 오류는 도메인 간 통신 해제 되어 없는 제대로 도메인 간 환경에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="30673-188">도메인 간 통신을 사용 하는 방법에 대 한 정보를 참조 하십시오. [도메인 간 연결을 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="30673-189">Silverlight 클라이언트에서 도메인 간 연결을 설정 하려면 참조 [Silverlight 클라이언트에서 도메인 간 연결](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="30673-190">"404 찾을 수 없음" 오류</span><span class="sxs-lookup"><span data-stu-id="30673-190">"404 Not Found" error</span></span>

<span data-ttu-id="30673-191">이 문제에 대 한 여러 원인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-191">There are several causes for this issue.</span></span> <span data-ttu-id="30673-192">다음을 모두 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-192">Verify all of the following:</span></span>

- <span data-ttu-id="30673-193">**허브 프록시 주소 참조 형식이 잘못:** 생성 된 허브 프록시 주소에 대 한 참조 올바르게 포맷 되어 있지 않으면이 오류는 일반적으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30673-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="30673-194">허브 주소에 대 한 참조가 제대로 적용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="30673-195">참조 [동적으로 생성 된 프록시를 참조 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="30673-196">**허브 경로 추가 하기 전에 응용 프로그램에 경로 추가:** 응용 프로그램에서 다른 경로 사용 하는 경우 추가 하는 첫 번째 경로에 대 한 호출 인지 확인 `MapHubs`합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="30673-197">"500 내부 서버 오류"</span><span class="sxs-lookup"><span data-stu-id="30673-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="30673-198">다양 한 원인이 있을 수 있으며 매우 일반적인 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="30673-199">오류의 세부 정보는 서버의 이벤트 로그에 표시 되어야 또는 서버 디버깅을 통해 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="30673-200">자세한 오류가 서버에서 설정 하 여 자세한 오류 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="30673-201">자세한 내용은 참조 [허브 클래스에는 오류 처리 방법을](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="30673-202">"TypeError: &lt;hubType&gt; 정의 되지 않았습니다" 오류</span><span class="sxs-lookup"><span data-stu-id="30673-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="30673-203">경우이 오류가 발생에 대 한 호출 `MapHubs` 제대로 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="30673-204">참조 [SignalR 경로 등록 하 고 SignalR 옵션을 구성 하는 방법](../guide-to-the-api/hubs-api-guide-server.md#route) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="30673-205">JsonSerializationException은 사용자 코드에 의해 처리 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="30673-206">메서드에 보낼 매개 변수 (예: 파일 핸들, 데이터베이스 연결) serializable이 아닌 형식에 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="30673-207">사용 하 여 (또는 보안에 대 한 직렬화에 속하는 이유로), 클라이언트에 전송 하지 않으려는 서버 측 개체에 멤버를 사용 해야 하는 경우는 `JSONIgnore` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="30673-208">"프로토콜 오류: 알 수 없는 전송" 오류</span><span class="sxs-lookup"><span data-stu-id="30673-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="30673-209">이 오류는 클라이언트가 SignalR에서 사용 되는 전송을 지원 하지 않는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="30673-210">참조 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports) 정보를 브라우저 사용 하 여 SignalR에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="30673-211">"JavaScript Hub 프록시 생성이 비활성화 되었습니다."</span><span class="sxs-lookup"><span data-stu-id="30673-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="30673-212">이 오류가 발생 합니다 `DisableJavaScriptProxies` 에서 동적으로 생성 된 프록시에 대 한 참조를 포함 하는 동안 설정 된 `signalr/hubs`합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="30673-213">프록시를 수동으로 만드는 방법에 대 한 자세한 내용은 참조 하십시오. [생성 된 프록시 및 수에 대 한 역할](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="30673-214">"잘못 된 형식의 연결 ID가" 또는 "사용자 id는 활성 SignalR 연결 중 변경할 수 없습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="30673-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="30673-215">인증을 사용 하 고 클라이언트 로그 아웃 됩니다. 연결을 중지 하기 전에 경우이 오류가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="30673-216">솔루션은 클라이언트 로그 아웃 하기 전에 SignalR 연결을 중지 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="30673-217">"오류 확인할 수 없는: SignalR: jQuery 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="30673-218">JQuery SignalR.js 파일 전에 참조를 확인 하십시오"오류</span><span class="sxs-lookup"><span data-stu-id="30673-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="30673-219">SignalR JavaScript 클라이언트를 실행 하는 jQuery 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="30673-220">참조 jQuery 사용 하는 경로 올바른지 및 SignalR에 대 한 참조 하기 전에 jQuery에 대 한 참조 인지 정확한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="30673-221">"TypeError 확인할 수 없는: 속성을 읽을 수 없습니다 '&lt;속성&gt;' 정의 되지 않은의" 오류</span><span class="sxs-lookup"><span data-stu-id="30673-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="30673-222">JQuery 또는 허브 프록시 올바르게 참조 하지 않아도이 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="30673-223">JQuery 및 허브 프록시에서는 참조 올바름, 사용 되는 경로가 올바른지, jQuery에 대 한 참조 허브 프록시에 대 한 참조 하기 전에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="30673-224">허브 프록시에 대 한 기본 참조는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30673-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="30673-225">**허브 프록시를 올바르게 참조 하는 HTML 클라이언트 쪽 코드**</span><span class="sxs-lookup"><span data-stu-id="30673-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="30673-226">"RuntimeBinderException 처리 되지 않았습니다. 사용자 코드에서" 오류</span><span class="sxs-lookup"><span data-stu-id="30673-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="30673-227">이 오류가 발생할 때의 잘못 된 오버 로드 `Hub.On` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30673-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="30673-228">메서드 반환 값이 있으면 반환 형식은 제네릭 형식 매개 변수로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="30673-229">**생성 된 프록시) (없이 클라이언트에 정의 된 메서드**</span><span class="sxs-lookup"><span data-stu-id="30673-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="30673-230">연결 페이지를 로드할 사이 나누기 또는 연결 ID 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="30673-231">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-231">This behavior is by design.</span></span> <span data-ttu-id="30673-232">Page 개체에는 허브 개체 호스팅되므로, 허브 페이지를 새로 고칠 때 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30673-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="30673-233">다중 페이지 응용 프로그램 사용자와 연결 Id 간의 연결 유지 하는 것은 페이지가 로드 간에 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="30673-234">연결 Id를 서버에 저장할 수는 `ConcurrentDictionary` 개체 또는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="30673-235">"값은 null 일 수 없습니다" 오류</span><span class="sxs-lookup"><span data-stu-id="30673-235">"Value cannot be null" error</span></span>

<span data-ttu-id="30673-236">선택적 매개 변수를 사용 하 여 서버 쪽 메서드는 현재 지원 되지 않습니다. 선택적 매개 변수를 생략 하면 메서드가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="30673-237">자세한 내용은 참조 [선택적 매개 변수](https://github.com/SignalR/SignalR/issues/324)합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="30673-238">"Firefox에 있는 서버에 연결을 만들지 &lt;주소&gt;" Firebug 하는 동안 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="30673-239">WebSocket 전송의 협상에 실패 하 고 다른 전송을 대신 사용 하는 경우이 오류 메시지가 Firebug에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="30673-240">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="30673-241">.NET 클라이언트 응용 프로그램에 오류가 "원격 인증서 유효성 검사 절차에 따라 잘못 되었습니다."</span><span class="sxs-lookup"><span data-stu-id="30673-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="30673-242">서버에 추가 하 여 x509certificate 연결을 요청 하기 전에 사용자 지정 클라이언트 인증서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="30673-243">인증서를 사용 하 여 연결 추가 `Connection.AddClientCertificate`합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="30673-244">인증 시간 초과 후 연결 삭제</span><span class="sxs-lookup"><span data-stu-id="30673-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="30673-245">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-245">This behavior is by design.</span></span> <span data-ttu-id="30673-246">연결이 활성 상태 동안 인증 자격 증명을 수정할 수 없습니다. 자격 증명을 새로 고치려면 연결을 중지 했다가 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="30673-247">OnConnected는 jQuery Mobile을 사용 하는 경우에 두 번 호출</span><span class="sxs-lookup"><span data-stu-id="30673-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="30673-248">jQuery Mobile의 `initializePage` 함수 강제로 다시 실행 하는 각 페이지의 스크립트는 두 번째 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30673-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="30673-249">이 문제에 대 한 솔루션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="30673-250">JQuery Mobile 전에 JavaScript 파일에 대 한 참조를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="30673-251">사용 하지 않도록 설정 된 `initializePage` 설정 하 여 함수 `$.mobile.autoInitializePage = false`합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="30673-252">연결을 시작 하기 전에 초기화를 완료 하려면 페이지를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="30673-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="30673-253">이벤트를 전송 하는 서버를 사용 하 여 Silverlight 응용 프로그램에서 메시지가 지연</span><span class="sxs-lookup"><span data-stu-id="30673-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="30673-254">Silverlight에서 이벤트를 보낸 서버를 사용 하는 경우 메시지가 지연 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="30673-255">연결을 시작할 때 긴 폴링과 대신 사용할를 강제로 표시 하려면 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="30673-256">프로토콜 프레임 영원히 "권한이 거부 되었습니다"를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="30673-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="30673-257">이것은 알려진된 문제를 설명 [여기](https://github.com/SignalR/SignalR/issues/1963)합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="30673-258">최신 JQuery 라이브러리를 사용 하 여 이러한 현상이 나타날 수 있습니다. 해결 방법은 JQuery 1.8.2에 응용 프로그램을 다운 그레이드 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="30673-259">컴파일 및 서버 쪽 오류</span><span class="sxs-lookup"><span data-stu-id="30673-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="30673-260">다음 섹션에는 컴파일러와 서버 쪽 런타임 오류에는 가능한 해결 방법이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="30673-261">허브 인스턴스에 대 한 참조는 null</span><span class="sxs-lookup"><span data-stu-id="30673-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="30673-262">허브 인스턴스를 각 연결에 대해 만든 있으므로 만들 수 없습니다 허브 인스턴스의 코드에서 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="30673-263">메서드를 호출할 허브 자체 외부에서 허브를 참조 하세요. [클라이언트 메서드를 호출할 허브 클래스 외부에서 그룹을 관리 하는 방법을](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) 허브 컨텍스트에 대 한 참조를 가져오는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="30673-264">HTTPContext.Current.Session null입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="30673-265">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-265">This behavior is by design.</span></span> <span data-ttu-id="30673-266">SignalR 이중 메시징을 작동 하지 않으므로 세션 상태를 사용 하도록 설정 하므로 ASP.NET 세션 상태를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="30673-267">재정의 하는 적절 한 방법</span><span class="sxs-lookup"><span data-stu-id="30673-267">No suitable method to override</span></span>

<span data-ttu-id="30673-268">이전 문서 또는 블로그에서 코드를 사용 하는 경우이 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="30673-269">변경 되었거나 더 이상 사용 되지 하는 메서드의 이름을 참조 하지 않는지 확인 하십시오 (같은 `OnConnectedAsync`).</span><span class="sxs-lookup"><span data-stu-id="30673-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="30673-270">HostContextExtensions.WebSocketServerUrl null입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="30673-271">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-271">This behavior is by design.</span></span> <span data-ttu-id="30673-272">이 멤버는 사용 되지 않으며 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="30673-273">"'Signalr.hubs' 라는 경로 경로 컬렉션에 이미 이" 오류</span><span class="sxs-lookup"><span data-stu-id="30673-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="30673-274">이 오류는 있으면 나타납니다 `MapHubs` 응용 프로그램에서 두 번 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30673-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="30673-275">일부 예제 응용 프로그램 호출 `MapHubs` 직접 전역 응용 프로그램 파일에 다른 확인은 래퍼 클래스에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="30673-276">응용 프로그램 둘 다 수행 하지 않습니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="30673-277">Visual Studio 문제</span><span class="sxs-lookup"><span data-stu-id="30673-277">Visual Studio issues</span></span>

<span data-ttu-id="30673-278">이 섹션에서는 Visual Studio에서 발생 하는 문제에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="30673-279">솔루션 탐색기에서 스크립트 문서 노드가 표시 되지 않으면</span><span class="sxs-lookup"><span data-stu-id="30673-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="30673-280">이 자습서의 일부 디버깅 하는 동안 솔루션 탐색기의 "스크립트 문서" 노드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="30673-281">이 노드는 JavaScript 디버거에서 생성 및 Internet Explorer;의 브라우저 클라이언트를 디버깅 하는 동안에 나타납니다. Chrome 또는 Firefox 사용 되는 경우에 노드가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="30673-282">JavaScript 디버거도 실행 되지 않습니다 Silverlight 디버거와 같은 다른 클라이언트 디버거가 실행 중인 경우.</span><span class="sxs-lookup"><span data-stu-id="30673-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="30673-283">또는 이전 버전의 Visual Studio 2008 SignalR 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="30673-284">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30673-284">This behavior is by design.</span></span> <span data-ttu-id="30673-285">SignalR은.NET Framework 4 이상을;이 필요 Visual Studio 2010 이상에서 SignalR 응용 프로그램을 개발할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="30673-286">IIS 문제</span><span class="sxs-lookup"><span data-stu-id="30673-286">IIS issues</span></span>

<span data-ttu-id="30673-287">이 섹션에는 인터넷 정보 서비스 문제가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="30673-288">웹 사이트가 MapHubs 호출한 후 중단</span><span class="sxs-lookup"><span data-stu-id="30673-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="30673-289">SignalR의 최신 버전에서이 문제가 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="30673-290">NuGet을 사용 하 여 설치를 업데이트 하 여 발표 된 최신 버전의 SignalR 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30673-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="30673-291">Azure 문제</span><span class="sxs-lookup"><span data-stu-id="30673-291">Azure issues</span></span>

<span data-ttu-id="30673-292">이 섹션에는 Microsoft Azure 문제가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="30673-293">항목 이름 변경 후 Azure 백플레인에서 통해 메시지가 수신 되지 않은</span><span class="sxs-lookup"><span data-stu-id="30673-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="30673-294">항목에서는 Azure 백플레인에서에서 사용 하는 사용자를 구성할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30673-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>
