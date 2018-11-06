::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController2.cs?name=snippet_todo1)]

<span data-ttu-id="01a8c-101">앞의 코드는 메서드 없이 API 컨트롤러 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-101">The preceding code defines an API controller class without methods.</span></span> <span data-ttu-id="01a8c-102">다음 섹션에서는 API를 구현하기 위해 메서드가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-102">In the next sections, methods are added to implement the API.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController2.cs?name=snippet_todo1)]

<span data-ttu-id="01a8c-103">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="01a8c-103">The preceding code:</span></span>

* <span data-ttu-id="01a8c-104">메서드 없이 API 컨트롤러 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-104">Defines an API controller class without methods.</span></span>
* <span data-ttu-id="01a8c-105">`TodoItems`가 비어 있는 경우 새 Todo 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-105">Creates a new Todo item when `TodoItems` is empty.</span></span> <span data-ttu-id="01a8c-106">`TodoItems`가 비어 있는 경우 생성자가 새 항목을 만들기 때문에 모든 Todo 항목을 삭제할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-106">You won't be able to delete all the Todo items because the constructor creates a new one if `TodoItems` is empty.</span></span>

<span data-ttu-id="01a8c-107">다음 섹션에서는 API를 구현하기 위해 메서드가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-107">In the next sections, methods are added to implement the API.</span></span> <span data-ttu-id="01a8c-108">클래스에는 편리한 기능을 사용하기 위해 `[ApiController]` 특성이 주석으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-108">The class is annotated with an `[ApiController]` attribute to enable some convenient features.</span></span> <span data-ttu-id="01a8c-109">이 특성으로 인해 활성화되는 기능에 대한 자세한 내용은 [ApiControllerAttribute로 주석 달기](xref:web-api/index#annotation-with-apicontrollerattribute)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01a8c-109">For information on features enabled by the attribute, see [Annotation with ApiControllerAttribute](xref:web-api/index#annotation-with-apicontrollerattribute).</span></span>

::: moniker-end

<span data-ttu-id="01a8c-110">컨트롤러의 생성자는 [종속성 주입](xref:fundamentals/dependency-injection)을 통해 컨트롤러에 데이터베이스 컨텍스트(`TodoContext`)를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-110">The controller's constructor uses [Dependency Injection](xref:fundamentals/dependency-injection) to inject the database context (`TodoContext`) into the controller.</span></span> <span data-ttu-id="01a8c-111">컨트롤러의 [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) 메서드 각각에서 데이터베이스 컨텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-111">The database context is used in each of the [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) methods in the controller.</span></span> <span data-ttu-id="01a8c-112">항목이 없는 경우 생성자는 메모리 내 데이터베이스에 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-112">The constructor adds an item to the in-memory database if one doesn't exist.</span></span>

## <a name="get-to-do-items"></a><span data-ttu-id="01a8c-113">할 일 항목 가져오기</span><span class="sxs-lookup"><span data-stu-id="01a8c-113">Get to-do items</span></span>

<span data-ttu-id="01a8c-114">할 일 항목을 가져오려면 다음 메서드를 `TodoController` 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-114">To get to-do items, add the following methods to the `TodoController` class:</span></span>

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetAll)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetAll)]

::: moniker-end

<span data-ttu-id="01a8c-115">다음과 같은 메서드는 두 개의 GET 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-115">These methods implement the two GET methods:</span></span>

* `GET /api/todo`
* `GET /api/todo/{id}`

<span data-ttu-id="01a8c-116">다음은 `GetAll` 메서드에 대한 샘플 HTTP 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-116">Here's a sample HTTP response for the `GetAll` method:</span></span>

```json
[
  {
    "id": 1,
    "name": "Item1",
    "isComplete": false
  }
]
```

<span data-ttu-id="01a8c-117">자습서의 뒷부분에서는 HTTP 응답을 [Postman](https://www.getpostman.com/) 또는 [curl](https://curl.haxx.se/docs/manpage.html)로 볼 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-117">Later in the tutorial, I'll show how the HTTP response can be viewed with [Postman](https://www.getpostman.com/) or [curl](https://curl.haxx.se/docs/manpage.html).</span></span>

### <a name="routing-and-url-paths"></a><span data-ttu-id="01a8c-118">라우팅 및 URL 경로</span><span class="sxs-lookup"><span data-stu-id="01a8c-118">Routing and URL paths</span></span>

<span data-ttu-id="01a8c-119">`[HttpGet]` 특성은 HTTP GET 요청에 응답하는 메서드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-119">The `[HttpGet]` attribute denotes a method that responds to an HTTP GET request.</span></span> <span data-ttu-id="01a8c-120">각 방법에 대한 URL 경로는 다음과 같이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-120">The URL path for each method is constructed as follows:</span></span>

* <span data-ttu-id="01a8c-121">컨트롤러의 `Route` 특성에서 템플릿 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-121">Take the template string in the controller's `Route` attribute:</span></span>

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=TodoController&highlight=3)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=TodoController&highlight=3)]

::: moniker-end

* <span data-ttu-id="01a8c-122">`[controller]`를 컨트롤러의 이름으로 바꿉니다. 즉, 컨트롤러 클래스 이름에서 "Controller" 접미사를 뺀 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-122">Replace `[controller]` with the name of the controller, which is the controller class name minus the "Controller" suffix.</span></span> <span data-ttu-id="01a8c-123">이 샘플의 경우 컨트롤러 클래스 이름은 **Todo**Controller이고 루트 이름은 "todo"입니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-123">For this sample, the controller class name is **Todo**Controller and the root name is "todo".</span></span> <span data-ttu-id="01a8c-124">ASP.NET Core [라우팅](xref:mvc/controllers/routing)은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-124">ASP.NET Core [routing](xref:mvc/controllers/routing) is case insensitive.</span></span>
* <span data-ttu-id="01a8c-125">`[HttpGet]` 특성에 경로 템플릿(예: `[HttpGet("/products")]`)이 있는 경우 경로에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-125">If the `[HttpGet]` attribute has a route template (such as `[HttpGet("/products")]`, append that to the path.</span></span> <span data-ttu-id="01a8c-126">이 샘플은 템플릿을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-126">This sample doesn't use a template.</span></span> <span data-ttu-id="01a8c-127">자세한 내용은 [Http[동사] 특성을 사용한 특성 라우팅](xref:mvc/controllers/routing#attribute-routing-with-httpverb-attributes)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01a8c-127">For more information, see [Attribute routing with Http[Verb] attributes](xref:mvc/controllers/routing#attribute-routing-with-httpverb-attributes).</span></span>

<span data-ttu-id="01a8c-128">다음 `GetById` 메서드에서 `"{id}"`는 할 일 항목의 고유 식별자에 대한 자리 표시자 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-128">In the following `GetById` method, `"{id}"` is a placeholder variable for the unique identifier of the to-do item.</span></span> <span data-ttu-id="01a8c-129">`GetById`가 호출되면 URL의 `"{id}"` 값을 메서드의 `id` 매개 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-129">When `GetById` is invoked, it assigns the value of `"{id}"` in the URL to the method's `id` parameter.</span></span>

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]

::: moniker-end

<span data-ttu-id="01a8c-130">`Name = "GetTodo"`는 명명된 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-130">`Name = "GetTodo"` creates a named route.</span></span> <span data-ttu-id="01a8c-131">명명된 경로:</span><span class="sxs-lookup"><span data-stu-id="01a8c-131">Named routes:</span></span>

* <span data-ttu-id="01a8c-132">앱에서 해당 경로 이름을 사용하여 HTTP 링크를 만들도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-132">Enable the app to create an HTTP link using the route name.</span></span>
* <span data-ttu-id="01a8c-133">자습서의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-133">Are explained later in the tutorial.</span></span>

### <a name="return-values"></a><span data-ttu-id="01a8c-134">반환 값</span><span class="sxs-lookup"><span data-stu-id="01a8c-134">Return values</span></span>

<span data-ttu-id="01a8c-135">`GetAll` 메서드는 `TodoItem` 개체의 컬렉션을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-135">The `GetAll` method returns a collection of `TodoItem` objects.</span></span> <span data-ttu-id="01a8c-136">MVC는 자동으로 [JSON](https://www.json.org/)에 개체를 직렬화하고 JSON을 응답 메시지의 본문에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-136">MVC automatically serializes the object to [JSON](https://www.json.org/) and writes the JSON into the body of the response message.</span></span> <span data-ttu-id="01a8c-137">이 메서드의 응답 코드는 200이며 처리되지 않은 예외가 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-137">The response code for this method is 200, assuming there are no unhandled exceptions.</span></span> <span data-ttu-id="01a8c-138">처리되지 않은 예외는 5xx 오류로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-138">Unhandled exceptions are translated into 5xx errors.</span></span>

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="01a8c-139">반면, `GetById` 메서드는 다양한 반환 형식을 나타내는 보다 일반적인 [IActionResult 형식](xref:web-api/action-return-types#iactionresult-type)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-139">In contrast, the `GetById` method returns the more general [IActionResult type](xref:web-api/action-return-types#iactionresult-type), which represents a wide range of return types.</span></span> <span data-ttu-id="01a8c-140">`GetById`에는 두 개의 다른 반환 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-140">`GetById` has two different return types:</span></span>

* <span data-ttu-id="01a8c-141">요청된 ID와 일치하는 항목이 없는 경우 메서드가 404 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-141">If no item matches the requested ID, the method returns a 404 error.</span></span> <span data-ttu-id="01a8c-142">[NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound)를 반환하면 HTTP 404 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-142">Returning [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) returns an HTTP 404 response.</span></span>
* <span data-ttu-id="01a8c-143">그렇지 않으면 메서드가 JSON 응답 본문에서 200을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-143">Otherwise, the method returns 200 with a JSON response body.</span></span> <span data-ttu-id="01a8c-144">[확인](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.ok)을 반환하면 HTTP 200 응답이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-144">Returning [Ok](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.ok) results in an HTTP 200 response.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="01a8c-145">반면, `GetById` 메서드는 다양한 반환 형식을 나타내는 [ActionResult\<T>형식](xref:web-api/action-return-types#actionresultt-type)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-145">In contrast, the `GetById` method returns the [ActionResult\<T> type](xref:web-api/action-return-types#actionresultt-type), which represents a wide range of return types.</span></span> <span data-ttu-id="01a8c-146">`GetById`에는 두 개의 다른 반환 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-146">`GetById` has two different return types:</span></span>

* <span data-ttu-id="01a8c-147">요청된 ID와 일치하는 항목이 없는 경우 메서드가 404 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-147">If no item matches the requested ID, the method returns a 404 error.</span></span> <span data-ttu-id="01a8c-148">[NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound)를 반환하면 HTTP 404 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-148">Returning [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) returns an HTTP 404 response.</span></span>
* <span data-ttu-id="01a8c-149">그렇지 않으면 메서드가 JSON 응답 본문에서 200을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-149">Otherwise, the method returns 200 with a JSON response body.</span></span> <span data-ttu-id="01a8c-150">`item`을 반환하면 HTTP 200 응답이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="01a8c-150">Returning `item` results in an HTTP 200 response.</span></span>

::: moniker-end
