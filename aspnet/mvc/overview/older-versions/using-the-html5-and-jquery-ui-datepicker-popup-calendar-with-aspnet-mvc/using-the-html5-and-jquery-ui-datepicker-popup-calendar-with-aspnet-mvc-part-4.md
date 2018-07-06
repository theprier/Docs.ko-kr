---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: ASP.NET MVC-4 부에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker 팝업 일정을 ASP.NET MV에서 사용 하는 방법의 기본 사항을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 08/29/2011
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: d50ce517df9bd834203cbd026d31db038cd02038
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835734"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a>ASP.NET MVC-4 부에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서는 편집기 템플릿, 표시 템플릿 및 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정을 사용 하는 방법의 기본 사항을 설명 합니다.


### <a name="adding-a-template-for-editing-dates"></a>날짜를 편집 하기 위한 템플릿 추가

이 섹션에서는 ASP.NET MVC로 표시 되는 모델 속성을 편집 하는 것에 대 한 UI를 표시 하는 경우 적용 되는 날짜를 편집 하는 것에 대 한 템플릿을 만듭니다는 **날짜** 열거를 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성입니다. 템플릿을 날짜만; 렌더링 시간 표시 되지 않습니다. 템플릿에서 사용 된 [jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/) 팝업 달력 날짜를 편집 하는 방법을 제공 합니다.

시작 하려면를 엽니다는 *Movie.cs* 파일을 추가 합니다 [데이터 형식](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성을 **날짜** 열거형을는 `ReleaseDate` 속성을 다음 코드 에서처럼:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

이 코드는 `ReleaseDate` 모두에 템플릿을 표시 및 서식 파일을 편집 하지 않고 표시할 필드입니다. 응용 프로그램을 포함 하는 경우는 *date.cshtml* 에서 서식 파일을 *Views\Shared\EditorTemplates* 폴더 또는 *Views\Movies\EditorTemplates* 폴더에서 해당 템플릿을 모든 렌더링 하는 데 사용할 `DateTime` 편집 하는 동안 속성입니다. 그렇지 않은 경우 기본 제공 ASP.NET 템플릿 시스템 날짜로 속성이 표시 됩니다.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다. 릴리스 날짜에 대 한 입력된 필드는 날짜만 표시 확인에 대 한 편집 링크를 선택 합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

**솔루션 탐색기**, 확장를 *뷰* 폴더를 확장 합니다 *공유* 폴더 및 마우스 오른쪽 단추로 *Views\Shared\EditorTemplates* 폴더입니다.

클릭 **추가**를 클릭 하 고 **보기**합니다. 합니다 **뷰 추가** 대화 상자가 표시 됩니다.

에 **뷰 이름** 상자에 입력 &quot;날짜&quot;합니다.

선택 된 **부분 뷰로 만들기** 확인란 합니다. 있는지 확인 합니다 **레이아웃 또는 마스터 페이지를 사용** 및 **강력한 형식의 뷰를 만들** 확인란을 선택 하지 않은 합니다.

**추가**를 클릭합니다. 합니다 *Views\Shared\EditorTemplates\Date.cshtml* 템플릿이 만들어집니다.

다음 코드를 추가 합니다 *Views\Shared\EditorTemplates\Date.cshtml* 템플릿.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

모델을 선언 하는 첫 번째 줄을 `DateTime` 형식입니다. 컴파일 시간을 받을 수 있도록 모범 사례는 편집에서 모델 형식을 선언 하 고 템플릿을 표시 하려면 필요가 있지만 보기에 전달 되는 모델을 검사 합니다. (다른 혜택은 Visual Studio에서 보기에서 모델에 대 한 IntelliSense를 가져올 다음.) ASP.NET MVC 모델 형식을 선언 되지 않으면 간주는 [동적](https://msdn.microsoft.com/library/dd264741.aspx) 입력 이며 없는 컴파일 타임 형식 검사 합니다. 모델을 선언 하는 경우는 `DateTime` 형식 강력 하 게 형식화 됩니다.

두 번째 줄은 표시 하는 HTML 태그를 리터럴 &quot;날짜 템플릿을 사용 하 여&quot; 날짜 필드를 전 합니다. 이 날짜 서식 파일 사용 되 고 있는지 확인 하려면이 줄을 일시적으로 사용 합니다.

다음 줄은는 [Html.TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx) 렌더링 하는 도우미는 `input` 필드 텍스트 상자에 있습니다. 도우미의 세 번째 매개 변수가 무명 형식을 사용 하 여 텍스트 상자에 대 한 클래스를 설정 `datefield` 하 고 형식을 `date`합니다. (때문에 `class` 는 예약 된 C#에서 사용 해야 합니다 `@` 이스케이프 문자는 `class` C# 파서는 특성.)

`date` 형식은 HTML5 인식 브라우저는 HTML5 달력 컨트롤을 렌더링할 수 있도록 설정 하는 HTML5 입력된 형식입니다. 나중에 JavaScript를 jQuery datepicker 후크를 추가 합니다 `Html.TextBox` 사용 하 여 요소를 `datefield` 클래스.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다. 중인지 확인할 수 있습니다 합니다 `ReleaseDate` 템플릿을 표시 하기 때문에 편집 보기에서 속성 편집 템플릿을 사용 하 여는 &quot;날짜 템플릿을 사용 하 여&quot; 직전를 `ReleaseDate` 이 이미지에 표시 된 대로 텍스트 입력 상자에서:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

브라우저에서 페이지의 소스를 봅니다. (예를 들어, 페이지를 마우스 오른쪽 단추로 클릭 하 고 선택 **소스 보기**.) 다음 예와 페이지에 대 한 태그 중 일부를 보여 주는 합니다 `class` 및 `type` 렌더링된 된 HTML 특성입니다.

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

반환 합니다 *Views\Shared\EditorTemplates\Date.cshtml* 템플릿과 제거는 &quot;날짜 템플릿을 사용 하 여&quot; 태그입니다. 이제 완료 된 서식 파일은 다음과 같습니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a>JQuery UI Datepicker 팝업 일정 추가 NuGet을 사용 하 여

이 섹션에서는 추가 합니다 [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) 날짜 편집 템플릿에 팝업 달력입니다. 합니다 [jQuery UI](http://jqueryui.com/) 라이브러리 효과 및 사용자 지정 가능한 위젯 고급 애니메이션에 대 한 지원을 제공 합니다. 이 jQuery JavaScript 라이브러리를 기반으로 구축 됩니다. Datepicker 팝업 일정 사용 하면 쉽고 자연스럽 게 일정을 사용 하 여 문자열을 입력 하는 대신 날짜를 입력 합니다. 팝업 달력에는 또한 사용자가 올바른 날짜 제한-같은 코드를 입력 날짜에 대 한 일반 텍스트 항목 수 `2/33/1999` (2 월 33rd, 1999), 하지만 [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) 팝업 달력은 허용 되지 않습니다.

먼저, jQuery UI 라이브러리를 설치 해야 합니다. 이렇게 하려면 SP1 버전의 Visual Studio 2010 및 Visual Web Developer에 포함 된 패키지 관리자 인 NuGet을 사용 합니다.

Visual Web developer에서에서 합니다 **도구** 메뉴에서 **라이브러리 패키지 관리자** 선택한 후 **NuGet 패키지 관리**합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

참고: 경우는 **도구** 메뉴를 표시 하지 않습니다는 **라이브러리 패키지 관리자** 명령, 지시에 따라 NuGet을 설치 해야 합니다 [NuGet 설치](http://docs.nuget.org/docs/start-here/installing-nuget) 페이지 NuGet 웹 사이트입니다.   
  
Visual Web Developer에서 대신 Visual Studio에서 사용 중인 경우는 **도구** 메뉴에서 **라이브러리 패키지 관리자** 선택한 후 **라이브러리 패키지 참조 추가**합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

에 **MVCMovie-NuGet 패키지 관리** 대화 상자에서 클릭 합니다 **온라인** 왼쪽에 탭 하 고 enter &quot;jQuery.UI&quot; 검색 상자에 합니다. J 선택 **쿼리 UI 위젯: Datepicker**를 선택 하 고는 **설치** 단추입니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

NuGet은 프로젝트에 이러한 디버그 버전 및 jQuery UI 코어 및 jQuery UI 날짜 선택의 축소 된 버전을 추가합니다.

- *jquery.ui.core.js*
- *jquery.ui.core.min.js*
- *jquery.ui.datepicker.js*
- *jquery.ui.datepicker.min.js*

참고: 디버그 버전 (없이 파일을 *. min.js* 확장) 유용 디버깅용 하지만 프로덕션 사이트에서 축소 된 버전에만 포함 합니다.

JQuery 날짜 선택기를 실제로 사용 하려면 템플릿 편집에 달력 위젯을 후크는 jQuery 스크립트를 만드는 해야 합니다. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *스크립트* 폴더를 선택 **추가**, 다음 **새 항목**를 차례로 **JScript 파일**합니다. 파일 이름을 *DatePickerReady.js*합니다.

다음 코드를 추가 합니다 *DatePickerReady.js* 파일:

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

JQuery를 사용 하 여 잘 모르는 경우이 기능에 대해 간략히 설명 같습니다: 첫 번째 줄은는 &quot;jQuery ready&quot; 페이지의 모든 DOM 요소를 로드 하는 때 호출 되는 함수입니다. 클래스 이름을 가진 모든 DOM 요소를 선택 하는 두 번째 줄 `datefield`, 다음 호출을 `datepicker` 각각에 대 한 함수입니다. (추가한 기억 합니다 `datefield` 클래스를 *Views\Shared\EditorTemplates\Date.cshtml* 자습서의 앞부분에 나오는 템플릿.)

다음으로 열고 합니다 *Views\Shared\\_Layout.cshtml* 파일입니다. 날짜 선택기를 사용할 수 있도록 필요한 모든는 다음 파일에 대 한 참조를 추가 해야 합니다.

- *Content/themes/base/jquery.ui.core.css*
- *Content/themes/base/jquery.ui.datepicker.css*
- *Content/themes/base/jquery.ui.theme.css*
- *jquery.ui.core.min.js*
- *jquery.ui.datepicker.min.js*
- *DatePickerReady.js*

다음 예제에서는 실제 코드의 맨 아래에 추가 해야 합니다 `head` 요소에는 *Views\Shared\\_Layout.cshtml* 파일입니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

전체 `head` 섹션은 다음과 같습니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

합니다 [URL 콘텐츠 도우미](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx) 메서드는 리소스 경로를 절대 경로로 변환 합니다. 사용 해야 `@URL.Content` 올바르게 응용 프로그램은 IIS에서 실행 중인 경우 이러한 리소스를 참조 합니다.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다. 편집 링크를 선택한 다음에 삽입 포인터를 **ReleaseDate** 필드입니다. JQuery UI 팝업 일정 표시 됩니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

대부분의 jQuery 컨트롤과 마찬가지로 datepicker 광범위 하 게 사용자 지정할 수 있습니다. 정보를 참조 하세요. [시각적으로 사용자 지정: jQuery UI 테마 디자인](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) 에 [jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/) 사이트입니다.

### <a name="supporting-the-html5-date-input-control"></a>HTML5 날짜 입력된 제어를 지원합니다.

입력와 같은 네이티브 HTML5를 사용 하려는 더 많은 브라우저가 HTML5 지원는 `date` 요소, 입력 및 jQuery UI 일정을 사용 하지. 자동으로 브라우저를 지 원하는 경우 HTML5 컨트롤을 사용 하도록 응용 프로그램 논리를 추가할 수 있습니다. 이 위해의 내용을 대체 합니다 *DatePickerReady.js* 다음을 사용 하 여 파일:

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

이 스크립트의 첫 번째 줄 Modernizr를 사용 하 여 HTML5 날짜 입력을 지원 하는지 확인 합니다. 지원 되지 않는 경우 jQuery UI 날짜 선택 대신 연결 됩니다. ([Modernizr](http://www.modernizr.com/docs/) 는 HTML5 및 CSS3의 네이티브 구현의 가용성을 검색 하는 오픈 소스 JavaScript 라이브러리입니다. Modernizr 사용자가 만든 모든 새로운 ASP.NET MVC 프로젝트에 포함 됩니다.)

이 변경을 완료 한 후에 Opera 11 같은 HTML5를 지 원하는 브라우저를 사용 하 여 테스트할 수 있습니다. HTML5 호환 브라우저를 사용 하 여 응용 프로그램을 실행 하 고 동영상 항목을 편집 합니다. HTML5 날짜 컨트롤은 jQuery UI 팝업 일정 대신 사용 됩니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

새 버전의 브라우저를 구현 하는 HTML5 증분 지금은 좋은 방법 이므로 다양 한 HTML5 지원을 수용 하는 웹 사이트에 코드를 추가 합니다. 예를 들어 있는 더 강력한 *DatePickerReady.js* 스크립트는 부분적 으로만 HTML5 날짜 컨트롤을 지 원하는 사이트 지원 브라우저 수 있도록 하는 다음과 같습니다.

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

이 스크립트 선택 HTML5 `input` 유형 요소의 `date` HTML5 날짜 컨트롤을 완전히 지원 하지 않는 합니다. 이러한 요소에 대 한 jQuery UI 팝업 일정을 연결 하 고 그런 다음 변경 합니다 `type` 에서 특성 `date` 에 `text`입니다. 변경 하 여 합니다 `type` 에서 특성 `date` 에 `text`, 부분 HTML5 날짜 지원 제거 됩니다. 더욱 강력한 *DatePickerReady.js* 스크립트에서 찾을 수 있습니다 [JSFIDDLE](http://jsfiddle.net/XSTK8/15/)합니다.

### <a name="adding-nullable-dates-to-the-templates"></a>Nullable 날짜 템플릿을 추가

기존 날짜 템플릿 중 하나를 사용 하 고 null 날짜를 전달 하는 경우 런타임 오류가 표시 됩니다. 날짜 서식 파일을 보다 강력 하 게 하려면 null 값을 처리 하는 데를 변경할 수 있습니다. Nullable이 날짜를 지원 하려면에서 코드를 변경 합니다 *Views\Shared\DisplayTemplates\DateTime.cshtml* 다음과:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

코드 모델 이면 빈 문자열이 반환 **null**합니다.

코드를 변경 합니다 *Views\Shared\EditorTemplates\Date.cshtml* 다음 파일:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

이 코드를 실행 하면 모델에서 null이 아닌 경우 모델의 `DateTime` 값이 사용 됩니다. 모델이 null 인 경우 현재 날짜가 대신 사용 됩니다.

### <a name="wrapup"></a>Wrapup

이 자습서는 ASP.NET 템플릿 기반 도우미는 기본적인 방법을 설명 했습니다 하 고 ASP.NET MVC 응용 프로그램에서 jQuery UI datepicker 팝업 일정을 사용 하는 방법을 보여 줍니다. 자세한 내용은 다음이 리소스를 참조 하십시오.

- 지역화에 대 한 내용은 Rajeesh의 블로그를 참조 하세요 [ASP.NET MVC에서 JQueryUI Datepicker](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/)합니다.
- JQuery UI에 대 한 정보를 참조 하세요 [jQuery UI](http://docs.jquery.com/UI)합니다.
- Datepicker 컨트롤을 지역화 하는 방법에 대 한 정보를 참조 하세요 [지역화Datepicker/UI/](http://docs.jquery.com/UI/Datepicker/Localization)합니다.
- ASP.NET MVC 템플릿에 대 한 자세한 내용은 Brad Wilson의 블로그 시리즈에서 참조 하세요 [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)합니다. 시리즈는 ASP.NET MVC 2 용으로 작성 되었지만, 자료는 ASP.NET MVC의 최신 버전은 계속 적용 됩니다.

> [!div class="step-by-step"]
> [이전](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
