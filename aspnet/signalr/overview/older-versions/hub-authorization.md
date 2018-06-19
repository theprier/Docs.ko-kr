---
uid: signalr/overview/older-versions/hub-authorization
title: 인증 및 권한 부여 SignalR 허브에 대 한 (SignalR 1.x) | Microsoft Docs
author: pfletcher
description: 이 항목에 있는 사용자 또는 역할에는 허브 메서드에 액세스할 수를 제한 하는 방법을 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: 3d2dfc0e-eac2-4076-a468-325d3d01cc7b
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: d73ab6c9091556a62e5d9475baf67a18e305585f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28042877"
---
<a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a>인증 및 권한 부여 SignalR 허브에 대 한 (SignalR 1.x)
====================
여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

> 이 항목에 있는 사용자 또는 역할에는 허브 메서드에 액세스할 수를 제한 하는 방법을 설명 합니다.


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
    - [Certificate](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a>특성을 권한 부여

SignalR 제공는 [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) 특성을 허브 또는 메서드에 있는 권한이 있는 사용자 또는 역할을 지정 합니다. 이 특성에는 `Microsoft.AspNet.SignalR` 네임 스페이스입니다. 적용는 `Authorize` 특성을 허브 또는 허브의 특정 메서드 중 하나입니다. 적용 하는 경우는 `Authorize` 허브에서 메서드의 모든 특성을 허브 클래스를 지정 된 인증 요구 사항에 적용 됩니다. 권한 부여 요구 사항 적용할 수 있는 다양 한 유형의 아래에 표시 됩니다. 없이 `Authorize` 특성, 허브에서 모든 공용 메서드는 허브에 연결 하는 클라이언트에 사용할 수 있습니다.

웹 응용 프로그램에서 이름이 "Admin" 역할을 정의 하면 해당 역할의 사용자만를 다음 코드로 허브에 액세스할 수 있도록 지정할 수 있습니다.

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

또는 허브를 아래와 같이 인증 된 사용자 에게만 제공 되는 두 번째 방법 및 모든 사용자에 게 사용할 수 있는 메서드가 포함 되어 있는지를 지정할 수 있습니다.

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

다음 예에서는 다양 한 권한 부여 시나리오를 처리 합니다.

- `[Authorize]`-인증 된 사용자만
- `[Authorize(Roles = "Admin,Manager")]`-인증 된 사용자 지정된 된 역할에만
- `[Authorize(Users = "user1,user2")]`– 지정된 된 사용자 이름 가진 사용자를 인증 된만
- `[Authorize(RequireOutgoing=false)]`-인증 된 사용자가 허브를 호출할 수 있지만 서버에서 클라이언트로 다시 호출 제한할 수 없는 권한 부여와 같은 특정 사용자만 메시지를 보낼 수 있지만 다른 모든 메시지를 받을 수만 있습니다. RequireOutgoing 속성 허브 내에서 개인 메서드에 없는 전체 hub에만 적용할 수 있습니다. RequireOutgoing을 false로 설정 하지 않으면 권한 부여 요구 사항을 충족 하는 사용자만 서버에서 호출 됩니다.

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a>모든 허브에 대 한 인증을 요구 합니다.

호출 하 여 응용 프로그램에서 인증 모든 허브 및 허브 메서드에 대 한 필요할 수 있습니다는 [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) 메서드 응용 프로그램이 시작 합니다. 여러 허브 있고 모두에 대 한 인증 요구를 적용 하려는 경우이 메서드를 사용할 수 있습니다. 이 메서드로 역할, 사용자 또는 나가는 권한 부여를 지정할 수 없습니다. 허브 메서드에 대 한 액세스는 인증 된 사용자로 제한만 지정할 수 있습니다. 그러나 권한 부여 속성 허브 또는 추가 요구 사항을 지정 하는 메서드를 여전히 적용할 수 있습니다. 특성에서 지정한 모든 요구 사항 인증의 기본 요구 사항 외에도 적용 됩니다.

다음 예제에서는 인증 된 사용자에 게 모든 허브 메서드를 제한 하는 Global.asax 파일을 보여 줍니다.

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

호출 하는 경우는 `RequireAuthentication()` SignalR 요청 처리 된 후에 메서드, SignalR는 throw 한 `InvalidOperationException` 예외입니다. 파이프라인 호출 된 후 HubPipeline에 모듈을 추가할 수 없으므로이 예외가 throw 됩니다. 이전 예제에서는 호출은 `RequireAuthentication` 에서 메서드는 `Application_Start` 메서드 첫 번째 요청을 처리 하기 전에 한 번 실행 합니다.

<a id="custom"></a>

## <a name="customized-authorization"></a>사용자 지정된 권한 부여

권한 부여를 결정 하는 방법을 사용자 지정 해야 할 경우에서 파생 되는 클래스를 만들 수 있습니다 `AuthorizeAttribute` 재정의 [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) 메서드. 이 메서드는 사용자에 게 요청을 완료할 수 있는 권한이 있는지 확인 하려면 각 요청에 대해 호출 됩니다. 재정의 된 메서드에서 권한 부여 시나리오에 필요한 논리를 제공합니다. 다음 예제에서는 클레임 기반 id 통해 권한 부여를 적용 하는 방법을 보여 줍니다.

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a>클라이언트에 인증 정보를 전달 합니다.

클라이언트에서 실행 되는 코드의 인증 정보를 사용 해야 합니다. 클라이언트에서 메서드를 호출할 때 필요한 정보를 전달 합니다. 예를 들어 채팅 응용 프로그램 메서드에 전달할 수 매개 변수로 메시지를 게시 하는 사람의 사용자 이름 아래와 같이 합니다.

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

또는 다음과 같이 해당 개체를 매개 변수로 전달 및 인증 정보를 나타내는 개체를 만들 수 있습니다.

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

직접 전달 하면 안 한 클라이언트 연결 id 다른 클라이언트를 악의적인 사용자가 해당 클라이언트의 요청을 모방 하기 위해 사용할 수 없습니다.

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a>.NET 클라이언트에 대 한 인증 옵션

.NET 클라이언트 등이 인증 된 사용자 제한 되는 허브와 상호 작용을 하 여 콘솔 응용 프로그램이 있는 경우에 쿠키, 연결 헤더 또는 인증서 인증 자격 증명을 전달할 수 있습니다. 이 섹션의 예제에는 사용자를 인증 하기 위한 다양 한 방법을 사용 하는 방법을 보여 줍니다. SignalR 응용 프로그램을 완벽 하 게 작동 하지 않습니다. SignalR과.NET 클라이언트에 대 한 자세한 내용은 참조 [허브 API 가이드-.NET 클라이언트](../guide-to-the-api/hubs-api-guide-net-client.md)합니다.

<a id="cookie"></a>

### <a name="cookie"></a>쿠키

.NET 클라이언트는 ASP.NET 폼 인증을 사용 하는 허브와 상호 작용을 하는 경우 연결에서 인증 쿠키를 수동으로 설정 해야 합니다. 쿠키를 추가 `CookieContainer` 속성에는 [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) 개체입니다. 다음 예제에서는 웹 페이지에서 인증 쿠키를 검색 하 고 연결에 해당 쿠키를 추가 하는 콘솔 응용 프로그램을 보여 줍니다. URL `https://www.contoso.com/RemoteLogin` 예제 가리키는 만들려는 해야 하는 웹 페이지입니다. 페이지에서 게시 된 사용자 이름과 암호를 검색 하 고 자격 증명으로 사용자 로그인을 시도할 게 됩니다.

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

콘솔 응용 프로그램에 다음 코드 숨김 파일을 포함 하는 빈 페이지를 참조할 수 있는 www.contoso.com/RemoteLogin 자격 증명을 게시 합니다.

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a>Windows 인증

Windows 인증을 사용할 경우 현재 사용자의 자격 증명을 사용 하 여 전달할 수 있습니다는 [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) 속성입니다. DefaultCredentials의 값에는 연결에 대 한 자격 증명을 설정 합니다.

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a>연결 헤더

응용 프로그램에서 쿠키를 사용 하지 않는 경우 연결 헤더의 사용자 정보를 전달할 수 있습니다. 예를 들어 연결 헤더에서 토큰을 전달할 수 있습니다.

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

그런 다음 허브에서 사용자의 토큰을 확인 합니다.

<a id="certificate"></a>

### <a name="certificate"></a>인증서

사용자를 확인 하는 클라이언트 인증서를 전달할 수 있습니다. 연결을 만들 때 인증서를 추가 합니다. 다음 예제에서는 연결;로 클라이언트 인증서를 추가 하는 방법에 대해서만 보여 줍니다. 전체 콘솔 응용 프로그램은 표시 되지 않습니다. 사용 하 여는 [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) 클래스 인증서를 만드는 여러 가지 방법으로 제공 합니다.

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
