---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
title: "컨트롤러 (VB)에서 모델의 데이터에 액세스 | Microsoft Docs"
author: Rick-Anderson
description: "이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: cad00de1-3c68-4ff4-a436-54236d449459
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: d0c6976519f4f4bae10fabf4cbf85401de4f58e7
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="accessing-your-models-data-from-a-controller-vb"></a>컨트롤러 (VB)에서 모델의 데이터에 액세스
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다. 다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> 이 항목에 수반 VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù. [VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. 원하는 경우 C#으로 전환 된 [C# 버전](../cs/accessing-your-models-data-from-a-controller.md) 이 자습서의 합니다.


이 섹션에서는 새 만들어 `MoviesController` 클래스 및 동영상 데이터를 검색 하 고 뷰 템플릿을 사용 하 여 브라우저에 표시 하는 코드를 작성 합니다. 계속 하기 전에 응용 프로그램을 작성 해야 합니다.

마우스 오른쪽 단추로 클릭는 *컨트롤러* 폴더를 만들고 새 `MoviesController` 컨트롤러입니다. 다음 옵션을 선택 합니다.

- 컨트롤러 이름: **MoviesController**합니다. (기본값입니다.)
- 서식 파일: **Entity Framework를 사용 하 여 읽기/쓰기 동작 및 뷰를 사용 하 여 컨트롤러**합니다.
- 모델 클래스: **동영상 (MvcMovie.Models)**합니다.
- 데이터 컨텍스트 클래스: **MovieDBContext (MvcMovie.Models)**합니다.
- 보기: **Razor (CSHTML)**합니다. (기본값입니다.)

[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)

**추가**를 클릭합니다. Visual Web Developer는 다음과 같은 파일 및 폴더를 만듭니다.

- *MoviesController.vb* 프로젝트의 파일 *컨트롤러* 폴더입니다.
- A *동영상* 프로젝트의 폴더 *뷰* 폴더입니다.
- *Create.vbhtml, Delete.vbhtml, Details.vbhtml, Edit.vbhtml*, 및 *Index.vbhtml* 새 *Views\Movies* 폴더입니다.

[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)

ASP.NET MVC 3 스 캐 폴딩 메커니즘 자동으로 생성 됩니다는 CRUD (만들기, 읽기, 업데이트 및 삭제) 작업 메서드 및 보기에 있습니다. 만들기, 목록, 편집 및 동영상 항목을 삭제할 수 있는 완벽 하 게 작동 하는 웹 응용 프로그램을 해야 합니다.

응용 프로그램을 실행 하 고를 찾습니다는 `Movies` 컨트롤러를 추가 하 여 */Movies* 브라우저의 주소 표시줄에 URL을 합니다. 응용 프로그램은 기본 라우팅에 의존 하므로 때문에 (에 정의 된는 *Global.asax* 파일), 브라우저 요청 `http://localhost:xxxxx/Movies` 기본값에 라우팅 된다고 `Index` 의 동작 메서드는 `Movies` 컨트롤러입니다. 즉, 브라우저 요청 `http://localhost:xxxxx/Movies` 브라우저 요청 동일은 사실상 `http://localhost:xxxxx/Movies/Index`합니다. 결과 아직 추가 하지 때문에 빈 목록 영화,입니다.

![](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="creating-a-movie"></a>동영상 만들기

**새로 만들기** 링크를 선택합니다. 동영상에 대 한 일부 세부 정보를 입력 한 다음 클릭는 **만들기** 단추입니다.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

클릭 하 고 **만들기** 단추를 클릭 하면 데이터베이스에 동영상 정보 저장 되는 서버에 게시 될 폼입니다. 다음 리디렉션됩니다 하는 */Movies* URL을 목록에서 새로 만든된 동영상을 볼 수 있습니다.

[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)

나머지 몇 개의 동영상 항목을 만듭니다. 모두 작동하는 **편집**, **세부 정보** 및 **삭제** 링크를 사용해 봅니다.

## <a name="examining-the-generated-code"></a>생성된 된 코드 검사

열기는 *Controllers\MoviesController.vb* 파일을 생성 된 검사 `Index` 메서드. 영화 컨트롤러와의 일부는 `Index` 메서드는 다음과 같습니다.

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample1.vb)]

다음 줄은 `MoviesController` 앞에서 설명한 대로 클래스는 영화 데이터베이스 컨텍스트를 인스턴스화합니다. 쿼리, 편집 및 삭제 영화를 영화 데이터베이스 컨텍스트를 사용할 수 있습니다.

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample2.vb)]

요청을는 `Movies` 컨트롤러의 모든 항목이 반환는 `Movies` 영화 데이터베이스 테이블의 다음 결과를 전달는 `Index` 보기.

## <a name="strongly-typed-models-and-the-model-keyword"></a>강력한 형식 모델 및 @model 키워드

이 자습서의 앞부분에서 언급 했 듯이 어떻게 컨트롤러를 전달할 수 데이터 나 개체를 사용 하 여 뷰 서식 파일은 `ViewBag` 개체입니다. `ViewBag` 정보 보기를 전달 하는 편리한 런타임에 바인딩된 방법을 제공 하는 동적 개체입니다.

또한 ASP.NET MVC는 강력 하 게 전달 하는 기능 입력 한 데이터 또는 개체 템플릿 보기를 제공 합니다. 이 접근 방식을 사용 하면 더 나은 컴파일 타임 검사 코드 및 Visual Web Developer 편집기에서 다양 한 IntelliSense의 강력한 형식입니다. 이 방법을 사용 하 여는 `MoviesController` 클래스 및 *Index.vbhtml* 템플릿 보기.

코드 만드는 방법을 확인할 수는 [ `List` ](https://msdn.microsoft.com/en-us/library/6sh2ey19.aspx) 호출 되 면 개체는 `View` 의 도우미 메서드는 `Index` 동작 메서드. 그런 다음이 `Movies` 보기에는 컨트롤러에서 목록:

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample3.vb)]

포함 하 여 한 `@ModelType` 문을 보기 템플릿 파일 맨 위에 있는 보기를 필요로 하는 개체의 유형을 지정할 수 있습니다. 다음에 Visual Web Developer 영화 컨트롤러를 만들 때 자동으로 포함 `@model` 맨 위에 있는 문에 *Index.vbhtml* 파일:

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.vbhtml)]

이 `@ModelType` 지시문을 사용 하면 컨트롤러 사용 하 여 보기에 전달 되는 동영상 목록을 액세스할 수 있습니다는 `Model` 강력한 형식 개체입니다. 예를 들어는 *Index.vbhtml* 서식 파일을 코드 반복 동영상 수행 하 여 한 `foreach` 문을 통해 강력한 형식의 `Model` 개체:

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.vbhtml)]

때문에 `Model` 개체는 강력한 형식 (으로 `IEnumerable<Movie>` 개체), 각 `item` 루프에서 개체도 입력 된 `Movie`합니다. 여러 가지 이점을 얻을이 의미 가져오기 코드의 컴파일 타임 검사 하 고 완벽 하 게 코드 편집기에서 IntelliSense 지원 합니다.

[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)

## <a name="working-with-sql-server-compact"></a>SQL Server Compact 작업

제공 된 데이터베이스 연결 문자열이 가리키는 entity Framework Code First 감지는 `Movies` 데이터베이스 코드 첫 번째 데이터베이스 자동으로 생성 하므로 아직 존재 하지 않습니다. 검색 하 여 생성 되어 있는지 확인할 수 있습니다는 *앱\_데이터* 폴더입니다. 표시 되지 않으면는 *Movies.sdf* 파일을 클릭는 **모든 파일 표시** 단추는 **솔루션 탐색기** 도구 모음에서 클릭 된 **새로 고침** 단추를 선택한 다음 확장은 *앱\_데이터* 폴더입니다.

[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)

두 번 클릭 *Movies.sdf* 열려는 **서버 탐색기**합니다. 다음 확장은 **테이블** 데이터베이스에서 생성 된 테이블을 표시 하는 폴더입니다.

> [!NOTE]
> 두 번 클릭 하면 오류가 발생 하는 경우 *Movies.sdf*, 이전에 설치한 해야 **SQL Server Compact 4.0 용 Visual Studio 2010 SP1 도구**합니다. (소프트웨어에 대 한 링크,이 자습서 시리즈의 일부 1에서에서 필수 구성 요소 목록 참조). 릴리스를 설치한 경우 해야 닫고 Visual Web Developer를 다시 여세요.


[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)

에 대해 하나씩, 두 개의 테이블이 `Movie` 엔터티 집합 다음의 `EdmMetadata` 테이블입니다. `EdmMetadata` 테이블 모델과 데이터베이스는 동기화 시기를 결정 하는 Entity Framework에서 사용 됩니다.

마우스 오른쪽 단추로 클릭는 `Movies` 테이블을 선택한 **테이블 데이터 표시** 만든 데이터를 볼 수 있습니다.

[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)

마우스 오른쪽 단추로 클릭는 `Movies` 테이블을 선택한 **테이블 스키마 편집**합니다.

[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)

![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image19.png)

알림 방법을의 스키마는 `Movies` 테이블에 매핑되는 `Movie` 앞에서 만든 클래스. Entity Framework Code First 자동으로이 스키마에 대해 만들어진에 따라 프로그램 `Movie` 클래스입니다.

완료 된 경우 연결을 닫습니다. (연결을 닫은 하지 않는 경우 오류가 발생할 수 있습니다는 다음에 프로젝트를 실행할 때).

[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)

이제는 데이터베이스와 여기에서 콘텐츠를 표시 하는 간단한 목록 페이지 만들어졌습니다. 다음 자습서에서는 합니다 스 캐 폴드 코드의 나머지 부분을 검사 하 고 추가 `SearchIndex` 메서드 및 `SearchIndex` 보기를이 데이터베이스에서 영화를 검색할 수 있습니다.

>[!div class="step-by-step"]
[이전](adding-a-model.md)
[다음](examining-the-edit-methods-and-edit-view.md)
