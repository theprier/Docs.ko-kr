---
title: >
  ASP.NET Core에서 분산 캐시 사용하기
author: ardalis
description: 특히 클라우드나 서버 팜 환경에서 ASP.NET Core의 분산 캐시를 사용하여 응용 프로그램의 성능 및 확장성을 개선하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 02/14/2017
uid: performance/caching/distributed
ms.openlocfilehash: 85da734f3ae7bcf0936888edfb6ac91d4362eef2
ms.sourcegitcommit: f5d403004f3550e8c46585fdbb16c49e75f495f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2018
ms.locfileid: "49477478"
---
# <a name="work-with-a-distributed-cache-in-aspnet-core"></a><span data-ttu-id="9e0f9-103">ASP.NET Core에서 분산 캐시 사용하기
</span><span class="sxs-lookup"><span data-stu-id="9e0f9-103">Work with a distributed cache in ASP.NET Core</span></span>

<span data-ttu-id="9e0f9-104">작성자: [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="9e0f9-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="9e0f9-105">분산 된 캐시는 클라우드 또는 서버 팜을 호스트 하는 경우에 특히 성능 및 ASP.NET Core 앱의 확장성을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-105">Distributed caches can improve the performance and scalability of ASP.NET Core apps, especially when hosted in the cloud or a server farm.</span></span>

<span data-ttu-id="9e0f9-106">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="9e0f9-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="what-is-a-distributed-cache"></a><span data-ttu-id="9e0f9-107">분산 캐시란</span><span class="sxs-lookup"><span data-stu-id="9e0f9-107">What is a distributed cache</span></span>

<span data-ttu-id="9e0f9-108">분산 캐시는 여러 응용 프로그램 서버에서 공유됩니다([캐시 기본 사항](memory.md#caching-basics) 참조).</span><span class="sxs-lookup"><span data-stu-id="9e0f9-108">A distributed cache is shared by multiple app servers (see [Cache Basics](memory.md#caching-basics)).</span></span> <span data-ttu-id="9e0f9-109">캐시에 저장된 정보는 개별 웹 서버의 메모리에 저장되지 않으며, 캐시된 데이터는 모든 응용 프로그램의 서버에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-109">The information in the cache isn't stored in the memory of individual web servers, and the cached data is available to all of the app's servers.</span></span> <span data-ttu-id="9e0f9-110">이는 몇 가지 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-110">This provides several advantages:</span></span>

1. <span data-ttu-id="9e0f9-111">캐시된 데이터가 모든 웹 서버에서 일관적입니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-111">Cached data is coherent on all web servers.</span></span> <span data-ttu-id="9e0f9-112">어떤 서버가 사용자의 요청을 처리하는지에 따라 다른 결과를 표시하거나 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-112">Users don't see different results depending on which web server handles their request</span></span>

2. <span data-ttu-id="9e0f9-113">캐시된 데이터는 웹 서버가 재시작되거나 배포된 후에도 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-113">Cached data survives web server restarts and deployments.</span></span> <span data-ttu-id="9e0f9-114">캐시에 영향을 주지 않고 개별 웹 서버를 제거하거나 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-114">Individual web servers can be removed or added without impacting the cache.</span></span>

3. <span data-ttu-id="9e0f9-115">원본 데이터 저장소에 대한 요청 회수가 줄어듭니다(다수의 메모리 내 캐시를 사용하거나 캐시를 전혀 사용하지 않는 경우 보다).</span><span class="sxs-lookup"><span data-stu-id="9e0f9-115">The source data store has fewer requests made to it (than with multiple in-memory caches or no cache at all).</span></span>

> [!NOTE]
> <span data-ttu-id="9e0f9-116">SQL Server 분산 캐시를 사용하는 경우 이런 장점 중 일부는 응용 프로그램의 원본 데이터와 다른 캐시 전용 데이터베이스 인스턴스를 사용하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-116">If using a SQL Server Distributed Cache, some of these advantages are only true if a separate database instance is used for the cache than for the app's source data.</span></span>

<span data-ttu-id="9e0f9-117">다른 모든 캐시와 마찬가지로, 대부분 관계형 데이터베이스(또는 웹 서비스)에서 조회하는 것보다 캐시에서 데이터를 훨씬 빠르게 조회할 수 있기 때문에 분산 캐시도 응용 프로그램의 응답성을 획기적으로 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-117">Like any cache, a distributed cache can dramatically improve an app's responsiveness, since typically data can be retrieved from the cache much faster than from a relational database (or web service).</span></span>

<span data-ttu-id="9e0f9-118">캐시 구성은 구현에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-118">Cache configuration is implementation specific.</span></span> <span data-ttu-id="9e0f9-119">이 문서에서는 Redis 및 SQL Server 분산 캐시를 구성하는 두 가지 방법을 모두 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-119">This article describes how to configure both Redis and SQL Server distributed caches.</span></span> <span data-ttu-id="9e0f9-120">어떤 구현을 선택하던지 응용 프로그램은 공통 `IDistributedCache` 인터페이스를 사용해서 캐시와 상호 작용합니다.
</span><span class="sxs-lookup"><span data-stu-id="9e0f9-120">Regardless of which implementation is selected, the app interacts with the cache using a common `IDistributedCache` interface.</span></span>

## <a name="the-idistributedcache-interface"></a><span data-ttu-id="9e0f9-121">IDistributedCache 인터페이스</span><span class="sxs-lookup"><span data-stu-id="9e0f9-121">The IDistributedCache Interface</span></span>

<span data-ttu-id="9e0f9-122">`IDistributedCache` 인터페이스는 동기 및 비동기 메서드를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-122">The `IDistributedCache` interface includes synchronous and asynchronous methods.</span></span> <span data-ttu-id="9e0f9-123">이 인터페이스를 사용하면 분산 캐시 구현에 항목을 추가하고, 검색하고, 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-123">The interface allows items to be added, retrieved, and removed from the distributed cache implementation.</span></span> <span data-ttu-id="9e0f9-124">`IDistributedCache` 인터페이스는 다음과 같은 메서드를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-124">The `IDistributedCache` interface includes the following methods:</span></span>

<span data-ttu-id="9e0f9-125">**Get, GetAsync**</span><span class="sxs-lookup"><span data-stu-id="9e0f9-125">**Get, GetAsync**</span></span>

<span data-ttu-id="9e0f9-126">문자열 키를 전달받아서 캐시에 항목이 존재할 경우 `byte[]`로 캐시 항목을 조회합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-126">Takes a string key and retrieves a cached item as a `byte[]` if found in the cache.</span></span>

<span data-ttu-id="9e0f9-127">**Set, SetAsync**</span><span class="sxs-lookup"><span data-stu-id="9e0f9-127">**Set, SetAsync**</span></span>

<span data-ttu-id="9e0f9-128">문자열 키를 사용해서 (`byte[]`로) 캐시에 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-128">Adds an item (as `byte[]`) to the cache using a string key.</span></span>

<span data-ttu-id="9e0f9-129">**RefreshAsync 새로 고침**</span><span class="sxs-lookup"><span data-stu-id="9e0f9-129">**Refresh, RefreshAsync**</span></span>

<span data-ttu-id="9e0f9-130">키를 기반으로 캐시 항목을 새로 고치고, 캐시 항목의 슬라이딩 만료 시간 제한을 재설정합니다(필요한 경우).</span><span class="sxs-lookup"><span data-stu-id="9e0f9-130">Refreshes an item in the cache based on its key, resetting its sliding expiration timeout (if any).</span></span>

<span data-ttu-id="9e0f9-131">**를 제거합니다 하 고 비동기적으로 제거**</span><span class="sxs-lookup"><span data-stu-id="9e0f9-131">**Remove, RemoveAsync**</span></span>

<span data-ttu-id="9e0f9-132">키를 기반으로 캐시 항목을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-132">Removes a cache entry based on its key.</span></span>

<span data-ttu-id="9e0f9-133">`IDistributedCache` 인터페이스를 사용하려면:</span><span class="sxs-lookup"><span data-stu-id="9e0f9-133">To use the `IDistributedCache` interface:</span></span>

   1. <span data-ttu-id="9e0f9-134">프로젝트 파일에 필요한 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-134">Add the required NuGet packages to your project file.</span></span>

   2. <span data-ttu-id="9e0f9-135">`IDistributedCache` 클래스의 `Startup` 메서드에서 `ConfigureServices`의 특정 구현을 구성하고 컨테이너에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-135">Configure the specific implementation of `IDistributedCache` in your `Startup` class's `ConfigureServices` method, and add it to the container there.</span></span>

   3. <span data-ttu-id="9e0f9-136">응용 프로그램의 [미들웨어](xref:fundamentals/middleware/index)나 MVC 컨트롤러 클래스의 생성자에서 `IDistributedCache`의 인스턴스를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-136">From the app's [Middleware](xref:fundamentals/middleware/index) or MVC controller classes, request an instance of `IDistributedCache` from the constructor.</span></span> <span data-ttu-id="9e0f9-137">인스턴스에 의해 제공 됩니다 [종속성 주입](../../fundamentals/dependency-injection.md) (DI).</span><span class="sxs-lookup"><span data-stu-id="9e0f9-137">The instance will be provided by [Dependency Injection](../../fundamentals/dependency-injection.md) (DI).</span></span>

> [!NOTE]
> <span data-ttu-id="9e0f9-138">`IDistributedCache` 인스턴스를 Singleton이나 Scoped 수명으로 사용할 필요는 없습니다(적어도 기본 구현일 경우).</span><span class="sxs-lookup"><span data-stu-id="9e0f9-138">There's no need to use a Singleton or Scoped lifetime for `IDistributedCache` instances (at least for the built-in implementations).</span></span> <span data-ttu-id="9e0f9-139">필요할 때마다 인스턴스를 생성할 수도 있지만([종속성 주입](../../fundamentals/dependency-injection.md)을 사용하는 대신), 그럴 경우 코드를 테스트하기가 어려워지고 [명시적 종속성 원칙](http://deviq.com/explicit-dependencies-principle/)을 위반하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-139">You can also create an instance wherever you might need one (instead of using [Dependency Injection](../../fundamentals/dependency-injection.md)), but this can make your code harder to test, and violates the [Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/).</span></span>

<span data-ttu-id="9e0f9-140">다음 예제는 간단한 미들웨어 구성 요소에서 `IDistributedCache`의 인스턴스를 사용하는 방법을 보여줍니다:</span><span class="sxs-lookup"><span data-stu-id="9e0f9-140">The following example shows how to use an instance of `IDistributedCache` in a simple middleware component:</span></span>

[!code-csharp[](distributed/sample/src/DistCacheSample/StartTimeHeader.cs)]

<span data-ttu-id="9e0f9-141">위의 코드는 캐시된 값을 읽기만 하고 작성하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-141">In the code above, the cached value is read, but never written.</span></span> <span data-ttu-id="9e0f9-142">이 예제에서 값은 오직 서버가 시작될 때만 설정하고 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-142">In this sample, the value is only set when a server starts up, and doesn't change.</span></span> <span data-ttu-id="9e0f9-143">다중 서버 시나리오에서는 가장 최근에 시작된 서버가 다른 서버에 의해 설정된 기존의 모든 값을 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-143">In a multi-server scenario, the most recent server to start will overwrite any previous values that were set by other servers.</span></span> <span data-ttu-id="9e0f9-144">그리고 `Get` 및 `Set` 메서드는 `byte[]` 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-144">The `Get` and `Set` methods use the `byte[]` type.</span></span> <span data-ttu-id="9e0f9-145">따라서 문자열 값은 `Encoding.UTF8.GetString`(`Get`을 사용할 때) 또는 `Encoding.UTF8.GetBytes`(`Set`을 사용할 때)를 사용해서 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-145">Therefore, the string value must be converted using `Encoding.UTF8.GetString` (for `Get`) and `Encoding.UTF8.GetBytes` (for `Set`).</span></span>

<span data-ttu-id="9e0f9-146">다음 코드는 *Startup.cs*에서 값이 설정되고 있는 부분을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-146">The following code from *Startup.cs* shows the value being set:</span></span>

[!code-csharp[](distributed/sample/src/DistCacheSample/Startup.cs?name=snippet1)]

<span data-ttu-id="9e0f9-147">`IDistributedCache` 메서드에서 `ConfigureServices`가 구성되고 나면 이를 `Configure` 메서드의 매개 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-147">Since `IDistributedCache` is configured in the `ConfigureServices` method, it's available to the `Configure` method as a parameter.</span></span> <span data-ttu-id="9e0f9-148">매개 변수로 추가 하면 DI를 통해 제공 인스턴스를 구성된 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-148">Adding it as a parameter will allow the configured instance to be provided through DI.</span></span>

## <a name="using-a-redis-distributed-cache"></a><span data-ttu-id="9e0f9-149">Redis 분산 캐시 사용하기</span><span class="sxs-lookup"><span data-stu-id="9e0f9-149">Using a Redis distributed cache</span></span>

<span data-ttu-id="9e0f9-150">[Redis](https://redis.io/)는 분산 캐시로 흔히 사용되는 오픈 소스 메모리 내 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-150">[Redis](https://redis.io/) is an open source in-memory data store, which is often used as a distributed cache.</span></span> <span data-ttu-id="9e0f9-151">로컬에서 사용할 수도 있고 Azure에서 호스팅되는 응용 프로그램에 대한 [Azure Redis Cache](https://azure.microsoft.com/services/cache/)를 구성할 수도 있습니다. </span><span class="sxs-lookup"><span data-stu-id="9e0f9-151">You can use it locally, and you can configure an [Azure Redis Cache](https://azure.microsoft.com/services/cache/) for your Azure-hosted ASP.NET Core apps.</span></span> <span data-ttu-id="9e0f9-152">ASP.NET Core 응용 프로그램은 `RedisDistributedCache`의 인스턴스를 사용해서 캐시 구현을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-152">Your ASP.NET Core app configures the cache implementation using a `RedisDistributedCache` instance.</span></span>

<span data-ttu-id="9e0f9-153">Redis cache 필요 [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis/)</span><span class="sxs-lookup"><span data-stu-id="9e0f9-153">The Redis cache requires [Microsoft.Extensions.Caching.Redis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Redis/)</span></span>

<span data-ttu-id="9e0f9-154">`ConfigureServices`에서 Redis 구현을 구성한 다음 응용 프로그램 코드에서 `IDistributedCache`의 인스턴스를 요청하여 이에 접근합니다(위의 코드 참조).</span><span class="sxs-lookup"><span data-stu-id="9e0f9-154">You configure the Redis implementation in `ConfigureServices` and access it in your app code by requesting an instance of `IDistributedCache` (see the code above).</span></span>

<span data-ttu-id="9e0f9-155">예제 코드에서는 서버가 `Staging` 환경으로 구성될 때 `RedisCache` 구현이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-155">In the sample code, a `RedisCache` implementation is used when the server is configured for a `Staging` environment.</span></span> <span data-ttu-id="9e0f9-156">따라서 `ConfigureStagingServices` 메서드에서 `RedisCache`를 구성합니다:</span><span class="sxs-lookup"><span data-stu-id="9e0f9-156">Thus the `ConfigureStagingServices` method configures the `RedisCache`:</span></span>

[!code-csharp[](distributed/sample/src/DistCacheSample/Startup.cs?name=snippet2)]

<span data-ttu-id="9e0f9-157">Redis를 로컬 컴퓨터에 설치 하려면 chocolatey 패키지 설치 [ https://chocolatey.org/packages/redis-64/ ](https://chocolatey.org/packages/redis-64/) 실행 `redis-server` 명령 프롬프트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-157">To install Redis on your local machine, install the chocolatey package [https://chocolatey.org/packages/redis-64/](https://chocolatey.org/packages/redis-64/) and run `redis-server` from a command prompt.</span></span>

## <a name="using-a-sql-server-distributed-cache"></a><span data-ttu-id="9e0f9-158">SQL Server 분산 캐시 사용하기
</span><span class="sxs-lookup"><span data-stu-id="9e0f9-158">Using a SQL Server distributed cache</span></span>

<span data-ttu-id="9e0f9-159">SqlServerCache 구현을 사용하면 SQL Server 데이터베이스를 백업 저장소로 이용해서 분산 캐시를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-159">The SqlServerCache implementation allows the distributed cache to use a SQL Server database as its backing store.</span></span> <span data-ttu-id="9e0f9-160">지정한 이름 및 스키마로 테이블을 생성하는 도구인 sql-cache 도구를 이용해서 SQL Server 테이블을 생성할 수 있습니다.
</span><span class="sxs-lookup"><span data-stu-id="9e0f9-160">To create SQL Server table you can use sql-cache tool, the tool creates a table with the name and schema you specify.</span></span>

::: moniker range="< aspnetcore-2.1"

<span data-ttu-id="9e0f9-161">추가 `SqlConfig.Tools` 에 `<ItemGroup>` 프로젝트 파일과 실행 요소의 `dotnet restore`합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-161">Add `SqlConfig.Tools` to the `<ItemGroup>` element of the project file and run `dotnet restore`.</span></span>

```xml
<ItemGroup>
  <DotNetCliToolReference Include="Microsoft.Extensions.Caching.SqlConfig.Tools" 
                          Version="2.0.2" />
</ItemGroup>
```

::: moniker-end

<span data-ttu-id="9e0f9-162">다음 명령을 실행 하 여 SqlConfig.Tools를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-162">Test SqlConfig.Tools by running the following command:</span></span>

```console
dotnet sql-cache create --help
```

<span data-ttu-id="9e0f9-163">SqlConfig.Tools는 사용량, 옵션 및 명령 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-163">SqlConfig.Tools displays usage, options, and command help.</span></span>

<span data-ttu-id="9e0f9-164">SQL Server에서 실행 하 여 테이블을 만들기는 `sql-cache create` 명령:</span><span class="sxs-lookup"><span data-stu-id="9e0f9-164">Create a table in SQL Server by running the `sql-cache create` command :</span></span>

```console
dotnet sql-cache create "Data Source=(localdb)\v11.0;Initial Catalog=DistCache;Integrated Security=True;" dbo TestCache
info: Microsoft.Extensions.Caching.SqlConfig.Tools.Program[0]
Table and index were created successfully.
```

<span data-ttu-id="9e0f9-165">생성된 테이블은 다음과 같은 스키마를 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-165">The created table has the following schema:</span></span>

![Sql Server 캐시 테이블](distributed/_static/SqlServerCacheTable.png)

<span data-ttu-id="9e0f9-167">다른 모든 캐시 구현과 마찬가지로, 응용 프로그램은 `SqlServerCache`가 아니라 `IDistributedCache`의 인스턴스를 사용해서 캐시 값을 읽고 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-167">Like all cache implementations, your app should get and set cache values using an instance of `IDistributedCache`, not a `SqlServerCache`.</span></span> <span data-ttu-id="9e0f9-168">이 샘플에서는 구현 `SqlServerCache` 프로덕션 환경에서 (에 구성 되어 있으므로 `ConfigureProductionServices`).</span><span class="sxs-lookup"><span data-stu-id="9e0f9-168">The sample implements `SqlServerCache` in the Production environment (so it's configured in `ConfigureProductionServices`).</span></span>

[!code-csharp[](distributed/sample/src/DistCacheSample/Startup.cs?name=snippet3)]

> [!NOTE]
> <span data-ttu-id="9e0f9-169">일반적으로 `ConnectionString`은 (그리고 필요한 경우 `SchemaName` 및 `TableName`은) 자격 증명이 포함되어 있을 수도 있기 때문에 소스 제어 외부에 (UserSecrets 같은) 저장되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-169">The `ConnectionString` (and optionally, `SchemaName` and `TableName`) should typically be stored outside of source control (such as UserSecrets), as they may contain credentials.</span></span>

## <a name="recommendations"></a><span data-ttu-id="9e0f9-170">권장 사항</span><span class="sxs-lookup"><span data-stu-id="9e0f9-170">Recommendations</span></span>

<span data-ttu-id="9e0f9-171">응용 프로그램에 적합한 `IDistributedCache`의 구현을 결정할 때는 기존 인프라와 환경, 성능 요구 사항 및 팀의 경험을 감안하여 Redis와 SQL Server 중 하나를 선택해야 합니다. </span><span class="sxs-lookup"><span data-stu-id="9e0f9-171">When deciding which implementation of `IDistributedCache` is right for your app, choose between Redis and SQL Server based on your existing infrastructure and environment, your performance requirements, and your team's experience.</span></span> <span data-ttu-id="9e0f9-172">Redis로 작업하는 것이 더 편안한 팀이라면 탁월한 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-172">If your team is more comfortable working with Redis, it's an excellent choice.</span></span> <span data-ttu-id="9e0f9-173">팀이 SQL Server를 선호한다면 해당 구현에도 확신을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-173">If your team prefers SQL Server, you can be confident in that implementation as well.</span></span> <span data-ttu-id="9e0f9-174">기존의 캐싱 솔루션은 데이터를 메모리 내에 저장하기 때문에 데이터를 빠르게 조회할 수 있다는 점에 주의하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-174">Note that a traditional caching solution stores data in-memory which allows for fast retrieval of data.</span></span> <span data-ttu-id="9e0f9-175">공통적으로 사용되는 데이터는 캐시에 저장하고 전체 데이터를 SQL Server 또는 Azure Storage 같은 백엔드 영구 저장소에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-175">You should store commonly used data in a cache and store the entire data in a backend persistent store such as SQL Server or Azure Storage.</span></span> <span data-ttu-id="9e0f9-176">Redis 캐시는 SQL 캐시와 비교하여 높은 처리량과 낮은 대기 시간을 제공하는 캐싱 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="9e0f9-176">Redis Cache is a caching solution which gives you high throughput and low latency as compared to SQL Cache.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9e0f9-177">추가 자료</span><span class="sxs-lookup"><span data-stu-id="9e0f9-177">Additional resources</span></span>

* [<span data-ttu-id="9e0f9-178">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="9e0f9-178">Redis Cache on Azure</span></span>](https://azure.microsoft.com/documentation/services/redis-cache/)
* [<span data-ttu-id="9e0f9-179">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="9e0f9-179">SQL Database on Azure</span></span>](https://azure.microsoft.com/documentation/services/sql-database/)
* <xref:performance/caching/memory>
* <xref:fundamentals/change-tokens>
* <xref:performance/caching/response>
* <xref:performance/caching/middleware>
* <xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper>
* <xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper>
* <xref:host-and-deploy/web-farm>
