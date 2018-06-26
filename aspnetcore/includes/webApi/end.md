## <a name="implement-the-other-crud-operations"></a><span data-ttu-id="def15-101">기타 CRUD 작업 구현</span><span class="sxs-lookup"><span data-stu-id="def15-101">Implement the other CRUD operations</span></span>

<span data-ttu-id="def15-102">다음 섹션에서 `Create`, `Update` 및 `Delete` 메서드가 컨트롤러에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="def15-102">In the following sections, `Create`, `Update`, and `Delete` methods are added to the controller.</span></span>

### <a name="create"></a><span data-ttu-id="def15-103">만들기</span><span class="sxs-lookup"><span data-stu-id="def15-103">Create</span></span>

<span data-ttu-id="def15-104">다음 `Create` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-104">Add the following `Create` method:</span></span>

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

<span data-ttu-id="def15-105">이전 코드는 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 특성으로 표시되는 HTTP POST 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="def15-105">The preceding code is an HTTP POST method, as indicated by the [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) attribute.</span></span> <span data-ttu-id="def15-106">[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) 특성은 HTTP 요청 본문에서 할 일 항목 값을 가져오도록 MVC에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-106">The [[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) attribute tells MVC to get the value of the to-do item from the body of the HTTP request.</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

<span data-ttu-id="def15-107">이전 코드는 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 특성으로 표시되는 HTTP POST 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="def15-107">The preceding code is an HTTP POST method, as indicated by the [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) attribute.</span></span> <span data-ttu-id="def15-108">MVC는 HTTP 요청 본문에서 할 일 항목 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="def15-108">MVC gets the value of the to-do item from the body of the HTTP request.</span></span>
::: moniker-end

<span data-ttu-id="def15-109">`CreatedAtRoute` 메서드는 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-109">The `CreatedAtRoute` method:</span></span>

* <span data-ttu-id="def15-110">201 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-110">Returns a 201 response.</span></span> <span data-ttu-id="def15-111">HTTP 201은 서버에서 새 리소스를 만드는 HTTP POST 메서드의 표준 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="def15-111">HTTP 201 is the standard response for an HTTP POST method that creates a new resource on the server.</span></span>
* <span data-ttu-id="def15-112">응답에 대한 위치 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-112">Adds a Location header to the response.</span></span> <span data-ttu-id="def15-113">위치 헤더는 새로 만들어진 할 일 항목의 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-113">The Location header specifies the URI of the newly created to-do item.</span></span> <span data-ttu-id="def15-114">[10.2.2 201 Created](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)(10.2.2 201 생성됨)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="def15-114">See [10.2.2 201 Created](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).</span></span>
* <span data-ttu-id="def15-115">“GetTodo”라는 경로를 사용하여 URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="def15-115">Uses the "GetTodo" named route to create the URL.</span></span> <span data-ttu-id="def15-116">“GetTodo”라는 경로는 `GetById`에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="def15-116">The "GetTodo" named route is defined in `GetById`:</span></span>

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]
::: moniker-end

### <a name="use-postman-to-send-a-create-request"></a><span data-ttu-id="def15-117">Postman을 사용하여 만들기 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="def15-117">Use Postman to send a Create request</span></span>

* <span data-ttu-id="def15-118">응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-118">Start the app.</span></span>
* <span data-ttu-id="def15-119">Postman을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="def15-119">Open Postman.</span></span>

![Postman 콘솔](../../tutorials/first-web-api/_static/pmc.png)

* <span data-ttu-id="def15-121">localhost URL에서 포트 번호를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-121">Update the port number in the localhost URL.</span></span>
* <span data-ttu-id="def15-122">HTTP 메서드를 *POST*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-122">Set the HTTP method to *POST*.</span></span>
* <span data-ttu-id="def15-123">**본문** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-123">Click the **Body** tab.</span></span>
* <span data-ttu-id="def15-124">**원시** 라디오 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-124">Select the **raw** radio button.</span></span>
* <span data-ttu-id="def15-125">유형을 *JSON(application/json)* 으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-125">Set the type to *JSON (application/json)*.</span></span>
* <span data-ttu-id="def15-126">다음 JSON과 같은 할 일 항목을 사용하여 요청 본문을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-126">Enter a request body with a to-do item resembling the following JSON:</span></span>

```json
{
  "name":"walk dog",
  "isComplete":true
}
```

* <span data-ttu-id="def15-127">**보내기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-127">Click the **Send** button.</span></span>

::: moniker range=">= aspnetcore-2.1"
> [!TIP]
> <span data-ttu-id="def15-128">**보내기**를 클릭한 후 응답이 표시되지 않는 경우 **SSL 인증 유효성 검사** 옵션을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="def15-128">If no response displays after clicking **Send**, disable the **SSL certification verification** option.</span></span> <span data-ttu-id="def15-129">이 옵션은 **파일** > **설정** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def15-129">This is found under **File** > **Settings**.</span></span> <span data-ttu-id="def15-130">설정을 사용하지 못하게 한 후 **보내기** 단추를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-130">Click the **Send** button again after disabling the setting.</span></span>
::: moniker-end

<span data-ttu-id="def15-131">**응답** 창에서 **헤더** 탭을 클릭하고 **위치** 헤더 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-131">Click the **Headers** tab in the **Response** pane and copy the **Location** header value:</span></span>

![Postman 콘솔의 헤더 탭](../../tutorials/first-web-api/_static/pmc2.png)

<span data-ttu-id="def15-133">위치 헤더 URI를 사용하여 새 항목에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def15-133">The Location header URI can be used to access the new item.</span></span>

### <a name="update"></a><span data-ttu-id="def15-134">업데이트</span><span class="sxs-lookup"><span data-stu-id="def15-134">Update</span></span>

<span data-ttu-id="def15-135">다음 `Update` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-135">Add the following `Update` method:</span></span>

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]
::: moniker-end

<span data-ttu-id="def15-136">HTTP PUT을 사용하는 것을 제외하고 `Update`는 `Create`와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-136">`Update` is similar to `Create`, except it uses HTTP PUT.</span></span> <span data-ttu-id="def15-137">응답은 [204(콘텐츠 없음)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)입니다.</span><span class="sxs-lookup"><span data-stu-id="def15-137">The response is [204 (No Content)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).</span></span> <span data-ttu-id="def15-138">HTTP 사양에 따라 PUT 요청의 경우 클라이언트는 델타만이 아니라 전체 업데이트된 엔터티를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-138">According to the HTTP specification, a PUT request requires the client to send the entire updated entity, not just the deltas.</span></span> <span data-ttu-id="def15-139">부분 업데이트를 지원하려면 HTTP PATCH를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-139">To support partial updates, use HTTP PATCH.</span></span>

<span data-ttu-id="def15-140">Postman을 사용하여 할 일 항목의 이름을 "walk cat"으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-140">Use Postman to update the to-do item's name to "walk cat":</span></span>

![204(콘텐츠 없음) 응답을 보여주는 Postman 콘솔](../../tutorials/first-web-api/_static/pmcput.png)

### <a name="delete"></a><span data-ttu-id="def15-142">삭제</span><span class="sxs-lookup"><span data-stu-id="def15-142">Delete</span></span>

<span data-ttu-id="def15-143">다음 `Delete` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-143">Add the following `Delete` method:</span></span>

[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Delete)]

<span data-ttu-id="def15-144">`Delete` 응답은 [204(콘텐츠 없음)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)입니다.</span><span class="sxs-lookup"><span data-stu-id="def15-144">The `Delete` response is [204 (No Content)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).</span></span>

<span data-ttu-id="def15-145">Postman을 사용하여 할 일 항목을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="def15-145">Use Postman to delete the to-do item:</span></span>

![204(콘텐츠 없음) 응답을 보여주는 Postman 콘솔](../../tutorials/first-web-api/_static/pmd.png)
