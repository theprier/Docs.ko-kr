---
title: ASP.NET Core SignalR 소개
author: tdykstra
description: ASP.NET Core SignalR 라이브러리를 앱에 실시간 기능 추가 간소화 하는 방법에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 04/25/2018
uid: signalr/introduction
ms.openlocfilehash: 2fff24609caf7592bad763a077288990a29617aa
ms.sourcegitcommit: 927e510d68f269d8335b5a7c8592621219a90965
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2018
ms.locfileid: "39342551"
---
# <a name="introduction-to-aspnet-core-signalr"></a><span data-ttu-id="5f644-103">ASP.NET Core SignalR 소개</span><span class="sxs-lookup"><span data-stu-id="5f644-103">Introduction to ASP.NET Core SignalR</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="5f644-104">SignalR 이란?</span><span class="sxs-lookup"><span data-stu-id="5f644-104">What is SignalR?</span></span>

<span data-ttu-id="5f644-105">ASP.NET Core SignalR은 실시간 웹 기능을 앱에 추가 간소화 하는 오픈 소스 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-105">ASP.NET Core SignalR is an open-source library that simplifies adding real-time web functionality to apps.</span></span> <span data-ttu-id="5f644-106">실시간 웹 기능 클라이언트로 푸시 콘텐츠를 서버 쪽 코드를 즉시 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-106">Real-time web functionality enables server-side code to push content to clients instantly.</span></span>

<span data-ttu-id="5f644-107">SignalR에 대 한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-107">Good candidates for SignalR:</span></span>

* <span data-ttu-id="5f644-108">서버에서 자주 업데이트가 필요한 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-108">Apps that require high frequency updates from the server.</span></span> <span data-ttu-id="5f644-109">게임, 소셜 네트워크, 투표, 경매, 지도 및 GPS 앱을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-109">Examples are gaming, social networks, voting, auction, maps, and GPS apps.</span></span>
* <span data-ttu-id="5f644-110">대시보드 및 모니터링 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-110">Dashboards and monitoring apps.</span></span> <span data-ttu-id="5f644-111">예를 들어 회사 대시보드, 즉석 판매 업데이트 또는 여행 경고가.</span><span class="sxs-lookup"><span data-stu-id="5f644-111">Examples include company dashboards, instant sales updates, or travel alerts.</span></span>
* <span data-ttu-id="5f644-112">공동 작업 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-112">Collaborative apps.</span></span> <span data-ttu-id="5f644-113">화이트 보드 앱 및 팀 회의 소프트웨어가 공동 작업 앱의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-113">Whiteboard apps and team meeting software are examples of collaborative apps.</span></span>
* <span data-ttu-id="5f644-114">알림이 필요한 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-114">Apps that require notifications.</span></span> <span data-ttu-id="5f644-115">소셜 네트워크, 이메일, 채팅, 게임, 여행 경고 및 다른 많은 앱 알림을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-115">Social networks, email, chat, games, travel alerts, and many other apps use notifications.</span></span>

<span data-ttu-id="5f644-116">서버에서 클라이언트를 만들기 위한 API를 제공 하는 SignalR [원격 프로시저 호출 (RPC)](https://wikipedia.org/wiki/Remote_procedure_call)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-116">SignalR provides an API for creating server-to-client [remote procedure calls (RPC)](https://wikipedia.org/wiki/Remote_procedure_call).</span></span> <span data-ttu-id="5f644-117">Rpc 서버 쪽.NET Core 코드에서 클라이언트에서 JavaScript 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-117">The RPCs call JavaScript functions on clients from server-side .NET Core code.</span></span>

<span data-ttu-id="5f644-118">ASP.NET core SignalR의 기능 중 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-118">Here are some features of SignalR for ASP.NET Core:</span></span>

* <span data-ttu-id="5f644-119">연결 관리를 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-119">Handles connection management automatically.</span></span>
* <span data-ttu-id="5f644-120">동시에 연결 된 모든 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-120">Sends messages to all connected clients simultaneously.</span></span> <span data-ttu-id="5f644-121">예를 들어 대화방입니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-121">For example, a chat room.</span></span>
* <span data-ttu-id="5f644-122">특정 클라이언트 또는 클라이언트 그룹에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-122">Sends messages to specific clients or groups of clients.</span></span>
* <span data-ttu-id="5f644-123">증가 트래픽을 처리 하도록 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-123">Scales to handle increasing traffic.</span></span>

<span data-ttu-id="5f644-124">원본에서 호스트 되는 [GitHub의 SignalR 리포지토리](https://github.com/aspnet/signalr)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-124">The source is hosted in a [SignalR repository on GitHub](https://github.com/aspnet/signalr).</span></span>

## <a name="transports"></a><span data-ttu-id="5f644-125">전송</span><span class="sxs-lookup"><span data-stu-id="5f644-125">Transports</span></span>

<span data-ttu-id="5f644-126">SignalR 실시간 통신을 처리 하기 위한 몇 가지 기법을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-126">SignalR supports several techniques for handling real-time communications:</span></span>

* [<span data-ttu-id="5f644-127">WebSockets</span><span class="sxs-lookup"><span data-stu-id="5f644-127">WebSockets</span></span>](https://tools.ietf.org/html/rfc7118)
* <span data-ttu-id="5f644-128">서버에서 전송 이벤트</span><span class="sxs-lookup"><span data-stu-id="5f644-128">Server-Sent Events</span></span>
* <span data-ttu-id="5f644-129">긴 폴링</span><span class="sxs-lookup"><span data-stu-id="5f644-129">Long Polling</span></span>

<span data-ttu-id="5f644-130">SignalR에는 자동으로 서버와 클라이언트의 기능 내에 있는 최상의 전송 방법을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-130">SignalR automatically chooses the best transport method that is within the capabilities of the server and client.</span></span>

## <a name="hubs"></a><span data-ttu-id="5f644-131">허브</span><span class="sxs-lookup"><span data-stu-id="5f644-131">Hubs</span></span>

<span data-ttu-id="5f644-132">사용 하 여 SignalR *hubs* 클라이언트와 서버 간 통신.</span><span class="sxs-lookup"><span data-stu-id="5f644-132">SignalR uses *hubs* to communicate between clients and servers.</span></span>

<span data-ttu-id="5f644-133">허브는 클라이언트와 서버에서 서로 다른 메서드를 호출할 수 있는 높은 수준의 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="5f644-133">A hub is a high-level pipeline that allows a client and server to call methods on each other.</span></span> <span data-ttu-id="5f644-134">클라이언트가 서버의 그 반대로 메서드를 호출할 수 있도록 자동으로 컴퓨터 경계를 넘어 디스패치 SignalR에서 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-134">SignalR handles the dispatching across machine boundaries automatically, allowing clients to call methods on the server and vice versa.</span></span> <span data-ttu-id="5f644-135">모델 바인딩을 활성화 하는 방법에 강력한 형식의 매개 변수를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-135">You can pass strongly-typed parameters to methods, which enables model binding.</span></span> <span data-ttu-id="5f644-136">SignalR 제공 두 가지 기본 제공 허브 프로토콜: JSON 및 기반 이진 프로토콜을 기반으로 하는 텍스트 프로토콜 [MessagePack](https://msgpack.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-136">SignalR provides two built-in hub protocols: a text protocol based on JSON and a binary protocol based on [MessagePack](https://msgpack.org/).</span></span>  <span data-ttu-id="5f644-137">일반적으로 MessagePack JSON에 비해 크기가 작은 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-137">MessagePack generally creates smaller messages compared to JSON.</span></span> <span data-ttu-id="5f644-138">이전 버전의 브라우저를 지원 해야 합니다 [XHR 수준 2](https://caniuse.com/#feat=xhr2) MessagePack 프로토콜 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-138">Older browsers must support [XHR level 2](https://caniuse.com/#feat=xhr2) to provide MessagePack protocol support.</span></span>

<span data-ttu-id="5f644-139">허브 이름 및 클라이언트 쪽 메서드의 매개 변수를 포함 하는 메시지를 전송 하 여 클라이언트 쪽 코드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-139">Hubs call client-side code by sending messages that contain the name and parameters of the client-side method.</span></span> <span data-ttu-id="5f644-140">메서드 매개 변수로 보낸 개체는 구성된 된 프로토콜을 사용 하 여 역직렬화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-140">Objects sent as method parameters are deserialized using the configured protocol.</span></span> <span data-ttu-id="5f644-141">클라이언트는 클라이언트 쪽 코드에서 메서드 이름을 찾으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-141">The client tries to match the name to a method in the client-side code.</span></span> <span data-ttu-id="5f644-142">클라이언트에 일치 항목을 찾으면 메서드를 호출 하 고 deserialize 된 매개 변수 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f644-142">When the client finds a match, it calls the method and passes to it the deserialized parameter data.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5f644-143">추가 자료</span><span class="sxs-lookup"><span data-stu-id="5f644-143">Additional resources</span></span>

* [<span data-ttu-id="5f644-144">ASP.NET core SignalR을 사용 하 여 시작</span><span class="sxs-lookup"><span data-stu-id="5f644-144">Get started with SignalR for ASP.NET Core</span></span>](xref:tutorials/signalr)
* [<span data-ttu-id="5f644-145">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="5f644-145">Supported Platforms</span></span>](xref:signalr/supported-platforms)
* [<span data-ttu-id="5f644-146">허브</span><span class="sxs-lookup"><span data-stu-id="5f644-146">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="5f644-147">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="5f644-147">JavaScript client</span></span>](xref:signalr/javascript-client)
