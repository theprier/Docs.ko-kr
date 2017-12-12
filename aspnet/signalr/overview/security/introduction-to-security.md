---
uid: signalr/overview/security/introduction-to-security
title: "SignalR 보안 소개 | Microsoft Docs"
author: pfletcher
description: "SignalR 응용 프로그램을 개발할 때 고려해 야 할 보안 문제에 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: ffe71f8ea7105db4d5a0c156e2b4e76d6e40761d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="introduction-to-signalr-security"></a>SignalR 보안 소개
====================
여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서는 SignalR 응용 프로그램을 개발할 때 고려해 야 할 보안 문제를 설명 합니다. 
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


## <a name="overview"></a>개요

이 문서는 다음 섹션으로 구성됩니다.

- [SignalR 보안 개념](#concepts)

    - [인증 및 권한 부여](#authentication)
    - [연결 토큰](#connectiontoken)
    - [다시 연결 될 때 그룹에 다시 가입](#rejoingroup)
- [SignalR 교차 사이트 요청 위조를 방지 하는 방법](#csrf)
- [SignalR 보안 권장 사항](#recommendations)

    - [보안 소켓 레이어 (SSL) 프로토콜](#ssl)
    - [그룹에 보안 메커니즘으로 사용 하지 마십시오](#groupsecurity)
    - [클라이언트의 입력을 안전 하 게 처리](#input)
    - [사용자 상태 활성 연결의 변경 내용 조정](#reconcile)
    - [자동으로 생성 된 JavaScript 프록시 파일](#autogen)
    - [예외](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>SignalR 보안 개념

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>인증 및 권한 부여

SignalR은 사용자를 인증 하기 위한 모든 기능을 제공 하지 않습니다. 대신, 응용 프로그램에 대해 기존 인증 구조에는 SignalR 기능을 통합합니다. 일반적으로 응용 프로그램 및 프로그램 SignalR에서 인증의 결과 함께 작업에 코딩할 때 사용자를 인증 합니다. 예를 들어 ASP.NET 폼 인증으로 사용자를 인증 하 고 허브에 있는 사용자를 적용할 수 있습니다 또는 메서드를 호출할 권한이 있는 역할입니다. 허브에서 사용자 이름 또는 사용자를 클라이언트에 게 역할에 속해 있는지 여부와 같은 인증 정보를 전달할 수 있습니다.

SignalR 제공는 [Authorize](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) 허브 또는 메서드에 액세스할 수 있는 사용자 지정 하는 특성입니다. 허브 또는 허브의 특정 메서드 중 하나를 권한 부여 특성을 적용 합니다. 권한 부여 속성 없으면 허브에서 모든 공용 메서드는 허브에 연결 하는 클라이언트에 사용할 수 있습니다. 허브에 대 한 자세한 내용은 참조 [인증 및 권한 부여 SignalR 허브에 대 한](hub-authorization.md)합니다.

적용 된 `Authorize` 허브 있지만 비영구적 연결 특성입니다. 사용 하는 경우 권한 부여 규칙을 적용 하는 `PersistentConnection` 재정의 해야 합니다는 `AuthorizeRequest` 메서드. 영구 연결에 대 한 자세한 내용은 참조 [인증 및 권한 부여 SignalR 영구 연결에 대 한](persistent-connection-authorization.md)합니다.

<a id="connectiontoken"></a>

### <a name="connection-token"></a>연결 토큰

SignalR은 발신자의 id 유효성을 검사 하 여 악의적인 명령이 실행의 위험을 완화 합니다. 각 요청에 대 한 서버와 클라이언트 연결 id 및 인증 된 사용자에 대 한 사용자 이름을 포함 하는 연결 토큰을 전달 합니다. 연결 id는 고유 하 게 연결 된 각 클라이언트를 식별합니다. 서버는 임의로 새 연결을 만들고 해당 id를 계속 되 면 연결 기간에 대 한 연결 id를 생성 합니다. 웹 응용 프로그램에 대 한 인증 메커니즘에는 사용자 이름을 제공합니다. SignalR 연결 토큰을 보호 하기 위해 암호화 및 디지털 서명을 사용 합니다.

![](introduction-to-security/_static/image2.png)

각 요청에 대 한 서버에서 지정된 된 사용자 요청 된 있는지 확인 하는 토큰의 내용을 확인 합니다. 연결 id 사용자 이름 일치 해야 합니다. 연결 id와 사용자 이름이 모두 유효성을 검사 함으로써 SignalR 악의적인 사용자를 쉽게 다른 사용자를 가장 하지 못하도록 방지 합니다. 서버 연결 토큰을 확인할 수 없습니다, 요청이 실패 합니다.

![](introduction-to-security/_static/image4.png)

연결 id는 확인 프로세스의 일부 이므로 하거나 하면 안 한 사용자의 연결 id 다른 사용자에 게 표시와 같은 쿠키에 클라이언트에서 값을 저장 합니다.

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>다시 연결 될 때 그룹에 다시 가입

기본적으로 SignalR 응용 프로그램은 자동으로 다시 할당 사용자 적절 한 그룹에 대 한 연결을 삭제 하 고 연결 시간이 초과 되기 전에 다시 설정 하는 경우 등의 임시 중단에서 다시 연결 될 때. 다시 연결할 때 클라이언트 연결 id 및 할당 된 그룹을 포함 하는 그룹 토큰을 전달 합니다. 그룹 토큰 디지털 서명 및 암호화 됩니다. 클라이언트에 다시 연결한; 후 동일한 연결 id를 유지 따라서 다시 연결 된 클라이언트에서 전달 된 연결 id는 클라이언트에서 사용 하는 이전 연결 id를 일치 해야 합니다. 이 확인 작업에서 다시 연결 될 때 무단된 그룹 가입 요청을 전달 악의적인 사용자가을 방지 합니다.

그러나이 중요 한 그룹 토큰 만료 되지 않습니다. 이전에는 그룹에 속한 사용자 해당 그룹에서 차단 된 경우 해당 사용자는 금지 된 그룹을 포함 하는 그룹 토큰을 모방 하기 위해 수. 있습니다 안전 하 게 어떤 그룹에 속해 있는 사용자를 관리 해야 하는 경우와 같은 데이터베이스에 서버에서 해당 데이터를 저장 해야 합니다. 그런 다음, 사용자 그룹에 속하는지 여부를 서버에서 확인 하는 응용 프로그램에 논리를 추가 합니다. 그룹 구성원 자격을 확인 하는 예제를 보려면 [그룹 작업](../guide-to-the-api/working-with-groups.md)합니다.

연결을 임시 중단 한 후 다시 연결 되 면 적용만 자동으로 그룹에 다시 가입 합니다. 하 여 연결이 끊기는 경우 응용 프로그램 또는 응용 프로그램 다시 시작, 응용 프로그램을 벗어나지 올바른 그룹에 해당 사용자를 추가 하는 방법을 처리 해야 합니다. 자세한 내용은 참조 [그룹 작업](../guide-to-the-api/working-with-groups.md)합니다.

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>SignalR 교차 사이트 요청 위조를 방지 하는 방법

교차 사이트 요청 위조 CSRF ()은 악성 사이트를 사용자가 현재 로그인 취약 한 사이트에 요청을 보냅니다는 방식의 공격입니다. SignalR은 SignalR 응용 프로그램에 대 한 올바른 요청을 만들려면 악성 사이트에 대 한 발생할 가능성이 거의 함으로써 CSRF 수 없습니다.

### <a name="description-of-csrf-attack"></a>CSRF 공격 설명

CSRF 공격의 예는 다음과 같습니다.

1. Www.example.com에 사용자가 사용 하 여 폼 인증 합니다.
2. 서버에서 사용자를 인증 합니다. 서버 로부터 응답 하면 인증 쿠키가 포함 되어 있습니다.
3. 사용자 로그 아웃을 하지 않고 악성 웹 사이트를 방문 합니다. 이 악성 사이트 다음 HTML 폼을 포함 되어 있습니다. 

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

 Form action에는 취약 한 사이트 악성 사이트에 게시 확인 합니다. CSRF의 "사이트 간" 부분입니다.
4. 사용자가 제출 단추를 클릭 합니다. 브라우저에는 요청과 함께 인증 쿠키가 포함 되어 있습니다.
5. 요청은 사용자의 인증 컨텍스트를 사용 하 여 example.com 서버에서 실행 되며 인증된 된 사용자가 수행할 수 있는 모든 작업을 수행할 수 있습니다.

하지만이 예제에서는 양식 단추를 클릭 하 여 사용자, 악의적인 페이지 것 처럼 쉽게 SignalR 응용 프로그램에 AJAX 요청을 전송 하는 스크립트를 실행할 수 있습니다. 또한 악성 사이트 "https://" 요청을 보낼 수 있으므로 SSL을 사용 하 여 CSRF 공격을 방지 하지 않습니다.

일반적으로 CSRF 공격은 브라우저가 대상 웹 사이트에 모든 관련 쿠키를 전송 하기 때문에 인증을 위한 쿠키를 사용 하는 웹 사이트에 대해 가능한 합니다. 그러나 CSRF 공격 쿠키 악용에 제한 되지 않습니다. 예를 들어, 기본 및 다이제스트 인증 취약 됩니다. 기본 또는 다이제스트 인증을 사용 하 여 사용자가 로그 되어 세션이 종료 될 때까지 브라우저가 자동으로 자격 증명을 보냅니다.

### <a name="csrf-mitigations-taken-by-signalr"></a>SignalR 수행한 CSRF 완화

SignalR 악성 사이트에서 응용 프로그램에 대 한 올바른 요청을 만들지 않으려면 다음 단계를 수행 합니다. 기본적으로 이러한 단계를 사용 하는 SignalR, 코드의 어떤 조치도 취할 필요가 없습니다.

- **도메인 간 요청을 사용 하지 않도록 설정**  
 SignalR 외부 도메인의 SignalR 끝점을 호출 하지 못하게 하려면 도메인 간 요청을 해제 합니다. SignalR 외부 도메인의 모든 요청을 유효 하지 않은 것으로 간주 하 고 요청을 차단 합니다. 이 기본 동작을 유지 하는 것이 좋습니다. 그렇지 않으면 악성 사이트 수 사용자 하도록 사이트에 명령을 전송 합니다. 도메인 간 요청 사용 해야 하는 경우 참조 [도메인 간 연결을 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) 합니다.
- **쿼리 문자열 하지 쿠키에에서 연결 토큰을 전달 합니다.**  
 SignalR 쿠키로 대신 쿼리 문자열 값으로 연결 토큰을 전달합니다. 악성 코드가 발견 되 면 브라우저 연결 토큰을 실수로 전달할 수 있으므로 연결 토큰 쿠키에 저장은 안전 하지 않습니다. 또한 쿼리 문자열의 연결 토큰을 전달 합니다. 현재 연결 이상 지속 연결 토큰을 방지 합니다. 따라서 악의적인 사용자는 다른 사용자의 인증 자격 증명 요청을 만들 수 없습니다.
- **연결 토큰을 확인 합니다.**  
 에 설명 된 대로 [연결 토큰](#connectiontoken) 섹션에서 서버를 알고 있는 연결 id는 각 인증 된 사용자와 연결 합니다. 서버는 사용자 이름 일치 하지 않는 연결 id의 모든 요청을 처리 하지 않습니다. 그럴 가능성은 악의적인 사용자가 사용자 이름 및 현재 임의로 생성 된 연결 id를 확인 해야 하기 때문에 악의적인 사용자는 유효한 요청 추측할 수 없습니다. 연결이 종료 되는 즉시 해당 연결 id 없게 됩니다. 익명 사용자가 중요 정보에 액세스할 수 없어야 합니다.

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>SignalR 보안 권장 사항

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>보안 소켓 레이어 (SSL) 프로토콜

SSL 프로토콜 암호화를 사용 하 여 클라이언트와 서버 간의 데이터 전송을 보호. 클라이언트와 서버 간에 중요 한 정보를 전송 하 여 SignalR 응용 프로그램을 전송 하는 경우 전송에 대 한 SSL을 사용 합니다. SSL 설정에 대 한 자세한 내용은 참조 [IIS 7에서 SSL을 설정 하는 방법을](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)합니다.

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>그룹에 보안 메커니즘으로 사용 하지 마십시오

그룹은 관련된 사용자가 수집 하는 편리한 방법을 있지만 중요 한 정보에 대 한 액세스를 제한 하는 보안 메커니즘 되지는 않습니다. 사용자가 자동으로 다시 가입할 수 그룹 다시 연결 하는 동안 때 특히 유용 합니다. 대신, 권한이 있는 사용자 역할에 추가 하 고 해당 역할의 구성원만 하는 허브 메서드에 대 한 액세스 제한 것이 좋습니다. 역할에 따라 액세스를 제한의 예제를 보려면 [인증 및 권한 부여 SignalR 허브에 대 한](hub-authorization.md)합니다. 그룹에 대 한 사용자 액세스를 확인 하 여 다시 연결 될 때 예제를 보려면 [그룹 작업](../guide-to-the-api/working-with-groups.md)합니다.

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>클라이언트의 입력을 안전 하 게 처리

악의적인 사용자는 다른 사용자에 게 스크립트를 전송 하지 않습니다을 보장 하려면 다른 클라이언트에는 브로드캐스트를 위한 클라이언트의 모든 입력을 인코딩해야 합니다. SignalR 응용 프로그램에 다양 한 유형의 클라이언트 있을 수 있으므로 서버를 보다는 받는 클라이언트에 메시지를 인코딩해야 합니다. 따라서 HTML 인코딩 웹 클라이언트에 대 한 작동 하지만 작동 다른 종류의 클라이언트에 대 한 없습니다. 예를 들어 채팅 메시지를 표시 하는 웹 클라이언트 메서드 안전 하 게 처리 하는 것은 사용자 이름 및 메시지를 호출 하 여는 `html()` 함수입니다.

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>사용자 상태 활성 연결의 변경 내용 조정

사용자의 인증 상태에 대 한 활성 연결이 있는 동안 변경 되 면 사용자는 내용의 오류가 표시 됩니다, 그리고 "사용자 id를 활성 SignalR 연결 중 변경할 수 없습니다." 이 경우 응용 프로그램 연결 id와 사용자 이름이 조정 되는지 확인 하는 서버에 다시 연결 해야 합니다. 예를 들어 응용 프로그램에 사용자를 로그 아웃 한 활성 연결이 있는 동안 허용 하는 경우 연결에 대 한 사용자 이름에 다음 요청에 전달 되는 이름과 일치 더 이상 합니다. 사용자가 로그 아웃 전에 연결을 중지 하려면 쿼리하고 다시 시작 합니다.

그러나 되기에 대부분의 응용 프로그램 수동으로 중지 하 고 연결을 시작 하지 않아도 됩니다. 응용 프로그램을 별도 페이지에서 사용자를 리디렉션하는 Web Forms 응용 프로그램 또는 MVC 응용 프로그램의 기본 동작 등으로 로그인 한 후 로그 아웃 한 후 현재 페이지를 새로 고칠 경우 활성 연결이 자동으로 끊기고 하지 않습니다. 별도 작업이 필요 합니다.

다음 예제에서는 중지 하 고 사용자 상태 변경 될 때 연결을 시작 하는 방법을 보여 줍니다.

[!code-html[Main](introduction-to-security/samples/sample3.html)]

또는 사이트 슬라이딩 만료를 사용 하 여 폼 인증을 유효한 인증 쿠키를 유지 하려면 활동이 없을 경우 사용자의 인증 상태가 변경 될 수 있습니다. 이 경우 사용자를 로그 아웃 됩니다 및 사용자 이름이 더 이상 일치 하지 연결 토큰에서 사용자 이름입니다. 유효한 인증 쿠키를 유지 하려면 웹 서버에서 리소스를 정기적으로 요청 하는 몇 가지 스크립트를 추가 하 여이 문제를 해결할 수 있습니다. 다음 예제에서는 30 분 마다 리소스를 요청 하는 방법을 보여 줍니다.

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>자동으로 생성 된 JavaScript 프록시 파일

각 사용자에 대 한 JavaScript 프록시 파일의 모든 허브 및 메서드를 포함 하지 않을 경우에 파일의 자동 생성을 비활성화할 수 있습니다. 허브 및 메서드를 여러 개 있어야 하지만 모든 메서드의 알아두어야 하는 모든 사용자를 원하지 않는 경우이 옵션을 선택할 수 있습니다. 자동 생성을 사용 하지 않도록 설정 하 여 **EnableJavaScriptProxies** 를 **false**합니다.

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

JavaScript 프록시 파일에 대 한 자세한 내용은 참조 [생성 된 프록시 및 수에 대 한 역할](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)합니다. <a id="exceptions"></a>

### <a name="exceptions"></a>예외

개체가 중요 한 정보는 클라이언트에 노출 될 수 있습니다 때문에 클라이언트에 예외 개체를 전달 하면 안 됩니다. 대신, 관련 된 오류 메시지를 표시 하는 클라이언트의 메서드를 호출 합니다.

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
