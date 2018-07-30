---
title: ASP.NET Core SignalR 소개
author: tdykstra
description: ASP.NET Core SignalR 라이브러리를 앱에 실시간 기능 추가 간소화 하는 방법에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 04/25/2018
uid: signalr/introduction
ms.openlocfilehash: 2fff24609caf7592bad763a077288990a29617aa
ms.sourcegitcommit: 927e510d68f269d8335b5a7c8592621219a90965
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2018
ms.locfileid: "39342551"
---
# <a name="introduction-to-aspnet-core-signalr"></a>ASP.NET Core SignalR 소개

## <a name="what-is-signalr"></a>SignalR 이란?

ASP.NET Core SignalR은 실시간 웹 기능을 앱에 추가 간소화 하는 오픈 소스 라이브러리입니다. 실시간 웹 기능 클라이언트로 푸시 콘텐츠를 서버 쪽 코드를 즉시 있습니다.

SignalR에 대 한 것이 좋습니다.

* 서버에서 자주 업데이트가 필요한 앱입니다. 게임, 소셜 네트워크, 투표, 경매, 지도 및 GPS 앱을 예로 들 수 있습니다.
* 대시보드 및 모니터링 앱입니다. 예를 들어 회사 대시보드, 즉석 판매 업데이트 또는 여행 경고가.
* 공동 작업 앱입니다. 화이트 보드 앱 및 팀 회의 소프트웨어가 공동 작업 앱의 예입니다.
* 알림이 필요한 앱입니다. 소셜 네트워크, 이메일, 채팅, 게임, 여행 경고 및 다른 많은 앱 알림을 사용합니다.

서버에서 클라이언트를 만들기 위한 API를 제공 하는 SignalR [원격 프로시저 호출 (RPC)](https://wikipedia.org/wiki/Remote_procedure_call)합니다. Rpc 서버 쪽.NET Core 코드에서 클라이언트에서 JavaScript 함수를 호출합니다.

ASP.NET core SignalR의 기능 중 일부는 다음과 같습니다.

* 연결 관리를 자동으로 처리합니다.
* 동시에 연결 된 모든 클라이언트에 메시지를 보냅니다. 예를 들어 대화방입니다.
* 특정 클라이언트 또는 클라이언트 그룹에 메시지를 보냅니다.
* 증가 트래픽을 처리 하도록 확장 합니다.

원본에서 호스트 되는 [GitHub의 SignalR 리포지토리](https://github.com/aspnet/signalr)합니다.

## <a name="transports"></a>전송

SignalR 실시간 통신을 처리 하기 위한 몇 가지 기법을 지원 합니다.

* [WebSockets](https://tools.ietf.org/html/rfc7118)
* 서버에서 전송 이벤트
* 긴 폴링

SignalR에는 자동으로 서버와 클라이언트의 기능 내에 있는 최상의 전송 방법을 선택 합니다.

## <a name="hubs"></a>허브

사용 하 여 SignalR *hubs* 클라이언트와 서버 간 통신.

허브는 클라이언트와 서버에서 서로 다른 메서드를 호출할 수 있는 높은 수준의 파이프라인. 클라이언트가 서버의 그 반대로 메서드를 호출할 수 있도록 자동으로 컴퓨터 경계를 넘어 디스패치 SignalR에서 처리 합니다. 모델 바인딩을 활성화 하는 방법에 강력한 형식의 매개 변수를 전달할 수 있습니다. SignalR 제공 두 가지 기본 제공 허브 프로토콜: JSON 및 기반 이진 프로토콜을 기반으로 하는 텍스트 프로토콜 [MessagePack](https://msgpack.org/)합니다.  일반적으로 MessagePack JSON에 비해 크기가 작은 메시지를 만듭니다. 이전 버전의 브라우저를 지원 해야 합니다 [XHR 수준 2](https://caniuse.com/#feat=xhr2) MessagePack 프로토콜 지원을 제공 합니다.

허브 이름 및 클라이언트 쪽 메서드의 매개 변수를 포함 하는 메시지를 전송 하 여 클라이언트 쪽 코드를 호출 합니다. 메서드 매개 변수로 보낸 개체는 구성된 된 프로토콜을 사용 하 여 역직렬화 됩니다. 클라이언트는 클라이언트 쪽 코드에서 메서드 이름을 찾으려고 합니다. 클라이언트에 일치 항목을 찾으면 메서드를 호출 하 고 deserialize 된 매개 변수 데이터를 전달 합니다.

## <a name="additional-resources"></a>추가 자료

* [ASP.NET core SignalR을 사용 하 여 시작](xref:tutorials/signalr)
* [지원되는 플랫폼](xref:signalr/supported-platforms)
* [허브](xref:signalr/hubs)
* [JavaScript 클라이언트](xref:signalr/javascript-client)
