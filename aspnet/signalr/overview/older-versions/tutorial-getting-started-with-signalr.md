---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr
title: '자습서: SignalR 시작 1.x | Microsoft Docs'
author: pfletcher
description: HTML 페이지에 실시간 채팅 응용 프로그램을 빌드하려면 ASP.NET SignalR을 사용 합니다.
ms.author: aspnetcontent
ms.date: 02/18/2013
ms.assetid: fdc3599a-5217-44c1-951f-0eec9812dce7
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 13d33ff7e3cfff996a9849cfccfcc43754c8234e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37838629"
---
<a name="tutorial-getting-started-with-signalr-1x"></a>자습서: SignalR 시작 1.x
====================
하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)

> 이 자습서에는 SignalR을 사용하여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다. SignalR 빈 ASP.NET 웹 응용 프로그램에 추가 하 고 보내고 메시지를 표시 하려면 HTML 페이지를 만듭니다.


## <a name="overview"></a>개요

이 자습서에서는 간단한 브라우저 기반 채팅 응용 프로그램을 빌드하는 방법을 보여 주는에서 SignalR 개발을 소개 합니다. 빈 ASP.NET 웹 응용 프로그램에 SignalR 라이브러리 추가, 메시지를 보내는 클라이언트에 허브 클래스 만들고 채팅 메시지를 주고받을 수 있는 HTML 페이지를 만듭니다. MVC 뷰를 사용 하 여 MVC 4에서 채팅 응용 프로그램을 만드는 방법을 보여 주는 유사한 자습서를 참조 하세요 [SignalR 및 MVC 4 시작](index.md)합니다.

> [!NOTE]
> 이 자습서의 SignalR 릴리스 (1.x) 버전을 사용합니다. SignalR의 차이점에 대 한 내용은 1.x 및 2.0 참조 [업그레이드 SignalR 1.x 프로젝트](../releases/upgrading-signalr-1x-projects-to-20.md)합니다.

SignalR은 실시간 사용자 상호 작용 또는 실시간 데이터 업데이트를 필요로 하는 웹 응용 프로그램을 빌드하기 위한 오픈 소스.NET 라이브러리를 합니다. 소셜 응용 프로그램, 다중 사용자 게임, 비즈니스 공동 작업 및 뉴스, 날씨, 또는 재무 업데이트 응용 프로그램을 예로 들 수 있습니다. 이러한 실시간 응용 프로그램 이라고 합니다.

SignalR 실시간 응용 프로그램을 빌드하는 프로세스를 간소화 합니다. ASP.NET 서버 라이브러리 및 클라이언트-서버 연결을 관리 하 여 클라이언트에 콘텐츠 업데이트 푸시할 수 있도록 하 여 JavaScript 클라이언트 라이브러리를 포함 합니다. SignalR 라이브러리 실시간 기능을 사용 하려면 기존 ASP.NET 응용 프로그램에 추가할 수 있습니다.

이 자습서에는 다음 SignalR 개발 작업을 보여 줍니다.

- ASP.NET 웹 응용 프로그램에 SignalR 라이브러리에 추가 합니다.
- 클라이언트에 콘텐츠를 푸시 하려면 허브 클래스를 만드는 중입니다.
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

이 섹션에는 빈 ASP.NET 웹 응용 프로그램을 만드는 방법을 보여 줍니다 SignalR에 추가한 채팅 응용 프로그램을 만듭니다.

필수 구성 요소:

- Visual Studio 2010 SP1 또는 2012입니다. Visual Studio가 없는 경우 [ASP.NET 다운로드](https://www.asp.net/downloads) 무료 Visual Studio 2012 Express 개발 도구를 가져오려고 합니다.
- [Microsoft ASP.NET 및 웹 도구 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941)합니다. Visual Studio 2012의 경우이 설치 관리자는 Visual Studio로 SignalR 템플릿을 포함 하는 새로운 ASP.NET 기능을 추가 합니다. Visual Studio 2010 SP1 용 설치 관리자는 사용할 수 없지만 설치 단계에 설명 된 대로 SignalR NuGet 패키지를 설치 하 여 자습서를 완료할 수 있습니다.

다음 단계를 Visual Studio 2012를 사용 하 여 ASP.NET 빈 웹 응용 프로그램 만들기를 SignalR 라이브러리를 추가 합니다.

1. Visual Studio에서 ASP.NET 빈 웹 응용 프로그램을 만듭니다.

    ![빈 웹 만들기](tutorial-getting-started-with-signalr/_static/image2.png)
2. 엽니다는 **패키지 관리자 콘솔** 를 선택 하 여 **도구 | 라이브러리 패키지 관리자 | 패키지 관리자 콘솔**합니다. 콘솔 창에 다음 명령을 입력 합니다.

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    이 명령은 설치 된 최신 버전의 SignalR 1.x 합니다.
3. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭을 **추가 | 클래스**합니다. 새 클래스 이름을 **ChatHub**합니다.
4. **솔루션 탐색기** 스크립트 노드를 확장 합니다. JQuery 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.

    ![라이브러리 참조](tutorial-getting-started-with-signalr/_static/image3.png)
5. 코드를 대체 합니다 **ChatHub** 다음 코드를 사용 하 여 클래스입니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 **추가 | 새 항목**합니다. 에 **새 항목 추가** 대화 상자에서 **전역 응용 프로그램 클래스** 클릭 **추가**합니다.

    ![전역 추가](tutorial-getting-started-with-signalr/_static/image4.png)
7. 다음을 추가 합니다 `using` 제공 된 후 문을 `using` Global.asax.cs 클래스에는 문입니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. 코드의 다음 줄을 추가 합니다 `Application_Start` SignalR 허브에 대 한 기본 경로 등록 하려면 전역 클래스의 메서드.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 **추가 | 새 항목**합니다. 에 **새 항목 추가** 대화 상자, Html 페이지 선택 및 클릭 **추가**합니다.
10. **솔루션 탐색기**방금 만든 HTML 페이지를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 페이지로 설정**합니다.
11. HTML 페이지의 기본 코드를 다음 코드로 바꿉니다.

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. **모두 저장** 프로젝트에 대 한 합니다.

<a id="run"></a>

## <a name="run-the-sample"></a>샘플 실행

1. F5 키를 눌러 디버그 모드에서 프로젝트를 실행 합니다. HTML 페이지 브라우저 인스턴스를 사용자 이름에 대 한 프롬프트에 로드합니다.

    ![사용자 이름 입력](tutorial-getting-started-with-signalr/_static/image5.png)
2. 사용자 이름을 입력 합니다.
3. 브라우저의 주소 줄에서 URL을 복사 하 고 사용 하 여 자세한 두 브라우저 인스턴스를 엽니다. 브라우저 인스턴스마다에서 고유한 사용자 이름을 입력 합니다.
4. 각 브라우저 인스턴스에서 주석을 추가 하 고 클릭 **보낼**합니다. 주석을 모든 브라우저 인스턴스에 표시 됩니다.

    > [!NOTE]
    > 이 간단한 채팅 응용 프로그램 서버에서 토론 컨텍스트를 유지 하지 않습니다. 허브는 모든 현재 사용자에 게 의견을 브로드캐스트합니다. 채팅을 나중에 조인 하는 사용자에 가입할 때부터 추가 된 메시지를 표시 됩니다.

    다음 스크린 샷은 세 가지 브라우저 인스턴스를 인스턴스 메시지를 보내는 경우 업데이트는 모두에서 실행 중인 채팅 응용 프로그램을 보여 줍니다.

    ![채팅 브라우저](tutorial-getting-started-with-signalr/_static/image6.png)
5. **솔루션 탐색기**를 검사 합니다 **스크립트 문서** 실행 중인 응용 프로그램에 대 한 노드. 명명 된 스크립트 파일이 **hubs** SignalR 라이브러리 런타임에 동적으로 생성 하는 합니다. 이 파일 jQuery 스크립트와 서버 쪽 코드 간의 통신을 관리합니다.

    ![생성 된 허브 스크립트](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a>코드 검사

SignalR 채팅 응용 프로그램에는 두 개의 기본 SignalR 개발 작업 방법을 보여 줍니다.: 서버에서 주 조정 개체로 허브를 만들고 SignalR jQuery 라이브러리를 사용 하 여 메시지를 주고받을 수 있습니다.

### <a name="signalr-hubs"></a>SignalR 허브

코드 샘플에는 **ChatHub** 클래스에서 파생 되는 **Microsoft.AspNet.SignalR.Hub** 클래스입니다. 파생 된 **허브** 클래스는 SignalR 응용 프로그램을 빌드하는 유용한 방법입니다. 허브 클래스에서 공용 메서드를 만들 수 있으며 그런 다음 웹 페이지에 jQuery 스크립트에서 호출 하 여 이러한 메서드에 액세스할 수 있습니다.

채팅 코드에서 클라이언트 호출을 **ChatHub.Send** 새 메시지를 전송 하는 방법입니다. 허브에 메시지를 보냅니다 모든 클라이언트를 호출 하 여 **Clients.All.broadcastMessage**합니다.

합니다 **보낼** 메서드 여러 허브 개념을 보여 줍니다.

- 클라이언트에서 호출할 수 있도록 허브에서 공용 메서드를 선언 합니다.
- 사용 된 **Microsoft.AspNet.SignalR.Hub.Clients** 이 허브에 연결 된 모든 클라이언트에 액세스 하는 동적 속성입니다.
- 클라이언트에서 jQuery 함수를 호출 (같은 `broadcastMessage` 함수) 클라이언트를 업데이트 합니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>SignalR 및 jQuery

코드 샘플에서 HTML 페이지에는 SignalR jQuery 라이브러리를 사용 하 여 SignalR 허브와 통신 하는 방법을 보여 줍니다. 프록시 서버는 클라이언트 밀어넣기 콘텐츠를 호출할 수 있는 함수를 선언 하 고 허브에 메시지를 보내기에 대 한 연결을 시작 허브 참조를 선언 하는 코드에는 필수 작업입니다.

다음 코드는 허브에 대 한 프록시를 선언합니다.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> JQuery에서는 서버 클래스 및 해당 멤버에 대 한 참조 (camel case) 에서입니다. 코드 샘플을 참조 하는 C# **ChatHub** 클래스와 jquery에서 **chatHub**합니다.


다음 코드는 스크립트에서 만든 콜백 함수입니다. 서버의 허브 클래스는 각 클라이언트에 콘텐츠 업데이트를 푸시 하려면이 함수를 호출 합니다. HTML을 표시 하기 전에 콘텐츠를 인코딩할 두 줄은 선택 사항 이므로 스크립트 삽입을 방지 하는 간단한 방법을 보여 줍니다.

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

다음 코드에는 허브를 사용 하 여 연결을 여는 방법을 보여 줍니다. 코드는 연결을 시작 하 고 다음에 클릭 이벤트를 처리 하는 함수 전달 합니다 **보낼** HTML 페이지에 단추.

> [!NOTE]
> 이 방법은 이벤트 처리기 실행 되기 전에 연결이 설정 되는 시나리오.


[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>다음 단계

SignalR은 실시간 웹 응용 프로그램을 빌드하기 위한 프레임 워크는 배웠습니다. 여러 SignalR 개발 작업에 배웠습니다: SignalR ASP.NET 응용 프로그램에 추가 하는 방법, 허브 클래스를 만드는 방법 및 허브에서 메시지를 송수신 하는 방법입니다.

할 수 있습니다 샘플 응용 프로그램은이 자습서 또는 기타 SignalR 응용 프로그램에서 사용할 수 있는 인터넷을 통해 호스팅 공급자에 배포 하 여. Microsoft에서 제공 하는 최대 10 개의 웹 사이트 무료의 무료 웹 호스팅 [Windows Azure 평가판 계정](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)합니다. 연습은 샘플 SignalR 응용 프로그램을 배포 하는 방법에 대해서 [는 SignalR Getting Started 샘플을 Windows Azure 웹 사이트 게시](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx)합니다. Visual Studio 웹 프로젝트를 Windows Azure 웹 사이트를 배포 하는 방법에 대 한 자세한 내용은 참조 하세요. [ASP.NET 응용 프로그램을 Windows Azure 웹 사이트를](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)입니다. (참고: WebSocket 전송이 Windows Azure 웹 사이트에 대 한 현재 지원 되지 않습니다. 사용할 수 없는 경우 WebSocket 전송이, SignalR 전송 부분에 설명 된 대로 사용할 수 있는 다른 전송을 사용 하 여 합니다 [SignalR 항목의 소개](index.md).)

고급 SignalR 개발 개념에 알아보려면 SignalR 소스 코드 및 리소스에 대 한 다음 사이트를 방문 하십시오.

- [SignalR 프로젝트](http://signalr.net)
- [SignalR Github 및 샘플](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
