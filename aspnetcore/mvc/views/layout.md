---
title: ASP.NET Core의 레이아웃
author: ardalis
description: ASP.NET Core 앱에서 뷰를 렌더링하기 전에 일반적인 레이아웃을 사용하고, 지시문을 공유하고, 공용 코드를 실행하는 방법을 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/layout
ms.openlocfilehash: 8e89c8e6cf18c47abb6bf432cdc6bb6b97e8aeb0
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
ms.locfileid: "29904753"
---
# <a name="layout-in-aspnet-core"></a><span data-ttu-id="d7d97-103">ASP.NET Core의 레이아웃</span><span class="sxs-lookup"><span data-stu-id="d7d97-103">Layout in ASP.NET Core</span></span>

<span data-ttu-id="d7d97-104">작성자: [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="d7d97-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="d7d97-105">뷰는 시각적 개체 및 프로그래밍 요소를 자주 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-105">Views frequently share visual and programmatic elements.</span></span> <span data-ttu-id="d7d97-106">이 문서에서는 ASP.NET 앱에서 뷰를 렌더링하기 전에 일반적인 레이아웃을 사용하고, 지시문을 공유하며, 공용 코드를 실행하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-106">In this article, you'll learn how to use common layouts, share directives, and run common code before rendering views in your ASP.NET app.</span></span>

## <a name="what-is-a-layout"></a><span data-ttu-id="d7d97-107">레이아웃이란</span><span class="sxs-lookup"><span data-stu-id="d7d97-107">What is a Layout</span></span>

<span data-ttu-id="d7d97-108">대부분의 웹앱에는 사용자가 페이지를 탐색하는 동안 일관된 환경을 제공하는 일반적인 레이아웃이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-108">Most web apps have a common layout that provides the user with a consistent experience as they navigate from page to page.</span></span> <span data-ttu-id="d7d97-109">일반적으로 레이아웃에는 앱 헤더, 탐색 또는 메뉴 요소, 바닥글과 같은 공통 사용자 인터페이스 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-109">The layout typically includes common user interface elements such as the app header, navigation or menu elements, and footer.</span></span>

![페이지 레이아웃 예제](layout/_static/page-layout.png)

<span data-ttu-id="d7d97-111">스크립트 및 스타일시트와 같은 공통 HTML 구조는 앱 내에서 여러 페이지에서도 자주 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-111">Common HTML structures such as scripts and stylesheets are also frequently used by many pages within an app.</span></span> <span data-ttu-id="d7d97-112">이러한 모든 공유 요소를 *레이아웃* 파일에 정의한 후 앱 내에 사용된 모든 뷰에서 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-112">All of these shared elements may be defined in a *layout* file, which can then be referenced by any view used within the app.</span></span> <span data-ttu-id="d7d97-113">레이아웃은 뷰에서 중복 코드를 줄여 [DRY(반복 금지) 원칙](http://deviq.com/don-t-repeat-yourself/)을 따르도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-113">Layouts reduce duplicate code in views, helping them follow the [Don't Repeat Yourself (DRY) principle](http://deviq.com/don-t-repeat-yourself/).</span></span>

<span data-ttu-id="d7d97-114">규칙에 따라, ASP.NET 앱의 기본 레이아웃 이름을 `_Layout.cshtml`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-114">By convention, the default layout for an ASP.NET app is named `_Layout.cshtml`.</span></span> <span data-ttu-id="d7d97-115">Visual Studio ASP.NET Core MVC 프로젝트 템플릿은 `Views/Shared` 폴더에 이 레이아웃 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-115">The Visual Studio ASP.NET Core MVC project template includes this layout file in the `Views/Shared` folder:</span></span>

![솔루션 탐색기의 뷰 폴더](layout/_static/web-project-views.png)

<span data-ttu-id="d7d97-117">이 레이아웃은 앱의 뷰에 대한 최상위 수준 템플릿을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-117">This layout defines a top level template for views in the app.</span></span> <span data-ttu-id="d7d97-118">앱에는 레이아웃이 필요하지 않으며, 앱은 다른 레이아웃을 지정하는 서로 다른 뷰를 포함하는 둘 이상의 레이아웃을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-118">Apps don't require a layout, and apps can define more than one layout, with different views specifying different layouts.</span></span>

<span data-ttu-id="d7d97-119">`_Layout.cshtml` 예:</span><span class="sxs-lookup"><span data-stu-id="d7d97-119">An example `_Layout.cshtml`:</span></span>

[!code-html[](../../common/samples/WebApplication1/Views/Shared/_Layout.cshtml?highlight=42,66)]

## <a name="specifying-a-layout"></a><span data-ttu-id="d7d97-120">레이아웃 지정</span><span class="sxs-lookup"><span data-stu-id="d7d97-120">Specifying a Layout</span></span>

<span data-ttu-id="d7d97-121">Razor 뷰는 `Layout` 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-121">Razor views have a `Layout` property.</span></span> <span data-ttu-id="d7d97-122">이 속성을 설정하여 레이아웃을 지정하는 개별 뷰:</span><span class="sxs-lookup"><span data-stu-id="d7d97-122">Individual views specify a layout by setting this property:</span></span>

[!code-html[](../../common/samples/WebApplication1/Views/_ViewStart.cshtml?highlight=2)]

<span data-ttu-id="d7d97-123">지정한 레이아웃은 전체 경로(예: `/Views/Shared/_Layout.cshtml`) 또는 부분 이름(예: `_Layout`)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-123">The layout specified can use a full path (example: `/Views/Shared/_Layout.cshtml`) or a partial name (example: `_Layout`).</span></span> <span data-ttu-id="d7d97-124">부분 이름이 제공되면 Razor 뷰 엔진이 표준 검색 프로세스를 사용하여 레이아웃 파일을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-124">When a partial name is provided, the Razor view engine will search for the layout file using its standard discovery process.</span></span> <span data-ttu-id="d7d97-125">컨트롤러 관련 폴더를 먼저 검색한 후 `Shared` 폴더를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-125">The controller-associated folder is searched first, followed by the `Shared` folder.</span></span> <span data-ttu-id="d7d97-126">이 검색 프로세스는 [부분 뷰](partial.md)를 검색하는 데 사용된 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-126">This discovery process is identical to the one used to discover [partial views](partial.md).</span></span>

<span data-ttu-id="d7d97-127">기본적으로 모든 레이아웃에서 `RenderBody`를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-127">By default, every layout must call `RenderBody`.</span></span> <span data-ttu-id="d7d97-128">`RenderBody` 호출이 배치될 때마다 뷰의 내용이 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-128">Wherever the call to `RenderBody` is placed, the contents of the view will be rendered.</span></span>

<a name="layout-sections-label"></a>

### <a name="sections"></a><span data-ttu-id="d7d97-129">섹션</span><span class="sxs-lookup"><span data-stu-id="d7d97-129">Sections</span></span>

<span data-ttu-id="d7d97-130">레이아웃은 `RenderSection`을 호출하여 필요에 따라 하나 이상의 *섹션*을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-130">A layout can optionally reference one or more *sections*, by calling `RenderSection`.</span></span> <span data-ttu-id="d7d97-131">섹션에서는 특정 페이지 요소를 배치할 위치를 구성하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-131">Sections provide a way to organize where certain page elements should be placed.</span></span> <span data-ttu-id="d7d97-132">`RenderSection` 호출 때마다 섹션이 필수 또는 옵션인지 여부를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-132">Each call to `RenderSection` can specify whether that section is required or optional.</span></span> <span data-ttu-id="d7d97-133">필수 섹션이 없는 경우 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-133">If a required section isn't found, an exception will be thrown.</span></span> <span data-ttu-id="d7d97-134">개별 뷰는 `@section` Razor 구문을 사용하여 섹션 내에 렌더링될 콘텐츠를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-134">Individual views specify the content to be rendered within a section using the `@section` Razor syntax.</span></span> <span data-ttu-id="d7d97-135">뷰에서 섹션을 정의하는 경우 렌더링되어야 합니다(그렇지 않은 경우 오류 발생).</span><span class="sxs-lookup"><span data-stu-id="d7d97-135">If a view defines a section, it must be rendered (or an error will occur).</span></span>

<span data-ttu-id="d7d97-136">뷰에서 `@section` 정의 예:</span><span class="sxs-lookup"><span data-stu-id="d7d97-136">An example `@section` definition in a view:</span></span>

```html
@section Scripts {
     <script type="text/javascript" src="/scripts/main.js"></script>
   }
   ```

<span data-ttu-id="d7d97-137">위의 코드에서는 유효성 검사 스크립트가 양식을 포함하는 뷰의 `scripts` 섹션에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-137">In the code above, validation scripts are added to the `scripts` section on a view that includes a form.</span></span> <span data-ttu-id="d7d97-138">동일한 응용 프로그램의 다른 뷰에는 추가 스크립트가 필요하지 않을 수 있으므로 스크립트 섹션을 정의할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-138">Other views in the same application might not require any additional scripts, and so wouldn't need to define a scripts section.</span></span>

<span data-ttu-id="d7d97-139">뷰에 정의된 섹션은 즉시 레이아웃 페이지에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-139">Sections defined in a view are available only in its immediate layout page.</span></span> <span data-ttu-id="d7d97-140">이들은 부분 뷰, 뷰 구성 요소 또는 뷰 시스템의 다른 부분에서 참조할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-140">They cannot be referenced from partials, view components, or other parts of the view system.</span></span>

### <a name="ignoring-sections"></a><span data-ttu-id="d7d97-141">섹션 무시</span><span class="sxs-lookup"><span data-stu-id="d7d97-141">Ignoring sections</span></span>

<span data-ttu-id="d7d97-142">기본적으로 콘텐츠 페이지 본문 및 모든 섹션은 레이아웃 페이지에서 모두 렌더링되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-142">By default, the body and all sections in a content page must all be rendered by the layout page.</span></span> <span data-ttu-id="d7d97-143">Razor 뷰 엔진은 본문과 각 섹션이 렌더링되었는지 여부를 추적하여 이를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-143">The Razor view engine enforces this by tracking whether the body and each section have been rendered.</span></span>

<span data-ttu-id="d7d97-144">뷰 엔진이 본문 또는 섹션을 무시하도록 지시하려면 `IgnoreBody` 및 `IgnoreSection` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-144">To instruct the view engine to ignore the body or sections, call the `IgnoreBody` and `IgnoreSection` methods.</span></span>

<span data-ttu-id="d7d97-145">Razor 페이지의 본문 및 모든 섹션은 렌더링되거나 무시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-145">The body and every section in a Razor page must be either rendered or ignored.</span></span>

<a name="viewimports"></a>

## <a name="importing-shared-directives"></a><span data-ttu-id="d7d97-146">공유 지시문 가져오기</span><span class="sxs-lookup"><span data-stu-id="d7d97-146">Importing Shared Directives</span></span>

<span data-ttu-id="d7d97-147">뷰는 Razor 지시문을 사용하여 네임스페이스 가져오기 또는 [종속성 주입](dependency-injection.md) 수행과 같은 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-147">Views can use Razor directives to do many things, such as importing namespaces or performing [dependency injection](dependency-injection.md).</span></span> <span data-ttu-id="d7d97-148">많은 뷰에서 공유된 지시문은 공용 `_ViewImports.cshtml` 파일에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-148">Directives shared by many views may be specified in a common `_ViewImports.cshtml` file.</span></span> <span data-ttu-id="d7d97-149">`_ViewImports` 파일은 다음 지시문을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-149">The `_ViewImports` file supports the following directives:</span></span>

* `@addTagHelper`

* `@removeTagHelper`

* `@tagHelperPrefix`

* `@using`

* `@model`

* `@inherits`

* `@inject`

<span data-ttu-id="d7d97-150">이 파일은 다른 Razor 기능(예: 함수 및 섹션 정의)을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-150">The file doesn't support other Razor features, such as functions and section definitions.</span></span>

<span data-ttu-id="d7d97-151">샘플 `_ViewImports.cshtml` 파일:</span><span class="sxs-lookup"><span data-stu-id="d7d97-151">A sample `_ViewImports.cshtml` file:</span></span>

[!code-html[](../../common/samples/WebApplication1/Views/_ViewImports.cshtml)]

<span data-ttu-id="d7d97-152">ASP.NET Core MVC 앱에 대한 `_ViewImports.cshtml` 파일은 일반적으로 `Views` 폴더에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-152">The `_ViewImports.cshtml` file for an ASP.NET Core MVC app is typically placed in the `Views` folder.</span></span> <span data-ttu-id="d7d97-153">`_ViewImports.cshtml` 파일은 모든 폴더 내에 배치할 수 있으며, 이 경우 해당 폴더 및 해당 하위 폴더 내의 뷰에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-153">A `_ViewImports.cshtml` file can be placed within any folder, in which case it will only be applied to views within that folder and its subfolders.</span></span> <span data-ttu-id="d7d97-154">`_ViewImports` 파일은 루트 수준에서부터 처리된 다음, 각 폴더에 대해 뷰 자체의 위치까지 처리되므로 루트 수준에서 지정된 설정이 폴더 수준에서 재정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-154">`_ViewImports` files are processed starting at the root level, and then for each folder leading up to the location of the view itself, so settings specified at the root level may be overridden at the folder level.</span></span>

<span data-ttu-id="d7d97-155">예를 들어 루트 수준 `_ViewImports.cshtml` 파일이 `@model` 및 `@addTagHelper`를 지정하고, 뷰의 컨트롤러 관련 폴더에서 다른 `_ViewImports.cshtml` 파일이 다른 `@model`을 지정하며 다른 `@addTagHelper`를 추가하면, 뷰는 두 태그 도우미에 액세스할 수 있고 후자 `@model`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-155">For example, if a root level `_ViewImports.cshtml` file specifies `@model` and `@addTagHelper`, and another `_ViewImports.cshtml` file in the controller-associated folder of the view specifies a different `@model` and adds another `@addTagHelper`, the view will have access to both tag helpers and will use the latter `@model`.</span></span>

<span data-ttu-id="d7d97-156">뷰에 대해 여러 `_ViewImports.cshtml` 파일이 실행되는 경우 `ViewImports.cshtml` 파일에 포함된 지시문의 결합된 동작은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-156">If multiple `_ViewImports.cshtml` files are run for a view, combined behavior of the directives included in the `ViewImports.cshtml` files will be as follows:</span></span>

* <span data-ttu-id="d7d97-157">`@addTagHelper`, `@removeTagHelper`: 순서대로 모두 실행</span><span class="sxs-lookup"><span data-stu-id="d7d97-157">`@addTagHelper`, `@removeTagHelper`: all run, in order</span></span>

* <span data-ttu-id="d7d97-158">`@tagHelperPrefix`: 뷰에 가장 가까운 것이 다른 것보다 우선함</span><span class="sxs-lookup"><span data-stu-id="d7d97-158">`@tagHelperPrefix`: the closest one to the view overrides any others</span></span>

* <span data-ttu-id="d7d97-159">`@model`: 뷰에 가장 가까운 것이 다른 것보다 우선함</span><span class="sxs-lookup"><span data-stu-id="d7d97-159">`@model`: the closest one to the view overrides any others</span></span>

* <span data-ttu-id="d7d97-160">`@inherits`: 뷰에 가장 가까운 것이 다른 것보다 우선함</span><span class="sxs-lookup"><span data-stu-id="d7d97-160">`@inherits`: the closest one to the view overrides any others</span></span>

* <span data-ttu-id="d7d97-161">`@using`: 모두 포함됨. 중복 항목은 무시됨</span><span class="sxs-lookup"><span data-stu-id="d7d97-161">`@using`: all are included; duplicates are ignored</span></span>

* <span data-ttu-id="d7d97-162">`@inject`: 각 속성에 대해 뷰에 가장 가까운 것이 같은 속성 이름의 다른 것보다 우선함</span><span class="sxs-lookup"><span data-stu-id="d7d97-162">`@inject`: for each property, the closest one to the view overrides any others with the same property name</span></span>

<a name="viewstart"></a>

## <a name="running-code-before-each-view"></a><span data-ttu-id="d7d97-163">각 뷰 이전에 코드 실행</span><span class="sxs-lookup"><span data-stu-id="d7d97-163">Running Code Before Each View</span></span>

<span data-ttu-id="d7d97-164">모든 뷰 이전에 실행해야 하는 코드가 있는 경우 `_ViewStart.cshtml` 파일에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-164">If you have code you need to run before every view, this should be placed in the `_ViewStart.cshtml` file.</span></span> <span data-ttu-id="d7d97-165">규칙에 따라 `_ViewStart.cshtml` 파일은 `Views` 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-165">By convention, the `_ViewStart.cshtml` file is located in the `Views` folder.</span></span> <span data-ttu-id="d7d97-166">`_ViewStart.cshtml`에 나열된 문은 모든 전체 뷰(레이아웃 및 부분 뷰가 아님) 이전에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-166">The statements listed in `_ViewStart.cshtml` are run before every full view (not layouts, and not partial views).</span></span> <span data-ttu-id="d7d97-167">[ViewImports.cshtml](xref:mvc/views/layout#viewimports)처럼 `_ViewStart.cshtml`은 계층적입니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-167">Like [ViewImports.cshtml](xref:mvc/views/layout#viewimports), `_ViewStart.cshtml` is hierarchical.</span></span> <span data-ttu-id="d7d97-168">`_ViewStart.cshtml` 파일이 컨트롤러 관련 뷰 폴더에 정의된 경우 `Views` 폴더의 루트에 정의된 항목 뒤에 실행됩니다(있는 경우).</span><span class="sxs-lookup"><span data-stu-id="d7d97-168">If a `_ViewStart.cshtml` file is defined in the controller-associated view folder, it will be run after the one defined in the root of the `Views` folder (if any).</span></span>

<span data-ttu-id="d7d97-169">샘플 `_ViewStart.cshtml` 파일:</span><span class="sxs-lookup"><span data-stu-id="d7d97-169">A sample `_ViewStart.cshtml` file:</span></span>

[!code-html[](../../common/samples/WebApplication1/Views/_ViewStart.cshtml)]

<span data-ttu-id="d7d97-170">위의 파일은 모든 뷰가 `_Layout.cshtml` 레이아웃을 사용하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-170">The file above specifies that all views will use the `_Layout.cshtml` layout.</span></span>

> [!NOTE]
> <span data-ttu-id="d7d97-171">일반적으로 `_ViewStart.cshtml` 또는 `_ViewImports.cshtml`은 `/Views/Shared` 폴더에 배치되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-171">Neither `_ViewStart.cshtml` nor `_ViewImports.cshtml` are typically placed in the `/Views/Shared` folder.</span></span> <span data-ttu-id="d7d97-172">이러한 파일의 앱 수준 버전은 `/Views` 폴더에 직접 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d97-172">The app-level versions of these files should be placed directly in the `/Views` folder.</span></span>
