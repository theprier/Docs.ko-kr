---
title: Swashbuckle 및 ASP.NET Core 시작
author: zuckerthoben
description: ASP.NET Core Web API 프로젝트에 Swashbuckle을 추가하여 Swagger UI를 통합하는 방법을 알아봅니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 05/08/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: tutorials/get-started-with-swashbuckle
ms.openlocfilehash: 0eb9aa12419cc09899af6bc85dd32a85687dab62
ms.sourcegitcommit: 9bc34b8269d2a150b844c3b8646dcb30278a95ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/12/2018
---
# <a name="get-started-with-swashbuckle-and-aspnet-core"></a>Swashbuckle 및 ASP.NET Core 시작

작성자: [Shayne Boyer](https://twitter.com/spboyer) 및 [Scott Addie](https://twitter.com/Scott_Addie)

::: moniker range="<= aspnetcore-2.0"
[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))
::: moniker-end

Swashbuckle에 대한 세 가지 주 구성 요소는 다음과 같습니다.

* [Swashbuckle.AspNetCore.Swagger](https://www.nuget.org/packages/Swashbuckle.AspNetCore.Swagger/): `SwaggerDocument` 개체를 JSON 엔드포인트로 노출하기 위한 Swagger 개체 모델 및 미들웨어.

* [Swashbuckle.AspNetCore.SwaggerGen](https://www.nuget.org/packages/Swashbuckle.AspNetCore.SwaggerGen/): 경로, 컨트롤러 및 모델에서 직접 `SwaggerDocument` 개체를 빌드하는 Swagger 생성기. 일반적으로 Swagger 끝점 미들웨어와 결합되어 자동으로 Swagger JSON을 노출합니다.

* [Swashbuckle.AspNetCore.SwaggerUI](https://www.nuget.org/packages/Swashbuckle.AspNetCore.SwaggerUI/): Swagger UI 도구의 포함된 버전. Swagger JSON을 해석하여 Web API 기능을 설명하기 위한 다양한 사용자 지정 가능한 환경을 빌드합니다. 여기에는 공용 메서드에 대한 기본 제공 테스트 도구가 포함됩니다.

## <a name="package-installation"></a>패키지 설치

다음 방법으로 Swashbuckle을 추가할 수 있습니다.

### <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* **패키지 관리자 콘솔** 창에서:
  * **보기** > **다른 창** > **패키지 관리자 콘솔**로 이동
  * *TodoApi.csproj* 파일이 위치한 디렉터리로 이동
  * 다음 명령을 실행합니다.

    ```powershell
    Install-Package Swashbuckle.AspNetCore
    ```

* **NuGet 패키지 관리** 대화 상자에서:
  * **솔루션 탐색기** > **NuGet 패키지 관리**에서 프로젝트를 마우스 오른쪽 단추로 클릭
  * **패키지 소스**를 “nuget.org”로 설정
  * 검색 상자에 “Swashbuckle.AspNetCore” 입력
  * **찾아보기** 탭에서 “Swashbuckle.AspNetCore” 패키지를 선택하고 **설치** 클릭

### <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* **Solution Pad**에서 *Packages* 폴더를 마우스 오른쪽 단추로 클릭 > **패키지 추가...** 선택
* **패키지 추가** 창의 **소스** 드롭다운을 “nuget.org”로 설정
* 검색 상자에 “Swashbuckle.AspNetCore” 입력
* 결과 창에서 "Swashbuckle.AspNetCore" 패키지를 선택하고 **패키지 추가** 클릭

### <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

**통합 터미널**에서 다음 명령을 실행합니다.

```console
dotnet add TodoApi.csproj package Swashbuckle.AspNetCore
```

### <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

다음 명령을 실행합니다.

```console
dotnet add TodoApi.csproj package Swashbuckle.AspNetCore
```

---

## <a name="add-and-configure-swagger-middleware"></a>Swagger 미들웨어 추가 및 구성

`Startup.ConfigureServices` 메서드의 서비스 컬렉션에 Swagger 생성기를 추가합니다.

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup2.cs?name=snippet_ConfigureServices&highlight=8-11)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Startup2.cs?name=snippet_ConfigureServices&highlight=9-12)]
::: moniker-end

`Info` 클래스를 사용하기 위해 다음 네임스페이스를 가져옵니다.

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup2.cs?name=snippet_InfoClassNamespace)]

`Startup.Configure` 메서드에서 생성된 JSON 문서 및 Swagger UI를 지원하기 위해 미들웨어를 사용하도록 설정합니다.

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup2.cs?name=snippet_Configure&highlight=4,8-11)]

앱을 시작하고 `http://localhost:<port>/swagger/v1/swagger.json`으로 이동합니다. 엔드포인트를 설명하는 생성된 문서는 [Swagger 사양(swagger.json)](xref:tutorials/web-api-help-pages-using-swagger#swagger-specification-swaggerjson)에 표시된 것처럼 나타납니다.

Swagger UI는 `http://localhost:<port>/swagger`에 있습니다. Swagger UI를 통해 API를 탐색하고 다른 프로그램에 통합합니다.

> [!TIP]
> 앱의 루트(`http://localhost:<port>/`)에서 Swagger UI를 제공하려면 `RoutePrefix` 속성을 빈 문자열로 설정합니다.
>
> [!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup3.cs?name=snippet_UseSwaggerUI&highlight=4)]

## <a name="customize--extend"></a>사용자 지정 및 확장

Swagger는 개체 모델을 설명하고 테마와 일치하도록 UI를 사용자 지정하는 옵션을 제공합니다.

### <a name="api-info-and-description"></a>API 정보 및 설명

`AddSwaggerGen` 메서드에 전달되는 구성 작업은 작성자, 라이선스 및 설명과 같은 정보를 추가합니다.

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup4.cs?name=snippet_AddSwaggerGen)]

Swagger UI는 버전의 정보를 표시합니다.

![버전 정보가 포함된 Swagger UI: 설명, 작성자 및 추가 링크 확인](web-api-help-pages-using-swagger/_static/custom-info.png)

### <a name="xml-comments"></a>XML 주석

XML 주석은 다음 방법으로 사용하도록 설정할 수 있습니다.

# <a name="visual-studiotabvisual-studio-xml"></a>[Visual Studio](#tab/visual-studio-xml/)

* **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성** 선택
* **빌드** 탭의 **출력** 섹션에서 **XML 문서 파일** 상자 선택

# <a name="visual-studio-for-mactabvisual-studio-mac-xml"></a>[Visual Studio for Mac](#tab/visual-studio-mac-xml/)

* **프로젝트 옵션** 대화 상자 열기 > **빌드** > **컴파일러** 선택
* **일반 옵션** 섹션에서 **XML 문서 생성** 상자 선택

# <a name="visual-studio-codetabvisual-studio-code-xml"></a>[Visual Studio Code](#tab/visual-studio-code-xml/)

*.csproj* 파일에 다음 코드 조각을 수동으로 추가합니다.

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/TodoApi.csproj?name=snippet_SuppressWarnings&highlight=2)]

---

XML 주석을 사용하면 문서화되지 않은 public 형식과 멤버에 대한 디버그 정보를 제공합니다. 문서화되지 않은 형식 및 멤버는 경고 메시지로 표시됩니다. 예를 들어 다음 메시지는 경고 코드 1591 위반을 나타냅니다.

```text
warning CS1591: Missing XML comment for publicly visible type or member 'TodoController.GetAll()'
```

*.csproj* 파일에서 무시할 경고 코드의 세미콜론으로 구분된 목록을 정의하여 경고를 표시하지 않습니다.

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/TodoApi.csproj?name=snippet_SuppressWarnings&highlight=3)]

생성된 XML 파일을 사용하도록 Swagger를 구성합니다. Linux 또는 Windows가 아닌 운영 체제의 경우 파일 이름 및 경로는 대/소문자를 구분할 수 있습니다. 예를 들어 *TodoApi.XML* 파일은 Windows에는 유효하지만 CentOS에는 그렇지 않습니다.

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup.cs?name=snippet_ConfigureServices&highlight=30-32)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Startup.cs?name=snippet_ConfigureServices&highlight=31-33)]
::: moniker-end

이전 코드에서 [리플렉션](/dotnet/csharp/programming-guide/concepts/reflection)은 Web API 프로젝트의 이름과 일치하는 XML 파일 이름을 빌드하는 데 사용됩니다. 이 방법은 생성된 XML 파일 이름이 프로젝트 이름과 일치하도록 합니다. [AppContext.BaseDirectory](/dotnet/api/system.appcontext.basedirectory#System_AppContext_BaseDirectory) 속성은 XML 파일에 대한 경로를 생성하는 데 사용됩니다.

작업에 3중 슬래시 주석을 추가하면 섹션 헤더에 설명이 추가되어 Swagger UI가 향상됩니다. `Delete` 작업 위에 [\<요약>](/dotnet/csharp/programming-guide/xmldoc/summary) 요소를 추가합니다.

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Delete&highlight=1-3)]

Swagger UI는 이전 코드 `<summary>` 요소의 내부 텍스트를 표시합니다.

![DELETE 메서드에 대한 XML 주석 ‘특정 TodoItem을 삭제합니다.’를 보여 주는 Swagger UI](web-api-help-pages-using-swagger/_static/triple-slash-comments.png)

UI는 생성된 JSON 스키마에 의해 구동됩니다.

```json
"delete": {
    "tags": [
        "Todo"
    ],
    "summary": "Deletes a specific TodoItem.",
    "operationId": "ApiTodoByIdDelete",
    "consumes": [],
    "produces": [],
    "parameters": [
        {
            "name": "id",
            "in": "path",
            "description": "",
            "required": true,
            "type": "integer",
            "format": "int64"
        }
    ],
    "responses": {
        "200": {
            "description": "Success"
        }
    }
}
```

[\<설명>](/dotnet/csharp/programming-guide/xmldoc/remarks) 요소를 `Create` 작업 메서드 문서에 추가합니다. 이는 `<summary>` 요소에 지정된 정보를 보충하고 더 강력한 Swagger UI를 제공합니다. `<remarks>` 요소 콘텐츠는 텍스트, JSON 또는 XML로 구성될 수 있습니다.

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=4-14)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=4-14)]
::: moniker-end

이러한 추가 주석이 포함된 향상된 UI 기능을 확인할 수 있습니다.

![추가 주석이 표시된 Swagger UI](web-api-help-pages-using-swagger/_static/xml-comments-extended.png)

### <a name="data-annotations"></a>데이터 주석

[System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) 네임스페이스에 있는 특성으로 모델을 데코레이트하여 Swagger UI 구성 요소를 구동합니다.

`[Required]` 특성을 `TodoItem` 클래스의 `Name` 속성에 추가합니다.

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Models/TodoItem.cs?highlight=10)]

이 특성이 있으면 UI 동작이 변경되고 기본 JSON 스키마가 변경됩니다.

```json
"definitions": {
    "TodoItem": {
        "required": [
            "name"
        ],
        "type": "object",
        "properties": {
            "id": {
                "format": "int64",
                "type": "integer"
            },
            "name": {
                "type": "string"
            },
            "isComplete": {
                "default": false,
                "type": "boolean"
            }
        }
    }
},
```

API 컨트롤러에 `[Produces("application/json")]` 특성을 추가합니다. 이 특성은 컨트롤러 동작이 *application/json*의 응답 콘텐츠 형식을 지원함을 선언하는 데 사용됩니다.

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_TodoController&highlight=1)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_TodoController&highlight=1)]
::: moniker-end

컨트롤러 GET 작업의 경우 **응답 콘텐츠 형식** 드롭다운에서 이 콘텐츠 형식이 기본값으로 선택됩니다.

![기본 응답 콘텐츠 형식이 포함된 Swagger UI](web-api-help-pages-using-swagger/_static/json-response-content-type.png)

Web API에서 데이터 주석 사용이 증가하면 UI 및 API 도움말 페이지에는 더 자세한 설명과 유용한 정보가 제공됩니다.

### <a name="describe-response-types"></a>응답 형식 설명

소비 개발자는 반환된 내용 중에서도 특히 응답 형식 및 오류 코드(표준이 아닌 경우)를 가장 중요하게 생각합니다. 응답 형식 및 오류 코드는 XML 주석 및 데이터 주석에 표시됩니다.

`Create` 작업은 성공 시 HTTP 201 상태 코드를 반환합니다. 게시된 요청 본문이 null일 경우 HTTP 400 상태 코드가 반환됩니다. Swagger UI에 적절한 문서가 없으면 소비자는 이러한 예상 결과에 대한 정보를 알 수 없습니다. 다음 예제에서 강조 표시된 줄을 추가하여 해당 문제를 해결합니다.

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=17,18,20,21)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.Swashbuckle/Controllers/TodoController.cs?name=snippet_Create&highlight=17,18,20,21)]
::: moniker-end

이제 Swagger UI에서는 예상 HTTP 응답 코드를 분명히 설명합니다.

![POST 응답 클래스 설명 ‘새로 만들어진 Todo 항목 반환’ 및 ‘400 - 응답 메시지에서 항목의 상태 코드 및 이유가 null인 경우’를 보여 주는 Swagger UI](web-api-help-pages-using-swagger/_static/data-annotations-response-types.png)

### <a name="customize-the-ui"></a>UI 사용자 지정

재고 UI는 기능적이며 표시 가능합니다. 그러나 API 설명서 페이지는 브랜드 또는 테마를 나타내야 합니다. Swashbuckle 구성 요소를 브랜딩하려면 리소스를 추가하여 정적 파일을 지원하고 폴더 구조를 빌드하여 해당 파일을 호스트해야 합니다.

.NET Framework 또는 NET Core 1.x를 대상으로 하는 경우 [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles) NuGet 패키지를 프로젝트에 추가합니다.

```xml
<PackageReference Include="Microsoft.AspNetCore.StaticFiles" Version="2.0.0" />
```

이전 NuGet 패키지는 .NET Core 2.x를 대상으로 하고 [metapackage](xref:fundamentals/metapackage)를 사용하는 경우 이미 설치되어 있습니다.

정적 파일 미들웨어를 사용하도록 설정합니다.

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/Startup.cs?name=snippet_Configure&highlight=3)]

[Swagger UI GitHub 리포지토리](https://github.com/swagger-api/swagger-ui/tree/master/dist)에서 *dist* 폴더의 콘텐츠를 가져옵니다. 이 폴더에는 Swagger UI 페이지에 필요한 자산이 포함됩니다.

*wwwroot/swagger/ui* 폴더를 만들고 *dist* 폴더의 콘텐츠를 복사합니다.

다음 CSS를 사용하여 *wwwroot/swagger/ui*에 *custom.css* 파일을 만들어 페이지 헤더를 사용자 지정합니다.

[!code-css[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/wwwroot/swagger/ui/custom.css)]

다른 CSS 파일 다음에 *index.html* 파일의 *custom.css*를 참조합니다.

[!code-html[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.Swashbuckle/wwwroot/swagger/ui/index.html?name=snippet_SwaggerUiCss&highlight=3)]

`http://localhost:<port>/swagger/ui/index.html`의 *index.html* 페이지로 이동합니다. 헤더의 텍스트 상자에 `http://localhost:<port>/swagger/v1/swagger.json`을 입력하고 **탐색** 단추를 클릭합니다. 결과 페이지가 다음과 같이 표시됩니다.

![사용자 지정 헤더 제목이 포함된 Swagger UI](web-api-help-pages-using-swagger/_static/custom-header.png)

페이지를 사용하여 훨씬 더 많은 작업을 수행할 수 있습니다. [Swagger UI GitHub 리포지토리](https://github.com/swagger-api/swagger-ui)에서 UI 리소스에 대한 전체 기능을 참조하세요.
