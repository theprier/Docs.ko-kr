---
title: "ASP.NET Core MVC에서에서 태그 도우미를 캐시 합니다."
author: pkellner
description: "캐시 태그 도우미를 사용 하는 방법을 보여 줍니다."
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: mvc/views/tag-helpers/builtin-th/cache-tag-helper
ms.openlocfilehash: dfd9c3c0c4e50a99e4f8703b01bd9b384930b87a
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="cache-tag-helper-in-aspnet-core-mvc"></a><span data-ttu-id="95a6a-103">ASP.NET Core MVC에서에서 태그 도우미를 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-103">Cache Tag Helper in ASP.NET Core MVC</span></span>

<span data-ttu-id="95a6a-104">작성자: [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="95a6a-104">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="95a6a-105">캐시 태그 도우미의 내부 ASP.NET Core 캐시 공급자를 해당 콘텐츠를 캐시 하 여 ASP.NET Core 응용 프로그램의 성능이 크게 향상 하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-105">The Cache Tag Helper provides the ability to dramatically improve the performance of your ASP.NET Core app by caching its content to the internal ASP.NET Core cache provider.</span></span>

<span data-ttu-id="95a6a-106">Razor 뷰 엔진 기본 설정 `expires-after` 20 분입니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-106">The Razor View Engine sets the default `expires-after` to twenty minutes.</span></span>

<span data-ttu-id="95a6a-107">날짜/시간을 캐시 하는 다음 Razor 태그:</span><span class="sxs-lookup"><span data-stu-id="95a6a-107">The following Razor markup caches the date/time:</span></span>

```cshtml
<cache>@DateTime.Now</cache>
```

<span data-ttu-id="95a6a-108">첫 번째 요청을 포함 하는 페이지 `CacheTagHelper` 현재 날짜/시간을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-108">The first request to the page that contains `CacheTagHelper` will display the current date/time.</span></span> <span data-ttu-id="95a6a-109">추가 요청은 캐시 (기본값: 20 분)을 만료 되거나 메모리가 중에 의해 제거 될 때까지 캐시 된 값이 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-109">Additional requests will show the cached value until the cache expires (default 20 minutes) or is evicted by memory pressure.</span></span>

<span data-ttu-id="95a6a-110">다음 특성을 가진 캐시 기간을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-110">You can set the cache duration with the following attributes:</span></span>

## <a name="cache-tag-helper-attributes"></a><span data-ttu-id="95a6a-111">캐시 태그 도우미 특성</span><span class="sxs-lookup"><span data-stu-id="95a6a-111">Cache Tag Helper Attributes</span></span>

- - -

### <a name="enabled"></a><span data-ttu-id="95a6a-112">사용</span><span class="sxs-lookup"><span data-stu-id="95a6a-112">enabled</span></span>    


| <span data-ttu-id="95a6a-113">특성 유형</span><span class="sxs-lookup"><span data-stu-id="95a6a-113">Attribute Type</span></span>    | <span data-ttu-id="95a6a-114">유효한 값</span><span class="sxs-lookup"><span data-stu-id="95a6a-114">Valid Values</span></span>      |
|----------------   |----------------   |
| <span data-ttu-id="95a6a-115">boolean</span><span class="sxs-lookup"><span data-stu-id="95a6a-115">boolean</span></span>           | <span data-ttu-id="95a6a-116">"true" (기본값)</span><span class="sxs-lookup"><span data-stu-id="95a6a-116">"true" (default)</span></span>  |
|                   | <span data-ttu-id="95a6a-117">"false"</span><span class="sxs-lookup"><span data-stu-id="95a6a-117">"false"</span></span>   |


<span data-ttu-id="95a6a-118">캐시 태그 도우미 포함 되는 콘텐츠가 캐시 되 고 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-118">Determines whether the content enclosed by the Cache Tag Helper is cached.</span></span> <span data-ttu-id="95a6a-119">기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-119">The default is `true`.</span></span>  <span data-ttu-id="95a6a-120">경우 설정 `false` 이 캐시 태그 도우미 렌더링된 된 출력에 캐싱 영향을 미치지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-120">If set to `false` this Cache Tag Helper will have no caching effect on the rendered output.</span></span>

<span data-ttu-id="95a6a-121">예제:</span><span class="sxs-lookup"><span data-stu-id="95a6a-121">Example:</span></span>

```cshtml
<cache enabled="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-on"></a><span data-ttu-id="95a6a-122">expires-on</span><span class="sxs-lookup"><span data-stu-id="95a6a-122">expires-on</span></span> 

| <span data-ttu-id="95a6a-123">특성 유형</span><span class="sxs-lookup"><span data-stu-id="95a6a-123">Attribute Type</span></span>    | <span data-ttu-id="95a6a-124">예제 값</span><span class="sxs-lookup"><span data-stu-id="95a6a-124">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="95a6a-125">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="95a6a-125">DateTimeOffset</span></span>    | <span data-ttu-id="95a6a-126">"@new DateTime(2025,1,29,17,02,0)"</span><span class="sxs-lookup"><span data-stu-id="95a6a-126">"@new DateTime(2025,1,29,17,02,0)"</span></span>    |


<span data-ttu-id="95a6a-127">절대 만료 날짜를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-127">Sets an absolute expiration date.</span></span> <span data-ttu-id="95a6a-128">다음 예제는 2025 년 1 월 29, 오후 5시 02분 될 때까지 캐시 태그 도우미의 콘텐츠를 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-128">The following example will cache the contents of the Cache Tag Helper until 5:02 PM on January 29, 2025.</span></span>

<span data-ttu-id="95a6a-129">예제:</span><span class="sxs-lookup"><span data-stu-id="95a6a-129">Example:</span></span>

```cshtml
<cache expires-on="@new DateTime(2025,1,29,17,02,0)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-after"></a><span data-ttu-id="95a6a-130">expires-after</span><span class="sxs-lookup"><span data-stu-id="95a6a-130">expires-after</span></span>

| <span data-ttu-id="95a6a-131">특성 유형</span><span class="sxs-lookup"><span data-stu-id="95a6a-131">Attribute Type</span></span>    | <span data-ttu-id="95a6a-132">예제 값</span><span class="sxs-lookup"><span data-stu-id="95a6a-132">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="95a6a-133">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="95a6a-133">TimeSpan</span></span>    | <span data-ttu-id="95a6a-134">"@TimeSpan.FromSeconds(120)"</span><span class="sxs-lookup"><span data-stu-id="95a6a-134">"@TimeSpan.FromSeconds(120)"</span></span>    |


<span data-ttu-id="95a6a-135">콘텐츠를 캐시할 첫 번째 요청 시간에서 시간을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-135">Sets the length of time from the first request time to cache the contents.</span></span> 

<span data-ttu-id="95a6a-136">예제:</span><span class="sxs-lookup"><span data-stu-id="95a6a-136">Example:</span></span>

```cshtml
<cache expires-after="@TimeSpan.FromSeconds(120)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-sliding"></a><span data-ttu-id="95a6a-137">expires-sliding</span><span class="sxs-lookup"><span data-stu-id="95a6a-137">expires-sliding</span></span>

| <span data-ttu-id="95a6a-138">특성 유형</span><span class="sxs-lookup"><span data-stu-id="95a6a-138">Attribute Type</span></span>    | <span data-ttu-id="95a6a-139">예제 값</span><span class="sxs-lookup"><span data-stu-id="95a6a-139">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="95a6a-140">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="95a6a-140">TimeSpan</span></span>    | <span data-ttu-id="95a6a-141">"@TimeSpan.FromSeconds(60)"</span><span class="sxs-lookup"><span data-stu-id="95a6a-141">"@TimeSpan.FromSeconds(60)"</span></span>     |


<span data-ttu-id="95a6a-142">액세스 하지 않은 경우 캐시 엔트리를 제거 해야 하는 시간을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-142">Sets the time that a cache entry should be evicted if it has not been accessed.</span></span>

<span data-ttu-id="95a6a-143">예제:</span><span class="sxs-lookup"><span data-stu-id="95a6a-143">Example:</span></span>

```cshtml
<cache expires-sliding="@TimeSpan.FromSeconds(60)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-header"></a><span data-ttu-id="95a6a-144">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="95a6a-144">vary-by-header</span></span>

| <span data-ttu-id="95a6a-145">특성 유형</span><span class="sxs-lookup"><span data-stu-id="95a6a-145">Attribute Type</span></span>    | <span data-ttu-id="95a6a-146">예제 값</span><span class="sxs-lookup"><span data-stu-id="95a6a-146">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="95a6a-147">문자열</span><span class="sxs-lookup"><span data-stu-id="95a6a-147">String</span></span>            | <span data-ttu-id="95a6a-148">"사용자-에이전트"</span><span class="sxs-lookup"><span data-stu-id="95a6a-148">"User-Agent"</span></span>                  |
|                   | <span data-ttu-id="95a6a-149">"User-Agent,content-encoding"</span><span class="sxs-lookup"><span data-stu-id="95a6a-149">"User-Agent,content-encoding"</span></span> |

<span data-ttu-id="95a6a-150">변경 될 때 캐시 새로 고침을 트리거하는 헤더 값의 쉼표로 구분 된 목록 또는 단일 헤더 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-150">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when they change.</span></span> <span data-ttu-id="95a6a-151">다음 예제에서는 헤더 값을 모니터링 `User-Agent`합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-151">The following example monitors the header value `User-Agent`.</span></span> <span data-ttu-id="95a6a-152">예제는에 대 한 콘텐츠를 캐시 하는 모든 다른 `User-Agent` 웹 서버에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-152">The example will cache the content for every different `User-Agent` presented to the web server.</span></span>

<span data-ttu-id="95a6a-153">예제:</span><span class="sxs-lookup"><span data-stu-id="95a6a-153">Example:</span></span>

```cshtml
<cache vary-by-header="User-Agent">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-query"></a><span data-ttu-id="95a6a-154">다 쿼리</span><span class="sxs-lookup"><span data-stu-id="95a6a-154">vary-by-query</span></span>

| <span data-ttu-id="95a6a-155">특성 유형</span><span class="sxs-lookup"><span data-stu-id="95a6a-155">Attribute Type</span></span>    | <span data-ttu-id="95a6a-156">예제 값</span><span class="sxs-lookup"><span data-stu-id="95a6a-156">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="95a6a-157">문자열</span><span class="sxs-lookup"><span data-stu-id="95a6a-157">String</span></span>            | <span data-ttu-id="95a6a-158">"Make"</span><span class="sxs-lookup"><span data-stu-id="95a6a-158">"Make"</span></span>                |
|                   | <span data-ttu-id="95a6a-159">"모델 만들기"</span><span class="sxs-lookup"><span data-stu-id="95a6a-159">"Make,Model"</span></span> |

<span data-ttu-id="95a6a-160">헤더 값이 변경 될 때 캐시 새로 고침을 트리거하는 헤더 값의 쉼표로 구분 된 목록 또는 단일 헤더 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-160">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header value changes.</span></span> <span data-ttu-id="95a6a-161">다음 예의 값을 검사 `Make` 및 `Model`합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-161">The following example looks at the values of `Make` and `Model`.</span></span>

<span data-ttu-id="95a6a-162">예제:</span><span class="sxs-lookup"><span data-stu-id="95a6a-162">Example:</span></span>

```cshtml
<cache vary-by-query="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-route"></a><span data-ttu-id="95a6a-163">vary-by-route</span><span class="sxs-lookup"><span data-stu-id="95a6a-163">vary-by-route</span></span>

| <span data-ttu-id="95a6a-164">특성 유형</span><span class="sxs-lookup"><span data-stu-id="95a6a-164">Attribute Type</span></span>    | <span data-ttu-id="95a6a-165">예제 값</span><span class="sxs-lookup"><span data-stu-id="95a6a-165">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="95a6a-166">문자열</span><span class="sxs-lookup"><span data-stu-id="95a6a-166">String</span></span>            | <span data-ttu-id="95a6a-167">"Make"</span><span class="sxs-lookup"><span data-stu-id="95a6a-167">"Make"</span></span>                |
|                   | <span data-ttu-id="95a6a-168">"모델 만들기"</span><span class="sxs-lookup"><span data-stu-id="95a6a-168">"Make,Model"</span></span> |

<span data-ttu-id="95a6a-169">경로 데이터 매개 변수 값 변경 하는 경우 캐시 새로 고침을 트리거하는 헤더 값의 쉼표로 구분 된 목록 또는 단일 헤더 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-169">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the route data parameter value(s) change.</span></span> <span data-ttu-id="95a6a-170">예제:</span><span class="sxs-lookup"><span data-stu-id="95a6a-170">Example:</span></span>

<span data-ttu-id="95a6a-171">*Startup.cs*</span><span class="sxs-lookup"><span data-stu-id="95a6a-171">*Startup.cs*</span></span> 

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{Make?}/{Model?}");
```
  
<span data-ttu-id="95a6a-172">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="95a6a-172">*Index.cshtml*</span></span>

```cshtml
<cache vary-by-route="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-cookie"></a><span data-ttu-id="95a6a-173">다 쿠키</span><span class="sxs-lookup"><span data-stu-id="95a6a-173">vary-by-cookie</span></span>

| <span data-ttu-id="95a6a-174">특성 유형</span><span class="sxs-lookup"><span data-stu-id="95a6a-174">Attribute Type</span></span>    | <span data-ttu-id="95a6a-175">예제 값</span><span class="sxs-lookup"><span data-stu-id="95a6a-175">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="95a6a-176">문자열</span><span class="sxs-lookup"><span data-stu-id="95a6a-176">String</span></span>            | <span data-ttu-id="95a6a-177">".AspNetCore.Identity.Application"</span><span class="sxs-lookup"><span data-stu-id="95a6a-177">".AspNetCore.Identity.Application"</span></span>                |
|                   | <span data-ttu-id="95a6a-178">".AspNetCore.Identity.Application,HairColor"</span><span class="sxs-lookup"><span data-stu-id="95a6a-178">".AspNetCore.Identity.Application,HairColor"</span></span> |

<span data-ttu-id="95a6a-179">헤더 값 (s) 변경 하는 경우 캐시 새로 고침을 트리거하는 헤더 값의 쉼표로 구분 된 목록 또는 단일 헤더 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-179">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header values(s) change.</span></span> <span data-ttu-id="95a6a-180">다음 예제에서는 ASP.NET Id와 연관 된 쿠키를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-180">The following example looks at the cookie associated with ASP.NET Identity.</span></span> <span data-ttu-id="95a6a-181">사용자가 인증 하는 경우 캐시 새로 고침을 트리거하는 요청 쿠키 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-181">When a user is authenticated the request cookie to be set which triggers a cache refresh.</span></span>

<span data-ttu-id="95a6a-182">예제:</span><span class="sxs-lookup"><span data-stu-id="95a6a-182">Example:</span></span>

```cshtml
<cache vary-by-cookie=".AspNetCore.Identity.Application">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-user"></a><span data-ttu-id="95a6a-183">사용자가 변경</span><span class="sxs-lookup"><span data-stu-id="95a6a-183">vary-by-user</span></span>

| <span data-ttu-id="95a6a-184">특성 유형</span><span class="sxs-lookup"><span data-stu-id="95a6a-184">Attribute Type</span></span>    | <span data-ttu-id="95a6a-185">예제 값</span><span class="sxs-lookup"><span data-stu-id="95a6a-185">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="95a6a-186">부울</span><span class="sxs-lookup"><span data-stu-id="95a6a-186">Boolean</span></span>             | <span data-ttu-id="95a6a-187">"true"</span><span class="sxs-lookup"><span data-stu-id="95a6a-187">"true"</span></span>                  |
|                     | <span data-ttu-id="95a6a-188">"false" (기본값)</span><span class="sxs-lookup"><span data-stu-id="95a6a-188">"false" (default)</span></span> |

<span data-ttu-id="95a6a-189">캐시에 로그인 한 사용자 (또는 컨텍스트 보안 주체)이 변경 될 때 다시 설정 해야 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-189">Specifies whether or not the cache should reset when the logged-in user (or Context Principal) changes.</span></span> <span data-ttu-id="95a6a-190">현재 사용자의 요청 컨텍스트 보안 주체 라고도 하 고 참조 하 여 Razor 보기에서 볼 수 있습니다 `@User.Identity.Name`합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-190">The current user is also known as the Request Context Principal and can be viewed in a Razor view by referencing `@User.Identity.Name`.</span></span>

<span data-ttu-id="95a6a-191">다음 예에서는 현재 로그인 한 사용자를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-191">The following example looks at the current logged in user.</span></span>  

<span data-ttu-id="95a6a-192">예제:</span><span class="sxs-lookup"><span data-stu-id="95a6a-192">Example:</span></span>

```cshtml
<cache vary-by-user="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

<span data-ttu-id="95a6a-193">이 특성을 사용 하 여 로그인 및 로그 아웃 주기를 통해 캐시에서 콘텐츠를 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-193">Using this attribute maintains the contents in cache through a log-in and log-out cycle.</span></span>  <span data-ttu-id="95a6a-194">사용 하는 경우 `vary-by-user="true"`, 로그인 및 로그 아웃 작업을 인증된 된 사용자에 대 한 캐시를 무효화 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-194">When using `vary-by-user="true"`, a log-in and log-out action invalidates the cache for the authenticated user.</span></span>  <span data-ttu-id="95a6a-195">로그인에 새 고유한 쿠키 값을 생성 하기 때문에 캐시를 무효화 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-195">The cache is invalidated because a new unique cookie value is generated on login.</span></span> <span data-ttu-id="95a6a-196">쿠키가 없는 없거나 만료 된 경우 익명 상태에 대 한 캐시 유지 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-196">Cache is maintained for the anonymous state when no cookie is present or has expired.</span></span> <span data-ttu-id="95a6a-197">즉, 사용자가 로그인 하는 경우 캐시는 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-197">This means if no user is logged in, the cache will be maintained.</span></span>

- - -

### <a name="vary-by"></a><span data-ttu-id="95a6a-198">변경</span><span class="sxs-lookup"><span data-stu-id="95a6a-198">vary-by</span></span>

| <span data-ttu-id="95a6a-199">특성 유형</span><span class="sxs-lookup"><span data-stu-id="95a6a-199">Attribute Type</span></span>    | <span data-ttu-id="95a6a-200">예제 값</span><span class="sxs-lookup"><span data-stu-id="95a6a-200">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="95a6a-201">문자열</span><span class="sxs-lookup"><span data-stu-id="95a6a-201">String</span></span>             | <span data-ttu-id="95a6a-202">"@Model"</span><span class="sxs-lookup"><span data-stu-id="95a6a-202">"@Model"</span></span>                 |


<span data-ttu-id="95a6a-203">데이터를 가져옵니다 캐시의 사용자 지정을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-203">Allows for customization of what data gets cached.</span></span> <span data-ttu-id="95a6a-204">특성의 문자열 값이 변경 되는 캐시 태그 도우미의 내용 참조 하는 개체를 업데이트 하는 경우</span><span class="sxs-lookup"><span data-stu-id="95a6a-204">When the object referenced by the attribute's string value changes, the content of the Cache Tag Helper is updated.</span></span> <span data-ttu-id="95a6a-205">종종 모델 값의 문자열 연결을이 특성에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-205">Often a string-concatenation of model values are assigned to this attribute.</span></span>  <span data-ttu-id="95a6a-206">실제로 캐시를 무효화 하는 연결 된 값 중 하나에 대 한 업데이트 것입니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-206">Effectively, that means an update to any of the concatenated values invalidates the cache.</span></span>

<span data-ttu-id="95a6a-207">다음 예에서는 두 개의 경로 매개 변수는 정수 값 보기 합계 렌더링 컨트롤러 메서드를 가정 `myParam1` 및 `myParam2`, 하는 단일 모델 속성을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-207">The following example assumes the controller method rendering the view sums the integer value of the two route parameters, `myParam1` and `myParam2`, and returns that as the single model property.</span></span> <span data-ttu-id="95a6a-208">이 Sum이 변경 될 때 캐시 태그 도우미의 내용은 렌더링 이며 다시 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-208">When this sum changes, the content of the Cache Tag Helper is rendered and cached again.</span></span>  

<span data-ttu-id="95a6a-209">예제:</span><span class="sxs-lookup"><span data-stu-id="95a6a-209">Example:</span></span>

<span data-ttu-id="95a6a-210">해결 방법:</span><span class="sxs-lookup"><span data-stu-id="95a6a-210">Action:</span></span>

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

<span data-ttu-id="95a6a-211">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="95a6a-211">*Index.cshtml*</span></span>

```cshtml
<cache vary-by="@Model"">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="priority"></a><span data-ttu-id="95a6a-212">priority</span><span class="sxs-lookup"><span data-stu-id="95a6a-212">priority</span></span>

| <span data-ttu-id="95a6a-213">특성 유형</span><span class="sxs-lookup"><span data-stu-id="95a6a-213">Attribute Type</span></span>    | <span data-ttu-id="95a6a-214">예제 값</span><span class="sxs-lookup"><span data-stu-id="95a6a-214">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="95a6a-215">CacheItemPriority</span><span class="sxs-lookup"><span data-stu-id="95a6a-215">CacheItemPriority</span></span>  | <span data-ttu-id="95a6a-216">"높음"</span><span class="sxs-lookup"><span data-stu-id="95a6a-216">"High"</span></span>                   |
|                    | <span data-ttu-id="95a6a-217">"낮음"</span><span class="sxs-lookup"><span data-stu-id="95a6a-217">"Low"</span></span> |
|                    | <span data-ttu-id="95a6a-218">"NeverRemove"</span><span class="sxs-lookup"><span data-stu-id="95a6a-218">"NeverRemove"</span></span> |
|                    | <span data-ttu-id="95a6a-219">"Normal"</span><span class="sxs-lookup"><span data-stu-id="95a6a-219">"Normal"</span></span> |

<span data-ttu-id="95a6a-220">기본 제공 캐시 공급자를 캐시 제거 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-220">Provides cache eviction guidance to the built-in cache provider.</span></span> <span data-ttu-id="95a6a-221">웹 서버를 제거 하 `Low` 메모리가 부족할 때 먼저 항목을 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-221">The web server will evict `Low` cache entries first when it's under memory pressure.</span></span>

<span data-ttu-id="95a6a-222">예제:</span><span class="sxs-lookup"><span data-stu-id="95a6a-222">Example:</span></span>

```cshtml
<cache priority="High">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

<span data-ttu-id="95a6a-223">`priority` 특성 특정 수준의 캐시 보존을 보장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-223">The `priority` attribute does not guarantee a specific level of cache retention.</span></span> <span data-ttu-id="95a6a-224">`CacheItemPriority`뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-224">`CacheItemPriority` is only a suggestion.</span></span> <span data-ttu-id="95a6a-225">이 특성을 설정 `NeverRemove` 캐시는 항상 유지 되어야 하는 것을 보장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-225">Setting this attribute to `NeverRemove` does not guarantee that the cache will always be retained.</span></span> <span data-ttu-id="95a6a-226">참조 [추가 리소스](#additional-resources) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-226">See [Additional Resources](#additional-resources) for more information.</span></span>

<span data-ttu-id="95a6a-227">캐시 태그 도우미에 따라 달라 집니다.는 [메모리 캐시 서비스](xref:performance/caching/memory)합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-227">The Cache Tag Helper is dependent on the [memory cache service](xref:performance/caching/memory).</span></span> <span data-ttu-id="95a6a-228">캐시 태그 도우미 추가 되지 않은 경우 서비스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="95a6a-228">The Cache Tag Helper adds the service if it has not been added.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="95a6a-229">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="95a6a-229">Additional resources</span></span>

* <xref:performance/caching/memory>
* <xref:security/authentication/identity>
