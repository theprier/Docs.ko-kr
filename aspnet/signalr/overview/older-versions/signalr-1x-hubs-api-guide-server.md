---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
title: "ASP.NET SignalR 허브 API 가이드-서버 (SignalR 1.x) | Microsoft Docs"
author: pfletcher
description: "이 문서에서는 코드 샘플 demonstratin와 버전 1.1에서 SignalR에 대 한 ASP.NET SignalR 허브 API의 서버 쪽 프로그래밍에 대 한 소개를 제공..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/17/2013
ms.topic: article
ms.assetid: 03e4b9f5-0fea-4d94-959f-014b2762a301
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: e594dd1ea4ae027cf0b82574fc5a3eb061b1f2e1
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-signalr-hubs-api-guide---server-signalr-1x"></a>ASP.NET SignalR 허브 API 가이드-서버 (SignalR 1.x)
====================
여 [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)

> 이 문서에서는 일반적인 옵션을 보여 주는 샘플 코드 버전 1.1에서 SignalR에 대 한 ASP.NET SignalR 허브 API의 서버 쪽 프로그래밍에 대 한 소개를 제공 합니다.
> 
> SignalR 허브 API를 사용 하면 클라이언트가 서버와 연결 된 클라이언트에는 서버에서 원격 프로시저 호출 (Rpc)을 만들 수 있습니다. 서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다. 클라이언트 코드에서 서버에서 호출 될 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다. SignalR은 클라이언트와 서버 작업을 처리의 모든 담당합니다.
> 
> 또한 SignalR 영구 연결을 호출 하는 하위 수준 API를 제공 합니다. SignalR, 허브 및 영구 연결에 대 한 소개 또는 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서에 대 한 참조 [SignalR-시작](index.md)합니다.


## <a name="overview"></a>개요

이 문서는 다음 섹션으로 구성됩니다.

- [SignalR 경로 등록 하 고 SignalR 옵션을 구성 하는 방법](#route)

    - [/Signalr URL](#signalrurl)
    - [SignalR 옵션 구성](#options)
- [만들고 허브 클래스를 사용 하는 방법](#hubclass)

    - [허브 개체 수명](#transience)
    - [카멜식 대 / 소문자 JavaScript 클라이언트에서 허브 이름](#hubnames)
    - [여러 허브](#multiplehubs)
- [클라이언트에서 호출할 수 있는 허브 클래스에 메서드를 정의 하는 방법](#hubmethods)

    - [JavaScript 클라이언트에서 메서드 이름의 카멜식 대 / 소문자](#methodnames)
    - [비동기적으로 실행 하는 경우](#asyncmethods)
    - [오버 로드를 정의합니다.](#overloads)
- [허브 클래스에서 클라이언트 메서드를 호출 하는 방법](#callfromhub)

    - [클라이언트를 선택 하는 RPC 받습니다.](#selectingclients)
    - [메서드 이름에 대 한 컴파일 시간 유효성](#dynamicmethodnames)
    - [일치 하는 대/소문자 구분 메서드 이름](#caseinsensitive)
    - [비동기 실행](#asyncclient)
- [허브 클래스에서 그룹 구성원 자격을 관리 하는 방법](#groupsfromhub)

    - [Add 및 Remove 메서드의 비동기 실행](#asyncgroupmethods)
    - [그룹 멤버 자격 지 속성](#grouppersistence)
    - [단일 사용자 그룹](#singleusergroups)
- [허브 클래스에서 연결 수명 이벤트를 처리 하는 방법](#connectionlifetime)

    - [OnConnected, OnDisconnected, 및 OnReconnected 호출 될 때](#onreconnected)
    - [채워지지 호출자 상태](#nocallerstate)
- [컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법](#contextproperty)
- [클라이언트와 허브 클래스 간의 상태를 전달 하는 방법](#passstate)
- [허브 클래스에는 오류를 처리 하는 방법](#handleErrors)
- [클라이언트 메서드를 호출할 허브 클래스 외부에서 그룹을 관리 하는 방법](#callfromoutsidehub)

    - [클라이언트 메서드 호출](#callingclientsoutsidehub)
    - [그룹 멤버 자격 관리](#managinggroupsoutsidehub)
- [추적을 사용 하는 방법](#tracing)
- [허브 파이프라인을 사용자 지정 하는 방법](#hubpipeline)

프로그램 클라이언트 하는 방법에 대 한 설명서를 다음 리소스를 참조 하십시오.

- [SignalR 허브 API 가이드-JavaScript 클라이언트](index.md)
- [SignalR 허브 API 가이드-.NET 클라이언트](index.md)

API 참조 항목의 링크를.NET 4.5 버전의 API 되도록합니다. .NET 4를 사용 하 여 참조 [.NET 4 버전의 API 항목](https://msdn.microsoft.com/en-us/library/jj891075(v=vs.100).aspx)합니다.

<a id="route"></a>

## <a name="how-to-register-the-signalr-route-and-configure-signalr-options"></a>SignalR 경로 등록 하 고 SignalR 옵션을 구성 하는 방법

클라이언트에서 허브에 연결 하는 데 사용 하는 경로 정의 하려면 호출는 [MapHubs](https://msdn.microsoft.com/en-us/library/system.web.routing.signalrrouteextensions.maphubs(v=vs.111).aspx) 메서드 응용 프로그램이 시작 합니다. `MapHubs`이 [확장 메서드](https://msdn.microsoft.com/en-us/library/vstudio/bb383977.aspx) 에 대 한는 `System.Web.Routing.RouteCollection` 클래스입니다. 다음 예제에서 SignalR 허브 경로 정의 하는 방법을 보여 줍니다는 *Global.asax* 파일입니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample1.cs)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample2.cs?highlight=5)]

ASP.NET MVC 응용 프로그램에 SignalR 기능을 추가 하는 경우 다른 경로 보다 SignalR 경로 추가 되어 있는지 확인 합니다. 자세한 내용은 참조 [자습서: SignalR 및 MVC 4 시작](index.md)합니다.

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>/Signalr URL

기본적으로 클라이언트에서 허브에 연결 하는 데 사용 하는 경로 URL은 "/ signalr"입니다. (자동으로 생성 된 JavaScript 파일에 "/ signalr/허브" URL로이 URL을 혼동 하지 마십시오. 생성 된 프록시에 대 한 자세한 내용은 참조 [SignalR 허브 API 가이드-JavaScript 클라이언트-생성 된 프록시 및 수에 대 한 역할](index.md).)

SignalR;에 대 한 사용할 수 없음이 기본 URL을 구성 하는 특수 상황 있을 수 있습니다. 예를 들어 이라는 프로젝트에 폴더를 있으면 *signalr* 이름을 변경 하려면. 이 경우 다음 예제에 나와 있는 것 처럼 기본 URL을 변경할 수 있습니다 (대체 "/ signalr" 원하는으로 URL 사용 하 여 샘플 코드에서).

**URL을 지정 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample3.cs?highlight=1)]

**URL (생성 된 프록시)를 지정 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample4.js?highlight=1)]

**(없이 생성 된 프록시) URL을 지정 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample5.js?highlight=1)]

**URL을 지정 하는.NET 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample6.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>SignalR 옵션 구성

오버 로드는 `MapHubs` 메서드를 사용 하는 사용자 지정 URL, 사용자 지정 종속성 확인자, 그리고 다음 옵션을 지정할 수 있습니다.

- 브라우저 클라이언트에서 도메인 간 호출을 사용 하도록 설정 합니다.

    일반적으로 브라우저에서 페이지를 로드 하는 경우 `http://contoso.com`, SignalR 연결에 동일한 도메인에는 `http://contoso.com/signalr`합니다. 경우에서 페이지 `http://contoso.com` 에 대 한 연결을 사용 하면 `http://fabrikam.com/signalr`, 도메인 간 연결입니다. 보안상의 이유로 도메인 간 연결이 기본적으로 비활성화 됩니다. 자세한 내용은 참조 [ASP.NET SignalR 허브 API 가이드-JavaScript 클라이언트-도메인 간 연결을 설정 하는 방법](index.md)합니다.
- 자세한 오류 메시지를 사용 하도록 설정 합니다.

    오류가 발생할 때 무슨 상황이 발생 하는 방법에 대 한 세부 정보가 없는 알림 메시지를 클라이언트에 보내는 데 SignalR의 기본 동작은입니다. 프로덕션, 악의적인 사용자가 응용 프로그램에 대 한 공격에 정보를 사용할 수 있습니다 클라이언트에 자세한 오류 정보를 보내 권장 되지 않습니다. 문제 해결을 위해 일시적으로 더 자세한 오류 보고를 활성화 하려면이 옵션을 사용할 수 있습니다.
- 자동으로 생성 된 JavaScript 프록시 파일을 사용 하지 않도록 설정 합니다.

    기본적으로 허브 클래스에 대 한 프록시와 JavaScript 파일은 "/ signalr/허브" URL에 대 한 응답으로 생성 됩니다. JavaScript 프록시를 사용 하지 않음 또는이 파일을 수동으로 생성 하 고 클라이언트의 물리적 파일을 참조 하려는 경우에 프록시 생성을 해제 하려면이 옵션을 사용할 수 있습니다. 자세한 내용은 참조 [SignalR 허브 API 가이드-JavaScript 클라이언트는 SignalR에 대 한 실제 파일을 만드는 방법에는 프록시 생성](index.md)합니다.

다음 예제에 대 한 호출에서 SignalR 연결 URL 및 이러한 옵션을 지정 하는 방법을 보여 줍니다는 `MapHubs` 메서드. 사용자 지정 URL을 지정 하려면 바꿉니다 "/ signalr"을 사용 하려면 URL로 예제에서입니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample7.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>만들고 허브 클래스를 사용 하는 방법

허브를 만들려면에서 파생 되는 클래스를 만듭니다 [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)합니다. 다음 예제에서는 채팅 응용 프로그램에 대 한 간단한 허브 클래스를 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample8.cs)]

이 예제에서는 연결 된 클라이언트가 호출할 수는 `NewContosoChatMessage` 메서드, 및 연결 된 모든 클라이언트에 수신 된 데이터가 브로드캐스트 될 경우.

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>허브 개체 수명

허브 클래스를 인스턴스화하거나; 서버에서 사용자 고유의 코드에서 해당 메서드를 호출 하지 않습니다. SignalR 허브 파이프라인에 의해 수행 되는 모든. SignalR은 클라이언트를 연결, 연결이 끊어진, 또는 서버에 메서드를 호출 하면 때 같은 허브 작업을 처리 해야 할 때마다 허브 클래스의 새 인스턴스를 만듭니다.

허브 클래스의 인스턴스는 일시적 이므로 다음에 대 한 메서드 호출에서 상태를 유지 하기 위해 사용할 수 없습니다. 될 때마다 서버 메서드 호출은 클라이언트에서 수신, 허브 클래스 프로세스의 새 인스턴스는 메시지입니다. 여러 개의 연결 및 메서드 호출을 통해 상태를 유지 하려면 허브 클래스 또는 다른 클래스에서 파생 되지 않은에 데이터베이스 또는 정적 변수와 같은 다른 방법을 사용 `Hub`합니다. 데이터를 메모리에에서 유지 하는 경우 정적 변수와 같은 메서드를 사용 하 여 허브 클래스에는 데이터는 손실 됩니다 응용 프로그램 도메인을 재활용 하면 합니다.

클라이언트에 허브 클래스 외부에서 실행 되는 사용자 고유의 코드에서 메시지를 전송 하려는 경우 허브 클래스 인스턴스를 인스턴스화하고 그럴 수 없습니다 되지만 허브 클래스에 대 한 SignalR 컨텍스트 개체에 대 한 참조를 가져오는 하 여 수행할 수 있습니다. 자세한 내용은 참조 [클라이언트 메서드를 호출할 허브 클래스 외부에서 그룹을 관리 하는 방법을](#callfromoutsidehub) 이 항목의 뒷부분에 나오는 합니다.

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>카멜식 대 / 소문자 JavaScript 클라이언트에서 허브 이름

기본적으로 JavaScript 클라이언트에 허브 클래스 이름의 카멜식 대/소문자 버전을 사용 하 여 참조 합니다. SignalR 자동으로 이러한 변경 때문 JavaScript 코드는 JavaScript 규칙을 따를 수 있습니다. 앞의 예제로 참조 될 `contosoChatHub` JavaScript 코드에서.

**서버**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample9.cs?highlight=1)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample10.js?highlight=1)]

추가 사용 하려면 클라이언트에 대해 다른 이름을 지정 하려는 경우는 `HubName` 특성입니다. 사용 하는 경우는 `HubName` 특성을 클라이언트 JavaScript에서 카멜식 대/소문자에 이름이 변경 되지 않았습니다.

**서버**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample11.cs?highlight=1)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample12.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>여러 허브

응용 프로그램에서 여러 허브 클래스를 정의할 수 있습니다. 그렇게 하면 연결이 공유 되어 있는 그룹은 별도 보이지만.

- 모든 클라이언트에서 동일한 URL을 사용 하 여 서비스와 SignalR 연결을 설정할 수 ("/ signalr" 또는 하나를 지정한 경우에 사용자 지정 URL), 서비스에 의해 정의 된 모든 허브에 대 한 연결을 사용 합니다.

    단일 클래스에서 정의 하는 모든 허브 기능에 비해 여러 허브에 대 한 성능 차이가 없습니다.
- 모든 허브 동일한 HTTP 요청 정보를 가져옵니다.

    같은 연결을 공유 하는 모든 허브를 유일한 HTTP 요청 정보를 서버 사용량이 이므로 SignalR 연결을 설정 하는 원래 HTTP 요청에 추가 되는 내용입니다. 쿼리 문자열을 지정 하 여 서버에 클라이언트에서 정보를 전달 하려면 연결 요청을 사용 하는 경우 다른 허브에 서로 다른 쿼리 문자열을 제공할 수 없습니다. 모든 허브 동일한 정보를 받게 됩니다.
- 생성 된 JavaScript 프록시 파일에는 하나의 파일에 있는 모든 허브에 대 한 프록시 포함 됩니다.

    JavaScript 프록시에 대 한 정보를 참조 하십시오. [SignalR 허브 API 가이드-JavaScript 클라이언트-생성 된 프록시 및 수에 대 한 역할](index.md)합니다.
- 그룹 허브 내에서 정의 됩니다.

    SignalR을 정의할 수 있습니다 이름이 그룹에 브로드캐스트하는 연결 된 클라이언트의 하위 집합입니다. 각 허브에 대 한 그룹 별도로 유지 관리 됩니다. 예를 들어 "Administrators" 라는 그룹 집합에 대 한 클라이언트 포함 프로그램 `ContosoChatHub` 클래스 이름과 동일한 그룹을 다른 집합에 대 한 클라이언트 참조 프로그램 `StockTickerHub` 클래스.

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>클라이언트에서 호출할 수 있는 허브 클래스에 메서드를 정의 하는 방법

다음 예제에 나와 있는 것 처럼 클라이언트에서 호출할 수를 허브에 대 한 메서드를 노출 하려면 공용 메서드를 선언 합니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample14.cs?highlight=3)]

반환 형식 및 C# 메서드에서 마찬가지로 배열 및 복합 형식을 포함 하 여 매개 변수를 지정할 수 있습니다. 매개 변수에서 수신 하거나 호출자에 게 반환 하는 모든 데이터는 JSON을 사용 하 여 클라이언트와 서버 간에 전송 되 고 자동으로 SignalR 처리 복잡 한 개체의 바인딩 및 개체의 배열을 합니다.

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>JavaScript 클라이언트에서 메서드 이름의 카멜식 대 / 소문자

기본적으로 메서드 이름의 카멜식 대/소문자 버전을 사용 하 여 JavaScript 클라이언트 허브 메서드를 참조 합니다. SignalR 자동으로 이러한 변경 때문 JavaScript 코드는 JavaScript 규칙을 따를 수 있습니다.

**서버**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample16.js?highlight=1)]

추가 사용 하려면 클라이언트에 대해 다른 이름을 지정 하려는 경우는 `HubMethodName` 특성입니다.

**서버**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>비동기적으로 실행 하는 경우

메서드는 될 장기 실행 또는 작업을 수행 해야 하는 경우에 대기 데이터베이스를 조회 하는 웹 서비스 호출 등을 포함를 반환 하 여 허브 메서드를 비동기적으로 만듭니다 하 하는 [작업](https://msdn.microsoft.com/en-us/library/system.threading.tasks.task.aspx) (대신 `void` 반환) 또는 [ 작업&lt;T&gt; ](https://msdn.microsoft.com/en-us/library/dd321424.aspx) 개체 (대신 `T` 반환 형식). 반환 하는 `Task` SignalR 메서드에서 개체에 대 한 대기는 `Task` 를 완료 하 고 전송 합니다 래핑되지 않은 결과 클라이언트에 클라이언트에서 메서드 호출 코드가 방식에 차이점이 하도록 합니다.

허브 메서드를 만드는 비동기 방지 WebSocket 전송 사용 하는 경우 연결을 차단 합니다. 허브 메서드를 동기적으로 실행 하는 경우 전송 WebSocket은 동일한 클라이언트에서 허브에 대 한 메서드는 다음 호출 허브 메서드가 완료 될 때까지 차단 됩니다.

다음 예제와 동일한 방법을 동기적으로 실행 하도록 코드를 작성 또는 비동기적으로 버전 중 하나를 호출 하기 위한 작동 하는 JavaScript 클라이언트 코드와 합니다.

**동기**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample19.cs)]

**비동기-ASP.NET 4.5**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample21.js)]

ASP.NET 4.5에서 비동기 메서드를 사용 하는 방법에 대 한 자세한 내용은 참조 [ASP.NET MVC 4의 비동기 메서드를 사용 하 여](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)합니다.

<a id="overloads"></a>

### <a name="defining-overloads"></a>오버 로드를 정의합니다.

메서드에 대 한 오버 로드를 정의 하려는 경우에 각 오버 로드에 매개 변수 수가 달라 야 합니다. 다른 매개 변수 형식을 지정 하 여 오버 로드를 구분 하는 경우 허브 클래스는 컴파일되지만 SignalR 서비스 오버 로드 중 하나를 호출한 클라이언트 통신을 시도 하면 런타임 시 예외를 throw 합니다.

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>허브 클래스에서 클라이언트 메서드를 호출 하는 방법

메서드를 호출 클라이언트에서 서버를 사용 하 여는 `Clients` 허브 클래스에서 메서드에서는 속성입니다. 다음 예제에서는 호출 하는 서버 코드 `addNewMessageToPage` 연결 된 모든 클라이언트 및 JavaScript 클라이언트에서 메서드를 정의 하는 클라이언트 코드에 있습니다.

**서버**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample22.cs?highlight=5)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample23.html?highlight=1)]

클라이언트 메서드에서 반환 값을 가져올 수 없습니다. 와 같은 구문 `int x = Clients.All.add(1,1)` 작동 하지 않습니다.

복합 형식 및 매개 변수 배열을 지정할 수 있습니다. 다음 예제에서는 메서드 매개 변수에서는 클라이언트에는 복합 유형을 전달합니다.

**복잡 한 개체를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample24.cs?highlight=3)]

**복잡 한 개체를 정의 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample25.cs?highlight=1)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample26.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>클라이언트를 선택 하는 RPC 받습니다.

클라이언트 속성은 반환 된 [HubConnectionContext](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) 클라이언트 RPC 받습니다 지정 하기 위한 몇 가지 옵션을 제공 하는 개체:

- 연결 된 모든 클라이언트입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample27.cs)]
- 호출 클라이언트만 합니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample28.cs)]
- 호출 클라이언트를 제외한 모든 클라이언트입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample29.cs)]
- 특정 클라이언트 연결 ID로 식별

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample30.css)]

    이 예제에서는 호출 `addContosoChatMessageToPage` 호출 클라이언트에 사용 하 여 것과 동일한 결과가 및 `Clients.Caller`합니다.
- 연결 된 모든 클라이언트 연결 ID로 식별 하는 지정 된 클라이언트를 제외한

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample31.cs)]
- 지정된 된 그룹에 연결 된 모든 클라이언트입니다.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample32.css)]
- 지정된 된 그룹의 모든 연결 된 클라이언트 연결 ID로 식별 하는 지정 된 클라이언트를 제외 하

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample33.cs)]
- 지정된 된 그룹의 모든 연결 된 클라이언트 호출 클라이언트를 제외 하 고 있습니다.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample34.css)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>메서드 이름에 대 한 컴파일 시간 유효성

메서드 이름은 지정 하는 의미 없는 IntelliSense 또는 컴파일 타임 유효성 검사에 대 한 동적 개체로 해석 됩니다. 식이 런타임 시 계산 됩니다. 메서드 호출이 실행 하는 경우, 메서드가 호출 되도록 SignalR 메서드 이름과 매개 변수 값을 클라이언트에 보내고의 이름과 일치 하는 클라이언트에서 메서드 및 매개 변수 값에 전달 됩니다. 메서드가 클라이언트에서 발견 되는 경우 오류가 발생 합니다. SignalR 클라이언트 메서드를 호출할 때 내부적 클라이언트에 전송 하는 데이터의 형식에 대 한 정보를 참조 하십시오. [SignalR 소개](index.md)합니다.

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>일치 하는 대/소문자 구분 메서드 이름

메서드 이름 일치는 대/소문자 구분 합니다. 예를 들어 `Clients.All.addContosoChatMessageToPage` 서버에서 실행 됩니다 `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, 또는 `addContosoChatMessageToPage` 클라이언트에서.

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>비동기 실행

호출 하는 메서드를 비동기적으로 실행 합니다. SignalR 클라이언트에 데이터를 전송 하 여 코드의 다음 줄 메서드 완료를 위해 대기 해야를 지정 하지 않으면 완료 될 때까지 기다리지 않고 즉시 실행 됩니다 클라이언트에 메서드 호출 뒤에 오는 모든 코드입니다. 다음 코드 예제는 두 개의 클라이언트 메서드를 순차적으로 실행 하는 방법을 보여 하나를 사용 하 여.NET 4.5에서 작동 하는 코드가, 하나를 사용 하 여.NET 4에서 작동 하는 코드가 있습니다.

**.NET 4.5 예제**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample35.cs?highlight=1,3)]

**.NET 4 예**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample36.cs?highlight=3-4)]

사용 하는 경우 `await` 또는 `ContinueWith` 클라이언트 메서드 코드의 다음 줄을 실행 하기 전에 완료 될 때까지 기다려야 의미는 아닙니다 클라이언트 코드의 다음 줄이 실행 되기 전에 메시지가 표시 실제로 됩니다. 클라이언트 메서드 호출의 "완료"만 SignalR 모든 작업을 완료 메시지를 보내는 데 필요한 것을 의미 합니다. 클라이언트는 메시지를 받았음을 확인 해야 할 경우 사용자가 직접 메커니즘을 프로그래밍 해야 합니다. 예를 들어 코딩할 수는 `MessageReceived` 허브 및 메서드는 `addContosoChatMessageToPage` 메서드를 호출할 수 있습니다 클라이언트 `MessageReceived` 클라이언트에서 수행 하는 것이 해야 하면 작업을 수행한 후 합니다. `MessageReceived` 허브에서 할 수 있는 실제 클라이언트 ं आ स ा 원래 메서드 호출의 처리에는 작업에 따라 달라 집니다.

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>메서드 이름으로 문자열 변수를 사용 하는 방법

캐스팅 메서드 이름으로 문자열 변수를 사용 하 여 클라이언트 메서드를 호출 하려면 `Clients.All` (또는 `Clients.Others`, `Clients.Caller`등)를 `IClientProxy` 호출 [Invoke (methodName,... args) ](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample37.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>허브 클래스에서 그룹 구성원 자격을 관리 하는 방법

SignalR에서 그룹 연결 된 클라이언트의 지정 된 하위 집합에 메시지 브로드캐스트에 대 한 메서드를 제공합니다. 그룹의 클라이언트, 모든 수 있고 클라이언트가 여러 그룹의 멤버일 수 있습니다.

그룹 구성원 자격을 관리 하려면 사용 하 여는 [추가](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 및 [제거](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) 에서 제공 하는 메서드는 `Groups` 허브 클래스의 속성입니다. 다음 예제와 `Groups.Add` 및 `Groups.Remove` 호출 하는 JavaScript 클라이언트 코드가 뒤에 오는 클라이언트 코드에서 호출할 허브 메서드에서 사용 하는 방법입니다.

**서버**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample38.cs?highlight=5,10)]

**생성 된 프록시를 사용 하 여 JavaScript 클라이언트**

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample39.js)]

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample40.js)]

명시적으로 그룹을 만들 필요가 없습니다. 그룹에 대 한 호출에 해당 이름을 지정 하는 처음으로 자동으로 생성 적용 `Groups.Add`, 마지막 연결에 대 한 멤버 자격에서 제거할 때 삭제 됩니다.

그룹 멤버 자격 목록 또는 그룹 목록을 가져오는 데 필요한 API는 없습니다. SignalR 클라이언트와 그룹을 기반으로 메시지를 보냅니다는 [pub/sub 모델](http://en.wikipedia.org/wiki/Publish/subscribe), 서버 그룹 또는 그룹 멤버 자격 목록이 유지 되지 않습니다. 이렇게 하면 확장성을 최대화 웹 팜에 노드를 추가할 때마다 SignalR 유지 하는 모든 상태 하기 때문에 새 노드를 전파할 수 있습니다.

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>Add 및 Remove 메서드의 비동기 실행

`Groups.Add` 및 `Groups.Remove` 메서드를 비동기적으로 실행 합니다. 다음 사항을 확인 해야 하는 그룹에 클라이언트를 추가 및 즉시 그룹을 사용 하 여 클라이언트에 메시지를 전송 하려는 경우는 `Groups.Add` 메서드를 먼저 완료 합니다. 다음 코드 예제는.NET 4.5와.NET 4에서 작동 하는 코드를 사용 하 여 사용할 수 있는 코드를 사용 하 여 하나를 수행 하는 방법을 보여 줍니다.

**.NET 4.5 예제**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

**.NET 4 예**

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample42.cs?highlight=3-4)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>그룹 멤버 자격 지 속성

연결을 추적 하는 SignalR, 사용자가 아닌, 그럴 경우 사용자가 동일한 그룹에 사용자 설정 될 때마다 연결 5d; 호출 해야 `Groups.Add` 될 때마다 사용자는 새 연결을 설정 합니다.

다음 임시 연결 끊김 때로는 SignalR 복원할 수 연결이 자동으로. 이 경우 SignalR은 같은 연결을 새 연결을 설정 하지 복원과 이므로 클라이언트의 그룹 구성원 자격 자동으로 복원 됩니다. 가능한 임시 중단에 서버를 다시 부팅 또는 실패, 결과가 하는 경우에 때문에 이것이 그룹 멤버 자격을 포함 하 여 각 클라이언트에 대 한 연결 상태는 클라이언트로 라운드트립 합니다. 서버 작동이 중단 하 연결 시간이 초과 되기 전에 새 서버를 교체 하는 경우 클라이언트에서 새 서버로 자동으로 연결할 수 있고의 멤버인 그룹에 다시 등록 합니다.

연결이 끊어진 후 연결을 자동으로 복원할 수 없습니다 또는 때 연결 시간이 초과 했거나 경우 (예를 들어 경우 브라우저를 새 페이지로 이동) 클라이언트의 연결이 끊어지면, 그룹 멤버 자격 손실 됩니다. 다음에 사용자 연결에 대 한 새 연결 됩니다. 파일을 동일한 사용자는 새 연결을 설정 하는 경우 그룹 구성원 자격을 유지 하려면 응용 프로그램 사용자 및 그룹, 간의 연결을 추적 및 될 때마다 새 연결을 설정 하는 사용자 그룹 멤버 자격을 복원 하는 있습니다.

연결 및 다시 연결 하는 방법에 대 한 자세한 내용은 참조 [허브 클래스에서 연결 수명 이벤트를 처리 하는 방법을](#connectionlifetime) 이 항목의 뒷부분에 나오는 합니다.

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>단일 사용자 그룹

SignalR을 일반적으로 사용 하는 응용 프로그램 어떤 사용자가 메시지를 보낸 및 어떤 사용자 메시지를 수신 해야을 확인 하기 위해 사용자와 연결 간의 연결을 추적할 수 있어야 합니다. 그룹 작업을 수행 하는 두 가지 자주 사용 되는 패턴 중 하나에 사용 됩니다.

- 단일 사용자 그룹입니다.

    그룹 이름으로 사용자 이름을 지정 하 고 사용자 연결 되거나 다시 연결 될 때마다 그룹에 현재 연결 ID를 추가할 수도 있지만 그룹에 보낼 사용자에 게 메시지를 보냅니다. 이 방법의 단점은 그룹 하지 않는 제공입니다 하면 사용자가 온라인 또는 오프 라인 인지 확인할 수 있습니다.
- 사용자 이름 및 연결 Id 간의 연결을 추적 합니다.

    사전 또는 데이터베이스에 각 사용자 이름 및 하나 이상의 연결 Id 간의 연결을 저장 하 고 사용자 연결 되거나 연결 해제 될 때마다 저장 된 데이터를 업데이트할 수 있습니다. 사용자에 게 메시지를 보낼 연결 Id를 지정 합니다. 이 방법의 단점은 더 많은 메모리를 차지 한다는 것입니다.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>허브 클래스에서 연결 수명 이벤트를 처리 하는 방법

연결 수명 이벤트를 처리 하기 위한 일반적인 이유는 여부는 사용자가 연결 되어 있는지 여부를 추적 하 고 사용자 이름 및 연결 Id 간의 연결을 추적 하는 합니다. 클라이언트에서 연결 하거나 연결을 끊을 때 코드를 실행 하려면 재정의 `OnConnected`, `OnDisconnected`, 및 `OnReconnected` 다음 예제와 같이 허브의 가상 메서드 클래스입니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample43.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>OnConnected, OnDisconnected, 및 OnReconnected 호출 될 때

브라우저를 새 페이지로 이동 될 때마다 새 연결에 설정 될 SignalR 실행될지 의미는 `OnDisconnected` 메서드는 `OnConnected` 메서드. SignalR 새 연결이 설정 될 때 항상 새 연결 ID를 만듭니다.

`OnReconnected` 메서드는 케이블을 일시적으로 분리 및 연결 시간이 초과 되기 전에 다시 연결 경우 등,에서 SignalR 수 자동으로 복구 하는 연결에서 임시 중단 되었습니다. `OnDisconnected` 클라이언트 연결이 끊기고 SignalR 자동으로 다시 연결할 수 없습니다, 브라우저를 새 페이지로 이동 하는 경우와 같은 때 메서드를 호출 합니다. 따라서 지정된 된 클라이언트에 대 한 이벤트의 가능한 시퀀스는 `OnConnected`, `OnReconnected`, `OnDisconnected`; 또는 `OnConnected`, `OnDisconnected`합니다. 시퀀스를 표시 되지 않습니다 `OnConnected`, `OnDisconnected`, `OnReconnected` 지정된 된 연결에 대 한 합니다.

`OnDisconnected` 가 서버 작동이 중단 될 때와 같은 일부 시나리오에서는 메서드 호출 또는 응용 프로그램 도메인 재활용을 가져옵니다. 일부 클라이언트 온라인 상태가 다른 서버 또는 응용 프로그램 도메인의 재활용 완료 하는 경우 다시 연결 하 고 발생 하는 작업을 할 수 있습니다는 `OnReconnected` 이벤트입니다.

자세한 내용은 참조 [이해 하 고 SignalR에서 연결 수명 이벤트를 처리](index.md)합니다.

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>채워지지 호출자 상태

에 저장 된 모든 상태를 의미 하는 서버에서 연결 수명 이벤트 처리기 메서드 호출의 `state` 클라이언트에서 개체에 입력 되지 것입니다는 `Caller` 서버에 대 한 속성. 에 대 한 내용은 `state` 개체 및 `Caller` 속성 참조 [클라이언트와 허브 클래스 간의 상태를 전달 하는 방법을](#passstate) 이 항목의 뒷부분에 나오는 합니다.

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법

클라이언트에 대 한 정보를 가져오려면는 `Context` 허브 클래스의 속성입니다. `Context` 속성에서 반환 된 [HubCallerContext](https://msdn.microsoft.com/en-us/library/jj890883(v=vs.111).aspx) 다음 정보에 대 한 액세스를 제공 하는 개체:

- 호출 클라이언트의 연결 ID입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample44.cs?highlight=1)]

    연결 ID는 SignalR (사용자 코드에서 값을 지정할 수 없습니다.)으로 할당 하는 GUID입니다. 각 연결과 동일한 연결 여러 허브 응용 프로그램에 있는 경우 모든 허브에서 ID를 사용 하는 것에 대 한 연결 ID를 하나 있습니다.
- HTTP 헤더 데이터입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample45.cs?highlight=1)]

    HTTP 헤더에서 얻을 수 있습니다 `Context.Headers`합니다. 동일한 작업에 대 한 여러 참조에 대 한 이유는 `Context.Headers` 먼저 만들어진는 `Context.Request` 속성, 나중에 추가 하 고 `Context.Headers` 이전 버전과 호환성을 위해 유지 되었습니다.
- 문자열 데이터를 쿼리 합니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample46.cs?highlight=1)]

    데이터를 쿼리 문자열을 얻을 수 있습니다 `Context.QueryString`합니다.

    이 속성에서 가져올 쿼리 문자열은는 SignalR 연결을 설정 하는 HTTP 요청과 함께 사용 된 것입니다. 서버에는 클라이언트에서 클라이언트에 대 한 데이터를 전달 하는 편리한 방법은 연결을 구성 하 여 클라이언트에서 쿼리 문자열 매개 변수를 추가할 수 있습니다. 다음 예제에서는 생성 된 프록시를 사용 하는 경우 JavaScript 클라이언트에서 쿼리 문자열을 추가 하는 방법을 보여 줍니다.

    [!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample47.js?highlight=1)]

    쿼리 문자열 매개 변수를 설정 하는 방법에 대 한 자세한 내용은 참조에 대 한 API 가이드는 [JavaScript](index.md) 및 [.NET](index.md) 클라이언트입니다.

    쿼리 문자열 데이터 SignalR에서 내부적으로 사용 되는 일부 다른 값과 함께 연결에 사용 된 전송 메서드를 찾을 수 있습니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample48.cs)]

    값 `transportMethod` "Websocket", "serverSentEvents", "foreverFrame" 또는 "longPolling" 됩니다. 이 값을 확인 하는 경우는 `OnConnected` 이벤트 처리기 메서드 일부 시나리오에서 발생할 수 있습니다 처음 연결에 대 한 최종 협상 된 전송 메서드 없는 전송 값입니다. 이 경우 메서드 예외가 throw 됩니다 하 고 최종 전송 방법 설정 되 면 나중에 다시 호출 됩니다.
- 쿠키입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    쿠키를 얻을 수 있습니다 `Context.RequestCookies`합니다.
- 사용자 정보입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample50.cs?highlight=1)]
- 요청에 대 한 HttpContext 개체:

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample51.cs?highlight=1)]

    이 메서드를 사용 하 여 아닌 `HttpContext.Current` 가져오려는 `HttpContext` SignalR 연결에 대 한 개체입니다.

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>클라이언트와 허브 클래스 간의 상태를 전달 하는 방법

클라이언트 프록시는 제공 하는 `state` 개체를 각 메서드 호출을 사용 하 여 서버에 전송 될 데이터를 저장할 수 있습니다. 서버에서이 데이터에 액세스할 수 있습니다는 `Clients.Caller` 클라이언트에서 호출 하는 허브 메서드의 속성입니다. `Clients.Caller` 연결 수명 이벤트 처리기 방법에 대 한 속성은 채워지지 않습니다 `OnConnected`, `OnDisconnected`, 및 `OnReconnected`합니다.

만들기 또는 업데이트에 데이터는 `state` 개체 및 `Clients.Caller` 속성은 두 방향으로 모두 사용할 수 있습니다. 서버에서 값을 업데이트할 수 있습니다 및 클라이언트에 다시 전달 됩니다.

다음 예제에서는 모든 메서드 호출을 사용 하 여 서버에 전송에 대 한 상태를 저장 하는 JavaScript 클라이언트 코드를 보여 줍니다.

[!code-javascript[Main](signalr-1x-hubs-api-guide-server/samples/sample52.js?highlight=1-2)]

다음 예제에서는.NET 클라이언트에 해당 하는 코드를 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample53.cs?highlight=1-2)]

허브 클래스에이 데이터에 액세스할 수 있습니다는 `Clients.Caller` 속성입니다. 다음 예제에서는 이전 예제에서 참조 하는 상태를 검색 하는 코드를 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample54.cs?highlight=3-4)]

> [!NOTE]
> 지속 상태에 대 한이 메커니즘을 사용할 수 없는 많은 양의 데이터를 이후 모드로 전환할 모든 항목은 `state` 또는 `Clients.Caller` 속성은 모든 메서드 호출으로 라운드트립 합니다. 사용자 이름 또는 카운터 등의 더 작은 항목에는 것이 유용합니다.


<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>허브 클래스에는 오류를 처리 하는 방법

허브 클래스 메서드에서 발생 하는 오류를 처리 하려면 다음 방법 중 하나 또는 모두를 사용 합니다.

- Try / catch 블록에서 메서드 코드를 래핑하고 예외 개체를 기록 합니다. 디버깅 목적으로 클라이언트에 예외를 보낼 수 있지만 보안에 대 한 프로덕션의 클라이언트에 자세한 정보를 보내의 이유로 권장 되지 않습니다.
- 처리 하는 허브 파이프라인 모듈 만들기는 [OnIncomingError](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) 메서드. 다음 예제에서는 모듈을 허브 파이프라인에 삽입 합니다. Global.asax에 코드가 뒤에 오는 오류 로그에 기록 하는 파이프라인 모듈을 보여 줍니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample55.cs)]

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample56.cs?highlight=3)]

허브 파이프라인 모듈에 대 한 자세한 내용은 참조 [허브 파이프라인을 사용자 지정 하는 방법을](#hubpipeline) 이 항목의 뒷부분에 나오는 합니다.

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>추적을 사용 하는 방법

서버 쪽 추적을 사용 하려면이 예제에 나와 있는 것 처럼 system.diagnostics 요소, Web.config 파일에 추가 합니다.

[!code-html[Main](signalr-1x-hubs-api-guide-server/samples/sample57.html?highlight=17-72)]

Visual Studio에서 응용 프로그램을 실행 하는 경우 로그를 볼 수 있습니다는 **출력** 창.

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>클라이언트 메서드를 호출할 허브 클래스 외부에서 그룹을 관리 하는 방법

클라이언트 허브 클래스와는 다른 클래스에서 메서드를 호출 하십시오 허브에 대 한 SignalR 컨텍스트 개체에 대 한 참조를 가져오고를 사용 하 여 클라이언트에서 메서드를 호출 또는 그룹을 관리 합니다.

다음 샘플 `StockTicker` 클래스 컨텍스트 개체를 가져옵니다, 클래스의 인스턴스에 저장, 클래스 인스턴스는 정적 속성에 저장 및 단일 항목 클래스 인스턴스에서 컨텍스트 호출에 사용 하 여 `updateStockPrice` 클라이언트 상의 메서드 명명 된 허브에 연결 된 `StockTickerHub`합니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample58.cs?highlight=8,24)]

수명이 긴 개체에 있는 상황에 맞는 여러 번을 사용 해야 하는 경우 한 번에 대 한 참조를 가져오려면 대신 될 때마다 다시 가져오는 저장 합니다. 컨텍스트를 한 번 가져오기 하면 SignalR 허브 메서드 수행할 수 있는 클라이언트를 메서드 호출 하 고 동일한 시퀀스의 클라이언트에 메시지를 보냅니다. 허브에 대 한 SignalR 컨텍스트를 사용 하는 방법을 보여 주는 자습서를 참조 하십시오. [ASP.NET SignalR과 서버 브로드캐스트](index.md)합니다.

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>클라이언트 메서드 호출

클라이언트는 RPC를 받게 됩니다 지정할 수 있지만 허브 클래스에서 호출 하는 경우 보다 더 적은 옵션이 있습니다. 이러한 이유로 없다는 컨텍스트는 클라이언트로부터 특정 호출에 연결 된 때문는 메서드는 현재 연결 ID 알고와 같은 `Clients.Others`, 또는 `Clients.Caller`, 또는 `Clients.OthersInGroup`는 사용할 수 없습니다. 다음 옵션을 사용할 수 있습니다.

- 연결 된 모든 클라이언트입니다.

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample59.cs)]
- 특정 클라이언트 연결 ID로 식별

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample60.css)]
- 연결 된 모든 클라이언트 연결 ID로 식별 하는 지정 된 클라이언트를 제외한

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample61.cs)]
- 지정된 된 그룹에 연결 된 모든 클라이언트입니다.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample62.css)]
- 연결 ID로 식별 하는 지정 된 클라이언트를 제외한 지정된 된 그룹의 모든 연결 된 클라이언트

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample63.cs)]

를 호출 하는 비-허브 클래스에 방법 중에서 허브 클래스에 경우에 현재 연결 ID를 전달할 고 된 경우에 사용할 수 있습니다 `Clients.Client`, `Clients.AllExcept`, 또는 `Clients.Group` 시뮬레이션할 `Clients.Caller`, `Clients.Others`, 또는 `Clients.OthersInGroup`합니다. 다음 예제에서는 `MoveShapeHub` 클래스 연결 ID를 전달는 `Broadcaster` 클래스 있도록는 `Broadcaster` 클래스를 시뮬레이션할 수 `Clients.Others`합니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample64.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>그룹 멤버 자격 관리

그룹 관리에 대 한 허브 클래스에 작업을 수행한와 동일한 옵션이 제공 됩니다.

- 그룹에 클라이언트 추가

    [!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample65.cs)]
- 그룹에서 클라이언트를 제거 합니다.

    [!code-css[Main](signalr-1x-hubs-api-guide-server/samples/sample66.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>허브 파이프라인을 사용자 지정 하는 방법

SignalR을 사용 하는 허브 파이프라인에 사용자 고유의 코드를 넣을 수 있습니다. 다음 예제에서는 클라이언트 및 클라이언트에서 호출 하는 나가는 메서드 호출에서 받은 각 들어오는 메서드 호출을 기록 하는 사용자 지정 허브 파이프라인 모듈을 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample67.cs)]

다음 코드에 *Global.asax* 허브 파이프라인에서 실행 하도록 모듈을 등록 하는 파일:

[!code-csharp[Main](signalr-1x-hubs-api-guide-server/samples/sample68.cs?highlight=3)]

재정의할 수 있는 여러 가지 방법이 있습니다. 전체 목록을 보려면를 참조 하십시오. [HubPipelineModule 메서드](https://msdn.microsoft.com/en-us/library/jj918633(v=vs.111).aspx)합니다.
