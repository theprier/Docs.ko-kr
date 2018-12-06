---
title: 웹 API 규칙 사용
author: pranavkm
description: ASP.NET Core에서 웹 API 규칙에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.2'
ms.author: pranavkm
ms.custom: mvc
ms.date: 11/13/2018
uid: web-api/advanced/conventions
ms.openlocfilehash: ede9a46c160cf6a49aa93da710af0bf0b8f59acc
ms.sourcegitcommit: c4572be5ebb301013a5698caf9b5572b76cb2e34
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52710077"
---
# <a name="use-web-api-conventions"></a><span data-ttu-id="de4b0-103">웹 API 규칙 사용</span><span class="sxs-lookup"><span data-stu-id="de4b0-103">Use web API conventions</span></span>

<span data-ttu-id="de4b0-104">ASP.NET Core 2.2에는 일반적인 [API 설명서](xref:tutorials/web-api-help-pages-using-swagger)를 추출하여 여러 작업, 컨트롤러 또는 어셈블리 내 모든 컨트롤러에 적용하는 방법이 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-104">ASP.NET Core 2.2 introduces a way to extract common [API documentation](xref:tutorials/web-api-help-pages-using-swagger) and apply it to multiple actions, controllers, or all controllers within an assembly.</span></span> <span data-ttu-id="de4b0-105">웹 API 규칙은 개별 작업을 [[ProducesResponseType]](xref:Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute)으로 데코레이팅하는 대체자입니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-105">Web API conventions are a substitute for decorating individual actions with [[ProducesResponseType]](xref:Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute).</span></span> <span data-ttu-id="de4b0-106">이 옵션을 사용하면 작업에 적용되는 규칙 메서드를 선택하는 방법으로 작업에서 반환되는 가장 일반적인 "기존" 반환 형식 및 상태 코드를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-106">It allows you to define the most common "conventional" return types and status codes that you return from your action with a way to select the convention method that applies to an action.</span></span>

<span data-ttu-id="de4b0-107">기본적으로 ASP.NET Core MVC 2.2는 기본 규칙 조합인 `Microsoft.AspNetCore.Mvc.DefaultApiConventions`와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-107">By default, ASP.NET Core MVC 2.2 ships with a set of default conventions, `Microsoft.AspNetCore.Mvc.DefaultApiConventions`.</span></span> <span data-ttu-id="de4b0-108">규칙은 ASP.NET Core 스캐폴드 컨트롤러를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-108">The conventions are based on the controller that ASP.NET Core scaffolds.</span></span> <span data-ttu-id="de4b0-109">작업이 스캐폴딩 생성의 패턴을 따르는 경우, 기본 규칙을 성공적으로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-109">If your actions follow the pattern that scaffolding produces, you should be successful using the default conventions.</span></span>

<span data-ttu-id="de4b0-110">런타임 시 <xref:Microsoft.AspNetCore.Mvc.ApiExplorer>가 규칙을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-110">At runtime, <xref:Microsoft.AspNetCore.Mvc.ApiExplorer> understands conventions.</span></span> <span data-ttu-id="de4b0-111">`ApiExplorer`는 Open API 문서 생성기와 통신하기 위한 MVC의 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-111">`ApiExplorer` is MVC's abstraction to communicate with Open API document generators.</span></span> <span data-ttu-id="de4b0-112">적용된 규칙의 특성은 작업과 연결되며 작업의 Swagger 설명서에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-112">Attributes from the applied convention get associated with an action and are included in the action's Swagger documentation.</span></span> <span data-ttu-id="de4b0-113">API 분석기도 규칙을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-113">API analyzers also understand conventions.</span></span> <span data-ttu-id="de4b0-114">작업이 색다른 경우(예를 들어 적용된 규칙에 의해 문서화되지 않은 상태 코드를 반환하는 경우) 경고가 생성되어 문서화하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-114">If your action is unconventional (for example, it returns a status code that isn't documented by the applied convention), it produces a warning, encouraging you to document it.</span></span>

<span data-ttu-id="de4b0-115">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/conventions/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="de4b0-115">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/conventions/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="apply-web-api-conventions"></a><span data-ttu-id="de4b0-116">웹 API 규칙 적용</span><span class="sxs-lookup"><span data-stu-id="de4b0-116">Apply web API conventions</span></span>

<span data-ttu-id="de4b0-117">규칙을 적용하는 세 가지가 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-117">There are three ways to apply a convention.</span></span> <span data-ttu-id="de4b0-118">규칙이 구성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-118">Conventions don't compose.</span></span> <span data-ttu-id="de4b0-119">각 작업이 정확히 하나의 규칙과 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-119">Each action may be associated with exactly one convention.</span></span> <span data-ttu-id="de4b0-120">보다 구체적인 규칙(아래에 자세히 설명됨)은 덜 구체적인 규칙보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-120">More specific conventions (detailed below) take precedence over less specific ones.</span></span> <span data-ttu-id="de4b0-121">동일한 우선순위의 둘 이상의 규칙이 작업에 적용되는 경우 선택은 명확하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-121">The selection is non-deterministic when two or more conventions of the same priority apply to an action.</span></span> <span data-ttu-id="de4b0-122">다음 옵션은 가장 구체적인 것에서 가장 덜 구체적인 것까지 작업에 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-122">The following options exist to apply a convention to an action, from the most specific to the least specific:</span></span>

1. <span data-ttu-id="de4b0-123">`Microsoft.AspNetCore.Mvc.ApiConventionMethodAttribute` &mdash; 개별 작업에 적용되며 규칙 형식 및 적용되는 규칙 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-123">`Microsoft.AspNetCore.Mvc.ApiConventionMethodAttribute` &mdash; Applies to individual actions and specifies the convention type and the convention method that applies.</span></span> <span data-ttu-id="de4b0-124">다음 샘플에서는 `Update` 작업에 규칙 메서드 `Microsoft.AspNetCore.Mvc.DefaultApiConventions.Put`이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-124">In the following sample, the convention method `Microsoft.AspNetCore.Mvc.DefaultApiConventions.Put` is applied to the `Update` action:</span></span>

    [!code-csharp[](conventions/sample/Controllers/ContactsConventionController.cs?name=apiconventionmethod&highlight=2-3)]

1. <span data-ttu-id="de4b0-125">&mdash; 컨트롤러에 `Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute`를 적용하면 컨트롤러에서 모든 작업에 규칙 유형을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-125">`Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute` applied to a controller &mdash; Applies the convention type to all actions on the controller.</span></span> <span data-ttu-id="de4b0-126">규칙 메서드는 적용하는 작업(작성 규칙의 일부로써의 세부 사항)를 결정하는 힌트로 데코레이팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-126">Convention methods are decorated with hints that determine which actions it would apply to (details as part of authoring conventions).</span></span> <span data-ttu-id="de4b0-127">예:</span><span class="sxs-lookup"><span data-stu-id="de4b0-127">For example:</span></span>

    [!code-csharp[](conventions/sample/Controllers/ContactsConventionController.cs?name=apiconventiontypeattribute)]

1. <span data-ttu-id="de4b0-128">&mdash; 어셈블리에 적용된 `Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute`는 현재 어셈블리의 모든 컨트롤러에 규칙 유형을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-128">`Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute` applied to an assembly &mdash; Applies the convention type to all controllers in the current assembly.</span></span> <span data-ttu-id="de4b0-129">예:</span><span class="sxs-lookup"><span data-stu-id="de4b0-129">For example:</span></span>

    [!code-csharp[](conventions/sample/Startup.cs?name=apiconventiontypeattribute)]

## <a name="create-web-api-conventions"></a><span data-ttu-id="de4b0-130">웹 API 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="de4b0-130">Create web API conventions</span></span>

<span data-ttu-id="de4b0-131">규칙은 메서드가 있는 정적 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-131">A convention is a static type with methods.</span></span> <span data-ttu-id="de4b0-132">이러한 메서드에는 `[ProducesResponseType]` 또는 `[ProducesDefaultResponseType]` 특성으로 주석이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-132">These methods are annotated with `[ProducesResponseType]` or `[ProducesDefaultResponseType]` attributes.</span></span>

```csharp
public static class MyAppConventions
{
    [ProducesResponseType(200)]
    [ProducesResponseType(404)]
    public static void Find(int id)
    {
    }
}
```

<span data-ttu-id="de4b0-133">이 규칙을 어셈블리에 적용하면 다른 특정 메타데이터 특성이 없는 한 이름이 `Find`이고 `id`로 명명된 정확히 하나의 매개 변수가 있는 모든 작업에 적용되는 규칙 메서드가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-133">Applying this convention to an assembly results in the convention method applying to any action with the name `Find` and having exactly one parameter named `id`, as long as they don't have other more specific metadata attributes.</span></span>

<span data-ttu-id="de4b0-134">`[ProducesResponseType]` 및 `[ProducesDefaultResponseType]` 외에도 `[ApiConventionNameMatch]` 및 `[ApiConventionTypeMatch]`를 적용할 메서드를 결정하는 규칙 메서드에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-134">In addition to `[ProducesResponseType]` and `[ProducesDefaultResponseType]`, `[ApiConventionNameMatch]` and `[ApiConventionTypeMatch]` can be applied to the convention method that determines the methods they apply to.</span></span> <span data-ttu-id="de4b0-135">예:</span><span class="sxs-lookup"><span data-stu-id="de4b0-135">For example:</span></span>

```csharp
[ProducesResponseType(200)]
[ProducesResponseType(404)]
[ApiConventionNameMatch(ApiConventionNameMatchBehavior.Prefix)]
public static void Find(
    [ApiConventionNameMatch(ApiConventionNameMatchBehavior.Suffix)]
    int id)
{ }
```

* <span data-ttu-id="de4b0-136">메서드에 적용된 `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Prefix` 옵션은 "찾기"로 접두사가 지정된 모든 작업과 일치할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-136">The `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Prefix` option applied to the method, indicates that the convention can match any action as long as it's prefixed with "Find".</span></span> <span data-ttu-id="de4b0-137">여기에는 `Find`, `FindPet` 또는 `FindById`와 같은 메서드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-137">This includes methods such as `Find`, `FindPet`, or `FindById`.</span></span>
* <span data-ttu-id="de4b0-138">매개 변수에 적용된 `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Suffix`는 규칙이 접미사 식별자로 끝나는 정확히 하나의 매개 변수와 메서드를 일치시킬 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-138">The `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Suffix` applied to the parameter indicates that the convention can match methods with exactly one parameter ending in the suffix identifier.</span></span> <span data-ttu-id="de4b0-139">여기에는 `id` 또는 `petId`와 같은 매개 변수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-139">This includes parameters such as `id` or `petId`.</span></span> <span data-ttu-id="de4b0-140">`ApiConventionTypeMatch`는 매개 변수 유형을 제한하는 형식에도 유사하게 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-140">`ApiConventionTypeMatch` can be similarly applied to types to constrain the type of the parameter.</span></span> <span data-ttu-id="de4b0-141">`params[]` 인수를 사용하여 명시적으로 일치할 필요가 없는 나머지 매개 변수를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de4b0-141">A `params[]` argument can be used to indicate remaining parameters that don't need to be explicitly matched.</span></span>
