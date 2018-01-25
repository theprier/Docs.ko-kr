---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
title: "ASP.NET SignalR 허브 API 가이드-서버 (SignalR 1.x) | Microsoft Docs"
author: pfletcher
description: "이 문서에서는 코드 샘플 demonstratin와 버전 1.1에서 SignalR에 대 한 ASP.NET SignalR 허브 API의 서버 쪽 프로그래밍에 대 한 소개를 제공..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/17/2013
ms.topic: article
ms.assetid: 03e4b9f5-0fea-4d94-959f-014b2762a301
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: 96155b1c648e5f6092b3ba67a560197f86a593b9
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-signalr-hubs-api-guide---server-signalr-1x"></a><span data-ttu-id="d62d9-103">ASP.NET SignalR 허브 API 가이드-서버 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="d62d9-103">ASP.NET SignalR Hubs API Guide - Server (SignalR 1.x)</span></span>
====================
<span data-ttu-id="d62d9-104">여 [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d62d9-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="d62d9-105">이 문서에서는 일반적인 옵션을 보여 주는 샘플 코드 버전 1.1에서 SignalR에 대 한 ASP.NET SignalR 허브 API의 서버 쪽 프로그래밍에 대 한 소개를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 1.1, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="d62d9-106">SignalR 허브 API를 사용 하면 클라이언트가 서버와 연결 된 클라이언트에는 서버에서 원격 프로시저 호출 (Rpc)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="d62d9-107">서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="d62d9-108">클라이언트 코드에서 서버에서 호출 될 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="d62d9-109">SignalR은 클라이언트와 서버 작업을 처리의 모든 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="d62d9-110">또한 SignalR 영구 연결을 호출 하는 하위 수준 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="d62d9-111">SignalR, 허브 및 영구 연결에 대 한 소개 또는 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서에 대 한 참조 [SignalR-시작](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](index.md).</span></span>


## <a name="overview"></a><span data-ttu-id="d62d9-112">개요</span><span class="sxs-lookup"><span data-stu-id="d62d9-112">Overview</span></span>

<span data-ttu-id="d62d9-113">이 문서는 다음 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="d62d9-114">SignalR 경로 등록 하 고 SignalR 옵션을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-114">How to register the SignalR route and configure SignalR options</span></span>](#route)

    - [<span data-ttu-id="d62d9-115">/Signalr URL</span><span class="sxs-lookup"><span data-stu-id="d62d9-115">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="d62d9-116">SignalR 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="d62d9-116">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="d62d9-117">만들고 허브 클래스를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-117">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="d62d9-118">허브 개체 수명</span><span class="sxs-lookup"><span data-stu-id="d62d9-118">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="d62d9-119">카멜식 대 / 소문자 JavaScript 클라이언트에서 허브 이름</span><span class="sxs-lookup"><span data-stu-id="d62d9-119">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="d62d9-120">여러 허브</span><span class="sxs-lookup"><span data-stu-id="d62d9-120">Multiple Hubs</span></span>](#multiplehubs)
- [<span data-ttu-id="d62d9-121">클라이언트에서 호출할 수 있는 허브 클래스에 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-121">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="d62d9-122">JavaScript 클라이언트에서 메서드 이름의 카멜식 대 / 소문자</span><span class="sxs-lookup"><span data-stu-id="d62d9-122">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="d62d9-123">비동기적으로 실행 하는 경우</span><span class="sxs-lookup"><span data-stu-id="d62d9-123">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="d62d9-124">오버 로드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-124">Defining overloads</span></span>](#overloads)
- [<span data-ttu-id="d62d9-125">허브 클래스에서 클라이언트 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-125">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="d62d9-126">클라이언트를 선택 하는 RPC 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-126">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="d62d9-127">메서드 이름에 대 한 컴파일 시간 유효성</span><span class="sxs-lookup"><span data-stu-id="d62d9-127">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="d62d9-128">일치 하는 대/소문자 구분 메서드 이름</span><span class="sxs-lookup"><span data-stu-id="d62d9-128">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="d62d9-129">비동기 실행</span><span class="sxs-lookup"><span data-stu-id="d62d9-129">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="d62d9-130">허브 클래스에서 그룹 구성원 자격을 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-130">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="d62d9-131">Add 및 Remove 메서드의 비동기 실행</span><span class="sxs-lookup"><span data-stu-id="d62d9-131">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="d62d9-132">그룹 멤버 자격 지 속성</span><span class="sxs-lookup"><span data-stu-id="d62d9-132">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="d62d9-133">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="d62d9-133">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="d62d9-134">허브 클래스에서 연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-134">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="d62d9-135">OnConnected, OnDisconnected, 및 OnReconnected 호출 될 때</span><span class="sxs-lookup"><span data-stu-id="d62d9-135">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="d62d9-136">채워지지 호출자 상태</span><span class="sxs-lookup"><span data-stu-id="d62d9-136">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="d62d9-137">컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-137">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="d62d9-138">클라이언트와 허브 클래스 간의 상태를 전달 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-138">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="d62d9-139">허브 클래스에는 오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-139">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="d62d9-140">클라이언트 메서드를 호출할 허브 클래스 외부에서 그룹을 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-140">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="d62d9-141">클라이언트 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="d62d9-141">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="d62d9-142">그룹 멤버 자격 관리</span><span class="sxs-lookup"><span data-stu-id="d62d9-142">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="d62d9-143">추적을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-143">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="d62d9-144">허브 파이프라인을 사용자 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-144">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="d62d9-145">프로그램 클라이언트 하는 방법에 대 한 설명서를 다음 리소스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d62d9-145">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="d62d9-146">SignalR 허브 API 가이드-JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="d62d9-146">SignalR Hubs API Guide - JavaScript Client</span></span>](index.md)
- [<span data-ttu-id="d62d9-147">SignalR 허브 API 가이드-.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="d62d9-147">SignalR Hubs API Guide - .NET Client</span></span>](index.md)

<span data-ttu-id="d62d9-148">API 참조 항목의 링크를.NET 4.5 버전의 API 되도록합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-148">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="d62d9-149">.NET 4를 사용 하 여 참조 [.NET 4 버전의 API 항목](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-149">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="route"></a>

## <a name="how-to-register-the-signalr-route-and-configure-signalr-options"></a><span data-ttu-id="d62d9-150">SignalR 경로 등록 하 고 SignalR 옵션을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-150">How to register the SignalR route and configure SignalR options</span></span>

<span data-ttu-id="d62d9-151">클라이언트에서 허브에 연결 하는 데 사용 하는 경로 정의 하려면 호출는 [MapHubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) 메서드 응용 프로그램이 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-151">To define the route that clients will use to connect to your Hub, call the [MapHubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="d62d9-152">`MapHubs`이 [확장 메서드](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) 에 대 한는 `System.Web.Routing.RouteCollection` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-152">`MapHubs` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `System.Web.Routing.RouteCollection` class.</span></span> <span data-ttu-id="d62d9-153">다음 예제에서 SignalR 허브 경로 정의 하는 방법을 보여 줍니다는 *Global.asax* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-153">The following example shows how to define the SignalR Hubs route in the *Global.asax* file.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample1.cs)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample2.cs?highlight=5)]

<span data-ttu-id="d62d9-154">ASP.NET MVC 응용 프로그램에 SignalR 기능을 추가 하는 경우 다른 경로 보다 SignalR 경로 추가 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-154">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="d62d9-155">자세한 내용은 참조 [자습서: SignalR 및 MVC 4 시작](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-155">For more information, see [Tutorial: Getting Started with SignalR and MVC 4](index.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="d62d9-156">/Signalr URL</span><span class="sxs-lookup"><span data-stu-id="d62d9-156">The /signalr URL</span></span>

<span data-ttu-id="d62d9-157">기본적으로 클라이언트에서 허브에 연결 하는 데 사용 하는 경로 URL은 "/ signalr"입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-157">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="d62d9-158">(자동으로 생성 된 JavaScript 파일에 "/ signalr/허브" URL로이 URL을 혼동 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d62d9-158">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="d62d9-159">생성 된 프록시에 대 한 자세한 내용은 참조 [SignalR 허브 API 가이드-JavaScript 클라이언트-생성 된 프록시 및 수에 대 한 역할](index.md).)</span><span class="sxs-lookup"><span data-stu-id="d62d9-159">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).)</span></span>

<span data-ttu-id="d62d9-160">SignalR;에 대 한 사용할 수 없음이 기본 URL을 구성 하는 특수 상황 있을 수 있습니다. 예를 들어 이라는 프로젝트에 폴더를 있으면 *signalr* 이름을 변경 하려면.</span><span class="sxs-lookup"><span data-stu-id="d62d9-160">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="d62d9-161">이 경우 다음 예제에 나와 있는 것 처럼 기본 URL을 변경할 수 있습니다 (대체 "/ signalr" 원하는으로 URL 사용 하 여 샘플 코드에서).</span><span class="sxs-lookup"><span data-stu-id="d62d9-161">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="d62d9-162">**URL을 지정 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="d62d9-162">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample3.cs?highlight=1)]

<span data-ttu-id="d62d9-163">**URL (생성 된 프록시)를 지정 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d62d9-163">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="d62d9-164">**(없이 생성 된 프록시) URL을 지정 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d62d9-164">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample5.js?highlight=1)]

<span data-ttu-id="d62d9-165">**URL을 지정 하는.NET 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d62d9-165">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample6.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="d62d9-166">SignalR 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="d62d9-166">Configuring SignalR Options</span></span>

<span data-ttu-id="d62d9-167">오버 로드는 `MapHubs` 메서드를 사용 하는 사용자 지정 URL, 사용자 지정 종속성 확인자, 그리고 다음 옵션을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-167">Overloads of the `MapHubs` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="d62d9-168">브라우저 클라이언트에서 도메인 간 호출을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-168">Enable cross-domain calls from browser clients.</span></span>

    <span data-ttu-id="d62d9-169">일반적으로 브라우저에서 페이지를 로드 하는 경우 `http://contoso.com`, SignalR 연결에 동일한 도메인에는 `http://contoso.com/signalr`합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-169">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="d62d9-170">경우에서 페이지 `http://contoso.com` 에 대 한 연결을 사용 하면 `http://fabrikam.com/signalr`, 도메인 간 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-170">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="d62d9-171">보안상의 이유로 도메인 간 연결이 기본적으로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-171">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="d62d9-172">자세한 내용은 참조 [ASP.NET SignalR 허브 API 가이드-JavaScript 클라이언트-도메인 간 연결을 설정 하는 방법](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-172">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](index.md).</span></span>
- <span data-ttu-id="d62d9-173">자세한 오류 메시지를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-173">Enable detailed error messages.</span></span>

    <span data-ttu-id="d62d9-174">오류가 발생할 때 무슨 상황이 발생 하는 방법에 대 한 세부 정보가 없는 알림 메시지를 클라이언트에 보내는 데 SignalR의 기본 동작은입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-174">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="d62d9-175">프로덕션, 악의적인 사용자가 응용 프로그램에 대 한 공격에 정보를 사용할 수 있습니다 클라이언트에 자세한 오류 정보를 보내 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-175">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="d62d9-176">문제 해결을 위해 일시적으로 더 자세한 오류 보고를 활성화 하려면이 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-176">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="d62d9-177">자동으로 생성 된 JavaScript 프록시 파일을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-177">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="d62d9-178">기본적으로 허브 클래스에 대 한 프록시와 JavaScript 파일은 "/ signalr/허브" URL에 대 한 응답으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-178">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="d62d9-179">JavaScript 프록시를 사용 하지 않음 또는이 파일을 수동으로 생성 하 고 클라이언트의 물리적 파일을 참조 하려는 경우에 프록시 생성을 해제 하려면이 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-179">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="d62d9-180">자세한 내용은 참조 [SignalR 허브 API 가이드-JavaScript 클라이언트는 SignalR에 대 한 실제 파일을 만드는 방법에는 프록시 생성](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-180">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](index.md).</span></span>

<span data-ttu-id="d62d9-181">다음 예제에 대 한 호출에서 SignalR 연결 URL 및 이러한 옵션을 지정 하는 방법을 보여 줍니다는 `MapHubs` 메서드.</span><span class="sxs-lookup"><span data-stu-id="d62d9-181">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapHubs` method.</span></span> <span data-ttu-id="d62d9-182">사용자 지정 URL을 지정 하려면 바꿉니다 "/ signalr"을 사용 하려면 URL로 예제에서입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-182">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample7.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="d62d9-183">만들고 허브 클래스를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-183">How to create and use Hub classes</span></span>

<span data-ttu-id="d62d9-184">허브를 만들려면에서 파생 되는 클래스를 만듭니다 [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-184">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="d62d9-185">다음 예제에서는 채팅 응용 프로그램에 대 한 간단한 허브 클래스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-185">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample8.cs)]

<span data-ttu-id="d62d9-186">이 예제에서는 연결 된 클라이언트가 호출할 수는 `NewContosoChatMessage` 메서드, 및 연결 된 모든 클라이언트에 수신 된 데이터가 브로드캐스트 될 경우.</span><span class="sxs-lookup"><span data-stu-id="d62d9-186">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="d62d9-187">허브 개체 수명</span><span class="sxs-lookup"><span data-stu-id="d62d9-187">Hub object lifetime</span></span>

<span data-ttu-id="d62d9-188">허브 클래스를 인스턴스화하거나; 서버에서 사용자 고유의 코드에서 해당 메서드를 호출 하지 않습니다. SignalR 허브 파이프라인에 의해 수행 되는 모든.</span><span class="sxs-lookup"><span data-stu-id="d62d9-188">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="d62d9-189">SignalR은 클라이언트를 연결, 연결이 끊어진, 또는 서버에 메서드를 호출 하면 때 같은 허브 작업을 처리 해야 할 때마다 허브 클래스의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-189">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="d62d9-190">허브 클래스의 인스턴스는 일시적 이므로 다음에 대 한 메서드 호출에서 상태를 유지 하기 위해 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-190">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="d62d9-191">될 때마다 서버 메서드 호출은 클라이언트에서 수신, 허브 클래스 프로세스의 새 인스턴스는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-191">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="d62d9-192">여러 개의 연결 및 메서드 호출을 통해 상태를 유지 하려면 허브 클래스 또는 다른 클래스에서 파생 되지 않은에 데이터베이스 또는 정적 변수와 같은 다른 방법을 사용 `Hub`합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-192">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="d62d9-193">데이터를 메모리에에서 유지 하는 경우 정적 변수와 같은 메서드를 사용 하 여 허브 클래스에는 데이터는 손실 됩니다 응용 프로그램 도메인을 재활용 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-193">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="d62d9-194">클라이언트에 허브 클래스 외부에서 실행 되는 사용자 고유의 코드에서 메시지를 전송 하려는 경우 허브 클래스 인스턴스를 인스턴스화하고 그럴 수 없습니다 되지만 허브 클래스에 대 한 SignalR 컨텍스트 개체에 대 한 참조를 가져오는 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-194">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="d62d9-195">자세한 내용은 참조 [클라이언트 메서드를 호출할 허브 클래스 외부에서 그룹을 관리 하는 방법을](#callfromoutsidehub) 이 항목의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-195">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="d62d9-196">카멜식 대 / 소문자 JavaScript 클라이언트에서 허브 이름</span><span class="sxs-lookup"><span data-stu-id="d62d9-196">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="d62d9-197">기본적으로 JavaScript 클라이언트에 허브 클래스 이름의 카멜식 대/소문자 버전을 사용 하 여 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-197">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="d62d9-198">SignalR 자동으로 이러한 변경 때문 JavaScript 코드는 JavaScript 규칙을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-198">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="d62d9-199">앞의 예제로 참조 될 `contosoChatHub` JavaScript 코드에서.</span><span class="sxs-lookup"><span data-stu-id="d62d9-199">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="d62d9-200">**Server**</span><span class="sxs-lookup"><span data-stu-id="d62d9-200">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample9.cs?highlight=1)]

<span data-ttu-id="d62d9-201">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="d62d9-201">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample10.js?highlight=1)]

<span data-ttu-id="d62d9-202">추가 사용 하려면 클라이언트에 대해 다른 이름을 지정 하려는 경우는 `HubName` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-202">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="d62d9-203">사용 하는 경우는 `HubName` 특성을 클라이언트 JavaScript에서 카멜식 대/소문자에 이름이 변경 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-203">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="d62d9-204">**Server**</span><span class="sxs-lookup"><span data-stu-id="d62d9-204">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample11.cs?highlight=1)]

<span data-ttu-id="d62d9-205">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="d62d9-205">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample12.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="d62d9-206">여러 허브</span><span class="sxs-lookup"><span data-stu-id="d62d9-206">Multiple Hubs</span></span>

<span data-ttu-id="d62d9-207">응용 프로그램에서 여러 허브 클래스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-207">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="d62d9-208">그렇게 하면 연결이 공유 되어 있는 그룹은 별도 보이지만.</span><span class="sxs-lookup"><span data-stu-id="d62d9-208">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="d62d9-209">모든 클라이언트에서 동일한 URL을 사용 하 여 서비스와 SignalR 연결을 설정할 수 ("/ signalr" 또는 하나를 지정한 경우에 사용자 지정 URL), 서비스에 의해 정의 된 모든 허브에 대 한 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-209">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="d62d9-210">단일 클래스에서 정의 하는 모든 허브 기능에 비해 여러 허브에 대 한 성능 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-210">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="d62d9-211">모든 허브 동일한 HTTP 요청 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-211">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="d62d9-212">같은 연결을 공유 하는 모든 허브를 유일한 HTTP 요청 정보를 서버 사용량이 이므로 SignalR 연결을 설정 하는 원래 HTTP 요청에 추가 되는 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-212">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="d62d9-213">쿼리 문자열을 지정 하 여 서버에 클라이언트에서 정보를 전달 하려면 연결 요청을 사용 하는 경우 다른 허브에 서로 다른 쿼리 문자열을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-213">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="d62d9-214">모든 허브 동일한 정보를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-214">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="d62d9-215">생성 된 JavaScript 프록시 파일에는 하나의 파일에 있는 모든 허브에 대 한 프록시 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-215">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="d62d9-216">JavaScript 프록시에 대 한 정보를 참조 하십시오. [SignalR 허브 API 가이드-JavaScript 클라이언트-생성 된 프록시 및 수에 대 한 역할](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-216">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).</span></span>
- <span data-ttu-id="d62d9-217">그룹 허브 내에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-217">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="d62d9-218">SignalR을 정의할 수 있습니다 이름이 그룹에 브로드캐스트하는 연결 된 클라이언트의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-218">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="d62d9-219">각 허브에 대 한 그룹 별도로 유지 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-219">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="d62d9-220">예를 들어 "Administrators" 라는 그룹 집합에 대 한 클라이언트 포함 프로그램 `ContosoChatHub` 클래스 이름과 동일한 그룹을 다른 집합에 대 한 클라이언트 참조 프로그램 `StockTickerHub` 클래스.</span><span class="sxs-lookup"><span data-stu-id="d62d9-220">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="d62d9-221">클라이언트에서 호출할 수 있는 허브 클래스에 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-221">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="d62d9-222">다음 예제에 나와 있는 것 처럼 클라이언트에서 호출할 수를 허브에 대 한 메서드를 노출 하려면 공용 메서드를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-222">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="d62d9-223">반환 형식 및 C# 메서드에서 마찬가지로 배열 및 복합 형식을 포함 하 여 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-223">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="d62d9-224">매개 변수에서 수신 하거나 호출자에 게 반환 하는 모든 데이터는 JSON을 사용 하 여 클라이언트와 서버 간에 전송 되 고 자동으로 SignalR 처리 복잡 한 개체의 바인딩 및 개체의 배열을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-224">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="d62d9-225">JavaScript 클라이언트에서 메서드 이름의 카멜식 대 / 소문자</span><span class="sxs-lookup"><span data-stu-id="d62d9-225">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="d62d9-226">기본적으로 메서드 이름의 카멜식 대/소문자 버전을 사용 하 여 JavaScript 클라이언트 허브 메서드를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-226">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="d62d9-227">SignalR 자동으로 이러한 변경 때문 JavaScript 코드는 JavaScript 규칙을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-227">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="d62d9-228">**Server**</span><span class="sxs-lookup"><span data-stu-id="d62d9-228">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="d62d9-229">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="d62d9-229">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="d62d9-230">추가 사용 하려면 클라이언트에 대해 다른 이름을 지정 하려는 경우는 `HubMethodName` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-230">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="d62d9-231">**Server**</span><span class="sxs-lookup"><span data-stu-id="d62d9-231">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="d62d9-232">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="d62d9-232">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="d62d9-233">비동기적으로 실행 하는 경우</span><span class="sxs-lookup"><span data-stu-id="d62d9-233">When to execute asynchronously</span></span>

<span data-ttu-id="d62d9-234">메서드는 될 장기 실행 또는 작업을 수행 해야 하는 경우에 대기 데이터베이스를 조회 하는 웹 서비스 호출 등을 포함를 반환 하 여 허브 메서드를 비동기적으로 만듭니다 하 하는 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (대신 `void` 반환) 또는 [ 작업&lt;T&gt; ](https://msdn.microsoft.com/library/dd321424.aspx) 개체 (대신 `T` 반환 형식).</span><span class="sxs-lookup"><span data-stu-id="d62d9-234">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="d62d9-235">반환 하는 `Task` SignalR 메서드에서 개체에 대 한 대기는 `Task` 를 완료 하 고 전송 합니다 래핑되지 않은 결과 클라이언트에 클라이언트에서 메서드 호출 코드가 방식에 차이점이 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-235">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="d62d9-236">허브 메서드를 만드는 비동기 방지 WebSocket 전송 사용 하는 경우 연결을 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-236">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="d62d9-237">허브 메서드를 동기적으로 실행 하는 경우 전송 WebSocket은 동일한 클라이언트에서 허브에 대 한 메서드는 다음 호출 허브 메서드가 완료 될 때까지 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-237">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="d62d9-238">다음 예제와 동일한 방법을 동기적으로 실행 하도록 코드를 작성 또는 비동기적으로 버전 중 하나를 호출 하기 위한 작동 하는 JavaScript 클라이언트 코드와 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-238">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="d62d9-239">**동기**</span><span class="sxs-lookup"><span data-stu-id="d62d9-239">**Synchronous**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="d62d9-240">**Asynchronous - ASP.NET 4.5**</span><span class="sxs-lookup"><span data-stu-id="d62d9-240">**Asynchronous - ASP.NET 4.5**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="d62d9-241">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="d62d9-241">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="d62d9-242">ASP.NET 4.5에서 비동기 메서드를 사용 하는 방법에 대 한 자세한 내용은 참조 [ASP.NET MVC 4의 비동기 메서드를 사용 하 여](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-242">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="d62d9-243">오버 로드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-243">Defining Overloads</span></span>

<span data-ttu-id="d62d9-244">메서드에 대 한 오버 로드를 정의 하려는 경우에 각 오버 로드에 매개 변수 수가 달라 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-244">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="d62d9-245">다른 매개 변수 형식을 지정 하 여 오버 로드를 구분 하는 경우 허브 클래스는 컴파일되지만 SignalR 서비스 오버 로드 중 하나를 호출한 클라이언트 통신을 시도 하면 런타임 시 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-245">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="d62d9-246">허브 클래스에서 클라이언트 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-246">How to call client methods from the Hub class</span></span>

<span data-ttu-id="d62d9-247">메서드를 호출 클라이언트에서 서버를 사용 하 여는 `Clients` 허브 클래스에서 메서드에서는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-247">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="d62d9-248">다음 예제에서는 호출 하는 서버 코드 `addNewMessageToPage` 연결 된 모든 클라이언트 및 JavaScript 클라이언트에서 메서드를 정의 하는 클라이언트 코드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-248">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="d62d9-249">**Server**</span><span class="sxs-lookup"><span data-stu-id="d62d9-249">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample22.cs?highlight=5)]

<span data-ttu-id="d62d9-250">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="d62d9-250">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample23.html?highlight=1)]

<span data-ttu-id="d62d9-251">클라이언트 메서드에서 반환 값을 가져올 수 없습니다. 와 같은 구문 `int x = Clients.All.add(1,1)` 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-251">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="d62d9-252">복합 형식 및 매개 변수 배열을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-252">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="d62d9-253">다음 예제에서는 메서드 매개 변수에서는 클라이언트에는 복합 유형을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-253">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="d62d9-254">**복잡 한 개체를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="d62d9-254">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample24.cs?highlight=3)]

<span data-ttu-id="d62d9-255">**복잡 한 개체를 정의 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="d62d9-255">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample25.cs?highlight=1)]

<span data-ttu-id="d62d9-256">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="d62d9-256">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample26.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="d62d9-257">클라이언트를 선택 하는 RPC 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-257">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="d62d9-258">클라이언트 속성은 반환 된 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) 클라이언트 RPC 받습니다 지정 하기 위한 몇 가지 옵션을 제공 하는 개체:</span><span class="sxs-lookup"><span data-stu-id="d62d9-258">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="d62d9-259">연결 된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-259">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample27.cs)]
- <span data-ttu-id="d62d9-260">호출 클라이언트만 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-260">Only the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="d62d9-261">호출 클라이언트를 제외한 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-261">All clients except the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="d62d9-262">특정 클라이언트 연결 ID로 식별</span><span class="sxs-lookup"><span data-stu-id="d62d9-262">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample30.css)]

    <span data-ttu-id="d62d9-263">이 예제에서는 호출 `addContosoChatMessageToPage` 호출 클라이언트에 사용 하 여 것과 동일한 결과가 및 `Clients.Caller`합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-263">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="d62d9-264">연결 된 모든 클라이언트 연결 ID로 식별 하는 지정 된 클라이언트를 제외한</span><span class="sxs-lookup"><span data-stu-id="d62d9-264">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample31.cs)]
- <span data-ttu-id="d62d9-265">지정된 된 그룹에 연결 된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-265">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample32.css)]
- <span data-ttu-id="d62d9-266">지정된 된 그룹의 모든 연결 된 클라이언트 연결 ID로 식별 하는 지정 된 클라이언트를 제외 하</span><span class="sxs-lookup"><span data-stu-id="d62d9-266">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample33.cs)]
- <span data-ttu-id="d62d9-267">지정된 된 그룹의 모든 연결 된 클라이언트 호출 클라이언트를 제외 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-267">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample34.css)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="d62d9-268">메서드 이름에 대 한 컴파일 시간 유효성</span><span class="sxs-lookup"><span data-stu-id="d62d9-268">No compile-time validation for method names</span></span>

<span data-ttu-id="d62d9-269">메서드 이름은 지정 하는 의미 없는 IntelliSense 또는 컴파일 타임 유효성 검사에 대 한 동적 개체로 해석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-269">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="d62d9-270">식이 런타임 시 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-270">The expression is evaluated at run time.</span></span> <span data-ttu-id="d62d9-271">메서드 호출이 실행 하는 경우, 메서드가 호출 되도록 SignalR 메서드 이름과 매개 변수 값을 클라이언트에 보내고의 이름과 일치 하는 클라이언트에서 메서드 및 매개 변수 값에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-271">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="d62d9-272">메서드가 클라이언트에서 발견 되는 경우 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-272">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="d62d9-273">SignalR 클라이언트 메서드를 호출할 때 내부적 클라이언트에 전송 하는 데이터의 형식에 대 한 정보를 참조 하십시오. [SignalR 소개](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-273">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](index.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="d62d9-274">일치 하는 대/소문자 구분 메서드 이름</span><span class="sxs-lookup"><span data-stu-id="d62d9-274">Case-insensitive method name matching</span></span>

<span data-ttu-id="d62d9-275">메서드 이름 일치는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-275">Method name matching is case-insensitive.</span></span> <span data-ttu-id="d62d9-276">예를 들어 `Clients.All.addContosoChatMessageToPage` 서버에서 실행 됩니다 `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, 또는 `addContosoChatMessageToPage` 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="d62d9-276">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="d62d9-277">비동기 실행</span><span class="sxs-lookup"><span data-stu-id="d62d9-277">Asynchronous execution</span></span>

<span data-ttu-id="d62d9-278">호출 하는 메서드를 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-278">The method that you call executes asynchronously.</span></span> <span data-ttu-id="d62d9-279">SignalR 클라이언트에 데이터를 전송 하 여 코드의 다음 줄 메서드 완료를 위해 대기 해야를 지정 하지 않으면 완료 될 때까지 기다리지 않고 즉시 실행 됩니다 클라이언트에 메서드 호출 뒤에 오는 모든 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-279">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="d62d9-280">다음 코드 예제는 두 개의 클라이언트 메서드를 순차적으로 실행 하는 방법을 보여 하나를 사용 하 여.NET 4.5에서 작동 하는 코드가, 하나를 사용 하 여.NET 4에서 작동 하는 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-280">The following code examples show how to execute two client methods sequentially, one using code that works in .NET 4.5, and one using code that works in .NET 4.</span></span>

<span data-ttu-id="d62d9-281">**.NET 4.5 예제**</span><span class="sxs-lookup"><span data-stu-id="d62d9-281">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample35.cs?highlight=1,3)]

<span data-ttu-id="d62d9-282">**.NET 4 예**</span><span class="sxs-lookup"><span data-stu-id="d62d9-282">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample36.cs?highlight=3-4)]

<span data-ttu-id="d62d9-283">사용 하는 경우 `await` 또는 `ContinueWith` 클라이언트 메서드 코드의 다음 줄을 실행 하기 전에 완료 될 때까지 기다려야 의미는 아닙니다 클라이언트 코드의 다음 줄이 실행 되기 전에 메시지가 표시 실제로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-283">If you use `await` or `ContinueWith` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="d62d9-284">클라이언트 메서드 호출의 "완료"만 SignalR 모든 작업을 완료 메시지를 보내는 데 필요한 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-284">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="d62d9-285">클라이언트는 메시지를 받았음을 확인 해야 할 경우 사용자가 직접 메커니즘을 프로그래밍 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-285">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="d62d9-286">예를 들어 코딩할 수는 `MessageReceived` 허브 및 메서드는 `addContosoChatMessageToPage` 메서드를 호출할 수 있습니다 클라이언트 `MessageReceived` 클라이언트에서 수행 하는 것이 해야 하면 작업을 수행한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-286">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="d62d9-287">`MessageReceived` 허브에서 할 수 있는 실제 클라이언트 ं आ स ा 원래 메서드 호출의 처리에는 작업에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-287">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="d62d9-288">메서드 이름으로 문자열 변수를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-288">How to use a string variable as the method name</span></span>

<span data-ttu-id="d62d9-289">캐스팅 메서드 이름으로 문자열 변수를 사용 하 여 클라이언트 메서드를 호출 하려면 `Clients.All` (또는 `Clients.Others`, `Clients.Caller`등)를 `IClientProxy` 호출 [Invoke (methodName,... args) ](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="d62d9-289">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample37.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="d62d9-290">허브 클래스에서 그룹 구성원 자격을 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-290">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="d62d9-291">SignalR에서 그룹 연결 된 클라이언트의 지정 된 하위 집합에 메시지 브로드캐스트에 대 한 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-291">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="d62d9-292">그룹의 클라이언트, 모든 수 있고 클라이언트가 여러 그룹의 멤버일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-292">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="d62d9-293">그룹 구성원 자격을 관리 하려면 사용 하 여는 [추가](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 및 [제거](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) 에서 제공 하는 메서드는 `Groups` 허브 클래스의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-293">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="d62d9-294">다음 예제와 `Groups.Add` 및 `Groups.Remove` 호출 하는 JavaScript 클라이언트 코드가 뒤에 오는 클라이언트 코드에서 호출할 허브 메서드에서 사용 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-294">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="d62d9-295">**Server**</span><span class="sxs-lookup"><span data-stu-id="d62d9-295">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample38.cs?highlight=5,10)]

<span data-ttu-id="d62d9-296">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="d62d9-296">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample39.js)]

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample40.js)]

<span data-ttu-id="d62d9-297">명시적으로 그룹을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-297">You don't have to explicitly create groups.</span></span> <span data-ttu-id="d62d9-298">그룹에 대 한 호출에 해당 이름을 지정 하는 처음으로 자동으로 생성 적용 `Groups.Add`, 마지막 연결에 대 한 멤버 자격에서 제거할 때 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-298">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="d62d9-299">그룹 멤버 자격 목록 또는 그룹 목록을 가져오는 데 필요한 API는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-299">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="d62d9-300">SignalR 클라이언트와 그룹을 기반으로 메시지를 보냅니다는 [pub/sub 모델](http://en.wikipedia.org/wiki/Publish/subscribe), 서버 그룹 또는 그룹 멤버 자격 목록이 유지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-300">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="d62d9-301">이렇게 하면 확장성을 최대화 웹 팜에 노드를 추가할 때마다 SignalR 유지 하는 모든 상태 하기 때문에 새 노드를 전파할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-301">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="d62d9-302">Add 및 Remove 메서드의 비동기 실행</span><span class="sxs-lookup"><span data-stu-id="d62d9-302">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="d62d9-303">`Groups.Add` 및 `Groups.Remove` 메서드를 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-303">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="d62d9-304">다음 사항을 확인 해야 하는 그룹에 클라이언트를 추가 및 즉시 그룹을 사용 하 여 클라이언트에 메시지를 전송 하려는 경우는 `Groups.Add` 메서드를 먼저 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-304">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="d62d9-305">다음 코드 예제는.NET 4.5와.NET 4에서 작동 하는 코드를 사용 하 여 사용할 수 있는 코드를 사용 하 여 하나를 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-305">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4</span></span>

<span data-ttu-id="d62d9-306">**.NET 4.5 예제**</span><span class="sxs-lookup"><span data-stu-id="d62d9-306">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="d62d9-307">**.NET 4 예**</span><span class="sxs-lookup"><span data-stu-id="d62d9-307">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample42.cs?highlight=3-4)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="d62d9-308">그룹 멤버 자격 지 속성</span><span class="sxs-lookup"><span data-stu-id="d62d9-308">Group membership persistence</span></span>

<span data-ttu-id="d62d9-309">연결을 추적 하는 SignalR, 사용자가 아닌, 그럴 경우 사용자가 동일한 그룹에 사용자 설정 될 때마다 연결 5d; 호출 해야 `Groups.Add` 될 때마다 사용자는 새 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-309">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="d62d9-310">다음 임시 연결 끊김 때로는 SignalR 복원할 수 연결이 자동으로.</span><span class="sxs-lookup"><span data-stu-id="d62d9-310">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="d62d9-311">이 경우 SignalR은 같은 연결을 새 연결을 설정 하지 복원과 이므로 클라이언트의 그룹 구성원 자격 자동으로 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-311">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="d62d9-312">가능한 임시 중단에 서버를 다시 부팅 또는 실패, 결과가 하는 경우에 때문에 이것이 그룹 멤버 자격을 포함 하 여 각 클라이언트에 대 한 연결 상태는 클라이언트로 라운드트립 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-312">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="d62d9-313">서버 작동이 중단 하 연결 시간이 초과 되기 전에 새 서버를 교체 하는 경우 클라이언트에서 새 서버로 자동으로 연결할 수 있고의 멤버인 그룹에 다시 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-313">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="d62d9-314">연결이 끊어진 후 연결을 자동으로 복원할 수 없습니다 또는 때 연결 시간이 초과 했거나 경우 (예를 들어 경우 브라우저를 새 페이지로 이동) 클라이언트의 연결이 끊어지면, 그룹 멤버 자격 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-314">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="d62d9-315">다음에 사용자 연결에 대 한 새 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-315">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="d62d9-316">파일을 동일한 사용자는 새 연결을 설정 하는 경우 그룹 구성원 자격을 유지 하려면 응용 프로그램 사용자 및 그룹, 간의 연결을 추적 및 될 때마다 새 연결을 설정 하는 사용자 그룹 멤버 자격을 복원 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-316">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="d62d9-317">연결 및 다시 연결 하는 방법에 대 한 자세한 내용은 참조 [허브 클래스에서 연결 수명 이벤트를 처리 하는 방법을](#connectionlifetime) 이 항목의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-317">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="d62d9-318">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="d62d9-318">Single-user groups</span></span>

<span data-ttu-id="d62d9-319">SignalR을 일반적으로 사용 하는 응용 프로그램 어떤 사용자가 메시지를 보낸 및 어떤 사용자 메시지를 수신 해야을 확인 하기 위해 사용자와 연결 간의 연결을 추적할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-319">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="d62d9-320">그룹 작업을 수행 하는 두 가지 자주 사용 되는 패턴 중 하나에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-320">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="d62d9-321">단일 사용자 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-321">Single-user groups.</span></span>

    <span data-ttu-id="d62d9-322">그룹 이름으로 사용자 이름을 지정 하 고 사용자 연결 되거나 다시 연결 될 때마다 그룹에 현재 연결 ID를 추가할 수도 있지만</span><span class="sxs-lookup"><span data-stu-id="d62d9-322">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="d62d9-323">그룹에 보낼 사용자에 게 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-323">To send messages to the user you send to the group.</span></span> <span data-ttu-id="d62d9-324">이 방법의 단점은 그룹 하지 않는 제공입니다 하면 사용자가 온라인 또는 오프 라인 인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-324">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="d62d9-325">사용자 이름 및 연결 Id 간의 연결을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-325">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="d62d9-326">사전 또는 데이터베이스에 각 사용자 이름 및 하나 이상의 연결 Id 간의 연결을 저장 하 고 사용자 연결 되거나 연결 해제 될 때마다 저장 된 데이터를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-326">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="d62d9-327">사용자에 게 메시지를 보낼 연결 Id를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-327">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="d62d9-328">이 방법의 단점은 더 많은 메모리를 차지 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-328">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="d62d9-329">허브 클래스에서 연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-329">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="d62d9-330">연결 수명 이벤트를 처리 하기 위한 일반적인 이유는 여부는 사용자가 연결 되어 있는지 여부를 추적 하 고 사용자 이름 및 연결 Id 간의 연결을 추적 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-330">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="d62d9-331">클라이언트에서 연결 하거나 연결을 끊을 때 코드를 실행 하려면 재정의 `OnConnected`, `OnDisconnected`, 및 `OnReconnected` 다음 예제와 같이 허브의 가상 메서드 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-331">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample43.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="d62d9-332">OnConnected, OnDisconnected, 및 OnReconnected 호출 될 때</span><span class="sxs-lookup"><span data-stu-id="d62d9-332">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="d62d9-333">브라우저를 새 페이지로 이동 될 때마다 새 연결에 설정 될 SignalR 실행될지 의미는 `OnDisconnected` 메서드는 `OnConnected` 메서드.</span><span class="sxs-lookup"><span data-stu-id="d62d9-333">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="d62d9-334">SignalR 새 연결이 설정 될 때 항상 새 연결 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-334">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="d62d9-335">`OnReconnected` 메서드는 케이블을 일시적으로 분리 및 연결 시간이 초과 되기 전에 다시 연결 경우 등,에서 SignalR 수 자동으로 복구 하는 연결에서 임시 중단 되었습니다. `OnDisconnected` 클라이언트 연결이 끊기고 SignalR 자동으로 다시 연결할 수 없습니다, 브라우저를 새 페이지로 이동 하는 경우와 같은 때 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-335">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="d62d9-336">따라서 지정된 된 클라이언트에 대 한 이벤트의 가능한 시퀀스는 `OnConnected`, `OnReconnected`, `OnDisconnected`; 또는 `OnConnected`, `OnDisconnected`합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-336">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="d62d9-337">시퀀스를 표시 되지 않습니다 `OnConnected`, `OnDisconnected`, `OnReconnected` 지정된 된 연결에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-337">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="d62d9-338">`OnDisconnected` 가 서버 작동이 중단 될 때와 같은 일부 시나리오에서는 메서드 호출 또는 응용 프로그램 도메인 재활용을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-338">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="d62d9-339">일부 클라이언트 온라인 상태가 다른 서버 또는 응용 프로그램 도메인의 재활용 완료 하는 경우 다시 연결 하 고 발생 하는 작업을 할 수 있습니다는 `OnReconnected` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-339">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="d62d9-340">자세한 내용은 참조 [이해 하 고 SignalR에서 연결 수명 이벤트를 처리](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-340">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="d62d9-341">채워지지 호출자 상태</span><span class="sxs-lookup"><span data-stu-id="d62d9-341">Caller state not populated</span></span>

<span data-ttu-id="d62d9-342">에 저장 된 모든 상태를 의미 하는 서버에서 연결 수명 이벤트 처리기 메서드 호출의 `state` 클라이언트에서 개체에 입력 되지 것입니다는 `Caller` 서버에 대 한 속성.</span><span class="sxs-lookup"><span data-stu-id="d62d9-342">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="d62d9-343">에 대 한 내용은 `state` 개체 및 `Caller` 속성 참조 [클라이언트와 허브 클래스 간의 상태를 전달 하는 방법을](#passstate) 이 항목의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-343">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="d62d9-344">컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-344">How to get information about the client from the Context property</span></span>

<span data-ttu-id="d62d9-345">클라이언트에 대 한 정보를 가져오려면는 `Context` 허브 클래스의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-345">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="d62d9-346">`Context` 속성에서 반환 된 [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) 다음 정보에 대 한 액세스를 제공 하는 개체:</span><span class="sxs-lookup"><span data-stu-id="d62d9-346">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="d62d9-347">호출 클라이언트의 연결 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-347">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample44.cs?highlight=1)]

    <span data-ttu-id="d62d9-348">연결 ID는 SignalR (사용자 코드에서 값을 지정할 수 없습니다.)으로 할당 하는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-348">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="d62d9-349">각 연결과 동일한 연결 여러 허브 응용 프로그램에 있는 경우 모든 허브에서 ID를 사용 하는 것에 대 한 연결 ID를 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-349">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="d62d9-350">HTTP 헤더 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-350">HTTP header data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample45.cs?highlight=1)]

    <span data-ttu-id="d62d9-351">HTTP 헤더에서 얻을 수 있습니다 `Context.Headers`합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-351">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="d62d9-352">동일한 작업에 대 한 여러 참조에 대 한 이유는 `Context.Headers` 먼저 만들어진는 `Context.Request` 속성, 나중에 추가 하 고 `Context.Headers` 이전 버전과 호환성을 위해 유지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-352">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="d62d9-353">문자열 데이터를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-353">Query string data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample46.cs?highlight=1)]

    <span data-ttu-id="d62d9-354">데이터를 쿼리 문자열을 얻을 수 있습니다 `Context.QueryString`합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-354">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="d62d9-355">이 속성에서 가져올 쿼리 문자열은는 SignalR 연결을 설정 하는 HTTP 요청과 함께 사용 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-355">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="d62d9-356">서버에는 클라이언트에서 클라이언트에 대 한 데이터를 전달 하는 편리한 방법은 연결을 구성 하 여 클라이언트에서 쿼리 문자열 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-356">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="d62d9-357">다음 예제에서는 생성 된 프록시를 사용 하는 경우 JavaScript 클라이언트에서 쿼리 문자열을 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-357">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample47.js?highlight=1)]

    <span data-ttu-id="d62d9-358">쿼리 문자열 매개 변수를 설정 하는 방법에 대 한 자세한 내용은 참조에 대 한 API 가이드는 [JavaScript](index.md) 및 [.NET](index.md) 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-358">For more information about setting query string parameters, see the API guides for the [JavaScript](index.md) and [.NET](index.md) clients.</span></span>

    <span data-ttu-id="d62d9-359">쿼리 문자열 데이터 SignalR에서 내부적으로 사용 되는 일부 다른 값과 함께 연결에 사용 된 전송 메서드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-359">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample48.cs)]

    <span data-ttu-id="d62d9-360">값 `transportMethod` "Websocket", "serverSentEvents", "foreverFrame" 또는 "longPolling" 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-360">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="d62d9-361">이 값을 확인 하는 경우는 `OnConnected` 이벤트 처리기 메서드 일부 시나리오에서 발생할 수 있습니다 처음 연결에 대 한 최종 협상 된 전송 메서드 없는 전송 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-361">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="d62d9-362">이 경우 메서드 예외가 throw 됩니다 하 고 최종 전송 방법 설정 되 면 나중에 다시 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-362">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="d62d9-363">쿠키입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-363">Cookies.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="d62d9-364">쿠키를 얻을 수 있습니다 `Context.RequestCookies`합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-364">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="d62d9-365">사용자 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-365">User information.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample50.cs?highlight=1)]
- <span data-ttu-id="d62d9-366">요청에 대 한 HttpContext 개체:</span><span class="sxs-lookup"><span data-stu-id="d62d9-366">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample51.cs?highlight=1)]

    <span data-ttu-id="d62d9-367">이 메서드를 사용 하 여 아닌 `HttpContext.Current` 가져오려는 `HttpContext` SignalR 연결에 대 한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-367">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="d62d9-368">클라이언트와 허브 클래스 간의 상태를 전달 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-368">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="d62d9-369">클라이언트 프록시는 제공 하는 `state` 개체를 각 메서드 호출을 사용 하 여 서버에 전송 될 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-369">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="d62d9-370">서버에서이 데이터에 액세스할 수 있습니다는 `Clients.Caller` 클라이언트에서 호출 하는 허브 메서드의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-370">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="d62d9-371">`Clients.Caller` 연결 수명 이벤트 처리기 방법에 대 한 속성은 채워지지 않습니다 `OnConnected`, `OnDisconnected`, 및 `OnReconnected`합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-371">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="d62d9-372">만들기 또는 업데이트에 데이터는 `state` 개체 및 `Clients.Caller` 속성은 두 방향으로 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-372">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="d62d9-373">서버에서 값을 업데이트할 수 있습니다 및 클라이언트에 다시 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-373">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="d62d9-374">다음 예제에서는 모든 메서드 호출을 사용 하 여 서버에 전송에 대 한 상태를 저장 하는 JavaScript 클라이언트 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-374">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample52.js?highlight=1-2)]

<span data-ttu-id="d62d9-375">다음 예제에서는.NET 클라이언트에 해당 하는 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-375">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample53.cs?highlight=1-2)]

<span data-ttu-id="d62d9-376">허브 클래스에이 데이터에 액세스할 수 있습니다는 `Clients.Caller` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-376">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="d62d9-377">다음 예제에서는 이전 예제에서 참조 하는 상태를 검색 하는 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-377">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample54.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="d62d9-378">지속 상태에 대 한이 메커니즘을 사용할 수 없는 많은 양의 데이터를 이후 모드로 전환할 모든 항목은 `state` 또는 `Clients.Caller` 속성은 모든 메서드 호출으로 라운드트립 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-378">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="d62d9-379">사용자 이름 또는 카운터 등의 더 작은 항목에는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-379">It's useful for smaller items such as user names or counters.</span></span>


<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="d62d9-380">허브 클래스에는 오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-380">How to handle errors in the Hub class</span></span>

<span data-ttu-id="d62d9-381">허브 클래스 메서드에서 발생 하는 오류를 처리 하려면 다음 방법 중 하나 또는 모두를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-381">To handle errors that occur in your Hub class methods, use one or both of the following methods:</span></span>

- <span data-ttu-id="d62d9-382">Try / catch 블록에서 메서드 코드를 래핑하고 예외 개체를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-382">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="d62d9-383">디버깅 목적으로 클라이언트에 예외를 보낼 수 있지만 보안에 대 한 프로덕션의 클라이언트에 자세한 정보를 보내의 이유로 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-383">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="d62d9-384">처리 하는 허브 파이프라인 모듈 만들기는 [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="d62d9-384">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="d62d9-385">다음 예제에서는 모듈을 허브 파이프라인에 삽입 합니다. Global.asax에 코드가 뒤에 오는 오류 로그에 기록 하는 파이프라인 모듈을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-385">The following example shows a pipeline module that logs errors, followed by code in Global.asax that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample55.cs)]

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample56.cs?highlight=3)]

<span data-ttu-id="d62d9-386">허브 파이프라인 모듈에 대 한 자세한 내용은 참조 [허브 파이프라인을 사용자 지정 하는 방법을](#hubpipeline) 이 항목의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-386">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="d62d9-387">추적을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-387">How to enable tracing</span></span>

<span data-ttu-id="d62d9-388">서버 쪽 추적을 사용 하려면이 예제에 나와 있는 것 처럼 system.diagnostics 요소, Web.config 파일에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-388">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample57.html?highlight=17-72)]

<span data-ttu-id="d62d9-389">Visual Studio에서 응용 프로그램을 실행 하는 경우 로그를 볼 수 있습니다는 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="d62d9-389">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="d62d9-390">클라이언트 메서드를 호출할 허브 클래스 외부에서 그룹을 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-390">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="d62d9-391">클라이언트 허브 클래스와는 다른 클래스에서 메서드를 호출 하십시오 허브에 대 한 SignalR 컨텍스트 개체에 대 한 참조를 가져오고를 사용 하 여 클라이언트에서 메서드를 호출 또는 그룹을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-391">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="d62d9-392">다음 샘플 `StockTicker` 클래스 컨텍스트 개체를 가져옵니다, 클래스의 인스턴스에 저장, 클래스 인스턴스는 정적 속성에 저장 및 단일 항목 클래스 인스턴스에서 컨텍스트 호출에 사용 하 여 `updateStockPrice` 클라이언트 상의 메서드 명명 된 허브에 연결 된 `StockTickerHub`합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-392">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample58.cs?highlight=8,24)]

<span data-ttu-id="d62d9-393">수명이 긴 개체에 있는 상황에 맞는 여러 번을 사용 해야 하는 경우 한 번에 대 한 참조를 가져오려면 대신 될 때마다 다시 가져오는 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-393">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="d62d9-394">컨텍스트를 한 번 가져오기 하면 SignalR 허브 메서드 수행할 수 있는 클라이언트를 메서드 호출 하 고 동일한 시퀀스의 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-394">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="d62d9-395">허브에 대 한 SignalR 컨텍스트를 사용 하는 방법을 보여 주는 자습서를 참조 하십시오. [ASP.NET SignalR과 서버 브로드캐스트](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-395">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](index.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="d62d9-396">클라이언트 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="d62d9-396">Calling client methods</span></span>

<span data-ttu-id="d62d9-397">클라이언트는 RPC를 받게 됩니다 지정할 수 있지만 허브 클래스에서 호출 하는 경우 보다 더 적은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-397">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="d62d9-398">이러한 이유로 없다는 컨텍스트는 클라이언트로부터 특정 호출에 연결 된 때문는 메서드는 현재 연결 ID 알고와 같은 `Clients.Others`, 또는 `Clients.Caller`, 또는 `Clients.OthersInGroup`는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-398">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="d62d9-399">다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-399">The following options are available:</span></span>

- <span data-ttu-id="d62d9-400">연결 된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-400">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample59.cs)]
- <span data-ttu-id="d62d9-401">특정 클라이언트 연결 ID로 식별</span><span class="sxs-lookup"><span data-stu-id="d62d9-401">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample60.css)]
- <span data-ttu-id="d62d9-402">연결 된 모든 클라이언트 연결 ID로 식별 하는 지정 된 클라이언트를 제외한</span><span class="sxs-lookup"><span data-stu-id="d62d9-402">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample61.cs)]
- <span data-ttu-id="d62d9-403">지정된 된 그룹에 연결 된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-403">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample62.css)]
- <span data-ttu-id="d62d9-404">연결 ID로 식별 하는 지정 된 클라이언트를 제외한 지정된 된 그룹의 모든 연결 된 클라이언트</span><span class="sxs-lookup"><span data-stu-id="d62d9-404">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample63.cs)]

<span data-ttu-id="d62d9-405">를 호출 하는 비-허브 클래스에 방법 중에서 허브 클래스에 경우에 현재 연결 ID를 전달할 고 된 경우에 사용할 수 있습니다 `Clients.Client`, `Clients.AllExcept`, 또는 `Clients.Group` 시뮬레이션할 `Clients.Caller`, `Clients.Others`, 또는 `Clients.OthersInGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-405">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="d62d9-406">다음 예제에서는 `MoveShapeHub` 클래스 연결 ID를 전달는 `Broadcaster` 클래스 있도록는 `Broadcaster` 클래스를 시뮬레이션할 수 `Clients.Others`합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-406">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample64.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="d62d9-407">그룹 멤버 자격 관리</span><span class="sxs-lookup"><span data-stu-id="d62d9-407">Managing group membership</span></span>

<span data-ttu-id="d62d9-408">그룹 관리에 대 한 허브 클래스에 작업을 수행한와 동일한 옵션이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-408">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="d62d9-409">그룹에 클라이언트 추가</span><span class="sxs-lookup"><span data-stu-id="d62d9-409">Add a client to a group</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample65.cs)]
- <span data-ttu-id="d62d9-410">그룹에서 클라이언트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-410">Remove a client from a group</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample66.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="d62d9-411">허브 파이프라인을 사용자 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d62d9-411">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="d62d9-412">SignalR을 사용 하는 허브 파이프라인에 사용자 고유의 코드를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-412">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="d62d9-413">다음 예제에서는 클라이언트 및 클라이언트에서 호출 하는 나가는 메서드 호출에서 받은 각 들어오는 메서드 호출을 기록 하는 사용자 지정 허브 파이프라인 모듈을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-413">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample67.cs)]

<span data-ttu-id="d62d9-414">다음 코드에 *Global.asax* 허브 파이프라인에서 실행 하도록 모듈을 등록 하는 파일:</span><span class="sxs-lookup"><span data-stu-id="d62d9-414">The following code in the *Global.asax* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample68.cs?highlight=3)]

<span data-ttu-id="d62d9-415">재정의할 수 있는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-415">There are many different methods that you can override.</span></span> <span data-ttu-id="d62d9-416">전체 목록을 보려면를 참조 하십시오. [HubPipelineModule 메서드](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d62d9-416">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
