---
uid: signalr/overview/older-versions/introduction-to-security
title: SignalR 보안 소개 (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: SignalR 응용 프로그램을 개발할 때 고려해 야 할 보안 문제를 설명 합니다.
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 715a4059-d307-4631-abbb-c789c95d6eb4
msc.legacyurl: /signalr/overview/older-versions/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 94a4598595d025267c69933a03be2c164066cc98
ms.sourcegitcommit: ebf4e5a7ca301af8494edf64f85d4a8deb61d641
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54837808"
---
<a name="introduction-to-signalr-security-signalr-1x"></a>SignalR 보안 소개 (SignalR 1.x)
====================
하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에는 SignalR 응용 프로그램을 개발할 때 고려해 야 할 보안 문제를 설명 합니다.


## <a name="overview"></a>개요

이 문서는 다음 섹션으로 구성됩니다.

- [SignalR 보안 개념](#concepts)

    - [인증 및 권한 부여](#authentication)
    - [연결 토큰](#connectiontoken)
    - [다시 연결 하는 경우 그룹에 다시 참여](#rejoingroup)
- [SignalR에서 교차 사이트 요청 위조를 방지 하는 방법](#csrf)
- [SignalR 보안 권장 사항](#recommendations)

    - [보안 소켓 레이어 (SSL) 프로토콜](#ssl)
    - [보안 메커니즘으로 그룹을 사용 하지 마세요](#groupsecurity)
    - [클라이언트에서 입력을 안전 하 게 처리](#input)
    - [활성 연결을 사용 하 여 사용자 상태 변경 내용 조정](#reconcile)
    - [자동으로 생성 된 JavaScript 프록시 파일](#autogen)
    - [예외](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>SignalR 보안 개념

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>인증 및 권한 부여

SignalR은 응용 프로그램에 대 한 기존 인증 구조에 통합 되도록 설계 되었습니다. 사용자를 인증 하기 위한 모든 기능을 제공 하지 않습니다. 대신 일반적으로 응용 프로그램에서 마찬가지로 SignalR 코드에서 인증의 결과 사용 하 여 다음 작업 사용자를 인증할 수 있습니다. 예를 들어 ASP.NET 폼 인증을 사용 하 여 사용자를 인증 하 고 그런 다음 허브에서 사용자를 적용할 수 있습니다 또는 메서드를 호출할 권한이 있는 역할입니다. 허브에서 사용자 이름 또는 사용자 클라이언트 역할에 속하는지 여부와 같은 인증 정보를 전달할 수 있습니다.

SignalR을 제공 합니다 [권한 부여](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) 허브 또는 메서드에 액세스할 수 있는 사용자 지정 하는 특성입니다. 허브 또는 허브의 특정 메서드를 Authorize 특성을 적용 됩니다. Authorize 특성이 없으면 허브에서 모든 공용 메서드를 허브에 연결 하는 클라이언트 제공 됩니다. 허브에 대 한 자세한 내용은 참조 하세요. [SignalR 허브에 대 한 인증과](../security/hub-authorization.md)합니다.

`Authorize` 특성 hubs 에서만 사용 됩니다. 사용 하는 경우 권한 부여 규칙을 적용 하는 `PersistentConnection` 재정의 해야 합니다는 `AuthorizeRequest` 메서드. 영구 연결에 대 한 자세한 내용은 참조 하세요. [SignalR 영구 연결에 대 한 인증과](../security/persistent-connection-authorization.md)합니다.

<a id="connectiontoken"></a>

### <a name="connection-token"></a>연결 토큰

SignalR은 발신자의 id 유효성을 검사 하 여 악의적인 명령을 실행 하는 위험을 완화 합니다. 각 요청에 대 한 연결 토큰을 인증 된 사용자에 대 한 사용자 이름 및 연결 id를 포함 하는 클라이언트와 서버 간에 전달 됩니다. 연결 id가 새 연결을 만들고 연결 기간 동안 유지 되는 서버에 의해 임의로 생성 된 고유 식별자입니다. 사용자는 웹 응용 프로그램에 대 한 인증 메커니즘을 통해 제공 됩니다. 연결 토큰 암호화 및 디지털 서명을 사용 하 여 보호 됩니다.

![](introduction-to-security/_static/image2.png)

각 요청에 대 한 서버 요청은 지정된 된 사용자에서 들어온 것임을 확인 하는 토큰의 내용을 확인 합니다. 연결 id 사용자 이름 일치 해야 합니다. 사용자 이름 및 연결 id 유효성을 검사 하 여 SignalR 악의적인 사용자를 쉽게 다른 사용자를 가장 하지 못하도록 방지 합니다. 서버 연결 토큰을 확인할 수 없습니다, 하는 경우 요청이 실패 합니다.

![](introduction-to-security/_static/image4.png)

연결 id를 확인 프로세스의 일부 이기 때문에 하지 다른 사용자가 한 사용자의 연결 id를 표시 하거나 클라이언트에서 값을 같은 쿠키에 저장 해야 있습니다.

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>다시 연결 하는 경우 그룹에 다시 참여

기본적으로 SignalR 응용 프로그램 자동으로 다시 할당할 사용자 적절 한 그룹에서 연결을 삭제 하 고 연결 시간이 초과 되기 전에 다시 설정 하는 경우와 같은 임시 중단, 다시 연결 하는 경우. 다시 연결할 때 클라이언트 연결 id와 할당 된 그룹을 포함 하는 그룹 토큰을 전달 합니다. 그룹 토큰을 디지털 서명 및 암호화 됩니다. 클라이언트에서 동일한 연결 id를;를 다시 연결한 후 유지 따라서 다시 연결된 클라이언트에서 전달 된 연결 id를 클라이언트에서 사용 하는 이전 연결 id가 일치 해야 합니다. 이 확인을 다시 연결 하는 경우 권한이 없는 그룹 가입 요청을 전달 하는 악의적인 사용자를 방지 합니다.

그러나 것이 중요 한 그룹 토큰 만료 되지 않습니다. 과거에는 그룹에 속한 사용자를 해당 그룹에서 차단 된 경우 해당 사용자는 금지 된 그룹을 포함 하는 그룹 토큰을 모방할 수 있습니다. 안전 하 게는 그룹에 속해 있는 사용자를 관리 해야 하는 경우 데이터베이스에 같은 서버에서 해당 데이터를 저장 해야 합니다. 사용자 그룹에 속하는지 여부를 서버에서 확인 하는 응용 프로그램 논리를 추가 합니다. 그룹 멤버 자격을 확인 하는 예제를 보려면 [그룹 작업](../guide-to-the-api/working-with-groups.md)합니다.

연결을 임시 중단 후 다시 연결 되 면 적용만 그룹에 자동으로 다시 참여 합니다. 사용자 연결을 해제 하는 경우 응용 프로그램 또는 응용 프로그램이 다시 시작, 응용 프로그램에서 벗어날 올바른 그룹에 해당 사용자를 추가 하는 방법을 처리 해야 합니다. 자세한 내용은 [그룹 작업](../guide-to-the-api/working-with-groups.md)합니다.

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>SignalR에서 교차 사이트 요청 위조를 방지 하는 방법

교차 사이트 요청 위조 (CSRF)은 악성 사이트 보내는 요청에 있는 사용자가 현재 로그인 한 취약 한 사이트를 공격 합니다. SignalR은 SignalR 응용 프로그램에 대 한 유효한 요청을 만들려면 악의적인 사이트에 대 한 가능성이 만들어 CSRF 방지 합니다.

### <a name="description-of-csrf-attack"></a>CSRF 공격의 설명

CSRF 공격의 예는 다음과 같습니다.

1. 사용자가 로그인 `www.example.com`, 폼 인증을 사용 합니다.
2. 서버에서 사용자를 인증 합니다. 인증 쿠키를 포함 하는 서버에서 응답 합니다.
3. 로그 아웃을 하지 않고 사용자가 악성 웹 사이트를 방문 합니다. 다음 HTML 양식을 포함 하는이 악성 사이트: 

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   Form action는 취약 한 사이트 악의적인 사이트에 게시 하는 확인 합니다. CSRF의 "교차 사이트" 부분입니다.
4. 제출 단추를 클릭 합니다. 브라우저 요청을 사용 하 여 인증 쿠키를 포함합니다.
5. 요청은 사용자의 인증 컨텍스트를 사용 하 여 example.com 서버에서 실행 되 고 인증된 된 사용자가 수행할 수 있는 아무 것도 가능 합니다.

이 예제에서는 사용자가 폼 단추 클릭, 있지만 쉽게 SignalR 응용 프로그램에 AJAX 요청을 전송 하는 스크립트를 실행 하는 마찬가지로 악의적인 페이지 수 없습니다. 또한 악성 사이트 "https://" 요청을 보낼 수 있기 때문에 SSL을 사용 하 여 CSRF 공격을 방지 하지 않습니다.

일반적으로 CSRF 공격은 인증용 쿠키를 사용 하는 웹 사이트에 대해 가능한 브라우저 대상 웹 사이트에 모든 관련 쿠키를 보낼 수 없기 때문입니다. 그러나 CSRF 공격 쿠키 악용에 제한 되지 않습니다. 예를 들어, 기본 및 다이제스트 인증은 또한 취약 합니다. 사용자가 기본 또는 다이제스트 인증으로 로그인 한 후 세션 종료 될 때까지 브라우저가 자동으로 자격 증명을 보냅니다.

### <a name="csrf-mitigations-taken-by-signalr"></a>SignalR 수행한 CSRF 완화

SignalR에는 SignalR 응용 프로그램에 유효한 요청을 만들지 못하게 악성 사이트를 방지 하기 위해 다음 단계를 수행 합니다. 이러한 단계는 기본적으로 이동 하 고 코드에서 모든 작업이 필요 하지 않습니다.

- **도메인 간 요청을 사용 하지 않도록 설정**  
 기본적으로 외부 도메인의 SignalR 끝점을 호출 하지 못하게 하려면 SignalR 응용 프로그램에서 도메인 간 요청 비활성화 됩니다. 외부 도메인에서 제공 되는 모든 요청에 잘못 된 자동으로 간주 됩니다을 차단 되었습니다. 이 기본 동작을 유지 하는 것이 좋습니다. 이 고, 그렇지 악성 사이트 수 사용자를 속여 사이트로 명령을 전송 합니다. 도메인 간 요청 사용 해야 하는 경우 참조 [도메인 간 연결을 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) 합니다.
- **쿠키 하지 쿼리 문자열에 연결 토큰을 전달 합니다.**  
 SignalR 쿠키 대신 쿼리 문자열 값으로 연결 토큰을 전달합니다. 쿠키로 연결 토큰을 저장 하지 않으므로,에서 연결 토큰을 전달 되지 않습니다 실수로 브라우저에서 악성 코드가 발생 하는 경우. 또한 현재 연결 이외의 연결 토큰 지속 되지 않습니다. 따라서 악의적인 사용자는 다른 사용자의 인증 자격 증명 요청을 만들 수 없습니다.
- **연결 토큰 확인**  
 에 설명 된 대로 합니다 [연결 토큰](#connectiontoken) 섹션에서는 서버 연결 id는 각 인증 된 사용자와 연결 된 인식 합니다. 서버는 사용자 이름 일치 하지 않는 연결 id의 모든 요청을 처리 하지 않습니다. 그럴 가능성은 악의적인 사용자 사용자 이름 및 현재 임의로 생성 된 연결 id를 알고 있어야 하기 때문에 악의적인 사용자 요청이 유효한 추측할 수 있습니다. 연결 id는 연결이 종료 되는 즉시 무효화 됩니다. 익명 사용자에 게 중요 한 정보를 권한이 있어야 합니다.

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>SignalR 보안 권장 사항

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>보안 소켓 레이어 (SSL) 프로토콜

SSL 프로토콜 암호화를 사용 하 여 클라이언트와 서버 간 데이터 전송 보안. 클라이언트와 서버 간에 중요 한 정보를 전송 하 여 SignalR 응용 프로그램을 전송 하는 경우 전송에 대 한 SSL을 사용 합니다. SSL 설정에 대 한 자세한 내용은 참조 하세요. [IIS 7에서 SSL을 설정 하는 방법을](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)합니다.

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>보안 메커니즘으로 그룹을 사용 하지 마세요

그룹은 관련된 사용자를 수집 하는 편리한 방법 이지만 중요 한 정보에 대 한 액세스를 제한 하기 위해 보안 메커니즘을 하지 않은 합니다. 사용자가 자동으로 다시 가입할 수 그룹을 다시 연결 하는 동안 하는 경우 특히 그렇습니다. 역할에 권한 있는 사용자를 추가 하 고 해당 역할의 멤버로 허브 메서드에 대 한 액세스 제한 대신 것이 좋습니다. 역할 기반 액세스를 제한 하는 예제를 참조 하세요 [SignalR 허브에 대 한 인증과](../security/hub-authorization.md)합니다. 다시 연결 하는 경우 그룹에 대 한 사용자 액세스를 확인 하는 예제를 보려면 [그룹 작업](../guide-to-the-api/working-with-groups.md)합니다.

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>클라이언트에서 입력을 안전 하 게 처리

클라이언트에서 다른 클라이언트에 브로드캐스트를 위한 모든 입력 악의적인 사용자가 다른 사용자에 게 스크립트를 보낼 되지 않습니다 있도록 인코딩해야 합니다. SignalR 응용 프로그램에 다양 한 유형의 클라이언트 있을 수 있으므로 것에서 서버 보다는 수신 클라이언트가 메시지를 인코딩하는 데 좋습니다. 다른 유형의 클라이언트 아니라 웹 클라이언트에 대 한 따라서 작동 HTML 인코딩. 예를 들어, 채팅 메시지를 표시 하는 웹 클라이언트 메서드는 안전 하 게 처리할 사용자 이름 및 메시지를 호출 하 여는 `html()` 함수입니다.

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>활성 연결을 사용 하 여 사용자 상태 변경 내용 조정

사용자의 인증 상태에 대 한 활성 연결이 있는 동안 변경 되 면 사용자는 내용의 오류가 표시 됩니다, 그리고 "사용자 id를 활성 SignalR 연결을 사용 하는 동안 변경할 수 없습니다." 이 경우 응용 프로그램 연결 id와 username 조정 되는지 확인 하려면 서버에 다시 연결 해야 합니다. 예를 들어, 응용 프로그램 사용자가 연결 되어 있는 동안 로그 아웃을 허용 하는 경우 연결에 대 한 사용자 이름이 더 이상 일치 하지 다음 요청에 전달 되는 이름입니다. 사용자가 로그 아웃 전에 연결을 중지 하려면를 다시 시작 합니다.

그러나 대부분의 응용 프로그램을 수동으로 중지 하거나 연결을 시작할 필요는 것이 반드시 합니다. 활성 연결 연결이 자동으로 끊어집니다 및 않습니다 응용 프로그램, Web Forms 응용 프로그램 또는 MVC 응용 프로그램에서 기본 동작과 같은 로그인 한 후 별도 페이지로 사용자를 리디렉션합니다, 로그 아웃 한 후 현재 페이지를 새로 고칩니다. 추가 조치가 필요 합니다.

다음 예에서는 중지 하 고 사용자 상태 변경 되 면 연결을 시작 하는 방법을 보여 줍니다.

[!code-html[Main](introduction-to-security/samples/sample3.html)]

또는 사이트 폼 인증을 사용 하 여 상대 (sliding) 만료를 사용 하 고 올바른 인증 쿠키를 유지 하려면 활동이 없는 경우 사용자의 인증 상태 변경 될 수 있습니다. 이런 경우 사용자를 로그 아웃 됩니다 및 사용자 이름이 더 이상 일치 하지 연결 토큰에서 사용자 이름입니다. 올바른 인증 쿠키를 유지 하려면 웹 서버에서 리소스를 정기적으로 요청 하는 몇 가지 스크립트를 추가 하 여이 문제를 해결할 수 있습니다. 다음 예제에서는 30 분 마다 리소스를 요청 하는 방법을 보여 줍니다.

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>자동으로 생성 된 JavaScript 프록시 파일

각 사용자에 대 한 JavaScript 프록시 파일의 모든 허브 및 메서드를 포함 하지 않을 경우에 파일의 자동 생성을 비활성화할 수 있습니다. 허브 및 메서드를 여러 개 있지만 모든 메서드의 알아야 할 모든 사용자를 원하지 않는 경우이 옵션을 선택할 수 있습니다. 자동 생성을 사용 하지 않도록 설정 하 여 **EnableJavaScriptProxies** 하 **false**합니다.

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

JavaScript 프록시 파일에 대 한 자세한 내용은 참조 하세요. [생성 된 프록시 및 용도를](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)입니다. <a id="exceptions"></a>

### <a name="exceptions"></a>예외

개체 클라이언트에 중요 한 정보를 노출할 수 있으므로 클라이언트에 예외 개체를 전달 하지 마십시오. 대신, 관련 오류 메시지를 표시 하는 클라이언트의 메서드를 호출 합니다.

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
