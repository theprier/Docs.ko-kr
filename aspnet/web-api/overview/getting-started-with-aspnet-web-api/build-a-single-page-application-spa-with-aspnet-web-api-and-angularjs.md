---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: '실습: ASP.NET Web API 및 Angular.js를 사용 하 여 단일 페이지 응용 프로그램 (SPA) 빌드 | Microsoft Docs'
author: rick-anderson
description: 기존 웹 응용 프로그램에서 클라이언트 (브라우저) 페이지를 요청 하 여 서버와의 통신을 시작 합니다. 서버는 다음 요청을 처리 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/30/2015
ms.topic: article
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 174084d6923cf1fa445485b7c0dc639a240720a5
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370865"
---
<a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a>실습: ASP.NET Web API 및 Angular.js를 사용 하 여 단일 페이지 응용 프로그램 (SPA) 빌드
====================
[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트 다운로드](http://aka.ms/webcamps-training-kit)

> 기존 웹 응용 프로그램에서 클라이언트 (브라우저) 페이지를 요청 하 여 서버와의 통신을 시작 합니다. 그런 다음 서버는 요청을 처리 하 고 페이지의 HTML 클라이언트에 보냅니다. – 예를 들어 사용자 링크에 이동 하거나 데이터를 사용 하 여 폼을 전송 – 페이지를 사용 하 여 후속 상호 작용에서 새 요청을 서버로 전송 되 고 흐름이 다시 시작: 서버가 요청을 처리 하 고 새 작업 요청에 대 한 응답으로 브라우저에 새 페이지를 보냅니다 클라이언트에서 ed 합니다.
> 
> 단일 페이지 응용 프로그램 (Spa)에서 전체 페이지 로드 브라우저에서 초기 요청 후 되었지만 후속 상호 작용 Ajax 요청을 통해 수행 합니다. 즉, 브라우저가 변경 되었으면 하는 페이지의 부분만 업데이트 해야 합니다. 전체 페이지를 로드할 필요가 없습니다 있습니다. SPA 접근 방식은 유연한 환경을 사용자 동작에 응답 하도록 응용 프로그램에서 소요 된 시간을 줄입니다.
> 
> SPA의 아키텍처는 기존 웹 응용 프로그램에 존재 하지 않는 몇 가지 문제에 포함 됩니다. 그러나 ASP.NET Web API와 같은 신기술을 JavaScript 프레임 워크 AngularJS 등 CSS3에서 제공 하는 새 스타일 기능 쉽게 디자인 하 고 Spa를 만들어야 합니다.
> 
> 이 실습 랩에서 Geek 퀴즈, SPA 개념을 기반으로 하는 기타 정보 웹 사이트를 구현 하는 이러한 기술 활용을 걸립니다. 먼저 퀴즈 질문을 검색 하 고 답변을 저장할 필요한 끝점을 노출할 ASP.NET Web API를 사용 하 여 서비스 계층을 구현 합니다. 그런 다음, AngularJS 및 CSS3 변환 효과 사용 하 여 풍부 하 고 응답성이 뛰어난 UI를 빌드할 수 있습니다.
> 
> 웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)합니다.


## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 학습할 방법:

- JSON 데이터를 수신 하는 ASP.NET Web API 서비스 만들기
- AngularJS를 사용 하 여 반응 형 UI 만들기
- CSS3 변환 사용 하 여 UI 환경을 향상합니다

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

다음는이 실습을 완료 해야 합니다.

- [Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상

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

1. [Web API 만들기](#Exercise1)
2. [SPA 인터페이스 만들기](#Exercise2)

이 랩을 완료 하기 위한 예상 시간: **60 분**

> [!NOTE]
> Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션에는 특정 개발 스타일에 맞게 설계 되었습니다 및 창 레이아웃, 동작 편집기, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 랩의 절차에서는 사용 하는 경우 Visual Studio에서 지정된 된 태스크를 수행 하는 데 필요한 작업을 설명 합니다 **일반 개발 설정** 컬렉션입니다. 개발 환경에 대 한 다양 한 설정 컬렉션을 선택 하는 경우를 고려해 야 하는 단계에 차이가 있을 수 있습니다.


<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a>연습 1: Web API 만들기

SPA의 주요 부분 중 하나는 서비스 계층입니다. 이 UI와 해당 호출에 응답 반환 데이터를 보낸 Ajax 호출을 처리 하는 일을 담당 합니다. 검색 데이터를 구문 분석 하 고 클라이언트에서 사용 하기 위해 컴퓨터가 읽을 수 있는 형식으로 표시 합니다.

Web API 프레임 워크 ASP.NET 스택에의 일부 이며는 쉽게 일반적으로 데이터 보내기 및 받기 JSON 또는 XML 형식 RESTful API를 통해 HTTP 서비스를 구현 하도록 설계 되었습니다. 이 연습에서 Geek 퀴즈 응용 프로그램을 호스트 하 고 다음 백 엔드 서비스를 노출 하 고 ASP.NET Web API를 사용 하 여 퀴즈 데이터 유지를 구현 하는 웹 사이트를 만듭니다.

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a>작업 1-Geek 퀴즈에 대 한 초기 프로젝트 만들기

이 태스크에서는 먼저 기반으로 하는 ASP.NET Web API에 대 한 지원을 사용 하 여 새 ASP.NET MVC 프로젝트 만들기를 **One ASP.NET** 프로젝트 Visual Studio와 함께 제공 되는 형식입니다. **One ASP.NET** 를 모든 ASP.NET 기술을 통합 하 고 혼합 하 고 필요에 따라 일치 하는 옵션이 있습니다. 다음 Entity Framework의 모델 클래스와 데이터베이스 initializator 퀴즈 질문에 삽입할 추가 합니다.

1. 오픈 **Visual Studio Express 2013 for Web** 선택한 **파일 | 새 프로젝트...**  새 솔루션을 시작 합니다.

    ![새 프로젝트를 만드는](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "새 프로젝트 만들기")

    *새 프로젝트 만들기*
2. 에 **새 프로젝트** 대화 상자에서 **ASP.NET 웹 응용 프로그램** 아래에서 **Visual C# | 웹** 탭 합니다. 있는지 **.NET Framework 4.5** 는 이름을 선택 *GeekQuiz*, 선택는 **위치** 클릭 **확인**합니다.

    ![새 ASP.NET 웹 응용 프로그램 프로젝트를 만드는](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "새 ASP.NET 웹 응용 프로그램 프로젝트 만들기")

    *새 ASP.NET 웹 응용 프로그램 프로젝트 만들기*
3. 에 **새 ASP.NET 프로젝트** 대화 상자에서를 **MVC** 템플릿을 선택한 합니다 **Web API** 옵션. 또한 있는지 확인 합니다 **인증** 옵션을 설정 **개별 사용자 계정**합니다. 계속하려면 **확인** 을 클릭합니다.

    ![Web API 구성 요소를 포함 하 여 MVC 템플릿을 사용 하 여 새 프로젝트 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    *Web API 구성 요소를 포함 하 여 MVC 템플릿을 사용 하 여 새 프로젝트 만들기*
4. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더를 **GeekQuiz** 프로젝트를 마우스 **추가 | 기존 항목...** .

    ![기존 항목 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "기존 항목 추가")

    *기존 항목 추가*
5. 에 **기존 항목 추가** 대화 상자에서 **소스/자산/모델** 폴더 및 파일을 모두 선택 합니다. **추가**를 클릭합니다.

    ![모델 자산 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "모델 자산 추가")

    *모델 자산 추가*

    > [!NOTE]
    > 이러한 파일에 추가 하 여 데이터 모델, Entity Framework의 데이터베이스 컨텍스트 및 Geek 퀴즈 응용 프로그램에 대 한 데이터베이스 이니셜라이저 추가 됩니다.
    > 
    > **Entity Framework (EF)** 는 관계형 저장소 스키마를 사용 하 여 직접 프로그래밍 하는 대신 개념적 응용 프로그램 모델을 사용 하 여 프로그래밍 하 여 데이터 액세스 응용 프로그램을 만들 수 있도록 개체 관계형 매퍼 (ORM). Entity Framework에 대 한 자세히 알아볼 수 있습니다 [여기](../../../entity-framework.md)합니다.
    > 
    > 다음은 방금 추가한 클래스의 설명입니다.
    > 
    > - **TriviaOption:** 퀴즈 질문을 사용 하 여 연결 된 단일 옵션을 나타냅니다
    > - **: TriviaQuestion** 퀴즈 질문을 나타내며를 통해 연결된 옵션을 제공 합니다 **옵션** 속성
    > - **TriviaAnswer:** 퀴즈 질문에 대 한 응답에서 사용자가 선택한 옵션을 나타냅니다
    > - **TriviaContext:** Geek 퀴즈 응용 프로그램의 Entity Framework의 데이터베이스 컨텍스트를 나타냅니다. 이 클래스에서 파생 됩니다 **DContext** 노출 **DbSet** 위에 설명 된 엔터티의 컬렉션을 나타내는 속성입니다.
    > - **TriviaDatabaseInitializer:** 에 대 한 Entity Framework 이니셜라이저 구현의 합니다 **TriviaContext** 클래스에서 상속 하는 **CreateDatabaseIfNotExists**합니다. 에 지정 된 엔터티를 삽입 합니다.이 클래스의 기본 동작은 존재 하지 않는 경우에 데이터베이스를 만들려고 합니다는 **시드** 메서드.
6. 엽니다는 **Global.asax.cs** 파일을 추가한 다음 문을 사용 하 여 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. 시작 부분에 다음 코드를 추가 합니다 **응용 프로그램\_시작** 설정 하는 방법의 **TriviaDatabaseInitializer** 데이터베이스 이니셜라이저를 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. 수정 된 **홈** 인증 된 사용자에 대 한 액세스를 제한 하는 컨트롤러입니다. 이 위해 엽니다는 **HomeController.cs** 파일을 **컨트롤러** 폴더 추가 **권한 부여** 특성을 **HomeController**클래스 정의 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > 합니다 **권한 부여** 사용자가 인증 하는 경우 확인을 필터링 합니다. 사용자 인증 되지 않은 경우 다음 작업을 호출 하지 않고 HTTP 상태 코드 401 (권한 없음)를 반환 합니다. 컨트롤러 수준에서 전역으로 또는 개별 작업 수준에서 필터를 적용할 수 있습니다.
9. 이제 웹 페이지 및 브랜딩 레이아웃을 사용자 지정 합니다. 이 작업을 수행 하려면 엽니다는  **\_Layout.cshtml** 파일을 **뷰 | 공유** 폴더의 콘텐츠를 업데이트 합니다 **&lt;title&gt;** 대체 하 여 요소 *내 ASP.NET 응용 프로그램* 사용 하 여 *Geek 퀴즈* .

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. 동일한 파일에서 제거 하 여 탐색 모음을 업데이트 합니다 *에 대 한* 및 *연락처* 링크 및 이름 바꾸기는 *홈* 연결할 *재생*합니다. 또한 이름 바꾸기는 *응용 프로그램 이름* 연결할 *매니아 퀴즈*합니다. HTML 탐색 모음에 다음 코드와 같습니다.

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. 대체 하 여 레이아웃 페이지의 바닥글 업데이트 *내 ASP.NET 응용 프로그램* 사용 하 여 *매니아 퀴즈*합니다. 이 위해의 콘텐츠를 대체 합니다 **&lt;바닥글&gt;** 요소를 다음 강조 표시 된 코드로.

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a>작업 2-TriviaController Web API 만들기

이전 작업에서는 Geek 퀴즈 웹 응용 프로그램의 초기 구조를 만들었습니다. 이제 퀴즈 데이터 모델과 상호 작용 하 고 다음 작업을 노출 하는 간단한 Web API 서비스를 빌드합니다.

- **GET/api/퀴즈**: 인증 된 사용자가 대답할 수 퀴즈 목록에서 다음 질문을 검색 합니다.
- **POST/api/퀴즈**: 인증 된 사용자 지정 퀴즈 답변을 저장 합니다.

Web API 컨트롤러 클래스에 대 한 초기 계획을 만들려면 Visual Studio에서 제공 하는 ASP.NET 스 캐 폴딩 도구를 사용 합니다.

1. 엽니다는 **WebApiConfig.cs** 파일을 **앱\_시작** 폴더. 이 파일 경로 Web API 컨트롤러 작업에 매핑되는 방식을 같은 Web API 서비스의 구성을 정의 합니다.
2. 다음 추가 문을 사용 하 여 파일의 시작 부분에 있습니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. 다음 강조 표시 된 코드를 추가 합니다 **등록** 전역적으로 Web API 작업 메서드에 의해 검색 되는 JSON 데이터에 대 한 포맷터를 구성 하는 방법입니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > **CamelCasePropertyNamesContractResolver** 자동으로 속성 이름을 변환 *카멜식 대 /* 사례는 JavaScript의 속성 이름에 대 한 일반 규칙입니다.
4. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 폴더를 **GeekQuiz** 프로젝트를 마우스 **추가 | 스 캐 폴드 된 새 항목...** .

    ![새 스 캐 폴드 된 항목을 만드는](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "스 캐 폴드 된 새 항목 만들기")

    *새 스 캐 폴드 된 항목 만들기*
5. 에 **스 캐 폴드 추가** 대화 상자에서 확인를 **일반적인** 왼쪽된 창에서 노드를 선택 합니다. 다음을 선택 합니다 **Web API 2 컨트롤러-비어 있음** 클릭 확인 하 고 가운데 창에서 템플릿을 **추가**합니다.

    ![웹 API 2 컨트롤러 빈 템플릿을 선택 하](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "웹 API 2 컨트롤러 빈 템플릿 선택")

    *웹 API 2 컨트롤러 빈 템플릿 선택*

    > [!NOTE]
    > **ASP.NET 스 캐 폴딩** 는 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크입니다. Visual Studio 2013 MVC 및 Web API 프로젝트에 대 한 사전 설치 된 코드 생성기를 포함합니다. 신속 하 게 표준 데이터 작업을 개발 하는 데 필요한 시간을 줄이기 위해 데이터 모델과 상호 작용 하는 코드를 추가 하려는 경우 프로젝트에서 스 캐 폴딩을 사용 해야 합니다.
    > 
    > 스 캐 폴딩 프로세스 하면 필요한 모든 종속성을 프로젝트에 설치 됩니다. 예를 들어, 빈 ASP.NET 프로젝트를 시작 하 고 다음 스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 추가할 경우 필요한 웹 API NuGet 패키지와 참조를 프로젝트에 자동으로 추가 됩니다.
6. 에 **컨트롤러 추가** 대화 상자에서 *TriviaController* 에 **컨트롤러 이름** 입력란을 클릭 **추가**합니다.

    ![기타 정보 컨트롤러 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "퀴즈 컨트롤러 추가")

    *기타 정보 컨트롤러 추가*
7. **TriviaController.cs** 파일에 추가 됩니다 합니다 **컨트롤러** 폴더를 **GeekQuiz** 빈 포함 된 프로젝트 **TriviaController** 클래스입니다. 다음 추가 using 문을 파일의 시작 부분에 있습니다.

    (코드 조각- *AspNetWebApiSpa-e x 1-TriviaControllerUsings*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. 시작 부분에 다음 코드를 추가 합니다 **TriviaController** 정의 초기화 및 삭제 하는 클래스는 **TriviaContext** 컨트롤러의 인스턴스.

    (코드 조각- *AspNetWebApiSpa-e x 1-TriviaControllerContext*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > **Dispose** 메서드의 **TriviaController** 를 호출 하는 **Dispose** 메서드의 **TriviaContext** 하도록 하는 경우 모든 컨텍스트 개체에서 사용 하는 리소스가 해제 됩니다 때 합니다 **TriviaContext** 인스턴스가 삭제 되거나 가비지 수집 합니다. Entity Framework에서 연 모든 데이터베이스 연결을 닫는 것이 여기 있습니다.
9. 끝에 다음 도우미 메서드를 추가 합니다 **TriviaController** 클래스입니다. 이 메서드는 다음 퀴즈 질문에 응답 하도록 지정된 된 사용자 데이터베이스에서 검색 합니다.

    (코드 조각- *AspNetWebApiSpa-e x 1-TriviaControllerNextQuestion*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. 다음을 추가 합니다 **가져오기** 하는 작업 메서드는 **TriviaController** 클래스입니다. 이 작업 메서드를 호출 합니다 **NextQuestionAsync** 인증된 된 사용자에 대 한 다음 질문을 검색 하는 이전 단계에서 정의 하는 도우미 메서드입니다.

    (코드 조각- *AspNetWebApiSpa-e x 1-TriviaControllerGetAction*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. 끝에 다음 도우미 메서드를 추가 합니다 **TriviaController** 클래스입니다. 이 메서드는 데이터베이스에 지정 된 응답을 저장 하 고 답이 맞으면 여부 나타내는 부울 값을 반환 합니다.

    (코드 조각- *AspNetWebApiSpa-e x 1-TriviaControllerStoreAsync*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. 다음을 추가 합니다 **게시물** 하는 작업 메서드는 **TriviaController** 클래스입니다. 이 동작 메서드에 인증 된 사용자 및 호출에 대 한 답을 연결 합니다 **StoreAsync** 도우미 메서드입니다. 그런 다음 도우미 메서드에 의해 반환 되는 부울 값을 사용 하 여 응답을 보냅니다.

    (코드 조각- *AspNetWebApiSpa-e x 1-TriviaControllerPostAction*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. 추가 하 여 인증 된 사용자에 게 액세스를 제한 하는 Web API 컨트롤러를 수정 합니다 **권한 부여** 특성을 합니다 **TriviaController** 클래스 정의 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>작업 3 – 솔루션 실행

이 작업에서는 이전 태스크에서 만든 웹 API 서비스를 예상 대로 작동 하는지 확인 합니다. Internet Explorer를 사용할지 **F12 개발자 도구** 네트워크 트래픽 캡처 및 Web API 서비스의 전체 응답을 검사 합니다.

> [!NOTE]
> 했는지 **Internet Explorer** 가 선택 합니다 **시작** Visual Studio 도구 모음에 있는 단추입니다.
> 
> ![Internet Explorer 옵션](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)


1. 키를 눌러 **F5** 솔루션을 실행 합니다. 합니다 **로그인** 페이지가 브라우저에 표시 됩니다.

    > [!NOTE]
    > 응용 프로그램이 시작 되 면 기본 MVC 경로 트리거될에 매핑되는 기본적으로는 **인덱스** 작업을 **HomeController** 클래스입니다. 하므로 **HomeController** 인증 된 사용자 에게만 부여 됩니다 (기억 사용 하 여 해당 클래스를 데코 레이트 하는 **권한 부여** 실습 1에서 특성) 인증 사용자 아직 응용 프로그램 이며 로그인 페이지를 원래 요청을 리디렉션합니다.

    ![솔루션을 실행](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "솔루션 실행")

    *솔루션 실행*
2. 클릭 **등록** 새 사용자를 만듭니다.

    ![새 사용자를 등록](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "새 사용자 등록")

    *새 사용자 등록*
3. 에 **등록** 페이지에서 입력을 **사용자 이름** 및 **암호**를 클릭 하 고 **등록**합니다.

    ![등록 페이지](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "등록 페이지")

    *등록 페이지*
4. 응용 프로그램에 새 계정을 등록 하 고 사용자가 인증 하 고 홈 페이지로 다시 리디렉션됩니다.

    ![사용자가 인증](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "인증 된 사용자")

    *사용자가 인증*
5. 키를 눌러 브라우저에서 **F12** 열려는 합니다 **개발자 도구** 패널입니다. 키를 눌러 **CTRL + 4** 누르거나를 **네트워크** 아이콘을 한 다음 단추를 클릭 하 고 녹색 화살표 네트워크 트래픽 캡처를 시작 합니다.

    ![Web API 네트워크 캡처를 시작](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Web API 시작 네트워크 캡처")

    *Web API 네트워크 캡처를 시작합니다.*
6. 추가 **api/퀴즈** 브라우저의 주소 표시줄에서 URL로 합니다. 이제 응답의 세부 정보를 검사 하는 합니다 **가져옵니다** 의 동작 메서드에 **TriviaController**합니다.

    ![웹 API를 통해 다음 질문 데이터를 검색할](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "웹 API를 통해 다음 질문 데이터를 검색 합니다.")

    *웹 API를 통해 다음 질문 데이터를 검색합니다.*

    > [!NOTE]
    > 다운로드가 완료 되 면 다운로드 한 파일을 사용 하 여 작업을 할 수 있도록 묻는 메시지가 나타납니다. 대화 상자는 개발자 도구 창을 통해 응답 콘텐츠를 볼 수 있도록 열어 둡니다.
7. 이제는 응답의 본문을 조사 합니다. 이렇게 하려면 클릭 합니다 **세부 정보** 탭을 클릭 한 다음 **응답 본문**합니다. 다운로드 한 데이터 속성을 사용 하 여 개체를 확인할 수 있습니다 **옵션** (의 목록인 **TriviaOption** 개체), **id** 및 **제목** 에 해당 하는 **TriviaQuestion** 클래스입니다.

    ![웹 API 응답 본문을 보는](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "웹 API 응답 본문 보기")

    *웹 API 응답 본문 보기*
8. Visual Studio 및 키를 눌러도 돌아가 **shift+f5** 디버깅을 중지 합니다.

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a>연습 2: SPA 인터페이스를 만드는 방법

이 연습에서는 먼저 빌드합니다 Geek 퀴즈의 웹 프런트 엔드 부분을 사용 하 여 단일 페이지 응용 프로그램 상호 작용에 집중 **AngularJS**합니다. 풍부한 애니메이션을 수행 하 고 다음 질문 중 하나에서 전환 하는 경우 하면 컨텍스트 전환을 활용 시각 효과 제공 하는 CSS3 사용 하 여 사용자 환경을 개선 다음 있습니다.

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a>작업 1-AngularJS를 사용 하 여 SPA 인터페이스를 만드는 방법

이 작업에서는 사용 하 여 **AngularJS** Geek 퀴즈 응용 프로그램의 클라이언트 쪽을 구현 합니다. **AngularJS** 는 브라우저 기반 응용 프로그램을 확대 하는 오픈 소스 JavaScript 프레임 워크 *모델-뷰-컨트롤러* (MVC) 기능을 모두 개발을 촉진 하 고 테스트 합니다.

Visual Studio의 패키지 관리자 콘솔에서 AngularJS를 설치 하 여 시작 합니다. 그런 다음 퀴즈 질문 및 답변에서 AngularJS 템플릿 엔진을 사용 하 여 렌더링할 뷰 Geek 퀴즈 앱의 동작을 제공 하도록 컨트롤러를 만듭니다.

> [!NOTE]
> AngularJS에 대 한 자세한 내용은 참조 [ [ http://angularjs.org/ ](http://angularjs.org/) ](http://angularjs.org/)합니다.


1. 엽니다 **Visual Studio Express 2013 for Web** 연 합니다 **GeekQuiz.sln** 솔루션을 **소스/e x 2-CreatingASPAInterface/시작** 폴더. 또는 계속할 수 있습니다 솔루션을 사용 하 여 이전 연습에서 얻은.
2. 엽니다는 **패키지 관리자 콘솔** 에서 **도구** | **라이브러리 패키지 관리자**합니다. 설치 하려면 다음 명령을 입력 합니다 **AngularJS.Core** NuGet 패키지.

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **스크립트** 폴더를 **GeekQuiz** 프로젝트를 마우스 **추가 | 새 폴더**합니다. 폴더의 이름을 **앱** 누릅니다 **Enter**합니다.
4. 마우스 오른쪽 단추로 클릭 합니다 **앱** 폴더 바로 전에 만들고 선택 **추가 | JavaScript 파일**합니다.

    ![새 JavaScript 파일 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    *새 JavaScript 파일 만들기*
5. 에 **항목에 대 한 이름 지정** 대화 상자에서 *퀴즈 컨트롤러* 에 **항목 이름** 입력란을 클릭 **확인**합니다.

    ![새 JavaScript 파일 이름 지정](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    *새 JavaScript 파일 이름 지정*
6. 에 **퀴즈 controller.js** 파일을 다음 코드를 선언 하 고 초기화 AngularJS 추가 **QuizCtrl** 컨트롤러입니다.

    (코드 조각- *AspNetWebApiSpa-e x 2-AngularQuizController*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > 생성자 함수는 **QuizCtrl** 컨트롤러 라는 injectable 매개 변수를 예상 **$scope**합니다. 범위의 초기 상태를 설정 해야 생성자 함수에서 속성을 연결 하 여 합니다 **$scope** 개체입니다. 속성을 포함 합니다 **뷰 모델**, 및 컨트롤러를 등록할 때 서식 파일에 액세스할 수 있습니다.
    > 
    > 합니다 **QuizCtrl** 컨트롤러 라는 모듈 내에서 정의 됩니다 **QuizApp**합니다. 모듈은 별도 구성 요소에 응용 프로그램 중단할 수 있는 작업 단위입니다. 모듈을 사용 하는 데 필요한 주요 이점은 코드를 이해 하기 쉬운 단위 테스트, 재사용 및 유지 관리를 용이 하 게 있다는 것입니다.
7. 이제 보기에서 트리거되는 이벤트에 대응 하기 위해 범위에 동작을 추가 합니다. 끝에 다음 코드를 추가 합니다 **QuizCtrl** 정의 하는 컨트롤러를 **nextQuestion** 함수를 **$scope** 개체입니다.

    (코드 조각- *AspNetWebApiSpa-e x 2-AngularQuizControllerNextQuestion*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > 이 함수에서 다음 질문을 검색 합니다는 **퀴즈** Web API는 이전 연습에서 만든 및 질문 데이터를 연결 합니다 **$scope** 개체입니다.
8. 끝에 다음 코드를 삽입 합니다 **QuizCtrl** 정의 하는 컨트롤러를 **sendAnswer** 함수를 **$scope** 개체입니다.

    (코드 조각- *AspNetWebApiSpa-e x 2-AngularQuizControllerSendAnswer*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > 이 함수를 사용자가 선택한 응답을 보냅니다 합니다 **퀴즈** Web API에서 여부 답이 맞으면 – 하는 경우 – 즉, 결과 저장 하 고는 **$scope** 개체.
    > 
    > **nextQuestion** 하 고 **sendAnswer** AngularJS를 사용 하 여 위의 함수 **$http** XMLHttpRequest 통해 웹 API와의 통신을 추상화 하는 개체 브라우저에서 JavaScript 개체입니다. AngularJS 더 높은 수준의 RESTful Api를 통해 리소스에 대 한 CRUD 작업을 수행 하는 추상화를 제공 하는 다른 서비스를 지원 합니다. AngularJS **$resource** 개체에 상호 작용 하지 않고도 높은 수준의 동작을 제공 하는 작업 메서드는 **$http** 개체입니다. 사용 하는 것이 좋습니다 합니다 **$resource** CRUD 모델을 해야 하는 시나리오에서 개체 ((영문) 정보를 참조 합니다 [$resource 설명서](https://docs.angularjs.org/api/ngResource/service/$resource)).
9. 다음 단계 퀴즈에 대 한 보기를 정의 하는 AngularJS 템플릿을 만드는 것입니다. 이 작업을 수행 하려면 엽니다는 **Index.cshtml** 파일을 **뷰 | 홈** 폴더 및 내용 다음 코드로 바꿉니다.

    (코드 조각- *AspNetWebApiSpa-e x 2-GeekQuizView*)

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > AngularJS 템플릿은 모델 및 컨트롤러의 정보를 사용 하 여 브라우저에서 사용자에 게 동적 보기에 정적 태그를 변환 하는 선언적 사양입니다. 다음은 AngularJS 요소 및 템플릿에서 사용할 수 있는 요소 특성의 예입니다.
    > 
    > - 합니다 **ng 앱** 지시문은 AngularJS 응용 프로그램의 루트 요소를 나타내는 DOM 요소입니다.
    > - 합니다 **ng-컨트롤러** 지시문 지점 지시문 선언 된 위치에서 DOM에 컨트롤러를 연결 합니다.
    > - 중괄호 표기법 **{{}}** 컨트롤러에 정의 된 범위 속성에 대 한 바인딩을 나타냅니다.
    > - 합니다 **ng 원클릭** 지시문 사용에 대 한 응답 사용자가 클릭할 때 범위에 정의 된 함수를 호출 하는 합니다.
10. 열기는 **Site.css** 파일을 **콘텐츠** 폴더 퀴즈 뷰에 대 한 모양 및 느낌을 제공 하는 파일의 끝에 다음 강조 표시 된 스타일을 추가 하 고 합니다.

    (코드 조각- *AspNetWebApiSpa-e x 2-GeekQuizStyles*)

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a>작업 2-솔루션 실행

실행 하는이 태스크에서는 새 사용자를 사용 하 여 솔루션 일부의 퀴즈 질문에 대답 하는 AngularJS를 사용 하 여 빌드한 있습니다 인터페이스입니다.

1. 키를 눌러 **F5** 솔루션을 실행 합니다.
2. 새 사용자 계정을 등록 합니다. 이 위해 연습 1, 작업 3에서에서 설명한 등록 단계를 수행 합니다.

    > [!NOTE]
    > 이전 연습에서 솔루션을 사용 하는 경우에 이전에 만든 사용자 계정으로 로그인 기록할 수 있습니다.
3. 합니다 **홈** 퀴즈의 첫 번째 질문을 보여 주는 페이지가 표시 됩니다. 옵션 중 하나를 클릭 하 여 질문에 대답 합니다. 이 트리거됩니다 합니다 **sendAnswer** 선택된 옵션은 전송 하는 앞에서 정의한 함수를 **퀴즈** Web API입니다.

    ![정보를 파악 하기가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "질문에 대답")

    *질문에 대답*
4. 단추 중 하나를 클릭 한 후 답변 표시 됩니다. 클릭 **다음 질문** 다음 질문을 표시 합니다. 이렇게 하면 트리거됩니다 합니다 **nextQuestion** 컨트롤러에 정의 된 함수입니다.

    ![다음 질문을 요청](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "다음 질문을 요청 합니다.")

    *다음 질문을 요청합니다.*
5. 다음 질문에 나타납니다. 원하는 횟수 만큼 질문에 응답을 계속 합니다. 모든 질문을 완료 한 후 첫 번째 질문을 반환 해야 합니다.

    ![다른 질문](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "또 다른 문제")

    *다음 질문*
6. Visual Studio 및 키를 눌러도 돌아가 **shift+f5** 디버깅을 중지 합니다.

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a>작업 3-만드는 Css3 애니메이션을 대칭 이동

이 작업에서 질문에 답변 하는 경우 및 다음 질문을 검색할 때 플립 효과 추가 하 여 다양 한 애니메이션을 수행 하려면 CSS3 속성을 사용 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **콘텐츠** 폴더를 **GeekQuiz** 프로젝트를 마우스 **추가 | 기존 항목...** .

    ![콘텐츠 폴더에 기존 항목 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "콘텐츠 폴더에 기존 항목 추가")

    *콘텐츠 폴더에 기존 항목 추가*
2. 에 **기존 항목 추가** 대화 상자에서 **원본/자산** 폴더를 선택 **Flip.css**합니다. **추가**를 클릭합니다.

    ![자산에서 Flip.css 파일 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "자산에서 Flip.css 파일 추가")

    *자산에서 Flip.css 파일 추가*
3. 엽니다는 **Flip.css** 방금 추가한 파일 및 해당 내용을 검사 합니다.
4. 찾을 합니다 **변환 대칭** 주석입니다. CSS를 사용 하 여 해당 주석에 아래의 스타일 **관점** 및 **rotateY** 생성 하는 변환을 &quot;대칭 이동 후 카드&quot; 적용 합니다.

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. 찾을 합니다 **대칭 이동 시의 창 숨기기** 주석입니다. 설정 하 여 뷰어에서 떨어져 직면 하는 경우 해당 주석에 아래 스타일 중 백 쪽을 숨깁니다 합니다 **뒷면 가시성** CSS 속성을 *숨겨진*합니다.

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. 열기는 **BundleConfig.cs** 파일을 **앱\_시작** 폴더에 대 한 참조를 추가 하 고는 **Flip.css** 파일는 **&quot;~/Content/css&quot;** 스타일 번들

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. 키를 눌러 **F5** 솔루션 및 자격 증명으로 로그인을 실행 합니다.
8. 옵션 중 하나를 클릭 하 여 질문에 대답 합니다. 뷰 간에 전환할 때 플립 효과 확인 합니다.

    ![전환 효과 사용 하 여 질문에 답하려면](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "플립 효과 사용 하 여 질문에 대답")

    *전환 효과 사용 하 여 질문에 대답*
9. 클릭 **의문이** 다음 질문을 검색 하려면. 전환 효과 다시 표시 됩니다.

    ![전환 효과 사용 하 여 다음 질문을 검색](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "플립 효과 사용 하 여 다음 질문을 검색 합니다.")

    *전환 효과 사용 하 여 다음 질문을 검색합니다.*

* * *

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습을 완료 하 여 배웠습니다 방법:

- ASP.NET 스 캐 폴딩을 사용 하는 ASP.NET Web API 컨트롤러 만들기
- 다음 퀴즈 질문을 검색 하는 웹 API 가져오기 작업을 구현 합니다.
- 구현에 퀴즈의 답을 저장 하는 Web API 게시 작업
- Visual Studio 패키지 관리자 콘솔에서 AngularJS를 설치 합니다.
- AngularJS 템플릿 구현 및 컨트롤러
- 사용 하 여 CSS3 전환 애니메이션 효과 수행 합니다.
