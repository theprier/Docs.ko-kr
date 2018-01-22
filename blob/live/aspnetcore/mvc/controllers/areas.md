---
title: "영역"
author: rick-anderson
description: "영역을 사용 하는 방법을 보여 줍니다."
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/controllers/areas
ms.openlocfilehash: 666be2da6b38ffb538ae3888ea879a4104c8fd12
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="areas"></a><span data-ttu-id="4f655-103">영역</span><span class="sxs-lookup"><span data-stu-id="4f655-103">Areas</span></span>

<span data-ttu-id="4f655-104">여 [Dhananjay Kumar](https://twitter.com/debug_mode) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4f655-104">By [Dhananjay Kumar](https://twitter.com/debug_mode)  and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="4f655-105">영역은 별도 네임 스페이스 (라우팅) 및 (views)에 대 한 폴더 구조와 관련 된 기능 그룹으로 구성 하는 데 사용 되는 ASP.NET MVC 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-105">Areas are an ASP.NET MVC feature used to organize related functionality into a group as a separate namespace (for routing) and folder structure (for views).</span></span> <span data-ttu-id="4f655-106">영역을 사용 하 여 다른 경로 매개 변수를 추가 하 여 라우팅 목적으로 계층 구조를 만듭니다 `area`을 `controller` 및 `action`합니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-106">Using areas creates a hierarchy for the purpose of routing by adding another route parameter, `area`, to `controller` and `action`.</span></span>

<span data-ttu-id="4f655-107">영역은 여러 개의 작은 기능 그룹으로 큰 ASP.NET Core MVC 웹 응용 프로그램을 분할 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-107">Areas provide a way to partition a large ASP.NET Core MVC Web app into smaller functional groupings.</span></span> <span data-ttu-id="4f655-108">실질적으로 영역은 응용 프로그램 내의 MVC 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-108">An area is effectively an MVC structure inside an application.</span></span> <span data-ttu-id="4f655-109">MVC 프로젝트에서 모델, 컨트롤러 및 보기와 같은 논리적 구성 요소는 서로 다른 폴더에 저장 하는 및 MVC 명명 규칙을 사용 하 여 이러한 구성 요소 간의 관계를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-109">In an MVC project, logical components like Model, Controller, and View are kept in different folders, and MVC uses naming conventions to create the relationship between these components.</span></span> <span data-ttu-id="4f655-110">규모가 큰 앱에 대 한 별도 높은 수준의 기능 영역을를 응용 프로그램을 분할 하는 것이 도움이 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-110">For a large app, it may be advantageous to partition the  app into separate high level areas of functionality.</span></span> <span data-ttu-id="4f655-111">예를 들어, 체크 아웃, 청구 및 검색 등과 같은 여러 비즈니스 단위를 사용 하 여 전자 상거래 앱입니다. 각 이러한 단위가 있는 자신의 논리적 구성 요소 뷰, 컨트롤러 및 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-111">For instance, an e-commerce app with multiple business units, such as checkout, billing, and search etc. Each of these units have their own logical component views, controllers, and models.</span></span> <span data-ttu-id="4f655-112">이 시나리오에서는 물리적으로 같은 프로젝트에 비즈니스 구성 요소를 분할 영역을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-112">In this scenario, you can use Areas to physically partition the business components in the same project.</span></span>

<span data-ttu-id="4f655-113">영역은 컨트롤러, 뷰 및 모델의 자체 집합으로 ASP.NET Core MVC 프로젝트에 기능 단위 보다 작은으로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-113">An area can be defined as smaller functional units in an ASP.NET Core MVC project with its own set of controllers, views, and models.</span></span>

<span data-ttu-id="4f655-114">MVC의 영역을 사용 하는 것이 좋습니다. 때 프로젝트:</span><span class="sxs-lookup"><span data-stu-id="4f655-114">Consider using Areas in an MVC project when:</span></span>

* <span data-ttu-id="4f655-115">응용 프로그램은 논리적으로 분리 해야 하는 여러 기능 높은 수준의 구성 요소 구성</span><span class="sxs-lookup"><span data-stu-id="4f655-115">Your application is made of multiple high-level functional components that should be logically separated</span></span>

* <span data-ttu-id="4f655-116">각 기능 영역 수 수에 독립적으로 작업 않도록 MVC 프로젝트를 분할.</span><span class="sxs-lookup"><span data-stu-id="4f655-116">You want to partition your MVC project so that each functional area can be worked on independently</span></span>

<span data-ttu-id="4f655-117">영역 기능:</span><span class="sxs-lookup"><span data-stu-id="4f655-117">Area features:</span></span>

* <span data-ttu-id="4f655-118">ASP.NET Core MVC 응용 프로그램에 다양 한 영역의 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-118">An ASP.NET Core MVC app can have any number of areas</span></span>

* <span data-ttu-id="4f655-119">각 영역에는 자체 컨트롤러, 모델 및 뷰</span><span class="sxs-lookup"><span data-stu-id="4f655-119">Each area has its own controllers, models, and views</span></span>

* <span data-ttu-id="4f655-120">있습니다. 수에 독립적으로 작업을 여러 높은 수준의 구성 요소에 대형 MVC 프로젝트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-120">Allows you to organize large MVC projects into multiple high-level components that can be worked on independently</span></span>

* <span data-ttu-id="4f655-121">서로 다른으로 동일한 이름의 여러 컨트롤러 지원 *영역*</span><span class="sxs-lookup"><span data-stu-id="4f655-121">Supports multiple controllers with the same name - as long as they have different *areas*</span></span>

<span data-ttu-id="4f655-122">영역 생성 및 사용 방법을 설명 하는 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-122">Let's take a look at an example to illustrate how Areas are created and used.</span></span> <span data-ttu-id="4f655-123">컨트롤러와 뷰의 두 가지 그룹화 된 스토어 앱이 있는 경우를 가정해: 제품 및 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-123">Let's say you have a store app that has two distinct groupings of controllers and views: Products and Services.</span></span> <span data-ttu-id="4f655-124">MVC 영역을 사용 하 여 다음과 같은 아래에 대 한 일반적인 폴더 구조:</span><span class="sxs-lookup"><span data-stu-id="4f655-124">A typical folder structure for that using MVC areas looks like below:</span></span>

* <span data-ttu-id="4f655-125">프로젝트 이름</span><span class="sxs-lookup"><span data-stu-id="4f655-125">Project name</span></span>

  * <span data-ttu-id="4f655-126">영역</span><span class="sxs-lookup"><span data-stu-id="4f655-126">Areas</span></span>

    * <span data-ttu-id="4f655-127">제품</span><span class="sxs-lookup"><span data-stu-id="4f655-127">Products</span></span>

      * <span data-ttu-id="4f655-128">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="4f655-128">Controllers</span></span>

        * <span data-ttu-id="4f655-129">HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="4f655-129">HomeController.cs</span></span>

        * <span data-ttu-id="4f655-130">ManageController.cs</span><span class="sxs-lookup"><span data-stu-id="4f655-130">ManageController.cs</span></span>

      * <span data-ttu-id="4f655-131">보기</span><span class="sxs-lookup"><span data-stu-id="4f655-131">Views</span></span>

        * <span data-ttu-id="4f655-132">홈</span><span class="sxs-lookup"><span data-stu-id="4f655-132">Home</span></span>

          * <span data-ttu-id="4f655-133">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="4f655-133">Index.cshtml</span></span>

        * <span data-ttu-id="4f655-134">관리</span><span class="sxs-lookup"><span data-stu-id="4f655-134">Manage</span></span>

          * <span data-ttu-id="4f655-135">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="4f655-135">Index.cshtml</span></span>

    * <span data-ttu-id="4f655-136">서비스</span><span class="sxs-lookup"><span data-stu-id="4f655-136">Services</span></span>

      * <span data-ttu-id="4f655-137">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="4f655-137">Controllers</span></span>

        * <span data-ttu-id="4f655-138">HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="4f655-138">HomeController.cs</span></span>

      * <span data-ttu-id="4f655-139">보기</span><span class="sxs-lookup"><span data-stu-id="4f655-139">Views</span></span>

        * <span data-ttu-id="4f655-140">홈</span><span class="sxs-lookup"><span data-stu-id="4f655-140">Home</span></span>

          * <span data-ttu-id="4f655-141">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="4f655-141">Index.cshtml</span></span>

<span data-ttu-id="4f655-142">MVC을 기본적으로는 영역에는 뷰를 렌더링 하려고 하는 경우 다음 위치에서 찾을 시도:</span><span class="sxs-lookup"><span data-stu-id="4f655-142">When MVC tries to render a view in an Area, by default, it tries to look in the following locations:</span></span>

```text
/Areas/<Area-Name>/Views/<Controller-Name>/<Action-Name>.cshtml
   /Areas/<Area-Name>/Views/Shared/<Action-Name>.cshtml
   /Views/Shared/<Action-Name>.cshtml
   ```

<span data-ttu-id="4f655-143">이 위치는 통해 변경할 수 있는 기본 위치는 `AreaViewLocationFormats` 에 `Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions`합니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-143">These are the default locations which can be changed via the `AreaViewLocationFormats` on the `Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions`.</span></span>

<span data-ttu-id="4f655-144">예를 들어는 아래 '영역'으로 폴더 이름을 포함 하는 대신 코드를 변경 된 '범주'에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-144">For example, in the below code instead of having the folder name as 'Areas', it has been changed to 'Categories'.</span></span>

```csharp
services.Configure<RazorViewEngineOptions>(options =>
   {
       options.AreaViewLocationFormats.Clear();
       options.AreaViewLocationFormats.Add("/Categories/{2}/Views/{1}/{0}.cshtml");
       options.AreaViewLocationFormats.Add("/Categories/{2}/Views/Shared/{0}.cshtml");
       options.AreaViewLocationFormats.Add("/Views/Shared/{0}.cshtml");
   });
   ```

<span data-ttu-id="4f655-145">한 가지 주의할 점은의 구조는 *뷰* 폴더는 유일 하 게 여기 중요 한 선호 되 고 나머지 폴더의 콘텐츠 형식 *컨트롤러* 및 *모델* 않습니다 **하지** 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-145">One thing to note is that the structure of the *Views* folder is the only one which is considered important here and the content of the rest of the folders like *Controllers* and *Models* does **not** matter.</span></span> <span data-ttu-id="4f655-146">예를 들어 필요 하면는 *컨트롤러* 및 *모델* 전혀 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-146">For example, you need not have a *Controllers* and *Models* folder at all.</span></span> <span data-ttu-id="4f655-147">하므로이 작업이 내용의 *컨트롤러* 및 *모델* 는의 내용으로 작업 하는 경우.dll으로 컴파일 가져옵니다 정당한 코드는 *뷰* 가 요청을 하는 되어야만 보기는 다음과 같이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-147">This works because the content of *Controllers* and *Models* is just code which gets compiled into a .dll where as the content of the *Views* is not until a request to that view has been made.</span></span>

<span data-ttu-id="4f655-148">폴더 계층 구조를 정의 하 고 나면 영역 연결 된 각 컨트롤러에 MVC를 지시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-148">Once you've defined the folder hierarchy, you need to tell MVC that each controller is associated with an area.</span></span> <span data-ttu-id="4f655-149">그렇게 하려면 사용 하 여 컨트롤러 이름을 데코레이팅하여는 `[Area]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-149">You do that by decorating the controller name with the `[Area]` attribute.</span></span>

```csharp
...
   namespace MyStore.Areas.Products.Controllers
   {
       [Area("Products")]
       public class HomeController : Controller
       {
           // GET: /Products/Home/Index
           public IActionResult Index()
           {
               return View();
           }

           // GET: /Products/Home/Create
           public IActionResult Create()
           {
               return View();
           }
       }
   }
   ```

<span data-ttu-id="4f655-150">새로 만든된 사용자 영역을 사용 하는 경로 정의를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-150">Set up a route definition that works with your newly created areas.</span></span> <span data-ttu-id="4f655-151">[컨트롤러 작업에 대 한 라우팅을](routing.md) 문서 특성 경로와 규칙에 따른 경로 사용 하는 등의 route 정의 만드는 방법에 대 한 정보를 확인할 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-151">The [Routing to Controller Actions](routing.md) article goes into detail about how to create route definitions, including using conventional routes versus attribute routes.</span></span> <span data-ttu-id="4f655-152">이 예제에서는 규칙에 따른 경로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-152">In this example, we'll use a conventional route.</span></span> <span data-ttu-id="4f655-153">이 위해 열고는 *Startup.cs* 파일을 추가 하 여 수정는 `areaRoute` 라는 아래 경로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-153">To do so, open the *Startup.cs* file and modify it by adding the `areaRoute` named route definition below.</span></span>

```csharp
...
   app.UseMvc(routes =>
   {
     routes.MapRoute(
         name: "areaRoute",
         template: "{area:exists}/{controller=Home}/{action=Index}/{id?}");

     routes.MapRoute(
         name: "default",
         template: "{controller=Home}/{action=Index}/{id?}");
   });
   ```

<span data-ttu-id="4f655-154">찾아 `http://<yourApp>/products`, `Index` 의 동작 메서드는 `HomeController` 에 `Products` 영역 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-154">Browsing to `http://<yourApp>/products`, the `Index` action method of the `HomeController` in the `Products` area will be invoked.</span></span>

## <a name="link-generation"></a><span data-ttu-id="4f655-155">링크 생성</span><span class="sxs-lookup"><span data-stu-id="4f655-155">Link Generation</span></span>

* <span data-ttu-id="4f655-156">컨트롤러를 같은 컨트롤러 내에서 다른 작업을 기반으로 작업 영역 내에서 링크를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-156">Generating links from an action within an area based controller to another action within the same controller.</span></span>

  <span data-ttu-id="4f655-157">현재 요청 경로 같은 경우를 가정해합니다`/Products/Home/Create`</span><span class="sxs-lookup"><span data-stu-id="4f655-157">Let's say the current request's path is like `/Products/Home/Create`</span></span>

  <span data-ttu-id="4f655-158">HtmlHelper 구문을 사용 하십시오.`@Html.ActionLink("Go to Product's Home Page", "Index")`</span><span class="sxs-lookup"><span data-stu-id="4f655-158">HtmlHelper syntax: `@Html.ActionLink("Go to Product's Home Page", "Index")`</span></span>

  <span data-ttu-id="4f655-159">TagHelper 구문을 사용 하십시오.`<a asp-action="Index">Go to Product's Home Page</a>`</span><span class="sxs-lookup"><span data-stu-id="4f655-159">TagHelper syntax: `<a asp-action="Index">Go to Product's Home Page</a>`</span></span>

  <span data-ttu-id="4f655-160">'영역' 및 'controller' 값 제공 하지 않아도 म 참고 여기에 현재 요청의 컨텍스트에서 사용할 수 있는 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-160">Note that we need not supply the 'area' and 'controller' values here as they are already available in the context of the current request.</span></span> <span data-ttu-id="4f655-161">이러한 종류의 값 이라고 `ambient` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-161">These kind of values are called `ambient` values.</span></span>

* <span data-ttu-id="4f655-162">컨트롤러를 다른 컨트롤러에 다른 작업을 기반으로 작업 영역 내에서 링크를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-162">Generating links from an action within an area based controller to another action on a different controller</span></span>

  <span data-ttu-id="4f655-163">현재 요청 경로 같은 경우를 가정해합니다`/Products/Home/Create`</span><span class="sxs-lookup"><span data-stu-id="4f655-163">Let's say the current request's path is like `/Products/Home/Create`</span></span>

  <span data-ttu-id="4f655-164">HtmlHelper 구문을 사용 하십시오.`@Html.ActionLink("Go to Manage Products’  Home Page", "Index", "Manage")`</span><span class="sxs-lookup"><span data-stu-id="4f655-164">HtmlHelper syntax: `@Html.ActionLink("Go to Manage Products’  Home Page", "Index", "Manage")`</span></span>

  <span data-ttu-id="4f655-165">TagHelper 구문을 사용 하십시오.`<a asp-controller="Manage" asp-action="Index">Go to Manage Products’  Home Page</a>`</span><span class="sxs-lookup"><span data-stu-id="4f655-165">TagHelper syntax: `<a asp-controller="Manage" asp-action="Index">Go to Manage Products’  Home Page</a>`</span></span>

  <span data-ttu-id="4f655-166">Note 앰비언트 값 '영역'를 사용 하는 여기 하지만 위에서 'controller' 값은 명시적으로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-166">Note that here the ambient value of an 'area' is used but the 'controller' value is specified explicitly above.</span></span>

* <span data-ttu-id="4f655-167">다른 컨트롤러와 다른 영역에 컨트롤러를 다른 작업 기반 작업 영역 내에서 링크를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-167">Generating links from an action within an area based controller to another action on a different controller and a different area.</span></span>

  <span data-ttu-id="4f655-168">현재 요청 경로 같은 경우를 가정해합니다`/Products/Home/Create`</span><span class="sxs-lookup"><span data-stu-id="4f655-168">Let's say the current request's path is like `/Products/Home/Create`</span></span>

  <span data-ttu-id="4f655-169">HtmlHelper 구문을 사용 하십시오.`@Html.ActionLink("Go to Services’ Home Page", "Index", "Home", new { area = "Services" })`</span><span class="sxs-lookup"><span data-stu-id="4f655-169">HtmlHelper syntax: `@Html.ActionLink("Go to Services’ Home Page", "Index", "Home", new { area = "Services" })`</span></span>

  <span data-ttu-id="4f655-170">TagHelper 구문을 사용 하십시오.`<a asp-area="Services" asp-controller="Home" asp-action="Index">Go to Services’ Home Page</a>`</span><span class="sxs-lookup"><span data-stu-id="4f655-170">TagHelper syntax: `<a asp-area="Services" asp-controller="Home" asp-action="Index">Go to Services’ Home Page</a>`</span></span>

  <span data-ttu-id="4f655-171">앰비언트 값이 없는 여기서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-171">Note that here no ambient values are used.</span></span>

* <span data-ttu-id="4f655-172">이 지역의 컨트롤러 내에서 액션에서 다른 컨트롤러에 다른 작업에 링크를 생성 하 고 **하지** 영역에서입니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-172">Generating links from an action within an area based controller to another action on a different controller and **not** in an area.</span></span>

  <span data-ttu-id="4f655-173">HtmlHelper 구문을 사용 하십시오.`@Html.ActionLink("Go to Manage Products’  Home Page", "Index", "Home", new { area = "" })`</span><span class="sxs-lookup"><span data-stu-id="4f655-173">HtmlHelper syntax: `@Html.ActionLink("Go to Manage Products’  Home Page", "Index", "Home", new { area = "" })`</span></span>

  <span data-ttu-id="4f655-174">TagHelper 구문을 사용 하십시오.`<a asp-area="" asp-controller="Manage" asp-action="Index">Go to Manage Products’  Home Page</a>`</span><span class="sxs-lookup"><span data-stu-id="4f655-174">TagHelper syntax: `<a asp-area="" asp-controller="Manage" asp-action="Index">Go to Manage Products’  Home Page</a>`</span></span>

  <span data-ttu-id="4f655-175">생성 하는 데는 비 영역에 대 한 링크 기반에서는 빈 컨트롤러 동작 '영역' 여기에 대 한 앰비언트 값</span><span class="sxs-lookup"><span data-stu-id="4f655-175">Since we want to generate links to a non-area based controller action, we empty the ambient value for 'area' here.</span></span>

## <a name="publishing-areas"></a><span data-ttu-id="4f655-176">게시 영역</span><span class="sxs-lookup"><span data-stu-id="4f655-176">Publishing Areas</span></span>

<span data-ttu-id="4f655-177">모든 `*.cshtml` 및 `wwwroot/**` 파일 경우 출력을 게시할 `<Project Sdk="Microsoft.NET.Sdk.Web">` 에 포함 되어는 *.csproj* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4f655-177">All `*.cshtml` and `wwwroot/**` files are published to output when `<Project Sdk="Microsoft.NET.Sdk.Web">` is included in the *.csproj* file.</span></span>
