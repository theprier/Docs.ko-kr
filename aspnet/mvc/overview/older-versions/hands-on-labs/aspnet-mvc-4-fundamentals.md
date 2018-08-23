---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 기본 사항 | Microsoft Docs
author: rick-anderson
description: 이 실습 랩에서 MVC (Model View Controller) Music Store 자습서 응용 프로그램을 소개 하 고 ASP.NET MV를 사용 하는 방법을 단계별로 설명를 기반으로 하는 중...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: d8e837a5d56871d271590859c2e82336111cc87a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836292"
---
# <a name="aspnet-mvc-4-fundamentals"></a>ASP.NET MVC 4 기본 사항

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트 다운로드](https://aka.ms/webcamps-training-kit)

이 실습 랩에서 MVC (Model View Controller) Music Store 자습서 응용 프로그램을 소개 하 고 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명를 기반으로 합니다. 간단 하 게, 연구소에서 배웁니다 함께 이러한 기술을 사용 하는 아직 power 합니다. 간단한 응용 프로그램을 시작 하 고 모든 기능을 갖춘 ASP.NET MVC 4 웹 응용 프로그램을 수 있을 때까지 빌드합니다 됩니다.

이 랩에서 ASP.NET MVC 4를 사용 하 여 작동합니다.

자습서 응용 프로그램의 ASP.NET MVC 3 버전을 탐색 하려는 경우에서 찾을 수 있습니다 [MVC 음악 스토어](https://github.com/evilDave/MVC-Music-Store)합니다.

이 실습에서는 개발자 HTML 및 JavaScript와 같은 웹 개발 기술을 환경에 있는지 가정 합니다.

> [!NOTE]
> 웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다. 이 랩에 특정 프로젝트에서 제공 됩니다 [ASP.NET MVC 4 기본 사항](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)합니다.

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a>Music Store 응용 프로그램

이 랩에서 전체에서 빌드되는 Music Store 웹 응용 프로그램 구성 세 가지 주요 부분이: 쇼핑, 체크 아웃 및 관리 합니다. 방문자 장르별로 앨범을 찾아보기, 앨범 자신의 카트에 추가 하 고, 선택 검토 하 고 마지막으로 로그인 하 고 순서를 완료 하는 결제로 진행 하는 일을 할 수 있습니다. 또한 저장소 관리자 주요 속성 뿐만 아니라 사용 가능한 앨범을 관리할 수 없게 됩니다.

![Music Store 화면](aspnet-mvc-4-fundamentals/_static/image1.png "Music Store 화면")

*Music Store 화면*

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a>ASP.NET MVC 4 Essentials

Music Store 응용 프로그램이 사용 하 여 빌드됩니다 **컨트롤러 MVC (Model View)**, 응용 프로그램을 세 가지 주요 구성 요소를 구분 하는 아키텍처 패턴:

- **모델**: 모델 개체는 도메인 논리를 구현 하는 응용 프로그램의 구성 요소입니다. 종종 모델 개체도 검색 및 데이터베이스에서 모델 상태를 저장 합니다.
- **보기:** 뷰는 응용 프로그램의 UI (사용자 인터페이스)를 표시 하는 구성 요소입니다. 일반적으로이 UI는 모델 데이터에서 생성 됩니다. 예로 앨범 개체의 현재 상태에 따라 드롭다운 목록과 텍스트 상자를 표시 하는 앨범의 편집 보기 것입니다.
- **컨트롤러:** 컨트롤러는, 사용자 상호 작용을 처리 하 고, 모델을 조작 하 고, 궁극적으로 UI를 렌더링 하는 뷰를 선택 하는 구성 요소입니다. MVC 응용 프로그램에서 보기는 정보만 표시합니다. 컨트롤러가 사용자 입력 및 상호 작용을 처리하고 응답합니다.

MVC 패턴을 사용 하면 이러한 요소 간의 느슨한 결합을 제공 하는 동안 응용 프로그램 (입력된 논리, 비즈니스 논리 및 UI 논리)의 다양 한 측면을 구분 하는 응용 프로그램을 만들 수 있습니다. 이러한 분리를 통해 한 번에 구현의 하나의 측면에 초점을 맞출 수 있도록 응용 프로그램을 빌드할 때 복잡성을 관리할 수 있습니다. 또한 MVC 패턴에서는 또한 응용 프로그램을 만들기 위한 테스트 기반 개발 (TDD)을 사용 하도록 권장 하는 응용 프로그램을 테스트 하기가 쉽습니다.

합니다 **ASP.NET MVC** 프레임 워크는 ASP.NET MVC 기반 웹 응용 프로그램을 만들기 위한 ASP.NET Web Forms 패턴에 대안을 제공 합니다. 합니다 **ASP.NET MVC** 프레임 워크는 간단 하 고 가볍고 테스트가 용이한 프레젠테이션 프레임 워크는 (Web forms 기반 응용 프로그램과 마찬가지로)은 같은 마스터 페이지 및 멤버 자격 기반 기존 ASP.NET 기능과 통합 .NET core framework의 모든 기능을 얻게 되므로 인증 합니다. 이 이미 잘 알고 있다면 ASP.NET Web Forms를 사용 하 여 이미 사용 하는 모든 라이브러리도 ASP.NET MVC 4에서 사용할 수 있으므로 유용 합니다.

또한 MVC 응용 프로그램의 세 가지 주요 구성 요소 간의 느슨한 결합은 병렬 개발을 촉진 하는 수도 있습니다. 예를 들어 한 개발자 보기에서 작업할 수 있습니다, 두 번째 개발자는 컨트롤러 논리를 작업할 수 있습니다 및 세 번째 개발자는 모델의 비즈니스 논리에 집중할 수 있습니다.

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 학습할 방법:

- Music Store 응용 프로그램 자습서를 기반으로 하는 처음부터 ASP.NET MVC 응용 프로그램 만들기
- 사이트 및 해당 주요 기능을 검색 하는 것에 대 한 홈 페이지 Url을 처리 하는 컨트롤러 추가
- 해당 스타일과 함께 표시 되는 내용에 맞게 뷰 추가
- 포함 하 고 데이터 및 도메인 논리를 관리할 모델 클래스 추가
- 뷰 모델 패턴을 사용 하 여 보기 템플릿은 컨트롤러 작업에서 정보를 전달
- 인터넷 응용 프로그램에 대 한 ASP.NET MVC 4 새 템플릿 탐색

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (읽을 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은)

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>설정

**설치 코드 조각**

편의 위해이 랩에서 함께 관리 하려는 코드의 대부분 제품은 Visual Studio 코드 조각입니다. 설치를 실행 하는 코드 조각 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.

이 문서의 부록 참조할 수 있습니다 사용 하는 방법을 알아보려면 원하는 고 Visual Studio 코드 조각을 사용 하 여 잘 모르는 경우 &quot; [부록 c:를 사용 하 여 코드 조각](#AppendixC)&quot;합니다.

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습으로 구성 됩니다.

1. [연습 1: MusicStore ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기](#Exercise1)
2. [연습 2: 컨트롤러 만들기](#Exercise2)
3. [연습 3: 컨트롤러에 매개 변수 전달](#Exercise3)
4. [실습 4: 뷰 만들기](#Exercise4)
5. [실습 5: 뷰 모델 만들기](#Exercise5)
6. [실습 6:를 사용 하 여 매개 변수 보기](#Exercise6)
7. [실습 7: ASP.NET MVC 4에 대 한 새 템플릿 주위의 랩](#Exercise7)

> [!NOTE]
> 각 실습 동반 되는 **최종** 연습을 완료 한 후 가져와야 결과 솔루션이 포함 된 폴더입니다. 이 연습을 진행 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.


이 랩을 완료 하기 위한 예상 시간: **60 분**합니다.

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a>연습 1: MusicStore ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기

이 연습에서는 해당 기본 폴더 조직 뿐만 아니라 웹에 대 한 Visual Studio 2012 Express에서 ASP.NET MVC 응용 프로그램을 만드는 방법에 배웁니다. 또한 새 컨트롤러를 추가 하 고 간단한 문자열을 응용 프로그램의 홈 페이지에 표시할 수 있도록 하는 방법을 배웁니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a>작업 1-ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기

1. 이 태스크에서는 MVC Visual Studio 템플릿을 사용 하 여 빈 ASP.NET MVC 응용 프로그램 프로젝트를 만들게 됩니다. 시작 **VS Express for Web**합니다.
2. **파일** 메뉴에서 **새 프로젝트**를 클릭합니다.
3. 에 **새 프로젝트** 대화 상자 선택 합니다 **ASP.NET MVC 4 웹 응용 프로그램** 프로젝트 아래에 있는 형식을 **Visual C#** **웹** 템플릿 목록입니다.
4. 변경 된 **이름을** 하 *MvcMusicStore*합니다.
5. 새 내부 솔루션의 위치를 설정 **시작할** 예를 들어가 연습이에서는 원본 폴더의 폴더 **[YOUR HOL 경로] \Source\Ex01-CreatingMusicStoreProject\Begin**합니다. **확인**을 클릭합니다.

    ![새 프로젝트 대화 상자를 만듭니다](aspnet-mvc-4-fundamentals/_static/image2.png "새 프로젝트 대화 상자 만들기")

    *새 프로젝트 대화 상자 만들기*
6. 에 **새 ASP.NET MVC 4 프로젝트** 대화 상자 선택을 **기본** 템플릿 되어 있는지 확인 합니다 **뷰 엔진** 선택한 **Razor**합니다. **확인**을 클릭합니다.

    ![새 ASP.NET MVC 4 프로젝트 대화 상자](aspnet-mvc-4-fundamentals/_static/image3.png "새 ASP.NET MVC 4 프로젝트 대화 상자")

    *새 ASP.NET MVC 4 프로젝트 대화 상자*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a>작업 2-솔루션 구조를 탐색 합니다.

ASP.NET MVC 프레임 워크는 MVC 패턴을 지 원하는 웹 응용 프로그램을 만들 수 있도록 Visual Studio 프로젝트 템플릿이 포함 되어 있습니다. 이 템플릿은 필요한 폴더, 항목 템플릿 및 구성 파일 항목을 사용 하 여 새 ASP.NET MVC 웹 응용 프로그램을 만듭니다.

이 작업에서는 관련 된 요소를 이해 하는 솔루션 구조 및 해당 관계를 검사 합니다. 기본적으로 ASP.NET MVC 프레임 워크를 사용 하기 때문에 모든 ASP.NET MVC 응용 프로그램에 다음 폴더가 포함 된 &quot;구성 보다 규칙&quot; 방식과 몇 가지 기본 가정이 폴더 이름에 따라 규칙입니다.

1. 프로젝트가 생성 되 면 오른쪽에 있는 솔루션 탐색기에서 만든 폴더 구조를 검토 합니다.

    ![솔루션 탐색기에서 ASP.NET MVC 폴더 구조](aspnet-mvc-4-fundamentals/_static/image4.png "솔루션 탐색기에서 ASP.NET MVC 폴더 구조")

    *솔루션 탐색기에서 ASP.NET MVC 폴더 구조*

   1. **컨트롤러**합니다. 이 폴더는 컨트롤러 클래스가 포함 됩니다. MVC 기반 응용 프로그램에서 컨트롤러는 최종 사용자 상호 작용을 처리 하 고 모델을 조작 하 고 궁극적으로 UI를 렌더링 하는 뷰를 선택 하는 일을 담당 합니다.

       > [!NOTE]
       > MVC 프레임 워크를 위해서는 끝나야 모든 컨트롤러의 이름이 &quot;컨트롤러&quot;-HomeController, LoginController 또는 ProductController 예를 들어 있습니다.
   2. **모델**합니다. 이 폴더는 MVC 웹 응용 프로그램에 대 한 응용 프로그램 모델을 나타내는 클래스에 대 한 제공 됩니다. 일반적으로 개체 및 데이터 저장소와 상호 작용 하기 위한 논리를 정의 하는 코드가 포함 됩니다. 일반적으로 실제 모델 개체는 별도 클래스 라이브러리에 있게 됩니다. 그러나 새 응용 프로그램을 만들면 클래스를 포함 하 고 개발 주기에서 나중에 별도 클래스 라이브러리로 이동할 수 있습니다.
   3. **뷰**합니다. 이 폴더에 보기를 응용 프로그램의 사용자 인터페이스를 표시 하는 일을 담당 하는 구성 요소에 대 한 권장 되는 위치입니다. 보기는.aspx,.ascx,.cshtml 및.master 파일 뷰 렌더링에 관련 된 다른 파일 외에도 사용 합니다. 각 컨트롤러에 대 한 폴더를 포함 하는 views 폴더 컨트롤러 이름 접두사를 사용 하 여 폴더의 이름은입니다. 예를 들어 라는 컨트롤러를 있다면 **HomeController**, Views 폴더에 Home 이라는 폴더가 포함 됩니다. 기본적으로 ASP.NET MVC 프레임 워크에서는 뷰를 찾습니다 Views\controllerName 폴더에서 요청 된 뷰 이름 사용 하 여.aspx 파일 (**[ControllerName] [작업] 보기.aspx**) 또는 (**뷰 [ControllerName] [작업].cshtml**) Razor 보기에 대 한 합니다.

      > [!NOTE]
      > MVC 웹 응용 프로그램을 사용 하 여 앞에서 설명한 폴더 외에도 합니다 **Global.asax** 전역 URL 라우팅 설정 하기 위해 파일의 기본값을 사용 하는 **Web.config** 응용 프로그램을 구성 파일입니다.

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a>작업 3-HomeController를 추가 합니다.

MVC 프레임 워크를 사용 하지 않는 ASP.NET 응용 프로그램에서 사용자 상호 작용이 발생 시키고 해당 페이지에서 이벤트를 처리 하 고 페이지를 중심으로 구성 됩니다. 반면, ASP.NET MVC 응용 프로그램을 사용 하 여 사용자 상호 작용은 컨트롤러 및 해당 작업 메서드 중심으로 구성 합니다.

반면에 ASP.NET MVC 프레임 워크는 컨트롤러 라고 하는 클래스에 Url을 매핑합니다. 컨트롤러 들어오는 요청을 처리, 사용자 입력 및 상호 작용을 처리, 적절 한 응용 프로그램 논리를 실행 및 클라이언트에 다시 전송할 응답 결정 (HTML을 표시, 파일을 다운로드, 등 다른 URL 리디렉션). HTML을 표시 하는 경우 컨트롤러 클래스는 일반적으로 요청에 대 한 HTML 태그를 생성 하는 별도 뷰 구성 요소를 호출 합니다. MVC 응용 프로그램에서 보기는 정보만 표시합니다. 컨트롤러가 사용자 입력 및 상호 작용을 처리하고 응답합니다.

이 태스크에서는 Music Store 사이트의 홈 페이지 Url을 처리 하는 컨트롤러 클래스를 추가 합니다.

1. 마우스 오른쪽 단추로 클릭 **컨트롤러** 솔루션 탐색기에서 선택 내에서 폴더 **추가** 차례로 **컨트롤러** 명령:

    ![컨트롤러는 명령을 추가](aspnet-mvc-4-fundamentals/_static/image5.png "컨트롤러 명령 추가")

    *컨트롤러 명령 추가*
2. 합니다 **컨트롤러 추가** 대화 상자가 나타납니다. 컨트롤러 이름을 *HomeController* 누릅니다 **추가**합니다.

    ![컨트롤러 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image6.png "컨트롤러 추가 대화 상자")

    *컨트롤러 추가 대화 상자*
3. 파일 **HomeController.cs** 만들어집니다 합니다 **컨트롤러** 폴더입니다. 위해서는 합니다 **HomeController** 대체, 해당 인덱스 작업에서 문자열을 반환 합니다 **인덱스** 메서드를 다음 코드로:

    (코드 조각- *ASP.NET MVC 4 기본 사항-e x 1 HomeController 인덱스*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해 됩니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다. 프로젝트를 컴파일할 하 고 로컬 IIS 웹 서버 시작 합니다. 로컬 IIS 웹 서버는 웹 서버의 URL을 가리키는 웹 브라우저를 열고 자동으로 됩니다.

    ![웹 브라우저에서 실행 중인 응용 프로그램](aspnet-mvc-4-fundamentals/_static/image7.png "웹 브라우저에서 실행 중인 응용 프로그램")

    *웹 브라우저에서 실행 중인 응용 프로그램*

    > [!NOTE]
    > 로컬 IIS 웹 서버에 임의 가능한 포트 번호를 웹 사이트를 실행 됩니다. 위의 그림에서는 사이트에서 실행 중인 `http://localhost:50103/`이므로 50103 포트를 사용 하는 것입니다. 포트 번호로 달라질 수 있습니다.
2. 브라우저를 닫습니다.

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a>연습 2: 컨트롤러 만들기

이 연습에서는 Music Store 응용 프로그램의 간단한 기능을 구현 하는 컨트롤러를 업데이트 하는 방법을 배웁니다. 해당 컨트롤러의 각 다음 특정 요청을 처리할 작업 메서드를 정의 합니다.

- Music Store에서 음악 장르 목록 페이지
- 특정 장르에 대 한 음악 앨범의 모든를 나열 하는 찾아보기 페이지
- 특정 음악 앨범에 대 한 정보를 보여 주는 세부 정보 페이지

이 연습의 범위에 단순히 해당 작업을 이제 문자열을 반환 합니다.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a>작업 1-새 StoreController 클래스 추가

이 태스크에서는 새 컨트롤러를 추가 합니다.

1. 아직 열지 않은 경우 시작 **VS Express for Web 2012**합니다.
2. 에 **파일** 메뉴 선택 **프로젝트 열기**합니다. 이동할 프로젝트 열기 대화 상자에서 **Source\Ex02 CreatingAController\Begin**를 선택 **Begin.sln** 클릭 **열기**합니다. 또는 계속 진행할 솔루션 이전 연습을 완료 한 후 가져온 합니다.

   1. 제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
3. 새 컨트롤러를 추가 합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 선택 솔루션 탐색기 내에서 폴더 **추가** 차례로 **컨트롤러** 명령입니다. 변경 된 **컨트롤러 이름** 에 *StoreController*, 클릭 **추가**.

    ![컨트롤러 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image8.png "컨트롤러 추가 대화 상자")

    *컨트롤러 추가 대화 상자*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a>작업 2-StoreController의 동작을 수정 합니다.

이 태스크에서는 호출 되는 컨트롤러 메서드를 수정 합니다 **작업**합니다. 작업은 URL 요청을 처리 하 고 브라우저 또는 URL을 호출 하는 사용자에 게 다시 보내야 하는 콘텐츠를 확인 하는 일을 담당 합니다.

1. 합니다 **StoreController** 클래스에 이미 있는 **인덱스** 메서드. Music store의 모든 장르를 나열 하는 페이지를 구현 하려면이 랩에서 사용 합니다. 지금은 바꾸기만 합니다 **인덱스** 메서드를 문자열로 반환 하는 다음 코드로 &quot;Hello Store.Index() from에서&quot;:

    (코드 조각- *ASP.NET MVC 4 기본 사항-e x 2 StoreController 인덱스*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. 추가 **찾아보기** 하 고 **세부 정보** 메서드. 이렇게 하려면 다음 코드를 추가 합니다 **StoreController**:

    (코드 조각- *ASP.NET MVC 4 기본 사항-e x 2 StoreController BrowseAndDetails*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>작업 3-응용 프로그램 실행

이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해 됩니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트에서 시작 합니다 **홈** 페이지입니다. 각 작업의 구현을 확인 하도록 URL을 변경 합니다.

    1. **/ 저장**합니다. 나타납니다  **&quot;Store.Index()에서 Hello&quot;** 합니다.
    2. **/ 저장소/찾아보기**합니다. 나타납니다  **&quot;Store.Browse()에서 Hello&quot;** 합니다.
    3. **/ 저장소/세부 정보**합니다. 나타납니다  **&quot;Store.Details()에서 Hello&quot;** 합니다.

        ![검색 StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "StoreBrowse 검색")

        *검색 /Store/Browse*
3. 브라우저를 닫습니다.

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a>연습 3: 컨트롤러에 매개 변수 전달

지금까지 사용자가 반환 해 왔습니다 상수 문자열 컨트롤러에서. 이 연습에서는 컨트롤러 URL 및 쿼리 문자열을 사용 하 고 브라우저에 텍스트를 사용 하 여 응답 메서드 동작을 설정한 후에 매개 변수를 전달 하는 방법을 배웁니다.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a>작업 1-StoreController 추가 장르 매개 변수

이 작업을 사용 하 여는 **querystring** 매개 변수를 보낼를 **찾아보기** 에서 작업 메서드를 **StoreController**합니다.

1. 아직 열지 않은 경우 시작 **VS Express for Web**합니다.
2. 에 **파일** 메뉴 선택 **프로젝트 열기**합니다. 이동할 프로젝트 열기 대화 상자에서 **Source\Ex03 PassingParametersToAController\Begin**를 선택 **Begin.sln** 클릭 **열기**합니다. 또는 계속 진행할 솔루션 이전 연습을 완료 한 후 가져온 합니다.

   1. 제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
3. 오픈 **StoreController** 클래스입니다. 이 수행 하는 **솔루션 탐색기**를 확장 합니다 **컨트롤러** 폴더를 두 번 클릭 **StoreController.cs**합니다.
4. 변경 된 **찾아보기** 메서드를 특정 장르를 요청 하려면 문자열 매개 변수를 추가 합니다. ASP.NET MVC는 자동으로 모든 쿼리 문자열을 전달 하거나 폼 게시 매개 변수 이름이 **장르** 호출 될 때이 동작 메서드에 있습니다. 이 작업을 수행 하려면 대체 합니다 **찾아보기** 메서드를 다음 코드로:

    (코드 조각- *ASP.NET MVC 4 기본 사항-Ex3 StoreController BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> 사용 중인 합니다 **HttpUtility.HtmlEncode** 유틸리티 메서드를 같은 링크를 사용 하 여 보기에 Javascript를 주입에서 사용자의 것을 금지   **/저장소/찾아보기? 장르 =&lt;스크립트&gt;window.location = '[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;** 합니다.
> 
> 설명은 참조 하세요 [이 msdn 문서](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx)합니다.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>작업 2-응용 프로그램 실행

이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해을 사용 합니다 **장르** 매개 변수입니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트에서 시작 합니다 **홈** 페이지입니다. URL을 변경   */저장/찾아보기? 장르 Disco =* 작업 장르 매개 변수를 수신 하는지 확인 합니다.

    ![StoreBrowseGenre 검색 = Disco](aspnet-mvc-4-fundamentals/_static/image10.png "StoreBrowseGenre 검색 Disco =")

    *검색 /Store/Browse? 장르 Disco =*
3. 브라우저를 닫습니다.

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a>작업 3-URL에 포함 하는 Id 매개 변수를 추가 합니다.

이 작업을 사용 하 여는 **URL** 전달 하는 **Id** 매개 변수를를 **세부 정보** 의 동작 메서드를 **StoreController**합니다. ASP.NET MVC의 기본 명명 된 매개 변수로 작업 메서드 이름 뒤에 url 세그먼트를 처리 하는 라우팅 규칙 **Id**합니다. 동작 메서드에서 Id 라는 매개 변수가 있으면 다음 ASP.NET MVC는 자동으로 URL 세그먼트를 매개 변수로 전달 합니다. URL에 **저장소/세부 정보/5**를 **Id** 로 해석 됩니다 **5**합니다.

1. 변경 합니다 **세부 정보** 메서드는 **StoreController**추가는 **int** 라는 매개 변수 **id**합니다. 이 작업을 수행 하려면 대체 합니다 **세부 정보** 메서드를 다음 코드로:

    (코드 조각- *ASP.NET MVC 4 기본 사항-Ex3 StoreController DetailsMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해을 사용 합니다 **Id** 매개 변수입니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트에서 시작 합니다 **홈** 페이지입니다. URL을 변경 */Store/Details/5* 동작 id 매개 변수를 수신 하는지 확인 합니다.

    ![검색 StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "StoreDetails5 검색")

    *검색 /Store/Details/5*

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a>실습 4: 뷰 만들기

지금 있습니다가 된 문자열에서에서 반환 컨트롤러 작업입니다. 컨트롤러의 작동 방식을 이해 하는 데 도움이 인 이지만 방식을 실제 웹 응용 프로그램은 빌드되지 있습니다. 뷰는 템플릿 파일을 사용 하 여 브라우저로 HTML을 생성 하는 것에 대 한 더 나은 방법을 제공 하는 구성 요소입니다.

이 연습에서는 일반 HTML 콘텐츠를 사이트 및 마지막으로 HTML을 반환 하는 HomeController를 사용 하도록 설정 하려면 보기 템플릿을의 모양과 느낌을 개선 하는 스타일 시트에 대 한 템플릿을 설정 하는 레이아웃 마스터 페이지를 추가 하는 방법을 배웁니다.

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-layoutcshtml"></a>작업 1-파일을 수정 \_layout.cshtml

파일 **~/Views/Shared/\_layout.cshtml** 전체 웹 사이트에서 사용 하기 위해 일반적인 HTML에 대 한 템플릿을 설치할 수 있습니다. 이 태스크에서는 홈 페이지 및 저장소 영역에 대 한 링크를 사용 하 여 공용 헤더를 사용 하 여 레이아웃 마스터 페이지를 추가 합니다.

1. 아직 열지 않은 경우 시작 **VS Express for Web**합니다.
2. 에 **파일** 메뉴 선택 **프로젝트 열기**합니다. 이동할 프로젝트 열기 대화 상자에서 **Source\Ex04 CreatingAView\Begin**를 선택 **Begin.sln** 클릭 **열기**합니다. 또는 계속 진행할 솔루션 이전 연습을 완료 한 후 가져온 합니다.

   1. 제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
3. 파일  <strong>\_layout.cshtml</strong> 사이트의 모든 페이지에 대 한 HTML 컨테이너 레이아웃을 포함 합니다. 여기에 <strong>&lt;html&gt;</strong> HTML 응답에 대 한 요소 뿐만 <strong>&lt;헤드&gt;</strong> 하 고 <strong>&lt;본문&gt;</strong> 요소입니다. <strong>@RenderBody()</strong> HTML 내 본문 영역을 확인할 해당 보기 템플릿은 동적 콘텐츠 채워지는 수 있게 됩니다.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. 모든 페이지는 사이트의 홈 페이지 및 저장소 영역에 대 한 링크를 사용 하 여 공용 헤더를 추가 합니다. 이 작업을 수행 하기 위해 아래 다음 코드를 추가 &lt;본문&gt; 문입니다.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. 각 페이지의 본문 섹션을 렌더링 하는 div를 포함 합니다. 바꿉니다  <strong>@RenderBody()</strong> 다음 higlighted 코드로: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > 알고 계세요? Visual Studio 2012 HTML, 코드 파일에서 자주 사용 되는 코드를 추가할 수 있도록 하는 조각이 있습니다. 입력 하 여 시도해 **&lt;div&gt;** 키를 눌러 **탭** 완전 삽입 하려면 두 번 **div** 태그입니다.

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a>작업 2-CSS 스타일 시트 추가

빈 프로젝트 템플릿을 기본 폼 및 유효성 검사 메시지를 표시 하는 데 사용 되는 스타일을 포함 하는 매우 간소화 된 CSS 파일을 포함 합니다. 사이트의 모양과 느낌을 개선 하기 위해 추가 CSS 및 이미지 (잠재적으로 디자이너에서 제공)를 사용 합니다.

이 태스크에서는 사이트의 스타일을 정의 하는 CSS 스타일 시트를 추가 합니다.

1. CSS 파일 및 이미지에 포함 되어는 **Source\Assets\Content** 이 랩의 폴더입니다. 응용 프로그램에 추가할 하기 위해 해당 콘텐츠를 끌어를 **Windows 탐색기** 창에는 **솔루션 탐색기** Visual Studio express for Web, 아래와 같이:

    ![스타일 콘텐츠를 끌어](aspnet-mvc-4-fundamentals/_static/image12.png "스타일 콘텐츠를 끌어")

    *스타일 콘텐츠를 끌어*
2. 경고 대화 상자가 표시 됩니다, 대체를 확인 하 라고 묻는 **Site.css** 파일과 일부 기존 이미지입니다. 확인할 **모든 항목에 적용** 누릅니다 **예**합니다.

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a>작업 3-보기 템플릿을 추가 합니다.

이 태스크에서는 레이아웃 마스터 페이지를 사용 하는 HTML 응답을 생성 하기 위해 뷰 템플릿을 추가 하 고이 연습에서 CSS 추가 합니다.

1. 사이트의 홈 페이지를 검색할 때 보기 템플릿을 사용 하려면 먼저 문자열을 반환 하는 대신 나타내는 합니다 **HomeController 인덱스** 메서드는 반환을 **보기**합니다. 열기 **HomeController** 클래스 및 변경 해당 **인덱스** 반환 하는 메서드는 **ActionResult**를 반환 하 **View()** 합니다.

    (코드 조각- *ASP.NET MVC 4 기본 사항-Ex4 HomeController 인덱스*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. 이제 적절 한 보기 템플릿을 추가 해야 합니다. 이렇게 하려면 **마우스 오른쪽 단추로 클릭** 내 합니다 **인덱스** 작업 메서드 및 선택 **뷰 추가**합니다. 그러면 합니다 **뷰 추가** 대화 합니다.

    ![인덱스 메서드 내에서 뷰를 추가](aspnet-mvc-4-fundamentals/_static/image13.png "인덱스 메서드 내에서 뷰 추가")

    *인덱스 메서드 내에서 뷰 추가*
3. 합니다 **뷰 추가** 보기 템플릿 파일을 생성 하려면 대화 상자가 나타납니다. 기본적으로이 대화 상자 미리 채웁니다 보기 템플릿의 이름을 사용 하는 작업 메서드를 일치 시킬 수 있도록 합니다. 사용 했기 때문에 **뷰 추가** 내 상황에 맞는 메뉴를 **인덱스** HomeController 내에서 작업 메서드를 **뷰 추가** 대화 상자에 기본 보기 이름으로 인덱스를 포함 합니다. **추가**를 클릭합니다.

    ![뷰 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image14.png "뷰 추가 대화 상자")

    *뷰 추가 대화 상자*
4. Visual Studio에서 생성을 **Index.cshtml** 내에서 템플릿 보기는 **Views\Home** 폴더를 클릭 합니다.

    ![만든 인덱스 뷰 홈](aspnet-mvc-4-fundamentals/_static/image15.png "만들어진 인덱스 홈 보기")

    *만든 홈 인덱스 보기*

    > [!NOTE]
    > 이름 및 위치를 **Index.cshtml** 파일 관련 되며 기본 ASP.NET MVC 명명 규칙을 따릅니다.
    > 
    > 폴더 \Views\**홈** 컨트롤러 이름과 일치 (**홈** 컨트롤러). 보기 템플릿 이름 (**인덱스**), 보기를 표시 하는 컨트롤러 작업 메서드와 일치 합니다.
    > 
    > 이러한 방식으로 ASP.NET MVC 뷰를 반환 하려면이 명명 규칙을 사용 하는 경우 이름 또는 뷰 템플릿의 위치를 명시적으로 지정 하지 않아도 됩니다.
5. 생성된 된 보기 템플릿을 기반으로 합니다  **\_layout.cshtml** 템플릿을 이전에 정의 합니다. ViewBag.Title 속성을 업데이트 **홈**, 기본 콘텐츠를 변경 하 고 **홈 페이지**아래 코드에 표시 된 것 처럼:

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. 선택 **MvcMusicStore** 누릅니다 솔루션 탐색기에서 프로젝트 **F5** 응용 프로그램을 실행 합니다.

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a>작업 4: 확인

이전 연습에서 단계를 올바르게 수행 했는지를 확인 하기 위해 다음과 같이 계속 진행 합니다.

브라우저에서 연 응용 프로그램에 유의 해야 합니다.

1. HomeController의 Index 작업 메서드에 찾아서 표시 합니다 **\Views\Home\Index.cshtml** 코드를 호출 하는 경우에 템플릿을 보려면 **View() 반환**이므로 뷰 템플릿을 표준 명명 규칙입니다.
2. 홈 페이지 내에 정의 된 환영 메시지를 표시 합니다 **\Views\Home\Index.cshtml** 템플릿 보기.
3. 홈 페이지를 사용 하는  **\_layout.cshtml** 템플릿을 이므로 환영 메시지는 표준 사이트 HTML 레이아웃 내에 포함 됩니다.

    ![인덱스 보기 정의 LayoutPage 및 스타일을 사용 하 여 홈](aspnet-mvc-4-fundamentals/_static/image16.png "정의 LayoutPage 및 스타일을 사용 하 여 인덱스 뷰 홈")

    *정의 된 LayoutPage 및 스타일을 사용 하 여 홈 인덱스 보기*

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a>실습 5: 뷰 모델 만들기

지금 하드 코드 된 HTML을 표시 하 여 보기를 수행 하지만 동적 웹 응용 프로그램을 만들기 위해 보기 템플릿 받아야 정보 컨트롤러에서. 해당 용도에 사용 되는 일반적인 방법은 하나는 **ViewModel** 적절 한 HTML 응답을 생성 하는 데 필요한 모든 정보를 패키지 하는 컨트롤러를 허용 하는 패턴입니다.

이 연습에서는 ViewModel 클래스를 만들고 필요한 속성을 추가 하는 방법을 배우게 됩니다: 저장소 및 해당 장르 목록에서 장르의 수입니다. 만든된 ViewModel을 사용 하 여 StoreController 업데이트도 하 고 마지막으로 페이지에 언급 된 속성을 표시 하는 새 보기 템플릿을 만듭니다.

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a>작업 1-ViewModel 클래스 만들기

이 태스크에서는 저장소 장르 목록 시나리오를 구현 하는 ViewModel 클래스를 만들게 됩니다.

1. 아직 열지 않은 경우 시작 **VS Express for Web**합니다.
2. 에 **파일** 메뉴 선택 **프로젝트 열기**합니다. 이동할 프로젝트 열기 대화 상자에서 **Source\Ex05 CreatingAViewModel\Begin**를 선택 **Begin.sln** 클릭 **열기**합니다. 또는 계속 진행할 솔루션 이전 연습을 완료 한 후 가져온 합니다.

   1. 제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
3. 만들기는 **Viewmodel** ViewModel을 보관할 폴더를 합니다. 이렇게 하려면 최상위을 마우스 오른쪽 단추로 **MvcMusicStore** 프로젝트 선택 **추가** 차례로 **새 폴더**합니다.

    ![새 폴더 추가](aspnet-mvc-4-fundamentals/_static/image17.png "새 폴더를 추가 합니다.")

    *새 폴더를 추가합니다.*
4. 폴더의 이름을 *Viewmodel*합니다.

    ![솔루션 탐색기에서 ViewModels 폴더](aspnet-mvc-4-fundamentals/_static/image18.png "솔루션 탐색기에서 ViewModels 폴더")

    *솔루션 탐색기에서 ViewModels 폴더*
5. 만들기는 **ViewModel** 클래스입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **ViewModels** 최근에 만든 폴더를 선택 **추가** 차례로 **새 항목**합니다. 아래 **코드**를 선택 합니다 **클래스** 항목 및 파일 이름을 *StoreIndexViewModel.cs*, 클릭 **추가**합니다.

    ![새 클래스를 추가](aspnet-mvc-4-fundamentals/_static/image19.png "새 클래스 추가")

    *새 클래스 추가*

    ![StoreIndexViewModel 클래스를 만들어](aspnet-mvc-4-fundamentals/_static/image20.png "만들기 StoreIndexViewModel 클래스")

    *StoreIndexViewModel 클래스 만들기*

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a>작업 2-ViewModel 클래스에 속성 추가

에서 전달할 수는 StoreController 보기 템플릿에서 예상 되는 HTML 응답을 생성 하기 위해 두 개의 매개 변수가: 저장소 및 해당 장르 목록에서 장르의 수입니다.

이 태스크에서는 이러한 2 속성을 추가 합니다 **StoreIndexViewModel** 클래스: **NumberOfGenres** (정수) 및 **장르** (문자열의 목록).

1. 추가 **NumberOfGenres** 하 고 **장르** 속성을 **StoreIndexViewModel** 클래스입니다. 이렇게 하려면 클래스 정의에 다음 두 줄 추가:

    (코드 조각- *ASP.NET MVC 4 기본 사항-Ex5 StoreIndexViewModel 속성*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> **{get; 설정;}**  표기법에서는 C#의 자동 구현 속성 기능입니다. 지원 필드를 선언 하기를 요구 하지 않고 속성의 이점을 제공 합니다.

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a>작업 3-업데이트 StoreController StoreIndexViewModel를 사용 하려면

합니다 **StoreIndexViewModel** 에서 전달 하는 데 필요한 정보를 캡슐화 하는 클래스 **StoreController**의 **인덱스** 응답을 생성 하기 위해 템플릿 보기를 사용 하는 방법 .

이 태스크에서는 업데이트를 **StoreController** 사용 하는 **StoreIndexViewModel**합니다.

1. 오픈 **StoreController** 클래스입니다.

    ![StoreController 클래스를 열고](aspnet-mvc-4-fundamentals/_static/image21.png "여 StoreController 클래스")

    *열기 StoreController 클래스*
2. 사용 하기 위해를 **StoreIndexViewModel** 에서 클래스를 **StoreController**, 맨 위에 있는 다음 네임 스페이스를 추가 합니다 **StoreController** 코드:

    (코드 조각- *ASP.NET MVC 4 기본 사항-Viewmodel을 사용 하 여 Ex5 StoreIndexViewModel*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. 변경 된 **StoreController**의 **인덱스** 를 만들고 채우는 작업 메서드를 **StoreIndexViewModel** 개체 한 다음를 뷰 템플릿으로 전달 이 사용 하 여 HTML 응답을 생성 합니다.

    > [!NOTE]
    > 랩에서 &quot;ASP.NET MVC 모델 및 데이터 액세스&quot; 저장소 장르 목록을 데이터베이스에서 검색 하는 코드를 작성 합니다. 다음 코드를 만듭니다는 **목록** 채울 더미 데이터가 장르를 **StoreIndexViewModel**합니다.
    > 
    > 만들기 및 설정 후 합니다 **StoreIndexViewModel** 개체를 인수로 전달 됩니다 합니다 **보기** 메서드. 보기 템플릿에서 된 HTML 응답을 생성 하려면 해당 개체를 사용할지를 나타냅니다.
4. 대체는 **인덱스** 메서드를 다음 코드로:

    (코드 조각- *ASP.NET MVC 4 기본 사항-Ex5 StoreController 인덱스 메서드*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> C#을 사용 하 여 잘 모르는 경우 사용 가정할 수 있습니다 **var** 함을 의미 합니다 **viewModel** 변수가 런타임에 바인딩된. 올바른-C# 컴파일러는 형식 유추를 변수에 할당 하는 항목에 따라 사용 하 여 확인 하는 없는 **viewModel** 유형의 **StoreIndexViewModel**합니다. 또한 로컬을 컴파일하여 **viewModel** 으로 변수를 **StoreIndexViewModel** 형식의 get 컴파일 타임 검사와 Visual Studio 코드 편집기 지원 합니다.

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a>작업 4-StoreIndexViewModel를 사용 하는 보기 템플릿 만들기

이 태스크에서는 장르 목록을 표시 하려면 컨트롤러에서 전달 되는 StoreIndexViewModel 개체에서 사용할 보기 템플릿을 만들게 됩니다.

1. 새 템플릿 보기를 만들기 전에 프로젝트를 빌드 해 보겠습니다 있도록를 **뷰 추가 대화 상자** 알고 합니다 **StoreIndexViewModel** 클래스입니다. 선택 하 여 프로젝트를 빌드할 합니다 **빌드** 메뉴 항목 차례로 **MvcMusicStore 빌드**합니다.

    ![프로젝트를 빌드하면](aspnet-mvc-4-fundamentals/_static/image22.png "프로젝트 빌드")

    *프로젝트 빌드*
2. 새 보기 템플릿을 만듭니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **인덱스** 선택한 메서드 **뷰 추가**합니다.

    ![뷰 추가](aspnet-mvc-4-fundamentals/_static/image23.png "뷰 추가")

    *보기 추가*
3. 때문에 **추가 보기 대화 상자** 에서 호출한를 **StoreController**, 템플릿 보기에는 기본적으로 추가 됩니다는 **\Views\Store\Index.cshtml** 파일. 확인 합니다 **는 강력한 형식의-뷰 만들기** 확인란을 선택한 후 **StoreIndexViewModel** 으로 **모델 클래스**. 또한 선택 하는 뷰 엔진이 인지를 확인 **Razor**합니다. **추가**를 클릭합니다.

    ![뷰 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image24.png "뷰 추가 대화 상자")

    *뷰 추가 대화 상자*

    합니다 **\Views\Store\Index.cshtml** 보기 템플릿 파일 만들어지고 열립니다. 에 제공 된 정보를 기반으로 **뷰 추가** 템플릿이 예상 하는 보기 마지막 단계에서는 대화를 **StoreIndexViewModel** 인스턴스로 데이터를 사용 하 여 HTML 응답을 생성 합니다. 템플릿을 상속 하는 것을 알 수 있습니다는 `ViewPage<musicstore.viewmodels.storeindexviewmodel>` C#입니다.

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a>작업 5-템플릿 보기를 업데이트 하는 중

이 태스크에서는 장르 및 페이지 내에서 해당 이름의 수를 검색 하려면 마지막 작업에서 만든 뷰 템플릿을 업데이트 합니다.

> [!NOTE]
> @ 구문은 사용 하 여 (라고도 &quot;코드 너 깃&quot;) 템플릿 보기 내에서 코드를 실행 합니다.

1. **Index.cshtml** 파일 내는 **저장소** 폴더를 해당 코드를 다음으로 바꿉니다.

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
2. 장르 목록 루프 **StoreIndexViewModel** HTML 만들어 **&lt;ul&gt;** 사용 하 여 목록을 **foreach** 루프입니다.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. 키를 눌러 **F5** 응용 프로그램을 실행 하 여 찾아보기 **스토어**합니다. 전달 하는 장르 목록을 표시 합니다 **StoreIndexViewModel** 에서 개체를 **StoreController** 보기 템플릿에 합니다.

    ![장르 목록을 표시 하는 보기](aspnet-mvc-4-fundamentals/_static/image26.png "장르 목록을 표시 하는 보기")

    *장르 목록을 표시 하는 보기*
4. 브라우저를 닫습니다.

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a>실습 6:를 사용 하 여 매개 변수 보기

연습 3의 컨트롤러에 매개 변수를 전달 하는 방법을 알아보았습니다. 이 연습에서는 보기 템플릿에서 이러한 매개 변수를 사용 하는 방법을 배웁니다. 이 위해 소개 합니다 먼저 사용자 데이터 및 도메인 논리를 관리 하는 데 도움이 되는 모델 클래스입니다. 또한 인코딩 URL 경로 등의 걱정 없이 ASP.NET MVC 응용 프로그램 내 페이지의 링크를 만드는 방법을 배웁니다.

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a>작업 1-모델 클래스 추가

모델 클래스는 컨트롤러에서 보기로 정보를 전달 하기 위한 것 만들어지는 Viewmodel와 달리 포함 하 고 데이터 및 도메인 논리를 관리할에 빌드됩니다. 이 작업에서는 이러한 개념을 나타내기 위해 두 모델 클래스를 추가 합니다. **장르** 하 고 **앨범**합니다.

1. 아직 열지 않은 경우 시작 **VS Express for Web**
2. 에 **파일** 메뉴 선택 **프로젝트 열기**합니다. 이동할 프로젝트 열기 대화 상자에서 **Source\Ex06 UsingParametersInView\Begin**를 선택 **Begin.sln** 클릭 **열기**합니다. 또는 계속 진행할 솔루션 이전 연습을 완료 한 후 가져온 합니다.

   1. 제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
3. 추가 된 **장르** 모델 클래스입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더에는 **솔루션 탐색기**를 선택 **추가** 차례로 **새 항목** 옵션. 아래 **코드**를 선택 합니다 **클래스** 항목 및 파일 이름을 *Genre.cs*, 클릭 **추가**합니다.

    ![클래스 추가](aspnet-mvc-4-fundamentals/_static/image27.png "클래스 추가")

    *새 항목 추가*

    ![장르 모델 클래스 추가](aspnet-mvc-4-fundamentals/_static/image28.png "장르 모델 클래스 추가")

    *장르 모델 클래스 추가*
4. 추가 된 **이름** 장르 클래스 속성입니다. 이렇게 하려면 다음 코드를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 기본 사항-Ex6 장르*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. 추가 이전으로 동일한 절차를 **앨범** 클래스입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더에는 **솔루션 탐색기**를 선택 **추가** 차례로 **새 항목** 옵션. 아래 **코드**를 선택 합니다 **클래스** 항목 및 파일 이름을 *Album.cs*, 클릭 **추가**합니다.
6. 앨범 클래스에 두 개의 속성을 추가 합니다. **장르** 하 고 **제목**합니다. 이렇게 하려면 다음 코드를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 기본 사항-Ex6 앨범*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a>작업 2-는 StoreBrowseViewModel 추가

A **StoreBrowseViewModel** 선택한 장르가 일치 하는 앨범에 표시할이 작업에 사용할 수 있습니다. 이 태스크에서는이 클래스 만들고 처리에 두 속성을 추가 합니다 **장르** 및 해당 **앨범**의 목록입니다.

1. 추가 된 **StoreBrowseViewModel** 클래스입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **Viewmodel** 폴더에는 **솔루션 탐색기**를 선택 **추가** 차례로 **새 항목** 옵션. 아래 **코드**를 선택 합니다 **클래스** 항목 및 파일 이름을 *StoreBrowseViewModel.cs*, 클릭 **추가**합니다.
2. 모델에 대 한 참조를 추가 **StoreBrowseViewModel** 클래스입니다. 이 작업을 수행 하려면 다음 추가 네임 스페이스를 사용 하 여:

    (코드 조각- *ASP.NET MVC 4 기본 사항-Ex6 UsingModel*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. 두 개의 속성을 추가 **StoreBrowseViewModel** 클래스: **장르** 하 고 **앨범**합니다. 이렇게 하려면 다음 코드를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 기본 사항-Ex6 ModelProperties*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> 란 **목록&lt;앨범&gt;**  ?:이 정의 사용 하는 **목록&lt;T&gt;**  형식 여기서 **T** 제한 합니다 이 요소 형식을 **목록을** 여기서 속한 **앨범** (또는 해당 하위 항목 중 하나).
> 
> 이 기능을 디자인 하는 클래스 또는 메서드 선언 및 기능은 C# 언어의 클라이언트 코드에서 인스턴스화할 때까지 하나 이상의 형식 사양을 따르는 클래스와 메서드 호출 **제네릭**합니다.
> 
> **목록&lt;T&gt;**  제네릭 동일 합니다 **ArrayList** 입력 하 고 사용할 수 있습니다 합니다 **System.Collections.Generic** 네임 스페이스입니다. 사용의 이점 중 하나 **제네릭을** 는 지정 된 형식 이므로 필요가 없습니다 형식 검사에 요소를 캐스팅 하는 등의 작업을 처리 하는 **앨범** 를사용하여마찬가지로**ArrayList**합니다.

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a>작업 3-는 StoreController에서 새 ViewModel을 사용 하 여

이 태스크에서는 수정 합니다 **StoreController**의 **찾아보기** 하 고 **세부 정보** 작업 메서드를 사용 하도록 **StoreBrowseViewModel** .

1. Models 폴더에 대 한 참조를 추가 **StoreController** 클래스입니다. 이 작업을 수행 하려면 확장 합니다 **컨트롤러** 폴더에는 **솔루션 탐색기** 연를 **StoreController** 클래스. 다음 코드를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 기본 사항-Ex6 UsingModelInController*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. 대체는 **찾아보기** 사용 하는 작업 메서드는 **StoreViewBrowseController** 클래스입니다. 더미 데이터를 사용 하 여 두 가지 새로운 앨범 개체 및 장르를 만듭니다 (다음 실습 랩에서 사용 데이터베이스의 실제 데이터). 이 작업을 수행 하려면 대체 합니다 **찾아보기** 메서드를 다음 코드로:

    (코드 조각- *ASP.NET MVC 4 기본 사항-Ex6 BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. 대체는 **세부 정보** 사용 하는 작업 메서드는 **StoreViewBrowseController** 클래스입니다. 새로 만든 **앨범** 가 반환 될 개체를 **보기**합니다. 이 작업을 수행 하려면 대체 합니다 **세부 정보** 메서드를 다음 코드로:

    (코드 조각- *ASP.NET MVC 4 기본 사항-Ex6 DetailsMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a>작업 4-찾아보기 보기 템플릿을 추가 합니다.

이 태스크에서는 추가 된 **찾아보기** 특정 장르에 앨범을 표시 하도록 보기.

1. 새 템플릿 보기를 만들기 전에 프로젝트를 작성 해야 있도록를 **뷰 추가** 대화에 대해 알고 합니다 **ViewModel** 클래스를 사용 합니다. 선택 하 여 프로젝트를 빌드할 합니다 **빌드** 메뉴 항목 차례로 **MvcMusicStore 빌드**합니다.
2. 추가 된 **찾아보기** 보기. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **찾아보기** 의 동작 메서드는 **StoreController** 클릭 **뷰 추가**합니다.
3. 에 **뷰 추가** 대화 상자에서 보기 이름 인지 확인 **찾아보기**합니다. 확인 합니다 **강력한 형식의 뷰를 만들** 확인란을 선택한 **StoreBrowseViewModel** 에서 **모델 클래스** 드롭다운 합니다. 다른 필드는 기본값으로 둡니다. **추가**를 클릭합니다.

    ![찾아보기 뷰 추가](aspnet-mvc-4-fundamentals/_static/image29.png "찾아보기 뷰 추가")

    *찾아보기 뷰 추가*
4. 수정 합니다 **Browse.cshtml** 장르의 정보를 표시 하에 액세스 하는 **StoreBrowseViewModel** 템플릿 보기에 전달 되는 개체입니다. 이 위해 콘텐츠를 다음으로 바꿉니다. (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>작업 5-응용 프로그램 실행

이 작업을 테스트 하는 합니다 **찾아보기** 앨범에서를 검색 하는 메서드는 **찾아보기** 메서드 작업 합니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경   **/저장/찾아보기? 장르 Disco =** 두 앨범을 반환 하는 작업을 확인 합니다.

    ![Disco 앨범 저장소 찾아보기](aspnet-mvc-4-fundamentals/_static/image30.png "Disco 앨범 저장소를 검색 합니다.")

    *Disco 앨범 저장소를 검색합니다.*

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a>태스크 6-정보는 특정 앨범 표시

이 작업을 구현 합니다 **저장소/세부 정보** 특정 앨범에 대 한 정보를 표시 하려면 보기. 이 실습 랩에서 앨범에 대 한 표시는 모든 항목에 이미 포함 되어는 **보기** 템플릿. 새로 만드는 대신이 **StoreDetailsViewModel** 클래스를 현재 사용 하 여 **StoreBrowseViewModel** 앨범 전달할 템플릿.

1. Visual Studio 창으로 돌아가려면 필요한 경우 브라우저를 닫습니다. 새 **세부 정보** 에 대 한 보기를 **StoreController**의 **세부 정보** 작업 메서드. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **세부 정보** 에서 메서드는 **StoreController** 클래스 및 클릭 **뷰 추가**합니다.
2. 에 **뷰 추가** 대화 상자에서 되어 있는지 확인 합니다 **뷰 이름** 는 **세부 정보**. 확인 합니다 **강력한 형식의 뷰를 만들** 확인란을 선택한 **앨범** 에서 **모델 클래스** 드롭다운 목록. 다른 필드는 기본값으로 둡니다. **추가**를 클릭합니다. 이 만들고 엽니다는 **\Views\Store\Details.cshtml** 파일입니다.

    ![추가 세부 정보 보기](aspnet-mvc-4-fundamentals/_static/image31.png "세부 정보 보기 추가")

    *세부 정보 보기 추가*
3. 수정 합니다 **Details.cshtml** 앨범의 정보를 표시 하는 파일에 액세스 하는 **앨범** 템플릿 보기에 전달 되는 개체입니다. 이 위해 콘텐츠를 다음으로 바꿉니다. (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>태스크 7-응용 프로그램 실행

이 작업을 테스트 하는 합니다 **세부 정보** 보기에서 앨범의 정보를 검색 합니다 **작업 세부 정보** 메서드.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트에서 시작 합니다 **홈** 페이지입니다. URL을 변경 **/Store/Details/5** 앨범의 정보를 확인 합니다.

    ![앨범 세부 정보를 검색](aspnet-mvc-4-fundamentals/_static/image32.png "앨범 세부 정보를 검색 합니다.")

    *앨범의 세부 정보를 검색합니다.*

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a>태스크 8-페이지 간 링크 추가

이 태스크에서는 적절 한 모든 장르 이름에 링크가 있습니다 저장소 뷰에서 링크를 추가 합니다 **/저장소/찾아보기** URL입니다. 이 이렇게 하면 예를 들어 장르를 클릭 **Disco**로 이동 됩니다 **/저장소/찾아보기? 장르 Disco =** URL입니다.

1. Visual Studio 창으로 돌아가려면 필요한 경우 브라우저를 닫습니다. 업데이트를 **인덱스** 에 대 한 링크를 추가 하려면 페이지의 **찾아보기** 페이지입니다. 이 수행 하는 **솔루션 탐색기** 확장를 **뷰** 폴더를 해당 **저장소** 폴더를 두 번 클릭 합니다 **Index.cshtml** 페이지.
2. 선택한 장르를 나타내는 찾아보기 보기에 대 한 링크를 추가 합니다. 이렇게 하려면 다음 강조 표시 된 코드를 대체 합니다 **&lt;li&gt;** 태그: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > 또 다른 방법은 다음과 같은 코드를 사용 하 여 페이지에 직접 연결할 수는 있습니다.
   > 
   > &lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;
   > 
   > 이 방법은 작동 하지만 하드 코드 된 문자열에 따라 다릅니다. 나중에 컨트롤러를 바꾸면를 사용 하는 경우에이 명령이 수동으로 변경 합니다. 더 나은 방법은 사용 하는 **HTML 도우미** 메서드. ASP.NET MVC에는 이러한 작업에 사용할 수 있는 HTML 도우미 메서드를 포함 합니다. **Html.ActionLink()** 도우미 메서드를 사용 하면 손쉽게 HTML 만들 **&lt;를&gt;** 링크, URL 경로 URL로 인코딩된 제대로 확인 합니다.
   > 
   > Htlm.ActionLink 여러 오버 로드가 있습니다. 이 연습의 세 매개 변수를 사용 하는 것을 사용 합니다.
   > 
   > 1. 장르 이름을 표시 하는 링크 텍스트
   > 2. 컨트롤러 작업 이름 (**찾아보기**)
   > 3. 경로 매개 변수 값, 두 이름을 지정 (**장르**)과 값 (**장르 이름**)

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a>태스크 9-응용 프로그램 실행

이 태스크에서는 테스트할 장르별로 적절 한 링크와 함께 표시 되도록 **/저장소/찾아보기** URL입니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **스토어** 장르별로 적절 한 링크를 확인 하려면 **/저장소/찾아보기** URL입니다.

    ![찾아보기 페이지에 대 한 링크를 사용 하 여 장르를 찾는](aspnet-mvc-4-fundamentals/_static/image33.png "찾아보기 페이지에 대 한 링크를 사용 하 여 장르 검색")

    *찾아보기 페이지에 대 한 링크를 사용 하 여 장르를 검색*

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a>태스크 10-를 사용 하 여 동적 ViewModel 컬렉션 값 전달

이 태스크에서는 모델에서 변경 하지 않고 컨트롤러와 뷰 간에 값을 전달 하는 단순 하면서도 강력한 메서드를 배우게 됩니다. 컬렉션을 제공 하는 ASP.NET MVC 4 &quot;ViewModel&quot;, 동적 값으로 할당 및 컨트롤러 및 보기도 내에서 액세스할 수는 있습니다.

이제 ViewBag 동적 컬렉션 목록을 전달 하는 데 사용할 &quot; **장르 별표 표시** &quot; 뷰 컨트롤러에서 합니다. 저장소 인덱스 보기에 액세스 하는 **ViewModel** 정보를 표시 합니다.

1. Visual Studio 창으로 돌아가려면 필요한 경우 브라우저를 닫습니다. 오픈 **StoreController.cs** 수정할 **인덱스** 목록을 만드는 메서드를 ViewModel 컬렉션에 장르를 별표 표시:

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > 구문을 사용할 수도 있습니다 **ViewBag [&quot;Starred&quot;]** 속성에 액세스할 수 있습니다.
2. 별 모양 아이콘 **&quot;starred.png&quot;** 에 포함 되는 **Source\Assets\Images** 이 랩의 폴더입니다. 응용 프로그램을 추가 하려면 해당 콘텐츠를 끌어를 **Windows 탐색기** 창에는 **솔루션 탐색기** Visual Web Developer Express를 아래와 같이에서:

    ![솔루션 별 이미지 추가](aspnet-mvc-4-fundamentals/_static/image34.png "솔루션 별 이미지 추가")

    *솔루션 별 이미지 추가*
3. 보기를 엽니다 **Store/Index.cshtml** 및 콘텐츠를 수정 합니다. 읽기는 &quot;별표 표시&quot; 속성에는 **ViewBag** 컬렉션 현재 장르 이름이 목록에 요청 합니다. 이 경우 장르 링크를 오른쪽에서 별 모양 아이콘을 표시 됩니다.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a>태스크 11-응용 프로그램 실행

이 태스크에서는 별점이 부여 된 장르 별 모양 아이콘 표시를 테스트 합니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트에서 시작 합니다 **홈** 페이지입니다. URL을 변경 **스토어** 주요 장르별로 respecting 레이블이 있는지 확인 하려면:

    ![별점이 부여 된 요소를 사용 하 여 장르를 찾는](aspnet-mvc-4-fundamentals/_static/image35.png "별점이 부여 된 요소를 사용 하 여 장르 검색")

    *별점이 부여 된 요소를 사용 하 여 장르를 검색*

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a>실습 7: ASP.NET MVC 4 새 템플릿 주위의 랩

이 연습에서는 탐색에서 ASP.NET MVC 4 프로젝트 템플릿, 향상 된 기능 가장 관련 된 기능의 새 템플릿 살펴보겠습니다.

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a>작업 1: ASP.NET MVC 4 인터넷 응용 프로그램 템플릿 탐색

1. 아직 열지 않은 경우 시작 **VS Express for Web**
2. 선택 된 **파일 | 새 | 프로젝트** 메뉴 명령입니다. 에 **새 프로젝트** 대화 상자에서 선택 된 **Visual C# | 웹** 왼쪽된 창에서 템플릿을 선택한 트리의 합니다 **ASP.NET MVC 4 웹 응용 프로그램**합니다. **이름** 프로젝트 *MusicStore* 하 고 업데이트를 **솔루션 이름** 에 *시작*, 다음 위치를 선택 (또는 기본값을 그대로 두고) 클릭 하 고 **확인** .

    ![새 ASP.NET MVC 4 프로젝트를 만드는](aspnet-mvc-4-fundamentals/_static/image36.png "새 ASP.NET MVC 4 프로젝트 만들기")

    *새 ASP.NET MVC 4 프로젝트 만들기*
3. 에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 선택 합니다 **인터넷 응용 프로그램** 프로젝트 템플릿 및 클릭 **확인**합니다. ASPX 또는 Razor 보기 엔진으로 선택할 수 있습니다를 확인 합니다.

    ![새 ASP.NET MVC 4 인터넷 응용 프로그램을 만드는](aspnet-mvc-4-fundamentals/_static/image37.png "새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기")

    *새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기*

    > [!NOTE]
    > ASP.NET MVC 3에서 razor 구문이 도입 되었습니다. 해당 목표 문자와 유체 워크플로 코딩을 빠르게 사용 하도록 설정 하면 파일에 필요한 키 입력 횟수를 최소화 하는 것입니다. 기존 C# /VB (또는 기타)을 활용 하는 razor 언어 실력 하 고 멋진 HTML 생성 워크플로 가능 하 게 하는 템플릿 태그 구문을 제공 합니다.
4. 키를 눌러 **F5** 솔루션을 실행 하 여 갱신 된 템플릿을 참조 하세요. 다음 기능을 사용해 확인할 수 있습니다.

    1. **최신 스타일 템플릿**

        템플릿은 갱신 되 었어야, 더 많은 최신 스타일을 제공 합니다.

        ![ASP.NET MVC 4 맞게 스타일을 다시 템플릿을](aspnet-mvc-4-fundamentals/_static/image38.png "맞게 템플릿 스타일을 다시 ASP.NET MVC 4")

        *ASP.NET MVC 4 맞게 스타일을 다시 템플릿*
    2. **적응형 렌더링**

        브라우저 창의 크기를 조정 확인 하 고 페이지 레이아웃 새 창 크기를 동적으로 조정 하는 방법을 확인할 수 있습니다. 이러한 템플릿은 적응형 렌더링 기술의 사용 하 여 사용자 지정 하지 않고 데스크톱 및 모바일 플랫폼에서 올바르게 렌더링 합니다.

        ![다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿은](aspnet-mvc-4-fundamentals/_static/image39.png "다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿")

        *다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿*
5. 디버거를 중지 하 고 Visual Studio로 돌아가서 브라우저를 닫습니다.
6. 이제 솔루션을 탐색 하 고 일부의 프로젝트 템플릿에서 ASP.NET MVC 4에서 도입 된 새로운 기능 확인 수 있습니다.

    ![ASP.NET mvc 4-인터넷-응용 프로그램-프로젝트-템플릿을](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿")

    *ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿*

   1. **HTML5 태그**

       예를 들어 열린 새 테마 태그를 확인 하려면 템플릿 보기 찾아보기 **About.cshtml** 내에서 보려면 **홈** 폴더입니다.

       ![HTML5 및 Razor 태그를 사용 하 여 새 템플릿을](aspnet-mvc-4-fundamentals/_static/image41.png "HTML5 및 Razor 태그를 사용 하 여 새 템플릿")

       *HTML5 및 Razor 태그를 사용 하 여 새 템플릿*
   2. **JavaScript 라이브러리가 포함**

      1. **jQuery**: jQuery HTML 문서 통과, 이벤트 처리, 애니메이션 효과 적용, 및 Ajax 상호 작용을 간소화 합니다.
      2. **jQuery UI**:이 라이브러리는 낮은 수준의 상호 작용 및 애니메이션 효과 고급 themeable widgets, jQuery JavaScript 라이브러리를 기반으로 구축 된 추상화를 제공 합니다.

         > [!NOTE]
         > JQuery 및 jQuery UI 알아볼 수 있습니다에 [ [ http://docs.jquery.com/ ](http://docs.jquery.com/) ](http://docs.jquery.com/)합니다.
      3. **KnockoutJS**: 이제는 ASP.NET MVC 4 기본 템플릿을 **KnockoutJS**, JavaScript 및 HTML을 사용 하 여 풍부 하 고 응답성이 뛰어난 웹 응용 프로그램을 만들 수 있는 JavaScript MVVM 프레임 워크입니다. 같은 ASP.NET MVC 3, jQuery 및 jQuery UI 라이브러리도 포함 되어 ASP.NET MVC 4입니다.

          > [!NOTE]
          > 이 링크에 KnockOutJS 라이브러리에 대 한 자세한 정보를 얻을 수 있습니다: [ http://learn.knockoutjs.com/ ](http://learn.knockoutjs.com/)합니다.
      4. **Modernizr**: HTML5 및 CSS3 기술을 사용 하는 경우 사이트를 이전 버전의 브라우저와 호환 하이 라이브러리를 자동으로 실행 됩니다.

          > [!NOTE]
          > 이 링크에 Modernizr 라이브러리에 대 한 자세한 정보를 얻을 수 있습니다: [ http://www.modernizr.com/ ](http://www.modernizr.com/)합니다.
   3. **SimpleMembership 솔루션에 포함**

       이전 ASP.NET 역할 및 멤버 자격 공급자 시스템의 대체로 SimpleMembership 설계 되었습니다. 쉽게 보안 웹 페이지 개발자를 위한 더 유연 하 게에서 하는 여러 가지 새로운 기능에

       인터넷 템플릿은 이미 설정한 SimpleMembership를 통합 하는 몇 가지, OAuthWebSecurity (에 대 한 OAuth 계정 등록, 로그인, 관리, 등) 및 웹 보안을 사용 하는 AccountController 준비 되는 예를 들어 있습니다.

       ![솔루션에 포함 된 SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership 솔루션에 포함")

       *SimpleMembership 솔루션에 포함*

       > [!NOTE]
       > 에 대 한 자세한 정보를 찾을 [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) MSDN에 있습니다.

> [!NOTE]
> 또한 다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다 [부록 b: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixB)합니다.


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습을 완료 하 여 ASP.NET MVC의 기본 사항을 알아보았습니다.

- MVC 응용 프로그램 및 이들이 어떻게 상호 작용의 핵심 요소
- ASP.NET MVC 응용 프로그램을 만드는 방법
- URL 및 쿼리 문자열을 통해 전달 된 추가 하 고 매개 변수를 처리 하는 컨트롤러를 구성 하는 방법
- 공통 HTML 콘텐츠, 모양 및 느낌 및 HTML 콘텐츠를 표시 하려면 보기 템플릿을 개선 하는 스타일 시트에 대 한 템플릿을 설정 하는 레이아웃 마스터 페이지를 추가 하는 방법
- 동적 정보를 표시 하려면 템플릿 보기에 속성을 전달 하는 것에 대 한 ViewModel 패턴을 사용 하는 방법
- 보기 템플릿은 컨트롤러에 전달 된 매개 변수를 사용 하는 방법
- ASP.NET MVC 응용 프로그램 내에서 페이지에 대 한 링크를 추가 하는 방법
- 추가 보기에서 동적 속성을 사용 하는 방법
- ASP.NET MVC 4 프로젝트 템플릿에서 향상 된 기능

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 a: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**. 다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.

1. 로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다. 또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Windows Azure SDK를 사용 하 여 Web</em>&quot;합니다.
2. 클릭할 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.

    ![Visual Studio Express를 설치](aspnet-mvc-4-fundamentals/_static/image43.png "Visual Studio Express를 설치 합니다.")

    *Visual Studio Express를 설치 합니다.*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건에 동의](aspnet-mvc-4-fundamentals/_static/image44.png)

    *사용 조건에 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-fundamentals/_static/image45.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **완료**합니다.

    ![설치 완료](aspnet-mvc-4-fundamentals/_static/image46.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. 로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.

    ![VS Express for Web 타일](aspnet-mvc-4-fundamentals/_static/image47.png)

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

    ![Windows Azure 포털에 로그온](aspnet-mvc-4-fundamentals/_static/image48.png "Windows Azure 포털에 로그온")

    *Windows Azure 관리 포털에 로그온*
2. 클릭 **새로 만들기** 명령 모음에서.

    ![새 웹 사이트를 만드는](aspnet-mvc-4-fundamentals/_static/image49.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. 클릭 **계산** | **웹 사이트**합니다. 선택한 **빨리 만들기** 옵션입니다. 새 웹 사이트를 사용할 수 있는 URL을 제공 하 고 클릭 **웹 사이트 만들기**합니다.

    > [!NOTE]
    > Windows Azure 웹 사이트는 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트. 빠른 생성 옵션을 사용 하면 완료 된 웹 응용 프로그램을 Windows Azure에서 웹 사이트 포털 외부에서 배포할 수 있습니다. 데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](aspnet-mvc-4-fundamentals/_static/image50.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.
5. 웹 사이트를 만든 후 아래의 링크를 클릭 합니다 **URL** 열입니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트를 찾아](aspnet-mvc-4-fundamentals/_static/image51.png "새 웹 사이트를 검색 합니다.")

    *새 웹 사이트를 검색합니다.*

    ![실행 중인 웹 사이트](aspnet-mvc-4-fundamentals/_static/image52.png "실행 중인 웹 사이트")

    *실행 중인 웹 사이트*
6. 포털로 돌아가서에서 웹 사이트의 이름을 클릭 합니다 **이름을** 관리 페이지를 표시 하는 열입니다.

    ![웹 사이트 관리 페이지를 열어](aspnet-mvc-4-fundamentals/_static/image53.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. **대시보드** 페이지의 **간략 상태** 섹션을 클릭 합니다 **게시 프로필 다운로드** 링크.

    > [!NOTE]
    > 합니다 *게시 프로필* 모든 각각의 설정 된 게시 방법에 대 한 Windows Azure 웹 사이트를 웹 응용 프로그램을 게시 하는 데 필요한 정보를 포함 합니다. 게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열을 포함 합니다. **Microsoft WebMatrix 2**하십시오 **Microsoft Visual Studio Express for Web** 하 고 **Microsoft Visual Studio 2012** 읽기 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화할 Windows Azure websites에 웹 응용 프로그램을 게시합니다.

    ![게시 프로필 다운로드 웹 사이트](aspnet-mvc-4-fundamentals/_static/image54.png "게시 프로필 다운로드 웹 사이트")

    *게시 프로필 다운로드 웹 사이트*
8. 알려진된 위치에 게시 프로필 파일을 다운로드 합니다. 추가이 연습에서이 파일을 사용 하 여 Visual Studio에서 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 방법을 표시 됩니다.

    ![게시 프로필 파일을 저장](aspnet-mvc-4-fundamentals/_static/image55.png "게시 프로필 저장")

    *게시 프로필 파일을 저장 하는 중*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL 서버를 사용할 경우 데이터베이스를 SQL Database 서버 만들기 해야 합니다. SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하는 것에 대 한 SQL Database 서버를 해야 합니다. Windows Azure 관리 포털에서 구독의 SQL Database 서버를 볼 수 있습니다 **Sql Database** | **서버** | **서버 대시보드**합니다. 만든 서버가 없는 경우 하나를 사용 하 여 만들 수 있습니다 합니다 **추가** 명령 모음에서 단추입니다. 기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**처럼 다음 작업에서 사용 됩니다. 만들지 마십시오 데이터베이스 아직 이후 단계에서 만들어집니다.

    ![SQL Database 서버 대시보드](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database 서버 대시보드")

    *SQL Database 서버 대시보드*
2. 다음 태스크에서는 테스트 Visual Studio에서 데이터베이스 연결 서버 목록에 로컬 IP 주소를 포함 해야 하는 이유로 **허용 된 IP 주소**합니다. 이렇게 하려면 클릭 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여 넣습니다 합니다 **시작 IP 주소** 및 **끝IP주소** 입력란을 클릭 합니다 ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) 단추입니다.

    ![클라이언트 IP 주소를 추가합니다.](aspnet-mvc-4-fundamentals/_static/image58.png)

    *클라이언트 IP 주소를 추가합니다.*
3. 한 번 합니다 **클라이언트 IP 주소** 허용 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 변경을 확인 합니다.

    ![변경 확인](aspnet-mvc-4-fundamentals/_static/image59.png)

    *변경 확인*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션 돌아갑니다. 에 **솔루션 탐색기**, 웹 사이트 프로젝트를 마우스 오른쪽 단추로 **게시**합니다.

    ![응용 프로그램 게시](aspnet-mvc-4-fundamentals/_static/image60.png "응용 프로그램 게시")

    *웹 사이트를 게시합니다.*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필 가져오기](aspnet-mvc-4-fundamentals/_static/image61.png "게시 프로필 가져오기")

    *게시 프로필 가져오기*
3. 클릭 **연결의 유효성을 검사**합니다. 유효성 검사가 완료 되 면 클릭 **다음**합니다.

    > [!NOTE]
    > 연결 유효성 검사 단추 옆에 나타나는 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.

    ![연결 유효성 검사](aspnet-mvc-4-fundamentals/_static/image62.png "연결 유효성 검사")

    *연결 유효성 검사*
4. 에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추를 클릭 (즉 **DefaultConnection**).

    ![웹 배포 구성](aspnet-mvc-4-fundamentals/_static/image63.png "웹 배포 구성")

    *웹 배포 구성*
5. 데이터베이스 연결을 다음과 같이 구성 합니다.

   - 에 **서버 이름** SQL Database 서버 URL 사용 하 여 입력 합니다 *tcp:* 접두사입니다.
   - **사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 서버 관리자 로그인 암호를 입력 합니다.
   - 예를 들어 새 데이터베이스 이름을 입력 합니다. *MVC4SampleDB*합니다.

     ![대상 연결 문자열 구성](aspnet-mvc-4-fundamentals/_static/image64.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 다음 **확인**을 클릭합니다. 데이터베이스를 만들라는 메시지가 나오면 **예**합니다.

    ![데이터베이스를 만드는](aspnet-mvc-4-fundamentals/_static/image65.png "데이터베이스 문자열 만들기")

    *데이터베이스 만들기*
7. 기본 연결 텍스트 상자 내에서 사용 하 여 Windows Azure에서 SQL Database에 연결 하는 연결 문자열 표시 됩니다. **다음**을 클릭합니다.

    ![SQL Database를 가리키는 연결 문자열](aspnet-mvc-4-fundamentals/_static/image66.png "SQL 데이터베이스를 가리키는 연결 문자열")

    *SQL Database를 가리키는 연결 문자열*
8. 에 **미리 보기** 페이지에서 클릭 **게시**합니다.

    ![웹 응용 프로그램 게시](aspnet-mvc-4-fundamentals/_static/image67.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.

    ![Windows Azure에 응용 프로그램 게시](aspnet-mvc-4-fundamentals/_static/image68.png "응용 프로그램이 Windows Azure에 게시")

    *Windows Azure에 게시 하는 응용 프로그램*

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>부록 c: 코드 조각 사용

코드 조각을 사용 하 여 결정적인 순간에 필요한 모든 코드를 해야 합니다. 랩 문서가 알려줍니다 정확 하 게 사용할 수 있는 시기를 다음 그림과 같습니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드를 삽입할](aspnet-mvc-4-fundamentals/_static/image69.png "프로젝트에 코드를 삽입 하는 Visual Studio를 사용 하 여 코드 조각을")

*프로젝트에 코드를 삽입 하려면 Visual Studio 코드 조각 사용*

***키보드 (C#만 해당)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드를 삽입 하려는 위치에 커서를 놓습니다.
2. 시작 (공백 없이 하이픈) 조각 이름을 입력 합니다.
3. IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.
4. 올바른 코드 조각을 선택 합니다 (또는 전체 코드 조각 이름을 선택 될 때까지 입력 유지).
5. 커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.

![코드 조각 이름을 입력](aspnet-mvc-4-fundamentals/_static/image70.png "조각 이름을 입력 하기 시작")

*코드 조각 이름을 입력 하기 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각을](aspnet-mvc-4-fundamentals/_static/image71.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")

*Tab 키를 눌러 강조 표시 된 코드 조각 선택*

![Tab 키를 다시 코드 조각 확장 됩니다](aspnet-mvc-4-fundamentals/_static/image72.png "다시 Tab 키를 누릅니다 하 고 코드 조각에서는 확장")

*Tab 키를 다시 및 코드 조각에서는 확장*

***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가할*** 1입니다. 코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.

1. 선택 **코드 조각 삽입** 뒤 **내 코드 조각**합니다.
2. 클릭 하 여 목록에서 관련 코드 조각을 선택 합니다.

![코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-fundamentals/_static/image73.png "코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭")

*코드 조각을 삽입할 선택한 코드 조각 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭*

![클릭 하 여 목록에서 관련 코드 조각 선택](aspnet-mvc-4-fundamentals/_static/image74.png "클릭 하 여 목록에서 관련 코드 조각 선택")

*클릭 하 여 목록에서 관련 코드 조각 선택*
