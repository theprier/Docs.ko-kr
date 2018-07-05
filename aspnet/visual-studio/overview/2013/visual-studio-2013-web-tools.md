---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: '실습: Visual Studio 2013 Web Tools | Microsoft Docs'
author: rick-anderson
description: Visual Studio는는 뛰어난 개발 환경입니다. NET 기반의 Windows 및 웹 프로젝트를 제공 합니다. 쉽게 사용할 수 있는 강력한 텍스트 편집기를 포함 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/16/2014
ms.topic: article
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
ms.technology: ''
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 8f0f19a184d50cdc6e8e5a2da0e55a0e8ca44dc5
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399402"
---
<a name="hands-on-lab-visual-studio-2013-web-tools"></a>실습: Visual Studio 2013 Web Tools
====================
[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트 다운로드](http://aka.ms/webcamps-training-kit)

> Visual Studio는는 뛰어난 개발 환경입니다. NET 기반의 Windows 및 웹 프로젝트를 제공 합니다. 프로젝트 없이 독립 실행형 파일을 편집 하려면 쉽게 사용할 수 있는 강력한 텍스트 편집기를 포함 합니다.
> 
> Visual Studio는 각 파일을 편집할 때 완전 한 구문 분석 트리를 유지 합니다. 이렇게 하면 Visual Studio 개발 환경을 훨씬 빠르고 더욱 쾌적 하는 동안 뛰어난된 자동 완성 기능 및 문서 기반 작업을 제공 합니다. 이러한 기능은 HTML 및 CSS 문서에서 특히 유용 합니다.
> 
> 이 전원의 모든 확장을 쉽게 확장 요구에 맞게 강력한 새 기능을 사용 하 여 편집기를 사용할 수도 있습니다. Web Essentials는 대부분 웹 관련 향상 된 Visual Studio의 컬렉션입니다. 여기에 많은 새 IntelliSense 완성 (특히에 대 한 CSS), 새 브라우저 링크 기능, 자동 JSHint JavaScript에 대 한 파일, HTML 및 CSS 및 최신 웹 개발에 필수적인 기타 많은 기능이 대 한 새 경고 합니다.
> 
> 웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)합니다.


<a id="Overview"></a>
## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 학습할 방법:

- 풍부한 HTML5 코드 조각 및 Zen 코딩 등 Web Essentials에 포함 된 새 HTML 편집기 기능 사용
- 색 선택 및 브라우저 행렬 도구 설명 등 Web Essentials에 포함 된 새 CSS 편집기 기능 사용
- 모든 HTML 요소에 대 한 IntelliSense 파일을 추출 등 Web Essentials에 포함 된 새 JavaScript 편집기 기능 사용
- 브라우저와 브라우저 링크를 사용 하 여 Visual Studio 간에 Exchange 데이터

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

다음는이 실습을 완료 해야 합니다.

- [Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) 이상
- [Web Essentials 2013](http://vswebessentials.com/)
- [Google Chrome](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a>설정

이 실습에서는 연습을 실행 하려면 먼저 환경 설정을 설정 해야 합니다.

1. Windows 탐색기 창을 열고 랩의 이동할 **원본** 폴더입니다.
2. 마우스 오른쪽 단추로 클릭 **Setup.cmd** 선택한 **관리자 권한으로 실행** 환경을 구성 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치는 설치 프로세스를 시작 합니다.
3. 사용자 계정 컨트롤 대화 상자를 표시 하는 경우 계속 하려면 작업을 확인 합니다.

> [!NOTE]
> 설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 선택 했는지 확인 합니다.


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>코드 조각 사용

랩 문서 전체에서 코드 블록을 삽입할 지시 됩니다. 사용자 편의 위해이 코드의 대부분은 수동으로 추가할 필요가 없도록 하려면 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.

> [!NOTE]
> 각 실습에 시작 솔루션을 함께 표시 됩니다는 **시작** 다른 독립적으로 각 연습에 따라 할 수 있는 연습 하는 폴더입니다. 주의 하십시오 연습 하는 동안 추가 되는 코드 조각은 솔루션부터 이러한 누락 되어 연습을 완료 될 때까지 작동 하지 않을 수 있습니다. 연습에 대 한 소스 코드 안에 있습니다.는 **최종** 해당 연습에서 단계를 완료 합니다. 결과로 생성 되는 코드를 사용 하 여 Visual Studio 솔루션에 포함 된 폴더입니다. 이 실습을 통해 작업 하는 동안 추가 도움이 필요한 경우 지침으로 이러한 솔루션을 사용할 수 있습니다.


* * *

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습에 포함 됩니다.

1. [브라우저 링크 및 Web Essentials 사용](#Exercise1)
2. [코드 조각 및 IntelliSense를 활용](#Exercise2)

> [!NOTE]
> Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션에는 특정 개발 스타일에 맞게 설계 되었습니다 및 창 레이아웃, 동작 편집기, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 랩의 절차에서는 사용 하는 경우 Visual Studio에서 지정된 된 태스크를 수행 하는 데 필요한 작업을 설명 합니다 **일반 개발 설정** 컬렉션입니다. 개발 환경에 대 한 다양 한 설정 컬렉션을 선택 하는 경우를 고려해 야 하는 단계에 차이가 있을 수 있습니다.


<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a>연습 1: 브라우저 링크 및 Web Essentials 사용

**Web Essentials** 는 다양 한 웹 개발 환경을 훨씬 빠르고 더욱 쾌적에 주로 초점을 최신 웹 개발을 위한 유용한 기능을 추가 하는 Visual Studio 확장입니다. Visual Studio 확장 갤러리에서 Web Essentials를 설치할 수 있습니다.

**브라우저 링크** 웹 응용 프로그램 및 Visual Studio 간에 데이터를 교환 하는 Visual Studio IDE 및 열려 있는 브라우저 사이 채널을 제공 하는 Visual Studio 2013에 포함 된 새로운 기능입니다. Web Essentials는 DOM 개체 모델 및 브라우저에서 직접 웹 페이지의 CSS 스타일을 조작 하는 도구를 사용 하 여 브라우저 링크를 확장 합니다.

이 연습에서는 탐색 지 원하는 기능 중 일부 **Web Essentials** 하 고 **브라우저 링크** 간단한 퀴즈 페이지를 향상 시키기 위해.

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a>작업 1-여러 브라우저에서 프로젝트를 실행 합니다.

이 태스크에서는 브라우저 간 테스트에 유용한 여러 브라우저에서 한 번에 실행 되도록 웹 응용 프로그램을 구성 합니다.

1. 오픈 **Microsoft Visual Studio**합니다.
2. 에 **파일** 메뉴에서 **열기 | 프로젝트/솔루션...**  로 이동한 **e x 1 WorkingwithBrowserLinkandWebEssentials\Begin** 에 **소스** 랩 (C:\WebCampsTK\HOL\VSWebTooling\Source)의 폴더입니다. 선택 **Begin.sln** 누릅니다 **오픈**합니다.
3. Visual Studio 도구 모음에서 브라우저의 메뉴를 확장 하 고 선택 **브라우저...** .

    ![메뉴 옵션 브라우저](visual-studio-2013-web-tools/_static/image1.png "... 브라우저 메뉴에서 사용 하 여 찾아보기")

    *브라우저 메뉴 옵션*
4. 에 **브라우저** 대화 상자에서 선택 **Google Chrome** 및 **Internet Explorer** 누른 합니다 **CTRL** 누른키 **기본값으로 설정**합니다.

    ![대화 상자를 사용 하 여 찾아보기](visual-studio-2013-web-tools/_static/image2.png "대화 상자를 사용 하 여 찾아보기")

    *여러 기본 브라우저를 선택합니다.*
5. Internet Explorer 및 Google Chrome 브라우저를 기본으로 나타나야 합니다. 클릭 **취소** 대화 상자를 닫습니다.

    ![기본 브라우저가 Internet Explorer 및 Google Chrome](visual-studio-2013-web-tools/_static/image3.png "Google Chrome 및 Internet Explorer 기본 브라우저")

    *Google Chrome 및 Internet Explorer 기본 브라우저*

    > [!NOTE]
    > 기본 브라우저를 구성한 후 합니다 **여러 브라우저** 브라우저 메뉴에서 옵션을 선택 합니다.
    > 
    > ![여러 브라우저](visual-studio-2013-web-tools/_static/image4.png "다중 브라우저")
6. 키를 눌러 **CTRL** + **F5** 디버깅 하지 않고 응용 프로그램을 실행 합니다.
7. 두 브라우저 창을 열면 두 브라우저에서 동시에 업데이트를 확인 하기 위해 다른 위에 그 중 하나를 배치 합니다. 브라우저 밝은 파란색 사각형을 사용 하 여 웹 페이지에 표시 됩니다.

    ![위의 다른 하나의 브라우저 배치](visual-studio-2013-web-tools/_static/image5.png "위에 다른 하나의 브라우저를 배치 합니다.")

    *위의 다른 하나의 브라우저를 배치합니다.*
8. 브라우저를 닫지 마세요. 다음 태스크에서 사용 됩니다.

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a>작업 2-를 사용 하 여 Zen HTML 요소를 만드는 코딩

**Zen 코딩** 는 고속 HTML, XML, XSL (또는 다른 구조적된 코드 형식)에 대 한 플러그 인을 코딩 하 고 편집 하는 편집기입니다. 이 플러그 인의 핵심은 HTML 코드에 지정 된 식을-CSS 선택기에 유사한 기능을 확장할 수 있는 강력한 약어 엔진입니다. Zen 코딩을 빠르게 CSS를 사용 하 여 HTML 스타일 선택기 구문을 작성 합니다.

이 연습에서는 질문의 옵션을 나타내는 HTML 단추를 생성 하려면 Web Essentials 제공한 Zen 코딩 기능을 사용 합니다.

1. Visual Studio로 다시 전환 합니다.
2. 엽니다는 **Index.cshtml** 에 있는 파일을 **뷰** | **홈** 폴더.
3. 대체는 **&lt;!-TODO: 옵션-추가&gt;** 키를 눌러에 고 다음 코드를 사용 하 여 주석을 **탭**합니다.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. 코드를 HTML로 확장 해야 합니다.

    ![HTML 확장](visual-studio-2013-web-tools/_static/image6.png "HTML 확장")

    *확장 된 HTML*

    > [!NOTE]
    > Zen 코딩 구문에 대 한 자세한 내용은 다음을 참조 하세요 [문서](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)합니다.
5. 클릭 합니다 **연결 된 브라우저 새로 고침** 두 브라우저를 업데이트 하는 단추입니다.

    ![연결 된 브라우저를 새로 고칠](visual-studio-2013-web-tools/_static/image7.png "연결 된 브라우저를 새로 고칩니다.")

    *연결 된 브라우저를 새로 고칩니다.*

    ![네 개의 단추를 사용 하 여 Internet Explorer-페이지가 업데이트](visual-studio-2013-web-tools/_static/image8.png "네 개의 단추를 사용 하 여 Internet Explorer-페이지 업데이트")

    *네 개의 단추를 사용 하 여 Internet Explorer-페이지 업데이트*

    ![Google Chrome-네 개의 단추를 사용 하 여 업데이트 된 페이지](visual-studio-2013-web-tools/_static/image9.png "네 개의 단추를 사용 하 여 Google Chrome-페이지 업데이트")

    *네 개의 단추를 사용 하 여 Google Chrome-페이지 업데이트*
6. Visual Studio로 다시 전환 합니다.
7. 페이지로 단추 추가 했지만 여전히 템플릿 질문을 추가 해야 합니다. 이렇게 하려면 새로운 기능에서에서 사용할 호출 Web Essentials **Lorem ipsum은 1500 년대 생성기**합니다. 찾을 합니다 **div** 요소를 **클래스** 특성 **프런트**합니다.
8. 다음 코드의 첫 번째 자식 요소로 추가 합니다 **div**, 누릅니다 **탭**합니다.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. 코드를 HTML로 확장 해야 합니다.

    ![Lorem ipsum은 1500 년대 자동으로 생성](visual-studio-2013-web-tools/_static/image10.png "Lorem ipsum은 1500 년대 자동 생성")

    *Lorem ipsum은 1500 년대 자동 생성*

    > [!NOTE]
    > Zen 코딩의 일부로, HTML 편집기에서 직접 이제 Lorem ipsum은 1500 년대 코드를 생성할 수 있습니다. 입력 **lorem** 누릅니다 **탭** 30 Lorem Ipsum 삽입할 텍스트를 word 및 합니다. 예: *lorem10* 10 Lorem ipsum은 1500 년대 단어를 삽입 합니다.
10. Web Essentials 라는 다른 새 기능을 사용 하 여 질문의 맨 위에 있는 로고를 추가 합니다 **Lorem 픽셀 생성기**합니다. 다음 코드의 첫 번째 자식 요소로 추가 합니다 **div** 요소 **컨테이너** 으로 **클래스** 값 및 키를 눌러 **탭**합니다.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. 코드를 HTML로 확장 해야 합니다.

    ![자동 생성 된 Lorem 픽셀](visual-studio-2013-web-tools/_static/image11.png "Lorem 픽셀 자동 생성")

    *Lorem 픽셀 자동 생성*

    > [!NOTE]
    > Zen 코딩의 일부로, HTML 편집기에서 직접 Lorem 픽셀 코드를 생성할 수도 있습니다. 입력 **pix-200x200-동물** 누릅니다 **탭** 및 **img** animal의 200x200 이미지를 사용 하 여 태그를 삽입 됩니다. 자세한 내용은 참조 [Lorem 픽셀](http://www.lorempixel.com)합니다.
12. 클릭 합니다 **연결 된 브라우저 새로 고침** 두 브라우저를 업데이트 하는 단추입니다.

    ![Internet Explorer-자동으로 생성 된 이미지 및 텍스트](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer-자동으로 생성 된 이미지 및 텍스트")

    *Internet Explorer-자동으로 생성 된 이미지 및 텍스트*

    ![Google Chrome-자동으로 생성 된 이미지 및 텍스트](visual-studio-2013-web-tools/_static/image13.png "Google Chrome-자동으로 생성 된 이미지 및 텍스트")

    *Google Chrome-자동으로 생성 된 이미지 및 텍스트*

    > [!NOTE]
    > 코드 조각을 추가 하는 경우 이미지를 임의로 선택, 때문에 브라우저에 표시 된 이미지 달라질 수 있습니다.
13. 브라우저를 닫지 마세요. 다음 태스크에서 사용 됩니다.

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a>작업 3-스타일 속성을 업데이트 합니다.

이 태스크에서는 브라우저 링크를 사용할지 **검사 모드** 여기서 특정 DOM 요소는 생성 된 정확한 위치를 검색 하 고 다음 웹에서 제공 하는 색 선택기를 사용 하는 요소의 색 속성을 업데이트 하는 기능 Essentials입니다.

1. Internet Explorer 브라우저에서 키를 누릅니다 **CTRL** + **ALT** + **I** 검사 모드를 사용 하도록 설정 합니다.
2. 밝은 파란색 테두리가 위로 포인터를 이동 하 고 클릭 합니다.

    ![밝은 파란색 테두리가 위로 포인터를 이동](visual-studio-2013-web-tools/_static/image14.png "연한 파랑 테두리 위로 포인터를 이동 합니다.")

    *연한 파랑 테두리 위로 포인터를 이동합니다.*
3. Visual Studio로 다시 전환 합니다. 브라우저에서 선택한 HTML 요소 또한 선택 하는 방법 Visual Studio HTML 편집기에서 확인할 수 있습니다.

    ![Visual Studio HTML 편집기에서 선택한 HTML 요소](visual-studio-2013-web-tools/_static/image15.png "Visual Studio HTML 편집기에서 선택한 HTML 요소")

    *Visual Studio HTML 편집기에서 선택한 HTML 요소*
4. 이제 업데이트를 **front** 선택한 요소의 스타일을 변경 하기 위해 CSS 클래스입니다. 이렇게 하려면 키를 누릅니다 **CTRL** + **,** 열려는 합니다 **탐색** 검색 상자입니다. 형식 **site.css** 누릅니다 **ENTER** 파일을 엽니다.

    ![Site.css 파일을 열면](visual-studio-2013-web-tools/_static/image16.png "Site.css 파일 열기")

    *Site.css 파일 열기*
5. 키를 눌러 **CTRL** + **F** 형식과 **.flip containter.front** CSS 선택기를 찾으려고 합니다.
6. 색 편집기를 열고 클래스의 테두리 속성에 밝은 파란색 사각형을 클릭 합니다.

    ![색 선택기를 열어](visual-studio-2013-web-tools/_static/image17.png "색 편집기 열기")

    *색 편집기 열기*
7. 갈매기형 펼침 단추를 클릭 하 여 색 선택기를 확장 하 고 새 색을 선택 합니다.

    ![색 선택 확장](visual-studio-2013-web-tools/_static/image18.png "색 선택 확장")

    *색 선택 확장*
8. 키를 눌러 **CTRL** + **ALT** + **ENTER** 연결 된 브라우저를 새로 고쳐야 합니다.
9. Internet Explorer로 전환 하 고 테두리의 색 어떻게 변경 되었는지 확인 합니다.

    ![Internet Explorer-테두리 색이 업데이트](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer-테두리 색 업데이트")

    *Internet Explorer – 테두리 색 업데이트*
10. Google Chrome 전환한 테두리의 색 어떻게 변경 되었는지 확인 합니다.

    ![Google Chrome-테두리 색이 업데이트](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-테두리 색 업데이트")

    *Google Chrome-테두리 색 업데이트*
11. Visual Studio로 다시 전환 합니다.
12. 끝으로 이동 합니다 **Site.css** 파일 및 키를 눌러 **CTRL** + **F** 찾으려고를 **.btn** 선택기입니다.
13. 있음을 합니다 **-webkit 테두리 반지름** 속성 녹색에 밑줄이 표시 됩니다.

    ![-webkit 테두리 반지름 속성 btn 선택기](visual-studio-2013-web-tools/_static/image21.png "btn 선택기의-webkit 테두리 반지름 속성")

    *btn 선택기의-webkit 테두리 반지름 속성*
14. 캐럿을 배치 합니다 **-webkit 테두리 반지름** 속성입니다. 속성의 첫 번째 단어의 첫 문자 아래 파란색 선이 표시 됩니다. 이 **스마트 태그**합니다.
15. 키를 눌러 **CTRL** + **합니다.** 제안 메뉴를 열고 클릭 **표준 속성 (테두리 반지름) 누락 된 추가**합니다.

    ![추가 표준 속성 제안 누락](visual-studio-2013-web-tools/_static/image22.png "추가 표준 속성 제안이 없습니다.")

    *표준 속성 제안 누락 된 추가*
16. 합니다 **테두리 반지름** 속성 CSS 규칙을 자동으로 추가 됩니다.

    ![추가 표준 속성이 누락](visual-studio-2013-web-tools/_static/image23.png "없습니다. 추가 하는 표준 속성")

    *추가 표준 속성이 없습니다.*
17. 위로 포인터를 이동 합니다 **테두리 반지름** 속성을 표시 합니다 **브라우저 행렬 도구 설명**합니다. 합니다 **브라우저 행렬 도구 설명** 각 브라우저에 속성이 있는지를 보여 줍니다.

    ![브라우저 행렬 도구 설명](visual-studio-2013-web-tools/_static/image24.png "브라우저 행렬 도구 설명")

    *브라우저 행렬 도구 설명*
18. 값을 **테두리 반지름** 속성이 여전히 밑줄이 그어진 합니다. 경고 메시지를 보려면 값 위로 포인터를 이동 합니다.

    ![테두리 반지름 속성 값 경고](visual-studio-2013-web-tools/_static/image25.png "테두리 반지름 속성 값 경고")

    *테두리 반지름 속성 값 경고*
19. 단위를 제거 합니다 **테두리 반지름** 도구 설명에서 제안 된 속성 값입니다.
20. 으로 **테두리 반지름** 모퉁이 제거할 수 있습니다 어떻게 둥근된 테두리를 정의 하기 위한 표준 속성을 **-webkit 테두리 반지름** 속성과 CSS 규칙의 값입니다.
21. 캐럿을 배치 합니다 **자동 줄 바꿈** 속성 및 스마트 태그 아래도 표시 됩니다.
22. 메뉴를 열고 클릭 **누락 된 공급 업체의 세부 정보 추가**합니다.

    ![누락 된 공급 업체에 대 한 구체적인 제안 사항을 추가](visual-studio-2013-web-tools/_static/image26.png "누락 된 공급 업체에 대 한 구체적인 제안 사항을 추가")

    *누락 된 공급 업체에 대 한 구체적인 제안 사항을 추가합니다*
23. 합니다 **ms 단어 잘림** 속성 CSS 규칙을 자동으로 추가 됩니다.

    ![공급 업체 특정 속성 추가](visual-studio-2013-web-tools/_static/image27.png "공급 업체 특정 속성 추가")

    *공급 업체 특정 속성 추가*

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a>작업 4-브라우저에서 HTML 코드를 업데이트 하는 중

이 태스크에서는 브라우저 링크를 사용할지 **디자인 모드** 브라우저에서 DOM 개체를 편집 하 고 Visual Studio에서 HTML 소스 파일에 변경 내용을 전송 하는 기능입니다.

1. Google Chrome에서 키를 누릅니다 **CTRL** + **ALT** + **D** 디자인 모드를 사용 하도록 설정 합니다.
2. 위로 포인터를 이동 합니다 **Lorem Ipsum dolor sit amet** 레이블을 지정 하 고 클릭 합니다.

    ![편집 된 질문](visual-studio-2013-web-tools/_static/image28.png "질문 편집")

    *질문 편집*
3. 커서가 표시 됩니다. 원래 텍스트를 바꿉니다 *어떤 모습은 긴 질문을 작성 하는 경우?*, 누릅니다 **ESC** 디자인 모드를 종료 합니다.

    ![편집할 질문](visual-studio-2013-web-tools/_static/image29.png "질문 편집")

    *편집 된 질문*
4. Visual Studio를 다시 열고 스위치 **Index.cshtml**열려 있지 않으면, 합니다. 내부 텍스트를 **&lt;p&gt;** 요소가 업데이트 되었습니다.

    ![HTML 페이지에서 업데이트 된 질문](visual-studio-2013-web-tools/_static/image30.png "HTML 페이지에서 업데이트 된 질문")

    *HTML 페이지에서 업데이트 된 질문*

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a>작업 5-검토 SEO 관련 경고

**검색 엔진 최적화** (SEO)가 검색 엔진의 결과 목록에서 더 높은 웹 사이트 순위를 만드는 프로세스입니다. 사이트의 순위가 높을수록 더 일관 되 게 표시 됩니다, 그리고 자세한 방문자가 사이트는 검색 엔진에서 받습니다. Web Essentials HTML을 검사 하는 분석 도구를 통합, 보고서 문제를 발견 하 고 해결 지원을 제공 합니다.

1. 로 이동 합니다 **보기** 메뉴를 클릭 **오류 목록** 열려는 합니다 **오류 목록** 창.

    ![오류 목록 보기 메뉴](visual-studio-2013-web-tools/_static/image31.png "오류 목록 보기 메뉴에서")

    *오류 목록 보기 메뉴*
2. SEO을 알리는 경고를 하는 것을 볼 수는 **&lt;메타&gt;** 페이지 설명에 대 한 태그를 지정 합니다. SEO 경고 항목 수정을 두 번 클릭 합니다.

    ![오류 목록 창](visual-studio-2013-web-tools/_static/image32.png "오류 목록 창")

    *오류 목록 창*
3. 에 **Web Essentials** 대화 상자, 클릭 **예** 설명을 삽입할 &lt;메타&gt; 태그 합니다.

    ![Web Essentials 대화 상자](visual-studio-2013-web-tools/_static/image33.png "Web Essentials 대화 상자")

    *Web Essentials 대화 상자*
4. 에 대 한 편집기  **\_Layout.cshtml** 열립니다 및 **&lt;메타&gt;** 태그에 자동으로 추가 됩니다는 **헤드** 섹션은 HTML 파일입니다.

    ![(_L) 페이지에 자동으로 추가 하는 메타 태그](visual-studio-2013-web-tools/_static/image34.png "Meta 태그 (_l) 페이지에 자동으로 추가")

    *Meta 태그에 자동으로 추가 \_레이아웃 페이지*
5. 값을 변경 합니다 **콘텐츠** 특성을 *GeekQuiz* 파일을 저장 합니다.

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a>연습 2: 코드 조각 및 IntelliSense를 활용 하 고

Web Essentials를 사용 하 여 HTML 편집기는 추가 기능을 사용 하 여 확장 되었습니다. 이 연습에서는 웹 응용 프로그램을 개발할 때 도움이 되는 몇 가지 새 기능이 표시 됩니다.

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a>작업 1-HTML 문서에 IntelliSense 사용

이 작업에 나타나는 첫 번째 새로운 기능은 이라고 **동적 IntelliSense**합니다. 동적 IntelliSense 다른 태그 및 사용 가능한 id를 유추 하는 특성을 읽습니다.

이 태스크에서는 레이블 및 입력된 필드를 포함 하는 새 HTML 폼 요소를 만들게 됩니다. 다음 추가 됩니다는 **에 대 한** 레이블에 입력을 바인딩할 특성 범위에서 입력의 id를 기반으로 하는 IntelliSense 제안 표시 됩니다.

1. 열기 **Visual Studio Express 2013 for Web** 하며 **Begin.sln** 솔루션에는 **소스/e x 2-TakingAdvantageofCodeSnippetsandIntelliSense/시작** 폴더입니다. 또는 계속할 수 있습니다 솔루션을 사용 하 여 이전 연습에서 얻은.
2. **솔루션 탐색기**오픈를 **Index.cshtml** 에 있는 파일을 **뷰** | **홈** 폴더.
3. 내에서 다음 폼을 추가 합니다 **&lt;섹션&gt;** 요소입니다.

    (코드 조각- *VisualStudio2013WebTooling* - *e x 2* - *폼*)

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. 입력된 태그 앞에 일부 설명은 필드를 사용 하 여 레이블이 있어야 합니다. 입력된 태그 앞에 다음 레이블을 추가 합니다.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. 합니다 **에 대 한** 특성을 **&lt;레이블&gt;** 레이블 a는 폼 요소에 바인딩되어 지정 합니다. 관련 요소의 id 특성의 값 같아야 합니다. 추가 된 **에 대 한** 특성을 합니다 **&lt;레이블&gt;** 요소입니다. 다음 그림에 표시 된 대로 합니다 &quot;이름을&quot; 값 팝업 IntelliSense 상자에서 동일한 범위 내 요소의 id를 기준으로 (바깥쪽  **&lt;폼&gt;**).

    ![IntelliSense의 id를 보여 주는](visual-studio-2013-web-tools/_static/image35.png "IntelliSense에서 id를 표시 합니다.")

    *IntelliSense에서 id를 표시합니다.*
6. 최근에 추가 된 삭제할 **&lt;양식&gt;** 요소 및 해당 콘텐츠입니다.

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a>작업 2-HTML 코드 조각을 사용 하 여

HTML5 25 개 이상의 새 의미 체계 태그를 소개 했습니다. Visual Studio에는 이미 이러한 태그에 대 한 IntelliSense 지원 하지만 Visual Studio 2013을 사용 하면 빠르고 쉽게 새 코드 조각을 추가 하 여 태그를 작성할 수 있습니다. 에 대 한 올바른 코덱이 대체를 추가 하는 등의 몇 가지 작은 미묘한 함께 제공 되는 이러한 태그를 복잡 한 없는 경우에 *오디오* 태그입니다. 이 태스크에서는 오디오 태그에 대 한 HTML 코드 조각을 표시 됩니다.

1. 에 **Index.cshtml** 파일을 입력  **&lt;aud** 내는 **&lt;섹션&gt;** 다음 그림에 표시 된 대로 요소.

    ![오디오 요소를 삽입할](visual-studio-2013-web-tools/_static/image36.png "audio 요소 삽입")

    *Audio 요소 삽입*
2. 키를 눌러 **탭** 두 번 페이지에서 다음 코드는 추가 하는 방법 및 커서에 배치 됩니다 합니다 **src** 특성 첫 번째 소스입니다.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > 키를 눌러 합니다 **탭** 키를 두 번 코드 조각 삽입 됩니다. 오디오 조각의 표준 사용이 표시는 *오디오* 지원 향상된에 대 한 두 개의 소스 파일을 사용 하 여 태그입니다.
3. 두 번째 줄을 삭제 하 고 WebCampsTV Katana 표시 하려면 다음 링크를 사용 하 여 첫 번째 줄의 소스를 업데이트 합니다. [ http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3 ](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)합니다. 결과 코드는 다음과 같습니다.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > 소스 파일 *KatanaProject.mp3* 예제로 사용 됩니다. 원하는 경우 다른 소스를 사용할 수 있습니다.
4. 키를 눌러 **CTRL** + **S** 파일을 저장 합니다.
5. 키를 눌러 **CTRL** + **F5** 응용 프로그램을 시작 합니다.
6. 응용 프로그램에는 오디오 플레이어가 추가 되었는지 확인 합니다.

    ![Internet Explorer에서 오디오 플레이어](visual-studio-2013-web-tools/_static/image37.png "Internet Explorer에서 오디오 플레이어")

    *Internet Explorer에서 오디오 플레이어*

    ![Google Chrome에서 오디오 플레이어](visual-studio-2013-web-tools/_static/image38.png "Google Chrome에서 오디오 플레이어")

    *Google Chrome에서 오디오 플레이어*
7. 브라우저를 닫지 마세요. 다음 태스크에서 사용 됩니다.

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a>작업 3-JavaScript 문서의 IntelliSense 사용

Web Essentials 2013을 사용 하 여 스타일 시트 및 HTML 페이지에 클래스 이름과 Id의 목록을 생성합니다. 이 태스크에서는 해당 목록의 Web Essentials 2013의 JavaScript IntelliSense 지원 개선 하는 방법을 배웁니다.

1. 에 **Index.cshtml** 파일을 정의 하는 다음 코드를 추가 **스크립트** JavaScript 코드에 대 한 태그입니다.

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. 안에 다음 코드를 추가 합니다 **스크립트** 준비 콜백 함수를 정의 하는 태그입니다.

    (코드 조각- *VisualStudio2013WebTooling* - *e x 2* - *ReadyFunction*)

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. 캐럿을 배치 합니다 **스크립트** 태그 및 키를 눌러 **CTRL** + **합니다.** 제안 메뉴를 엽니다.
4. 클릭 **파일에 추출**합니다.

    ![JavaScript 파일 제안 추출할](visual-studio-2013-web-tools/_static/image39.png "JavaScript 파일 제안 추출")

    *JavaScript 파일 제안 추출*
5. 에 **다른 이름으로 저장** 창에서를 **스크립트** 폴더, 파일 이름 **init.js** 클릭 **저장**합니다.

    ![다른 이름으로 저장 창](visual-studio-2013-web-tools/_static/image40.png "창 이름으로 저장")

    *다른 이름으로 저장 창*

    > [!NOTE]
    > 합니다 **init.js** 파일을 만들고 스크립트의 콘텐츠 파일로 이동 합니다.
    > 
    > ![포함 된 콘텐츠를 사용 하 여 만든 Init.js 파일](visual-studio-2013-web-tools/_static/image41.png "포함 된 콘텐츠를 사용 하 여 만든 Init.js 파일")
    > 
    > *포함 된 콘텐츠를 사용 하 여 만든 Init.js 파일*
6. 엽니다는 **Index.cshtml** 파일 및 스크립트 태그에 대 한 참조로 교체 되었습니다 있는지 확인 합니다 **init.js** 파일.

    ![Html에 대 한 참조 Init.js](visual-studio-2013-web-tools/_static/image42.png "Init.js html 참조")

    *Init.js html 참조*
7. 로 이동 합니다 **솔루션 탐색기** 알 수 있습니다는 **init.js** 파일이 솔루션에 자동으로 포함 되었습니다.

    ![솔루션에 포함 된 Init.js 파일](visual-studio-2013-web-tools/_static/image43.png "솔루션에 포함 된 Init.js 파일")

    *솔루션에 포함 된 Init.js 파일*
8. 다시 전환 합니다 **init.js** 업데이트할 파일의 **준비** 콜백 함수.
9. 에 전달 되는 함수 콜백 정의 안에 *준비*, 특정 클래스 특성으로 요소를 모두 가져오려면 다음 코드를 추가 합니다.

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. 키를 눌러 **CTRL** + **공간** 내에서 열의 큰따옴표 사이 **getElementsByClassName** 함수 호출 합니다.

    ![GetElementsByClassName 함수에 대 한 IntelliSense를 보여 주는](visual-studio-2013-web-tools/_static/image44.png "getElementsByClassName 함수에 대 한 IntelliSense 표시")

    *GetElementsByClassName 함수에 대 한 IntelliSense 표시*

    > [!NOTE]
    > IntelliSense 프로젝트 스타일 시트에 정의 된 클래스에 표시 되는지 확인 합니다.
11. 다음 코드를 사용 하 여 만든 줄을 대체 합니다.

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. 뒤에 커서를 놓습니다 **au** 에서 따옴표 안의 합니다 **getElementsByTagName** 함수 및 키를 눌러 **CTRL** + **공간**.

    ![GetElementByTagName 메서드에 대 한 IntelliSense를 보여 주는](visual-studio-2013-web-tools/_static/image45.png "getElementByTagName 메서드에 대 한 IntelliSense 표시")

    *GetElementsByTagName 메서드를 보여 주는 IntelliSense*
13. 선택 **&quot;오디오&quot;** 목록에서 키를 눌러 **ENTER**합니다. 결과는 다음 그림에 나와 있습니다.

    ![오디오 요소 검색](visual-studio-2013-web-tools/_static/image46.png "오디오 요소 검색")

    *오디오 요소 검색*
14. **솔루션 탐색기**, 마우스 오른쪽 단추로 클릭 합니다 **init.js** 파일을 **스크립트** 폴더를 선택 **축소 JavaScript 파일** 에서 **Web Essentials** 메뉴.

    ![JavaScript 파일을 축소](visual-studio-2013-web-tools/_static/image47.png "축소 JavaScript 파일")

    *JavaScript 파일을 축소*
15. 원본 파일이 변경 클릭 자동 축소를 사용 하도록 설정 하 라는 메시지가 나타나면 **예**합니다.

    ![자동 축소 경고를 사용 하도록 설정](visual-studio-2013-web-tools/_static/image48.png "자동 축소 경고를 사용 하도록 설정")

    *자동 축소 경고를 사용 하도록 설정*

    > [!NOTE]
    > 합니다 **init.min.js** 만들어지고의 종속성으로 추가 되는 **init.js** 파일입니다.
    > 
    > ![Init.min.js 파일 생성](visual-studio-2013-web-tools/_static/image49.png "Init.min.js 파일 생성")
    > 
    > *Init.min.js 파일 생성*
16. 엽니다는 **init.min.js** 파일 및 파일 축소는 알 수 있습니다.

    ![파일 콘텐츠 Init.min.js](visual-studio-2013-web-tools/_static/image50.png "Init.min.js 파일 콘텐츠")

    *Init.min.js 파일 콘텐츠*
17. **init.js** 파일을 아래에 다음 코드를 추가 합니다 **getElementsByTagName** 모든 오디오 요소를 재생 하려면 호출 함수.

    (코드 조각- *VisualStudio2013WebTooling* - *e x 2* - *PlayAudioElements*)

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. 클릭 **CTRL** + **S** 파일을 저장 합니다. 축소 된 파일이 이미 열려 있으므로 소스 편집기 외부에서 파일을 수정한 하 라는 대화 상자가 표시 됩니다. **예**를 클릭합니다.

    ![Microsoft Visual Studio 경고](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio 경고")

    *Microsoft Visual Studio 경고*
19. 으로 전환 합니다 **init.min.js** 파일을 새 코드를 사용 하 여 파일 업데이트 되었는지 확인 합니다.

    ![Init.min.js 파일 업데이트](visual-studio-2013-web-tools/_static/image52.png "Init.min.js 파일 업데이트")

    *Init.min.js 파일 업데이트*
20. 클릭 합니다 **브라우저 링크 새로 고침** 단추입니다.
21. 두 브라우저 새로 고쳐집니다 이전 태스크에서 확인 했던 오디오 플레이어를 자동으로 재생 되기 시작 됩니다.

    ![보기에 포함 하는 오디오 플레이어](visual-studio-2013-web-tools/_static/image53.png "보기에 포함 하는 오디오 플레이어")

    *보기에 포함 하는 오디오 플레이어*

* * *

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습을 완료 하 여 배웠습니다 방법:

- 풍부한 HTML5 코드 조각 및 Zen 코딩 등 Web Essentials에 포함 된 새 HTML 편집기 기능 사용
- 색 선택 및 브라우저 행렬 도구 설명 등 Web Essentials에 포함 된 새 CSS 편집기 기능 사용
- 모든 HTML 요소에 대 한 IntelliSense 파일을 추출 등 Web Essentials에 포함 된 새 JavaScript 편집기 기능 사용
- 브라우저와 브라우저 링크를 사용 하 여 Visual Studio 간에 Exchange 데이터
