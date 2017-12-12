---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: "실습 랩: One ASP.NET: ASP.NET Web Forms, MVC 및 Web API 통합 | Microsoft Docs"
author: rick-anderson
description: "ASP.NET은 웹 사이트, 응용 프로그램 및 MVC, Web API 등과 같은 특수 한 기술을 사용 하 여 서비스를 빌드하기 위한 프레임 워크입니다. 와 ASP.NET h 확장 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/16/2014
ms.topic: article
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 55109723e566a9f7c66c1a59414377b05dbec760
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a>실습 랩: One ASP.NET: ASP.NET Web Forms, MVC 및 Web API 통합 합니다.
====================
으로 [웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트를 다운로드 합니다.](http://aka.ms/webcamps-training-kit)

> ASP.NET은 웹 사이트, 응용 프로그램 및 MVC, Web API 등과 같은 특수 한 기술을 사용 하 여 서비스를 빌드하기 위한 프레임 워크입니다. 확장과 함께 ASP.NET에서 만들어진 이후 표시 및 표시 된 해야 이러한 기술을 통합, 방향으로 작업에 최근 활동 내용이 **One ASP.NET**합니다.
> 
> Visual Studio 2013 응용 프로그램을 구축 하 한 프로젝트에서 모든 ASP.NET 기술이 사용할 수 있는 새 통합된 프로젝트 시스템을 소개 합니다. 이 기능은, 스틱 및 프로젝트의 시작 부분에 한 가지 기술 선택 하지 않아도 되며 대신 하나의 프로젝트 내에서 여러 ASP.NET 프레임 워크를 사용 하도록 할.
> 
> 모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit)합니다.


<a id="Overview"></a>
## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 배웁니다 하는 방법:

- 에 따라 웹 사이트 만들기는 **One ASP.NET** 프로젝트 형식
- 사용 하 여 다른 **ASP.NET** 같은 프레임 워크 **MVC** 및 **웹 API** 같은 프로젝트에
- 주요 구성 요소를 식별 한 **ASP.NET** 응용 프로그램
- 활용 하기 위해는 **ASP.NET 스 캐 폴딩** 모델 클래스를 기반으로 자동으로 CRUD 작업을 수행 하는 컨트롤러와 뷰를 만들기 위해 프레임 워크
- 동일한 집합이 각 작업에 대 한 적절 한 도구를 사용 하 여 컴퓨터 및 사람이-읽을 수 있는 형식으로 정보를 노출 합니다.

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>필수 구성 요소

다음은이 실습 랩을 완료 하려면 필요 합니다.

- [Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상
- [Visual Studio 2013 업데이트 1](https://go.microsoft.com/fwlink/?LinkId=301714)

<a id="Setup"></a>
### <a name="setup"></a>설정

이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.

1. Windows 탐색기를 열고에 랩 찾아보기 **소스** 폴더입니다.
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

1. [새 Web Forms 프로젝트 만들기](#Exercise1)
2. [스 캐 폴딩을 사용 하 여 MVC 컨트롤러 만들기](#Exercise2)
3. [스 캐 폴딩을 사용 하 여 웹 API 컨트롤러 만들기](#Exercise3)

예상 소요 시간: **60 분**

> [!NOTE]
> Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션 특정 개발 스타일에 맞게 설계 하 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 랩의 절차를 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업 설명에서 **일반 개발 설정** 컬렉션입니다. 개발 환경에 대 한 서로 다른 설정 컬렉션을 선택 하면 고려해 야 하는 단계에 차이가 있을 수 있습니다.


<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a>연습 1: 새 Web Forms 프로젝트 만들기

이 연습에서는 다음을 사용 하 여 Visual Studio 2013에서 새 Web Forms 사이트 만들어집니다는 **One ASP.NET** 동일한 응용 프로그램에서 Web Forms, MVC 및 Web API 구성 요소를 쉽게 통합할 수 있는 프로젝트 경험을 통합 합니다. 그런 다음 생성 된 솔루션을 탐색 하 고 해당 부분을 식별 합니다 및 웹 사이트의 작업을 마지막으로 표시 됩니다.

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a>작업 1 – 하나의 ASP.NET 환경을 사용 하 여 새 사이트 만들기

먼저이 작업에서에 따라 Visual Studio에서 새 웹 사이트 만들기는 **One ASP.NET** 프로젝트 유형입니다. **One ASP.NET** 모든 ASP.NET 기술을 통합 하 고는 혼합 하 고 원하는 대로 얻었으면이 옵션을 제공 합니다. 응용 프로그램 내에서 함께 존재 하는 Web Forms, MVC 및 Web API의 다른 구성 요소를 인식 다음 됩니다.

1. 열기 **Visual Studio Express 2013 for Web** 선택 **파일 | 새 프로젝트...**  새 솔루션을 시작 합니다.

    ![새 프로젝트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    *새 프로젝트 만들기*
2. 에 **새 프로젝트** 대화 상자에서 **ASP.NET 웹 응용 프로그램** 아래는 **Visual C# | 웹** 탭 하 고 있는지 확인 **.NET Framework 4.5** 을 선택 합니다. 프로젝트 이름을 *MyHybridSite*, 선택는 **위치** 클릭 **확인**합니다.

    ![새 ASP.NET 웹 응용 프로그램 프로젝트](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    *새 ASP.NET 웹 응용 프로그램 프로젝트 만들기*
3. 에 **새 ASP.NET 프로젝트** 대화 상자는 **Web Forms** 서식 파일을 선택은 **MVC** 및 **웹 API** 옵션입니다. 또한 있는지 확인 하 고 **인증** 옵션을 설정 **개별 사용자 계정**합니다. 계속하려면 **확인** 을 클릭합니다.

    ![웹 API 및 MVC 구성 요소를 포함 하 여 Web Forms 템플릿을 사용 하 여 새 프로젝트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    *웹 API 및 MVC 구성 요소를 포함 하 여 Web Forms 템플릿을 사용 하 여 새 프로젝트 만들기*
4. 이제 생성 된 솔루션의 구조를 탐색할 수 있습니다.

    ![생성 된 솔루션을 탐색합니다.](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    *생성 된 솔루션을 탐색합니다.*

    1. **계정:** 이 폴더에는 Web Form 페이지 등록, 로그인 및 응용 프로그램의 사용자 계정 관리를 포함 합니다. 이 폴더를 추가 하는 경우는 **개별 사용자 계정** Web Forms 프로젝트 템플릿 구성 하는 동안 인증 옵션을 선택 합니다.
    2. **모델:** 이 폴더에는 응용 프로그램 데이터를 나타내는 클래스가 포함 됩니다.
    3. **컨트롤러** 및 **뷰**: 하는 데 필요한 이러한 폴더는 **ASP.NET MVC** 및 **ASP.NET Web API** 구성 요소입니다. 다음 연습에 포함 된 MVC 및 Web API 기술을 살펴봅니다.
    4. **Default.aspx**, **Contact.aspx** 및 **About.aspx** 파일은 미리 정의 된 Web Form 페이지에만 페이지를 구성할 때 기준으로 사용할 수 있는 사용자 응용 프로그램입니다. 으로 참조 하는 별도 파일에 있는 해당 파일의 프로그래밍 논리는 &quot;코드 숨김&quot; 파일은 &quot;. aspx.vb&quot; 또는 &quot;. aspx.cs&quot; 확장 (에 따라는 언어 사용)입니다. 코드 숨김 논리 서버에서 실행 하 고 동적으로 페이지의 HTML 출력을 생성 합니다.
    5. **Site.Master** 및 **Site.Mobile.Master** 페이지 응용 프로그램의 모양과 느낌와 모든 페이지의 표준 동작을 정의 합니다.
5. 두 번 클릭 하 여 **Default.aspx** 페이지의 내용을 탐색 하는 파일입니다.

    ![Default.aspx 페이지를 탐색합니다.](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    *Default.aspx 페이지를 탐색합니다.*

    > [!NOTE]
    > **페이지** 지시문 파일 맨 위에 있는 Web Forms 페이지의 특성을 정의 합니다. 예를 들어는 **MasterPageFile** 마스터에 대 한 경로 지정 하는 특성-이 경우 페이지는 *Site.Master* 페이지-및 **Inherits** 특성 정의 상속 하도록 페이지에 대 한 코드 숨김 클래스입니다. 이 클래스에 의해 결정 되는 파일에는 **코드 숨김** 특성입니다.
    > 
    > **asp: Content** 컨트롤 (텍스트, 태그 및 컨트롤) 페이지의 실제 콘텐츠를 보유 하 고에 매핑된는 **asp: ContentPlaceHolder** 마스터 페이지에 컨트롤입니다. 내부 페이지 콘텐츠를 렌더링할 경우에 *MainContent* 에 정의 된 컨트롤의 *Site.Master* 페이지.
6. 확장의 **앱\_시작** 폴더와 통지는 **WebApiConfig.cs** 파일입니다. Visual Studio One ASP.NET 템플릿을 사용 하 여 프로젝트를 구성할 때 웹 API를 포함 하기 때문에 생성 된 솔루션에서 해당 파일을 포함 했습니다.
7. 열기는 **WebApiConfig.cs** 파일입니다. 에 *경우 WebApiConfig* HTTP 매핑하는 Web API와 관련 된 구성이 있습니다 클래스에 라우팅하여 **Web API 컨트롤러**합니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. 열기는 **RouteConfig.cs** 파일입니다. 내에서 *RegisterRoutes* HTTP 경로를 매핑하는 MVC와 연관 된 구성이 있습니다 메서드 **MVC 컨트롤러**합니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a>작업 2-솔루션 실행

이 작업에서 생성 된 솔루션 실행 되 면 응용 프로그램 및 해당 기능을 URL 다시 작성 및 기본 제공 인증 같은 중 일부를 탐색 합니다.

1. 눌러 솔루션을 실행 **F5** 하거나 클릭 하 고 **시작** 단추는 도구 모음에 있는 합니다. 응용 프로그램 홈 페이지는 브라우저에서 열립니다.

    ![솔루션을 실행](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. Web Forms 페이지를 호출 하 고 확인 하십시오. 이 작업을 수행 하려면 추가 **/contact.aspx** 누릅니다 주소 표시줄에서 URL로 **Enter**합니다.

    ![친화적 Url](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    *친화적 Url*

    > [!NOTE]
    > URL로 변경 볼 수 있듯이 **문의/**합니다. 시작 **ASP.NET 4**, URL 라우팅 기능 Web Forms에 추가 된, Url 등 작성할 수 있습니다  *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)*  대신 *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)*합니다. 자세한 내용은를 참조 [URL 라우팅](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md)합니다.
3. 이제 응용 프로그램에 통합 된 인증 흐름을 탐색 합니다. 이 작업을 수행 하려면 **등록** 페이지의 오른쪽 위 모퉁이에 있습니다.

    ![새 사용자를 등록 하는 중](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    *새 사용자를 등록 하는 중*
4. 에 **등록** 페이지에서 입력 한 **사용자 이름** 및 **암호**, 클릭 하 고 **등록**합니다.

    ![등록 페이지](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    *등록 페이지*
5. 사용자가 인증 및 응용 프로그램에서 새 계정을 등록 합니다.

    ![인증 된 사용자](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    *인증 된 사용자*
6. Visual Studio 및 키를 눌러로 돌아가서 **SHIFT + f 5를 눌러** 디버깅을 중지 합니다.

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a>연습 2: 스 캐 폴딩을 사용 하 여 MVC 컨트롤러 만들기

이 연습에서는 동작 및 Razor 뷰가 코드 한 줄도 작성 하지 않고 CRUD 작업을 수행 하려면을 사용 하 여 ASP.NET MVC 5 컨트롤러를 만들려면 Visual Studio에서 제공 하는 스 캐 폴딩 ASP.NET 프레임 워크의 장점은 걸립니다. 스 캐 폴딩 프로세스는 SQL 데이터베이스의 데이터 컨텍스트 및 데이터베이스 스키마를 생성 하려면 Entity Framework Code First 사용 합니다.

**Entity Framework에 대 한 Code First**

Entity Framework (EF) 관계형 저장소 스키마를 사용 하 여 직접 프로그래밍 하는 대신 개념적 응용 프로그램 모델을 사용 하 여 프로그래밍 하 여 데이터 액세스 응용 프로그램을 만들 수 있도록 하는 개체 관계형 매퍼 (ORM)입니다.

Entity Framework Code First 모델링 워크플로가 있습니다 EF는 쿼리를 수행할 때 사용 하는 모델을 나타내기 위해 사용자 고유의 도메인 클래스를 사용할 변경 내용 추적 및 업데이트 기능. Code First 개발 워크플로 사용 하지 필요가 데이터베이스를 만들거나 한 스키마를 지정 하 여 응용 프로그램을 시작 합니다. 대신, 응용 프로그램에 가장 적합 한 도메인 모델 개체를 정의 하는 표준.NET 클래스를 작성할 수 있습니다 및 Entity Framework에서 데이터베이스를 만듭니다.

> [!NOTE]
> Entity Framework에 대 한 자세히 알아볼 수 있습니다 [여기](../../../entity-framework.md)합니다.


<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a>1 – 새 모델을 만드는 작업

이제를 정의 합니다는 **사람** 클래스 MVC 컨트롤러 및 뷰를 만들기 위해 스 캐 폴딩 프로세스에서 사용 하는 모델입니다. 만들어 먼저는 **사람** 모델 클래스 및 컨트롤러의 CRUD 작업은 자동으로 만들어집니다 스 캐 폴딩 기능을 사용 하 여 합니다.

1. 열기 **Visual Studio Express 2013 for Web** 및 **MyHybridSite.sln** 솔루션에 있는 **소스/e x 2-MvcScaffolding/시작** 폴더입니다. 또는 계속할 수 있습니다 솔루션으로, 이전 연습에서 가져올 있음을.
2. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **모델** 의 폴더는 **MyHybridSite** 프로젝트를 마우스 선택 **추가 | 클래스 중...** .

    ![사용자 모델 클래스를 추가합니다.](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    *사용자 모델 클래스를 추가합니다.*
3. 에 **새 항목 추가** 대화 상자에서 파일 이름 *Person.cs* 클릭 **추가**합니다.

    ![사용자 모델 클래스 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    *사용자 모델 클래스 만들기*
4. 내용을 대체는 **Person.cs** 다음 코드가 포함 된 파일입니다. 키를 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.

    (코드 조각- *BringingTogetherOneAspNet-e x 2-PersonClass*)

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **MyHybridSite** 선택한 프로젝트 **빌드**, 하거나 키를 눌러 **CTRL + SHIFT + B** 프로젝트를 빌드합니다.

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a>작업 2-MVC 컨트롤러 만들기

이제는 **사람** 모델이 만들어질, Entity Framework를 ASP.NET MVC 스 캐 폴딩 CRUD 컨트롤러 작업 및 보기를 만드는 데 사용할 **사람**합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **컨트롤러** 의 폴더는 **MyHybridSite** 프로젝트를 마우스 선택 **추가 | 새 스 캐 폴드 항목...** .

    ![새 스 캐 폴드 컨트롤러 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    *스 캐 폴드 된 새 컨트롤러 만들기*
2. 에 **추가 스 캐 폴드** 대화 상자에서 **Entity Framework를 사용 하 여 뷰를 포함 된 MVC 5 컨트롤러** 클릭 한 다음 **추가 합니다.**

    ![뷰 및 Entity Framework MVC 5 컨트롤러 선택](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    *뷰 및 Entity Framework MVC 5 컨트롤러 선택*
3. 설정 *MvcPersonController* 로 **컨트롤러 이름**, 선택는 **비동기 컨트롤러 동작을 사용 하 여** 및 옵션을 선택 **사람 (MyHybridSite.Models)**  로 **모델 클래스**합니다.

    ![스 캐 폴딩 포함 된 MVC 컨트롤러 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    *스 캐 폴딩 포함 된 MVC 컨트롤러 추가*
4. 아래 **데이터 컨텍스트 클래스가**, 클릭 **새 데이터 컨텍스트에...** .

    ![새 데이터 컨텍스트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    *새 데이터 컨텍스트 만들기*
5. 에 **새 데이터 컨텍스트에** 대화 상자에 새 데이터 컨텍스트 이름 *PersonContext* 클릭 **추가**합니다.

    ![새 PersonContext 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    *새 PersonContext 형식 만들기*
6. 클릭 **추가** 에 대 한 새 컨트롤러 **사람** 스 캐 폴딩을 사용 합니다. Visual Studio에서 다음 컨트롤러 작업, 사용자 데이터 컨텍스트 및 Razor 뷰가 생성 됩니다.

    ![스 캐 폴딩을 사용 MVC 컨트롤러를 만든 다음](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    *스 캐 폴딩을 사용 MVC 컨트롤러를 만든 다음*
7. 열기는 **MvcPersonController.cs** 파일에 **컨트롤러** 폴더입니다. CRUD 작업 메서드를 자동으로 생성 된 것을 확인 합니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > 선택 하 여는 **비동기 컨트롤러 동작을 사용 하 여** 이전 단계에서 스 캐 폴딩에서 확인란 옵션, Visual Studio에서 사용자 데이터 컨텍스트에 대 한 액세스와 관련 된 모든 작업에 대 한 비동기 작업 메서드를 생성 합니다. 비동기 작업 메서드를 사용 하 여 장기 실행에 대 한, CPU 바인딩되지 않은 요청을 차단 하는 웹 서버의 요청 처리 되는 동안 작업을 수행 것이 좋습니다.

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a>작업 3 – 솔루션 실행

이 작업을 실행 하 다시 확인 하는 솔루션에 대 한 보기 **사람** 예상 대로 작동 합니다. 데이터베이스에 저장 된 성공적으로 확인 하려면 새 사용자를 추가 합니다.

1. 키를 눌러 **F5** 솔루션을 실행 합니다.
2. 로 이동 **/MvcPerson**합니다. 사용자의 목록을 표시 하는 스 캐 폴드 보기 표시 되어야 합니다.
3. 클릭 **새로 만들기** 새 사람을 추가 하려면.

    ![스 캐 폴드 MVC 뷰로 이동](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    *스 캐 폴드 MVC 뷰로 이동*
4. 에 **만들기** 보기에서 제공는 **이름** 및 **Age** 사람과 클릭에 대 한 **만들기**합니다.

    ![새 사용자 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    *새 사용자 추가*
5. 새 사람 목록에 추가 됩니다. 요소 목록에서 클릭 **세부 정보** 사용자의 세부 정보 보기를 표시 합니다. 그런 다음는 **세부 정보** 보려면 클릭 하십시오. **목록으로 돌아가기** 목록 보기도 다시 돌아가십시오.

    ![사용자의 세부 정보 보기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    *사용자의 세부 정보 보기*
6. 클릭는 **삭제** 사람을 삭제 하려면 링크 합니다. 에 **삭제** 보려면 클릭 하십시오. **삭제** 작업을 확인 합니다.

    ![사용자 삭제](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    *사용자 삭제*
7. Visual Studio 및 키를 눌러로 돌아가서 **SHIFT + f 5를 눌러** 디버깅을 중지 합니다.

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a>연습 3: 스 캐 폴딩을 사용 하 여 웹 API 컨트롤러 만들기

Web API 프레임 워크 ASP.NET 스택에서의 일부 이며 일반적으로 데이터 보내기 및 받기 JSON 또는 XML 형식 RESTful API를 통해 쉽게 HTTP 서비스를 구현할 수 있도록 설계 되었습니다.

이 연습에서는 사용 하 여 ASP.NET 스 캐 폴딩 다시 Web API 컨트롤러를 생성 하 합니다. 동일한를 사용 하 여 **사람** 및 **PersonContext** JSON 형식에 동일한 사용자 데이터를 제공 하려면 이전 연습에서 클래스입니다. 보게 같은 ASP.NET 응용 프로그램의 다양 한 방식에서으로 동일한 리소스 노출할 수 있습니다.

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a>작업 1 – 웹 API 컨트롤러 만들기

이 작업에서는 새 만들어집니다 **Web API 컨트롤러** 하는 JSON와 같은 시스템에서 사용할 형식 person 데이터를 제공 합니다.

1. 열려 있지 않으면 열고 **Visual Studio Express 2013 for Web** 엽니다는 **MyHybridSite.sln** 솔루션에 있는 **소스/Ex3-WebAPI/시작** 폴더입니다. 또는 계속할 수 있습니다 솔루션으로, 이전 연습에서 가져올 있음을.

    > [!NOTE]
    > 연습 3 자에서 Begin 솔루션으로 시작 하는 경우 키를 눌러 **CTRL + SHIFT + B** 솔루션을 빌드합니다.
2. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **컨트롤러** 의 폴더는 **MyHybridSite** 프로젝트를 마우스 선택 **추가 | 새 스 캐 폴드 항목...** .

    ![새 스 캐 폴드 컨트롤러 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    *새 스 캐 폴드 컨트롤러 만들기*
3. 에 **추가 스 캐 폴드** 대화 상자에서 **웹 API** 왼쪽된 창에서 **Entity Framework를 사용 하 여 작업을 포함 된 Web API 2 컨트롤러** 가운데 창에서 클릭하고 **추가 합니다.**

    ![작업 및 Entity Framework와 Web API 2 컨트롤러를 선택 하면](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "동작 및 Entity Framework 포함 된 Web API 2 컨트롤러 선택")

    *작업 및 Entity Framework와 Web API 2 컨트롤러 선택*
4. 설정 *ApiPersonController* 로 **컨트롤러 이름**, 선택는 **비동기 컨트롤러 동작을 사용 하 여** 및 옵션을 선택 **사람 (MyHybridSite.Models)**  및 **PersonContext (MyHybridSite.Models)** 로 **모델** 및 **데이터 컨텍스트** 각각. **추가**를 클릭합니다.

    ![스 캐 폴딩 사용 하 여 웹 API 컨트롤러 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "스 캐 폴딩 사용 하 여 Web API 컨트롤러 추가")

    *스 캐 폴딩 사용 하 여 Web API 컨트롤러 추가*
5. Visual Studio에서 생성 한 다음는 **ApiPersonController** 데이터와 함께 작동 하도록 4 개의 CRUD 동작이 포함 된 클래스입니다.

    ![스 캐 폴딩을 사용 Web API 컨트롤러를 만든 다음](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "스 캐 폴딩을 사용 Web API 컨트롤러를 만든 다음")

    *스 캐 폴딩을 사용 Web API 컨트롤러를 만든 다음*
6. 열기는 **ApiPersonController.cs** 파일을 검사 하는 *GetPeople* 동작 메서드. 이 메서드는 db 필드의 쿼리 **PersonContext** 사용자 데이터를 가져오기 위해 유형입니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. 이제 메서드 정의 위의 설명을 확인 합니다. 사용 하는 다음 태스크에서는 해당이 동작을 표시 하는 URI를 제공 합니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > 기본적으로 웹 API에 대 한 쿼리로 catch 하도록 구성 된 */api* MVC 컨트롤러와 충돌을 피하기 위해 경로입니다. 이 설정을 변경 해야 할 경우 참조 [ASP.NET Web API에서 라우팅](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)합니다.

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a>작업 2-솔루션 실행

이 작업을 사용 하 여 Internet Explorer **F12 개발자 도구** Web API 컨트롤러 로부터 전체 응답을 검사 합니다. 응용 프로그램 데이터에 대 한 자세한 정보를 가져오려는 네트워크 트래픽을 캡처할 수는 어떻게 확인할 수 있습니다.

> [!NOTE]
> 다음 사항을 확인 **Internet Explorer** 에서 선택한는 **시작** 단추 Visual Studio 도구 모음에 있는 합니다.
> 
> ![Internet Explorer 옵션](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> **F12 개발자 도구** 넓은 집합이이 실습 랩에는 적용 되지 않는 기능입니다. 항목에 대 한 자세한 내용을 보려면 원하는 경우 참조 [F12 개발자 도구를 사용 하 여](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85))합니다.


1. 키를 눌러 **F5** 솔루션을 실행 합니다.

    > [!NOTE]
    > 이 작업을 올바르게 실행 하려면 응용 프로그램에 데이터가 포함 해야 합니다. 데이터베이스가 비어 있으면 다시 Exercise 2에서 작업 3으로 돌아가서 MVC 뷰를 사용 하는 새 사용자를 만드는 방법에 대 한 단계를 수행 합니다.
2. 키를 눌러 브라우저에서 **F12** 열려는 **개발자 도구** 패널입니다. 키를 누릅니다 **CTRL** + **4** 하거나 클릭 하 고 **네트워크** 네트워크 트래픽 캡처를 시작 하 고 녹색 화살표 단추 아이콘을 클릭 합니다.

    ![웹 API 네트워크 캡처를 시작](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Web API 시작 네트워크 캡처")

    *웹 API 네트워크 캡처를 시작합니다.*
3. 추가 **api/ApiPerson** 브라우저의 주소 표시줄에 URL을 합니다. 응답의 세부 정보를 이제 검사 하는 **ApiPersonController**합니다.

    ![웹 API를 통해 사용자 데이터를 검색](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "웹 API를 통해 사용자 데이터 검색")

    *웹 API를 통해 사용자 데이터 검색*

    > [!NOTE]
    > 다운로드를 완료 한 후에 다운로드 한 파일 작업으로 설정할 하 라는 메시지가 표시 됩니다. 대화 상자를 개발자 도구 창을 통해 응답 콘텐츠를 볼 수 있도록 열어 둡니다.
4. 이제는 응답의 본문을 조사 합니다. 이 작업을 수행 하려면는 **세부 정보** 탭을 클릭 한 다음 **응답 본문**합니다. 속성을 가진 개체의 목록을 다운로드 한 데이터를 확인할 수 있습니다 **Id**, **이름** 및 **Age** 에 해당 하는 **사람** 클래스입니다.

    ![보기 웹 API 응답 본문](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "보기 웹 API 응답 본문")

    *보기 웹 API 응답 본문*

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a>작업 3 – 웹 API 도움말 페이지 추가

웹 API를 만들 때에 도움말 페이지를 다른 개발자가 API를 호출 하는 방법을 알 수 있도록 유용 합니다. 만들고 설명서 페이지를 수동으로 업데이트할 수 있지만 자동 생성 유지 관리 작업을 수행할 필요가 없도록 하는 것이 좋습니다. 이 작업에서는 솔루션에 웹 API 도움말 페이지를 자동으로 생성 하는 Nuget 패키지를 사용 합니다.

1. **도구** 선택 Visual Studio에서 메뉴 **라이브러리 패키지 관리자**, 클릭 하 고 **패키지 관리자 콘솔**합니다.
2. 에 **패키지 관리자 콘솔** 창에서 다음 명령을 실행 합니다.

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > **Microsoft.AspNet.WebApi.HelpPage** 는 필요한 어셈블리를 설치 하 고 아래 도움말 페이지에 대 한 MVC 뷰를 추가 하는 패키지는 **영역/HelpPage** 폴더입니다.

    ![HelpPage 영역](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage 영역")

    *HelpPage 영역*
3. 기본적으로 도움말 페이지는 설명서에 대 한 자리 표시자 문자열을 제공 합니다. XML 문서 주석에서 문서를 만들 수에 사용할 수 있습니다. 이 기능을 사용 하려면 엽니다는 **HelpPageConfig.cs** 에 있는 파일의 **영역/HelpPage/응용 프로그램\_시작** 폴더에 다음 줄에서 주석 처리 제거:

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. **솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 **MyHybridSite**선택, **속성** 클릭는 **빌드** 탭 합니다.

    ![빌드 탭](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "섹션 빌드")

    *빌드 탭*
5. 아래 **출력**선택, **XML 문서 파일**합니다. 편집 상자에 입력 **앱\_Data/XmlDocument.xml**합니다.

    ![빌드 탭에는 섹션 출력](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "출력 빌드 탭에는 섹션")

    *빌드 탭에 출력 섹션*
6. 키를 눌러 **CTRL** + **S** 여 변경 내용을 저장 합니다.
7. 열기는 **ApiPersonController.cs** 에서 파일의 **컨트롤러** 폴더입니다.
8. 사이 새 줄 입력는 *GetPeople* 메서드 서명 및 */ api/ApiPerson 가져오기 /* 주석 처리 한 다음 세 개의 슬래시를 입력 합니다.

    > [!NOTE]
    > Visual Studio는 자동으로 메서드 설명서를 정의 하는 XML 요소를 삽입 합니다.
9. 요약 텍스트와 반환 값에 대 한 추가 *GetPeople* 메서드. 다음과 같이 표시 됩니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. 키를 눌러 **F5** 솔루션을 실행 합니다.
11. 추가 **/help** 도움말 페이지로 이동 하기 위해 주소 표시줄에 URL을 합니다.

    ![ASP.NET Web API 도움말 페이지](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API 도움말 페이지")

    *ASP.NET Web API 도움말 페이지*

    > [!NOTE]
    > 페이지의 기본 콘텐츠는 컨트롤러로 그룹화 된, Api의 테이블입니다. 사용 하 여 테이블 항목으로 동적으로 생성 된 **IApiExplorer** 인터페이스입니다. 를 추가 하거나 업데이트 된 API 컨트롤러는 테이블이 자동으로 업데이트 됩니다 다음에 응용 프로그램을 빌드합니다.
    > 
    > **API** 열에 나열 된 HTTP 메서드 및 상대 URI입니다. **설명** 열 메서드 설명서에서 추출 된 정보를 포함 합니다.
12. 메서드 정의 위에 추가 설명 하는 참고 설명 열에 표시 됩니다.

    ![API 메서드 설명](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API 메서드 설명")

    *API 메서드 설명*
13. 샘플 응답 본문을 포함 하 여 더 자세한 정보를 페이지로 이동 하 고 API 메서드 중 하나를 클릭 합니다.

    ![세부 정보 페이지](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "세부 정보 페이지")

    *세부 정보 페이지*

* * *

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩을 완료 하 여 배웠습니다 하는 방법:

- Visual Studio 2013에서 한 ASP.NET 환경을 사용 하 여 새 웹 응용 프로그램 만들기
- 하나의 단일 프로젝트에 여러 ASP.NET 기술의 통합
- ASP.NET 스 캐 폴딩을 사용 하 여 모델 클래스에서 MVC 컨트롤러와 뷰를 생성 합니다.
- 비동기 프로그래밍 및 Entity Framework를 통해 데이터 액세스와 같은 기능을 사용 하는 Web API 컨트롤러 생성
- 컨트롤러에 대 한 웹 API 도움말 페이지를 자동으로 생성
