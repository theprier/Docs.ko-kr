---
title: ASP.NET Core에서 필터링
author: ardalis
description: 필터 작동 방법 및 ASP.NET Core MVC에서 사용하는 방법을 자세히 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 4/10/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/controllers/filters
ms.openlocfilehash: 24e754daa68d5247fa444e87ba733891c908d32c
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="filters-in-aspnet-core"></a><span data-ttu-id="a2266-103">ASP.NET Core에서 필터링</span><span class="sxs-lookup"><span data-stu-id="a2266-103">Filters in ASP.NET Core</span></span>

<span data-ttu-id="a2266-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra/) 및 [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="a2266-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra/), and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="a2266-105">ASP.NET Core MVC에서 *필터*를 사용하면 요청 처리 파이프라인의 특정 단계 전후에 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-105">*Filters* in ASP.NET Core MVC allow you to run code before or after specific stages in the request processing pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2266-106">이 항목은 Razor 페이지에 적용되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="a2266-106">This topic does **not** apply to Razor Pages.</span></span> <span data-ttu-id="a2266-107">ASP.NET Core 2.1 미리 보기 및 이상에서는 Razor 페이지에 대해 [IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter?view=aspnetcore-2.0) 및 [IAsyncPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncpagefilter?view=aspnetcore-2.0)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-107">ASP.NET Core 2.1 preview and later supports [IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter?view=aspnetcore-2.0) and [IAsyncPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncpagefilter?view=aspnetcore-2.0) for Razor Pages.</span></span> <span data-ttu-id="a2266-108">자세한 내용은 [Razor 페이지에 대한 필터 메서드](xref:mvc/razor-pages/filter)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a2266-108">For more information, see [Filter methods for Razor Pages](xref:mvc/razor-pages/filter).</span></span>

 <span data-ttu-id="a2266-109">기본 제공 필터는 다음과 같은 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-109">Built-in filters handle tasks such as:</span></span>
 
 * <span data-ttu-id="a2266-110">권한 부여(사용자가 권한이 없는 리소스에 액세스 방지).</span><span class="sxs-lookup"><span data-stu-id="a2266-110">Authorization (preventing access to resources a user isn't authorized for).</span></span>
 * <span data-ttu-id="a2266-111">모든 요청이 HTTPS를 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-111">Ensuring that all requests use HTTPS.</span></span>
 * <span data-ttu-id="a2266-112">응답 캐싱(요청 파이프라인을 단락하면 캐시된 응답을 반환합니다).</span><span class="sxs-lookup"><span data-stu-id="a2266-112">Response caching (short-circuiting the request pipeline to return a cached response).</span></span> 

<span data-ttu-id="a2266-113">사용자 지정 필터를 만들어 교차 편집 문제를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-113">Custom filters can be created to handle cross-cutting concerns.</span></span> <span data-ttu-id="a2266-114">필터는 작업 간 코드 중복을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-114">Filters can avoid duplicating code across actions.</span></span> <span data-ttu-id="a2266-115">예를 들어 오류 처리 예외 필터는 오류 처리를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-115">For example, an error handling exception filter could consolidate error handling.</span></span>

<span data-ttu-id="a2266-116">[GitHub에서 샘플 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/filters/sample)</span><span class="sxs-lookup"><span data-stu-id="a2266-116">[View or download sample from GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/filters/sample).</span></span>

## <a name="how-do-filters-work"></a><span data-ttu-id="a2266-117">필터 작동 방법</span><span class="sxs-lookup"><span data-stu-id="a2266-117">How do filters work?</span></span>

<span data-ttu-id="a2266-118">필터는 *필터 파이프라인*이라고도 하는 *MVC 동작 호출 파이프라인*내에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-118">Filters run within the *MVC action invocation pipeline*, sometimes referred to as the *filter pipeline*.</span></span>  <span data-ttu-id="a2266-119">필터 파이프라인은 MVC가 실행할 작업을 선택한 후에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-119">The filter pipeline runs after MVC selects the action to execute.</span></span>

![다른 미들웨어, 라우팅 미들웨어, 작업 선택 영역 및 MVC 작업 호출 파이프라인을 통해 요청이 처리됩니다.](filters/_static/filter-pipeline-1.png)

### <a name="filter-types"></a><span data-ttu-id="a2266-122">필터 형식</span><span class="sxs-lookup"><span data-stu-id="a2266-122">Filter types</span></span>

<span data-ttu-id="a2266-123">각 필터 형식은 필터 파이프라인의 다른 단계에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-123">Each filter type is executed at a different stage in the filter pipeline.</span></span>

* <span data-ttu-id="a2266-124">[권한 부여 필터](#authorization-filters)는 먼저 실행되고 현재 사용자가 현재 요청에 대한 권한이 있는지 여부를 결정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-124">[Authorization filters](#authorization-filters) run first and are used to determine whether the current user is authorized for the current request.</span></span> <span data-ttu-id="a2266-125">요청이 인증되지 않는 경우 파이프라인을 단락(short-circuit) 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-125">They can short-circuit the pipeline if a request is unauthorized.</span></span> 

* <span data-ttu-id="a2266-126">[리소스 필터](#resource-filters)는 권한 부여 이후 먼저 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-126">[Resource filters](#resource-filters) are the first to handle a request after authorization.</span></span>  <span data-ttu-id="a2266-127">필터 파이프라인의 나머지 이전 및 파이프라인의 나머지가 완료된 후에 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-127">They can run code before the rest of the filter pipeline, and after the rest of the pipeline has completed.</span></span> <span data-ttu-id="a2266-128">캐싱을 구현하거나 그렇지 않은 경우 성능상의 이유로 필터 파이프라인을 단락(short-circuit) 처리하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-128">They're useful to implement caching or otherwise short-circuit the filter pipeline for performance reasons.</span></span> <span data-ttu-id="a2266-129">모델 바인딩 전에 실행하므로 모델 바인딩에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-129">They run before model binding, so they can influence model binding.</span></span>

* <span data-ttu-id="a2266-130">[작업 필터](#action-filters)는 개별 작업 메서드가 호출된 전후에 즉시 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-130">[Action filters](#action-filters) can run code immediately before and after an individual action method is called.</span></span> <span data-ttu-id="a2266-131">작업에 전달된 인수 및 작업에서 반환된 결과를 조작하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-131">They can be used to manipulate the arguments passed into an action and the result returned from the action.</span></span>

* <span data-ttu-id="a2266-132">[예외 필터](#exception-filters)는 응답 본문에 무언가 쓰여지기 전에 발생한 처리되지 않은 예외에 전역 정책을 적용하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-132">[Exception filters](#exception-filters) are used to apply global policies to unhandled exceptions that occur before anything has been written to the response body.</span></span>

* <span data-ttu-id="a2266-133">[결과 필터](#result-filters)는 개별 작업이 실행된 전후에 즉시 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-133">[Result filters](#result-filters) can run code immediately before and after the execution of individual action results.</span></span> <span data-ttu-id="a2266-134">작업 메서드가 성공적으로 실행되는 경우에만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-134">They run only when the action method has executed successfully.</span></span> <span data-ttu-id="a2266-135">보기 또는 포맷터 실행을 둘러싸야 하는 논리에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-135">They are useful for logic that must surround view or formatter execution.</span></span>

<span data-ttu-id="a2266-136">다음 다이어그램에서는 이러한 필터 형식이 필터 파이프라인에서 상호 작용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-136">The following diagram shows how these filter types interact in the filter pipeline.</span></span>

![요청은 권한 부여 필터, 리소스 필터, 모델 바인딩, 작업 필터, 작업 실행 및 작업 결과 변환, 예외 필터, 결과 필터 및 결과 실행을 통해 처리됩니다.](filters/_static/filter-pipeline-2.png)

## <a name="implementation"></a><span data-ttu-id="a2266-139">구현</span><span class="sxs-lookup"><span data-stu-id="a2266-139">Implementation</span></span>

<span data-ttu-id="a2266-140">필터는 다른 인터페이스 정의를 통해 동기 및 비동기 구현을 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-140">Filters support both synchronous and asynchronous implementations through different interface definitions.</span></span> 

<span data-ttu-id="a2266-141">동기 필터는 해당 파이프라인 단계가 On*Stage*Executing 및 On*Stage*Executed를 정의하는 전후에 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-141">Synchronous filters that can run code both before and after their pipeline stage define On*Stage*Executing and On*Stage*Executed methods.</span></span> <span data-ttu-id="a2266-142">예를 들어 `OnActionExecuting`은 작업 메서드를 호출하기 전에 호출되고 `OnActionExecuted`는 작업 메서드가 반환한 후에 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-142">For example, `OnActionExecuting` is called before the action method is called, and `OnActionExecuted` is called after the action method returns.</span></span>

[!code-csharp[](./filters/sample/src/FiltersSample/Filters/SampleActionFilter.cs?name=snippet1)]

<span data-ttu-id="a2266-143">비동기 필터는 단일 On*Stage*ExecutionAsync 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-143">Asynchronous filters define a single On*Stage*ExecutionAsync method.</span></span> <span data-ttu-id="a2266-144">이 메서드는 필터의 파이프라인 단계를 실행하는 *FilterType*ExecutionDelegate 대리자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-144">This method takes a *FilterType*ExecutionDelegate delegate which executes the filter's pipeline stage.</span></span> <span data-ttu-id="a2266-145">예를 들어 `ActionExecutionDelegate`는 작업 메서드를 호출하고 호출 전후에 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-145">For example, `ActionExecutionDelegate` calls the action method, and you can execute code before and after you call it.</span></span>

[!code-csharp[](./filters/sample/src/FiltersSample/Filters/SampleAsyncActionFilter.cs?highlight=6,8-10,13)]

<span data-ttu-id="a2266-146">단일 클래스에서 여러 필터 단계에 대한 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-146">You can implement interfaces for multiple filter stages in a single class.</span></span> <span data-ttu-id="a2266-147">예를 들어 [ActionFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.actionfilterattribute?view=aspnetcore-2.0) 클래스는 `IActionFilter`, `IResultFilter` 및 해당 비동기 값을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-147">For example, the [ActionFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.actionfilterattribute?view=aspnetcore-2.0) class implements `IActionFilter`, `IResultFilter`, and their async equivalents.</span></span>

> [!NOTE]
> <span data-ttu-id="a2266-148">필터 인터페이스의 동기 또는 비동기 버전 중 **하나**를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-148">Implement **either** the synchronous or the async version of a filter interface, not both.</span></span> <span data-ttu-id="a2266-149">프레임워크는 먼저 필터가 비동기 인터페이스를 구현하는지를 확인하고 그렇다면 이를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-149">The framework checks first to see if the filter implements the async interface, and if so, it calls that.</span></span> <span data-ttu-id="a2266-150">그렇지 않으면 동기 인터페이스의 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-150">If not, it calls the synchronous interface's method(s).</span></span> <span data-ttu-id="a2266-151">하나의 클래스에 두 인터페이스를 모두 구현하는 경우 비동기 메서드만이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-151">If you were to implement both interfaces on one class, only the async method would be called.</span></span> <span data-ttu-id="a2266-152">[ActionFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.actionfilterattribute?view=aspnetcore-2.0)와 같은 추상 클래스를 사용하는 경우 각 필터 형식에 대한 동기 메서드 또는 비동기 메서드만을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-152">When using abstract classes like [ActionFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.actionfilterattribute?view=aspnetcore-2.0) you would override only the synchronous methods or the async method for each filter type.</span></span>

### <a name="ifilterfactory"></a><span data-ttu-id="a2266-153">IFilterFactory</span><span class="sxs-lookup"><span data-stu-id="a2266-153">IFilterFactory</span></span>

<span data-ttu-id="a2266-154">`IFilterFactory`는 `IFilter`를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-154">`IFilterFactory` implements `IFilter`.</span></span> <span data-ttu-id="a2266-155">따라서 `IFilterFactory` 인스턴스를 필터 파이프라인에서 `IFilter` 인스턴스로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-155">Therefore, an `IFilterFactory` instance can be used as an `IFilter` instance anywhere in the filter pipeline.</span></span> <span data-ttu-id="a2266-156">프레임워크가 필터를 호출하려고 준비하는 경우 `IFilterFactory`으로 캐스팅을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-156">When the framework prepares to invoke the filter, it attempts to cast it to an `IFilterFactory`.</span></span> <span data-ttu-id="a2266-157">해당 캐스트에 성공하면 `CreateInstance` 메서드를 호출하여 호출되는 `IFilter` 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-157">If that cast succeeds, the `CreateInstance` method is called to create the `IFilter` instance that will be invoked.</span></span> <span data-ttu-id="a2266-158">앱이 시작될 때 정확한 필터 파이프라인을 명시적으로 설정할 필요가 없으므로 유연한 디자인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-158">This provides a flexible design, since the precise filter pipeline doesn't need to be set explicitly when the app starts.</span></span>

<span data-ttu-id="a2266-159">필터를 만드는 다른 방법으로 고유한 특성 구현에서 `IFilterFactory`를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-159">You can implement `IFilterFactory` on your own attribute implementations as another approach to creating filters:</span></span>

[!code-csharp[](./filters/sample/src/FiltersSample/Filters/AddHeaderWithFactoryAttribute.cs?name=snippet_IFilterFactory&highlight=1,4,5,6,7)]

### <a name="built-in-filter-attributes"></a><span data-ttu-id="a2266-160">기본 제공 필터 특성</span><span class="sxs-lookup"><span data-stu-id="a2266-160">Built-in filter attributes</span></span>

<span data-ttu-id="a2266-161">프레임워크에는 하위 클래스를 지정하고 사용자 지정할 수 있는 기본 제공 특성 기반 필터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-161">The framework includes built-in attribute-based filters that you can subclass and customize.</span></span> <span data-ttu-id="a2266-162">예를 들어 다음 결과 필터는 응답에 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-162">For example, the following Result filter adds a header to the response.</span></span>

<a name="add-header-attribute"></a>

[!code-csharp[](./filters/sample/src/FiltersSample/Filters/AddHeaderAttribute.cs?highlight=5,16)]

<span data-ttu-id="a2266-163">특성을 사용하면 위의 예제와 같이 필터에서 인수를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-163">Attributes allow filters to accept arguments, as shown in the example above.</span></span> <span data-ttu-id="a2266-164">컨트롤러나 작업 메서드에 이 특성을 추가하고 HTTP 헤더의 이름 및 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-164">You would add this attribute to a controller or action method and specify the name and value of the HTTP header:</span></span>

[!code-csharp[](./filters/sample/src/FiltersSample/Controllers/SampleController.cs?name=snippet_AddHeader&highlight=1)]

<span data-ttu-id="a2266-165">`Index` 작업의 결과는 다음과 같습니다. 응답 헤더는 오른쪽 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-165">The result of the `Index` action is shown below - the response headers are displayed on the bottom right.</span></span>

![작성자 Steve Smith @ardalis를 비롯한 응답 헤더를 보여주는 Microsoft Edge의 개발자 도구](filters/_static/add-header.png)

<span data-ttu-id="a2266-167">여러 필터 인터페이스에는 사용자 지정 구현에 대한 기본 클래스로 사용할 수 있는 해당 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-167">Several of the filter interfaces have corresponding attributes that can be used as base classes for custom implementations.</span></span>

<span data-ttu-id="a2266-168">필터 특성:</span><span class="sxs-lookup"><span data-stu-id="a2266-168">Filter attributes:</span></span>

* `ActionFilterAttribute`
* `ExceptionFilterAttribute`
* `ResultFilterAttribute`
* `FormatFilterAttribute`
* `ServiceFilterAttribute`
* `TypeFilterAttribute`

<span data-ttu-id="a2266-169">`TypeFilterAttribute` 및 `ServiceFilterAttribute`는 [이 문서의 뒷부분](#dependency-injection)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-169">`TypeFilterAttribute` and `ServiceFilterAttribute` are explained [later in this article](#dependency-injection).</span></span>

## <a name="filter-scopes-and-order-of-execution"></a><span data-ttu-id="a2266-170">필터 범위 및 실행 순서</span><span class="sxs-lookup"><span data-stu-id="a2266-170">Filter scopes and order of execution</span></span>

<span data-ttu-id="a2266-171">세 개의 *범위* 중 하나에서 파이프라인에 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-171">A filter can be added to the pipeline at one of three *scopes*.</span></span> <span data-ttu-id="a2266-172">특성을 사용하여 특정 작업 메서드 또는 컨트롤러 클래스에 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-172">You can add a filter to a particular action method or to a controller class by using an attribute.</span></span> <span data-ttu-id="a2266-173">또는 모든 컨트롤러와 동작에 대해 전역적으로 필터를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-173">Or you can register a filter globally for all controllers and actions.</span></span> <span data-ttu-id="a2266-174">`ConfigureServices`의 `MvcOptions.Filters` 컬렉션에 추가하여 전역적으로 필터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-174">Filters are added globally by adding it to the `MvcOptions.Filters` collection in `ConfigureServices`:</span></span>

[!code-csharp[](./filters/sample/src/FiltersSample/Startup.cs?name=snippet_ConfigureServices&highlight=5-8)]

### <a name="default-order-of-execution"></a><span data-ttu-id="a2266-175">기본 실행 순서</span><span class="sxs-lookup"><span data-stu-id="a2266-175">Default order of execution</span></span>

<span data-ttu-id="a2266-176">파이프라인의 특정 단계에 여러 개의 필터가 있는 경우 범위는 기본 필터 실행 순서를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-176">When there are multiple filters for a particular stage of the pipeline, scope determines the default order of filter execution.</span></span>  <span data-ttu-id="a2266-177">전역 필터는 메서드 필터를 둘러싼 클래스 필터를 둘러쌉니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-177">Global filters surround class filters, which in turn surround method filters.</span></span> <span data-ttu-id="a2266-178">범위가 증가할 때마다 [중첩되는 인형](https://wikipedia.org/wiki/Matryoshka_doll)처럼 이전 범위를 둘러싸게 되므로 이를 "러시아 인형"이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-178">This is sometimes referred to as "Russian doll" nesting, as each increase in scope is wrapped around the previous scope, like a [nesting doll](https://wikipedia.org/wiki/Matryoshka_doll).</span></span> <span data-ttu-id="a2266-179">일반적으로 명시적으로 순서를 결정할 필요 없이 원하는 재정의 동작을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-179">You generally get the desired overriding behavior without having to explicitly determine ordering.</span></span>

<span data-ttu-id="a2266-180">이 중첩의 결과로 필터의 *after* 코드는 *before* 코드의 역순으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-180">As a result of this nesting, the *after* code of filters runs in the reverse order of the *before* code.</span></span> <span data-ttu-id="a2266-181">시퀀스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-181">The sequence looks like this:</span></span>

* <span data-ttu-id="a2266-182">전역적으로 적용된 필터의 *before* 코드</span><span class="sxs-lookup"><span data-stu-id="a2266-182">The *before* code of filters applied globally</span></span>
  * <span data-ttu-id="a2266-183">컨트롤러에 적용된 필터의 *before* 코드</span><span class="sxs-lookup"><span data-stu-id="a2266-183">The *before* code of filters applied to controllers</span></span>
    * <span data-ttu-id="a2266-184">작업 메서드에 적용된 필터의 *before* 코드</span><span class="sxs-lookup"><span data-stu-id="a2266-184">The *before* code of filters applied to action methods</span></span>
    * <span data-ttu-id="a2266-185">작업 메서드에 적용된 필터의 *after* 코드</span><span class="sxs-lookup"><span data-stu-id="a2266-185">The *after* code of filters applied to action methods</span></span>
  * <span data-ttu-id="a2266-186">컨트롤러에 적용된 필터의 *after* 코드</span><span class="sxs-lookup"><span data-stu-id="a2266-186">The *after* code of filters applied to controllers</span></span>
* <span data-ttu-id="a2266-187">전역적으로 적용된 필터의 *after* 코드</span><span class="sxs-lookup"><span data-stu-id="a2266-187">The *after* code of filters applied globally</span></span>
  
<span data-ttu-id="a2266-188">필터 메서드가 동기 작업 필터에 대해 호출되는 순서를 보여주는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-188">Here's an example that illustrates the order in which filter methods are called for synchronous Action filters.</span></span>

| <span data-ttu-id="a2266-189">Sequence</span><span class="sxs-lookup"><span data-stu-id="a2266-189">Sequence</span></span> | <span data-ttu-id="a2266-190">필터 범위</span><span class="sxs-lookup"><span data-stu-id="a2266-190">Filter scope</span></span> | <span data-ttu-id="a2266-191">필터 메서드</span><span class="sxs-lookup"><span data-stu-id="a2266-191">Filter method</span></span> |
|:--------:|:------------:|:-------------:|
| <span data-ttu-id="a2266-192">1</span><span class="sxs-lookup"><span data-stu-id="a2266-192">1</span></span> | <span data-ttu-id="a2266-193">Global</span><span class="sxs-lookup"><span data-stu-id="a2266-193">Global</span></span> | `OnActionExecuting` |
| <span data-ttu-id="a2266-194">2</span><span class="sxs-lookup"><span data-stu-id="a2266-194">2</span></span> | <span data-ttu-id="a2266-195">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="a2266-195">Controller</span></span> | `OnActionExecuting` |
| <span data-ttu-id="a2266-196">3</span><span class="sxs-lookup"><span data-stu-id="a2266-196">3</span></span> | <span data-ttu-id="a2266-197">메서드</span><span class="sxs-lookup"><span data-stu-id="a2266-197">Method</span></span> | `OnActionExecuting` |
| <span data-ttu-id="a2266-198">4</span><span class="sxs-lookup"><span data-stu-id="a2266-198">4</span></span> | <span data-ttu-id="a2266-199">메서드</span><span class="sxs-lookup"><span data-stu-id="a2266-199">Method</span></span> | `OnActionExecuted` |
| <span data-ttu-id="a2266-200">5</span><span class="sxs-lookup"><span data-stu-id="a2266-200">5</span></span> | <span data-ttu-id="a2266-201">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="a2266-201">Controller</span></span> | `OnActionExecuted` |
| <span data-ttu-id="a2266-202">6</span><span class="sxs-lookup"><span data-stu-id="a2266-202">6</span></span> | <span data-ttu-id="a2266-203">Global</span><span class="sxs-lookup"><span data-stu-id="a2266-203">Global</span></span> | `OnActionExecuted` |

<span data-ttu-id="a2266-204">이 시퀀스는 다음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-204">This sequence shows:</span></span>

* <span data-ttu-id="a2266-205">메서드 필터는 컨트롤러 필터 내에서 중첩됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-205">The method filter is nested within the controller filter.</span></span>
* <span data-ttu-id="a2266-206">컨트롤러 필터는 전역 필터 내에서 중첩됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-206">The controller filter is nested within the global filter.</span></span> 

<span data-ttu-id="a2266-207">즉, 비동기 필터의 On*Stage*ExecutionAsync 메서드 내에 있는 경우 코드가 스택에 있는 반면 좁은 범위를 가진 모든 필터가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-207">To put it another way, if you're inside an async filter's On*Stage*ExecutionAsync method, all of the filters with a tighter scope run while your code is on the stack.</span></span>

> [!NOTE]
> <span data-ttu-id="a2266-208">`Controller` 기본 클래스에서 상속되는 모든 컨트롤러에는 `OnActionExecuting` 및 `OnActionExecuted` 메서드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-208">Every controller that inherits from the `Controller` base class includes `OnActionExecuting` and `OnActionExecuted` methods.</span></span> <span data-ttu-id="a2266-209">이러한 메서드는 지정된 작업에 대해 실행되는 필터를 래핑합니다. `OnActionExecuting`은 필터 이전에 호출되고 `OnActionExecuted`는 모든 필터 이후에 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-209">These methods wrap the filters that run for a given action:  `OnActionExecuting` is called before any of the filters, and `OnActionExecuted` is called after all of the filters.</span></span>

### <a name="overriding-the-default-order"></a><span data-ttu-id="a2266-210">기본 순서 재정의</span><span class="sxs-lookup"><span data-stu-id="a2266-210">Overriding the default order</span></span>

<span data-ttu-id="a2266-211">`IOrderedFilter`를 구현하여 실행의 기본 시퀀스를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-211">You can override the default sequence of execution by implementing `IOrderedFilter`.</span></span> <span data-ttu-id="a2266-212">이 인터페이스는 실행 순서를 결정하는 범위에 대해 우선 순위를 갖는 `Order` 속성을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-212">This interface exposes an `Order` property that takes precedence over scope to determine the order of execution.</span></span> <span data-ttu-id="a2266-213">낮은 `Order` 값을 가진 필터는 `Order`라는 큰 값을 가진 필터 이전에 해당 *before* 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-213">A filter with a lower `Order` value will have its *before* code executed before that of a filter with a higher value of `Order`.</span></span> <span data-ttu-id="a2266-214">낮은 `Order` 값을 가진 필터는 `Order`라는 큰 값을 가진 필터 이후에 해당 *after* 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-214">A filter with a lower `Order` value will have its *after* code executed after that of a filter with a higher `Order` value.</span></span> <span data-ttu-id="a2266-215">생성자 매개 변수를 사용하여 `Order` 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-215">You can set the `Order` property by using a constructor parameter:</span></span>

```csharp
[MyFilter(Name = "Controller Level Attribute", Order=1)]
```

<span data-ttu-id="a2266-216">위의 예제에 표시된 3개의 동일한 작업 필터가 있지만 컨트롤러 및 글로벌 필터의 `Order` 속성을 각각 1 및 2로 설정한 경우 실행 순서는 반대입니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-216">If you have the same 3 Action filters shown in the preceding example but set the `Order` property of the controller and global filters to 1 and 2 respectively, the order of execution would be reversed.</span></span>

| <span data-ttu-id="a2266-217">Sequence</span><span class="sxs-lookup"><span data-stu-id="a2266-217">Sequence</span></span> | <span data-ttu-id="a2266-218">필터 범위</span><span class="sxs-lookup"><span data-stu-id="a2266-218">Filter scope</span></span> | <span data-ttu-id="a2266-219">`Order` 속성</span><span class="sxs-lookup"><span data-stu-id="a2266-219">`Order` property</span></span> | <span data-ttu-id="a2266-220">필터 메서드</span><span class="sxs-lookup"><span data-stu-id="a2266-220">Filter method</span></span> |
|:--------:|:------------:|:-----------------:|:-------------:|
| <span data-ttu-id="a2266-221">1</span><span class="sxs-lookup"><span data-stu-id="a2266-221">1</span></span> | <span data-ttu-id="a2266-222">메서드</span><span class="sxs-lookup"><span data-stu-id="a2266-222">Method</span></span> | <span data-ttu-id="a2266-223">0</span><span class="sxs-lookup"><span data-stu-id="a2266-223">0</span></span> | `OnActionExecuting` |
| <span data-ttu-id="a2266-224">2</span><span class="sxs-lookup"><span data-stu-id="a2266-224">2</span></span> | <span data-ttu-id="a2266-225">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="a2266-225">Controller</span></span> | <span data-ttu-id="a2266-226">1</span><span class="sxs-lookup"><span data-stu-id="a2266-226">1</span></span>  | `OnActionExecuting` |
| <span data-ttu-id="a2266-227">3</span><span class="sxs-lookup"><span data-stu-id="a2266-227">3</span></span> | <span data-ttu-id="a2266-228">Global</span><span class="sxs-lookup"><span data-stu-id="a2266-228">Global</span></span> | <span data-ttu-id="a2266-229">2</span><span class="sxs-lookup"><span data-stu-id="a2266-229">2</span></span>  | `OnActionExecuting` |
| <span data-ttu-id="a2266-230">4</span><span class="sxs-lookup"><span data-stu-id="a2266-230">4</span></span> | <span data-ttu-id="a2266-231">Global</span><span class="sxs-lookup"><span data-stu-id="a2266-231">Global</span></span> | <span data-ttu-id="a2266-232">2</span><span class="sxs-lookup"><span data-stu-id="a2266-232">2</span></span>  | `OnActionExecuted` |
| <span data-ttu-id="a2266-233">5</span><span class="sxs-lookup"><span data-stu-id="a2266-233">5</span></span> | <span data-ttu-id="a2266-234">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="a2266-234">Controller</span></span> | <span data-ttu-id="a2266-235">1</span><span class="sxs-lookup"><span data-stu-id="a2266-235">1</span></span>  | `OnActionExecuted` |
| <span data-ttu-id="a2266-236">6</span><span class="sxs-lookup"><span data-stu-id="a2266-236">6</span></span> | <span data-ttu-id="a2266-237">메서드</span><span class="sxs-lookup"><span data-stu-id="a2266-237">Method</span></span> | <span data-ttu-id="a2266-238">0</span><span class="sxs-lookup"><span data-stu-id="a2266-238">0</span></span>  | `OnActionExecuted` |

<span data-ttu-id="a2266-239">`Order` 속성은 필터가 실행되는 순서를 결정할 때 범위를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-239">The `Order` property trumps scope when determining the order in which filters will run.</span></span> <span data-ttu-id="a2266-240">필터가 순서에 따라 먼저 정렬된 다음, 범위는 연결을 끊는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-240">Filters are sorted first by order, then scope is used to break ties.</span></span> <span data-ttu-id="a2266-241">모든 기본 제공 필터는 `IOrderedFilter`을 구현하고 기본 `Order` 값을 0으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-241">All of the built-in filters implement `IOrderedFilter` and set the default `Order` value to 0.</span></span> <span data-ttu-id="a2266-242">기본 제공 필터의 경우 `Order`를 0이 아닌 값으로 설정하지 않는 한 범위가 순서를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-242">Fir built-in filters, scope determines order unless you set `Order` to a non-zero value.</span></span>

## <a name="cancellation-and-short-circuiting"></a><span data-ttu-id="a2266-243">취소 및 단락(short-circuit)</span><span class="sxs-lookup"><span data-stu-id="a2266-243">Cancellation and short circuiting</span></span>

<span data-ttu-id="a2266-244">제공된 `context` 매개 변수의 `Result` 속성을 필터 메서드로 설정하여 언제든지 필터 파이프라인을 단락(short-circuit) 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-244">You can short-circuit the filter pipeline at any point by setting the `Result` property on the `context` parameter provided to the filter method.</span></span> <span data-ttu-id="a2266-245">예를 들어 다음과 같은 리소스 필터는 파이프라인의 나머지 부분이 실행되지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-245">For instance, the following Resource filter prevents the rest of the pipeline from executing.</span></span>

<a name="short-circuiting-resource-filter"></a>

[!code-csharp[](./filters/sample/src/FiltersSample/Filters/ShortCircuitingResourceFilterAttribute.cs?highlight=12,13,14,15)]

<span data-ttu-id="a2266-246">다음 코드에서 `ShortCircuitingResourceFilter` 및 `AddHeader` 필터는 `SomeResource` 작업 메서드를 대상으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-246">In the following code, both the `ShortCircuitingResourceFilter` and the `AddHeader` filter target the `SomeResource` action method.</span></span> <span data-ttu-id="a2266-247">`ShortCircuitingResourceFilter`:</span><span class="sxs-lookup"><span data-stu-id="a2266-247">The `ShortCircuitingResourceFilter`:</span></span>

* <span data-ttu-id="a2266-248">리소스 필터이고 `AddHeader`이 작업 필터이기 때문에 먼저 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-248">Runs first, because it's a Resource Filter and `AddHeader` is an Action Filter.</span></span>
* <span data-ttu-id="a2266-249">나머지 파이프라인을 단락(Short-circuit) 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-249">Short-circuits the rest of the pipeline.</span></span>

<span data-ttu-id="a2266-250">따라서 `AddHeader` 필터는 `SomeResource` 작업에 대해 절대 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-250">Therefore the `AddHeader` filter never runs for the `SomeResource` action.</span></span> <span data-ttu-id="a2266-251">이 동작은 작업 메서드 수준에서 두 필터를 적용한 경우에도 동일하며 먼저 실행되는 `ShortCircuitingResourceFilter`를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-251">This behavior would be the same if both filters were applied at the action method level, provided the `ShortCircuitingResourceFilter` ran first.</span></span> <span data-ttu-id="a2266-252">해당 필터 형식 또는 `Order` 속성의 명시적 사용으로 인해 `ShortCircuitingResourceFilter`이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-252">The `ShortCircuitingResourceFilter` runs first because of its filter type, or by explicit use of `Order` property.</span></span>

[!code-csharp[](./filters/sample/src/FiltersSample/Controllers/SampleController.cs?name=snippet_AddHeader&highlight=1,9)]

## <a name="dependency-injection"></a><span data-ttu-id="a2266-253">종속성 주입</span><span class="sxs-lookup"><span data-stu-id="a2266-253">Dependency injection</span></span>

<span data-ttu-id="a2266-254">형식 또는 인스턴스별로 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-254">Filters can be added by type or by instance.</span></span> <span data-ttu-id="a2266-255">인스턴스를 추가하는 경우 해당 인스턴스가 모든 요청에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-255">If you add an instance, that instance will be used for every request.</span></span> <span data-ttu-id="a2266-256">형식을 추가하면 활성화됩니다. 즉, DI([종속성 주입](../../fundamentals/dependency-injection.md))에서 각 요청에 대한 인스턴스를 만들고 모든 생성자 종속성을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-256">If you add a type, it will be type-activated, meaning an instance will be created for each request and any constructor dependencies will be populated by [dependency injection](../../fundamentals/dependency-injection.md) (DI).</span></span> <span data-ttu-id="a2266-257">형식별 필터를 추가하는 작업은 `filters.Add(new TypeFilterAttribute(typeof(MyFilter)))`에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-257">Adding a filter by type is equivalent to `filters.Add(new TypeFilterAttribute(typeof(MyFilter)))`.</span></span>

<span data-ttu-id="a2266-258">특성으로 구현되고 컨트롤러 클래스 또는 작업 메서드에 직접 추가되는 필터에는 DI([종속성 주입](../../fundamentals/dependency-injection.md))에서 제공하는 생성자 종속성이 없을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-258">Filters that are implemented as attributes and added directly to controller classes or action methods cannot have constructor dependencies provided by [dependency injection](../../fundamentals/dependency-injection.md) (DI).</span></span> <span data-ttu-id="a2266-259">특성이 적용될 때 해당 생성자 매개 변수가 제공되어야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-259">This is because attributes must have their constructor parameters supplied where they're applied.</span></span> <span data-ttu-id="a2266-260">특성이 작동하는 방법의 제한 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-260">This is a limitation of how attributes work.</span></span>

<span data-ttu-id="a2266-261">필터에 DI에서 액세스해야 하는 종속성이 있는 경우 지원되는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-261">If your filters have dependencies that you need to access from DI, there are several supported approaches.</span></span> <span data-ttu-id="a2266-262">다음 중 하나를 사용하여 클래스 또는 작업 메서드에 필터를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-262">You can apply your filter to a class or action method using one of the following:</span></span>

* `ServiceFilterAttribute`
* `TypeFilterAttribute`
* <span data-ttu-id="a2266-263">특성에서 구현된 `IFilterFactory`</span><span class="sxs-lookup"><span data-stu-id="a2266-263">`IFilterFactory` implemented on your attribute</span></span>

> [!NOTE]
> <span data-ttu-id="a2266-264">DI에서 가져오려는 하나의 종속성은 로거입니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-264">One dependency you might want to get from DI is a logger.</span></span> <span data-ttu-id="a2266-265">그러나 [기본 제공 프레임워크 로깅 기능](xref:fundamentals/logging/index)이 필요한 기능을 이미 제공할 수 있으므로 로깅 용도로 필터를 만들고 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-265">However, avoid creating and using filters purely for logging purposes, since the [built-in framework logging features](xref:fundamentals/logging/index) may already provide what you need.</span></span> <span data-ttu-id="a2266-266">필터에 로깅을 추가하려는 경우 MVC 작업 또는 다른 프레임워크 이벤트보다 비즈니스 도메인 문제 또는 필터에 특정된 동작에 집중해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-266">If you're going to add logging to your filters, it should focus on business domain concerns or behavior specific to your filter, rather than MVC actions or other framework events.</span></span>

### <a name="servicefilterattribute"></a><span data-ttu-id="a2266-267">ServiceFilterAttribute</span><span class="sxs-lookup"><span data-stu-id="a2266-267">ServiceFilterAttribute</span></span>

<span data-ttu-id="a2266-268">`ServiceFilter`는 DI에서 필터의 인스턴스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-268">A `ServiceFilter` retrieves an instance of the filter from DI.</span></span> <span data-ttu-id="a2266-269">필터를 `ConfigureServices`의 컨테이너에 추가하고, `ServiceFilter` 특성에서 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-269">You add the filter to the container in `ConfigureServices`, and reference it in a `ServiceFilter` attribute</span></span>

[!code-csharp[](./filters/sample/src/FiltersSample/Startup.cs?name=snippet_ConfigureServices&highlight=11)]

[!code-csharp[](../../mvc/controllers/filters/sample/src/FiltersSample/Controllers/HomeController.cs?name=snippet_ServiceFilter&highlight=1)]

<span data-ttu-id="a2266-270">필터 형식을 등록하지 않고 `ServiceFilter`를 사용하여 예외를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-270">Using `ServiceFilter` without registering the filter type results in an exception:</span></span>

```
System.InvalidOperationException: No service for type
'FiltersSample.Filters.AddHeaderFilterWithDI' has been registered.
```

<span data-ttu-id="a2266-271">`ServiceFilterAttribute`는 `IFilterFactory`를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-271">`ServiceFilterAttribute` implements `IFilterFactory`.</span></span> <span data-ttu-id="a2266-272">`IFilterFactory`은 `IFilter` 인스턴스를 만들기 위해 `CreateInstance` 메서드를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-272">`IFilterFactory` exposes the `CreateInstance` method for creating an `IFilter` instance.</span></span> <span data-ttu-id="a2266-273">`CreateInstance` 메서드는 서비스 컨테이너(DI)에서 지정된 형식을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-273">The `CreateInstance` method loads the specified type from the services container (DI).</span></span>

### <a name="typefilterattribute"></a><span data-ttu-id="a2266-274">TypeFilterAttribute</span><span class="sxs-lookup"><span data-stu-id="a2266-274">TypeFilterAttribute</span></span>

<span data-ttu-id="a2266-275">`TypeFilterAttribute`는 `ServiceFilterAttribute`와 비슷하지만 해당 형식은 DI 컨테이너에서 직접 확인되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-275">`TypeFilterAttribute` is similar to `ServiceFilterAttribute`, but its type isn't resolved directly from the DI container.</span></span> <span data-ttu-id="a2266-276">`Microsoft.Extensions.DependencyInjection.ObjectFactory`를 사용하여 형식을 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-276">It instantiates the type by using `Microsoft.Extensions.DependencyInjection.ObjectFactory`.</span></span>

<span data-ttu-id="a2266-277">이 차이 때문에:</span><span class="sxs-lookup"><span data-stu-id="a2266-277">Because of this difference:</span></span>

* <span data-ttu-id="a2266-278">`TypeFilterAttribute`을 사용하여 참조되는 형식은 먼저 컨테이너를 사용하여 등록할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-278">Types that are referenced using the `TypeFilterAttribute` don't need to be registered with the container first.</span></span>  <span data-ttu-id="a2266-279">컨테이너에서 충족하는 종속성을 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-279">They do have their dependencies fulfilled by the container.</span></span> 
* <span data-ttu-id="a2266-280">`TypeFilterAttribute`는 형식에 대한 생성자 인수를 필요에 따라 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-280">`TypeFilterAttribute` can optionally accept constructor arguments for the type.</span></span> 

<span data-ttu-id="a2266-281">다음 예제에서는 `TypeFilterAttribute`를 사용하여 인수를 형식에 전달하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-281">The following example demonstrates how to pass arguments to a type using `TypeFilterAttribute`:</span></span>

[!code-csharp[](../../mvc/controllers/filters/sample/src/FiltersSample/Controllers/HomeController.cs?name=snippet_TypeFilter&highlight=1,2)]

<span data-ttu-id="a2266-282">다음과 같은 필터가 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="a2266-282">If you have a filter that:</span></span>

* <span data-ttu-id="a2266-283">인수가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-283">Doesn't require any arguments.</span></span>
* <span data-ttu-id="a2266-284">DI에서 채워야 할 생성자 종속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-284">Has constructor dependencies that need to be filled by DI.</span></span>

<span data-ttu-id="a2266-285">`[TypeFilter(typeof(FilterType))]` 대신에 클래스 및 메서드에 대한 자신의 명명된 특성을 사용할 수 있습니다).</span><span class="sxs-lookup"><span data-stu-id="a2266-285">You can use your own named attribute on classes and methods instead of `[TypeFilter(typeof(FilterType))]`).</span></span> <span data-ttu-id="a2266-286">다음 필터에서는 이를 구현하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-286">The following filter shows how this can be implemented:</span></span>

[!code-csharp[](./filters/sample/src/FiltersSample/Filters/SampleActionFilterAttribute.cs?name=snippet_TypeFilterAttribute&highlight=1,3,7)]

<span data-ttu-id="a2266-287">이 필터는 `[TypeFilter]` 또는 `[ServiceFilter]`를 사용하는 대신 `[SampleActionFilter]` 구문을 사용하여 클래스 또는 메서드에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-287">This filter can be applied to classes or methods using the `[SampleActionFilter]` syntax, instead of having to use `[TypeFilter]` or `[ServiceFilter]`.</span></span>

## <a name="authorization-filters"></a><span data-ttu-id="a2266-288">권한 부여 필터</span><span class="sxs-lookup"><span data-stu-id="a2266-288">Authorization filters</span></span>

<span data-ttu-id="a2266-289">\*권한 부여 필터:</span><span class="sxs-lookup"><span data-stu-id="a2266-289">\*Authorization filters:</span></span>
* <span data-ttu-id="a2266-290">동작 메서드에 대한 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-290">Control access to action methods.</span></span>
* <span data-ttu-id="a2266-291">필터 파이프라인 내에서 실행되어야 할 첫 번째 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-291">Are the first filters to be executed within the filter pipeline.</span></span> 
* <span data-ttu-id="a2266-292">before 메서드는 있지만 after 메서드는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-292">Have a before method, but no after method.</span></span> 

<span data-ttu-id="a2266-293">고유한 권한 부여 프레임워크를 작성하는 경우에만 사용자 지정 권한 부여 필터를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-293">You should only write a custom authorization filter if you are writing your own authorization framework.</span></span> <span data-ttu-id="a2266-294">사용자 지정 필터를 작성하는 대신 권한 부여 정책을 구성하거나 사용자 지정 권한 부여 정책을 작성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-294">Prefer configuring your authorization policies or writing a custom authorization policy over writing a custom filter.</span></span> <span data-ttu-id="a2266-295">기본 제공 필터 구현은 권한 부여 시스템을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-295">The built-in filter implementation is just responsible for calling the authorization system.</span></span>

<span data-ttu-id="a2266-296">무엇도 예외를 처리하지 않으므로 권한 부여 필터 내에서 예외를 throw해서는 안됩니다(예외 필터는 처리하지 않음).</span><span class="sxs-lookup"><span data-stu-id="a2266-296">You shouldn't throw exceptions within authorization filters, since nothing will handle the exception (exception filters won't handle them).</span></span> <span data-ttu-id="a2266-297">예외가 발생할 경우 과제 실행을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-297">Consider issuing a challenge when an exception occurs.</span></span>

<span data-ttu-id="a2266-298">[권한 부여](../../security/authorization/index.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-298">Learn more about [Authorization](../../security/authorization/index.md).</span></span>

## <a name="resource-filters"></a><span data-ttu-id="a2266-299">리소스 필터</span><span class="sxs-lookup"><span data-stu-id="a2266-299">Resource filters</span></span>

* <span data-ttu-id="a2266-300">`IResourceFilter` 또는 `IAsyncResourceFilter` 인터페이스 중 하나를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-300">Implement either the `IResourceFilter` or `IAsyncResourceFilter` interface,</span></span>
* <span data-ttu-id="a2266-301">해당 실행은 필터 파이프라인 대부분을 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-301">Their execution wraps most of the filter pipeline.</span></span> 
* <span data-ttu-id="a2266-302">[권한 부여 필터](#authorization-filters)만 리소스 필터 전에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-302">Only [Authorization filters](#authorization-filters) run before Resource filters.</span></span>

<span data-ttu-id="a2266-303">리소스 필터는 요청을 수행하는 대부분의 작업을 단락(short-circuit) 처리해야 하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-303">Resource filters are useful to short-circuit most of the work a request is doing.</span></span> <span data-ttu-id="a2266-304">예를 들어 응답이 캐시에 있는 경우 캐싱 필터는 파이프라인의 나머지 부분을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-304">For example, a caching filter can avoid the rest of the pipeline if the response is in the cache.</span></span>

<span data-ttu-id="a2266-305">앞에서 살펴본 [단락(short-circuit) 리소스 필터](#short-circuiting-resource-filter)는 리소스 필터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-305">The [short circuiting resource filter](#short-circuiting-resource-filter) shown earlier is one example of a resource filter.</span></span> <span data-ttu-id="a2266-306">다른 예는 [DisableFormValueModelBindingAttribute](https://github.com/aspnet/Entropy/blob/rel/1.1.1/samples/Mvc.FileUpload/Filters/DisableFormValueModelBindingAttribute.cs)입니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-306">Another example is [DisableFormValueModelBindingAttribute](https://github.com/aspnet/Entropy/blob/rel/1.1.1/samples/Mvc.FileUpload/Filters/DisableFormValueModelBindingAttribute.cs):</span></span>

* <span data-ttu-id="a2266-307">모델 바인딩이 양식 데이터에 액세스하는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-307">It prevents model binding from accessing the form data.</span></span> 
* <span data-ttu-id="a2266-308">대형 파일 업로드에 유용하며 형식이 메모리로 읽히는 것을 방지하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-308">It's useful for large file uploads and want to prevent the form from being read into memory.</span></span>

## <a name="action-filters"></a><span data-ttu-id="a2266-309">작업 필터</span><span class="sxs-lookup"><span data-stu-id="a2266-309">Action filters</span></span>

<span data-ttu-id="a2266-310">*작업 필터*:</span><span class="sxs-lookup"><span data-stu-id="a2266-310">*Action filters*:</span></span>

* <span data-ttu-id="a2266-311">`IActionFilter` 또는 `IAsyncActionFilter` 인터페이스 중 하나를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-311">Implement either the `IActionFilter` or `IAsyncActionFilter` interface.</span></span>
* <span data-ttu-id="a2266-312">해당 실행은 작업 메서드의 실행을 둘러쌉니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-312">Their execution surrounds the execution of action methods.</span></span>

<span data-ttu-id="a2266-313">샘플 작업 필터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-313">Here's a sample action filter:</span></span>

[!code-csharp[](./filters/sample/src/FiltersSample/Filters/SampleActionFilter.cs?name=snippet_ActionFilter)]

<span data-ttu-id="a2266-314">[ActionExecutingContext](/dotnet/api/microsoft.aspnetcore.mvc.filters.actionexecutingcontext)는 다음과 같은 속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-314">The [ActionExecutingContext](/dotnet/api/microsoft.aspnetcore.mvc.filters.actionexecutingcontext) provides the following properties:</span></span>

* <span data-ttu-id="a2266-315">`ActionArguments` - 작업에 대한 입력을 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-315">`ActionArguments` - lets you manipulate the inputs to the action.</span></span>
* <span data-ttu-id="a2266-316">`Controller` - 컨트롤러 인스턴스를 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-316">`Controller` - lets you manipulate the controller instance.</span></span> 
* <span data-ttu-id="a2266-317">`Result` - 작업 메서드 및 후속 작업 필터의 단락(short-circuit) 실행을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-317">`Result` - setting this short-circuits execution of the action method and subsequent action filters.</span></span> <span data-ttu-id="a2266-318">또한 예외를 throw하면 작업 메서드 및 후속 필터의 실행을 방지하지만 성공적인 결과가 아닌 실패로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-318">Throwing an exception also prevents execution of the action method and subsequent filters, but is treated as a failure instead of a successful result.</span></span>

<span data-ttu-id="a2266-319">[ActionExecutedContext](/dotnet/api/microsoft.aspnetcore.mvc.filters.actionexecutedcontext)는 `Controller`과 `Result` 및 다음과 같은 속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-319">The [ActionExecutedContext](/dotnet/api/microsoft.aspnetcore.mvc.filters.actionexecutedcontext) provides `Controller` and `Result` plus the following properties:</span></span>

* <span data-ttu-id="a2266-320">`Canceled` - 작업 실행이 다른 필터에 의해 단락(short-circuit) 처리된 경우 true입니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-320">`Canceled` - will be true if the action execution was short-circuited by another filter.</span></span>
* <span data-ttu-id="a2266-321">`Exception` - 작업 또는 후속 작업 필터에서 예외가 throw된 경우 null이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-321">`Exception` - will be non-null if the action or a subsequent action filter threw an exception.</span></span> <span data-ttu-id="a2266-322">이 속성을 효과적으로 null로 설정하면 예외를 '처리'하고 `Result`이 정상적으로 작업 메서드에서 반환된 것처럼 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-322">Setting this property to null effectively 'handles' an exception, and `Result` will be executed as if it were returned from the action method normally.</span></span>

<span data-ttu-id="a2266-323">`IAsyncActionFilter`의 경우 `ActionExecutionDelegate`에 대한 호출:</span><span class="sxs-lookup"><span data-stu-id="a2266-323">For an `IAsyncActionFilter`, a call to the `ActionExecutionDelegate`:</span></span>

* <span data-ttu-id="a2266-324">후속 작업 필터 및 작업 메서드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-324">Executes any subsequent action filters and the action method.</span></span>
* <span data-ttu-id="a2266-325">`ActionExecutedContext`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-325">returns `ActionExecutedContext`.</span></span> 

<span data-ttu-id="a2266-326">단락(short-circuit) 처리하려면 `ActionExecutingContext.Result`을 일부 결과 인스턴스에 를 할당하고 `ActionExecutionDelegate`를 호출하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-326">To short-circuit, assign `ActionExecutingContext.Result` to some result instance and don't call the `ActionExecutionDelegate`.</span></span>

<span data-ttu-id="a2266-327">프레임워크는 하위 클래스를 지정할 수 있는 추상 `ActionFilterAttribute`을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-327">The framework provides an abstract `ActionFilterAttribute` that you can subclass.</span></span> 

<span data-ttu-id="a2266-328">작업 필터를 사용하여 모델 상태를 확인하고 상태가 잘못된 경우 오류를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-328">You can use an action filter to validate model state and return any errors if the state is invalid:</span></span>

[!code-csharp[](./filters/sample/src/FiltersSample/Filters/ValidateModelAttribute.cs)]

<span data-ttu-id="a2266-329">`OnActionExecuted` 메서드는 작업 메서드 이후에 실행되고 `ActionExecutedContext.Result` 속성을 통해 작업의 결과를 확인하고 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-329">The `OnActionExecuted` method runs after the action method and can see and manipulate the results of the action through the `ActionExecutedContext.Result` property.</span></span> <span data-ttu-id="a2266-330">`ActionExecutedContext.Canceled`는 작업 실행이 다른 필터에 의해 단락(short-circuit) 처리된 경우 true로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-330">`ActionExecutedContext.Canceled` will be set to true if the action execution was short-circuited by another filter.</span></span> <span data-ttu-id="a2266-331">`ActionExecutedContext.Exception`은 작업 또는 후속 작업 필터에서 예외가 throw된 경우 null이 아닌 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-331">`ActionExecutedContext.Exception` will be set to a non-null value if the action or a subsequent action filter threw an exception.</span></span> <span data-ttu-id="a2266-332">`ActionExecutedContext.Exception`을 Null로 설정:</span><span class="sxs-lookup"><span data-stu-id="a2266-332">Setting `ActionExecutedContext.Exception` to null:</span></span>

* <span data-ttu-id="a2266-333">예외를 효과적으로 ‘처리’합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-333">Effectively 'handles' an exception.</span></span>
* <span data-ttu-id="a2266-334">`ActionExectedContext.Result`은 작업 메서드에서 정상적으로 반환되는 것처럼 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-334">`ActionExectedContext.Result` is executed as if it were returned normally from the action method.</span></span>

## <a name="exception-filters"></a><span data-ttu-id="a2266-335">예외 필터</span><span class="sxs-lookup"><span data-stu-id="a2266-335">Exception filters</span></span>

<span data-ttu-id="a2266-336">*예외 필터*는 `IExceptionFilter` 또는 `IAsyncExceptionFilter` 인터페이스 중 하나를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-336">*Exception filters* implement either the `IExceptionFilter` or `IAsyncExceptionFilter` interface.</span></span> <span data-ttu-id="a2266-337">앱에서 일반적인 오류 처리 정책을 구현하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-337">They can be used to implement common error handling policies for an app.</span></span> 

<span data-ttu-id="a2266-338">다음 샘플 예외 필터는 사용자 지정 개발자 오류 보기를 사용하여 앱을 개발 중인 경우에 발생하는 예외에 대한 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-338">The following sample exception filter uses a custom developer error view to display details about exceptions that occur when the app is in development:</span></span>

[!code-csharp[](./filters/sample/src/FiltersSample/Filters/CustomExceptionFilterAttribute.cs?name=snippet_ExceptionFilter&highlight=1,14)]

<span data-ttu-id="a2266-339">예외 필터:</span><span class="sxs-lookup"><span data-stu-id="a2266-339">Exception filters:</span></span>

* <span data-ttu-id="a2266-340">before 및 after 이벤트는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-340">Don't have before and after events.</span></span> 
* <span data-ttu-id="a2266-341">`OnException` 또는 `OnExceptionAsync`를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-341">Implement `OnException` or `OnExceptionAsync`.</span></span> 
* <span data-ttu-id="a2266-342">컨트롤러 생성, [모델 바인딩](../models/model-binding.md), 작업 필터 또는 작업 메서드에서 발생하는 처리되지 않은 예외를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-342">Handle unhandled exceptions that occur in controller creation, [model binding](../models/model-binding.md), action filters, or action methods.</span></span> 
* <span data-ttu-id="a2266-343">리소스 필터, 결과 필터 또는 MVC 결과 실행에서 발생하는 예외를 catch하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-343">Do not catch exceptions that occur in Resource filters, Result filters, or MVC Result execution.</span></span>

<span data-ttu-id="a2266-344">예외를 처리하려면 `ExceptionContext.ExceptionHandled` 속성을 true로 설정하거나 응답을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-344">To handle an exception, set the `ExceptionContext.ExceptionHandled` property to true or write a response.</span></span> <span data-ttu-id="a2266-345">그러면 예외가 전파되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-345">This stops propagation of the exception.</span></span> <span data-ttu-id="a2266-346">예외 필터는 예외를 "성공"으로 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-346">An Exception filter can't turn an exception into a "success".</span></span> <span data-ttu-id="a2266-347">작업 필터에서만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-347">Only an Action filter can do that.</span></span>

> [!NOTE]
> <span data-ttu-id="a2266-348">ASP.NET Core 1.1에서 `ExceptionHandled`을 true로 설정**하고** 응답을 작성하는 경우 응답이 전송되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-348">In ASP.NET Core 1.1, the response isn't sent if you set `ExceptionHandled` to true **and** write a response.</span></span> <span data-ttu-id="a2266-349">이 시나리오에서 ASP.NET Core 1.0은 응답을 전송하고 ASP.NET Core 1.1.2는 1.0 동작에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-349">In that scenario, ASP.NET Core 1.0 does send the response, and ASP.NET Core 1.1.2 will return to the 1.0 behavior.</span></span> <span data-ttu-id="a2266-350">자세한 내용은 GitHub 리포지토리에서 [문제 #5594](https://github.com/aspnet/Mvc/issues/5594)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a2266-350">For more information, see [issue #5594](https://github.com/aspnet/Mvc/issues/5594) in the GitHub repository.</span></span> 

<span data-ttu-id="a2266-351">예외 필터:</span><span class="sxs-lookup"><span data-stu-id="a2266-351">Exception filters:</span></span>

* <span data-ttu-id="a2266-352">MVC 작업 내에서 발생하는 트래핑 예외에 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-352">Are good for trapping exceptions that occur within MVC actions.</span></span>
* <span data-ttu-id="a2266-353">오류 처리 미들웨어만큼 유연하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-353">Are not as flexible as error handling middleware.</span></span> 

<span data-ttu-id="a2266-354">예외 처리의 경우 미들웨어를 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-354">Prefer middleware for exception handling.</span></span> <span data-ttu-id="a2266-355">선택한 MVC 작업에 따라 오류 처리를 *다르게* 수행해야 하는 경우에만 예외 필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-355">Use exception filters only where you need to do error handling *differently* based on which MVC action was chosen.</span></span> <span data-ttu-id="a2266-356">예를 들어 앱에는 API 끝점 및 보기/HTML 모두에 대한 작업 메서드가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-356">For example, your app might have action methods for both API endpoints and for views/HTML.</span></span> <span data-ttu-id="a2266-357">API 끝점은 JSON으로 오류 정보를 반환할 수 있습니다. 반면 보기 기반 작업은 HTML로 오류 페이지를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-357">The API endpoints could return error information as JSON, while the view-based actions could return an error page as HTML.</span></span>

<span data-ttu-id="a2266-358">`ExceptionFilterAttribute`을 서브클래스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-358">The `ExceptionFilterAttribute` can be subclassed.</span></span> 

## <a name="result-filters"></a><span data-ttu-id="a2266-359">결과 필터</span><span class="sxs-lookup"><span data-stu-id="a2266-359">Result filters</span></span>

* <span data-ttu-id="a2266-360">`IResultFilter` 또는 `IAsyncResultFilter` 인터페이스 중 하나를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-360">Implement either the `IResultFilter` or `IAsyncResultFilter` interface.</span></span>
* <span data-ttu-id="a2266-361">해당 실행은 작업 결과의 실행을 둘러쌉니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-361">Their execution surrounds the execution of action results.</span></span> 

<span data-ttu-id="a2266-362">HTTP 헤더를 추가하는 결과 필터의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-362">Here's an example of a Result filter that adds an HTTP header.</span></span>

[!code-csharp[](./filters/sample/src/FiltersSample/Filters/LoggingAddHeaderFilter.cs?name=snippet_ResultFilter)]

<span data-ttu-id="a2266-363">실행되는 결과의 종류는 문제가 되는 작업에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-363">The kind of result being executed depends on the action in question.</span></span> <span data-ttu-id="a2266-364">보기를 반환하는 MVC 작업에는 실행되는 `ViewResult`의 일부인 모든 Razor 프로세스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-364">An MVC action returning a view would include all razor processing as part of the `ViewResult` being executed.</span></span> <span data-ttu-id="a2266-365">API 메서드는 실행 결과의 일부로 일부 serialization을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-365">An API method might perform some serialization as part of the execution of the result.</span></span> <span data-ttu-id="a2266-366">[작업 결과](actions.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="a2266-366">Learn more about [action results](actions.md)</span></span>

<span data-ttu-id="a2266-367">결과 필터는 작업 또는 작업 필터가 작업 결과 생성하는 성공적인 결과에 대해서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-367">Result filters are only executed for successful results - when the action or action filters produce an action result.</span></span> <span data-ttu-id="a2266-368">예외 필터가 예외를 처리하는 경우 결과 필터는 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-368">Result filters are not executed when exception filters handle an exception.</span></span>

<span data-ttu-id="a2266-369">`OnResultExecuting` 메서드는 `ResultExecutingContext.Cancel`를 true로 설정하여 작업 결과 및 후속 결과 필터를 단락(short-circuit) 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-369">The `OnResultExecuting` method can short-circuit execution of the action result and subsequent result filters by setting `ResultExecutingContext.Cancel` to true.</span></span> <span data-ttu-id="a2266-370">일반적으로 빈 응답을 생성하지 않도록 단락(short-circuit) 처리하는 경우 응답 개체에 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-370">You should generally write to the response object when short-circuiting to avoid generating an empty response.</span></span> <span data-ttu-id="a2266-371">예외를 throw하면:</span><span class="sxs-lookup"><span data-stu-id="a2266-371">Throwing an exception will:</span></span>

* <span data-ttu-id="a2266-372">작업 결과 및 후속 필터의 실행을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-372">Prevent execution of the action result and subsequent filters.</span></span>
* <span data-ttu-id="a2266-373">성공적인 결과 대신 실패로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-373">Be treated as a failure instead of a successful result.</span></span>

<span data-ttu-id="a2266-374">`OnResultExecuted` 메서드를 실행하는 경우 응답은 클라이언트에 전송되고 추가로 변경될 수 없습니다(예외가 throw되지 않는 경우).</span><span class="sxs-lookup"><span data-stu-id="a2266-374">When the `OnResultExecuted` method runs, the response has likely been sent to the client and cannot be changed further (unless an exception was thrown).</span></span> <span data-ttu-id="a2266-375">`ResultExecutedContext.Canceled`는 작업 결과 실행이 다른 필터에 의해 단락(short-circuit) 처리된 경우 true로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-375">`ResultExecutedContext.Canceled` will be set to true if the action result execution was short-circuited by another filter.</span></span>

<span data-ttu-id="a2266-376">`ResultExecutedContext.Exception`은 작업 결과 또는 후속 결과 필터에서 예외가 throw된 경우 null이 아닌 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-376">`ResultExecutedContext.Exception` will be set to a non-null value if the action result or a subsequent result filter threw an exception.</span></span> <span data-ttu-id="a2266-377">`Exception`을 효과적으로 null로 설정하면 예외를 '처리'하고 예외가 파이프라인의 뒷부분에 나오는 MVC 에 의해 다시 throw되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-377">Setting `Exception` to null effectively 'handles' an exception and prevents the exception from being rethrown by MVC later in the pipeline.</span></span> <span data-ttu-id="a2266-378">결과 필터에서 예외를 처리하는 경우 응답에 모든 데이터를 쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-378">When you're handling an exception in a result filter, you might not be able to write any data to the response.</span></span> <span data-ttu-id="a2266-379">작업 결과가 해당 실행을 통해 일부 throw되고 헤더가 이미 클라이언트에 플러시된 경우 오류 코드를 전송하는 신뢰할 수 있는 메커니즘이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-379">If the action result throws partway through its execution, and the headers have already been flushed to the client, there's no reliable mechanism to send a failure code.</span></span>

<span data-ttu-id="a2266-380">`IAsyncResultFilter`의 경우 `ResultExecutionDelegate`에서 `await next`에 대한 호출은 후속 결과 필터 및 작업 결과를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-380">For an `IAsyncResultFilter` a call to `await next` on the `ResultExecutionDelegate` executes any subsequent result filters and the action result.</span></span> <span data-ttu-id="a2266-381">단락(short-circuit) 처리하려면 `ResultExecutingContext.Cancel`를 true로 설정하고 `ResultExectionDelegate`를 호출하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-381">To short-circuit, set `ResultExecutingContext.Cancel` to true and don't call the `ResultExectionDelegate`.</span></span>

<span data-ttu-id="a2266-382">프레임워크는 하위 클래스를 지정할 수 있는 추상 `ResultFilterAttribute`을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-382">The framework provides an abstract `ResultFilterAttribute` that you can subclass.</span></span> <span data-ttu-id="a2266-383">앞에 표시된 [AddHeaderAttribute](#add-header-attribute) 클래스는 결과 필터 특성의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-383">The [AddHeaderAttribute](#add-header-attribute) class shown earlier is an example of a result filter attribute.</span></span>

## <a name="using-middleware-in-the-filter-pipeline"></a><span data-ttu-id="a2266-384">필터 파이프라인에서 미들웨어 사용</span><span class="sxs-lookup"><span data-stu-id="a2266-384">Using middleware in the filter pipeline</span></span>

<span data-ttu-id="a2266-385">리소스 필터는 파이프라인의 뒷부분에 제공되는 모든 실행을 둘러싼다는 점에서 [미들웨어](xref:fundamentals/middleware/index)처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-385">Resource filters work like [middleware](xref:fundamentals/middleware/index) in that they surround the execution of everything that comes later in the pipeline.</span></span> <span data-ttu-id="a2266-386">하지만 필터는 MVC의 일부라는 점에서 미들웨어와 다릅니다. 즉, MVC 컨텍스트 및 구문에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-386">But filters differ from middleware in that they're part of MVC, which means that they have access to MVC context and constructs.</span></span>

<span data-ttu-id="a2266-387">ASP.NET Core 1.1에서 필터 파이프라인에 미들웨어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-387">In ASP.NET Core 1.1, you can use middleware in the filter pipeline.</span></span> <span data-ttu-id="a2266-388">MVC 경로 데이터에 액세스해야 하는 미들웨어 구성 요소 또는 특정 컨트롤러 또는 작업에서만 실행해야 하는 미들웨어 구성 요소가 있는 경우 해당 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-388">You might want to do that if you have a middleware component that needs access to MVC route data, or one that should run only for certain controllers or actions.</span></span>

<span data-ttu-id="a2266-389">미들웨어를 필터로 사용하려면 필터 파이프라인에 삽입하려고 하는 미들웨어를 지정하는 `Configure` 메서드를 포함한 형식을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-389">To use middleware as a filter, create a type with a `Configure` method that specifies the middleware that you want to inject into the filter pipeline.</span></span> <span data-ttu-id="a2266-390">요청에서 현재 문화권을 설정하는 지역화 미들웨어를 사용하는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-390">Here's an example that uses the localization middleware to establish the current culture for a request:</span></span>

[!code-csharp[](./filters/sample/src/FiltersSample/Filters/LocalizationPipeline.cs?name=snippet_MiddlewareFilter&highlight=3,21)]

<span data-ttu-id="a2266-391">`MiddlewareFilterAttribute`을 사용하여 선택한 컨트롤러나 작업에서 또는 전역적으로 미들웨어를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-391">You can then use the `MiddlewareFilterAttribute` to run the middleware for a selected controller or action or globally:</span></span>

[!code-csharp[](./filters/sample/src/FiltersSample/Controllers/HomeController.cs?name=snippet_MiddlewareFilter&highlight=2)]

<span data-ttu-id="a2266-392">미들웨어 필터는 모델 바인딩 이전 및 나머지 파이프라인 이후에 리소스 필터와 동일한 필터 파이프라인 단계에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-392">Middleware filters run at the same stage of the filter pipeline as Resource filters, before model binding and after the rest of the pipeline.</span></span>

## <a name="next-actions"></a><span data-ttu-id="a2266-393">다음 작업</span><span class="sxs-lookup"><span data-stu-id="a2266-393">Next actions</span></span>

<span data-ttu-id="a2266-394">필터를 실험하려면 [샘플을 다운로드하고, 테스트하고, 수정](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/filters/sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2266-394">To experiment with filters, [download, test and modify the sample](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/filters/sample).</span></span>
