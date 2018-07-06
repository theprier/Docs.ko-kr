---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: ASP.NET MVC에서 페이지 검사기 사용 | Microsoft Docs
author: rick-anderson
description: Visual Studio 2012에서 페이지 검사기는 통합 된 브라우저를 사용 하 여 웹 개발 도구입니다. 통합 된 브라우저 및 페이지 검사기 i 요소를 선택 하는 중...
ms.author: aspnetcontent
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: e3a6b79811cae15ec69ba3c5babe38b117b697a5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37806088"
---
<a name="using-page-inspector-in-aspnet-mvc"></a>ASP.NET MVC에서 페이지 검사기 사용
====================
Tim Ammann 여

> Visual Studio 2012에서 페이지 검사기는 통합 된 브라우저를 사용 하 여 웹 개발 도구입니다. 통합 된 브라우저에서 모든 요소를 선택 하 고 요소의 소스 및 CSS 페이지 검사기를 즉시 강조 표시 합니다. MVC 보기 찾아보기, 신속 하 게 렌더링 된 태그의 원본을 살펴봅니다를 Visual Studio 환경 내에서 바로 브라우저 도구를 사용 합니다.
> 
> [비디오를 시청 하세요.](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> 이 자습서에서는 검사 모드를 활성화 한 후 신속 하 게 찾아 웹 프로젝트 내에서 태그와 CSS를 편집 하는 방법을 보여 줍니다. 이 자습서에서는 MVC 프로젝트를 사용 하지만 용 페이지 검사기를 사용할 수도 있습니다 [Web Forms](https://go.microsoft.com/?linkid=9802001) 및 다른 ASP.NET 응용 프로그램입니다.
> 
> 이 자습서에는 다음 섹션이 있습니다.
> 
> - [필수 조건](#_1_prerequisites)
> - [웹 응용 프로그램 만들기](#_2_creating_a)
> - [뷰를 탐색 페이지 검사기 사용](#_3_using_page)
> - [검사 모드를 사용 하도록 설정](#_4_inspection_mode)
> - [페이지 검사기를 사용 하 여 태그를 변경 하려면](#_5_using_page)
> - [HTML 창과 검사 모드](#_6_inspection_mode)
> - [스타일 창에서 CSS 변경 내용 미리 보기](#_7_previewing_css)
> - [CSS 자동 동기화](#css_auto_sync)
> - [CSS 색 선택을 사용 하 여](#css_color_picker)
> - [동적 페이지 요소를 JavaScript에 매핑](#map_dynamic_elements)


<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>전제 조건

- [Visual Studio 2012](https://www.microsoft.com/visualstudio/11) 나 [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)합니다.

> [!NOTE]
> 페이지 검사기의 최신 버전을 사용 [웹 플랫폼 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=255386) .NET 2.0에 대 한 Windows Azure SDK를 설치 합니다.


페이지 검사기는 Microsoft Web 개발자 도구를 사용 하 여 제공 됩니다. 최신 버전 1.3입니다. 어떤 버전을 확인 하려면, Visual Studio를 실행 있고 선택 **Microsoft Visual Studio 정보** 에서 합니다 **도움말** 메뉴.

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>웹 응용 프로그램 만들기

먼저 사용 하 여 페이지 검사기 사용 하 여 웹 응용 프로그램을 만듭니다. Visual Studio에서 선택 **파일** &gt; **새 프로젝트**합니다. 왼쪽의 확장 **Visual C#** 를 선택 **웹**를 선택한 후 **ASP.NET MVC4 웹 응용 프로그램**합니다.

![새 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image2.png)

**확인**을 클릭합니다.

에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**합니다. 둡니다 **Razor** 기본 뷰 엔진으로 합니다.

![새 ASP.NET MVC 프로젝트-인터넷 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image4.png)

응용 프로그램에서 엽니다 **원본** 보기.

![소스 뷰에서 새 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image6.png)

응용 프로그램 사용을 설정 했으므로 점검 하 여 수정 페이지 검사기를 사용할 수 있습니다.

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a>뷰를 탐색 페이지 검사기 사용

Visual Studio 2012에서 단추로 보기에서 프로젝트를 선택 **페이지 검사기에서 보기**, 페이지 검사기는 경로 파악 하 고 페이지를 표시 합니다.

**솔루션 탐색기**를 확장 합니다 **뷰** 폴더 차례로 **홈** 폴더입니다. Index.cshtml 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **페이지 검사기에서 보기**합니다.

![페이지 검사기에서 보기 Index.cshtml](using-page-inspector-in-aspnet-mvc/_static/image8.png)

기본적으로 Visual Studio 환경의 왼쪽에서 페이지 검사기 창으로 도킹 됩니다. 원하는 경우 다른 곳에서 도킹 하거나 창의 도킹을 해제 수 있습니다. 참조 [방법: 정렬 및 도킹 Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx)합니다.

페이지 검사기 창 상단의 브라우저 창에서 현재 페이지를 보여 줍니다. 아래쪽 창의 페이지의 다양 한 측면을 검사할 수 있도록 탭도 함께 HTML 태그에서 페이지를 보여 줍니다. 아래쪽 창은 비슷합니다는 [F12 개발자 도구](https://msdn.microsoft.com/ie/aa740478) Internet Explorer에서.

![페이지 검사기에서 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image10.png)

이 자습서에서는 사용 하 여는 **HTML** 하 고 **스타일** 신속 하 게 이동 하 고 응용 프로그램을 변경 하는 탭 합니다.

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a>EnableInspection 모드

페이지 검사기를 검사 모드에 두려면를 클릭 합니다 **검사** 단추입니다. 검사 모드에서 렌더링된 된 페이지 부분 위로 마우스 포인터를 가져가면 해당 소스 태그나 코드가 강조 표시 됩니다.

![검사 모드 설정/해제](using-page-inspector-in-aspnet-mvc/_static/image12.png)

이제 페이지 검사기 내에서 페이지의 다른 부분 위로 마우스를 이동 합니다. 마찬가지로, 마우스 포인터 큰 더하기 기호를으로 변경 되 고 아래에 있는 요소가 강조 표시 됩니다.

![Div.content 래퍼를 가리키면](using-page-inspector-in-aspnet-mvc/_static/image14.png)

마우스 포인터를 이동 하면 Visual Studio에는 소스 파일의 해당 Razor 구문 강조 표시 합니다. 다른 소스 파일에서 HTML 요소 상태가 되 면 Visual Studio는 자동으로 파일을 엽니다.

페이지 검사기에는 **HTML** 탭 Razor 구문에서 생성 된 HTML을 표시 합니다. 마우스 포인터를 이동 하면 HTML 요소를 강조 표시 됩니다. 합니다 **스타일** 탭 요소에 대 한 CSS 규칙을 보여 줍니다.

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>페이지 검사기를 사용 하 여 태그를 변경 하려면

페이지 검사기를 사용 하면 위치가 명확 하지 않을 태그를 찾을 수 있습니다. 다음 태그를 수정 하 고 결과 변경 내용을 볼 수 있습니다.

이 확인 하려면 클릭 **검사** 페이지 검사기 창의 페이지의 아래쪽으로 스크롤합니다.

영역의 바닥글 부분에 마우스 포인터를 이동 하는 경우 페이지 검사기 열립니다는 \_Layout.cshtml 파일 선택한 레이아웃 페이지의 섹션을 강조 표시 합니다. 알 수 있듯이 바닥글은 레이아웃 파일 뷰 자체에 정의 됩니다.

![바닥글](using-page-inspector-in-aspnet-mvc/_static/image16.png)

이제 저작권 정보를 사용 하 여 선 위로 마우스 포인터를 이동 <a id="a"> </a>알 수 있습니다. 에 \_Layout.cshtml 페이지에서 해당 줄이 강조 표시 합니다.

![바닥글 저작권 줄 강조 표시](using-page-inspector-in-aspnet-mvc/_static/image18.png)

텍스트 줄의 끝에 추가 된 \_Layout.cshtml 파일입니다.

&lt;p&gt;&amp;복사 합니다. @DateTime.Now.Year -내 ASP.NET MVC 응용 프로그램이 최고인!  &lt; /p&gt;

이제 Ctrl + Alt + Enter를 누르거나 페이지 검사기 브라우저 창에서 결과 볼 수 업데이트 표시줄을 클릭 합니다.

![내 ASP.NET 응용 프로그램 Rocks!](using-page-inspector-in-aspnet-mvc/_static/image20.png)

바닥글 Index.cshtml에서 정의 되지만 평범한 일에 생각을 \_Layout.cshtml, 및 페이지 검사기를 발견 합니다.

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>HTML 창과 검사 모드

다음으로, HTML 창과 요소를 매핑되는 방법을 빠르게 확인을 해야 합니다.

클릭 **검사** 를 검사 모드에서 페이지 검사기를 배치 합니다.

"Logohere" 라고 표시 되는 페이지의 위쪽을 클릭 합니다. 보다 세부적으로 마우스 포인터를 이동 하면 브라우저 창에 표시를 변경 하는 더 이상 특정 요소를 검사 하 고 없습니다.

이제 마우스 포인터를 이동 합니다 **HTML** 창입니다. 마우스 포인터를 이동 하면 페이지 검사기 내의 요소를 설명 합니다 **HTML** 창 고 브라우저 창에서 해당 요소를 강조 표시 합니다.

![HTML 창](using-page-inspector-in-aspnet-mvc/_static/image22.png)

페이지 검사기가 열리면 이전에 \_임시 탭에서 Layout.cshtml 파일입니다. 클릭 합니다 \_Layout.cshtml 임시 탭 및 해당 태그에서 강조 표시 됩니다는 &lt;헤더&gt; 를 섹션:

![강조 표시 된 태그](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>스타일 창에서 CSS 변경 내용 미리 보기

다음으로, 페이지 검사기 사용할지 **스타일** css 변경 내용 미리 보기 창입니다.

클릭 **검사** 를 검사 모드에서 페이지 검사기를 배치 합니다.

페이지 검사기 브라우저 창에서 마우스 포인터를 이동 될 때까지 "홈 페이지" 섹션을 마우스로 합니다 **div.content 래퍼** 레이블이 나타납니다.

![Div.content 래퍼를 가리키면](using-page-inspector-in-aspnet-mvc/_static/image26.png)

Div.content 래퍼 섹션 내에서 한 번 클릭 하 고 다음으로 마우스 포인터를 이동 합니다 **스타일** 창입니다. 합니다 **스타일** 이 요소에 대 한 CSS 규칙의 모든 창을 표시 합니다. 찾기.featured.content 래퍼 클래스 선택기까지 아래로 스크롤하십시오. 이제 배경색 속성에 대 한 확인란의 선택을 취소 합니다.

![투명 한 배경이 색](using-page-inspector-in-aspnet-mvc/_static/image28.png)

방법 변경 내용을 미리 봅니다. 즉시 페이지 검사기 브라우저 창에서 확인할 수 있습니다.

다시 확인란을 선택 하, 속성 값을 두 번 클릭 및 빨강으로 변경 합니다. 변경 내용을 즉시 보여 줍니다.

![빨강 배경색.](using-page-inspector-in-aspnet-mvc/_static/image30.png)

합니다 **스타일** 스타일으로 변경 내용을 커밋하기 전에 변경 하는 쉽게 테스트 하 고 CSS를 미리 보기 창을 사용 하면 자체 시트입니다.

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>CSS 자동 동기화

> [!NOTE]
> 이 기능은 페이지 검사기의 버전 1.3을 필요합니다.


CSS 자동 동기화 기능을 사용 하면 CSS 파일을 직접 편집 하 고 페이지 검사기 브라우저에서 즉시 변경 내용을 확인할 수 있습니다.

클릭 **검사** 를 검사 모드에서 페이지 검사기를 배치 합니다.

페이지 검사기 브라우저에서 "홈 페이지" 섹션까지 위로 마우스 포인터를 이동 합니다 **div.content 래퍼** 레이블이 나타납니다. 이 요소를 한 번 클릭 합니다.

합니다 **스타일** 이 요소에 대 한 CSS 규칙의 모든 창을 표시 합니다. 찾기.featured.content 래퍼 클래스 선택기까지 아래로 스크롤하십시오. ".Featured.content-래퍼"를 클릭 합니다. 페이지 검사기 (Site.css)이이 스타일을 정의 하 고 해당 CSS 스타일을 강조 표시 하는 CSS 파일을 엽니다.

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

이제 값을 변경 `background-color` "red"로 합니다. 페이지 검사기 브라우저에 변경 내용을 즉시 표시 됩니다.

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a>CSS 색 선택을 사용 하 여

Visual Studio 2012에서 CSS 편집기에 쉽게 선택 하 고 색을 삽입 하는 색 선택 합니다. 색 선택 표준 색 팔레트가 포함 표준 색 이름, 해시 코드, RGB, RGBA, HSL 및 HSLA 색을 지원 하며 문서에서 가장 최근에 사용 했던 색 목록을 유지 관리 합니다.

이전 섹션에서 값을 변경 하 여 `background-color` 속성입니다. 색 선택기를 호출 하려면 속성 이름 및 형식을 후 삽입 포인터를 놓습니다 **#** 하거나 **rgb (** 합니다.

![CSS 색 선택 막대](using-page-inspector-in-aspnet-mvc/_static/image36.png)

아래쪽 화살표 키를 누르거나 선택한 색을 클릭 하 고 왼쪽 및 오른쪽 화살표 키를 사용 하 여 색을 트래버스할 수 있습니다. 색을 방문 하면 해당 16 진수 값을 미리 보기:

![미리 보기 배경 색 속성 값](using-page-inspector-in-aspnet-mvc/_static/image38.png)

색 막대 없는 경우 원하는 정확한 색, 색 선택 팝업 목록을 사용할 수 있습니다. 를 열려면 색 막대의 오른쪽 끝에서 이중 펼침 단추를 클릭 하거나 키보드의 아래쪽 화살표 또는 두 번 누릅니다.

![CSS 색 선택 팝업 다운](using-page-inspector-in-aspnet-mvc/_static/image40.png)

오른쪽에 있는 세로 막대에서 색을 클릭 합니다. 주 창에서 해당 색 그라데이션을 보여 줍니다. Enter 키를 눌러 세로 막대에서 직접 색을 선택 하거나 더 높은 정밀도 사용 하 여 선택할 수 주 창의 시점을 클릭 합니다.

사용 하려는 컴퓨터 화면에서 색을 있는지 (Visual Studio 사용자 인터페이스 내에 없는 함), 오른쪽 아래에 스 포 이트 도구를 사용 하 여 해당 값을 캡처할 수 있습니다.

색 편집기의 맨 아래에서 슬라이더를 이동 하 여 색의 불투명도 변경할 수도 있습니다. 이렇게 하면 변경 내용을 색 값을 RGBA 값 RGBA 형식을 불투명도 나타낼 수 있으므로 합니다.

색을 선택한 후 enter 키를 한 다음 배경색 항목을 완료 하려면 세미콜론을 입력 합니다 *Site.css* 파일입니다.

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>페이지 검사기 업데이트 표시줄

페이지 검사기는 즉시 변경 감지 합니다 *Site.css* 파일과 업데이트 표시줄이에 경고를 표시 합니다.

![업데이트 표시줄](using-page-inspector-in-aspnet-mvc/_static/image42.png)

모든 파일을 저장 하 고 페이지 검사기 브라우저 새로 고침을 Ctrl + Alt + Enter 누르거나 업데이트 표시줄을 클릭 합니다. 강조 표시 색 변화는 브라우저에 나타납니다.

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a>동적 페이지 요소를 JavaScript에 매핑

최신 웹 응용 프로그램에서 페이지의 요소는 JavaScript를 사용 하 여 동적으로 생성 경우가 많습니다. 즉, 이러한 페이지 요소에 해당 하는 없는 정적 태그 (HTML 또는 Razor).

버전 1.3 사용 하 여 페이지 검사기에 페이지를 다시 해당 JavaScript 코드에 동적으로 추가 된 항목에 이제 매핑할 수 있습니다. 이 기능을 보여 주기 위해 사용 합니다 [단일 페이지 응용 프로그램 (SPA) 템플릿](../../../single-page-application/overview/introduction/knockoutjs-template.md)합니다.

> [!NOTE]
> SPA 템플릿에 필요 합니다 [ASP.NET 및 웹 도구 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) 업데이트 합니다.


Visual Studio에서 선택 **파일** &gt; **새 프로젝트**합니다. 왼쪽의 확장 **Visual C#** 를 선택 **웹**를 선택한 후 **ASP.NET MVC4 웹 응용 프로그램**합니다. **확인**을 클릭합니다.

에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **단일 페이지 응용 프로그램**합니다.

솔루션 탐색기에서 확장을 **뷰** 폴더 차례로 합니다 **홈** 폴더. Index.cshtml 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **페이지 검사기에서 보기**합니다.

페이지 검사기 브라우저에서이 먼저 표시 되는 로그인 페이지입니다. "등록"을 클릭 하 고 사용자 이름 및 암호를 만듭니다. 등록 하면 응용 프로그램 로그인 하 고 몇 가지 샘플 항목 할 일 목록을 만듭니다.

클릭 **검사** 를 검사 모드에서 페이지 검사기를 배치 합니다. 페이지 검사기 브라우저에서 할 일 항목 중 하나를 클릭 합니다. 파란색으로 강조 표시 되는 대신 요소는 주황색으로 강조 표시, "JS"를 사용 하 여 요소 이름 옆에 있는 알 수 있습니다. 이 스크립트를 통해 동적으로 요소 만들어졌음을 나타냅니다.

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

에 주황색 밑줄이 표시 되는 또한 합니다 **호출 스택** 탭 합니다. 이 나타내는 합니다 **호출 스택** 창에는 요소에 대 한 자세한 정보.

클릭 합니다 **호출 스택** 탭 합니다. 합니다 **호출 스택** 요소를 만든 JavaScript 호출이 다소 어렵게 호출 스택 창에 표시 합니다. 외부 라이브러리에 jQuery 축소 되어 있으면 같은 있도록 호출 응용 프로그램 스크립트에 대 한 호출을 쉽게 확인할 수 있습니다.

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

외부 라이브러리에 대 한 호출을 포함 하 여 전체 스택을 보려면 "외부 라이브러리" 이라는 노드를 확장할 수 있습니다.

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

호출 스택의 항목을 클릭 하면 Visual Studio 코드 파일이 열리고 해당 스크립트를 강조 표시 합니다.

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a>참고 항목

[Visual Studio를 사용 하 여 ASP.NET MVC 4 소개](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net 웹 사이트)

[페이지 검사기 소개](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (채널 9 비디오)

[페이지 검사자 오류 메시지](https://go.microsoft.com/?linkid=9813062) (MSDN)
