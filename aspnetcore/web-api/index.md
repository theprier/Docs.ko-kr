---
title: ASP.NET Core에서 Web API 빌드
author: scottaddie
description: ASP.NET Core에서 Web API를 빌드하는 데 사용할 수 있는 기능과 각 기능을 사용하기에 적합한 시기에 대해 알아봅니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 01/11/2019
uid: web-api/index
ms.openlocfilehash: bc8be67957a56a818a88e0496d45db1e7b7aed0e
ms.sourcegitcommit: a467828b5e4eaae291d961ffe2279a571900de23
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2019
ms.locfileid: "58142363"
---
# <a name="build-web-apis-with-aspnet-core"></a><span data-ttu-id="3d742-103">ASP.NET Core에서 Web API 빌드</span><span class="sxs-lookup"><span data-stu-id="3d742-103">Build web APIs with ASP.NET Core</span></span>

<span data-ttu-id="3d742-104">작성자: [Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="3d742-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="3d742-105">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="3d742-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="3d742-106">이 문서에서는 ASP.NET Core에서 Web API를 빌드하는 방법과 각 기능을 사용하기에 가장 적합한 시기에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-106">This document explains how to build a web API in ASP.NET Core and when it's most appropriate to use each feature.</span></span>

## <a name="derive-class-from-controllerbase"></a><span data-ttu-id="3d742-107">ControllerBase에서 클래스 파생</span><span class="sxs-lookup"><span data-stu-id="3d742-107">Derive class from ControllerBase</span></span>

<span data-ttu-id="3d742-108">Web API를 제공할 목적으로 컨트롤의 <xref:Microsoft.AspNetCore.Mvc.ControllerBase> 클래스에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-108">Inherit from the <xref:Microsoft.AspNetCore.Mvc.ControllerBase> class in a controller that's intended to serve as a web API.</span></span> <span data-ttu-id="3d742-109">예:</span><span class="sxs-lookup"><span data-stu-id="3d742-109">For example:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

<span data-ttu-id="3d742-110">`ControllerBase` 클래스는 여러 속성 및 메서드에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-110">The `ControllerBase` class provides access to several properties and methods.</span></span> <span data-ttu-id="3d742-111">위의 코드에 나온 예제에는 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest(Microsoft.AspNetCore.Mvc.ModelBinding.ModelStateDictionary)> 및 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction(System.String,System.Object,System.Object)>가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-111">In the preceding code, examples include <xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest(Microsoft.AspNetCore.Mvc.ModelBinding.ModelStateDictionary)> and <xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction(System.String,System.Object,System.Object)>.</span></span> <span data-ttu-id="3d742-112">이러한 메서드는 각각 HTTP 400와 201 상태 코드를 반환하는 작업 메서드 내에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-112">These methods are called within action methods to return HTTP 400 and 201 status codes, respectively.</span></span> <span data-ttu-id="3d742-113">요청 모델 유효성 검사를 처리하기 위해 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.ModelState> 속성에 액세스하며, 이 속성은 `ControllerBase`에서도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-113">The <xref:Microsoft.AspNetCore.Mvc.ControllerBase.ModelState> property, also provided by `ControllerBase`, is accessed to handle request model validation.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="annotation-with-apicontroller-attribute"></a><span data-ttu-id="3d742-114">ApiController 특성 주석</span><span class="sxs-lookup"><span data-stu-id="3d742-114">Annotation with ApiController attribute</span></span>

<span data-ttu-id="3d742-115">ASP.NET Core 2.1에서는 Web API 컨트롤러 클래스를 나타내는 [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) 특성을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-115">ASP.NET Core 2.1 introduces the [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) attribute to denote a web API controller class.</span></span> <span data-ttu-id="3d742-116">예:</span><span class="sxs-lookup"><span data-stu-id="3d742-116">For example:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]

<span data-ttu-id="3d742-117"><xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*>을 통해 설정된 호환성 버전 2.1 이상은 컨트롤러 수준에서 이 특성을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-117">A compatibility version of 2.1 or later, set via <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*>, is required to use this attribute at the controller level.</span></span> <span data-ttu-id="3d742-118">예를 들어 `Startup.ConfigureServices`에서 강조 표시된 코드는 2.1 호환성 플래그를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-118">For example, the highlighted code in `Startup.ConfigureServices` sets the 2.1 compatibility flag:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Startup.cs?name=snippet_SetCompatibilityVersion&highlight=2)]

<span data-ttu-id="3d742-119">자세한 내용은 <xref:mvc/compatibility-version>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d742-119">For more information, see <xref:mvc/compatibility-version>.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="3d742-120">ASP.NET Core 2.2 이상에서는 `[ApiController]` 특성을 어셈블리에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-120">In ASP.NET Core 2.2 or later, the `[ApiController]` attribute can be applied to an assembly.</span></span> <span data-ttu-id="3d742-121">이 방식의 주석은 웹 API 동작을 어셈블리의 모든 컨트롤러에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-121">Annotation in this manner applies web API behavior to all controllers in the assembly.</span></span> <span data-ttu-id="3d742-122">개별 컨트롤러에 대해 옵트아웃하는 방법은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-122">Beware that there's no way to opt out for individual controllers.</span></span> <span data-ttu-id="3d742-123">권장 사항으로 어셈블리 수준의 특성이 `Startup` 클래스에 적용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-123">As a recommendation, assembly-level attributes should be applied to the `Startup` class:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.22/Startup.cs?name=snippet_ApiControllerAttributeOnAssembly&highlight=1)]

<span data-ttu-id="3d742-124"><xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*>을 통해 설정된 호환성 버전 2.2 이상은 어셈블리 수준에서 이 특성을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-124">A compatibility version of 2.2 or later, set via <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*>, is required to use this attribute at the assembly level.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="3d742-125">`[ApiController]` 특성은 일반적으로 `ControllerBase`와 함께 컨트롤러에 대한 REST 특정 동작을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-125">The `[ApiController]` attribute is commonly coupled with `ControllerBase` to enable REST-specific behavior for controllers.</span></span> <span data-ttu-id="3d742-126">`ControllerBase`는 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.NotFound*> 및 <xref:Microsoft.AspNetCore.Mvc.ControllerBase.File*> 같은 메서드에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-126">`ControllerBase` provides access to methods such as <xref:Microsoft.AspNetCore.Mvc.ControllerBase.NotFound*> and <xref:Microsoft.AspNetCore.Mvc.ControllerBase.File*>.</span></span>

<span data-ttu-id="3d742-127">다른 방법은 `[ApiController]` 특성으로 주석 지정된 사용자 지정 기본 컨트롤러 클래스를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-127">Another approach is to create a custom base controller class annotated with the `[ApiController]` attribute:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]

<span data-ttu-id="3d742-128">다음 섹션에서는 특성으로 추가된 편리한 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-128">The following sections describe convenience features added by the attribute.</span></span>

### <a name="automatic-http-400-responses"></a><span data-ttu-id="3d742-129">자동 HTTP 400 응답</span><span class="sxs-lookup"><span data-stu-id="3d742-129">Automatic HTTP 400 responses</span></span>

<span data-ttu-id="3d742-130">모델 유효성 검사 오류 시 HTTP 400 응답이 자동으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-130">Model validation errors automatically trigger an HTTP 400 response.</span></span> <span data-ttu-id="3d742-131">따라서 다음 코드는 실제 작업 시 불필요하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-131">Consequently, the following code becomes unnecessary in your actions:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_ModelStateIsValidCheck)]

<span data-ttu-id="3d742-132"><xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.InvalidModelStateResponseFactory>를 사용하여 결과 응답의 출력을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-132">Use <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.InvalidModelStateResponseFactory> to customize the output of the resulting response.</span></span>

<span data-ttu-id="3d742-133">모델 유효성 검사 오류에서 작업을 복구할 수 있을 때 기본 동작을 비활성화하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-133">Disabling the default behavior is useful when your action can recover from a model validation error.</span></span> <span data-ttu-id="3d742-134"><xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressModelStateInvalidFilter> 속성이 `true`로 설정된 경우 기본 동작이 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-134">The default behavior is disabled when the <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressModelStateInvalidFilter> property is set to `true`.</span></span> <span data-ttu-id="3d742-135">`services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_<version_number>);` 뒤에 다음 코드를 `Startup.ConfigureServices`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-135">Add the following code in `Startup.ConfigureServices` after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_<version_number>);`:</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

[!code-csharp[](define-controller/samples/WebApiSample.Api.22/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=7)]

::: moniker-end

::: moniker range="= aspnetcore-2.1"

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="3d742-136">호환성 플래그가 2.2 이상이면 HTTP 400 응답에 대한 기본 응답 형식은 <xref:Microsoft.AspNetCore.Mvc.ValidationProblemDetails>입니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-136">With a compatibility flag of 2.2 or later, the default response type for HTTP 400 responses is <xref:Microsoft.AspNetCore.Mvc.ValidationProblemDetails>.</span></span> <span data-ttu-id="3d742-137">`ValidationProblemDetails` 형식은 [RFC 7807 사양](https://tools.ietf.org/html/rfc7807)을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-137">The `ValidationProblemDetails` type complies with the [RFC 7807 specification](https://tools.ietf.org/html/rfc7807).</span></span> <span data-ttu-id="3d742-138">대신 `SuppressUseValidationProblemDetailsForInvalidModelStateResponses` 속성을 `true`로 설정하여 <xref:Microsoft.AspNetCore.Mvc.SerializableError>의 ASP.NET Core 2.1 오류 형식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-138">Set the `SuppressUseValidationProblemDetailsForInvalidModelStateResponses` property to `true` to instead return the ASP.NET Core 2.1 error format of <xref:Microsoft.AspNetCore.Mvc.SerializableError>.</span></span> <span data-ttu-id="3d742-139">다음 코드를 `Startup.ConfigureServices`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-139">Add the following code in `Startup.ConfigureServices`:</span></span>

```csharp
services.AddMvc()
    .SetCompatibilityVersion(CompatibilityVersion.Version_2_2)
    .ConfigureApiBehaviorOptions(options =>
    {
        options
          .SuppressUseValidationProblemDetailsForInvalidModelStateResponses = true;
    });
```

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

### <a name="binding-source-parameter-inference"></a><span data-ttu-id="3d742-140">바인딩 소스 매개 변수 유추</span><span class="sxs-lookup"><span data-stu-id="3d742-140">Binding source parameter inference</span></span>

<span data-ttu-id="3d742-141">바인딩 소스 특성은 작업 매개 변수 값이 발견되는 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-141">A binding source attribute defines the location at which an action parameter's value is found.</span></span> <span data-ttu-id="3d742-142">다음 바인딩 소스 특성이 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-142">The following binding source attributes exist:</span></span>

|<span data-ttu-id="3d742-143">특성</span><span class="sxs-lookup"><span data-stu-id="3d742-143">Attribute</span></span>|<span data-ttu-id="3d742-144">바인딩 원본</span><span class="sxs-lookup"><span data-stu-id="3d742-144">Binding source</span></span> |
|---------|---------|
|<span data-ttu-id="3d742-145">**[[FromBody]](xref:Microsoft.AspNetCore.Mvc.FromBodyAttribute)**</span><span class="sxs-lookup"><span data-stu-id="3d742-145">**[[FromBody]](xref:Microsoft.AspNetCore.Mvc.FromBodyAttribute)**</span></span>     | <span data-ttu-id="3d742-146">요청 본문</span><span class="sxs-lookup"><span data-stu-id="3d742-146">Request body</span></span> |
|<span data-ttu-id="3d742-147">**[[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute)**</span><span class="sxs-lookup"><span data-stu-id="3d742-147">**[[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute)**</span></span>     | <span data-ttu-id="3d742-148">요청 본문에서 양식 데이터</span><span class="sxs-lookup"><span data-stu-id="3d742-148">Form data in the request body</span></span> |
|<span data-ttu-id="3d742-149">**[[FromHeader]](xref:Microsoft.AspNetCore.Mvc.FromHeaderAttribute)**</span><span class="sxs-lookup"><span data-stu-id="3d742-149">**[[FromHeader]](xref:Microsoft.AspNetCore.Mvc.FromHeaderAttribute)**</span></span> | <span data-ttu-id="3d742-150">요청 헤더</span><span class="sxs-lookup"><span data-stu-id="3d742-150">Request header</span></span> |
|<span data-ttu-id="3d742-151">**[[FromQuery]](xref:Microsoft.AspNetCore.Mvc.FromQueryAttribute)**</span><span class="sxs-lookup"><span data-stu-id="3d742-151">**[[FromQuery]](xref:Microsoft.AspNetCore.Mvc.FromQueryAttribute)**</span></span>   | <span data-ttu-id="3d742-152">요청 쿼리 문자열 매개 변수</span><span class="sxs-lookup"><span data-stu-id="3d742-152">Request query string parameter</span></span> |
|<span data-ttu-id="3d742-153">**[[FromRoute]](xref:Microsoft.AspNetCore.Mvc.FromRouteAttribute)**</span><span class="sxs-lookup"><span data-stu-id="3d742-153">**[[FromRoute]](xref:Microsoft.AspNetCore.Mvc.FromRouteAttribute)**</span></span>   | <span data-ttu-id="3d742-154">현재 요청의 경로 데이터</span><span class="sxs-lookup"><span data-stu-id="3d742-154">Route data from the current request</span></span> |
|<span data-ttu-id="3d742-155">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span><span class="sxs-lookup"><span data-stu-id="3d742-155">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span></span> | <span data-ttu-id="3d742-156">작업 매개 변수로 삽입된 요청 서비스</span><span class="sxs-lookup"><span data-stu-id="3d742-156">The request service injected as an action parameter</span></span> |

> [!WARNING]
> <span data-ttu-id="3d742-157">값에 `%2f`(즉, `/`)이 포함될 수 있는 경우 `[FromRoute]`를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-157">Don't use `[FromRoute]` when values might contain `%2f` (that is `/`).</span></span> <span data-ttu-id="3d742-158">`%2f`는 `/`로 이스케이프가 해제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-158">`%2f` won't be unescaped to `/`.</span></span> <span data-ttu-id="3d742-159">값에 `%2f`가 포함될 수 있으면 `[FromQuery]`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-159">Use `[FromQuery]` if the value might contain `%2f`.</span></span>

<span data-ttu-id="3d742-160">`[ApiController]` 특성 없이, 바인딩 소스 특성이 명시적으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-160">Without the `[ApiController]` attribute, binding source attributes are explicitly defined.</span></span> <span data-ttu-id="3d742-161">`[ApiController]` 또는 `[FromQuery]` 같은 다른 바인딩 소스 특성 없이, ASP.NET Core 런타임에서 복합 개체 모델 바인더 사용을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-161">Without `[ApiController]` or other binding source attributes like `[FromQuery]`, the ASP.NET Core runtime attempts to use the complex object model binder.</span></span> <span data-ttu-id="3d742-162">복합 개체 모델 바인더는 값 공급자(정의된 순서가 있음)로부터 데이터를 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-162">The complex object model binder pulls data from value providers (which have a defined order).</span></span> <span data-ttu-id="3d742-163">예를 들어 ‘본문 모델 바인더’는 항상 옵트인됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-163">For instance, the 'body model binder' is always opt in.</span></span>

<span data-ttu-id="3d742-164">다음 예제에서 `[FromQuery]` 특성은 `discontinuedOnly` 매개 변수 값이 요청 URL의 쿼리 문자열에 제공됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-164">In the following example, the `[FromQuery]` attribute indicates that the `discontinuedOnly` parameter value is provided in the request URL's query string:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=3)]

<span data-ttu-id="3d742-165">유추 규칙이 작업 매개 변수의 기본 데이터 원본에 대해 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-165">Inference rules are applied for the default data sources of action parameters.</span></span> <span data-ttu-id="3d742-166">이러한 규칙은 작업 매개 변수에 달리 수동으로 적용할 가능성이 높은 바인딩 소스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-166">These rules configure the binding sources you're otherwise likely to manually apply to the action parameters.</span></span> <span data-ttu-id="3d742-167">바인딩 소스 특성은 다음과 같이 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-167">The binding source attributes behave as follows:</span></span>

* <span data-ttu-id="3d742-168">**[FromBody]** 는 복합 형식 매개 변수에 대해 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-168">**[FromBody]** is inferred for complex type parameters.</span></span> <span data-ttu-id="3d742-169">이 규칙은 <xref:Microsoft.AspNetCore.Http.IFormCollection> 및 <xref:System.Threading.CancellationToken> 같이 특별한 의미를 지닌 복합 기본 제공 형식에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-169">An exception to this rule is any complex, built-in type with a special meaning, such as <xref:Microsoft.AspNetCore.Http.IFormCollection> and <xref:System.Threading.CancellationToken>.</span></span> <span data-ttu-id="3d742-170">바인딩 소스 유추 코드는 이러한 특별한 형식을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-170">The binding source inference code ignores those special types.</span></span> <span data-ttu-id="3d742-171">`[FromBody]`는 `string` 또는 `int` 같은 단순 형식에 대해 유추되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-171">`[FromBody]` isn't inferred for simple types such as `string` or `int`.</span></span> <span data-ttu-id="3d742-172">따라서 해당 기능이 필요한 경우 단순 형식에 `[FromBody]` 특성을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-172">Therefore, the `[FromBody]` attribute should be used for simple types when that functionality is needed.</span></span> <span data-ttu-id="3d742-173">작업에 명시적으로 지정(`[FromBody]`를 통해)되거나 요청 본문의 바인딩으로 유추된 한 개를 초과하는 매개 변수가 있는 경우 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-173">When an action has more than one parameter explicitly specified (via `[FromBody]`) or inferred as bound from the request body, an exception is thrown.</span></span> <span data-ttu-id="3d742-174">예를 들어 다음 작업 서명으로 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-174">For example, the following action signatures cause an exception:</span></span>

    [!code-csharp[](define-controller/samples/WebApiSample.Api.21/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]

    > [!NOTE]
    > <span data-ttu-id="3d742-175">ASP.NET Core 2.1에서 목록, 배열 등의 컬렉션 형식 매개 변수를 [[FromQuery]](xref:Microsoft.AspNetCore.Mvc.FromQueryAttribute)로 잘못 유추합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-175">In ASP.NET Core 2.1, collection type parameters such as lists and arrays are incorrectly inferred as [[FromQuery]](xref:Microsoft.AspNetCore.Mvc.FromQueryAttribute).</span></span> <span data-ttu-id="3d742-176">이러한 매개 변수가 요청 본문에서 바인딩되는 경우 해당 매개 변수에 [[FromBody]](xref:Microsoft.AspNetCore.Mvc.FromBodyAttribute)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-176">[[FromBody]](xref:Microsoft.AspNetCore.Mvc.FromBodyAttribute) should be used for these parameters if they are to be bound from the request body.</span></span> <span data-ttu-id="3d742-177">이 문제는 ASP.NET Core 2.2 이상에서 해결됩니다. 즉, 기본적으로 컬렉션 형식 매개 변수를 본문에서 바인딩되도록 유추합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-177">This behavior is fixed in ASP.NET Core 2.2 or later, where collection type parameters are inferred to be bound from the body by default.</span></span>

* <span data-ttu-id="3d742-178">**[FromForm]** 은 <xref:Microsoft.AspNetCore.Http.IFormFile> 및 <xref:Microsoft.AspNetCore.Http.IFormFileCollection> 형식의 작업 매개 변수에 대해 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-178">**[FromForm]** is inferred for action parameters of type <xref:Microsoft.AspNetCore.Http.IFormFile> and <xref:Microsoft.AspNetCore.Http.IFormFileCollection>.</span></span> <span data-ttu-id="3d742-179">단순 또는 사용자 정의 형식에 대해서는 유추되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-179">It's not inferred for any simple or user-defined types.</span></span>
* <span data-ttu-id="3d742-180">**[FromRoute]** 는 경로 템플릿에서 매개 변수와 일치하는 작업 매개 변수 이름에 대해 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-180">**[FromRoute]** is inferred for any action parameter name matching a parameter in the route template.</span></span> <span data-ttu-id="3d742-181">둘 이상의 경로가 작업 매개 변수와 일치하는 경우 모든 경로 값은 `[FromRoute]`로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-181">When more than one route matches an action parameter, any route value is considered `[FromRoute]`.</span></span>
* <span data-ttu-id="3d742-182">**[FromQuery]** 는 다른 작업 매개 변수에 대해 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-182">**[FromQuery]** is inferred for any other action parameters.</span></span>

<span data-ttu-id="3d742-183"><xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressInferBindingSourcesForParameters> 속성이 `true`로 설정된 경우 기본 유추 규칙이 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-183">The default inference rules are disabled when the <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressInferBindingSourcesForParameters> property is set to `true`.</span></span> <span data-ttu-id="3d742-184">`services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_<version_number>);` 뒤에 다음 코드를 `Startup.ConfigureServices`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-184">Add the following code in `Startup.ConfigureServices` after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_<version_number>);`:</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

[!code-csharp[](define-controller/samples/WebApiSample.Api.22/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=6)]

::: moniker-end

::: moniker range="= aspnetcore-2.1"

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

### <a name="multipartform-data-request-inference"></a><span data-ttu-id="3d742-185">다중 파트/폼 데이터 요청 유추</span><span class="sxs-lookup"><span data-stu-id="3d742-185">Multipart/form-data request inference</span></span>

<span data-ttu-id="3d742-186">작업 매개 변수를 [[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute) 특성으로 주석 처리하는 경우 `multipart/form-data` 요청 콘텐츠 형식이 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-186">When an action parameter is annotated with the [[FromForm]](xref:Microsoft.AspNetCore.Mvc.FromFormAttribute) attribute, the `multipart/form-data` request content type is inferred.</span></span>

<span data-ttu-id="3d742-187"><xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressConsumesConstraintForFormFileParameters> 속성이 `true`로 설정된 경우 기본 동작이 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-187">The default behavior is disabled when the <xref:Microsoft.AspNetCore.Mvc.ApiBehaviorOptions.SuppressConsumesConstraintForFormFileParameters> property is set to `true`.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="3d742-188">다음 코드를 `Startup.ConfigureServices`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-188">Add the following code in `Startup.ConfigureServices`:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.22/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]

::: moniker-end

::: moniker range="= aspnetcore-2.1"

<span data-ttu-id="3d742-189">`services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 뒤에 다음 코드를 `Startup.ConfigureServices`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-189">Add the following code in `Startup.ConfigureServices` after `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);`:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

### <a name="attribute-routing-requirement"></a><span data-ttu-id="3d742-190">특성 라우팅 요구 사항</span><span class="sxs-lookup"><span data-stu-id="3d742-190">Attribute routing requirement</span></span>

<span data-ttu-id="3d742-191">특성 라우팅은 요구 사항이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-191">Attribute routing becomes a requirement.</span></span> <span data-ttu-id="3d742-192">예:</span><span class="sxs-lookup"><span data-stu-id="3d742-192">For example:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]

<span data-ttu-id="3d742-193">작업은 <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvc*>에 정의된 [규칙 기반 경로](xref:mvc/controllers/routing#conventional-routing)를 통해 또는 `Startup.Configure`의 <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*>에 의해 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-193">Actions are inaccessible via [conventional routes](xref:mvc/controllers/routing#conventional-routing) defined in <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvc*> or by <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> in `Startup.Configure`.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

### <a name="problem-details-responses-for-error-status-codes"></a><span data-ttu-id="3d742-194">오류 상태 코드에 대한 문제 세부 정보 응답</span><span class="sxs-lookup"><span data-stu-id="3d742-194">Problem details responses for error status codes</span></span>

<span data-ttu-id="3d742-195">ASP.NET Core 2.2 이상에서 MVC는 오류 결과(상태 코드 400 이상의 결과)를 <xref:Microsoft.AspNetCore.Mvc.ProblemDetails>가 있는 결과로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-195">In ASP.NET Core 2.2 or later, MVC transforms an error result (a result with status code 400 or higher) to a result with <xref:Microsoft.AspNetCore.Mvc.ProblemDetails>.</span></span> <span data-ttu-id="3d742-196">`ProblemDetails`인 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-196">`ProblemDetails` is:</span></span>

* <span data-ttu-id="3d742-197">[RFC 7807 사양](https://tools.ietf.org/html/rfc7807)에 기반한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-197">A type based on the [RFC 7807 specification](https://tools.ietf.org/html/rfc7807).</span></span>
* <span data-ttu-id="3d742-198">HTTP 응답에서 머신에서 읽을 수 있는 오류 세부 정보를 지정하기 위한 표준화된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-198">A standardized format for specifying machine-readable error details in an HTTP response.</span></span>

<span data-ttu-id="3d742-199">다음 컨트롤러 작업에서 다음 코드를 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="3d742-199">Consider the following code in a controller action:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.22/Controllers/ProductsController.cs?name=snippet_ProblemDetailsStatusCode)]

<span data-ttu-id="3d742-200">`NotFound`에 대한 HTTP 응답에는 `ProblemDetails` 본문과 함께 404 상태 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-200">The HTTP response for `NotFound` has a 404 status code with a `ProblemDetails` body.</span></span> <span data-ttu-id="3d742-201">예:</span><span class="sxs-lookup"><span data-stu-id="3d742-201">For example:</span></span>

```json
{
    type: "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    title: "Not Found",
    status: 404,
    traceId: "0HLHLV31KRN83:00000001"
}
```

<span data-ttu-id="3d742-202">문제 세부 정보 기능을 사용하려면 2.2 이상의 호환성 플래그가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-202">The problem details feature requires a compatibility flag of 2.2 or later.</span></span> <span data-ttu-id="3d742-203">`SuppressMapClientErrors` 속성이 `true`로 설정된 경우 기본 동작이 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-203">The default behavior is disabled when the `SuppressMapClientErrors` property is set to `true`.</span></span> <span data-ttu-id="3d742-204">다음 코드를 `Startup.ConfigureServices`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-204">Add the following code in `Startup.ConfigureServices`:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.22/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=8)]

<span data-ttu-id="3d742-205">`ClientErrorMapping` 속성을 사용하여 `ProblemDetails` 응답의 내용을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-205">Use the `ClientErrorMapping` property to configure the contents of the `ProblemDetails` response.</span></span> <span data-ttu-id="3d742-206">예를 들어 다음 코드는 404 응답에 대해 `type` 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3d742-206">For example, the following code updates the `type` property for 404 responses:</span></span>

[!code-csharp[](define-controller/samples/WebApiSample.Api.22/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=10-11)]

::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="3d742-207">추가 자료</span><span class="sxs-lookup"><span data-stu-id="3d742-207">Additional resources</span></span>

* <xref:web-api/action-return-types>
* <xref:web-api/advanced/custom-formatters>
* <xref:web-api/advanced/formatting>
* <xref:tutorials/web-api-help-pages-using-swagger>
* <xref:mvc/controllers/routing>
