---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: '자습서: SignalR 2를 사용 하 여 자주 실시간 앱 만들기 | Microsoft Docs'
author: bradygaster
description: 이 자습서에는 빈도가 높은 메시징 기능을 제공 하는 데 ASP.NET SignalR을 사용 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 44aaa2b0c059de310e963f642fa56c2f00a7e443
ms.sourcegitcommit: ebf4e5a7ca301af8494edf64f85d4a8deb61d641
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54836729"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a>자습서: SignalR 2를 사용 하 여 자주 실시간 앱 만들기

이 자습서에는 빈도가 높은 메시징 기능을 제공 하는 데 ASP.NET SignalR 2를 사용 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 이 경우 "빈도가 높은 메시징" 의미 서버는 고정된 요금으로 업데이트를 보냅니다. 초당 최대 10 개의 메시지를 보냅니다.

만든 응용 프로그램에 사용자를 끌 수 있는 셰이프를 표시 합니다. 서버는 업데이트를 사용 하 여 끌어 온 모양의 위치와 일치 하도록 모든 연결 된 브라우저에서 모양의 위치를 업데이트 합니다.

이 자습서에 도입 된 개념 실시간 게임에서 응용 프로그램 및 다른 시뮬레이션 응용 프로그램을 갖습니다.

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 프로젝트 설정
> * 기본 응용 프로그램 만들기
> * 앱 시작 시 허브에 매핑
> * 클라이언트 추가
> * 앱 실행
> * 클라이언트 루프 추가
> * 서버 루프를 추가 합니다.
> * 부드러운 애니메이션 추가

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>전제 조건

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 사용 하 여 합니다 **ASP.NET 및 웹 개발** 워크 로드.

## <a name="set-up-the-project"></a>프로젝트 설정

이 섹션에서는 Visual Studio 2017에서 프로젝트를 만들 수 있습니다.

이 섹션에서는 Visual Studio 2017을 사용 하 여 빈 ASP.NET 웹 응용 프로그램을 만들고 SignalR 및 jQuery.UI 라이브러리를 추가 하는 방법을 보여 줍니다.

1. Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.

    ![웹 만들기](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. 에 **새 ASP.NET 웹 응용 프로그램-MoveShapeDemo** 창에서 유지 **빈** 선택 하 고 선택 **확인**합니다.

1. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **새 항목**합니다.

1. **새 항목 추가-MoveShapeDemo**를 선택 **설치 됨** > **시각적 C#**   >  **Web**  >  **SignalR** 선택한 후 **SignalR 허브 클래스 (v2)** 합니다.

1. 클래스의 이름을 *MoveShapeHub* 하 고 프로젝트에 추가 합니다.

    이 단계에서는 합니다 *MoveShapeHub.cs* 클래스 파일입니다. 동시에 스크립트 파일 및 프로젝트에 SignalR을 지 원하는 어셈블리 참조의 집합을 추가 합니다.

1. 선택 **도구가** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**합니다.

1. **패키지 관리자 콘솔**,이 명령을 실행 합니다.

    ```console
    Install-Package jQuery.UI.Combined
    ```

    이 명령은 jQuery UI 라이브러리를 설치합니다. 도형에 애니메이션 효과를 사용 합니다.

1. **솔루션 탐색기**, 스크립트 노드를 확장 합니다.

    ![스크립트 라이브러리 참조](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    JQuery, jQueryUI, 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.

## <a name="create-the-base-application"></a>기본 응용 프로그램 만들기

이 섹션에서는 브라우저 응용 프로그램을 만들 수 있습니다. 앱 서버에 각 마우스 이동 이벤트 동안 모양의 위치를 보냅니다. 서버에는이 정보를 실시간으로 연결 된 다른 모든 클라이언트를 브로드캐스트합니다. 이후 섹션에서이 응용 프로그램에 대 한 자세히 알아봅니다.

1. 엽니다는 *MoveShapeHub.cs* 파일입니다.

1. 코드를 대체 합니다 *MoveShapeHub.cs* 이 코드를 사용 하 여 파일:

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. 파일을 저장합니다.

`MoveShapeHub` 클래스는 SignalR 허브의 구현입니다. 에서처럼 합니다 [SignalR을 사용 하 여 시작](tutorial-getting-started-with-signalr.md) 자습서에서는 허브에 클라이언트를 직접 호출 하는 메서드가 있습니다. 이 경우 새 X 및 Y를 사용 하 여 개체를 서버로 셰이프 조정 하는 클라이언트 전송 합니다. 이러한 좌표는 연결 된 다른 모든 클라이언트에 브로드캐스트 가져옵니다. SignalR은 자동으로 JSON을 사용 하 여이 개체를 serialize 합니다.

앱 보내기는 `ShapeModel` 클라이언트 개체입니다. 모양의 위치를 저장 하는 멤버가 있습니다. 또한 서버에서 개체의 버전이 저장 되는 클라이언트의 데이터 추적에 멤버가 있습니다. 이 개체는 서버 자체를 다시 클라이언트의 데이터를 보내지 못하도록 방지 합니다. 이 멤버를 사용 하는 `JsonIgnore` 에서 데이터를 직렬화 및 다시 클라이언트로 보내는 응용 프로그램을 유지 하는 특성입니다.

## <a name="map-to-the-hub-when-app-starts"></a>앱 시작 시 허브에 매핑

다음으로 허브에 대 한 매핑 때 설정한 응용 프로그램을 시작 합니다. SignalR 2에 OWIN 시작 클래스 추가 매핑을 만듭니다.

1. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **새 항목**합니다.

1. **새 항목 추가-MoveShapeDemo** 선택 **설치 됨** > **시각적 C#**   >  **Web** 차례로 선택 **OWIN Startup 클래스**합니다.

1. 클래스의 이름을 *시동* 선택한 **확인**합니다.

1. 기본 코드를 대체 합니다 *Startup.cs* 이 코드를 사용 하 여 파일:

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

OWIN 시작 클래스 호출 `MapSignalR` 앱을 실행 하는 경우는 `Configuration` 메서드. OWIN의 시작 클래스 처리를 사용 하 여 앱 추가 `OwinStartup` 어셈블리 특성입니다.

## <a name="add-the-client"></a>클라이언트 추가

클라이언트에 대 한 HTML 페이지를 추가 합니다.

1. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **HTML 페이지**합니다.

1. 페이지의 이름을 **기본** 선택한 **확인**합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *Default.html* 선택한 **시작 페이지로 설정**합니다.

1. 기본 코드를 대체 합니다 *Default.html* 이 코드를 사용 하 여 파일:

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. **솔루션 탐색기**를 확장 하 고 **스크립트**합니다.

    JQuery 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.

    > [!IMPORTANT]
    > 패키지 관리자 SignalR 스크립트의 이후 버전을 설치합니다.

1. 프로젝트에서 스크립트 파일의 버전에 해당 하는 코드 블록의 스크립트 참조를 업데이트 합니다.

이 HTML 및 JavaScript 코드에서는 빨간색 `div` 호출 `shape`합니다. JQuery 라이브러리를 사용 하 여 셰이프 끌기 동작을 사용 하도록 설정 하 고 사용 하 여 `drag` 도형의 위치 서버로 보낼 이벤트.

## <a name="run-the-app"></a>앱 실행

앱을 실행할 수 있습니다 se'e에 작동 합니다. 브라우저 창 주위 셰이프를 끌어 놓으면 다른 브라우저에서 셰이프 너무 이동 합니다.

1. 도구 모음에서 설정 **스크립트 디버깅** 다음 디버그 모드에서 응용 프로그램을 실행 하려면 재생 단추를 선택 합니다.

    ![디버깅 모드 켜기 재생을 선택 하는 사용자의 스크린샷.](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    오른쪽 위 모퉁이에 있는 빨간색 셰이프를 사용 하 여 브라우저 창이 열립니다.

1. 페이지의 URL을 복사 합니다.

1. 다른 브라우저를 열고 주소 표시줄에 URL을 붙여넣습니다.

1. 브라우저 창 중 하나에서 셰이프를 끕니다. 다른 브라우저 창에서 셰이프는 다음과 같습니다.

응용 프로그램을 하는 동안이 메서드를 사용 하 여 함수를 하지 권장 되는 프로그래밍 모델입니다. 보낸 시작 메시지의 수는 상한 제한은 없습니다. 결과적으로, 클라이언트와 서버가 가져올 메시지로 인해 과부하가 걸리면 및 성능이 저하 됩니다. 또한 앱 클라이언트에서 연결 되지 않은 애니메이션을 표시합니다. 이 불규칙적인 애니메이션 셰이프 각 메서드에 의해 즉시 이동 하기 때문에 발생 합니다. 셰이프 원활 하 게 각 새 위치로 이동 하는 경우에 것이 좋습니다. 다음으로, 해당 문제를 해결 하는 방법에 알아봅니다.

## <a name="add-the-client-loop"></a>클라이언트 루프 추가

모든 마우스 이동 이벤트의 셰이프를 위치의 보내기는 불필요 한 네트워크 트래픽 양에 만듭니다. 앱은 클라이언트에서 메시지를 제한 해야 합니다.

Javascript를 사용 하 여 `setInterval` 고정된 요금으로 서버에 새 위치 정보를 전송 하는 루프를 설정 하는 함수입니다. 이 루프는 "게임 루프입니다."의 기본 표현 반복적으로 호출된 된 함수는 게임의 모든 기능을 구동 하는 것입니다.

1. 클라이언트 코드를 대체 합니다 *Default.html* 이 코드를 사용 하 여 파일:

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > 스크립트 파일에 대 한 참조를 다시 대체 해야 합니다. 프로젝트의 스크립트 버전이 일치 해야 합니다.

    이 새 코드를 추가 합니다 `updateServerModel` 함수입니다. 고정 된 빈도에 메서드가 호출 됩니다. 함수는 서버에 위치 데이터를 보냅니다 때마다는 `moved` 플래그 보낼 새 위치 데이터 임을 나타냅니다.

1. 응용 프로그램을 시작 하려면 재생 단추를 선택 합니다.

1. 페이지의 URL을 복사 합니다.

1. 다른 브라우저를 열고 주소 표시줄에 URL을 붙여넣습니다.

1. 브라우저 창 중 하나에서 셰이프를 끕니다. 다른 브라우저 창에서 셰이프는 다음과 같습니다.

앱에 전송 된 서버를 애니메이션으로 부드러운 나타나지 메시지 수가 제한 되므로 처음 않았습니다.

## <a name="add-the-server-loop"></a>서버 루프를 추가 합니다.

현재 응용 프로그램에서 서버에서 클라이언트로 전송 된 메시지 서 수신 하는 경우가 많습니다. 이 네트워크 트래픽을 클라이언트에서 볼 수 있듯이 유사한 문제를 표시 합니다.

필요한 것 보다 더 자주 앱 메시지를 보낼 수 있습니다. 결과적으로 연결이 플 러 딩 될 수 있습니다. 이 섹션에는 나가는 메시지의 속도 제한 하는 타이머를 추가 하려면 서버를 업데이트 하는 방법을 설명 합니다.

1. 내용을 바꿉니다 `MoveShapeHub.cs` 이 코드를 사용 하 여:

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. 응용 프로그램을 시작 하려면 재생 단추를 선택 합니다.

1. 페이지의 URL을 복사 합니다.

1. 다른 브라우저를 열고 주소 표시줄에 URL을 붙여넣습니다.

1. 브라우저 창 중 하나에서 셰이프를 끕니다.

이 코드를 추가 하는 클라이언트를 확장 합니다 `Broadcaster` 클래스입니다. 새 클래스를 사용 하 여 나가는 메시지를 제한 합니다 `Timer` .NET framework 클래스입니다.

자체 허브 일시적인을 학습 하는 것이 좋습니다. 필요할 때마다 생성 됩니다. 앱은 하므로 `Broadcaster` 단일 항목으로 합니다. 초기화 지연을 사용 하 여 지연 된 `Broadcaster`의 필요할 때까지 생성 합니다. 앱은 첫 번째 인스턴스에 완전히 타이머를 시작 하기 전에 보장 합니다.

클라이언트에 대 한 호출 `UpdateShape` 함수는 허브의 외부로 이동 후 `UpdateModel` 메서드. 더 이상 앱 들어오는 메시지를 수신 될 때마다 즉시 호출 됩니다. 대신 앱 초 당 25 호출의 속도로 클라이언트에 메시지를 보냅니다. 프로세스에서 관리 되는 `_broadcastLoop` 내에서 타이머를 `Broadcaster` 클래스입니다.

허브에서 직접 클라이언트 메서드를 호출 하는 대신에 마지막으로, 합니다 `Broadcaster` 클래스는 현재 운영 체제에 대 한 참조를 가져올 해야 `_hubContext` 허브입니다. 사용 하 여 참조를 가져옵니다는 `GlobalHost`합니다.

## <a name="add-smooth-animation"></a>부드러운 애니메이션 추가

거의 완료 되 면 응용 프로그램 이지만 하나 더 개선 수 있도록 합니다. 앱 서버 메시지에 따라에서 클라이언트에서 셰이프를 이동합니다. 서버에서 지정 된 새 위치로 모양의 위치를 설정 하는 대신 JQuery UI 라이브러리를 사용 하 여 `animate` 함수입니다. 셰이프 현재 및 새 위치로 간에 원활 하 게 이동할 수 있습니다.

1. 클라이언트의 업데이트 `updateShape` 의 메서드를 *Default.html* 파일을 강조 표시 된 코드와 같습니다.

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. 응용 프로그램을 시작 하려면 재생 단추를 선택 합니다.

1. 페이지의 URL을 복사 합니다.

1. 다른 브라우저를 열고 주소 표시줄에 URL을 붙여넣습니다.

1. 브라우저 창 중 하나에서 셰이프를 끕니다.

다른 창에서 모양 이동 덜 불규칙적인 나타납니다. 앱을 통해 들어오는 메시지당 한 번 설정 하는 것이 아니라 시간 이동을 보간합니다.

이 코드의 이전 위치에서 새 셰이프를 이동합니다. 애니메이션 간격에 걸쳐 모양의 위치를 제공 하는 서버입니다. 이 경우에은 100 밀리초입니다. 앱을 새 애니메이션을 시작 하기 전에 셰이프를 실행 하는 모든 이전 애니메이션을 지웁니다.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

## <a name="additional-resources"></a>추가 자료

방금 알아본 통신 패러다임은 온라인 게임 및 다른 시뮬레이션 같은 개발 하기 위한 유용한 [SignalR을 사용 하 여 만든 ShootR 게임](https://shootr.azurewebsites.net/)합니다.

SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

* [SignalR 프로젝트](http://signalr.net)

* [SignalR GitHub 및 샘플](https://github.com/SignalR/SignalR)

* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 프로젝트 설정
> * 기본 응용 프로그램을 만들었습니다.
> * 앱 시작 시 허브에 매핑
> * 클라이언트 추가
> * 앱 실행
> * 클라이언트 루프를 추가합니다.
> * 서버 루프를 추가합니다.
> * 부드러운 애니메이션 추가

ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법에 알아보려면 다음 문서로 계속 진행 하세요.
> [!div class="nextstepaction"]
> [SignalR 2 및 서버 브로드캐스트](tutorial-server-broadcast-with-signalr.md)