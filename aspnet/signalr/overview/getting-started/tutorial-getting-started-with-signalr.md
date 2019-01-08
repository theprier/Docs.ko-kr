---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: '자습서: SignalR 2를 사용 하 여 실시간 채팅 | Microsoft Docs'
author: pfletcher
description: 이 자습서에는 SignalR을 사용하여 실시간 채팅 애플리케이션을 만드는 방법을 보여 줍니다. 빈 ASP.NET 웹 응용 프로그램에 SignalR을 추가합니다.
ms.author: riande
ms.date: 01/02/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: aa015abc47bb2450e04e167c0404aaa1d119ba2c
ms.sourcegitcommit: 97d7a00bd39c83a8f6bccb9daa44130a509f75ce
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54098626"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a>자습서: SignalR 2를 사용 하 여 실시간 채팅

이 자습서에서는 실시간 채팅 응용 프로그램을 만드는 SignalR을 사용 하는 방법을 보여 줍니다. SignalR 빈 ASP.NET 웹 응용 프로그램에 추가 하 고이 정보를 보내고 메시지를 표시 하는 HTML 페이지를 만듭니다.

이 자습서에서는 있습니다.

> [!div class="checklist"]
> * 프로젝트 설정
> * 샘플 실행
> * 코드 검사

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>전제 조건

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 사용 하 여 합니다 **ASP.NET 및 웹 개발** 워크 로드.

## <a name="set-up-the-project"></a>프로젝트 설정

이 섹션에서는 Visual Studio 2017 및 SignalR 2를 사용 하 여 빈 ASP.NET 웹 응용 프로그램을 만드는 방법을 보여 줍니다. SignalR에 추가한 채팅 응용 프로그램을 만듭니다.

1. Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.

    ![웹 만들기](tutorial-getting-started-with-signalr/_static/image2.png)

1. 에 **새 ASP.NET 프로젝트-SignalRChat** 창에서 유지 **빈** 선택 하 고 선택 **확인**합니다.

1. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **새 항목**합니다.

1. **새 항목 추가-SignalRChat**를 선택 **설치 됨** > **시각적 C#**   >  **Web**  >  **SignalR** 선택한 후 **SignalR 허브 클래스 (v2)** 합니다.

1. 클래스의 이름을 *ChatHub* 하 고 프로젝트에 추가 합니다.

    이 단계에서는 합니다 *ChatHub.cs* 클래스 파일 및 스크립트 파일 및 프로젝트에 SignalR을 지 원하는 어셈블리 참조의 집합을 추가 합니다.

1. 새 코드를 바꿉니다 *ChatHub.cs* 이 코드를 사용 하 여 클래스 파일:

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **새 항목**합니다.

1. **새 항목 추가-SignalRChat** 선택 **설치 됨** > **시각적 C#**   >  **Web** 차례로 선택 **OWIN Startup 클래스**합니다.

1. 클래스의 이름을 *시작* 하 고 프로젝트에 추가 합니다.

1. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **HTML 페이지**합니다.

1. 새 페이지의 이름을 *인덱스* 선택한 **확인**합니다.

1. **솔루션 탐색기**, 만든 HTML 페이지를 마우스 오른쪽 단추로 **시작 페이지로 설정**합니다.

1. HTML 페이지의 기본 코드를이 코드로 바꿉니다.

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. **솔루션 탐색기**를 확장 하 고 **스크립트**합니다.

    JQuery 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.

    > [!IMPORTANT]
    > 패키지 관리자 SignalR 스크립트의 이후 버전이 설치 될 수 있습니다.

1. 프로젝트에서 스크립트 파일의 버전에 해당 하는 코드 블록에 대 한 스크립트 참조는 확인 합니다.

    원래 코드 블록에서 스크립트 참조:
    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. 일치 하지 않으면 업데이트 합니다 *.html* 파일입니다.

1. 메뉴 모음에서 선택 **파일** > **모두 저장**합니다.

## <a name="run-the-sample"></a>샘플 실행

1. 도구 모음에서 설정 **스크립트 디버깅** 다음 디버그 모드에서 샘플을 실행 하려면 재생 단추를 선택 합니다.

    ![사용자 이름 입력](tutorial-getting-started-with-signalr/_static/image3.png)

1. 브라우저가 열리면 채팅 id에 대 한 이름을 입력 합니다.

1. 브라우저에서 URL을 복사 하 고 다른 두 브라우저를 열고 주소 표시줄에 Url을 붙여 넣습니다.

1. 각 브라우저에서 고유한 이름을 입력 합니다.

1. 이제 선택한 주석 추가 **보낼**합니다. 다른 브라우저에는 반복 합니다. 실시간 설명이 나타납니다.

    > [!NOTE]
    > 이 간단한 채팅 응용 프로그램 서버에서 토론 컨텍스트를 유지 하지 않습니다. 허브는 모든 현재 사용자에 게 의견을 브로드캐스트합니다. 채팅을 나중에 조인 하는 사용자에 가입할 때부터 추가 된 메시지를 표시 됩니다.

    세 가지 다른 브라우저에서 채팅 응용 프로그램을 실행 하는 방법을 참조 하세요. Tom, Anand, 및 Susan 메시지를 보낼 때, 모든 브라우저 실시간으로 업데이트 합니다.

    ![모든 세 가지 브라우저 동일한 채팅 기록 표시](tutorial-getting-started-with-signalr/_static/image4.png)

1. **솔루션 탐색기**를 검사 합니다 **스크립트 문서** 실행 중인 응용 프로그램에 대 한 노드. 명명 된 스크립트 파일이 *hubs* SignalR 라이브러리는 런타임에 생성 하는 합니다. 이 파일 jQuery 스크립트와 서버 쪽 코드 간의 통신을 관리합니다.

    ![스크립트 문서 노드의 hubs 스크립트 자동 생성](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a>코드 검사

SignalRChat 응용 프로그램에서는 두 가지 기본 SignalR 개발 작업을 보여 줍니다. 허브를 만드는 방법을 보여줍니다. 서버는 주 조정 개체와 해당 허브를 사용합니다. 허브는 SignalR jQuery 라이브러리를 사용 하 여 메시지 보내기 및 받기.

### <a name="signalr-hubs-in-the-chathubcs"></a>SignalR 허브를 ChatHub.cs에서

위의 코드 샘플에는 `ChatHub` 클래스에서 파생 되는 `Microsoft.AspNet.SignalR.Hub` 클래스입니다. 파생 된 `Hub` 클래스는 SignalR 응용 프로그램을 빌드하는 유용한 방법입니다. 허브 클래스에서 public 메서드를 만들고 해당 메서드를 사용 하 여 웹 페이지의 스크립트에서 호출 하 여 수 있습니다.

채팅 코드에서 클라이언트 호출을 `ChatHub.Send` 새 메시지를 전송 하는 방법입니다. 허브는 메시지를 전송 합니다 모든 클라이언트를 호출 하 여 `Clients.All.broadcastMessage`입니다.

`Send` 메서드 여러 허브 개념을 보여 줍니다.

* 클라이언트에서 호출할 수 있도록 허브에서 공용 메서드를 선언 합니다.

* 사용 된 `Microsoft.AspNet.SignalR.Hub.Clients` 이 허브에 연결 된 모든 클라이언트와 통신 하는 동적 속성입니다.

* 클라이언트에서 함수를 호출 (같은 `broadcastMessage` 함수) 클라이언트를 업데이트 합니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a>SignalR 및 index.html에서 jQuery

합니다 *index.html* 코드 샘플에서 페이지에는 SignalR jQuery 라이브러리를 사용 하 여 SignalR 허브와 통신 하는 방법을 보여 줍니다. 코드는 여러 중요 한 작업을 수행합니다. 허브를 참조 하는 프록시를 선언, 서버는 클라이언트 밀어넣기 콘텐츠를 호출할 수 있습니다 하 고 허브에 메시지를 보내는 연결을 시작 하는 함수를 선언 합니다.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> JavaScript에서 서버 클래스 및 해당 멤버에 대 한 참조는 camelCase 여야 합니다. 코드 샘플 참조는 C# *ChatHub* 으로 JavaScript에서 클래스 `chatHub`합니다.

이 코드 블록을 스크립트에 콜백 함수를 만듭니다.

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

서버의 허브 클래스는 각 클라이언트에 콘텐츠 업데이트를 푸시 하려면이 함수를 호출 합니다. 두 줄 해당 HTML 인코딩해야 표시 하기 전에 콘텐츠는 선택 사항 및 스크립트 삽입을 방지 하는 좋은 방법은 표시 합니다.

이 코드는 허브를 사용 하 여 연결을 엽니다.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> 이 방법을 사용 하면 이벤트 처리기 실행 되기 전에 코드는 연결을 설정 합니다.

코드는 연결을 시작 하 고 다음에 클릭 이벤트를 처리 하는 함수 전달 합니다 **보낼** HTML 페이지에 단추.

## <a name="additional-resources"></a>추가 자료

SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

* [SignalR 프로젝트](http://signalr.net)

* [SignalR Github 및 샘플](https://github.com/SignalR/SignalR)

* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>다음 단계

이 자습서에 있습니다.

> [!div class="checklist"]
> * 프로젝트 설정
> * 샘플 실행
> * 코드 검사

SignalR 및 MVC 5를 사용 하는 방법을 알아보려면 다음 문서로 계속 진행 하세요.
> [!div class="nextstepaction"]
> [SignalR 2 및 MVC 5](tutorial-getting-started-with-signalr-and-mvc.md)