---
uid: signalr/overview/older-versions/hub-authorization
title: SignalR 허브 프로그램용 인증과 권한 부여 (SignalR 1.x) | Microsoft Docs
author: pfletcher
description: 이 항목에서는 어떤 사용자 또는 역할에는 허브 메서드에 액세스할 수를 제한 하는 방법을 설명 합니다.
ms.author: aspnetcontent
ms.date: 10/17/2013
ms.assetid: 3d2dfc0e-eac2-4076-a468-325d3d01cc7b
msc.legacyurl: /signalr/overview/older-versions/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 1bb10a49a0d783300c145c30ad09e31f8e6055d6
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37808281"
---
<a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a>SignalR 허브 프로그램용 인증과 권한 부여 (SignalR 1.x)
====================
하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

> 이 항목에서는 어떤 사용자 또는 역할에는 허브 메서드에 액세스할 수를 제한 하는 방법을 설명 합니다.


## <a name="overview"></a>개요

이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [특성을 권한 부여](#authorizeattribute)
- [모든 허브에 대 한 인증을 요구 합니다.](#requireauth)
- [사용자 지정된 권한 부여](#custom)
- [클라이언트에 인증 정보를 전달 합니다.](#passauth)
- [.NET 클라이언트에 대 한 인증 옵션](#authoptions)

    - [폼 인증 쿠키](#cookie)
    - [Windows 인증](#windows)
    - [연결 헤더](#header)
    - [인증서](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a>특성을 권한 부여

SignalR을 제공 합니다 [권한 부여](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) 허브 또는 메서드에 있는 권한이 있는 사용자 또는 역할을 지정 하는 특성입니다. 이 특성에는 `Microsoft.AspNet.SignalR` 네임 스페이스입니다. 적용 된 `Authorize` 허브 또는 허브의 특정 메서드 특성입니다. 적용 하는 경우는 `Authorize` 모든 허브에 메서드의 지정 된 권한 부여 요구 사항 허브 클래스 특성이 적용 되 합니다. 권한 부여 요구 사항 적용할 수 있는 다양 한 유형의 다음과 같습니다. 없이 `Authorize` 특성, 허브에서 모든 공용 메서드는 허브에 연결 된 클라이언트에 사용할 수 있습니다.

웹 응용 프로그램에서 이름이 "Admin" 역할을 정의한 경우 해당 역할의 사용자만 다음 코드를 사용 하 여 허브에 액세스할 수 있도록 지정할 수 있습니다.

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

또는 허브에 아래 표시 된 것 처럼 인증 된 사용자 에게만 제공 되는 두 번째 메서드와 모든 사용자가 사용할 수 있는 한 가지 방법을 지정할 수 있습니다.

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

다음 예제에서는 다른 권한 부여 시나리오를 처리 합니다.

- `[Authorize]` -인증 된 사용자만
- `[Authorize(Roles = "Admin,Manager")]` -인증 된 사용자 지정된 된 역할에만
- `[Authorize(Users = "user1,user2")]` – 지정된 된 사용자 이름 사용 하 여 사용자를 인증 된만
- `[Authorize(RequireOutgoing=false)]` -인증 된 사용자 허브를 호출할 수 있습니다 되지만 서버에서 클라이언트에 다시 호출 따라 제한 되지 않습니다 권한 부여와 같은 특정 사용자만 메시지를 보낼 수 있지만 다른 모든 메시지를 받을 수 있습니다. RequireOutgoing 속성 개인 메서드 허브 내에 없는 전체 허브에만 적용할 수 있습니다. RequireOutgoing을 false로 설정 하지 않으면 권한 부여 요구 사항을 충족 하는 사용자만 서버에서 호출 됩니다.

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a>모든 허브에 대 한 인증을 요구 합니다.

호출 하 여 응용 프로그램에서 인증 모든 허브 및 허브 메서드에 대 한 필요할 수 있습니다 합니다 [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) 메서드 시작 하면 응용 프로그램입니다. 여러 허브를 있고 모두에 대 한 인증 요구 사항이 적용 하려는 경우이 메서드를 사용할 수 있습니다. 이 메서드를 사용 하 여 역할, 사용자 또는 나가는 권한 부여를 지정할 수 없습니다. 허브 메서드에 대 한 액세스는 인증 된 사용자로 제한만 지정할 수 있습니다. 그러나 hubs 추가 요구 사항을 지정 하는 방법에 Authorize 특성을 계속 적용할 수 있습니다. 특성에 지정할 필요는 인증의 기본 요구 사항 외에도 적용 됩니다.

다음 예제에서는 인증 된 사용자에 게 모든 허브 메서드를 제한 하는 Global.asax 파일을 보여 줍니다.

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

호출 하는 경우는 `RequireAuthentication()` SignalR 요청을 처리 된 후에 메서드를 SignalR 시킵니다를 `InvalidOperationException` 예외입니다. 파이프라인에 호출 되 고 나면 HubPipeline에 모듈을 추가할 수 없습니다 때문에이 예외가 throw 됩니다. 앞의 예와 호출을 `RequireAuthentication` 의 메서드는 `Application_Start` 첫 번째 요청을 처리 하기 전에 한 번 실행 되는 메서드.

<a id="custom"></a>

## <a name="customized-authorization"></a>사용자 지정된 권한 부여

권한 부여를 결정 하는 방법을 사용자 지정 해야 하는 경우에서 파생 된 클래스를 만들 수 있습니다 `AuthorizeAttribute` 시키고 합니다 [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) 메서드. 이 메서드는 사용자 요청을 완료할 권한이 있는지 확인 하려면 각 요청에 대해 호출 됩니다. 재정의 된 메서드를 권한 부여 시나리오에 필요한 논리를 제공합니다. 다음 예제에서는 클레임 기반 id 통해 권한 부여를 적용 하는 방법을 보여 줍니다.

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a>클라이언트에 인증 정보를 전달 합니다.

클라이언트에서 실행 되는 코드에서 인증 정보를 사용 해야 합니다. 클라이언트에서 메서드를 호출할 때 필요한 정보를 전달 합니다. 예를 들어, 채팅 응용 프로그램 메서드 수를 매개 변수로 전달 메시지를 게시 하는 사용자의 사용자 이름 아래와 같이 합니다.

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

또는 아래와 같이 해당 개체를 매개 변수로 전달 및 인증 정보를 나타내는 개체를 만들 수 있습니다.

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

악의적인 사용자가 해당 클라이언트에서 요청을 모방 하기 위해 사용할 수 있습니다 다른 클라이언트에 하나의 클라이언트 연결 id를 전달 하지 해야 합니다.

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a>.NET 클라이언트에 대 한 인증 옵션

.NET 클라이언트를 인증 된 사용자로 제한 되는 허브와 상호 작용을 하는 콘솔 앱과 같은 경우에 쿠키, 연결 헤더 또는 인증서 인증 자격 증명을 전달할 수 있습니다. 이 섹션의 예제에는 사용자를 인증 하기 위해 이러한 여러 메서드를 사용 하는 방법을 보여 줍니다. SignalR 앱을 완벽 하 게 작동 하지 않습니다. SignalR 사용 하 여.NET 클라이언트에 대 한 자세한 내용은 참조 하세요. [허브 API 가이드-.NET 클라이언트](../guide-to-the-api/hubs-api-guide-net-client.md)합니다.

<a id="cookie"></a>

### <a name="cookie"></a>쿠키

.NET 클라이언트는 ASP.NET 폼 인증을 사용 하는 허브와 상호 작용을 하는 경우에 연결에서 인증 쿠키를 수동으로 설정 해야 합니다. 쿠키를 추가 합니다 `CookieContainer` 속성에는 [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) 개체입니다. 다음 예제에서는 웹 페이지에서 인증 쿠키를 검색 하 고 연결에는 쿠키를 추가 하는 콘솔 앱을 보여 줍니다. URL `https://www.contoso.com/RemoteLogin` 만들려면 해야 하는 웹 페이지에 예제를 가리킵니다. 페이지는 게시 된 사용자 이름 및 암호를 검색 하 고 자격 증명을 사용 하 여 사용자를 로그인 시도 합니다.

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

콘솔 앱 www.contoso.com/RemoteLogin 다음 코드 숨김 파일이 포함 된 빈 페이지를 참조할 수 있는 자격 증명을 게시 합니다.

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a>Windows 인증

Windows 인증을 사용 하면 현재 사용자의 자격 증명을 사용 하 여 전달할 수 있습니다 합니다 [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) 속성입니다. DefaultCredentials의 값에는 연결에 대 한 자격 증명을 설정 합니다.

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a>연결 헤더

응용 프로그램 쿠키에 사용 하지 않는 경우에 연결 헤더에 사용자 정보를 전달할 수 있습니다. 예를 들어 연결 헤더에 토큰을 전달할 수 있습니다.

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

그런 다음 허브에서 사용자의 토큰은 확인 합니다.

<a id="certificate"></a>

### <a name="certificate"></a>인증서

사용자를 확인 하기 위한 클라이언트 인증서를 전달할 수 있습니다. 연결을 만들 때 인증서를 추가 합니다. 다음 예제에서는 연결에 클라이언트 인증서를 추가 하는 방법만 전체 콘솔 앱은 표시 되지 않습니다. 사용 된 [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) 인증서를 만드는 여러 가지 방법으로 제공 하는 클래스입니다.

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
