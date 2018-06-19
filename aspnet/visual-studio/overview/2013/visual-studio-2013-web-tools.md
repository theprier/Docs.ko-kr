---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: '실습 랩: Visual Studio 2013 웹 도구 | Microsoft Docs'
author: rick-anderson
description: Visual Studio는에 대 한 뛰어난 개발 환경입니다. 또한 Windows 및 웹 프로젝트입니다. 쉽게 사용할 수 있는 강력한 텍스트 편집기를 포함...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/16/2014
ms.topic: article
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: ef8ab82f9043ef9da3a3e6a146a97f083149534d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
ms.locfileid: "26507132"
---
<a name="hands-on-lab-visual-studio-2013-web-tools"></a>실습 랩: Visual Studio 2013 웹 도구
====================
으로 [웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트를 다운로드 합니다.](http://aka.ms/webcamps-training-kit)

> Visual Studio는에 대 한 뛰어난 개발 환경입니다. 또한 Windows 및 웹 프로젝트입니다. 쉽게 프로젝트 없이 독립 실행형 파일을 편집 하는 데 사용할 수 있는 강력한 텍스트 편집기를 포함 합니다.
> 
> 각 파일을 편집할 때 visual Studio는 모든 기능을 갖춘 구문 분석 트리를 유지 관리 합니다. 이렇게 하면 훨씬 빠르고 더 쾌적 한 개발 환경을 만드는 동안 최상의 자동 완성 기능 및 문서 기반 동작을 제공 하는 Visual Studio 있습니다. 이러한 기능은 HTML 및 CSS 문서에서 특히 유용 합니다.
> 
> 이 전원의 모든 확장의 경우 필요에 따라 강력한 새 기능으로 편집기를 확장 하 여 사용할 수도 있습니다. 웹 Essentials은 대부분 웹 관련 향상 된 Visual Studio의 컬렉션입니다. (특히 CSS)에 대해 새 IntelliSense 완성, 새로운 브라우저 링크 기능으로, 자동 많이 포함 JSHint JavaScript에 대 한 파일, HTML 및 CSS 및 최신 웹 개발에 꼭 필요한 기타 많은 기능에 대 한 새 경고 합니다.
> 
> 모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)합니다.


<a id="Overview"></a>
## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 배웁니다 하는 방법:

- 풍부한 HTML5 코드 조각 및 Zen 코딩 등 웹 Essentials에 포함 된 새 HTML 편집기 기능을 사용 하 여
- 색 선택 및 브라우저 매트릭스 도구 설명 같은 웹 Essentials에 포함 된 새 CSS 편집기 기능을 사용 하 여
- 모든 HTML 요소에 대 한 IntelliSense 파일을 추출 같은 웹 Essentials에 포함 된 새로운 JavaScript 편집기 기능을 사용 하 여
- 브라우저 및 브라우저 링크를 사용 하 여 Visual Studio 사이 데이터 교환

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

다음은이 실습 랩을 완료 하려면 필요 합니다.

- [Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) 이상
- [Web Essentials 2013](http://vswebessentials.com/)
- [Google Chrome](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a>설정

이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.

1. Windows 탐색기 창을 열고 다음을 찾아보기에 랩 **소스** 폴더입니다.
2. 마우스 오른쪽 단추로 클릭 **Setup.cmd** 선택 **관리자 권한으로 실행** 환경을 구성 되며이 랩에 대 한 Visual Studio 코드 조각을 설치 하는 설치 프로세스를 시작 합니다.
3. 사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.

> [!NOTE]
> 설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 선택 했는지 확인 합니다.


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>코드 조각을 사용 하 여

랩 문서를 통해 코드 블록을 삽입 하도록 합니다. 사용자 편의 위해이 코드의 대부분을 수동으로 추가할 필요가 없도록 하려면 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.

> [!NOTE]
> 각 연습에는 시작 솔루션 동반 되는 **시작** 개별적으로 각 연습에 따라 할 수 있는 작업의 폴더입니다. 주의 하십시오 연습 하는 동안 추가 된 코드 조각은 솔루션 시작이 항목에서 누락 되어 연습을 완료 될 때까지 작동 하지 않을 수 있습니다. 실행에 대 한 소스 코드에서 찾아볼 수 있습니다는 **끝** 해당 연습에서 단계를 완료 한 결과인 코드와 함께 Visual Studio 솔루션에 포함 된 폴더입니다. 이 실습 랩에서 진행할 때는 추가 도움이 필요한 경우 이러한 솔루션 가이드로 사용할 수 있습니다.


* * *

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습에 포함 됩니다.

1. [브라우저 링크 및 웹 Essentials 작업](#Exercise1)
2. [코드 조각 및 IntelliSense를 활용 하기 위해](#Exercise2)

> [!NOTE]
> Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션 특정 개발 스타일에 맞게 설계 하 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 랩의 절차를 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업 설명에서 **일반 개발 설정** 컬렉션입니다. 개발 환경에 대 한 서로 다른 설정 컬렉션을 선택 하면 고려해 야 하는 단계에 차이가 있을 수 있습니다.


<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a>브라우저 링크 및 웹 Essentials 연습 1: 작업

**Essentials 웹** 다양 한 웹 개발 환경을 훨씬 빠르고 편리한에 주로 초점을 최신 웹 개발을 위한 유용한 기능을 추가 하는 Visual Studio 확장 합니다. Visual Studio에서 확장 갤러리에서 웹 Essentials를 설치할 수 있습니다.

**브라우저 링크** 웹 응용 프로그램 및 Visual Studio 간에 데이터를 교환 하기 위해 Visual Studio IDE와 모든 열려 있는 브라우저 간의 채널을 제공 하는 Visual Studio 2013에 포함 된 새로운 기능입니다. 웹 Essentials DOM 개체 모델 및 브라우저에서 직접 웹 페이지의 CSS 스타일을 조작 하는 도구와 함께 브라우저 링크 확장 합니다.

이 연습에서는 탐색에서 지 원하는 기능 중 일부 **웹 Essentials** 및 **브라우저 링크** 간단한 퀴즈 페이지를 향상 시키기 위해.

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a>작업 1-다중 브라우저에서 프로젝트를 실행 합니다.

이 작업에서는 다중 브라우저 테스트에 한 번에 여러 브라우저에서 실행 되도록 웹 응용 프로그램을 구성 합니다.

1. 열기 **Microsoft Visual Studio**합니다.
2. 에 **파일** 메뉴 선택 **열기 | 프로젝트/솔루션...**  을 찾아서 **e x 1 WorkingwithBrowserLinkandWebEssentials\Begin** 에 **소스** 랩 (C:\WebCampsTK\HOL\VSWebTooling\Source)의 폴더입니다. 선택 **Begin.sln** 클릭 **열려**합니다.
3. Visual Studio 도구 모음에서 브라우저 메뉴를 확장 하 고 선택 **브라우저 중...** .

    ![메뉴 옵션 브라우저](visual-studio-2013-web-tools/_static/image1.png "브라우저 선택... 브라우저 메뉴에")

    *브라우저 메뉴 옵션*
4. 에 **브라우저** 대화 상자에서 선택 **Google Chrome** 및 **Internet Explorer** 누른는 **CTRL** 누른키 **기본값으로 설정**합니다.

    ![브라우저 대화 상자](visual-studio-2013-web-tools/_static/image2.png "브라우저 대화 상자")

    *여러 기본 브라우저를 선택합니다.*
5. Google Chrome 및 Internet Explorer 모두 기본 브라우저 나타나야 합니다. 클릭 **취소** 대화 상자를 닫습니다.

    ![Internet Explorer를 기본 브라우저 및 Google Chrome](visual-studio-2013-web-tools/_static/image3.png "Google Chrome 및 Internet Explorer 기본 브라우저")

    *Google Chrome 및 Internet Explorer를 기본 브라우저*

    > [!NOTE]
    > 기본 브라우저를 구성한 후의 **여러 브라우저** 브라우저 메뉴에서 옵션을 선택 합니다.
    > 
    > ![여러 브라우저](visual-studio-2013-web-tools/_static/image4.png "여러 브라우저")
6. 키를 눌러 **CTRL** + **F5** 디버깅 하지 않고 응용 프로그램을 실행 합니다.
7. 두 브라우저 창을 열면 브라우저 모두에서 동시에 업데이트를 확인 하기 위해 상하로 둘 중 하나를 배치 합니다. 브라우저는 연한 파란색 사각형에 포함 된 웹 페이지가 표시 됩니다.

    ![하나의 브라우저 상하로 배치](visual-studio-2013-web-tools/_static/image5.png "브라우저 상하로 배치")

    *하나의 브라우저 상하로 배치*
8. 브라우저를 닫지 마십시오. 다음 태스크에서에 사용 합니다.

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a>작업 2-를 사용 하 여 Zen HTML 요소를 만드는 코딩

**Zen 코딩** 은 편집기 고속 HTML, XML, XSL (또는 다른 구조적된 코드 형식)에 대 한 플러그 인을 코딩 하 고 편집 합니다. 이 플러그 인의 핵심은 식을-CSS 선택기 비슷합니다-HTML 코드도 확장할 수 있는 강력한 약어 엔진입니다. Zen 코딩을 빠르게 CSS를 사용 하 여 HTML 스타일 선택기 구문을 쓰려고 합니다.

이 연습에서는 질문의 옵션을 나타내는 HTML 단추를 생성 하려면 웹 Essentials에서 제공 Zen 코딩 기능을 사용 합니다.

1. Visual Studio로 다시 전환 합니다.
2. 열기는 **Index.cshtml** 에 있는 파일의 **뷰** | **홈** 폴더입니다.
3. 대체는 **&lt;!-TODO: 여기-옵션 추가&gt;** 메모 앞에 다음 코드 및 키를 눌러 **탭**합니다.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. 코드를 HTML로 확장 해야 합니다.

    ![HTML 확장](visual-studio-2013-web-tools/_static/image6.png "HTML 확장")

    *확장 된 HTML*

    > [!NOTE]
    > Zen 코딩 구문에 대 한 자세한 내용은 다음을 참조 [문서](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)합니다.
5. 클릭는 **연결 된 브라우저를 새로 고칠** 단추를 두는 브라우저를 업데이트 합니다.

    ![연결 된 브라우저를 새로 고침](visual-studio-2013-web-tools/_static/image7.png "연결 된 브라우저를 새로 고칩니다.")

    *연결 된 브라우저를 새로 고칩니다.*

    ![단추가 네 개 있는 Internet Explorer-페이지가 업데이트](visual-studio-2013-web-tools/_static/image8.png "단추가 네 개 있는 Internet Explorer-페이지가 업데이트")

    *단추가 네 개 있는 Internet Explorer-페이지가 업데이트*

    ![Google Chrome-페이지가 업데이트 단추가 네 개 있는](visual-studio-2013-web-tools/_static/image9.png "단추가 네 개 있는 Google Chrome-페이지가 업데이트")

    *단추가 네 개 있는 Google Chrome-페이지가 업데이트*
6. Visual Studio로 다시 전환 합니다.
7. 단추는 페이지에 추가 했지만 여전히 템플릿 질문 추가 해야 합니다. 이렇게 하려면 호출 하는 웹 Essentials의 새로운 기능을 사용 합니다 **Lorem Ipsum 생성기**합니다. 찾을 **div** 인 요소는 **클래스** 특성 **앞**합니다.
8. 다음 코드의 첫 번째 자식 요소로 추가 **div**, 누릅니다 **탭**합니다.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. 코드를 HTML로 확장 해야 합니다.

    ![자동 생성 된 Lorem Ipsum](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum 자동 생성")

    *Lorem Ipsum 자동 생성*

    > [!NOTE]
    > Zen 코딩의 일환으로, HTML 편집기에서 직접 이제 Lorem Ipsum 코드를 생성할 수 있습니다. 입력 **lorem** 적중 및 **탭** 30 Lorem Ipsum 텍스트가 삽입 됩니다. 예: *lorem10* 10 Lorem Ipsum 단어를 삽입 합니다.
10. 호출 웹 Essentials의 또 다른 새로운 기능을 사용 하 여 질문 맨 위에 있는 로고를 추가 합니다 **Lorem 픽셀 생성기**합니다. 다음 코드의 첫 번째 자식 요소로 추가 **div** 요소 **컨테이너** 으로 **클래스** 값 및 키를 눌러 **탭**합니다.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. 코드는 HTML을 확장 해야 합니다.

    ![자동 생성 된 Lorem 픽셀](visual-studio-2013-web-tools/_static/image11.png "Lorem 픽셀 자동 생성")

    *Lorem 픽셀 자동 생성*

    > [!NOTE]
    > Zen 코딩의 일환으로, HTML 편집기에서 직접 Lorem 픽셀 코드를 생성할 수도 있습니다. 입력 **pix-200 x 200-동물** 적중 및 **탭** 및 **img** 태그 동물의 200 x 200 이미지와 함께 삽입 됩니다. 자세한 내용은를 참조 [Lorem 픽셀](http://www.lorempixel.com)합니다.
12. 클릭는 **연결 된 브라우저를 새로 고칠** 단추를 두는 브라우저를 업데이트 합니다.

    ![Internet Explorer-자동으로 생성 된 이미지 및 텍스트](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer-자동으로 생성 된 이미지 및 텍스트")

    *Internet Explorer-자동으로 생성 된 이미지 및 텍스트*

    ![Google Chrome-자동으로 생성 된 이미지 및 텍스트](visual-studio-2013-web-tools/_static/image13.png "Google Chrome-자동으로 생성 된 이미지 및 텍스트")

    *Google Chrome-자동으로 생성 된 이미지 및 텍스트*

    > [!NOTE]
    > 코드 조각을 추가 하는 경우 이미지를 임의로 선택, 때문에 브라우저에 표시 되는 이미지 달라질 수 있습니다.
13. 브라우저를 닫지 마십시오. 다음 태스크에서에 사용 합니다.

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a>작업 3-스타일 속성 업데이트

이 작업을 사용 하 여 브라우저 링크 **검사 모드** 여기서 특정 DOM 요소는 생성 된 정확한 위치를 검색 하 고 다음 웹에서 제공 되는 색상 선택기를 사용 하 여 해당 요소의 color 속성을 업데이트 하는 기능 필수 정보입니다.

1. Internet Explorer 브라우저에서 눌러 **CTRL** + **ALT** + **I** 검사 모드를 사용 하도록 합니다.
2. 밝은 파란색 테두리가 위로 포인터를 이동 하 고를 클릭 합니다.

    ![밝은 파란색 테두리가 위로 포인터를 이동](visual-studio-2013-web-tools/_static/image14.png "밝은 파란색 테두리가 위로 포인터를 이동")

    *밝은 파란색 테두리가 위로 포인터를 이동*
3. Visual Studio로 다시 전환 합니다. 브라우저에서 선택 하는 HTML 요소 Visual Studio HTML 편집기에서 선택도 방법을 확인 하십시오.

    ![Visual Studio HTML 편집기에서 선택 된 HTML 요소](visual-studio-2013-web-tools/_static/image15.png "HTML 요소를 Visual Studio HTML 편집기에서 선택 합니다.")

    *Visual Studio HTML 편집기에서 선택 된 HTML 요소*
4. 가 지금 업데이트는 **앞** 선택한 요소의 스타일을 변경 하기 위해 CSS 클래스입니다. 이렇게 하려면 다음을 눌러 **CTRL** + **,** 열려는 **탐색** 검색 상자. 형식 **site.css** 누릅니다 **ENTER** 파일을 열 수 있습니다.

    ![Site.css 파일을 열면](visual-studio-2013-web-tools/_static/image16.png "Site.css 파일을 여는")

    *Site.css 파일 열기*
5. 키를 눌러 **CTRL** + **F** 유형과 **.flip 컨테이너.front** CSS 선택기를 찾으려고 합니다.
6. 색상 선택기를 열려는 클래스의 테두리 속성에 있는 밝은 파란색 사각형을 클릭 합니다.

    ![색 선택 열기](visual-studio-2013-web-tools/_static/image17.png "색 선택 열기")

    *색 선택 열기*
7. 펼침 단추를 클릭 하 여 색상 선택기를 확장 하 고 새 색을 선택 합니다.

    ![색 선택 확장](visual-studio-2013-web-tools/_static/image18.png "색상 선택기를 확장 합니다.")

    *색상 선택기를 확장합니다.*
8. 키를 눌러 **CTRL** + **ALT** + **ENTER** 연결 된 브라우저를 새로 고칠 수 있습니다.
9. Internet Explorer로 전환한 테두리의 색 어떻게 변경 되었는지 확인 합니다.

    ![Internet Explorer-업데이트 테두리 색](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer-업데이트 테두리 색입니다.")

    *Internet Explorer-업데이트 테두리 색입니다.*
10. Google Chrome 전환한 테두리의 색 어떻게 변경 되었는지 확인 합니다.

    ![Google Chrome-업데이트 테두리 색](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-업데이트 테두리 색입니다.")

    *Google Chrome-업데이트 테두리 색입니다.*
11. Visual Studio로 다시 전환 합니다.
12. 끝으로 이동는 **Site.css** 파일 및 키를 눌러 **CTRL** + **F** 찾으려고는 **.btn** 선택기입니다.
13. 다음에 유의 **-webkit 테두리 반지름** 속성은 녹색으로 밑줄이 표시 됩니다.

    ![-webkit 테두리 반지름 속성 btn 선택기의](visual-studio-2013-web-tools/_static/image21.png "btn 선택기의-webkit 테두리 반지름 속성")

    *btn 선택기의-webkit 테두리 반지름 속성*
14. 에 캐럿 배치는 **-webkit 테두리 반지름** 속성입니다. 속성의 첫 번째 단어의 첫 문자 아래 파란색 선이 표시 됩니다. 이는 **스마트 태그**합니다.
15. 키를 눌러 **CTRL** + **합니다.** 제안 메뉴를 열고 클릭 **표준 속성 (테두리 radius) 누락 된 추가**합니다.

    ![표준 속성 제안 누락 추가](visual-studio-2013-web-tools/_static/image22.png "표준 속성 제안 누락 추가")

    *표준 속성 제안 누락 된 추가*
16. **테두리 radius** 속성 CSS 규칙에 자동으로 추가 됩니다.

    ![추가 표준 속성이 누락](visual-studio-2013-web-tools/_static/image23.png "누락를 추가 하는 표준 속성")

    *표준 속성 추가*
17. 포인터를 가져가서는 **테두리 radius** 속성을 표시는 **브라우저 매트릭스 도구 설명**합니다. **브라우저 매트릭스 도구 설명** 각 브라우저에서 속성의 가용성을 보여 줍니다.

    ![브라우저 매트릭스 도구 설명](visual-studio-2013-web-tools/_static/image24.png "브라우저 매트릭스 도구 설명")

    *브라우저 매트릭스 도구 설명*
18. 다음에 유의 값은 **테두리 radius** 속성은 여전히 밑줄 서식을 적용 합니다. 경고 메시지를 보려면 값 위로 포인터를 이동 합니다.

    ![테두리 radius 속성 값 경고](visual-studio-2013-web-tools/_static/image25.png "테두리 radius 속성 값 경고")

    *테두리 radius 속성 값 경고*
19. 단위를 제거는 **테두리 radius** 도구 설명에서 제시한 대로 속성 값입니다.
20. 으로 **테두리 radius** 모서리는 제거할 수 있습니다 어떻게 모서리가 둥근된 테두리를 정의 하기 위한 표준 속성는 **-webkit 테두리 반지름** 속성 및 CSS 규칙에서 값입니다.
21. 에 캐럿 배치는 **바꿈** 속성 및 스마트 태그 아래도 나타납니다.
22. 메뉴를 열고 클릭 **누락 된 공급 업체 비슷하므로 추가**합니다.

    ![누락 된 공급 업체에 대 한 구체적인 제안 사항을 추가](visual-studio-2013-web-tools/_static/image26.png "누락 된 공급 업체에 대 한 구체적인 제안 사항을 추가")

    *누락 된 공급 업체에 대 한 구체적인 제안 사항을 추가합니다*
23. **ms 단어 잘림** 속성 CSS 규칙에 자동으로 추가 됩니다.

    ![공급 업체 관련 속성 추가](visual-studio-2013-web-tools/_static/image27.png "공급 업체 관련 속성 추가")

    *공급 업체 관련 속성 추가*

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a>작업 4-브라우저에서 HTML 코드 업데이트

이 작업을 사용 하 여 브라우저 링크 **디자인 모드** 브라우저에서 DOM 개체를 편집 및 Visual Studio에서 HTML 소스 파일에 변경 내용을 전송 하는 기능입니다.

1. Google Chrome에서 눌러 **CTRL** + **ALT** + **D** 디자인 모드를 사용 하도록 합니다.
2. 위로 포인터를 이동는 **Lorem Ipsum dolor sit amet** 레이블을 지정 하 고를 클릭 합니다.

    ![질문 편집](visual-studio-2013-web-tools/_static/image28.png "질문 편집")

    *질문을 편집합니다.*
3. 커서가 표시 됩니다. 원래 텍스트를 대체 *않습니다 것 모양을 긴 질문을 쓸 때?*, 한 다음 키를 누릅니다 **ESC** 디자인 모드를 종료 합니다.

    ![편집할 질문](visual-studio-2013-web-tools/_static/image29.png "질문 편집")

    *편집할 질문*
4. Visual Studio로 다시 및 open 스위치 **Index.cshtml**열려 있지 않으면, 합니다. 다음에 유의의 내부 텍스트는 **&lt;p&gt;** 요소가 업데이트 되었습니다.

    ![HTML 페이지에 업데이트 된 질문](visual-studio-2013-web-tools/_static/image30.png "HTML 페이지에 업데이트 된 질문")

    *HTML 페이지에 업데이트 된 질문*

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a>작업 5-검토 SEO 관련 경고

**검색 엔진 최적화** SEO ()은 검색 엔진 결과 목록에 더 높은 순위 웹 사이트를 만드는 프로세스입니다. 사이트의 순위가 높을수록, 나열 된 더 일관 되 게, 더 많은 방문자 사이트 해당 검색 엔진에서 발생 합니다. 웹 Essentials 통합 HTML을 검사 하는 분석 도구, 보고서 문제 발견 하 고 수정 지원을 제공 합니다.

1. 이동 하는 **보기** 메뉴를 클릭 **오류 목록** 열려는 **오류 목록** 창.

    ![오류 목록 보기에 메뉴](visual-studio-2013-web-tools/_static/image31.png "보기 메뉴의 오류 목록")

    *오류 목록 보기에 메뉴*
2. 한 SEO을 알리는 경고를 하는 한 **&lt;메타&gt;** 페이지 설명에 대 한 태그를 지정 합니다. 이 문제를 해결할 SEO 경고 항목을 두 번 클릭 합니다.

    ![오류 목록 창](visual-studio-2013-web-tools/_static/image32.png "오류 목록 창")

    *오류 목록 창*
3. 에 **웹 Essentials** 대화 상자에서 클릭 **예** 설명은 삽입 하려면 &lt;메타&gt; 태그입니다.

    ![웹 Essentials 대화 상자](visual-studio-2013-web-tools/_static/image33.png "웹 Essentials 대화 상자")

    *웹 Essentials 대화 상자*
4. 에 대 한 편집기  **\_Layout.cshtml** 열립니다 및 **&lt;메타&gt;** 태그 자동으로 추가 되는 **h e a d** 의 섹션의 HTML 파일입니다.

    ![_Layout 페이지에 자동으로 추가 하는 메타 태그](visual-studio-2013-web-tools/_static/image34.png "_Layout 페이지에 자동으로 추가 하는 메타 태그")

    *에 자동으로 추가 하는 메타 태그 \_페이지 레이아웃*
5. 값을 변경는 **콘텐츠** 특성을 *GeekQuiz* 파일을 저장 합니다.

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a>연습 2: 코드 조각 및 IntelliSense를 활용 하기 위해

웹 essentials HTML 편집기는 추가 기능으로 확장 되었습니다. 이 연습에서는 웹 응용 프로그램을 개발할 때 도움이 되는 일부 새로운 기능은 표시 됩니다.

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a>작업 1-HTML 문서에 IntelliSense 사용

이 작업에 표시 되는 첫 번째 새 기능을 라고 **동적 IntelliSense**합니다. 동적 IntelliSense에는 다른 태그 및 특성을 사용 하 여 가능한 id 유추 읽습니다.

이 태스크에서는 레이블 및 입력된 필드를 포함 하는 새 HTML 폼 요소에 만들어집니다. 다음 추가 됩니다 한 **에 대 한** 입력을 바인딩할 레이블에 특성 범위에서 입력의 id에 따라 IntelliSense 제안 사항이 표시 됩니다.

1. 열기 **Visual Studio Express 2013 for Web** 및 **Begin.sln** 솔루션에 있는 **소스/e x 2-TakingAdvantageofCodeSnippetsandIntelliSense/시작** 폴더입니다. 또는 계속할 수 있습니다 솔루션으로, 이전 연습에서 가져올 있음을.
2. **솔루션 탐색기**열고는 **Index.cshtml** 에 있는 파일의 **뷰** | **홈** 폴더입니다.
3. 내부 다음 양식을 추가 **&lt;섹션&gt;** 요소입니다.

    (코드 조각- *VisualStudio2013WebTooling* - *e x 2* - *양식*)

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. 입력된 태그 일부 설명은 필드 레이블 뒤에 야 합니다. 입력된 태그 앞에 다음 레이블을 추가 합니다.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. **에 대 한** 특성에는 **&lt;레이블&gt;** 레이블이 폼 요소에 바인딩된 지정 합니다. 특성의 값은 관련 된 요소의 id로 같아야 합니다. 추가 **에 대 한** 특성을 **&lt;레이블&gt;** 요소입니다. 다음 그림에 나와 있는 것 처럼는 &quot;이름&quot; 값 팝업 IntelliSense 상자에서 동일한 범위 내 요소의 id에 따라 (묶는  **&lt;양식&gt;**).

    ![IntelliSense의 id를 보여 주는](visual-studio-2013-web-tools/_static/image35.png "IntelliSense에 id를 표시 합니다.")

    *IntelliSense에 id를 표시합니다.*
6. 최근에 추가 된 삭제 **&lt;양식&gt;** 요소와 해당 콘텐츠입니다.

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a>작업 2-HTML 코드 조각을 사용 하 여

HTML5 25 개 이상의 새로운 의미 체계 태그를 도입 되었습니다. Visual Studio가 이미 이러한 태그에 대 한 IntelliSense 지원 하지만 Visual Studio 2013을 사용 하면 빠르고 쉽게 새 코드 조각을 추가 하 여 태그를 작성 하 합니다. 에 대 한 올바른 코덱을 대체를 추가 하는 등 몇 가지 작은 미묘한 함께 제공 되는 경우에 이러한 태그 크게 복잡 하지 않습니다는 *오디오* 태그입니다. 이 태스크에서는 오디오 태그에 대 한 HTML 코드 조각을 표시 됩니다.

1. 에 **Index.cshtml** 파일, 입력  **&lt;aud** 내는 **&lt;섹션&gt;** 요소는 다음 그림에 나와 있는 것 처럼 합니다.

    ![오디오 요소를 삽입할](visual-studio-2013-web-tools/_static/image36.png "오디오 요소 삽입")

    *오디오 요소 삽입*
2. 키를 눌러 **탭** 두 번과 페이지에서 다음 코드에 어떻게 추가 되었는지를에 커서가 놓입니다는 **src** 첫 번째 소스의 특성입니다.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > 키를 눌러는 **탭** 키를 두 번 코드 조각을 삽입 됩니다. 오디오 조각 대 한 일반 사용법을 보여 줍니다.는 *오디오* 지원 향상된에 대 한 소스 파일의 태그입니다.
3. 두 번째 줄을 삭제 하 고 다음 링크를 WebCampsTV Katana 표시도 첫 번째 줄의 소스를 업데이트: [ http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3 ](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)합니다. 결과 코드는 다음과 같습니다.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > 소스 파일 *KatanaProject.mp3* 예제로 사용 합니다. 다른 소스 원할 경우 사용할 수 있습니다.
4. 키를 눌러 **CTRL** + **S** 파일을 저장 합니다.
5. 키를 눌러 **CTRL** + **F5** 는 응용 프로그램을 시작 합니다.
6. 오디오 플레이어 응용 프로그램에 추가 되는지 확인 합니다.

    ![Internet Explorer에서 오디오 플레이어](visual-studio-2013-web-tools/_static/image37.png "Internet Explorer에서 오디오 플레이어")

    *Internet Explorer에서 오디오 플레이어*

    ![Google Chrome의 오디오 플레이어](visual-studio-2013-web-tools/_static/image38.png "Google Chrome의 오디오 플레이어")

    *Google Chrome의 오디오 플레이어*
7. 브라우저를 닫지 마십시오. 다음 태스크에서에 사용 합니다.

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a>작업 3-JavaScript 문서에 IntelliSense 사용

웹 Essentials 2013과 함께 스타일 시트 및 HTML 페이지의 Id 및 클래스 이름 목록을 생성 합니다. 이 태스크에서는 해당 목록의 웹 Essentials 2013의 JavaScript IntelliSense 지원 개선 하는 방법을 배웁니다.

1. 에 **Index.cshtml** 파일에서 다음 코드를 추가 정의 **스크립트** JavaScript 코드에 대 한 태그입니다.

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. 다음 코드를 추가 **스크립트** 준비 콜백 함수를 정의 하는 태그입니다.

    (코드 조각- *VisualStudio2013WebTooling* - *e x 2* - *ReadyFunction*)

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. 에 캐럿 배치는 **스크립트** 태그 및 키를 눌러 **CTRL** + **합니다.** 메뉴를 열려면 제안 합니다.
4. 클릭 **파일로 추출할**합니다.

    ![JavaScript 파일 제안 추출할](visual-studio-2013-web-tools/_static/image39.png "JavaScript 파일 제안에 추출")

    *JavaScript 파일 제안에 추출*
5. 에 **다른 이름으로 저장** 창에서는 **스크립트** 폴더에서 파일 이름 **init.js** 클릭 **저장**합니다.

    ![다른 이름으로 저장 창](visual-studio-2013-web-tools/_static/image40.png "이름으로 저장 창")

    *다른 이름으로 저장 창*

    > [!NOTE]
    > **init.js** 파일을 만들고 파일에 스크립트의 내용을 이동 됩니다.
    > 
    > ![포함 된 콘텐츠를 사용 하 여 만든 Init.js 파일](visual-studio-2013-web-tools/_static/image41.png "포함 된 콘텐츠를 사용 하 여 만든 Init.js 파일")
    > 
    > *포함 된 콘텐츠를 사용 하 여 만든 Init.js 파일*
6. 열기는 **Index.cshtml** 파일 및 스크립트 태그에 대 한 참조로 교체 되었습니다 확인는 **init.js** 파일입니다.

    ![Init.js html 참조](visual-studio-2013-web-tools/_static/image42.png "Init.js html 참조")

    *Init.js html 참조*
7. 이동 하는 **솔루션 탐색기** 과 **init.js** 파일이 솔루션에 자동으로 포함 되었습니다.

    ![솔루션에 포함 된 Init.js 파일](visual-studio-2013-web-tools/_static/image43.png "솔루션에 포함 된 Init.js 파일")

    *솔루션에 포함 된 Init.js 파일*
8. 로 다시 전환는 **init.js** 업데이트할 파일을 여 **준비** 콜백 함수입니다.
9. 에 전달 되는 함수 콜백 정의 내 *준비*, 요소를 가져오는 모든 특정 클래스 특성으로 다음 코드를 추가 합니다.

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. 키를 눌러 **CTRL** + **공간** 내 고 따옴표 사이 **getElementsByClassName** 함수 호출 합니다.

    ![GetElementsByClassName 함수에 대 한 IntelliSense를 보여 주는](visual-studio-2013-web-tools/_static/image44.png "getElementsByClassName 함수에 대 한 보여 주는 IntelliSense")

    *IntelliSense getElementsByClassName 함수에 대 한 표시*

    > [!NOTE]
    > IntelliSense 프로젝트 스타일 시트에 정의 된 클래스에 표시 되는지 확인 합니다.
11. 다음 코드를 사용 하 여 생성 하는 줄을 바꿉니다.

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. 뒤에 커서를 놓습니다 **au** 에서 따옴표에 포함 된 **getElementsByTagName** 함수 및 키를 눌러 **CTRL** + **공간**.

    ![GetElementByTagName 메서드에 대 한 IntelliSense를 보여 주는](visual-studio-2013-web-tools/_static/image45.png "getElementByTagName 메서드를 보여 주는 IntelliSense")

    *IntelliSense getElementsByTagName 메서드에 대 한 표시*
13. 선택 **&quot;오디오&quot;** 목록 및 키를 눌러 **ENTER**합니다. 결과는 다음 그림에 나와 있습니다.

    ![오디오 요소 검색](visual-studio-2013-web-tools/_static/image46.png "오디오으로 요소 검색")

    *오디오 요소 검색*
14. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **init.js** 파일에 **스크립트** 폴더를 선택 **축소할 JavaScript 파일** 에서 **웹 Essentials** 메뉴.

    ![JavaScript 파일을 축소할](visual-studio-2013-web-tools/_static/image47.png "축소할 JavaScript 파일")

    *JavaScript 파일을 축소합니다*
15. 소스 파일 변경 내용을 클릭할 때 자동 축소를 사용 하도록 설정 하 라는 메시지가 나타나면 **예**합니다.

    ![자동 축소 경고를 사용 하도록 설정](visual-studio-2013-web-tools/_static/image48.png "자동 축소 경고를 사용 하도록 설정")

    *자동 축소 경고를 사용 하도록 설정*

    > [!NOTE]
    > **init.min.js** 생성 되 고의 종속 항목으로 추가 된 **init.js** 파일입니다.
    > 
    > ![만든 Init.min.js 파일](visual-studio-2013-web-tools/_static/image49.png "만든 Init.min.js 파일")
    > 
    > *만든 Init.min.js 파일*
16. 열기는 **init.min.js** 파일 및 파일 축소는 확인 합니다.

    ![Init.min.js 파일 내용을](visual-studio-2013-web-tools/_static/image50.png "Init.min.js 파일 콘텐츠")

    *Init.min.js 파일 콘텐츠*
17. 에 **init.js** 파일, 아래 다음 코드를 추가 **getElementsByTagName** 함수 호출에 오디오 모든 요소를 재생할 수 있습니다.

    (코드 조각- *VisualStudio2013WebTooling* - *e x 2* - *PlayAudioElements*)

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. 클릭 **CTRL** + **S** 파일을 저장 합니다. 축소 된 파일을 열면 이미 있으므로 파일이 소스 편집기 외부에서 수정 된 없다는 대화 상자가 표시 됩니다. **예**를 클릭합니다.

    ![Microsoft Visual Studio 경고](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio 경고")

    *Microsoft Visual Studio 경고*
19. 로 다시 전환는 **init.min.js** 파일을 새 코드 파일을 업데이트를 확인 합니다.

    ![업데이트 Init.min.js 파일](visual-studio-2013-web-tools/_static/image52.png "Init.min.js 파일 업데이트")

    *Init.min.js 파일 업데이트*
20. 클릭는 **브라우저 링크 새로 고침** 단추입니다.
21. 두 브라우저 새로 고침 되 면 이전 작업에서 표시 오디오 플레이어는 자동으로 재생이 시작 됩니다.

    ![보기에 포함 되는 오디오 플레이어](visual-studio-2013-web-tools/_static/image53.png "오디오 플레이어 보기에 포함")

    *보기에 포함 되는 오디오 플레이어*

* * *

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩을 완료 하 여 배웠습니다 하는 방법:

- 풍부한 HTML5 코드 조각 및 Zen 코딩 등 웹 Essentials에 포함 된 새 HTML 편집기 기능을 사용 하 여
- 색 선택 및 브라우저 매트릭스 도구 설명 같은 웹 Essentials에 포함 된 새 CSS 편집기 기능을 사용 하 여
- 모든 HTML 요소에 대 한 IntelliSense 파일을 추출 같은 웹 Essentials에 포함 된 새로운 JavaScript 편집기 기능을 사용 하 여
- 브라우저 및 브라우저 링크를 사용 하 여 Visual Studio 사이 데이터 교환
