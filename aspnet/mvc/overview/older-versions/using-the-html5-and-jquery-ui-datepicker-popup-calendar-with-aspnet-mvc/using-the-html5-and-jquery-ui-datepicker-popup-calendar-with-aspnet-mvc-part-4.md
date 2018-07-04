---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: ASP.NET MVC-4 부에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker 팝업 일정을 ASP.NET MV에서 사용 하는 방법의 기본 사항을 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: 74bd88408c4d60032a1275aa9f8540cf710dac36
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37380910"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a><span data-ttu-id="46554-103">ASP.NET MVC-4 부에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용</span><span class="sxs-lookup"><span data-stu-id="46554-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 4</span></span>
====================
<span data-ttu-id="46554-104">[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="46554-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="46554-105">이 자습서는 편집기 템플릿, 표시 템플릿 및 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정을 사용 하는 방법의 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>


### <a name="adding-a-template-for-editing-dates"></a><span data-ttu-id="46554-106">날짜를 편집 하기 위한 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="46554-106">Adding a Template for Editing Dates</span></span>

<span data-ttu-id="46554-107">이 섹션에서는 ASP.NET MVC로 표시 되는 모델 속성을 편집 하는 것에 대 한 UI를 표시 하는 경우 적용 되는 날짜를 편집 하는 것에 대 한 템플릿을 만듭니다는 **날짜** 열거를 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-107">In this section you'll create a template for editing dates that will be applied when ASP.NET MVC displays UI for editing model properties that are marked with the **Date** enumeration of the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attibute.</span></span> <span data-ttu-id="46554-108">템플릿을 날짜만; 렌더링 시간 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="46554-108">The template will render only the date; time will not be displayed.</span></span> <span data-ttu-id="46554-109">템플릿에서 사용 된 [jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/) 팝업 달력 날짜를 편집 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-109">In the template you'll use the [jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to provide a way to edit dates.</span></span>

<span data-ttu-id="46554-110">시작 하려면를 엽니다는 *Movie.cs* 파일을 추가 합니다 [데이터 형식](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성을 **날짜** 열거형을는 `ReleaseDate` 속성을 다음 코드 에서처럼:</span><span class="sxs-lookup"><span data-stu-id="46554-110">To begin, open the *Movie.cs* file and add the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute with the **Date** enumeration to the `ReleaseDate` property, as shown in the following code:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

<span data-ttu-id="46554-111">이 코드는 `ReleaseDate` 모두에 템플릿을 표시 및 서식 파일을 편집 하지 않고 표시할 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-111">This code causes the `ReleaseDate` field to be displayed without the time in both display templates and edit templates.</span></span> <span data-ttu-id="46554-112">응용 프로그램을 포함 하는 경우는 *date.cshtml* 에서 서식 파일을 *Views\Shared\EditorTemplates* 폴더 또는 *Views\Movies\EditorTemplates* 폴더에서 해당 템플릿을 모든 렌더링 하는 데 사용할 `DateTime` 편집 하는 동안 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-112">If your application contains a *date.cshtml* template in the *Views\Shared\EditorTemplates* folder or in the *Views\Movies\EditorTemplates* folder, that template will be used to render any `DateTime` property while editing.</span></span> <span data-ttu-id="46554-113">그렇지 않은 경우 기본 제공 ASP.NET 템플릿 시스템 날짜로 속성이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46554-113">Otherwise the built-in ASP.NET templating system will display the property as a date.</span></span>

<span data-ttu-id="46554-114">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-114">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="46554-115">릴리스 날짜에 대 한 입력된 필드는 날짜만 표시 확인에 대 한 편집 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-115">Select an edit link to verify that the input field for the release date is showing only the date.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

<span data-ttu-id="46554-116">**솔루션 탐색기**, 확장를 *뷰* 폴더를 확장 합니다 *공유* 폴더 및 마우스 오른쪽 단추로 *Views\Shared\EditorTemplates* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-116">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\EditorTemplates* folder.</span></span>

<span data-ttu-id="46554-117">클릭 **추가**를 클릭 하 고 **보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-117">Click **Add**, and then click **View**.</span></span> <span data-ttu-id="46554-118">합니다 **뷰 추가** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46554-118">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="46554-119">에 **뷰 이름** 상자에 입력 &quot;날짜&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-119">In the **View name** box, type &quot;Date&quot;.</span></span>

<span data-ttu-id="46554-120">선택 된 **부분 뷰로 만들기** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-120">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="46554-121">있는지 확인 합니다 **레이아웃 또는 마스터 페이지를 사용** 및 **강력한 형식의 뷰를 만들** 확인란을 선택 하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-121">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

<span data-ttu-id="46554-122">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-122">Click **Add**.</span></span> <span data-ttu-id="46554-123">합니다 *Views\Shared\EditorTemplates\Date.cshtml* 템플릿이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="46554-123">The *Views\Shared\EditorTemplates\Date.cshtml* template is created.</span></span>

<span data-ttu-id="46554-124">다음 코드를 추가 합니다 *Views\Shared\EditorTemplates\Date.cshtml* 템플릿.</span><span class="sxs-lookup"><span data-stu-id="46554-124">Add the following code to the *Views\Shared\EditorTemplates\Date.cshtml* template.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

<span data-ttu-id="46554-125">모델을 선언 하는 첫 번째 줄을 `DateTime` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-125">The first line declares the model to be a `DateTime` type.</span></span> <span data-ttu-id="46554-126">컴파일 시간을 받을 수 있도록 모범 사례는 편집에서 모델 형식을 선언 하 고 템플릿을 표시 하려면 필요가 있지만 보기에 전달 되는 모델을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-126">Although you don't need to declare the model type in edit and display templates, it's a best practice so that you get compile-time checking of the model being passed to the view.</span></span> <span data-ttu-id="46554-127">(다른 혜택은 Visual Studio에서 보기에서 모델에 대 한 IntelliSense를 가져올 다음.) ASP.NET MVC 모델 형식을 선언 되지 않으면 간주는 [동적](https://msdn.microsoft.com/library/dd264741.aspx) 입력 이며 없는 컴파일 타임 형식 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-127">(Another benefit is that you then get IntelliSense for the model in the view in Visual Studio.) If the model type is not declared, ASP.NET MVC considers it a [dynamic](https://msdn.microsoft.com/library/dd264741.aspx) type and there's no compile-time type checking.</span></span> <span data-ttu-id="46554-128">모델을 선언 하는 경우는 `DateTime` 형식 강력 하 게 형식화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46554-128">If you declare the model to be a `DateTime` type, it becomes strongly typed.</span></span>

<span data-ttu-id="46554-129">두 번째 줄은 표시 하는 HTML 태그를 리터럴 &quot;날짜 템플릿을 사용 하 여&quot; 날짜 필드를 전 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-129">The second line is just literal HTML markup that displays &quot;Using Date Template&quot; before a date field.</span></span> <span data-ttu-id="46554-130">이 날짜 서식 파일 사용 되 고 있는지 확인 하려면이 줄을 일시적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-130">You'll use this line temporarily to verify that this date template is being used.</span></span>

<span data-ttu-id="46554-131">다음 줄은는 [Html.TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx) 렌더링 하는 도우미는 `input` 필드 텍스트 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46554-131">The next line is an [Html.TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx) helper that renders an `input` field that's a text box.</span></span> <span data-ttu-id="46554-132">도우미의 세 번째 매개 변수가 무명 형식을 사용 하 여 텍스트 상자에 대 한 클래스를 설정 `datefield` 하 고 형식을 `date`합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-132">The third parameter for the helper uses an anonymous type to set the class for the text box to `datefield` and the type to `date`.</span></span> <span data-ttu-id="46554-133">(때문에 `class` 는 예약 된 C#에서 사용 해야 합니다 `@` 이스케이프 문자는 `class` C# 파서는 특성.)</span><span class="sxs-lookup"><span data-stu-id="46554-133">(Because `class` is a reserved in C#, you need to use the `@` character to escape the `class` attribute in the C# parser.)</span></span>

<span data-ttu-id="46554-134">`date` 형식은 HTML5 인식 브라우저는 HTML5 달력 컨트롤을 렌더링할 수 있도록 설정 하는 HTML5 입력된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-134">The `date` type is an HTML5 input type that enables HTML5-aware browsers to render a HTML5 calendar control.</span></span> <span data-ttu-id="46554-135">나중에 JavaScript를 jQuery datepicker 후크를 추가 합니다 `Html.TextBox` 사용 하 여 요소를 `datefield` 클래스.</span><span class="sxs-lookup"><span data-stu-id="46554-135">Later on you'll add some JavaScript to hook up the jQuery datepicker to the `Html.TextBox` element using the `datefield` class.</span></span>

<span data-ttu-id="46554-136">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-136">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="46554-137">중인지 확인할 수 있습니다 합니다 `ReleaseDate` 템플릿을 표시 하기 때문에 편집 보기에서 속성 편집 템플릿을 사용 하 여는 &quot;날짜 템플릿을 사용 하 여&quot; 직전를 `ReleaseDate` 이 이미지에 표시 된 대로 텍스트 입력 상자에서:</span><span class="sxs-lookup"><span data-stu-id="46554-137">You can verify that the `ReleaseDate` property in the edit view is using the edit template because the template displays &quot;Using Date Template&quot; just before the `ReleaseDate` text input box, as shown in this image:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

<span data-ttu-id="46554-138">브라우저에서 페이지의 소스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="46554-138">In your browser, view the source of the page.</span></span> <span data-ttu-id="46554-139">(예를 들어, 페이지를 마우스 오른쪽 단추로 클릭 하 고 선택 **소스 보기**.) 다음 예와 페이지에 대 한 태그 중 일부를 보여 주는 합니다 `class` 및 `type` 렌더링된 된 HTML 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-139">(For example, right-click the page and select **View source**.) The following example shows some of the markup for the page, illustrating the `class` and `type` attributes in the rendered HTML.</span></span>

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

<span data-ttu-id="46554-140">반환 합니다 *Views\Shared\EditorTemplates\Date.cshtml* 템플릿과 제거는 &quot;날짜 템플릿을 사용 하 여&quot; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-140">Return to the *Views\Shared\EditorTemplates\Date.cshtml* template and remove the &quot;Using Date Template&quot; markup.</span></span> <span data-ttu-id="46554-141">이제 완료 된 서식 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="46554-141">Now the completed template looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a><span data-ttu-id="46554-142">JQuery UI Datepicker 팝업 일정 추가 NuGet을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="46554-142">Adding a jQuery UI Datepicker Popup Calendar using NuGet</span></span>

<span data-ttu-id="46554-143">이 섹션에서는 추가 합니다 [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) 날짜 편집 템플릿에 팝업 달력입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-143">In this section you'll add the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to the date-edit template.</span></span> <span data-ttu-id="46554-144">합니다 [jQuery UI](http://jqueryui.com/) 라이브러리 효과 및 사용자 지정 가능한 위젯 고급 애니메이션에 대 한 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-144">The [jQuery UI](http://jqueryui.com/) library provides support for animation, advanced effects, and customizable widgets.</span></span> <span data-ttu-id="46554-145">이 jQuery JavaScript 라이브러리를 기반으로 구축 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46554-145">It's built on top of the jQuery JavaScript library.</span></span> <span data-ttu-id="46554-146">Datepicker 팝업 일정 사용 하면 쉽고 자연스럽 게 일정을 사용 하 여 문자열을 입력 하는 대신 날짜를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-146">The datepicker popup calendar makes it easy and natural to enter dates using a calendar instead of entering a string.</span></span> <span data-ttu-id="46554-147">팝업 달력에는 또한 사용자가 올바른 날짜 제한-같은 코드를 입력 날짜에 대 한 일반 텍스트 항목 수 `2/33/1999` (2 월 33rd, 1999), 하지만 [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) 팝업 달력은 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="46554-147">The popup calendar also limits users to legal dates — ordinary text entry for a date would let you enter something like `2/33/1999` ( February 33rd, 1999), but the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar won't allow that.</span></span>

<span data-ttu-id="46554-148">먼저, jQuery UI 라이브러리를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-148">First, you have to install the jQuery UI libraries.</span></span> <span data-ttu-id="46554-149">이렇게 하려면 SP1 버전의 Visual Studio 2010 및 Visual Web Developer에 포함 된 패키지 관리자 인 NuGet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-149">To do that, you'll use NuGet, which is a package manager that's included in SP1 versions of Visual Studio 2010 and Visual Web Developer.</span></span>

<span data-ttu-id="46554-150">Visual Web developer에서에서 합니다 **도구** 메뉴에서 **라이브러리 패키지 관리자** 선택한 후 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-150">In Visual Web Developer, from the **Tools** menu, select **Library Package Manager** and then select **Manage NuGet Packages**.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

<span data-ttu-id="46554-151">참고: 경우는 **도구** 메뉴를 표시 하지 않습니다는 **라이브러리 패키지 관리자** 명령, 지시에 따라 NuGet을 설치 해야 합니다 [NuGet 설치](http://docs.nuget.org/docs/start-here/installing-nuget) 페이지 NuGet 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-151">Note: If the **Tools** menu doesn't display the **Library Package Manager** command, you need to install NuGet by following the instructions on the [Installing NuGet](http://docs.nuget.org/docs/start-here/installing-nuget) page of the NuGet website.</span></span>   
  
<span data-ttu-id="46554-152">Visual Web Developer에서 대신 Visual Studio에서 사용 중인 경우는 **도구** 메뉴에서 **라이브러리 패키지 관리자** 선택한 후 **라이브러리 패키지 참조 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-152">If you're using Visual Studio instead of Visual Web Developer, from the **Tools** menu, select **Library Package Manager** and then select **Add Library Package Reference**.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

<span data-ttu-id="46554-153">에 **MVCMovie-NuGet 패키지 관리** 대화 상자에서 클릭 합니다 **온라인** 왼쪽에 탭 하 고 enter &quot;jQuery.UI&quot; 검색 상자에 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-153">In the **MVCMovie - Manage NuGet Packages** dialog box, click the **Online** tab on the left and then enter &quot;jQuery.UI&quot; in the search box.</span></span> <span data-ttu-id="46554-154">J 선택 **쿼리 UI 위젯: Datepicker**를 선택 하 고는 **설치** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-154">Select j **Query UI WIdgets:Datepicker**, then select the **Install** button.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

<span data-ttu-id="46554-155">NuGet은 프로젝트에 이러한 디버그 버전 및 jQuery UI 코어 및 jQuery UI 날짜 선택의 축소 된 버전을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-155">NuGet adds these debug versions and minified versions of jQuery UI Core and the jQuery UI date picker to your project:</span></span>

- <span data-ttu-id="46554-156">*jquery.ui.core.js*</span><span class="sxs-lookup"><span data-stu-id="46554-156">*jquery.ui.core.js*</span></span>
- <span data-ttu-id="46554-157">*jquery.ui.core.min.js*</span><span class="sxs-lookup"><span data-stu-id="46554-157">*jquery.ui.core.min.js*</span></span>
- <span data-ttu-id="46554-158">*jquery.ui.datepicker.js*</span><span class="sxs-lookup"><span data-stu-id="46554-158">*jquery.ui.datepicker.js*</span></span>
- <span data-ttu-id="46554-159">*jquery.ui.datepicker.min.js*</span><span class="sxs-lookup"><span data-stu-id="46554-159">*jquery.ui.datepicker.min.js*</span></span>

<span data-ttu-id="46554-160">참고: 디버그 버전 (없이 파일을 *. min.js* 확장) 유용 디버깅용 하지만 프로덕션 사이트에서 축소 된 버전에만 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-160">Note: The debug versions (the files without the *.min.js* extension) are useful for debugging, but in a production site, you'd include only the minified versions.</span></span>

<span data-ttu-id="46554-161">JQuery 날짜 선택기를 실제로 사용 하려면 템플릿 편집에 달력 위젯을 후크는 jQuery 스크립트를 만드는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-161">To actually use the jQuery date picker, you need to create a jQuery script that will hook up the calendar widget to the edit template.</span></span> <span data-ttu-id="46554-162">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *스크립트* 폴더를 선택 **추가**, 다음 **새 항목**를 차례로 **JScript 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-162">In **Solution Explorer**, right-click the *Scripts* folder and select **Add**, then **New Item**, and then **JScript File**.</span></span> <span data-ttu-id="46554-163">파일 이름을 *DatePickerReady.js*합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-163">Name the file *DatePickerReady.js*.</span></span>

<span data-ttu-id="46554-164">다음 코드를 추가 합니다 *DatePickerReady.js* 파일:</span><span class="sxs-lookup"><span data-stu-id="46554-164">Add the following code to the *DatePickerReady.js* file:</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

<span data-ttu-id="46554-165">JQuery를 사용 하 여 잘 모르는 경우이 기능에 대해 간략히 설명 같습니다: 첫 번째 줄은는 &quot;jQuery ready&quot; 페이지의 모든 DOM 요소를 로드 하는 때 호출 되는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-165">If you're not familiar with jQuery, here's a brief explanation of what this does: the first line is the &quot;jQuery ready&quot; function, which is called when all the DOM elements in a page have loaded.</span></span> <span data-ttu-id="46554-166">클래스 이름을 가진 모든 DOM 요소를 선택 하는 두 번째 줄 `datefield`, 다음 호출을 `datepicker` 각각에 대 한 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-166">The second line selects all DOM elements that have the class name `datefield`, then invokes the `datepicker` function for each of them.</span></span> <span data-ttu-id="46554-167">(추가한 기억 합니다 `datefield` 클래스를 *Views\Shared\EditorTemplates\Date.cshtml* 자습서의 앞부분에 나오는 템플릿.)</span><span class="sxs-lookup"><span data-stu-id="46554-167">(Remember that you added the `datefield` class to the *Views\Shared\EditorTemplates\Date.cshtml* template earlier in the tutorial.)</span></span>

<span data-ttu-id="46554-168">다음으로 열고 합니다 *Views\Shared\\_Layout.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-168">Next, open the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="46554-169">날짜 선택기를 사용할 수 있도록 필요한 모든는 다음 파일에 대 한 참조를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-169">You need to add references to the following files, which are all required so that you can use the date picker:</span></span>

- <span data-ttu-id="46554-170">*Content/themes/base/jquery.ui.core.css*</span><span class="sxs-lookup"><span data-stu-id="46554-170">*Content/themes/base/jquery.ui.core.css*</span></span>
- <span data-ttu-id="46554-171">*Content/themes/base/jquery.ui.datepicker.css*</span><span class="sxs-lookup"><span data-stu-id="46554-171">*Content/themes/base/jquery.ui.datepicker.css*</span></span>
- <span data-ttu-id="46554-172">*Content/themes/base/jquery.ui.theme.css*</span><span class="sxs-lookup"><span data-stu-id="46554-172">*Content/themes/base/jquery.ui.theme.css*</span></span>
- <span data-ttu-id="46554-173">*jquery.ui.core.min.js*</span><span class="sxs-lookup"><span data-stu-id="46554-173">*jquery.ui.core.min.js*</span></span>
- <span data-ttu-id="46554-174">*jquery.ui.datepicker.min.js*</span><span class="sxs-lookup"><span data-stu-id="46554-174">*jquery.ui.datepicker.min.js*</span></span>
- <span data-ttu-id="46554-175">*DatePickerReady.js*</span><span class="sxs-lookup"><span data-stu-id="46554-175">*DatePickerReady.js*</span></span>

<span data-ttu-id="46554-176">다음 예제에서는 실제 코드의 맨 아래에 추가 해야 합니다 `head` 요소에는 *Views\Shared\\_Layout.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-176">The following example shows the actual code that you should add at the bottom of the `head` element in the *Views\Shared\\_Layout.cshtml* file.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

<span data-ttu-id="46554-177">전체 `head` 섹션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="46554-177">The complete `head` section is shown here:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

<span data-ttu-id="46554-178">합니다 [URL 콘텐츠 도우미](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx) 메서드는 리소스 경로를 절대 경로로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-178">The [URL content helper](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx) method converts the resource path to an absolute path.</span></span> <span data-ttu-id="46554-179">사용 해야 `@URL.Content` 올바르게 응용 프로그램은 IIS에서 실행 중인 경우 이러한 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-179">You must use `@URL.Content` to correctly reference these resources when the application is running on IIS.</span></span>

<span data-ttu-id="46554-180">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-180">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="46554-181">편집 링크를 선택한 다음에 삽입 포인터를 **ReleaseDate** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-181">Select an edit link, then put the insertion point into the **ReleaseDate** field.</span></span> <span data-ttu-id="46554-182">JQuery UI 팝업 일정 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46554-182">The jQuery UI popup calendar is displayed.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

<span data-ttu-id="46554-183">대부분의 jQuery 컨트롤과 마찬가지로 datepicker 광범위 하 게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46554-183">Like most jQuery controls, the datepicker lets you customize it extensively.</span></span> <span data-ttu-id="46554-184">정보를 참조 하세요. [시각적으로 사용자 지정: jQuery UI 테마 디자인](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) 에 [jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-184">For information, see [Visual Customization: Designing a jQuery UI theme](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) on the [jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/) site.</span></span>

### <a name="supporting-the-html5-date-input-control"></a><span data-ttu-id="46554-185">HTML5 날짜 입력된 제어를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-185">Supporting the HTML5 Date Input Control</span></span>

<span data-ttu-id="46554-186">입력와 같은 네이티브 HTML5를 사용 하려는 더 많은 브라우저가 HTML5 지원는 `date` 요소, 입력 및 jQuery UI 일정을 사용 하지.</span><span class="sxs-lookup"><span data-stu-id="46554-186">As more browsers support HTML5, you'll want to use the native HTML5 input, such as the `date` input element, and not use the jQuery UI calendar.</span></span> <span data-ttu-id="46554-187">자동으로 브라우저를 지 원하는 경우 HTML5 컨트롤을 사용 하도록 응용 프로그램 논리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46554-187">You can add logic to your application to automatically use HTML5 controls if the browser supports them.</span></span> <span data-ttu-id="46554-188">이 위해의 내용을 대체 합니다 *DatePickerReady.js* 다음을 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="46554-188">To do this, replace the contents of the *DatePickerReady.js* file with the following:</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

<span data-ttu-id="46554-189">이 스크립트의 첫 번째 줄 Modernizr를 사용 하 여 HTML5 날짜 입력을 지원 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-189">The first line of this script uses Modernizr to verify that HTML5 date input is supported.</span></span> <span data-ttu-id="46554-190">지원 되지 않는 경우 jQuery UI 날짜 선택 대신 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46554-190">If it's not supported, the jQuery UI date picker is hooked up instead.</span></span> <span data-ttu-id="46554-191">([Modernizr](http://www.modernizr.com/docs/) 는 HTML5 및 CSS3의 네이티브 구현의 가용성을 검색 하는 오픈 소스 JavaScript 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-191">([Modernizr](http://www.modernizr.com/docs/) is an open-source JavaScript library that detects the availability of native implementations of HTML5 and CSS3.</span></span> <span data-ttu-id="46554-192">Modernizr 사용자가 만든 모든 새로운 ASP.NET MVC 프로젝트에 포함 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="46554-192">Modernizr is included in any new ASP.NET MVC projects that you create.)</span></span>

<span data-ttu-id="46554-193">이 변경을 완료 한 후에 Opera 11 같은 HTML5를 지 원하는 브라우저를 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46554-193">After you've made this change, you can test it by using a browser that supports HTML5, such as Opera 11.</span></span> <span data-ttu-id="46554-194">HTML5 호환 브라우저를 사용 하 여 응용 프로그램을 실행 하 고 동영상 항목을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-194">Run the application using an HTML5-compatible browser and edit a movie entry.</span></span> <span data-ttu-id="46554-195">HTML5 날짜 컨트롤은 jQuery UI 팝업 일정 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46554-195">The HTML5 date control is used instead of the jQuery UI popup calendar:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

<span data-ttu-id="46554-196">새 버전의 브라우저를 구현 하는 HTML5 증분 지금은 좋은 방법 이므로 다양 한 HTML5 지원을 수용 하는 웹 사이트에 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-196">Because new versions of browsers are implementing HTML5 incrementally, a good approach for now is to add code to your website that accommodates a wide variety of HTML5 support.</span></span> <span data-ttu-id="46554-197">예를 들어 있는 더 강력한 *DatePickerReady.js* 스크립트는 부분적 으로만 HTML5 날짜 컨트롤을 지 원하는 사이트 지원 브라우저 수 있도록 하는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="46554-197">For example, a more robust *DatePickerReady.js* script is shown below that lets your site support browsers that only partially support the HTML5 date control.</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

<span data-ttu-id="46554-198">이 스크립트 선택 HTML5 `input` 유형 요소의 `date` HTML5 날짜 컨트롤을 완전히 지원 하지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-198">This script selects HTML5 `input` elements of type `date` that don't fully support the HTML5 date control.</span></span> <span data-ttu-id="46554-199">이러한 요소에 대 한 jQuery UI 팝업 일정을 연결 하 고 그런 다음 변경 합니다 `type` 에서 특성 `date` 에 `text`입니다.</span><span class="sxs-lookup"><span data-stu-id="46554-199">For those elements, it hooks up the jQuery UI popup calendar and then changes the `type` attribute from `date` to `text`.</span></span> <span data-ttu-id="46554-200">변경 하 여 합니다 `type` 에서 특성 `date` 에 `text`, 부분 HTML5 날짜 지원 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46554-200">By changing the `type` attribute from `date` to `text`, partial HTML5 date support is eliminated.</span></span> <span data-ttu-id="46554-201">더욱 강력한 *DatePickerReady.js* 스크립트에서 찾을 수 있습니다 [JSFIDDLE](http://jsfiddle.net/XSTK8/15/)합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-201">An even more robust *DatePickerReady.js* script can be found at [JSFIDDLE](http://jsfiddle.net/XSTK8/15/).</span></span>

### <a name="adding-nullable-dates-to-the-templates"></a><span data-ttu-id="46554-202">Nullable 날짜 템플릿을 추가</span><span class="sxs-lookup"><span data-stu-id="46554-202">Adding Nullable Dates to the Templates</span></span>

<span data-ttu-id="46554-203">기존 날짜 템플릿 중 하나를 사용 하 고 null 날짜를 전달 하는 경우 런타임 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46554-203">If you use one of the existing date templates and pass a null date, you'll get a run-time error.</span></span> <span data-ttu-id="46554-204">날짜 서식 파일을 보다 강력 하 게 하려면 null 값을 처리 하는 데를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46554-204">To make the date templates more robust, you'll change them to handle null values.</span></span> <span data-ttu-id="46554-205">Nullable이 날짜를 지원 하려면에서 코드를 변경 합니다 *Views\Shared\DisplayTemplates\DateTime.cshtml* 다음과:</span><span class="sxs-lookup"><span data-stu-id="46554-205">To support nullable dates, change the code in the *Views\Shared\DisplayTemplates\DateTime.cshtml* to the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

<span data-ttu-id="46554-206">코드 모델 이면 빈 문자열이 반환 **null**합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-206">The code returns an empty string when the model is **null**.</span></span>

<span data-ttu-id="46554-207">코드를 변경 합니다 *Views\Shared\EditorTemplates\Date.cshtml* 다음 파일:</span><span class="sxs-lookup"><span data-stu-id="46554-207">Change the code in the *Views\Shared\EditorTemplates\Date.cshtml* file to the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

<span data-ttu-id="46554-208">이 코드를 실행 하면 모델에서 null이 아닌 경우 모델의 `DateTime` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46554-208">When this code runs, if the model is not null, the model's `DateTime` value is used.</span></span> <span data-ttu-id="46554-209">모델이 null 인 경우 현재 날짜가 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46554-209">If the model is null, the current date is used instead.</span></span>

### <a name="wrapup"></a><span data-ttu-id="46554-210">Wrapup</span><span class="sxs-lookup"><span data-stu-id="46554-210">Wrapup</span></span>

<span data-ttu-id="46554-211">이 자습서는 ASP.NET 템플릿 기반 도우미는 기본적인 방법을 설명 했습니다 하 고 ASP.NET MVC 응용 프로그램에서 jQuery UI datepicker 팝업 일정을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="46554-211">This tutorial has covered the basics of ASP.NET templated helpers and shows you how to use the jQuery UI datepicker popup calendar in an ASP.NET MVC application.</span></span> <span data-ttu-id="46554-212">자세한 내용은 다음이 리소스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="46554-212">For more information, try these resources:</span></span>

- <span data-ttu-id="46554-213">지역화에 대 한 내용은 Rajeesh의 블로그를 참조 하세요 [ASP.NET MVC에서 JQueryUI Datepicker](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/)합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-213">For information on localization, see Rajeesh's blog [JQueryUI Datepicker in ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/).</span></span>
- <span data-ttu-id="46554-214">JQuery UI에 대 한 정보를 참조 하세요 [jQuery UI](http://docs.jquery.com/UI)합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-214">For information about jQuery UI, see [jQuery UI](http://docs.jquery.com/UI).</span></span>
- <span data-ttu-id="46554-215">Datepicker 컨트롤을 지역화 하는 방법에 대 한 정보를 참조 하세요 [지역화Datepicker/UI/](http://docs.jquery.com/UI/Datepicker/Localization)합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-215">For information about how to localize the datepicker control, see [UI/Datepicker/Localization](http://docs.jquery.com/UI/Datepicker/Localization).</span></span>
- <span data-ttu-id="46554-216">ASP.NET MVC 템플릿에 대 한 자세한 내용은 Brad Wilson의 블로그 시리즈에서 참조 하세요 [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="46554-216">For more information about the ASP.NET MVC templates, see Brad Wilson's blog series on [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html).</span></span> <span data-ttu-id="46554-217">시리즈는 ASP.NET MVC 2 용으로 작성 되었지만, 자료는 ASP.NET MVC의 최신 버전은 계속 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46554-217">Although the series was written for ASP.NET MVC 2, the material still applies for the current version of ASP.NET MVC.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="46554-218">이전</span><span class="sxs-lookup"><span data-stu-id="46554-218">Previous</span></span>](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
