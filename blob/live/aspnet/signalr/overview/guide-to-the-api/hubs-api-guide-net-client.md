---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: "ASP.NET SignalR 허브 API 가이드-.NET 클라이언트 (C#) | Microsoft Docs"
author: pfletcher
description: "이 문서에서는 허브 API를 사용 하 여 버전 2, WPF, Silverlight, 및 단점을 Windows 스토어 (WinRT) 등의.NET 클라이언트에서 SignalR에 대 한 소개를 제공..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: a03c8c42622a768d706acf5ac1f23b37a830d426
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="13447-103">ASP.NET SignalR 허브 API 가이드-.NET 클라이언트 (C#)</span><span class="sxs-lookup"><span data-stu-id="13447-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>
====================
<span data-ttu-id="13447-104">여 [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="13447-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="13447-105">이 문서에서는 허브 API를 사용 하 여 SignalR 버전 2에서 Windows 스토어 (WinRT), WPF, Silverlight 및 콘솔 응용 프로그램 등의.NET 클라이언트에 대 한 소개를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-105">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
> 
> <span data-ttu-id="13447-106">SignalR 허브 API를 사용 하면 클라이언트가 서버와 연결 된 클라이언트에는 서버에서 원격 프로시저 호출 (Rpc)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="13447-107">서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="13447-108">클라이언트 코드에서 서버에서 호출 될 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="13447-109">SignalR은 클라이언트와 서버 작업을 처리의 모든 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="13447-110">또한 SignalR 영구 연결을 호출 하는 하위 수준 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="13447-111">SignalR, 허브 및 영구 연결에 대 한 소개 또는 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서에 대 한 참조 [SignalR-시작](../getting-started/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="13447-112">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="13447-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="13447-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="13447-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="13447-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="13447-114">.NET 4.5</span></span>
> - <span data-ttu-id="13447-115">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="13447-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="13447-116">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="13447-116">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="13447-117">이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="13447-118">질문이 나 의견이</span><span class="sxs-lookup"><span data-stu-id="13447-118">Questions and comments</span></span>
> 
> <span data-ttu-id="13447-119">이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="13447-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="13447-120">자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="13447-121">개요</span><span class="sxs-lookup"><span data-stu-id="13447-121">Overview</span></span>

<span data-ttu-id="13447-122">이 문서는 다음 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="13447-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="13447-123">클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="13447-123">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="13447-124">연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-124">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="13447-125">Silverlight 클라이언트에서 도메인 간 연결</span><span class="sxs-lookup"><span data-stu-id="13447-125">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="13447-126">연결을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-126">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="13447-127">WPF 클라이언트의 최대 동시 연결 수를 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-127">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="13447-128">쿼리 문자열 매개 변수를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-128">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="13447-129">전송 메서드를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-129">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="13447-130">HTTP 헤더를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-130">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="13447-131">클라이언트 인증서를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-131">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="13447-132">허브 프록시를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-132">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="13447-133">서버를 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-133">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="13447-134">매개 변수 없이 메서드</span><span class="sxs-lookup"><span data-stu-id="13447-134">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="13447-135">매개 변수를 매개 변수 형식 지정 메서드</span><span class="sxs-lookup"><span data-stu-id="13447-135">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="13447-136">매개 변수를 매개 변수에 대해 동적 개체를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-136">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="13447-137">처리기를 제거 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-137">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="13447-138">클라이언트에서 서버 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-138">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="13447-139">연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-139">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="13447-140">오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-140">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="13447-141">클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-141">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="13447-142">WPF, Silverlight 및 서버를 호출할 수 있는 클라이언트 메서드에 대 한 콘솔 응용 프로그램 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="13447-142">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="13447-143">샘플.NET 클라이언트 프로젝트에 대 한 다음 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-143">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="13447-144">[길동 armenta / SignalR 샘플](https://github.com/gustavo-armenta/SignalR-Samples) GitHub.com (WinRT, Silverlight, 콘솔 응용 프로그램 예제)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-144">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="13447-145">[DamianEdwards / SignalR MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) GitHub.com (WPF 예제)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-145">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="13447-146">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) GitHub.com (콘솔 응용 프로그램 예제)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-146">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="13447-147">프로그래밍 하는 방법에 대 한 설명서는 서버 또는 JavaScript 클라이언트는 다음 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-147">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="13447-148">SignalR 허브 API 가이드-서버</span><span class="sxs-lookup"><span data-stu-id="13447-148">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="13447-149">SignalR 허브 API 가이드-JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="13447-149">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="13447-150">API 참조 항목의 링크를.NET 4.5 버전의 API 되도록합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-150">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="13447-151">.NET 4를 사용 하 여 참조 [.NET 4 버전의 API 항목](https://msdn.microsoft.com/en-us/library/jj891075(v=vs.100).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-151">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/en-us/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="13447-152">클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="13447-152">Client setup</span></span>

<span data-ttu-id="13447-153">설치는 [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet 패키지 (하지는 [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) 패키지).</span><span class="sxs-lookup"><span data-stu-id="13447-153">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="13447-154">이 패키지는.NET 4.5와.NET 4에 대 한 WinRT, Silverlight, WPF, 콘솔 응용 프로그램 및 Windows Phone 클라이언트를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-154">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="13447-155">SignalR 클라이언트에가지고 있는 버전이 서버에 있는 버전과 일치 하는 경우에 SignalR에서 차이 수 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-155">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="13447-156">예를 들어 SignalR 버전 2 실행 하는 서버는 클라이언트 버전 2가 설치 되어 있는 뿐만 아니라 1.1.x 설치 되어 있는 클라이언트를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-156">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="13447-157">클라이언트 버전과 서버 버전 간의 차이점은 너무 클 경우 또는 SignalR throw 클라이언트가 서버 보다 최신인 경우는 `InvalidOperationException` 클라이언트 연결을 설정 하려고 시도 하는 동안 예외가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-157">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="13447-158">오류 메시지는 "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`"입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-158">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="13447-159">연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-159">How to establish a connection</span></span>

<span data-ttu-id="13447-160">연결을 설정할 수 있습니다, 전에 만들어야 할 한 `HubConnection` 개체 및 프록시 만들기.</span><span class="sxs-lookup"><span data-stu-id="13447-160">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="13447-161">연결을 설정 하려면 호출는 `Start` 에서 메서드는 `HubConnection` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-161">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> <span data-ttu-id="13447-162">JavaScript 클라이언트에 대 한 호출 하기 전에 하나 이상의 이벤트 처리기를 등록 해야는 `Start` 메서드 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-162">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="13447-163">.NET 클라이언트 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-163">This is not necessary for .NET clients.</span></span> <span data-ttu-id="13447-164">JavaScript 클라이언트에 대 한 생성된 된 프록시 코드 자동으로 존재 하는 모든 허브에 대 한 프록시 서버에서 만들어지고 있는 허브를 표시 하는 방법에 처리기를 등록 하는 중에 클라이언트를 사용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-164">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="13447-165">하지만.NET 클라이언트에 대 한 만들면 허브 프록시를 수동으로 SignalR을 사용 하려는 모든 허브에 대 한 프록시는 가정.</span><span class="sxs-lookup"><span data-stu-id="13447-165">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>


<span data-ttu-id="13447-166">기본값을 사용 하 여 샘플 코드는 "/ signalr" SignalR 서비스에 연결 하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-166">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="13447-167">다른 기본 URL을 지정 하는 방법에 대 한 정보를 참조 하십시오. [ASP.NET SignalR 허브 API 가이드-서버-/signalr URL](hubs-api-guide-server.md#signalrurl)합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-167">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="13447-168">`Start` 메서드가 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-168">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="13447-169">을 코드 줄에는 연결이 설정 된 후 될 때까지 실행 하지 않습니다 확인 하기 위해 사용 하 여 `await` ASP.NET 4.5 비동기 메서드에서 또는 `.Wait()` 에 동기 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-169">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="13447-170">사용 하지 않는 `.Wait()` WinRT 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="13447-170">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="13447-171">Silverlight 클라이언트에서 도메인 간 연결</span><span class="sxs-lookup"><span data-stu-id="13447-171">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="13447-172">Silverlight 클라이언트에서 도메인 간 연결을 설정 하는 방법에 대 한 정보를 참조 하십시오. [하는 서비스 사용 가능한 도메인 경계를 넘어](https://msdn.microsoft.com/en-us/library/cc197955(v=vs.95).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-172">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/en-us/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="13447-173">연결을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-173">How to configure the connection</span></span>

<span data-ttu-id="13447-174">연결을 설정 하기 전에 다음 옵션 중 하나를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-174">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="13447-175">동시 연결 수가 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13447-175">Concurrent connections limit.</span></span>
- <span data-ttu-id="13447-176">쿼리 문자열 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-176">Query string parameters.</span></span>
- <span data-ttu-id="13447-177">전송 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-177">The transport method.</span></span>
- <span data-ttu-id="13447-178">HTTP 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-178">HTTP headers.</span></span>
- <span data-ttu-id="13447-179">클라이언트 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-179">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="13447-180">WPF 클라이언트의 최대 동시 연결 수를 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-180">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="13447-181">WPF 클라이언트 2의 값이 기본값에서 동시 연결의 최대 수를 증가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-181">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="13447-182">권장 되는 값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-182">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

<span data-ttu-id="13447-183">자세한 내용은 참조 [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/en-us/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-183">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/en-us/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="13447-184">쿼리 문자열 매개 변수를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-184">How to specify query string parameters</span></span>

<span data-ttu-id="13447-185">클라이언트가 연결할 때 서버에 데이터를 전송 하려는 경우에 연결 개체에 쿼리 문자열 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-185">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="13447-186">다음 예제에서는 클라이언트 코드에서 쿼리 문자열 매개 변수를 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="13447-186">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="13447-187">다음 예제에는 서버 코드에서 쿼리 문자열 매개 변수를 읽는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="13447-187">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="13447-188">전송 메서드를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-188">How to specify the transport method</span></span>

<span data-ttu-id="13447-189">연결 하는 과정의 일환으로, SignalR 클라이언트는 일반적으로 서버와 클라이언트 모두에서 지원 되는 가장 좋은 전송을 결정할 서버와 협상 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-189">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="13447-190">어떤 전송을 사용 하려는 이미 알고 있는 경우이 협상 프로세스를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-190">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="13447-191">전송 메서드를 지정 하려면 Start 메서드를 전송 개체에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-191">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="13447-192">다음 예제에서는 클라이언트 코드에서 전송 방법을 지정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="13447-192">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

<span data-ttu-id="13447-193">[Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/en-us/library/jj918090(v=vs.111).aspx) 네임 스페이스는 전송을 지정 하는 데 사용할 수 있는 다음과 같은 클래스가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13447-193">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/en-us/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="13447-194">[LongPollingTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="13447-194">[LongPollingTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="13447-195">[ServerSentEventsTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="13447-195">[ServerSentEventsTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="13447-196">[WebSocketTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (사용 가능 서버와 클라이언트 모두.NET 4.5를 사용 하는 경우에 합니다.)</span><span class="sxs-lookup"><span data-stu-id="13447-196">[WebSocketTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="13447-197">[AutoTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (클라이언트와 서버 모두에서 지 원하는 최상의 전송에서 자동으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-197">[AutoTransport](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="13447-198">이 기본 전송입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-198">This is the default transport.</span></span> <span data-ttu-id="13447-199">전달 하려면이 작업에 `Start` 메서드는 모든 항목에 전달 하지 않을 것과 같습니다.)</span><span class="sxs-lookup"><span data-stu-id="13447-199">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="13447-200">ForeverFrame 전송 브라우저에만 사용 되기 때문에이 목록에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-200">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="13447-201">서버 코드에서 전송 방법을 확인 하는 방법에 대 한 정보를 참조 하십시오. [ASP.NET SignalR 허브 API 가이드-서버-컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법](hubs-api-guide-server.md#contextproperty)합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-201">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="13447-202">전송 및 대체 하는 방법에 대 한 자세한 내용은 참조 [SignalR-전송 및 대체 소개](../getting-started/introduction-to-signalr.md#transports)합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-202">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="13447-203">HTTP 헤더를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-203">How to specify HTTP headers</span></span>

<span data-ttu-id="13447-204">HTTP 헤더를 설정 하려면 사용 하 여는 `Headers` connection 개체의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-204">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="13447-205">다음 예제에서는 HTTP 헤더를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="13447-205">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="13447-206">클라이언트 인증서를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-206">How to specify client certificates</span></span>

<span data-ttu-id="13447-207">클라이언트 인증서를 추가 하려면 사용 된 `AddClientCertificate` 연결 개체에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="13447-207">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="13447-208">허브 프록시를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-208">How to create the Hub proxy</span></span>

<span data-ttu-id="13447-209">허브의 서버에서 호출할 수 있는 클라이언트에서 메서드를 정의 하기 위해 하 고 서버에서 허브에 대 한 메서드를 호출할 허브에 대 한 프록시 호출 하 여 만듭니다 `CreateHubProxy` 연결 개체에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-209">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="13447-210">문자열에 전달할 있습니다 `CreateHubProxy` 지정 하는 이름 또는 허브 클래스의 이름을 `HubName` 특성 경우 서버에서 사용 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-210">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="13447-211">이름 일치는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-211">Name matching is case-insensitive.</span></span>

<span data-ttu-id="13447-212">**서버 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="13447-212">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="13447-213">**허브 클래스에 대 한 클라이언트 프록시 만들기**</span><span class="sxs-lookup"><span data-stu-id="13447-213">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

<span data-ttu-id="13447-214">하면 허브 클래스를 추가 하는 경우는 `HubName` 특성에서 해당 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-214">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="13447-215">**서버 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="13447-215">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="13447-216">**허브 클래스에 대 한 클라이언트 프록시 만들기**</span><span class="sxs-lookup"><span data-stu-id="13447-216">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

<span data-ttu-id="13447-217">호출 하는 경우 `HubConnection.CreateHubProxy` 으로 여러 번 동일한 `hubName`, 캐시 같은 `IHubProxy` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-217">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="13447-218">서버를 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-218">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="13447-219">프록시를 사용 하 여 서버를 호출할 수 있는 메서드를 정의 하려면 `On` 메서드를 이벤트 처리기를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-219">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="13447-220">메서드 이름 일치는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-220">Method name matching is case-insensitive.</span></span> <span data-ttu-id="13447-221">예를 들어 `Clients.All.UpdateStockPrice` 서버에서 실행 됩니다 `updateStockPrice`, `updatestockprice`, 또는 `UpdateStockPrice` 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="13447-221">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="13447-222">다른 클라이언트 플랫폼에는 UI를 업데이트 하 메서드 코드를 작성 하는 방법에 대 한 다른 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-222">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="13447-223">WinRT (Windows 스토어.NET) 클라이언트에 대 한 예제 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13447-223">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="13447-224">WPF, Silverlight, 및 콘솔 응용 프로그램 예제에 제공 됩니다 [이 항목의 뒷부분에 나오는 별도 섹션](#wpfsl)합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-224">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="13447-225">매개 변수 없이 메서드</span><span class="sxs-lookup"><span data-stu-id="13447-225">Methods without parameters</span></span>

<span data-ttu-id="13447-226">처리 하는 방법에는 매개 변수가의 비 제네릭 오버 로드를 사용는 `On` 메서드:</span><span class="sxs-lookup"><span data-stu-id="13447-226">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="13447-227">**매개 변수 없이 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="13447-227">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="13447-228">**매개 변수 없이 서버에서 WinRT 클라이언트 코드에 대 한 메서드 호출 ([이 항목 뒷부분의 예제를 WPF 및 Silverlight 참조](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="13447-228">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="13447-229">매개 변수를 매개 변수 형식 지정 메서드</span><span class="sxs-lookup"><span data-stu-id="13447-229">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="13447-230">처리 하는 메서드 매개 변수가 있으면 변수의 제네릭 형식 매개 변수 형식 지정은 `On` 메서드.</span><span class="sxs-lookup"><span data-stu-id="13447-230">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="13447-231">제네릭 오버 로드는는 `On` 메서드 최대 8 (Windows Phone 7에서 4) 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-231">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="13447-232">다음 예제에서는 매개 변수 하나에 전달 되어는 `UpdateStockPrice` 메서드.</span><span class="sxs-lookup"><span data-stu-id="13447-232">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="13447-233">**매개 변수가 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="13447-233">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="13447-234">**매개 변수에 대해 사용 되는 Stock 클래스**</span><span class="sxs-lookup"><span data-stu-id="13447-234">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="13447-235">**WinRT 클라이언트 코드는 메서드에 대 한 매개 변수를 사용 하는 서버에서 호출 ([이 항목 뒷부분의 예제를 WPF 및 Silverlight 참조](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="13447-235">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="13447-236">매개 변수를 매개 변수에 대해 동적 개체를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-236">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="13447-237">제네릭 형식으로 매개 변수를 지정 하는 대신는 `On` 메서드를 동적 개체로 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-237">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="13447-238">**매개 변수가 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="13447-238">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="13447-239">**매개 변수에 대해 사용 되는 Stock 클래스**</span><span class="sxs-lookup"><span data-stu-id="13447-239">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="13447-240">**동적 개체를 사용 하 여 매개 변수에 대해 매개 변수를 사용 하는 서버에서 WinRT 클라이언트 코드는 메서드에 대 한 호출 ([이 항목 뒷부분의 예제를 WPF 및 Silverlight 참조](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="13447-240">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="13447-241">처리기를 제거 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-241">How to remove a handler</span></span>

<span data-ttu-id="13447-242">처리기를 제거 하려면 해당 `Dispose` 메서드.</span><span class="sxs-lookup"><span data-stu-id="13447-242">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="13447-243">**서버에서 호출 된 메서드에 대 한 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="13447-243">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="13447-244">**처리기를 제거 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="13447-244">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="13447-245">클라이언트에서 서버 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-245">How to call server methods from the client</span></span>

<span data-ttu-id="13447-246">메서드를 호출 하는 서버를 사용 하 여는 `Invoke` 허브 프록시에 대 한 메서드.</span><span class="sxs-lookup"><span data-stu-id="13447-246">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="13447-247">비 제네릭 오버 로드를 사용 하 여 서버 메서드 반환 값이 없는 경우는 `Invoke` 메서드.</span><span class="sxs-lookup"><span data-stu-id="13447-247">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="13447-248">**반환 값이 없는 메서드에 대 한 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="13447-248">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="13447-249">**반환 값이 없는 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="13447-249">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="13447-250">서버 메서드 반환 값이 있으면의 제네릭 형식으로 반환 형식을 지정 된 `Invoke` 메서드.</span><span class="sxs-lookup"><span data-stu-id="13447-250">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="13447-251">**반환 값이 있는 복합 형식 매개 변수를 사용 하는 메서드에 대 한 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="13447-251">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="13447-252">**매개 변수 및 반환 값에 대 한 사용 되는 Stock 클래스**</span><span class="sxs-lookup"><span data-stu-id="13447-252">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="13447-253">**반환 값을 ASP.NET 4.5 비동기 메서드에서 복합 유형 매개 변수를 사용 하는 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="13447-253">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="13447-254">**반환 값을 포함 하 고 동기 메서드를 복합 형식 매개 변수를 사용 하는 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="13447-254">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="13447-255">`Invoke` 비동기적으로 실행 하 고 반환 하는 메서드는 `Task` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-255">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="13447-256">지정 하지 않으면 `await` 또는 `.Wait()`, 코드의 다음 줄은 호출 하는 메서드 실행을 완료 하기 전에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13447-256">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="13447-257">연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-257">How to handle connection lifetime events</span></span>

<span data-ttu-id="13447-258">SignalR 다음 연결을 처리할 수 있는 수명 이벤트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-258">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="13447-259">`Received`: 연결에서 모든 데이터를 수신할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-259">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="13447-260">수신된 된 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-260">Provides the received data.</span></span>
- <span data-ttu-id="13447-261">`ConnectionSlow`: 클라이언트 느리거나 자주 삭제 연결을 검색 하는 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-261">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="13447-262">`Reconnecting`: 기본 전송 다시 시작 될 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-262">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="13447-263">`Reconnected`: 기본 전송에 다시 연결 되 면 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-263">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="13447-264">`StateChanged`: 연결 상태가 변경 될 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-264">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="13447-265">이전 상태와 새 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-265">Provides the old state and the new state.</span></span> <span data-ttu-id="13447-266">연결에 대 한 정보에 대 한 상태 값 참조 [ConnectionState 열거형](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-266">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="13447-267">`Closed`: 연결을 끊을 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-267">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="13447-268">예를 들어 심각한 되지 않으며 간헐적인 연결 문제가 발생 하는 오류에 대 한 경고 메시지를 표시 하려는 경우 속도 저하가 또는 자주 등의 연결을 삭제 하는 중 처리 된 `ConnectionSlow` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-268">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="13447-269">자세한 내용은 참조 [이해 하 고 SignalR에서 연결 수명 이벤트를 처리](handling-connection-lifetime-events.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-269">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="13447-270">오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-270">How to handle errors</span></span>

<span data-ttu-id="13447-271">서버에 대 한 자세한 오류 메시지를 명시적으로 활성화 하지 않는 경우 오류가 발생 한 후 SignalR 반환 하는 예외 개체는 오류에 대 한 최소한의 정보만을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-271">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="13447-272">예를 들어, 호출 하는 경우 `newContosoChatMessage` 실패, 오류 개체에서 오류 메시지에 "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" 보내는 프로덕션의 클라이언트에 자세한 오류 메시지에 대 한 자세한 오류 메시지를 사용 하도록 설정 하려면 보안상의 이유로 적합 하지 않습니다 문제 해결을 위해 서버에서 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-272">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="13447-273">SignalR에서 발생 시키는 오류를 처리 하려면에 대 한 처리기를 추가할 수 있습니다는 `Error` connection 개체의 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-273">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="13447-274">이 메서드 호출에서 오류를 처리 하려면 try / catch 블록의 코드를 래핑하십시오.</span><span class="sxs-lookup"><span data-stu-id="13447-274">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="13447-275">클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-275">How to enable client-side logging</span></span>

<span data-ttu-id="13447-276">클라이언트 쪽 로깅을 사용 하려면 설정는 `TraceLevel` 및 `TraceWriter` connection 개체의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="13447-276">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="13447-277">WPF, Silverlight 및 서버를 호출할 수 있는 클라이언트 메서드에 대 한 콘솔 응용 프로그램 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="13447-277">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="13447-278">서버를 호출할 수 있는 클라이언트 메서드를 정의 앞에 표시 된 코드 샘플 WinRT 클라이언트에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="13447-278">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="13447-279">다음 예에서는 WPF, Silverlight 및 콘솔 응용 프로그램 클라이언트에 대 한 해당 하는 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="13447-279">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="13447-280">매개 변수 없이 메서드</span><span class="sxs-lookup"><span data-stu-id="13447-280">Methods without parameters</span></span>

<span data-ttu-id="13447-281">**매개 변수 없이 서버에서 호출 하는 방법에 대 한 WPF 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="13447-281">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="13447-282">**매개 변수 없이 서버에서 Silverlight 클라이언트 코드에 대 한 메서드 호출**</span><span class="sxs-lookup"><span data-stu-id="13447-282">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="13447-283">**매개 변수 없이 서버에서 메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드 호출**</span><span class="sxs-lookup"><span data-stu-id="13447-283">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="13447-284">매개 변수를 매개 변수 형식 지정 메서드</span><span class="sxs-lookup"><span data-stu-id="13447-284">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="13447-285">**매개 변수를 사용 하는 서버에서 호출 된 메서드에 대 한 WPF 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="13447-285">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="13447-286">**Silverlight 클라이언트 코드에 대 한 매개 변수를 사용 하는 서버에서 호출 된 메서드**</span><span class="sxs-lookup"><span data-stu-id="13447-286">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="13447-287">**콘솔 응용 프로그램 클라이언트 코드는 메서드에 대 한 매개 변수를 사용 하는 서버에서 호출**</span><span class="sxs-lookup"><span data-stu-id="13447-287">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="13447-288">매개 변수를 매개 변수에 대해 동적 개체를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="13447-288">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="13447-289">**동적 개체를 사용 하 여 매개 변수에 대해 매개 변수를 사용 하는 서버에서 호출 된 메서드에 대 한 WPF 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="13447-289">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="13447-290">**동적 개체를 사용 하 여 매개 변수에 대해 매개 변수를 사용 하는 서버에서 Silverlight 클라이언트 코드는 메서드에 대 한 호출**</span><span class="sxs-lookup"><span data-stu-id="13447-290">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="13447-291">**메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드는 매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수를 사용 하는 서버에서 호출**</span><span class="sxs-lookup"><span data-stu-id="13447-291">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
