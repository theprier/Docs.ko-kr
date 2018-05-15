::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="f9dc8-101">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController2.cs?name=snippet_todo1)]</span><span class="sxs-lookup"><span data-stu-id="f9dc8-101">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController2.cs?name=snippet_todo1)]</span></span>

<span data-ttu-id="f9dc8-102">앞의 코드는 메서드 없이 API 컨트롤러 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-102">The preceding code defines an API controller class without methods.</span></span> <span data-ttu-id="f9dc8-103">다음 섹션에서는 API를 구현하기 위해 메서드가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-103">In the next sections, methods are added to implement the API.</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="f9dc8-104">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController2.cs?name=snippet_todo1)]</span><span class="sxs-lookup"><span data-stu-id="f9dc8-104">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController2.cs?name=snippet_todo1)]</span></span>

<span data-ttu-id="f9dc8-105">앞의 코드는 메서드 없이 API 컨트롤러 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-105">The preceding code defines an API controller class without methods.</span></span> <span data-ttu-id="f9dc8-106">다음 섹션에서는 API를 구현하기 위해 메서드가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-106">In the next sections, methods are added to implement the API.</span></span> <span data-ttu-id="f9dc8-107">클래스에는 편리한 기능을 사용하기 위해 `[ApiController]` 특성이 주석으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-107">The class is annotated with an `[ApiController]` attribute to enable some convenient features.</span></span> <span data-ttu-id="f9dc8-108">이 특성으로 인해 활성화되는 기능에 대한 자세한 내용은 [ApiControllerAttribute로 클래스에 주석 달기](xref:web-api/index#annotate-class-with-apicontrollerattribute)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-108">For information on features enabled by the attribute, see [Annotate class with ApiControllerAttribute](xref:web-api/index#annotate-class-with-apicontrollerattribute).</span></span>
::: moniker-end

<span data-ttu-id="f9dc8-109">컨트롤러의 생성자는 [종속성 주입](xref:fundamentals/dependency-injection)을 통해 컨트롤러에 데이터베이스 컨텍스트(`TodoContext`)를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-109">The controller's constructor uses [Dependency Injection](xref:fundamentals/dependency-injection) to inject the database context (`TodoContext`) into the controller.</span></span> <span data-ttu-id="f9dc8-110">컨트롤러의 [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) 메서드 각각에서 데이터베이스 컨텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-110">The database context is used in each of the [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) methods in the controller.</span></span> <span data-ttu-id="f9dc8-111">항목이 없는 경우 생성자는 메모리 내 데이터베이스에 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-111">The constructor adds an item to the in-memory database if one doesn't exist.</span></span>

## <a name="get-to-do-items"></a><span data-ttu-id="f9dc8-112">할 일 항목 가져오기</span><span class="sxs-lookup"><span data-stu-id="f9dc8-112">Get to-do items</span></span>

<span data-ttu-id="f9dc8-113">할 일 항목을 가져오려면 다음 메서드를 `TodoController` 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-113">To get to-do items, add the following methods to the `TodoController` class:</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="f9dc8-114">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetAll)]</span><span class="sxs-lookup"><span data-stu-id="f9dc8-114">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetAll)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="f9dc8-115">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetAll)]</span><span class="sxs-lookup"><span data-stu-id="f9dc8-115">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetAll)]</span></span>
::: moniker-end

<span data-ttu-id="f9dc8-116">다음과 같은 메서드는 두 개의 GET 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-116">These methods implement the two GET methods:</span></span>

* `GET /api/todo`
* `GET /api/todo/{id}`

<span data-ttu-id="f9dc8-117">다음은 `GetAll` 메서드에 대한 샘플 HTTP 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-117">Here's a sample HTTP response for the `GetAll` method:</span></span>

```json
[
  {
    "id": 1,
    "name": "Item1",
    "isComplete": false
  }
]
```

<span data-ttu-id="f9dc8-118">자습서의 뒷부분에서는 HTTP 응답을 [Postman](https://www.getpostman.com/) 또는 [curl](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/curl.1.html)로 볼 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-118">Later in the tutorial, I'll show how the HTTP response can be viewed with [Postman](https://www.getpostman.com/) or [curl](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/curl.1.html).</span></span>

### <a name="routing-and-url-paths"></a><span data-ttu-id="f9dc8-119">라우팅 및 URL 경로</span><span class="sxs-lookup"><span data-stu-id="f9dc8-119">Routing and URL paths</span></span>

<span data-ttu-id="f9dc8-120">`[HttpGet]` 특성은 HTTP GET 요청에 응답하는 메서드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-120">The `[HttpGet]` attribute denotes a method that responds to an HTTP GET request.</span></span> <span data-ttu-id="f9dc8-121">각 방법에 대한 URL 경로는 다음과 같이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-121">The URL path for each method is constructed as follows:</span></span>

* <span data-ttu-id="f9dc8-122">컨트롤러의 `Route` 특성에서 템플릿 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-122">Take the template string in the controller's `Route` attribute:</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="f9dc8-123">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=TodoController&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="f9dc8-123">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=TodoController&highlight=3)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="f9dc8-124">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=TodoController&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="f9dc8-124">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=TodoController&highlight=3)]</span></span>
::: moniker-end

* <span data-ttu-id="f9dc8-125">`[controller]`를 컨트롤러의 이름으로 바꿉니다. 즉, 컨트롤러 클래스 이름에서 "Controller" 접미사를 뺀 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-125">Replace `[controller]` with the name of the controller, which is the controller class name minus the "Controller" suffix.</span></span> <span data-ttu-id="f9dc8-126">이 샘플의 경우 컨트롤러 클래스 이름은 **Todo**Controller이고 루트 이름은 "todo"입니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-126">For this sample, the controller class name is **Todo**Controller and the root name is "todo".</span></span> <span data-ttu-id="f9dc8-127">ASP.NET Core [라우팅](xref:mvc/controllers/routing)은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-127">ASP.NET Core [routing](xref:mvc/controllers/routing) is case insensitive.</span></span>
* <span data-ttu-id="f9dc8-128">`[HttpGet]` 특성에 경로 템플릿(예: `[HttpGet("/products")]`)이 있는 경우 경로에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-128">If the `[HttpGet]` attribute has a route template (such as `[HttpGet("/products")]`, append that to the path.</span></span> <span data-ttu-id="f9dc8-129">이 샘플은 템플릿을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-129">This sample doesn't use a template.</span></span> <span data-ttu-id="f9dc8-130">자세한 내용은 [Http[동사] 특성을 사용한 특성 라우팅](xref:mvc/controllers/routing#attribute-routing-with-httpverb-attributes)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-130">For more information, see [Attribute routing with Http[Verb] attributes](xref:mvc/controllers/routing#attribute-routing-with-httpverb-attributes).</span></span>

<span data-ttu-id="f9dc8-131">다음 `GetById` 메서드에서 `"{id}"`는 할 일 항목의 고유 식별자에 대한 자리 표시자 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-131">In the following `GetById` method, `"{id}"` is a placeholder variable for the unique identifier of the to-do item.</span></span> <span data-ttu-id="f9dc8-132">`GetById`가 호출되면 URL의 `"{id}"` 값을 메서드의 `id` 매개 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-132">When `GetById` is invoked, it assigns the value of `"{id}"` in the URL to the method's `id` parameter.</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="f9dc8-133">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]</span><span class="sxs-lookup"><span data-stu-id="f9dc8-133">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="f9dc8-134">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]</span><span class="sxs-lookup"><span data-stu-id="f9dc8-134">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]</span></span>
::: moniker-end

<span data-ttu-id="f9dc8-135">`Name = "GetTodo"`는 명명된 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-135">`Name = "GetTodo"` creates a named route.</span></span> <span data-ttu-id="f9dc8-136">명명된 경로:</span><span class="sxs-lookup"><span data-stu-id="f9dc8-136">Named routes:</span></span>

* <span data-ttu-id="f9dc8-137">앱에서 해당 경로 이름을 사용하여 HTTP 링크를 만들도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-137">Enable the app to create an HTTP link using the route name.</span></span>
* <span data-ttu-id="f9dc8-138">자습서의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-138">Are explained later in the tutorial.</span></span>

### <a name="return-values"></a><span data-ttu-id="f9dc8-139">반환 값</span><span class="sxs-lookup"><span data-stu-id="f9dc8-139">Return values</span></span>

<span data-ttu-id="f9dc8-140">`GetAll` 메서드는 `TodoItem` 개체의 컬렉션을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-140">The `GetAll` method returns a collection of `TodoItem` objects.</span></span> <span data-ttu-id="f9dc8-141">MVC는 자동으로 [JSON](https://www.json.org/)에 개체를 직렬화하고 JSON을 응답 메시지의 본문에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-141">MVC automatically serializes the object to [JSON](https://www.json.org/) and writes the JSON into the body of the response message.</span></span> <span data-ttu-id="f9dc8-142">이 메서드의 응답 코드는 200이며 처리되지 않은 예외가 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-142">The response code for this method is 200, assuming there are no unhandled exceptions.</span></span> <span data-ttu-id="f9dc8-143">처리되지 않은 예외는 5xx 오류로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-143">Unhandled exceptions are translated into 5xx errors.</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="f9dc8-144">반면, `GetById` 메서드는 다양한 반환 형식을 나타내는 보다 일반적인 [IActionResult 형식](xref:web-api/action-return-types#iactionresult-type)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-144">In contrast, the `GetById` method returns the more general [IActionResult type](xref:web-api/action-return-types#iactionresult-type), which represents a wide range of return types.</span></span> <span data-ttu-id="f9dc8-145">`GetById`에는 두 개의 다른 반환 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-145">`GetById` has two different return types:</span></span>

* <span data-ttu-id="f9dc8-146">요청된 ID와 일치하는 항목이 없는 경우 메서드가 404 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-146">If no item matches the requested ID, the method returns a 404 error.</span></span> <span data-ttu-id="f9dc8-147">[NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound)를 반환하면 HTTP 404 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-147">Returning [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) returns an HTTP 404 response.</span></span>
* <span data-ttu-id="f9dc8-148">그렇지 않으면 메서드가 JSON 응답 본문에서 200을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-148">Otherwise, the method returns 200 with a JSON response body.</span></span> <span data-ttu-id="f9dc8-149">[확인](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.ok)을 반환하면 HTTP 200 응답이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-149">Returning [Ok](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.ok) results in an HTTP 200 response.</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="f9dc8-150">반면, `GetById` 메서드는 다양한 반환 형식을 나타내는 [ActionResult\<T>형식](xref:web-api/action-return-types#actionresultt-type)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-150">In contrast, the `GetById` method returns the [ActionResult\<T> type](xref:web-api/action-return-types#actionresultt-type), which represents a wide range of return types.</span></span> <span data-ttu-id="f9dc8-151">`GetById`에는 두 개의 다른 반환 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-151">`GetById` has two different return types:</span></span>

* <span data-ttu-id="f9dc8-152">요청된 ID와 일치하는 항목이 없는 경우 메서드가 404 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-152">If no item matches the requested ID, the method returns a 404 error.</span></span> <span data-ttu-id="f9dc8-153">[NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound)를 반환하면 HTTP 404 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-153">Returning [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) returns an HTTP 404 response.</span></span>
* <span data-ttu-id="f9dc8-154">그렇지 않으면 메서드가 JSON 응답 본문에서 200을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-154">Otherwise, the method returns 200 with a JSON response body.</span></span> <span data-ttu-id="f9dc8-155">`item`을 반환하면 HTTP 200 응답이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dc8-155">Returning `item` results in an HTTP 200 response.</span></span>
::: moniker-end