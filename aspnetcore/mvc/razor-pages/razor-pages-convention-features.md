---
title: "ASP.NET Core에서 Razor 페이지 경로 및 앱 규칙 기능"
author: guardrex
description: "경로 및 앱 모델 공급자 규칙 기능을 통해 페이지 라우팅, 검색 및 처리를 제어하는 방법을 검색합니다."
manager: wpickett
ms.author: riande
ms.date: 10/23/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/razor-pages/razor-pages-convention-features
ms.openlocfilehash: bf1c895fc972310d5541d0098226d58b8183e320
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="razor-pages-route-and-app-convention-features-in-aspnet-core"></a><span data-ttu-id="c38f9-103">ASP.NET Core에서 Razor 페이지 경로 및 앱 규칙 기능</span><span class="sxs-lookup"><span data-stu-id="c38f9-103">Razor Pages route and app convention features in ASP.NET Core</span></span>

<span data-ttu-id="c38f9-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="c38f9-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="c38f9-105">페이지 경로 및 앱 모델 공급자 규칙 기능을 사용하여 Razor 페이지 앱에서 페이지 라우팅, 검색 및 처리를 제어하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-105">Learn how to use page route and app model provider convention features to control page routing, discovery, and processing in Razor Pages apps.</span></span> <span data-ttu-id="c38f9-106">개별 페이지에 대한 사용자 지정 페이지 경로를 구성해야 하는 경우 이 항목의 뒷부분에서 설명할 [AddPageRoute 규칙](#configure-a-page-route)을 사용하여 페이지에 대한 라우팅을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-106">When you need to configure custom page routes for individual pages, configure routing to pages with the [AddPageRoute convention](#configure-a-page-route) described later in this topic.</span></span>

<span data-ttu-id="c38f9-107">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/razor-pages-convention-features/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))을 사용하여 이 항목에서 설명한 기능을 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-107">Use the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/razor-pages-convention-features/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)) to explore the features described in this topic.</span></span>

| <span data-ttu-id="c38f9-108">기능</span><span class="sxs-lookup"><span data-stu-id="c38f9-108">Features</span></span> | <span data-ttu-id="c38f9-109">샘플에서는 다음 사항을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-109">The sample demonstrates ...</span></span> |
| -------- | --------------------------- |
| [<span data-ttu-id="c38f9-110">경로 및 앱 모델 규칙</span><span class="sxs-lookup"><span data-stu-id="c38f9-110">Route and app model conventions</span></span>](#add-route-and-app-model-conventions)<br><br><span data-ttu-id="c38f9-111">Conventions.Add</span><span class="sxs-lookup"><span data-stu-id="c38f9-111">Conventions.Add</span></span><ul><li><span data-ttu-id="c38f9-112">IPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="c38f9-112">IPageRouteModelConvention</span></span></li><li><span data-ttu-id="c38f9-113">IPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="c38f9-113">IPageApplicationModelConvention</span></span></li></ul> | <span data-ttu-id="c38f9-114">경로 템플릿 및 헤더를 앱의 페이지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-114">Adding a route template and header to an app's pages.</span></span> |
| [<span data-ttu-id="c38f9-115">페이지 경로 작업 규칙</span><span class="sxs-lookup"><span data-stu-id="c38f9-115">Page route action conventions</span></span>](#page-route-action-conventions)<ul><li><span data-ttu-id="c38f9-116">AddFolderRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="c38f9-116">AddFolderRouteModelConvention</span></span></li><li><span data-ttu-id="c38f9-117">AddPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="c38f9-117">AddPageRouteModelConvention</span></span></li><li><span data-ttu-id="c38f9-118">AddPageRoute</span><span class="sxs-lookup"><span data-stu-id="c38f9-118">AddPageRoute</span></span></li></ul> | <span data-ttu-id="c38f9-119">폴더에 있는 페이지 및 단일 페이지에 경로 템플릿을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-119">Adding a route template to pages in a folder and to a single page.</span></span> |
| [<span data-ttu-id="c38f9-120">페이지 모델 작업 규칙</span><span class="sxs-lookup"><span data-stu-id="c38f9-120">Page model action conventions</span></span>](#page-model-action-conventions)<ul><li><span data-ttu-id="c38f9-121">AddFolderApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="c38f9-121">AddFolderApplicationModelConvention</span></span></li><li><span data-ttu-id="c38f9-122">AddPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="c38f9-122">AddPageApplicationModelConvention</span></span></li><li><span data-ttu-id="c38f9-123">ConfigureFilter(필터 클래스, 람다 식 또는 필터 팩터리)</span><span class="sxs-lookup"><span data-stu-id="c38f9-123">ConfigureFilter (filter class, lambda expression, or filter factory)</span></span></li></ul> | <span data-ttu-id="c38f9-124">폴더의 페이지에 헤더를 추가하고, 단일 페이지에 헤더를 추가하고, [필터 팩토리](xref:mvc/controllers/filters#ifilterfactory)를 구성하여 헤더를 앱의 페이지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-124">Adding a header to pages in a folder, adding a header to a single page, and configuring a [filter factory](xref:mvc/controllers/filters#ifilterfactory) to add a header to an app's pages.</span></span> |
| [<span data-ttu-id="c38f9-125">기본 페이지 앱 모델 공급자</span><span class="sxs-lookup"><span data-stu-id="c38f9-125">Default page app model provider</span></span>](#replace-the-default-page-app-model-provider) | <span data-ttu-id="c38f9-126">기본 페이지 모델 공급자를 대체하여 처리기 이름 지정에 대한 규칙을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-126">Replacing the default page model provider to change the conventions for handler naming.</span></span> |

## <a name="add-route-and-app-model-conventions"></a><span data-ttu-id="c38f9-127">경로 및 앱 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="c38f9-127">Add route and app model conventions</span></span>

<span data-ttu-id="c38f9-128">[IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention)의 대리자를 추가하여 Razor 페이지에 적용되는 경로 및 앱 모델 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-128">Add a delegate for [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) to add route and app model conventions that apply to Razor Pages.</span></span>

<span data-ttu-id="c38f9-129">**모든 페이지에 경로 모델 규칙 추가**</span><span class="sxs-lookup"><span data-stu-id="c38f9-129">**Add a route model convention to all pages**</span></span>

<span data-ttu-id="c38f9-130">[규칙](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)을 사용하여 경로 및 페이지 모델을 구축하는 동안 적용되는 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 인스턴스의 컬렉션에 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)을 만들고 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-130">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during route and page model construction.</span></span>

<span data-ttu-id="c38f9-131">샘플 앱은 앱의 모든 페이지에 `{globalTemplate?}` 경로 템플릿을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-131">The sample app adds a `{globalTemplate?}` route template to all of the pages in the app:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Conventions/GlobalTemplatePageRouteModelConvention.cs?name=snippet1)]

> [!NOTE]
> <span data-ttu-id="c38f9-132">`AttributeRouteModel`의 `Order` 속성은 `0`(영)으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-132">The `Order` property for the `AttributeRouteModel` is set to `0` (zero).</span></span> <span data-ttu-id="c38f9-133">그러면 단일 경로 값을 제공하는 경우 이 템플릿이 첫 번째 경로 데이터 값 위치에 지정된 우선 순위가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-133">This ensures that this template is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="c38f9-134">예를 들어 샘플은 항목의 뒷부분에서 `{aboutTemplate?}` 경로 템플릿을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-134">For example, the sample adds an `{aboutTemplate?}` route template later in the topic.</span></span> <span data-ttu-id="c38f9-135">`{aboutTemplate?}` 템플릿이 `1`의 `Order`로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-135">The `{aboutTemplate?}` template is given an `Order` of `1`.</span></span> <span data-ttu-id="c38f9-136">`/About/RouteDataValue`에서 정보 페이지를 요청하는 경우 "RouteDataValue"는 `Order` 속성 설정으로 인해 `RouteData.Values["aboutTemplate"]`(`Order = 1`)이 아닌 `RouteData.Values["globalTemplate"]`(`Order = 0`)으로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-136">When the About page is requested at `/About/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 0`) and not `RouteData.Values["aboutTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="c38f9-137">*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="c38f9-137">*Startup.cs*:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet1)]

<span data-ttu-id="c38f9-138">`localhost:5000/About/GlobalRouteValue`에서 샘플의 정보 페이지를 요청하고 결과를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-138">Request the sample's About page at `localhost:5000/About/GlobalRouteValue` and inspect the result:</span></span>

![GlobalRouteValue의 경로 세그먼트를 사용하여 정보 페이지를 요청합니다.](razor-pages-convention-features/_static/about-page-global-template.png)

<span data-ttu-id="c38f9-141">**모든 페이지에 앱 모델 규칙 추가**</span><span class="sxs-lookup"><span data-stu-id="c38f9-141">**Add an app model convention to all pages**</span></span>

<span data-ttu-id="c38f9-142">[규칙](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)을 사용하여 경로 및 페이지 모델을 구축하는 동안 적용되는 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 인스턴스의 컬렉션에 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention)을 만들고 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-142">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during route and page model construction.</span></span>

<span data-ttu-id="c38f9-143">이 항목의 뒷부분에서 이 규칙 및 다른 규칙을 설명하기 위해 샘플 앱에는 `AddHeaderAttribute` 클래스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-143">To demonstrate this and other conventions later in the topic, the sample app includes an `AddHeaderAttribute` class.</span></span> <span data-ttu-id="c38f9-144">클래스 생성자가 `name` 문자열 및 `values` 문자열 배열을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-144">The class constructor accepts a `name` string and a `values` string array.</span></span> <span data-ttu-id="c38f9-145">이러한 값은 응답 헤더를 설정하는 `OnResultExecuting` 메서드에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-145">These values are used in its `OnResultExecuting` method to set a response header.</span></span> <span data-ttu-id="c38f9-146">전체 클래스는 항목의 뒷부분에 나오는 [페이지 모델 작업 규칙](#page-model-action-conventions) 섹션에서 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-146">The full class is shown in the [Page model action conventions](#page-model-action-conventions) section later in the topic.</span></span>

<span data-ttu-id="c38f9-147">샘플 앱에서는 앱의 모든 페이지에 `GlobalHeader` 헤더를 추가하는 `AddHeaderAttribute` 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-147">The sample app uses the `AddHeaderAttribute` class to add a header, `GlobalHeader`, to all of the pages in the app:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Conventions/GlobalHeaderPageApplicationModelConvention.cs?name=snippet1)]

<span data-ttu-id="c38f9-148">*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="c38f9-148">*Startup.cs*:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet2)]

<span data-ttu-id="c38f9-149">`localhost:5000/About`에서 샘플의 정보 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-149">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![정보 페이지의 응답 헤더는 GlobalHeader가 추가되었음을 보여줍니다.](razor-pages-convention-features/_static/about-page-global-header.png)

## <a name="page-route-action-conventions"></a><span data-ttu-id="c38f9-151">페이지 경로 작업 규칙</span><span class="sxs-lookup"><span data-stu-id="c38f9-151">Page route action conventions</span></span>

<span data-ttu-id="c38f9-152">[IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider)에서 파생되는 기본 경로 모델 공급자는 페이지 경로를 구성하기 위한 확장성 지점을 제공하도록 설계된 규칙을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-152">The default route model provider that derives from [IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider) invokes conventions which are designed to provide extensibility points for configuring page routes.</span></span>

<span data-ttu-id="c38f9-153">**폴더 경로 모델 규칙**</span><span class="sxs-lookup"><span data-stu-id="c38f9-153">**Folder route model convention**</span></span>

<span data-ttu-id="c38f9-154">[AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention)을 사용하여 지정된 폴더 아래에 있는 모든 페이지에 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel)에 대한 작업을 호출하는 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)을 만들고 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-154">Use [AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) that invokes an action on the [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) for all of the pages under the specified folder.</span></span>

<span data-ttu-id="c38f9-155">샘플 앱에서는 `AddFolderRouteModelConvention`를 사용하여 `{otherPagesTemplate?}` 경로 템플릿을 *OtherPages* 폴더의 페이지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-155">The sample app uses `AddFolderRouteModelConvention` to add an `{otherPagesTemplate?}` route template to the pages in the *OtherPages* folder:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet3)]

> [!NOTE]
> <span data-ttu-id="c38f9-156">`AttributeRouteModel`에 대한 `Order` 속성을 `1`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-156">The `Order` property for the `AttributeRouteModel` is set to `1`.</span></span> <span data-ttu-id="c38f9-157">그러면 단일 경로 값을 제공하는 경우 `{globalTemplate?}`에 대한 템플릿(항목의 앞에서 설정함)이 첫 번째 경로 데이터 값 위치에 지정된 우선 순위가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-157">This ensures that the template for `{globalTemplate?}` (set earlier in the topic) is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="c38f9-158">`/OtherPages/Page1/RouteDataValue`에서 Page1 페이지를 요청하는 경우 "RouteDataValue"는 `Order` 속성 설정으로 인해 `RouteData.Values["otherPagesTemplate"]`(`Order = 1`)이 아닌 `RouteData.Values["globalTemplate"]`(`Order = 0`)으로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-158">If the Page1 page is requested at `/OtherPages/Page1/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 0`) and not `RouteData.Values["otherPagesTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="c38f9-159">`localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue`에서 샘플의 Page1 페이지를 요청하고 결과를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-159">Request the sample's Page1 page at `localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue` and inspect the result:</span></span>

![OtherPages 폴더의 Page1은 GlobalRouteValue 및 OtherPagesRouteValue라는 경로 세그먼트를 사용하여 요청됩니다.](razor-pages-convention-features/_static/otherpages-page1-global-and-otherpages-templates.png)

<span data-ttu-id="c38f9-162">**페이지 경로 모델 규칙**</span><span class="sxs-lookup"><span data-stu-id="c38f9-162">**Page route model convention**</span></span>

<span data-ttu-id="c38f9-163">[AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention)을 사용하여 지정된 이름을 가진 페이지에 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel)에 대한 작업을 호출하는 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)을 만들고 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-163">Use [AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) that invokes an action on the [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) for the page with the specified name.</span></span>

<span data-ttu-id="c38f9-164">샘플 앱에서는 `AddPageRouteModelConvention`를 사용하여 `{aboutTemplate?}` 경로 템플릿을 정보 페이지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-164">The sample app uses `AddPageRouteModelConvention` to add an `{aboutTemplate?}` route template to the About page:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet4)]

> [!NOTE]
> <span data-ttu-id="c38f9-165">`AttributeRouteModel`에 대한 `Order` 속성을 `1`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-165">The `Order` property for the `AttributeRouteModel` is set to `1`.</span></span> <span data-ttu-id="c38f9-166">그러면 단일 경로 값을 제공하는 경우 `{globalTemplate?}`에 대한 템플릿(항목의 앞에서 설정함)이 첫 번째 경로 데이터 값 위치에 지정된 우선 순위가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-166">This ensures that the template for `{globalTemplate?}` (set earlier in the topic) is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="c38f9-167">`/About/RouteDataValue`에서 정보 페이지를 요청하는 경우 "RouteDataValue"는 `Order` 속성 설정으로 인해 `RouteData.Values["aboutTemplate"]`(`Order = 1`)이 아닌 `RouteData.Values["globalTemplate"]`(`Order = 0`)으로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-167">If the About page is requested at `/About/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 0`) and not `RouteData.Values["aboutTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="c38f9-168">`localhost:5000/About/GlobalRouteValue/AboutRouteValue`에서 샘플의 정보 페이지를 요청하고 결과를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-168">Request the sample's About page at `localhost:5000/About/GlobalRouteValue/AboutRouteValue` and inspect the result:</span></span>

![정보 페이지는 GlobalRouteValue 및 AboutRouteValue에 대한 경로 세그먼트를 사용하여 요청됩니다.](razor-pages-convention-features/_static/about-page-global-and-about-templates.png)

## <a name="configure-a-page-route"></a><span data-ttu-id="c38f9-171">페이지 경로 구성</span><span class="sxs-lookup"><span data-stu-id="c38f9-171">Configure a page route</span></span>

<span data-ttu-id="c38f9-172">[AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute)를 사용하여 지정된 페이지 경로에 페이지에 대한 경로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-172">Use [AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute) to configure a route to a page at the specified page path.</span></span> <span data-ttu-id="c38f9-173">페이지에 생성된 링크는 지정된 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-173">Generated links to the page use your specified route.</span></span> <span data-ttu-id="c38f9-174">`AddPageRoute`는 `AddPageRouteModelConvention`을 사용하여 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-174">`AddPageRoute` uses `AddPageRouteModelConvention` to establish the route.</span></span>

<span data-ttu-id="c38f9-175">샘플 앱은 *Contact.cshtml*의 `/TheContactPage`에 대한 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-175">The sample app creates a route to `/TheContactPage` for *Contact.cshtml*:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet5)]

<span data-ttu-id="c38f9-176">연락처 페이지도 기본 경로를 통해 `/Contact`에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-176">The Contact page can also be reached at `/Contact` via its default route.</span></span>

<span data-ttu-id="c38f9-177">연락처 페이지에 대한 샘플 앱의 사용자 지정 경로는 선택적 `text` 경로 세그먼트(`{text?}`)에 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-177">The sample app's custom route to the Contact page allows for an optional `text` route segment (`{text?}`).</span></span> <span data-ttu-id="c38f9-178">방문자가 해당 `/Contact` 경로에 있는 페이지에 액세스하는 경우 페이지에는 해당 `@page` 지시문에 있는 이 선택적 세그먼트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-178">The page also includes this optional segment in its `@page` directive in case the visitor accesses the page at its `/Contact` route:</span></span>

[!code-cshtml[Main](razor-pages-convention-features/sample/Pages/Contact.cshtml?highlight=1)]

<span data-ttu-id="c38f9-179">렌더링된 페이지의 **연락처** 링크에 생성된 URL이 업데이트된 경로를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-179">Note that the URL generated for the **Contact** link in the rendered page reflects the updated route:</span></span>

![탐색 모음의 샘플 앱 연락처 링크](razor-pages-convention-features/_static/contact-link.png)

![렌더링된 HTML에서 연락처 링크를 검사하면 href가 '/TheContactPage'로 설정되어 있음을 나타냅니다.](razor-pages-convention-features/_static/contact-link-source.png)

<span data-ttu-id="c38f9-182">일반적인 경로 `/Contact` 또는 사용자 지정 경로 `/TheContactPage`에서 연락처 페이지를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="c38f9-182">Visit the Contact page at either its ordinary route, `/Contact`, or the custom route, `/TheContactPage`.</span></span> <span data-ttu-id="c38f9-183">추가 `text` 경로 세그먼트를 제공하는 경우 페이지는 제공한 HTML 인코딩 세그먼트를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-183">If you supply an additional `text` route segment, the page shows the HTML-encoded segment that you provide:</span></span>

![URL에서 'TextValue'라는 선택적 'text' 경로 세그먼트를 제공하는 에지 브라우저 예제입니다.](razor-pages-convention-features/_static/route-segment-with-custom-route.png)

## <a name="page-model-action-conventions"></a><span data-ttu-id="c38f9-186">페이지 모델 작업 규칙</span><span class="sxs-lookup"><span data-stu-id="c38f9-186">Page model action conventions</span></span>

<span data-ttu-id="c38f9-187">[IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider)에서 파생되는 기본 페이지 모델 공급자는 페이지 모델을 구성하기 위한 확장성 지점을 제공하도록 설계된 규칙을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-187">The default page model provider that implements [IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider) invokes conventions which are designed to provide extensibility points for configuring page models.</span></span> <span data-ttu-id="c38f9-188">이러한 규칙은 페이지 검색 및 처리 기능을 빌드하고 수정하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-188">These conventions are useful when building and modifying page discovery and processing features.</span></span>

<span data-ttu-id="c38f9-189">샘플 앱은 이 섹션의 예제에서 응답 헤더를 적용하는 [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute)라는 `AddHeaderAttribute` 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-189">For the examples in this section, the sample app uses an `AddHeaderAttribute` class, which is a [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute), that applies a response header:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Filters/AddHeader.cs?name=snippet1)]

<span data-ttu-id="c38f9-190">샘플을 규칙을 사용하여 폴더에 있는 모든 페이지 및 단일 페이지에 특성을 적용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-190">Using conventions, the sample demonstrates how to apply the attribute to all of the pages in a folder and to a single page.</span></span>

<span data-ttu-id="c38f9-191">**폴더 앱 모델 규칙**</span><span class="sxs-lookup"><span data-stu-id="c38f9-191">**Folder app model convention**</span></span>

<span data-ttu-id="c38f9-192">[AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention)을 사용하여 지정된 폴더 아래에 있는 모든 페이지에 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) 인스턴스에 대한 작업을 호출하는 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention)을 만들고 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-192">Use [AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) that invokes an action on [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) instances for all pages under the specified folder.</span></span>

<span data-ttu-id="c38f9-193">이 샘플은 *OtherPages* 폴더 내의 페이지에 `OtherPagesHeader` 헤더를 추가하여 앱의 `AddFolderApplicationModelConvention`을 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-193">The sample demonstrates the use of `AddFolderApplicationModelConvention` by adding a header, `OtherPagesHeader`, to the pages inside the *OtherPages* folder of the app:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet6)]

<span data-ttu-id="c38f9-194">`localhost:5000/OtherPages/Page1`에서 샘플의 Page1 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-194">Request the sample's Page1 page at `localhost:5000/OtherPages/Page1` and inspect the headers to view the result:</span></span>

![OtherPages/Page1 페이지의 응답 헤더는 OtherPagesHeader가 추가되었음을 보여줍니다.](razor-pages-convention-features/_static/page1-otherpages-header.png)

<span data-ttu-id="c38f9-196">**페이지 앱 모델 규칙**</span><span class="sxs-lookup"><span data-stu-id="c38f9-196">**Page app model convention**</span></span>

<span data-ttu-id="c38f9-197">[AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention)을 사용하여 지정된 이름을 가진 페이지에 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel)에 대한 작업을 호출하는 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention)을 만들고 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-197">Use [AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) that invokes an action on the [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) for the page with the speciifed name.</span></span>

<span data-ttu-id="c38f9-198">샘플은 정보 페이지에 `AboutHeader` 헤더를 추가하여 `AddPageApplicationModelConvention`를 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-198">The sample demonstrates the use of `AddPageApplicationModelConvention` by adding a header, `AboutHeader`, to the About page:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet7)]

<span data-ttu-id="c38f9-199">`localhost:5000/About`에서 샘플의 정보 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-199">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![정보 페이지의 응답 헤더는 AboutHeader가 추가되었음을 보여줍니다.](razor-pages-convention-features/_static/about-page-about-header.png)

<span data-ttu-id="c38f9-201">**필터 구성**</span><span class="sxs-lookup"><span data-stu-id="c38f9-201">**Configure a filter**</span></span>

<span data-ttu-id="c38f9-202">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter)는 지정된 필터를 적용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-202">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter) configures the specified filter to apply.</span></span> <span data-ttu-id="c38f9-203">필터 클래스를 구현할 수 있지만 샘플 앱은 람다 식으로 필터를 구현하는 방법을 보여줍니다. 그러면 백그라운드에서 필터를 반환하는 팩터리로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-203">You can implement a filter class, but the sample app shows how to implement a filter in a lambda expression, which is implemented behind-the-scenes as a factory that returns a filter:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet8)]

<span data-ttu-id="c38f9-204">페이지 앱 모델은 *OtherPages* 폴더에 있는 Page2 페이지로 이동하는 세그먼트에 대한 상대 경로를 확인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-204">The page app model is used to check the relative path for segments that lead to the Page2 page in the *OtherPages* folder.</span></span> <span data-ttu-id="c38f9-205">조건이 통과하는 경우 헤더가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-205">If the condition passes, a header is added.</span></span> <span data-ttu-id="c38f9-206">그렇지 않으면 `EmptyFilter`이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-206">If not, the `EmptyFilter` is applied.</span></span>

<span data-ttu-id="c38f9-207">`EmptyFilter`은 [작업 필터](xref:mvc/controllers/filters#action-filters)입니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-207">`EmptyFilter` is an [Action filter](xref:mvc/controllers/filters#action-filters).</span></span> <span data-ttu-id="c38f9-208">Razor 페이지에서 작업 필터를 무시하므로 경로에 `OtherPages/Page2`가 포함되지 않는 경우 의도한 대로 `EmptyFilter`이 작동되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-208">Since Action filters are ignored by Razor Pages, the `EmptyFilter` no-ops as intended if the path doesn't contain `OtherPages/Page2`.</span></span>

<span data-ttu-id="c38f9-209">`localhost:5000/OtherPages/Page2`에서 샘플의 Page2 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-209">Request the sample's Page2 page at `localhost:5000/OtherPages/Page2` and inspect the headers to view the result:</span></span>

![OtherPagesPage2Header는 Page2에 대한 응답에 추가됩니다.](razor-pages-convention-features/_static/page2-filter-header.png)

<span data-ttu-id="c38f9-211">**필터 팩터리 구성**</span><span class="sxs-lookup"><span data-stu-id="c38f9-211">**Configure a filter factory**</span></span>

<span data-ttu-id="c38f9-212">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__)는 모든 Razor 페이지에 [필터](xref:mvc/controllers/filters)를 적용하도록 지정된 팩터리를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-212">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__) configures the specified factory to apply [filters](xref:mvc/controllers/filters) to all Razor Pages.</span></span>

<span data-ttu-id="c38f9-213">샘플 앱은 앱의 페이지에 두 개의 값이 포함된 `FilterFactoryHeader` 헤더를 추가하여 [필터 팩터리](xref:mvc/controllers/filters#ifilterfactory)를 사용하는 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-213">The sample app provides an example of using a [filter factory](xref:mvc/controllers/filters#ifilterfactory) by adding a header, `FilterFactoryHeader`, with two values to the app's pages:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet9)]

<span data-ttu-id="c38f9-214">*AddHeaderWithFactory.cs*:</span><span class="sxs-lookup"><span data-stu-id="c38f9-214">*AddHeaderWithFactory.cs*:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Factories/AddHeaderWithFactory.cs?name=snippet1)]

<span data-ttu-id="c38f9-215">`localhost:5000/About`에서 샘플의 정보 페이지를 요청하고 헤더를 검사하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-215">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![정보 페이지의 응답 헤더에서는 두 개의 FilterFactoryHeader 헤더가 추가되었음을 보여줍니다.](razor-pages-convention-features/_static/about-page-filter-factory-header.png)

## <a name="replace-the-default-page-app-model-provider"></a><span data-ttu-id="c38f9-217">기본 페이지 앱 모델 공급자 바꾸기</span><span class="sxs-lookup"><span data-stu-id="c38f9-217">Replace the default page app model provider</span></span>

<span data-ttu-id="c38f9-218">Razor 페이지는 `IPageApplicationModelProvider` 인터페이스를 사용하여 [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-218">Razor Pages uses the `IPageApplicationModelProvider` interface to create a [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider).</span></span> <span data-ttu-id="c38f9-219">처리기 검색 및 처리에 대해 고유한 구현 논리를 제공하기 위해 기본 모델 공급자에서 상속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-219">You can inherit from the default model provider to provide your own implementation logic for handler discovery and processing.</span></span> <span data-ttu-id="c38f9-220">기본 구현([참조 원본](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs))은 아래에서 설명할 *명명되지 않은* 및 *명명된* 처리기 명명에 대한 규칙을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-220">The default implementation ([reference source](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs)) establishes conventions for *unnamed* and *named* handler naming, which is described below.</span></span>

<span data-ttu-id="c38f9-221">**기본 명명되지 않은 처리기 메서드**</span><span class="sxs-lookup"><span data-stu-id="c38f9-221">**Default unnamed handler methods**</span></span>

<span data-ttu-id="c38f9-222">HTTP 동사에 대한 처리기 메서드("명명되지 않은" 처리기 메서드)는 다음 규칙을 따릅니다. `On<HTTP verb>[Async]`(`Async`를 추가하는 것은 선택적이지만 비동기 메서드에서 사용하는 것이 좋습니다.)</span><span class="sxs-lookup"><span data-stu-id="c38f9-222">Handler methods for HTTP verbs ("unnamed" handler methods) follow a convention: `On<HTTP verb>[Async]` (appending `Async` is optional but recommended for async methods).</span></span>

| <span data-ttu-id="c38f9-223">명명되지 않은 처리기 메서드</span><span class="sxs-lookup"><span data-stu-id="c38f9-223">Unnamed handler method</span></span>     | <span data-ttu-id="c38f9-224">작업</span><span class="sxs-lookup"><span data-stu-id="c38f9-224">Operation</span></span>                      |
| -------------------------- | ------------------------------ |
| `OnGet`/`OnGetAsync`       | <span data-ttu-id="c38f9-225">페이지 상태를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-225">Initialize the page state.</span></span>     |
| `OnPost`/`OnPostAsync`     | <span data-ttu-id="c38f9-226">POST 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-226">Handle POST requests.</span></span>          |
| `OnDelete`/`OnDeleteAsync` | <span data-ttu-id="c38f9-227">DELETE 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-227">Handle DELETE requests&#8224;.</span></span> |
| `OnPut`/`OnPutAsync`       | <span data-ttu-id="c38f9-228">PUT 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-228">Handle PUT requests&#8224;.</span></span>    |
| `OnPatch`/`OnPatchAsync`   | <span data-ttu-id="c38f9-229">PATCH 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-229">Handle PATCH requests&#8224;.</span></span>  |

<span data-ttu-id="c38f9-230">페이지에 대한 API를 호출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-230">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="c38f9-231">**기본 명명된 처리기 메서드**</span><span class="sxs-lookup"><span data-stu-id="c38f9-231">**Default named handler methods**</span></span>

<span data-ttu-id="c38f9-232">개발자가 제공하는 처리기 메서드("명명된" 처리기 메서드)는 비슷한 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-232">Handler methods provided by the developer ("named" handler methods) follow a similar convention.</span></span> <span data-ttu-id="c38f9-233">처리기 이름은 HTTP 동사 뒤에 또는 HTTP 동사와 `Async` 사이에 표시됩니다. `On<HTTP verb><handler name>[Async]`(`Async`을 추가하는 것은 선택적이지만 비동기 메서드에서 사용하는 것이 좋습니다.)</span><span class="sxs-lookup"><span data-stu-id="c38f9-233">The handler name appears after the HTTP verb or between the HTTP verb and `Async`: `On<HTTP verb><handler name>[Async]` (appending `Async` is optional but recommended for async methods).</span></span> <span data-ttu-id="c38f9-234">예를 들어 메시지를 처리하는 메서드는 아래 표에 표시된 명명된 메시지일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-234">For example, methods that process messages might take the naming shown in the table below.</span></span>

| <span data-ttu-id="c38f9-235">예제 명명된 처리기 메서드</span><span class="sxs-lookup"><span data-stu-id="c38f9-235">Example named handler method</span></span>             | <span data-ttu-id="c38f9-236">예제 작업</span><span class="sxs-lookup"><span data-stu-id="c38f9-236">Example operation</span></span>        |
| ---------------------------------------- | ------------------------ |
| `OnGetMessage`/`OnGetMessageAsync`       | <span data-ttu-id="c38f9-237">메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-237">Obtain a message.</span></span>        |
| `OnPostMessage`/`OnPostMessageAsync`     | <span data-ttu-id="c38f9-238">메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-238">POST a message.</span></span>          |
| `OnDeleteMessage`/`OnDeleteMessageAsync` | <span data-ttu-id="c38f9-239">메시지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-239">DELETE a message&#8224;.</span></span> |
| `OnPutMessage`/`OnPutMessageAsync`       | <span data-ttu-id="c38f9-240">메시지를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-240">PUT a message&#8224;.</span></span>    |
| `OnPatchMessage`/`OnPatchMessageAsync`   | <span data-ttu-id="c38f9-241">메시지를 패치합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-241">PATCH a message&#8224;.</span></span>  |

<span data-ttu-id="c38f9-242">페이지에 대한 API를 호출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-242">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="c38f9-243">**처리기 메서드 이름 사용자 지정**</span><span class="sxs-lookup"><span data-stu-id="c38f9-243">**Customize handler method names**</span></span>

<span data-ttu-id="c38f9-244">명명되지 않은 및 명명된 처리기 메서드의 이름을 지정하는 방식을 변경하려는 경우를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-244">Assume that you prefer to change the way unnamed and named handler methods are named.</span></span> <span data-ttu-id="c38f9-245">대체 이름 지정 체계는 메서드 이름을 "On"으로 시작되지 않도록 방지하고 첫 번째 단어 세그먼트를 사용하여 HTTP 동사를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-245">An alternative naming scheme is to avoid starting the method names with "On" and use the first word segment to determine the HTTP verb.</span></span> <span data-ttu-id="c38f9-246">다른 변경을 수행할 수 있습니다(예: DELETE, PUT 및 PATCH에 대한 동사를 POST로 변환).</span><span class="sxs-lookup"><span data-stu-id="c38f9-246">You can make other changes, such as converting the verbs for DELETE, PUT, and PATCH to POST.</span></span> <span data-ttu-id="c38f9-247">이러한 체계는 다음 표에 표시된 메서드 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-247">Such a scheme provides the method names shown in the following table.</span></span>

| <span data-ttu-id="c38f9-248">처리기 메서드</span><span class="sxs-lookup"><span data-stu-id="c38f9-248">Handler method</span></span>                       | <span data-ttu-id="c38f9-249">작업</span><span class="sxs-lookup"><span data-stu-id="c38f9-249">Operation</span></span>                      |
| ------------------------------------ | ------------------------------ |
| `Get`                                | <span data-ttu-id="c38f9-250">페이지 상태를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-250">Initialize the page state.</span></span>     |
| `Post`/`PostAsync`                   | <span data-ttu-id="c38f9-251">POST 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-251">Handle POST requests.</span></span>          |
| `Delete`/`DeleteAsync`               | <span data-ttu-id="c38f9-252">DELETE 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-252">Handle DELETE requests&#8224;.</span></span> |
| `Put`/`PutAsync`                     | <span data-ttu-id="c38f9-253">PUT 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-253">Handle PUT requests&#8224;.</span></span>    |
| `Patch`/`PatchAsync`                 | <span data-ttu-id="c38f9-254">PATCH 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-254">Handle PATCH requests&#8224;.</span></span>  |
| `GetMessage`                         | <span data-ttu-id="c38f9-255">메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-255">Obtain a message.</span></span>              |
| `PostMessage`/`PostMessageAsync`     | <span data-ttu-id="c38f9-256">메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-256">POST a message.</span></span>                |
| `DeleteMessage`/`DeleteMessageAsync` | <span data-ttu-id="c38f9-257">삭제할 메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-257">POST a message to delete.</span></span>      |
| `PutMessage`/`PutMessageAsync`       | <span data-ttu-id="c38f9-258">배치할 메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-258">POST a message to put.</span></span>         |
| `PatchMessage`/`PatchMessageAsync`   | <span data-ttu-id="c38f9-259">패치할 메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-259">POST a message to patch.</span></span>       |

<span data-ttu-id="c38f9-260">페이지에 대한 API를 호출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-260">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="c38f9-261">이 체계를 설정하려면 `DefaultPageApplicationModelProvider` 클래스에서 상속하고, [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) 메서드를 재정의하여 [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) 처리기 이름을 확인하는 사용자 지정 논리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-261">To establish this scheme, inherit from the `DefaultPageApplicationModelProvider` class and override the [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) method to supply custom logic for resolving [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) handler names.</span></span> <span data-ttu-id="c38f9-262">샘플 앱에서는 `CustomPageApplicationModelProvider` 클래스에서 이 작업을 수행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-262">The sample app shows you how this is done in its `CustomPageApplicationModelProvider` class:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/CustomPageApplicationModelProvider.cs?name=snippet1&highlight=1-2,45-46,64-68,78-85,87,92,106)]

<span data-ttu-id="c38f9-263">클래스의 장점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-263">Highlights of the class include:</span></span>

* <span data-ttu-id="c38f9-264">클래스는 `DefaultPageApplicationModelProvider`에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-264">The class inherits from `DefaultPageApplicationModelProvider`.</span></span>
* <span data-ttu-id="c38f9-265">`TryParseHandlerMethod`는 `PageHandlerModel`를 만들 때 HTTP 동사(`httpMethod`) 및 명명된 처리기 이름(`handlerName`)을 결정하는 처리기를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-265">The `TryParseHandlerMethod` processes a handler to determine the HTTP verb (`httpMethod`) and named handler name (`handlerName`) when creating the `PageHandlerModel`.</span></span>
  * <span data-ttu-id="c38f9-266">`Async` 후위가 있다면 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-266">An `Async` postfix is ignored, if present.</span></span>
  * <span data-ttu-id="c38f9-267">대/소문자 구분을 사용하여 메서드 이름에서 HTTP 동사를 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-267">Casing is used to parse the HTTP verb from the method name.</span></span>
  * <span data-ttu-id="c38f9-268">메서드 이름(`Async` 제외)이 HTTP 동사 이름과 같은 경우 명명된 처리기가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-268">When the method name (without `Async`) is equal to the HTTP verb name, there's no named handler.</span></span> <span data-ttu-id="c38f9-269">`handlerName`가 `null` 로 설정되고, 메서드 이름이 `Get`, `Post`, `Delete`, `Put` 또는 `Patch`입니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-269">The `handlerName` is set to `null`, and the method name is `Get`, `Post`, `Delete`, `Put`, or `Patch`.</span></span>
  * <span data-ttu-id="c38f9-270">메서드 이름(`Async` 제외)이 HTTP 동사 이름보다 긴 경우 명명된 처리기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-270">When the method name (without `Async`) is longer than the HTTP verb name, there's a named handler.</span></span> <span data-ttu-id="c38f9-271">`handlerName`는 `<method name (less 'Async', if present)>`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-271">The `handlerName` is set to `<method name (less 'Async', if present)>`.</span></span> <span data-ttu-id="c38f9-272">예를 들어 "GetMessage" 및 "GetMessageAsync"는 모두 "GetMessage"라는 처리기 이름을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-272">For example, both "GetMessage" and "GetMessageAsync" yield a handler name of "GetMessage".</span></span>
  * <span data-ttu-id="c38f9-273">DELETE, PUT 및 PATCH HTTP 동사는 POST로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-273">DELETE, PUT, and PATCH HTTP verbs are converted to POST.</span></span>

<span data-ttu-id="c38f9-274">`Startup` 클래스에 `CustomPageApplicationModelProvider`을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-274">Register the `CustomPageApplicationModelProvider` in the `Startup` class:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet10)]

<span data-ttu-id="c38f9-275">*Index.cshtml.cs*의 페이지 모델은 앱에서 페이지에 대한 일반 처리기 메서드 명명 규칙을 변경하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-275">The page model in *Index.cshtml.cs* shows how the ordinary handler method naming conventions are changed for pages in the app.</span></span> <span data-ttu-id="c38f9-276">Razor 페이지에서 사용되는 일반적인 "On" 접두사 이름 지정이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-276">The ordinary "On" prefix naming used with Razor Pages is removed.</span></span> <span data-ttu-id="c38f9-277">페이지 상태를 초기화하는 메서드의 이름은 이제 `Get`입니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-277">The method that initializes the page state is now named `Get`.</span></span> <span data-ttu-id="c38f9-278">페이지에 대한 페이지 모델을 여는 경우 앱 전체에서 사용하는 이 규칙을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-278">You can see this convention used throughout the app if you open any page model for any of the pages.</span></span>

<span data-ttu-id="c38f9-279">다른 메서드는 각각 해당 프로세스를 설명하는 HTTP 동사로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-279">Each of the other methods start with the HTTP verb that describes its processing.</span></span> <span data-ttu-id="c38f9-280">`Delete`로 시작하는 두 가지 메서드는 DELETE HTTP 동사로 정상적으로 처리되지만 `TryParseHandlerMethod`의 논리는 명시적으로 처리기 모두의 POST에 대해 동사로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-280">The two methods that start with `Delete` would normally be treated as DELETE HTTP verbs, but the logic in `TryParseHandlerMethod` explicitly sets the verb to POST for both handlers.</span></span>

<span data-ttu-id="c38f9-281">`Async`는 `DeleteAllMessages`와 `DeleteMessageAsync` 간에 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-281">Note that `Async` is optional between `DeleteAllMessages` and `DeleteMessageAsync`.</span></span> <span data-ttu-id="c38f9-282">모두 비동기 메서드이지만 `Async` 후위를 사용할지 선택할 수 있다면 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-282">They're both asynchronous methods, but you can choose to use the `Async` postfix or not; we recommend that you do.</span></span> <span data-ttu-id="c38f9-283">`DeleteAllMessages`는 설명을 위해 사용되지만 이러한 `DeleteAllMessagesAsync` 메서드의 이름을 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-283">`DeleteAllMessages` is used here for demonstration purposes, but we recommend that you name such a method `DeleteAllMessagesAsync`.</span></span> <span data-ttu-id="c38f9-284">샘플의 구현이라는 프로세스에 영향을 주지 않지만 `Async` 후위를 사용하면 비동기 메서드라는 점을 부각시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-284">It doesn't affect the processing of the sample's implementation, but using the `Async` postfix calls out the fact that it's an asynchronous method.</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Pages/Index.cshtml.cs?name=snippet1&highlight=1,6,16,29)]

<span data-ttu-id="c38f9-285">*Index.cshtml*에서 제공된 처리기 이름은 `DeleteAllMessages` 및 `DeleteMessageAsync` 처리기 메서드와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-285">Note the handler names provided in *Index.cshtml* match the `DeleteAllMessages` and `DeleteMessageAsync` handler methods:</span></span>

[!code-cshtml[Main](razor-pages-convention-features/sample/Pages/Index.cshtml?range=29-60&highlight=7-8,24-25)]

<span data-ttu-id="c38f9-286">처리기 메서드 이름 `DeleteMessageAsync`의 `Async`는 메서드에 대한 POST 요청과 일치하는 처리기에 대해 `TryParseHandlerMethod`을 기준으로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-286">`Async` in the handler method name `DeleteMessageAsync` is factored out by the `TryParseHandlerMethod` for handler matching of POST request to method.</span></span> <span data-ttu-id="c38f9-287">`DeleteMessage`라는 `asp-page-handler` 이름은 처리기 메서드 `DeleteMessageAsync`와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-287">The `asp-page-handler` name of `DeleteMessage` is matched to the handler method `DeleteMessageAsync`.</span></span>

## <a name="mvc-filters-and-the-page-filter-ipagefilter"></a><span data-ttu-id="c38f9-288">MVC 필터 및 페이지 필터(IPageFilter)</span><span class="sxs-lookup"><span data-stu-id="c38f9-288">MVC Filters and the Page filter (IPageFilter)</span></span>

<span data-ttu-id="c38f9-289">Razor 페이지가 처리기 메서드를 사용하므로 MVC [작업 필터](xref:mvc/controllers/filters#action-filters)는 Razor 페이지에서 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-289">MVC [Action filters](xref:mvc/controllers/filters#action-filters) are ignored by Razor Pages, since Razor Pages use handler methods.</span></span> <span data-ttu-id="c38f9-290">[권한 부여](xref:mvc/controllers/filters#authorization-filters), [예외](xref:mvc/controllers/filters#exception-filters), [리소스](xref:mvc/controllers/filters#resource-filters) 및 [결과](xref:mvc/controllers/filters#result-filters)에 다른 유형의 MVC 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-290">Other types of MVC filters are available for you to use: [Authorization](xref:mvc/controllers/filters#authorization-filters), [Exception](xref:mvc/controllers/filters#exception-filters), [Resource](xref:mvc/controllers/filters#resource-filters), and [Result](xref:mvc/controllers/filters#result-filters).</span></span> <span data-ttu-id="c38f9-291">자세한 내용은 [필터](xref:mvc/controllers/filters) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c38f9-291">For more information, see the [Filters](xref:mvc/controllers/filters) topic.</span></span>

<span data-ttu-id="c38f9-292">페이지 필터([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter))는 Razor 페이지에 적용되는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-292">The Page filter ([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)) is a filter that applies to Razor Pages.</span></span> <span data-ttu-id="c38f9-293">페이지 처리기 메서드를 실행할 때 둘러쌉니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-293">It surrounds the execution of a page handler method.</span></span> <span data-ttu-id="c38f9-294">그러면 페이지 처리기 메서드를 실행하는 단계에서 사용자 지정 코드를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-294">It allows you to process custom code at stages of page handler method execution.</span></span> <span data-ttu-id="c38f9-295">샘플 앱의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-295">Here's an example from the sample app:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Filters/ReplaceRouteValueFilterAttribute.cs?name=snippet1)]

<span data-ttu-id="c38f9-296">이 필터는 "TriggerValue"의 `globalTemplate` 경로 값을 확인하고 "ReplacementValue"를 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-296">This filter checks for a `globalTemplate` route value of "TriggerValue" and swaps in "ReplacementValue".</span></span>

<span data-ttu-id="c38f9-297">`ReplaceRouteValueFilter` 특성은 `PageModel`에 직접 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-297">The `ReplaceRouteValueFilter` attribute can be applied directly to a `PageModel`:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Pages/OtherPages/Page3.cshtml.cs?range=10-12&highlight=1)]

<span data-ttu-id="c38f9-298">`localhost:5000/OtherPages/Page3/TriggerValue`에 있는 샘플 앱에서 Page3 페이지를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-298">Request the Page3 page from the sample app with at `localhost:5000/OtherPages/Page3/TriggerValue`.</span></span> <span data-ttu-id="c38f9-299">필터가 경로 값을 대체하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c38f9-299">Notice how the filter replaces the route value:</span></span>

![TriggerValue 경로 세그먼트를 포함하는 OtherPages/Page3에 대한 요청은 경로 값을 ReplacementValue로 바꾸는 필터를 발생시킵니다.](razor-pages-convention-features/_static/otherpages-page3-filter-replacement-value.png)

## <a name="see-also"></a><span data-ttu-id="c38f9-301">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c38f9-301">See also</span></span>

* [<span data-ttu-id="c38f9-302">Razor 페이지 권한 부여 규칙</span><span class="sxs-lookup"><span data-stu-id="c38f9-302">Razor Pages authorization conventions</span></span>](xref:security/authorization/razor-pages-authorization)
