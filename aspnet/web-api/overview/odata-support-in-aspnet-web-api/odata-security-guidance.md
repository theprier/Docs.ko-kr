---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: ASP.NET Web API 2에 대 한 보안 지침 OData | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 02/06/2013
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 2a5b776a81cb3e3cf809dd3c4229448988086a32
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828354"
---
<a name="security-guidance-for-aspnet-web-api-2-odata"></a><span data-ttu-id="010fe-102">ASP.NET Web API 2에 대 한 보안 지침 OData</span><span class="sxs-lookup"><span data-stu-id="010fe-102">Security Guidance for ASP.NET Web API 2 OData</span></span>
====================
<span data-ttu-id="010fe-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="010fe-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="010fe-104">이 항목에서는 OData 통해 데이터 집합을 노출 하는 경우 고려해 야 하는 보안 문제 중 일부를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-104">This topic describes some of the security issues that you should consider when exposing a dataset through OData.</span></span>

## <a name="edm-security"></a><span data-ttu-id="010fe-105">EDM 보안</span><span class="sxs-lookup"><span data-stu-id="010fe-105">EDM Security</span></span>

<span data-ttu-id="010fe-106">쿼리 의미 체계 엔터티 데이터 모델 (EDM)에서 기본 모델 형식 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-106">The query semantics are based on the entity data model (EDM), not the underlying model types.</span></span> <span data-ttu-id="010fe-107">EDM에서 속성을 제외할 수 있습니다 및 쿼리에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-107">You can exclude a property from the EDM and it will not be visible to the query.</span></span> <span data-ttu-id="010fe-108">예를 들어 모델에는 급여 속성을 포함 하는 직원 형식 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-108">For example, suppose your model includes an Employee type with a Salary property.</span></span> <span data-ttu-id="010fe-109">클라이언트에서 숨기려면 EDM에서이 속성을 제외 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-109">You might want to exclude this property from the EDM to hide it from clients.</span></span>

<span data-ttu-id="010fe-110">두 가지는 제외를 EDM 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-110">There are two ways to exlude a property from the EDM.</span></span> <span data-ttu-id="010fe-111">설정할 수 있습니다 합니다 **[IgnoreDataMember]** 모델 클래스의 속성을 특성:</span><span class="sxs-lookup"><span data-stu-id="010fe-111">You can set the **[IgnoreDataMember]** attribute on the property in the model class:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

<span data-ttu-id="010fe-112">프로그래밍 방식으로 EDM에서 속성을 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-112">You can also remove the property from the EDM programmatically:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a><span data-ttu-id="010fe-113">쿼리 보안</span><span class="sxs-lookup"><span data-stu-id="010fe-113">Query Security</span></span>

<span data-ttu-id="010fe-114">악성 또는 네이티브 클라이언트를 실행 하는 매우 긴 시간이 소요 되는 쿼리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-114">A malicious or naive client may be able to construct a query that takes a very long time to execute.</span></span> <span data-ttu-id="010fe-115">최악의 경우에서이 서비스에 대 한 액세스를 방해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-115">In the worst case this can disrupt access to your service.</span></span>

<span data-ttu-id="010fe-116">합니다 **[Queryable]** 가 구문 분석, 유효성을 검사, 쿼리를 적용 하는 작업 필터 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-116">The **[Queryable]** attribute is an action filter that parses, validates, and applies the query.</span></span> <span data-ttu-id="010fe-117">필터는 LINQ 식에 쿼리 옵션을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-117">The filter converts the query options into a LINQ expression.</span></span> <span data-ttu-id="010fe-118">OData 컨트롤러를 반환 하는 경우는 **IQueryable** 형식에는 **IQueryable** LINQ 공급자는 LINQ 식 쿼리로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-118">When the OData controller returns an **IQueryable** type, the **IQueryable** LINQ provider converts the LINQ expression into a query.</span></span> <span data-ttu-id="010fe-119">따라서 성능에 사용 되는 LINQ 공급자 및 데이터 집합 또는 데이터베이스 스키마의 특정 특성에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-119">Therefore, performance depends on the LINQ provider that is used, and also on the particular characteristics of your dataset or database schema.</span></span>

<span data-ttu-id="010fe-120">ASP.NET Web API에서 OData 쿼리 옵션을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [OData 쿼리 옵션 지원](supporting-odata-query-options.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-120">For more information about using OData query options in ASP.NET Web API, see [Supporting OData Query Options](supporting-odata-query-options.md).</span></span>

<span data-ttu-id="010fe-121">않을 (예를 들어, 엔터프라이즈 환경)에서 모든 클라이언트는 신뢰할 수 있는지 알고 있는 경우 또는 데이터 집합이 작은 경우 쿼리 성능 문제를 하지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-121">If you know that all clients are trusted (for example, in an enterprise environment), or if your dataset is small, query performance might not be an issue.</span></span> <span data-ttu-id="010fe-122">그렇지 않은 경우 다음 권장 사항을 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-122">Otherwise, you should consider the following recommendations.</span></span>

- <span data-ttu-id="010fe-123">다양 한 쿼리를 사용 하 여 서비스를 테스트 하 고 DB를 프로 파일링 합니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-123">Test your service with various queries and profile the DB.</span></span>
- <span data-ttu-id="010fe-124">한 쿼리에서 큰 데이터 집합을 반환 하지 않으려면 서버 기반 페이징이 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-124">Enable server-driven paging, to avoid returning a large data set in one query.</span></span> <span data-ttu-id="010fe-125">자세한 내용은 [Server-Driven 페이징](supporting-odata-query-options.md#server-paging)합니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-125">For more information, see [Server-Driven Paging](supporting-odata-query-options.md#server-paging).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- <span data-ttu-id="010fe-126">$Filter 및 $orderby 필요 한가요?</span><span class="sxs-lookup"><span data-stu-id="010fe-126">Do you need $filter and $orderby?</span></span> <span data-ttu-id="010fe-127">일부 응용 프로그램 페이징 $top $skip을 사용 하 여, 클라이언트 허용 되었지만 다른 쿼리 옵션을 사용 하지 않도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-127">Some applications might allow client paging, using $top and $skip, but disable the other query options.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- <span data-ttu-id="010fe-128">클러스터형된 인덱스의 속성에 $orderby를 제한 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-128">Consider restricting $orderby to properties in a clustered index.</span></span> <span data-ttu-id="010fe-129">클러스터형된 인덱스가 없는 큰 데이터를 정렬 하는 속도가 느립니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-129">Sorting large data without a clustered index is slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- <span data-ttu-id="010fe-130">최대 노드 수: 합니다 **MaxNodeCount** 속성을 **[Queryable]** $filter 구문 트리에서 허용 된 최대 노드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-130">Maximum node count: The **MaxNodeCount** property on **[Queryable]** sets the maximum number nodes allowed in the $filter syntax tree.</span></span> <span data-ttu-id="010fe-131">기본값은 100으로 하지만 많은 수의 노드는 컴파일 느린 수 있기 때문에 더 낮은 값을 설정 하려면 가리키려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-131">The default value is 100, but you may want to set a lower value, because a large number of nodes can be slow to compile.</span></span> <span data-ttu-id="010fe-132">LINQ to Objects (즉, 중간 LINQ 공급자를 사용 하지 않고 메모리에서 컬렉션에 대 한 LINQ 쿼리)를 사용 하는 경우 특히 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-132">This is particularly true if you are using LINQ to Objects (i.e., LINQ queries on a collection in memory, without the use of an intermediate LINQ provider).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- <span data-ttu-id="010fe-133">속도가 느려질 수 있습니다 이러한 any () 및 all ()과 함수를 사용 하지 않도록 설정 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-133">Consider disabling the any() and all() functions, as these can be slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- <span data-ttu-id="010fe-134">큰 문자열 및 #8212for 예제, 제품 설명 또는 블로그 항목 및 문자열 함수를 사용 하지 않도록 설정 하는 #8212consider 모든 문자열 속성에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-134">If any string properties contain large strings&#8212for example, a product description or a blog entry&#8212consider disabling the string functions.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- <span data-ttu-id="010fe-135">탐색 속성에 대해 필터링을 허용 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-135">Consider disallowing filtering on navigation properties.</span></span> <span data-ttu-id="010fe-136">데이터베이스 스키마에 따라 저하 될 수 있는 조인에서는 탐색 속성에 대해 필터링 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-136">Filtering on navigation properties can result in a join, which might be slow, depending on your database schema.</span></span> <span data-ttu-id="010fe-137">다음 코드에서는 탐색 속성에 대해 필터링을 방지 하는 쿼리 검사기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-137">The following code shows a query validator that prevents filtering on navigation properties.</span></span> <span data-ttu-id="010fe-138">쿼리 유효성 검사기에 대 한 자세한 내용은 참조 하세요. [쿼리 유효성 검사](supporting-odata-query-options.md#query-validation)합니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-138">For more information about query validators, see [Query Validation](supporting-odata-query-options.md#query-validation).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- <span data-ttu-id="010fe-139">데이터베이스에 대 한 사용자 지정 된 유효성 검사기를 작성 하 여 $filter 쿼리를 제한 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-139">Consider restricting $filter queries by writing a validator that is customized for your database.</span></span> <span data-ttu-id="010fe-140">예를 들어,이 두 가지 쿼리를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-140">For example, consider these two queries:</span></span> 

  - <span data-ttu-id="010fe-141">마지막으로 이름이 'A'로 시작 하는 행위자를 사용 하 여 모든 동영상입니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-141">All movies with actors whose last name starts with ‘A'.</span></span>
  - <span data-ttu-id="010fe-142">1994 년에 릴리스된 모든 동영상입니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-142">All movies released in 1994.</span></span>

    <span data-ttu-id="010fe-143">행위자가 영화는 인덱싱되지 않는 한 첫 번째 쿼리는 동영상의 전체 목록을 검색 하려면 DB 엔진이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-143">Unless movies are indexed by actors, the first query might require the DB engine to scan the entire list of movies.</span></span> <span data-ttu-id="010fe-144">두 번째 쿼리는 허용 될 수 있습니다, 있지만 릴리스 연도별 되었다고 가정 하 고 영화가 인덱싱됩니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-144">Whereas the second query might be acceptable, assuming movies are indexed by release year.</span></span>

    <span data-ttu-id="010fe-145">다음 코드에 있지만 "ReleaseYear" 및 "Title" 속성을 필터링 할 수 있습니다 하는 유효성 검사기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-145">The following code shows a validator that allows filtering on the "ReleaseYear" and "Title" properties but no other properties.</span></span>

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- <span data-ttu-id="010fe-146">일반적으로 필요한 $filter 함수를 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-146">In general, consider which $filter functions you need.</span></span> <span data-ttu-id="010fe-147">클라이언트의 $filter의 전체 표현이 필요 하지 않은 경우에 허용 된 함수를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="010fe-147">If your clients do not need the full expressiveness of $filter, you can limit the allowed functions.</span></span>
