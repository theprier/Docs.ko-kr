---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: ASP.NET MVC-2 부에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MV에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 84112316a9ace732cb7d75d7cbaeb071c72de822
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875450"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a><span data-ttu-id="be39e-103">ASP.NET MVC-2 부에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용</span><span class="sxs-lookup"><span data-stu-id="be39e-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 2</span></span>
====================
<span data-ttu-id="be39e-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="be39e-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="be39e-105">이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>


## <a name="adding-an-automatic-datetime-template"></a><span data-ttu-id="be39e-106">자동 DateTime 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="be39e-106">Adding an Automatic DateTime Template</span></span>

<span data-ttu-id="be39e-107">이 자습서의 첫 번째 부분을 명시적으로 서식을 지정 하려면 모델에 특성을 추가할 수 및 모델을 렌더링 하는 데 사용 하는 템플릿을 명시적으로 지정 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-107">In the first part of this tutorial, you saw how you can add attributes to the model to explicitly specify formatting, and how you can explicitly specify the template that's used to render the model.</span></span> <span data-ttu-id="be39e-108">예를 들어는 [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 에 다음 코드 명시적 특성에 대 한 서식을 지정는 `ReleaseDate` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-108">For example, the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute in the following code explicity specifies the formatting for the `ReleaseDate` property.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

<span data-ttu-id="be39e-109">다음 예제에서는 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성을 사용 하는 `Date` 열거형, 모델을 렌더링 하는 날짜 템플릿을 쓰일 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-109">In the following example, the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute, using the `Date` enumeration, specifies that the date template should be used to render the model.</span></span> <span data-ttu-id="be39e-110">프로젝트에서 date 템플릿이 없는 경우 기본 제공 된 날짜 템플릿이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-110">If there's no date template in your project, the built-in date template is used.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

<span data-ttu-id="be39e-111">그러나 ASP 합니다. MVC 형식 일치 규칙-조치-구성 형식의 이름을 일치 하는 템플릿을 검색 하 여 사용 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-111">However, ASP.MVC can perform type matching using convention-over-configuration, by looking for a template that matches the name of a type.</span></span> <span data-ttu-id="be39e-112">이렇게 하면 자동으로 모든 특성이 나 코드를 전혀 사용 하지 않고 데이터의 형식을 지정 하는 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-112">This lets you create a template that automatically formats data without using any attributes or code at all.</span></span> <span data-ttu-id="be39e-113">자습서의이 부분에 대 한 형식의 모델 속성에 자동으로 적용 되는 템플릿을 만듭니다 [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-113">For this part of the tutorial, you'll create a template that's automatically applied to model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span> <span data-ttu-id="be39e-114">형식의 모든 모델 속성을 렌더링 하는 템플릿 쓰일 수를 지정 하는 특성 또는 다른 구성을 사용할 필요가 없습니다 [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-114">You won't need to use an attribute or other configuration to specify that the template should be used to render all model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span>

<span data-ttu-id="be39e-115">또한 개별 속성 또는 개별 필드의 표시를 사용자 지정 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-115">You'll also learn a way to customize the display of individual properties or even individual fields.</span></span>

<span data-ttu-id="be39e-116">를 시작 하려면 기존 서식 지정 정보를 제거 하 고 응용 프로그램의 전체 날짜 표시 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-116">To begin, let's remove existing formatting information and display full dates in the application.</span></span>

<span data-ttu-id="be39e-117">열기는 *Movie.cs* 파일을 주석으로 처리는 `DataType` 특성에 `ReleaseDate` 속성:</span><span class="sxs-lookup"><span data-stu-id="be39e-117">Open the *Movie.cs* file and comment out the `DataType` attribute on the `ReleaseDate` property:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

<span data-ttu-id="be39e-118">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-118">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="be39e-119">에 `ReleaseDate` 속성 없는 서식 지정 정보를 제공 하는 경우 기본값 이기 때문에 해당 날짜와 시간을 이제 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-119">Notice that the `ReleaseDate` property now displays both the date and time, because that's the default when no formatting information is provided.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a><span data-ttu-id="be39e-120">새 서식 파일을 테스트 하기 위한 CSS 스타일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-120">Adding CSS Styles for Testing New Templates</span></span>

<span data-ttu-id="be39e-121">날짜 형식 지정에 대 한 템플릿을 만들기 전에 새 템플릿을 적용할 수 있는 몇 가지 CSS 스타일 규칙을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-121">Before you create a template for formatting dates, you'll add a few CSS style rules that you can apply to the new templates.</span></span> <span data-ttu-id="be39e-122">이러한 렌더링된 된 페이지는 새 템플릿을 사용 하 고 있는지 확인 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-122">These will help you verify that the rendered page is using the new template.</span></span>

<span data-ttu-id="be39e-123">열기는 *Content\Site.cs*s 파일을 파일의 맨 아래에 다음과 같은 CSS 규칙을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-123">Open the *Content\Site.cs*s file and add the following CSS rules to the bottom of the file:</span></span>

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a><span data-ttu-id="be39e-124">날짜/시간 표시 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="be39e-124">Adding DateTime Display Templates</span></span>

<span data-ttu-id="be39e-125">이제 새 서식 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-125">Now you can create the new template.</span></span> <span data-ttu-id="be39e-126">에 *Views\Movies* 폴더를 만들는 *DisplayTemplates* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-126">In the *Views\Movies* folder, create a *DisplayTemplates* folder.</span></span>

<span data-ttu-id="be39e-127">에 *Views\Shared* 폴더를 만들는 *DisplayTemplates* 폴더 및 *EditorTemplates* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-127">In the *Views\Shared* folder, create a *DisplayTemplates* folder and an *EditorTemplates* folder.</span></span>

<span data-ttu-id="be39e-128">표시 템플릿은 *Views\Shared\DisplayTemplates* 폴더 모든 컨트롤러에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-128">The display templates in the *Views\Shared\DisplayTemplates* folder will be used by all controllers.</span></span> <span data-ttu-id="be39e-129">표시 템플릿은 *Views\Movie\DisplayTemplates* 폴더에만 사용 됩니다는 `Movie` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-129">The display templates in the *Views\Movie\DisplayTemplates* folder will be used only by the `Movie` controller.</span></span> <span data-ttu-id="be39e-130">(동일한 이름의 템플릿이 두 폴더에서 서식 파일에 표시 되 면는 *Views\Movie\DisplayTemplates* 폴더-즉, 더 구체적인 서식 파일-에서 반환 된 뷰에 대 한 우선는 `Movie` 컨트롤러입니다.)</span><span class="sxs-lookup"><span data-stu-id="be39e-130">(If a template with the same name appears in both folders, the template in the *Views\Movie\DisplayTemplates* folder — that is, the more specific template — takes precedence for views returned by the `Movie` controller.)</span></span>

<span data-ttu-id="be39e-131">**솔루션 탐색기**를 확장 하 고는 *뷰* 폴더를 확장 하 고는 *Shared* 폴더를 마우스 오른쪽 단추로 *Views\Shared\DisplayTemplates* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-131">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\DisplayTemplates* folder.</span></span>

<span data-ttu-id="be39e-132">클릭 **추가** 클릭 하 고 **보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-132">Click **Add** and then click **View**.</span></span> <span data-ttu-id="be39e-133">**뷰 추가** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-133">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="be39e-134">에 **뷰 이름** 상자에서 입력 `DateTime`합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-134">In the **View name** box, type `DateTime`.</span></span> <span data-ttu-id="be39e-135">(형식의 이름을 찾을 수 있도록이 이름을 사용 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="be39e-135">(You must use this name in order to match the name of the type.)</span></span>

<span data-ttu-id="be39e-136">선택 된 **부분 뷰로 만들기** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-136">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="be39e-137">다음 사항을 확인는 **레이아웃 또는 마스터 페이지를 사용 하 여** 및 **강력한 형식의 뷰 만들기** 확인란을 선택 하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-137">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

<span data-ttu-id="be39e-138">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-138">Click **Add**.</span></span> <span data-ttu-id="be39e-139">A *DateTime.cshtml* 템플릿이에 생성 되는 *Views\Shared\DisplayTemplates*합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-139">A *DateTime.cshtml* template is created in the *Views\Shared\DisplayTemplates*.</span></span>

<span data-ttu-id="be39e-140">다음 그림에서는 *뷰* 폴더에 **솔루션 탐색기** 후는 `DateTime` 표시 및 편집기 템플릿은 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-140">The following image shows the *Views* folder in **Solution Explorer** after the `DateTime` display and editor templates are created.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

<span data-ttu-id="be39e-141">열기는 *Views\Shared\DisplayTemplates\DateTime.cshtml* 파일을 사용 하 여 다음 태그를 추가 [String.Format](https://msdn.microsoft.com/library/system.string.format.aspx) 메서드는 시간을 제외한 날짜가으로 속성을 지정 하려면.</span><span class="sxs-lookup"><span data-stu-id="be39e-141">Open the *Views\Shared\DisplayTemplates\DateTime.cshtml* file and add the following markup, which uses the [String.Format](https://msdn.microsoft.com/library/system.string.format.aspx) method to format the property as a date without the time.</span></span> <span data-ttu-id="be39e-142">(의 `{0:d}` 형식은 간단한 날짜 서식을 지정 합니다.)</span><span class="sxs-lookup"><span data-stu-id="be39e-142">(The `{0:d}` format specifies short date format.)</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

<span data-ttu-id="be39e-143">이 단계를 반복 만듭니다는 `DateTime` 에서 서식 파일의 *Views\Movie\DisplayTemplates* 폴더.</span><span class="sxs-lookup"><span data-stu-id="be39e-143">Repeat this step to create a `DateTime` template in the *Views\Movie\DisplayTemplates* folder.</span></span> <span data-ttu-id="be39e-144">다음 코드를 사용 하 여는 *Views\Movie\DisplayTemplates\DateTime.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-144">Use the following code in the *Views\Movie\DisplayTemplates\DateTime.cshtml* file.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

<span data-ttu-id="be39e-145">`loud-1` CSS 클래스 때문에 해당 날짜가 굵은 빨간색 텍스트로 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-145">The `loud-1` CSS class causes the date to be display in bold red text.</span></span> <span data-ttu-id="be39e-146">추가한는 `loud-1` 이 특정 템플릿이 사용 되는 경우 쉽게 확인할 수 있도록은 임시 방책와 마찬가지로 CSS 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-146">You added the `loud-1` CSS class just as a temporary measure so you can easily see when this particular template is being used.</span></span>

<span data-ttu-id="be39e-147">완료 했으면 생성 되 고 사용자 지정 된 날짜를 표시 하도록 ASP.NET에서 사용할 템플릿.</span><span class="sxs-lookup"><span data-stu-id="be39e-147">What you've done is created and customized templates that ASP.NET will use to display dates.</span></span> <span data-ttu-id="be39e-148">보다 일반적인 서식 파일 (에 *Views\Shared\DisplayTemplates* 폴더) 단순 하 고 간단한 날짜를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-148">The more general template (in the *Views\Shared\DisplayTemplates* folder) displays a simple short date.</span></span> <span data-ttu-id="be39e-149">서식 파일을 대상으로 `Movie` 컨트롤러 (에 *Views\Movies\DisplayTemplates* 폴더) 포맷 하 고 간단한 날짜를 굵은 빨간색 텍스트로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-149">The template that's specifically for the `Movie` controller (in the *Views\Movies\DisplayTemplates* folder) displays a short date that's also formatted as bold red text.</span></span>

<span data-ttu-id="be39e-150">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-150">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="be39e-151">브라우저 응용 프로그램에 대 한 인덱스 뷰를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-151">The browser renders the Index view for the application.</span></span>

<span data-ttu-id="be39e-152">`ReleaseDate` 속성 이제는 시간을 제외한 굵은 빨간색 글꼴로 날짜를 표시 합니다. 이렇게 하면 확인는 `DateTime` 에서 템플릿 기반 도우미는 *Views\Movies\DisplayTemplates* 통해 폴더를 선택는 `DateTime` 공유 폴더에서 템플릿 기반 도우미 (*Views\Shared\ DisplayTemplates*).</span><span class="sxs-lookup"><span data-stu-id="be39e-152">The `ReleaseDate` property now displays the date in a bold red font without the time.This helps you confirm that the `DateTime` templated helper in the *Views\Movies\DisplayTemplates* folder is selected over the `DateTime` templated helper in the shared folder (*Views\Shared\DisplayTemplates*).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

<span data-ttu-id="be39e-153">이름을 바꿀는 *Views\Movies\DisplayTemplates\DateTime.cshtml* 파일을 *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-153">Now rename the *Views\Movies\DisplayTemplates\DateTime.cshtml* file to *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*.</span></span>

<span data-ttu-id="be39e-154">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-154">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="be39e-155">이 현재는 `ReleaseDate` 속성 시간 및 굵은 빨간색 글꼴로 없는 날짜를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-155">This time the `ReleaseDate` property displays a date without the time and without the bold red font.</span></span> <span data-ttu-id="be39e-156">데이터의 이름이 있는 서식 파일을 입력할 들 (이 경우 `DateTime`) 자동으로 해당 형식의 모든 모델 속성을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-156">This illustrates that a template that has the name of the data type (in this case `DateTime`) is automatically used to display all model properties of that type.</span></span> <span data-ttu-id="be39e-157">이름을 바꾼 후는 *DateTime.cshtml* 파일을 *LoudDateTime.cshtml*, ASP.NET에는 더 이상에서 템플릿을 찾을 수는 *Views\Movies\DisplayTemplates* 있으므로 사용할 폴더 *DateTime.cshtml* 에서 서식 파일은 * Views\Movies\Shared\* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-157">After you renamed the *DateTime.cshtml* file to *LoudDateTime.cshtml*, ASP.NET no longer found a template in the *Views\Movies\DisplayTemplates* folder, so it used the *DateTime.cshtml* template from the *Views\Movies\Shared\* folder.</span></span>

<span data-ttu-id="be39e-158">(일치 하는 서식 파일 이므로 대/소문자 구분을 만들 수는 템플릿 파일 이름 모두 대/소문자.</span><span class="sxs-lookup"><span data-stu-id="be39e-158">(The template matching is case insensitive, so you could have created the template file name with any casing.</span></span> <span data-ttu-id="be39e-159">예를 들어 *DATETIME.chstml, datetime.cshtml*, 및 *DaTeTiMe.cshtml* 모두 일치는 `DateTime` 유형입니다.)</span><span class="sxs-lookup"><span data-stu-id="be39e-159">For example, *DATETIME.chstml, datetime.cshtml*, and *DaTeTiMe.cshtml* would all match the `DateTime` type.)</span></span>

<span data-ttu-id="be39e-160">검토 하려면:이 시점에서 `ReleaseDate` 필드를 사용 하 여 표시 되는 *Views\Movies\DisplayTemplates\DateTime.cshtml* 템플릿을 간단한 날짜 서식을 사용 하 여 데이터를 표시 하지만 그렇지 않은 경우 추가 하는 특별 한 형식이 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-160">To review: at this point, the `ReleaseDate` field is being displayed using the *Views\Movies\DisplayTemplates\DateTime.cshtml* template, which displays the data using a short date format, but otherwise adds no special format.</span></span>

### <a name="using-uihint-to-specify-a-display-template"></a><span data-ttu-id="be39e-161">UIHint를 사용 하 여 디스플레이 템플릿을 지정 하려면</span><span class="sxs-lookup"><span data-stu-id="be39e-161">Using UIHint to Specify a Display Template</span></span>

<span data-ttu-id="be39e-162">웹 응용 프로그램에 많은 경우 `DateTime` 필드 전체 또는 대부분의 날짜 전용으로 표시 하려면 기본적으로는 *DateTime.cshtml* 서식 파일에 있는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-162">If your web application has many `DateTime` fields and by default you want to display all or most of them in date-only format, the *DateTime.cshtml* template is a good approach.</span></span> <span data-ttu-id="be39e-163">하지만 훨씬 쉽게 몇 가지 날짜 전체 날짜 및 시간을 표시 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="be39e-163">But what if you have a few dates where you want to display the full date and time?</span></span> <span data-ttu-id="be39e-164">이전 버전도 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-164">No problem.</span></span> <span data-ttu-id="be39e-165">추가 템플릿을 만들고 사용 하는 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 전체 날짜 및 시간에 대 한 서식을 지정 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-165">You can create an additional template and use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to specify formatting for the full date and time.</span></span> <span data-ttu-id="be39e-166">그런 다음 해당 템플릿을 선택적으로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-166">You can then selectively apply that template.</span></span> <span data-ttu-id="be39e-167">사용할 수는 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 이거나 모델 수준에서 특성 보기 내 파일을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-167">You can use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute at the model level or you can specify the template inside a view.</span></span> <span data-ttu-id="be39e-168">이 섹션에 사용 하는 방법을 표시 됩니다는 `UIHint` 특성을 선택적으로 날짜-시간 필드의 일부 인스턴스에 대 한 서식을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-168">In this section, you'll see how to use the `UIHint` attribute to selectively change the formatting for some instances of date-time fields.</span></span>

<span data-ttu-id="be39e-169">열기는 *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* 파일 및 기존 코드를 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-169">Open the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* file and replace the existing code with the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

<span data-ttu-id="be39e-170">전체 날짜 및 시간을 표시할 하면 녹색과 큰 텍스트를 호출 하는 CSS 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-170">This causes the full date and time to be displayed and adds the CSS class that makes the text green and large.</span></span>

<span data-ttu-id="be39e-171">열기는 *Movie.cs* 파일을 추가 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 특성을 `ReleaseDate` 속성을 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="be39e-171">Open the *Movie.cs* file and add the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to the `ReleaseDate` property, as shown in the following example:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

<span data-ttu-id="be39e-172">그러면 ASP.NET MVC를 표시 하는 경우는 `ReleaseDate` 속성 (특히, 및 아닌 `DateTime` 개체)를 사용 해야는 *LoudDateTime.cshtml* 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-172">This tells ASP.NET MVC that when it displays the `ReleaseDate` property (specifically, and not just any `DateTime` object), it should use the *LoudDateTime.cshtml* template.</span></span>

<span data-ttu-id="be39e-173">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-173">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="be39e-174">에 `ReleaseDate` 속성 이제 날짜와 시간을 표시 녹색를 큰 글꼴로 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-174">Notice that the `ReleaseDate` property now displays the date and time in a large green font.</span></span>

<span data-ttu-id="be39e-175">으로 돌아와서는 `UIHint` 특성에 *Movie.cs* 파일을 주석으로 처리 하므로 *LoudDateTime.cshtml* 서식 파일 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-175">Return to the `UIHint` attribute in the *Movie.cs* file and comment it out so the *LoudDateTime.cshtml* template won't be used.</span></span> <span data-ttu-id="be39e-176">응용 프로그램을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-176">Run the application again.</span></span> <span data-ttu-id="be39e-177">릴리스 날짜 광범위 하 고 녹색 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-177">The release date is not displayed large and green.</span></span> <span data-ttu-id="be39e-178">이 확인은 *Views\Shared\DisplayTemplates\DateTime.cshtml* 템플릿은 인덱스 및 세부 정보 보기에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-178">This verifies that the *Views\Shared\DisplayTemplates\DateTime.cshtml* template is used in the Index and Details views.</span></span>

<span data-ttu-id="be39e-179">앞서 언급 했 듯이 개별 인스턴스의 일부 데이터에 템플릿을 적용할 수 있는 보기에서 서식 파일을 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-179">As mentioned earlier, you can also apply a template in a view, which lets you apply the template to an individual instance of some data.</span></span> <span data-ttu-id="be39e-180">열기는 *Views\Movies\Details.cshtml* 보기.</span><span class="sxs-lookup"><span data-stu-id="be39e-180">Open the *Views\Movies\Details.cshtml* view.</span></span> <span data-ttu-id="be39e-181">추가 `"LoudDateTime"` 의 두 번째 매개 변수로 [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) 에 대 한 호출에서 `ReleaseDate` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-181">Add `"LoudDateTime"` as the second parameter of the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call for the `ReleaseDate` field.</span></span> <span data-ttu-id="be39e-182">완성된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-182">The completed code looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

<span data-ttu-id="be39e-183">이 지정 하는 `LoudDateTime` 어떤 특성이 모델에 적용 되었는지에 관계 없이 모델 속성을 표시 하려면 서식 파일을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-183">This specifies that the `LoudDateTime` template should be used to display the model property, regardless of what attributes are applied to the model.</span></span>

<span data-ttu-id="be39e-184">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-184">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="be39e-185">영화 인덱스 페이지를 사용 하는지 확인는 *Views\Shared\DisplayTemplates\DateTime.cshtml* 서식 파일 (굵은 빨간색) 및 *Movie\Details* 페이지를 사용 하는 *Views\Movies\ DisplayTemplates\LoudDateTime.cshtml* 서식 파일 (대형 및 녹색).</span><span class="sxs-lookup"><span data-stu-id="be39e-185">Verify that the movie index page is using the *Views\Shared\DisplayTemplates\DateTime.cshtml* template (red bold) and the *Movie\Details* page is using the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* template (large and green).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

<span data-ttu-id="be39e-186">다음 섹션에서는 복합 유형에 대 한 서식 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be39e-186">In the next section, you'll create a template for a complex type.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="be39e-187">[이전](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [다음](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="be39e-187">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span></span>
