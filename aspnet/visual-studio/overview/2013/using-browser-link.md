---
uid: visual-studio/overview/2013/using-browser-link
title: Visual Studio 2013의 브라우저 링크를 사용 하 여 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/04/2013
ms.topic: article
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: e5a13405a303580ec8c1d4cdacafc26c6f8ff34a
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28044112"
---
<a name="using-browser-link-in-visual-studio-2013"></a>Visual Studio 2013의 브라우저 링크를 사용 하 여
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

브라우저 링크는 개발 환경 및 하나 이상의 웹 브라우저 간에 통신 채널을 만드는 Visual Studio 2013의 새로운 기능입니다. 다중 브라우저 테스트에 대 한 유용한 여러 브라우저에서 웹 응용 프로그램 한 번에 새로 고치려면 브라우저 링크를 사용할 수 있습니다.

- [브라우저 새로 고침](#browser-refresh)
- [브라우저 링크 대시보드 보기](#dashboard)
- [정적 HTML 파일에 대 한 브라우저 링크를 사용 하도록 설정](#static-html)
- [브라우저 링크를 사용 하지 않도록 설정](#disabling)
- [어떻게 작동 합니까?](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a>브라우저 새로 고침

브라우저 새로 고침와 브라우저 링크를 통해 Visual Studio에 연결 되어 있는 여러 브라우저를 새로 고칠 수 있습니다.

브라우저 새로 고침을 사용 하려면 먼저 프로젝트 템플릿 중 하나를 사용 하 여 ASP.NET 응용 프로그램을 만듭니다. F5 키를 누르거나 도구 모음에 있는 화살표 아이콘을 클릭 하 여 응용 프로그램을 디버깅 합니다.

![](using-browser-link/_static/image1.png)

디버깅에 대 한 특정 브라우저 선택 드롭다운을 사용할 수도 있습니다.

![](using-browser-link/_static/image2.png)

여러 브라우저를 디버깅 하려면 선택 **브라우저**합니다. 에 **브라우저** 대화 상자에서 둘 이상의 브라우저를 선택 하려면 CTRL 키를 보류 합니다. 클릭 **찾아보기** 선택한 브라우저를 사용 하 여 디버그 하 합니다. 브라우저 링크는 Visual Studio 외부에서 브라우저를 시작 하 고 응용 프로그램 URL로 이동 하는 경우에 작동 합니다.

![](using-browser-link/_static/image3.png)

브라우저 링크 컨트롤은 순환 화살표 아이콘으로 드롭다운 목록에 있습니다. 화살표 아이콘은는 **새로 고침** 단추입니다.

![](using-browser-link/_static/image4.png)

브라우저에서 어떤 연결을 보려면 위로 마우스를 가져가고는 **새로 고침** 디버깅 하는 동안 단추입니다. 연결 된 브라우저 도구 설명 창에 표시 됩니다.

![](using-browser-link/_static/image5.png)

연결 된 브라우저를 새로 고치려면 클릭는 **새로 고침** 단추 또는 CTRL + ALT + ENTER를 누릅니다. 예를 들어 다음 스크린 샷에서 MVC 5 프로젝트 템플릿을 사용 하 여 만든 ASP.NET 프로젝트를 보여 줍니다. 위쪽에서 두 개의 브라우저에서 실행 중인 응용 프로그램을 볼 수 있습니다. 아래쪽에서 프로젝트가 Visual Studio에서 열려 있습니다.

![](using-browser-link/_static/image6.png)

변경한 다음 Visual Studio에서의 &lt;h1&gt; 홈 페이지에 대 한 제목:

![](using-browser-link/_static/image7.png)

클릭 시는 **새로 고침** 단추 변경에서는 브라우저 창에 표시 되었습니다.

![](using-browser-link/_static/image8.png)

**참고**

- 브라우저 링크를 사용 하려면 설정 `debug=true` 에 [ &lt;컴파일&gt; ](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) 프로젝트의 Web.config 파일의 요소입니다.
- 응용 프로그램은 로컬 호스트에서 실행 되어야 합니다.
- 응용 프로그램.NET 4.0 이상을 대상으로 해야 합니다.

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a>브라우저 링크 대시보드 보기

브라우저 링크 대시보드에 브라우저 링크 연결에 대 한 정보를 표시 됩니다. 대시보드를 보려면 브라우저 링크 드롭다운 메뉴를 선택 (옆에 있는 작은 화살표는 **새로 고침** 단추). 클릭 **브라우저 링크 대시보드에**합니다.

![](using-browser-link/_static/image9.png)

대시보드는 연결 된 브라우저와 각 브라우저가 탐색 하는 URL을 나열 합니다.

![](using-browser-link/_static/image10.png)

**필수 구성 요소** 섹션에서는 해당 프로젝트에 대 한 브라우저 링크를 사용 하는 데 필요한 모든 단계를 보여 줍니다. 예를 들어 다음 스크린샷은 프로젝트 "debug" 설정 되어 있는 false로 Web.config 파일에 있습니다.

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a>정적 HTML 파일에 대 한 브라우저 링크를 사용 하도록 설정

브라우저 링크에 정적 HTML 파일을 사용 하려면 다음 Web.config 파일을 추가 합니다.

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

성능상의 이유로 프로젝트를 게시할 때이 설정을 제거 합니다.

<a id="disabling"></a>
## <a name="disabling-browser-link"></a>브라우저 링크를 사용 하지 않도록 설정

브라우저 링크는 기본적으로 사용 됩니다. 여러 가지 방법으로 사용 하지 않도록.

- 브라우저 링크 드롭다운 메뉴에서의 선택을 취소 **브라우저 링크를 사용 하도록 설정**합니다. 

    ![](using-browser-link/_static/image12.png)
- Web.config 파일에서 "vs: EnableBrowserLink"와 "false" 값 appSettings 섹션에서 키를 추가 합니다. 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- Web.config 파일에 디버그를 false로 설정 합니다. 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a>어떻게 작동 합니까?

브라우저 링크를 사용 하 여 [SignalR](../../../signalr/index.md) Visual Studio 및 브라우저 간 통신 채널을 만듭니다. 브라우저 링크를 사용 하는 Visual Studio는 여러 명의 클라이언트 (브라우저)에 연결할 수 있는 SignalR 서버로 작동 합니다. 브라우저 링크는 또한 asp.net HTTP 모듈을 등록합니다. 이 모듈에는 특수 삽입 합니다. &lt;스크립트&gt; 서버에서 모든 페이지 요청에 대 한 참조입니다. 브라우저에서 "소스 보기"를 선택 하 여 스크립트 참조를 확인할 수 있습니다.

![](using-browser-link/_static/image13.png)

소스 파일을 수정 되지 않습니다. HTTP 모듈 스크립트 참조를 동적으로 삽입합니다.

모든 브라우저에서 작동 하는 모든 JavaScript 브라우저 쪽 코드 이므로 [SignalR 지원](../../../signalr/overview/getting-started/supported-platforms.md), 모든 브라우저 플러그 인을 요구 하지 않고 있습니다.
