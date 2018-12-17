---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: '자습서: SignalR 2 시작 | Microsoft Docs'
author: pfletcher
description: 이 자습서에는 SignalR을 사용하여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다. SignalR 빈 ASP.NET 웹 응용 프로그램에 추가 하 고는 HTML pa 만들기...
ms.author: riande
ms.date: 06/10/2014
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 3b06e7d0a602e061112adbceba92276f836f6311
ms.sourcegitcommit: 74e3be25ea37b5fc8b4b433b0b872547b4b99186
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53287340"
---
<a name="tutorial-getting-started-with-signalr-2"></a>자습서: SignalR 2 시작
====================
[Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

> 이 자습서에는 SignalR을 사용하여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다. SignalR 빈 ASP.NET 웹 응용 프로그램에 추가 하 고 보내고 메시지를 표시 하려면 HTML 페이지를 만듭니다. 
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR 버전 2
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a>이 자습서를 사용 하 여 Visual Studio 2012를 사용 하 여
> 
> 
> 이 자습서를 사용 하 여 Visual Studio 2012를 사용 하려면 다음을 수행 합니다.
> 
> - 업데이트 프로그램 [패키지 관리자](http://docs.nuget.org/docs/start-here/installing-nuget) 최신 버전으로 합니다.
> - 설치 합니다 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)합니다.
> - 웹 플랫폼 설치 관리자에서 검색 하 고 설치 **ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1**합니다. SignalR 클래스에 대 한 Visual Studio 템플릿 같은 설치 합니다 **허브**합니다.
> - 일부 템플릿 (와 같은 **OWIN 시작 클래스**)를 사용할 수 없습니다;이 대 한 클래스 파일을 대신 사용 합니다.
> 
> 
> ## <a name="tutorial-versions"></a>자습서 버전
> 
> 이전 버전의 SignalR에 대 한 정보를 참조 하세요 [SignalR 이전 버전](../older-versions/index.md)합니다.
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이 있으면
> 
> 이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요. 에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


## <a name="overview"></a>개요

이 자습서에서는 간단한 브라우저 기반 채팅 응용 프로그램을 빌드하는 방법을 보여 주는에서 SignalR 개발을 소개 합니다. 빈 ASP.NET 웹 응용 프로그램에 SignalR 라이브러리 추가, 메시지를 보내는 클라이언트에 허브 클래스 만들고 채팅 메시지를 주고받을 수 있는 HTML 페이지를 만듭니다. MVC 뷰를 사용 하 여 MVC 5에서 채팅 응용 프로그램을 만드는 방법을 보여 주는 유사한 자습서를 참조 하세요 [SignalR 2 및 MVC 5 시작](tutorial-getting-started-with-signalr-and-mvc.md)합니다.

> [!NOTE]
> 이 자습서에는 버전 2에서에서 SignalR 응용 프로그램을 만드는 방법을 보여 줍니다. SignalR의 차이점에 대 한 내용은 1.x과 2를 참조 하세요 [업그레이드 SignalR 1.x 프로젝트](../releases/upgrading-signalr-1x-projects-to-20.md) 하 고 [Visual Studio 2013 릴리스 정보](../../../visual-studio/overview/2013/release-notes.md#TOC13)합니다.

SignalR은 실시간 사용자 상호 작용 또는 실시간 데이터 업데이트를 필요로 하는 웹 응용 프로그램을 빌드하기 위한 오픈 소스.NET 라이브러리를 합니다. 소셜 응용 프로그램, 다중 사용자 게임, 비즈니스 공동 작업 및 뉴스, 날씨, 또는 재무 업데이트 응용 프로그램을 예로 들 수 있습니다. 이러한 실시간 응용 프로그램 이라고 합니다.

SignalR 실시간 응용 프로그램을 빌드하는 프로세스를 간소화 합니다. ASP.NET 서버 라이브러리 및 클라이언트-서버 연결을 관리 하 여 클라이언트에 콘텐츠 업데이트 푸시할 수 있도록 하 여 JavaScript 클라이언트 라이브러리를 포함 합니다. SignalR 라이브러리 실시간 기능을 사용 하려면 기존 ASP.NET 응용 프로그램에 추가할 수 있습니다.

이 자습서에는 다음 SignalR 개발 작업을 보여 줍니다.

- ASP.NET 웹 응용 프로그램에 SignalR 라이브러리에 추가 합니다.
- 클라이언트에 콘텐츠를 푸시 하려면 허브 클래스를 만드는 중입니다.
- 응용 프로그램을 구성 하는 OWIN 시작 클래스를 만드는 중입니다.
- 웹 페이지에서 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 허브에서 업데이트를 표시 합니다.

다음 스크린 샷은 채팅 응용 프로그램을 브라우저에서 실행을 보여 줍니다. 새로운 각 사용자 의견을 게시 하 고 사용자 조인 채팅 후 추가 참조 하세요. 수 있습니다.

![채트 인스턴스](tutorial-getting-started-with-signalr/_static/image1.png)

섹션:

- [프로젝트 설정](#setup)
- [샘플 실행](#run)
- [코드 검사](#code)
- [다음 단계](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>프로젝트 설정

이 섹션에서는 Visual Studio 2013 및 SignalR 버전 2 사용 하 여 빈 ASP.NET 웹 응용 프로그램을 만드는 방법을 보여 줍니다. SignalR에 추가한 채팅 응용 프로그램을 만듭니다.

필수 구성 요소:

- Visual Studio 2013. Visual Studio가 없는 경우 [ASP.NET 다운로드](https://www.asp.net/downloads) 무료 Visual Studio 2013 Express 개발 도구를 가져오려고 합니다.

다음 단계를 ASP.NET 빈 웹 응용 프로그램을 만들고 SignalR 라이브러리를 추가 하려면 Visual Studio 2013을 사용 합니다.

1. Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.

    ![웹 만들기](tutorial-getting-started-with-signalr/_static/image2.png)
2. 에 **새 ASP.NET 프로젝트** 둡니다 창 **빈** 선택 하 고 클릭 **프로젝트 만들기**합니다.

    ![빈 웹 만들기](tutorial-getting-started-with-signalr/_static/image3.png)
3. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭을 **추가 | SignalR 허브 클래스 (v2)** 합니다. 클래스의 이름을 **ChatHub.cs** 하 고 프로젝트에 추가 합니다. 이 단계에서는 합니다 **ChatHub** 클래스 및 스크립트 파일 및 SignalR을 지 원하는 어셈블리 참조의 집합을 프로젝트에 추가 합니다.

    > [!NOTE]
    > 열어 프로젝트에 SignalR을 추가할 수도 있습니다는 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 명령을 실행 하 고:

    `install-package Microsoft.AspNet.SignalR`

    SignalR을 추가 하려면 콘솔을 사용 하는 경우는 SignalR을 추가한 후 별도 단계로 SignalR 허브 클래스를 만듭니다.

    > [!NOTE]
    > Visual Studio 2012를 사용 하는 경우는 **SignalR 허브 클래스 (v2)** 템플릿을 사용할 수 없습니다. 일반을 추가할 수 있습니다 **클래스** 호출 `ChatHub` 대신 합니다.
4. **솔루션 탐색기**, 스크립트 노드를 확장 합니다. JQuery 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.
5. 새 코드를 바꿉니다 **ChatHub** 다음 코드를 사용 하 여 클래스입니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 **추가 | OWIN 시작 클래스**합니다. 새 클래스 이름을 `Startup` 확인을 클릭 합니다.

    > [!NOTE]
    > Visual Studio 2012를 사용 하는 경우는 **OWIN Startup 클래스** 템플릿을 사용할 수 없습니다. 일반을 추가할 수 있습니다 **클래스** 호출 `Startup` 대신 합니다.
7. 다음에 새 시작 클래스의 콘텐츠를 변경 합니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 **추가 | HTML 페이지**합니다. 새 페이지의 이름을 `index.html`입니다.
    >[!NOTE]
    >SignalR 및 JQuery 라이브러리에 대 한 참조의 버전 번호를 변경 해야 합니다.
9. **솔루션 탐색기**방금 만든 HTML 페이지를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 페이지로 설정**합니다.
10. HTML 페이지의 기본 코드를 다음 코드로 바꿉니다.

    > [!NOTE]
    > 패키지 관리자에서 SignalR 스크립트의 이후 버전을 설치할 수 있습니다. 아래 스크립트 참조 (해당 달라 지므로 SignalR 허브를 추가 하는 대신 NuGet을 사용 하 여 추가한 경우) 프로젝트에서 스크립트 파일의 버전에 해당 확인

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]
11. **모두 저장** 프로젝트에 대 한 합니다.

<a id="run"></a>

## <a name="run-the-sample"></a>샘플 실행

1. F5 키를 눌러 디버그 모드에서 프로젝트를 실행 합니다. HTML 페이지 브라우저 인스턴스를 사용자 이름에 대 한 프롬프트에 로드합니다.

    ![사용자 이름 입력](tutorial-getting-started-with-signalr/_static/image4.png)
2. 사용자 이름을 입력 합니다.
3. 브라우저의 주소 줄에서 URL을 복사 하 고 사용 하 여 자세한 두 브라우저 인스턴스를 엽니다. 브라우저 인스턴스마다에서 고유한 사용자 이름을 입력 합니다.
4. 각 브라우저 인스턴스에서 주석을 추가 하 고 클릭 **보낼**합니다. 주석을 모든 브라우저 인스턴스에 표시 됩니다.

    > [!NOTE]
    > 이 간단한 채팅 응용 프로그램 서버에서 토론 컨텍스트를 유지 하지 않습니다. 허브는 모든 현재 사용자에 게 의견을 브로드캐스트합니다. 채팅을 나중에 조인 하는 사용자에 가입할 때부터 추가 된 메시지를 표시 됩니다.

    다음 스크린 샷은 세 가지 브라우저 인스턴스를 인스턴스 메시지를 보내는 경우 업데이트는 모두에서 실행 중인 채팅 응용 프로그램을 보여 줍니다.

    ![채팅 브라우저](tutorial-getting-started-with-signalr/_static/image5.png)
5. **솔루션 탐색기**를 검사 합니다 **스크립트 문서** 실행 중인 응용 프로그램에 대 한 노드. 명명 된 스크립트 파일이 **hubs** SignalR 라이브러리 런타임에 동적으로 생성 하는 합니다. 이 파일 jQuery 스크립트와 서버 쪽 코드 간의 통신을 관리합니다.

    ![](tutorial-getting-started-with-signalr/_static/image6.png)

<a id="code"></a>

## <a name="examine-the-code"></a>코드 검사

SignalR 채팅 응용 프로그램에는 두 개의 기본 SignalR 개발 작업 방법을 보여 줍니다.: 서버에서 주 조정 개체로 허브를 만들고 SignalR jQuery 라이브러리를 사용 하 여 메시지를 주고받을 수 있습니다.

### <a name="signalr-hubs"></a>SignalR 허브

코드 샘플에는 **ChatHub** 클래스에서 파생 되는 **Microsoft.AspNet.SignalR.Hub** 클래스입니다. 파생 된 **허브** 클래스는 SignalR 응용 프로그램을 빌드하는 유용한 방법입니다. 허브 클래스에서 공용 메서드를 만들 수 있으며 그런 다음 웹 페이지의 스크립트에서 호출 하 여 이러한 메서드에 액세스할 수 있습니다.

채팅 코드에서 클라이언트 호출을 **ChatHub.Send** 새 메시지를 전송 하는 방법입니다. 허브에 메시지를 보냅니다 모든 클라이언트를 호출 하 여 **Clients.All.broadcastMessage**합니다.

합니다 **보낼** 메서드 여러 허브 개념을 보여 줍니다.

- 클라이언트에서 호출할 수 있도록 허브에서 공용 메서드를 선언 합니다.
- 사용 된 **Microsoft.AspNet.SignalR.Hub.Clients** 이 허브에 연결 된 모든 클라이언트에 액세스 하는 동적 속성입니다.
- 클라이언트에서 함수를 호출 (같은 `broadcastMessage` 함수) 클라이언트를 업데이트 합니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery"></a>SignalR 및 jQuery

코드 샘플에서 HTML 페이지에는 SignalR jQuery 라이브러리를 사용 하 여 SignalR 허브와 통신 하는 방법을 보여 줍니다. 프록시 서버는 클라이언트 밀어넣기 콘텐츠를 호출할 수 있는 함수를 선언 하 고 허브에 메시지를 보내기에 대 한 연결을 시작 허브 참조를 선언 하는 코드에는 필수 작업입니다.

다음 코드는 허브 프록시에 대 한 참조를 선언 합니다.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> JavaScript (camel case)에서 서버 클래스 및 해당 멤버에 대 한 참조는입니다. 코드 샘플을 참조 하는 C# **ChatHub** JavaScript는 클래스 **chatHub**합니다.


다음 코드는 스크립트에서 만든 콜백 함수입니다. 서버의 허브 클래스는 각 클라이언트에 콘텐츠 업데이트를 푸시 하려면이 함수를 호출 합니다. HTML을 표시 하기 전에 콘텐츠를 인코딩할 두 줄은 선택 사항 이므로 스크립트 삽입을 방지 하는 간단한 방법을 보여 줍니다.

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

다음 코드에는 허브를 사용 하 여 연결을 여는 방법을 보여 줍니다. 코드는 연결을 시작 하 고 다음에 클릭 이벤트를 처리 하는 함수 전달 합니다 **보낼** HTML 페이지에 단추.

> [!NOTE]
> 이 방법은 이벤트 처리기 실행 되기 전에 연결이 설정 되어 있는지 확인 합니다.


[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

<a id="next"></a>

## <a name="next-steps"></a>다음 단계

SignalR은 실시간 웹 응용 프로그램을 빌드하기 위한 프레임 워크는 배웠습니다. 여러 SignalR 개발 작업에 배웠습니다: SignalR ASP.NET 응용 프로그램에 추가 하는 방법, 허브 클래스를 만드는 방법 및 허브에서 메시지를 송수신 하는 방법입니다.

연습은 샘플 SignalR 응용 프로그램을 Azure에 배포 하는 방법에 대해서 [Azure App Service에서 Web apps를 사용 하 여 SignalR](../deployment/using-signalr-with-azure-web-sites.md)합니다. Visual Studio 웹 프로젝트를 Windows Azure 웹 사이트를 배포 하는 방법에 대 한 자세한 내용은 참조 하세요. [Azure App Service에서 ASP.NET 웹 앱 만들기](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)합니다.

고급 SignalR 개발 개념에 알아보려면 SignalR 소스 코드 및 리소스에 대 한 다음 사이트를 방문 하십시오.

- [SignalR 프로젝트](http://signalr.net)
- [SignalR Github 및 샘플](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
