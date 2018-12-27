---
uid: signalr/overview/performance/signalr-connection-density-testing-with-crank
title: SignalR 연결 밀도 크랭크를 사용 하 여 테스트 | Microsoft Docs
author: Rick-Anderson
description: SignalR 연결 밀도 크랭크를 사용 하 여 테스트
ms.author: riande
ms.date: 02/22/2015
ms.assetid: 148d9ca7-1af1-44b6-a9fb-91e261b9b463
msc.legacyurl: /signalr/overview/performance/signalr-connection-density-testing-with-crank
msc.type: authoredcontent
ms.openlocfilehash: 308fed51953b085506488c5e0dda1ced9f4d09fb
ms.sourcegitcommit: 74e3be25ea37b5fc8b4b433b0b872547b4b99186
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53287584"
---
<a name="signalr-connection-density-testing-with-crank"></a>SignalR 연결 밀도 크랭크를 사용 하 여 테스트
====================
[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 크랭크 도구를 사용 하 여 여러 시뮬레이션 된 클라이언트를 사용 하 여 응용 프로그램을 테스트 하는 방법을 설명 합니다.


응용 프로그램 호스팅 환경 (중 하나는 Azure 웹 역할, IIS 또는 Owin을 사용 하 여 자체 호스팅)에서 실행 되 면 응용 프로그램의 높은 수준의 크랭크 도구를 사용 하 여 연결 밀도에 대 한 응답을 테스트할 수 있습니다. 인터넷 정보 서비스 (IIS) 서버를, Owin 호스트를 또는 Azure 웹 역할을 호스팅 환경 수 있습니다. (참고: 성능 카운터 하지 않으므로 Azure App Service Web Apps에서 사용할 수 있는 연결 밀도 테스트에서 성능 데이터를 가져올 수 없습니다.)

연결 밀도 서버에 설정할 수 있는 동시 TCP 연결의 수를 나타냅니다. 자체 오버 헤드를 초래 하는 각 TCP 연결 및 많은 수의 유휴 연결을 열고 메모리 병목 상태가 최종적으로 만들어집니다.

[SignalR 코드 베이스](https://github.com/signalr/signalr) 부하 테스트 도구가 포함 **온난화**합니다. 크랭크의 최신 버전에서 찾을 수 있습니다 [Dev 분기](https://github.com/SignalR/signalr/tree/dev) github입니다. Zip 보관 SignalR의 개발 분기의 코드 베이스를 다운로드할 수 있습니다 [여기](https://github.com/SignalR/SignalR/archive/dev.zip)합니다.

크랭크 서버 하드웨어에 가능한 유휴 연결의 총 수를 계산 하기 위해 서버의 메모리를 완벽 하 게 포화를 사용할 수 있습니다. 또는 사용할 수도 있습니다 크랭크 부하 테스트 일정량의 메모리 압력을 아래에 있는 서버에서 특정 개수 또는 특정 메모리 임계값에 도달할 때까지 연결을 늘려 합니다.

테스트할 때 리소스 (예: TCP 연결 및 메모리)에 대 한 경쟁을 방지 하려면 원격 클라이언트를 사용 하는 것이 반드시 합니다. 서버 전체 용량 (메모리 또는 CPU)에 도달 하지 못하게 할 수 있는 병목 현상을 도달 하지는 되도록 클라이언트를 모니터링 합니다. 전체 서버를 로드 하기 위해 클라이언트의 수를 늘릴 해야 합니다.

### <a name="running-a-connection-density-test"></a>연결 밀도 테스트 실행

이 섹션에는 SignalR 응용 프로그램에서 연결 밀도 테스트를 실행 하는 데 필요한 단계를 설명 합니다.

1. 다운로드 및 빌드를 [SignalR의 개발 분기에 코드 베이스](https://github.com/SignalR/SignalR/archive/dev.zip)합니다. 명령 프롬프트에서로 이동 &lt;프로젝트 디렉터리&gt;\src\Microsoft.AspNet.SignalR.Crank\bin\debug 합니다.
2. 의도 한 호스팅 환경에 응용 프로그램을 배포 합니다. 응용 프로그램을 사용 하 여;는 끝점의 기록 만든 응용 프로그램의 예를 들어 합니다 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md), 끝점이 `http://<yourhost>:8080/signalr`합니다.
3. 설치할 [SignalR 성능 카운터](signalr-performance.md#perfcounters) 서버의 합니다. 응용 프로그램은 Azure에서 실행 하는 경우 참조 [Azure 웹 역할에서 SignalR 성능 카운터를 사용 하 여](using-signalr-performance-counters-in-an-azure-web-role.md)입니다.

다운로드 및 코드 베이스를 작성 하 고 호스트에서 성능 카운터를 설치 했으면, 크랭크 명령줄 도구에서 찾을 수 있습니다는 `src\Microsoft.AspNet.SignalR.Crank\bin\Debug` 폴더입니다.

크랭크 도구에 대 한 사용 가능한 옵션은 다음과 같습니다.

- **/?** : 도움말 화면을 보여 줍니다. 경우에 사용 가능한 옵션이 표시 됩니다는 **Url** 매개 변수를 생략 합니다.
- **/ Url**: SignalR 연결에 대 한 URL입니다. 이 매개 변수는 필수적 요소입니다. 기본 매핑을 사용 하 여 SignalR 응용 프로그램에 대 한 경로에 종료 됩니다 "/ signalr"입니다.
- **/ 전송**: 사용 되는 전송의 이름입니다. 기본값은 `auto`, 어떤 가장 사용 가능한 프로토콜 선택 됩니다. 옵션에 포함 됩니다 `WebSockets`, `ServerSentEvents`, 및 `LongPolling` (`ForeverFrame` 불가능 한 크랭크에 대 한.NET 클라이언트부터 Internet Explorer 사용 하는 것이 아니라). SignalR 전송을 선택 하는 방법에 대 한 자세한 내용은 참조 하세요. [전송과 대체](../getting-started/introduction-to-signalr.md#transports)합니다.
- **/ BatchSize**: 각 일괄 처리에 추가 하는 클라이언트의 수입니다. 기본값은 50입니다.
- **/ ConnectInterval**: 연결을 추가 하는 간격 (밀리초) 간격입니다. 기본값은 500입니다.
- **/ 연결**: 부하 테스트 응용 프로그램에 사용 되는 연결의 수입니다. 기본값은 100,000입니다.
- **/ ConnectTimeout**: 테스트를 중단 하기 전 시간 (초)의 제한 시간입니다. 기본값은 300입니다.
- **MinServerMBytes**: 연결할 최소 서버 메가바이트입니다. 기본값은 500입니다.
- **SendBytes**: 크기 (바이트)에서 서버에 전송 된 페이로드입니다. 기본값은 0입니다.
- **SendInterval**: 서버로 메시지를 밀리초 단위로 지연입니다. 기본값은 500입니다.
- **SendTimeout**: 서버에는 메시지에 대 한 밀리초 단위의 제한 시간입니다. 기본값은 300입니다.
- **ControllerUrl**: 클라이언트 컨트롤러 허브를 호스트 하는 Url입니다. 기본값은 null (컨트롤러 허브 없음). 크랭크 세션이 시작 되 면 컨트롤러 허브 시작 더 이상 크랭크 고 컨트롤러 hub 간의 연결이 됩니다.
- **NumClients**: 시뮬레이션 된 클라이언트 응용 프로그램에 연결할 수 있습니다. 기본값은 1입니다.
- **로그 파일**: 테스트 실행에 대 한 로그 파일에 대 한 파일 이름입니다. 기본값은 `crank.csv`입니다.
- **SampleInterval**: 성능 카운터 샘플 간격 (밀리초) 시간입니다. 기본값은 1000입니다.
- **SignalRInstance**: 서버에서 성능 카운터에 대 한 인스턴스 이름입니다. 기본은 클라이언트 연결 상태를 사용 하는 것입니다.

### <a name="example"></a>예제

다음 명령을 호출 하는 사이트를 테스트 합니다 `pfsignalr` "ControllerHub" 라는 허브를 사용 하 여 포트 8080에서 응용 프로그램을 호스트 하는 Azure에서 100 개의 연결을 사용 합니다.

`crank /Connections:100 /Url:http://pfsignalr.cloudapp.net:8080/signalr`
