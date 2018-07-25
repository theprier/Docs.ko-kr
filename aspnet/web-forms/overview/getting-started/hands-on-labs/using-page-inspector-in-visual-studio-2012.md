---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: Visual Studio 2012에서 페이지 검사기 사용 | Microsoft Docs
author: rick-anderson
description: 이 실습 랩에서 찾기 및 페이지 검사기 Visual Studio에서 웹 페이지 문제를 해결 하는 새 도구를 알게 됩니다. 페이지 검사기는 새 도구는 b가...
ms.author: aspnetcontent
ms.date: 02/18/2013
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: ac945a23dc6ef060340320d047f13c8e81057138
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37833674"
---
<a name="using-page-inspector-in-visual-studio-2012"></a>Visual Studio 2012에서 페이지 검사기 사용
====================
[웹 캠프 팀](https://twitter.com/webcamps)

> 이 실습 랩에서 찾기 및 페이지 검사기 Visual Studio에서 웹 페이지 문제를 해결 하는 새 도구를 알게 됩니다.
> 
> 페이지 검사기는 Visual Studio에 브라우저 진단 도구를 제공 하 고 브라우저, ASP.NET 및 소스 코드 간에 통합된 된 환경을 제공 하는 새로운 도구입니다. Visual Studio IDE 내에서 직접 웹 페이지 (HTML, Web Forms, ASP.NET MVC 또는 웹 페이지)를 렌더링 하 고 소스 코드 및 결과 출력을 검토할 수 있습니다. 페이지 검사기를 사용 하면 웹 사이트를 쉽게 분해, 신속 하 게,부터 페이지를 빌드 및 신속 하 게 문제를 진단할 수 있습니다.
> 
> 오늘날 많은 Asp.net WebForms 등 적절 한 시간에서 유연 하 고 확장 가능한 웹 사이트를 만드는 웹 프레임 워크가 했습니다. 반면에 어렵습니다 아래에 도달할 때 IDE 템플릿 기반 페이지에 동적 콘텐츠 디자이너 뷰를 지원 하지 않으므로 페이지에는 문제를 찾습니다. 따라서 이러한 웹 사이트 사용자에 게 어떻게 표시 되는지 확인 하려면 브라우저에서 열려 있어야 합니다.
> 
> 웹 개발자 외부 도구를 사용 하 여 브라우저에서 정기적으로 실행 되는 문제를 찾을 수 있습니다. 그런 다음 IDE를 반환 하며 해결을 시작 합니다. 이 앞뒤로 IDE, 브라우저 및 프로 파일링 도구는 작업, 비효율적일 수 있습니다 하며 경우에 따라 문제를 재현 하려는 때마다 정리 캐시를 새로 배포 합니다.
> 
> 페이지 검사기의 장점만 결합 된 기능 집합을 사용 하 여 최고를 결합 하 여 웹 개발 (브라우저 도구) 클라이언트와 서버 (ASP.NET 및 소스 코드) 사이에서 간격이 연결 합니다.
> 
> Page Inspector를 사용 (서버 쪽 코드 포함)를 원본 파일의 요소를 생성 한 브라우저에서 렌더링할 HTML 태그를 볼 수 있습니다. 페이지 검사기에서는 CSS 속성과 DOM 요소 특성을 보려면 브라우저에서 즉시 반영 된 변경 내용을 수정할 수도 있습니다.
> 
> 이 실습 페이지 검사기 기능을 통해 안내를 사용 하 여 웹 응용 프로그램에서 문제를 해결 하도록 하는 방법을 표시 합니다. **이 랩에서 비슷한 흐름을 사용 하 여 다양 한 기술을 대상으로 하지만 두 연습을 포함 합니다. ASP.NET MVC 개발자 인 경우에 따라 하나; 연습 두 WebForms 개발자에 따라 연습 경우**합니다.
> 
> 이 실습을 이용 하면 향상 된 기능 및 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 내용을 적용 하 여 이전에 설명 된 새 기능을 통해 안내 합니다.
> 
> 웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)합니다.


<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 학습할 방법:

- 페이지 검사기를 사용 하 여 웹 사이트를 분해 합니다.
- 검사 하 고 페이지 검사기를 사용 하 여 CSS 스타일 변경 내용 미리 보기
- 검색 하 고 페이지 검사기를 사용 하 여 웹 페이지에서 문제를 해결 합니다.

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽을 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).
- Internet Explorer 9 이상

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습에 포함 됩니다.

1. [ASP.NET MVC 프로젝트에서 페이지 검사기를 사용 하는 연습 1:](#Exercise1)
2. [WebForms 프로젝트에서 페이지 검사기를 사용 하는 연습 2:](#Exercise2)

> [!NOTE]
> 각 실습은 다른 독립적으로 각 연습에 따라 할 수 있는 실습 시작 폴더에 있는 시작 솔루션에서 제공 됩니다. 연습에 대 한 소스 코드 내에 해당 연습에서 단계를 완료 합니다. 결과로 생성 되는 코드를 사용 하 여 Visual Studio 솔루션을 포함 하는 최종 폴더를 찾을 수 있습니다. 이 실습을 통해 작업 하는 동안 추가 도움이 필요한 경우 지침으로 이러한 솔루션을 사용할 수 있습니다.


이 랩을 완료 하기 위한 예상 시간: **30 분**합니다.

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a>ASP.NET MVC 프로젝트에서 페이지 검사기를 사용 하는 연습 1:

이 연습에서는 미리 보기 및 디버그 하는 방법을 배우게 됩니다는 **ASP.NET MVC 4** 사용 하 여 솔루션 **페이지 검사기**합니다. 첫째, 프로세스를 디버깅 하는 웹을 쉽게 수행할 수 있는 기능을 알아보려면 간략 한 둘러보기 도구 수행 합니다. 그런 다음 스타일 문제를 포함 하는 웹 페이지에서 작업 합니다. 페이지 검사기를 사용 하 여 문제를 생성 하는 소스 코드를 수정 하는 방법을 배웁니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>작업 1-페이지 검사기를 탐색 합니다.

이 태스크에서는 사진 갤러리를 표시 하는 ASP.NET MVC 4 프로젝트의 컨텍스트에서 페이지 검사기를 사용 하는 방법을 배웁니다.

1. 엽니다는 **시작할** 솔루션에 있는 **소스/e x 1-MVC4/시작/** 폴더.

   1. 일부 누락 된 NuGet 패키지를 다운로드 해야 하기 전에 계속 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 솔루션 탐색기에서 찾습니다 **Index.cshtml** 보기는 **/뷰/홈** 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 및 선택 **페이지 검사기에서 보기**합니다.

    ![페이지 검사기에서 미리 보기 위해 파일을 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image1.png "페이지 검사기에서 미리 보기 위해 파일을 선택 하면")

    *페이지 검사기에서 미리 보기 위해 파일을 선택 하면*
3. 페이지 검사기 창에 표시 됩니다는 */Home/Index* URL 소스 선택한 보기에 매핑됩니다.

    ![ThefirstcontactwithPageInspector](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    *페이지 검사기를 사용 하 여 첫 번째 연락처*

    페이지 검사기 도구는 Visual Studio 환경에 통합 되어 있습니다. 검사기는 강력한 HTML 프로파일러 함께 포함 된 브라우저를 포함합니다. 확인 페이지에 표시 되는 방식을 확인 하려면 솔루션을 실행할 필요가 없습니다.

    > [!NOTE]
    > 페이지 검사기 브라우저의 너비 열린된 페이지의 너비 보다 작은 경우 표시 되지 않습니다 페이지 적절 합니다. 이 경우 페이지 검사기의 너비를 조정 합니다.
4. 클릭 합니다 **파일** 페이지 검사기에서 탭 합니다.

    인덱스 페이지를 작성 하는 모든 소스 파일에 표시 됩니다. 이 기능은 부분 뷰 및 템플릿을 사용 하 여 작업 하는 경우에 특히 눈에 모든 요소를 식별할 수 있습니다. 열 수 있습니다도 각 파일의 링크를 클릭 하면 알 수 있습니다.

    ![파일 탭](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    *파일 탭*
5. 클릭 합니다 **검사 모드 설정/해제** 탭의 왼쪽에 있는 단추입니다.

    이 도구를 사용 하면 페이지의 모든 요소를 선택 하 고 HTML 및 Razor 코드를 참조 하세요.

    ![검사 모드 단추 설정/해제](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    *설정/해제 검사 모드 단추*
6. 페이지 검사기 브라우저에서 페이지 요소 위에 마우스 포인터를 이동 합니다. 렌더링된 된 페이지 부분 위로 마우스 포인터를 이동 하는 동안 요소 형식이 표시 되 고 Visual Studio 편집기에서 해당 소스 태그나 코드가 강조 표시 됩니다.

    ![Inspectionmodeinaction](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    *실행 중인 검사 모드*

    > [!NOTE]
    > 페이지 검사기 창을 최대화 하지 않습니다 또는 소스 코드를 보여 주는 미리 보기 탭을 볼 수 없습니다. 최대화 되었을 때 페이지 검사기에서 요소를 클릭 하면 선택 항목의 소스 코드를 나타나지만 페이지 검사기 창에 게 숨겨집니다.

    에 주의 기울여야 하는 경우는 **Index.cshtml** 파일인 선택한 요소를 생성 하는 소스 코드의 부분을 강조 표시 되어 있는지을 알 수 있습니다. 이 기능을 사용 하면 코드에 액세스 하는 직접 및 빠른 방법을 제공 하는 긴 소스 파일을 편집 합니다.

    ![Inspectingelements](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    *요소를 검사합니다.*
7. 클릭 합니다 **검사 모드 설정/해제** 단추 (![HTML 탭을 선택 하 고 페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 합니다.](using-page-inspector-in-visual-studio-2012/_static/image7.png "페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시할 HTML 탭을 선택 합니다.") ) 커서를 사용 하지 않도록 설정 합니다.
8. 선택 된 **HTML** 탭 페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 합니다.
9. HTML 태그에서 Koala 링크를 사용 하 여 목록 항목을 찾아 선택 합니다.

    코드를 선택 하면 해당 출력을 자동으로 강조 표시 하는 브라우저에서 확인할 수 있습니다. 이 기능은 HTML 블록을 페이지에 렌더링 되는 방법을 참조 하는 데 유용 합니다.

    ![페이지의 HTML 요소를 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image8.png "페이지의 HTML 선택 요소")

    *페이지에서 HTML 요소를 선택합니다.*
10. 클릭 합니다 **검사 모드 설정/해제** 단추를 사용 하도록 설정 *검사 모드* 탐색 모음을 클릭 합니다. 오른쪽의 HTML 코드의 스타일 창에서 선택한 요소에 적용 된 CSS 스타일을 사용 하 여 목록이 나타납니다.

    > [!NOTE]
    > 페이지 검사기를 열 수도 헤더 사이트 레이아웃의 일부 이므로 \_Layout.cshtml 파일 및 영향을 받는 코드의 세그먼트를 강조 표시 합니다.

    ![Discoveringstyles](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    *스타일 및 선택한 요소의 소스 파일 검색*
11. 사용 설정/해제 검사 포인터를 사용 하 여 주요 파란색 막대 아래 마우스 포인터를 이동 하 고 절반 원을 클릭 합니다.

    ![요소 선택](using-page-inspector-in-visual-studio-2012/_static/image10.png "요소 선택")

    *요소 선택*
12. 스타일 창에서 찾을 합니다 **배경 이미지** 아래에 있는 항목을 **.main 콘텐츠** 그룹. **선택 취소** 는 **배경 이미지** 를 살펴봅니다. 브라우저는 변경 내용의 즉시 반영 됩니다 하 원 숨겨지는지를 확인할 수 있습니다.

    > [!NOTE]
    > 페이지 검사기 스타일 탭에 적용할 변경 내용을 원래 스타일 시트는 영향을 주지 않습니다. 스타일을 선택 취소 하거나 만큼 있지만 페이지를 새로 고친 후 복원할 수는 해당 값을 변경할 수 있습니다.

    ![CSS 스타일을 설정 하거나 해제](using-page-inspector-in-visual-studio-2012/_static/image11.png "및 CSS 스타일을 사용 하지 않도록 설정")

    *설정 및 CSS 스타일을 사용 하지 않도록 설정*
13. 이제 클릭을 '**사용자 로고는 여기**' 검사 모드를 사용 하 여 헤더 텍스트입니다.
14. 에 **스타일** 탭에서 찾을 **글꼴 크기** 에서 CSS 특성를 **.site 제목** 그룹. 특성 값을 두 번 클릭 하 고 2.3 em 값을 바꿉니다 **3 em**, 누릅니다 **ENTER**합니다. 제목을 더 큰 표시 되는지 확인 합니다.

    ![페이지 검사기에서 CSS 값을 변경](using-page-inspector-in-visual-studio-2012/_static/image12.png "페이지 검사기에서 CSS 변경 값")

    *페이지 검사기에서 CSS 값을 변경*
15. 클릭 합니다 **스타일 추적** 페이지 검사기의 오른쪽 창에 있는 탭입니다. 이것이 특성 이름별으로 정렬 하 고 선택 항목을 적용할 모든 스타일을 참조 하는 대체 방법입니다.

    ![CSSstylestracing](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    *선택한 요소의 CSS 스타일 추적*
16. 페이지 검사기의 또 다른 기능은 레이아웃 창입니다. 탐색 모음을 선택한 다음 클릭 검사 모드를 사용 하 여 **레이아웃** 오른쪽 창에서 탭 합니다. 선택한 요소의 정확한 크기와 오프셋, 여백, 안쪽 여백 및 테두리 크기를 볼 수 있습니다. 이 보기에서 값을 수정할 수도 있습니다 알 수 있습니다.

    ![페이지 검사기에서 요소 레이아웃](using-page-inspector-in-visual-studio-2012/_static/image14.png "페이지 검사기에서 요소 레이아웃")

    *페이지 검사기에서 요소 레이아웃*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>작업 2-찾기 및 사진 갤러리에서 스타일 문제 해결

이전 버전의 Visual Studio를 사용 하 여 웹 페이지 문제를 진단 하는 어떻게는? Internet Explorer 개발자 도구 또는 Firebug와 같은 Visual Studio IDE 외부에서 실행 되는 도구를 디버깅 하는 웹 익숙할 것 이며 브라우저에만 HTML 이해 스크립팅 및 스타일, 기본 프레임 워크를 렌더링할 HTML을 생성 하는 동안. 이런 이유로 웹 페이지와 같은 어떻게 표시 되는지 확인 하려면 전체 사이트를 배포 해야 합니다.

아마도 감지 하 고 웹 사이트에서 문제를 해결 하려는 경우 다음이 단계를 수행 했습니다.

1. Visual Studio에서 솔루션을 실행 하거나 웹 서버에서 페이지를 배포 합니다.
2. 브라우저에서 개발자 도구를 사용 하거나 단순히 소스 코드와 스타일을 열고 문제 일치 시 키 려를 엽니다. 관련 된 파일을 찾을 사용 하는 합니다 &quot;검색&quot; 또는 &quot;파일에서 검색&quot; 스타일 클래스 이름 사용 하 여 기능 합니다.
3. 오류가 감지 되 면 웹 브라우저 및 서버를 중지 합니다.
4. 브라우저 캐시를 지웁니다.
5. 수정 프로그램을 적용 하려면 Visual Studio로 돌아갑니다. 테스트 하는 모든 단계를 반복 합니다.

ASP.NET MVC 4에서 없는 실제 WYSIWYG 그대로 스타일 문제를 대부분 실행 또는 웹 응용 프로그램을 배포 후 이후 단계에서 검색 됩니다. 이제 페이지 검사기를 사용 하 여 솔루션을 실행 하지 않고 모든 페이지를 미리 보려면는 것이 같습니다.

이 태스크에서는 페이지 검사기 사용 및 사진 갤러리 응용 프로그램 몇 가지 문제를 해결 합니다.

1. 페이지 검사기를 사용 하 여 찾습니다 합니다 **등록** 하며 **로그인** 헤더의 왼쪽에 있는 링크입니다.

    링크를 오른쪽의 예상된 된 위치에 표시 되지 않습니다 글머리 기호 목록 처럼 표시 됩니다에 유의 하십시오. 이제 링크를 오른쪽 맞춤 하 고 스타일을 다시 지정을 적절 하 게 됩니다.

    ![링크에서 등록 및 로그를 찾는](using-page-inspector-in-visual-studio-2012/_static/image15.png "링크에서 등록 및 로그 찾기")

    *링크에서 등록 및 로그 찾기*
2. 선택한 검사 모드를 설정/해제, 가까이에 없지만, 해당 코드를 열려면 등록 링크를 클릭 합니다.

    링크의 소스 코드에는  **\_LoginPartial.cshtml** 하지 Index.cshtml 파일 또는 \_Layout.cshtml 첫 번째 위치에서 찾을 수 있습니다 위치입니다. 올바른 소스 파일에 직접 배치 된 했으면 합니다.
3. 에 **스타일** 탭을 찾아 클릭 합니다 **<section> #login</section>** 항목 이러한 링크의 HTML 컨테이너입니다.

    있음을 합니다 **#login** 스타일에 자동으로 위치한 **Site.css** 클릭 한 후입니다. 또한 코드는 이제 강조 표시 됩니다.

    ![CSS 스타일을 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image16.png "CSS 스타일을 선택 합니다.")

    *CSS 스타일을 선택합니다.*
4. 주석 처리를 제거 합니다 **텍스트 맞춤** 을 열고 닫는 문자를 제거 하 여 강조 표시 된 코드에서 특성 및 저장 합니다 **Site.css** 파일입니다.

    페이지 검사기는 현재 페이지를 구성 하는 모든 다른 파일을 인식 하 고 이러한 파일 중 하나를 변경 하는 경우 검색할 수 있습니다. 사용자에 게 경고 때마다 브라우저에서 현재 페이지 원본 파일과 함께 동기화 되지 않았습니다.
5. 페이지 검사기 브라우저에서 페이지를 다시 로드 주소 표시줄 아래에 있는 막대를 클릭 합니다.

    ![페이지를 다시 로드](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    *페이지를 다시 로드*

    오른쪽에서 링크 됩니다 있지만 여전히 글머리 기호 목록 처럼 보입니다. 이제 글머리 기호 제거 및 링크를 가로로 정렬 합니다.

    ![업데이트 된 페이지](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    *업데이트 된 페이지*
6. 중 하나를 선택 하는 검사 모드를 사용 하 여 합니다 **&lt;li&gt;** 포함 된 항목을 &quot;등록&quot; 및 &quot;로그인&quot; 링크 합니다. 클릭 합니다  **&lt;섹션&gt; #login** 액세스 항목 **Styles.css** 코드입니다.

    ![스타일 찾기](using-page-inspector-in-visual-studio-2012/_static/image19.png "스타일 찾기")

    *스타일 찾기*
7. **Style.css**에 대 한 코드를 주석 처리 제거 **#login li** 항목입니다. 추가할 스타일 글머리 숨기고 항목 가로로 표시 됩니다.

    ![로그인 링크를 재지정](using-page-inspector-in-visual-studio-2012/_static/image20.png "로그인 링크를 재지정")

    *로그인 링크를 재지정*
8. 저장할 **Style.css** 파일 및 페이지를 다시 로드 하는 주소 아래에 있는 표시줄에서 한 번 클릭 합니다. 링크를 올바르게 표시 되는지 확인 합니다.

    ![링크는 왼쪽에서 오른쪽으로 정렬](using-page-inspector-in-visual-studio-2012/_static/image21.png "링크는 왼쪽에서 오른쪽으로 정렬")

    *왼쪽에서 오른쪽으로 정렬 하는 링크*
9. 마지막으로 머리글 제목을 변경 합니다. 검사 모드를 사용 하 여 **사용자 로고는 여기** 텍스트 및 생성 하는 소스 코드를 가져옵니다.
10. 에 이제  **\_Layout.cshtml**, 대체 '**여기에 로고**'텍스트'**사진 갤러리**'. 저장 하 고 페이지 검사기 브라우저를 업데이트 합니다.

    ![새 제목을 할당](using-page-inspector-in-visual-studio-2012/_static/image22.png "새 제목을 할당")

    *새 제목을 할당*

    ![PhotoGallerypage](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    *사진 갤러리 페이지 업데이트*
11. 마지막으로 선택 합니다 **PhotoGallery** 프로젝트 및 키를 눌러 **F5** 앱을 실행 합니다. 모든 변경 내용이 예상 대로 작동을 확인 합니다.

* * *

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a>WebForms 프로젝트에서 페이지 검사기를 사용 하는 연습 2:

이 연습에서는 미리 보기 및 페이지 검사기를 사용 하 여 WebForms 솔루션을 디버그 하는 방법을 배웁니다. 먼저 웹 디버깅 프로세스에 도움이 되는 페이지 검사기 기능에 대 한 간략 한 둘러보기 도구를 수행 합니다. 그런 다음 스타일 문제를 포함 하는 웹 페이지에서 작업 합니다. 페이지 검사기를 사용 하 여 문제를 생성 하는 소스 코드를 수정 하는 방법을 배웁니다.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>작업 1-페이지 검사기를 탐색 합니다.

이 태스크에서는 사진 갤러리를 보여 주는 WebForms 프로젝트의 컨텍스트에서 페이지 검사기 기능을 사용 하는 방법을 배우게 됩니다.

1. 엽니다는 **시작할** 솔루션에 있는 **소스/e x 2-WebForms/시작/** 폴더.

   1. 일부 누락 된 NuGet 패키지를 다운로드 해야 하기 전에 계속 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 솔루션 탐색기에서 찾습니다 **Default.aspx** 페이지를 마우스 오른쪽 단추로 클릭 하 고 선택 **페이지 검사기에서 보기**합니다.

    ![Default.aspx 페이지 검사기로 열기](using-page-inspector-in-visual-studio-2012/_static/image24.png "Default.aspx 페이지 검사기를 사용 하 여 열기")

    *페이지 검사기를 사용 하 여 열기 Default.aspx*
3. 페이지 검사기 창에는 Default.aspx 표시 됩니다.

    ![페이지 검사기에서 Default.aspx를 보는](using-page-inspector-in-visual-studio-2012/_static/image25.png "Default.aspx 페이지 검사기에서 보기")

    *Default.aspx 페이지 검사기에서 보기*

    페이지 검사기 도구는 Visual Studio 환경에 통합 되어 있습니다. 검사기는 선택한 코드를 보여 주는 강력한 HTML 프로파일러 함께 포함 된 브라우저를 포함 합니다. 확인 페이지에 표시 되는 방식을 확인 하려면 솔루션을 실행할 필요가 없습니다.

    > [!NOTE]
    > 페이지 검사기 브라우저의 너비 열린된 페이지의 너비 보다 작은 경우 표시 되지 않습니다 페이지 적절 합니다. 이 경우 페이지 검사기의 너비를 조정 합니다.
4. 클릭 합니다 **파일** 페이지 검사기에서 탭 합니다.

    렌더링된 된 기본 페이지를 작성 하는 모든 소스 파일에 표시 됩니다. 이것이 사용자 컨트롤과 마스터 페이지를 사용 하 여 작업 하는 경우에 특히 눈에 모든 요소를 식별 하는 유용한 기능입니다. 각 파일을 이동할 수 있는지 확인 합니다.

    ![파일 탭](using-page-inspector-in-visual-studio-2012/_static/image26.png "The 파일 탭")

    *파일 탭*
5. 클릭 합니다 **검사 모드 설정/해제** 탭의 왼쪽에 있는 단추입니다.

    이 도구를 사용 하면 페이지의 모든 요소를 선택 하 고 해당 HTML 코드와.aspx 소스를 참조 하세요.

    ![검사 모드 단추 토글](using-page-inspector-in-visual-studio-2012/_static/image27.png "검사 모드 설정/해제 단추")

    *설정/해제 검사 모드 단추*
6. 페이지 검사기 브라우저에서 페이지 요소 위로 마우스를 이동 합니다. 렌더링된 된 페이지 부분 위로 마우스 포인터를 이동 하는 동안 요소 형식이 표시 되 고 Visual Studio 편집기에서 해당 소스 태그나 코드가 강조 표시 됩니다.

    ![실행 중인 검사 모드](using-page-inspector-in-visual-studio-2012/_static/image28.png "실행 중인 검사 모드")

    *실행 중인 검사 모드*

    > [!NOTE]
    > 페이지 검사기 창을 최대화 하지 않습니다 또는 소스 코드를 보여 주는 미리 보기 탭을 볼 수 없습니다. 최대화 되었을 때 페이지 검사기에서 요소를 클릭 하면 선택 항목의 소스 코드를 나타나지만 페이지 검사기 창에 게 숨겨집니다.

    경우에 주의 기울여야 **Default.aspx** 파일인 선택한 요소를 생성 하는 소스 코드의 부분을 강조 표시 되어 있는지을 알 수 있습니다. 이 기능은 코드에 액세스 하는 직접 및 빠른 방법을 제공 하는 긴 원본 파일의 버전을 지원 합니다.

    ![요소를 검사할](using-page-inspector-in-visual-studio-2012/_static/image29.png "요소를 검사 합니다.")

    *요소를 검사합니다.*
7. 클릭 합니다 **검사 모드 설정/해제** 단추 (![Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.](using-page-inspector-in-visual-studio-2012/_static/image30.png "Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser 합니다.") ), 커서를 사용 하지 않도록 설정 페이지 검사기 탭에 있습니다.
8. 선택 된 **HTML** 탭 페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 합니다.
9. HTML 코드에서 Koala 링크를 사용 하 여 목록 항목을 찾아 선택 합니다.

    코드를 선택 하면 해당 출력은 자동으로 강조 표시 된 브라우저를 확인 합니다. 이 기능은 HTML 블록을 페이지에 렌더링 되는 방법을 참조 하는 데 유용 합니다.

    ![페이지에서 HTML 요소 선택](using-page-inspector-in-visual-studio-2012/_static/image31.png "페이지에서 HTML 요소를 선택 합니다.")

    *페이지에서 HTML 요소를 선택합니다.*
10. 클릭 합니다 **검사 모드 설정/해제** 단추를 사용 하도록 설정 *검사 모드* 탐색 모음을 클릭 합니다. 오른쪽의 HTML 코드의 스타일 창에서 선택한 요소에 적용 된 CSS 스타일을 사용 하 여 목록이 나타납니다.

    > [!NOTE]
    > 헤더 사이트 레이아웃의 일부분 이므로 페이지 검사기는 Site.Master 파일 열고 영향을 받는 코드의 세그먼트를 강조 표시 합니다.

    ![DiscoveringstylesWebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "스타일 및 선택한 요소의 소스 파일 검색")

    *스타일 및 선택한 요소의 소스 파일 검색*
11. 사용 설정/해제 검사 포인터를 사용 하 여 메뉴 모음 아래 마우스 포인터를 이동 하 고 빈 절반 원을 클릭 합니다.

    ![요소 선택](using-page-inspector-in-visual-studio-2012/_static/image33.png "요소 선택")

    *요소 선택*
12. 스타일 창에서 찾을 합니다 **배경 이미지** 아래에 있는 항목을 **.main 콘텐츠** 그룹. **선택 취소** 는 **배경 이미지** 를 살펴봅니다. 브라우저는 변경 내용의 즉시 반영 됩니다 하 원 숨겨지는지를 확인할 수 있습니다.

    > [!NOTE]
    > 페이지 검사기 스타일 탭에 적용할 변경 내용을 원래 스타일 시트는 영향을 주지 않습니다. 스타일을 선택 취소 하거나 만큼 있지만 페이지를 새로 고친 후 복원할 수는 해당 값을 변경할 수 있습니다.

    ![설정 및 해제 CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "및 CSS 스타일을 사용 하지 않도록 설정")

    *설정 및 CSS 스타일을 사용 하지 않도록 설정*
13. 이제 클릭을 '**프로그램** **로고는 여기 '** 검사 모드를 사용 하 여 헤더 텍스트입니다.
14. 에 **스타일** 탭에서 찾을 **글꼴 크기** 에서 CSS 특성를 **.site 제목** 그룹. 해당 값을 편집 하려면 특성을 한 번를 두 번 클릭 합니다. 값 바꾸기는 2.3em **3em**, 한 다음 ENTER를 누릅니다. 제목을 더 큰 표시 되는지 확인 합니다.

    ![페이지 Inspector2에서 CSS 값을 변경](using-page-inspector-in-visual-studio-2012/_static/image35.png "페이지 검사기에서 CSS 변경 값")

    *페이지 검사기에서 CSS 값을 변경*
15. 클릭 합니다 **스타일 추적** 페이지 검사기의 오른쪽 창에 있는 탭입니다. 이것이 특성 이름별으로 정렬 하 고 선택 항목을 적용할 모든 스타일을 참조 하는 대체 방법입니다.

    ![선택한 요소의 CSS 스타일 추적](using-page-inspector-in-visual-studio-2012/_static/image36.png "선택한 요소의 CSS 스타일 추적")

    *선택한 요소의 CSS 스타일 추적*
16. 페이지 검사기의 또 다른 기능은 레이아웃 창입니다. 탐색 모음을 선택한 다음 클릭 검사 모드를 사용 하 여 **레이아웃** 오른쪽 창에서 탭 합니다. 선택한 요소의 정확한 크기와 오프셋, 여백, 안쪽 여백 및 테두리 크기를 볼 수 있습니다. 이 보기에서 값을 수정할 수도 있습니다 알 수 있습니다.

    ![페이지 검사기에서 요소 레이아웃](using-page-inspector-in-visual-studio-2012/_static/image37.png "페이지 검사기에서 요소 레이아웃")

    *페이지 검사기에서 요소 레이아웃*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>작업 2-찾기 및 사진 갤러리에서 스타일 문제 해결

이전 버전의 Visual Studio를 사용 하 여 웹 페이지 문제를 진단 하는 어떻게는? Internet Explorer 개발자 도구 또는 Firebug와 같은 Visual Studio IDE 외부에서 실행 되는 도구를 디버깅 하는 웹 익숙할 것 이며 브라우저에만 HTML 이해 스크립팅 및 스타일, 기본 프레임 워크를 렌더링할 HTML을 생성 하는 동안. 이런 이유로 웹 페이지와 같은 어떻게 표시 되는지 확인 하려면 전체 사이트를 배포 해야 합니다.

아마도 감지 하 고 웹 사이트에서 문제를 해결 하려는 경우 다음이 단계를 수행 했습니다.

1. Visual Studio에서 솔루션을 실행 하거나 웹 서버에서 페이지를 배포 합니다.
2. 브라우저에서 개발자 도구를 사용 하거나 단순히 소스 코드와 스타일을 열고 문제 일치 시 키 려를 엽니다. 관련 된 파일을 찾을 사용 하는 합니다 &quot;검색&quot; 또는 &quot;파일에서 검색&quot; 스타일 클래스 이름 사용 하 여 기능 합니다.
3. 오류가 감지 되 면 웹 브라우저 및 서버를 중지 합니다.
4. 브라우저 캐시를 지웁니다.
5. 수정 프로그램을 적용 하려면 Visual Studio로 돌아갑니다. 테스트 하는 모든 단계를 반복 합니다.

더 실제 wysiwyg (위지윅)에서 ASP.NET WebForms, 일부 스타일 문제를 실행 또는 배포 후 이후 단계에서 검색 됩니다. 이제 페이지 검사기를 사용 하 여 솔루션을 실행 하지 않고 모든 페이지를 미리 보려면는 것이 같습니다.

이 태스크에서는 사진 갤러리 응용 프로그램의 몇 가지 문제를 해결 하기 위한 페이지 검사기를 사용 합니다. 다음 단계에서 검색 한 신속 하 게 헤더에 몇 가지 간단한 스타일 문제를 해결 합니다.

1. 페이지 검사를 사용 하 여 찾습니다 합니다 **등록** 하며 **로그인** 헤더의 왼쪽에 있는 링크입니다.

    링크를 오른쪽에 예상된 된 위치에 표시 되지 않도록 확인 합니다. 이제 오른쪽에 대 한 링크를 정렬 하 고 적절 하 게 스타일을 다시 적용 됩니다.

    ![왼쪽에 배치 하는 링크에 로그인](using-page-inspector-in-visual-studio-2012/_static/image38.png "왼쪽에 배치 하는 링크에 로그인")

    *로그인 링크는 왼쪽에 배치*
2. 선택한 검사 모드를 설정/해제를 사용 하 여 해당 코드를 열고 로그인 링크를 선택 합니다.

    링크 소스 코드에 있는 알림 합니다 **Site.Master** 파일 위치는 Default.aspx 페이지의 첫 번째 위치에서 볼 수 있습니다 하지; 올바른 소스 파일에서 직접 전환할 합니다.
3. 에 **스타일** 탭을 찾아 클릭 합니다  **&lt;섹션&gt; #login** 항목 이러한 링크의 HTML 컨테이너입니다.

    있음을 합니다 **#login** 스타일에 자동으로 위치한 **Site.css** 클릭 한 후입니다. 또한 코드는 이제 강조 표시 됩니다.

    ![CSS 스타일을 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image39.png "CSS 스타일을 선택 합니다.")

    *CSS 스타일을 선택합니다.*
4. 주석 처리를 제거 합니다 **텍스트 맞춤** 을 열고 닫는 문자를 제거 하 여 강조 표시 된 코드에서 특성 및 저장 합니다 **Site.css** 파일입니다.

    페이지 검사기는 현재 페이지를 구성 하는 모든 다른 파일을 인식 하 고 이러한 파일 중 하나를 변경 하는 경우 검색할 수 있습니다. 사용자에 게 경고 때마다 브라우저에서 현재 페이지 원본 파일과 함께 동기화 되지 않았습니다.
5. 페이지 검사기 브라우저에서 변경 내용을 저장 하 고 페이지를 다시 로드 주소 표시줄 아래에 있는 막대를 클릭 합니다.

    ![Reloadingthepage](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    *페이지를 다시 로드*

    오른쪽에서 링크 됩니다 있지만 여전히 글머리 기호 목록 처럼 보입니다. 이제 글머리 기호 제거 및 링크를 가로로 정렬 합니다.

    ![업데이트 된 페이지](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    *업데이트 된 페이지*
6. 중 하나를 선택 하는 검사 모드를 사용 하 여 합니다 **&lt;li&gt;** 포함 된 항목을 &quot;등록&quot; 및 &quot;로그인&quot; 링크 합니다. 클릭 합니다  **&lt;섹션&gt; #login** 액세스 항목 **Styles.css** 코드입니다.

    ![스타일 찾기](using-page-inspector-in-visual-studio-2012/_static/image42.png "스타일 찾기")

    *스타일 찾기*
7. **Style.css**에 대 한 코드를 주석 처리 제거 **#login li** 항목입니다. 추가할 스타일 글머리 숨기고 항목 가로로 표시 됩니다.

    ![로그인 링크를 재지정](using-page-inspector-in-visual-studio-2012/_static/image43.png "로그인 링크를 재지정")

    *로그인 링크를 재지정*
8. 저장할 **Style.css** 파일 및 페이지를 다시 로드 하는 주소 아래에 있는 표시줄에서 한 번 클릭 합니다. 링크를 올바르게 표시 되는지 확인 합니다.

    ![링크는 왼쪽에서 오른쪽으로 정렬](using-page-inspector-in-visual-studio-2012/_static/image44.png "링크는 왼쪽에서 오른쪽으로 정렬")

    *왼쪽에서 오른쪽으로 정렬 하는 링크*
9. 마지막으로 머리글 제목을 변경 합니다. 에 대 한 검색 하는 대신는 '**사용자 로고는 여기 '** 검사 모드는 텍스트를 클릭 하 고 생성 하는 소스 코드를 가져오면를 사용 하는 모든 파일에 텍스트입니다.

    ![사이트 제목 찾기](using-page-inspector-in-visual-studio-2012/_static/image45.png "사이트 제목 찾기")

    *사이트 제목 찾기*
10. 에 이제 **Site.Master**, 대체는 '**사용자 로고는 여기**'텍스트'**사진 갤러리**'. 저장 하 고 페이지 검사기 브라우저를 업데이트 합니다.

    ![사진 갤러리 페이지 업데이트](using-page-inspector-in-visual-studio-2012/_static/image46.png "사진 갤러리 페이지 업데이트")

    *사진 갤러리 페이지 업데이트*
11. 마지막으로 누릅니다 **F5** 체크 아웃 변경 내용이 예상 대로 작동 하는 모든 앱을 실행 하려면.

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습을 완료 하면 페이지 검사기를 사용 하 여 웹 응용 프로그램을 다시 빌드하고 브라우저에서 웹 사이트를 실행 하지 않고도 미리 하는 방법을 배웠습니다 있어야 합니다. 또한 신속 하 게 찾기 및 소스 코드에 렌더링된 된 출력에서 직접 액세스 하 여 버그를 수정 하는 방법에 배운 합니다.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 a: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**. 다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.

1. 로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다. 또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Windows Azure SDK를 사용 하 여 Web</em>&quot;합니다.
2. 클릭할 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.

    ![Visual Studio Express를 설치](using-page-inspector-in-visual-studio-2012/_static/image47.png "Visual Studio Express를 설치 합니다.")

    *Visual Studio Express를 설치 합니다.*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건에 동의](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    *사용 조건에 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **완료**합니다.

    ![설치 완료](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. 로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.

    ![VS Express for Web 타일](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    *VS Express for Web 타일*
