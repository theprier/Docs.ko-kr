---
title: ASP.NET Core SignalR 소개
author: rachelappel
description: ASP.NET Core SignalR 라이브러리 간소화 앱에 실시간 웹 기능을 추가 하는 방법을 알아봅니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 03/07/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/introduction
ms.openlocfilehash: fa9b10201b5dc0e67bcd6d1321a3737e2025fda4
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="introduction-to-aspnet-core-signalr"></a>ASP.NET Core SignalR 소개

작성자: [Rachel Appel](https://twitter.com/rachelappel)


[!INCLUDE [2.1 preview notice](~/includes/2.1.md)]

## <a name="what-is-signalr"></a>SignalR 란?

ASP.NET Core SignalR은 간소화 실시간 웹 기능을 응용 프로그램을 추가 하는 라이브러리입니다. 실시간 웹 기능을 통해 서버 쪽 코드를 클라이언트에 푸시 콘텐츠 즉시 합니다.

SignalR 하기에 적합 합니다.

* 서버에서 자주 발생 하는 업데이트를 필요로 하는 앱입니다. 예로 게임, 소셜 네트워크, 투표, 경매, 맵 및 GPS 앱에는 있습니다.
* 대시보드 및 모니터링 응용 프로그램입니다. 예로 회사 대시보드를 인스턴트 판매 업데이트 하거나 경고를 이동 합니다.
* 공동 작업 응용 프로그램입니다. 화이트 보드 앱과 소프트웨어를 충족 하는 팀은 공동 작업 응용 프로그램의 예입니다.
* 알림이 필요로 하는 앱입니다. 소셜 네트워크, 전자 메일, 채팅, 게임, 여행 경고 및 다른 많은 응용 프로그램 알림을 사용합니다.

서버-클라이언트를 만들기 위한 API를 제공 하는 SignalR [원격 프로시저 호출 (RPC)](https://wikipedia.org/wiki/Remote_procedure_call)합니다. Rpc 서버 쪽.NET Core 코드에서 클라이언트에서 JavaScript 함수를 호출 합니다.

ASP.NET Core 용 SignalR:

* 연결 관리를 자동으로 처리합니다.
* 연결 된 모든 클라이언트에 동시에 메시지를 브로드캐스트를 사용 합니다. 예를 들어: 채트 방 합니다.
* 특정 클라이언트 또는 그룹의 클라이언트에 메시지를 보낼 수 있습니다.
* 오픈 소스는 [GitHub](https://github.com/aspnet/signalr)합니다.
* 확장 가능 합니다.

클라이언트와 서버 간의 연결이 HTTP 연결과 달리 지속 됩니다.

## <a name="transports"></a>전송

다양 한 기술을 갖추고 실시간 웹 응용 프로그램을 통해 SignalR 간단히 설명 합니다. [Websocket](https://tools.ietf.org/html/rfc7118) 는 최적의 전송 되지만 해당 장치가 사용할 수 없는 경우 Server-Sent 이벤트 및 긴 폴링와 같은 다른 기법을 사용할 수 있습니다. SignalR에서는 자동으로 검색 하 고 서버와 클라이언트에서 지원 되는 기능을 기반으로 적절 한 전송을 초기화 합니다.

## <a name="hubs-and-endpoints"></a>허브 및 끝점

SignalR 허브와 끝점을 사용 하 여 클라이언트와 서버 간 통신 합니다. 허브 API에서는 대부분의 시나리오에 설명 합니다.

허브는 클라이언트와 서버에서 다른 메서드를 호출할 수 있도록 하는 끝점 API를 기반으로 하는 높은 수준의 파이프라인입니다. 클라이언트가 서버에서 로컬 메서드로 쉽게 그 반대의으로 메서드를 호출할 수 있도록 자동으로 컴퓨터 경계 간 디스패치 SignalR에서 처리 합니다. 허브 모델 바인딩 수 있는 강력한 형식의 매개 변수 하는 메서드에 전달 되도록 허용 합니다. 두 개의 기본 제공 허브 프로토콜을 제공 하는 SignalR: JSON 및 기반 이진 프로토콜을 기반으로 텍스트 프로토콜 [MessagePack](https://msgpack.org/)합니다.  MessagePack은 일반적으로 JSON을 사용할 때 보다 작은 메시지를 만듭니다. 이전 버전의 브라우저를 지원 해야 [XHR 수준 2](https://caniuse.com/#feat=xhr2) MessagePack 프로토콜 지원을 제공 하기 위해 합니다.

활성 전송을 사용 하 여 메시지를 전송 하 여 클라이언트 쪽 코드를 호출 하는 허브입니다. 메시지 이름 및 클라이언트 쪽 메서드의 매개 변수를 포함 합니다. 메서드 매개 변수로 보낸 개체 구성 된 프로토콜을 사용 하 여 deserialize 됩니다. 클라이언트는 클라이언트 쪽 코드의 메서드에 대 한 이름과 일치 하도록 시도 합니다. 일치 하는 경우 클라이언트 메서드는 deserialize 된 매개 변수 데이터를 사용 하 여 실행 합니다.

끝점에는 클라이언트에서 읽고 쓸 수 있도록 원시 소켓 같은 API를 제공 합니다. 그룹화, 브로드캐스트, 및 기타 기능을 처리 하도록 개발자에 게 중인지 합니다. 허브 API 끝점 계층 위에 빌드됩니다.

다음 다이어그램은 허브, 끝점 및 클라이언트 간의 관계를 보여줍니다.

![SignalR 맵](introduction/_static/signalr-core-architecture.png)

## <a name="related-resources"></a>관련 참고 자료

[ASP.NET Core 용 SignalR 시작](xref:signalr/get-started)
