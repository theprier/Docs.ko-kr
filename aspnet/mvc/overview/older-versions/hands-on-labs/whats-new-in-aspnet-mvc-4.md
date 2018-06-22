---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: ASP.NET MVC 4의에서 새로운 기능 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4는 ASP.NET의 능력에 대 한 체계적인 디자인 패턴을 사용 하 여 확장 가능 하 고 표준 기반 웹 응용 프로그램을 구축 하기 위한 프레임 워크 및...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 485d2ba7a1274bbb36cfbcbca9322cecc8c8d77c
ms.sourcegitcommit: 3a893ae05f010656d99d6ddf55e82f1b5b6933bc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/18/2018
ms.locfileid: "34306899"
---
# <a name="whats-new-in-aspnet-mvc-4"></a>ASP.NET MVC 4의에서 새로운 기능

으로 [웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트를 다운로드 합니다.](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 4는 ASP.NET 및.NET framework의 능력에 대 한 체계적인 디자인 패턴을 사용 하 여 확장 가능 하 고 표준 기반 웹 응용 프로그램을 구축 하기 위한 프레임 워크. 이 새로운, 네 번째 버전의 framework 모바일 웹 응용 프로그램 개발을 보다 쉽게에 중점을 둡니다.

처음에 새 ASP.NET MVC 4 프로젝트를 만들 때 이제 되어 모바일 응용 프로그램 프로젝트 템플릿을 모바일 장치용으로 독립 실행형 응용 프로그램을 만드는 데 사용할 수 있습니다. 또한 ASP.NET MVC 4 jQuery Mobile jQuery.Mobile.MVC NuGet 패키지를 통해 통합합니다. jQuery Mobile 등의 Windows Phone, iPhone, Android를 포함 하 여 모든 인기 있는 모바일 장치 플랫폼에 호환 되는 웹 응용 프로그램을 개발 하기 위한 HTML5 기반 프레임 워크입니다. 그러나 특수화 해야 할 경우 ASP.NET MVC 4도 사용 하면 다양 한 장치에 대해 개별 보기를 처리 하 고 장치별 최적화를 제공 합니다.

ASP.NET MVC 4로 시작 됩니다이 실습 랩에서 &quot;인터넷 응용 프로그램&quot; 사진 갤러리 응용 프로그램을 만드는 프로젝트 템플릿을 합니다. JQuery Mobile 및 ASP.NET MVC 4의 새로운 기능을 사용 하 여 다양 한 모바일 장치 및 데스크톱 웹 브라우저와 호환 되도록 하려면 앱을 점진적으로 향상 됩니다. 코드 생성 및 ASP.NET MVC 4 사용을 쉽게 방법 작업을 지원 하 여 비동기 작업 메서드를 작성할 수에 대 한 새 코드 레시피에 대 한 배웁니다&lt;ActionResult&gt; 형식을 반환 합니다.

> [!NOTE]
> 모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다. 이 랩에 특정 프로젝트에서 사용할 수는 [What's New in ASP.NET 4.5에서 Web Forms](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)합니다.

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 배웁니다 하는 방법:

- ASP.NET MVC 프로젝트 템플릿을 포함 한 새로운 모바일 응용 프로그램 프로젝트 템플릿을에 향상 된 기능을 활용
- HTML5 뷰포트 특성 및 CSS 미디어 쿼리를 사용 하 여 모바일 장치에 표시를 향상 시키기
- JQuery Mobile 점진적 향상 된 기능에 대 한 터치에 최적화 된 웹 UI를 작성 하기 위한 사용
- 모바일 전용 뷰 만들기
- 뷰 전환기 구성 요소를 사용 하 여 응용 프로그램에 모바일 및 데스크톱 뷰 사이 전환 하려면
- 비동기 컨트롤러 작업 지원을 사용 하 여 만들기

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 B](#AppendixB) 설치 하는 방법에 대 한 지침은).
- [ASP.NET MVC 4](../../../mvc4.md) (Microsoft Visual Studio 2012 설치에 포함 됨)
- Windows Phone 에뮬레이터 (에 포함 된 [7.1.1 Windows Phone SDK](https://www.microsoft.com/download/details.aspx?id=29233))
- 선택 사항- [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) 와 **Electric Plum iPhone 시뮬레이터** (iPhone 시뮬레이터와 웹 응용 프로그램을 탐색 하는 데 사용 하는 연습 3)에 확장

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>설정

랩 문서를 통해 코드 블록을 삽입 하도록 합니다. 사용자 편의 위해 해당 코드의 대부분을 수동으로 추가할 필요가 없도록 하려면 Visual Studio 내에서 사용할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.

설치 하려면 코드 조각:

1. Windows 탐색기 창을 열고 다음을 찾아보기에 랩 **Source\Setup** 폴더입니다.
2. 두 번 클릭은 **Setup.cmd** Visual Studio 코드 조각을 설치 하려면이 폴더에는 파일입니다.

이 문서에서 부록을 참조할 수 사용 하는 방법에 알아봅니다 사용 하 고 Visual Studio 코드 조각에 익숙한 경우 &quot; [부록 a:를 사용 하 여 코드 조각을](#AppendixA)&quot;합니다.

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습에 포함 됩니다.

1. [새 ASP.NET MVC 4 프로젝트 템플릿](#Exercise1)
2. [사진 갤러리 웹 응용 프로그램 만들기](#Exercise2)
3. [모바일 장치에 대 한 지원 추가](#Exercise3)
4. [비동기 컨트롤러를 사용 하 여](#Exercise4)

> [!NOTE]
> 각 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다. 연습을 통해 작업 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.


예상 소요 시간: **60 분**합니다.

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a>연습 1: 새 ASP.NET MVC 4 프로젝트 템플릿

이 연습에서는 ASP.NET MVC 4 프로젝트 템플릿의 향상 된 기능을 탐색 합니다. 인터넷 응용 프로그램 템플릿 외에 MVC 3에 이미 있는이 버전 이제 포함 된 별도 템플릿이 모바일 응용 프로그램에 대 한 합니다. 먼저, 각 템플릿의 몇 가지 관련 기능에 확인 합니다. 그런 다음에서 적합 한 접근 방식을 사용 하 여 서로 다른 플랫폼에서 올바르게 페이지 렌더링에 사용 합니다.

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a>작업 1-인터넷 응용 프로그램 템플릿에서 탐색

1. 열기 **Visual Studio**합니다.
2. 선택 된 **파일 | 새로 만들기 | 프로젝트** 메뉴 명령입니다. 에 **새 프로젝트** 대화 상자에서 선택 된 **Visual C# | 웹** 서식 파일의 왼쪽된 창에서 선택한 트리의 **ASP.NET MVC 4 웹 응용 프로그램입니다.** 프로젝트 이름을 **PhotoGallery**, 위치를 선택 (또는 기본값을 그대로 적용)를 클릭 하 고 **확인**합니다.

    > [!NOTE]
    > 지금 만들려는 PhotoGallery ASP.NET MVC 4 솔루션 나중에 사용자 지정 합니다.

    ![새 프로젝트를 만드는](whats-new-in-aspnet-mvc-4/_static/image1.png "새 프로젝트 만들기")

    *새 프로젝트 만들기*
3. 에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서는 **인터넷 응용 프로그램** 프로젝트 템플릿과 클릭 **확인**합니다. Razor 뷰 엔진으로 선택 되어 있는지 확인 합니다.

    ![새 ASP.NET MVC 4 인터넷 응용 프로그램을 만드는](whats-new-in-aspnet-mvc-4/_static/image2.png "새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기")

    *새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기*

    > [!NOTE]
    > ASP.NET MVC 3에서 razor 구문이 도입 되었습니다. 목표의 문자 및 fast 및 워크플로 코딩 하는 유체 파일에 필요한 키 입력의 수를 최소화 하는 것입니다. Razor를 활용 하 여 기존 C# / VB 또는 다른 언어 기술을 놀라운 HTML 생성 워크플로 수 있도록 하는 템플릿 태그 구문을 제공 합니다.
4. 키를 눌러 **F5** 하는 솔루션을 실행 하 고 갱신 된 템플릿을 확인 합니다. 다음 기능을 사용해 확인할 수 있습니다.

    **최신 스타일 템플릿**

    서식 파일 갱신 된, 더 많은 현대 수준의 스타일을 제공 합니다.

    ![ASP.NET MVC 4 맞게 스타일을 다시 템플릿](whats-new-in-aspnet-mvc-4/_static/image3.png "맞게 템플릿 스타일을 다시 MVC 4")

    *ASP.NET MVC 4 맞게 스타일을 다시 템플릿*

    ![새 연락처 페이지](whats-new-in-aspnet-mvc-4/_static/image4.png "새 연락처 페이지")

    *새 연락처 페이지*

    **자동 선택 렌더링**

    체크 아웃 브라우저 창 크기 조정 고 페이지 레이아웃 새 창 크기를 동적으로 반응 방법을 확인 합니다. 이러한 템플릿은 자동 선택 렌더링 기술을 사용 하 여 사용자 지정 하지 않고 데스크톱 및 모바일 플랫폼에서 모두 올바르게 렌더링 합니다.

    ![다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿에서](whats-new-in-aspnet-mvc-4/_static/image5.png "다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿")

    *다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿*

    **JavaScript와 함께 다양 한 UI**

    기본 프로젝트 템플릿과 다른 향상 좀 더 대화형 JavaScript를 제공 하는 JavaScript 사용 하는 기능입니다. 서식 파일에 사용 된 로그인 및 등록 링크를 jQuery 유효성 검사를 사용 하 여 클라이언트 쪽에서 입력된 필드의 유효성을 검사 하는 방법을 보여 줍니다.

    ![jQuery 유효성 검사](whats-new-in-aspnet-mvc-4/_static/image6.png)

    *jQuery 유효성 검사*

    > [!NOTE]
    > 두 섹션에서는 첫 번째 섹션에 로그인 하는 예 고 두 번째 섹션 altenativelly google (기본적으로 해제 됨)와 같은 다른 인증 서비스를 사용 하 여 로그인 할 수 있습니다 및 사이트에서 registerd 계정을 사용 하 여 기록할 수 있습니다.
5. 디버거를 중지 하려면 Visual Studio로 되돌아가려면 브라우저를 닫습니다.
6. 파일을 열고 **AuthConfig.cs** 아래에 **앱\_시작** 폴더입니다.
7. 에 대 한 Google 클라이언트를 등록 하 고 마지막 줄에서 주석 제거 *OAuth* 인증 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > Facebook, Twitter, Microsoft 등과 같은 모든 OAuth 또는 OpenID 서비스를 사용 하 여 인증을 쉽게 사용할 수 있습니다를 확인 합니다.
8. 키를 눌러 **F5** 하는 솔루션을 실행 하 고 로그인 페이지로 이동 합니다.
9. 선택 **Google** 서비스에 로그인 합니다.

    ![서비스에서 로그를 선택합니다.](whats-new-in-aspnet-mvc-4/_static/image7.png)

    *서비스에서 로그를 선택합니다.*
10. Google 계정을 사용 하 여 로그인 합니다.
11. Google 계정에서 정보를 검색할 사이트 (localhost)를 허용 합니다.
12. 마지막으로, Google 계정을 연결 하는 사이트에 등록 해야 합니다.

   ![Google 계정 연결](whats-new-in-aspnet-mvc-4/_static/image8.png)

   *Google 계정 연결*
13. 디버거를 중지 하려면 Visual Studio로 되돌아가려면 브라우저를 닫습니다.
14. 이제 솔루션을 체크 아웃 프로젝트 템플릿에 있는 ASP.NET MVC 4에서 도입 된 몇 가지 다른 새로운 기능을 탐색 합니다.

   ![ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿을](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿을")

   *ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿*

   - **HTML 5 태그**

       새 테마 마크업 알아보려면 템플릿을 뷰를 찾습니다.

       ![Razor 및 HTML5 태그 About.cshtml를 사용 하 여 새 템플릿. ](whats-new-in-aspnet-mvc-4/_static/image10.png "About.cshtml Razor 및 HTML5 태그를 사용 하 여 새 서식 파일입니다.")

       *Razor 및 HTML5 태그 (About.cshtml)를 사용 하 여 새 템플릿.*
   - **업데이트 된 JavaScript 라이브러리**

       ASP.NET MVC 4 기본 서식 파일에는 이제 KnockoutJS, 풍부한 만들 수 있는 JavaScript MVVM 프레임 워크 및 JavaScript 및 HTML을 사용 하 여 응답성이 높은 웹 응용 프로그램 포함 됩니다. 마찬가지로 mvc 3, jQuery 및 jQuery UI 라이브러리도 포함 되어 ASP.NET MVC 4입니다.

     > [!NOTE]
     > 이 링크에 KnockOutJS 라이브러리에 대 한 자세한 정보를 얻을 수 있습니다: [ [ http://learn.knockoutjs.com/ ](http://learn.knockoutjs.com/) ](http://learn.knockoutjs.com/)합니다. 또한, jQuery 및 jQuery UI에 대해 알아볼 수 있습니다에 [ [ http://docs.jquery.com/ ](http://docs.jquery.com/) ](http://docs.jquery.com/)합니다.

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a>작업 2-탐색 모바일 응용 프로그램 템플릿

ASP.NET MVC 4 모바일 앱을 위해 웹 사이트 및 태블릿 브라우저의 개발을 용이 하 게 합니다. 이 템플릿은 인터넷 응용 프로그램 템플릿 (통지는 컨트롤러 코드가 거의 동일)와 동일한 응용 프로그램 구조를 갖지만 스타일은 터치 기반 모바일 장치에서 제대로 렌더링 하도록 수정 되었습니다.

1. 선택 된 **파일 | 새로 만들기 | 프로젝트** 메뉴 명령입니다. 에 **새 프로젝트** 대화 상자에서 선택 된 **Visual C# | 웹** 서식 파일의 왼쪽된 창에서 트리를 선택 하 고는 **ASP.NET MVC 4 웹 응용 프로그램입니다.** 프로젝트 이름을 **PhotoGallery.Mobile**, 위치를 선택 (또는 기본값을 그대로 적용) 선택 &quot;솔루션에 추가&quot; 클릭 **확인**합니다.
2. 에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서는 **모바일 응용 프로그램** 프로젝트 템플릿과 클릭 **확인**합니다. Razor 뷰 엔진으로 선택 되어 있는지 확인 합니다.

    ![새 ASP.NET MVC 4 모바일 응용 프로그램을 만드는](whats-new-in-aspnet-mvc-4/_static/image11.png "새 ASP.NET MVC 4 모바일 응용 프로그램 만들기")

    *새 ASP.NET MVC 4 모바일 응용 프로그램 만들기*
3. 이제 사용자는 솔루션을 탐색 하 고 체크 아웃 모바일용 ASP.NET MVC 4 솔루션 템플릿을 의해 도입 된 새로운 기능 중 일부를 수 있습니다:

    - **jQuery Mobile 라이브러리**

        모바일 응용 프로그램 프로젝트 템플릿을 있는 오픈 소스 라이브러리 모바일 브라우저 호환성을 위해 jQuery 모바일 라이브러리에 포함 됩니다. jQuery Mobile CSS 및 JavaScript를 지 원하는 모바일 브라우저에 점진적인 기능 향상을 적용 합니다. 점진적인 기능 향상에 사용 하도록 콘텐츠를 표시 하는 경우 가장 강력한 브라우저가 설정 하는 동안 웹 페이지의 기본 콘텐츠를 표시 하려면 모든 브라우저 수 있습니다. JQuery 모바일 스타일에에서 포함 된 JavaScript 및 CSS 파일, 페이지 태그에서 변경 하지 않고 화면에서 내용에 맞게 모바일 브라우저 데 도움이 됩니다.

        ![jQuery-mobile-library-included-in-the-template](whats-new-in-aspnet-mvc-4/_static/image12.png)

        *서식 파일에 포함 된 jQuery 모바일 라이브러리*
    - **HTML5 기반 태그**

        ![Mobile-application-template-using-HTML5-markup](whats-new-in-aspnet-mvc-4/_static/image13.png)

        *HTML5 태그, (Login.cshtml 및 index.cshtml)를 사용 하 여 모바일 응용 프로그램 템플릿*
4. 키를 눌러 **F5** 솔루션을 실행 합니다.
5. 열기는 **Windows Phone 7 에뮬레이터**합니다.
6. Phone 시작 화면에서 Internet Explorer를 엽니다. 데스크톱 응용 프로그램의 시작 위치 URL을 확인 하 고 전화를 통해 해당 URL로 이동 (예: `http://localhost:[PortNumber]/`).
7. 로그인 페이지를 입력 하거나 체크 아웃할 수 이제는 페이지에 대 한 합니다. 웹 사이트의 스타일은 모바일 앱을 위해 새 Metro 응용 프로그램에 따라 있는지를 확인 합니다. ASP.NET MVC 4 프로젝트 템플릿은 모든 페이지의 요소가 표시 되 고 사용할 수 있도록 하는 모바일 장치에 올바르게 표시 됩니다. 헤더에 대 한 링크를 클릭 하거나 누를 충분히 큰 되는지 확인 합니다.

    ![모바일 장치에서 서식 파일 페이지 프로젝트](whats-new-in-aspnet-mvc-4/_static/image14.png "서식 파일 페이지에서 모바일 장치 프로젝트")

    *모바일 장치에서 프로젝트 템플릿 페이지*
8. 새 템플릿을 사용 하 여도 **뷰포트 메타 태그**합니다. 대부분의 모바일 브라우저 가상 브라우저 창에 대 한 너비를 정의 하거나 &quot;뷰포트&quot;, 모바일 장치에서의 실제 너비 보다 큰 합니다. 이 통해 모바일 브라우저 가상 디스플레이로 내 전체 웹 페이지를 엽니다. **뷰포트 메타 태그** 웹 개발자가 모바일 장치에 너비, 높이 및 브라우저 영역 사이의 값을 설정할 수 있도록 **합니다.** 장치 너비에 뷰포트를 설정 하는 모바일 응용 프로그램에 대 한 ASP.NET MVC 4 템플릿 (&quot;너비 장치 너비 =&quot;) 레이아웃 템플릿에 (*Views\Shared\_Layout.cshtml*) 되도록 모든는 페이지의 뷰포트 장치 화면 너비를 설정 해야 합니다. 뷰포트 메타 태그에서 기본 브라우저 보기를 변경 하지 않는다는 것을 확인 합니다.
9. 열기  **\_Layout.cshtml**에 있는 **보기 | 공유** 폴더 및 주석 뷰포트 메타 태그입니다. 응용 프로그램을 실행 하지 않은 경우 이미 열리고 차이 확인해 보세요.


[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

![뷰포트 메타 태그를 주석 처리 한 후 사이트](whats-new-in-aspnet-mvc-4/_static/image15.png "뷰포트 메타 태그를 주석 처리 한 후 사이트")

*뷰포트 메타 태그를 주석 처리 한 후 사이트*
10. 키를 눌러 Visual Studio에서 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.
11. 뷰포트 메타 태그 주석 처리를 제거 합니다.


[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a>작업 3-자동 선택 렌더링을 사용 하 여

이 태스크에서는 사용자 지정 하지 않고 동시에 올바르게 모바일 장치 및 웹 브라우저에서 웹 페이지를 렌더링 하는 다른 방법에 설명 합니다. 유사한 용도의 뷰포트 메타 태그를 이미 사용 했습니다. 다른 강력한 방법을 부합 하는 이제: *자동 선택 렌더링*합니다.

자동 선택 렌더링은 사용 하는 기술 **CSS3 미디어 쿼리** 페이지에 적용 되는 스타일을 사용자 지정할 수 있습니다. 미디어 쿼리 조건 내 특정 조건에서 CSS 스타일을 그룹화 하 여 스타일 시트를 정의 합니다. 조건이 true 이면 하는 경우에 스타일 선언 된 개체에 적용 됩니다.

자동 선택 렌더링 방법에서 제공 하는 유연성에 서로 다른 장치에서 사이트를 표시 하기 위한 모든 사용자 지정 수 있습니다. 원하는 만큼 하나의 스타일 시트에서 논리 코드를 작성 하지 않고 스타일을 선택할 수 만큼 스타일을 정의할 수 있습니다. 따라서 중복 된 코드와 목적으로 렌더링 하기 위한 논리의 양이 줄어 대로 페이지 스타일 적용의 매우 유용한 방법입니다. 반면에 대역폭 소비 늘어나기, CSS 파일의 크기 미미 늘어나면 수 없습니다.

자동 선택 렌더링 기술을 사용 하 여 해당 사이트 수 **브라우저와 상관 없이 적절 하 게 표시 합니다.** 하지만 추가 대역폭 로드 되는 문제를 고려해 야 합니다.

> [!NOTE]
> 미디어 쿼리의 기본 형식은: @media \[범위: 모든 | 핸드헬드 | 인쇄 | 프로젝션 | 화면\] ([속성: 값] 및... [속성: 값])


미디어 쿼리 예제: &gt;  <strong>@media 모든 및 (최대 너비: 1000px) 및 (최소 너비: 700px) {}:</strong> 700px 1000px 사이의 모든 해상도 대해 합니다.

> <strong>@media 화면 및 (최소 너비: 400px) 및 (최대 너비: 700px) {...}:</strong> 화면에 대 한 합니다. 해상도 400에서 700px 사이 여야 합니다.
> 
> <strong>@media 핸드헬드 장치 및 (최소 너비: 20em), 화면 및 (최소 너비: 20em) {...}:</strong> (모바일 및 장치) 휴대 장치 및 화면에 있습니다. 최소 너비 20em 보다 커야 합니다.
> 
> 이 대 한 자세한 정보를 찾을 수 있습니다는 [W3C 사이트](http://www.w3.org/TR/css3-mediaqueries/)합니다.


이제 자동 선택 렌더링의 작동 원리를 탐색, 4는 웹 사이트 템플릿을 기본 ASP.NET MVC의 가독성을 향상 합니다.

1. 열기는 **PhotoGallery.sln** 솔루션 작업 1에서 만든 하 고 선택 된 **PhotoGallery** 프로젝트. 키를 눌러 **F5** 솔루션을 실행 합니다.
2. 브라우저의 너비 절반 또는 원래 크기의 1/4 보다 작은 창을 설정의 크기를 조정 합니다. 이 어떻게 바뀌는지 헤더의 항목과: 일부 요소 헤더의 표시 영역에 나타나지 것입니다.
3. 열기 <strong>Site.css</strong> 파일에 있는 Visual Studio 솔루션 탐색기에서 <strong>콘텐츠</strong> 프로젝트 폴더입니다. 키를 눌러 <strong>CTRL + F</strong> Visual Studio 통합된 검색을 열고 쓸 <strong>@media</strong> 찾으려고는 <strong>CSS 미디어 쿼리</strong>합니다.

    이 서식 파일에 정의 된 경우 미디어 쿼리 조건이이 방식으로 작동: 브라우저의 창 크기 미만인 **850 px**를 위해 CSS 규칙이 적용 되는이 미디어 블록 내에 정의 된 것입니다.

    ![미디어 쿼리 찾기](whats-new-in-aspnet-mvc-4/_static/image16.png "미디어 쿼리 찾기")

    *미디어 쿼리 찾기*
4. 850에 설정 된 최대 너비 특성 값을 대체와 px **10px**자동 선택 렌더링을 사용 하지 않도록 설정 하려면 한 키를 누릅니다 **CTRL + S** 여 변경 내용을 저장 합니다. 브라우저와 키를 눌러 돌아갑니다 **CTRL + f 5를 눌러** 변경 내용을 사용 하 여 페이지를 새로 고칠 수 있습니다. 창의 너비를 조정할 때 두 페이지에서 차이 알고 있습니다.

    ![페이지 왼쪽에 적용 하는 @media 스타일 오른쪽에 스타일을 생략 하면](whats-new-in-aspnet-mvc-4/_static/image17.png "페이지 왼쪽에 적용 하는 @media 스타일을 스타일 오른쪽에서을 생략 하면")

    <em>페이지 왼쪽에 적용 하는 @media 스타일을 스타일 오른쪽에서을 생략 하면</em>

    이제 모바일 장치에서 어떤 일이 생기 확인해 보겠습니다.

    ![페이지 왼쪽에 적용 하는 @media 스타일 오른쪽에 스타일을 생략 하면](whats-new-in-aspnet-mvc-4/_static/image18.png "페이지 왼쪽에 적용 하는 @media 스타일을 스타일 오른쪽에서을 생략 하면")

    <em>페이지 왼쪽에 적용 하는 @media 스타일을 스타일 오른쪽에서을 생략 하면</em>

    모바일 장치를 사용 하는 경우 페이지는 웹 브라우저에서 렌더링 될 때 변경 내용을 매우 중요 한 없는지 확인할 수 있지만 차이점 더욱 명확 하 게 됩니다. 이미지의 왼쪽에 사용자 지정 스타일 가독성 향상 되었는지 확인할 수 있습니다.

    자동 선택 렌더링에 쉽게 조건부 웹 사이트에 스타일을 지정 하 고는 깔끔한 접근 방식으로 일반 스타일 문제를 해결 하기 위해 적용 하 여 더 많은 시나리오를 사용할 수 있습니다.

    뷰포트 메타 태그 및 CSS 미디어 쿼리 ASP.NET MVC 4에 한정 되지 않는 모든 웹 응용 프로그램에서 이러한 기능을 활용 될 수 있도록 합니다.
5. 키를 눌러 Visual Studio에서 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a>연습 2: 사진 갤러리 웹 응용 프로그램 만들기

이 연습에서는 사진을 표시 하는 사진 갤러리 응용 프로그램에서 작동 합니다. ASP.NET MVC 4 프로젝트 템플릿을 사용 하 여 먼저 및 서비스에서 사진을 검색 하 고 홈 페이지에 표시 하는 기능에서 추가 합니다.

다음 연습에서는 모바일 장치에 표시 되는 방식을 강화 하기 위해이 솔루션을 업데이트 합니다.

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a>작업 1-모의 사진 서비스 만들기

이 태스크에서는 갤러리에 표시 되는 콘텐츠를 검색 하는 사진 서비스의 모의 만들게 됩니다. 이렇게 하려면 단순히 각 사진 데이터와 함께 JSON 파일을 반환 하는 새로운 컨트롤러를 추가 합니다.

1. 열기 **Visual Studio** 열려 있지 않으면입니다.
2. 선택 된 **파일 | 새로 만들기 | 프로젝트** 메뉴 명령입니다. 에 **새 프로젝트** 대화 상자에서 선택 된 **Visual C# | 웹** 서식 파일의 왼쪽된 창에서 선택한 트리의 **ASP.NET MVC 4 웹 응용 프로그램입니다.** 프로젝트 이름을 **PhotoGallery**, 위치를 선택 (또는 기본값을 그대로 적용)를 클릭 하 고 **확인**합니다. 기존 ASP.NET MVC 4 프로그램에서 작업을 계속할 수 또는 **인터넷 응용 프로그램** 솔루션에서 **연습 1** 하 고 다음 단계를 건너뜁니다.
3. 에 **새 ASP.NET MVC 4 프로젝트** 대화 상자는 **인터넷 응용 프로그램** 프로젝트 템플릿과 클릭 **확인**합니다. Razor 뷰 엔진으로 선택 되어 있는지 확인 합니다.
4. 에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **앱\_데이터** 프로젝트 및 선택의 폴더 **추가 | 기존 항목**합니다. 찾아는 **Source\Assets\App\_데이터** 이 랩의 폴더를 추가 하 고는 **Photos.json** 파일입니다.
5. 만들 새 컨트롤러 이름의 **PhotoController**합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **컨트롤러** 폴더를 이동 **추가** 선택 **컨트롤러입니다.** 컨트롤러 이름을 작성, 둡니다는 **빈 MVC 컨트롤러** 템플릿을 **추가**합니다.

    ![추가 PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "는 PhotoController 추가")

    *PhotoController 추가*
6. 대체는 **인덱스** 메서드를 다음 **갤러리** 작업 및 최근에 프로젝트에 추가한 JSON 파일에서 콘텐츠를 반환 합니다.

    (코드 조각- *ASP.NET MVC 4-Ex02-랩 갤러리 실행*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. 키를 눌러 **F5** 솔루션을 실행 하 여 다음 모의 사진 서비스를 테스트 하려면 다음 URL로 이동: `http://localhost:[port]/photo/gallery` ([port] 값 응용 프로그램이 시작 된 현재 포트에 따라 다름). 이 URL로 요청 콘텐츠를 검색 해야는 **Photos.json** 파일입니다.

    ![모의 사진 서비스 테스트](whats-new-in-aspnet-mvc-4/_static/image20.png "모의 사진 서비스 테스트")

    *모의 사진 서비스 테스트*

실제 구현에서 사용할 수 있습니다 [ASP.NET Web API](../../../../web-api/index.md) 사진 갤러리 서비스를 구현 하 합니다. ASP.NET Web API는 브라우저 및 모바일 장치를 비롯한 광범위한 클라이언트에 연결하는 HTTP 서비스를 쉽게 빌드할 수 있게 해 주는 프레임워크입니다. ASP.NET Web API는 .NET Framework에서 RESTful 응용 프로그램을 빌드하는 데 이상적인 플랫폼입니다.

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a>작업 2-사진 갤러리를 표시 합니다.

이 작업에서는이 작업의 첫 번째 작업에서 만든 모의 서비스를 사용 하 여 사진 갤러리를 표시 하려면 홈 페이지를 업데이트 합니다. 모델 파일을 추가 하 고 갤러리 보기를 업데이트 합니다.

1. 키를 눌러 Visual Studio에서 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.
2. 만들기는 **사진** 클래스에 **모델** 폴더입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **모델** 폴더를 **추가** 클릭 **클래스**합니다. 그런 다음 이름으로 설정할 **Photo.cs** 클릭 **추가**합니다.
3. 다음 멤버를 추가할는 **사진** 클래스입니다.

    (코드 조각- *ASP.NET MVC 4 랩-Ex02-사진 모델*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. **컨트롤러** 폴더에서 **HomeController.cs** 파일을 엽니다.
5. 다음 using 문을 추가합니다.

    (코드 조각- *ASP.NET MVC 4-Ex02-랩 HomeController Using*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. 업데이트는 **인덱스** 동작을 사용 하 여 **HttpClient** 갤러리 데이터 검색을 사용 하 여는 **JavaScriptSerializer** 뷰 모델을 deserialize 하는 데 있습니다.

    (코드 조각- *ASP.NET MVC 4-Ex02-랩 인덱스 동작*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. 열기는 **Index.cshtml** 아래에 있는 파일의 **Views\Home** 폴더 및 모든 콘텐츠를 다음 코드로 바꿉니다.

    이 코드는 서비스에서 검색 된 모든 사진 하는 순서가 지정 되지 않은 목록으로 표시입니다.

    (코드 조각- *ASP.NET MVC 4-Ex02-랩 사진 목록*)

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. 에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **콘텐츠** 프로젝트 및 선택의 폴더 **추가 | 기존 항목**합니다. 찾아는 **Source\Assets\Content** 이 랩의 폴더를 추가 하 고는 **Site.css** 파일입니다. 대체를 확인 해야 합니다. 있는 경우는 **Site.css** 파일을 열 수, 파일을 다시 로드할지도 확인 해야 합니다.
9. 파일 탐색기를 열고 전체를 복사 **사진** 폴더 아래에 **Source\Assets** 솔루션 탐색기에서 프로젝트의 루트 폴더에이 랩의 폴더입니다.
10. 응용 프로그램을 실행합니다. 이제 갤러리에는 사진 표시 홈 페이지가 나타납니다.

    ![사진 갤러리](whats-new-in-aspnet-mvc-4/_static/image21.png "사진 갤러리")

    *사진 갤러리*
11. 키를 눌러 Visual Studio에서 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a>연습 3: 모바일 장치에 대 한 지원 추가

ASP.NET MVC 4에서 키 업데이트 중 하나에 모바일 개발에 대 한 지원입니다. 이 연습에서는, 이전 연습에서 만든 PhotoGallery 솔루션을 확장 하 여 ASP.NET MVC 4 모바일 응용 프로그램에 대 한 새로운 기능을 탐색 합니다.

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a>작업 1-ASP.NET MVC 4 응용 프로그램에서 jQuery Mobile 설치

1. 열기는 **시작** 솔루션에 있는 **소스/Ex3-MobileSupport/시작/** 폴더입니다. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 열기는 **패키지 관리자 콘솔** 클릭 하 여는 **도구** &gt; **라이브러리 패키지 관리자** &gt; **패키지 관리자 콘솔** 메뉴 옵션입니다.

    ![NuGet 패키지 관리자 콘솔을 열고](whats-new-in-aspnet-mvc-4/_static/image22.png "NuGet 패키지 관리자 콘솔을 열고")

    *NuGet 패키지 관리자 콘솔 열기*
3. 패키지 관리자 콘솔에서 설치 하려면 다음 명령을 실행 하는 **jQuery.Mobile.MVC** 패키지 합니다.

    jQuery Mobile은 터치에 최적화 된 웹 UI를 작성 하기 위한 오픈 소스 라이브러리. JQuery Mobile ASP.NET MVC 4 응용 프로그램을 사용 하는 도우미 jQuery.Mobile.MVC NuGet 패키지에 포함 합니다.

    > [!NOTE]
    > 다음 명령은 실행 하 여 있습니다 됩니다 수 jQuery.Mobile.MVC 라이브러리에서에서 다운로드 Nuget 합니다.

    PM

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    이 명령은 jQuery Mobile 및 다음을 비롯 한 일부 도우미 파일을 설치 합니다.

    - **뷰/공유/\_Layout.Mobile.cshtml**: jQuery Mobile 기반 레이아웃을 더 작은 화면에 맞게 최적화 됩니다. 웹 사이트의 모바일 브라우저에서 요청을 받으면 원래 레이아웃 바뀝니다 (\_Layout.cshtml)이 있습니다.
    - 뷰 전환기 구성 요소: 이루어져는 **뷰/공유/\_ViewSwitcher.cshtml** 부분 뷰 및 **ViewSwitcherController.cs** 컨트롤러입니다. 이 구성 요소는 사용자가 페이지의 데스크톱 버전으로 전환할 수 있도록 모바일 브라우저에 링크를 표시 됩니다.  
        ![모바일 지원 사진 갤러리 프로젝트](whats-new-in-aspnet-mvc-4/_static/image23.png "사진 갤러리 프로젝트 모바일 지원")

        *사진 갤러리 프로젝트 모바일 지원*
4. 모바일 번들을 등록 합니다. 이 작업을 수행 하려면 엽니다는 **Global.asax.cs** 파일을 다음 줄을 추가 합니다.

    (코드 조각- *ASP.NET MVC 4-Ex03-랩 레지스터 모바일 번들*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. 데스크톱 웹 브라우저를 사용 하 여 응용 프로그램을 실행 합니다.
6. 열기는 **Windows Phone 7 Emulator** 에 **시작 메뉴 | 모든 프로그램 | Windows Phone SDK 7.1 | Windows Phone 에뮬레이터입니다.**
7. Phone 시작 화면에서 Internet Explorer를 엽니다. 응용 프로그램을 시작할 URL을 확인 하 고 전화 브라우저와 해당 URL로 이동 (예: `http://localhost:[PortNumber]/`).

    jQuery.Mobile.MVC 모바일 장치에 대 한 액세스에 최적화 된 뷰를 표시 하는 프로젝트에서 새 자산을 만들 때 응용 프로그램이 Windows Phone 에뮬레이터에서 다르게 표시를 확인할 수 있습니다.

    데스크톱 보기로 전환 하는 링크를 보여 주는 전화를 맨 위에 있는 메시지를 확인 합니다. 또한는  **\_Layout.Mobile.cshtml** 레이아웃 설치 패키지에 의해 생성 된 응용 프로그램에서 다른 레이아웃이 포함 되어 있습니다.

    > [!NOTE]
    > 지금까지 모바일 보기에 복귀할의 연결이 없습니다. 이상 버전에 포함 됩니다.

    ![사진 갤러리 홈 페이지의 모바일 뷰](whats-new-in-aspnet-mvc-4/_static/image24.png "사진 갤러리 홈 페이지의 모바일 뷰")

    *사진 갤러리 홈 페이지의 모바일 뷰*
8. 키를 눌러 Visual Studio에서 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a>작업 2-모바일 뷰 만들기

이 태스크에서는 모바일 장치에서 더 나은 appareance에 적용할 콘텐츠로 인덱스 보기의 모바일 버전이 만들어집니다.

1. 복사는 **Views\Home\Index.cshtml** 확인 하 고 붙여 넣어 복사본을 만들고, 새 파일을 이름를 **Index.Mobile.cshtml**합니다.
2. 새 만든 열기 **Index.Mobile.cshtml** 보기 및 기존 바꾸기 &lt;ul&gt; 이 코드로 태그입니다. 이 통해 업데이트 됩니다.는 &lt;ul&gt; jQuery 모바일 데이터의 주석에서 jQuery 모바일 테마를 사용 하는 태그입니다.

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > 다음 사항을 참고하세요.
    > 
    > - **데이터 역할** 특성이로 설정 **listview** listview 스타일을 사용 하 여 목록을 렌더링 합니다.
    > 
    > - **데이터 inset** 특성이 true로 설정 둥근된 테두리 및 여백을 사용 하 여 목록에 표시 됩니다.
    > 
    > - **데이터 필터** 특성이로 설정 **true** 검색 상자를 생성 합니다.
    > 
    > JQuery 모바일 규칙 프로젝트 문서에 대해 자세히 알아볼 수 있습니다. [[http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)
3. 키를 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.
4. 전환 하는 **Windows Phone 에뮬레이터** 사이트를 새로 고칩니다. 갤러리 목록 뿐만 아니라 새로운 검색 상자 위쪽에 있는의 새로운 디자인을 확인 합니다. 그런 다음 검색 상자에 단어를 입력 (예를 들어, **Tulips**) 사진 갤러리에서 검색을 시작 하려면.

    ![필터링 된 listview 스타일을 사용 하 여 갤러리](whats-new-in-aspnet-mvc-4/_static/image25.png "listview 스타일을 사용 하 여 필터링 된 갤러리")

    *필터링 된 listview 스타일을 사용 하 여 갤러리*

    요약 하면,를 사용 하 여 보기 Mobilizer 조리법 사용 하 여 인덱스 뷰의 복사본을 만들고는 &quot;모바일&quot; 접미사입니다. 이 접미사 모바일 장치에서 생성 된 모든 요청은 인덱스의이 복사본 사용 하 여 ASP.NET MVC 4를 나타냅니다. 또한 모바일 장치에 있는 사이트 디자인을 향상 시키기 위한 jQuery Mobile을 사용 하 여 인덱스 뷰의 모바일 버전을 업데이트 했습니다.
5. Visual Studio로 다시 이동 및 열기 **Site.Mobile.css** 아래에 **콘텐츠** 폴더입니다.
6. 이미지의 오른쪽에 표시 되도록 사진 제목의 위치를 수정 합니다. 이렇게 하려면 다음 코드를 추가 **Site.Mobile.css** 파일입니다.

    CSS

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. 키를 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.
8. 로 다시 전환는 **Windows Phone 에뮬레이터** 사이트를 새로 고칩니다. 공지 사진 제목 제대로 이제에 배치 됩니다.

    ![이미지의 오른쪽에 배치 하는 제목](whats-new-in-aspnet-mvc-4/_static/image26.png "이미지의 오른쪽에 배치 하는 제목")

    *이미지의 오른쪽에 배치 하는 제목*

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a>작업 3-jQuery Mobile 테마

모든 레이아웃 및 jQuery Mobile 위젯의 새로운 개체 지향 CSS 프레임 워크 사이트 및 응용 프로그램에 완전히 통합 된 비주얼 디자인 테마를 적용할 수 있도록 하 여 설계 됩니다.

jQuery Mobile 기본 테마 문자 권한이 부여 된 5 견본 포함 (a, b, c, d, e)에 대해 빠른 참조입니다.

이 태스크에서는 모바일 사용할 레이아웃을 기본값 보다 다양 한 테마를 업데이트 합니다.

1. Visual Studio로 다시 전환 합니다.
2. 열기는  **\_Layout.Mobile.cshtml** 에 있는 파일 **Views\Shared**합니다.
3. 로 설정 하는 데이터-역할 div 요소를 찾은 &quot;페이지&quot; 하 고 업데이트는 **데이터 테마** 를 &quot; **e**&quot;합니다.

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. 키를 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.
5. 사이트 새로 고침의 **Windows Phone 에뮬레이터** 새 색 구성표를 확인 합니다.

    ![다른 색 구성표를 사용 하는 모바일 레이아웃](whats-new-in-aspnet-mvc-4/_static/image27.png "다른 색 구성표를 사용 하는 모바일 레이아웃")

    *다른 색 구성표를 사용 하는 모바일 레이아웃*

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a>4-뷰 전환기 구성 요소 및 기능을 재정의 하는 브라우저를 사용 하 여 작업

모바일 액세스에 최적화 된 웹 페이지에 대 한 규칙 텍스트가 리 바탕 화면 보기 또는 사용자가 페이지의 데스크톱 버전으로 전환할 수 있는 전체 사이트 모드와 같은 링크를 추가 하는 것입니다. JQuery.Mobile.MVC 패키지에는 샘플이 들어 **뷰 전환기** 에 사용 되는이 목적을 위해 구성 요소는  **\_Layout.Mobile.cshtml** 보기.

![데스크톱 보기로 전환 하려면 링크](whats-new-in-aspnet-mvc-4/_static/image28.png "링크 데스크톱 보기로 전환 하려면")

*데스크톱 보기로 전환에 연결*

라는 새로운 기능을 사용 하 여 뷰 전환기 **브라우저 재정의**합니다. 이 기능에는 다른 브라우저 (사용자 에이전트)에서 실제로 생성 되는 것에서 온 요청 처럼 처리할 응용을 프로그램 수 있습니다.

이 태스크에서는 샘플 구현 jQuery.Mobile.MVC 및 ASP.NET MVC 4의 기능을 재정의 하는 새 브라우저 추가 뷰 전환기를 탐색 합니다.

1. Visual Studio로 다시 전환 합니다.
2. 열기는  **\_Layout.Mobile.cshtml** 보기 아래에 **Views\Shared** 폴더 및 부분 뷰로 참조 하 고 뷰 전환기 구성 요소를 표시 합니다.

    ![뷰 전환기 구성 요소를 사용 하 여 모바일 레이아웃](whats-new-in-aspnet-mvc-4/_static/image29.png "뷰 전환기 구성 요소를 사용 하 여 모바일 레이아웃")

    *뷰 전환기 구성 요소를 사용 하 여 모바일 레이아웃*
3. 열기는  **\_ViewSwitcher.cshtml** 부분 뷰입니다.

    새 메서드를 사용 하는 부분 뷰 **ViewContext.HttpContext.GetOverriddenBrowser()** 하 웹 요청의 원점을 확인 하 고 데스크톱 또는 모바일 뷰를 전환 하려면 해당 링크를 표시 합니다.

    **GetOverridenBrowser** 메서드가 반환 되는 **HttpBrowserCapabilitiesBase** 사용자 에이전트 요청에 대 한 현재 설정에 해당 하는 인스턴스 (실제 또는 재정의). 이 값을 사용 하 여 같은 속성을 가져오는 **IsMobileDevice**합니다.

    ![부분 뷰 ViewSwitcher](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher 부분 뷰")

    *ViewSwitcher 부분 뷰*
4. 열기는 **ViewSwitcherController.cs** 클래스는 **컨트롤러** 폴더입니다. 체크 아웃 해당 SwitchView 작업 ViewSwitcher 구성 요소에 있는 링크에 의해 호출 되 고 새 HttpContext 메서드 확인 합니다.

    - **HttpContext.ClearOverridenBrowser()** 메서드는 현재 요청에 대 한 재정의 된 사용자 에이전트를 제거 합니다.
    - **HttpContext.SetOverridenBrowser()** 메서드가 지정된 된 사용자 에이전트를 사용 하 여 요청의 실제 사용자 에이전트 값을 재정의 합니다.  
        ![ViewSwitcher 컨트롤러](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher 컨트롤러")  
*ViewSwitcher 컨트롤러*

        브라우저 재정의 사용 하지 않는 jQuery.Mobile.MVC 패키지를 설치 하지 않는 경우에 ASP.NET MVC 4의 핵심 기능입니다. 그러나이 기능에는 뷰, 레이아웃 및 부분 뷰 영향을 받으며 Request.Browser 개체에 종속 되는 기능의 변경 되지 않습니다.

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a>작업 5-바탕 화면 보기에 있는 뷰 전환기를 추가 합니다.

이 태스크에서는 데스크톱 레이아웃 뷰 전환기를 포함 하도록 업데이트 됩니다. 이렇게 하면 모바일 사용자가 바탕 화면 보기를 탐색할 때 모바일 보기도 다시 돌아가십시오.

1. 사이트를 새로 고 **Windows Phone 에뮬레이터**합니다.
2. 클릭는 **바탕 화면 보기** 갤러리의 위쪽에 링크 합니다. 모바일 보기를 반환할 수 있도록 바탕 화면 보기에 없는 뷰 전환기 것을 볼 수 있습니다.
3. Visual Studio로 다시 이동 및 열기는  **\_Layout.cshtml** 보기.
4. 로그인 섹션을 찾아 렌더링에 대 한 호출을 삽입의  **\_ViewSwitcher** 아래 부분 뷰는  **\_LogOnPartial** 부분 뷰입니다. 그런 다음 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. 키를 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.
6. Windows Phone 에뮬레이터에서 페이지를 새로 고치고 확대 하려면 화면을 두 번 클릭 합니다. 홈 페이지에 이제 표시에 **모바일 보기** 모바일에서 데스크톱 보기로 전환 하는 링크입니다.

    ![바탕 화면 보기에서 렌더링 전환기 볼](whats-new-in-aspnet-mvc-4/_static/image32.png "뷰 전환기 바탕 화면 보기에서 렌더링")

    *바탕 화면 보기에서 렌더링 된 뷰 전환기*
7. 모바일 뷰로 다시 전환 하 고 찾아보기 <strong>에 대 한</strong> 페이지 (http://localhost[port]/Home/About). About.Mobile.cshtml 보기를 만들지 않은 경우에 정보 페이지 표시 되는지 확인 모바일 레이아웃을 사용 하 여 (\_Layout.Mobile.cshtml).

    ![페이지에 대 한](whats-new-in-aspnet-mvc-4/_static/image33.png "페이지에 대 한")

    *페이지 정보*
8. 마지막으로, 데스크톱 웹 브라우저에서 사이트를 엽니다. 이전 업데이트에 영향을 미치지 않습니다 바탕 화면 보기를 확인 합니다.

    ![바탕 화면 보기 PhotoGallery](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery 바탕 화면 보기")

    *PhotoGallery 바탕 화면 보기*

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a>태스크 6-새 디스플레이 모드 만들기

새 디스플레이 모드 기능을 사용 하는 응용 프로그램 요청을 생성 하는 브라우저에 따라 보기를 선택 합니다. 예를 들어 데스크톱 브라우저 홈 페이지를 요청 하는 경우 응용 프로그램은 반환 된 **Views\Home\Index.cshtml** 서식 파일입니다. 그런 다음 모바일 브라우저 홈 페이지를 요청 하는 경우 응용 프로그램은 반환 된 **Views\Home\Index.mobile.cshtml** 서식 파일입니다.

이 태스크에서는 iPhone 장치에 대 한 사용자 지정된 레이아웃을 만듭니다 및 iPhone 장치에서 요청을 시뮬레이션 해야 합니다. 이 위해 중 하나는 iPhone 에뮬레이터/시뮬레이터를 사용할 수 있습니다 (같은 [Electric 모바일 시뮬레이터](http://www.electricplum.com/)) 또는 사용자 에이전트를 수정 하는 추가 기능을 사용 하 여 브라우저. Safari 브라우저에서 사용자 에이전트 문자열을 설정 하는 방법에는 iPhone을 에뮬레이션 하기 위해 지침은 [Safari 있다고 생각 IE 되 게 하는 방법](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) David Alison 블로그에서.

**이 작업은 선택 사항 실행 하지 않고 랩 전체에서 계속 수에 유의 하십시오.**

1. 키를 눌러 Visual Studio에서 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.
2. 열기 **Global.asax.cs** 다음 추가 문을 사용 하 여 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. 응용 프로그램에 다음 강조 표시 된 코드를 추가\_메서드를 시작 합니다.

    (코드 조각- *ASP.NET MVC 4 랩-Ex03-iPhone DisplayMode*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

새 등록 **라는 DefaultDisplayMode &quot;iPhone&quot;**, 정적 내 **DisplayModeProvider.Instance.Modes** 과 일치 하는 정적 목록 들어오는 각 요청 합니다. 들어오는 요청에는 문자열이 포함 되어 있으면 &quot;iPhone&quot;, ASP.NET MVC에서 이름이 포함 하는 뷰를 찾습니다는 &quot;iPhone&quot; 접미사입니다. 매개 변수 0 특정는 새 모드; 나타냅니다. 이 뷰는 일반적인 보다 구체적인 예를 들어, &quot;.mobile&quot; 모바일 장치의 요청을에서 일치 하는 규칙입니다.

응용 프로그램을 사용 하는 iPhone 브라우저 요청을 생성 하는 경우이 코드가 실행 된 후 합니다는 **Views\Shared\\_Layout.iPhone.cshtml** 레이아웃에서 다음 단계를 만듭니다.

> [!NOTE]
> 이러한 방식의 iPhone 데모 용도로 간소화 되었습니다 (예에서는 테스트는 대/소문자 구분) 예의 모든 iPhone 사용자 에이전트 문자열에 대해 예상 대로 작동 하지 않을 수에 대 한 요청을 테스트 합니다.

4. 복사본을 만듭니다는  **\_Layout.Mobile.cshtml** 파일에 **Views\Shared** 폴더에 복사본의 이름을 바꾼 및 &quot; **\_Layout.iPhone.csthml**&quot;.
5. 열기  **\_Layout.iPhone.csthml** 이전 단계에서 만든 합니다.
6. 데이터 역할 특성 설정 하 여 div 요소를 찾아 **페이지** 변경 하 고는 **데이터 테마** 특성을 &quot; **는**&quot;합니다.


[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

이제 ASP.NET MVC 4 응용 프로그램에서 3 레이아웃을 사용할 수 있습니다.

1. **\_Layout.cshtml**: 데스크톱 브라우저의 경우에 사용 되는 기본 레이아웃 합니다.
2. **\_Layout.mobile.cshtml**: 모바일 장치에 사용 되는 기본 레이아웃 합니다.
3. **\_Layout.iPhone.cshtml**: 구별 하기 위해 다른 색 구성표를 사용 하는 iPhone 장치에 대 한 특정 레이아웃 \_Layout.mobile.cshtml 합니다.
7. 키를 눌러 **F5** 응용 프로그램을 실행 하 고 사이트에서 탐색 하 고 **Windows Phone 에뮬레이터**합니다.
8. 열기는 **iPhone 시뮬레이터** (참조 [부록 C](#AppendixC) 설치 하 고 iPhone 시뮬레이터가 구성 하는 방법에 대 한 지침은), 너무 사이트를 찾습니다. 각 전화는 특정 템플릿을 사용 하 고 있는지 확인 합니다.

    ![Using-different-views-for-each-mobile-device2](whats-new-in-aspnet-mvc-4/_static/image35.png)

    *서로 다른 뷰를 사용 하 여 각 모바일 장치에 대 한*

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a>연습 4: 비동기 컨트롤러를 사용 하 여

Microsoft.NET Framework 4.5에서는 C# 및 Visual Basic로 비동기.NET 프로그래밍에 대 한 새 기초를 제공 하는 새로운 언어 기능을 소개 합니다. 이 새 foundation 비슷합니다-쉽고 약-동기 프로그래밍으로 간단한 비동기 프로그래밍을 사용 하십시오. ASP.NET MVC 4의 비동기 작업 메서드를 사용 하 여 쓸 수는 **AsyncController** 클래스입니다. 장기 실행에 대 한 비동기 작업 메서드를 사용할 수 있는데, CPU 바인딩되지 않은 요청 합니다. 이렇게 차단 하는 웹 서버의 요청 처리 되는 동안 작업을 수행 합니다. AsyncController 클래스는 일반적으로 장기 실행 웹 서비스 호출에 사용 됩니다.

이 연습에서는 ASP.NET MVC 4의 비동기 작업의 기본 사항을 설명합니다. 심층 분석 하려는 경우에 다음 문서 아웃 확인할 수 있습니다. [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a>작업 1-비동기 컨트롤러를 구현 합니다.

1. 열기는 **시작** 솔루션에 있는 **소스/Ex4-Async/시작/** 폴더입니다. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 열기는 **HomeController.cs** 에서 클래스는 **컨트롤러** 폴더입니다.
3. 다음 추가 문을 사용 하 여 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. 업데이트는 **HomeController** 클래스에서 상속 하도록 **AsyncController**합니다. 컨트롤러 AsyncController에서 파생 되는 비동기 요청을 처리 하는 ASP.NET을 사용 하 고 여전히 서비스 동기 작업 메서드 할 수 있습니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. 추가 **비동기** 키워드를는 **인덱스** 메서드 형식을 반환 하 고 **작업&lt;ActionResult&gt;** 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > **비동기** 키워드를 사용 하면.NET Framework 4.5를 제공 하는 새 키워드 중 하나인;이 메서드에 비동기 코드를 포함 하는 컴파일러 표시 합니다. A **작업** 개체는 특정 시점에 나중에 완료할 수 있는 비동기 작업을 나타냅니다.
6. 대체는 **클라이언트입니다. GetAsync()** 아래와 같이 await 키워드를 사용 하 여 전체 비동기 버전 사용 하 여 호출 합니다.

    (코드 조각- *ASP.NET MVC 4-Ex04-랩 GetAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > 사용 하 던 이전 버전에서의 **결과** 속성은 **작업** 결과 (동기화 버전)를 반환 될 때까지 스레드를 차단 하는 개체입니다.
    > 
    > 추가 **await** 키워드를 메서드 호출에서 반환 된 작업을 비동기적으로 기다리는 컴파일러에 알립니다. 즉, 코드의 나머지 대기 중이 던된 메서드가 완료 된 후에 콜백으로 실행 됩니다. 다른 눈에 띄는 것은이 작동 될 수 있도록 하기 위해 try / catch 블록을 변경할 필요가 없습니다: 프레임 워크에서 제공 된 처리기를 사용 하는 추가 작업 없이 포그라운드 또는 백그라운드에서 발생 하는 예외를 발생 계속 됩니다.
7. 아래와 같이 새 코드 줄을 대체 하 여 비동기 구현의을 계속 하는 코드 변경

    (코드 조각- *ASP.NET MVC 4-Ex04-랩 ReadAsStringAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. 응용 프로그램을 실행합니다. 크게 변경 되지를 확인할 수 있지만 코드 스레드 풀은 서버 리소스의 더 나은 사용량 및 성능 향상에서 스레드를 차단 하지 않습니다.

    > [!NOTE]
    > 랩에 새로운 비동기 프로그래밍 기능에 대 한 자세히 알아볼 수 있습니다 &quot; **C# 및 Visual Basic.NET 4.5의 비동기 프로그래밍** &quot; Visual Studio 트레이닝 키트에 포함 합니다.

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a>작업 2-취소 토큰 인 처리 제한 시간

작업 인스턴스를 반환 하는 비동기 작업 메서드에 시간 제한도 지원할 수 있습니다. 이 작업의 취소 토큰을 사용 하 여 제한 시간 시나리오를 처리 하는 인덱스 메서드 코드를 업데이트 합니다.

1. Visual Studio 및 키를 눌러로 돌아가서 **SHIFT + f 5를 눌러** 디버깅을 중지 합니다.
2. 다음 코드를 추가 하는 문을 사용 하는 **HomeController.cs** 파일입니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. 받을 인덱스 동작을 업데이트 한 **CancellationToken** 인수입니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. 업데이트는 **GetAsync** 호출 취소 토큰을 전달 합니다.

    (코드 조각- *CancellationToken과 함께 ASP.NET MVC 4-Ex04-랩 SendAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. 데코 레이트는 *인덱스* 메서드는 **AsyncTimeout** 특성이 500 밀리초로 설정 및 **HandleError** 처리 하도록 구성 하는 특성  **TaskCanceledException** 리디렉션하여는 **TimedOut** 보기.

    (코드 조각- *ASP.NET MVC 4-Ex04-랩 특성*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. 열기는 **PhotoController** 클래스 및 업데이트는 **갤러리** 메서드를 장기 실행 작업을 시뮬레이션 하는 실행 1000 밀리초 (1 초)을 지연 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. 열기는 **Web.config** 파일을 다음 요소를 추가 하 여 사용자 지정 오류를 사용 합니다.

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. 새 보기 만들기 **Views\Shared** 라는 **TimedOut** 및 기본 레이아웃을 사용 합니다. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭는 **Views\Shared** 폴더를 선택 **추가 | 보기**합니다.

    ![각 모바일 장치에 대 한 서로 다른 뷰를 사용 하 여](whats-new-in-aspnet-mvc-4/_static/image36.png "서로 다른 뷰를 사용 하 여 각 모바일 장치에 대 한")

    *서로 다른 뷰를 사용 하 여 각 모바일 장치에 대 한*
9. 업데이트는 **TimedOut** 아래와 같이 콘텐츠를 보고 합니다.

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. 응용 프로그램을 실행 하 고 루트 URL로 이동 합니다. 추가한는 **Thread.Sleep** 1000 밀리초에서 생성 된 시간 제한 오류를 얻게 됩니다는 **AsyncTimeout** 특성과 여 catch는 **HandleError** 특성입니다.

    ![처리 시간 제한 예외](whats-new-in-aspnet-mvc-4/_static/image37.png "처리 시간 제한 예외")

    *처리 시간 제한 예외*

> [!NOTE]
> 다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수는 또한 [부록 d: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixD)합니다.


<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩에서 있습니다 한 관찰 된 새로운 기능 중 일부에 ASP.NET MVC 4. 다음과 같은 개념을 설명 했습니다.

- ASP.NET MVC 프로젝트 템플릿을 포함 한 새로운 모바일 응용 프로그램 프로젝트 템플릿을에 향상 된 기능을 활용
- HTML5 뷰포트 특성 및 CSS 미디어 쿼리를 사용 하 여 모바일 장치에 표시를 향상 시키기
- JQuery Mobile 점진적 향상 된 기능에 대 한 터치에 최적화 된 웹 UI를 작성 하기 위한 사용
- 모바일 전용 뷰 만들기
- 뷰 전환기 구성 요소를 사용 하 여 응용 프로그램에 모바일 및 데스크톱 뷰 사이 전환 하려면
- 비동기 컨트롤러 작업 지원을 사용 하 여 만들기

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>부록 a: 코드 조각을 사용 하 여

코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다. 랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.

![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](whats-new-in-aspnet-mvc-4/_static/image38.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")

*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*

***키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드를 삽입 하려는 위치에 커서를 놓습니다.
2. 공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.
3. IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.
4. 올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).
5. 커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.

![코드 조각 이름을 입력 하기 시작](whats-new-in-aspnet-mvc-4/_static/image39.png "조각 이름을 입력 하기 시작")

*코드 조각 이름을 입력 하기 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각 선택](whats-new-in-aspnet-mvc-4/_static/image40.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")

*Tab 키를 눌러 강조 표시 된 코드 조각 선택*

![확장 하 고 Tab 키를 눌러 다시 코드 조각](whats-new-in-aspnet-mvc-4/_static/image41.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")

*확장 하 고 Tab 키를 눌러 다시 코드 조각*

***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.
2. 선택 **조각 삽입** 이어서 **내 코드 조각**합니다.
3. 클릭 하 여 목록에서 관련 조각을 선택 합니다.

![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](whats-new-in-aspnet-mvc-4/_static/image42.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")

*코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*

![클릭 하 여 목록에서 관련 조각을 선택](whats-new-in-aspnet-mvc-4/_static/image43.png "클릭 하 여 목록에서 관련 조각을 선택")

*클릭 하 여 목록에서 관련 조각을 선택합니다*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>부록 b: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여 **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)**. 다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.

1. 로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다. 또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Windows Azure SDK와</em>&quot;합니다.
2. 클릭 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.

    ![Visual Studio Express 설치](whats-new-in-aspnet-mvc-4/_static/image44.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건 동의](whats-new-in-aspnet-mvc-4/_static/image45.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](whats-new-in-aspnet-mvc-4/_static/image46.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **마침**합니다.

    ![설치 완료](whats-new-in-aspnet-mvc-4/_static/image47.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.

    ![웹 타일에 대 한 VS Express](whats-new-in-aspnet-mvc-4/_static/image48.png)

    *웹 타일에 대 한 VS Express*

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a>부록 c: 설치 WebMatrix 2 및 iPhone 시뮬레이터

시뮬레이션 된 iPhone 장치에서 사이트를 실행 하려면 WebMatrix 확장을 사용할 수 있습니다 &quot;iPhone에 대 한 전기 모바일 시뮬레이터&quot;합니다. 또한 Visual Studio 2012에서 시뮬레이터를 실행 하려면 같은 확장 프로그램을 구성할 수 있습니다.

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a>작업 1-WebMatrix 2 설치

1. 로 이동 [ [ https://go.microsoft.com/?linkid=9809776 ](https://go.microsoft.com/?linkid=9809776) ](https://go.microsoft.com/?linkid=9810169)합니다. 또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>WebMatrix 2</em>&quot;합니다.
2. 클릭 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.

    ![WebMatrix 2 설치](whats-new-in-aspnet-mvc-4/_static/image49.png "WebMatrix 2를 설치 합니다.")

    *WebMatrix 2를 설치 합니다.*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건 동의](whats-new-in-aspnet-mvc-4/_static/image50.png "사용 조건 동의")

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](whats-new-in-aspnet-mvc-4/_static/image51.png "설치 진행률")

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **마침**합니다.

    ![설치가 완료](whats-new-in-aspnet-mvc-4/_static/image52.png "설치 완료")

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a>작업 2-iPhone 시뮬레이터 확장 설치

1. 실행 **WebMatrix** 및 모든 기존 웹 사이트를 열거나 새로 만듭니다.
2. 클릭는 **실행** 에서 단추는 **홈** 리본 및 선택 **새로 추가**합니다.

    ![새 WebMatrix 확장을 추가](whats-new-in-aspnet-mvc-4/_static/image53.png "새 WebMatrix 확장을 추가 합니다.")

    *새 WebMatrix 확장을 추가합니다.*
3. 선택 **iPhone 시뮬레이터** 클릭 **설치**합니다.

    ![WebMatrix 확장을 검색](whats-new-in-aspnet-mvc-4/_static/image54.png "WebMatrix 검색 확장")

    *WebMatrix 확장 검색*
4. 패키지 세부 정보 클릭 **설치** 확장 설치를 계속 하려면.

    ![iPhone 시뮬레이터 확장](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone 시뮬레이터 확장")

    *iPhone 시뮬레이터 확장*
5. 읽고 확장 EULA에 동의 합니다.

    ![WebMatrix 확장 EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix 확장 EULA")

    *WebMatrix 확장 EULA*
6. 이제, 실행할 수 있습니다 웹 사이트가 WebMatrix에서 iPhone 시뮬레이터 옵션을 사용 하 여 합니다.

    ![IPhone을 사용 하 여 실행](whats-new-in-aspnet-mvc-4/_static/image57.png "iPhone을 사용 하 여 실행")

    *IPhone을 사용 하 여 실행*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a>작업 3-iPhone 시뮬레이터를 실행 하려면 Visual Studio 2012를 구성 합니다.

1. 열고 **Visual Studio 2012** 및 모든 웹 사이트를 열거나 새 프로젝트를 만듭니다.
2. 실행 단추에서 아래쪽 화살표를 클릭 하 고 선택 **브라우저 선택**합니다.

    ![브라우저 선택](whats-new-in-aspnet-mvc-4/_static/image58.png "브라우저 선택")

    *브라우저 선택*
3. 에 &quot;브라우저&quot; 대화 상자를 클릭 하 여 **추가**합니다.
4. 에 &quot;프로그램 추가&quot; 대화 상자에서 다음 값을 사용 합니다.

   - <strong>프로그램</strong>: C:\Users\*{CurrentUser}<em>\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe * (경로 적절 하 게 업데이트)</em>
   - **인수**: &quot;1&quot;
   - **식별 이름**: iPhone 시뮬레이터

     ![프로그램 추가](whats-new-in-aspnet-mvc-4/_static/image59.png "프로그램 추가")

     *로 검색 하도록 프로그램 추가*
5. 클릭 **확인** 대화 상자를 닫습니다.
6. 이제 Visual Studio 2012에서 iPhone 시뮬레이터에서 웹 응용 프로그램을 실행할 수 있습니다.

    ![브라우저 선택 iPhone 시뮬레이터](whats-new-in-aspnet-mvc-4/_static/image60.png "iPhone 시뮬레이터 브라우저 선택")

    *IPhone 시뮬레이터 브라우저 선택*

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>부록 d: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

이 부록에서는 Windows Azure 관리 포털에서 새 웹 사이트를 만들고 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하기 위해 랩에서 수행 하 여 가져온 응용 프로그램을 게시 하는 방법을 보여줍니다.

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>작업 1-Windows에서 새 웹 사이트를 만드는 Azure 포털

1. 이동 하 여 [Windows Azure 관리 포털](https://manage.windowsazure.com/) 구독에 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.

    > [!NOTE]
    > Windows Azure를 무료로 10 개 ASP.NET 웹 사이트를 호스트 하 고 트래픽이 증가 됨을 확장 한 다음 사용할 수 있습니다. 등록할 수 [여기](http://aka.ms/aspnet-hol-azure)합니다.

    ![Windows Azure 포털에 로그온](whats-new-in-aspnet-mvc-4/_static/image61.png "Windows Azure 포털에 로그인")

    *Windows Azure 관리 포털에 로그온*
2. 클릭 **새로** 명령 모음에서 합니다.

    ![새 웹 사이트를 만드는](whats-new-in-aspnet-mvc-4/_static/image62.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. 클릭 **계산** | **웹 사이트**합니다. 그런 다음 선택 **빠른 생성** 옵션입니다. 새 웹 사이트에 대 한 사용 가능한 URL을 입력 하 고 클릭 **웹 사이트 만들기**합니다.

    > [!NOTE]
    > Windows Azure 웹 사이트는 호스트를 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램입니다. 빨리 만들기 옵션을 사용 하면 완성 된 웹 응용 프로그램을 Windows Azure 웹 사이트에서 포털 외부에 배포할 수 있습니다. 데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](whats-new-in-aspnet-mvc-4/_static/image63.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.
5. 웹 사이트가 만들어지면 아래 링크를 클릭 하 고 **URL** 열입니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트를 찾아](whats-new-in-aspnet-mvc-4/_static/image64.png "새 웹 사이트를 검색 합니다.")

    *새 웹 사이트를 검색합니다.*

    ![실행 중인 웹 사이트](whats-new-in-aspnet-mvc-4/_static/image65.png "실행 중인 웹 사이트")

    *실행 중인 웹 사이트*
6. 포털로 돌아가서 아래에서 웹 사이트의 이름을 클릭는 **이름** 관리 페이지를 표시 하는 열입니다.

    ![웹 사이트 관리 페이지 열기](whats-new-in-aspnet-mvc-4/_static/image66.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. 에 **대시보드** 페이지의 **눈에 보는** 섹션에서 클릭는 **게시 프로필 다운로드** 링크 합니다.

    > [!NOTE]
    > *게시 프로필* 각각의 활성화 된 게시 방법에 대 한 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 데 필요한 정보가 모두 포함 되어 있습니다. 게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열이 포함 되어 있습니다. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 읽는 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 합니다.

    ![게시 프로필 다운로드 웹 사이트](whats-new-in-aspnet-mvc-4/_static/image67.png "게시 프로필 다운로드 웹 사이트")

    *게시 프로필 다운로드 웹 사이트*
8. 알려진된 위치에 게시 프로필 파일을 다운로드 합니다. 더 이상이 연습에서는 Visual Studio에서 웹 응용 프로그램 Windows Azure 웹 사이트를 게시 하려면이 파일을 사용 하는 방법을 표시 됩니다.

    ![게시 프로필 파일을 저장](whats-new-in-aspnet-mvc-4/_static/image68.png "게시 프로필 저장")

    *게시 프로필 파일을 저장합니다.*

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL Server를 활용 하는 경우 데이터베이스를 SQL 데이터베이스 서버 만들기 해야 합니다. SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 태스크를 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하기 위해 SQL 데이터베이스 서버를 해야 합니다. Windows Azure 관리 포털에서 구독의 SQL 데이터베이스 서버를 볼 수 있습니다 **Sql 데이터베이스** | **서버** | **서버 대시보드**합니다. 만든 서버 없는 경우 수행 하 여 만들 수 있습니다는 **추가** 명령 모음에서 단추입니다. 기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**, 다음 작업에 사용 됩니다. 만들지 마십시오 데이터베이스 아직 대로 이후 단계에서 생성 됩니다.

    ![SQL 데이터베이스 서버 대시보드](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL 데이터베이스 서버 대시보드")

    *SQL 데이터베이스 서버 대시보드*
2. 다음 태스크에서는 서버 목록에 사용자의 로컬 IP 주소를 포함 해야 이러한 이유로 Visual Studio에서 데이터베이스 연결을 테스트 **허용 IP 주소**합니다. 작업을 수행 하려면 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여넣습니다는 **시작 IP 주소** 및 **끝IP주소** 클릭 하 고 텍스트 상자는 ![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png) 단추입니다.

    ![클라이언트 IP 주소를 추가합니다.](whats-new-in-aspnet-mvc-4/_static/image71.png)

    *클라이언트 IP 주소를 추가합니다.*
3. 한 번는 **클라이언트 IP 주소** 허용된 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 하 여 변경 사항을 확인 합니다.

    ![변경 확인](whats-new-in-aspnet-mvc-4/_static/image72.png)

    *변경 확인*

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션으로 돌아갑니다. 에 **솔루션 탐색기**웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.

    ![응용 프로그램을 게시](whats-new-in-aspnet-mvc-4/_static/image73.png "응용 프로그램을 게시")

    *웹 사이트를 게시*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필 가져오기](whats-new-in-aspnet-mvc-4/_static/image74.png "게시 프로필 가져오기")

    *게시 프로필 가져오기*
3. 클릭 **연결 확인**합니다. 유효성 검사가 완료 되 면 클릭 **다음**합니다.

    > [!NOTE]
    > 연결 유효성 검사 단추 옆에 표시 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.

    ![연결 유효성 검사](whats-new-in-aspnet-mvc-4/_static/image75.png "연결 유효성 검사")

    *연결 유효성 검사*
4. 에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추 클릭 (즉, **DefaultConnection**).

    ![웹 배포 구성](whats-new-in-aspnet-mvc-4/_static/image76.png "웹 배포 구성")

    *웹 배포 구성*
5. 다음과 같이 데이터베이스 연결을 구성 합니다.

   - 에 **서버 이름** SQL 데이터베이스 서버 URL 사용 하 여 입력 된 *tcp:* 접두사입니다.
   - **사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 서버 관리자 로그인 암호를 입력 합니다.
   - 예를 들어 새 데이터베이스 이름 입력: *MVC4SampleDB*합니다.

     ![대상 연결 문자열 구성](whats-new-in-aspnet-mvc-4/_static/image77.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 다음 **확인**을 클릭합니다. 데이터베이스를 만들려는 대화 상자가 나타나면 **예**합니다.

    ![데이터베이스를 만드는](whats-new-in-aspnet-mvc-4/_static/image78.png "데이터베이스 문자열 만들기")

    *데이터베이스를 만드는 중*
7. Windows azure에서 SQL 데이터베이스에 연결 하기 위해 사용할 연결 문자열은 기본 연결 텍스트 상자 내에서 표시 됩니다. **다음**을 클릭합니다.

    ![SQL 데이터베이스를 가리키는 연결 문자열](whats-new-in-aspnet-mvc-4/_static/image79.png "SQL 데이터베이스를 가리키는 연결 문자열")

    *SQL 데이터베이스를 가리키는 연결 문자열*
8. 에 **미리 보기** 페이지 **게시**합니다.

    ![웹 응용 프로그램을 게시](whats-new-in-aspnet-mvc-4/_static/image80.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.

    ![Windows Azure에 게시 된 응용 프로그램](whats-new-in-aspnet-mvc-4/_static/image81.png "Windows Azure에 게시 된 응용 프로그램")

    *Windows Azure에 게시 된 응용 프로그램*
