---
title: ASP.NET Core 및 Mac용 Visual Studio를 사용하여 Web API 만들기
author: rick-anderson
description: ASP.NET Core MVC 및 Mac용 Visual Studio를 사용하여 Web API 만들기
ms.author: riande
ms.custom: mvc
ms.date: 05/08/2018
uid: tutorials/first-web-api-mac
ms.openlocfilehash: 40f9bd9c57b97826edfddeb00cb4fb38a026d46e
ms.sourcegitcommit: b2723654af4969a24545f09ebe32004cb5e84a96
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2018
ms.locfileid: "46011627"
---
# <a name="create-a-web-api-with-aspnet-core-and-visual-studio-for-mac"></a>ASP.NET Core 및 Mac용 Visual Studio를 사용하여 Web API 만들기

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Mike Wasson](https://github.com/mikewasson)

이 자습서에서는 “할 일” 항목 목록을 관리하기 위한 웹 API를 빌드합니다. UI는 생성되지 않습니다.

이 자습서는 다음 세 가지 버전으로 제공됩니다.

* macOS: Mac용 Visual Studio를 사용한 Web API(이 자습서)
* Windows: [Windows용 Visual Studio를 사용한 Web API](xref:tutorials/first-web-api)
* macOS, Linux, Windows: [Visual Studio Code를 사용한 Web API](xref:tutorials/web-api-vsc)

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[template files](../includes/webApi/intro.md)]

영구 데이터베이스를 사용하는 예제를 보려면 [macOS 또는 Linux의 ASP.NET Core MVC 소개](xref:tutorials/first-mvc-app-xplat/index)를 참조하세요.

## <a name="prerequisites"></a>전제 조건

[!INCLUDE[](~/includes/net-core-prereqs-macos.md)]

## <a name="create-the-project"></a>프로젝트를 만듭니다.

Visual Studio에서 **파일** > **새 솔루션**을 선택합니다.

![macOS 새 솔루션](first-web-api-mac/_static/sln.png)

**.NET Core App** > **ASP.NET Core Web API** > **다음**을 선택합니다.

![macOS 새 프로젝트 대화 상자](first-web-api-mac/_static/1.png)

**프로젝트 이름**으로 *TodoApi*를 입력한 다음, **만들기**를 클릭합니다.

![구성 대화 상자](first-web-api-mac/_static/2.png)

### <a name="launch-the-app"></a>앱 시작

Visual Studio에서 **실행** > **디버깅 시작**을 선택하여 앱을 시작합니다. Visual Studio가 브라우저를 시작하고 `http://localhost:5000`으로 이동합니다. HTTP 404(찾을 수 없음) 오류가 표시됩니다. URL을 `http://localhost:<port>/api/values`로 변경합니다. `ValuesController` 데이터가 표시됩니다.

```json
["value1","value2"]
```

### <a name="add-support-for-entity-framework-core"></a>Entity Framework Core에 대한 지원 추가

[Entity Framework Core InMemory](/ef/core/providers/in-memory/) 데이터베이스 공급자를 설치합니다. 이 데이터베이스 공급자를 설치하면 Entity Framework Core를 메모리 내 데이터베이스에서 사용할 수 있습니다.

* **프로젝트** 메뉴에서 **NuGet 패키지 추가**를 선택합니다.

  * 또는 **종속성**을 마우스 오른쪽 단추로 클릭한 다음, **패키지 추가**를 선택합니다.

* 검색 상자에 `EntityFrameworkCore.InMemory`를 입력합니다.
* `Microsoft.EntityFrameworkCore.InMemory`를 선택하고 **패키지 추가**를 선택합니다.

### <a name="add-a-model-class"></a>모델 클래스 추가

모델은 앱에서 데이터를 나타내는 개체입니다. 이 경우 유일한 모델은 할 일 항목입니다.

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다. **추가** > **새 폴더**를 선택합니다. 폴더 이름을 *Models*로 지정합니다.

![새 폴더](first-web-api-mac/_static/folder.png)

> [!NOTE]
> 프로젝트의 아무 곳에나 모델 클래스를 넣을 수 있지만 일반적으로 *Models* 폴더를 사용합니다.

*모델* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 파일** > **일반** > **빈 클래스**를 선택합니다. 클래스 이름을 *TodoItem*으로 지정한 다음, **새로 만들기**를 클릭합니다.

생성된 코드를 다음으로 바꿉니다.

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoItem.cs)]

`TodoItem`이 만들어질 때 데이터베이스가 `Id`를 생성합니다.

### <a name="create-the-database-context"></a>데이터베이스 컨텍스트 만들기

*데이터베이스 컨텍스트*는 특정 데이터 모델에 맞게 Entity Framework 기능을 조정하는 주 클래스입니다. `Microsoft.EntityFrameworkCore.DbContext` 클래스에서 파생시키는 방식으로 이 클래스를 만듭니다.

`TodoContext` 클래스를 *Models* 폴더에 추가합니다.

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

## <a name="add-a-controller"></a>컨트롤러 추가

솔루션 탐색기의 *Controllers* 폴더에서 `TodoController` 클래스를 추가합니다.

생성된 코드를 다음으로 바꿉니다.

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a>앱 시작

Visual Studio에서 **실행** > **디버깅 시작**을 선택하여 앱을 시작합니다. Visual Studio가 브라우저를 시작하고 `http://localhost:<port>`로 이동합니다. 여기서 `<port>`는 임의로 선택된 포트 번호입니다. HTTP 404(찾을 수 없음) 오류가 표시됩니다. URL을 `http://localhost:<port>/api/values`로 변경합니다. `ValuesController` 데이터가 표시됩니다.

```json
["value1","value2"]
```

`http://localhost:<port>/api/todo`의 `Todo` 컨트롤러로 이동합니다. 다음 JSON이 반환됩니다.

```json
[{"key":1,"name":"Item1","isComplete":false}]
```

## <a name="implement-the-other-crud-operations"></a>기타 CRUD 작업 구현

`Create`, `Update` 및 `Delete` 메서드를 컨트롤러에 추가합니다. 이러한 메서드는 테마에 대한 변형이므로 코드를 표시하고 주요 차이점을 강조 표시하겠습니다. 코드를 추가하거나 변경한 후 프로젝트를 빌드합니다.

### <a name="create"></a>만들기

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

이전 메서드는 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 특성으로 표시되는 HTTP POST에 응답합니다. [[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) 특성은 HTTP 요청 본문에서 할 일 항목 값을 가져오도록 MVC에 지시합니다.

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

이전 메서드는 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 특성으로 표시되는 HTTP POST에 응답합니다. MVC는 HTTP 요청 본문에서 할 일 항목 값을 가져옵니다.

::: moniker-end

`CreatedAtRoute` 메서드는 201 응답을 반환합니다. 이는 서버에서 새 리소스를 만드는 HTTP POST 메서드의 표준 응답입니다. `CreatedAtRoute`는 응답에 대한 위치 헤더도 추가합니다. 위치 헤더는 새로 만들어진 할 일 항목의 URI를 지정합니다. [10.2.2 201 Created](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)(10.2.2 201 생성됨)를 참조하세요.

### <a name="use-postman-to-send-a-create-request"></a>Postman을 사용하여 만들기 요청 보내기

* 앱을 시작합니다(**실행** > **디버깅 시작**).
* Postman을 엽니다.

![Postman 콘솔](first-web-api/_static/pmc.png)

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

![Postman 콘솔의 헤더 탭](first-web-api/_static/pmc2.png)

위치 헤더 URI를 사용하여 만든 리소스에 액세스할 수 있습니다. `Create` 메서드는 [CreatedAtRoute](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdatroute#Microsoft_AspNetCore_Mvc_ControllerBase_CreatedAtRoute_System_String_System_Object_System_Object_)를 반환합니다. `CreatedAtRoute`에 전달된 첫 번째 매개 변수는 URL을 생성하는 데 사용할 이름이 지정된 경로를 나타냅니다. `GetById` 메서드가 `"GetTodo"`로 명명된 경로를 만들었다는 사실을 기억하세요.

```csharp
[HttpGet("{id}", Name = "GetTodo")]
```

### <a name="update"></a>업데이트

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]

::: moniker-end

`Update`는 `Create`와 비슷하지만 HTTP PUT을 사용합니다. 응답은 [204(콘텐츠 없음)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)입니다. HTTP 사양에 따라 PUT 요청의 경우 클라이언트는 델타만이 아니라 전체 업데이트된 엔터티를 보내야 합니다. 부분 업데이트를 지원하려면 HTTP PATCH를 사용합니다.

```json
{
  "key": 1,
  "name": "walk dog",
  "isComplete": true
}
```

![204(콘텐츠 없음) 응답을 보여주는 Postman 콘솔](first-web-api/_static/pmcput.png)

### <a name="delete"></a>삭제

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Delete)]

응답은 [204(콘텐츠 없음)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)입니다.

![204(콘텐츠 없음) 응답을 보여주는 Postman 콘솔](first-web-api/_static/pmd.png)

[!INCLUDE[jQuery](../includes/webApi/add-jquery.md)]

[!INCLUDE[next steps](../includes/webApi/next.md)]
