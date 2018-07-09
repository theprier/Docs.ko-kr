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
# <a name="migrate-from-aspnet-web-api-to-aspnet-core"></a><span data-ttu-id="fb570-103">ASP.NET Core에 ASP.NET Web API에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="fb570-103">Migrate from ASP.NET Web API to ASP.NET Core</span></span>

<span data-ttu-id="fb570-104">작성자: [Steve Smith](https://ardalis.com/) 및 [Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="fb570-104">By [Steve Smith](https://ardalis.com/) and [Scott Addie](https://scottaddie.com)</span></span>

<span data-ttu-id="fb570-105">Web Api는 HTTP 서비스는 광범위 한 브라우저 및 모바일 장치를 비롯 한 클라이언트 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-105">Web APIs are HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="fb570-106">ASP.NET Core MVC 웹 응용 프로그램을 구축 하는 단일 하 고 일관 된 방법을 제공 하는 웹 Api를 구축 하는 것에 대 한 지원이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-106">ASP.NET Core MVC includes support for building Web APIs providing a single, consistent way of building web applications.</span></span> <span data-ttu-id="fb570-107">이 문서에서는 ASP.NET Core MVC로 웹 API 구현 ASP.NET Web API에서 마이그레이션하는 데 필요한 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-107">In this article, we demonstrate the steps required to migrate a Web API implementation from ASP.NET Web API to ASP.NET Core MVC.</span></span>

<span data-ttu-id="fb570-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/webapi/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="fb570-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/webapi/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="review-aspnet-web-api-project"></a><span data-ttu-id="fb570-109">ASP.NET Web API 프로젝트 검토</span><span class="sxs-lookup"><span data-stu-id="fb570-109">Review ASP.NET Web API project</span></span>

<span data-ttu-id="fb570-110">이 문서에서는 샘플 프로젝트 *ProductsApp*문서에서 만든 [ASP.NET Web API 2 시작](/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) 시작 지점으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-110">This article uses the sample project, *ProductsApp*, created in the article [Getting Started with ASP.NET Web API 2](/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) as its starting point.</span></span> <span data-ttu-id="fb570-111">해당 프로젝트에 간단한 ASP.NET Web API 프로젝트는 다음과 같이 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-111">In that project, a simple ASP.NET Web API  project is configured as follows.</span></span>

<span data-ttu-id="fb570-112">*Global.asax.cs*를 호출 하려고 `WebApiConfig.Register`:</span><span class="sxs-lookup"><span data-stu-id="fb570-112">In *Global.asax.cs*, a call is made to `WebApiConfig.Register`:</span></span>

[!code-csharp[](../migration/webapi/sample/ProductsApp/Global.asax.cs?highlight=14)]

<span data-ttu-id="fb570-113">`WebApiConfig` 에 정의 된 *App_Start*, 있고 하나의 정적 `Register` 메서드:</span><span class="sxs-lookup"><span data-stu-id="fb570-113">`WebApiConfig` is defined in *App_Start*, and has just one static `Register` method:</span></span>

[!code-csharp[](../migration/webapi/sample/ProductsApp/App_Start/WebApiConfig.cs?highlight=15,16,17,18,19,20)]

<span data-ttu-id="fb570-114">이 클래스를 구성 [특성 라우팅은](/aspnet/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2)이지만 프로젝트에 실제로 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-114">This class configures [attribute routing](/aspnet/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2), although it's not actually being used in the project.</span></span> <span data-ttu-id="fb570-115">또한 ASP.NET Web API에서 사용 되는 라우팅 테이블을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-115">It also configures the routing table, which is used by ASP.NET Web API.</span></span> <span data-ttu-id="fb570-116">ASP.NET Web API가 형식과 일치 하도록 Url을 예상 하는 예에서 */api/ {컨트롤러} / {id}* 를 사용 하 여 *{id}* 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-116">In this case, ASP.NET Web API will expect URLs to match the format */api/{controller}/{id}*, with *{id}* being optional.</span></span>

<span data-ttu-id="fb570-117">합니다 *ProductsApp* 프로젝트 포함에서 상속 하는 하나의 simple 컨트롤러 `ApiController` 두 메서드를 노출:</span><span class="sxs-lookup"><span data-stu-id="fb570-117">The *ProductsApp* project includes just one simple controller, which inherits from `ApiController` and exposes two methods:</span></span>

[!code-csharp[](../migration/webapi/sample/ProductsApp/Controllers/ProductsController.cs?highlight=19,24)]

<span data-ttu-id="fb570-118">마지막으로 모델을 *제품*는 데 사용 합니다 *ProductsApp*, 단순 클래스:</span><span class="sxs-lookup"><span data-stu-id="fb570-118">Finally, the model, *Product*, used by the *ProductsApp*, is a simple class:</span></span>

[!code-csharp[](webapi/sample/ProductsApp/Models/Product.cs)]

<span data-ttu-id="fb570-119">시작 하는 간단한 프로젝트를 만들었으므로에서는 수이 Web API 프로젝트를 ASP.NET Core MVC로 마이그레이션하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-119">Now that we have a simple project from which to start, we can demonstrate how to migrate this Web API project to ASP.NET Core MVC.</span></span>

## <a name="create-the-destination-project"></a><span data-ttu-id="fb570-120">대상 프로젝트를 만들려면</span><span class="sxs-lookup"><span data-stu-id="fb570-120">Create the Destination Project</span></span>

<span data-ttu-id="fb570-121">새로 만든 빈 솔루션을 만들려면 Visual Studio를 사용 하 고 이름을 *WebAPIMigration*합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-121">Using Visual Studio, create a new, empty solution, and name it *WebAPIMigration*.</span></span> <span data-ttu-id="fb570-122">기존 항목 추가 *ProductsApp* , 프로젝트를 솔루션에 새 ASP.NET Core 웹 응용 프로그램 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-122">Add the existing *ProductsApp* project to it, then, add a new ASP.NET Core Web Application Project to the solution.</span></span> <span data-ttu-id="fb570-123">새 프로젝트의 이름을 *ProductsCore*합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-123">Name the new project *ProductsCore*.</span></span>

![웹 템플릿에 새 프로젝트 대화 상자 열기](webapi/_static/add-web-project.png)

<span data-ttu-id="fb570-125">다음으로, 웹 API 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-125">Next, choose the Web API project template.</span></span> <span data-ttu-id="fb570-126">마이그레이션할 예정 합니다 *ProductsApp* 이 새 프로젝트에 대 한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-126">We will migrate the *ProductsApp* contents to this new project.</span></span>

![ASP.NET Core 템플릿 목록에서 선택 하는 Web API 프로젝트 템플릿 사용 하 여 새 웹 응용 프로그램 대화 상자](webapi/_static/aspnet-5-webapi.png)

<span data-ttu-id="fb570-128">삭제 된 `Project_Readme.html` 새 프로젝트의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-128">Delete the `Project_Readme.html` file from the new project.</span></span> <span data-ttu-id="fb570-129">이제 다음과 같은 경우에 솔루션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-129">Your solution should now look like this:</span></span>

![응용 프로그램 솔루션 파일 및 ProductsApp 및 ProductsCore 프로젝트의 폴더를 보여 주는 솔루션 탐색기에서 열기](webapi/_static/webapimigration-solution.png)

## <a name="migrate-configuration"></a><span data-ttu-id="fb570-131">구성 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="fb570-131">Migrate Configuration</span></span>

<span data-ttu-id="fb570-132">ASP.NET Core 더 이상 사용 하지 *Global.asax*를 *web.config*, 또는 *App_Start* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-132">ASP.NET Core no longer uses *Global.asax*, *web.config*, or *App_Start* folders.</span></span> <span data-ttu-id="fb570-133">모든 시작 작업을 수행 하는 대신 *Startup.cs* 프로젝트의 루트에 (참조 [응용 프로그램 시작](../fundamentals/startup.md)).</span><span class="sxs-lookup"><span data-stu-id="fb570-133">Instead, all startup tasks are done in *Startup.cs* in the root of the project (see [Application Startup](../fundamentals/startup.md)).</span></span> <span data-ttu-id="fb570-134">ASP.NET Core mvc에서 특성 기반 라우팅은 이제 기본적으로 포함 된 경우 `UseMvc()` 가 호출 되 고,이 웹 API 경로 구성 하는 데 권장 되는 방법 (Web API 시작 프로젝트에는 라우팅을 처리 하는 방법).</span><span class="sxs-lookup"><span data-stu-id="fb570-134">In ASP.NET Core MVC, attribute-based routing is now included by default when `UseMvc()` is called; and, this is the recommended approach for configuring Web API routes (and is how the Web API starter project handles routing).</span></span>

[!code-csharp[](../migration/webapi/sample/ProductsCore/Startup.cs?highlight=31)]

<span data-ttu-id="fb570-135">앞으로 프로젝트에서 특성 라우팅을 사용 하 려 한다고 가정 하므로, 추가 구성이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-135">Assuming you want to use attribute routing in your project going forward, no additional configuration is needed.</span></span> <span data-ttu-id="fb570-136">이 샘플에서와 같이 컨트롤러 및 작업을 필요에 따라 특성을 적용 하기만 하면 `ValuesController` Web API 시작 프로젝트에 포함 된 클래스:</span><span class="sxs-lookup"><span data-stu-id="fb570-136">Simply apply the attributes as needed to your controllers and actions, as is done in the sample `ValuesController` class that's included in the Web API starter project:</span></span>

[!code-csharp[](../migration/webapi/sample/ProductsCore/Controllers/ValuesController.cs?highlight=9,13,20,27,33,39)]

<span data-ttu-id="fb570-137">있다는 사실에 주의 *[컨트롤러]* 8 줄에서.</span><span class="sxs-lookup"><span data-stu-id="fb570-137">Note the presence of *[controller]* on line 8.</span></span> <span data-ttu-id="fb570-138">와 같은 특정 토큰, 지원 이제 특성 기반 라우팅은 *[컨트롤러]* 하 고 *[action]* 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-138">Attribute-based routing now supports certain tokens, such as *[controller]* and *[action]*.</span></span> <span data-ttu-id="fb570-139">이러한 토큰 바뀝니다 런타임에 컨트롤러 또는 작업의 이름으로 각각 특성이 적용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-139">These tokens are replaced at runtime with the name of the controller or action, respectively, to which the attribute has been applied.</span></span> <span data-ttu-id="fb570-140">이 프로젝트에서 매직 문자열의 수를 줄이는 역할 및 경로 동기화 되어야 해당 컨트롤러와 작업을 사용 하 여 자동 이름 바꾸기 리팩터링 적용 될 때 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-140">This serves to reduce the number of magic strings in the project, and it ensures the routes will be kept synchronized with their corresponding controllers and actions when automatic rename refactorings are applied.</span></span>

<span data-ttu-id="fb570-141">제품 API 컨트롤러를 마이그레이션하려면에서는 먼저 복사 해야 합니다 *ProductsController* 새 프로젝트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-141">To migrate the Products API controller, we must first copy *ProductsController* to the new project.</span></span> <span data-ttu-id="fb570-142">다음 컨트롤러에서 경로 특성을 포함 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-142">Then simply include the route attribute on the controller:</span></span>

```csharp
[Route("api/[controller]")]
```

<span data-ttu-id="fb570-143">추가 해야 합니다 `[HttpGet]` 모두를 HTTP Get을 통해 호출 해야 하므로 두 개의 메서드 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-143">You also need to add the `[HttpGet]` attribute to the two methods, since they both should be called via HTTP Get.</span></span> <span data-ttu-id="fb570-144">"Id" 매개 변수를 기대에 대 한 특성에 포함할 `GetProduct()`:</span><span class="sxs-lookup"><span data-stu-id="fb570-144">Include the expectation of an "id" parameter in the attribute for `GetProduct()`:</span></span>

```csharp
// /api/products
[HttpGet]
...

// /api/products/1
[HttpGet("{id}")]
```

<span data-ttu-id="fb570-145">이 시점에서 제대로 구성 된 라우팅 그러나 것 수 없습니다. 아직 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-145">At this point, routing is configured correctly; however, we can't yet test it.</span></span> <span data-ttu-id="fb570-146">추가 변경 해야 하기 전에 *ProductsController* 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-146">Additional changes must be made before *ProductsController* will compile.</span></span>

## <a name="migrate-models-and-controllers"></a><span data-ttu-id="fb570-147">모델 및 컨트롤러를 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="fb570-147">Migrate Models and Controllers</span></span>

<span data-ttu-id="fb570-148">이 간단한 Web API 프로젝트에 대 한 마이그레이션 프로세스의 마지막 단계는 컨트롤러 및 모든 모델을 사용 하 여 복사 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-148">The last step in the migration process for this simple Web API project is to copy over the Controllers and any Models they use.</span></span> <span data-ttu-id="fb570-149">이 경우 단순히 복사 *Controllers/ProductsController.cs* 새 원래 프로젝트에서.</span><span class="sxs-lookup"><span data-stu-id="fb570-149">In this case, simply copy *Controllers/ProductsController.cs* from the original project to the new one.</span></span> <span data-ttu-id="fb570-150">그런 다음 새 원래 프로젝트에서 전체 모델 폴더를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-150">Then, copy the entire Models folder from the original project to the new one.</span></span> <span data-ttu-id="fb570-151">새 프로젝트 이름과 일치 하도록 네임 스페이스를 조정 (*ProductsCore*).</span><span class="sxs-lookup"><span data-stu-id="fb570-151">Adjust the namespaces to match the new project name (*ProductsCore*).</span></span>  <span data-ttu-id="fb570-152">이 시점에서 응용 프로그램을 빌드하고 컴파일 오류를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-152">At this point, you can build the application, and you will find a number of compilation errors.</span></span> <span data-ttu-id="fb570-153">이 일반적으로 다음 범주로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-153">These should generally fall into the following categories:</span></span>

* <span data-ttu-id="fb570-154">*ApiController* 없는 경우</span><span class="sxs-lookup"><span data-stu-id="fb570-154">*ApiController* does not exist</span></span>

* <span data-ttu-id="fb570-155">*System.Web.Http* 네임 스페이스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-155">*System.Web.Http* namespace does not exist</span></span>

* <span data-ttu-id="fb570-156">*IHttpActionResult* 없는 경우</span><span class="sxs-lookup"><span data-stu-id="fb570-156">*IHttpActionResult* does not exist</span></span>

<span data-ttu-id="fb570-157">다행 스럽게도 이들은 모두를 쉽게 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-157">Fortunately, these are all very easy to correct:</span></span>

* <span data-ttu-id="fb570-158">변경 *ApiController* 하 *컨트롤러* (추가 해야 *Microsoft.AspNetCore.Mvc를 사용 하 여*)</span><span class="sxs-lookup"><span data-stu-id="fb570-158">Change *ApiController* to *Controller* (you may need to add *using Microsoft.AspNetCore.Mvc*)</span></span>

* <span data-ttu-id="fb570-159">삭제를 참조 하는 문을 사용 하 여 *System.Web.Http*</span><span class="sxs-lookup"><span data-stu-id="fb570-159">Delete any using statement referring to *System.Web.Http*</span></span>

* <span data-ttu-id="fb570-160">반환 하는 모든 메서드에 변경할 *IHttpActionResult* 반환할는 *IActionResult*</span><span class="sxs-lookup"><span data-stu-id="fb570-160">Change any method returning *IHttpActionResult* to return a *IActionResult*</span></span>

<span data-ttu-id="fb570-161">수행 하 고 사용 되지 않는 이러한 변경 된 후 문을 사용 하 여 제거 마이그레이션된 *ProductsController* 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-161">Once these changes have been made and unused using statements removed, the migrated *ProductsController* class looks like this:</span></span>

[!code-csharp[](../migration/webapi/sample/ProductsCore/Controllers/ProductsController.cs?highlight=1,2,6,8,9,27)]

<span data-ttu-id="fb570-162">이제 마이그레이션된 프로젝트를 실행 하 여 이동할 수 있어야 */api/제품*; 및 3 제품의 전체 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-162">You should now be able to run the migrated project and browse to */api/products*; and, you should see the full list of 3 products.</span></span> <span data-ttu-id="fb570-163">이동할 */api/products/1* 첫 번째 제품 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-163">Browse to */api/products/1* and you should see the first product.</span></span>

## <a name="aspnet-4x-web-api-2-compatibility-shim"></a><span data-ttu-id="fb570-164">ASP.NET Web API 2 4.x 호환성 shim</span><span class="sxs-lookup"><span data-stu-id="fb570-164">ASP.NET 4.x Web API 2 compatibility shim</span></span>

<span data-ttu-id="fb570-165">ASP.NET Core로 마이그레이션 ASP.NET Web API 프로젝트 때 유용한 도구는 합니다 [Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-165">A useful tool when migrating ASP.NET Web API projects to ASP.NET Core is the [Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) library.</span></span> <span data-ttu-id="fb570-166">호환성 shim의 다양 한 Web API 2 규칙이 사용할 수 있도록 ASP.NET Core를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-166">The compatibility shim extends ASP.NET Core to allow a number of different Web API 2 conventions to be used.</span></span> <span data-ttu-id="fb570-167">이 문서에서는 이전에 이식 샘플은 기본 충분히 호환성 shim 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-167">The sample ported previously in this document is basic enough that the compatibility shim was not necessary.</span></span> <span data-ttu-id="fb570-168">대규모 프로젝트 호환성 shim을 사용 하 여 가능 일시적으로 ASP.NET Core 및 ASP.NET Web API 2 사이의 API 차이 조정 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-168">For larger projects, using the compatibility shim can be useful for temporarily bridging the API gap between ASP.NET Core and ASP.NET Web API 2.</span></span>

<span data-ttu-id="fb570-169">Web API 호환성 shim은 ASP.NET core Web API 프로젝트를 마이그레이션 큰를 용이 하 게 임시 수단으로 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-169">The Web API compatibility shim is meant to be used as a temporary measure to facilitate migrating large Web API projects to ASP.NET Core.</span></span> <span data-ttu-id="fb570-170">시간이 지남에 따라 프로젝트 호환성 shim에 의존 하지 않고 ASP.NET Core 패턴을 사용 하도록 업데이트 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-170">Over time, projects should be updated to use ASP.NET Core patterns instead of relying on the compatibility shim.</span></span>

<span data-ttu-id="fb570-171">에 포함 된 호환성 기능 `Microsoft.AspNetCore.Mvc.WebApiCompatShim` 포함:</span><span class="sxs-lookup"><span data-stu-id="fb570-171">Compatibility features included in `Microsoft.AspNetCore.Mvc.WebApiCompatShim` include:</span></span>

* <span data-ttu-id="fb570-172">추가 `ApiController` 을 입력 하 여 컨트롤러의 기본 형식 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-172">Adds an `ApiController` type so that controllers' base types don't need to be updated.</span></span>
* <span data-ttu-id="fb570-173">웹 API 스타일 모델 바인딩을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-173">Enables Web API-style model binding.</span></span> <span data-ttu-id="fb570-174">ASP.NET Core MVC는 MVC 5의 경우와 유사 하 게 바인딩 함수 기본적으로 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-174">ASP.NET Core MVC model binding functions similarly to MVC 5, by default.</span></span> <span data-ttu-id="fb570-175">호환성 shim 변경 모델 바인딩 Web API 2 모델 바인딩 규칙 더 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-175">The compatibility shim changes model binding to be more similar to Web API 2 model binding conventions.</span></span> <span data-ttu-id="fb570-176">예를 들어, 복합 형식은 자동으로 요청 본문에서 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-176">For example, complex types are automatically bound from the request body.</span></span>
* <span data-ttu-id="fb570-177">컨트롤러 작업의 형식 매개 변수를 취할 수 있도록 모델 바인딩 확장 `HttpRequestMessage`합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-177">Extends model binding so that controller actions can take parameters of type `HttpRequestMessage`.</span></span>
* <span data-ttu-id="fb570-178">형식의 결과 반환할 작업을 허용 메시지 포맷터를 추가 `HttpResponseMessage`합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-178">Adds message formatters allowing actions to return results of type `HttpResponseMessage`.</span></span>
* <span data-ttu-id="fb570-179">Web API 2 작업 응답에 맞도록 사용 했을 수 있는 추가 응답 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-179">Adds additional response methods that Web API 2 actions may have used to serve responses:</span></span>
  * <span data-ttu-id="fb570-180">HttpResponseMessage 생성기:</span><span class="sxs-lookup"><span data-stu-id="fb570-180">HttpResponseMessage generators:</span></span>
    * `CreateResponse<T>`
    * `CreateErrorResponse`
  * <span data-ttu-id="fb570-181">작업 결과 메서드:</span><span class="sxs-lookup"><span data-stu-id="fb570-181">Action result methods:</span></span>
    * `BadRequestErrorMessageResult`
    * `ExceptionResult`
    * `InternalServerErrorResult`
    * `InvalidModelStateResult`
    * `NegotiatedContentResult`
    * `ResponseMessageResult`
* <span data-ttu-id="fb570-182">인스턴스를 추가 `IContentNegotiator` 앱의 DI 컨테이너에는 콘텐츠 협상 관련 형식에서 [Microsoft.AspNet.WebApi.Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-182">Adds an instance of `IContentNegotiator` to the app's DI container and makes content negotiation-related types from [Microsoft.AspNet.WebApi.Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) available.</span></span> <span data-ttu-id="fb570-183">같은 형식이 포함 됩니다 `DefaultContentNegotiator`, `MediaTypeFormatter`등입니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-183">This includes types like `DefaultContentNegotiator`, `MediaTypeFormatter`, etc.</span></span>

<span data-ttu-id="fb570-184">호환성 shim을 사용 하려면를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-184">To use the compatibility shim, you need to:</span></span>

* <span data-ttu-id="fb570-185">설치 합니다 [Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="fb570-185">Install the [Microsoft.AspNetCore.Mvc.WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim) NuGet package.</span></span>
* <span data-ttu-id="fb570-186">호환성 shim의 서비스를 호출 하 여 앱의 DI 컨테이너를 사용 하 여 등록 `services.AddMvc().AddWebApiConventions()` 앱의 `Startup.ConfigureServices` 메서드.</span><span class="sxs-lookup"><span data-stu-id="fb570-186">Register the compatibility shim's services with the app's DI container by calling `services.AddMvc().AddWebApiConventions()` in the app's `Startup.ConfigureServices` method.</span></span>
* <span data-ttu-id="fb570-187">사용 하 여 웹 API 관련 경로 정의 `MapWebApiRoute` 에 `IRouteBuilder` 앱의 `IApplicationBuilder.UseMvc` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-187">Define Web API-specific routes using `MapWebApiRoute` on the `IRouteBuilder` in the app's `IApplicationBuilder.UseMvc` call.</span></span>

## <a name="summary"></a><span data-ttu-id="fb570-188">요약</span><span class="sxs-lookup"><span data-stu-id="fb570-188">Summary</span></span>

<span data-ttu-id="fb570-189">간단한 ASP.NET Web API 프로젝트를 ASP.NET Core MVC로 마이그레이션가 상당히 간단한 감사 ASP.NET Core MVC에서 Web Api에 대 한 기본 제공 지원.</span><span class="sxs-lookup"><span data-stu-id="fb570-189">Migrating a simple ASP.NET Web API project to ASP.NET Core MVC is fairly straightforward, thanks to the built-in support for Web APIs in ASP.NET Core MVC.</span></span> <span data-ttu-id="fb570-190">모든 ASP.NET Web API 프로젝트를 마이그레이션해야 할 중요 한 부분은 경로, 컨트롤러 및 모델, 컨트롤러 및 작업에 의해 사용 되는 형식으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb570-190">The main pieces every ASP.NET Web API project will need to migrate are routes, controllers, and models, along with updates to the types used by  controllers and actions.</span></span>
