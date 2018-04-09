---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework 스 캐 폴딩 및 마이그레이션 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 컨트롤러 메서드에 익숙한 경우 또는 완료에서 &quot;도우미, 폼 및 유효성 검사&quot; 실습 랩 알고 있어야...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 548afe1926eed49841251832d54dc213da0cb753
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a>ASP.NET MVC 4 Entity Framework 스 캐 폴딩 및 마이그레이션

으로 [웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트를 다운로드 합니다.](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 4 컨트롤러 메서드에 익숙한 경우 또는 완료에서 &quot;도우미, 폼 및 유효성 검사&quot; 실습 랩 수 있는지, 만들 논리를 다양 한 업데이트, 목록 및 반복 되는 데이터 엔터티를 제거 합니다. 간에 응용 프로그램입니다. 있음은 물론, 하는 모델을 조작 하는 여러 클래스에 있으면 각 엔터티 작업 뿐만 아니라 각 보기에 대 한 POST 및 GET 작업 메서드를 작성 하는 시간이 많이 소요 될 수 있습니다.

이 랩에서 자동으로 응용 프로그램의 CRUD (만들기, 읽기, 업데이트 및 삭제)의 기준선을 생성 하는 ASP.NET MVC 4 기반 구조를 사용 하는 방법에 설명 합니다. 시작 간단한 모델 클래스에서 코드의 한 줄도 작성 하지 않고, 만듭니다으로 모든 CRUD 작업의 모든 필요한 뷰를 포함 하는 컨트롤러. 빌드하고 간단한 솔루션을 실행 한 후 응용 프로그램 데이터베이스의 MVC 논리 및 데이터 조작에 대 한 보기와 함께 생성 해야 합니다.

또한 전체 응용 프로그램 전반에 걸쳐 모델 업데이트를 수행 하려면 Entity Framework 마이그레이션을 사용 하는 것이 얼마나 쉬운지에 대해 설명 합니다. Entity Framework 마이그레이션 간단한 단계만 거치면 모델 변경 된 후 데이터베이스를 수정할 수 있습니다. 이러한 모든 염두에서,와 됩니다 구축 하 고 웹 응용 프로그램을 보다 효율적으로 관리할 수 ASP.NET MVC 4의 최신 기능을 활용 하기 위해.

> [!NOTE]
> 모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다. 이 랩에 특정 프로젝트에서 사용할 수는 [ASP.NET MVC 4 Entity Framework 스 캐 폴딩 및 마이그레이션을](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)합니다.

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 배우게 됩니다 하는 방법:

- 컨트롤러의 CRUD 작업에 대해 ASP.NET 스 캐 폴딩을 사용 합니다.
- Entity Framework 마이그레이션을 사용 하 여 데이터베이스 모델을 변경 합니다.

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

다음 연습 실습 랩이를 구성 합니다.

1. [ASP.NET MVC 4 스 캐 폴딩을 사용 하 여 Entity Framework 마이그레이션과 함께](#Exercise1)

> [!NOTE]
> 이 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다. 연습을 통해 작업 하 고 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.


예상 소요 시간: **30 분**

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a>연습 1: 스 캐 폴딩 ASP.NET MVC 4 사용 하 여 Entity Framework 마이그레이션과 함께

ASP.NET MVC 스 캐 폴딩 데이터베이스 계층 상호 작용 하는 응용 프로그램 수 있도록 하는 데 필요한 논리를 만드는 표준화 된 방식으로 CRUD 작업을 생성 하는 빠른 방법을 제공 합니다.

이 연습에서는 CRUD 메서드를 만들려면 먼저 ASP.NET MVC 4 스 캐 폴딩 코드와 함께 사용 하는 방법에 설명 합니다. 그런 다음 데이터베이스에 변경 내용을 적용 하는 Entity Framework 마이그레이션을 사용 하 여 모델을 업데이트 하는 방법에 설명 합니다.

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a>스 캐 폴딩을 사용 하 여 작업 1-Creating 새 ASP.NET MVC 4 프로젝트

1. 아직 열지 않은 경우 시작 **Visual Studio 2012**합니다.
2. 선택 **파일 | 새 프로젝트**합니다. 새로 만들기 대화 상자에서를 아래에서 프로젝트는 **Visual C# | 웹** 섹션에서 **ASP.NET MVC 4 웹 응용 프로그램**합니다. 에 프로젝트 이름을 **MVC4andEFMigrations** 위치를 설정 하 고 **Source\Ex1 UsingMVC4ScaffoldingEFMigrations** 이 랩의 폴더입니다. 설정의 **솔루션 이름** 를 **시작** 확인 **솔루션용 디렉터리 만들기** 을 선택 합니다. **확인**을 클릭합니다.

    ![새 ASP.NET MVC 4 프로젝트 대화 상자](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "새 ASP.NET MVC 4 프로젝트 대화 상자")

    *새 ASP.NET MVC 4 프로젝트 대화 상자*
3. 에 **새 ASP.NET MVC 4 프로젝트** 대화 상자 선택은 **인터넷 응용 프로그램** 서식 파일을 있는지 확인 하 고 **Razor** 은 선택한 **뷰 엔진**. **확인**을 클릭해 프로젝트를 만듭니다.

    ![새 ASP.NET MVC 4 인터넷 응용 프로그램](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "새 ASP.NET MVC 4 인터넷 응용 프로그램")

    *새 ASP.NET MVC 4 인터넷 응용 프로그램*
4. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 **모델** 선택 **추가 | 클래스** 간단한 클래스 사람 POCO ()를 만들려고 합니다. 이름을 **사람** 클릭 **확인**합니다.
5. 사용자 클래스를 열고 다음 속성을 삽입 합니다.

    (코드 조각- *ASP.NET MVC 4 및 Entity Framework 마이그레이션-e x 1 사람 속성*)


~~~
[!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
~~~
6. 클릭 **빌드 | 솔루션 빌드** 는 변경 내용을 저장 하는 프로젝트를 빌드합니다.

    ![응용 프로그램 빌드](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "응용 프로그램 빌드")

    *응용 프로그램 빌드*
7. 솔루션 탐색기에서 controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가 | 컨트롤러**합니다.
8. 컨트롤러 이름을 *PersonController* 완료는 **스 캐 폴딩 옵션** 다음 값을 사용 합니다.

   1. 에 **템플릿** 드롭 다운 목록에서 **읽기/쓰기 동작 및 뷰가, Entity Framework를 사용 하 여 포함 된 MVC 컨트롤러** 옵션.
   2. 에 **모델 클래스** 드롭 다운 목록에서 **사람** 클래스입니다.
   3. 에 **데이터 컨텍스트 클래스** 목록에서  **&lt;새 데이터 컨텍스트에... &gt;**. 모든 이름을 선택 하 고 클릭 **확인**합니다.
   4. 에 **뷰** 드롭 다운 목록에서 다음 사항을 확인 **Razor** 을 선택 합니다.

      ![스 캐 폴딩에 사람 컨트롤러 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "스 캐 폴딩에 사람 컨트롤러 추가")

      *스 캐 폴딩에 사람 컨트롤러 추가*
9. 클릭 **추가** 사람에 대 한 새 컨트롤러 스 캐 폴딩을 만들려고 합니다. 이제 컨트롤러 작업 뿐만 아니라 뷰를 생성 한 합니다.

    ![스 캐 폴딩을 사용 사람 컨트롤러를 만든 다음](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "스 캐 폴딩을 사용 사람 컨트롤러를 만든 다음")

    *스 캐 폴딩을 사용 사람 컨트롤러를 만든 다음*
10. 열기 **PersonController** 클래스입니다. 전체 CRUD 작업 메서드를 자동으로 생성 된 것을 확인 합니다.

   ![Person 컨트롤러 내](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "사람 내부 컨트롤러")

   *사람 컨트롤러 내*

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a>작업 2-실행 응용 프로그램

이 시점에서 데이터베이스 아직 생성 되지 않습니다. 이 태스크에서는 처음으로 응용 프로그램을 실행 하 고 CRUD 작업을 테스트 됩니다. 데이터베이스에서 Code First를 사용 하 여 즉시 생성 됩니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.
2. 브라우저에서 추가 **/Person** 사용자 페이지를 열려면 URL에 있습니다.

    ![응용 프로그램 먼저 실행](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "응용 프로그램 먼저 실행")

    *응용 프로그램: 먼저 실행 합니다.*
3. 이제 사용자 페이지 탐색 및 CRUD 작업을 테스트 합니다.

    1. 클릭 **새로 만들기** 새 사람을 추가 하려면. 첫 번째 이름 및 성을 입력 하 고 클릭 **만들기**합니다.

        ![새로운 사람 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "새 사용자 추가")

        *새 사용자 추가*
    2. 사용자의 목록에서 삭제, 편집 하거나 항목을 추가할 수 있습니다.

        ![개인 목록](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "개인 목록")

        *개인 목록*
    3. 클릭 **세부 정보** 를 사용자의 세부 정보를 엽니다.

        ![사용자의 세부 정보](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "사용자의 세부 정보")

        *사용자의 세부 정보*
4. 브라우저를 닫고 Visual Studio로 돌아갑니다. 만든 사람 엔터티에 대 한 전체 CRUD 보기에 모델--에서 응용 프로그램 전체에서 코드를 전혀 작성 하지 않고도 점에 주의 하십시오.

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a>작업 3-업데이트 Entity Framework 마이그레이션을 사용 하 여 데이터베이스

이 작업에서는 Entity Framework 마이그레이션을 사용 하 여 데이터베이스를 업데이트 합니다. 모델을 변경 하 고 Entity Framework 마이그레이션 기능을 사용 하 여 데이터베이스에서 변경 내용을 반영 하는 것이 얼마나 쉬운지에서 검색 합니다.

1. 패키지 관리자 콘솔을 엽니다. 선택 **도구 | 라이브러리 패키지 관리자 | 패키지 관리자 콘솔**합니다.
2. 패키지 관리자 콘솔에서 다음 명령을 입력 합니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    ![마이그레이션을 사용 하도록 설정](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "마이그레이션을 사용 하도록 설정")

    *마이그레이션을 사용 하도록 설정*

    마이그레이션을 사용 하도록 설정 명령은 만듭니다는 **마이그레이션** 데이터베이스 초기화에 스크립트가 들어 있는 폴더입니다.

    ![Migrations 폴더](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Migrations 폴더")

    *Migrations 폴더*
3. 열기는 **Configuration.cs** Migrations 폴더에서 파일입니다. 클래스 생성자를 찾아 변경는 **AutomaticMigrationsEnabled** 값을 *true*합니다.


~~~
[!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
~~~
4. 사용자 클래스를 열고 있는 사람의 중간 이름을 대 한 특성을 추가 합니다. 이 새 특성으로 모델을 변경 됩니다.


~~~
[!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
~~~
5. 선택 **빌드 | 솔루션 빌드** 메뉴에서 응용 프로그램을 빌드합니다.

    ![응용 프로그램 빌드](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "응용 프로그램 빌드")

    *응용 프로그램 빌드*
6. 패키지 관리자 콘솔에서 다음 명령을 입력 합니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    이 명령은 데이터 개체의 변경 내용을 찾아서 그런 다음 데이터베이스를 적절 하 게 수정 하는 데 필요한 명령을 추가 합니다.

    ![중간 이름 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "중간 이름 추가")

    *중간 이름 추가*
7. (선택 사항) 차등 업데이트와 함께 SQL 스크립트를 생성 하려면 다음 명령을 실행할 수 있습니다. 그러면 데이터베이스를 수동으로 업데이트할 수 있습니다 (이 경우에 필요 없는), 또는 다른 데이터베이스의 변경 내용을 적용 합니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    ![SQL 스크립트를 생성](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "SQL 스크립트 생성")

    *SQL 스크립트 생성*

    ![SQL 스크립트 업데이트](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL 스크립트 업데이트")

    *SQL 스크립트 업데이트*
8. 패키지 관리자 콘솔에서 데이터베이스를 업데이트 하려면 다음 명령을 입력 합니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    ![데이터베이스 업데이트](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "데이터베이스 업데이트")

    *데이터베이스 업데이트*

    이렇게 하면 추가 됩니다는 **MiddleName** 열에는 **사람** 테이블의 현재 정의가 일치 하도록는 **사람** 클래스입니다.
9. 데이터베이스를 업데이트 후 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가 | 컨트롤러** 컨트롤러 추가 하는 사람 다시 (동일한 값을 가진 전체). 이렇게 하면 기존 방법 및 새 특성을 추가 하는 뷰 업데이트 됩니다.

    ![컨트롤러 업데이트 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "컨트롤러 업데이트 추가")

    *컨트롤러 업데이트*
10. **추가**를 클릭합니다. 값을 선택한 다음, **덮어쓰기 PersonController.cs** 및 **덮어쓰기 관련 뷰** 클릭 **확인**합니다.

   ![컨트롤러 덮어쓰기 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   *컨트롤러 업데이트*

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a>Task4-응용 프로그램을 실행 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.
2. 열기 **/Person**합니다. 중간 이름 열이 추가 하는 동안 데이터를 보존 있는지 확인 합니다.

    ![중간 이름 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "중간 이름 추가")

    *중간 이름 추가*
3. 클릭 하면 **편집**, 현재 사용자에 게 중간 이름을 추가할 수 있습니다.

    ![중간 이름 버전](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "중간 이름 버전")

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩에서 간단한 단계를 ASP.NET MVC 4 스 캐 폴딩이 모든 모델 클래스를 사용 하 여와 CRUD 작업을 만드는 방법을 배웠습니다. 그런 다음 엔터티 프레임 워크 마이그레이션을 사용 하 여 보기에는 데이터베이스에서 응용 프로그램에 대 한 종단 간 업데이트를 수행 하는 방법을 배웠습니다.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 a: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여 **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)**. 다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.

1. 로 이동 [ [ https://go.microsoft.com/? linkid = 9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)합니다. 또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Windows Azure SDK와</em>&quot;합니다.
2. 클릭 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.

    ![Visual Studio Express 설치](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건 동의](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **마침**합니다.

    ![설치 완료](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.

    ![웹 타일에 대 한 VS Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    *웹 타일에 대 한 VS Express*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>부록 b: 코드 조각을 사용 하 여

코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다. 랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.

![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")

*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*

***키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드를 삽입 하려는 위치에 커서를 놓습니다.
2. 공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.
3. IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.
4. 올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).
5. 커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.

![코드 조각 이름을 입력 하기 시작](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "조각 이름을 입력 하기 시작")

*코드 조각 이름을 입력 하기 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각 선택](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")

*Tab 키를 눌러 강조 표시 된 코드 조각 선택*

![확장 하 고 Tab 키를 눌러 다시 코드 조각](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")

*확장 하 고 Tab 키를 눌러 다시 코드 조각*

***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1입니다. 코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.

1. 선택 **조각 삽입** 이어서 **내 코드 조각**합니다.
2. 클릭 하 여 목록에서 관련 조각을 선택 합니다.

![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")

*코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*

![클릭 하 여 목록에서 관련 조각을 선택](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "클릭 하 여 목록에서 관련 조각을 선택")

*클릭 하 여 목록에서 관련 조각을 선택합니다*
