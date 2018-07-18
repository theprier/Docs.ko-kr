---
title: ASP.NET Core SignalR 소개
author: tdykstra
description: ASP.NET Core SignalR 라이브러리를 앱에 실시간 기능 추가 간소화 하는 방법에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 04/25/2018
uid: signalr/introduction
ms.openlocfilehash: bc6f25c3f35e7fb0c2c68220697f2e0fdc6a9958
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095391"
---
# <a name="introduction-to-aspnet-core-signalr"></a>ASP.NET Core SignalR 소개

작성자: [Rachel Appel](https://twitter.com/rachelappel)

## <a name="what-is-signalr"></a>SignalR 이란?

ASP.NET Core SignalR은 실시간 웹 기능을 앱에 추가 간소화 하는 라이브러리. 실시간 웹 기능 클라이언트로 푸시 콘텐츠를 서버 쪽 코드를 즉시 있습니다.

SignalR에 대 한 것이 좋습니다.

* 서버에서 자주 업데이트가 필요한 앱입니다. 게임, 소셜 네트워크, 투표, 경매, 지도 및 GPS 앱을 예로 들 수 있습니다.
* 대시보드 및 모니터링 앱입니다. 예를 들어 회사 대시보드, 즉석 판매 업데이트 또는 여행 경고가.
* 공동 작업 앱입니다. 화이트 보드 앱 및 팀 회의 소프트웨어가 공동 작업 앱의 예입니다.
* 알림이 필요한 앱입니다. 소셜 네트워크, 이메일, 채팅, 게임, 여행 경고 및 다른 많은 앱 알림을 사용합니다.

서버에서 클라이언트를 만들기 위한 API를 제공 하는 SignalR [원격 프로시저 호출 (RPC)](https://wikipedia.org/wiki/Remote_procedure_call)합니다. Rpc 서버 쪽.NET Core 코드에서 클라이언트에서 JavaScript 함수를 호출합니다.

ASP.NET core SignalR:

* 연결 관리를 자동으로 처리합니다.
* 메시지가 연결 된 모든 클라이언트에 동시에 브로드캐스트할 수 있습니다. 예를 들어 대화방입니다.
* 특정 클라이언트 또는 클라이언트 그룹에 메시지를 보낼 수 있습니다.
* 오픈 소싱할 [GitHub](https://github.com/aspnet/signalr)합니다.
* 확장 가능 합니다.

클라이언트와 서버 간의 연결이 영구적 이므로, HTTP 연결과 달리 합니다.

## <a name="transports"></a>전송

실시간 웹 응용 프로그램을 구축 하는 방법의 여러 SignalR 요약 합니다. [Websocket](https://tools.ietf.org/html/rfc7118) 최적의 전송 이지만 Server-Sent 이벤트 및 Long Polling과 같은 다른 기술을 사용할 수 없는 해당 하는 경우 사용할 수 있습니다. SignalR은 자동으로 감지 하 고 서버 및 클라이언트에서 지원 되는 기능을 기반으로 하는 적절 한 전송을 초기화 합니다.

## <a name="hubs"></a>허브

SignalR 허브를 사용 하 여 클라이언트와 서버 간 통신.

허브는 클라이언트와 서버에서 서로 다른 메서드를 호출할 수 있도록 하는 높은 수준의 파이프라인. 클라이언트가 서버에서 로컬 메서드로 쉽게 이동 하 고 그 반대의 경우로 메서드를 호출할 수 있도록 자동으로 컴퓨터 경계를 넘어 디스패치 SignalR에서 처리 합니다. 허브 모델 바인딩을 활성화 하는 방법에 강력한 형식의 매개 변수를 전달할 수 있도록 합니다. SignalR 제공 두 가지 기본 제공 허브 프로토콜: JSON 및 기반 이진 프로토콜을 기반으로 하는 텍스트 프로토콜 [MessagePack](https://msgpack.org/)합니다.  MessagePack은 일반적으로 JSON을 사용할 때 보다 작은 메시지를 만듭니다. 이전 버전의 브라우저를 지원 해야 합니다 [XHR 수준 2](https://caniuse.com/#feat=xhr2) MessagePack 프로토콜 지원을 제공 합니다.

허브 활성 전송을 사용 하 여 메시지를 전송 하 여 클라이언트 쪽 코드를 호출 합니다. 메시지 이름 및 클라이언트 쪽 메서드의 매개 변수를 포함 합니다. 메서드 매개 변수로 보낸 개체는 구성된 된 프로토콜을 사용 하 여 역직렬화 됩니다. 클라이언트는 클라이언트 쪽 코드에서 메서드 이름을 찾으려고 합니다. 일치 하는 경우 클라이언트 메서드는 deserialize 된 매개 변수 데이터를 사용 하 여 실행 합니다.

## <a name="additional-resources"></a>추가 자료

* [ASP.NET core SignalR을 사용 하 여 시작](xref:tutorials/signalr)
* [지원되는 플랫폼](xref:signalr/supported-platforms)
* [허브](xref:signalr/hubs)
* [JavaScript 클라이언트](xref:signalr/javascript-client)
