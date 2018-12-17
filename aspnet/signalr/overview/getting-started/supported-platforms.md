---
uid: signalr/overview/getting-started/supported-platforms
title: 지원 되는 플랫폼 | Microsoft Docs
author: pfletcher
description: 이 문서에서는 어떤 클라이언트 및 서버에 SignalR 지 설명 합니다.
ms.author: riande
ms.date: 04/18/2018
ms.assetid: eac31beb-0f46-4afa-9def-e80904dea4f0
msc.legacyurl: /signalr/overview/getting-started/supported-platforms
msc.type: authoredcontent
ms.openlocfilehash: e270f9a328f36854fdfb3e23b78e0b40cdda6411
ms.sourcegitcommit: 74e3be25ea37b5fc8b4b433b0b872547b4b99186
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53287377"
---
<a name="supported-platforms"></a>지원되는 플랫폼
====================
[Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 어떤 클라이언트 및 서버에 SignalR 지 설명 합니다. 
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이 있으면
> 
> 이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요. 에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.

SignalR은 다양 한 서버 및 클라이언트 구성에서 지원 됩니다. 또한 각 전송 옵션에는 고유한; 요구 사항 전송에 대 한 시스템 요구 사항에 사용할 수 없으면 SignalR 정상적으로 장애 조치 다른 전송 됩니다. SignalR을 지 원하는 전송에 대 한 자세한 내용은 참조 하세요. [전송과 대체](introduction-to-signalr.md#transports)합니다.

## <a name="server-system-requirements"></a>서버 시스템 요구 사항

다양 한 서버 구성에서 SignalR 서버 구성 요소를 호스팅할 수 있습니다. 이 섹션에서는 지원 되는 버전의 운영 체제,.NET framework, 인터넷 정보 서버 및 기타 구성 요소를 설명 합니다.

### <a name="supported-server-operating-systems"></a>지원되는 서버 운영 체제

다음 서버 또는 클라이언트 운영 체제에서 SignalR 서버 구성 요소를 호스팅할 수 있습니다. Websocket을 사용 하는 SignalR에 대 한 Windows Server 2012, Windows Server 2016 또는 Windows 8이 필요 (WebSocket 사용할 수 있습니다 Windows Azure 웹 사이트에서 사이트의.NET framework 버전 4.5로 설정 되어 있고 웹 소켓 사이트의 사용 가능 구성 페이지)입니다.

- Windows Server 2016
- Windows Server 2012
- Windows Server 2008 r2
- Windows 10
- Windows 8
- Windows 7
- Windows Azure

### <a name="supported-server-net-framework-version"></a>지원 되는 서버.NET Framework 버전

.NET Framework 4.5에서 SignalR 2 에서만 지원 됩니다. 참조 된 [권장 업데이트](#updates) 안정성, 호환성, 안정성 및 성능을 향상 시키는 업데이트에 대 한 섹션입니다.

### <a name="supported-server-iis-versions"></a>지원 되는 서버 IIS 버전

SignalR IIS에서 호스트 되는 경우 다음 버전은 지원 됩니다. 클라이언트 운영 체제를 사용 하는 경우와 같은 개발에 대 한 (Windows 8 또는 Windows 7)에서는 전체 버전의 IIS 또는 Cassini 쓰일 수 없습니다, 최대 연결 이후 아주 빨리 도달할 수 있는 10 개의 동시 연결에 적용 될 것 이므로 note 일시적이 지를 자주 다시 설정 되며 삭제 되지 않습니다 즉시 더 이상 사용 되지 시. 클라이언트 운영 체제에서 IIS Express를 사용 해야 합니다.

또한 WebSocket을 사용 하는 SignalR에 대 한 IIS 8 또는 IIS 8 Express를 사용 해야 합니다, 서버를 Windows 8, Windows Server 2012 이상을 사용 해야 합니다을 IIS에서 WebSocket을 활성화 해야 note 합니다. IIS에서 WebSocket을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [IIS 8.0 WebSocket 프로토콜 지원](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)합니다.

- IIS 8 또는 IIS 8 Express입니다.
- IIS 7 및 7.5입니다. 에 대 한 지원 [확장명 없는 Url](https://support.microsoft.com/kb/980368) 필요 합니다.
- IIS 통합된 모드에서 실행 되어야 합니다. 클래식 모드는 지원 되지 않습니다. 최대 30 초의 메시지 지연 Server-Sent 이벤트 전송을 사용 하 여 클래식 모드에서 IIS를 실행 하는 경우 발생할 수 있습니다.
- 호스팅 응용 프로그램은 완전 신뢰 모드로 실행 되어야 합니다.

## <a name="client-system-requirements"></a>클라이언트 시스템 요구 사항

다양 한 클라이언트 플랫폼에서에서 SignalR은 사용할 수 있습니다. 이 섹션에는 SignalR을 사용 하 여 웹 브라우저, Windows 데스크톱 응용 프로그램, Silverlight 응용 프로그램 및 모바일 장치에 대 한 시스템 요구 사항을 설명 합니다.

### <a name="web-browsers"></a>웹 브라우저

SignalR을 다양 한 웹 브라우저에서에서 사용할 수 있지만 일반적으로 최신 두 버전 에서만 지원 됩니다.

브라우저에서 SignalR을 사용 하는 응용 프로그램에는 jQuery 버전 1.6.4 또는 주 이상 버전 (예: 1.7.2, 1.8.2, 또는 1.9.1) 사용 해야 합니다.

다음 브라우저에서 SignalR은 사용할 수 있습니다.

- Microsoft Internet Explorer 버전 8, 9, 10 및 11입니다. 최신 데스크톱 및 모바일 버전 지원 됩니다.
- Mozilla Firefox: 현재 버전-1, Windows 및 Mac 버전입니다.
- Google Chrome: 현재 버전-1, Windows 및 Mac 버전입니다.
- Safari: 현재 버전-1, Mac 및 iOS 버전입니다.
- Opera: 현재 버전-1, Windows에만 합니다.
- Android 브라우저

특정 브라우저에 요구 하는 것 외에도 SignalR을 사용 하는 다양 한 전송에는 자체의 요구 사항을 갖습니다. 다음 전송 다음 구성에서 지원 됩니다.

<a id="browser"></a>

**웹 브라우저에 대 한 전송 요구 사항**

| 전송 | Internet Explorer | Chrome (Windows 또는 iOS) | Firefox | Safari (OSX 또는 iOS) | Android |
| --- | --- | --- | --- | --- | --- |
| WebSocket | 10+ | 1-현재 | 1-현재 | 1-현재 | N/A |
| 서버에서 전송 이벤트 | N/A | 1-현재 | 1-현재 | 1-현재 | N/A |
| ForeverFrame | 8+ | N/A | N/A | N/A | 4.1 |
| 긴 폴링 | 8+ | 1-현재 | 1-현재 | 1-현재 | 4.1 |

\*: 6 + 전체 기능에 필요 합니다.

#### <a name="unsupported-browsers"></a>지원 되지 않는 브라우저

SignalR while *있습니다* 를 이전 버전의 브라우저에서 주요 문제 없이 실행에서 SignalR을 적극적으로 테스트 하지 마십시오 하 고 일반적으로에 나타날 수 있는 버그를 수정 하지 않습니다.

### <a name="windows-desktop-and-silverlight-applications"></a>Windows 데스크톱 및 Silverlight 응용 프로그램

웹 브라우저에서 실행 하는 것 외에도 SignalR 독립 실행형 Windows 클라이언트 또는 Silverlight 응용 프로그램에서 호스트할 수 있습니다. Windows 데스크톱 및 Silverlight SignalR 응용 프로그램 같은 시스템 요구 사항이 있습니다.

- .NET 4를 사용 하 여 응용 프로그램은 Windows XP SP3 이상을 지원 됩니다.
- .NET Framework 4.5를 사용 하 여 응용 프로그램은 Windows Vista 이상을 지원 됩니다.

운영 체제 및.NET framework 요구 사항 외에도 SignalR을 사용할 수 있는 전송에는 자체의 요구 사항을 갖습니다. 다음 전송 다음 구성에서 지원 됩니다.

**Windows 데스크톱 및 Silverlight 전송 요구 사항**

| 전송 | .NET 응용 프로그램 | Silverlight |
| --- | --- | --- |
| 웹 소켓 | Windows 8 이상 및.NET 4.5 이상 | N/A |
| 영원히 프레임 | N/A | N/A |
| 서버에서 전송 이벤트 | .NET 4+ | 5+ |
| 긴 폴링 | .NET 4+ | 5+ |

<a id="android"></a>

### <a name="windows-store-and-windows-phone-applications"></a>Windows 스토어 및 Windows Phone 응용 프로그램

Windows 스토어 응용 프로그램 및 Windows Phone 8 응용 프로그램에서 SignalR은 사용할 수 있습니다. 다음 전송 다음 구성에서 지원 됩니다.

**Windows 스토어 및 Windows Phone 전송 요구 사항**

| 전송 | Windows 스토어 /.NET | Windows 스토어 / JavaScript | Windows Phone / IE | Windows Phone /.NET |
| --- | --- | --- | --- | --- |
| WebSocket | N/A | Win8 + | 8+ | N/A |
| 영원히 프레임 | N/A | Win8 + | 7.5+ | N/A |
| 서버에서 전송 이벤트 | Win8 + | N/A | N/A | 8+ |
| 긴 폴링 | Win8 + | Win8 + | 7.5+ | 8+ |

<a id="updates"></a>

## <a name="recommended-updates"></a>권장 되는 업데이트

SignalR 서버에 대 한 다음 업데이트를 사용 하는 것이 좋습니다.

- .NET Framework 4.5에 대 한 업데이트를 사용할 수 있습니다 [여기](https://support.microsoft.com/kb/2750149)합니다.
- Microsoft은 ASP.NET 용 Qfe를 주기적으로 해제 됩니다. 이 사용 가능한 것으로 적용 됩니다.
