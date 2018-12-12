---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
title: ASP.NET SignalR 허브 API 가이드-서버 (SignalR 1.x) | Microsoft Docs
author: pfletcher
description: 이 문서에서는 코드 샘플 demonstratin 사용 하 여 버전 1.1에서 SignalR에 대 한 ASP.NET SignalR 허브 API의 서버 쪽 프로그래밍 소개를 제공 하는 중...
ms.author: riande
ms.date: 04/17/2013
ms.assetid: 03e4b9f5-0fea-4d94-959f-014b2762a301
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: a51a2077e0b6cde80bc679e3a310c0c804d19d68
ms.sourcegitcommit: 74e3be25ea37b5fc8b4b433b0b872547b4b99186
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53288029"
---
<a name="aspnet-signalr-hubs-api-guide---server-signalr-1x"></a>ASP.NET SignalR 허브 API 가이드-서버 (SignalR 1.x)
====================
하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 일반 옵션을 보여 주는 코드 샘플을 사용 하 여 서버 쪽 ASP.NET SignalR 허브 API의 버전 1.1에서 SignalR에 대 한 프로그래밍을 소개 합니다.
> 
> SignalR 허브 API를 사용 하면 클라이언트가 서버에 연결 된 클라이언트에는 서버에서 원격 프로시저 호출 (Rpc)을 만들 수 있습니다. 서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다. 클라이언트 코드에서 서버에서 호출할 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다. SignalR은 모든 클라이언트-서버 연결 구조를 처리합니다.
> 
> 또한 SignalR 영구 연결을 호출 하는 하위 수준 API를 제공 합니다. SignalR에서 허브 및 영구 연결에 대 한 소개, 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서에 대 한 참조 [SignalR-Getting Started](index.md)합니다.


## <a name="overview"></a>개요

이 문서는 다음 섹션으로 구성됩니다.

- [SignalR 경로 등록 하 고 SignalR 옵션을 구성 하는 방법](#route)

    - [/Signalr URL](#signalrurl)
    - [SignalR 옵션 구성](#options)
- [만들고 허브 클래스를 사용 하는 방법](#hubclass)

    - [허브 개체 수명](#transience)
    - [카멜식 대 / JavaScript 클라이언트에 허브 이름](#hubnames)
    - [여러 허브](#multiplehubs)
- [클라이언트에서 호출할 수 있는 허브 클래스에 메서드를 정의 하는 방법](#hubmethods)

    - [JavaScript 클라이언트에서 메서드 이름의 카멜식 대 / 소문자](#methodnames)
    - [비동기적으로 실행 하는 경우](#asyncmethods)
    - [오버 로드를 정의합니다.](#overloads)
- [허브 클래스에서 클라이언트 메서드를 호출 하는 방법](#callfromhub)

    - [RPC를 수신할 클라이언트를 선택 합니다.](#selectingclients)
    - [메서드 이름에 대 한 컴파일 시간 유효성 검사 없음](#dynamicmethodnames)
    - [대/소문자 메서드 이름 일치](#caseinsensitive)
    - [비동기 실행](#asyncclient)
- [허브 클래스에서 그룹 멤버 자격을 관리 하는 방법](#groupsfromhub)

    - [비동기 실행의 Add 및 Remove 메서드](#asyncgroupmethods)
    - [그룹 멤버 자격 지 속성](#grouppersistence)
    - [단일 사용자 그룹](#singleusergroups)
- [허브 클래스에서 연결 수명 이벤트를 처리 하는 방법](#connectionlifetime)

    - [OnConnected, OnDisconnected, 및 OnReconnected 호출 될 때](#onreconnected)
    - [채워지지 호출자 상태](#nocallerstate)
- [컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법](#contextproperty)
- [클라이언트와 허브 클래스 간의 상태를 전달 하는 방법](#passstate)
- [허브 클래스에서 오류를 처리 하는 방법](#handleErrors)
- [클라이언트 메서드를 호출 하 고 허브 클래스 외부에서 그룹을 관리 하는 방법](#callfromoutsidehub)

    - [클라이언트 메서드를 호출합니다.](#callingclientsoutsidehub)
    - [그룹 멤버 자격 관리](#managinggroupsoutsidehub)
- [추적을 사용 하는 방법](#tracing)
- [허브 파이프라인 사용자 지정 하는 방법](#hubpipeline)

프로그램 클라이언트 하는 방법에 대 한 설명서를 다음 리소스를 참조 합니다.

- [SignalR 허브 API 가이드-JavaScript 클라이언트](index.md)
- [SignalR 허브 API 가이드-.NET 클라이언트](index.md)

.NET 4.5 버전의 API는 API 참조 항목에 대 한 링크. .NET 4를 사용 하는 경우 참조 [항목에서는 API의.NET 4 버전](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)합니다.

<a id="route"></a>

## <a name="how-to-register-the-signalr-route-and-configure-signalr-options"></a>SignalR 경로 등록 하 고 SignalR 옵션을 구성 하는 방법

클라이언트가 사용 하 여 허브에 연결 하는 경로 정의 하려면 호출을 [MapHubs](https://msdn.microsoft.com/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) 메서드 시작 하면 응용 프로그램입니다. `MapHubs` [확장 메서드](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) 에 대 한는 `System.Web.Routing.RouteCollection` 클래스입니다. 다음 예제에서 SignalR 허브 경로 정의 하는 방법을 보여 줍니다 합니다 *Global.asax* 파일입니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample1.cs)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample2.cs?highlight=5)]

ASP.NET MVC 응용 프로그램에 SignalR 기능을 추가 하는 경우에 SignalR 경로의 다른 경로 보다 먼저 추가 되었는지 확인 합니다. 자세한 내용은 참조 하세요. [자습서: SignalR 및 MVC 4 시작](index.md)합니다.

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>/Signalr URL

기본적으로 클라이언트가 사용 하 여 허브에 연결 하는 경로 URL은 "/ signalr"입니다. (자동으로 생성된 된 JavaScript 파일에는 "/ signalr 허브" URL 사용 하 여이 URL을 혼동 하지 마세요. 생성 된 프록시에 대 한 자세한 내용은 참조 하세요. [SignalR 허브 API 가이드-JavaScript 클라이언트-생성 된 프록시 및 용도를](index.md).)

SignalR;에 대 한 기본 URL을 사용할 수 없습니다 하는 특수 상황 있을 수 있습니다. 예를 들어 있는 폴더 라는 프로젝트가 *signalr* 이름을 변경 하지 않으려는 및 합니다. 이 경우 다음 예와에서 같이 기본 URL을 변경할 수 있습니다 (대체 "/ signalr" 원하는 URL 사용 하 여 샘플 코드에서).

**URL을 지정 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample3.cs?highlight=1)]

**URL (생성된 된 프록시)를 지정 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample4.js?highlight=1)]

**(없이 생성된 된 프록시) URL을 지정 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample5.js?highlight=1)]

**URL을 지정 하는.NET 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample6.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>SignalR 옵션 구성

오버 로드는 `MapHubs` 메서드를 사용 하는 사용자 지정 URL, 사용자 지정 종속성 확인자를 및 다음 옵션을 지정할 수 있습니다.

- 브라우저 클라이언트에서 도메인 간 호출을 사용 하도록 설정 합니다.

    일반적으로 브라우저에서 페이지를 로드 하는 경우 `http://contoso.com`, SignalR 연결에 동일한 도메인에 `http://contoso.com/signalr`입니다. 경우 페이지가 `http://contoso.com` 에 연결 `http://fabrikam.com/signalr`, 도메인 간 연결입니다. 보안상의 이유로 기본적으로 도메인 간 연결을 사용할 수 있습니다. 자세한 내용은 [ASP.NET SignalR 허브 API 가이드-JavaScript 클라이언트-도메인 간 연결을 설정 하는 방법을](index.md)합니다.
- 자세한 오류 메시지를 사용 합니다.

    오류가 발생 하면 SignalR의 기본 동작 내용에 대 한 세부 정보가 없는 알림 메시지를 클라이언트로 보내는 것입니다. 프로덕션 환경에서는 악의적인 사용자가 응용 프로그램에 대 한 공격의 정보를 사용 하는 일을 할 수 있습니다 클라이언트에 자세한 오류 정보를 보내지 권장 되지 않습니다. 문제를 해결 하려면 자세한 오류 보고를 일시적으로 사용 하도록 설정 하려면이 옵션을 사용할 수 있습니다.
- 자동으로 생성 된 JavaScript 프록시 파일을 사용 하지 않도록 설정 합니다.

    기본적으로 허브 클래스에 대해 프록시를 사용 하 여 JavaScript 파일에 대 한 응답 URL "/ signalr 허브"로 생성 됩니다. JavaScript 프록시를 사용 하지 않으려는 경우,이 파일을 수동으로 생성 하 고 클라이언트에 물리적 파일을 참조 하려는 경우에 프록시 생성을 사용 하지 않도록 설정 하려면이 옵션을 사용할 수 있습니다. 자세한 내용은 [SignalR 허브 API 가이드-JavaScript 클라이언트-SignalR에 대 한 실제 파일을 만드는 방법에는 프록시 생성](index.md)합니다.

다음 예제에서는 SignalR 연결 URL 및 이러한 옵션에 대 한 호출에서 지정 하는 방법의 `MapHubs` 메서드. 사용자 지정 URL을 지정 하려면 대체 "/ signalr"를 사용 하려는 URL 사용 하 여 예제에서입니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample7.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>만들고 허브 클래스를 사용 하는 방법

허브를 만들려면에서 파생 되는 클래스를 만듭니다 [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)합니다. 다음 예제에서는 채팅 응용 프로그램에 대 한 간단한 허브 클래스를 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample8.cs)]

이 예제에서는 연결 된 클라이언트가 호출할 수는 `NewContosoChatMessage` 메서드 및 모든 연결 된 클라이언트에 받은 데이터 브로드캐스트 될 경우.

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>허브 개체 수명

허브 클래스를 인스턴스화할 하지 않거나 서버에서 사용자 고유의 코드에서 해당 메서드를 호출 합니다. SignalR 허브 파이프라인에 의해 수행 됩니다 모든 것입니다. SignalR은 클라이언트를 연결, 연결 해제 또는 서버 메서드를 호출 작업을 수행 하면 같은 허브 작업을 처리 해야 할 때마다 허브 클래스의 새 인스턴스를 만듭니다.

허브 클래스 인스턴스의 임시 이기 때문에 다음에 대 한 메서드 호출에서 상태를 유지 하기 위해 사용할 수 없습니다. 각 시간 서버의 메시지를 받습니다 메서드 호출을 허브 클래스 프로세스의 새 인스턴스를 클라이언트에서. 여러 개의 연결 및 메서드 호출을 통해 상태를 유지 하려면 허브 클래스에서 파생 되지 않은 다른 클래스에는 데이터베이스 또는 정적 변수와 같은 일부 다른 메서드를 사용 `Hub`합니다. 메모리에서 데이터를 유지 하는 경우 허브 클래스에서 정적 변수와 같은 메서드를 사용 하 여 데이터 손실 됩니다 응용 프로그램 도메인 재활용 하는 경우.

허브 클래스 외부에서 실행 되는 사용자 고유의 코드에서 클라이언트로 메시지를 보내려는 경우 허브 클래스 인스턴스를 인스턴스화하여 그럴 수 없습니다 있지만 허브 클래스에 대 한 SignalR 컨텍스트 개체에 대 한 참조를 가져와서 수행할 수 있습니다. 자세한 내용은 [클라이언트 메서드를 호출 하 여 허브 클래스 외부에서 그룹을 관리 하는 방법을](#callfromoutsidehub) 이 항목의에서 뒷부분에 있습니다.

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>카멜식 대 / JavaScript 클라이언트에 허브 이름

기본적으로 JavaScript 클라이언트는 클래스 이름의 카멜식 대 / 소문자 버전을 사용 하 여 허브를 참조 합니다. SignalR 자동으로이 변경 되므로 JavaScript 코드는 JavaScript 규칙을 따를 수 있습니다. 앞의 예제로 간주 됩니다 `contosoChatHub` JavaScript 코드에서입니다.

**서버**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample9.cs?highlight=1)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample10.js?highlight=1)]

추가 사용 하는 클라이언트에 대 한 다른 이름을 지정 하려는 경우는 `HubName` 특성입니다. 사용 하는 경우는 `HubName` 특성는 JavaScript 클라이언트에서 카멜식 대 / 소문자 이름 변경 되지 않았습니다.

**서버**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample11.cs?highlight=1)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample12.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>여러 허브

응용 프로그램에서 여러 허브 클래스를 정의할 수 있습니다. 이렇게 하면 연결 공유 되지만 그룹은 별도:

- 모든 클라이언트가 동일한 URL을 사용 하 여 서비스를 사용 하 여 SignalR 연결 ("/ signalr" 또는 하나를 지정한 경우 사용자 지정 URL), 모든 허브에 대 한 연결을 사용 하 고 서비스에 의해 정의 됩니다.

    단일 클래스에서 정의 하는 모든 허브 기능에 비해 여러 허브에 대 한 성능 차이가 없습니다.
- 모든 허브에는 동일한 HTTP 요청 정보를 가져옵니다.

    같은 연결을 공유 하는 모든 허브에 서버를 가져오는 유일한 HTTP 요청 정보 이므로 SignalR 연결을 설정 하는 원래 HTTP 요청에 무엇이. 쿼리 문자열을 지정 하 여 클라이언트에서 서버로 정보를 전달 하는 연결 요청을 사용 하는 경우 쿼리 문자열이 서로 다른 여러 허브를 제공할 수 없습니다. 모든 허브에는 동일한 정보를 받게 됩니다.
- 생성된 된 JavaScript 프록시 파일에는 하나의 파일에 모든 허브에 대 한 프록시 포함 됩니다.

    JavaScript 프록시에 대 한 정보를 참조 하세요 [SignalR 허브 API 가이드-JavaScript 클라이언트-생성 된 프록시 및 용도를](index.md)입니다.
- 그룹 허브 내에서 정의 됩니다.

    SignalR을 정의할 수 있습니다 그룹에 브로드캐스트하는 연결 된 클라이언트의 하위 집합 이름이입니다. 그룹은 각 허브에 대해 개별적으로 유지 됩니다. 예를 들어, "Administrators" 라는 그룹을 하나의 집합에 대 한 클라이언트는 사용자 `ContosoChatHub` 클래스 및 그룹 이름이 같은 다양 한 클라이언트에 대 한 참조는 프로그램 `StockTickerHub` 클래스입니다.

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>클라이언트에서 호출할 수 있는 허브 클래스에 메서드를 정의 하는 방법

클라이언트에서 호출할 수 있는 허브의 메서드를 노출 하려면 다음 예제와 같이 공용 메서드를 선언 합니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample14.cs?highlight=3)]

일반적인 C# 메서드와 마찬가지로 복합 형식 및 배열 등을 사용해서 반환 형식과 매개 변수를 지정할 수 있습니다. 매개 변수에서 받거나 호출자에 게 반환 하는 모든 데이터는 JSON을 사용 하 여 클라이언트와 서버 간에 전송 되 고 자동으로 SignalR 처리 복잡 한 개체의 바인딩 및 개체의 배열 합니다.

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>JavaScript 클라이언트에서 메서드 이름의 카멜식 대 / 소문자

기본적으로 JavaScript 클라이언트 허브 메서드를 메서드 이름의 카멜식 대 / 소문자 버전을 사용 하 여 참조 합니다. SignalR 자동으로이 변경 되므로 JavaScript 코드는 JavaScript 규칙을 따를 수 있습니다.

**서버**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample16.js?highlight=1)]

추가 사용 하는 클라이언트에 대 한 다른 이름을 지정 하려는 경우는 `HubMethodName` 특성입니다.

**서버**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>비동기적으로 실행 하는 경우

메서드는 수 장기 실행 또는 작업을 수행 해야 하는 경우에 대기 데이터베이스를 검색 하는 웹 서비스 호출 등을 포함를 반환 하 여 허브 메서드를 비동기화 하는 한 [태스크](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (대신 `void` 반환) 또는 [ 태스크&lt;T&gt; ](https://msdn.microsoft.com/library/dd321424.aspx) 개체 (대신 `T` 반환 형식). 반환 하는 경우는 `Task` SignalR 메서드에서 개체에 대 한 대기를 `Task` 를 완료 하려면 다음 보냅니다 래핑되지 않은 결과 클라이언트로 다시 이므로 클라이언트에서 메서드 호출을 코드 하는 방법에 차이가 없습니다.

허브 메서드를 만드는 비동기 방지 WebSocket 전송이 사용 하는 경우 연결을 차단 합니다. 허브 메서드를 동기적으로 실행 하 고 WebSocket 전송이 후속 호출에서 동일한 클라이언트 허브 메서드의 허브 메서드 완료 될 때까지 차단 됩니다.

다음 예제와 동일한 방법을 동기적으로 실행 하도록 코딩 또는 버전 중 하나를 호출 하기 위한 작동 하는 JavaScript 클라이언트 코드에서 비동기적으로 수행 합니다.

**동기**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample19.cs)]

**비동기-ASP.NET 4.5**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample21.js)]

ASP.NET 4.5의 비동기 메서드를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오 [ASP.NET MVC 4에서 비동기 메서드를 사용 하 여](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)입니다.

<a id="overloads"></a>

### <a name="defining-overloads"></a>오버 로드를 정의합니다.

메서드에 대 한 오버 로드를 정의 하려는 경우에 각 오버 로드에 매개 변수 수가 달라 야 합니다. 다른 매개 변수 유형을 지정 하 여 오버 로드를 구별 하는 경우 허브 클래스는 컴파일되지만 SignalR service를 오버 로드 중 하나를 호출한 클라이언트 시도 하는 경우 런타임 시 예외를 throw 합니다.

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>허브 클래스에서 클라이언트 메서드를 호출 하는 방법

메서드를 호출할 클라이언트에서 서버를 사용 하 여는 `Clients` 허브 클래스에서 메서드에서는 속성입니다. 다음 예제에서는 호출 하는 서버 코드 `addNewMessageToPage` 연결 된 모든 클라이언트에 JavaScript 클라이언트에서 메서드를 정의 하는 클라이언트 코드입니다.

**서버**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample22.cs?highlight=5)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample23.html?highlight=1)]

클라이언트; 메서드에서 반환 값을 가져올 수 없습니다. 와 같은 구문을 `int x = Clients.All.add(1,1)` 작동 하지 않습니다.

복합 형식 및 배열 매개 변수를 지정할 수 있습니다. 다음 예제에서는 복합 형식을 메서드 매개 변수에 클라이언트에 전달 합니다.

**복잡 한 개체를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample24.cs?highlight=3)]

**복합 개체를 정의 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample25.cs?highlight=1)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample26.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>RPC를 수신할 클라이언트를 선택 합니다.

클라이언트 속성은 반환 된 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) RPC를 수신할 클라이언트를 지정 하기 위한 몇 가지 옵션을 제공 하는 개체:

- 연결 된 모든 클라이언트입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample27.cs)]
- 호출 클라이언트입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample28.cs)]
- 호출 클라이언트를 제외한 모든 클라이언트입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample29.cs)]
- 특정 클라이언트 연결 ID로 식별

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample30.css)]

    이 예제에서는 호출 `addContosoChatMessageToPage` 호출 클라이언트에서 사용 하는 것과 동일한 효과가 및 `Clients.Caller`합니다.
- 연결 된 모든 클라이언트를 제외 하 고 지정 된 클라이언트 연결 ID로 식별

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample31.cs)]
- 지정된 된 그룹에 연결 된 모든 클라이언트입니다.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample32.css)]
- 지정된 된 그룹에 연결 된 모든 클라이언트를 제외 하 고 지정 된 클라이언트 연결 ID로 식별

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample33.cs)]
- 지정된 된 그룹에 연결 된 모든 클라이언트 호출 클라이언트를 제외 합니다.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample34.css)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>메서드 이름에 대 한 컴파일 시간 유효성 검사 없음

지정 하는 메서드 이름에 대 한 컴파일 시간 유효성 검사 나 IntelliSense 즉 동적 개체로 해석 됩니다. 식은 런타임에 평가 됩니다. 메서드 호출이 실행 될 때 메서드가 호출 되도록, SignalR 메서드 이름과 매개 변수 값을 클라이언트에 보내고는 이름과 일치 하는 경우 클라이언트에 메서드 및 매개 변수 값에 전달 됩니다. 일치 하는 메서드가 없는 클라이언트에 있으면 오류가 발생 하지 않습니다. SignalR 클라이언트 메서드를 호출할 때 백그라운드에서 클라이언트로 전송 하는 데이터의 형식에 대 한 정보를 참조 하세요 [SignalR 소개](index.md)합니다.

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>대/소문자 메서드 이름 일치

메서드 이름 일치는 대/소문자 구분 합니다. 예를 들어 `Clients.All.addContosoChatMessageToPage` 서버에서 실행 됩니다 `AddContosoChatMessageToPage`를 `addcontosochatmessagetopage`, 또는 `addContosoChatMessageToPage` 클라이언트에서.

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>비동기 실행

호출 하는 메서드를 비동기적으로 실행 합니다. SignalR 클라이언트에 데이터를 전송 하 여 코드의 다음 줄은 메서드 완료 시 대기 해야 함을 지정 하지 않으면 완료 될 때까지 기다리지 않고 즉시 실행 됩니다 클라이언트 메서드 호출 후 제공 되는 모든 코드입니다. 두 클라이언트 메서드를 순차적으로 실행 하는 방법을 보여 줍니다. 다음 코드 예제를 사용 하 여.NET 4.5에서 작동 하는 코드가, 하나 하나를 사용 하 여.NET 4에서 작동 하는 코드가 있습니다.

**.NET 4.5 예제**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample35.cs?highlight=1,3)]

**.NET 4 예제**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample36.cs?highlight=3-4)]

사용 하는 경우 `await` 또는 `ContinueWith` 클라이언트 메서드 코드의 다음 줄을 실행 하기 전에 완료 될 때까지 대기할 의미는 아닙니다 클라이언트 코드의 다음 줄이 실행 되기 전에 메시지가 표시 실제로 됩니다. 클라이언트 메서드 호출의 "완료"는 SignalR 모든 작업을 완료 메시지를 보내는 데 필요한 것을 의미할 뿐입니다. 클라이언트 메시지를 수신 했다고 확인을 할 경우이 메커니즘을 직접 프로그래밍 해야 합니다. 예를 들어, 코딩할 수는 `MessageReceived` 허브 및 메서드를 `addContosoChatMessageToPage` 메서드를 호출할 수 있습니다 클라이언트 `MessageReceived` 작업을 수행한 후 클라이언트에서 수행 해야 하면 작업 합니다. `MessageReceived` 허브에서 할 수 있는 실제 클라이언트 수신 및 처리 원래 메서드 호출의 모든 작업에 따라 달라 집니다.

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>메서드 이름으로 문자열 변수를 사용 하는 방법

캐스팅 메서드 이름으로 문자열 변수를 사용 하 여 클라이언트 메서드를 호출 하려는 경우 `Clients.All` (또는 `Clients.Others`를 `Clients.Caller`등)에 `IClientProxy` 호출 [(methodName, args...) 호출 ](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample37.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>허브 클래스에서 그룹 멤버 자격을 관리 하는 방법

SignalR에서 그룹에 연결 된 클라이언트의 지정 된 하위 집합에 메시지 브로드캐스트 하는 방법을 제공합니다. 그룹의 클라이언트에서 모든 수 있고 클라이언트가 여러 그룹의 멤버일 수 있습니다.

그룹 멤버 자격을 관리 하려면 사용 합니다 [추가](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 및 [제거](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) 에서 제공 하는 메서드는 `Groups` 허브 클래스의 속성입니다. 다음 예제에서는 합니다 `Groups.Add` 및 `Groups.Remove` 호출 하는 JavaScript 클라이언트 코드 뒤에 클라이언트 코드에서 호출 되는 허브 메서드에서 사용 되는 메서드.

**서버**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample38.cs?highlight=5,10)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample39.js)]

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample40.js)]

명시적으로 그룹을 만들 필요가 없습니다. 그룹을 처음에 대 한 호출에 해당 이름을 지정 하는 자동으로 생성 하는 적용 `Groups.Add`, 마지막 연결에 대 한 멤버 자격에서 제거할 때 삭제 됩니다.

그룹 멤버 자격 목록 또는 그룹 목록을 가져오기 위한 API는 없습니다. SignalR 클라이언트와 그룹을 기반으로 메시지를 보냅니다는 [pub/sub 모델](http://en.wikipedia.org/wiki/Publish/subscribe), 서버 그룹 또는 그룹 멤버 자격 목록이 유지 되지 않습니다. 이렇게 하면 확장성을 최대화 하기 때문에 웹 팜에 노드를 추가할 때마다 SignalR 유지 관리 하는 모든 상태를 새 노드에 전파 합니다.

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>비동기 실행의 Add 및 Remove 메서드

합니다 `Groups.Add` 고 `Groups.Remove` 메서드가 비동기적으로 실행 합니다. 있는지 확인 해야 하는 그룹에 클라이언트를 추가 하 고 즉시 그룹을 사용 하 여 클라이언트에 메시지를 송신 하려는 경우는 `Groups.Add` 메서드는 먼저 완료 합니다. 다음 코드 예제에서는 그렇게 하는 방법,.NET 4.5 및.NET 4에서 작동 하는 코드를 사용 하 여 작동 하는 코드를 사용 하 여 하나를 보여 줍니다.

**.NET 4.5 예제**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

**.NET 4 예제**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample42.cs?highlight=3-4)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>그룹 멤버 자격 지 속성

SignalR 연결을 추적, 사용자 수 있도록 하려면 동일한 그룹에 사용자 설정 될 때마다 연결 하려는 사용자가 아닌 경우에 따라서, 호출 해야 `Groups.Add` 될 때마다 사용자는 새 연결을 설정 합니다.

연결 손실로 임시 후 때때로 SignalR 복원할 수 연결이 자동으로. 이런 경우 SignalR은 동일한 연결을 새 연결을 설정 하지 복원과 하므로 클라이언트의 그룹 멤버 자격 자동으로 복원 됩니다. 왜냐하면 가능한 임시 중단 서버를 다시 부팅 또는 실패의 결과가 하는 경우에 그룹 멤버 자격을 포함 하 여 각 클라이언트에 대 한 연결 상태를 클라이언트로 라운드트립 됩니다. 서버 다운 하 고 새 서버 연결 시간이 초과 되기 전에 바뀝니다, 클라이언트 새 서버에 자동으로 다시 연결 하 고 그룹의 멤버인에 다시 등록 수 있습니다.

연결의 연결 손실 후 자동으로 복원할 수 없는 경우 연결 시간이 종료 될 때 또는 클라이언트의 연결을 끊습니다 (예를 들어 경우 브라우저를 새 페이지로 이동) 하는 경우, 그룹 멤버 자격 손실 됩니다. 다음에 사용자 연결에 대 한 새 연결 됩니다. 파일을 동일한 사용자는 새 연결을 설정 하는 경우 그룹 멤버 자격을 유지 하려면 응용 프로그램에 사용자와 그룹 간의 연결을 추적 하 고 될 때마다 새 연결을 설정 하는 사용자 그룹 멤버 자격을 복원 합니다.

연결 및 다시 연결 하는 방법에 대 한 자세한 내용은 참조 하세요. [허브 클래스에서 연결 수명 이벤트를 처리 하는 방법을](#connectionlifetime) 이 항목의에서 뒷부분에 있습니다.

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>단일 사용자 그룹

SignalR을 일반적으로 사용 하는 응용 프로그램 사용자 메시지를 전송한 및 사용자는 메시지를 받을 수 해야 확인 하기 위해 사용자와 연결 간 연결을 추적할 수 있습니다. 그룹 작업을 수행 하는 일반적으로 사용 되는 두 가지 패턴 중 하나에 사용 됩니다.

- 단일 사용자 그룹입니다.

    그룹 이름으로 사용자 이름을 지정 하 고 사용자 연결 되거나 다시 연결 될 때마다 현재 연결 ID를 그룹에 추가할 수 있습니다. 사용자에 게 메시지를 보내도록 그룹에 보냅니다. 이 방법의 단점은 그룹 기능은 제공 되지 않습니다 사용자 온라인 또는 오프 라인 인지 확인 하는 방법입니다.
- 사용자 이름 및 연결 Id 간의 연결을 추적 합니다.

    사전 또는 데이터베이스에서 각 사용자 이름 및 하나 이상의 연결 Id 간의 연결을 저장 하 고 사용자 연결 또는 연결 해제 될 때마다 저장된 된 데이터를 업데이트할 수 있습니다. 사용자에 게 메시지를 보낼 연결 Id를 지정할 수 있습니다. 이 방법의 단점은 더 많은 메모리는입니다.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>허브 클래스에서 연결 수명 이벤트를 처리 하는 방법

연결 수명 이벤트를 처리 하는 것에 대 한 일반적인 이유는 여부는 사용자가 연결 되어 있는지 여부를 추적 하 고 사용자 이름 및 연결 Id 간의 연결을 추적 하는입니다. 클라이언트 연결 하거나 연결을 끊을 때 사용자 고유의 코드를 실행 하려면 재정의 `OnConnected`, `OnDisconnected`, 및 `OnReconnected` 다음 예제에서와 같이 허브의 가상 메서드 클래스입니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample43.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>OnConnected, OnDisconnected, 및 OnReconnected 호출 될 때

브라우저는 새 페이지를 이동할 때마다 새 연결에 설정 되어야 즉, SignalR 실행될지를 `OnDisconnected` 메서드를 호출한는 `OnConnected` 메서드. SignalR 새 연결이 설정 될 때 항상 새 연결 ID를 만듭니다.

`OnReconnected` 경우 케이블을는 일시적으로 연결이 끊어지고 연결 시간이 초과 되기 전에 다시 연결 등에서 SignalR 수 자동으로 복구 하는 연결에서 임시 중단 되었을 때 메서드가 호출 됩니다. `OnDisconnected` 메서드는 클라이언트는 연결이 끊어집니다 및 SignalR 자동으로 다시 연결할 수 없습니다, 브라우저를 새 페이지로 이동 하는 경우와 같은 때 호출 됩니다. 따라서 가능한 지정된 된 클라이언트에 대 한 이벤트 시퀀스가 `OnConnected`, `OnReconnected`를 `OnDisconnected`; 또는 `OnConnected`, `OnDisconnected`합니다. 시퀀스를 표시 하지 않습니다 `OnConnected`, `OnDisconnected`, `OnReconnected` 지정된 된 연결에 대 한 합니다.

`OnDisconnected` 메서드 서버가 중단 등의 일부 시나리오에서 호출 하지 않습니다 또는 응용 프로그램 도메인 재활용을 가져옵니다. 일부 클라이언트를 다시 연결 하 고 실행 하는 일을 할 수 있습니다 다른 서버가 온라인 상태가 또는 응용 프로그램 도메인의 재생을 완료 하는 경우는 `OnReconnected` 이벤트입니다.

자세한 내용은 [이해 및 SignalR의 연결 수명 이벤트 처리](index.md)합니다.

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>채워지지 호출자 상태

즉에 삽입 하는 모든 상태는 서버에서 연결 수명 이벤트 처리기 메서드를 호출 되는 `state` 클라이언트 개체에서 채워지지 것입니다을 `Caller` 서버의 속성. 에 대 한 자세한 합니다 `state` 개체 및 `Caller` 속성을 참조 하세요 [클라이언트와 허브 클래스 간의 상태를 전달 하는 방법을](#passstate) 이 항목의 뒷부분에 나오는.

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법

클라이언트에 대 한 정보를 가져오려면는 `Context` 허브 클래스의 속성입니다. 합니다 `Context` 속성에서 반환 된 [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) 다음 정보에 대 한 액세스를 제공 하는 개체:

- 호출 클라이언트의 연결 ID입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample44.cs?highlight=1)]

    연결 ID는 SignalR (사용자 고유의 코드에서 값을 지정할 수 없습니다.)가 할당 하는 GUID입니다. 각 연결과 동일한 연결 응용 프로그램에서 여러 허브를 설정한 경우 모든 허브에서 ID를 사용 하는 것에 대 한 연결 ID를 하나 있습니다.
- HTTP 헤더 데이터입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample45.cs?highlight=1)]

    HTTP 헤더를 가져올 수도 있습니다 `Context.Headers`합니다. 동일한 작업에 대 한 여러 참조에 대 한 이유는 `Context.Headers` 먼저 만들어진 합니다 `Context.Request` 속성은 나중에 추가 되었습니다 및 `Context.Headers` 이전 버전과 호환성을 위해 유지 되었습니다.
- 문자열 데이터를 쿼리 합니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample46.cs?highlight=1)]

    쿼리 문자열 데이터를 가져올 수도 있습니다 `Context.QueryString`합니다.

    이 속성에서 수행 되는 쿼리 문자열은 SignalR 연결을 설정 하는 HTTP 요청에 사용 된 것입니다. 서버에 클라이언트에서 클라이언트에 대 한 데이터를 전달 하는 편리한 방법에 따라 연결을 구성 하 여 클라이언트에서 쿼리 문자열 매개 변수를 추가할 수 있습니다. 다음 예제에서는 생성 된 프록시를 사용 하는 경우 JavaScript 클라이언트에서 쿼리 문자열을 추가 하는 한 가지 방법은 보여 줍니다.

    [!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample47.js?highlight=1)]

    쿼리 문자열 매개 변수를 설정 하는 방법에 대 한 자세한 내용은 API 설명서를 참조 합니다 [JavaScript](index.md) 하 고 [.NET](index.md) 클라이언트입니다.

    SignalR에서 내부적으로 사용 하는 몇 가지 다른 값과 함께 쿼리 문자열 데이터를 연결에 사용 되는 전송 메서드를 찾을 수 있습니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample48.cs)]

    변수의 `transportMethod` "Websocket", "serverSentEvents", "foreverFrame" 또는 "longPolling" 됩니다. 이 값을 확인 하는 경우는 `OnConnected` 이벤트 처리기 메서드를 일부 시나리오에서 발생할 수 있습니다 처음에 연결에 대 한 최종 협상 된 전송 메서드 없는 전송 값입니다. 이 경우 메서드는 예외가 throw 됩니다 하 고 최종 전송을 설정 되 면 나중에 다시 호출 됩니다.
- 쿠키입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    쿠키를 가져올 수도 있습니다 `Context.RequestCookies`합니다.
- 사용자 정보입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample50.cs?highlight=1)]
- 요청에 대 한 HttpContext 개체:

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample51.cs?highlight=1)]

    이 메서드를 사용 하 여 시작 하는 대신 `HttpContext.Current` 가져오려고 합니다 `HttpContext` SignalR 연결에 대 한 개체입니다.

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>클라이언트와 허브 클래스 간의 상태를 전달 하는 방법

클라이언트 프록시는 제공 된 `state` 개체는 각 메서드 호출을 사용 하 여 서버에 전송 하려는 데이터를 저장할 수 있습니다. 서버에서이 데이터에 액세스할 수는 `Clients.Caller` 허브 메서드에서 클라이언트에서 호출 되는 속성입니다. 합니다 `Clients.Caller` 연결 수명 이벤트 처리기 메서드에 대 한 속성은 채워지지 않습니다 `OnConnected`를 `OnDisconnected`, 및 `OnReconnected`합니다.

만들거나의 데이터를 업데이트 합니다 `state` 개체 및 `Clients.Caller` 속성이 두 방향 모두에서 작동 합니다. 서버에서 값을 업데이트할 수 있습니다 하 고 클라이언트에 다시 전달 됩니다.

다음 예제에서는 모든 메서드 호출을 사용 하 여 서버에 전송에 대 한 상태를 저장 하는 JavaScript 클라이언트 코드를 보여 줍니다.

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample52.js?highlight=1-2)]

다음 예제에서는.NET 클라이언트에서 해당 하는 코드를 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample53.cs?highlight=1-2)]

허브 클래스에서이 데이터에 액세스할 수 있습니다는 `Clients.Caller` 속성입니다. 다음 예제에서는 이전 예제에서 참조 하는 상태를 검색 하는 코드를 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample54.cs?highlight=3-4)]

> [!NOTE]
> 지속 상태에 대 한이 메커니즘을 사용할 수 없습니다 많은 양의 데이터에 넣으면 모든 이후 합니다 `state` 또는 `Clients.Caller` 속성은 모든 메서드 호출을 사용 하 여 라운드트립 합니다. 사용자 이름이 나 카운터 같은 더 작은 항목에 대 한 두는 것이 유용합니다.


<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>허브 클래스에서 오류를 처리 하는 방법

허브 클래스 메서드에서 발생 하는 오류를 처리 하려면 다음 방법 중 하나 또는 모두를 사용 합니다.

- Try / catch 블록에서 메서드 코드를 래핑하고 예외 개체를 기록 합니다. 디버깅 목적으로 클라이언트에 예외를 보낼 수 있지만 보안상의 이유로 프로덕션의 클라이언트에 자세한 정보를 보내는 권장 되지 않습니다.
- 처리 하는 허브 파이프라인 모듈을 만들어야 합니다 [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) 메서드. 다음 예제에서는 global.asax 허브 파이프라인에 모듈을 삽입 하는 코드 뒤에 오류를 기록 하는 파이프라인 모듈을 보여 줍니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample55.cs)]

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample56.cs?highlight=3)]

Hub 파이프라인 모듈에 대 한 자세한 내용은 참조 하세요. [Hubs 파이프라인 사용자 지정 하는 방법을](#hubpipeline) 이 항목의에서 뒷부분에 있습니다.

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>추적을 사용 하는 방법

서버 쪽 추적을 사용 하려면이 예와 같이 system.diagnostics 요소를 Web.config 파일을 추가 합니다.

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample57.html?highlight=17-72)]

Visual Studio에서 응용 프로그램을 실행 하는 경우 로그를 볼 수 있습니다 합니다 **출력** 창입니다.

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>클라이언트 메서드를 호출 하 고 허브 클래스 외부에서 그룹을 관리 하는 방법

메서드를 호출할 클라이언트 허브 클래스와는 다른 클래스에서 허브에 대 한 SignalR 컨텍스트 개체에 대 한 참조를 가져와 클라이언트에서 메서드를 호출 하거나 그룹을 관리 하는 사용 합니다.

다음 샘플 `StockTicker` 클래스는 컨텍스트 개체를 가져옵니다, 클래스의 인스턴스에 저장, 클래스 인스턴스는 정적 속성에 저장 및 singleton 클래스 인스턴스에서 컨텍스트를 사용 하 여 호출 하 여 `updateStockPrice` 메서드는 클라이언트에서 명명 된 허브에 연결 `StockTickerHub`합니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample58.cs?highlight=8,24)]

수명이 긴 개체에서 상황에 맞는 여러 번 사용 하는 경우 참조를 한 번 가져와 저장 될 때마다 다시 것 보다는 해당 합니다. 컨텍스트를 한 번 시작 하면 SignalR 순서는 허브 메서드 확인 클라이언트 메서드 호출의 클라이언트에 메시지를 보냅니다. 허브에 대해 SignalR 컨텍스트를 사용 하는 방법을 보여 주는 자습서를 참조 하세요 [ASP.NET SignalR을 사용 하 여 서버 브로드캐스트](index.md)합니다.

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>클라이언트 메서드를 호출합니다.

클라이언트 RPC를 받을 지정할 수 있지만 허브 클래스에서 호출 하는 경우 보다 더 적은 옵션이 있습니다. 이러한 이유로 없다는 컨텍스트 클라이언트에서 특정 호출과 관련 된 모든 메서드는 필요 현재 연결 ID의 기술 자료와 같은 `Clients.Others`, 또는 `Clients.Caller`, 또는 `Clients.OthersInGroup`를 사용할 수 없습니다. 다음 옵션을 사용할 수 있습니다.

- 연결 된 모든 클라이언트입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample59.cs)]
- 특정 클라이언트 연결 ID로 식별

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample60.css)]
- 연결 된 모든 클라이언트를 제외 하 고 지정 된 클라이언트 연결 ID로 식별

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample61.cs)]
- 지정된 된 그룹에 연결 된 모든 클라이언트입니다.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample62.css)]
- 연결 ID로 식별 하는 지정 된 클라이언트를 제외한 지정된 된 그룹의 모든 연결 된 클라이언트

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample63.cs)]

현재 연결 ID를 전달 하 고 사용 하 여 사용 하 여 호출 하는 경우 비-허브 클래스에 메서드에서 허브 클래스에서를 `Clients.Client`, `Clients.AllExcept`, 또는 `Clients.Group` 시뮬레이션 `Clients.Caller`, `Clients.Others`, 또는 `Clients.OthersInGroup`합니다. 다음 예제에서는 `MoveShapeHub` 연결 ID를 전달 하는 클래스를 `Broadcaster` 클래스 있도록를 `Broadcaster` 클래스를 시뮬레이션할 수 있습니다 `Clients.Others`.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample64.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>그룹 멤버 자격 관리

그룹 관리를 위한 허브 클래스에서와 마찬가지로 동일한 옵션 있는 합니다.

- 클라이언트 그룹에 추가

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample65.cs)]
- 그룹에서 클라이언트 제거

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample66.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>허브 파이프라인 사용자 지정 하는 방법

SignalR을 사용 하면 허브 파이프라인에 사용자 고유의 코드를 삽입할 수 있습니다. 다음 예제에서는 클라이언트와 클라이언트에서 보내는 메서드 호출에서 받은 각 들어오는 메서드 호출을 기록 하는 사용자 지정 허브 파이프라인 모듈을 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample67.cs)]

다음 코드를 *Global.asax* 허브 파이프라인에서 실행 하려면 모듈을 등록 하는 파일:

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample68.cs?highlight=3)]

재정의할 수 있는 여러 가지 방법 이며 전체 목록을 참조 하세요 [HubPipelineModule 메서드](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)합니다.
