## <a name="implement-the-other-crud-operations"></a>기타 CRUD 작업 구현

다음 섹션에서 `Create`, `Update` 및 `Delete` 메서드가 컨트롤러에 추가됩니다.

### <a name="create"></a>만들기

다음 `Create` 메서드를 추가합니다.

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

이전 코드는 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 특성으로 표시되는 HTTP POST 메서드입니다. [[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) 특성은 HTTP 요청 본문에서 할 일 항목 값을 가져오도록 MVC에 지시합니다.

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

이전 코드는 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 특성으로 표시되는 HTTP POST 메서드입니다. MVC는 HTTP 요청 본문에서 할 일 항목 값을 가져옵니다.

::: moniker-end

`CreatedAtRoute` 메서드는 다음과 같은 작업을 수행합니다.

* 201 응답을 반환합니다. HTTP 201은 서버에서 새 리소스를 만드는 HTTP POST 메서드의 표준 응답입니다.
* 응답에 대한 위치 헤더를 추가합니다. 위치 헤더는 새로 만들어진 할 일 항목의 URI를 지정합니다. [10.2.2 201 Created](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)(10.2.2 201 생성됨)를 참조하세요.
* “GetTodo”라는 경로를 사용하여 URL을 만듭니다. “GetTodo”라는 경로는 `GetById`에 정의됩니다.

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]

::: moniker-end

### <a name="use-postman-to-send-a-create-request"></a>Postman을 사용하여 만들기 요청 보내기

* 응용 프로그램을 시작합니다.
* Postman을 엽니다.

![Postman 콘솔](../../tutorials/first-web-api/_static/pmc.png)

* localhost URL에서 포트 번호를 업데이트합니다.
* HTTP 메서드를 *POST*로 설정합니다.
* **본문** 탭을 클릭합니다.
* **원시** 라디오 단추를 선택합니다.
* 유형을 *JSON(application/json)* 으로 설정합니다.
* 다음 JSON과 같은 할 일 항목을 사용하여 요청 본문을 입력합니다.

```json
{
  "name":"walk dog",
  "isComplete":true
}
```

* **보내기** 단추를 클릭합니다.

::: moniker range=">= aspnetcore-2.1"

> [!TIP]
> **보내기**를 클릭한 후 응답이 표시되지 않는 경우 **SSL 인증 유효성 검사** 옵션을 사용하지 않습니다. 이 옵션은 **파일** > **설정** 아래에 있습니다. 설정을 사용하지 못하게 한 후 **보내기** 단추를 다시 클릭합니다.

::: moniker-end

**응답** 창에서 **헤더** 탭을 클릭하고 **위치** 헤더 값을 복사합니다.

![Postman 콘솔의 헤더 탭](../../tutorials/first-web-api/_static/pmc2.png)

위치 헤더 URI를 사용하여 새 항목에 액세스할 수 있습니다.

### <a name="update"></a>업데이트

다음 `Update` 메서드를 추가합니다.

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]

::: moniker-end

HTTP PUT을 사용하는 것을 제외하고 `Update`는 `Create`와 비슷합니다. 응답은 [204(콘텐츠 없음)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)입니다. HTTP 사양에 따라 PUT 요청의 경우 클라이언트는 델타만이 아니라 전체 업데이트된 엔터티를 보내야 합니다. 부분 업데이트를 지원하려면 HTTP PATCH를 사용합니다.

Postman을 사용하여 할 일 항목의 이름을 "walk cat"으로 업데이트합니다.

![204(콘텐츠 없음) 응답을 보여주는 Postman 콘솔](../../tutorials/first-web-api/_static/pmcput.png)

### <a name="delete"></a>삭제

다음 `Delete` 메서드를 추가합니다.

[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Delete)]

`Delete` 응답은 [204(콘텐츠 없음)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)입니다.

Postman을 사용하여 할 일 항목을 삭제합니다.

![204(콘텐츠 없음) 응답을 보여주는 Postman 콘솔](../../tutorials/first-web-api/_static/pmd.png)
