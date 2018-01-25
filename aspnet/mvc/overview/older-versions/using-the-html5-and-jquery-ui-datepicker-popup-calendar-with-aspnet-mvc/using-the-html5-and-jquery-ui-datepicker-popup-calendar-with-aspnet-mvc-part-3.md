---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: "ASP.NET MVC-3 부 HTML5 및 jQuery UI Datepicker 팝업 일정 사용 | Microsoft Docs"
author: Rick-Anderson
description: "이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MV에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: 7d4ed67254c2b0fc2aef748cfab1c8f628b25641
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a><span data-ttu-id="2872b-103">ASP.NET MVC-3 부 HTML5 및 jQuery UI Datepicker 팝업 일정 사용</span><span class="sxs-lookup"><span data-stu-id="2872b-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 3</span></span>
====================
<span data-ttu-id="2872b-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="2872b-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="2872b-105">이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>


## <a name="working-with-complex-types"></a><span data-ttu-id="2872b-106">복합 형식 사용</span><span class="sxs-lookup"><span data-stu-id="2872b-106">Working with Complex Types</span></span>

<span data-ttu-id="2872b-107">이 섹션에서는 주소 클래스를 만드는 하 고 표시 하는 템플릿을 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-107">In this section you'll create an address class and learn how to create a template to display it.</span></span>

<span data-ttu-id="2872b-108">에 *모델* 폴더를 라는 새 클래스 파일을 만들 *Person.cs* 두 유형이 넣습니다:는 `Person` 클래스 및 `Address` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-108">In the *Models* folder, create a new class file named *Person.cs* where you'll put two types: a `Person` class and an `Address` class.</span></span> <span data-ttu-id="2872b-109">`Person` 클래스도 형식화 된 속성에 포함 될 `Address`합니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-109">The `Person` class will contain a property that's typed as `Address`.</span></span> <span data-ttu-id="2872b-110">`Address` 형식이 같은 기본 제공 형식 중 하나가 아니므로 의미 하는 복합 유형을 `int`, `string`, 또는 `double`합니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-110">The `Address` type is a complex type, meaning it's not one of the built-in types like `int`, `string`, or `double`.</span></span> <span data-ttu-id="2872b-111">대신에 몇 가지 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-111">Instead, it has several properties.</span></span> <span data-ttu-id="2872b-112">새 클래스에 대 한 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-112">The code for the new classes looks like this:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

<span data-ttu-id="2872b-113">에 `Movie` 컨트롤러에는 다음 추가 `PersonDetail` 사용자 인스턴스를 표시 하는 작업:</span><span class="sxs-lookup"><span data-stu-id="2872b-113">In the `Movie` controller, add the following `PersonDetail` action to display a person instance:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

<span data-ttu-id="2872b-114">다음 코드를 추가 `Movie` 를 채우는 컨트롤러는 `Person` 예제 데이터 모델:</span><span class="sxs-lookup"><span data-stu-id="2872b-114">Then add the following code to the `Movie` controller to populate the `Person` model with some sample data:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

<span data-ttu-id="2872b-115">열기는 *Views\Movies\PersonDetail.cshtml* 파일에 대 한 다음 태그를 추가 하 고는 `PersonDetail` 보기.</span><span class="sxs-lookup"><span data-stu-id="2872b-115">Open the *Views\Movies\PersonDetail.cshtml* file and add the following markup for the `PersonDetail` view.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

<span data-ttu-id="2872b-116">Ctrl + f 5를 눌러 응용 프로그램을 실행 하 여 탐색 하 *영화/PersonDetail*합니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-116">Press Ctrl+F5 to run the application and navigate to *Movies/PersonDetail*.</span></span>

<span data-ttu-id="2872b-117">`PersonDetail` 보기 포함 되어 있지 않습니다는 `Address` 복합 유형을 볼 수 있듯이이 스크린 샷에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-117">The `PersonDetail` view doesn't contain the `Address` complex type, as you can see in this screenshot.</span></span> <span data-ttu-id="2872b-118">(주소가 없는 표시 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="2872b-118">(No address is shown.)</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

<span data-ttu-id="2872b-119">`Address` 복합 유형 이므로 모델 데이터가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-119">The `Address` model data is not displayed because it's a complex type.</span></span> <span data-ttu-id="2872b-120">주소 정보를 표시 하려면 열에서 *Views\Movies\PersonDetail.cshtml* 다시 파일을 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-120">To display the address information, open the *Views\Movies\PersonDetail.cshtml* file again and add the following markup.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

<span data-ttu-id="2872b-121">에 대 한 전체 태그는 `PersonDetail` 이제 보기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-121">The complete markup for the `PersonDetail` now view looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

<span data-ttu-id="2872b-122">응용 프로그램을 다시 실행 하 고 표시 된 `PersonDetail` 보기.</span><span class="sxs-lookup"><span data-stu-id="2872b-122">Run the application again and display the `PersonDetail` view.</span></span> <span data-ttu-id="2872b-123">주소 정보는 이제 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-123">The address information is now displayed:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a><span data-ttu-id="2872b-124">복합 형식에 대 한 서식 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="2872b-124">Creating a Template for a Complex Type</span></span>

<span data-ttu-id="2872b-125">이 섹션에서는 렌더링에 사용 되는 템플릿을 만듭니다는 `Address` 복합 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-125">In this section you'll create a template that will be used to render the `Address` complex type.</span></span> <span data-ttu-id="2872b-126">에 대 한 템플릿을 만들 때의 `Address` 유형, ASP.NET MVC 자동으로 사용할 수는 주소 모델은 응용 프로그램의 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-126">When you create a template for the `Address` type, ASP.NET MVC can automatically use it to format an address model anywhere in the application.</span></span> <span data-ttu-id="2872b-127">이렇게 하면 렌더링을 제어 하는 방법의 `Address` 응용 프로그램에서 한 장소에서 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-127">This gives you a way to control the rendering of the `Address` type from just one place in the application.</span></span>

<span data-ttu-id="2872b-128">에 *Views\Shared\DisplayTemplates* 폴더 라는 강력한 형식의 부분 뷰를 만들 **주소**:</span><span class="sxs-lookup"><span data-stu-id="2872b-128">In the *Views\Shared\DisplayTemplates* folder, create a strongly typed partial view named **Address**:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

<span data-ttu-id="2872b-129">클릭 **추가**를 연 다음 새 *Views\Shared\DisplayTemplates\Address.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-129">Click **Add**, and then open the new *Views\Shared\DisplayTemplates\Address.cshtml* file.</span></span> <span data-ttu-id="2872b-130">새 보기는 다음과 같은 생성 된 태그가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-130">The new view contains the following generated markup:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

<span data-ttu-id="2872b-131">응용 프로그램을 실행 하 고 표시 된 `PersonDetail` 보기.</span><span class="sxs-lookup"><span data-stu-id="2872b-131">Run the application and display the `PersonDetail` view.</span></span> <span data-ttu-id="2872b-132">이 이번에는 `Address` 방금 만든 서식 파일은 표시 하는 데 사용 되는 `Address` 복합 형식 이므로 표시는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-132">This time, the `Address` template that you just created is used to display the `Address` complex type, so the display looks like the following:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a><span data-ttu-id="2872b-133">요약: 모델 표시 형식 및 서식 파일을 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2872b-133">Summary: Ways to Specify the Model Display Format and Template</span></span>

<span data-ttu-id="2872b-134">다음 방법 중 하나를 사용 하 여 형식 또는 모델 속성에 대 한 템플릿을 지정할 수 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-134">You've seen that you can specify the format or template for a model property by using the following approaches:</span></span>

- <span data-ttu-id="2872b-135">적용 된 `DisplayFormat` 특성 모델의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-135">Applying the `DisplayFormat` attribute to a property in the model.</span></span> <span data-ttu-id="2872b-136">예를 들어 다음 코드는 시간을 제외 표시할 날짜를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-136">For example, the following code causes the date to be displayed without the time:</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- <span data-ttu-id="2872b-137">적용 한 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성 데이터 형식 지정 및 모델에 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-137">Applying a [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute to a property in the model and specifying the data type.</span></span> <span data-ttu-id="2872b-138">예를 들어 다음 코드에서는 시간을 제외한 표시할 날짜를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-138">For example, the following code causes the date to be displayed without the time.</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    <span data-ttu-id="2872b-139">응용 프로그램을 포함 하는 경우는 *date.cshtml* 에서 서식 파일은 *Views\Shared\DisplayTemplates* 폴더 또는 *Views\Movies\DisplayTemplates* 해당 서식 파일, 폴더 렌더링에 사용 되는 `DateTime` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-139">If the application contains a *date.cshtml* template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder, that template will be used to render the `DateTime` property.</span></span> <span data-ttu-id="2872b-140">그렇지 않은 경우 기본 제공 ASP.NET 템플릿 시스템 날짜로 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-140">Otherwise the built-in ASP.NET templating system displays the property as a date.</span></span>
- <span data-ttu-id="2872b-141">디스플레이 템플릿을 만드는 *Views\Shared\DisplayTemplates* 폴더 또는 *Views\Movies\DisplayTemplates* 폴더 이름이 서식을 지정할 데이터 형식이 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-141">Creating a display template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder whose name matches the data type that you want to format.</span></span> <span data-ttu-id="2872b-142">예를 들어 언급 했 듯이 하는 *Views\Shared\DisplayTemplates\DateTime.cshtml* 렌더링 하는 데 사용한 `DateTime` 모델에 특성을 추가 하지 않고 및 보기에 태그를 추가 하지 않고 모델의 속성.</span><span class="sxs-lookup"><span data-stu-id="2872b-142">For example, you saw that the *Views\Shared\DisplayTemplates\DateTime.cshtml* was used to render `DateTime` properties in a model, without adding an attribute to the model and without adding any markup to views.</span></span>
- <span data-ttu-id="2872b-143">사용 하는 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 모델 속성을 표시 하려면 서식 파일을 지정 하려면 모델에는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-143">Using the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute on the model to specify the template to display the model property.</span></span>
- <span data-ttu-id="2872b-144">표시 템플릿 이름을 명시적으로 추가 된 [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) 보기에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-144">Explicitly adding the display template name to the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call in a view.</span></span>

<span data-ttu-id="2872b-145">응용 프로그램에서 작업을 수행 해야 할 작업에 사용 하는 방법에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-145">The approach you use depends on what you need to do in your application.</span></span> <span data-ttu-id="2872b-146">이러한 접근 방식을 정확 하 게 종류의 서식 지정 해야 하는 get를 혼합 하는 일반적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-146">It's not uncommon to mix these approaches to get exactly the kind of formatting that you need.</span></span>

<span data-ttu-id="2872b-147">다음 섹션에서 전환 하 여 약간 주제 및 입력 방식을 사용자 지정 데이터 표시 방법을 사용자 지정에서 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-147">In the next section, you'll switch gears a bit and move from customizing how data is displayed to customizing how it's entered.</span></span> <span data-ttu-id="2872b-148">JQuery datepicker 날짜를 지정 하는 편리한 방법을 제공 하기 위해 응용 프로그램의 편집 뷰에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2872b-148">You'll hook up the jQuery datepicker to the edit views in the application in order to provide a slick way to specify dates.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="2872b-149">[이전](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
[다음](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="2872b-149">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span></span>
