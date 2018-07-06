---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
title: ASP.NET SignalR 허브 API 가이드-.NET 클라이언트 (SignalR 1.x) | Microsoft Docs
author: pfletcher
description: 이 문서에서는 허브 API를 사용 하 여 버전 2 (WinRT) Windows 스토어, WPF, Silverlight 및 단점 같은.NET 클라이언트에서 SignalR에 대 한 소개를 제공 하는 중...
ms.author: aspnetcontent
ms.date: 04/17/2013
ms.assetid: c334adc3-d6dc-44f3-9f06-f7634475aad3
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 64d4f16dfcd121bc73f05cf8d320dc6ff2488f9a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37834690"
---
<a name="aspnet-signalr-hubs-api-guide---net-client-signalr-1x"></a><span data-ttu-id="1d3e8-103">ASP.NET SignalR 허브 API 가이드-.NET 클라이언트 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="1d3e8-103">ASP.NET SignalR Hubs API Guide - .NET Client (SignalR 1.x)</span></span>
====================
<span data-ttu-id="1d3e8-104">하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="1d3e8-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="1d3e8-105">이 문서에서는 허브 API를 사용 하 여 버전 2 (WinRT) Windows 스토어, WPF, Silverlight 및 콘솔 응용 프로그램 등.NET 클라이언트에서 SignalR에 대 한 소개를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-105">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
> 
> <span data-ttu-id="1d3e8-106">SignalR 허브 API를 사용 하면 클라이언트가 서버에 연결 된 클라이언트에는 서버에서 원격 프로시저 호출 (Rpc)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="1d3e8-107">서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="1d3e8-108">클라이언트 코드에서 서버에서 호출할 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="1d3e8-109">SignalR은 모든 클라이언트-서버 연결 구조를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="1d3e8-110">또한 SignalR 영구 연결을 호출 하는 하위 수준 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="1d3e8-111">SignalR에서 허브 및 영구 연결에 대 한 소개, 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서에 대 한 참조 [SignalR-Getting Started](../getting-started/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>


## <a name="overview"></a><span data-ttu-id="1d3e8-112">개요</span><span class="sxs-lookup"><span data-stu-id="1d3e8-112">Overview</span></span>

<span data-ttu-id="1d3e8-113">이 문서는 다음 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="1d3e8-114">클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="1d3e8-114">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="1d3e8-115">연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-115">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="1d3e8-116">Silverlight 클라이언트에서 도메인 간 연결</span><span class="sxs-lookup"><span data-stu-id="1d3e8-116">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="1d3e8-117">연결을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-117">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="1d3e8-118">WPF 클라이언트의 최대 동시 연결 수를 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-118">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="1d3e8-119">쿼리 문자열 매개 변수를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-119">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="1d3e8-120">전송 메서드를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-120">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="1d3e8-121">HTTP 헤더를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-121">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="1d3e8-122">클라이언트 인증서를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-122">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="1d3e8-123">허브 프록시를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-123">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="1d3e8-124">서버를 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-124">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="1d3e8-125">매개 변수 없이 메서드</span><span class="sxs-lookup"><span data-stu-id="1d3e8-125">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="1d3e8-126">매개 변수 형식을 지정 하는 매개 변수를 사용 하 여 메서드</span><span class="sxs-lookup"><span data-stu-id="1d3e8-126">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="1d3e8-127">매개 변수에 대해 동적 개체를 지정 하는 매개 변수를 사용 하 여 메서드</span><span class="sxs-lookup"><span data-stu-id="1d3e8-127">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="1d3e8-128">처리기를 제거 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-128">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="1d3e8-129">클라이언트에서 서버 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-129">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="1d3e8-130">연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-130">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="1d3e8-131">오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-131">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="1d3e8-132">클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-132">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="1d3e8-133">WPF, Silverlight 및 콘솔 응용 프로그램 서버를 호출할 수 있는 클라이언트 방법에 대 한 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="1d3e8-133">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="1d3e8-134">샘플.NET 클라이언트 프로젝트에 대 한 다음 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-134">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="1d3e8-135">[gustavo armenta / SignalR 샘플](https://github.com/gustavo-armenta/SignalR-Samples) github.com (WinRT, Silverlight, 콘솔 앱 예제).</span><span class="sxs-lookup"><span data-stu-id="1d3e8-135">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="1d3e8-136">[DamianEdwards / SignalR MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) github.com (WPF 예제).</span><span class="sxs-lookup"><span data-stu-id="1d3e8-136">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="1d3e8-137">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) github.com (콘솔 앱 예제).</span><span class="sxs-lookup"><span data-stu-id="1d3e8-137">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="1d3e8-138">프로그래밍 하는 방법에 대 한 설명서에 대 한 서버 또는 JavaScript 클라이언트는 다음 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-138">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="1d3e8-139">SignalR 허브 API 가이드-서버</span><span class="sxs-lookup"><span data-stu-id="1d3e8-139">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="1d3e8-140">SignalR 허브 API 가이드-JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="1d3e8-140">SignalR Hubs API Guide - JavaScript Client</span></span>](../guide-to-the-api/hubs-api-guide-javascript-client.md)

<span data-ttu-id="1d3e8-141">.NET 4.5 버전의 API는 API 참조 항목에 대 한 링크.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-141">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="1d3e8-142">.NET 4를 사용 하는 경우 참조 [항목에서는 API의.NET 4 버전](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-142">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="1d3e8-143">클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="1d3e8-143">Client setup</span></span>

<span data-ttu-id="1d3e8-144">설치를 [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet 패키지 (되지 합니다 [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) 패키지).</span><span class="sxs-lookup"><span data-stu-id="1d3e8-144">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="1d3e8-145">이 패키지는.NET 4 및.NET 4.5에 대 한 WinRT, Silverlight, WPF, 콘솔 응용 프로그램 및 Windows Phone 클라이언트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-145">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="1d3e8-146">버전의 SignalR 클라이언트에 있는 서버에 있는 버전과 다른 경우 SignalR은 차이 할 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-146">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="1d3e8-147">예를 들어, SignalR 2.0 버전은 출시을 설치 하는 서버의 경우 서버 1.1.x 2.0이 설치 되어 있는 클라이언트를 설치 되어 있는 클라이언트 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-147">For example, when SignalR version 2.0 is released and you install that on the server, the server will support clients that have 1.1.x installed as well as clients that have 2.0 installed.</span></span> <span data-ttu-id="1d3e8-148">클라이언트 버전과 서버 버전 간의 차이점은 너무, SignalR throw는 `InvalidOperationException` 클라이언트 연결을 시도 하는 동안 예외가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-148">If the difference between the version on the server and the version on the client is too great, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="1d3e8-149">오류 메시지는 "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`"입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-149">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="1d3e8-150">연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-150">How to establish a connection</span></span>

<span data-ttu-id="1d3e8-151">만들 필요가 대 한 연결을 설정 하기 전에 `HubConnection` 개체 및 프록시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-151">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="1d3e8-152">연결을 설정 하려면 호출을 `Start` 메서드는 `HubConnection` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-152">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> <span data-ttu-id="1d3e8-153">JavaScript 클라이언트에 대 한 하나 이상의 이벤트 처리기를 호출 하기 전에 등록 해야 합니다 `Start` 연결을 설정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-153">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="1d3e8-154">.NET 클라이언트에 대 한 필요한 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-154">This is not necessary for .NET clients.</span></span> <span data-ttu-id="1d3e8-155">JavaScript 클라이언트에 대 한 생성 된 프록시 코드를 자동으로 존재 하는 모든 허브에 대 한 프록시 서버에서 만들어지고 있는 허브를 표시 하는 방법에 처리기를 등록 클라이언트에서 사용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-155">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="1d3e8-156">.NET 클라이언트에 대 한 수 있지만 만들 허브 프록시를 수동으로 SignalR를 사용 하 게 모든 허브에 대 한 프록시를 만드는 것으로 가정 하므로.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-156">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>


<span data-ttu-id="1d3e8-157">기본값을 사용 하 여 샘플 코드는 "/ signalr" SignalR 서비스에 연결 하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-157">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="1d3e8-158">다른 기본 URL을 지정 하는 방법에 대 한 정보를 참조 하세요 [ASP.NET SignalR 허브 API 가이드-서버-/signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-158">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="1d3e8-159">`Start` 메서드를 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-159">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="1d3e8-160">연결이 설정 되 면 코드의 다음 줄까지 실행 하지 않도록 확인을 사용 하 여 `await` ASP.NET 4.5 비동기 메서드에서 또는 `.Wait()` 동기 메서드에서.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-160">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="1d3e8-161">사용 하지 않는 `.Wait()` WinRT 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-161">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<span data-ttu-id="1d3e8-162">`HubConnection` 클래스는 스레드로부터 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-162">The `HubConnection` class is thread-safe.</span></span>

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="1d3e8-163">Silverlight 클라이언트에서 도메인 간 연결</span><span class="sxs-lookup"><span data-stu-id="1d3e8-163">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="1d3e8-164">Silverlight 클라이언트에서 도메인 간 연결을 사용 하는 방법에 대 한 정보를 참조 하세요 [는 서비스 사용 가능한 도메인 경계를 넘어 수행](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-164">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="1d3e8-165">연결을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-165">How to configure the connection</span></span>

<span data-ttu-id="1d3e8-166">연결을 설정 하기 전에 다음 옵션 중 하나를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-166">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="1d3e8-167">동시 연결 수 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-167">Concurrent connections limit.</span></span>
- <span data-ttu-id="1d3e8-168">쿼리 문자열 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-168">Query string parameters.</span></span>
- <span data-ttu-id="1d3e8-169">전송 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-169">The transport method.</span></span>
- <span data-ttu-id="1d3e8-170">HTTP 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-170">HTTP headers.</span></span>
- <span data-ttu-id="1d3e8-171">클라이언트 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-171">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="1d3e8-172">WPF 클라이언트의 최대 동시 연결 수를 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-172">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="1d3e8-173">WPF 클라이언트의 기본 값 2의 동시 연결의 최대 수를 증가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-173">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="1d3e8-174">권장된 값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-174">The recommended value is 10.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

<span data-ttu-id="1d3e8-175">자세한 내용은 [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-175">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="1d3e8-176">쿼리 문자열 매개 변수를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-176">How to specify query string parameters</span></span>

<span data-ttu-id="1d3e8-177">클라이언트가 연결할 때 서버에 데이터를 전송 하려는 경우에 연결 개체에 쿼리 문자열 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-177">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="1d3e8-178">다음 예제에서는 클라이언트 코드에서 쿼리 문자열 매개 변수를 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-178">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="1d3e8-179">다음 예에서는 서버 코드에서 쿼리 문자열 매개 변수를 읽는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-179">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="1d3e8-180">전송 메서드를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-180">How to specify the transport method</span></span>

<span data-ttu-id="1d3e8-181">연결 하는 프로세스의 일환으로, SignalR 클라이언트는 일반적으로 서버와 클라이언트 모두에서 지원 되는 최상의 전송을 확인 하도록 서버를 사용 하 여 협상 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-181">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="1d3e8-182">사용 하려는 하는 전송, 이미 알고 있는 경우에이 협상 프로세스를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-182">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="1d3e8-183">전송 메서드를 지정 하려면 Start 메서드에 전송 개체에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-183">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="1d3e8-184">다음 예제에서는 클라이언트 코드에서 전송 메서드를 지정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-184">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

<span data-ttu-id="1d3e8-185">합니다 [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) 네임 스페이스는 전송을 지정 하는 데 사용할 수 있는 다음 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-185">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="1d3e8-186">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="1d3e8-186">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="1d3e8-187">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="1d3e8-187">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="1d3e8-188">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (사용 가능 서버와 클라이언트 모두.NET 4.5를 사용 하는 경우에)</span><span class="sxs-lookup"><span data-stu-id="1d3e8-188">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="1d3e8-189">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (자동으로 선택 되는 클라이언트와 서버 모두에서 지원 되는 최상의 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-189">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="1d3e8-190">이 기본 전송입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-190">This is the default transport.</span></span> <span data-ttu-id="1d3e8-191">전달 하려면이 작업에 `Start` 메서드에 아무 것도 전달 하지 않고 것과 동일한 효과가 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="1d3e8-191">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="1d3e8-192">브라우저에만 사용 되므로 ForeverFrame 전송이이 목록에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-192">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="1d3e8-193">서버 코드에서 전송 메서드를 확인 하는 방법에 대 한 정보를 참조 하세요 [ASP.NET SignalR 허브 API 가이드-서버-컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법을](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-193">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="1d3e8-194">전송 및 대체에 대 한 자세한 내용은 참조 하세요. [SignalR-전송 및 대체 소개](../getting-started/introduction-to-signalr.md#transports)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-194">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="1d3e8-195">HTTP 헤더를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-195">How to specify HTTP headers</span></span>

<span data-ttu-id="1d3e8-196">HTTP 헤더를 설정 하려면 사용 된 `Headers` 연결 개체의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-196">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="1d3e8-197">다음 예제에서는 HTTP 헤더를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-197">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="1d3e8-198">클라이언트 인증서를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-198">How to specify client certificates</span></span>

<span data-ttu-id="1d3e8-199">클라이언트 인증서를 추가 하려면 사용 된 `AddClientCertificate` 연결 개체에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-199">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="1d3e8-200">허브 프록시를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-200">How to create the Hub proxy</span></span>

<span data-ttu-id="1d3e8-201">허브를 서버에서 호출할 수 있는 클라이언트에서 메서드를 정의 하기 위해 및 서버에서 허브에서 메서드를 호출할 호출 하 여 허브에 대 한 프록시를 만들 `CreateHubProxy` 연결 개체에서.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-201">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="1d3e8-202">문자열에 전달할 `CreateHubProxy` 허브 클래스의 이름 또는 지정 된 이름을 `HubName` 서버에서 사용 된 경우 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-202">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="1d3e8-203">이름 일치는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-203">Name matching is case-insensitive.</span></span>

<span data-ttu-id="1d3e8-204">**서버의 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-204">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="1d3e8-205">**허브 클래스에 대 한 클라이언트 프록시 생성**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-205">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

<span data-ttu-id="1d3e8-206">사용 하 여 허브 클래스를 데코 레이트 하는 경우는 `HubName` 특성에 해당 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-206">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="1d3e8-207">**서버의 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-207">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="1d3e8-208">**허브 클래스에 대 한 클라이언트 프록시 생성**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-208">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

<span data-ttu-id="1d3e8-209">프록시 개체는 스레드로부터 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-209">The proxy object is thread-safe.</span></span> <span data-ttu-id="1d3e8-210">사실 호출 하는 경우 `HubConnection.CreateHubProxy` 여러 번 사용 하 여 동일한 `hubName`, 이와 같은 캐시 `IHubProxy` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-210">In fact, if you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="1d3e8-211">서버를 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-211">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="1d3e8-212">서버를 호출할 수 있는 메서드를 정의 하려면 프록시를 사용 하 여 `On` 이벤트 처리기를 등록 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-212">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="1d3e8-213">메서드 이름 일치는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-213">Method name matching is case-insensitive.</span></span> <span data-ttu-id="1d3e8-214">예를 들어 `Clients.All.UpdateStockPrice` 서버에서 실행 됩니다 `updateStockPrice`를 `updatestockprice`, 또는 `UpdateStockPrice` 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-214">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="1d3e8-215">여러 클라이언트 플랫폼에는 UI를 업데이트 하려면 메서드 코드를 작성 하는 방법에 대 한 다른 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-215">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="1d3e8-216">WinRT (Windows 스토어.NET) 클라이언트에 대 한 예로 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-216">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="1d3e8-217">WPF, Silverlight 및 콘솔 응용 프로그램 예제에 나와 [이 항목의 뒷부분에 나오는 별도 섹션](#wpfsl)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-217">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="1d3e8-218">매개 변수 없이 메서드</span><span class="sxs-lookup"><span data-stu-id="1d3e8-218">Methods without parameters</span></span>

<span data-ttu-id="1d3e8-219">비 제네릭 오버 로드를 사용 하 여 처리 하는 메서드 매개 변수가 없으면는 `On` 메서드:</span><span class="sxs-lookup"><span data-stu-id="1d3e8-219">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="1d3e8-220">**매개 변수 없이 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-220">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="1d3e8-221">**매개 변수 없이 서버에서 호출 메서드에 대 한 WinRT 클라이언트 코드 ([이 항목 뒷부분의 예제를 WPF와 Silverlight 참조](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-221">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="1d3e8-222">형식 매개 변수를 지정 하는 매개 변수를 사용 하 여 메서드</span><span class="sxs-lookup"><span data-stu-id="1d3e8-222">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="1d3e8-223">처리 하는 메서드 매개 변수가 매개 변수의 형식을 제네릭 형식으로 지정 된 `On` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-223">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="1d3e8-224">제네릭 오버 로드가 있습니다를 `On` 메서드를 사용 하면 최대 8 개의 매개 변수 (Windows Phone 7에서 4)을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-224">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="1d3e8-225">다음 예제에서는 매개 변수 하나에 전송 됩니다는 `UpdateStockPrice` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-225">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="1d3e8-226">**매개 변수를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-226">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="1d3e8-227">**매개 변수에 대해 사용 되는 Stock 클래스**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-227">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="1d3e8-228">**매개 변수를 사용 하 여 서버에서 호출 메서드에 대 한 WinRT 클라이언트 코드 ([이 항목 뒷부분의 예제를 WPF와 Silverlight 참조](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-228">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="1d3e8-229">매개 변수에 대해 동적 개체를 지정 하는 매개 변수를 사용 하 여 메서드</span><span class="sxs-lookup"><span data-stu-id="1d3e8-229">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="1d3e8-230">제네릭 형식으로 매개 변수를 지정 하는 대 안으로 `On` 메서드를 동적 개체로 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-230">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="1d3e8-231">**매개 변수를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-231">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="1d3e8-232">**매개 변수에 대해 사용 되는 Stock 클래스**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-232">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="1d3e8-233">**동적 개체를 사용 하 여 매개 변수는 매개 변수를 사용 하 여 서버에서 호출 메서드에 대 한 WinRT 클라이언트 코드 ([이 항목 뒷부분의 예제를 WPF와 Silverlight 참조](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-233">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="1d3e8-234">처리기를 제거 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-234">How to remove a handler</span></span>

<span data-ttu-id="1d3e8-235">호출 처리기를 제거 하려면 해당 `Dispose` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-235">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="1d3e8-236">**서버에서 호출 된 메서드에 대 한 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-236">**Client code for a method called from server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="1d3e8-237">**클라이언트 코드 처리기를 제거 하려면**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-237">**Client code to remove the handler**</span></span>

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="1d3e8-238">클라이언트에서 서버 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-238">How to call server methods from the client</span></span>

<span data-ttu-id="1d3e8-239">서버에서 메서드를 호출 하려면 사용는 `Invoke` 허브 프록시 메서드.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-239">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="1d3e8-240">서버 메서드가 반환 값이 없는 경우의 비 제네릭 오버 로드를 사용 합니다 `Invoke` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-240">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="1d3e8-241">**반환 값이 없는 메서드에 대 한 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-241">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="1d3e8-242">**반환 값이 없는 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-242">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="1d3e8-243">서버 메서드 반환 값이 있으면 반환 형식을 제네릭 형식으로 지정 된 `Invoke` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-243">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="1d3e8-244">**반환 값 및 복합 형식 매개 변수를 사용 하는 메서드에 대 한 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-244">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="1d3e8-245">**매개 변수 및 반환 값에 사용 되는 Stock 클래스**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-245">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="1d3e8-246">**반환 값을 포함 하 고 ASP.NET 4.5 비동기 메서드를 복합 형식 매개 변수를 사용 하는 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-246">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="1d3e8-247">**반환 값을 포함 하 고 동기 메서드를 복합 형식 매개 변수를 사용 하는 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-247">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="1d3e8-248">합니다 `Invoke` 비동기적으로 실행 하 고 반환 하는 메서드를 `Task` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-248">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="1d3e8-249">지정 하지 않으면 `await` 또는 `.Wait()`를 호출 하는 메서드 실행이 완료 되기 전에 코드의 다음 줄이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-249">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="1d3e8-250">연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-250">How to handle connection lifetime events</span></span>

<span data-ttu-id="1d3e8-251">SignalR 처리할 수 있는 수명 이벤트 다음 연결을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-251">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="1d3e8-252">`Received`: 연결에서 모든 데이터를 수신할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-252">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="1d3e8-253">수신된 된 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-253">Provides the received data.</span></span>
- <span data-ttu-id="1d3e8-254">`ConnectionSlow`: 클라이언트 느리거나 자주 삭제 연결을 검색 하는 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-254">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="1d3e8-255">`Reconnecting`: 기본 전송 다시 시작 될 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-255">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="1d3e8-256">`Reconnected`: 기본 전송에 다시 연결 되 면 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-256">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="1d3e8-257">`StateChanged`: 연결 상태가 변경 될 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-257">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="1d3e8-258">이전 상태 및 새 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-258">Provides the old state and the new state.</span></span> <span data-ttu-id="1d3e8-259">연결에 대 한 상태 값에 대해서 [ConnectionState 열거형](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-259">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="1d3e8-260">`Closed`: 연결이 끊어지면 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-260">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="1d3e8-261">예를 들어, 심각한 되지 않지만 간헐적인 연결 문제가 발생 하는 오류에 대 한 경고 메시지를 표시 하려는 경우 속도 저하 또는 자주 등 연결의 삭제를 처리 합니다 `ConnectionSlow` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-261">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="1d3e8-262">자세한 내용은 [이해 및 SignalR의 연결 수명 이벤트 처리](../guide-to-the-api/handling-connection-lifetime-events.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-262">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="1d3e8-263">오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-263">How to handle errors</span></span>

<span data-ttu-id="1d3e8-264">서버에 대 한 자세한 오류 메시지를 명시적으로 사용 하지 않는 경우 SignalR 오류가 발생 한 후 반환 하는 예외 개체는 오류에 대 한 최소한의 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-264">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="1d3e8-265">예를 들어, 호출 하는 경우 `newContosoChatMessage` 실패 하면 오류 개체에 오류 메시지에 "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" 프로덕션에서 클라이언트에 자세한 오류 메시지에 대 한 자세한 오류 메시지를 사용 하도록 설정 하려는 경우 있지만 보안상의 이유로 적합 하지 않습니다 보내기 문제 해결을 위해 서버에서 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-265">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="1d3e8-266">SignalR에서 발생 하는 오류를 처리 하려면에 대 한 처리기를 추가할 수 있습니다는 `Error` 연결 개체의 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-266">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="1d3e8-267">메서드 호출에서 오류를 처리 하려면 try / catch 블록에서 코드를 래핑하십시오.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-267">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="1d3e8-268">클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d3e8-268">How to enable client-side logging</span></span>

<span data-ttu-id="1d3e8-269">클라이언트 쪽 로깅을 사용 하려면 다음을 설정 합니다 `TraceLevel` 및 `TraceWriter` 연결 개체의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-269">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="1d3e8-270">WPF, Silverlight 및 콘솔 응용 프로그램 서버를 호출할 수 있는 클라이언트 방법에 대 한 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="1d3e8-270">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="1d3e8-271">코드 샘플에서는 이전 서버를 호출할 수 있는 클라이언트 메서드를 정의 하는 것에 대 한 WinRT 클라이언트에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-271">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="1d3e8-272">다음 샘플에서는 WPF, Silverlight 및 콘솔 응용 프로그램 클라이언트에 해당 하는 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d3e8-272">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="1d3e8-273">매개 변수 없이 메서드</span><span class="sxs-lookup"><span data-stu-id="1d3e8-273">Methods without parameters</span></span>

<span data-ttu-id="1d3e8-274">**WPF 클라이언트 코드에서 서버 매개 변수 없이 호출 된 메서드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-274">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="1d3e8-275">**Silverlight 클라이언트 코드에서 서버 매개 변수 없이 호출 된 메서드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-275">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="1d3e8-276">**메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드에서 서버 매개 변수 없이 호출**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-276">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="1d3e8-277">형식 매개 변수를 지정 하는 매개 변수를 사용 하 여 메서드</span><span class="sxs-lookup"><span data-stu-id="1d3e8-277">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="1d3e8-278">**WPF 클라이언트 코드는 매개 변수를 사용 하 여 서버에서 호출 된 메서드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-278">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="1d3e8-279">**Silverlight 클라이언트 코드는 매개 변수를 사용 하 여 서버에서 호출 된 메서드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-279">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="1d3e8-280">**메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드는 매개 변수를 사용 하 여 서버에서 호출**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-280">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="1d3e8-281">매개 변수에 대해 동적 개체를 지정 하는 매개 변수를 사용 하 여 메서드</span><span class="sxs-lookup"><span data-stu-id="1d3e8-281">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="1d3e8-282">**동적 개체를 사용 하 여 매개 변수는 매개 변수를 사용 하 여 서버에서 호출 된 메서드에 대 한 WPF 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-282">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="1d3e8-283">**Silverlight 클라이언트 코드는 동적 개체를 사용 하 여 매개 변수에 대해 매개 변수를 사용 하 여 서버에서 호출 된 메서드**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-283">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="1d3e8-284">**동적 개체를 사용 하 여 매개 변수는 매개 변수를 사용 하 여 서버에서 메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드 호출**</span><span class="sxs-lookup"><span data-stu-id="1d3e8-284">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
