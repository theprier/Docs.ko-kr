---
title: 라우팅 razor 구성 요소
author: guardrex
description: 앱에 NavLink 구성 요소에 대 한 요청을 라우팅하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 04/07/2019
uid: razor-components/routing
ms.openlocfilehash: ef82fa7e0d571979a43fd8ce712bf4f22c06f9a7
ms.sourcegitcommit: 948e533e02c2a7cb6175ada20b2c9cabb7786d0b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2019
ms.locfileid: "59515678"
---
# <a name="razor-components-routing"></a><span data-ttu-id="4668c-103">라우팅 razor 구성 요소</span><span class="sxs-lookup"><span data-stu-id="4668c-103">Razor Components routing</span></span>

<span data-ttu-id="4668c-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="4668c-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="4668c-105">앱에 NavLink 구성 요소에 대 한 요청을 라우팅하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-105">Learn how to route requests in apps and about the NavLink component.</span></span>

## <a name="aspnet-core-endpoint-routing-integration"></a><span data-ttu-id="4668c-106">ASP.NET Core 끝점 라우팅 통합</span><span class="sxs-lookup"><span data-stu-id="4668c-106">ASP.NET Core endpoint routing integration</span></span>

<span data-ttu-id="4668c-107">Razor 구성 요소에 통합 되어 [ASP.NET Core 라우팅](xref:fundamentals/routing)합니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-107">Razor Components are integrated into [ASP.NET Core routing](xref:fundamentals/routing).</span></span> <span data-ttu-id="4668c-108">ASP.NET Core 앱을 사용 하 여 대화형 Razor 구성 요소에 대 한 들어오는 연결을 허용 하도록 구성 된 `MapComponentHub<TComponent>` 에서 `Startup.Configure`합니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-108">An ASP.NET Core app is configured to accept incoming connections for interactive Razor Components with `MapComponentHub<TComponent>` in `Startup.Configure`.</span></span> `MapComponentHub` <span data-ttu-id="4668c-109">지정 된 루트 구성 요소 `App` 선택기와 일치 하는 DOM 요소 안에 렌더링 해야 `app`:</span><span class="sxs-lookup"><span data-stu-id="4668c-109">specifies that the root component `App` should be rendered within a DOM element matching the selector `app`:</span></span>

```csharp
app.UseRouting(routes =>
{
    routes.MapRazorPages();
    routes.MapComponentHub<App>("app");
});
```

## <a name="route-templates"></a><span data-ttu-id="4668c-110">경로 템플릿</span><span class="sxs-lookup"><span data-stu-id="4668c-110">Route templates</span></span>

<span data-ttu-id="4668c-111">`<Router>` 구성 요소를 사용 하면 라우팅 및 경로 템플릿에 액세스할 수 있는 각 구성 요소에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-111">The `<Router>` component enables routing, and a route template is provided to each accessible component.</span></span> <span data-ttu-id="4668c-112">합니다 `<Router>` 구성 요소에 표시 되는 *Components/App.razor* 파일:</span><span class="sxs-lookup"><span data-stu-id="4668c-112">The `<Router>` component appears in the *Components/App.razor* file:</span></span>

```cshtml
<Router AppAssembly="typeof(Program).Assembly" />
```

<span data-ttu-id="4668c-113">때를 *.razor* 또는 *.cshtml* 파일을 `@page` 지시문 컴파일됩니다, 생성된 된 클래스는 지정 된을 <xref:Microsoft.AspNetCore.Mvc.RouteAttribute> 경로 템플릿을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-113">When a *.razor* or *.cshtml* file with an `@page` directive is compiled, the generated class is given a <xref:Microsoft.AspNetCore.Mvc.RouteAttribute> specifying the route template.</span></span> <span data-ttu-id="4668c-114">런타임 시 사용 하 여 구성 요소 클래스에 대 한 라우터 찾습니다는 `RouteAttribute` 하 고 어떤 구성 요소는 요청 된 URL과 일치 하는 경로 템플릿을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-114">At runtime, the router looks for component classes with a `RouteAttribute` and renders whichever component has a route template that matches the requested URL.</span></span>

<span data-ttu-id="4668c-115">여러 경로 템플릿 구성 요소에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-115">Multiple route templates can be applied to a component.</span></span> <span data-ttu-id="4668c-116">다음 구성 요소에 대 한 요청에 응답할 `/BlazorRoute` 고 `/DifferentBlazorRoute`:</span><span class="sxs-lookup"><span data-stu-id="4668c-116">The following component responds to requests for `/BlazorRoute` and `/DifferentBlazorRoute`:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRoute.cshtml?name=snippet_BlazorRoute)]

`<Router>` <span data-ttu-id="4668c-117">확인할 때 요청 된 경로 렌더링에 대 한 대체 (fallback) 구성 요소를 설정 하는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-117">supports setting a fallback component for rendering when a requested route isn't resolved.</span></span> <span data-ttu-id="4668c-118">설정 하 여이 옵트인 시나리오를 사용 하도록 설정 된 `FallbackComponent` 대체 (fallback) 구성 요소 클래스의 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-118">Enable this opt-in scenario by setting the `FallbackComponent` parameter to the type of the fallback component class.</span></span>

<span data-ttu-id="4668c-119">다음 예제에서는 설정에 정의 된 구성 요소 *Pages/MyFallbackRazorComponent.cshtml* 에 대 한 대체 (fallback) 구성 요소로 `<Router>`:</span><span class="sxs-lookup"><span data-stu-id="4668c-119">The following example sets a component defined in *Pages/MyFallbackRazorComponent.cshtml* as the fallback component for a `<Router>`:</span></span>

```cshtml
<Router ... FallbackComponent="typeof(Pages.MyFallbackRazorComponent)" />
```

> [!IMPORTANT]
> <span data-ttu-id="4668c-120">경로 올바르게 생성 하려면 앱을 포함 해야 합니다는 `<base>` 태그 해당 *wwwroot/index.html* 에 지정 된 앱 기본 경로 사용 하 여 파일을 `href` 특성 (`<base href="/">`).</span><span class="sxs-lookup"><span data-stu-id="4668c-120">To generate routes properly, the app must include a `<base>` tag in its *wwwroot/index.html* file with the app base path specified in the `href` attribute (`<base href="/">`).</span></span> <span data-ttu-id="4668c-121">자세한 내용은 <xref:host-and-deploy/razor-components-blazor/blazor#app-base-path>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4668c-121">For more information, see <xref:host-and-deploy/razor-components-blazor/blazor#app-base-path>.</span></span>

## <a name="route-parameters"></a><span data-ttu-id="4668c-122">경로 매개 변수</span><span class="sxs-lookup"><span data-stu-id="4668c-122">Route parameters</span></span>

<span data-ttu-id="4668c-123">라우터 경로 매개 변수를 사용 하 여 동일한 이름 (대/소문자 구분)를 사용 하 여 해당 구성 요소 매개 변수를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-123">The router uses route parameters to populate the corresponding component parameters with the same name (case insensitive):</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/RouteParameter.cshtml?name=snippet_RouteParameter&highlight=2,7-8)]

<span data-ttu-id="4668c-124">선택적 매개 변수는 아직 지원 되지 않습니다 하므로 두 `@page` 지시문 위의 예제에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-124">Optional parameters aren't supported yet, so two `@page` directives are applied in the example above.</span></span> <span data-ttu-id="4668c-125">첫 번째 매개 변수 없이 구성 요소에 대 한 탐색을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-125">The first permits navigation to the component without a parameter.</span></span> <span data-ttu-id="4668c-126">두 번째 `@page` 지시문은 합니다 `{text}` 경로 매개 변수 및 값을 할당 합니다 `Text` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-126">The second `@page` directive takes the `{text}` route parameter and assigns the value to the `Text` property.</span></span>

## <a name="route-constraints"></a><span data-ttu-id="4668c-127">경로 제약 조건</span><span class="sxs-lookup"><span data-stu-id="4668c-127">Route constraints</span></span>

<span data-ttu-id="4668c-128">경로 제약 조건 형식 구성 요소에 경로 세그먼트에서 일치를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-128">A route constraint enforces type matching on a route segment to a component.</span></span>

<span data-ttu-id="4668c-129">다음 예에서 경로 사용자 구성 요소를 경우에 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-129">In the following example, the route to the Users component only matches if:</span></span>

* <span data-ttu-id="4668c-130">`Id` 경로 세그먼트는 요청 URL에 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-130">An `Id` route segment is present on the request URL.</span></span>
* <span data-ttu-id="4668c-131">합니다 `Id` 세그먼트는 정수 (`int`).</span><span class="sxs-lookup"><span data-stu-id="4668c-131">The `Id` segment is an integer (`int`).</span></span>

[!code-cshtml[](routing/samples_snapshot/3.x/Constraint.cshtml?highlight=1)]

<span data-ttu-id="4668c-132">다음 표에 표시 된 경로 제약 조건을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-132">The route constraints shown in the following table are available.</span></span> <span data-ttu-id="4668c-133">고정 문화권을 사용 하 여 일치 하는 경로 제약 조건에 대 한이 경고 테이블에 대 한 자세한 내용은 아래를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4668c-133">For the route constraints that match with the invariant culture, see the warning below the table for more information.</span></span>

| <span data-ttu-id="4668c-134">제약 조건</span><span class="sxs-lookup"><span data-stu-id="4668c-134">Constraint</span></span> | <span data-ttu-id="4668c-135">예제</span><span class="sxs-lookup"><span data-stu-id="4668c-135">Example</span></span>           | <span data-ttu-id="4668c-136">일치하는 예제</span><span class="sxs-lookup"><span data-stu-id="4668c-136">Example Matches</span></span>                                                                  | <span data-ttu-id="4668c-137">고정</span><span class="sxs-lookup"><span data-stu-id="4668c-137">Invariant</span></span><br><span data-ttu-id="4668c-138">culture</span><span class="sxs-lookup"><span data-stu-id="4668c-138">culture</span></span><br><span data-ttu-id="4668c-139">일치</span><span class="sxs-lookup"><span data-stu-id="4668c-139">matching</span></span> |
| ---------- | ----------------- | -------------------------------------------------------------------------------- | :------------------------------: |
| `bool`     | `{active:bool}`   | `true`<span data-ttu-id="4668c-140">,</span><span class="sxs-lookup"><span data-stu-id="4668c-140">,</span></span> `FALSE`                                                                  | <span data-ttu-id="4668c-141">아니요</span><span class="sxs-lookup"><span data-stu-id="4668c-141">No</span></span>                               |
| `datetime` | `{dob:datetime}`  | `2016-12-31`<span data-ttu-id="4668c-142">,</span><span class="sxs-lookup"><span data-stu-id="4668c-142">,</span></span> `2016-12-31 7:32pm`                                                | <span data-ttu-id="4668c-143">예</span><span class="sxs-lookup"><span data-stu-id="4668c-143">Yes</span></span>                              |
| `decimal`  | `{price:decimal}` | `49.99`<span data-ttu-id="4668c-144">,</span><span class="sxs-lookup"><span data-stu-id="4668c-144">,</span></span> `-1,000.01`                                                             | <span data-ttu-id="4668c-145">예</span><span class="sxs-lookup"><span data-stu-id="4668c-145">Yes</span></span>                              |
| `double`   | `{weight:double}` | `1.234`<span data-ttu-id="4668c-146">,</span><span class="sxs-lookup"><span data-stu-id="4668c-146">,</span></span> `-1,001.01e8`                                                           | <span data-ttu-id="4668c-147">예</span><span class="sxs-lookup"><span data-stu-id="4668c-147">Yes</span></span>                              |
| `float`    | `{weight:float}`  | `1.234`<span data-ttu-id="4668c-148">,</span><span class="sxs-lookup"><span data-stu-id="4668c-148">,</span></span> `-1,001.01e8`                                                           | <span data-ttu-id="4668c-149">예</span><span class="sxs-lookup"><span data-stu-id="4668c-149">Yes</span></span>                              |
| `guid`     | `{id:guid}`       | `CD2C1638-1638-72D5-1638-DEADBEEF1638`<span data-ttu-id="4668c-150">,</span><span class="sxs-lookup"><span data-stu-id="4668c-150">,</span></span> `{CD2C1638-1638-72D5-1638-DEADBEEF1638}` | <span data-ttu-id="4668c-151">아니요</span><span class="sxs-lookup"><span data-stu-id="4668c-151">No</span></span>                               |
| `int`      | `{id:int}`        | `123456789`<span data-ttu-id="4668c-152">,</span><span class="sxs-lookup"><span data-stu-id="4668c-152">,</span></span> `-123456789`                                                        | <span data-ttu-id="4668c-153">예</span><span class="sxs-lookup"><span data-stu-id="4668c-153">Yes</span></span>                              |
| `long`     | `{ticks:long}`    | `123456789`<span data-ttu-id="4668c-154">,</span><span class="sxs-lookup"><span data-stu-id="4668c-154">,</span></span> `-123456789`                                                        | <span data-ttu-id="4668c-155">예</span><span class="sxs-lookup"><span data-stu-id="4668c-155">Yes</span></span>                              |

> [!WARNING]
> <span data-ttu-id="4668c-156">CLR 형식(예: `int` 또는 `DateTime`)으로 변환되는 URL을 확인하는 경로 제약 조건은 항상 고정 문화권을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-156">Route constraints that verify the URL and are converted to a CLR type (such as `int` or `DateTime`) always use the invariant culture.</span></span> <span data-ttu-id="4668c-157">이러한 제약 조건은 URL은 지역화될 수 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-157">These constraints assume that the URL is non-localizable.</span></span>

## <a name="navlink-component"></a><span data-ttu-id="4668c-158">NavLink 구성 요소</span><span class="sxs-lookup"><span data-stu-id="4668c-158">NavLink component</span></span>

<span data-ttu-id="4668c-159">HTML 대신 NavLink 구성 요소를 사용 하 여 `<a>` 탐색 링크를 만들 때 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-159">Use a NavLink component in place of HTML `<a>` elements when creating navigation links.</span></span> <span data-ttu-id="4668c-160">NavLink 구성 요소 처럼를 `<a>` 요소를 설정/해제 하는 점을 제외 하 고는 `active` CSS 클래스에 따라 해당 `href` 현재 URL과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-160">A NavLink component behaves like an `<a>` element, except it toggles an `active` CSS class based on whether its `href` matches the current URL.</span></span> <span data-ttu-id="4668c-161">`active` 클래스는 사용자는 페이지는 표시 된 탐색 링크 간에 활성 페이지를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-161">The `active` class helps a user understand which page is the active page among the navigation links displayed.</span></span>

<span data-ttu-id="4668c-162">다음 NavMenu 구성 요소를 만듭니다는 [부트스트랩](https://getbootstrap.com/docs/) NavLink 구성 요소를 사용 하는 방법에 설명 하는 탐색 모음:</span><span class="sxs-lookup"><span data-stu-id="4668c-162">The following NavMenu component creates a [Bootstrap](https://getbootstrap.com/docs/) navigation bar that demonstrates how to use NavLink components:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Shared/NavMenu.cshtml?name=snippet_NavLinks&highlight=4-6,9-11)]

<span data-ttu-id="4668c-163">두 개의 `NavLinkMatch` 옵션:</span><span class="sxs-lookup"><span data-stu-id="4668c-163">There are two `NavLinkMatch` options:</span></span>

* `NavLinkMatch.All` <span data-ttu-id="4668c-164">&ndash; 전체 현재 URL 일치 하는 경우는 NavLink 해야 활성 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-164">&ndash; Specifies that the NavLink should be active when it matches the entire current URL.</span></span>
* `NavLinkMatch.Prefix` <span data-ttu-id="4668c-165">&ndash; NavLink 함을 active 현재 URL의 접두사를 벗어난 일치할 경우를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-165">&ndash; Specifies that the NavLink should be active when it matches any prefix of the current URL.</span></span>

<span data-ttu-id="4668c-166">위의 예에서 홈 NavLink (`href=""`) 모든 Url과 일치 하 고 항상 수신 된 `active` CSS 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4668c-166">In the preceding example, the Home NavLink (`href=""`) matches all URLs and always receives the `active` CSS class.</span></span> <span data-ttu-id="4668c-167">두 번째 NavLink 데이터만 수신 합니다 `active` Blazor 경로 구성 요소를 방문 하는 사용자 클래스 (`href="BlazorRoute"`).</span><span class="sxs-lookup"><span data-stu-id="4668c-167">The second NavLink only receives the `active` class when the user visits the Blazor Route component (`href="BlazorRoute"`).</span></span>
