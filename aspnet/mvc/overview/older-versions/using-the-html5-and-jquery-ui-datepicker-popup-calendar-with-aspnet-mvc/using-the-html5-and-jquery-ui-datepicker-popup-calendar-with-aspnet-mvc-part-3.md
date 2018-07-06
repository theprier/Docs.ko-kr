---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: 3 부-ASP.NET MVC에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker 팝업 일정을 ASP.NET MV에서 사용 하는 방법의 기본 사항을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: 27bbc4e1df6e26eed66680d596d13863dfab5db0
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37812272"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a><span data-ttu-id="04080-103">3 부-ASP.NET MVC에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용</span><span class="sxs-lookup"><span data-stu-id="04080-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 3</span></span>
====================
<span data-ttu-id="04080-104">[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="04080-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="04080-105">이 자습서는 편집기 템플릿, 표시 템플릿 및 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정을 사용 하는 방법의 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="04080-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>


## <a name="working-with-complex-types"></a><span data-ttu-id="04080-106">복합 형식 사용</span><span class="sxs-lookup"><span data-stu-id="04080-106">Working with Complex Types</span></span>

<span data-ttu-id="04080-107">이 섹션의 address 클래스를 만들고 표시 하는 템플릿을 만드는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="04080-107">In this section you'll create an address class and learn how to create a template to display it.</span></span>

<span data-ttu-id="04080-108">에 *모델* 폴더를 라는 새 클래스 파일을 만듭니다 *Person.cs* 배치할 두 형식:를 `Person` 클래스 및 `Address` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="04080-108">In the *Models* folder, create a new class file named *Person.cs* where you'll put two types: a `Person` class and an `Address` class.</span></span> <span data-ttu-id="04080-109">합니다 `Person` 클래스와 형식화 된 속성이 포함 됩니다 `Address`합니다.</span><span class="sxs-lookup"><span data-stu-id="04080-109">The `Person` class will contain a property that's typed as `Address`.</span></span> <span data-ttu-id="04080-110">합니다 `Address` 형식은 복합 형식, 즉 같은 기본 제공 형식 중 하나가 아닙니다 `int`를 `string`, 또는 `double`합니다.</span><span class="sxs-lookup"><span data-stu-id="04080-110">The `Address` type is a complex type, meaning it's not one of the built-in types like `int`, `string`, or `double`.</span></span> <span data-ttu-id="04080-111">대신 여러 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04080-111">Instead, it has several properties.</span></span> <span data-ttu-id="04080-112">새 클래스에 대 한 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="04080-112">The code for the new classes looks like this:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

<span data-ttu-id="04080-113">에 `Movie` 컨트롤러에는 다음 추가 `PersonDetail` 사용자 인스턴스를 표시 하는 작업:</span><span class="sxs-lookup"><span data-stu-id="04080-113">In the `Movie` controller, add the following `PersonDetail` action to display a person instance:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

<span data-ttu-id="04080-114">에 다음 코드를 추가 합니다 `Movie` 채우는 데 컨트롤러는 `Person` 몇 가지 샘플 데이터를 사용 하 여 모델:</span><span class="sxs-lookup"><span data-stu-id="04080-114">Then add the following code to the `Movie` controller to populate the `Person` model with some sample data:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

<span data-ttu-id="04080-115">열기는 *Views\Movies\PersonDetail.cshtml* 파일을 다음 태그를 추가 합니다 `PersonDetail` 보기.</span><span class="sxs-lookup"><span data-stu-id="04080-115">Open the *Views\Movies\PersonDetail.cshtml* file and add the following markup for the `PersonDetail` view.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

<span data-ttu-id="04080-116">Ctrl + F5 키를 눌러 응용 프로그램을 실행 하 고 이동 *영화/PersonDetail*합니다.</span><span class="sxs-lookup"><span data-stu-id="04080-116">Press Ctrl+F5 to run the application and navigate to *Movies/PersonDetail*.</span></span>

<span data-ttu-id="04080-117">`PersonDetail` 보기를 포함 하지 않습니다는 `Address` 복합 형식을 볼 수 있듯이이 스크린샷에 합니다.</span><span class="sxs-lookup"><span data-stu-id="04080-117">The `PersonDetail` view doesn't contain the `Address` complex type, as you can see in this screenshot.</span></span> <span data-ttu-id="04080-118">(주소 없음 표시 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="04080-118">(No address is shown.)</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

<span data-ttu-id="04080-119">`Address` 복합 유형 이므로 모델 데이터가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04080-119">The `Address` model data is not displayed because it's a complex type.</span></span> <span data-ttu-id="04080-120">주소 정보를 표시 하려면 열을 *Views\Movies\PersonDetail.cshtml* 다시 파일을 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="04080-120">To display the address information, open the *Views\Movies\PersonDetail.cshtml* file again and add the following markup.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

<span data-ttu-id="04080-121">전체 태그를는 `PersonDetail` 이제 뷰는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="04080-121">The complete markup for the `PersonDetail` now view looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

<span data-ttu-id="04080-122">응용 프로그램을 다시 실행 하 고 표시 된 `PersonDetail` 보기.</span><span class="sxs-lookup"><span data-stu-id="04080-122">Run the application again and display the `PersonDetail` view.</span></span> <span data-ttu-id="04080-123">주소 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04080-123">The address information is now displayed:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a><span data-ttu-id="04080-124">복합 형식에 대 한 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="04080-124">Creating a Template for a Complex Type</span></span>

<span data-ttu-id="04080-125">이 섹션에서는 렌더링 하는 데 사용할 템플릿으로 만듭니다는 `Address` 복합 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="04080-125">In this section you'll create a template that will be used to render the `Address` complex type.</span></span> <span data-ttu-id="04080-126">에 대 한 템플릿을 만들 때의 `Address` 형식, ASP.NET MVC 자동으로 사용 하 여 응용 프로그램에서 임의의 위치를 주소 모델 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04080-126">When you create a template for the `Address` type, ASP.NET MVC can automatically use it to format an address model anywhere in the application.</span></span> <span data-ttu-id="04080-127">이렇게 하면 렌더링을 제어 하는 방법의 `Address` 응용 프로그램의 한 위치에서 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="04080-127">This gives you a way to control the rendering of the `Address` type from just one place in the application.</span></span>

<span data-ttu-id="04080-128">에 *Views\Shared\DisplayTemplates* 폴더를 명명 된 강력한 형식의 부분 보기를 만들 **주소**:</span><span class="sxs-lookup"><span data-stu-id="04080-128">In the *Views\Shared\DisplayTemplates* folder, create a strongly typed partial view named **Address**:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

<span data-ttu-id="04080-129">클릭 **추가**를 연 다음 새 *Views\Shared\DisplayTemplates\Address.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="04080-129">Click **Add**, and then open the new *Views\Shared\DisplayTemplates\Address.cshtml* file.</span></span> <span data-ttu-id="04080-130">다음 생성 된 태그를 포함 하는 새 보기:</span><span class="sxs-lookup"><span data-stu-id="04080-130">The new view contains the following generated markup:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

<span data-ttu-id="04080-131">응용 프로그램을 실행 하 고 표시 된 `PersonDetail` 보기.</span><span class="sxs-lookup"><span data-stu-id="04080-131">Run the application and display the `PersonDetail` view.</span></span> <span data-ttu-id="04080-132">이 이번에는 `Address` 방금 만든 템플릿 표시 되는 `Address` 표시를 다음과 같이 표시 되도록 복합 형식:</span><span class="sxs-lookup"><span data-stu-id="04080-132">This time, the `Address` template that you just created is used to display the `Address` complex type, so the display looks like the following:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a><span data-ttu-id="04080-133">요약: 모델 표시 형식 및 서식 파일을 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="04080-133">Summary: Ways to Specify the Model Display Format and Template</span></span>

<span data-ttu-id="04080-134">다음 방법 중 하나를 사용 하 여 형식 또는 모델 속성에 대 한 템플릿을 지정할 수 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="04080-134">You've seen that you can specify the format or template for a model property by using the following approaches:</span></span>

- <span data-ttu-id="04080-135">적용 된 `DisplayFormat` 특성을 모델의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="04080-135">Applying the `DisplayFormat` attribute to a property in the model.</span></span> <span data-ttu-id="04080-136">예를 들어, 다음 코드는 시간을 제외한 표시할 날짜를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="04080-136">For example, the following code causes the date to be displayed without the time:</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- <span data-ttu-id="04080-137">적용을 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성의 속성에 모델 및 데이터 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04080-137">Applying a [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute to a property in the model and specifying the data type.</span></span> <span data-ttu-id="04080-138">예를 들어, 다음 코드는 시간을 제외한 표시할 날짜를 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04080-138">For example, the following code causes the date to be displayed without the time.</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    <span data-ttu-id="04080-139">응용 프로그램을 포함 하는 경우는 *date.cshtml* 에서 서식 파일을 *Views\Shared\DisplayTemplates* 폴더 또는 *Views\Movies\DisplayTemplates* 폴더에서 해당 템플릿을 렌더링 하는 데 사용할는 `DateTime` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="04080-139">If the application contains a *date.cshtml* template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder, that template will be used to render the `DateTime` property.</span></span> <span data-ttu-id="04080-140">그렇지 않은 경우 기본 제공 ASP.NET 템플릿 시스템 날짜 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="04080-140">Otherwise the built-in ASP.NET templating system displays the property as a date.</span></span>
- <span data-ttu-id="04080-141">표시 템플릿 만들기를 *Views\Shared\DisplayTemplates* 폴더 또는 *Views\Movies\DisplayTemplates* 폴더 이름이 서식을 지정 하려는 데이터 형식과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="04080-141">Creating a display template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder whose name matches the data type that you want to format.</span></span> <span data-ttu-id="04080-142">살펴본 예를 들어 합니다 *Views\Shared\DisplayTemplates\DateTime.cshtml* 렌더링 하는 데 사용 된 `DateTime` 보기에 태그를 추가 하지 않고 모델에 특성을 추가 하지 않고 모델의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="04080-142">For example, you saw that the *Views\Shared\DisplayTemplates\DateTime.cshtml* was used to render `DateTime` properties in a model, without adding an attribute to the model and without adding any markup to views.</span></span>
- <span data-ttu-id="04080-143">사용 하는 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 모델 속성을 표시 하려면 서식 파일을 지정 하려면 모델에는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="04080-143">Using the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute on the model to specify the template to display the model property.</span></span>
- <span data-ttu-id="04080-144">표시 템플릿 이름을 명시적으로 추가 합니다 [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) 보기에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="04080-144">Explicitly adding the display template name to the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call in a view.</span></span>

<span data-ttu-id="04080-145">응용 프로그램에서 작업을 수행 해야 하는 항목에 사용 하는 방법에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="04080-145">The approach you use depends on what you need to do in your application.</span></span> <span data-ttu-id="04080-146">혼합 해야 하는 서식 지정의 종류를 정확히 얻으려면 이러한 접근 방식은 일반적이 지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04080-146">It's not uncommon to mix these approaches to get exactly the kind of formatting that you need.</span></span>

<span data-ttu-id="04080-147">다음 섹션에서 전환 하 여 약간 다뤄을 입력 하는 방법을 사용자 지정 데이터 표시 방법을 사용자 지정으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="04080-147">In the next section, you'll switch gears a bit and move from customizing how data is displayed to customizing how it's entered.</span></span> <span data-ttu-id="04080-148">날짜를 지정 하는 능률적인 방법을 제공 하기 위해 응용 프로그램에서 편집 보기로 jQuery datepicker에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04080-148">You'll hook up the jQuery datepicker to the edit views in the application in order to provide a slick way to specify dates.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="04080-149">[이전](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [다음](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="04080-149">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span></span>
