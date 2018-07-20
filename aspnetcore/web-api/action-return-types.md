---
title: ASP.NET Core Web API에서 컨트롤러 작업 반환 형식
author: scottaddie
description: ASP.NET Core Web API에서 다양한 컨트롤러 작업 메서드 반환 형식을 사용하는 방법을 알아봅니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 03/21/2018
uid: web-api/action-return-types
ms.openlocfilehash: 422db97da222fb5e742e1d8e6ae410edc90dbc18
ms.sourcegitcommit: ee2b26c7d08b38c908c668522554b52ab8efa221
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2018
ms.locfileid: "36273558"
---
# <a name="controller-action-return-types-in-aspnet-core-web-api"></a>ASP.NET Core Web API에서 컨트롤러 작업 반환 형식

작성자: [Scott Addie](https://github.com/scottaddie)

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/action-return-types/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

ASP.NET Core에서는 Web API 컨트롤러 작업 반환 형식에 다음 옵션을 제공합니다.

::: moniker range="<= aspnetcore-2.0"
* [특정 형식](#specific-type)
* [IActionResult](#iactionresult-type)
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
* [특정 형식](#specific-type)
* [IActionResult](#iactionresult-type)
* [ActionResult\<T>](#actionresultt-type)
::: moniker-end

이 문서에서는 각 반환 형식을 사용하는 것이 가장 적합한 경우를 설명합니다.

## <a name="specific-type"></a>특정 형식

가장 간단한 작업은 기본 또는 복합 데이터 형식을 반환합니다(예: `string` 또는 사용자 지정 개체 형식). 다음 작업을 사용하여 사용자 지정 `Product` 개체의 컬렉션을 반환합니다.

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_Get)]

작업 실행 중에 보호할 알려진 조건 없이 특정 형식을 반환하는 것으로 충분합니다. 매개 변수 제약 조건 유효성 검사가 필요하지 않으므로 위의 작업은 매개 변수를 허용하지 않습니다.

알려진 조건이 작업에서 고려되지 않으면 여러 반환 경로가 도입됩니다’. 이 경우에 기본 또는 복합적인 반환 형식의 [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) 반환 형식을 혼합하는 것이 일반적입니다. 이 종류의 동작을 수용하기 위해 [IActionResult](#iactionresult-type) 또는 [ActionResult\<T>](#actionresultt-type) 중 하나가 필요합니다.

## <a name="iactionresult-type"></a>IActionResult 형식

여러 [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) 반환 형식을 동작에서 사용할 수 있는 경우 [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult) 반환 형식이 적절합니다. `ActionResult` 형식은 다양한 HTTP 상태 코드를 나타냅니다. 이 범주에 속하는 몇 가지 일반적인 반환 형식은 [BadRequestResult](/dotnet/api/microsoft.aspnetcore.mvc.badrequestresult)(400), [NotFoundResult](/dotnet/api/microsoft.aspnetcore.mvc.notfoundresult)(404) 및 [OkObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.okobjectresult)(200)입니다.

작업에서 자유롭게 여러 반환 형식 및 경로가 있기 때문에 [[ProducesResponseType]](/dotnet/api/microsoft.aspnetcore.mvc.producesresponsetypeattribute.-ctor) 특성이 필요합니다. 이 특성은 [Swagger](/aspnet/core/tutorials/web-api-help-pages-using-swagger)와 같은 도구에서 생성한 API 도움말 페이지에 대해 설명이 포함된 응답 세부 정보를 생성합니다. `[ProducesResponseType]`은 작업에서 반환한 알려진 형식 및 HTTP 상태 코드을 나타냅니다.

### <a name="synchronous-action"></a>동기화 작업

두 가지 가능한 반환 형식이 포함된 다음과 같은 동기 작업을 사용합니다.

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.Pre21/Controllers/ProductsController.cs?name=snippet_GetById&highlight=8,11)]

위의 작업에서 `id`에서 표시하는 제품이 기본 데이터 저장소에 없는 경우 404 상태 코드가 반환됩니다. [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) 도우미 메서드는 `return new NotFoundResult();`에 대한 바로 가기로 호출됩니다. 제품이 있으면 페이로드를 나타내는 `Product` 개체가 200 상태 코드와 함께 반환됩니다. [확인](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.ok) 도우미 메서드가 `return new OkObjectResult(product);`의 축약형으로 호출됩니다.

### <a name="asynchronous-action"></a>비동기 작업

두 가지 가능한 반환 형식이 포함된 다음과 같은 비동기 작업을 사용합니다.

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.Pre21/Controllers/ProductsController.cs?name=snippet_CreateAsync&highlight=8,13)]

위의 작업에서 모델 유효성 검사에 실패하고 [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) 도우미 메서드를 호출할 때 400 상태 코드가 반환됩니다. 예를 들어 다음 모델은 요청이 `Name` 속성 및 값을 제공해야 함을 나타냅니다. 따라서 요청에서 적절한 `Name`을 제공하지 못하면 모델 유효성 검사에 실패합니다.

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.DataAccess/Models/Product.cs?name=snippet_ProductClass&highlight=5-6)]

이전 동작의 기타 알려진 반환 코드는 201이며 [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction) 도우미 메서드에서 생성합니다. 이 경로에 `Product` 개체가 반환됩니다.

::: moniker range=">= aspnetcore-2.1"
## <a name="actionresultt-type"></a>ActionResult\<T> 형식

ASP.NET Core 2.1은 Web API 컨트롤러 작업에 대해 [ActionResult\<T>](/dotnet/api/microsoft.aspnetcore.mvc.actionresult-1) 반환 형식을 소개합니다. [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult)에서 파생된 형식을 반환하거나 [특정 형식](#specific-type)을 반환할 수 있습니다. `ActionResult<T>`는 [IActionResult 형식](#iactionresult-type)을 통해 다음과 같은 혜택을 제공합니다.

* [[ProducesResponseType]](/dotnet/api/microsoft.aspnetcore.mvc.producesresponsetypeattribute) 특성의 `Type` 속성을 제외할 수 있습니다.
* [암시적 캐스트 연산자](/dotnet/csharp/language-reference/keywords/implicit)는 `T` 및 `ActionResult` 모두를 `ActionResult<T>`로 변환하도록 지원합니다. `T`는 [ObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.objectresult)로 변환합니다. 즉, `return new ObjectResult(T);`는 `return T;`로 간소화됩니다.

대부분의 작업에는 특정 반환 형식이 있습니다. 작업을 실행하는 동안 예기치 않은 조건이 발생할 수 있습니다. 이 경우에 특정 형식이 반환되지 않습니다. 예를 들어 작업의 입력 매개 변수는 모델 유효성 검사에 실패할 수 있습니다. 이러한 경우에 일반적으로 특정 형식이 아닌 적절한 `ActionResult` 형식을 반환합니다.

### <a name="synchronous-action"></a>동기화 작업

두 가지 가능한 반환 형식이 포함된 동기 작업을 사용합니다.

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_GetById&highlight=8,11)]

위의 코드에서 404 상태 코드는 제품이 데이터베이스에 존재하지 않는 경우에 반환됩니다. 제품이 없는 경우 해당하는 `Product` 개체가 반환됩니다. ASP.NET Core 2.1 이전에 `return product;` 줄은 `return Ok(product);`이었습니다.

> [!TIP]
> ASP.NET Core 2.1을 기준으로 작업 매개 변수 바인딩 원본 유추는 컨트롤러 클래스를 `[ApiController]` 특성으로 데코레이팅할 때 사용합니다. 경로 템플릿의 이름과 일치하는 매개 변수 이름은 요청 경로 데이터를 사용하여 자동으로 바인딩됩니다. 따라서 위 작업의 `id` 매개 변수가 [[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute) 특성을 사용하여 명시적으로 주석으로 추가되지 않습니다.

### <a name="asynchronous-action"></a>비동기 작업

두 가지 가능한 반환 형식이 포함된 비동기 작업을 사용합니다.

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_CreateAsync&highlight=8,13)]

모델 유효성 검사에 실패하는 경우 [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest#Microsoft_AspNetCore_Mvc_ControllerBase_BadRequest_Microsoft_AspNetCore_Mvc_ModelBinding_ModelStateDictionary_) 메서드를 호출하여 400 상태 코드를 반환합니다. 특정 유효성 검사 오류를 포함하는 [ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) 속성을 전달합니다. 모델 유효성 검사에 성공하는 경우 제품이 데이터베이스에서 만들어집니다. 201 상태 코드가 반환됩니다.

> [!TIP]
> ASP.NET Core 2.1을 기준으로 작업 매개 변수 바인딩 원본 유추는 컨트롤러 클래스를 `[ApiController]` 특성으로 데코레이팅할 때 사용합니다. 복합 형식 매개 변수는 요청 본문을 사용하여 자동으로 바인딩됩니다. 따라서 위 작업의 `product` 매개 변수가 [[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) 특성을 사용하여 명시적으로 주석으로 추가되지 않습니다.
::: moniker-end

## <a name="additional-resources"></a>추가 자료

* [컨트롤러 작업](xref:mvc/controllers/actions)
* [모델 유효성 검사](xref:mvc/models/validation)
* [Swagger를 사용한 Web API 도움말 페이지](xref:tutorials/web-api-help-pages-using-swagger)
