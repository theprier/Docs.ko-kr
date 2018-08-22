---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 효율적인 데이터 페이징 구현 | Microsoft Docs
author: microsoft
description: 8 단계 대신 dinners 한 번에 수천 개의 표시만 표시 됩니다에서 10 향후 dinners 있도록 /Dinners URL 페이징 지원을 추가 하는 방법을 보여 줍니다...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: 2bef690355cd1f89a15a67f0c49775296d551136
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837531"
---
<a name="implement-efficient-data-paging"></a><span data-ttu-id="deb1c-103">효율적인 데이터 페이징 구현</span><span class="sxs-lookup"><span data-stu-id="deb1c-103">Implement Efficient Data Paging</span></span>
====================
<span data-ttu-id="deb1c-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="deb1c-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="deb1c-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="deb1c-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="deb1c-106">이 무료의 8 단계로 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-106">This is step 8 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="deb1c-107">8 단계 dinners 한 번에 수천 개의 표시 하는 대신 수만 번-10 향후 dinners 표시 하 고 다시 페이지를 앞뒤로 전체 목록 SEO 친숙 한 방식으로 최종 사용자를 허용 /Dinners URL에 대 한 페이징 지원을 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-107">Step 8 shows how to add paging support to our /Dinners URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>
> 
> <span data-ttu-id="deb1c-108">ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-8-paging-support"></a><span data-ttu-id="deb1c-109">NerdDinner 8 단계: 페이징 지원</span><span class="sxs-lookup"><span data-stu-id="deb1c-109">NerdDinner Step 8: Paging Support</span></span>

<span data-ttu-id="deb1c-110">사이트에 성공한 경우 향후 dinners 수천 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-110">If our site is successful, it will have thousands of upcoming dinners.</span></span> <span data-ttu-id="deb1c-111">UI 모두 이러한 dinners 처리 크기를 조정 하 고 찾아볼 수 있도록 허용 하는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-111">We need to make sure that our UI scales to handle all of these dinners, and allows users to browse them.</span></span> <span data-ttu-id="deb1c-112">이 작업이 가능 하도록 페이징 지원을 추가한 우리의 */Dinners* 에서는 한 번에 수천 개의 dinners 표시의 URL에서는 표시 10 향후 dinners-번 하 고 최종 사용자의 전체 목록을 통해 앞뒤로 페이지 뒤로 허용 SEO 친숙 한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-112">To enable this, we'll add paging support to our */Dinners* URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>

### <a name="index-action-method-recap"></a><span data-ttu-id="deb1c-113">Index () 작업 메서드 요약</span><span class="sxs-lookup"><span data-stu-id="deb1c-113">Index() Action Method Recap</span></span>

<span data-ttu-id="deb1c-114">Index () 작업 메서드에서 DinnersController 클래스 내에서 현재 같습니다 아래:</span><span class="sxs-lookup"><span data-stu-id="deb1c-114">The Index() action method within our DinnersController class currently looks like below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

<span data-ttu-id="deb1c-115">요청 하면를 */Dinners* URL 모든 향후 dinners 목록을 검색 하 고 모든 수의 목록을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-115">When a request is made to the */Dinners* URL, it retrieves a list of all upcoming dinners and then renders a listing of all of them out:</span></span>

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iquerablelttgt"></a><span data-ttu-id="deb1c-116">이해 IQuerable&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="deb1c-116">Understanding IQuerable&lt;T&gt;</span></span>

<span data-ttu-id="deb1c-117">*IQueryable&lt;T&gt;*  LINQ를 사용 하 여.NET 3.5의 일부로 도입 하는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-117">*IQueryable&lt;T&gt;* is an interface that was introduced with LINQ as part of .NET 3.5.</span></span> <span data-ttu-id="deb1c-118">에서는 사용할 수 있는의 페이징 지원을 구현 하기 위해 강력한 "지연 된 실행" 시나리오를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-118">It enables powerful "deferred execution" scenarios that we can take advantage of to implement paging support.</span></span>

<span data-ttu-id="deb1c-119">우리의 DinnerRepository에서 IQueryable 받았다고 했습니다&lt;Dinner&gt; FindUpcomingDinners() 메서드 시퀀스:</span><span class="sxs-lookup"><span data-stu-id="deb1c-119">In our DinnerRepository we are returning an IQueryable&lt;Dinner&gt; sequence from our FindUpcomingDinners() method:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

<span data-ttu-id="deb1c-120">IQueryable&lt;Dinner&gt; 우리의 FindUpcomingDinners() 메서드에서 반환 된 개체를 LINQ to SQL 사용 하 여 데이터베이스에서 Dinner 개체를 검색할 쿼리를 캡슐화 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-120">The IQueryable&lt;Dinner&gt; object returned by our FindUpcomingDinners() method encapsulates a query to retrieve Dinner objects from our database using LINQ to SQL.</span></span> <span data-ttu-id="deb1c-121">중요 한 점은 tolist () 메서드를 호출 하거나 쿼리에서 데이터에 대해 액세스/반복 시도 될 때까지 데이터베이스에 대해 쿼리를 실행 하지 않습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-121">Importantly, it won't execute the query against the database until we attempt to access/iterate over the data in the query, or until we call the ToList() method on it.</span></span> <span data-ttu-id="deb1c-122">FindUpcomingDinners() 메서드를 호출 하는 코드를 IQueryable "연결된" 작업/필터를 추가 하도록 선택할 수도&lt;Dinner&gt; 쿼리를 실행 하기 전에 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-122">The code calling our FindUpcomingDinners() method can optionally choose to add additional "chained" operations/filters to the IQueryable&lt;Dinner&gt; object before executing the query.</span></span> <span data-ttu-id="deb1c-123">LINQ to SQL은 다음 데이터가 요청 될 때 데이터베이스에 대해 결합 된 쿼리를 실행 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-123">LINQ to SQL is then smart enough to execute the combined query against the database when the data is requested.</span></span>

<span data-ttu-id="deb1c-124">페이징 논리를 구현 하려면 업데이트할 수 있습니다 추가 "Skip" 및 "Take" 연산자는 반환 된 IQueryable에 적용 되도록이 DinnersController index () 작업 메서드&lt;Dinner&gt; tolist ()를 호출 하기 전에 시퀀스:</span><span class="sxs-lookup"><span data-stu-id="deb1c-124">To implement paging logic we can update our DinnersController's Index() action method so that it applies additional "Skip" and "Take" operators to the returned IQueryable&lt;Dinner&gt; sequence before calling ToList() on it:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

<span data-ttu-id="deb1c-125">위의 코드는 데이터베이스의 처음 10 개 향후 dinners 건너뜁니다 및 다시 20 dinners 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-125">The above code skips over the first 10 upcoming dinners in the database, and then returns back 20 dinners.</span></span> <span data-ttu-id="deb1c-126">LINQ to SQL은 웹 서버 및 SQL database –의 논리를 건너뛰는 중 수행 하는 최적화 된 SQL 쿼리를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-126">LINQ to SQL is smart enough to construct an optimized SQL query that performs this skipping logic in the SQL database – and not in the web-server.</span></span> <span data-ttu-id="deb1c-127">즉, 한 예정 된 Dinners 수백만 개의 데이터베이스의 경우에 원하는 10만 (있으므로 효율적이 고 확장 가능한)이 요청의 일부로 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-127">This means that even if we have millions of upcoming Dinners in the database, only the 10 we want will be retrieved as part of this request (making it efficient and scalable).</span></span>

### <a name="adding-a-page-value-to-the-url"></a><span data-ttu-id="deb1c-128">URL에 "페이지" 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-128">Adding a "page" value to the URL</span></span>

<span data-ttu-id="deb1c-129">하드 코딩 대신 특정 페이지 범위에는 사용자가 요청 하는 Dinner 범위를 나타내는 "페이지" 매개 변수를 포함 하도록 Url 하 려 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-129">Instead of hard-coding a specific page range, we'll want our URLs to include a "page" parameter that indicates which Dinner range a user is requesting.</span></span>

#### <a name="using-a-querystring-value"></a><span data-ttu-id="deb1c-130">쿼리 문자열 값을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="deb1c-130">Using a Querystring value</span></span>

<span data-ttu-id="deb1c-131">아래 코드 쿼리 문자열 매개 변수를 지원 하 고 같은 Url을 사용 하도록 설정 하는 우리의 index () 작업 메서드를 업데이트 하는 방법을 보여 줍니다 */Dinners? 페이지 2 =*:</span><span class="sxs-lookup"><span data-stu-id="deb1c-131">The code below demonstrates how we can update our Index() action method to support a querystring parameter and enable URLs like */Dinners?page=2*:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

<span data-ttu-id="deb1c-132">위의 index () 작업 메서드는 "페이지" 라는 매개 변수.</span><span class="sxs-lookup"><span data-stu-id="deb1c-132">The Index() action method above has a parameter named "page".</span></span> <span data-ttu-id="deb1c-133">Nullable 정수로 선언 된 매개 변수 (어떤 int는? 나타냅니다).</span><span class="sxs-lookup"><span data-stu-id="deb1c-133">The parameter is declared as a nullable integer (that is what int? indicates).</span></span> <span data-ttu-id="deb1c-134">즉 합니다 */Dinners? 페이지 = 2* URL 값이 "2" 매개 변수 값으로 전달할 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-134">This means that the */Dinners?page=2* URL will cause a value of "2" to be passed as the parameter value.</span></span> <span data-ttu-id="deb1c-135">합니다 */Dinners* URL (쿼리 문자열 값)이 없는 null 값이 전달 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-135">The */Dinners* URL (without a querystring value) will cause a null value to be passed.</span></span>

<span data-ttu-id="deb1c-136">건너뛸 수 dinners 결정할 페이지 크기 (이 경우 10 행)에 따라 페이지 값을 곱하여 됩니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-136">We are multiplying the page value by the page size (in this case 10 rows) to determine how many dinners to skip over.</span></span> <span data-ttu-id="deb1c-137">사용 하 여 [C# null "병합" 연산자 (?) ](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) nullable 형식을 처리할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-137">We are using the [C# null "coalescing" operator (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) which is useful when dealing with nullable types.</span></span> <span data-ttu-id="deb1c-138">위의 코드 페이지 매개 변수가 null 이면 페이지 값이 0 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-138">The code above assigns page the value of 0 if the page parameter is null.</span></span>

#### <a name="using-embedded-url-values"></a><span data-ttu-id="deb1c-139">포함 된 URL 값을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="deb1c-139">Using Embedded URL values</span></span>

<span data-ttu-id="deb1c-140">쿼리 문자열 값을 사용 하는 대신 실제 URL 자체 내에서 페이지 매개 변수를 포함 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-140">An alternative to using a querystring value would be to embed the page parameter within the actual URL itself.</span></span> <span data-ttu-id="deb1c-141">예를 들어: */Dinners/Page/2* 하거나 *Dinners/2*합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-141">For example: */Dinners/Page/2* or */Dinners/2*.</span></span> <span data-ttu-id="deb1c-142">ASP.NET MVC에는 이와 같은 시나리오를 지원 하기 위해 활용할 수 있는 강력한 URL 라우팅 엔진을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-142">ASP.NET MVC includes a powerful URL routing engine that makes it easy to support scenarios like this.</span></span>

<span data-ttu-id="deb1c-143">모든 들어오는 URL 또는 URL 형식을 원하는 모든 컨트롤러 클래스 또는 동작 메서드에 매핑되는 사용자 지정 라우팅 규칙을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-143">We can register custom routing rules that map any incoming URL or URL format to any controller class or action method we want.</span></span> <span data-ttu-id="deb1c-144">할 일 됩니다 프로젝트 내에서 Global.asax 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-144">All we need to-do is to open the Global.asax file within our project:</span></span>

![](implement-efficient-data-paging/_static/image2.png)

<span data-ttu-id="deb1c-145">및 다음 첫 번째 경로 같은 MapRoute() 도우미 메서드를 사용 하 여 새 매핑 규칙을 등록 합니다. MapRoute() 아래:</span><span class="sxs-lookup"><span data-stu-id="deb1c-145">And then register a new mapping rule using the MapRoute() helper method like the first call to routes.MapRoute() below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

<span data-ttu-id="deb1c-146">위의 "UpcomingDinners" 이라는 새 라우팅 규칙을 등록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-146">Above we are registering a new routing rule named "UpcomingDinners".</span></span> <span data-ttu-id="deb1c-147">URL 형식은 나타내는 됩니다 것 "Dinners/페이지 / {페이지}" – {page} 인 URL 내에 포함 된 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-147">We are indicating it has the URL format "Dinners/Page/{page}" – where {page} is a parameter value embedded within the URL.</span></span> <span data-ttu-id="deb1c-148">MapRoute() 메서드에 세 번째 매개 변수 DinnersController 클래스에 index () 작업 메서드에이 형식과 일치 하는 Url 매핑하는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-148">The third parameter to the MapRoute() method indicates that we should map URLs that match this format to the Index() action method on the DinnersController class.</span></span>

<span data-ttu-id="deb1c-149">앞에서 사용한 Querystring 시나리오-를 사용 하 여 URL과 쿼리 문자열 하지에서 가져온이 "페이지" 매개 변수는 이제 점을 제외 하 고 정확 하 게 동일한 index () 코드를 사용할 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-149">We can use the exact same Index() code we had before with our Querystring scenario – except now our "page" parameter will come from the URL and not the querystring:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

<span data-ttu-id="deb1c-150">이제 응용 프로그램을 실행 하 고 입력 했습니다 */Dinners* 처음 10 개 향후 dinners를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-150">And now when we run the application and type in */Dinners* we'll see the first 10 upcoming dinners:</span></span>

![](implement-efficient-data-paging/_static/image3.png)

<span data-ttu-id="deb1c-151">에서는 입력 */Dinners/Page/1* dinners의 다음 페이지를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-151">And when we type in */Dinners/Page/1* we'll see the next page of dinners:</span></span>

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a><span data-ttu-id="deb1c-152">페이지 탐색 UI를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-152">Adding page navigation UI</span></span>

<span data-ttu-id="deb1c-153">페이징 시나리오를 완료 하기 위한 마지막 단계 Dinner 데이터를 쉽게 건너뛸 수 있도록 하려면 우리의 보기 템플릿에서 "다음" 및 "이전" 탐색 UI를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-153">The last step to complete our paging scenario will be to implement "next" and "previous" navigation UI within our view template to enable users to easily skip over the Dinner data.</span></span>

<span data-ttu-id="deb1c-154">이 올바르게 구현 하기에서는 알아야 Dinners 총 데이터베이스에도로 변환 됩니다이 데이터 페이지 수는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-154">To implement this correctly, we'll need to know the total number of Dinners in the database, as well as how many pages of data this translates to.</span></span> <span data-ttu-id="deb1c-155">그런 다음 시작 또는 데이터의 끝에서 현재 요청 된 "페이지" 값이 있는지 여부를 계산 및 표시 하거나 숨기기 "이전" 및 "다음" UI를 적절 하 게 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-155">We'll then need to calculate whether the currently requested "page" value is at the beginning or end of the data, and show or hide the "previous" and "next" UI accordingly.</span></span> <span data-ttu-id="deb1c-156">index () 작업 메서드 내에서이 논리를 구현할 수 것입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-156">We could implement this logic within our Index() action method.</span></span> <span data-ttu-id="deb1c-157">또는 더 재사용 가능한 방식으로이 논리를 캡슐화 하는 프로젝트에는 도우미 클래스를 추가할 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-157">Alternatively we can add a helper class to our project that encapsulates this logic in a more re-usable way.</span></span>

<span data-ttu-id="deb1c-158">목록에서 파생 되는 간단한 "PaginatedList" 도우미 클래스는 다음과 같습니다&lt;T&gt; 에 기본 제공 컬렉션 클래스는.NET Framework입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-158">Below is a simple "PaginatedList" helper class that derives from the List&lt;T&gt; collection class built-into the .NET Framework.</span></span> <span data-ttu-id="deb1c-159">페이지를 매기 IQueryable 데이터의 모든 시퀀스는 다시 사용할 수 있는 컬렉션 클래스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-159">It implements a re-usable collection class that can be used to paginate any sequence of IQueryable data.</span></span> <span data-ttu-id="deb1c-160">NerdDinner 응용 프로그램에서 마련 IQueryable을 통해 작동&lt;Dinner&gt; 하지만 결과 쉽게 사용 될 수 IQueryable&lt;제품&gt; 또는 IQueryable&lt;고객&gt;다른 응용 프로그램 시나리오에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-160">In our NerdDinner application we'll have it work over IQueryable&lt;Dinner&gt; results, but it could just as easily be used against IQueryable&lt;Product&gt; or IQueryable&lt;Customer&gt; results in other application scenarios:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

<span data-ttu-id="deb1c-161">계산 하는 방법을 위의 예제와 다음 속성을 노출 "PageIndex", "PageSize", "TotalCount" 및 "TotalPages"입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-161">Notice above how it calculates and then exposes properties like "PageIndex", "PageSize", "TotalCount", and "TotalPages".</span></span> <span data-ttu-id="deb1c-162">또한 다음 컬렉션에 있는 데이터 페이지의 시작 또는 원래 시퀀스의 끝에 있는지 여부를 나타내는 두 개의 도우미 속성 "HasPreviousPage" 및 "HasNextPage"를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-162">It also then exposes two helper properties "HasPreviousPage" and "HasNextPage" that indicate whether the page of data in the collection is at the beginning or end of the original sequence.</span></span> <span data-ttu-id="deb1c-163">위의 코드는 두 SQL 쿼리 실행 수 Dinner 개체의 총 수를 검색할 첫 번째를 하면 (이 개체를 반환 하지 않습니다 – 대신 정수를 반환 하는 "SELECT COUNT" 문을 수행) 및 두 번째의 행만 검색 현재 페이지 데이터에 대 한 데이터베이스에서 필요한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-163">The above code will cause two SQL queries to be run - the first to retrieve the count of the total number of Dinner objects (this doesn't return the objects – rather it performs a "SELECT COUNT" statement that returns an integer), and the second to retrieve just the rows of data we need from our database for the current page of data.</span></span>

<span data-ttu-id="deb1c-164">DinnersController.Index() 도우미 메서드는 PaginatedList를 만들려면 다음 업데이트할 수 있습니다&lt;Dinner&gt; 우리의 DinnerRepository.FindUpcomingDinners()에서 결과 보기 템플릿은로 전달 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-164">We can then update our DinnersController.Index() helper method to create a PaginatedList&lt;Dinner&gt; from our DinnerRepository.FindUpcomingDinners() result, and pass it to our view template:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

<span data-ttu-id="deb1c-165">그런 다음 ViewPage 상속할 \Views\Dinners\Index.aspx 보기 템플릿을 업데이트할 수 있습니다&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt; &gt; ViewPage 대신&lt;IEnumerable&lt;Dinner&gt;&gt;를 표시 하거나 숨기려면 다음 및 이전 탐색 UI 보기-템플릿의 맨 아래에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-165">We can then update the \Views\Dinners\Index.aspx view template to inherit from ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt;&gt; instead of ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;, and then add the following code to the bottom of our view-template to show or hide next and previous navigation UI:</span></span>

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

<span data-ttu-id="deb1c-166">어떻게 Html.RouteLink() 도우미 메서드를 사용 하 여는 하이퍼링크를 생성은에서는 위의 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-166">Notice above how we are using the Html.RouteLink() helper method to generate our hyperlinks.</span></span> <span data-ttu-id="deb1c-167">이 메서드는 이전에 사용한 Html.ActionLink() 도우미 메서드는 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-167">This method is similar to the Html.ActionLink() helper method we've used previously.</span></span> <span data-ttu-id="deb1c-168">차이점 "UpcomingDinners" 라우팅 Global.asax 파일 내에서 설정 하는 규칙을 사용 하 여 URL을 생성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-168">The difference is that we are generating the URL using the "UpcomingDinners" routing rule we setup within our Global.asax file.</span></span> <span data-ttu-id="deb1c-169">형식이 index () 동작 메서드에 Url 생성 하는 것이 이렇게: */Dinners/페이지 / {page}* – {page} 값이 제공 하 고 위에서 현재 PageIndex 기반 변수 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-169">This ensures that we'll generate URLs to our Index() action method that have the format: */Dinners/Page/{page}* – where the {page} value is a variable we are providing above based on the current PageIndex.</span></span>

<span data-ttu-id="deb1c-170">고 이제 응용 프로그램 실행 하면 다시 한 번에 10 dinners 브라우저에서:</span><span class="sxs-lookup"><span data-stu-id="deb1c-170">And now when we run our application again we'll see 10 dinners at a time in our browser:</span></span>

![](implement-efficient-data-paging/_static/image5.png)

<span data-ttu-id="deb1c-171">이 밖에도 &lt; &lt; &lt; 하 고 &gt; &gt; &gt; 탐색 전달 건너뛰고 이전 버전과 사용 하 여 데이터를 통해 엔진 액세스할 수 있는 Url을 검색할 수 있는 페이지의 맨 아래에 UI:</span><span class="sxs-lookup"><span data-stu-id="deb1c-171">We also have &lt;&lt;&lt; and &gt;&gt;&gt; navigation UI at the bottom of the page that allows us to skip forwards and backwards over our data using search engine accessible URLs:</span></span>

![](implement-efficient-data-paging/_static/image6.png)

| <span data-ttu-id="deb1c-172">**쪽 항목: IQueryable의 의미를 이해 하&lt;T&gt;**</span><span class="sxs-lookup"><span data-stu-id="deb1c-172">**Side Topic: Understanding the implications of IQueryable&lt;T&gt;**</span></span> |
| --- |
| <span data-ttu-id="deb1c-173">IQueryable&lt;T&gt; 다양 한 흥미로운 지연 된 실행 시나리오를 사용 하도록 설정 하는 매우 강력한 기능입니다 (페이징 및 컴퍼지션과 같은 쿼리 기반).</span><span class="sxs-lookup"><span data-stu-id="deb1c-173">IQueryable&lt;T&gt; is a very powerful feature that enables a variety of interesting deferred execution scenarios (like paging and composition based queries).</span></span> <span data-ttu-id="deb1c-174">으로 모든 강력한 기능을 사용 하 여 사용 방법에 주의를 기울여야을 남용 되지 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-174">As with all powerful features, you want to be careful with how you use it and make sure it is not abused.</span></span> <span data-ttu-id="deb1c-175">해당 반환 IQueryable을 인식 해야&lt;T&gt; 리포지토리의 결과 호출 코드에 연결 된 연산자 메서드에 추가 하 고 따라서 ultimate 쿼리 실행에 참여를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-175">It is important to recognize that returning an IQueryable&lt;T&gt; result from your repository enables calling code to append on chained operator methods to it, and so participate in the ultimate query execution.</span></span> <span data-ttu-id="deb1c-176">호출 코드가이 기능을 제공 하지 않을 경우 반환 해야 다시 IList&lt;T&gt; 또는 IEnumerable&lt;T&gt; 이미 실행 하는 쿼리 결과 포함 하는 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="deb1c-176">If you do not want to provide calling code this ability, then you should return back IList&lt;T&gt; or IEnumerable&lt;T&gt; results - which contain the results of a query that has already executed.</span></span> <span data-ttu-id="deb1c-177">페이지 매김 시나리오의 실제 데이터 페이지 매김 논리 호출 되는 리포지토리 메서드로 푸시 해야 함.</span><span class="sxs-lookup"><span data-stu-id="deb1c-177">For pagination scenarios this would require you to push the actual data pagination logic into the repository method being called.</span></span> <span data-ttu-id="deb1c-178">이 시나리오에서는 FindUpcomingDinners() finder 메서드 시그니처에서 PaginatedList를 반환 하거나 업데이트 될 수 있습니다: PaginatedList&lt; Dinner&gt; FindUpcomingDinners (pageIndex int, int pageSize) {} 반환 IList 또는 &lt;Dinner&gt;, "totalCount" out 매개 변수를 사용 하 여 Dinners의 총 개수를 반환 합니다: IList&lt;Dinner&gt; FindUpcomingDinners (pageIndex int, int totalCount 아웃 int pageSize) {}</span><span class="sxs-lookup"><span data-stu-id="deb1c-178">In this scenario we might update our FindUpcomingDinners() finder method to have a signature that either returned a PaginatedList: PaginatedList&lt; Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize) { } Or return back an IList&lt;Dinner&gt;, and use a "totalCount" out param to return the total count of Dinners: IList&lt;Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize, out int totalCount) { }</span></span> |

### <a name="next-step"></a><span data-ttu-id="deb1c-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="deb1c-179">Next Step</span></span>

<span data-ttu-id="deb1c-180">이제 살펴보겠습니다 응용 프로그램에 대 한 인증 및 권한 부여 지원을 추가할 수 있습니다 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="deb1c-180">Let's now look at how we can add authentication and authorization support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="deb1c-181">[이전](re-use-ui-using-master-pages-and-partials.md)
> [다음](secure-applications-using-authentication-and-authorization.md)</span><span class="sxs-lookup"><span data-stu-id="deb1c-181">[Previous](re-use-ui-using-master-pages-and-partials.md)
[Next](secure-applications-using-authentication-and-authorization.md)</span></span>
