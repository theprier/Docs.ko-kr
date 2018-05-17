## <a name="call-the-web-api-with-jquery"></a>jQuery를 사용하여 Web API 호출

이 섹션에서는 jQuery를 사용하여 Web API를 호출하는 HTML 페이지가 추가되었습니다. jQuery는 요청을 시작하고 API 응답의 세부 정보로 페이지를 업데이트합니다.

정적 파일을 제공하고 기본 파일 매핑을 사용하도록 프로젝트를 구성합니다. 이는 *Startup.Configure*에서 [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 및 [UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 확장 메서드를 호출하여 수행됩니다. 자세한 내용은 [정적 파일](xref:fundamentals/static-files)을 참조하세요.

[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Startup2.cs?name=snippet_Configure&highlight=3-4)]

*index.html*이라는 HTML 파일을 해당 프로젝트의 *wwwroot* 디렉터리에 추가합니다. 다음 표시로 콘텐츠를 바꿉니다.

[!code-html[](../../tutorials/first-web-api/samples/2.0/TodoApi/wwwroot/index.html)]

*site.js*라는 JavaScript 파일을 해당 프로젝트의 *wwwroot* 디렉터리에 추가합니다. 다음 코드로 콘텐츠를 바꿉니다.

[!code-javascript[](../../tutorials/first-web-api/samples/2.0/TodoApi/wwwroot/site.js?name=snippet_SiteJs)]

HTML 페이지를 로컬에서 테스트하려면 ASP.NET Core 프로젝트의 시작 설정을 변경해야 할 수 있습니다. 프로젝트의 *속성* 디렉터리에서 *launchSettings.json*을 엽니다. `launchUrl` 속성을 제거하여 앱이 *index.html*&mdash; 프로젝트의 기본 파일에서 열리도록 합니다.

여러 가지 방법으로 jQuery를 가져올 수 있습니다. 위의 코드 조각에서 라이브러리는 CDN에서 로드됩니다. 이 샘플은 jQuery를 사용하여 API를 호출하는 완전한 CRUD 예제입니다. 이 샘플에는 경험을 풍부하게 하는 추가 기능이 있습니다. 다음은 API 호출에 대한 설명입니다.

### <a name="get-a-list-of-to-do-items"></a>할 일 항목의 목록 가져오기

할 일 항목의 목록을 가져오려면 HTTP GET 요청을 */api/todo*에 보냅니다.

jQuery [ajax](https://api.jquery.com/jquery.ajax/) 함수는 개체 또는 배열을 나타내는 JSON을 반환하는 API에 AJAX 요청을 보냅니다. 이 함수는 HTTP 요청을 지정된 `url`로 보내는 모든 형태의 HTTP 상호 작용을 처리할 수 있습니다. `GET`이 `type`으로 사용됩니다. 요청이 성공하면 `success` 콜백 함수가 호출됩니다. 콜백에서 DOM은 할 일 정보로 업데이트됩니다.

[!code-javascript[](../../tutorials/first-web-api/samples/2.0/TodoApi/wwwroot/site.js?name=snippet_GetData)]

### <a name="add-a-to-do-item"></a>할 일 항목 추가

할 일 항목을 추가하려면 HTTP POST 요청을 */api/todo/* 에 보냅니다. 요청 본문은 할 일 개체를 포함해야 합니다. [ajax](https://api.jquery.com/jquery.ajax/) 함수는 `POST`를 사용하여 API를 호출합니다. `POST` 및 `PUT` 요청의 경우, 요청 본문은 API에 전송되는 데이터를 나타냅니다. API는 JSON 요청 본문을 요구합니다. `accepts` 및 `contentType` 옵션은 수신 및 전송되는 미디어 유형을 각각 분류하기 위해 `application/json`으로 설정됩니다. 데이터는 [`JSON.stringify`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)를 사용하여 JSON 개체로 변환됩니다. API가 성공적인 상태 코드를 반환하면 `getData` 함수가 호출되어 HTML 테이블을 업데이트합니다.

[!code-javascript[](../../tutorials/first-web-api/samples/2.0/TodoApi/wwwroot/site.js?name=snippet_AddItem)]

### <a name="update-a-to-do-item"></a>할 일 항목 업데이트

할 일 항목을 업데이트하는 것은 할 일 항목을 추가하는 것과 매우 유사합니다. 두 작업 모두 요청 본문에 의존하기 때문입니다. 이 경우 두 작업의 유일한 차이점은 항목의 고유 식별자를 추가하기 위해 `url`이 변경되고, `type`은 `PUT`입니다.

[!code-javascript[](../../tutorials/first-web-api/samples/2.0/TodoApi/wwwroot/site.js?name=snippet_AjaxPut)]

### <a name="delete-a-to-do-item"></a>할 일 항목 삭제

할 일 항목을 삭제하려면 AJAX 호출에서 `type`을 `DELETE`로 설정하고 URL에서 항목의 고유 식별자를 지정하면 됩니다.

[!code-javascript[](../../tutorials/first-web-api/samples/2.0/TodoApi/wwwroot/site.js?name=snippet_AjaxDelete)]
