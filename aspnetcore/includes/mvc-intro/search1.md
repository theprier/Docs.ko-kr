# <a name="add-search-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="5a1dd-101">ASP.NET Core MVC 앱에 검색 추가</span><span class="sxs-lookup"><span data-stu-id="5a1dd-101">Add search to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="5a1dd-102">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="5a1dd-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="5a1dd-103">이 섹션에서는 *장르* 또는 *이름*별로 영화를 검색할 수 있는 `Index` 작업 메서드에 검색 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-103">In this section you add search capability to the `Index` action method that lets you search movies by *genre* or *name*.</span></span>

<span data-ttu-id="5a1dd-104">`Index` 메서드를 다음 코드로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-104">Update the `Index` method with the following code:</span></span>
<!--
[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Shared/_Layout.cshtml?highlight=7,31)]
-->

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_1stSearch)]

<span data-ttu-id="5a1dd-105">`Index` 작업 메서드의 첫 번째 줄은 영화를 선택하는 [LINQ](/dotnet/standard/using-linq) 쿼리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-105">The first line of the `Index` action method creates a [LINQ](/dotnet/standard/using-linq) query to select the movies:</span></span>

```csharp
var movies = from m in _context.Movie
             select m;
```

<span data-ttu-id="5a1dd-106">쿼리는 이 시점에서*만* 정의되며 데이터베이스에 대해 실행되지 **않았습니다**.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-106">The query is *only* defined at this point, it has **not** been run against the database.</span></span>

<span data-ttu-id="5a1dd-107">`searchString` 매개 변수에 문자열이 포함되는 경우 영화 쿼리는 검색 문자열의 값에 대해 필터링하도록 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-107">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_SearchNull2)]

<span data-ttu-id="5a1dd-108">위의 `s => s.Title.Contains()` 코드는 [람다 식](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)입니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-108">The `s => s.Title.Contains()` code above is a [Lambda Expression](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span></span> <span data-ttu-id="5a1dd-109">람다 식은 메서드 기반 [LINQ](/dotnet/standard/using-linq) 쿼리에서 [Where](/dotnet/api/system.linq.enumerable.where) 메서드 또는 `Contains`(위의 코드에서 사용됨)와 같은 표준 쿼리 연산자 메서드의 인수로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-109">Lambdas are used in method-based [LINQ](/dotnet/standard/using-linq) queries as arguments to standard query operator methods such as the [Where](/dotnet/api/system.linq.enumerable.where) method or `Contains` (used in the code above).</span></span> <span data-ttu-id="5a1dd-110">LINQ 쿼리는 정의될 때 또는 메서드(예: `Where`, `Contains` 또는 `OrderBy`)를 호출하여 수정될 때 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-110">LINQ queries are not executed when they're defined or when they're modified by calling a method such as `Where`, `Contains`  or `OrderBy`.</span></span> <span data-ttu-id="5a1dd-111">대신 쿼리 실행이 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-111">Rather, query execution is deferred.</span></span>  <span data-ttu-id="5a1dd-112">즉, 실제로 실현된 값이 반복되거나 `ToListAsync` 메서드가 호출될 때까지 식의 계산이 지연되는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-112">That means that the evaluation of an expression is delayed until its realized value is actually iterated over or the `ToListAsync` method is called.</span></span> <span data-ttu-id="5a1dd-113">지연된 쿼리 실행에 대한 자세한 내용은 [쿼리 실행](/dotnet/framework/data/adonet/ef/language-reference/query-execution)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-113">For more information about deferred query execution, see [Query Execution](/dotnet/framework/data/adonet/ef/language-reference/query-execution).</span></span>

<span data-ttu-id="5a1dd-114">참고: [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) 메서드는 위에 표시된 C# 코드에서가 아닌 데이터베이스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-114">Note: The [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) method is run on the database, not in the c# code shown above.</span></span> <span data-ttu-id="5a1dd-115">쿼리에 대한 대/소문자 구분은 데이터베이스 및 데이터 정렬에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-115">The case sensitivity on the query depends on the database and the collation.</span></span> <span data-ttu-id="5a1dd-116">SQL Server에서 [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains)는 대/소문자를 구분하는 [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql)로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-116">On SQL Server, [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) maps to [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql), which is case insensitive.</span></span> <span data-ttu-id="5a1dd-117">SQLlite에서 기본 데이터 정렬과 함께 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-117">In SQLlite, with the default collation, it's case sensitive.</span></span>

<span data-ttu-id="5a1dd-118">`/Movies/Index`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-118">Navigate to `/Movies/Index`.</span></span> <span data-ttu-id="5a1dd-119">쿼리 문자열(예: `?searchString=Ghost`)을 URL에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-119">Append a query string such as `?searchString=Ghost` to the URL.</span></span> <span data-ttu-id="5a1dd-120">필터링된 영화가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-120">The filtered movies are displayed.</span></span>

![인덱스 보기](~/tutorials/first-mvc-app/search/_static/ghost.png)

<span data-ttu-id="5a1dd-122">`id`라는 매개 변수를 포함하도록 `Index` 메서드의 서명을 변경하는 경우 `id` 매개 변수는 *Startup.cs*에서 설정된 기본 경로의 선택적 `{id}` 자리 표시자와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1dd-122">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the optional `{id}` placeholder for the default routes set in *Startup.cs*.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?highlight=5&name=snippet_1)]
