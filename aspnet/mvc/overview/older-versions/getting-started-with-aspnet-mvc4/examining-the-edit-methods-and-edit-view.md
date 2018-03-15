---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
title: "편집 메서드 및 편집 보기 검사 | Microsoft Docs"
author: Rick-Anderson
description: "참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 진행할 데모를 단순..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 41eb99ca-e88f-4720-ae6d-49a958da8116
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 315914056c0a666fdf23cf82a314a999e03114b6
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
<a name="examining-the-edit-methods-and-edit-view"></a>편집 메서드 및 편집 보기 검사
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다. 더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.


이 섹션에서는 생성 된 작업 메서드 및 동영상 컨트롤러에 대 한 뷰를 검토 합니다. 그런 다음 사용자 지정 검색 페이지를 추가 합니다.

응용 프로그램을 실행 하 고를 찾습니다는 `Movies` 컨트롤러를 추가 하 여 */Movies* 브라우저의 주소 표시줄에 URL을 합니다. 위에 마우스 포인터는 **편집** 를 연결 하는 URL을 보려면이 링크를 합니다.

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

**편집** 에 의해 생성 된 링크는 `Html.ActionLink` 에서 메서드는 *Views\Movies\Index.cshtml* 보기:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

![Html.ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html` 개체에서 속성을 사용 하 여 노출 되는 도우미는는 [System.Web.Mvc.WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx) 기본 클래스입니다. `ActionLink` 도우미의 메서드를 사용 하면 쉽게를 동적으로 컨트롤러 작업 메서드에 연결 되는 하이퍼링크는 HTML을 생성 합니다. 첫 번째 인수는 `ActionLink` 메서드를 렌더링 하는 링크 텍스트는 (예를 들어 `<a>Edit Me</a>`). 두 번째 인수는 호출할 동작 메서드의 이름입니다. 마지막 인수는는 [익명 개체](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) (이 경우 ID가 4)에서 경로 데이터를 생성 하 합니다.

이전 그림에 표시 된 생성 된 링크는 `http://localhost:xxxxx/Movies/Edit/4`합니다. 기본 경로 (에 설정 된 *앱\_Start\RouteConfig.cs*) URL 패턴은 `{controller}/{action}/{id}`합니다. 따라서 ASP.NET 변환 `http://localhost:xxxxx/Movies/Edit/4` 하는 요청에는 `Edit` 의 동작 메서드는 `Movies` 매개 변수와 함께 컨트롤러 `ID` 4와 같습니다. 다음 코드를 검사 하는 *앱\_Start\RouteConfig.cs* 파일입니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

쿼리 문자열을 사용 하 여 동작 메서드 매개 변수를 전달할 수 있습니다. 예를 들어 URL `http://localhost:xxxxx/Movies/Edit?ID=4` 매개 변수 전달 `ID` 개로 이루어진는 `Edit` 의 동작 메서드는 `Movies` 컨트롤러입니다.

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

열기는 `Movies` 컨트롤러입니다. 두 `Edit` 작업 메서드는 다음과 같습니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cs)]

두 번째 `Edit` 작업 메서드는 `HttpPost` 특성 뒤에 옵니다. 이 특성의 오버 로드 하는 지정 된 `Edit` POST 요청에 대 한 메서드를 호출할 수 있습니다. 적용할 수는 `HttpGet` 첫 번째 특성 편집 메서드를 사용할 수 있지만 필요한 기본값 이기 때문에 있습니다. (암시적으로 할당 된 작업 메서드를 지칭는 `HttpGet` 특성은 `HttpGet` 메서드.)

`HttpGet` `Edit` 메서드 영화 ID 매개 변수를 조회 하는 Entity Framework를 사용 하 여 동영상 `Find` 메서드를 선택한 동영상 편집 뷰를 반환 합니다. ID 매개 변수 지정는 [기본값](https://msdn.microsoft.com/library/dd264739.aspx) 경우 0의 `Edit` 매개 변수 없이 메서드를 호출 합니다. 동영상을 찾을 수 없는 경우 [HttpNotFound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) 반환 됩니다. 편집 보기에서 스캐폴딩 시스템이 만들어질 때 `Movie` 클래스를 조사하고 클래스의 각 속성에 대해 `<label>` 및 `<input>` 요소를 렌더링하기 위한 코드를 만들었습니다. 다음 예제에서는 생성 된 편집 뷰를 보여 줍니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cshtml)]

템플릿 보기에는 어떻게는 `@model MvcMovie.Models.Movie` 문을 파일의 맨-이 여부를 지정 된 보기 형식으로 템플릿 보기에 대 한 모델 `Movie`합니다.

스 캐 폴드 코드가 사용 하는 여러 *도우미 메서드* HTML 태그를 간소화할 수 있습니다. [ `Html.LabelFor` ](https://msdn.microsoft.com/library/gg401864(VS.98).aspx) 필드의 이름을 표시 하는 도우미 (&quot;제목&quot;, &quot;ReleaseDate&quot;, &quot;장르&quot;, 또는 &quot;가격 &quot;). [ `Html.EditorFor` ](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) 도우미는 HTML 렌더링 `<input>` 요소입니다. [ `Html.ValidationMessageFor` ](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) 도우미 해당 속성과 관련 된 유효성 검사 메시지를 표시 합니다.

응용 프로그램을 실행 하 고 탐색 하 고 */Movies* URL입니다. **편집** 링크를 클릭합니다. 브라우저에서 페이지에 대한 소스를 봅니다. HTML 폼 요소에는 다음과 같습니다.

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample5.html?highlight=7,10-11)]

`<input>` html에서 요소는 `<form>` 요소 인 `action` 특성에 게시 하도록 설정 되어는 */영화/편집* URL입니다. 양식 데이터 서버에 게시 될 때는 **편집** 단추를 클릭 합니다.

## <a name="processing-the-post-request"></a>POST 요청 처리

다음 목록은 `Edit` 작업 메서드의 `HttpPost` 버전을 보여 줍니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

[ASP.NET MVC 모델 바인더](https://msdn.microsoft.com/magazine/hh781022.aspx) 에서는 게시 된 양식 값을 사용 하 고 만듭니다는 `Movie` 변수로 전달 되는 개체는 `movie` 매개 변수입니다. `ModelState.IsValid` 메서드는 양식에서 제출된 데이터가 `Movie` 개체를 수정하는 데(편집 또는 업데이트) 사용될 수 있음을 확인합니다. 데이터가 올바른지, 동영상 데이터에 저장 됩니다는 `Movies` 의 컬렉션은 `db(MovieDBContext` 인스턴스). 새 동영상 데이터를 호출 하 여 데이터베이스에 저장 되는 `SaveChanges` 방식의 `MovieDBContext`합니다. 데이터를 저장 한 후 코드에 사용자를 리디렉션하는 `Index` 의 동작 메서드는 `MoviesController` 클래스를 표시 하 고 방금 변경한을 포함 하 여 동영상 컬렉션의 합니다.

게시 된 값에 유효 하지 않습니다, 이러한 형태로 다시 표시 됩니다. `Html.ValidationMessageFor` 에서 도우미는 *Edit.cshtml* 보기 서식 파일을 적절 한 오류 메시지 표시 처리 합니다.

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

> [!NOTE]
> 쉼표를 사용 하는 영어가 아닌 로캘의 jQuery 유효성 검사를 지원 하기 위해 (&quot;,&quot;) 소수점을 포함 해야 *globalize.js* 및 특정 *cultures/globalize.cultures.js* 파일 (에서 [ https://github.com/jquery/globalize ](https://github.com/jquery/globalize) ) 및 사용 하는 JavaScript `Globalize.parseFloat`합니다. 다음 코드와 작업할 Views\Movies\Edit.cshtml 파일을 수정 된 &quot;FR-FR&quot; 문화권:


[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

10 진수 필드에는 쉼표를 소수점 하지 필요할 수 있습니다. 임시 수정과 프로젝트 루트 web.config 파일에 세계화 요소를 추가할 수 있습니다. 다음 코드는 문화권을 영어 (미국)로 설정 된 세계화 요소를 보여 줍니다.

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.xml)]

모든는 `HttpGet` 메서드는 유사한 패턴을 따릅니다. 영화 개체를 가져옵니다 (또는 개체의 경우에서 목록이 `Index`), 보기에는 모델을 전달 합니다. `Create` 메서드 만들기 뷰 빈 영화 개체를 전달 합니다. 생성, 편집, 삭제 또는 어떤 식으로든 데이터를 수정하는 모든 메서드는 메서드의 `HttpPost` 오버로드에서 해당 작업을 수행합니다. 블로그 게시물에에서 설명 된 대로 보안 위험 요소는 HTTP GET 메서드에서 데이터 수정 [ASP.NET MVC 팁 #46-보안 허점을 만들기 때문에 삭제 링크를 사용 하지 않는](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)합니다. HTTP에 대 한 유용한 정보 및 아키텍처는 또한 위반 GET 메서드가의 데이터 수정 [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) 패턴 지정 한 GET 요청을 응용 프로그램의 상태를 변경 하지 않아야 합니다. 다시 말해 GET 작업 수행은 부작용 없이 안전하고 영속 데이터를 수정하지 않는 방법으로 이루어져야 합니다.

## <a name="adding-a-search-method-and-search-view"></a>검색 방법 및 검색 뷰를 추가합니다.

이 섹션에서는 추가 `SearchIndex` 작업 메서드를 사용 하면 영화 장르 또는 이름으로 검색 합니다. 사용 하 여 사용할 수 있는 됩니다는 */영화/SearchIndex* URL입니다. 요청은 사용자가 영화를 검색 하기 위해 입력할 수 있는 입력된 요소가 포함 된 HTML 폼에 표시 됩니다. 사용자가 폼을 제출, 작업 메서드는 사용자가 게시 된 검색 값 가져오고 데이터베이스를 검색 하려면 값을 사용 합니다.

## <a name="displaying-the-searchindex-form"></a>SearchIndex 폼을 표시

추가 하 여 시작 된 `SearchIndex` 동작 메서드를 기존 `MoviesController` 클래스입니다. 메서드는 HTML 폼을 포함 하는 뷰를 반환 합니다. 코드는 다음과 같습니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

첫 번째 줄은 `SearchIndex` 메서드 다음 항목을 만듭니다 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 쿼리는 영화를 선택 하려면:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cs)]

쿼리가 시점에서 정의 되었지만 아직 데이터 저장소에 대해 실행 되지 않았습니다.

경우는 `searchString` 매개 변수는 문자열이 포함 된, 다음 코드를 사용 하 여 검색 문자열을 값으로 필터링 하려면 영화 쿼리가 수정 됩니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample11.cs)]

위의 `s => s.Title` 코드는 [람다 식](https://msdn.microsoft.com/library/bb397687.aspx)입니다. 람다 식은 메서드 기반에 사용 되 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 와 같은 표준 쿼리 연산자 메서드의 인수로 쿼리는 [여기서](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) 위의 코드에서 사용 하는 방법입니다. 정의 된 또는 같은 메서드를 호출 하 여 수정 된 경우에 LINQ 쿼리 실행 되지 않습니다 `Where` 또는 `OrderBy`합니다. 대신, 쿼리 실행이 지연, 즉, 실제로 실현된 값 반복 될 때까지 식의 계산이 지연 되는지 또는 [ `ToList` ](https://msdn.microsoft.com/library/bb342261.aspx) 메서드를 호출 합니다. 에 `SearchIndex` 샘플 SearchIndex 보기에서 쿼리가 실행 됩니다. 지연된 쿼리 실행에 대한 자세한 내용은 [쿼리 실행](https://msdn.microsoft.com/library/bb738633.aspx)을 참조하세요.

이제 구현할 수는 `SearchIndex` 보기를 사용자에 게 폼을 표시 합니다. 마우스 오른쪽 단추로 클릭는 `SearchIndex` 메서드와 클릭 **뷰 추가**합니다. 에 **뷰 추가** 대화 상자를 전달 하려는 지정는 `Movie` 개체 모델 클래스와 템플릿 보기입니다. 에 **스 캐 폴드 템플릿이** 목록에서 선택 **목록**, 클릭 **추가**합니다.

![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image5.png)

클릭할 때는 **추가** 단추를는 *Views\Movies\SearchIndex.cshtml* 템플릿 보기 생성 됩니다. 선택 했기 때문에 **목록** 에 **스 캐 폴드 템플릿이** 목록에서 자동으로 생성 하는 Visual Studio (스 캐 폴드) 보기에서 일부 기본 태그입니다. 스 캐 폴딩을 HTML 폼을 생성 합니다. 코드 검토는 `Movie` 클래스 및 생성된 된 렌더링 하는 코드 `<label>` 클래스의 각 속성에 대 한 요소입니다. 아래 목록에서는 생성 된 뷰를 만들기를 보여 줍니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cshtml)]

응용 프로그램을 실행 하 고 이동 */영화/SearchIndex*합니다. 쿼리 문자열(예: `?searchString=ghost`)을 URL에 추가합니다. 필터링된 동영상이 표시됩니다.

![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image6.png)

시그니처를 변경 하는 경우는 `SearchIndex` 메서드 라는 매개 변수를 사용 하려면 `id`, `id` 매개 변수는 일치는 `{id}` 기본값에 대 한 자리 표시자 경로 집합에는 *Global.asax* 파일입니다.

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample13.json)]

원래 `SearchIndex` 메서드는 다음과 같습니다::

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cs)]

수정 된 `SearchIndex` 메서드를 보여 줍니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cs?highlight=1,3)]

이제 쿼리 문자열 값이 아닌 경로 데이터(URL 세그먼트)로 검색 제목을 전달할 수 있습니다.

![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image7.png)

그러나 사용자가 영화를 검색하려고 할 때마다 URL을 수정하지는 않습니다. 수 있도록 UI를 추가 합니다 있습니다 지금 동영상을 필터링 합니다. 시그니처를 변경 하는 경우는 `SearchIndex` 경로 바인딩된 ID 매개 변수를 전달 하는 방법을 테스트 하는 메서드 변경 다시 있도록 프로그램 `SearchIndex` 메서드 라는 문자열 매개 변수 `searchString`:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

열기는 *Views\Movies\SearchIndex.cshtml* 파일을 찾아 바로 뒤에 `@Html.ActionLink("Create New", "Create")`, 다음 코드를 추가 합니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml?highlight=2)]

다음 예제에서는 일부는 *Views\Movies\SearchIndex.cshtml* 파일을 추가 된 태그를 필터링 합니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cshtml?highlight=12-15)]

`Html.BeginForm` 도우미 만듭니다 여 `<form>` 태그입니다. `Html.BeginForm` 도우미 하면 사용자가 클릭 하 여 폼을 제출 하는 경우 자신에 게 게시 하려면 폼의 **필터** 단추입니다.

응용 프로그램을 실행 하 고 동영상에 대 한 검색을 시도 합니다.

![](examining-the-edit-methods-and-edit-view/_static/image8.png)

없는 `HttpPost` 오버 로드는 `SearchIndex` 메서드. 필요 없는, 메서드는 응용 프로그램의 상태를 변경 되지 않습니다 때문에 데이터를 필터링 합니다.

다음 `HttpPost SearchIndex` 메서드를 추가할 수 있습니다. 작업 호출자는 일치 하는 경우에 `HttpPost SearchIndex` 메서드, 및 `HttpPost SearchIndex` 메서드 아래 이미지에 나와 있는 것 처럼 실행 됩니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image9.png)

그러나 이 `HttpPost` 버전의 `SearchIndex` 메서드를 추가하는 경우에도 이를 모두 구현하는 방법은 제한됩니다. 특정 검색을 책갈피로 설정하거나 동일하게 필터링된 영화 목록을 보기 위해 클릭할 수 있는 링크를 친구에게 보내려고 한다고 가정합니다. HTTP POST에 대 한 URL를 요청 하는 GET 요청 (localhost:xxxxx/영화/SearchIndex)에 대 한 URL과 동일한-URL 자체에 검색 정보가 없습니다. 오른쪽 지금 검색 문자열 정보는 전송 서버에 양식 필드 값으로. 즉, 책갈피를 URL에는 친구에 게 보내고 해당 검색 정보를 캡처할 수 없습니다.

솔루션의 오버 로드를 사용 하는 것 `BeginForm` 에 POST 요청 URL에 검색 정보를 추가 하도록 및의 HttpGet 버전으로 라우팅할 수를 지정 하는 `SearchIndex` 메서드. 매개 변수가 없는 기존 항목 바꾸기 `BeginForm` 메서드를 다음:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cshtml)]

![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image10.png)

이제 검색을 제출할 때 URL 검색 쿼리 문자열을 포함 합니다. `HttpPost SearchIndex` 메서드가 있는 경우에도 검색은 `HttpGet SearchIndex` 작업 메서드로 이동합니다.

![SearchIndexWithGetURL](examining-the-edit-methods-and-edit-view/_static/image11.png)

## <a name="adding-search-by-genre"></a>장르별로 검색 추가

추가한 경우는 `HttpPost` 버전의는 `SearchIndex` 메서드를 지금 삭제 합니다.

다음으로, 사용자가 영화가 장르별로 검색할 수 있도록 하는 기능을 추가 합니다. `SearchIndex` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cs)]

이 버전의는 `SearchIndex` 메서드는 추가 매개 변수, 즉 `movieGenre`합니다. 코드의 처음 몇 줄 만들기는 `List` 데이터베이스에서 영화 장르를 보유 하는 개체입니다.

다음 코드는 데이터베이스에서 모든 장르를 검색하는 LINQ 쿼리입니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample22.cs)]

코드를 사용 하 여는 `AddRange` 메서드는 제네릭의 `List` 모든 고유 장르 목록에 추가할 컬렉션입니다. (없이 `Distinct` 한정자를 중복 장르는 추가-샘플에 두 번 코미디는 추가 하는 예를 들어). 코드에는 다음에 장르 목록을 저장 된 `ViewBag` 개체입니다.

다음 코드를 확인 하는 방법을 보여 줍니다는 `movieGenre` 매개 변수입니다. 비어 있지 않으면 코드를 추가로 지정된 장르에 선택 된 동영상을 제한 하려면 영화 쿼리를 제한 합니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample23.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>장르별로 검색을 지 원하는 SearchIndex 보기에 태그 추가

추가 `Html.DropDownList` 도우미에는 *Views\Movies\SearchIndex.cshtml* 파일, 바로 앞의 `TextBox` 도우미입니다. 완성 된 태그는 다음과 같습니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample24.cshtml?highlight=4)]

응용 프로그램을 실행 하 고 찾아보기 */영화/SearchIndex*합니다. 장르, 영화 제목 및 두 조건으로 검색을 시도 하십시오.

![](examining-the-edit-methods-and-edit-view/_static/image12.png)

이 섹션의 CRUD 작업 메서드 및 프레임 워크에 의해 생성 된 뷰를 검사 합니다. 검색 작업 메서드와 뷰 사용자가 영화 제목 및 장르 하 여 검색할 수 있도록 만들었습니다. 다음 섹션에서 살펴보겠습니다 속성을 추가 하는 방법의 `Movie` 모델 및 테스트 데이터베이스에서 자동으로 만듭니다는 이니셜라이저를 추가 하는 방법입니다.

>[!div class="step-by-step"]
[이전](accessing-your-models-data-from-a-controller.md)
[다음](adding-a-new-field-to-the-movie-model-and-table.md)
