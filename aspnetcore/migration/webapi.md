---
title: ASP.NET Core에 ASP.NET Web API에서 마이그레이션
author: ardalis
description: ASP.NET Core MVC로 웹 API 구현 ASP.NET Web API에서 마이그레이션하는 방법에 알아봅니다.
ms.author: riande
ms.date: 05/10/2018
uid: migration/webapi
ms.openlocfilehash: 8dd969c8644525606227989ca87e41fbfae5aed1
ms.sourcegitcommit: ea7ec8d47f94cfb8e008d771f647f86bbb4baa44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37894194"
---
# <a name="migrate-from-aspnet-web-api-to-aspnet-core"></a>ASP.NET Core에 ASP.NET Web API에서 마이그레이션

작성자: [Steve Smith](https://ardalis.com/) 및 [Scott Addie](https://scottaddie.com)

Web Api는 HTTP 서비스는 광범위 한 브라우저 및 모바일 장치를 비롯 한 클라이언트 연결입니다. ASP.NET Core MVC 웹 응용 프로그램을 구축 하는 단일 하 고 일관 된 방법을 제공 하는 웹 Api를 구축 하는 것에 대 한 지원이 포함 됩니다. 이 문서에서는 ASP.NET Core MVC로 웹 API 구현 ASP.NET Web API에서 마이그레이션하는 데 필요한 단계를 보여 줍니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/webapi/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="review-aspnet-web-api-project"></a>ASP.NET Web API 프로젝트 검토

이 문서에서는 샘플 프로젝트 *ProductsApp*문서에서 만든 [ASP.NET Web API 2 시작](/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) 시작 지점으로 합니다. 해당 프로젝트에 간단한 ASP.NET Web API 프로젝트는 다음과 같이 구성 됩니다.

*Global.asax.cs*를 호출 하려고 `WebApiConfig.Register`:

[!code-csharp[](../migration/webapi/sample/ProductsApp/Global.asax.cs?highlight=14)]

`WebApiConfig` 에 정의 된 *App_Start*, 있고 하나의 정적 `Register` 메서드:

[!code-csharp[](../migration/webapi/sample/ProductsApp/App_Start/WebApiConfig.cs?highlight=15,16,17,18,19,20)]

이 클래스를 구성 [특성 라우팅은](/aspnet/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2)이지만 프로젝트에 실제로 사용 되는 합니다. 또한 ASP.NET Web API에서 사용 되는 라우팅 테이블을 구성 합니다. ASP.NET Web API가 형식과 일치 하도록 Url을 예상 하는 예에서 */api/ {컨트롤러} / {id}* 를 사용 하 여 *{id}* 선택 사항입니다.

합니다 *ProductsApp* 프로젝트 포함에서 상속 하는 하나의 simple 컨트롤러 `ApiController` 두 메서드를 노출:

[!code-csharp[](../migration/webapi/sample/ProductsApp/Controllers/ProductsController.cs?highlight=19,24)]

마지막으로 모델을 *제품*는 데 사용 합니다 *ProductsApp*, 단순 클래스:

[!code-csharp[](webapi/sample/ProductsApp/Models/Product.cs)]

시작 하는 간단한 프로젝트를 만들었으므로에서는 수이 Web API 프로젝트를 ASP.NET Core MVC로 마이그레이션하는 방법을 설명 합니다.

## <a name="create-the-destination-project"></a>대상 프로젝트를 만들려면

새로 만든 빈 솔루션을 만들려면 Visual Studio를 사용 하 고 이름을 *WebAPIMigration*합니다. 기존 항목 추가 *ProductsApp* , 프로젝트를 솔루션에 새 ASP.NET Core 웹 응용 프로그램 프로젝트를 추가 합니다. 새 프로젝트의 이름을 *ProductsCore*합니다.

![웹 템플릿에 새 프로젝트 대화 상자 열기](webapi/_static/add-web-project.png)

다음으로, 웹 API 프로젝트 템플릿을 선택 합니다. 마이그레이션할 예정 합니다 *ProductsApp* 이 새 프로젝트에 대 한 내용입니다.

![ASP.NET Core 템플릿 목록에서 선택 하는 Web API 프로젝트 템플릿 사용 하 여 새 웹 응용 프로그램 대화 상자](webapi/_static/aspnet-5-webapi.png)

삭제 된 `Project_Readme.html` 새 프로젝트의 파일입니다. 이제 다음과 같은 경우에 솔루션이 표시 됩니다.

![응용 프로그램 솔루션 파일 및 ProductsApp 및 ProductsCore 프로젝트의 폴더를 보여 주는 솔루션 탐색기에서 열기](webapi/_static/webapimigration-solution.png)

## <a name="migrate-configuration"></a>구성 마이그레이션

ASP.NET Core 더 이상 사용 하지 *Global.asax*를 *web.config*, 또는 *App_Start* 폴더입니다. 모든 시작 작업을 수행 하는 대신 *Startup.cs* 프로젝트의 루트에 (참조 [응용 프로그램 시작](../fundamentals/startup.md)). ASP.NET Core mvc에서 특성 기반 라우팅은 이제 기본적으로 포함 된 경우 `UseMvc()` 가 호출 되 고,이 웹 API 경로 구성 하는 데 권장 되는 방법 (Web API 시작 프로젝트에는 라우팅을 처리 하는 방법).

[!code-csharp[](../migration/webapi/sample/ProductsCore/Startup.cs?highlight=31)]

앞으로 프로젝트에서 특성 라우팅을 사용 하 려 한다고 가정 하므로, 추가 구성이 필요 하지 않습니다. 이 샘플에서와 같이 컨트롤러 및 작업을 필요에 따라 특성을 적용 하기만 하면 `ValuesController` Web API 시작 프로젝트에 포함 된 클래스:

[!code-csharp[](../migration/webapi/sample/ProductsCore/Controllers/ValuesController.cs?highlight=9,13,20,27,33,39)]

있다는 사실에 주의 *[컨트롤러]* 8 줄에서. 와 같은 특정 토큰, 지원 이제 특성 기반 라우팅은 *[컨트롤러]* 하 고 *[action]* 합니다. 이러한 토큰 바뀝니다 런타임에 컨트롤러 또는 작업의 이름으로 각각 특성이 적용 되었습니다. 이 프로젝트에서 매직 문자열의 수를 줄이는 역할 및 경로 동기화 되어야 해당 컨트롤러와 작업을 사용 하 여 자동 이름 바꾸기 리팩터링 적용 될 때 확인 합니다.

제품 API 컨트롤러를 마이그레이션하려면에서는 먼저 복사 해야 합니다 *ProductsController* 새 프로젝트에 있습니다. 다음 컨트롤러에서 경로 특성을 포함 하기만 하면 됩니다.

```csharp
[Route("api/[controller]")]
```

추가 해야 합니다 `[HttpGet]` 모두를 HTTP Get을 통해 호출 해야 하므로 두 개의 메서드 특성입니다. "Id" 매개 변수를 기대에 대 한 특성에 포함할 `GetProduct()`:

```csharp
// /api/products
[HttpGet]
...

// /api/products/1
[HttpGet("{id}")]
```

이 시점에서 제대로 구성 된 라우팅 그러나 것 수 없습니다. 아직 테스트 합니다. 추가 변경 해야 하기 전에 *ProductsController* 컴파일됩니다.

## <a name="migrate-models-and-controllers"></a>모델 및 컨트롤러를 마이그레이션

이 간단한 Web API 프로젝트에 대 한 마이그레이션 프로세스의 마지막 단계는 컨트롤러 및 모든 모델을 사용 하 여 복사 하는 것입니다. 이 경우 단순히 복사 *Controllers/ProductsController.cs* 새 원래 프로젝트에서. 그런 다음 새 원래 프로젝트에서 전체 모델 폴더를 복사 합니다. 새 프로젝트 이름과 일치 하도록 네임 스페이스를 조정 (*ProductsCore*).  이 시점에서 응용 프로그램을 빌드하고 컴파일 오류를 수 있습니다. 이 일반적으로 다음 범주로 구분 됩니다.

* *ApiController* 없는 경우

* *System.Web.Http* 네임 스페이스가 없습니다.

* *IHttpActionResult* 없는 경우

다행 스럽게도 이들은 모두를 쉽게 해결 합니다.

* 변경 *ApiController* 하 *컨트롤러* (추가 해야 *Microsoft.AspNetCore.Mvc를 사용 하 여*)

* 삭제를 참조 하는 문을 사용 하 여 *System.Web.Http*

* 반환 하는 모든 메서드에 변경할 *IHttpActionResult* 반환할는 *IActionResult*

수행 하 고 사용 되지 않는 이러한 변경 된 후 문을 사용 하 여 제거 마이그레이션된 *ProductsController* 클래스는 다음과 같습니다.

[!code-csharp[](../migration/webapi/sample/ProductsCore/Controllers/ProductsController.cs?highlight=1,2,6,8,9,27)]

이제 마이그레이션된 프로젝트를 실행 하 여 이동할 수 있어야 */api/제품*; 및 3 제품의 전체 목록을 표시 합니다. 이동할 */api/products/1* 첫 번째 제품 표시 되어야 합니다.

## <a name="aspnet-4x-web-api-2-compatibility-shim"></a>ASP.NET Web API 2 4.x 호환성 shim

ASP.NET Core로 마이그레이션 ASP.NET Web API 프로젝트 때 유용한 도구는 합니다 [Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) 라이브러리입니다. 호환성 shim의 다양 한 Web API 2 규칙이 사용할 수 있도록 ASP.NET Core를 확장 합니다. 이 문서에서는 이전에 이식 샘플은 기본 충분히 호환성 shim 필요 없습니다. 대규모 프로젝트 호환성 shim을 사용 하 여 가능 일시적으로 ASP.NET Core 및 ASP.NET Web API 2 사이의 API 차이 조정 하는 데 유용 합니다.

Web API 호환성 shim은 ASP.NET core Web API 프로젝트를 마이그레이션 큰를 용이 하 게 임시 수단으로 사용할 것입니다. 시간이 지남에 따라 프로젝트 호환성 shim에 의존 하지 않고 ASP.NET Core 패턴을 사용 하도록 업데이트 되어야 합니다.

에 포함 된 호환성 기능 `Microsoft.AspNetCore.Mvc.WebApiCompatShim` 포함:

* 추가 `ApiController` 을 입력 하 여 컨트롤러의 기본 형식 업데이트할 필요가 없습니다.
* 웹 API 스타일 모델 바인딩을 활성화합니다. ASP.NET Core MVC는 MVC 5의 경우와 유사 하 게 바인딩 함수 기본적으로 모델입니다. 호환성 shim 변경 모델 바인딩 Web API 2 모델 바인딩 규칙 더 유사 합니다. 예를 들어, 복합 형식은 자동으로 요청 본문에서 바인딩됩니다.
* 컨트롤러 작업의 형식 매개 변수를 취할 수 있도록 모델 바인딩 확장 `HttpRequestMessage`합니다.
* 형식의 결과 반환할 작업을 허용 메시지 포맷터를 추가 `HttpResponseMessage`합니다.
* Web API 2 작업 응답에 맞도록 사용 했을 수 있는 추가 응답 메서드를 추가 합니다.
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
* 인스턴스를 추가 `IContentNegotiator` 앱의 DI 컨테이너에는 콘텐츠 협상 관련 형식에서 [Microsoft.AspNet.WebApi.Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) 사용할 수 있습니다. 같은 형식이 포함 됩니다 `DefaultContentNegotiator`, `MediaTypeFormatter`등입니다.

호환성 shim을 사용 하려면를 지정 해야 합니다.

* 설치 합니다 [Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) NuGet 패키지.
* 호환성 shim의 서비스를 호출 하 여 앱의 DI 컨테이너를 사용 하 여 등록 `services.AddMvc().AddWebApiConventions()` 앱의 `Startup.ConfigureServices` 메서드.
* 사용 하 여 웹 API 관련 경로 정의 `MapWebApiRoute` 에 `IRouteBuilder` 앱의 `IApplicationBuilder.UseMvc` 호출 합니다.

## <a name="summary"></a>요약

간단한 ASP.NET Web API 프로젝트를 ASP.NET Core MVC로 마이그레이션가 상당히 간단한 감사 ASP.NET Core MVC에서 Web Api에 대 한 기본 제공 지원. 모든 ASP.NET Web API 프로젝트를 마이그레이션해야 할 중요 한 부분은 경로, 컨트롤러 및 모델, 컨트롤러 및 작업에 의해 사용 되는 형식으로 업데이트 됩니다.
