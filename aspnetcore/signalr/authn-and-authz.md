---
title: ASP.NET Core SignalR의 인증 및 권한 부여
author: tdykstra
description: ASP.NET Core SignalR에서 인증 및 권한 부여를 사용하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: anurse
ms.custom: mvc
ms.date: 06/29/2018
uid: signalr/authn-and-authz
ms.openlocfilehash: 6624b2b4361eb0a5bb6e45108878ee6fe5ecb443
ms.sourcegitcommit: b34b25da2ab68e6495b2460ff570468f16a9bf0d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53284428"
---
# <a name="authentication-and-authorization-in-aspnet-core-signalr"></a>ASP.NET Core SignalR의 인증 및 권한 부여

작성자: [Andrew Stanton-Nurse](https://twitter.com/anurse)

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/authn-and-authz/sample/) [(다운로드 방법)](xref:index#how-to-download-a-sample)

## <a name="authenticate-users-connecting-to-a-signalr-hub"></a>SignalR 허브에 연결하는 사용자 인증하기

SignalR을 [ASP.NET Core 인증](xref:security/authentication/identity)과 함께 사용하여 각 연결에 사용자를 연결할 수 있습니다. 허브에서는 [`HubConnectionContext.User`](/dotnet/api/microsoft.aspnetcore.signalr.hubconnectioncontext.user) 속성을 통해서 인증 데이터에 접근할 수 있습니다. 인증을 사용하면 허브가 특정 사용자와 관련된 모든 연결에서 메서드를 호출할 수 있습니다(자세한 정보는 [SignalR의 사용자 및 그룹 관리](xref:signalr/groups)를 참고하시기 바랍니다). 단일 사용자에게 다수의 연결을 연결할 수 있습니다.

### <a name="cookie-authentication"></a>쿠키 인증

브라우저 기반의 앱에서 쿠키 인증을 사용할 경우 기존의 사용자 자격 증명을 자동으로 SignalR 연결로 전달할 수 있습니다. 브라우저 클라이언트를 사용하면 추가적인 구성이 필요 없습니다. 사용자가 앱에 로그인하면 자동으로 SignalR 연결이 해당 인증을 상속받습니다.

쿠키는 액세스 토큰을 전송하는 브라우저 고유의 방식이지만 비 브라우저 클라이언트에서도 쿠키를 전송할 수 있습니다. [.NET 클라이언트](xref:signalr/dotnet-client)를 사용할 경우 `.WithUrl` 호출에서 `Cookies` 속성을 구성하여 쿠키를 제공할 수 있습니다. 그러나 .NET 클라이언트에서 쿠키 인증을 사용하려면 앱이 쿠키에 대한 인증 데이터를 교환하는 API를 제공해야 합니다.

### <a name="bearer-token-authentication"></a>전달자 토큰 인증

클라이언트는 쿠키를 사용하는 대신 액세스 토큰을 제공할 수도 있습니다. 서버는 토큰의 유효성을 검사하고 이를 이용해서 사용자를 식별합니다. 이 유효성 검사는 연결이 설정될 때만 수행됩니다. 서버는 연결이 유지되는 동안 토큰이 해지되었는지를 확인하기 위해 자동으로 유효성을 재검사하지 않습니다.

서버에서 전달자 토큰 인증은 [JWT 전달자 미들웨어](/dotnet/api/microsoft.extensions.dependencyinjection.jwtbearerextensions.addjwtbearer)를 사용하여 구성합니다.

JavaScript 클라이언트에서는 [accessTokenFactory](xref:signalr/configuration#configure-bearer-authentication) 옵션을 통해서 토큰을 제공할 수 있습니다.

[!code-typescript[Configure Access Token](authn-and-authz/sample/wwwroot/js/chat.ts?range=63-65)]

.NET 클라이언트에는 토큰을 구성하기 위해 사용할 수 있는 비슷한 [AccessTokenProvider](xref:signalr/configuration#configure-bearer-authentication) 속성이 존재합니다.

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options =>
    { 
        options.AccessTokenProvider = () => Task.FromResult(_myAccessToken);
    })
    .Build();
```

> [!NOTE]
> 지정한 액세스 토큰 함수는 SignalR이 만들어내는 **모든** HTTP 요청 전에 호출됩니다. 연결을 활성 상태로 유지하기 위해 토큰을 갱신해야 할 경우 (연결 중 만료될 수 있으므로), 이 함수 내에서 작업을 수행하고 갱신된 토큰을 반환해야 합니다.

표준 웹 API에서 전달자 토큰은 HTTP 헤더로 전송됩니다. 그러나 일부 전송을 사용하는 경우에는 SignalR이 브라우저에서 이런 헤더를 설정할 수 없습니다. WebSockets 및 서버-전송 이벤트를 사용할 경우 토큰은 쿼리 문자열 매개 변수로 전송됩니다. 서버에서 이를 지원하려면 추가적인 구성이 필요합니다.

[!code-csharp[Configure Server to accept access token from Query String](authn-and-authz/sample/Startup.cs?name=snippet)]

### <a name="cookies-vs-bearer-tokens"></a>쿠키 대 전달자 토큰 

쿠키는 브라우저에 한정되기 때문에 다른 유형의 클라이언트에서 쿠키를 전송하는 작업은 전달자 토큰 전송에 비해 복잡성이 증가합니다. 따라서 앱이 브라우저 클라이언트에서만 사용자 인증이 필요한 것이 아니라면 쿠키 인증은 권장되지 않습니다. 브라우저 클라이언트 이외의 클라이언트도 사용할 경우 전달자 토큰 인증이 권장되는 방식입니다.

### <a name="windows-authentication"></a>Windows 인증

앱에 [Windows 인증](xref:security/authentication/windowsauth)이 구성되어 있을 경우 SignalR은 해당 신원을 이용해서 허브를 보호할 수 있습니다. 그러나 개별 사용자에게 메시지를 전송하려면 사용자 지정 사용자 ID 공급자를 추가해야 합니다. 그 이유는 Windows 인증 시스템이 SignalR이 사용자 이름을 결정하는 데 사용하는 "이름 식별자" 클레임을 제공하지 않기 때문입니다.

`IUserIdProvider`를 구현하는 새 클래스를 추가하고 사용자로부터 식별자로 사용할 클레임 중 하나를 가져옵니다. 예를 들어, "Name" 클레임(`[Domain]\[Username]` 형태의 Windows 사용자 이름)을 사용하려면 다음과 같은 클래스를 생성합니다.

```csharp
public class NameUserIdProvider : IUserIdProvider
{
    public string GetUserId(HubConnectionContext connection)
    {
        return connection.User?.FindFirst(ClaimTypes.Name)?.Value;
    }
}
```

`ClaimTypes.Name` 대신 `User`의 다른 모든 값(예: Windows SID 식별자 등)을 사용할 수 있습니다.

> [!NOTE]
> 선택한 값은 시스템의 모든 사용자 간에 고유해야 합니다. 그렇지 않으면 특정 사용자를 대상으로 한 메시지가 다른 사용자에게 전달될 수 있습니다.

`Startup.ConfigureServices` 메서드에서 `.AddSignalR`을 호출한 **후에** 이 구성 요소를 등록합니다.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // ... other services ...

    services.AddSignalR();
    services.AddSingleton<IUserIdProvider, NameUserIdProvider>();
}
```

.NET 클라이언트에서는 [UseDefaultCredentials](/dotnet/api/microsoft.aspnetcore.http.connections.client.httpconnectionoptions.usedefaultcredentials) 속성을 설정해서 Windows 인증을 활성화시켜야 합니다.

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options =>
    {
        options.UseDefaultCredentials = true;
    })
    .Build();
```

Windows 인증은 Microsoft Internet Explorer 또는 Microsoft Edge를 사용하는 경우에만 브라우저 클라이언트에서 지원됩니다.

## <a name="authorize-users-to-access-hubs-and-hub-methods"></a>허브 및 허브 메서드 접근에 대한 사용자 권한 부여

기본적으로, 인증되지 않은 사용자도 허브의 모든 메서드를 호출할 수 있습니다. 인증을 요구하려면 허브에 [Authorize](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute) 특성을 적용합니다.

[!code-csharp[Restrict a hub to only authorized users](authn-and-authz/sample/Hubs/ChatHub.cs?range=8-10,32)]

`[Authorize]` 특성의 생성자 인수 및 속성을 이용해서 특정 [권한 부여 정책](xref:security/authorization/policies)을 만족하는 사용자만 접근할 수 있도록 제한할 수 있습니다. 예를 들어 `MyAuthorizationPolicy`라는 사용자 지정 권한 부여 정책이 존재할 경우, 다음과 같은 코드를 사용해서 해당 정책을 만족하는 사용자만 허브에 접근할 수 있도록 만들 수 있습니다.

```csharp
[Authorize("MyAuthorizationPolicy")]
public class ChatHub: Hub
{
}
```

각각의 허브 메서드에도 `[Authorize]` 특성을 적용할 수 있습니다. 현재 사용자가 메서드에 적용된 정책을 만족하지 않으면 호출자에게 오류가 반환됩니다.

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

## <a name="additional-resources"></a>추가 자료

* [ASP.NET Core에서 전달자 토큰 인증](https://blogs.msdn.microsoft.com/webdev/2016/10/27/bearer-token-authentication-in-asp-net-core/)
