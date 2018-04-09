---
title: ASP.NET Core SignalR 소개
author: rachelappel
description: ASP.NET Core SignalR 라이브러리 간소화 앱에 실시간 웹 기능을 추가 하는 방법을 알아봅니다.
manager: wpickett
ms.author: rachelap
ms.custom: mvc
ms.date: 03/07/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/introduction
ms.openlocfilehash: 2da6737c09ab922b0e02c1dfeba3b1808c98ea4c
ms.sourcegitcommit: 71b93b42cbce8a9b1a12c4d88391e75a4dfb6162
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2018
---
# <a name="introduction-to-aspnet-core-signalr"></a><span data-ttu-id="80a63-103">ASP.NET Core SignalR 소개</span><span class="sxs-lookup"><span data-stu-id="80a63-103">Introduction to ASP.NET Core SignalR</span></span>

<span data-ttu-id="80a63-104">작성자: [Rachel Appel](https://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="80a63-104">By [Rachel Appel](https://twitter.com/rachelappel)</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="80a63-105">SignalR 란?</span><span class="sxs-lookup"><span data-stu-id="80a63-105">What is SignalR?</span></span>

<span data-ttu-id="80a63-106">ASP.NET Core SignalR은 간소화 실시간 웹 기능을 응용 프로그램을 추가 하는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-106">ASP.NET Core SignalR is a library that simplifies adding real-time web functionality to apps.</span></span> <span data-ttu-id="80a63-107">실시간 웹 기능을 통해 서버 쪽 코드를 클라이언트에 푸시 콘텐츠 즉시 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-107">Real-time web functionality enables server-side code to push content to clients instantly.</span></span>

<span data-ttu-id="80a63-108">SignalR 하기에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-108">Good candidates for SignalR:</span></span>

* <span data-ttu-id="80a63-109">서버에서 자주 발생 하는 업데이트를 필요로 하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-109">Apps that require high frequency updates from the server.</span></span> <span data-ttu-id="80a63-110">예로 게임, 소셜 네트워크, 투표, 경매, 맵 및 GPS 앱에는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-110">Examples are gaming, social networks, voting, auction, maps, and GPS apps.</span></span>
* <span data-ttu-id="80a63-111">대시보드 및 모니터링 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-111">Dashboards and monitoring apps.</span></span> <span data-ttu-id="80a63-112">예로 회사 대시보드를 인스턴트 판매 업데이트 하거나 경고를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-112">Examples include company dashboards, instant sales updates, or travel alerts.</span></span>
* <span data-ttu-id="80a63-113">공동 작업 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-113">Collaborative apps.</span></span> <span data-ttu-id="80a63-114">화이트 보드 앱과 소프트웨어를 충족 하는 팀은 공동 작업 응용 프로그램의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-114">Whiteboard apps and team meeting software are examples of collaborative apps.</span></span>
* <span data-ttu-id="80a63-115">알림이 필요로 하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-115">Apps that require notifications.</span></span> <span data-ttu-id="80a63-116">소셜 네트워크, 전자 메일, 채팅, 게임, 여행 경고 및 다른 많은 응용 프로그램 알림을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-116">Social networks, email, chat, games, travel alerts, and many other apps use notifications.</span></span>

<span data-ttu-id="80a63-117">서버-클라이언트를 만들기 위한 API를 제공 하는 SignalR [원격 프로시저 호출 (RPC)](https://wikipedia.org/wiki/Remote_procedure_call)합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-117">SignalR provides an API for creating server-to-client [remote procedure calls (RPC)](https://wikipedia.org/wiki/Remote_procedure_call).</span></span> <span data-ttu-id="80a63-118">Rpc 서버 쪽.NET Core 코드에서 클라이언트에서 JavaScript 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-118">The RPCs call JavaScript functions on clients from server-side .NET Core code.</span></span>

<span data-ttu-id="80a63-119">ASP.NET Core 용 SignalR:</span><span class="sxs-lookup"><span data-stu-id="80a63-119">SignalR for ASP.NET Core:</span></span>

* <span data-ttu-id="80a63-120">연결 관리를 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-120">Handles connection management automatically.</span></span>
* <span data-ttu-id="80a63-121">연결 된 모든 클라이언트에 동시에 메시지를 브로드캐스트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-121">Enables broadcasting messages to all connected clients simultaneously.</span></span> <span data-ttu-id="80a63-122">예를 들어: 채트 방 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-122">For example, a chat room.</span></span>
* <span data-ttu-id="80a63-123">특정 클라이언트 또는 그룹의 클라이언트에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-123">Enables sending messages to specific clients or groups of clients.</span></span>
* <span data-ttu-id="80a63-124">오픈 소스는 [GitHub](https://github.com/aspnet/signalr)합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-124">Is open-sourced at [GitHub](https://github.com/aspnet/signalr).</span></span>
* <span data-ttu-id="80a63-125">확장 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-125">Scalable.</span></span>

<span data-ttu-id="80a63-126">클라이언트와 서버 간의 연결이 HTTP 연결과 달리 지속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-126">The connection between the client and server is persistent, unlike an HTTP connection.</span></span>

## <a name="transports"></a><span data-ttu-id="80a63-127">전송</span><span class="sxs-lookup"><span data-stu-id="80a63-127">Transports</span></span>

<span data-ttu-id="80a63-128">다양 한 기술을 갖추고 실시간 웹 응용 프로그램을 통해 SignalR 간단히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-128">SignalR abstracts over a number of techniques for building real-time web applications.</span></span> <span data-ttu-id="80a63-129">[Websocket](https://tools.ietf.org/html/rfc7118) 는 최적의 전송 되지만 해당 장치가 사용할 수 없는 경우 Server-Sent 이벤트 및 긴 폴링와 같은 다른 기법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-129">[WebSockets](https://tools.ietf.org/html/rfc7118) is the optimal transport, but other techniques like Server-Sent Events and Long Polling can be used when those aren't available.</span></span> <span data-ttu-id="80a63-130">SignalR에서는 자동으로 검색 하 고 서버와 클라이언트에서 지원 되는 기능을 기반으로 적절 한 전송을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-130">SignalR will automatically detect and initialize the appropriate transport based on features supported on the server and client.</span></span>

## <a name="hubs-and-endpoints"></a><span data-ttu-id="80a63-131">허브 및 끝점</span><span class="sxs-lookup"><span data-stu-id="80a63-131">Hubs and Endpoints</span></span>

<span data-ttu-id="80a63-132">SignalR 허브와 끝점을 사용 하 여 클라이언트와 서버 간 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-132">SignalR uses Hubs and Endpoints to communicate between clients and servers.</span></span> <span data-ttu-id="80a63-133">허브 API에서는 대부분의 시나리오에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-133">The Hubs API covers the most scenarios.</span></span>

<span data-ttu-id="80a63-134">허브는 클라이언트와 서버에서 다른 메서드를 호출할 수 있도록 하는 끝점 API를 기반으로 하는 높은 수준의 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-134">A hub is a high-level pipeline built upon the Endpoint API that allows your client and server to call methods on each other.</span></span> <span data-ttu-id="80a63-135">클라이언트가 서버에서 로컬 메서드로 쉽게 그 반대의으로 메서드를 호출할 수 있도록 자동으로 컴퓨터 경계 간 디스패치 SignalR에서 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-135">SignalR handles the dispatching across machine boundaries automatically, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="80a63-136">허브 모델 바인딩 수 있는 강력한 형식의 매개 변수 하는 메서드에 전달 되도록 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-136">Hubs allow passing strongly-typed parameters to methods, which enables model binding.</span></span> <span data-ttu-id="80a63-137">두 개의 기본 제공 허브 프로토콜을 제공 하는 SignalR: JSON 및 기반 이진 프로토콜을 기반으로 텍스트 프로토콜 [MessagePack](https://msgpack.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-137">SignalR provides two built-in hub protocols: a text protocol based on JSON and a binary protocol based on [MessagePack](https://msgpack.org/).</span></span>  <span data-ttu-id="80a63-138">MessagePack은 일반적으로 JSON을 사용할 때 보다 작은 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-138">MessagePack generally creates smaller messages than when using JSON.</span></span> <span data-ttu-id="80a63-139">이전 버전의 브라우저를 지원 해야 [XHR 수준 2](https://caniuse.com/#feat=xhr2) MessagePack 프로토콜 지원을 제공 하기 위해 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-139">Older browsers must support [XHR level 2](https://caniuse.com/#feat=xhr2) to provide MessagePack protocol support.</span></span>

<span data-ttu-id="80a63-140">활성 전송을 사용 하 여 메시지를 전송 하 여 클라이언트 쪽 코드를 호출 하는 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-140">Hubs call client-side code by sending messages using the active transport.</span></span> <span data-ttu-id="80a63-141">메시지 이름 및 클라이언트 쪽 메서드의 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-141">The messages contain the name and parameters of the client-side method.</span></span> <span data-ttu-id="80a63-142">메서드 매개 변수로 보낸 개체 구성 된 프로토콜을 사용 하 여 deserialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-142">Objects sent as method parameters are deserialized using the configured protocol.</span></span> <span data-ttu-id="80a63-143">클라이언트는 클라이언트 쪽 코드의 메서드에 대 한 이름과 일치 하도록 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-143">The client tries to match the name to a method in the client-side code.</span></span> <span data-ttu-id="80a63-144">일치 하는 경우 클라이언트 메서드는 deserialize 된 매개 변수 데이터를 사용 하 여 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-144">When a match happens, the client method runs using the deserialized parameter data.</span></span>

<span data-ttu-id="80a63-145">끝점에는 클라이언트에서 읽고 쓸 수 있도록 원시 소켓 같은 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-145">Endpoints provide a raw socket-like API, enabling them to read and write from the client.</span></span> <span data-ttu-id="80a63-146">그룹화, 브로드캐스트, 및 기타 기능을 처리 하도록 개발자에 게 중인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-146">It's up to the developer to handle grouping, broadcasting, and other functions.</span></span> <span data-ttu-id="80a63-147">허브 API 끝점 계층 위에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-147">The Hubs API is built on top of the Endpoints layer.</span></span>

<span data-ttu-id="80a63-148">다음 다이어그램은 허브, 끝점 및 클라이언트 간의 관계를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="80a63-148">The following diagram shows the relationship between hubs, endpoints, and clients.</span></span>

![SignalR 맵](introduction/_static/signalr-core-architecture.png)

## <a name="related-resources"></a><span data-ttu-id="80a63-150">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="80a63-150">Related resources</span></span>

[<span data-ttu-id="80a63-151">ASP.NET Core 용 SignalR 시작</span><span class="sxs-lookup"><span data-stu-id="80a63-151">Get started with SignalR for ASP.NET Core</span></span>](xref:signalr/get-started)
