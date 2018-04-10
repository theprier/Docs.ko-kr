---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: 페이지 검사기를 사용 하 여 Visual Studio 2012에서 | Microsoft Docs
author: rick-anderson
description: 이 실습 랩에서 새로운 도구를 찾아 Visual Studio-에서 페이지 검사기에서에서 웹 페이지 문제 해결에서 검색 합니다. 페이지 검사기는 새 도구 b는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 052d29dba170d403c2b1c1667c55fc2c34045615
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
<a name="using-page-inspector-in-visual-studio-2012"></a>페이지 검사기를 사용 하 여 Visual Studio 2012에서
====================
으로 [웹 캠프 팀](https://twitter.com/webcamps)

> 이 실습 랩에서 새로운 도구를 찾아 Visual Studio-에서 페이지 검사기에서에서 웹 페이지 문제 해결에서 검색 합니다.
> 
> 페이지 검사기는 Visual Studio에 브라우저 진단 도구를 제공 하 고 브라우저, ASP.NET 및 소스 코드 간에 통합된 된 환경을 제공 하는 새로운 도구입니다. Visual Studio IDE 내에서 직접 웹 페이지 (HTML, Web Forms, ASP.NET MVC 또는 웹 페이지)를 렌더링 하 고 소스 코드와 출력 결과 살펴볼 수 있습니다. 페이지 검사기를 사용 하면 웹 사이트를 쉽게 분해 하 고, up, 처음부터 페이지를 빠르게 작성할 신속 하 게 문제를 진단할 수 있습니다.
> 
> 오늘날 여러 가지 ASP.NET MVC WebForms 등의 적절 한 시기에 유연 하 고 확장 가능한 웹 사이트를 생성 하는 웹 프레임 워크 했습니다. 반면에 도달할 더 어려워지므로 IDE에서 템플릿 기반 페이지 및 동적 콘텐츠에 디자이너 뷰를 지원 하지 않으므로 페이지에는 문제를 찾을 수 있습니다. 따라서 이러한 타사 웹 사이트가 사용자에 게 표시 되는 방식을 보려면 브라우저에서 열립니다.
> 
> 웹 개발자 외부 도구를 사용 하 여 브라우저에서 정기적으로 실행 하는 문제를 찾을 수 있습니다. 그런 다음 이러한 IDE 돌아가서 해결을 시작 합니다. 이 전환 IDE, 브라우저 및 프로 파일링 도구, 비효율적일 수 있습니다 활동과 경우에 따라 새로운 배포 및 정리 하는 문제를 재현 하 려 할 때마다 캐시를 필요로 합니다.
> 
> 페이지 검사기의 결합된 된 일련의 기능을 사용 하 여 두 장점 결합 하 여 웹 개발 (브라우저 도구) 클라이언트와 서버 (ASP.NET 및 소스 코드) 사이에서 간격이 연결 합니다.
> 
> 페이지 검사기를 사용 하는 원본 파일 (서버 쪽 코드 포함)의 요소를 브라우저에 렌더링 하는 HTML 태그를 생성 해야 볼 수 있습니다. 페이지 검사기도 CSS 속성 및 브라우저에 바로 반영 되 변경 내용을 보려면 DOM 요소 특성을 수정할 수 있습니다.
> 
> 이 실습 랩에서 페이지 검사기 기능 있습니다 안내 하 고 사용 하 여 웹 응용 프로그램의 문제를 해결 하도록 하는 방법을 보여 줍니다. **이 랩에서 비슷한 흐름을 사용 하 여 다양 한 기술을 대상으로 하지만 두 연습을 포함 합니다. ASP.NET MVC 개발자 인 경우에 따라 요소가 연습 두 WebForms 개발자에 따라 실행 중인 경우**합니다.
> 
> 이 랩에서 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 내용을 적용 하 여 이전에 설명 된 새로운 기능 및 향상 된 기능을 통해 설명 합니다.
> 
> 모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)합니다.


<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 배웁니다 하는 방법:

- 페이지 검사기를 사용 하 여 웹 사이트를 구성 해제
- 검사 하 고 페이지 검사기로 CSS 스타일 변경 내용 미리 보기
- 검색 하 고 페이지 검사기를 사용 하 여 웹 페이지에서 문제 해결

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).
- Internet Explorer 9 이상이

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습에 포함 됩니다.

1. [연습 1: 페이지 검사기를 사용 하 여 ASP.NET MVC 프로젝트의](#Exercise1)
2. [연습 2: WebForms 프로젝트에서 페이지 검사기를 사용 하 여](#Exercise2)

> [!NOTE]
> 각 연습 시작 솔루션을 개별적으로 각 연습에 따라 할 수 있는 작업의 시작 폴더에 있는 함께 제공 됩니다. 실행에 대 한 소스 코드에서 해당 연습에서 단계를 완료 한 결과인 코드와 함께 Visual Studio 솔루션을 포함 하는 최종 폴더를 찾을 수 있습니다. 이 실습 랩에서 진행할 때는 추가 도움이 필요한 경우 이러한 솔루션 가이드로 사용할 수 있습니다.


예상 소요 시간: **30 분**합니다.

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a>연습 1: 페이지 검사기를 사용 하 여 ASP.NET MVC 프로젝트의

이 연습에서는 미리 보기 및 디버그 하는 방법을 배우게 됩니다는 **ASP.NET MVC 4** 사용 하 여 솔루션 **페이지 검사기**합니다. 첫째, 웹 디버깅 프로세스를 용이 하 게 하는 기능에 알아보려면이 도구는 간략 한 및을 수행 합니다. 그런 다음 스타일 문제를 포함 하는 웹 페이지에서 작업 합니다. 페이지 검사기를 사용 하 여 문제를 생성 하는 소스 코드를 찾을 하 고 해결 하는 방법에 설명 합니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>작업 1-탐색 페이지 검사기

이 태스크에서는 페이지 검사기 사진 갤러리를 표시 하는 ASP.NET MVC 4 프로젝트의 컨텍스트에서 사용 하는 방법에 설명 합니다.

1. 열기는 **시작** 솔루션에 있는 **소스/e x 1-MVC4/시작/** 폴더입니다.

   1. 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 전에 계속 합니다. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 솔루션 탐색기에서 찾을 **Index.cshtml** 뷰에 **/뷰/홈** 폴더를 프로젝트 마우스 오른쪽 단추로 클릭 한 다음 선택 **페이지 검사기에서 보기**합니다.

    ![페이지 검사기에서 미리 보기 위해 파일을 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image1.png "페이지 검사기에서 미리 보기 위해 파일을 선택 하면")

    *페이지 검사기에서 미리 보기 위해 파일을 선택 하면*
3. 페이지 검사기 창에 표시 됩니다는 */Home/Index* 소스 선택한 뷰에 매핑되는 URL입니다.

    ![ThefirstcontactwithPageInspector](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    *페이지 검사기를 사용 하 여 첫 번째 연락처*

    페이지 검사기 도구는 Visual Studio 환경에 통합 됩니다. 검사기 내장된 브라우저, 강력한 HTML 프로파일러 함께 포함 되어 있습니다. 확인 페이지에 표시 되는 모양을 보려면 솔루션을 실행할 필요가 없습니다.

    > [!NOTE]
    > 페이지 검사기 브라우저의 너비는이 페이지의 너비 보다 작은 경우 표시 되지 않습니다 페이지 제대로 합니다. 이 경우 페이지 검사기의 너비를 조정 합니다.
4. 클릭는 **파일** 페이지 검사기의 탭에에서 있습니다.

    인덱스 페이지를 작성 하는 모든 소스 파일에 표시 됩니다. 이 기능은 부분 뷰 및 템플릿을 사용 하 여 작업할 때 특히 한 눈에 모든 요소를 식별할 수 있습니다. 또한 열 수 각 파일의 링크를 클릭 하는 경우를 확인 합니다.

    ![파일 탭](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    *파일 탭*
5. 클릭는 **검사 모드를 설정/해제** 탭의 왼쪽에 있는 단추를 합니다.

    이 도구는 페이지의 모든 요소를 선택 하 고 HTML 및 Razor 코드를 확인할 수 있습니다.

    ![검사 모드 단추 설정/해제](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    *토글 검사 모드 단추*
6. 페이지 검사기 브라우저에서 페이지 요소 위로 마우스 포인터를 이동 합니다. 렌더링된 된 페이지 부분 위로 마우스 포인터를 이동 하는 동안 요소 형식이 표시 되 고 해당 소스 태그 또는 코드가 Visual Studio 편집기에서 강조 표시 됩니다.

    ![Inspectionmodeinaction](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    *작업에서 검사 모드*

    > [!NOTE]
    > 페이지 검사기 창을 최대화 하지 않는 또는 소스 코드를 보여 주는 미리 보기 탭을 볼 수 없습니다. 가 최대화 될 때 페이지 검사기에 요소를 클릭 하면 선택 항목의 소스 코드는 표시 되지만 페이지 검사기 창이 숨겨집니다.

    에 주의 해야 하는 경우는 **Index.cshtml** 파일을 선택 된 요소를 생성 하는 소스 코드의 부분을 강조 표시 되어 있는지을 확인할 수 있습니다. 이 기능은 코드에 액세스 하는 직접 및 빠른 방법을 제공 하 긴 소스 파일을 편집할 수 있습니다.

    ![Inspectingelements](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    *요소를 검사합니다.*
7. 클릭는 **검사 모드를 설정/해제** 단추 (![페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 하려면 HTML 탭을 선택 합니다.] (using-page-inspector-in-visual-studio-2012/_static/image7.png "페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 하려면 HTML 탭을 선택 합니다.") )를 커서를 사용 하지 않도록 설정 합니다.
8. 선택 된 **HTML** 탭 페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 합니다.
9. HTML 태그에서 Koala 링크와 목록 항목을 찾아 선택 합니다.

    코드를 선택 하면 해당 출력은 자동으로 강조 표시 되어 있는지 브라우저에 표시 합니다. 이 기능은 미리 HTML 블록 페이지에 렌더링 되는 방식을 볼 수 있습니다.

    ![페이지의 HTML 요소를 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image8.png "페이지의 HTML을 선택 하면 요소")

    *페이지의 HTML 요소를 선택합니다.*
10. 클릭는 **검사 모드를 설정/해제** 사용할 수 있도록 단추 *검사 모드* 탐색 모음을 클릭 합니다. 오른쪽의 HTML 코드의 스타일 창에서 선택한 요소에 적용 된 CSS 스타일으로 목록이 나타납니다.

    > [!NOTE]
    > 페이지 검사기는 또한 열지 헤더 사이트 레이아웃에 포함 되므로 \_Layout.cshtml 파일 및 코드의 세그먼트에 영향을 강조 표시 합니다.

    ![Discoveringstyles](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    *스타일 및 선택 된 요소의 소스 파일 검색*
11. 토글 검사 포인터를 사용 하도록 설정 기능 갖춘된 파란색 막대 아래 마우스 포인터를 이동 하 고 절반 원을 클릭 합니다.

    ![요소 선택](using-page-inspector-in-visual-studio-2012/_static/image10.png "요소 선택")

    *요소 선택*
12. 스타일 창에서 찾습니다는 **배경 이미지** 항목 아래에서 **.main 콘텐츠** 그룹입니다. **선택을 취소** 는 **배경 이미지** 를 살펴봅니다. 브라우저는 변경 내용이 즉시 반영 됩니다 및 원 숨겨지는지를 확인할 수 있습니다.

    > [!NOTE]
    > 페이지 검사기 스타일 탭에 적용 하면 변경 내용이 원래 스타일 시트는 영향을 주지 않습니다. 스타일을 선택 취소 하거나 원하는 하지만 페이지를 새로 고친 후 복원 됩니다 만큼 여러 번 해당 값을 변경할 수 있습니다.

    ![CSS 스타일을 설정 하거나 해제](using-page-inspector-in-visual-studio-2012/_static/image11.png "활성화 및 CSS 스타일 사용 안 함")

    *사용 하도록 설정 및 CSS 스타일 사용 안 함*
13. 이제 클릭는 '**사용자 로고는 여기**' 검사 모드를 사용 하 여 헤더에는 텍스트입니다.
14. 에 **스타일** 탭에서 찾을 **글꼴 크기** CSS 특성에서 **.site 제목** 그룹입니다. 특성 값을 두 번 클릭 하 고 2.3 em 값을 바꿀 내용 **3 em**, 누릅니다 **ENTER**합니다. 제목 큰 표시 되는지 확인 합니다.

    ![페이지 검사기의 CSS 값을 변경](using-page-inspector-in-visual-studio-2012/_static/image12.png "페이지 검사기에 CSS 변경 값")

    *페이지 검사기의 CSS 값 변경*
15. 클릭는 **스타일 추적** 페이지 검사기의 오른쪽 창에 있는 탭입니다. 이것이 특성 이름으로 정렬 된 선택 항목에 적용 되는 모든 스타일을 참조 하는 대체 방법입니다.

    ![CSSstylestracing](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    *선택 된 요소의 CSS 스타일 추적*
16. 페이지 검사기의 다른 기능에는 레이아웃 창입니다. 탐색 모음을 선택한 다음 클릭 검사 모드를 사용 하 여 **레이아웃** 오른쪽 창에서 탭 합니다. 선택한 창의 정확한 크기와 오프셋, 여백, 안쪽 여백 및 테두리 크기가 표시 됩니다. 이 보기에서 값을 수정할 수도 수를 확인 합니다.

    ![페이지 검사기에서 요소 레이아웃](using-page-inspector-in-visual-studio-2012/_static/image14.png "페이지 검사기에서 요소 레이아웃")

    *페이지 검사기에서 요소 레이아웃*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>작업 2-확인 및 사진 갤러리 스타일 문제 수정

이전 버전의 Visual Studio 웹 페이지 문제를 진단할 어떻게는? Internet Explorer의 도구 개발자 또는 Firebug와 같은 Visual Studio IDE 외부에서 실행 되는 도구를 디버깅 하는 웹 익숙할 것 됩니다. 브라우저에 HTML, 이해 스크립팅 및 스타일, 기본 프레임 워크는 렌더링할 HTML을 생성 하는 동안 합니다. 이런 이유로 전체 사이트와 같은 웹 페이지의 모양을 확인를 배포 해야 하는 경우가 많습니다.

아마도 검색 하 고 웹 사이트에서 문제를 해결 하려는 경우 다음이 단계를 따라 했습니다.

1. Visual Studio에서 솔루션을 실행 하거나 웹 서버에서 페이지를 배포 합니다.
2. 브라우저에서 사용 하 여, 또는 단순히 소스 코드와 스타일을 열고 문제를 일치 시 키 려 개발자 도구를 엽니다. 관련 된 파일을 찾을 사용 했을 것은 &quot;검색&quot; 또는 &quot;파일에서 검색&quot; 스타일 클래스의 이름으로는 기능.
3. 오류가 감지 되 면 웹 브라우저와 서버를 중지 합니다.
4. 브라우저 캐시를 지웁니다.
5. 수정 프로그램을 적용 하려면 Visual Studio로 반환 합니다. 테스트 하는 모든 단계를 반복 합니다.

ASP.NET MVC 4의 없는 실제 WYSIWYG 그대로 스타일 문제를 대부분 실행 하거나 웹 응용 프로그램을 배포한 후에 이후 단계에서 검색 된 합니다. 이제 페이지 검사기 이므로 솔루션을 실행 하지 않고 모든 페이지를 미리 볼 수 있습니다.

이 태스크에서는 페이지 검사기를 사용 하 여 쿼리하고 사진 갤러리 응용 프로그램의 몇 가지 문제를 수정 합니다.

1. 페이지 검사기를 사용 하 여 찾습니다는 **등록** 및 **로그인** 머리글의 왼쪽에 링크 합니다.

    링크의 오른쪽에 예상된 위치에 표시 되지 않습니다는 글머리 기호 목록 처럼 표시 된에 유의 하십시오. 이제 오른쪽에 대 한 링크를 정렬 하 고 스타일을 다시 지정을 적절 하 게 됩니다.

    ![링크에서 레지스터 및 로그 찾기](using-page-inspector-in-visual-studio-2012/_static/image15.png "링크에서 레지스터 및 로그 찾기")

    *링크에서 레지스터 및 로그 찾기*
2. 선택한 검사 모드를 설정/해제를 사용 닫기를는 없지만, 해당 코드를 열려는 레지스터 링크를 클릭 합니다.

    링크의 소스 코드에 있는 공지는  **\_LoginPartial.cshtml** 파일, Index.cshtml 하지와 \_Layout.cshtml는는 첫 번째 위치에서 찾을 수 있습니다. 올바른 소스 파일에서 직접 넣었습니다.
3. 에 **스타일** 탭을 찾아서 클릭는 **<section> #login</section>** 항목 이러한 링크에 대 한 HTML 컨테이너입니다.

    다음에 유의 **#login** 스타일에 있는 자동으로 **Site.css** 클릭 합니다. 또한 코드는 이제 강조 표시 합니다.

    ![CSS 스타일을 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image16.png "CSS 스타일 선택")

    *CSS 스타일을 선택 하면*
4. 주석 처리 제거는 **-** 강조 표시 된 코드에서 여는 태그와 닫는 문자를 제거 하 여 특성을 저장할는 **Site.css** 파일입니다.

    페이지 검사기를 현재 페이지를 구성 하는 다른 모든 파일의 인식 하며 이러한 파일을 변경 하는 경우를 감지할 수 있습니다. 브라우저에서 현재 페이지 원본 파일과 함께 동기화 되지 않았습니다. 때마다 경우 알려 줍니다.
5. 페이지 검사기 브라우저에서 페이지를 다시 로드 하려면 주소 표시줄 아래에 있는 막대를 클릭 합니다.

    ![페이지를 다시 로드](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    *페이지를 다시 로드*

    오른쪽에 있는 링크는 이제 하지만 여전히 글머리 기호 목록 처럼 보입니다. 이제 글머리 기호를 제거 및 링크를 가로 방향으로 정렬 합니다.

    ![업데이트 페이지](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    *업데이트 페이지*
6. 검사 모드를 사용 하 여 중 하나를 선택는 **&lt;li&gt;** 포함 된 항목의 &quot;등록&quot; 및 &quot;로그인&quot; 링크 합니다. 클릭는  **&lt;섹션&gt; #login** 항목의 액세스 **Styles.css** 코드입니다.

    ![스타일 찾기](using-page-inspector-in-visual-studio-2012/_static/image19.png "스타일 찾기")

    *스타일 찾기*
7. **Style.css**에 대 한 코드를 주석 처리 제거 **#login li** 항목입니다. 추가 하는 스타일 글머리 기호 숨기고 항목 가로로 표시 됩니다.

    ![로그인 링크 스타일 재설정](using-page-inspector-in-visual-studio-2012/_static/image20.png "스타일의 로그인 링크를 재설정")

    *로그인 링크 스타일 재설정*
8. 저장 **Style.css** 파일 및 페이지를 다시 로드 하는 주소 아래에 있는 표시줄에 한 번 클릭 합니다. 링크는 올바르게 표시 되는지 확인 합니다.

    ![오른쪽으로 정렬 하는 링크](using-page-inspector-in-visual-studio-2012/_static/image21.png "오른쪽으로 정렬 하는 링크")

    *오른쪽으로 정렬 하는 링크*
9. 마지막으로, 머리글 제목을 변경 합니다. 검사 모드를 사용 하 여 클릭 하 여 **사용자 로고는 여기** 텍스트 및 get을 생성 하는 소스 코드를 실행 합니다.
10. 에 이제  **\_Layout.cshtml**, 대체 '**사용자 로고는 여기**'텍스트와 '**사진 갤러리**'. 저장 하 고 페이지 검사기 브라우저를 업데이트 합니다.

    ![새 제목을 할당](using-page-inspector-in-visual-studio-2012/_static/image22.png "새 제목을 할당")

    *새 제목을 할당*

    ![PhotoGallerypage](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    *업데이트 사진 갤러리 페이지*
11. 마지막으로, 선택은 **PhotoGallery** 프로젝트 및 키를 눌러 **F5** 앱을 실행 합니다. 모든 체크 아웃 변경 내용이 예상 대로 작동 합니다.

* * *

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a>연습 2: WebForms 프로젝트에서 페이지 검사기를 사용 하 여

이 연습에서는 미리 보기 및 페이지 검사기를 사용 하 여 WebForms 솔루션을 디버그 하는 방법에 설명 합니다. 웹 프로세스를 디버깅을 용이 하 게 하는 페이지 검사기 기능에 알아보려면 도구 관련 간략 한 랩을 먼저 수행 합니다. 그런 다음 스타일 문제를 포함 하는 웹 페이지에서 작업 합니다. 페이지 검사기를 사용 하 여 문제를 생성 하는 소스 코드를 찾을 하 고 해결 하는 방법에 설명 합니다.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>작업 1-탐색 페이지 검사기

이 태스크에서는 사진 갤러리를 보여 주는 WebForms 프로젝트의 컨텍스트에서 페이지 검사기 기능을 사용 하는 방법에 설명 합니다.

1. 열기는 **시작** 솔루션에 있는 **소스/e x 2-WebForms/시작/** 폴더입니다.

   1. 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 전에 계속 합니다. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 솔루션 탐색기에서 찾아 **Default.aspx** 페이지 마우스 오른쪽 단추로 클릭 한 다음 선택 **페이지 검사기에서 보기**합니다.

    ![Default.aspx 페이지 검사기를 사용 하 여 열기](using-page-inspector-in-visual-studio-2012/_static/image24.png "Default.aspx 페이지 검사기를 사용 하 여 열기")

    *페이지 검사기로 열기 Default.aspx*
3. 페이지 검사기 창에는 Default.aspx 표시 됩니다.

    ![Default.aspx 페이지 검사기에서 보기](using-page-inspector-in-visual-studio-2012/_static/image25.png "Default.aspx 페이지 검사기에서 보기")

    *Default.aspx 페이지 검사기에서 보기*

    페이지 검사기 도구는 Visual Studio 환경에 통합 됩니다. 검사기 내장된 브라우저, 선택한 코드를 표시 하는 강력한 HTML 프로파일러 함께 포함 되어 있습니다. 확인 페이지에 표시 되는 모양을 보려면 솔루션을 실행할 필요가 없습니다.

    > [!NOTE]
    > 페이지 검사기 브라우저의 너비는이 페이지의 너비 보다 작은 경우 표시 되지 않습니다 페이지 제대로 합니다. 이 경우 페이지 검사기의 너비를 조정 합니다.
4. 클릭는 **파일** 페이지 검사기의 탭에에서 있습니다.

    렌더링된 된 기본 페이지를 작성 하는 모든 소스 파일에 표시 됩니다. 이것은 사용자 정의 컨트롤 및 마스터 페이지를 사용 하 여 작업할 때 특히 한 눈에 모든 요소를 식별 하는 유용한 기능입니다. 각 파일을 이동할 수 있는지 확인 합니다.

    ![파일 탭](using-page-inspector-in-visual-studio-2012/_static/image26.png "파일 탭")

    *파일 탭*
5. 클릭는 **검사 모드를 설정/해제** 탭의 왼쪽에 있는 단추를 합니다.

    이 도구는 페이지의 모든 요소를 선택 하 고 해당 HTML 코드와.aspx 소스를 볼 수 있습니다.

    ![토글 검사 모드 단추](using-page-inspector-in-visual-studio-2012/_static/image27.png "검사 모드를 설정/해제 단추")

    *토글 검사 모드 단추*
6. 페이지 검사기 브라우저에서 페이지 요소 위로 마우스를 이동 합니다. 렌더링된 된 페이지 부분 위로 마우스 포인터를 이동 하는 동안 요소 형식이 표시 되 고 해당 소스 태그 또는 코드가 Visual Studio 편집기에서 강조 표시 됩니다.

    ![작업에서 검사 모드](using-page-inspector-in-visual-studio-2012/_static/image28.png "동작에서 검사 모드")

    *작업에서 검사 모드*

    > [!NOTE]
    > 페이지 검사기 창을 최대화 하지 않는 또는 소스 코드를 보여 주는 미리 보기 탭을 볼 수 없습니다. 가 최대화 될 때 페이지 검사기에 요소를 클릭 하면 선택 항목의 소스 코드는 표시 되지만 페이지 검사기 창이 숨겨집니다.

    에 주의 해야 하는 경우 **Default.aspx** 파일을 선택 된 요소를 생성 하는 소스 코드의 부분을 강조 표시 되어 있는지을 확인할 수 있습니다. 이 기능은 코드에 액세스 하는 직접 및 빠른 방법을 제공 하 긴 소스 파일의 버전을 지원 합니다.

    ![요소를 검사](using-page-inspector-in-visual-studio-2012/_static/image29.png "요소를 검사 합니다.")

    *요소를 검사합니다.*
7. 클릭는 **검사 모드를 설정/해제** 단추 (![Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.] (using-page-inspector-in-visual-studio-2012/_static/image30.png "Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser 합니다.") ), 커서를 사용 하지 않도록 설정 하려면 페이지 검사기 탭에 위치 합니다.
8. 선택 된 **HTML** 탭 페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 합니다.
9. HTML 코드에서 Koala 링크 된 목록 항목을 찾아 선택 합니다.

    코드를 선택 하면 해당 출력은 자동으로 강조 표시 된 브라우저를 확인 합니다. 이 기능은 미리 HTML 블록 페이지에 렌더링 되는 방식을 볼 수 있습니다.

    ![페이지의 HTML 요소를 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image31.png "페이지의 HTML 요소를 선택 합니다.")

    *페이지의 HTML 요소를 선택합니다.*
10. 클릭는 **검사 모드를 설정/해제** 사용할 수 있도록 단추 *검사 모드* 탐색 모음을 클릭 합니다. 오른쪽의 HTML 코드의 스타일 창에서 선택한 요소에 적용 된 CSS 스타일으로 목록이 나타납니다.

    > [!NOTE]
    > 헤더 사이트 레이아웃의 일부 이므로, 페이지 검사기는 Site.Master 파일 열고 영향을 받는 코드의 세그먼트를 강조 표시 합니다.

    ![DiscoveringstylesWebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "스타일과 선택 된 요소의 소스 파일 검색")

    *스타일 및 선택 된 요소의 소스 파일 검색*
11. 설정/해제 검사 포인터를 사용 하도록 설정, 메뉴 모음 아래 마우스 포인터를 이동 하 고 빈 반원을 클릭 합니다.

    ![요소 선택](using-page-inspector-in-visual-studio-2012/_static/image33.png "요소 선택")

    *요소 선택*
12. 스타일 창에서 찾습니다는 **배경 이미지** 항목 아래에서 **.main 콘텐츠** 그룹입니다. **선택을 취소** 는 **배경 이미지** 를 살펴봅니다. 브라우저는 변경 내용이 즉시 반영 됩니다 및 원 숨겨지는지를 확인할 수 있습니다.

    > [!NOTE]
    > 페이지 검사기 스타일 탭에 적용 하면 변경 내용이 원래 스타일 시트는 영향을 주지 않습니다. 스타일을 선택 취소 하거나 원하는 하지만 페이지를 새로 고친 후 복원 됩니다 만큼 여러 번 해당 값을 변경할 수 있습니다.

    ![설정 및 해제 CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "활성화 및 CSS 스타일 사용 안 함")

    *사용 하도록 설정 및 CSS 스타일 사용 안 함*
13. 이제를 클릭 합니다는 '**프로그램** **로고는 여기 '** 검사 모드를 사용 하 여 헤더에는 텍스트입니다.
14. 에 **스타일** 탭에서 찾을 **글꼴 크기** CSS 특성에서 **.site 제목** 그룹입니다. 특성을 한 번를 두 번 클릭 해당 값을 편집 합니다. Replace는 2.3em 값과 **3em**, 한 다음 ENTER 키를 누릅니다. 제목 큰 표시 되는지 확인 합니다.

    ![페이지 Inspector2에서 CSS 값을 변경](using-page-inspector-in-visual-studio-2012/_static/image35.png "페이지 검사기에 CSS 변경 값")

    *페이지 검사기의 CSS 값 변경*
15. 클릭는 **스타일 추적** 페이지 검사기의 오른쪽 창에 있는 탭입니다. 이것이 특성 이름으로 정렬 된 선택 항목에 적용 되는 모든 스타일을 참조 하는 대체 방법입니다.

    ![선택 된 요소의 CSS 스타일 추적](using-page-inspector-in-visual-studio-2012/_static/image36.png "선택 된 요소의 CSS 스타일 추적")

    *선택 된 요소의 CSS 스타일 추적*
16. 페이지 검사기의 다른 기능에는 레이아웃 창입니다. 탐색 모음을 선택한 다음 클릭 검사 모드를 사용 하 여 **레이아웃** 오른쪽 창에서 탭 합니다. 선택한 창의 정확한 크기와 오프셋, 여백, 안쪽 여백 및 테두리 크기가 표시 됩니다. 이 보기에서 값을 수정할 수도 수를 확인 합니다.

    ![페이지 검사기에서 요소 레이아웃](using-page-inspector-in-visual-studio-2012/_static/image37.png "페이지 검사기에서 요소 레이아웃")

    *페이지 검사기에서 요소 레이아웃*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>작업 2-확인 및 사진 갤러리 스타일 문제 수정

이전 버전의 Visual Studio 웹 페이지 문제를 진단할 어떻게는? Internet Explorer의 도구 개발자 또는 Firebug와 같은 Visual Studio IDE 외부에서 실행 되는 도구를 디버깅 하는 웹 익숙할 것 됩니다. 브라우저에 HTML, 이해 스크립팅 및 스타일, 기본 프레임 워크는 렌더링할 HTML을 생성 하는 동안 합니다. 이런 이유로 전체 사이트와 같은 웹 페이지의 모양을 확인를 배포 해야 하는 경우가 많습니다.

아마도 검색 하 고 웹 사이트에서 문제를 해결 하려는 경우 다음이 단계를 따라 했습니다.

1. Visual Studio에서 솔루션을 실행 하거나 웹 서버에서 페이지를 배포 합니다.
2. 브라우저에서 사용 하 여, 또는 단순히 소스 코드와 스타일을 열고 문제를 일치 시 키 려 개발자 도구를 엽니다. 관련 된 파일을 찾을 사용 했을 것은 &quot;검색&quot; 또는 &quot;파일에서 검색&quot; 스타일 클래스의 이름으로는 기능.
3. 오류가 감지 되 면 웹 브라우저와 서버를 중지 합니다.
4. 브라우저 캐시를 지웁니다.
5. 수정 프로그램을 적용 하려면 Visual Studio로 반환 합니다. 테스트 하는 모든 단계를 반복 합니다.

ASP.NET WebForms의 실제 WYSIWYG 더 있으면, 일부 스타일 문제를 실행 하거나 배포한 후에 이후 단계에서 검색 된 합니다. 이제 페이지 검사기 이므로 솔루션을 실행 하지 않고 모든 페이지를 미리 볼 수 있습니다.

이 태스크에서는 사진 갤러리 응용 프로그램의 몇 가지 문제를 해결 하기 위한 페이지 검사기를 사용 합니다. 다음 단계에서 검색 한 신속 하 게 헤더에 몇 가지 간단한 스타일 문제를 해결 합니다.

1. 검사 페이지를 사용 하 여 찾습니다는 **등록** 및 **로그인** 머리글의 왼쪽에 링크 합니다.

    알림 오른쪽에 예상된 위치에는 링크가 표시 되지 않습니다. 이제 오른쪽에 대 한 링크를 정렬 하 고 그에 따라 스타일을 다시 적용 됩니다.

    ![왼쪽에 배치 하는 링크 로그인](using-page-inspector-in-visual-studio-2012/_static/image38.png "왼쪽에 배치 하는 링크에 로그인")

    *로그인 링크 왼쪽에 배치*
2. 선택한 검사 모드를 설정/해제를 해당 코드를 열려는 로그인 링크를 선택 합니다.

    링크 소스 코드에 있는 통지는 **Site.Master** 안함 첫 번째 위치에서 찾을 수 있습니다 여기에서 Default.aspx 페이지에; 올바른 소스 파일에 직접 배치 했으면 파일을 합니다.
3. 에 **스타일** 탭을 찾아서 클릭는  **&lt;섹션&gt; #login** 항목 이러한 링크에 대 한 HTML 컨테이너입니다.

    다음에 유의 **#login** 스타일에 있는 자동으로 **Site.css** 클릭 합니다. 또한 코드는 이제 강조 표시 합니다.

    ![CSS 스타일을 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image39.png "CSS 스타일 선택")

    *CSS 스타일을 선택 하면*
4. 주석 처리 제거는 **-** 강조 표시 된 코드에서 여는 태그와 닫는 문자를 제거 하 여 특성을 저장할는 **Site.css** 파일입니다.

    페이지 검사기를 현재 페이지를 구성 하는 다른 모든 파일의 인식 하며 이러한 파일을 변경 하는 경우를 감지할 수 있습니다. 브라우저에서 현재 페이지 원본 파일과 함께 동기화 되지 않았습니다. 때마다 경우 알려 줍니다.
5. 페이지 검사기 브라우저에서 변경 내용을 저장 하 고 페이지를 다시 로드 하려면 주소 표시줄 아래에 있는 막대를 클릭 합니다.

    ![Reloadingthepage](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    *페이지를 다시 로드*

    오른쪽에 있는 링크는 이제 하지만 여전히 글머리 기호 목록 처럼 보입니다. 이제 글머리 기호를 제거 및 링크를 가로 방향으로 정렬 합니다.

    ![업데이트 페이지](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    *업데이트 페이지*
6. 검사 모드를 사용 하 여 중 하나를 선택는 **&lt;li&gt;** 포함 된 항목의 &quot;등록&quot; 및 &quot;로그인&quot; 링크 합니다. 클릭는  **&lt;섹션&gt; #login** 항목의 액세스 **Styles.css** 코드입니다.

    ![스타일 찾기](using-page-inspector-in-visual-studio-2012/_static/image42.png "스타일 찾기")

    *스타일 찾기*
7. **Style.css**에 대 한 코드를 주석 처리 제거 **#login li** 항목입니다. 추가 하는 스타일 글머리 기호 숨기고 항목 가로로 표시 됩니다.

    ![로그인 링크 스타일 재설정](using-page-inspector-in-visual-studio-2012/_static/image43.png "스타일의 로그인 링크를 재설정")

    *로그인 링크 스타일 재설정*
8. 저장 **Style.css** 파일 및 페이지를 다시 로드 하는 주소 아래에 있는 표시줄에 한 번 클릭 합니다. 링크는 올바르게 표시 되는지 확인 합니다.

    ![오른쪽으로 정렬 하는 링크](using-page-inspector-in-visual-studio-2012/_static/image44.png "오른쪽으로 정렬 하는 링크")

    *오른쪽으로 정렬 하는 링크*
9. 마지막으로, 머리글 제목을 변경 합니다. 에 대 한 검색 하는 대신는 '**사용자 로고는 여기 '** 의 모든 파일을 텍스트를 클릭 하 고 생성 하는 소스 코드를 검사 모드를 사용 합니다.

    ![사이트 제목 찾기](using-page-inspector-in-visual-studio-2012/_static/image45.png "사이트 제목 찾기")

    *사이트 제목 찾기*
10. 에 이제 **Site.Master**, 대체는 '**사용자 로고는 여기**'텍스트와 '**사진 갤러리**'. 저장 하 고 페이지 검사기 브라우저를 업데이트 합니다.

    ![업데이트 사진 갤러리 페이지](using-page-inspector-in-visual-studio-2012/_static/image46.png "업데이트 사진 갤러리 페이지")

    *업데이트 사진 갤러리 페이지*
11. 마지막으로 키를 눌러 **F5** 체크 아웃 변경 내용이 예상 대로 작동 하는 모든 앱을 실행 하려면.

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩을 완료 하면 다시 작성 하 여 브라우저에서 웹 사이트를 실행할 필요 없이 웹 응용 프로그램을 미리 보려면 페이지 검사기를 사용 하는 방법을 배운 있습니다. 신속 하 게 찾아서 소스 코드에 렌더링된 된 출력에서 직접 액세스 하 여 버그를 수정 하는 방법을 배운 합니다.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 a: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여 **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)**. 다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.

1. 로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다. 또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Windows Azure SDK와</em>&quot;합니다.
2. 클릭 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.

    ![Visual Studio Express 설치](using-page-inspector-in-visual-studio-2012/_static/image47.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건 동의](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **마침**합니다.

    ![설치 완료](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.

    ![웹 타일에 대 한 VS Express](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    *웹 타일에 대 한 VS Express*
