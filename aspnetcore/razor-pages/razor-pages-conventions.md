---
title: ASP.NET Core에서 Razor 페이지 경로 및 앱 규칙
author: guardrex
description: 경로 및 앱 모델 공급자 규칙을 통해 페이지 라우팅, 검색 및 처리를 제어하는 방법을 검색합니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 10/12/2018
uid: razor-pages/razor-pages-conventions
ms.openlocfilehash: f04e0930966c9aaf38543729565b1ef4a80a09e2
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207695"
---
# <a name="razor-pages-route-and-app-conventions-in-aspnet-core"></a><span data-ttu-id="8faa6-103">ASP.NET Core에서 Razor 페이지 경로 및 앱 규칙</span><span class="sxs-lookup"><span data-stu-id="8faa6-103">Razor Pages route and app conventions in ASP.NET Core</span></span>

<span data-ttu-id="8faa6-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="8faa6-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="8faa6-105">페이지 [경로 및 앱 모델 공급자 규칙](xref:mvc/controllers/application-model#conventions)을 사용하여 Razor 페이지 앱에서 페이지 라우팅, 검색 및 처리를 제어하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-105">Learn how to use page [route and app model provider conventions](xref:mvc/controllers/application-model#conventions) to control page routing, discovery, and processing in Razor Pages apps.</span></span>

<span data-ttu-id="8faa6-106">개별 페이지에 대한 사용자 지정 페이지 경로를 구성해야 하는 경우 이 항목의 뒷부분에서 설명할 [AddPageRoute 규칙](#configure-a-page-route)을 사용하여 페이지에 대한 라우팅을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-106">When you need to configure custom page routes for individual pages, configure routing to pages with the [AddPageRoute convention](#configure-a-page-route) described later in this topic.</span></span>

<span data-ttu-id="8faa6-107">페이지 경로 지정, 경로 세그먼트를 추가 하거나 매개 변수는 경로를 추가 하려면 페이지의 사용 `@page` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-107">To specify a page route, add route segments, or add parameters to a route, use the page's `@page` directive.</span></span> <span data-ttu-id="8faa6-108">자세한 내용은 [사용자 지정 경로](xref:razor-pages/index#custom-routes)합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-108">For more information, see [Custom routes](xref:razor-pages/index#custom-routes).</span></span>

<span data-ttu-id="8faa6-109">경로 세그먼트 또는 매개 변수 이름으로 사용할 수 없는 예약어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-109">There are reserved words that can't be used as route segments or parameter names.</span></span> <span data-ttu-id="8faa6-110">자세한 내용은 [라우팅: 예약 된 라우팅 이름](xref:fundamentals/routing#reserved-routing-names)합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-110">For more information, see [Routing: Reserved routing names](xref:fundamentals/routing#reserved-routing-names).</span></span>

<span data-ttu-id="8faa6-111">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/razor-pages-conventions/sample/) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="8faa6-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/razor-pages-conventions/sample/) ([how to download](xref:index#how-to-download-a-sample))</span></span>

::: moniker range="= aspnetcore-2.0"

| <span data-ttu-id="8faa6-112">시나리오</span><span class="sxs-lookup"><span data-stu-id="8faa6-112">Scenario</span></span> | <span data-ttu-id="8faa6-113">샘플에서는 다음 사항을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-113">The sample demonstrates ...</span></span> |
| -------- | --------------------------- |
| [<span data-ttu-id="8faa6-114">모델 규칙</span><span class="sxs-lookup"><span data-stu-id="8faa6-114">Model conventions</span></span>](#model-conventions)<br><br><span data-ttu-id="8faa6-115">Conventions.Add</span><span class="sxs-lookup"><span data-stu-id="8faa6-115">Conventions.Add</span></span><ul><li><span data-ttu-id="8faa6-116">IPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="8faa6-116">IPageRouteModelConvention</span></span></li><li><span data-ttu-id="8faa6-117">IPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="8faa6-117">IPageApplicationModelConvention</span></span></li></ul> | <span data-ttu-id="8faa6-118">경로 템플릿 및 헤더를 앱의 페이지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-118">Add a route template and header to an app's pages.</span></span> |
| [<span data-ttu-id="8faa6-119">페이지 경로 작업 규칙</span><span class="sxs-lookup"><span data-stu-id="8faa6-119">Page route action conventions</span></span>](#page-route-action-conventions)<ul><li><span data-ttu-id="8faa6-120">AddFolderRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="8faa6-120">AddFolderRouteModelConvention</span></span></li><li><span data-ttu-id="8faa6-121">AddPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="8faa6-121">AddPageRouteModelConvention</span></span></li><li><span data-ttu-id="8faa6-122">AddPageRoute</span><span class="sxs-lookup"><span data-stu-id="8faa6-122">AddPageRoute</span></span></li></ul> | <span data-ttu-id="8faa6-123">폴더에 있는 페이지 및 단일 페이지에 경로 템플릿을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-123">Add a route template to pages in a folder and to a single page.</span></span> |
| [<span data-ttu-id="8faa6-124">페이지 모델 작업 규칙</span><span class="sxs-lookup"><span data-stu-id="8faa6-124">Page model action conventions</span></span>](#page-model-action-conventions)<ul><li><span data-ttu-id="8faa6-125">AddFolderApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="8faa6-125">AddFolderApplicationModelConvention</span></span></li><li><span data-ttu-id="8faa6-126">AddPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="8faa6-126">AddPageApplicationModelConvention</span></span></li><li><span data-ttu-id="8faa6-127">ConfigureFilter(필터 클래스, 람다 식 또는 필터 팩터리)</span><span class="sxs-lookup"><span data-stu-id="8faa6-127">ConfigureFilter (filter class, lambda expression, or filter factory)</span></span></li></ul> | <span data-ttu-id="8faa6-128">폴더의 페이지에 헤더를 추가하고, 단일 페이지에 헤더를 추가하고, [필터 팩터리](xref:mvc/controllers/filters#ifilterfactory)를 구성하여 헤더를 앱의 페이지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-128">Add a header to pages in a folder, add a header to a single page, and configure a [filter factory](xref:mvc/controllers/filters#ifilterfactory) to add a header to an app's pages.</span></span> |
| [<span data-ttu-id="8faa6-129">기본 페이지 앱 모델 공급자</span><span class="sxs-lookup"><span data-stu-id="8faa6-129">Default page app model provider</span></span>](#replace-the-default-page-app-model-provider) | <span data-ttu-id="8faa6-130">기본 페이지 모델 공급자를 대체하여 처리기 이름에 대한 규칙을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-130">Replace the default page model provider to change the conventions for handler names.</span></span> |

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

| <span data-ttu-id="8faa6-131">시나리오</span><span class="sxs-lookup"><span data-stu-id="8faa6-131">Scenario</span></span> | <span data-ttu-id="8faa6-132">샘플에서는 다음 사항을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-132">The sample demonstrates ...</span></span> |
| -------- | --------------------------- |
| [<span data-ttu-id="8faa6-133">모델 규칙</span><span class="sxs-lookup"><span data-stu-id="8faa6-133">Model conventions</span></span>](#model-conventions)<br><br><span data-ttu-id="8faa6-134">Conventions.Add</span><span class="sxs-lookup"><span data-stu-id="8faa6-134">Conventions.Add</span></span><ul><li><span data-ttu-id="8faa6-135">IPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="8faa6-135">IPageRouteModelConvention</span></span></li><li><span data-ttu-id="8faa6-136">IPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="8faa6-136">IPageApplicationModelConvention</span></span></li><li><span data-ttu-id="8faa6-137">IPageHandlerModelConvention</span><span class="sxs-lookup"><span data-stu-id="8faa6-137">IPageHandlerModelConvention</span></span></li></ul> | <span data-ttu-id="8faa6-138">경로 템플릿 및 헤더를 앱의 페이지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-138">Add a route template and header to an app's pages.</span></span> |
| [<span data-ttu-id="8faa6-139">페이지 경로 작업 규칙</span><span class="sxs-lookup"><span data-stu-id="8faa6-139">Page route action conventions</span></span>](#page-route-action-conventions)<ul><li><span data-ttu-id="8faa6-140">AddFolderRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="8faa6-140">AddFolderRouteModelConvention</span></span></li><li><span data-ttu-id="8faa6-141">AddPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="8faa6-141">AddPageRouteModelConvention</span></span></li><li><span data-ttu-id="8faa6-142">AddPageRoute</span><span class="sxs-lookup"><span data-stu-id="8faa6-142">AddPageRoute</span></span></li></ul> | <span data-ttu-id="8faa6-143">폴더에 있는 페이지 및 단일 페이지에 경로 템플릿을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-143">Add a route template to pages in a folder and to a single page.</span></span> |
| [<span data-ttu-id="8faa6-144">페이지 모델 작업 규칙</span><span class="sxs-lookup"><span data-stu-id="8faa6-144">Page model action conventions</span></span>](#page-model-action-conventions)<ul><li><span data-ttu-id="8faa6-145">AddFolderApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="8faa6-145">AddFolderApplicationModelConvention</span></span></li><li><span data-ttu-id="8faa6-146">AddPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="8faa6-146">AddPageApplicationModelConvention</span></span></li><li><span data-ttu-id="8faa6-147">ConfigureFilter(필터 클래스, 람다 식 또는 필터 팩터리)</span><span class="sxs-lookup"><span data-stu-id="8faa6-147">ConfigureFilter (filter class, lambda expression, or filter factory)</span></span></li></ul> | <span data-ttu-id="8faa6-148">폴더의 페이지에 헤더를 추가하고, 단일 페이지에 헤더를 추가하고, [필터 팩터리](xref:mvc/controllers/filters#ifilterfactory)를 구성하여 헤더를 앱의 페이지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-148">Add a header to pages in a folder, add a header to a single page, and configure a [filter factory](xref:mvc/controllers/filters#ifilterfactory) to add a header to an app's pages.</span></span> |
| [<span data-ttu-id="8faa6-149">기본 페이지 앱 모델 공급자</span><span class="sxs-lookup"><span data-stu-id="8faa6-149">Default page app model provider</span></span>](#replace-the-default-page-app-model-provider) | <span data-ttu-id="8faa6-150">기본 페이지 모델 공급자를 대체하여 처리기 이름에 대한 규칙을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-150">Replace the default page model provider to change the conventions for handler names.</span></span> |

::: moniker-end

<span data-ttu-id="8faa6-151">Razor 페이지 규칙은 `Startup` 클래스의 서비스 컬렉션에서 [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc)에 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 확장 메서드를 사용하여 추가되고 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-151">Razor Pages conventions are added and configured using the [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) extension method to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc) on the service collection in the `Startup` class.</span></span> <span data-ttu-id="8faa6-152">다음 규칙 예제는 이 토픽의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-152">The following convention examples are explained later in this topic:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc()
        .AddRazorPagesOptions(options =>
            {
                options.Conventions.Add( ... );
                options.Conventions.AddFolderRouteModelConvention("/OtherPages", model => { ... });
                options.Conventions.AddPageRouteModelConvention("/About", model => { ... });
                options.Conventions.AddPageRoute("/Contact", "TheContactPage/{text?}");
                options.Conventions.AddFolderApplicationModelConvention("/OtherPages", model => { ... });
                options.Conventions.AddPageApplicationModelConvention("/About", model => { ... });
                options.Conventions.ConfigureFilter(model => { ... });
                options.Conventions.ConfigureFilter( ... );
            });
}
```

## <a name="route-order"></a><span data-ttu-id="8faa6-153">경로 순서</span><span class="sxs-lookup"><span data-stu-id="8faa6-153">Route order</span></span>

<span data-ttu-id="8faa6-154">경로 지정을 <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> (경로 일치)을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-154">Routes specify an <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> for processing (route matching).</span></span>

| <span data-ttu-id="8faa6-155">순서</span><span class="sxs-lookup"><span data-stu-id="8faa6-155">Order</span></span>            | <span data-ttu-id="8faa6-156">동작</span><span class="sxs-lookup"><span data-stu-id="8faa6-156">Behavior</span></span> |
| :--------------: | -------- |
| <span data-ttu-id="8faa6-157">-1</span><span class="sxs-lookup"><span data-stu-id="8faa6-157">-1</span></span>               | <span data-ttu-id="8faa6-158">경로 다른 경로 처리 되기 전에 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-158">The route is processed before other routes are processed.</span></span> |
| <span data-ttu-id="8faa6-159">0</span><span class="sxs-lookup"><span data-stu-id="8faa6-159">0</span></span>                | <span data-ttu-id="8faa6-160">순서 지정 하지 않으면 (기본값).</span><span class="sxs-lookup"><span data-stu-id="8faa6-160">Order isn't specified (default value).</span></span> <span data-ttu-id="8faa6-161">할당 되지 `Order` (`Order = null`) 경로 기본값 `Order` 처리를 위해 0 (영)입니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-161">Not assigning `Order` (`Order = null`) defaults the route `Order` to 0 (zero) for processing.</span></span> |
| <span data-ttu-id="8faa6-162">1, 2, &hellip; n</span><span class="sxs-lookup"><span data-stu-id="8faa6-162">1, 2, &hellip; n</span></span> | <span data-ttu-id="8faa6-163">경로 처리 순서를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-163">Specifies the route processing order.</span></span> |

<span data-ttu-id="8faa6-164">경로 처리 규칙에 따라 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-164">Route processing is established by convention:</span></span>

* <span data-ttu-id="8faa6-165">경로 순서 대로 처리 됩니다 (-1, 0, 1, 2, &hellip; n).</span><span class="sxs-lookup"><span data-stu-id="8faa6-165">Routes are processed in sequential order (-1, 0, 1, 2, &hellip; n).</span></span>
* <span data-ttu-id="8faa6-166">경로 있는 경우 동일한 `Order`가장 덜 구체적인 경로 뒤에 먼저 특정 경로가 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-166">When routes have the same `Order`, the most specific route is matched first followed by less specific routes.</span></span>
* <span data-ttu-id="8faa6-167">때 동일한 경로 `Order` 매개 변수 수가 같은 일치 요청 URL을 경로에 추가 된 순서 대로 처리 되는 <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.PageConventionCollection>합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-167">When routes with the same `Order` and the same number of parameters match a request URL, routes are processed in the order that they're added to the <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.PageConventionCollection>.</span></span>

<span data-ttu-id="8faa6-168">가능 하면 설정 된 경로 처리 순서에 따라 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8faa6-168">If possible, avoid depending on an established route processing order.</span></span> <span data-ttu-id="8faa6-169">일반적으로 라우팅 URL 일치 하는 올바른 경로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-169">Generally, routing selects the correct route with URL matching.</span></span> <span data-ttu-id="8faa6-170">경로 설정 해야 하는 경우 `Order` 아마도 클라이언트로 복잡 하 고 유지 하기 위해 취약 한 응용 프로그램의 라우팅 체계는 속성 경로를 올바르게 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-170">If you must set route `Order` properties to route requests correctly, the app's routing scheme is probably confusing to clients and fragile to maintain.</span></span> <span data-ttu-id="8faa6-171">앱의 라우팅 체계를 간소화 하기 위해 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-171">Seek to simplify the app's routing scheme.</span></span> <span data-ttu-id="8faa6-172">샘플 앱은 단일 앱을 사용 하는 여러 라우팅 시나리오를 시연 하려면 처리 명시적인 경로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-172">The sample app requires an explicit route processing order to demonstrate several routing scenarios using a single app.</span></span> <span data-ttu-id="8faa6-173">그러나 설정 경로의 연습을 방지 하려고 해야 `Order` 프로덕션 앱에서.</span><span class="sxs-lookup"><span data-stu-id="8faa6-173">However, you should attempt to avoid the practice of setting route `Order` in production apps.</span></span>

<span data-ttu-id="8faa6-174">Razor Pages 라우팅과 MVC 컨트롤러 라우팅은 구현을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-174">Razor Pages routing and MVC controller routing share an implementation.</span></span> <span data-ttu-id="8faa6-175">MVC 항목의 경로 순서에 대 한 정보에서 제공 됩니다 [컨트롤러 작업에 라우팅: 특성 경로 순서 지정](xref:mvc/controllers/routing#ordering-attribute-routes)합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-175">Information on route order in the MVC topics is available at [Routing to controller actions: Ordering attribute routes](xref:mvc/controllers/routing#ordering-attribute-routes).</span></span>

## <a name="model-conventions"></a><span data-ttu-id="8faa6-176">모델 규칙</span><span class="sxs-lookup"><span data-stu-id="8faa6-176">Model conventions</span></span>

<span data-ttu-id="8faa6-177">[IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention)의 대리자를 추가하여 Razor 페이지에 적용되는 [모델 규칙](xref:mvc/controllers/application-model#conventions)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-177">Add a delegate for [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) to add [model conventions](xref:mvc/controllers/application-model#conventions) that apply to Razor Pages.</span></span>

### <a name="add-a-route-model-convention-to-all-pages"></a><span data-ttu-id="8faa6-178">모든 페이지에 경로 모델 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="8faa6-178">Add a route model convention to all pages</span></span>

<span data-ttu-id="8faa6-179">[규칙](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)을 사용하여 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)을 만들고, 페이지 경로 모델을 구축하는 동안 적용되는 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 인스턴스의 컬렉션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-179">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during page route model construction.</span></span>

<span data-ttu-id="8faa6-180">샘플 앱은 앱의 모든 페이지에 `{globalTemplate?}` 경로 템플릿을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-180">The sample app adds a `{globalTemplate?}` route template to all of the pages in the app:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Conventions/GlobalTemplatePageRouteModelConvention.cs?name=snippet1)]

<span data-ttu-id="8faa6-181"><xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel>에 대한 <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> 속성을 `1`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-181">The <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> property for the <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel> is set to `1`.</span></span> <span data-ttu-id="8faa6-182">이렇게 하면 샘플 앱의 동작을 일치 하는 다음 경로:</span><span class="sxs-lookup"><span data-stu-id="8faa6-182">This ensures the following route matching behavior in the sample app:</span></span>

* <span data-ttu-id="8faa6-183">에 대 한 경로 템플릿을 `TheContactPage/{text?}` 항목의 뒷부분에 나오는 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-183">A route template for `TheContactPage/{text?}` is added later in the topic.</span></span> <span data-ttu-id="8faa6-184">연락처 페이지 경로는 기본 순서 `null` (`Order = 0`) 하기 전에 일치 하도록는 `{globalTemplate?}` 경로 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-184">The Contact Page route has a default order of `null` (`Order = 0`), so it matches before the `{globalTemplate?}` route template.</span></span>
* <span data-ttu-id="8faa6-185">`{aboutTemplate?}` 항목의 뒷부분에 나오는 경로 템플릿이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-185">An `{aboutTemplate?}` route template is added later in the topic.</span></span> <span data-ttu-id="8faa6-186">`{aboutTemplate?}` 템플릿이 `2`의 `Order`로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-186">The `{aboutTemplate?}` template is given an `Order` of `2`.</span></span> <span data-ttu-id="8faa6-187">`/About/RouteDataValue`에서 정보 페이지를 요청하는 경우 "RouteDataValue"는 `Order` 속성 설정으로 인해 `RouteData.Values["aboutTemplate"]`(`Order = 2`)이 아닌 `RouteData.Values["globalTemplate"]`(`Order = 1`)으로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-187">When the About page is requested at `/About/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 1`) and not `RouteData.Values["aboutTemplate"]` (`Order = 2`) due to setting the `Order` property.</span></span>
* <span data-ttu-id="8faa6-188">`{otherPagesTemplate?}` 항목의 뒷부분에 나오는 경로 템플릿이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-188">An `{otherPagesTemplate?}` route template is added later in the topic.</span></span> <span data-ttu-id="8faa6-189">`{otherPagesTemplate?}` 템플릿이 `2`의 `Order`로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-189">The `{otherPagesTemplate?}` template is given an `Order` of `2`.</span></span> <span data-ttu-id="8faa6-190">모든 페이지는 *페이지/OtherPages* 폴더 경로 매개 변수를 사용 하 여 요청 (예를 들어 `/OtherPages/Page1/RouteDataValue`), "RouteDataValue"는 로드 `RouteData.Values["globalTemplate"]` (`Order = 1`) 및 not `RouteData.Values["otherPagesTemplate"]` (`Order = 2`) 설정으로 인해는 `Order` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-190">When any page in the *Pages/OtherPages* folder is requested with a route parameter (for example, `/OtherPages/Page1/RouteDataValue`), "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 1`) and not `RouteData.Values["otherPagesTemplate"]` (`Order = 2`) due to setting the `Order` property.</span></span>

<span data-ttu-id="8faa6-191">가능 하면 설정 하지 않은 합니다 `Order`, 그러면 `Order = 0`합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-191">Wherever possible, don't set the `Order`, which results in `Order = 0`.</span></span> <span data-ttu-id="8faa6-192">올바른 경로 선택 하려면 라우팅에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-192">Rely on routing to select the correct route.</span></span>

<span data-ttu-id="8faa6-193">[규칙](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) 추가와 같은 Razor 페이지 옵션은 MVC가 `Startup.ConfigureServices`의 서비스 컬렉션에 추가될 때 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-193">Razor Pages options, such as adding [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions), are added when MVC is added to the service collection in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="8faa6-194">예제는 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/razor-pages-conventions/sample/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8faa6-194">For an example, see the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/razor-pages-conventions/sample/).</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet1)]

<span data-ttu-id="8faa6-195">`localhost:5000/About/GlobalRouteValue`에서 샘플의 정보 페이지를 요청하고 결과를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-195">Request the sample's About page at `localhost:5000/About/GlobalRouteValue` and inspect the result:</span></span>

![GlobalRouteValue의 경로 세그먼트를 사용하여 정보 페이지를 요청합니다.](razor-pages-conventions/_static/about-page-global-template.png)

### <a name="add-an-app-model-convention-to-all-pages"></a><span data-ttu-id="8faa6-198">모든 페이지에 앱 모델 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="8faa6-198">Add an app model convention to all pages</span></span>

<span data-ttu-id="8faa6-199">[규칙](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)을 사용하여 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention)을 만들고, 페이지 앱 모델을 구축하는 동안 적용되는 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 인스턴스의 컬렉션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-199">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during page app model construction.</span></span>

<span data-ttu-id="8faa6-200">이 항목의 뒷부분에서 이 규칙 및 다른 규칙을 설명하기 위해 샘플 앱에는 `AddHeaderAttribute` 클래스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-200">To demonstrate this and other conventions later in the topic, the sample app includes an `AddHeaderAttribute` class.</span></span> <span data-ttu-id="8faa6-201">클래스 생성자가 `name` 문자열 및 `values` 문자열 배열을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-201">The class constructor accepts a `name` string and a `values` string array.</span></span> <span data-ttu-id="8faa6-202">이러한 값은 응답 헤더를 설정하는 `OnResultExecuting` 메서드에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-202">These values are used in its `OnResultExecuting` method to set a response header.</span></span> <span data-ttu-id="8faa6-203">전체 클래스는 항목의 뒷부분에 나오는 [페이지 모델 작업 규칙](#page-model-action-conventions) 섹션에서 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-203">The full class is shown in the [Page model action conventions](#page-model-action-conventions) section later in the topic.</span></span>

<span data-ttu-id="8faa6-204">샘플 앱에서는 앱의 모든 페이지에 `GlobalHeader` 헤더를 추가하는 `AddHeaderAttribute` 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-204">The sample app uses the `AddHeaderAttribute` class to add a header, `GlobalHeader`, to all of the pages in the app:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Conventions/GlobalHeaderPageApplicationModelConvention.cs?name=snippet1)]

<span data-ttu-id="8faa6-205">*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="8faa6-205">*Startup.cs*:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet2)]

<span data-ttu-id="8faa6-206">`localhost:5000/About`에서 샘플의 정보 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-206">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![정보 페이지의 응답 헤더는 GlobalHeader가 추가되었음을 보여줍니다.](razor-pages-conventions/_static/about-page-global-header.png)

::: moniker range=">= aspnetcore-2.1"

### <a name="add-a-handler-model-convention-to-all-pages"></a><span data-ttu-id="8faa6-208">모든 페이지에는 처리기 모델 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="8faa6-208">Add a handler model convention to all pages</span></span>

<span data-ttu-id="8faa6-209">[규칙](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)을 사용하여 [IPageHandlerModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipagehandlermodelconvention)을 만들고, 페이지 처리기 모델을 구축하는 동안 적용되는 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 인스턴스의 컬렉션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-209">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageHandlerModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipagehandlermodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during page handler model construction.</span></span>

```csharp
public class GlobalPageHandlerModelConvention
    : IPageHandlerModelConvention
{
    public void Apply(PageHandlerModel model)
    {
        ...
    }
}
```

<span data-ttu-id="8faa6-210">`Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="8faa6-210">`Startup.ConfigureServices`:</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
        {
            options.Conventions.Add(new GlobalPageHandlerModelConvention());
        });
```

::: moniker-end

## <a name="page-route-action-conventions"></a><span data-ttu-id="8faa6-211">페이지 경로 작업 규칙</span><span class="sxs-lookup"><span data-stu-id="8faa6-211">Page route action conventions</span></span>

<span data-ttu-id="8faa6-212">[IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider)에서 파생되는 기본 경로 모델 공급자는 페이지 경로를 구성하기 위한 확장성 지점을 제공하도록 설계된 규칙을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-212">The default route model provider that derives from [IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider) invokes conventions which are designed to provide extensibility points for configuring page routes.</span></span>

### <a name="folder-route-model-convention"></a><span data-ttu-id="8faa6-213">폴더 경로 모델 규칙</span><span class="sxs-lookup"><span data-stu-id="8faa6-213">Folder route model convention</span></span>

<span data-ttu-id="8faa6-214">[AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention)을 사용하여 지정된 폴더 아래에 있는 모든 페이지에 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel)에 대한 작업을 호출하는 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)을 만들고 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-214">Use [AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) that invokes an action on the [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) for all of the pages under the specified folder.</span></span>

<span data-ttu-id="8faa6-215">샘플 앱에서는 `AddFolderRouteModelConvention`를 사용하여 `{otherPagesTemplate?}` 경로 템플릿을 *OtherPages* 폴더의 페이지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-215">The sample app uses `AddFolderRouteModelConvention` to add an `{otherPagesTemplate?}` route template to the pages in the *OtherPages* folder:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet3)]

<span data-ttu-id="8faa6-216"><xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel>에 대한 <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> 속성을 `2`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-216">The <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> property for the <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel> is set to `2`.</span></span> <span data-ttu-id="8faa6-217">이렇게 하면에 대 한 템플릿을 `{globalTemplate?}` (항목의 앞부분에서 설정 `1`) 단일 경로 값을 제공 하는 경우 첫 번째 경로 데이터 값 위치에 대 한 우선 순위가 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-217">This ensures that the template for `{globalTemplate?}` (set earlier in the topic to `1`) is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="8faa6-218">경우 페이지에는 *페이지/OtherPages* 폴더 경로 매개 변수 값을 사용 하 여 요청 (예를 들어 `/OtherPages/Page1/RouteDataValue`), "RouteDataValue"는 로드 `RouteData.Values["globalTemplate"]` (`Order = 1`) 및 not `RouteData.Values["otherPagesTemplate"]` (`Order = 2`) 설정으로 인해는 `Order` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-218">If a page in the *Pages/OtherPages* folder is requested with a route parameter value (for example, `/OtherPages/Page1/RouteDataValue`), "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 1`) and not `RouteData.Values["otherPagesTemplate"]` (`Order = 2`) due to setting the `Order` property.</span></span>

<span data-ttu-id="8faa6-219">가능 하면 설정 하지 않은 합니다 `Order`, 그러면 `Order = 0`합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-219">Wherever possible, don't set the `Order`, which results in `Order = 0`.</span></span> <span data-ttu-id="8faa6-220">올바른 경로 선택 하려면 라우팅에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-220">Rely on routing to select the correct route.</span></span>

<span data-ttu-id="8faa6-221">`localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue`에서 샘플의 Page1 페이지를 요청하고 결과를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-221">Request the sample's Page1 page at `localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue` and inspect the result:</span></span>

![OtherPages 폴더의 Page1은 GlobalRouteValue 및 OtherPagesRouteValue라는 경로 세그먼트를 사용하여 요청됩니다.](razor-pages-conventions/_static/otherpages-page1-global-and-otherpages-templates.png)

### <a name="page-route-model-convention"></a><span data-ttu-id="8faa6-224">페이지 경로 모델 규칙</span><span class="sxs-lookup"><span data-stu-id="8faa6-224">Page route model convention</span></span>

<span data-ttu-id="8faa6-225">[AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention)을 사용하여 지정된 이름을 가진 페이지에 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel)에 대한 작업을 호출하는 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)을 만들고 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-225">Use [AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) that invokes an action on the [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) for the page with the specified name.</span></span>

<span data-ttu-id="8faa6-226">샘플 앱에서는 `AddPageRouteModelConvention`를 사용하여 `{aboutTemplate?}` 경로 템플릿을 정보 페이지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-226">The sample app uses `AddPageRouteModelConvention` to add an `{aboutTemplate?}` route template to the About page:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet4)]

<span data-ttu-id="8faa6-227"><xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel>에 대한 <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> 속성을 `2`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-227">The <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> property for the <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel> is set to `2`.</span></span> <span data-ttu-id="8faa6-228">이렇게 하면에 대 한 템플릿을 `{globalTemplate?}` (항목의 앞부분에서 설정 `1`) 단일 경로 값을 제공 하는 경우 첫 번째 경로 데이터 값 위치에 대 한 우선 순위가 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-228">This ensures that the template for `{globalTemplate?}` (set earlier in the topic to `1`) is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="8faa6-229">경로 매개 변수 값에서 정보 페이지를 요청 하는 경우 `/About/RouteDataValue`, "RouteDataValue"는 로드 `RouteData.Values["globalTemplate"]` (`Order = 1`) 및 not `RouteData.Values["aboutTemplate"]` (`Order = 2`) 설정으로 인해는 `Order` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-229">If the About page is requested with a route parameter value at `/About/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 1`) and not `RouteData.Values["aboutTemplate"]` (`Order = 2`) due to setting the `Order` property.</span></span>

<span data-ttu-id="8faa6-230">가능 하면 설정 하지 않은 합니다 `Order`, 그러면 `Order = 0`합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-230">Wherever possible, don't set the `Order`, which results in `Order = 0`.</span></span> <span data-ttu-id="8faa6-231">올바른 경로 선택 하려면 라우팅에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-231">Rely on routing to select the correct route.</span></span>

<span data-ttu-id="8faa6-232">`localhost:5000/About/GlobalRouteValue/AboutRouteValue`에서 샘플의 정보 페이지를 요청하고 결과를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-232">Request the sample's About page at `localhost:5000/About/GlobalRouteValue/AboutRouteValue` and inspect the result:</span></span>

![정보 페이지는 GlobalRouteValue 및 AboutRouteValue에 대한 경로 세그먼트를 사용하여 요청됩니다.](razor-pages-conventions/_static/about-page-global-and-about-templates.png)

::: moniker range=">= aspnetcore-2.2"

## <a name="use-a-parameter-transformer-to-customize-page-routes"></a><span data-ttu-id="8faa6-235">매개 변수 변환기를 사용 하 여 페이지 경로 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="8faa6-235">Use a parameter transformer to customize page routes</span></span>

<span data-ttu-id="8faa6-236">ASP.NET Core에서 생성 된 페이지 경로 매개 변수 변환기를 사용 하 여 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-236">Page routes generated by ASP.NET Core can be customized using a parameter transformer.</span></span> <span data-ttu-id="8faa6-237">매개 변수 변환기는 `IOutboundParameterTransformer`를 구현하고 매개 변수의 값을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-237">A parameter transformer implements `IOutboundParameterTransformer` and transforms the value of parameters.</span></span> <span data-ttu-id="8faa6-238">예를 들어 사용자 지정 `SlugifyParameterTransformer` 매개 변수 변환기는 `SubscriptionManagement` 경로 값을 `subscription-management`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-238">For example, a custom `SlugifyParameterTransformer` parameter transformer changes the `SubscriptionManagement` route value to `subscription-management`.</span></span>

<span data-ttu-id="8faa6-239">`PageRouteTransformerConvention` 페이지 경로 모델 규칙 폴더 및 파일 이름 부분은 앱에서 자동으로 생성 된 페이지 경로 매개 변수 변환기를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-239">The `PageRouteTransformerConvention` page route model convention applies a parameter transformer to the folder and file name segments of automatically generated page routes in an app.</span></span> <span data-ttu-id="8faa6-240">예를 들어, Razor 페이지 파일을 */Pages/SubscriptionManagement/ViewAll.cshtml* 해당 경로에서 다시 작성 해야 `/SubscriptionManagement/ViewAll` 하려면 `/subscription-management/view-all`합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-240">For example, the Razor Pages file at */Pages/SubscriptionManagement/ViewAll.cshtml* would have its route rewritten from `/SubscriptionManagement/ViewAll` to `/subscription-management/view-all`.</span></span>

<span data-ttu-id="8faa6-241">`PageRouteTransformerConvention` Razor 페이지 폴더 및 파일 이름에서 제공 되는 자동으로 생성 된 페이지 경로 세그먼트를만 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-241">`PageRouteTransformerConvention` only transforms the automatically generated segments of a page route that come from the Razor Pages folder and file name.</span></span> <span data-ttu-id="8faa6-242">사용 하 여 추가 경로 세그먼트를 변환 하지 않습니다는 `@page` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-242">It doesn't transform route segments added with the `@page` directive.</span></span> <span data-ttu-id="8faa6-243">규칙 또한 변형 하지 않습니다 하 여 추가 된 경로 <xref:Microsoft.Extensions.DependencyInjection.PageConventionCollectionExtensions.AddPageRoute*>합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-243">The convention also doesn't transform routes added by <xref:Microsoft.Extensions.DependencyInjection.PageConventionCollectionExtensions.AddPageRoute*>.</span></span>

<span data-ttu-id="8faa6-244">합니다 `PageRouteTransformerConvention` 에 옵션으로 등록 되어 `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="8faa6-244">The `PageRouteTransformerConvention` is registered as an option in `Startup.ConfigureServices`:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc()
        .AddRazorPagesOptions(options =>
            {
                options.Conventions.Add(
                    new PageRouteTransformerConvention(
                        new SlugifyParameterTransformer()));
            });
}

public class SlugifyParameterTransformer : IOutboundParameterTransformer
{
    public string TransformOutbound(object value)
    {
        if (value == null) { return null; }

        // Slugify value
        return Regex.Replace(value.ToString(), "([a-z])([A-Z])", "$1-$2").ToLower();
    }
}
```

::: moniker-end

## <a name="configure-a-page-route"></a><span data-ttu-id="8faa6-245">페이지 경로 구성</span><span class="sxs-lookup"><span data-stu-id="8faa6-245">Configure a page route</span></span>

<span data-ttu-id="8faa6-246">[AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute)를 사용하여 지정된 페이지 경로에 페이지에 대한 경로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-246">Use [AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute) to configure a route to a page at the specified page path.</span></span> <span data-ttu-id="8faa6-247">페이지에 생성된 링크는 지정된 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-247">Generated links to the page use your specified route.</span></span> <span data-ttu-id="8faa6-248">`AddPageRoute`는 `AddPageRouteModelConvention`을 사용하여 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-248">`AddPageRoute` uses `AddPageRouteModelConvention` to establish the route.</span></span>

<span data-ttu-id="8faa6-249">샘플 앱은 *Contact.cshtml*의 `/TheContactPage`에 대한 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-249">The sample app creates a route to `/TheContactPage` for *Contact.cshtml*:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet5)]

<span data-ttu-id="8faa6-250">연락처 페이지도 기본 경로를 통해 `/Contact`에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-250">The Contact page can also be reached at `/Contact` via its default route.</span></span>

<span data-ttu-id="8faa6-251">연락처 페이지에 대한 샘플 앱의 사용자 지정 경로는 선택적 `text` 경로 세그먼트(`{text?}`)에 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-251">The sample app's custom route to the Contact page allows for an optional `text` route segment (`{text?}`).</span></span> <span data-ttu-id="8faa6-252">방문자가 해당 `/Contact` 경로에 있는 페이지에 액세스하는 경우 페이지에는 해당 `@page` 지시문에 있는 이 선택적 세그먼트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-252">The page also includes this optional segment in its `@page` directive in case the visitor accesses the page at its `/Contact` route:</span></span>

[!code-cshtml[](razor-pages-conventions/sample/Pages/Contact.cshtml?highlight=1)]

<span data-ttu-id="8faa6-253">렌더링된 페이지의 **연락처** 링크에 생성된 URL이 업데이트된 경로를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-253">Note that the URL generated for the **Contact** link in the rendered page reflects the updated route:</span></span>

![탐색 모음의 샘플 앱 연락처 링크](razor-pages-conventions/_static/contact-link.png)

![렌더링된 HTML에서 연락처 링크를 검사하면 href가 '/TheContactPage'로 설정되어 있음을 나타냅니다.](razor-pages-conventions/_static/contact-link-source.png)

<span data-ttu-id="8faa6-256">일반적인 경로 `/Contact` 또는 사용자 지정 경로 `/TheContactPage`에서 연락처 페이지를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="8faa6-256">Visit the Contact page at either its ordinary route, `/Contact`, or the custom route, `/TheContactPage`.</span></span> <span data-ttu-id="8faa6-257">추가 `text` 경로 세그먼트를 제공하는 경우 페이지는 제공한 HTML 인코딩 세그먼트를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-257">If you supply an additional `text` route segment, the page shows the HTML-encoded segment that you provide:</span></span>

![URL에서 'TextValue'라는 선택적 'text' 경로 세그먼트를 제공하는 에지 브라우저 예제입니다.](razor-pages-conventions/_static/route-segment-with-custom-route.png)

## <a name="page-model-action-conventions"></a><span data-ttu-id="8faa6-260">페이지 모델 작업 규칙</span><span class="sxs-lookup"><span data-stu-id="8faa6-260">Page model action conventions</span></span>

<span data-ttu-id="8faa6-261">[IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider)에서 파생되는 기본 페이지 모델 공급자는 페이지 모델을 구성하기 위한 확장성 지점을 제공하도록 설계된 규칙을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-261">The default page model provider that implements [IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider) invokes conventions which are designed to provide extensibility points for configuring page models.</span></span> <span data-ttu-id="8faa6-262">이러한 규칙은 페이지 검색 및 처리 시나리오를 빌드하고 수정하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-262">These conventions are useful when building and modifying page discovery and processing scenarios.</span></span>

<span data-ttu-id="8faa6-263">샘플 앱은 이 섹션의 예제에서 응답 헤더를 적용하는 [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute)라는 `AddHeaderAttribute` 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-263">For the examples in this section, the sample app uses an `AddHeaderAttribute` class, which is a [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute), that applies a response header:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Filters/AddHeader.cs?name=snippet1)]

<span data-ttu-id="8faa6-264">샘플을 규칙을 사용하여 폴더에 있는 모든 페이지 및 단일 페이지에 특성을 적용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-264">Using conventions, the sample demonstrates how to apply the attribute to all of the pages in a folder and to a single page.</span></span>

<span data-ttu-id="8faa6-265">**폴더 앱 모델 규칙**</span><span class="sxs-lookup"><span data-stu-id="8faa6-265">**Folder app model convention**</span></span>

<span data-ttu-id="8faa6-266">[AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention)을 사용하여 지정된 폴더 아래에 있는 모든 페이지에 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) 인스턴스에 대한 작업을 호출하는 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention)을 만들고 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-266">Use [AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) that invokes an action on [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) instances for all pages under the specified folder.</span></span>

<span data-ttu-id="8faa6-267">이 샘플은 *OtherPages* 폴더 내의 페이지에 `OtherPagesHeader` 헤더를 추가하여 앱의 `AddFolderApplicationModelConvention`을 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-267">The sample demonstrates the use of `AddFolderApplicationModelConvention` by adding a header, `OtherPagesHeader`, to the pages inside the *OtherPages* folder of the app:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet6)]

<span data-ttu-id="8faa6-268">`localhost:5000/OtherPages/Page1`에서 샘플의 Page1 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-268">Request the sample's Page1 page at `localhost:5000/OtherPages/Page1` and inspect the headers to view the result:</span></span>

![OtherPages/Page1 페이지의 응답 헤더는 OtherPagesHeader가 추가되었음을 보여줍니다.](razor-pages-conventions/_static/page1-otherpages-header.png)

<span data-ttu-id="8faa6-270">**페이지 앱 모델 규칙**</span><span class="sxs-lookup"><span data-stu-id="8faa6-270">**Page app model convention**</span></span>

<span data-ttu-id="8faa6-271">사용 하 여 [AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention) 만들고 추가 하는 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) 하는 작업을 호출 합니다 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) 페이지에 대 한 지정 된 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-271">Use [AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) that invokes an action on the [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) for the page with the specified name.</span></span>

<span data-ttu-id="8faa6-272">샘플은 정보 페이지에 `AboutHeader` 헤더를 추가하여 `AddPageApplicationModelConvention`를 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-272">The sample demonstrates the use of `AddPageApplicationModelConvention` by adding a header, `AboutHeader`, to the About page:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet7)]

<span data-ttu-id="8faa6-273">`localhost:5000/About`에서 샘플의 정보 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-273">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![정보 페이지의 응답 헤더는 AboutHeader가 추가되었음을 보여줍니다.](razor-pages-conventions/_static/about-page-about-header.png)

<span data-ttu-id="8faa6-275">**필터 구성**</span><span class="sxs-lookup"><span data-stu-id="8faa6-275">**Configure a filter**</span></span>

<span data-ttu-id="8faa6-276">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter)는 지정된 필터를 적용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-276">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter) configures the specified filter to apply.</span></span> <span data-ttu-id="8faa6-277">필터 클래스를 구현할 수 있지만 샘플 앱은 람다 식으로 필터를 구현하는 방법을 보여줍니다. 그러면 백그라운드에서 필터를 반환하는 팩터리로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-277">You can implement a filter class, but the sample app shows how to implement a filter in a lambda expression, which is implemented behind-the-scenes as a factory that returns a filter:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet8)]

<span data-ttu-id="8faa6-278">페이지 앱 모델은 *OtherPages* 폴더에 있는 Page2 페이지로 이동하는 세그먼트에 대한 상대 경로를 확인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-278">The page app model is used to check the relative path for segments that lead to the Page2 page in the *OtherPages* folder.</span></span> <span data-ttu-id="8faa6-279">조건이 통과하는 경우 헤더가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-279">If the condition passes, a header is added.</span></span> <span data-ttu-id="8faa6-280">그렇지 않으면 `EmptyFilter`이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-280">If not, the `EmptyFilter` is applied.</span></span>

<span data-ttu-id="8faa6-281">`EmptyFilter`은 [작업 필터](xref:mvc/controllers/filters#action-filters)입니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-281">`EmptyFilter` is an [Action filter](xref:mvc/controllers/filters#action-filters).</span></span> <span data-ttu-id="8faa6-282">Razor 페이지에서 작업 필터를 무시하므로 경로에 `OtherPages/Page2`가 포함되지 않는 경우 의도한 대로 `EmptyFilter`이 작동되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-282">Since Action filters are ignored by Razor Pages, the `EmptyFilter` no-ops as intended if the path doesn't contain `OtherPages/Page2`.</span></span>

<span data-ttu-id="8faa6-283">`localhost:5000/OtherPages/Page2`에서 샘플의 Page2 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-283">Request the sample's Page2 page at `localhost:5000/OtherPages/Page2` and inspect the headers to view the result:</span></span>

![OtherPagesPage2Header는 Page2에 대한 응답에 추가됩니다.](razor-pages-conventions/_static/page2-filter-header.png)

<span data-ttu-id="8faa6-285">**필터 팩터리 구성**</span><span class="sxs-lookup"><span data-stu-id="8faa6-285">**Configure a filter factory**</span></span>

<span data-ttu-id="8faa6-286">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__)는 모든 Razor 페이지에 [필터](xref:mvc/controllers/filters)를 적용하도록 지정된 팩터리를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-286">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__) configures the specified factory to apply [filters](xref:mvc/controllers/filters) to all Razor Pages.</span></span>

<span data-ttu-id="8faa6-287">샘플 앱은 앱의 페이지에 두 개의 값이 포함된 `FilterFactoryHeader` 헤더를 추가하여 [필터 팩터리](xref:mvc/controllers/filters#ifilterfactory)를 사용하는 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-287">The sample app provides an example of using a [filter factory](xref:mvc/controllers/filters#ifilterfactory) by adding a header, `FilterFactoryHeader`, with two values to the app's pages:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet9)]

<span data-ttu-id="8faa6-288">*AddHeaderWithFactory.cs*:</span><span class="sxs-lookup"><span data-stu-id="8faa6-288">*AddHeaderWithFactory.cs*:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Factories/AddHeaderWithFactory.cs?name=snippet1)]

<span data-ttu-id="8faa6-289">`localhost:5000/About`에서 샘플의 정보 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-289">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![정보 페이지의 응답 헤더에서는 두 개의 FilterFactoryHeader 헤더가 추가되었음을 보여줍니다.](razor-pages-conventions/_static/about-page-filter-factory-header.png)

## <a name="replace-the-default-page-app-model-provider"></a><span data-ttu-id="8faa6-291">기본 페이지 앱 모델 공급자 바꾸기</span><span class="sxs-lookup"><span data-stu-id="8faa6-291">Replace the default page app model provider</span></span>

<span data-ttu-id="8faa6-292">Razor 페이지는 `IPageApplicationModelProvider` 인터페이스를 사용하여 [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-292">Razor Pages uses the `IPageApplicationModelProvider` interface to create a [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider).</span></span> <span data-ttu-id="8faa6-293">처리기 검색 및 처리에 대해 고유한 구현 논리를 제공하기 위해 기본 모델 공급자에서 상속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-293">You can inherit from the default model provider to provide your own implementation logic for handler discovery and processing.</span></span> <span data-ttu-id="8faa6-294">기본 구현([참조 원본](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs))은 아래에서 설명할 *명명되지 않은* 및 *명명된* 처리기 명명에 대한 규칙을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-294">The default implementation ([reference source](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs)) establishes conventions for *unnamed* and *named* handler naming, which is described below.</span></span>

<span data-ttu-id="8faa6-295">**기본 명명되지 않은 처리기 메서드**</span><span class="sxs-lookup"><span data-stu-id="8faa6-295">**Default unnamed handler methods**</span></span>

<span data-ttu-id="8faa6-296">HTTP 동사에 대한 처리기 메서드("명명되지 않은" 처리기 메서드)는 다음 규칙을 따릅니다. `On<HTTP verb>[Async]`(`Async`를 추가하는 것은 선택적이지만 비동기 메서드에서 사용하는 것이 좋습니다.)</span><span class="sxs-lookup"><span data-stu-id="8faa6-296">Handler methods for HTTP verbs ("unnamed" handler methods) follow a convention: `On<HTTP verb>[Async]` (appending `Async` is optional but recommended for async methods).</span></span>

| <span data-ttu-id="8faa6-297">명명되지 않은 처리기 메서드</span><span class="sxs-lookup"><span data-stu-id="8faa6-297">Unnamed handler method</span></span>     | <span data-ttu-id="8faa6-298">작업</span><span class="sxs-lookup"><span data-stu-id="8faa6-298">Operation</span></span>                      |
| -------------------------- | ------------------------------ |
| `OnGet`/`OnGetAsync`       | <span data-ttu-id="8faa6-299">페이지 상태를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-299">Initialize the page state.</span></span>     |
| `OnPost`/`OnPostAsync`     | <span data-ttu-id="8faa6-300">POST 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-300">Handle POST requests.</span></span>          |
| `OnDelete`/`OnDeleteAsync` | <span data-ttu-id="8faa6-301">DELETE 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-301">Handle DELETE requests&#8224;.</span></span> |
| `OnPut`/`OnPutAsync`       | <span data-ttu-id="8faa6-302">PUT 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-302">Handle PUT requests&#8224;.</span></span>    |
| `OnPatch`/`OnPatchAsync`   | <span data-ttu-id="8faa6-303">PATCH 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-303">Handle PATCH requests&#8224;.</span></span>  |

<span data-ttu-id="8faa6-304">페이지에 대한 API를 호출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-304">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="8faa6-305">**기본 명명된 처리기 메서드**</span><span class="sxs-lookup"><span data-stu-id="8faa6-305">**Default named handler methods**</span></span>

<span data-ttu-id="8faa6-306">개발자가 제공하는 처리기 메서드("명명된" 처리기 메서드)는 비슷한 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-306">Handler methods provided by the developer ("named" handler methods) follow a similar convention.</span></span> <span data-ttu-id="8faa6-307">처리기 이름은 HTTP 동사 뒤에 또는 HTTP 동사와 `Async` 사이에 표시됩니다. `On<HTTP verb><handler name>[Async]`(`Async`을 추가하는 것은 선택적이지만 비동기 메서드에서 사용하는 것이 좋습니다.)</span><span class="sxs-lookup"><span data-stu-id="8faa6-307">The handler name appears after the HTTP verb or between the HTTP verb and `Async`: `On<HTTP verb><handler name>[Async]` (appending `Async` is optional but recommended for async methods).</span></span> <span data-ttu-id="8faa6-308">예를 들어 메시지를 처리하는 메서드는 아래 표에 표시된 명명된 메시지일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-308">For example, methods that process messages might take the naming shown in the table below.</span></span>

| <span data-ttu-id="8faa6-309">예제 명명된 처리기 메서드</span><span class="sxs-lookup"><span data-stu-id="8faa6-309">Example named handler method</span></span>             | <span data-ttu-id="8faa6-310">예제 작업</span><span class="sxs-lookup"><span data-stu-id="8faa6-310">Example operation</span></span>        |
| ---------------------------------------- | ------------------------ |
| `OnGetMessage`/`OnGetMessageAsync`       | <span data-ttu-id="8faa6-311">메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-311">Obtain a message.</span></span>        |
| `OnPostMessage`/`OnPostMessageAsync`     | <span data-ttu-id="8faa6-312">메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-312">POST a message.</span></span>          |
| `OnDeleteMessage`/`OnDeleteMessageAsync` | <span data-ttu-id="8faa6-313">메시지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-313">DELETE a message&#8224;.</span></span> |
| `OnPutMessage`/`OnPutMessageAsync`       | <span data-ttu-id="8faa6-314">메시지를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-314">PUT a message&#8224;.</span></span>    |
| `OnPatchMessage`/`OnPatchMessageAsync`   | <span data-ttu-id="8faa6-315">메시지를 패치합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-315">PATCH a message&#8224;.</span></span>  |

<span data-ttu-id="8faa6-316">페이지에 대한 API를 호출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-316">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="8faa6-317">**처리기 메서드 이름 사용자 지정**</span><span class="sxs-lookup"><span data-stu-id="8faa6-317">**Customize handler method names**</span></span>

<span data-ttu-id="8faa6-318">명명되지 않은 및 명명된 처리기 메서드의 이름을 지정하는 방식을 변경하려는 경우를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-318">Assume that you prefer to change the way unnamed and named handler methods are named.</span></span> <span data-ttu-id="8faa6-319">대체 이름 지정 체계는 메서드 이름을 "On"으로 시작되지 않도록 방지하고 첫 번째 단어 세그먼트를 사용하여 HTTP 동사를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-319">An alternative naming scheme is to avoid starting the method names with "On" and use the first word segment to determine the HTTP verb.</span></span> <span data-ttu-id="8faa6-320">다른 변경을 수행할 수 있습니다(예: DELETE, PUT 및 PATCH에 대한 동사를 POST로 변환).</span><span class="sxs-lookup"><span data-stu-id="8faa6-320">You can make other changes, such as converting the verbs for DELETE, PUT, and PATCH to POST.</span></span> <span data-ttu-id="8faa6-321">이러한 체계는 다음 표에 표시된 메서드 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-321">Such a scheme provides the method names shown in the following table.</span></span>

| <span data-ttu-id="8faa6-322">처리기 메서드</span><span class="sxs-lookup"><span data-stu-id="8faa6-322">Handler method</span></span>                       | <span data-ttu-id="8faa6-323">작업</span><span class="sxs-lookup"><span data-stu-id="8faa6-323">Operation</span></span>                      |
| ------------------------------------ | ------------------------------ |
| `Get`                                | <span data-ttu-id="8faa6-324">페이지 상태를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-324">Initialize the page state.</span></span>     |
| `Post`/`PostAsync`                   | <span data-ttu-id="8faa6-325">POST 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-325">Handle POST requests.</span></span>          |
| `Delete`/`DeleteAsync`               | <span data-ttu-id="8faa6-326">DELETE 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-326">Handle DELETE requests&#8224;.</span></span> |
| `Put`/`PutAsync`                     | <span data-ttu-id="8faa6-327">PUT 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-327">Handle PUT requests&#8224;.</span></span>    |
| `Patch`/`PatchAsync`                 | <span data-ttu-id="8faa6-328">PATCH 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-328">Handle PATCH requests&#8224;.</span></span>  |
| `GetMessage`                         | <span data-ttu-id="8faa6-329">메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-329">Obtain a message.</span></span>              |
| `PostMessage`/`PostMessageAsync`     | <span data-ttu-id="8faa6-330">메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-330">POST a message.</span></span>                |
| `DeleteMessage`/`DeleteMessageAsync` | <span data-ttu-id="8faa6-331">삭제할 메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-331">POST a message to delete.</span></span>      |
| `PutMessage`/`PutMessageAsync`       | <span data-ttu-id="8faa6-332">배치할 메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-332">POST a message to put.</span></span>         |
| `PatchMessage`/`PatchMessageAsync`   | <span data-ttu-id="8faa6-333">패치할 메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-333">POST a message to patch.</span></span>       |

<span data-ttu-id="8faa6-334">페이지에 대한 API를 호출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-334">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="8faa6-335">이 체계를 설정하려면 `DefaultPageApplicationModelProvider` 클래스에서 상속하고, [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) 메서드를 재정의하여 [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) 처리기 이름을 확인하는 사용자 지정 논리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-335">To establish this scheme, inherit from the `DefaultPageApplicationModelProvider` class and override the [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) method to supply custom logic for resolving [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) handler names.</span></span> <span data-ttu-id="8faa6-336">샘플 앱에서는 `CustomPageApplicationModelProvider` 클래스에서 이 작업을 수행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-336">The sample app shows you how this is done in its `CustomPageApplicationModelProvider` class:</span></span>

[!code-csharp[](razor-pages-conventions/sample/CustomPageApplicationModelProvider.cs?name=snippet1&highlight=1-2,45-46,64-68,78-85,87,92,106)]

<span data-ttu-id="8faa6-337">클래스의 장점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-337">Highlights of the class include:</span></span>

* <span data-ttu-id="8faa6-338">클래스는 `DefaultPageApplicationModelProvider`에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-338">The class inherits from `DefaultPageApplicationModelProvider`.</span></span>
* <span data-ttu-id="8faa6-339">`TryParseHandlerMethod`는 `PageHandlerModel`를 만들 때 HTTP 동사(`httpMethod`) 및 명명된 처리기 이름(`handlerName`)을 결정하는 처리기를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-339">The `TryParseHandlerMethod` processes a handler to determine the HTTP verb (`httpMethod`) and named handler name (`handlerName`) when creating the `PageHandlerModel`.</span></span>
  * <span data-ttu-id="8faa6-340">`Async` 후위가 있다면 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-340">An `Async` postfix is ignored, if present.</span></span>
  * <span data-ttu-id="8faa6-341">대/소문자 구분을 사용하여 메서드 이름에서 HTTP 동사를 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-341">Casing is used to parse the HTTP verb from the method name.</span></span>
  * <span data-ttu-id="8faa6-342">메서드 이름(`Async` 제외)이 HTTP 동사 이름과 같은 경우 명명된 처리기가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-342">When the method name (without `Async`) is equal to the HTTP verb name, there's no named handler.</span></span> <span data-ttu-id="8faa6-343">`handlerName`가 `null` 로 설정되고, 메서드 이름이 `Get`, `Post`, `Delete`, `Put` 또는 `Patch`입니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-343">The `handlerName` is set to `null`, and the method name is `Get`, `Post`, `Delete`, `Put`, or `Patch`.</span></span>
  * <span data-ttu-id="8faa6-344">메서드 이름(`Async` 제외)이 HTTP 동사 이름보다 긴 경우 명명된 처리기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-344">When the method name (without `Async`) is longer than the HTTP verb name, there's a named handler.</span></span> <span data-ttu-id="8faa6-345">`handlerName`는 `<method name (less 'Async', if present)>`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-345">The `handlerName` is set to `<method name (less 'Async', if present)>`.</span></span> <span data-ttu-id="8faa6-346">예를 들어 "GetMessage" 및 "GetMessageAsync"는 모두 "GetMessage"라는 처리기 이름을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-346">For example, both "GetMessage" and "GetMessageAsync" yield a handler name of "GetMessage".</span></span>
  * <span data-ttu-id="8faa6-347">DELETE, PUT 및 PATCH HTTP 동사는 POST로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-347">DELETE, PUT, and PATCH HTTP verbs are converted to POST.</span></span>

<span data-ttu-id="8faa6-348">`Startup` 클래스에 `CustomPageApplicationModelProvider`을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-348">Register the `CustomPageApplicationModelProvider` in the `Startup` class:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet10)]

<span data-ttu-id="8faa6-349">*Index.cshtml.cs*의 페이지 모델은 앱에서 페이지에 대한 일반 처리기 메서드 명명 규칙을 변경하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-349">The page model in *Index.cshtml.cs* shows how the ordinary handler method naming conventions are changed for pages in the app.</span></span> <span data-ttu-id="8faa6-350">Razor 페이지에서 사용되는 일반적인 "On" 접두사 이름 지정이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-350">The ordinary "On" prefix naming used with Razor Pages is removed.</span></span> <span data-ttu-id="8faa6-351">페이지 상태를 초기화하는 메서드의 이름은 이제 `Get`입니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-351">The method that initializes the page state is now named `Get`.</span></span> <span data-ttu-id="8faa6-352">페이지에 대한 페이지 모델을 여는 경우 앱 전체에서 사용하는 이 규칙을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-352">You can see this convention used throughout the app if you open any page model for any of the pages.</span></span>

<span data-ttu-id="8faa6-353">다른 메서드는 각각 해당 프로세스를 설명하는 HTTP 동사로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-353">Each of the other methods start with the HTTP verb that describes its processing.</span></span> <span data-ttu-id="8faa6-354">`Delete`로 시작하는 두 가지 메서드는 DELETE HTTP 동사로 정상적으로 처리되지만 `TryParseHandlerMethod`의 논리는 명시적으로 처리기 모두의 POST에 대해 동사로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-354">The two methods that start with `Delete` would normally be treated as DELETE HTTP verbs, but the logic in `TryParseHandlerMethod` explicitly sets the verb to POST for both handlers.</span></span>

<span data-ttu-id="8faa6-355">`Async`는 `DeleteAllMessages`와 `DeleteMessageAsync` 간에 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-355">Note that `Async` is optional between `DeleteAllMessages` and `DeleteMessageAsync`.</span></span> <span data-ttu-id="8faa6-356">모두 비동기 메서드이지만 `Async` 후위를 사용할지 선택할 수 있다면 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-356">They're both asynchronous methods, but you can choose to use the `Async` postfix or not; we recommend that you do.</span></span> <span data-ttu-id="8faa6-357">`DeleteAllMessages`는 설명을 위해 사용되지만 이러한 `DeleteAllMessagesAsync` 메서드의 이름을 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-357">`DeleteAllMessages` is used here for demonstration purposes, but we recommend that you name such a method `DeleteAllMessagesAsync`.</span></span> <span data-ttu-id="8faa6-358">샘플의 구현이라는 프로세스에 영향을 주지 않지만 `Async` 후위를 사용하면 비동기 메서드라는 점을 부각시킵니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-358">It doesn't affect the processing of the sample's implementation, but using the `Async` postfix calls out the fact that it's an asynchronous method.</span></span>

[!code-csharp[](razor-pages-conventions/sample/Pages/Index.cshtml.cs?name=snippet1&highlight=1,6,16,29)]

<span data-ttu-id="8faa6-359">*Index.cshtml*에서 제공된 처리기 이름은 `DeleteAllMessages` 및 `DeleteMessageAsync` 처리기 메서드와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-359">Note the handler names provided in *Index.cshtml* match the `DeleteAllMessages` and `DeleteMessageAsync` handler methods:</span></span>

[!code-cshtml[](razor-pages-conventions/sample/Pages/Index.cshtml?range=29-60&highlight=7-8,24-25)]

<span data-ttu-id="8faa6-360">처리기 메서드 이름 `DeleteMessageAsync`의 `Async`는 메서드에 대한 POST 요청과 일치하는 처리기에 대해 `TryParseHandlerMethod`을 기준으로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-360">`Async` in the handler method name `DeleteMessageAsync` is factored out by the `TryParseHandlerMethod` for handler matching of POST request to method.</span></span> <span data-ttu-id="8faa6-361">`DeleteMessage`라는 `asp-page-handler` 이름은 처리기 메서드 `DeleteMessageAsync`와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-361">The `asp-page-handler` name of `DeleteMessage` is matched to the handler method `DeleteMessageAsync`.</span></span>

## <a name="mvc-filters-and-the-page-filter-ipagefilter"></a><span data-ttu-id="8faa6-362">MVC 필터 및 페이지 필터(IPageFilter)</span><span class="sxs-lookup"><span data-stu-id="8faa6-362">MVC Filters and the Page filter (IPageFilter)</span></span>

<span data-ttu-id="8faa6-363">Razor 페이지가 처리기 메서드를 사용하므로 MVC [작업 필터](xref:mvc/controllers/filters#action-filters)는 Razor 페이지에서 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-363">MVC [Action filters](xref:mvc/controllers/filters#action-filters) are ignored by Razor Pages, since Razor Pages use handler methods.</span></span> <span data-ttu-id="8faa6-364">[권한 부여](xref:mvc/controllers/filters#authorization-filters), [예외](xref:mvc/controllers/filters#exception-filters), [리소스](xref:mvc/controllers/filters#resource-filters) 및 [결과](xref:mvc/controllers/filters#result-filters)에 다른 유형의 MVC 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-364">Other types of MVC filters are available for you to use: [Authorization](xref:mvc/controllers/filters#authorization-filters), [Exception](xref:mvc/controllers/filters#exception-filters), [Resource](xref:mvc/controllers/filters#resource-filters), and [Result](xref:mvc/controllers/filters#result-filters).</span></span> <span data-ttu-id="8faa6-365">자세한 내용은 [필터](xref:mvc/controllers/filters) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8faa6-365">For more information, see the [Filters](xref:mvc/controllers/filters) topic.</span></span>

<span data-ttu-id="8faa6-366">페이지 필터([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter))는 Razor 페이지에 적용되는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="8faa6-366">The Page filter ([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)) is a filter that applies to Razor Pages.</span></span> <span data-ttu-id="8faa6-367">자세한 내용은 [Razor 페이지에 대한 필터 메서드](xref:razor-pages/filter)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8faa6-367">For more information, see [Filter methods for Razor Pages](xref:razor-pages/filter).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8faa6-368">추가 자료</span><span class="sxs-lookup"><span data-stu-id="8faa6-368">Additional resources</span></span>

* [<span data-ttu-id="8faa6-369">Razor 페이지 권한 부여 규칙</span><span class="sxs-lookup"><span data-stu-id="8faa6-369">Razor Pages authorization conventions</span></span>](xref:security/authorization/razor-pages-authorization)
