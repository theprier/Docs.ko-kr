---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 사용자 지정 작업 필터 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC는 작업 메서드가 호출 되기 전후 필터링 논리를 실행 하기 위한 작업 필터를 제공 합니다. 작업 필터는 사용자 지정 특성 tha...
ms.author: aspnetcontent
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: c435fef624d526ceb01dbc370c5df52e2a1e8350
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37807937"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a>ASP.NET MVC 4 사용자 지정 작업 필터

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트 다운로드](https://aka.ms/webcamps-training-kit)

ASP.NET MVC는 작업 메서드가 호출 되기 전후 필터링 논리를 실행 하기 위한 작업 필터를 제공 합니다. 작업 필터는 컨트롤러의 작업 메서드에 사전 작업 및 작업 이후의 동작을 추가 하는 선언적 방법을 제공 하는 사용자 지정 특성입니다.

이 실습 랩에서 MvcMusicStore 컨트롤러의 요청을 catch 하 고 솔루션을 데이터베이스 테이블에는 사이트의 활동 로그에 사용자 지정 작업 필터 특성을 만듭니다. 모든 컨트롤러 또는 동작을 주입 하 여 로깅 필터를 추가 하려면 됩니다. 마지막으로, 방문자 목록을 보여 주는 로그 보기를 표시 됩니다.

이 실습 랩 기본 지식이 있다고 가정 **ASP.NET MVC**합니다. 사용 하지 않은 경우 **ASP.NET MVC** 이전 좋습니다 이동해 **ASP.NET MVC 4 기본 사항** 실습 합니다.

> [!NOTE]
> 웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다. 이 랩에 특정 프로젝트에서 제공 됩니다 [ASP.NET MVC 4 사용자 지정 작업 필터](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)합니다.

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 학습할 방법:

- 필터링 기능을 확장 하는 사용자 지정 작업 필터 특성 만들기
- 특정 수준에 주입 하 여 사용자 지정 필터 특성 적용
- 사용자 지정 작업 필터를 전역으로 등록

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽을 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>설정

**설치 코드 조각**

편의 위해이 랩에서 함께 관리 하려는 코드의 대부분 제품은 Visual Studio 코드 조각입니다. 설치를 실행 하는 코드 조각 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.

이 문서의 부록 참조할 수 있습니다 사용 하는 방법을 알아보려면 원하는 고 Visual Studio 코드 조각을 사용 하 여 잘 모르는 경우 &quot; [부록 c:를 사용 하 여 코드 조각](#AppendixC)&quot;합니다.

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습으로 구성 됩니다.

1. [연습 1: 작업 로깅](#Exercise1)
2. [연습 2: 여러 작업 필터 관리](#Exercise2)

이 랩을 완료 하기 위한 예상 시간: **30 분**합니다.

> [!NOTE]
> 각 실습 동반 되는 **최종** 연습을 완료 한 후 가져와야 결과 솔루션이 포함 된 폴더입니다. 이 연습을 진행 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.


<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a>연습 1: 작업 로깅

이 연습에서는 ASP.NET MVC 4 필터 공급자를 사용 하 여 사용자 지정 작업 로그 필터를 만드는 방법을 배웁니다. 해당 목적을 위해 선택한 컨트롤러의 모든 활동을 기록 하는 MusicStore 사이트로 로깅 필터를 적용 합니다.

필터를 확장 합니다 **ActionFilterAttributeClass** 시키고 **OnActionExecuting** 메서드를 각 요청을 catch 하 고 다음 로깅 작업을 수행 합니다. HTTP 요청에 대 한 컨텍스트 정보를 실행 하는 메서드, 결과 및 매개 변수에서 제공 합니다 ASP.NET MVC **ActionExecutingContext** 클래스 **합니다.**

> [!NOTE]
> ASP.NET MVC 4 기본 필터 공급자는 사용자 지정 필터를 만들지 않고도 사용할 수 있습니다. ASP.NET MVC 4는 다음과 같은 유형의 필터를 제공합니다.
> 
> - **권한 부여** 그러면 인증 수행 또는 요청의 속성 유효성 검사 등의 작업 메서드를 실행할 것인지에 대 한 보안 결정을 필터링 합니다.
> - **작업** 작업 메서드 실행을 래핑하는 필터입니다. 이 필터는 작업 메서드에 추가 데이터를 제공, 반환 값 검사 또는 작업 메서드 실행을 취소 하는 등의 추가적인 처리를 수행할 수 있습니다.
> - **결과** ActionResult 개체의 실행을 래핑하는 필터입니다. 이 필터는 결과 HTTP 응답을 수정 하는 등의 추가 처리를 수행할 수 있습니다.
> - **예외** 어딘가에 메서드에서 예외를 throw 작업, 권한 부여 필터를 사용 하 여 시작 하 고 결과의 실행을 사용 하 여 종료 처리 되지 않은 예외가 발생 하는 경우를 실행 하는 필터입니다. 예외 필터는 로깅 또는 오류 페이지 표시 등의 작업에 사용할 수 있습니다.
> 
> 필터 공급자에 대 한 자세한 내용은이 MSDN 링크를 참조 하세요. ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)).


<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a>MVC Music Store 응용 프로그램 로깅 기능에 대 한

이 Music Store 솔루션에 사이트 로깅에 대 한 새 데이터 모델 테이블이 **ActionLog**, 다음 필드를 사용 하 여: 요청, 호출 동작, 클라이언트 IP 및 타임 스탬프를 수신 하는 컨트롤러의 이름입니다.

![데이터 모델입니다. ActionLog 테이블입니다. ](aspnet-mvc-4-custom-action-filters/_static/image1.png "데이터 모델입니다. ActionLog 테이블입니다.")

*데이터 모델-ActionLog 테이블*

솔루션에서 찾을 수 있는 작업 로그에 대 한 ASP.NET MVC 뷰를 제공 **MvcMusicStores/보기/ActionLog**:

![작업 로그 보기](aspnet-mvc-4-custom-action-filters/_static/image2.png "작업 로그 보기")

*작업 로그 보기*

이 구조를 사용 하 여 모든 작업 컨트롤러의 요청을 중단 하 고 사용자 지정 필터링을 사용 하 여 로깅을 수행에 집중 될 것입니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a>작업 1-컨트롤러의 요청을 Catch 하는 사용자 지정 필터 만들기

이 태스크에서 로깅 논리를 포함 하는 사용자 지정 필터 특성 클래스를 만들게 됩니다. ASP.NET MVC를 확장 하면 해당 용도로 **ActionFilterAttribute** 클래스 및 인터페이스를 구현 하 **IActionFilter**합니다.

> [!NOTE]
> 합니다 **ActionFilterAttribute** 모든 특성 필터에 대 한 기본 클래스입니다. 컨트롤러 작업의 실행 전과 후에 특정 논리를 실행 하려면 다음 메서드를 제공 합니다.
> 
> - **OnActionExecuting**(ActionExecutingContext filterContext): 작업 바로 전에 호출 됩니다.
> - **OnActionExecuted**(ActionExecutedContext filterContext): 작업 메서드가 호출 된 후 및 결과 보기 렌더링) (이전에 실행 되기 전에 합니다.
> - **OnResultExecuting**(ResultExecutingContext filterContext): 결과 보기 렌더링) (이전에 실행 되기 전에 합니다.
> - **OnResultExecuted**(ResultExecutedContext filterContext): (뷰를 렌더링할) 후 결과 실행 합니다.
> 
> 이러한 방법 중 하나를 파생 클래스로 재정의 함으로써 필터링 사용자 고유의 코드를 실행할 수 있습니다.


1. 엽니다는 **시작할** 솔루션에 있는 **\Source\Ex01-LoggingActions\Begin** 폴더.

   1. 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
      > 
      > 자세한 내용은이 문서를 참조 하세요. [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.
2. 에 새 C# 클래스를 추가 합니다 **필터** 폴더 하 고 이름을 *CustomActionFilter.cs*합니다. 이 폴더는 모든 사용자 지정 필터를 저장 합니다.
3. 오픈 **CustomActionFilter.cs** 에 대 한 참조를 추가 하 고 **System.Web.Mvc** 하 고 **MvcMusicStore.Models** 네임 스페이스:

    (코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 1 CustomActionFilterNamespaces*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. 상속 된 **CustomActionFilter** 에서 클래스 **ActionFilterAttribute** 한 다음 **CustomActionFilter** 클래스 구현 **IActionFilter** 인터페이스입니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. 확인 **CustomActionFilter** 메서드를 재정의 하는 클래스 **OnActionExecuting** 필터의 실행을 기록 하는 데 필요한 논리가 추가 합니다. 이렇게 하려면 다음 강조 표시 된 코드를 추가 **CustomActionFilter** 클래스입니다.

    (코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 1 LoggingActions*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > **OnActionExecuting** 메서드를 사용 하 여 **Entity Framework** 새 ActionLog 레지스터를 추가 합니다. 만들고 새 엔터티 인스턴스 컨텍스트 정보로 채웁니다 **filterContext**합니다.
    > 
    > 에 대 한 자세한 내용은 **ControllerContext** 에서 클래스 [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)합니다.

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a>작업 2-코드 인터셉터 저장소 컨트롤러 클래스에 삽입

이 작업에서 모든 컨트롤러 클래스 및 기록 될 컨트롤러 작업에 삽입 하 여 사용자 지정 필터를 추가 합니다. 이 연습에서는 저장소 컨트롤러 클래스에 로그를 해야 합니다.

메서드 **OnActionExecuting** 에서 **ActionLogFilterAttribute** 삽입 된 요소를 호출할 때 사용자 지정 필터를 실행 합니다.

특정 컨트롤러 메서드를 가로챌 수 이기도 합니다.

1. 열기는 **StoreController** 에 **MvcMusicStore\Controllers** 에 대 한 참조를 추가 합니다 **필터** 네임 스페이스:

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. 사용자 지정 필터를 삽입할 **CustomActionFilter** 로 **StoreController** 클래스를 추가 하 여 **[CustomActionFilter]** 특성 클래스 선언 전 합니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > 필터는 컨트롤러 클래스에 주입 됩니다을 하는 경우 모든 작업 삽입도 됩니다. 일련의 작업에 대해서만 필터를 적용 하려는 있다면 삽입할 **[CustomActionFilter]** 중 각각에:
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>작업 3-응용 프로그램 실행

이 태스크에서는 로깅 필터 작동 하는지 테스트 합니다. 응용 프로그램을 시작 되며 스토어 방문 및 로그인된 활동 확인 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.
2. 이동할 **/ActionLog** 로그 보기에 대 한 초기 상태를 보려면:

    ![로그 페이지 작업 하기 전에 상태 추적기](aspnet-mvc-4-custom-action-filters/_static/image3.png "페이지 작업 전에 추적 상태를 기록 합니다.")

    *페이지 작업 하기 전에 로그 추적기 상태*

   > [!NOTE]
   > 기본적으로 메뉴에 대 한 기존 장르를 검색 하는 경우 생성 되는 하나의 항목이 항상 표시 됩니다.
   > 
   > 간단히 하기 위해 정리 될 예정 된 **ActionLog** 각 특정 작업의 확인의 로그만 표시 됩니다 있도록 응용 프로그램이 실행 될 때마다 테이블입니다.
   > 
   > 다음 코드를 제거 해야 하는 **세션\_시작** 메서드 (에 **Global.asax** 클래스) 저장소 내에서 실행 되는 모든 작업에 대 한 기록 로그를 저장 하기 위해 컨트롤러입니다.
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. 중 하나를 클릭 합니다 **장르** 메뉴에서 사용할 수 있는 앨범을 검색 하는 등 일부 작업을 수행 합니다.
4. 이동할 **/ActionLog** 경우 로그 빈 키를 눌러 **F5** 페이지를 새로 고칠 합니다. 에 방문 추적 된를 확인 합니다.

    ![활동 로그를 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image4.png "활동 로그를 사용 하 여 작업 로그")

    *활동 로그를 사용 하 여 작업 로그*

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a>연습 2: 여러 작업 필터 관리

이 연습에서 StoreController 클래스에 두 번째 사용자 지정 작업 필터를 추가 하 고 필터 둘 모두를 실행할 수 있는 특정 순서를 정의 합니다. 그런 다음 필터를 전역으로 등록 하는 코드를 업데이트 됩니다.

필터 실행 순서를 정의할 때 고려해 야 할 다른 옵션이 있습니다. 예를 들어 주문 속성 및 필터 범위:

정의할 수 있습니다는 **범위** 각 필터에 대 한 예를 들어, 있습니다 수 범위 내에서 실행 하는 모든 작업 필터는 **컨트롤러 범위**, 및에서 실행 하려면 모든 권한 부여 필터 **전역 범위** . 범위 정의 된 실행 순서는 경우

또한 각 작업 필터에는 실행 순서는 필터의 범위를 결정 하는 데 사용 되는 순서 속성이 있습니다.

사용자 지정 작업 필터 실행 순서에 대 한 자세한 내용은이 MSDN 문서를 참조 하세요. ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a>태스크 1: 새 사용자 지정 작업 필터 만들기

이 태스크에서는 만들려는 StoreController 클래스에 삽입 하려면 새 사용자 지정 작업 필터를 필터의 실행 순서를 관리 하는 방법을 학습 합니다.

1. 엽니다는 **시작할** 솔루션에 있는 **\Source\Ex02-ManagingMultipleActionFilters\Begin** 폴더. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.

    1. 제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
    2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
    3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

        > [!NOTE]
        > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
        > 
        > 자세한 내용은이 문서를 참조 하세요. [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.
2. 에 새 C# 클래스를 추가 합니다 **필터** 폴더 이름을 *MyNewCustomActionFilter.cs*
3. 오픈 **MyNewCustomActionFilter.cs** 에 대 한 참조를 추가 하 고 **System.Web.Mvc** 하며 **MvcMusicStore.Models** 네임 스페이스:

    (코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 2 MyNewCustomActionFilterNamespaces*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. 기본 클래스 선언을 다음 코드로 바꿉니다.

    (코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-e x 2 MyNewCustomActionFilterClass*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > 이 사용자 지정 작업 필터는 이전 연습에서 만든 것 보다 거의 동일 합니다. 주요 차이점은 있는지는 *&quot;하 여 기록&quot;* 본 필터를 식별 하는이 새 클래스의이 이름으로 업데이트 하는 특성의 로그를 등록 합니다.

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a>작업 2: StoreController 클래스에는 새 코드 인터셉터 삽입

이 태스크에서는 StoreController 클래스에 새 사용자 지정 필터를 추가 하 고 필터 둘 모두 어떻게 함께 작동을 확인 하려면 솔루션을 실행 합니다.

1. 엽니다는 **StoreController** 클래스에 있는 **MvcMusicStore\Controllers** 하 고 새 사용자 지정 필터 삽입 **MyNewCustomActionFilter** 에  **StoreController** 과 같은 클래스는 다음 코드에 표시 됩니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. 이제 이러한 두 사용자 지정 작업 필터의 작동 방식을 확인 하기 위해 응용 프로그램을 실행 합니다. 이 작업을 수행 하려면 키를 누릅니다 **F5** 응용 프로그램이 시작 될 때까지 기다립니다.
3. 이동할 **/ActionLog** 로그 보기에 대 한 초기 상태를 확인 합니다.

    ![로그 페이지 작업 하기 전에 상태 추적기](aspnet-mvc-4-custom-action-filters/_static/image5.png "페이지 작업 전에 추적 상태를 기록 합니다.")

    *페이지 작업 하기 전에 로그 추적기 상태*
4. 중 하나를 클릭 합니다 **장르** 메뉴에서 사용할 수 있는 앨범을 검색 하는 등 일부 작업을 수행 합니다.
5. 이 시간 확인 에 방문 두 번 추적 된:에 추가한 각 사용자 지정 작업 필터에 대 한 합니다 **StorageController** 클래스입니다.

    ![활동 로그를 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image6.png "활동 로그를 사용 하 여 작업 로그")

    *활동 로그를 사용 하 여 작업 로그*
6. 브라우저를 닫습니다.

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a>작업 3: 필터 순서 관리

이 작업 순서 속성을 사용 하 여 필터 실행 순서를 관리 하는 방법을 배웁니다.

1. 열기는 **StoreController** 클래스에 있는 **MvcMusicStore\Controllers** 지정 합니다 **순서** 속성 필터 둘 모두에 같은 아래와 같이 합니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. 이제 필터의 순서 속성의 값에 따라 실행 되는 방식을 확인 합니다. 필터의 가장 작은 값을 사용 하 여 볼 수 있습니다 (**CustomActionFilter**)이 실행 되는 1입니다. 키를 눌러 **F5** 응용 프로그램이 시작 될 때까지 기다립니다.
3. 이동할 **/ActionLog** 로그 보기에 대 한 초기 상태를 확인 합니다.

    ![로그 페이지 작업 하기 전에 상태 추적기](aspnet-mvc-4-custom-action-filters/_static/image7.png "페이지 작업 전에 추적 상태를 기록 합니다.")

    *페이지 작업 하기 전에 로그 추적기 상태*
4. 중 하나를 클릭 합니다 **장르** 메뉴에서 사용할 수 있는 앨범을 검색 하는 등 일부 작업을 수행 합니다.
5. 검사는이 이번에 따라 방문 추적 된 필터의 순서 값으로 정렬 합니다. **CustomActionFilter** 로그의 첫 번째입니다.

    ![활동 로그를 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image8.png "활동 로그를 사용 하 여 작업 로그")

    *활동 로그를 사용 하 여 작업 로그*
6. 이제 필터의 순서 값을 업데이트 한 로깅 순서가 변경 하는 방법을 확인 합니다. 에 **StoreController** 클래스, 아래와 같은 필터의 순서 값을 업데이트 합니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. 키를 눌러 응용 프로그램을 다시 실행 **F5**합니다.
8. 중 하나를 클릭 합니다 **장르** 메뉴에서 사용할 수 있는 앨범을 검색 하는 등 일부 작업을 수행 합니다.
9. 이 이번에는 로그 여 만들어졌는지 확인 **MyNewCustomActionFilter** 필터 첫 번째로 표시 됩니다.

    ![활동 로그를 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image9.png "활동 로그를 사용 하 여 작업 로그")

    *활동 로그를 사용 하 여 작업 로그*

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a>작업 4: 전역 필터 등록

이 태스크에서는 새 필터를 등록 하는 솔루션 업데이트 됩니다 (**MyNewCustomActionFilter**) 글로벌 필터로 합니다. 이 작업을 수행 하 여 이전 태스크와 같이 StoreController 것 뿐만 아니라 응용 프로그램에 모든 작업 perfomed로 트리거할 수 됩니다.

1. **StoreController** 클래스를 제거할 **[MyNewCustomActionFilter]** 특성과 order 속성에서 **[CustomActionFilter]** 합니다. 다음과 같아야 합니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. 오픈 **Global.asax** 찾아서 파일을 **응용 프로그램\_시작** 메서드. 때마다 응용 프로그램 시작 알림 전역 필터를 등록 하는 호출 하 여 **RegisterGlobalFilters** 내에서 메서드 **FilterConfig** 클래스입니다.

    ![Global.asax의 전역 필터 등록](aspnet-mvc-4-custom-action-filters/_static/image10.png "Global.asax의 전역 필터 등록")

    *Global.asax의 전역 필터 등록*
3. 오픈 **등록 합니다** 내에 파일이 **앱\_시작** 폴더입니다.
4. System.Web.Mvc;를 사용 하 여에 대 한 참조를 추가 합니다. MvcMusicStore.Filters;를 사용 하 여 네임 스페이스입니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. 업데이트 **RegisterGlobalFilters** 메서드를 사용자 지정 필터를 추가 합니다. 이렇게 하려면 강조 표시 된 코드를 추가 합니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. 키를 눌러 응용 프로그램을 실행 **F5**합니다.
7. 중 하나를 클릭 합니다 **장르** 메뉴에서 사용할 수 있는 앨범을 검색 하는 등 일부 작업을 수행 합니다.
8. 이제 확인 **[MyNewCustomActionFilter]** 너무 HomeController ActionLogController에 삽입 되 고 됩니다.

    ![활동 로그를 사용 하 여 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image11.png "활동 로그를 사용 하 여 작업 로그")

    *전역 작업 로그를 사용 하 여 작업 로그*

> [!NOTE]
> 또한 다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다 [부록 b: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixB)합니다.


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습을 완료 하 여 사용자 지정 작업을 실행 하는 작업 필터를 확장 하는 방법을 배웠습니다. 또한 페이지 컨트롤러에 필터를 주입 하는 방법을 배웠습니다. 다음 개념 사용 되었습니다.

- ASP.NET MVC ActionFilterAttribute 클래스를 사용 하 여 사용자 지정 작업 필터를 만드는 방법
- ASP.NET MVC 컨트롤러에 필터를 삽입 하는 방법
- 필터 순서 속성을 사용 하 여 순서를 관리 하는 방법
- 필터를 전역으로 등록 하는 방법

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 a: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**. 다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.

1. 로 이동 [ [ https://go.microsoft.com/? linkid 9810169 =](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)합니다. 또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Windows Azure SDK를 사용 하 여 Web</em>&quot;합니다.
2. 클릭할 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.

    ![Visual Studio Express를 설치](aspnet-mvc-4-custom-action-filters/_static/image12.png "Visual Studio Express를 설치 합니다.")

    *Visual Studio Express를 설치 합니다.*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건에 동의](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    *사용 조건에 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **완료**합니다.

    ![설치 완료](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. 로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.

    ![VS Express for Web 타일](aspnet-mvc-4-custom-action-filters/_static/image16.png)

    *VS Express for Web 타일*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>부록 b: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

이 부록은 Windows Azure 관리 포털에서 새 웹 사이트를 만들고 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하 고 랩에 따라 얻은 응용 프로그램을 게시 하는 방법을 보여 줍니다.

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>작업 1-Windows에서 새 웹 사이트를 만드는 Azure Portal

1. 로 이동 합니다 [Windows Azure 관리 포털](https://manage.windowsazure.com/) 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.

    > [!NOTE]
    > Windows Azure를 사용 하 여 10 개의 ASP.NET 웹 사이트를 무료로 호스트할 수 있으며 다음 트래픽 증가 따라 확장할 수 있습니다. 등록할 수 있습니다 [여기](http://aka.ms/aspnet-hol-azure)합니다.

    ![Windows Azure 포털에 로그온](aspnet-mvc-4-custom-action-filters/_static/image17.png "Windows Azure 포털에 로그온")

    *Windows Azure 관리 포털에 로그온*
2. 클릭 **새로 만들기** 명령 모음에서.

    ![새 웹 사이트를 만드는](aspnet-mvc-4-custom-action-filters/_static/image18.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. 클릭 **계산** | **웹 사이트**합니다. 선택한 **빨리 만들기** 옵션입니다. 새 웹 사이트를 사용할 수 있는 URL을 제공 하 고 클릭 **웹 사이트 만들기**합니다.

    > [!NOTE]
    > Windows Azure 웹 사이트는 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트. 빠른 생성 옵션을 사용 하면 완료 된 웹 응용 프로그램을 Windows Azure에서 웹 사이트 포털 외부에서 배포할 수 있습니다. 데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](aspnet-mvc-4-custom-action-filters/_static/image19.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.
5. 웹 사이트를 만든 후 아래의 링크를 클릭 합니다 **URL** 열입니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트를 찾아](aspnet-mvc-4-custom-action-filters/_static/image20.png "새 웹 사이트를 검색 합니다.")

    *새 웹 사이트를 검색합니다.*

    ![실행 중인 웹 사이트](aspnet-mvc-4-custom-action-filters/_static/image21.png "실행 중인 웹 사이트")

    *실행 중인 웹 사이트*
6. 포털로 돌아가서에서 웹 사이트의 이름을 클릭 합니다 **이름을** 관리 페이지를 표시 하는 열입니다.

    ![웹 사이트 관리 페이지를 열어](aspnet-mvc-4-custom-action-filters/_static/image22.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. **대시보드** 페이지의 **간략 상태** 섹션을 클릭 합니다 **게시 프로필 다운로드** 링크.

    > [!NOTE]
    > 합니다 *게시 프로필* 모든 각각의 설정 된 게시 방법에 대 한 Windows Azure 웹 사이트를 웹 응용 프로그램을 게시 하는 데 필요한 정보를 포함 합니다. 게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열을 포함 합니다. **Microsoft WebMatrix 2**하십시오 **Microsoft Visual Studio Express for Web** 하 고 **Microsoft Visual Studio 2012** 읽기 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화할 Windows Azure websites에 웹 응용 프로그램을 게시합니다.

    ![게시 프로필 다운로드 웹 사이트](aspnet-mvc-4-custom-action-filters/_static/image23.png "게시 프로필 다운로드 웹 사이트")

    *게시 프로필 다운로드 웹 사이트*
8. 알려진된 위치에 게시 프로필 파일을 다운로드 합니다. 추가이 연습에서이 파일을 사용 하 여 Visual Studio에서 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 방법을 표시 됩니다.

    ![게시 프로필 파일을 저장](aspnet-mvc-4-custom-action-filters/_static/image24.png "게시 프로필 저장")

    *게시 프로필 파일을 저장 하는 중*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL 서버를 사용할 경우 데이터베이스를 SQL Database 서버 만들기 해야 합니다. SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하는 것에 대 한 SQL Database 서버를 해야 합니다. Windows Azure 관리 포털에서 구독의 SQL Database 서버를 볼 수 있습니다 **Sql Database** | **서버** | **서버 대시보드**합니다. 만든 서버가 없는 경우 하나를 사용 하 여 만들 수 있습니다 합니다 **추가** 명령 모음에서 단추입니다. 기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**처럼 다음 작업에서 사용 됩니다. 만들지 마십시오 데이터베이스 아직 이후 단계에서 만들어집니다.

    ![SQL Database 서버 대시보드](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database 서버 대시보드")

    *SQL Database 서버 대시보드*
2. 다음 태스크에서는 테스트 Visual Studio에서 데이터베이스 연결 서버 목록에 로컬 IP 주소를 포함 해야 하는 이유로 **허용 된 IP 주소**합니다. 이렇게 하려면 클릭 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여 넣습니다 합니다 **시작 IP 주소** 및 **끝IP주소** 입력란을 클릭 합니다 ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) 단추입니다.

    ![클라이언트 IP 주소를 추가합니다.](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    *클라이언트 IP 주소를 추가합니다.*
3. 한 번 합니다 **클라이언트 IP 주소** 허용 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 변경을 확인 합니다.

    ![변경 확인](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    *변경 확인*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션 돌아갑니다. 에 **솔루션 탐색기**, 웹 사이트 프로젝트를 마우스 오른쪽 단추로 **게시**합니다.

    ![응용 프로그램 게시](aspnet-mvc-4-custom-action-filters/_static/image29.png "응용 프로그램 게시")

    *웹 사이트를 게시합니다.*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필 가져오기](aspnet-mvc-4-custom-action-filters/_static/image30.png "게시 프로필 가져오기")

    *게시 프로필 가져오기*
3. 클릭 **연결의 유효성을 검사**합니다. 유효성 검사가 완료 되 면 클릭 **다음**합니다.

    > [!NOTE]
    > 연결 유효성 검사 단추 옆에 나타나는 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.

    ![연결 유효성 검사](aspnet-mvc-4-custom-action-filters/_static/image31.png "연결 유효성 검사")

    *연결 유효성 검사*
4. 에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추를 클릭 (즉 **DefaultConnection**).

    ![웹 배포 구성](aspnet-mvc-4-custom-action-filters/_static/image32.png "웹 배포 구성")

    *웹 배포 구성*
5. 데이터베이스 연결을 다음과 같이 구성 합니다.

   - 에 **서버 이름** SQL Database 서버 URL 사용 하 여 입력 합니다 *tcp:* 접두사입니다.
   - **사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 서버 관리자 로그인 암호를 입력 합니다.
   - 새 데이터베이스 이름을 입력 합니다.

     ![대상 연결 문자열 구성](aspnet-mvc-4-custom-action-filters/_static/image33.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 다음 **확인**을 클릭합니다. 데이터베이스를 만들라는 메시지가 나오면 **예**합니다.

    ![데이터베이스를 만드는](aspnet-mvc-4-custom-action-filters/_static/image34.png "데이터베이스 문자열 만들기")

    *데이터베이스 만들기*
7. 기본 연결 텍스트 상자 내에서 사용 하 여 Windows Azure에서 SQL Database에 연결 하는 연결 문자열 표시 됩니다. **다음**을 클릭합니다.

    ![SQL Database를 가리키는 연결 문자열](aspnet-mvc-4-custom-action-filters/_static/image35.png "SQL 데이터베이스를 가리키는 연결 문자열")

    *SQL Database를 가리키는 연결 문자열*
8. 에 **미리 보기** 페이지에서 클릭 **게시**합니다.

    ![웹 응용 프로그램 게시](aspnet-mvc-4-custom-action-filters/_static/image36.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>부록 c: 코드 조각 사용

코드 조각을 사용 하 여 결정적인 순간에 필요한 모든 코드를 해야 합니다. 랩 문서가 알려줍니다 정확 하 게 사용할 수 있는 시기를 다음 그림과 같습니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드를 삽입할](aspnet-mvc-4-custom-action-filters/_static/image37.png "프로젝트에 코드를 삽입 하는 Visual Studio를 사용 하 여 코드 조각을")

*프로젝트에 코드를 삽입 하려면 Visual Studio 코드 조각 사용*

***키보드 (C#만 해당)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드를 삽입 하려는 위치에 커서를 놓습니다.
2. 시작 (공백 없이 하이픈) 조각 이름을 입력 합니다.
3. IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.
4. 올바른 코드 조각을 선택 합니다 (또는 전체 코드 조각 이름을 선택 될 때까지 입력 유지).
5. 커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.

![코드 조각 이름을 입력](aspnet-mvc-4-custom-action-filters/_static/image38.png "조각 이름을 입력 하기 시작")

*코드 조각 이름을 입력 하기 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각을](aspnet-mvc-4-custom-action-filters/_static/image39.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")

*Tab 키를 눌러 강조 표시 된 코드 조각 선택*

![Tab 키를 다시 코드 조각 확장 됩니다](aspnet-mvc-4-custom-action-filters/_static/image40.png "다시 Tab 키를 누릅니다 하 고 코드 조각에서는 확장")

*Tab 키를 다시 및 코드 조각에서는 확장*

***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가할*** 1입니다. 코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.

1. 선택 **코드 조각 삽입** 뒤 **내 코드 조각**합니다.
2. 클릭 하 여 목록에서 관련 코드 조각을 선택 합니다.

![코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-custom-action-filters/_static/image41.png "코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭")

*코드 조각을 삽입할 선택한 코드 조각 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭*

![클릭 하 여 목록에서 관련 코드 조각 선택](aspnet-mvc-4-custom-action-filters/_static/image42.png "클릭 하 여 목록에서 관련 코드 조각 선택")

*클릭 하 여 목록에서 관련 코드 조각 선택*
