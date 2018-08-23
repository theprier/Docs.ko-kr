---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: '자습서: SignalR 자체 호스팅 | Microsoft Docs'
author: pfletcher
description: 이 자습서에는 SignalR 2 자체 호스팅된 서버를 만드는 방법과 JavaScript 클라이언트에 연결 하는 방법을 보여 줍니다. 소프트웨어 버전 V 자습서에서 사용 하는 중...
ms.author: riande
ms.date: 06/10/2014
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: 5d7d485357a6c820f11e0135e2ff9479c1965d96
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836136"
---
<a name="tutorial-signalr-self-host"></a>자습서: SignalR 자체 호스팅
====================
[Patrick Fletcher](https://github.com/pfletcher)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/SignalR-Self-Host-Sample-6da0f383)

> 이 자습서에는 SignalR 2 자체 호스팅된 서버를 만드는 방법과 JavaScript 클라이언트에 연결 하는 방법을 보여 줍니다.
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
> ## <a name="questions-and-comments"></a>질문이 나 의견이 있으면
> 
> 이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요. 에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


## <a name="overview"></a>개요

SignalR 서버는 일반적으로 IIS에서 ASP.NET 응용 프로그램에서 호스팅되지만 자체 호스트 될 수도 있습니다 (예: 콘솔 응용 프로그램 또는 Windows 서비스)는 자체 호스트 라이브러리를 사용 하 여 합니다. 모든 SignalR 2와 같은이 라이브러리는 OWIN 기반 ([Open Web Interface for.NET](http://owin.org)). OWIN은.NET 웹 서버 및 웹 응용 프로그램 간의 추상화를 정의합니다. OWIN 이상적인 OWIN 자체 IIS 외부에서 사용자 고유의 프로세스에서 웹 응용 프로그램을 호스팅하는 서버에서 웹 응용 프로그램을 분리 합니다.

IIS에서 호스트 하지 이유는 다음과 같습니다.

- 여기서 IIS 없거나 사용할 수 없는 IIS 없이 기존 서버 팜에 같은 바람직하지 환경입니다.
- IIS의 성능 오버 헤드를 방지 해야 합니다.
- SignalR 기능은 Windows 서비스, Azure 작업자 역할 또는 다른 프로세스에서 실행 되는 기존 응용 프로그램을 추가할 수 있습니다.

성능상의 이유로 self-host으로 솔루션을 개발 하는 경우는 것이 좋습니다 테스트도 성능 혜택을 확인 하려면 IIS에서 호스트 된 응용 프로그램을입니다.

이 자습서는 다음 섹션이 포함 되어 있습니다.

- [서버 만들기](#server)
- [JavaScript 클라이언트와 서버에 액세스](#js)

<a id="server"></a>

## <a name="creating-the-server"></a>서버 만들기

이 자습서에서는 콘솔 응용 프로그램에서 호스트 되는 서버를 만들어야 하지만 모든 종류의 Windows 서비스 또는 Azure 작업자 역할 등의 프로세스에서 서버를 호스팅할 수 있습니다. SignalR의 서버에 Windows 서비스 호스팅에 대 한 샘플 코드를 보려면 [Windows 서비스에서 Self-Hosting SignalR](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3)합니다.

1. 관리자 권한으로 Visual Studio 2013을 엽니다. 선택 **파일**하십시오 **새 프로젝트**합니다. 선택 **Windows** 아래를 **Visual C#** 에서 노드를 **템플릿** 창과 선택 합니다 **콘솔 응용 프로그램** 템플릿. 새 프로젝트 "SignalRSelfHost" 이름을 지정 하 고 클릭 **확인**합니다.

    ![](tutorial-signalr-self-host/_static/image1.png)
2. 선택 하 여 라이브러리 패키지 관리자 콘솔을 엽니다 **도구**, **라이브러리 패키지 관리자**하십시오 **패키지 관리자 콘솔**합니다.
3. 패키지 관리자 콘솔에서 다음 명령을 입력 합니다.

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    이 명령은 프로젝트에 SignalR 2 여 라이브러리를 추가합니다.
4. 패키지 관리자 콘솔에서 다음 명령을 입력 합니다.

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    이 명령은 프로젝트에 Microsoft.Owin.Cors 라이브러리를 추가합니다. 이 라이브러리는 SignalR 및 웹 페이지에 있는 클라이언트 서로 다른 도메인에 호스트 하는 응용 프로그램에 필요한 도메인 간 지원을 위해 사용 됩니다. 호스팅한다고 SignalR 서버와 다른 포트에서 웹 클라이언트, 되므로 해당 도메인 간 이러한 구성 요소 간의 통신에 사용 하도록 설정 해야 합니다.
5. Program.cs의 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    위의 코드는 세 가지 클래스가 포함 되어 있습니다.

    - **프로그램**등의 **Main** 주 실행 경로 정의 하는 메서드. 이 방법에서는 웹 응용 프로그램 유형의 **시작** 지정된 된 URL에서 시작 됩니다 (`http://localhost:8080`). 끝점에서 보안에 필요한 경우에 SSL은 구현할 수 있습니다. 참조 [방법: SSL 인증서로 포트 구성](https://msdn.microsoft.com/library/ms733791.aspx) 자세한 내용은 합니다.
    - **시작**, SignalR server에 대 한 구성을 포함 하는 클래스 (이 자습서에서는 구성 하는 데 `UseCors`), 및에 대 한 호출 `MapSignalR`, 프로젝트의 모든 허브 개체에 대 한 경로 만드는.
    - **MyHub**, 응용 프로그램 클라이언트에 제공 하는 SignalR 허브 클래스입니다. 이 클래스는 단일 메서드 **보낼**, 클라이언트는 다른 모든 연결 된 클라이언트에 메시지를 브로드캐스팅하 호출 합니다.
6. 응용 프로그램을 컴파일하고 실행합니다. 주소는 서버에서 실행 하는 콘솔 창에 표시 됩니다.

    ![](tutorial-signalr-self-host/_static/image2.png)
7. 예외를 사용 하 여 실행이 실패 하면 `System.Reflection.TargetInvocationException was unhandled`, 관리자 권한으로 Visual Studio를 다시 시작 해야 합니다.
8. 다음 섹션으로 계속 진행 하기 전에 응용 프로그램을 중지 합니다.

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a>JavaScript 클라이언트와 서버에 액세스

이 섹션에서는 같은 JavaScript 클라이언트에서 사용 하는 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md)합니다. 클라이언트에 허브 URL을 명시적으로 정의 하는 한 번 수정만 확인 합니다. 자체 호스팅 응용 프로그램의 경우 서버 반드시 수 없습니다 (역방향 프록시 및 부하 분산 장치)으로 인해 연결 URL와 동일한 주소에 있으므로 명시적으로 정의 URL 요구 사항.

1. **솔루션 탐색기**, 솔루션을 마우스 오른쪽 단추로 **추가**하십시오 **새 프로젝트**합니다. 선택 합니다 **웹** 노드를 차례로 선택 합니다 **ASP.NET 웹 응용 프로그램** 템플릿. "JavascriptClient" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

    ![](tutorial-signalr-self-host/_static/image3.png)
2. 선택 된 **빈** 템플릿과 나머지 옵션은 선택 하지 않은 상태로 둡니다. 선택 **프로젝트를 만들**합니다.

    ![](tutorial-signalr-self-host/_static/image4.png)
3. 패키지 관리자 콘솔에서에서 "JavascriptClient" 프로젝트를 선택 합니다 **기본 프로젝트** 드롭다운 목록에서 다음 명령을 실행:

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    이 명령은 클라이언트에 필요한 SignalR 및 JQuery 라이브러리를 설치 합니다.
4. 선택한 서버 프로젝트를 마우스 오른쪽 단추로 클릭 **추가**하십시오 **새 항목**합니다. 선택 된 **웹** 노드와 HTML 페이지를 선택 합니다. 페이지의 이름을 **Default.html**합니다.

    ![](tutorial-signalr-self-host/_static/image5.png)
5. 새 HTML 페이지의 내용을 다음 코드로 바꿉니다. 스크립트 참조를 프로젝트의 Scripts 폴더에서 스크립트와 일치 하는지 확인 합니다.

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    (위의 코드 예제에서 강조 표시 됨) 다음 코드는 (외에도 코드 SignalR 버전 2 beta로 업그레이드) 과장 된 시작 자습서에 사용 되는 클라이언트에 대 한 추가 합니다. 이 코드 줄 SignalR에 대 한 기본 연결 URL을 서버에 명시적으로 설정합니다.

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **시작 프로젝트 설정...** . 선택 합니다 **여러 개의 시작 프로젝트** 라디오 단추를 선택한 두 프로젝트의 설정 **동작** 에 **시작**합니다.

    ![](tutorial-signalr-self-host/_static/image6.png)
7. "Default.html"를 마우스 오른쪽 단추로 클릭 하 고 선택 **시작 페이지로 설정**합니다.
8. 응용 프로그램을 실행합니다. 서버 및 페이지 시작 됩니다. 웹 페이지를 다시 로드 해야 할 수 있습니다 (누르거나 **계속** 디버거에서) 서버를 시작 하기 전에 페이지가 로드 되 면 합니다.
9. 브라우저에서 메시지가 표시 되 면 사용자 이름을 제공 합니다. 다른 브라우저 탭 또는 창에 페이지의 URL을 복사 하 고 다른 사용자 이름을 제공 합니다. 시작 자습서와 같이 다른 브라우저 창에서 메시지를 보낼 수 없게 됩니다.
