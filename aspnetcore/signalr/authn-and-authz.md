---
title: 인증 및 ASP.NET Core SignalR의 권한 부여
author: tdykstra
description: ASP.NET Core SignalR의 인증 및 권한 부여를 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: anurse
ms.custom: mvc
ms.date: 06/29/2018
uid: signalr/authn-and-authz
ms.openlocfilehash: d4259e04a0e3bb9ff517a10465323ccb5e2895a5
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095173"
---
# <a name="authentication-and-authorization-in-aspnet-core-signalr"></a><span data-ttu-id="d0247-103">인증 및 ASP.NET Core SignalR의 권한 부여</span><span class="sxs-lookup"><span data-stu-id="d0247-103">Authentication and authorization in ASP.NET Core SignalR</span></span>

<span data-ttu-id="d0247-104">[Andrew Stanton-nurse](https://twitter.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="d0247-104">By [Andrew Stanton-Nurse](https://twitter.com/anurse)</span></span>

<span data-ttu-id="d0247-105">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/authn-and-authz/sample/) [(다운로드 하는 방법)](xref:tutorials/index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="d0247-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/authn-and-authz/sample/) [(how to download)](xref:tutorials/index#how-to-download-a-sample)</span></span>

## <a name="authenticate-users-connecting-to-a-signalr-hub"></a><span data-ttu-id="d0247-106">SignalR 허브에 연결 된 사용자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-106">Authenticate users connecting to a SignalR hub</span></span>

<span data-ttu-id="d0247-107">SignalR을 사용 하 여 사용할 수 있습니다 [ASP.NET Core 인증](xref:security/authentication/index) 각 연결을 사용 하 여 사용자를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-107">SignalR can be used with [ASP.NET Core Authentication](xref:security/authentication/index) to associate a user with each connection.</span></span> <span data-ttu-id="d0247-108">허브와 인증 데이터에서 액세스할 수 있습니다 합니다 [ `HubConnectionContext.User` ](/dotnet/api/microsoft.aspnetcore.signalr.hubconnectioncontext.user) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-108">In a hub, authentication data can be accessed from the [`HubConnectionContext.User`](/dotnet/api/microsoft.aspnetcore.signalr.hubconnectioncontext.user) property.</span></span> <span data-ttu-id="d0247-109">인증을 사용 하면 사용자와 관련 된 모든 연결에서 메서드를 호출할 허브 (참조 [SignalR의 사용자 및 그룹 관리](xref:signalr/groups) 자세한).</span><span class="sxs-lookup"><span data-stu-id="d0247-109">Authentication allows the hub to call methods on all connections associated with a user (See [Manage users and groups in SignalR](xref:signalr/groups) for more information).</span></span> <span data-ttu-id="d0247-110">여러 연결을 단일 사용자로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-110">Multiple connections may be associated with a single user.</span></span>

### <a name="cookie-authentication"></a><span data-ttu-id="d0247-111">쿠키 인증</span><span class="sxs-lookup"><span data-stu-id="d0247-111">Cookie authentication</span></span>

<span data-ttu-id="d0247-112">브라우저 기반 앱에서 쿠키 인증에는 SignalR 연결에 자동으로 이동 하 여 기존 사용자 자격 증명을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-112">In a browser-based app, cookie authentication allows your existing user credentials to automatically flow to SignalR connections.</span></span> <span data-ttu-id="d0247-113">브라우저 클라이언트를 사용 하는 경우 추가 구성이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-113">When using the browser client, no additional configuration is needed.</span></span> <span data-ttu-id="d0247-114">사용자가 앱에 로그인 하는 경우 SignalR 연결이이 인증은 자동으로 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-114">If the user is logged in to your app, the SignalR connection automatically inherits this authentication.</span></span>

<span data-ttu-id="d0247-115">쿠키 인증 앱만 브라우저 클라이언트에서 사용자를 인증 해야 할 경우가 아니면 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-115">Cookie authentication isn't recommended unless the app only needs to authenticate users from the browser client.</span></span> <span data-ttu-id="d0247-116">사용 하는 경우는 [.NET 클라이언트](xref:signalr/dotnet-client)의 `Cookies` 속성에서 구성할 수 있습니다는 `.WithUrl` 쿠키를 제공 하기 위해 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-116">When using the [.NET Client](xref:signalr/dotnet-client), the `Cookies` property can be configured in the `.WithUrl` call in order to provide a cookie.</span></span> <span data-ttu-id="d0247-117">그러나.NET 클라이언트에서 쿠키 인증을 사용 하 여 응용 프로그램에서 쿠키에 대 한 인증 데이터를 교환 하기 위한 API를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-117">However, using cookie authentication from the .NET Client requires the app to provide an API to exchange authentication data for a cookie.</span></span>

### <a name="bearer-token-authentication"></a><span data-ttu-id="d0247-118">전달자 토큰 인증</span><span class="sxs-lookup"><span data-stu-id="d0247-118">Bearer token authentication</span></span>

<span data-ttu-id="d0247-119">전달자 토큰 인증은 권장 되는 방법은 브라우저 클라이언트 이외의 클라이언트를 사용 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-119">Bearer token authentication is the recommended approach when using clients other than the browser client.</span></span> <span data-ttu-id="d0247-120">이 방법에서는 클라이언트 서버 유효성을 검사 하 고 사용 하 여 사용자를 식별 하는 액세스 토큰을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-120">In this approach, the client provides an access token that the server validates and uses to identify the user.</span></span> <span data-ttu-id="d0247-121">전달자 토큰 인증의 세부 정보는이 문서에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-121">The details of bearer token authentication are beyond the scope of this document.</span></span> <span data-ttu-id="d0247-122">서버에서 전달자 토큰 인증을 사용 하도록 구성 합니다 [JWT 전달자 미들웨어](/dotnet/api/microsoft.extensions.dependencyinjection.jwtbearerextensions.addjwtbearer)합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-122">On the server, bearer token authentication is configured using the [JWT Bearer middleware](/dotnet/api/microsoft.extensions.dependencyinjection.jwtbearerextensions.addjwtbearer).</span></span>

<span data-ttu-id="d0247-123">JavaScript 클라이언트에서 토큰을 제공할 수 있습니다 사용 하 여 [accessTokenFactory](xref:signalr/configuration#configure-bearer-authentication) 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-123">In the JavaScript client, the token can be provided using the [accessTokenFactory](xref:signalr/configuration#configure-bearer-authentication) option.</span></span>

[!code-typescript[Configure Access Token](authn-and-authz/sample/wwwroot/js/chat.ts?range=63-65)]

<span data-ttu-id="d0247-124">.NET 클라이언트는 유사한 [AccessTokenProvider](xref:signalr/configuration#configure-bearer-authentication) 토큰을 구성 하는 데 사용할 수 있는 속성:</span><span class="sxs-lookup"><span data-stu-id="d0247-124">In the .NET client, there is a similar [AccessTokenProvider](xref:signalr/configuration#configure-bearer-authentication) property that can be used to configure the token:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options =>
    { 
        options.AccessTokenProvider = () => _myAccessToken;
    })
    .Build();
```

> [!NOTE]
> <span data-ttu-id="d0247-125">제공한 액세스 토큰 함수 전에 호출 됩니다 **마다** SignalR에서 HTTP 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-125">The access token function you provide is called before **every** HTTP request made by SignalR.</span></span> <span data-ttu-id="d0247-126">(때문에 연결 되어 있는 동안 만료 될 수 있습니다) 연결을 활성 상태로 유지 하기 위해 토큰을 갱신 해야 하는 경우이 함수 내에서 수행 하며 업데이트 된 토큰을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-126">If you need to renew the token in order to keep the connection active (because it may expire during the connection), do so from within this function and return the updated token.</span></span>

<span data-ttu-id="d0247-127">표준 웹 Api에서 HTTP 헤더에서 전달자 토큰이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-127">In standard web APIs, bearer tokens are sent in an HTTP header.</span></span> <span data-ttu-id="d0247-128">그러나 SignalR은 일부 전송을 사용 하는 경우 브라우저에서 이러한 헤더를 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-128">However, SignalR is unable to set these headers in browsers when using some transports.</span></span> <span data-ttu-id="d0247-129">Websocket 및 Server-Sent 이벤트를 사용 하는 경우 토큰은 쿼리 문자열 매개 변수로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-129">When using WebSockets and Server-Sent Events, the token is transmitted as a query string parameter.</span></span> <span data-ttu-id="d0247-130">이 서버에서 지원 하기 위해 추가 구성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-130">In order to support this on the server, additional configuration is required:</span></span>

[!code-csharp[Configure Server to accept access token from Query String](authn-and-authz/sample/Startup.cs?name=snippet)]

### <a name="windows-authentication"></a><span data-ttu-id="d0247-131">Windows 인증</span><span class="sxs-lookup"><span data-stu-id="d0247-131">Windows authentication</span></span>

<span data-ttu-id="d0247-132">하는 경우 [Windows 인증](xref:security/authentication/windowsauth) 구성 된 앱에서 SignalR 해당 id 하 여 허브를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-132">If [Windows authentication](xref:security/authentication/windowsauth) is configured in your app, SignalR can use that identity to secure hubs.</span></span> <span data-ttu-id="d0247-133">그러나 개별 사용자에 게 메시지를 보내려면 해야 사용자 지정 사용자 ID 공급자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-133">However, in order to send messages to individual users, you need to add a custom User ID provider.</span></span> <span data-ttu-id="d0247-134">즉, Windows 인증 시스템 사용자 이름을 확인할 SignalR을 사용 하 여 "Nameidentifier" 클레임을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-134">This is because the Windows authentication system doesn't provide the "Name Identifier" claim that SignalR uses to determine the user name.</span></span>

<span data-ttu-id="d0247-135">구현 하는 새 클래스 추가 `IUserIdProvider` 및 식별자로 사용 하는 사용자 로부터 클레임 중 하나를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-135">Add a new class that implements `IUserIdProvider` and retrieve one of the claims from the user to use as the identifier.</span></span> <span data-ttu-id="d0247-136">예를 들어, "Name" 클레임을 사용 하 (폼에서의 Windows 사용자는 `[Domain]\[Username]`), 다음 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-136">For example, to use the "Name" claim (which is the Windows username in the form `[Domain]\[Username]`), create the following class:</span></span>

```csharp
public class NameUserIdProvider : IUserIdProvider
{
    public string GetUserId(HubConnectionContext connection)
    {
        return connection.User?.FindFirst(ClaimTypes.Name)?.Value;
    }
}
```

<span data-ttu-id="d0247-137">대신 `ClaimTypes.Name`에서 값을 사용할 수는 `User` (Windows SID 식별자와 같은 등).</span><span class="sxs-lookup"><span data-stu-id="d0247-137">Rather than `ClaimTypes.Name`, you can use any value from the `User` (such as the Windows SID identifier, etc.).</span></span>

> [!NOTE]
> <span data-ttu-id="d0247-138">선택한 값은 시스템의 모든 사용자 간에 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-138">The value you choose must be unique among all the users in your system.</span></span> <span data-ttu-id="d0247-139">이 고, 그렇지 한 명의 사용자를 위한 메시지를 다른 사용자에 게 진행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-139">Otherwise, a message intended for one user could end up going to a different user.</span></span>

<span data-ttu-id="d0247-140">이 구성 요소를 등록 하 `Startup.ConfigureServices` 메서드 **후** 호출 `.AddSignalR`</span><span class="sxs-lookup"><span data-stu-id="d0247-140">Register this component in your `Startup.ConfigureServices` method **after** the call to `.AddSignalR`</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // ... other services ...

    services.AddSignalR();
    services.AddSingleton<IUserIdProvider, NameUserIdProvider>();
}
```

## <a name="authorize-users-to-access-hubs-and-hub-methods"></a><span data-ttu-id="d0247-141">액세스 허브 및 허브 메서드에 대 한 사용자 권한 부여</span><span class="sxs-lookup"><span data-stu-id="d0247-141">Authorize users to access hubs and hub methods</span></span>

<span data-ttu-id="d0247-142">기본적으로 인증 되지 않은 사용자가 허브의 모든 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-142">By default, all methods in a hub can be called by an unauthenticated user.</span></span> <span data-ttu-id="d0247-143">인증을 요구 하기 위해 적용 된 [권한 부여](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute) 허브 특성:</span><span class="sxs-lookup"><span data-stu-id="d0247-143">In order to require authentication, apply the [Authorize](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute) attribute to the hub:</span></span>

[!code-csharp[Restrict a hub to only authorized users](authn-and-authz/sample/Hubs/ChatHub.cs?range=8-10,32)]

<span data-ttu-id="d0247-144">생성자 인수 및 속성을 사용할 수는 `[Authorize]` 특정 일치만 사용자에 게 액세스를 제한 하는 특성 [권한 부여 정책](xref:security/authorization/policies)합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-144">You can use the constructor arguments and properties of the `[Authorize]` attribute to restrict access to only users matching specific [authorization policies](xref:security/authorization/policies).</span></span> <span data-ttu-id="d0247-145">예를 들어 라는 사용자 지정 권한 부여 정책이 있는 `MyAuthorizationPolicy` 해당 정책과 일치 하는 사용자만 다음 코드를 사용 하 여 허브에 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-145">For example, if you have a custom authorization policy called `MyAuthorizationPolicy` you can ensure that only users matching that policy can access the hub using the following code:</span></span>

```csharp
[Authorize("MyAuthorizationPolicy")]
public class ChatHub: Hub
{
}
```

<span data-ttu-id="d0247-146">개별 허브 메서드에 사용할 수는 `[Authorize]` 특성으로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-146">Individual hub methods can have the `[Authorize]` attribute applied as well.</span></span> <span data-ttu-id="d0247-147">현재 사용자 메서드에 적용 된 정책에 맞지 경우 호출자에 게 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0247-147">If the current user doesn't match the policy applied to the method, an error is returned to the caller:</span></span>

```csharp
[Authorize]
public class ChatHub: Hub
{
    public async Task Send(string message)
    {
        // ... send a message to all users ...
    }

    [Authorize("Administrators")]
    public void BanUser(string userName)
    {
        // ... ban a user from the chat room (something only Administrators can do) ...
    }
}
```
