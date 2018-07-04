---
uid: signalr/overview/performance/signalr-performance
title: SignalR 성능 | Microsoft Docs
author: pfletcher
description: SignalR 성능
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
ms.technology: dotnet-signalr
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: 9d032f84bbbc3ddb2e102cb37fd4d52ae5ef75c4
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388755"
---
<a name="signalr-performance"></a>SignalR 성능
====================
[Patrick Fletcher](https://github.com/pfletcher)

> 이 항목에 대 한 디자인, 측정 및 SignalR 응용 프로그램의 성능을 향상 하는 방법을 설명 합니다.
> 
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에서 사용 하는 소프트웨어 버전
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
> 이전 버전의 SignalR에 대 한 정보를 참조 하세요 [SignalR 이전 버전](../older-versions/index.md)합니다.
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이 있으면
> 
> 이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요. 에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


SignalR 성능 및 크기 조정에서 최근 프레젠테이션을 참조 하세요 [ASP.NET SignalR을 사용 하 여 실시간 웹 크기 조정](https://channel9.msdn.com/Events/Build/2013/3-502)합니다.

이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [디자인 고려 사항](#design)
- [SignalR 서버 성능 튜닝](#tuning)
- [성능 문제 해결](#troubleshooting)
- [SignalR 성능 카운터를 사용 하 여](#perfcounters)
- [다른 성능 카운터를 사용 하 여](#othercounters)
- [기타 리소스](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>디자인 고려 사항

이 섹션에서는 성능 불필요 한 네트워크 트래픽을 생성 하 여 하지 저하 되는 되도록 SignalR 응용 프로그램을 설계할 때 구현할 수 있는 패턴을 설명 합니다.

### <a name="throttling-message-frequency"></a>메시지 빈도 조정합니다.

(예: 실시간 게임 응용 프로그램)는 높은 빈도로 메시지를 전송 하는 응용 프로그램에도 대부분의 응용 프로그램을 두 번째로 많은 메시지를 보낼 필요가 없습니다. 각 클라이언트를 생성 하는 트래픽 용량을 줄이기 위해 메시지 루프를 구현할 수 있습니다 큐 및 보내는 아웃 보다 자주 고정된 요금 메시지는 (즉, 특정 개수의 메시지를 최대 보내집니다 매초에서 해당 시간에 메시지가 있는 경우 보낼 terval)입니다. (클라이언트 및 서버)에서 특정 속도로 메시지를 제한 하는 샘플 응용 프로그램을 참조 하세요 [SignalR 고주파수](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)합니다.

### <a name="reducing-message-size"></a>메시지 크기를 줄임으로써

Serialize 된 개체의 크기를 줄임으로써 SignalR 메시지의 크기를 줄일 수 있습니다. 서버 코드에서 전송할 필요가 없는 속성을 포함 하는 개체를 보내는 경우 방지 속성만 사용 하 여 serialize 되는 `JsonIgnore` 특성입니다. 속성의 이름은 메시지에도 저장 됩니다. 속성의 이름을 사용 하 여 줄일 수 있습니다는 `JsonProperty` 특성입니다. 다음 코드 샘플에는 클라이언트에 전송 되는 속성을 제외 하는 방법 및 속성 이름을 단축 하는 방법을 보여 줍니다.

**클라이언트에 전송 중인 데이터를 제외할 JsonIgnore 특성 및 메시지 크기를 줄이기 위해 JsonProperty 특성을 보여 주는.NET 서버 코드**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

가독성을 유지 하기 위해 / 클라이언트 코드에서 유지 관리를 약식된 속성 이름을 사람이 읽기 편한 매핑된 이름 메시지를 수신 합니다. 다음 코드 샘플을 보여 줍니다 (매핑), 메시지 계약을 정의 하 여 길이가 더 긴 약식된 이름 다시 매핑의 한 가지 방법을 사용 하는 `reMap` 계약 최적화 된 메시지 클래스에 적용할 함수입니다:

**클라이언트 쪽 JavaScript 코드가 다시 매핑하는 알기 쉬운 이름으로 속성 이름 단축**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

이름이 같은 메서드를 사용 하 여도 서버에 클라이언트에서 메시지에 줄일 수 있습니다.

메모리 사용 공간 (즉, 메시지에 사용 되는 메모리의 양)를 줄이고 메시지의 개체 성능을 향상할 수도 있습니다. 예를 들어 경우의 전체 범위는 `int` 필요 하지 않은 `short` 또는 `byte` 대신 사용할 수 있습니다.

메시지의 크기를 줄이면 서버 메모리에 메시지 버스에서 메시지 저장 되므로 서버 메모리 문제를 해결 수도 있습니다.

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>SignalR 서버 성능 튜닝

SignalR 응용 프로그램에서 성능 향상을 위해 서버를 튜닝 하려면 다음 구성 설정은 사용할 수 있습니다. ASP.NET 응용 프로그램에서 성능 향상 방법에 대 한 일반 정보를 참조 하세요 [ASP.NET 성능 향상](https://msdn.microsoft.com/library/ff647787.aspx)합니다.

**SignalR 구성 설정**

- **DefaultMessageBufferSize**: 기본적으로 SignalR 허브 연결당 당 메모리에 1000 개의 메시지를 유지 합니다. 큰 메시지를 사용 하는 경우이이 값을 줄여 완화할 수 있는 메모리 문제를 발생할 수 있습니다. 이 설정을 지정할 수 있습니다 합니다 `Application_Start` 또는 ASP.NET 응용 프로그램에서 이벤트 처리기는 `Configuration` 자체 호스팅된 응용 프로그램의 OWIN 시작 클래스의 메서드. 다음 샘플을 사용 하는 서버 메모리의 양을 줄이기 위해 응용 프로그램의 메모리 공간을 줄이기 위해이 값을 줄이는 방법을 보여 줍니다.

    **기본 메시지 버퍼 크기를 줄이는 것에 대 한 Startup.cs에서.NET 서버 코드**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**IIS 구성 설정**

- **응용 프로그램 당 최대 동시 요청**: 동시 IIS의 수를 늘리면 요청 증가 요청을 처리 하는 것에 대 한 사용 가능한 서버 리소스입니다. 기본값은 5000입니다. 이 설정을 늘릴, 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **ApplicationPool QueueLength**: 응용 프로그램 풀에 대 한 Http.sys 큐는 요청의 최대 수입니다. 큐 가득 차면 새 요청 503 "서비스를 사용할 수 없음" 응답을 수신 합니다. 기본값은 1000입니다.

    응용 프로그램을 호스팅하는 응용 프로그램 풀에서 작업자 프로세스에 대 한 큐 길이 줄이는 메모리 리소스가 절약 됩니다. 자세한 내용은 [관리, 튜닝, 및 응용 프로그램 풀 구성](https://technet.microsoft.com/library/cc745955.aspx)합니다.

**ASP.NET 구성 설정**

이 섹션에서는 구성 파일에서 설정할 수 있는 `aspnet.config` 파일입니다. 이 파일은 플랫폼에 따라 두 위치 중 하나에 있습니다.

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

SignalR 성능 향상 시킬 수 있는 ASP.NET 설정은 다음과 같습니다.

- **CPU 당 최대 동시 요청**:이 설정을 성능 병목 현상을 줄일 수 있습니다. 이 설정을 늘릴를 추가 하려면 다음 구성 설정을 `aspnet.config` 파일:

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **요청 큐 제한**: 총 연결 수를 초과 하는 경우는 `maxConcurrentRequestsPerCPU` 설정을 ASP.NET 요청 큐를 사용 하 여 제한을 시작 됩니다. 큐의 크기를 늘리려면 늘릴 수 있습니다는 `requestQueueLimit` 설정 합니다. 이 작업을 수행 하려면 다음 구성 설정을 추가 합니다 `processModel` 에 노드 `config/machine.config` (대신 `aspnet.config`):

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>성능 문제 해결

이 섹션에서는 응용 프로그램에서 성능 병목 지점을 찾는 방법을 설명 합니다.

### <a name="verifying-that-websocket-is-being-used"></a>WebSocket 사용 되 고 있는지 확인 합니다.

SignalR 클라이언트와 서버 간의 통신에 대 한 다양 한 전송 방식 사용할 수 있습니다, WebSocket 상당한 성능 이점이 클라이언트 및 서버를 지 원하는 경우에 사용 해야 합니다. 클라이언트 및 서버에 WebSocket에 대 한 요구 사항을 충족 하는 경우를 확인 하려면 참조 [전송과 대체](../getting-started/introduction-to-signalr.md#transports)합니다. 전송 되는 응용 프로그램을 확인 하려면 브라우저 개발자 도구를 사용할 수 있으며 로그 전송 연결에 사용 되는 검사 키를 누릅니다. Internet Explorer 및 Chrome 브라우저 개발 도구 사용에 대 한 자세한 내용은 [전송과 대체](../getting-started/introduction-to-signalr.md#transports)합니다.

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>SignalR 성능 카운터를 사용 하 여

이 섹션에서는 사용 하 여 SignalR 성능 카운터를 사용 하는 방법을 설명에 `Microsoft.AspNet.SignalR.Utils` 패키지 합니다.

### <a name="installing-signalrexe"></a>Signalr.exe 설치

성능 카운터 SignalR.exe 라는 유틸리티를 사용 하 여 서버에 추가할 수 있습니다. 이 유틸리티를 설치 하려면 다음이 단계를 수행 합니다.

1. Visual Studio 응용 프로그램에서 선택 **도구**하십시오 **라이브러리 패키지 관리자**, **솔루션용 NuGet 패키지 관리...**
2. 검색할 **signalr.utils**, 설치를 선택 합니다.

    ![](signalr-performance/_static/image1.png)
3. 패키지를 설치 하려면 사용권 계약에 동의 합니다.
4. SignalR.exe 되도록 설치 됩니다. `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`합니다.

### <a name="installing-performance-counters-with-signalrexe"></a>SignalR.exe를 사용 하 여 성능 카운터를 설치합니다.

SignalR 성능 카운터를 설치 하려면 다음 매개 변수를 사용 하 여 관리자 권한 명령 프롬프트에서 SignalR.exe를 실행 합니다.

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

SignalR 성능 카운터를 제거 하려면 다음 매개 변수를 사용 하 여 관리자 권한 명령 프롬프트에서 SignalR.exe를 실행 합니다.

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>SignalR 성능 카운터

유틸리티 패키지는 다음 성능 카운터를 설치합니다. 마지막 응용 프로그램 풀에 서버를 다시 시작한 이후 "전체" 카운터 이벤트 수를 측정 합니다.

**연결 메트릭**

다음 메트릭을 측정 연결 수명 이벤트를 발생 합니다. 자세한 내용은 [이해 하 고 연결 수명 이벤트 처리](../guide-to-the-api/handling-connection-lifetime-events.md)합니다.

- **연결 된 연결**
- **다시 연결**
- **연결이 끊긴 연결**
- **현재 연결**

**메시지 메트릭스**

다음 메트릭은 SignalR에서 생성 되는 메시지 트래픽을 측정 합니다.

- **총 받은 연결 메시지**
- **총 보낸 연결 메시지**
- **연결에 수신 메시지/초**
- **연결 메시지 전송 수/초**

**메시지 버스 메트릭**

다음 메트릭은 내부 SignalR 메시지 버스에 배치 되는 모든 들어오고 나가는 SignalR 메시지 큐를 통해 트래픽을 측정 합니다. 메시지가 **게시** 전송 되거나 브로드캐스트 경우. A **구독자** 이 컨텍스트에서 메시지 버스에서 구독, 클라이언트 및 서버 자체의 수는 같아야 합니다. **할당 된 작업자** 활성 연결;에 데이터를 전송 하는 구성 요소를 **바쁜 작업자** 메시지를 보내는 것입니다.

- **메시지 버스 받은 총 메시지 수**
- **메시지 버스 메시지 Received/Sec**
- **메시지 버스 메시지 총 게시**
- **메시지 버스에 게시 된 초당 메시지**
- **메시지 버스 구독자 현재**
- **메시지 버스에 대 한 구독자 총 수**
- **메시지 버스 구독자/Sec**
- **메시지 버스 작업자 할당**
- **메시지 버스 작업 중인 작업자**
- **메시지 버스 항목 현재**

**오차 메트릭**

다음 메트릭은 SignalR 메시지 트래픽에 의해 생성 된 오류를 측정 합니다. **허브 확인** 허브 또는 허브 메서드를 확인할 수 없는 경우 오류가 발생 합니다. **허브 호출** 오류는 허브 메서드를 호출 하는 동안 throw 된 예외입니다. **전송** 오류는 HTTP 요청 또는 응답 하는 동안 발생 하는 연결 오류입니다.

- **오류: 모든 합계**
- **오류: All/Sec**
- **오류: 허브 확인 합계**
- **오류: 허브 확인/Sec**
- **허브 호출 총 오류 수:**
- **오류: 허브 호출/Sec**
- **총 오류: 전송 수**
- **오류: 전송 수/초**

<a id="scaleout_metrics"></a>

**확장 메트릭**

다음 메트릭은 트래픽 및 확장 공급자에 의해 생성 된 오류를 측정 합니다. A **Stream** 이 컨텍스트에서 확장 공급자에서 사용 하는 배율 단위는이 테이블은 SQL Server를 사용 하는 경우, Service Bus를 사용 하면 토픽 및 구독 Redis 사용 되는 경우. 각 스트림 하면 정렬 된 읽기 및 쓰기 작업 단일 스트림을 잠재적 확장 병목 상태 이므로 해당 병목 상태를 줄일 수 있도록 스트림 수를 늘릴 수 있습니다. 여러 개의 스트림을 사용 하는 경우 SignalR 순서에서 지정된 된 연결에서 보낸 메시지를 확인 하는 방식으로 이러한 스트림에서 (분할) 메시지를 자동으로 배포 됩니다.

합니다 [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) 컨트롤 SignalR에서 유지 관리 확장 송신 큐의 길이 설정 합니다. 설정 값으로 0 모든 메시지가 한 번에 하나씩로 보내도록 구성 된를 메시징 백플레인으로 송신 큐에 배치 하는 보다 큰 합니다. 큐의 크기 구성 된 길이 초과, 하는 경우는 보내도록 후속 호출은 즉시 실패를 [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) 설정 보다 낮은 큐의 메시지 수가 될 때까지 다시 합니다. 큐는 구현 된 백플레인 일반적으로 있는 고유한 큐 또는 흐름 제어 하기 때문에 기본적으로 비활성화 됩니다. SQL Server의 경우 한 번에 진행 하는 전송 수를 제한 효과적으로 연결 풀링을 합니다.

기본적으로 SQL Server 및 Redis에 대 한 스트림이 하나만 되 고 Service Bus에 대 한 5 개의 스트림이 사용 되는, 큐를 사용 하지 않도록 설정 하며 SQL Server 및 Service Bus에 대 한 구성을 통해 이러한 설정을 변경할 수 있습니다.

**SQL Server 백플레인에 대 한 테이블 개수 및 큐 길이 구성 하는 것에 대 한.NET 서버 코드**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**Service Bus 백플레인에 대 한 항목 수 및 큐 길이 구성 하는 것에 대 한.NET 서버 코드**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

A **버퍼링** 스트림이 오류 상태가 된; 스트림이 오류 상태에 하는 경우를 백플레인에 보낸 모든 메시지 스트림을 더 이상 오류가 발생할 때까지 즉시 실패 합니다. 합니다 **전송 큐 길이** 게시 되었지만 아직 보내지 않은 메시지 수입니다.

- **확장 메시지 버스 메시지 Received/Sec**
- **확장 스트림 합계**
- **Scaleout 스트림 열기**
- **Scaleout 스트림 버퍼링**
- **총 확장 오류 수**
- **초당 확장 오류**
- **확장 송신 큐 길이**

이러한 카운터는 측정 되는 항목에 대 한 자세한 내용은 참조 하세요. [Azure Service Bus로 SignalR 규모 확장](scaleout-with-windows-azure-service-bus.md)합니다.

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>다른 성능 카운터를 사용 하 여

다음 성능 카운터는 응용 프로그램의 성능을 모니터링할 때 유용한 수도 있습니다.

**메모리**

- .NET CLR Memory\\모든 힙 (w3wp)에서 바이트

**ASP.NET**

- ASP.NET\Requests Current
- ASP.NET\Queued
- ASP.NET\Rejected

**CPU**

- 프로세서 Information\Processor 시간

**TCP/IP**

- TCPv6/연결 설정
- TCPv4/연결 설정

**웹 서비스**

- 웹 Connections
- 웹 Service\Maximum 연결

**스레딩**

- .NET CLR 잠금 및 스레드\\현재 논리 스레드
- .NET CLR 잠금 및 스레드\\현재 실제 스레드

<a id="otherresources"></a>

## <a name="other-resources"></a>기타 리소스

ASP.NET 성능 모니터링 및 튜닝에 대 한 자세한 내용은 다음 항목을 참조 하세요.

- [ASP.NET 성능 개요](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [IIS 7.5, IIS 7.0 및 IIS 6.0에서 ASP.NET 스레드 사용량](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;applicationPool&gt; 요소 (웹 설정)](https://msdn.microsoft.com/library/dd560842.aspx)
