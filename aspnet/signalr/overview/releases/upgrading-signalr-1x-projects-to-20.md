---
uid: signalr/overview/releases/upgrading-signalr-1x-projects-to-20
title: SignalR 1.x 프로젝트를 버전 2로 업그레이드 | Microsoft Docs
author: pfletcher
description: 이 항목에서는 signalr 기존 SignalR 1.x 프로젝트를 업그레이드 하는 방법에 설명 합니다 2.x 및 업그레이드 프로세스 중 발생할 수 있는 문제를 해결 하는 방법...
ms.author: aspnetcontent
ms.date: 06/10/2014
ms.assetid: adcfef99-9bc5-489d-a91b-9b7c2bc35e04
msc.legacyurl: /signalr/overview/releases/upgrading-signalr-1x-projects-to-20
msc.type: authoredcontent
ms.openlocfilehash: 393beb1ef696bd2dfae25789f79a67157780a219
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37824165"
---
<a name="upgrading-signalr-1x-projects-to-version-2"></a>SignalR 1.x 프로젝트를 버전 2로 업그레이드
====================
[Patrick Fletcher](https://github.com/pfletcher)

> 이 항목에서는 signalr 기존 SignalR 1.x 프로젝트를 업그레이드 하는 방법에 설명 합니다 2.x 및 업그레이드 프로세스 중 발생할 수 있는 문제를 해결 하는 방법입니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR 버전 1과 2
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


SignalR 2를 사용 하 여 서버 플랫폼에서 일관 된 개발 환경을 제공 [OWIN](http://owin.org)합니다. 이 문서에서는 버전 2로 SignalR 1.x 응용 프로그램을 업데이트 하는 데 필요한 몇 가지 단계를 설명 합니다.

SignalR 2로 응용 프로그램을 업그레이드 하는 것이 좋습니다, 있지만 SignalR 1.x를 계속 지원 합니다.

이 자습서에는 SignalR 2를 웹 호스팅 응용 프로그램을 업그레이드 하는 방법을 설명 합니다. (콘솔 응용 프로그램, Windows 서비스 또는 다른 프로세스에서 서버를 호스팅하는) 자체 호스팅된 응용 프로그램은 이제 SignalR 2에서 지원 됩니다. SignalR 2를 사용 하 여 자체 호스팅된 응용 프로그램을 만들기 시작 하는 방법에 대 한 자세한 내용은 [자습서: SignalR 자체 호스팅](../deployment/tutorial-signalr-self-host.md)합니다.

## <a name="contents"></a>목차

다음 섹션에서는 발생할 수 있는 문제를 해결 하는 방법과 SignalR 프로젝트 업그레이드와 관련 된 태스크를 설명 합니다.

- [예: SignalR 2 시작 자습서로](#example)
- [업그레이드 하는 동안 발생 한 오류 문제 해결](#troubleshooting)

<a id="example"></a>

## <a name="example-upgrading-the-getting-started-tutorial-application-to-signalr-2"></a>예: Getting Started tutorial 응용 프로그램 업그레이드에서 SignalR 2

이 섹션에서는에서 만든 응용 프로그램을 업데이트 합니다 [시작 자습서의 SignalR 1.x 버전](../older-versions/index.md) SignalR 2를 사용 하도록 합니다.

1. 시작 자습서를 마친 후 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다. 있는지 확인 합니다 **대상 프레임 워크** 로 설정 된 **.NET Framework 4.5.**
2. 패키지 관리자 콘솔을 엽니다. SignalR 제거 명령을 사용 하 여 프로젝트에서 1.x:

    [!code-powershell[Main](upgrading-signalr-1x-projects-to-20/samples/sample1.ps1)]
3. 다음 명령을 사용 하 여 SignalR 2를 설치 합니다.

    [!code-powershell[Main](upgrading-signalr-1x-projects-to-20/samples/sample2.ps1)]
4. HTML 페이지에 이제 프로젝트에 포함 된 스크립트의 버전과 일치 하도록 SignalR에 대 한 스크립트 참조를 업데이트 합니다.

    [!code-html[Main](upgrading-signalr-1x-projects-to-20/samples/sample3.html)]
5. 전역 응용 프로그램 클래스에서 MapHubs에 대 한 호출을 제거 합니다.

    [!code-csharp[Main](upgrading-signalr-1x-projects-to-20/samples/sample4.cs)]
6. 솔루션을 마우스 오른쪽 단추로 클릭 **추가**, **새 항목...** . 대화 상자에서 선택 **Owin Startup 클래스**합니다. 새 클래스 이름을 **Startup.cs**합니다.

    ![](upgrading-signalr-1x-projects-to-20/_static/image1.png)
7. Startup.cs의 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](upgrading-signalr-1x-projects-to-20/samples/sample5.cs)]

    Owin의 시작 프로세스를 실행 하는 클래스를 추가 하는 어셈블리 특성을 `Configuration` Owin 시작 되 면 메서드. 가 호출 된 `MapSignalR` 메서드를 응용 프로그램에서 모든 SignalR 허브에 대 한 경로 만듭니다.
8. 프로젝트를 실행 하 고 다른 기본 페이지의 URL을 복사 브라우저나 이전 처럼 브라우저 창. 각 페이지는 사용자 이름을 요청 하 고 각 페이지에서 보낸 메시지는 두 브라우저 창에 표시 되어야 합니다.

<a id="troubleshooting"></a>

## <a name="troubleshooting-errors-encountered-during-upgrading"></a>업그레이드 하는 동안 발생 한 오류 문제 해결

이 섹션에서는 업그레이드 하는 동안 발생할 수 있는 문제를 설명 합니다. 오류 보다 포괄적인 목록과 SignalR 응용 프로그램을 사용 하 여 발생할 수 있는 문제를 참조 하세요 [SignalR 문제 해결](../testing-and-debugging/troubleshooting.md)합니다.

### <a name="the-call-is-ambiguous-between-the-following-methods-or-properties"></a>' 호출 되는 다음 메서드 또는 속성 사이 모호한 '

이 오류가 발생 하는 경우에 대 한 참조 `Microsoft.AspNet.SignalR.Owin` 제거 되지 않습니다. 이 패키지는 사용 되지 않습니다. 참조를 제거 해야 하 고 SelfHost 패키지의 1.x 버전을 제거 해야 합니다.

### <a name="hub-methods-fail-silently"></a>허브 메서드를 자동으로 실패

날짜 및는 최대 클라이언트에서 스크립트 참조 되는지 확인 합니다 `OwinStartup` Startup 클래스에는 올바른 클래스와 프로젝트의 어셈블리 이름에 대 한 특성입니다. 또한 열어보세요; 브라우저에서 hubs 주소 (/ signalr 허브) 표시 되는 모든 오류는 무엇이 하는 방법에 대 한 자세한 정보를 제공 합니다.
