---
title: NSwag 및 ASP.NET Core 시작
author: zuckerthoben
description: NSwag를 사용하여 ASP.NET Core Web API 앱에 대한 설명서 및 도움말 페이지를 생성하는 방법을 배웁니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 03/15/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: tutorials/get-started-with-nswag
ms.openlocfilehash: 80e6a9e1702d8f68d139d2ff9c3a01a27c40cecb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="get-started-with-nswag-and-aspnet-core"></a>NSwag 및 ASP.NET Core 시작

작성자: [Christoph Nienaber](https://twitter.com/zuckerthoben) 및 [Rico Suter](https://rsuter.com)

ASP.NET Core 미들웨어에서 [NSwag](https://github.com/RSuter/NSwag)를 사용하려면 [NSwag.AspNetCore](https://www.nuget.org/packages/NSwag.AspNetCore/) NuGet 패키지가 필요합니다. 이 패키지는 Swagger 생성기, Swagger UI(v2 및 v3) 및 [ReDoc UI](https://github.com/Rebilly/ReDoc)로 구성됩니다.

NSwag의 코드 생성 기능을 사용하는 것이 좋습니다. 코드 생성을 위해 다음 옵션 중 하나를 선택합니다.

* API용 C# 및 TypeScript로 클라이언트 코드를 생성하는 Windows 데스크톱 앱인 [NSwagStudio](https://github.com/NSwag/NSwag/wiki/NSwagStudio) 사용
* 프로젝트 내에서 코드 생성을 수행하기 위해 [NSwag.CodeGeneration.CSharp](https://www.nuget.org/packages/NSwag.CodeGeneration.CSharp/) 또는 [NSwag.CodeGeneration.TypeScript](https://www.nuget.org/packages/NSwag.CodeGeneration.TypeScript/) NuGet 패키지 사용
* [명령줄](https://github.com/NSwag/NSwag/wiki/CommandLine)에서 NSwag 사용
* [NSwag.MSBuild](https://github.com/NSwag/NSwag/wiki/MSBuild) NuGet 패키지 사용

## <a name="features"></a>기능

NSwag를 사용하는 주요 이유는 UI Swagger 및 Swagger 생성기를 도입할 뿐만 아니라 유연한 코드 생성 기능을 사용하기 위함입니다. 기존 API가 필요하지 않으므로 Swagger를 통합하고 NSwag가 클라이언트 구현을 생성하도록 하는 타사 API를 사용할 수 있습니다. 어느 쪽이든 개발 주기가 빠르며 API 변경에 보다 쉽게 대응할 수 있습니다.

## <a name="package-installation"></a>패키지 설치

다음 방법으로 NSwag NuGet 패키지를 추가할 수 있습니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* **패키지 관리자 콘솔** 창에서:

    ```powershell
    Install-Package NSwag.AspNetCore
    ```

* **NuGet 패키지 관리** 대화 상자에서:
  * **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 > **NuGet 패키지 관리** 선택
  * **패키지 소스**를 “nuget.org”로 설정
  * 검색 상자에 “NSwag.AspNetCore” 입력
  * **찾아보기** 탭에서 "NSwag.AspNetCore" 패키지를 선택하고 **설치** 클릭

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* **Solution Pad**에서 *Packages* 폴더를 마우스 오른쪽 단추로 클릭 > **패키지 추가...** 선택
* **패키지 추가** 창의 **소스** 드롭다운을 “nuget.org”로 설정
* 검색 상자에 NSwag.AspNetCore 입력
* 결과 창에서 NSwag.AspNetCore 패키지를 선택하고 **패키지 추가** 클릭

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

**통합 터미널**에서 다음 명령을 실행합니다.

```console
dotnet add TodoApi.NSwag.csproj package NSwag.AspNetCore
```

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

다음 명령을 실행합니다.

```console
dotnet add TodoApi.NSwag.csproj package NSwag.AspNetCore
```

---

## <a name="add-and-configure-swagger-middleware"></a>Swagger 미들웨어 추가 및 구성

`Info` 클래스에서 다음 네임스페이스를 가져옵니다.

```csharp
using NSwag.AspNetCore;
using System.Reflection;
using NJsonSchema;
```

`Startup.Configure` 메서드에서 생성된 Swagger 사양 및 Swagger UI를 지원하기 위해 미들웨어를 사용하도록 설정합니다.

[!code-cs[](../tutorials/web-api-help-pages-using-swagger/samples/TodoApi.NSwag/Startup.cs?name=snippet_Configure&highlight=4,7-10)]

앱을 시작합니다. Swagger UI를 보려면 `/swagger`로 이동합니다. Swagger 사양을 보려면 `/swagger/v1/swagger.json`으로 이동합니다.

## <a name="code-generation"></a>코드 생성

### <a name="via-nswagstudio"></a>NSwagStudio를 통해

* 공식 [GitHub 리포지토리](https://github.com/RSuter/NSwag/wiki/NSwagStudio)에서 `NSwagStudio`를 설치합니다.

* NSwagStudio를 시작합니다. *swagger.json*의 위치를 입력하거나 직접 복사합니다.

![NSwagStudio](web-api-help-pages-using-swagger/_static/NSwagStudio.png)

* 원하는 클라이언트 출력 유형을 나타냅니다. 옵션에는 **TypeScript 클라이언트**, **CSharp 클라이언트** 또는 **CSharp Web API 컨트롤러**가 포함됩니다. Web API 컨트롤러를 사용할 경우 기본적으로 역방향으로 생성됩니다. 서비스의 사양을 사용하여 서비스가 다시 빌드됩니다.

* **출력 생성**을 클릭합니다.

* 여기서 C#으로 작성된 *TodoApi.NSwag* 샘플의 완전한 클라이언트 구현을 확인할 수 있습니다.

![NSwagStudio-Output](web-api-help-pages-using-swagger/_static/NSwagStudio-Output.png)

* 파일을 클라이언트 프로젝트(예: [Xamarin.Forms](/xamarin/xamarin-forms/) 앱)에 넣습니다. API 사용 시작:

```csharp
var todoClient = new TodoClient();

// Gets all Todos from the Api
var allTodos = await todoClient.GetAllAsync();

// Create a new TodoItem and save it in the Api
var createdTodo = await todoClient.CreateAsync(new TodoItem);

// Get a single Todo by Id
var foundTodo = await todoClient.GetByIdAsync(1);
```

> [!NOTE]
> 기본 URL 및/또는 HTTP 클라이언트를 API 클라이언트에 삽입할 수 있습니다. 가장 좋은 방법은 항상 [HttpClient를 다시 사용](https://aspnetmonsters.com/2016/08/2016-08-27-httpclientwrong/)하는 것입니다.

이제 클라이언트 프로젝트에 API를 쉽게 구현할 수 있습니다.

### <a name="other-ways-to-generate-client-code"></a>클라이언트 코드를 생성하는 다른 방법

워크플로에 더 적합한 다른 방법으로 코드를 생성할 수 있습니다.

* [MSBuild](https://www.nuget.org/packages/NSwag.MSBuild/)

* [코드 내](https://github.com/NSwag/NSwag/wiki/SwaggerToCSharpClientGenerator)

* [T4 템플릿](https://github.com/NSwag/NSwag/wiki/T4)

## <a name="customization"></a>사용자 지정

### <a name="xml-comments"></a>XML 주석

XML 주석은 다음과 같은 방법으로 활성화됩니다.

#### <a name="visual-studiotabvisual-studio-xml"></a>[Visual Studio](#tab/visual-studio-xml/)
* **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성** 선택
* **빌드** 탭의 **출력** 섹션에서 **XML 문서 파일** 상자 선택:

![프로젝트 속성의 빌드 탭](web-api-help-pages-using-swagger/_static/swagger-xml-comments.png)

#### <a name="visual-studio-for-mactabvisual-studio-mac-xml"></a>[Visual Studio for Mac](#tab/visual-studio-mac-xml/)
* **프로젝트 옵션** 대화 상자 열기 > **빌드** > **컴파일러** 선택
* **일반 옵션** 섹션에서 **XML 문서 생성** 상자 선택:

![프로젝트 옵션의 일반 옵션 섹션](web-api-help-pages-using-swagger/_static/swagger-xml-comments-mac.png)

#### <a name="visual-studio-codetabvisual-studio-code-xml"></a>[Visual Studio Code](#tab/visual-studio-code-xml/)
*.csproj* 파일에 다음 코드 조각을 수동으로 추가합니다.

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/TodoApi.NSwag/TodoApiNSwag.csproj?range=7-9)]

* * *
## <a name="data-annotations"></a>데이터 주석

NSwag는 [리플렉션](/dotnet/csharp/programming-guide/concepts/reflection)을 사용하며, Web API 작업의 가장 좋은 방법은 [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult)를 반환하는 것입니다. 따라서 NSwag는 사용자가 무슨 작업을 수행하고 반환하는지 유추할 없습니다. 다음 예제를 참조하세요.

```csharp
public IActionResult Create([FromBody] TodoItem item)
{
    if (item == null)
    {
        return BadRequest();
    }

    _context.TodoItems.Add(item);
    _context.SaveChanges();

     return CreatedAtRoute("GetTodo", new { id = item.Id }, item);
}
```

이전 작업은 `IActionResult`를 반환하지만 작업 내에서는 [CreatedAtRoute](/dotnet/api/system.web.http.apicontroller.createdatroute) 또는 [BadRequest](/dotnet/api/system.web.http.apicontroller.badrequest)를 반환합니다. 데이터 주석은 이 작업이 반환하는 HTTP 응답을 클라이언트에 알리는 데 사용됩니다. 다음 특성으로 작업을 데코레이트하세요.

```csharp
[HttpPost]
[ProducesResponseType(typeof(TodoItem), 201)] // Created
[ProducesResponseType(typeof(TodoItem), 400)] // BadRequest
public IActionResult Create([FromBody] TodoItem item)
```

이제 Swagger 생성기는 이 작업을 정확하게 설명할 수 있으며, 생성된 클라이언트가 엔드포인트를 호출할 때 수신한 내용을 알 수 있습니다. 이러한 특성으로 모든 작업을 데코레이트하는 것이 좋습니다. API 작업에서 반환해야 하는 HTTP 응답에 대한 지침은 [RFC 7231 사양](https://tools.ietf.org/html/rfc7231#section-4.3)을 참조하세요.
