---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/examining-the-edit-methods-and-edit-view
title: 편집 메서드 및 편집 보기 (C#) 검사 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 1d266bf0-a61e-423b-a3d2-13773d7dafe2
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 581138bb25b95ef9002a2bd97d1fa28797d96bfa
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="examining-the-edit-methods-and-edit-view-c"></a>편집 메서드 및 편집 보기 (C#) 검사
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다. 더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.
> 
> 
> 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다. 다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> 이 항목에 수반 C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù. [C# 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. Visual Basic을 선호 하는 경우 전환의 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.


이 섹션에서는 생성 된 작업 메서드 및 동영상 컨트롤러에 대 한 뷰를 검토 합니다. 그런 다음 사용자 지정 검색 페이지를 추가 합니다.

응용 프로그램을 실행 하 고를 찾습니다는 `Movies` 컨트롤러를 추가 하 여 */Movies* 브라우저의 주소 표시줄에 URL을 합니다. 위에 마우스 포인터는 **편집** 를 연결 하는 URL을 보려면이 링크를 합니다.

[![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image2.png)](examining-the-edit-methods-and-edit-view/_static/image1.png)

**편집** 에 의해 생성 된 링크는 `Html.ActionLink` 에서 메서드는 *Views\Movies\Index.cshtml* 보기:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

[![Html.ActionLink](examining-the-edit-methods-and-edit-view/_static/image4.png)](examining-the-edit-methods-and-edit-view/_static/image3.png)

`Html` 개체에서 속성을 사용 하 여 노출 되는 도우미는는 `WebViewPage` 기본 클래스입니다. `ActionLink` 도우미의 메서드를 사용 하면 쉽게를 동적으로 컨트롤러 작업 메서드에 연결 되는 하이퍼링크는 HTML을 생성 합니다. 첫 번째 인수는 `ActionLink` 메서드를 렌더링 하는 링크 텍스트는 (예를 들어 `<a>Edit Me</a>`). 두 번째 인수는 호출할 동작 메서드의 이름입니다. 마지막 인수는는 [익명 개체](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) (이 경우 ID가 4)에서 경로 데이터를 생성 하 합니다.

이전 그림에 표시 된 생성 된 링크는 `http://localhost:xxxxx/Movies/Edit/4`합니다. 기본 경로 URL 패턴 `{controller}/{action}/{id}`합니다. 따라서 ASP.NET 변환 `http://localhost:xxxxx/Movies/Edit/4` 하는 요청에는 `Edit` 의 동작 메서드는 `Movies` 매개 변수와 함께 컨트롤러 `ID` 4와 같습니다.

쿼리 문자열을 사용 하 여 동작 메서드 매개 변수를 전달할 수 있습니다. 예를 들어 URL `http://localhost:xxxxx/Movies/Edit?ID=4` 매개 변수 전달 `ID` 개로 이루어진는 `Edit` 의 동작 메서드는 `Movies` 컨트롤러입니다.

[![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image6.png)](examining-the-edit-methods-and-edit-view/_static/image5.png)

열기는 `Movies` 컨트롤러입니다. 두 `Edit` 작업 메서드는 다음과 같습니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

두 번째 `Edit` 작업 메서드는 `HttpPost` 특성 뒤에 옵니다. 이 특성의 오버 로드 하는 지정 된 `Edit` POST 요청에 대 한 메서드를 호출할 수 있습니다. 적용할 수는 `HttpGet` 첫 번째 특성 편집 메서드를 사용할 수 있지만 필요한 기본값 이기 때문에 있습니다. (암시적으로 할당 된 작업 메서드를 지칭는 `HttpGet` 특성은 `HttpGet` 메서드.)

`HttpGet` `Edit` 메서드 영화 ID 매개 변수를 조회 하는 Entity Framework를 사용 하 여 동영상 `Find` 메서드를 선택한 동영상 편집 뷰를 반환 합니다. 편집 보기에서 스캐폴딩 시스템이 만들어질 때 `Movie` 클래스를 조사하고 클래스의 각 속성에 대해 `<label>` 및 `<input>` 요소를 렌더링하기 위한 코드를 만들었습니다. 다음 예제에서는 생성 된 편집 뷰를 보여 줍니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

템플릿 보기에는 어떻게는 `@model MvcMovie.Models.Movie` 문을 파일의 맨-이 여부를 지정 된 보기 형식으로 템플릿 보기에 대 한 모델 `Movie`합니다.

스 캐 폴드 코드가 사용 하는 여러 *도우미 메서드* HTML 태그를 간소화할 수 있습니다. [ `Html.LabelFor` ](https://msdn.microsoft.com/library/gg401864(VS.98).aspx) 도우미 필드 (예: "제목", "ReleaseDate", "장르" 또는 "Price")의 이름을 표시 합니다. [ `Html.EditorFor` ](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) HTML을 표시 하는 도우미 `<input>` 요소입니다. [ `Html.ValidationMessageFor` ](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) 도우미 해당 속성과 관련 된 유효성 검사 메시지를 표시 합니다.

응용 프로그램을 실행 하 고 탐색 하 고 */Movies* URL입니다. **편집** 링크를 클릭합니다. 브라우저에서 페이지에 대한 소스를 봅니다. HTML 페이지에서 다음 예제와 유사 합니다. (메뉴 태그는 명확한 설명을 위해 제외 되었습니다.)

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample4.html)]

`<input>` html에서 요소는 `<form>` 요소 인 `action` 특성에 게시 하도록 설정 되어는 */영화/편집* URL입니다. 양식 데이터 서버에 게시 될 때는 **편집** 단추를 클릭 합니다.

## <a name="processing-the-post-request"></a>POST 요청 처리

다음 목록은 `Edit` 작업 메서드의 `HttpPost` 버전을 보여 줍니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs)]

ASP.NET 프레임 워크 모델 바인더는 게시 된 양식 값을 만들고는 `Movie` 변수로 전달 되는 개체는 `movie` 매개 변수입니다. `ModelState.IsValid` 코드에서 검사 수정 하려면 형태로 전송 된 데이터를 사용할 수 있는지 확인 한 `Movie` 개체입니다. 코드 영화 데이터를 저장 된 데이터가 유효한 이면는 `Movies` 의 컬렉션은 `MovieDBContext` 인스턴스. 코드 저장 다음 호출 하 여 새 동영상 데이터를 데이터베이스에는 `SaveChanges` 방식의 `MovieDBContext`, 데이터베이스의 변경 내용을 유지 하는입니다. 데이터를 저장 한 후 코드에 사용자를 리디렉션하는 `Index` 의 동작 메서드는 `MoviesController` 업데이트 된 동영상 영화 목록에 표시 되는 클래스입니다.

게시 된 값에 유효 하지 않습니다, 이러한 형태로 다시 표시 됩니다. `Html.ValidationMessageFor` 에서 도우미는 *Edit.cshtml* 보기 서식 파일을 적절 한 오류 메시지 표시 처리 합니다.

[![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image8.png)](examining-the-edit-methods-and-edit-view/_static/image7.png)

> **로캘에 대 한 참고** 영어가 아닌 로캘로 일반적으로 작업 하는 경우 참조 [영어가 아닌 로캘로 ASP.NET MVC 3 유효성 지원 합니다.](https://msdn.microsoft.com/library/gg674880(VS.98).aspx)


## <a name="making-the-edit-method-more-robust"></a>Edit 메서드 보다 강력한 만들기

`HttpGet` `Edit` 스 캐 폴딩 시스템에서 생성 하는 메서드에 전달 되는 ID가 유효한 지 검사 하지 않습니다. 사용자는 URL에서 ID 세그먼트를 제거 하는 경우 (`http://localhost:xxxxx/Movies/Edit`), 다음과 같은 오류가 표시 됩니다.

[![Null_ID](examining-the-edit-methods-and-edit-view/_static/image10.png)](examining-the-edit-methods-and-edit-view/_static/image9.png)

사용자 수와 같은 데이터베이스에 존재 하지 않는 ID를 전달할 수도 `http://localhost:xxxxx/Movies/Edit/1234`합니다. 두 개의 변경할 수는 `HttpGet` `Edit` 작업 메서드를 이러한 제한 사항을 해결 합니다. 먼저, 변경 된 `ID` ID 명시적으로 전달 되지 않은 경우 기본값인 0 매개 변수입니다. 확인할 수는 `Find` 메서드 템플릿 보기에 동영상 개체를 반환 하기 전에 동영상을 실제로 발견 합니다. 업데이트 된 `Edit` 메서드는 다음과 같습니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

없는 영화 발견 되 면 하는 경우는 `HttpNotFound` 메서드를 호출 합니다.

모든는 `HttpGet` 메서드는 유사한 패턴을 따릅니다. 영화 개체를 가져옵니다 (또는 개체의 경우에서 목록이 `Index`), 보기에는 모델을 전달 합니다. `Create` 메서드 만들기 뷰 빈 영화 개체를 전달 합니다. 생성, 편집, 삭제 또는 어떤 식으로든 데이터를 수정하는 모든 메서드는 메서드의 `HttpPost` 오버로드에서 해당 작업을 수행합니다. 블로그 게시물에에서 설명 된 대로 보안 위험 요소는 HTTP GET 메서드에서 데이터 수정 [ASP.NET MVC 팁 #46-보안 허점을 만들기 때문에 삭제 링크를 사용 하지 않는](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)합니다. HTTP에 대 한 유용한 정보 및 GET 요청 응용 프로그램의 상태를 변경 하지 않아야 지정 아키텍처 REST 패턴에 위반 또한 GET 메서드가에서 데이터를 수정 합니다. 즉, GET 작업을 수행 하면 의도 하는 안전한 연산을 이어야 합니다.

## <a name="adding-a-search-method-and-search-view"></a>검색 방법 및 검색 뷰를 추가합니다.

이 섹션에서는 추가 `SearchIndex` 작업 메서드를 사용 하면 영화 장르 또는 이름으로 검색 합니다. 사용 하 여 사용할 수 있는 됩니다는 */영화/SearchIndex* URL입니다. 요청은 사용자가 영화를 검색 하기 위해에 입력할 수 있는 입력된 요소가 포함 된 HTML 폼에 표시 됩니다. 사용자가 폼을 제출, 작업 메서드는 사용자가 게시 된 검색 값 가져오고 데이터베이스를 검색 하려면 값을 사용 합니다.

## <a name="displaying-the-searchindex-form"></a>SearchIndex 폼을 표시

추가 하 여 시작 된 `SearchIndex` 동작 메서드를 기존 `MoviesController` 클래스입니다. 메서드는 HTML 폼을 포함 하는 뷰를 반환 합니다. 코드는 다음과 같습니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cs)]

첫 번째 줄은 `SearchIndex` 메서드 다음 항목을 만듭니다 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 쿼리는 영화를 선택 하려면:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cs)]

쿼리가 시점에서 정의 되었지만 아직 데이터 저장소에 대해 실행 되지 않았습니다.

경우는 `searchString` 매개 변수는 문자열이 포함 된, 다음 코드를 사용 하 여 검색 문자열을 값으로 필터링 하려면 영화 쿼리가 수정 됩니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

정의 된 또는 같은 메서드를 호출 하 여 수정 된 경우에 LINQ 쿼리 실행 되지 않습니다 `Where` 또는 `OrderBy`합니다. 대신, 쿼리 실행이 지연, 즉, 실제로 실현된 값 반복 될 때까지 식의 계산이 지연 되는지 또는 [ `ToList` ](https://msdn.microsoft.com/library/bb342261.aspx) 메서드를 호출 합니다. 에 `SearchIndex` 샘플 SearchIndex 보기에서 쿼리가 실행 됩니다. 지연된 쿼리 실행에 대한 자세한 내용은 [쿼리 실행](https://msdn.microsoft.com/library/bb738633.aspx)을 참조하세요.

이제 구현할 수는 `SearchIndex` 보기를 사용자에 게 폼을 표시 합니다. 마우스 오른쪽 단추로 클릭는 `SearchIndex` 메서드와 클릭 **뷰 추가**합니다. 에 **뷰 추가** 대화 상자를 전달 하려는 지정는 `Movie` 개체 모델 클래스와 템플릿 보기입니다. 에 **스 캐 폴드 템플릿이** 목록에서 선택 **목록**, 클릭 **추가**합니다.

[![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image12.png)](examining-the-edit-methods-and-edit-view/_static/image11.png)

클릭할 때는 **추가** 단추를는 *Views\Movies\SearchIndex.cshtml* 템플릿 보기 생성 됩니다. 선택 했기 때문에 **목록** 에 **스 캐 폴드 템플릿이** 목록에서 자동으로 생성 하는 Visual Web Developer (스 캐 폴드) 보기의 일부 기본 콘텐츠입니다. 스 캐 폴딩을 HTML 폼을 생성 합니다. 코드 검토는 `Movie` 클래스 및 생성된 된 렌더링 하는 코드 `<label>` 클래스의 각 속성에 대 한 요소입니다. 아래 목록에서는 생성 된 뷰를 만들기를 보여 줍니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

응용 프로그램을 실행 하 고 이동 */영화/SearchIndex*합니다. 쿼리 문자열(예: `?searchString=ghost`)을 URL에 추가합니다. 필터링된 동영상이 표시됩니다.

[![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image14.png)](examining-the-edit-methods-and-edit-view/_static/image13.png)

시그니처를 변경 하는 경우는 `SearchIndex` 메서드 라는 매개 변수를 사용 하려면 `id`, `id` 매개 변수는 일치는 `{id}` 기본값에 대 한 자리 표시자 경로 집합에는 *Global.asax* 파일입니다.

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample11.json)]

수정 된 `SearchIndex` 메서드를 보여 줍니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cs)]

이제 쿼리 문자열 값이 아닌 경로 데이터(URL 세그먼트)로 검색 제목을 전달할 수 있습니다.

[![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image16.png)](examining-the-edit-methods-and-edit-view/_static/image15.png)

그러나 사용자가 영화를 검색하려고 할 때마다 URL을 수정하지는 않습니다. 수 있도록 UI를 추가 합니다 있습니다 지금 동영상을 필터링 합니다. 시그니처를 변경 하는 경우는 `SearchIndex` 경로 바인딩된 ID 매개 변수를 전달 하는 방법을 테스트 하는 메서드 변경 다시 있도록 프로그램 `SearchIndex` 메서드 라는 문자열 매개 변수 `searchString`:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample13.cs)]

열기는 *Views\Movies\SearchIndex.cshtml* 파일을 찾아 바로 뒤에 `@Html.ActionLink("Create New", "Create")`, 다음 코드를 추가 합니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cshtml)]

다음 예제에서는 일부는 *Views\Movies\SearchIndex.cshtml* 파일을 추가 된 태그를 필터링 합니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cshtml)]

`Html.BeginForm` 도우미 만듭니다 여 `<form>` 태그입니다. `Html.BeginForm` 도우미 하면 사용자가 클릭 하 여 폼을 제출 하는 경우 자신에 게 게시 하려면 폼의 **필터** 단추입니다.

응용 프로그램을 실행 하 고 동영상에 대 한 검색을 시도 합니다.

[![SearchIndxIE9_title](examining-the-edit-methods-and-edit-view/_static/image18.png)](examining-the-edit-methods-and-edit-view/_static/image17.png)

없는 `HttpPost` 오버 로드는 `SearchIndex` 메서드. 필요 없는, 메서드는 응용 프로그램의 상태를 변경 되지 않습니다 때문에 데이터를 필터링 합니다.

다음 `HttpPost SearchIndex` 메서드를 추가할 수 있습니다. 작업 호출자는 일치 하는 경우에 `HttpPost SearchIndex` 메서드, 및 `HttpPost SearchIndex` 메서드 아래 이미지에 나와 있는 것 처럼 실행 됩니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

[![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image20.png)](examining-the-edit-methods-and-edit-view/_static/image19.png)

그러나 이 `HttpPost` 버전의 `SearchIndex` 메서드를 추가하는 경우에도 이를 모두 구현하는 방법은 제한됩니다. 특정 검색을 책갈피로 설정하거나 동일하게 필터링된 영화 목록을 보기 위해 클릭할 수 있는 링크를 친구에게 보내려고 한다고 가정합니다. HTTP POST에 대 한 URL를 요청 하는 GET 요청 (localhost:xxxxx/영화/SearchIndex)에 대 한 URL과 동일한-URL 자체에 검색 정보가 없습니다. 오른쪽 지금 검색 문자열 정보는 전송 서버에 양식 필드 값으로. 즉, 책갈피를 URL에는 친구에 게 보내고 해당 검색 정보를 캡처할 수 없습니다.

솔루션의 오버 로드를 사용 하는 것 `BeginForm` POST 요청 URL에 검색 정보를 추가 해야 하 고 있어야 하는 지정 하는의 HttpGet 버전으로 라우팅되는 `SearchIndex` 메서드. 매개 변수가 없는 기존 항목 바꾸기 `BeginForm` 메서드를 다음:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml)]

[![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image22.png)](examining-the-edit-methods-and-edit-view/_static/image21.png)

이제 검색을 제출할 때 URL 검색 쿼리 문자열을 포함 합니다. `HttpPost SearchIndex` 메서드가 있는 경우에도 검색은 `HttpGet SearchIndex` 작업 메서드로 이동합니다.

[![SearchIndexWithGetURL](examining-the-edit-methods-and-edit-view/_static/image24.png)](examining-the-edit-methods-and-edit-view/_static/image23.png)

## <a name="adding-search-by-genre"></a>장르별로 검색 추가

추가한 경우는 `HttpPost` 버전의는 `SearchIndex` 메서드를 지금 삭제 합니다.

다음으로, 사용자가 영화가 장르별로 검색할 수 있도록 하는 기능을 추가 합니다. `SearchIndex` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cs)]

이 버전의는 `SearchIndex` 메서드는 추가 매개 변수, 즉 `movieGenre`합니다. 코드의 처음 몇 줄 만들기는 `List` 데이터베이스에서 영화 장르를 보유 하는 개체입니다.

다음 코드는 데이터베이스에서 모든 장르를 검색하는 LINQ 쿼리입니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

코드를 사용 하 여는 `AddRange` 메서드는 제네릭의 `List` 모든 고유 장르 목록에 추가할 컬렉션입니다. (없이 `Distinct` 한정자를 중복 장르는 추가-샘플에 두 번 코미디는 추가 하는 예를 들어). 코드에는 다음에 장르 목록을 저장 된 `ViewBag` 개체입니다.

다음 코드를 확인 하는 방법을 보여 줍니다는 `movieGenre` 매개 변수입니다. 비어 있지 않으면 코드를 추가로 지정된 장르에 선택 된 동영상을 제한 하려면 영화 쿼리를 제한 합니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>장르별로 검색을 지 원하는 SearchIndex 보기에 태그 추가

추가 `Html.DropDownList` 도우미에는 *Views\Movies\SearchIndex.cshtml* 파일, 바로 앞의 `TextBox` 도우미입니다. 완성 된 태그는 다음과 같습니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cshtml)]

응용 프로그램을 실행 하 고 찾아보기 */영화/SearchIndex*합니다. 장르, 영화 제목 및 두 조건으로 검색을 시도 하십시오.

이 섹션의 CRUD 작업 메서드 및 프레임 워크에 의해 생성 된 뷰를 검사 합니다. 검색 작업 메서드와 뷰 사용자가 영화 제목 및 장르 하 여 검색할 수 있도록 만들었습니다. 다음 섹션에서 살펴보겠습니다 속성을 추가 하는 방법의 `Movie` 모델 및 테스트 데이터베이스에서 자동으로 만듭니다는 이니셜라이저를 추가 하는 방법입니다.

> [!div class="step-by-step"]
> [이전](accessing-your-models-data-from-a-controller.md)
> [다음](adding-a-new-field.md)
