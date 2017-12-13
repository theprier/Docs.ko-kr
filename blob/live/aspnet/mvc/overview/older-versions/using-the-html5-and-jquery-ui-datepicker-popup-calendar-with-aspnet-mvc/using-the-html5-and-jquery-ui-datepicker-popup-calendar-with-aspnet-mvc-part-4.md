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
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a><span data-ttu-id="f7859-103">ASP.NET MVC-4 부 HTML5 및 jQuery UI Datepicker 팝업 일정 사용</span><span class="sxs-lookup"><span data-stu-id="f7859-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 4</span></span>
====================
<span data-ttu-id="f7859-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="f7859-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="f7859-105">이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>


### <a name="adding-a-template-for-editing-dates"></a><span data-ttu-id="f7859-106">날짜를 편집용 템플릿을 추가</span><span class="sxs-lookup"><span data-stu-id="f7859-106">Adding a Template for Editing Dates</span></span>

<span data-ttu-id="f7859-107">이 섹션에서는 ASP.NET MVC로 표시 된 모델 속성을 편집 하기 위해 UI를 표시 하는 경우 적용 되는 날짜 편집에 대 한 템플릿을 만듭니다는 **날짜** 의 열거 된 [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-107">In this section you'll create a template for editing dates that will be applied when ASP.NET MVC displays UI for editing model properties that are marked with the **Date** enumeration of the [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) attibute.</span></span> <span data-ttu-id="f7859-108">서식 파일은 날짜만; 렌더링 합니다. 시간 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-108">The template will render only the date; time will not be displayed.</span></span> <span data-ttu-id="f7859-109">템플릿을 사용 하 여는 [jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/) 팝업 달력 날짜 편집 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-109">In the template you'll use the [jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to provide a way to edit dates.</span></span>

<span data-ttu-id="f7859-110">를 시작 하려면 열기는 *Movie.cs* 파일을 추가 [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성이 **날짜** 열거형을는 `ReleaseDate` 속성을 다음 코드에 나와 있는 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="f7859-110">To begin, open the *Movie.cs* file and add the [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute with the **Date** enumeration to the `ReleaseDate` property, as shown in the following code:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

<span data-ttu-id="f7859-111">이 코드는 `ReleaseDate` 둘 다의 시간과 템플릿을 표시 및 서식 파일을 편집 하지 않고 표시할 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-111">This code causes the `ReleaseDate` field to be displayed without the time in both display templates and edit templates.</span></span> <span data-ttu-id="f7859-112">응용 프로그램을 포함 하는 경우는 *date.cshtml* 에서 서식 파일은 *Views\Shared\EditorTemplates* 폴더 또는 *Views\Movies\EditorTemplates* 해당 서식 파일, 폴더 모든 렌더링에 사용 되는 `DateTime` 편집 하는 동안 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-112">If your application contains a *date.cshtml* template in the *Views\Shared\EditorTemplates* folder or in the *Views\Movies\EditorTemplates* folder, that template will be used to render any `DateTime` property while editing.</span></span> <span data-ttu-id="f7859-113">그렇지 않은 경우 기본 제공 ASP.NET 템플릿 시스템 날짜로 속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-113">Otherwise the built-in ASP.NET templating system will display the property as a date.</span></span>

<span data-ttu-id="f7859-114">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-114">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="f7859-115">릴리스 날짜에 대 한 입력된 필드는 날짜를 표시 하는지 확인 하려면 편집 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-115">Select an edit link to verify that the input field for the release date is showing only the date.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

<span data-ttu-id="f7859-116">**솔루션 탐색기**를 확장 하 고는 *뷰* 폴더를 확장 하 고는 *Shared* 폴더를 마우스 오른쪽 단추로 *Views\Shared\EditorTemplates* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-116">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\EditorTemplates* folder.</span></span>

<span data-ttu-id="f7859-117">클릭 **추가**, 클릭 하 고 **보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-117">Click **Add**, and then click **View**.</span></span> <span data-ttu-id="f7859-118">**뷰 추가** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-118">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="f7859-119">에 **뷰 이름** 상자에서 입력 &quot;날짜&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-119">In the **View name** box, type &quot;Date&quot;.</span></span>

<span data-ttu-id="f7859-120">선택 된 **부분 뷰로 만들기** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-120">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="f7859-121">다음 사항을 확인는 **레이아웃 또는 마스터 페이지를 사용 하 여** 및 **강력한 형식의 뷰 만들기** 확인란을 선택 하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-121">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

<span data-ttu-id="f7859-122">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-122">Click **Add**.</span></span> <span data-ttu-id="f7859-123">*Views\Shared\EditorTemplates\Date.cshtml* 템플릿이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-123">The *Views\Shared\EditorTemplates\Date.cshtml* template is created.</span></span>

<span data-ttu-id="f7859-124">다음 코드를 추가 하는 *Views\Shared\EditorTemplates\Date.cshtml* 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-124">Add the following code to the *Views\Shared\EditorTemplates\Date.cshtml* template.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

<span data-ttu-id="f7859-125">첫 번째 줄은 선언 된 모델을는 `DateTime` 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-125">The first line declares the model to be a `DateTime` type.</span></span> <span data-ttu-id="f7859-126">편집에서 모델 형식을 선언 하 고 템플릿을 표시 하지 않아도, 이지만 가장 좋은 방법은 컴파일 타임을 받을 수 있도록 뷰에 전달 되 고 모델 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-126">Although you don't need to declare the model type in edit and display templates, it's a best practice so that you get compile-time checking of the model being passed to the view.</span></span> <span data-ttu-id="f7859-127">(또 다른 이점은 Visual Studio에서 보기에서 모델에 대 한 IntelliSense를 가져온 후.) 모델 형식, 선언 되지 않은 경우 ASP.NET MVC 간주 하는 [동적](https://msdn.microsoft.com/en-us/library/dd264741.aspx) 입력 하 고 컴파일 시간이 없습니다 형식 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-127">(Another benefit is that you then get IntelliSense for the model in the view in Visual Studio.) If the model type is not declared, ASP.NET MVC considers it a [dynamic](https://msdn.microsoft.com/en-us/library/dd264741.aspx) type and there's no compile-time type checking.</span></span> <span data-ttu-id="f7859-128">모델을 선언 하는 경우는 `DateTime` 유형, 강력 하 게 형식화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-128">If you declare the model to be a `DateTime` type, it becomes strongly typed.</span></span>

<span data-ttu-id="f7859-129">두 번째 줄은 표시 하는 HTML 태그 리터럴 &quot;날짜 템플릿을 사용 하 여&quot; 날짜 필드 앞입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-129">The second line is just literal HTML markup that displays &quot;Using Date Template&quot; before a date field.</span></span> <span data-ttu-id="f7859-130">이 날짜 서식 파일 사용 되 고 있는지 확인 하려면이 줄을 일시적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-130">You'll use this line temporarily to verify that this date template is being used.</span></span>

<span data-ttu-id="f7859-131">다음 줄은는 [Html.TextBox](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.inputextensions.textbox.aspx) 렌더링 하는 도우미는 `input` 필드는 텍스트 상자가입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-131">The next line is an [Html.TextBox](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.inputextensions.textbox.aspx) helper that renders an `input` field that's a text box.</span></span> <span data-ttu-id="f7859-132">도우미에 대 한 세 번째 매개 변수 익명 형식을 사용 하 여 텍스트 상자에 대 한 클래스를 설정 `datefield` 하 고 형식을 `date`합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-132">The third parameter for the helper uses an anonymous type to set the class for the text box to `datefield` and the type to `date`.</span></span> <span data-ttu-id="f7859-133">(때문에 `class` 는 예약 되어 C#에서 사용 해야는 `@` 문자를 이스케이프 하는 `class` C# 파서에 특성입니다.)</span><span class="sxs-lookup"><span data-stu-id="f7859-133">(Because `class` is a reserved in C#, you need to use the `@` character to escape the `class` attribute in the C# parser.)</span></span>

<span data-ttu-id="f7859-134">`date` 형식은 HTML5 인식 브라우저는 HTML5 달력 컨트롤을 렌더링할 수 있도록 설정 하는 HTML5 입력된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-134">The `date` type is an HTML5 input type that enables HTML5-aware browsers to render a HTML5 calendar control.</span></span> <span data-ttu-id="f7859-135">일부 JavaScript에 jQuery datepicker 후크를 나중에 추가 된 `Html.TextBox` 사용 하 여 요소는 `datefield` 클래스.</span><span class="sxs-lookup"><span data-stu-id="f7859-135">Later on you'll add some JavaScript to hook up the jQuery datepicker to the `Html.TextBox` element using the `datefield` class.</span></span>

<span data-ttu-id="f7859-136">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-136">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="f7859-137">중인지 확인할 수 있습니다는 `ReleaseDate` 템플릿을 표시 하기 때문에 편집 보기에서 속성 편집 템플릿을 사용 하 여는 &quot;날짜 템플릿을 사용 하 여&quot; 바로 앞의 `ReleaseDate` 이 이미지에 나와 있는 것 처럼 텍스트 입력 상자:</span><span class="sxs-lookup"><span data-stu-id="f7859-137">You can verify that the `ReleaseDate` property in the edit view is using the edit template because the template displays &quot;Using Date Template&quot; just before the `ReleaseDate` text input box, as shown in this image:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

<span data-ttu-id="f7859-138">브라우저에서 페이지의 소스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-138">In your browser, view the source of the page.</span></span> <span data-ttu-id="f7859-139">(예를 들어 페이지를 마우스 오른쪽 단추로 클릭 하 고 선택 **소스 보기**.) 다음 보여 주는 예제는 페이지에 대 한 태그 중 일부를 보여는 `class` 및 `type` 렌더링 된 html에서 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-139">(For example, right-click the page and select **View source**.) The following example shows some of the markup for the page, illustrating the `class` and `type` attributes in the rendered HTML.</span></span>

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

<span data-ttu-id="f7859-140">으로 돌아와서는 *Views\Shared\EditorTemplates\Date.cshtml* 템플릿과 제거는 &quot;날짜 템플릿을 사용 하 여&quot; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-140">Return to the *Views\Shared\EditorTemplates\Date.cshtml* template and remove the &quot;Using Date Template&quot; markup.</span></span> <span data-ttu-id="f7859-141">이제 완료 된 서식 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-141">Now the completed template looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a><span data-ttu-id="f7859-142">JQuery UI Datepicker 팝업 일정을 추가 합니다. NuGet을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f7859-142">Adding a jQuery UI Datepicker Popup Calendar using NuGet</span></span>

<span data-ttu-id="f7859-143">이 섹션에서는 추가 된 [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) 날짜 편집 템플릿에 팝업 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-143">In this section you'll add the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to the date-edit template.</span></span> <span data-ttu-id="f7859-144">[jQuery UI](http://jqueryui.com/) 라이브러리 효과 및 사용자 지정 가능한 위젯을 고급 애니메이션에 대 한 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-144">The [jQuery UI](http://jqueryui.com/) library provides support for animation, advanced effects, and customizable widgets.</span></span> <span data-ttu-id="f7859-145">JQuery JavaScript 라이브러리를 기반으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-145">It's built on top of the jQuery JavaScript library.</span></span> <span data-ttu-id="f7859-146">Datepicker 팝업 일정 사용 하면 쉽고 자연 스러운 일정을 사용 하는 문자열을 입력 하는 대신 날짜를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-146">The datepicker popup calendar makes it easy and natural to enter dates using a calendar instead of entering a string.</span></span> <span data-ttu-id="f7859-147">팝업 일정도 사용자가 법적 날짜 수를 제한-날짜에 대 한 일반 텍스트 항목 사용 같은 코드를 입력 하면 `2/33/1999` (2 월 33rd, 1999), 하지만 [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) 팝업 일정 작업을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-147">The popup calendar also limits users to legal dates — ordinary text entry for a date would let you enter something like `2/33/1999` ( February 33rd, 1999), but the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar won't allow that.</span></span>

<span data-ttu-id="f7859-148">먼저, jQuery UI 라이브러리를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-148">First, you have to install the jQuery UI libraries.</span></span> <span data-ttu-id="f7859-149">이렇게 하려면 Visual Studio 2010 및 Visual Web Developer의 SP1 버전에 포함 된 패키지 관리자 인 NuGet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-149">To do that, you'll use NuGet, which is a package manager that's included in SP1 versions of Visual Studio 2010 and Visual Web Developer.</span></span>

<span data-ttu-id="f7859-150">Visual Web developer에서에서 **도구** 메뉴 선택 **라이브러리 패키지 관리자** 선택한 후 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-150">In Visual Web Developer, from the **Tools** menu, select **Library Package Manager** and then select **Manage NuGet Packages**.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

<span data-ttu-id="f7859-151">참고: 경우는 **도구** 메뉴에 표시 되지 않습니다는 **라이브러리 패키지 관리자** 명령의 지침에 따라 NuGet을 설치 해야는 [NuGet 설치](http://docs.nuget.org/docs/start-here/installing-nuget) 페이지 NuGet 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-151">Note: If the **Tools** menu doesn't display the **Library Package Manager** command, you need to install NuGet by following the instructions on the [Installing NuGet](http://docs.nuget.org/docs/start-here/installing-nuget) page of the NuGet website.</span></span>   
  
<span data-ttu-id="f7859-152">Visual Web Developer 대신 Visual Studio에서 사용 중인 경우는 **도구** 메뉴 선택 **라이브러리 패키지 관리자** 선택한 후 **라이브러리 패키지 참조 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-152">If you're using Visual Studio instead of Visual Web Developer, from the **Tools** menu, select **Library Package Manager** and then select **Add Library Package Reference**.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

<span data-ttu-id="f7859-153">에 **MVCMovie-NuGet 패키지 관리** 대화 상자를 클릭는 **온라인** 왼쪽 탭 한 다음 입력 &quot;jQuery.UI&quot; 검색 상자에 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-153">In the **MVCMovie - Manage NuGet Packages** dialog box, click the **Online** tab on the left and then enter &quot;jQuery.UI&quot; in the search box.</span></span> <span data-ttu-id="f7859-154">J 선택 **쿼리 UI 위젯: Datepicker**을 선택한 후는 **설치** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-154">Select j **Query UI WIdgets:Datepicker**, then select the **Install** button.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

<span data-ttu-id="f7859-155">NuGet을 프로젝트에 이러한 디버그 버전 및 jQuery UI 코어 및 jQuery UI 날짜 선택의 축소 된 버전을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-155">NuGet adds these debug versions and minified versions of jQuery UI Core and the jQuery UI date picker to your project:</span></span>

- <span data-ttu-id="f7859-156">*jquery.ui.core.js*</span><span class="sxs-lookup"><span data-stu-id="f7859-156">*jquery.ui.core.js*</span></span>
- <span data-ttu-id="f7859-157">*jquery.ui.core.min.js*</span><span class="sxs-lookup"><span data-stu-id="f7859-157">*jquery.ui.core.min.js*</span></span>
- <span data-ttu-id="f7859-158">*jquery.ui.datepicker.js*</span><span class="sxs-lookup"><span data-stu-id="f7859-158">*jquery.ui.datepicker.js*</span></span>
- <span data-ttu-id="f7859-159">*jquery.ui.datepicker.min.js*</span><span class="sxs-lookup"><span data-stu-id="f7859-159">*jquery.ui.datepicker.min.js*</span></span>

<span data-ttu-id="f7859-160">참고: 디버그 버전 (없이 파일의 *. min.js* 확장) 유용한 디버깅을 위해 있지만 프로덕션 사이트에 축소 된 버전에만 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-160">Note: The debug versions (the files without the *.min.js* extension) are useful for debugging, but in a production site, you'd include only the minified versions.</span></span>

<span data-ttu-id="f7859-161">JQuery 날짜 선택을 실제로 사용 하려면 템플릿 편집을 달력 도구를 후크 할는 jQuery 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-161">To actually use the jQuery date picker, you need to create a jQuery script that will hook up the calendar widget to the edit template.</span></span> <span data-ttu-id="f7859-162">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *스크립트* 폴더와 선택 **추가**, 다음 **새 항목**, 차례로 **JScript 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-162">In **Solution Explorer**, right-click the *Scripts* folder and select **Add**, then **New Item**, and then **JScript File**.</span></span> <span data-ttu-id="f7859-163">파일 이름을 *DatePickerReady.js*합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-163">Name the file *DatePickerReady.js*.</span></span>

<span data-ttu-id="f7859-164">다음 코드를 추가 하는 *DatePickerReady.js* 파일:</span><span class="sxs-lookup"><span data-stu-id="f7859-164">Add the following code to the *DatePickerReady.js* file:</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

<span data-ttu-id="f7859-165">JQuery 모르는 경우이 수행 하는 작업에 대 한 간략 한 설명이 있습니다: 첫 번째 줄은는 &quot;jQuery 준비&quot; 함수는 페이지의 모든 DOM 요소를 로드 했 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-165">If you're not familiar with jQuery, here's a brief explanation of what this does: the first line is the &quot;jQuery ready&quot; function, which is called when all the DOM elements in a page have loaded.</span></span> <span data-ttu-id="f7859-166">클래스 이름을 가진 모든 DOM 요소를 선택 하는 두 번째 줄 `datefield`, 다음 호출에서 `datepicker` 채 각 항목에 대 한 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-166">The second line selects all DOM elements that have the class name `datefield`, then invokes the `datepicker` function for each of them.</span></span> <span data-ttu-id="f7859-167">(추가 하는 `datefield` 클래스를 *Views\Shared\EditorTemplates\Date.cshtml* 자습서의 앞부분에 나오는 템플릿.)</span><span class="sxs-lookup"><span data-stu-id="f7859-167">(Remember that you added the `datefield` class to the *Views\Shared\EditorTemplates\Date.cshtml* template earlier in the tutorial.)</span></span>

<span data-ttu-id="f7859-168">을 열고는 *Views\Shared\\_Layout.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-168">Next, open the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="f7859-169">날짜 선택을 사용할 수 있도록 필요한 대로 모두 있는 다음 파일에 대 한 참조를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-169">You need to add references to the following files, which are all required so that you can use the date picker:</span></span>

- <span data-ttu-id="f7859-170">*Content/themes/base/jquery.ui.core.css*</span><span class="sxs-lookup"><span data-stu-id="f7859-170">*Content/themes/base/jquery.ui.core.css*</span></span>
- <span data-ttu-id="f7859-171">*Content/themes/base/jquery.ui.datepicker.css*</span><span class="sxs-lookup"><span data-stu-id="f7859-171">*Content/themes/base/jquery.ui.datepicker.css*</span></span>
- <span data-ttu-id="f7859-172">*Content/themes/base/jquery.ui.theme.css*</span><span class="sxs-lookup"><span data-stu-id="f7859-172">*Content/themes/base/jquery.ui.theme.css*</span></span>
- <span data-ttu-id="f7859-173">*jquery.ui.core.min.js*</span><span class="sxs-lookup"><span data-stu-id="f7859-173">*jquery.ui.core.min.js*</span></span>
- <span data-ttu-id="f7859-174">*jquery.ui.datepicker.min.js*</span><span class="sxs-lookup"><span data-stu-id="f7859-174">*jquery.ui.datepicker.min.js*</span></span>
- <span data-ttu-id="f7859-175">*DatePickerReady.js*</span><span class="sxs-lookup"><span data-stu-id="f7859-175">*DatePickerReady.js*</span></span>

<span data-ttu-id="f7859-176">다음 예제에서는 실제 코드의 맨 아래에 추가 해야 하는 `head` 요소에는 *Views\Shared\\_Layout.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-176">The following example shows the actual code that you should add at the bottom of the `head` element in the *Views\Shared\\_Layout.cshtml* file.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

<span data-ttu-id="f7859-177">전체 `head` 섹션은 같습니다.:</span><span class="sxs-lookup"><span data-stu-id="f7859-177">The complete `head` section is shown here:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

<span data-ttu-id="f7859-178">[URL 콘텐츠 도우미](https://msdn.microsoft.com/en-us/library/system.web.mvc.urlhelper.content.aspx) 메서드 리소스 경로 절대 경로로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-178">The [URL content helper](https://msdn.microsoft.com/en-us/library/system.web.mvc.urlhelper.content.aspx) method converts the resource path to an absolute path.</span></span> <span data-ttu-id="f7859-179">사용 해야 `@URL.Content` 올바르게 응용 프로그램은 IIS에서 실행 되는 이러한 리소스를 참조 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-179">You must use `@URL.Content` to correctly reference these resources when the application is running on IIS.</span></span>

<span data-ttu-id="f7859-180">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-180">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="f7859-181">편집 링크를 선택한 다음에 삽입 지점을 **ReleaseDate** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-181">Select an edit link, then put the insertion point into the **ReleaseDate** field.</span></span> <span data-ttu-id="f7859-182">JQuery UI 팝업 일정 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-182">The jQuery UI popup calendar is displayed.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

<span data-ttu-id="f7859-183">대부분의 jQuery 컨트롤과 마찬가지로 datepicker는 광범위 하 게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-183">Like most jQuery controls, the datepicker lets you customize it extensively.</span></span> <span data-ttu-id="f7859-184">정보를 참조 하십시오. [시각적으로 사용자 지정: jQuery UI 테마 디자인](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) 에 [jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-184">For information, see [Visual Customization: Designing a jQuery UI theme](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) on the [jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/) site.</span></span>

### <a name="supporting-the-html5-date-input-control"></a><span data-ttu-id="f7859-185">HTML5 날짜 입력된 제어를 지 원하는</span><span class="sxs-lookup"><span data-stu-id="f7859-185">Supporting the HTML5 Date Input Control</span></span>

<span data-ttu-id="f7859-186">브라우저는 HTML5 지원, 입력, 네이티브 HTML5 사용 하려면 합니다는 `date` 요소, 입력 및 jQuery UI 일정을 사용 하지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-186">As more browsers support HTML5, you'll want to use the native HTML5 input, such as the `date` input element, and not use the jQuery UI calendar.</span></span> <span data-ttu-id="f7859-187">브라우저가 지 원하는 경우 HTML5 컨트롤을 자동으로 사용 하도록 응용 프로그램에 논리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-187">You can add logic to your application to automatically use HTML5 controls if the browser supports them.</span></span> <span data-ttu-id="f7859-188">이 위해의 내용을 바꿉니다는 *DatePickerReady.js* 다음 파일:</span><span class="sxs-lookup"><span data-stu-id="f7859-188">To do this, replace the contents of the *DatePickerReady.js* file with the following:</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

<span data-ttu-id="f7859-189">이 스크립트의 첫 번째 줄 Modernizr를 사용 하 여 HTML5 날짜 입력을 지원 하는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f7859-189">The first line of this script uses Modernizr to verify that HTML5 date input is supported.</span></span> <span data-ttu-id="f7859-190">지원 되지 않는 경우 jQuery UI 날짜 선택 대신 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-190">If it's not supported, the jQuery UI date picker is hooked up instead.</span></span> <span data-ttu-id="f7859-191">([Modernizr](http://www.modernizr.com/docs/) 는 HTML5 및 CSS3의 네이티브 구현의 가용성을 검색 하는 오픈 소스 JavaScript 라이브러리.</span><span class="sxs-lookup"><span data-stu-id="f7859-191">([Modernizr](http://www.modernizr.com/docs/) is an open-source JavaScript library that detects the availability of native implementations of HTML5 and CSS3.</span></span> <span data-ttu-id="f7859-192">Modernizr은 만들면 새 ASP.NET MVC 프로젝트에 포함 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="f7859-192">Modernizr is included in any new ASP.NET MVC projects that you create.)</span></span>

<span data-ttu-id="f7859-193">이 변경을 수행한 후에 HTML5 Opera 11 등을 지 원하는 브라우저를 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-193">After you've made this change, you can test it by using a browser that supports HTML5, such as Opera 11.</span></span> <span data-ttu-id="f7859-194">HTML5 호환 브라우저를 사용 하 여 응용 프로그램을 실행 하 고 동영상 항목을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-194">Run the application using an HTML5-compatible browser and edit a movie entry.</span></span> <span data-ttu-id="f7859-195">HTML5 날짜 컨트롤은 jQuery UI 팝업 일정 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-195">The HTML5 date control is used instead of the jQuery UI popup calendar:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

<span data-ttu-id="f7859-196">새 버전의 브라우저를 구현 하는 HTML5 증분 때문에 광범위 한 HTML5 지원 제공 하는 웹 사이트에 코드를 추가 하는 좋은 방법은 지금은입니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-196">Because new versions of browsers are implementing HTML5 incrementally, a good approach for now is to add code to your website that accommodates a wide variety of HTML5 support.</span></span> <span data-ttu-id="f7859-197">예를 들어 더 강력한 *DatePickerReady.js* 스크립트는 부분적 으로만 HTML5 날짜 컨트롤을 지원 하 여 사이트 지원 브라우저 수 있는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-197">For example, a more robust *DatePickerReady.js* script is shown below that lets your site support browsers that only partially support the HTML5 date control.</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

<span data-ttu-id="f7859-198">이 스크립트는 HTML5 선택 `input` 형식의 요소 `date` HTML5 날짜 컨트롤을 완벽 하 게 지원 하지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-198">This script selects HTML5 `input` elements of type `date` that don't fully support the HTML5 date control.</span></span> <span data-ttu-id="f7859-199">이러한 요소에 대 한 jQuery UI 팝업 일정 연결 하는 것을를 수정한 다음는 `type` 에서 특성 `date` 를 `text`합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-199">For those elements, it hooks up the jQuery UI popup calendar and then changes the `type` attribute from `date` to `text`.</span></span> <span data-ttu-id="f7859-200">변경 하 여는 `type` 에서 특성 `date` 를 `text`, 부분 HTML5 날짜 지원 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-200">By changing the `type` attribute from `date` to `text`, partial HTML5 date support is eliminated.</span></span> <span data-ttu-id="f7859-201">훨씬 더 강력한 *DatePickerReady.js* 스크립트에서 찾을 수 있습니다 [JSFIDDLE](http://jsfiddle.net/XSTK8/15/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-201">An even more robust *DatePickerReady.js* script can be found at [JSFIDDLE](http://jsfiddle.net/XSTK8/15/).</span></span>

### <a name="adding-nullable-dates-to-the-templates"></a><span data-ttu-id="f7859-202">Null 허용 날짜 서식 파일에 추가</span><span class="sxs-lookup"><span data-stu-id="f7859-202">Adding Nullable Dates to the Templates</span></span>

<span data-ttu-id="f7859-203">기존 날짜 서식 파일 중 하나를 사용 하 여 null 날짜를 전달 하는 경우 런타임 오류가 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-203">If you use one of the existing date templates and pass a null date, you'll get a run-time error.</span></span> <span data-ttu-id="f7859-204">날짜 서식 파일을 보다 강력 하려면 null 값을 처리 하도록 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-204">To make the date templates more robust, you'll change them to handle null values.</span></span> <span data-ttu-id="f7859-205">Null을 허용 하는 날짜를 지원 하기 위해 변경의 코드는 *Views\Shared\DisplayTemplates\DateTime.cshtml* 다음과:</span><span class="sxs-lookup"><span data-stu-id="f7859-205">To support nullable dates, change the code in the *Views\Shared\DisplayTemplates\DateTime.cshtml* to the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

<span data-ttu-id="f7859-206">모델은 빈 문자열을 반환 하는 코드 **null**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-206">The code returns an empty string when the model is **null**.</span></span>

<span data-ttu-id="f7859-207">코드 변경의 *Views\Shared\EditorTemplates\Date.cshtml* 다음과 파일:</span><span class="sxs-lookup"><span data-stu-id="f7859-207">Change the code in the *Views\Shared\EditorTemplates\Date.cshtml* file to the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

<span data-ttu-id="f7859-208">이 코드를 실행할 때 모델이 null 인 경우 모델의 `DateTime` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-208">When this code runs, if the model is not null, the model's `DateTime` value is used.</span></span> <span data-ttu-id="f7859-209">모델이 null 인 경우 현재 날짜가 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-209">If the model is null, the current date is used instead.</span></span>

### <a name="wrapup"></a><span data-ttu-id="f7859-210">Wrapup</span><span class="sxs-lookup"><span data-stu-id="f7859-210">Wrapup</span></span>

<span data-ttu-id="f7859-211">이 자습서는 템플릿 기반 도우미 ASP.NET의 기본 사항을 검사가 수행 하 고 ASP.NET MVC 응용 프로그램에서 jQuery UI datepicker 팝업 일정을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-211">This tutorial has covered the basics of ASP.NET templated helpers and shows you how to use the jQuery UI datepicker popup calendar in an ASP.NET MVC application.</span></span> <span data-ttu-id="f7859-212">자세한 내용은 다음이 리소스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f7859-212">For more information, try these resources:</span></span>

- <span data-ttu-id="f7859-213">지역화에 대 한 내용은 Rajeesh의 블로그를 참조 [ASP.NET MVC에서 JQueryUI Datepicker](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-213">For information on localization, see Rajeesh's blog [JQueryUI Datepicker in ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/).</span></span>
- <span data-ttu-id="f7859-214">JQuery UI에 대 한 정보를 참조 하십시오. [jQuery UI](http://docs.jquery.com/UI)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-214">For information about jQuery UI, see [jQuery UI](http://docs.jquery.com/UI).</span></span>
- <span data-ttu-id="f7859-215">Datepicker 컨트롤 지역화 하는 방법에 대 한 정보를 참조 하십시오. [UI/Datepicker/지역화](http://docs.jquery.com/UI/Datepicker/Localization)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-215">For information about how to localize the datepicker control, see [UI/Datepicker/Localization](http://docs.jquery.com/UI/Datepicker/Localization).</span></span>
- <span data-ttu-id="f7859-216">ASP.NET MVC 템플릿에 대 한 자세한 내용은 Brad Wilson의 블로그 시리즈에 참조 [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-216">For more information about the ASP.NET MVC templates, see Brad Wilson's blog series on [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html).</span></span> <span data-ttu-id="f7859-217">계열을 ASP.NET MVC 2 용으로 작성 된, 하지만 자료는 ASP.NET MVC의 최신 버전은 여전히 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7859-217">Although the series was written for ASP.NET MVC 2, the material still applies for the current version of ASP.NET MVC.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="f7859-218">이전</span><span class="sxs-lookup"><span data-stu-id="f7859-218">Previous</span></span>](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
