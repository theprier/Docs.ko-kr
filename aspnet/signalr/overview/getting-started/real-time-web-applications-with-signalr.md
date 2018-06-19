---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: '랩 관련 한 실질적인: SignalR과 실시간 웹 응용 프로그램 | Microsoft Docs'
author: rick-anderson
description: 실시간 웹 응용 프로그램 서버 쪽으로 실시간으로 발생 하는 대로 연결 된 클라이언트에 콘텐츠를 기능입니다. ASP는 ASP.NET 개발자를 위한...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/16/2014
ms.topic: article
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 5a2bc120ded18ad2302fd6c5cde65a5323e86ca8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30878050"
---
<a name="hands-on-lab-real-time-web-applications-with-signalr"></a>SignalR과 실습 랩: 실시간 웹 응용 프로그램
====================
으로 [웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트를 다운로드 합니다.](http://aka.ms/webcamps-training-kit)

> 실시간 웹 응용 프로그램 서버 쪽으로 실시간으로 발생 하는 대로 연결 된 클라이언트에 콘텐츠를 기능입니다. ASP.NET 개발자를 위한 **ASP.NET SignalR** 응용 프로그램에 실시간 웹 기능을 추가 하려면 라이브러리입니다. 이용할 여러 전송의 경우 클라이언트 및 서버의 가장 사용 가능한 전송 가장 사용 가능한 전송을 자동으로 선택 합니다. 에서는 활용 **WebSocket**, 브라우저와 서버 간의 양방향 통신을 허용 하는 HTML5 API입니다.
> 
> **SignalR** 클라이언트 RPC 서버를 수행 하는 데 간단 하 고 상위 수준 API를 제공 (서버 쪽.NET 코드에서 클라이언트의 브라우저에서 JavaScript 함수 호출) 연결 관리에 대 한 유용한 후크를 추가할 뿐 아니라 ASP.NET 응용 프로그램에서 같은 연결/연결 끊기 이벤트, 그룹화 연결 및 권한 부여 합니다.
> 
> **SignalR** 은 일부 클라이언트와 서버 간의 실시간 작업을 수행 하는 데 필요한 전송을 통한 추상화입니다. A **SignalR** 연결 HTTP로 시작 하 고 다음 수준으로 올린는 **WebSocket** 사용 가능한 경우 연결 합니다. **WebSocket** 는 대 한 이상적인 전송 **SignalR**이므로 서버 메모리의 가장 효율적으로 사용 하는 대기 시간이 가장 많고 가장 기본 기능 (클라이언트 간의 양방향 통신 등 및 서버)를 없지만 역시 가장 엄격한 요구 사항: **WebSocket** 서버 수를 사용 하 여를 **Windows Server 2012** 또는 **Windows 8**, 함께 **.NET framework 4.5**합니다. 이러한 요구 사항을 충족 되지 않는 경우 **SignalR** 다른 전송의 연결을 사용 하려고 합니다 (같은 *Ajax 긴 폴링과*).
> 
> **SignalR** 클라이언트와 서버 간의 통신을 위해 두 개의 모델을 포함 하는 API: **영구 연결** 및 **허브**합니다. A **연결** -받는 사람, 단일 그룹화를 보내거나 전체 메시지에 대 한 간단한 끝점을 나타냅니다. A **허브** 기반으로 클라이언트와 서버가 서로에서 메서드를 직접 호출할 수 있도록 연결 API 보다 높은 수준의 파이프라인.
> 
> ![SignalR 아키텍처](real-time-web-applications-with-signalr/_static/image1.png)
> 
> 모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)합니다.


<a id="Overview"></a>
## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 배웁니다 하는 방법:

- SignalR을 사용 하 여 클라이언트에 서버에서 알림을 보냅니다.
- 사용 하 여 SignalR 응용 프로그램 확장 **SQL Server**합니다.

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

다음은이 실습 랩을 완료 하려면 필요 합니다.

- [Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상

<a id="Setup"></a>
### <a name="setup"></a>설정

이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.

1. Windows 탐색기 창을 열고 다음을 찾아보기에 랩 **소스** 폴더입니다.
2. 마우스 오른쪽 단추로 클릭 **Setup.cmd** 선택 **관리자 권한으로 실행** 환경을 구성 되며이 랩에 대 한 Visual Studio 코드 조각을 설치 하는 설치 프로세스를 시작 합니다.
3. 사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.

> [!NOTE]
> 설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 선택 했는지 확인 합니다.


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>코드 조각을 사용 하 여

랩 문서를 통해 코드 블록을 삽입 하도록 합니다. 사용자 편의 위해이 코드의 대부분을 수동으로 추가할 필요가 없도록 하려면 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.

> [!NOTE]
> 각 연습에는 시작 솔루션 동반 되는 **시작** 개별적으로 각 연습에 따라 할 수 있는 작업의 폴더입니다. 주의 하십시오 연습 하는 동안 추가 된 코드 조각은 솔루션 시작이 항목에서 누락 되어 연습을 완료 될 때까지 작동 하지 않을 수 있습니다. 실행에 대 한 소스 코드에서 찾아볼 수 있습니다는 **끝** 해당 연습에서 단계를 완료 한 결과인 코드와 함께 Visual Studio 솔루션에 포함 된 폴더입니다. 이 실습 랩에서 진행할 때는 추가 도움이 필요한 경우 이러한 솔루션 가이드로 사용할 수 있습니다.


* * *

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습에 포함 됩니다.

1. [SignalR을 사용 하 여 실시간 데이터 사용](#Exercise1)
2. [SQL Server를 사용 하 여 확장 합니다.](#Exercise2)

예상 소요 시간: **60 분**

> [!NOTE]
> Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션 특정 개발 스타일에 맞게 설계 하 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 랩의 절차를 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업 설명에서 **일반 개발 설정** 컬렉션입니다. 개발 환경에 대 한 서로 다른 설정 컬렉션을 선택 하면 고려해 야 하는 단계에 차이가 있을 수 있습니다.


<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a>연습 1: SignalR을 사용 하 여 실시간 데이터 사용

채팅은 일반적으로 예를 들어 사용 되지만 할 수 있는 전체 실시간 웹 기능으로 추가 합니다. 사용자를 새 데이터 나 페이지 구현 Ajax 긴 폴링과 새 데이터를 검색 하는 웹 페이지를 새로 고칩니다. 언제 든 지 SignalR를 사용할 수 있습니다.

SignalR 지원 **서버 푸시** 또는 **브로드캐스트** 기능을 자동으로 연결 관리 처리 합니다. 클라이언트-서버 통신에 대 한 기본 HTTP 연결에서 연결이 각 요청에 대 한 다시 설정 하지만 SignalR 클라이언트와 서버 간에 영구 연결을 제공 합니다. 서버 코드가 원격 프로시저 호출 (RPC)을 사용 하 여 브라우저에서 클라이언트 코드를 호출할 SignalR에서 요청-응답 모델 대신 알고 오늘 있습니다.

이 연습에서는 구성에서 **들은 퀴즈** 전체 페이지를 새로 고칠 하지 않고도 업데이트 된 메트릭 사용 하 여 통계 대시보드 표시 하려면 SignalR을 사용 하도록 응용 프로그램입니다.

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a>작업 1-들은 퀴즈 통계 페이지 탐색

이 태스크에서는 응용 프로그램을 통해 이동 하 고 통계 페이지가 어떻게 표시 되는지 확인 하십시오 됩니다 고 방식으로 정보를 개선 하는 방법을 업데이트 됩니다.

1. 열고 **Visual Studio Express 2013 for Web** 엽니다는 **GeekQuiz.sln** 솔루션에 있는 **Source\Ex1 WorkingWithRealTimeData\Begin** 폴더입니다.
2. 키를 눌러 **F5** 솔루션을 실행 합니다. **로그인** 페이지가 브라우저에 표시 됩니다.

    ![솔루션을 실행](real-time-web-applications-with-signalr/_static/image2.png "솔루션 실행")

    *솔루션을 실행*
3. 클릭 **등록** 사용자를 만들려면 새 응용 프로그램에서 페이지의 오른쪽 위 모퉁이에 있습니다.

    ![등록 링크](real-time-web-applications-with-signalr/_static/image3.png "레지스터 링크")

    *링크를 등록 합니다.*
4. 에 **등록** 페이지에서 입력 한 **사용자 이름** 및 **암호**, 클릭 하 고 **등록**합니다.

    ![사용자 등록](real-time-web-applications-with-signalr/_static/image4.png "사용자 등록")

    *사용자 등록*
5. 응용 프로그램에서 새 계정을 등록 하 고 사용자가 인증 되 고 첫 번째 퀴즈 질문을 보여 주는 홈 페이지로 다시 리디렉션되 며 합니다.
6. 열기는 **통계** 넣은 새 창에서 페이지는 **홈** 페이지 및 **통계** -나란히 페이지입니다.

    ![Side-by-side-windows](real-time-web-applications-with-signalr/_static/image5.png "측 windows 쪽")

    *Side-by-side-windows*
7. 에 **홈** 페이지에서 옵션 중 하나를 클릭 하 여 응답 합니다.

    ![질문에 대답](real-time-web-applications-with-signalr/_static/image6.png "질문에 대답")

    *질문에 대답*
8. 단추 중 하나를 클릭 한 후에 대답 나타나야 합니다.

    ![질문에 대답할 올바른](real-time-web-applications-with-signalr/_static/image7.png "질문에 대답할 올바른")

    *올바르게 대답 질문*
9. 오래 된 통계 페이지에 제공 된 정보를 확인 합니다. 업데이트 된 결과 확인 하기 위해 페이지를 새로 고칩니다.

    ![통계 페이지](real-time-web-applications-with-signalr/_static/image8.png "통계 페이지")

    *통계 페이지*
10. Visual Studio로 다시 이동 하 고 디버깅을 중지 합니다.

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a>작업 2-온라인 차트를 표시 하 게 퀴즈를 추가 SignalR

이 태스크에서는 SignalR 솔루션에 추가 하 고 때 업데이트 전송 되는 클라이언트에 자동으로 새 응답을 서버에 전송 됩니다.

1. **도구** 선택 Visual Studio에서 메뉴 **라이브러리 패키지 관리자**, 클릭 하 고 **패키지 관리자 콘솔**합니다.
2. 에 **패키지 관리자 콘솔** 창에서 다음 명령을 실행 합니다.

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    ![SignalR 패키지 설치](real-time-web-applications-with-signalr/_static/image9.png "SignalR 패키지 설치")

    *SignalR 패키지 설치*

   > [!NOTE]
   > 설치할 때 **SignalR** 를 수동으로 업데이트 해야 합니다는 완전히 새로운 MVC 5 응용 프로그램에서 NuGet 패키지 버전 2.0.2, **OWIN** 버전 2.0.1 패키지 (또는 이상) SignalR을 설치 하기 전에. 이 작업을 수행 하려면 다음 스크립트를 실행할 수 있습니다는 **패키지 관리자 콘솔**:
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > SignalR의 이후 릴리스에서 OWIN 종속성 자동으로 업데이트 됩니다.
3. **솔루션 탐색기**, 확장는 **스크립트** 폴더 및 표시 하는 SignalR *js* 솔루션에 추가 된 파일이 있습니다.

    ![SignalR JavaScript 참조](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript 참조")

    *SignalR JavaScript 참조*
4. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **GeekQuiz** 프로젝트를 **추가** | **새 폴더**, 고 이름을 **허브**합니다.
5. 마우스 오른쪽 단추로 클릭는 **허브** 폴더를 선택 **추가 | 새 항목**합니다.

    ![새 항목 추가](real-time-web-applications-with-signalr/_static/image11.png "새 항목 추가")

    *새 항목 추가*
6. 에 **새 항목 추가** 대화 상자는 **Visual C# | 웹 | SignalR** 선택 왼쪽된 창에서 노드 **SignalR 허브 클래스 (v2)** 가운데 창에서 파일 이름을 **StatisticsHub.cs** 클릭 **추가**합니다.

    ![새 항목 추가 대화 상자](real-time-web-applications-with-signalr/_static/image12.png "새 항목 추가 대화 상자")

    *새 항목 추가 대화 상자*
7. 코드는 **StatisticsHub** 를 다음 코드로 클래스입니다.

    (코드 조각- *RealTimeSignalR e x-1-StatisticsHubClass*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. 열기 **Startup.cs** 에 다음 줄의 끝에 추가 하 고는 **구성** 메서드.

    (코드 조각- *RealTimeSignalR e x-1-MapSignalR*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. 열기는 **StatisticsService.cs** 내 페이지는 **서비스** 폴더 다음 추가 using 지시문을 사용 합니다.

    (코드 조각- *RealTimeSignalR e x-1-UsingDirectives*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. 업데이트의 연결 된 클라이언트에 알리려면를 먼저 검색 한 **컨텍스트** 현재 연결에 대 한 개체입니다. **허브** 개체 단일 클라이언트 또는 브로드캐스트를 연결 된 모든 클라이언트에 메시지를 보낼 메서드가 포함 되어 있습니다. 다음 메서드를 추가 **StatisticsService** 통계 데이터를 클래스입니다.

    (코드 조각- *RealTimeSignalR e x-1-NotifyUpdatesMethod*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > 위의 코드에서 사용 하는 임의의 메서드 이름 클라이언트에서 함수를 호출할 수 (예:: *updateStatistics*). 메서드 이름은 지정 하는 의미 없는 IntelliSense 또는 컴파일 타임 유효성 검사에 대 한 동적 개체로 해석 됩니다. 식이 런타임 시 계산 됩니다. 메서드 호출이 실행 되 면 SignalR 메서드 이름과 매개 변수 값을 클라이언트로 보냅니다. 클라이언트에 있는 경우 메서드가 호출 되 고 매개 변수 값이 전달 되는 이름과 일치 하는 메서드. 메서드가 클라이언트에서 발견 되는 경우 오류가 발생 합니다. 자세한 내용은를 참조 [ASP.NET SignalR 허브 API 가이드](../guide-to-the-api/hubs-api-guide-server.md)합니다.
11. 열기는 **TriviaController.cs** 내 페이지는 **컨트롤러** 폴더 다음 추가 using 지시문을 사용 합니다.

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. 다음 강조 표시 된 코드를 추가 하는 **Post** 동작 메서드.

    (코드 조각- *RealTimeSignalR e x-1-NotifyUpdatesCall*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. 열기는 **Statistics.cshtml** 내 페이지는 **보기 | 홈** 폴더입니다. 찾을 **스크립트** 섹션 및 섹션의 시작 부분에 다음 스크립트 참조를 추가 합니다.

    (코드 조각- *RealTimeSignalR e x-1-SignalRScriptReferences*)

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > SignalR 및 기타 스크립트 라이브러리를 Visual Studio 프로젝트에 추가 하면 패키지 관리자는이 항목에 표시 된 버전 보다 더 최신 SignalR 스크립트 파일의 버전을 설치 될 수 있습니다. 코드에서 스크립트 참조가 프로젝트에 설치 된 스크립트 라이브러리의 버전이 일치 하는지 확인 합니다.
14. SignalR 허브에 클라이언트를 연결 하 고 허브에서 새 메시지를 받으면 통계 데이터를 업데이트 하려면 다음 강조 표시 된 코드를 추가 합니다.

    (코드 조각- *RealTimeSignalR e x-1-SignalRClientCode*)

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    이 코드에서는 허브 프록시를 만드는 하는 서버에서 보낸 메시지를 수신할 이벤트 처리기를 등록 합니다. 통해 전송 된 메시지를 수신 하는 경우에 *updateStatistics* 메서드.

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>작업 3 – 솔루션 실행

이 태스크에서는 자동으로 SignalR을 사용 하 여 새 질문에 답변 한 후 통계 뷰가 업데이트 되어 있는지 확인 하려면 솔루션을 실행 합니다.

1. 키를 눌러 **F5** 솔루션을 실행 합니다.

    > [!NOTE]
    > 아직 응용 프로그램에 로그인 하는 경우 작업 1에서 만든 사용자를 로그인 합니다.
2. 열기는 **통계** 넣은 새 창에서 페이지는 **홈** 페이지 및 **통계** 작업 1에서와 같이-나란히 페이지입니다.
3. 에 **홈** 페이지에서 옵션 중 하나를 클릭 하 여 응답 합니다.

    ![다른 질문에 답하려면](real-time-web-applications-with-signalr/_static/image13.png "다른 질문에 응답")

    *다른 질문에 응답*
4. 단추 중 하나를 클릭 한 후에 대답 나타나야 합니다. 알림 페이지에 대 한 통계 정보를 전체 페이지를 새로 고치려면 하지 않고도 업데이트 된 정보로 질문에 답변 한 후 자동으로 업데이트 됩니다.

    ![응답 한 후 통계 페이지를 새로](real-time-web-applications-with-signalr/_static/image14.png "답변 후 새로 고침 통계 페이지")

    *응답 한 후 새로 고친된 통계 페이지*

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a>연습 2: SQL Server를 사용 하 여 확장 합니다.

웹 응용 프로그램을 확장 하는 경우 일반적으로 중 선택할 수 있습니다 *스케일 업* 및 *수평 확장* 옵션입니다. *수직* 의미 하는 동안 더 많은 리소스 (CPU, RAM, 등)와 더 큰 서버를 사용 하 여 *확장할* 부하를 처리할 서버 추가 의미 합니다. 후자와 문제는 클라이언트가 서로 다른 서버에 라우팅될 얻을 수 있습니다. 하나의 서버에 연결 된 클라이언트에서 다른 서버에서 보낸 메시지를 받지 못합니다.

라는 구성 요소를 사용 하 여 이러한 문제를 해결할 수 *백플레인*, 서버 간에 메시지를 전달 합니다. 사용 하도록 설정 하는 백플레인에 각 응용 프로그램 인스턴스에 메시지를 백플레인에 보내고 백플레인에서 다른 응용 프로그램 인스턴스에 전달 합니다.

현재 세 가지 유형의 SignalR에 대 한 백플레인

- **Windows Azure 서비스 버스**합니다. 서비스 버스는 메시징 인프라 느슨하게 결합 된 메시지를 보내는 구성 요소입니다.
- **SQL Server**. SQL Server 백플레인에서 SQL 테이블에 메시지를 씁니다. 백플레인에서 효율적인 메시징에 대 한 Service Broker를 사용 합니다. 그러나 해당 Service Broker를 사용 하지 않는 경우에 작동 합니다.
- **Redis**합니다. Redis는 메모리에 키-값 저장소입니다. Redis는 메시지를 보내기 위한 게시/구독 ("pub/sub") 패턴을 지원 합니다.

모든 메시지가 메시지 버스를 통해 전송 됩니다. 메시지 버스 구현 하는 [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) 인터페이스에는 게시/구독 추상화를 제공 합니다. 기본 대체 하 여 작업의 백플레인 **IMessageBus** 는 버스 해당 백플레인에서 위한 것입니다.

버스를 통해 백플레인에서에 각 서버 인스턴스에 연결합니다. 메시지를 보낼 때를 백플레인에 이동 하 고 백플레인에서 모든 서버에 보냅니다. 서버 백플레인에서 메시지를 받으면 해당 로컬 캐시에서 메시지를 저장 합니다. 서버는 다음 로컬 캐시에서 클라이언트에 메시지를 배달 합니다.

SignalR 백플레인에서 작동 방식, 여기에 대 한 자세한 내용은 [문서](../performance/scaleout-in-signalr.md)합니다.

> [!NOTE]
> 백플레인에 병목이 될 수 있는 몇 가지 시나리오가 있습니다. 다음은 몇 가지 일반적인 SignalR 시나리오입니다.
> 
> - [서버 브로드캐스트](tutorial-server-broadcast-with-signalr.md) (예: 주식 시세): 백플레인 서버 메시지를 보내는 속도 제어 하기 때문에이 시나리오에 대 한 잘 작동 합니다.
> - [클라이언트-](tutorial-getting-started-with-signalr.md) (예: 채트):이 시나리오에서는 클라이언트의 수와 크기와 메시지 수가 조정 백플레인에서 병목 지점이 될 수 있습니다; 그리고 즉, 증가 하는 메시지의 속도 비율에 따라 더 많은 클라이언트에 조인 합니다.
> - [높은 주파수 실시간](tutorial-high-frequency-realtime-with-signalr.md) (예: 실시간 게임): 백플레인에이 시나리오에 적합 하지 않습니다.


이 연습을 사용 하 여 **SQL Server** 간에 메시지를 분산는 **들은 퀴즈** 응용 프로그램입니다. 모든 결과 얻기 위해 하지만 구성을 설정 하는 방법은 단일 테스트 컴퓨터에서 이러한 작업을 실행 합니다, 그리고 SignalR 응용 프로그램 두 개 이상의 서버에 배포 해야 합니다. 서버 중 하나 또는 별도 전용된 서버에도 SQL Server를 설치 해야 합니다.

![SQL Server 다이어그램을 사용 하 여 확장](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a>작업 1-시나리오 이해

이 작업의 2 개의 인스턴스를 실행 합니다 **들은 퀴즈** 로컬 컴퓨터의 인스턴스를 여러 개의 IIS를 시뮬레이션 합니다. 이 시나리오에서는 하나의 응용 프로그램에 trivia 질문에 대답 하는 경우, 업데이트는 두 번째 인스턴스의 통계 페이지에 알림이 발송 되지 않습니다. 이 시뮬레이션 유사한 여러 인스턴스에서 응용 프로그램를 배포할 환경을 부하 분산 장치를 사용 하 여 서로 통신 하 고 있습니다.

1. 열기는 **Begin.sln** 솔루션에 있는 **소스/e x 2-ScalingOutWithSQLServer/시작** 폴더입니다. 로드 되 고 나면 알게 될 것에 **서버 탐색기** 하지만 서로 다른 이름을 구조 솔루션에 동일한 두 개의 프로젝트. 로컬 컴퓨터에서 동일한 응용 프로그램의 두 인스턴스를 실행 중인 시뮬레이트합니다.

    ![시작 이라는 말 퀴즈의 2 개의 인스턴스를 시뮬레이션 하는 솔루션](real-time-web-applications-with-signalr/_static/image16.png "들은 퀴즈의 2 개의 인스턴스를 시뮬레이션 하는 솔루션 시작")

    *2 개의 들은 퀴즈의 인스턴스를 시뮬레이션 하는 솔루션 시작*
2. 솔루션 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 솔루션의 속성 페이지를 열고 **속성**합니다. **시작 프로젝트**선택, **여러 개의 시작 프로젝트** 변경는 **동작** 두 프로젝트에 대 한 값 *시작*합니다.

    ![여러 프로젝트를 시작](real-time-web-applications-with-signalr/_static/image17.png "여러 프로젝트를 시작")

    *여러 프로젝트를 시작*
3. 키를 눌러 **F5** 솔루션을 실행 합니다. 두 인스턴스는 응용 프로그램이 시작 **들은 퀴즈** 서로 다른 포트를 동일한 응용 프로그램의 여러 인스턴스를 시뮬레이션 합니다. 왼쪽에 화면의 오른쪽에도 브라우저 중 하나를 고정 합니다. 자격 증명으로 로그인 하거나 새 사용자를 등록 합니다. 로그인 한 Trivia 페이지 왼쪽에 유지 하 고 이동는 **통계** 오른쪽의 브라우저에서 페이지입니다.

    ![나란히 들은 퀴즈](real-time-web-applications-with-signalr/_static/image18.png)

    *나란히 들은 퀴즈*

    ![서로 다른 포트에서 들은 퀴즈](real-time-web-applications-with-signalr/_static/image19.png)

    *서로 다른 포트에서 들은 퀴즈*
4. 왼쪽된 브라우저에서 질문에 응답을 시작한 것을 확인할 수는 **통계** 오른쪽 브라우저에서 페이지 업데이트 되지 않습니다. 때문에 이것이 **SignalR** 해당 클라이언트에 메시지를 분산 하는 로컬 캐시에서 사용 하 여 및이 시나리오는 여러 인스턴스를 시뮬레이션 하 고, 따라서 캐시 간에 공유 되지 않습니다. 확인할 수 있습니다 **SignalR** 테스트 단계와 동일 하지만 단일 앱을 사용 하 여 작동 합니다. 다음 태스크에서는 인스턴스 간에 메시지를 복제 하려면 백플레인을 구성 합니다.
5. Visual Studio로 다시 이동 하 고 디버깅을 중지 합니다.

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a>작업 2-SQL Server 백플레인에서 만들기

이 태스크에서는 역할에 대 한 백플레인을 할 데이터베이스가 만들어집니다는 **들은 퀴즈** 응용 프로그램입니다. 사용 하 여 **SQL Server 개체 탐색기** 서버를 찾아 데이터베이스를 초기화 합니다. 또한 기능을 사용 하기는 **Service Broker**합니다.

1. **Visual Studio**, 열기 메뉴 **보기** 선택 **SQL Server 개체 탐색기**합니다.
2. 마우스 오른쪽 단추로 클릭 하 여 LocalDB 인스턴스에 연결 된 **SQL Server** 노드를 선택 하 고 **SQL Server 추가...**  옵션입니다.

    ![SQL Server 인스턴스를 추가](real-time-web-applications-with-signalr/_static/image20.png "SQL Server 인스턴스를 추가 합니다.")

    *SQL Server 인스턴스를 SQL Server 개체 탐색기에 추가*
3. 설정의 **서버 이름** 를 *(localdb) \v11.0* 둡니다 **Windows 인증** 인증 모드로 합니다. 클릭 **연결** 를 계속 합니다.

    ![LocalDB에 연결](real-time-web-applications-with-signalr/_static/image21.png "LocalDB에 연결")

    *LocalDB에 연결*
4. LocalDB 인스턴스를 연결한 했으므로 나타내는 SQL Server 백플레인에서 SignalR에 대 한 데이터베이스 만들기 해야 합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **데이터베이스** 노드 선택한 **새 데이터베이스 추가**합니다.

    ![새 데이터베이스에 추가](real-time-web-applications-with-signalr/_static/image22.png "새 데이터베이스에 추가")

    *새 데이터베이스에 추가*
5. 데이터베이스 이름을 설정 *SignalR* 클릭 **확인** 를 만듭니다.

    ![SignalR 데이터베이스를 만드는](real-time-web-applications-with-signalr/_static/image23.png "SignalR 데이터베이스를 만드는 중")

    *SignalR 데이터베이스 만들기*

    > [!NOTE]
    > 데이터베이스에 대 한 이름을 임의로 선택할 수 있습니다.
6. 에서 업데이트를 받는 보다 효율적으로 백플레인에서, 데이터베이스에 대 한 Service Broker를 활성화 하는 것이 좋습니다. Service Broker는 메시징 및 SQL Server의 큐에 대 한 기본 지원을 제공 합니다. 백플레인에서는 Service Broker 없이 작동합니다. 선택한 데이터베이스를 마우스 오른쪽 단추로 클릭 하 여 새 쿼리를 열고 **새 쿼리**합니다.

    ![새 쿼리를 열면](real-time-web-applications-with-signalr/_static/image24.png "새 쿼리 열기")

    *새 쿼리 열기*
7. Service Broker가 설정 여부를 확인 하려면 쿼리는 **은\_브로커\_활성화** 열에는 **sys.databases** 카탈로그 뷰. 최근에 열어 쿼리 창에서 다음 스크립트를 실행 합니다.

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    ![Service Broker 상태를 쿼리](real-time-web-applications-with-signalr/_static/image25.png "Service Broker 상태를 쿼리 합니다.")

    *Service Broker 상태를 쿼리합니다.*
8. 하는 경우의 값은 **은\_브로커\_활성화** 데이터베이스의 열은 &quot;0&quot;를 사용 하도록 설정 하려면 다음 명령을 사용 합니다. 대체 **&lt;귀하가 데이터베이스&gt;** 데이터베이스를 만들 때 설정한 이름 (예:: SignalR).

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    ![Service Broker를 사용 하도록 설정](real-time-web-applications-with-signalr/_static/image26.png "Service Broker 사용")

    *Service Broker를 사용 하도록 설정*

    > [!NOTE]
    > DB에 연결 하는 응용 프로그램이 없습니다 없으면이 쿼리 표시 하려면 교착 상태에 있는지 확인 하세요.

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a>작업 3 – SignalR 응용 프로그램 구성

이 태스크에서는 구성 **들은 퀴즈** 백플레인에서 SQL Server에 연결 하 합니다. 먼저 추가한는 **SignalR.SqlServer** 백플레인 데이터베이스에는 NuGet 패키지 및 연결 집합 문자열입니다.

1. 열기는 **패키지 관리자 콘솔** 에서 **도구** | **라이브러리 패키지 관리자**합니다. 다음 사항을 확인 **GeekQuiz** 에서 프로젝트를 선택는 **기본 프로젝트** 드롭 다운 목록입니다. 설치 하려면 다음 명령을 입력 하 고 **Microsoft.AspNet.SignalR.SqlServer** NuGet 패키지 합니다.

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. 프로젝트에 대해 이전 단계 하지만이 이번 반복 **GeekQuiz2**합니다.
3. SQL Server 백플레인에서 구성 하려면 엽니다는 **Startup.cs** 의 파일은 **GeekQuiz** 프로젝트 및 다음 코드를 추가 하는 **구성** 메서드. 대체 **&lt;귀하가 데이터베이스&gt;** 을 SQL Server 백플레인에서 만들 때 사용한 데이터베이스 이름입니다. 이 단계를 반복 하는 **GeekQuiz2** 프로젝트.

    (코드 조각- *RealTimeSignalR-e x 2-StartupConfiguration*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. 키를 눌러 프로젝트를 모두 SQL Server 백플레인에서 사용 하도록 구성 된, 했으므로 **F5** 으로 동시에 실행할 수 있습니다.
5. 다시, **Visual Studio** 의 두 인스턴스가 시작 됩니다 **들은 퀴즈** 서로 다른 포트에 있습니다. 브라우저 중 하나는 왼쪽의 다른 사용자의 화면 오른쪽에 고정 및 사용자 자격 증명으로 로그인 합니다. 왼쪽에 퀴즈 페이지를 유지 하 고 이동 **통계** pagein 오른쪽 브라우저.
6. 왼쪽된 브라우저에서 질문에 대답을 시작 합니다. 이 이번에는 **통계** 백플레인에서 덕분에 페이지를 업데이트 합니다. 응용 프로그램 간 전환 (**통계** 왼쪽에는 이제 및 **퀴즈** 오른쪽에 표시 됩니다) 하 고 두 인스턴스 모두에 대 한 작동 하는지 유효성을 검사 하는 테스트를 반복 합니다. 백플레인에서 역할을 한 *캐시 공유* 연결 된 클라이언트를 배포 하기 위한 자체 로컬 캐시에 메시지가 저장은 각 연결 된 서버와 각 서버에 대 한 메시지입니다.
7. Visual Studio로 다시 이동 하 고 디버깅을 중지 합니다.
8. SQL Server 백플레인 구성 요소는 자동으로 지정된 된 데이터베이스에 필요한 테이블을 생성합니다. 에 **SQL Server 개체 탐색기** 패널에서 백플레인에서 대해 만든 데이터베이스를 엽니다 (예:: SignalR) 해당 테이블을 확장 하 고 있습니다. 다음 표에 표시 됩니다.

    ![백플레인 테이블 생성](real-time-web-applications-with-signalr/_static/image27.png)

    *백플레인 테이블 생성*
9. 마우스 오른쪽 단추로 클릭는 **SignalR.Messages\_0** 테이블을 선택한 **데이터 보기**합니다.

    ![SignalR 백플레인 메시지 테이블 보기](real-time-web-applications-with-signalr/_static/image28.png)

    *SignalR 백플레인 메시지 테이블 보기*
10. 로 전송 된 다른 메시지를 볼 수는 **허브** trivia 질문에 대답 하는 경우. 백플레인에서이 메시지는 연결 된 인스턴스를 배포합니다.

    ![백플레인 메시지 테이블](real-time-web-applications-with-signalr/_static/image29.png)

    *백플레인 메시지 테이블*

* * *

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩에서 추가 하는 방법을 배웠습니다 **SignalR** 를 사용 하 여 연결 된 클라이언트에 서버에서 응용 프로그램 및 보내기 알림에 **허브**합니다. 사용 하 여 응용 프로그램을 확장 하는 방법을 배웠습니다 또한는 *백플레인* 여러 IIS 인스턴스에 응용 프로그램을 배포할 때 구성 요소입니다.
