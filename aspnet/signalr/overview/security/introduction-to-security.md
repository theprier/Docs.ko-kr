---
uid: signalr/overview/security/introduction-to-security
title: SignalR 보안 소개 | Microsoft Docs
author: pfletcher
description: SignalR 응용 프로그램을 개발할 때 고려해 야 할 보안 문제에 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 9a4f09c8036d6d662dfdc44d7c7feaba0101e0c6
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30873903"
---
<a name="introduction-to-signalr-security"></a><span data-ttu-id="3d1a5-103">SignalR 보안 소개</span><span class="sxs-lookup"><span data-stu-id="3d1a5-103">Introduction to SignalR Security</span></span>
====================
<span data-ttu-id="3d1a5-104">여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3d1a5-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3d1a5-105">이 문서는 SignalR 응용 프로그램을 개발할 때 고려해 야 할 보안 문제를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-105">This article describes the security issues you must consider when developing a SignalR application.</span></span> 
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="3d1a5-106">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="3d1a5-106">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="3d1a5-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3d1a5-107">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="3d1a5-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="3d1a5-108">.NET 4.5</span></span>
> - <span data-ttu-id="3d1a5-109">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="3d1a5-109">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="3d1a5-110">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="3d1a5-110">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="3d1a5-111">이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="3d1a5-112">질문이 나 의견이</span><span class="sxs-lookup"><span data-stu-id="3d1a5-112">Questions and comments</span></span>
> 
> <span data-ttu-id="3d1a5-113">이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="3d1a5-114">자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="3d1a5-115">개요</span><span class="sxs-lookup"><span data-stu-id="3d1a5-115">Overview</span></span>

<span data-ttu-id="3d1a5-116">이 문서는 다음 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-116">This document contains the following sections:</span></span>

- [<span data-ttu-id="3d1a5-117">SignalR 보안 개념</span><span class="sxs-lookup"><span data-stu-id="3d1a5-117">SignalR Security Concepts</span></span>](#concepts)

    - [<span data-ttu-id="3d1a5-118">인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="3d1a5-118">Authentication and authorization</span></span>](#authentication)
    - [<span data-ttu-id="3d1a5-119">연결 토큰</span><span class="sxs-lookup"><span data-stu-id="3d1a5-119">Connection token</span></span>](#connectiontoken)
    - [<span data-ttu-id="3d1a5-120">다시 연결 될 때 그룹에 다시 가입</span><span class="sxs-lookup"><span data-stu-id="3d1a5-120">Rejoining groups when reconnecting</span></span>](#rejoingroup)
- [<span data-ttu-id="3d1a5-121">SignalR 교차 사이트 요청 위조를 방지 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3d1a5-121">How SignalR prevents Cross-Site Request Forgery</span></span>](#csrf)
- [<span data-ttu-id="3d1a5-122">SignalR 보안 권장 사항</span><span class="sxs-lookup"><span data-stu-id="3d1a5-122">SignalR Security Recommendations</span></span>](#recommendations)

    - [<span data-ttu-id="3d1a5-123">보안 소켓 레이어 (SSL) 프로토콜</span><span class="sxs-lookup"><span data-stu-id="3d1a5-123">Secure Socket Layers (SSL) protocol</span></span>](#ssl)
    - [<span data-ttu-id="3d1a5-124">그룹에 보안 메커니즘으로 사용 하지 마십시오</span><span class="sxs-lookup"><span data-stu-id="3d1a5-124">Do not use groups as a security mechanism</span></span>](#groupsecurity)
    - [<span data-ttu-id="3d1a5-125">클라이언트의 입력을 안전 하 게 처리</span><span class="sxs-lookup"><span data-stu-id="3d1a5-125">Safely handling input from clients</span></span>](#input)
    - [<span data-ttu-id="3d1a5-126">사용자 상태 활성 연결의 변경 내용 조정</span><span class="sxs-lookup"><span data-stu-id="3d1a5-126">Reconciling a change in user status with an active connection</span></span>](#reconcile)
    - [<span data-ttu-id="3d1a5-127">자동으로 생성 된 JavaScript 프록시 파일</span><span class="sxs-lookup"><span data-stu-id="3d1a5-127">Automatically generated JavaScript proxy files</span></span>](#autogen)
    - [<span data-ttu-id="3d1a5-128">예외</span><span class="sxs-lookup"><span data-stu-id="3d1a5-128">Exceptions</span></span>](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a><span data-ttu-id="3d1a5-129">SignalR 보안 개념</span><span class="sxs-lookup"><span data-stu-id="3d1a5-129">SignalR Security Concepts</span></span>

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a><span data-ttu-id="3d1a5-130">인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="3d1a5-130">Authentication and authorization</span></span>

<span data-ttu-id="3d1a5-131">SignalR은 사용자를 인증 하기 위한 모든 기능을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-131">SignalR does not provide any features for authenticating users.</span></span> <span data-ttu-id="3d1a5-132">대신, 응용 프로그램에 대해 기존 인증 구조에는 SignalR 기능을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-132">Instead, you integrate the SignalR features into the existing authentication structure for an application.</span></span> <span data-ttu-id="3d1a5-133">일반적으로 응용 프로그램 및 프로그램 SignalR에서 인증의 결과 함께 작업에 코딩할 때 사용자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-133">You authenticate users as you would normally in your application, and work with the results of the authentication in your SignalR code.</span></span> <span data-ttu-id="3d1a5-134">예를 들어 ASP.NET 폼 인증으로 사용자를 인증 하 고 허브에 있는 사용자를 적용할 수 있습니다 또는 메서드를 호출할 권한이 있는 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-134">For example, you might authenticate your users with ASP.NET forms authentication, and then in your hub, enforce which users or roles are authorized to call a method.</span></span> <span data-ttu-id="3d1a5-135">허브에서 사용자 이름 또는 사용자를 클라이언트에 게 역할에 속해 있는지 여부와 같은 인증 정보를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-135">In your hub, you can also pass authentication information, such as user name or whether a user belongs to a role, to the client.</span></span>

<span data-ttu-id="3d1a5-136">SignalR 제공는 [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) 허브 또는 메서드에 액세스할 수 있는 사용자 지정 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-136">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users have access to a hub or method.</span></span> <span data-ttu-id="3d1a5-137">허브 또는 허브의 특정 메서드 중 하나를 권한 부여 특성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-137">You apply the Authorize attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="3d1a5-138">권한 부여 속성 없으면 허브에서 모든 공용 메서드는 허브에 연결 하는 클라이언트에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-138">Without the Authorize attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span> <span data-ttu-id="3d1a5-139">허브에 대 한 자세한 내용은 참조 [인증 및 권한 부여 SignalR 허브에 대 한](hub-authorization.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-139">For more information about hubs, see [Authentication and Authorization for SignalR Hubs](hub-authorization.md).</span></span>

<span data-ttu-id="3d1a5-140">적용 된 `Authorize` 허브 있지만 비영구적 연결 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-140">You apply the `Authorize` attribute to hubs, but not persistent connections.</span></span> <span data-ttu-id="3d1a5-141">사용 하는 경우 권한 부여 규칙을 적용 하는 `PersistentConnection` 재정의 해야 합니다는 `AuthorizeRequest` 메서드.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-141">To enforce authorization rules when using a `PersistentConnection` you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="3d1a5-142">영구 연결에 대 한 자세한 내용은 참조 [인증 및 권한 부여 SignalR 영구 연결에 대 한](persistent-connection-authorization.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-142">For more information about persistent connections, see [Authentication and Authorization for SignalR Persistent Connections](persistent-connection-authorization.md).</span></span>

<a id="connectiontoken"></a>

### <a name="connection-token"></a><span data-ttu-id="3d1a5-143">연결 토큰</span><span class="sxs-lookup"><span data-stu-id="3d1a5-143">Connection token</span></span>

<span data-ttu-id="3d1a5-144">SignalR은 발신자의 id 유효성을 검사 하 여 악의적인 명령이 실행의 위험을 완화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-144">SignalR mitigates the risk of executing malicious commands by validating the identity of the sender.</span></span> <span data-ttu-id="3d1a5-145">각 요청에 대 한 서버와 클라이언트 연결 id 및 인증 된 사용자에 대 한 사용자 이름을 포함 하는 연결 토큰을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-145">For each request, the client and server pass a connection token which contains the connection id and username for authenticated users.</span></span> <span data-ttu-id="3d1a5-146">연결 id는 고유 하 게 연결 된 각 클라이언트를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-146">The connection id uniquely identifies each connected client.</span></span> <span data-ttu-id="3d1a5-147">서버는 임의로 새 연결을 만들고 해당 id를 계속 되 면 연결 기간에 대 한 연결 id를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-147">The server randomly generates the connection id when a new connection is created, and persists that id for the duration of the connection.</span></span> <span data-ttu-id="3d1a5-148">웹 응용 프로그램에 대 한 인증 메커니즘에는 사용자 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-148">The authentication mechanism for the web application provides the username.</span></span> <span data-ttu-id="3d1a5-149">SignalR 연결 토큰을 보호 하기 위해 암호화 및 디지털 서명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-149">SignalR uses encryption and a digital signature to protect the connection token.</span></span>

![](introduction-to-security/_static/image2.png)

<span data-ttu-id="3d1a5-150">각 요청에 대 한 서버에서 지정된 된 사용자 요청 된 있는지 확인 하는 토큰의 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-150">For each request, the server validates the contents of the token to ensure that the request is coming from the specified user.</span></span> <span data-ttu-id="3d1a5-151">연결 id 사용자 이름 일치 해야 합니다. 연결 id와 사용자 이름이 모두 유효성을 검사 함으로써 SignalR 악의적인 사용자를 쉽게 다른 사용자를 가장 하지 못하도록 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-151">The username must correspond to the connection id. By validating both the connection id and the username, SignalR prevents a malicious user from easily impersonating another user.</span></span> <span data-ttu-id="3d1a5-152">서버 연결 토큰을 확인할 수 없습니다, 요청이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-152">If the server cannot validate the connection token, the request fails.</span></span>

![](introduction-to-security/_static/image4.png)

<span data-ttu-id="3d1a5-153">연결 id는 확인 프로세스의 일부 이므로 하거나 하면 안 한 사용자의 연결 id 다른 사용자에 게 표시와 같은 쿠키에 클라이언트에서 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-153">Because the connection id is part of the verification process, you should not reveal one user's connection id to other users or store the value on the client, such as in a cookie.</span></span>

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a><span data-ttu-id="3d1a5-154">다시 연결 될 때 그룹에 다시 가입</span><span class="sxs-lookup"><span data-stu-id="3d1a5-154">Rejoining groups when reconnecting</span></span>

<span data-ttu-id="3d1a5-155">기본적으로 SignalR 응용 프로그램은 자동으로 다시 할당 사용자 적절 한 그룹에 대 한 연결을 삭제 하 고 연결 시간이 초과 되기 전에 다시 설정 하는 경우 등의 임시 중단에서 다시 연결 될 때. 다시 연결할 때 클라이언트 연결 id 및 할당 된 그룹을 포함 하는 그룹 토큰을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-155">By default, the SignalR application will automatically re-assign a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. When reconnecting, the client passes a group token that includes the connection id and the assigned groups.</span></span> <span data-ttu-id="3d1a5-156">그룹 토큰 디지털 서명 및 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-156">The group token is digitally signed and encrypted.</span></span> <span data-ttu-id="3d1a5-157">클라이언트에 다시 연결한; 후 동일한 연결 id를 유지 따라서 다시 연결 된 클라이언트에서 전달 된 연결 id는 클라이언트에서 사용 하는 이전 연결 id를 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-157">The client retains the same connection id after a reconnection; therefore, the connection id passed from the reconnected client must match the previous connection id used by the client.</span></span> <span data-ttu-id="3d1a5-158">이 확인 작업에서 다시 연결 될 때 무단된 그룹 가입 요청을 전달 악의적인 사용자가을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-158">This verification prevents a malicious user from passing requests to join unauthorized groups when reconnecting.</span></span>

<span data-ttu-id="3d1a5-159">그러나이 중요 한 그룹 토큰 만료 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-159">However, it is important to note, that the group token does not expire.</span></span> <span data-ttu-id="3d1a5-160">이전에는 그룹에 속한 사용자 해당 그룹에서 차단 된 경우 해당 사용자는 금지 된 그룹을 포함 하는 그룹 토큰을 모방 하기 위해 수. 있습니다</span><span class="sxs-lookup"><span data-stu-id="3d1a5-160">If a user belonged to a group in the past, but was banned from that group, that user may be able to mimic a group token that includes the prohibited group.</span></span> <span data-ttu-id="3d1a5-161">안전 하 게 어떤 그룹에 속해 있는 사용자를 관리 해야 하는 경우와 같은 데이터베이스에 서버에서 해당 데이터를 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-161">If you need to securely manage which users belong to which groups, you need to store that data on the server, such as in a database.</span></span> <span data-ttu-id="3d1a5-162">그런 다음, 사용자 그룹에 속하는지 여부를 서버에서 확인 하는 응용 프로그램에 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-162">Then, add logic to your application that verifies on the server whether a user belongs to a group.</span></span> <span data-ttu-id="3d1a5-163">그룹 구성원 자격을 확인 하는 예제를 보려면 [그룹 작업](../guide-to-the-api/working-with-groups.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-163">For an example of verifying group membership, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<span data-ttu-id="3d1a5-164">연결을 임시 중단 한 후 다시 연결 되 면 적용만 자동으로 그룹에 다시 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-164">Automatically rejoining groups only applies when a connection is reconnected after a temporary disruption.</span></span> <span data-ttu-id="3d1a5-165">하 여 연결이 끊기는 경우 응용 프로그램 또는 응용 프로그램 다시 시작, 응용 프로그램을 벗어나지 올바른 그룹에 해당 사용자를 추가 하는 방법을 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-165">If a user disconnects by navigating away from the application or the application restarts, your application must handle how to add that user to the correct groups.</span></span> <span data-ttu-id="3d1a5-166">자세한 내용은 참조 [그룹 작업](../guide-to-the-api/working-with-groups.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-166">For more information, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a><span data-ttu-id="3d1a5-167">SignalR 교차 사이트 요청 위조를 방지 하는 방법</span><span class="sxs-lookup"><span data-stu-id="3d1a5-167">How SignalR prevents Cross-Site Request Forgery</span></span>

<span data-ttu-id="3d1a5-168">교차 사이트 요청 위조 CSRF ()은 악성 사이트를 사용자가 현재 로그인 취약 한 사이트에 요청을 보냅니다는 방식의 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-168">Cross-Site Request Forgery (CSRF) is an attack where a malicious site sends a request to a vulnerable site where the user is currently logged in.</span></span> <span data-ttu-id="3d1a5-169">SignalR은 SignalR 응용 프로그램에 대 한 올바른 요청을 만들려면 악성 사이트에 대 한 발생할 가능성이 거의 함으로써 CSRF 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-169">SignalR prevents CSRF by making it extremely unlikely for a malicious site to create a valid request for your SignalR application.</span></span>

### <a name="description-of-csrf-attack"></a><span data-ttu-id="3d1a5-170">CSRF 공격 설명</span><span class="sxs-lookup"><span data-stu-id="3d1a5-170">Description of CSRF attack</span></span>

<span data-ttu-id="3d1a5-171">CSRF 공격의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-171">Here is an example of a CSRF attack:</span></span>

1. <span data-ttu-id="3d1a5-172">Www.example.com에 사용자가 사용 하 여 폼 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-172">A user logs into www.example.com, using forms authentication.</span></span>
2. <span data-ttu-id="3d1a5-173">서버에서 사용자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-173">The server authenticates the user.</span></span> <span data-ttu-id="3d1a5-174">서버 로부터 응답 하면 인증 쿠키가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-174">The response from the server includes an authentication cookie.</span></span>
3. <span data-ttu-id="3d1a5-175">사용자 로그 아웃을 하지 않고 악성 웹 사이트를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-175">Without logging out, the user visits a malicious web site.</span></span> <span data-ttu-id="3d1a5-176">이 악성 사이트 다음 HTML 폼을 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-176">This malicious site contains the following HTML form:</span></span> 

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   <span data-ttu-id="3d1a5-177">Form action에는 취약 한 사이트 악성 사이트에 게시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-177">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="3d1a5-178">CSRF의 "사이트 간" 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-178">This is the "cross-site" part of CSRF.</span></span>
4. <span data-ttu-id="3d1a5-179">사용자가 제출 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-179">The user clicks the submit button.</span></span> <span data-ttu-id="3d1a5-180">브라우저에는 요청과 함께 인증 쿠키가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-180">The browser includes the authentication cookie with the request.</span></span>
5. <span data-ttu-id="3d1a5-181">요청은 사용자의 인증 컨텍스트를 사용 하 여 example.com 서버에서 실행 되며 인증된 된 사용자가 수행할 수 있는 모든 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-181">The request runs on the example.com server with the user's authentication context, and can do anything that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="3d1a5-182">하지만이 예제에서는 양식 단추를 클릭 하 여 사용자, 악의적인 페이지 것 처럼 쉽게 SignalR 응용 프로그램에 AJAX 요청을 전송 하는 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-182">Although this example requires the user to click the form button, the malicious page could just as easily run a script that sends an AJAX request to your SignalR application.</span></span> <span data-ttu-id="3d1a5-183">또한 악성 사이트 "https://" 요청을 보낼 수 있으므로 SSL을 사용 하 여 CSRF 공격을 방지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-183">Moreover, using SSL does not prevent a CSRF attack, because the malicious site can send an "https://" request.</span></span>

<span data-ttu-id="3d1a5-184">일반적으로 CSRF 공격은 브라우저가 대상 웹 사이트에 모든 관련 쿠키를 전송 하기 때문에 인증을 위한 쿠키를 사용 하는 웹 사이트에 대해 가능한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-184">Typically, CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="3d1a5-185">그러나 CSRF 공격 쿠키 악용에 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-185">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="3d1a5-186">예를 들어, 기본 및 다이제스트 인증 취약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-186">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="3d1a5-187">기본 또는 다이제스트 인증을 사용 하 여 사용자가 로그 되어 세션이 종료 될 때까지 브라우저가 자동으로 자격 증명을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-187">After a user logs in with Basic or Digest authentication, the browser automatically sends the credentials until the session ends.</span></span>

### <a name="csrf-mitigations-taken-by-signalr"></a><span data-ttu-id="3d1a5-188">SignalR 수행한 CSRF 완화</span><span class="sxs-lookup"><span data-stu-id="3d1a5-188">CSRF mitigations taken by SignalR</span></span>

<span data-ttu-id="3d1a5-189">SignalR 악성 사이트에서 응용 프로그램에 대 한 올바른 요청을 만들지 않으려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-189">SignalR takes the following steps to prevent a malicious site from creating valid requests to your application.</span></span> <span data-ttu-id="3d1a5-190">기본적으로 이러한 단계를 사용 하는 SignalR, 코드의 어떤 조치도 취할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-190">SignalR takes these steps by default, you do not need to take any action in your code.</span></span>

- <span data-ttu-id="3d1a5-191">**도메인 간 요청을 사용 하지 않도록 설정**</span><span class="sxs-lookup"><span data-stu-id="3d1a5-191">**Disable cross domain requests**</span></span>  
 <span data-ttu-id="3d1a5-192">SignalR 외부 도메인의 SignalR 끝점을 호출 하지 못하게 하려면 도메인 간 요청을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-192">SignalR disables cross domain requests to prevent users from calling a SignalR endpoint from an external domain.</span></span> <span data-ttu-id="3d1a5-193">SignalR 외부 도메인의 모든 요청을 유효 하지 않은 것으로 간주 하 고 요청을 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-193">SignalR considers any request from an external domain to be invalid and blocks the request.</span></span> <span data-ttu-id="3d1a5-194">이 기본 동작을 유지 하는 것이 좋습니다. 그렇지 않으면 악성 사이트 수 사용자 하도록 사이트에 명령을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-194">We recommend that you keep this default behavior; otherwise, a malicious site could trick users into sending commands to your site.</span></span> <span data-ttu-id="3d1a5-195">도메인 간 요청 사용 해야 하는 경우 참조 [도메인 간 연결을 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-195">If you need to use cross domain requests, see     [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) .</span></span>
- <span data-ttu-id="3d1a5-196">**쿼리 문자열 하지 쿠키에에서 연결 토큰을 전달 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3d1a5-196">**Pass connection token in query string, not cookie**</span></span>  
 <span data-ttu-id="3d1a5-197">SignalR 쿠키로 대신 쿼리 문자열 값으로 연결 토큰을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-197">SignalR passes the connection token as a query string value, instead of as a cookie.</span></span> <span data-ttu-id="3d1a5-198">악성 코드가 발견 되 면 브라우저 연결 토큰을 실수로 전달할 수 있으므로 연결 토큰 쿠키에 저장은 안전 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-198">Storing the connection token in a cookie is unsafe because the browser can inadvertently forward the connection token when malicious code is encountered.</span></span> <span data-ttu-id="3d1a5-199">또한 쿼리 문자열의 연결 토큰을 전달 합니다. 현재 연결 이상 지속 연결 토큰을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-199">Also, passing the connection token in the query string prevents the connection token from persisting beyond the current connection.</span></span> <span data-ttu-id="3d1a5-200">따라서 악의적인 사용자는 다른 사용자의 인증 자격 증명 요청을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-200">Therefore, a malicious user cannot make a request under another user's authentication credentials.</span></span>
- <span data-ttu-id="3d1a5-201">**연결 토큰을 확인 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3d1a5-201">**Verify connection token**</span></span>  
 <span data-ttu-id="3d1a5-202">에 설명 된 대로 [연결 토큰](#connectiontoken) 섹션에서 서버를 알고 있는 연결 id는 각 인증 된 사용자와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-202">As described in the     [Connection token](#connectiontoken) section, the server knows which connection id is associated with each authenticated user.</span></span> <span data-ttu-id="3d1a5-203">서버는 사용자 이름 일치 하지 않는 연결 id의 모든 요청을 처리 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-203">The server does not process any request from a connection id that does not match the user name.</span></span> <span data-ttu-id="3d1a5-204">그럴 가능성은 악의적인 사용자가 사용자 이름 및 현재 임의로 생성 된 연결 id를 확인 해야 하기 때문에 악의적인 사용자는 유효한 요청 추측할 수 없습니다. 연결이 종료 되는 즉시 해당 연결 id 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-204">It is unlikely a malicious user could guess a valid request because the malicious user would have to know the user name and the current randomly-generated connection id. That connection id becomes invalid as soon as the connection is ended.</span></span> <span data-ttu-id="3d1a5-205">익명 사용자가 중요 정보에 액세스할 수 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-205">Anonymous users should not have access to any sensitive information.</span></span>

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a><span data-ttu-id="3d1a5-206">SignalR 보안 권장 사항</span><span class="sxs-lookup"><span data-stu-id="3d1a5-206">SignalR Security Recommendations</span></span>

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a><span data-ttu-id="3d1a5-207">보안 소켓 레이어 (SSL) 프로토콜</span><span class="sxs-lookup"><span data-stu-id="3d1a5-207">Secure Socket Layers (SSL) protocol</span></span>

<span data-ttu-id="3d1a5-208">SSL 프로토콜 암호화를 사용 하 여 클라이언트와 서버 간의 데이터 전송을 보호.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-208">The SSL protocol uses encryption to secure the transport of data between a client and server.</span></span> <span data-ttu-id="3d1a5-209">클라이언트와 서버 간에 중요 한 정보를 전송 하 여 SignalR 응용 프로그램을 전송 하는 경우 전송에 대 한 SSL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-209">If your SignalR application transmits sensitive information between the client and server, use SSL for the transport.</span></span> <span data-ttu-id="3d1a5-210">SSL 설정에 대 한 자세한 내용은 참조 [IIS 7에서 SSL을 설정 하는 방법을](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-210">For more information about setting up SSL, see [How to set up SSL on IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span></span>

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a><span data-ttu-id="3d1a5-211">그룹에 보안 메커니즘으로 사용 하지 마십시오</span><span class="sxs-lookup"><span data-stu-id="3d1a5-211">Do not use groups as a security mechanism</span></span>

<span data-ttu-id="3d1a5-212">그룹은 관련된 사용자가 수집 하는 편리한 방법을 있지만 중요 한 정보에 대 한 액세스를 제한 하는 보안 메커니즘 되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-212">Groups are a convenient way of collecting related users, but they are not a secure mechanism for limiting access to sensitive information.</span></span> <span data-ttu-id="3d1a5-213">사용자가 자동으로 다시 가입할 수 그룹 다시 연결 하는 동안 때 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-213">This is especially true when users can automatically rejoin groups during a reconnect.</span></span> <span data-ttu-id="3d1a5-214">대신, 권한이 있는 사용자 역할에 추가 하 고 해당 역할의 구성원만 하는 허브 메서드에 대 한 액세스 제한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-214">Instead, consider adding privileged users to a role and limiting access to a hub method to only members of that role.</span></span> <span data-ttu-id="3d1a5-215">역할에 따라 액세스를 제한의 예제를 보려면 [인증 및 권한 부여 SignalR 허브에 대 한](hub-authorization.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-215">For an example of restricting access based on a role, see [Authentication and Authorization for SignalR Hubs](hub-authorization.md).</span></span> <span data-ttu-id="3d1a5-216">그룹에 대 한 사용자 액세스를 확인 하 여 다시 연결 될 때 예제를 보려면 [그룹 작업](../guide-to-the-api/working-with-groups.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-216">For an example of checking user access to groups when reconnecting, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a><span data-ttu-id="3d1a5-217">클라이언트의 입력을 안전 하 게 처리</span><span class="sxs-lookup"><span data-stu-id="3d1a5-217">Safely handling input from clients</span></span>

<span data-ttu-id="3d1a5-218">악의적인 사용자는 다른 사용자에 게 스크립트를 전송 하지 않습니다을 보장 하려면 다른 클라이언트에는 브로드캐스트를 위한 클라이언트의 모든 입력을 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-218">To ensure that a malicious user does not send script to other users, you must encode all input from clients that is intended for broadcast to other clients.</span></span> <span data-ttu-id="3d1a5-219">SignalR 응용 프로그램에 다양 한 유형의 클라이언트 있을 수 있으므로 서버를 보다는 받는 클라이언트에 메시지를 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-219">You should encode messages on the receiving clients rather than the server, because your SignalR application may have many different types of clients.</span></span> <span data-ttu-id="3d1a5-220">따라서 HTML 인코딩 웹 클라이언트에 대 한 작동 하지만 작동 다른 종류의 클라이언트에 대 한 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-220">Therefore, HTML-encoding works for a web client, but not for other types of clients.</span></span> <span data-ttu-id="3d1a5-221">예를 들어 채팅 메시지를 표시 하는 웹 클라이언트 메서드 안전 하 게 처리 하는 것은 사용자 이름 및 메시지를 호출 하 여는 `html()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-221">For example, a web client method to display a chat message would safely handle the user name and message by calling the `html()` function.</span></span>

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a><span data-ttu-id="3d1a5-222">사용자 상태 활성 연결의 변경 내용 조정</span><span class="sxs-lookup"><span data-stu-id="3d1a5-222">Reconciling a change in user status with an active connection</span></span>

<span data-ttu-id="3d1a5-223">사용자의 인증 상태에 대 한 활성 연결이 있는 동안 변경 되 면 사용자는 내용의 오류가 표시 됩니다, 그리고 "사용자 id를 활성 SignalR 연결 중 변경할 수 없습니다."</span><span class="sxs-lookup"><span data-stu-id="3d1a5-223">If a user's authentication status changes while an active connection exists, the user will receive an error that states, "The user identity cannot change during an active SignalR connection."</span></span> <span data-ttu-id="3d1a5-224">이 경우 응용 프로그램 연결 id와 사용자 이름이 조정 되는지 확인 하는 서버에 다시 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-224">In that case, your application should re-connect to the server to make sure the connection id and username are coordinated.</span></span> <span data-ttu-id="3d1a5-225">예를 들어 응용 프로그램에 사용자를 로그 아웃 한 활성 연결이 있는 동안 허용 하는 경우 연결에 대 한 사용자 이름에 다음 요청에 전달 되는 이름과 일치 더 이상 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-225">For example, if your application allows the user to log out while an active connection exists, the username for the connection will no longer match the name that is passed in for the next request.</span></span> <span data-ttu-id="3d1a5-226">사용자가 로그 아웃 전에 연결을 중지 하려면 쿼리하고 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-226">You will want to stop the connection before the user logs out, and then restart it.</span></span>

<span data-ttu-id="3d1a5-227">그러나 되기에 대부분의 응용 프로그램 수동으로 중지 하 고 연결을 시작 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-227">However, it is important to note that most applications will not need to manually stop and start the connection.</span></span> <span data-ttu-id="3d1a5-228">응용 프로그램을 별도 페이지에서 사용자를 리디렉션하는 Web Forms 응용 프로그램 또는 MVC 응용 프로그램의 기본 동작 등으로 로그인 한 후 로그 아웃 한 후 현재 페이지를 새로 고칠 경우 활성 연결이 자동으로 끊기고 하지 않습니다. 별도 작업이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-228">If your application redirects users to a separate page after logging out, such as the default behavior in a Web Forms application or MVC application, or refreshes the current page after logging out, the active connection is automatically disconnected and does not require any additional action.</span></span>

<span data-ttu-id="3d1a5-229">다음 예제에서는 중지 하 고 사용자 상태 변경 될 때 연결을 시작 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-229">The following example shows how to stop and start a connection when the user status has changed.</span></span>

[!code-html[Main](introduction-to-security/samples/sample3.html)]

<span data-ttu-id="3d1a5-230">또는 사이트 슬라이딩 만료를 사용 하 여 폼 인증을 유효한 인증 쿠키를 유지 하려면 활동이 없을 경우 사용자의 인증 상태가 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-230">Or, the user's authentication status may change if your site uses sliding expiration with Forms Authentication, and there is no activity to keep the authentication cookie valid.</span></span> <span data-ttu-id="3d1a5-231">이 경우 사용자를 로그 아웃 됩니다 및 사용자 이름이 더 이상 일치 하지 연결 토큰에서 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-231">In that case, the user will be logged out and the user name will no longer match the user name in the connection token.</span></span> <span data-ttu-id="3d1a5-232">유효한 인증 쿠키를 유지 하려면 웹 서버에서 리소스를 정기적으로 요청 하는 몇 가지 스크립트를 추가 하 여이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-232">You can fix this problem by adding some script that periodically requests a resource on the web server to keep the authentication cookie valid.</span></span> <span data-ttu-id="3d1a5-233">다음 예제에서는 30 분 마다 리소스를 요청 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-233">The following example shows how to request a resource every 30 minutes.</span></span>

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a><span data-ttu-id="3d1a5-234">자동으로 생성 된 JavaScript 프록시 파일</span><span class="sxs-lookup"><span data-stu-id="3d1a5-234">Automatically generated JavaScript proxy files</span></span>

<span data-ttu-id="3d1a5-235">각 사용자에 대 한 JavaScript 프록시 파일의 모든 허브 및 메서드를 포함 하지 않을 경우에 파일의 자동 생성을 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-235">If you do not want to include all of the hubs and methods in the JavaScript proxy file for each user, you can disable the automatic generation of the file.</span></span> <span data-ttu-id="3d1a5-236">허브 및 메서드를 여러 개 있어야 하지만 모든 메서드의 알아두어야 하는 모든 사용자를 원하지 않는 경우이 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-236">You might choose this option if you have multiple hubs and methods, but do not want every user to be aware of all of the methods.</span></span> <span data-ttu-id="3d1a5-237">자동 생성을 사용 하지 않도록 설정 하 여 **EnableJavaScriptProxies** 를 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-237">You disable automatic generation by setting **EnableJavaScriptProxies** to **false**.</span></span>

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

<span data-ttu-id="3d1a5-238">JavaScript 프록시 파일에 대 한 자세한 내용은 참조 [생성 된 프록시 및 수에 대 한 역할](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-238">For more information about the JavaScript proxy files, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span> <a id="exceptions"></a>

### <a name="exceptions"></a><span data-ttu-id="3d1a5-239">예외</span><span class="sxs-lookup"><span data-stu-id="3d1a5-239">Exceptions</span></span>

<span data-ttu-id="3d1a5-240">개체가 중요 한 정보는 클라이언트에 노출 될 수 있습니다 때문에 클라이언트에 예외 개체를 전달 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-240">You should avoid passing exception objects to clients because the objects may expose sensitive information to the clients.</span></span> <span data-ttu-id="3d1a5-241">대신, 관련 된 오류 메시지를 표시 하는 클라이언트의 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d1a5-241">Instead, call a method on the client that displays the relevant error message.</span></span>

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
