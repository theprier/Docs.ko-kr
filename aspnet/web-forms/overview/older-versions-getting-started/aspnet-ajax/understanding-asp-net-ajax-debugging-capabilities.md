---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
title: ASP.NET AJAX 디버깅 기능을 이해 | Microsoft Docs
author: scottcate
description: 코드를 디버깅 하는 기능에서 사용 하는 기술에 관계 없이 해당 무기 모든 개발자 가져야 하는 기술입니다. 대부분의 개발자는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/28/2008
ms.topic: article
ms.assetid: 7f9380c6-19f7-4c82-a019-916ec6dffc9c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
msc.type: authoredcontent
ms.openlocfilehash: f082e2206f5e691579670e42634f30b57e3b3593
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30890933"
---
<a name="understanding-aspnet-ajax-debugging-capabilities"></a>ASP.NET AJAX 디버깅 기능 이해
====================
으로 [Scott 인증서](https://github.com/scottcate)

[PDF 다운로드](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial06_Debugging_MS_Ajax_Applications_cs.pdf)

> 코드를 디버깅 하는 기능에서 사용 하는 기술에 관계 없이 해당 무기 모든 개발자 가져야 하는 기술입니다. 대부분의 개발자는 VISUAL Studio 또는 Web Developer Express를 사용 하 여 VB.NET 또는 C# 코드를 사용 하는 ASP.NET 응용 프로그램 디버깅에 익숙한, 일부 JavaScript 같은 클라이언트 쪽 코드를 디버깅할 때 매우 유용도 없습니다. 동일한 유형의.NET 응용 프로그램을 디버깅 하는 데 사용 되는 기술 AJAX 사용 응용 프로그램 및 좀 더 구체적으로 ASP.NET AJAX 응용 프로그램에도 적용할 수 있습니다.


## <a name="debugging-aspnet-ajax-applications"></a>ASP.NET AJAX 응용 프로그램 디버깅

Dan Wahlin

코드를 디버깅 하는 기능에서 사용 하는 기술에 관계 없이 해당 무기 모든 개발자 가져야 하는 기술입니다. 에 맞는 사용할 수 있는 다양 한 디버깅 옵션을 이해 하 시간에 따라 엄청난 프로젝트와 몇 가지 심지어 headaches에 저장할 수 있습니다. 대부분의 개발자는 VISUAL Studio 또는 Web Developer Express를 사용 하 여 VB.NET 또는 C# 코드를 사용 하는 ASP.NET 응용 프로그램 디버깅에 익숙한, 일부 JavaScript 같은 클라이언트 쪽 코드를 디버깅할 때 매우 유용도 없습니다. 동일한 유형의.NET 응용 프로그램을 디버깅 하는 데 사용 되는 기술 AJAX 사용 응용 프로그램 및 좀 더 구체적으로 ASP.NET AJAX 응용 프로그램에도 적용할 수 있습니다.

이 문서에서 Visual Studio 2008 및 기타 여러 가지 도구로 사용할 수 있는 방법을 버그 및 기타 문제를 빠르게 찾은 ASP.NET AJAX 응용 프로그램을 디버깅 볼 수 있습니다. 이 섹션에는 Internet Explorer 6 이상을 디버깅, Visual Studio 2008 및 스크립트 탐색기를 사용 하 여 코드를 단계별로으로 웹 개발 도우미 등의 다른 사용 가능한 도구를 사용 하 여에 대 한 사용 하도록 설정 하는 방법에 대 한 정보가 포함 됩니다. 또한 Firefox 확장 이라는 Firebug 게 다양 한 도구 없이 브라우저에서 직접 JavaScript 코드를 단계별로 실행 하는 사용 하 여 ASP.NET AJAX 응용 프로그램을 디버깅 하는 방법을 설명 합니다. 마지막으로, 소개 추적 및 코드 어설션 문 등의 다양 한 디버깅 작업에 도움이 되는 ASP.NET AJAX 라이브러리의 클래스에 있습니다.

Internet Explorer에서 본 페이지를 디버그 하려고 하기 전에 디버깅을 위한 사용 하기 위해 수행 해야 하는 몇 가지 기본 단계가 있습니다. 시작 하기 위해 수행 해야 하는 몇 가지 기본 설치 요구 사항에 살펴보겠습니다.

## <a name="configuring-internet-explorer-for-debugging"></a>디버깅을 위한 Internet Explorer 구성

Internet Explorer를 사용 하 여 볼 하는 웹 사이트에서 발생 하는 JavaScript 문제를 거의 보지 대부분의 사람들이 가장 되지 않습니다. 사실, 평균 사용자도 알 수 없습니다는 오류 메시지를 표시 하는 경우 수행할 작업입니다. 결과적으로, 디버깅 옵션은 브라우저에서 기본적으로 비활성화 되어 있습니다. 그러나 되기 디버깅을 사용 하 여 새 AJAX 응용 프로그램을 개발 하는 경우 사용 하도록 설정 하는 매우 간단 합니다.

디버깅 기능을 사용 하려면 Internet Explorer 메뉴 도구 인터넷 옵션으로 이동 하 고 [고급] 탭을 선택 합니다. 검색 섹션 내에서 다음 항목이 선택 되지 않았는지를 확인 합니다.

- 스크립트 디버깅 (Internet Explorer)
- 스크립트 디버깅 (기타)

경우에 필요 하지 않지만 JavaScript 오류가 표시 되 고 분명해 즉시 수의 페이지에 작성할 응용 프로그램을 디버깅 하려고 하 합니다. "모든 스크립트 오류에 대 한 알림 표시" 확인란을 선택 하 여 메시지 상자가 표시 되도록 모든 오류를 강제할 수 있습니다. 응용 프로그램을 개발 하는 동안 켜려면 유용한 옵션 이지만, 효율적인 JavaScript 오류가 발생할 가능성은 다른 웹 사이트를 읽는 데만 하는 경우 번거로울 될 신속 하 게 수 있습니다.

그림 1에서는 고급 대화 상자에서 어떤 Internet Explorer 제대로 디버깅을 위해 구성 된 후 표시 됩니다.


[![디버깅을 위한 Internet Explorer를 구성 합니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image2.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image1.png)

**그림 1**: 디버깅을 위한 Internet Explorer를 구성 합니다.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image3.png))


디버깅 설정 되어 있으면, 일단 라는 스크립트 디버거 보기 메뉴에 표시 되는 새 메뉴 항목을 볼 수 있습니다. 다음 문에서 열기 및 중단 비롯 하 여 사용할 수 있는 두 가지 옵션이 있습니다. 열을 선택 하는 메시지가 표시 됩니다 (참고는 Visual Web Developer Express 사용할 수도 있습니다 디버깅에) Visual Studio 2008에서 페이지를 디버그 하 합니다. Visual Studio.NET 현재 실행 중인 경우 새 인스턴스를 만들지 또는 해당 인스턴스를 사용 하도록 선택할 수 있습니다. 다음 문장에서 중단을 선택 하는 JavaScript 코드를 실행할 때 페이지를 디버그 하 라는 메시지가 표시 합니다. 페이지의 onLoad 이벤트에서 실행 되는 JavaScript 코드를 디버그 세션을 트리거하는 페이지를 새로 고칠 수 있습니다. JavaScript 코드는 단추를 클릭 한 후 실행 단추를 클릭 한 후에 즉시 디버거에서 실행 됩니다.

> *> [!NOTE] 와 액세스 제어 UAC (사용자)을 사용 하는 Windows Vista에서 실행 하는 경우 관리자 권한으로 실행 되도록 설정 하는 Visual Studio 2008을 있으면 Visual Studio 연결 메시지가 표시 되는 경우 프로세스에 연결 되지 것입니다. 이 문제를 해결 하려면 먼저 Visual Studio를 시작 하 고 디버깅 하기 위해 해당 인스턴스를 사용 합니다.*


다음 섹션에서는 Visual Studio 2008 내에서 직접는 ASP.NET AJAX 페이지를 디버깅 하는 방법을 보여 줍니다, 있지만 Internet Explorer 스크립트 디버거 옵션을 사용 하 여 유용 페이지가 이미 열려 있고 보다 완전 하 게 조사 하도록 하려는 경우 합니다.

## <a name="debugging-with-visual-studio-2008"></a>Visual Studio 2008을 사용 하 여 디버깅

Visual Studio 2008는 전 세계 개발자가 디버그.NET 응용 프로그램에 매일 사용 하는 디버깅 기능을 제공 합니다. 기본 제공 디버거를 사용 하면 코드를 호출 스택 및 더 많은 개체 데이터를 특정 변수에 대해서는 조사식 모니터링 보기 수 있습니다. VB.NET 또는 C# 코드를 디버깅 하는 것 외에도 디버거 ASP.NET AJAX 응용 프로그램을 디버깅 하는 데 도움이 되며 여 한 줄씩 JavaScript 코드를 단계별로 실행할 수 있습니다. Visual Studio 2008을 사용 하 여 응용 프로그램을 디버깅 하는 전체 과정에서 discourse 제공 하는 것이 아니라 클라이언트 쪽 스크립트 파일을 디버깅 하는 데 사용할 수 있는 기술에 포커스를 추적 하는 세부 정보.

Visual Studio 2008에서 페이지를 디버깅 하는 과정은 여러 가지 방법으로 시작할 수 있습니다. 첫째, 이전 섹션에 언급 된 Internet Explorer 스크립트 디버거 옵션을 사용할 수 있습니다. 이 페이지는 이미 브라우저에 로드 하 고 디버깅을 시작 하려는 경우에 적합 합니다. 또는 솔루션 탐색기에서.aspx 페이지를 마우스 오른쪽 단추로 클릭 하 고 메뉴에서 시작 페이지로 설정 선택 수 있습니다. ASP.NET 페이지 디버깅에 익숙한 사용자 라면 다음 있습니다 것이 작업을 수행 하기 전에 합니다. F5 키를 누른 후에 페이지를 디버깅할 수 있습니다. 그러나 일반적으로 중단점 설정할 수 있습니다는 아무 곳 이나 동안 되지 않는 JavaScript의 경우 다음 알게 VB.NET 또는 C# 코드에서 하 고 원할 것입니다.

*외부 스크립트 및 포함*

Visual Studio 2008 디버거 외부 JavaScript 파일이 아닌 다른 페이지에 포함 하는 JavaScript를 처리 합니다. 외부 스크립트 파일을 파일 열고 선택한 모든 줄에 중단점을 설정할 수 있습니다. 코드 편집기 창 왼쪽에 회색 트레이에서 영역을 클릭 하 여 중단점을 설정할 수 있습니다. JavaScript를 사용 하 여 페이지에 직접 포함 된 경우는 `<script>` 회색 트레이에서 영역에서 클릭 하 여 중단점을 설정 태그는 좋은 방법이 아닙니다. 포함 된 스크립트의 줄에 중단점을 설정 하려고 "이것은 중단점에 대 한 유효한 위치가 아닙니다" 내용의 경고가 발생 합니다.

외부.js 파일에는 코드 이동의 src 특성을 사용 하 여이 참조 하 여이 문제를 해결할 수 있습니다는 &lt;스크립트&gt; 태그:


[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample1.html)]

외부 파일에는 코드 이동 불가능 또는 것 보다 더 많은 작업이 필요 어떻게 가치가? 편집기를 사용 하 여 중단점을 설정할 수 있지만 디버거 문을 디버깅을 시작 하려는 코드에 직접 추가할 수 있습니다. 시작 하려면 디버깅을 강제로 ASP.NET AJAX 라이브러리에서 사용할 수 있는 Sys.Debug 클래스를 사용할 수 있습니다. 이 문서의 뒷부분에 나오는 Sys.Debug 클래스에 대해 자세히 설명 합니다.

사용 하는 예제는 `debugger` 키워드 목록 1에 표시 됩니다. 이 예에서는 update 함수를 호출 하기 전에 오른쪽 중단 하도록 디버거를 강제로 수행 합니다.

**목록 1입니다. 디버거 키워드를 사용 하는 Visual Studio.NET 디버거를 중단 되도록 합니다.**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample2.js)]

Debugger 문 도달 되 면 Visual Studio.NET을 사용 하 여 페이지를 디버그 하 라는 메시지가 표시 하 고 코드를 단계별로 시작할 수 있습니다. 이제 페이지에서 사용 되는 ASP.NET AJAX 라이브러리 스크립트 파일에 액세스에 문제가 발생할 수 있습니다 하는 동안 Visual Studio를 사용 하 여 살펴보겠습니다. NET의 스크립트 탐색기입니다.

## <a name="using-visual-studio-net-windows-to-debug"></a>Visual Studio.NET Windows를 사용 하 여 디버깅

디버그 세션이 시작 되 고 기본 F11 키를 사용 하 여 코드를 통해 탐색을 시작, 발생할 수 있습니다는 페이지에서 사용 하는 모든 스크립트 파일은 열려 있고 디버깅을 위해 사용 가능 하지 않으면 오류 대화 상자에 표시 된 그림 2 참조.


[![디버깅에 사용할 수 있는 소스 코드가 없는 경우 표시 된 오류 대화 상자입니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image5.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image4.png)

**그림 2**: 디버깅에 사용할 수 있는 소스 코드가 없는 경우 표시 된 오류 대화 상자.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image6.png))


이 대화 상자에 Visual Studio.NET 있는지 일부 페이지에서 참조 하는 스크립트의 소스 코드를 보는 방법에 표시 됩니다. 이 매우 번거로울 수 있지만, 처음에는 간단한 수정 프로그램. 디버그 세션을 시작 하 고 중단점에 도달 했으면, Visual Studio 2008 메뉴에서 Windows 스크립트 탐색기 디버그 창으로 이동 하거나 Ctrl + Alt + N 바로 가기 키를 사용 하 여 합니다.

> *> [!NOTE] 나열 된 스크립트 탐색기 메뉴에 볼 수 없는 경우 도구를 이동* *사용자 지정* *VISUAL Studio 메뉴에서 명령입니다. 범주 섹션에서 디버그 항목을 찾아 모든 사용 가능한 메뉴 항목을 표시 하도록 클릭 합니다. 명령 목록에서 스크립트 탐색기 아래로 스크롤하여 다음으로 끌어와 디버그* *Windows 메뉴에 앞에서 언급 한 합니다. 이 작업을 수행 하면 스크립트 탐색기 메뉴 항목 사용 가능한 VISUAL Studio를 실행할 때마다 있습니다.*


스크립트 탐색기를 사용 하 여를 페이지에 사용 되는 모든 스크립트를 보고 하 여 코드 편집기에서 열 수 있습니다. 스크립트 탐색기를 열면 코드 편집기 창에서 열려는 현재 디버깅 중인.aspx 페이지에서 두 번 클릭 합니다. 스크립트 탐색기에 표시 되는 다른 스크립트의 모든에 대해 같은 작업을 수행 합니다. 모든 스크립트 할 수 있습니다 코드 창에서 열려 있는 되 면 코드를 단계별로 실행 하려면 f 11 누릅니다 (및 다른 디버그 바로 가기 키 사용). 그림 3에는 스크립트 탐색기의 예가 나와 있습니다. 두 개의 사용자 지정 스크립트와 ASP.NET AJAX ScriptManager에서 동적으로 인해 페이지에 삽입 하는 두 개의 스크립트 뿐만 아니라 현재 디버깅 중인 파일 (Demo.aspx)를 나열 합니다.


[![스크립트 탐색기 페이지에서 사용 되는 스크립트에 쉽게 액세스할 수 있습니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image8.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image7.png)

**그림 3**합니다. 스크립트 탐색기 페이지에서 사용 되는 스크립트에 쉽게 액세스할 수 있습니다.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image9.png))


여러 다른 windows 페이지의 코드를 단계별로 실행할 때 유용한 정보를 제공 하 여 사용할 수도 있습니다. 예를 들어 특정 변수 또는 조건을 평가 하 고 출력을 확인 하려면 직접 실행 창 페이지에 사용 되는 서로 다른 변수의 값을 보려면 지역 창에 사용할 수 있습니다. 또한 Sys.Debug.trace 함수 (이 문서의 뒷부분에 나오는 설명한) 또는 Internet Explorer의 Debug.writeln 함수를 사용 하 여 기록 추적 문을 보려면 출력 창을 사용할 수 있습니다.

디버거를 사용 하 여 코드를 단계별로 실행할 때 할당 된 값을 확인 하는 코드에서 변수 위에 마우스를 놓습니다. 그러나 스크립트 디버거 가끔 표시 되지 않습니다 아무 것도 지정 된 JavaScript 변수 위로 마우스를 이동할 때. 값을 보려면 문 또는 코드 편집기 창에 보고 한 다음 위로 마우스를 만들려고 하는 변수를 강조 표시 합니다. 이 기술은 모든 상황에서 작동 하지 않습니다, 하지만 여러 번 됩니다 지역 창과 같은 다른 디버그 창에서 검색 하지 않고도 값을 볼 수 있습니다.

여기서 설명 하는 기능 중 일부를 보여 주는 비디오 자습서에서 볼 수 있습니다 [ http://www.xmlforasp.net ](http://www.xmlforasp.net)합니다.

## <a name="debugging-with-web-development-helper"></a>웹 개발 도우미를 사용 하 여 디버깅

Visual Studio 2008 및 Visual Web Developer Express 2008는 매우 다양 한 디버깅 도구, 있지만 더 간단한 요소인도 사용할 수 있는 추가 옵션이 있습니다. 해제 될 수 있는 최신 도구 중 하나에 웹 개발 도우미입니다. (Microsoft는 주요 ASP.NET AJAX 설계자 중 하나)는 Microsoft의 Nikhil Kothari HTTP 요청 및 응답 메시지를 확인 하 여 간단한 디버깅에서 많은 다양 한 작업을 수행할 수 있도록이 우수한 도구를 썼습니다. 웹 개발 도우미에서 다운로드할 수 있습니다 [ http://projects.nikhilk.net/Projects/WebDevHelper.aspx ](http://projects.nikhilk.net/Projects/WebDevHelper.aspx)합니다.

웹 개발 도우미 Internet Explorer를 사용 하는 데 편리를 직접 사용할 수 있습니다. Internet Explorer 메뉴에서 웹 개발 도우미 도구를 선택 하 여 시작 됩니다. HTTP 요청 및 응답 메시지 로깅 등 여러 가지 작업을 수행 하도록 브라우저를 없으므로 좋은 브라우저의 하단에서 도구가 열립니다. 그림 4는 작업의 웹 개발 도우미 모양을 보여 줍니다.


[![웹 개발 도우미](understanding-asp-net-ajax-debugging-capabilities/_static/image11.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image10.png)

**그림 4**: 웹 개발 도우미 ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image12.png))


웹 개발 도우미 없는 도구를 사용 하 여 한 줄씩으로 Visual Studio 2008과 함께 코드를 단계별로 합니다. 그러나 추적 출력을 표시, 쉽게 스크립트의 변수를 평가할 또는 탐색 사용할 수는 JSON 개체 내의 데이터는 합니다. ASP.NET AJAX 페이지와 서버에서 전달 되는 데이터를 보는 데 매우 유용 이기도 합니다.

웹 개발 도우미를 열면 Internet Explorer에서 스크립트 디버깅이 활성화 메뉴 선택 하 여 스크립트 디버깅 사용 스크립트는 웹 개발 도우미 그림 4에서 설명한 것 처럼 합니다. 이 통해 절편 오류는 페이지가 실행 될 때 발생 하는 도구입니다. 또한이 페이지에서 출력 추적 메시지에 쉽게 액세스할 수 있습니다. 추적 정보를 보거나 페이지 내에서 다양 한 기능을 테스트 하려면 스크립트 명령을 실행 하려면 웹 개발 도우미 메뉴에서 스크립트 콘솔을 표시 하는 스크립트를 선택 합니다. 명령 창 및 간단한 직접 실행 창에 대 한 액세스를 제공합니다.

*추적 메시지 및 JSON 개체 데이터 보기*

직접 실행 창 스크립트 명령을 실행 하거나도 로드 하거나 저장 하려면 페이지에서 다양 한 기능을 테스트 하는 데 사용 되는 스크립트를 사용할 수 있습니다. 명령 창에 표시 되는 페이지에서 기록 하는 추적 또는 디버그 메시지가 표시 됩니다. 목록 2에서는 Internet Explorer의 Debug.writeln 함수를 사용 하 여 추적 메시지를 작성 하는 방법을 보여 줍니다.

**2를 나열 합니다. Debug 클래스를 사용 하 여 클라이언트 쪽 추적 메시지를 작성 합니다.**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample3.js)]

웹 개발 도우미 메시지를 표시 합니다 LastName 속성 Doe의 값이 있으면 "사람 이름: Doe" 스크립트 콘솔의 명령 창 (있는지 디버깅 하도록 설정한 경우)에 있습니다. 또한 웹 개발 도우미 추적 정보를 작성 또는 JSON 개체의 내용을 보는 데 사용할 수 있는 페이지에는 최상위 debugService 개체를 추가 합니다. 코드 3 debugService 클래스의 추적 함수를 사용 하는 예제를 보여 줍니다.

**3을 나열 합니다. 추적 메시지 작성 하는 웹 개발 도우미 debugService 클래스를 사용 합니다.**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample4.js)]

DebugService 클래스의 뛰어난 기능 쉽게 웹 개발 도우미 실행 중일 때 항상 추적 데이터에 액세스할 수 있도록 Internet Explorer에서 활성화 되어 있지 않으면 디버깅 하는 경우에 작동을입니다. 이 도구를 사용 하는 페이지를 디버그 하 되 고 있지, window.debugService에 대 한 호출에서 false를 반환 합니다 이후 trace 문은 무시 됩니다.

DebugService 클래스에서는 또한 JSON 개체 데이터를 웹 개발 도우미의 검사기 창을 사용 하 여 볼 수 있습니다. 목록 4 개인 데이터를 포함 하는 간단한 JSON 개체를 만듭니다. 호출 되는 개체를 만든 후 클래스의는 debugService를 시각적으로 검사 하려면 JSON 개체를 허용 하는 함수를 검사 합니다.

**4를 나열 합니다. DebugService.inspect 함수를 사용 하 여 JSON 개체 데이터를 볼 수 있습니다.**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample5.js)]

그림 5에 표시 된 것 처럼 나타나는 개체 검사기 대화 상자 창에서 직접 실행 창 또는 페이지에서 GetPerson() 함수를 호출 발생 합니다. 속성 개체 내에서, 강조 표시 하 여 동적으로 변경할 수 있습니다 값 텍스트 상자에 표시 되는 값을 변경 하 고 업데이트 링크를 클릭 합니다. 개체 관리자를 사용 하 여은 JSON 개체를 데이터를 보고 속성에 다른 값을 적용할 시험해 간단 하 게 합니다.

*디버깅 오류*

추적 데이터 및 JSON 개체를 표시할 수를 허용 하는 것 외에도 웹 개발 도우미도 오류 페이지에 디버깅에 도움이 될 수 있습니다. 코드의 다음 줄을 계속 하거나 스크립트를 디버그 하 라는 메시지가 표시 오류가 발생 하는 경우 (그림 6 참조). 스크립트 내에 있는 문제를 쉽게 식별할 수 있도록 줄 번호 뿐 아니라 완전 한 호출 스택 스크립트 오류 대화 상자 창 표시 됩니다.


[![개체 검사기 창을 사용 하 여 JSON 개체를 볼 수 있습니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image14.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image13.png)

**그림 5**: 개체 검사기 창을 사용 하 여 JSON 개체를 볼 수 있습니다.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image15.png))


디버그 옵션을 선택 하면 웹 개발 도우미를 변수 값을 보려면 JSON 개체와 더 쓰지 직접 실행 창에서 직접 스크립트 문을 실행할 수 있습니다. 오류를 발생 시킨 같은 작업을 다시 수행 하는 경우 Visual Studio 2008은 시스템에서 디버그 세션을 시작 하 여 한 줄씩 이전 섹션에서 설명한 대로 코드를 단계별로 실행할 수 있습니다 라는 메시지가 표시 됩니다.


[![웹 개발 도우미 스크립트 오류 대화 상자](understanding-asp-net-ajax-debugging-capabilities/_static/image17.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image16.png)

**그림 6**: 웹 개발 도우미 스크립트 오류 대화 상자 ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image18.png))


*요청 및 응답 메시지를 검사합니다.*

ASP.NET AJAX 페이지를 디버깅 하는 동안 유용 페이지와 서버 간에 전송 요청 및 응답 메시지를 확인 합니다. 메시지 내에서 내용 보기를 사용 하면 적절 한 데이터가 메시지의 크기 뿐만 아니라 전달 되는 경우를 볼 수 있습니다. 웹 개발 도우미에서는 손쉽게 원시 텍스트 또는 더 읽기 쉬운 형식 데이터를 볼 수 있는 뛰어난 HTTP 메시지로 거 기능을 제공 합니다.

ASP.NET AJAX 요청 및 응답 메시지를 보려면 웹 개발 도우미 메뉴에서 HTTP 로깅 사용 HTTP를 선택 하 여 HTTP로 거를 활성화 해야 합니다. 활성화 되 면 현재 페이지에서 보낸 모든 메시지는 HTTP 로그를 표시 하는 HTTP를 선택 하 여 액세스할 수 있는 HTTP 로그 뷰어에서 볼 수 있습니다.

각 요청/응답 메시지에 전송 되는 원시 텍스트를 표시 하는 것은 확실히 유용 하지만 (및 웹 개발 도우미에서 옵션), 쉽습니다 더 그래픽 형식으로 메시지 데이터를 볼 수 있습니다. HTTP 로깅을 사용 하도록 설정한 후 메시지가 기록 되었음을 HTTP 로그 뷰어에 메시지를 두 번 클릭 하 여 메시지 데이터를 볼 수 있습니다. 이렇게 하면 실제 메시지 뿐 아니라 메시지와 연결 된 모든 헤더를 볼 수 콘텐츠입니다. 그림 7에는 요청 메시지와 HTTP 로그 뷰어 창에서 응답 메시지의 예가 나와 있습니다.


[![HTTP 로그 뷰어를 사용 하 여 요청 및 응답 메시지 데이터를 볼 수 있습니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image20.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image19.png)

**그림 7**: HTTP 로그 뷰어를 사용 하 여 요청 및 응답 메시지 데이터를 볼 수 있습니다.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image21.png))


HTTP 로그 뷰어는 자동으로 JSON 개체를 구문 분석 하 고 빠르고 쉽게 개체의 속성 데이터를 볼 수 있도록 트리 뷰를 사용 하 여 표시 합니다. UpdatePanel는 ASP.NET AJAX 페이지에서 사용 중인 경우 그림 8 에서처럼 뷰어 개별 부분으로 메시지의 각 부분을 중단 합니다. 이 훌륭한 기능 훨씬 쉽게 파악 하 고 이해할 원시 메시지 데이터 보기와 비교해 서 메시지에 포함 된 내용입니다.


[![HTTP 로그 뷰어를 사용 하 여 볼 UpdatePanel 응답 메시지입니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image23.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image22.png)

**그림 8**: 응답 메시지는 UpdatePanel HTTP 로그 뷰어를 사용 하 여 볼 합니다.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image24.png))


웹 개발 도우미 외에도 요청 및 응답 메시지를 보는 데 사용할 수 있는 다른 여러 도구가 있습니다. 또 다른 좋은 옵션은 Fiddler에서을 무료로 제공 되는 [ http://www.fiddlertool.com ](http://www.fiddlertool.com)합니다. Fiddler는 여기 언급 하지 것입니다, 있지만 것도 좋은 방법 철저 하 게 메시지 헤더 및 데이터를 검사 해야 할 때 합니다.

## <a name="debugging-with-firefox-and-firebug"></a>Firefox 및 Firebug를 사용 하 여 디버깅

Internet Explorer 가장 널리 사용 되는 브라우저 여전히 이지만, Firefox와 같은 다른 브라우저 매우 인기가 하 고 더 많은 사용 되는 합니다. 결과적으로, Firefox 뿐만 아니라 Internet Explorer 응용 프로그램을 제대로 작동 되도록에서 ASP.NET AJAX 페이지 디버그를 보고 합니다. Firefox 디버깅을 위해 Visual Studio 2008에 직접 연결할 수 없습니다, 있지만 호출 Firebug 페이지를 디버깅을 사용할 수 있는 확장을 있습니다. 로 이동 하 여 firebug를 무료로 다운로드할 [ http://www.getfirebug.com ](http://www.getfirebug.com)합니다.

Firebug 여 한 줄씩 코드를 단계별로, 페이지 내에서 사용 되는 모든 스크립트에 액세스 하 고 DOM 구조를 볼, CSS 스타일 및 발생 하는 추적 이벤트에도 페이지에 표시 하는 데 사용할 수 있는 모든 기능을 갖춘 디버깅 환경을 제공 합니다. 설치 되 면 Firebug 도구 Firebug 열려 Firebug Firefox 메뉴에서 선택 하 여 액세스할 수 있습니다. 독립 실행형 응용 프로그램으로도 사용 될 수 있지만 웹 개발 도우미와 같은 Firebug 브라우저에서 직접 사용 됩니다.

Firebug를 실행 하 고 있는지 여부는 스크립트는 페이지에 포함 된 JavaScript 파일의 모든 줄에 중단점 설정할 수 있습니다. 중단점을 설정 하려면 먼저 Firefox에서 디버그 하려면 적절 한 페이지를 로드 합니다. 페이지가 로드 되 면 Firebug의 스크립트 드롭 다운 목록에서 디버그 하는 스크립트를 선택 합니다. 페이지에서 사용 되는 모든 스크립트에 표시 됩니다. 중단점은 중단점 해야 Visual Studio 2008에서 같이 이동 해야 하는 줄에 Firebug의 회색 트레이에서 영역을 클릭 하 여 설정 됩니다.

중단점 Firebug에 설정 되 면 단추를 클릭 하거나 onLoad 이벤트를 트리거할 브라우저를 새로 고쳐 같은 디버그 해야 하는 스크립트를 실행 하는 데 필요한 작업을 수행할 수 있습니다. 실행이 중단점을 포함 하는 줄에 자동으로 중지 됩니다. 그림 9 Firebug에서 트리거 되었습니다 중단점의 예를 보여 줍니다.


[![Firebug에 중단점을 처리 합니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image26.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image25.png)

**그림 9**: Firebug에 중단점을 처리 합니다.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image27.png))


중단점이 적중 되 면 한 단계씩 코드 실행을 건너뛸 또는 화살표 단추를 사용 하 여 코드에서 나갈 수 있습니다. 코드를 단계별로 실행 함에 따라 스크립트 변수 값이 표시 및 개체로 드릴 다운 수 있도록 디버거의 오른쪽 부분에 표시 됩니다. Firebug 디버깅 중인 현재 줄을 초래한 스크립트의 실행 단계를 보려면 호출 스택 드롭 다운 목록도 제공 합니다.

Firebug에는 다른 스크립트 문을 테스트, 변수를 평가 및 추적 출력을 보는 데 사용할 수 있는 콘솔 창이 포함 되어 있습니다. Firebug 창의 맨 아래에 있는 콘솔 탭을 클릭 하 여 액세스 합니다. 디버깅 중인 페이지도 검사할 수 있습니다 "" 검사 탭을 클릭 하 여 DOM 구조 및 내용을 볼 수 있습니다. 때 다양 한 페이지의 적절 한 부분 검사기 창에 표시 된 DOM 요소 위에 마우스를 놓았은 페이지에서 사용 되는 요소 확인까지 쉽게 찾을 수 있습니다. 요소에 서로 다른 두께, 스타일 등을 적용 하 여 시험해 "라이브" 지정된 된 요소와 관련 된 특성 값을 변경할 수 있습니다. 이것이 지속적으로 소스 코드 편집기 및 Firefox 브라우저를 보려면 어떻게 간단한 변경 내용이 영향을 페이지 사이 전환 하지 않아도 절감 되는 유용한 기능입니다.

그림 10에는 DOM 검사기를 사용 하 여 페이지에서 txtCountry 라는 텍스트 상자를 찾을 수의 예가 나와 있습니다. Firebug 관리자도 추적 마우스 이동, 단추 클릭과 같은 발생 하는 이벤트를 비롯 하 여 페이지에 사용 되는 CSS 스타일을 보는 데 사용할 수 있습니다.


[![Firebug의 DOM 관리자를 사용 합니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image29.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image28.png)

**그림 10**:를 사용 하 여 Firebug DOM 검사 합니다.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image30.png))


Firebug를 신속 하 게 페이지 내에서 다양 한 요소를 검사 하는 데 적합 한 도구 뿐만 아니라 Firefox에서 직접 페이지를 디버그 하는 간단한 방법을 제공 합니다.

## <a name="debugging-support-in-aspnet-ajax"></a>ASP.NET ajax에서 디버깅 지원

ASP.NET AJAX 라이브러리가 웹 페이지에 AJAX 기능을 추가 하는 과정을 간소화 하기 위해 사용할 수 있는 여러 클래스를 포함 합니다. 페이지 내에서 요소를 검색 및 조작할 새 컨트롤을 추가, 웹 서비스를 호출 및 이벤트를 처리 하는 이러한 클래스를 사용할 수 있습니다. ASP.NET AJAX 라이브러리에는 디버깅 페이지의 프로세스를 향상 시키기 위해 사용할 수 있는 클래스도 포함 되어 있습니다. 이 섹션에서는 소개 Sys.Debug 클래스 하 고 응용 프로그램에서 사용할 수 있습니다 어떻게 참조 합니다.

*Sys.Debug 클래스를 사용 하 여*

추적 출력을 쓸 코드 어설션을 수행 하 고 코드에 디버깅할 수 있도록 오류를 강제 적용을 포함 하 여 여러 가지 서로 다른 기능을 수행할 Sys.Debug 클래스 (Sys 네임 스페이스에 있는 JavaScript 클래스)를 사용할 수 있습니다. 것 광범위 하 게 파일에 사용 되는 ASP.NET AJAX 라이브러리의 디버그 (기본적으로 C:\Program Files\Microsoft ASP.NET\ASP.NET 2.0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0에 설치) (조건부 검사를 수행 하려면 어설션 라고 함) 매개 변수는 함수, 개체에서 필요한 데이터를 포함 하 고 추적 문을 작성할 수 제대로 전달 되었는지 확인 하는 합니다.

Sys.Debug 클래스는 추적, 코드 어설션 또는 실패로 인해 표 1에 나와 있는 것 처럼 처리 하는 데 사용할 수 있는 다양 한 기능을 노출 합니다.

**표 1입니다. Sys.Debug 클래스 함수입니다.**

| **함수 이름** | **설명** |
| --- | --- |
| assert(condition, message, displayCaller) | 조건 매개 변수가 true 인지를 어설션 합니다. 테스트 하는 조건이 false 이면 메시지 매개 변수 값을 표시 하는 메시지 상자가 사용 됩니다. DisplayCaller 매개 변수가 true 인 경우 메서드는 또한 호출자에 대 한 정보를 표시 합니다. |
| clearTrace() | 문 작업의 결과를를 추적을 지웁니다. |
| fail(message) | 프로그램을 실행을 중지 하 고 디버거를 중단 하면 됩니다. 실패 한 이유를 제공 하 메시지 매개 변수를 사용할 수 있습니다. |
| trace(message) | 추적 출력을 메시지 매개 변수를 씁니다. |
| traceDump (개체, 이름) | 개체의 형식으로 데이터를 읽을 수 있는 출력합니다. Name 매개 변수 레이블을 제공 하기 위해 추적 덤프에 대 한 사용할 수 있습니다. 모든 하위 개체 덤프 되는 개체 내에서 기본적으로 작성 됩니다. |

클라이언트 쪽 추적을 거의 동일한 방법으로 ASP.NET에서 사용할 수 있는 추적 기능에 사용할 수 있습니다. 다양 한 메시지를를 응용 프로그램의 흐름을 중단 하지 않고 쉽게 볼 수 있습니다. 목록 5 Sys.Debug.trace 함수를 사용 하 여 추적 로그에 쓰기의 예를 보여 줍니다. 이 함수는 단순히 매개 변수로 계약을 써야 하는 메시지를 사용 합니다.

**5를 나열 합니다. Sys.Debug.trace 함수를 사용 합니다.**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample6.js)]

목록 5에 표시 된 코드를 실행 하는 경우에 페이지에서 모든 추적 출력을 볼 수 없습니다. 볼 수 있는 유일한 방법은 VISUAL Studio, 웹 개발 도우미 또는 Firebug에서 사용할 수 있는 콘솔 창을 사용 하는 것입니다. 페이지에서 추적 출력을 보려면 않을 경우 다음 해야 TextArea 태그를 추가 하 고 다음 예와 같이 TraceConsole의 id 지정:


[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample7.html)]

페이지에 있는 Sys.Debug.trace 문이 TraceConsole TextArea에 기록 됩니다.

JSON 개체 내에 포함 된 데이터를 저장할 경우에서 Sys.Debug 클래스의 traceDump 함수를 사용할 수 있습니다. 이 함수는 추적 콘솔에 덤프 해야 하는 개체와 추적 출력에서 개체를 식별 하는 데 사용할 수 있는 이름을 포함 하는 두 개의 매개 변수를 사용 합니다. 목록 6 traceDump 함수를 사용 하는 예제를 보여 줍니다.

**6을 나열 합니다. Sys.Debug.traceDump 함수를 사용 합니다.**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample8.js)]

그림 11 Sys.Debug.traceDump 함수 호출의 출력을 보여 줍니다. 사용자 개체의 데이터를 쓰는 외에 쓰는지 주소 하위 개체의 데이터를 확인 합니다.

추적을 외에도 Sys.Debug 클래스 코드 어설션을 수행 하려면 사용 수도 있습니다. 어설션 응용 프로그램이 실행 되는 동안 특정 조건이 충족 되는 테스트 하는 데 사용 됩니다. ASP.NET AJAX 라이브러리 스크립트의 디버그 버전에 여러 포함 assert 다양 한 조건 테스트 합니다.

목록 7 Sys.Debug.assert 함수를 사용 하 여 조건을 테스트 하려면 예를 보여 줍니다. 코드는 사용자 개체를 업데이트 하기 전에 주소 개체는 null 인지 여부를 테스트 합니다.


[![출력 Sys.Debug.traceDump 함수입니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image32.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image31.png)

**그림 11**: Sys.Debug.traceDump 함수의 출력 합니다.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image33.png))


**7을 나열 합니다. Debug.assert 함수를 사용 합니다.**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample9.js)]

어설션이 false이 고 호출자에 대 한 정보를 표시할지 여부를 반환 하는 경우 표시할 메시지를 평가 하는 조건을 포함 하 여 세 개의 매개 변수가 전달 됩니다. 어설션이 실패 하는 경우에 세 번째 매개 변수 되었으면 true 호출자 정보 뿐만 아니라 메시지를 표시 됩니다. 그림 12 목록 7에 표시 된 어설션이 실패 하는 경우 표시 되는 오류 대화 상자 예를 보여 줍니다.

최종 함수를 포함 하는 Sys.Debug.fail입니다. 코드에 스크립트의 특정 줄에서 오류를 강제 적용 하려는 경우 JavaScript 응용 프로그램에서 일반적으로 사용 되는 디버거 문이 아니라 Sys.Debug.fail 호출을 추가할 수 있습니다. Sys.Debug.fail 함수는 다음과 같이 실패 한 이유를 나타내는 단일 문자열 매개 변수를 허용 합니다.


[!code-css[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample10.css)]


[![Sys.Debug.assert 실패 메시지입니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image35.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image34.png)

**그림 12**: A Sys.Debug.assert 오류 메시지입니다.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image36.png))


Sys.Debug.fail 문을 스크립트를 실행 하는 동안 오류가 발생 하면 메시지 매개 변수의 값을 Visual Studio 2008과 같은 디버그 응용 프로그램의 콘솔에 표시 됩니다 및 응용 프로그램을 디버깅 하 라는 메시지가 나타납니다. 이 될 수 있는 매우 유용 하 게 하는 한 가지 경우는 인라인 스크립트에 Visual Studio 2008을 사용 하 여 중단점을 설정할 수 없습니다 하지만 코드를 변수 값을 검사할 수 있도록 특정 줄에서 중지 하려는 경우.

*ScriptManager 컨트롤 ScriptMode 속성 이해*

ASP.NET AJAX 라이브러리에서는 디버그 및 릴리스 기본적으로 C:\Program Files\Microsoft ASP.NET\ASP.NET 2.0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0에 설치 된 스크립트 버전입니다. 디버그 스크립트 좋고, 쉽게 읽을 수 있으며 있는 여러 개의 Sys.Debug.assert 호출에 흩어져 해당 릴리스 스크립트 공백 제거 있고의 전체 크기를 최소화 하기 위해 Sys.Debug 클래스를 제한적으로 사용 하는 동안.

ASP.NET AJAX 페이지에 추가 된 ScriptManager 컨트롤 라이브러리 로드할 스크립트의 버전을 확인 하려면 web.config에 컴파일 요소 디버그 특성을 읽습니다. 그러나 경우를 제어할 수 있습니다 디버그 또는 릴리스 스크립트는 로드 (라이브러리 스크립트 또는 사용자 지정 스크립트) ScriptMode 속성을 변경 하 여 합니다. ScriptMode는 ScriptMode 열거형 멤버가 포함 자동, 디버그, 릴리스 및 상속을 허용 합니다.

ScriptMode는 ScriptManager web.config에서 debug 특성을 확인 합니다 즉 자동 값이 기본값으로 사용 됩니다. 디버그가 false 인 경우 ScriptManager ASP.NET AJAX 라이브러리 스크립트의 릴리스 버전을 로드 합니다. 디버그 참인 경우 스크립트의 디버그 버전을 로드 됩니다. 임대 해제 또는 디버그 ScriptMode 속성을 변경 하면 디버그 특성 web.config는 어떤 값에 관계 없이 적절 한 스크립트를 로드 하도록 ScriptManager 시작. 8 나열 ScriptManager 컨트롤을 사용 하 여 ASP.NET AJAX 라이브러리에서 스크립트 디버그를 로드 하는 예제를 보여 줍니다.

**8를 나열 합니다. ScriptManager를 사용 하 여 디버그 스크립트 로드**합니다.


[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample11.aspx)]

또한 목록 9에 표시 된 대로 ScriptReference 구성 요소와 함께 ScriptManager의 스크립트 속성을 사용 하 여 사용자 지정 스크립트의 다른 버전 (예: 디버그 또는 릴리스)를 로드할 수 있습니다.

**9를 나열 합니다. ScriptManager를 사용 하 여 사용자 지정 스크립트를 로드 합니다.**


[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample12.aspx)]

> [!NOTE]
> ScriptReference 구성 요소를 사용 하 여 사용자 지정 스크립트를 로드 하는 경우 스크립트는 스크립트의 맨 아래에 다음 코드를 추가 하 여 로드가 완료 하는 경우 ScriptManager를 알려야 합니다.


[!code-csharp[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample13.cs)]

목록 9에 표시 된 코드 지시 ScriptManager 사용자 스크립트의 디버그 버전에 대 한 보려는 Person.debug.js Person.js 대신에 대 한 자동으로 검색 됩니다. 없으면 Person.debug.js 파일 오류가 발생 합니다.

디버그 나 ScriptManager 컨트롤에 설정 ScriptMode 속성의 값을 기준으로 로드할 사용자 지정 스크립트의 릴리스 버전의 경우에서 상속으로 ScriptReference 컨트롤의 ScriptMode 속성을 설정할 수 있습니다. 이렇게 하면 로드 되도록 사용자 지정 스크립트의 적절 한 버전 목록 10 에서처럼 ScriptManager의 ScriptMode 속성에 따라 합니다. 디버그에 ScriptManager 컨트롤의 ScriptMode 속성이 설정 되어 있지만 Person.debug.js 스크립트를 로드 하 고 웹 페이지에서 사용 됩니다.

**10을 나열 합니다. 사용자 지정 스크립트에 대 한 ScriptManager에서는 ScriptMode를 상속 합니다.**


[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample14.aspx)]

ScriptMode 속성을 적절 하 게 사용 하 여 응용 프로그램을 디버깅 하 고 전체 프로세스를 간소화 보다 쉽게 수입니다. ASP.NET AJAX 라이브러리의 릴리스 스크립트는 대신 단계별로 실행 하 고 코드 서식이 제거 된 디버그 스크립트 디버깅을 위해에는 구체적으로 지정 하는 동안 후 읽기 하기가 어렵습니다.

## <a name="conclusion"></a>결론

Microsoft의 ASP.NET AJAX 기술은 최종 사용자의 전반적인 성능이 향상 시킬 수 있는 AJAX 사용 응용 프로그램을 구축 하기 위한 견고한 토대를 제공 합니다. 그러나로 모든 프로그래밍 기술을 사용 하면 버그 및 다른 응용 프로그램 문제 확실히 발생 합니다. 다른 디버깅 옵션에 대해 알고 있으면 보다 안정적 제품 많은 시간과 결과 절약할 수 있습니다.

이 문서에서 Visual Studio 2008, 웹 개발 도우미 Firebug와 Internet Explorer를 포함 하 여 ASP.NET AJAX 페이지 디버깅을 위한 여러 가지 방법을를 파악 했으므로 합니다. 이러한 도구는 변수 데이터에 액세스 하 여 한 줄씩 코드를 단계별로 고 trace 문을 볼 수 있습니다 이므로 전체 디버깅 프로세스를 간소화할 수 있습니다. 설명 하는 다른 디버깅 도구를 외에 응용 프로그램에서 ASP.NET AJAX 라이브러리 Sys.Debug 클래스를 사용할 수 있는 방법 및을 로드할 ScriptManager 클래스를 사용할 수 있습니다 어떻게 디버그 또는 릴리스 버전의 스크립트 있을 것입니다.

## <a name="bio"></a>약력

Dan Wahlin (Microsoft 가장 중요 한 Professional ASP.NET 및 XML 웹 서비스)는 기술 교육 인터페이스에서.NET 개발 강사 및 아키텍처 컨설턴트 ([www.interfacett.com)](http://www.interfacett.com)합니다. Dan ASP.NET 개발자 웹 사이트에 대 한 XML을 기초로 ([www.XMLforASP.NET](http://www.XMLforASP.NET)), INETA 스피커 Bureau에 및 여러 강연 합니다. Dan Professional Windows DNA (Wrox) ASP.NET을 함께 작성: 팁, 자습서 및 코드 (Sam), ASP.NET 1.1 내부자 솔루션, Professional ASP.NET 2.0 AJAX (Wrox), ASP.NET 2.0 MVP 해킹 및 ASP.NET 개발자 (Sam)에 대 한 작성 된 XML입니다. 그 코드, 문서 또는 책을 기록 하지 않습니다, 작성 및 음악 기록 및 재생 있고 그의 아내와 어린이 야구 Dan 이용할 수 있습니다.

Scott 인증서의 근무 기간이 Microsoft 웹 기술을 1997 년부터 이며 myKB.com 부서장 ([www.myKB.com](http://www.myKB.com)) ASP.NET 작성 i 여기서 기반 응용 프로그램 기술 자료 소프트웨어 솔루션에 집중 합니다. Scott에 전자 메일을 통해 연결할 수 [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com) 또는에서 그의 블로그 [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [이전](understanding-asp-net-ajax-web-services.md)
