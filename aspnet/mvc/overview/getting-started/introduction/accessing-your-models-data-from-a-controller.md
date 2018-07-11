---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: 컨트롤러에서 모델의 데이터에 액세스 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: a3f3f4a030650ff65b070528c5efa1605be764a0
ms.sourcegitcommit: b8a2f14bf8dd346d7592977642b610bbcb0b0757
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38120155"
---
<a name="accessing-your-models-data-from-a-controller"></a>컨트롤러에서 모델의 데이터에 액세스
====================
[Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE [Tutorial Note](sample/code-location.md)]

이 섹션에서는 새 만듭니다 `MoviesController` 클래스 및 영화 데이터를 검색 하 고 뷰 템플릿을 사용 하 여 브라우저에 표시 하는 코드를 작성 합니다.

**응용 프로그램을 빌드할** 다음 단계로 진행 하기 전에 합니다. 응용 프로그램을 작성 하지 않아도 오류가 컨트롤러를 추가 합니다.

솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 *컨트롤러* 폴더 및 클릭 한 다음 **추가**, 한 다음 **컨트롤러**합니다.

![](accessing-your-models-data-from-a-controller/_static/image1.png)

에 **스 캐 폴드 추가** 대화 상자, 클릭 **Entity Framework를 사용 하 여 뷰를 사용 하 여 MVC 5 컨트롤러**를 클릭 하 고 **추가**합니다.

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- 선택 **Movie (MvcMovie.Models)** 모델 클래스에 대 한 합니다.
- 선택 **MovieDBContext (MvcMovie.Models)** 데이터 컨텍스트 클래스에 대 한 합니다.
- 컨트롤러 이름을 입력 **MoviesController**합니다.

  아래 이미지에서는 완료 된 대화 상자를 보여 줍니다.  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

**추가**를 클릭합니다. (오류가 발생 하면 아마도 빌드하지 않은 컨트롤러 추가 시작 하기 전에 응용 프로그램입니다.) Visual Studio는 다음 파일 및 폴더를 만듭니다.

- *MoviesController.cs* 파일을 *컨트롤러* 폴더입니다.
- A *Views\Movies* 폴더입니다.
- *Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, 및 *Index.cshtml* 새 *Views\Movies* 폴더입니다.

Visual Studio에서 자동으로 작성 된 [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (만들기, 읽기, 업데이트 및 삭제) 작업 메서드와 뷰 있습니다 (자동으로 만들도록 CRUD 작업 메서드와 뷰 스 캐 폴딩이라고). 이제 모든 기능을 갖춘 웹 응용 프로그램을 만들기, 나열, 편집 및 동영상 항목을 삭제할 수 있습니다.

응용 프로그램을 실행 하 고 클릭 합니다 **MVC 동영상** 링크 (찾아보거나 합니다 `Movies` 추가 하 여 컨트롤러 */Movies* 브라우저의 주소 표시줄에서 URL로). 응용 프로그램은 기본 라우팅을 의존 하기 때문에 (에 정의 된를 *앱\_start\* 파일), 브라우저 요청 `http://localhost:xxxxx/Movies` 기본값으로 라우팅됩니다 `Index` 합니다 의동작메서드`Movies` 컨트롤러입니다. 브라우저 요청 말해 `http://localhost:xxxxx/Movies` 같습니다 효과적으로 브라우저 요청 `http://localhost:xxxxx/Movies/Index`합니다. 결과 빈 목록을 영화, 이므로 아직 추가 하지 않았습니다.

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>영화를 만들기

**새로 만들기** 링크를 선택합니다. 영화에 대 한 일부 정보를 입력 한 다음 클릭 합니다 **만들기** 단추입니다.


![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> Price 필드에서 소수점 또는 쉼표를 입력할 수 있습니다. 쉼표를 사용 하는 영어가 아닌 로캘의 jQuery 유효성 검사를 지원 하도록 (&quot;,&quot;), 소수점 및 미국 영어가 아닌 날짜 형식에 대 한 포함 해야 합니다 *globalize.js* 및 특정  *cultures/globalize.cultures.js* 파일 (에서 [ https://github.com/jquery/globalize ](https://github.com/jquery/globalize) ) 및 JavaScript를 사용 하 여 `Globalize.parseFloat`입니다. 다음 자습서에서이 작업을 수행 하는 방법을 살펴보겠습니다. 이제 10 같은 정수를 입력하면 됩니다.


클릭 하는 **만들기** 단추 하면 폼이 데이터베이스에서 동영상 정보가 저장 된 서버에 게시할 수 있습니다. 다음으로 리디렉션됩니다 합니다 */Movies* URL을 목록에서 새로 만든된 동영상을 볼 수 있습니다.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

나머지 몇 개의 동영상 항목을 만듭니다. 모두 작동하는 **편집**, **세부 정보** 및 **삭제** 링크를 사용해 봅니다.

## <a name="examining-the-generated-code"></a>생성된 된 코드 검사

엽니다는 *Controllers\MoviesController.cs* 파일을 생성 된 검사 `Index` 메서드. 영화 컨트롤러와의 일부를 `Index` 메서드는 다음과 같습니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

요청을를 `Movies` 컨트롤러의 모든 항목을 반환 합니다 `Movies` 테이블 및 결과를 전달 합니다는 `Index` 보기. 다음 줄을 `MoviesController` 앞에서 설명한 대로 클래스는 영화 데이터베이스 컨텍스트를 인스턴스화합니다. 쿼리, 편집 및 삭제 영화에 영화 데이터베이스 컨텍스트를 사용할 수 있습니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>강력한 형식의 모델 및 @model 키워드

이 자습서의 앞부분에서 컨트롤러를 전달 하는 방법 데이터 또는 개체를 사용 하 여 뷰 템플릿 본는 `ViewBag` 개체입니다. `ViewBag` 뷰 정보를 전달 하는 편리한 런타임에 바인딩된 방법을 제공 하는 동적 개체입니다.

MVC를 전달 하는 기능도 제공 *강력한* 보기 템플릿에 개체를 입력 합니다. 이 강력한 형식의 방법을 더 나은 컴파일 타임 풍부 하 고 코드 검사를 사용 하면 [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) Visual Studio 편집기에서. 이 방법을 사용 하는 Visual Studio에서 스 캐 폴딩 메커니즘 (즉, 전달를 *강력한* 형식화 된 모델) 사용 하 여는 `MoviesController` 메서드 및 뷰를 만들면 템플릿 클래스 및 보기.

에 *Controllers\MoviesController.cs* 생성 된 파일 검사 `Details` 메서드. `Details` 메서드는 다음과 같습니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

`id` 매개 변수는 경로 데이터 변수로 예를 들어 전달 일반적으로 `http://localhost:1234/movies/details/1` 영화 컨트롤러에 동작을 컨트롤러 설정이 `details` 및 `id` 1입니다. 또한 다음과 전달할 수 있습니다 일괄 처리 id는 쿼리 문자열을 사용 하 여 다음과 같이

`http://localhost:1234/movies/details?id=1`

경우는 `Movie` 발견 되는 인스턴스의 합니다 `Movie` 모델에 전달 되는 `Details` 보기:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

콘텐츠를 검사 합니다 *Views\Movies\Details.cshtml* 파일:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

포함 하 여를 `@model` 보기 템플릿 파일의 맨 위에 있는 문을 뷰에서 필요로 하는 개체의 형식을 지정할 수 있습니다. 영화 컨트롤러를 만들 때 Visual Studio에서는 *Details.cshtml* 파일의 맨 위에 다음 `@model` 문을 자동으로 포함했습니다.

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

이 `@model` 지시문을 사용하면 강력한 형식인 `Model` 개체를 사용하여 컨트롤러가 뷰에 전달된 영화에 액세스할 수 있습니다. 예를 들어, 합니다 *Details.cshtml* 템플릿 코드는 각 영화 필드를 전달 합니다 `DisplayNameFor` 및 [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 도우미와 강력한 형식의 `Model` 개체. 합니다 `Create` 및 `Edit` 메서드 및 보기 템플릿은 동영상 모델 개체를 전달할 수도 있습니다.

검사는 *Index.cshtml* 템플릿 보기 및 `Index` 의 메서드를 *MoviesController.cs* 파일입니다. 코드를 만드는 방법을 확인할 수 있습니다는 [ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx) 호출할 때 개체를 `View` 의 도우미 메서드에 `Index` 작업 메서드. 그런 다음이 `Movies` 에서 나열 된 `Index` 보기로 작업 메서드:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

다음에 Visual Studio 영화 컨트롤러를 만들 때 자동으로 포함 `@model` 맨 위에 있는 문을 합니다 *Index.cshtml* 파일:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

이렇게 `@model` 지시문을 사용 하면 사용 하 여 컨트롤러에서 보기로 전달 하는 영화 목록에 액세스할 수 있습니다는 `Model` 개체는 강력한 형식입니다. 예를 들어 합니다 *Index.cshtml* 수행 하 여 영화를 통해 템플릿 코드를 루프를 `foreach` 는 강력한 형식의 문을 `Model` 개체:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

때문에 `Model` 개체는 강력한 (으로 `IEnumerable<Movie>` 개체), 각 `item` 루프에 있는 개체 형식의 `Movie`합니다. 다른 이점과 함께이 의미는 코드의 컴파일 타임 검사을 얻고 완벽 하 게 코드 편집기에서 IntelliSense 지원 합니다.

![ModelIntellisene](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>SQL Server LocalDB 사용

제공 된 데이터베이스 연결 문자열을 가리키는 entity Framework Code First 검색을 `Movies` Code First 데이터베이스 자동으로 생성 하므로 아직 존재 하지 않는 데이터베이스입니다. 확인 하 여 생성 된 것을 확인할 수 있습니다 합니다 *앱\_데이터* 폴더입니다. 표시 되지 않는 경우는 *Movies.mdf* 파일을 클릭 합니다 **모든 파일 표시** 단추를 **솔루션 탐색기** 도구 모음에서 클릭는 **새로 고침** 단추를 클릭 한 다음를 확장 합니다 *앱\_데이터* 폴더입니다.

![](accessing-your-models-data-from-a-controller/_static/image9.png)

두 번 클릭 *Movies.mdf* 열려는 **서버 탐색기**를 차례로 확장 합니다 **테이블** 영화 표를 참조 하는 폴더. Note id입니다. 옆에 있는 키 아이콘 기본적으로 EF는 기본 키 ID 라는 속성을 확인 합니다. EF 및 MVC에 대 한 자세한 내용은 Tom Dykstra 훌륭한 자습서를 참조 하세요 [MVC 및 EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

마우스 오른쪽 단추로 클릭 합니다 `Movies` 선택한 테이블 **테이블 데이터 표시** 만든 데이터를 볼 수 있습니다.

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

마우스 오른쪽 단추로 클릭 합니다 `Movies` 선택한 테이블 **테이블 정의 열기** 구조체는 Entity Framework Code First를 생성 하는 테이블을 확인 합니다.

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

알림 방법의 스키마를 `Movies` 테이블에 매핑됩니다는 `Movie` 앞에서 만든 클래스입니다. Entity Framework Code First 자동으로 생성이 스키마에 따라 프로그램 `Movie` 클래스입니다.

완료 되 면, 마우스 오른쪽 단추로 클릭 하 여 연결을 닫습니다 *MovieDBContext* 를 선택 하 고 **연결 닫기**합니다. (연결을 닫으려면 없는 경우 하면 오류가 발생할 수 다음에 프로젝트를 실행할 때).

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

이제 데이터를 표시, 편집, 업데이트 및 삭제할 데이터베이스 및 페이지가 제공됩니다. 다음 자습서에서에서는 스 캐 폴드 된 코드의 나머지 부분을 검사 하 고 추가 된 `SearchIndex` 메서드 및 `SearchIndex` 영화가이 데이터베이스에 대 한 검색할 수 있는 보기입니다. MVC와 함께 Entity Framework를 사용 하는 방법은 참조 하세요 [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.

> [!div class="step-by-step"]
> [이전](creating-a-connection-string.md)
> [다음](examining-the-edit-methods-and-edit-view.md)
