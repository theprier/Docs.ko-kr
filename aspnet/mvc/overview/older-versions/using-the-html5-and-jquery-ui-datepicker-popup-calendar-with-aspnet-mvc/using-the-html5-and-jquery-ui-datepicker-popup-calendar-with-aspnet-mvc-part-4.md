---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: "ASP.NET MVC-4 부 HTML5 및 jQuery UI Datepicker 팝업 일정 사용 | Microsoft Docs"
author: Rick-Anderson
description: "이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MV에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: 2b76d2e449d491fd8d808343065b22ba267f1152
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a>ASP.NET MVC-4 부 HTML5 및 jQuery UI Datepicker 팝업 일정 사용
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다.


### <a name="adding-a-template-for-editing-dates"></a>날짜를 편집용 템플릿을 추가

이 섹션에서는 ASP.NET MVC로 표시 된 모델 속성을 편집 하기 위해 UI를 표시 하는 경우 적용 되는 날짜 편집에 대 한 템플릿을 만듭니다는 **날짜** 의 열거 된 [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) 특성이 있습니다. 서식 파일은 날짜만; 렌더링 합니다. 시간 표시 되지 않습니다. 템플릿을 사용 하 여는 [jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/) 팝업 달력 날짜 편집 하는 방법을 제공 합니다.

를 시작 하려면 열기는 *Movie.cs* 파일을 추가 [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성이 **날짜** 열거형을는 `ReleaseDate` 속성을 다음 코드에 나와 있는 것 처럼:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

이 코드는 `ReleaseDate` 둘 다의 시간과 템플릿을 표시 및 서식 파일을 편집 하지 않고 표시할 필드입니다. 응용 프로그램을 포함 하는 경우는 *date.cshtml* 에서 서식 파일은 *Views\Shared\EditorTemplates* 폴더 또는 *Views\Movies\EditorTemplates* 해당 서식 파일, 폴더 모든 렌더링에 사용 되는 `DateTime` 편집 하는 동안 속성입니다. 그렇지 않은 경우 기본 제공 ASP.NET 템플릿 시스템 날짜로 속성을 표시 합니다.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다. 릴리스 날짜에 대 한 입력된 필드는 날짜를 표시 하는지 확인 하려면 편집 링크를 선택 합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

**솔루션 탐색기**를 확장 하 고는 *뷰* 폴더를 확장 하 고는 *Shared* 폴더를 마우스 오른쪽 단추로 *Views\Shared\EditorTemplates* 폴더입니다.

클릭 **추가**, 클릭 하 고 **보기**합니다. **뷰 추가** 대화 상자가 표시 됩니다.

에 **뷰 이름** 상자에서 입력 &quot;날짜&quot;합니다.

선택 된 **부분 뷰로 만들기** 확인란 합니다. 다음 사항을 확인는 **레이아웃 또는 마스터 페이지를 사용 하 여** 및 **강력한 형식의 뷰 만들기** 확인란을 선택 하지 않은 합니다.

**추가**를 클릭합니다. *Views\Shared\EditorTemplates\Date.cshtml* 템플릿이 만들어집니다.

다음 코드를 추가 하는 *Views\Shared\EditorTemplates\Date.cshtml* 서식 파일입니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

첫 번째 줄은 선언 된 모델을는 `DateTime` 유형입니다. 편집에서 모델 형식을 선언 하 고 템플릿을 표시 하지 않아도, 이지만 가장 좋은 방법은 컴파일 타임을 받을 수 있도록 뷰에 전달 되 고 모델 검사를 수행 합니다. (또 다른 이점은 Visual Studio에서 보기에서 모델에 대 한 IntelliSense를 가져온 후.) 모델 형식, 선언 되지 않은 경우 ASP.NET MVC 간주 하는 [동적](https://msdn.microsoft.com/en-us/library/dd264741.aspx) 입력 하 고 컴파일 시간이 없습니다 형식 검사 합니다. 모델을 선언 하는 경우는 `DateTime` 유형, 강력 하 게 형식화 됩니다.

두 번째 줄은 표시 하는 HTML 태그 리터럴 &quot;날짜 템플릿을 사용 하 여&quot; 날짜 필드 앞입니다. 이 날짜 서식 파일 사용 되 고 있는지 확인 하려면이 줄을 일시적으로 사용 합니다.

다음 줄은는 [Html.TextBox](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.inputextensions.textbox.aspx) 렌더링 하는 도우미는 `input` 필드는 텍스트 상자가입니다. 도우미에 대 한 세 번째 매개 변수 익명 형식을 사용 하 여 텍스트 상자에 대 한 클래스를 설정 `datefield` 하 고 형식을 `date`합니다. (때문에 `class` 는 예약 되어 C#에서 사용 해야는 `@` 문자를 이스케이프 하는 `class` C# 파서에 특성입니다.)

`date` 형식은 HTML5 인식 브라우저는 HTML5 달력 컨트롤을 렌더링할 수 있도록 설정 하는 HTML5 입력된 형식입니다. 일부 JavaScript에 jQuery datepicker 후크를 나중에 추가 된 `Html.TextBox` 사용 하 여 요소는 `datefield` 클래스.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다. 중인지 확인할 수 있습니다는 `ReleaseDate` 템플릿을 표시 하기 때문에 편집 보기에서 속성 편집 템플릿을 사용 하 여는 &quot;날짜 템플릿을 사용 하 여&quot; 바로 앞의 `ReleaseDate` 이 이미지에 나와 있는 것 처럼 텍스트 입력 상자:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

브라우저에서 페이지의 소스를 봅니다. (예를 들어 페이지를 마우스 오른쪽 단추로 클릭 하 고 선택 **소스 보기**.) 다음 보여 주는 예제는 페이지에 대 한 태그 중 일부를 보여는 `class` 및 `type` 렌더링 된 html에서 특성입니다.

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

으로 돌아와서는 *Views\Shared\EditorTemplates\Date.cshtml* 템플릿과 제거는 &quot;날짜 템플릿을 사용 하 여&quot; 태그입니다. 이제 완료 된 서식 파일은 다음과 같습니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a>JQuery UI Datepicker 팝업 일정을 추가 합니다. NuGet을 사용 하 여

이 섹션에서는 추가 된 [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) 날짜 편집 템플릿에 팝업 일정입니다. [jQuery UI](http://jqueryui.com/) 라이브러리 효과 및 사용자 지정 가능한 위젯을 고급 애니메이션에 대 한 지원을 제공 합니다. JQuery JavaScript 라이브러리를 기반으로 만들어집니다. Datepicker 팝업 일정 사용 하면 쉽고 자연 스러운 일정을 사용 하는 문자열을 입력 하는 대신 날짜를 입력 합니다. 팝업 일정도 사용자가 법적 날짜 수를 제한-날짜에 대 한 일반 텍스트 항목 사용 같은 코드를 입력 하면 `2/33/1999` (2 월 33rd, 1999), 하지만 [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) 팝업 일정 작업을 허용 하지 않습니다.

먼저, jQuery UI 라이브러리를 설치 해야 합니다. 이렇게 하려면 Visual Studio 2010 및 Visual Web Developer의 SP1 버전에 포함 된 패키지 관리자 인 NuGet을 사용 합니다.

Visual Web developer에서에서 **도구** 메뉴 선택 **라이브러리 패키지 관리자** 선택한 후 **NuGet 패키지 관리**합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

참고: 경우는 **도구** 메뉴에 표시 되지 않습니다는 **라이브러리 패키지 관리자** 명령의 지침에 따라 NuGet을 설치 해야는 [NuGet 설치](http://docs.nuget.org/docs/start-here/installing-nuget) 페이지 NuGet 웹 사이트입니다.   
  
Visual Web Developer 대신 Visual Studio에서 사용 중인 경우는 **도구** 메뉴 선택 **라이브러리 패키지 관리자** 선택한 후 **라이브러리 패키지 참조 추가**합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

에 **MVCMovie-NuGet 패키지 관리** 대화 상자를 클릭는 **온라인** 왼쪽 탭 한 다음 입력 &quot;jQuery.UI&quot; 검색 상자에 합니다. J 선택 **쿼리 UI 위젯: Datepicker**을 선택한 후는 **설치** 단추입니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

NuGet을 프로젝트에 이러한 디버그 버전 및 jQuery UI 코어 및 jQuery UI 날짜 선택의 축소 된 버전을 추가합니다.

- *jquery.ui.core.js*
- *jquery.ui.core.min.js*
- *jquery.ui.datepicker.js*
- *jquery.ui.datepicker.min.js*

참고: 디버그 버전 (없이 파일의 *. min.js* 확장) 유용한 디버깅을 위해 있지만 프로덕션 사이트에 축소 된 버전에만 포함 합니다.

JQuery 날짜 선택을 실제로 사용 하려면 템플릿 편집을 달력 도구를 후크 할는 jQuery 스크립트를 만듭니다. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *스크립트* 폴더와 선택 **추가**, 다음 **새 항목**, 차례로 **JScript 파일**합니다. 파일 이름을 *DatePickerReady.js*합니다.

다음 코드를 추가 하는 *DatePickerReady.js* 파일:

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

JQuery 모르는 경우이 수행 하는 작업에 대 한 간략 한 설명이 있습니다: 첫 번째 줄은는 &quot;jQuery 준비&quot; 함수는 페이지의 모든 DOM 요소를 로드 했 때 호출 됩니다. 클래스 이름을 가진 모든 DOM 요소를 선택 하는 두 번째 줄 `datefield`, 다음 호출에서 `datepicker` 채 각 항목에 대 한 함수입니다. (추가 하는 `datefield` 클래스를 *Views\Shared\EditorTemplates\Date.cshtml* 자습서의 앞부분에 나오는 템플릿.)

을 열고는 *Views\Shared\\_Layout.cshtml* 파일입니다. 날짜 선택을 사용할 수 있도록 필요한 대로 모두 있는 다음 파일에 대 한 참조를 추가 해야 합니다.

- *Content/themes/base/jquery.ui.core.css*
- *Content/themes/base/jquery.ui.datepicker.css*
- *Content/themes/base/jquery.ui.theme.css*
- *jquery.ui.core.min.js*
- *jquery.ui.datepicker.min.js*
- *DatePickerReady.js*

다음 예제에서는 실제 코드의 맨 아래에 추가 해야 하는 `head` 요소에는 *Views\Shared\\_Layout.cshtml* 파일입니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

전체 `head` 섹션은 같습니다.:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

[URL 콘텐츠 도우미](https://msdn.microsoft.com/en-us/library/system.web.mvc.urlhelper.content.aspx) 메서드 리소스 경로 절대 경로로 변환 합니다. 사용 해야 `@URL.Content` 올바르게 응용 프로그램은 IIS에서 실행 되는 이러한 리소스를 참조 하도록 합니다.

Ctrl+F5를 눌러 응용 프로그램을 실행합니다. 편집 링크를 선택한 다음에 삽입 지점을 **ReleaseDate** 필드입니다. JQuery UI 팝업 일정 표시 됩니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

대부분의 jQuery 컨트롤과 마찬가지로 datepicker는 광범위 하 게 사용자 지정할 수 있습니다. 정보를 참조 하십시오. [시각적으로 사용자 지정: jQuery UI 테마 디자인](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) 에 [jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/) 사이트입니다.

### <a name="supporting-the-html5-date-input-control"></a>HTML5 날짜 입력된 제어를 지 원하는

브라우저는 HTML5 지원, 입력, 네이티브 HTML5 사용 하려면 합니다는 `date` 요소, 입력 및 jQuery UI 일정을 사용 하지 합니다. 브라우저가 지 원하는 경우 HTML5 컨트롤을 자동으로 사용 하도록 응용 프로그램에 논리를 추가할 수 있습니다. 이 위해의 내용을 바꿉니다는 *DatePickerReady.js* 다음 파일:

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

이 스크립트의 첫 번째 줄 Modernizr를 사용 하 여 HTML5 날짜 입력을 지원 하는지 확인 하십시오. 지원 되지 않는 경우 jQuery UI 날짜 선택 대신 연결 되어 있습니다. ([Modernizr](http://www.modernizr.com/docs/) 는 HTML5 및 CSS3의 네이티브 구현의 가용성을 검색 하는 오픈 소스 JavaScript 라이브러리. Modernizr은 만들면 새 ASP.NET MVC 프로젝트에 포함 됩니다.)

이 변경을 수행한 후에 HTML5 Opera 11 등을 지 원하는 브라우저를 사용 하 여 테스트할 수 있습니다. HTML5 호환 브라우저를 사용 하 여 응용 프로그램을 실행 하 고 동영상 항목을 편집 합니다. HTML5 날짜 컨트롤은 jQuery UI 팝업 일정 대신 사용 됩니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

새 버전의 브라우저를 구현 하는 HTML5 증분 때문에 광범위 한 HTML5 지원 제공 하는 웹 사이트에 코드를 추가 하는 좋은 방법은 지금은입니다. 예를 들어 더 강력한 *DatePickerReady.js* 스크립트는 부분적 으로만 HTML5 날짜 컨트롤을 지원 하 여 사이트 지원 브라우저 수 있는 다음과 같습니다.

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

이 스크립트는 HTML5 선택 `input` 형식의 요소 `date` HTML5 날짜 컨트롤을 완벽 하 게 지원 하지 않는 합니다. 이러한 요소에 대 한 jQuery UI 팝업 일정 연결 하는 것을를 수정한 다음는 `type` 에서 특성 `date` 를 `text`합니다. 변경 하 여는 `type` 에서 특성 `date` 를 `text`, 부분 HTML5 날짜 지원 제거 됩니다. 훨씬 더 강력한 *DatePickerReady.js* 스크립트에서 찾을 수 있습니다 [JSFIDDLE](http://jsfiddle.net/XSTK8/15/)합니다.

### <a name="adding-nullable-dates-to-the-templates"></a>Null 허용 날짜 서식 파일에 추가

기존 날짜 서식 파일 중 하나를 사용 하 여 null 날짜를 전달 하는 경우 런타임 오류가 얻게 됩니다. 날짜 서식 파일을 보다 강력 하려면 null 값을 처리 하도록 변경 합니다. Null을 허용 하는 날짜를 지원 하기 위해 변경의 코드는 *Views\Shared\DisplayTemplates\DateTime.cshtml* 다음과:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

모델은 빈 문자열을 반환 하는 코드 **null**합니다.

코드 변경의 *Views\Shared\EditorTemplates\Date.cshtml* 다음과 파일:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

이 코드를 실행할 때 모델이 null 인 경우 모델의 `DateTime` 값이 사용 됩니다. 모델이 null 인 경우 현재 날짜가 대신 사용 됩니다.

### <a name="wrapup"></a>Wrapup

이 자습서는 템플릿 기반 도우미 ASP.NET의 기본 사항을 검사가 수행 하 고 ASP.NET MVC 응용 프로그램에서 jQuery UI datepicker 팝업 일정을 사용 하는 방법을 보여 줍니다. 자세한 내용은 다음이 리소스를 참조 하십시오.

- 지역화에 대 한 내용은 Rajeesh의 블로그를 참조 [ASP.NET MVC에서 JQueryUI Datepicker](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/)합니다.
- JQuery UI에 대 한 정보를 참조 하십시오. [jQuery UI](http://docs.jquery.com/UI)합니다.
- Datepicker 컨트롤 지역화 하는 방법에 대 한 정보를 참조 하십시오. [UI/Datepicker/지역화](http://docs.jquery.com/UI/Datepicker/Localization)합니다.
- ASP.NET MVC 템플릿에 대 한 자세한 내용은 Brad Wilson의 블로그 시리즈에 참조 [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)합니다. 계열을 ASP.NET MVC 2 용으로 작성 된, 하지만 자료는 ASP.NET MVC의 최신 버전은 여전히 적용 됩니다.

>[!div class="step-by-step"]
[이전](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
