---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 기본 사항 | Microsoft Docs
author: rick-anderson
description: 이 실습 랩에서 MVC (모델 뷰 컨트롤러) 음악 스토어를 소개 하 고 ASP.NET MV를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램을 기반으로...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 225dff4663e0e556cfb8966f1078848b4c2b47a5
ms.sourcegitcommit: 3a893ae05f010656d99d6ddf55e82f1b5b6933bc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/18/2018
ms.locfileid: "34306769"
---
# <a name="aspnet-mvc-4-fundamentals"></a>ASP.NET MVC 4 기본 사항

으로 [웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트를 다운로드 합니다.](https://aka.ms/webcamps-training-kit)

이 실습 랩에서 MVC (모델 뷰 컨트롤러) 음악 스토어를 소개 하 고 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램을 기반으로 합니다. 랩 전체은 단순 하기 때문에 설명 합니다 함께 이러한 기술을 사용 하 여의 전원 아직 합니다. 간단한 응용 프로그램으로 시작 하 고를 구성할 때까지 모든 기능을 갖춘 ASP.NET MVC 4 웹 응용 프로그램 작성 합니다.

이 랩에서 ASP.NET MVC 4에서 작동합니다.

찾을 수 자습서 응용 프로그램의 ASP.NET MVC 3 버전을 탐색 하려면 [MVC 음악 저장소](https://github.com/evilDave/MVC-Music-Store)합니다.

이 실습 랩에서 개발자가의 HTML 및 JavaScript 등의 웹 개발 기술을 경험 가정 합니다.

> [!NOTE]
> 모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다. 이 랩에 특정 프로젝트에서 사용할 수는 [ASP.NET MVC 4 기초](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)합니다.

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a>음악 스토어 응용 프로그램

이 랩에서 전체에서 빌드되는 음악 스토어 웹 응용 프로그램 세 부분으로 구성: 쇼핑, 체크 아웃, 및 관리 합니다. 방문자 장르별로 앨범 찾아보기, 앨범 자신의 카트에 추가 하 고, 선택 검토 하 고 마지막으로 로그인 하 고 주문을 완료할 체크 아웃을 계속 진행 하는 작업을 할 수 있습니다. 또한 저장소 관리자가 사용할 수 있는 앨범 뿐 아니라 주 속성을 관리할 수 없게 됩니다.

![Music Store 화면](aspnet-mvc-4-fundamentals/_static/image1.png "Music Store 화면")

*Music Store 화면*

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a>ASP.NET MVC 4 Essentials

사용 하 여 음악 스토어 응용 프로그램을 작성 **컨트롤러 MVC (Model View)**, 응용 프로그램을 세 가지 주요 구성 요소를 구분 하는 아키텍처 패턴:

- **모델**: 모델 개체는 도메인 논리를 구현 하는 응용 프로그램의 구성 요소입니다. 종종, 모델 개체도 검색 및 모델 상태를 데이터베이스에 저장 합니다.
- **보기:** 뷰는 응용 프로그램의 UI (사용자 인터페이스)를 표시 하는 구성 요소입니다. 일반적으로이 UI는 모델 데이터에서 만들어집니다. 텍스트 상자 및 앨범 개체의 현재 상태에 따라 드롭 다운 목록을 표시 하는 앨범의 편집 뷰 예로 들 수 있습니다.
- **컨트롤러의 경우:** 컨트롤러는 사용자 상호 작용 처리는 모델을 조작 하 고 궁극적으로 UI를 렌더링 하는 뷰를 선택 하는 구성 요소입니다. MVC 응용 프로그램에서 보기는 정보만 표시합니다. 컨트롤러가 사용자 입력 및 상호 작용을 처리하고 응답합니다.

MVC 패턴을 사용 하면 이러한 요소 간의 느슨한 결합을 제공 하는 동안 응용 프로그램 (입력된 논리, 비즈니스 논리 및 UI 논리)의 다양 한 측면을 구분 하는 응용 프로그램을 만들 수 있습니다. 이러한 분리 구현 시 한 번에 하나의 측면에 초점을 맞출 수 있으므로 응용 프로그램을 빌드할 때 복잡도 관리할 수 있습니다. 또한 MVC 패턴을 사용 하면 쉽게도 응용 프로그램을 만들기 위한 테스트 기반 개발 (TDD) 사용을 권장 하는 응용 프로그램을 테스트할 수 있습니다.

**ASP.NET MVC** 프레임 워크는 ASP.NET MVC 기반 웹 응용 프로그램을 만들기 위한 ASP.NET Web Forms 패턴에 대 한 대안을 제공 합니다. **ASP.NET MVC** 프레임 워크는 간단 하 고 테스트 하기 편리한 프레젠테이션 프레임 워크는 (웹 폼 기반 응용 프로그램와 마찬가지로) 마스터 페이지 및 멤버 자격을 기반으로 기존 ASP.NET 기능과 통합 되어 핵심.NET framework의 모든 기능을 얻게 되므로 인증입니다. 이미 잘 알고 있다면 ASP.NET Web Forms 이미 사용 하는 모든 라이브러리도 ASP.NET MVC 4에서 사용할 수 있는 경우에 유용 합니다.

또한 MVC 응용 프로그램의 세 가지 주요 구성 요소 간의 느슨한 결합 병렬 개발을 촉진 하기도 합니다. 예를 들어 한 개발자 보기에서 작업할 수 있습니다, 두 번째 개발자는 컨트롤러 논리에서 작업할 수 있습니다 및 세 번째 개발자는 모델의 비즈니스 논리에 집중할 수 있습니다.

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 배우게 됩니다 하는 방법:

- 음악 스토어 응용 프로그램 자습서를 기반으로 ASP.NET MVC 응용 프로그램 만들기
- 사이트 및 검색의 주요 기능에 대 한 홈 페이지 Url을 처리 하기 위해 컨트롤러 추가
- 노드 스타일 함께 표시 되는 콘텐츠를 사용자 지정 하는 뷰 추가
- 모델 클래스를 포함 하 고 관리할 데이터 및 도메인 논리를 추가 합니다.
- 뷰 모델 패턴을 사용 하 여 컨트롤러 작업에서 정보 보기 템플릿을 전달
- 인터넷 응용 프로그램에 대 한 ASP.NET MVC 4 새 서식 파일을 탐색 합니다.

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (읽기 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은)

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>설정

**설치 하는 코드 조각**

편의 위해는이 랩에 따라 관리 코드의 대부분 Visual Studio 코드 조각 수 있습니다. 실행 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.

이 문서에서 부록을 참조할 수 사용 하는 방법에 알아봅니다 사용 하 고 Visual Studio 코드 조각에 익숙한 경우 &quot; [부록 c:를 사용 하 여 코드 조각을](#AppendixC)&quot;합니다.

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습으로 구성 됩니다.

1. [연습 1: MusicStore ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기](#Exercise1)
2. [연습 2: 컨트롤러 만들기](#Exercise2)
3. [연습 3: 컨트롤러에 매개 변수 전달](#Exercise3)
4. [보기를 만드는 연습 4:](#Exercise4)
5. [연습 5: 뷰 모델 만들기](#Exercise5)
6. [실습 6: 매개 변수를 보기에 사용](#Exercise6)
7. [7 연습: ASP.NET MVC 4 새 템플릿 주위 랩](#Exercise7)

> [!NOTE]
> 각 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다. 연습을 통해 작업 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.


예상 소요 시간: **60 분**합니다.

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a>연습 1: MusicStore ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기

이 연습에서는 Visual Studio 2012 express의 주 폴더 조직와 함께 웹에 대 한 ASP.NET MVC 응용 프로그램을 만드는 방법에 설명 합니다. 또한 새 컨트롤러를 추가 하 고 응용 프로그램의 홈 페이지에 단순 문자열을 표시 하는 방법에 설명 합니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a>작업 1-ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기

1. 이 태스크에서는 MVC Visual Studio 템플릿을 사용 하 여 빈 ASP.NET MVC 응용 프로그램 프로젝트를 만듭니다. 시작 **VS Express for Web**합니다.
2. **파일** 메뉴에서 **새 프로젝트**를 클릭합니다.
3. 에 **새 프로젝트** 대화 상자 선택 된 **ASP.NET MVC 4 웹 응용 프로그램** 프로젝트 아래에 있는 형식을 **Visual C#** **웹** 서식 파일 목록입니다.
4. 변경 된 **이름** 를 *MvcMusicStore*합니다.
5. 새 내부 솔루션의 위치를 설정할 **시작** 예를 들어가이 연습 원본 폴더에 폴더 **[귀하가 HOL 경로] \Source\Ex01-CreatingMusicStoreProject\Begin**합니다. **확인**을 클릭합니다.

    ![새 프로젝트 대화 상자 만들기](aspnet-mvc-4-fundamentals/_static/image2.png "새 프로젝트 대화 상자 만들기")

    *새 프로젝트 대화 상자 만들기*
6. 에 **새 ASP.NET MVC 4 프로젝트** 대화 상자 선택은 **기본** 템플릿 있는지 확인 하 고는 **뷰 엔진** 선택한 **Razor**합니다. **확인**을 클릭합니다.

    ![새 ASP.NET MVC 4 프로젝트 대화 상자](aspnet-mvc-4-fundamentals/_static/image3.png "새 ASP.NET MVC 4 프로젝트 대화 상자")

    *새 ASP.NET MVC 4 프로젝트 대화 상자*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a>작업 2-솔루션 구조 탐색

ASP.NET MVC 프레임 워크에는 MVC 패턴을 지 원하는 웹 응용 프로그램을 만들 때 도움이 되는 Visual Studio 프로젝트 템플릿이 포함 되어 있습니다. 이 템플릿은 필요한 폴더, 항목 템플릿 및 구성 파일 항목 새 ASP.NET MVC 웹 응용 프로그램을 만듭니다.

이 작업에서는 포함 된 요소를 이해 하는 솔루션 구조 및 해당 관계를 검사 합니다. 기본적으로 ASP.NET MVC 프레임 워크를 사용 하기 때문에 모든 ASP.NET MVC 응용 프로그램에는 다음 폴더가 포함 된 한 &quot;구성의 관례&quot; 접근 방식 및 폴더 이름 지정에 따라 몇 가지 기본 사항을 가정 하면 규칙입니다.

1. 프로젝트를 만든 후 오른쪽에 솔루션 탐색기에서 만든 폴더 구조를 검토 합니다.

    ![솔루션 탐색기에서 ASP.NET MVC 폴더 구조](aspnet-mvc-4-fundamentals/_static/image4.png "솔루션 탐색기에서 ASP.NET MVC 폴더 구조")

    *솔루션 탐색기에서 ASP.NET MVC 폴더 구조*

   1. **컨트롤러**합니다. 이 폴더는 컨트롤러 클래스가 포함 됩니다. MVC 기반 응용 프로그램에서 컨트롤러는 최종 사용자 상호 작용을 처리 모델을 조작 하 고, 궁극적으로 UI를 렌더링 하는 뷰를 선택 해야 합니다.

       > [!NOTE]
       > MVC 프레임 워크를 위해서는 끝나야 모든 컨트롤러의 이름이 &quot;컨트롤러&quot;-예를 들어 HomeController, LoginController 또는 ProductController 합니다.
   2. **모델**합니다. 이 폴더는 MVC 웹 응용 프로그램에 대 한 응용 프로그램 모델을 나타내는 클래스를 위해 제공 됩니다. 일반적으로 개체와 데이터 저장소와 상호 작용 하기 위한 논리를 정의 하는 코드가 포함 됩니다. 일반적으로 실제 모델 개체는 별도 클래스 라이브러리에 있게 됩니다. 그러나 새 응용 프로그램을 만들 때 클래스를 포함 한 다음 개발 주기에서 나중에 별도 클래스 라이브러리로 이동할 수 있습니다.
   3. **뷰**합니다. 이 폴더에는 뷰, 응용 프로그램의 사용자 인터페이스를 표시 하는 일을 담당 하는 구성 요소에 대 한 권장된 위치입니다. 보기 뷰 렌더링에 관련 된 다른 파일이.aspx,.ascx,.cshtml 및.master 파일을 사용 합니다. Views 폴더에는 각 컨트롤러;에 대 한 컨트롤러 이름 접두사가 포함 된 폴더의 이름은입니다. 예를 들어, 라는 컨트롤러가 있으면 **HomeController**, Views 폴더에 Home 이라는 폴더가 포함 됩니다. 기본적으로 ASP.NET MVC 프레임 워크에서는 뷰를 찾습니다 Views\controllerName 폴더에 요청 된 뷰 이름으로.aspx 파일 (**[ControllerName] [작업] 보기.aspx**) 또는 (**뷰 [ControllerName] [작업].cshtml**) Razor 뷰의 합니다.

      > [!NOTE]
      > MVC 웹 응용 프로그램은 앞에서 설명한 폴더 외에도 사용 하 여는 **Global.asax** 전역 URL 라우팅 설정 하기 위해 파일 기본값을 사용 하는 **Web.config** 파일을 응용 프로그램을 구성 합니다.

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a>작업 3-한 HomeController 추가

MVC 프레임 워크를 사용 하지 않는 ASP.NET 응용 프로그램에서 사용자 상호 작용을 발생 시키고 해당 페이지에서 이벤트를 처리 하 고 페이지를 중심 구성 됩니다. 반면, ASP.NET MVC 응용 프로그램의 사용자 상호 컨트롤러 및 해당 작업 메서드를 중심으로 구성 됩니다.

반면에 ASP.NET MVC 프레임 워크는 컨트롤러로 참조 하는 클래스에 Url을 매핑합니다. 컨트롤러 들어오는 요청을 처리, 사용자 입력 및 상호 작용을 처리, 적절 한 응용 프로그램 논리를 실행 및 클라이언트에 다시 전송할 응답을 결정 (HTML을 표시, 파일을 다운로드, 등 다른 URL 리디렉션). HTML을 표시 하는 경우 컨트롤러 클래스는 일반적으로 요청에 대 한 HTML 태그를 생성 하는 별도 뷰 구성 요소를 호출 합니다. MVC 응용 프로그램에서 보기는 정보만 표시합니다. 컨트롤러가 사용자 입력 및 상호 작용을 처리하고 응답합니다.

이 태스크에서는 Music Store 사이트의 홈 페이지 Url을 처리 하는 컨트롤러 클래스를 추가 합니다.

1. 마우스 오른쪽 단추로 클릭 **컨트롤러** 선택 솔루션 탐색기에서 폴더 **추가** 차례로 **컨트롤러** 명령:

    ![컨트롤러 명령을 추가](aspnet-mvc-4-fundamentals/_static/image5.png "컨트롤러 명령 추가")

    *컨트롤러 명령 추가*
2. **컨트롤러 추가** 대화 상자가 나타납니다. 컨트롤러 이름을 *HomeController* 누릅니다 **추가**합니다.

    ![컨트롤러 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image6.png "컨트롤러 추가 대화 상자")

    *컨트롤러 추가 대화 상자*
3. 파일 **HomeController.cs** 에서 만든는 **컨트롤러** 폴더입니다. 가지려면는 **HomeController** 문자열을 반환 하는 인덱스 작업에서 교체는 **인덱스** 메서드를 다음 코드로:

    (코드 조각- *기본 ASP.NET MVC 4-e x 1 HomeController 인덱스*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 태스크에서는 웹 브라우저에서 응용 프로그램을 사용해 됩니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다. 프로젝트를 컴파일할 하 고 로컬 IIS 웹 서버 시작 합니다. 로컬 IIS 웹 서버는 웹 서버의 URL을 가리키는 웹 브라우저를 열고 자동으로 됩니다.

    ![웹 브라우저에서 실행 중인 응용 프로그램](aspnet-mvc-4-fundamentals/_static/image7.png "웹 브라우저에서 실행 중인 응용 프로그램")

    *웹 브라우저에서 실행 중인 응용 프로그램*

    > [!NOTE]
    > 로컬 IIS 웹 서버는 임의의 가능한 포트 번호를에서 웹 사이트를 실행 합니다. 위 그림에는 사이트에서 실행 `http://localhost:50103/`, 50103 포트를 사용 하 고 있습니다. 포트 번호가 달라질 수 있습니다.
2. 브라우저를 닫습니다.

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a>연습 2: 컨트롤러 만들기

이 연습에서는 음악 스토어 응용 프로그램의 간단한 기능을 구현 하는 컨트롤러를 업데이트 하는 방법에 설명 합니다. 해당 컨트롤러는 각 다음과 같은 특정 요청을 처리 하는 작업 메서드를 정의 합니다.

- Music Store에서 음악 장르 목록 페이지
- 특정 장르에 대 한 음악 앨범을 모두 나열 하는 찾아보기 페이지
- 특정 음악 앨범에 대 한 정보를 표시 하는 세부 정보 페이지

이 작업의 범위에 대해 단순히 해당 작업을 지금까지 문자열을 반환 합니다.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a>작업 1-새 StoreController 클래스 추가

이 태스크에서는 새 컨트롤러를 추가 합니다.

1. 아직 열지 않은 경우 시작 **VS 2012 Web Express**합니다.
2. 에 **파일** 메뉴 선택 **프로젝트 열기**합니다. 프로젝트 열기 대화 상자에서 찾은 **Source\Ex02 CreatingAController\Begin**선택, **Begin.sln** 클릭 **열려**합니다. 또는 계속 진행할 솔루션, 이전 연습을 완료 한 후 가져올 있음을 합니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
3. 새 컨트롤러를 추가 합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **컨트롤러** 선택 솔루션 탐색기에서 폴더 **추가** 차례로 **컨트롤러** 명령입니다. 변경 된 **컨트롤러 이름** 를 *StoreController*를 클릭 하 고 **추가**합니다.

    ![컨트롤러 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image8.png "컨트롤러 추가 대화 상자")

    *컨트롤러 추가 대화 상자*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a>작업 2-StoreController의 동작을 수정 합니다.

이 작업을 호출 되는 컨트롤러 메서드를 수정 합니다 **동작**합니다. 작업은 URL 요청을 처리 하 고 브라우저 또는 URL을 호출 하는 사용자에 게 다시 보내야 하는 내용을 결정 하는 일을 담당 합니다.

1. **StoreController** 클래스에 이미 있는 **인덱스** 메서드. 음악 스토어의 모든 장르 나열 되는 페이지를 구현 하려면이 랩에서 사용 합니다. 지금은 바꾸면는 **인덱스** 메서드는 문자열을 반환 하는 다음 코드를 &quot;Store.Index()에서 Hello&quot;:

    (코드 조각- *기본 ASP.NET MVC 4-e x 2 StoreController 인덱스*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. 추가 **찾아보기** 및 **세부 정보** 메서드. 이렇게 하려면 다음 코드를 추가 **StoreController**:

    (코드 조각- *기본 ASP.NET MVC 4-e x 2 StoreController BrowseAndDetails*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>작업 3-응용 프로그램 실행

이 태스크에서는 웹 브라우저에서 응용 프로그램을 사용해 됩니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 시작 날짜는 **홈** 페이지. 각 동작의 구현을 확인 하려면 URL을 변경 합니다.

    1. **/ 저장**합니다. 나타납니다  **&quot;Store.Index()에서 Hello&quot;** 합니다.
    2. **/ 저장소/찾아보기**합니다. 나타납니다  **&quot;Store.Browse()에서 Hello&quot;** 합니다.
    3. **/ 저장소/세부 정보**합니다. 나타납니다  **&quot;Store.Details()에서 Hello&quot;** 합니다.

        ![StoreBrowse 검색](aspnet-mvc-4-fundamentals/_static/image9.png "StoreBrowse 검색")

        */Store/Browse 검색*
3. 브라우저를 닫습니다.

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a>연습 3: 컨트롤러에 매개 변수 전달

지금까지 있습니다 있는 된 문자열을 반환 상수는 컨트롤러에서 합니다. 이 연습에서는 컨트롤러의 URL과 쿼리 문자열을 사용 하 여 하 고 다음 브라우저에 텍스트를 사용 하 여 응답할 메서드 동작에 매개 변수를 전달 하는 방법에 설명 합니다.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a>작업 1-StoreController 추가 장르 매개 변수

이 작업을 사용 하 여는 **querystring** 매개 변수를 보낼는 **찾아보기** 의 동작 메서드에 **StoreController**합니다.

1. 아직 열지 않은 경우 시작 **VS Express for Web**합니다.
2. 에 **파일** 메뉴 선택 **프로젝트 열기**합니다. 프로젝트 열기 대화 상자에서 찾은 **Source\Ex03 PassingParametersToAController\Begin**선택, **Begin.sln** 클릭 **열려**합니다. 또는 계속 진행할 솔루션, 이전 연습을 완료 한 후 가져올 있음을 합니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
3. 열기 **StoreController** 클래스입니다. 이 수행 하는 **솔루션 탐색기**를 확장 하 고는 **컨트롤러** 폴더를 두 번 클릭 **StoreController.cs**합니다.
4. 변경 된 **찾아보기** 메서드를 특정 장르를 요청 하려면 문자열 매개 변수를 추가 합니다. ASP.NET MVC 자동으로 모든 쿼리 문자열을 통과 또는 폼 게시 매개 변수 라는 **장르** 호출 될 때이 동작 메서드에 합니다. 이 작업을 수행 하려면 대체는 **찾아보기** 메서드를 다음 코드로:

    (코드 조각- *기본 ASP.NET MVC 4-Ex3 StoreController BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> 사용 하는 **HttpUtility.HtmlEncode** 같은 링크와 보기에 Javascript 주입에서 사용자가 방지 하는 유틸리티 메서드를   **/저장소/찾아보기? 장르 =&lt;스크립트&gt;window.location='[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;** 합니다.
> 
> 자세한 내용을 보려면 방문 하세요 [이 msdn 문서](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx)합니다.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>작업 2-응용 프로그램 실행

이 작업은 웹 브라우저에서 응용 프로그램 사용을 하 여 사용 하는 **장르** 매개 변수입니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 시작 날짜는 **홈** 페이지. URL을 변경 *찾아보기/저장 /? Genre Disco =* 동작 장르 매개 변수를 수신 되는지 확인 합니다.

    ![StoreBrowseGenre 검색 Disco =](aspnet-mvc-4-fundamentals/_static/image10.png "StoreBrowseGenre 검색 Disco =")

    *검색 /Store/Browse? Genre Disco =*
3. 브라우저를 닫습니다.

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a>작업 3-URL에 포함 하는 Id 매개 변수를 추가 합니다.

이 작업을 사용 하 여는 **URL** 전달 하는 **Id** 매개 변수는 **세부 정보** 의 동작 메서드는 **StoreController**합니다. ASP.NET MVC의 기본 매개 변수 이름으로 작업 메서드 이름 뒤에 오는 URL의 세그먼트를 처리 하는 라우팅 규칙 **Id**합니다. 작업 메서드에 매개 변수 Id 라는 경우 다음 ASP.NET MVC는 자동으로 URL 세그먼트를 매개 변수로 전달 합니다. URL에서 **저장소/세부 정보/5**, **Id** 로 해석 됩니다 **5**합니다.

1. 변경 된 **세부 정보** 의 메서드는 **StoreController**추가는 **int** 라는 매개 변수 **id**합니다. 이 작업을 수행 하려면 대체는 **세부 정보** 메서드를 다음 코드로:

    (코드 조각- *기본 ASP.NET MVC 4-Ex3 StoreController DetailsMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 작업은 웹 브라우저에서 응용 프로그램 사용을 하 여 사용 하는 **Id** 매개 변수입니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 시작 날짜는 **홈** 페이지. URL을 변경 */Store/Details/5* 동작 id 매개 변수를 수신 되는지 확인 합니다.

    ![StoreDetails5 검색](aspnet-mvc-4-fundamentals/_static/image11.png "StoreDetails5 검색")

    */Store/Details/5 검색*

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a>보기를 만드는 연습 4:

지금까지 있습니다 있는 된 문자열에서에서 반환 컨트롤러 작업. 컨트롤러의 작동 방식을 이해 하는 데 도움이 되 이지만 실제 웹 응용 프로그램은 작성 하는 방법에 없습니다. 뷰는 다시 템플릿 파일을 사용 하 여 브라우저에 HTML을 생성 하기 위한 더 나은 방법은 제공 하는 구성 요소입니다.

이 연습에서는 공통 HTML 콘텐츠, 사이트 및 마지막으로 HomeController HTML을 반환할 수 있도록 뷰 템플릿을의 모양과 느낌을 개선 하는 스타일 시트에 대 한 템플릿을 설정 하는 레이아웃 마스터 페이지를 추가 하는 방법에 설명 합니다.

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-layoutcshtml"></a>작업 파일을 수정 하는 1- \_layout.cshtml

파일 **~/Views/Shared/\_layout.cshtml** 전체 웹 사이트에 대해 사용 하는 일반적인 HTML에 대 한 템플릿을 설정할 수 있습니다. 이 작업 홈 페이지 및 저장소 영역에 대 한 링크가 있는 일반적인 헤더로 레이아웃 마스터 페이지를 추가 합니다.

1. 아직 열지 않은 경우 시작 **VS Express for Web**합니다.
2. 에 **파일** 메뉴 선택 **프로젝트 열기**합니다. 프로젝트 열기 대화 상자에서 찾은 **Source\Ex04 CreatingAView\Begin**선택, **Begin.sln** 클릭 **열려**합니다. 또는 계속 진행할 솔루션, 이전 연습을 완료 한 후 가져올 있음을 합니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
3. 파일  <strong>\_layout.cshtml</strong> 사이트에 있는 모든 페이지에 대 한 HTML 컨테이너 레이아웃을 포함 합니다. 여기에 포함 됩니다는 <strong>&lt;html&gt;</strong> HTML 응답에 대 한 요소와 <strong>&lt;h e a d&gt;</strong> 및 <strong>&lt;본문&gt;</strong> 요소입니다. <strong>@RenderBody()</strong> HTML 내에서 본문 영역을 확인할 해당 보기 서식 파일은 동적 콘텐츠를 사용 하 여 작성 됩니다.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. 사이트의 모든 페이지에 홈 페이지 및 저장소 영역을 링크와 함께 공용 헤더를 추가 합니다. 파일을 수집 하려면 아래에 다음 코드를 추가 &lt;본문&gt; 문.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. 각 페이지의 본문 섹션을 렌더링 하는 div를 포함 합니다. 대체  <strong>@RenderBody()</strong> 다음 higlighted 코드로: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > 알고 계십니까? Visual Studio 2012는 HTML, 코드 파일의 자주 사용 되는 코드를 추가 하기 쉽도록 코드 조각을 사용 합니다. 입력 하 여 확인해 **&lt;div&gt;** 한 키를 눌러 **탭** 전체 삽입을 두 번 **div** 태그입니다.

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a>작업 2-CSS 스타일 시트를 추가

빈 프로젝트 템플릿은 기본 형태 및 유효성 검사 메시지를 표시 하는 데 사용 되는 스타일을 포함 하는 매우 간소화 된 CSS 파일을 포함 합니다. 사이트의 모양과 느낌을 개선 하기 위해 추가 CSS 및 이미지 (잠재적으로 디자이너에서 제공)를 사용 합니다.

이 태스크에서는 해당 사이트의 스타일을 정의 하는 CSS 스타일 시트를 추가 합니다.

1. CSS 파일 및 이미지에 포함 됩니다는 **Source\Assets\Content** 이 랩의 폴더입니다. 응용 프로그램에 기호를 추가 하기 위해 자신의 콘텐츠를 끌어 한 **Windows 탐색기** 창에는 **솔루션 탐색기** Visual Studio express for Web을 아래와 같이:

    ![스타일 내용을 끌어](aspnet-mvc-4-fundamentals/_static/image12.png "끌어 스타일 내용")

    *스타일 내용을 끌기*
2. 경고 대화 상자가 표시 됩니다, 대체할 것인지 확인 하 라는 **Site.css** 파일 및 일부 기존 이미지입니다. 확인 **전체 적용** 클릭 **예**합니다.

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a>작업 3-보기 템플릿 추가

이 작업에서는 레이아웃 마스터 페이지를 사용 하 여 HTML 응답을 생성 하는 보기 템플릿을 추가한 하 고 CSS이이 연습에서는 추가 합니다.

1. 사이트의 홈 페이지를 검색할 때 뷰 템플릿을 사용 하려면 먼저 해야 합니다는 문자열을 반환 하는 대신 있음을 **HomeController 인덱스** 메서드는 반환는 **보기**합니다. 열기 **HomeController** 클래스 및 변경의 **인덱스** 반환 하는 메서드는 **ActionResult**, 고 반환 하도록 **View()** 합니다.

    (코드 조각- *기본 ASP.NET MVC 4-Ex4 HomeController 인덱스*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. 이제는 적절 한 템플릿 보기를 추가 해야 합니다. 이렇게 하려면 **마우스 오른쪽 단추로 클릭** 내는 **인덱스** 동작 메서드와 선택 **뷰 추가**합니다. 그러면 표시 됩니다는 **뷰 추가** 대화 상자.

    ![Index 메서드 내에서 뷰 추가](aspnet-mvc-4-fundamentals/_static/image13.png "인덱스 메서드 내에서 뷰를 추가 합니다.")

    *Index 메서드 내에서 뷰를 추가합니다.*
3. **뷰 추가** 보기 템플릿 파일을 생성 하려면 대화 상자가 나타납니다. 기본적으로이 대화 상자 미리 채웁니다 보기 서식 파일의 이름을 사용 하 여 동작 메서드가 일치 하도록 합니다. 사용 했기 때문에 **뷰 추가** 내 상황에 맞는 메뉴는 **인덱스** 고 HomeController 내에서 작업 메서드는 **뷰 추가** 대화 상자에 기본 보기 이름으로 인덱스입니다. **추가**를 클릭합니다.

    ![뷰 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image14.png "뷰 추가 대화 상자")

    *뷰 추가 대화 상자*
4. Visual Studio에서 생성 한 **Index.cshtml** 내 템플릿 보기는 **Views\Home** 폴더를 클릭 합니다.

    ![생성 된 인덱스 뷰 홈](aspnet-mvc-4-fundamentals/_static/image15.png "홈 인덱스 뷰 생성")

    *만든 홈 인덱스 뷰*

    > [!NOTE]
    > 이름 및 위치는 **Index.cshtml** 파일은 관련 되며 기본 ASP.NET MVC 명명 규칙을 따릅니다.
    > 
    > 폴더 \Views\**홈** 컨트롤러 이름과 일치 (**홈** 컨트롤러). 보기 템플릿 이름 (**인덱스**), 보기를 표시 하는 컨트롤러 동작 메서드에 일치 합니다.
    > 
    > 이러한 방식으로 ASP.NET MVC는 뷰를 반환 하려면이 명명 규칙을 사용 하는 경우 이름 또는 뷰 서식 파일의 위치를 명시적으로 지정 하지 않아도 합니다.
5. 생성된 된 뷰 템플릿을 기반으로  **\_layout.cshtml** 템플릿을 이전에 정의 합니다. ViewBag.Title 속성을 업데이트 **홈**, 주 콘텐츠를 변경 하 고 **는 홈 페이지**아래 코드에 표시 된 것 처럼:

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. 선택 **MvcMusicStore** 누릅니다 솔루션 탐색기에서 프로젝트 **F5** 응용 프로그램을 실행 합니다.

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a>태스크 4: 확인

이전 연습에서 모든 단계를 올바르게 수행 했는지를 확인 하려면 다음을 수행 합니다.

브라우저에서 열 응용 프로그램과 함께 있습니다 한다는 점에 유의 해야 합니다.

1. HomeController의 Index 작업 메서드의 발견 하 고 표시 되는 **\Views\Home\Index.cshtml** 코드가 있더라도 서식 파일을 볼 **View() 반환**뒤에 템플릿 보기 때문에 표준 명명 규칙입니다.
2. 내에 정의 된 환영 메시지를 표시 하는 홈 페이지는 **\Views\Home\Index.cshtml** 템플릿 보기.
3. 홈 페이지를 사용 하 여  **\_layout.cshtml** 서식 파일을 시작 메시지 표준 사이트 HTML 레이아웃 내에 포함 되어 있으므로 합니다.

    ![정의 된 LayoutPage 및 스타일을 사용 하 여 인덱스 뷰 홈](aspnet-mvc-4-fundamentals/_static/image16.png "정의 LayoutPage 및 스타일을 사용 하 여 인덱스 뷰 홈")

    *정의 된 LayoutPage 및 스타일을 사용 하 여 홈 인덱스 뷰*

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a>연습 5: 뷰 모델 만들기

지금까지 하드 코드 된 HTML을 표시 하 여 보기를 수행 하지만 동적 웹 응용 프로그램을 만들려면 템플릿 보기 받아야 정보 컨트롤러에서 합니다. 해당 용도로 사용할 일반적인 기술이 **ViewModel** 패턴을 적절 한 HTML 응답을 생성 하는 데 필요한 모든 정보를 패키지 하려면 컨트롤러가 수 있습니다.

이 연습에서는 ViewModel 클래스를 만들고 필요한 속성을 추가 하는 방법을 배우게 됩니다: 저장소 및 해당 장르 목록에는 장르의 수입니다. 만든된 ViewModel 사용할 StoreController도 업데이트 됩니다 하 고 마지막으로 페이지에서 언급 한 속성을 표시 하는 새 보기 템플릿 만들어집니다.

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a>작업 1-ViewModel 클래스 만들기

이 작업은 저장소 장르 목록 시나리오를 구현 하는 ViewModel 클래스를 만듭니다.

1. 아직 열지 않은 경우 시작 **VS Express for Web**합니다.
2. 에 **파일** 메뉴 선택 **프로젝트 열기**합니다. 프로젝트 열기 대화 상자에서 찾은 **Source\Ex05 CreatingAViewModel\Begin**선택, **Begin.sln** 클릭 **열려**합니다. 또는 계속 진행할 솔루션, 이전 연습을 완료 한 후 가져올 있음을 합니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
3. 만들기는 **Viewmodel** ViewModel 보관할 폴더를 합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 최상위 **MvcMusicStore** 프로젝트를 **추가** 차례로 **새 폴더**합니다.

    ![새 폴더 추가](aspnet-mvc-4-fundamentals/_static/image17.png "새 폴더 추가")

    *새 폴더 추가*
4. 폴더 이름을 *Viewmodel*합니다.

    ![솔루션 탐색기에서 폴더 Viewmodel](aspnet-mvc-4-fundamentals/_static/image18.png "솔루션 탐색기에서 Viewmodel 폴더")

    *솔루션 탐색기에서 Viewmodel 폴더*
5. 만들기는 **ViewModel** 클래스입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **Viewmodel** 최근에 만든 폴더를 선택 **추가** 차례로 **새 항목**합니다. 아래 **코드**, 선택는 **클래스** 항목 및 파일 이름을 *StoreIndexViewModel.cs*, 클릭 **추가**합니다.

    ![새 클래스 추가](aspnet-mvc-4-fundamentals/_static/image19.png "새 클래스 추가")

    *새 클래스 추가*

    ![StoreIndexViewModel 클래스 만들기](aspnet-mvc-4-fundamentals/_static/image20.png "만드는 StoreIndexViewModel 클래스")

    *StoreIndexViewModel 클래스 만들기*

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a>작업 2-ViewModel 클래스에 속성 추가

두 매개 변수는 StoreController에서 예상 되는 HTML 응답을 생성 하기 위해 템플릿 보기를 전달 하도록: 저장소 및 해당 장르 목록에는 장르의 수입니다.

이 작업에서는 이러한 2 속성을 추가 합니다는 **StoreIndexViewModel** 클래스: **NumberOfGenres** (정수) 및 **장르** (문자열의 목록).

1. 추가 **NumberOfGenres** 및 **장르** 속성을는 **StoreIndexViewModel** 클래스입니다. 이 위해 클래스 정의에 다음 두 줄을 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex5 StoreIndexViewModel 속성*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> **{get; 설정;을 (를)**  표기법에서 활용 C#의 자동 구현 속성 기능입니다. 지원 필드 선언를 요구 하지 않고 속성의 이점을 제공 합니다.

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a>작업 3-업데이트 StoreController는 StoreIndexViewModel 사용 하려면

**StoreIndexViewModel** 클래스에서 전달 하는 데 필요한 정보를 캡슐화 **StoreController**의 **인덱스** 보기 템플릿에 대 한 응답을 생성 하기 위해 메서드 .

이 태스크에서는 업데이트 됩니다는 **StoreController** 사용 하는 **StoreIndexViewModel**합니다.

1. 열기 **StoreController** 클래스입니다.

    ![StoreController 클래스를 열고](aspnet-mvc-4-fundamentals/_static/image21.png "여 StoreController 클래스")

    *Opening StoreController 클래스*
2. 사용 하려면는 **StoreIndexViewModel** 에서 클래스는 **StoreController**, 맨 위에 있는 다음 네임 스페이스 추가 **StoreController** 코드:

    (코드 조각- *ASP.NET MVC 4 기본-Viewmodel를 사용 하 여 Ex5 StoreIndexViewModel*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. 변경 된 **StoreController**의 **인덱스** 를 만들고 채우는 동작 메서드는 **StoreIndexViewModel** 개체를 보기 서식 파일에 전달 함께 HTML 응답을 생성 합니다.

    > [!NOTE]
    > 랩에서 &quot;ASP.NET MVC 모델 및 데이터 액세스&quot; 저장소 장르 목록을 데이터베이스에서 검색 하는 코드를 작성 합니다. 다음 코드에서는 만듭니다는 **목록** 채울 더미 데이터가 장르는 **StoreIndexViewModel**합니다.
    > 
    > 만들고 설정 후는 **StoreIndexViewModel** 개체에 대 한 인수로 전달 됩니다는 **보기** 메서드. 이 템플릿 보기를 함께 HTML 응답을 생성 하려면 해당 개체를 사용 함을 나타냅니다.
4. 대체는 **인덱스** 메서드를 다음 코드로:

    (코드 조각- *ASP.NET MVC 4 기본-Ex5 StoreController 인덱스 메서드*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> C#과 함께 잘 모르는 경우 맞는 방법 가정할 수 있으며 **var** 됨을 의미는 **viewModel** 변수는 런타임에 바인딩된 합니다. 틀렸습니다-C# 컴파일러는 형식 유추를 변수에 할당에 따라 사용 하 여 확인 되 **viewModel** 유형의 **StoreIndexViewModel**합니다. 또한 로컬을 컴파일하여 **viewModel** 변수으로 **StoreIndexViewModel** get 컴파일 타임 검사 및 Visual Studio 코드 편집기 지원을 입력 합니다.

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a>작업 4-StoreIndexViewModel를 사용 하는 보기 템플릿 만들기

이 작업에서는 장르의 목록을 표시 하려면 컨트롤러에서 전달 되는 StoreIndexViewModel 개체에서 사용할 보기 템플릿을 만듭니다.

1. 새 보기 서식 파일을 만들기 전에 프로젝트를 제작 해 보겠습니다 있도록는 **보기 대화 상자 추가** 에 대해 알고는 **StoreIndexViewModel** 클래스입니다. 선택 하 여 프로젝트를 빌드합니다는 **빌드** 메뉴 항목 차례로 **빌드 MvcMusicStore**합니다.

    ![프로젝트를 빌드하면](aspnet-mvc-4-fundamentals/_static/image22.png "프로젝트 빌드")

    *프로젝트 빌드*
2. 새 보기 템플릿을 만듭니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **인덱스** 메서드와 선택 **뷰 추가**합니다.

    ![뷰 추가](aspnet-mvc-4-fundamentals/_static/image23.png "뷰 추가")

    *보기 추가*
3. 때문에 **보기 대화 상자 추가** 에서 호출 되었습니다는 **StoreController**, 템플릿 보기에 기본적으로 추가 되는 **\Views\Store\Index.cshtml** 파일입니다. 확인은 **보기를 만들 강력한-입력 한-** 확인란을 선택한 후 **StoreIndexViewModel** 으로 **모델 클래스**합니다. 또한 선택한 뷰 엔진을 반드시 **Razor**합니다. **추가**를 클릭합니다.

    ![뷰 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image24.png "뷰 추가 대화 상자")

    *뷰 추가 대화 상자*

    **\Views\Store\Index.cshtml** 보기 템플릿 파일을 만들고 열 수 있습니다. 에 제공 된 정보에 따라는 **뷰 추가** 대화 상자는 마지막 단계 템플릿을 증명 보기에에서는 **StoreIndexViewModel** HTML 응답을 생성 하는 데 데이터로 인스턴스. 서식 파일의 상속 함을 알 수는 `ViewPage<musicstore.viewmodels.storeindexviewmodel>` C#입니다.

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a>작업 5-보기 템플릿 업데이트

이 태스크에서는 장르 및 페이지 내에서 이름을의 수를 검색 하려면 마지막 작업에서 만든 보기 서식 파일을 업데이트 합니다.

> [!NOTE]
> @ 구문을 사용 합니다 (이 라 불리 &quot;코드 너&quot;) 보기 템플릿 내에서 코드를 실행 합니다.

1. 에 **Index.cshtml** 파일 내에서 **저장소** 폴더를 해당 코드를 다음과 같이 바꿉니다.

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. 장르 목록에 대해 루프 **StoreIndexViewModel** HTML 만들고 **&lt;ul&gt;** 사용 하 여 나열는 **foreach** 루프 합니다.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. 키를 눌러 **F5** 하는 응용 프로그램을 실행 하 고 찾아볼 **/저장소**합니다. 전달 된 장르 목록이 표시 됩니다는 **StoreIndexViewModel** 에서 개체는 **StoreController** 템플릿 보기에 있습니다.

    ![장르의 목록을 표시 하는 보기](aspnet-mvc-4-fundamentals/_static/image26.png "보기 장르 목록 표시")

    *보기 장르 목록 표시*
4. 브라우저를 닫습니다.

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a>실습 6: 매개 변수를 보기에 사용

연습 3에서 컨트롤러에 매개 변수를 전달 하는 방법을 배웠습니다. 이 연습에서는 뷰 템플릿에 이러한 매개 변수를 사용 하는 방법에 설명 합니다. 이 위해 있습니다 도입 될 것 먼저를 사용자 데이터 및 도메인 논리를 관리 하는 데 도움이 되는 모델 클래스입니다. 또한 인코딩 URL 경로 등의 걱정 하지 않고 ASP.NET MVC 응용 프로그램 내 페이지 링크를 만드는 방법에 설명 합니다.

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a>작업 1-모델 클래스 추가

보기에는 컨트롤러에서 정보를 전달 하기 위한 것 만들어진 Viewmodel 달리 모델 클래스를 포함 하 고 데이터 및 도메인 논리를 관리할 빌드됩니다. 이 작업에서는 이러한 개념을 표현 하는 두 개의 모델 클래스를 추가 합니다: **장르** 및 **앨범**합니다.

1. 아직 열지 않은 경우 시작 **VS Express for Web**
2. 에 **파일** 메뉴 선택 **프로젝트 열기**합니다. 프로젝트 열기 대화 상자에서 찾은 **Source\Ex06 UsingParametersInView\Begin**선택, **Begin.sln** 클릭 **열려**합니다. 또는 계속 진행할 솔루션, 이전 연습을 완료 한 후 가져올 있음을 합니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
3. 추가 **장르** 모델 클래스입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **모델** 폴더에는 **솔루션 탐색기**선택, **추가** 차례로 **새 항목** 옵션입니다. 아래 **코드**, 선택는 **클래스** 항목 및 파일 이름을 *Genre.cs*, 클릭 **추가**합니다.

    ![클래스 추가](aspnet-mvc-4-fundamentals/_static/image27.png "클래스 추가")

    *새 항목 추가*

    ![Genre 모델 클래스를 추가](aspnet-mvc-4-fundamentals/_static/image28.png "장르 모델 클래스를 추가 합니다.")

    *Genre 모델 클래스를 추가 합니다.*
4. 추가 **이름** 장르 클래스에 속성입니다. 이렇게 하려면 다음 코드를 추가 합니다.

    (코드 조각- *기본 ASP.NET MVC 4-Ex6 장르*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. 추가 적으로 동일한 절차는 **앨범** 클래스입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **모델** 폴더에는 **솔루션 탐색기**선택, **추가** 차례로 **새 항목** 옵션입니다. 아래 **코드**, 선택는 **클래스** 항목 및 파일 이름을 *Album.cs*, 클릭 **추가**합니다.
6. 앨범 클래스에 두 개의 속성 추가: **장르** 및 **제목**합니다. 이렇게 하려면 다음 코드를 추가 합니다.

    (코드 조각- *기본 ASP.NET MVC 4-Ex6 앨범*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a>작업 2-는 StoreBrowseViewModel 추가

A **StoreBrowseViewModel** 선택한 장르와 일치 하는 앨범 표시 하려면이 작업에 사용할 수 있습니다. 이 작업에서는이 클래스 만들고 처리 하는 두 개의 속성을 추가 합니다는 **장르** 및 해당 **앨범**의 목록입니다.

1. 추가 **StoreBrowseViewModel** 클래스입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **Viewmodel** 폴더에는 **솔루션 탐색기**선택, **추가** 차례로 **새 항목** 옵션입니다. 아래 **코드**, 선택는 **클래스** 항목 및 파일 이름을 *StoreBrowseViewModel.cs*, 클릭 **추가**합니다.
2. 모델에 대 한 참조를 추가 **StoreBrowseViewModel** 클래스입니다. 이 작업을 수행 하려면 다음 추가 네임 스페이스를 사용 하 여:

    (코드 조각- *기본 ASP.NET MVC 4-Ex6 UsingModel*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. 두 속성을 추가 **StoreBrowseViewModel** 클래스: **장르** 및 **앨범**합니다. 이렇게 하려면 다음 코드를 추가 합니다.

    (코드 조각- *기본 ASP.NET MVC 4-Ex6 ModelProperties*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> 이란 **목록&lt;앨범&gt;**  ?:이 정의 사용 하는 **목록&lt;T&gt;**  형식, 여기서 **T** 제한 하는 이 요소 형식을 **목록** 이 경우 속한 **앨범** (또는 해당 하위 항목 중 하나).
> 
> 클래스 또는 메서드 선언 하 고는 C# 언어의 기능을 클라이언트 코드에 의해 인스턴스화될 때까지 하나 이상의 형식 사양을 연기 하는 클래스와 메서드를 디자인 하는이 기능 호출 **제네릭**합니다.
> 
> **목록&lt;T&gt;**  제네릭 해당는 **ArrayList** 입력 하 고 사용할 수는 **System.Collections.Generic** 네임 스페이스입니다. 사용의 이점 중 하나 **제네릭** 는 형식이 지정 되어 있으므로 불필요 형식 검사에 요소를 캐스팅 하는 등의 작업을 처리 하는 **앨범** 는 와마찬가지로**ArrayList**합니다.

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a>작업 3-새 ViewModel는 StoreController에서 사용 하 여

이 작업에서 수정 됩니다는 **StoreController**의 **찾아보기** 및 **세부 정보** 작업 메서드를 사용 하 여 새 **StoreBrowseViewModel** .

1. 모델 폴더에 대 한 참조를 추가 **StoreController** 클래스입니다. 이 작업을 수행 하려면 확장 된 **컨트롤러** 폴더에는 **솔루션 탐색기** 엽니다는 **StoreController** 클래스. 다음 코드를 추가 합니다.

    (코드 조각- *기본 ASP.NET MVC 4-Ex6 UsingModelInController*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. 대체는 **찾아보기** 사용 하도록 동작 메서드는 **StoreViewBrowseController** 클래스입니다. 더미 데이터로 장르와 두 개의 새로운 앨범 개체 만듭니다 (다음 실습 랩에는 사용 데이터베이스의 실제 데이터). 이 작업을 수행 하려면 대체는 **찾아보기** 메서드를 다음 코드로:

    (코드 조각- *기본 ASP.NET MVC 4-Ex6 BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. 대체는 **세부 정보** 사용 하도록 동작 메서드는 **StoreViewBrowseController** 클래스입니다. 새 만들려는 **앨범** 에 반환 되는 개체는 **보기**합니다. 이 작업을 수행 하려면 대체는 **세부 정보** 메서드를 다음 코드로:

    (코드 조각- *기본 ASP.NET MVC 4-Ex6 DetailsMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a>작업 4-찾아보기 보기 템플릿 추가

이 태스크에서는 추가한는 **찾아보기** 특정 장르에 대 한 앨범 표시 하도록 보기.

1. 새 보기 서식 파일을 만들기 전에 프로젝트를 작성 해야 하는 **뷰 추가** 대화에 대해 알고는 **ViewModel** 클래스를 사용 합니다. 선택 하 여 프로젝트를 빌드합니다는 **빌드** 메뉴 항목 차례로 **빌드 MvcMusicStore**합니다.
2. 추가 **찾아보기** 보기. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **찾아보기** 의 동작 메서드는 **StoreController** 클릭 **뷰 추가**합니다.
3. 에 **뷰 추가** 대화 상자, 뷰 이름 인지 확인 **찾아보기**합니다. 확인의 **강력한 형식의 뷰 만들기** 확인란을 선택 하 고 **StoreBrowseViewModel** 에서 **모델 클래스** 드롭다운입니다. 다른 필드를 기본값으로 둡니다. **추가**를 클릭합니다.

    ![브라우저 보기 추가](aspnet-mvc-4-fundamentals/_static/image29.png "찾아보기 뷰 추가")

    *브라우저 보기를 추가합니다.*
4. 수정 된 **Browse.cshtml** Genre의 정보를 표시 하에 액세스 하는 **StoreBrowseViewModel** 템플릿 보기에 전달 되는 개체입니다. 이 위해 콘텐츠를 다음과 같이 바꿉니다: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>5-응용 프로그램 실행 작업

에서는이 작업을 테스트 하는 **찾아보기** 메서드 앨범에서 검색 된 **찾아보기** 메서드 작업 합니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **찾아보기/저장 /? Genre Disco =** 동작 두 앨범을 반환 하는지 확인 합니다.

    ![저장소 디스코 앨범 검색](aspnet-mvc-4-fundamentals/_static/image30.png "디스코 앨범 저장소를 검색 합니다.")

    *저장소 디스코 앨범 찾아보기*

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a>태스크 6-정보는 특정 앨범 표시

이 작업을 구현 합니다는 **저장소/세부 정보** 특정 앨범에 대 한 정보를 표시 하는 보기입니다. 이 실습 랩에서 앨범에 대 한 표시는 모든 항목에 이미 포함 되어는 **보기** 템플릿. 따라서 만드는 대신 한 **StoreDetailsViewModel** 클래스 현재 사용 하 여 **StoreBrowseViewModel** 앨범을 전달 하는 서식 파일.

1. Visual Studio 창에 반환 하는 데 필요한 경우 브라우저를 닫습니다. 새로 추가 **세부 정보** 에 대 한 보기 된 **StoreController**의 **세부 정보** 동작 메서드. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **세부 정보** 에서 메서드는 **StoreController** 클래스 및 클릭 **뷰 추가**합니다.
2. 에 **뷰 추가** 대화 상자에서 되어 있는지 확인은 **뷰 이름** 은 **세부 정보**합니다. 확인의 **강력한 형식의 뷰 만들기** 확인란을 선택 하 고 **앨범** 에서 **모델 클래스** 드롭 다운 합니다. 다른 필드를 기본값으로 둡니다. **추가**를 클릭합니다. 만들고 열려면는 **\Views\Store\Details.cshtml** 파일입니다.

    ![세부 정보 뷰 추가](aspnet-mvc-4-fundamentals/_static/image31.png "추가 세부 정보 보기")

    *추가 세부 정보 보기*
3. 수정 된 **Details.cshtml** 앨범의 정보를 표시 하는 파일에 액세스 하는 **앨범** 템플릿 보기에 전달 되는 개체입니다. 이 위해 콘텐츠를 다음과 같이 바꿉니다: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>7-응용 프로그램 실행 작업

에서는이 작업을 테스트 하는 **세부 정보** 에서 앨범의 정보를 검색 하는 보기는 **동작에 자세히 설명** 메서드.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 시작 날짜는 **홈** 페이지. URL을 변경 **/Store/Details/5** 앨범의 정보를 확인 합니다.

    ![앨범 세부 정보를 검색](aspnet-mvc-4-fundamentals/_static/image32.png "앨범 세부 정보를 검색 합니다.")

    *앨범 세부 정보를 검색합니다.*

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a>태스크 8-페이지 간 링크 추가

이 작업을 적절 한 모든 장르 이름에 링크가 있으며이를 저장소 보기의 링크를 추가 합니다 **/저장소/찾아보기** URL입니다. 이런 방식이으로, 예를 들어는 장르에서 클릭 **Disco**, 검색을 시작 합니다 **/저장소/찾아보기? 장르 Disco =** URL입니다.

1. Visual Studio 창에 반환 하는 데 필요한 경우 브라우저를 닫습니다. 업데이트는 **인덱스** 페이지에 대 한 링크를 추가 하는 **찾아보기** 페이지. 이 수행 하는 **솔루션 탐색기** 확장는 **뷰** 폴더를 하면 **저장소** 폴더를 두 번 클릭은 **Index.cshtml** 페이지.
2. 선택한 장르를 나타내는 찾아보기 보기에 대 한 링크를 추가 합니다. 이 작업을 수행 하려면 내에서 강조 표시 된 다음 코드를 대체는 **&lt;li&gt;** 태그: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > 또 다른 방법은 다음과 같은 코드 페이지에 직접 연결 합니다.
   > 
   > &lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;
   > 
   > 이 방법은 작동 하지만 하드 코드 된 문자열에 따라 다릅니다. 나중에 컨트롤러를 바꾸면이 명령을 수동으로 변경 해야 합니다. 사용 하는 것이 더 좋은 것는 **HTML 도우미** 메서드. ASP.NET MVC 등의 작업에 사용할 수 있는 HTML 도우미 메서드를 포함 합니다. **Html.ActionLink()** 도우미 메서드를 사용 하면 HTML 만들려는 쉽게 **&lt;는&gt;** 링크, URL 경로 URL로 인코딩된 제대로 확인 합니다.
   > 
   > Htlm.ActionLink 여러 오버 로드가 있습니다. 이 연습에서는 세 개의 매개 변수 하나를 사용 합니다.
   > 
   > 1. 링크 텍스트는 장르 이름이 표시 됩니다
   > 2. 컨트롤러 동작 이름 (**찾아보기**)
   > 3. 경로 이름을 둘 다 지정 하는 매개 변수 값 (**장르**)과 값 (**장르 이름**)

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a>태스크 9-응용 프로그램 실행

에서는이 작업을 테스트 각각 적절 한 링크와 함께 표시 되도록 **/저장소/찾아보기** URL입니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **/저장소** 각각을 적절 한 링크를 확인 하려면 **/저장소/찾아보기** URL입니다.

    ![찾아보기 페이지에 대 한 링크와 장르 검색](aspnet-mvc-4-fundamentals/_static/image33.png "찾아보기 페이지에 대 한 링크와 장르 검색")

    *찾아보기 페이지에 대 한 링크와 장르 검색*

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a>태스크 10-값을 전달 하기를 사용 하 여 동적 ViewModel 컬렉션

이 작업에서는 값을 전달 하는 컨트롤러와 뷰 간에 모델에 변경 하지 않고 단순 하 고 강력한 방법에 설명 합니다. 컬렉션을 제공 하는 ASP.NET MVC 4 &quot;ViewModel&quot;, 모든 동적 값에 할당 및 컨트롤러와도 뷰 내에서 액세스할 수 있으며 합니다.

ViewBag 동적 컬렉션의 목록을 전달 하는 데 사용할 이제 &quot; **장르 별모양** &quot; 보기로 컨트롤러에서 합니다. 인덱스 저장소 보기를 액세스할 **ViewModel** 정보를 표시 합니다.

1. Visual Studio 창에 반환 하는 데 필요한 경우 브라우저를 닫습니다. 열기 **StoreController.cs** 수정 **인덱스** 목록을 만드는 메서드를 ViewModel 컬렉션으로 장르 별모양:

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > 구문을 사용할 수도 있습니다 **ViewBag [&quot;Starred&quot;]** 속성에 액세스할 수 있습니다.
2. 별표 아이콘 **&quot;starred.png&quot;** 에 포함 된 **Source\Assets\Images** 이 랩의 폴더입니다. 응용 프로그램을 추가 하기 위해 자신의 콘텐츠를 끌어 한 **Windows 탐색기** 창에는 **솔루션 탐색기** Visual Web Developer Express, 아래와 같이에서:

    ![솔루션에 추가 별 이미지](aspnet-mvc-4-fundamentals/_static/image34.png "솔루션 별 이미지 추가")

    *솔루션에 별 이미지 추가*
3. 보기를 열 **Store/Index.cshtml** 콘텐츠를 수정 하 고 있습니다. 읽기 합니다는 &quot;별모양&quot; 속성에는 **ViewBag** 컬렉션 현재 장르 이름이 목록에 게 요청 합니다. 이 경우 장르 링크 오른쪽에서 별 모양 아이콘을 표시 됩니다.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a>태스크 11-응용 프로그램 실행

이 작업에서는 별표 장르 별 모양 아이콘을 표시를 테스트 합니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 시작 날짜는 **홈** 페이지. URL을 변경 **/저장소** 각 기능 갖춘된 장르 respecting 레이블에 있는지 확인 하려면:

    ![찾아보기 장르 별표 요소 기능이](aspnet-mvc-4-fundamentals/_static/image35.png "별표 요소와 장르 검색")

    *장르 별표 요소 검색*

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a>7 연습: ASP.NET MVC 4 새 템플릿 주위 랩

이 연습에서는 탐색 ASP.NET MVC 4 프로젝트 템플릿, 향상 된 새 서식 파일의 가장 관련 기능 살펴보겠습니다.

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a>작업 1: 탐색 ASP.NET MVC 4 인터넷 응용 프로그램 템플릿

1. 아직 열지 않은 경우 시작 **VS Express for Web**
2. 선택 된 **파일 | 새로 만들기 | 프로젝트** 메뉴 명령입니다. 에 **새 프로젝트** 대화 상자에서 선택 된 **Visual C# | 웹** 서식 파일의 왼쪽된 창에서 트리를 선택 하 고는 **ASP.NET MVC 4 웹 응용 프로그램**합니다. **이름** 프로젝트 *MusicStore* 하 고 업데이트는 **솔루션 이름** 를 *시작*, 다음 위치를 선택 (또는 기본값을 그대로 적용)를 클릭 하 고 **확인** .

    ![새 ASP.NET MVC 4 프로젝트를 만드는](aspnet-mvc-4-fundamentals/_static/image36.png "새 ASP.NET MVC 4 프로젝트 만들기")

    *새 ASP.NET MVC 4 프로젝트 만들기*
3. 에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서는 **인터넷 응용 프로그램** 프로젝트 템플릿과 클릭 **확인**합니다. 표시 뷰 엔진으로 Razor 또는 ASPX 중 하나를 선택할 수 있습니다.

    ![새 ASP.NET MVC 4 인터넷 응용 프로그램을 만드는](aspnet-mvc-4-fundamentals/_static/image37.png "새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기")

    *새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기*

    > [!NOTE]
    > ASP.NET MVC 3에서 razor 구문이 도입 되었습니다. 목표의 문자 및 fast 및 워크플로 코딩 하는 유체 파일에 필요한 키 입력의 수를 최소화 하는 것입니다. 기존 C# /VB 또는 다른 razor 활용 하 여 언어 기술을 놀라운 HTML 생성 워크플로 수 있도록 하는 템플릿 태그 구문을 제공 합니다.
4. 키를 눌러 **F5** 솔루션을 실행 하 고 갱신 된 서식 파일을 표시 합니다. 다음 기능을 사용해 확인할 수 있습니다.

    1. **최신 스타일 템플릿**

        서식 파일 갱신 된, 더 많은 현대 수준의 스타일을 제공 합니다.

        ![ASP.NET MVC 4 맞게 스타일을 다시 템플릿](aspnet-mvc-4-fundamentals/_static/image38.png "맞게 템플릿 스타일을 다시 ASP.NET MVC 4")

        *ASP.NET MVC 4 맞게 스타일을 다시 템플릿*
    2. **자동 선택 렌더링**

        체크 아웃 브라우저 창 크기 조정 고 페이지 레이아웃 새 창 크기를 동적으로 반응 방법을 확인 합니다. 이러한 템플릿은 자동 선택 렌더링 기술을 사용 하 여 사용자 지정 하지 않고 데스크톱 및 모바일 플랫폼에서 모두 올바르게 렌더링 합니다.

        ![다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿에서](aspnet-mvc-4-fundamentals/_static/image39.png "다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿")

        *다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿*
5. 디버거를 중지 하려면 Visual Studio로 되돌아가려면 브라우저를 닫습니다.
6. 이제 솔루션을 탐색 하 고 체크 아웃 프로젝트 템플릿에 있는 ASP.NET MVC 4에서 도입 된 새로운 기능 중 일부를 수 있습니다.

    ![ASP.NET mvc 4-인터넷-응용 프로그램-프로젝트-템플릿을](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿을")

    *ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿*

   1. **HTML5 태그**

       예를 들어 열린 새 테마 마크업 알아보려면 템플릿 보기 찾아보기 **About.cshtml** 내의 볼 **홈** 폴더입니다.

       ![Razor 및 HTML5 태그를 사용 하 여 새로운 템플릿을](aspnet-mvc-4-fundamentals/_static/image41.png "Razor 및 HTML5 태그를 사용 하 여 새 서식 파일")

       *Razor 및 HTML5 태그를 사용 하 여 새 서식 파일*
   2. **포함 된 JavaScript 라이브러리**

      1. **jQuery**: jQuery HTML 문서 통과, 이벤트 처리, 애니메이션, 및 Ajax 상호 작용을 간소화 합니다.
      2. **jQuery UI**:이 라이브러리는 낮은 수준의 상호 작용 및 애니메이션 효과 고급 및 스타일 widgets, jQuery JavaScript 라이브러리를 기반으로 빌드된에 대 한 추상화를 제공 합니다.

         > [!NOTE]
         > JQuery 및 jQuery UI에 대해 알아볼 수 있습니다에 [ [ http://docs.jquery.com/ ](http://docs.jquery.com/) ](http://docs.jquery.com/)합니다.
      3. **KnockoutJS**: ASP.NET MVC 4의 기본 서식 파일에 포함 되어 이제 **KnockoutJS**, JavaScript 및 HTML을 사용 하 여 풍부 하 고 응답성 높은 웹 응용 프로그램을 만들 수 있는 JavaScript MVVM 프레임 워크입니다. 와 같은 ASP.NET MVC 3, jQuery 및 jQuery UI 라이브러리에에서도 나와 ASP.NET MVC 4입니다.

          > [!NOTE]
          > 이 링크에 KnockOutJS 라이브러리에 대 한 자세한 정보를 얻을 수 있습니다: [ http://learn.knockoutjs.com/ ](http://learn.knockoutjs.com/)합니다.
      4. **Modernizr**:이 라이브러리에서는 호환성이 사이트 이전 브라우저 HTML5 및 CSS3 기술을 사용할 때 자동으로 실행 합니다.

          > [!NOTE]
          > 이 링크에 Modernizr 라이브러리에 대 한 자세한 정보를 얻을 수 있습니다: [ http://www.modernizr.com/ ](http://www.modernizr.com/)합니다.
   3. **SimpleMembership 솔루션에 포함**

       SimpleMembership는 이전 ASP.NET 역할 및 멤버 자격 공급자 시스템에 대 한 대체 값으로 설계 되었습니다. 도와 주는 개발자가 보안 웹 페이지를 보다 융통성 있는 방식으로 여러 가지 새로운 기능이 있음

       인터넷 템플릿을 이미 설정한 SimpleMembership를 통합 하는 몇 가지, OAuthWebSecurity (에 대 한 OAuth 계정 등록, 로그인, 관리, 등) 및 웹 보안을 사용 하 여 AccountController 준비 예를 들어 합니다.

       ![솔루션에 포함 된 SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership 솔루션에 포함")

       *SimpleMembership 솔루션에 포함*

       > [!NOTE]
       > 에 대 한 자세한 내용을 보려면 [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) MSDN에 있습니다.

> [!NOTE]
> 다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수는 또한 [부록 b: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixB)합니다.


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩을 완료 하 여 ASP.NET MVC의 기본적인 사항을 배웠습니다.

- MVC 응용 프로그램 및 조작 방법을의 핵심 요소
- ASP.NET MVC 응용 프로그램을 만드는 방법
- URL 및 쿼리 문자열을 통해 전달 된 추가 하 고 매개 변수를 처리 하기 위해 컨트롤러를 구성 하는 방법
- 공통 HTML 콘텐츠, 모양 및 HTML 콘텐츠를 표시 하려면 보기 서식 파일을 개선 하는 스타일 시트에 대 한 템플릿을 설정 하는 레이아웃 마스터 페이지를 추가 하는 방법
- 동적 정보를 표시 하려면 템플릿 보기에 속성을 전달 하기 위한 ViewModel 패턴을 사용 하는 방법
- 템플릿 보기에서에서 컨트롤러에 전달 된 매개 변수를 사용 하는 방법
- ASP.NET MVC 응용 프로그램 내 페이지에 대 한 링크를 추가 하는 방법
- 추가 하 고 보기에서 동적 속성을 사용 하는 방법
- ASP.NET MVC 4 프로젝트 템플릿의 향상 된 기능

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 a: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여 **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)**. 다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.

1. 로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다. 또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Windows Azure SDK와</em>&quot;합니다.
2. 클릭 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.

    ![Visual Studio Express 설치](aspnet-mvc-4-fundamentals/_static/image43.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건 동의](aspnet-mvc-4-fundamentals/_static/image44.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-fundamentals/_static/image45.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **마침**합니다.

    ![설치 완료](aspnet-mvc-4-fundamentals/_static/image46.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.

    ![웹 타일에 대 한 VS Express](aspnet-mvc-4-fundamentals/_static/image47.png)

    *웹 타일에 대 한 VS Express*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>부록 b: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

이 부록에서는 Windows Azure 관리 포털에서 새 웹 사이트를 만들고 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하기 위해 랩에서 수행 하 여 가져온 응용 프로그램을 게시 하는 방법을 보여줍니다.

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>작업 1-Windows에서 새 웹 사이트를 만드는 Azure 포털

1. 이동 하 여 [Windows Azure 관리 포털](https://manage.windowsazure.com/) 구독에 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.

    > [!NOTE]
    > Windows Azure를 무료로 10 개 ASP.NET 웹 사이트를 호스트 하 고 트래픽이 증가 됨을 확장 한 다음 사용할 수 있습니다. 등록할 수 [여기](http://aka.ms/aspnet-hol-azure)합니다.

    ![Windows Azure 포털에 로그온](aspnet-mvc-4-fundamentals/_static/image48.png "Windows Azure 포털에 로그인")

    *Windows Azure 관리 포털에 로그온*
2. 클릭 **새로** 명령 모음에서 합니다.

    ![새 웹 사이트를 만드는](aspnet-mvc-4-fundamentals/_static/image49.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. 클릭 **계산** | **웹 사이트**합니다. 그런 다음 선택 **빠른 생성** 옵션입니다. 새 웹 사이트에 대 한 사용 가능한 URL을 입력 하 고 클릭 **웹 사이트 만들기**합니다.

    > [!NOTE]
    > Windows Azure 웹 사이트는 호스트를 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램입니다. 빨리 만들기 옵션을 사용 하면 완성 된 웹 응용 프로그램을 Windows Azure 웹 사이트에서 포털 외부에 배포할 수 있습니다. 데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](aspnet-mvc-4-fundamentals/_static/image50.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.
5. 웹 사이트가 만들어지면 아래 링크를 클릭 하 고 **URL** 열입니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트를 찾아](aspnet-mvc-4-fundamentals/_static/image51.png "새 웹 사이트를 검색 합니다.")

    *새 웹 사이트를 검색합니다.*

    ![실행 중인 웹 사이트](aspnet-mvc-4-fundamentals/_static/image52.png "실행 중인 웹 사이트")

    *실행 중인 웹 사이트*
6. 포털로 돌아가서 아래에서 웹 사이트의 이름을 클릭는 **이름** 관리 페이지를 표시 하는 열입니다.

    ![웹 사이트 관리 페이지 열기](aspnet-mvc-4-fundamentals/_static/image53.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. 에 **대시보드** 페이지의 **눈에 보는** 섹션에서 클릭는 **게시 프로필 다운로드** 링크 합니다.

    > [!NOTE]
    > *게시 프로필* 각각의 활성화 된 게시 방법에 대 한 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 데 필요한 정보가 모두 포함 되어 있습니다. 게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열이 포함 되어 있습니다. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 읽는 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 합니다.

    ![게시 프로필 다운로드 웹 사이트](aspnet-mvc-4-fundamentals/_static/image54.png "게시 프로필 다운로드 웹 사이트")

    *게시 프로필 다운로드 웹 사이트*
8. 알려진된 위치에 게시 프로필 파일을 다운로드 합니다. 더 이상이 연습에서는 Visual Studio에서 웹 응용 프로그램 Windows Azure 웹 사이트를 게시 하려면이 파일을 사용 하는 방법을 표시 됩니다.

    ![게시 프로필 파일을 저장](aspnet-mvc-4-fundamentals/_static/image55.png "게시 프로필 저장")

    *게시 프로필 파일을 저장합니다.*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL Server를 활용 하는 경우 데이터베이스를 SQL 데이터베이스 서버 만들기 해야 합니다. SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 태스크를 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하기 위해 SQL 데이터베이스 서버를 해야 합니다. Windows Azure 관리 포털에서 구독의 SQL 데이터베이스 서버를 볼 수 있습니다 **Sql 데이터베이스** | **서버** | **서버 대시보드**합니다. 만든 서버 없는 경우 수행 하 여 만들 수 있습니다는 **추가** 명령 모음에서 단추입니다. 기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**, 다음 작업에 사용 됩니다. 만들지 마십시오 데이터베이스 아직 대로 이후 단계에서 생성 됩니다.

    ![SQL 데이터베이스 서버 대시보드](aspnet-mvc-4-fundamentals/_static/image56.png "SQL 데이터베이스 서버 대시보드")

    *SQL 데이터베이스 서버 대시보드*
2. 다음 태스크에서는 서버 목록에 사용자의 로컬 IP 주소를 포함 해야 이러한 이유로 Visual Studio에서 데이터베이스 연결을 테스트 **허용 IP 주소**합니다. 작업을 수행 하려면 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여넣습니다는 **시작 IP 주소** 및 **끝IP주소** 클릭 하 고 텍스트 상자는 ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) 단추입니다.

    ![클라이언트 IP 주소를 추가합니다.](aspnet-mvc-4-fundamentals/_static/image58.png)

    *클라이언트 IP 주소를 추가합니다.*
3. 한 번는 **클라이언트 IP 주소** 허용된 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 하 여 변경 사항을 확인 합니다.

    ![변경 확인](aspnet-mvc-4-fundamentals/_static/image59.png)

    *변경 확인*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션으로 돌아갑니다. 에 **솔루션 탐색기**웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.

    ![응용 프로그램을 게시](aspnet-mvc-4-fundamentals/_static/image60.png "응용 프로그램을 게시")

    *웹 사이트를 게시*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필 가져오기](aspnet-mvc-4-fundamentals/_static/image61.png "게시 프로필 가져오기")

    *게시 프로필 가져오기*
3. 클릭 **연결 확인**합니다. 유효성 검사가 완료 되 면 클릭 **다음**합니다.

    > [!NOTE]
    > 연결 유효성 검사 단추 옆에 표시 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.

    ![연결 유효성 검사](aspnet-mvc-4-fundamentals/_static/image62.png "연결 유효성 검사")

    *연결 유효성 검사*
4. 에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추 클릭 (즉, **DefaultConnection**).

    ![웹 배포 구성](aspnet-mvc-4-fundamentals/_static/image63.png "웹 배포 구성")

    *웹 배포 구성*
5. 다음과 같이 데이터베이스 연결을 구성 합니다.

   - 에 **서버 이름** SQL 데이터베이스 서버 URL 사용 하 여 입력 된 *tcp:* 접두사입니다.
   - **사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 서버 관리자 로그인 암호를 입력 합니다.
   - 예를 들어 새 데이터베이스 이름 입력: *MVC4SampleDB*합니다.

     ![대상 연결 문자열 구성](aspnet-mvc-4-fundamentals/_static/image64.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 다음 **확인**을 클릭합니다. 데이터베이스를 만들려는 대화 상자가 나타나면 **예**합니다.

    ![데이터베이스를 만드는](aspnet-mvc-4-fundamentals/_static/image65.png "데이터베이스 문자열 만들기")

    *데이터베이스를 만드는 중*
7. Windows azure에서 SQL 데이터베이스에 연결 하기 위해 사용할 연결 문자열은 기본 연결 텍스트 상자 내에서 표시 됩니다. **다음**을 클릭합니다.

    ![SQL 데이터베이스를 가리키는 연결 문자열](aspnet-mvc-4-fundamentals/_static/image66.png "SQL 데이터베이스를 가리키는 연결 문자열")

    *SQL 데이터베이스를 가리키는 연결 문자열*
8. 에 **미리 보기** 페이지 **게시**합니다.

    ![웹 응용 프로그램을 게시](aspnet-mvc-4-fundamentals/_static/image67.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.

    ![Windows Azure에 게시 된 응용 프로그램](aspnet-mvc-4-fundamentals/_static/image68.png "Windows Azure에 게시 된 응용 프로그램")

    *Windows Azure에 게시 된 응용 프로그램*

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>부록 c: 코드 조각을 사용 하 여

코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다. 랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.

![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](aspnet-mvc-4-fundamentals/_static/image69.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")

*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*

***키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드를 삽입 하려는 위치에 커서를 놓습니다.
2. 공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.
3. IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.
4. 올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).
5. 커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.

![코드 조각 이름을 입력 하기 시작](aspnet-mvc-4-fundamentals/_static/image70.png "조각 이름을 입력 하기 시작")

*코드 조각 이름을 입력 하기 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각 선택](aspnet-mvc-4-fundamentals/_static/image71.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")

*Tab 키를 눌러 강조 표시 된 코드 조각 선택*

![확장 하 고 Tab 키를 눌러 다시 코드 조각](aspnet-mvc-4-fundamentals/_static/image72.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")

*확장 하 고 Tab 키를 눌러 다시 코드 조각*

***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1입니다. 코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.

1. 선택 **조각 삽입** 이어서 **내 코드 조각**합니다.
2. 클릭 하 여 목록에서 관련 조각을 선택 합니다.

![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-fundamentals/_static/image73.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")

*코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*

![클릭 하 여 목록에서 관련 조각을 선택](aspnet-mvc-4-fundamentals/_static/image74.png "클릭 하 여 목록에서 관련 조각을 선택")

*클릭 하 여 목록에서 관련 조각을 선택합니다*
