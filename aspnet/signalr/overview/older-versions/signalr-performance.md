---
uid: signalr/overview/older-versions/signalr-performance
title: "SignalR 성능 (SignalR 1.x) | Microsoft Docs"
author: pfletcher
description: "SignalR 성능"
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/03/2013
ms.topic: article
ms.assetid: 9594d644-66b6-4223-acdd-23e29a6e4c46
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: bad742af28d6c36bb1b66207c2ba09d140332449
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="signalr-performance-signalr-1x"></a>SignalR 성능 (SignalR 1.x)
====================
으로 [Patrick Fletcher](https://github.com/pfletcher)

> 이 항목에 대 한 디자인 하 고 정확한 SignalR 응용 프로그램의 성능을 향상 하는 방법을 설명 합니다.


SignalR 성능 및 확장성에 최근 프레젠테이션용 참조 [SignalR로 실시간 웹 크기 조정](https://channel9.msdn.com/Events/Build/2013/3-502)합니다.

이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [디자인 고려 사항](#design)
- [SignalR 서버 성능을 튜닝](#tuning)
- [성능 문제 해결](#troubleshooting)
- [SignalR 성능 카운터를 사용 하 여](#perfcounters)
- [다른 성능 카운터를 사용 하 여](#othercounters)
- [기타 리소스](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>디자인 고려 사항

이 섹션에 성능 불필요 한 네트워크 트래픽이 생성 하 여 저하 되 고 있지은 되도록 SignalR 응용 프로그램을 디자인 하는 동안 구현할 수 있는 패턴에 설명 합니다.

### <a name="throttling-message-frequency"></a>메시지 빈도 조정합니다.

높은 주파수 (예: 실시간 게임 응용 프로그램)에서 메시지를 전송 하는 응용 프로그램에도 대부분의 응용 프로그램을 두 번째로 많은 메시지를 보낼 필요가 없습니다. 각 클라이언트에서 생성 되는 트래픽 용량을 줄이기 위해 메시지 루프를 구현할 수 있습니다 큐 및 보냅니다. 고정된 속도 보다 자주 더 이상 메시지가 있는지 (즉, 특정 메시지의 수로 전송 되지 않음 1 초 마다 해당 시간에 메시지가 있을 경우 전송 terval)입니다. (클라이언트 및 서버)에서 특정 속도로 메시지를 제한 하는 샘플 응용 프로그램에 대 한 참조 [SignalR과 높은 주파수 실시간](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)합니다.

### <a name="reducing-message-size"></a>메시지 크기 감소

Serialize 된 개체의 크기를 줄여 SignalR 메시지의 크기를 줄일 수 있습니다. 서버 코드에서 전송 될 필요가 없는 속성을 포함 하는 개체를 보내는 경우 되지 않도록 해당 속성에서 사용 하 여 serialize 되는 `JsonIgnore` 특성입니다. 속성의 이름은 메시지;에 저장 속성의 이름을 사용 하 여 단축할 수는 `JsonProperty` 특성입니다. 다음 코드 샘플을 클라이언트로 보낼 속성을 제외 하는 방법과 속성 이름을 단축 하는 방법을 보여 줍니다.

**데이터를 제외 하도록 클라이언트에 전송 되지 JsonIgnore 특성 및 메시지 크기를 줄이는 JsonProperty 특성을 보여 주는.NET 서버 코드**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

가독성을 유지 하기 위해 클라이언트 코드에서 관리의 용이성, 약식된 속성 이름은 이름일 수도 있습니다 사람이 친화적인에 매핑이 변경 메시지를 받은 후 / 합니다. 다음 코드 예제에서는 메시지 계약 (매핑)을 정의 하 여 긴 프로토콜로 약식된 이름을 다시 매핑의 한 가지 방법을 사용 하 고는 `reMap` 계약 최적화 된 메시지 클래스에 적용할 함수:

**다시 매핑하는 클라이언트 쪽 JavaScript 코드를 이해 하기 쉬운 이름 속성 이름 단축**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

이름은 동일한 방법을 사용 하 여도 서버에 클라이언트에서 메시지에 단축 될 수 있습니다.

(즉, 메시지에 사용 된 메모리의 양)에 메모리 사용 공간 감소 메시지의 개체도 성능을 향상 시킬 수 있습니다. 예를 들어 경우의 전체 범위는 `int` 필요 하지 않은 한 `short` 또는 `byte` 대신 사용할 수 있습니다.

메시지는 메시지의 크기를 줄이면 서버 메모리의 메시지 버스에 저장 되므로 서버 메모리 문제를 해결 수도 있습니다.

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>SignalR 서버 성능을 튜닝

다음 구성 설정은 SignalR 응용 프로그램에서 성능 향상을 위해 서버 조정할 데 사용할 수 있습니다. ASP.NET 응용 프로그램의 성능을 향상 하는 방법에 대 한 일반적인 정보를 참조 하십시오. [ASP.NET 성능 향상](https://msdn.microsoft.com/library/ff647787.aspx)합니다.

**SignalR 구성 설정**

- **DefaultMessageBufferSize**: 기본적으로 SignalR 허브 연결당 당 메모리에서 1000 메시지를 유지 합니다. 큰 메시지를 사용 하는 경우 이렇게이 값을 감소 시켜 용량을 줄일 수 있는 메모리 문제를 만들 수 있습니다. 이 설정을 설정할 수는 `Application_Start` 또는 ASP.NET 응용 프로그램에서 이벤트 처리기는 `Configuration` 자체 호스팅된 응용 프로그램에는 OWIN 시작 클래스의 메서드. 다음 샘플에 사용 되는 서버 메모리의 양을 줄이기 위해 응용 프로그램의 메모리 사용 공간을 최소화 하기 위해이 값을 줄이는 방법을 보여 줍니다.

    **기본 메시지 버퍼 크기를 줄이면에 대 한 Global.asax에.NET 서버 코드**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**IIS 구성 설정**

- **응용 프로그램 당 최대 동시 요청**: 동시 IIS의 수를 늘리면 요청 늘어납니다 서버 리소스의 요청 처리에 사용할 수 있습니다. 기본값은 5000입니다. 이 설정의 늘리려면 다음 명령을 관리자 권한 명령 프롬프트를 실행 합니다.

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]

**ASP.NET 구성 설정**

이 섹션에서 설정할 수 있는 구성 설정에는 `aspnet.config` 파일입니다. 이 파일은 플랫폼에 따라 다음 두 위치 중 하나에 있습니다.

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

SignalR 성능이 향상 될 수 있는 ASP.NET 설정은 다음과 같습니다.

- **CPU 당 최대 동시 요청**:이 설정을 성능 병목 현상을 줄일 수 있습니다. 이 설정을 늘릴,에 다음 구성 설정을 추가 `aspnet.config` 파일:

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **요청 큐 제한**: 총 연결 수 초과 하는 경우는 `maxConcurrentRequestsPerCPU` 설정, ASP.NET 요청 큐를 사용 하 여 시작 됩니다. 큐의 크기를 늘리려면 늘릴 수 있습니다는 `requestQueueLimit` 설정 합니다. 이 수행 하려면에 다음 구성 설정을 추가 `processModel` 노드에서 `config/machine.config` (대신 `aspnet.config`):

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>성능 문제 해결

이 섹션에서는 응용 프로그램에서 성능 병목 상태를 발견 하는 방법을 설명 합니다.

### <a name="verifying-that-websocket-is-being-used"></a>WebSocket이 사용 되 고 있는지 확인 하는 중

SignalR를 사용할 수 있지만 다양 한 전송 방식 클라이언트와 서버 간의 통신에 대 한 WebSocket 뛰어난 성공을 제공 하 고 클라이언트와 서버에서 지 원하는 경우 사용 해야 합니다. 클라이언트와 서버 WebSocket에 대 한 요구 사항을 충족 하는 경우를 확인 하려면 참조 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports)합니다. 어떤 전송을 응용 프로그램에서 사용량을 확인 하려면 브라우저 개발자 도구를 사용할 수 있으며 어떤 전송을 연결에 사용 되는지 확인 하려면 로그를 검사 키를 누릅니다. Internet Explorer 및 Chrome 브라우저 개발 도구를 사용 하는 방법은 참조 하십시오. [전송 및 대체](../getting-started/introduction-to-signalr.md#transports)합니다.

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>SignalR 성능 카운터를 사용 하 여

이 섹션에서는 SignalR 성능 카운터를 사용 하는 방법 설명에 `Microsoft.AspNet.SignalR.Utils` 패키지 합니다.

### <a name="installing-signalrexe"></a>Signalr.exe 설치

성능 카운터 SignalR.exe 라는 유틸리티를 사용 하 여 서버에 추가할 수 있습니다. 이 유틸리티를 설치 하려면 다음이 단계를 수행 합니다.

1. Visual Studio 응용 프로그램에서 선택 **도구**, **라이브러리 패키지 관리자**, **솔루션에 대 한 NuGet 패키지 관리...**
2. 검색할 **signalr.utils**, 설치를 선택 하 고 있습니다.

    ![](signalr-performance/_static/image1.png)
3. 패키지를 설치 하려면 사용권 계약에 동의 합니다.
4. SignalR.exe 되도록 설치 됩니다. `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`합니다.

### <a name="installing-performance-counters-with-signalrexe"></a>SignalR.exe와 성능 카운터를 설치합니다.

SignalR 성능 카운터를 설치 하려면 다음 매개 변수를 사용 하는 관리자 권한 명령 프롬프트에서 SignalR.exe를 실행 합니다.

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

SignalR 성능 카운터를 제거 하려면 다음 매개 변수를 사용 하는 관리자 권한 명령 프롬프트에서 SignalR.exe를 실행 합니다.

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>SignalR 성능 카운터

유틸리티도 패키지는 다음 성능 카운터를 설치합니다. "Total" 카운터는 마지막 응용 프로그램 풀 또는 서버를 다시 시작한 이후 이벤트의 수를 측정 합니다.

**연결 메트릭**

다음과 같은 메트릭이 발생 하는 연결 수명 이벤트를 측정 합니다. 자세한 내용은 참조 [이해 하 고 연결 수명 이벤트를 처리](../guide-to-the-api/handling-connection-lifetime-events.md)합니다.

- **연결 된 연결**
- **다시 연결 하는 연결**
- **연결 Disonnected**
- **현재 연결**

**메시지 메트릭스**

다음과 같은 메트릭이 SignalR에 의해 생성 된 메시지 트래픽을 측정 합니다.

- **총 받은 연결 메시지**
- **총 보낸 연결 메시지**
- **연결에 수신 메시지/초**
- **전송 연결 Messages/Sec**

**메시지 버스 메트릭**

다음 메트릭을 모든 들어오는 / 나가는 SignalR 메시지 사항이 큐는 내부 SignalR 메시지 버스를 통해 트래픽을 측정 합니다. 메시지는 **게시 됨** 전송 되거나 브로드캐스트 때. A **구독자** 이 컨텍스트에서 메시지 버스에서 구독;이 클라이언트와 서버 자체의 수와 같아야 합니다. **할당 된 작업자** 활성 연결;에 데이터를 전송 하는 구성 요소는 **사용 중인 작업자** 는 보내는 메시지입니다.

- **메시지 버스 받은 총 메시지**
- **메시지 버스 메시지 Received/Sec**
- **메시지 버스 메시지 게시 합계**
- **메시지 버스 Messages 게시/Sec**
- **메시지 버스 구독자 현재**
- **메시지 버스 구독자 합계**
- **메시지 버스 구독자/Sec**
- **메시지 버스 작업자를 할당 합니다.**
- **메시지 버스 근무 중인 노동자**
- **메시지 버스 항목 현재**

**오차 메트릭**

SignalR 메시지 트래픽에 의해 생성 된 오류를 측정 하는 다음 메트릭을 합니다. **허브 해상도** 허브 또는 허브 메서드를 확인할 수 없는 경우 오류가 발생 합니다. **허브 호출** 오류는 허브 메서드를 호출 하는 동안 발생 한 예외입니다. **전송** 오류는 연결 오류는 HTTP 요청 또는 응답 하는 동안 발생 합니다.

- **모든 총 오류 수:**
- **오류: All/Sec**
- **허브 해상도 총 오류 수:**
- **오류: 허브 해상도/초**
- **허브 호출 총 오류 수:**
- **오류: 허브 호출 수/초**
- **전송 총 오류 수:**
- **오류: 전송 수/초**

**확장 메트릭**

다음 메트릭을 트래픽과 확장 공급자에서 발생 한 오류를 측정 합니다. A **스트림** 이 컨텍스트에서이 확장 공급자에서 사용 하는 배율 단위에는이 SQL Server가 사용 하는 경우 테이블, 서비스 버스를 사용 하는 경우 항목 및 구독을 Redis 사용 되는 경우. 기본적으로 스트림을 하나만 사용 되지만이 SQL Server와 서비스 버스에서 구성을 통해 늘릴 수 있습니다. A **버퍼링** 스트림이 faulted 상태로 전환; 스트림이 faulted 상태가 즉시 스트림에 오류가 더 이상 될 때까지 백플레인에 보낸 모든 메시지가 실패 합니다. **전송 큐 길이** 게시 되었지만 아직 보내지 않은 메시지 수입니다.

- **확장 메시지 버스 메시지 Received/Sec**
- **확장 스트림 합계**
- **확장 스트림 열기**
- **확장 스트림 버퍼링**
- **확장 오류 합계**
- **초당 확장 오류**
- **확장 송신 큐 길이**

이러한 카운터를 측정 하는 기능에 대 한 자세한 내용은 참조 하십시오. [Azure 서비스 버스에 SignalR 확장](scaleout-with-windows-azure-service-bus.md)합니다.

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>다른 성능 카운터를 사용 하 여

다음 성능 카운터는 응용 프로그램의 성능 모니터링에 유용한 수도 있습니다.

**Memory**

- 전체 힙 (w3wp)의.NET CLR 메모리 # 바이트

**ASP.NET**

- ASP.NET\Requests Current
- ASP.NET\Queued
- ASP.NET\Rejected

**CPU**

- Processor Information\Processor Time

**TCP/IP**

- 설정 된 TCPv6/연결
- 설정 된 TCPv4/연결

**웹 서비스**

- 웹 Connections
- 웹 Service\Maximum 연결

**스레딩**

- .NET CLR LocksAndThreads\# 현재 논리 스레드
- .NET CLR LocksAnd 스레드\# 현재 실제 스레드

<a id="otherresources"></a>

## <a name="other-resources"></a>기타 리소스

ASP.NET 성능 모니터링 및 튜닝에 대 한 자세한 내용은 다음 항목을 참조 합니다.

- [ASP.NET 성능 개요](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [IIS 7.5, IIS 7.0 및 IIS 6.0에 ASP.NET 스레드 사용](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;applicationPool&gt; 요소 (웹 설정)](https://msdn.microsoft.com/library/dd560842.aspx)
