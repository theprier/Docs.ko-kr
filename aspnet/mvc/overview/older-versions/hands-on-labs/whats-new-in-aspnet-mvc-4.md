---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: ASP.NET MVC 4의에서 새로운 기능 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4는 체계적인 디자인 패턴 및 ASP.NET의 기능을 사용 하 여 확장성이 뛰어난 표준 기반 웹 응용 프로그램을 빌드하기 위한 프레임 워크 및...
ms.author: aspnetcontent
ms.date: 02/18/2013
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 718a31de3d2d60788ba4affb0463a4ae871ef89a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37805352"
---
# <a name="whats-new-in-aspnet-mvc-4"></a>ASP.NET MVC 4의에서 새로운 기능

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트 다운로드](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 4는 체계적인 디자인 패턴 및 ASP.NET 및.NET framework의 기능을 사용 하 여 확장성이 뛰어난 표준 기반 웹 응용 프로그램을 빌드하기 위한 프레임 워크입니다. 이 새로운, 네 번째 버전의 framework 모바일 웹 응용 프로그램 개발을 더 쉽게에 중점을 둡니다.

시작 하려면 새 ASP.NET MVC 4 프로젝트를 만들 때 이제 됩니다 모바일 응용 프로그램 프로젝트 템플릿을 특히 모바일 장치에 대 한 독립 실행형 앱을 빌드하는 동안 사용할 수 있습니다. 또한 ASP.NET MVC 4는 jQuery Mobile jQuery.Mobile.MVC NuGet 패키지를 통해와 통합 됩니다. jQuery Mobile는 등 Windows Phone, iPhone, Android를 비롯 한 모든 인기 있는 모바일 장치 플랫폼에 호환 되는 웹 앱 개발을 위한 HTML5 기반 프레임 워크입니다. 그러나 특수화를 해야 하는 경우 ASP.NET MVC 4 수 있습니다 다른 장치에 대 한 서로 다른 뷰를 제공 하 고 장치별 최적화를 제공 합니다.

이 실습 랩에서 ASP.NET MVC 4를 사용 하 여 시작 합니다 &quot;인터넷 응용 프로그램&quot; 사진 갤러리 응용 프로그램을 만들기 위한 프로젝트 템플릿. JQuery Mobile 및 ASP.NET MVC 4의 새로운 기능을 사용 하 여 다양 한 모바일 장치 및 데스크톱 웹 브라우저와 호환 되도록 앱을 점진적으로 향상 됩니다. 코드 생성 및 방법을 ASP.NET MVC 4 쉽게 작업을 지원 하 여 비동기 동작 메서드를 쓸 수에 대 한 새 코드 작성법에 대해서도 배웁니다&lt;ActionResult&gt; 형식을 반환 합니다.

> [!NOTE]
> 웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다. 이 랩에 특정 프로젝트에서 제공 됩니다 [What's New in ASP.NET 4.5에서 Web Forms](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)합니다.

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 학습할 방법:

- 향상 된 기능을 ASP.NET MVC 프로젝트 템플릿을 포함 한 새 모바일 응용 프로그램 프로젝트 템플릿을 활용합니다
- HTML5 사용 하 여 뷰포트 특성 및 모바일 장치의 디스플레이 향상 시키기 위해 CSS 미디어 쿼리
- JQuery Mobile 터치에 최적화 된 웹 UI를 구축 하기 위한 점진적 향상 된 기능을 사용 하 여
- 모바일 전용 뷰 만들기
- 전환기 뷰 구성 요소를 사용 하 여 응용 프로그램에서 모바일 및 데스크톱 뷰 사이 전환 하려면
- 작업을 사용 하 여 비동기 컨트롤러 만들기

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽을 [부록 B](#AppendixB) 설치 하는 방법에 대 한 지침은).
- [ASP.NET MVC 4](../../../mvc4.md) (Microsoft Visual Studio 2012 설치에 포함)
- Windows Phone 에뮬레이터 (에 포함 된 [7.1.1 Windows Phone SDK](https://www.microsoft.com/download/details.aspx?id=29233))
- 선택 사항- [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) 사용 하 여 **Electric Plum iPhone 시뮬레이터** (iPhone 시뮬레이터가 사용 하 여 웹 응용 프로그램을 탐색 하는 데 사용 되는 연습 3)에 확장

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>설정

랩 문서 전체에서 코드 블록을 삽입할 지시 됩니다. 사용자 편의 위해 해당 코드의 대부분은 수동으로 추가할 필요가 없도록 하려면 Visual Studio 내에서 사용할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.

설치 하려면 코드 조각:

1. Windows 탐색기 창을 열고 랩의 이동할 **Source\Setup** 폴더입니다.
2. 두 번 클릭 합니다 **Setup.cmd** Visual Studio 코드 조각은 설치 하려면이 폴더의 파일입니다.

이 문서의 부록 참조할 수 있습니다 사용 하는 방법을 알아보려면 원하는 고 Visual Studio 코드 조각을 사용 하 여 잘 모르는 경우 &quot; [부록 a: 사용 하 여 코드 조각](#AppendixA)&quot;합니다.

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습에 포함 됩니다.

1. [새 ASP.NET MVC 4 프로젝트 템플릿](#Exercise1)
2. [사진 갤러리 웹 응용 프로그램 만들기](#Exercise2)
3. [모바일 장치에 대 한 지원 추가](#Exercise3)
4. [비동기 컨트롤러를 사용 하 여](#Exercise4)

> [!NOTE]
> 각 실습 동반 되는 **최종** 연습을 완료 한 후 가져와야 결과 솔루션이 포함 된 폴더입니다. 이 연습을 진행 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.


이 랩을 완료 하기 위한 예상 시간: **60 분**합니다.

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a>연습 1: 새 ASP.NET MVC 4 프로젝트 템플릿

이 연습에서는 ASP.NET MVC 4 프로젝트 템플릿에서 향상 된 기능을 살펴봅니다. 인터넷 응용 프로그램 템플릿 외에 MVC 3에서 이미이 버전 이제 모바일 응용 프로그램에 대 한 별도 템플릿에 합니다. 먼저 템플릿의 각 관련 기능의 일부 보면 됩니다. 그런 다음 작업할 적합 한 접근 방식을 사용 하 여 다른 플랫폼에서 올바르게 페이지를 렌더링 합니다.

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a>작업 1-인터넷 응용 프로그램 템플릿 탐색

1. 오픈 **Visual Studio**합니다.
2. 선택 된 **파일 | 새 | 프로젝트** 메뉴 명령입니다. 에 **새 프로젝트** 대화 상자에서 선택 된 **Visual C# | 웹** 왼쪽된 창에서 템플릿을 선택한 트리의 **ASP.NET MVC 4 웹 응용 프로그램입니다.** 프로젝트 이름을 **PhotoGallery**, 선택 위치 (또는 기본값)를 클릭 하 고 **확인**합니다.

    > [!NOTE]
    > 이제 만들려는 PhotoGallery ASP.NET MVC 4 솔루션 나중에 사용자 지정 합니다.

    ![새 프로젝트를 만드는](whats-new-in-aspnet-mvc-4/_static/image1.png "새 프로젝트 만들기")

    *새 프로젝트 만들기*
3. 에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 선택 합니다 **인터넷 응용 프로그램** 프로젝트 템플릿 및 클릭 **확인**합니다. Razor 뷰 엔진으로 선택 했는지 확인 합니다.

    ![새 ASP.NET MVC 4 인터넷 응용 프로그램을 만드는](whats-new-in-aspnet-mvc-4/_static/image2.png "새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기")

    *새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기*

    > [!NOTE]
    > ASP.NET MVC 3에서 razor 구문이 도입 되었습니다. 해당 목표 문자와 유체 워크플로 코딩을 빠르게 사용 하도록 설정 하면 파일에 필요한 키 입력 횟수를 최소화 하는 것입니다. Razor를 활용 하 여 기존 C# / VB (또는 다른) 언어 실력 하 고 멋진 HTML 생성 워크플로 가능 하 게 하는 템플릿 태그 구문을 제공 합니다.
4. 키를 눌러 **F5** 솔루션을 실행 하 여 갱신 된 템플릿을 참조 하세요. 다음 기능을 사용해 확인할 수 있습니다.

    **최신 스타일 템플릿**

    템플릿은 갱신 되 었어야, 더 많은 최신 스타일을 제공 합니다.

    ![ASP.NET MVC 4 맞게 스타일을 다시 템플릿을](whats-new-in-aspnet-mvc-4/_static/image3.png "맞게 템플릿 스타일을 다시 MVC 4")

    *ASP.NET MVC 4 맞게 스타일을 다시 템플릿*

    ![새 연락처 페이지](whats-new-in-aspnet-mvc-4/_static/image4.png "새 연락처 페이지")

    *새 연락처 페이지*

    **적응형 렌더링**

    브라우저 창의 크기를 조정 확인 하 고 페이지 레이아웃 새 창 크기를 동적으로 조정 하는 방법을 확인할 수 있습니다. 이러한 템플릿은 적응형 렌더링 기술의 사용 하 여 사용자 지정 하지 않고 데스크톱 및 모바일 플랫폼에서 올바르게 렌더링 합니다.

    ![다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿은](whats-new-in-aspnet-mvc-4/_static/image5.png "다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿")

    *다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿*

    **JavaScript 사용 하 여 보다 풍부한 UI**

    또 다른 개선 사항은 기본 프로젝트 템플릿에 좀 더 대화형 JavaScript를 제공 하는 JavaScript의 사용입니다. 템플릿에서 사용 되는 로그인 및 등록 링크를 클라이언트 쪽에서 입력된 필드의 유효성을 검사 하려면 jQuery 유효성 검사를 사용 하는 방법을 보여 줍니다.

    ![jQuery 유효성 검사](whats-new-in-aspnet-mvc-4/_static/image6.png)

    *jQuery 유효성 검사*

    > [!NOTE]
    > 두 섹션에서는 첫 번째 섹션에서 로그인 하는 알림 altenativelly google (기본적으로 사용 안 함)와 같은 다른 인증 서비스를 사용 하 여 로그인 하면 두 번째 섹션에 사이트에서 등록 계정으로 기록할 수 있습니다.
5. 디버거를 중지 하 고 Visual Studio로 돌아가서 브라우저를 닫습니다.
6. 파일을 엽니다 **AuthConfig.cs** 아래에 **앱\_시작** 폴더입니다.
7. Google 클라이언트를 등록 하려면 마지막 줄에서 주석 제거 *OAuth* 인증 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > Facebook, Twitter, Microsoft 등 모든 OAuth 또는 OpenID 서비스를 사용 하 여 인증을 쉽게 설정할 수 있습니다. 알 수 있습니다.
8. 키를 눌러 **F5** 솔루션을 실행 하 여 로그인 페이지로 이동 합니다.
9. 선택 **Google** 서비스에 로그인 합니다.

    ![서비스에서 로그 선택](whats-new-in-aspnet-mvc-4/_static/image7.png)

    *서비스에서 로그 선택*
10. Google 계정으로 로그인 합니다.
11. Google 계정에서 정보를 검색할 사이트 (localhost)를 허용 합니다.
12. 마지막으로, Google 계정을 연결 하려면 사이트에 등록 해야 합니다.

   ![Google 계정 연결](whats-new-in-aspnet-mvc-4/_static/image8.png)

   *Google 계정 연결*
13. 디버거를 중지 하 고 Visual Studio로 돌아가서 브라우저를 닫습니다.
14. 이제 프로젝트 템플릿에서 ASP.NET MVC 4에서 도입 된 일부 다른 새 기능을 확인 하는 솔루션을 탐색 합니다.

   ![ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿을](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿")

   *ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿*

   - **HTML 5 태그**

       새 테마 태그를 확인 하려면 템플릿 뷰를 찾습니다.

       ![Razor 및 HTML5 태그 About.cshtml를 사용 하 여 새 템플릿. ](whats-new-in-aspnet-mvc-4/_static/image10.png "About.cshtml Razor 및 HTML5 태그를 사용 하 여 새 서식 파일입니다.")

       *HTML5 및 Razor 태그 (About.cshtml)를 사용 하 여 새 템플릿.*
   - **업데이트 된 JavaScript 라이브러리**

       KnockoutJS, 풍부한 만들 수 있는 JavaScript MVVM 프레임 워크 및 JavaScript 및 HTML을 사용 하 여 응답성이 뛰어난 웹 응용 프로그램에 이제 ASP.NET MVC 4 기본 템플릿이 포함 되어 있습니다. 같은 mvc 3, jQuery 및 jQuery UI 라이브러리도 포함 되어 ASP.NET MVC 4입니다.

     > [!NOTE]
     > 이 링크에 KnockOutJS 라이브러리에 대 한 자세한 정보를 얻을 수 있습니다: [ [ http://learn.knockoutjs.com/ ](http://learn.knockoutjs.com/) ](http://learn.knockoutjs.com/)합니다. 또한 jQuery 및 jQuery UI에 대해 알아볼 수 있습니다에 [ [ http://docs.jquery.com/ ](http://docs.jquery.com/) ](http://docs.jquery.com/)합니다.

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a>작업 2-모바일 응용 프로그램 템플릿 탐색

ASP.NET MVC 4 웹 사이트에 모바일 및 태블릿 브라우저의 개발을 용이 하 게 합니다. 이 템플릿은 인터넷 응용 프로그램 템플릿 (이때 컨트롤러 코드 실질적으로 동일)와 동일한 응용 프로그램 구조를 갖지만 해당 스타일 터치 기반 모바일 장치에서 제대로 렌더링 하도록 수정 되었습니다.

1. 선택 된 **파일 | 새 | 프로젝트** 메뉴 명령입니다. 에 **새 프로젝트** 대화 상자에서 선택 된 **Visual C# | 웹** 왼쪽된 창에서 템플릿을 선택한 트리에 **ASP.NET MVC 4 웹 응용 프로그램입니다.** 프로젝트 이름을 **PhotoGallery.Mobile**, 위치를 선택 (또는 기본값) 선택 &quot;솔루션에 추가할&quot; 클릭 **확인**합니다.
2. 에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 선택 합니다 **모바일 응용 프로그램** 프로젝트 템플릿 및 클릭 **확인**합니다. Razor 뷰 엔진으로 선택 했는지 확인 합니다.

    ![새 ASP.NET MVC 4 모바일 응용 프로그램을 만드는](whats-new-in-aspnet-mvc-4/_static/image11.png "새 ASP.NET MVC 4 모바일 응용 프로그램 만들기")

    *새 ASP.NET MVC 4 모바일 응용 프로그램 만들기*
3. 이제 솔루션을 탐색 하 고 일부의 mobile에 대 한 ASP.NET MVC 4 솔루션 템플릿을 통해 도입 된 새로운 기능 확인을 수행할 수 있습니다.

    - **jQuery Mobile 라이브러리**

        모바일 응용 프로그램 프로젝트 템플릿에 오픈 소스 라이브러리인 모바일 브라우저 호환성을 위해 jQuery Mobile 라이브러리를 포함 합니다. jQuery Mobile에는 CSS 및 JavaScript를 지 원하는 모바일 브라우저에 점진적인 기능 향상 적용 됩니다. 점진적인 기능 향상만 가장 강력한 브라우저 풍부한 콘텐츠를 표시할 수 있도록 하는 동안 웹 페이지의 기본 콘텐츠를 표시 하는 모든 브라우저를 수 있습니다. Jquery 모바일 스타일을 포함 하는 JavaScript 및 CSS 파일에는 페이지 태그에서 전혀 변경 하지 않고 콘텐츠를 화면에 맞게 모바일 브라우저 데 도움이 됩니다.

        ![jQuery-mobile-library-included-in-the-template](whats-new-in-aspnet-mvc-4/_static/image12.png)

        *템플릿에 포함 된 jQuery mobile 라이브러리*
    - **HTML5 기반 태그**

        ![Mobile-application-template-using-HTML5-markup](whats-new-in-aspnet-mvc-4/_static/image13.png)

        *HTML5 태그, (Login.cshtml 및 index.cshtml)를 사용 하 여 모바일 응용 프로그램 템플릿*
4. 키를 눌러 **F5** 솔루션을 실행 합니다.
5. 엽니다는 **Windows Phone 7 에뮬레이터**합니다.
6. Phone 시작 화면에서 Internet Explorer를 엽니다. 데스크톱 응용 프로그램의 시작 위치 URL을 확인 하 고 휴대폰에서 해당 URL로 이동 (예: `http://localhost:[PortNumber]/`).
7. 로그인 페이지를 입력 하거나 체크 아웃 수 있다면 이제는 페이지에 대 한 합니다. 웹 사이트의 스타일 mobile에 대 한 새 Metro 앱은 기반으로 한다는 것을 확인 합니다. ASP.NET MVC 4 프로젝트 템플릿 페이지의 모든 요소는 표시 되 고 사용할 수 있도록 모바일 장치에서 제대로 표시 됩니다. 헤더에서 링크를 클릭 하거나 탭 할 충분 한 크기는 알 수 있습니다.

    ![모바일 장치에서 템플릿 페이지 프로젝트](whats-new-in-aspnet-mvc-4/_static/image14.png "템플릿 페이지에서 모바일 장치 프로젝트")

    *모바일 장치에서 프로젝트 템플릿 페이지*
8. 새 템플릿을 사용 하 여도 합니다 **뷰포트 meta 태그**합니다. 대부분의 모바일 브라우저에는 가상 브라우저 창의 너비를 정의 하거나 &quot;뷰포트&quot;, 모바일 장치의 실제 너비 보다 큰 시간 세분화 합니다. 따라서 모바일 브라우저를 가상 표시 내의 전체 웹 페이지를 표시할 수 있습니다. 합니다 **뷰포트 meta 태그** 웹 개발자가 모바일 장치의 너비, 높이 및 브라우저 영역의 규모를 설정 하려면 **합니다.** 장치 너비 뷰포트를 설정 하는 모바일 응용 프로그램에 대 한 ASP.NET MVC 4 템플릿 (&quot;너비 = 장치&quot;) 레이아웃 템플릿에 (*Views\Shared\_Layout.cshtml*)는 모든 합니다 페이지에는 해당 뷰포트 장치 화면 너비를 설정 해야 합니다. 알림 뷰포트 메타 태그 기본 브라우저 보기를 변경 되지 것입니다.
9. 오픈  **\_Layout.cshtml**에 있는 **보기 | 공유** 폴더 및 주석 뷰포트 메타 태그입니다. 응용 프로그램을 실행 합니다. 그렇지 않은 경우 이미 열리고 차이점을 확인 합니다.


[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

![뷰포트 meta 태그를 주석 처리 한 후 사이트](whats-new-in-aspnet-mvc-4/_static/image15.png "뷰포트 meta 태그를 주석 처리 한 후 사이트")

*뷰포트 meta 태그를 주석 처리 한 후 사이트*
10. Visual Studio에서 눌러 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.
11. 뷰포트 meta 태그 주석 처리를 제거 합니다.


[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a>작업 3-적응형 렌더링을 사용 하 여

이 태스크에서는 사용자 지정 하지 않고 동시에 모바일 장치 및 웹 브라우저에서 올바르게 웹 페이지를 렌더링 하는 다른 방법에 배웁니다. 이미 비슷한 용도로 사용 하 여 뷰포트 meta 태그를 사용 했습니다. 다른 강력한 방법을 충족 하는 이제: *적응형 렌더링*합니다.

사용 하는 방법은 적응형 렌더링 **CSS3 미디어 쿼리** 페이지에 적용 되는 스타일을 사용자 지정할 수 있습니다. 미디어 쿼리에 특정 조건에서 CSS 스타일을 그룹화 하 여 스타일 시트를 내부에 조건을 정의 합니다. 조건이 true 인 경우에 스타일 선언 된 개체에 적용 됩니다.

기준 적응형 렌더링 기술을 제공 하는 유연성에는 다양 한 장치에서 사이트를 표시 하는 것에 대 한 모든 사용자 지정할 수 있습니다. 원하는 만큼 스타일 시트 하나에 논리 코드를 작성 하지 않고 스타일을 선택할 수 만큼 스타일을 정의할 수 있습니다. 따라서 중복 된 코드와 목적을 렌더링 하는 것에 대 한 논리의 양이 줄어 대로 조정 페이지 스타일의 매우 간단한 방법입니다. 반면, 대역폭 사용량 증가, CSS 파일의 크기 수 증가 함에 따라 미미 합니다.

적응형 렌더링 기술을 사용 하 여 사이트 됩니다 **브라우저에 관계 없이 올바르게 표시 합니다.** 하지만 추가 대역폭 로드 되는 문제를 고려해 야 합니다.

> [!NOTE]
> 미디어 쿼리의 기본 형식은: @media \[범위: 모든 | 핸드헬드 | 출력 | 프로젝션 | 화면\] ([속성: 값] 및... [속성: 값])


미디어 쿼리 예: &gt;  <strong>@media 모든 및 (최대 너비: 1000px) 및 (최소 너비: 700px) {}:</strong> 700px 사이의 1000px 해상도 모두에 대 한 합니다.

> <strong>@media 화면 및 (최소 너비: 400px) 및 (최대 너비: 700px) {...}:</strong> 화면에 대 한 합니다. 해상도 400 700px 사이 여야 합니다.
> 
> <strong>@media 핸드헬드 및 (최소 너비: 20em), 화면 및 (최소 너비: 20em) {...}:</strong> 휴대 장치 (휴대폰 및 장치) 및 화면에 대 한 합니다. 최소 너비는 20em 보다 커야 합니다.
> 
> 이 대 한 자세한 정보를 찾을 수 있습니다 합니다 [W3C 사이트](http://www.w3.org/TR/css3-mediaqueries/)합니다.


적응형 렌더링의 작동 원리 이제 탐색, 4는 웹 사이트 템플릿을 기본 ASP.NET MVC의 가독성을 향상 합니다.

1. 엽니다는 **PhotoGallery.sln** 솔루션 작업 1에서 만든 하 고 선택 합니다 **PhotoGallery** 프로젝트. 키를 눌러 **F5** 솔루션을 실행 합니다.
2. 브라우저의 너비 절반 또는 원래 크기의 1/4 보다 작은 windows 설정 크기를 조정 합니다. 헤더 항목을 사용 하 여 어떻게 되는지 살펴보십시오: 일부 요소는 헤더의 표시 영역에 표시 되지 것입니다.
3. 오픈 <strong>Site.css</strong> 에 Visual Studio 솔루션 탐색기에서 파일 <strong>콘텐츠</strong> 프로젝트 폴더입니다. 키를 눌러 <strong>CTRL + F</strong> 검색을 통합된 하는 Visual Studio를 열고 쓸 수 <strong>@media</strong> 찾으려고 합니다 <strong>CSS 미디어 쿼리</strong>합니다.

    이 템플릿에 정의 된 미디어 쿼리 조건은이 방식으로 작동: 브라우저의 창 크기 미만인 **850 px**,이 미디어 블록 내에 정의 된 CSS 규칙이 적용 됩니다.

    ![미디어 쿼리를 찾는](whats-new-in-aspnet-mvc-4/_static/image16.png "미디어 쿼리 찾기")

    *미디어 쿼리 찾기*
4. 850에 설정 된 최대 너비 특성 값으로 바꿉니다. 포함 하 여 850px **10px**적응형 렌더링을 사용 하지 않도록 설정 하기 위해 키를 누릅니다 **CTRL + S** 변경 내용을 저장 합니다. 키를 눌러 브라우저에 반환 **ctrl+f5** 변경 내용이 있는 페이지를 새로 고쳐야 합니다. 창의 너비를 조정 하는 경우 두 페이지의 차이 확인 합니다.

    ![페이지 왼쪽에 적용 하는 합니다 @media 생략 되 면 오른쪽 스타일에서에서 스타일](whats-new-in-aspnet-mvc-4/_static/image17.png "페이지 왼쪽에 적용 하는 @media 오른쪽 스타일의 스타일을 생략 하면")

    <em>페이지 왼쪽에 적용 되는 @media 생략 되 면 오른쪽 스타일에서에서 스타일</em>

    이제 모바일 장치에서 어떤 일이 생기 확인해 보겠습니다.

    ![페이지 왼쪽에 적용 하는 합니다 @media 생략 되 면 오른쪽 스타일에서에서 스타일](whats-new-in-aspnet-mvc-4/_static/image18.png "페이지 왼쪽에 적용 하는 @media 오른쪽 스타일의 스타일을 생략 하면")

    <em>페이지 왼쪽에 적용 되는 @media 생략 되 면 오른쪽 스타일에서에서 스타일</em>

    웹 브라우저에서 페이지를 렌더링할 때 변경 되지 않았는지 매우 중요 한 모바일 장치를 사용 하는 경우 알 수 있습니다 하지만 차이점 보다 명확 하 게 됩니다. 이미지의 왼쪽에는 사용자 지정 스타일 가독성을 향상 볼 수 있습니다.

    적응형 렌더링 쉽게 적용 조건부 웹 사이트에 스타일 지정 및 간단한 접근 방식으로 일반적인 스타일 문제를 해결 하는 많은 더 많은 시나리오에서 사용할 수 있습니다.

    뷰포트 메타 태그 및 CSS 미디어 쿼리 되므로 ASP.NET MVC 4 관련 웹 응용 프로그램에서 이러한 기능을 수행할 수 있는 합니다.
5. Visual Studio에서 눌러 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a>연습 2: 사진 갤러리 웹 응용 프로그램 만들기

이 연습에서는 사진 표시 사진 갤러리 응용 프로그램에서 작동 합니다. ASP.NET MVC 4 프로젝트 템플릿을 사용 하 여 먼저 및 서비스에서 사진을 검색 하 고 홈페이지에 표시 하는 기능이 추가 합니다.

다음 연습에서는 모바일 장치에 표시 되는 방법을 향상 시키기 위해이 솔루션에서는 업데이트 합니다.

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a>작업 1-모의 사진 서비스 만들기

이 태스크에서는 갤러리에 표시 되는 콘텐츠를 검색할 사진 서비스의 모형을 만듭니다. 이렇게 하려면 단순히 각 사진 데이터를 사용 하 여 JSON 파일을 반환 하는 새 컨트롤러를 추가 합니다.

1. 오픈 **Visual Studio** 열려 있지 않으면입니다.
2. 선택 된 **파일 | 새 | 프로젝트** 메뉴 명령입니다. 에 **새 프로젝트** 대화 상자에서 선택 된 **Visual C# | 웹** 왼쪽된 창에서 템플릿을 선택한 트리의 **ASP.NET MVC 4 웹 응용 프로그램입니다.** 프로젝트 이름을 **PhotoGallery**, 선택 위치 (또는 기본값)를 클릭 하 고 **확인**합니다. 또는 기존 ASP.NET MVC 4 프로그램에서 작업을 계속할 수 있습니다 **인터넷 응용 프로그램** 에서 솔루션 **실습 1** 하 고 다음 단계를 건너뜁니다.
3. 에 **새 ASP.NET MVC 4 프로젝트** 대화 상자를 선택 합니다 **인터넷 응용 프로그램** 프로젝트 템플릿 및 클릭 **확인**합니다. Razor 뷰 엔진으로 선택 했는지 확인 합니다.
4. 에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **앱\_데이터** 선택한 서버 프로젝트의 폴더 **추가 | 기존 항목**합니다. 로 이동 합니다 **Source\Assets\App\_데이터** 이 랩의 폴더 추가 합니다 **Photos.json** 파일.
5. 이름을 사용 하 여 새 컨트롤러를 만듭니다 **PhotoController**합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 폴더를 이동 **추가** 선택한 **컨트롤러입니다.** 컨트롤러 이름을 완성 합니다 **빈 MVC 컨트롤러** 템플릿과 클릭 **추가**합니다.

    ![추가 된 PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "는 PhotoController 추가")

    *PhotoController 추가*
6. 대체는 **인덱스** 메서드를 다음 **갤러리** 작업 및 최근에 프로젝트에 추가한 JSON 파일의 콘텐츠를 반환 합니다.

    (코드 조각- *ASP.NET MVC 4 실습-Ex02-갤러리 작업*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. 키를 눌러 **F5** 솔루션을 실행 하 여 모의 사진 서비스를 테스트 하려면 다음 URL로 이동 합니다. `http://localhost:[port]/photo/gallery` ([포트] 값은 현재 실행 되는 포트에 따라 다름). 이 URL로 요청 콘텐츠를 검색 해야 합니다 **Photos.json** 파일입니다.

    ![모의 사진 서비스 테스트](whats-new-in-aspnet-mvc-4/_static/image20.png "모의 사진 서비스를 테스트 합니다.")

    *모의 사진 서비스를 테스트합니다.*

실제 구현에서 사용할 수 있습니다 [ASP.NET Web API](../../../../web-api/index.md) 사진 갤러리 서비스를 구현 합니다. ASP.NET Web API는 브라우저 및 모바일 장치를 비롯한 광범위한 클라이언트에 연결하는 HTTP 서비스를 쉽게 빌드할 수 있게 해 주는 프레임워크입니다. ASP.NET Web API는 .NET Framework에서 RESTful 응용 프로그램을 빌드하는 데 이상적인 플랫폼입니다.

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a>작업 2-사진 갤러리를 표시 합니다.

이 태스크에서는이 연습의 첫 번째 작업에서 만든 모의 서비스를 사용 하 여 사진 갤러리를 표시 하도록 홈 페이지가 업데이트 됩니다. 모델 파일을 추가 하 고 갤러리 보기를 업데이트 합니다.

1. Visual Studio에서 눌러 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.
2. 만들기는 **사진** 클래스는 **모델** 폴더입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더 선택 **추가** 클릭 **클래스**합니다. 그런 다음 다른 이름으로 설정할 **Photo.cs** 누릅니다 **추가**합니다.
3. 다음 멤버를 추가 합니다 **사진** 클래스입니다.

    (코드 조각- *ASP.NET MVC 4 실습-Ex02-사진 모델*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. **컨트롤러** 폴더에서 **HomeController.cs** 파일을 엽니다.
5. 다음 using 문을 추가합니다.

    (코드 조각- *ASP.NET MVC 4 실습-Ex02-HomeController Using*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. 업데이트를 **인덱스** 작업을 사용 하 여 **HttpClient** 갤러리 데이터를 검색 한 다음 사용 하는 **JavaScriptSerializer** 뷰 모델을 역직렬화 하는 것을 합니다.

    (코드 조각- *ASP.NET MVC 4 실습-Ex02-인덱스 작업*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. 엽니다는 **Index.cshtml** 아래에 있는 파일을 **Views\Home** 폴더 및 모든 내용 다음 코드로 바꿉니다.

    이 코드는 서비스에서 검색 된 모든 사진을 반복 하 고 순서 없는 목록에 표시 합니다.

    (코드 조각- *ASP.NET MVC 4 실습-Ex02-사진 목록*)

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. 에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **콘텐츠** 선택한 서버 프로젝트의 폴더 **추가 | 기존 항목**합니다. 로 이동 합니다 **Source\Assets\Content** 이 랩의 폴더 추가 합니다 **Site.css** 파일. 대체를 확인 해야 합니다. 있는 경우는 **Site.css** 파일 열기, 파일을 다시 로드할지도 확인 해야 합니다.
9. 파일 탐색기를 열고 전체를 복사 합니다 **사진** 폴더 아래에 **Source\Assets** 솔루션 탐색기에서 프로젝트의 루트 폴더에이 랩의 폴더입니다.
10. 응용 프로그램을 실행합니다. 이제 갤러리에 사진을 표시 홈 페이지가 나타납니다.

    ![사진 갤러리](whats-new-in-aspnet-mvc-4/_static/image21.png "사진 갤러리")

    *사진 갤러리*
11. Visual Studio에서 눌러 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a>연습 3: 모바일 장치에 대 한 지원 추가

모바일 개발에 대 한 지원은 ASP.NET MVC 4에서 키 업데이트 중 하나입니다. 이 연습에서는 이전 연습에서 만든 PhotoGallery 솔루션을 확장 하 여 ASP.NET MVC 4 모바일 응용 프로그램에 대 한 새로운 기능을 탐색 합니다.

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a>작업 1-ASP.NET MVC 4 응용 프로그램에서 jQuery Mobile 설치

1. 엽니다는 **시작할** 솔루션에 있는 **소스/Ex3-MobileSupport/시작/** 폴더. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.

   1. 제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 엽니다는 **패키지 관리자 콘솔** 를 클릭 하 여 합니다 **도구** &gt; **라이브러리 패키지 관리자** &gt; **패키지 관리자 콘솔** 메뉴 옵션입니다.

    ![NuGet 패키지 관리자 콘솔을 열고](whats-new-in-aspnet-mvc-4/_static/image22.png "NuGet 패키지 관리자 콘솔을 열고")

    *NuGet 패키지 관리자 콘솔 열기*
3. 패키지 관리자 콘솔에서 설치 하려면 다음 명령을 실행 합니다 **jQuery.Mobile.MVC** 패키지 있습니다.

    jQuery Mobile은 터치에 최적화 된 웹 UI를 빌드하기 위한 오픈 소스 라이브러리입니다. JQuery.Mobile.MVC NuGet 패키지를 ASP.NET MVC 4 응용 프로그램을 사용 하 여 jQuery Mobile을 사용 하는 도우미를 포함 합니다.

    > [!NOTE]
    > 다음 명령을 실행 하 여 있습니다 됩니다 수 jQuery.Mobile.MVC 라이브러리 다운로드 Nuget에서.

    PM

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    이 명령은 다음과 같은 몇 가지 도우미 파일 및 jQuery Mobile을 설치 합니다.

    - **Views/Shared/\_Layout.Mobile.cshtml**: jQuery Mobile 기반 레이아웃을 더 작은 화면에 맞게 최적화 됩니다. 웹 사이트의 모바일 브라우저에서 요청을 받으면 원래 레이아웃 바뀝니다 (\_Layout.cshtml)이이 하나를 사용 하 여 합니다.
    - 뷰 전환기 구성 요소: 이루어져 합니다 **Views/Shared/\_ViewSwitcher.cshtml** 부분 뷰 및 **ViewSwitcherController.cs** 컨트롤러입니다. 이 구성 요소에서는 사용자가 페이지의 데스크톱 버전으로 전환할 수 있도록 모바일 브라우저에서 링크를 표시 합니다.  
        ![모바일 지원을 사용 하 여 사진 갤러리 프로젝트](whats-new-in-aspnet-mvc-4/_static/image23.png "사진 갤러리 프로젝트 모바일 지원")

        *사진 갤러리 프로젝트 모바일 지원*
4. 모바일 번들을 등록 합니다. 이 작업을 수행 하려면 엽니다는 **Global.asax.cs** 파일을 다음 줄을 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 실습-Ex03-등록 모바일 번들*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. 데스크톱 웹 브라우저를 사용 하 여 응용 프로그램을 실행 합니다.
6. 엽니다는 **Windows Phone 7 에뮬레이터** 에 있는 **시작 메뉴 | 모든 프로그램 | Windows Phone SDK 7.1 | Windows Phone Emulator입니다.**
7. Phone 시작 화면에서 Internet Explorer를 엽니다. 응용 프로그램의 시작 위치 URL을 확인 하 고 휴대폰 브라우저를 사용 하 여 해당 URL로 이동 (예: `http://localhost:[PortNumber]/`).

    jQuery.Mobile.MVC에 모바일 장치에 대 한 액세스에 최적화 된 뷰를 표시 하는 프로젝트에서 새 자산을 만들 때 응용 프로그램은 Windows Phone 에뮬레이터에서 다르게 보일 것을 확인할 수 있습니다.

    데스크톱 뷰로 전환 되는 링크를 보여 주는 휴대폰의 맨 위에 있는 메시지를 확인 합니다. 또한 합니다  **\_Layout.Mobile.cshtml** 레이아웃 설치한 패키지에 의해 생성 된 응용 프로그램에서 다른 레이아웃을 포함 합니다.

    > [!NOTE]
    > 지금 모바일 뷰로 돌아가는 데의 연결이 없습니다. 이상 버전에 포함 됩니다.

    ![사진 갤러리 홈 페이지의 모바일 뷰로](whats-new-in-aspnet-mvc-4/_static/image24.png "사진 갤러리 홈 페이지의 모바일 뷰")

    *사진 갤러리 홈 페이지의 모바일 뷰*
8. Visual Studio에서 눌러 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a>작업 2-모바일 뷰 만들기

이 태스크에서는 모바일 장치에서 더 나은 appareance에 적용할 콘텐츠를 사용 하 여 인덱스 보기의 모바일 버전을 만들어집니다.

1. 복사 합니다 **Views\Home\Index.cshtml** 확인 하 고 붙여 넣어 복사본 만들기, 새 파일 이름 바꾸기 **Index.Mobile.cshtml**합니다.
2. 열린 새 생성 **Index.Mobile.cshtml** 살펴보고로 기존 &lt;ul&gt; 이 코드를 사용 하 여 태그입니다. 이 작업을 수행 하 여 업데이트 됩니다. 합니다 &lt;ul&gt; jQuery에서 모바일 테마를 사용 하려면 jQuery 모바일 데이터 주석 사용한 태그입니다.

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > 다음 사항을 참고하세요.
    > 
    > - 합니다 **데이터 역할** 특성이로 설정 **listview** listview 스타일을 사용 하 여 목록에 렌더링 됩니다.
    > 
    > - 합니다 **inset 데이터** 특성 true로 설정할 둥근된 테두리와 여백을 사용 하 여 목록에 표시 됩니다.
    > 
    > - 합니다 **데이터 필터** 특성이로 설정 **true** 검색 상자에 생성 됩니다.
    > 
    > 프로젝트 문서의 jQuery 모바일 규칙에 대 한 자세한 수 있습니다. [[http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)
3. 키를 눌러 **CTRL + S** 변경 내용을 저장 합니다.
4. 으로 전환 합니다 **Windows Phone 에뮬레이터** 사이트를 새로 고칩니다. 새로운 모양과 느낌으로 갤러리 목록 맨 위에 새 검색 상자를 확인 합니다. 그런 다음 검색 상자에 단어를 입력 (예를 들어 **Tulips**) 사진 갤러리에서 검색을 시작 합니다.

    ![Listview 스타일을 사용 하 여 필터링 된 갤러리](whats-new-in-aspnet-mvc-4/_static/image25.png "listview 스타일을 사용 하 여 필터링 된 갤러리")

    *Listview 스타일을 사용 하 여 필터링 된 갤러리*

    요약 하자면, 사용한 보기 Mobilizer 작성법 사용 하 여 인덱스 뷰의 복사본을 만드는 합니다 &quot;모바일&quot; 접미사. 이 접미사는 모바일 장치에서 생성 된 모든 요청은 인덱스의이 복사본을 사용 하 고는 ASP.NET MVC 4 나타냅니다. 또한 jQuery Mobile을 사용 하 여 모바일 장치에서 사이트 모양과 느낌을 강화를 위해 인덱스 보기로의 모바일 버전을 업데이트 했습니다.
5. Visual Studio로 다시 이동 및 열기 **Site.Mobile.css** 아래에 **콘텐츠** 폴더입니다.
6. 이미지의 오른쪽에 표시 되도록 사진 제목의 위치를 수정 합니다. 이렇게 하려면 다음 코드를 추가 합니다 **Site.Mobile.css** 파일입니다.

    CSS

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. 키를 눌러 **CTRL + S** 변경 내용을 저장 합니다.
8. 다시 전환 합니다 **Windows Phone 에뮬레이터** 사이트를 새로 고칩니다. 사진 제목 제대로 위치가 이제 알 수 있습니다.

    ![이미지의 오른쪽에 배치 하는 title](whats-new-in-aspnet-mvc-4/_static/image26.png "이미지의 오른쪽에 배치 하는 제목")

    *이미지의 오른쪽에 배치 하는 제목*

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a>작업 3-jQuery Mobile 테마

모든 레이아웃 및 jQuery Mobile에서에서 위젯을 새로운 개체 지향 CSS 프레임 워크 사이트 및 응용 프로그램에 완전 통합 된 비주얼 디자인 테마를 적용할 수 있도록 하는 중심으로 디자인 되었습니다.

jQuery Mobile의 기본 테마에는 문자를 지정 된 5 견본 포함 (a, b, c, d, e)에 대 한 빠른 참조입니다.

이 태스크에서는 기본값과 다른 테마를 사용 하는 모바일 레이아웃을 업데이트 합니다.

1. Visual Studio로 다시 전환 합니다.
2. 엽니다는  **\_Layout.Mobile.cshtml** 에 있는 파일 **Views\Shared**합니다.
3. 로 데이터 역할을 사용 하 여 div 요소를 찾습니다 &quot;페이지&quot; 업데이트 및 합니다 **데이터 테마** 에 &quot; **e**&quot;합니다.

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. 키를 눌러 **CTRL + S** 변경 내용을 저장 합니다.
5. 사이트에 새로 고침 합니다 **Windows Phone 에뮬레이터** 새로운 색 구성표를 확인 합니다.

    ![다른 색 구성표를 사용 하 여 모바일 레이아웃](whats-new-in-aspnet-mvc-4/_static/image27.png "다른 색 구성표를 사용 하 여 모바일 레이아웃")

    *다른 색 구성표를 사용 하 여 모바일 레이아웃*

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a>작업 4-뷰 전환기 구성 요소 및 기능을 재정의 하는 브라우저를 사용 하 여

모바일에 최적화 된 웹 페이지에 대 한 규칙을 해당 텍스트는 바탕 화면 보기 또는 사용자가 페이지의 데스크톱 버전을 전환할 수 있는 전체 사이트 모드와 같은 링크를 추가 하는 것입니다. JQuery.Mobile.MVC 패키지가 포함 샘플 **뷰 전환기** 에 사용 되는이 목적을 위해 구성 요소를  **\_Layout.Mobile.cshtml** 보기.

![데스크톱 뷰로 전환 하려면 링크](whats-new-in-aspnet-mvc-4/_static/image28.png "데스크톱 뷰로 전환 하려면 링크")

*데스크톱 뷰로 전환 하려면 링크*

라는 새 기능을 사용 하 여 뷰 전환기 **브라우저 재정의**합니다. 이 기능에서 이루어졌는지도 실제로 아닌 다른 브라우저 (사용자 에이전트)에서 튀어 나오는 것 처럼 요청을 처리 하는 응용을 프로그램을 수 있습니다.

이 태스크에서는 뷰 전환기 jQuery.Mobile.MVC 및 ASP.NET MVC 4의 기능을 재정의 하는 새 브라우저 추가 샘플 구현을 살펴봅니다.

1. Visual Studio로 다시 전환 합니다.
2. 열기는  **\_Layout.Mobile.cshtml** 보기 아래에 **Views\Shared** 폴더 및 통지를 부분 보기로 참조 하 고 뷰 전환기 구성 요소입니다.

    ![전환기 뷰 구성 요소를 사용 하 여 모바일 레이아웃](whats-new-in-aspnet-mvc-4/_static/image29.png "뷰 전환기 구성 요소를 사용 하 여 모바일 레이아웃")

    *전환기 뷰 구성 요소를 사용 하 여 모바일 레이아웃*
3. 엽니다는  **\_ViewSwitcher.cshtml** 부분 뷰.

    새 메서드를 사용 하 여 부분 뷰 **ViewContext.HttpContext.GetOverriddenBrowser()** 웹 요청의 원점을 확인 하 여 데스크톱 또는 모바일 뷰를 전환 하려면 해당 링크를 표시 합니다.

    합니다 **GetOverridenBrowser** 메서드가 반환 되는 **HttpBrowserCapabilitiesBase** 사용자 에이전트 요청에 대 한 현재 설정에 해당 하는 인스턴스 (실제 또는 재정의). 같은 속성을 가져오는 데이 값을 사용할 수 있습니다 **IsMobileDevice**합니다.

    ![부분 뷰 ViewSwitcher](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher 부분 뷰")

    *ViewSwitcher 부분 뷰*
4. 엽니다는 **ViewSwitcherController.cs** 클래스에는 **컨트롤러** 폴더입니다. 체크 아웃 해당 SwitchView 작업 ViewSwitcher 구성 요소의 링크에서 호출 되 고 새로운 HttpContext 메서드를 확인할 수 있습니다.

    - 합니다 **HttpContext.ClearOverridenBrowser()** 메서드는 현재 요청에 대 한 재정의 된 사용자 에이전트를 제거 합니다.
    - 합니다 **HttpContext.SetOverridenBrowser()** 메서드는 지정 된 사용자 에이전트를 사용 하 여 요청의 실제 사용자 에이전트 값을 재정의 합니다.  
        ![ViewSwitcher 컨트롤러](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher 컨트롤러")  
*ViewSwitcher 컨트롤러*

        브라우저 재정의 역시 jQuery.Mobile.MVC 패키지를 설치 하지 않는 경우에 ASP.NET MVC 4의 핵심 기능입니다. 그러나 뷰, 레이아웃 및 부분 뷰,이 기능에 영향을 줍니다 및 Request.Browser 개체에 종속 된 기능이 변경 되지 않습니다.

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a>작업 5-바탕 화면 보기에서 뷰 전환기를 추가 합니다.

이 태스크에서는 데스크톱 레이아웃 뷰 전환기를 포함 하도록 업데이트 합니다. 이렇게 하면 모바일 사용자가 바탕 화면 보기를 검색할 때 모바일 보기로 다시 이동 합니다.

1. 사이트에 새로 고침 합니다 **Windows Phone 에뮬레이터**합니다.
2. 클릭 합니다 **바탕 화면 보기** 갤러리의 맨 위에 있는 링크입니다. 모바일 뷰를 반환할 수 있도록 바탕 화면 보기에 없는 뷰 전환기를 확인 합니다.
3. Visual Studio로 다시 이동 하 고 엽니다는  **\_Layout.cshtml** 보기.
4. 로그인 섹션을 찾고 렌더링에 대 한 호출을 삽입 합니다  **\_ViewSwitcher** 아래의 부분 보기를  **\_LogOnPartial** 부분 뷰. 그런 다음 키를 눌러 **CTRL + S** 변경 내용을 저장 합니다.

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. 키를 눌러 **CTRL + S** 변경 내용을 저장 합니다.
6. Windows Phone 에뮬레이터에서 페이지를 새로 고치고 화면 확대/축소를 두 번 클릭 합니다. 홈 페이지에는 이제 표시 하는 **모바일 뷰** 모바일에서 데스크톱 보기로 전환 하는 링크입니다.

    ![바탕 화면 보기에서 렌더링 전환기 보고](whats-new-in-aspnet-mvc-4/_static/image32.png "바탕 화면 보기에서 렌더링 하는 뷰 전환기")

    *바탕 화면 보기에서 렌더링 하는 뷰 전환기*
7. 모바일 뷰로 다시 전환 하 고 찾아보기 <strong>에 대 한</strong> 페이지 (http://localhost[port]/Home/About). About.Mobile.cshtml 뷰를 만들지 않은, 경우에 정보 페이지 표시 됩니다 모바일 레이아웃을 사용 하 여 (\_Layout.Mobile.cshtml).

    ![페이지에 대 한](whats-new-in-aspnet-mvc-4/_static/image33.png "페이지에 대 한")

    *페이지에 대 한*
8. 마지막으로, 데스크톱 웹 브라우저에서 사이트를 엽니다. 이전 업데이트에 영향을 미치지 않습니다 바탕 화면 보기를 확인 합니다.

    ![바탕 화면 보기 PhotoGallery](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery 바탕 화면 보기")

    *PhotoGallery 바탕 화면 보기*

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a>태스크 6-새 디스플레이 모드 만들기

새로운 디스플레이 모드 기능에는 응용 프로그램을 요청을 생성 하는 브라우저에 따라 뷰를 선택할 수 있습니다. 예를 들어, 데스크톱 브라우저 홈 페이지를 요청 하는 경우 응용 프로그램은 반환 된 **Views\Home\Index.cshtml** 템플릿. 그런 다음 모바일 브라우저 홈 페이지를 요청 하는 경우 응용 프로그램은 반환 된 **Views\Home\Index.mobile.cshtml** 템플릿.

이 태스크에서는 iPhone 장치에 대 한 사용자 지정된 레이아웃을 만들려는 및 iPhone 장치에서 요청을 시뮬레이션 해야 합니다. 이렇게 하려면 중 하나는 iPhone 에뮬레이터/시뮬레이터를 사용할 수 있습니다 (같은 [Electric Mobile 시뮬레이터](http://www.electricplum.com/)) 또는 사용자 에이전트를 수정 하는 추가 기능을 사용 하 여 브라우저입니다. IPhone을 에뮬레이트 하려면 Safari 브라우저에서 사용자 에이전트 문자열을 설정 하는 방법에 지침을 참조 하세요 [하도록 Safari IE 것으로 가정 하는 방법을](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) David Alison 블로그에서.

**이 작업은 선택 사항는 연구소에서 실행 하지 않고 것에 유의 하십시오.**

1. Visual Studio에서 눌러 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.
2. 오픈 **Global.asax.cs** 추가한 다음 문을 사용 하 여 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. 다음 강조 표시 된 코드를 응용 프로그램에 추가\_메서드를 시작 합니다.

    (코드 조각- *ASP.NET MVC 4 실습-Ex03-iPhone DisplayMode*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

새 등록 **라는 DefaultDisplayMode &quot;iPhone&quot;**, 정적 내 **DisplayModeProvider.Instance.Modes** 과 일치 하는 정적 목록 들어오는 각 요청입니다. 들어오는 요청 문자열을 포함 하는 경우 &quot;iPhone&quot;, ASP.NET MVC 이름이 포함 하는 뷰를 찾을 수 합니다 &quot;iPhone&quot; 접미사. 매개 변수 0 나타냅니다 어떻게 특정 새 모드입니다. 이 보기는 일반 보다 구체적인 예를 들어 &quot;.mobile&quot; 모바일 장치에서 요청을 일치 하는 규칙입니다.

응용 프로그램에서 사용할이 코드를 실행 한 후 iPhone 브라우저는 요청을 생성 하는 경우에 **Views\Shared\\_Layout.iPhone.cshtml** 다음 단계에서 만든 레이아웃 합니다.

> [!NOTE]
> 이러한 방식의 iPhone 데모를 위해 간소화 되었으며 (에 대 한 예제 테스트는 대/소문자 구분) 모든 iPhone 사용자 에이전트 문자열에 대 한 예상 대로 작동 하지 않을 수 있습니다에 대 한 요청을 테스트 합니다.

4. 복사본을 만듭니다를  **\_Layout.Mobile.cshtml** 파일을 **Views\Shared** 폴더에 복사를 바꾸고 &quot; **\_Layout.iPhone.csthml**&quot;.
5. 오픈  **\_Layout.iPhone.csthml** 이전 단계에서 만들었습니다.
6. 으로 설정 된 데이터 역할 특성을 사용 하 여 div 요소를 찾습니다 **페이지** 변경 합니다 **데이터 테마** 특성을 &quot; **는**&quot;합니다.


[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

ASP.NET MVC 4 응용 프로그램에서 3 레이아웃을 이제 해야합니다.

1. **\_Layout.cshtml**: 데스크톱 브라우저에 사용 되는 기본 레이아웃입니다.
2. **\_Layout.mobile.cshtml**: 모바일 장치에 사용 되는 기본 레이아웃입니다.
3. **\_Layout.iPhone.cshtml**: iPhone 장치를 구별 하기 위해 다른 색 구성표를 사용 하 여 특정 레이아웃 \_Layout.mobile.cshtml 합니다.
7. 키를 눌러 **F5** 에서 사이트를 찾아 응용 프로그램을 실행 하는 **Windows Phone 에뮬레이터**합니다.
8. 열기는 **iPhone 시뮬레이터** (참조 [부록 C](#AppendixC) 설치 하 고 iPhone 시뮬레이터가 구성 하는 방법에 대 한 지침은), 너무 사이트로 이동 합니다. 각 전화 특정 템플릿을 사용 하 고 있음을 알 수 있습니다.

    ![Using-different-views-for-each-mobile-device2](whats-new-in-aspnet-mvc-4/_static/image35.png)

    *각 모바일 장치에 대 한 서로 다른 뷰를 사용 하 여*

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a>실습 4: 비동기 컨트롤러 사용

Microsoft.NET Framework 4.5에서는 C# 및 Visual Basic.NET 프로그래밍의 비동기에 대 한 새 기반을 제공 하는 새로운 언어 기능을 소개 합니다. 이 새 foundation에서 비동기 프로그래밍을 비슷합니다-및 약-동기 프로그래밍 만큼 간단 합니다. ASP.NET MVC 4에서 비동기 작업 메서드를 사용 하 여 쓸 수 있습니다 합니다 **AsyncController** 클래스입니다. CPU 바인딩되지 않은 요청, 장기 실행에 대 한 비동기 작업 메서드를 사용할 수 있습니다. 웹 서버 요청을 처리 하는 동안 작업을 수행할 수 없도록 차단 하는 것이 이렇게 없습니다. AsyncController 클래스는 일반적으로 장기 실행 웹 서비스 호출에 사용 됩니다.

이 연습에서는 ASP.NET MVC 4에서 비동기 작업의 기본 사항을 설명합니다. 심층 분석을 하려는 경우 다음 문서를 확인할 수 있습니다. [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a>작업 1-비동기 컨트롤러를 구현 합니다.

1. 엽니다는 **시작할** 솔루션에 있는 **소스/Ex4-Async/시작/** 폴더. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.

   1. 제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 엽니다는 **HomeController.cs** 에서 클래스를 **컨트롤러** 폴더입니다.
3. 다음 추가 문을 사용 하 여 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. 업데이트를 **HomeController** 클래스에서 상속 하도록 **AsyncController**합니다. AsyncController에서 파생 된 컨트롤러는 비동기 요청을 처리 하는 ASP.NET을 사용 하도록 설정 하 고 여전히 서비스 동기 작업 메서드 할 수 있습니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. 추가 합니다 **비동기** 키워드를를 **인덱스** 메서드 형식을 반환할 수 있도록 **태스크&lt;ActionResult&gt;** 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > 합니다 **비동기** 키워드를 사용 하면.NET Framework 4.5를 제공 하는 새 키워드 중 하나인; 컴파일러에 알려 준다는이 메서드가 비동기 코드를 포함 합니다. A **태스크** 개체 시점에서 나중에 완료할 수 있는 비동기 작업을 나타냅니다.
6. 대체는 **클라이언트입니다. Getasync ()** 아래와 같이 await 키워드를 사용 하 여 전체 비동기 버전 호출 합니다.

    (코드 조각- *ASP.NET MVC 4-Ex04-랩 GetAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > 이전 버전에서 사용 했습니다 합니다 **결과** 속성을 **작업** 결과 (동기화 버전)를 반환 될 때까지 스레드를 차단 하는 개체.
    > 
    > 추가 된 **await** 키워드 메서드 호출에서 반환 된 작업을 비동기적으로 대기할 컴파일러에 알립니다. 즉, 대기 중인된 메서드가 완료 된 후에 코드의 나머지 콜백으로 실행할 수 있습니다. 다른 눈에 띄는 것은이 작업을 수행 하기 위해 try / catch 블록을 변경할 필요가 없습니다: 프레임 워크에서 제공 하는 처리기를 사용 하 여 추가 작업 없이 포그라운드 또는 백그라운드에서 발생 하는 예외를 포착 계속 됩니다.
7. 아래와 같이 새 코드를 사용 하 여 줄을 대체 하 여 비동기 구현을 사용 하 여 계속 하도록 코드를 변경

    (코드 조각- *ASP.NET MVC 4-Ex04-랩 ReadAsStringAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. 응용 프로그램을 실행합니다. 주요 내용이 표시 됩니다 있지만 코드 성능 향상 및 더 나은 서버 리소스를 사용 하는 스레드 풀에서 스레드를 차단 하지 않습니다.

    > [!NOTE]
    > 랩에서 새로운 비동기 프로그래밍 기능에 대해 자세히 알아볼 수 있습니다 &quot; **C# 및 Visual Basic.NET 4.5의 비동기 프로그래밍** &quot; Visual Studio 교육 키트에 포함 합니다.

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a>작업 2-취소 토큰을 사용 하 여 처리 시간 제한

태스크 인스턴스를 반환 하는 비동기 작업 메서드는 시간 제한도 지원할 수 있습니다. 이 태스크에서는 취소 토큰을 사용 하는 시간 제한 시나리오를 처리 하는 인덱스 메서드 코드를 업데이트 합니다.

1. Visual Studio 및 키를 눌러도 돌아가 **shift+f5** 디버깅을 중지 합니다.
2. 다음 코드를 추가 하는 문을 사용 하 여는 **HomeController.cs** 파일.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. 업데이트를 받을 인덱스 작업을 **CancellationToken** 인수입니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. 업데이트를 **GetAsync** 호출 취소 토큰을 전달 합니다.

    (코드 조각- *CancellationToken 사용 하 여 ASP.NET MVC 4-Ex04-랩 SendAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. 데코 레이트 합니다 *인덱스* 메서드는 **AsyncTimeout** 500 밀리초로 설정 된 특성 및 **HandleError** 처리 하도록 구성 하는 특성  **TaskCanceledException** 리디렉션하여를 **TimedOut** 보기.

    (코드 조각- *ASP.NET MVC 4 실습-Ex04-특성*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. 엽니다는 **PhotoController** 클래스 및 업데이트를 **갤러리** 는 장기 실행 작업을 시뮬레이션 하기 위해 실행 1000 밀리초 (1 초)을 지연 하는 방법입니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. 엽니다는 **Web.config** 파일과 다음 요소를 추가 하 여 사용자 지정 오류를 사용 하도록 설정 합니다.

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. 새 뷰를 만들 **Views\Shared** 라는 **TimedOut** 및 기본 레이아웃을 사용 합니다. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 **Views\Shared** 선택한 폴더 **추가 | 보기**합니다.

    ![서로 다른 뷰를 사용 하 여 각 모바일 장치에 대 한](whats-new-in-aspnet-mvc-4/_static/image36.png "서로 다른 뷰를 사용 하 여 각 모바일 장치에 대 한")

    *각 모바일 장치에 대 한 서로 다른 뷰를 사용 하 여*
9. 업데이트를 **TimedOut** 아래와 같이 콘텐츠를 확인 합니다.

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. 응용 프로그램을 실행 하 고 루트 URL로 이동 합니다. 추가한를 **Thread.Sleep** 1000 밀리초에서 생성 된 시간 제한 오류를 받습니다 합니다 **AsyncTimeout** 특성 및 catch 하 여 합니다 **HandleError** 특성입니다.

    ![처리 시간 제한 예외](whats-new-in-aspnet-mvc-4/_static/image37.png "처리 시간 제한 예외")

    *처리 시간 제한 예외*

> [!NOTE]
> 또한 다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다 [부록 d: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixD)합니다.


<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩, 있습니다 했으므로 관찰 몇 가지 새로운 기능에 ASP.NET MVC 4. 다음 개념 설명 했습니다.

- 향상 된 기능을 ASP.NET MVC 프로젝트 템플릿을 포함 한 새 모바일 응용 프로그램 프로젝트 템플릿을 활용합니다
- HTML5 사용 하 여 뷰포트 특성 및 모바일 장치의 디스플레이 향상 시키기 위해 CSS 미디어 쿼리
- JQuery Mobile 터치에 최적화 된 웹 UI를 구축 하기 위한 점진적 향상 된 기능을 사용 하 여
- 모바일 전용 뷰 만들기
- 전환기 뷰 구성 요소를 사용 하 여 응용 프로그램에서 모바일 및 데스크톱 뷰 사이 전환 하려면
- 작업을 사용 하 여 비동기 컨트롤러 만들기

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>부록 a: 코드 조각 사용

코드 조각을 사용 하 여 결정적인 순간에 필요한 모든 코드를 해야 합니다. 랩 문서가 알려줍니다 정확 하 게 사용할 수 있는 시기를 다음 그림과 같습니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드를 삽입할](whats-new-in-aspnet-mvc-4/_static/image38.png "프로젝트에 코드를 삽입 하는 Visual Studio를 사용 하 여 코드 조각을")

*프로젝트에 코드를 삽입 하려면 Visual Studio 코드 조각 사용*

***키보드 (C#만 해당)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드를 삽입 하려는 위치에 커서를 놓습니다.
2. 시작 (공백 없이 하이픈) 조각 이름을 입력 합니다.
3. IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.
4. 올바른 코드 조각을 선택 합니다 (또는 전체 코드 조각 이름을 선택 될 때까지 입력 유지).
5. 커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.

![코드 조각 이름을 입력](whats-new-in-aspnet-mvc-4/_static/image39.png "조각 이름을 입력 하기 시작")

*코드 조각 이름을 입력 하기 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각을](whats-new-in-aspnet-mvc-4/_static/image40.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")

*Tab 키를 눌러 강조 표시 된 코드 조각 선택*

![Tab 키를 다시 코드 조각 확장 됩니다](whats-new-in-aspnet-mvc-4/_static/image41.png "다시 Tab 키를 누릅니다 하 고 코드 조각에서는 확장")

*Tab 키를 다시 및 코드 조각에서는 확장*

***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.
2. 선택 **코드 조각 삽입** 뒤 **내 코드 조각**합니다.
3. 클릭 하 여 목록에서 관련 코드 조각을 선택 합니다.

![코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭](whats-new-in-aspnet-mvc-4/_static/image42.png "코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭")

*코드 조각을 삽입할 선택한 코드 조각 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭*

![클릭 하 여 목록에서 관련 코드 조각 선택](whats-new-in-aspnet-mvc-4/_static/image43.png "클릭 하 여 목록에서 관련 코드 조각 선택")

*클릭 하 여 목록에서 관련 코드 조각 선택*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>부록 b: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**. 다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.

1. 로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다. 또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Windows Azure SDK를 사용 하 여 Web</em>&quot;합니다.
2. 클릭할 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.

    ![Visual Studio Express를 설치](whats-new-in-aspnet-mvc-4/_static/image44.png "Visual Studio Express를 설치 합니다.")

    *Visual Studio Express를 설치 합니다.*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건에 동의](whats-new-in-aspnet-mvc-4/_static/image45.png)

    *사용 조건에 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](whats-new-in-aspnet-mvc-4/_static/image46.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **완료**합니다.

    ![설치 완료](whats-new-in-aspnet-mvc-4/_static/image47.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. 로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.

    ![VS Express for Web 타일](whats-new-in-aspnet-mvc-4/_static/image48.png)

    *VS Express for Web 타일*

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a>부록 c: 설치 WebMatrix 2 및 iPhone 시뮬레이터

시뮬레이션 된 iPhone 장치에서 사이트를 실행 하는 WebMatrix 확장을 사용할 수 있습니다 &quot;iPhone 용 Electric Mobile 시뮬레이터&quot;합니다. 또한 Visual Studio 2012에서 시뮬레이터를 실행 하려면 같은 확장 프로그램을 구성할 수 있습니다.

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a>작업 1-WebMatrix 설치 2

1. 로 이동 [ [ https://go.microsoft.com/?linkid=9809776 ](https://go.microsoft.com/?linkid=9809776) ](https://go.microsoft.com/?linkid=9810169)합니다. 또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>WebMatrix 2</em>&quot;합니다.
2. 클릭할 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.

    ![WebMatrix 2를 설치할](whats-new-in-aspnet-mvc-4/_static/image49.png "WebMatrix 2를 설치 합니다.")

    *WebMatrix 2를 설치 합니다.*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건에 동의](whats-new-in-aspnet-mvc-4/_static/image50.png "사용 조건에 동의")

    *사용 조건에 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](whats-new-in-aspnet-mvc-4/_static/image51.png "설치 진행률")

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **완료**합니다.

    ![설치 완료](whats-new-in-aspnet-mvc-4/_static/image52.png "설치 완료")

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a>작업 2-iPhone 시뮬레이터 확장 설치

1. 실행할 **WebMatrix** 및 기존 웹 사이트를 열거나 새로 만듭니다.
2. 클릭 합니다 **실행** 에서 단추를 **홈** 선택한 리본 **새로 추가**합니다.

    ![새 WebMatrix 확장을 추가](whats-new-in-aspnet-mvc-4/_static/image53.png "새 WebMatrix 확장 추가")

    *새 WebMatrix 확장 추가*
3. 선택 **iPhone 시뮬레이터** 누릅니다 **설치**합니다.

    ![WebMatrix 확장을 탐색](whats-new-in-aspnet-mvc-4/_static/image54.png "WebMatrix 검색 확장")

    *WebMatrix 확장 검색*
4. 패키지 세부 정보를 클릭 **설치** 확장 설치를 사용 하 여 계속 합니다.

    ![iPhone 시뮬레이터 확장](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone 시뮬레이터 확장")

    *iPhone 시뮬레이터 확장*
5. 읽기 및 확장 EULA에 동의 합니다.

    ![WebMatrix 확장 EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix 확장 EULA")

    *WebMatrix 확장 EULA*
6. 이제 실행할 수 있습니다 웹 사이트가 WebMatrix에서 iPhone 시뮬레이터 옵션을 사용 하 여.

    ![IPhone을 사용 하 여 실행할](whats-new-in-aspnet-mvc-4/_static/image57.png "iPhone을 사용 하 여 실행")

    *IPhone을 사용 하 여 실행*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a>작업 3-iPhone 시뮬레이터를 실행 하려면 Visual Studio 2012를 구성 합니다.

1. 엽니다 **Visual Studio 2012** 및 웹 사이트를 열거나 새 프로젝트를 만듭니다.
2. 실행 단추에서 아래쪽 화살표를 클릭 하 고 선택 **사용 하 여 찾아보기**합니다.

    ![사용 하 여 찾아보기](whats-new-in-aspnet-mvc-4/_static/image58.png "찾아보기")

    *사용 하 여 찾아보기*
3. 에 &quot;브라우저&quot; 대화 상자에서 클릭 **추가**합니다.
4. 에 &quot;프로그램 추가&quot; 대화 상자에서 다음 값을 사용 합니다.

   - <strong>프로그램</strong>: C:\Users\*{CurrentUser}<em>\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe * (경로 적절 하 게 업데이트)</em>
   - **인수**: &quot;1&quot;
   - **이름을**: iPhone 시뮬레이터

     ![프로그램 추가](whats-new-in-aspnet-mvc-4/_static/image59.png "프로그램 추가")

     *로 검색 하도록 프로그램 추가*
5. 클릭 **확인** 대화 상자를 닫습니다.
6. 이제 Visual Studio 2012에서 iPhone 시뮬레이터에서 웹 응용 프로그램을 실행할 수 있습니다.

    ![IPhone 시뮬레이터를 사용 하 여 찾아보기](whats-new-in-aspnet-mvc-4/_static/image60.png "iPhone 시뮬레이터를 사용 하 여 찾아보기")

    *IPhone 시뮬레이터를 사용 하 여 찾아보기*

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>부록 d: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

이 부록은 Windows Azure 관리 포털에서 새 웹 사이트를 만들고 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하 고 랩에 따라 얻은 응용 프로그램을 게시 하는 방법을 보여 줍니다.

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>작업 1-Windows에서 새 웹 사이트를 만드는 Azure Portal

1. 로 이동 합니다 [Windows Azure 관리 포털](https://manage.windowsazure.com/) 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.

    > [!NOTE]
    > Windows Azure를 사용 하 여 10 개의 ASP.NET 웹 사이트를 무료로 호스트할 수 있으며 다음 트래픽 증가 따라 확장할 수 있습니다. 등록할 수 있습니다 [여기](http://aka.ms/aspnet-hol-azure)합니다.

    ![Windows Azure 포털에 로그온](whats-new-in-aspnet-mvc-4/_static/image61.png "Windows Azure 포털에 로그온")

    *Windows Azure 관리 포털에 로그온*
2. 클릭 **새로 만들기** 명령 모음에서.

    ![새 웹 사이트를 만드는](whats-new-in-aspnet-mvc-4/_static/image62.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. 클릭 **계산** | **웹 사이트**합니다. 선택한 **빨리 만들기** 옵션입니다. 새 웹 사이트를 사용할 수 있는 URL을 제공 하 고 클릭 **웹 사이트 만들기**합니다.

    > [!NOTE]
    > Windows Azure 웹 사이트는 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트. 빠른 생성 옵션을 사용 하면 완료 된 웹 응용 프로그램을 Windows Azure에서 웹 사이트 포털 외부에서 배포할 수 있습니다. 데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](whats-new-in-aspnet-mvc-4/_static/image63.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.
5. 웹 사이트를 만든 후 아래의 링크를 클릭 합니다 **URL** 열입니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트를 찾아](whats-new-in-aspnet-mvc-4/_static/image64.png "새 웹 사이트를 검색 합니다.")

    *새 웹 사이트를 검색합니다.*

    ![실행 중인 웹 사이트](whats-new-in-aspnet-mvc-4/_static/image65.png "실행 중인 웹 사이트")

    *실행 중인 웹 사이트*
6. 포털로 돌아가서에서 웹 사이트의 이름을 클릭 합니다 **이름을** 관리 페이지를 표시 하는 열입니다.

    ![웹 사이트 관리 페이지를 열어](whats-new-in-aspnet-mvc-4/_static/image66.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. **대시보드** 페이지의 **간략 상태** 섹션을 클릭 합니다 **게시 프로필 다운로드** 링크.

    > [!NOTE]
    > 합니다 *게시 프로필* 모든 각각의 설정 된 게시 방법에 대 한 Windows Azure 웹 사이트를 웹 응용 프로그램을 게시 하는 데 필요한 정보를 포함 합니다. 게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열을 포함 합니다. **Microsoft WebMatrix 2**하십시오 **Microsoft Visual Studio Express for Web** 하 고 **Microsoft Visual Studio 2012** 읽기 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화할 Windows Azure websites에 웹 응용 프로그램을 게시합니다.

    ![게시 프로필 다운로드 웹 사이트](whats-new-in-aspnet-mvc-4/_static/image67.png "게시 프로필 다운로드 웹 사이트")

    *게시 프로필 다운로드 웹 사이트*
8. 알려진된 위치에 게시 프로필 파일을 다운로드 합니다. 추가이 연습에서이 파일을 사용 하 여 Visual Studio에서 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 방법을 표시 됩니다.

    ![게시 프로필 파일을 저장](whats-new-in-aspnet-mvc-4/_static/image68.png "게시 프로필 저장")

    *게시 프로필 파일을 저장 하는 중*

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL 서버를 사용할 경우 데이터베이스를 SQL Database 서버 만들기 해야 합니다. SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하는 것에 대 한 SQL Database 서버를 해야 합니다. Windows Azure 관리 포털에서 구독의 SQL Database 서버를 볼 수 있습니다 **Sql Database** | **서버** | **서버 대시보드**합니다. 만든 서버가 없는 경우 하나를 사용 하 여 만들 수 있습니다 합니다 **추가** 명령 모음에서 단추입니다. 기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**처럼 다음 작업에서 사용 됩니다. 만들지 마십시오 데이터베이스 아직 이후 단계에서 만들어집니다.

    ![SQL Database 서버 대시보드](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database 서버 대시보드")

    *SQL Database 서버 대시보드*
2. 다음 태스크에서는 테스트 Visual Studio에서 데이터베이스 연결 서버 목록에 로컬 IP 주소를 포함 해야 하는 이유로 **허용 된 IP 주소**합니다. 이렇게 하려면 클릭 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여 넣습니다 합니다 **시작 IP 주소** 및 **끝IP주소** 입력란을 클릭 합니다 ![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png) 단추입니다.

    ![클라이언트 IP 주소를 추가합니다.](whats-new-in-aspnet-mvc-4/_static/image71.png)

    *클라이언트 IP 주소를 추가합니다.*
3. 한 번 합니다 **클라이언트 IP 주소** 허용 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 변경을 확인 합니다.

    ![변경 확인](whats-new-in-aspnet-mvc-4/_static/image72.png)

    *변경 확인*

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션 돌아갑니다. 에 **솔루션 탐색기**, 웹 사이트 프로젝트를 마우스 오른쪽 단추로 **게시**합니다.

    ![응용 프로그램 게시](whats-new-in-aspnet-mvc-4/_static/image73.png "응용 프로그램 게시")

    *웹 사이트를 게시합니다.*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필 가져오기](whats-new-in-aspnet-mvc-4/_static/image74.png "게시 프로필 가져오기")

    *게시 프로필 가져오기*
3. 클릭 **연결의 유효성을 검사**합니다. 유효성 검사가 완료 되 면 클릭 **다음**합니다.

    > [!NOTE]
    > 연결 유효성 검사 단추 옆에 나타나는 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.

    ![연결 유효성 검사](whats-new-in-aspnet-mvc-4/_static/image75.png "연결 유효성 검사")

    *연결 유효성 검사*
4. 에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추를 클릭 (즉 **DefaultConnection**).

    ![웹 배포 구성](whats-new-in-aspnet-mvc-4/_static/image76.png "웹 배포 구성")

    *웹 배포 구성*
5. 데이터베이스 연결을 다음과 같이 구성 합니다.

   - 에 **서버 이름** SQL Database 서버 URL 사용 하 여 입력 합니다 *tcp:* 접두사입니다.
   - **사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 서버 관리자 로그인 암호를 입력 합니다.
   - 예를 들어 새 데이터베이스 이름을 입력 합니다. *MVC4SampleDB*합니다.

     ![대상 연결 문자열 구성](whats-new-in-aspnet-mvc-4/_static/image77.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 다음 **확인**을 클릭합니다. 데이터베이스를 만들라는 메시지가 나오면 **예**합니다.

    ![데이터베이스를 만드는](whats-new-in-aspnet-mvc-4/_static/image78.png "데이터베이스 문자열 만들기")

    *데이터베이스 만들기*
7. 기본 연결 텍스트 상자 내에서 사용 하 여 Windows Azure에서 SQL Database에 연결 하는 연결 문자열 표시 됩니다. **다음**을 클릭합니다.

    ![SQL Database를 가리키는 연결 문자열](whats-new-in-aspnet-mvc-4/_static/image79.png "SQL 데이터베이스를 가리키는 연결 문자열")

    *SQL Database를 가리키는 연결 문자열*
8. 에 **미리 보기** 페이지에서 클릭 **게시**합니다.

    ![웹 응용 프로그램 게시](whats-new-in-aspnet-mvc-4/_static/image80.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.

    ![Windows Azure에 응용 프로그램 게시](whats-new-in-aspnet-mvc-4/_static/image81.png "응용 프로그램이 Windows Azure에 게시")

    *Windows Azure에 게시 하는 응용 프로그램*
