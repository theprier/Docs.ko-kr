---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
title: ASP.NET AJAX 디버깅 기능 이해 | Microsoft Docs
author: scottcate
description: 코드를 디버그 하는 기능은 모든 개발자를 사용 하는 기술에 상관 없이 해당 셈에 있어야 하는 기술입니다. 대부분의 개발자는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/28/2008
ms.topic: article
ms.assetid: 7f9380c6-19f7-4c82-a019-916ec6dffc9c
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
msc.type: authoredcontent
ms.openlocfilehash: 533eb8d2faf735915fa5cf5044db09d0ab636938
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37390974"
---
<a name="understanding-aspnet-ajax-debugging-capabilities"></a>ASP.NET AJAX 디버깅 기능 이해
====================
[Scott Cate](https://github.com/scottcate)

[PDF 다운로드](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial06_Debugging_MS_Ajax_Applications_cs.pdf)

> 코드를 디버그 하는 기능은 모든 개발자를 사용 하는 기술에 상관 없이 해당 셈에 있어야 하는 기술입니다. 대부분의 개발자는 익숙한 VB.NET 또는 C# 코드를 사용 하는 ASP.NET 응용 프로그램을 디버깅 하려면 VISUAL Studio 또는 Web Developer Express를 사용 하 여, 일부 JavaScript와 같은 클라이언트 쪽 코드를 디버깅할 때 매우 유용도 없습니다. 또한 AJAX 지원 응용 프로그램 및 좀 더 구체적으로 ASP.NET AJAX 응용 프로그램에 동일한 유형의.NET 응용 프로그램을 디버그 하는 데 사용 되는 기법을 적용할 수 있습니다.


## <a name="debugging-aspnet-ajax-applications"></a>ASP.NET AJAX 응용 프로그램 디버깅

Dan Wahlin

코드를 디버그 하는 기능은 모든 개발자를 사용 하는 기술에 상관 없이 해당 셈에 있어야 하는 기술입니다. 두 말할 필요도 없이 사용할 수 있는 다양 한 디버깅 옵션을 이해는 엄청난 시간 이보다 몇 가지 골치 아픈 문제를 프로젝트에 저장할 수 있습니다. 대부분의 개발자는 익숙한 VB.NET 또는 C# 코드를 사용 하는 ASP.NET 응용 프로그램을 디버깅 하려면 VISUAL Studio 또는 Web Developer Express를 사용 하 여, 일부 JavaScript와 같은 클라이언트 쪽 코드를 디버깅할 때 매우 유용도 없습니다. 또한 AJAX 지원 응용 프로그램 및 좀 더 구체적으로 ASP.NET AJAX 응용 프로그램에 동일한 유형의.NET 응용 프로그램을 디버그 하는 데 사용 되는 기법을 적용할 수 있습니다.

이 문서의 Visual Studio 2008 및 여러 다른 도구 사용할 수 있는 방법을 버그 및 기타 문제를 빠르게 찾은 ASP.NET AJAX 응용 프로그램 디버그에 표시 됩니다. 이 문서에는 Internet Explorer 6 이상 디버깅, Visual Studio 2008 및 스크립트 탐색기를 사용 하 여 코드를 단계별로 실행할 뿐만 아니라 Web Development Helper와 같은 다른 무료 도구를 사용 하 여 사용 하도록 설정 하는 방법에 대 한 정보가 포함 됩니다. 또한 Firefox 확장 이라는 Firebug 다른 도구 없이 브라우저에서 직접 JavaScript 코드를 단계별로 실행할 수 있는 사용 하 여 ASP.NET AJAX 응용 프로그램을 디버그 하는 방법을 알아봅니다. 마지막으로, 있습니다 추적 및 코드 어설션 문 등의 다양 한 디버깅 작업에 도움이 되는 ASP.NET AJAX 라이브러리의 클래스를 도입 될 것입니다.

Internet Explorer에서 페이지를 디버깅 하려고 하기 전에 몇 가지 기본 단계가 디버깅을 위한 사용 하기 위해 수행 해야 합니다. 시작 하기 위해 수행 해야 하는 일부 기본 설정 요구 사항에 살펴보겠습니다.

## <a name="configuring-internet-explorer-for-debugging"></a>디버깅을 위한 Internet Explorer 구성

대부분의 사람들이 볼 Internet Explorer를 사용 하 여 웹 사이트에서 발생 하는 JavaScript 문제를 보려고 하지 않습니다. 사실, 평균 사용자 줬 오류가 발생 하는 경우 수행할 작업을 알고도 하지 않습니다. 결과적으로, 디버깅 옵션은 브라우저에서 기본적으로 해제 되어 있습니다. 그러나 것 디버깅을 사용 하 여 새 AJAX 응용 프로그램을 개발 하는 경우 사용 하도록 하는 매우 간단 합니다.

디버깅 기능을 사용 하려면 Internet Explorer 메뉴의 도구 인터넷 옵션으로 이동 하 고 [고급] 탭을 선택 합니다. 검색 섹션에서 다음 항목이 선택 되지 않았는지 확인 합니다.

- 스크립트 디버깅 (Internet Explorer)를 사용 하지 않도록 설정
- 스크립트 디버깅 (기타)를 사용 하지 않도록 설정

하지만 경우에 필요 하지 않습니다 페이지에 표시 되 고 분명해 즉시 수 있는 모든 JavaScript 오류 싶을 응용 프로그램을 디버그 하려는 합니다. 모든 오류는 "모든 스크립트 오류에 대 한 알림 표시" 확인란을 선택 하 여 메시지 상자를 사용 하 여 표시를 할 수 있습니다. 응용 프로그램을 개발 하는 동안 설정 하는 좋은 옵션 이지만, JavaScript 오류가 발생할 가능성은 매우 좋은 하므로 다른 웹 사이트를 읽는 데만 하는 경우 성가신 해질 수 있습니다.

그림 1에서는 어떤 Internet Explorer 대화 상자 고급 디버깅에 대 한 제대로 구성 된 후에 표시 됩니다.


[![디버깅을 위한 Internet Explorer를 구성 합니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image2.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image1.png)

**그림 1**: 디버깅을 위한 Internet Explorer를 구성 합니다.  ([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-debugging-capabilities/_static/image3.png))


디버깅을 설정한, 되 면 스크립트 디버거 라는 보기 메뉴에 표시 되는 새 메뉴 항목을 볼 수 있습니다. 다음 문에서 열고 중단 비롯 하 여 사용할 수 있는 두 가지 옵션이 있습니다. 오픈을 선택한 경우 Visual Studio 2008 (참고는 Visual Web Developer Express 사용할 수도 있습니다 디버깅용)에서 페이지를 디버그 하 라는 메시지가 됩니다. Visual Studio는 현재 실행 중인 경우 해당 인스턴스를 사용 하거나 새 인스턴스를 만들고 선택할 수 있습니다. 다음 문장에서 중단을 선택 하면 JavaScript 코드를 실행할 때 페이지를 디버그 하 라는 메시지가 됩니다. 페이지의 onLoad 이벤트의 JavaScript 코드를 실행 하는 경우 디버그 세션을 트리거하려면 페이지를 새로 고칠 수 있습니다. JavaScript 코드는 단추를 클릭 한 후 실행 되 면 단추를 클릭 한 후에 즉시 디버거가 실행 됩니다.

> *> [!NOTE] 사용 하 여 액세스 제어 (UAC (사용자)을 사용 하는 Windows Vista에서 실행 하는 경우 관리자 권한으로 실행 되도록 설정 하는 Visual Studio 2008 있으면, Visual Studio 연결 하 라는 메시지가 나타나면 프로세스에 연결 하지 못합니다. 이 문제를 해결 하려면 먼저 Visual Studio를 시작 하 고 해당 인스턴스를 사용 하 여 디버그 합니다.*


다음 섹션에서는 Visual Studio 2008 내에서 직접 ASP.NET AJAX 페이지를 디버그 하는 방법을 보여 줍니다, 하지만 Internet Explorer 스크립트 디버거 옵션을 사용 하 여 유용 페이지가 이미 열려 있고 자세히 검사 하려는 경우.

## <a name="debugging-with-visual-studio-2008"></a>Visual Studio 2008을 사용 하 여 디버깅

Visual Studio 2008는 전 세계 개발자가.NET 응용 프로그램 디버그를 매일 사용 하는 디버깅 기능을 제공 합니다. 기본 제공 디버거를 사용 하면 코드를 호출 스택 및 등을 모니터링 하는 개체 데이터를 특정 변수에 대 한 조사식 보기 단계별로 수 있습니다. VB.NET 또는 C# 코드를 디버깅 하는 것 외에도 디버거가 ASP.NET AJAX 응용 프로그램을 디버깅 하는 데 도움이 되며 줄씩 JavaScript 코드를 단계별로 실행할 수 있습니다. Visual Studio 2008을 사용 하 여 응용 프로그램 디버깅의 전체 프로세스에 discourse 제공 하는 것이 아니라 클라이언트 쪽 스크립트 파일을 디버그 하는 기법에 포커스를 추적 하는 세부 정보.

Visual Studio 2008에서 페이지를 디버깅 하는 과정은 여러 가지 방법으로 시작할 수 있습니다. 먼저 이전 섹션에서 설명한 Internet Explorer 스크립트 디버거 옵션을 사용할 수 있습니다. 이 페이지는 이미 브라우저에 로드 하 고 디버깅을 시작 하려는 경우에 작동 합니다. 또는 솔루션 탐색기에서.aspx 페이지를 마우스 오른쪽 단추로 클릭 하 고 시작 페이지로 설정 메뉴에서 선택 수 있습니다. ASP.NET 페이지를 디버깅에 익숙한 사용자 라면 다음 있습니다 아마도이 작업을 수행 하기 전에 합니다. F5 키를 누른 후에 페이지를 디버깅할 수 있습니다. 그러나 어디서 나 중단점을 설정할 일반적으로 수 있지만 선택 되지 않는 JavaScript 사용 하는 경우 다음에 알 수 있듯이 VB.NET 또는 C# 코드에서.

*외부 스크립트 및 포함*

Visual Studio 2008 디버거 외부 JavaScript 파일에 다른 페이지에 포함 하는 JavaScript를 처리 합니다. 외부 스크립트 파일을 사용 하 여 파일을 열고 선택한 모든 줄에 중단점을 설정 합니다. 코드 편집기 창 왼쪽에 회색 트레이 영역을 클릭 하 여 중단점을 설정할 수 있습니다. JavaScript를 사용 하 여 페이지에 직접 포함 된 경우는 `<script>` 회색 트레이 영역을 클릭 하 여 중단점을 설정 하는 태그를 사용할 수 없습니다. 포함 된 스크립트의 줄에 중단점을 설정 하려고 내용의 "이는 중단점에 대 한 유효한 위치가 아닙니다" 경고가 발생 합니다.

외부.js 파일에 코드를 이동 하 고 참조의 src 특성을 사용 하 여이 문제를 해결할 수 있습니다 합니다 &lt;스크립트&gt; 태그:


[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample1.html)]

외부 파일에 코드를 이동 불가능 하거나 보다 더 많은 작업이 필요 경우 가치가? 편집기를 사용 하 여 중단점을 설정할 수 없습니다, 하는 동안 디버거 문이 디버깅을 시작 하려는 코드에 직접 추가할 수 있습니다. 디버깅을 시작 하도록 ASP.NET AJAX 라이브러리의 사용 가능한 Sys.Debug 클래스를 사용할 수 있습니다. 이 문서의 뒷부분에 나오는 Sys.Debug 클래스에 대 한 자세히 알아봅니다.

사용 하는 예제는 `debugger` 키워드 목록 1에 표시 됩니다. 이 예제에서는 업데이트 함수에 대 한 호출을 시작 하기 전에 오른쪽 중단 하도록 디버거를 강제로 수행 합니다.

**목록 1. Visual Studio 디버거에서 실행을 중단 하도록 디버거 키워드를 사용 합니다.**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample2.js)]

디버거 문이 적중 되 면 Visual Studio.NET을 사용 하 여 페이지를 디버그 하 라는 메시지가 표시 하 고 코드를 단계별로 시작할 수 있습니다. 보겠습니다 페이지에서 사용 되는 ASP.NET AJAX 라이브러리 스크립트 파일에 액세스 하는 문제가 발생할 수 있습니다 하는 동안 Visual Studio를 사용 하 여 살펴보세요. NET의 스크립트 탐색기입니다.

## <a name="using-visual-studio-net-windows-to-debug"></a>Visual Studio.NET Windows를 사용 하 여 디버깅 하려면

디버그 세션을 시작 하 고 기본 F11 키를 사용 하 여 코드를 살펴보는 것이 먼저 발생할 수 있습니다 면에 표시 된 오류 대화 상자 페이지에서 사용 되는 모든 스크립트 파일 열기 및 디버깅에 사용할 수 있는 않는 그림 2를 참조 하세요.


[![디버깅에 사용할 수 있는 소스 코드가 없는 경우 표시 된 오류 대화 상자입니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image5.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image4.png)

**그림 2**: 디버깅에 사용할 수 있는 소스 코드가 없는 경우 표시 되는 오류 대화 상자.  ([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-debugging-capabilities/_static/image6.png))


이 대화 상자는 하지 않기 때문에 Visual Studio.NET 있는지 시작 페이지에서 참조 하는 스크립트의 일부 소스 코드 하는 방법에 표시 됩니다. 매우 번거로울 수 있지만이 처음에 간단한 수정 합니다. 디버그 세션을 시작 하 고 중단점에 도달 했으면, Visual Studio 2008 메뉴의 Windows 스크립트 탐색기 디버그 창으로 이동 하거나 Ctrl + Alt + N 바로 가기 키를 사용 합니다.

> *> [!NOTE] 나열 된 스크립트 탐색기 메뉴를 보이지 않으면 도구 이동할* *사용자 지정* *VISUAL Studio 메뉴에서 명령입니다. 범주 섹션에서 디버그 항목을 찾아 모든 사용 가능한 메뉴 항목을 표시 하도록 클릭 합니다. 명령 목록의 스크립트 탐색기 스크롤하고 디버그를 위로 끌어* *Windows 메뉴에 앞에서 언급 한 합니다. 이 수행 하는 사용할 수 있도록 스크립트 탐색기 메뉴 항목이 VISUAL Studio를 실행할 때마다 합니다.*


스크립트 탐색기 페이지에서 사용 되는 모든 스크립트를 보려면 코드 편집기에서 열을 사용할 수 있습니다. 스크립트 탐색기를 연 후 코드 편집기 창에서 열려는 현재 디버깅 중인.aspx 페이지에서 두 번 클릭 합니다. 모든 스크립트 탐색기에 표시 된 다른 스크립트에 대해 동일한 작업을 수행 합니다. 모든 스크립트 있습니다 코드 창에서 열기 되 면 코드를 단계별로 실행 하려면 F11 키를 누릅니다 (및 다른 디버그 바로 가기 키를 사용 하 여). 그림 3에는 스크립트 탐색기의 예가 나와 있습니다. 두 개의 사용자 지정 스크립트 및 ASP.NET AJAX ScriptManager에서 페이지에 동적으로 삽입 하는 두 개의 스크립트 뿐만 아니라 현재 디버깅 중인 파일 (Demo.aspx) 나열 합니다.


[![스크립트 탐색기 페이지에서 사용 되는 스크립트에 쉽게 액세스할 수 있습니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image8.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image7.png)

**그림 3**합니다. 스크립트 탐색기 페이지에서 사용 되는 스크립트에 쉽게 액세스할 수 있습니다.  ([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-debugging-capabilities/_static/image9.png))


여러 다른 windows 코드 페이지를 단계별로 실행 하면서 유용한 정보를 제공 하려면 사용할 수도 있습니다. 예를 들어, 페이지 출력을 살펴보고 특정 변수 또는 조건 평가를 직접 실행 창에서에서 사용 되는 다른 변수 값을 보려면 지역 창을 사용할 수 있습니다. Sys.Debug.trace 함수 (이 문서의 뒷부분에서 다룰) 또는 Internet Explorer의 Debug.writeln 함수를 사용 하 여 작성 하는 추적 문을 보려면 출력 창도 사용할 수 있습니다.

디버거를 사용 하 여 코드를 단계별로 실행 하는 대로 할당 된 값을 보려면 코드에서 변수 위로 마우스를 이동할 수 있습니다. 그러나 스크립트 디버거 가끔씩 표시 되지 않습니다 아무 것도 지정 된 JavaScript 변수 위로 마우스를 이동할 때. 값을 보려면 문 또는 코드 편집기 창에서 참조 한 다음 위로 마우스를 시도 하는 변수를 강조 표시 합니다. 이 기술은 모든 상황에서 작동 하지 않습니다, 하지만 여러 번 됩니다 지역 창과 같은 다른 디버그 창에서 검색 하지 않고도 값을 확인할 수 있습니다.

여기에 설명 된 기능 중 일부를 보여 주는 비디오 자습서에서 볼 수 있습니다 [ http://www.xmlforasp.net ](http://www.xmlforasp.net)합니다.

## <a name="debugging-with-web-development-helper"></a>Web Development Helper를 사용 하 여 디버깅

Visual Studio 2008 (및 Visual Web Developer Express 2008)은 뛰어난 디버깅 도구 이지만 더 가벼운 되도 사용할 수 있는 추가 옵션이 있습니다. 출시 될 수 있는 최신 도구 중 하나는 Web Development Helper입니다. Microsoft의 Nikhil Kothari (microsoft ASP.NET AJAX 설계자 키 중 하나)를 HTTP 요청 및 응답 메시지를 보는 간단한 디버깅에서 많은 다양 한 작업을 수행할 수 있는 뛰어난 도구가 작성 되었습니다. Web Development Helper에서 다운로드할 수 있습니다 [ http://projects.nikhilk.net/Projects/WebDevHelper.aspx ](http://projects.nikhilk.net/Projects/WebDevHelper.aspx)합니다.

Web Development helper는 Internet Explorer를 사용 하는 데 편리 내에서 직접 사용할 수 있습니다. Internet Explorer 메뉴에서 Web Development Helper 도구를 선택 하 여 시작 됩니다. HTTP 요청 및 응답 메시지 로깅 등의 여러 작업을 수행 하도록 브라우저를 둘 필요가 없으므로 유용는 브라우저의 하단에서 도구가 열립니다. 그림 4는 실행 중인 Web Development Helper 모양을 보여 줍니다.


[![Web Development Helper](understanding-asp-net-ajax-debugging-capabilities/_static/image11.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image10.png)

**그림 4**: Web Development Helper ([큰 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image12.png))


Web Development helper 도구 사용 되지 않습니다 코드 줄을 줄 별로으로 Visual Studio 2008을 사용 하 여 단계별로 합니다. 추적 출력 보기, 쉽게 스크립트에서 변수를 평가 또는 탐색 사용할 수 있지만 데이터가 JSON 개체 내에서. ASP.NET AJAX 페이지와 서버에 전달 되는 데이터를 보기 위한 매우 유용 합니다.

Web Development Helper를 열면 Internet Explorer에서 스크립트 디버깅가 활성화 해야 그림 4에 나와 있는 것 처럼 웹 개발 도우미 메뉴에서 스크립트 디버깅 사용 스크립트 선택 합니다. 이 통해 절편 오류는 페이지가 실행 될 때 발생 하는 도구입니다. 또한 페이지에서 출력 되는 추적 메시지에 쉽게 액세스할 수 있습니다. 추적 정보를 보거나 페이지 내에서 다양 한 기능을 테스트 하려면 스크립트 명령을 실행 하려면 Web Development Helper 메뉴에서 스크립트 콘솔을 표시 하는 스크립트를 선택 합니다. 명령 창 및 간단한 직접 실행 창에 대 한 액세스를 제공합니다.

*추적 메시지 및 JSON 개체 데이터 보기*

직접 실행 창 스크립트 명령을 실행 하거나도 로드 하거나 저장 하려면 페이지에 다양 한 기능을 테스트 하는 데 사용 되는 스크립트를 사용할 수 있습니다. 명령 창에 표시 되는 페이지에서 기록 하는 추적 또는 디버그 메시지가 표시 됩니다. 목록 2 Internet Explorer의 Debug.writeln 함수를 사용 하 여 추적 메시지를 작성 하는 방법을 보여 줍니다.

**2를 나열 합니다. Debug 클래스를 사용 하 여 클라이언트 쪽 추적 메시지를 작성 합니다.**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample3.js)]

Web Development Helper가 메시지를 표시 하면 LastName 속성 Doe의 값이 있으면 "사용자 이름: Doe" 스크립트 콘솔의 명령 창 (디버깅가 설정 되어 있는지 가정). 또한 web Development Helper는 JSON 개체의 콘텐츠를 보거나 추적 정보를 쓰는 데 사용할 수 있는 페이지에 최상위 debugService 개체를 추가 합니다. 코드 3 debugService 클래스의 추적 함수를 사용 하는 예제를 보여 줍니다.

**코드 3. 추적 메시지를 쓸 Web Development Helper debugService 클래스를 사용 합니다.**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample4.js)]

DebugService 클래스의 유용한 기능 Web Development Helper 실행 중일 때 추적 데이터를 항상 액세스할 수 있도록 Internet Explorer에서 활성화 되어 있지 않으면 디버깅 하는 경우에 작동 됩니다. 도구를 사용 하는 페이지를 디버그 하 되 고 있지, window.debugService 호출 false를 반환 하므로 추적 문은 무시 됩니다.

DebugService 클래스에는 JSON 개체 데이터를를 Web Development Helper의 검사기 창을 사용 하 여 볼 수 있습니다. 코드 4 개인 데이터가 포함 된 간단한 JSON 개체를 만듭니다. 개체를 만든 후 호출 된 debugService를 클래스의 JSON 개체를 시각적으로 검사할 수 있도록 함수를 검사 합니다.

**코드 4. DebugService.inspect 함수를 사용 하 여 JSON 개체 데이터를 볼 수 있습니다.**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample5.js)]

페이지에서 사용 하거나 직접 실행 창을 통해 GetPerson() 함수를 호출 개체 검사기 대화 상자 창 그림 5와 같이 표시 됩니다. 개체 내에서 속성을 강조 표시 하 여 동적으로 변경할 수 있습니다 값 텍스트 상자에 표시 되는 값을 변경 하 고 업데이트 링크를 클릭 합니다. 개체 관리자를 사용 하 여은 데이터를 보고 JSON 개체 속성에 다른 값을 적용할 시험해 간단 하 게 합니다.

*디버깅 오류*

추적 데이터 및 JSON 개체를 표시할 수를 허용 하는 것 외에도 Web Development helper 오류 페이지에 디버깅에 도움이 될 수 있습니다. 다음 코드 줄을 계속 하려면 스크립트를 디버그 메시지가 표시 되는 오류가 발생 하는 경우 (그림 6 참조). 스크립트 내에 있는 문제를 쉽게 식별할 수 있도록 줄 번호 뿐만 아니라 전체 호출 스택 스크립트 오류 대화 상자 창 표시 됩니다.


[![개체 검사기 창을 사용 하 여 JSON 개체를 볼 수 있습니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image14.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image13.png)

**그림 5**: 개체 검사기 창을 사용 하 여 JSON 개체를 볼 수 있습니다.  ([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-debugging-capabilities/_static/image15.png))


디버그 옵션을 선택 하면 변수 값 보기, 기타 다양 한 JSON 개체를 작성 하려면 Web Development Helper 직접 실행 창에서 직접 스크립트 문을 실행할 수 있습니다. 오류를 트리거한 동일한 작업을 다시 수행 하는 경우 Visual Studio 2008은 컴퓨터에서 사용할 디버그 세션을 시작 하 여 한 줄씩 이전 섹션에서 설명한 대로 코드를 단계별로 실행할 수 있습니다를 묻는 메시지가 나타납니다.


[![Web Development Helper 스크립트 오류 대화 상자](understanding-asp-net-ajax-debugging-capabilities/_static/image17.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image16.png)

**그림 6**: Web Development Helper 스크립트 오류 대화 상자 ([큰 이미지를 보려면 클릭](understanding-asp-net-ajax-debugging-capabilities/_static/image18.png))


*요청 및 응답 메시지를 검사합니다.*

ASP.NET AJAX 페이지를 디버깅 하는 동안 페이지와 서버 간에 전송 되는 요청 및 응답 메시지를 확인 하는 데 유용 경우가 있습니다. 메시지 내에서 콘텐츠 보기를 사용 하면 적절 한 데이터 메시지의 크기 뿐만 아니라 전달 되는 경우 확인할 수 있습니다. Web Development Helper를 원시 텍스트 또는 좀 더 읽기 쉬운 형식으로 데이터를 볼 수 있도록 하는 뛰어난 HTTP 메시지로 거 기능을 제공 합니다.

ASP.NET AJAX 요청 및 응답 메시지를 보려면 Web Development Helper 메뉴에서 HTTP 로깅 사용 HTTP를 선택 하 여 HTTP로 거를 사용할 수 있어야 합니다. 사용 하도록 설정 하면 현재 페이지에서 보낸 모든 메시지는 HTTP 로그를 표시 하는 HTTP를 선택 하 여 액세스할 수 있는 HTTP 로그 뷰어에서 볼 수 있습니다.

각 요청/응답 메시지에 전송 되는 원시 텍스트를 보고 하는 것은 확실히 유용 하지만 Web Development Helper에서 옵션 쉽습니다 그래픽 형식으로 메시지 데이터를 볼 수 있습니다. HTTP 로깅을 사용 하도록 설정한 후 메시지가 기록 되었음을 HTTP 로그 뷰어에 메시지를 두 번 클릭 하 여 메시지 데이터를 볼 수 있습니다. 이렇게 하면 실제 메시지 뿐만 아니라 메시지를 연관 된 모든 헤더를 볼 수 콘텐츠. 그림 7에는 요청 메시지 및 HTTP 로그 뷰어 창에 표시 되는 응답 메시지의 예가 나와 있습니다.


[![HTTP 로그 뷰어를 사용 하 여 요청 및 응답 메시지 데이터를 볼 수 있습니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image20.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image19.png)

**그림 7**: HTTP 로그 뷰어를 사용 하 여 요청 및 응답 메시지 데이터를 볼 수 있습니다.  ([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-debugging-capabilities/_static/image21.png))


HTTP 로그 뷰어는 자동으로 JSON 개체를 구문 분석 하 고 빠르고 쉽게 개체의 속성 데이터를 볼 수 있도록 트리 뷰를 사용 하 여 표시 합니다. ASP.NET AJAX 페이지에서 UpdatePanel 사용 중인 경우 그림 8 에서처럼 개별 파트 메시지의 각 부분 아웃 뷰어를 중단 합니다. 이 훨씬 쉽게 원시 메시지 데이터가 보기에 비해 메시지에 포함 된 내용 파악 해야 하는 훌륭한 기능입니다.


[![HTTP 로그 뷰어를 사용 하 여 볼 UpdatePanel 응답 메시지입니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image23.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image22.png)

**그림 8**: 응답 메시지는 UpdatePanel HTTP 로그 뷰어를 사용 하 여 표시 합니다.  ([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-debugging-capabilities/_static/image24.png))


Web Development Helper 외에도 요청 및 응답 메시지를 보는 데 사용할 수 있는 다른 몇 가지 도구가 있습니다. 또 다른 좋은 옵션은 무료로 사용할 수 있는 Fiddler [ http://www.fiddlertool.com ](http://www.fiddlertool.com)합니다. Fiddler는 여기 언급 하지 것입니다, 하지만 것도 좋은 철저 하 게 메시지 헤더 및 데이터를 검사 해야 할 경우.

## <a name="debugging-with-firefox-and-firebug"></a>Firefox와 Firebug를 사용 하 여 디버깅

Internet Explorer는 여전히 널리 사용 되는 브라우저, Firefox와 같은 다른 브라우저 매우 인기가 및 점점 더 사용 됩니다. 결과적으로, 보기 및 Firefox로 Internet Explorer 응용 프로그램을 제대로 작동 하는지 확인 하 여 ASP.NET AJAX 페이지를 디버그 해야 합니다. Firefox는 디버깅에 대 한 Visual Studio 2008에 직접 연결할 수 없습니다, 있지만 해당 확장명이 페이지를 디버깅 하는 Firebug를 호출 합니다. Firebug로 이동 하 여 무료로 다운로드할 수 있습니다 [ http://www.getfirebug.com ](http://www.getfirebug.com)합니다.

Firebug가 제공 하 여 한 줄씩 코드를 단계별로, 페이지 내에서 사용 되는 모든 스크립트에 액세스, DOM 구조를 보고, CSS 스타일 및 추적 이벤트가 발생 하는 페이지에 표시할 수 있는 완전 한 기능의 디버깅 환경. 설치 되 면 Firebug는 Firefox 메뉴에서 도구 Firebug 열기 Firebug를 선택 하 여 액세스할 수 있습니다. Firebug는 Web Development Helper와 같은 독립 실행형 응용 프로그램으로도 사용 될 수 있지만 브라우저에서 직접 사용 됩니다.

Firebug가 실행 되 면 여부 스크립트를 페이지에 포함 되어 있는지 여부를 JavaScript 파일의 모든 줄에 중단점 설정할 수 있습니다. 중단점을 설정 하려면 먼저 Firefox에서 디버그 하려는 해당 페이지를 로드 합니다. 페이지 로드 되 면 Firebug의 스크립트 드롭 다운 목록에서 디버그 하는 스크립트를 선택 합니다. 페이지를 사용 하는 모든 스크립트에 표시 됩니다. 중단점은 중단점은 어디에 해야 Visual Studio 2008의 경우와 같은 줄에서 Firebug의 회색 트레이 영역을 클릭 하 여 설정 됩니다.

Firebug에서 중단점을 설정한 후에 단추를 클릭 하거나 onLoad 이벤트를 트리거하는 브라우저를 새로 고쳐 같은 디버그 해야 하는 스크립트를 실행 하는 데 필요한 작업을 수행할 수 있습니다. 실행이 중단점을 포함 하는 줄에 자동으로 중지 됩니다. 그림 9 Firebug 트리거한 되어 중단점의 예제를 보여 줍니다.


[![Firebug에서 중단점을 처리 합니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image26.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image25.png)

**그림 9**: Firebug에서 중단점을 처리 합니다.  ([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-debugging-capabilities/_static/image27.png))


중단점이 적중 되 면 한 단계씩 코드 실행 프로시저 단위로 실행 하거나 화살표 단추를 사용 하 여 코드에서 나갈 수 있습니다. 코드를 단계별로 실행 하는 대로 스크립트 변수 값을 개체로 드릴 다운 수 있도록 디버거의 오른쪽 부분에 표시 됩니다. Firebug는 디버그 중인 현재 줄을 초래한 스크립트의 실행 단계를 보려면 호출 스택 드롭 다운 목록도 제공 합니다.

Firebug는 다른 스크립트 문을 테스트 변수를 평가, 추적 출력 보기를 사용할 수 있는 콘솔 창을도 포함 되어 있습니다. Firebug 창의 맨 위에 있는 콘솔 탭을 클릭 하 여 액세스 합니다. 디버깅 중인 페이지도 검사할 수 있습니다 "" 검사 탭을 클릭 하 여 DOM 구조 및 내용을 볼 수 있습니다. 때 페이지에서 사용 되는 요소 볼 수 있도록 적절 한 부분 페이지 검사기 창에 표시 된 다양 한 DOM 요소 위에 마우스를 놓았을 선택 됩니다. "실시간" 요소에 서로 다른 너비, 스타일 등 적용 실험으로 지정된 된 요소와 연결 된 특성 값을 변경할 수 있습니다. 이것이 얼마나 간단한 변경 내용에 영향을 페이지를 보려면 소스 코드 편집기 및 Firefox 브라우저를 지속적으로 전환 하지 않아도 저장 하는 멋진 기능입니다.

그림 10에는 DOM 검사기를 사용 하 여 페이지에서 txtCountry 라는 텍스트 상자에 찾으려는 예가 나와 있습니다. 또한 Firebug 검사기 마우스 이동, 단추 클릭, 기타 다양 한 추적과 같이 발생 하는 이벤트를 비롯 하 여 페이지에 사용 되는 CSS 스타일을 보는 데 사용할 수 있습니다.


[![Firebug의 DOM 검사기를 사용 합니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image29.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image28.png)

**그림 10**:를 사용 하 여 Firebug DOM 검사기입니다.  ([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-debugging-capabilities/_static/image30.png))


Firebug는 페이지 내에서 다양 한 요소를 검사 하는 데 적합 한 도구 뿐만 아니라 Firefox에서 바로 페이지로 신속 하 게 디버그 하는 간단한 방법을 제공 합니다.

## <a name="debugging-support-in-aspnet-ajax"></a>ASP.NET ajax에서 디버깅 지원

ASP.NET AJAX library 웹 페이지에 AJAX 기능을 추가 하는 프로세스를 간소화 하기 위해 사용할 수 있는 여러 클래스를 포함 합니다. 페이지 내에서 요소를 검색 및 조작 하, 새 컨트롤을 추가, 웹 서비스를 호출 및도 이벤트를 처리할 이러한 클래스를 사용할 수 있습니다. ASP.NET AJAX 라이브러리는 또한 디버깅 페이지의 프로세스를 향상 시키기 위해 사용할 수 있는 클래스를 포함 합니다. 이 섹션에서는 Sys.Debug 클래스 소개 하 고 참조 하는 방법을 응용 프로그램에서 사용할 수 있습니다.

*Sys.Debug 클래스를 사용 하 여*

추적 출력을 작성, 코드 어설션을 수행 및 디버깅할 수 있도록 실패 하는 코드를 강제 적용을 포함 하 여 여러 다른 기능을 수행 하는 Sys.Debug 클래스 (Sys 네임 스페이스에 있는 JavaScript 클래스)를 사용할 수 있습니다. 것에서 널리 사용 됩니다 (기본적으로 C:\Program Files\Microsoft ASP.NET\ASP.NET 2.0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0에서 설치) 하는 ASP.NET AJAX 라이브러리의 디버그 파일 (조건부 테스트를 수행 하려면 어설션 이라고 함) 매개 변수는 함수, 개체에 예상된 데이터가 포함 하는 데 추적 문을 작성할 제대로 전달 되었는지 확인 하는 합니다.

Sys.Debug 클래스는 추적, 코드 어설션 또는 표 1에 나와 있는 것 처럼 오류 처리를 사용할 수 있는 다양 한 기능을 제공 합니다.

**표 1입니다. Sys.Debug 클래스 함수입니다.**

| **함수 이름** | **설명** |
| --- | --- |
| assert(condition, message, displayCaller) | 조건 매개 변수가 true 임을 어설션 합니다. 테스트 중인 조건이 false 이면 메시지 매개 변수 값을 표시 하는 메시지 상자가 사용 됩니다. DisplayCaller 매개 변수가 true 인 경우 메서드는 또한 호출자에 대 한 정보를 표시 합니다. |
| clearTrace() | 추적 작업에서 문을 출력을 지웁니다. |
| fail(message) | 프로그램을 실행을 중지 하 고 디버거를 중단 하면 됩니다. 실패 한 이유를 제공 하는 메시지 매개 변수를 사용할 수 있습니다. |
| trace(message) | 추적 출력에 메시지 매개 변수를 씁니다. |
| traceDump (object, 이름) | 개체의 데이터를 읽을 수 있는 형식으로 출력합니다. 레이블을 제공 하기 위해 추적 덤프에 대 한 name 매개 변수를 사용할 수 있습니다. 모든 하위 개체 덤프 되는 개체 내에서 기본적으로 작성 됩니다. |

ASP.NET에서 사용할 수 있는 추적 기능을 거의 동일한 방식 클라이언트 쪽 추적을 사용할 수 있습니다. 다양 한 메시지를를 응용 프로그램의 흐름을 방해 하지 않고 쉽게 볼 수 있습니다. 목록 5 추적 로그에 쓸 Sys.Debug.trace 함수를 사용 하는 예제를 보여 줍니다. 이 함수는 단순히 매개 변수로 기록 되어야 하는 메시지를 사용 합니다.

**5를 나열 합니다. Sys.Debug.trace 함수를 사용합니다.**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample6.js)]

목록 5에 나와 있는 코드를 실행 하는 경우에 페이지에서 추적 출력을 볼 수 없습니다. 표시 하는 유일한 방법은 Visual Studio.NET, Web Development Helper 또는 Firebug에서 사용할 수 있는 콘솔 창을 사용 하는 것입니다. 페이지에서 추적 출력을 표시 하지 않으려면 다음 해야 텍스트 영역 태그를 추가 하 고 다음과 같이 TraceConsole의 id를 지정 합니다.


[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample7.html)]

페이지에 있는 Sys.Debug.trace 문이 TraceConsole TextArea에 기록 됩니다.

JSON 개체 내에 포함 된 데이터를 보려는 경우 Sys.Debug 클래스의 traceDump 함수를 사용할 수 있습니다. 이 함수는 추적 콘솔로 덤프할 수 해야 하는 개체와 추적 출력에서 개체를 식별 하는 이름을 포함 하는 두 개의 매개 변수를 사용 합니다. 코드 6 traceDump 함수를 사용 하는 예제를 보여 줍니다.

**코드 6. Sys.Debug.traceDump 함수를 사용합니다.**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample8.js)]

그림 11 Sys.Debug.traceDump 함수 호출의 출력을 보여 줍니다. 사용자 개체의 데이터를 작성 하는 것 외에도 또한 쓰는지 주소 하위 개체의 데이터를 확인 합니다.

추적 하는 것 외에도 Sys.Debug 클래스 코드 어설션을 수행 하려면 데도 수 있습니다. 어설션 응용 프로그램이 실행 되는 동안 특정 조건이 충족 되는 테스트 하는 데 사용 됩니다. ASP.NET AJAX 스크립트 라이브러리의 디버그 버전에 포함 여러 assert 다양 한 조건 테스트 합니다.

코드 7 Sys.Debug.assert 함수를 사용 하 여 조건을 테스트 하려면 예를 보여 줍니다. 코드 주소 개체를 사용자 개체를 업데이트 하기 전에 null 인지 여부를 테스트 합니다.


[![Sys.Debug.traceDump 함수 출력입니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image32.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image31.png)

**그림 11**: Sys.Debug.traceDump 함수 출력입니다.  ([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-debugging-capabilities/_static/image33.png))


**코드 7. Debug.assert 함수를 사용합니다.**


[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample9.js)]

세 개의 매개 변수는 어설션이 false이 고 호출자에 대 한 정보를 표시 하는 여부를 반환 하는 경우 표시할 메시지를 평가 하는 조건을 포함 하 여 전달 됩니다. 어설션이 실패 하는 경우에 세 번째 매개 변수 되었으면 true 호출자 정보 뿐만 아니라 메시지를 표시 됩니다. 그림 12에는 7 에서처럼 어설션이 실패 하는 경우 표시 되는 오류 대화 상자의 예가 나와 있습니다.

포함 하는 마지막 기능은 Sys.Debug.fail 사용 하는 것입니다. 스크립트에서 특정 줄에 실패 하는 코드를 강제로 하려는 경우에 JavaScript 응용 프로그램에서 일반적으로 사용 하는 디버거 문이 아니라 Sys.Debug.fail 호출을 추가할 수 있습니다. Sys.Debug.fail 함수는 다음과 같이 실패 한 이유를 나타내는 단일 문자열 매개 변수를 허용 합니다.


[!code-css[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample10.css)]


[![Sys.Debug.assert 실패 메시지입니다.](understanding-asp-net-ajax-debugging-capabilities/_static/image35.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image34.png)

**그림 12**:는 Sys.Debug.assert 오류 메시지입니다.  ([클릭 하 여 큰 이미지 보기](understanding-asp-net-ajax-debugging-capabilities/_static/image36.png))


Sys.Debug.fail 문을 스크립트를 실행 하는 동안 발생 하면 Visual Studio 2008과 같은 디버그 응용 프로그램의 콘솔에 표시할 메시지 매개 변수의 값 및 응용 프로그램을 디버깅 하 라는 메시지가 나타납니다. 한 가지 사례가이 유용할 수 있는 매우은 인라인 스크립트에 Visual Studio 2008을 사용 하 여 중단점을 설정할 수 없습니다 있지만 변수의 값을 검사할 수 있도록 특정 줄에서 중지 하는 코드를 원하는 경우.

*Scriptmanager의 ScriptMode 속성 이해*

ASP.NET AJAX 라이브러리에서는 디버그 및 기본적으로 C:\Program Files\Microsoft ASP.NET\ASP.NET 2.0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0에 설치 된 스크립트 버전을 릴리스 합니다. 디버그 스크립트 보기 좋게 서식이 지정 된, 쉽게 읽을 수 및가 여러 Sys.Debug.assert 호출 전체에 흩어져 있는 해당 릴리스 스크립트 공백을 제거 하 고 전체 크기를 최소화 하기 위해 꼭 필요할 때만 Sys.Debug 클래스를 사용 하는 동안.

ASP.NET AJAX 페이지에 추가 되는 ScriptManager 컨트롤 라이브러리를 로드 하는 스크립트의 버전을 확인 하려면 web.config의 컴파일 요소의 debug 특성을 읽습니다. 그러나 경우를 제어할 수 있습니다. 디버그 또는 릴리스 스크립트는 로드 (라이브러리 스크립트 또는 사용자 고유의 사용자 지정 스크립트) ScriptMode 속성을 변경 하 여 합니다. ScriptMode는 ScriptMode 열거형 멤버가 포함 자동, 디버그, 릴리스 및 상속을 허용 합니다.

ScriptMode 자동 ScriptManager는 web.config에 디버그 특성을 확인 하는 값이 기본값으로 사용 됩니다. 디버그가 false 인 경우 ASP.NET AJAX 라이브러리 스크립트의 릴리스 버전 ScriptManager에 로드 됩니다. 디버그 true 인 경우 스크립트의 디버그 버전 로드 됩니다. 릴리스 또는 디버그 ScriptMode 속성을 변경 하면 web.config에는 debug 특성 값에 관계 없이 적절 한 스크립트를 로드 하는 ScriptManager 강제 됩니다. 코드 8 ScriptManager 컨트롤을 사용 하 여 ASP.NET AJAX 라이브러리의 디버그 스크립트를 로드 하는 예를 보여 줍니다.

**8를 나열 합니다. ScriptManager를 사용 하 여 디버그 스크립트 로드**합니다.


[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample11.aspx)]

또한 목록 9에 표시 된 대로 ScriptReference 구성 요소와 함께 ScriptManager의 스크립트 속성을 사용 하 여 사용자 고유의 사용자 지정 스크립트의 다른 버전 (디버그 또는 릴리스)를 로드할 수 있습니다.

**코드 9. ScriptManager를 사용 하 여 사용자 지정 스크립트를 로드 합니다.**


[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample12.aspx)]

> [!NOTE]
> ScriptReference 구성 요소를 사용 하 여 사용자 지정 스크립트를 로드 하는 경우 스크립트가 스크립트 맨 아래에 다음 코드를 추가 하 여 로드를 완료 된 경우 ScriptManager 알려야 합니다.


[!code-csharp[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample13.cs)]

목록 9에 표시 된 코드 사용자 스크립트의 디버그 버전에 대 한 검색할 Person.debug.js Person.js 대신에 대 한 자동으로 검색 됩니다 ScriptManager를 알려 줍니다. Person.debug.js 파일이 없는 경우 오류가 발생 합니다.

디버그 나 ScriptManager 컨트롤에 설정 된 ScriptMode 속성의 값에 따라 로드 되도록 사용자 지정 스크립트의 릴리스 버전의 경우에서 상속에 ScriptReference 컨트롤의 ScriptMode 속성을 설정할 수 있습니다. 이렇게 하면 로드할 사용자 지정 스크립트의 적합 한 버전 10 목록에 표시 된 것 처럼 ScriptManager의 ScriptMode 속성을 기반으로 합니다. Scriptmanager의 ScriptMode 속성 디버그로 설정 되어, 있으므로 Person.debug.js 스크립트를 로드 하 고 페이지에서 사용 됩니다.

**코드 10. 사용자 지정 스크립트에 대 한 ScriptManager의 ScriptMode를 상속 합니다.**


[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample14.aspx)]

ScriptMode 속성을 적절 하 게 사용 하 여 응용 프로그램을 디버그 하 고 전체 프로세스를 간소화 쉽게 수 있습니다. ASP.NET AJAX 라이브러리의 릴리스 스크립트를 단계별로 실행 코드 서식 지정 제거 된 디버그 스크립트 디버깅 목적을 위해 특히 형식이 지정 하는 동안 있으므로 읽기 보다 어렵습니다.

## <a name="conclusion"></a>결론

Microsoft의 ASP.NET AJAX 기술을 최종 사용자의 전반적인 환경을 향상 시킬 수 있는 AJAX 지원 응용 프로그램을 빌드하기 위한 견고한 토대를 제공 합니다. 그러나으로 모든 프로그래밍 기술을 사용 하 여 버그 및 다른 응용 프로그램 문제를 확실히 발생 합니다. 사용 가능한 다른 디버깅 옵션을 알지 더 안정적인 제품 수많은 시간 및 결과 저장할 수 있습니다.

이 문서의 Visual Studio 2008, Web Development Helper와 Firebug를 사용 하 여 Internet Explorer를 포함 하 여 ASP.NET AJAX 페이지를 디버깅 하는 것에 대 한 몇 가지 다른 기법을 검토 하면 했습니다. 이러한 도구는 변수 데이터에 액세스 하, 코드 줄 단위로 안내 하 고 추적 문을 볼 수 있으므로 전체 디버깅 프로세스를 간소화할 수 있습니다. 설명 된 다양 한 디버깅 도구를 외에 응용 프로그램에서 ASP.NET AJAX 라이브러리의 Sys.Debug 클래스를 사용할 수 있는 방법 및 살펴보았습니다 로드 ScriptManager 클래스를 사용할 수 있는 방법을 디버그 또는 릴리스 버전의 스크립트입니다.

## <a name="bio"></a>사용자 정보

Dan Wahlin (Microsoft Most Valuable Professional ASP.NET 및 XML 웹 서비스에 대 한)은 인터페이스 기술 교육에.NET 개발 강사 및 아키텍처 컨설턴트 ([www.interfacett.com)](http://www.interfacett.com)합니다. Dan 설립 ASP.NET 개발자 웹 사이트에 대 한 XML ([www.XMLforASP.NET](http://www.XMLforASP.NET)), INETA 발표자 기관에 및 여러 컨퍼런스에서 강연 합니다. Dan을 공동 저술 했습니다 Professional Windows DNA (Wrox) ASP.NET: 팁, 자습서 및 코드 (Sams), ASP.NET 1.1 Insider, Professional ASP.NET 2.0 AJAX (Wrox), ASP.NET 2.0 MVP Hacks 솔루션과 (Sams) ASP.NET 개발자를 위한 작성 된 XML입니다. 그 코드, 기사 또는 책을 기록 하지 않습니다, 작성 및 음악을 기록 및 골프 및 그의 아내와 어린이 농구 재생 Dan 이용할 수 있습니다.

Scott Cate 1997 년부터 Microsoft 웹 기술을 사용 하 여 왔습니다 이며 myKB.com의 대표이사로 서 ([www.myKB.com](http://www.myKB.com)) ASP.NET 작성 전문적 기반 응용 프로그램 기술 자료 소프트웨어 솔루션에 집중 합니다. Scott 전자 메일을 통해 연락할 수 있습니다 [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com) 저자의 블로그 또는 [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [이전](understanding-asp-net-ajax-web-services.md)
