---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: ViewData 사용 및 ViewModel 클래스 구현 | Microsoft Docs
author: microsoft
description: 6 단계에서는 어떻게 지원할 시나리오를 편집 하는 다양 한 형식에 대 한 컨트롤러에서 보기로 데이터를 전달 하는 두 가지 방법에 설명 합니다....
ms.author: aspnetcontent
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 70b264def11b55fc08165dda307ff9e82fd4be7f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37826961"
---
<a name="use-viewdata-and-implement-viewmodel-classes"></a><span data-ttu-id="be842-103">ViewData 사용 및 ViewModel 클래스 구현</span><span class="sxs-lookup"><span data-stu-id="be842-103">Use ViewData and Implement ViewModel Classes</span></span>
====================
<span data-ttu-id="be842-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="be842-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="be842-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="be842-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="be842-106">이 무료의 6 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="be842-106">This is step 6 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="be842-107">시나리오를 편집 하는 다양 한 형식에 대 한 지원을 어떻게 사용 하는 6 단계 표시 컨트롤러에서 보기로 데이터를 전달 하는 두 가지 방법에 설명 합니다: ViewData 및 ViewModel입니다.</span><span class="sxs-lookup"><span data-stu-id="be842-107">Step 6 shows how enable support for richer form editing scenarios, and also discusses two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>
> 
> <span data-ttu-id="be842-108">ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="be842-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a><span data-ttu-id="be842-109">NerdDinner 6 단계: ViewData 및 ViewModel</span><span class="sxs-lookup"><span data-stu-id="be842-109">NerdDinner Step 6: ViewData and ViewModel</span></span>

<span data-ttu-id="be842-110">다양 한 폼 게시 시나리오를 다루는 구현 하는 방법을 설명 했습니다 만들기, 업데이트 및 삭제 (CRUD) 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-110">We've covered a number of form post scenarios, and discussed how to implement create, update and delete (CRUD) support.</span></span> <span data-ttu-id="be842-111">에서는 이제 DinnersController 구현은 좀 더 수행 하 고 시나리오를 편집 하는 다양 한 형식에 대 한 지원을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-111">We'll now take our DinnersController implementation further and enable support for richer form editing scenarios.</span></span> <span data-ttu-id="be842-112">이 작업을 수행 하는 동안 컨트롤러에서 보기로 데이터를 전달 하는 두 가지 방법을 설명 합니다: ViewData 및 ViewModel입니다.</span><span class="sxs-lookup"><span data-stu-id="be842-112">While doing this we'll discuss two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>

### <a name="passing-data-from-controllers-to-view-templates"></a><span data-ttu-id="be842-113">템플릿 보기에 컨트롤러에서 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="be842-113">Passing Data from Controllers to View-Templates</span></span>

<span data-ttu-id="be842-114">MVC 패턴의 결정적인 특징 중 하나는 엄격한 "문제의 분리" 응용 프로그램의 다른 구성 요소 간에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be842-114">One of the defining characteristics of the MVC pattern is the strict "separation of concerns" it helps enforce between the different components of an application.</span></span> <span data-ttu-id="be842-115">모델, 컨트롤러 및 뷰 각 있는 잘 정의 된 역할 및 책임 및 잘 정의 된 방식으로 서로 간에 통신할 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-115">Models, Controllers and Views each have well defined roles and responsibilities, and they communicate amongst each other in well defined ways.</span></span> <span data-ttu-id="be842-116">이 통해 테스트 용이성을 승격 하 고 코드 재사용.</span><span class="sxs-lookup"><span data-stu-id="be842-116">This helps promote testability and code reuse.</span></span>

<span data-ttu-id="be842-117">컨트롤러 클래스를 클라이언트에 HTML 응답을 렌더링 하기로 하는 경우에 보기 템플릿에서 응답을 렌더링 하는 데 필요한 모든 데이터를 명시적으로 전달 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-117">When a Controller class decides to render an HTML response back to a client, it is responsible for explicitly passing to the view template all of the data needed to render the response.</span></span> <span data-ttu-id="be842-118">보기 템플릿은 모든 데이터 검색 또는 응용 프로그램 논리를 수행 하면 안 및 컨트롤러에 의해 전달 된 모델/데이터 구동 되는 코드를 렌더링 하려면만 자체 대신 제한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-118">View templates should never perform any data retrieval or application logic – and should instead limit themselves to only have rendering code that is driven off of the model/data passed to it by the controller.</span></span>

<span data-ttu-id="be842-119">지금은 모델 데이터 Details(), 되, create () 및 delete ()의 경우 개체의 index (), 경우 Dinner 개체 목록 및 단일 Dinner 간단 – 및 우리의 DinnersController에 의해 전달 되는 보기 템플릿 클래스는 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-119">Right now the model data being passed by our DinnersController class to our view templates is simple and straight-forward – a list of Dinner objects in the case of Index(), and a single Dinner object in the case of Details(), Edit(), Create() and Delete().</span></span> <span data-ttu-id="be842-120">응용 프로그램에 더 많은 UI 기능을 추가 했습니다 종종 하겠습니다 이상의이 데이터는 보기 템플릿 내에서 HTML 응답을 렌더링를 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-120">As we add more UI capabilities to our application, we are often going to need to pass more than just this data to render HTML responses within our view templates.</span></span> <span data-ttu-id="be842-121">예를 들어, dropdownlist HTML 텍스트 상자에서 보기를 만들고이 편집 내에서 "Country" 필드를 변경 하겠습니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be842-121">For example, we might want to change the "Country" field within our Edit and Create views from being an HTML textbox to a dropdownlist.</span></span> <span data-ttu-id="be842-122">하드 코드 보기 템플릿에서 국가 이름 드롭다운 목록에는 대신 동적으로 채우기는 지원 되는 국가 목록을 생성 하고자 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be842-122">Rather than hard-code the dropdown list of country names in the view template, we might want to generate it from a list of supported countries that we populate dynamically.</span></span> <span data-ttu-id="be842-123">Dinner 개체 모두에 전달할 방법이 필요 합니다 *고* 우리의 보기 템플릿은 컨트롤러에서 지원 되는 국가 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be842-123">We will need a way to pass both the Dinner object *and* the list of supported countries from our controller to our view templates.</span></span>

<span data-ttu-id="be842-124">두 가지 방법으로이 위해서는 수를 살펴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="be842-124">Let's look at two ways we can accomplish this.</span></span>

### <a name="using-the-viewdata-dictionary"></a><span data-ttu-id="be842-125">ViewData 사전을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="be842-125">Using the ViewData Dictionary</span></span>

<span data-ttu-id="be842-126">컨트롤러 기본 클래스는 컨트롤러에서 다른 데이터 항목 보기에 전달할 수 있는 "ViewData" 사전 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-126">The Controller base class exposes a "ViewData" dictionary property that can be used to pass additional data items from Controllers to Views.</span></span>

<span data-ttu-id="be842-127">예를 들어, dropdownlist HTML 텍스트 상자에서 편집 보기 내에서 "Country" 텍스트를 변경 하려는 시나리오를 지원 하려면 업데이트할 수 있습니다 (외에 Dinner 개체)는 m으로 사용할 수 있는 SelectList 개체를 전달 하는 되 작업 메서드 국가 dropdownlist의 odel 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-127">For example, to support the scenario where we want to change the "Country" textbox within our Edit view from being an HTML textbox to a dropdownlist, we can update our Edit() action method to pass (in addition to a Dinner object) a SelectList object that can be used as the model of a countries dropdownlist.</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

<span data-ttu-id="be842-128">위의 SelectList의 생성자가 현재 선택된 된 값 뿐만 아니라, 놓기 downlist 채우려면 군은 목록을 승인 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-128">The constructor of the SelectList above is accepting a list of counties to populate the drop-downlist with, as well as the currently selected value.</span></span>

<span data-ttu-id="be842-129">그런 다음 이전에 사용 되는 Html.TextBox() 도우미 메서드를 대신 Html.DropDownList() 도우미 메서드를 사용 하도록 Edit.aspx 보기 템플릿을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be842-129">We can then update our Edit.aspx view template to use the Html.DropDownList() helper method instead of the Html.TextBox() helper method we used previously:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

<span data-ttu-id="be842-130">위의 Html.DropDownList() 도우미 메서드는 두 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-130">The Html.DropDownList() helper method above takes two parameters.</span></span> <span data-ttu-id="be842-131">첫 번째는 HTML 폼 요소 출력의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="be842-131">The first is the name of the HTML form element to output.</span></span> <span data-ttu-id="be842-132">두 번째는 "SelectList" 모델 ViewData 사전을 통해 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-132">The second is the "SelectList" model we passed via the ViewData dictionary.</span></span> <span data-ttu-id="be842-133">"C#로 사용" 키워드를 SelectList으로 사전 내에서 형식을 캐스팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-133">We are using the C# "as" keyword to cast the type within the dictionary as a SelectList.</span></span>

<span data-ttu-id="be842-134">이제을 실행할 때이 응용 프로그램 및 액세스 하 고는 */Dinners/Edit/1* URL 브라우저 내 살펴보겠습니다 텍스트 대신 국가의 dropdownlist에 표시할이 편집 UI 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="be842-134">And now when we run our application and access the */Dinners/Edit/1* URL within our browser we'll see that our edit UI has been updated to display a dropdownlist of countries instead of a textbox:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

<span data-ttu-id="be842-135">편집 보기 템플릿에서 HTTP POST 편집 메서드 (오류 발생 시 시나리오)를 렌더링할 수도, 때문에 오류 시나리오에서 템플릿 보기를 렌더링할 때는 SelectList ViewData를 추가 하려면이 메서드는 또한 업데이트 되었는지 확인 하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-135">Because we also render the Edit view template from the HTTP-POST Edit method (in scenarios when errors occur), we'll want to make sure that we also update this method to add the SelectList to ViewData when the view template is rendered in error scenarios:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

<span data-ttu-id="be842-136">하며 이제 DinnersController 편집 시나리오 DropDownList를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-136">And now our DinnersController edit scenario supports a DropDownList.</span></span>

### <a name="using-a-viewmodel-pattern"></a><span data-ttu-id="be842-137">ViewModel 패턴 사용</span><span class="sxs-lookup"><span data-stu-id="be842-137">Using a ViewModel Pattern</span></span>

<span data-ttu-id="be842-138">ViewData 사전을 접근 방식은 매우 빠르고 쉽게 구현할 수 있는 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be842-138">The ViewData dictionary approach has the benefit of being fairly fast and easy to implement.</span></span> <span data-ttu-id="be842-139">일부 개발자 마음에 들지 않는 문자열 기반 사전을 사용 하 여 그러나 오타 컴파일 타임에 발견 되지 않으므로 오류를 일으킬 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-139">Some developers don't like using string-based dictionaries, though, since typos can lead to errors that will not be caught at compile-time.</span></span> <span data-ttu-id="be842-140">형식화 되지 않은 ViewData 사전을 "as" 연산자를 사용 하 여 또는 캐스팅 보기 템플릿에서 C#과 같은 강력한 형식의 언어를 사용 하는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-140">The un-typed ViewData dictionary also requires using the "as" operator or casting when using a strongly-typed language like C# in a view template.</span></span>

<span data-ttu-id="be842-141">또 다른 방법을 사용 하 여 사용 이란 "ViewModel" 패턴 이라고 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be842-141">An alternative approach that we could use is one often referred to as the "ViewModel" pattern.</span></span> <span data-ttu-id="be842-142">이 패턴을 사용 하는 경우 시나리오는 특정 보기에 최적화 된 및 우리의 보기 템플릿에서 필요한 동적 값/콘텐츠에 대 한 속성을 노출 하는 강력한 형식의 클래스 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be842-142">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="be842-143">다음 컨트롤러 클래스 채우고 이러한 보기에 최적화 된 클래스를 사용 하 여 보기 템플릿은 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be842-143">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="be842-144">이렇게 하면 형식 안전성, 컴파일 시간 검사 및 템플릿 보기 내에서 편집기 intellisense 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be842-144">This enables type-safety, compile-time checking, and editor intellisense within view templates.</span></span>

<span data-ttu-id="be842-145">예를 들어, 두 가지 강력한 형식의 속성을 노출 하는 dinner 폼 편집 시나리오 "DinnerFormViewModel" 만들면 아래와 같은 클래스를 사용 하도록 설정 하려면: 저녁 식사를 및 국가 dropdownlist를 채우는 데 필요한 SelectList 모델:</span><span class="sxs-lookup"><span data-stu-id="be842-145">For example, to enable dinner form editing scenarios we can create a "DinnerFormViewModel" class like below that exposes two strongly-typed properties: a Dinner object, and the SelectList model needed to populate the countries dropdownlist:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

<span data-ttu-id="be842-146">리포지토리에서에서 검색 하는 Dinner 개체를 사용 하 여 DinnerFormViewModel 만들려면 되 작업 메서드는 다음 업데이트 되 고 보기 템플릿은에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be842-146">We can then update our Edit() action method to create the DinnerFormViewModel using the Dinner object we retrieve from our repository, and then pass it to our view template:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

<span data-ttu-id="be842-147">다음과 같이 업데이트 보기 템플릿은 해당 it "Dinner" 대신 "DinnerFormViewModel" 것으로 예상 하므로 edit.aspx 페이지의 맨 위에 있는 "상속" 특성을 변경 하 여 개체를 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-147">We'll then update our view template so that it expects a "DinnerFormViewModel" instead of a "Dinner" object by changing the "inherits" attribute at the top of the edit.aspx page like so:</span></span>

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

<span data-ttu-id="be842-148">완료 되 면이 우리의 보기 템플릿에서 "모델" 속성의 intellisense 전달이 DinnerFormViewModel 형식의 개체 모델을 반영 하도록 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be842-148">Once we do this, the intellisense of the "Model" property within our view template will be updated to reflect the object model of the DinnerFormViewModel type we are passing it:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

<span data-ttu-id="be842-149">그런 다음 뷰 코드를 누를 때 작업을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be842-149">We can then update our view code to work off of it.</span></span> <span data-ttu-id="be842-150">만들고 방법에서는 변경 하지 않는 입력 요소의 이름은 아래 통지 (폼 요소 여전히 이름은 "Title", "Country")-DinnerFormViewModel 클래스를 사용 하 여 값을 검색 하는 HTML 도우미 메서드를 업데이트 하는 것 이지만:</span><span class="sxs-lookup"><span data-stu-id="be842-150">Notice below how we are not changing the names of the input elements we are creating (the form elements will still be named "Title", "Country") – but we are updating the HTML Helper methods to retrieve the values using the DinnerFormViewModel class:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

<span data-ttu-id="be842-151">또한 오류를 렌더링할 때 DinnerFormViewModel 클래스를 사용 하 여 편집 post 메서드를 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be842-151">We'll also update our Edit post method to use the DinnerFormViewModel class when rendering errors:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

<span data-ttu-id="be842-152">업데이트할 수 있습니다도 다시 정확한를 사용 하려면 create () 작업 메서드가 동일한 *DinnerFormViewModel* 클래스를 사용 하는 국가 DropDownList 내에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-152">We can also update our Create() action methods to re-use the exact same *DinnerFormViewModel* class to enable the countries DropDownList within those as well.</span></span> <span data-ttu-id="be842-153">다음은 HTTP GET 구현이입니다.</span><span class="sxs-lookup"><span data-stu-id="be842-153">Below is the HTTP-GET implementation:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

<span data-ttu-id="be842-154">다음은 만드는 HTTP POST 메서드의 구현이입니다.</span><span class="sxs-lookup"><span data-stu-id="be842-154">Below is the implementation of the HTTP-POST Create method:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

<span data-ttu-id="be842-155">이제 편집 및 만들기 화면 모두 드롭다운 목록을 위한 지원과 국가 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-155">And now both our Edit and Create screens support drop-downlists for picking the country.</span></span>

### <a name="custom-shaped-viewmodel-classes"></a><span data-ttu-id="be842-156">사용자 지정 모양의 ViewModel 클래스</span><span class="sxs-lookup"><span data-stu-id="be842-156">Custom-shaped ViewModel classes</span></span>

<span data-ttu-id="be842-157">위의 시나리오 DinnerFormViewModel 클래스 직접 지원 SelectList 모델 속성과 함께 속성으로 Dinner 모델 개체를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-157">In the scenario above, our DinnerFormViewModel class directly exposes the Dinner model object as a property, along with a supporting SelectList model property.</span></span> <span data-ttu-id="be842-158">이 방법은 시나리오는 우리의 보기 템플릿에서 생성 하려는 HTML UI 비교적 밀접 하 게에 해당 도메인 모델 개체에 대 한 제대로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-158">This approach works fine for scenarios where the HTML UI we want to create within our view template corresponds relatively closely to our domain model objects.</span></span>

<span data-ttu-id="be842-159">이러한 방식이 대 한 경우 사용할 수 있는 한 가지 옵션을 사용자 지정 모양의 ViewModel 클래스 뷰에서 – 소비 해당 개체 모델은 더 최적화 하는 기본 도메인 모델 개체와 완전히 다르게 보일 수 있습니다를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="be842-159">For scenarios where this isn't the case, one option that you can use is to create a custom-shaped ViewModel class whose object model is more optimized for consumption by the view – and which might look completely different from the underlying domain model object.</span></span> <span data-ttu-id="be842-160">예를 들어, 다른 속성 이름 및/또는 여러 모델 개체에서 수집 된 집계 속성 노출 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="be842-160">For example, it could potentially expose different property names and/or aggregate properties collected from multiple model objects.</span></span>

<span data-ttu-id="be842-161">ViewModel 클래스 사용자 지정 모양 수 모두 전달할 데이터 컨트롤러에서 뷰를 렌더링 하려면 뿐만 아니라 컨트롤러의 동작 메서드를 다시 게시 하는 폼 데이터를 처리 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-161">Custom-shaped ViewModel classes can be used both to pass data from controllers to views to render, as well as to help handle form data posted back to a controller's action method.</span></span> <span data-ttu-id="be842-162">이후이 시나리오에서는 동작 메서드가 폼 게시 데이터를 사용 하 여 ViewModel 개체를 업데이트 하 고 다음 ViewModel 인스턴스를 사용 하 여 그림을 매핑하거나 실제 도메인 모델 개체를 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-162">For this later scenario, you might have the action method update a ViewModel object with the form-posted data, and then use the ViewModel instance to map or retrieve an actual domain model object.</span></span>

<span data-ttu-id="be842-163">ViewModel 클래스 사용자 지정 모양의 상당한 유연성을 제공할 수 있습니다 및은 너무 복잡 하기 시작 하 여 작업 메서드 내에서 보기 템플릿을 또는 폼 게시 코드 내에서 렌더링 코드를 찾을 때마다 조사 해야 할 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="be842-163">Custom-shaped ViewModel classes can provide a great deal of flexibility, and are something to investigate any time you find the rendering code within your view templates or the form-posting code inside your action methods starting to get too complicated.</span></span> <span data-ttu-id="be842-164">이 종종 도메인 모델을 생성 하는 UI 완전히 동일 하지 않습니다 하 고 중간 사용자 지정 모양의 ViewModel 클래스가 도움이 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="be842-164">This is often a sign that your domain models don't cleanly correspond to the UI you are generating, and that an intermediate custom-shaped ViewModel class can help.</span></span>

### <a name="next-step"></a><span data-ttu-id="be842-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="be842-165">Next Step</span></span>

<span data-ttu-id="be842-166">이제 살펴보겠습니다 사용 하 여 부분 및 마스터 페이지를 다시 사용 하 여 응용 프로그램에서 UI를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="be842-166">Let's now look at how we can use partials and master-pages to re-use and share UI across our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="be842-167">[이전](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [다음](re-use-ui-using-master-pages-and-partials.md)</span><span class="sxs-lookup"><span data-stu-id="be842-167">[Previous](provide-crud-create-read-update-delete-data-form-entry-support.md)
[Next](re-use-ui-using-master-pages-and-partials.md)</span></span>
