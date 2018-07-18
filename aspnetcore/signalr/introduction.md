---
title: ASP.NET Core SignalR 소개
author: tdykstra
description: ASP.NET Core SignalR 라이브러리를 앱에 실시간 기능 추가 간소화 하는 방법에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 04/25/2018
uid: signalr/introduction
ms.openlocfilehash: bc6f25c3f35e7fb0c2c68220697f2e0fdc6a9958
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095391"
---
# <a name="introduction-to-aspnet-core-signalr"></a><span data-ttu-id="641ad-103">ASP.NET Core SignalR 소개</span><span class="sxs-lookup"><span data-stu-id="641ad-103">Introduction to ASP.NET Core SignalR</span></span>

<span data-ttu-id="641ad-104">작성자: [Rachel Appel](https://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="641ad-104">By [Rachel Appel](https://twitter.com/rachelappel)</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="641ad-105">SignalR 이란?</span><span class="sxs-lookup"><span data-stu-id="641ad-105">What is SignalR?</span></span>

<span data-ttu-id="641ad-106">ASP.NET Core SignalR은 실시간 웹 기능을 앱에 추가 간소화 하는 라이브러리.</span><span class="sxs-lookup"><span data-stu-id="641ad-106">ASP.NET Core SignalR is a library that simplifies adding real-time web functionality to apps.</span></span> <span data-ttu-id="641ad-107">실시간 웹 기능 클라이언트로 푸시 콘텐츠를 서버 쪽 코드를 즉시 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-107">Real-time web functionality enables server-side code to push content to clients instantly.</span></span>

<span data-ttu-id="641ad-108">SignalR에 대 한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-108">Good candidates for SignalR:</span></span>

* <span data-ttu-id="641ad-109">서버에서 자주 업데이트가 필요한 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-109">Apps that require high frequency updates from the server.</span></span> <span data-ttu-id="641ad-110">게임, 소셜 네트워크, 투표, 경매, 지도 및 GPS 앱을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-110">Examples are gaming, social networks, voting, auction, maps, and GPS apps.</span></span>
* <span data-ttu-id="641ad-111">대시보드 및 모니터링 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-111">Dashboards and monitoring apps.</span></span> <span data-ttu-id="641ad-112">예를 들어 회사 대시보드, 즉석 판매 업데이트 또는 여행 경고가.</span><span class="sxs-lookup"><span data-stu-id="641ad-112">Examples include company dashboards, instant sales updates, or travel alerts.</span></span>
* <span data-ttu-id="641ad-113">공동 작업 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-113">Collaborative apps.</span></span> <span data-ttu-id="641ad-114">화이트 보드 앱 및 팀 회의 소프트웨어가 공동 작업 앱의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-114">Whiteboard apps and team meeting software are examples of collaborative apps.</span></span>
* <span data-ttu-id="641ad-115">알림이 필요한 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-115">Apps that require notifications.</span></span> <span data-ttu-id="641ad-116">소셜 네트워크, 이메일, 채팅, 게임, 여행 경고 및 다른 많은 앱 알림을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-116">Social networks, email, chat, games, travel alerts, and many other apps use notifications.</span></span>

<span data-ttu-id="641ad-117">서버에서 클라이언트를 만들기 위한 API를 제공 하는 SignalR [원격 프로시저 호출 (RPC)](https://wikipedia.org/wiki/Remote_procedure_call)합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-117">SignalR provides an API for creating server-to-client [remote procedure calls (RPC)](https://wikipedia.org/wiki/Remote_procedure_call).</span></span> <span data-ttu-id="641ad-118">Rpc 서버 쪽.NET Core 코드에서 클라이언트에서 JavaScript 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-118">The RPCs call JavaScript functions on clients from server-side .NET Core code.</span></span>

<span data-ttu-id="641ad-119">ASP.NET core SignalR:</span><span class="sxs-lookup"><span data-stu-id="641ad-119">SignalR for ASP.NET Core:</span></span>

* <span data-ttu-id="641ad-120">연결 관리를 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-120">Handles connection management automatically.</span></span>
* <span data-ttu-id="641ad-121">메시지가 연결 된 모든 클라이언트에 동시에 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-121">Enables broadcasting messages to all connected clients simultaneously.</span></span> <span data-ttu-id="641ad-122">예를 들어 대화방입니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-122">For example, a chat room.</span></span>
* <span data-ttu-id="641ad-123">특정 클라이언트 또는 클라이언트 그룹에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-123">Enables sending messages to specific clients or groups of clients.</span></span>
* <span data-ttu-id="641ad-124">오픈 소싱할 [GitHub](https://github.com/aspnet/signalr)합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-124">Is open-sourced at [GitHub](https://github.com/aspnet/signalr).</span></span>
* <span data-ttu-id="641ad-125">확장 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-125">Scalable.</span></span>

<span data-ttu-id="641ad-126">클라이언트와 서버 간의 연결이 영구적 이므로, HTTP 연결과 달리 합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-126">The connection between the client and server is persistent, unlike an HTTP connection.</span></span>

## <a name="transports"></a><span data-ttu-id="641ad-127">전송</span><span class="sxs-lookup"><span data-stu-id="641ad-127">Transports</span></span>

<span data-ttu-id="641ad-128">실시간 웹 응용 프로그램을 구축 하는 방법의 여러 SignalR 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-128">SignalR abstracts over a number of techniques for building real-time web applications.</span></span> <span data-ttu-id="641ad-129">[Websocket](https://tools.ietf.org/html/rfc7118) 최적의 전송 이지만 Server-Sent 이벤트 및 Long Polling과 같은 다른 기술을 사용할 수 없는 해당 하는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-129">[WebSockets](https://tools.ietf.org/html/rfc7118) is the optimal transport, but other techniques like Server-Sent Events and Long Polling can be used when those aren't available.</span></span> <span data-ttu-id="641ad-130">SignalR은 자동으로 감지 하 고 서버 및 클라이언트에서 지원 되는 기능을 기반으로 하는 적절 한 전송을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-130">SignalR will automatically detect and initialize the appropriate transport based on features supported on the server and client.</span></span>

## <a name="hubs"></a><span data-ttu-id="641ad-131">허브</span><span class="sxs-lookup"><span data-stu-id="641ad-131">Hubs</span></span>

<span data-ttu-id="641ad-132">SignalR 허브를 사용 하 여 클라이언트와 서버 간 통신.</span><span class="sxs-lookup"><span data-stu-id="641ad-132">SignalR uses hubs to communicate between clients and servers.</span></span>

<span data-ttu-id="641ad-133">허브는 클라이언트와 서버에서 서로 다른 메서드를 호출할 수 있도록 하는 높은 수준의 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="641ad-133">A hub is a high-level pipeline that allows your client and server to call methods on each other.</span></span> <span data-ttu-id="641ad-134">클라이언트가 서버에서 로컬 메서드로 쉽게 이동 하 고 그 반대의 경우로 메서드를 호출할 수 있도록 자동으로 컴퓨터 경계를 넘어 디스패치 SignalR에서 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-134">SignalR handles the dispatching across machine boundaries automatically, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="641ad-135">허브 모델 바인딩을 활성화 하는 방법에 강력한 형식의 매개 변수를 전달할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-135">Hubs allow passing strongly-typed parameters to methods, which enables model binding.</span></span> <span data-ttu-id="641ad-136">SignalR 제공 두 가지 기본 제공 허브 프로토콜: JSON 및 기반 이진 프로토콜을 기반으로 하는 텍스트 프로토콜 [MessagePack](https://msgpack.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-136">SignalR provides two built-in hub protocols: a text protocol based on JSON and a binary protocol based on [MessagePack](https://msgpack.org/).</span></span>  <span data-ttu-id="641ad-137">MessagePack은 일반적으로 JSON을 사용할 때 보다 작은 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-137">MessagePack generally creates smaller messages than when using JSON.</span></span> <span data-ttu-id="641ad-138">이전 버전의 브라우저를 지원 해야 합니다 [XHR 수준 2](https://caniuse.com/#feat=xhr2) MessagePack 프로토콜 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-138">Older browsers must support [XHR level 2](https://caniuse.com/#feat=xhr2) to provide MessagePack protocol support.</span></span>

<span data-ttu-id="641ad-139">허브 활성 전송을 사용 하 여 메시지를 전송 하 여 클라이언트 쪽 코드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-139">Hubs call client-side code by sending messages using the active transport.</span></span> <span data-ttu-id="641ad-140">메시지 이름 및 클라이언트 쪽 메서드의 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-140">The messages contain the name and parameters of the client-side method.</span></span> <span data-ttu-id="641ad-141">메서드 매개 변수로 보낸 개체는 구성된 된 프로토콜을 사용 하 여 역직렬화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-141">Objects sent as method parameters are deserialized using the configured protocol.</span></span> <span data-ttu-id="641ad-142">클라이언트는 클라이언트 쪽 코드에서 메서드 이름을 찾으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-142">The client tries to match the name to a method in the client-side code.</span></span> <span data-ttu-id="641ad-143">일치 하는 경우 클라이언트 메서드는 deserialize 된 매개 변수 데이터를 사용 하 여 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="641ad-143">When a match happens, the client method runs using the deserialized parameter data.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="641ad-144">추가 자료</span><span class="sxs-lookup"><span data-stu-id="641ad-144">Additional resources</span></span>

* [<span data-ttu-id="641ad-145">ASP.NET core SignalR을 사용 하 여 시작</span><span class="sxs-lookup"><span data-stu-id="641ad-145">Get started with SignalR for ASP.NET Core</span></span>](xref:tutorials/signalr)
* [<span data-ttu-id="641ad-146">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="641ad-146">Supported Platforms</span></span>](xref:signalr/supported-platforms)
* [<span data-ttu-id="641ad-147">허브</span><span class="sxs-lookup"><span data-stu-id="641ad-147">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="641ad-148">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="641ad-148">JavaScript client</span></span>](xref:signalr/javascript-client)
