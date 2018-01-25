---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
title: "ASP.NET MVC DropDownList 도우미 사용 | Microsoft Docs"
author: Rick-Anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2012
ms.topic: article
ms.assetid: 53767e05-c8ab-42e1-a94b-22d906195200
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 278d04aec68e93f3ebfd12d06a96b59f3bcbef4b
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="using-the-dropdownlist-helper-with-aspnet-mvc"></a>ASP.NET MVC DropDownList 도우미 사용
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

이 자습서의 작업을 기본 사항은 설명 됩니다는 [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) 도우미 및 [ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) ASP.NET MVC 웹 응용 프로그램에서 도우미입니다. Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 자습서를 수행 하려면 Microsoft Visual Studio의 무료 버전을 사용할 수 있습니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다. 다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.

- [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)<a id="post"></a>
- [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)

Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다. 이 자습서를 마쳤습니다 가정는 [ASP.NET MVC 소개](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서 또는[ASP.NET MVC Music Store](../mvc-music-store/mvc-music-store-part-1.md) 자습서 이거나 익숙한 ASP.NET MVC 개발 합니다. 이 자습서에서 수정 된 프로젝트 시작의 [ASP.NET MVC Music Store](../mvc-music-store/mvc-music-store-part-1.md) 자습서입니다. 다음 링크를 사용 하 여 시작 프로젝트를 다운로드할 수 있습니다 [C# 버전을 다운로드](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829)합니다.

C# 소스 코드 완성 된 자습서와 함께 Visual Web Developer 프로젝트는이 항목에 수반 됩니다. [다운로드](https://code.msdn.microsoft.com/Using-the-DropDownList-67f9367d)합니다.

### <a name="what-youll-build"></a>만들 것인지

작업 메서드 및 뷰를 사용 하는 만듭니다는 [DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) 범주를 선택 하는 도우미입니다. 또한 사용 합니다 **jQuery** 새 범주 (예: 장르 또는 예술가)이 필요한 경우 사용할 수 있는 삽입 범주 대화 상자를 추가 합니다. 다음은 새 장르를 추가 하 고 새 예술가 추가에 대 한 링크를 보여 주는 뷰 만들기의 스크린샷을입니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image1.png)

### <a name="skills-youll-learn"></a>기술을 알아봅니다

학습할 다음과 같습니다.

- 사용 하는 방법의 [DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) 범주 데이터를 선택 하는 도우미입니다.
- 추가 하는 방법 한 **jQuery** 대화 새 범주를 추가 합니다.

### <a name="getting-started"></a>시작

다음 링크를 사용 하 여 시작 프로젝트를 다운로드 하 여 시작 [다운로드](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829)합니다. Windows 탐색기에서 마우스 오른쪽 단추로 클릭는 *DDL\_Starter.zip* 파일 및 속성을 선택 합니다. 에 **DDL\_Starter.zip 속성** 대화 상자에서 선택 차단 해제 합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image2.png)

DDL을 마우스 오른쪽 단추로 클릭\_Starter.zip 파일과 선택 **압축 풀기** 파일 압축을 풀입니다. 열기는 *StartMusicStore.sln* Visual Studio 2010 또는 Visual Web Developer 2010 Express ("Visual Web Developer" 또는 "VWD" 줄여서) 파일입니다.

CTRL + f 5를 눌러 응용 프로그램을 실행 하 고 클릭 하 고 **테스트** 링크 합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image3.png)

선택 된 **영화 범주 선택 (단순)** 링크 합니다. 선택한 값 코미디 영화 형식 선택 목록 표시 됩니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image4.png)

마우스 오른쪽 단추로 클릭 하면 브라우저 창과 소스 뷰를 선택 합니다. HTML 페이지에 표시 됩니다. 아래 코드에서는 HTML select 요소를 보여 줍니다.

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample1.html)]

Select 목록의 각 항목에 값 (작업에 대 한 0, 드라마 1, 2 코미디에 대 한 및 과학 소설에 대 한 3) 및 표시 이름 (예: 작업, 드라마, 코미디 및 과학 소설) 있는지 확인할 수 있습니다. 위의 코드에는 select 목록에 대 한 표준 HTML입니다.

드라마 고 select 목록 변경는 **전송** 단추입니다. 브라우저에서 URL은 `http://localhost:2468/Home/CategoryChosen?MovieType=1` 페이지에는 표시 및 **선택한: 1**합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image5.png)

열기는 *Controllers\HomeController.cs* 파일 및 검사는 `SelectCategory` 메서드.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample2.cs)]

[DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) 도우미 HTML 선택 목록을 만드는 데 필요한는 **IEnumerable&lt;SelectListItem &gt;** , 명시적 또는 암시적으로 합니다. 즉, 전달할 수 있습니다는 **a b l e&lt;SelectListItem &gt;**  에 명시적으로 [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) 도우미 추가할 수 있습니다는 **IEnumerable&lt; SelectListItem &gt;**  에 [ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 에 동일한 이름을 사용 하는 **SelectListItem** 모델 속성으로. 전달 된 **SelectListItem** 암시적 및 명시적으로 자습서의 다음 부분에 대해서는 설명 합니다. 위의 코드를 만드는 가장 간단한 가능한 방법은 표시는 **a b l e&lt;SelectListItem &gt;**  텍스트와 값으로 채웁니다. 참고는 `Comedy` [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) 에 [선택한](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.selected.aspx) 속성이로 설정 **true;** 이렇게 렌더링 된 선택 목록 표시 하도록 하면 **코미디** 목록에서 선택한 항목으로 합니다.

**a b l e&lt;SelectListItem &gt;**  만든 위에에 추가 되는 [ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) MovieType 이름의 합니다. 이 전달 방법을 **a b l e&lt;SelectListItem &gt;**  암시적으로 [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) 도우미 아래에 표시 합니다.

열기는 *Views\Home\SelectCategory.cshtml* 파일 및 태그를 검사 합니다.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample3.cshtml)]

세 번째 줄에 설정 하 여 레이아웃을 뷰/공유/\_간단한\_Layout.cshtml은 표준 레이아웃 파일의 단순화 된 버전입니다. 표시 하지 않으려면이 작업을 수행 하 고 렌더링 된 HTML 단순 합니다.

이 샘플에서는 변경 하지 않는 응용 프로그램의 상태 하므로 사용 하 여 데이터 전송 됩니다는 **HTTP GET**이 아니라 **HTTP POST**합니다. W3C 섹션을 참조 [선택 HTTP GET 또는 POST에 대 한 빠른 검사 목록](http://www.w3.org/2001/tag/doc/whenToUseGet.html#checklist)합니다. 사용 하지는 응용 프로그램을 변경 하 고 폼 게시, 때문에 [Html.BeginForm](https://msdn.microsoft.com/library/dd460344.aspx) 동작 메서드, 컨트롤러 및 폼 메서드를 지정할 수 있도록 하는 오버 로드 (**HTTP POST** 또는 **HTTP GET**). 일반적으로 뷰를 포함 된 [Html.BeginForm](https://msdn.microsoft.com/library/dd505244.aspx) 매개 변수가 없는 오버 로드 합니다. 매개 변수 버전이 없는 POST 버전의 동일한 작업 메서드 및 컨트롤러에 양식 데이터를 게시 기본값으로 사용 됩니다.

다음 줄

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample4.cshtml)]

에 대 한 문자열 인수를 전달 된 **DropDownList** 도우미입니다. 이 문자열 "MovieType" 예제에서는 두 가지 작업을 수행합니다.

- 에 대 한 키를 제공 한다고는 **DropDownList** 찾으려고 도우미는 **a b l e&lt;SelectListItem &gt;**  에 **ViewBag**합니다.
- 이 데이터 바인딩된 MovieType 폼 요소에 있습니다. Submit 메서드가 **HTTP GET**, `MovieType` 쿼리 문자열이 됩니다. Submit 메서드가 **HTTP POST**, `MovieType` 메시지 본문에 추가 됩니다. 다음 그림에서는 값이 1 인 쿼리 문자열을 보여 줍니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image6.png)

다음 코드는 `CategoryChosen` 메서드 폼에 전송 합니다.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample5.cs)]

테스트 페이지로 다시 이동 하 고 선택 된 **HTML SelectList** 링크 합니다. HTML 페이지 간단한 ASP.NET MVC 테스트 페이지 유사 하 게 select 요소를 렌더링합니다. 브라우저 창을 마우스 오른쪽 단추로 클릭 하 고 선택 **소스 보기**합니다. Select 목록에 대 한 HTML 태그는 기본적으로 동일 합니다. 테스트 HTML 페이지는 ASP.NET MVC 동작 메서드 및 보기 이미 테스트 처럼 작동 합니다.

### <a name="improving-the-movie-select-list-with-enums"></a>열거형을 사용 하 여 영화 선택 목록 개선

응용 프로그램에 있는 범주 해결 변경 되지 것입니다을 더욱 강력 하 고 더 쉽게 확장 하 여 코드를 쉽게 열거형을 이용할 수 있습니다. 새 범주를 추가 하는 경우 올바른 범주 값이 생성 됩니다. 새 범주를 추가 하지만 범주 값을 업데이트 하지 복사 및 붙여넣기 오류를 방지 합니다.

열기는 *Controllers\HomeController.cs* 파일을 다음 코드를 검사 합니다.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample6.cs)]

[enum](https://msdn.microsoft.com/library/sbbt4032(VS.80).aspx) `eMovieCategories` 4 개의 동영상 유형 캡처합니다. `SetViewBagMovieType` 메서드를 만듭니다는 **a b l e&lt;SelectListItem &gt;**  에서 `eMovieCategories` **enum**, 설정 및는 `Selected` 는 속성`selectedMovie` 매개 변수입니다. `SelectCategoryEnum` 작업 메서드가 동일한 뷰를 사용 하 여는 `SelectCategory` 동작 메서드가 있습니다.

테스트 페이지를 탐색 하 고 클릭는 `Select Movie Category (Enum)` 링크 합니다. 이 이번에 표시 되는 값 (숫자), 대신 열거형을 나타내는 문자열로 표시 됩니다.

### <a name="posting-enum-values"></a>열거형 값에 게시

HTML 폼 서버에 데이터를 게시 하려면 일반적으로 사용 됩니다. 다음 코드는 `HTTP GET` 및 `HTTP POST` 버전의는 `SelectCategoryEnumPost` 메서드.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample7.cs)]

전달 하 여 한 `eMovieCategories` 열거형에는 `POST` 메서드를 enum 값과 열거형 문자열 모두 추출할 수 있습니다. 이 샘플을 실행 하 고 테스트 페이지로 이동 합니다. 클릭는 `Select Movie Category(Enum Post)` 링크 합니다. 영화 유형을 선택 하 고 전송 단추를 누릅니다. 값과 영화 형식의 이름을 모두 표시합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image7.png)

### <a name="creating-a-multiple-section-select-element"></a>여러 섹션 Select 요소 만들기

[ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) HTML을 렌더링 하는 HTML 도우미 `<select>` 인 요소는 `multiple` 특성을 여러 개 선택할 수 있습니다. 테스트 링크 문서로 이동한 다음 선택에서 **다중 선택 국가** 링크 합니다. 렌더링 된 UI를 사용 하면 여러 국가 선택할 수 있습니다. 아래 그림에서는 캐나다 및 중국 선택 됩니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image8.png)

### <a name="examining-the-multiselectcountry-code"></a>MultiSelectCountry 코드 검사

다음 코드를 검사 하는 *Controllers\HomeController.cs* 파일입니다.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample8.cs)]

`GetCountries` 메서드 국가, 목록을 만들어 다음에 전달 된 `MultiSelectList` 생성자입니다. `MultiSelectList` 생성자 오버 로드에 사용 되는 `GetCountries` 위의 메서드 4 개의 매개 변수를 사용 합니다.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample9.cs)]

1. *항목*:는 [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) 목록에 항목을 포함 하 합니다. 국가의 목록 위의 예제입니다.
2. *dataValueField*:에 속성의 이름은 **IEnumerable** 값이 포함 된 목록입니다. 위의 예에는 `ID` 속성입니다.
3. *dataTextField*:에 속성의 이름은 **IEnumerable** 표시할 정보를 포함 하는 목록입니다. 위의 예에는 `name` 속성입니다.
4. *selectedValues*: 선택한 값 목록입니다.

위의 예에는 `MultiSelectCountry` 메서드가 전달은 `null` UI에 표시 될 때 없는 국가 선택 되어 있으므로 선택 된 국가 대 한 값입니다. 다음 코드에서는 Razor 태그를 렌더링 하는 데는 `MultiSelectCountry` 보기.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample10.cshtml)]

HTML 도우미 [ListBox](https://msdn.microsoft.com/library/dd470200.aspx) 메서드 위에 사용 두 개의 매개 변수를 모델 바인딩할 속성의 이름 및 [MultiSelectList](https://msdn.microsoft.com/library/system.web.mvc.multiselectlist.aspx) 포함 옵션을 선택 하 고 값입니다. `ViewBag.YouSelected` 위의 코드는 폼을 제출 하면 선택한 국가 같이 값을 표시 하는 데 사용 됩니다. HTTP POST 오버 로드 확인은 `MultiSelectCountry` 메서드.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample11.cs)]

`ViewBag.YouSelected` 동적 속성에 대 한 가져온 선택 된 국가, 포함 된 `Countries` 폼 컬렉션의에서 항목입니다. 이 버전에서는 GetCountries 메서드 전달 합니다. 선택한 국가 목록이 있으므로 `MultiSelectCountry` 보기 표시 되 면 UI에서 선택한 국가 같이 선택 합니다.

### <a name="making-a-select-element-friendly-with-the-harvest-chosen-jquery-plugin"></a>선택 요소 친숙 한 수확 선택한 jQuery 플러그 인으로 만들기

수집 [선택한](http://harvesthq.github.com/chosen/) HTML에 jQuery 플러그 인을 추가할 수 있습니다 &lt;선택&gt; 사용자를 만들려면 요소 친화적 UI입니다. 아래 이미지는 수집을 보여 줍니다. [선택한](http://harvesthq.github.com/chosen/) jQuery 인 플러그 인 `MultiSelectCountry` 보기.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image9.png)

아래의 두 가지 이미지에서 **캐나다** 을 선택 합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image10.png)

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image11.png)

위의 그림에서 캐나다를 선택한 포함 된 프로그램 **x** 선택 영역을 제거 하기 위해 클릭할 수 있습니다. 아래 이미지 캐나다, 중국, 보여주며, 일본 선택 합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image12.png)

### <a name="hooking-up-the-harvest-chosen-jquery-plugin"></a>플러그 인 수확 선택한 jQuery 후크

다음 섹션은 이해를 돕기 jQuery 다소 경험이 있는 경우. JQuery 하기 전에 처음 사용 하는 경우 다음 jQuery 자습서 중 하나를 시도 하는 것이 좋습니다.

- [JQuery의 작동 원리](http://docs.jquery.com/Tutorials:How_jQuery_Works) 여 [John Resig](http://ejohn.org/)
- [JQuery 시작](http://docs.jquery.com/Tutorials:Getting_Started_with_jQuery) 여 [Jörn Zaefferer](http://bassistance.de/)
- [JQuery의 예 라이브](http://codylindley.com/blogstuff/js/jquery/#) 여 [Cody Lindley](http://codylindley.com/)

선택한 플러그 인이이 자습서와 함께 제공 되는 완성 된 샘플 프로젝트와 스타터에 포함 됩니다. 이 자습서에 대 한만 jQuery UI 후크 하는 데 필요 합니다. ASP.NET MVC 프로젝트에서 9 월 선택한 jQuery 플러그 인을 사용 하려면 다음을 수행 해야 합니다.

1. 선택한 플러그 인을 다운로드 [github](https://github.com/harvesthq/chosen/)합니다. 이 단계를 수행 하지 않았습니다.
2. 선택한 폴더를 ASP.NET MVC 프로젝트를 추가 합니다. 선택한 폴더에 이전 단계에서 다운로드 한 선택한 플러그 인에서 자산을 추가 합니다. 이 단계를 수행 하지 않았습니다.
3. 선택한 플러그 인을 연결 된 **DropDownList** 또는 **ListBox** HTML 도우미입니다.

### <a name="hooking-up-the-chosen-plugin-to-the-multiselectcountry-view"></a>선택한 플러그 인 MultiSelectCountry 보기에 연결 합니다.

열기는 *Views\Home\MultiSelectCountry.cshtml* 파일을 추가 `htmlAttributes` 매개 변수는 `Html.ListBox`합니다. 추가한 매개 변수는 select 목록에 대 한 클래스 이름 포함 (`@class = "chzn-select"`). 완성 된 코드는 다음과 같습니다.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample12.cshtml)]

위의 코드에 추가 하 고 HTML 특성 및 특성 값 `class = "chzn-select"`합니다. @ 문자 앞에 클래스 아무런 상관이 Razor 뷰 엔진입니다. `class`이 [C# 키워드](https://msdn.microsoft.com/library/x53a06bb.aspx)합니다. 접두사로 @을 포함 하지 않는 한 C# 키워드를 식별자로 사용할 수 없습니다. 위의 예에서 `@class` 올바른 식별자가 있지만 **클래스** 않으므로 **클래스** 는 키워드입니다.

에 대 한 참조 추가 *Chosen/chosen.jquery.js* 및 *Chosen/chosen.css* 파일입니다. *Chosen/chosen.jquery.js* 구현 하는 선택한 플러그 인의 기능적으로 합니다. *Chosen/chosen.css* 파일은 스타일 지정을 제공 합니다. 맨 아래에 다음이 참조를 추가 *Views\Home\MultiSelectCountry.cshtml* 파일입니다. 다음 코드에는 선택한 플러그 인을 참조 하는 방법을 보여 줍니다.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample13.cshtml)]

선택한 플러그 인에 사용 된 클래스 이름을 사용 하 여 활성화는 **Html.ListBox** 코드입니다. 위의 예에서 클래스 이름은 `chzn-select`합니다. 맨 아래에 다음 줄 추가 *Views\Home\MultiSelectCountry.cshtml* 파일 보기. 이 줄은 선택한 플러그 인을 활성화합니다.

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample14.html)]

다음 줄은 클래스 이름으로 DOM 요소를 선택 하는 jQuery 준비 함수를 호출 하는 구문을 `chzn-select`합니다.

[!code-powershell[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample15.ps1)]

선택한 메서드를 설정한 후 위의 호출에서 반환 되는 래핑된 적용 (`.chosen();`), 선택한 플러그 인 연결 하는입니다.

다음 코드에서는 완료 된 *Views\Home\MultiSelectCountry.cshtml* 파일 보기.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample16.cshtml)]

응용 프로그램을 실행 하 고 탐색 하는 `MultiSelectCountry` 보기. 추가 하는 시도 및 국가 삭제 합니다. 제공 된 샘플 다운로드도 포함 되어는 `MultiCountryVM` 메서드 및 보기는 보기를 사용 하 여 MultiSelectCountry 기능을 구현 하는 대신 모델을 **ViewBag**합니다.

다음 섹션에 표시 된 ASP.NET MVC 스 캐 폴딩 메커니즘의 작동 방식을 **DropDownList** 도우미입니다.

>[!div class="step-by-step"]
[다음](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
