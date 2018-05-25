---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: '자습서: 높은 주파수 실시간 2 SignalR과 | Microsoft Docs'
author: pfletcher
description: 이 자습서에는 ASP.NET SignalR을 사용 하 여 높은 주파수 메시징 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 높은 주파수의 메시징 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: ab051b2ab85d1aac1e7179f342f22f470b1d1cc7
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="tutorial-high-frequency-realtime-with-signalr-2"></a>자습서: 높은 주파수 실시간 2 SignalR과
====================
으로 [Patrick Fletcher](https://github.com/pfletcher)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

> 이 자습서에는 ASP.NET SignalR 2를 사용 하 여 높은 주파수 메시징 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 고정 된 요금이; 전송 하는 업데이트를 의미이 경우 높은 주파수 메시징 이 응용 프로그램의 경우 최대 10 개까지 두 번째를 메시지입니다.
> 
> 이 자습서에서 만드는 응용 프로그램 사용자가 끌 수 있는 셰이프를 표시 합니다. 연결 된 다른 모든 브라우저에서 도형의 위치 다음 업데이트를 사용 하 여 끌어온 도형의 위치와 일치 하도록 업데이트 됩니다.
> 
> 이 자습서의 개념을 실시간 게임에서 응용 프로그램 및 기타 시뮬레이션 응용 프로그램에 있어야 합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR 버전 2
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a>이 자습서와 함께 Visual Studio 2012를 사용 하 여
> 
> 
> 이 자습서와 함께 Visual Studio 2012를 사용 하려면 다음을 수행 합니다.
> 
> - 업데이트 프로그램 [패키지 관리자](http://docs.nuget.org/docs/start-here/installing-nuget) 를 최신 버전입니다.
> - 설치는 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)합니다.
> - 웹 플랫폼 설치 관리자에서 검색 하 고 설치 **ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1**합니다. SignalR 클래스에 대 한 Visual Studio 템플릿을와 같은 설치 **허브**합니다.
> - 일부 서식 파일 (와 같은 **OWIN 시작 클래스**)은 사용할 수 없습니다; 이러한 경우에 대 한 클래스 파일을 대신 사용 합니다.
> 
> 
> ## <a name="tutorial-versions"></a>자습서 버전
> 
> 이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이
> 
> 이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요. 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


## <a name="overview"></a>개요

이 자습서에는 개체의 상태를 실시간으로 다른 브라우저를 공유 하는 응용 프로그램을 만드는 방법을 보여 줍니다. 응용 프로그램 만들겠습니다 MoveShape 라고 합니다. MoveShape 페이지는 다음을 끌 수 있습니다; HTML Div 요소를 표시 합니다. 사용자가 컨트롤을 끌면 새 위치로 쿼리를 다음에 맞게 도형의 위치를 업데이트 하려면 다른 모든 연결 된 클라이언트를 확인할 서버로 보내집니다.

![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

이 자습서에서 만든 응용 프로그램은 Damian edwards의 데모를 기반으로 한 것입니다. 이 데모를 포함 하는 비디오를 볼 수 있습니다 [여기](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)합니다.

이 자습서는 셰이프를 끌 때 발생 하는 각 이벤트에서 SignalR 메시지를 보내는 방법을 보여 주는으로 시작 됩니다. 연결 된 각 클라이언트가 셰이프의 로컬 버전의 위치는 메시지를 받을 때마다 업데이트 후 됩니다.

응용 프로그램에서이 방법을 사용 하 여 작동 합니다이 아닙니다 권장된 프로그래밍 모델을 전송, 하므로 클라이언트와 서버가 메시지와 함께 당황 얻을 수 하 고 성능 저하는 메시지 수에 제한이 없어집니다 있을 수 있으므로 . 각 새 위치로 부드럽게 이동 하는 대신 각 메서드에서 셰이프를 즉시 이동은 연결이 끊긴 클라이언트에 표시 된 애니메이션 이어야 합니다. 자습서의 뒷부분에 나오는 섹션에서는 클라이언트 또는 서버에서 메시지를 보내는 최대 속도 제한 하는 타이머 함수를 만드는 방법 및 위치 간에 셰이프를 원활 하 게 이동 하는 방법을 보여 줍니다. 이 자습서에서 만든 응용 프로그램의 최종 버전에서 다운로드할 수 있습니다 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)합니다.

이 자습서에는 다음 섹션이 포함 됩니다.

- [필수 조건](#prerequisites)
- [프로젝트의 프로젝트를 만들고 SignalR 및 JQuery.UI NuGet 패키지를 추가 합니다.](#createtheproject2013)
- [기본 응용 프로그램 만들기](#baseapp)
- [응용 프로그램을 시작할 때 허브 시작](#startup2013)
- [클라이언트 루프 추가](#clientloop)
- [서버 루프 추가](#serverloop)
- [클라이언트에서 부드러운 애니메이션 추가](#animation)
- [추가 단계](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a>필수 구성 요소

이 자습서는 Visual Studio 2013 필요합니다.

<a id="createtheproject2013"></a>

## <a name="create-the-project-and-add-the-signalr-and-jqueryui-nuget-package"></a>프로젝트의 프로젝트를 만들고 SignalR 및 JQuery.UI NuGet 패키지를 추가 합니다.

이 섹션에서는 Visual Studio 2013에서 프로젝트를 만들겠습니다.

다음 단계는 ASP.NET 빈 웹 응용 프로그램을 만들고 SignalR 및 jQuery.UI 라이브러리를 추가 Visual Studio 2013을 사용 합니다.

1. Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.

    ![웹 만들기](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)
2. 에 **새 ASP.NET 프로젝트** 창 leave **빈** 선택한 클릭 **프로젝트 만들기**합니다.

    ![빈 웹 만들기](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
3. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 선택 **추가 | SignalR 허브 클래스 (v2)** 합니다. 클래스의 이름을 **MoveShapeHub.cs** 프로젝트에 추가 합니다. 이 단계에서는 **MoveShapeHub** 클래스 및 스크립트 파일 및 SignalR을 지 원하는 어셈블리 참조의 집합을 프로젝트에 추가 합니다.

    > [!NOTE]
    > 클릭 하 여 SignalR 프로젝트에 추가할 수도 있습니다 **도구 | 라이브러리 패키지 관리자 | 패키지 관리자 콘솔** 하 고 명령을 실행 합니다.

    `install-package Microsoft.AspNet.SignalR`. 

    SignalR을 추가 하 고 콘솔을 사용 하는 경우는 SignalR을 추가한 다음 별도 단계로 SignalR 허브 클래스를 만듭니다.
4. 클릭 **도구 | 라이브러리 패키지 관리자 | 패키지 관리자 콘솔**합니다. 패키지 관리자 창에서 다음 명령을 실행 합니다.

    `Install-Package jQuery.UI.Combined`

    이 셰이프 애니메이션 효과 적용 하는 데 사용할 하는 jQuery UI 라이브러리를 설치 합니다.
5. **솔루션 탐색기** 스크립트 노드를 확장 합니다. JQuery, jQueryUI, 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.

    ![스크립트 라이브러리 참조](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="baseapp"></a>

## <a name="create-the-base-application"></a>기본 응용 프로그램 만들기

이 섹션에서는 각 마우스 이동 이벤트 동안 셰이프의 위치는 서버에 전송 하는 브라우저 응용 프로그램을 만들겠습니다. 다음 서버를 수신할 때 연결 된 다른 모든 클라이언트에이 정보를 전파 합니다. 이후 섹션에서이 응용 프로그램에 확장 합니다.

1. MoveShapeHub.cs 클래스에서 이미 만든 하지 않은 경우 **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가**, **클래스 중...** . 클래스의 이름을 **MoveShapeHub** 클릭 **추가**합니다.
2. 새 코드를 바꿉니다 **MoveShapeHub** 를 다음 코드로 클래스입니다.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

    `MoveShapeHub` 위의 클래스는 SignalR 허브의 구현입니다. 와 같이 [SignalR 시작](tutorial-getting-started-with-signalr.md) 자습서, 허브 클라이언트를 직접 호출 하는 메서드가 있습니다. 이 경우 클라이언트는 새을 포함 하는 개체를 보냅니다 서버에 연결 된 다른 모든 클라이언트에 브로드캐스트 가져옵니다 셰이프의 X 및 Y 좌표입니다. SignalR은 JSON을 사용 하 여이 개체를 자동으로 serialize 됩니다.

    클라이언트에 전송 될 개체 (`ShapeModel`) 도형의 위치를 저장 하는 멤버가 포함 되어 있습니다. 서버에서 개체의 버전도 포함 되어 구성원을 추적 하는 클라이언트의 데이터에 저장 하는 지정된 된 클라이언트 데이터를 전송 되지 않습니다. 사용 하 여이 멤버는 `JsonIgnore` 되지 않도록 하려면 serialize 하 고 클라이언트에 전송 되는 특성입니다.

<a id="startup2013"></a>
## <a name="starting-the-hub-when-the-application-starts"></a>응용 프로그램을 시작할 때 허브 시작

1. 다음, 응용 프로그램이 시작 허브에 대 한 매핑을를 설정 합니다. SignalR 2에서 호출 되는 OWIN 시작 클래스, 추가 하 여 수행 됩니다 `MapSignalR` 때 시작 클래스 `Configuration` OWIN 시작 될 때 메서드를 실행 합니다. OWIN의 시작 하는 클래스가 추가 됩니다 사용 하 여 처리는 `OwinStartup` 어셈블리 특성입니다.

    **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 **추가 | OWIN 시작 클래스**합니다. 클래스의 이름을 *시작* 클릭 **확인**합니다.
2. 다음에 Startup.cs의 내용을 변경 합니다.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

<a id="client"></a>
## <a name="adding-the-client"></a>클라이언트 추가

1. 다음으로, 클라이언트를 추가 합니다. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 **추가 | 새 항목**합니다. 에 **새 항목 추가** 대화 상자에서 **Html 페이지**합니다. 페이지 이름을 **Default.html** 클릭 **추가**합니다.
2. **솔루션 탐색기**방금 만든 페이지를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 페이지로 설정**합니다.
3. 다음 코드 조각으로 HTML 페이지의 기본 코드를 대체 합니다.

    > [!NOTE]
    > 스크립트 참조 Scripts 폴더에서 프로젝트에 추가 된 패키지에 일치 하는 항목 아래를 확인 합니다.

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html)]

    위의 HTML 및 JavaScript 코드 셰이프라고 빨간색 Div 만듭니다 jQuery 라이브러리를 사용 하 여 셰이프 끌기 동작을 활성화 하 고 셰이프를 사용 하 여 `drag` 이벤트의 셰이프 위치는 서버에 보내도록 합니다.
4. F5 키를 눌러 응용 프로그램을 시작 합니다. 페이지의 URL을 복사 하 고 두 번째 브라우저 창에 붙여 넣습니다. 브라우저 창을; 중 하나에 셰이프를 끌어 옵니다. 다른 브라우저 창에서 모양 이동 해야 합니다.

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a>클라이언트 루프 추가

모든 마우스 이동 이벤트의 셰이프를 위치 보내는 불필요 한 네트워크 트래픽 용량을 만들고, 클라이언트의 메시지 스로틀할 수 해야 합니다. Javascript에서는 `setInterval` 고정 된 요금이 서버에 새 위치 정보를 전송 하는 루프를 설정 하는 함수입니다. 이 루프는 "게임 루프의" 게임 나 다른 시뮬레이션의 기능을 모두를 구동 하는 반복 해 서 호출된 된 함수는 매우 기본적인 표현입니다.

1. 다음 코드 조각에 맞게 HTML 페이지에서 클라이언트 코드를 업데이트 합니다.

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html)]

    위의 업데이트 추가 `updateServerModel` 고정된 주파수 호출 되는 함수입니다. 이 함수는 위치 데이터에서 서버로 보내는 때마다는 `moved` 플래그 보낼 새 위치 데이터 임을 나타냅니다.
2. F5 키를 눌러 응용 프로그램을 시작 합니다. 페이지의 URL을 복사 하 고 두 번째 브라우저 창에 붙여 넣습니다. 브라우저 창을; 중 하나에 셰이프를 끌어 옵니다. 다른 브라우저 창에서 모양 이동 해야 합니다. 서버에 전송 될 메시지 수는 스로틀, 이후 애니메이션 이전 단원에서와 마찬가지로 자연스럽 게 표시 되지 않습니다.

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a>서버 루프 추가

현재 응용 프로그램에서 클라이언트에 서버에서 보낸 메시지 이동 받을 때 종종 합니다. 클라이언트에서 표시 된 유사한 문제가 발생 필요 하 고 연결 결과적으로 서비스 장애 유발 될 수 보다 더 자주 메시지를 보낼 수 있습니다. 이 섹션에서는 보내는 메시지의 속도 제한 하는 타이머를 구현 하는 서버를 업데이트 하는 방법에 설명 합니다.

1. 내용을 대체 `MoveShapeHub.cs` 다음 코드 조각으로 합니다.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    위의 코드를 추가 하려면 클라이언트 확장는 `Broadcaster` 보내는 나와 있는 클래스를 사용 하 여 메시지는 `Timer` 에서.NET framework 클래스입니다.

    허브 자체는 일시적 이므로 (만들어질 필요할 때마다)는 `Broadcaster` 단일 항목으로 생성 됩니다. (.NET 4에 도입 된) 초기화 지연 사용 되는 타이머를 시작 하기 전에 첫 번째 허브 인스턴스 완전히 생성 되었는지 확인, 필요할 때까지 해당 생성을 연기 하는 데 사용 됩니다.

    클라이언트에 대 한 호출 `UpdateShape` 함수 다음 허브의 외부로 이동할 `UpdateModel` 메서드, 들어오는 메시지를 받을 때마다에 즉시 한다는 더 이상 호출 됩니다. 초당, 25 호출의 속도로 클라이언트에 메시지는 전송 하는 대신, 관리 하는 `_broadcastLoop` 내에서 타이머는 `Broadcaster` 클래스입니다.

    허브에서 클라이언트 메서드를 직접 호출 하는 대신 마지막으로,는 `Broadcaster` 클래스에서 현재 작동 허브에 대 한 참조를 가져올 해야 (`_hubContext`)를 사용 하는 `GlobalHost`합니다.
2. F5 키를 눌러 응용 프로그램을 시작 합니다. 페이지의 URL을 복사 하 고 두 번째 브라우저 창에 붙여 넣습니다. 브라우저 창을; 중 하나에 셰이프를 끌어 옵니다. 다른 브라우저 창에서 모양 이동 해야 합니다. 이전 섹션에서 브라우저에서 눈에 띄는 차이 됩니다 하지 하지만 클라이언트에 전송 될 메시지 수가 제한 됩니다.

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a>클라이언트에서 부드러운 애니메이션 추가

응용 프로그램은 거의 완료 하지만 하나 더 개선, 클라이언트에서 모양의 동작에서 서버 메시지에 대 한 응답으로 이동할 때 만들 수 있습니다. 도형의 위치 서버에 의해 지정 된 새 위치를 설정 하는 대신 JQuery UI 라이브러리에서는 `animate` 현재와 새 위치로 간에 셰이프를 원활 하 게 이동 하는 함수입니다.

1. 클라이언트의 업데이트 `updateShape` 검색할 메서드 아래의 강조 표시 된 코드와 같은:

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

    위의 코드는 애니메이션 간격 (이 경우 100 밀리초)의 과정 동안 서버에 의해 지정 된 새 레코드로 이전 위치에서 셰이프를 이동 합니다. 새 애니메이션을 시작 하기 전에 모든 이전 애니메이션 도형에서 실행 되는 해제 됩니다.
2. F5 키를 눌러 응용 프로그램을 시작 합니다. 페이지의 URL을 복사 하 고 두 번째 브라우저 창에 붙여 넣습니다. 브라우저 창을; 중 하나에 셰이프를 끌어 옵니다. 다른 브라우저 창에서 모양 이동 해야 합니다. 다른 창에 있는 셰이프에 이동 시간 들어오는 메시지당 한 번 설정 하는 대신이 이동을 보간은 처럼 덜 불규칙적인 표시 되어야 합니다.

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image8.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a>추가 단계

이 자습서에서는 클라이언트와 서버 간에 높은 주파수 메시지를 보내는 SignalR 응용 프로그램을 프로그래밍 하는 방법을 배웠습니다. 이 통신 패러다임 온라인 게임 및 다른 시뮬레이션을와 같은 개발 하는 데 유용 [SignalR을 사용 하 여 만든 ShootR 게임](http://shootr.signalr.net)합니다.

이 자습서에서 만든 전체 응용 프로그램에서 다운로드할 수 있습니다 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)합니다.

SignalR 개발 개념에 대 한 자세한 내용은 SignalR 소스 코드 및 리소스에 대 한 다음 사이트를 방문 하십시오.

- [SignalR 프로젝트](http://signalr.net)
- [SignalR Github 및 샘플](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

SignalR 응용 프로그램을 Azure에 배포 하는 방법에 대 한 연습을을 참조 하십시오. [Azure 앱 서비스의 웹 앱과 함께 사용 하 여 SignalR](../deployment/using-signalr-with-azure-web-sites.md)합니다. Visual Studio 웹 프로젝트는 Windows Azure 웹 사이트를 배포 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure 앱 서비스에서 ASP.NET 웹 앱을 만들](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)합니다.
