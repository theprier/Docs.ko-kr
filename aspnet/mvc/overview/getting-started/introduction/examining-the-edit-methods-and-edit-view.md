---
uid: mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
title: "편집 메서드 및 편집 보기 검사 | Microsoft Docs"
author: Rick-Anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/22/2015
ms.topic: article
ms.assetid: 52a4d5fe-aa31-4471-b3cb-a064f82cb791
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 84aadccc18e7fa0fb56c7a78e144a1bf1038aac5
ms.sourcegitcommit: d1d8071d4093bf2444b5ae19d6e45c3d187e338b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/19/2017
---
<a name="examining-the-edit-methods-and-edit-view"></a>편집 메서드 및 편집 보기 검사
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE[Tutorial Note](sample/code-location.md)]

이 섹션에서는 검토해 생성 된 `Edit` 작업 메서드 및 동영상 컨트롤러에 대 한 뷰. 하지만 먼저 더 보기 좋게 출시 날짜에 있도록 짧은 전환 소요 됩니다. 열기는 *Models\Movie.cs* 파일을 아래 표시 된 강조 표시 된 줄을 추가 합니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cs?highlight=2,12-14)]

다음과 같은 특정 날짜 문화권을도 만들 수 있습니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs?highlight=3)]

다음 자습서에서는 [DataAnnotations](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.aspx)를 다룹니다. [Display](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayattribute.aspx) 특성은 필드의 이름에 표시할 대상을 지정합니다(이 경우 "ReleaseDate" 대신 "Release Date"). [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성 데이터의 형식을 지정,이 경우 이므로 날짜 필드에 저장 된 시간 정보 표시 되지 않습니다. [DisplayFormat](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 날짜 형식을 올바르게 렌더링 Chrome 브라우저에서 버그에 대 한 특성은 필요 합니다.

응용 프로그램을 실행 하 고를 찾습니다는 `Movies` 컨트롤러입니다. 위에 마우스 포인터는 **편집** 를 연결 하는 URL을 보려면이 링크를 합니다.

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

**편집** 에 의해 생성 된 링크는 `Html.ActionLink` 에서 메서드는 *Views\Movies\Index.cshtml* 보기:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

![Html.ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html` 개체에서 속성을 사용 하 여 노출 되는 도우미는는 [System.Web.Mvc.WebViewPage](https://msdn.microsoft.com/en-us/library/gg402107(VS.98).aspx) 기본 클래스입니다. `ActionLink` 도우미의 메서드를 사용 하면 쉽게를 동적으로 컨트롤러 작업 메서드에 연결 되는 하이퍼링크는 HTML을 생성 합니다. 첫 번째 인수는 `ActionLink` 메서드를 렌더링 하는 링크 텍스트는 (예를 들어 `<a>Edit Me</a>`). 두 번째 인수는 호출할 동작 메서드의 이름 (이 경우는 `Edit` 동작). 마지막 인수는는 [익명 개체](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) (이 경우 ID가 4)에서 경로 데이터를 생성 하 합니다.

이전 그림에 표시 된 생성 된 링크는 `http://localhost:1234/Movies/Edit/4`합니다. 기본 경로 (에 설정 된 *앱\_Start\RouteConfig.cs*) URL 패턴은 `{controller}/{action}/{id}`합니다. 따라서 ASP.NET 변환 `http://localhost:1234/Movies/Edit/4` 하는 요청에는 `Edit` 의 동작 메서드는 `Movies` 매개 변수와 함께 컨트롤러 `ID` 4와 같습니다. 다음 코드를 검사 하는 *앱\_Start\RouteConfig.cs* 파일입니다. [MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) HTTP 요청을 올바른 컨트롤러 및 작업 메서드로 라우팅하고 선택적 ID 매개 변수를 지정한 메서드를 사용 합니다. [MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) 메서드를 사용 하 여 [HtmlHelpers](https://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper(v=vs.108).aspx) 같은 `ActionLink` 컨트롤러, 작업 메서드 및 경로 데이터를 제공 하는 Url을 생성 하 합니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cs?highlight=7)]

쿼리 문자열을 사용 하 여 동작 메서드 매개 변수를 전달할 수 있습니다. 예를 들어 URL `http://localhost:1234/Movies/Edit?ID=3` 매개 변수 전달 `ID` 3는 `Edit` 의 동작 메서드는 `Movies` 컨트롤러입니다.

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

열기는 `Movies` 컨트롤러입니다. 두 `Edit` 작업 메서드는 다음과 같습니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs?highlight=19-21)]

두 번째 `Edit` 작업 메서드는 `HttpPost` 특성 뒤에 옵니다. 이 특성을 지정 하는 오버 로드는 `Edit` POST 요청에 대 한 메서드를 호출할 수 있습니다. 적용할 수는 `HttpGet` 첫 번째 특성 편집 메서드를 사용할 수 있지만 필요한 기본값 이기 때문에 있습니다. (암시적으로 할당 된 작업 메서드를 지칭는 `HttpGet` 특성은 `HttpGet` 메서드.) [바인딩할](https://msdn.microsoft.com/en-us/library/system.web.mvc.bindattribute(v=vs.108).aspx) 특성은가 과도 하 게 모델에 데이터를 게시 해커를 유지 하는 또 다른 중요 한 보안 메커니즘입니다. 변경 하려면 바인딩 특성의 속성만 포함 해야 합니다. Overposting와 바인딩 특성에 대해 알아볼 수 있습니다 내 [보안 정보를 초과 게시](https://go.microsoft.com/fwlink/?LinkId=317598)합니다. 이 자습서에 사용 된 단순 모델에서 모델의 모든 데이터 바인딩 수 됩니다 것입니다. [ValidateAntiForgeryToken](https://msdn.microsoft.com/en-us/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) 특성 요청 위조를 방지 하기 위해 사용 되 고을 이룹니다 `@Html.AntiForgeryToken()` 파일 편집 보기에서에서 (*Views\Movies\Edit.cshtml*), 일부는 다음과 같습니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cshtml?highlight=9)]

`@Html.AntiForgeryToken()`에 일치 하는 숨겨진된 폼 위조 방지 토큰을 생성 된 `Edit` 의 메서드는 `Movies` 컨트롤러입니다. 자세히 알아볼 수 있습니다에 대 한 사이트 간 요청 위조 (XSRF 또는 CSRF 라고도 함) 내 자습서에서 [mvc에서 XSRF/CSRF 방지](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)합니다.

`HttpGet` `Edit` 메서드 영화 ID 매개 변수를 조회 하는 Entity Framework를 사용 하 여 동영상 `Find` 메서드를 선택한 동영상 편집 뷰를 반환 합니다. 동영상을 찾을 수 없는 경우 [HttpNotFound](https://msdn.microsoft.com/en-us/library/gg453938(VS.98).aspx) 반환 됩니다. 편집 보기에서 스캐폴딩 시스템이 만들어질 때 `Movie` 클래스를 조사하고 클래스의 각 속성에 대해 `<label>` 및 `<input>` 요소를 렌더링하기 위한 코드를 만들었습니다. 다음 예제에서는 visual studio 스 캐 폴딩 시스템에서 생성 된 편집 뷰를 보여 줍니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

템플릿 보기에는 어떻게는 `@model MvcMovie.Models.Movie` 문을 파일의 맨-이 여부를 지정 된 보기 형식으로 템플릿 보기에 대 한 모델 `Movie`합니다.

스 캐 폴드 코드가 사용 하는 여러 *도우미 메서드* HTML 태그를 간소화할 수 있습니다. [ `Html.LabelFor` ](https://msdn.microsoft.com/en-us/library/gg401864(VS.98).aspx) 필드의 이름을 표시 하는 도우미 (&quot;제목&quot;, &quot;ReleaseDate&quot;, &quot;장르&quot;, 또는 &quot;가격 &quot;). [ `Html.EditorFor` ](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) 도우미는 HTML 렌더링 `<input>` 요소입니다. [ `Html.ValidationMessageFor` ](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) 도우미 해당 속성과 관련 된 유효성 검사 메시지를 표시 합니다.

응용 프로그램을 실행 하 고 탐색 하 고 */Movies* URL입니다. **편집** 링크를 클릭합니다. 브라우저에서 페이지에 대한 소스를 봅니다. HTML 폼 요소에는 다음과 같습니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cshtml?highlight=1-2)]

`<input>` html에서 요소는 `<form>` 요소 인 `action` 특성에 게시 하도록 설정 되어는 */영화/편집* URL입니다. 양식 데이터 서버에 게시 될 때는 **저장** 단추를 클릭 합니다. 두 번째 줄은 표시 숨겨진 [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) 에 의해 생성 된 토큰의 `@Html.AntiForgeryToken()` 호출 합니다.

## <a name="processing-the-post-request"></a>POST 요청 처리

다음 목록은 `Edit` 작업 메서드의 `HttpPost` 버전을 보여 줍니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

[ValidateAntiForgeryToken](https://msdn.microsoft.com/en-us/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) 특성의 유효성을 검사는 [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) 에 의해 생성 된 토큰은 `@Html.AntiForgeryToken()` 보기에서 호출 합니다.

[ASP.NET MVC 모델 바인더](https://msdn.microsoft.com/en-us/library/dd410405.aspx) 에서는 게시 된 양식 값을 사용 하 고 만듭니다는 `Movie` 변수로 전달 되는 개체는 `movie` 매개 변수입니다. `ModelState.IsValid` 메서드는 양식에서 제출된 데이터가 `Movie` 개체를 수정하는 데(편집 또는 업데이트) 사용될 수 있음을 확인합니다. 데이터가 올바른지, 동영상 데이터에 저장 됩니다는 `Movies` 의 컬렉션은 `db(MovieDBContext` 인스턴스). 새 동영상 데이터를 호출 하 여 데이터베이스에 저장 되는 `SaveChanges` 방식의 `MovieDBContext`합니다. 데이터를 저장한 후 코드는 사용자를 `MoviesController` 클래스의 `Index` 동작 메서드로 다시 전달하며, 여기에는 방금 수행한 변경 사항을 포함하여 동영상 컬렉션이 표시됩니다.

클라이언트 쪽 유효성 검사 필드의 값이 유효한 지를 결정 하는 즉시 오류 메시지가 표시 됩니다. JavaScript를 비활성화 하면 클라이언트 쪽 유효성 검사 없을 수 있지만 서버에서 감지 하는 게시 된 값에 올바르지 않은 폼 값은 오류 메시지를 다시 표시 됩니다. 이 자습서의 뒷부분에 나오는 유효성 검사를에서 자세히 살펴보겠습니다.

`Html.ValidationMessageFor` 에서 도우미는 *Edit.cshtml* 보기 서식 파일을 적절 한 오류 메시지 표시 처리 합니다.

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

모든는 `HttpGet` 메서드는 유사한 패턴을 따릅니다. 영화 개체를 가져옵니다 (또는 개체의 경우에서 목록이 `Index`), 보기에는 모델을 전달 합니다. `Create` 메서드 만들기 뷰 빈 영화 개체를 전달 합니다. 생성, 편집, 삭제 또는 어떤 식으로든 데이터를 수정하는 모든 메서드는 메서드의 `HttpPost` 오버로드에서 해당 작업을 수행합니다. 블로그 게시물에에서 설명 된 대로 보안 위험 요소는 HTTP GET 메서드에서 데이터 수정 [ASP.NET MVC 팁 #46-보안 허점을 만들기 때문에 삭제 링크를 사용 하지 않는](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)합니다. HTTP에 대 한 유용한 정보 및 아키텍처는 또한 위반 GET 메서드가의 데이터 수정 [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) 패턴 지정 한 GET 요청을 응용 프로그램의 상태를 변경 하지 않아야 합니다. 다시 말해 GET 작업 수행은 부작용 없이 안전하고 영속 데이터를 수정하지 않는 방법으로 이루어져야 합니다.

영어 (미국) 컴퓨터를 사용 하는 경우이 단계를 생략 하 고 자습서로 이동할 수 있습니다. 이 자습서의 Globalize 버전을 다운로드할 수 [여기](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475)합니다. 국제화에 뛰어난 두 부분으로 구성 자습서를 참조 하십시오. [Nadeem의 ASP.NET MVC 5 국제화](http://afana.me/post/aspnet-mvc-internationalization.aspx)합니다.


> [!NOTE]
> 쉼표를 사용 하는 영어가 아닌 로캘의 jQuery 유효성 검사를 지원 하기 위해 (&quot;,&quot;) 소수점 및 미국 영어가 아닌 날짜 형식을 포함 해야 *globalize.js* 및 특정  *cultures/globalize.cultures.js* 파일 (에서 [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) 및 사용 하는 JavaScript `Globalize.parseFloat`합니다. NuGet에서 jQuery 영어가 아닌 유효성 검사를 가져올 수 있습니다. (설치 하지 마십시오 Globalize 영어 로캘의 사용 하는 경우.)


1. **도구** 메뉴 클릭 **NuGetLibrary 패키지 관리자**, 클릭 하 고 **솔루션에 대 한 NuGet 패키지 관리**합니다.  
  
    ![](examining-the-edit-methods-and-edit-view/_static/image5.png)
2. 왼쪽된 창에서 선택  **찾아보기*.* * * (아래 그림 참조).
3. 입력된 상자에 입력 *Globalize** 합니다.  
  
    ![](examining-the-edit-methods-and-edit-view/_static/image6.png)선택 `jQuery.Validation.Globalize`, 선택 `MvcMovie` 클릭 **설치**합니다. *Scripts\jquery.globalize\globalize.js* 파일을 프로젝트에 추가 됩니다. *Scripts\jquery.globalize\cultures\* 폴더 많은 문화권 JavaScript 파일에 포함 됩니다. Note:이 패키지를 설치 하는 데 5 분이 걸릴 수 있습니다.

 다음 코드에서는 Views\Movies\Edit.cshtml 파일의 수정 내용을 보여 줍니다. 

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

반복 되는 모든 편집 보기에서이 코드를 방지 하려면 레이아웃 파일을 이동할 수 있습니다. 스크립트 다운로드를 최적화 하려면 내 자습서를 참조 하십시오. [묶음 및 축소](../../performance/bundling-and-minification.md)합니다.

자세한 내용은 참조 [ASP.NET MVC 3 국제화](http://afana.me/post/aspnet-mvc-internationalization.aspx) 및 [ASP.NET MVC 3 국제화-2 부 (업그레이드 되었으며 수정)](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx)합니다.

임시 수정과 해당 로캘에에서 작업 하는 유효성 검사를 가져올 수 없습니다 영어 (미국)를 사용 하도록 컴퓨터를 강제로 수행할 수 있습니다 또는 브라우저에서 JavaScript를 비활성화할 수 있습니다. 영어 (미국)를 사용 하도록 컴퓨터를 강제로 표시 하려면 프로젝트 루트에 세계화 요소를 추가할 수 있습니다 *web.config* 파일입니다. 다음 코드는 문화권을 영어 (미국)로 설정 된 세계화 요소를 보여 줍니다.

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample11.xml)]

<a id="gettingstarted"></a><a id="jQueryAjaxJSON"></a>다음 자습서에서에서는 검색 기능을 구현 합니다.

>[!div class="step-by-step"]
[이전](accessing-your-models-data-from-a-controller.md)
[다음](adding-search.md)
