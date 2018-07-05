---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: ASP.NET 및 웹 개발에 Visual Studio 2012의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: 새 버전의 Visual Studio 웹 기술을 사용할 경우 환경 및 성능이 향상에 집중 하는 향상 된 여러 가지를 소개 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d037ccb62693a07ab8e2640b2d930ec7093b35da
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37375887"
---
<a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a>ASP.NET 및 웹 개발에 Visual Studio 2012의 새로운 기능
====================
[웹 캠프 팀](https://twitter.com/webcamps)

> 새 버전의 Visual Studio에서는 다양 한 웹 기술을 사용할 경우 환경 및 성능이 향상에 집중 하는 향상 된 기능을 소개 합니다. CSS, JavaScript 및 HTML에 대 한 visual Studio 편집기 가장 많이 코드 지원을 IntelliSense에서 자동 들여쓰기 등의 대부분을 포함 하도록 완전히 새롭게 수정 되었습니다 했습니다. 성능에 대 한 묶음 및 축소는 이제 처럼 통합 기본 제공 기능 페이지를 손쉽게 줄일을 로드 합니다.
> 
> Visual Studio를 사용 하는 최신 웹 사이트를 사용 하 여 사용할 수 있습니다. 브라우저 간 CSS3 조각 사이트도 활용 하는 새로운 HTML5 요소 및 기능 하는 동안 클라이언트 플랫폼에 관계 없이 작동 하는지 확인 해야 사용할 수 있습니다.
> 
> 작성 및 JavaScript 코드 프로 파일링이 Visual Studio 버전을 사용 하 여 쉽게 이어야 합니다. IntelliSense 목록 XML 설명서 및 탐색 기능 통합된 JavaScript 코드에 대해 제공 됩니다. 여러분의 손끝 이제 JavaScript 카탈로그입니다. 또한 스크립트 ECMAScript5 준수 하는지 확인할 수 있으며 초기 단계에서 구문 오류를 검색할 수 있습니다.
> 
> 마지막으로, 기본 제공 묶음 및 축소가 Visual Studio 버전을 구현합니다. 스크립트 파일 및 스타일 시트 압축 및 압축 사이트를 더 빠르게 수행 되도록 합니다.
> 
> 이 실습을 이용 하면 향상 된 기능 및 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 내용을 적용 하 여 이전에 설명 된 새 기능을 통해 안내 합니다.
> 
> 웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)합니다.


<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 배웁니다 방법:

- CSS 편집기에서 새로운 기능과 향상 된 기능 사용
- HTML 편집기에서 새로운 기능과 향상 된 기능 사용
- JavaScript 편집기의 새로운 기능과 향상 된 기능 사용
- 구성 및 묶음 및 축소를 사용 합니다.

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽을 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).
- [Windows PowerShell](https://support.microsoft.com/kb/968930/) (스크립트에 대 한 설치-Windows 8 및 Windows Server 2008 R2에 이미 설치)
- [Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) -또는 HTML5 호환 브라우저

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습에 포함 됩니다.

1. [연습 1:의 새로운 CSS 편집기](#Exercise1)
2. [연습 2: 새로운 HTML 편집기에서](#Exercise2)
3. [연습 3:의 새로운 JavaScript 편집기](#Exercise3)
4. [실습 4: 묶음 및 축소](#Exercise4)

이 랩을 완료 하기 위한 예상 시간: **60 분**합니다.

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a>연습 1:의 새로운 CSS 편집기

웹 개발자는 다양 한 CSS 편집 관련 문제를 사용 하 여 잘 알고 있어야 합니다. CSS 스타일을 지정 하는 가장 큰 문제 중 하나에 브라우저 간 호환성입니다. 또한, 사이트에 스타일을 적용 한 후 표시 다르게 보입니다 다른 브라우저 또는 장치에서 여는 경우에 이러한 상황이 자주 발생 합니다. 따라서, 마지막으로 할 때 하나의 브라우저에서 작동 하는지, 났다고 다른에서 실현 하는 데 해당 시각적 문제 해결 하기 위해 상당한 시간이 찾아오는 합니다.

이제 visual Studio 개발자 액세스, 작업 및 CSS 스타일 시트를 효과적으로 구성할 수 있도록 기능을 포함 합니다. 이 연습에서는 전체 효과적인 조직과 edition의 새로운 기능 및 브라우저 간 호환성에 대 한 CSS3 코드 조각은 충족 됩니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a>작업 1-새 편집기 기능

이 태스크에서는 CSS 편집기의 새로운 기능 알게 됩니다. 이 새 편집기를 사용 하면 새 스마트 들여쓰기, 향상 된 코드 주석 및 향상 된 IntelliSense 목록 활용 하 여 생산성을 높일 수 있습니다.

1. 시작 **Visual Studio** 연 합니다 **WhatsNewASPNET.sln** 솔루션을 **Source\WhatsNewASPNET** 이 랩의 폴더입니다.
2. 솔루션 탐색기에서 엽니다는 **Site.css** 아래에 있는 파일을 **스타일** 폴더입니다. 있는지 확인 합니다 **텍스트 편집기** 도구 모음의 표시 됩니다. 이렇게 하려면 선택 합니다 **보기** | **도구 모음** 메뉴 옵션을 확인 합니다 **텍스트 편집기** 옵션. 이 새 버전 이후에 알 수 있습니다 합니다 **주석** 단추 (![주석 단추](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png) ) 및 **주석** 단추 (![주석 처리 제거 단추](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png)) CSS 편집기의 활성화 됩니다.

    ![편집기 및 CSS 도구를 사용 하도록 설정](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "편집기 및 CSS 도구를 사용 하도록 설정")

    *편집기 및 CSS 도구를 사용 하도록 설정*
3. 코드를 스크롤하여 모든 CSS 클래스 정의 선택 합니다. 클릭 합니다 **주석** (![주석 단추](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png) ) 단추를 선택한 줄 주석 처리 합니다. 클릭 합니다 **주석** (![주석 처리 제거 단추](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png) ) 변경 내용을 취소 하는 단추입니다.
4. 클릭 합니다 **축소** (![축소](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png) ) 및 **확장** (![확장](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png) ) 텍스트의 왼쪽된 여백에 있는 단추입니다. 알림 이제 더 자세히 보려면을 사용 하지 않는 스타일을 숨길 수 있습니다.

    ![CSS 클래스를 축소](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "축소 CSS 클래스")

    *CSS 클래스를 축소합니다.*
5. 스마트 들여쓰기 기능이 활성화 되어 있는지 확인 합니다. 선택 된 **도구** | **옵션** 메뉴 옵션을 선택 합니다 **텍스트 편집기** | **CSS**  |  **서식** 화면의 왼쪽된 창에서 페이지입니다. 확인 합니다 **계층적 들여쓰기** 옵션입니다.

    ![계층적 들여쓰기를 사용 하도록 설정](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "계층적 들여쓰기를 사용 하도록 설정")

    *계층적 들여쓰기를 사용 하도록 설정*
6. 기본 클래스 정의 (.main) 찾은 div 요소에 스타일을 추가 합니다. 코드를 한 눈에 부모 클래스를 찾을 수 있도록 사용자가 자동으로 맞춥니다 확인할 수 있습니다.

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    ![CSS에서 계층적 맞춤](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "CSS에서 계층적 맞춤")

    *CSS에서 계층적 맞춤*
7. 내 **.main div** 클래스를 끝에 커서를 찾아 **테두리: 0px;** 키를 누릅니다 **Enter** IntelliSense 목록에 표시할 합니다. 입력을 시작 **위쪽** 입력할 때 목록을 필터링 하는 방법을 확인 합니다. 목록에 포함 된 요소가 표시 됩니다 **위쪽** 단어의 모든 부분에서 (Visual Studio의 이전 버전에서는 목록 항목에 의해 필터링 되는 *시작* 용어를 사용 하 여).

    ![CSS IntelliSense 개선 사항](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "CSS IntelliSense 개선 사항")

    *CSS IntelliSense 개선 사항*

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a>작업 2-색 선택

이 태스크에서는 새 CSS 색 선택을 Visual Studio IntelliSense 통합에서 검색 합니다.

1. **Site.css를** 헤더 클래스 정의 (.header)를 찾아 옆에 커서를 놓고 **배경색** 특성 간에 &quot;:&quot; 및 &quot; # &quot; 코드의 해당 줄의 문자 **합니다.**

    ![커서를 찾는](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "커서 찾기")

    *커서 찾기*
2. 삭제 합니다 **콜론** (:) 및 색상 선택기를 표시 하도록 다시 작성 합니다. 첫 번째 색 표시 됩니다는 사이트의 빈도가 가장 높은 색을 확인 합니다. 흰색을 클릭 하면 해당 HTML 색 코드를 (#fff) 스타일 시트에서 현재 색 코드를 바뀝니다.

    ![색 선택기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "색 선택")

    *색 선택*
3. 키를 눌러 합니다 **확장** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png) ) 색 그라데이션을 표시 하 고 다음 그라데이션 색을 선택할 커서를 끌어 색 선택 단추입니다. 그 후를 클릭 합니다 **스 포 이트** 단추 및 화면에서 색을 선택 합니다. 배경색 값 변경 커서를 이동 하는 동안 동적으로 확인할 수 있습니다.

    ![색 선택기 그라데이션](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "색 선택기 그라데이션")

    *색 선택기 그라데이션*
4. 에 **불투명도** 슬라이더 불투명도 줄이기 위해 막대의 가운데에 선택기를 이동 합니다. 배경색 값 RGBA로 해당 크기를 이제 변경 되는지 확인 합니다.

    ![색 선택 불투명도](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "불투명도 색 선택")

    *색 선택 불투명도*

    > [!NOTE]
    > CSS3의 RGBA (빨강, 녹색, 파란색, 알파) 색 정의 사용 하면 단일 항목에 대 한 색 불투명도 값을 정의할 수 있습니다. 와 달리 **불투명도-** 유사한 CSS 특성 **-** RGBA 색도 최신 브라우저와 호환 됩니다.

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a>작업 3-CSS 호환 코드 조각

이 작업에서는 웹 사이트의 일부 기능을 구현 하기 위해 브라우저 간 호환 CSS3 코드 조각을 사용 하는 방법을 배웁니다.

1. 에 **Site.css** 파일을 찾습니다는 **헤더** CSS 클래스 정의 (.header) 및 아래에 커서를 배치 합니다 **/ \*테두리 반지름\* /** 새 코드 조각을 추가 하는 자리 표시자입니다. 키를 눌러 **Enter** 유형과 IntelliSense 목록에 표시할 **radius** 목록을 필터링 합니다. 선택 합니다 **테두리 반지름** 를 두 번 클릭을 사용 하 여 목록에서 옵션 및 키를 누릅니다 합니다 **탭** 조각을 삽입 하는 키입니다. 그런 다음 픽셀 및 키를 눌러 radius 크기를 입력 **Enter**합니다. 예를 들어 입력 **15px**합니다.

    코드 조각을 추가 CSS3 특성 둥근된 테두리 Mozilla 및 WebKit 기반 브라우저를 비롯 한 대부분의 HTML5 준수 브라우저에서 렌더링 됩니다.

    ![테두리 반지름 조각을 사용 하 여](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "테두리 반지름 조각을 사용 하 여")

    *테두리 반지름 조각을 사용 하 여*
2. 같은 적용 **테두리** 조각을 페이지 스타일 (.page).

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. 키를 눌러 **F5** 솔루션을 실행 합니다. 각 페이지 이제 둥근 테두리를 확인 합니다.

    ![모서리가 둥근](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "모서리가 둥근 모양")

    *둥근된 모서리*
4. 브라우저를 닫고 Visual Studio로 돌아갑니다.
5. 열기는 **Custom.css** 아래에 있는 파일을 **스타일** 폴더 내부에 커서를 놓습니다 **div.images ul li img** 클래스 정의 합니다.
6. Enter 키를 눌러 IntelliSense 목록에 표시 유형 **상자 섀도** 키를 누릅니다 합니다 **탭** 클래스 정의 내에서 기본 섀도 코드 조각을 삽입 하려면 두 번 키. 섀도 값을 설정 **10px 10px 5px #888**합니다. 그런 다음 입력 **테두리 반지름** 및 코드 조각을 삽입 합니다. 형식 **15px** 누릅니다 radius 크기를 설정 하려면 **ENTER**합니다.

    ![그림자가 적용 된 모서리가 둥근](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "그림자가 적용 된 모서리가 둥근")

    *그림자를 사용 하 여 둥근된 모서리*

    > [!NOTE]
    > 이 시점에서 섀도 특성 (Chrome, Safari, Konkeror) Webkit 브라우저 (설정, webkit, o) Mozilla를 지원 하기 위해 해당 접두사와 삽입 됩니다.
7. 새 클래스를 만듭니다 **div.images ul li img:hover** 아래 합니다 **div.images ul li img** 클래스 정의 및 대괄호 안에 커서를 놓고 **합니다.**

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. 형식 **변환** 누릅니다 합니다 **탭** 변환 코드 조각을 삽입 하려면 두 번 키입니다. 그런 다음 입력 **rotate(-15deg)** 이미지는 가져갈 때 회전 각도 값을 변경 합니다.

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. 키를 눌러 **F5** 솔루션을 실행 하 여 CSS3 페이지로 이동 합니다. 이미지 모서리가 둥글게 변합니다에 그림자를 상자 유의 하십시오. 이미지 위로 마우스를 이동 하 고 회전을 관찰 합니다.

    ![이미지를 회전 하는 코드 조각 변환](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "이미지 회전 변환 코드 조각")

    *이미지를 회전 하는 코드 조각 변환*

    > [!NOTE]
    > 그림자를 볼 수 없는 경우 Internet Explorer 10을 사용 하는 문서 모드는 IE10 표준으로 설정 되어 있는지 확인 합니다. 키를 눌러 **F12** Internet Explorer 개발자 도구를 열고 클릭 **문서 모드** IE10 표준으로 변경 하려면.

    ![에 대 한-us](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a>연습 2: 새로운 HTML 편집기에서

Visual Studio에는 향상 된 HTML 편집기. 이 버전의 향상 된 기능 중 일부에 HTML 문서, HTML5 조각, HTML 시작 및 끝 태그 일치 및 HTML 유효성 검사에서 스마트 들여쓰기 됩니다. 이 연습에서는 전체 웹 사이트 마크업에서 작업할 때 이러한 변경 내용을 사용자 수준은 개선 하는 방법을 볼 수 있습니다.

CSS 편집기와 같은 HTML 편집기도 향상 되었습니다. 이러한 향상 된이 기능 대부분은 웹 개발자의 작업을 쉽게 작은 이미지용입니다. HTML5, 스마트 들여쓰기를 편집 하 고 HTML 문서 DOCTYPE을 대상으로 하는 유효성 검사는 이러한 향상 된이 기능 중 일부 경우에 일치 하는 시작 및 끝 태그에 대 한 더 많은 코드 조각을 등입니다.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a>작업 1-향상 된 DOCTYPE 유효성 검사

마스터 페이지는 정의 될 수 있지만 이제 HTML 편집기는 페이지의 DOCTYPE에 검사할 수 있습니다. 페이지의 DOCTYPE에 따라 HTML 편집기에서는 올바른 규칙 집합과 유효성을 검사 및 DOCTYPE 요소를 고려 IntelliSense 목록을 필터링 하는 합니다.

이 태스크에서는 페이지의 HTML 편집기 동작을 적절 하 게 변경 하는 방법을 보려면 DOCTYPE 변경 합니다.

1. 열려 있지 않으면 시작 **Visual Studio** 연 합니다 **WhatsNewASPNET.sln** 솔루션을 **Source\WhatsNewASPNET** 이 랩의 폴더입니다.
2. 엽니다는 **Site.Master** 페이지입니다.
3. 유효성 검사 도구 모음에 대 한 대상 스키마를 확인 합니다. HTML 편집기 (유효성 검사, IntelliSense 등)을 작동 하는 방식을 선택 Doctype에 맞게 올바르게 변경 됩니다.

    ![Doctype을 사용 하 여 HTML 소스 편집 도구 모음의](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "HTML 소스 편집 도구 모음에서 사용 하 여 Doctype")

    *Doctype을 사용 하 여 HTML 소스 편집 도구 모음의*
4. HTML 4.01에 대상 스키마를 변경 합니다.

    ![HTML 소스 편집 도구 모음의 Doctype 변경](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "HTML 소스 편집 도구 모음의 Doctype 변경")

    *HTML 소스 편집 도구 모음의 Doctype 변경*
5. 커서를 놓고 합니다 **본문** 요소와 HTML5 요소의 이름을 입력 하기 시작 (예를 들어 **비디오**). 요소 IntelliSense 목록에서 사용할 수 있는 인지 확인 합니다.

    ![HTML5 요소 나타나지](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "나열 되지 않은 HTML5 요소")

    *나열 되지 않은 HTML5 요소*
6. DOCTYPE을 선택 합니다. 유효성 검사 도구 모음에 대 한 대상 스키마의 변경 내용을 취소 합니다: 드롭다운 목록에서 XHTML5 합니다.

    ![Doctype을 사용 하 여 HTML 소스 편집 도구 모음의](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "HTML 소스 편집 도구 모음에서 사용 하 여 Doctype")

    *HTML 소스 편집 도구 모음의 Doctype을 다시 설정*
7. 커서를 놓고 합니다 **본문** 요소 및 HTML5 요소를 다시 입력 하기 시작 (예를 들어 같은 **비디오**). HTML5 요소는 이제 IntelliSense 목록에 알 수 있습니다.

    ![나열 되는 HTML5 요소](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "나열 되는 HTML5 요소")

    *나열 되는 HTML5 요소*

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a>작업 2-시작/끝 태그를 자동 업데이트

이제 visual Studio를 열거나 닫는 태그가 서로 일치 하도록 편집 하는 요소의 HTML을 업데이트 합니다. 이 새로운 기능은 HTML 태그를 편집할 때 생산성을 향상 됩니다.

1. 에 **Default.aspx** 페이지에서 추가 **H3** 제목 (예를 들어, Visual Studio 2012 Rocks!)를 사용 하 여 요소입니다.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. 변경 된 **H3** 태그 유형과 **H2** 또는 **H1 합니다.**

    끝 태그가 자동으로 업데이트 하도록 확인 합니다. 시작 태그를 적절 하 게 업데이트 너무 보려는 끝 태그를 수정할 수도 있습니다.

    ![끝 태그의 자동 업데이트](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "끝 태그의 자동 업데이트")

    *끝 태그의 자동 업데이트*

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a>작업 3-새 HTML5 코드 조각

Visual Studio에는 이제 여러 HTML5 코드 조각을 포함합니다. 이 태스크에서는 이러한 조각 중 일부를 사용 합니다.

1. 라는 새 폴더 추가 **오디오** 웹 사이트 폴더의 루트에 있습니다. Windows 탐색기를 열고 모든 오디오 파일을 복사 합니다 **오디오** 폴더를 **WhatsNewASPNET.sln** 솔루션입니다.
2. 에 **Default.aspx** 페이지에서 아래 Web11 Rocks 커서!! 헤더입니다. 형식 **오디오** TAB 키를 누릅니다.

    새 HTML 편집기에는 HTML5 콘텐츠에 대 한 코드 조각을 포함합니다. HTML5 조각 수 있도록 적절 한 문서 종류 정의 사용 해야 합니다.

    ![HTML5 코드 조각 삽입](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "HTML5 코드 조각 삽입")

    *HTML5 코드 조각 삽입*
3. 기존 오디오 파일을 가리키도록 오디오 소스를 업데이트 합니다.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > 오디오 파일을 솔루션에 추가 해야 합니다.
4. 키를 눌러 **F5** 사이트를 실행 하 여 오디오를 재생 합니다.

    ![실행 중인 오디오 컨트롤](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "실행 중인 오디오 컨트롤")

    *실행 중인 오디오 컨트롤*

    > [!NOTE]
    > 또한 비디오, 그림 등 Visual Studio에 포함 하는 자세한 코드 조각을 시도할 수 있습니다.
5. 이제 페이지의 일부에 컨트롤을 삽입 하려고 합니다. 예를 들어 삽입 하려고를 **GridView** 컨트롤을 입력 하는 대신  **&lt;눈금선에 맞춤,** 입력을 시작  **&lt;GV**합니다. IntelliSense 목록에 표시 하는 **asp: GridView** 제어 합니다.

    HTML 편집기에서 IntelliSense는 이제 부분 일치 하는 (검색 용어를 포함 하는 모든 요소) 뿐만 아니라 제목 대/소문자 구분 검색을 제공 합니다.

    ![IntelliSense 목록 사용 하 여 GridView 삽입](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "IntelliSense 목록 사용 하 여 GridView를 삽입 합니다.")

    *IntelliSense 목록 사용 하 여 GridView를 삽입합니다.*

    입력 하는 경우  **&lt;그리드** 용어와 일치 하는 모든 항목을 받을 수 있지만 Visual Studio가 제안 합니다 **gridview** 컨트롤:

    ![IntelliSense 목록 및 부분 일치를 사용 하 여 GridView 삽입](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "IntelliSense 목록 및 부분 일치를 사용 하 여 GridView를 삽입 합니다.")

    *IntelliSense 목록 및 부분 일치를 사용 하 여 GridView를 삽입합니다.*

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a>작업 4-HTML 편집기 스마트 태그

HTML 편집기에서 향상 된 또 다른는 스마트 태그 기능입니다. 스마트 태그를 사용 하면 쉽게 컨트롤 당 기준 일반 또는 반복 개발 작업을 수행할 수 있습니다. 이 기능을 사용할 수 있는 이미 HTML 디자이너, 있지만 HTML 편집기에 없습니다.

1. 오픈 **Site.Master** 찾아서 합니다 **asp: 메뉴** 요소입니다. 시작 태그에 알림-요소의 아래쪽에 작은 문자 모양을 클릭 하 여 스마트 작업 메뉴를 엽니다는 커서를 놓습니다. 메뉴 컨트롤에 관련 된 몇 가지 작업에 빠르게 액세스할 수 있는지 확인 합니다.

    ![메뉴 컨트롤에 대 한 작업을 스마트](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "스마트 메뉴 컨트롤에 대 한 작업")

    *메뉴 컨트롤에 대 한 스마트 작업*

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a>작업 5-스마트 들여쓰기

읽을 수 있는 코드를 유지 하는 중첩 된 요소를 들여쓰기는 HTML의 모범 사례 중 하나입니다. Visual Studio 2012의 편집기는 코드를 작성 하는 동안 자동으로 요소를 들여쓰기는 확인할 수 있습니다.

> [!NOTE]
> Visual Studio의 이전 버전에서는 스마트 들여쓰기 있던 HTML 편집기 아니라 XML 편집기에서.


1. 스마트 들여쓰기를 들여쓰기 구성 HTML 편집기에 설정 되어 있는지 확인 합니다. 이 위해 선택 된 **도구 | 옵션** 메뉴 옵션을 선택 하 고는 **텍스트 편집기 | HTML | 탭** 화면의 왼쪽된 창에서 페이지입니다. 스마트 들여쓰기 옵션을 선택 합니다.

    ![HTML 편집기 설정을](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML 편집기 설정")

    *HTML 편집기 설정*
2. 에 **Default.aspx** 페이지, 오디오 요소 아래에 있는 모든 콘텐츠를 제거 합니다.
3. 열기의 끝에 커서를 놓고 **오디오** 요소 및 적중 **ENTER**합니다.

    커서의 새 위치는 추가 들여쓰기 수준에 있는지 확인 합니다.

    ![HTML 편집기에서 들여쓰기를 스마트](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "스마트 들여쓰기 HTML 편집기에서")

    *HTML 편집기에서 스마트 들여쓰기*
4. 콘텐츠를 제거 하거나 닫을 있습니다를 사용 하 여 오디오 태그를 복원 **Default.aspx** 없이 변경 내용을 저장 합니다.

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a>태스크 6-사용자 정의 컨트롤로 추출

함수에 코드 부분을 추출 하는 등 Visual Studio에서 포함 된 리팩터링 도구는 쉽게 개선 하 고 기존 코드를 리팩터링 하는 훌륭한 기능입니다. ASP.NET 페이지에 대 한 대응 하는 사용자 정의 컨트롤의 HTML 코드가 추출 됩니다. 수동으로 수행 하는 여러 단계를 만들고 새 사용자 정의 컨트롤을 이동 코드 섹션 사용자 정의 컨트롤, 사용자 컨트롤에 대 한 태그 접두사를 등록 하 고, 마지막으로, 페이지에서 사용자 컨트롤을 인스턴스화한 같은 작업이 포함 됩니다. 이제 새 *사용자 정의 컨트롤로 추출* 도구를 자동으로 이러한 모든 단계를 수행 합니다.

이 태스크에서는 선택한 코드에서 새 사용자 정의 컨트롤을 생성 하려면 새 사용자 정의 컨트롤 상황에 맞는 작업 추출을 사용 합니다.

1. 에 **Default.aspx** 페이지를 선택 합니다 **H2** 및 **오디오** 요소입니다.
2. 마우스 오른쪽 단추로 클릭 하 고 선택 **사용자 정의 컨트롤로 추출**합니다.

    ![사용자 정의 컨트롤 메뉴 옵션에 압축을 풉니다](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "사용자 컨트롤 메뉴 옵션을 추출 합니다.")

    *사용자 정의 컨트롤 메뉴 옵션을 추출 합니다.*
3. 새 사용자 정의 컨트롤에 대 한 이름을 입력 합니다. 예를 들어 **Jukebox.ascx**를 클릭 하 고 **확인**합니다.

    ![추출 된 사용자 정의 컨트롤을 저장할](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "추출 된 사용자 정의 컨트롤을 저장 합니다.")

    *추출 된 사용자 정의 컨트롤을 저장합니다.*
4. 선택한 코드를 사용자 정의 컨트롤로 추출 된 새 사용자 정의 컨트롤의 인스턴스를 사용 하 여 대체 된 선택한 코드의 원래 위치에 유의 하십시오.

    ![페이지는 자동으로 새 사용자 컨트롤을 사용 하도록 업데이트](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "페이지 새 사용자 컨트롤을 사용 하도록 자동으로 업데이트")

    *페이지는 자동으로 새 사용자 컨트롤을 사용 하도록 업데이트*
5. 키를 눌러 **F5** 페이지를 실행 하 고 컨트롤 작동 하는지 확인 합니다.

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a>연습 3:의 새로운 JavaScript 편집기

작성 하거나 JavaScript 코드를 편집 아닙니다 쉽지만은 않은 작업 크기가 증가 하기 시작 하는 응용 프로그램 및 있다면 긴 파일을 사용 하 여 처리 하 고 수백 개의 함수가 그렇습니다. 스크립트 개발자는 일반적으로 코드 가독성을 유지 관리 하 고 파일 간에 이동 하려면 몇 가지 추가 작업을 수행 해야 합니다. 예: jQuery JavaScript 라이브러리를 포함 하는 것을 스크립트 탐색 코드 길이 때문에 자체 질문을 해 왔습니다.

Visual Studio JavaScript 편집기를 액세스할 수 있고 구성 코드 모드에 있도록 프라미스를 갱신 했습니다. C# 또는 VB 편집기에 이미 존재 하는 여러 Visual Studio 기능 이제 JavaScript 편집기에서 구현: 정의로 이동, 자동 들여쓰기, 설명서 및 작성 하는 경우 유효성 검사 합니다. 갱신 된 IntelliSense 목록을 사용 하 여 JavaScript 함수 카탈로그 신청 해야 합니다.

이 연습에서는 몇 가지 새로운 기능 및 JavaScript 편집기의 향상 된 기능 배웁니다. 샘플 파일 찾아보기 및 각 새 특성은 JavaScript 프로그래밍 보다 효율적인 Visual Studio 2012 내의 검색 합니다.

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a>작업 1-JavaScript 편집기의 새로운 기능

이 작업에 대 한 코드를 구성 하 고 더 나은 사용자 환경을에 집중 하는 새 JavaScript 편집기 기능을 소개 합니다.

1. 열려 있지 않으면 시작 **Visual Studio** 연 합니다 **WhatsNewASPNET.sln** 솔루션을 **Source\WhatsNewASPNET** 이 랩의 폴더입니다.
2. 키를 눌러 **F5** 응용 프로그램을 실행 하려면 다음 탐색 모음에서 JavaScript 링크를 클릭 합니다. 페이지를 새로 고칩니다 여러 시간 및 확인 하는 방법을 카운터가 증가 합니다.

    ![페이지 카운터](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "페이지 카운터")

    *페이지 카운터*
3. 브라우저를 닫고 Visual Studio로 다시 이동 합니다.
4. 엽니다는 **JavaScript.aspx** 찾아서 페이지는 **&lt;스크립트&gt;** 블록 (아래 참조).

    다음 코드는 HTML5 로컬 저장소를 사용 하 여 저장 된 *pageLoadCount* 현재 사용자가 페이지를 방문한 횟수를 저장 하는 변수입니다. 로컬 저장소는 HTML5 표준을 도입 하는 클라이언트 쪽 키-값 데이터베이스. 데이터는 사용자의 브라우저 내에서 로컬 컴퓨터에 저장 됩니다.

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > DOCTYPE은 다음 단계를 진행 하기 전에 XHTML5로 확인 합니다.
5. 코드를 편집 하 고 JavaScript 용 IntelliSense는 로컬 저장소 및 해당 내부 메서드 같은 HTML5 기능을 포함 합니다.

    ![JavaScript의 HTML5 JavaScript 기능](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "javascript에서 HTML5 JavaScript 기능")

    *JavaScript의 HTML5 JavaScript 기능*
6. 모든 여는 대괄호를 클릭 합니다. (**{**) 스크립팅 코드에서 대괄호를 강조 표시 됩니다.

    ![대괄호를 강조 표시 됩니다](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "대괄호는 강조 표시")

    *대괄호는 강조 표시*
7. 함수를 주석 처리 제거 **testAutoAlign()** (세 줄을 선택 하 고 사용할 수 있습니다 **CTRL** + **K**; **CTRL** + **U**) 함수 코드 내부에 커서를 찾습니다. 두 번째 줄을 추가 하려면 enter 키를 누릅니다. 이제 코드는 되었다는 **정렬** 하 고 **자동으로 들여쓰기 되며**합니다.

    ![JavaScript 코드는 자동 정렬](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript 코드는 자동 정렬")

    *JavaScript 코드는 자동 정렬*

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a>작업 2-JavaScript 유효성 검사

이 태스크에서는 ECMAScript5 표준에 대 한 새 JavaScript 유효성 검사에서 검색 합니다. 이 기능은 사이트 배포 하기 전에 스크립트 문제를 방지 하는 동안 호환 JavaScript 코드를 작성 하는 데 도움이 됩니다.

> [!NOTE]
> Visual Studio 2010 ECMAScript5 규정 준수를 제공 하는 Visual Studio 2012 ECMAStript3 규정 준수를 구현 합니다.


1. 오픈 **ECMA5script5.js** 아래에 **Scripts\custom** 프로젝트 폴더입니다. 이제 표준 ECMAScript5에 대 한 유효성 검사를 테스트 합니다.

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    체크 아웃할 수 있습니다는 &quot; **사용 하 여 엄격한** &quot; ECMAScript5 수 있도록 하는 파일의 첫 번째 줄 방향을 **strict 모드**합니다. 이 모드는 이전 버전에서 모호성을 명확히 하 고 개체 속성에 getter 및 setter, JSON 및 자세한 리플렉션 라이브러리 지원 같은 새로운 일부 기능을 추가 하는 언어의 하위 집합으로 구성 됩니다.
2. 엽니다는 **오류 목록** 열려 있지 않으면 (**보기** 메뉴 | **오류 목록**). 알림 합니다 **함수** 선언 밑줄이 표시 됩니다. 즉, ECMA5 표준 함수 언어 구조 내에서 중첩 될 수 없습니다. 오류에 아래 목록에는 경고 세부 정보 표시 됩니다.

    ![JavaScript 유효성 검사 오류 메시지](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript 유효성 검사 오류 메시지")

    *JavaScript 유효성 검사 오류 메시지*
3. 주석으로 처리 합니다 **&quot;사용 하 여 엄격한&quot;** 방향 및 오류, 사라집니다. 하지만 경고 상태로 유지 하는 합니다.
4. 파일의 마지막 줄에 쓰기와 같은 문자열일 **&quot;테스트&quot;** (인용 부호를 나타내는 문자열로 포함). IntelliSense 목록 표시 및 선택할 문자열 옆의 기간을 작성 합니다 **trim** 옵션입니다.

    ECMAScript5 표준에서 문자열 값 및 변수 수도 정의 trim, 대문자, 찾기 및 바꾸기와 같은 문자열 메서드.

    ![JavaScript IntelliSense 목록의](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "JavaScript IntelliSense 목록")

    *JavaScript IntelliSense 목록*

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a>작업 3-JavaScript에 대 한 XML 설명서

이 태스크에서는 javascript에서 XML 문서에 대 한 Visual Studio 기능을 살펴봅니다. 이제 JavaScript IntelliSense 목록에 표시 된 각 함수의 XML 문서를 볼 수 있습니다. 또한 JavaScript의 탐색 기능을 알게 됩니다.

1. 오픈 **XMLDoc.js** 파일에 있는 **스크립트/사용자 지정** 프로젝트 폴더입니다. 이 파일에 JavaScript 함수의 각 XML 문서를 포함합니다.

    ![Intellisense 통합 JavaScript XML 문서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "intellisense 통합 JavaScript XML 문서")

    *IntelliSense를 통합 하는 JavaScript XML 문서*
2. 아래 **추가할** 함수 **XMLDoc.js** 라는 새 함수를 만들고, 파일 **테스트**합니다.
3. 에 **테스트** 함수를 호출 합니다 **곱하기** 두 개의 매개 변수를 받는 함수입니다. 도구 설명 상자는 표시를 확인 합니다 **곱하기** 함수 설명서.

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    ![JavaScript 함수에 대 한 XML 설명서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "JavaScript 함수에 대 한 XML 설명서")

    *JavaScript 함수에 대 한 XML 설명서*
4. 입력 하 고 함수 호출 문 완료를 *점* 반환된 된 값에서 IntelliSense 목록을 엽니다. Visual Studio를 감지 하는 **반환** 설명서의 숫자 값을 처리 하는 방법에 대 한 값입니다.

    ![반환 형식에 대 한 XML 설명서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "반환 형식에 대 한 XML 설명서")

    *반환 형식에 대 한 XML 설명서*
5. 이제 함수를 추가에 대 한 호출을 삽입 합니다. JavaScript 편집기는 이제 함수 오버 로드는 알 수 있습니다. 함수 이름, 작성 하는 경우 설명서에 지정 된 사용 가능한 오버 로드 중 하나를 선택할 수 있습니다.

    ![오버 로드에 대 한 XML 설명서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "오버 로드에 대 한 XML 설명서")

    *오버 로드에 대 한 XML 설명서*
6. 열기 **GotoDefinition.js** 찾아서 파일을 **$().html()** 함수 호출 합니다. 커서를 찾는 **html**합니다.
7. 키를 눌러 **F12** 정의로 이동 합니다. 알림 이제 액세스 하 고 사용 하지 않고 JavaScript 코드를 찾아볼 수 있습니다 합니다 **찾을** 도구입니다.
8. 코드 파일의 맨 아래에 있는 시그니처 블록 전에 jQuery 명령에 커서를 찾습니다. 키를 눌러 **F12**합니다. JQuery 라이브러리 파일을 이동 합니다. 탐색할 수 있습니다 사용 하 여 jQuery 파일을 확인할 수 있습니다 **F12**합니다.

    ![JQuery 정의로 이동](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "jQuery 정의로 이동")

    *JQuery 정의로 이동*

> [!NOTE]
> 파일을 저장 하기 전에 GotoDefinition.js에 구문 오류가 있는지 확인 합니다.


<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a>실습 4: 묶음 및 축소

몇 번 수행 하 여 웹 사이트 파일을 포함 둘 이상의 JavaScript 또는 CSS? 묶음 및 축소 파일 크기를 줄이고 더 빠르게 수행 하는 사이트를 확인 하는 데는 도움이 매우 일반적인 시나리오입니다. ASP.NET 4.5의 새로운 번들 기능 CSS 또는 JS 파일 집합을 단일 요소를 압축 하 고 (즉, 필요 하지 않습니다 공백 제거, 메모 제거, 식별자를 줄이는) 콘텐츠를 축소 하 여 해당 크기를 줄입니다.

프로세스에서 사용자 에이전트 (예: IE, Mozilla, 등)를 식별 하 고 따라서 (예를 들어 제거 보았던 Mozilla 특정 사용자 브라우저를 대상으로 하 여 압축을 향상 시킬 수 있도록 묶음 및 축소 ASP.NET 4.5의 런타임에 수행 됩니다. 요청 가져온 경우 IE에서).

이 연습에서는 ASP.NET 4.5의 다양 한 유형의 묶음 및 축소를 사용 하는 방법에 배웁니다.

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a>작업 1-의 번들을 설치 하 고 NuGet에서 패키지를 축소

1. 열려 있지 않으면 시작 **Visual Studio** 연 합니다 **WhatsNewASPNET.sln** 솔루션을 **Source\WhatsNewASPNET** 이 랩의 폴더입니다.
2. NuGet 패키지 관리자 콘솔을 엽니다. 이렇게 하려면 메뉴를 사용 하 여 **뷰** | **기타 Windows** | **패키지 관리자 콘솔**합니다.

    ![패키지 관리자 file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole 열기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "패키지 관리자 콘솔 열기")

    *패키지 관리자 콘솔 열기*
3. 에 **패키지 관리자 콘솔** 형식 **Install-package Microsoft.Web.Optimization** 누릅니다 **ENTER**합니다.

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a>작업 2-기본 번들

묶음 및 축소를 사용 하는 가장 간단한 방법은 기본 번들을 사용 하도록 설정 됩니다. 이 메서드가 묶이고 버전 폴더의 CSS 및 JS 파일을 참조할 수 있도록 규칙을 사용 합니다.

이 작업을 사용 하도록 설정 묶이고 CSS 및 JS 파일을 참조 하 고 결과 출력을 확인 하는 방법을 배웁니다.

1. 열려 있지 않으면 시작 **Visual Studio** 연 합니다 **WhatsNewASPNET.sln** 솔루션을 **Source\WhatsNewASPNET** 이 랩의 폴더입니다.
2. 에 **솔루션 탐색기**를 확장 합니다 **스타일**, **Scripts\custom** 및 **Scripts\bundle** 폴더.

    응용 프로그램이 둘 이상의 CSS 및 JS 파일을 사용 하 고 있음을 알 수 있습니다.

    ![응용 프로그램의 여러 스타일 시트 및 JavaScript 파일과](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "응용 프로그램의 여러 스타일 시트 및 JavaScript 파일")

    *응용 프로그램의 여러 스타일 시트 및 JavaScript 파일*
3. 엽니다는 **Global.asax.cs** 파일입니다.

    새 **Microsoft.Web.Optimization** 네임 스페이스는 파일의 시작 부분에서 주석 처리 합니다. 사용 하 여 주석 처리 제거 지시문 묶음 및 축소 기능을 포함 하도록 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. 찾을 합니다 **응용 프로그램\_시작** 메서드.

    이 방법에서는 아래 코드 조각에 표시 된 대로 EnableDefaultBundles 호출을 주석 처리 제거 합니다. 이 사용 하면 해당 폴더의 경로 사용 하 여 폴더의 CSS 파일의 번들된 컬렉션을 참조와 &quot;CSS&quot; 또는 &quot;JS&quot; 접미사.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. 엽니다는 **Optimization.aspx** 파일과 콘텐츠 컨트롤을 찾으십시오 **HeadContent**합니다.

    CSS 파일 및 단일 참조 태그가 JS 파일을 확인 합니다.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > 이 코드는 데모 목적입니다. 이상적으로 Site.Master 파일에 번들을 참조 합니다. 이 샘플 코드를 찾을 수 있습니다는 번들된 된 파일의 일부도 참조 하는 Site.Master 파일에 의해이 마지막 참조를 중복 수행 합니다.
6. 링크의 번들 규칙 사용 하 고 있는지 확인 합니다 **href** 스타일 및 Scripts\custom에서 모든 CSS 또는 JS 파일을 가져올 특성 폴더 각각.

    경로 사용할 수 있습니다 **스크립트/사용자 지정/JS** 아래와 같이 번들 내의 모든 JS 파일을 축소 하는 **스크립트/사용자 지정** 폴더입니다. 이것이 기본 번들을 사용 하 여 기본 동작입니다.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. 엽니다는 **Styles\Site.css** 파일입니다.

    원래 CSS 파일 들여쓴된 코드, 공백 및 파일을 확대 하는 주석이 포함 되어 있는지 확인 합니다. (또한 JavaScript 파일에 공백이 및 주석).

    ![Scripts 폴더에서 파일을 원래 CSS 중 하나가](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "Scripts 폴더에서 파일을 원래 CSS 중")

    *스크립트 폴더에 원래 CSS 파일 중 하나*
8. 키를 눌러 **F5** 응용 프로그램을 실행 하 고 이동 하 여 **최적화** 페이지입니다.
9. 클릭 합니다 **CSS 번들** 링크를 다운로드 하 여 파일을 엽니다.

    파일을 체크 아웃 된 번들입니다. 표시 됩니다는 공백, 주석 및 들여쓰기 문자 제거 되었거나, 더 작은 파일을 생성 합니다.

    ![CSS 파일을 번들](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "CSS 번들 파일")

    *번들된 CSS 파일*
10. 이제 클릭 합니다 **JS 번들** 링크를 제공 하는 JavaScript 파일을 엽니다. 탐색기 경고를 안전 하 게 무시할 수 있습니다. JavaScript 파일을 확인 합니다 **사용자 지정** 폴더는 또한 번들 및 축소 합니다.

    ![JavaScript 파일을 번들](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "번들 JavaScript 파일")

    *번들된 JavaScript 파일*

    CSS 또는 JS 파일에 대 한 압축을 사용 하도록 설정 된 이전 ASP.NET 버전에서 훨씬 더 복잡 합니다. 이제 앞에서 설명한 것 처럼 하면 한 줄을 추가 합니다 *Global.asax* 묶음을 사용 하도록 설정 하려면 파일을 다음 사이트에서 번들된 된 파일을 참조 합니다.

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a>작업 3-정적 번들

정적 번들 접근 방식은 사용 하면 파일을 번들, 참조 및 사용 되는 축소 메서드 집합을 사용자 지정할 수 있습니다.

이 태스크에서는 번들 및 축소 하는 파일의 특정 집합을 정의 하는 정적 번들을 구성 합니다.

1. 브라우저를 닫습니다.
2. 열기는 **Global.asax.cs** 찾아서 파일을 **응용 프로그램\_시작** 메서드.
3. 아래 코드와 같이 정적 번들 코드 주석 처리를 제거 합니다.

    사용 하 여 참조 되는 정적 번들을 정의 하는 합니다 &quot; **~/StaticBundle** &quot; 가상 경로 및 사용 하 여 **JsMinify** 사용 하 여 지정된 된 모든 파일의 축소에 대 한 합니다 **AddFile** 메서드. 마지막으로 정적 번들을 추가 하는 합니다 **BundleTable** 사용 합니다.

    파일; 같은 위치에 있지 않은 알 수 있습니다. 기본 번들을 통해 또 다른 이점은입니다.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. 엽니다는 **Optimization.aspx** 파일입니다.

    에 대 한 링크 **정적 JS 번들** Global.asax.cs 파일에서 정적 번들을 구성할 때 사용자가 선언한 경로 사용 하는: **/StaticBundle**합니다.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. 키를 눌러 **F5** 응용 프로그램을 실행 한 다음 이동 하 여 **최적화** 페이지입니다.
6. 클릭 합니다 **정적 JS 번들** 링크 파일을 엽니다.

    하는 축소 된 번들 JavaScript 파일은 경로 아래에 있는 정적 번들 파일에 구성 된 모든 JavaScript 파일에 대 한 출력 &quot;/StaticBundle&quot;합니다.

    ![정적 JavaScript 파일 번들](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "정적 JavaScript 파일 번들")

    *정적 JavaScript 파일에 번들*
7. 브라우저를 닫고 Visual Studio로 돌아갑니다.

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a>작업 4-동적 폴더 번들

이 태스크에서는 동적 폴더 번들을 구성 하는 방법에 배웁니다. 동적 묶음의 JavaScript로 컴파일되는 언어에서 다른 파일 뿐만 아니라 정적 JavaScript를 포함 하 고 번들로 실행 되기 전에 일부 처리 필요로 하므로, 수 있는 경우

이 예에서 사용 하는 방법을 배우게 됩니다 합니다 **DynamicFolderBundle** CofeeScript로 작성 된 파일에 대 한 동적 번들을 만들지는 클래스입니다. CofeeScript은 프로그래밍 언어 JavaScript로 컴파일되는 JavaScript 코드를 작성, JavaScript의 간 결함 및 가독성 향상에 대 한 간단한 구문을 제공 합니다.

1. 열기는 **Global.asax.cs** 찾아서 파일을 **응용 프로그램\_시작** 메서드.
2. 아래 코드 에서처럼 동적 번들 코드 주석 처리를 제거 합니다.

    사용 하는 동적 폴더 번들을 정의 하는 합니다 **CoffeeMinify** 사용 하 여 파일에만 적용 되는 사용자 지정 축소 프로세서는 &quot; **.coffee** &quot; 확장 ( CoffeeScript 파일)입니다. 표시 폴더 내의 같은 번들로 파일을 선택 하는 검색 패턴을 사용할 수 있는 '\*.coffee'.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. NuGet 패키지 관리자 콘솔을 엽니다. 이렇게 하려면 메뉴를 사용 하 여 **뷰** | **기타 Windows** | **패키지 관리자 콘솔**합니다.
4. 에 **패키지 관리자 콘솔** 형식 **Install-package CoffeeSharp** 누릅니다 **ENTER**합니다.
5. 클릭 합니다 **모든 파일 표시** 단추를 **솔루션 탐색기** 창

    ![모든 파일을 보여 주는](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "모든 파일 표시")

    *모든 파일 표시*
6. 마우스 오른쪽 단추로 클릭 합니다 **CoffeeMinify.cs** 파일을 **솔루션 탐색기** 선택한 **프로젝트에 포함**

    ![프로젝트에 CoffeeMinify.cs 파일 포함](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "CoffeeMinify.cs 파일 프로젝트에 포함")

    *프로젝트에서 CoffeeMinify.cs 파일을 포함 합니다.*
7. 엽니다는 **CoffeeMinify.cs** 파일입니다.

    이 클래스는 CoffeeScript 코드 컴파일에서 결과 JavaScript 출력을 축소 하려면 JsMinify에서 상속 됩니다. CoffeeScript 생성 하도록 컴파일러에 JavaScript 코드를 먼저 호출 하 고에 전송할 JsMinify.Process 방법 코드도 축소 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. 열기는 **Script1.coffee** 및 **Script2.coffee** 에서 파일을 **스크립트/번들** 폴더입니다.

    이러한 파일 CoffeeMinify 클래스와 함께 번들로 수행 하는 동안 컴파일할 CoffeScript 코드가 포함 됩니다.

    단순성을 위해 제공 하는 CoffeeScript 파일 CoffeeScript 샘플 코드만 포함 합니다. 주석을은 JsMinify 프로세스에서 제외 됩니다.

    ![CoffeeScript 파일](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript 파일")

    *CoffeeScript 파일*

    > [!NOTE]
    > [CofeeScript](https://github.com/jashkenas/coffeescript/) JavaScript 코드를 작성, JavaScript의 간 결함 및 가독성을 향상 시킬 뿐만 아니라 배열 이해 및 패턴 일치와 같은 다른 기능을 추가 하는 것에 대 한 간단한 구문을 제공 합니다.
9. 엽니다는 **Optimization.aspx** 파일을 번들 파일에 대 한 링크를 찾습니다.

    에 대 한 링크 **동적 JS 번들** 참조를 **스크립트/번들** 를 사용 하 여 폴더를 **커피/** 접미사 동적 폴더 번들에 대 한 구성.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. 키를 눌러 **F5** 응용 프로그램을 실행 한 다음 이동 하 여 **최적화** 페이지입니다.
11. 클릭 합니다 **동적 JS 번들** 링크 생성 된 파일을 엽니다.

    이 번들에 포함 된 콘텐츠 포함 되었다는 **.coffee** 파일입니다. CoffeeScript 코드가 JavaScript로 컴파일된을 주석 처리 된 줄이 제거 되었습니다 볼 수 있습니다.

    ![동적 JS 파일을 번들](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "동적 JS 파일 번들")

    *동적 JS 파일을 번들*

> [!NOTE]
> 또한 다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다 [부록 b: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixB)합니다.


<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습을 사용 하면 ASP.NET의 새로운 기능 및 Visual Studio 2012에서 웹 개발 이란 무엇 이며 Visual Studio 2012의 다양 한 향상 된 기능을 활용 하는 방법을 이해 하도록 도와줍니다.

이 실습을 완료 하면 Visual Studio 2012 편집기에서 CSS, JavaScript 및 HTML에 대 한 새로운 기능과 향상 된 기능을 사용 하는 방법을 배운 있습니다. 또한 Visual Studio 2012는 기본 제공 묶음 및 축소를 구현 하는 방법에 대해 배운 합니다.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 a: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**. 다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.

1. 로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다. 또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Windows Azure SDK를 사용 하 여 Web</em>&quot;합니다.
2. 클릭할 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.

    ![Visual Studio Express를 설치](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Visual Studio Express를 설치 합니다.")

    *Visual Studio Express를 설치 합니다.*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건에 동의](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    *사용 조건에 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **완료**합니다.

    ![설치 완료](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. 로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.

    ![VS Express for Web 타일](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    *VS Express for Web 타일*

* * *

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>부록 b: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

이 부록은 Windows Azure 관리 포털에서 새 웹 사이트를 만들고 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하 고 랩에 따라 얻은 응용 프로그램을 게시 하는 방법을 보여 줍니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>작업 1-Windows에서 새 웹 사이트를 만드는 Azure Portal

1. 로 이동 합니다 [Windows Azure 관리 포털](https://manage.windowsazure.com/) 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.

    > [!NOTE]
    > Windows Azure를 사용 하 여 10 개의 ASP.NET 웹 사이트를 무료로 호스트할 수 있으며 다음 트래픽 증가 따라 확장할 수 있습니다. 등록할 수 있습니다 [여기](http://aka.ms/aspnet-hol-azure)합니다.

    ![Windows Azure 포털에 로그온](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Windows Azure 포털에 로그온")

    *Windows Azure 관리 포털에 로그온*
2. 클릭 **새로 만들기** 명령 모음에서.

    ![새 웹 사이트를 만드는](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. 클릭 **계산** | **웹 사이트**합니다. 선택한 **빨리 만들기** 옵션입니다. 새 웹 사이트를 사용할 수 있는 URL을 제공 하 고 클릭 **웹 사이트 만들기**합니다.

    > [!NOTE]
    > Windows Azure 웹 사이트는 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트. 빠른 생성 옵션을 사용 하면 완료 된 웹 응용 프로그램을 Windows Azure에서 웹 사이트 포털 외부에서 배포할 수 있습니다. 데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.
5. 웹 사이트를 만든 후 아래의 링크를 클릭 합니다 **URL** 열입니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트를 찾아](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "새 웹 사이트를 검색 합니다.")

    *새 웹 사이트를 검색합니다.*

    ![실행 중인 웹 사이트](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "실행 중인 웹 사이트")

    *실행 중인 웹 사이트*
6. 포털로 돌아가서에서 웹 사이트의 이름을 클릭 합니다 **이름을** 관리 페이지를 표시 하는 열입니다.

    ![웹 사이트 관리 페이지를 열어](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. **대시보드** 페이지의 **간략 상태** 섹션을 클릭 합니다 **게시 프로필 다운로드** 링크.

    > [!NOTE]
    > 합니다 *게시 프로필* 모든 각각의 설정 된 게시 방법에 대 한 Windows Azure 웹 사이트를 웹 응용 프로그램을 게시 하는 데 필요한 정보를 포함 합니다. 게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열을 포함 합니다. **Microsoft WebMatrix 2**하십시오 **Microsoft Visual Studio Express for Web** 하 고 **Microsoft Visual Studio 2012** 읽기 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화할 Windows Azure websites에 웹 응용 프로그램을 게시합니다.

    ![게시 프로필 다운로드 웹 사이트](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "게시 프로필 다운로드 웹 사이트")

    *게시 프로필 다운로드 웹 사이트*
8. 알려진된 위치에 게시 프로필 파일을 다운로드 합니다. 추가이 연습에서이 파일을 사용 하 여 Visual Studio에서 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 방법을 표시 됩니다.

    ![게시 프로필 파일을 저장](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "게시 프로필 저장")

    *게시 프로필 파일을 저장 하는 중*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL 서버를 사용할 경우 데이터베이스를 SQL Database 서버 만들기 해야 합니다. SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하는 것에 대 한 SQL Database 서버를 해야 합니다. Windows Azure 관리 포털에서 구독의 SQL Database 서버를 볼 수 있습니다 **Sql Database** | **서버** | **서버 대시보드**합니다. 만든 서버가 없는 경우 하나를 사용 하 여 만들 수 있습니다 합니다 **추가** 명령 모음에서 단추입니다. 기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**처럼 다음 작업에서 사용 됩니다. 만들지 마십시오 데이터베이스 아직 이후 단계에서 만들어집니다.

    ![SQL Database 서버 대시보드](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database 서버 대시보드")

    *SQL Database 서버 대시보드*
2. 다음 태스크에서는 테스트 Visual Studio에서 데이터베이스 연결 서버 목록에 로컬 IP 주소를 포함 해야 하는 이유로 **허용 된 IP 주소**합니다. 이렇게 하려면 클릭 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여 넣습니다 합니다 **시작 IP 주소** 및 **끝IP주소** 텍스트 상자입니다. 규칙에 대 한 이름을 입력 하 고 클릭 합니다 ![add-client-ip-address-ok-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) 단추입니다.

    ![클라이언트 IP 주소를 추가합니다.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    *클라이언트 IP 주소를 추가합니다.*
3. 한 번 합니다 **클라이언트 IP 주소** 허용 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 변경을 확인 합니다.

    ![변경 확인](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    *변경 확인*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션 돌아갑니다. 에 **솔루션 탐색기**, 웹 사이트 프로젝트를 마우스 오른쪽 단추로 **게시**합니다.

    ![응용 프로그램 게시](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "응용 프로그램 게시")

    *웹 사이트를 게시합니다.*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필 가져오기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "게시 프로필 가져오기")

    *게시 프로필 가져오기*
3. 클릭 **연결의 유효성을 검사**합니다. 유효성 검사가 완료 되 면 클릭 **다음**합니다.

    > [!NOTE]
    > 연결 유효성 검사 단추 옆에 나타나는 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.

    ![연결 유효성 검사](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "연결 유효성 검사")

    *연결 유효성 검사*
4. 에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추를 클릭 (즉 **DefaultConnection**).

    ![웹 배포 구성](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "웹 배포 구성")

    *웹 배포 구성*
5. 데이터베이스 연결을 다음과 같이 구성 합니다.

   - 에 **서버 이름** SQL Database 서버 URL 사용 하 여 입력 합니다 *tcp:* 접두사입니다.
   - **사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 서버 관리자 로그인 암호를 입력 합니다.
   - 예를 들어 새 데이터베이스 이름을 입력 합니다. *MVC4SampleDB*합니다.

     ![대상 연결 문자열 구성](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 다음 **확인**을 클릭합니다. 데이터베이스를 만들라는 메시지가 나오면 **예**합니다.

    ![데이터베이스를 만드는](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "데이터베이스 문자열 만들기")

    *데이터베이스 만들기*
7. 기본 연결 텍스트 상자 내에서 사용 하 여 Windows Azure에서 SQL Database에 연결 하는 연결 문자열 표시 됩니다. **다음**을 클릭합니다.

    ![SQL Database를 가리키는 연결 문자열](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "SQL 데이터베이스를 가리키는 연결 문자열")

    *SQL Database를 가리키는 연결 문자열*
8. 에 **미리 보기** 페이지에서 클릭 **게시**합니다.

    ![웹 응용 프로그램 게시](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.

    ![Windows Azure에 응용 프로그램 게시](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "응용 프로그램이 Windows Azure에 게시")

    *Windows Azure에 게시 하는 응용 프로그램*
