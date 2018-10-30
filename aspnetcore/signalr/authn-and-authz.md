---
title: 인증 및 ASP.NET Core SignalR의 권한 부여
author: tdykstra
description: ASP.NET Core SignalR의 인증 및 권한 부여를 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: anurse
ms.custom: mvc
ms.date: 06/29/2018
uid: signalr/authn-and-authz
ms.openlocfilehash: 7cfe90115b0710fba196693efd309f7c914f0ad4
ms.sourcegitcommit: 2ef32676c16f76282f7c23154d13affce8c8bf35
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50234542"
---
# <a name="authentication-and-authorization-in-aspnet-core-signalr"></a>인증 및 ASP.NET Core SignalR의 권한 부여

[Andrew Stanton-nurse](https://twitter.com/anurse)

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/authn-and-authz/sample/) [(다운로드 방법)](xref:index#how-to-download-a-sample)

## <a name="authenticate-users-connecting-to-a-signalr-hub"></a>SignalR 허브에 연결 된 사용자를 인증 합니다.

SignalR을 사용 하 여 사용할 수 있습니다 [ASP.NET Core 인증](xref:security/authentication/index) 각 연결을 사용 하 여 사용자를 연결 합니다. 허브와 인증 데이터에서 액세스할 수 있습니다 합니다 [ `HubConnectionContext.User` ](/dotnet/api/microsoft.aspnetcore.signalr.hubconnectioncontext.user) 속성입니다. 인증을 사용 하면 사용자와 관련 된 모든 연결에서 메서드를 호출할 허브 (참조 [SignalR의 사용자 및 그룹 관리](xref:signalr/groups) 자세한). 여러 연결을 단일 사용자로 연결할 수 있습니다.

### <a name="cookie-authentication"></a>쿠키 인증

브라우저 기반 앱에서 쿠키 인증에는 SignalR 연결에 자동으로 이동 하 여 기존 사용자 자격 증명을 수 있습니다. 브라우저 클라이언트를 사용 하는 경우 추가 구성이 필요 하지 않습니다. 사용자가 앱에 로그인 하는 경우 SignalR 연결이이 인증은 자동으로 상속 합니다.

쿠키는 액세스 토큰 전송 방법 브라우저별 있지만 비 브라우저 클라이언트를 보낼 수 있습니다. 사용 하는 경우는 [.NET 클라이언트](xref:signalr/dotnet-client)의 `Cookies` 속성에서 구성할 수 있습니다는 `.WithUrl` 쿠키를 제공 하기 위해 호출 합니다. 그러나.NET 클라이언트에서 쿠키 인증을 사용 하 여 응용 프로그램에서 쿠키에 대 한 인증 데이터를 교환 하기 위한 API를 제공 해야 합니다.

### <a name="bearer-token-authentication"></a>전달자 토큰 인증

클라이언트가 쿠키를 사용 하는 대신 액세스 토큰을 제공할 수 있습니다. 서버 토큰의 유효성을 검사 하 고 사용자를 식별 하는 데 사용 합니다. 이 유효성 검사는 연결이 설정 된 경우에 수행 됩니다. 연결 기간 동안 서버 토큰 해지 확인을 자동으로 재검사 하지 않습니다.

서버에서 전달자 토큰 인증을 사용 하도록 구성 합니다 [JWT 전달자 미들웨어](/dotnet/api/microsoft.extensions.dependencyinjection.jwtbearerextensions.addjwtbearer)합니다.

JavaScript 클라이언트에서 토큰을 제공할 수 있습니다 사용 하 여 [accessTokenFactory](xref:signalr/configuration#configure-bearer-authentication) 옵션입니다.

[!code-typescript[Configure Access Token](authn-and-authz/sample/wwwroot/js/chat.ts?range=63-65)]

.NET 클라이언트는 유사한 [AccessTokenProvider](xref:signalr/configuration#configure-bearer-authentication) 토큰을 구성 하는 데 사용할 수 있는 속성:

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options =>
    { 
        options.AccessTokenProvider = () => Task.FromResult(_myAccessToken);
    })
    .Build();
```

> [!NOTE]
> 제공한 액세스 토큰 함수 전에 호출 됩니다 **마다** SignalR에서 HTTP 요청입니다. (때문에 연결 되어 있는 동안 만료 될 수 있습니다) 연결을 활성 상태로 유지 하기 위해 토큰을 갱신 해야 하는 경우이 함수 내에서 수행 하며 업데이트 된 토큰을 반환 합니다.

표준 웹 Api에서 HTTP 헤더에서 전달자 토큰이 전송 됩니다. 그러나 SignalR은 일부 전송을 사용 하는 경우 브라우저에서 이러한 헤더를 설정할 수 없습니다. Websocket 및 Server-Sent 이벤트를 사용 하는 경우 토큰은 쿼리 문자열 매개 변수로 전송 됩니다. 이 서버에서 지원 하기 위해 추가 구성이 필요 합니다.

[!code-csharp[Configure Server to accept access token from Query String](authn-and-authz/sample/Startup.cs?name=snippet)]

### <a name="cookies-vs-bearer-tokens"></a>전달자 토큰 및 쿠키 

쿠키는 브라우저에 특정 이기 때문에 다른 종류의 클라이언트에서 전송 하기 복잡해 전달자 토큰을 전송 하도록 비교 합니다. 따라서 쿠키 인증 앱만 브라우저 클라이언트에서 사용자를 인증 해야 할 경우가 아니면 권장 되지 않습니다. 전달자 토큰 인증은 권장 되는 방법은 브라우저 클라이언트 이외의 클라이언트를 사용 하는 경우입니다.

### <a name="windows-authentication"></a>Windows 인증

하는 경우 [Windows 인증](xref:security/authentication/windowsauth) 구성 된 앱에서 SignalR 해당 id 하 여 허브를 보호 합니다. 그러나 개별 사용자에 게 메시지를 보내려면 해야 사용자 지정 사용자 ID 공급자를 추가 합니다. 즉, Windows 인증 시스템 사용자 이름을 확인할 SignalR을 사용 하 여 "Nameidentifier" 클레임을 제공 하지 않습니다.

구현 하는 새 클래스 추가 `IUserIdProvider` 및 식별자로 사용 하는 사용자 로부터 클레임 중 하나를 검색 합니다. 예를 들어, "Name" 클레임을 사용 하 (폼에서의 Windows 사용자는 `[Domain]\[Username]`), 다음 클래스를 만듭니다.

```csharp
public class NameUserIdProvider : IUserIdProvider
{
    public string GetUserId(HubConnectionContext connection)
    {
        return connection.User?.FindFirst(ClaimTypes.Name)?.Value;
    }
}
```

대신 `ClaimTypes.Name`에서 값을 사용할 수는 `User` (Windows SID 식별자와 같은 등).

> [!NOTE]
> 선택한 값은 시스템의 모든 사용자 간에 고유 해야 합니다. 이 고, 그렇지 한 명의 사용자를 위한 메시지를 다른 사용자에 게 진행 될 수 있습니다.

이 구성 요소를 등록 하 `Startup.ConfigureServices` 메서드 **후** 호출 `.AddSignalR`

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // ... other services ...

    services.AddSignalR();
    services.AddSingleton<IUserIdProvider, NameUserIdProvider>();
}
```

.NET 클라이언트에서 Windows 인증을 설정 하 여 사용 해야 합니다 [UseDefaultCredentials](/dotnet/api/microsoft.aspnetcore.http.connections.client.httpconnectionoptions.usedefaultcredentials) 속성:

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options =>
    {
        options.UseDefaultCredentials = true;
    })
    .Build();
```

Windows 인증은 Microsoft Internet Explorer 또는 Microsoft Edge를 사용 하는 경우에 브라우저 클라이언트에서 지원 됩니다.

## <a name="authorize-users-to-access-hubs-and-hub-methods"></a>액세스 허브 및 허브 메서드에 대 한 사용자 권한 부여

기본적으로 인증 되지 않은 사용자가 허브의 모든 메서드를 호출할 수 있습니다. 인증을 요구 하기 위해 적용 된 [권한 부여](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute) 허브 특성:

[!code-csharp[Restrict a hub to only authorized users](authn-and-authz/sample/Hubs/ChatHub.cs?range=8-10,32)]

생성자 인수 및 속성을 사용할 수는 `[Authorize]` 특정 일치만 사용자에 게 액세스를 제한 하는 특성 [권한 부여 정책](xref:security/authorization/policies)합니다. 예를 들어 라는 사용자 지정 권한 부여 정책이 있는 `MyAuthorizationPolicy` 해당 정책과 일치 하는 사용자만 다음 코드를 사용 하 여 허브에 액세스할 수 있는지 확인 합니다.

```csharp
[Authorize("MyAuthorizationPolicy")]
public class ChatHub: Hub
{
}
```

개별 허브 메서드에 사용할 수는 `[Authorize]` 특성으로 적용 합니다. 현재 사용자 메서드에 적용 된 정책에 맞지 경우 호출자에 게 오류가 반환 됩니다.

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
