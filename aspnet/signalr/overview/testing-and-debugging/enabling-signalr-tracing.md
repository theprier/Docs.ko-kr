---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: SignalR 추적 사용 | Microsoft Docs
author: bradygaster
description: 이 문서에 사용 하도록 설정 하 여 SignalR 서버 및 클라이언트에 대 한 추적을 구성 하는 방법을 설명 합니다. 추적을 사용 하면 이벤트에 대 한 진단 정보를 볼 수 있습니다...
ms.author: bradyg
ms.date: 08/08/2014
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: c6515e3653798ef50e2d2dcb7354ffed407a190e
ms.sourcegitcommit: ebf4e5a7ca301af8494edf64f85d4a8deb61d641
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54836469"
---
<a name="enabling-signalr-tracing"></a>SignalR 추적 사용
====================
[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에 사용 하도록 설정 하 여 SignalR 서버 및 클라이언트에 대 한 추적을 구성 하는 방법을 설명 합니다. 추적을 사용 하 여 SignalR 응용 프로그램에서 이벤트에 대 한 진단 정보를 볼 수 있습니다.
>
> 이 항목에서는 Patrick Fletcher 하 여 원래 작성 되었습니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET Framework 4.5
> - SignalR 버전 2
>
>
>
> ## <a name="questions-and-comments"></a>질문이 나 의견이 있으면
>
> 이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요. 에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


추적을 사용 하는 경우는 SignalR 응용 프로그램 이벤트 로그 항목을 만듭니다. 클라이언트와 서버 모두에서 이벤트를 기록할 수 있습니다. 서버 로그 연결, 확장 공급자 및 메시지 버스 이벤트를 추적 합니다. 클라이언트 로그 연결 이벤트에서 추적 합니다. SignalR 2.1 이상 버전에서는 추적 클라이언트 허브 호출 메시지의 전체 콘텐츠를 기록합니다.

## <a name="contents"></a>목차

- [서버에서 추적을 사용 하도록 설정](#server)

    - [텍스트 파일에 서버 이벤트를 기록합니다.](#server_text)
    - [서버 이벤트를 이벤트 로그에 로깅](#server_eventlog)
- [.NET 클라이언트 (Windows 데스크톱 앱)에서 추적을 사용 하도록 설정](#net_client)

    - [콘솔에 데스크톱 클라이언트 이벤트를 기록합니다.](#desktop_console)
    - [텍스트 파일에 데스크톱 클라이언트 이벤트를 기록합니다.](#desktop_text)
- [Windows Phone 8 클라이언트에서 추적을 사용 하도록 설정](#phone)

    - [UI에 Windows Phone 클라이언트 이벤트를 기록합니다.](#phone_ui)
    - [디버그 콘솔에 Windows Phone 클라이언트 이벤트를 기록합니다.](#phone_debug)
- [JavaScript 클라이언트에서 추적 사용](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a>서버에서 추적을 사용 하도록 설정

응용 프로그램의 구성 파일 (App.config 또는 Web.config 프로젝트의 유형에 따라.) 내에 서버에서 추적을 사용 하도록 설정 기록 하려는 이벤트 범주를 지정할 수 있습니다. 구성 파일에도 지정할 텍스트 파일, Windows 이벤트 로그의 구현을 사용 하 여 사용자 지정 로그에 이벤트를 기록할 것인지 [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx)합니다.

서버 이벤트 범주 메시지는 다음과를 같습니다.

| 소스 | 메시지 |
| --- | --- |
| SignalR.SqlMessageBus | SQL 메시지 버스 확장 공급자를 설치, 데이터베이스 작업, 오류 및 시간 제한 이벤트 |
| SignalR.ServiceBusMessageBus | Service bus 확장 공급자 항목 만들기 "및" 구독 "," error "및" 메시징 이벤트 |
| SignalR.RedisMessageBus | Redis 확장 공급자 연결, 연결 끊기 및 오류 이벤트 |
| SignalR.ScaleoutMessageBus | 메시징 이벤트 확장 |
| SignalR.Transports.WebSocketTransport | WebSocket 전송 연결, 연결 끊기, 메시징 및 오류 이벤트 |
| SignalR.Transports.ServerSentEventsTransport | ServerSentEvents 전송 연결, 연결 끊기, 메시징 및 오류 이벤트 |
| SignalR.Transports.ForeverFrameTransport | ForeverFrame 전송 연결, 연결 끊기, 메시징 및 오류 이벤트 |
| SignalR.Transports.LongPollingTransport | LongPolling 전송 연결, 연결 끊기, 메시징 및 오류 이벤트 |
| SignalR.Transports.TransportHeartBeat | 연결, 연결 끊기 및 keepalive 이벤트를 전송 합니다. |
| SignalR.ReflectedHubDescriptorProvider | 검색 이벤트 허브 |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a>텍스트 파일에 서버 이벤트를 기록합니다.

다음 코드에는 각 범주의 이벤트에 대 한 추적을 설정 하는 방법을 보여 줍니다. 이 샘플에서는 텍스트 파일에 이벤트를 기록 하도록 응용 프로그램을 구성 합니다.

**추적 사용에 대 한 XML 서버 코드**

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

위의 코드에서를 `SignalRSwitch` 항목을 지정 합니다 [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) 지정 된 로그로 전송 하는 이벤트에 대 한 사용. 이 경우 설정은 `Verbose` 즉, 디버깅 및 추적 메시지를 모두 기록 됩니다.

다음 출력에서는에서 항목을 `transports.log.txt` 위의 구성 파일을 사용 하 여 응용 프로그램에 대 한 파일입니다. 새 표시 연결, 연결을 제거 및 하트 비트 이벤트를 전송 합니다.

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a>서버 이벤트를 이벤트 로그에 로깅

텍스트 파일이 아닌 이벤트 로그에 이벤트를 기록할 항목에 대 한 값을 변경 합니다 `sharedListeners` 노드. 다음 코드에는 서버 이벤트를 이벤트 로그를 기록 하는 방법을 보여 줍니다.

**이벤트 로그에 로깅 이벤트에 대 한 XML 서버 코드**

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

이벤트를 응용 프로그램 로그에 기록 되 고 아래와 같이 이벤트 뷰어를 통해 사용할 수 있습니다:

![SignalR 로그를 표시 하는 이벤트 뷰어](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> 이벤트 로그를 사용 하는 경우 설정 합니다 **TraceLevel** 에 **오류** 메시지 수를 관리할 수 있도록 합니다.

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a>.NET 클라이언트 (Windows 데스크톱 앱)에서 추적을 사용 하도록 설정

.NET 클라이언트는 콘솔에 텍스트 파일 또는 구현을 사용 하는 사용자 지정 로그에 이벤트를 기록할 수 있습니다 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)합니다.

.NET 클라이언트 로그인을 사용 하려면 연결의 설정 `TraceLevel` 속성을 [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) 값 및 `TraceWriter` 속성을 유효한 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) 인스턴스.

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a>콘솔에 데스크톱 클라이언트 이벤트를 기록합니다.

다음 C# 코드에는.NET 클라이언트 콘솔에 이벤트를 기록 하는 방법을 보여 줍니다.

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a>텍스트 파일에 데스크톱 클라이언트 이벤트를 기록합니다.

다음 C# 코드를 텍스트 파일에.NET 클라이언트에서 이벤트를 기록 하는 방법을 보여 줍니다.

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

다음 출력에서는에서 항목을 `ClientLog.txt` 위의 구성 파일을 사용 하 여 응용 프로그램에 대 한 파일입니다. 서버에 연결 하는 클라이언트 표시 하 고 클라이언트 메서드를 호출 하는 허브 라는 `addMessage`:

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a>Windows Phone 8 클라이언트에서 추적을 사용 하도록 설정

Windows Phone 앱 용 SignalR 응용 프로그램 같은.NET 클라이언트를 사용 하 여 데스크톱 앱으로 하지만 [Console.Out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) 사용 하 여 파일에 쓰고 [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) 를 사용할 수 없습니다. 사용자 지정 구현을 생성 해야 하는 대신 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) 추적 합니다.

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a>UI에 Windows Phone 클라이언트 이벤트를 기록합니다.

[SignalR 코드 베이스](https://github.com/SignalR/SignalR/archive/master.zip) 추적 출력을 기록 하는 Windows Phone 샘플을 포함 한 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 사용자 지정을 사용 하 여 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) 구현을 호출 `TextBlockWriter`. 이 클래스에서 찾을 수 있습니다 합니다 **samples/Microsoft.AspNet.SignalR.Client.WP8.Samples** 프로젝트입니다. 인스턴스를 만들 때 `TextBlockWriter`, 현재 전달 [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx), 및 [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) 만들어집니다 위치를 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 추적에 사용할 출력:

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

추적 출력을 새 기록 되도록 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 에서 만든 합니다 [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) 에 전달 합니다.

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a>디버그 콘솔에 Windows Phone 클라이언트 이벤트를 기록합니다.

구현을 만드는 UI 보다 디버그 콘솔에 출력을 보내도록 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) 디버그 창에 기록 하 고 연결에 할당할 [TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) 속성:

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

Visual Studio의 디버그 창에 추적 정보 기록 되도록 합니다.

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a>JavaScript 클라이언트에서 추적 사용

클라이언트 쪽에서 로깅을 사용 하도록 연결을 설정 합니다 `logging` 를 호출 하기 전에 연결 개체의 속성을 `start` 연결을 설정 하는 방법.

**(사용 하 여 생성된 된 프록시) 브라우저 콘솔에 대 한 추적을 사용 하도록 설정 하는 것에 대 한 클라이언트 JavaScript 코드**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

**생성된 된 프록시) (없이 브라우저 콘솔에 대 한 추적을 사용 하도록 설정 하는 것에 대 한 클라이언트 JavaScript 코드**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

추적을 사용 하는 경우 JavaScript 클라이언트 브라우저 콘솔에 이벤트를 기록 합니다. 브라우저 콘솔에 액세스 하려면 참조 [전송 모니터링](../getting-started/introduction-to-signalr.md#MonitoringTransports)합니다.

다음 스크린 샷에서 추적 기능이 활성화 된 SignalR JavaScript 클라이언트를 보여 줍니다. 브라우저 콘솔에서 연결 및 허브 호출 이벤트를 보여줍니다.

![브라우저 콘솔에서 SignalR 추적 이벤트](enabling-signalr-tracing/_static/image4.png)
