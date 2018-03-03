---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: "ASP.NET MVC 4 모델 및 데이터 액세스 | Microsoft Docs"
author: rick-anderson
description: "참고:이 실습 랩 ASP.NET MVC에 대 한 기본 지식이 있다고 가정 합니다. 하기 전에 ASP.NET MVC를 사용 하지 않은 경우 좋습니다 ASP.NET MVC 4를 초과할 수 있습니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 353419077422516761df56f730352b19b5db5ff2
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="aspnet-mvc-4-models-and-data-access"></a>ASP.NET MVC 4 모델 및 데이터 액세스

으로 [웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트를 다운로드 합니다.](https://aka.ms/webcamps-training-kit)

이 실습 랩 대 한 기본 지식이 있다고 가정 하 고 **ASP.NET MVC**합니다. 사용 하지 않은 경우 **ASP.NET MVC** 를 권장 앞, **ASP.NET MVC 4 기초** 실습 랩입니다.

이 랩에서 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 내용을 적용 하 여 이전에 설명 된 새로운 기능 및 향상 된 기능을 통해 설명 합니다.

> [!NOTE]
> 모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다. 이 랩에 특정 프로젝트에서 사용할 수는 [ASP.NET MVC 4 모델 및 데이터 액세스](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess)합니다.

**ASP.NET MVC의 기본 사항** 실습 랩 있습니다 전달 했기 하드 코드 된 데이터는 컨트롤러에서 템플릿 보기에 있습니다. 그러나 실제 웹 응용 프로그램을 작성 하기 위해 실제 데이터베이스를 사용 수 있습니다.

이 실습 랩 음악 스토어 응용 프로그램에 필요한 데이터 저장 및 검색 하기 위해 데이터베이스 엔진을 사용 하는 방법을 설명 합니다. 이를 위해 기존 데이터베이스를 시작 쿼리하고에서 엔터티 데이터 모델을 생성 합니다. 이 랩의 경우 전체에서 해결할 지는 **Database First** 접근 방식으로 **Code First** 접근 방식입니다.

그러나 사용할 수도 있습니다는 **Model First** 접근 방식, 도구를 사용 하는 동일한 모델을 만들 및 다음에서 데이터베이스를 생성 합니다.

![데이터베이스의 첫 번째 vs입니다. 첫 번째 모델](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. 먼저 모델")

*데이터베이스의 첫 번째 vs입니다. 먼저 모델

모델을 생성 하 고 나면 StoreController 하드 코드 된 데이터를 사용 하는 대신 데이터베이스에서 가져온 데이터와 함께 저장소 보기를 제공 하기에 적절 한 조정 생성 됩니다. 어떠한 변경 템플릿 보기에는 StoreController 반품할 동일한 Viewmodel 보기 템플릿 때문에이 시간 데이터가 데이터베이스에서 나올지 있지만 않아도 됩니다.

**코드의 첫 번째 방법인**

Code First 접근 방식은 일반적으로 프레임 워크와 연결 되어 있는 클래스를 생성 하지 않고 코드에서 모델을 정의할 수 있습니다.

코드에서 먼저, 모델 개체도 정의 됩니다 POCOs, &quot;일반 이전 CLR 개체&quot;합니다. POCOs는 간단한 일반 클래스 없는 상속을 포함 하 고 인터페이스를 구현 하지 않는입니다. 데이터베이스에서, 자동으로 생성할 수 또는 기존 데이터베이스를 코드에서 클래스 매핑을 생성할 수 있습니다.

이 접근 방식을 사용의 이점에는 모델 유지 됩니다 (이 경우 Entity Framework)의 지 속성 프레임 워크와 독립적인 POCOs 클래스 매핑 프레임 워크와 연결 되어 있지는입니다.

> [!NOTE]
> 이 랩에서 ASP.NET MVC 4에 근거 하며 버전 Music Store 샘플 응용 프로그램의 사용자 지정 하 고이 실습 랩에 표시 된 기능에 맞게 최소화 합니다.
> 
> 전체 탐색 하려는 경우 **Music Store** 자습서 응용 프로그램에서 찾을 수 [MVC 음악 저장소](https://github.com/evilDave/MVC-Music-Store)합니다.


<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>필수 구성 요소

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>설정

**설치 하는 코드 조각**

편의 위해는이 랩에 따라 관리 코드의 대부분 Visual Studio 코드 조각 수 있습니다. 실행 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.

이 문서에서 부록을 참조할 수 사용 하는 방법에 알아봅니다 사용 하 고 Visual Studio 코드 조각에 익숙한 경우 &quot; [부록 c:를 사용 하 여 코드 조각을](#AppendixC)&quot;합니다.

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습으로 구성 됩니다.

1. [연습 1: 데이터베이스 추가](#Exercise1)
2. [연습 2: Code First를 사용 하 여 데이터베이스 만들기](#Exercise2)
3. [매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 연습 3:](#Exercise3)

> [!NOTE]
> 각 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다. 연습을 통해 작업 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.


예상 소요 시간: **35 분**합니다.

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a>연습 1: 데이터베이스 추가

이 연습에서는 해당 데이터를 처리 하기 위해 솔루션에 MusicStore 응용 프로그램의 테이블이 포함 된 데이터베이스를 추가 하는 방법에 설명 합니다. 데이터베이스 모델을 사용 하 여 생성 되 고 솔루션에 추가 되 면 하드 코드 된 값을 사용 하는 대신 데이터베이스에서 가져온 데이터와 함께 템플릿 보기를 제공 하기 위해 StoreController 클래스를 수정 합니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a>작업 1-데이터베이스 추가

이 작업에서는 솔루션 MusicStore 응용 프로그램의 주 테이블을 사용 하 여 이미 생성된 된 데이터베이스를 추가 합니다.

1. 열기는 **시작** 솔루션에 있는 **소스/e x 1-AddingADatabaseDBFirst/시작/** 폴더입니다.

    1. 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 전에 계속 합니다. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
    2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
    3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

    > [!NOTE]
    > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 추가 **MvcMusicStore** 데이터베이스 파일입니다. 이 실습 랩을 사용 하 여 호출 하는 이미 만들어진된 데이터베이스 **MvcMusicStore.mdf**합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 **앱\_데이터** 폴더를 가리키도록 **추가** 클릭 하 고 **기존 항목**합니다. 찾아 **\Source\Assets** 선택 하 고는 **MvcMusicStore.mdf** 파일입니다.

    ![기존 항목 추가](aspnet-mvc-4-models-and-data-access/_static/image2.png "기존 항목 추가")

    *기존 항목 추가*

    ![데이터베이스 파일 MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf 데이터베이스 파일")

    *MvcMusicStore.mdf 데이터베이스 파일*

    데이터베이스는 프로젝트에 추가 되었습니다. 솔루션 내에서 데이터베이스가 하는 경우에 쿼리 하 고 다른 데이터베이스 서버에서 호스트 되는 대로 업데이트 수 있습니다.

    ![솔루션 탐색기에서 데이터베이스 MvcMusicStore](aspnet-mvc-4-models-and-data-access/_static/image4.png "솔루션 탐색기에서 MvcMusicStore 데이터베이스")

    *솔루션 탐색기에서 MvcMusicStore 데이터베이스*
3. 데이터베이스에 연결을 확인 합니다. 이 작업을 수행 하려면 두 번 클릭 **MvcMusicStore.mdf** 는 연결을 설정할 수 있습니다.

    ![MvcMusicStore.mdf 연결할](aspnet-mvc-4-models-and-data-access/_static/image5.png "MvcMusicStore.mdf에 연결")

    *MvcMusicStore.mdf에 연결*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a>작업 2-데이터 모델 만들기

이 작업에서는 이전 태스크에서 추가 데이터베이스와 상호 작용 하는 데이터 모델을 만듭니다.

1. 데이터베이스를 나타내는 데이터 모델을 만듭니다. 솔루션 탐색기 오른쪽 클릭에서이 작업을 수행 하는 **모델** 폴더를 가리키도록 **추가** 클릭 하 고 **새 항목**합니다. 에 **새 항목 추가** 대화 상자에서는 **데이터** 템플릿을 차례로 **ADO.NET 엔터티 데이터 모델** 항목입니다. 데이터 모델 이름을 **StoreDB.edmx** 클릭 **추가**합니다.

    ![StoreDB ADO.NET 엔터티 데이터 모델 추가](aspnet-mvc-4-models-and-data-access/_static/image6.png "StoreDB ADO.NET 엔터티 데이터 모델 추가")

    *StoreDB ADO.NET 엔터티 데이터 모델 추가*
2. **엔터티 데이터 모델 마법사** 표시 됩니다. 이 마법사에서는 모델 계층을 만드는 과정을 안내 합니다. 선택 모델 만들어야 할 추가 기존 데이터베이스 recentyl에 따라 이후 **데이터베이스에서 생성** 클릭 **다음**합니다.

    ![모델 콘텐츠 선택](aspnet-mvc-4-models-and-data-access/_static/image7.png "모델 콘텐츠 선택")

    *모델 콘텐츠 선택*
3. 데이터베이스에서 모델을 생성 하는 이후 사용에 대 한 연결을 지정 해야 합니다. 클릭 **새 연결**합니다.
4. 선택 **Microsoft SQL Server 데이터베이스 파일** 클릭 **계속**합니다.

    ![데이터 원본 선택](aspnet-mvc-4-models-and-data-access/_static/image8.png "데이터 원본 선택")

    *데이터 원본 대화 상자를 선택 합니다.*
5. 클릭 **찾아보기** 데이터베이스를 선택 하 고 **MvcMusicStore.mdf** 에 있는 **앱\_데이터** 폴더 **확인**합니다.

    ![연결 속성](aspnet-mvc-4-models-and-data-access/_static/image9.png "연결 속성")

    *연결 속성*
6. 생성 된 클래스 엔터티 연결 문자열 이름이 같은, 따라서 해당 이름을 변경 해야 **MusicStoreEntities** 클릭 **다음**합니다.

    ![데이터 연결 선택](aspnet-mvc-4-models-and-data-access/_static/image10.png "데이터 연결 선택")

    *데이터 연결 선택*
7. 데이터베이스 개체를 사용 하 여 선택 합니다. 엔터티 모델만 데이터베이스의 테이블을 사용 하는 경우 선택 된 **테이블** 옵션을 선택한 다음 사항을 확인는 **모델에 외래 키 열을 포함할** 및 **복수화 또는 단 수 화 생성 개체 이름** 옵션 선택 됩니다. 변경 하려면 모델 Namespace **MvcMusicStore.Model** 클릭 **마침**합니다.

    ![데이터베이스 개체 선택](aspnet-mvc-4-models-and-data-access/_static/image11.png "데이터베이스 개체 선택")

    *데이터베이스 개체 선택*

    > [!NOTE]
    > 보안 경고 대화 상자가 표시 되 면 클릭 **확인** 하 여 템플릿을 실행 하 고 모델 엔터티에 대 한 클래스를 생성 합니다.
8. 데이터베이스에 각 테이블을 매핑하는 별도 클래스를 만들 수는 동안 데이터베이스는 엔터티 다이어그램이 표시 됩니다. 예를 들어는 **앨범** 테이블으로 표현 됩니다는 **앨범** 클래스, 클래스 속성 테이블의 각 열이 매핑됩니다. 이렇게 하면 쿼리 및 데이터베이스의 행을 나타내는 개체를 사용 합니다.

    ![엔터티 다이어그램](aspnet-mvc-4-models-and-data-access/_static/image12.png "엔터티 다이어그램")

    *엔터티 다이어그램*

> [!NOTE]
> T4 템플릿 (.tt) 엔터티 클래스를 생성 하는 코드를 실행 하 고 같은 이름의 기존 클래스를 덮어쓰게 됩니다. 이 예제에서는 클래스 &quot;앨범&quot;, &quot;장르&quot; 및 &quot;아티스트&quot; 생성 된 코드와 덮어쓴 합니다.


<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a>작업 3-응용 프로그램 빌드

이 작업을 검사 해야는 모델 생성이 제거 되지만 **앨범**, **장르** 및 **아티스트** 모델 클래스는 프로젝트 빌드 성공적으로 사용 하 여 새 데이터 모델 클래스입니다.

1. 선택 하 여 프로젝트를 빌드합니다는 **빌드** 메뉴 항목 차례로 **빌드 MvcMusicStore**합니다.

    ![프로젝트를 빌드하면](aspnet-mvc-4-models-and-data-access/_static/image13.png "프로젝트 빌드")

    *프로젝트 빌드*
2. 프로젝트가는 성공적으로 빌드됩니다. 이유 여전히 작동 합니까? 데이터베이스 테이블에 있는 필드를 제거 하는 클래스에 사용 된 속성을 포함 하기 때문에 작동 **앨범** 및 **장르**합니다.

    ![빌드 성공](aspnet-mvc-4-models-and-data-access/_static/image14.png "빌드 성공")

    *빌드 성공*
3. 엔터티를 다이어그램 형태로 표시 하는 디자이너, C# 클래스는 실제로 합니다. 확장의 **StoreDB.edmx** 솔루션 탐색기에서 노드 차례로 **StoreDB.tt**생성된 한 새 엔터티 표시 됩니다.

    ![생성 된 파일](aspnet-mvc-4-models-and-data-access/_static/image15.png "생성 된 파일")

    *생성 된 파일*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>작업 4-데이터베이스 쿼리

이 태스크에서는 하드 코드 된 데이터를 사용 하는 대신 쿼리 하는 데이터베이스 정보를 검색할 수 있도록 StoreController 클래스를 업데이트 합니다.

1. 열기 **Controllers\StoreController.cs** 의 인스턴스를 저장 하는 클래스에 다음 필드를 추가 하 고는 **MusicStoreEntities** 라는 클래스를 **storeDB**:

    (코드 조각- *모델 데이터 액세스 및-e x 1 storeDB*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. **MusicStoreEntities** 클래스는 데이터베이스의 각 테이블에 대 한 컬렉션 속성을 노출 합니다. 업데이트 **찾아보기** 모든 장르를 가져오려는 작업 메서드는 **앨범**합니다.

    (코드 조각- *모델 및 데이터 액세스-e x 1 저장소 찾아보기*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > .NET 호출의 기능을 사용 하는 **LINQ** 프로그래밍할 수 있습니다 (통합 언어 쿼리)-이 데이터베이스에 대해 코드를 실행 하 고 반환 하는 이러한 컬렉션에 대 한 강력한 형식의 쿼리 식을 작성 하 개체 합니다.
    > 
    > LINQ에 대 한 자세한 내용은 참조 하십시오는 [msdn 사이트](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)합니다.
3. 업데이트 **인덱스** 동작 메서드를 모든 장르를 검색 합니다.

    (코드 조각- *모델 및 데이터 액세스-e x 1 저장소 인덱스*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. 업데이트 **인덱스** 동작 메서드의 모든 장르를 검색 하 고 목록에 컬렉션을 변환 합니다.

    (코드 조각- *모델 및 데이터 액세스-e x 1 저장소 GenreMenu*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>5-응용 프로그램 실행 작업

이 작업에서는 저장소 인덱스 페이지에 하드 코드 된 것 대신 데이터베이스에 저장 된 장르 표시 이제 됩니다 확인 합니다. 하기 때문에 템플릿 보기를 변경할 필요가 없습니다는 **StoreController** 되는 동일한 엔터티 반환 이전 처럼 있지만이 이번 데이터 데이터베이스에서 가져옵니다.

1. 솔루션 및 키를 눌러 다시 빌드 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. 확인의 메뉴 **장르** 는 더 이상 하드 코드 된 목록 및 데이터는 데이터베이스에서 직접 검색 됩니다.

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    *데이터베이스에서 검색 장르*
3. 이제 모든 장르로 이동 하 고 데이터베이스에서 앨범 채워집니다 확인 합니다.

    ![데이터베이스에서 앨범 검색](aspnet-mvc-4-models-and-data-access/_static/image17.png "앨범을 데이터베이스에서 검색")

    *데이터베이스에서 검색 앨범*

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a>연습 2: 먼저 코드를 사용 하 여 데이터베이스 만들기

이 연습에서는 MusicStore 응용 프로그램의 테이블을 사용 하 여 데이터베이스를 만들려면 Code First 접근 방식을 사용 하는 방법과 해당 데이터를 액세스 하는 방법을 배웁니다.

모델 생성 되 면에 하드 코드 된 값을 사용 하는 대신 데이터베이스에서 가져온 데이터 템플릿 보기를 제공 하려면 StoreController 수정 합니다.

> [!NOTE]
> 연습 1 완료 이미 Database First 접근 방식으로 작업을 수행 하는 경우 이제 다른 프로세스와 동일한 결과를 얻는 방법을 배웁니다. 연습 1과 마찬가지로 포함 된 태스크는 읽는 쉽게 수행할 수 있도록 표시 되어 있습니다. 실습 1 완료 되지 않은 하지만 자세한 Code First 접근 방식으로이 연습에서 시작를 항목의 전체 범위를 가져올 수 있습니다.


<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a>작업 1-샘플 데이터를 구성

이 작업에서는 코드 중심을 사용 하 여 intially 만들어질 때 데이터베이스를 샘플 데이터로 있습니다 채워집니다.

1. 열기는 **시작** 솔루션에 있는 **소스/e x 2-CreatingADatabaseCodeFirst/시작/** 폴더입니다. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.

    1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
    2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
    3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

    > [!NOTE]
    > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 추가 **SampleData.cs** 파일을 여 **모델** 폴더입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 **모델** 폴더를 가리키도록 **추가** 클릭 하 고 **기존 항목**합니다. 찾아 **\Source\Assets** 선택 하 고는 **SampleData.cs** 파일입니다.

    ![예제 데이터 코드를 채우는](aspnet-mvc-4-models-and-data-access/_static/image18.png "예제 데이터 코드 채우기")

    *예제 데이터 코드 채우기*
3. 열기는 **Global.asax.cs** 파일을 다음 추가 *를 사용 하 여* 문.

    (코드 조각- *모델 및 데이터 액세스-e x 2 글로벌 Asax Using*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. 에 **응용 프로그램\_start ()** 메서드 데이터베이스 이니셜라이저를 설정 하려면 다음 줄을 추가 합니다.

    (코드 조각- *모델 및 데이터 액세스-e x 2 글로벌 Asax SetInitializer*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a>작업 2-데이터베이스 연결 구성

이 프로젝트에 데이터베이스를 이미 추가한 했으므로에서 작성할는 **Web.config** 파일 연결 문자열입니다.

1. 연결 문자열에 추가 **Web.config**합니다. 이러한 파일을 열고 **Web.config** 프로젝트 루트 및 연결 문자열에서이 줄 DefaultConnection 라는 replace는  **&lt;connectionStrings&gt;**  섹션:

    ![Web.config 파일 위치](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config 파일 위치")

    *web.config 파일 위치*


    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a>작업 3-모델 작업

이미 데이터베이스에 연결을 구성 했으므로 데이터베이스 테이블을 사용 하 여 모델을 연결 됩니다. 이 태스크에서는 Code First로 데이터베이스에 연결할 수 있는 클래스를 만듭니다. 수정 해야 하는 기존 POCO 모델 클래스 임을 기억 합니다.

> [!NOTE]
> 연습 1을 완료 한 경우이 단계는 마법사에 의해 수행 된를 언급 합니다. Code First를 통해 수동으로 데이터 엔터티에 연결 하는 클래스 만듭니다.


1. POCO 모델 클래스를 열고 **장르** 에서 **모델** 폴더를 프로젝트 및 ID를 포함 합니다. Int 속성 이름으로 사용 하 여 **GenreId**합니다.

    (코드 조각- *모델 및 데이터 액세스-e x 2 코드 첫 번째 장르*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > Code First 규칙을 사용 하려면 Genre 클래스에 자동으로 검색 하는 기본 키 속성이 있어야 합니다.
    > 
    > 자세한 내용은이 코드의 첫 번째 규칙에 대 한 [msdn 문서](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)합니다.
2. 이제는 POCO 모델 클래스를 열 **앨범** 에서 **모델** 폴더를 프로젝트 및 외래 키를 포함를 이름으로 속성을 만들 **GenreId** 및  **ArtistId**합니다. 가 이미이 클래스는 **GenreId** 기본 키에 대 한 합니다.

    (코드 조각- *모델 및 데이터 액세스-e x 2 코드 첫 번째 앨범*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. POCO 모델 클래스를 열고 **아티스트** 포함는 **ArtistId** 속성입니다.

    (코드 조각- *모델 및 데이터 액세스-e x 2 코드 첫 번째 아티스트*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. 마우스 오른쪽 단추로 클릭는 **모델** 프로젝트 폴더를 선택 **추가 | 클래스**합니다. 파일 이름을 **MusicStoreEntities.cs**합니다. 클릭 **추가 합니다.**

    ![클래스 추가](aspnet-mvc-4-models-and-data-access/_static/image20.png "클래스 추가")

    *새 항목 추가*

    ![추가 class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "는 class2 추가")

    *클래스 추가*
5. 방금 만든 클래스를 열고 **MusicStoreEntities.cs**, 네임 스페이스를 포함 하 고 **System.Data.Entity** 및 **System.Data.Entity.Infrastructure**합니다.


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. 확장 하는 클래스 선언 대신는 **DbContext** 클래스: 공용 선언 **DBSet** 재정의 **OnModelCreating** 메서드. 이 단계에서는 Entity Framework를 사용 하 여 모델을 연결 하는 도메인 클래스를 받아볼 수 있습니다. 파일을 수집 하려면 클래스 코드를 다음으로 바꿉니다.

    (코드 조각- *모델 및 데이터 액세스-e x 2 코드 첫 번째 MusicStoreEntities*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

    > [!NOTE]
    > Entity Framework와 함께 **DbContext** 및 **DBSet** POCO 클래스 장르를 쿼리할 수 있습니다. 확장 하 여 **OnModelCreating** 에서 지정 하는 메서드를는 **코드** 데이터베이스 테이블에 장르 매핑할 수는 방법입니다. 이 msdn 문서에서 DBContext 및 DBSet에 대 한 자세한 정보를 찾을 수 있습니다: [링크](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>작업 4-데이터베이스 쿼리

이 태스크에서는 하드 코드 된 데이터를 사용 하는 대신를 검색 하는 데이터베이스에서 있도록 StoreController 클래스를 업데이트 합니다.

> [!NOTE]
> 연습 1과 마찬가지로이 작업이입니다.
> 
> 연습 1을 완료 한 경우 이러한 단계는 두 방법 모두 동일 하 게 기록 됩니다 (처음에 데이터베이스 또는 Code first). 데이터가 모델에 연결 어떻게 다른 지 하지만 데이터 엔터티에 대 한 액세스는 컨트롤러에서 투명 아직 합니다.


1. 열기 **Controllers\StoreController.cs** 의 인스턴스를 저장 하는 클래스에 다음 필드를 추가 하 고는 **MusicStoreEntities** 라는 클래스를 **storeDB**:

    (코드 조각- *모델 데이터 액세스 및-e x 1 storeDB*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. **MusicStoreEntities** 클래스는 데이터베이스의 각 테이블에 대 한 컬렉션 속성을 노출 합니다. 업데이트 **찾아보기** 모든 장르를 가져오려는 작업 메서드는 **앨범**합니다.

    (코드 조각- *모델 및 데이터 액세스-e x 2 저장소 찾아보기*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > .NET 호출의 기능을 사용 하는 **LINQ** 프로그래밍할 수 있습니다 (통합 언어 쿼리)-이 데이터베이스에 대해 코드를 실행 하 고 반환 하는 이러한 컬렉션에 대 한 강력한 형식의 쿼리 식을 작성 하 개체 합니다.
    > 
    > LINQ에 대 한 자세한 내용은 참조 하십시오는 [msdn 사이트](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)합니다.
3. 업데이트 **인덱스** 동작 메서드를 모든 장르를 검색 합니다.

    (코드 조각- *모델 및 데이터 액세스-e x 2 저장소 인덱스*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. 업데이트 **인덱스** 동작 메서드의 모든 장르를 검색 하 고 목록에 컬렉션을 변환 합니다.

    (코드 조각- *모델 및 데이터 액세스-e x 2 저장소 GenreMenu*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>5-응용 프로그램 실행 작업

이 작업에서는 저장소 인덱스 페이지에 하드 코드 된 것 대신 데이터베이스에 저장 된 장르 표시 이제 됩니다 확인 합니다. 하기 때문에 템플릿 보기를 변경할 필요가 없습니다는 **StoreController** 동일한 반환 **StoreIndexViewModel** 이전 처럼 하지만이 이번에는 데이터는 데이터베이스에서 가져옵니다.

1. 솔루션 및 키를 눌러 다시 빌드 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. 확인의 메뉴 **장르** 는 더 이상 하드 코드 된 목록 및 데이터는 데이터베이스에서 직접 검색 됩니다.

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    *데이터베이스에서 검색 장르*
3. 이제 모든 장르로 이동 하 고 데이터베이스에서 앨범 채워집니다 확인 합니다.

    ![데이터베이스에서 앨범 검색](aspnet-mvc-4-models-and-data-access/_static/image23.png "앨범을 데이터베이스에서 검색")

    *데이터베이스에서 검색 앨범*

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a>매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 연습 3:

이 연습에서는 매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 방법 및 쿼리 결과 모양 지정을 사용 하는 방법에 설명 합니다, 그리고 번호 데이터베이스 감소 하는 기능에 더 효율적으로 검색 하는 동안 데이터에 액세스 합니다.

> [!NOTE]
> 쿼리 결과 모양 지정에 자세한 내용은 다음을 방문 [msdn 문서](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)합니다.


<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a>작업 1-수정 StoreController 앨범 데이터베이스에서 검색 하려면

이 작업에서는 변경 됩니다는 **StoreController** 앨범 특정 장르에서 검색할 데이터베이스에 액세스 하는 클래스입니다.

1. 열기는 **시작** 솔루션에 있는 **Source\Ex3 QueryingTheDatabaseWithParametersCodeFirst\Begin** 코드 중심 접근 방식을 사용 하려는 경우 폴더 또는 **Source\ Ex3 QueryingTheDatabaseWithParametersDBFirst\Begin** 폴더 데이터베이스 중심 접근 방식을 사용 하려는 경우. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.

    1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
    2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
    3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

    > [!NOTE]
    > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 열기는 **StoreController** 변경 하는 클래스는 **찾아보기** 동작 메서드가 있습니다. 이 수행 하는 **솔루션 탐색기**를 확장 하 고는 **컨트롤러** 폴더를 두 번 클릭 **StoreController.cs**합니다.
3. 변경 된 **찾아보기** 동작 메서드를 앨범 특정 장르에 대 한 검색 합니다. 이렇게 하려면 다음 코드를 바꿉니다.

    (코드 조각- *모델 및 데이터 액세스-Ex3 StoreController BrowseMethod*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

    > [!NOTE]
    > 엔터티 컬렉션을 채우려면 사용 해야는 **Include** 너무 앨범을 검색 하려면를 지정 하는 메서드. 사용할 수는 있습니다. **Single()** linq에서 확장 때문이 경우 하나의 장르 앨범에 대 한 합니다. **Single()** 메서드는이 경우 이름이 정의 된 값과 일치 되도록 단일 장르 개체를 지정 하는 매개 변수로 람다 식을 사용 합니다.
    > 
    > 장르 개체를 검색할 때도 로드를 원하는 다른 관련된 엔터티를 나타낼 수 있도록 하는 기능을 걸립니다. 라는이 기능은 **쿼리 결과 셰이핑**, 정보를 검색할 데이터베이스에 액세스 하는 데 필요한 시간 수를 줄일 수 있습니다. 이 시나리오에서는 검색할 장르에 대 한 앨범을 프리페치 하도록 합니다.
    > 
    > 쿼리에 포함 된 **Genres.Include (&quot;앨범&quot;)** 관련된 앨범도 지정할 수 있습니다. 이 값은 단일 데이터베이스 요청에서 Genre 및 앨범 모두 데이터를 검색 하므로 보다 효율적인 응용 프로그램에서 발생 합니다.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>작업 2-응용 프로그램 실행

이 작업에서는 응용 프로그램을 실행 하 고 데이터베이스에서 특정 genre의 앨범을 검색 합니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **/저장소/찾아보기? 장르 Pop =** 데이터베이스에서 결과 가져오는 중 확인 합니다.

    ![장르별로 검색](aspnet-mvc-4-models-and-data-access/_static/image24.png "장르별로 검색")

    *검색/저장소/찾아보기? 장르 Pop =*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a>작업 3-Id로 앨범에 액세스

이 태스크에서는 앨범 자신의 id를 가져올 이전 절차를 반복 합니다.

1. Visual Studio로 반환 하는 데 필요한 경우 브라우저를 닫습니다. 열기는 **StoreController** 변경 하는 클래스는 **세부 정보** 동작 메서드가 있습니다. 이 수행 하는 **솔루션 탐색기**를 확장 하 고는 **컨트롤러** 폴더를 두 번 클릭 **StoreController.cs**합니다.
2. 변경 된 **세부 정보** 앨범 세부 정보를 검색할 작업 메서드를 기반으로 해당 **Id**합니다. 이렇게 하려면 다음 코드를 바꿉니다.

    (코드 조각- *모델 및 데이터 액세스-Ex3 StoreController DetailsMethod*)


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 태스크에서는 웹 브라우저에서 응용 프로그램을 실행 및 해당 id 앨범 세부 정보를 가져올 됩니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 합니다.
2. 프로젝트 홈 페이지에서 시작합니다. URL을 변경 **/Store/Details/51** 하거나 장르 찾은 앨범 데이터베이스에서 결과 가져오는 중 확인을 선택 합니다.

    ![세부 정보를 검색](aspnet-mvc-4-models-and-data-access/_static/image25.png "세부 정보를 검색 합니다.")

    */Store/Details/51 검색*

> [!NOTE]
> 다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수는 또한 [부록 b: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixB)합니다.


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

ASP.NET MVC 모델 및 데이터 액세스의 기본적인 사항을 배웠습니다 실습 랩이 완료, 사용 하 여는 **Database First** 접근 방식으로 **Code First** 접근 방식:

- 해당 데이터를 처리 하기 위해 솔루션에 데이터베이스를 추가 하는 방법
- 대신 하드 코드 된 데이터베이스에서 가져온 데이터와 함께 템플릿 보기를 제공 하기 위해 컨트롤러를 업데이트 하는 방법
- 매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 방법
- 쿼리 결과 셰이핑, 데이터베이스 액세스의 수를 줄이는 기능 데이터를 더욱 효율적으로 검색을 사용 하는 방법
- 모델 데이터베이스에 연결할 Microsoft Entity framework에서 Database First 및 Code First 접근 방식을 사용 하는 방법

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 a: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여  **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** . 다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.

1. 로 이동 [ [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)합니다. 또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; *Visual Studio Express 2012 for Web Windows Azure SDK와*&quot;합니다.
2. 클릭 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.

    ![Visual Studio Express 설치](aspnet-mvc-4-models-and-data-access/_static/image26.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건 동의](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **마침**합니다.

    ![설치 완료](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.

    ![웹 타일에 대 한 VS Express](aspnet-mvc-4-models-and-data-access/_static/image30.png)

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

    ![Windows Azure 포털에 로그온](aspnet-mvc-4-models-and-data-access/_static/image31.png "Windows Azure 포털에 로그인")

    *Windows Azure 관리 포털에 로그온*
2. 클릭 **새로** 명령 모음에서 합니다.

    ![새 웹 사이트를 만드는](aspnet-mvc-4-models-and-data-access/_static/image32.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. 클릭 **계산** | **웹 사이트**합니다. 그런 다음 선택 **빠른 생성** 옵션입니다. 새 웹 사이트에 대 한 사용 가능한 URL을 입력 하 고 클릭 **웹 사이트 만들기**합니다.

    > [!NOTE]
    > Windows Azure 웹 사이트는 호스트를 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램입니다. 빨리 만들기 옵션을 사용 하면 완성 된 웹 응용 프로그램을 Windows Azure 웹 사이트에서 포털 외부에 배포할 수 있습니다. 데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](aspnet-mvc-4-models-and-data-access/_static/image33.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.
5. 웹 사이트가 만들어지면 아래 링크를 클릭 하 고 **URL** 열입니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트를 찾아](aspnet-mvc-4-models-and-data-access/_static/image34.png "새 웹 사이트를 검색 합니다.")

    *새 웹 사이트를 검색합니다.*

    ![실행 중인 웹 사이트](aspnet-mvc-4-models-and-data-access/_static/image35.png "실행 중인 웹 사이트")

    *실행 중인 웹 사이트*
6. 포털로 돌아가서 아래에서 웹 사이트의 이름을 클릭는 **이름** 관리 페이지를 표시 하는 열입니다.

    ![웹 사이트 관리 페이지 열기](aspnet-mvc-4-models-and-data-access/_static/image36.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. 에 **대시보드** 페이지의 **눈에 보는** 섹션에서 클릭는 **게시 프로필 다운로드** 링크 합니다.

    > [!NOTE]
    > *게시 프로필* 각각의 활성화 된 게시 방법에 대 한 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 데 필요한 정보가 모두 포함 되어 있습니다. 게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열이 포함 되어 있습니다. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 읽는 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 합니다.

    ![게시 프로필 다운로드 웹 사이트](aspnet-mvc-4-models-and-data-access/_static/image37.png "게시 프로필 다운로드 웹 사이트")

    *게시 프로필 다운로드 웹 사이트*
8. 알려진된 위치에 게시 프로필 파일을 다운로드 합니다. 더 이상이 연습에서는 Visual Studio에서 웹 응용 프로그램 Windows Azure 웹 사이트를 게시 하려면이 파일을 사용 하는 방법을 표시 됩니다.

    ![게시 프로필 파일을 저장](aspnet-mvc-4-models-and-data-access/_static/image38.png "게시 프로필 저장")

    *게시 프로필 파일을 저장합니다.*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL Server를 활용 하는 경우 데이터베이스를 SQL 데이터베이스 서버 만들기 해야 합니다. SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 태스크를 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하기 위해 SQL 데이터베이스 서버를 해야 합니다. Windows Azure 관리 포털에서 구독의 SQL 데이터베이스 서버를 볼 수 있습니다 **Sql 데이터베이스** | **서버** | **서버 대시보드**합니다. 만든 서버 없는 경우 수행 하 여 만들 수 있습니다는 **추가** 명령 모음에서 단추입니다. 기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**, 다음 작업에 사용 됩니다. 만들지 마십시오 데이터베이스 아직 대로 이후 단계에서 생성 됩니다.

    ![SQL 데이터베이스 서버 대시보드](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL 데이터베이스 서버 대시보드")

    *SQL 데이터베이스 서버 대시보드*
2. 다음 태스크에서는 서버 목록에 사용자의 로컬 IP 주소를 포함 해야 이러한 이유로 Visual Studio에서 데이터베이스 연결을 테스트 **허용 IP 주소**합니다. 작업을 수행 하려면 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여넣습니다는 **시작 IP 주소** 및 **끝IP주소** 클릭 하 고 텍스트 상자는 ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) 단추입니다.

    ![클라이언트 IP 주소를 추가합니다.](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    *클라이언트 IP 주소를 추가합니다.*
3. 한 번는 **클라이언트 IP 주소** 허용된 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 하 여 변경 사항을 확인 합니다.

    ![변경 확인](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    *변경 확인*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션으로 돌아갑니다. 에 **솔루션 탐색기**웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.

    ![응용 프로그램을 게시](aspnet-mvc-4-models-and-data-access/_static/image43.png "응용 프로그램을 게시")

    *웹 사이트를 게시*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필 가져오기](aspnet-mvc-4-models-and-data-access/_static/image44.png "게시 프로필 가져오기")

    *게시 프로필 가져오기*
3. 클릭 **연결 확인**합니다. 유효성 검사가 완료 되 면 클릭 **다음**합니다.

    > [!NOTE]
    > 연결 유효성 검사 단추 옆에 표시 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.

    ![연결 유효성 검사](aspnet-mvc-4-models-and-data-access/_static/image45.png "연결 유효성 검사")

    *연결 유효성 검사*
4. 에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추 클릭 (즉, **DefaultConnection**).

    ![웹 배포 구성](aspnet-mvc-4-models-and-data-access/_static/image46.png "웹 배포 구성")

    *웹 배포 구성*
5. 다음과 같이 데이터베이스 연결을 구성 합니다.

    - 에 **서버 이름** SQL 데이터베이스 서버 URL 사용 하 여 입력 된 *tcp:* 접두사입니다.
    - **사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.
    - **암호** 서버 관리자 로그인 암호를 입력 합니다.
    - 새 데이터베이스 이름을 입력 합니다.

    ![대상 연결 문자열 구성](aspnet-mvc-4-models-and-data-access/_static/image47.png "대상 연결 문자열 구성")

    *대상 연결 문자열 구성*
6. 그런 다음 **확인**을 클릭합니다. 데이터베이스를 만들려는 대화 상자가 나타나면 **예**합니다.

    ![데이터베이스를 만드는](aspnet-mvc-4-models-and-data-access/_static/image48.png "데이터베이스 문자열 만들기")

    *데이터베이스를 만드는 중*
7. Windows azure에서 SQL 데이터베이스에 연결 하기 위해 사용할 연결 문자열은 기본 연결 텍스트 상자 내에서 표시 됩니다. **다음**을 클릭합니다.

    ![SQL 데이터베이스를 가리키는 연결 문자열](aspnet-mvc-4-models-and-data-access/_static/image49.png "SQL 데이터베이스를 가리키는 연결 문자열")

    *SQL 데이터베이스를 가리키는 연결 문자열*
8. 에 **미리 보기** 페이지 **게시**합니다.

    ![웹 응용 프로그램을 게시](aspnet-mvc-4-models-and-data-access/_static/image50.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>부록 c: 코드 조각을 사용 하 여

코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다. 랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.

![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](aspnet-mvc-4-models-and-data-access/_static/image51.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")

*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*

***키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드를 삽입 하려는 위치에 커서를 놓습니다.
2. 공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.
3. IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.
4. 올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).
5. 커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.

![코드 조각 이름을 입력 하기 시작](aspnet-mvc-4-models-and-data-access/_static/image52.png "조각 이름을 입력 하기 시작")

*코드 조각 이름을 입력 하기 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각 선택](aspnet-mvc-4-models-and-data-access/_static/image53.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")

*Tab 키를 눌러 강조 표시 된 코드 조각 선택*

![확장 하 고 Tab 키를 눌러 다시 코드 조각](aspnet-mvc-4-models-and-data-access/_static/image54.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")

*확장 하 고 Tab 키를 눌러 다시 코드 조각*

***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1입니다. 코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.

1. 선택 **조각 삽입** 이어서 **내 코드 조각**합니다.
2. 클릭 하 여 목록에서 관련 조각을 선택 합니다.

![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-models-and-data-access/_static/image55.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")

*코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*

![클릭 하 여 목록에서 관련 조각을 선택](aspnet-mvc-4-models-and-data-access/_static/image56.png "클릭 하 여 목록에서 관련 조각을 선택")

*클릭 하 여 목록에서 관련 조각을 선택합니다*
