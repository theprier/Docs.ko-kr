---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: ASP.NET Web API 2 OData 쿼리 옵션 지원 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/04/2013
ms.topic: article
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 3ce2b38a13e8684a88bb0ce6183671fae98795c7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37380845"
---
<a name="supporting-odata-query-options-in-aspnet-web-api-2"></a><span data-ttu-id="73a9d-102">ASP.NET Web API 2에서에서 OData 쿼리 옵션 지원</span><span class="sxs-lookup"><span data-stu-id="73a9d-102">Supporting OData Query Options in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="73a9d-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="73a9d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="73a9d-104">OData는 OData 쿼리를 수정 하는 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-104">OData defines parameters that can be used to modify an OData query.</span></span> <span data-ttu-id="73a9d-105">클라이언트는 요청 URI의 쿼리 문자열에서 이러한 매개 변수를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-105">The client sends these parameters in the query string of the request URI.</span></span> <span data-ttu-id="73a9d-106">예를 들어, 클라이언트가 결과 정렬 하려면 $orderby 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-106">For example, to sort the results, a client uses the $orderby parameter:</span></span>

`http://localhost/Products?$orderby=Name`

<span data-ttu-id="73a9d-107">이러한 매개 변수를 호출 하는 OData 사양 *쿼리 옵션*합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-107">The OData specification calls these parameters *query options*.</span></span> <span data-ttu-id="73a9d-108">프로젝트에서 모든 Web API 컨트롤러에 대 한 OData 쿼리 옵션을 설정할 수 있습니다. &#8212; 컨트롤러는 OData 끝점일 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-108">You can enable OData query options for any Web API controller in your project &#8212; the controller does not need to be an OData endpoint.</span></span> <span data-ttu-id="73a9d-109">이 모든 Web API 응용 프로그램에 필터링 및 정렬을 등 기능을 추가 하는 편리한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-109">This gives you a convenient way to add features such as filtering and sorting to any Web API application.</span></span>

<span data-ttu-id="73a9d-110">항목을 쿼리 옵션을 사용 하도록 설정 하기 전에 [OData 보안 지침](odata-security-guidance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-110">Before enabling query options, please read the topic [OData Security Guidance](odata-security-guidance.md).</span></span>

- [<span data-ttu-id="73a9d-111">OData 쿼리 옵션을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="73a9d-111">Enabling OData Query Options</span></span>](#enable)
- [<span data-ttu-id="73a9d-112">예제 쿼리</span><span class="sxs-lookup"><span data-stu-id="73a9d-112">Example Queries</span></span>](#examples)
- [<span data-ttu-id="73a9d-113">서버 기반 페이징</span><span class="sxs-lookup"><span data-stu-id="73a9d-113">Server-Driven Paging</span></span>](#server-paging)
- [<span data-ttu-id="73a9d-114">쿼리 옵션을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-114">Limiting the Query Options</span></span>](#limiting_query_options)
- [<span data-ttu-id="73a9d-115">쿼리 옵션을 직접 호출</span><span class="sxs-lookup"><span data-stu-id="73a9d-115">Invoking Query Options Directly</span></span>](#ODataQueryOptions)
- [<span data-ttu-id="73a9d-116">쿼리 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="73a9d-116">Query Validation</span></span>](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a><span data-ttu-id="73a9d-117">OData 쿼리 옵션을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="73a9d-117">Enabling OData Query Options</span></span>

<span data-ttu-id="73a9d-118">웹 API는 OData 쿼리 옵션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-118">Web API supports the following OData query options:</span></span>

| <span data-ttu-id="73a9d-119">옵션</span><span class="sxs-lookup"><span data-stu-id="73a9d-119">Option</span></span> | <span data-ttu-id="73a9d-120">설명</span><span class="sxs-lookup"><span data-stu-id="73a9d-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="73a9d-121">$expand</span><span class="sxs-lookup"><span data-stu-id="73a9d-121">$expand</span></span> | <span data-ttu-id="73a9d-122">관련된 엔터티 인라인을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-122">Expands related entities inline.</span></span> |
| <span data-ttu-id="73a9d-123">$filter</span><span class="sxs-lookup"><span data-stu-id="73a9d-123">$filter</span></span> | <span data-ttu-id="73a9d-124">부울 조건에 따라 결과 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-124">Filters the results, based on a Boolean condition.</span></span> |
| <span data-ttu-id="73a9d-125">$inlinecount</span><span class="sxs-lookup"><span data-stu-id="73a9d-125">$inlinecount</span></span> | <span data-ttu-id="73a9d-126">응답에 일치 하는 항목의 총 수를 포함 하도록 서버를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-126">Tells the server to include the total count of matching entities in the response.</span></span> <span data-ttu-id="73a9d-127">(서버 쪽 페이징에 유용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="73a9d-127">(Useful for server-side paging.)</span></span> |
| <span data-ttu-id="73a9d-128">$orderby</span><span class="sxs-lookup"><span data-stu-id="73a9d-128">$orderby</span></span> | <span data-ttu-id="73a9d-129">결과 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-129">Sorts the results.</span></span> |
| <span data-ttu-id="73a9d-130">$select</span><span class="sxs-lookup"><span data-stu-id="73a9d-130">$select</span></span> | <span data-ttu-id="73a9d-131">응답에 포함할 속성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-131">Selects which properties to include in the response.</span></span> |
| <span data-ttu-id="73a9d-132">$skip</span><span class="sxs-lookup"><span data-stu-id="73a9d-132">$skip</span></span> | <span data-ttu-id="73a9d-133">처음 n 개 결과 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-133">Skips the first n results.</span></span> |
| <span data-ttu-id="73a9d-134">$top</span><span class="sxs-lookup"><span data-stu-id="73a9d-134">$top</span></span> | <span data-ttu-id="73a9d-135">첫 번째 n만 결과 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-135">Returns only the first n the results.</span></span> |

<span data-ttu-id="73a9d-136">OData 쿼리 옵션을 사용 하려면 활성화 해야 합니다을 명시적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-136">To use OData query options, you must enable them explicitly.</span></span> <span data-ttu-id="73a9d-137">전체 응용 프로그램에 대 한 전역적으로 있도록 수도 있고 특정 컨트롤러 또는 특정 작업에 대해 사용 하도록 설정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-137">You can enable them globally for the entire application, or enable them for specific controllers or specific actions.</span></span>

<span data-ttu-id="73a9d-138">OData 쿼리 옵션을 전체적으로 설정 하려면 호출 **EnableQuerySupport** 에 **HttpConfiguration** 시작 시 클래스:</span><span class="sxs-lookup"><span data-stu-id="73a9d-138">To enable OData query options globally, call **EnableQuerySupport** on the **HttpConfiguration** class at startup:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

<span data-ttu-id="73a9d-139">**EnableQuerySupport** 메서드를 사용 하면 반환 하는 모든 컨트롤러 작업에 대 한 전역적으로 쿼리 옵션을 **IQueryable** 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-139">The **EnableQuerySupport** method enables query options globally for any controller action that returns an **IQueryable** type.</span></span> <span data-ttu-id="73a9d-140">전체 응용 프로그램에 대해 사용 하도록 설정 하는 쿼리 옵션을 사용 하지 않으려는 경우 하도록 할 수 있습니다 특정 컨트롤러 작업에 대 한 추가 하 여 합니다 **[Queryable]** 작업 메서드에 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-140">If you don't want query options enabled for the entire application, you can enable them for specific controller actions by adding the **[Queryable]** attribute to the action method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a><span data-ttu-id="73a9d-141">예제 쿼리</span><span class="sxs-lookup"><span data-stu-id="73a9d-141">Example Queries</span></span>

<span data-ttu-id="73a9d-142">이 섹션에서는 OData 쿼리 옵션을 사용 하 여 가능한 쿼리 유형을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-142">This section shows the types of queries that are possible using the OData query options.</span></span> <span data-ttu-id="73a9d-143">쿼리 옵션에 대 한 특정 내용은 OData 설명서에서 참조 [www.odata.org](http://www.odata.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-143">For specific details about the query options, refer to the OData documentation at [www.odata.org](http://www.odata.org/).</span></span>

<span data-ttu-id="73a9d-144">$에 대 한 정보에 대 한 확장 및 $select을 참조 하세요 [$expand $select 사용 및 ASP.NET Web API OData의 $value](using-select-expand-and-value.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-144">For information about $expand and $select, see [Using $select, $expand, and $value in ASP.NET Web API OData](using-select-expand-and-value.md).</span></span>

<span data-ttu-id="73a9d-145">**클라이언트 기반 페이징**</span><span class="sxs-lookup"><span data-stu-id="73a9d-145">**Client-Driven Paging**</span></span>

<span data-ttu-id="73a9d-146">큰 엔터티 집합에 대 한 클라이언트 결과의 수를 제한 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-146">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="73a9d-147">예를 들어, 클라이언트는 결과의 다음 페이지를 가져오는 "다음" 링크를 사용 하 여 한 번에 10 개 항목을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-147">For example, a client might show 10 entries at a time, with "next" links to get the next page of results.</span></span> <span data-ttu-id="73a9d-148">이렇게 하려면 클라이언트 $top 및 $skip 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-148">To do this, the client uses the $top and $skip options.</span></span>

`http://localhost/Products?$top=10&$skip=20`

<span data-ttu-id="73a9d-149">$Top 옵션 반환할 항목의 최대 수를 제공 하 고 $skip 옵션을 건너뛸 항목 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-149">The $top option gives the maximum number of entries to return, and the $skip option gives the number of entries to skip.</span></span> <span data-ttu-id="73a9d-150">앞의 예제 항목 21-30 인출합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-150">The previous example fetches entries 21 through 30.</span></span>

<span data-ttu-id="73a9d-151">**필터링**</span><span class="sxs-lookup"><span data-stu-id="73a9d-151">**Filtering**</span></span>

<span data-ttu-id="73a9d-152">$Filter 옵션에는 부울 식을 적용 하 여 결과 필터링 하는 클라이언트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-152">The $filter option lets a client filter the results by applying a Boolean expression.</span></span> <span data-ttu-id="73a9d-153">필터 식이 모두 매우 강력 합니다. 논리 및 산술 연산자, 문자열 함수 및 날짜 함수의 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-153">The filter expressions are quite powerful; they include logical and arithmetic operators, string functions, and date functions.</span></span>

| <span data-ttu-id="73a9d-154">"Toys" 같은 범주를 사용 하 여 모든 제품을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-154">Return all products with category equal to "Toys".</span></span> | <span data-ttu-id="73a9d-155">`http://localhost/Products?$filter=Category` eq 'Toys'</span><span class="sxs-lookup"><span data-stu-id="73a9d-155">`http://localhost/Products?$filter=Category` eq 'Toys'</span></span> |
| --- | --- |
| <span data-ttu-id="73a9d-156">10 보다 낮은 가격으로 모든 제품을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-156">Return all products with price less than 10.</span></span> | <span data-ttu-id="73a9d-157">`http://localhost/Products?$filter=Price` lt 10</span><span class="sxs-lookup"><span data-stu-id="73a9d-157">`http://localhost/Products?$filter=Price` lt 10</span></span> |
| <span data-ttu-id="73a9d-158">논리 연산자: 모든 제품을 반환할 위치 가격 > = 5이 고 가격 < = 15입니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-158">Logical operators: Return all products where price >= 5 and price <= 15.</span></span> | <span data-ttu-id="73a9d-159">`http://localhost/Products?$filter=Price` ge 5와 보다 적거나 같은 가격 15</span><span class="sxs-lookup"><span data-stu-id="73a9d-159">`http://localhost/Products?$filter=Price` ge 5 and Price le 15</span></span> |
| <span data-ttu-id="73a9d-160">문자열 함수: 이름에 "zz"를 사용 하 여 모든 제품을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-160">String functions: Return all products with "zz" in the name.</span></span> | `http://localhost/Products?$filter=substringof('zz',Name)` |
| <span data-ttu-id="73a9d-161">날짜 함수: 2005 이후 ReleaseDate 사용 하 여 모든 제품을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-161">Date functions: Return all products with ReleaseDate after 2005.</span></span> | <span data-ttu-id="73a9d-162">`http://localhost/Products?$filter=year(ReleaseDate)` 2005 gt</span><span class="sxs-lookup"><span data-stu-id="73a9d-162">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span></span> |

<span data-ttu-id="73a9d-163">**정렬**</span><span class="sxs-lookup"><span data-stu-id="73a9d-163">**Sorting**</span></span>

<span data-ttu-id="73a9d-164">결과 정렬 하려면 $orderby 필터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-164">To sort the results, use the $orderby filter.</span></span>

| <span data-ttu-id="73a9d-165">가격으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-165">Sort by price.</span></span> | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| <span data-ttu-id="73a9d-166">내림차순 (가장 낮은 가장 높음) 가격으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-166">Sort by price in descending order (highest to lowest).</span></span> | `http://localhost/Products?$orderby=Price desc` |
| <span data-ttu-id="73a9d-167">범주별으로 정렬 한 다음 가격 범주 내에서 내림차순으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-167">Sort by category, then sort by price in descending order within categories.</span></span> | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a><span data-ttu-id="73a9d-168">서버 기반 페이징</span><span class="sxs-lookup"><span data-stu-id="73a9d-168">Server-Driven Paging</span></span>

<span data-ttu-id="73a9d-169">보낼 않으려는 데이터베이스 수백만 개의 레코드를 포함 하는 경우 페이로드 하나에 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-169">If your database contains millions of records, you don't want to send them all in one payload.</span></span> <span data-ttu-id="73a9d-170">이 방지 하려면 서버가 단일 응답에 전송 되는 엔트리의 수를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-170">To prevent this, the server can limit the number of entries that it sends in a single response.</span></span> <span data-ttu-id="73a9d-171">페이징을 사용 하도록 서버를 설정 합니다 **PageSize** 속성에는 **Queryable** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-171">To enable server paging, set the **PageSize** property in the **Queryable** attribute.</span></span> <span data-ttu-id="73a9d-172">값에는 반환할 항목의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-172">The value is the maximum number of entries to return.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

<span data-ttu-id="73a9d-173">컨트롤러 OData 형식을 반환 하는 경우 응답 본문에는 데이터의 다음 페이지에 대 한 링크를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-173">If your controller returns OData format, the response body will contain a link to the next page of data:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

<span data-ttu-id="73a9d-174">클라이언트는이 링크를 사용 하 여 다음 페이지를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-174">The client can use this link to fetch the next page.</span></span> <span data-ttu-id="73a9d-175">결과 집합에 있는 항목의 총 수에 알아보려면 "allpages" 클라이언트 $inlinecount 쿼리 옵션 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-175">To learn the total number of entries in the result set, the client can set the $inlinecount query option with the value "allpages".</span></span>

`http://localhost/Products?$inlinecount=allpages`

<span data-ttu-id="73a9d-176">값 "allpages" 응답의 총 수를 포함 하도록 서버에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-176">The value "allpages" tells the server to include the total count in the response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> <span data-ttu-id="73a9d-177">다음 페이지 링크 및 인라인 카운트는 모두 OData 포맷을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-177">Next-page links and inline count both require OData format.</span></span> <span data-ttu-id="73a9d-178">OData 링크 및 개수를 보유 하는 응답 본문의 특수 필드를 정의 하는 이유 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-178">The reason is that OData defines special fields in the response body to hold the link and count.</span></span>


<span data-ttu-id="73a9d-179">OData이 아닌 형식에 대 한 것도 가능에서 쿼리 결과 래핑하여 다음 페이지 링크 및 인라인 카운트를 지원 하기를 **PageResult&lt;T&gt;**  개체입니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-179">For non-OData formats, it is still possible to support next-page links and inline count, by wrapping the query results in a **PageResult&lt;T&gt;** object.</span></span> <span data-ttu-id="73a9d-180">그러나 더 많은 코드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-180">However, it requires a bit more code.</span></span> <span data-ttu-id="73a9d-181">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-181">Here is an example:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

<span data-ttu-id="73a9d-182">JSON 응답 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-182">Here is an example JSON response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a><span data-ttu-id="73a9d-183">쿼리 옵션을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-183">Limiting the Query Options</span></span>

<span data-ttu-id="73a9d-184">쿼리 옵션을 여러 가지 제어 서버에서 실행 되는 쿼리 클라이언트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-184">The query options give the client a lot of control over the query that is run on the server.</span></span> <span data-ttu-id="73a9d-185">경우에 따라 보안 또는 성능 이유로 사용할 수 있는 옵션을 제한 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-185">In some cases, you might want to limit the available options for security or performance reasons.</span></span> <span data-ttu-id="73a9d-186">합니다 **[Queryable]** 특성에 일부 기본 제공 속성에서이 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-186">The **[Queryable]** attribute has some built in properties for this.</span></span> <span data-ttu-id="73a9d-187">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-187">Here are some examples.</span></span>

<span data-ttu-id="73a9d-188">$Skip 및 $top, 페이징 및 아무 지원 하기 위해 허용:</span><span class="sxs-lookup"><span data-stu-id="73a9d-188">Allow only $skip and $top, to support paging and nothing else:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

<span data-ttu-id="73a9d-189">데이터베이스에서 인덱싱되지 않은 속성에 대해 정렬을 방지 하기 위해 특정 속성에 의해서만 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-189">Allow ordering only by certain properties, to prevent sorting on properties that are not indexed in the database:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

<span data-ttu-id="73a9d-190">"Eq" 논리 함수가 되었지만 다른 논리 함수가 없는 허용:</span><span class="sxs-lookup"><span data-stu-id="73a9d-190">Allow the "eq" logical function but no other logical functions:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

<span data-ttu-id="73a9d-191">모든 산술 연산자를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-191">Do not allow any arithmetic operators:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

<span data-ttu-id="73a9d-192">생성 하 여 옵션을 전역적으로 제한할 수 있습니다는 **QueryableAttribute** 인스턴스를 전달 하는 **EnableQuerySupport** 함수:</span><span class="sxs-lookup"><span data-stu-id="73a9d-192">You can restrict options globally by constructing a **QueryableAttribute** instance and passing it to the **EnableQuerySupport** function:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a><span data-ttu-id="73a9d-193">쿼리 옵션을 직접 호출</span><span class="sxs-lookup"><span data-stu-id="73a9d-193">Invoking Query Options Directly</span></span>

<span data-ttu-id="73a9d-194">사용 하는 대신 합니다 **[Queryable]** 특성을 컨트롤러에 직접 쿼리 옵션을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-194">Instead of using the **[Queryable]** attribute, you can invoke the query options directly in your controller.</span></span> <span data-ttu-id="73a9d-195">이렇게 하려면 추가 된 **ODataQueryOptions** 컨트롤러 메서드의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-195">To do so, add an **ODataQueryOptions** parameter to the controller method.</span></span> <span data-ttu-id="73a9d-196">필요 하지 않습니다는 경우에 **[Queryable]** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-196">In this case, you don't need the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

<span data-ttu-id="73a9d-197">웹 API 채웁니다 합니다 **ODataQueryOptions** URI에서 쿼리 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-197">Web API populates the **ODataQueryOptions** from the URI query string.</span></span> <span data-ttu-id="73a9d-198">쿼리를 적용 하려면 전달를 **IQueryable** 에 **ApplyTo** 메서드.</span><span class="sxs-lookup"><span data-stu-id="73a9d-198">To apply the query, pass an **IQueryable** to the **ApplyTo** method.</span></span> <span data-ttu-id="73a9d-199">메서드가 반환 하는 값 **IQueryable**합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-199">The method returns another **IQueryable**.</span></span>

<span data-ttu-id="73a9d-200">고급 시나리오에서는 되지 않은 경우는 **IQueryable** 쿼리 공급자를 검사할 수 있습니다는 **ODataQueryOptions** 쿼리 옵션을 다른 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-200">For advanced scenarios, if you do not have an **IQueryable** query provider, you can examine the **ODataQueryOptions** and translate the query options into another form.</span></span> <span data-ttu-id="73a9d-201">(예를 들어 RaghuRam Nadiminti 블로그 게시물을 참조 [변환 OData 쿼리를 HQL로](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx)에 포함 됩니다는 [샘플](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span><span class="sxs-lookup"><span data-stu-id="73a9d-201">(For example, see RaghuRam Nadiminti's blog post [Translating OData queries to HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), which also includes a [sample](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span></span>

<a id="query-validation"></a>
## <a name="query-validation"></a><span data-ttu-id="73a9d-202">쿼리 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="73a9d-202">Query Validation</span></span>

<span data-ttu-id="73a9d-203">합니다 **[Queryable]** 특성의 쿼리 실행 하기 전에 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-203">The **[Queryable]** attribute validates the query before executing it.</span></span> <span data-ttu-id="73a9d-204">유효성 검사 단계에서 수행 되는 **QueryableAttribute.ValidateQuery** 메서드.</span><span class="sxs-lookup"><span data-stu-id="73a9d-204">The validation step is performed in the **QueryableAttribute.ValidateQuery** method.</span></span> <span data-ttu-id="73a9d-205">유효성 검사 프로세스를 사용자 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-205">You can also customize the validation process.</span></span>

<span data-ttu-id="73a9d-206">도 참조 하세요 [OData 보안 지침](odata-security-guidance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-206">Also see [OData Security Guidance](odata-security-guidance.md).</span></span>

<span data-ttu-id="73a9d-207">즉 클래스 유효성 검사기 중 하나는 재정의에서 정의 하는 먼저 합니다 **Web.Http.OData.Query.Validators** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-207">First, override one of the validator classes that is defined in the **Web.Http.OData.Query.Validators** namespace.</span></span> <span data-ttu-id="73a9d-208">예를 들어, 다음 유효성 검사기 클래스 $orderby 옵션에 대 한 'desc' 옵션을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-208">For example, the following validator class disables the 'desc' option for the $orderby option.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

<span data-ttu-id="73a9d-209">하위 클래스를 **[Queryable]** 특성을 재정의 하는 **ValidateQuery** 메서드.</span><span class="sxs-lookup"><span data-stu-id="73a9d-209">Subclass the **[Queryable]** attribute to override the **ValidateQuery** method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

<span data-ttu-id="73a9d-210">그런 다음 사용자 지정 특성 하거나 전역으로 설정 하거나-컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="73a9d-210">Then set your custom attribute either globally or per-controller:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

<span data-ttu-id="73a9d-211">사용 중인 경우 **ODataQueryOptions** 직접 유효성 검사기에 옵션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="73a9d-211">If you are using **ODataQueryOptions** directly, set the validator on the options:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
