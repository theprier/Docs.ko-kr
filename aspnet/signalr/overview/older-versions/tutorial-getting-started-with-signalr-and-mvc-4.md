---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
title: '자습서: 시작 SignalR 1.x 및 MVC 4 | Microsoft Docs'
author: pfletcher
description: ASP.NET SignalR 및 ASP.NET MVC 4를 사용 하 여 실시간 채팅 응용 프로그램을 빌드합니다.
ms.author: riande
ms.date: 03/29/2013
ms.assetid: eeef9f73-6de3-49f9-b50b-9af22108f2ce
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 95fc3315149e07dbdb0505a2b5ab197bfedba097
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48910878"
---
<a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a>자습서: 시작 SignalR 1.x 및 MVC 4
====================
하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)

> 이 자습서에는 ASP.NET SignalR을 사용 하 여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다. SignalR MVC 4 응용 프로그램에 추가 하 고 보내고 메시지를 표시 하려면 채팅 뷰를 만듭니다.


## <a name="overview"></a>개요

이 자습서에서는 ASP.NET SignalR 및 ASP.NET MVC 4를 사용 하 여 실시간 웹 응용 프로그램 개발 소개 합니다. 이 자습서에서는 같은 채팅 응용 프로그램 코드를 사용 합니다 [SignalR 시작 자습서](tutorial-getting-started-with-signalr.md), 하지만 인터넷 템플릿을 기반으로 하는 MVC 4 응용 프로그램에 추가 하는 방법을 보여 줍니다.

이 항목에서는 다음 SignalR 개발 작업을 배웁니다.

- MVC 4 응용 프로그램에 SignalR 라이브러리에 추가 합니다.
- 클라이언트에 콘텐츠를 푸시 하려면 허브 클래스를 만드는 중입니다.
- 웹 페이지에서 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 허브에서 업데이트를 표시 합니다.

다음 스크린샷은 완료 된 채팅 응용 프로그램을 브라우저에서 실행을 보여 줍니다.

![채트 인스턴스](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

섹션:

- [프로젝트 설정](#setup)
- [샘플 실행](#run)
- [코드 검사](#code)
- [다음 단계](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>프로젝트 설정

필수 구성 요소:

- Visual Studio 2010 SP1, Visual Studio 2012 또는 Visual Studio 2012 Express를 선택 합니다. Visual Studio가 없는 경우 [ASP.NET 다운로드](https://www.asp.net/downloads) 무료 Visual Studio 2012 Express 개발 도구를 가져오려고 합니다.
- Visual Studio 2010을 설치 [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683)합니다.

이 섹션에서는 ASP.NET MVC 4 응용 프로그램을 만들고 SignalR 라이브러리를 추가, 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.

1. 1. Visual Studio에서 ASP.NET MVC 4 응용 프로그램, SignalRChat, 이름을 만들고 확인을 클릭 합니다.

        > [!NOTE]
        > VS 2010에서 선택 **.NET Framework 4** Framework 버전 드롭다운 컨트롤에서. SignalR 코드가.NET Framework 버전 4 및 4.5에서 실행 됩니다.

        ![Mvc 웹 만들기](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. 인터넷 응용 프로그램 템플릿을 선택 하는 옵션의 선택을 취소 합니다 **단위 테스트 프로젝트 만들기**, 확인을 클릭 합니다.

         ![Mvc 인터넷 사이트 만들기](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. 엽니다는 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 하 고 다음 명령을 실행 합니다. 이 단계는 스크립트 파일 및 SignalR 기능을 사용 하는 어셈블리 참조의 집합을 프로젝트에 추가 합니다.

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. **솔루션 탐색기** 스크립트 폴더를 확장 합니다. SignalR에 대 한 스크립트 라이브러리를 프로젝트에 추가한 참고 합니다.

         ![라이브러리 참조](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭을 **추가 | 새 폴더**, 라는 새 폴더를 추가한 **Hubs**합니다.
      6. 마우스 오른쪽 단추로 클릭 합니다 **Hubs** 폴더를 클릭 **추가 | 클래스**, C# 라는 새 클래스를 만들어 **ChatHub.cs**합니다. 이 클래스를 사용 하 여 모든 클라이언트에 메시지를 보내는 SignalR server 허브로 합니다.

> [!NOTE]
> 설치한 후 Visual Studio 2012를 사용 하는 경우는 [ASP.NET 및 웹 도구 2012.2 업데이트](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), 허브 클래스를 만들려면 새 SignalR 항목 템플릿을 사용할 수 있습니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **Hubs** 폴더를 클릭 **추가 | 새 항목**을 선택 **SignalR 허브 클래스 (v1)**, 및 클래스 이름을 **ChatHub.cs**합니다.


1. 코드를 대체 합니다 **ChatHub** 다음 코드를 사용 하 여 클래스입니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. 엽니다는 **Global.asax** 프로젝트의 파일 및 메서드 호출을 추가 `RouteTable.Routes.MapHubs();` 에서 코드의 첫 번째 줄으로는 `Application_Start` 메서드. 이 코드는 SignalR 허브에 대 한 기본 경로 등록 하 고 다른 경로 등록 하기 전에 호출 해야 합니다. 완료 된 `Application_Start` 메서드는 다음 예제와 같습니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. 편집 합니다 `HomeController` 클래스에서 찾을 **controllers/Homecontroller.cs** 클래스에 다음 메서드를 추가 합니다. 이 메서드는 반환 된 **채팅** 이후 단계에서 만들 뷰.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. 마우스 오른쪽 단추로 클릭 합니다 `Chat` 방금 생성 하 고 클릭 메서드 **뷰 추가** 새 뷰 파일을 만들려면.
5. 에 **뷰 추가** 대화 상자에서 하는 확인란을 선택 해야 **레이아웃 또는 마스터 페이지를 사용 하 여** (다른 확인란을 선택 취소)를 클릭 하 고 **추가**합니다.

    ![보기 추가](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. 라는 새 뷰 파일을 편집 **Chat.cshtml**합니다. 후는 &lt;h2&gt; 태그에 다음을 붙여넣고 &lt;div&gt; 섹션 및 `@section scripts` 페이지에 코드 블록입니다. 이 스크립트는 채팅 메시지를 보내고 서버에서 메시지를 표시 하려면 페이지를 활성화 합니다. 채팅 뷰에 대 한 전체 코드는 다음 코드 블록에 표시 됩니다.

    > [!IMPORTANT]
    > SignalR 및 기타 스크립트 라이브러리를 Visual Studio 프로젝트에 추가 하면 패키지 관리자는이 항목에 표시 된 버전 보다 최신 스크립트의 버전을 설치할 수 있습니다. 코드에서 스크립트 참조를 프로젝트에 설치 스크립트 라이브러리의 버전 일치 하는지 확인 합니다.

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. **모두 저장** 프로젝트에 대 한 합니다.

<a id="run"></a>

## <a name="run-the-sample"></a>샘플 실행

1. F5 키를 눌러 디버그 모드에서 프로젝트를 실행 합니다.
2. 브라우저 주소 줄에 추가할 **/home/채팅** 프로젝트에 대 한 기본 페이지의 url입니다. 채팅 페이지가 브라우저 인스턴스를 사용자 이름에 대 한 프롬프트에 로드 합니다.

    ![사용자 이름 입력](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. 사용자 이름을 입력 합니다.
4. 브라우저의 주소 줄에서 URL을 복사 하 고 사용 하 여 자세한 두 브라우저 인스턴스를 엽니다. 브라우저 인스턴스마다에서 고유한 사용자 이름을 입력 합니다.
5. 각 브라우저 인스턴스에서 주석을 추가 하 고 클릭 **보낼**합니다. 주석을 모든 브라우저 인스턴스에 표시 됩니다.

    > [!NOTE]
    > 이 간단한 채팅 응용 프로그램 서버에서 토론 컨텍스트를 유지 하지 않습니다. 허브는 모든 현재 사용자에 게 의견을 브로드캐스트합니다. 채팅을 나중에 조인 하는 사용자에 가입할 때부터 추가 된 메시지를 표시 됩니다.
6. 다음 스크린 샷은 채팅 응용 프로그램을 브라우저에서 실행을 보여 줍니다.

    ![채팅 브라우저](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. **솔루션 탐색기**를 검사 합니다 **스크립트 문서** 실행 중인 응용 프로그램에 대 한 노드. 이 노드는 브라우저와 Internet Explorer를 사용 하는 경우 디버그 모드에서 표시 합니다. 명명 된 스크립트 파일이 **hubs** SignalR 라이브러리 런타임에 동적으로 생성 하는 합니다. 이 파일 jQuery 스크립트와 서버 쪽 코드 간의 통신을 관리합니다. Internet Explorer 이외의 브라우저를 사용 하는 경우 동적도 액세스할 수 있습니다 **hubs** 탐색 하 여 직접 예를 들어 파일 http://mywebsite/signalr/hubs합니다.

    ![생성 된 허브 스크립트](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a>코드 검사

SignalR 채팅 응용 프로그램에는 두 개의 기본 SignalR 개발 작업 방법을 보여 줍니다.: 서버에서 주 조정 개체로 허브를 만들고 SignalR jQuery 라이브러리를 사용 하 여 메시지를 주고받을 수 있습니다.

### <a name="signalr-hubs"></a>SignalR 허브

코드 샘플에는 **ChatHub** 클래스에서 파생 되는 **Microsoft.AspNet.SignalR.Hub** 클래스입니다. 파생 된 **허브** 클래스는 SignalR 응용 프로그램을 빌드하는 유용한 방법입니다. 허브 클래스에서 공용 메서드를 만들 수 있으며 그런 다음 웹 페이지에 jQuery 스크립트에서 호출 하 여 이러한 메서드에 액세스할 수 있습니다.

채팅 코드에서 클라이언트 호출을 **ChatHub.Send** 새 메시지를 전송 하는 방법입니다. 허브에 메시지를 보냅니다 모든 클라이언트를 호출 하 여 **Clients.All.addNewMessageToPage**합니다.

합니다 **보낼** 메서드 여러 허브 개념을 보여 줍니다.

- 클라이언트에서 호출할 수 있도록 허브에서 공용 메서드를 선언 합니다.
- 사용 된 **Microsoft.AspNet.SignalR.Hub.Clients** 이 허브에 연결 된 속성을 모든 클라이언트에 액세스 합니다.
- 클라이언트에서 jQuery 함수를 호출 (같은 `addNewMessageToPage` 함수) 클라이언트를 업데이트 합니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>SignalR 및 jQuery

합니다 **Chat.cshtml** 코드 샘플에서 파일 보기 SignalR jQuery 라이브러리를 사용 하 여 SignalR 허브와 통신 하는 방법을 보여 줍니다. 코드에서 필수 작업을 자동으로 생성 된 프록시에 허브에 대 한 서버는 클라이언트 밀어넣기 콘텐츠를 호출할 수 있는 함수를 선언 하 고 연결을 시작 하는 허브에 메시지를 보낼 대 한 참조를 만듭니다.

다음 코드는 허브에 대 한 프록시를 선언합니다.

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> JQuery에서는 서버 클래스 및 해당 멤버에 대 한 참조 (camel case) 에서입니다. 코드 샘플을 참조 하는 C# **ChatHub** 클래스와 jquery에서 **chatHub**합니다. 참조 하려는 경우는 `ChatHub` 클래스 기존 파스칼을 사용 하 여 jquery에서 ChatHub.cs 클래스 파일을 편집 하듯이 C#에서는 대/소문자 구분 합니다. 추가 `using` 문을 참조 하는 `Microsoft.AspNet.SignalR.Hubs` 네임 스페이스입니다. 추가한 합니다 `HubName` 특성을 합니다 `ChatHub` 클래스, 예를 들어 `[HubName("ChatHub")]`합니다. 마지막으로 업데이트 하려면 jQuery 참조는 `ChatHub` 클래스입니다.


다음 코드에는 스크립트에 콜백 함수를 만드는 방법을 보여 줍니다. 서버의 허브 클래스는 각 클라이언트에 콘텐츠 업데이트를 푸시 하려면이 함수를 호출 합니다. 에 대 한 선택적인 호출을 `htmlEncode` 함수 표시 방법은 HTML 스크립트 삽입을 방지 하는 방법으로 페이지에 표시 하기 전에 메시지 콘텐츠를 인코딩.

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

다음 코드에는 허브를 사용 하 여 연결을 여는 방법을 보여 줍니다. 코드는 연결을 시작 하 고 다음에 클릭 이벤트를 처리 하는 함수 전달 합니다 **보낼** 채팅 페이지에서 단추.

> [!NOTE]
> 이 방법은 이벤트 처리기 실행 되기 전에 연결이 설정 되어 있는지 확인 합니다.


[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>다음 단계

SignalR은 실시간 웹 응용 프로그램을 빌드하기 위한 프레임 워크는 배웠습니다. 여러 SignalR 개발 작업에 배웠습니다: SignalR ASP.NET 응용 프로그램에 추가 하는 방법, 허브 클래스를 만드는 방법 및 허브에서 메시지를 송수신 하는 방법입니다.

고급 SignalR 개발 개념에 알아보려면 SignalR 소스 코드 및 리소스에 대 한 다음 사이트를 방문 하십시오.

- [SignalR 프로젝트](http://signalr.net)
- [SignalR Github 및 샘플](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
