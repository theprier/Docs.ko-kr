---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: '실습: 하나의 ASP.NET: ASP.NET Web Forms, MVC 및 Web API 통합 | Microsoft Docs'
author: rick-anderson
description: ASP.NET은 웹 사이트, 앱 및 MVC, Web API 등과 같은 특수 한 기술을 사용 하 여 서비스를 빌드하기 위한 프레임 워크입니다. 확장과 ASP.NET h...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: c18911680b59448cd67190f71e951a3fcf3d0478
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48912737"
---
<a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a>실습: 하나의 ASP.NET: ASP.NET Web Forms, MVC 및 Web API 통합
====================
[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트 다운로드](http://aka.ms/webcamps-training-kit)

> ASP.NET은 웹 사이트, 앱 및 MVC, Web API 등과 같은 특수 한 기술을 사용 하 여 서비스를 빌드하기 위한 프레임 워크입니다. 확장을 사용 하 여 ASP.NET에서 생성 된 후 표시를 표현 해야 이러한 기술을 통합 하 고 있었는지 최근 작업으로 작업 **One ASP.NET**합니다.
> 
> Visual Studio 2013 응용 프로그램을 빌드하고 프로젝트 중 하나에 모든 ASP.NET 기술을 사용 하 여 수 있는 새로운 통합형된 프로젝트 시스템인을 소개 합니다. 이 기능은, 스틱을 프로젝트의 시작 부분에 한 기술을 선택 하지 않아도 되며 대신 하나의 프로젝트 내에서 여러 ASP.NET 프레임 워크를 사용 하도록 할.
> 
> 웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)합니다.


<a id="Overview"></a>
## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 학습할 방법:

- 기반 웹 사이트 만들기는 **One ASP.NET** 프로젝트 형식
- 사용 하 여 다른 **ASP.NET** 같은 프레임 워크 **MVC** 하 고 **Web API** 동일한 프로젝트에서
- 주요 구성 요소를 식별 한 **ASP.NET** 응용 프로그램
- 활용 합니다 **ASP.NET 스 캐 폴딩** 모델 클래스를 기반으로 자동으로 만들고 컨트롤러 뷰 CRUD 작업을 수행 하기 위해 프레임 워크
- 동일한 집합의 각 작업에 대 한 적합 한 도구를 사용 하 여 컴퓨터 및 사람이 인식할 수 형식으로 정보를 노출 합니다.

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

다음는이 실습을 완료 해야 합니다.

- [Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상
- [Visual Studio 2013 업데이트 1](https://go.microsoft.com/fwlink/?LinkId=301714)

<a id="Setup"></a>
### <a name="setup"></a>설정

이 실습에서는 연습을 실행 하려면 먼저 환경 설정을 설정 해야 합니다.

1. Windows 탐색기를 열고 실습용 **원본** 폴더입니다.
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

1. [새 웹 폼 프로젝트 만들기](#Exercise1)
2. [스 캐 폴딩을 사용 하 여 MVC 컨트롤러 만들기](#Exercise2)
3. [스 캐 폴딩을 사용 하 여 웹 API 컨트롤러 만들기](#Exercise3)

이 랩을 완료 하기 위한 예상 시간: **60 분**

> [!NOTE]
> Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션에는 특정 개발 스타일에 맞게 설계 되었습니다 및 창 레이아웃, 동작 편집기, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 랩의 절차에서는 사용 하는 경우 Visual Studio에서 지정된 된 태스크를 수행 하는 데 필요한 작업을 설명 합니다 **일반 개발 설정** 컬렉션입니다. 개발 환경에 대 한 다양 한 설정 컬렉션을 선택 하는 경우를 고려해 야 하는 단계에 차이가 있을 수 있습니다.


<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a>연습 1: 새 웹 폼 프로젝트 만들기

이 연습에서 사용 하 여 Visual Studio 2013에서 새 Web Forms 사이트를 만듭니다는 **One ASP.NET** 통합 프로젝트 경험을 사용 하면 동일한 응용 프로그램에서 Web Forms, MVC 및 Web API 구성 요소를 쉽게 통합할 수 있습니다. 그런 다음 생성 된 솔루션을 탐색 하 고 해당 파트를 식별 합니다 및 웹 사이트의 작업을 마지막으로 표시 됩니다.

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a>작업 1 – 하나의 ASP.NET 환경을 사용 하 여 새 사이트 만들기

먼저이 작업에 따라 Visual Studio에서 새 웹 사이트 만들기는 **One ASP.NET** 형식 프로젝션 합니다. **One ASP.NET** 를 모든 ASP.NET 기술을 통합 하 고 혼합 하 고 필요에 따라 일치 하는 옵션이 있습니다. 응용 프로그램 내에서 나란히 상주 하는 Web Forms, MVC 및 Web API의 다른 구성 요소를 인식 다음 됩니다.

1. 오픈 **Visual Studio Express 2013 for Web** 선택한 **파일 | 새 프로젝트...**  새 솔루션을 시작 합니다.

    ![새 프로젝트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    *새 프로젝트 만들기*
2. 에 **새 프로젝트** 대화 상자에서 **ASP.NET 웹 응용 프로그램** 아래에서 **Visual C# | 웹** 탭을 했는지 **.NET Framework 4.5** 을 선택 합니다. 프로젝트 이름을 *MyHybridSite*, 선택 된 **위치** 클릭 **확인**.

    ![새 ASP.NET 웹 응용 프로그램 프로젝트](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    *새 ASP.NET 웹 응용 프로그램 프로젝트 만들기*
3. 에 **새 ASP.NET 프로젝트** 대화 상자에서를 **Web Forms** 템플릿을 선택한 합니다 **MVC** 및 **Web API** 옵션. 또한 있는지 확인 합니다 **인증** 옵션을 설정 **개별 사용자 계정**합니다. 계속하려면 **확인** 을 클릭합니다.

    ![Web API 및 MVC 구성 요소를 포함 하 여 Web Forms 템플릿을 사용 하 여 새 프로젝트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    *Web API 및 MVC 구성 요소를 포함 하 여 Web Forms 템플릿을 사용 하 여 새 프로젝트 만들기*
4. 이제 생성 된 솔루션의 구조를 탐색할 수 있습니다.

    ![생성 된 솔루션 탐색](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    *생성 된 솔루션 탐색*

    1. **계정:** 이 폴더에는 Web Form 페이지 등록, 로그인 및 응용 프로그램의 사용자 계정 관리를 포함 합니다. 이 폴더를 추가 하는 경우는 **개별 사용자 계정** Web Forms 프로젝트 템플릿 구성 하는 동안 인증 옵션을 선택 합니다.
    2. **모델:** 이 폴더에는 응용 프로그램 데이터를 나타내는 클래스가 포함 됩니다.
    3. **컨트롤러** 하 고 **뷰**: 이러한 폴더는 필요 합니다 **ASP.NET MVC** 및 **ASP.NET Web API** 구성 요소. 다음 연습에서는 MVC 및 Web API 기술을 살펴봅니다.
    4. **Default.aspx**, **Contact.aspx** 하 고 **About.aspx** 파일이 빌드 관련 페이지를 시작 점으로 사용할 수 있는 미리 정의 된 Web Form 페이지에 응용 프로그램입니다. 이라고 하는 별도 파일에 있는 해당 파일의 프로그래밍 논리는 &quot;코드 숨김&quot; 포함 된 파일을 &quot;합니다.에서는&quot; 또는 &quot;. aspx.cs&quot; 확장 (에 따라는 언어 사용)입니다. 코드 숨김 논리 서버에서 실행 하 고 동적으로 페이지에 대 한 HTML 출력을 생성 합니다.
    5. 합니다 **Site.Master** 하 고 **Site.Mobile.Master** 페이지 응용 프로그램의 모양과 느낌 및 모든 페이지의 표준 동작을 정의 합니다.
5. 두 번 클릭 합니다 **Default.aspx** 페이지의 내용을 탐색 하는 파일입니다.

    ![Default.aspx 페이지를 탐색합니다.](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    *Default.aspx 페이지를 탐색합니다.*

    > [!NOTE]
    > 합니다 **페이지** 지시문 파일의 맨 위에 있는 Web Forms 페이지의 특성을 정의 합니다. 예를 들어, 합니다 **MasterPageFile** 마스터에 대 한 경로 지정 하는 특성 페이지-이 경우에 *Site.Master* 페이지 및 **Inherits** 특성 정의 상속 하도록 페이지에 대 한 코드 숨김 클래스입니다. 이 클래스에 의해 결정 되는 파일에는 **코드 숨김** 특성입니다.
    > 
    > 합니다 **asp: Content** 컨트롤 (텍스트, 태그 및 컨트롤) 페이지의 실제 콘텐츠를 보유 하 고에 매핑되는 **asp: ContentPlaceHolder** 마스터 페이지의 컨트롤입니다. 내에서 페이지 콘텐츠를 렌더링 하는 경우에 *MainContent* 에 정의 된 컨트롤을 *Site.Master* 페이지.
6. 확장을 **앱\_시작** 폴더 및 통지를 **WebApiConfig.cs** 파일입니다. Visual Studio One ASP.NET 템플릿을 사용 하 여 프로젝트를 구성 하는 경우 웹 API를 포함 하기 때문에 생성 된 솔루션에 해당 파일을 포함 합니다.
7. 엽니다는 **WebApiConfig.cs** 파일입니다. 에 *WebApiConfig* 있습니다. HTTP를 매핑하는 Web API 사용 하 여 관련 된 구성 클래스 라우팅합니다 **Web API 컨트롤러**합니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. 엽니다는 **RouteConfig.cs** 파일입니다. 내 합니다 *RegisterRoutes* 메서드를 HTTP 경로 매핑하는 MVC와 연관 된 구성을 찾을 수 있습니다 **MVC 컨트롤러**합니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a>작업 2-솔루션 실행

이 작업에서 생성 된 솔루션을 실행를 하는 앱과 같은 URL 재작성 및 기본 제공 인증 기능을 일부를 탐색 합니다.

1. 키를 눌러 솔루션을 실행 하려면 **F5** 누르거나를 **시작** 도구 모음에 있는 단추입니다. 브라우저에서 응용 프로그램 홈 페이지를 열어야 합니다.

    ![솔루션 실행](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. Web Forms 페이지 호출 되는 것을 확인 합니다. 이 작업을 수행 하려면 추가 **/contact.aspx** 누릅니다 주소 표시줄에서 URL로 **Enter**합니다.

    ![친화적 Url](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    *친화적 Url*

    > [!NOTE]
    > URL로 변경 알 수 있듯이 **에문의/** 합니다. 시작 **ASP.NET 4**URL 라우팅 기능이 Web Forms에 추가 된, Url 등 작성할 수 있습니다 *[ http://www.mysite.com/products/software ](http://www.mysite.com/products/software)* 대신  *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)*. 자세한 내용은를 참조 [URL 라우팅](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md)합니다.
3. 이제 응용 프로그램에 통합 된 인증 흐름을 살펴봅니다. 이 작업을 수행 하려면 **등록** 페이지의 오른쪽 위 모퉁이에서.

    ![새 사용자 등록](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    *새 사용자 등록*
4. 에 **등록** 페이지에서 입력을 **사용자 이름** 및 **암호**를 클릭 하 고 **등록**합니다.

    ![등록 페이지](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    *등록 페이지*
5. 응용 프로그램에서 새 계정을 등록 하 고 사용자가 인증 키를 누릅니다.

    ![인증 된 사용자](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    *인증 된 사용자*
6. Visual Studio 및 키를 눌러도 돌아가 **shift+f5** 디버깅을 중지 합니다.

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a>연습 2: 스 캐 폴딩을 사용 하 여 MVC 컨트롤러 만들기

이 연습에서 작업 및 코드 한 줄도 작성 하지 않고 CRUD 작업을 수행 하는 Razor 뷰를 사용 하 여 ASP.NET MVC 5 컨트롤러를 만들려면 Visual Studio에서 제공 하는 ASP.NET 스 캐 폴딩 프레임 워크를 활용을 걸립니다. SQL database에서 데이터 컨텍스트 및 데이터베이스 스키마를 생성 하는 스 캐 폴딩 프로세스 Entity Framework Code First 사용 합니다.

**Entity framework Code First**

EF (entity Framework)는 관계형 저장소 스키마를 사용 하 여 직접 프로그래밍 하는 대신 개념적 응용 프로그램 모델을 사용 하 여 프로그래밍 하 여 데이터 액세스 응용 프로그램을 만들 수 있게 하는 개체 관계형 매퍼 (ORM).

Entity Framework Code First 모델링 워크플로가 있습니다 나타내기 위해 사용할 고유한 도메인 클래스는 쿼리를 수행 하는 경우 EF가 의존 하는 모델 변경 내용 추적 및 업데이트 함수. Code First 개발 워크플로 사용 하면 필요가 없습니다 데이터베이스를 만들거나 스키마를 지정 하 여 응용 프로그램을 시작 합니다. 대신, 응용 프로그램에 가장 적합 한 도메인 모델 개체를 정의 하는 표준.NET 클래스를 작성할 수 있습니다 하 고 Entity Framework에서 데이터베이스를 만듭니다.

> [!NOTE]
> Entity Framework에 대 한 자세히 알아볼 수 있습니다 [여기](../../../entity-framework.md)합니다.


<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a>작업 1-새 모델 만들기

이제 정의 **Person** 모델 스 캐 폴딩 프로세스에서 MVC 컨트롤러 및 뷰를 만드는 데 될 클래스입니다. 만들어 시작 합니다는 **Person** 모델 클래스와 컨트롤러의 CRUD 작업은 자동으로 만들어집니다 스 캐 폴딩 기능을 사용 합니다.

1. 열기 **Visual Studio Express 2013 for Web** 하며 **MyHybridSite.sln** 솔루션에는 **소스/e x 2-MvcScaffolding/시작** 폴더입니다. 또는 계속할 수 있습니다 솔루션을 사용 하 여 이전 연습에서 얻은.
2. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더를 **MyHybridSite** 프로젝트를 마우스 **추가 | 클래스...** .

    ![사용자 모델 클래스 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    *사용자 모델 클래스 추가*
3. 에 **새 항목 추가** 대화 상자에서 파일 이름 *Person.cs* 클릭 **추가**합니다.

    ![사용자 모델 클래스 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    *사용자 모델 클래스 만들기*
4. 콘텐츠를 대체 합니다 **Person.cs** 를 다음 코드로 파일. 키를 눌러 **CTRL + S** 변경 내용을 저장 합니다.

    (코드 조각- *BringingTogetherOneAspNet-e x 2-PersonClass*)

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **MyHybridSite** 프로젝트를 마우스 **빌드**를 누르거나 **CTRL + SHIFT + B** 프로젝트를 빌드합니다.

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a>작업 2-MVC 컨트롤러 만들기

이제는 **Person** 모델을 만들, Entity Framework를 사용 하 여 ASP.NET MVC 스 캐 폴딩의 CRUD 컨트롤러 작업 및 보기를 만드는 데 사용할 **Person**.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 폴더를 **MyHybridSite** 프로젝트를 마우스 **추가 | 스 캐 폴드 된 새 항목...** .

    ![새 스 캐 폴드 된 컨트롤러 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    *새 스 캐 폴드 된 컨트롤러 만들기*
2. 에 **스 캐 폴드 추가** 대화 상자에서 **Entity Framework를 사용 하 여 뷰를 사용 하 여 MVC 5 컨트롤러** 클릭 하 고 **추가 합니다.**

    ![뷰 및 Entity Framework를 사용 하 여 선택한 MVC 5 컨트롤러](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    *뷰 및 Entity Framework를 사용 하 여 선택한 MVC 5 컨트롤러*
3. 설정 *MvcPersonController* 으로 **컨트롤러 이름**를 선택 합니다 **비동기 컨트롤러 동작을 사용 하 여** 옵션을 선택 **사람 (MyHybridSite.Models)**  으로 **모델 클래스**합니다.

    ![스 캐 폴딩 사용 하 여 MVC 컨트롤러 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    *스 캐 폴딩 사용 하 여 MVC 컨트롤러 추가*
4. 아래 **데이터 컨텍스트 클래스**, 클릭 **새 데이터 컨텍스트...** .

    ![새 데이터 컨텍스트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    *새 데이터 컨텍스트 만들기*
5. 에 **새 데이터 컨텍스트에** 대화 상자에서 이름 새 데이터 컨텍스트에 *PersonContext* 클릭 **추가**합니다.

    ![새 PersonContext 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    *새 PersonContext 형식 만들기*
6. 클릭 **추가** 에 대 한 새 컨트롤러에 만들려는 **Person** 스 캐 폴딩을 사용 하 여 합니다. Visual Studio에서 컨트롤러 작업, 사용자 데이터 컨텍스트 및 Razor 뷰 생성 합니다.

    ![MVC 컨트롤러 스 캐 폴딩을 사용 하 여 만든 후](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    *MVC 컨트롤러 스 캐 폴딩을 사용 하 여 만든 후*
7. 엽니다는 **MvcPersonController.cs** 파일을 **컨트롤러** 폴더. CRUD 작업 메서드에 자동으로 생성 되었는지 확인 합니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > 선택 하 여 합니다 **비동기 컨트롤러 동작을 사용 하 여** 이전 단계에서 스 캐 폴딩에서 확인란 옵션, Visual Studio 사용자 데이터 컨텍스트에 대 한 액세스와 관련 된 모든 작업에 대 한 비동기 동작 메서드를 생성 합니다. CPU 바인딩되지 않은 요청을 처리 하는 동안 작업을 수행할 수 없도록 웹 서버를 차단 하지 않도록 요청을 비동기 작업 메서드를 사용 하 여 장기 실행에 대 한 것이 좋습니다.

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a>작업 3 – 솔루션 실행

이 태스크에서는 실행 되었는지 확인 하려면 다시 솔루션에 대 한 보기 **Person** 예상 대로 작동 합니다. 데이터베이스에 성공적으로 저장 되는 확인 하려면 새 사용자를 추가 합니다.

1. 키를 눌러 **F5** 솔루션을 실행 합니다.
2. 이동할 **/MvcPerson**합니다. 사용자의 목록을 보여 주는 스 캐 폴드 된 뷰에 나타납니다.
3. 클릭 **새로 만들기** 새 사용자를 추가 합니다.

    ![스 캐 폴드 된 MVC 뷰로 이동](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    *스 캐 폴드 된 MVC 뷰로 이동*
4. 에 **만들기** 보기에서 제공를 **이름** 및 **Age** 사람과 클릭에 대 한 **만들기**합니다.

    ![새 사람 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    *새 사람 추가*
5. 새 사람 목록에 추가 됩니다. 요소 목록에서 클릭 **세부 정보** 사람의 세부 정보 보기를 표시 합니다. 그런 다음 합니다 **세부 정보** 보기를 클릭 **목록으로 돌아가기** 목록 보기로 다시 이동 합니다.

    ![사용자의 세부 정보 보기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    *사용자의 세부 정보 보기*
6. 클릭 합니다 **삭제** 사용자를 삭제 하는 링크입니다. 에 **삭제** 보기에서 클릭 **삭제** 작업을 확인 하 합니다.

    ![사용자 삭제](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    *사용자 삭제*
7. Visual Studio 및 키를 눌러도 돌아가 **shift+f5** 디버깅을 중지 합니다.

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a>연습 3: Web API 컨트롤러 스 캐 폴딩을 사용 하 여 만들기

Web API 프레임 워크 ASP.NET 스택에의 일부 이며 쉽게 구현 하는 HTTP 서비스, 일반적으로 보내고 RESTful API를 통해 JSON 또는 XML 형식의 데이터를 받는 데 사용 됩니다.

이 연습에서는 Web API 컨트롤러를 생성 하려면 ASP.NET 스 캐 폴딩을 다시 사용 합니다. 사용 하 여 동일한 **Person** 하 고 **PersonContext** JSON 형식에서 같은 사용자 데이터를 제공 하 여 이전 연습에서 클래스입니다. 동일한 리소스를 동일한 ASP.NET 응용 프로그램 내에서 다른 방법으로 노출할 수 있습니다 하는 방법을 볼 수 있습니다.

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a>작업 1-웹 API 컨트롤러 만들기

이 작업을 만든 새 **Web API 컨트롤러** JSON과 같은 컴퓨터에서 사용할 수 있는 형식으로 사용자 데이터를 노출 하는 됩니다.

1. 열려 있지 않으면 엽니다 **Visual Studio Express 2013 for Web** 연 합니다 **MyHybridSite.sln** 솔루션을 **소스/Ex3-WebAPI/시작** 폴더입니다. 또는 계속할 수 있습니다 솔루션을 사용 하 여 이전 연습에서 얻은.

    > [!NOTE]
    > 연습 3에서 시작 솔루션을 사용 하 여 시작 하는 경우 키를 눌러 **CTRL + SHIFT + B** 솔루션을 빌드합니다.
2. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 폴더를 **MyHybridSite** 프로젝트를 마우스 **추가 | 스 캐 폴드 된 새 항목...** .

    ![새 스 캐 폴드 된 컨트롤러 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    *새 스 캐 폴드 된 컨트롤러 만들기*
3. 에 **스 캐 폴드 추가** 대화 상자에서 **Web API** 한 다음 왼쪽된 창에서 **Entity Framework를 사용 하 여 작업을 사용 하 여 Web API 2 컨트롤러** 가운데 창에서 를클릭하고 **추가 합니다.**

    ![작업 및 Entity Framework를 사용 하 여 Web API 2 컨트롤러를 선택 하면](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "작업 및 Entity Framework를 사용 하 여 Web API 2 컨트롤러 선택")

    *작업 및 Entity Framework를 사용 하 여 Web API 2 컨트롤러 선택*
4. 설정 *ApiPersonController* 으로 **컨트롤러 이름**를 선택 합니다 **비동기 컨트롤러 동작을 사용 하 여** 옵션을 선택 **사람 (MyHybridSite.Models)**  하 고 **PersonContext (MyHybridSite.Models)** 으로 **모델** 및 **데이터 컨텍스트** 각각 클래스입니다. **추가**를 클릭합니다.

    ![스 캐 폴딩 사용 하 여 웹 API 컨트롤러 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "스 캐 폴딩 사용 하 여 Web API 컨트롤러 추가")

    *스 캐 폴딩 사용 하 여 Web API 컨트롤러 추가*
5. Visual Studio에서 생성 한 다음 합니다 **ApiPersonController** 데이터와 함께 작동 하도록 4 개의 CRUD 동작이 포함 된 클래스입니다.

    ![Web API 컨트롤러 스 캐 폴딩을 사용 하 여 만들었으면](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "Web API 컨트롤러 스 캐 폴딩을 사용 하 여 만든 후")

    *Web API 컨트롤러 스 캐 폴딩을 사용 하 여 만든 후*
6. 열기는 **ApiPersonController.cs** 파일을 검사 합니다 *GetPeople* 작업 메서드. 이 메서드는 db 필드 쿼리 **PersonContext** 사용자 데이터를 가져오기 위해 형식입니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. 이제 메서드 정의 위의 설명을 확인할 수 있습니다. 다음 태스크에서 사용 하는이 작업을 노출 하는 URI를 제공 합니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > 기본적으로 웹 API가 catch에 대 한 쿼리로 구성 된 */a p i* MVC 컨트롤러를 사용 하 여 충돌을 방지 하는 방법입니다. 이 설정을 변경 해야 할 경우 가리킵니다 [ASP.NET Web API에서 라우팅](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)합니다.

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a>작업 2-솔루션 실행

이 작업에서는 사용 하 여 Internet Explorer **F12 개발자 도구** Web API 컨트롤러에서 전체 응답을 검사 합니다. 응용 프로그램 데이터에 대 한 자세한 정보를 가져오려는 네트워크 트래픽을 캡처할 수 있습니다 하는 방법을 볼 수 있습니다.

> [!NOTE]
> 했는지 **Internet Explorer** 가 선택 합니다 **시작** Visual Studio 도구 모음에 있는 단추입니다.
> 
> ![Internet Explorer 옵션](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> 합니다 **F12 개발자 도구** 와이드이 실습 랩에 적용 되지 않는 기능 집합이 있습니다. 자세한 내용을 원한다 면 가리킵니다 [F12 개발자 도구를 사용 하 여](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85))입니다.


1. 키를 눌러 **F5** 솔루션을 실행 합니다.

    > [!NOTE]
    > 이 작업을 올바르게 수행 하려면 응용 프로그램에 데이터가 포함 해야 합니다. 데이터베이스가 비어 있는 경우 연습 2에서 작업 3으로 돌아가서 하 수 MVC 뷰를 사용 하 여 새 사용자를 만드는 방법의 단계를 수행 합니다.
2. 키를 눌러 브라우저에서 **F12** 열려는 합니다 **개발자 도구** 패널입니다. 키를 눌러 **CTRL** + **4** 누르거나를 **네트워크** 아이콘을 한 다음 단추를 클릭 하 고 녹색 화살표 네트워크 트래픽 캡처를 시작 합니다.

    ![Web API 네트워크 캡처를 시작](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Web API 시작 네트워크 캡처")

    *Web API 네트워크 캡처를 시작합니다.*
3. 추가 **api/ApiPerson** 브라우저의 주소 표시줄에서 URL로 합니다. 이제 응답의 세부 정보를 검사 하는 합니다 **ApiPersonController**합니다.

    ![웹 API를 통해 사용자 데이터를 검색할](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "웹 API를 통해 사용자 데이터를 검색 합니다.")

    *웹 API를 통해 사용자 데이터를 검색합니다.*

    > [!NOTE]
    > 다운로드가 완료 되 면 다운로드 한 파일을 사용 하 여 작업을 할 수 있도록 묻는 메시지가 나타납니다. 대화 상자는 개발자 도구 창을 통해 응답 콘텐츠를 볼 수 있도록 열어 둡니다.
4. 이제는 응답의 본문을 조사 합니다. 이렇게 하려면 클릭 합니다 **세부 정보** 탭을 클릭 한 다음 **응답 본문**합니다. 다운로드 한 데이터는 속성을 사용 하 여 개체의 목록을 확인할 수 있습니다 **Id**, **이름** 및 **Age** 에 해당 하는 **사용자** 클래스입니다.

    ![보기 웹 API 응답 본문이](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "보기 웹 API 응답 본문")

    *웹 API 응답 본문 보기*

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a>작업 3 – Web API 도움말 페이지 추가

Web API를 만들 때 다른 개발자가 API를 호출 하는 방법을 알 수 있도록 도움말 페이지를 만드는 것이 유용할 것입니다. 만들고 설명서 페이지를 수동으로 업데이트할 수 있지만 유지 관리 작업을 수행할 것을 방지 하도록 자동으로 생성 하는 것이 좋습니다. 이 작업에서는 솔루션에 Web API 도움말 페이지를 자동으로 생성 하는 Nuget 패키지를 사용 합니다.

1. **도구** Visual Studio에서 메뉴 **NuGet 패키지 관리자**를 클릭 하 고 **패키지 관리자 콘솔**합니다.
2. 에 **패키지 관리자 콘솔** 창에서 다음 명령을 실행 합니다.

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > **Microsoft.AspNet.WebApi.HelpPage** 패키지는 필요한 어셈블리를 설치 하 고 아래에 있는 도움말 페이지에 대 한 MVC 뷰를 추가 합니다 **영역/HelpPage** 폴더입니다.

    ![HelpPage 영역](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage 영역")

    *HelpPage 영역*
3. 기본적으로 도움말 페이지에 설명서에 대 한 자리 표시자 문자열을 포함 합니다. 문서를 만들려면 XML 문서 주석을 사용할 수 있습니다. 이 기능을 사용 하려면 엽니다는 **HelpPageConfig.cs** 에 있는 파일을 **영역/HelpPage/앱\_시작** 폴더 다음 줄을 주석 처리 제거:

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 **MyHybridSite**를 선택 **속성** 을 클릭 합니다 **빌드** 탭.

    ![빌드 탭](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "빌드 섹션")

    *빌드 탭*
5. 아래 **출력**를 선택 **XML 문서 파일**합니다. 편집 상자에 입력 **앱\_Data/XmlDocument.xml**합니다.

    ![출력 섹션의 빌드 탭](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "출력 섹션의 빌드 탭")

    *빌드 탭에서 출력 섹션*
6. 키를 눌러 **CTRL** + **S** 변경 내용을 저장 합니다.
7. 엽니다는 **ApiPersonController.cs** 에서 파일을 **컨트롤러** 폴더입니다.
8. 간의 새 줄을 입력 합니다 *GetPeople* 메서드 시그니처 및 */ / api/ApiPerson GET* 주석 처리 한 다음 3 개의 슬래시를 입력 합니다.

    > [!NOTE]
    > Visual Studio는 자동으로 메서드 설명서를 정의 하는 XML 요소를 삽입 합니다.
9. 요약 텍스트 및 반환 값을 추가 합니다 *GetPeople* 메서드. 다음과 같이 표시 됩니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. 키를 눌러 **F5** 솔루션을 실행 합니다.
11. 추가 **/help** 도움말 페이지로 이동할 주소 표시줄에서 URL로 합니다.

    ![ASP.NET Web API 도움말 페이지](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API 도움말 페이지")

    *ASP.NET Web API 도움말 페이지*

    > [!NOTE]
    > 페이지의 주요 내용에는 api, 컨트롤러 별로 그룹화 된 테이블입니다. 사용 하 여 테이블 항목을 동적으로 생성 합니다 **IApiExplorer** 인터페이스입니다. 를 추가 하거나 API 컨트롤러를 업데이트 하는 경우 테이블 자동으로 업데이트 됩니다 다음에 응용 프로그램을 빌드합니다.
    > 
    > 합니다 **API** 열에는 HTTP 메서드 및 상대 URI를 나열 합니다. 합니다 **설명을** 열 메서드의 설명서에서 추출 된 정보를 포함 합니다.
12. 메서드 정의 위에 추가 설명을 참고 설명 열에 표시 됩니다.

    ![API 메서드 설명을](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API 메서드 설명")

    *API 메서드 설명*
13. 샘플 응답 본문을 포함 하 여 자세한 정보를 사용 하 여 페이지로 이동 하는 API 방법 중 하나를 클릭 합니다.

    ![세부 정보 페이지](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "세부 정보 페이지")

    *세부 정보 페이지*

* * *

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습을 완료 하 여 배웠습니다 방법:

- 하나는 ASP.NET 환경을 사용 하 여 Visual Studio 2013에서 새 웹 응용 프로그램 만들기
- 하나의 단일 프로젝트에 여러 ASP.NET 기술을 통합합니다
- ASP.NET 스 캐 폴딩을 사용 하 여 모델 클래스에서 MVC 컨트롤러 및 뷰를 생성 합니다.
- 비동기 프로그래밍 및 Entity Framework를 통해 데이터 액세스와 같은 기능을 사용 하는 Web API 컨트롤러를 생성 합니다.
- 컨트롤러에 대 한 Web API 도움말 페이지를 자동으로 생성
