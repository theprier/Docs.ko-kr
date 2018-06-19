---
uid: signalr/overview/performance/signalr-connection-density-testing-with-crank
title: SignalR 연결 밀도 크랭크를 사용 하 여 테스트 | Microsoft Docs
author: tfitzmac
description: SignalR 연결 밀도 크랭크를 사용 하 여 테스트
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/22/2015
ms.topic: article
ms.assetid: 148d9ca7-1af1-44b6-a9fb-91e261b9b463
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/signalr-connection-density-testing-with-crank
msc.type: authoredcontent
ms.openlocfilehash: a3e8fdb47bd80d819358f9c48cd82fd51d6c0400
ms.sourcegitcommit: fe880bf4ed1c8116071c0e47c0babf3623b7f44a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
ms.locfileid: "26535332"
---
<a name="signalr-connection-density-testing-with-crank"></a>SignalR 연결 밀도 크랭크를 사용 하 여 테스트
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에는 시뮬레이션 된 여러 클라이언트에 응용 프로그램을 테스트 하려면 크랭크 도구를 사용 하는 방법을 설명 합니다.


응용 프로그램 (중 하나는 Azure 웹 역할, IIS, 또는 Owin를 사용 하 여 자체 호스트) 호스팅 환경에서 실행 하 고, 응용 프로그램의 높은 수준의 크랭크 도구를 사용 하 여 연결 밀도에 대 한 응답을 테스트할 수 있습니다. 인터넷 정보 서비스 (IIS) 서버는 Owin 호스트 또는 Azure 웹 역할에는 호스팅 환경 수 있습니다. (참고: 성능 카운터 Azure 앱 서비스 웹 앱에서 사용할 수 없는 때문 연결 밀도 테스트에서 성능 데이터를 가져올 수 없습니다.)

연결 밀도 서버에 설정할 수 있는 동시 TCP 연결의 수를 나타냅니다. 각 TCP 연결은 자체 오버 헤드를 초래 하 고 많은 수의 유휴 연결을 열어 메모리 병목 현상을 결국 만들어집니다.

[SignalR 코드 베이스](https://github.com/signalr/signalr) 부하 테스트 도구가 포함 **올릴**합니다. 에 최신 버전의 크랭크 있습니다 [Dev 분기](https://github.com/SignalR/signalr/tree/dev) GitHub에서 합니다. Zip 보관 파일에서 signalr Dev 분기의 코드 베이스를 다운로드할 수 있습니다 [여기](https://github.com/SignalR/SignalR/archive/dev.zip)합니다.

크랭크 서버 하드웨어에 가능한 유휴 연결의 총 수를 계산 하기 위해 서버에서 메모리를 완벽 하 게 포화를 사용할 수 있습니다. 또는 사용할 수도 있습니다 크랭크 부하 테스트 일정량의 메모리 부족 하 여 서버 특정 count 또는 특정 메모리 임계값에 도달할 때까지 연결을 램프 하 여 합니다.

을 테스트할 때에 리소스 (예: TCP 연결 및 메모리)에 대 한 경쟁을 방지 하려면 원격 클라이언트를 사용 해야 합니다. 서버 전체 용량 (메모리 또는 CPU)에 도달 하지 못하게 할 수 있는 병목 현상을 도달 하지는 되도록 클라이언트를 모니터링 합니다. 완전히 서버를 로드 하기 위해 클라이언트의 수를 늘려야 할 수 있습니다.

### <a name="running-a-connection-density-test"></a>연결 밀도 테스트 실행

이 섹션에서는 SignalR 응용 프로그램에서 연결 밀도 테스트를 실행 하는 데 필요한 단계를 설명 합니다.

1. 다운로드 하 고 빌드는 [SignalR의 Dev 분기에서 코드 베이스](https://github.com/SignalR/SignalR/archive/dev.zip)합니다. 명령 프롬프트에서로 이동 &lt;프로젝트 디렉터리&gt;\src\Microsoft.AspNet.SignalR.Crank\bin\debug 합니다.
2. 응용 프로그램 의도 한 호스팅 환경에 배포 합니다. 응용 프로그램을 사용 하 여; 끝점의 기록 예를 들어에서 만든 응용 프로그램에에서는 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md), 끝점은 `http://<yourhost>:8080/signalr`합니다.
3. 설치 [SignalR 성능 카운터](signalr-performance.md#perfcounters) 서버에 있습니다. 응용 프로그램이 Azure에서 실행 되는 경우 참조 [Azure 웹 역할에서 SignalR 성능 카운터를 사용 하 여](using-signalr-performance-counters-in-an-azure-web-role.md)합니다.

다운로드 하 고 하 고 코드를 작성 하 고, 호스트에서 성능 카운터를 설치 했으므로, 크랭크 명령줄 도구에서 확인할 수 있습니다는 `src\Microsoft.AspNet.SignalR.Crank\bin\Debug` 폴더입니다.

크랭크 도구에 대 한 사용 가능한 옵션은 다음과 같습니다.

- **/?** : 도움말 화면을 보여 줍니다. 경우에 사용할 수 있는 옵션이 표시 됩니다는 **Url** 매개 변수를 생략 합니다.
- **/ Url**: SignalR 연결에 대 한 URL입니다. 이 매개 변수는 필수적 요소입니다. 기본 매핑을 사용 하 여 SignalR 응용 프로그램에 대 한 경로에 종료 됩니다 "/ signalr"입니다.
- **/ 전송**: 사용 되는 전송의 이름입니다. 기본값은 `auto`, 어떤 가장 사용 가능한 프로토콜을 선택 합니다. 옵션 포함 `WebSockets`, `ServerSentEvents`, 및 `LongPolling` (`ForeverFrame` 이 불가능 크랭크에 대 한.NET 클라이언트 이후 Internet Explorer를 사용 하지 않고). SignalR 전송을 선택 하는 방법에 대 한 자세한 내용은 참조 하십시오. [전송 및 대체](../getting-started/introduction-to-signalr.md#transports)합니다.
- **/ BatchSize**: 각 일괄 처리에 추가 되는 클라이언트의 수입니다. 기본값은 50입니다.
- **/ ConnectInterval**: 연결을 추가 하는 간격 (밀리초) 간격입니다. 기본값은 500입니다.
- **/ 연결**: 부하 테스트 응용 프로그램에 사용 되는 연결의 수입니다. 기본값은 100, 000입니다.
- **/ ConnectTimeout**: 테스트를 중단 하기 전 시간 (초)의 제한 시간입니다. 기본값은 300입니다.
- **MinServerMBytes**: 최소 서버 메가바이트에 도달 합니다. 기본값은 500입니다.
- **SendBytes**: 바이트의 서버로 전송 된 페이로드 크기입니다. 기본값은 0입니다.
- **SendInterval**: 서버로 메시지를 사이의 밀리초의 지연 합니다. 기본값은 500입니다.
- **SendTimeout**: 서버에는 메시지에 대 한 밀리초 단위로 제한 시간입니다. 기본값은 300입니다.
- **ControllerUrl**: 하나의 클라이언트 컨트롤러 허브를 호스팅하는 Url입니다. 기본값은 null (컨트롤러 허브 제외). 크랭크 세션이 시작 되; 컨트롤러 허브 시작 더 이상 컨트롤러 허브와 크랭크 간의 이루어집니다.
- **NumClients**: 시뮬레이션 된 클라이언트 응용 프로그램에 연결할 수 있습니다. 기본값은 1입니다.
- **로그 파일**: 테스트 실행에 대 한 로그 파일에 대 한 파일 이름입니다. 기본값은 `crank.csv`입니다.
- **SampleInterval**: 성능 카운터 샘플 사이의 밀리초의 시간입니다. 기본값은 1000입니다.
- **SignalRInstance**: 서버에서 성능 카운터에 대 한 인스턴스 이름입니다. 기본값은 클라이언트 연결 상태를 사용 하는 것입니다.

### <a name="example"></a>예제

다음 명령은 이라고 하는 사이트를 테스트 합니다 `pfsignalr` 허브 "ControllerHub" 라는 포트 8080에서 응용 프로그램을 호스트 하는 Azure에서 100 개의 연결을 사용 하 여 합니다.

`crank /Connections:100 /Url:http://pfsignalr.cloudapp.net:8080/signalr`
