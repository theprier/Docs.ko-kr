---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: '실습 랩: 빌드 ASP.NET Web API 및 Angular.js 단일 페이지 응용 프로그램 (SPA) | Microsoft Docs'
author: rick-anderson
description: 기존 웹 응용 프로그램에서 클라이언트 (브라우저) 페이지를 요청 하 여 서버와의 통신을 시작 합니다. 서버는 다음 요청을 처리 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/30/2015
ms.topic: article
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 9a748628d53878be380869ac5327de0111d2284d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a>ASP.NET Web API 및 Angular.js 단일 페이지 응용 프로그램 (SPA)을 작성 하는 실습 랩:
====================
으로 [웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트를 다운로드 합니다.](http://aka.ms/webcamps-training-kit)

> 기존 웹 응용 프로그램에서 클라이언트 (브라우저) 페이지를 요청 하 여 서버와의 통신을 시작 합니다. 그런 다음 서버는 요청을 처리 하 고 페이지의 HTML 클라이언트에 보냅니다. -예: 사용자 링크를 탐색 하거나 데이터를 사용 하 여 폼을 제출 – 페이지와 후속 상호 작용에서 새 요청을 서버에 전송 되 고는 흐름이 다시 시작: 서버가 요청을 처리 하 고 새 작업 요청에 대 한 응답으로 브라우저에 새 페이지 보냅니다 클라이언트에서 ed 합니다.
> 
> 단일 페이지 응용 프로그램 (SPAs)에서 전체 페이지 로드 브라우저에서 초기 요청 후 되었지만 후속 상호 작용 Ajax 요청을 통해 수행 합니다. 즉, 변경 된 페이지의 부분만 업데이트 하는 브라우저에 전체 페이지를 다시 로드 하지 않아도가 됩니다. SPA 접근 방식을 시켜 더 강조 경험 하는 사용자 동작에 응답 하도록 응용 프로그램에서 사용한 시간을 줄입니다.
> 
> SPA의 아키텍처는 기존 웹 응용 프로그램에 존재 하지 않는 특정 한 문제가 포함 됩니다. 그러나 CSS3에서 제공 하는 새 스타일 지정 기능 정말 쉽게 수 있도록 설계 및 구축 SPAs 및 ASP.NET Web API와 같은 기술을 발생 하 고, JavaScript 프레임 워크 같은 AngularJS 합니다.
> 
> 이 실습 랩에서 들은 퀴즈를 SPA 개념에 따라 trivia 웹 사이트를 구현 하는 이러한 기술 활용을 걸립니다. 먼저 ASP.NET 웹 api 퀴즈 질문을 검색 하 고 답을 저장할 필요한 끝점을 노출할 서비스 계층을 구현 합니다. 그런 다음, AngularJS 및 CSS3 변환 효과 사용 하 여 풍부 하 고 응답성이 뛰어난 UI를 만들 수 있습니다.
> 
> 모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit)합니다.


## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 배웁니다 하는 방법:

- JSON 데이터를 받거나 보내기 위해 ASP.NET 웹 API 서비스 만들기
- AngularJS를 사용 하 여 응답성이 뛰어난 UI 만들기
- CSS3 변형이 있는 기능의 UI 환경 향상

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>필수 구성 요소

다음은이 실습 랩을 완료 하려면 필요 합니다.

- [Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상

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

1. [Web API 만들기](#Exercise1)
2. [SPA 인터페이스 만들기](#Exercise2)

예상 소요 시간: **60 분**

> [!NOTE]
> Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션 특정 개발 스타일에 맞게 설계 하 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 랩의 절차를 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업 설명에서 **일반 개발 설정** 컬렉션입니다. 개발 환경에 대 한 서로 다른 설정 컬렉션을 선택 하면 고려해 야 하는 단계에 차이가 있을 수 있습니다.


<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a>연습 1: Web API 만들기

SPA의 주요 부분 중 하나는 서비스 계층입니다. UI 및 해당 호출에 대 한 응답에서 반환 데이터에서 보낸 Ajax 호출을 처리 담당 합니다. 검색 된 데이터를 구문 분석 하 고 클라이언트에서 사용 하기 위해 컴퓨터가 읽을 수 있는 형식으로 표시 되어야 합니다.

Web API 프레임 워크는 ASP.NET 스택에서의 일부 이며은 쉽게 일반적으로 데이터 보내기 및 받기 JSON 또는 XML 형식 RESTful API를 통해 HTTP 서비스를 구현할 수 있도록 설계 되었습니다. 이 연습에서는 들은 퀴즈 응용 프로그램을 호스트 하 고 백 엔드 서비스를 노출 하 고 ASP.NET Web API를 사용 하 여 퀴즈 데이터 유지를 구현 하려면 웹 사이트에 만들어집니다.

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a>작업 1-들은 퀴즈에 대 한 초기 프로젝트 만들기

이 작업에서는 먼저에 기반으로 하는 ASP.NET Web API를 지 원하는 새 ASP.NET MVC 프로젝트를 만드는 **One ASP.NET** 프로젝트 Visual Studio와 함께 제공 되는 형식입니다. **One ASP.NET** 모든 ASP.NET 기술을 통합 하 고는 혼합 하 고 원하는 대로 얻었으면이 옵션을 제공 합니다. Entity Framework 모델 클래스와 데이터베이스 initializator 퀴즈 질문을 삽입 하려면 다음 추가 합니다.

1. 열기 **Visual Studio Express 2013 for Web** 선택 **파일 | 새 프로젝트...**  새 솔루션을 시작 합니다.

    ![새 프로젝트를 만드는](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "새 프로젝트 만들기")

    *새 프로젝트 만들기*
2. 에 **새 프로젝트** 대화 상자에서 **ASP.NET 웹 응용 프로그램** 아래는 **Visual C# | 웹** 탭 합니다. 있는지 확인 **.NET Framework 4.5** 은 이름을 선택 하면 *GeekQuiz*, 선택는 **위치** 클릭 **확인**합니다.

    ![새 ASP.NET 웹 응용 프로그램 프로젝트를 만드는](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "새 ASP.NET 웹 응용 프로그램 프로젝트 만들기")

    *새 ASP.NET 웹 응용 프로그램 프로젝트 만들기*
3. 에 **새 ASP.NET 프로젝트** 대화 상자는 **MVC** 템플릿과 선택은 **웹 API** 옵션입니다. 또한 있는지 확인 하 고 **인증** 옵션을 설정 **개별 사용자 계정**합니다. 계속하려면 **확인** 을 클릭합니다.

    ![Web API 구성 요소를 포함 하 여 MVC 템플릿을 사용 하 여 새 프로젝트 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    *Web API 구성 요소를 포함 하 여 MVC 템플릿을 사용 하 여 새 프로젝트 만들기*
4. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **모델** 의 폴더는 **GeekQuiz** 프로젝트를 마우스 선택 **추가 | 기존 항목...** .

    ![기존 항목 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "기존 항목 추가")

    *기존 항목 추가*
5. 에 **기존 항목 추가** 대화 상자에서 이동 하는 **소스/자산/모델** 폴더와 파일을 모두 선택 합니다. **추가**를 클릭합니다.

    ![모델 자산 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "모델 자산 추가")

    *모델 자산 추가*

    > [!NOTE]
    > 이러한 파일을 추가 하 여 데이터 모델, 엔터티 프레임 워크의 데이터베이스 컨텍스트 및 들은 퀴즈 응용 프로그램에 대 한 데이터베이스 이니셜라이저도 추가 됩니다.
    > 
    > **Entity Framework (EF)** 관계형 저장소 스키마를 사용 하 여 직접 프로그래밍 하는 대신 개념적 응용 프로그램 모델을 사용 하 여 프로그래밍 하 여 데이터 액세스 응용 프로그램을 만들 수 있도록 하는 개체 관계형 매퍼 (ORM). Entity Framework에 대 한 자세히 알아볼 수 있습니다 [여기](../../../entity-framework.md)합니다.
    > 
    > 다음은 방금 추가한 클래스에 대 한 설명을입니다.
    > 
    > - **TriviaOption:** 퀴즈 질문에 연결 된 단일 옵션을 나타냅니다
    > - **TriviaQuestion:** 퀴즈 질문을 나타내며 연결된 옵션을 통해 노출 된 **옵션** 속성
    > - **TriviaAnswer:** 퀴즈 질문에 대 한 응답으로 사용자가 선택한 옵션을 나타냅니다
    > - **TriviaContext:** 들은 퀴즈 응용 프로그램의 Entity Framework 데이터베이스 컨텍스트를 나타냅니다. 이 클래스에서 파생 **DContext** 노출 **DbSet** 위에서 설명한 엔터티 컬렉션을 나타내는 속성입니다.
    > - **TriviaDatabaseInitializer:** 구현에 대 한 Entity Framework 이니셜라이저의 여 **TriviaContext** 클래스에서 상속 하는 **CreateDatabaseIfNotExists**합니다. 에 지정 된 엔터티를 삽입 합니다.이 클래스의 기본 동작은 존재 하지 않는 경우에 데이터베이스를 만드는 것은 **시드** 메서드.
6. 열기는 **Global.asax.cs** 파일을 다음 추가 문을 사용 하 여 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. 맨 앞에 다음 코드를 추가 **응용 프로그램\_시작** 설정 하는 메서드는 **TriviaDatabaseInitializer** 데이터베이스 이니셜라이저로 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. 수정 된 **홈** 인증 된 사용자에 대 한 액세스를 제한 하는 컨트롤러입니다. 이 위해 엽니다는 **HomeController.cs** 내 파일의 **컨트롤러** 폴더 추가 **Authorize** 특성을 **HomeController**클래스 정의 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > **Authorize** 를 사용자가 인증 하는 경우 확인을 필터링 합니다. 사용자 인증 되지 않은 경우 다음 작업을 호출 하지 않고 HTTP 상태 코드 401 (권한 없음)를 반환 합니다. 컨트롤러 수준에서 전역적으로 또는 개별 작업 수준에서 필터를 적용할 수 있습니다.
9. 이제 브랜딩 하 고 웹 페이지의 레이아웃을 사용자 지정할는 있습니다. 이 작업을 수행 하려면 엽니다는  **\_Layout.cshtml** 내 파일의 **보기 | 공유** 폴더의 내용을 업데이트 하 고는 **&lt;제목&gt;** 대체 하 여 요소 *내 ASP.NET 응용 프로그램* 와 *들은 퀴즈* .

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. 같은 파일에서 제거 하 여 탐색 모음을 업데이트는 *에 대 한* 및 *연락처* 링크 및 이름 바꾸기는 *홈* 연결할 *재생*합니다. 이름도 변경는 *응용 프로그램 이름* 연결할 *들은 퀴즈*합니다. HTML 탐색 모음에 다음 코드와 같습니다.

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. 레이아웃 페이지의 바닥글을 대체 하 여 업데이트 *내 ASP.NET 응용 프로그램* 와 *들은 퀴즈*합니다. 이 위해의 내용을 대체는 **&lt;바닥글&gt;** 요소 강조 표시 된 다음 코드를 사용 합니다.

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a>작업 2-TriviaController 웹 API 만들기

이전 태스크에서 웹 응용 프로그램 들은 퀴즈의 초기 구조를 만들었습니다. 이제 퀴즈 데이터 모델과 상호 작용 하 고 다음 작업을 노출 하는 간단한 웹 API 서비스를 작성 합니다.

- **GET/api/trivia**: 인증 된 사용자가 대답 해야 할 퀴즈 목록에서 다음 질문을 검색 합니다.
- **POST/api/trivia**: 인증 된 사용자가 지정한 퀴즈 답변을 저장 합니다.

Web API 컨트롤러 클래스에 대 한 기준을 만드는 데 Visual Studio에서 제공 하는 ASP.NET 스 캐 폴딩 도구를 사용 합니다.

1. 열기는 **WebApiConfig.cs** 내 파일의 **앱\_시작** 폴더입니다. 이 파일에는 경로 Web API 컨트롤러 작업에 매핑하는 방식을 같은 웹 API 서비스의 구성을 정의 합니다.
2. 다음 추가 문을 사용 하 여 파일의 시작 부분에 있습니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. 다음 강조 표시 된 코드를 추가 하는 **등록** 웹 API 작업 메서드에 의해 검색 되는 JSON 데이터에 대 한 포맷터를 전역적으로 구성 하는 메서드.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > **CamelCasePropertyNamesContractResolver** 속성 이름을 자동으로 변환 *카멜식* 경우 JavaScript에서 속성 이름에 대 한 일반 규칙입니다.
4. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **컨트롤러** 의 폴더는 **GeekQuiz** 프로젝트를 마우스 선택 **추가 | 새 스 캐 폴드 항목...** .

    ![새 스 캐 폴드 항목을 만드는](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "스 캐 폴드 새 항목 만들기")

    *새 스 캐 폴드 항목 만들기*
5. 에 **스 캐 폴드를 추가** 대화 상자에서 다음 사항을 확인는 **일반적인** 왼쪽된 창에서 노드를 선택 합니다. 그런 다음 선택에서 **Web API 2 컨트롤러-비어 있지** 클릭 확인 하 고 가운데 창에서 템플릿을 **추가**합니다.

    ![Web API 2 컨트롤러 빈 템플릿을 선택 하면](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Web API 2 컨트롤러 빈 템플릿 선택")

    *Web API 2 컨트롤러 빈 템플릿 선택*

    > [!NOTE]
    > **ASP.NET 스 캐 폴딩** 는 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크입니다. Visual Studio 2013 MVC 및 Web API 프로젝트에 대 한 사전 설치 된 코드 생성기를 포함합니다. 신속 하 게 표준 데이터 작업을 개발 하는 데 필요한 시간을 줄이기 위해 데이터 모델과 상호 작용 하는 코드를 추가 하려면 프로젝트에 스 캐 폴딩을 사용 해야 합니다.
    > 
    > 스 캐 폴딩 프로세스는 또한 모든 필요한 종속 프로젝트에 설치 되어 있는지 확인 합니다. 예를 들어 빈 ASP.NET 프로젝트 시작 다음 스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 추가 하는 경우 필요한 웹 API NuGet 패키지와 참조를 프로젝트에 자동으로 추가 됩니다.
6. 에 **컨트롤러 추가** 대화 상자에서 *TriviaController* 에 **컨트롤러 이름** 텍스트 상자 **추가**합니다.

    ![Trivia 컨트롤러 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "Trivia 컨트롤러 추가")

    *Trivia 컨트롤러 추가*
7. **TriviaController.cs** 파일에 추가 됩니다는 **컨트롤러** 의 폴더는 **GeekQuiz** 비어 있는 포함 된 프로젝트 **TriviaController** 클래스입니다. 다음 추가 문을 사용 하 여 파일의 시작 부분에 있습니다.

    (코드 조각- *AspNetWebApiSpa e x-1-TriviaControllerUsings*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. 맨 앞에 다음 코드를 추가 **TriviaController** 정의 초기화 및 삭제 하는 클래스는 **TriviaContext** 컨트롤러의 인스턴스.

    (코드 조각- *AspNetWebApiSpa e x-1-TriviaControllerContext*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > **Dispose** 방식의 **TriviaController** 호출는 **Dispose** 의 메서드는 **TriviaContext** 인스턴스를 사용 하면 모든 컨텍스트 개체에서 사용 하는 리소스가 해제 때는 **TriviaContext** 인스턴스를 삭제 하거나 가비지 수집 합니다. Entity Framework에서 연 모든 데이터베이스 연결을 닫는 포함 됩니다.
9. 끝에 다음 도우미 메서드를 추가 합니다.는 **TriviaController** 클래스입니다. 이 메서드는 지정된 된 사용자가 대답 해야 할 데이터베이스에서 다음 질문의 퀴즈를 검색 합니다.

    (코드 조각- *AspNetWebApiSpa e x-1-TriviaControllerNextQuestion*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. 다음 추가 **가져오기** 동작 메서드의 **TriviaController** 클래스입니다. 이 작업 메서드를 호출는 **NextQuestionAsync** 인증된 된 사용자에 대 한 다음 질문을 검색 하는 이전 단계에 정의 된 도우미 메서드입니다.

    (코드 조각- *AspNetWebApiSpa e x-1-TriviaControllerGetAction*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. 끝에 다음 도우미 메서드를 추가 합니다.는 **TriviaController** 클래스입니다. 이 메서드는 데이터베이스에 지정한 응답을 저장 하 고 답이 맞으면 여부를 나타내는 부울 값을 반환 합니다.

    (코드 조각- *AspNetWebApiSpa e x-1-TriviaControllerStoreAsync*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. 다음 추가 **Post** 동작 메서드의 **TriviaController** 클래스입니다. 이 동작 메서드에 연결 인증 된 사용자 및 호출에 대 한 대답은 **StoreAsync** 도우미 메서드입니다. 그런 다음 도우미 메서드에 의해 반환 된 부울 값으로 응답을 보냅니다.

    (코드 조각- *AspNetWebApiSpa e x-1-TriviaControllerPostAction*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. 수정 Web API 컨트롤러를 추가 하 여 인증 된 사용자 에게만 액세스를 제한 하는 **Authorize** 특성을 **TriviaController** 클래스 정의 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>작업 3 – 솔루션 실행

이 작업에서는 이전 태스크에서 작성 된 웹 API 서비스가 예상 대로 작동 하는지 확인 합니다. Internet Explorer를 사용 합니다 **F12 개발자 도구** 네트워크 트래픽을 캡처하고 웹 API 서비스의 전체 응답을 검사 합니다.

> [!NOTE]
> 다음 사항을 확인 **Internet Explorer** 에서 선택한는 **시작** 단추 Visual Studio 도구 모음에 있는 합니다.
> 
> ![Internet Explorer 옵션](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)


1. 키를 눌러 **F5** 솔루션을 실행 합니다. **로그인** 페이지가 브라우저에 표시 됩니다.

    > [!NOTE]
    > 응용 프로그램이 시작 되 면 기본 MVC 경로 트리거된에 매핑되는 기본적으로는 **인덱스** 의 동작에서 **HomeController** 클래스입니다. 이후 **HomeController** 인증 된 사용자 에게만 부여 됩니다 (해당 클래스와 데코 레이트 된 기억는 **Authorize** 연습 1의 특성) 되어 있으므로 사용자가 인증 아직 응용 프로그램 로그인 페이지에 원래 요청을 리디렉션합니다.

    ![솔루션을 실행](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "솔루션 실행")

    *솔루션을 실행*
2. 클릭 **등록** 새 사용자를 만듭니다.

    ![새 사용자 등록](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "새 사용자를 등록 하는 중")

    *새 사용자를 등록 하는 중*
3. 에 **등록** 페이지에서 입력 한 **사용자 이름** 및 **암호**, 클릭 하 고 **등록**합니다.

    ![등록 페이지](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "등록 페이지")

    *등록 페이지*
4. 응용 프로그램에서 새 계정을 등록 하 고 사용자가 인증 되 고 홈 페이지로 다시 리디렉션되 며 합니다.

    ![사용자가 인증](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "인증 된 사용자")

    *사용자가 인증*
5. 키를 눌러 브라우저에서 **F12** 열려는 **개발자 도구** 패널입니다. 키를 누릅니다 **CTRL + 4** 하거나 클릭 하 고 **네트워크** 네트워크 트래픽 캡처를 시작 하 고 녹색 화살표 단추 아이콘을 클릭 합니다.

    ![웹 API 네트워크 캡처를 시작](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Web API 시작 네트워크 캡처")

    *웹 API 네트워크 캡처를 시작합니다.*
6. 추가 **api/trivia** 브라우저의 주소 표시줄에 URL을 합니다. 응답의 세부 정보를 이제 검사 하는 **가져오기** 의 동작 메서드에 **TriviaController**합니다.

    ![웹 API를 통해 다음 질문 데이터 검색](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "웹 API를 통해 다음 질문 데이터 검색")

    *웹 API를 통해 다음 질문 데이터 검색*

    > [!NOTE]
    > 다운로드를 완료 한 후에 다운로드 한 파일 작업으로 설정할 하 라는 메시지가 표시 됩니다. 대화 상자를 개발자 도구 창을 통해 응답 콘텐츠를 볼 수 있도록 열어 둡니다.
7. 이제는 응답의 본문을 조사 합니다. 이 작업을 수행 하려면는 **세부 정보** 탭을 클릭 한 다음 **응답 본문**합니다. 다운로드 한 데이터 속성을 가진 개체를 확인할 수 있습니다 **옵션** (의 목록인 **TriviaOption** 개체), **id** 및 **제목** 에 해당 하는 **TriviaQuestion** 클래스입니다.

    ![웹 API 응답 본문을 보기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "웹 API 응답 본문을 보기")

    *보기 웹 API 응답 본문*
8. Visual Studio 및 키를 눌러로 돌아가서 **SHIFT + f 5를 눌러** 디버깅을 중지 합니다.

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a>연습 2: SPA 인터페이스 만들기

이 연습에서는 먼저 빌드합니다 웹 프런트 엔드 부분 들은 퀴즈를 사용 하 여 단일 페이지 응용 프로그램 상호 작용에 중점을 두기 **AngularJS**합니다. 다음 컨텍스트 전환 질문 중 하나에서 다음 전환할 때의 시각적 효과 고 풍부한 애니메이션을 수행 하기 위한 CSS3 만들어 사용자 환경을 향상 됩니다.

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a>작업 1 – AngularJS를 사용 하 여 SPA 인터페이스 만들기

이 작업을 사용 하 여 **AngularJS** 들은 퀴즈 응용 프로그램의 클라이언트 쪽을 구현 하 합니다. **AngularJS** 브라우저 기반 응용 프로그램을 보완 하는 오픈 소스 JavaScript 프레임 워크는 *모델-뷰-컨트롤러* (MVC) 기능을 모두 개발을 촉진 하 고 테스트 합니다.

Visual Studio의 패키지 관리자 콘솔에서 AngularJS를 설치 하 여 시작 합니다. 그런 다음 들은 퀴즈 응용 프로그램 및 퀴즈 질문 및 답변은 AngularJS 템플릿 엔진을 사용 하 여 렌더링 하는 보기의 동작을 제공 하도록 컨트롤러를 만듭니다.

> [!NOTE]
> AngularJS에 대 한 자세한 내용은를 참조 [ [http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/)합니다.


1. 열고 **Visual Studio Express 2013 for Web** 엽니다는 **GeekQuiz.sln** 솔루션에 있는 **소스/e x 2-CreatingASPAInterface/시작** 폴더입니다. 또는 계속할 수 있습니다 솔루션으로, 이전 연습에서 가져올 있음을.
2. 열기는 **패키지 관리자 콘솔** 에서 **도구** | **라이브러리 패키지 관리자**합니다. 설치 하려면 다음 명령을 입력 하 고 **AngularJS.Core** NuGet 패키지 합니다.

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **스크립트** 의 폴더는 **GeekQuiz** 프로젝트를 마우스 선택 **추가 | 새 폴더**합니다. 폴더 이름을 **앱** 누릅니다 **Enter**합니다.
4. 마우스 오른쪽 단추로 클릭는 **앱** 폴더 바로 전에 만들고 선택 **추가 | JavaScript 파일**합니다.

    ![새 JavaScript 파일 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    *새 JavaScript 파일 만들기*
5. 에 **항목에 대 한 이름 지정** 대화 상자에서 *퀴즈 컨트롤러* 에 **항목 이름** 텍스트 상자 **확인**합니다.

    ![새 JavaScript 파일 이름 지정](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    *새 JavaScript 파일 이름 지정*
6. 에 **퀴즈 controller.js** 파일에서 다음 코드를 선언 하 고 초기화 AngularJS 추가 **QuizCtrl** 컨트롤러입니다.

    (코드 조각- *AspNetWebApiSpa-e x 2-AngularQuizController*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > 생성자 함수는 **QuizCtrl** 컨트롤러에서는 라는 injectable 매개 변수는 **$scope**합니다. 범위의 초기 상태를 설정 해야 생성자 함수에서 속성을 연결 하 여는 **$scope** 개체입니다. 속성 포함 되는 **뷰 모델**, 하는 컨트롤러를 등록 하는 경우 서식 파일에 액세스할 수 있습니다.
    > 
    > **QuizCtrl** 컨트롤러가 라는 모듈 내에 정의 되어 **QuizApp**합니다. 모듈은 수 있는 작업 단위를 개별 구성 요소로 분해 합니다. 응용 프로그램입니다. 모듈을 사용 하는 주요 이점은 코드 이해 하기 쉬우며 이며 단위 테스트, 재사용 및 유지 관리를 용이 하 게 것입니다.
7. 이제 보기에서 트리거되는 이벤트에 대응 하기 위해 범위에 동작을 추가 합니다. 끝에 다음 코드를 추가 **QuizCtrl** 정의 하는 컨트롤러는 **nextQuestion** 함수는 **$scope** 개체입니다.

    (코드 조각- *AspNetWebApiSpa-e x 2-AngularQuizControllerNextQuestion*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > 이 함수에서 다음 질문을 검색 합니다.는 **퀴즈** Web API 이전 연습에서 만든 및 질문 데이터를 연결 된 **$scope** 개체입니다.
8. 끝에 다음 코드를 삽입는 **QuizCtrl** 정의 하는 컨트롤러는 **sendAnswer** 함수는 **$scope** 개체입니다.

    (코드 조각- *AspNetWebApiSpa-e x 2-AngularQuizControllerSendAnswer*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > 이 함수를 사용자가 선택한 응답을 보냅니다는 **퀴즈** Web API에서-즉, 대답 한 경우 올바른 여부-결과 저장 하는 **$scope** 개체입니다.
    > 
    > **nextQuestion** 및 **sendAnswer** 위에서 함수는 AngularJS를 사용 하 여 **$http** 는 XMLHttpRequest 통해 웹 API와의 통신을 추상화 하는 개체 브라우저에서 JavaScript 개체입니다. AngularJS 더 높은 수준의 RESTful Api를 통해 리소스에 대해 CRUD 작업을 수행 하는 추상화를 제공 하는 다른 서비스를 지원 합니다. AngularJS **$resource** 개체의 상호 작용 하지 않고도 높은 수준의 동작을 제공 하는 작업 메서드는 **$http** 개체입니다. 사용 하는 것이 좋습니다는 **$resource** CRUD 모델을 필요로 하는 시나리오에서 개체 (전경 정보 참조는 [$resource 설명서](https://docs.angularjs.org/api/ngResource/service/$resource)).
9. 다음 단계에서는 퀴즈에 대 한 뷰를 정의 하는 AngularJS 템플릿입니다를 만드는 것입니다. 이 작업을 수행 하려면 엽니다는 **Index.cshtml** 내 파일의 **보기 | 홈** 폴더 및 콘텐츠를 다음 코드로 바꿉니다.

    (코드 조각- *AspNetWebApiSpa-e x 2-GeekQuizView*)

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > AngularJS 템플릿은 static 태그 브라우저에 표시 되는 동적 뷰를 변환할 모델과 컨트롤러의 정보를 사용 하는 선언적 지정입니다. 다음은 AngularJS 요소 고 서식 파일에 사용할 수 있는 특성의 예입니다.
    > 
    > - **ng 앱** 지시문 AngularJS 응용 프로그램의 루트 요소를 나타내는 DOM 요소를 나타냅니다.
    > - **ng 컨트롤러** 지시문의 지시문이 선언 된 지점에서 DOM에는 컨트롤러를 연결 합니다.
    > - 중괄호 표기법 **{{}}** 컨트롤러에 정의 된 범위 속성에 대 한 바인딩을 나타냅니다.
    > - **ng 클릭** 지시문을 사용 하 여을 사용자가 클릭에 대 한 응답에는 범위에 정의 된 함수를 호출 합니다.
10. 열기는 **Site.css** 내 파일의 **콘텐츠** 폴더 고 퀴즈 보기에 대 한 모양 및 느낌을 제공 하는 파일의 끝에 다음 강조 표시 된 스타일을 추가 합니다.

    (코드 조각- *AspNetWebApiSpa-e x 2-GeekQuizStyles*)

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a>작업 2-솔루션 실행

이 태스크를 실행 합니다 새 사용자를 사용 하 여 솔루션 인터페이스인 일부의 퀴즈 질문에 답변 하는 AngularJS를 사용 하 여 작성 합니다.

1. 키를 눌러 **F5** 솔루션을 실행 합니다.
2. 새 사용자 계정을 등록 합니다. 이 작업을 수행 하려면 연습 1, 작업 3에에서 설명 된 등록 단계를 수행 합니다.

    > [!NOTE]
    > 이전 연습에서 솔루션을 사용 하는 경우에 이전에 만든 사용자 계정으로 기록할 수 있습니다.
3. **홈** 퀴즈의 첫 번째 질문을 보여 주는 페이지가 표시 됩니다. 옵션 중 하나를 클릭 하 여 응답 합니다. 이 트리거하는 **sendAnswer** 선택 된 옵션을 전송 하는 이전에 정의 된 함수는 **퀴즈** 웹 API입니다.

    ![질문에 대답](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "질문에 대답")

    *질문에 대답*
4. 단추 중 하나를 클릭 한 후에 대답 나타나야 합니다. 클릭 **다음 질문** 다음과 같은 질문을 표시 합니다. 이 트리거하는 **nextQuestion** 컨트롤러에 정의 된 함수입니다.

    ![다음 질문을 요청](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "다음 질문을 요청 합니다.")

    *다음 질문을 요청합니다.*
5. 다음 질문 표시 되어야 합니다. 원하는 횟수 만큼 질문에 응답을 계속 합니다. 모든 질문을 완료 한 후 첫 번째 질문을 반환 해야 합니다.

    ![다른 질문](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "다른 질문")

    *다음 질문*
6. Visual Studio 및 키를 눌러로 돌아가서 **SHIFT + f 5를 눌러** 디버깅을 중지 합니다.

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a>작업 3 – CSS3를 사용 하 여 플립 애니메이션 만들기

이 작업에서 애니메이션을 수행 하 다양 한 질문에 대답할 및 다음 질문을 검색할 때 플립 효과 추가 하 여 CSS3 속성을 사용 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **콘텐츠** 의 폴더는 **GeekQuiz** 프로젝트를 마우스 선택 **추가 | 기존 항목...** .

    ![콘텐츠 폴더에 기존 항목 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "콘텐츠 폴더에 기존 항목 추가")

    *콘텐츠 폴더에 기존 항목 추가*
2. 에 **기존 항목 추가** 대화 상자에서 이동 하는 **소스/자산의** 폴더를 선택 **Flip.css**합니다. **추가**를 클릭합니다.

    ![자산 중에서 Flip.css 파일을 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "자산 중에서 Flip.css 파일을 추가 합니다.")

    *자산 중에서 Flip.css 파일을 추가합니다.*
3. 열기는 **Flip.css** 방금 추가한 파일 및 해당 내용을 검사 합니다.
4. 찾을 **변환 대칭** 메모 합니다. CSS를 사용 하 여 해당 의견 아래의 스타일 **관점** 및 **rotateY** 변환을 생성 하는 &quot;대칭 이동 카드&quot; 효과입니다.

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. 찾을 **대칭 이동 하는 동안 창 뒷면 숨깁니다** 메모 합니다. 설정 하 여 뷰어에서 직면 하는 경우 해당 의견 아래의 스타일 숨깁니다 얼굴 백 측은 **뒷면 가시성** CSS 속성을 *숨겨진*합니다.

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. 열기는 **BundleConfig.cs** 내 파일의 **앱\_시작** 폴더에 대 한 참조를 추가 하 고는 **Flip.css** 파일에 **&quot;~/Content/css&quot;** 스타일 번들

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. 키를 눌러 **F5** 솔루션 및 자격 증명을 사용 하 여 로그를 실행 합니다.
8. 옵션 중 하나를 클릭 하 여 질문에 대답 합니다. 뷰 간에 전환할 때 플립 효과 확인 합니다.

    ![플립 영향을 주지 않고 질문에 대답](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "플립 효과 함께 질문에 대답")

    *플립 효과 함께 질문에 대답*
9. 클릭 **다음 질문** 를 다음과 같은 질문을 검색 합니다. 플립 효과 다시 표시 됩니다.

    ![플립 효과 함께 다음 질문의 검색](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "플립 효과 함께 다음 질문을 검색 합니다.")

    *플립 효과 함께 다음과 같은 질문을 검색합니다.*

* * *

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩을 완료 하 여 배웠습니다 하는 방법:

- ASP.NET 스 캐 폴딩을 사용 하 여 ASP.NET Web API 컨트롤러 만들기
- 다음 퀴즈 질문을 검색 하는 웹 API 가져오기 작업을 구현 합니다.
- 답을 저장 하는 웹 API Post 작업 구현
- Visual Studio 패키지 관리자 콘솔에서 AngularJS 설치
- AngularJS 템플릿 구현 및 컨트롤러
- 사용 하 여 CSS3 애니메이션 효과 수행 하려면 전환
