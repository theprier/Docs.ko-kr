---
uid: signalr/overview/security/hub-authorization
title: 인증 및 권한 부여 SignalR 허브에 대 한 | Microsoft Docs
author: pfletcher
description: 이 항목에 있는 사용자 또는 역할에는 허브 메서드에 액세스할 수를 제한 하는 방법을 설명 합니다. 이 항목에서 Visual Studio 2013.NET 4.5 SignalR 했습니다 사용 하는 소프트웨어 버전 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/05/2015
ms.topic: article
ms.assetid: a610c796-c131-473c-baef-2e6c568cb2a2
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/security/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8e3bc8889efb1be80c57084fb04dc8030b386601
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872756"
---
<a name="authentication-and-authorization-for-signalr-hubs"></a><span data-ttu-id="31587-104">인증 및 권한 부여 SignalR 허브에 대 한</span><span class="sxs-lookup"><span data-stu-id="31587-104">Authentication and Authorization for SignalR Hubs</span></span>
====================
<span data-ttu-id="31587-105">여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="31587-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="31587-106">이 항목에 있는 사용자 또는 역할에는 허브 메서드에 액세스할 수를 제한 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-106">This topic describes how to restrict which users or roles can access hub methods.</span></span> 
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="31587-107">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="31587-107">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="31587-108">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="31587-108">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="31587-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="31587-109">.NET 4.5</span></span>
> - <span data-ttu-id="31587-110">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="31587-110">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="31587-111">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="31587-111">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="31587-112">이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-112">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="31587-113">질문이 나 의견이</span><span class="sxs-lookup"><span data-stu-id="31587-113">Questions and comments</span></span>
> 
> <span data-ttu-id="31587-114">이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="31587-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="31587-115">자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="31587-116">개요</span><span class="sxs-lookup"><span data-stu-id="31587-116">Overview</span></span>

<span data-ttu-id="31587-117">이 항목에는 다음과 같은 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="31587-118">특성을 권한 부여</span><span class="sxs-lookup"><span data-stu-id="31587-118">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="31587-119">모든 허브에 대 한 인증을 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-119">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="31587-120">사용자 지정된 권한 부여</span><span class="sxs-lookup"><span data-stu-id="31587-120">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="31587-121">클라이언트에 인증 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-121">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="31587-122">.NET 클라이언트에 대 한 인증 옵션</span><span class="sxs-lookup"><span data-stu-id="31587-122">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="31587-123">폼 인증 쿠키</span><span class="sxs-lookup"><span data-stu-id="31587-123">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="31587-124">Windows 인증</span><span class="sxs-lookup"><span data-stu-id="31587-124">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="31587-125">연결 헤더</span><span class="sxs-lookup"><span data-stu-id="31587-125">Connection header</span></span>](#header)
    - [<span data-ttu-id="31587-126">Certificate</span><span class="sxs-lookup"><span data-stu-id="31587-126">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="31587-127">특성을 권한 부여</span><span class="sxs-lookup"><span data-stu-id="31587-127">Authorize attribute</span></span>

<span data-ttu-id="31587-128">SignalR 제공는 [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) 특성을 허브 또는 메서드에 있는 권한이 있는 사용자 또는 역할을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-128">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="31587-129">이 특성에는 `Microsoft.AspNet.SignalR` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="31587-129">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="31587-130">적용는 `Authorize` 특성을 허브 또는 허브의 특정 메서드 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="31587-130">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="31587-131">적용 하는 경우는 `Authorize` 허브에서 메서드의 모든 특성을 허브 클래스를 지정 된 인증 요구 사항에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31587-131">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="31587-132">이 항목에서는 다양 한 유형의 권한 부여 요구 사항 적용할 수 있는 몇 가지 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-132">This topic provides examples of the different types of authorization requirements that you can apply.</span></span> <span data-ttu-id="31587-133">없이 `Authorize` 특성, 연결 된 클라이언트 허브의 모든 public 메서드를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-133">Without the `Authorize` attribute, a connected client can access any public method on the hub.</span></span>

<span data-ttu-id="31587-134">웹 응용 프로그램에서 이름이 "Admin" 역할을 정의 하면 해당 역할의 사용자만를 다음 코드로 허브에 액세스할 수 있도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-134">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="31587-135">또는 허브를 아래와 같이 인증 된 사용자 에게만 제공 되는 두 번째 방법 및 모든 사용자에 게 사용할 수 있는 메서드가 포함 되어 있는지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-135">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="31587-136">다음 예에서는 다양 한 권한 부여 시나리오를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-136">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="31587-137">`[Authorize]` -인증 된 사용자만</span><span class="sxs-lookup"><span data-stu-id="31587-137">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="31587-138">`[Authorize(Roles = "Admin,Manager")]` -인증 된 사용자 지정된 된 역할에만</span><span class="sxs-lookup"><span data-stu-id="31587-138">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="31587-139">`[Authorize(Users = "user1,user2")]` – 지정된 된 사용자 이름 가진 사용자를 인증 된만</span><span class="sxs-lookup"><span data-stu-id="31587-139">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="31587-140">`[Authorize(RequireOutgoing=false)]` -인증 된 사용자가 허브를 호출할 수 있지만 서버에서 클라이언트로 다시 호출 제한할 수 없는 권한 부여와 같은 특정 사용자만 메시지를 보낼 수 있지만 다른 모든 메시지를 받을 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-140">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="31587-141">RequireOutgoing 속성 허브 내에서 개인 메서드에 없는 전체 hub에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-141">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="31587-142">RequireOutgoing을 false로 설정 하지 않으면 권한 부여 요구 사항을 충족 하는 사용자만 서버에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31587-142">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="31587-143">모든 허브에 대 한 인증을 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-143">Require authentication for all hubs</span></span>

<span data-ttu-id="31587-144">호출 하 여 응용 프로그램에서 인증 모든 허브 및 허브 메서드에 대 한 필요할 수 있습니다는 [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) 메서드 응용 프로그램이 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-144">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="31587-145">여러 허브 있고 모두에 대 한 인증 요구를 적용 하려는 경우이 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-145">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="31587-146">이 메서드로 역할, 사용자 또는 나가는 권한 부여에 대 한 요구 사항을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-146">With this method, you cannot specify requirements for role, user, or outgoing authorization.</span></span> <span data-ttu-id="31587-147">허브 메서드에 대 한 액세스는 인증 된 사용자로 제한만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-147">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="31587-148">그러나 권한 부여 속성 허브 또는 추가 요구 사항을 지정 하는 메서드를 여전히 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-148">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="31587-149">특성에 지정 하는 모든 요구 사항 인증의 기본 요구 사항에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31587-149">Any requirement you specify in an attribute is added to the basic requirement of authentication.</span></span>

<span data-ttu-id="31587-150">다음 예제에서는 인증 된 사용자에 게 모든 허브 메서드를 제한 하는 시작 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="31587-150">The following example shows a Startup file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="31587-151">호출 하는 경우는 `RequireAuthentication()` SignalR 요청 처리 된 후에 메서드, SignalR는 throw 한 `InvalidOperationException` 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="31587-151">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="31587-152">SignalR은 파이프라인 호출 된 후 HubPipeline에 모듈을 추가할 수 없으므로이 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-152">SignalR throws this exception because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="31587-153">이전 예제에서는 호출은 `RequireAuthentication` 에서 메서드는 `Configuration` 메서드 첫 번째 요청을 처리 하기 전에 한 번 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-153">The previous example shows calling the `RequireAuthentication` method in the `Configuration` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="31587-154">사용자 지정된 권한 부여</span><span class="sxs-lookup"><span data-stu-id="31587-154">Customized authorization</span></span>

<span data-ttu-id="31587-155">권한 부여를 결정 하는 방법을 사용자 지정 해야 할 경우에서 파생 되는 클래스를 만들 수 있습니다 `AuthorizeAttribute` 재정의 [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="31587-155">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="31587-156">SignalR 각 요청에 대 한 사용자에 게 요청을 완료할 수 있는 권한이 있는지 여부를 확인 하려면이 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-156">For each request, SignalR invokes this method to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="31587-157">재정의 된 메서드에서 권한 부여 시나리오에 필요한 논리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-157">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="31587-158">다음 예제에서는 클레임 기반 id 통해 권한 부여를 적용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="31587-158">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="31587-159">클라이언트에 인증 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-159">Pass authentication information to clients</span></span>

<span data-ttu-id="31587-160">클라이언트에서 실행 되는 코드의 인증 정보를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-160">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="31587-161">클라이언트에서 메서드를 호출할 때 필요한 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-161">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="31587-162">예를 들어 채팅 응용 프로그램 메서드에 전달할 수 매개 변수로 메시지를 게시 하는 사람의 사용자 이름 아래와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-162">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="31587-163">또는 다음과 같이 해당 개체를 매개 변수로 전달 및 인증 정보를 나타내는 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-163">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="31587-164">직접 전달 하면 안 한 클라이언트 연결 id 다른 클라이언트를 악의적인 사용자가 해당 클라이언트의 요청을 모방 하기 위해 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-164">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="31587-165">.NET 클라이언트에 대 한 인증 옵션</span><span class="sxs-lookup"><span data-stu-id="31587-165">Authentication options for .NET clients</span></span>

<span data-ttu-id="31587-166">.NET 클라이언트 등이 인증 된 사용자 제한 되는 허브와 상호 작용을 하 여 콘솔 응용 프로그램이 있는 경우에 쿠키, 연결 헤더 또는 인증서 인증 자격 증명을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-166">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="31587-167">이 섹션의 예제에는 사용자를 인증 하기 위한 다양 한 방법을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="31587-167">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="31587-168">SignalR 응용 프로그램을 완벽 하 게 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-168">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="31587-169">SignalR과.NET 클라이언트에 대 한 자세한 내용은 참조 [허브 API 가이드-.NET 클라이언트](../guide-to-the-api/hubs-api-guide-net-client.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-169">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="31587-170">쿠키</span><span class="sxs-lookup"><span data-stu-id="31587-170">Cookie</span></span>

<span data-ttu-id="31587-171">.NET 클라이언트는 ASP.NET 폼 인증을 사용 하는 허브와 상호 작용을 하는 경우 연결에서 인증 쿠키를 수동으로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-171">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="31587-172">쿠키를 추가 `CookieContainer` 속성에는 [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="31587-172">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="31587-173">다음 예제에서는 웹 페이지에서 인증 쿠키를 검색 하 고 연결에 해당 쿠키를 추가 하는 콘솔 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="31587-173">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="31587-174">콘솔 응용 프로그램 게시 자격 증명을 <strong>www.contoso.com/RemoteLogin</strong> 다음 코드 숨김 파일을 포함 하는 빈 페이지를 참조할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-174">The console app posts the credentials to <strong>www.contoso.com/RemoteLogin</strong> which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="31587-175">Windows 인증</span><span class="sxs-lookup"><span data-stu-id="31587-175">Windows authentication</span></span>

<span data-ttu-id="31587-176">Windows 인증을 사용할 경우 현재 사용자의 자격 증명을 사용 하 여 전달할 수 있습니다는 [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="31587-176">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="31587-177">DefaultCredentials의 값에는 연결에 대 한 자격 증명을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-177">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="31587-178">연결 헤더</span><span class="sxs-lookup"><span data-stu-id="31587-178">Connection header</span></span>

<span data-ttu-id="31587-179">응용 프로그램에서 쿠키를 사용 하지 않는 경우 연결 헤더의 사용자 정보를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-179">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="31587-180">예를 들어 연결 헤더에서 토큰을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-180">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="31587-181">그런 다음 허브에서 사용자의 토큰을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-181">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="31587-182">인증서</span><span class="sxs-lookup"><span data-stu-id="31587-182">Certificate</span></span>

<span data-ttu-id="31587-183">사용자를 확인 하는 클라이언트 인증서를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-183">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="31587-184">연결을 만들 때 인증서를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-184">You add the certificate when creating the connection.</span></span> <span data-ttu-id="31587-185">다음 예제에서는 연결;로 클라이언트 인증서를 추가 하는 방법에 대해서만 보여 줍니다. 전체 콘솔 응용 프로그램은 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31587-185">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="31587-186">사용 하 여는 [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) 클래스 인증서를 만드는 여러 가지 방법으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="31587-186">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
