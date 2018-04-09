---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 효율적인 데이터 페이징을 구현 | Microsoft Docs
author: microsoft
description: '8 단계에는 한 번에 dinners의 단위: 1000s를 표시 하는 대신 것만 표시에 예정 된 dinners 10 있도록 페이징 지원을 우리의 /Dinners URL을 추가 하는 방법을 보여 줍니다 중...'
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: 0188e21438820adf2adbe05b047fdb772540e1a0
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="implement-efficient-data-paging"></a><span data-ttu-id="23eeb-103">효율적인 데이터 페이징을 구현합니다</span><span class="sxs-lookup"><span data-stu-id="23eeb-103">Implement Efficient Data Paging</span></span>
====================
<span data-ttu-id="23eeb-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="23eeb-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="23eeb-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="23eeb-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="23eeb-106">이 무료의 8 단계로 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-106">This is step 8 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="23eeb-107">8 단계에는 한 번에 dinners의 단위: 1000s를 표시 하는 대신 것만 표시 10 예정 된 dinners-한 번에 되 고 최종 사용자가 전체 목록을 SEO 친화적인 방식에서 앞뒤로 이동 하며 다시 페이지 수 있도록 우리의 /Dinners URL에 대 한 페이징 지원을 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-107">Step 8 shows how to add paging support to our /Dinners URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>
> 
> <span data-ttu-id="23eeb-108">ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-8-paging-support"></a><span data-ttu-id="23eeb-109">업그레이드 되었으며 수정 8 단계: 페이징 지원</span><span class="sxs-lookup"><span data-stu-id="23eeb-109">NerdDinner Step 8: Paging Support</span></span>

<span data-ttu-id="23eeb-110">사이트에 성공한 경우 예정 된 dinners 수천을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-110">If our site is successful, it will have thousands of upcoming dinners.</span></span> <span data-ttu-id="23eeb-111">UI 조정 이러한 dinners 모두 처리 하 고 사용자가 찾아볼 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-111">We need to make sure that our UI scales to handle all of these dinners, and allows users to browse them.</span></span> <span data-ttu-id="23eeb-112">이 작업이 가능 하려면 페이징 지원을 추가 합니다 우리의 */Dinners* dinners의 1000s에서는 한 번에 표시 하는의 대신 URL 합니다만-한 번에 10 예정 된 dinners 표시 및 최종 사용자가 전체 목록에서 앞뒤로 이동 하며 백 페이지 수 SEO 친숙 한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-112">To enable this, we'll add paging support to our */Dinners* URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>

### <a name="index-action-method-recap"></a><span data-ttu-id="23eeb-113">Index () 동작 방법 간략하게 설명</span><span class="sxs-lookup"><span data-stu-id="23eeb-113">Index() Action Method Recap</span></span>

<span data-ttu-id="23eeb-114">Index () 동작 메서드가 DinnersController 클래스 내에서 현재과 같은 형식 아래:</span><span class="sxs-lookup"><span data-stu-id="23eeb-114">The Index() action method within our DinnersController class currently looks like below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

<span data-ttu-id="23eeb-115">요청 하면는 */Dinners* URL을 모든 향후 dinners의 목록을 검색 하 고 모든 여 목록이 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-115">When a request is made to the */Dinners* URL, it retrieves a list of all upcoming dinners and then renders a listing of all of them out:</span></span>

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iquerablelttgt"></a><span data-ttu-id="23eeb-116">이해 IQuerable&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="23eeb-116">Understanding IQuerable&lt;T&gt;</span></span>

<span data-ttu-id="23eeb-117">*IQueryable&lt;T&gt;*  LINQ 사용 하 여.NET 3.5의 일부로 도입 된 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-117">*IQueryable&lt;T&gt;* is an interface that was introduced with LINQ as part of .NET 3.5.</span></span> <span data-ttu-id="23eeb-118">에서는 사용할 수 있는의 페이징 지원을 구현 하는 강력한 "지연 된 실행" 시나리오를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-118">It enables powerful "deferred execution" scenarios that we can take advantage of to implement paging support.</span></span>

<span data-ttu-id="23eeb-119">우리의 DinnerRepository에서 우리 반환 하는 경우 IQueryable&lt;Dinner&gt; 우리의 FindUpcomingDinners() 메서드에서 시퀀스:</span><span class="sxs-lookup"><span data-stu-id="23eeb-119">In our DinnerRepository we are returning an IQueryable&lt;Dinner&gt; sequence from our FindUpcomingDinners() method:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

<span data-ttu-id="23eeb-120">IQueryable&lt;Dinner&gt; 우리의 FindUpcomingDinners() 메서드에서 반환 된 개체는 LINQ to SQL 사용 하 여 데이터베이스에서 Dinner 개체를 검색 하는 쿼리를 캡슐화 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-120">The IQueryable&lt;Dinner&gt; object returned by our FindUpcomingDinners() method encapsulates a query to retrieve Dinner objects from our database using LINQ to SQL.</span></span> <span data-ttu-id="23eeb-121">중요 한 사실은 tolist () 메서드를 호출 하거나 액세스/는 쿼리의 데이터를에서 반복 하려고 하면 될 때까지 데이터베이스에 대해 쿼리를 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-121">Importantly, it won't execute the query against the database until we attempt to access/iterate over the data in the query, or until we call the ToList() method on it.</span></span> <span data-ttu-id="23eeb-122">우리의 FindUpcomingDinners() 메서드를 호출 하는 코드는 IQueryable에 "연결 된" 작업/필터를 추가 하도록 선택할 수도&lt;Dinner&gt; 쿼리를 실행 하기 전에 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-122">The code calling our FindUpcomingDinners() method can optionally choose to add additional "chained" operations/filters to the IQueryable&lt;Dinner&gt; object before executing the query.</span></span> <span data-ttu-id="23eeb-123">LINQ to SQL은 다음 데이터가 요청 될 때 데이터베이스에 대해 결합 된 쿼리를 실행 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-123">LINQ to SQL is then smart enough to execute the combined query against the database when the data is requested.</span></span>

<span data-ttu-id="23eeb-124">페이징 논리를 구현 하려면 업데이트 하면 다음과 같이 우리의 DinnersController index () 동작 메서드에 추가 "Skip"과 "사용" 연산자는 반환 된 IQueryable에 적용 되도록&lt;Dinner&gt; 시퀀스에 tolist () 호출 하기 전에:</span><span class="sxs-lookup"><span data-stu-id="23eeb-124">To implement paging logic we can update our DinnersController's Index() action method so that it applies additional "Skip" and "Take" operators to the returned IQueryable&lt;Dinner&gt; sequence before calling ToList() on it:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

<span data-ttu-id="23eeb-125">위의 코드는 데이터베이스에 있는 처음 10 개의 예정 된 dinners 다루지 않으며 하 고 20 dinners 다시 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-125">The above code skips over the first 10 upcoming dinners in the database, and then returns back 20 dinners.</span></span> <span data-ttu-id="23eeb-126">LINQ to SQL은 SQL 데이터베이스-와 웹 서버에 없는 논리를 건너뛰는 중 수행 하는 최적화 된 SQL 쿼리를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-126">LINQ to SQL is smart enough to construct an optimized SQL query that performs this skipping logic in the SQL database – and not in the web-server.</span></span> <span data-ttu-id="23eeb-127">즉, 예정 된 Dinners 수많은 데이터베이스에 있는, 경우에 원하는 10만 (있어 효율적이 고 확장 가능한)이 요청의 일부로 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-127">This means that even if we have millions of upcoming Dinners in the database, only the 10 we want will be retrieved as part of this request (making it efficient and scalable).</span></span>

### <a name="adding-a-page-value-to-the-url"></a><span data-ttu-id="23eeb-128">URL에 "페이지" 값 추가</span><span class="sxs-lookup"><span data-stu-id="23eeb-128">Adding a "page" value to the URL</span></span>

<span data-ttu-id="23eeb-129">대신를 하드 코딩 하는 특정 페이지 범위는 사용자가 요청 하는 Dinner 범위를 나타내는 "페이지" 매개 변수를 포함 하도록 Url 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-129">Instead of hard-coding a specific page range, we'll want our URLs to include a "page" parameter that indicates which Dinner range a user is requesting.</span></span>

#### <a name="using-a-querystring-value"></a><span data-ttu-id="23eeb-130">쿼리 문자열 값을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="23eeb-130">Using a Querystring value</span></span>

<span data-ttu-id="23eeb-131">아래의 코드 우리의 index () 동작 메서드를 쿼리 문자열 매개 변수를 지원 하 고 같은 Url을 사용 하려면 업데이트 하면 어떻게 설명 */Dinners? 페이지 2 =*:</span><span class="sxs-lookup"><span data-stu-id="23eeb-131">The code below demonstrates how we can update our Index() action method to support a querystring parameter and enable URLs like */Dinners?page=2*:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

<span data-ttu-id="23eeb-132">위의 index () 동작 메서드 매개 변수 이름 "페이지"에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-132">The Index() action method above has a parameter named "page".</span></span> <span data-ttu-id="23eeb-133">매개 변수는 null을 허용 정수로 선언 (즉 어떤 int? 나타냅니다).</span><span class="sxs-lookup"><span data-stu-id="23eeb-133">The parameter is declared as a nullable integer (that is what int? indicates).</span></span> <span data-ttu-id="23eeb-134">즉는 */Dinners? 페이지 2 =* URL 값이 "2" 매개 변수 값으로 전달 하도록 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-134">This means that the */Dinners?page=2* URL will cause a value of "2" to be passed as the parameter value.</span></span> <span data-ttu-id="23eeb-135">*/Dinners* (querystring 값)이 없는 URL에는 null 값이 전달 될 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-135">The */Dinners* URL (without a querystring value) will cause a null value to be passed.</span></span>

<span data-ttu-id="23eeb-136">페이지 크기 (이 경우 10 행)에 따라 페이지 값을 곱하여 우리를 건너 뛰 개수 dinners 확인 하려면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-136">We are multiplying the page value by the page size (in this case 10 rows) to determine how many dinners to skip over.</span></span> <span data-ttu-id="23eeb-137">사용 하 여 ["C# null 병합" 연산자 (?) ](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) nullable 형식을 처리할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-137">We are using the [C# null "coalescing" operator (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) which is useful when dealing with nullable types.</span></span> <span data-ttu-id="23eeb-138">위의 코드 페이지 매개 변수가 null 이면 페이지 0의 값을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-138">The code above assigns page the value of 0 if the page parameter is null.</span></span>

#### <a name="using-embedded-url-values"></a><span data-ttu-id="23eeb-139">포함 된 URL 값을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="23eeb-139">Using Embedded URL values</span></span>

<span data-ttu-id="23eeb-140">쿼리 문자열 값을 사용 하는 대신 실제 URL 자체 내에서 페이지 매개 변수를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-140">An alternative to using a querystring value would be to embed the page parameter within the actual URL itself.</span></span> <span data-ttu-id="23eeb-141">예를 들어: */Dinners/Page/2* 또는 */Dinners/2*합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-141">For example: */Dinners/Page/2* or */Dinners/2*.</span></span> <span data-ttu-id="23eeb-142">ASP.NET MVC에는 다음과 같은 시나리오를 지원 하기 위해 활용할 수 있는 강력한 URL 라우팅 엔진 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-142">ASP.NET MVC includes a powerful URL routing engine that makes it easy to support scenarios like this.</span></span>

<span data-ttu-id="23eeb-143">수신 하는 URL 또는 URL 형식을 원하는 모든 컨트롤러 클래스 또는 동작 메서드에 매핑되는 사용자 지정 라우팅 규칙을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-143">We can register custom routing rules that map any incoming URL or URL format to any controller class or action method we want.</span></span> <span data-ttu-id="23eeb-144">이 프로젝트 내에서 Global.asax 파일을 여는 해야 할 일:</span><span class="sxs-lookup"><span data-stu-id="23eeb-144">All we need to-do is to open the Global.asax file within our project:</span></span>

![](implement-efficient-data-paging/_static/image2.png)

<span data-ttu-id="23eeb-145">다음 경로에 첫 번째 호출 처럼 MapRoute() 도우미 메서드를 사용 하 여 새 매핑 규칙을 등록 하십시오. 아래 MapRoute():</span><span class="sxs-lookup"><span data-stu-id="23eeb-145">And then register a new mapping rule using the MapRoute() helper method like the first call to routes.MapRoute() below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

<span data-ttu-id="23eeb-146">위에 "UpcomingDinners" 이라는 새 라우팅 규칙을 등록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-146">Above we are registering a new routing rule named "UpcomingDinners".</span></span> <span data-ttu-id="23eeb-147">URL 형식은 있음을 나타냅니다 합니다. "Dinners/페이지 / {페이지}" – 여기서 {페이지}은 URL 내에 포함 된 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-147">We are indicating it has the URL format "Dinners/Page/{page}" – where {page} is a parameter value embedded within the URL.</span></span> <span data-ttu-id="23eeb-148">MapRoute() 메서드를 세 번째 매개 변수는이 형식을 DinnersController 클래스에 index () 동작 메서드에 일치 하는 Url을 매핑할 해야 있습니다를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-148">The third parameter to the MapRoute() method indicates that we should map URLs that match this format to the Index() action method on the DinnersController class.</span></span>

<span data-ttu-id="23eeb-149">해야 하기 전에 쿼리 문자열-이 시나리오와 URL과 쿼리 문자열 하지에서 가져온 우리의 "페이지" 매개 변수는 이제 점을 제외 하 고 정확한 동일한 index () 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-149">We can use the exact same Index() code we had before with our Querystring scenario – except now our "page" parameter will come from the URL and not the querystring:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

<span data-ttu-id="23eeb-150">이제 응용 프로그램을 실행 하 고를 입력 했습니다 및 */Dinners* 처음 10 개의 예정 된 dinners 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-150">And now when we run the application and type in */Dinners* we'll see the first 10 upcoming dinners:</span></span>

![](implement-efficient-data-paging/_static/image3.png)

<span data-ttu-id="23eeb-151">여기서 입력 하 고 */Dinners/Page/1* dinners의 다음 페이지를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-151">And when we type in */Dinners/Page/1* we'll see the next page of dinners:</span></span>

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a><span data-ttu-id="23eeb-152">페이지 탐색 UI 추가</span><span class="sxs-lookup"><span data-stu-id="23eeb-152">Adding page navigation UI</span></span>

<span data-ttu-id="23eeb-153">페이징 시나리오를 완료 하기 위한 마지막 단계는 사용자가을 쉽게 Dinner 데이터에 대해 건너뛸 수 있도록 우리의 보기 템플릿 내에서 "다음" 및 "이전" 탐색 UI를 구현 하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-153">The last step to complete our paging scenario will be to implement "next" and "previous" navigation UI within our view template to enable users to easily skip over the Dinner data.</span></span>

<span data-ttu-id="23eeb-154">이 올바르게 구현 하려면 해야 데이터베이스에 Dinners의 총 수를 아는 데이터의 여러 페이지를 변환 하는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-154">To implement this correctly, we'll need to know the total number of Dinners in the database, as well as how many pages of data this translates to.</span></span> <span data-ttu-id="23eeb-155">그런 다음는 데이터의 끝 부분이 나 부분에 현재 요청 된 "페이지" 값이 있는지 여부를 계산 하 고 표시 하거나 그에 따라 "이전" 및 "다음" UI를 숨길 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-155">We'll then need to calculate whether the currently requested "page" value is at the beginning or end of the data, and show or hide the "previous" and "next" UI accordingly.</span></span> <span data-ttu-id="23eeb-156">구현 하 여이 논리는 index () 작업 메서드 내에서.</span><span class="sxs-lookup"><span data-stu-id="23eeb-156">We could implement this logic within our Index() action method.</span></span> <span data-ttu-id="23eeb-157">또는 더 재사용 가능한 방식으로이 논리를 캡슐화 하는 프로젝트에는 도우미 클래스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-157">Alternatively we can add a helper class to our project that encapsulates this logic in a more re-usable way.</span></span>

<span data-ttu-id="23eeb-158">다음 목록에서 파생 되는 간단한 "PaginatedList" 도우미 클래스를은&lt;T&gt; 에 기본 제공 컬렉션 클래스는.NET Framework입니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-158">Below is a simple "PaginatedList" helper class that derives from the List&lt;T&gt; collection class built-into the .NET Framework.</span></span> <span data-ttu-id="23eeb-159">IQueryable 데이터의 모든 연속 페이지를 매기는 데 사용할 수 있는 재사용 가능한 컬렉션 클래스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-159">It implements a re-usable collection class that can be used to paginate any sequence of IQueryable data.</span></span> <span data-ttu-id="23eeb-160">이 업그레이드 되었으며 수정 응용 프로그램에서 되 겠 IQueryable을 통해 작동&lt;Dinner&gt; 하지만 결과 쉽게 사용 될 수 IQueryable&lt;제품&gt; 또는 IQueryable&lt;고객&gt;다른 응용 프로그램 시나리오에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-160">In our NerdDinner application we'll have it work over IQueryable&lt;Dinner&gt; results, but it could just as easily be used against IQueryable&lt;Product&gt; or IQueryable&lt;Customer&gt; results in other application scenarios:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

<span data-ttu-id="23eeb-161">위의 계산 방법 및 다음 속성을 노출 "PageIndex", "PageSize", "TotalCount" 및 "TotalPages"와 같은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-161">Notice above how it calculates and then exposes properties like "PageIndex", "PageSize", "TotalCount", and "TotalPages".</span></span> <span data-ttu-id="23eeb-162">그 후 컬렉션에 있는 데이터 페이지의 시작 이나는 원래 시퀀스의 끝이를 나타내는 두 개의 도우미 속성 "HasPreviousPage" 및 "HasNextPage"를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-162">It also then exposes two helper properties "HasPreviousPage" and "HasNextPage" that indicate whether the page of data in the collection is at the beginning or end of the original sequence.</span></span> <span data-ttu-id="23eeb-163">위의 코드에서는 두 개의 SQL 쿼리 Dinner 개체의 총 수를 검색할 때 첫 번째 실행-수를 발생 시킵니다 (이 개체를 반환 하지 않는 – 대신 정수를 반환 하는 "SELECT COUNT" 문을 수행)의 행만 검색 하 고 두 번째 데이터의 현재 페이지에 대 한 데이터베이스에서 필요한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-163">The above code will cause two SQL queries to be run - the first to retrieve the count of the total number of Dinner objects (this doesn't return the objects – rather it performs a "SELECT COUNT" statement that returns an integer), and the second to retrieve just the rows of data we need from our database for the current page of data.</span></span>

<span data-ttu-id="23eeb-164">PaginatedList 만들려는 DinnersController.Index() 도우미 메서드를 업데이트할 수 있습니다&lt;Dinner&gt; 우리의 DinnerRepository.FindUpcomingDinners()에서 결과, 우리의 템플릿 보기에 게 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-164">We can then update our DinnersController.Index() helper method to create a PaginatedList&lt;Dinner&gt; from our DinnerRepository.FindUpcomingDinners() result, and pass it to our view template:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

<span data-ttu-id="23eeb-165">ViewPage 상속할 \Views\Dinners\Index.aspx 뷰 템플릿을 업데이트할 수 있습니다&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt; &gt; ViewPage 대신&lt;IEnumerable&lt;Dinner&gt;&gt;을 표시 하거나 숨기려면 다음 및 이전 탐색 UI 우리의 보기 템플릿 맨 아래에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-165">We can then update the \Views\Dinners\Index.aspx view template to inherit from ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt;&gt; instead of ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;, and then add the following code to the bottom of our view-template to show or hide next and previous navigation UI:</span></span>

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

<span data-ttu-id="23eeb-166">위의 Html.RouteLink() 도우미 메서드를 사용 하는 하이퍼링크를 생성할 우리는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-166">Notice above how we are using the Html.RouteLink() helper method to generate our hyperlinks.</span></span> <span data-ttu-id="23eeb-167">이 메서드는 이전에 사용한 Html.ActionLink() 도우미 메서드는 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-167">This method is similar to the Html.ActionLink() helper method we've used previously.</span></span> <span data-ttu-id="23eeb-168">쿼리하여 Global.asax 파일 내에서 설정 하는 규칙을 라우팅 "UpcomingDinners"를 사용 하 여 URL을 생성 하기는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-168">The difference is that we are generating the URL using the "UpcomingDinners" routing rule we setup within our Global.asax file.</span></span> <span data-ttu-id="23eeb-169">이렇게 하면 형식 취급 index () 동작 메서드에 Url을 생성 합니다 म: */Dinners/페이지 / {페이지}* – 여기서 {페이지} 값은 변수를 제공 하 고 위에 현재 PageIndex 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-169">This ensures that we'll generate URLs to our Index() action method that have the format: */Dinners/Page/{page}* – where the {page} value is a variable we are providing above based on the current PageIndex.</span></span>

<span data-ttu-id="23eeb-170">지금 응용 프로그램을 실행할 때 다시 보게 한 번에 10 dinners 브라우저에:</span><span class="sxs-lookup"><span data-stu-id="23eeb-170">And now when we run our application again we'll see 10 dinners at a time in our browser:</span></span>

![](implement-efficient-data-paging/_static/image5.png)

<span data-ttu-id="23eeb-171">이 밖에도 &lt; &lt; &lt; 및 &gt; &gt; &gt; 탐색 UI 통해 전달 건너뛰고 이전 버전과 사용 하 여이 데이터를 통해 엔진 액세스할 수 있는 Url을 검색 하는 페이지의 맨 아래에:</span><span class="sxs-lookup"><span data-stu-id="23eeb-171">We also have &lt;&lt;&lt; and &gt;&gt;&gt; navigation UI at the bottom of the page that allows us to skip forwards and backwards over our data using search engine accessible URLs:</span></span>

![](implement-efficient-data-paging/_static/image6.png)

| <span data-ttu-id="23eeb-172">**쪽 주제: IQueryable의 의미를 이해 하&lt;T&gt;**</span><span class="sxs-lookup"><span data-stu-id="23eeb-172">**Side Topic: Understanding the implications of IQueryable&lt;T&gt;**</span></span> |
| --- |
| <span data-ttu-id="23eeb-173">IQueryable&lt;T&gt; 는 다양 한 흥미로운 지연 된 실행 시나리오를 사용 하도록 설정 하는 매우 강력한 기능 (페이징 및 컴퍼지션와 마찬가지로 쿼리 기반).</span><span class="sxs-lookup"><span data-stu-id="23eeb-173">IQueryable&lt;T&gt; is a very powerful feature that enables a variety of interesting deferred execution scenarios (like paging and composition based queries).</span></span> <span data-ttu-id="23eeb-174">으로 모든 강력한 기능이 사용법에 주의를 기울여야을 남용 되지 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-174">As with all powerful features, you want to be careful with how you use it and make sure it is not abused.</span></span> <span data-ttu-id="23eeb-175">해당 반환 IQueryable 인식 해야&lt;T&gt; 리포지토리에서 결과 호출 코드에 연결 된 연산자 메서드를 추가 하 고 최고의 쿼리 실행에 참여 하므로를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-175">It is important to recognize that returning an IQueryable&lt;T&gt; result from your repository enables calling code to append on chained operator methods to it, and so participate in the ultimate query execution.</span></span> <span data-ttu-id="23eeb-176">호출 코드에이 기능을 제공 하지 않을 경우 되돌려야 IList 다시&lt;T&gt; 또는 IEnumerable&lt;T&gt; 가 이미 실행 된 쿼리의 결과 포함 하는 결과-합니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-176">If you do not want to provide calling code this ability, then you should return back IList&lt;T&gt; or IEnumerable&lt;T&gt; results - which contain the results of a query that has already executed.</span></span> <span data-ttu-id="23eeb-177">페이지 매김 시나리오에 대 한 해야 실제 데이터 페이지 매김 논리 호출 되는 저장소 메서드에 푸시 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23eeb-177">For pagination scenarios this would require you to push the actual data pagination logic into the repository method being called.</span></span> <span data-ttu-id="23eeb-178">이 시나리오에서는 우리의 FindUpcomingDinners() finder 메서드를 사용 하려면 한 PaginatedList를 반환 하거나 서명 업데이트 될 수 있습니다: PaginatedList&lt; Dinner&gt; FindUpcomingDinners (pageIndex int, int pageSize) {} 반환 IList 또는 &lt;Dinner&gt;, param 아웃 "totalCount"를 사용 하 여 Dinners의 총 수를 반환 하: IList&lt;Dinner&gt; FindUpcomingDinners (pageIndex int, int totalCount out int pageSize) {}</span><span class="sxs-lookup"><span data-stu-id="23eeb-178">In this scenario we might update our FindUpcomingDinners() finder method to have a signature that either returned a PaginatedList: PaginatedList&lt; Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize) { } Or return back an IList&lt;Dinner&gt;, and use a "totalCount" out param to return the total count of Dinners: IList&lt;Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize, out int totalCount) { }</span></span> |

### <a name="next-step"></a><span data-ttu-id="23eeb-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="23eeb-179">Next Step</span></span>

<span data-ttu-id="23eeb-180">이제 살펴보겠습니다 응용 프로그램에 인증 및 권한 부여 지원을 추가할 수 있는 방법.</span><span class="sxs-lookup"><span data-stu-id="23eeb-180">Let's now look at how we can add authentication and authorization support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="23eeb-181">[이전](re-use-ui-using-master-pages-and-partials.md)
> [다음](secure-applications-using-authentication-and-authorization.md)</span><span class="sxs-lookup"><span data-stu-id="23eeb-181">[Previous](re-use-ui-using-master-pages-and-partials.md)
[Next](secure-applications-using-authentication-and-authorization.md)</span></span>
