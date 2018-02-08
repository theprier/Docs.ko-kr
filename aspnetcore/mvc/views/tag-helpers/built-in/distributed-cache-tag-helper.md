---
title: "ASP.NET Core의 분산 캐시 태그 도우미"
author: pkellner
description: "캐시 태그 도우미 사용 방법 소개"
manager: wpickett
ms.author: riande
ms.date: 02/14/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper
ms.openlocfilehash: 710477732b865e2e3821102d34545bbd4e0a5919
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="distributed-cache-tag-helper"></a><span data-ttu-id="eccca-103">분산 캐시 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="eccca-103">Distributed Cache Tag Helper</span></span>

<span data-ttu-id="eccca-104">작성자: [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="eccca-104">By [Peter Kellner](http://peterkellner.net)</span></span> 


<span data-ttu-id="eccca-105">분산 캐시 태그 도우미는 콘텐츠를 분산 캐시 원본에 캐싱하여 ASP.NET Core 앱 성능을 획기적으로 개선하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eccca-105">The Distributed Cache Tag Helper provides the ability to dramatically improve the performance of your ASP.NET Core app by caching its content to a distributed cache source.</span></span>

<span data-ttu-id="eccca-106">분산 캐시 태그 도우미는 캐시 태그 도우미와 동일한 기본 클래스에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="eccca-106">The Distributed Cache Tag Helper inherits from the same base class as the Cache Tag Helper.</span></span>  <span data-ttu-id="eccca-107">캐시 태그 도우미와 연결된 모든 특성은 분산 태그 도우미에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="eccca-107">All attributes associated with the Cache Tag Helper will also work on the Distributed Tag Helper.</span></span>


<span data-ttu-id="eccca-108">분산 캐시 태그 도우미는 **생성자 주입**이라고도 하는 **명시적 종속성 원칙**을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="eccca-108">The Distributed Cache Tag Helper follows the **Explicit Dependencies Principle** known as **Constructor Injection**.</span></span>  <span data-ttu-id="eccca-109">특히 `IDistributedCache` 인터페이스 컨테이너는 분산 캐시 태그 도우미의 생성자에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="eccca-109">Specifically, the `IDistributedCache` interface container is passed into the Distributed Cache Tag Helper's constructor.</span></span>  <span data-ttu-id="eccca-110">`IDistributedCache`의 구체적인 구현이 `ConfigureServices`에 생성되지 않은 경우(주로 startup.cs에서 발견됨) 분산 캐시 태그 도우미는 동일한 메모리 내 공급자를 사용하여 캐시된 데이터를 기본 캐시 태그 도우미로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="eccca-110">If no specific concrete implementation of `IDistributedCache` has been created in `ConfigureServices`, usually found in startup.cs, then the Distributed Cache Tag Helper will use the same in-memory provider for storing cached data as the basic Cache Tag Helper.</span></span>

## <a name="distributed-cache-tag-helper-attributes"></a><span data-ttu-id="eccca-111">분산 캐시 태그 도우미 특성</span><span class="sxs-lookup"><span data-stu-id="eccca-111">Distributed Cache Tag Helper Attributes</span></span>

- - -

### <a name="enabled-expires-on-expires-after-expires-sliding-vary-by-header-vary-by-query-vary-by-route-vary-by-cookie-vary-by-user-vary-by-priority"></a><span data-ttu-id="eccca-112">설정된 expires-on expires-after expires-sliding vary-by-header vary-by-query vary-by-route vary-by-cookie vary-by-user vary-by priority</span><span class="sxs-lookup"><span data-stu-id="eccca-112">enabled expires-on expires-after expires-sliding vary-by-header vary-by-query vary-by-route vary-by-cookie vary-by-user vary-by priority</span></span>

<span data-ttu-id="eccca-113">정의는 캐시 태그 도우미를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eccca-113">See Cache Tag Helper for definitions.</span></span> <span data-ttu-id="eccca-114">분산 캐시 태그 도우미는 캐시 태그 도우미와 동일한 클래스에서 상속하므로 이 모든 특성이 캐시 태그 도우미에서 공통입니다.</span><span class="sxs-lookup"><span data-stu-id="eccca-114">Distributed Cache Tag Helper inherits from the same class as Cache Tag Helper so all these attributes are common from Cache Tag Helper.</span></span>

- - -

### <a name="name-required"></a><span data-ttu-id="eccca-115">이름(필수)</span><span class="sxs-lookup"><span data-stu-id="eccca-115">name (required)</span></span>

| <span data-ttu-id="eccca-116">특성 유형</span><span class="sxs-lookup"><span data-stu-id="eccca-116">Attribute Type</span></span>    | <span data-ttu-id="eccca-117">예제 값</span><span class="sxs-lookup"><span data-stu-id="eccca-117">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="eccca-118">string</span><span class="sxs-lookup"><span data-stu-id="eccca-118">string</span></span>    | <span data-ttu-id="eccca-119">"my-distributed-cache-unique-key-101"</span><span class="sxs-lookup"><span data-stu-id="eccca-119">"my-distributed-cache-unique-key-101"</span></span>     |

<span data-ttu-id="eccca-120">필수 `name` 특성은 분산 캐시 태그 도우미의 각 인스턴스에 대해 저장된 캐시의 키로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eccca-120">The required `name` attribute is used as a key to that cache stored for each instance of a Distributed Cache Tag Helper.</span></span>  <span data-ttu-id="eccca-121">razor 페이지의 Razor 페이지 이름 및 태그 도우미 위치를 기준으로 각 캐시 태그 도우미 인스턴스에 키를 할당하는 기본 캐시 태그 도우미와는 달리, 분산 캐시 태그 도우미는 `name` 특성의 키만을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="eccca-121">Unlike the basic Cache Tag Helper that assigns a key to each Cache Tag Helper instance based on the Razor page name and location of the tag helper in the razor page, the Distributed Cache Tag Helper only bases it's key on the attribute `name`</span></span>

<span data-ttu-id="eccca-122">사용 예제:</span><span class="sxs-lookup"><span data-stu-id="eccca-122">Usage Example:</span></span>

```cshtml
<distributed-cache name="my-distributed-cache-unique-key-101">
    Time Inside Cache Tag Helper: @DateTime.Now
</distributed-cache>
```

## <a name="distributed-cache-tag-helper-idistributedcache-implementations"></a><span data-ttu-id="eccca-123">분산 캐시 태그 도우미 IDistributedCache 구현</span><span class="sxs-lookup"><span data-stu-id="eccca-123">Distributed Cache Tag Helper IDistributedCache Implementations</span></span>

<span data-ttu-id="eccca-124">ASP.NET Core에 두 가지 `IDistributedCache` 구현이 기본적으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="eccca-124">There are two implementations of `IDistributedCache` built in to ASP.NET Core.</span></span>  <span data-ttu-id="eccca-125">하나는 **Sql Server** 기반이고 다른 하나는 **Redis** 기반입니다.</span><span class="sxs-lookup"><span data-stu-id="eccca-125">One is based on **Sql Server** and the other is based on **Redis**.</span></span> <span data-ttu-id="eccca-126">이러한 구현의 세부 정보는 아래에서 참조하는 "분산 캐시 작업"이라는 리소스에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eccca-126">Details of these implementations can be found at the resource referenced below named "Working with a distributed cache".</span></span> <span data-ttu-id="eccca-127">두 구현 모두 ASP.NET Core의 **startup.cs**에서 `IDistributedCache` 인스턴스를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eccca-127">Both implementations involve setting an instance of `IDistributedCache` in ASP.NET Core's **startup.cs**.</span></span>

<span data-ttu-id="eccca-128">특정 `IDistributedCache` 구현 사용과 특별히 관련된 태그 특성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eccca-128">There are no tag attributes specifically associated with using any specific implementation of `IDistributedCache`.</span></span>



- - -



## <a name="additional-resources"></a><span data-ttu-id="eccca-129">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="eccca-129">Additional resources</span></span>

* <xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper>
* <xref:fundamentals/dependency-injection#service-lifetimes-and-registration-options>
* <xref:performance/caching/distributed>
* <xref:performance/caching/memory>
* <xref:security/authentication/identity>
