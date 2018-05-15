---
title: ASP.NET Core의 보기 구성 요소
author: rick-anderson
description: ASP.NET Core에서 보기 구성 요소가 사용되는 방법 및 이를 앱에 추가하는 방법을 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 02/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/view-components
ms.openlocfilehash: a3614024c7f776e4502bc049180ae1c965e31db4
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="view-components-in-aspnet-core"></a><span data-ttu-id="db3c0-103">ASP.NET Core의 보기 구성 요소</span><span class="sxs-lookup"><span data-stu-id="db3c0-103">View components in ASP.NET Core</span></span>

<span data-ttu-id="db3c0-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="db3c0-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="db3c0-105">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="db3c0-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="introducing-view-components"></a><span data-ttu-id="db3c0-106">뷰 구성 요소 소개</span><span class="sxs-lookup"><span data-stu-id="db3c0-106">Introducing view components</span></span>

<span data-ttu-id="db3c0-107">ASP.NET Core MVC에 새로 도입된 뷰 구성 요소는 부분 뷰와 유사하지만 훨씬 강력합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-107">New to ASP.NET Core MVC, view components are similar to partial views, but they're much more powerful.</span></span> <span data-ttu-id="db3c0-108">뷰 구성 요소는 모델 바인딩을 사용하지 않으며 호출할 때 제공되는 데이터에만 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-108">View components don't use model binding, and only depend on the data provided when calling into it.</span></span> <span data-ttu-id="db3c0-109">뷰 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="db3c0-109">A view component:</span></span>

* <span data-ttu-id="db3c0-110">전체 응답보다는 청크를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-110">Renders a chunk rather than a whole response.</span></span>
* <span data-ttu-id="db3c0-111">컨트롤러 및 뷰 간에 확인할 수 있는 동일한 개념 분리 및 테스트 가능성 이점을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-111">Includes the same separation-of-concerns and testability benefits found between a controller and view.</span></span>
* <span data-ttu-id="db3c0-112">매개 변수 및 비즈니스 논리를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-112">Can have parameters and business logic.</span></span>
* <span data-ttu-id="db3c0-113">일반적으로 레이아웃 페이지에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-113">Is typically invoked from a layout page.</span></span>

<span data-ttu-id="db3c0-114">뷰 구성 요소는 다음과 같이 부분 뷰에 대해 너무 복잡한 재사용 가능한 렌더링 논리를 포함하는 모든 곳에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-114">View components are intended anywhere you have reusable rendering logic that's too complex for a partial view, such as:</span></span>

* <span data-ttu-id="db3c0-115">동적 탐색 메뉴</span><span class="sxs-lookup"><span data-stu-id="db3c0-115">Dynamic navigation menus</span></span>
* <span data-ttu-id="db3c0-116">태그 클라우드(여기서는 데이터베이스를 쿼리)</span><span class="sxs-lookup"><span data-stu-id="db3c0-116">Tag cloud (where it queries the database)</span></span>
* <span data-ttu-id="db3c0-117">로그인 패널</span><span class="sxs-lookup"><span data-stu-id="db3c0-117">Login panel</span></span>
* <span data-ttu-id="db3c0-118">쇼핑 카트</span><span class="sxs-lookup"><span data-stu-id="db3c0-118">Shopping cart</span></span>
* <span data-ttu-id="db3c0-119">최근에 게시된 문서</span><span class="sxs-lookup"><span data-stu-id="db3c0-119">Recently published articles</span></span>
* <span data-ttu-id="db3c0-120">일반적인 블로그에서 추가 기사 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="db3c0-120">Sidebar content on a typical blog</span></span>
* <span data-ttu-id="db3c0-121">모든 페이지에 렌더링되고 사용자의 로그인 상태에 따라 로그아웃 또는 로그인하는 링크를 표시하는 로그인 패널</span><span class="sxs-lookup"><span data-stu-id="db3c0-121">A login panel that would be rendered on every page and show either the links to log out or log in, depending on the log in state of the user</span></span>

<span data-ttu-id="db3c0-122">뷰 구성 요소는 클래스(일반적으로 [ViewComponent](/dotnet/api/microsoft.aspnetcore.mvc.viewcomponent)에서 파생됨)와 반환되는 결과(일반적으로 뷰)의 두 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-122">A view component consists of two parts: the class (typically derived from [ViewComponent](/dotnet/api/microsoft.aspnetcore.mvc.viewcomponent)) and the result it returns (typically a view).</span></span> <span data-ttu-id="db3c0-123">컨트롤러와 마찬가지로, 뷰 구성 요소는 POCO일 수 있지만 대부분의 개발자는 `ViewComponent`에서 파생되어 사용 가능한 메서드와 속성을 활용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-123">Like controllers, a view component can be a POCO, but most developers will want to take advantage of the methods and properties available by deriving from `ViewComponent`.</span></span>

## <a name="creating-a-view-component"></a><span data-ttu-id="db3c0-124">뷰 구성 요소 만들기</span><span class="sxs-lookup"><span data-stu-id="db3c0-124">Creating a view component</span></span>

<span data-ttu-id="db3c0-125">이 섹션에서는 뷰 구성 요소를 만들기 위한 전반적인 요구 사항이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-125">This section contains the high-level requirements to create a view component.</span></span> <span data-ttu-id="db3c0-126">이 문서의 뒷부분에서는 각 단계를 자세히 검토하고 뷰 구성 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-126">Later in the article, we'll examine each step in detail and create a view component.</span></span>

### <a name="the-view-component-class"></a><span data-ttu-id="db3c0-127">뷰 구성 요소 클래스</span><span class="sxs-lookup"><span data-stu-id="db3c0-127">The view component class</span></span>

<span data-ttu-id="db3c0-128">다음 방법으로 뷰 구성 요소 클래스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-128">A view component class can be created by any of the following:</span></span>

* <span data-ttu-id="db3c0-129">*ViewComponent*에서 파생</span><span class="sxs-lookup"><span data-stu-id="db3c0-129">Deriving from *ViewComponent*</span></span>
* <span data-ttu-id="db3c0-130">`[ViewComponent]` 특성으로 클래스 데코레이팅 또는 `[ViewComponent]` 특성을 사용하여 클래스에서 파생</span><span class="sxs-lookup"><span data-stu-id="db3c0-130">Decorating a class with the `[ViewComponent]` attribute, or deriving from a class with the `[ViewComponent]` attribute</span></span>
* <span data-ttu-id="db3c0-131">이름이 *ViewComponent* 접미사로 끝나는 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="db3c0-131">Creating a class where the name ends with the suffix *ViewComponent*</span></span>

<span data-ttu-id="db3c0-132">컨트롤러와 마찬가지로, 뷰 구성 요소는 공용이고 비중첩 및 비추상 클래스여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-132">Like controllers, view components must be public, non-nested, and non-abstract classes.</span></span> <span data-ttu-id="db3c0-133">뷰 구성 요소 이름은 "ViewComponent" 접미사가 제거된 클래스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-133">The view component name is the class name with the "ViewComponent" suffix removed.</span></span> <span data-ttu-id="db3c0-134">또한 `ViewComponentAttribute.Name` 속성을 사용하여 명시적으로 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-134">It can also be explicitly specified using the `ViewComponentAttribute.Name` property.</span></span>

<span data-ttu-id="db3c0-135">뷰 구성 요소 클래스:</span><span class="sxs-lookup"><span data-stu-id="db3c0-135">A view component class:</span></span>

* <span data-ttu-id="db3c0-136">생성자 [종속성 주입](../../fundamentals/dependency-injection.md)을 완전히 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-136">Fully supports constructor [dependency injection](../../fundamentals/dependency-injection.md)</span></span>

* <span data-ttu-id="db3c0-137">컨트롤러 수명 주기를 따르지 않습니다. 즉, 뷰 구성 요소에 [필터](../controllers/filters.md)를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-137">Doesn't take part in the controller lifecycle, which means you can't use [filters](../controllers/filters.md) in a view component</span></span>

### <a name="view-component-methods"></a><span data-ttu-id="db3c0-138">뷰 구성 요소 메서드</span><span class="sxs-lookup"><span data-stu-id="db3c0-138">View component methods</span></span>

<span data-ttu-id="db3c0-139">뷰 구성 요소는 해당 논리를 `IViewComponentResult`를 반환하는 `InvokeAsync` 메서드에 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-139">A view component defines its logic in an `InvokeAsync` method that returns an `IViewComponentResult`.</span></span> <span data-ttu-id="db3c0-140">매개 변수는 모델 바인딩이 아닌 뷰 구성 요소 호출에서 직접 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-140">Parameters come directly from invocation of the view component, not from model binding.</span></span> <span data-ttu-id="db3c0-141">뷰 구성 요소는 요청을 직접 처리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-141">A view component never directly handles a request.</span></span> <span data-ttu-id="db3c0-142">일반적으로 뷰 구성 요소는 모델을 초기화하고 `View` 메서드를 호출하여 뷰에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-142">Typically, a view component initializes a model and passes it to a view by calling the `View` method.</span></span> <span data-ttu-id="db3c0-143">요약하자면, 뷰 구성 요소 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-143">In summary, view component methods:</span></span>

* <span data-ttu-id="db3c0-144">`IViewComponentResult`를 반환하는 `InvokeAsync` 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-144">Define an `InvokeAsync` method that returns an `IViewComponentResult`</span></span>
* <span data-ttu-id="db3c0-145">일반적으로 모델을 초기화하고 `ViewComponent` `View` 메서드를 호출하여 뷰에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-145">Typically initializes a model and passes it to a view by calling the `ViewComponent` `View` method</span></span>
* <span data-ttu-id="db3c0-146">매개 변수는 HTTP가 아닌 호출 메서드에서 가져오며 모델 바인딩이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-146">Parameters come from the calling method, not HTTP, there's no model binding</span></span>
* <span data-ttu-id="db3c0-147">HTTP 끝점으로 직접 연결할 수 없으며 코드(일반적으로 뷰에서)에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-147">Are not reachable directly as an HTTP endpoint, they're invoked from your code (usually in a view).</span></span> <span data-ttu-id="db3c0-148">뷰 구성 요소는 요청을 처리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-148">A view component never handles a request</span></span>
* <span data-ttu-id="db3c0-149">현재 HTTP 요청의 세부 정보가 아닌 서명에 오버로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-149">Are overloaded on the signature rather than any details from the current HTTP request</span></span>

### <a name="view-search-path"></a><span data-ttu-id="db3c0-150">뷰 검색 경로</span><span class="sxs-lookup"><span data-stu-id="db3c0-150">View search path</span></span>

<span data-ttu-id="db3c0-151">런타임은 다음 경로에서 뷰를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-151">The runtime searches for the view in the following paths:</span></span>

   * <span data-ttu-id="db3c0-152">Views/\<controller_name>/Components/\<view_component_name>/\<view_name></span><span class="sxs-lookup"><span data-stu-id="db3c0-152">Views/\<controller_name>/Components/\<view_component_name>/\<view_name></span></span>
   * <span data-ttu-id="db3c0-153">Views/Shared/Components/\<view_component_name>/\<view_name></span><span class="sxs-lookup"><span data-stu-id="db3c0-153">Views/Shared/Components/\<view_component_name>/\<view_name></span></span>

<span data-ttu-id="db3c0-154">뷰 구성 요소에 대한 기본 뷰 이름은 *Default*이며 이것은 일반적으로 뷰 파일의 이름이 *Default.cshtml*로 지정됨을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-154">The default view name for a view component is *Default*, which means your view file will typically be named *Default.cshtml*.</span></span> <span data-ttu-id="db3c0-155">뷰 구성 요소 결과를 만들거나 `View` 메서드를 호출할 때 다른 뷰 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-155">You can specify a different view name when creating the view component result or when calling the `View` method.</span></span>

<span data-ttu-id="db3c0-156">뷰 파일 이름을 *Default.cshtml*로 지정하고 *Views/Shared/Components/\<view_component_name>/\<view_name>* 경로를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-156">We recommend you name the view file *Default.cshtml* and use the *Views/Shared/Components/\<view_component_name>/\<view_name>* path.</span></span> <span data-ttu-id="db3c0-157">이 샘플에 사용된 `PriorityList` 뷰 구성 요소는 뷰 구성 요소 보기에 *Views/Shared/Components/PriorityList/Default.cshtml*을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-157">The `PriorityList` view component used in this sample uses *Views/Shared/Components/PriorityList/Default.cshtml* for the view component view.</span></span>

## <a name="invoking-a-view-component"></a><span data-ttu-id="db3c0-158">뷰 구성 요소 호출</span><span class="sxs-lookup"><span data-stu-id="db3c0-158">Invoking a view component</span></span>

<span data-ttu-id="db3c0-159">뷰 구성 요소를 사용하려면 뷰 내에서 다음을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-159">To use the view component, call the following inside a view:</span></span>

```cshtml
@Component.InvokeAsync("Name of view component", <anonymous type containing parameters>)
```

<span data-ttu-id="db3c0-160">매개 변수가 `InvokeAsync` 메서드에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-160">The parameters will be passed to the `InvokeAsync` method.</span></span> <span data-ttu-id="db3c0-161">문서에서 개발된 `PriorityList` 뷰 구성 요소가 *Views/Todo/Index.cshtml* 뷰 파일에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-161">The `PriorityList` view component developed in the article is invoked from the *Views/Todo/Index.cshtml* view file.</span></span> <span data-ttu-id="db3c0-162">다음에서 `InvokeAsync` 메서드는 두 매개 변수를 사용하여 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-162">In the following, the `InvokeAsync` method is called with two parameters:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/Todo/IndexFinal.cshtml?range=35)]

## <a name="invoking-a-view-component-as-a-tag-helper"></a><span data-ttu-id="db3c0-163">태그 도우미로 뷰 구성 요소 호출</span><span class="sxs-lookup"><span data-stu-id="db3c0-163">Invoking a view component as a Tag Helper</span></span>

<span data-ttu-id="db3c0-164">ASP.NET Core 1.1 이상에서는 뷰 구성 요소를 [태그 도우미](xref:mvc/views/tag-helpers/intro)로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-164">For ASP.NET Core 1.1 and higher, you can invoke a view component as a [Tag Helper](xref:mvc/views/tag-helpers/intro):</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/Todo/IndexTagHelper.cshtml?range=37-38)]

<span data-ttu-id="db3c0-165">태그 도우미에 대한 파스칼식 클래스 및 메서드 매개 변수가 [kebab 소문자](https://stackoverflow.com/questions/11273282/whats-the-name-for-dash-separated-case/12273101)로 번역됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-165">Pascal-cased class and method parameters for Tag Helpers are translated into their [lower kebab case](https://stackoverflow.com/questions/11273282/whats-the-name-for-dash-separated-case/12273101).</span></span> <span data-ttu-id="db3c0-166">뷰 구성 요소를 호출하는 태그 도우미는 `<vc></vc>` 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-166">The Tag Helper to invoke a view component uses the `<vc></vc>` element.</span></span> <span data-ttu-id="db3c0-167">뷰 구성 요소는 다음과 같이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-167">The view component is specified as follows:</span></span>

```cshtml
<vc:[view-component-name]
  parameter1="parameter1 value"
  parameter2="parameter2 value">
</vc:[view-component-name]>
```

<span data-ttu-id="db3c0-168">참고: 태그 도우미로 뷰 구성 요소를 사용하려면 `@addTagHelper` 지시문을 사용하여 뷰 구성 요소가 포함된 어셈블리를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-168">Note: In order to use a View Component as a Tag Helper, you must register the assembly containing the View Component using the `@addTagHelper` directive.</span></span> <span data-ttu-id="db3c0-169">예를 들어 뷰 구성 요소가 "MyWebApp"이라는 어셈블리에 있으면 다음 지시문을 `_ViewImports.cshtml` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-169">For example, if your View Component is in an assembly called "MyWebApp", add the following directive to the `_ViewImports.cshtml` file:</span></span>

```cshtml
@addTagHelper *, MyWebApp
```

<span data-ttu-id="db3c0-170">뷰 구성 요소를 참조하는 모든 파일에 태그 도우미로 뷰 구성 요소를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-170">You can register a View Component as a Tag Helper to any file that references the View Component.</span></span> <span data-ttu-id="db3c0-171">태그 도우미를 등록하는 방법에 대한 자세한 내용은 [태그 도우미 범위 관리](xref:mvc/views/tag-helpers/intro#managing-tag-helper-scope)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db3c0-171">See [Managing Tag Helper Scope](xref:mvc/views/tag-helpers/intro#managing-tag-helper-scope) for more information on how to register Tag Helpers.</span></span>

<span data-ttu-id="db3c0-172">이 자습서에 사용된 `InvokeAsync` 메서드:</span><span class="sxs-lookup"><span data-stu-id="db3c0-172">The `InvokeAsync` method used in this tutorial:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/Todo/IndexFinal.cshtml?range=35)]

<span data-ttu-id="db3c0-173">태그 도우미 태그에서:</span><span class="sxs-lookup"><span data-stu-id="db3c0-173">In Tag Helper markup:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/Todo/IndexTagHelper.cshtml?range=37-38)]

<span data-ttu-id="db3c0-174">위의 샘플에서 `PriorityList` 뷰 구성 요소는 `priority-list`가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-174">In the sample above, the `PriorityList` view component becomes `priority-list`.</span></span> <span data-ttu-id="db3c0-175">뷰 구성 요소에 대한 매개 변수는 kebab 소문자의 특성으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-175">The parameters to the view component are passed as attributes in lower kebab case.</span></span>

### <a name="invoking-a-view-component-directly-from-a-controller"></a><span data-ttu-id="db3c0-176">컨트롤러에서 뷰 구성 요소 직접 호출</span><span class="sxs-lookup"><span data-stu-id="db3c0-176">Invoking a view component directly from a controller</span></span>

<span data-ttu-id="db3c0-177">일반적으로 뷰 구성 요소는 뷰에서 호출되지만 컨트롤러 메서드에서 직접 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-177">View components are typically invoked from a view, but you can invoke them directly from a controller method.</span></span> <span data-ttu-id="db3c0-178">뷰 구성 요소는 컨트롤러와 같은 끝점을 정의하지 않지만 `ViewComponentResult`의 내용을 반환하는 컨트롤러 동작을 쉽게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-178">While view components don't define endpoints like controllers, you can easily implement a controller action that returns the content of a `ViewComponentResult`.</span></span>

<span data-ttu-id="db3c0-179">이 예제에서는 뷰 구성 요소가 컨트롤러에서 직접 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-179">In this example, the view component is called directly from the controller:</span></span>

[!code-csharp[](view-components/sample/ViewCompFinal/Controllers/ToDoController.cs?name=snippet_IndexVC)]

## <a name="walkthrough-creating-a-simple-view-component"></a><span data-ttu-id="db3c0-180">연습: 간단한 뷰 구성 요소 만들기</span><span class="sxs-lookup"><span data-stu-id="db3c0-180">Walkthrough: Creating a simple view component</span></span>

<span data-ttu-id="db3c0-181">시작 코드를 [다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample), 빌드 및 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-181">[Download](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample), build and test the starter code.</span></span> <span data-ttu-id="db3c0-182">*Todo* 항목의 목록을 표시하는 `Todo` 컨트롤러가 포함된 간단한 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-182">It's a simple project with a `Todo` controller that displays a list of *Todo* items.</span></span>

![ToDo 목록](view-components/_static/2dos.png)

### <a name="add-a-viewcomponent-class"></a><span data-ttu-id="db3c0-184">ViewComponent 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="db3c0-184">Add a ViewComponent class</span></span>

<span data-ttu-id="db3c0-185">*ViewComponents* 폴더를 만들고 다음 `PriorityListViewComponent` 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-185">Create a *ViewComponents* folder and add the following `PriorityListViewComponent` class:</span></span>

[!code-csharp[](view-components/sample/ViewCompFinal/ViewComponents/PriorityListViewComponent1.cs?name=snippet1)]

<span data-ttu-id="db3c0-186">코드에 대한 참고 사항:</span><span class="sxs-lookup"><span data-stu-id="db3c0-186">Notes on the code:</span></span>

* <span data-ttu-id="db3c0-187">뷰 구성 요소 클래스는 프로젝트의 **모든** 폴더에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-187">View component classes can be contained in **any** folder in the project.</span></span>
* <span data-ttu-id="db3c0-188">클래스 이름 PriorityList**ViewComponent**는 **ViewComponent** 접미사로 끝나기 때문에 런타임은 뷰에서 클래스 구성 요소를 참조할 때 "PriorityList" 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-188">Because the class name PriorityList**ViewComponent** ends with the suffix **ViewComponent**, the runtime will use the string "PriorityList" when referencing the class component from a view.</span></span> <span data-ttu-id="db3c0-189">나중에 보다 자세히 설명하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-189">I'll explain that in more detail later.</span></span>
* <span data-ttu-id="db3c0-190">`[ViewComponent]` 특성은 뷰 구성 요소를 참조하는 데 사용된 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-190">The `[ViewComponent]` attribute can change the name used to reference a view component.</span></span> <span data-ttu-id="db3c0-191">예를 들어 클래스 `XYZ`의 이름을 지정하고 `ViewComponent` 특성을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-191">For example, we could've named the class `XYZ` and applied the `ViewComponent` attribute:</span></span>

  ```csharp
  [ViewComponent(Name = "PriorityList")]
     public class XYZ : ViewComponent
     ```

* <span data-ttu-id="db3c0-192">위의 `[ViewComponent]` 특성은 구성 요소와 연관된 뷰를 찾을 때 `PriorityList` 이름을 사용하고, 뷰에서 클래스 구성 요소를 참조할 때 "PriorityList" 문자열을 사용하도록 뷰 구성 요소 선택기에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-192">The `[ViewComponent]` attribute above tells the view component selector to use the name `PriorityList` when looking for the views associated with the component, and to use the string "PriorityList" when referencing the class component from a view.</span></span> <span data-ttu-id="db3c0-193">나중에 보다 자세히 설명하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-193">I'll explain that in more detail later.</span></span>
* <span data-ttu-id="db3c0-194">이 구성 요소에서는 [종속성 주입](../../fundamentals/dependency-injection.md)을 사용하여 데이터 컨텍스트를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-194">The component uses [dependency injection](../../fundamentals/dependency-injection.md) to make the data context available.</span></span>
* <span data-ttu-id="db3c0-195">`InvokeAsync`는 뷰에서 호출할 수 있는 메서드를 노출하며 임의 수의 인수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-195">`InvokeAsync` exposes a method which can be called from a view, and it can take an arbitrary number of arguments.</span></span>
* <span data-ttu-id="db3c0-196">`InvokeAsync` 메서드는 `isDone` 및 `maxPriority` 매개변수를 충족하는 `ToDo` 항목 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-196">The `InvokeAsync` method returns the set of `ToDo` items that satisfy the `isDone` and `maxPriority` parameters.</span></span>

### <a name="create-the-view-component-razor-view"></a><span data-ttu-id="db3c0-197">뷰 구성 요소 Razor 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="db3c0-197">Create the view component Razor view</span></span>

* <span data-ttu-id="db3c0-198">*Views/Shared/Components* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-198">Create the *Views/Shared/Components* folder.</span></span> <span data-ttu-id="db3c0-199">이 폴더의 이름은 *Components*로 **지정되어야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-199">This folder **must** be named *Components*.</span></span>

* <span data-ttu-id="db3c0-200">*Views/Shared/Components/PriorityList* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-200">Create the *Views/Shared/Components/PriorityList* folder.</span></span> <span data-ttu-id="db3c0-201">이 폴더 이름은 뷰 구성 요소 클래스의 이름 또는 클래스 이름에서 접미사를 뺀 이름과 일치해야 합니다(규칙을 준수하고 클래스 이름에 *ViewComponent* 접미사를 사용한 경우).</span><span class="sxs-lookup"><span data-stu-id="db3c0-201">This folder name must match the name of the view component class, or the name of the class minus the suffix (if we followed convention and used the *ViewComponent* suffix in the class name).</span></span> <span data-ttu-id="db3c0-202">`ViewComponent` 특성을 사용한 경우 클래스 이름은 특성 지정과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-202">If you used the `ViewComponent` attribute, the class name would need to match the attribute designation.</span></span>

* <span data-ttu-id="db3c0-203">*Views/Shared/Components/PriorityList/Default.cshtml* Razor 뷰를 만듭니다. [!code-cshtml[](view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/Default1.cshtml)]</span><span class="sxs-lookup"><span data-stu-id="db3c0-203">Create a *Views/Shared/Components/PriorityList/Default.cshtml* Razor view: [!code-cshtml[](view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/Default1.cshtml)]</span></span>
    
   <span data-ttu-id="db3c0-204">Razor 뷰는 `TodoItem` 목록을 가져와 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-204">The Razor view takes a list of `TodoItem` and displays them.</span></span> <span data-ttu-id="db3c0-205">뷰 구성 요소 `InvokeAsync` 메서드가 뷰의 이름을 전달하지 않은 경우(샘플에서처럼) 규칙에 따라 뷰 이름으로 *Default*가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-205">If the view component `InvokeAsync` method doesn't pass the name of the view (as in our sample), *Default* is used for the view name by convention.</span></span> <span data-ttu-id="db3c0-206">자습서의 뒷부분에서 뷰 이름을 전달하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-206">Later in the tutorial, I'll show you how to pass the name of the view.</span></span> <span data-ttu-id="db3c0-207">특정 컨트롤러에 대한 기본 스타일 지정을 재정의하려면 컨트롤러 관련 뷰 폴더에 뷰를 추가합니다(예를 들어 *Views/Todo/Components/PriorityList/Default.cshtml)*.</span><span class="sxs-lookup"><span data-stu-id="db3c0-207">To override the default styling for a specific controller, add a view to the controller-specific view folder (for example *Views/Todo/Components/PriorityList/Default.cshtml)*.</span></span>
    
    <span data-ttu-id="db3c0-208">뷰 구성 요소가 컨트롤러에 관한 것이면 컨트롤러 관련 폴더에 추가할 수 있습니다(*Views/Todo/Components/PriorityList/Default.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="db3c0-208">If the view component is controller-specific, you can add it to the controller-specific folder (*Views/Todo/Components/PriorityList/Default.cshtml*).</span></span>

* <span data-ttu-id="db3c0-209">우선 순위 목록 구성 요소에 대한 호출을 포함하는 `div`를 *Views/Todo/index.cshtml* 파일 맨 아래에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-209">Add a `div` containing a call to the priority list component to the bottom of the *Views/Todo/index.cshtml* file:</span></span>

    [!code-cshtml[](view-components/sample/ViewCompFinal/Views/Todo/IndexFirst.cshtml?range=34-38)]

<span data-ttu-id="db3c0-210">`@await Component.InvokeAsync` 태그는 호출하는 뷰 구성 요소에 대한 구문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-210">The markup `@await Component.InvokeAsync` shows the syntax for calling view components.</span></span> <span data-ttu-id="db3c0-211">첫 번째 인수는 호출하려는 구성 요소의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-211">The first argument is the name of the component we want to invoke or call.</span></span> <span data-ttu-id="db3c0-212">후속 매개 변수는 구성 요소에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-212">Subsequent parameters are passed to the component.</span></span> <span data-ttu-id="db3c0-213">`InvokeAsync`는 임의 개수의 인수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-213">`InvokeAsync` can take an arbitrary number of arguments.</span></span>

<span data-ttu-id="db3c0-214">앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-214">Test the app.</span></span> <span data-ttu-id="db3c0-215">다음 이미지는 ToDo 목록 및 우선 순위 항목을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-215">The following image shows the ToDo list and the priority items:</span></span>

![todo 목록 및 우선 순위 항목](view-components/_static/pi.png)

<span data-ttu-id="db3c0-217">또한 컨트롤러에서 직접 뷰 구성 요소를 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-217">You can also call the view component directly from the controller:</span></span>

[!code-csharp[](view-components/sample/ViewCompFinal/Controllers/ToDoController.cs?name=snippet_IndexVC)]

![IndexVC 작업에서 우선 순위 항목](view-components/_static/indexvc.png)

### <a name="specifying-a-view-name"></a><span data-ttu-id="db3c0-219">뷰 이름 지정</span><span class="sxs-lookup"><span data-stu-id="db3c0-219">Specifying a view name</span></span>

<span data-ttu-id="db3c0-220">복잡한 뷰 구성 요소에는 조건에 따라 기본값이 아닌 뷰를 지정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-220">A complex view component might need to specify a non-default view under some conditions.</span></span> <span data-ttu-id="db3c0-221">다음 코드에서 `InvokeAsync` 메서드에서 "PVC" 뷰를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-221">The following code shows how to specify the "PVC" view  from the `InvokeAsync` method.</span></span> <span data-ttu-id="db3c0-222">`PriorityListViewComponent` 클래스에서 `InvokeAsync` 메서드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-222">Update the `InvokeAsync` method in the `PriorityListViewComponent` class.</span></span>

[!code-csharp[](../../mvc/views/view-components/sample/ViewCompFinal/ViewComponents/PriorityListViewComponentFinal.cs?highlight=4,5,6,7,8,9&range=28-39)]

<span data-ttu-id="db3c0-223">*Views/Shared/Components/PriorityList/Default.cshtml* 파일을 *Views/Shared/Components/PriorityList/PVC.cshtml*이라는 뷰에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-223">Copy the *Views/Shared/Components/PriorityList/Default.cshtml* file to a view named *Views/Shared/Components/PriorityList/PVC.cshtml*.</span></span> <span data-ttu-id="db3c0-224">PVC 뷰가 사용되었다는 것을 나타내는 제목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-224">Add a heading to indicate the PVC view is being used.</span></span>

[!code-cshtml[](../../mvc/views/view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/PVC.cshtml?highlight=3)]

<span data-ttu-id="db3c0-225">*Views/TodoList/Index.cshtml*을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-225">Update *Views/TodoList/Index.cshtml*:</span></span>

<!-- Views/TodoList/Index.cshtml is never imported, so change to test tutorial -->

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/Todo/IndexFinal.cshtml?range=35)]

<span data-ttu-id="db3c0-226">앱을 실행하고 PVC 뷰를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-226">Run the app and verify PVC view.</span></span>

![우선 순위 뷰 구성 요소](view-components/_static/pvc.png)

<span data-ttu-id="db3c0-228">PVC 뷰가 렌더링되지 않는 경우 우선 순위가 4 이상인 뷰 구성 요소를 호출하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-228">If the PVC view isn't rendered, verify you are calling the view component with a priority of 4 or higher.</span></span>

### <a name="examine-the-view-path"></a><span data-ttu-id="db3c0-229">뷰 경로 검사</span><span class="sxs-lookup"><span data-stu-id="db3c0-229">Examine the view path</span></span>

* <span data-ttu-id="db3c0-230">우선 순위 뷰가 반환되지 않도록 우선 순위 매개 변수를 3 이하로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-230">Change the priority parameter to three or less so the priority view isn't returned.</span></span>
* <span data-ttu-id="db3c0-231">*Views/Todo/Components/PriorityList/Default.cshtml*의 이름을 *1Default.cshtml*로 임시로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-231">Temporarily rename the *Views/Todo/Components/PriorityList/Default.cshtml* to *1Default.cshtml*.</span></span>
* <span data-ttu-id="db3c0-232">앱을 테스트하면 다음과 같은 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-232">Test the app, you'll get the following error:</span></span>

   ```
   An unhandled exception occurred while processing the request.
   InvalidOperationException: The view 'Components/PriorityList/Default' wasn't found. The following locations were searched:
   /Views/ToDo/Components/PriorityList/Default.cshtml
   /Views/Shared/Components/PriorityList/Default.cshtml
   EnsureSuccessful
   ```

* <span data-ttu-id="db3c0-233">*Views/Todo/Components/PriorityList/1Default.cshtml*을 *Views/Shared/Components/PriorityList/Default.cshtml*에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-233">Copy *Views/Todo/Components/PriorityList/1Default.cshtml* to *Views/Shared/Components/PriorityList/Default.cshtml*.</span></span>
* <span data-ttu-id="db3c0-234">*Shared* Todo 뷰 구성 요소 보기에 일부 태그를 추가하여 뷰가 *Shared* 폴더에 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-234">Add some markup to the *Shared* Todo view component view to indicate the view is from the *Shared* folder.</span></span>
* <span data-ttu-id="db3c0-235">**Shared** 구성 요소 뷰를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-235">Test the **Shared** component view.</span></span>

![공유 구성 요소 뷰가 있는 ToDo 출력](view-components/_static/shared.png)

### <a name="avoiding-magic-strings"></a><span data-ttu-id="db3c0-237">매직 문자열 방지</span><span class="sxs-lookup"><span data-stu-id="db3c0-237">Avoiding magic strings</span></span>

<span data-ttu-id="db3c0-238">컴파일 시간 안전성을 원하는 경우 하드 코드된 뷰 구성 요소 이름을 클래스 이름으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-238">If you want compile time safety, you can replace the hard-coded view component name with the class name.</span></span> <span data-ttu-id="db3c0-239">"ViewComponent" 접미사 없이 뷰 구성 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-239">Create the view component without the "ViewComponent" suffix:</span></span>

[!code-csharp[](../../mvc/views/view-components/sample/ViewCompFinal/ViewComponents/PriorityList.cs?highlight=10&range=5-35)]

<span data-ttu-id="db3c0-240">`using` 문을 Razor 뷰 파일에 추가하고 `nameof` 연산자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db3c0-240">Add a `using` statement to your Razor view file, and use the `nameof` operator:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/Todo/IndexNameof.cshtml?range=1-6,35-)]

## <a name="additional-resources"></a><span data-ttu-id="db3c0-241">추가 자료</span><span class="sxs-lookup"><span data-stu-id="db3c0-241">Additional resources</span></span>

* [<span data-ttu-id="db3c0-242">뷰에 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="db3c0-242">Dependency injection into views</span></span>](xref:mvc/views/dependency-injection)
