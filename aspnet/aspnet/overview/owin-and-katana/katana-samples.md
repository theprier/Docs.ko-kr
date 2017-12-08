---
uid: aspnet/overview/owin-and-katana/katana-samples
title: "Katana 샘플 | Microsoft Docs"
author: microsoft
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2014
ms.topic: article
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 5540164bda8db31c4e78b49ecb7f7c573acca013
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="katana-samples"></a>Katana 샘플
====================
여 [Microsoft](https://github.com/microsoft)

## <a name="katana-samples"></a>Katana 샘플

**ASP.NET 라우팅합니다 샘플** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/AspNetRoutes/ReadMe.txt)  
일부 응용 프로그램 비 OWIN 구성 요소와 함께 Asp.Net 경로 테이블에는 OWIN 구성 요소를 연결 합니다. 이 샘플에서는 MapOwinPath 및 Microsoft.Owin.Host.SystemWeb 제공한 MapOwinRoute RouteCollection 확장 메서드를 사용 하는 방법을 보여 줍니다.

**샘플 파이프라인 분기** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/BranchingPipelines/ReadMe.txt)  
OWIN 요청 처리 파이프라인을 선형 될 필요가 없습니다, 다른 방법으로 요청을 처리 하는 분기 될 수 있는 합니다. 이 샘플에는 요청 경로 또는 헤더와 같은 다른 요청 데이터에 따라 분기 파이프라인을 생성 하는 방법을 보여 줍니다. 이러한 구성 요소는 Microsoft.Owin.Mapping nuget 패키지에서 사용할 수 있습니다.

**사용자 지정 서버 샘플** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/CustomServer/MyCustomServer/CustomServer.cs)   
자체 호스팅하는 경우 사용자 지정 OWIN 서버를 사용 하는 방법을 보여 줍니다. OWIN 합니다.

**샘플에 포함 된** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/Embedded/ReadMe.txt)  
사용자가 소유한 프로세스 환경 일부 OWIN 서버에서 실행 될 수 있습니다 (&quot;자체 호스트&quot;). 이 샘플에서는 Microsoft.Owin.Hosting nuget 패키지에서 제공 하는 도구를 사용 하 여 OWIN 응용 프로그램을 시작 하는 방법을 보여 줍니다.

**HelloWorld 샘플** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/HelloWorld/ReadMe.txt)  
OWIN은 HTTP 서버 응용 프로그램 이식성을 통해 다양 한 서버 간에 API 추상화입니다. 이 샘플에서는 일부를 사용 하 여 Hello World 응용 프로그램을 작성 하는 방법을 보여 줍니다. **간단한 래퍼** ASP.NET 웹 서버에 같은 원시 OWIN 추상화 및 실행 합니다.

**Hello World 원시 OWIN 샘플** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/HelloWorldRawOwin/ReadMe.txt)  
이 샘플에 사용 하 여 Hello World 응용 프로그램을 작성 하는 방법을 보여 줍니다는 **원시** OWIN 추상화 및 Asp.Net과 같은 웹 서버에서 실행 합니다.

**SignalR 샘플** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/SignalR/Program.cs)  
SignalR OWIN를 사용 하 여 자체 호스트 하는 방법을 보여 줍니다. / Katana 합니다. 자체 호스팅을 SignalR에 대 한 자세한 내용은 참조 하십시오. [자습서: 자체 호스트 하는 SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)합니다.

**정적 샘플 파일** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/StaticFilesSample/Startup.cs)   
OWIN를 사용 하 여 정적 파일에 대 한 HTTP 요청을 지 원하는 방법을 보여 줍니다. / Katana 합니다.

**Web API** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/WebApi/ReadMe.txt)   
이 예제에는 OWIN IIS에서 호스트 웹 API OWIN 파이프라인을 추가 하는 방법을 보여 줍니다.

**웹 소켓 샘플** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/WebSocketSample/WebSocketServer/Startup.cs)   
사용 하 여 웹 소켓 OWIN에서 지 원하는 방법을 보여 줍니다는 [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/en-us/library/system.net.websockets.websocket(v=vs.110).aspx) 클래스입니다.
