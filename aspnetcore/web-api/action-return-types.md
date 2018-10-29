---
title: ASP.NET Core Web API에서 컨트롤러 작업 반환 형식
author: scottaddie
description: ASP.NET Core Web API에서 다양한 컨트롤러 작업 메서드 반환 형식을 사용하는 방법을 알아봅니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 07/23/2018
uid: web-api/action-return-types
ms.openlocfilehash: 84300eae4271c3ee4387be022c3576dc83e144eb
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207526"
---
# <a name="controller-action-return-types-in-aspnet-core-web-api"></a><span data-ttu-id="2ab1c-103">ASP.NET Core Web API에서 컨트롤러 작업 반환 형식</span><span class="sxs-lookup"><span data-stu-id="2ab1c-103">Controller action return types in ASP.NET Core Web API</span></span>

<span data-ttu-id="2ab1c-104">작성자: [Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="2ab1c-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="2ab1c-105">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/action-return-types/samples)([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="2ab1c-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/action-return-types/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="2ab1c-106">ASP.NET Core에서는 Web API 컨트롤러 작업 반환 형식에 다음 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-106">ASP.NET Core offers the following options for Web API controller action return types:</span></span>

::: moniker range=">= aspnetcore-2.1"

* [<span data-ttu-id="2ab1c-107">특정 형식</span><span class="sxs-lookup"><span data-stu-id="2ab1c-107">Specific type</span></span>](#specific-type)
* [<span data-ttu-id="2ab1c-108">IActionResult</span><span class="sxs-lookup"><span data-stu-id="2ab1c-108">IActionResult</span></span>](#iactionresult-type)
* [<span data-ttu-id="2ab1c-109">ActionResult\<T></span><span class="sxs-lookup"><span data-stu-id="2ab1c-109">ActionResult\<T></span></span>](#actionresultt-type)

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

* [<span data-ttu-id="2ab1c-110">특정 형식</span><span class="sxs-lookup"><span data-stu-id="2ab1c-110">Specific type</span></span>](#specific-type)
* [<span data-ttu-id="2ab1c-111">IActionResult</span><span class="sxs-lookup"><span data-stu-id="2ab1c-111">IActionResult</span></span>](#iactionresult-type)

::: moniker-end

<span data-ttu-id="2ab1c-112">이 문서에서는 각 반환 형식을 사용하는 것이 가장 적합한 경우를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-112">This document explains when it's most appropriate to use each return type.</span></span>

## <a name="specific-type"></a><span data-ttu-id="2ab1c-113">특정 형식</span><span class="sxs-lookup"><span data-stu-id="2ab1c-113">Specific type</span></span>

<span data-ttu-id="2ab1c-114">가장 간단한 작업은 기본 또는 복합 데이터 형식을 반환합니다(예: `string` 또는 사용자 지정 개체 형식).</span><span class="sxs-lookup"><span data-stu-id="2ab1c-114">The simplest action returns a primitive or complex data type (for example, `string` or a custom object type).</span></span> <span data-ttu-id="2ab1c-115">다음 작업을 사용하여 사용자 지정 `Product` 개체의 컬렉션을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-115">Consider the following action, which returns a collection of custom `Product` objects:</span></span>

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_Get)]

<span data-ttu-id="2ab1c-116">작업 실행 중에 보호할 알려진 조건 없이 특정 형식을 반환하는 것으로 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-116">Without known conditions to safeguard against during action execution, returning a specific type could suffice.</span></span> <span data-ttu-id="2ab1c-117">매개 변수 제약 조건 유효성 검사가 필요하지 않으므로 위의 작업은 매개 변수를 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-117">The preceding action accepts no parameters, so parameter constraints validation isn't needed.</span></span>

<span data-ttu-id="2ab1c-118">알려진 조건이 작업에서 고려되지 않으면 여러 반환 경로가 도입됩니다’.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-118">When known conditions need to be accounted for in an action, multiple return paths are introduced.</span></span> <span data-ttu-id="2ab1c-119">이 경우에 기본 또는 복합적인 반환 형식의 [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) 반환 형식을 혼합하는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-119">In such a case, it's common to mix an [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) return type with the primitive or complex return type.</span></span> <span data-ttu-id="2ab1c-120">이 종류의 동작을 수용하기 위해 [IActionResult](#iactionresult-type) 또는 [ActionResult\<T>](#actionresultt-type) 중 하나가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-120">Either [IActionResult](#iactionresult-type) or [ActionResult\<T>](#actionresultt-type) are necessary to accommodate this type of action.</span></span>

## <a name="iactionresult-type"></a><span data-ttu-id="2ab1c-121">IActionResult 형식</span><span class="sxs-lookup"><span data-stu-id="2ab1c-121">IActionResult type</span></span>

<span data-ttu-id="2ab1c-122">여러 [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) 반환 형식을 동작에서 사용할 수 있는 경우 [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult) 반환 형식이 적절합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-122">The [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult) return type is appropriate when multiple [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) return types are possible in an action.</span></span> <span data-ttu-id="2ab1c-123">`ActionResult` 형식은 다양한 HTTP 상태 코드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-123">The `ActionResult` types represent various HTTP status codes.</span></span> <span data-ttu-id="2ab1c-124">이 범주에 속하는 몇 가지 일반적인 반환 형식은 [BadRequestResult](/dotnet/api/microsoft.aspnetcore.mvc.badrequestresult)(400), [NotFoundResult](/dotnet/api/microsoft.aspnetcore.mvc.notfoundresult)(404) 및 [OkObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.okobjectresult)(200)입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-124">Some common return types falling into this category are [BadRequestResult](/dotnet/api/microsoft.aspnetcore.mvc.badrequestresult) (400), [NotFoundResult](/dotnet/api/microsoft.aspnetcore.mvc.notfoundresult) (404), and [OkObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.okobjectresult) (200).</span></span>

<span data-ttu-id="2ab1c-125">작업에서 자유롭게 여러 반환 형식 및 경로가 있기 때문에 [[ProducesResponseType]](/dotnet/api/microsoft.aspnetcore.mvc.producesresponsetypeattribute.-ctor) 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-125">Because there are multiple return types and paths in the action, liberal use of the [[ProducesResponseType]](/dotnet/api/microsoft.aspnetcore.mvc.producesresponsetypeattribute.-ctor) attribute is necessary.</span></span> <span data-ttu-id="2ab1c-126">이 특성은 [Swagger](/aspnet/core/tutorials/web-api-help-pages-using-swagger)와 같은 도구에서 생성한 API 도움말 페이지에 대해 설명이 포함된 응답 세부 정보를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-126">This attribute produces more descriptive response details for API help pages generated by tools like [Swagger](/aspnet/core/tutorials/web-api-help-pages-using-swagger).</span></span> <span data-ttu-id="2ab1c-127">`[ProducesResponseType]`은 작업에서 반환한 알려진 형식 및 HTTP 상태 코드을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-127">`[ProducesResponseType]` indicates the known types and HTTP status codes to be returned by the action.</span></span>

### <a name="synchronous-action"></a><span data-ttu-id="2ab1c-128">동기화 작업</span><span class="sxs-lookup"><span data-stu-id="2ab1c-128">Synchronous action</span></span>

<span data-ttu-id="2ab1c-129">두 가지 가능한 반환 형식이 포함된 다음과 같은 동기 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-129">Consider the following synchronous action in which there are two possible return types:</span></span>

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.Pre21/Controllers/ProductsController.cs?name=snippet_GetById&highlight=8,11)]

<span data-ttu-id="2ab1c-130">위의 작업에서 `id`에서 표시하는 제품이 기본 데이터 저장소에 없는 경우 404 상태 코드가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-130">In the preceding action, a 404 status code is returned when the product represented by `id` doesn't exist in the underlying data store.</span></span> <span data-ttu-id="2ab1c-131">[NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) 도우미 메서드는 `return new NotFoundResult();`에 대한 바로 가기로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-131">The [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) helper method is invoked as a shortcut to `return new NotFoundResult();`.</span></span> <span data-ttu-id="2ab1c-132">제품이 있으면 페이로드를 나타내는 `Product` 개체가 200 상태 코드와 함께 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-132">If the product does exist, a `Product` object representing the payload is returned with a 200 status code.</span></span> <span data-ttu-id="2ab1c-133">[확인](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.ok) 도우미 메서드가 `return new OkObjectResult(product);`의 축약형으로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-133">The [Ok](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.ok) helper method is invoked as the shorthand form of `return new OkObjectResult(product);`.</span></span>

### <a name="asynchronous-action"></a><span data-ttu-id="2ab1c-134">비동기 작업</span><span class="sxs-lookup"><span data-stu-id="2ab1c-134">Asynchronous action</span></span>

<span data-ttu-id="2ab1c-135">두 가지 가능한 반환 형식이 포함된 다음과 같은 비동기 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-135">Consider the following asynchronous action in which there are two possible return types:</span></span>

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.Pre21/Controllers/ProductsController.cs?name=snippet_CreateAsync&highlight=8,13)]

<span data-ttu-id="2ab1c-136">위의 작업에서 모델 유효성 검사에 실패하고 [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) 도우미 메서드를 호출할 때 400 상태 코드가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-136">In the preceding action, a 400 status code is returned when model validation fails and the [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) helper method is invoked.</span></span> <span data-ttu-id="2ab1c-137">예를 들어 다음 모델은 요청이 `Name` 속성 및 값을 제공해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-137">For example, the following model indicates that requests must provide the `Name` property and a value.</span></span> <span data-ttu-id="2ab1c-138">따라서 요청에서 적절한 `Name`을 제공하지 못하면 모델 유효성 검사에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-138">Therefore, failure to provide a proper `Name` in the request causes model validation to fail.</span></span>

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.DataAccess/Models/Product.cs?name=snippet_ProductClass&highlight=5-6)]

<span data-ttu-id="2ab1c-139">이전 동작의 기타 알려진 반환 코드는 201이며 [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction) 도우미 메서드에서 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-139">The preceding action's other known return code is a 201, which is generated by the [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction) helper method.</span></span> <span data-ttu-id="2ab1c-140">이 경로에 `Product` 개체가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-140">In this path, the `Product` object is returned.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="actionresultt-type"></a><span data-ttu-id="2ab1c-141">ActionResult\<T> 형식</span><span class="sxs-lookup"><span data-stu-id="2ab1c-141">ActionResult\<T> type</span></span>

<span data-ttu-id="2ab1c-142">ASP.NET Core 2.1은 Web API 컨트롤러 작업에 대해 [ActionResult\<T>](/dotnet/api/microsoft.aspnetcore.mvc.actionresult-1) 반환 형식을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-142">ASP.NET Core 2.1 introduces the [ActionResult\<T>](/dotnet/api/microsoft.aspnetcore.mvc.actionresult-1) return type for Web API controller actions.</span></span> <span data-ttu-id="2ab1c-143">[ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult)에서 파생된 형식을 반환하거나 [특정 형식](#specific-type)을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-143">It enables you to return a type deriving from [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) or return a [specific type](#specific-type).</span></span> <span data-ttu-id="2ab1c-144">`ActionResult<T>`는 [IActionResult 형식](#iactionresult-type)을 통해 다음과 같은 혜택을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-144">`ActionResult<T>` offers the following benefits over the [IActionResult type](#iactionresult-type):</span></span>

* <span data-ttu-id="2ab1c-145">[[ProducesResponseType]](/dotnet/api/microsoft.aspnetcore.mvc.producesresponsetypeattribute) 특성의 `Type` 속성을 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-145">The [[ProducesResponseType]](/dotnet/api/microsoft.aspnetcore.mvc.producesresponsetypeattribute) attribute's `Type` property can be excluded.</span></span> <span data-ttu-id="2ab1c-146">예를 들어 `[ProducesResponseType(200, Type = typeof(Product))]`은 `[ProducesResponseType(200)]`으로 단순화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-146">For example, `[ProducesResponseType(200, Type = typeof(Product))]` is simplified to `[ProducesResponseType(200)]`.</span></span> <span data-ttu-id="2ab1c-147">작업의 예상 반환 형식은 대신 `ActionResult<T>`의 `T`에서 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-147">The action's expected return type is instead inferred from the `T` in `ActionResult<T>`.</span></span>
* <span data-ttu-id="2ab1c-148">[암시적 캐스트 연산자](/dotnet/csharp/language-reference/keywords/implicit)는 `T` 및 `ActionResult` 모두를 `ActionResult<T>`로 변환하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-148">[Implicit cast operators](/dotnet/csharp/language-reference/keywords/implicit) support the conversion of both `T` and `ActionResult` to `ActionResult<T>`.</span></span> <span data-ttu-id="2ab1c-149">`T`는 [ObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.objectresult)로 변환합니다. 즉, `return new ObjectResult(T);`는 `return T;`로 간소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-149">`T` converts to [ObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.objectresult), which means `return new ObjectResult(T);` is simplified to `return T;`.</span></span>

<span data-ttu-id="2ab1c-150">C#은 인터페이스에서 암시적 캐스트 연산자를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-150">C# doesn't support implicit cast operators on interfaces.</span></span> <span data-ttu-id="2ab1c-151">따라서 인터페이스를 구체적인 형식으로 전환하려면 `ActionResult<T>`를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-151">Consequently, conversion of the interface to a concrete type is necessary to use `ActionResult<T>`.</span></span> <span data-ttu-id="2ab1c-152">예를 들어 다음 예제에서 `IEnumerable`을 사용하면 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-152">For example, use of `IEnumerable` in the following example doesn't work:</span></span>

```csharp
[HttpGet]
public ActionResult<IEnumerable<Product>> Get()
{
    return _repository.GetProducts();
}
```

<span data-ttu-id="2ab1c-153">이전 코드를 수정하는 한 가지 옵션으로 `_repository.GetProducts().ToList();`를 반환해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-153">One option to fix the preceding code is to return `_repository.GetProducts().ToList();`.</span></span>

<span data-ttu-id="2ab1c-154">대부분의 작업에는 특정 반환 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-154">Most actions have a specific return type.</span></span> <span data-ttu-id="2ab1c-155">작업을 실행하는 동안 예기치 않은 조건이 발생할 수 있습니다. 이 경우에 특정 형식이 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-155">Unexpected conditions can occur during action execution, in which case the specific type isn't returned.</span></span> <span data-ttu-id="2ab1c-156">예를 들어 작업의 입력 매개 변수는 모델 유효성 검사에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-156">For example, an action's input parameter may fail model validation.</span></span> <span data-ttu-id="2ab1c-157">이러한 경우에 일반적으로 특정 형식이 아닌 적절한 `ActionResult` 형식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-157">In such a case, it's common to return the appropriate `ActionResult` type instead of the specific type.</span></span>

### <a name="synchronous-action"></a><span data-ttu-id="2ab1c-158">동기화 작업</span><span class="sxs-lookup"><span data-stu-id="2ab1c-158">Synchronous action</span></span>

<span data-ttu-id="2ab1c-159">두 가지 가능한 반환 형식이 포함된 동기 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-159">Consider a synchronous action in which there are two possible return types:</span></span>

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_GetById&highlight=8,11)]

<span data-ttu-id="2ab1c-160">위의 코드에서 404 상태 코드는 제품이 데이터베이스에 존재하지 않는 경우에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-160">In the preceding code, a 404 status code is returned when the product doesn't exist in the database.</span></span> <span data-ttu-id="2ab1c-161">제품이 없는 경우 해당하는 `Product` 개체가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-161">If the product does exist, the corresponding `Product` object is returned.</span></span> <span data-ttu-id="2ab1c-162">ASP.NET Core 2.1 이전에 `return product;` 줄은 `return Ok(product);`이었습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-162">Before ASP.NET Core 2.1, the `return product;` line would have been `return Ok(product);`.</span></span>

> [!TIP]
> <span data-ttu-id="2ab1c-163">ASP.NET Core 2.1을 기준으로 작업 매개 변수 바인딩 원본 유추는 컨트롤러 클래스를 `[ApiController]` 특성으로 데코레이팅할 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-163">As of ASP.NET Core 2.1, action parameter binding source inference is enabled when a controller class is decorated with the `[ApiController]` attribute.</span></span> <span data-ttu-id="2ab1c-164">경로 템플릿의 이름과 일치하는 매개 변수 이름은 요청 경로 데이터를 사용하여 자동으로 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-164">A parameter name matching a name in the route template is automatically bound using the request route data.</span></span> <span data-ttu-id="2ab1c-165">따라서 위 작업의 `id` 매개 변수가 [[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute) 특성을 사용하여 명시적으로 주석으로 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-165">Consequently, the preceding action's `id` parameter isn't explicitly annotated with the [[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute) attribute.</span></span>

### <a name="asynchronous-action"></a><span data-ttu-id="2ab1c-166">비동기 작업</span><span class="sxs-lookup"><span data-stu-id="2ab1c-166">Asynchronous action</span></span>

<span data-ttu-id="2ab1c-167">두 가지 가능한 반환 형식이 포함된 비동기 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-167">Consider an asynchronous action in which there are two possible return types:</span></span>

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_CreateAsync&highlight=8,13)]

<span data-ttu-id="2ab1c-168">모델 유효성 검사에 실패하는 경우 [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest#Microsoft_AspNetCore_Mvc_ControllerBase_BadRequest_Microsoft_AspNetCore_Mvc_ModelBinding_ModelStateDictionary_) 메서드를 호출하여 400 상태 코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-168">If model validation fails, the [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest#Microsoft_AspNetCore_Mvc_ControllerBase_BadRequest_Microsoft_AspNetCore_Mvc_ModelBinding_ModelStateDictionary_) method is invoked to return a 400 status code.</span></span> <span data-ttu-id="2ab1c-169">특정 유효성 검사 오류를 포함하는 [ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) 속성을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-169">The [ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) property containing the specific validation errors is passed to it.</span></span> <span data-ttu-id="2ab1c-170">모델 유효성 검사에 성공하는 경우 제품이 데이터베이스에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-170">If model validation succeeds, the product is created in the database.</span></span> <span data-ttu-id="2ab1c-171">201 상태 코드가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-171">A 201 status code is returned.</span></span>

> [!TIP]
> <span data-ttu-id="2ab1c-172">ASP.NET Core 2.1을 기준으로 작업 매개 변수 바인딩 원본 유추는 컨트롤러 클래스를 `[ApiController]` 특성으로 데코레이팅할 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-172">As of ASP.NET Core 2.1, action parameter binding source inference is enabled when a controller class is decorated with the `[ApiController]` attribute.</span></span> <span data-ttu-id="2ab1c-173">복합 형식 매개 변수는 요청 본문을 사용하여 자동으로 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-173">Complex type parameters are automatically bound using the request body.</span></span> <span data-ttu-id="2ab1c-174">따라서 위 작업의 `product` 매개 변수가 [[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) 특성을 사용하여 명시적으로 주석으로 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab1c-174">Consequently, the preceding action's `product` parameter isn't explicitly annotated with the [[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) attribute.</span></span>

::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="2ab1c-175">추가 자료</span><span class="sxs-lookup"><span data-stu-id="2ab1c-175">Additional resources</span></span>

* <xref:mvc/controllers/actions>
* <xref:mvc/models/validation>
* <xref:tutorials/web-api-help-pages-using-swagger>
