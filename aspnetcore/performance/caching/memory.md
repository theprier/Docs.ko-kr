---
title: ASP.NET Core의 메모리 내 캐시
author: rick-anderson
description: ASP.NET Core에서 데이터를 메모리에 캐시하는 방법을 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 12/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: performance/caching/memory
ms.openlocfilehash: a1ceb6c577c634aae7ee9c327e8e5b33e973912d
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="cache-in-memory-in-aspnet-core"></a><span data-ttu-id="1cf31-103">ASP.NET Core의 메모리 내 캐시</span><span class="sxs-lookup"><span data-stu-id="1cf31-103">Cache in-memory in ASP.NET Core</span></span>

<span data-ttu-id="1cf31-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [John Luo](https://github.com/JunTaoLuo) 및 [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="1cf31-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [John Luo](https://github.com/JunTaoLuo), and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="1cf31-105">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/memory/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="1cf31-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/memory/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="caching-basics"></a><span data-ttu-id="1cf31-106">캐싱 기본 사항</span><span class="sxs-lookup"><span data-stu-id="1cf31-106">Caching basics</span></span>

<span data-ttu-id="1cf31-107">캐싱은 콘텐츠를 생성하기 위해 필요한 작업을 줄임으로써 응용 프로그램의 성능 및 확장성을 크게 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-107">Caching can significantly improve the performance and scalability of an app by reducing the work required to generate content.</span></span> <span data-ttu-id="1cf31-108">캐싱은 자주 변경되지 않는 데이터에 가장 효과가 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-108">Caching works best with data that changes infrequently.</span></span> <span data-ttu-id="1cf31-109">캐싱은 원본에서 가져와서 반환하는 것보다 더 빠르게 반환할 수 있는 데이터의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-109">Caching makes a copy of data that can be returned much faster than from the original source.</span></span> <span data-ttu-id="1cf31-110">응용 프로그램이 캐시된 데이터에 의존하지 않도록 만들어야 하고 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-110">You should write and test your app to never depend on cached data.</span></span>

<span data-ttu-id="1cf31-111">ASP.NET Core는 몇 가지 다른 종류의 캐시를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-111">ASP.NET Core supports several different caches.</span></span> <span data-ttu-id="1cf31-112">가장 간단한 캐시는 웹 서버의 메모리에 저장된 캐시를 나타내는 [IMemoryCache](/dotnet/api/microsoft.extensions.caching.memory.imemorycache)를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-112">The simplest cache is based on the [IMemoryCache](/dotnet/api/microsoft.extensions.caching.memory.imemorycache), which represents a cache stored in the memory of the web server.</span></span> <span data-ttu-id="1cf31-113">다수의 서버로 구성된 서버 팜에서 실행되는 응용 프로그램이 메모리 내 캐시를 사용할 경우에는 세션이 고정적인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-113">Apps which run on a server farm of multiple servers should ensure that sessions are sticky when using the in-memory cache.</span></span> <span data-ttu-id="1cf31-114">고정 세션은 클라이언트의 이어지는 후속 요청이 모두 동일한 서버로 전달되도록 보장해줍니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-114">Sticky sessions ensure that subsequent requests from a client all go to the same server.</span></span> <span data-ttu-id="1cf31-115">예를 들어 Azure 웹 앱은 이어지는 모든 후속 요청을 동일한 서버로 라우트하기 위해서 [응용 프로그램 요청 라우팅](https://www.iis.net/learn/extensions/planning-for-arr)(ARR)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-115">For example, Azure Web apps use [Application Request Routing](https://www.iis.net/learn/extensions/planning-for-arr) (ARR) to route all subsequent requests to the same server.</span></span>

<span data-ttu-id="1cf31-116">웹 팜에서 비-고정 세션을 사용할 경우에는 캐시 일관성 문제가 발생하지 않도록 [분산 캐시](distributed.md)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-116">Non-sticky sessions in a web farm require a [distributed cache](distributed.md) to avoid cache consistency problems.</span></span> <span data-ttu-id="1cf31-117">일부 응용 프로그램의 경우, 분산 캐시가 메모리 내 캐시보다 더 높은 규모 확장을 지원할 수 있습니다. </span><span class="sxs-lookup"><span data-stu-id="1cf31-117">For some apps, a distributed cache can support higher scale out than an in-memory cache.</span></span> <span data-ttu-id="1cf31-118">분산 캐시를 사용하면 캐시 메모리를 외부 프로세스에서 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-118">Using a distributed cache offloads the cache memory to an external process.</span></span> 

<span data-ttu-id="1cf31-119">`IMemoryCache` 캐시는 [캐시 우선 순위](/dotnet/api/microsoft.extensions.caching.memory.cacheitempriority)가 `CacheItemPriority.NeverRemove`로 설정되지 않은 캐시 항목을 메모리 부하에 따라 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-119">The `IMemoryCache` cache will evict cache entries under memory pressure unless the [cache priority](/dotnet/api/microsoft.extensions.caching.memory.cacheitempriority) is set to `CacheItemPriority.NeverRemove`.</span></span> <span data-ttu-id="1cf31-120">`CacheItemPriority`를 설정하면 메모리에 부하가 걸렸을 때 캐시가 항목을 제거하는 우선 순위를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-120">You can set the `CacheItemPriority` to adjust the priority with which the cache evicts items under memory pressure.</span></span>

<span data-ttu-id="1cf31-121">메모리 내 캐시는 모든 개체를 저장할 수 있는 반면, 분산 캐시 인터페이스는 `byte[]`만 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-121">The in-memory cache can store any object; the distributed cache interface is limited to `byte[]`.</span></span>

## <a name="using-imemorycache"></a><span data-ttu-id="1cf31-122">IMemoryCache 사용하기</span><span class="sxs-lookup"><span data-stu-id="1cf31-122">Using IMemoryCache</span></span>

<span data-ttu-id="1cf31-123">메모리 내 캐시는 응용 프로그램에서 [종속성 주입](../../fundamentals/dependency-injection.md)을 통해서 참조되는 *서비스*입니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-123">In-memory caching is a *service* that's referenced from your app using [Dependency Injection](../../fundamentals/dependency-injection.md).</span></span> <span data-ttu-id="1cf31-124">`ConfigureServices`에서 `AddMemoryCache`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-124">Call `AddMemoryCache` in `ConfigureServices`:</span></span>

[!code-csharp[](memory/sample/WebCache/Startup.cs?highlight=8)] 

<span data-ttu-id="1cf31-125">그런 다음 생성자에서 `IMemoryCache`의 인스턴스를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-125">Request the `IMemoryCache` instance in the constructor:</span></span>

[!code-csharp[](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_ctor&highlight=3,5-999)] 

<span data-ttu-id="1cf31-126">`IMemoryCache`를 사용하려면 "Microsoft.Extensions.Caching.Memory" NuGet 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-126">`IMemoryCache` requires NuGet package "Microsoft.Extensions.Caching.Memory".</span></span>

<span data-ttu-id="1cf31-127">다음 코드는 [TryGetValue](/dotnet/api/microsoft.extensions.caching.memory.imemorycache.trygetvalue?view=aspnetcore-2.0#Microsoft_Extensions_Caching_Memory_IMemoryCache_TryGetValue_System_Object_System_Object__)를 이용해서 시간이 캐시되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-127">The following code uses [TryGetValue](/dotnet/api/microsoft.extensions.caching.memory.imemorycache.trygetvalue?view=aspnetcore-2.0#Microsoft_Extensions_Caching_Memory_IMemoryCache_TryGetValue_System_Object_System_Object__) to check if a time is in the cache.</span></span> <span data-ttu-id="1cf31-128">만약 시간이 캐시되어 있지 않다면 새로운 항목이 생성되고 [Set](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions.set?view=aspnetcore-2.0#Microsoft_Extensions_Caching_Memory_CacheExtensions_Set__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object___0_Microsoft_Extensions_Caching_Memory_MemoryCacheEntryOptions_)을 통해서 캐시에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-128">If a time isn't cached, a new entry is created and added to the cache with [Set](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions.set?view=aspnetcore-2.0#Microsoft_Extensions_Caching_Memory_CacheExtensions_Set__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object___0_Microsoft_Extensions_Caching_Memory_MemoryCacheEntryOptions_).</span></span>

[!code-csharp[](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet1)]

<span data-ttu-id="1cf31-129">현재 시간과 캐시된 시간이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-129">The current time and the cached time are displayed:</span></span>

[!code-cshtml[](memory/sample/WebCache/Views/Home/Cache.cshtml)]

<span data-ttu-id="1cf31-130">제한 시간 안에 요청이 전달되는 동안에는 (그리고 메모리 부족으로 제거되지 않은 경우에는) 캐시된 `DateTime` 값이 캐시에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-130">The cached `DateTime` value remains in the cache while there are requests within the timeout period (and no eviction due to memory pressure).</span></span> <span data-ttu-id="1cf31-131">다음 그림은 현재 시간과 캐시에서 조회한 그보다 오래된 시간을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-131">The following image shows the current time and an older time retrieved from the cache:</span></span>

![두 개의 서로 다른 시간을 표시하는 Index 뷰](memory/_static/time.png)

<span data-ttu-id="1cf31-133">다음 코드는 [GetOrCreate](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreate__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry___0__) 및 [GetOrCreateAsync](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreateAsync__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry_System_Threading_Tasks_Task___0___) 를 이용해서 데이터를 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-133">The following code uses [GetOrCreate](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreate__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry___0__) and [GetOrCreateAsync](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreateAsync__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry_System_Threading_Tasks_Task___0___) to cache data.</span></span> 

[!code-csharp[](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet2&highlight=3-7,14-19)]

<span data-ttu-id="1cf31-134">다음 코드는 [Get](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_Get__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_) 을 호출해서 캐시된 시간을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-134">The following code calls [Get](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_Get__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_) to fetch the cached time:</span></span>

[!code-csharp[](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_gct)]

<span data-ttu-id="1cf31-135">캐시 메서드에 대한 설명은 [IMemoryCache 메서드](/dotnet/api/microsoft.extensions.caching.memory.imemorycache) 및 [CacheExtensions 메서드](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-135">See [IMemoryCache methods](/dotnet/api/microsoft.extensions.caching.memory.imemorycache) and [CacheExtensions methods](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions) for a description of the cache methods.</span></span>

## <a name="using-memorycacheentryoptions"></a><span data-ttu-id="1cf31-136">MemoryCacheEntryOptions 사용하기</span><span class="sxs-lookup"><span data-stu-id="1cf31-136">Using MemoryCacheEntryOptions</span></span>

<span data-ttu-id="1cf31-137">다음 예제에서는:</span><span class="sxs-lookup"><span data-stu-id="1cf31-137">The following sample:</span></span>

- <span data-ttu-id="1cf31-138">절대 만료 시간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-138">Sets the absolute expiration time.</span></span> <span data-ttu-id="1cf31-139">절대 만료 시간은 항목이 캐시될 수 있는 최대 시간으로, 슬라이딩 만료가 지속적으로 갱신될 경우 항목이 이전 상태로 지속되는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-139">This is the maximum time the entry can be cached and prevents the item from becoming too stale when the sliding expiration is continuously renewed.</span></span>
- <span data-ttu-id="1cf31-140">슬라이딩 만료 시간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-140">Sets a sliding expiration time.</span></span> <span data-ttu-id="1cf31-141">상대 만료 시계는 캐시된 항목에 접근하는 요청에 따라 재설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-141">Requests that access this cached item will reset the sliding expiration clock.</span></span>
- <span data-ttu-id="1cf31-142">캐시 우선 순위를 `CacheItemPriority.NeverRemove`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-142">Sets the cache priority to `CacheItemPriority.NeverRemove`.</span></span> 
- <span data-ttu-id="1cf31-143">캐시에서 항목이 제거된 후에 호출되는 [PostEvictionDelegate](/dotnet/api/microsoft.extensions.caching.memory.postevictiondelegate) 를 설정합니다. 콜백은 캐시에서 항목을 제거하는 코드와 다른 스레드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-143">Sets a [PostEvictionDelegate](/dotnet/api/microsoft.extensions.caching.memory.postevictiondelegate) that will be called after the entry is evicted from the cache.</span></span> <span data-ttu-id="1cf31-144">콜백 캐시에서 항목을 제거 하는 코드에서 다른 스레드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-144">The callback is run on a different thread from the code that removes the item from the cache.</span></span>

[!code-csharp[](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_et&highlight=14-20)]

## <a name="cache-dependencies"></a><span data-ttu-id="1cf31-145">캐시 종속성</span><span class="sxs-lookup"><span data-stu-id="1cf31-145">Cache dependencies</span></span>

<span data-ttu-id="1cf31-146">다음 예제는 종속적인 항목을 만료할 경우 캐시 항목을 만료하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-146">The following sample shows how to expire a cache entry if a dependent entry expires.</span></span> <span data-ttu-id="1cf31-147">캐시된 항목에 `CancellationChangeToken`이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-147">A `CancellationChangeToken` is added to the cached item.</span></span> <span data-ttu-id="1cf31-148">`CancellationTokenSource`의 `Cancel`이 호출되면 캐시된 두 항목 모두 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-148">When `Cancel` is called on the `CancellationTokenSource`, both cache entries are evicted.</span></span> 

[!code-csharp[](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_ed)]

<span data-ttu-id="1cf31-149">`CancellationTokenSource`를 사용하면 다수의 캐시 항목을 그룹으로 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-149">Using a `CancellationTokenSource` allows multiple cache entries to be evicted as a group.</span></span> <span data-ttu-id="1cf31-150">위의 코드의 `using` 패턴을 사용하면,`using` 블록 안에서 생성된 캐시 항목들이 트리거 및 만료 설정을 상속받습니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-150">With the `using` pattern in the code above, cache entries created inside the `using` block will inherit triggers and expiration settings.</span></span>

## <a name="additional-notes"></a><span data-ttu-id="1cf31-151">추가 참고 사항</span><span class="sxs-lookup"><span data-stu-id="1cf31-151">Additional notes</span></span>

- <span data-ttu-id="1cf31-152">캐시 항목을 다시 채우기 위해서 콜백을 사용할 때:</span><span class="sxs-lookup"><span data-stu-id="1cf31-152">When using a callback to repopulate a cache item:</span></span>

  - <span data-ttu-id="1cf31-153">다수의 요청이 캐시된 키 값으로 빈 값을 얻을 수도 있는데, 이는 콜백이 완료되지 않았기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-153">Multiple requests can find the cached key value empty because the callback hasn't completed.</span></span> 
  - <span data-ttu-id="1cf31-154">이로 인해 다수의 스레드가 캐시된 항목을 다시 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-154">This can result in several threads repopulating the cached item.</span></span>

- <span data-ttu-id="1cf31-155">한 캐시 항목을 사용해서 다른 캐시 항목을 만들 때, 하위 항목은 부모 항목의 만료 토큰 및 시간 기반의 만료 설정을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-155">When one cache entry is used to create another, the child copies the parent entry's expiration tokens and time-based expiration settings.</span></span> <span data-ttu-id="1cf31-156">하위 항목은 부모 항목을 수동으로 제거하거나 갱신하더라도 만료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1cf31-156">The child isn't expired by manual removal or updating of the parent entry.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1cf31-157">추가 자료</span><span class="sxs-lookup"><span data-stu-id="1cf31-157">Additional resources</span></span>

* [<span data-ttu-id="1cf31-158">분산 캐시 사용하기</span><span class="sxs-lookup"><span data-stu-id="1cf31-158">Work with a distributed cache</span></span>](xref:performance/caching/distributed)
* [<span data-ttu-id="1cf31-159">변경 토큰을 이용해서 변경 감지하기</span><span class="sxs-lookup"><span data-stu-id="1cf31-159">Detect changes with change tokens</span></span>](xref:fundamentals/primitives/change-tokens)
* [<span data-ttu-id="1cf31-160">응답 캐싱</span><span class="sxs-lookup"><span data-stu-id="1cf31-160">Response caching</span></span>](xref:performance/caching/response)
* [<span data-ttu-id="1cf31-161">응답 캐싱 미들웨어</span><span class="sxs-lookup"><span data-stu-id="1cf31-161">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
* [<span data-ttu-id="1cf31-162">캐시 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="1cf31-162">Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [<span data-ttu-id="1cf31-163">분산 캐시 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="1cf31-163">Distributed Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
