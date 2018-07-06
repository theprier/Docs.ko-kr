---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework 스 캐 폴딩 및 마이그레이션 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 컨트롤러 메서드를 사용 하 여 익숙한 또는 완료 하는 경우는 &quot;도우미, 폼 및 유효성 검사&quot; 실습 알아야 하는 중...
ms.author: aspnetcontent
ms.date: 02/18/2013
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 31f593f294c4865f621a8556cb43d0d9c42f2660
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37814124"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a>ASP.NET MVC 4 Entity Framework 스 캐 폴딩 및 마이그레이션

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트 다운로드](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 4 컨트롤러 메서드를 사용 하 여 익숙한 또는 완료 하는 경우는 &quot;도우미, 폼 및 유효성 검사&quot; 실습 알아야는 논리를 만들려면 많은 업데이트, 목록 및 반복이 모든 데이터 엔터티를 제거 합니다. 응용 프로그램 간에 있음은 물론, 경우에 모델에 조작할 수 있는 여러 클래스가 각 엔터티 작업 뿐만 아니라 각 보기에 대 한 POST 및 GET 작업 메서드를 작성 하는 상당한 시간을 소비 하는 일을 할 수 있습니다.

이 랩에서 ASP.NET MVC 4 스 캐 폴딩을 사용 하 여 자동으로 응용 프로그램의 CRUD (만들기, 읽기, 업데이트 및 삭제)의 기준선을 생성 하는 방법을 배웁니다. 간단한 모델 클래스에서 작성 하지 않고, 단일 코드 줄부터 만들려는 컨트롤러의 모든 필요한 보기 뿐만 아니라 모든 CRUD 작업을 포함할 합니다. 빌드하고 간단한 솔루션을 실행 한 후 MVC 논리 및 데이터 조작에 대 한 보기와 함께 생성 된 응용 프로그램 데이터베이스를 사용 해야 합니다.

또한 Entity Framework 마이그레이션 전체 응용 프로그램 전체에서 모델 업데이트를 수행 하는 데 얼마나 쉬운지 배웁니다. Entity Framework 마이그레이션 모델이 간단한 단계를 사용 하 여 변경 된 후 데이터베이스를 수정할 수 있습니다. 모든 이러한 염두에서 됩니다 수 구축 하 고 웹 응용 프로그램을 보다 효율적으로 관리할 ASP.NET MVC 4의 최신 기능을 활용 합니다.

> [!NOTE]
> 웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다. 이 랩에 특정 프로젝트에서 제공 됩니다 [ASP.NET MVC 4 Entity Framework 스 캐 폴딩 및 마이그레이션](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)합니다.

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 학습할 방법:

- 컨트롤러의 CRUD 작업에 대 한 ASP.NET 스 캐 폴딩을 사용 합니다.
- Entity Framework 마이그레이션을 사용 하 여 데이터베이스 모델을 변경 합니다.

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

이 문서의 부록 참조할 수 있습니다 사용 하는 방법을 알아보려면 원하는 고 Visual Studio 코드 조각을 사용 하 여 잘 모르는 경우 &quot; [부록 b:를 사용 하 여 코드 조각](#AppendixB)&quot;합니다.

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>연습

다음 연습 실습 랩이를 구성 합니다.

1. [Entity Framework 마이그레이션을 사용 하 여 ASP.NET MVC 4 스 캐 폴딩을 사용](#Exercise1)

> [!NOTE]
> 이 연습에서는 동반 되는 **최종** 연습을 완료 한 후 가져와야 결과 솔루션을 포함 하는 폴더입니다. 연습을 통해 작업 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.


이 랩을 완료 하기 위한 예상 시간: **30 분**

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a>연습 1: Entity Framework 마이그레이션 ASP.NET MVC 4 스 캐 폴딩 사용

데이터베이스 계층 상호 작용 하는 응용 프로그램을 수 있는 필요한 논리를 작성 하는 표준화 된 방식으로에서 CRUD 작업을 생성 하는 빠른 방법은 제공 하는 ASP.NET MVC 스 캐 폴딩 합니다.

이 연습에서는 CRUD 메서드를 만드는 코드를 사용 하 여 ASP.NET MVC 4 스 캐 폴딩 처음 사용 하는 방법을 배웁니다. 그런 다음 데이터베이스에 변경 내용을 적용 하는 Entity Framework 마이그레이션을 사용 하 여 모델을 업데이트 하는 방법을 배웁니다.

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a>태스크 1-만들기 새 ASP.NET MVC 4 프로젝트에 스 캐 폴딩을 사용

1. 아직 열지 않은 경우 시작 **Visual Studio 2012**합니다.
2. 선택 **파일 | 새 프로젝트**합니다. 새 프로젝트에서 대화 상자에서 아래는 **Visual C# | 웹** 섹션에서 **ASP.NET MVC 4 웹 응용 프로그램**합니다. 프로젝트 이름을 **MVC4andEFMigrations** 위치를 설정 하 고 **Source\Ex1 UsingMVC4ScaffoldingEFMigrations** 이 랩의 폴더입니다. 설정 합니다 **솔루션 이름** 를 **시작** 확인 **솔루션용 디렉터리 만들기** 확인란이 선택 되어 있습니다. **확인**을 클릭합니다.

    ![새 ASP.NET MVC 4 프로젝트 대화 상자](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "새 ASP.NET MVC 4 프로젝트 대화 상자")

    *새 ASP.NET MVC 4 프로젝트 대화 상자*
3. 에 **새 ASP.NET MVC 4 프로젝트** 대화 상자 선택 합니다 **인터넷 응용 프로그램** 템플릿이 되어 있는지 확인 **Razor** 는 선택한 **뷰 엔진**. **확인**을 클릭해 프로젝트를 만듭니다.

    ![새 ASP.NET MVC 4 인터넷 응용 프로그램](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "새 ASP.NET MVC 4 인터넷 응용 프로그램")

    *새 ASP.NET MVC 4 인터넷 응용 프로그램*
4. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 **모델** 선택한 **추가 | 클래스** 간단한 클래스 사람 (POCO)을 만들려고 합니다. 이름을 **Person** 누릅니다 **확인**합니다.
5. Person 클래스를 열고 다음 속성을 삽입 합니다.

    (코드 조각- *ASP.NET MVC 4 및 Entity Framework 마이그레이션-e x 1 개인 속성*)

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. 클릭 **빌드 | 솔루션 빌드** 변경 내용을 저장 하 여 프로젝트를 빌드합니다.

    ![응용 프로그램 빌드](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "응용 프로그램 빌드")

    *응용 프로그램 빌드*
7. 솔루션 탐색기에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가 | 컨트롤러**합니다.
8. 컨트롤러 이름을 *PersonController* 하 고 완료 합니다 **스 캐 폴딩 옵션** 다음 값으로.

   1. 에 **템플릿을** 드롭 다운 목록에서를 **읽기/쓰기 동작 및 Entity Framework를 사용 하 여 뷰를 사용 하 여 MVC 컨트롤러** 옵션입니다.
   2. 에 **모델 클래스** 드롭 다운 목록에서를 **Person** 클래스입니다.
   3. 에 **데이터 컨텍스트 클래스** 목록에서  **&lt;새 데이터 컨텍스트... &gt;**. 모든 이름을 선택 하 고 클릭 **확인**합니다.
   4. 에 **뷰** 드롭 다운 나열 되어 있는지 확인 합니다 **Razor** 을 선택 합니다.

      ![스 캐 폴딩 사용 하 여 Person 컨트롤러 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "스 캐 폴딩 사용 하 여 Person 컨트롤러 추가")

      *스 캐 폴딩 사용 하 여 Person 컨트롤러 추가*
9. 클릭 **추가** 스 캐 폴딩을 사용 하 여 사용자에 대 한 새 컨트롤러를 만들려고 합니다. 이제 컨트롤러 작업 뿐만 아니라 뷰를 생성 합니다.

    ![스 캐 폴딩을 사용 하 여 Person 컨트롤러를 만들면](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "Person 컨트롤러 스 캐 폴딩을 사용 하 여 만든 후")

    *스 캐 폴딩을 사용 하 여 Person 컨트롤러를 만든 후*
10. 오픈 **PersonController** 클래스입니다. 전체 CRUD 작업 메서드에 자동으로 생성 되었는지 확인 합니다.

   ![Person 컨트롤러 내](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "사람 내부 컨트롤러")

   *Person 컨트롤러 내에서*

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a>작업 2-응용 프로그램 실행

이 시점에서 데이터베이스 아직 생성 되지 않습니다. 이 태스크에서는 처음으로 응용 프로그램을 실행 하 고 CRUD 작업을 테스트 합니다. Code First를 사용 하 여 즉석에서 데이터베이스 생성 됩니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.
2. 브라우저에서 추가 **/Person** 사용자 페이지를 열려면 url입니다.

    ![응용 프로그램을 먼저 실행](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "응용 프로그램을 먼저 실행")

    *응용 프로그램: 먼저 실행 합니다.*
3. 이제 Person 페이지 탐색 및 CRUD 작업을 테스트 합니다.

    1. 클릭 **새로 만들기** 새 사용자를 추가 합니다. 첫 번째 이름과 마지막 이름을 입력 하 고 클릭 **만들기**합니다.

        ![새 사용자 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "새 사용자 추가")

        *새 사람 추가*
    2. 사용자의 목록에서 삭제, 편집 하거나 항목을 추가할 수 있습니다.

        ![개인 목록](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "사람 목록")

        *사용자 목록*
    3. 클릭 **세부 정보** 사람의 세부 정보를 엽니다.

        ![사용자의 세부 정보](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "사람의 세부 정보")

        *사용자의 세부 정보*
4. 브라우저를 닫고 Visual Studio로 돌아갑니다. 만든 사용자 엔터티에 대 한 전체 CRUD-보기-모델에서에서 응용 프로그램 전체에서 코드를 전혀 작성 하지 않고도 확인할 수 있습니다.

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a>작업 3-Entity Framework 마이그레이션을 사용 하 여 데이터베이스 업데이트

이 작업에서는 Entity Framework 마이그레이션을 사용 하 여 데이터베이스를 업데이트 합니다. 알게 될 것이 얼마나 쉬운지 모델을 변경 하 여 Entity Framework 마이그레이션 기능을 사용 하 여 데이터베이스에서 변경 내용을 반영 합니다.

1. 패키지 관리자 콘솔을 엽니다. 선택 **도구 | 라이브러리 패키지 관리자 | 패키지 관리자 콘솔**합니다.
2. 패키지 관리자 콘솔에서 다음 명령을 입력 합니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    ![마이그레이션을 사용 하도록 설정](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "마이그레이션을 사용 하도록 설정")

    *마이그레이션을 사용 하도록 설정*

    마이그레이션 사용 설정 명령을 만듭니다는 **마이그레이션을** 데이터베이스를 초기화 하는 스크립트를 포함 하는 폴더입니다.

    ![마이그레이션 폴더](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "마이그레이션 폴더")

    *예제에 표시 합니다 *데이터베이스 업데이트 배포* 자습서입니다.*
3. 엽니다는 **Configuration.cs** 마이그레이션 폴더에는 파일입니다. 클래스 생성자를 찾아서 변경 합니다 **AutomaticMigrationsEnabled** 값을 *true*합니다.

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. Person 클래스를 열고 사용자의 중간 이름에 대 한 특성을 추가 합니다. 이 새로운 특성을 사용 하 여 모델을 변경 됩니다.

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. 선택 **빌드 | 솔루션 빌드** 메뉴에서 응용 프로그램을 빌드합니다.

    ![응용 프로그램 빌드](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "응용 프로그램 빌드")

    *응용 프로그램 빌드*
6. 패키지 관리자 콘솔에서 다음 명령을 입력 합니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    이 명령은 데이터 개체의 변경 내용을 찾고 그런 다음 데이터베이스를 적절 하 게 수정 하는 데 필요한 명령을 추가 합니다.

    ![중간 이름 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "중간 이름 추가")

    *중간 이름 추가*
7. (선택 사항) 차등 업데이트를 사용 하 여 SQL 스크립트를 생성 하려면 다음 명령을 실행할 수 있습니다. 그러면 데이터베이스를 수동으로 업데이트할 수 있습니다 (이 경우에 필요 없는), 또는 다른 데이터베이스의 변경 내용을 적용 합니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    ![SQL 스크립트를 생성](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "SQL 스크립트 생성")

    *SQL 스크립트 생성*

    ![SQL 스크립트 업데이트](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL 스크립트 업데이트")

    *SQL 스크립트 업데이트*
8. 패키지 관리자 콘솔에서 데이터베이스를 업데이트 하려면 다음 명령을 입력 합니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    ![데이터베이스를 업데이트할](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "데이터베이스 업데이트")

    *데이터베이스를 업데이트 하는 중*

    추가 됩니다는 **MiddleName** 열에는 **사용자** 테이블의 현재 정의와 일치 하는 **Person** 클래스.
9. 데이터베이스 업데이트 되 면 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가 | 컨트롤러** 컨트롤러를 추가 하려면 사용자 다시 (동일한 값을 사용 하 여 전체). 이렇게 하면 기존 메서드와 새 특성을 추가 하는 뷰 업데이트 됩니다.

    ![컨트롤러 업데이트를 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "컨트롤러 업데이트 추가")

    *컨트롤러를 업데이트 하는 중*
10. **추가**를 클릭합니다. 값을 선택한 다음, **덮어쓰기 PersonController.cs** 및 **덮어쓰기 관련 뷰** 클릭 **확인**합니다.

   ![컨트롤러 덮어쓰기 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   *컨트롤러를 업데이트 하는 중*

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a>Task4-응용 프로그램을 실행 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.
2. 오픈 **/Person**합니다. 데이터 유지 된, 중간 이름 열이 추가 하는 동안 알 수 있습니다.

    ![중간 이름 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "중간 이름 추가")

    *중간 이름 추가*
3. 클릭 하면 **편집**, 중간 이름 현재 사용자를 추가할 수 있습니다.

    ![중간 이름 edition](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "중간 edition")

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩에서 ASP.NET MVC 4 스 캐 폴딩이 모든 모델 클래스를 사용 하 여 포함 된 CRUD 작업을 만드는 간단한 단계에 알아보았습니다. 그런 다음 뷰를 데이터베이스에서 응용 프로그램에서 Entity Framework 마이그레이션을 사용 하 여 종단 간 업데이트를 수행 하는 방법을 배웠습니다.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 a: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**. 다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.

1. 로 이동 [ [ https://go.microsoft.com/? linkid 9810169 =](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)합니다. 또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Windows Azure SDK를 사용 하 여 Web</em>&quot;합니다.
2. 클릭할 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.

    ![Visual Studio Express를 설치](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Visual Studio Express를 설치 합니다.")

    *Visual Studio Express를 설치 합니다.*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건에 동의](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    *사용 조건에 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **완료**합니다.

    ![설치 완료](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. 로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.

    ![VS Express for Web 타일](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    *VS Express for Web 타일*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>부록 b: 코드 조각 사용

코드 조각을 사용 하 여 결정적인 순간에 필요한 모든 코드를 해야 합니다. 랩 문서가 알려줍니다 정확 하 게 사용할 수 있는 시기를 다음 그림과 같습니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드를 삽입할](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "프로젝트에 코드를 삽입 하는 Visual Studio를 사용 하 여 코드 조각을")

*프로젝트에 코드를 삽입 하려면 Visual Studio 코드 조각 사용*

***키보드 (C#만 해당)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드를 삽입 하려는 위치에 커서를 놓습니다.
2. 시작 (공백 없이 하이픈) 조각 이름을 입력 합니다.
3. IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.
4. 올바른 코드 조각을 선택 합니다 (또는 전체 코드 조각 이름을 선택 될 때까지 입력 유지).
5. 커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.

![코드 조각 이름을 입력](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "조각 이름을 입력 하기 시작")

*코드 조각 이름을 입력 하기 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각을](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")

*Tab 키를 눌러 강조 표시 된 코드 조각 선택*

![Tab 키를 다시 코드 조각 확장 됩니다](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "다시 Tab 키를 누릅니다 하 고 코드 조각에서는 확장")

*Tab 키를 다시 및 코드 조각에서는 확장*

***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가할*** 1입니다. 코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.

1. 선택 **코드 조각 삽입** 뒤 **내 코드 조각**합니다.
2. 클릭 하 여 목록에서 관련 코드 조각을 선택 합니다.

![코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭")

*코드 조각을 삽입할 선택한 코드 조각 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭*

![클릭 하 여 목록에서 관련 코드 조각 선택](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "클릭 하 여 목록에서 관련 코드 조각 선택")

*클릭 하 여 목록에서 관련 코드 조각 선택*
