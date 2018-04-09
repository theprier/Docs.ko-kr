---
uid: mvc/overview/getting-started/introduction/adding-search
title: 검색 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/22/2015
ms.topic: article
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: 8afa72d4dbc4695e7d26c6ef4052be08a7c69080
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="search"></a><span data-ttu-id="cc533-102">검색</span><span class="sxs-lookup"><span data-stu-id="cc533-102">Search</span></span>
====================
<span data-ttu-id="cc533-103">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="cc533-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

## <a name="adding-a-search-method-and-search-view"></a><span data-ttu-id="cc533-104">검색 방법 및 검색 뷰를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-104">Adding a Search Method and Search View</span></span>

<span data-ttu-id="cc533-105">이 섹션에서는 검색 기능을 추가 `Index` 작업 메서드를 사용 하면 영화 장르 또는 이름으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-105">In this section you'll add search capability to the `Index` action method that lets you search movies by genre or name.</span></span>

## <a name="updating-the-index-form"></a><span data-ttu-id="cc533-106">인덱스 형식 업데이트</span><span class="sxs-lookup"><span data-stu-id="cc533-106">Updating the Index Form</span></span>

<span data-ttu-id="cc533-107">업데이트 하 여 시작 된 `Index` 동작 메서드를 기존 `MoviesController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-107">Start by updating the `Index` action method to the existing `MoviesController` class.</span></span> <span data-ttu-id="cc533-108">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-108">Here's the code:</span></span>

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

<span data-ttu-id="cc533-109">첫 번째 줄은 `Index` 메서드 다음 항목을 만듭니다 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 쿼리는 영화를 선택 하려면:</span><span class="sxs-lookup"><span data-stu-id="cc533-109">The first line of the `Index` method creates the following [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) query to select the movies:</span></span>

[!code-csharp[Main](adding-search/samples/sample2.cs)]

<span data-ttu-id="cc533-110">쿼리가 시점에서 정의 되었지만 아직 데이터베이스에 대해 실행 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-110">The query is defined at this point, but hasn't yet been run against the database.</span></span>

<span data-ttu-id="cc533-111">경우는 `searchString` 매개 변수는 문자열이 포함 된, 다음 코드를 사용 하 여 검색 문자열을 값으로 필터링 하려면 영화 쿼리가 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-111">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string, using the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample3.cs)]

<span data-ttu-id="cc533-112">위의 `s => s.Title` 코드는 [람다 식](https://msdn.microsoft.com/library/bb397687.aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-112">The `s => s.Title` code above is a [Lambda Expression](https://msdn.microsoft.com/library/bb397687.aspx).</span></span> <span data-ttu-id="cc533-113">람다 식은 메서드 기반에 사용 되 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 와 같은 표준 쿼리 연산자 메서드의 인수로 쿼리는 [여기서](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) 위의 코드에서 사용 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-113">Lambdas are used in method-based [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) queries as arguments to standard query operator methods such as the [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) method used in the above code.</span></span> <span data-ttu-id="cc533-114">정의 된 또는 같은 메서드를 호출 하 여 수정 된 경우에 LINQ 쿼리 실행 되지 않습니다 `Where` 또는 `OrderBy`합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-114">LINQ queries are not executed when they are defined or when they are modified by calling a method such as `Where` or `OrderBy`.</span></span> <span data-ttu-id="cc533-115">대신, 쿼리 실행이 지연, 즉, 실제로 실현된 값 반복 될 때까지 식의 계산이 지연 되는지 또는 [ `ToList` ](https://msdn.microsoft.com/library/bb342261.aspx) 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-115">Instead, query execution is deferred, which means that the evaluation of an expression is delayed until its realized value is actually iterated over or the [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) method is called.</span></span> <span data-ttu-id="cc533-116">에 `Search` 샘플에서는 쿼리가에서 실행 되는 *Index.cshtml* 보기.</span><span class="sxs-lookup"><span data-stu-id="cc533-116">In the `Search` sample, the query is executed in the *Index.cshtml* view.</span></span> <span data-ttu-id="cc533-117">지연된 쿼리 실행에 대한 자세한 내용은 [쿼리 실행](https://msdn.microsoft.com/library/bb738633.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc533-117">For more information about deferred query execution, see [Query Execution](https://msdn.microsoft.com/library/bb738633.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="cc533-118">[Contains](https://msdn.microsoft.com/library/bb155125.aspx) 데이터베이스 하지는 위의 c# 코드에서 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-118">The [Contains](https://msdn.microsoft.com/library/bb155125.aspx) method is run on the database, not the c# code above.</span></span> <span data-ttu-id="cc533-119">다음은 데이터베이스에서 [Contains](https://msdn.microsoft.com/library/bb155125.aspx) 매핑됩니다 [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), 대/소문자 구분 되 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-119">On the database, [Contains](https://msdn.microsoft.com/library/bb155125.aspx) maps to [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), which is case insensitive.</span></span>

<span data-ttu-id="cc533-120">업데이트할 수 이제는 `Index` 사용자에 게 폼을 표시 하는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-120">Now you can update the `Index` view that will display the form to the user.</span></span>

<span data-ttu-id="cc533-121">응용 프로그램을 실행 하 고 이동 */영화/인덱스*합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-121">Run the application and navigate to */Movies/Index*.</span></span> <span data-ttu-id="cc533-122">쿼리 문자열(예: `?searchString=ghost`)을 URL에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-122">Append a query string such as `?searchString=ghost` to the URL.</span></span> <span data-ttu-id="cc533-123">필터링된 동영상이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-123">The filtered movies are displayed.</span></span>

![SearchQryStr](adding-search/_static/image1.png)

<span data-ttu-id="cc533-125">시그니처를 변경 하는 경우는 `Index` 메서드 라는 매개 변수를 사용 하려면 `id`, `id` 매개 변수는 일치는 `{id}` 기본값에 대 한 자리 표시자 경로 집합에는 *앱\_시작 RouteConfig.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-125">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the `{id}` placeholder for the default routes set in the *App\_Start\RouteConfig.cs* file.</span></span>

[!code-json[Main](adding-search/samples/sample4.json)]

<span data-ttu-id="cc533-126">원래 `Index` 메서드는 다음과 같습니다::</span><span class="sxs-lookup"><span data-stu-id="cc533-126">The original `Index` method looks like this::</span></span>

[!code-csharp[Main](adding-search/samples/sample5.cs)]

<span data-ttu-id="cc533-127">수정 된 `Index` 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-127">The modified `Index` method would look as follows:</span></span>

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

<span data-ttu-id="cc533-128">이제 쿼리 문자열 값이 아닌 경로 데이터(URL 세그먼트)로 검색 제목을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-128">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![](adding-search/_static/image2.png)

<span data-ttu-id="cc533-129">그러나 사용자가 영화를 검색하려고 할 때마다 URL을 수정하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-129">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="cc533-130">수 있도록 UI를 추가 합니다 있습니다 지금 동영상을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-130">So now you you'll add UI to help them filter movies.</span></span> <span data-ttu-id="cc533-131">시그니처를 변경 하는 경우는 `Index` 경로 바인딩된 ID 매개 변수를 전달 하는 방법을 테스트 하는 메서드 변경 다시 있도록 프로그램 `Index` 메서드 라는 문자열 매개 변수 `searchString`:</span><span class="sxs-lookup"><span data-stu-id="cc533-131">If you changed the signature of the `Index` method to test how to pass the route-bound ID parameter, change it back so that your `Index` method takes a string parameter named `searchString`:</span></span>

[!code-csharp[Main](adding-search/samples/sample7.cs)]

<span data-ttu-id="cc533-132">열기는 *Views\Movies\Index.cshtml* 파일을 선택한 후 바로 `@Html.ActionLink("Create New", "Create")`, 폼 태그 아래에 강조 표시에 추가:</span><span class="sxs-lookup"><span data-stu-id="cc533-132">Open the *Views\Movies\Index.cshtml* file, and just after `@Html.ActionLink("Create New", "Create")`, add the form markup highlighted below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

<span data-ttu-id="cc533-133">`Html.BeginForm` 도우미 만듭니다 여 `<form>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-133">The `Html.BeginForm` helper creates an opening `<form>` tag.</span></span> <span data-ttu-id="cc533-134">`Html.BeginForm` 도우미 하면 사용자가 클릭 하 여 폼을 제출 하는 경우 자신에 게 게시 하려면 폼의 **필터** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-134">The `Html.BeginForm` helper causes the form to post to itself when the user submits the form by clicking the **Filter** button.</span></span>

<span data-ttu-id="cc533-135">Visual Studio 2013에는 표시 및 보기 파일을 편집 하는 경우 좋은 개선을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-135">Visual Studio 2013 has a nice improvement when displaying and editing View files.</span></span> <span data-ttu-id="cc533-136">를 실행 하면 응용 프로그램 보기 파일 열기 Visual Studio 2013 보기 표시 하려면 올바른 컨트롤러 동작 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-136">When you run the application with a view file open, Visual Studio 2013 invokes the correct controller action method to display the view.</span></span>

![](adding-search/_static/image3.png)

<span data-ttu-id="cc533-137">인덱스 뷰를 포함 (위의 그림에 표시 된) 하는 대로 Visual Studio에서 열기, 응용 프로그램을 실행 하 고 동영상에 대 한 검색을 시도 하려면 Ctr F5 또는 f5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-137">With the Index view open in Visual Studio (as shown in the image above), tap Ctr F5 or F5 to run the application and then try searching for a movie.</span></span>

![](adding-search/_static/image4.png)

<span data-ttu-id="cc533-138">없는 `HttpPost` 오버 로드는 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="cc533-138">There's no `HttpPost` overload of the `Index` method.</span></span> <span data-ttu-id="cc533-139">필요 없는, 메서드는 응용 프로그램의 상태를 변경 되지 않습니다 때문에 데이터를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-139">You don't need it, because the method isn't changing the state of the application, just filtering data.</span></span>

<span data-ttu-id="cc533-140">다음 `HttpPost Index` 메서드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-140">You could add the following `HttpPost Index` method.</span></span> <span data-ttu-id="cc533-141">작업 호출자는 일치 하는 경우에 `HttpPost Index` 메서드, 및 `HttpPost Index` 메서드 아래 이미지에 나와 있는 것 처럼 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-141">In that case, the action invoker would match the `HttpPost Index` method, and the `HttpPost Index` method would run as shown in the image below.</span></span>

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

<span data-ttu-id="cc533-143">그러나 이 `HttpPost` 버전의 `Index` 메서드를 추가하는 경우에도 이를 모두 구현하는 방법은 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-143">However, even if you add this `HttpPost` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="cc533-144">특정 검색을 책갈피로 설정하거나 동일하게 필터링된 영화 목록을 보기 위해 클릭할 수 있는 링크를 친구에게 보내려고 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-144">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="cc533-145">HTTP POST에 대 한 URL를 요청 하는 GET 요청 (localhost:xxxxx/영화/인덱스)에 대 한 URL과 동일-URL 자체에 검색 정보가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-145">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL itself.</span></span> <span data-ttu-id="cc533-146">오른쪽 지금 검색 문자열 정보는 전송 서버에 양식 필드 값으로.</span><span class="sxs-lookup"><span data-stu-id="cc533-146">Right now, the search string information is sent to the server as a form field value.</span></span> <span data-ttu-id="cc533-147">즉, 책갈피를 URL에는 친구에 게 보내고 해당 검색 정보를 캡처할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-147">This means you can't capture that search information to bookmark or send to friends in a URL.</span></span>

<span data-ttu-id="cc533-148">솔루션의 오버 로드를 사용 하는 것 `BeginForm` 에 POST 요청 URL에 검색 정보를 추가 하도록와으로 라우팅할 수를 지정 하는 `HttpGet` 버전의는 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="cc533-148">The solution is to use an overload of `BeginForm` that specifies that the POST request should add the search information to the URL and that it should be routed to the `HttpGet` version of the `Index` method.</span></span> <span data-ttu-id="cc533-149">매개 변수가 없는 기존 항목 바꾸기 `BeginForm` 메서드를 다음 태그로:</span><span class="sxs-lookup"><span data-stu-id="cc533-149">Replace the existing parameterless `BeginForm` method with the following markup:</span></span>

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

<span data-ttu-id="cc533-151">이제 검색을 제출할 때 URL 검색 쿼리 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-151">Now when you submit a search, the URL contains a search query string.</span></span> <span data-ttu-id="cc533-152">`HttpPost Index` 메서드가 있는 경우에도 검색은 `HttpGet Index` 작업 메서드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-152">Searching will also go to the `HttpGet Index` action method, even if you have a `HttpPost Index` method.</span></span>

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a><span data-ttu-id="cc533-154">장르별로 검색 추가</span><span class="sxs-lookup"><span data-stu-id="cc533-154">Adding Search by Genre</span></span>

<span data-ttu-id="cc533-155">추가한 경우는 `HttpPost` 버전의는 `Index` 메서드를 지금 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-155">If you added the `HttpPost` version of the `Index` method, delete it now.</span></span>

<span data-ttu-id="cc533-156">다음으로, 사용자가 영화가 장르별로 검색할 수 있도록 하는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-156">Next, you'll add a feature to let users search for movies by genre.</span></span> <span data-ttu-id="cc533-157">`Index` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-157">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample11.cs)]

<span data-ttu-id="cc533-158">이 버전의는 `Index` 메서드는 추가 매개 변수, 즉 `movieGenre`합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-158">This version of the `Index` method takes an additional parameter, namely `movieGenre`.</span></span> <span data-ttu-id="cc533-159">코드의 처음 몇 줄 만들기는 `List` 데이터베이스에서 영화 장르를 보유 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-159">The first few lines of code create a `List` object to hold movie genres from the database.</span></span>

<span data-ttu-id="cc533-160">다음 코드는 데이터베이스에서 모든 장르를 검색하는 LINQ 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-160">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[Main](adding-search/samples/sample12.cs)]

<span data-ttu-id="cc533-161">코드를 사용 하 여는 `AddRange` 메서드는 제네릭의 `List` 모든 고유 장르 목록에 추가할 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-161">The code uses the `AddRange` method of the generic `List` collection to add all the distinct genres to the list.</span></span> <span data-ttu-id="cc533-162">(없이 `Distinct` 한정자를 중복 장르는 추가-샘플에 두 번 코미디는 추가 하는 예를 들어).</span><span class="sxs-lookup"><span data-stu-id="cc533-162">(Without the `Distinct` modifier, duplicate genres would be added — for example, comedy would be added twice in our sample).</span></span> <span data-ttu-id="cc533-163">코드에는 다음에 장르 목록을 저장 된 `ViewBag.MovieGenre` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-163">The code then stores the list of genres in the `ViewBag.MovieGenre` object.</span></span> <span data-ttu-id="cc533-164">범주 데이터 (이러한 동영상 장르의)으로 저장 한 [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) 개체는 `ViewBag`, MVC 응용 프로그램에 대 한 일반적인 방법은 드롭다운 목록 상자에서 범주 데이터에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-164">Storing category data (such a movie genre's) as a [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) object in a `ViewBag`, then accessing the category data in a dropdown list box is a typical approach for MVC applications.</span></span>

<span data-ttu-id="cc533-165">다음 코드를 확인 하는 방법을 보여 줍니다는 `movieGenre` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-165">The following code shows how to check the `movieGenre` parameter.</span></span> <span data-ttu-id="cc533-166">비어 있지 않으면 코드를 추가로 지정된 장르에 선택 된 동영상을 제한 하려면 영화 쿼리를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-166">If it's not empty, the code further constrains the movies query to limit the selected movies to the specified genre.</span></span>

[!code-csharp[Main](adding-search/samples/sample13.cs)]

<span data-ttu-id="cc533-167">동영상 목록을 반복 될 때까지 쿼리가 데이터베이스에서 실행 되지 앞서 설명한 것 처럼 (후 보기에서 발생 하는 `Index` 작업 메서드가 반환).</span><span class="sxs-lookup"><span data-stu-id="cc533-167">As stated previously, the query is not run on the data base until the movie list is iterated over (which happens in the View, after the `Index` action method returns).</span></span>

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a><span data-ttu-id="cc533-168">장르별로 검색을 지 원하는 인덱스 보기에 태그 추가</span><span class="sxs-lookup"><span data-stu-id="cc533-168">Adding Markup to the Index View to Support Search by Genre</span></span>

<span data-ttu-id="cc533-169">추가 `Html.DropDownList` 도우미에는 *Views\Movies\Index.cshtml* 파일, 바로 앞의 `TextBox` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-169">Add an `Html.DropDownList` helper to the *Views\Movies\Index.cshtml* file, just before the `TextBox` helper.</span></span> <span data-ttu-id="cc533-170">완성 된 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-170">The completed markup is shown below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

<span data-ttu-id="cc533-171">다음 코드:</span><span class="sxs-lookup"><span data-stu-id="cc533-171">In the following code:</span></span>

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

<span data-ttu-id="cc533-172">에 대 한 키를 제공 하는 "MovieGenre" 매개 변수는 `DropDownList` 찾으려고 도우미는 `IEnumerable<SelectListItem>` 에 `ViewBag`합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-172">The parameter "MovieGenre" provides the key for the `DropDownList` helper to find a `IEnumerable<SelectListItem>` in the `ViewBag`.</span></span> <span data-ttu-id="cc533-173">`ViewBag` 작업 메서드에서 채워졌습니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-173">The `ViewBag` was populated in the action method:</span></span>

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

<span data-ttu-id="cc533-174">옵션 레이블을 제공 "All" 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-174">The parameter "All" provides an option label.</span></span> <span data-ttu-id="cc533-175">브라우저에서 여기에서 선택한 항목을 검사 하는 경우 해당 "value" 특성이 비어 있음을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-175">If you inspect that choice in your browser, you'll see that its "value" attribute is empty.</span></span> <span data-ttu-id="cc533-176">Controller만 필터링 하므로 `if` 문자열은 `null` 또는 empty 인에 대 한 빈 값을 제출 `movieGenre` 모든 장르를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-176">Since our controller only filters `if` the string is not `null` or empty, submitting an empty value for `movieGenre` shows all genres.</span></span>

<span data-ttu-id="cc533-177">또한 기본적으로 선택 하는 옵션을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-177">You can also set an option to be selected by default.</span></span> <span data-ttu-id="cc533-178">컨트롤러에 코드를 변경할 것을 기본 옵션으로 "코미디"을 원하는 경우 같이:</span><span class="sxs-lookup"><span data-stu-id="cc533-178">If you wanted "Comedy" as your default option, you would change the code in the Controller like so:</span></span>

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

<span data-ttu-id="cc533-179">응용 프로그램을 실행 하 고 찾아보기 */영화/인덱스*합니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-179">Run the application and browse to */Movies/Index*.</span></span> <span data-ttu-id="cc533-180">장르, 영화 제목 및 두 조건으로 검색을 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cc533-180">Try a search by genre, by movie name, and by both criteria.</span></span>

![](adding-search/_static/image8.png)

<span data-ttu-id="cc533-181">이 섹션에서는 검색 동작 메서드와 영화 제목 및 장르 하 여 검색할 수 있도록 하는 뷰를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-181">In this section you created a search action method and view that let users search by movie title and genre.</span></span> <span data-ttu-id="cc533-182">다음 섹션에서 살펴보겠습니다 속성을 추가 하는 방법의 `Movie` 모델 및 테스트 데이터베이스에서 자동으로 만듭니다는 이니셜라이저를 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cc533-182">In the next section, you'll look at how to add a property to the `Movie` model and how to add an initializer that will automatically create a test database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cc533-183">[이전](examining-the-edit-methods-and-edit-view.md)
> [다음](adding-a-new-field.md)</span><span class="sxs-lookup"><span data-stu-id="cc533-183">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-a-new-field.md)</span></span>
