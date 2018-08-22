---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
title: LINQ to SQL (C#)를 사용 하 여 모델 클래스 만들기 | Microsoft Docs
author: microsoft
description: 이 자습서의 목표는 한 가지 방법은 ASP.NET MVC 응용 프로그램에 대 한 모델 클래스 만들기를 설명 합니다. 이 자습서에서는 모델 c를 빌드하는 방법 알아보기...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f84b4a16-e8bb-49e8-87a0-1832879a3501
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
msc.type: authoredcontent
ms.openlocfilehash: c76e92ebfab1db162151ea5753888a60a4d54e59
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828629"
---
<a name="creating-model-classes-with-linq-to-sql-c"></a>LINQ to SQL (C#)를 사용 하 여 모델 클래스 만들기
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_CS.pdf)

> 이 자습서의 목표는 한 가지 방법은 ASP.NET MVC 응용 프로그램에 대 한 모델 클래스 만들기를 설명 합니다. 이 자습서에서는 모델 클래스를 작성 하 여 SQL로 Microsoft LINQ 기능을 활용 하 여 데이터베이스 액세스를 수행 하는 방법을 알아봅니다.


이 자습서의 목표는 한 가지 방법은 ASP.NET MVC 응용 프로그램에 대 한 모델 클래스 만들기를 설명 합니다. 이 자습서에서는 모델 클래스를 빌드하고 to SQL Microsoft LINQ 기능을 활용 하 여 데이터베이스 액세스를 수행 하는 방법을 알아봅니다.

이 자습서에서는 기본 영화 데이터베이스 응용 프로그램을 구축 합니다. 가능한 가장 빠르고 가장 쉬운 방법은에 영화 데이터베이스 응용 프로그램을 만들어 시작 합니다. 이 컨트롤러 작업에서 직접 데이터 액세스를 모두 수행합니다.

다음으로, 리포지토리 패턴을 사용 하는 방법에 알아봅니다. 리포지토리 패턴을 사용 하 여 약간 더 많은 작업이 필요 합니다. 그러나이 패턴을 채택의 장점은에 적응할 수 있는 응용 프로그램을 빌드할 수 있도록 변경 하 고 쉽게 테스트할 수 있습니다.

## <a name="what-is-a-model-class"></a>모델 클래스 란?

MVC 모델을 모든 MVC 뷰 또는 MVC 컨트롤러에서 포함 되지 않은 응용 프로그램 논리를 포함 합니다. 특히 MVC 모델을 모든 응용 프로그램 비즈니스 및 데이터 액세스 논리를 포함합니다.

데이터 액세스 논리를 구현 하는 다양 한 기술에 사용할 수 있습니다. 예를 들어, Microsoft Entity Framework, NHibernate, Subsonic 또는 ADO.NET 클래스를 사용 하 여 데이터 액세스 클래스를 빌드할 수 있습니다.

이 자습서에서는 쿼리 및 데이터베이스를 업데이트 하려면 LINQ to SQL 사용 합니다. LINQ to SQL Microsoft SQL Server 데이터베이스와 상호 작용을 매우 쉽게 메서드를 제공 합니다. 그러나 어떤 방식으로 ASP.NET MVC 프레임 워크 LINQ to SQL에 연결 되지 않은 알아야 할 것입니다. ASP.NET MVC는 모든 데이터 액세스 기술은 호환입니다.

## <a name="create-a-movie-database"></a>영화 데이터베이스 만들기

이 자습서-모델 클래스-을 빌드하는 방법을 보여 주기 위해 구축 간단한 영화 데이터베이스 응용 프로그램입니다. 첫 번째 단계는 새 데이터베이스를 만드는 것입니다. 앱을 마우스 오른쪽 단추로 클릭\_메뉴 옵션을 선택 하는 솔루션 탐색기 창에서 데이터 폴더 **추가, 새 항목**합니다. 선택 합니다 **SQL Server 데이터베이스** 템플릿을 MoviesDB.mdf, 이름을 지정 하 고 클릭 합니다 **추가** 단추 (그림 1 참조).


[![새 SQL Server 데이터베이스 추가](creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)

**그림 01**: 새 SQL Server 데이터베이스 추가 ([큰 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-cs/_static/image3.png))


새 데이터베이스를 만든 후 앱에서 MoviesDB.mdf 파일을 두 번 클릭 하 여 데이터베이스를 열 수 있습니다\_데이터 폴더. 서버 탐색기 창을 엽니다. MoviesDB.mdf 파일을 두 번 클릭 (그림 2 참조).

Visual Web Developer를 사용 하는 경우 서버 탐색기 창의 데이터베이스 탐색기 창이 라고 합니다.


[![서버 탐색기 창을 사용 하 여](creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)

**그림 02**: 서버 탐색기 창을 사용 하 여 ([큰 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-cs/_static/image6.png))


이 영화를 나타내는 데이터베이스에 테이블을 추가 해야 합니다. 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다. 이 메뉴 옵션을 선택 하면 테이블 디자이너를 엽니다 (그림 3 참조).


[![서버 탐색기 창을 사용 하 여](creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)

**그림 03**: 테이블 디자이너 ([큰 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-cs/_static/image9.png))


데이터베이스 테이블에는 다음 열을 추가 해야 합니다.

| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| ID | Int | False |
| 제목 | Nvarchar(200) | False |
| 책임자 | nvarchar (50) | False |

Id 열에 두 가지 특별 한 작업을 수행 해야 합니다. 첫째, 테이블 디자이너에서 열을 선택 하 고 키 아이콘을 클릭 하 여 Id 열에 기본 키 열으로 표시 해야 합니다. LINQ to SQL 삽입 또는 업데이트 된 데이터베이스에 대해 수행 하는 경우에 기본 키 열을 지정 해야 합니다.

예의 값을 할당 하 여 Id 열을 Id 열으로 표시 해야 하는 다음에 **Id** 속성 (그림 3 참조). Id 열은 할당 된 새 번호를 자동으로 데이터의 새 행을 테이블에 추가 되는 열.

## <a name="create-linq-to-sql-classes"></a>LINQ to SQL 클래스 만들기

MVC 모델은 LINQ to SQL 클래스 tblMovie 데이터베이스 테이블을 나타내는 포함 됩니다. 이러한 LINQ to SQL 클래스를 만드는 가장 쉬운 방법은 Models 폴더를 마우스 오른쪽 단추로 클릭을 선택 하는 것 **추가, 새 항목**, LINQ to SQL 클래스 템플릿 선택, 클래스 이름을 Movie.dbml, 제공 및 클릭을 **추가**단추 (그림 4 참조).


[![LINQ to SQL 클래스 만들기](creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)

**그림 04**: LINQ to SQL 클래스 만들기 ([큰 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-cs/_static/image12.png))


영화 LINQ to SQL 클래스를 만든 후에 즉시 Object Relational Designer에 표시 됩니다. Object Relational Designer LINQ to SQL 나타내는 클래스는 특정 데이터베이스 테이블을 만들려면 서버 탐색기 창에서 데이터베이스 테이블을 끌 수 있습니다. Object Relational Designer tblMovie 데이터베이스 테이블을 추가 해야 (그림 5 참조).


[![Object Relational Designer를 사용 하 여](creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)

**그림 05**: Object Relational Designer를 사용 하 여 ([큰 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-cs/_static/image15.png))


기본적으로 개체 관계형 디자이너는 디자이너를 끌어 데이터베이스 테이블 동일한 이름의 클래스를 만듭니다. 그러나 클래스를 호출 하려고 하지 않습니다 `tblMovie`합니다. 따라서 디자이너에서 클래스의 이름을 클릭 하 고 영화를 클래스의 이름을 변경 합니다.

마지막으로 클릭 해야 합니다 **저장** 단추 (플로피 그림) LINQ to SQL 클래스에 저장 합니다. 이 고, 그렇지 Object Relational Designer에서 LINQ to SQL 클래스를 생성할 수 없습니다.

## <a name="using-linq-to-sql-in-a-controller-action"></a>LINQ to SQL 사용 하 여 컨트롤러 작업

LINQ to SQL 클래스를 만들었으므로 이제 해당 데이터베이스에서 데이터를 검색할 이러한 클래스를 사용할 수 있습니다. 이 섹션에서는 LINQ to SQL 클래스는 컨트롤러 작업 내에서 직접 사용 하는 방법을 알아봅니다. MVC 뷰의 tblMovies 데이터베이스 테이블에서 영화 목록에 표시 됩니다.

첫째, HomeController 클래스를 수정 해야 합니다. 이 클래스는 응용 프로그램의 컨트롤러 폴더에서 찾을 수 있습니다. 목록 1에서 클래스와 비슷하게 클래스를 수정 합니다.

**목록 1 – `Controllers\HomeController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample1.cs)]

합니다 `Index()` 목록 1의 작업은 LINQ to SQL DataContext 클래스를 사용 (합니다 `MovieDataContext`)를 나타내는 `MoviesDB` 데이터베이스입니다. `MoveDataContext` Visual Studio 개체 관계형 디자이너에서 생성 된 클래스입니다.

모든 영화를 검색 하려면 DataContext에 대해 LINQ 쿼리를 수행 합니다 `tblMovies` 데이터베이스 테이블입니다. 영화 목록에 명명 된 로컬 변수에 할당 됩니다 `movies`합니다. 마지막으로, 영화 목록에는 뷰에 데이터 보기를 통해 전달 됩니다.

영화를 표시 하기 위해 다음 인덱스 보기 수정 해야 합니다. 인덱스 뷰를 찾을 수 있습니다는 `Views\Home\` 폴더입니다. 목록 2에서 뷰와 같이 표시 되도록 인덱스 보기를 업데이트 합니다.

**2 – 나열 `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample2.aspx)]

수정한 인덱스 뷰를 포함 하는 공지를 `<%@ import namespace %>` 뷰의 맨 위에 있는 지시문입니다. 이 지시문을 가져옵니다는 `MvcApplication1.Models namespace`합니다. 이 네임 스페이스를 사용 하기 위해 필요 합니다 `model` 특히 클래스는 `Movie` 뷰에서 클래스.

목록 2에서 뷰에 `foreach` 가 나타내는 항목의 모든 반복 루프를 `ViewData.Model` 속성입니다. 값을 `Title` 각각에 대 한 속성이 표시 됩니다 `movie`합니다.

값을 `ViewData.Model` 속성으로 캐스팅 됩니다는 `IEnumerable`합니다. 내용을 반복 하는 데 필요한 이것이 `ViewData.Model`합니다. 강력한 형식의 만들려면 또 다른 옵션 여기은 `view`합니다. 강력한 형식의 만들면 `view`, 캐스팅을 `ViewData.Model` 뷰의 코드 숨김 클래스의 특정 형식으로 속성입니다.

수정 후 응용 프로그램을 실행 하는 경우는 `HomeController` 클래스 및 인덱스 보기 빈 페이지를 갖게 됩니다. 에 영화 레코드가 없으므로 빈 페이지를 얻게 된 `tblMovies` 데이터베이스 테이블입니다.

레코드를 추가 하려면 합니다 `tblMovies` 데이터베이스 테이블을 마우스 오른쪽 단추로 클릭는 `tblMovies` 데이터베이스 (데이터베이스 탐색기 창이 Visual Web Developer) 서버 탐색기 창에서 테이블 및 테이블 데이터 표시 메뉴 옵션을 선택 합니다. 삽입할 수 있습니다 `movie` 나타납니다 (그림 6 참조)는 표를 사용 하 여 레코드입니다.


[![영화를 삽입합니다.](creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)

**그림 06**: 영화 삽입 ([큰 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-cs/_static/image18.png))


일부 데이터베이스 레코드를 추가한 후의 `tblMovies` 테이블에 응용 프로그램을 실행, 그림 7에서 페이지가 표시 됩니다. 모든 영화 데이터베이스 레코드의 글머리 기호 목록에 표시 됩니다.


[![인덱스 뷰를 사용 하 여 영화를 표시합니다.](creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)

**그림 07**: 인덱스 뷰를 사용 하 여 영화 표시 ([큰 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-cs/_static/image21.png))


## <a name="using-the-repository-pattern"></a>리포지토리 패턴을 사용 하 여

이전 섹션에서는 LINQ to SQL 클래스는 컨트롤러 작업 내에서 직접 사용 했습니다. 사용 합니다 `MovieDataContext` 에서 직접 클래스를 `Index()` 컨트롤러 작업입니다. 간단한 응용 프로그램의 경우 이렇게 문제가 없습니다. 그러나 더 복잡 한 응용 프로그램을 빌드하는 경우 컨트롤러 클래스에서 직접 LINQ to SQL 사용 하 여 작업 문제를 만듭니다.

컨트롤러 클래스 내에서 LINQ to SQL 사용 하면 나중에 데이터 액세스 기술 전환 하기 어렵습니다. 예를 들어, Microsoft Entity Framework를 사용 하 여 데이터 액세스 기술로 사용자를 Microsoft LINQ to SQL 사용 하 여 전환할 수도 있습니다. 이 경우 응용 프로그램 내에서 데이터베이스에 액세스 하는 모든 컨트롤러를 다시 작성 해야 합니다.

컨트롤러 클래스 내에서 LINQ to SQL 사용 하기가 응용 프로그램에 대 한 단위 테스트를 작성 하기가 어렵습니다. 일반적으로 단위 테스트를 수행 하는 경우 데이터베이스와 상호 작용 하지 않을 수 있습니다. 단위 테스트를 사용 하 여 응용 프로그램 논리와 데이터베이스 서버 없습니다를 테스트할 하려고 합니다.

MVC 응용 프로그램을 빌드하려면는 향후에 더 융통성 있는 변경 하며 더 쉽게 테스트 하는, 리포지토리 패턴을 사용 하는 것이 좋습니다. 리포지토리 패턴을 사용 하면 모든 데이터베이스 액세스 논리를 포함 하는 별도 리포지토리 클래스를 만듭니다.

리포지토리 클래스를 만들 때 만든 모든 리포지토리 클래스에 의해 사용 된 메서드를 나타내는 인터페이스입니다. 컨트롤러 내에서 저장소 대신 인터페이스에 대 한 코드를 작성 합니다. 이런 방식으로 나중에 다른 데이터 액세스 기술을 사용 하 여 저장소를 구현할 수 있습니다.

보기 3의 인터페이스 이름은 `IMovieRepository` 라는 단일 메서드가 나타내고 `ListAll()`합니다.

**3 – 나열 `Models\IMovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample3.cs)]

목록 4에서 리포지토리 클래스를 구현 하는 `IMovieRepository` 인터페이스입니다. 메서드가 포함 되어 있는지 `ListAll()` 에서 요구 하는 방법에 해당 하는 `IMovieRepository` 인터페이스입니다.

**4-목록 `Models\MovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample4.cs)]

마지막으로 `MoviesController` 목록 5의 클래스는 리포지토리 패턴을 사용 합니다. 이 더 이상 LINQ to SQL 클래스 직접 사용 합니다.

**5-목록 `Controllers\MoviesController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample5.cs)]

다음에 유의 합니다 `MoviesController` 목록 5의 클래스는 두 명의 생성자입니다. 매개 변수가 없는 생성자를 첫 번째 생성자는 응용 프로그램을 실행 하는 경우 호출 됩니다. 이 생성자의 인스턴스를 만듭니다는 `MovieRepository` 클래스 및 두 번째 생성자에 전달 합니다.

두 번째 생성자는 단일 매개 변수가:는 `IMovieRepository` 매개 변수입니다. 이 생성자 라는 클래스 수준 필드에는 매개 변수 값 할당 `_repository`합니다.

`MoviesController` 클래스 종속성 주입 패턴 이라는 소프트웨어 디자인 패턴을 활용 됩니다. 특히 생성자 종속성 주입에 잠깐 사용 하는 것입니다. 자세한 내용은 Martin fowler의 다음 문서를 참조 하 여이 패턴에 대 한 합니다.

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

코드의 모든 합니다 `MoviesController` (제외 하 고 첫 번째 생성자는) 클래스와 상호 작용 하는 `IMovieRepository` 인터페이스 대신 실제 `MovieRepository` 클래스입니다. 인터페이스의 구체적인 구현 대신 추상 인터페이스를 사용 하 여 코드를 상호 작용합니다.

응용 프로그램에서 사용 되는 데이터 액세스 기술 수정 하려는 경우 간단히 구현할 수 있습니다는 `IMovieRepository` 대체 데이터베이스 액세스 기술을 사용 하는 클래스를 사용 하 여 인터페이스입니다. 예를 들어, 만들 수 있습니다는 `EntityFrameworkMovieRepository` 클래스 또는 `SubSonicMovieRepository` 클래스입니다. 컨트롤러 클래스는 인터페이스에 대해 프로그래밍을 새롭게 구현한 전달할 수 있습니다 `IMovieRepository` 컨트롤러에 클래스 및 클래스는 계속 작동 합니다.

또한 테스트 하려는 경우는 `MoviesController` 가짜 영화 리포지토리 클래스를 전달할 수 있습니다 다음 클래스는 `HomeController`합니다. 구현할 수 있습니다 합니다 `IMovieRepository` 않습니다 실제로 액세스 데이터베이스 모두의 필수 메서드를 포함 하는 클래스를 사용 하 여 클래스를 `IMovieRepository` 인터페이스입니다. 이렇게 하면 단위 테스트는 `MoviesController` 실제로 실제 데이터베이스에 액세스 하지 않고 클래스입니다.

## <a name="summary"></a>요약

이 자습서의 목적은 sql Microsoft LINQ 기능을 활용 하 여 MVC 모델 클래스를 만드는 방법을 보여 주기 위해 했습니다. ASP.NET MVC 응용 프로그램에서 데이터베이스 데이터를 표시 하기 위한 두 가지 전략을 검사 했습니다. 첫째, LINQ to SQL 클래스 생성 하 고 컨트롤러 작업 내에서 직접 클래스를 사용 합니다. LINQ to SQL 클래스는 컨트롤러 내에서 사용 하 여 신속 하 게 할 수 있도록 하 고 쉽게 MVC 응용 프로그램에서 데이터베이스 데이터를 표시 합니다.

다음으로, 데이터베이스 데이터를 표시 하기 위한 약간 더 어렵습니다 하지만 훨씬 고리가 만들어집니다 경로 살펴보았습니다. 리포지토리 패턴을 활용 하 고 모든 데이터베이스 액세스 논리는 별도 저장소 클래스에 배치 합니다. 컨트롤러에서 우리가 작성 한 모든 구체적인 클래스가 아니라 인터페이스에 대 한 코드입니다. 리포지토리 패턴의 장점은 나중에 데이터베이스 액세스 기술을 쉽게 변경할 수 있도록 하는 컨트롤러 클래스를 쉽게 테스트할 수 있도록 합니다.

> [!div class="step-by-step"]
> [이전](creating-model-classes-with-the-entity-framework-cs.md)
> [다음](displaying-a-table-of-database-data-cs.md)
