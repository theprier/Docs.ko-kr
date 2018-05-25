---
uid: signalr/overview/testing-and-debugging/troubleshooting
title: SignalR 문제 해결 | Microsoft Docs
author: pfletcher
description: 이 문서에서는 SignalR 응용 프로그램을 개발 하는 일반적인 문제를 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 4b559e6c-4fb0-4a04-9812-45cf08ae5779
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/testing-and-debugging/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 2394ee81f4592417a034e47db6eefd3e4b91a9af
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="signalr-troubleshooting"></a>SignalR 문제 해결
====================
으로 [Patrick Fletcher](https://github.com/pfletcher)

> 이 문서는 SignalR과 일반적인 문제 해결을 설명합니다.
> 
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR 버전 2
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a>이 항목의 이전 버전
> 
> 이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이
> 
> 이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요. 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


이 문서는 다음 섹션이 포함 되어 있습니다.

- [메서드를 호출 하는 클라이언트와 서버 간에 자동으로 실패](#connection)
- [IIS websockets ping/퐁 비활성 클라이언트 검색을 구성 합니다.](#pong)
- [기타 연결 문제](#other)
- [컴파일 및 서버 쪽 오류](#server)
- [Visual Studio 문제](#vs)
- [인터넷 정보 서비스 문제](#iis)
- [Microsoft Azure issues](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>메서드를 호출 하는 클라이언트와 서버 간에 자동으로 실패

이 섹션에서는 의미 있는 오류 메시지가 표시 되지 않고 실패 하는 클라이언트와 서버 간의 메서드 호출에 대 한 가능한 원인을 설명 합니다. SignalR 응용 프로그램에서 서버에 클라이언트 구현; 하는 방법에 대 한 정보가 없습니다. 서버 클라이언트 메서드를 호출 하면 메서드 이름과 매개 변수 데이터는 클라이언트에 전송 되 고 메서드는 서버를 지정 하는 형식에 있는 경우에 실행 됩니다. 메서드가 아무 작업도 수행 클라이언트에서 발견 되는 서버에 오류 메시지가 발생 하는 경우.

더 자세히 조사 하려면 클라이언트 메서드를 호출 하지, 서버에서 들어오는 어떤 호출을 표시 하도록 허브에서 start 메서드 호출 하기 전에 로깅을 설정할 수 있습니다. JavaScript 응용 프로그램에 로그인 할 참조 [클라이언트 쪽 로깅 (JavaScript 클라이언트 버전)를 사용 하도록 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)합니다. .NET 클라이언트 응용 프로그램에 로그인 할 참조 [클라이언트 쪽 로깅 (.NET 클라이언트 버전)를 사용 하도록 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-net-client.md#logging)합니다.

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>철자가 잘못 된 메서드, 잘못 된 메서드 서명 또는 잘못 된 허브 이름

이름 또는 호출 메서드의 시그니처가 정확히 일치 하지 않는 클라이언트에서 적절 한 메서드를 호출 실패 합니다. 호출 하 여 메서드 이름을 클라이언트에 대 한 메서드의 이름과 일치 하는지 확인 합니다. 또한 SignalR 카멜식 대/소문자를 사용 하는 메서드를 사용 하 여 허브 프록시를 만들고 JavaScript에서 적절 한 그대로 따라서 메서드가 호출 `SendMessage` 서버에서 호출 되 `sendMessage` 클라이언트 프록시에 합니다. 사용 하는 경우는 `HubName` 서버 쪽 코드에 특성을 사용 하는 이름을 클라이언트에 허브를 만드는 데 이름 일치 하는지 확인 합니다. 사용 하지 않는 경우는 `HubName` 특성을 카멜식 대, ChatHub 대신 chatHub 같은 JavaScript 클라이언트에 허브의 이름 인지 확인 합니다.

### <a name="duplicate-method-name-on-client"></a>클라이언트에서 중복 된 메서드 이름

대/소문자만 다른 클라이언트에 중복 된 메서드를 되어 있지 않은 것을 확인 합니다. 클라이언트 응용 프로그램 라는 메서드가 경우 `sendMessage`, 메서드 호출 또한 없는지 확인 `SendMessage` 도 합니다.

### <a name="missing-json-parser-on-the-client"></a>클라이언트에서 누락 된 JSON 파서

SignalR의 서버와 클라이언트 간의 호출을 직렬화 하는 데 사용할 수는 JSON 파서가 필요 합니다. 클라이언트는 기본 제공 JSON 파서 (예: Internet Explorer 7)가 없으면 응용 프로그램에서 종료자를 포함 해야 합니다. JSON 파서를 다운로드할 수 있습니다 [여기](http://nuget.org/packages/json2)합니다.

### <a name="mixing-hub-and-persistentconnection-syntax"></a>허브 및 PersistentConnection 구문을 함께

두 개의 통신 모델을 사용 하 여 SignalR: 허브 및 PersistentConnections 합니다. 이러한 두 개의 통신 모델을 호출 하기 위한 구문이 클라이언트 코드에서 서로 다릅니다. 서버 코드에서 허브를 추가한 경우 모든 클라이언트 코드에서는 적절 한 허브 구문을 사용을 확인 합니다.

**JavaScript 클라이언트에에서 만드는 코드를 한 PersistentConnection은 JavaScript 클라이언트**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**JavaScript 클라이언트 코드는 Javascript 클라이언트의 허브 프록시를 생성 합니다.**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**C# 서버 코드 경로 PersistentConnection 매핑되는**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**C# 서버 코드 여러 응용 프로그램의 경우를 허브 또는 여러 허브에 대 한 경로 매핑하는**

[!code-css[Main](troubleshooting/samples/sample4.css)]

### <a name="connection-started-before-subscriptions-are-added"></a>구독 추가 되기 전에 시작 된 연결

연결 허브의 서버에서 호출 될 수 있는 메서드는 프록시에 추가 되기 전에 시작 되 면 메시지를 수신할 되지 않습니다. 다음 JavaScript 코드에서 허브를 제대로 시작 되지 않습니다.

**허브 메시지를 받으려면 수 없는 잘못 된 JavaScript 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

대신, 시작을 호출 하기 전에 메서드 구독을 추가 합니다.

**올바르게 허브에 구독을 추가 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>허브 프록시에 누락 된 메서드 이름

클라이언트에서 서버에 정의 된 메서드는을 구독을 확인 합니다. 서버는 메서드를 정의 하는 경우에 여전히 클라이언트 프록시에 추가 합니다. 메서드는 다음과 같은 방법으로 클라이언트 프록시에 추가할 수 있습니다 (에 메서드가 추가 되는 `client` 하지 허브 직접 허브 소속):

**허브 프록시에 메서드를 추가 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>허브 또는 허브 메서드를 Public로 선언 되지 않았습니다

클라이언트에 표시 되려면 허브 구현 및 메서드도 선언 해야 `public`합니다.

### <a name="accessing-hub-from-a-different-application"></a>다른 응용 프로그램에서 허브에 액세스

SignalR 허브 SignalR 클라이언트를 구현 하는 응용 프로그램을 통해 액세스할 수만 있습니다. SignalR 다른 통신 라이브러리 (예: SOAP 또는 WCF 웹 서비스입니다.)와 상호 작용할 수 없습니다. 대상 플랫폼에서 사용할 수 없는 SignalR 클라이언트 경우 서버의 끝점을 직접 액세스할 수 없습니다.

### <a name="manually-serializing-data"></a>수동으로 데이터를 직렬화합니다.

SignalR 자동으로 사용 됩니다 JSON 메서드를 직렬화 하는 데 매개 변수-여기의 않아도 직접 수행 합니다.

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>OnDisconnected 함수에는 클라이언트에서 실행 되지 않은 원격 허브 메서드

이 동작은 설계 시 의도된 것입니다. 때 `OnDisconnected` 는 호출할 허브 이미 입력는 `Disconnected` 허브 호출 될 메서드를 더 이상 허용 하지 않는 상태입니다.

**C# 서버 코드 올바르게 OnDisconnected 이벤트의 코드를 실행 하는**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="ondisconnect-not-firing-at-consistent-times"></a>OnDisconnect 일관 된 시간에 발생 되지 않습니다

이 동작은 설계 시 의도된 것입니다. 사용자가 활성 SignalR 연결 페이지를 나 가려고 하려고 하는 경우 SignalR 클라이언트는 클라이언트 연결이 중지 되는 서버에 알리기 위해 시도 하는 최상의 노력을 확인 합니다. SignalR 클라이언트의 최상의 경우에서 서버에 연결 시도가 실패 하면, 후 구성 가능한 연결의 서버를 삭제 `DisconnectTimeout` 나중 시간에는 `OnDisconnected` 이벤트가 발생 합니다. 시도가 성공 하는 SignalR 클라이언트의 최상의 경우는 `OnDisconnected` 이벤트는 즉시 발생 합니다.

설정에 대 한 내용은 `DisconnectTimeout` 참조 설정, [연결 수명 이벤트를 처리: DisconnectTimeout](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout)합니다.

### <a name="connection-limit-reached"></a>연결 제한에 도달

Windows 7과 같은 클라이언트 운영 체제에서 IIS의 전체 버전을 사용할 경우 10 연결 제한 됩니다. 클라이언트 운영 체제를 사용 하는 경우 IIS Express 대신 사용이 제한을 피할 수 있습니다.

### <a name="cross-domain-connection-not-set-up-properly"></a>도메인 간 연결을 적절히 설정 되지

도메인 간 연결 하는 경우 (입니다 SignalR URL이 호스팅 페이지와 동일한 도메인에 연결)가 올바르게 설정 되지, 오류 메시지 없이 연결이 실패할 수 있습니다. 도메인 간 통신을 사용 하는 방법에 대 한 정보를 참조 하십시오. [도메인 간 연결을 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)합니다.

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>.NET 클라이언트에서 작동 하지 않을 NTLM (Active Directory)를 사용 하 여 연결

도메인 보안을 사용 하는.NET 클라이언트 응용 프로그램에서 연결 연결이 제대로 구성 되지 않은 경우에 실패할 수 있습니다. 도메인 환경에서 SignalR을 사용 하려면 필요한 연결 속성을 다음과 같이 설정.

**C# 클라이언트 코드는 연결 자격 증명을 구현 합니다.**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="pong"></a>

## <a name="configuring-iis-websockets-to-pingpong-to-detect-a-dead-client"></a>IIS websockets ping/퐁 비활성 클라이언트 검색을 구성 합니다.

SignalR의 서버 클라이언트는 작동 하지 않는 또는 not이 고 의존 연결 실패에 대 한 기본 websocket에서 알림을 즉, OnClose 콜백 하는 경우 알 수 없습니다. 이 문제에 대 한 한 가지 해결 ping/퐁 안 IIS websockets를 구성 하는 것입니다. 이렇게 하면 예기치 않게 중단 연결이 종료 됩니다. 자세한 내용은 참조 [이 stackoverflow 게시물](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss)합니다.

<a id="other"></a>

## <a name="other-connection-issues"></a>기타 연결 문제

이 섹션에서는 원인과 그 해결 특정 증상 또는 연결 하는 동안 발생 하는 오류 메시지에 대 한 설명입니다.

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>"시작 해야 데이터를 보내기 전에 호출 됨" 오류

이 오류는 일반적으로 연결을 시작 하기 전에 코드 SignalR 개체를 참조 하는 경우에 표시 됩니다. 처리기와 유사한에 대 한 연결이 메서드를 호출 하는 서버에 정의 된 추가 되어야 함을 연결이 완료 된 후입니다. 에 대 한 호출 `Start` 비동기 이므로 호출 되기 전에 실행 될 수 후에 코드를 완료 합니다. 처리기를 추가 하려면 연결이 완전히 시작 된 후에 start 메서드를 매개 변수로 전달 되는 콜백 함수에 배치 하는 가장 좋은 방법은:

**올바르게 SignalR 개체를 참조 하는 이벤트 처리기를 추가 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

이 오류는 연결 하는 SignalR 개체가 여전히 참조 하는 동안 중지 하는 경우에 나타납니다.

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>"301 영구적으로 이동" 또는 "302 일시적으로 이동" 오류

이 오류는 프로젝트에 자동으로 만들어진 프록시에 방해가 됩니다는 SignalR 이라는 경우 나타날 수 있습니다. 이 오류를 방지 하려면 라는 폴더를 사용 하지 않는 `SignalR` 응용 프로그램 또는 off 자동 프록시 생성 설정에서 합니다. 참조 [은을 수행 하 고 생성 된 프록시](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) 자세한 세부 정보에 대 한 합니다.

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>.NET 또는 Silverlight 클라이언트에서 "403 사용할 수 없음" 오류

이 오류는 도메인 간 통신 해제 되어 없는 제대로 도메인 간 환경에서 발생할 수 있습니다. 도메인 간 통신을 사용 하는 방법에 대 한 정보를 참조 하십시오. [도메인 간 연결을 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)합니다. Silverlight 클라이언트에서 도메인 간 연결을 설정 하려면 참조 [Silverlight 클라이언트에서 도메인 간 연결](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)합니다.

### <a name="404-not-found-error"></a>"404 찾을 수 없음" 오류

이 문제에 대 한 여러 원인이 있습니다. 다음을 모두 확인 합니다.

- **허브 프록시 주소 참조 형식이 잘못:** 생성 된 허브 프록시 주소에 대 한 참조 올바르게 포맷 되어 있지 않으면이 오류는 일반적으로 표시 됩니다. 허브 주소에 대 한 참조가 제대로 적용 하 고 있는지 확인 합니다. 참조 [동적으로 생성 된 프록시를 참조 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) 대 한 자세한 내용은 합니다.
- **허브 경로 추가 하기 전에 응용 프로그램에 경로 추가:** 응용 프로그램에서 다른 경로 사용 하는 경우 추가 하는 첫 번째 경로에 대 한 호출 인지 확인 `MapSignalR`합니다.
- **확장명 없는 Url에 대 한 업데이트가 없는 7.5 또는 IIS 7을 사용 하 여:** 를 사용 하 여 IIS 7 또는 7.5를 업데이트 해야 확장명 없는 Url에 대 한 서버에서의 허브 정의에 대 한 액세스를 제공할 수 있도록 `/signalr/hubs`합니다. 업데이트를 찾을 수 [여기](https://support.microsoft.com/kb/980368)합니다.
- **IIS 캐시 만료 됨 또는 손상 되어:** 캐시 내용 만료 됨 없는지를 확인 하려면 캐시를 지우는 PowerShell 창에서 다음 명령을 입력 합니다.

    [!code-powershell[Main](troubleshooting/samples/sample11.ps1)]

### <a name="500-internal-server-error"></a>"500 내부 서버 오류"

다양 한 원인이 있을 수 있으며 매우 일반적인 오류입니다. 오류의 세부 정보는 서버의 이벤트 로그에 표시 되어야 또는 서버 디버깅을 통해 확인할 수 있습니다. 자세한 오류가 서버에서 설정 하 여 자세한 오류 정보를 얻을 수 있습니다. 자세한 내용은 참조 [허브 클래스에는 오류 처리 방법을](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)합니다.

이 오류는 일반적으로 방화벽 또는 프록시 구성 되지 않은 경우 적절 하 게 다시 작성 하는 요청 헤더를 일으키는 표시 됩니다. 포트 80 방화벽 또는 프록시에 활성화 되어 있는지 확인 하는 솔루션은입니다.

### <a name="unexpected-response-code-500"></a>"예기치 않은 응답 코드: 500"

응용 프로그램에 사용 된.NET framework의 버전 Web.Config에 지정 된 버전이 일치 하지 않으면이 오류가 발생할 수 있습니다. .NET 4.5의 응용 프로그램 설정 및 Web.Config 파일 둘 다에 사용 되 고 있는지 확인 하는 솔루션은입니다.

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>"TypeError: &lt;hubType&gt; 정의 되지 않았습니다" 오류

경우이 오류가 발생에 대 한 호출 `MapSignalR` 제대로 수행 되지 않습니다. 참조 [SignalR 미들웨어를 등록 하 고 SignalR 옵션을 구성 하는 방법을](../guide-to-the-api/hubs-api-guide-server.md#route) 자세한 정보에 대 한 합니다.

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>JsonSerializationException은 사용자 코드에 의해 처리 되지 않았습니다.

메서드에 보낼 매개 변수 (예: 파일 핸들, 데이터베이스 연결) serializable이 아닌 형식에 포함 되어 있는지 확인 합니다. 사용 하 여 (또는 보안에 대 한 직렬화에 속하는 이유로), 클라이언트에 전송 하지 않으려는 서버 측 개체에 멤버를 사용 해야 하는 경우는 `JSONIgnore` 특성입니다.

### <a name="protocol-error-unknown-transport-error"></a>"프로토콜 오류: 알 수 없는 전송" 오류

이 오류는 클라이언트가 SignalR에서 사용 되는 전송을 지원 하지 않는 경우에 발생할 수 있습니다. 참조 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports) 정보를 브라우저 사용 하 여 SignalR에 대 한 합니다.

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>"JavaScript Hub 프록시 생성이 비활성화 되었습니다."

이 오류가 발생 합니다 `DisableJavaScriptProxies` 에서 동적으로 생성 된 프록시에 대 한 참조를 포함 하는 동안 설정 된 `signalr/hubs`합니다. 프록시를 수동으로 만드는 방법에 대 한 자세한 내용은 참조 하십시오. [생성 된 프록시 및 수에 대 한 역할](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)합니다.

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>"잘못 된 형식의 연결 ID가" 또는 "사용자 id는 활성 SignalR 연결 중 변경할 수 없습니다." 오류

인증을 사용 하 고 클라이언트 로그 아웃 됩니다. 연결을 중지 하기 전에 경우이 오류가 나타날 수 있습니다. 솔루션은 클라이언트 로그 아웃 하기 전에 SignalR 연결을 중지 하는 것입니다.

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>"오류 확인할 수 없는: SignalR: jQuery 찾을 수 없습니다. JQuery SignalR.js 파일 전에 참조를 확인 하십시오"오류

SignalR JavaScript 클라이언트를 실행 하는 jQuery 필요 합니다. 참조 jQuery 사용 하는 경로 올바른지 및 SignalR에 대 한 참조 하기 전에 jQuery에 대 한 참조 인지 정확한 지 확인 합니다.

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>"TypeError 확인할 수 없는: 속성을 읽을 수 없습니다 '&lt;속성&gt;' 정의 되지 않은의" 오류

JQuery 또는 허브 프록시 올바르게 참조 하지 않아도이 오류가 발생 합니다. JQuery 및 허브 프록시에서는 참조 올바름, 사용 되는 경로가 올바른지, jQuery에 대 한 참조 허브 프록시에 대 한 참조 하기 전에 있는지 확인 합니다. 허브 프록시에 대 한 기본 참조는 다음과 같이 표시 됩니다.

**허브 프록시를 올바르게 참조 하는 HTML 클라이언트 쪽 코드**

[!code-html[Main](troubleshooting/samples/sample12.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>"RuntimeBinderException 처리 되지 않았습니다. 사용자 코드에서" 오류

이 오류가 발생할 때의 잘못 된 오버 로드 `Hub.On` 사용 됩니다. 메서드 반환 값이 있으면 반환 형식은 제네릭 형식 매개 변수로 지정 해야 합니다.

**생성 된 프록시) (없이 클라이언트에 정의 된 메서드**

[!code-html[Main](troubleshooting/samples/sample13.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>연결 페이지를 로드할 사이 나누기 또는 연결 ID 일치 하지 않습니다.

이 동작은 설계 시 의도된 것입니다. Page 개체에는 허브 개체 호스팅되므로, 허브 페이지를 새로 고칠 때 삭제 됩니다. 다중 페이지 응용 프로그램 사용자와 연결 Id 간의 연결 유지 하는 것은 페이지가 로드 간에 일치 해야 합니다. 연결 Id를 서버에 저장할 수는 `ConcurrentDictionary` 개체 또는 데이터베이스입니다.

### <a name="value-cannot-be-null-error"></a>"값은 null 일 수 없습니다" 오류

선택적 매개 변수를 사용 하 여 서버 쪽 메서드는 현재 지원 되지 않습니다. 선택적 매개 변수를 생략 하면 메서드가 실패 합니다. 자세한 내용은 참조 [선택적 매개 변수](https://github.com/SignalR/SignalR/issues/324)합니다.

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>"Firefox에 있는 서버에 연결을 만들지 &lt;주소&gt;" Firebug 하는 동안 오류가 발생 했습니다.

WebSocket 전송의 협상에 실패 하 고 다른 전송을 대신 사용 하는 경우이 오류 메시지가 Firebug에서 볼 수 있습니다. 이 동작은 설계 시 의도된 것입니다.

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>.NET 클라이언트 응용 프로그램에 오류가 "원격 인증서 유효성 검사 절차에 따라 잘못 되었습니다."

서버에 추가 하 여 x509certificate 연결을 요청 하기 전에 사용자 지정 클라이언트 인증서 필요 합니다. 인증서를 사용 하 여 연결 추가 `Connection.AddClientCertificate`합니다.

### <a name="connection-drops-after-authentication-times-out"></a>인증 시간 초과 후 연결 삭제

이 동작은 설계 시 의도된 것입니다. 연결이 활성 상태 동안 인증 자격 증명을 수정할 수 없습니다. 자격 증명을 새로 고치려면 연결을 중지 했다가 다시 시작 합니다.

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>OnConnected는 jQuery Mobile을 사용 하는 경우에 두 번 호출

jQuery Mobile의 `initializePage` 함수 강제로 다시 실행 하는 각 페이지의 스크립트는 두 번째 연결을 만듭니다. 이 문제에 대 한 솔루션은 다음과 같습니다.

- JQuery Mobile 전에 JavaScript 파일에 대 한 참조를 포함 합니다.
- 사용 하지 않도록 설정 된 `initializePage` 설정 하 여 함수 `$.mobile.autoInitializePage = false`합니다.
- 연결을 시작 하기 전에 초기화를 완료 하려면 페이지를 기다립니다.

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>이벤트를 전송 하는 서버를 사용 하 여 Silverlight 응용 프로그램에서 메시지가 지연

Silverlight에서 이벤트를 보낸 서버를 사용 하는 경우 메시지가 지연 되었습니다. 연결을 시작할 때 긴 폴링과 대신 사용할를 강제로 표시 하려면 다음을 사용 합니다.

[!code-css[Main](troubleshooting/samples/sample14.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>프로토콜 프레임 영원히 "권한이 거부 되었습니다"를 사용 하 여

이것은 알려진된 문제를 설명 [여기](https://github.com/SignalR/SignalR/issues/1963)합니다. 최신 JQuery 라이브러리를 사용 하 여 이러한 현상이 나타날 수 있습니다. 해결 방법은 JQuery 1.8.2에 응용 프로그램을 다운 그레이드 하는 것입니다.

### <a name="invalidoperationexception-not-a-valid-web-socket-request"></a>"InvalidOperationException: 올바른 웹 소켓 요청이 아닙니다.

WebSocket 프로토콜을 사용 하지만 네트워크 프록시 요청 헤더를 수정 하는 경우이 오류가 발생할 수 있습니다. 솔루션 포트 80에서 WebSocket을 허용 하도록 프록시를 구성 하는 것입니다.

### <a name="exception-ltmethod-namegt-method-could-not-be-resolved-when-client-calls-method-on-server"></a>"예외: &lt;메서드 이름&gt; 메서드를 확인할 수 없는" 클라이언트가 서버에서 메서드를 호출 하는 경우

이 오류는 배열 등과 같이 JSON 페이로드는 검색할 수 없으므로 데이터 형식을 사용 하 여 발생할 수 있습니다. 이를 해결 하려면 i s t와 같은 JSON으로 검색할 수 있는 데이터 형식을 사용 합니다. 자세한 내용은 참조 [배열 매개 변수가 있는 허브 메서드를 호출할 수 없습니다.NET 클라이언트](https://github.com/SignalR/SignalR/issues/2672)합니다.

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>컴파일 및 서버 쪽 오류

 다음 섹션에는 컴파일러와 서버 쪽 런타임 오류에는 가능한 해결 방법이 포함 되어 있습니다. 

### <a name="reference-to-hub-instance-is-null"></a>허브 인스턴스에 대 한 참조는 null

허브 인스턴스를 각 연결에 대해 만든 있으므로 만들 수 없습니다 허브 인스턴스의 코드에서 직접 합니다. 메서드를 호출할 허브 자체 외부에서 허브를 참조 하세요. [클라이언트 메서드를 호출할 허브 클래스 외부에서 그룹을 관리 하는 방법을](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) 허브 컨텍스트에 대 한 참조를 가져오는 방법에 대 한 합니다.

### <a name="httpcontextcurrentsession-is-null"></a>HTTPContext.Current.Session null입니다.

이 동작은 설계 시 의도된 것입니다. SignalR 이중 메시징을 작동 하지 않으므로 세션 상태를 사용 하도록 설정 하므로 ASP.NET 세션 상태를 지원 하지 않습니다.

### <a name="no-suitable-method-to-override"></a>재정의 하는 적절 한 방법

이전 문서 또는 블로그에서 코드를 사용 하는 경우이 오류가 표시 될 수 있습니다. 변경 되었거나 더 이상 사용 되지 하는 메서드의 이름을 참조 하지 않는지 확인 하십시오 (같은 `OnConnectedAsync`).

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>HostContextExtensions.WebSocketServerUrl null입니다.

이 동작은 설계 시 의도된 것입니다. 이 멤버는 사용 되지 않으며 사용할 수 없습니다.

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>"'Signalr.hubs' 라는 경로 경로 컬렉션에 이미 이" 오류

이 오류는 있으면 나타납니다 `MapSignalR` 응용 프로그램에서 두 번 호출 됩니다. 일부 예제 응용 프로그램 호출 `MapSignalR` 직접 시작 클래스;에 다른 전화할 래퍼 클래스에 있습니다. 응용 프로그램 둘 다 수행 하지 않습니다 확인 합니다.

### <a name="websocket-is-not-used"></a>WebSocket이 사용 되지 않습니다.

서버 및 클라이언트 WebSocket에 대 한 요구 사항을 충족 하는지 확인 한 경우 (에 나열 된는 [지원 되는 플랫폼](../getting-started/supported-platforms.md) 문서)를 서버에서 WebSocket을 사용 하도록 설정 해야 합니다. 이 작업을 수행 하는 것에 대 한 지침은 [여기](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)합니다.

### <a name="connection-is-undefined"></a>$.connection 정의 되지 않습니다.

이 오류는 페이지에 스크립트를 제대로 로드 되지 않은 없거나 허브 프록시를 연결할 수 없거나 제대로 액세스 하는 나타냅니다. 페이지에 스크립트 참조는 프로젝트에 로드 된 스크립트에 해당 하는 서버를 실행할 때 /signalr/hubs 브라우저에서 액세스할 수 있는지 확인 합니다.

### <a name="one-or-more-types-required-to-compile-a-dynamic-expression-cannot-be-found"></a>동적 식을 컴파일하는 데 필요한 하나 이상의 형식은 찾을 수 없습니다.

이 오류는 `Microsoft.CSharp` 라이브러리가 없습니다. 에 추가 된 **어셈블리-&gt;프레임 워크** 탭 합니다.

### <a name="caller-state-cannot-be-accessed-from-clientscaller-in-visual-basic-or-in-a-strongly-typed-hub-conversion-from-type-taskof-object-to-type-string-is-not-valid-error"></a>호출자 상태 Clients.Caller 강력한 형식의 허브;에서 또는 Visual basic에서에서 액세스할 수 없습니다. "'String' 형식으로 'Task (Of Object)' 형식에서 변환이 유효 하지 않습니다." 오류

Visual basic에서 또는 강력한 형식의 허브의 호출자 상태에 액세스 하려면 사용 된 `Clients.CallerState` 속성 (SignalR 2.1에 도입 된) 대신 `Clients.Caller`합니다.

<a id="vs"></a>

## <a name="visual-studio-issues"></a>Visual Studio 문제

이 섹션에서는 Visual Studio에서 발생 하는 문제에 설명 합니다.

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>솔루션 탐색기에서 스크립트 문서 노드가 표시 되지 않으면

이 자습서의 일부 디버깅 하는 동안 솔루션 탐색기의 "스크립트 문서" 노드로 이동합니다. 이 노드는 JavaScript 디버거에서 생성 및 Internet Explorer;의 브라우저 클라이언트를 디버깅 하는 동안에 나타납니다. Chrome 또는 Firefox 사용 되는 경우에 노드가 표시 되지 않습니다. JavaScript 디버거도 실행 되지 않습니다 Silverlight 디버거와 같은 다른 클라이언트 디버거가 실행 중인 경우.

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>또는 이전 버전의 Visual Studio 2008 SignalR 작동 하지 않습니다.

이 동작은 설계 시 의도된 것입니다. SignalR은.NET Framework 4 이상을;이 필요 Visual Studio 2010 이상에서 SignalR 응용 프로그램을 개발할 수 있어야 합니다. SignalR의 서버 구성 요소가.NET Framework 4.5를 필요합니다.

<a id="iis"></a>

## <a name="iis-issues"></a>IIS 문제

이 섹션에는 인터넷 정보 서비스 문제가 포함 되어 있습니다.

### <a name="signalr-works-on-visual-studio-development-server-but-not-in-iis"></a>IIS 있지만 Visual Studio 개발 서버에서 작동 하는 SignalR

SignalR에서 IIS 7.0 및 7.5를 업그레이드할 수 있지만 지원 확장명 없는 Url을 추가 해야 합니다. 확장명 없는 Url에 대 한 지원을 추가할 참조 [https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)

SignalR ASP.NET (ASP.NET가 IIS에 기본적으로 설치 되지) 서버에 설치 되어 있어야 합니다. ASP.NET을 설치 하려면 참조 [ASP.NET 다운로드](https://www.asp.net/downloads)합니다.

<a id="azure"></a>

## <a name="microsoft-azure-issues"></a>Microsoft Azure issues

이 섹션에는 Microsoft Azure 문제가 포함 되어 있습니다.

### <a name="fileloadexception-when-hosting-signalr-in-an-azure-worker-role"></a>FileLoadException SignalR의 Azure 작업자 역할을 호스트 하는 경우

Azure 작업자 역할에서 SignalR 호스팅 예외가 발생할 수 있습니다 "파일이 나 어셈블리를 로드할 수 없습니다 ' Microsoft.Owin, Version = 2.0.0.0"입니다. 이것은; NuGet이 포함 된 알려진된 문제 Azure 작업자 역할 프로젝트에서 바인딩 리디렉션은 자동으로 추가 되지 않습니다. 이 해결 하려면 바인딩 리디렉션을 수동으로 추가할 수 있습니다. 다음 줄을 추가 하는 `app.config` 작업자 역할 프로젝트에 대 한 파일입니다.

[!code-xml[Main](troubleshooting/samples/sample15.xml)]

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>항목 이름 변경 후 Azure 백플레인에서 통해 메시지가 수신 되지 않은

Azure 백플레인에서에서 사용 하는 항목은 내부적으로; 유지 관리 사용자를 구성할 수 없습니다.
