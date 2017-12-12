---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: "SignalR 추적 사용 | Microsoft Docs"
author: tfitzmac
description: "이 문서에서는 SignalR 서버와 클라이언트에 대 한 추적을 구성 하는 방법에 설명 합니다. 추적을 사용 하면 이벤트에 대 한 진단 정보를 볼 수 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/08/2014
ms.topic: article
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 2f01ab5d66e44cd82634f1b3df1ca6c78b7fd9d5
ms.sourcegitcommit: c07fb5cb5df0a12f9fe6735fcbc90964608fa687
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/14/2017
---
<a name="enabling-signalr-tracing"></a>SignalR 추적 사용
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 SignalR 서버와 클라이언트에 대 한 추적을 구성 하는 방법에 설명 합니다. 추적을 사용 하 여 SignalR 응용 프로그램에서 이벤트에 대 한 진단 정보를 볼 수 있습니다.
> 
> 이 항목 원래 Patrick Fletcher 썼습니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET Framework 4.5
> - SignalR 버전 2
>   
> 
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이
> 
> 이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요. 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


추적을 사용 하는 경우는 SignalR 응용 프로그램 이벤트에 대 한 로그 항목을 만듭니다. 클라이언트와 서버 모두에서 이벤트를 기록할 수 있습니다. 서버 로그를 연결, 확장 공급자 및 메시지 버스 이벤트에서 추적 합니다. 클라이언트 연결 이벤트는 추적 중입니다. SignalR 2.1 이상 버전에서는 추적이 클라이언트에 허브 호출 메시지의 전체 콘텐츠를 기록합니다.

## <a name="contents"></a>목차

- [서버에서 추적을 사용 하도록 설정](#server)

    - [텍스트 파일에 서버 이벤트 로깅](#server_text)
    - [서버 이벤트를 이벤트 로그에 로깅](#server_eventlog)
- [.NET 클라이언트 (Windows 바탕 화면 앱)에서 추적 설정](#net_client)

    - [콘솔에 데스크톱 클라이언트 이벤트 로깅](#desktop_console)
    - [텍스트 파일에 로깅 데스크톱 클라이언트 이벤트](#desktop_text)
- [Windows Phone 8 클라이언트에서 추적 설정](#phone)

    - [UI에 Windows Phone 클라이언트 이벤트 로깅](#phone_ui)
    - [디버그 콘솔에 Windows Phone 클라이언트 이벤트 로깅](#phone_debug)
- [JavaScript 클라이언트에서 추적 설정](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a>서버에서 추적을 사용 하도록 설정

응용 프로그램의 구성 파일 (App.config 또는 Web.config 프로젝트의 유형에 따라.) 서버에서 추적을 사용 하도록 설정 기록 하려는 이벤트의 범주를 지정 합니다. 구성 파일도 지정 텍스트 파일, Windows 이벤트 로그 또는의 구현을 사용 하 여 사용자 지정 로그에 이벤트를 기록할 것인지 [TraceListener](https://msdn.microsoft.com/en-us/library/system.diagnostics.tracelistener(v=vs.110).aspx)합니다.

서버 이벤트 범주에는 다음과 같은 메시지

| 소스 | 메시지 |
| --- | --- |
| SignalR.SqlMessageBus | SQL 메시지 버스 확장 공급자를 설치, 데이터베이스 작업, 오류 및 제한 시간 이벤트 |
| SignalR.ServiceBusMessageBus | 서비스 버스 확장 공급자 항목 만들기 및 구독, 오류 및 메시징 이벤트 |
| SignalR.RedisMessageBus | Redis 확장 공급자 연결, 연결 끊기 및 오류 이벤트 |
| SignalR.ScaleoutMessageBus | 메시징 이벤트 확장 |
| SignalR.Transports.WebSocketTransport | WebSocket 전송 연결, 연결 끊기, 메시징 및 오류 이벤트 |
| SignalR.Transports.ServerSentEventsTransport | ServerSentEvents 전송 연결, 연결 끊기, 메시징 및 오류 이벤트 |
| SignalR.Transports.ForeverFrameTransport | ForeverFrame 전송 연결, 연결 끊기, 메시징 및 오류 이벤트 |
| SignalR.Transports.LongPollingTransport | LongPolling 전송 연결, 연결 끊기, 메시징 및 오류 이벤트 |
| SignalR.Transports.TransportHeartBeat | 연결, 연결 끊기 및 keepalive 이벤트 전송 |
| SignalR.ReflectedHubDescriptorProvider | 검색 이벤트 허브 |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a>텍스트 파일에 서버 이벤트 로깅

다음 코드에는 각 범주의 이벤트에 대 한 추적을 설정 하는 방법을 보여 줍니다. 이 샘플에서는 텍스트 파일에 이벤트를 기록 하도록 응용 프로그램을 구성 합니다.

**추적 사용에 대 한 XML 서버 코드**

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

위의 코드에서는 `SignalRSwitch` 항목 지정는 [TraceLevel](https://msdn.microsoft.com/en-us/library/system.diagnostics.tracelevel(v=vs.110).aspx) 지정 된 로그로 전송 하는 이벤트에 사용 합니다. 이 경우 설정 되어 `Verbose` 즉, 모든 디버깅 및 추적 메시지가 기록 됩니다.

다음과 같은 출력 항목을 보여 줍니다.는 `transports.log.txt` 위의 구성 파일을 사용 하 여 응용 프로그램에 대 한 파일입니다. 새 표시 연결, 제거 된 연결 및 전송 하트 비트 이벤트입니다.

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a>서버 이벤트를 이벤트 로그에 로깅

텍스트 파일이 아닌 이벤트 로그에 이벤트를 기록 하려면의 엔터티에 대 한 값을 변경는 `sharedListeners` 노드. 다음 코드에는 서버 이벤트를 이벤트 로그에 기록 하는 방법을 보여 줍니다.

**이벤트 로그에 이벤트를 기록에 대 한 XML 서버 코드**

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

이벤트 응용 프로그램 로그에 기록 되 고 아래 표시 된 것과 같이 이벤트 뷰어를 통해 사용할 수 있습니다.

![SignalR 로그를 표시 하는 이벤트 뷰어](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> 이벤트 로그를 사용할 때는 **TraceLevel** 를 **오류** 메시지 수를 관리할 수 있도록 합니다.

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a>.NET 클라이언트 (Windows 바탕 화면 앱)에서 추적 설정

.NET 클라이언트는 콘솔에 텍스트 파일 또는의 구현을 사용 하 여 사용자 지정 로그에 이벤트를 기록할 수 있습니다 [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter.aspx)합니다.

.NET 클라이언트 로그인을 사용 하려면 연결의 설정 `TraceLevel` 속성을 한 [TraceLevels](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) 값 및 `TraceWriter` 속성을 유효한 [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter.aspx) 인스턴스.

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a>콘솔에 데스크톱 클라이언트 이벤트 로깅

다음 C# 코드에서.NET 클라이언트는 콘솔에 이벤트를 기록 하는 방법을 보여 줍니다.

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a>텍스트 파일에 로깅 데스크톱 클라이언트 이벤트

다음 C# 코드를 텍스트 파일로.NET 클라이언트에서 이벤트를 기록 하는 방법을 보여 줍니다.

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

다음과 같은 출력 항목을 보여 줍니다.는 `ClientLog.txt` 위의 구성 파일을 사용 하 여 응용 프로그램에 대 한 파일입니다. 클라이언트 메서드를 호출할 허브 호출 및 서버에 연결 하는 클라이언트를 보여 주므로 `addMessage`:

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a>Windows Phone 8 클라이언트에서 추적 설정

Windows Phone 앱 용 SignalR 응용 프로그램 같은.NET 클라이언트를 사용 하 여 데스크톱 응용 프로그램으로 하지만 [Console.Out](https://msdn.microsoft.com/en-us/library/system.console.out(v=vs.110).aspx) 및 사용 하 여 파일 쓰기 [StreamWriter](https://msdn.microsoft.com/en-us/library/system.io.streamwriter(v=vs.110).aspx) 는 사용할 수 없습니다. 대신, 사용자 지정 구현을 만들 해야 [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter(v=vs.110).aspx) 추적에 대 한 합니다. 

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a>UI에 Windows Phone 클라이언트 이벤트 로깅

[SignalR 코드 베이스](https://github.com/SignalR/SignalR/archive/master.zip) 추적 출력을 작성 하는 Windows Phone 샘플이 포함 되어는 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 사용자 지정을 사용 하 여 [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter(v=vs.110).aspx) 호출 구현 `TextBlockWriter`합니다. 이 클래스에서 확인할 수 있습니다는 **samples/Microsoft.AspNet.SignalR.Client.WP8.Samples** 프로젝트. 인스턴스를 만들 때 `TextBlockWriter`, 현재에서 전달 [SynchronizationContext](https://msdn.microsoft.com/en-us/library/system.threading.synchronizationcontext(v=vs.110).aspx), 및 [StackPanel](https://msdn.microsoft.com/en-us/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) 생성 됩니다는 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 추적에 사용할 출력:

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

그런 다음 새에 추적 출력을 기록 됩니다 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 에서 만든는 [StackPanel](https://msdn.microsoft.com/en-us/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) 에 전달 합니다.

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a>디버그 콘솔에 Windows Phone 클라이언트 이벤트 로깅

UI가 아닌 디버그 콘솔에 출력을 보내려면의 구현을 만드는 [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter(v=vs.110).aspx) 디버그 창에 기록 하 고이 연결의 할당 [TraceWriter](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) 속성:

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

그런 다음 Visual Studio의 디버그 창에 추적 정보를 기록 합니다.

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a>JavaScript 클라이언트에서 추적 설정

클라이언트 쪽 로깅에 대 한 연결을 사용 하려면 설정는 `logging` 호출 하기 전에 연결 개체에 `start` 연결을 설정 하는 메서드.

**생성 된 프록시) (사용 하 여 브라우저 콘솔에 대 한 추적을 사용 하기 위한 클라이언트 JavaScript 코드**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

**생성 된 프록시) (없이 브라우저 콘솔에 대 한 추적을 사용 하기 위한 클라이언트 JavaScript 코드**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

추적을 사용 하는 경우 JavaScript 클라이언트 브라우저 콘솔에 이벤트를 기록 합니다. 브라우저 콘솔에 액세스 하려면 참조 [모니터링 전송](../getting-started/introduction-to-signalr.md#MonitoringTransports)합니다.

다음 스크린 샷에서 추적을 사용 하면서 SignalR JavaScript 클라이언트를 보여 줍니다. 브라우저 콘솔의 연결 및 허브 호출 이벤트를 나타냅니다.

![브라우저 콘솔에서 SignalR 추적 이벤트](enabling-signalr-tracing/_static/image4.png)
