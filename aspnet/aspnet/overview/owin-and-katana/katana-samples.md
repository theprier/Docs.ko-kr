---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana 샘플 | Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: b8ce2b40a19e0429f1ccedb03b8f829582652d24
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828530"
---
<a name="katana-samples"></a>Katana 샘플
====================
[Microsoft](https://github.com/microsoft)

## <a name="katana-samples"></a>Katana 샘플

**ASP.NET 샘플 라우팅합니다** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
일부 응용 프로그램에서 비 OWIN 구성 요소와 함께 Asp.Net 경로 테이블에는 OWIN 구성 요소를 연결 해야 합니다. 이 샘플에서는 MapOwinPath 및 Microsoft.Owin.Host.SystemWeb 제공한 MapOwinRoute RouteCollection 확장 메서드를 사용 하는 방법을 보여 줍니다.

**샘플 파이프라인 분기** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
다른 방법으로 요청을 처리 하는 분기 될 수 있는 OWIN 요청 처리 파이프라인 선형 할 필요는 없습니다. 이 샘플에는 헤더와 같은 다른 요청 데이터 또는 요청 경로에 따라 파이프라인을 분기를 생성 하는 방법을 보여 줍니다. 이러한 구성 요소 Microsoft.Owin.Mapping nuget 패키지에 사용할 수 있습니다.

**사용자 지정 서버 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)   
자체 호스팅하는 경우 사용자 지정 OWIN 서버를 사용 하는 방법을 보여 줍니다. OWIN 합니다.

**샘플을 포함** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)  
사용자 고유의 프로세스 내에서 일부 OWIN 서버를 실행할 수 있습니다 (&quot;자체 호스팅&quot;). 이 샘플에서는 Microsoft.Owin.Hosting nuget 패키지에서 제공 하는 도구를 사용 하 여 OWIN 응용 프로그램을 시작 하는 방법을 보여 줍니다.

**HelloWorld 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN은 HTTP 서버에서 다양 한 서버 응용 프로그램 이식성을 수 있는 API 추상화를입니다. 이 샘플에서는 일부를 사용 하 여 Hello World 응용 프로그램을 작성 하는 방법을 보여 줍니다 **간단한 래퍼** ASP.NET 웹 서버에서 같은 원시 OWIN 추상화 및 실행 합니다.

**Hello World 원시 OWIN 예제** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
이 샘플을 사용 하 여 Hello World 응용 프로그램을 작성 하는 방법에 설명 합니다 **원시** OWIN 추상화 및 Asp.Net과 같은 웹 서버에서 실행 합니다.

**SignalR 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
OWIN을 사용 하 여 SignalR 자체 호스트 하는 방법을 보여 줍니다 / Katana 합니다. 자체 호스팅 SignalR에 대 한 자세한 내용은 참조 하세요. [자습서: SignalR 자체 호스팅](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)합니다.

**정적 파일 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)   
OWIN을 사용 하 여 정적 파일에 대 한 HTTP 요청을 지 원하는 방법을 보여 줍니다 / Katana 합니다.

**웹 API** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)   
이 샘플에는 IIS에서 OWIN 호스트 OWIN 파이프라인에 Web API를 추가 하는 방법을 보여 줍니다.

**웹 소켓 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)   
사용 하 여 OWIN에서 Websocket을 지원 하는 방법을 보여 줍니다 합니다 [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) 클래스입니다.
