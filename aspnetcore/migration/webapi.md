---
title: ASP.NET Web API에서에서 ASP.NET Core로 마이그레이션
author: ardalis
description: ASP.NET Core mvc 웹 API 구현 ASP.NET Web API에서 마이그레이션하는 방법에 알아봅니다.
ms.author: riande
ms.date: 05/10/2018
uid: migration/webapi
ms.openlocfilehash: 4f4dc140bd60463037be0757176dcf7a619918bd
ms.sourcegitcommit: 79b756ea03eae77a716f500ef88253ee9b1464d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36327511"
---
# <a name="migrate-from-aspnet-web-api-to-aspnet-core"></a>ASP.NET Web API에서에서 ASP.NET Core로 마이그레이션

작성자: [Steve Smith](https://ardalis.com/) 및 [Scott Addie](https://scottaddie.com)

웹 Api는 다양 한 브라우저 및 모바일 장치를 포함 한 클라이언트를 연결할 HTTP 서비스입니다. ASP.NET Core MVC 웹 응용 프로그램의 단일 방법을 제공 하는 Web Api 작성에 대 한 지원이 포함 되어 있습니다. 이 문서에서 ASP.NET Core mvc 웹 API 구현 ASP.NET Web API에서 마이그레이션하는 데 필요한 단계 보여 줍니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/webapi/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="review-aspnet-web-api-project"></a>ASP.NET Web API 프로젝트 검토

이 문서에서는 샘플 프로젝트 *ProductsApp*문서에서 만든 [ASP.NET Web API 2 시작](/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) 기준으로 합니다. 해당 프로젝트에서 간단한 ASP.NET 웹 API 프로젝트는 다음과 같이 구성 됩니다.

*Global.asax.cs*, 하도록 호출 `WebApiConfig.Register`:

[!code-csharp[](../migration/webapi/sample/ProductsApp/Global.asax.cs?highlight=14)]

`WebApiConfig` 에 정의 된 *App_Start*, 하나의 정적 있으며 `Register` 메서드:

[!code-csharp[](../migration/webapi/sample/ProductsApp/App_Start/WebApiConfig.cs?highlight=15,16,17,18,19,20)]


이 클래스를 구성 [특성 라우팅을](https://docs.microsoft.com/aspnet/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2)프로젝트에 사용 되 고 실제로 하지 않지만, 합니다. 또한 ASP.NET Web API에서 사용 되는 라우팅 테이블을 구성 합니다. 이 경우 ASP.NET Web API는 것을 예상 형식과 일치 하도록 Url */api/ {controller} / {id}* 와 *{id}* 선택 사항입니다.

*ProductsApp* 프로젝트에서 상속 하는 하나의 simple 컨트롤러에 `ApiController` 두 메서드를 노출 합니다.

[!code-csharp[](../migration/webapi/sample/ProductsApp/Controllers/ProductsController.cs?highlight=19,24)]

모델을 마지막으로, *제품*여는 데 사용 되는 *ProductsApp*, 간단한 클래스입니다.

[!code-csharp[](webapi/sample/ProductsApp/Models/Product.cs)]

시작 하는 간단한 프로젝트를 만들었으므로 이제 해당 ASP.NET Core mvc이 웹 API 프로젝트를 마이그레이션하는 방법에 보여줄 수 있습니다.

## <a name="create-the-destination-project"></a>대상 프로젝트 만들기

새로 만든 빈 솔루션을 만들려면 Visual Studio를 사용 하 고 이름을 *WebAPIMigration*합니다. 기존 항목 추가 *ProductsApp* 다음 프로젝트를 솔루션에 새 ASP.NET Core 웹 응용 프로그램 프로젝트를 추가 합니다. 새 프로젝트의 이름을 *ProductsCore*합니다.

![웹 서식 파일을 새 프로젝트 대화 상자를 엽니다.](webapi/_static/add-web-project.png)

웹 API 프로젝트 템플릿을 선택 합니다. 마이그레이션할 예정는 *ProductsApp* 이 새 프로젝트에 대 한 내용입니다.

![ASP.NET Core 템플릿 목록에서 선택한 웹 API 프로젝트 템플릿 사용 하 여 새 웹 응용 프로그램 대화 상자](webapi/_static/aspnet-5-webapi.png)

삭제 된 `Project_Readme.html` 새 프로젝트의 파일입니다. 솔루션은 이제 다음과 같이 표시 됩니다.

![응용 프로그램 솔루션 파일 및 ProductsApp 및 ProductsCore 프로젝트의 폴더를 나타내는 솔루션 탐색기에서 열기](webapi/_static/webapimigration-solution.png)

## <a name="migrate-configuration"></a>구성 마이그레이션

ASP.NET Core 더 이상 사용 되지 *Global.asax*, *web.config*, 또는 *App_Start* 폴더입니다. 모든 시작 작업을 수행 하는 대신, *Startup.cs* 프로젝트의 루트에 (참조 [응용 프로그램 시작](../fundamentals/startup.md)). ASP.NET Core MVC에서 라우팅 특성 기반 이제 기본적으로 포함 됩니다 때 `UseMvc()` 가 호출 되 고 이것은 웹 API 경로 구성 하는 데 권장 되는 방법 (이며 라우팅 Web API 시작 프로젝트를 처리 하는 방법).

[!code-csharp[](../migration/webapi/sample/ProductsCore/Startup.cs?highlight=31)]

특성 라우팅을 앞으로 프로젝트에 사용 하려는 경우 추가 구성이 필요 하지 않습니다. 샘플 에서처럼 컨트롤러 및 작업을 하는 데 필요한 특성을 적용 하기만 하면 `ValuesController` Web API 시작 프로젝트에 포함 된 클래스:

[!code-csharp[](../migration/webapi/sample/ProductsCore/Controllers/ValuesController.cs?highlight=9,13,20,27,33,39)]

있다는 사실에 주의 *[컨트롤러]* 8입니다. 이제 특성 기반 라우팅와 같은 특정 토큰, 지원 *[컨트롤러]* 및 *[작업]* 합니다. 이러한 토큰은 런타임에 교체 됨 컨트롤러 또는 동작의 이름으로 각각 특성이 적용 되었습니다. 프로젝트에서 매직 문자열의 수를 줄이기 위해이 처리 되 고 확인 하는 경로 동기화 되어야 해당 컨트롤러 및 작업 항목과 함께 자동 이름 바꾸기 리팩터링 적용 되는 경우.

제품 API 컨트롤러를 마이그레이션하려면에서는 먼저 복사 *ProductsController* 새 프로젝트에 있습니다. 단순히 컨트롤러에서 경로 특성을 포함 한 다음:

```csharp
[Route("api/[controller]")]
```

추가 해야는 `[HttpGet]` HTTP Get을 호출할 수는 모두 있으므로 두 개의 메서드 특성입니다. 에 대 한 특성에는 "id" 매개 변수를 기대 포함 `GetProduct()`:

```csharp
// /api/products
[HttpGet]
...

// /api/products/1
[HttpGet("{id}")]
```

이 시점에서 제대로 구성 되어 라우팅 그러나 해당 테스트 아직 없습니다. 추가 변경이 필요 하기 전에 *ProductsController* 컴파일됩니다.

## <a name="migrate-models-and-controllers"></a>모델 및 컨트롤러 마이그레이션

이 간단한 Web API 프로젝트에 대 한 마이그레이션 프로세스의 마지막 단계는 컨트롤러 및를 사용 하는 모델을 통해 복사 하는 것입니다. 이 경우 단순히 복사할 *Controllers/ProductsController.cs* 새로운 원래 프로젝트에서. 그런 다음 새로운 원래 프로젝트에서 전체 모델 폴더를 복사 합니다. 새 프로젝트 이름과 일치 하도록 네임 스페이스 조정 (*ProductsCore*).  이 시점에서 응용 프로그램을 빌드하고 컴파일 오류의 수 있습니다. 일반적으로 다음 범주에 속해 있어야 합니다. 이러한:

* *ApiController* 존재 하지 않는

* *System.Web.Http* 네임 스페이스가 없습니다.

* *IHttpActionResult* 존재 하지 않는

다행히 이들은 모두를 쉽게 해결 합니다.

* 변경 *ApiController* 를 *컨트롤러* (추가 해야 할 수도 *Microsoft.AspNetCore.Mvc를 사용 하 여*)

* 삭제를 참조 하는 문을 사용 하 여 *System.Web.Http*

* 반환 하는 모든 메서드에 변경 *IHttpActionResult* 반환 하는 *IActionResult*

이러한 변경에 수행 하 고 사용 하지 않는 된 문을 사용 하 여 면 제거 마이그레이션된 *ProductsController* 클래스는 다음과 같습니다.

[!code-csharp[](../migration/webapi/sample/ProductsCore/Controllers/ProductsController.cs?highlight=1,2,6,8,9,27)]

마이그레이션된 프로젝트를 실행 하 고를 이제 있어야 */api/제품*; 및 3 제품의 전체 목록을 표시 되어야 합니다. 찾아 */api/products/1* 첫 번째 제품 표시 되어야 합니다.

## <a name="microsoftaspnetcoremvcwebapicompatshim"></a>Microsoft.AspNetCore.Mvc.WebApiCompatShim

ASP.NET Core 마이그레이션 ASP.NET Web API 프로젝트 때 유용한 도구는는 [Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) 라이브러리입니다. 호환성 shim 다양 한 다른 Web API 2 사용할 규칙을 허용 하도록 ASP.NET Core를 확장 합니다. 이 문서에서 이전에 이식 샘플은 기본 충분히 호환성 shim 필요 없습니다. 대규모 프로젝트 호환성 shim을 사용 하 여 가능 일시적으로 ASP.NET Core 및 ASP.NET Web API 2 간의 API 차이 조정 하는 데 유용 합니다.

웹 API 호환성 shim ASP.NET Core로 큰 웹 API 프로젝트 마이그레이션 용이 하 게 임시 측정값으로 사용할 것입니다. 시간이 지남에 따라 프로젝트 호환성 shim에 의존 하지 않고 ASP.NET Core 패턴을 사용 하도록 업데이트 되어야 합니다. 

Microsoft.AspNetCore.Mvc.WebApiCompatShim에 포함 된 호환성 기능은 다음과 같습니다.

* 추가 `ApiController` 을 입력 하 여 컨트롤러의 기본 형식 업데이트할 필요가 없습니다.
* 웹 API 스타일 모델 바인딩을 활성화합니다. ASP.NET Core MVC 모델 바인딩 비슷하게 작동 기본적으로 MVC 5입니다. 호환성 shim 변경 모델 바인딩을 유사한 Web API 2 모델 바인딩 규칙을 준수 해야 합니다. 예를 들어 복합 형식은 자동으로 요청 본문에서 바인딩됩니다.
* 컨트롤러 동작의 형식 매개 변수를 사용할 수 있도록 모델 바인딩 확장 `HttpRequestMessage`합니다.
* 추가 하는 형식의 결과를 반환할 작업 수 있도록 메시지 포맷터 `HttpResponseMessage`합니다.
* Web API 2 작업 응답을 제공 하도록 사용 했을 수 있는 추가 응답 메서드를 추가 합니다.
    * HttpResponseMessage 생성기:
        * `CreateResponse<T>`
        * `CreateErrorResponse`
    * 작업 결과 메서드:
        * `BadRequestErrorMessageResult`
        * `ExceptionResult`
        * `InternalServerErrorResult`
        * `InvalidModelStateResult`
        * `NegotiatedContentResult`
        * `ResponseMessageResult`
* 인스턴스를 추가 `IContentNegotiator` 응용 프로그램의 DI 컨테이너에는 콘텐츠 협상 관련 형식에서 및 [Microsoft.AspNet.WebApi.Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) 사용할 수 있습니다. 에 같은 `DefaultContentNegotiator`, `MediaTypeFormatter`등입니다.

호환성 shim을 사용 하려면:

* 참조는 [Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) NuGet 패키지 합니다.
* 호환성 shim 서비스를 호출 하 여 응용 프로그램의 DI 컨테이너와 등록 `services.AddWebApiConventions()` 응용 프로그램의 `Startup.ConfigureServices` 메서드.
* 웹 API 관련 경로 사용 하 여 정의 `MapWebApiRoute` 에 `IRouteBuilder` 응용 프로그램의 `IApplicationBuilder.UseMvc` 호출 합니다.

## <a name="summary"></a>요약

ASP.NET Core mvc 간단한 ASP.NET 웹 API 프로젝트를 마이그레이션하는 매우 간단 고마워요 ASP.NET Core MVC의 웹 Api에 대 한 기본 제공 지원으로 합니다. 모든 ASP.NET Web API 프로젝트는 마이그레이션해야 할 주요 작업은 경로, 컨트롤러 및 컨트롤러 및 작업에서 사용 되는 형식에 대 한 업데이트와 함께 모델입니다.
