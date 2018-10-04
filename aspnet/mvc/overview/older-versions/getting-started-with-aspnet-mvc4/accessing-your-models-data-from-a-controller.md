---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: 컨트롤러에서 모델의 데이터에 액세스 | Microsoft Docs
author: Rick-Anderson
description: '참고: 업데이트 된이이 자습서는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 더 간단 하 게 따르고 데모 중...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 6d4d2a5f30e55cc876632f9f1bf73ab534a702ad
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577407"
---
<a name="accessing-your-models-data-from-a-controller"></a>컨트롤러에서 모델의 데이터에 액세스
====================
[Rick Anderson]((https://twitter.com/RickAndMSFT))

> > [!NOTE]
> > 이 자습서는 업데이트 된 버전을 사용할 수 [여기](../../getting-started/introduction/getting-started.md) 는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 합니다. 보다 안전 하 고 더 간단 하 게 수행 되며 더 많은 기능을 보여 줍니다.


이 섹션에서는 새 만듭니다 `MoviesController` 클래스 및 영화 데이터를 검색 하 고 뷰 템플릿을 사용 하 여 브라우저에 표시 하는 코드를 작성 합니다.

**응용 프로그램을 빌드할** 다음 단계로 진행 하기 전에 합니다.

마우스 오른쪽 단추로 클릭 합니다 *컨트롤러* 폴더를 만들어 새 `MoviesController` 컨트롤러입니다. 아래 옵션에는 응용 프로그램을 빌드할 때까지 표시 되지 않습니다. 다음 옵션을 선택 합니다.

- 컨트롤러 이름: **MoviesController**합니다. (기본값입니다. )
- 템플릿: **Entity Framework를 사용 하 여 읽기/쓰기 작업 및 보기를 사용 하 여 MVC 컨트롤러**합니다.
- 모델 클래스: **Movie (MvcMovie.Models)** 합니다.
- 데이터 컨텍스트 클래스: **MovieDBContext (MvcMovie.Models)** 합니다.
- 보기: **Razor (CSHTML)** 합니다. (기본값입니다.)

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

**추가**를 클릭합니다. Visual Studio Express 다음 파일 및 폴더를 만듭니다.

- *MoviesController.cs* 프로젝트의 파일 *컨트롤러* 폴더입니다.
- A *영화* 프로젝트의 폴더 *뷰* 폴더입니다.
- *Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, 및 *Index.cshtml* 새 *Views\Movies* 폴더입니다.

ASP.NET MVC 4 자동으로 생성 됩니다는 CRUD (만들기, 읽기, 업데이트 및 삭제) 작업 메서드와 뷰 있습니다 (자동으로 만들도록 CRUD 작업 메서드와 뷰 스 캐 폴딩이라고). 이제 모든 기능을 갖춘 웹 응용 프로그램을 만들기, 나열, 편집 및 동영상 항목을 삭제할 수 있습니다.

응용 프로그램을 실행 하 고 이동 합니다 `Movies` 컨트롤러를 추가 하 여 */Movies* 브라우저의 주소 표시줄에서 URL로 합니다. 응용 프로그램은 기본 라우팅을 의존 하기 때문에 (에 정의 된 합니다 *Global.asax* 파일), 브라우저 요청 `http://localhost:xxxxx/Movies` 기본값으로 라우팅됩니다 `Index` 의 동작 메서드는 `Movies` 컨트롤러입니다. 브라우저 요청 말해 `http://localhost:xxxxx/Movies` 같습니다 효과적으로 브라우저 요청 `http://localhost:xxxxx/Movies/Index`합니다. 결과 빈 목록을 영화, 이므로 아직 추가 하지 않았습니다.

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a>영화를 만들기

**새로 만들기** 링크를 선택합니다. 영화에 대 한 일부 정보를 입력 한 다음 클릭 합니다 **만들기** 단추입니다.

![](accessing-your-models-data-from-a-controller/_static/image3.png)

클릭 하는 **만들기** 단추 하면 폼이 데이터베이스에서 동영상 정보가 저장 된 서버에 게시할 수 있습니다. 다음으로 리디렉션됩니다 합니다 */Movies* URL을 목록에서 새로 만든된 동영상을 볼 수 있습니다.

![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")

나머지 몇 개의 동영상 항목을 만듭니다. 모두 작동하는 **편집**, **세부 정보** 및 **삭제** 링크를 사용해 봅니다.

## <a name="examining-the-generated-code"></a>생성된 된 코드 검사

엽니다는 *Controllers\MoviesController.cs* 파일을 생성 된 검사 `Index` 메서드. 영화 컨트롤러와의 일부를 `Index` 메서드는 다음과 같습니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

다음 줄을 `MoviesController` 앞에서 설명한 대로 클래스는 영화 데이터베이스 컨텍스트를 인스턴스화합니다. 쿼리, 편집 및 삭제 영화에 영화 데이터베이스 컨텍스트를 사용할 수 있습니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

요청을를 `Movies` 컨트롤러의 모든 항목을 반환 합니다 `Movies` 영화 데이터베이스의 테이블 다음 결과 전달는 `Index` 보기.

## <a name="strongly-typed-models-and-the-model-keyword"></a>강력한 형식의 모델 및 @model 키워드

이 자습서의 앞부분에서 컨트롤러를 전달 하는 방법 데이터 또는 개체를 사용 하 여 뷰 템플릿 본는 `ViewBag` 개체입니다. `ViewBag` 뷰 정보를 전달 하는 편리한 런타임에 바인딩된 방법을 제공 하는 동적 개체입니다.

ASP.NET MVC는 또한 형식화 된 데이터 또는 개체를 뷰 템플릿으로 강력 하 게 전달 하는 기능을 제공 합니다. 이 접근 방식을 사용 하면 컴파일 시간을 개선할 Visual Studio 편집기에서 더 다양 한 IntelliSense 및 코드 검사를 강력한 형식입니다. 이 방법을 사용 하는 Visual Studio에서 스 캐 폴딩 메커니즘을 `MoviesController` 메서드 및 뷰를 만들면 템플릿 클래스 및 보기.

에 *Controllers\MoviesController.cs* 생성 된 파일 검사 `Details` 메서드. 영화 컨트롤러와의 일부를 `Details` 메서드는 다음과 같습니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

경우는 `Movie` 발견 되는 인스턴스의 `Movie` 모델 세부 정보 보기에 전달 됩니다. 콘텐츠를 검사 합니다 *Views\Movies\Details.cshtml* 파일입니다.

포함 하 여를 `@model` 보기 템플릿 파일의 맨 위에 있는 문을 뷰에서 필요로 하는 개체의 형식을 지정할 수 있습니다. 영화 컨트롤러를 만들 때 Visual Studio에서는 *Details.cshtml* 파일의 맨 위에 다음 `@model` 문을 자동으로 포함했습니다.

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

이 `@model` 지시문을 사용하면 강력한 형식인 `Model` 개체를 사용하여 컨트롤러가 뷰에 전달된 영화에 액세스할 수 있습니다. 예를 들어, 합니다 *Details.cshtml* 템플릿 코드는 각 영화 필드를 전달 합니다 `DisplayNameFor` 및 [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 도우미와 강력한 형식의 `Model` 개체. 만들기 및 편집 메서드 및 보기 템플릿은 동영상 모델 개체를 전달할 수도 있습니다.

검사는 *Index.cshtml* 템플릿 보기 및 `Index` 의 메서드를 *MoviesController.cs* 파일입니다. 코드를 만드는 방법을 확인할 수 있습니다는 [ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx) 호출할 때 개체를 `View` 의 도우미 메서드에 `Index` 작업 메서드. 그런 다음이 `Movies` 컨트롤러에서 보기로 목록:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

영화 컨트롤러를 만들 때 다음에 포함 된 자동으로 Visual Studio Express `@model` 맨 위에 있는 문을 합니다 *Index.cshtml* 파일:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

이렇게 `@model` 지시문을 사용 하면 사용 하 여 컨트롤러에서 보기로 전달 하는 영화 목록에 액세스할 수 있습니다는 `Model` 개체는 강력한 형식입니다. 예를 들어 합니다 *Index.cshtml* 수행 하 여 영화를 통해 템플릿 코드를 루프를 `foreach` 는 강력한 형식의 문을 `Model` 개체:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

때문에 `Model` 개체는 강력한 (으로 `IEnumerable<Movie>` 개체), 각 `item` 루프에 있는 개체 형식의 `Movie`합니다. 다른 이점과 함께이 의미는 코드의 컴파일 타임 검사을 얻고 완벽 하 게 코드 편집기에서 IntelliSense 지원 합니다.

![ModelIntellisene](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a>SQL Server LocalDB 사용

제공 된 데이터베이스 연결 문자열을 가리키는 entity Framework Code First 검색을 `Movies` Code First 데이터베이스 자동으로 생성 하므로 아직 존재 하지 않는 데이터베이스입니다. 확인 하 여 생성 된 것을 확인할 수 있습니다 합니다 *앱\_데이터* 폴더입니다. 표시 되지 않는 경우는 *Movies.mdf* 파일을 클릭 합니다 **모든 파일 표시** 단추를 **솔루션 탐색기** 도구 모음에서 클릭는 **새로 고침** 단추를 클릭 한 다음를 확장 합니다 *앱\_데이터* 폴더입니다.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

두 번 클릭 *Movies.mdf* 열려는 **데이터베이스 탐색기**를 차례로 확장 합니다 **테이블** 영화 표를 참조 하는 폴더.

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")

> [!NOTE]
> 데이터베이스 탐색기에 나타나지 않으면에서 **도구** 메뉴에서 **데이터베이스에 연결**를 취소 한 다음를 **데이터 소스 선택** 대화 합니다. 이렇게 하면 강제로 열기 면 데이터베이스 탐색기.


> [!NOTE]
> VWD 또는 Visual Studio 2010을 사용 하 고 다음 중 하나에 유사한 오류가 발생 하는:
> 
> - 데이터베이스 ' C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES 합니다. MDF' 706 버전 이므로 열 수 없습니다. 이 서버 버전 655 및 이전 버전을 지원합니다. 다운 그레이드 경로가 지원 되지 않습니다.
> - &quot;InvalidOperation 예외가 사용자 코드에서 처리 되지 않았습니다.&quot; 제공 된 SqlConnection이 초기 카탈로그를 지정 하지 않습니다.
> 
> 설치 해야 합니다 [SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) 하 고 [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)합니다. 확인 된 `MovieDBContext` 이전 페이지에서 지정 된 연결 문자열입니다.


마우스 오른쪽 단추로 클릭 합니다 `Movies` 선택한 테이블 **테이블 데이터 표시** 만든 데이터를 볼 수 있습니다.

![](accessing-your-models-data-from-a-controller/_static/image8.png)

마우스 오른쪽 단추로 클릭 합니다 `Movies` 선택한 테이블 **테이블 정의 열기** 구조체는 Entity Framework Code First를 생성 하는 테이블을 확인 합니다.

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

알림 방법의 스키마를 `Movies` 테이블에 매핑됩니다는 `Movie` 앞에서 만든 클래스입니다. Entity Framework Code First 자동으로 생성이 스키마에 따라 프로그램 `Movie` 클래스입니다.

완료 되 면, 마우스 오른쪽 단추로 클릭 하 여 연결을 닫습니다 *MovieDBContext* 를 선택 하 고 **연결 닫기**합니다. (연결을 닫으려면 없는 경우 하면 오류가 발생할 수 다음에 프로젝트를 실행할 때).

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

이제 있고 데이터베이스는 단순 목록 페이지에서 콘텐츠를 표시 합니다. 다음 자습서에서에서는 스 캐 폴드 된 코드의 나머지 부분을 검사 하 고 추가 된 `SearchIndex` 메서드 및 `SearchIndex` 영화가이 데이터베이스에 대 한 검색할 수 있는 보기입니다.

> [!div class="step-by-step"]
> [이전](adding-a-model.md)
> [다음](examining-the-edit-methods-and-edit-view.md)
