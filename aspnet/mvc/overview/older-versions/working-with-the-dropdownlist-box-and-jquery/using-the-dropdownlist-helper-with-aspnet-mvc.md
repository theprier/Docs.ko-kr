---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
title: ASP.NET MVC DropDownList 도우미 사용 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
ms.date: 01/12/2012
ms.assetid: 53767e05-c8ab-42e1-a94b-22d906195200
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 9f16c01515bde80d3994618d26818c2d93f69d87
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37828379"
---
<a name="using-the-dropdownlist-helper-with-aspnet-mvc"></a>ASP.NET MVC DropDownList 도우미 사용
====================
[Rick Anderson](https://github.com/Rick-Anderson)

이 자습서는 작업의 기본 사항을 설명 합니다 [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) 도우미 및 [ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) ASP.NET MVC 웹 응용 프로그램의 도우미입니다. Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 자습서를 수행 하려면 Microsoft Visual Studio의 무료 버전인를 사용할 수 있습니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다. 다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.

- [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack) <a id="post"></a>
- [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)

Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다. 이 자습서를 완료 했다고 가정 합니다 [ASP.NET MVC 소개](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서 또는[ASP.NET MVC Music Store](../mvc-music-store/mvc-music-store-part-1.md) 자습서 또는 익숙한 ASP.NET MVC 개발 합니다. 이 자습서에서 수정 된 프로젝트를 시작 합니다 [ASP.NET MVC Music Store](../mvc-music-store/mvc-music-store-part-1.md) 자습서입니다. 다음 링크를 사용 하 여 시작 프로젝트를 다운로드할 수 있습니다 [C# 버전 다운로드](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829)합니다.

완성된 된 자습서 C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다. [다운로드](https://code.msdn.microsoft.com/Using-the-DropDownList-67f9367d)합니다.

### <a name="what-youll-build"></a>만들 내용

작업 메서드와 뷰를 사용 하는 만들어야 합니다 [DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) 도우미 범주를 선택 합니다. 사용할 수도 있습니다 **jQuery** (예: 장르 또는 artist) 새 범주를 필요할 때 사용할 수 있는 insert 범주 대화 상자를 추가 합니다. 다음은 만들기 뷰는 새로운 장르를 추가 하 고 새 artist를 추가 하는 링크를 보여 주는 스크린샷입니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image1.png)

### <a name="skills-youll-learn"></a>학습할 기술

학습할 다음과 같습니다.

- 사용 하는 방법을 합니다 [DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) 범주 데이터를 선택 하는 도우미입니다.
- 추가 하는 방법을 **jQuery** 대화 새 범주를 추가 합니다.

### <a name="getting-started"></a>시작

다음 링크를 사용 하 여 시작 프로젝트를 다운로드 하 여 시작 [다운로드](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829)합니다. Windows 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 *DDL\_Starter.zip* 파일 및 속성을 선택 합니다. 에 **DDL\_Starter.zip 속성** 대화 상자에서 선택 차단 해제 합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image2.png)

DDL을 마우스 오른쪽 단추로 클릭\_Starter.zip 파일과 선택 **풀기** 파일 압축을 풀 합니다. 엽니다는 *StartMusicStore.sln* Visual Web Developer 2010 Express ("Visual Web Developer" 또는 줄여서 "VWD") 또는 Visual Studio 2010을 사용 하 여 파일입니다.

CTRL + f5를 눌러 응용 프로그램을 실행 하 고 클릭 합니다 **테스트** 링크 합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image3.png)

선택 된 **영화 범주 선택 (단순)** 링크 합니다. 코미디 선택한 값을 사용 하 여 동영상 형식 선택 목록이 표시 됩니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image4.png)

마우스 오른쪽 단추로 소스 보기를 선택한 브라우저를 클릭 합니다. HTML 페이지에 표시 됩니다. 아래 코드는 HTML select 요소를 보여 줍니다.

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample1.html)]

(작업에 대 한 0, 드라마에 대 한 1, 2 코미디 및 공상 과학에 대 한 3) 값 및 표시 이름 (작업, 드라마, 코미디 및 공상 과학) select 목록의 각 항목에 있는지 확인할 수 있습니다. 위의 코드에는 select 목록에 대 한 표준 HTML입니다.

드라마 및 적중 선택 목록 변경 합니다 **제출** 단추입니다. 브라우저에서 URL은 `http://localhost:2468/Home/CategoryChosen?MovieType=1` 페이지를 표시 하 고 **선택한: 1**합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image5.png)

엽니다는 *controllers\ homecontroller.cs* 파일을 검사 합니다 `SelectCategory` 메서드.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample2.cs)]

합니다 [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) 도우미는 HTML 선택 목록을 만드는 데 필요는 **IEnumerable&lt;SelectListItem &gt;** , 명시적 또는 암시적으로 합니다. 즉, 전달할 수 있습니다는 **IEnumerable&lt;SelectListItem &gt;**  명시적으로 [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) 도우미 하거나 추가할 수 있습니다 합니다 **IEnumerable&lt; SelectListItem &gt;**  에 [ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 에 대 한 동일한 이름을 사용 하는 **SelectListItem** 모델 속성으로. 전달 된 **SelectListItem** 자습서의 다음 부분에서는 암시적 및 명시적으로 설명 합니다. 위의 코드를 만드는 가장 간단한 가능한 방법을 보여 줍니다.는 **IEnumerable&lt;SelectListItem &gt;**  텍스트와 값으로 채웁니다. 참고 합니다 `Comedy` [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) 에 [선택한](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.selected.aspx) 속성이로 설정 **true;** 표시할 선택 목록 렌더링된 하면 **코미디** 목록에서 선택한 항목으로 합니다.

**IEnumerable&lt;SelectListItem &gt;**  생성 이상에 추가 되는 [ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) MovieType 이름의 합니다. 전달 하는 방법입니다 합니다 **IEnumerable&lt;SelectListItem &gt;**  암시적으로 [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) 도우미 아래에 표시 합니다.

엽니다는 *Views\Home\SelectCategory.cshtml* 파일과 태그를 검사 합니다.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample3.cshtml)]

레이아웃 Views/Shared로 설정에서는 세 번째 줄에서 /\_간단한\_Layout.cshtml는 표준 레이아웃 파일의 단순화 된 버전입니다. 표시 되도록이 작업을 수행 하 고 간단한 HTML을 렌더링 합니다.

이 샘플에서 변경 하 고 하지 응용 프로그램의 상태 데이터를 통해 전송 됩니다 있도록를 **HTTP GET**가 아닌 **HTTP POST**합니다. W3C 섹션을 참조 하세요 [선택 HTTP GET 또는 POST에 대 한 빠른 검사 목록](http://www.w3.org/2001/tag/doc/whenToUseGet.html#checklist)합니다. 응용 프로그램을 변경 하 고 양식을 게시 하지, 때문에 사용 된 [Html.BeginForm](https://msdn.microsoft.com/library/dd460344.aspx) 동작 메서드, 컨트롤러 및 폼 메서드를 지정할 수 있도록 하는 오버 로드 (**HTTP POST** 또는 **HTTP GET**). 일반적으로 뷰를 포함 합니다 [Html.BeginForm](https://msdn.microsoft.com/library/dd505244.aspx) 매개 변수가 없는 오버 로드 합니다. 매개 변수 버전이 없는 폼 데이터를 동일한 작업 메서드 및 컨트롤러의 POST 버전 게시 기본값으로 사용 됩니다.

다음 줄

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample4.cshtml)]

문자열 인수를 전달 합니다 **DropDownList** 도우미입니다. 이 문자열 "MovieType" 예제에서는 두 가지를 수행합니다.

- 에 대 한 키를 제공 합니다 **DropDownList** 찾으려고 도우미를 **IEnumerable&lt;SelectListItem &gt;**  에서 **ViewBag**.
- 이 데이터 바인딩된 MovieType 폼 요소입니다. 전송 메서드 이면 **HTTP GET**, `MovieType` 쿼리 문자열이 됩니다. 전송 메서드 이면 **HTTP POST**, `MovieType` 메시지 본문에 추가 됩니다. 다음 그림은 값 1 사용 하 여 쿼리 문자열을 보여 줍니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image6.png)

다음 코드에서는 `CategoryChosen` 메서드를 폼에 전송 되었습니다.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample5.cs)]

선택한 테스트 페이지로 다시 이동 합니다 **HTML SelectList** 링크 합니다. HTML 페이지 간단한 ASP.NET MVC 테스트 페이지와 마찬가지로 select 요소를 렌더링합니다. 브라우저 창을 마우스 오른쪽 단추로 클릭 하 고 선택 **소스 보기**합니다. Select 목록에 대 한 HTML 태그는 기본적으로 동일 합니다. HTML 테스트 페이지를 ASP.NET MVC 동작 메서드 및 뷰 이전에 테스트 처럼 작동 합니다.

### <a name="improving-the-movie-select-list-with-enums"></a>열거형을 사용 하 여 영화 선택 목록 개선

응용 프로그램의 범주 수정 바뀌지를 더욱 강력 하 고 간단 하 게 확장 코드를 쉽게 열거형 활용을 걸릴 수 있습니다. 새 범주를 추가할 때 올바른 범주 값이 생성 됩니다. 새 범주를 추가 하지만 범주 값을 업데이트 해야 하는 경우 복사 및 붙여넣기 오류를 방지 합니다.

엽니다는 *controllers\ homecontroller.cs* 파일을 다음 코드를 검사 합니다.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample6.cs)]

합니다 [enum](https://msdn.microsoft.com/library/sbbt4032(VS.80).aspx) `eMovieCategories` 4 개의 영화 형식을 캡처합니다. `SetViewBagMovieType` 메서드를 만듭니다 합니다 **IEnumerable&lt;SelectListItem &gt;**  에서 `eMovieCategories` **열거형**, 설정 및는 `Selected` 속성을 `selectedMovie` 매개 변수입니다. 합니다 `SelectCategoryEnum` 으로 동일한 뷰를 사용 하 여 동작 메서드는 `SelectCategory` 작업 메서드.

테스트 페이지를 탐색 하 고 클릭는 `Select Movie Category (Enum)` 링크 합니다. 이 이때 표시 되는 값 (숫자)을 대신 열거형을 나타내는 문자열로 표시 됩니다.

### <a name="posting-enum-values"></a>열거형 값을 게시

HTML 폼 게시 서버에 데이터를 일반적으로 사용 됩니다. 다음 코드에서는 합니다 `HTTP GET` 하 고 `HTTP POST` 버전의는 `SelectCategoryEnumPost` 메서드.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample7.cs)]

전달 하 여를 `eMovieCategories` 열거형을 `POST` 메서드, 열거형 값과 열거형 문자열을 추출할 수 있습니다. 샘플을 실행 하 고 시험 페이지까지 이동 합니다. 클릭 된 `Select Movie Category(Enum Post)` 링크 합니다. 영화 유형을 선택 하 고 전송 단추를 누릅니다. 표시 된 값과 영화 형식의 이름입니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image7.png)

### <a name="creating-a-multiple-section-select-element"></a>여러 섹션 선택 요소 만들기

합니다 [ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) HTML 도우미는 HTML 렌더링 `<select>` 사용 하 여 요소를 `multiple` 특성을 여러 개 선택할 수 있습니다. 테스트 링크를 이동한 다음 선택 합니다 **국가 선택 하는 다중** 링크 합니다. 렌더링 된 UI를 사용 하면 여러 국가 선택할 수 있습니다. 아래 이미지에서 캐나다 및 중국 선택 됩니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image8.png)

### <a name="examining-the-multiselectcountry-code"></a>MultiSelectCountry 코드 검사

다음 코드를 검토 합니다 *controllers\ homecontroller.cs* 파일입니다.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample8.cs)]

합니다 `GetCountries` 메서드 국가 목록을 만들어 다음에 전달 된 `MultiSelectList` 생성자입니다. 합니다 `MultiSelectList` 에 사용 되는 생성자 오버 로드는 `GetCountries` 위의 메서드는 4 개의 매개 변수:

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample9.cs)]

1. *항목*:를 [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) 목록의 항목을 포함 합니다. 목록 위의 예에서 국가.
2. *dataValueField*: 속성의 이름을 합니다 **IEnumerable** 값이 포함 된 목록입니다. 위의 예제는 `ID` 속성입니다.
3. *dataTextField*: 속성의 이름을 합니다 **IEnumerable** 표시할 정보를 포함 하는 목록입니다. 위의 예제는 `name` 속성입니다.
4. *selectedValues*: 선택한 값 목록입니다.

위의 예제는 `MultiSelectCountry` 메서드가 전달은 `null` 하므로 UI가 표시 되 면 없는 국가 선택은 선택된 된 국가 대 한 값입니다. 다음 코드에서는 Razor 태그를 렌더링 하는 데 사용 된 `MultiSelectCountry` 보기.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample10.cshtml)]

HTML 도우미 [ListBox](https://msdn.microsoft.com/library/dd470200.aspx) 두 매개 변수를 모델 바인딩할 속성의 이름을 위에 메서드 사용 하며 [MultiSelectList](https://msdn.microsoft.com/library/system.web.mvc.multiselectlist.aspx) 선택 옵션 및 값을 포함 하 합니다. `ViewBag.YouSelected` 위의 코드는 폼을 제출할 때 선택한 국가 값을 표시 하는 데 사용 됩니다. HTTP POST 오버 로드 확인은 `MultiSelectCountry` 메서드.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample11.cs)]

합니다 `ViewBag.YouSelected` 동적 속성에 대해 얻은, 선택한 국가 포함 합니다 `Countries` 폼 컬렉션의 항목입니다. GetCountries 메서드를 선택한 국가 목록의 전달 하는 데이 버전에서는 있으므로 `MultiSelectCountry` 뷰가 표시 됩니다, 선택된 된 국가 UI에서 선택 됩니다.

### <a name="making-a-select-element-friendly-with-the-harvest-chosen-jquery-plugin"></a>선택 요소 친숙 한 Harvest 선택한 jQuery 플러그 인을 사용 하 여 만들기

Harvest [선택한](http://harvesthq.github.com/chosen/) HTML에 jQuery 플러그 인을 추가할 수 있습니다 &lt;선택&gt; 사용자를 만들려면 요소 친숙 한 UI입니다. 아래 이미지는 Harvest 보여 [선택한](http://harvesthq.github.com/chosen/) jQuery 플러그 인 `MultiSelectCountry` 보기.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image9.png)

두 이미지 아래에서 **캐나다** 을 선택 합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image10.png)

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image11.png)

위의 이미지에서 캐나다를 선택 하 고 포함 하는 **x** 선택 항목을 제거 하기 위해 클릭할 수 있습니다. 아래 이미지는 캐나다, 중국, 나타나며 일본 선택 합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image12.png)

### <a name="hooking-up-the-harvest-chosen-jquery-plugin"></a>Harvest 선택한 jQuery 플러그 인 연결

다음 섹션은 jQuery 사용한 경험이 있는 경우에 따라 하기 더 쉽습니다. 전에 jQuery를 사용한 적이 없는,를 사용 하는 경우에 다음 jQuery 자습서 중 하나를 시도 합니다.

- [JQuery의 작동 원리](http://docs.jquery.com/Tutorials:How_jQuery_Works) 여 [John Resig](http://ejohn.org/)
- [JQuery를 사용 하 여 시작](http://docs.jquery.com/Tutorials:Getting_Started_with_jQuery) 여 [Jörn Zaefferer](http://bassistance.de/)
- [JQuery 예가 live](http://codylindley.com/blogstuff/js/jquery/#) 여 [Cody Lindley](http://codylindley.com/)

선택한 플러그 인을 시작 하 고이 자습서와 함께 제공 되는 완성 된 샘플 프로젝트에 포함 됩니다. 이 자습서는 jQuery UI를 후크 하는 데만 해야 합니다. ASP.NET MVC 프로젝트에서 Harvest 선택한 jQuery 플러그 인을 사용 하려면 다음을 수행 해야 합니다.

1. 선택한 플러그 인을 다운로드 [github](https://github.com/harvesthq/chosen/)합니다. 이 단계는 수행 된 것입니다.
2. 선택한 폴더를 ASP.NET MVC 프로젝트를 추가 합니다. 선택한 폴더에 이전 단계에서 다운로드 하 여 선택한 플러그 인에서 자산을 추가 합니다. 이 단계는 수행 된 것입니다.
3. 선택한 플러그 인을 연결 합니다 **DropDownList** 하거나 **ListBox** HTML 도우미입니다.

### <a name="hooking-up-the-chosen-plugin-to-the-multiselectcountry-view"></a>MultiSelectCountry 보기로 선택한 플러그 인을 연결 합니다.

열기를 *Views\Home\MultiSelectCountry.cshtml* 파일을 추가 `htmlAttributes` 매개 변수는 `Html.ListBox`합니다. 추가 매개 변수 선택 목록에 대 한 클래스 이름을 포함 (`@class = "chzn-select"`). 완료 된 코드는 다음과 같습니다.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample12.cshtml)]

위의 코드에서 추가 HTML 특성 및 특성 값 `class = "chzn-select"`합니다. @ 문자 앞에 클래스는 관련이 Razor 보기 엔진을 사용 하 여 합니다. `class` [C# 키워드](https://msdn.microsoft.com/library/x53a06bb.aspx)합니다. 접두사로 @을 포함 하지 않는 한 C# 키워드를 식별자로 사용할 수 없습니다. 위의 예에서 `@class` 올바른 식별자가 있지만 **클래스** 아니므로 **클래스** 는 키워드입니다.

에 대 한 참조를 추가 합니다 *Chosen/chosen.jquery.js* 하 고 *Chosen/chosen.css* 파일입니다. 합니다 *Chosen/chosen.jquery.js* 구현 및는 기능적의 선택한 플러그 인입니다. 합니다 *Chosen/chosen.css* 파일은 스타일을 제공 합니다. 맨 아래에 다음이 참조를 추가 합니다 *Views\Home\MultiSelectCountry.cshtml* 파일입니다. 다음 코드에는 선택한 플러그 인을 참조 하는 방법을 보여 줍니다.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample13.cshtml)]

에 사용 되는 클래스 이름을 사용 하 여 선택한 플러그 인을 활성화 합니다 **Html.ListBox** 코드입니다. 위의 예제에서 클래스 이름은 `chzn-select`합니다. 맨 아래에 다음 줄을 추가 합니다 *Views\Home\MultiSelectCountry.cshtml* 파일 보기. 이 줄은 선택한 플러그 인을 활성화합니다.

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample14.html)]

다음 줄은 클래스 이름으로 DOM 요소를 선택 하는 jQuery 준비 함수를 호출 하는 구문은 `chzn-select`합니다.

[!code-powershell[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample15.ps1)]

선택한 메서드를 래핑된 다음 위의 호출에서 반환 된 설정 적용 (`.chosen();`), 선택한 플러그 인을 연결 하는 합니다.

다음 코드를 보여줍니다 *Views\Home\MultiSelectCountry.cshtml* 파일 보기.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample16.cshtml)]

응용 프로그램을 실행 하 고 이동 된 `MultiSelectCountry` 보기. 추가 하거나 국가 삭제 합니다. 제공 된 샘플 다운로드도 포함 되어 있습니다를 `MultiCountryVM` 메서드 및 보기는 보기를 사용 하 여 MultiSelectCountry 기능을 구현 하는 대신 모델을 **ViewBag**합니다.

다음 섹션에 표시 된 ASP.NET MVC 스 캐 폴딩 메커니즘의 작동 방식을 합니다 **DropDownList** 도우미입니다.

> [!div class="step-by-step"]
> [다음](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
