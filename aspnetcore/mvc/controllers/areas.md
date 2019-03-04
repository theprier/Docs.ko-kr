---
title: ASP.NET Core의 영역
author: rick-anderson
description: 관련 기능을 별도의 네임스페이스(라우팅용) 및 폴더 구조(보기용)로 그룹화하는 데 사용되는 ASP.NET MVC 기능인 영역에 대해 알아봅니다.
ms.author: riande
ms.date: 02/14/2019
uid: mvc/controllers/areas
ms.openlocfilehash: c21eed04ea68512515da262b6b6895dc1a821039
ms.sourcegitcommit: 2c7ffe349eabdccf2ed748dd303ffd0ba6e1cfe3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56833529"
---
# <a name="areas-in-aspnet-core"></a><span data-ttu-id="87cff-103">ASP.NET Core의 영역</span><span class="sxs-lookup"><span data-stu-id="87cff-103">Areas in ASP.NET Core</span></span>

<span data-ttu-id="87cff-104">작성자: [Dhananjay Kumar](https://twitter.com/debug_mode) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="87cff-104">By [Dhananjay Kumar](https://twitter.com/debug_mode) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="87cff-105">영역은 관련 기능을 별도의 네임스페이스(라우팅용) 및 폴더 구조(보기용)로 그룹화하는 데 사용되는 ASP.NET 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-105">Areas are an ASP.NET feature used to organize related functionality into a group as a separate namespace (for routing) and folder structure (for views).</span></span> <span data-ttu-id="87cff-106">영역을 사용하면 다른 경로 매개 변수 `area`를 `controller` 및 `action` 또는 Razor Page `page`에 추가하여 라우팅을 위한 계층 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-106">Using areas creates a hierarchy for the purpose of routing by adding another route parameter, `area`, to `controller` and `action` or a Razor Page `page`.</span></span>

<span data-ttu-id="87cff-107">영역에서는 ASP.NET Core 웹앱을 각각의 Razor Pages, 컨트롤러, 보기 및 모델의 자체 세트가 있는 작은 기능 그룹으로 분할하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-107">Areas provide a way to partition an ASP.NET Core Web app into smaller functional groups, each  with its own set of Razor Pages, controllers, views, and models.</span></span> <span data-ttu-id="87cff-108">영역은 앱 내에서 효과적인 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-108">An area is effectively a structure inside an app.</span></span> <span data-ttu-id="87cff-109">ASP.NET Core 웹 프로젝트에서 페이지, 모델, 컨트롤러 및 보기와 같은 논리적 구성 요소는 서로 다른 폴더에 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-109">In an ASP.NET Core web project, logical components like Pages, Model, Controller, and View are kept in different folders.</span></span> <span data-ttu-id="87cff-110">ASP.NET Core 런타임은 명명 규칙을 사용하여 이러한 구성 요소 간의 관계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-110">The ASP.NET Core runtime uses naming conventions to create the relationship between these components.</span></span> <span data-ttu-id="87cff-111">대형 앱의 경우 앱을 별도의 고급 기능 영역으로 나누는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-111">For a large app, it may be advantageous to partition the app into separate high level areas of functionality.</span></span> <span data-ttu-id="87cff-112">결제, 청구 및 검색과 같은 여러 비즈니스 단위가 있는 전자상거래 앱을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-112">For instance, an e-commerce app with multiple business units, such as checkout, billing, and search.</span></span> <span data-ttu-id="87cff-113">이러한 각 단위에는 보기, 컨트롤러, Razor Pages 및 모델을 포함하는 고유의 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-113">Each of these units have their own area to contain views, controllers, Razor Pages, and models.</span></span>

<span data-ttu-id="87cff-114">다음과 같은 경우 프로젝트에서 영역을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-114">Consider using Areas in an project when:</span></span>

* <span data-ttu-id="87cff-115">앱은 논리적으로 분리할 수 있는 여러 개의 고급 기능 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-115">The app is made of multiple high-level functional components that can be logically separated.</span></span>
* <span data-ttu-id="87cff-116">각 기능 영역을 독립적으로 작업할 수 있도록 앱을 파티션하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-116">You want to partition the app so that each functional area can be worked on independently.</span></span>

<span data-ttu-id="87cff-117">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/areas/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="87cff-117">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/areas/samples) ([how to download](xref:index#how-to-download-a-sample)).</span></span> <span data-ttu-id="87cff-118">다운로드 샘플은 테스트 영역에 대한 기본 앱을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-118">The download sample provides a basic app for testing areas.</span></span>

## <a name="areas-for-controllers-with-views"></a><span data-ttu-id="87cff-119">보기가 있는 컨트롤러 영역</span><span class="sxs-lookup"><span data-stu-id="87cff-119">Areas for controllers with views</span></span>

<span data-ttu-id="87cff-120">영역, 컨트롤러 및 보기를 사용하는 일반적인 ASP.NET Core 웹앱에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-120">A typical ASP.NET Core web app using areas, controllers, and views contains the following:</span></span>

* <span data-ttu-id="87cff-121">[영역 폴더 구조](#area-folder-structure).</span><span class="sxs-lookup"><span data-stu-id="87cff-121">An [Area folder structure](#area-folder-structure).</span></span>
* <span data-ttu-id="87cff-122">컨트롤러를 [&lbrack;영역&rbrack;](#attribute) 특성으로 데코레이트하여 해당 영역([!code-csharp[](areas/samples/MVCareas/Areas/Products/Controllers/ManageController.cs?name=snippet2)])과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-122">Controllers decorated with the [&lbrack;Area&rbrack;](#attribute) attribute to associate the controller with the area: [!code-csharp[](areas/samples/MVCareas/Areas/Products/Controllers/ManageController.cs?name=snippet2)]</span></span>
* <span data-ttu-id="87cff-123">[시작 시 영역 경로 추가](#add-area-route): [!code-csharp[](areas/samples/MVCareas/Startup.cs?name=snippet2&highlight=3-6)]</span><span class="sxs-lookup"><span data-stu-id="87cff-123">The [area route added to startup](#add-area-route): [!code-csharp[](areas/samples/MVCareas/Startup.cs?name=snippet2&highlight=3-6)]</span></span>

## <a name="area-folder-structure"></a><span data-ttu-id="87cff-124">영역 폴더 구조</span><span class="sxs-lookup"><span data-stu-id="87cff-124">Area folder structure</span></span>
<span data-ttu-id="87cff-125">*제품* 및 *서비스*의 두 논리 그룹이 있는 앱을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-125">Consider an app that has two logical groups, *Products* and *Services*.</span></span> <span data-ttu-id="87cff-126">영역을 사용하면 폴더 구조는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-126">Using areas, the folder structure would be similar to the following:</span></span>

* <span data-ttu-id="87cff-127">프로젝트 이름</span><span class="sxs-lookup"><span data-stu-id="87cff-127">Project name</span></span>
  * <span data-ttu-id="87cff-128">영역</span><span class="sxs-lookup"><span data-stu-id="87cff-128">Areas</span></span>
    * <span data-ttu-id="87cff-129">제품</span><span class="sxs-lookup"><span data-stu-id="87cff-129">Products</span></span>
      * <span data-ttu-id="87cff-130">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="87cff-130">Controllers</span></span>
        * <span data-ttu-id="87cff-131">HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="87cff-131">HomeController.cs</span></span>
        * <span data-ttu-id="87cff-132">ManageController.cs</span><span class="sxs-lookup"><span data-stu-id="87cff-132">ManageController.cs</span></span>
      * <span data-ttu-id="87cff-133">보기</span><span class="sxs-lookup"><span data-stu-id="87cff-133">Views</span></span>
        * <span data-ttu-id="87cff-134">홈</span><span class="sxs-lookup"><span data-stu-id="87cff-134">Home</span></span>
          * <span data-ttu-id="87cff-135">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="87cff-135">Index.cshtml</span></span>
        * <span data-ttu-id="87cff-136">관리</span><span class="sxs-lookup"><span data-stu-id="87cff-136">Manage</span></span>
          * <span data-ttu-id="87cff-137">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="87cff-137">Index.cshtml</span></span>
          * <span data-ttu-id="87cff-138">About.cshtml</span><span class="sxs-lookup"><span data-stu-id="87cff-138">About.cshtml</span></span>
    * <span data-ttu-id="87cff-139">서비스</span><span class="sxs-lookup"><span data-stu-id="87cff-139">Services</span></span>
      * <span data-ttu-id="87cff-140">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="87cff-140">Controllers</span></span>
        * <span data-ttu-id="87cff-141">HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="87cff-141">HomeController.cs</span></span>
      * <span data-ttu-id="87cff-142">보기</span><span class="sxs-lookup"><span data-stu-id="87cff-142">Views</span></span>
        * <span data-ttu-id="87cff-143">홈</span><span class="sxs-lookup"><span data-stu-id="87cff-143">Home</span></span>
          * <span data-ttu-id="87cff-144">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="87cff-144">Index.cshtml</span></span>

<span data-ttu-id="87cff-145">영역을 사용할 때 이전 레이아웃이 일반적이지만, 이 폴더 구조를 사용하려면 보기 파일만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-145">While the preceding layout is typical when using Areas, only the view files are required to use this folder structure.</span></span> <span data-ttu-id="87cff-146">보기 검색은 일치하는 영역 보기 파일을 다음 순서로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-146">View discovery searches for a matching area view file in the following order:</span></span>

```text
/Areas/<Area-Name>/Views/<Controller-Name>/<Action-Name>.cshtml
/Areas/<Area-Name>/Views/Shared/<Action-Name>.cshtml
/Views/Shared/<Action-Name>.cshtml
/Pages/Shared/<Action-Name>.cshtml
   ```

<span data-ttu-id="87cff-147">*컨트롤러* 및 *모델*과 같은 보기가 아닌 폴더의 위치는 중요하지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="87cff-147">The location of non-view folders like *Controllers* and *Models* does **not** matter.</span></span> <span data-ttu-id="87cff-148">예를 들어 *컨트롤러* 및 *모델* 폴더는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-148">For example, the *Controllers* and *Models* folder are not required.</span></span> <span data-ttu-id="87cff-149">*컨트롤러* 및 *모델*의 내용은 .dll로 컴파일되는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-149">The content of *Controllers* and *Models* is code which gets compiled into a .dll.</span></span> <span data-ttu-id="87cff-150">*보기*의 내용은 해당 보기에 대한 요청이 있을 때까지 컴파일되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-150">The content of the *Views* isn't compiled until a request to that view has been made.</span></span>

<!-- TODO review:
The content of the *Views* isn't compiled until a request to that view has been made.

What about precompiled views? 
 -->
<a name="attribute"></a>

### <a name="associate-the-controller-with-an-area"></a><span data-ttu-id="87cff-151">컨트롤러를 영역과 연결</span><span class="sxs-lookup"><span data-stu-id="87cff-151">Associate the controller with an Area</span></span>

<span data-ttu-id="87cff-152">영역 컨트롤러는 [&lbrack;영역&rbrack;](xref:Microsoft.AspNetCore.Mvc.AreaAttribute) 특성으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-152">Area controllers are designated with the [&lbrack;Area&rbrack;](xref:Microsoft.AspNetCore.Mvc.AreaAttribute) attribute:</span></span>

[!code-csharp[](areas/samples/MVCareas/Areas/Products/Controllers/ManageController.cs?highlight=5&name=snippet)]

### <a name="add-area-route"></a><span data-ttu-id="87cff-153">영역 경로 추가</span><span class="sxs-lookup"><span data-stu-id="87cff-153">Add Area route</span></span>

<span data-ttu-id="87cff-154">영역 경로는 일반적으로 특성 라우팅보다는 규칙 기반 라우팅을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-154">Area routes typically use conventional routing rather than attribute routing.</span></span> <span data-ttu-id="87cff-155">규칙 기반 라우팅은 순서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-155">Conventional routing is order-dependent.</span></span> <span data-ttu-id="87cff-156">일반적으로 영역이 있는 경로는 영역이 없는 경로에 비해 구체적이기 때문에 경로 테이블의 앞부분에 배치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-156">In general, routes with areas should be placed earlier in the route table as they're more specific than routes without an area.</span></span>

<span data-ttu-id="87cff-157">모든 영역에서 url 공간이 통일된 경우 `{area:...}`를 경로 템플릿의 토큰으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-157">`{area:...}` can be used as a token in route templates if url space is uniform across all areas:</span></span>

[!code-csharp[](areas/samples/MVCareas/Startup.cs?name=snippet&highlight=18-21)]

<span data-ttu-id="87cff-158">앞의 코드에서 `exists`는 경로가 영역과 일치해야 한다는 제한 조건을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-158">In the preceding code, `exists` applies a constraint that the route must match an area.</span></span> <span data-ttu-id="87cff-159">`{area:...}`를 사용하는 것은 영역에 라우팅을 추가하는 가장 간단한 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-159">Using `{area:...}` is the least complicated mechanism to adding routing to areas.</span></span>

<span data-ttu-id="87cff-160">다음 코드는 <xref:Microsoft.AspNetCore.Builder.MvcAreaRouteBuilderExtensions.MapAreaRoute*>를 사용하여 명명된 두 개의 영역 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-160">The following code uses <xref:Microsoft.AspNetCore.Builder.MvcAreaRouteBuilderExtensions.MapAreaRoute*> to create two named area routes:</span></span>

[!code-csharp[](areas/samples/MVCareas/StartupMapAreaRoute.cs?name=snippet&highlight=18-27)]

<span data-ttu-id="87cff-161">ASP.NET Core 2.2와 함께 `MapAreaRoute`를 사용하는 경우 [이 GitHub 문제](https://github.com/aspnet/AspNetCore/issues/7772)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87cff-161">When using `MapAreaRoute` with ASP.NET Core 2.2, see [this GitHub issue](https://github.com/aspnet/AspNetCore/issues/7772).</span></span>

<span data-ttu-id="87cff-162">자세한 내용은 [영역 라우팅](xref:mvc/controllers/routing#areas)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87cff-162">For more information, see [Area routing](xref:mvc/controllers/routing#areas).</span></span>

### <a name="link-generation-with-areas"></a><span data-ttu-id="87cff-163">영역과 링크 생성</span><span class="sxs-lookup"><span data-stu-id="87cff-163">Link Generation with Areas</span></span>

<span data-ttu-id="87cff-164">[샘플 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/areas/samples)의 다음 코드는 지정된 영역과 링크 생성을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-164">The following code from the [sample download](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/areas/samples) shows link generation with the area specified:</span></span>

[!code-cshtml[](areas/samples/MVCareas/Views/Shared/_testLinksPartial.cshtml?name=snippet)]

<span data-ttu-id="87cff-165">앞의 코드로 생성된 링크는 앱의 어느 위치에서나 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-165">The links generated with the preceding code are valid anywhere in the app.</span></span>

<span data-ttu-id="87cff-166">샘플 다운로드에는 영역을 지정하지 않고 위의 링크 및 동일한 링크를 포함하는 [부분 뷰](xref:mvc/views/partial)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-166">The sample download includes a [partial view](xref:mvc/views/partial) that contains the preceding links and the same links without specifying the area.</span></span> <span data-ttu-id="87cff-167">부분 뷰는 [레이아웃 파일]()에서 참조되므로, 앱의 모든 페이지에 생성된 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-167">The partial view is referenced in the [layout file](), so every page in the app displays the generated links.</span></span> <span data-ttu-id="87cff-168">영역을 지정하지 않고 생성된 링크는 동일한 영역 및 컨트롤러 페이지에서 참조할 때만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-168">The links generated without specifying the area are only valid when referenced from a page in the same area and controller.</span></span>

<span data-ttu-id="87cff-169">영역 또는 컨트롤러를 지정하지 않으면 라우팅은 *앰비언트* 값에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-169">When the area or controller is not specified, routing depends on the *ambient* values.</span></span> <span data-ttu-id="87cff-170">현재 요청의 현재 경로 값은 링크 생성에 대한 앰비언트 값으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-170">The current route values of the current request are considered ambient values for link generation.</span></span> <span data-ttu-id="87cff-171">샘플 앱의 대부분의 경우 앰비언트 값을 사용하면 잘못된 링크가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-171">In many cases for the sample app, using the ambient values generates incorrect links.</span></span>

<span data-ttu-id="87cff-172">자세한 정보는 [컨트롤러 작업에 라우팅](xref:mvc/controllers/routing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87cff-172">For more information, see [Routing to controller actions](xref:mvc/controllers/routing).</span></span>

### <a name="shared-layout-for-areas-using-the-viewstartcshtml-file"></a><span data-ttu-id="87cff-173">_ViewStart.cshtml 파일을 사용하여 영역에 대한 레이아웃 공유</span><span class="sxs-lookup"><span data-stu-id="87cff-173">Shared layout for Areas using the _ViewStart.cshtml file</span></span>

<span data-ttu-id="87cff-174">전체 앱의 일반적인 레이아웃을 공유하려면 *_ViewStart.cshtml*을 애플리케이션 루트 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-174">To share a common layout for the entire app, move the *_ViewStart.cshtml* to the application root folder.</span></span>

<!-- This section will be completed after https://github.com/aspnet/Docs/pull/10978 is merged.
<a name="arp"></a>

## Areas for Razor Pages
-->
<a name="rename"></a>

### <a name="change-default-area-folder-where-views-are-stored"></a><span data-ttu-id="87cff-175">보기가 저장된 기본 영역 폴더 변경</span><span class="sxs-lookup"><span data-stu-id="87cff-175">Change default area folder where views are stored</span></span>

<span data-ttu-id="87cff-176">다음 코드는 기본 영역 폴더를 `"Areas"`에서 `"MyAreas"`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-176">The following code changes the default area folder from `"Areas"` to `"MyAreas"`:</span></span>

[!code-csharp[](areas/samples/MVCareas/Startup2.cs?name=snippet)]

<!-- TODO review - can we delete this. Areas doesn't change publishing - right? -->
### <a name="publishing-areas"></a><span data-ttu-id="87cff-177">영역 게시</span><span class="sxs-lookup"><span data-stu-id="87cff-177">Publishing Areas</span></span>

<span data-ttu-id="87cff-178">`<Project Sdk="Microsoft.NET.Sdk.Web">`이 *.csproj* 파일에 포함되면 모든 `*.cshtml` 및 `wwwroot/**` 파일이 출력으로 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="87cff-178">All `*.cshtml` and `wwwroot/**` files are published to output when `<Project Sdk="Microsoft.NET.Sdk.Web">` is included in the *.csproj* file.</span></span>
