---
title: ASP.NET Core의 스캐폴드된 Razor 페이지
author: rick-anderson
description: 스캐폴딩을 통해 생성된 Razor 페이지를 설명합니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 12/4/2018
uid: tutorials/razor-pages/page
ms.openlocfilehash: acfc446732803c67714943fe3e5b7a31055ebcd7
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2018
ms.locfileid: "52862007"
---
# <a name="scaffolded-razor-pages-in-aspnet-core"></a><span data-ttu-id="9f03e-103">ASP.NET Core의 스캐폴드된 Razor 페이지</span><span class="sxs-lookup"><span data-stu-id="9f03e-103">Scaffolded Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="9f03e-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9f03e-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="9f03e-105">이 자습서에서는 이전 자습서에서 스캐폴딩을 통해 만든 Razor 페이지를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-105">This tutorial examines the Razor Pages created by scaffolding in the previous tutorial.</span></span>

<span data-ttu-id="9f03e-106">샘플을 [보거나 다운로드합니다](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22).</span><span class="sxs-lookup"><span data-stu-id="9f03e-106">[View or download](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22) sample.</span></span>

## <a name="the-create-delete-details-and-edit-pages"></a><span data-ttu-id="9f03e-107">만들기, 삭제, 세부 정보 및 편집 페이지</span><span class="sxs-lookup"><span data-stu-id="9f03e-107">The Create, Delete, Details, and Edit pages</span></span>

<span data-ttu-id="9f03e-108">*Pages/Movies/Index.cshtml.cs* 페이지 모델을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-108">Examine the *Pages/Movies/Index.cshtml.cs* Page Model:</span></span>

[!code-csharp[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs)]

<span data-ttu-id="9f03e-109">Razor 페이지는 `PageModel`에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-109">Razor Pages are derived from `PageModel`.</span></span> <span data-ttu-id="9f03e-110">일반적으로 `PageModel` 파생 클래스를 `<PageName>Model`이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-110">By convention, the `PageModel`-derived class is called `<PageName>Model`.</span></span> <span data-ttu-id="9f03e-111">생성자는 [종속성 주입](xref:fundamentals/dependency-injection)을 사용하여 `RazorPagesMovieContext`를 페이지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-111">The constructor uses [dependency injection](xref:fundamentals/dependency-injection) to add the `RazorPagesMovieContext` to the page.</span></span> <span data-ttu-id="9f03e-112">모든 스캐폴드된 페이지가 이 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-112">All the scaffolded pages follow this pattern.</span></span> <span data-ttu-id="9f03e-113">엔터티 프레임워크로 비동기 프로그래밍에 대한 자세한 내용은 [비동기 코드](xref:data/ef-rp/intro#asynchronous-code)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f03e-113">See [Asynchronous code](xref:data/ef-rp/intro#asynchronous-code) for more information on asynchronous programing with Entity Framework.</span></span>

<span data-ttu-id="9f03e-114">페이지에 대한 요청을 만들면 `OnGetAsync` 메서드가 Razor 페이지에 동영상 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-114">When a request is made for the page, the `OnGetAsync` method returns a list of movies to the Razor Page.</span></span> <span data-ttu-id="9f03e-115">페이지 상태를 초기화하기 위해 `OnGetAsync` 또는 `OnGet`이 Razor 페이지에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-115">`OnGetAsync` or `OnGet` is called on a Razor Page to initialize the state for the page.</span></span> <span data-ttu-id="9f03e-116">이 경우 `OnGetAsync`는 동영상 목록을 가져와 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-116">In this case, `OnGetAsync` gets a list of movies and displays them.</span></span>

<span data-ttu-id="9f03e-117">`OnGet`에서 `void`를 반환하거나 `OnGetAsync`에서 `Task`를 반환하면 반환 메서드가 사용되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-117">When `OnGet` returns `void` or `OnGetAsync` returns`Task`, no return method is used.</span></span> <span data-ttu-id="9f03e-118">반환 형식이 `IActionResult` 또는 `Task<IActionResult>`이면 반환 문을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-118">When the return type is `IActionResult` or `Task<IActionResult>`, a return statement must be provided.</span></span> <span data-ttu-id="9f03e-119">*Pages/Movies/Create.cshtml.cs* `OnPostAsync` 메서드를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-119">For example, the *Pages/Movies/Create.cshtml.cs* `OnPostAsync` method:</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Create.cshtml.cs?name=snippet)]

<a name="index"></a> <span data-ttu-id="9f03e-120">*Pages/Movies/Index.cshtml* Razor 페이지를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-120">Examine the *Pages/Movies/Index.cshtml* Razor Page:</span></span>

[!code-cshtml[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml)]

<span data-ttu-id="9f03e-121">Razor는 HTML에서 C# 또는 Razor 관련 태그로 전환될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-121">Razor can transition from HTML into C# or into Razor-specific markup.</span></span> <span data-ttu-id="9f03e-122">`@` 기호 뒤에 [Razor 예약 키워드](xref:mvc/views/razor#razor-reserved-keywords)가 사용되면 이 기호는 Razor 관련 태그로 전환됩니다. 이외의 경우에는 C#으로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-122">When an `@` symbol is followed by a [Razor reserved keyword](xref:mvc/views/razor#razor-reserved-keywords), it transitions into Razor-specific markup, otherwise it transitions into C#.</span></span>

<span data-ttu-id="9f03e-123">`@page` Razor 지시문은 파일을 MVC 작업으로 만들고, 이것은 요청을 처리할 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-123">The `@page` Razor directive makes the file into an MVC action, which means that it can handle requests.</span></span> <span data-ttu-id="9f03e-124">`@page`는 페이지의 첫 번째 Razor 지시문이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-124">`@page` must be the first Razor directive on a page.</span></span> <span data-ttu-id="9f03e-125">`@page`는 Razor 관련 태그로 전환되는 하나의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-125">`@page` is an example of transitioning into Razor-specific markup.</span></span> <span data-ttu-id="9f03e-126">자세한 내용은 [Razor 구문](xref:mvc/views/razor#razor-syntax)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f03e-126">See [Razor syntax](xref:mvc/views/razor#razor-syntax) for more information.</span></span>

<span data-ttu-id="9f03e-127">다음 HTML 도우미에서 사용되는 람다 식을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-127">Examine the lambda expression used in the following HTML Helper:</span></span>

```cshtml
@Html.DisplayNameFor(model => model.Movie[0].Title))
```

<span data-ttu-id="9f03e-128">`DisplayNameFor` HTML 도우미는 람다 식에서 참조되는 `Title` 속성을 검사하여 표시 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-128">The `DisplayNameFor` HTML Helper inspects the `Title` property referenced in the lambda expression to determine the display name.</span></span> <span data-ttu-id="9f03e-129">람다 식은 계산되는 것이 아니라 검사됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-129">The lambda expression is inspected rather than evaluated.</span></span> <span data-ttu-id="9f03e-130">즉, `model`, `model.Movie` 또는 `model.Movie[0]`가 `null`이거나 비어 있을 경우 액세스 위반이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-130">That means there is no access violation when `model`, `model.Movie`, or `model.Movie[0]` are `null` or empty.</span></span> <span data-ttu-id="9f03e-131">람다 식이 계산될 경우(예: `@Html.DisplayFor(modelItem => item.Title)` 사용) 모델의 속성 값이 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-131">When the lambda expression is evaluated (for example, with `@Html.DisplayFor(modelItem => item.Title)`), the model's property values are evaluated.</span></span>

<a name="md"></a>
### <a name="the-model-directive"></a><span data-ttu-id="9f03e-132">@model 지시문</span><span class="sxs-lookup"><span data-stu-id="9f03e-132">The @model directive</span></span>

[!code-cshtml[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml?range=1-2&highlight=2)]

<span data-ttu-id="9f03e-133">`@model` 지시문은 Razor 페이지에 전달되는 모델 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-133">The `@model` directive specifies the type of the model passed to the Razor Page.</span></span> <span data-ttu-id="9f03e-134">이전 예제에서 `@model` 줄은 Razor 페이지에서 `PageModel` 파생 클래스를 사용할 수 있게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-134">In the preceding example, the `@model` line makes the `PageModel`-derived class available to the Razor Page.</span></span> <span data-ttu-id="9f03e-135">모델은 페이지에서 `@Html.DisplayNameFor` 및 `@Html.DisplayFor` [HTML 도우미](/aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs#understanding-html-helpers)에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-135">The model is used in the `@Html.DisplayNameFor` and `@Html.DisplayFor` [HTML Helpers](/aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs#understanding-html-helpers) on the page.</span></span>

<a name="vd"></a>
### <a name="viewdata-and-layout"></a><span data-ttu-id="9f03e-136">ViewData 및 레이아웃</span><span class="sxs-lookup"><span data-stu-id="9f03e-136">ViewData and layout</span></span>

<span data-ttu-id="9f03e-137">*Pages/Movies/Index.cshtml* 파일의 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-137">Consider the following code from the *Pages/Movies/Index.cshtml* file:</span></span>

[!code-cshtml[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml?range=1-6&highlight=4-999)]

<span data-ttu-id="9f03e-138">이전 강조 표시된 코드는 C#으로 전환되는 Razor의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-138">The preceding highlighted code is an example of Razor transitioning into C#.</span></span> <span data-ttu-id="9f03e-139">`{` 및 `}` 문자로 C# 코드 블록을 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-139">The `{` and `}` characters enclose a block of C# code.</span></span>

<span data-ttu-id="9f03e-140">`PageModel` 기본 클래스에는 뷰에 전달할 데이터를 추가하는 데 사용될 수 있는 `ViewData` 사전 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-140">The `PageModel` base class has a `ViewData` dictionary property that can be used to add data that you want to pass to a View.</span></span> <span data-ttu-id="9f03e-141">키/쌍 패턴을 사용하여 개체를 `ViewData` 사전에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-141">You add objects into the `ViewData` dictionary using a key/value pattern.</span></span> <span data-ttu-id="9f03e-142">이전 샘플에서는 “Title” 속성이 `ViewData` 사전에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-142">In the preceding sample, the "Title" property is added to the `ViewData` dictionary.</span></span> 

<span data-ttu-id="9f03e-143">"Title" 속성은 *Pages/Shared/_Layout.cshtml* 파일에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-143">The "Title" property is used in the *Pages/Shared/_Layout.cshtml* file.</span></span> <span data-ttu-id="9f03e-144">다음 태그는 *_Layout.cshtml* 파일의 처음 몇 줄을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-144">The following markup shows the first few lines of the *_Layout.cshtml* file.</span></span>

<!-- we need a snapshot copy of layout because we are
changing in in the next step. 
-->
[!code-cshtml[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/NU/_Layout.cshtml?highlight=6-99)]

<span data-ttu-id="9f03e-145">`@*Markup removed for brevity.*@` 줄은 레이아웃 파일에 나타나지 않는 Razor 주석입니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-145">The line `@*Markup removed for brevity.*@` is a Razor comment which doesn't appear in your layout file.</span></span> <span data-ttu-id="9f03e-146">HTML 주석(`<!-- -->`)과 달리 Razor 주석은 클라이언트에 전송되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-146">Unlike HTML comments (`<!-- -->`), Razor comments are not sent to the client.</span></span>

### <a name="update-the-layout"></a><span data-ttu-id="9f03e-147">레이아웃 업데이트</span><span class="sxs-lookup"><span data-stu-id="9f03e-147">Update the layout</span></span>

<span data-ttu-id="9f03e-148">*Pages/Shared/_Layout.cshtml* 파일에서 `<title>` 요소를 변경합니다. **RazorPagesMovie**가 아닌 **Movie**를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-148">Change the `<title>` element in the *Pages/Shared/_Layout.cshtml* file display **Movie** rather than **RazorPagesMovie**.</span></span>

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie22/Pages/Shared/_Layout.cshtml?range=1-6&highlight=6)]


<span data-ttu-id="9f03e-149">*Pages/Shared/_Layout.cshtml* 파일에서 다음 앵커 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-149">Find the following anchor element in the *Pages/Shared/_Layout.cshtml* file.</span></span>

```cshtml
<a class="navbar-brand" asp-area="" asp-page="/Index">RazorPagesMovie</a>
```

<span data-ttu-id="9f03e-150">이전 요소를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-150">Replace the preceding element with the following markup.</span></span>

```cshtml
<a class="navbar-brand" asp-page="/Movies/Index">RpMovie</a>
```

<span data-ttu-id="9f03e-151">이전 앵커 요소는 [태그 도우미](xref:mvc/views/tag-helpers/intro)입니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-151">The preceding anchor element is a [Tag Helper](xref:mvc/views/tag-helpers/intro).</span></span> <span data-ttu-id="9f03e-152">이 경우에는 [앵커 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)입니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-152">In this case, it's the [Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper).</span></span> <span data-ttu-id="9f03e-153">`asp-page="/Movies/Index"` 태그 도우미 특성 및 값으로 `/Movies/Index` Razor 페이지의 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-153">The `asp-page="/Movies/Index"` Tag Helper attribute and value creates a link to the `/Movies/Index` Razor Page.</span></span> <span data-ttu-id="9f03e-154">`asp-area` 특성 값이 비어 있으므로 영역은 링크에서 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-154">The `asp-area` attribute value is empty, so the area isn't used in the link.</span></span> <span data-ttu-id="9f03e-155">자세한 내용은 [영역](xref:mvc/controllers/areas)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f03e-155">See [Areas](xref:mvc/controllers/areas) for more information.</span></span>

<span data-ttu-id="9f03e-156">변경 내용을 저장하고 **RpMovie** 링크를 클릭하여 앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-156">Save your changes, and test the app by clicking on the **RpMovie** link.</span></span> <span data-ttu-id="9f03e-157">문제가 있는 경우 GitHub에서 [_Layout.cshtml](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Pages/Shared/_Layout.cshtml) 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f03e-157">See the [_Layout.cshtml](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Pages/Shared/_Layout.cshtml) file in GitHub if you have any problems.</span></span>

<span data-ttu-id="9f03e-158">다른 링크(**홈**, **RpMovie**, **만들기**, **편집** 및 **삭제**)를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-158">Test the other links (**Home**, **RpMovie**, **Create**, **Edit**, and **Delete**).</span></span> <span data-ttu-id="9f03e-159">각 페이지에서 설정되는 제목은 브라우저 탭에서 확인할 수 있습니다. 페이지의 책갈피를 지정하면 제목이 책갈피에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-159">Each page sets the title, which you can see in the browser tab. When you bookmark a page, the title is used for the bookmark.</span></span> <span data-ttu-id="9f03e-160">*Pages/Index.cshtml* 및 *Pages/Movies/Index.cshtml*의 제목은 현재 동일하지만 다른 값으로 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-160">*Pages/Index.cshtml* and *Pages/Movies/Index.cshtml* currently have the same title, but you can modify them to have different values.</span></span>

> [!NOTE]
> <span data-ttu-id="9f03e-161">`Price` 필드에는 소수점을 입력하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-161">You may not be able to enter decimal commas in the `Price` field.</span></span> <span data-ttu-id="9f03e-162">소수점으로 쉼표(“,”)를 사용하는 영어가 아닌 로캘 및 미국 영어가 아닌 날짜 형식에 대해 [jQuery 유효성 검사](https://jqueryvalidation.org/)를 지원하려면 앱을 전역화하는 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-162">To support [jQuery validation](https://jqueryvalidation.org/) for non-English locales that use a comma (",") for a decimal point, and non US-English date formats, you must take steps to globalize your app.</span></span> <span data-ttu-id="9f03e-163">소수점 추가에 대한 지침은 이 [GitHub 문제 4076](https://github.com/aspnet/Docs/issues/4076#issuecomment-326590420)에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-163">This [GitHub issue 4076](https://github.com/aspnet/Docs/issues/4076#issuecomment-326590420) for instructions on adding decimal comma.</span></span>

<span data-ttu-id="9f03e-164">`Layout` 속성은 *Pages/_ViewStart.cshtml* 파일에서 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-164">The `Layout` property is set in the *Pages/_ViewStart.cshtml* file:</span></span>

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie22/Pages/_ViewStart.cshtml)]

<span data-ttu-id="9f03e-165">이전 태그는 *Pages* 폴더 아래에 있는 모든 Razor 파일에 대한 레이아웃 파일을 *Pages/Shared/_Layout.cshtml*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-165">The preceding markup sets the layout file to *Pages/Shared/_Layout.cshtml* for all Razor files under the *Pages* folder.</span></span> <span data-ttu-id="9f03e-166">자세한 내용은 [레이아웃](xref:razor-pages/index#layout)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f03e-166">See [Layout](xref:razor-pages/index#layout) for more information.</span></span>

### <a name="the-create-page-model"></a><span data-ttu-id="9f03e-167">Create 페이지 모델</span><span class="sxs-lookup"><span data-stu-id="9f03e-167">The Create page model</span></span>

<span data-ttu-id="9f03e-168">*Pages/Movies/Create.cshtml.cs* 페이지 모델을 살펴봅니다. </span><span class="sxs-lookup"><span data-stu-id="9f03e-168">Examine the *Pages/Movies/Create.cshtml.cs* page model:</span></span>

[!code-csharp[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml.cs?name=snippetALL)]

<span data-ttu-id="9f03e-169">`OnGet` 메서드는 페이지에 필요한 상태를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-169">The `OnGet` method initializes any state needed for the page.</span></span> <span data-ttu-id="9f03e-170">만들기 페이지에는 초기화할 상태가 없습니다. 따라서 `Page`가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-170">The Create page doesn't have any state to initialize, so `Page` is returned.</span></span> <span data-ttu-id="9f03e-171">이 자습서의 뒷부분에서 `OnGet` 메서드 초기화 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-171">Later in the tutorial you see `OnGet` method initialize state.</span></span> <span data-ttu-id="9f03e-172">`Page` 메서드는 *Create.cshtml* 페이지를 렌더링하는 `PageResult` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-172">The `Page` method creates a `PageResult` object that renders the *Create.cshtml* page.</span></span>

<span data-ttu-id="9f03e-173">`Movie` 속성은 `[BindProperty]` 특성을 사용하여 [모델 바인딩](xref:mvc/models/model-binding)을 옵트인(opt in)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-173">The `Movie` property uses the `[BindProperty]` attribute to opt-in to [model binding](xref:mvc/models/model-binding).</span></span> <span data-ttu-id="9f03e-174">만들기 폼이 폼 값을 게시하면 ASP.NET Core 런타임이 게시된 값을 `Movie` 모델에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-174">When the Create form posts the form values, the ASP.NET Core runtime binds the posted values to the `Movie` model.</span></span>

<span data-ttu-id="9f03e-175">페이지에 폼 데이터가 게시되면 `OnPostAsync` 메서드가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-175">The `OnPostAsync` method is run when the page posts form data:</span></span>

[!code-csharp[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml.cs?name=snippetPost)]

<span data-ttu-id="9f03e-176">모델 오류가 있는 경우 폼과 게시된 모든 폼 데이터가 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-176">If there are any model errors, the form is redisplayed, along with any form data posted.</span></span> <span data-ttu-id="9f03e-177">대부분의 모델 오류는 폼이 게시되기 전에 클라이언트 쪽에서 catch할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-177">Most model errors can be caught on the client-side before the form is posted.</span></span> <span data-ttu-id="9f03e-178">예를 들어 데이터로 변환될 수 없는 날짜 필드에 대한 값을 게시하는 모델 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-178">An example of a model error is posting a value for the date field that cannot be converted to a date.</span></span> <span data-ttu-id="9f03e-179">클라이언트 쪽 유효성 검사 및 모델 유효성 검사는 자습서의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-179">Client-side validation and model validation are discussed later in the tutorial.</span></span>

<span data-ttu-id="9f03e-180">모델 오류가 없는 경우 데이터가 저장되고 브라우저가 인덱스 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-180">If there are no model errors, the data is saved, and the browser is redirected to the Index page.</span></span>

### <a name="the-create-razor-page"></a><span data-ttu-id="9f03e-181">만들기 Razor 페이지</span><span class="sxs-lookup"><span data-stu-id="9f03e-181">The Create Razor Page</span></span>

<span data-ttu-id="9f03e-182">*Pages/Movies/Create.cshtml* Razor 페이지 파일을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-182">Examine the *Pages/Movies/Create.cshtml* Razor Page file:</span></span>

[!code-cshtml[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml)]

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="9f03e-183">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9f03e-183">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="9f03e-184">Visual Studio에서는 `<form method="post">` 태그를 태그 도우미에 사용되는 독특한 굵은 글꼴로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-184">Visual Studio displays the `<form method="post">` tag in a distinctive bold font used for Tag Helpers:</span></span>

<span data-ttu-id="9f03e-185">![Create.cshtml 페이지의 VS17 보기](page/_static/th.png)
<!-- Code --------------------------></span><span class="sxs-lookup"><span data-stu-id="9f03e-185">![VS17 view of Create.cshtml page](page/_static/th.png)
<!-- Code --------------------------></span></span>
# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="9f03e-186">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9f03e-186">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="9f03e-187">태그 도우미(예: `<form method="post">`)에 대한 자세한 내용은 [ASP.NET Core의 태그 도우미](xref:mvc/views/tag-helpers/intro)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f03e-187">For more information on Tag Helpers such as `<form method="post">`, see [Tag Helpers in ASP.NET Core](xref:mvc/views/tag-helpers/intro).</span></span>

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="9f03e-188">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="9f03e-188">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="9f03e-189">Mac용 Visual Studio에서는 `<form method="post">` 태그를 태그 도우미에 사용되는 독특한 굵은 글꼴로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-189">Visual Studio for Mac displays the `<form method="post">` tag in a distinctive bold font used for Tag Helpers.</span></span>

---  
<!-- End of VS tabs -->

<span data-ttu-id="9f03e-190">`<form method="post">` 요소는 [폼 태그 도우미](xref:mvc/views/working-with-forms#the-form-tag-helper)입니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-190">The `<form method="post">` element is a [Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper).</span></span> <span data-ttu-id="9f03e-191">폼 태그 도우미에는 [위조 방지 토큰](xref:security/anti-request-forgery)이 자동으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-191">The Form Tag Helper automatically includes an [antiforgery token](xref:security/anti-request-forgery).</span></span>

<span data-ttu-id="9f03e-192">스캐폴딩 엔진은 다음과 비슷한 모델에서 각 필드(ID 제외)에 대한 Razor 태그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-192">The scaffolding engine creates Razor markup for each field in the model (except the ID) similar to the following:</span></span>

[!code-cshtml[](~/tutorials/razor-pages/razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml?range=15-20)]

<span data-ttu-id="9f03e-193">[유효성 검사 태그 도우미](xref:mvc/views/working-with-forms#the-validation-tag-helpers) (`<div asp-validation-summary` 및 ` <span asp-validation-for`) 는 유효성 검사 오류를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-193">The [Validation Tag Helpers](xref:mvc/views/working-with-forms#the-validation-tag-helpers) (`<div asp-validation-summary` and ` <span asp-validation-for`) display validation errors.</span></span> <span data-ttu-id="9f03e-194">유효성 검사는 이 시리즈의 뒷부분에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-194">Validation is covered in more detail later in this series.</span></span>

<span data-ttu-id="9f03e-195">[레이블 태그 도우미](xref:mvc/views/working-with-forms#the-label-tag-helper)(`<label asp-for="Movie.Title" class="control-label"></label>`)는 `Title` 속성에 대한 레이블 캡션 및 `for` 특성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-195">The [Label Tag Helper](xref:mvc/views/working-with-forms#the-label-tag-helper) (`<label asp-for="Movie.Title" class="control-label"></label>`) generates the label caption and `for` attribute for the `Title` property.</span></span>

<span data-ttu-id="9f03e-196">[입력 태그 도우미](xref:mvc/views/working-with-forms)(`<input asp-for="Movie.Title" class="form-control" />`)는 [DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) 특성을 사용하고 클라이언트 쪽의 jQuery 유효성 검사에 필요한 HTML 특성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9f03e-196">The [Input Tag Helper](xref:mvc/views/working-with-forms) (`<input asp-for="Movie.Title" class="form-control" />`) uses the [DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) attributes and produces HTML attributes needed for jQuery Validation on the client-side.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9f03e-197">[이전: 모델 추가](xref:tutorials/razor-pages/model)
> [다음: 데이터 베이스](xref:tutorials/razor-pages/sql)</span><span class="sxs-lookup"><span data-stu-id="9f03e-197">[Previous: Adding a model](xref:tutorials/razor-pages/model)
[Next: Data Base](xref:tutorials/razor-pages/sql)</span></span>
