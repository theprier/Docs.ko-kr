---
title: ASP.NET Core의 부분 태그 도우미
author: scottaddie
description: ASP.NET Core 부분 태그 도우미와 부분 보기를 렌더링할 때 각 특성이 수행하는 역할을 알아봅니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: scaddie
ms.custom: mvc
ms.date: 04/13/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/partial-tag-helper
ms.openlocfilehash: 786c333980db89a9a5a60dc70c0bd1998ca159cd
ms.sourcegitcommit: 74be78285ea88772e7dad112f80146b6ed00e53e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="partial-tag-helper-in-aspnet-core"></a><span data-ttu-id="85296-103">ASP.NET Core의 부분 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="85296-103">Partial Tag Helper in ASP.NET Core</span></span>

<span data-ttu-id="85296-104">작성자: [Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="85296-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="85296-105">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/tag-helpers/built-in/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="85296-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/tag-helpers/built-in/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="overview"></a><span data-ttu-id="85296-106">개요</span><span class="sxs-lookup"><span data-stu-id="85296-106">Overview</span></span>

<span data-ttu-id="85296-107">부분 태그 도우미는 Razor 페이지 및 MVC 앱에서 [부분 보기](xref:mvc/views/partial)를 렌더링하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="85296-107">The Partial Tag Helper is used for rendering a [partial view](xref:mvc/views/partial) in Razor Pages and MVC apps.</span></span> <span data-ttu-id="85296-108">고려 사항:</span><span class="sxs-lookup"><span data-stu-id="85296-108">Consider that it:</span></span>

* <span data-ttu-id="85296-109">ASP.NET Core 2.1 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="85296-109">Requires ASP.NET Core 2.1 or later.</span></span>
* <span data-ttu-id="85296-110">[HTML 도우미 구문](xref:mvc/views/partial#referencing-a-partial-view) 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85296-110">Is an alternative to [HTML Helper syntax](xref:mvc/views/partial#referencing-a-partial-view).</span></span>
* <span data-ttu-id="85296-111">부분 보기를 비동기적으로 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="85296-111">Renders the partial view asynchronously.</span></span>

<span data-ttu-id="85296-112">부분 보기 렌더링을 위한 HTML 도우미 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85296-112">The HTML Helper options for rendering a partial view include:</span></span>

* [<span data-ttu-id="85296-113">@await Html.PartialAsync</span><span class="sxs-lookup"><span data-stu-id="85296-113">@await Html.PartialAsync</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partialasync)
* [<span data-ttu-id="85296-114">@await Html.RenderPartialAsync</span><span class="sxs-lookup"><span data-stu-id="85296-114">@await Html.RenderPartialAsync</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartialasync)
* [@Html.Partial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partial)
* [@Html.RenderPartial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartial)

<span data-ttu-id="85296-115">*제품* 모델은 이 문서 전반의 샘플에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="85296-115">The *Product* model is used in samples throughout this document:</span></span>

[!code-csharp[](samples/TagHelpersBuiltIn/Models/Product.cs)]

<span data-ttu-id="85296-116">부분 태그 도우미 특성의 인벤토리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85296-116">An inventory of the Partial Tag Helper attributes follows.</span></span>

## <a name="name"></a><span data-ttu-id="85296-117">name</span><span class="sxs-lookup"><span data-stu-id="85296-117">name</span></span>

<span data-ttu-id="85296-118">`name` 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="85296-118">The `name` attribute is required.</span></span> <span data-ttu-id="85296-119">렌더링할 부분 보기의 이름 또는 경로를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85296-119">It indicates the name or the path of the partial view to be rendered.</span></span> <span data-ttu-id="85296-120">부분 보기 이름이 제공되는 경우 [보기 검색](xref:mvc/views/overview#view-discovery) 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="85296-120">When a partial view name is provided, the [view discovery](xref:mvc/views/overview#view-discovery) process is initiated.</span></span> <span data-ttu-id="85296-121">해당 프로세스는 명시적 경로가 제공될 때 우회됩니다.</span><span class="sxs-lookup"><span data-stu-id="85296-121">That process is bypassed when an explicit path is provided.</span></span>

<span data-ttu-id="85296-122">다음 표시에서는 명시적 경로를 사용하여 *_ProductPartial.cshtml*이 *공유* 폴더에서 로드됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85296-122">The following markup uses an explicit path, indicating that *_ProductPartial.cshtml* is to be loaded from the *Shared* folder.</span></span> <span data-ttu-id="85296-123">[for](#for) 특성을 사용하면 모델이 바인딩을 위해 부분 보기에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="85296-123">Using the [for](#for) attribute, a model is passed to the partial view for binding.</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_Name)]

## <a name="for"></a><span data-ttu-id="85296-124">for</span><span class="sxs-lookup"><span data-stu-id="85296-124">for</span></span>

<span data-ttu-id="85296-125">`for` 특성은 현재 모델과 비교 평가할 [ModelExpression](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.modelexpression)을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="85296-125">The `for` attribute assigns a [ModelExpression](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.modelexpression) to be evaluated against the current model.</span></span> <span data-ttu-id="85296-126">`ModelExpression`은 `@Model.` 구문을 유추합니다.</span><span class="sxs-lookup"><span data-stu-id="85296-126">A `ModelExpression` infers the `@Model.` syntax.</span></span> <span data-ttu-id="85296-127">예를 들어 `for="@Model.Product"` 대신 `for="Product"`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85296-127">For example, `for="Product"` can be used instead of `for="@Model.Product"`.</span></span> <span data-ttu-id="85296-128">이 기본 유추 동작은 인라인 식을 정의하는 `@` 기호를 사용하여 재정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="85296-128">This default inference behavior is overridden by using the `@` symbol to define an inline expression.</span></span> <span data-ttu-id="85296-129">`for` 특성은 [모델](#model) 특성과 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85296-129">The `for` attribute can't be used with the [model](#model) attribute.</span></span>

<span data-ttu-id="85296-130">다음 표시는 *_ProductPartial.cshtml*을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="85296-130">The following markup loads *_ProductPartial.cshtml*:</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_For)]

<span data-ttu-id="85296-131">부분 보기는 연결된 페이지 모델의 `Product` 속성에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="85296-131">The partial view is bound to the associated page model's `Product` property:</span></span>

[!code-csharp[](samples/TagHelpersBuiltIn/Pages/Product.cshtml.cs?highlight=8)]

## <a name="model"></a><span data-ttu-id="85296-132">모델</span><span class="sxs-lookup"><span data-stu-id="85296-132">model</span></span>

<span data-ttu-id="85296-133">`model` 특성은 부분 보기에 전달할 모델 인스턴스를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="85296-133">The `model` attribute assigns a model instance to pass to the partial view.</span></span> <span data-ttu-id="85296-134">`model` 특성은 [for](#for) 특성과 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85296-134">The `model` attribute can't be used with the [for](#for) attribute.</span></span>

<span data-ttu-id="85296-135">다음 표시에서는 새 `Product` 개체가 인스턴스화되고 바인딩을 위해 `model` 특성에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="85296-135">In the following markup, a new `Product` object is instantiated and passed to the `model` attribute for binding:</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_Model)]

## <a name="view-data"></a><span data-ttu-id="85296-136">view-data</span><span class="sxs-lookup"><span data-stu-id="85296-136">view-data</span></span>

<span data-ttu-id="85296-137">`view-data` 특성은 부분 보기에 전달할 [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary)를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="85296-137">The `view-data` attribute assigns a [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) to pass to the partial view.</span></span> <span data-ttu-id="85296-138">다음 표시를 사용하면 부분 보기에서 전체 ViewData 컬렉션에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85296-138">The following markup makes the entire ViewData collection accessible to the partial view:</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_ViewData&highlight=5-)]

<span data-ttu-id="85296-139">위의 코드에서 `IsNumberReadOnly` 키 값은 `true`로 설정되고 ViewData 컬렉션에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="85296-139">In the preceding code, the `IsNumberReadOnly` key value is set to `true` and added to the ViewData collection.</span></span> <span data-ttu-id="85296-140">따라서 `ViewData["IsNumberReadOnly"]`는 다음 부분 보기 내에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85296-140">Consequently, `ViewData["IsNumberReadOnly"]` is made accessible within the following partial view:</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Shared/_ProductViewDataPartial.cshtml?highlight=5)]

<span data-ttu-id="85296-141">이 예제에서 `ViewData["IsNumberReadOnly"]` 값은 *번호* 필드가 읽기 전용으로 표시되는지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85296-141">In this example, the value of `ViewData["IsNumberReadOnly"]` determines whether the *Number* field is displayed as read only.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="85296-142">추가 자료</span><span class="sxs-lookup"><span data-stu-id="85296-142">Additional resources</span></span>

* [<span data-ttu-id="85296-143">부분 뷰</span><span class="sxs-lookup"><span data-stu-id="85296-143">Partial views</span></span>](xref:mvc/views/partial)
* [<span data-ttu-id="85296-144">약한 형식의 데이터(ViewData, ViewData 특성 및 ViewBag)</span><span class="sxs-lookup"><span data-stu-id="85296-144">Weakly typed data (ViewData, ViewData attribute, and ViewBag)</span></span>](xref:mvc/views/overview#weakly-typed-data-viewdata-viewdata-attribute-and-viewbag)
