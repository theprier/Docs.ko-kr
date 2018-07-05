# <a name="add-search-to-an-aspnet-core-razor-pages-app"></a><span data-ttu-id="cc595-101">ASP.NET Core Razor Pages 앱에 검색 추가</span><span class="sxs-lookup"><span data-stu-id="cc595-101">Add search to an ASP.NET Core Razor Pages app</span></span>

<span data-ttu-id="cc595-102">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="cc595-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="cc595-103">이 문서에서 *장르* 또는 *이름*으로 동영상을 검색할 수 있는 인덱스 페이지에 검색 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-103">In this document, search capability is added to the Index page that enables searching movies by *genre* or *name*.</span></span>

<span data-ttu-id="cc595-104">인덱스 페이지의 `OnGetAsync` 메서드를 다음 코드로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-104">Update the Index page's `OnGetAsync` method with the following code:</span></span>

[!code-cshtml[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/_ViewStart.cshtml)]

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_1stSearch)]

<span data-ttu-id="cc595-105">`OnGetAsync` 메서드의 첫 번째 줄은 동영상을 선택하는 [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) 쿼리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-105">The first line of the `OnGetAsync` method creates a [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) query to select the movies:</span></span>

```csharp
var movies = from m in _context.Movie
             select m;
```

<span data-ttu-id="cc595-106">쿼리는 이 시점에서*만* 정의되며 데이터베이스에 대해 실행되지 **않았습니다**.</span><span class="sxs-lookup"><span data-stu-id="cc595-106">The query is *only* defined at this point, it has **not** been run against the database.</span></span>

<span data-ttu-id="cc595-107">`searchString` 매개 변수에 문자열이 포함되는 경우 동영상 쿼리는 검색 문자열에 대해 필터링하도록 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-107">If the `searchString` parameter contains a string, the movies query is modified to filter on the search string:</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SearchNull)]

<span data-ttu-id="cc595-108">`s => s.Title.Contains()` 코드는 [람다 식](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)입니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-108">The `s => s.Title.Contains()` code is a [Lambda Expression](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span></span> <span data-ttu-id="cc595-109">람다 식은 메서드 기반 [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) 쿼리에서 [Where](/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) 메서드 또는 `Contains`(위의 코드에서 사용됨)와 같은 표준 쿼리 연산자 메서드의 인수로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-109">Lambdas are used in method-based [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) queries as arguments to standard query operator methods such as the [Where](/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) method or `Contains` (used in the preceding code).</span></span> <span data-ttu-id="cc595-110">LINQ 쿼리는 정의될 때 또는 메서드(예: `Where`, `Contains` 또는 `OrderBy`)를 호출하여 수정될 때 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-110">LINQ queries are not executed when they're defined or when they're modified by calling a method (such as `Where`, `Contains`  or `OrderBy`).</span></span> <span data-ttu-id="cc595-111">대신 쿼리 실행이 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-111">Rather, query execution is deferred.</span></span> <span data-ttu-id="cc595-112">즉, 실현된 값이 반복되거나 `ToListAsync` 메서드가 호출될 때까지 식의 계산이 지연되는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-112">That means the evaluation of an expression is delayed until its realized value is iterated over or the `ToListAsync` method is called.</span></span> <span data-ttu-id="cc595-113">자세한 내용은 [쿼리 실행](/dotnet/framework/data/adonet/ef/language-reference/query-execution)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc595-113">See [Query Execution](/dotnet/framework/data/adonet/ef/language-reference/query-execution) for more information.</span></span>

<span data-ttu-id="cc595-114">**참고:** [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) 메서드는 C# 코드에서가 아닌 데이터베이스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-114">**Note:** The [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) method is run on the database, not in the C# code.</span></span> <span data-ttu-id="cc595-115">쿼리에 대한 대/소문자 구분은 데이터베이스 및 데이터 정렬에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-115">The case sensitivity on the query depends on the database and the collation.</span></span> <span data-ttu-id="cc595-116">SQL Server에서 `Contains`는 대/소문자를 구분하는 [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql)로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-116">On SQL Server, `Contains` maps to [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql), which is case insensitive.</span></span> <span data-ttu-id="cc595-117">SQLite에서 기본 데이터 정렬과 함께 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-117">In SQLite, with the default collation, it's case sensitive.</span></span>

<span data-ttu-id="cc595-118">Movies 페이지로 이동하고 `?searchString=Ghost`와 같은 쿼리 문자열을 URL에 추가합니다(예: `http://localhost:5000/Movies?searchString=Ghost`).</span><span class="sxs-lookup"><span data-stu-id="cc595-118">Navigate to the Movies page and append a query string such as `?searchString=Ghost` to the URL (for example, `http://localhost:5000/Movies?searchString=Ghost`).</span></span> <span data-ttu-id="cc595-119">필터링된 동영상이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-119">The filtered movies are displayed.</span></span>

![인덱스 보기](../../tutorials/razor-pages/search/_static/ghost.png)

<span data-ttu-id="cc595-121">다음 경로 템플릿이 인덱스 페이지에 추가되는 경우 검색 문자열이 URL 세그먼트로 전달될 수 있습니다(예: `http://localhost:5000/Movies/ghost`).</span><span class="sxs-lookup"><span data-stu-id="cc595-121">If the following route template is added to the Index page, the search string can be passed as a URL segment (for example, `http://localhost:5000/Movies/ghost`).</span></span>

```cshtml
@page "{searchString?}"
```

<span data-ttu-id="cc595-122">이전 경로 제약 조건을 통해 쿼리 문자열 값 대신 경로 데이터(URL 세그먼트)로 제목을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-122">The preceding route constraint allows searching the title as route data (a URL segment) instead of as a query string value.</span></span>  <span data-ttu-id="cc595-123">`"{searchString?}"`에서 `?`는 선택적 경로 매개 변수임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-123">The `?` in `"{searchString?}"` means this is an optional route parameter.</span></span>

![Url에 추가된 단어 ghost와 두 개의 동영상, Ghostbusters 및 Ghostbusters 2의 반환된 동영상 목록이 있는 인덱스 보기](../../tutorials/razor-pages/search/_static/g2.png)

<span data-ttu-id="cc595-125">그러나 사용자가 동영상 검색을 위해 URL을 수정하는 것을 기대할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-125">However, you can't expect users to modify the URL to search for a movie.</span></span> <span data-ttu-id="cc595-126">이 단계에서 동영상을 필터링하도록 UI가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-126">In this step, UI is added to filter movies.</span></span> <span data-ttu-id="cc595-127">경로 제약 조건 `"{searchString?}"`을 추가한 경우 이를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-127">If you added the route constraint `"{searchString?}"`, remove it.</span></span>

<span data-ttu-id="cc595-128">*Pages/Movies/Index.cshtml* 파일을 열고 다음 코드에서 강조 표시된 `<form>` 표시를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-128">Open the *Pages/Movies/Index.cshtml* file, and add the `<form>` markup highlighted in the following code:</span></span>

[!code-cshtml[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index2.cshtml?highlight=14-19&range=1-22)]

<span data-ttu-id="cc595-129">HTML `<form>` 태그는 [양식 태그 도우미](xref:mvc/views/working-with-forms#the-form-tag-helper)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-129">The HTML `<form>` tag uses the [Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper).</span></span> <span data-ttu-id="cc595-130">양식이 제출되면 필터 문자열이 *Pages/Movies/Index* 페이지로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-130">When the form is submitted, the filter string is sent to the *Pages/Movies/Index* page.</span></span> <span data-ttu-id="cc595-131">변경 내용을 저장하고 필터를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-131">Save the changes and test the filter.</span></span>

![제목 필터 텍스트 상자에 단어 ghost를 입력하여 인덱스 보기](../../tutorials/razor-pages/search/_static/filter.png)

## <a name="search-by-genre"></a><span data-ttu-id="cc595-133">장르별 검색</span><span class="sxs-lookup"><span data-stu-id="cc595-133">Search by genre</span></span>

<span data-ttu-id="cc595-134">*Pages/Movies/Index.cshtml.cs*에 강조 표시된 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-134">Add the following highlighted properties to *Pages/Movies/Index.cshtml.cs*:</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_newProps&highlight=11-999)]

<span data-ttu-id="cc595-135">`SelectList Genres`는 장르 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-135">The `SelectList Genres` contains the list of genres.</span></span> <span data-ttu-id="cc595-136">이를 통해 사용자는 목록에서 장르를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-136">This allows the user to select a genre from the list.</span></span>

<span data-ttu-id="cc595-137">`MovieGenre` 속성은 사용자가 선택하는 특정 장르를 포함합니다(예: "서부 영화").</span><span class="sxs-lookup"><span data-stu-id="cc595-137">The `MovieGenre` property contains the specific genre the user selects (for example, "Western").</span></span>

<span data-ttu-id="cc595-138">`OnGetAsync` 메서드를 다음 코드로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-138">Update the `OnGetAsync` method with the following code:</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SearchGenre)]

<span data-ttu-id="cc595-139">다음 코드는 데이터베이스에서 모든 장르를 검색하는 LINQ 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-139">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_LINQ)]

<span data-ttu-id="cc595-140">장르의 `SelectList`는 고유 장르를 프로젝션함으로써 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-140">The `SelectList` of genres is created by projecting the distinct genres.</span></span>

<!-- BUG in OPS
Tag snippet_selectlist's start line '75' should be less than end line '29' when resolving "[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SelectList)]"

There's no start line.

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SelectList)]
-->

```csharp
Genres = new SelectList(await genreQuery.Distinct().ToListAsync());
```

### <a name="adding-search-by-genre"></a><span data-ttu-id="cc595-141">장르별 검색 추가</span><span class="sxs-lookup"><span data-stu-id="cc595-141">Adding search by genre</span></span>

<span data-ttu-id="cc595-142">다음과 같이 *Index.cshtml*을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-142">Update *Index.cshtml* as follows:</span></span>

[!code-cshtml[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/IndexFormGenreNoRating.cshtml?highlight=16-18&range=1-26)]

<span data-ttu-id="cc595-143">장르별, 동영상 제목별 및 둘 다로 검색하여 앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cc595-143">Test the app by searching by genre, by movie title, and by both.</span></span>
