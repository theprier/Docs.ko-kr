---
title: ASP.NET Core MVC의 캐시 태그 도우미
author: pkellner
description: 캐시 태그 도우미 사용 방법 소개
ms.author: riande
ms.date: 02/14/2017
uid: mvc/views/tag-helpers/builtin-th/cache-tag-helper
ms.openlocfilehash: 969716e21211513053f52049368a0a7190ffba47
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276554"
---
# <a name="cache-tag-helper-in-aspnet-core-mvc"></a><span data-ttu-id="7e34c-103">ASP.NET Core MVC의 캐시 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="7e34c-103">Cache Tag Helper in ASP.NET Core MVC</span></span>

<span data-ttu-id="7e34c-104">작성자: [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="7e34c-104">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="7e34c-105">캐시 태그 도우미는 콘텐츠를 내부 ASP.NET Core 캐시 공급자에 캐시하여 ASP.NET Core 앱 성능을 획기적으로 개선하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-105">The Cache Tag Helper provides the ability to dramatically improve the performance of your ASP.NET Core app by caching its content to the internal ASP.NET Core cache provider.</span></span>

<span data-ttu-id="7e34c-106">Razor 보기 엔진은 기본 `expires-after`를 20분으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-106">The Razor View Engine sets the default `expires-after` to twenty minutes.</span></span>

<span data-ttu-id="7e34c-107">다음 Razor 태그는 날짜/시간을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-107">The following Razor markup caches the date/time:</span></span>

```cshtml
<cache>@DateTime.Now</cache>
```

<span data-ttu-id="7e34c-108">`CacheTagHelper`를 포함하는 페이지에 대한 첫 번째 요청은 현재 날짜/시간을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-108">The first request to the page that contains `CacheTagHelper` will display the current date/time.</span></span> <span data-ttu-id="7e34c-109">추가 요청은 캐시가 만료될 때까지(기본값 20분) 또는 메모리 압력에 의해 제거될 때까지 캐시된 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-109">Additional requests will show the cached value until the cache expires (default 20 minutes) or is evicted by memory pressure.</span></span>

<span data-ttu-id="7e34c-110">다음 특성을 사용하여 캐시 기간을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-110">You can set the cache duration with the following attributes:</span></span>

## <a name="cache-tag-helper-attributes"></a><span data-ttu-id="7e34c-111">캐시 태그 도우미 특성</span><span class="sxs-lookup"><span data-stu-id="7e34c-111">Cache Tag Helper Attributes</span></span>

- - -

### <a name="enabled"></a><span data-ttu-id="7e34c-112">사용</span><span class="sxs-lookup"><span data-stu-id="7e34c-112">enabled</span></span>    


| <span data-ttu-id="7e34c-113">특성 유형</span><span class="sxs-lookup"><span data-stu-id="7e34c-113">Attribute Type</span></span>    | <span data-ttu-id="7e34c-114">유효한 값</span><span class="sxs-lookup"><span data-stu-id="7e34c-114">Valid Values</span></span>      |
|----------------   |----------------   |
| <span data-ttu-id="7e34c-115">boolean</span><span class="sxs-lookup"><span data-stu-id="7e34c-115">boolean</span></span>           | <span data-ttu-id="7e34c-116">"true"(기본값)</span><span class="sxs-lookup"><span data-stu-id="7e34c-116">"true" (default)</span></span>  |
|                   | <span data-ttu-id="7e34c-117">"false"</span><span class="sxs-lookup"><span data-stu-id="7e34c-117">"false"</span></span>   |


<span data-ttu-id="7e34c-118">캐시 태그 도우미로 묶인 콘텐츠가 캐시되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-118">Determines whether the content enclosed by the Cache Tag Helper is cached.</span></span> <span data-ttu-id="7e34c-119">기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-119">The default is `true`.</span></span>  <span data-ttu-id="7e34c-120">`false`로 설정되면 이 캐시 태그 도우미는 렌더링된 출력에 캐싱 효과를 적용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-120">If set to `false` this Cache Tag Helper will have no caching effect on the rendered output.</span></span>

<span data-ttu-id="7e34c-121">예제:</span><span class="sxs-lookup"><span data-stu-id="7e34c-121">Example:</span></span>

```cshtml
<cache enabled="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-on"></a><span data-ttu-id="7e34c-122">expires-on</span><span class="sxs-lookup"><span data-stu-id="7e34c-122">expires-on</span></span> 

| <span data-ttu-id="7e34c-123">특성 유형</span><span class="sxs-lookup"><span data-stu-id="7e34c-123">Attribute Type</span></span> |           <span data-ttu-id="7e34c-124">예제 값</span><span class="sxs-lookup"><span data-stu-id="7e34c-124">Example Value</span></span>            |
|----------------|------------------------------------|
| <span data-ttu-id="7e34c-125">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="7e34c-125">DateTimeOffset</span></span> | <span data-ttu-id="7e34c-126">"@new DateTime(2025,1,29,17,02,0)"</span><span class="sxs-lookup"><span data-stu-id="7e34c-126">"@new DateTime(2025,1,29,17,02,0)"</span></span> |

<span data-ttu-id="7e34c-127">절대 만료 날짜를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-127">Sets an absolute expiration date.</span></span> <span data-ttu-id="7e34c-128">다음 예제는 2025년 1월 29일 오후 5시 2분이 될 때까지 캐시 태그 도우미의 콘텐츠를 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-128">The following example will cache the contents of the Cache Tag Helper until 5:02 PM on January 29, 2025.</span></span>

<span data-ttu-id="7e34c-129">예제:</span><span class="sxs-lookup"><span data-stu-id="7e34c-129">Example:</span></span>

```cshtml
<cache expires-on="@new DateTime(2025,1,29,17,02,0)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-after"></a><span data-ttu-id="7e34c-130">expires-after</span><span class="sxs-lookup"><span data-stu-id="7e34c-130">expires-after</span></span>

| <span data-ttu-id="7e34c-131">특성 유형</span><span class="sxs-lookup"><span data-stu-id="7e34c-131">Attribute Type</span></span> |        <span data-ttu-id="7e34c-132">예제 값</span><span class="sxs-lookup"><span data-stu-id="7e34c-132">Example Value</span></span>         |
|----------------|------------------------------|
|    <span data-ttu-id="7e34c-133">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="7e34c-133">TimeSpan</span></span>    | <span data-ttu-id="7e34c-134">"@TimeSpan.FromSeconds(120)"</span><span class="sxs-lookup"><span data-stu-id="7e34c-134">"@TimeSpan.FromSeconds(120)"</span></span> |

<span data-ttu-id="7e34c-135">콘텐츠를 캐시할 첫 번째 요청 시간부터 시간 길이를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-135">Sets the length of time from the first request time to cache the contents.</span></span> 

<span data-ttu-id="7e34c-136">예제:</span><span class="sxs-lookup"><span data-stu-id="7e34c-136">Example:</span></span>

```cshtml
<cache expires-after="@TimeSpan.FromSeconds(120)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-sliding"></a><span data-ttu-id="7e34c-137">expires-sliding</span><span class="sxs-lookup"><span data-stu-id="7e34c-137">expires-sliding</span></span>

| <span data-ttu-id="7e34c-138">특성 유형</span><span class="sxs-lookup"><span data-stu-id="7e34c-138">Attribute Type</span></span> |        <span data-ttu-id="7e34c-139">예제 값</span><span class="sxs-lookup"><span data-stu-id="7e34c-139">Example Value</span></span>        |
|----------------|-----------------------------|
|    <span data-ttu-id="7e34c-140">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="7e34c-140">TimeSpan</span></span>    | <span data-ttu-id="7e34c-141">"@TimeSpan.FromSeconds(60)"</span><span class="sxs-lookup"><span data-stu-id="7e34c-141">"@TimeSpan.FromSeconds(60)"</span></span> |

<span data-ttu-id="7e34c-142">캐시 항목이 액세스되지 않는 경우 캐시 항목을 제거해야 하는 시간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-142">Sets the time that a cache entry should be evicted if it has not been accessed.</span></span>

<span data-ttu-id="7e34c-143">예제:</span><span class="sxs-lookup"><span data-stu-id="7e34c-143">Example:</span></span>

```cshtml
<cache expires-sliding="@TimeSpan.FromSeconds(60)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-header"></a><span data-ttu-id="7e34c-144">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="7e34c-144">vary-by-header</span></span>

| <span data-ttu-id="7e34c-145">특성 유형</span><span class="sxs-lookup"><span data-stu-id="7e34c-145">Attribute Type</span></span>    | <span data-ttu-id="7e34c-146">예제 값</span><span class="sxs-lookup"><span data-stu-id="7e34c-146">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="7e34c-147">문자열</span><span class="sxs-lookup"><span data-stu-id="7e34c-147">String</span></span>            | <span data-ttu-id="7e34c-148">"User-Agent"</span><span class="sxs-lookup"><span data-stu-id="7e34c-148">"User-Agent"</span></span>                  |
|                   | <span data-ttu-id="7e34c-149">"User-Agent,content-encoding"</span><span class="sxs-lookup"><span data-stu-id="7e34c-149">"User-Agent,content-encoding"</span></span> |

<span data-ttu-id="7e34c-150">값이 변경되면 캐시 새로 고침을 트리거하는 단일 헤더 값 또는 쉼표로 구분된 헤더 값 목록을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-150">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when they change.</span></span> <span data-ttu-id="7e34c-151">다음 예제에서는 헤더 값 `User-Agent`를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-151">The following example monitors the header value `User-Agent`.</span></span> <span data-ttu-id="7e34c-152">이 예제는 웹 서버에 제공된 모든 `User-Agent`에 대한 콘텐츠를 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-152">The example will cache the content for every different `User-Agent` presented to the web server.</span></span>

<span data-ttu-id="7e34c-153">예제:</span><span class="sxs-lookup"><span data-stu-id="7e34c-153">Example:</span></span>

```cshtml
<cache vary-by-header="User-Agent">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-query"></a><span data-ttu-id="7e34c-154">vary-by-query</span><span class="sxs-lookup"><span data-stu-id="7e34c-154">vary-by-query</span></span>

| <span data-ttu-id="7e34c-155">특성 유형</span><span class="sxs-lookup"><span data-stu-id="7e34c-155">Attribute Type</span></span>    | <span data-ttu-id="7e34c-156">예제 값</span><span class="sxs-lookup"><span data-stu-id="7e34c-156">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="7e34c-157">문자열</span><span class="sxs-lookup"><span data-stu-id="7e34c-157">String</span></span>            | <span data-ttu-id="7e34c-158">"Make"</span><span class="sxs-lookup"><span data-stu-id="7e34c-158">"Make"</span></span>                |
|                   | <span data-ttu-id="7e34c-159">"Make,Model"</span><span class="sxs-lookup"><span data-stu-id="7e34c-159">"Make,Model"</span></span> |

<span data-ttu-id="7e34c-160">헤더 값이 변경되면 캐시 새로 고침을 트리거하는 단일 헤더 값 또는 쉼표로 구분된 헤더 값 목록을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-160">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header value changes.</span></span> <span data-ttu-id="7e34c-161">다음 예제에서는 `Make` 및 `Model` 값을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-161">The following example looks at the values of `Make` and `Model`.</span></span>

<span data-ttu-id="7e34c-162">예제:</span><span class="sxs-lookup"><span data-stu-id="7e34c-162">Example:</span></span>

```cshtml
<cache vary-by-query="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-route"></a><span data-ttu-id="7e34c-163">vary-by-route</span><span class="sxs-lookup"><span data-stu-id="7e34c-163">vary-by-route</span></span>

| <span data-ttu-id="7e34c-164">특성 유형</span><span class="sxs-lookup"><span data-stu-id="7e34c-164">Attribute Type</span></span>    | <span data-ttu-id="7e34c-165">예제 값</span><span class="sxs-lookup"><span data-stu-id="7e34c-165">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="7e34c-166">문자열</span><span class="sxs-lookup"><span data-stu-id="7e34c-166">String</span></span>            | <span data-ttu-id="7e34c-167">"Make"</span><span class="sxs-lookup"><span data-stu-id="7e34c-167">"Make"</span></span>                |
|                   | <span data-ttu-id="7e34c-168">"Make,Model"</span><span class="sxs-lookup"><span data-stu-id="7e34c-168">"Make,Model"</span></span> |

<span data-ttu-id="7e34c-169">경로 데이터 매개 변수 값이 변경되면 캐시 새로 고침을 트리거하는 단일 헤더 값 또는 쉼표로 구분된 헤더 값 목록을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-169">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the route data parameter value(s) change.</span></span> <span data-ttu-id="7e34c-170">예제:</span><span class="sxs-lookup"><span data-stu-id="7e34c-170">Example:</span></span>

<span data-ttu-id="7e34c-171">*Startup.cs*</span><span class="sxs-lookup"><span data-stu-id="7e34c-171">*Startup.cs*</span></span> 

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{Make?}/{Model?}");
```

<span data-ttu-id="7e34c-172">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="7e34c-172">*Index.cshtml*</span></span>

```cshtml
<cache vary-by-route="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-cookie"></a><span data-ttu-id="7e34c-173">vary-by-cookie</span><span class="sxs-lookup"><span data-stu-id="7e34c-173">vary-by-cookie</span></span>

| <span data-ttu-id="7e34c-174">특성 유형</span><span class="sxs-lookup"><span data-stu-id="7e34c-174">Attribute Type</span></span>    | <span data-ttu-id="7e34c-175">예제 값</span><span class="sxs-lookup"><span data-stu-id="7e34c-175">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="7e34c-176">문자열</span><span class="sxs-lookup"><span data-stu-id="7e34c-176">String</span></span>            | <span data-ttu-id="7e34c-177">".AspNetCore.Identity.Application"</span><span class="sxs-lookup"><span data-stu-id="7e34c-177">".AspNetCore.Identity.Application"</span></span>                |
|                   | <span data-ttu-id="7e34c-178">".AspNetCore.Identity.Application,HairColor"</span><span class="sxs-lookup"><span data-stu-id="7e34c-178">".AspNetCore.Identity.Application,HairColor"</span></span> |

<span data-ttu-id="7e34c-179">헤더 값이 변경되면 캐시 새로 고침을 트리거하는 단일 헤더 값 또는 쉼표로 구분된 헤더 값 목록을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-179">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header values(s) change.</span></span> <span data-ttu-id="7e34c-180">다음 예제에서는 ASP.NET ID와 연결된 쿠키를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-180">The following example looks at the cookie associated with ASP.NET Identity.</span></span> <span data-ttu-id="7e34c-181">사용자가 인증되면 캐시 새로 고침을 트리거하는 요청 쿠키를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-181">When a user is authenticated the request cookie to be set which triggers a cache refresh.</span></span>

<span data-ttu-id="7e34c-182">예제:</span><span class="sxs-lookup"><span data-stu-id="7e34c-182">Example:</span></span>

```cshtml
<cache vary-by-cookie=".AspNetCore.Identity.Application">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-user"></a><span data-ttu-id="7e34c-183">vary-by-user</span><span class="sxs-lookup"><span data-stu-id="7e34c-183">vary-by-user</span></span>

| <span data-ttu-id="7e34c-184">특성 유형</span><span class="sxs-lookup"><span data-stu-id="7e34c-184">Attribute Type</span></span>    | <span data-ttu-id="7e34c-185">예제 값</span><span class="sxs-lookup"><span data-stu-id="7e34c-185">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="7e34c-186">부울</span><span class="sxs-lookup"><span data-stu-id="7e34c-186">Boolean</span></span>             | <span data-ttu-id="7e34c-187">"true"</span><span class="sxs-lookup"><span data-stu-id="7e34c-187">"true"</span></span>                  |
|                     | <span data-ttu-id="7e34c-188">"false"(기본값)</span><span class="sxs-lookup"><span data-stu-id="7e34c-188">"false" (default)</span></span> |

<span data-ttu-id="7e34c-189">로그인한 사용자(또는 컨텍스트 보안 주체)가 변경되면 캐시를 다시 설정해야 하는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-189">Specifies whether or not the cache should reset when the logged-in user (or Context Principal) changes.</span></span> <span data-ttu-id="7e34c-190">현재 사용자를 요청 컨텍스트 보안 주체라고도 하며 `@User.Identity.Name`을 참조하여 Razor 보기에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-190">The current user is also known as the Request Context Principal and can be viewed in a Razor view by referencing `@User.Identity.Name`.</span></span>

<span data-ttu-id="7e34c-191">다음 예제는 현재 로그인한 사용자를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-191">The following example looks at the current logged in user.</span></span>  

<span data-ttu-id="7e34c-192">예제:</span><span class="sxs-lookup"><span data-stu-id="7e34c-192">Example:</span></span>

```cshtml
<cache vary-by-user="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

<span data-ttu-id="7e34c-193">이 특성을 사용하면 로그인 및 로그아웃 주기 동안 콘텐츠가 캐시에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-193">Using this attribute maintains the contents in cache through a log-in and log-out cycle.</span></span>  <span data-ttu-id="7e34c-194">`vary-by-user="true"`를 사용하면 로그인 및 로그아웃 작업에서 인증된 사용자에 대한 캐시를 무효화합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-194">When using `vary-by-user="true"`, a log-in and log-out action invalidates the cache for the authenticated user.</span></span>  <span data-ttu-id="7e34c-195">로그인 시 새로운 고유 쿠키 값이 생성되므로 캐시가 무효화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-195">The cache is invalidated because a new unique cookie value is generated on login.</span></span> <span data-ttu-id="7e34c-196">쿠키가 없거나 만료된 경우 캐시는 익명 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-196">Cache is maintained for the anonymous state when no cookie is present or has expired.</span></span> <span data-ttu-id="7e34c-197">즉, 로그인한 사용자가 없으면 캐시가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-197">This means if no user is logged in, the cache will be maintained.</span></span>

- - -

### <a name="vary-by"></a><span data-ttu-id="7e34c-198">vary-by</span><span class="sxs-lookup"><span data-stu-id="7e34c-198">vary-by</span></span>

| <span data-ttu-id="7e34c-199">특성 유형</span><span class="sxs-lookup"><span data-stu-id="7e34c-199">Attribute Type</span></span> | <span data-ttu-id="7e34c-200">예제 값</span><span class="sxs-lookup"><span data-stu-id="7e34c-200">Example Values</span></span> |
|----------------|----------------|
|     <span data-ttu-id="7e34c-201">문자열</span><span class="sxs-lookup"><span data-stu-id="7e34c-201">String</span></span>     |    <span data-ttu-id="7e34c-202">"@Model"</span><span class="sxs-lookup"><span data-stu-id="7e34c-202">"@Model"</span></span>    |

<span data-ttu-id="7e34c-203">캐시되는 데이터의 사용자 지정을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-203">Allows for customization of what data gets cached.</span></span> <span data-ttu-id="7e34c-204">특성의 문자열 값에서 참조하는 개체가 변경되면 캐시 태그 도우미의 콘텐츠가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-204">When the object referenced by the attribute's string value changes, the content of the Cache Tag Helper is updated.</span></span> <span data-ttu-id="7e34c-205">종종 모델 값의 문자열 연결이 이 특성에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-205">Often a string-concatenation of model values are assigned to this attribute.</span></span>  <span data-ttu-id="7e34c-206">연결된 값을 업데이트하면 캐시가 무효화된다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-206">Effectively, that means an update to any of the concatenated values invalidates the cache.</span></span>

<span data-ttu-id="7e34c-207">다음 예제에서는 보기를 렌더링하는 컨트롤러 메서드가 두 경로 매개 변수 `myParam1` 및 `myParam2`의 정수 값을 합산하고, 그 값을 단일 모델 속성으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-207">The following example assumes the controller method rendering the view sums the integer value of the two route parameters, `myParam1` and `myParam2`, and returns that as the single model property.</span></span> <span data-ttu-id="7e34c-208">이 합계가 변경되면 캐시 태그 도우미의 콘텐츠가 다시 렌더링 및 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-208">When this sum changes, the content of the Cache Tag Helper is rendered and cached again.</span></span>  

<span data-ttu-id="7e34c-209">예제:</span><span class="sxs-lookup"><span data-stu-id="7e34c-209">Example:</span></span>

<span data-ttu-id="7e34c-210">작업:</span><span class="sxs-lookup"><span data-stu-id="7e34c-210">Action:</span></span>

```csharp
public IActionResult Index(string myParam1,string myParam2,string myParam3)
{
    int num1;
    int num2;
    int.TryParse(myParam1, out num1);
    int.TryParse(myParam2, out num2);
    return View(viewName, num1 + num2);
}
```

<span data-ttu-id="7e34c-211">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="7e34c-211">*Index.cshtml*</span></span>

```cshtml
<cache vary-by="@Model"">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="priority"></a><span data-ttu-id="7e34c-212">priority</span><span class="sxs-lookup"><span data-stu-id="7e34c-212">priority</span></span>

| <span data-ttu-id="7e34c-213">특성 유형</span><span class="sxs-lookup"><span data-stu-id="7e34c-213">Attribute Type</span></span>    | <span data-ttu-id="7e34c-214">예제 값</span><span class="sxs-lookup"><span data-stu-id="7e34c-214">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="7e34c-215">CacheItemPriority</span><span class="sxs-lookup"><span data-stu-id="7e34c-215">CacheItemPriority</span></span>  | <span data-ttu-id="7e34c-216">"High"</span><span class="sxs-lookup"><span data-stu-id="7e34c-216">"High"</span></span>                   |
|                    | <span data-ttu-id="7e34c-217">"Low"</span><span class="sxs-lookup"><span data-stu-id="7e34c-217">"Low"</span></span> |
|                    | <span data-ttu-id="7e34c-218">"NeverRemove"</span><span class="sxs-lookup"><span data-stu-id="7e34c-218">"NeverRemove"</span></span> |
|                    | <span data-ttu-id="7e34c-219">"Normal"</span><span class="sxs-lookup"><span data-stu-id="7e34c-219">"Normal"</span></span> |

<span data-ttu-id="7e34c-220">기본 제공 캐시 공급자에게 캐시 제거 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-220">Provides cache eviction guidance to the built-in cache provider.</span></span> <span data-ttu-id="7e34c-221">웹 서버는 메모리가 부족할 경우 가장 먼저 `Low` 캐시 항목을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-221">The web server will evict `Low` cache entries first when it's under memory pressure.</span></span>

<span data-ttu-id="7e34c-222">예제:</span><span class="sxs-lookup"><span data-stu-id="7e34c-222">Example:</span></span>

```cshtml
<cache priority="High">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

<span data-ttu-id="7e34c-223">`priority` 특성은 특정 수준의 캐시 보존을 보장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-223">The `priority` attribute doesn't guarantee a specific level of cache retention.</span></span> <span data-ttu-id="7e34c-224">`CacheItemPriority`는 권장 사항일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-224">`CacheItemPriority` is only a suggestion.</span></span> <span data-ttu-id="7e34c-225">이 특성을 `NeverRemove`로 설정해도 캐시가 항상 보존된다는 보장은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-225">Setting this attribute to `NeverRemove` doesn't guarantee that the cache will always be retained.</span></span> <span data-ttu-id="7e34c-226">자세한 내용은 [추가 리소스](#additional-resources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e34c-226">See [Additional Resources](#additional-resources) for more information.</span></span>

<span data-ttu-id="7e34c-227">캐시 태그 도우미는 [메모리 캐시 서비스](xref:performance/caching/memory)에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-227">The Cache Tag Helper is dependent on the [memory cache service](xref:performance/caching/memory).</span></span> <span data-ttu-id="7e34c-228">서비스가 추가되지 않은 경우 캐시 태그 도우미가 서비스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-228">The Cache Tag Helper adds the service if it has not been added.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7e34c-229">추가 자료</span><span class="sxs-lookup"><span data-stu-id="7e34c-229">Additional resources</span></span>

* [<span data-ttu-id="7e34c-230">메모리 내 캐시</span><span class="sxs-lookup"><span data-stu-id="7e34c-230">Cache in-memory</span></span>](xref:performance/caching/memory)
* [<span data-ttu-id="7e34c-231">ID 소개</span><span class="sxs-lookup"><span data-stu-id="7e34c-231">Introduction to Identity</span></span>](xref:security/authentication/identity)
