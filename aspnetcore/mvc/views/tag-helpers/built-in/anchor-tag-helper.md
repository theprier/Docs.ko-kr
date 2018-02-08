---
title: "ASP.NET Core의 앵커 태그 도우미"
author: pkellner
description: "앵커 태그 도우미 사용 방법 소개"
manager: wpickett
ms.author: riande
ms.date: 12/20/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/anchor-tag-helper
ms.openlocfilehash: 404fc7bc3b35114066f035e1ac28d10a8279ccbc
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="anchor-tag-helper"></a><span data-ttu-id="2a1ec-103">앵커 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="2a1ec-103">Anchor Tag Helper</span></span>

<span data-ttu-id="2a1ec-104">작성자: [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="2a1ec-104">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="2a1ec-105">앵커 태그 도우미는 새 특성을 추가하여 HTML 앵커(`<a ... ></a>`) 태그를 강화합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-105">The Anchor Tag Helper enhances the HTML anchor (`<a ... ></a>`) tag by adding new attributes.</span></span> <span data-ttu-id="2a1ec-106">생성되는(`href` 태그에서) 링크는 새 특성을 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-106">The link generated (on the `href` tag) is created using the new attributes.</span></span> <span data-ttu-id="2a1ec-107">해당 URL은 https 같은 선택적 프로토콜을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-107">That URL can include an optional protocol such as https.</span></span>

<span data-ttu-id="2a1ec-108">아래의 스피커 컨트롤러는 이 문서의 샘플에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-108">The speaker controller below is used in samples in this document.</span></span>

<span data-ttu-id="2a1ec-109">**SpeakerController.cs**</span><span class="sxs-lookup"><span data-stu-id="2a1ec-109">**SpeakerController.cs**</span></span> 

[!code-csharp[SpeakerController](sample/TagHelpersBuiltInAspNetCore/src/TagHelpersBuiltInAspNetCore/Controllers/SpeakerController.cs)]


## <a name="anchor-tag-helper-attributes"></a><span data-ttu-id="2a1ec-110">앵커 태그 도우미 특성</span><span class="sxs-lookup"><span data-stu-id="2a1ec-110">Anchor Tag Helper Attributes</span></span>

### <a name="asp-controller"></a><span data-ttu-id="2a1ec-111">asp-controller</span><span class="sxs-lookup"><span data-stu-id="2a1ec-111">asp-controller</span></span>

<span data-ttu-id="2a1ec-112">`asp-controller`는 URL을 생성하는 데 사용할 컨트롤러를 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-112">`asp-controller` is used to associate which controller will be used to generate the URL.</span></span> <span data-ttu-id="2a1ec-113">지정된 컨트롤러가 현재 프로젝트에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-113">The controllers specified must exist in the current project.</span></span> <span data-ttu-id="2a1ec-114">다음 코드는 모든 스피커를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-114">The following code lists all speakers:</span></span> 

```cshtml
<a asp-controller="Speaker" asp-action="Index">All Speakers</a>
```

<span data-ttu-id="2a1ec-115">생성된 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-115">The generated markup will be:</span></span>

```html
<a href="/Speaker">All Speakers</a>
```

<span data-ttu-id="2a1ec-116">`asp-controller`를 지정하고 `asp-action`을 지정하지 않으면 기본 `asp-action`이 현재 실행 중인 보기의 기본 컨트롤러 메서드가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-116">If the `asp-controller` is specified and `asp-action` isn't, the default `asp-action` will be the default controller method of the currently executing view.</span></span> <span data-ttu-id="2a1ec-117">즉, 위의 예에서 `asp-action`을 생략하면 이 앵커 태그 도우미는 *HomeController*의 `Index` 보기(**/Home**)에서 생성되고, 생성된 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-117">That is, in the above example, if `asp-action` is left out, and this Anchor Tag Helper is generated from *HomeController*'s `Index` view (**/Home**), the generated markup will be:</span></span>

```html
<a href="/Home">All Speakers</a>
```

### <a name="asp-action"></a><span data-ttu-id="2a1ec-118">asp-action</span><span class="sxs-lookup"><span data-stu-id="2a1ec-118">asp-action</span></span>

<span data-ttu-id="2a1ec-119">`asp-action`은 생성되는 `href`에 포함할 컨트롤러의 작업 메서드 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-119">`asp-action` is the name of the action method in the controller that will be included in the generated `href`.</span></span> <span data-ttu-id="2a1ec-120">예를 들어 다음 코드는 생성된 `href`가 스피커 세부 정보 페이지를 가리키도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-120">For example, the following code set the generated `href` to point to the speaker detail page:</span></span>

```html
<a asp-controller="Speaker" asp-action="Detail">Speaker Detail</a>
```

<span data-ttu-id="2a1ec-121">생성된 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-121">The generated markup will be:</span></span>

```html
<a href="/Speaker/Detail">Speaker Detail</a>
```

<span data-ttu-id="2a1ec-122">`asp-controller` 특성을 지정하지 않으면 현재 보기를 실행 중인 보기를 호출하는 기본 컨트롤러가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-122">If no `asp-controller` attribute is specified, the default controller calling the view executing the current view will be used.</span></span>  
 
<span data-ttu-id="2a1ec-123">`asp-action` 특성이 `Index`이면 URL에 아무 작업도 추가되지 않고, 기본 `Index` 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-123">If the attribute `asp-action` is `Index`, then no action is appended to the URL, leading to the default `Index` method being called.</span></span> <span data-ttu-id="2a1ec-124">지정된(또는 기본값으로 설정된) 작업은 `asp-controller`에서 참조되는 컨트롤러에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-124">The action specified (or defaulted), must exist in the controller referenced in `asp-controller`.</span></span>

### <a name="asp-page"></a><span data-ttu-id="2a1ec-125">asp-page</span><span class="sxs-lookup"><span data-stu-id="2a1ec-125">asp-page</span></span>

<span data-ttu-id="2a1ec-126">앵커 태그에 `asp-page` 특성을 사용하여 특정 페이지를 가리키도록 URL을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-126">Use the `asp-page` attribute in an anchor tag to set its URL to point to a specific page.</span></span> <span data-ttu-id="2a1ec-127">페이지 이름에 슬래시("/")를 접두사로 사용하여 URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-127">Prefixing the page name with a forward slash "/" creates the URL.</span></span> <span data-ttu-id="2a1ec-128">아래 샘플의 URL은 현재 디렉터리의 "스피커" 페이지를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-128">The URL in the sample below points to the "Speaker" page in the current directory.</span></span>

```cshtml
<a asp-page="/Speakers">All Speakers</a>
```

<span data-ttu-id="2a1ec-129">이전 코드 샘플의 `asp-page` 특성은 보기에서 다음 코드 조각과 비슷한 HTML 출력을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-129">The `asp-page` attribute in the previous code sample renders HTML output in the view that's similar to the following snippet:</span></span>

```html
<a href="/items?page=%2FSpeakers">Speakers</a>
```

<span data-ttu-id="2a1ec-130">`asp-page` 특성은 `asp-route`, `asp-controller` 및 `asp-action` 특성과 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-130">The `asp-page` attribute is mutually exclusive with the `asp-route`, `asp-controller`, and `asp-action` attributes.</span></span> <span data-ttu-id="2a1ec-131">그러나 다음 코드 샘플에서 보여주듯이, `asp-page`는 `asp-route-id`와 함께 사용하여 라우팅을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-131">However, `asp-page` can be used with `asp-route-id` to control routing, as the following code sample demonstrates:</span></span>

```cshtml
<a asp-page="/Speaker" asp-route-id="@speaker.Id">View Speaker</a>
```

<span data-ttu-id="2a1ec-132">`asp-route-id`는 다음 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-132">The `asp-route-id` produces the following output:</span></span>

```html
https://localhost:44399/Speakers/Index/2?page=%2FSpeaker
```

> [!NOTE]
> <span data-ttu-id="2a1ec-133">`asp-page` 특성을 Razor 페이지에 사용하려면 URL이 상대 경로(예: `"./Speaker"`)여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-133">To use the `asp-page` attribute in Razor Pages, the URLs must be a relative path, for example `"./Speaker"`.</span></span> <span data-ttu-id="2a1ec-134">`asp-page` 특성의 상대 경로는 MVC 보기에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-134">Relative paths in the `asp-page` attribute are not available in MVC views.</span></span> <span data-ttu-id="2a1ec-135">MVC 보기에는 "/" 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-135">Use the "/" syntax for MVC views instead.</span></span>

### <a name="asp-route-value"></a><span data-ttu-id="2a1ec-136">asp-route-{value}</span><span class="sxs-lookup"><span data-stu-id="2a1ec-136">asp-route-{value}</span></span>

<span data-ttu-id="2a1ec-137">`asp-route-`는 와일드 카드 경로 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-137">`asp-route-` is a wild card route prefix.</span></span> <span data-ttu-id="2a1ec-138">후행 대시 뒤에 배치되는 모든 값은 잠재적 경로 매개 변수로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-138">Any value you put after the trailing dash will be interpreted as a potential route parameter.</span></span> <span data-ttu-id="2a1ec-139">기본 경로를 찾을 수 없는 경우 이 경로 접두사는 생성되는 href에 요청 매개 변수 및 값으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-139">If a default route isn't found, this route prefix will be appended to the generated href as a request parameter and value.</span></span> <span data-ttu-id="2a1ec-140">그렇지 않은 경우 이 경로 접두사는 경로 템플릿에서 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-140">Otherwise it will be substituted in the route template.</span></span>

<span data-ttu-id="2a1ec-141">다음과 같이 정의된 컨트롤러 메서드가 있다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-141">Assuming you have a controller method defined as follows:</span></span>

```csharp
public IActionResult AnchorTagHelper(string id)
{
    var speaker = new SpeakerData()
    {
        SpeakerId = 12
    };
    return View(viewName, speaker);
}
```

<span data-ttu-id="2a1ec-142">그리고 *Startup.cs*에 다음과 같은 기본 경로 템플릿이 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-142">And have the default route template defined in your *Startup.cs* as follows:</span></span>

```csharp
app.UseMvc(routes =>
{
   routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id?}");
});

```

<span data-ttu-id="2a1ec-143">컨트롤러에서 보기로 전달된 **스피커** 모델 매개 변수를 사용하는 데 필요한 앵커 태그 도우미를 포함하고 있는 **cshtml** 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-143">The **cshtml** file that contains the Anchor Tag Helper necessary to use the **speaker** model parameter passed in from the controller to the view is as follows:</span></span>

```cshtml
@model SpeakerData
<!DOCTYPE html>
<html><body>
<a asp-controller='Speaker' asp-action='Detail' asp-route-id=@Model.SpeakerId>SpeakerId: @Model.SpeakerId</a>
<body></html>
```

<span data-ttu-id="2a1ec-144">**id**가 기본 경로에서 발견되었기 때문에 다음과 같은 HTML이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-144">The generated HTML will then be as follows because **id** was found in the default route.</span></span>

```html
<a href='/Speaker/Detail/12'>SpeakerId: 12</a>
```

<span data-ttu-id="2a1ec-145">경로 접두사가 발견된 라우팅 템플릿의 일부가 아닌 경우 **cshtml** 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-145">If the route prefix isn't part of the routing template found, which is the case with the following **cshtml** file:</span></span>

```cshtml
@model SpeakerData
<!DOCTYPE html>
<html><body>
<a asp-controller='Speaker' asp-action='Detail' asp-route-speakerid=@Model.SpeakerId>SpeakerId: @Model.SpeakerId</a>
<body></html>
```

<span data-ttu-id="2a1ec-146">매칭된 경로에서 **speakerid**를 찾지 못했기 때문에 다음과 같은 HTML이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-146">The generated HTML will then be as follows because **speakerid** wasn't found in the route matched:</span></span>

```html
<a href='/Speaker/Detail?speakerid=12'>SpeakerId: 12</a>
```

<span data-ttu-id="2a1ec-147">`asp-controller` 또는 `asp-action`을 지정하지 않으면 동일한 기본 처리가 `asp-route` 특성에 있는 그대로 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-147">If either `asp-controller` or `asp-action` are not specified, then the same default processing is followed as is in the `asp-route` attribute.</span></span>

### <a name="asp-route"></a><span data-ttu-id="2a1ec-148">asp-route</span><span class="sxs-lookup"><span data-stu-id="2a1ec-148">asp-route</span></span>

<span data-ttu-id="2a1ec-149">`asp-route`는 명명된 경로에 직접 연결되는 URL을 만드는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-149">`asp-route` provides a way to create a URL that links directly to a named route.</span></span> <span data-ttu-id="2a1ec-150">라우팅 특성을 사용하면 `SpeakerController`에서 보여주는 것처럼 이름을 지정하고 해당 `Evaluations` 메서드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-150">Using routing attributes, a route can be named as shown in the `SpeakerController` and used in its `Evaluations` method.</span></span>

<span data-ttu-id="2a1ec-151">`Name = "speakerevals"`는 `/Speaker/Evaluations` URL을 사용하여 해당 컨트롤러 메서드에 직접 연결되는 경로를 생성하라고 앵커 태그 도우미에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-151">`Name = "speakerevals"` tells the Anchor Tag Helper to generate a route directly to that controller method using the URL `/Speaker/Evaluations`.</span></span> <span data-ttu-id="2a1ec-152">`asp-route` 외에 `asp-controller` 또는 `asp-action`을 지정하면 예상과 다른 경로가 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-152">If `asp-controller` or `asp-action` is specified in addition to `asp-route`, the route generated may not be what you expect.</span></span> <span data-ttu-id="2a1ec-153">경로 충돌을 방지하기 위해 `asp-route`를 `asp-controller` 또는 `asp-action` 특성과 함께 사용하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-153">`asp-route` shouldn't be used with either of the attributes `asp-controller` or `asp-action` to avoid a route conflict.</span></span>

### <a name="asp-all-route-data"></a><span data-ttu-id="2a1ec-154">asp-all-route-data</span><span class="sxs-lookup"><span data-stu-id="2a1ec-154">asp-all-route-data</span></span>

<span data-ttu-id="2a1ec-155">`asp-all-route-data`를 사용하면 키가 매개 변수이고 값은 그 키와 연결된 값인 키 값 쌍 사전을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-155">`asp-all-route-data` allows creating a dictionary of key value pairs where the key is the parameter name and the value is the value associated with that key.</span></span>

<span data-ttu-id="2a1ec-156">아래 예제처럼 인라인 사전이 만들어지고 razor 보기에 데이터가 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-156">As the example below shows, an inline dictionary is created and the data is passed to the razor view.</span></span> <span data-ttu-id="2a1ec-157">모델을 사용하여 데이터를 전달하는 방법도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-157">As an alternative, the data could also be passed in with your model.</span></span>

```cshtml
@{
    var dict =
        new Dictionary<string, string>
        {
            {"speakerId", "11"},
            {"currentYear", "true"}
        };
}
<a asp-route="speakerevalscurrent"
asp-all-route-data="dict">SpeakerEvals</a>
```

<span data-ttu-id="2a1ec-158">위의 코드는 http://localhost/Speaker/EvaluationsCurrent?speakerId=11&currentYear=true URL을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-158">The code above generates the following URL: http://localhost/Speaker/EvaluationsCurrent?speakerId=11&currentYear=true</span></span>

<span data-ttu-id="2a1ec-159">링크를 클릭하면 컨트롤러 메서드 `EvaluationsCurrent`가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-159">When the link is clicked, the controller method `EvaluationsCurrent` is called.</span></span> <span data-ttu-id="2a1ec-160">해당 컨트롤러에는 `asp-all-route-data` 사전에서 만들어진 항목과 일치하는 두 개의 문자열 매개 변수가 있기 때문에 이 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-160">It's called because that controller has two string parameters that match what has been created from the `asp-all-route-data` dictionary.</span></span>

<span data-ttu-id="2a1ec-161">사전에 있는 아무 키가 경로 매개 변수와 일치하는 경우 경로에서 해당 값이 적절하게 대체되고 일치하지 않는 다른 값은 요청 매개 변수로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-161">If any keys in the dictionary match route parameters, those values will be substituted in the route as appropriate and the other non-matching values will be generated as request parameters.</span></span>

### <a name="asp-fragment"></a><span data-ttu-id="2a1ec-162">asp-fragment</span><span class="sxs-lookup"><span data-stu-id="2a1ec-162">asp-fragment</span></span>

<span data-ttu-id="2a1ec-163">`asp-fragment`는 URL에 추가할 URL 조각을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-163">`asp-fragment` defines a URL fragment to append to the URL.</span></span> <span data-ttu-id="2a1ec-164">앵커 태그 도우미는 해시 문자(#)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-164">The Anchor Tag Helper will add the hash character (#).</span></span> <span data-ttu-id="2a1ec-165">태그를 만들면:</span><span class="sxs-lookup"><span data-stu-id="2a1ec-165">If you create a tag:</span></span>

```cshtml
<a asp-action="Evaluations" asp-controller="Speaker"  
   asp-fragment="SpeakerEvaluations">About Speaker Evals</a>
```

<span data-ttu-id="2a1ec-166">http://localhost/Speaker/Evaluations#SpeakerEvaluations URL이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-166">The generated URL will be: http://localhost/Speaker/Evaluations#SpeakerEvaluations</span></span>

<span data-ttu-id="2a1ec-167">해시 태그는 클라이언트 쪽 응용 프로그램을 빌드할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-167">Hash tags are useful when building client-side applications.</span></span> <span data-ttu-id="2a1ec-168">다음과 같이 JavaScript에서 손쉽게 만들고 검색하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-168">They can be used for easy marking and searching in JavaScript, for example.</span></span>

### <a name="asp-area"></a><span data-ttu-id="2a1ec-169">asp-area</span><span class="sxs-lookup"><span data-stu-id="2a1ec-169">asp-area</span></span>

<span data-ttu-id="2a1ec-170">`asp-area`는 ASP.NET Core에서 적절한 경로를 설정하기 위해 사용하는 영역 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-170">`asp-area` sets the area name that ASP.NET Core uses to set the appropriate route.</span></span> <span data-ttu-id="2a1ec-171">아래는 영역 특성으로 인해 경로가 다시 매핑되는 원리를 보여주는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-171">Below are examples of how the area attribute causes a remapping of routes.</span></span> <span data-ttu-id="2a1ec-172">`asp-area`를 Blogs로 설정하면 이 앵커 태그에 대해 연결된 컨트롤러 및 보기의 경로에 `Areas/Blogs` 디렉터리가 접두사로 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-172">Setting `asp-area` to Blogs prefixes the directory `Areas/Blogs` to the routes of the associated controllers and views for this anchor tag.</span></span>

* <span data-ttu-id="2a1ec-173">프로젝트 이름</span><span class="sxs-lookup"><span data-stu-id="2a1ec-173">Project name</span></span>
  * <span data-ttu-id="2a1ec-174">wwwroot</span><span class="sxs-lookup"><span data-stu-id="2a1ec-174">wwwroot</span></span>
  * <span data-ttu-id="2a1ec-175">영역</span><span class="sxs-lookup"><span data-stu-id="2a1ec-175">Areas</span></span>
    * <span data-ttu-id="2a1ec-176">블로그</span><span class="sxs-lookup"><span data-stu-id="2a1ec-176">Blogs</span></span>
      * <span data-ttu-id="2a1ec-177">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="2a1ec-177">Controllers</span></span>
        * <span data-ttu-id="2a1ec-178">HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="2a1ec-178">HomeController.cs</span></span>
      * <span data-ttu-id="2a1ec-179">보기</span><span class="sxs-lookup"><span data-stu-id="2a1ec-179">Views</span></span>
        * <span data-ttu-id="2a1ec-180">홈</span><span class="sxs-lookup"><span data-stu-id="2a1ec-180">Home</span></span>
          * <span data-ttu-id="2a1ec-181">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="2a1ec-181">Index.cshtml</span></span>
          * <span data-ttu-id="2a1ec-182">AboutBlog.cshtml</span><span class="sxs-lookup"><span data-stu-id="2a1ec-182">AboutBlog.cshtml</span></span>
  * <span data-ttu-id="2a1ec-183">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="2a1ec-183">Controllers</span></span>

<span data-ttu-id="2a1ec-184">```AboutBlog.cshtml``` 파일을 참조할 때 ```area="Blogs"``` 같은 유효한 영역 태그를 지정하면 앵커 태그 도우미를 사용하여 다음 예처럼 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-184">Specifying an area tag that's valid, such as ```area="Blogs"``` when referencing the ```AboutBlog.cshtml``` file will look like the following using the Anchor Tag Helper.</span></span>

```cshtml
<a asp-action="AboutBlog" asp-controller="Home" asp-area="Blogs">Blogs About</a>
```

<span data-ttu-id="2a1ec-185">생성된 HTML에는 영역 세그먼트가 포함되며 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-185">The generated HTML will include the areas segment and will be as follows:</span></span>

```html
<a href="/Blogs/Home/AboutBlog">Blogs About</a>
```

> [!TIP]
> <span data-ttu-id="2a1ec-186">MVC 영역이 웹 응용 프로그램에서 작동하려면 경로 템플릿에 영역의 참조가 포함되어야 합니다(있는 경우).</span><span class="sxs-lookup"><span data-stu-id="2a1ec-186">For MVC areas to work in a web application, the route template must include a reference to the area if it exists.</span></span> <span data-ttu-id="2a1ec-187">`routes.MapRoute` 메서드 호출의 두 번째 매개 변수인 이 템플릿은 `template: '"{area:exists}/{controller=Home}/{action=Index}"'`와 비슷하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-187">That template, which is the second parameter of the `routes.MapRoute` method call, will appear as: `template: '"{area:exists}/{controller=Home}/{action=Index}"'`</span></span>

### <a name="asp-protocol"></a><span data-ttu-id="2a1ec-188">asp-protocol</span><span class="sxs-lookup"><span data-stu-id="2a1ec-188">asp-protocol</span></span>

<span data-ttu-id="2a1ec-189">`asp-protocol`은 URL에서 프로토콜(예: `https`)을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-189">The `asp-protocol` is for specifying a protocol (such as `https`) in your URL.</span></span> <span data-ttu-id="2a1ec-190">프로토콜을 포함하는 앵커 태그 도우미 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-190">An example Anchor Tag Helper that includes the protocol will look as follows:</span></span>

```<a asp-protocol="https" asp-action="About" asp-controller="Home">About</a>```

<span data-ttu-id="2a1ec-191">그리고 다음과 같은 HTML을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-191">and will generate HTML as follows:</span></span>

```<a href="https://localhost/Home/About">About</a>```

<span data-ttu-id="2a1ec-192">이 예제의 도메인인 localhost이지만, 앵커 태그 도우미는 URL을 생성할 때 웹 사이트의 공용 도메인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1ec-192">The domain in the example is localhost, but the Anchor Tag Helper uses the website's public domain when generating the URL.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2a1ec-193">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2a1ec-193">Additional resources</span></span>

* [<span data-ttu-id="2a1ec-194">영역</span><span class="sxs-lookup"><span data-stu-id="2a1ec-194">Areas</span></span>](xref:mvc/controllers/areas)
