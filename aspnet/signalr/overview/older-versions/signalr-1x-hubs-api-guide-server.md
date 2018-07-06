---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
title: ASP.NET SignalR 허브 API 가이드-서버 (SignalR 1.x) | Microsoft Docs
author: pfletcher
description: 이 문서에서는 코드 샘플 demonstratin 사용 하 여 버전 1.1에서 SignalR에 대 한 ASP.NET SignalR 허브 API의 서버 쪽 프로그래밍 소개를 제공 하는 중...
ms.author: aspnetcontent
ms.date: 04/17/2013
ms.assetid: 03e4b9f5-0fea-4d94-959f-014b2762a301
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: 15d2f4e9eaff0d47a3bdce489dfc1d19177423f8
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37826415"
---
<a name="aspnet-signalr-hubs-api-guide---server-signalr-1x"></a><span data-ttu-id="3c7d0-103">ASP.NET SignalR 허브 API 가이드-서버 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="3c7d0-103">ASP.NET SignalR Hubs API Guide - Server (SignalR 1.x)</span></span>
====================
<span data-ttu-id="3c7d0-104">하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="3c7d0-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="3c7d0-105">이 문서에서는 일반 옵션을 보여 주는 코드 샘플을 사용 하 여 서버 쪽 ASP.NET SignalR 허브 API의 버전 1.1에서 SignalR에 대 한 프로그래밍을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 1.1, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="3c7d0-106">SignalR 허브 API를 사용 하면 클라이언트가 서버에 연결 된 클라이언트에는 서버에서 원격 프로시저 호출 (Rpc)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="3c7d0-107">서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="3c7d0-108">클라이언트 코드에서 서버에서 호출할 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="3c7d0-109">SignalR은 모든 클라이언트-서버 연결 구조를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="3c7d0-110">또한 SignalR 영구 연결을 호출 하는 하위 수준 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="3c7d0-111">SignalR에서 허브 및 영구 연결에 대 한 소개, 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서에 대 한 참조 [SignalR-Getting Started](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](index.md).</span></span>


## <a name="overview"></a><span data-ttu-id="3c7d0-112">개요</span><span class="sxs-lookup"><span data-stu-id="3c7d0-112">Overview</span></span>

<span data-ttu-id="3c7d0-113">이 문서는 다음 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="3c7d0-114">SignalR 경로 등록 하 고 SignalR 옵션을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-114">How to register the SignalR route and configure SignalR options</span></span>](#route)

    - [<span data-ttu-id="3c7d0-115">/Signalr URL</span><span class="sxs-lookup"><span data-stu-id="3c7d0-115">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="3c7d0-116">SignalR 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="3c7d0-116">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="3c7d0-117">만들고 허브 클래스를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-117">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="3c7d0-118">허브 개체 수명</span><span class="sxs-lookup"><span data-stu-id="3c7d0-118">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="3c7d0-119">카멜식 대 / JavaScript 클라이언트에 허브 이름</span><span class="sxs-lookup"><span data-stu-id="3c7d0-119">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="3c7d0-120">여러 허브</span><span class="sxs-lookup"><span data-stu-id="3c7d0-120">Multiple Hubs</span></span>](#multiplehubs)
- [<span data-ttu-id="3c7d0-121">클라이언트에서 호출할 수 있는 허브 클래스에 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-121">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="3c7d0-122">JavaScript 클라이언트에서 메서드 이름의 카멜식 대 / 소문자</span><span class="sxs-lookup"><span data-stu-id="3c7d0-122">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="3c7d0-123">비동기적으로 실행 하는 경우</span><span class="sxs-lookup"><span data-stu-id="3c7d0-123">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="3c7d0-124">오버 로드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-124">Defining overloads</span></span>](#overloads)
- [<span data-ttu-id="3c7d0-125">허브 클래스에서 클라이언트 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-125">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="3c7d0-126">RPC를 수신할 클라이언트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-126">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="3c7d0-127">메서드 이름에 대 한 컴파일 시간 유효성 검사 없음</span><span class="sxs-lookup"><span data-stu-id="3c7d0-127">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="3c7d0-128">대/소문자 메서드 이름 일치</span><span class="sxs-lookup"><span data-stu-id="3c7d0-128">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="3c7d0-129">비동기 실행</span><span class="sxs-lookup"><span data-stu-id="3c7d0-129">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="3c7d0-130">허브 클래스에서 그룹 멤버 자격을 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-130">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="3c7d0-131">비동기 실행의 Add 및 Remove 메서드</span><span class="sxs-lookup"><span data-stu-id="3c7d0-131">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="3c7d0-132">그룹 멤버 자격 지 속성</span><span class="sxs-lookup"><span data-stu-id="3c7d0-132">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="3c7d0-133">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="3c7d0-133">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="3c7d0-134">허브 클래스에서 연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-134">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="3c7d0-135">OnConnected, OnDisconnected, 및 OnReconnected 호출 될 때</span><span class="sxs-lookup"><span data-stu-id="3c7d0-135">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="3c7d0-136">채워지지 호출자 상태</span><span class="sxs-lookup"><span data-stu-id="3c7d0-136">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="3c7d0-137">컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-137">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="3c7d0-138">클라이언트와 허브 클래스 간의 상태를 전달 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-138">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="3c7d0-139">허브 클래스에서 오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-139">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="3c7d0-140">클라이언트 메서드를 호출 하 고 허브 클래스 외부에서 그룹을 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-140">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="3c7d0-141">클라이언트 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-141">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="3c7d0-142">그룹 멤버 자격 관리</span><span class="sxs-lookup"><span data-stu-id="3c7d0-142">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="3c7d0-143">추적을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-143">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="3c7d0-144">허브 파이프라인 사용자 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-144">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="3c7d0-145">프로그램 클라이언트 하는 방법에 대 한 설명서를 다음 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-145">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="3c7d0-146">SignalR 허브 API 가이드-JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="3c7d0-146">SignalR Hubs API Guide - JavaScript Client</span></span>](index.md)
- [<span data-ttu-id="3c7d0-147">SignalR 허브 API 가이드-.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="3c7d0-147">SignalR Hubs API Guide - .NET Client</span></span>](index.md)

<span data-ttu-id="3c7d0-148">.NET 4.5 버전의 API는 API 참조 항목에 대 한 링크.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-148">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="3c7d0-149">.NET 4를 사용 하는 경우 참조 [항목에서는 API의.NET 4 버전](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-149">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="route"></a>

## <a name="how-to-register-the-signalr-route-and-configure-signalr-options"></a><span data-ttu-id="3c7d0-150">SignalR 경로 등록 하 고 SignalR 옵션을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-150">How to register the SignalR route and configure SignalR options</span></span>

<span data-ttu-id="3c7d0-151">클라이언트가 사용 하 여 허브에 연결 하는 경로 정의 하려면 호출을 [MapHubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) 메서드 시작 하면 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-151">To define the route that clients will use to connect to your Hub, call the [MapHubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="3c7d0-152">`MapHubs` [확장 메서드](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) 에 대 한는 `System.Web.Routing.RouteCollection` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-152">`MapHubs` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `System.Web.Routing.RouteCollection` class.</span></span> <span data-ttu-id="3c7d0-153">다음 예제에서 SignalR 허브 경로 정의 하는 방법을 보여 줍니다 합니다 *Global.asax* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-153">The following example shows how to define the SignalR Hubs route in the *Global.asax* file.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample1.cs)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample2.cs?highlight=5)]

<span data-ttu-id="3c7d0-154">ASP.NET MVC 응용 프로그램에 SignalR 기능을 추가 하는 경우에 SignalR 경로의 다른 경로 보다 먼저 추가 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-154">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="3c7d0-155">자세한 내용은 [자습서: SignalR 및 MVC 4 시작](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-155">For more information, see [Tutorial: Getting Started with SignalR and MVC 4](index.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="3c7d0-156">/Signalr URL</span><span class="sxs-lookup"><span data-stu-id="3c7d0-156">The /signalr URL</span></span>

<span data-ttu-id="3c7d0-157">기본적으로 클라이언트가 사용 하 여 허브에 연결 하는 경로 URL은 "/ signalr"입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-157">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="3c7d0-158">(자동으로 생성된 된 JavaScript 파일에는 "/ signalr 허브" URL 사용 하 여이 URL을 혼동 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-158">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="3c7d0-159">생성 된 프록시에 대 한 자세한 내용은 참조 하세요. [SignalR 허브 API 가이드-JavaScript 클라이언트-생성 된 프록시 및 용도를](index.md).)</span><span class="sxs-lookup"><span data-stu-id="3c7d0-159">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).)</span></span>

<span data-ttu-id="3c7d0-160">SignalR;에 대 한 기본 URL을 사용할 수 없습니다 하는 특수 상황 있을 수 있습니다. 예를 들어 있는 폴더 라는 프로젝트가 *signalr* 이름을 변경 하지 않으려는 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-160">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="3c7d0-161">이 경우 다음 예와에서 같이 기본 URL을 변경할 수 있습니다 (대체 "/ signalr" 원하는 URL 사용 하 여 샘플 코드에서).</span><span class="sxs-lookup"><span data-stu-id="3c7d0-161">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="3c7d0-162">**URL을 지정 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-162">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample3.cs?highlight=1)]

<span data-ttu-id="3c7d0-163">**URL (생성된 된 프록시)를 지정 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-163">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="3c7d0-164">**(없이 생성된 된 프록시) URL을 지정 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-164">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample5.js?highlight=1)]

<span data-ttu-id="3c7d0-165">**URL을 지정 하는.NET 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-165">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample6.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="3c7d0-166">SignalR 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="3c7d0-166">Configuring SignalR Options</span></span>

<span data-ttu-id="3c7d0-167">오버 로드는 `MapHubs` 메서드를 사용 하는 사용자 지정 URL, 사용자 지정 종속성 확인자를 및 다음 옵션을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-167">Overloads of the `MapHubs` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="3c7d0-168">브라우저 클라이언트에서 도메인 간 호출을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-168">Enable cross-domain calls from browser clients.</span></span>

    <span data-ttu-id="3c7d0-169">일반적으로 브라우저에서 페이지를 로드 하는 경우 `http://contoso.com`, SignalR 연결에 동일한 도메인에 `http://contoso.com/signalr`입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-169">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="3c7d0-170">경우 페이지가 `http://contoso.com` 에 연결 `http://fabrikam.com/signalr`, 도메인 간 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-170">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="3c7d0-171">보안상의 이유로 기본적으로 도메인 간 연결을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-171">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="3c7d0-172">자세한 내용은 [ASP.NET SignalR 허브 API 가이드-JavaScript 클라이언트-도메인 간 연결을 설정 하는 방법을](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-172">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](index.md).</span></span>
- <span data-ttu-id="3c7d0-173">자세한 오류 메시지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-173">Enable detailed error messages.</span></span>

    <span data-ttu-id="3c7d0-174">오류가 발생 하면 SignalR의 기본 동작 내용에 대 한 세부 정보가 없는 알림 메시지를 클라이언트로 보내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-174">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="3c7d0-175">프로덕션 환경에서는 악의적인 사용자가 응용 프로그램에 대 한 공격의 정보를 사용 하는 일을 할 수 있습니다 클라이언트에 자세한 오류 정보를 보내지 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-175">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="3c7d0-176">문제를 해결 하려면 자세한 오류 보고를 일시적으로 사용 하도록 설정 하려면이 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-176">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="3c7d0-177">자동으로 생성 된 JavaScript 프록시 파일을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-177">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="3c7d0-178">기본적으로 허브 클래스에 대해 프록시를 사용 하 여 JavaScript 파일에 대 한 응답 URL "/ signalr 허브"로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-178">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="3c7d0-179">JavaScript 프록시를 사용 하지 않으려는 경우,이 파일을 수동으로 생성 하 고 클라이언트에 물리적 파일을 참조 하려는 경우에 프록시 생성을 사용 하지 않도록 설정 하려면이 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-179">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="3c7d0-180">자세한 내용은 [SignalR 허브 API 가이드-JavaScript 클라이언트-SignalR에 대 한 실제 파일을 만드는 방법에는 프록시 생성](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-180">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](index.md).</span></span>

<span data-ttu-id="3c7d0-181">다음 예제에서는 SignalR 연결 URL 및 이러한 옵션에 대 한 호출에서 지정 하는 방법의 `MapHubs` 메서드.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-181">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapHubs` method.</span></span> <span data-ttu-id="3c7d0-182">사용자 지정 URL을 지정 하려면 대체 "/ signalr"를 사용 하려는 URL 사용 하 여 예제에서입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-182">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample7.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="3c7d0-183">만들고 허브 클래스를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-183">How to create and use Hub classes</span></span>

<span data-ttu-id="3c7d0-184">허브를 만들려면에서 파생 되는 클래스를 만듭니다 [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-184">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="3c7d0-185">다음 예제에서는 채팅 응용 프로그램에 대 한 간단한 허브 클래스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-185">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample8.cs)]

<span data-ttu-id="3c7d0-186">이 예제에서는 연결 된 클라이언트가 호출할 수는 `NewContosoChatMessage` 메서드 및 모든 연결 된 클라이언트에 받은 데이터 브로드캐스트 될 경우.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-186">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="3c7d0-187">허브 개체 수명</span><span class="sxs-lookup"><span data-stu-id="3c7d0-187">Hub object lifetime</span></span>

<span data-ttu-id="3c7d0-188">허브 클래스를 인스턴스화할 하지 않거나 서버에서 사용자 고유의 코드에서 해당 메서드를 호출 합니다. SignalR 허브 파이프라인에 의해 수행 됩니다 모든 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-188">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="3c7d0-189">SignalR은 클라이언트를 연결, 연결 해제 또는 서버 메서드를 호출 작업을 수행 하면 같은 허브 작업을 처리 해야 할 때마다 허브 클래스의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-189">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="3c7d0-190">허브 클래스 인스턴스의 임시 이기 때문에 다음에 대 한 메서드 호출에서 상태를 유지 하기 위해 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-190">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="3c7d0-191">각 시간 서버의 메시지를 받습니다 메서드 호출을 허브 클래스 프로세스의 새 인스턴스를 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-191">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="3c7d0-192">여러 개의 연결 및 메서드 호출을 통해 상태를 유지 하려면 허브 클래스에서 파생 되지 않은 다른 클래스에는 데이터베이스 또는 정적 변수와 같은 일부 다른 메서드를 사용 `Hub`합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-192">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="3c7d0-193">메모리에서 데이터를 유지 하는 경우 허브 클래스에서 정적 변수와 같은 메서드를 사용 하 여 데이터 손실 됩니다 응용 프로그램 도메인 재활용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-193">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="3c7d0-194">허브 클래스 외부에서 실행 되는 사용자 고유의 코드에서 클라이언트로 메시지를 보내려는 경우 허브 클래스 인스턴스를 인스턴스화하여 그럴 수 없습니다 있지만 허브 클래스에 대 한 SignalR 컨텍스트 개체에 대 한 참조를 가져와서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-194">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="3c7d0-195">자세한 내용은 [클라이언트 메서드를 호출 하 여 허브 클래스 외부에서 그룹을 관리 하는 방법을](#callfromoutsidehub) 이 항목의에서 뒷부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-195">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="3c7d0-196">카멜식 대 / JavaScript 클라이언트에 허브 이름</span><span class="sxs-lookup"><span data-stu-id="3c7d0-196">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="3c7d0-197">기본적으로 JavaScript 클라이언트는 클래스 이름의 카멜식 대 / 소문자 버전을 사용 하 여 허브를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-197">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="3c7d0-198">SignalR 자동으로이 변경 되므로 JavaScript 코드는 JavaScript 규칙을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-198">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="3c7d0-199">앞의 예제로 간주 됩니다 `contosoChatHub` JavaScript 코드에서입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-199">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="3c7d0-200">**서버**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-200">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample9.cs?highlight=1)]

<span data-ttu-id="3c7d0-201">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-201">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample10.js?highlight=1)]

<span data-ttu-id="3c7d0-202">추가 사용 하는 클라이언트에 대 한 다른 이름을 지정 하려는 경우는 `HubName` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-202">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="3c7d0-203">사용 하는 경우는 `HubName` 특성는 JavaScript 클라이언트에서 카멜식 대 / 소문자 이름 변경 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-203">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="3c7d0-204">**서버**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-204">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample11.cs?highlight=1)]

<span data-ttu-id="3c7d0-205">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-205">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample12.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="3c7d0-206">여러 허브</span><span class="sxs-lookup"><span data-stu-id="3c7d0-206">Multiple Hubs</span></span>

<span data-ttu-id="3c7d0-207">응용 프로그램에서 여러 허브 클래스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-207">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="3c7d0-208">이렇게 하면 연결 공유 되지만 그룹은 별도:</span><span class="sxs-lookup"><span data-stu-id="3c7d0-208">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="3c7d0-209">모든 클라이언트가 동일한 URL을 사용 하 여 서비스를 사용 하 여 SignalR 연결 ("/ signalr" 또는 하나를 지정한 경우 사용자 지정 URL), 모든 허브에 대 한 연결을 사용 하 고 서비스에 의해 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-209">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="3c7d0-210">단일 클래스에서 정의 하는 모든 허브 기능에 비해 여러 허브에 대 한 성능 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-210">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="3c7d0-211">모든 허브에는 동일한 HTTP 요청 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-211">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="3c7d0-212">같은 연결을 공유 하는 모든 허브에 서버를 가져오는 유일한 HTTP 요청 정보 이므로 SignalR 연결을 설정 하는 원래 HTTP 요청에 무엇이.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-212">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="3c7d0-213">쿼리 문자열을 지정 하 여 클라이언트에서 서버로 정보를 전달 하는 연결 요청을 사용 하는 경우 쿼리 문자열이 서로 다른 여러 허브를 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-213">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="3c7d0-214">모든 허브에는 동일한 정보를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-214">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="3c7d0-215">생성된 된 JavaScript 프록시 파일에는 하나의 파일에 모든 허브에 대 한 프록시 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-215">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="3c7d0-216">JavaScript 프록시에 대 한 정보를 참조 하세요 [SignalR 허브 API 가이드-JavaScript 클라이언트-생성 된 프록시 및 용도를](index.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-216">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](index.md).</span></span>
- <span data-ttu-id="3c7d0-217">그룹 허브 내에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-217">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="3c7d0-218">SignalR을 정의할 수 있습니다 그룹에 브로드캐스트하는 연결 된 클라이언트의 하위 집합 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-218">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="3c7d0-219">그룹은 각 허브에 대해 개별적으로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-219">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="3c7d0-220">예를 들어, "Administrators" 라는 그룹을 하나의 집합에 대 한 클라이언트는 사용자 `ContosoChatHub` 클래스 및 그룹 이름이 같은 다양 한 클라이언트에 대 한 참조는 프로그램 `StockTickerHub` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-220">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="3c7d0-221">클라이언트에서 호출할 수 있는 허브 클래스에 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-221">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="3c7d0-222">클라이언트에서 호출할 수 있는 허브의 메서드를 노출 하려면 다음 예제와 같이 공용 메서드를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-222">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="3c7d0-223">반환 형식 및 C# 메서드에서 마찬가지로 복합 형식 및 배열 등 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-223">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="3c7d0-224">매개 변수에서 받거나 호출자에 게 반환 하는 모든 데이터는 JSON을 사용 하 여 클라이언트와 서버 간에 전송 되 고 자동으로 SignalR 처리 복잡 한 개체의 바인딩 및 개체의 배열 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-224">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="3c7d0-225">JavaScript 클라이언트에서 메서드 이름의 카멜식 대 / 소문자</span><span class="sxs-lookup"><span data-stu-id="3c7d0-225">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="3c7d0-226">기본적으로 JavaScript 클라이언트 허브 메서드를 메서드 이름의 카멜식 대 / 소문자 버전을 사용 하 여 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-226">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="3c7d0-227">SignalR 자동으로이 변경 되므로 JavaScript 코드는 JavaScript 규칙을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-227">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="3c7d0-228">**서버**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-228">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="3c7d0-229">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-229">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="3c7d0-230">추가 사용 하는 클라이언트에 대 한 다른 이름을 지정 하려는 경우는 `HubMethodName` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-230">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="3c7d0-231">**서버**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-231">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="3c7d0-232">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-232">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="3c7d0-233">비동기적으로 실행 하는 경우</span><span class="sxs-lookup"><span data-stu-id="3c7d0-233">When to execute asynchronously</span></span>

<span data-ttu-id="3c7d0-234">메서드는 수 장기 실행 또는 작업을 수행 해야 하는 경우에 대기 데이터베이스를 검색 하는 웹 서비스 호출 등을 포함를 반환 하 여 허브 메서드를 비동기화 하는 한 [태스크](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (대신 `void` 반환) 또는 [ 태스크&lt;T&gt; ](https://msdn.microsoft.com/library/dd321424.aspx) 개체 (대신 `T` 반환 형식).</span><span class="sxs-lookup"><span data-stu-id="3c7d0-234">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="3c7d0-235">반환 하는 경우는 `Task` SignalR 메서드에서 개체에 대 한 대기를 `Task` 를 완료 하려면 다음 보냅니다 래핑되지 않은 결과 클라이언트로 다시 이므로 클라이언트에서 메서드 호출을 코드 하는 방법에 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-235">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="3c7d0-236">허브 메서드를 만드는 비동기 방지 WebSocket 전송이 사용 하는 경우 연결을 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-236">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="3c7d0-237">허브 메서드를 동기적으로 실행 하 고 WebSocket 전송이 후속 호출에서 동일한 클라이언트 허브 메서드의 허브 메서드 완료 될 때까지 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-237">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="3c7d0-238">다음 예제와 동일한 방법을 동기적으로 실행 하도록 코딩 또는 버전 중 하나를 호출 하기 위한 작동 하는 JavaScript 클라이언트 코드에서 비동기적으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-238">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="3c7d0-239">**동기**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-239">**Synchronous**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="3c7d0-240">**비동기-ASP.NET 4.5**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-240">**Asynchronous - ASP.NET 4.5**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="3c7d0-241">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-241">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="3c7d0-242">ASP.NET 4.5의 비동기 메서드를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오 [ASP.NET MVC 4에서 비동기 메서드를 사용 하 여](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-242">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="3c7d0-243">오버 로드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-243">Defining Overloads</span></span>

<span data-ttu-id="3c7d0-244">메서드에 대 한 오버 로드를 정의 하려는 경우에 각 오버 로드에 매개 변수 수가 달라 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-244">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="3c7d0-245">다른 매개 변수 유형을 지정 하 여 오버 로드를 구별 하는 경우 허브 클래스는 컴파일되지만 SignalR service를 오버 로드 중 하나를 호출한 클라이언트 시도 하는 경우 런타임 시 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-245">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="3c7d0-246">허브 클래스에서 클라이언트 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-246">How to call client methods from the Hub class</span></span>

<span data-ttu-id="3c7d0-247">메서드를 호출할 클라이언트에서 서버를 사용 하 여는 `Clients` 허브 클래스에서 메서드에서는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-247">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="3c7d0-248">다음 예제에서는 호출 하는 서버 코드 `addNewMessageToPage` 연결 된 모든 클라이언트에 JavaScript 클라이언트에서 메서드를 정의 하는 클라이언트 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-248">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="3c7d0-249">**서버**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-249">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample22.cs?highlight=5)]

<span data-ttu-id="3c7d0-250">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-250">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample23.html?highlight=1)]

<span data-ttu-id="3c7d0-251">클라이언트; 메서드에서 반환 값을 가져올 수 없습니다. 와 같은 구문을 `int x = Clients.All.add(1,1)` 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-251">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="3c7d0-252">복합 형식 및 배열 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-252">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="3c7d0-253">다음 예제에서는 복합 형식을 메서드 매개 변수에 클라이언트에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-253">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="3c7d0-254">**복잡 한 개체를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-254">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample24.cs?highlight=3)]

<span data-ttu-id="3c7d0-255">**복합 개체를 정의 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-255">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample25.cs?highlight=1)]

<span data-ttu-id="3c7d0-256">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-256">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample26.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="3c7d0-257">RPC를 수신할 클라이언트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-257">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="3c7d0-258">클라이언트 속성은 반환 된 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) RPC를 수신할 클라이언트를 지정 하기 위한 몇 가지 옵션을 제공 하는 개체:</span><span class="sxs-lookup"><span data-stu-id="3c7d0-258">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="3c7d0-259">연결 된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-259">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample27.cs)]
- <span data-ttu-id="3c7d0-260">호출 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-260">Only the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="3c7d0-261">호출 클라이언트를 제외한 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-261">All clients except the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="3c7d0-262">특정 클라이언트 연결 ID로 식별</span><span class="sxs-lookup"><span data-stu-id="3c7d0-262">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample30.css)]

    <span data-ttu-id="3c7d0-263">이 예제에서는 호출 `addContosoChatMessageToPage` 호출 클라이언트에서 사용 하는 것과 동일한 효과가 및 `Clients.Caller`합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-263">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="3c7d0-264">연결 된 모든 클라이언트를 제외 하 고 지정 된 클라이언트 연결 ID로 식별</span><span class="sxs-lookup"><span data-stu-id="3c7d0-264">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample31.cs)]
- <span data-ttu-id="3c7d0-265">지정된 된 그룹에 연결 된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-265">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample32.css)]
- <span data-ttu-id="3c7d0-266">지정된 된 그룹에 연결 된 모든 클라이언트를 제외 하 고 지정 된 클라이언트 연결 ID로 식별</span><span class="sxs-lookup"><span data-stu-id="3c7d0-266">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample33.cs)]
- <span data-ttu-id="3c7d0-267">지정된 된 그룹에 연결 된 모든 클라이언트 호출 클라이언트를 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-267">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample34.css)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="3c7d0-268">메서드 이름에 대 한 컴파일 시간 유효성 검사 없음</span><span class="sxs-lookup"><span data-stu-id="3c7d0-268">No compile-time validation for method names</span></span>

<span data-ttu-id="3c7d0-269">지정 하는 메서드 이름에 대 한 컴파일 시간 유효성 검사 나 IntelliSense 즉 동적 개체로 해석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-269">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="3c7d0-270">식은 런타임에 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-270">The expression is evaluated at run time.</span></span> <span data-ttu-id="3c7d0-271">메서드 호출이 실행 될 때 메서드가 호출 되도록, SignalR 메서드 이름과 매개 변수 값을 클라이언트에 보내고는 이름과 일치 하는 경우 클라이언트에 메서드 및 매개 변수 값에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-271">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="3c7d0-272">일치 하는 메서드가 없는 클라이언트에 있으면 오류가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-272">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="3c7d0-273">SignalR 클라이언트 메서드를 호출할 때 백그라운드에서 클라이언트로 전송 하는 데이터의 형식에 대 한 정보를 참조 하세요 [SignalR 소개](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-273">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](index.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="3c7d0-274">대/소문자 메서드 이름 일치</span><span class="sxs-lookup"><span data-stu-id="3c7d0-274">Case-insensitive method name matching</span></span>

<span data-ttu-id="3c7d0-275">메서드 이름 일치는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-275">Method name matching is case-insensitive.</span></span> <span data-ttu-id="3c7d0-276">예를 들어 `Clients.All.addContosoChatMessageToPage` 서버에서 실행 됩니다 `AddContosoChatMessageToPage`를 `addcontosochatmessagetopage`, 또는 `addContosoChatMessageToPage` 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-276">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="3c7d0-277">비동기 실행</span><span class="sxs-lookup"><span data-stu-id="3c7d0-277">Asynchronous execution</span></span>

<span data-ttu-id="3c7d0-278">호출 하는 메서드를 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-278">The method that you call executes asynchronously.</span></span> <span data-ttu-id="3c7d0-279">SignalR 클라이언트에 데이터를 전송 하 여 코드의 다음 줄은 메서드 완료 시 대기 해야 함을 지정 하지 않으면 완료 될 때까지 기다리지 않고 즉시 실행 됩니다 클라이언트 메서드 호출 후 제공 되는 모든 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-279">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="3c7d0-280">두 클라이언트 메서드를 순차적으로 실행 하는 방법을 보여 줍니다. 다음 코드 예제를 사용 하 여.NET 4.5에서 작동 하는 코드가, 하나 하나를 사용 하 여.NET 4에서 작동 하는 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-280">The following code examples show how to execute two client methods sequentially, one using code that works in .NET 4.5, and one using code that works in .NET 4.</span></span>

<span data-ttu-id="3c7d0-281">**.NET 4.5 예제**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-281">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample35.cs?highlight=1,3)]

<span data-ttu-id="3c7d0-282">**.NET 4 예제**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-282">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample36.cs?highlight=3-4)]

<span data-ttu-id="3c7d0-283">사용 하는 경우 `await` 또는 `ContinueWith` 클라이언트 메서드 코드의 다음 줄을 실행 하기 전에 완료 될 때까지 대기할 의미는 아닙니다 클라이언트 코드의 다음 줄이 실행 되기 전에 메시지가 표시 실제로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-283">If you use `await` or `ContinueWith` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="3c7d0-284">클라이언트 메서드 호출의 "완료"는 SignalR 모든 작업을 완료 메시지를 보내는 데 필요한 것을 의미할 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-284">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="3c7d0-285">클라이언트 메시지를 수신 했다고 확인을 할 경우이 메커니즘을 직접 프로그래밍 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-285">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="3c7d0-286">예를 들어, 코딩할 수는 `MessageReceived` 허브 및 메서드를 `addContosoChatMessageToPage` 메서드를 호출할 수 있습니다 클라이언트 `MessageReceived` 작업을 수행한 후 클라이언트에서 수행 해야 하면 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-286">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="3c7d0-287">`MessageReceived` 허브에서 할 수 있는 실제 클라이언트 수신 및 처리 원래 메서드 호출의 모든 작업에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-287">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="3c7d0-288">메서드 이름으로 문자열 변수를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-288">How to use a string variable as the method name</span></span>

<span data-ttu-id="3c7d0-289">캐스팅 메서드 이름으로 문자열 변수를 사용 하 여 클라이언트 메서드를 호출 하려는 경우 `Clients.All` (또는 `Clients.Others`를 `Clients.Caller`등)에 `IClientProxy` 호출 [(methodName, args...) 호출 ](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="3c7d0-289">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample37.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="3c7d0-290">허브 클래스에서 그룹 멤버 자격을 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-290">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="3c7d0-291">SignalR에서 그룹에 연결 된 클라이언트의 지정 된 하위 집합에 메시지 브로드캐스트 하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-291">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="3c7d0-292">그룹의 클라이언트에서 모든 수 있고 클라이언트가 여러 그룹의 멤버일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-292">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="3c7d0-293">그룹 멤버 자격을 관리 하려면 사용 합니다 [추가](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 및 [제거](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) 에서 제공 하는 메서드는 `Groups` 허브 클래스의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-293">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="3c7d0-294">다음 예제에서는 합니다 `Groups.Add` 및 `Groups.Remove` 호출 하는 JavaScript 클라이언트 코드 뒤에 클라이언트 코드에서 호출 되는 허브 메서드에서 사용 되는 메서드.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-294">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="3c7d0-295">**서버**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-295">**Server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample38.cs?highlight=5,10)]

<span data-ttu-id="3c7d0-296">**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-296">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample39.js)]

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample40.js)]

<span data-ttu-id="3c7d0-297">명시적으로 그룹을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-297">You don't have to explicitly create groups.</span></span> <span data-ttu-id="3c7d0-298">그룹을 처음에 대 한 호출에 해당 이름을 지정 하는 자동으로 생성 하는 적용 `Groups.Add`, 마지막 연결에 대 한 멤버 자격에서 제거할 때 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-298">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="3c7d0-299">그룹 멤버 자격 목록 또는 그룹 목록을 가져오기 위한 API는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-299">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="3c7d0-300">SignalR 클라이언트와 그룹을 기반으로 메시지를 보냅니다는 [pub/sub 모델](http://en.wikipedia.org/wiki/Publish/subscribe), 서버 그룹 또는 그룹 멤버 자격 목록이 유지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-300">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="3c7d0-301">이렇게 하면 확장성을 최대화 하기 때문에 웹 팜에 노드를 추가할 때마다 SignalR 유지 관리 하는 모든 상태를 새 노드에 전파 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-301">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="3c7d0-302">비동기 실행의 Add 및 Remove 메서드</span><span class="sxs-lookup"><span data-stu-id="3c7d0-302">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="3c7d0-303">합니다 `Groups.Add` 고 `Groups.Remove` 메서드가 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-303">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="3c7d0-304">있는지 확인 해야 하는 그룹에 클라이언트를 추가 하 고 즉시 그룹을 사용 하 여 클라이언트에 메시지를 송신 하려는 경우는 `Groups.Add` 메서드는 먼저 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-304">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="3c7d0-305">다음 코드 예제에서는 그렇게 하는 방법,.NET 4.5 및.NET 4에서 작동 하는 코드를 사용 하 여 작동 하는 코드를 사용 하 여 하나를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-305">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4</span></span>

<span data-ttu-id="3c7d0-306">**.NET 4.5 예제**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-306">**.NET 4.5 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="3c7d0-307">**.NET 4 예제**</span><span class="sxs-lookup"><span data-stu-id="3c7d0-307">**.NET 4 example**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample42.cs?highlight=3-4)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="3c7d0-308">그룹 멤버 자격 지 속성</span><span class="sxs-lookup"><span data-stu-id="3c7d0-308">Group membership persistence</span></span>

<span data-ttu-id="3c7d0-309">SignalR 연결을 추적, 사용자 수 있도록 하려면 동일한 그룹에 사용자 설정 될 때마다 연결 하려는 사용자가 아닌 경우에 따라서, 호출 해야 `Groups.Add` 될 때마다 사용자는 새 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-309">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="3c7d0-310">연결 손실로 임시 후 때때로 SignalR 복원할 수 연결이 자동으로.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-310">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="3c7d0-311">이런 경우 SignalR은 동일한 연결을 새 연결을 설정 하지 복원과 하므로 클라이언트의 그룹 멤버 자격 자동으로 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-311">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="3c7d0-312">왜냐하면 가능한 임시 중단 서버를 다시 부팅 또는 실패의 결과가 하는 경우에 그룹 멤버 자격을 포함 하 여 각 클라이언트에 대 한 연결 상태를 클라이언트로 라운드트립 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-312">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="3c7d0-313">서버 다운 하 고 새 서버 연결 시간이 초과 되기 전에 바뀝니다, 클라이언트 새 서버에 자동으로 다시 연결 하 고 그룹의 멤버인에 다시 등록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-313">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="3c7d0-314">연결의 연결 손실 후 자동으로 복원할 수 없는 경우 연결 시간이 종료 될 때 또는 클라이언트의 연결을 끊습니다 (예를 들어 경우 브라우저를 새 페이지로 이동) 하는 경우, 그룹 멤버 자격 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-314">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="3c7d0-315">다음에 사용자 연결에 대 한 새 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-315">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="3c7d0-316">파일을 동일한 사용자는 새 연결을 설정 하는 경우 그룹 멤버 자격을 유지 하려면 응용 프로그램에 사용자와 그룹 간의 연결을 추적 하 고 될 때마다 새 연결을 설정 하는 사용자 그룹 멤버 자격을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-316">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="3c7d0-317">연결 및 다시 연결 하는 방법에 대 한 자세한 내용은 참조 하세요. [허브 클래스에서 연결 수명 이벤트를 처리 하는 방법을](#connectionlifetime) 이 항목의에서 뒷부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-317">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="3c7d0-318">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="3c7d0-318">Single-user groups</span></span>

<span data-ttu-id="3c7d0-319">SignalR을 일반적으로 사용 하는 응용 프로그램 사용자 메시지를 전송한 및 사용자는 메시지를 받을 수 해야 확인 하기 위해 사용자와 연결 간 연결을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-319">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="3c7d0-320">그룹 작업을 수행 하는 일반적으로 사용 되는 두 가지 패턴 중 하나에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-320">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="3c7d0-321">단일 사용자 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-321">Single-user groups.</span></span>

    <span data-ttu-id="3c7d0-322">그룹 이름으로 사용자 이름을 지정 하 고 사용자 연결 되거나 다시 연결 될 때마다 현재 연결 ID를 그룹에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-322">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="3c7d0-323">사용자에 게 메시지를 보내도록 그룹에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-323">To send messages to the user you send to the group.</span></span> <span data-ttu-id="3c7d0-324">이 방법의 단점은 그룹 기능은 제공 되지 않습니다 사용자 온라인 또는 오프 라인 인지 확인 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-324">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="3c7d0-325">사용자 이름 및 연결 Id 간의 연결을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-325">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="3c7d0-326">사전 또는 데이터베이스에서 각 사용자 이름 및 하나 이상의 연결 Id 간의 연결을 저장 하 고 사용자 연결 또는 연결 해제 될 때마다 저장된 된 데이터를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-326">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="3c7d0-327">사용자에 게 메시지를 보낼 연결 Id를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-327">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="3c7d0-328">이 방법의 단점은 더 많은 메모리는입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-328">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="3c7d0-329">허브 클래스에서 연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-329">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="3c7d0-330">연결 수명 이벤트를 처리 하는 것에 대 한 일반적인 이유는 여부는 사용자가 연결 되어 있는지 여부를 추적 하 고 사용자 이름 및 연결 Id 간의 연결을 추적 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-330">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="3c7d0-331">클라이언트 연결 하거나 연결을 끊을 때 사용자 고유의 코드를 실행 하려면 재정의 `OnConnected`, `OnDisconnected`, 및 `OnReconnected` 다음 예제에서와 같이 허브의 가상 메서드 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-331">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample43.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="3c7d0-332">OnConnected, OnDisconnected, 및 OnReconnected 호출 될 때</span><span class="sxs-lookup"><span data-stu-id="3c7d0-332">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="3c7d0-333">브라우저는 새 페이지를 이동할 때마다 새 연결에 설정 되어야 즉, SignalR 실행될지를 `OnDisconnected` 메서드를 호출한는 `OnConnected` 메서드.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-333">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="3c7d0-334">SignalR 새 연결이 설정 될 때 항상 새 연결 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-334">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="3c7d0-335">`OnReconnected` 경우 케이블을는 일시적으로 연결이 끊어지고 연결 시간이 초과 되기 전에 다시 연결 등에서 SignalR 수 자동으로 복구 하는 연결에서 임시 중단 되었을 때 메서드가 호출 됩니다. `OnDisconnected` 메서드는 클라이언트는 연결이 끊어집니다 및 SignalR 자동으로 다시 연결할 수 없습니다, 브라우저를 새 페이지로 이동 하는 경우와 같은 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-335">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="3c7d0-336">따라서 가능한 지정된 된 클라이언트에 대 한 이벤트 시퀀스가 `OnConnected`, `OnReconnected`를 `OnDisconnected`; 또는 `OnConnected`, `OnDisconnected`합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-336">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="3c7d0-337">시퀀스를 표시 하지 않습니다 `OnConnected`, `OnDisconnected`, `OnReconnected` 지정된 된 연결에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-337">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="3c7d0-338">`OnDisconnected` 메서드 서버가 중단 등의 일부 시나리오에서 호출 하지 않습니다 또는 응용 프로그램 도메인 재활용을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-338">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="3c7d0-339">일부 클라이언트를 다시 연결 하 고 실행 하는 일을 할 수 있습니다 다른 서버가 온라인 상태가 또는 응용 프로그램 도메인의 재생을 완료 하는 경우는 `OnReconnected` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-339">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="3c7d0-340">자세한 내용은 [이해 및 SignalR의 연결 수명 이벤트 처리](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-340">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="3c7d0-341">채워지지 호출자 상태</span><span class="sxs-lookup"><span data-stu-id="3c7d0-341">Caller state not populated</span></span>

<span data-ttu-id="3c7d0-342">즉에 삽입 하는 모든 상태는 서버에서 연결 수명 이벤트 처리기 메서드를 호출 되는 `state` 클라이언트 개체에서 채워지지 것입니다을 `Caller` 서버의 속성.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-342">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="3c7d0-343">에 대 한 자세한 합니다 `state` 개체 및 `Caller` 속성을 참조 하세요 [클라이언트와 허브 클래스 간의 상태를 전달 하는 방법을](#passstate) 이 항목의 뒷부분에 나오는.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-343">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="3c7d0-344">컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-344">How to get information about the client from the Context property</span></span>

<span data-ttu-id="3c7d0-345">클라이언트에 대 한 정보를 가져오려면는 `Context` 허브 클래스의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-345">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="3c7d0-346">합니다 `Context` 속성에서 반환 된 [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) 다음 정보에 대 한 액세스를 제공 하는 개체:</span><span class="sxs-lookup"><span data-stu-id="3c7d0-346">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="3c7d0-347">호출 클라이언트의 연결 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-347">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample44.cs?highlight=1)]

    <span data-ttu-id="3c7d0-348">연결 ID는 SignalR (사용자 고유의 코드에서 값을 지정할 수 없습니다.)가 할당 하는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-348">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="3c7d0-349">각 연결과 동일한 연결 응용 프로그램에서 여러 허브를 설정한 경우 모든 허브에서 ID를 사용 하는 것에 대 한 연결 ID를 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-349">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="3c7d0-350">HTTP 헤더 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-350">HTTP header data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample45.cs?highlight=1)]

    <span data-ttu-id="3c7d0-351">HTTP 헤더를 가져올 수도 있습니다 `Context.Headers`합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-351">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="3c7d0-352">동일한 작업에 대 한 여러 참조에 대 한 이유는 `Context.Headers` 먼저 만들어진 합니다 `Context.Request` 속성은 나중에 추가 되었습니다 및 `Context.Headers` 이전 버전과 호환성을 위해 유지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-352">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="3c7d0-353">문자열 데이터를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-353">Query string data.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample46.cs?highlight=1)]

    <span data-ttu-id="3c7d0-354">쿼리 문자열 데이터를 가져올 수도 있습니다 `Context.QueryString`합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-354">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="3c7d0-355">이 속성에서 수행 되는 쿼리 문자열은 SignalR 연결을 설정 하는 HTTP 요청에 사용 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-355">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="3c7d0-356">서버에 클라이언트에서 클라이언트에 대 한 데이터를 전달 하는 편리한 방법에 따라 연결을 구성 하 여 클라이언트에서 쿼리 문자열 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-356">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="3c7d0-357">다음 예제에서는 생성 된 프록시를 사용 하는 경우 JavaScript 클라이언트에서 쿼리 문자열을 추가 하는 한 가지 방법은 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-357">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample47.js?highlight=1)]

    <span data-ttu-id="3c7d0-358">쿼리 문자열 매개 변수를 설정 하는 방법에 대 한 자세한 내용은 API 설명서를 참조 합니다 [JavaScript](index.md) 하 고 [.NET](index.md) 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-358">For more information about setting query string parameters, see the API guides for the [JavaScript](index.md) and [.NET](index.md) clients.</span></span>

    <span data-ttu-id="3c7d0-359">SignalR에서 내부적으로 사용 하는 몇 가지 다른 값과 함께 쿼리 문자열 데이터를 연결에 사용 되는 전송 메서드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-359">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample48.cs)]

    <span data-ttu-id="3c7d0-360">변수의 `transportMethod` "Websocket", "serverSentEvents", "foreverFrame" 또는 "longPolling" 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-360">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="3c7d0-361">이 값을 확인 하는 경우는 `OnConnected` 이벤트 처리기 메서드를 일부 시나리오에서 발생할 수 있습니다 처음에 연결에 대 한 최종 협상 된 전송 메서드 없는 전송 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-361">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="3c7d0-362">이 경우 메서드는 예외가 throw 됩니다 하 고 최종 전송을 설정 되 면 나중에 다시 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-362">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="3c7d0-363">쿠키입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-363">Cookies.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="3c7d0-364">쿠키를 가져올 수도 있습니다 `Context.RequestCookies`합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-364">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="3c7d0-365">사용자 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-365">User information.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample50.cs?highlight=1)]
- <span data-ttu-id="3c7d0-366">요청에 대 한 HttpContext 개체:</span><span class="sxs-lookup"><span data-stu-id="3c7d0-366">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample51.cs?highlight=1)]

    <span data-ttu-id="3c7d0-367">이 메서드를 사용 하 여 시작 하는 대신 `HttpContext.Current` 가져오려고 합니다 `HttpContext` SignalR 연결에 대 한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-367">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="3c7d0-368">클라이언트와 허브 클래스 간의 상태를 전달 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-368">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="3c7d0-369">클라이언트 프록시는 제공 된 `state` 개체는 각 메서드 호출을 사용 하 여 서버에 전송 하려는 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-369">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="3c7d0-370">서버에서이 데이터에 액세스할 수는 `Clients.Caller` 허브 메서드에서 클라이언트에서 호출 되는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-370">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="3c7d0-371">합니다 `Clients.Caller` 연결 수명 이벤트 처리기 메서드에 대 한 속성은 채워지지 않습니다 `OnConnected`를 `OnDisconnected`, 및 `OnReconnected`합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-371">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="3c7d0-372">만들거나의 데이터를 업데이트 합니다 `state` 개체 및 `Clients.Caller` 속성이 두 방향 모두에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-372">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="3c7d0-373">서버에서 값을 업데이트할 수 있습니다 하 고 클라이언트에 다시 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-373">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="3c7d0-374">다음 예제에서는 모든 메서드 호출을 사용 하 여 서버에 전송에 대 한 상태를 저장 하는 JavaScript 클라이언트 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-374">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample52.js?highlight=1-2)]

<span data-ttu-id="3c7d0-375">다음 예제에서는.NET 클라이언트에서 해당 하는 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-375">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample53.cs?highlight=1-2)]

<span data-ttu-id="3c7d0-376">허브 클래스에서이 데이터에 액세스할 수 있습니다는 `Clients.Caller` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-376">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="3c7d0-377">다음 예제에서는 이전 예제에서 참조 하는 상태를 검색 하는 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-377">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample54.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="3c7d0-378">지속 상태에 대 한이 메커니즘을 사용할 수 없습니다 많은 양의 데이터에 넣으면 모든 이후 합니다 `state` 또는 `Clients.Caller` 속성은 모든 메서드 호출을 사용 하 여 라운드트립 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-378">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="3c7d0-379">사용자 이름이 나 카운터 같은 더 작은 항목에 대 한 두는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-379">It's useful for smaller items such as user names or counters.</span></span>


<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="3c7d0-380">허브 클래스에서 오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-380">How to handle errors in the Hub class</span></span>

<span data-ttu-id="3c7d0-381">허브 클래스 메서드에서 발생 하는 오류를 처리 하려면 다음 방법 중 하나 또는 모두를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-381">To handle errors that occur in your Hub class methods, use one or both of the following methods:</span></span>

- <span data-ttu-id="3c7d0-382">Try / catch 블록에서 메서드 코드를 래핑하고 예외 개체를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-382">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="3c7d0-383">디버깅 목적으로 클라이언트에 예외를 보낼 수 있지만 보안상의 이유로 프로덕션의 클라이언트에 자세한 정보를 보내는 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-383">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="3c7d0-384">처리 하는 허브 파이프라인 모듈을 만들어야 합니다 [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-384">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="3c7d0-385">다음 예제에서는 global.asax 허브 파이프라인에 모듈을 삽입 하는 코드 뒤에 오류를 기록 하는 파이프라인 모듈을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-385">The following example shows a pipeline module that logs errors, followed by code in Global.asax that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample55.cs)]

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample56.cs?highlight=3)]

<span data-ttu-id="3c7d0-386">Hub 파이프라인 모듈에 대 한 자세한 내용은 참조 하세요. [Hubs 파이프라인 사용자 지정 하는 방법을](#hubpipeline) 이 항목의에서 뒷부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-386">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="3c7d0-387">추적을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-387">How to enable tracing</span></span>

<span data-ttu-id="3c7d0-388">서버 쪽 추적을 사용 하려면이 예와 같이 system.diagnostics 요소를 Web.config 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-388">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample57.html?highlight=17-72)]

<span data-ttu-id="3c7d0-389">Visual Studio에서 응용 프로그램을 실행 하는 경우 로그를 볼 수 있습니다 합니다 **출력** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-389">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="3c7d0-390">클라이언트 메서드를 호출 하 고 허브 클래스 외부에서 그룹을 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-390">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="3c7d0-391">메서드를 호출할 클라이언트 허브 클래스와는 다른 클래스에서 허브에 대 한 SignalR 컨텍스트 개체에 대 한 참조를 가져와 클라이언트에서 메서드를 호출 하거나 그룹을 관리 하는 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-391">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="3c7d0-392">다음 샘플 `StockTicker` 클래스는 컨텍스트 개체를 가져옵니다, 클래스의 인스턴스에 저장, 클래스 인스턴스는 정적 속성에 저장 및 singleton 클래스 인스턴스에서 컨텍스트를 사용 하 여 호출 하 여 `updateStockPrice` 메서드는 클라이언트에서 명명 된 허브에 연결 `StockTickerHub`합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-392">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample58.cs?highlight=8,24)]

<span data-ttu-id="3c7d0-393">수명이 긴 개체에서 상황에 맞는 여러 번 사용 하는 경우 참조를 한 번 가져와 저장 될 때마다 다시 것 보다는 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-393">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="3c7d0-394">컨텍스트를 한 번 시작 하면 SignalR 순서는 허브 메서드 확인 클라이언트 메서드 호출의 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-394">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="3c7d0-395">허브에 대해 SignalR 컨텍스트를 사용 하는 방법을 보여 주는 자습서를 참조 하세요 [ASP.NET SignalR을 사용 하 여 서버 브로드캐스트](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-395">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](index.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="3c7d0-396">클라이언트 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-396">Calling client methods</span></span>

<span data-ttu-id="3c7d0-397">클라이언트 RPC를 받을 지정할 수 있지만 허브 클래스에서 호출 하는 경우 보다 더 적은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-397">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="3c7d0-398">이러한 이유로 없다는 컨텍스트 클라이언트에서 특정 호출과 관련 된 모든 메서드는 필요 현재 연결 ID의 기술 자료와 같은 `Clients.Others`, 또는 `Clients.Caller`, 또는 `Clients.OthersInGroup`를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-398">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="3c7d0-399">다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-399">The following options are available:</span></span>

- <span data-ttu-id="3c7d0-400">연결 된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-400">All connected clients.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample59.cs)]
- <span data-ttu-id="3c7d0-401">특정 클라이언트 연결 ID로 식별</span><span class="sxs-lookup"><span data-stu-id="3c7d0-401">A specific client identified by connection ID.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample60.css)]
- <span data-ttu-id="3c7d0-402">연결 된 모든 클라이언트를 제외 하 고 지정 된 클라이언트 연결 ID로 식별</span><span class="sxs-lookup"><span data-stu-id="3c7d0-402">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample61.cs)]
- <span data-ttu-id="3c7d0-403">지정된 된 그룹에 연결 된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-403">All connected clients in a specified group.</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample62.css)]
- <span data-ttu-id="3c7d0-404">연결 ID로 식별 하는 지정 된 클라이언트를 제외한 지정된 된 그룹의 모든 연결 된 클라이언트</span><span class="sxs-lookup"><span data-stu-id="3c7d0-404">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample63.cs)]

<span data-ttu-id="3c7d0-405">현재 연결 ID를 전달 하 고 사용 하 여 사용 하 여 호출 하는 경우 비-허브 클래스에 메서드에서 허브 클래스에서를 `Clients.Client`, `Clients.AllExcept`, 또는 `Clients.Group` 시뮬레이션 `Clients.Caller`, `Clients.Others`, 또는 `Clients.OthersInGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-405">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="3c7d0-406">다음 예제에서는 `MoveShapeHub` 연결 ID를 전달 하는 클래스를 `Broadcaster` 클래스 있도록를 `Broadcaster` 클래스를 시뮬레이션할 수 있습니다 `Clients.Others`.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-406">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample64.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="3c7d0-407">그룹 멤버 자격 관리</span><span class="sxs-lookup"><span data-stu-id="3c7d0-407">Managing group membership</span></span>

<span data-ttu-id="3c7d0-408">그룹 관리를 위한 허브 클래스에서와 마찬가지로 동일한 옵션 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-408">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="3c7d0-409">클라이언트 그룹에 추가</span><span class="sxs-lookup"><span data-stu-id="3c7d0-409">Add a client to a group</span></span>

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample65.cs)]
- <span data-ttu-id="3c7d0-410">그룹에서 클라이언트 제거</span><span class="sxs-lookup"><span data-stu-id="3c7d0-410">Remove a client from a group</span></span>

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample66.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="3c7d0-411">허브 파이프라인 사용자 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c7d0-411">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="3c7d0-412">SignalR을 사용 하면 허브 파이프라인에 사용자 고유의 코드를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-412">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="3c7d0-413">다음 예제에서는 클라이언트와 클라이언트에서 보내는 메서드 호출에서 받은 각 들어오는 메서드 호출을 기록 하는 사용자 지정 허브 파이프라인 모듈을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-413">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample67.cs)]

<span data-ttu-id="3c7d0-414">다음 코드를 *Global.asax* 허브 파이프라인에서 실행 하려면 모듈을 등록 하는 파일:</span><span class="sxs-lookup"><span data-stu-id="3c7d0-414">The following code in the *Global.asax* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample68.cs?highlight=3)]

<span data-ttu-id="3c7d0-415">재정의할 수 있는 여러 가지 방법 이며</span><span class="sxs-lookup"><span data-stu-id="3c7d0-415">There are many different methods that you can override.</span></span> <span data-ttu-id="3c7d0-416">전체 목록을 참조 하세요 [HubPipelineModule 메서드](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c7d0-416">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
