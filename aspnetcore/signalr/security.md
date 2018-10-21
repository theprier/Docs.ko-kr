---
title: ASP.NET Core SignalR의 보안 고려 사항
author: tdykstra
description: ASP.NET Core SignalR의 인증 및 권한 부여를 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: anurse
ms.custom: mvc
ms.date: 10/17/2018
uid: signalr/security
ms.openlocfilehash: 1adf762cd6de4f0cf62e31c0ec6e595a32ed56f8
ms.sourcegitcommit: f5d403004f3550e8c46585fdbb16c49e75f495f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2018
ms.locfileid: "49477542"
---
# <a name="security-considerations-in-aspnet-core-signalr"></a>ASP.NET Core SignalR의 보안 고려 사항

[Andrew Stanton-nurse](https://twitter.com/anurse)

이 문서에서 SignalR 보안 정보를 제공 합니다.

## <a name="cross-origin-resource-sharing"></a>크로스-원본 자원 공유

[크로스-원본 자원 공유 (CORS)](https://www.w3.org/TR/cors/) 브라우저에서 크로스-원본 SignalR 연결을 허용 하도록 사용할 수 있습니다. JavaScript 코드는 SignalR 앱에서 다른 도메인에서 호스팅되는 경우 [CORS 미들웨어](xref:security/cors) SignalR 앱에 연결 하는 JavaScript를 허용 하도록 설정 해야 합니다. 신뢰 하는 도메인 또는 컨트롤 에서만 크로스-원본 요청을 허용 합니다. 예를 들어:

* 사이트에서 호스팅됩니다. `http://www.example.com`
* SignalR 앱에서 호스팅됩니다. `http://signalr.example.com`

원본만 사용할 수 있도록 SignalR 앱에서 CORS를 구성 해야 `www.example.com`합니다.

CORS를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [크로스-원본 요청 (CORS)](xref:security/cors)합니다. SignalR **필요** 다음 CORS 정책:

* 특정 예상된 원본을 허용 합니다. 모든 원본을 허용 수 있지만 **되지** 보안 또는 권장 합니다.
* HTTP 메서드 `GET` 고 `POST` 허용 해야 합니다.
* 자격 증명 인증 사용 되지 않는 경우에 사용할 수 있어야 합니다.

다음 CORS 정책에서 SignalR 브라우저 클라이언트에서 호스트를 허용 하는 예를 들어 `http://example.com` 에 호스트 된 SignalR 앱에 액세스 하도록 `http://signalr.example.com`:

[!code-csharp[Main](security/sample/Startup.cs?name=snippet1)]

> [!NOTE]
> SignalR은 Azure App Service의 기본 제공 CORS 기능을 사용 하 여 호환 되지 않습니다.

## <a name="websocket-origin-restriction"></a>WebSocket 원본 제한

CORS에서 제공 하는 보호는 websocket 적용 되지 않습니다. 브라우저 수행 **되지**:

* 사전 CORS 요청을 수행 합니다.
* 에 지정 된 제한 사항을 준수 `Access-Control` WebSocket 요청을 생성할 때 헤더입니다.

그러나 브라우저를 보낼 수행을 `Origin` WebSocket 요청을 발급 하는 경우 헤더입니다. 응용 프로그램을 예상된 원본에서 제공 하는 Websocket만 허용 되는지 확인 하려면 이러한 헤더를 검사할 구성 되어야 합니다.

배치 하는 사용자 지정 미들웨어를 사용 하 여 헤더 유효성 검사 가능 ASP.NET Core 2.1 이상 버전에서는 **하기 전에 `UseSignalR`, 및 인증 미들웨어** 에서 `Configure`:

[!code-csharp[Main](security/sample/Startup.cs?name=snippet2)]

> [!NOTE]
> 합니다 `Origin` 헤더는 클라이언트에서 그리고 제어 되는 `Referer` 헤더 가짜일 수 있습니다. 이러한 헤더 해야 **되지** 인증 메커니즘으로 사용할 수 있습니다.

## <a name="access-token-logging"></a>액세스 토큰 로깅

Websocket 또는 Server-Sent 이벤트를 사용 하면 브라우저 클라이언트가 쿼리 문자열에 액세스 토큰을 보냅니다. 쿼리 문자열을 통해 액세스 토큰을 수신 하는 것은 일반적으로 표준을 사용 하는 것 만큼 안전 `Authorization` 헤더입니다. 그러나 여러 웹 서버 로그 쿼리 문자열을 포함 하 여 각 요청에 대 한 URL입니다. 로그인 Url 액세스 토큰을 기록할 수 있습니다. 웹 서버 로깅 설정을 로깅 액세스 토큰을 방지 하기 위해 설정 하는 것이 좋습니다.

## <a name="exceptions"></a>예외

예외 메시지는 일반적으로 클라이언트에 게 공개 하지 않아야 하는 중요 한 데이터를 간주 해야 합니다. 기본적으로 SignalR 클라이언트에 허브 메서드에서 throw 된 예외 세부 정보를 보내지 않습니다. 대신 클라이언트에는 오류가 발생 했음을 나타내는 일반 메시지를 받습니다. 클라이언트에 예외 메시지 배달을 사용 하 여 (예: 개발 또는 테스트) 재정의할 수 있습니다 [ `EnableDetailedErrors` ](xref:signalr/configuration#configure-server-options)합니다. 예외 메시지를 프로덕션 앱에서 클라이언트에 노출 되어야 합니다.

## <a name="buffer-management"></a>버퍼 관리

SignalR은 연결당 버퍼를 사용 하 여 들어오고 나가는 메시지를 관리 합니다. 기본적으로 SignalR 32KB로 이러한 버퍼를 제한합니다. 클라이언트 또는 서버 보낼 수 있는 가장 큰 메시지는 32KB입니다. 메시지에 대 한 연결에서 사용 하는 최대 메모리는 32KB입니다. 32KB 보다 작은 항상 메시지 경우 제한을 줄일 수 있습니다는.

* 클라이언트가 큰 메시지를 보낼 수 없도록 방지 합니다.
* 서버는 메시지를 받을 큰 버퍼를 할당할 필요가 없습니다.

메시지 32KB 보다 큰 경우에 한도 늘릴 수 있습니다. 이 제한을 늘리면 의미 합니다.

* 클라이언트는 대용량 메모리 버퍼를 할당 하도록 서버에 발생할 수 있습니다.
* 대용량 버퍼 server 할당 동시 연결 수를 줄일 수 있습니다.

들어오고 나가는 메시지에 대 한 제한은, 둘 다에서 구성할 수 있습니다 합니다 [ `HttpConnectionDispatcherOptions` ](xref:signalr/configuration#configure-server-options) 개체에 구성 된 `MapHub`:

* `ApplicationMaxBufferSize` 클라이언트에서 바이트의 최대 수를 나타냅니다는 서버 버퍼입니다. 클라이언트를이 제한 보다 큰 메시지를 전송 하려고 하는 경우 연결이 닫힐 수 있습니다.
* `TransportMaxBufferSize` 바이트를 보낼 수의 최대 수를 나타냅니다. 서버를이 제한 보다 큰 메시지 (허브 메서드의 반환 값 포함)를 전송 하려고 하는 경우 예외가 throw 됩니다.

제한 설정을 `0` 제한을 사용 하지 않도록 설정 합니다. 도 제거 하면 모든 규모의 메시지를 보내는 클라이언트 있습니다. 큰 메시지를 전송 하는 악의적인 클라이언트가 과도 한 메모리 할당 될 수 있습니다. 과도 한 메모리 사용량 동시 연결 수를 크게 줄일 수 있습니다.
