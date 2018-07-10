---
title: ASP.NET Core에서 Web API 빌드
author: scottaddie
description: ASP.NET Core에서 Web API를 빌드하는 데 사용할 수 있는 기능과 각 기능을 사용하기에 적합한 시기에 대해 알아봅니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 07/06/2018
uid: web-api/index
ms.openlocfilehash: 84e4a51a8a8ab031752ef054cba834bd202a4927
ms.sourcegitcommit: ea7ec8d47f94cfb8e008d771f647f86bbb4baa44
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37894217"
---
# <a name="build-web-apis-with-aspnet-core"></a>ASP.NET Core에서 Web API 빌드

작성자: [Scott Addie](https://github.com/scottaddie)

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

이 문서에서는 ASP.NET Core에서 Web API를 빌드하는 방법과 각 기능을 사용하기에 가장 적합한 시기에 대해 설명합니다.

## <a name="derive-class-from-controllerbase"></a>ControllerBase에서 클래스 파생

Web API를 제공할 목적으로 컨트롤의 [ControllerBase](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase) 클래스에서 상속합니다. 예:

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]

::: moniker-end

`ControllerBase` 클래스는 여러 속성 및 메서드에 대한 액세스를 제공합니다. 앞의 코드에서 예제에는 [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) 및 [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction)이 포함됩니다. 이러한 메서드는 각각 HTTP 400와 201 상태 코드를 반환하는 작업 메서드 내에서 호출됩니다. 요청 모델 유효성 검사를 처리하기 위해 `ControllerBase`에 의해서도 제공된 [ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) 속성에 액세스합니다.

::: moniker range=">= aspnetcore-2.1"

## <a name="annotate-class-with-apicontrollerattribute"></a>ApiControllerAttribute로 클래스에 주석 달기

ASP.NET Core 2.1에서는 Web API 컨트롤러 클래스를 나타내는 [[ApiController]](/dotnet/api/microsoft.aspnetcore.mvc.apicontrollerattribute) 특성을 소개합니다. 예:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]

[SetCompatibilityVersion](/dotnet/api/microsoft.extensions.dependencyinjection.mvccoremvcbuilderextensions.setcompatibilityversion)을 통해 설정된 호환성 버전 2.1 이상은 이 특성을 사용해야 합니다. 예를 들어 *Startup.ConfigureServices*에서 강조 표시된 코드는 2.1 호환성 플래그를 설정합니다.

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_SetCompatibilityVersion&highlight=2)]

`[ApiController]` 특성은 일반적으로 `ControllerBase`와 함께 컨트롤러에 대한 REST 특정 동작을 사용하도록 설정합니다. `ControllerBase`는 [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) 및 [File](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.file)과 같은 메서드에 대한 액세스를 제공합니다.

다른 방법은 `[ApiController]` 특성으로 주석 지정된 사용자 지정 기본 컨트롤러 클래스를 만드는 것입니다.

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]

다음 섹션에서는 특성으로 추가된 편리한 기능을 설명합니다.

### <a name="automatic-http-400-responses"></a>자동 HTTP 400 응답

유효성 검사 오류 시 HTTP 400 응답이 자동으로 트리거됩니다. 다음 코드는 실제 작업 시 불필요하게 됩니다.

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?range=46-49)]

[SuppressModelStateInvalidFilter](/dotnet/api/microsoft.aspnetcore.mvc.apibehavioroptions.suppressmodelstateinvalidfilter) 속성이 `true`로 설정된 경우 기본 동작이 사용되지 않습니다. `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 뒤에 *Startup.ConfigureServices*에서 다음 코드를 추가합니다.

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]

### <a name="binding-source-parameter-inference"></a>바인딩 소스 매개 변수 유추

바인딩 소스 특성은 작업 매개 변수 값이 발견되는 위치를 정의합니다. 다음 바인딩 소스 특성이 존재합니다.

|특성|바인딩 원본 |
|---------|---------|
|**[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute)**     | 요청 본문 |
|**[[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute)**     | 요청 본문에서 양식 데이터 |
|**[[FromHeader]](/dotnet/api/microsoft.aspnetcore.mvc.fromheaderattribute)** | 요청 헤더 |
|**[[FromQuery]](/dotnet/api/microsoft.aspnetcore.mvc.fromqueryattribute)**   | 요청 쿼리 문자열 매개 변수 |
|**[[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute)**   | 현재 요청의 경로 데이터 |
|**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)** | 작업 매개 변수로 삽입된 요청 서비스 |

> [!WARNING]
> 값에 `%2f`(즉, `/`)이 포함될 수 있는 경우 `[FromRoute]`를 사용하지 않습니다. `%2f`는 `/`로 이스케이프가 해제되지 않습니다. 값에 `%2f`가 포함될 수 있으면 `[FromQuery]`를 사용합니다.

`[ApiController]` 특성 없이, 바인딩 소스 특성이 명시적으로 정의됩니다. 다음 예제에서 `[FromQuery]` 특성은 `discontinuedOnly` 매개 변수 값이 요청 URL의 쿼리 문자열에 제공됨을 나타냅니다.

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=2)]

유추 규칙이 작업 매개 변수의 기본 데이터 원본에 대해 적용됩니다. 이러한 규칙은 작업 매개 변수에 달리 수동으로 적용할 가능성이 높은 바인딩 소스를 구성합니다. 바인딩 소스 특성은 다음과 같이 동작합니다.

* **[FromBody]** 는 복합 형식 매개 변수에 대해 유추됩니다. 이 규칙은 [IFormCollection](/dotnet/api/microsoft.aspnetcore.http.iformcollection) 및 [CancellationToken](/dotnet/api/system.threading.cancellationtoken)과 같이 특별한 의미를 지닌 복합 기본 제공 형식에는 적용되지 않습니다. 바인딩 소스 유추 코드는 이러한 특별한 형식을 무시합니다. 작업에 명시적으로 지정(`[FromBody]`를 통해)되거나 요청 본문의 바인딩으로 유추된 한 개를 초과하는 매개 변수가 있는 경우 예외가 throw됩니다. 예를 들어 다음 작업 서명으로 예외가 발생합니다.

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]

* **[FromForm]** 은 [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) 및 [IFormFileCollection](/dotnet/api/microsoft.aspnetcore.http.iformfilecollection) 형식의 작업 매개 변수에 대해 유추됩니다. 단순 또는 사용자 정의 형식에 대해서는 유추되지 않습니다.
* **[FromRoute]** 는 경로 템플릿에서 매개 변수와 일치하는 작업 매개 변수 이름에 대해 유추됩니다. 둘 이상의 경로가 작업 매개 변수와 일치하는 경우 모든 경로 값은 `[FromRoute]`로 간주됩니다.
* **[FromQuery]** 는 다른 작업 매개 변수에 대해 유추됩니다.

[SuppressInferBindingSourcesForParameters](/dotnet/api/microsoft.aspnetcore.mvc.apibehavioroptions.suppressinferbindingsourcesforparameters) 속성이 `true`로 설정되는 경우 기본 유추 규칙을 사용하지 않습니다. `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 뒤에 *Startup.ConfigureServices*에서 다음 코드를 추가합니다.

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]

### <a name="multipartform-data-request-inference"></a>다중 파트/폼 데이터 요청 유추

작업 매개 변수를 [[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute) 특성으로 주석 처리하는 경우 `multipart/form-data` 요청 콘텐츠 형식이 유추됩니다.

[SuppressConsumesConstraintForFormFileParameters](/dotnet/api/microsoft.aspnetcore.mvc.apibehavioroptions.suppressconsumesconstraintforformfileparameters) 속성이 `true`로 설정되는 경우 기본 동작이 사용되지 않습니다. `services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);` 뒤에 *Startup.ConfigureServices*에서 다음 코드를 추가합니다.

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]

### <a name="attribute-routing-requirement"></a>특성 라우팅 요구 사항

특성 라우팅은 요구 사항이 됩니다. 예:

[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]

작업은 [UseMvc](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvc#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvc_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Action_Microsoft_AspNetCore_Routing_IRouteBuilder__)에 정의된 [규칙 기반 경로](xref:mvc/controllers/routing#conventional-routing)를 통해 또는 *Startup.Configure*의 [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvcwithdefaultroute#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_)에 의해 액세스할 수 없습니다.

::: moniker-end

## <a name="additional-resources"></a>추가 자료

* <xref:web-api/action-return-types>
* <xref:web-api/advanced/custom-formatters>
* <xref:web-api/advanced/formatting>
* <xref:tutorials/web-api-help-pages-using-swagger>
* <xref:mvc/controllers/routing>
