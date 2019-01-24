---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: '실습: SignalR 사용 하 여 실시간 웹 응용 프로그램 | Microsoft Docs'
author: bradygaster
description: 실시간 웹 응용 프로그램 기능을 실시간으로 발생 하는 대로 연결 된 클라이언트에 콘텐츠 서버 쪽을 푸시할 수 있습니다. ASP.NET 개발자에 게 ASP...
ms.author: bradyg
ms.date: 07/16/2014
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: d4998c8b739b4b1a06699a17464a7399a87a8595
ms.sourcegitcommit: ebf4e5a7ca301af8494edf64f85d4a8deb61d641
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54837509"
---
<a name="hands-on-lab-real-time-web-applications-with-signalr"></a>실습: SignalR 사용 하 여 실시간 웹 응용 프로그램
====================

[웹 캠프 팀](https://twitter.com/webcamps)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[웹 캠프 학습 키트 다운로드](http://aka.ms/webcamps-training-kit)

> 실시간 웹 응용 프로그램 기능을 실시간으로 발생 하는 대로 연결 된 클라이언트에 콘텐츠 서버 쪽을 푸시할 수 있습니다. ASP.NET 개발자에 게 **ASP.NET SignalR** 응용 프로그램에 실시간 웹 기능을 추가 하려면 라이브러리입니다. 이 여러 전송, 클라이언트 및 서버의 가장 사용 가능한 전송 가장 사용 가능한 전송 선택 하면 자동으로 활용 합니다. 활용 **WebSocket**, 브라우저와 서버 간의 양방향 통신을 사용 하도록 설정 하는 HTML5 API.
> 
> **SignalR** 클라이언트 RPC 서버 작업을 수행 하는 간단 하 고 상위 수준 API도 제공 (서버 쪽.NET 코드에서 클라이언트의 브라우저에서 JavaScript 함수 호출) 연결 관리에 대 한 유용한 후크 추가 뿐만 아니라 ASP.NET 응용 프로그램 연결/연결 끊기 이벤트, 연결 그룹화 및 권한 부여와 같은
> 
> **SignalR** 클라이언트와 서버 간의 실시간 작업을 수행 하는 데 필요한 전송의 몇 가지 추상화입니다. A **SignalR** 연결 HTTP로 시작 하 고 다음 수준으로 올린를 **WebSocket** 사용 가능한 경우 연결 합니다. **WebSocket** 에 대 한 이상적인 전송이 **SignalR**서버 메모리의 가장 효율적으로 사용 하기 때문에, 가장 낮은 대기 시간에이 있고 대부분의 기본 기능 (클라이언트 간의 전이중 통신 등 및 server), 하지만 가장 엄격한 요구 사항이 있습니다. **WebSocket** 서버를 사용 해야 **Windows Server 2012** 하거나 **Windows 8**를 함께 **.NET Framework 4.5**합니다. 이러한 요구 사항을 충족 되지 않는 경우 **SignalR** 와 연결을 확인 하려면 다른 전송을 사용 하려고 합니다 (같은 *긴 폴링 Ajax*).
> 
> 합니다 **SignalR** API 클라이언트와 서버 간의 통신을 위한 두 가지 모델을 포함 합니다. **영구 연결** 하 고 **Hubs**합니다. A **연결** -받는 사람, 단일 그룹화 보내거나 메시지를 브로드캐스트에 대 한 간단한 끝점을 나타냅니다. A **허브** 보다 높은 수준의 파이프라인 클라이언트 및 서버에서 서로 다른 메서드를 직접 호출할 수 있도록 연결 API를 기반으로 합니다.
> 
> ![SignalR 아키텍처](real-time-web-applications-with-signalr/_static/image1.png)
> 
> 웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)합니다.


<a id="Overview"></a>
## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 학습할 방법:

- 서버에서 SignalR을 사용 하 여 클라이언트 알림을 보냅니다.
- 사용 하 여 SignalR 응용 프로그램 확장 **SQL Server**합니다.

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

다음는이 실습을 완료 해야 합니다.

- [Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상

<a id="Setup"></a>
### <a name="setup"></a>설정

이 실습에서는 연습을 실행 하려면 먼저 환경 설정을 설정 해야 합니다.

1. Windows 탐색기 창을 열고 랩의 이동할 **원본** 폴더입니다.
2. 마우스 오른쪽 단추로 클릭 **Setup.cmd** 선택한 **관리자 권한으로 실행** 환경을 구성 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치는 설치 프로세스를 시작 합니다.
3. 사용자 계정 컨트롤 대화 상자를 표시 하는 경우 계속 하려면 작업을 확인 합니다.

> [!NOTE]
> 설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 선택 했는지 확인 합니다.


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>코드 조각 사용

랩 문서 전체에서 코드 블록을 삽입할 지시 됩니다. 사용자 편의 위해이 코드의 대부분은 수동으로 추가할 필요가 없도록 하려면 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.

> [!NOTE]
> 각 실습에 시작 솔루션을 함께 표시 됩니다는 **시작** 다른 독립적으로 각 연습에 따라 할 수 있는 연습 하는 폴더입니다. 주의 하십시오 연습 하는 동안 추가 되는 코드 조각은 솔루션부터 이러한 누락 되어 연습을 완료 될 때까지 작동 하지 않을 수 있습니다. 연습에 대 한 소스 코드 안에 있습니다.는 **최종** 해당 연습에서 단계를 완료 합니다. 결과로 생성 되는 코드를 사용 하 여 Visual Studio 솔루션에 포함 된 폴더입니다. 이 실습을 통해 작업 하는 동안 추가 도움이 필요한 경우 지침으로 이러한 솔루션을 사용할 수 있습니다.


* * *

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습에 포함 됩니다.

1. [SignalR을 사용 하 여 실시간 데이터 사용](#Exercise1)
2. [SQL Server를 사용 하 여 확장 합니다.](#Exercise2)

이 랩을 완료 하는 시간을 예상 합니다. **60 분**

> [!NOTE]
> Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션에는 특정 개발 스타일에 맞게 설계 되었습니다 및 창 레이아웃, 동작 편집기, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 랩의 절차에서는 사용 하는 경우 Visual Studio에서 지정된 된 태스크를 수행 하는 데 필요한 작업을 설명 합니다 **일반 개발 설정** 컬렉션입니다. 개발 환경에 대 한 다양 한 설정 컬렉션을 선택 하는 경우를 고려해 야 하는 단계에 차이가 있을 수 있습니다.


<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a>연습 1: SignalR을 사용 하 여 실시간 데이터 사용

예를 들어 채팅 흔히 하는 동안 전체를 수행할 수 있습니다 실시간 웹 기능을 사용 하 여 더 많은 합니다. 사용자를 새 데이터 또는 긴 폴링 새 데이터를 검색 하려면 Ajax 페이지 구현 하는 웹 페이지를 새로 고칩니다. 언제 든 지 SignalR을 사용할 수 있습니다.

SignalR을 지 원하는 **서버 푸시** 또는 **브로드캐스팅** 기능 연결 관리 자동으로 처리 합니다. 클라이언트-서버 통신에 대 한 클래식 HTTP 연결에서 각 요청에 대 한 연결이 다시 설정 하지만 SignalR 클라이언트와 서버 간에 영구 연결을 제공 합니다. 서버 코드를 원격 프로시저 호출 (RPC)을 사용 하 여 브라우저에서 클라이언트 코드를 호출 하는 signalr에서 요청-응답 모델 대신 알게 지금 합니다.

이 연습에서 구성한 합니다 **Geek 퀴즈** SignalR을 사용 하 여 전체 페이지를 새로 고칠 필요 없이 업데이트 된 메트릭 사용 하 여 통계 대시보드를 표시 하도록 응용 프로그램입니다.

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a>작업 1-Geek 퀴즈 통계 페이지 탐색

이 작업에서는 응용 프로그램을 통해 이동 되며 통계 페이지가 어떻게 표시 되는지 확인 하 고 서 정보를 개선 하는 방법을 업데이트 됩니다.

1. 엽니다 **Visual Studio Express 2013 for Web** 연 합니다 **GeekQuiz.sln** 솔루션을 **Source\Ex1 WorkingWithRealTimeData\Begin** 폴더.
2. 키를 눌러 **F5** 솔루션을 실행 합니다. 합니다 **로그인** 페이지가 브라우저에 표시 됩니다.

    ![솔루션을 실행](real-time-web-applications-with-signalr/_static/image2.png "솔루션 실행")

    *솔루션 실행*
3. 클릭 **등록** 응용 프로그램에서 새 사용자 페이지의 오른쪽 위 모퉁이에서.

    ![등록 링크](real-time-web-applications-with-signalr/_static/image3.png "등록 링크")

    *등록 링크*
4. 에 **등록** 페이지에서 입력을 **사용자 이름** 및 **암호**를 클릭 하 고 **등록**합니다.

    ![사용자 등록](real-time-web-applications-with-signalr/_static/image4.png "사용자 등록")

    *사용자 등록*
5. 응용 프로그램에 새 계정을 등록 하 고 사용자가 인증 하 고 첫 번째 퀴즈 질문을 보여 주는 홈 페이지로 다시 리디렉션됩니다.
6. 엽니다는 **통계** 넣은 새 창에서 페이지를 **홈** 페이지 및 **통계** side-by-side-페이지.

    ![Side-by-side-windows](real-time-web-applications-with-signalr/_static/image5.png "쪽 windows 쪽")

    *Side-by-side-windows*
7. 에 **홈** 페이지에서 옵션 중 하나를 클릭 하 여 질문에 대답 합니다.

    ![정보를 파악 하기가](real-time-web-applications-with-signalr/_static/image6.png "질문에 대답")

    *질문에 대답*
8. 단추 중 하나를 클릭 한 후 답변 표시 됩니다.

    ![올바른 질문에 대답할](real-time-web-applications-with-signalr/_static/image7.png "올바른 질문에 대답")

    *정확 하 게 대답 하는 질문*
9. 오래 된 통계 페이지에서 제공 하는 정보 인지 확인 합니다. 업데이트 된 결과 확인 하기 위해 페이지를 새로 고칩니다.

    ![통계 페이지가](real-time-web-applications-with-signalr/_static/image8.png "통계 페이지")

    *통계 페이지*
10. Visual Studio로 다시 이동 하 고 디버깅을 중지 합니다.

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a>작업 2-Geek 퀴즈 온라인 차트를 표시 하려면 추가 SignalR

이 태스크에서는 SignalR 솔루션에 추가 하 고 업데이트를 보내는 클라이언트에 자동으로 새 응답을 서버에 전송 될 때입니다.

1. **도구** Visual Studio에서 메뉴 **NuGet 패키지 관리자**를 클릭 하 고 **패키지 관리자 콘솔**합니다.
2. 에 **패키지 관리자 콘솔** 창에서 다음 명령을 실행 합니다.

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    ![SignalR 패키지 설치](real-time-web-applications-with-signalr/_static/image9.png "SignalR 패키지 설치")

    *SignalR 패키지 설치*

   > [!NOTE]
   > 설치할 때 **SignalR** 수동으로 업데이트 해야 새 MVC 5 응용 프로그램에서 NuGet 패키지 버전 2.0.2를 **OWIN** 버전 2.0.1 패키지 (또는 이상) SignalR을 설치 하기 전에 합니다. 이 작업을 수행 하려면 다음 스크립트를 실행할 수 있습니다 합니다 **패키지 관리자 콘솔**:
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > SignalR의 향후 릴리스에서 OWIN 종속성 자동으로 업데이트 됩니다.
3. **솔루션 탐색기**를 확장 합니다 **스크립트** 폴더 및 알림은 SignalR *js* 솔루션에 추가 된 파일이 합니다.

    ![SignalR JavaScript 참조](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript 참조")

    *SignalR JavaScript 참조*
4. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **GeekQuiz** 프로젝트를 **추가** | **새 폴더**, 이름을 **허브**합니다.
5. 마우스 오른쪽 단추로 클릭 합니다 **Hubs** 선택한 폴더 **추가 | 새 항목**합니다.

    ![새 항목 추가](real-time-web-applications-with-signalr/_static/image11.png "새 항목 추가")

    *새 항목 추가*
6. 에 **새 항목 추가** 대화 상자는 **Visual C# | 웹 | SignalR** 의 왼쪽된 창에서 노드 **SignalR 허브 클래스 (v2)** 가운데 창에서 파일 이름을 **StatisticsHub.cs** 누릅니다 **추가**합니다.

    ![새 항목 추가 대화 상자](real-time-web-applications-with-signalr/_static/image12.png "새 항목 추가 대화 상자")

    *새 항목 추가 대화 상자*
7. 코드를 대체 합니다 **StatisticsHub** 다음 코드를 사용 하 여 클래스입니다.

    (코드 조각- *RealTimeSignalR-e x 1-StatisticsHubClass*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. 오픈 **Startup.cs** 끝에 다음 줄을 추가 합니다 **구성** 메서드.

    (코드 조각- *RealTimeSignalR-e x 1-MapSignalR*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. 열기는 **StatisticsService.cs** 내에서 페이지를 **서비스** 폴더 추가한 다음 지시문을 사용 하 여 합니다.

    (코드 조각- *RealTimeSignalR-e x 1-UsingDirectives*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. 업데이트의 연결 된 클라이언트 알림 먼저 검색 한 **상황에 맞는** 현재 연결에 대 한 개체입니다. 합니다 **허브** 단일 클라이언트 또는 연결 된 모든 브로드캐스트 클라이언트에 메시지를 보내는 메서드를 포함 하는 개체입니다. 다음 메서드를 추가 합니다 **StatisticsService** 통계 데이터를 브로드캐스트하는 클래스입니다.

    (코드 조각- *RealTimeSignalR-e x 1-NotifyUpdatesMethod*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > 위의 코드에서 클라이언트에서 함수를 호출 하는 임의의 메서드 이름이 사용 중이거나 (예: *updateStatistics*). 지정 하는 메서드 이름에 대 한 컴파일 시간 유효성 검사 나 IntelliSense 즉 동적 개체로 해석 됩니다. 식은 런타임에 평가 됩니다. 메서드 호출이 실행 되 면 SignalR 메서드 이름과 매개 변수 값을 클라이언트에 보냅니다. 클라이언트 이름이 일치 하는 메서드가 있으면 해당 메서드가 호출 되 고 매개 변수 값에 전달 됩니다. 일치 하는 메서드가 없는 클라이언트에 있으면 오류가 발생 하지 않습니다. 자세한 내용은 참조 [ASP.NET SignalR 허브 API 가이드](../guide-to-the-api/hubs-api-guide-server.md)합니다.
11. 열기는 **TriviaController.cs** 내에서 페이지를 **컨트롤러** 폴더 추가한 다음 지시문을 사용 하 여 합니다.

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. 다음 강조 표시 된 코드를 추가 합니다 **Post** 작업 메서드.

    (코드 조각- *RealTimeSignalR-e x 1-NotifyUpdatesCall*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. 엽니다는 **Statistics.cshtml** 내에서 페이지를 **보기 | 홈** 폴더입니다. 찾을 합니다 **스크립트** 섹션 및 섹션의 시작 부분에 다음 스크립트 참조를 추가 합니다.

    (코드 조각- *RealTimeSignalR-e x 1-SignalRScriptReferences*)

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > SignalR 및 기타 스크립트 라이브러리를 Visual Studio 프로젝트에 추가 하면 패키지 관리자는이 항목에 표시 된 버전 보다 최신 SignalR 스크립트 파일의 버전을 설치할 수 있습니다. 코드에서 스크립트 참조를 프로젝트에 설치 스크립트 라이브러리의 버전과 일치 하는지 확인 합니다.
14. SignalR 허브에 클라이언트를 연결 하 고 허브에서 새 메시지를 받으면 통계 데이터를 업데이트 하려면 다음 강조 표시 된 코드를 추가 합니다.

    (코드 조각- *RealTimeSignalR-e x 1-SignalRClientCode*)

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    이 코드에서는 허브 프록시를 만들고 서버에서 보낸 메시지를 수신할 이벤트 처리기를 등록 합니다. 이 경우 메시지를 수신 대기를 통해 전송 합니다 *updateStatistics* 메서드.

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>작업 3 – 솔루션 실행

이 태스크에서는 자동으로 SignalR을 사용 하 여 새로운 질문에 답변 한 후 통계 보기 업데이트 되었는지 확인 하려면 솔루션을 실행 합니다.

1. 키를 눌러 **F5** 솔루션을 실행 합니다.

    > [!NOTE]
    > 아직 응용 프로그램에 로그인 하는 경우 작업 1에서 만든 사용자로 로그인 합니다.
2. 엽니다는 **통계** 넣은 새 창에서 페이지를 **홈** 페이지 및 **통계** 작업 1에서 수행한 것 처럼 side-by-side-페이지.
3. 에 **홈** 페이지에서 옵션 중 하나를 클릭 하 여 질문에 대답 합니다.

    ![다른 질문에 답하려면](real-time-web-applications-with-signalr/_static/image13.png "다른 질문에 답하려면")

    *다른 질문에 답*
4. 단추 중 하나를 클릭 한 후 답변 표시 됩니다. 알림 페이지의 통계 정보를 전체 페이지를 새로 고칠 필요 없이 업데이트 된 정보를 사용 하 여 질문에 답변 한 후 자동으로 업데이트 됩니다.

    ![응답 한 후 통계 페이지가 새로 고쳐지고](real-time-web-applications-with-signalr/_static/image14.png "응답 후 통계 페이지 새로 고침")

    *응답 한 후 새로 고침된 통계 페이지*

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a>연습 2: SQL Server를 사용 하 여 확장 합니다.

웹 응용 프로그램의 크기를 조정할 때 일반적으로 간에 선택할 수 있습니다 *강화* 하 고 *규모* 옵션입니다. *강화* 하는 동안 더 많은 리소스 (CPU, RAM, 등)를 사용 하 여 더 큰 서버를 사용 하 여 의미 *규모* 로드를 처리 하려면 더 많은 서버를 추가 하는 것입니다. 후자를 사용 하 여 문제를 다른 서버는 클라이언트 수 라우팅됩니다입니다. 하나의 서버에 연결 된 클라이언트에서 다른 서버에서 보낸 메시지를 받지 못합니다.

라는 구성 요소를 사용 하 여 이러한 문제를 해결할 수 있습니다 *백플레인*, 서버 간에 메시지를 전달 합니다. 활성화 백 블 레인에를 사용 하 여 각 응용 프로그램 인스턴스가 메시지를 백플레인에 보냅니다 및 백플레인에서 다른 응용 프로그램 인스턴스에 전달 합니다.

현재 세 가지 유형의 SignalR에 대 한 백플레인

- **Windows Azure Service Bus**합니다. Service Bus는 메시징 인프라를 통해 느슨하게 결합 된 메시지를 보내도록 구성 요소입니다.
- **SQL Server**. SQL Server 백플레인에서 SQL 테이블에 메시지를 씁니다. 백플레인에서 효율적인 메시징에 대 한 Service Broker를 사용합니다. 그러나 해당 Service Broker를 사용 하지 않는 경우에 작동 합니다.
- **Redis**합니다. Redis는 메모리 내 키-값 저장소입니다. Redis는 메시지를 보내기 위한 ("pub/sub") 게시/구독 패턴을 지원 합니다.

모든 메시지가 메시지 버스를 통해 전송 됩니다. 메시지 버스 구현 된 [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) 게시/구독 추상화를 제공 하는 인터페이스입니다. 기본 대체 하 여 작업의 백플레인 **IMessageBus** 해당 백플레인 위한 버스를 사용 하 여 합니다.

각 서버 인스턴스에 백플레인에서 버스를 통해 연결할 수 있습니다. 메시지를 보낼 때 백 블 레인에 이동 하 고 백플레인에서 모든 서버에 보냅니다. 서버 백플레인에서에서 메시지를 받으면 해당 로컬 캐시에서 메시지를 저장 합니다. 서버는 다음 로컬 캐시에서 클라이언트로 메시지를 배달합니다.

SignalR 백플레인으로 작동 원리,이 대 한 자세한 내용은 [문서](../performance/scaleout-in-signalr.md)합니다.

> [!NOTE]
> 가지를 백플레인으로 병목 현상이 발생할 수 있는 몇 가지 시나리오가 있습니다. 몇 가지 일반적인 SignalR 시나리오는 다음과 같습니다.
> 
> - [서버 브로드캐스트](tutorial-server-broadcast-with-signalr.md) (예: 주식 시세 표시기): 백플레인 서버 메시지가 전송 되는 속도 제어 하므로이 시나리오에 대 한 잘 작동 합니다.
> - [클라이언트-](tutorial-getting-started-with-signalr.md) (채팅 예): 이 시나리오에서는 클라이언트의 수를 사용 하 여 메시지 수가 조정 하는 경우 백플레인에서 병목 지점이 될 수 있습니다. 즉, 메시지의 속도 증가 함에 따라 비례적으로 더 많은 클라이언트 조인 합니다.
> - [고주파수](tutorial-high-frequency-realtime-with-signalr.md) (예: 실시간 게임): 이 시나리오를 백플레인으로 권장 되지 않습니다.


이 연습에서는 사용할지 **SQL Server** 간에 메시지를 분산 하는 **Geek 퀴즈** 응용 프로그램입니다. 전체 효과 얻기 위해 있지만 구성을 설정 하는 방법은 단일 테스트 컴퓨터에서 이러한 작업을 실행 하는, 두 개 이상의 서버에 SignalR 응용 프로그램을 배포 해야 합니다. 서버 중 하나에서 또는 별도 전용 서버에 SQL Server를 설치 해야 합니다.

![SQL Server 다이어그램을 사용 하 여 확장](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a>작업 1-시나리오 이해

이 태스크에서는 2 인스턴스의 실행될지 **Geek 퀴즈** 로컬 컴퓨터의 인스턴스를 여러 IIS를 시뮬레이션 합니다. 이 시나리오에서는 응용 프로그램에 대 한 기타 정보 질문 하는 경우, 업데이트는 두 번째 인스턴스의 통계 페이지에 알림이 표시 되지 않습니다. 이 시뮬레이션 유사한 여러 인스턴스에서 응용 프로그램을 배포 하는 위치 environment 부하 분산 장치를 사용 하 여 통신 하 합니다.

1. 엽니다는 **Begin.sln** 솔루션에는 **소스/e x 2-ScalingOutWithSQLServer/시작** 폴더입니다. 로드 되 면에서 알 수 있습니다 합니다 **서버 탐색기** 다른 이름을 구조 솔루션에 동일한 두 개의 프로젝트입니다. 이에서는 로컬 컴퓨터에서 동일한 응용 프로그램의 두 인스턴스 실행을 시뮬레이션 합니다.

    ![Geek 퀴즈의 2 개의 인스턴스를 시뮬레이션 솔루션 시작](real-time-web-applications-with-signalr/_static/image16.png "2 인스턴스의 Geek 퀴즈 시뮬레이션 솔루션 시작")

    *Geek 퀴즈의 2 개의 인스턴스를 시뮬레이션 솔루션 시작*
2. 솔루션 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 솔루션의 속성 페이지를 열려면 **속성**합니다. 아래 **시작 프로젝트**를 선택 **여러 개의 시작 프로젝트** 변경 하 고는 **작업** 두 프로젝트에 대 한 값 *시작*합니다.

    ![여러 프로젝트를 시작](real-time-web-applications-with-signalr/_static/image17.png "여러 프로젝트 시작")

    *여러 프로젝트 시작*
3. 키를 눌러 **F5** 솔루션을 실행 합니다. 응용 프로그램의 두 인스턴스가 시작 됩니다 **Geek 퀴즈** 서로 다른 포트에서 동일한 응용 프로그램의 여러 인스턴스를 시뮬레이션 합니다. 왼쪽 및 오른쪽 화면에 다른 브라우저 중 하나를 고정 합니다. 자격 증명으로 로그인 하거나 새 사용자를 등록 합니다. 일단 로그인 하면 왼쪽의 기타 정보 페이지를 유지 하 고로 이동 합니다 **통계** 오른쪽 브라우저의 페이지입니다.

    ![Geek 퀴즈 나란히](real-time-web-applications-with-signalr/_static/image18.png)

    *Geek 퀴즈 나란히*

    ![서로 다른 포트에서 geek 퀴즈](real-time-web-applications-with-signalr/_static/image19.png)

    *서로 다른 포트에서 geek 퀴즈*
4. 왼쪽된 브라우저에서 질문에 응답을 시작 하 고는 합니다 **통계** 오른쪽 브라우저에서 페이지 업데이트 되지 않습니다. 왜냐하면 **SignalR** 해당 클라이언트에 메시지를 분산 하는 로컬 캐시를 사용 하 여가이 시나리오는 여러 인스턴스를 시뮬레이션 하 고 따라서 캐시 간에 공유 되지 않습니다. 중인지 확인할 수 있습니다 **SignalR** 동일한 단계를 테스트 하지만 단일 앱을 사용 하 여 작동 합니다. 다음 태스크에서는 인스턴스 간에 메시지를 복제할 백플레인을 구성 합니다.
5. Visual Studio로 다시 이동 하 고 디버깅을 중지 합니다.

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a>작업 2-SQL Server 백플레인에서 만들기

이 작업에서는 데이터베이스에 대 한 백플레인으로 사용할 만들어집니다 합니다 **Geek 퀴즈** 응용 프로그램입니다. 사용할지 **SQL Server 개체 탐색기** 서버를 찾아보고 데이터베이스를 초기화 합니다. 또한를 사용 하도록 설정한 합니다 **Service Broker**합니다.

1. **Visual Studio**오픈 메뉴 **뷰** 선택한 **SQL Server 개체 탐색기**합니다.
2. 마우스 오른쪽 단추로 클릭 하 여 LocalDB 인스턴스에 연결 합니다 **SQL Server** 노드와 선택 **SQL Server 추가...**  옵션입니다.

    ![SQL Server 인스턴스를 추가](real-time-web-applications-with-signalr/_static/image20.png "SQL Server 인스턴스를 추가 합니다.")

    *SQL Server 인스턴스를 SQL Server 개체 탐색기에 추가*
3. 설정 합니다 **서버 이름** 하 *(localdb) \v11.0* 두고 **Windows 인증** 을 인증 모드로 합니다. 클릭 **Connect** 를 계속 합니다.

    ![LocalDB에 연결](real-time-web-applications-with-signalr/_static/image21.png "LocalDB에 연결")

    *LocalDB에 연결*
4. LocalDB 인스턴스를 연결한 했으므로 나타내는 SQL Server 백플레인에서 SignalR에 대 한 데이터베이스를 만들려고 해야 합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **데이터베이스** 노드와 선택 **새 데이터베이스 추가**합니다.

    ![새 데이터베이스 추가](real-time-web-applications-with-signalr/_static/image22.png "새 데이터베이스 추가")

    *새 데이터베이스 추가*
5. 데이터베이스 이름으로 설정 *SignalR* 클릭 **확인** 만들어야 합니다.

    ![SignalR 데이터베이스를 만드는](real-time-web-applications-with-signalr/_static/image23.png "SignalR 데이터베이스 만들기")

    *SignalR 데이터베이스 만들기*

    > [!NOTE]
    > 데이터베이스의 이름을 선택할 수 있습니다.
6. 백플레인에서 보다 효율적으로 업데이트를 받으려면, 데이터베이스에 대 한 Service Broker를 활성화 하는 것이 좋습니다. Service Broker는 메시징 및 SQL Server의 큐에 대 한 기본 지원을 제공 합니다. 백플레인에서는 Service Broker 없이 작동합니다. 선택한 데이터베이스를 마우스 오른쪽 단추로 클릭 하 여 새 쿼리를 엽니다 **새 쿼리**합니다.

    ![새 쿼리를 열어](real-time-web-applications-with-signalr/_static/image24.png "새 쿼리 열기")

    *새 쿼리 열기*
7. Service Broker 사용 되는지 여부를 확인, 쿼리를 **은\_broker\_사용 하도록 설정** 열에는 **sys.databases** 카탈로그 뷰. 최근에 열린된 쿼리 창에서 다음 스크립트를 실행 합니다.

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    ![Service Broker 상태를 쿼리할](real-time-web-applications-with-signalr/_static/image25.png "서비스 Broker 상태를 쿼리 합니다.")

    *Service Broker 상태를 쿼리합니다.*
8. 경우 값을 **은\_broker\_사용 하도록 설정** 데이터베이스의 열은 &quot;0&quot;, 사용 하도록 설정 하려면 다음 명령을 사용 합니다. 바꿉니다 **&lt;YOUR DATABASE&gt;** 데이터베이스를 만들 때 설정한 이름 (예: SignalR)입니다.

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    ![Service Broker를 사용 하도록 설정](real-time-web-applications-with-signalr/_static/image26.png "Service Broker를 사용 하도록 설정")

    *Service Broker를 사용 하도록 설정*

    > [!NOTE]
    > 교착 상태가 발생 했는지를이 쿼리가 나타납니다 경우 DB에 연결 하는 응용 프로그램이 없습니다.

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a>작업 3 – SignalR 응용 프로그램 구성

이 작업에서 구성한 **Geek 퀴즈** SQL Server 백플레인에서 연결할 합니다. 먼저 추가 합니다 **SignalR.SqlServer** 백플레인 데이터베이스에 NuGet 패키지 및 연결 집합 문자열입니다.

1. 엽니다는 **패키지 관리자 콘솔** 에서 **도구** > **NuGet 패키지 관리자**합니다. 했는지 **GeekQuiz** 에서 프로젝트를 선택 합니다 **기본 프로젝트** 드롭 다운 목록. 설치 하려면 다음 명령을 입력 합니다 **Microsoft.AspNet.SignalR.SqlServer** NuGet 패키지.

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. 프로젝트에 대해 이전 단계 이번 반복 **GeekQuiz2**합니다.
3. 구성 하려면 SQL Server 백플레인에서 엽니다는 **Startup.cs** 파일의는 **GeekQuiz** 프로젝트 및 다음 코드를 추가 합니다 **구성** 메서드. 바꿉니다 **&lt;YOUR DATABASE&gt;** SQL Server 백플레인에서 만들 때 사용한 데이터베이스 이름입니다. 이 단계를 반복 합니다 **GeekQuiz2** 프로젝트입니다.

    (코드 조각- *RealTimeSignalR-e x 2-StartupConfiguration*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. 키를 눌러 두 프로젝트는 SQL Server 백플레인에서 사용 하도록 구성 된, 했으므로 **F5** 동시에 실행할 수 있습니다.
5. 마찬가지로 **Visual Studio** 의 두 인스턴스가 시작 됩니다 **매니아 퀴즈** 서로 다른 포트에서. 왼쪽 및 오른쪽 화면에 다른 브라우저 중 하나를 고정 하 고 자격 증명으로 로그인 합니다. 왼쪽의 기타 정보 페이지를 유지 하 고 이동할 **통계** pagein 오른쪽 브라우저입니다.
6. 왼쪽된 브라우저에서 질문을 시작 합니다. 이 이번에는 **통계** 백플레인에서 덕분에 페이지를 업데이트 합니다. 응용 프로그램 간 전환 (**통계** 왼쪽에 이제 및 **퀴즈** 오른쪽에 표시 됩니다) 인스턴스 모두에 대해 작동 하는지 유효성을 검사 하려면 테스트를 반복 합니다. 백플레인에서 역할도 *캐시 공유* 연결 된 클라이언트에 배포 하는 자체 로컬 캐시에서 메시지 저장은 각 연결 된 서버 및 각 서버에 대 한 메시지입니다.
7. Visual Studio로 다시 이동 하 고 디버깅을 중지 합니다.
8. SQL Server 백플레인 구성 요소는 자동으로 지정된 된 데이터베이스에 필요한 테이블을 생성합니다. 에 **SQL Server 개체 탐색기** 패널에서 백플레인에서 대해 만든 데이터베이스를 엽니다 (예: SignalR) 해당 테이블을 확장 합니다. 다음 표에 표시 됩니다.

    ![백플레인에서 테이블 생성](real-time-web-applications-with-signalr/_static/image27.png)

    *백플레인에서 테이블 생성*
9. 마우스 오른쪽 단추로 클릭 합니다 **SignalR.Messages\_0** 선택한 테이블 **데이터 보기**합니다.

    ![SignalR 백플레인으로 메시지 테이블 보기](real-time-web-applications-with-signalr/_static/image28.png)

    *SignalR 백플레인으로 메시지 테이블 보기*
10. 전송할 다양 한 메시지를 볼 수는 **허브** 퀴즈 질문에 답변 하는 경우. 백플레인에서 연결 인스턴스에 이러한 메시지를 분산합니다.

    ![백플레인에서 메시지 테이블](real-time-web-applications-with-signalr/_static/image29.png)

    *백플레인에서 메시지 테이블*

* * *

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습에서는 추가 하는 방법을 익 혔 **SignalR** 사용 하 여 연결 된 클라이언트에 서버에서 응용 프로그램 및 송신 알림에 **Hubs**합니다. 사용 하 여 응용 프로그램을 확장 하는 방법과 또한을 *백플레인* 여러 IIS 인스턴스에 응용 프로그램을 배포할 때 구성 요소입니다.
