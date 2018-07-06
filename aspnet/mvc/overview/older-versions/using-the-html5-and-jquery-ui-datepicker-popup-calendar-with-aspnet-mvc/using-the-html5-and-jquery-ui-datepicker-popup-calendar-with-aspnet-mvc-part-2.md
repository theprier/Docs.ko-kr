---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: ASP.NET MVC-2 부에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker 팝업 일정을 ASP.NET MV에서 사용 하는 방법의 기본 사항을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 08/29/2011
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 0dc9957bbb13394a4ee225d9966f4004de5714b9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37839309"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a><span data-ttu-id="11bec-103">ASP.NET MVC-2 부에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용</span><span class="sxs-lookup"><span data-stu-id="11bec-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 2</span></span>
====================
<span data-ttu-id="11bec-104">[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="11bec-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="11bec-105">이 자습서는 편집기 템플릿, 표시 템플릿 및 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정을 사용 하는 방법의 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>


## <a name="adding-an-automatic-datetime-template"></a><span data-ttu-id="11bec-106">자동 날짜/시간 서식 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-106">Adding an Automatic DateTime Template</span></span>

<span data-ttu-id="11bec-107">이 자습서의 첫 번째 부분을 명시적으로 서식 지정을 지정 하려면 모델에 특성을 추가 하는 방법 및 모델을 렌더링 하는 데 사용 되는 템플릿을 명시적으로 지정 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-107">In the first part of this tutorial, you saw how you can add attributes to the model to explicitly specify formatting, and how you can explicitly specify the template that's used to render the model.</span></span> <span data-ttu-id="11bec-108">예를 들어 합니다 [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 다음 코드가 명시적으로 특성에 대 한 서식을 지정 합니다 `ReleaseDate` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-108">For example, the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute in the following code explicity specifies the formatting for the `ReleaseDate` property.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

<span data-ttu-id="11bec-109">다음 예제에서는 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성을 사용 하 여를 `Date` 열거형 지정 하는 날짜 사용 되는 템플릿 모델을 렌더링 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-109">In the following example, the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute, using the `Date` enumeration, specifies that the date template should be used to render the model.</span></span> <span data-ttu-id="11bec-110">프로젝트에서 날짜 템플릿이 없는 경우에 기본 제공 날짜 템플릿이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-110">If there's no date template in your project, the built-in date template is used.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

<span data-ttu-id="11bec-111">그러나 ASP 합니다. MVC 형식 일치 규칙-over-configuration을 사용 하 여 형식의 이름과 일치 하는 템플릿을 검색 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-111">However, ASP.MVC can perform type matching using convention-over-configuration, by looking for a template that matches the name of a type.</span></span> <span data-ttu-id="11bec-112">이렇게 하면 자동으로 모든 특성 또는 코드를 전혀 사용 하지 않고 데이터의 형식을 지정 하는 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-112">This lets you create a template that automatically formats data without using any attributes or code at all.</span></span> <span data-ttu-id="11bec-113">자습서의이 부분에 대 한 형식의 모델 속성에 자동으로 적용 되는 템플릿을 만들어 [날짜/시간](https://msdn.microsoft.com/library/system.datetime.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-113">For this part of the tutorial, you'll create a template that's automatically applied to model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span> <span data-ttu-id="11bec-114">형식의 모든 모델 속성을 렌더링 하는 템플릿을 사용 해야를 지정 하려면 특성 또는 다른 구성을 사용할 필요가 없습니다 [날짜/시간](https://msdn.microsoft.com/library/system.datetime.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-114">You won't need to use an attribute or other configuration to specify that the template should be used to render all model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span>

<span data-ttu-id="11bec-115">또한 개별 속성 또는 개별 필드의 표시를 사용자 지정 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-115">You'll also learn a way to customize the display of individual properties or even individual fields.</span></span>

<span data-ttu-id="11bec-116">먼저 기존 서식 지정 정보를 제거 하 고 응용 프로그램의 전체 날짜를 표시 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-116">To begin, let's remove existing formatting information and display full dates in the application.</span></span>

<span data-ttu-id="11bec-117">열기는 *Movie.cs* 파일을 주석으로 처리 합니다 `DataType` 특성을 `ReleaseDate` 속성:</span><span class="sxs-lookup"><span data-stu-id="11bec-117">Open the *Movie.cs* file and comment out the `DataType` attribute on the `ReleaseDate` property:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

<span data-ttu-id="11bec-118">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-118">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="11bec-119">다음에 유의 합니다 `ReleaseDate` 속성 없는 서식 지정 정보를 제공 하는 경우 기본값 이기 때문에 해당 날짜와 시간을 이제 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-119">Notice that the `ReleaseDate` property now displays both the date and time, because that's the default when no formatting information is provided.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a><span data-ttu-id="11bec-120">새 템플릿 테스트에 대 한 CSS 스타일 추가</span><span class="sxs-lookup"><span data-stu-id="11bec-120">Adding CSS Styles for Testing New Templates</span></span>

<span data-ttu-id="11bec-121">날짜 형식 지정에 대 한 서식 파일을 만들기 전에 새 템플릿에 적용할 수 있는 몇 가지 CSS 스타일 규칙을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-121">Before you create a template for formatting dates, you'll add a few CSS style rules that you can apply to the new templates.</span></span> <span data-ttu-id="11bec-122">이러한 새 템플릿 렌더링된 된 페이지를 사용 하는지 확인 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-122">These will help you verify that the rendered page is using the new template.</span></span>

<span data-ttu-id="11bec-123">열기는 *Content\Site.cs*s 파일 및 파일의 맨 아래에 다음 CSS 규칙을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-123">Open the *Content\Site.cs*s file and add the following CSS rules to the bottom of the file:</span></span>

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a><span data-ttu-id="11bec-124">날짜/시간 표시 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="11bec-124">Adding DateTime Display Templates</span></span>

<span data-ttu-id="11bec-125">이제 새 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-125">Now you can create the new template.</span></span> <span data-ttu-id="11bec-126">에 *Views\Movies* 폴더를 만들기는 *DisplayTemplates* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-126">In the *Views\Movies* folder, create a *DisplayTemplates* folder.</span></span>

<span data-ttu-id="11bec-127">에 *Views\Shared* 폴더 만들기를 *DisplayTemplates* 폴더와 *EditorTemplates* 폴더.</span><span class="sxs-lookup"><span data-stu-id="11bec-127">In the *Views\Shared* folder, create a *DisplayTemplates* folder and an *EditorTemplates* folder.</span></span>

<span data-ttu-id="11bec-128">표시 템플릿은 합니다 *Views\Shared\DisplayTemplates* 폴더 모든 컨트롤러에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-128">The display templates in the *Views\Shared\DisplayTemplates* folder will be used by all controllers.</span></span> <span data-ttu-id="11bec-129">표시 템플릿은 합니다 *Views\Movie\DisplayTemplates* 폴더에만 사용 됩니다는 `Movie` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-129">The display templates in the *Views\Movie\DisplayTemplates* folder will be used only by the `Movie` controller.</span></span> <span data-ttu-id="11bec-130">(템플릿이 두 폴더에 이름이 같은 템플릿을 표시 하는 경우는 *Views\Movie\DisplayTemplates* 폴더-구체적인 서식 파일 즉,-반환한 보기에 대 한 우선는 `Movie` 컨트롤러.)</span><span class="sxs-lookup"><span data-stu-id="11bec-130">(If a template with the same name appears in both folders, the template in the *Views\Movie\DisplayTemplates* folder — that is, the more specific template — takes precedence for views returned by the `Movie` controller.)</span></span>

<span data-ttu-id="11bec-131">**솔루션 탐색기**, 확장를 *뷰* 폴더를 확장 합니다 *공유* 폴더 및 마우스 오른쪽 단추로 *Views\Shared\DisplayTemplates* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-131">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\DisplayTemplates* folder.</span></span>

<span data-ttu-id="11bec-132">클릭 **추가** 을 클릭 한 다음 **보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-132">Click **Add** and then click **View**.</span></span> <span data-ttu-id="11bec-133">합니다 **뷰 추가** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-133">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="11bec-134">에 **뷰 이름** 상자에 입력 `DateTime`합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-134">In the **View name** box, type `DateTime`.</span></span> <span data-ttu-id="11bec-135">(형식의 이름과 일치 하기 위해이 이름을 사용 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="11bec-135">(You must use this name in order to match the name of the type.)</span></span>

<span data-ttu-id="11bec-136">선택 된 **부분 뷰로 만들기** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-136">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="11bec-137">있는지 확인 합니다 **레이아웃 또는 마스터 페이지를 사용** 및 **강력한 형식의 뷰를 만들** 확인란을 선택 하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-137">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

<span data-ttu-id="11bec-138">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-138">Click **Add**.</span></span> <span data-ttu-id="11bec-139">A *DateTime.cshtml* 에서 템플릿을 만든 합니다 *Views\Shared\DisplayTemplates*합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-139">A *DateTime.cshtml* template is created in the *Views\Shared\DisplayTemplates*.</span></span>

<span data-ttu-id="11bec-140">다음 이미지는 *뷰* 폴더에서 **솔루션 탐색기** 후의 `DateTime` 표시 및 편집기 템플릿이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-140">The following image shows the *Views* folder in **Solution Explorer** after the `DateTime` display and editor templates are created.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

<span data-ttu-id="11bec-141">열기는 *Views\Shared\DisplayTemplates\DateTime.cshtml* 파일을 사용 하는 다음 태그를 추가 합니다 [String.Format](https://msdn.microsoft.com/library/system.string.format.aspx) 속성 시간 없이 날짜 서식을 지정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-141">Open the *Views\Shared\DisplayTemplates\DateTime.cshtml* file and add the following markup, which uses the [String.Format](https://msdn.microsoft.com/library/system.string.format.aspx) method to format the property as a date without the time.</span></span> <span data-ttu-id="11bec-142">(의 `{0:d}` 형식은 간단한 날짜 서식을 지정 합니다.)</span><span class="sxs-lookup"><span data-stu-id="11bec-142">(The `{0:d}` format specifies short date format.)</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

<span data-ttu-id="11bec-143">만들려면이 단계를 반복을 `DateTime` 서식 파일에는 *Views\Movie\DisplayTemplates* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-143">Repeat this step to create a `DateTime` template in the *Views\Movie\DisplayTemplates* folder.</span></span> <span data-ttu-id="11bec-144">다음 코드를 사용 합니다 *Views\Movie\DisplayTemplates\DateTime.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-144">Use the following code in the *Views\Movie\DisplayTemplates\DateTime.cshtml* file.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

<span data-ttu-id="11bec-145">`loud-1` 날짜를 굵은 빨간색 텍스트로 표시를 사용 하면 CSS 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-145">The `loud-1` CSS class causes the date to be display in bold red text.</span></span> <span data-ttu-id="11bec-146">추가 된 `loud-1` 이 특정 템플릿에서 사용 되는 경우 쉽게 확인할 수 있도록 임시 수단으로 바로 CSS 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-146">You added the `loud-1` CSS class just as a temporary measure so you can easily see when this particular template is being used.</span></span>

<span data-ttu-id="11bec-147">완료 했으면 생성 되 고 ASP.NET가 날짜를 표시 하는 데 사용할 템플릿을 사용자 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-147">What you've done is created and customized templates that ASP.NET will use to display dates.</span></span> <span data-ttu-id="11bec-148">일반 템플릿 (에 *Views\Shared\DisplayTemplates* 폴더) 간단한 짧은 날짜를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-148">The more general template (in the *Views\Shared\DisplayTemplates* folder) displays a simple short date.</span></span> <span data-ttu-id="11bec-149">템플릿을 합니다 `Movie` 컨트롤러 (에 *Views\Movies\DisplayTemplates* 폴더) 포맷 하는 간단한 날짜를 굵은 빨간색 텍스트로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-149">The template that's specifically for the `Movie` controller (in the *Views\Movies\DisplayTemplates* folder) displays a short date that's also formatted as bold red text.</span></span>

<span data-ttu-id="11bec-150">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-150">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="11bec-151">브라우저 응용 프로그램에 대 한 인덱스 뷰를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-151">The browser renders the Index view for the application.</span></span>

<span data-ttu-id="11bec-152">`ReleaseDate` 속성 시간 없이 굵은 빨간색 글꼴로 이제 날짜를 표시 합니다. 이렇게 확인 하면를 `DateTime` 에서 템플릿 기반 도우미는 *Views\Movies\DisplayTemplates* 를 통해 폴더를 선택 합니다 `DateTime` 공유 폴더에서 템플릿 기반 도우미 (*Views\Shared\ DisplayTemplates*).</span><span class="sxs-lookup"><span data-stu-id="11bec-152">The `ReleaseDate` property now displays the date in a bold red font without the time.This helps you confirm that the `DateTime` templated helper in the *Views\Movies\DisplayTemplates* folder is selected over the `DateTime` templated helper in the shared folder (*Views\Shared\DisplayTemplates*).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

<span data-ttu-id="11bec-153">이제 이름을 변경 합니다 *Views\Movies\DisplayTemplates\DateTime.cshtml* 파일을 *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-153">Now rename the *Views\Movies\DisplayTemplates\DateTime.cshtml* file to *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*.</span></span>

<span data-ttu-id="11bec-154">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-154">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="11bec-155">이 이번에는 `ReleaseDate` 빨간색 굵게 하지 않고 시간 날짜를 표시 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-155">This time the `ReleaseDate` property displays a date without the time and without the bold red font.</span></span> <span data-ttu-id="11bec-156">데이터의 이름을 가진 템플릿 형식 있음을 보여줍니다 (이 경우 `DateTime`)는 자동으로 해당 형식의 모든 모델 속성을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-156">This illustrates that a template that has the name of the data type (in this case `DateTime`) is automatically used to display all model properties of that type.</span></span> <span data-ttu-id="11bec-157">이름을 바꾼 후는 *DateTime.cshtml* 파일을 *LoudDateTime.cshtml*, ASP.NET에서 템플릿을 찾을 수 없는 합니다 *Views\Movies\DisplayTemplates* 폴더를 사용 하므로 합니다 *DateTime.cshtml* 템플릿에서 * Views\Movies\Shared\* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-157">After you renamed the *DateTime.cshtml* file to *LoudDateTime.cshtml*, ASP.NET no longer found a template in the *Views\Movies\DisplayTemplates* folder, so it used the *DateTime.cshtml* template from the *Views\Movies\Shared\* folder.</span></span>

<span data-ttu-id="11bec-158">(일치 하는 템플릿 이므로 대/소문자 구분, 없습니다 템플릿 파일 이름을 사용 하 여 만든 모든 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-158">(The template matching is case insensitive, so you could have created the template file name with any casing.</span></span> <span data-ttu-id="11bec-159">예를 들어 *DATETIME.chstml, datetime.cshtml*, 및 *DaTeTiMe.cshtml* 일치 모든는 `DateTime` 형식입니다.)</span><span class="sxs-lookup"><span data-stu-id="11bec-159">For example, *DATETIME.chstml, datetime.cshtml*, and *DaTeTiMe.cshtml* would all match the `DateTime` type.)</span></span>

<span data-ttu-id="11bec-160">검토 하려면:이 시점에서 `ReleaseDate` 필드를 사용 하 여 표시 되는 *Views\Movies\DisplayTemplates\DateTime.cshtml* 서식 파일을 간단한 날짜 형식을 사용 하 여 데이터를 표시 하지만 그렇지 않으면 없는 특수 형식으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-160">To review: at this point, the `ReleaseDate` field is being displayed using the *Views\Movies\DisplayTemplates\DateTime.cshtml* template, which displays the data using a short date format, but otherwise adds no special format.</span></span>

### <a name="using-uihint-to-specify-a-display-template"></a><span data-ttu-id="11bec-161">UIHint를 사용 하 여 표시 템플릿을 지정 하려면</span><span class="sxs-lookup"><span data-stu-id="11bec-161">Using UIHint to Specify a Display Template</span></span>

<span data-ttu-id="11bec-162">웹 응용 프로그램에 여러 `DateTime` 필드 및 모든 또는 대부분의 날짜 전용으로 표시 하려면 기본적으로는 *DateTime.cshtml* 템플릿은 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-162">If your web application has many `DateTime` fields and by default you want to display all or most of them in date-only format, the *DateTime.cshtml* template is a good approach.</span></span> <span data-ttu-id="11bec-163">있으 나 경우 몇 가지 날짜 전체 날짜 및 시간을 표시 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="11bec-163">But what if you have a few dates where you want to display the full date and time?</span></span> <span data-ttu-id="11bec-164">이전 버전도 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-164">No problem.</span></span> <span data-ttu-id="11bec-165">추가 템플릿을 만들고 사용할 수 있는 합니다 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 전체 날짜 및 시간에 대 한 서식을 지정 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-165">You can create an additional template and use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to specify formatting for the full date and time.</span></span> <span data-ttu-id="11bec-166">그런 다음 해당 템플릿을 선택적으로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-166">You can then selectively apply that template.</span></span> <span data-ttu-id="11bec-167">사용할 수는 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 하거나 모델 수준에서 특성에는 뷰 내에서 템플릿을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-167">You can use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute at the model level or you can specify the template inside a view.</span></span> <span data-ttu-id="11bec-168">이 섹션에서는 사용 하는 방법을 볼는 `UIHint` 특성을 선택적으로 일부 인스턴스의 날짜-시간 필드에 대 한 서식 지정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-168">In this section, you'll see how to use the `UIHint` attribute to selectively change the formatting for some instances of date-time fields.</span></span>

<span data-ttu-id="11bec-169">엽니다는 *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* 파일 및 기존 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-169">Open the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* file and replace the existing code with the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

<span data-ttu-id="11bec-170">이 표시 전체 날짜 및 시간을 사용 하면 고 녹색 크고 텍스트를 호출 하는 CSS 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-170">This causes the full date and time to be displayed and adds the CSS class that makes the text green and large.</span></span>

<span data-ttu-id="11bec-171">열기는 *Movie.cs* 파일을 추가 합니다 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 특성을 `ReleaseDate` 속성을 다음 예와에서 같이:</span><span class="sxs-lookup"><span data-stu-id="11bec-171">Open the *Movie.cs* file and add the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to the `ReleaseDate` property, as shown in the following example:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

<span data-ttu-id="11bec-172">그러면 ASP.NET MVC는 표시 될 때를 `ReleaseDate` 속성 (특히 및 되지 `DateTime` 개체)를 사용 해야 합니다 *LoudDateTime.cshtml* 템플릿.</span><span class="sxs-lookup"><span data-stu-id="11bec-172">This tells ASP.NET MVC that when it displays the `ReleaseDate` property (specifically, and not just any `DateTime` object), it should use the *LoudDateTime.cshtml* template.</span></span>

<span data-ttu-id="11bec-173">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-173">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="11bec-174">다음에 유의 합니다 `ReleaseDate` 속성 이제 날짜와 시간을 표시는 큰 녹색 글꼴로 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-174">Notice that the `ReleaseDate` property now displays the date and time in a large green font.</span></span>

<span data-ttu-id="11bec-175">돌아가서를 `UIHint` 특성을 *Movie.cs* 파일을 주석으로 처리 하므로 *LoudDateTime.cshtml* 템플릿을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-175">Return to the `UIHint` attribute in the *Movie.cs* file and comment it out so the *LoudDateTime.cshtml* template won't be used.</span></span> <span data-ttu-id="11bec-176">응용 프로그램을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-176">Run the application again.</span></span> <span data-ttu-id="11bec-177">릴리스 날짜 크고 녹색 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-177">The release date is not displayed large and green.</span></span> <span data-ttu-id="11bec-178">이 있는지 확인 합니다 *Views\Shared\DisplayTemplates\DateTime.cshtml* 템플릿이 인덱스 및 세부 정보 보기에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-178">This verifies that the *Views\Shared\DisplayTemplates\DateTime.cshtml* template is used in the Index and Details views.</span></span>

<span data-ttu-id="11bec-179">앞에서 설명한 대로 뷰의 일부 데이터의 개별 인스턴스에 템플릿을 적용할 수 있는 템플릿을 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-179">As mentioned earlier, you can also apply a template in a view, which lets you apply the template to an individual instance of some data.</span></span> <span data-ttu-id="11bec-180">엽니다는 *Views\Movies\Details.cshtml* 보기.</span><span class="sxs-lookup"><span data-stu-id="11bec-180">Open the *Views\Movies\Details.cshtml* view.</span></span> <span data-ttu-id="11bec-181">추가 `"LoudDateTime"` 의 두 번째 매개 변수로 합니다 [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) 에 대 한 호출을 `ReleaseDate` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-181">Add `"LoudDateTime"` as the second parameter of the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call for the `ReleaseDate` field.</span></span> <span data-ttu-id="11bec-182">완성된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-182">The completed code looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

<span data-ttu-id="11bec-183">이 지정 된 `LoudDateTime` 어떤 특성이 모델에 적용 되었는지에 관계 없이 모델 속성을 표시 하려면 사용 되는 템플릿.</span><span class="sxs-lookup"><span data-stu-id="11bec-183">This specifies that the `LoudDateTime` template should be used to display the model property, regardless of what attributes are applied to the model.</span></span>

<span data-ttu-id="11bec-184">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-184">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="11bec-185">영화 인덱스 페이지를 사용 하는지 확인 합니다 *Views\Shared\DisplayTemplates\DateTime.cshtml* 템플릿 (굵은 빨간색) 및 *Movie\Details* 페이지를 사용 하는 *Views\Movies\ DisplayTemplates\LoudDateTime.cshtml* 템플릿 (크고 녹색).</span><span class="sxs-lookup"><span data-stu-id="11bec-185">Verify that the movie index page is using the *Views\Shared\DisplayTemplates\DateTime.cshtml* template (red bold) and the *Movie\Details* page is using the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* template (large and green).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

<span data-ttu-id="11bec-186">다음 섹션에서는 복합 형식에 대 한 템플릿을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11bec-186">In the next section, you'll create a template for a complex type.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="11bec-187">[이전](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [다음](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="11bec-187">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span></span>
