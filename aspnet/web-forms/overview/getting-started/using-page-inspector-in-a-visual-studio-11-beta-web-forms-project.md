---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: Visual Studio 2012에 ASP.NET Web forms 페이지 검사기 사용 | Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 용 페이지 검사기는 통합 된 브라우저를 사용 하 여 웹 개발 도구입니다. 통합 된 브라우저 및 페이지 검사기에서 모든 요소를 선택 하는 중...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: d2c377f8466f8f324b75ce60860aa00c11bc0ffe
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837675"
---
<a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a>ASP.NET Web Forms에서 Visual Studio 2012 용 페이지 검사기 사용
====================
Tim Ammann 여

> Visual Studio 2012 용 페이지 검사기는 통합 된 브라우저를 사용 하 여 웹 개발 도구입니다. 통합 된 브라우저에서 모든 요소를 선택 하 고 요소의 소스 및 CSS 페이지 검사기를 즉시 강조 표시 합니다. 응용 프로그램에서 모든 페이지를 탐색, 신속 하 게 렌더링 된 태그의 원본을 살펴봅니다를 Visual Studio 환경 내에서 바로 브라우저 도구를 사용 합니다.
> 
> 이 자습서 shwos 검사 모드를 활성화 한 후 신속 하 게 찾아 CSS 규칙 및 웹 프로젝트 내에서 텍스트를 편집 하는 방법입니다. 이 자습서에서는 Web Forms 응용 프로그램 프로젝트를 사용 하지만 웹 사이트 프로젝트에 대 한 페이지 검사기를 사용할 수도 있습니다 및 [MVC](https://go.microsoft.com/?linkid=9802002) 응용 프로그램입니다.
> 
> 이 자습서에는 다음 섹션이 있습니다.
> 
> [필수 조건](#_1_prerequisites)
> 
> [웹 응용 프로그램 만들기](#_2_creating_a)
> 
> [페이지 검사기를 사용 하 여 응용 프로그램을 보려면](#_3_using_page)
> 
> [검사 모드를 사용 하도록 설정](#_4_inspection_mode)
> 
> [페이지 검사기를 사용 하 여 태그를 변경 하려면](#_5_using_page)
> 
> [HTML 창과 검사 모드](#_6_inspection_mode)
> 
> [스타일 창에서 CSS 변경 내용 미리 보기](#_7_previewing_css)
> 
> [CSS 자동 동기화](#css_auto_sync)
> 
> [CSS 색 선택을 사용 하 여](#css_color_picker)


<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>전제 조건

- [Visual Studio 2012](https://www.microsoft.com/visualstudio/11) 나 [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)합니다.

> [!NOTE]
> 페이지 검사기의 최신 버전을 사용 [웹 플랫폼 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=255386) .NET 2.0에 대 한 Azure SDK를 설치 합니다.


페이지 검사기는 Microsoft Web 개발자 도구를 사용 하 여 제공 됩니다. 최신 버전 1.3입니다. 어떤 버전을 확인 하려면, Visual Studio를 실행 있고 선택 **Microsoft Visual Studio 정보** 에서 합니다 **도움말** 메뉴.

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>웹 응용 프로그램 만들기

먼저 사용 하 여 페이지 검사기 사용 하 여 웹 응용 프로그램을 만들게 됩니다. Visual Studio에서 선택 **파일** &gt; **새 프로젝트**합니다. 왼쪽의 확장 **Visual C#** 를 선택 **웹**를 선택한 후 **ASP.NET Web Forms 응용 프로그램**합니다.

![새 Web Forms 응용 프로그램](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

**확인**을 클릭합니다.

응용 프로그램에서 엽니다 **원본** 보기.

![소스 뷰에서 새 Web Forms 응용 프로그램](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

응용 프로그램 사용을 설정 했으므로 점검 하 여 수정 페이지 검사기를 사용할 수 있습니다.

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a>페이지 검사기를 사용 하 여 응용 프로그램을 보려면

다음으로, 페이지 검사기를 사용 하 여 응용 프로그램에 살펴봅니다. **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택한 **페이지 검사기에서 보기**합니다.

![페이지 검사기에서 보기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

기본적으로 페이지 검사기가 처음으로 시작 되 면 도킹 될 좁은 창으로 Visual Studio 환경의 왼쪽에 있습니다. 도구 영역 중 하나에서 위쪽, 아래쪽 또는 오른쪽에 도킹 되거나를 편리 하 게 되는 너비를 설정 하 고 왼쪽에 도킹 된 상태로 두십시오.

![페이지 검사기 도킹 위치](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

페이지 검사기 창의 도킹을 해제 하는 경우 배치할 수 있습니다 Visual Studio 외부에서 또는 두 번째 모니터에도 있는 경우. 그러나 하려면 ALT + TAB 페이지 검사기 및 Visual Studio 사이에서 페이지 검사기 창을 도킹 없는 경우 이동할 **도구가** &gt; **옵션** &gt;  **환경** &gt; **탭과 Windows**, 및 **탭도**호출 하는 확인란의 선택을 취소 **부동 도구 창 위쪽에 항상 유지 합니다 주 창**:

![ALT + TAB Visual Studio와 도킹 되지 않은 페이지 검사기 창 사이 부동 도구 windows 확인란의 선택을 취소합니다](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

페이지 검사기 창 상단의 브라우저 창에서 현재 페이지를 보여 줍니다. 아래쪽 창 왼쪽에서 HTML 태그에서 페이지가 표시 되 고 일부 탭 수 있도록 하는 오른쪽 페이지의 다양 한 측면을 검사 합니다. 아래쪽 창은 비슷합니다는 [F12 개발자 도구](https://msdn.microsoft.com/ie/aa740478) Internet Explorer에서. 그러나 (개발자 도구와는 달리 사용할 수 있습니다 Visual Studio 내에서 오른쪽 페이지 검사기.)

![페이지 검사기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

이 자습서에서는 페이지 검사기 브라우저 창에서 사용할지 및 **HTML** 하 고 **스타일** 수 있도록 신속 하 게 탭 탐색 및 응용 프로그램에 대 한 변경.

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a>검사 모드를 사용 하도록 설정

다음으로, 페이지 검사기의 검사 모드의 작동 원리에 대해 표시 됩니다. 페이지 검사기 창에서 클릭 합니다 **검사** 단추입니다.

![요소를 검사 합니다.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

실행 중인 검사 모드를 확인 하려면 페이지 검사기 브라우저 창 내에서 페이지의 다른 부분 위로 마우스를 이동 합니다. 마찬가지로, 마우스 포인터 큰 더하기 기호를으로 변경 되 고 아래에 있는 요소가 강조 표시 됩니다.

![Div.content 래퍼를 가리키면](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

마우스 포인터를 이동 하면 note는

- 내용을 **원본** 보기 페이지에서 선택한 요소에 해당 태그를 표시 하도록 변경 합니다. 관련 태그 강조 표시 됩니다. 원본이 다른 파일에 있으면 해당 파일이 강조 표시 된 관련 태그를 사용 하 여 소스 뷰에서 열립니다.

- 에 표시 되는 태그를 **HTML** 페이지 검사기에서 탭 페이지에서 선택한 요소에 일치 하도록 변경 합니다. 에 **HTML** 탭 관련 태그는 설명 합니다.

- 합니다 **스타일** 탭 현재 선택 영역에 관한 CSS 규칙이 표시 됩니다.

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>페이지 검사기를 사용 하 여 태그를 변경 하려면

이제를 찾고 태그 또는 위치가 즉시 명확 하지 않을 텍스트 변경 페이지 검사기를 사용 하는 방법을 표시 됩니다.

검사 모드에서 페이지 검사기를 배치 하 고 홈 페이지의 아래쪽으로 스크롤하십시오.

영역의 바닥글 부분을 입력 하면 즉시 페이지 검사기 열립니다는 *Site.Master* 레이아웃 파일의 **원본** 오른쪽에 다른 임시 탭에서 보기 탭 및 마스터 부분을 강조 표시는 페이지 선택 했습니다. 이렇게 하면 페이지 검사기 수 검색 하 고 원래 열과 다른 파일에서 실제로 수행할 수 있는 페이지에 콘텐츠를 표시 하는 방법.

![검사 모드에서 바닥글 강조 표시](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

페이지 검사기 브라우저 창에서 저작권 정보를 사용 하 여 줄 위로 마우스 포인터를 이동 <a id="a"> </a>알 수 있습니다.

에 *Site.Master* 페이지에서 해당 줄이 강조 표시 합니다.

![바닥글 저작권 줄 강조 표시](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

줄의 끝에 일부 텍스트를 추가 합니다 *Site.Master* 파일입니다.

&lt;p&gt;&amp;복사 합니다. &lt;%: DateTime.Now.Year %&gt; -내 ASP.NET 응용 프로그램 Rocks!&lt; / p&gt;

이제 Ctrl + Alt + Enter를 누르거나 페이지 검사기 브라우저 창에서 결과 볼 수 업데이트 표시줄을 클릭 합니다.

![내 ASP.NET 응용 프로그램 Rocks!](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

바닥글에 있었음을 생각 합니다 *Default.aspx* 페이지 하지만 탓에 마스터 레이아웃 페이지에서를 페이지 검사기를 찾았습니다.

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>HTML 창과 검사 모드

다음으로, HTML 창과 요소를 매핑되는 방법을 빠르게 확인을 해야 합니다.

검사 모드에서 페이지 검사기를 배치 합니다.

![요소를 검사 합니다.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

"사용자 로고는 여기" 라고 표시 되는 페이지의 위쪽을 클릭 합니다. 보다 세부적으로 마우스 포인터를 이동 하면 브라우저 창에 표시를 변경 하는 더 이상 특정 요소를 검사 하 고 없습니다.

이제 마우스 포인터를 이동 합니다 **HTML** 창입니다. 마우스 포인터를 이동 하면 페이지 검사기 내의 요소를 설명 합니다 **HTML** 창 고 브라우저 창에서 해당 요소를 강조 표시 합니다.

![HTML 창](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

페이지 검사기가 열리면 이전에 *Site.Master* 임시 탭에서 파일입니다. Site.Master 탭을 클릭 하 고 해당 태그에서 강조 표시 됩니다는 &lt;헤더&gt; 섹션:

![강조 표시 된 태그](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>스타일 창에서 CSS 변경 내용 미리 보기

다음으로 표시 됩니다 페이지 검사기를 사용 하는 방법을 **스타일** css 변경 내용 미리 보기 창입니다.

클릭 합니다 **검사** 검사 모드에서 페이지 검사기를 배치 하는 단추입니다.

페이지 검사기 브라우저 창에서 마우스 포인터를 이동 될 때까지 "홈 페이지" 섹션을 마우스로 합니다 **div.content 래퍼** 레이블이 나타납니다.

![요소를 마우스로 가리킬](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

Div.content 래퍼 섹션 내에서 한 번 클릭 하 고 다음으로 마우스 포인터를 이동 합니다 **스타일** 창입니다. 아래.featured.content 래퍼 클래스 선택기를 지우고 배경색 속성에 대 한 확인란을 선택 합니다.

![투명 한 배경이 색](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

방법 변경 내용을 미리 봅니다. 즉시 페이지 검사기 브라우저 창에서 확인할 수 있습니다.

다시 확인란을 선택, 다음 속성 값을 두 번 클릭 하 고 변경 `red`합니다. 변경 내용을 즉시 보여 줍니다.

![빨강 배경색.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

합니다 **스타일** 스타일으로 변경 내용을 커밋하기 전에 변경 하는 쉽게 테스트 하 고 CSS를 미리 보기 창을 사용 하면 자체 시트입니다.

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>CSS 자동 동기화

> [!NOTE]
> 이 기능은 페이지 검사기의 버전 1.3을 필요합니다.


CSS 자동 동기화 기능을 사용 하면 CSS 파일을 직접 편집 하 고 페이지 검사기 브라우저에서 즉시 변경 내용을 확인할 수 있습니다.

클릭 **검사** 를 검사 모드에서 페이지 검사기를 배치 합니다.

페이지 검사기 브라우저에서 "홈 페이지" 섹션까지 위로 마우스 포인터를 이동 합니다 **div.content 래퍼** 레이블이 나타납니다. 이 요소를 한 번 클릭 합니다.

합니다 **스타일** 이 요소에 대 한 CSS 규칙의 모든 창을 표시 합니다. 찾기.featured.content 래퍼 클래스 선택기까지 아래로 스크롤하십시오. ".Featured.content-래퍼"를 클릭 합니다. 페이지 검사기 (Site.css)이이 스타일을 정의 하 고 해당 CSS 스타일을 강조 표시 하는 CSS 파일을 엽니다.

![CSS 파일](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

이제 값을 변경 `background-color` "red"로 합니다. 페이지 검사기 브라우저에 변경 내용을 즉시 표시 됩니다.

![페이지 검사기 브라우저](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a>CSS 색 선택을 사용 하 여

다음으로, 페이지 검사기를 사용 하 여 신속 하 게 찾아서 CSS 기본 응용 프로그램에서 강조 표시 된 텍스트를 변경 하는 방법에 알아봅니다. 이 예제에서는 없는 파란색 강조 표시 하 고 싶으면 다른 색으로 변경 하려면 결정 하면 됩니다.

클릭 합니다 **검사** 단추입니다.

![요소를 검사 합니다.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

페이지 검사기 브라우저 창에서 위로 마우스 포인터를 강조 표시 된 "비디오, 자습서 및 샘플" 텍스트가 CSS "표시" 레이블 되도록 표시 됩니다.

![표시 요소를 가리키면](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

텍스트 선택를 클릭 합니다. 해당 CSS 표시 선택기의 맨 아래에 표시 되는 **스타일** 창입니다.

![스타일 창에서 선택기를 표시 합니다.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

Mark 선택기를 클릭 합니다. 열립니다는 *Site.css* 웹 응용 프로그램에 대 한 파일입니다. Site.css 탭을 클릭 하 고 해당 CSS 선택기를 강조 표시 됩니다.

![스타일 시트에서 선택기를 표시 합니다.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

선택한 배경색 속성을 사용 하 여 줄을 제거 합니다.

새 Visual Studio 2012 CSS 색 편집기 새 색을 선택 하는 데 사용할 이제 합니다 **표시** 배경색 속성입니다.

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a>Visual Studio 2012 CSS 색 선택을 사용 하 여

Visual Studio 2012에서 CSS 편집기에 쉽게 선택 하 고 색을 삽입 하는 색 선택 합니다. 간단한 색 막대 및 보다 세부적으로 제어를 제공 하는 "pop 다운" 선택기를 있습니다.

색 선택 표준 색 팔레트가 포함 표준 색 이름, 해시 코드, RGB, RGBA, HSL 및 HSLA 색을 지원 하며 문서에서 가장 최근에 사용 했던 색 목록을 유지 관리 합니다.

배경색 속성이 줄에서 "bc"를 입력 하 고 아래쪽 화살표를 한 번 키를 누릅니다.

"배경색"와 같은 하이픈으로 구분 된 속성에서 각 단어의 첫 번째 문자를 입력할 때 IntelliSense와 일치 하는 속성만 표시 하기에 대 한 목록이 필터링:

![Intellisense 필터링 값](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

이제 콜론을 입력 합니다. 작업을 수행 하면 전체 배경색 속성 이름을 삽입 됩니다. 형식 **#** 또는 **rgb (**, 색 선택 막대에 표시 됩니다.

![CSS 색 선택 막대](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

색 선택 막대의 작동 원리를 보려면 마우스 포인터를 사용 하 여 해당 색 또는 아래쪽 화살표 키를 누릅니다 및 다음 왼쪽 및 오른쪽 화살표 키를 사용 하 여 색을 트래버스 합니다. 색을 방문 하면 배경색 속성에 대 한 해당 값을 미리 보기:

![미리 보기 배경 색 속성 값](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

이 시점에서 선택한 값을 다음 CSS 항목을 완료 하려면 세미콜론 (;) Enter 키를 눌러 수 있습니다. 이제 이동 다음 섹션의 색 선택 팝업 목록의 작동 원리를 볼 수 있도록 합니다.

#### <a name="using-the-color-picker-pop-down"></a>색 선택 팝업 목록 사용

색 막대에 대 한 원하는 색에 없는 경우 pop 다운 색 선택기를 사용할 수 있습니다.

를 열려면 색 막대의 오른쪽 끝에서 이중 펼침 단추를 클릭 하거나 키보드의 아래쪽 화살표 또는 두 번 누릅니다.

![CSS 색 선택 팝업 다운](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

오른쪽에 있는 세로 막대에서 색을 클릭 합니다. 주 창에서 해당 색 그라데이션을 보여 줍니다. Enter 키를 눌러 세로 막대에서 직접 색을 선택 하거나 더 높은 정밀도 사용 하 여 선택할 수 주 창의 시점을 클릭 합니다.

사용 하려는 컴퓨터 화면에서 색을 있는지 (Visual Studio 사용자 인터페이스 내에 없는 함), 오른쪽 아래에 스 포 이트 도구를 사용 하 여 해당 값을 캡처할 수 있습니다.

색 편집기의 맨 아래에서 슬라이더를 이동 하 여 색의 불투명도 변경할 수도 있습니다. 이렇게 하면 RGBA 형식을 불투명도 나타낼 수 있으므로 색상 RGBA 값에 값을 변경 합니다.

색을 선택한 후 enter 키를 한 다음 배경색 항목을 완료 하려면 세미콜론을 입력 합니다 *Site.css* 파일입니다.

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>페이지 검사기 업데이트 표시줄

페이지 검사기를 즉시 변경 검색 합니다 *Site.css* 파일 (또는 응용 프로그램의 모든 파일)에 업데이트 표시줄이 경고를 표시 합니다.

![업데이트 표시줄](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

모든 파일을 저장 하 고 페이지 검사기 브라우저 새로 고침을 Ctrl + Alt + Enter 누르거나 업데이트 표시줄을 클릭 합니다. 강조 표시 색 변화는 브라우저에 나타납니다.

![강조 색 변경](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a>편리 하 게 Visual Studio 환경 내에서 오른쪽 페이지 검사기 브라우저를 새로 고치는 알 수 있습니다. 페이지 검사기를 사용 하 여 외부 브라우저를 대신 하 여 웹 응용 프로그램을 개발할 때 편집기에서 상태를 유지할 수 있습니다.

## <a name="see-also"></a>참고 항목

[페이지 검사기 소개](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (채널 9 비디오)

[페이지 검사자 오류 메시지](https://go.microsoft.com/?linkid=9813062) (MSDN)
