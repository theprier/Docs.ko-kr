---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 도우미, 폼 및 유효성 검사 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 모델 및 데이터 액세스 실습 랩 하면 로드 되어 데이터베이스에서 데이터를 표시 합니다. 에 추가 합니다이 실습 랩에서 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 4cfa98144919c3f1bdb3608970af1a7952fe6ea7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a>ASP.NET MVC 4 도우미, 폼 및 유효성 검사

으로 [웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트를 다운로드 합니다.](https://aka.ms/webcamps-training-kit)

**ASP.NET MVC 4 모델 및 데이터 액세스** 실습 랩 되었습니다 로드 하 고 데이터베이스에서 데이터를 표시 합니다. 에 추가 합니다이 실습 랩에서 **Music Store** 응용 프로그램이 해당 데이터를 편집할 수 있는 기능입니다.

해당 목표를 염두에서에 두고 앨범의 만들기, 읽기, 업데이트 및 삭제 (CRUD) 작업을 지 원하는 컨트롤러는 먼저 만듭니다. HTML 표에 앨범 속성을 표시 하려면 ASP.NET MVC 스 캐 폴딩 기능을 활용 하는 인덱스 뷰 서식 파일을 생성 합니다. 해당 보기를 강화 하려면 긴 설명을 잘립니다 하는 사용자 지정 HTML 도우미를 추가 합니다.

그 후에 편집 하며 수 있는 뷰 만들기 alter 앨범 드롭다운 같은 폼 요소를 사용 하 여 데이터베이스에 추가 합니다.

마지막으로, 앨범을 삭제 하는 사용자 수와 있습니다 됩니다 수 없게 입력을 확인 하 여 잘못 된 데이터를 입력 합니다.

이 실습 랩 대 한 기본 지식이 있다고 가정 하 고 **ASP.NET MVC**합니다. 사용 하지 않은 경우 **ASP.NET MVC** 를 권장 앞, **ASP.NET MVC의 기본 사항** 실습 랩입니다.

이 랩에서 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 내용을 적용 하 여 이전에 설명 된 새로운 기능 및 향상 된 기능을 통해 설명 합니다.

> [!NOTE]
> 모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다. 이 랩에 특정 프로젝트에서 사용할 수는 [ASP.NET MVC 4 도우미, 폼 및 유효성 검사](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)합니다.

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 배우게 됩니다 하는 방법:

- CRUD 작업을 지 원하는 컨트롤러 만들기
- HTML 테이블에 엔터티 속성을 표시 하는 인덱스 뷰를 생성 합니다.
- 사용자 지정 HTML 도우미를 추가 합니다.
- 만들기 및 편집 보기를 사용자 지정
- HTTP GET 또는 HTTP POST 호출에 반응 하는 작업 메서드를 구별
- 추가 및 Create View를 사용자 지정
- 엔터티 삭제 처리
- 사용자 입력 유효성 검사

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>설정

**설치 하는 코드 조각**

편의 위해는이 랩에 따라 관리 코드의 대부분 Visual Studio 코드 조각 수 있습니다. 실행 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.

이 문서에서 부록을 참조할 수 사용 하는 방법에 알아봅니다 사용 하 고 Visual Studio 코드 조각에 익숙한 경우 &quot; [부록 b:를 사용 하 여 코드 조각을](#AppendixB)&quot;합니다.

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>연습

다음 연습 실습 랩이를 구성합니다.

1. [저장소 관리자 컨트롤러 및 해당 인덱스 뷰 만들기](#Exercise1)
2. [HTML 도우미를 추가합니다.](#Exercise2)
3. [편집 뷰 만들기](#Exercise3)
4. [만들기 뷰 추가](#Exercise4)
5. [삭제를 처리합니다.](#Exercise5)
6. [유효성 검사 추가](#Exercise6)
7. [클라이언트 쪽에서 비 가시적인 jQuery를 사용 하 여](#Exercise7)

> [!NOTE]
> 각 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다. 연습을 통해 작업 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.


예상 소요 시간: **60 분**

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a>연습 1: 저장소 관리자 컨트롤러 및 해당 인덱스 뷰 만들기

이 연습에서는 데이터베이스와 마지막으로 ASP.NET MVC 스 캐 폴딩을 활용 하는 인덱스 뷰 서식 파일 생성 중에서 앨범의 목록을 반환 하는 인덱스 작업 메서드를 사용자 지정을 CRUD 작업을 지원 하려면 새 컨트롤러를 만드는 방법을 배우게 됩니다. HTML 표에 앨범 속성을 표시 하는 기능입니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a>작업 1-는 StoreManagerController 만들기

이 작업을 호출 하는 새 컨트롤러 만듭니다 **StoreManagerController** CRUD 작업을 지원 합니다.

1. 열기는 **시작** 솔루션에 있는 **소스/e x 1-CreatingTheStoreManagerController/시작/** 폴더입니다.

   1. 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 전에 계속 합니다. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 새 컨트롤러를 추가 합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **컨트롤러** 선택 솔루션 탐색기에서 폴더 **추가** 차례로 **컨트롤러** 명령입니다. 변경 된 **컨트롤러** **이름** 를 **StoreManagerController** 옵션 있는지 확인 하 고 **빈읽기/쓰기동작이포함된MVC컨트롤러**을 선택 합니다. **추가**를 클릭합니다.

    ![추가 컨트롤러 대화](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "추가 컨트롤러 대화 상자")

    *컨트롤러 추가 대화 상자*

    새 컨트롤러 클래스가 생성 됩니다. 스텁 메서드,에 대 한 읽기/쓰기에 대 한 작업을 추가 하려면 표시 된 이후 응용 프로그램별 논리를 포함 하는 메시지를 입력할 TODO 주석을 사용 하 여 일반적인 위한 CRUD 동작이 생성 됩니다.

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a>작업 2-StoreManager 인덱스를 사용자 지정

이 작업에서는 데이터베이스에서 앨범 목록 사용 하 여 뷰를 반환 하기 StoreManager Index 동작 메서드를 사용자 지정 합니다.

1. StoreManagerController 클래스에 다음 추가 *를 사용 하 여* 지시문입니다.

    (코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-e x 1 MvcMusicStore를 사용 하 여*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. 필드를 추가 하는 **StoreManagerController** 의 인스턴스를 포함 하려면 **MusicStoreEntities 합니다.**

    (코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-e x 1 MusicStoreEntities*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. 앨범 목록 사용 하 여 뷰를 반환 하 여 StoreManagerController 인덱스 작업을 구현 합니다.

    컨트롤러 동작 논리 매우 유사 StoreController의 인덱스 동작이 이전에 작성 됩니다. LINQ를 사용 하 여 표시를 위해 Genre 및 음악가 정보를 포함 한 모든 앨범, 검색할.

    (코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-e x 1 StoreManagerController 인덱스*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a>작업 3-인덱스 보기를 만드는 방법

이 태스크에서는에서 반환 되는 앨범의 목록을 표시 하려면 인덱스 뷰 템플릿을 만들어집니다는 **StoreManager** 컨트롤러입니다.

1. 새 보기 서식 파일을 만들기 전에 프로젝트를 작성 해야 하는 **보기 대화 상자 추가** 에 대해 알고는 **앨범** 클래스를 사용 합니다. 선택 **빌드 | 빌드 MvcMusicStore** 프로젝트를 빌드합니다.
2. 마우스 오른쪽 단추로 클릭는 **인덱스** 동작 메서드와 선택 **뷰 추가**합니다. 그러면 표시 됩니다는 **뷰 추가** 대화 상자.

    ![뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "뷰 추가")

    *Index 메서드 내에서 뷰를 추가합니다.*
3. 뷰 추가 대화 상자에서 보기 이름 인지 확인 **인덱스**합니다. 선택 된 **강력한 형식의 뷰 만들기** 옵션을 선택 **앨범 (MvcMusicStore.Models)** 에서 **모델 클래스** 드롭 다운 합니다. 선택 **목록** 에서 **스 캐 폴드 템플릿이** 드롭 다운 합니다. 둡니다는 **뷰 엔진** 를 **Razor** 와 해당 기본값은 다른 필드 값을 클릭 한 다음 **추가**합니다.

    ![인덱스 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "인덱스 뷰 추가")

    *인덱스 뷰 추가*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a>작업 4-인덱스 보기의 스 캐 폴드를 사용자 지정

이 태스크에서는 원하는 필드를 표시 하도록 ASP.NET MVC 스 캐 폴딩 기능을 사용 하 여 만든 간단한 뷰 템플릿을 조정 합니다.

> [!NOTE]
> **스 캐 폴딩** 앨범 모델의 모든 필드를 나열 하는 간단한 보기 서식 파일을 생성 하는 ASP.NET MVC 내에서 지원 합니다. **스 캐 폴딩** 강력한 형식의 뷰에서 시작 하는 빠른 방법을 제공: 신속 하 게 스 캐 폴딩 템플릿 보기를 수동으로 작성 하는 대신 기본 템플릿을 생성 하 고 그런 다음 생성된 된 코드를 수정할 수 있습니다.


1. 작성 한 코드를 검토 합니다. 생성 된 필드 목록에는 다음의 일부가 될 HTML 테이블 **스 캐 폴딩** 표 형식 데이터를 표시 하기 위해 사용 합니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. 대체는 **&lt;테이블&gt;** 만 표시 하는 다음 코드를 사용 하 여 코드의 **장르**, **아티스트**, **앨범 제목**, 및 **가격** 필드입니다. 그러면 삭제는 **AlbumId** 및 **앨범 아트 URL** 열입니다. 또한 해당 연결 된 클래스 속성을 표시 GenreId 및 ArtistId 열을 변경 **Artist.Name** 및 **Genre.Name**를 제거 하 고는 **세부 정보** 링크 합니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. 다음 설명을 변경 합니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>5-응용 프로그램 실행 작업

에서는이 작업을 테스트 하는 **StoreManager** **인덱스** 템플릿 보기에는 이전 단계의 디자인에 따라 앨범 목록이 표시 됩니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **/StoreManager** 보여 주는 목록이 앨범 표시 되는지 확인 하려면 해당 **제목**, **아티스트** 및 **장르**합니다.

    ![앨범 목록을 찾는](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "앨범 목록 탐색")

    *앨범 목록 탐색*

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a>연습 2: HTML 도우미를 추가합니다.

StoreManager 인덱스 페이지에 하나 이상의 잠재적인 문제가: 제목 및 아티스트 Name 속성은 모두 테이블 서식 지정에 충분 합니다. 이 연습에서는 해당 텍스트를 잘라내려면 사용자 지정 HTML 도우미를 추가 하는 방법에 설명 합니다.

다음 그림에는 작은 브라우저 크기를 사용 하는 경우 텍스트의 길이 때문에 형식이 수정 되는 방법을 확인할 수 있습니다.

![잘린 텍스트와 앨범의 목록을 검색 하지](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "텍스트 잘리지 앨범으로 목록 검색")

*텍스트 잘리지와 앨범 목록 탐색*

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a>작업 1-확장 된 HTML 도우미

이 태스크에서는 새 메서드 추가 **Truncate** 에 **HTML** ASP.NET MVC 뷰 내에서 노출 된 개체입니다. 이 수행 하려면 구현 합니다는 **확장 메서드** 기본 제공 되 **System.Web.Mvc.HtmlHelper** ASP.NET MVC에서 제공 하는 클래스입니다.

> [!NOTE]
> 에 대 한 자세한 내용은 **확장 메서드**,이 msdn 문서를 참조 하십시오. [https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).


1. 열기는 **시작** 솔루션에 있는 **소스/e x 2-AddingAnHTMLHelper/시작/** 폴더입니다. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. StoreManager의 인덱스 뷰를 엽니다. 이렇게 하려면 솔루션 탐색기에서 확장 하 고는 **뷰** 폴더는 다음 **StoreManager** 엽니다는 **Index.cshtml** 파일입니다.
3. 아래에 다음 코드를 추가 <strong>@model</strong> 지시문을 정의 하는 <strong>Truncate</strong> 도우미 메서드입니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a>작업 2-잘라내기가 텍스트 페이지

이 작업을 사용 하 여는 **Truncate** 템플릿 보기에에서 있는 텍스트를 잘라내려면 메서드.

1. StoreManager의 인덱스 뷰를 엽니다. 이렇게 하려면 솔루션 탐색기에서 확장 하 고는 **뷰** 폴더는 다음 **StoreManager** 엽니다는 **Index.cshtml** 파일입니다.
2. 표시 된 줄을 바꿀는 **음악가 이름** 및 앨범 **제목**합니다. 이 작업을 수행 하려면 다음 줄을 바꿉니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>작업 3-응용 프로그램 실행

에서는이 작업을 테스트 하는 **StoreManager** **인덱스** 앨범의 제목 및 아티스트 이름 템플릿 보기를 자릅니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **/StoreManager** 해당 장기 확인 하려면 텍스트에는 **제목** 및 **아티스트** 열은 잘립니다.

    ![제목 및 예술가 이름이 잘립니다](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "잘린 제목과 예술가 이름")

    *잘린 제목과 아티스트 이름*

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a>연습 3: 편집 보기를 만드는 방법

이 연습에서는 매장 관리자 앨범을 편집할 수 있도록 폼을 만드는 방법에 설명 합니다. 찾아보기 됩니다는 **/StoreManager/Edit/id** URL (**id** 되 편집 하는 앨범의 고유 id), 서버에 대 한 HTTP GET 호출 하 합니다.

컨트롤러 Edit 동작 메서드는 데이터베이스에서 적절 한 앨범 검색, 만들기는 **StoreManagerViewModel** 목록 아티스트, 장르), (함께 캡슐화 한 다음 보기 서식 파일에 전달할 개체 다시 사용자에 게 HTML 페이지를 렌더링 합니다. 이 페이지에 포함 됩니다는 **&lt;양식&gt;** 텍스트 상자 및 드롭다운 앨범 속성 편집에 있는 요소입니다.

사용자 앨범 양식 값을 업데이트 하 고 클릭 한 후의 **저장** 의 변경 내용을 통해 제출 단추를 HTTP POST를 다시 호출 **/StoreManager/Edit/id**합니다. URL 마지막 호출에서와 동일 하 게 유지, 있지만 ASP.NET MVC 식별 하는 HTTP 게시 되 고 다른 편집 동작 메서드를 실행 하므로이 시간 (로 데코레이팅 하나 **[HttpPost]**).

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a>작업 1-HTTP GET 편집 동작 메서드를 구현 합니다.

이 작업에서는 HTTP GET 버전의 데이터베이스에서 적절 한 앨범을 가져오려는 편집 작업 메서드 뿐 아니라 모든 장르 및 예술가 목록을 구현 합니다. 로이 데이터 패키징하고 것은 **StoreManagerViewModel** 다음 응답을 렌더링 하는 보기 템플릿을에 전달 될는 마지막 단계에서 정의 된 개체입니다.

1. 열기는 **시작** 솔루션에 있는 **소스/Ex3-CreatingTheEditView/시작/** 폴더입니다. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 열기는 **StoreManagerController** 클래스입니다. 이 작업을 수행 하려면 확장 된 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.
3. 대체는 **HTTP GET 편집** 동작 메서드를 다음 코드로를 적절 한 검색 **앨범** 으로 **장르** 및 **예술가**나열 합니다.

    (코드 조각- *ASP.NET MVC 4 도우미와 폼 및 유효성 검사-작업 Ex3 StoreManagerController HTTP GET 편집*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > 사용 중인 **System.Web.Mvc** **SelectList** 아티스트, 대신 장르에 대 한는 **System.Collections.Generic** 목록입니다.
    > 
    > **SelectList** HTML 드롭다운 목록 채우기 등으로 현재 선택 영역을 관리 하는 보다 명확한 방법이 됩니다. 하 고 컨트롤러 작업에서 이러한 ViewModel 개체를 이상으로 설정 하면 편집 폼 시나리오 클리너 있습니다.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a>작업 2-편집 보기를 만드는 방법

이 태스크에서는 나중에 앨범 속성을 표시 하는 보기 편집 템플릿을 만듭니다.

1. 편집 뷰를 만듭니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **편집** 동작 메서드와 선택 **뷰 추가**합니다.
2. 뷰 추가 대화 상자에서 보기 이름 인지 확인 **편집**합니다. 확인는 **강력한 형식의 뷰 만들기** 확인란을 선택 하 고 **앨범 (MvcMusicStore.Models)** 에서 **데이터 클래스 보기** 드롭 다운 합니다. 선택 **편집** 에서 **스 캐 폴드 템플릿이** 드롭 다운 합니다. 다른 필드를 기본값으로 두고 클릭 **추가**합니다.

    ![편집 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "편집 뷰 추가")

    *편집 뷰 추가*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>작업 3-응용 프로그램 실행

에서는이 작업을 테스트 하는 **StoreManager** **편집** 보기 페이지에 매개 변수로 전달 된 앨범에 대 한 속성의 값이 표시 됩니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **/StoreManager/Edit/1** 에 전달 된 앨범에 대 한 속성의 값이 표시 되는지 확인 합니다.

    ![앨범 편집 보기 찾아보기](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "앨범 편집 보기 찾아보기")

    *앨범 편집 보기 찾아보기*

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a>작업 4-앨범 편집기 서식 파일에서 구현 하는 드롭다운 목록

이 태스크에서는 추가 합니다 드롭다운 목록 마지막 작업에서 만든 템플릿 보기에 사용자 예술가 및 장르 목록에서 선택할 수 있도록 합니다.

1. 모두 바꾸기는 **앨범** 필드 집합 코드를 다음 코드로:

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > **Html.DropDownList** 도우미 렌더링 아티스트, 장르 선택에 대 한 드롭다운 목록에 추가 되었습니다. 매개 변수가 전달 **Html.DropDownList** 됩니다.
    > 
    > 1. 양식 필드의 이름 (**&quot;ArtistId&quot;**).
    > 2. **SelectList** 드롭다운 목록에 대 한 값입니다.

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>5-응용 프로그램 실행 작업

에서는이 작업을 테스트 하는 **StoreManager** **편집** 보기 페이지 아티스트 및 장르 ID 텍스트 필드 대신 드롭다운 목록에 표시 됩니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **/StoreManager/Edit/1** 아티스트 및 장르 ID 텍스트 필드 대신 드롭다운을 표시 되는지 확인 하려면.

    ![검색 드롭다운 있는 앨범 편집 뷰](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "검색 앨범 드롭다운와 보기 편집")

    *검색 앨범 편집 보기,이 이번에는 드롭다운 목록*

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a>태스크 6-HTTP POST Edit 동작 메서드를 구현 합니다.

보기 편집 예상 대로 나타나면 했으므로 앨범에 변경한 내용을 저장 하려면 작업을 편집 하는 HTTP POST 메서드를 구현 해야 합니다.

1. Visual Studio 창에 반환 하는 데 필요한 경우 브라우저를 닫습니다. 열기 **StoreManagerController** 에서 **컨트롤러** 폴더입니다.
2. 대체 **HTTP POST 편집** 동작 메서드 코드를 다음 코드로 (참고: 두 개의 매개 변수를 수신 하는 오버 로드 된 버전을 교체 해야 하는 방법).

    (코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-작업 Ex3 StoreManagerController HTTP POST 편집*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > 이 메서드는 사용자가 클릭할 때 실행 됩니다는 **저장** 보기의 단추는 HTTP-POST 서버에 다시 폼 값의 데이터베이스에 유지 하도록를 수행 합니다. Decorator **[HttpPost]** HTTP POST 한 시나리오에 메서드를 사용 해야을 나타냅니다. 메서드를 사용 하며는 **앨범** 개체입니다. ASP.NET MVC는 게시 된에서 앨범 개체를 자동으로 만들 됩니다 &lt;양식&gt; 값입니다.
    > 
    > 메서드는 다음이 단계를 수행 합니다.
    > 
    > 1. 모델이 유효한 경우:
    > 
    >     1. 수정된 된 개체로 표시 하는 컨텍스트에서 앨범 항목을 업데이트 합니다.
    >     2. 변경 내용을 저장 하 고 인덱스 뷰 리디렉션됩니다.
    > 2. 모델이 유효 하지 않을 경우와 ViewBag 채웁니다는 **GenreId** 및 **ArtistId**, 사용자 수를 받은 앨범 개체를 사용 하 여 뷰 반환 됩니다 모든 필수 업데이트를 수행 합니다.

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>7-응용 프로그램 실행 작업

에서는이 작업을 테스트 하는 **StoreManager 편집** 뷰 페이지는 데이터베이스에 실제로 업데이트 된 앨범 데이터를 저장 합니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **/StoreManager/Edit/1**합니다. 앨범 제목을 변경 **부하** 을 클릭할 **저장**합니다. 앨범 제목 앨범 목록에서 실제로 변경 되었는지 확인 합니다.

    ![앨범 업데이트](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "앨범 업데이트")

    *앨범 업데이트*

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a>만들기 뷰를 추가 하는 연습 4:

이제는 **StoreManagerController** 지원는 **편집** 기능 저장할 수 있도록 Create View 템플릿을 추가 하는 방법을 배우게 됩니다이 연습에서는 응용 프로그램에 새 앨범을 추가 하는 관리자입니다.

내에서 두 개의 별도 메서드를 사용 하 여 만들기 시나리오를 구현 합니다 편집 기능을 갖춘 했던 것 처럼는 **StoreManagerController** 클래스:

1. 저장소 관리자를 처음 방문할 때 하나의 작업 메서드가 빈 폼 표시 됩니다는 **/StoreManager/만들기** URL입니다.
2. 두 번째 동작 메서드를 처리할 시나리오 저장소 관리자는 클릭할 수 있는 **저장** 폼 내에서 단추에 값을 다시 전송 하는 **/StoreManager/만들기** HTTP POST로 써는 URL입니다.

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a>작업 1-HTTP GET 만들 동작 메서드 구현

이 작업에서는 HTTP GET 버전의 모든 장르와 예술가 목록을 검색,이 데이터에 패키지를 만들기 작업 메서드를 구현 합니다는 **StoreManagerViewModel** 개체 보기 서식 파일에 전달 될 다음입니다.

1. 열기는 **시작** 솔루션에 있는 **소스/Ex4-AddingACreateView/시작/** 폴더입니다. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 열기 **StoreManagerController** 클래스입니다. 이 작업을 수행 하려면 확장 된 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.
3. 대체는 **만들기** 동작 메서드 코드를 다음 코드로:

    (코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-Ex4 StoreManagerController HTTP GET 만들기 동작*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a>작업 2-만들기 뷰 추가

이 태스크에서는 새 (비어 있음) 앨범 폼을 표시 하는 Create View 서식 파일을 추가 합니다.

1. 마우스 오른쪽 단추로 클릭는 **만들기** 동작 메서드와 선택 **뷰 추가**합니다. 이 뷰 추가 대화 상자를 표시 합니다.
2. 뷰 추가 대화 상자에서 보기 이름 인지 확인 **만들기**합니다. 선택 된 **강력한 형식의 뷰 만들기** 및 옵션을 선택 **앨범 (MvcMusicStore.Models)** 에서 **모델 클래스** 드롭 다운 및 **만들기** 에서 **스 캐 폴드 템플릿이** 드롭 다운 합니다. 다른 필드를 기본값으로 두고 클릭 **추가**합니다.

    ![만들기 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "추가-a-만들기-view.png")

    *만들기 뷰 추가*
3. 업데이트는 **GenreId** 및 **ArtistId** 아래 표시 된 것 처럼 드롭 다운 목록을 사용 하는 필드:

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>작업 3-응용 프로그램 실행

에서는이 작업을 테스트 하는 **StoreManager** **만들기** 빈 앨범 폼 보기 페이지에 표시 됩니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **/StoreManager/만들기**합니다. 새 앨범 속성을 채우기 위한 빈 폼이 표시 되는지 확인 합니다.

    ![Create View 빈 양식으로](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "빈 양식으로 보기 만들기")

    *빈 폼 보기 만들기*

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a>작업 4-구현 HTTP POST 작업 메서드 만들기

이 작업에서는 Create 작업 메서드는 사용자가 클릭할 때 호출 되는 HTTP POST 버전을 구현 합니다는 **저장** 단추입니다. 메서드는 데이터베이스에 새 앨범을 저장 해야 합니다.

1. Visual Studio 창에 반환 하는 데 필요한 경우 브라우저를 닫습니다. 열기 **StoreManagerController** 클래스입니다. 이 작업을 수행 하려면 확장 된 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.
2. 대체 **HTTP POST 만들** 동작 메서드 코드를 다음 코드로:

    (코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-Ex4 StoreManagerController HTTP POST 만들기 작업*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > 만들기 작업은 이전 편집 작업 메서드와 매우 유사 하지만 수정 된 개체를 설정 하는 대신 컨텍스트에 추가 되 고 됩니다.

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>5-응용 프로그램 실행 작업

에서는이 작업을 테스트 하는 **StoreManager 만들** 보기 페이지 새 앨범을 만들 수 있습니다 및 StoreManager 인덱스 뷰를 리디렉션합니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **/StoreManager/만들기**합니다. 다음 그림에서와 같은 새 앨범에 대 한 데이터 사용 모든 양식 필드를 입력 합니다.

    ![앨범 만드는](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "앨범 만들기")

    *앨범 만들기*
3. 방금 만든 새 앨범을 포함 하는 StoreManager 인덱스 보기도 리디렉션됩니다 있는지 확인 합니다.

    ![만든 새 앨범](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "만든 새 앨범")

    *만든 새 앨범*

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a>삭제를 처리 하는 연습 5:

앨범을 삭제 하는 기능이 아직 구현 되지 않았습니다. 에 대 한이 연습은 것입니다. 내에서 두 개의 별도 메서드를 사용 하 여 Delete 시나리오를 구현 합니다 이전 처럼는 **StoreManagerController** 클래스:

1. 하나의 작업 메서드 확인 폼이 표시 됩니다.
2. 두 번째 동작 메서드를 처리할 양식 전송

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a>작업 1-HTTP GET Delete 동작 메서드를 구현 합니다.

이 태스크는 앨범의 정보를 검색 하는 Delete 동작 메서드의 GET HTTP 버전을 구현 합니다.

1. 열기는 **시작** 솔루션에 있는 **소스/Ex5-HandlingDeletion/시작/** 폴더입니다. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 열기 **StoreManagerController** 클래스입니다. 이 작업을 수행 하려면 확장 된 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.
3. Delete 컨트롤러 작업은 정확 하 게 이전 저장소 세부 정보 컨트롤러 작업와 동일: 쿼리하여는 **앨범** 사용 하 여 데이터베이스에서 개체는 **id** URL과 반환에서 제공 되는 적절 한 **보기**합니다. 이 작업을 수행 하려면 HTTP GET을 대체 **삭제** 동작 메서드 코드를 다음 코드로:

    (코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-Ex5 처리 삭제 HTTP GET 삭제 작업*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. 마우스 오른쪽 단추로 클릭는 **삭제** 동작 메서드와 선택 **뷰 추가**합니다. 이 뷰 추가 대화 상자를 표시 합니다.
5. 뷰 추가 대화 상자에서 보기 이름 인지 확인 **삭제**합니다. 선택 된 **강력한 형식의 뷰 만들기** 및 옵션을 선택 **앨범 (MvcMusicStore.Models)** 에서 **모델 클래스** 드롭 다운 합니다. 선택 **삭제** 에서 **스 캐 폴드 템플릿이** 드롭 다운 합니다. 다른 필드를 기본값으로 두고 클릭 **추가**합니다.

    ![삭제 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "삭제 뷰 추가")

    *삭제 뷰 추가*
6. Delete 템플릿 모델에서 모든 필드를 표시 합니다. 앨범 제목에만 표시 됩니다. 이렇게 하려면 보기의 내용을 다음 코드로 바꿉니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>작업 2-응용 프로그램 실행

에서는이 작업을 테스트 하는 **StoreManager** **삭제** 확인 삭제 양식 보기 페이지에 표시 됩니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **/StoreManager**합니다. 클릭 하 여 삭제할 하나 앨범 선택 **삭제** 새 보기는 업로드 되었는지 확인 합니다.

    ![앨범 삭제](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "앨범 삭제")

    *앨범 삭제*

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a>작업 3-HTTP POST Delete 동작 메서드를 구현 합니다.

이 작업을 클릭할 때 호출 되는 Delete 동작 메서드의 POST HTTP 버전을 구현 합니다는 **삭제** 단추입니다. 메서드는 앨범의 데이터베이스에서 삭제 해야 합니다.

1. Visual Studio 창에 반환 하는 데 필요한 경우 브라우저를 닫습니다. 열기 **StoreManagerController** 클래스입니다. 이 작업을 수행 하려면 확장 된 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.
2. 대체 **HTTP POST 삭제** 동작 메서드 코드를 다음 코드로:

    (코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-Ex5 처리 삭제 HTTP POST 삭제 작업*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

에서는이 작업을 테스트 하는 **StoreManager Delete** 보기 페이지에서는 앨범을 삭제할 수 있습니다 및 StoreManager 인덱스 뷰를 리디렉션합니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **/StoreManager**합니다. 클릭 하 여 삭제할 하나 앨범 선택 **삭제 합니다.** 클릭 하 여 삭제를 확인 **삭제** 단추:

    ![앨범 삭제](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "앨범 삭제")

    *앨범 삭제*
3. 앨범에 나타나지 않도록 이후 삭제 되었는지 확인는 **인덱스** 페이지.

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a>실습 6: 유효성 검사 추가

현재 위치에 있는 만들기 및 편집 폼 유효성 검사를 수행 하지 않습니다. 사용자가 필수 필드를 비워 또는 형식 편지 price 필드에서를 완료 하는 경우에 데이터베이스에서 첫 번째 오류를 받게 됩니다 됩니다.

데이터 주석 모델 클래스를 추가 하 여 응용 프로그램에 유효성 검사를 추가할 수 있습니다. ASP.NET MVC에서 자동으로 처리를 적용 하 고 사용자에 게 적절 한 메시지를 표시 및 데이터 주석 모델 속성을 적용할 규칙을 설명 하는 허용 합니다.

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a>작업 1-데이터 주석 추가

이 작업에서는 적절 한 경우 유효성 검사 메시지를 표시 하는 데이터 주석 만들기 및 편집 페이지에 있도록 앨범 모델에 추가 합니다.

간단한 모델 클래스에 대 한 데이터 주석이 방금 처리 추가 추가 하 여 한 **를 사용 하 여** 문을 **System.ComponentModel.DataAnnotation**, 다음 배치는 **[필수]**적절 한 속성에는 특성입니다. 다음 예제에서는 하 게 만드는 **이름** 속성 보기에서 필수 필드입니다.

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

이 엔터티 데이터 모델 생성은이 응용 프로그램 같은 경우 좀 더 복잡 합니다. 데이터 주석 모델 클래스에 직접 추가한 데이터베이스에서 모델을 업데이트 하는 경우 덮어쓰게 됩니다. 만들 수는 대신, 됩니다 주석을 저장할 수 있고 모델에 연결 된 메타 데이터 부분 클래스를 사용 하 여 클래스를 사용 하는 **[MetadataType]** 특성입니다.

1. 열기는 **시작** 솔루션에 있는 **소스/Ex6-AddingValidation/시작/** 폴더입니다. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 열기는 **Album.cs** 에서 **모델** 폴더입니다.
3. 대체 **Album.cs** 을 다음과 같이 강조 표시 된 코드를 있는 콘텐츠:

    > [!NOTE]
    > 줄 **[DisplayFormat(ConvertEmptyStringToNull=false)]** 빈 문자열은 모델에서 데이터 원본에서 데이터 필드가 업데이트 되는 경우 null로 변환 되지 않습니다 나타냅니다. 이 설정은 데이터 주석 필드의 유효성을 검사 하기 전에 Entity Framework 모델에 null 값을 할당 하는 경우 예외가 필요가 없습니다.

    (코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-Ex6 앨범 메타 데이터에 대 한 partial 클래스*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > 이 **앨범** 부분 클래스에는 **MetadataType** 가리키는 특성은 **AlbumMetaData** 데이터 주석에 대 한 클래스입니다. 다음은 앨범 모델 주석을 사용 하는 데이터 주석을 특성 중 일부입니다.
    > 
    > - 필수-속성이 필수 필드 임을 나타냅니다.
    > - DisplayName-양식 필드 및 유효성 검사 메시지에 사용할 텍스트를 정의 합니다.
    > - DisplayFormat-데이터 필드가 표시 되 고 서식이 지정 되는 방식을 지정 합니다.
    > - StringLength-문자열 필드에 대 한 최대 길이 정의 합니다.
    > - 범위가-숫자 필드에 대 한 최대 및 최소 값을 제공 합니다.
    > - ScaffoldColumn-편집기 양식에서 필드를 숨길 수 있습니다.

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>작업 2-응용 프로그램 실행

에서는이 작업을 테스트 만들기 및 편집 페이지 필드의 유효성을 검사 마지막 작업에서 선택한 표시 이름을 사용 하 여 합니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **/StoreManager/만들기**합니다. 표시 이름이 partial 클래스에서 일치 하는지 확인 하십시오 (같은 **앨범 아트 URL** 대신 **AlbumArtUrl**)
3. 클릭 **만들기**를 폼 입력 하지 않고 있습니다. 해당 하는 유효성 검사 메시지 얻어지는 지 확인 합니다.

    ![필드 만들기 페이지에 유효성을 검사할](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "만들기 페이지의 필드 유효성 검사")

    *유효성 검사 필드 만들기 페이지*
4. 와 동일한 발생 하는지 확인할 수 있습니다는 **편집** 페이지. URL을 변경 **/StoreManager/Edit/1** 표시 이름에서 partial 클래스와 일치 하는지 확인 하 고 (같은 **앨범 아트 URL** 대신 **AlbumArtUrl**). 빈는 **제목** 및 **가격** 필드와 클릭 **저장**합니다. 해당 하는 유효성 검사 메시지 얻어지는 지 확인 합니다.

    ![편집 페이지의 유효성이 검사 된 필드](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    *편집 페이지의 유효성이 검사 된 필드*

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a>7 연습: 클라이언트 쪽에서 비 가시적인 jQuery를 사용 하 여

이 연습에서는 클라이언트 쪽에서 MVC 4 비 가시적인 jQuery 유효성 검사를 사용 하는 방법에 설명 합니다.

> [!NOTE]
> 비 가시적인 jQuery 데이터 ajax 접두사 JavaScript를 사용 하 여 영향을 주지 않고 내보내는 인라인 클라이언트 스크립트 아닌 서버에서 작업 메서드를 호출 합니다.


<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a>작업 1-사용 하도록 설정 비 가시적인 jQuery 전에 응용 프로그램 실행

이 작업을 모두 유효성 검사 모델을 비교 하기 위해 jQuery를 포함 하기 전에 응용 프로그램을 실행 합니다.

1. 열기는 **시작** 솔루션에 있는 **소스/Ex7-UnobtrusivejQueryValidation/시작/** 폴더입니다. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. **F5** 키를 눌러 응용 프로그램을 실행합니다.
3. 프로젝트 홈 페이지에서 시작합니다. 찾아보기 **/StoreManager/만들기** 클릭 **만들기** 폼 유효성 검사 메시지 얻어지는 지 확인을 채우지 않고:

    ![사용 하지 않도록 설정 하는 클라이언트 유효성 검사](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "사용 하지 않도록 설정 하는 클라이언트 유효성 검사")

    *클라이언트 유효성 검사를 사용 하지 않도록 설정*
4. 브라우저에서 HTML 소스 코드를 엽니다.

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a>작업 2-비 가시적인 클라이언트 유효성 검사를 사용 하도록 설정

이 태스크에서는 jQuery 하면 **비간섭 클라이언트 유효성 검사** 에서 **Web.config** 기본적으로 모든 새 ASP.NET MVC 4 프로젝트에는 false로 설정 된 파일을 가져오는 합니다. 또한 필요한 스크립트 jQuery 비 가시적인 클라이언트 유효성 검사 작업 확인에 대 한 참조를 추가 합니다.

1. 열기 **Web.Config** 파일을 프로젝트 루트에 있는지 확인 하 고는 **ClientValidationEnabled** 및 **UnobtrusiveJavaScriptEnabled** 키 값 로설정되며**true**합니다.

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > 또한 동일한 결과 얻기 위해 Global.asax.cs에서 코드에 의해 클라이언트 유효성 검사를 설정할 수 있습니다.
    > 
    > **HtmlHelper.ClientValidationEnabled = true;**
    > 
    > 또한 ClientValidationEnabled 특성을 사용자 지정 동작을 갖는 모든 컨트롤러에 할당할 수 있습니다.
2. 열기 **Create.cshtml** 에서 **Views\StoreManager**합니다.
3. 다음 스크립트 파일을 확인 **jquery.validate** 및 **jquery.validate.unobtrusive**, 보기 제외에서 참조 되는 &quot; **~/bundles/jqueryval** &quot; 번들입니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > 새 MVC 4 프로젝트에 이러한 모든 jQuery 라이브러리가 포함 됩니다. 더 많은 라이브러리를 찾을 수 있습니다는 **스크립트/** 있습니다 프로젝트의 폴더입니다.
    > 
    > 이 유효성 검사를 확인 하려면 라이브러리가 작동, jQuery 프레임 워크 라이브러리에 대 한 참조를 추가 해야 합니다. 이 참조에 이미 추가 하므로  **\_Layout.cshtml** 파일인 않아도이 특정 뷰에 추가할 합니다.

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a>작업 3-응용 프로그램 사용 하 여 비 가시적인 jQuery 유효성 검사를 실행 합니다.

에서는이 작업을 테스트 하는 **StoreManager** 템플릿을 사용자가 새 앨범을 만들 때 jQuery 라이브러리를 사용 하 여 클라이언트 쪽 유효성 검사를 수행 하는 뷰를 만듭니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.
2. 프로젝트 홈 페이지에서 시작합니다. 찾아보기 **/StoreManager/만들기** 클릭 **만들기** 폼 유효성 검사 메시지 얻어지는 지 확인을 채우지 않고:

    ![사용 하도록 설정 하는 jQuery 사용 하 여 클라이언트 유효성](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "jQuery 사용 하도록 설정 된 클라이언트 유효성 검사")

    *JQuery 사용 하도록 설정 된 클라이언트 유효성 검사*
3. 브라우저에서 뷰 만들기에 대 한 소스 코드를 엽니다.

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > 각 클라이언트 유효성 검사 규칙에 대해 비 가시적인 jQuery 추가 데이터를 사용 하 여 특성-val-*rulename*=&quot;*메시지*&quot;합니다. 아래 해당 Unobtrusive는 태그의 목록 jQuery 클라이언트 유효성 검사를 수행 하려면 html 입력된 필드에 삽입 합니다.
   > 
   > - 데이터 val
   > - Data-val-number
   > - 데이터 val 범위
   > - 데이터 val-범위 min/데이터 val-범위 최대값
   > - 데이터 val 필요
   > - 데이터 val 길이
   > - Val 길이 최대 데이터/val 길이 min 데이터
   > 
   > 모든 데이터 값이 모델 채워집니다 **데이터 주석을**합니다. 그런 다음 클라이언트 쪽에서 서버 쪽에서 작동 하는 모든 논리를 실행할 수 있습니다. 예를 들어 Price 특성에 다음 데이터 주석을 모델에 있습니다.
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > 비 가시적인 jQuery를 사용한 후 생성 된 코드는입니다.
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩을 완료 하 여 사용자가 다음를 사용 하 여 데이터베이스에 저장 된 데이터를 변경할 수 있게 하는 방법을 배웠습니다.

- 인덱스, 만들기, 편집, 삭제와 같은 컨트롤러 작업
- HTML 표에 속성을 표시 하기 위한 ASP.NET MVC 스 캐 폴딩 기능
- 사용자를 개선 하기 위해 사용자 지정 HTML 도우미 경험
- HTTP GET 또는 HTTP POST 호출에 반응 하는 작업 메서드
- 템플릿 만들기 및 편집와 같은 비슷한 보기에 대 한 공유 편집기 서식 파일
- 드롭다운 목록 같은 form 요소
- 모델 유효성 검사에 대 한 데이터 주석
- 비 가시적인 jQuery 라이브러리를 사용 하 여 클라이언트 쪽 유효성 검사

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 a: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여 **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)**. 다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.

1. 로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다. 또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Windows Azure SDK와</em>&quot;합니다.
2. 클릭 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.

    ![Visual Studio Express 설치](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건 동의](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **마침**합니다.

    ![설치 완료](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.

    ![웹 타일에 대 한 VS Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    *웹 타일에 대 한 VS Express*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>부록 b: 코드 조각을 사용 하 여

코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다. 랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.

![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")

*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*

***키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드를 삽입 하려는 위치에 커서를 놓습니다.
2. 공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.
3. IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.
4. 올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).
5. 커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.

![코드 조각 이름을 입력 하기 시작](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "조각 이름을 입력 하기 시작")

*코드 조각 이름을 입력 하기 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각 선택](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")

*Tab 키를 눌러 강조 표시 된 코드 조각 선택*

![확장 하 고 Tab 키를 눌러 다시 코드 조각](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")

*확장 하 고 Tab 키를 눌러 다시 코드 조각*

***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1입니다. 코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.

1. 선택 **조각 삽입** 이어서 **내 코드 조각**합니다.
2. 클릭 하 여 목록에서 관련 조각을 선택 합니다.

![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")

*코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*

![클릭 하 여 목록에서 관련 조각을 선택](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "클릭 하 여 목록에서 관련 조각을 선택")

*클릭 하 여 목록에서 관련 조각을 선택합니다*
