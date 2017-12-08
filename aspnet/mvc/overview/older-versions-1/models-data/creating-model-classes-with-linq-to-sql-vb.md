---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
title: "LINQ to SQL (VB)를 사용 하 여 모델 클래스 만들기 | Microsoft Docs"
author: microsoft
description: "이 자습서의 목표는 ASP.NET MVC 응용 프로그램에 대 한 모델 클래스를 만드는 방법 중 하나가 설명 하는입니다. 이 자습서에서는 c 모델을 작성 하는 방법에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: a4a25a75-d71f-4509-98b4-df72e748985a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
msc.type: authoredcontent
ms.openlocfilehash: 972d5b11049825e84e070ef1c4b2b90116654397
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-model-classes-with-linq-to-sql-vb"></a>LINQ to SQL (VB)를 사용 하 여 모델 클래스 만들기
====================
여 [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_VB.pdf)

> 이 자습서의 목표는 ASP.NET MVC 응용 프로그램에 대 한 모델 클래스를 만드는 방법 중 하나가 설명 하는입니다. 이 자습서에서는 모델 클래스를 만들고 to SQL Microsoft LINQ 기능을 이용 하 여 데이터베이스 액세스를 수행 하는 방법에 알아봅니다.


이 자습서의 목표는 ASP.NET MVC 응용 프로그램에 대 한 모델 클래스를 만드는 방법 중 하나가 설명 하는입니다. 이 자습서에서는 모델 클래스를 만들고 to SQL Microsoft LINQ 기능을 이용 하 여 데이터베이스 액세스를 수행 하는 방법에 알아봅니다.

이 자습서에서는 기본 영화 데이터베이스 응용 프로그램을 빌드합니다. 빠르고 쉬운 방법에서 영화 데이터베이스 응용 프로그램을 가능한 만들어 시작 합니다. 이 컨트롤러 작업에서 직접 데이터 액세스는의 모든을 수행합니다.

다음으로, 저장소 패턴을 사용 하는 방법을 배웁니다. 리포지토리 패턴을 사용 하 여 약간 더 많은 작업이 필요 합니다. 그러나 채택이 패턴의 장점은에 적용할 수 있는 응용 프로그램을 빌드할 수 있다는 점입니다 변경 하 고 쉽게 테스트할 수 있습니다.

## <a name="what-is-a-model-class"></a>모델 클래스는 무엇입니까?

MVC 모델의 모든 MVC 뷰 또는 MVC 컨트롤러에 포함 되지 않은 응용 프로그램 논리를 포함 합니다. 특히, MVC 모델 모든 비즈니스 응용 프로그램 및 데이터 액세스 논리를 포함합니다.

데이터 액세스 논리를 구현 하는 다양 한 다양 한 기술 사용할 수 있습니다. 예를 들어 Microsoft Entity Framework, NHibernate, subsonic은 이러한 방식을, 또는 ADO.NET 클래스를 사용 하 여 데이터 액세스 클래스를 빌드할 수 있습니다.

이 자습서에서는 LINQ to SQL 사용 합니까를 쿼리하고 데이터베이스를 업데이트 합니다. LINQ to SQL의 Microsoft SQL Server 데이터베이스와의 상호 작용을 매우 쉽게 메서드를 제공 합니다. 그러나은 어떤 방식으로든에서 ASP.NET MVC 프레임 워크 LINQ to SQL에 연결 되지 않은 것을 알아야 합니다. ASP.NET MVC는 모든 데이터 액세스 기술과 호환 됩니다.

## <a name="create-a-movie-database"></a>영화 데이터베이스 만들기

이 자습서---모델 클래스를 구축 하는 방법을 보여 주기 위해 우리 작성 간단한 영화 데이터베이스 응용 프로그램. 첫 번째 단계는 새 데이터베이스를 만드는 것입니다. 응용 프로그램을 마우스 오른쪽 단추로 클릭\_메뉴 옵션을 선택 하는 솔루션 탐색기 창에서 데이터 폴더 **추가, 새 항목**합니다. SQL Server 데이터베이스 템플릿을 선택 MoviesDB.mdf, 이름을 지정 하 고 클릭 하 고 **추가** 단추 (그림 1 참조).


[![새 SQL Server 데이터베이스 추가](creating-model-classes-with-linq-to-sql-vb/_static/image2.png)](creating-model-classes-with-linq-to-sql-vb/_static/image1.png)

**그림 01**: 새 SQL Server 데이터베이스 추가 ([전체 크기 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-vb/_static/image3.png))


새 데이터베이스를 만든 후 응용 프로그램에서 MoviesDB.mdf 파일을 두 번 클릭 하 여 데이터베이스를 열 수 있습니다\_데이터 폴더. 서버 탐색기 창을 엽니다 MoviesDB.mdf 파일을 두 번 (그림 2 참조).

|  | Visual Web Developer를 사용 하는 경우 서버 탐색기 창의 데이터베이스 탐색기 창이 라고 합니다. |
| --- | --- |


[![서버 탐색기 창을 사용 하 여](creating-model-classes-with-linq-to-sql-vb/_static/image5.png)](creating-model-classes-with-linq-to-sql-vb/_static/image4.png)

**그림 02**: 서버 탐색기 창을 사용 하 여 ([전체 크기 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-vb/_static/image6.png))


우리의 영화를 나타내는 데이터베이스에 하나의 테이블을 추가 해야 합니다. 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다. 이 메뉴 옵션을 선택 하면 테이블 디자이너를 엽니다 (그림 3 참조).


[![서버 탐색기 창을 사용 하 여](creating-model-classes-with-linq-to-sql-vb/_static/image8.png)](creating-model-classes-with-linq-to-sql-vb/_static/image7.png)

**그림 03**: 테이블 디자이너 ([전체 크기 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-vb/_static/image9.png))


데이터베이스 테이블에 다음 열을 추가 해야 합니다.

| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| ID | Int | False |
| 제목 | Nvarchar(200) | False |
| 감독 | Nvarchar (50) | False |

Id 열에 두 가지 특별 한 작업을 수행 해야 합니다. 먼저, 테이블 디자이너에서 열을 선택 하 고 키 아이콘을 클릭 하 여 Id 열에 기본 키 열으로 표시 해야 합니다. LINQ to SQL 삽입을 수행 하거나 데이터베이스에 대해 업데이트할 때 기본 키 열을 지정 해야 합니다.

다음으로에 예는 값을 할당 하 여 Id 열을 Id 열으로 표시 해야는 **Id** 속성 (그림 3 참조). Id 열에 할당 된 새 번호를 자동으로 새 데이터 행을 테이블에 추가 되는 열이입니다.

이러한 변경을 수행한 후 이름 tblMovie로 테이블을 저장 합니다. 저장 단추를 클릭 하 여 테이블을 저장할 수 있습니다.

## <a name="create-linq-to-sql-classes"></a>LINQ to SQL 클래스 만들기

예제의 MVC 모델은 LINQ to SQL 클래스 tblMovie 데이터베이스 테이블을 나타내는 포함 됩니다. 이러한 LINQ to SQL 클래스를 만드는 가장 쉬운 방법은 모델 폴더를 마우스 오른쪽 단추로 클릭 한 다음를 선택 하십시오 **추가, 새 항목**, LINQ to SQL 클래스 템플릿 선택, 이름을 Movie.dbml, 클래스를 지정 하 고 클릭 하 고 **추가**단추 (그림 4 참조).


[![LINQ to SQL 클래스 만들기](creating-model-classes-with-linq-to-sql-vb/_static/image11.png)](creating-model-classes-with-linq-to-sql-vb/_static/image10.png)

**그림 04**: LINQ to SQL 클래스 만들기 ([전체 크기 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-vb/_static/image12.png))


영화 LINQ to SQL 클래스를 만든 후 즉시 개체 관계형 디자이너 나타납니다. LINQ to SQL 클래스 특정 데이터베이스 테이블을 나타내는 만들려는 Object Relational Designer로 서버 탐색기 창에서 데이터베이스 테이블을 끌 수 있습니다. Object Relational Designer로 tblMovie 데이터베이스 테이블을 추가 해야 한다고 (그림 4 참조).


[![개체 관계형 디자이너를 사용 하 여](creating-model-classes-with-linq-to-sql-vb/_static/image14.png)](creating-model-classes-with-linq-to-sql-vb/_static/image13.png)

**그림 05**: 개체 관계형 디자이너를 사용 하 여 ([전체 크기 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-vb/_static/image15.png))


기본적으로 개체 관계형 디자이너는 디자이너를 끌어다 놓으면 데이터베이스 테이블로 매우 동일한 이름을 가진 클래스를 만듭니다. 그러나 우리 클래스 tblMovie 호출 않으려는 경우 따라서 디자이너에서 클래스의 이름을 클릭 하 고 클래스의 이름을 영화로 변경 합니다.

마지막으로,를 클릭 해야는 **저장** 단추 (플로피 그림) LINQ to SQL 클래스에 저장 합니다. 그렇지 않으면 개체 관계형 디자이너에서 LINQ to SQL 클래스를 생성 하지 않습니다.

## <a name="using-linq-to-sql-in-a-controller-action"></a>LINQ to SQL 사용 하 여 컨트롤러 작업에서

LINQ to SQL 클래스를 만들었으므로 이제 해당 데이터를 검색 하는 데이터베이스에서 이러한 클래스를 사용할 수 있습니다. 이 섹션에서는 LINQ to SQL 클래스는 컨트롤러 작업 내에서 직접 사용 하는 방법을 설명 합니다. MVC 뷰에 tblMovies 데이터베이스 테이블에서 영화 목록을 표시 합니다.

먼저, HomeController 클래스를 수정 해야 합니다. 이 클래스는 응용 프로그램의 컨트롤러 폴더에서 찾을 수 있습니다. 목록 1의 클래스와 비슷하게 클래스를 수정 합니다.

**1 – 나열`Controllers\HomeController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample1.vb)]

목록 1의 index () 동작 LINQ to SQL DataContext 클래스 (MovieDataContext)를 사용 하 여 MoviesDB 데이터베이스를 나타냅니다. MoveDataContext 클래스는 Visual Studio 개체 관계형 디자이너에서 생성 되었습니다.

LINQ 쿼리는 모든 동영상 tblMovies 데이터베이스 테이블에서 검색 하는 DataContext에 대해 수행 됩니다. 영화 목록이 영화 라는 지역 변수가에 할당 됩니다. 마지막으로, 데이터 보기를 통해 보기에는 동영상 목록을 전달 됩니다.

영화를 표시 하려면 다음 인덱스 뷰를 수정 해야 합니다. Views\Home\ 폴더에 있는 인덱스 뷰를 찾을 수 있습니다. 보기 목록 2에서와 같이 인덱스 뷰를 업데이트 합니다.

**2 – 나열`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample2.aspx)]

공지 수정한 인덱스 뷰를 포함 하는 &lt;% 가져오기 네임 스페이스: % @&gt; 보기의 예외입니다. 이 지시어 MvcApplication1 네임 스페이스를 가져옵니다. 이 네임 스페이스 보기에서 영화 클래스-모델 클래스-특히에서 사용 하려면 필요 합니다.

목록 2 뷰에 For Each 루프의 모든 ViewData.Model 속성으로 표현 되는 항목을 반복 하 합니다. 각 동영상에 대 한 Title 속성의 값 표시 됩니다.

IEnumerable ViewData.Model 속성 값을 캐스팅 된 있는지를 확인 합니다. 이 ViewData.Model 내용을 반복 하는 데 필요 합니다. 또 다른 옵션 여기는 강력한 형식의 뷰를 만드는 것입니다. 강력한 형식의 뷰를 만들 때 보기의 코드 숨김 클래스의 특정 형식에 ViewData.Model 속성을 캐스팅 합니다.

HomeController 클래스 및 인덱스 뷰를 수정한 후 응용 프로그램을 실행 하는 경우 다음 받아볼 수 빈 페이지가 있습니다. TblMovies 데이터베이스 테이블의 영화 레코드가 있기 때문에 빈 페이지를 볼 수 있습니다.

TblMovies 데이터베이스 테이블에 레코드를 추가 하려면 서버 탐색기 창 (Visual Web Developer에서 데이터베이스 탐색기 창)에서 tblMovies 데이터베이스 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다. (그림 5 참조) 나타나는 표를 사용 하 여 영화 레코드를 삽입할 수 있습니다.


[![영화를 삽입합니다.](creating-model-classes-with-linq-to-sql-vb/_static/image17.png)](creating-model-classes-with-linq-to-sql-vb/_static/image16.png)

**그림 06**: 영화 삽입 ([전체 크기 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-vb/_static/image18.png))


TblMovies 테이블에 일부 데이터베이스 레코드를 추가 하는 응용 프로그램을 실행 한 후에 그림 7의 페이지가 표시 됩니다. 영화 데이터베이스 레코드의 모든 글머리 기호 목록에 표시 됩니다.


[![인덱스 뷰를 포함 하는 영화를 표시합니다.](creating-model-classes-with-linq-to-sql-vb/_static/image20.png)](creating-model-classes-with-linq-to-sql-vb/_static/image19.png)

**그림 07**: 표시 인덱스 뷰를 사용 하 여 동영상 ([전체 크기 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-vb/_static/image21.png))


## <a name="using-the-repository-pattern"></a>리포지토리 패턴을 사용 하 여

이전 섹션에서 LINQ to SQL 클래스는 컨트롤러 작업 내에서 직접 사용 했습니다. Index () 컨트롤러 작업에서 직접 MovieDataContext 클래스를 사용 합니다. 잘못 된 간단한 응용 프로그램의 경우이 작업을 수행 하는 일은 없습니다. 그러나 LINQ to SQL에 직접 작업 컨트롤러 클래스에서 더 복잡 한 응용 프로그램을 작성 해야 할 때 문제를 만듭니다.

컨트롤러 클래스 내에서 LINQ to SQL 사용 하면 나중에 데이터 액세스 기술 전환 하기 어렵습니다. 예를 들어 Microsoft LINQ to SQL 사용 하 여 Microsoft Entity Framework를 사용 하 여 데이터 액세스 기술로 전환할 수도 있습니다. 이 경우 응용 프로그램 내에서 데이터베이스를 액세스 하는 모든 컨트롤러를 다시 작성 해야 합니다.

LINQ to SQL 사용 하 여 컨트롤러 클래스 내에서 뿐만 아니라 어렵게 응용 프로그램에 대 한 단위 테스트를 작성 합니다. 일반적으로 단위 테스트를 수행 하는 경우 데이터베이스와 상호 작용 하지 않을 수 있습니다. 응용 프로그램 논리와 프로그램이 데이터베이스 서버를 테스트 하려면 단위 테스트를 사용 하려는 합니다.

MVC 응용 프로그램을 작성 하기 위해는 향후에 더 적응력이 뛰어난 변경 하며 더 쉽게 테스트할 수 있는, 리포지토리 패턴을 사용 하는 것이 좋습니다. 리포지토리 패턴을 사용 하면 모든 데이터베이스 액세스 논리를 포함 하는 별도 저장소 클래스를 만듭니다.

저장소 클래스를 만들 때 모든 저장소 클래스에 의해 사용 되는 메서드를 나타내는 인터페이스를 만듭니다. 컨트롤러에 내에서 저장소 대신 인터페이스에 대 한 코드를 작성 합니다. 이런 방식으로 나중에 다른 데이터 액세스 기술을 사용 하 여 저장소를 구현할 수 있습니다.

인터페이스 목록 3은 IMovieRepository, ListAll() 라는 단일 메서드를 나타냅니다.

**3 – 나열`Models\IMovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample3.vb)]

목록 4에 저장소 클래스 IMovieRepository 인터페이스를 구현합니다. 라는 ListAll() IMovieRepository 인터페이스에서 요구 하는 방법에 해당 하는 메서드가 포함 되어 있음을 확인 합니다.

**4 – 나열`Models\MovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample4.vb)]

마지막으로, 목록 5의 MoviesController 클래스는 리포지토리 패턴을 사용합니다. 더 이상 사용 LINQ to SQL 클래스 직접 합니다.

**5-나열`Controllers\MoviesController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample5.vb)]

MoviesController 클래스 목록 5에서 두 명의 생성자가 있는지 확인 합니다. 매개 변수가 없는 생성자를 첫 번째 생성자는 응용 프로그램을 실행 하는 경우 호출 됩니다. 이 생성자 MovieRepository 클래스의 인스턴스를 만들고 두 번째 생성자에 전달 합니다.

두 번째 생성자에 단일 매개 변수:는 IMovieRepository 매개 변수입니다. 이 생성자 라는 클래스 수준 필드에 매개 변수 값을 지정 \_저장소입니다.

MoviesController 클래스 종속성 주입 패턴 이라는 소프트웨어 디자인 패턴의 장점은 걸리고 있습니다. 특히 사용 생성자 종속성 주입 라는 것입니다. 자세한 내용은 Martin Fowler 하 여 다음 문서를 참조 하 여이 패턴에 대 한:

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

모든 (첫 번째 생성자는) 제외 MoviesController 클래스에서 코드와 상호 작용 하는 실제 MovieRepository 클래스 대신 IMovieRepository 인터페이스를 확인 합니다. 코드는 인터페이스의 구체적 구현 하는 대신 추상 인터페이스 상호 작용합니다.

응용 프로그램에서 사용 하는 데이터 액세스 기술 수정 하려는 경우 다음 있습니다 단순히 인터페이스를 구현할 수는 IMovieRepository 대체 데이터베이스 액세스 기술을 사용 하는 클래스입니다. 예를 들어 EntityFrameworkMovieRepository 클래스 또는 SubSonicMovieRepository 클래스를 만들 수 있습니다. 컨트롤러 클래스는 인터페이스에 대해 프로그래밍을 하기 때문에 IMovieRepository의 새 구현을 컨트롤러 클래스에 전달할 수 있습니다 및 클래스는 계속 작동 합니다.

또한 MoviesController 클래스를 테스트 하려는 경우 다음 전달할 수 있습니다 가짜 영화 저장소 클래스는 MoviesController를 합니다. 데이터베이스에 실제로 액세스 하지 않는 모든 IMovieRepository 인터페이스의 필요한 메서드를 포함 하는 클래스를 사용 하 여 IMovieRepository 클래스를 구현할 수 있습니다. 이런 방식으로 실제로 실제 데이터베이스에 액세스 하지 않고 단위 테스트 MoviesController 클래스 수 있습니다.

## <a name="summary"></a>요약

이 자습서의 목표는 to SQL Microsoft LINQ 기능을 이용 하 여 MVC 모델 클래스를 만드는 방법을 보여 주기 위해 했습니다. ASP.NET MVC 응용 프로그램에서 데이터베이스 데이터를 표시 하기 위한 두 가지 전략을 검사 했습니다. 첫째, LINQ to SQL 클래스 생성 하 고 사용 하는 컨트롤러 동작 내에서 직접 클래스. LINQ to SQL 클래스는 컨트롤러 내에서 사용 하 여 MVC 응용 프로그램에서 데이터베이스 데이터를 쉽게 표시할 및 수를 신속 하 게 있습니다.

다음으로, 데이터베이스 데이터를 표시 하기 위한 약간 더 어려운 하지만 더 확실 하 게 원동력이 경로 살펴본 합니다. 리포지토리 패턴을 활용 하 고 모든 데이터베이스 액세스 논리는 별도 저장소 클래스에 배치 합니다. 컨트롤러에 안내 드린 바 구체적인 클래스가 아니라 인터페이스에 대해 코드의 모든 합니다. 리포지토리 패턴의 장점은 나중에 데이터베이스 액세스 기술을 쉽게 변경할 수 있도록 하 고 컨트롤러 클래스를 쉽게 테스트할 수 있게 됩니다.

>[!div class="step-by-step"]
[이전](creating-model-classes-with-the-entity-framework-vb.md)
[다음](displaying-a-table-of-database-data-vb.md)
