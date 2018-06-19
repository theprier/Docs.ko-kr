---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: 사용 하 여 ViewData 및 구현 ViewModel 클래스 | Microsoft Docs
author: microsoft
description: 6 단계에서는 시나리오를 편집 하는 다양 한 형식에 대 한 지원을 어떻게 사용 하도록 설정 하 고 컨트롤러에서 뷰로 데이터를 전달 하는 데 사용할 수 있는 두 가지 방법에 대해서도 설명:...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 9ba8758bd6524f3e300f3fd91ef68cfe8a3587a7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879428"
---
<a name="use-viewdata-and-implement-viewmodel-classes"></a><span data-ttu-id="85015-103">사용 하 여 ViewData 및 구현 ViewModel 클래스</span><span class="sxs-lookup"><span data-stu-id="85015-103">Use ViewData and Implement ViewModel Classes</span></span>
====================
<span data-ttu-id="85015-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="85015-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="85015-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="85015-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="85015-106">이 무료의 6 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="85015-106">This is step 6 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="85015-107">6 단계에서는 시나리오를 편집 하는 다양 한 형식에 대 한 지원을 어떻게 사용 하도록 설정 하 고 컨트롤러에서 뷰로 데이터를 전달 하는 데 사용할 수 있는 두 가지 방법에 대해서도 설명: ViewData 및 ViewModel입니다.</span><span class="sxs-lookup"><span data-stu-id="85015-107">Step 6 shows how enable support for richer form editing scenarios, and also discusses two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>
> 
> <span data-ttu-id="85015-108">ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="85015-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a><span data-ttu-id="85015-109">업그레이드 되었으며 수정 단계 6: ViewData 및 ViewModel</span><span class="sxs-lookup"><span data-stu-id="85015-109">NerdDinner Step 6: ViewData and ViewModel</span></span>

<span data-ttu-id="85015-110">다양 한 폼 게시 시나리오를 대상 고 구현 하는 방법을 논의 했으므로 만들기, 업데이트 및 삭제 (CRUD) 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-110">We've covered a number of form post scenarios, and discussed how to implement create, update and delete (CRUD) support.</span></span> <span data-ttu-id="85015-111">이제 추가 DinnersController 구현은 수행할 알아보고 시나리오를 편집 하는 다양 한 형식에 대 한 지원을 사용 하도록 설정 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="85015-111">We'll now take our DinnersController implementation further and enable support for richer form editing scenarios.</span></span> <span data-ttu-id="85015-112">이 작업을 수행 하는 동안 컨트롤러에서 뷰로 데이터를 전달 하는 데 사용할 수 있는 두 가지 방법에 설명 합니다: ViewData 및 ViewModel입니다.</span><span class="sxs-lookup"><span data-stu-id="85015-112">While doing this we'll discuss two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>

### <a name="passing-data-from-controllers-to-view-templates"></a><span data-ttu-id="85015-113">템플릿 보기에 컨트롤러에서 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="85015-113">Passing Data from Controllers to View-Templates</span></span>

<span data-ttu-id="85015-114">엄격한 "문제의 분리" MVC 패턴의 결정적인 특징 중 하나는 응용 프로그램의 여러 구성 요소 간의 적용 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85015-114">One of the defining characteristics of the MVC pattern is the strict "separation of concerns" it helps enforce between the different components of an application.</span></span> <span data-ttu-id="85015-115">모델, 컨트롤러와 뷰 각각 잘 정의 되어 역할 및 책임 및 잘 정의 된 방법으로 서로 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-115">Models, Controllers and Views each have well defined roles and responsibilities, and they communicate amongst each other in well defined ways.</span></span> <span data-ttu-id="85015-116">이렇게 하면 테스트 가능성을 승격 하 고 코드 재사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-116">This helps promote testability and code reuse.</span></span>

<span data-ttu-id="85015-117">컨트롤러 클래스를 클라이언트에 다시를 HTML 응답을 렌더링 하기로 하는 경우에 응답을 렌더링 하는 데 필요한 모든 데이터 템플릿 보기에 명시적으로 전달 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-117">When a Controller class decides to render an HTML response back to a client, it is responsible for explicitly passing to the view template all of the data needed to render the response.</span></span> <span data-ttu-id="85015-118">템플릿 보기 – 데이터 검색 또는 응용 프로그램 논리를 수행 하면 안 및만 하는 컨트롤러에 의해 전달 모델/데이터 구동 되는 렌더링 코드 자체 제한 대신 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-118">View templates should never perform any data retrieval or application logic – and should instead limit themselves to only have rendering code that is driven off of the model/data passed to it by the controller.</span></span>

<span data-ttu-id="85015-119">지금은 모델 데이터 우리의 DinnersController에 의해 전달 되 클래스 템플릿 우리의 보기를 단순 하 고 직관적인 – index ()의 경우 Dinner 개체의 목록 및 단일 Dinner 개체 Details(), Edit(), create () 및 delete ()의 경우.</span><span class="sxs-lookup"><span data-stu-id="85015-119">Right now the model data being passed by our DinnersController class to our view templates is simple and straight-forward – a list of Dinner objects in the case of Index(), and a single Dinner object in the case of Details(), Edit(), Create() and Delete().</span></span> <span data-ttu-id="85015-120">응용 프로그램에 더 많은 UI 기능을 추가 했습니다 종종을 하겠습니다 보다 더 우리의 템플릿 보기에서 HTML 응답을 렌더링 하려면이 데이터를 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-120">As we add more UI capabilities to our application, we are often going to need to pass more than just this data to render HTML responses within our view templates.</span></span> <span data-ttu-id="85015-121">예를 들어 다음 우리의 편집 내의 "국가" 필드를 변경 하 고 dropdownlist는 HTML 텍스트 상자에서 보기를 만들 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85015-121">For example, we might want to change the "Country" field within our Edit and Create views from being an HTML textbox to a dropdownlist.</span></span> <span data-ttu-id="85015-122">하드 코딩 템플릿 보기에에서 국가 이름 드롭다운 목록, 대신 동적으로 채울에서는 지원 되는 국가 목록은에서 생성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85015-122">Rather than hard-code the dropdown list of country names in the view template, we might want to generate it from a list of supported countries that we populate dynamically.</span></span> <span data-ttu-id="85015-123">저녁 개체를 전달 하는 방법이 필요 합니다 *및* 우리의 템플릿 보기에는 컨트롤러에서 지원 되는 국가 목록은 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-123">We will need a way to pass both the Dinner object *and* the list of supported countries from our controller to our view templates.</span></span>

<span data-ttu-id="85015-124">두 가지 방법으로이 위해 수를 살펴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="85015-124">Let's look at two ways we can accomplish this.</span></span>

### <a name="using-the-viewdata-dictionary"></a><span data-ttu-id="85015-125">사전은 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="85015-125">Using the ViewData Dictionary</span></span>

<span data-ttu-id="85015-126">컨트롤러의 기본 클래스는 컨트롤러에서 뷰를 다른 데이터 항목을 전달 하는 데 사용할 수 있는 "ViewData" 사전 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-126">The Controller base class exposes a "ViewData" dictionary property that can be used to pass additional data items from Controllers to Views.</span></span>

<span data-ttu-id="85015-127">예를 들어 우리의 편집 뷰 내에서 "국가" textbox dropdownlist는 HTML 텍스트 상자에서 변경 하려는 시나리오를 지원 하려면 수 업데이트 (뿐 아니라 Dinner 개체)는 m으로 사용할 수 있는 SelectList 개체를 전달 하는 Edit() 동작 메서드 국가 dropdownlist의 odel 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-127">For example, to support the scenario where we want to change the "Country" textbox within our Edit view from being an HTML textbox to a dropdownlist, we can update our Edit() action method to pass (in addition to a Dinner object) a SelectList object that can be used as the model of a countries dropdownlist.</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

<span data-ttu-id="85015-128">위의 SelectList의 생성자에서 현재 선택 된 값과 함께, 놓기 downlist를 채우는 데 군 목록을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-128">The constructor of the SelectList above is accepting a list of counties to populate the drop-downlist with, as well as the currently selected value.</span></span>

<span data-ttu-id="85015-129">우리의 Edit.aspx 보기 템플릿 Html.TextBox() 도우미 메서드 이전에 사용 되는 대신 Html.DropDownList() 도우미 메서드를 사용 하도록 업데이트할 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="85015-129">We can then update our Edit.aspx view template to use the Html.DropDownList() helper method instead of the Html.TextBox() helper method we used previously:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

<span data-ttu-id="85015-130">위의 Html.DropDownList() 도우미 메서드 두 개의 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-130">The Html.DropDownList() helper method above takes two parameters.</span></span> <span data-ttu-id="85015-131">첫 번째에는 HTML 폼 요소 출력의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="85015-131">The first is the name of the HTML form element to output.</span></span> <span data-ttu-id="85015-132">두 번째는 사전은 통해 전달 했습니다 "SelectList" 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="85015-132">The second is the "SelectList" model we passed via the ViewData dictionary.</span></span> <span data-ttu-id="85015-133">사용 하 여 C# "키워드 as"는 SelectList로 사전에 있는 형식을 캐스팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-133">We are using the C# "as" keyword to cast the type within the dictionary as a SelectList.</span></span>

<span data-ttu-id="85015-134">म 실행할 때이 응용 프로그램 및 액세스 하 고는 */Dinners/Edit/1* URL 브라우저 내에서 볼 수 있겠지만, 우리의 편집 UI가 텍스트 상자 대신 국가의 dropdownlist를 표시 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85015-134">And now when we run our application and access the */Dinners/Edit/1* URL within our browser we'll see that our edit UI has been updated to display a dropdownlist of countries instead of a textbox:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

<span data-ttu-id="85015-135">시나리오에서 오류 발생 시 HTTP POST 편집 메서드에서 템플릿 편집 뷰를 렌더링할 수도, 때문에 것도 보기 템플릿 오류 시나리오에서 렌더링 될 때 ViewData 하 여 SelectList를 추가 하려면이 메서드를 업데이트할 수 있는지 확인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-135">Because we also render the Edit view template from the HTTP-POST Edit method (in scenarios when errors occur), we'll want to make sure that we also update this method to add the SelectList to ViewData when the view template is rendered in error scenarios:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

<span data-ttu-id="85015-136">이제 DinnersController 편집 시나리오 DropDownList를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-136">And now our DinnersController edit scenario supports a DropDownList.</span></span>

### <a name="using-a-viewmodel-pattern"></a><span data-ttu-id="85015-137">ViewModel 패턴 사용</span><span class="sxs-lookup"><span data-stu-id="85015-137">Using a ViewModel Pattern</span></span>

<span data-ttu-id="85015-138">ViewData 사전 접근 방식에 매우 쉽고 빠르게 구현할 수 있다는 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85015-138">The ViewData dictionary approach has the benefit of being fairly fast and easy to implement.</span></span> <span data-ttu-id="85015-139">일부 개발자 마음에 들지 않는 문자열 기반 사전을 사용 하 여 하지만 오타 컴파일 타임에 발견 되지 않으므로 오류가 발생할 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-139">Some developers don't like using string-based dictionaries, though, since typos can lead to errors that will not be caught at compile-time.</span></span> <span data-ttu-id="85015-140">형식화 되지 않은 사전은 "as" 연산자를 사용 하 여 또는 캐스팅 템플릿 보기에서에서 C#과 같은 강력한 형식의 언어를 사용 하는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-140">The un-typed ViewData dictionary also requires using the "as" operator or casting when using a strongly-typed language like C# in a view template.</span></span>

<span data-ttu-id="85015-141">한 대체 방법을 사용 하 여은 하나는 "ViewModel" 패턴 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-141">An alternative approach that we could use is one often referred to as the "ViewModel" pattern.</span></span> <span data-ttu-id="85015-142">이 패턴을 사용 하는 경우 강력한 형식의 클래스의 특정 보기 시나리오에 최적화 된 및 우리의 템플릿 보기에 필요한 동적 값/콘텐츠에 대 한 속성을 노출 합니다 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85015-142">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="85015-143">컨트롤러 클래스 다음 이러한 보기 액세스에 최적화 된 클래스 우리의 뷰 템플릿을 사용 하려면에 전달을 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85015-143">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="85015-144">이렇게 하면 형식 안전성, 컴파일 타임 검사 및 템플릿 보기 내에서 편집기 intellisense 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85015-144">This enables type-safety, compile-time checking, and editor intellisense within view templates.</span></span>

<span data-ttu-id="85015-145">예를 들어, 두 개의 강력한 형식의 속성을 표시 하는 dinner 양식 "DinnerFormViewModel"을 만들 수 있습니다 편집 시나리오 아래와 같은 클래스를 사용 하도록 설정 하려면: Dinner 개체 및 국가 dropdownlist를 채우는 데 필요한 SelectList 모델:</span><span class="sxs-lookup"><span data-stu-id="85015-145">For example, to enable dinner form editing scenarios we can create a "DinnerFormViewModel" class like below that exposes two strongly-typed properties: a Dinner object, and the SelectList model needed to populate the countries dropdownlist:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

<span data-ttu-id="85015-146">다음 우리의 저장소에서 검색 하는 Dinner 개체를 사용 하 여 DinnerFormViewModel 만들려는 우리의 Edit() 작업 메서드를 업데이트 하 고 우리의 템플릿 보기에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85015-146">We can then update our Edit() action method to create the DinnerFormViewModel using the Dinner object we retrieve from our repository, and then pass it to our view template:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

<span data-ttu-id="85015-147">त ु म च 같이 우리의 보기 템플릿 한다는 "Dinner" 대신 "DinnerFormViewModel" 필요 하므로 개체 edit.aspx 페이지 맨 위에 있는 "inherits" 특성을 변경 하 여 업데이트 한 후:</span><span class="sxs-lookup"><span data-stu-id="85015-147">We'll then update our view template so that it expects a "DinnerFormViewModel" instead of a "Dinner" object by changing the "inherits" attribute at the top of the edit.aspx page like so:</span></span>

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

<span data-ttu-id="85015-148">이렇게 म 우리의 보기 템플릿 내에서 "모델" 속성의 intellisense 것 전달 DinnerFormViewModel 형식의 개체 모델을 반영 하도록 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85015-148">Once we do this, the intellisense of the "Model" property within our view template will be updated to reflect the object model of the DinnerFormViewModel type we are passing it:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

<span data-ttu-id="85015-149">그런 다음 밖 작업 보기 코드를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85015-149">We can then update our view code to work off of it.</span></span> <span data-ttu-id="85015-150">생성 방법에서는 변경 하지 않는 입력 요소의 이름 아래 공지 (form 요소는 여전히 지정 "제목", "국가") – DinnerFormViewModel 클래스를 사용 하 여 값을 검색 하는 HTML 도우미 메서드를 업데이트 하려고 하지만:</span><span class="sxs-lookup"><span data-stu-id="85015-150">Notice below how we are not changing the names of the input elements we are creating (the form elements will still be named "Title", "Country") – but we are updating the HTML Helper methods to retrieve the values using the DinnerFormViewModel class:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

<span data-ttu-id="85015-151">또한 업데이트 하는 중 오류를 렌더링할 때 DinnerFormViewModel 클래스를 사용 하는 편집 post 메서드:</span><span class="sxs-lookup"><span data-stu-id="85015-151">We'll also update our Edit post method to use the DinnerFormViewModel class when rendering errors:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

<span data-ttu-id="85015-152">동일한 재사용 하 여 정확한 create () 동작 메서드를 업데이트할 수도 있습니다 *DinnerFormViewModel* 클래스 국가 같이 DropDownList 내는 것도 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-152">We can also update our Create() action methods to re-use the exact same *DinnerFormViewModel* class to enable the countries DropDownList within those as well.</span></span> <span data-ttu-id="85015-153">다음은 HTTP GET 구현이입니다.</span><span class="sxs-lookup"><span data-stu-id="85015-153">Below is the HTTP-GET implementation:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

<span data-ttu-id="85015-154">다음은 HTTP POST 만들 메서드의 구현이입니다.</span><span class="sxs-lookup"><span data-stu-id="85015-154">Below is the implementation of the HTTP-POST Create method:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

<span data-ttu-id="85015-155">고 이제이 우리의 만들기 및 편집 화면 드롭다운 목록을 국가 선택 하는 데 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-155">And now both our Edit and Create screens support drop-downlists for picking the country.</span></span>

### <a name="custom-shaped-viewmodel-classes"></a><span data-ttu-id="85015-156">사용자 지정 모양의 ViewModel 클래스</span><span class="sxs-lookup"><span data-stu-id="85015-156">Custom-shaped ViewModel classes</span></span>

<span data-ttu-id="85015-157">위 시나리오 DinnerFormViewModel 클래스 직접 지원 SelectList 모델 속성과 함께 속성으로 저녁 모델 개체를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-157">In the scenario above, our DinnerFormViewModel class directly exposes the Dinner model object as a property, along with a supporting SelectList model property.</span></span> <span data-ttu-id="85015-158">이 방법은 시나리오 여기서 우리의 보기 템플릿 내에서 만들려고 HTML UI 비교적 밀접 하 게에 해당 도메인 모델 개체에 대 한 제대로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-158">This approach works fine for scenarios where the HTML UI we want to create within our view template corresponds relatively closely to our domain model objects.</span></span>

<span data-ttu-id="85015-159">이 시나리오에 대 한 경우 사용할 수 있는 옵션 중 하나를 뷰에서 – 소비에 대 한 개체 모델로 최적화 더 되 고 기본 도메인 모델 개체와에서 다 같습니다 사용자 지정 모양의 ViewModel 클래스를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85015-159">For scenarios where this isn't the case, one option that you can use is to create a custom-shaped ViewModel class whose object model is more optimized for consumption by the view – and which might look completely different from the underlying domain model object.</span></span> <span data-ttu-id="85015-160">예를 들어 서로 다른 속성 이름 및/또는 여러 모델 개체에서 수집 하는 집계 속성 노출 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85015-160">For example, it could potentially expose different property names and/or aggregate properties collected from multiple model objects.</span></span>

<span data-ttu-id="85015-161">사용자 지정 모양의 ViewModel 클래스 수 모두 뷰를 렌더링 하려면 뿐만 아니라 컨트롤러의 동작 메서드를 다시 게시 하는 양식 데이터를 처리 하려면 컨트롤러에서 데이터를 전달 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-161">Custom-shaped ViewModel classes can be used both to pass data from controllers to views to render, as well as to help handle form data posted back to a controller's action method.</span></span> <span data-ttu-id="85015-162">나중이 시나리오에 대 한 폼 게시 데이터를 사용 된 ViewModel 개체를 업데이트 하 고 다음 ViewModel 인스턴스를 사용 하 여 매핑하거나 실제 도메인 모델 개체를 검색할 작업 메서드를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85015-162">For this later scenario, you might have the action method update a ViewModel object with the form-posted data, and then use the ViewModel instance to map or retrieve an actual domain model object.</span></span>

<span data-ttu-id="85015-163">ViewModel 클래스 사용자 지정 모양의 많은 유연성을 제공할 수 있습니다 및은 시작 너무 복잡 하는 작업 메서드 내 보기 템플릿 또는 폼 게시 코드 내에서 렌더링 코드를 찾을 언제 든 지 조사 해야 할 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="85015-163">Custom-shaped ViewModel classes can provide a great deal of flexibility, and are something to investigate any time you find the rendering code within your view templates or the form-posting code inside your action methods starting to get too complicated.</span></span> <span data-ttu-id="85015-164">이 도메인 모델을 생성 하는 UI 완전히 동일 하지 않습니다는 및 중간 사용자 지정 모양의 ViewModel 클래스가 도와 나타내기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-164">This is often a sign that your domain models don't cleanly correspond to the UI you are generating, and that an intermediate custom-shaped ViewModel class can help.</span></span>

### <a name="next-step"></a><span data-ttu-id="85015-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="85015-165">Next Step</span></span>

<span data-ttu-id="85015-166">이제 살펴보겠습니다 사용 하는 방법을 부분 및 마스터 페이지를 다시 사용 하 고 응용 프로그램에서 UI를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="85015-166">Let's now look at how we can use partials and master-pages to re-use and share UI across our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="85015-167">[이전](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [다음](re-use-ui-using-master-pages-and-partials.md)</span><span class="sxs-lookup"><span data-stu-id="85015-167">[Previous](provide-crud-create-read-update-delete-data-form-entry-support.md)
[Next](re-use-ui-using-master-pages-and-partials.md)</span></span>
