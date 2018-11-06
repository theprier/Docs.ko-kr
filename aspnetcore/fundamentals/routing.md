---
title: ASP.NET Core에서 라우팅
author: ardalis
description: ASP.NET Core 라우팅 기능에서 들어오는 요청을 경로 처리기에 매핑하는 일을 담당하는 방법을 파악합니다.
ms.author: riande
ms.custom: mvc
ms.date: 10/01/2018
uid: fundamentals/routing
ms.openlocfilehash: a014782ba503bc8bd0fdefb4cb4f382aa8fde4cd
ms.sourcegitcommit: c43a6f1fe72d7c2db4b5815fd532f2b45d964e07
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50244972"
---
# <a name="routing-in-aspnet-core"></a>ASP.NET Core에서 라우팅

작성자: [Ryan Nowak](https://github.com/rynowak), [Steve Smith](https://ardalis.com/) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

라우팅 기능은 들어오는 요청을 경로 처리기에 매핑하는 일을 담당합니다. 경로는 앱에서 정의되고 앱 시작 시 구성됩니다. 경로는 요청에 포함된 URL에서 필요에 따라 값을 추출할 수 있으며 이러한 값은 요청 처리를 위해 사용될 수 있습니다. 앱에서 경로 정보를 사용하여 라우팅 기능은 경로 처리기에 매핑되는 URL을 생성할 수 있습니다. 따라서 라우팅은 URL에 따라 경로 처리기를 찾거나 경로 처리기 정보에 따라 지정된 경로 처리기에 해당하는 URL을 찾을 수 있습니다.

대부분의 앱은 URL이 읽을 수 있고 의미 있도록 기본적이고 설명적인 라우팅 체계를 선택해야 합니다. 기본 기존 경로 `{controller=Home}/{action=Index}/{id?}`:

* 기본적이고 설명적인 라우팅 체계를 지원합니다.
* 브라우저에서 사용할 웹앱의 경우 좋은 시작점입니다.

특별한 경우(예: 블로그, 전자 상거래)에 [특성 라우팅](xref:mvc/controllers/routing#attribute-routing) 또는 전용 기존 경로를 사용하여 앱의 트래픽이 많은 영역에 간결한 경로를 추가하는 것이 일반적입니다.

웹 API는 특성 라우팅을 사용하여 작업이 HTTP 동사로 표현되는 리소스 집합으로 앱의 기능을 모델링해야 합니다. 즉 동일한 논리 리소스의 많은 작업(예: GET, POST)이 동일한 URL을 사용합니다. 특성 라우팅은 API의 URL 공간을 신중하게 설계하는 데 필요한 제어 수준을 제공합니다.

MVC의 URL 생성 지원에서는 URL을 하드 코딩하지 않고 앱을 개발하여 앱을 서로 연결할 수 있습니다. 이렇게 하면 기본 라우팅 구성으로 시작하고 앱의 모양이 결정된 후 경로를 수정할 수 있습니다.

> [!IMPORTANT]
> 이 문서에서는 낮은 수준의 ASP.NET Core 라우팅을 설명합니다. ASP.NET Core MVC 라우팅에 대한 내용은 <xref:mvc/controllers/routing>을 참조하세요.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/routing/samples)([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="routing-basics"></a>라우팅 기본 사항

라우팅은 *경로*(<xref:Microsoft.AspNetCore.Routing.IRouter>의 구현)를 사용하여 다음 작업을 수행합니다.

* 들어오는 요청을 *경로 처리기*에 매핑
* 응답에 사용되는 URL 생성

일반적으로 앱은 단일 경로의 컬렉션을 갖습니다. 요청이 도착하면 경로 컬렉션이 순서대로 처리됩니다. 들어오는 요청은 경로 컬렉션에서 사용 가능한 각 경로의 <xref:Microsoft.AspNetCore.Routing.IRouter.RouteAsync*> 메서드를 호출하여 요청 URL과 일치하는 경로를 찾습니다. 이와 반대로 응답은 라우팅을 사용하여 경로 정보에 따라 URL(예: 리디렉션 또는 링크용)을 생성할 수 있으므로 하드 코딩 URL을 갖는 것을 방지합니다. 이는 유지 관리에 도움이 됩니다.

라우팅은 <xref:Microsoft.AspNetCore.Builder.RouterMiddleware> 클래스에 의해 [미들웨어](xref:fundamentals/middleware/index) 파이프라인에 연결되어 있습니다. [ASP.NET Core MVC](xref:mvc/overview)는 해당 구성의 일부분으로 라우팅을 미들웨어 파이프라인에 추가합니다. 독립 실행형 구성 요소로 라우팅 사용에 대한 자세한 내용은 [라우팅 미들웨어 사용](#use-routing-middleware) 섹션을 참조하세요.

### <a name="url-matching"></a>URL 일치

URL 일치는 라우팅에서 들어오는 요청을 *처리기*로 디스패치하는 프로세스입니다. 이 프로세스는 URL 경로의 데이터를 기반으로 하지만 요청에 있는 모든 데이터를 고려하도록 확장될 수 있습니다. 요청을 별도의 처리기로 디스패치하는 기능은 앱의 크기와 복잡성을 확장하는 핵심입니다.

들어오는 요청은 시퀀스의 각 경로에서 <xref:Microsoft.AspNetCore.Routing.IRouter.RouteAsync*> 메서드를 호출하는 `RouterMiddleware`를 입력합니다. <xref:Microsoft.AspNetCore.Routing.IRouter> 인스턴스는 [RouteContext.Handler](xref:Microsoft.AspNetCore.Routing.RouteContext.Handler*)를 null이 아닌 <xref:Microsoft.AspNetCore.Http.RequestDelegate>로 설정하여 요청을 *처리*할지 여부를 선택합니다. 경로가 요청에 대한 처리기를 설정하는 경우 경로 처리가 중지되고 처리기가 요청을 처리하도록 호출됩니다. 모든 경로가 시도되고 요청에 대한 처리기를 찾을 수 없는 경우 미들웨어는 *다음*을 호출하고 요청 파이프라인의 다음 미들웨어가 호출됩니다.

`RouteAsync`에 대한 기본 입력은 현재 요청과 연결된 [RouteContext.HttpContext](xref:Microsoft.AspNetCore.Routing.RouteContext.HttpContext*)입니다. `RouteContext.Handler` 및 [RouteContext.RouteData](xref:Microsoft.AspNetCore.Routing.RouteContext.RouteData*)는 경로가 일치된 후 설정된 출력입니다.

`RouteAsync` 동안 일치는 `RouteContext.RouteData`의 속성을 지금까지 수행된 요청 처리에 따라 적절한 값으로 설정합니다. 경로가 요청과 일치하는 경우 `RouteContext.RouteData`는 *결과*에 대한 중요한 상태 정보를 포함합니다.

[RouteData.Values](xref:Microsoft.AspNetCore.Routing.RouteData.Values*)는 경로에서 생성된 *경로 값*의 사전입니다. 이러한 값은 일반적으로 URL을 토큰화하여 결정되고, 사용자 입력을 수락하거나 앱 내부의 추가 디스패치 결정을 내리는 데 사용될 수 있습니다.

[RouteData.DataTokens](xref:Microsoft.AspNetCore.Routing.RouteData.DataTokens*)는 일치하는 경로와 관련된 추가 데이터의 속성 모음입니다. `DataTokens`는 각 경로와 상태 데이터 연결을 지원하도록 제공되므로 앱은 일치된 경로에 따라 나중에 결정을 내릴 수 있습니다. 이러한 값은 개발자 정의되고 어떤 방식으로든 라우팅의 동작에 영향을 주지 **않습니다**. 또한 `RouteData.DataTokens`에 스태시된 값은 `RouteData.Values`와 달리 모든 형식일 수 있습니다. 이는 문자열 간 쉽게 변환될 수 있어야 합니다.

[RouteData.Routers](xref:Microsoft.AspNetCore.Routing.RouteData.Routers*)는 성공적으로 요청 일치에 참여한 경로의 목록입니다. 경로는 서로 중첩될 수 있습니다. `Routers` 속성은 결과적으로 일치한 경로의 논리 트리를 통해 경로를 반영합니다. 일반적으로 `Routers`의 첫 번째 항목은 경로 컬렉션이며 URL 생성을 위해 사용되어야 합니다. `Routers`의 마지막 항목은 일치한 경로 처리기입니다.

### <a name="url-generation"></a>URL 생성

URL 생성은 라우팅이 경로 값의 집합을 기반으로 하는 URL 경로를 만들 수 있는 프로세스입니다. 따라서 처리기와 액세스하는 URL 간의 논리 구분을 허용합니다.

URL 생성은 비슷한 반복적인 프로세스를 따르지만 경로 컬렉션의 <xref:Microsoft.AspNetCore.Routing.IRouter.GetVirtualPath*> 메서드로 호출하는 사용자 또는 프레임워크 코드로 시작합니다. 각 *경로*는 null이 아닌 <xref:Microsoft.AspNetCore.Routing.VirtualPathData>가 반환될 때까지 시퀀스에서 호출된 해당 `GetVirtualPath` 메서드를 갖습니다.

`GetVirtualPath`에 대한 기본 입력은 다음과 같습니다.

* [VirtualPathContext.HttpContext](xref:Microsoft.AspNetCore.Routing.VirtualPathContext.HttpContext*)
* [VirtualPathContext.Values](xref:Microsoft.AspNetCore.Routing.VirtualPathContext.Values*)
* [VirtualPathContext.AmbientValues](xref:Microsoft.AspNetCore.Routing.VirtualPathContext.AmbientValues*)

경로는 주로 `Values` 및 `AmbientValues`에서 제공하는 경로 값을 사용하여 URL을 생성할 수 있는지 여부와 포함할 값을 결정합니다. `AmbientValues`는 현재 요청과 라우팅 시스템의 일치에서 생성된 경로 값의 집합입니다. 반면, `Values`는 현재 작업에 대한 원하는 URL을 생성하는 방법을 지정하는 경로 값입니다. `HttpContext`는 경로가 서비스 또는 현재 컨텍스트와 연결된 추가 데이터를 가져와야 할 경우에 제공됩니다.

> [!TIP]
> [VirtualPathContext.Values](xref:Microsoft.AspNetCore.Routing.VirtualPathContext.Values*)를 [VirtualPathContext.AmbientValues](xref:Microsoft.AspNetCore.Routing.VirtualPathContext.AmbientValues*)에 대한 재정의의 집합으로 생각합니다. URL 생성은 동일한 경로 또는 경로 값을 사용하여 링크에 대한 URL을 쉽게 생성할 수 있도록 현재 요청에서 경로 값을 다시 사용하려고 시도합니다.

`GetVirtualPath`의 출력은 `VirtualPathData`입니다. `VirtualPathData`는 `RouteData`의 병렬입니다. `VirtualPathData`는 출력 URL 및 경로에 의해 설정되어야 하는 몇 가지 추가 속성에 대한 `VirtualPath`를 포함합니다.

[VirtualPathData.VirtualPath](xref:Microsoft.AspNetCore.Routing.VirtualPathData.VirtualPath*) 속성은 경로에 의해 생성된 *가상 경로*를 포함합니다. 필요에 따라 경로를 추가로 처리해야 합니다. HTML에서 생성된 URL을 렌더링하려는 경우 앱의 기본 경로를 추가합니다.

[VirtualPathData.Router](xref:Microsoft.AspNetCore.Routing.VirtualPathData.Router*)는 성공적으로 URL을 생성한 경로에 대한 참조입니다.

[VirtualPathData.DataTokens](xref:Microsoft.AspNetCore.Routing.VirtualPathData.DataTokens*) 속성은 URL을 생성한 경로와 관련된 추가 데이터의 사전입니다. 이는 [RouteData.DataTokens](xref:Microsoft.AspNetCore.Routing.RouteData.DataTokens*)의 병렬입니다.

### <a name="creating-routes"></a>경로 만들기

라우팅은 <xref:Microsoft.AspNetCore.Routing.IRouter>의 표준 구현으로 <xref:Microsoft.AspNetCore.Routing.Route> 클래스를 제공합니다. `Route`는 *경로 템플릿* 구문을 사용하여 <xref:Microsoft.AspNetCore.Routing.IRouter.RouteAsync*>가 호출되었을 때 URL 경로에 대해 일치하는 패턴을 정의합니다. `Route`는 동일한 경로 템플릿을 사용하여 `GetVirtualPath`가 호출되었을 때 URL을 생성합니다.

대부분의 앱은 <xref:Microsoft.AspNetCore.Builder.MapRouteRouteBuilderExtensions.MapRoute*> 또는 <xref:Microsoft.AspNetCore.Routing.IRouteBuilder>에 정의된 유사한 확장 메서드 중 하나를 호출하여 경로를 만듭니다. 이러한 모든 메서드는 <xref:Microsoft.AspNetCore.Routing.Route>의 인스턴스를 만들고 경로 컬렉션에 추가합니다.

`MapRoute`는 경로 처리기 매개 변수를 사용하지 않습니다. `MapRoute`는 <xref:Microsoft.AspNetCore.Routing.RouteBuilder.DefaultHandler*>에 의해 처리되는 경로만 추가합니다. 기본 처리기는 `IRouter`이므로 요청을 처리하지 않도록 결정할 것입니다. 예를 들어 ASP.NET Core MVC는 일반적으로 사용 가능한 컨트롤러 및 작업과 일치하는 요청만 처리하는 기본 처리기로 구성됩니다. MVC로 라우팅에 대해 자세히 알아보려면 <xref:mvc/controllers/routing>을 참조하세요.

다음 코드 예제는 일반적인 ASP.NET Core MVC 경로 정의에서 사용되는 `MapRoute` 호출의 예제입니다.

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id?}");
```

이 템플릿은 `/Products/Details/17`과 같이 URL 경로와 일치시키고 경로 값 `{ controller = Products, action = Details, id = 17 }`을 추출합니다. 경로 값은 URL 경로를 세그먼트로 분할하고 각 세그먼트를 경로 템플릿의 *경로 매개 변수* 이름과 일치시켜 결정됩니다. 경로 매개 변수의 이름이 지정됩니다. 중괄호 `{ ... }`로 매개 변수 이름을 묶어 정의됩니다.

위의 템플릿은 URL 경로 `/`와 일치시킬 수도 있으며 값 `{ controller = Home, action = Index }`를 생성합니다. 이는 `{controller}` 및 `{action}` 경로 매개 변수에 기본값이 있으며 `id` 경로 매개 변수는 선택 사항이기 때문에 발생합니다. 경로 매개 변수 이름 뒤에 값이 뒤에 오는 등호(`=`) 기호는 매개 변수에 대한 기본값을 정의합니다. 경로 매개 변수 이름 뒤의 물음표(`?`)는 선택적으로 매개 변수를 정의합니다. 기본 값을 사용하는 경로 매개 변수는 경로가 일치하는 경우 *항상* 경로 값을 생성합니다. 해당 URL 경로 세그먼트가 없는 경우 선택적 매개 변수는 경로 값을 생성하지 않습니다.

경로 템플릿 기능 및 구문의 세부적 설명은 [경로 템플릿 참조](#route-template-reference)를 참조하세요.

이 예제는 *경로 제약 조건*을 포함합니다.

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id:int}");
```

이 템플릿은 `/Products/Details/Apples`가 아닌 `/Products/Details/17`과 같이 URL 경로와 일치시킵니다. 경로 매개 변수 정의 `{id:int}`는 `id` 경로 매개 변수에 대한 [경로 제약 조건](#route-constraint-reference)을 정의합니다. 경로 제약 조건은 <xref:Microsoft.AspNetCore.Routing.IRouteConstraint>를 구현하고 경로 값을 검사하여 확인합니다. 이 예제에서 경로 값 `id`는 정수로 변환할 수 있어야 합니다. 프레임워크에서 제공되는 경로 제약 조건에 대한 자세한 설명은 [경로 제약 조건 참조](#route-constraint-reference)를 참조하세요.

`MapRoute`의 추가 오버로드는 `constraints`, `dataTokens` 및 `defaults`에 대한 값을 허용합니다. 이러한 `MapRoute`의 추가 매개 변수는 `object` 형식으로 정의됩니다. 이러한 매개 변수의 일반적인 사용법은 익명 형식의 속성 이름이 경로 매개 변수 이름과 일치하는 익명으로 형식화된 개체를 전달하는 것입니다.

다음 두 예제는 해당 경로를 만듭니다.

```csharp
routes.MapRoute(
    name: "default_route",
    template: "{controller}/{action}/{id?}",
    defaults: new { controller = "Home", action = "Index" });

routes.MapRoute(
    name: "default_route",
    template: "{controller=Home}/{action=Index}/{id?}");
```

> [!TIP]
> 제약 조건 및 기본값을 정의하기 위한 인라인 구문은 단순 경로에 편리할 수 있습니다. 그러나 인라인 구문에서 지원되지 않는 데이터 토큰 등의 기능이 있습니다.

다음 예제에서는 몇 가지 더 많은 시나리오를 보여줍니다.

```csharp
routes.MapRoute(
    name: "blog",
    template: "Blog/{*article}",
    defaults: new { controller = "Blog", action = "ReadArticle" });
```

이 템플릿은 `/Blog/All-About-Routing/Introduction`과 같이 URL 경로와 일치시키고 값 `{ controller = Blog, action = ReadArticle, article = All-About-Routing/Introduction }`을 추출합니다. `controller` 및 `action`에 대 한 기본 경로 값은 템플릿에 해당 경로 매개 변수가 없는 경우에도 경로에 의해 생성됩니다. 기본값은 경로 템플릿에서 지정될 수 있습니다. `article` 경로 매개 변수는 경로 매개 변수 이름 앞에 별표(`*`) 모양으로 *범용*으로 정의됩니다. 범용 경로 매개 변수는 URL 경로의 나머지를 캡처하고 빈 문자열과 일치시킬 수 있습니다.

이 예제는 경로 제약 조건 및 데이터 토큰을 추가합니다.

```csharp
routes.MapRoute(
    name: "us_english_products",
    template: "en-US/Products/{id}",
    defaults: new { controller = "Products", action = "Details" },
    constraints: new { id = new IntRouteConstraint() },
    dataTokens: new { locale = "en-US" });
```

이 템플릿은 `/en-US/Products/5`와 같은 URL 경로와 일치하고 값 `{ controller = Products, action = Details, id = 5 }` 및 데이터 토큰 `{ locale = en-US }`를 추출합니다.

![지역 Windows 토큰](routing/_static/tokens.png)

### <a name="url-generation"></a>URL 생성

`Route` 클래스는 경로 값의 집합을 해당 경로 템플릿과 결합하여 URL 생성을 수행할 수도 있습니다. 이는 논리적으로 URL 경로와 일치시키는 역방향 프로세스입니다.

> [!TIP]
> URL 생성을 보다 잘 이해하려면 생성하려는 URL을 가정한 다음, 경로 템플릿을 해당 URL과 일치시키는 방법을 생각합니다. 어떤 값이 생성되나요? 이는 URL 생성이 `Route` 클래스에서 작동하는 방식과 대략적으로 동일합니다.

이 예제에서는 기본 ASP.NET Core MVC 스타일 경로를 사용합니다.

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id?}");
```

`{ controller = Products, action = List }`의 경로 값으로 이 경로는 URL `/Products/List`를 생성합니다. 경로 값은 URL 경로를 구성하기 위해 해당 경로 매개 변수에 대해 대체됩니다. `id`는 선택적 매개 변수이므로 값이 없어도 문제가 되지 않습니다.

`{ controller = Home, action = Index }`의 경로 값으로 이 경로는 URL `/`를 생성합니다. 제공된 경로 값은 기본값과 일치하므로 해당 값에 해당하는 세그먼트는 안전하게 생략될 수 있습니다. 생성된 두 URL은 이 경로 정의로 왕복하며 URL을 생성하는 데 사용된 동일한 경로 값을 생성합니다.

> [!TIP]
> ASP.NET Core MVC를 사용하는 앱은 <xref:Microsoft.AspNetCore.Mvc.Routing.UrlHelper>를 사용하여 라우팅으로 직접 호출하는 대신 URL을 생성해야 합니다.

URL 생성에 대한 자세한 내용은 [url-generation-reference](#url-generation-reference)를 참조하세요.

## <a name="use-routing-middleware"></a>라우팅 미들웨어 사용

::: moniker range=">= aspnetcore-2.1"

앱의 프로젝트 파일에서 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)를 참조하세요.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

앱의 프로젝트 파일에서 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)를 참조하세요.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

앱의 프로젝트 파일에서 [Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)을 참조하세요.

::: moniker-end

`Startup.ConfigureServices`의 서비스 컨테이너에 라우팅을 추가합니다.

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](routing/samples/2.x/RoutingSample/Startup.cs?name=snippet_ConfigureServices&highlight=3)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](routing/samples/1.x/RoutingSample/Startup.cs?name=snippet_ConfigureServices&highlight=3)]

::: moniker-end

경로는 `Startup.Configure` 메서드에서 구성되어야 합니다. 샘플 앱에서는 이러한 API를 사용합니다.

* `RouteBuilder`
* `Build`
* `MapGet` &ndash; HTTP GET 요청만 일치시킵니다.
* `UseRouter`

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](routing/samples/2.x/RoutingSample/Startup.cs?name=snippet_RouteHandler)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](routing/samples/1.x/RoutingSample/Startup.cs?name=snippet_RouteHandler)]

::: moniker-end

다음 표는 지정된 URI로 응답을 보여줍니다.

| URI                  | 응답                                          |
| -------------------- | ------------------------------------------------- |
| /package/create/3    | Hello! 경로 값: [작업, 만들기], [id, 3] |
| /package/track/-3    | Hello! 경로 값: [작업, 트랙], [id, -3] |
| /package/track/-3/   | Hello! 경로 값: [작업, 트랙], [id, -3] |
| /package/track/      | &lt;실패, 일치하지 않음&gt;                    |
| GET /hello/Joe       | Hi, Joe!                                          |
| POST /hello/Joe      | &lt;실패, HTTP GET만 일치&gt;       |
| GET /hello/Joe/Smith | &lt;실패, 일치하지 않음&gt;                    |

단일 경로를 구성하는 경우 `IRouter` 인스턴스를 전달하는 <xref:Microsoft.AspNetCore.Builder.RoutingBuilderExtensions.UseRouter*>를 호출합니다. <xref:Microsoft.AspNetCore.Routing.RouteBuilder>를 사용할 필요가 없습니다.

프레임워크는 다음과 같은 경로를 만들기 위한 확장 메서드 집합을 제공합니다.

* `MapRoute`
* `MapGet`
* `MapPost`
* `MapPut`
* `MapDelete`
* `MapVerb`

`MapGet`과 같은 이러한 메서드의 일부는 `RequestDelegate`를 제공 받아야 합니다. `RequestDelegate`는 경로가 일치하는 경우 *경로 처리기*로 사용됩니다. 이 제품군의 다른 메서드는 경로 처리기로 사용할 미들웨어 파이프라인 구성을 허용합니다. *Map* 메서드가 `MapRoute`와 같은 처리기를 허용하지 않는 경우 <xref:Microsoft.AspNetCore.Routing.RouteBuilder.DefaultHandler*>를 사용합니다.

`Map[Verb]` 메서드는 제약 조건을 사용하여 메서드 이름에서 HTTP 동사에 대한 경로를 제한합니다. 예제는 <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapGet*> 및 <xref:Microsoft.AspNetCore.Routing.RequestDelegateRouteBuilderExtensions.MapVerb*>을 참조하세요.

## <a name="route-template-reference"></a>경로 템플릿 참조

중괄호(`{ ... }`) 내 토큰은 경로가 일치하는 경우 바인딩될 *경로 매개 변수*를 정의합니다. 경로 세그먼트에 둘 이상의 경로 매개 변수를 정의할 수 있지만 리터럴 값으로 구분되어야 합니다. 예를 들어 `{controller=Home}{action=Index}`는 `{controller}` 및 `{action}` 사이에 리터럴 값이 없으므로 유효 경로일 수 없습니다. 이러한 경로 매개 변수는 이름이 있어야 하며 지정된 추가 특성을 가질 수 있습니다.

경로 매개 변수 이외의 리터럴 텍스트(예: `{id}`) 및 경로 구분 기호(`/`)는 URL의 텍스트와 일치해야 합니다. 텍스트 일치는 대/소문자를 구분하지 않으며 URL 경로의 디코딩된 표현을 기반으로 합니다. 리터럴 경로 매개 변수 구분 기호 `{` 또는 `}`와 일치시키려면 문자(`{{` 또는 `}}`)를 반복하여 이스케이프합니다.

선택적 파일 확장명을 가진 파일 이름 캡처를 시도하는 URL 패턴에는 추가 고려 사항이 있습니다. 예를 들어 템플릿 `files/{filename}.{ext?}`를 가정해 보겠습니다. `filename` 및 `ext`가 모두 존재하는 경우 두 값이 채워집니다. URL에 `filename`만 존재하는 경우 마침표(`.`)는 선택 사항이므로 경로가 일치합니다. 다음 URL은 이 경로와 일치합니다.

* `/files/myFile.txt`
* `/files/myFile`

경로 매개 변수에 대한 접두사로 `*` 문자를 사용하여 URI의 나머지 부분에 바인딩할 수 있습니다. 이를 *범용* 매개 변수라고 합니다. 예를 들어 `blog/{*slug}`는 `/blog`로 시작하는 모든 URI와 일치하며 다음 값이 뒤에 옵니다(`slug` 경로 값에 할당됨). 범용 매개 변수는 빈 문자열과 일치시킬 수도 있습니다.

::: moniker range=">= aspnetcore-2.2"

catch-all 매개 변수는 경로 구분 기호(`/`) 문자를 포함하여 URL을 생성하는 데 경로가 사용될 때 적절한 문자를 이스케이프합니다. 예를 들어 경로 값이 `{ path = "my/path" }`인 경로 `foo/{*path}`는 `foo/my%2Fpath`를 생성합니다. 이스케이프된 슬래시에 주의하세요. 경로 구분 기호 문자를 왕복하려면 `**` 경로 매개 변수 접두사를 사용합니다. `{ path = "my/path" }`가 있는 경로 `foo/{**path}`은 `foo/my/path`를 생성합니다.

::: moniker-end

경로 매개 변수는 등호(`=`)로 구분된 매개 변수 이름 뒤에 기본값을 지정하여 지정된 *기본값*을 가질 수 있습니다. 예를 들어 `{controller=Home}`은 `controller`에 대한 기본값으로 `Home`을 정의합니다. URL에 매개 변수에 대한 값이 없는 경우 기본값이 사용됩니다. 기본값 뿐만 아니라 경로 매개 변수를 생략할 수 있으며, `id?`와 같이 매개 변수 이름의 끝에 물음표(`?`)를 추가하여 지정됩니다. 선택 사항 값과 기본 경로 매개 변수 간의 차이점은 기본값이 있는 경로 매개 변수는 항상 값을 생성한다는 점입니다. 선택적 매개 변수는 값이 요청 URL에 의해 제공되는 경우에만 값을 갖습니다.

::: moniker range=">= aspnetcore-2.2"

경로 매개 변수에는 URL에서 바인딩된 경로 값과 일치해야 한다는 제약 조건이 있을 수 있습니다. 경로 매개 변수 이름 뒤에 콜론(`:`)과 제약 조건 이름을 추가하여 경로 매개 변수에서 *인라인 제약 조건*을 지정합니다. 제약 조건에 인수가 필요한 경우 제약 조건 이름 뒤에서 괄호 `( )`로 묶입니다. 여러 인라인 제약 조건은 다른 콜론(`:`) 및 제약 조건 이름을 추가하여 지정될 수 있습니다. 제약 조건 이름 및 인수는 <xref:Microsoft.AspNetCore.Routing.IRouteConstraint>의 인스턴스를 만드는 <xref:Microsoft.AspNetCore.Routing.IInlineConstraintResolver> 서비스로 전달되어 URL 처리에서 사용합니다. 제약 조건 생성자에 서비스가 필요한 경우 해당 서비스는 종속성 주입의 앱 서비스에서 확인됩니다. 예를 들어 경로 템플릿 `blog/{article:minlength(10)}`는 인수 `10`으로 `minlength` 제약 조건을 지정합니다. 경로 제약 조건에 대한 자세한 내용 및 프레임워크에서 제공되는 제약 조건 목록은 [경로 제약 조건 참조](#route-constraint-reference) 섹션을 참조하세요.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

경로 매개 변수에는 URL에서 바인딩된 경로 값과 일치해야 한다는 제약 조건이 있을 수 있습니다. 경로 매개 변수 이름 뒤에 콜론(`:`)과 제약 조건 이름을 추가하여 경로 매개 변수에서 *인라인 제약 조건*을 지정합니다. 제약 조건에 인수가 필요한 경우 제약 조건 이름 뒤에서 괄호 `( )`로 묶입니다. 여러 인라인 제약 조건은 다른 콜론(`:`) 및 제약 조건 이름을 추가하여 지정될 수 있습니다. 제약 조건 이름 및 인수는 <xref:Microsoft.AspNetCore.Routing.IRouteConstraint>의 인스턴스를 만드는 <xref:Microsoft.AspNetCore.Routing.IInlineConstraintResolver> 서비스로 전달되어 URL 처리에서 사용합니다. 예를 들어 경로 템플릿 `blog/{article:minlength(10)}`는 인수 `10`으로 `minlength` 제약 조건을 지정합니다. 경로 제약 조건에 대한 자세한 내용 및 프레임워크에서 제공되는 제약 조건 목록은 [경로 제약 조건 참조](#route-constraint-reference) 섹션을 참조하세요.

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

경로 매개 변수에는 링크 및 일치 작업과 URI에 대한 페이지를 생성할 때 매개 변수 값을 변환하는 매개 변수 변환기가 있을 수도 있습니다. 제한 조건과 마찬가지로, 매개 변수 변환기는 경로 매개 변수 이름 뒤에 콜론(`:`)과 변환기 이름을 추가하여 라우트 매개 변수에 인라인으로 추가될 수 있습니다. 예를 들어 경로 템플릿 `blog/{article:slugify}`는 `slugify` 변환기를 지정합니다.

::: moniker-end

다음 표는 일부 경로 템플릿 및 해당 동작을 보여 줍니다.

| 경로 템플릿                         | 일치하는 URL 예제  | 노트                                                                  |
| -------------------------------------- | --------------------- | ---------------------------------------------------------------------- |
| hello                                  | /hello                | 단일 경로 `/hello`만 일치                                  |
| {Page=Home}                            | /                     | 일치 및 `Page`를 `Home`으로 설정                                      |
| {Page=Home}                            | /Contact              | 일치 및 `Page`를 `Contact`로 설정                                   |
| {controller}/{action}/{id?}            | /Products/List        | `Products` 컨트롤러 및 `List` 작업에 매핑                       |
| {controller}/{action}/{id?}            | /Products/Details/123 |  `Products` 컨트롤러 및 `Details` 작업에 매핑  123으로 설정된 `id` |
| {controller=Home}/{action=Index}/{id?} | /                     |  `Home` 컨트롤러 및 `Index` 메서드에 매핑, `id`는 무시됩니다.       |

템플릿 사용은 일반적으로 라우팅에 대한 가장 간단한 방식입니다. 제약 조건 및 기본값을 경로 템플릿 외부에서 지정할 수도 있습니다.

> [!TIP]
> [로깅](xref:fundamentals/logging/index)을 활성화하여 `Route`와 같은 기본 제공 라우팅 구현이 요청과 일치시키는 방법을 확인합니다.

## <a name="reserved-routing-names"></a>예약된 라우팅 이름

다음 키워드는 예약된 이름이므로 경로 이름 또는 매개 변수로 사용할 수 없습니다.

* `action`
* `area`
* `controller`
* `handler`
* `page`

## <a name="route-constraint-reference"></a>경로 제약 조건 참조

경로 제약 조건은 `Route`가 들어오는 URL의 구문과 일치시키고 URL 경로를 경로 값으로 토큰화할 때 실행됩니다. 일반적으로 경로 제약 조건은 경로 템플릿을 통해 연결된 경로 값을 검사하고 값 허용 여부에 대한 예/아니요 의사 결정을 내립니다. 일부 경로 제약 조건은 경로 값 외부의 데이터를 사용하여 요청을 라우팅할 수 있는지 여부를 고려합니다. 예를 들어 <xref:Microsoft.AspNetCore.Routing.Constraints.HttpMethodRouteConstraint>는 해당 HTTP 동사에 따라 요청을 허용하거나 거부할 수 있습니다.

> [!WARNING]
> 잘못된 입력으로 적절한 오류 메시지가 있는 *400 - 잘못된 요청* 대신 *404 - 찾을 수 없음* 응답이 발생하므로 **입력 유효성 검사**에 대해 제약 조건을 사용하지 마십시오. 경로 제약 조건은 특정 경로에 대한 입력의 유효성을 검사하는 데가 아닌 비슷한 경로 간을 **명확하게 구분하는 데** 사용됩니다.

다음 표는 일부 경로 제약 조건 및 예상되는 해당 동작을 보여 줍니다.

| 제약 조건 | 예 | 일치하는 예제 | 노트 |
| ---------- | ------- | --------------- | ----- |
| `int` | `{id:int}` | `123456789`, `-123456789`  | 임의의 정수와 일치 |
| `bool` | `{active:bool}` | `true`, `FALSE` | `true` 또는 `false` 일치(대/소문자 구분하지 않음) |
| `datetime` | `{dob:datetime}` | `2016-12-31`, `2016-12-31 7:32pm`  | 유효한 `DateTime` 값 일치(고정 문화권에서 - 경고 참조) |
| `decimal` | `{price:decimal}` | `49.99`, `-1,000.01` | 유효한 `decimal` 값 일치(고정 문화권에서 - 경고 참조) |
| `double` | `{weight:double}` | `1.234`, `-1,001.01e8` | 유효한 `double` 값 일치(고정 문화권에서 - 경고 참조) |
| `float` | `{weight:float}` | `1.234`, `-1,001.01e8` | 유효한 `float` 값 일치(고정 문화권에서 - 경고 참조) |
| `guid` | `{id:guid}` | `CD2C1638-1638-72D5-1638-DEADBEEF1638`, `{CD2C1638-1638-72D5-1638-DEADBEEF1638}` | 유효한 `Guid` 값 일치 |
| `long` | `{ticks:long}` | `123456789`, `-123456789` | 유효한 `long` 값 일치 |
| `minlength(value)` | `{username:minlength(4)}` | `Rick` | 문자열은 4자 이상이어야 합니다. |
| `maxlength(value)` | `{filename:maxlength(8)}` | `Richard` | 문자열은 8자 이하여야 합니다. |
| `length(length)` | `{filename:length(12)}` | `somefile.txt` | 문자열은 정확히 12자여야 합니다. |
| `length(min,max)` | `{filename:length(8,16)}` | `somefile.txt` | 문자열의 길이는 8자 이상이며 16자 이하여야 합니다. |
| `min(value)` | `{age:min(18)}` | `19` | 정수 값은 18자 이상이어야 합니다. |
| `max(value)` | `{age:max(120)}` | `91` | 정수 값은 120자 이하여야 합니다. |
| `range(min,max)` | `{age:range(18,120)}` | `91` | 정수 값은 18자 이상이며 120자 이하여야 합니다. |
| `alpha` | `{name:alpha}` | `Rick` | 문자열은 하나 이상의 알파벳 문자(`a`-`z`, 대/소문자 구분)로 구성되어야 합니다. |
| `regex(expression)` | `{ssn:regex(^\\d{{3}}-\\d{{2}}-\\d{{4}}$)}` | `123-45-6789` | 문자열은 정규식과 일치해야 합니다(정규식 정의에 대한 팁 참조). |
| `required` | `{name:required}` | `Rick` |  URL을 생성하는 동안 비-매개 변수 값이 있도록 하는 데 사용됨 |

콜론으로 구분된 여러 개의 제약 조건을 단일 매개 변수에 적용할 수 있습니다. 예를 들어 다음 제약 조건은 매개 변수를 1 이상의 정수 값으로 제한합니다.

```csharp
[Route("users/{id:int:min(1)}")]
public User GetUserById(int id) { }
```

> [!WARNING]
> CLR 형식(예: `int` 또는 `DateTime`)으로 변환되는 URL을 확인하는 경로 제약 조건은 항상 고정 문화권을 사용합니다. 이러한 제약 조건은 URL은 지역화될 수 없다고 가정합니다. 프레임워크에서 제공한 경로 제약 조건은 경로 값에 저장된 값을 수정하지 않습니다. URL에서 구문 분석되는 모든 경로 값은 문자열로 저장됩니다. 예를 들어 `float` 제약 조건은 경로 값을 부동으로 변환하려고 하지만 변환된 값은 부동으로 변환될 수 있는지 확인하는 데만 사용됩니다.

## <a name="regular-expressions"></a>정규식

ASP.NET Core 프레임워크는 정규식 생성자에 `RegexOptions.IgnoreCase | RegexOptions.Compiled | RegexOptions.CultureInvariant`를 추가합니다. 이러한 멤버에 대한 설명은 <xref:System.Text.RegularExpressions.RegexOptions>를 참조하세요.

정규식은 라우팅 및 C# 언어에서 사용하는 것과 유사한 구분 기호 및 토큰을 사용합니다. 정규식 토큰은 이스케이프되어야 합니다. 라우팅에서 `^\d{3}-\d{2}-\d{4}$` 정규식을 사용하려면 식은 `\` 문자열 이스케이프 문자를 이스케이프하도록 C# 원본 파일에서 `\\`로 입력된 `\` 문자를 가져야 합니다([약어 문자열 리터럴](/dotnet/csharp/language-reference/keywords/string)을 사용하지 않는 한). `{`, `}`, `[` 및 `]` 문자는 라우팅 매개 변수 구분 기호 문자를 이스케이프하도록 이중으로 처리하여 이스케이프되어야 합니다. 아래 표는 정규식 및 이스케이프된 버전을 보여 줍니다.

| 식            | 이스케이프됨                        |
| --------------------- | ------------------------------ |
| `^\d{3}-\d{2}-\d{4}$` | `^\\d{{3}}-\\d{{2}}-\\d{{4}}$` |
| `^[a-z]{2}$`          | `^[[a-z]]{{2}}$`               |

라우팅에 사용된 정규식은 종종 `^` 문자(문자열의 시작 위치와 일치)로 시작하고 `$` 문자(문자열의 끝 위치와 일치)로 끝납니다. `^` 및 `$` 문자는 정규식이 전체 경로 매개 변수 값과 일치하도록 합니다. `^` 및 `$` 문자 없이 정규식은 문자열 내의 모든 하위 문자열과 일치합니다. 이는 종종 원하는 것이 아닙니다. 아래 표는 몇 가지 예를 보여 주고 일치하거나 일치에 실패하는 이유를 설명합니다.

| 식   | 문자열    | 일치 | 주석               |
| ------------ | --------- |  ---- |  -------------------- |
| `[a-z]{2}`   | hello     | 예   | 부분 문자열 일치     |
| `[a-z]{2}`   | 123abc456 | 예   | 부분 문자열 일치     |
| `[a-z]{2}`   | mz        | 예   | 식 일치    |
| `[a-z]{2}`   | MZ        | 예   | 대/소문자 구분하지 않음    |
| `^[a-z]{2}$` |  hello    | 아니요    | 위의 `^` 및 `$` 참조 |
| `^[a-z]{2}$` | 123abc456 | 아니요    | 위의 `^` 및 `$` 참조 |

정규식 구문에 대한 자세한 내용은 [.NET Framework 정규식](/dotnet/standard/base-types/regular-expression-language-quick-reference)을 참조하세요.

가능한 값의 알려진 집합으로 매개 변수를 제한하려면 정규식을 사용합니다. 예를 들어 `{action:regex(^(list|get|create)$)}`는 `action` 경로 값을 `list`, `get` 또는 `create`으로만 일치시킵니다. 제약 조건 사전으로 전달되면 `^(list|get|create)$` 문자열은 동일합니다. 알려진 제약 조건 중 하나와 일치하지 않는 제약 조건 사전(템플릿 내 인라인이 아님)에서 전달되는 제약 조건도 정규식으로 처리됩니다.

::: moniker range=">= aspnetcore-2.2"

## <a name="parameter-transformer-reference"></a>매개 변수 변환기 참조

매개 변수 변환기:

* `Route`에 대한 링크를 생성할 때 실행합니다.
* `Microsoft.AspNetCore.Routing.IOutboundParameterTransformer`를 구현해야 합니다.
* <xref:Microsoft.AspNetCore.Routing.RouteOptions.ConstraintMap>을 사용하여 구성됩니다.
* 매개 변수의 경로 값을 가져와서 새 문자열 값으로 변환합니다.
* 변환된 값은 생성된 링크에서 사용됩니다.

예를 들어, `Url.Action(new { article = "MyTestArticle" })`을 사용하는 경로 패턴 `blog\{article:slugify}`의 사용자 지정 `slugify` 매개 변수 변환기는 `blog\my-test-article`을 생성합니다.

또한 매개 변수 변환기는 엔드포인트가 확인되는 URI를 변환하기 위해 프레임워크에서 사용합니다. 예를 들어 ASP.NET Core MVC는 매개 변수 변환기를 사용하여 `area` , `controller` , `action` 및 `page`와 일치하도록 사용되는 경로 값을 변환합니다.

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home:slugify}/{action=Index:slugify}/{id?}");
```

이전 경로를 사용하면 `SubscriptionManagementController.GetAll()` 작업이 URI `/subscription-management/get-all`과 일치됩니다. 매개 변수 변환기는 링크를 생성하는 데 사용되는 경로 값을 변경하지 않습니다. `Url.Action("GetAll", "SubscriptionManagement")`가 `/subscription-management/get-all`을 출력합니다.

ASP.NET Core는 생성된 경로가 있는 매개 변수 변환기를 사용하기 위한 API 규칙을 제공합니다.

* ASP.NET Core MVC에는 `Microsoft.AspNetCore.Mvc.ApplicationModels.RouteTokenTransformerConvention` API 규칙이 있습니다. 이 규칙은 앱의 모든 특성 경로에 지정된 매개 변수 변환기를 적용합니다. 매개 변수 변환기는 특성 경로 토큰이 교체될 때 변환합니다. 자세한 내용은 [매개 변수 변환기를 사용하여 토큰 교체 사용자 지정](/aspnet/core/mvc/controllers/routing#use-a-parameter-transformer-to-customize-token-replacement)을 참조하세요.
* Razor 페이지에는 `Microsoft.AspNetCore.Mvc.ApplicationModels.PageRouteTransformerConvention` API 규칙이 있습니다. 이 규칙은 자동으로 검색된 모든 Razor 페이지에 지정된 매개 변수 변환기를 적용합니다. 매개 변수 변환기는 Razor 페이지 경로의 폴더와 파일 이름 부분을 변환합니다. 자세한 내용은 [매개 변수 변환기를 사용하여 페이지 경로 사용자 지정](/aspnet/core/razor-pages/razor-pages-conventions#use-a-parameter-transformer-to-customize-page-routes)을 참조하세요.

::: moniker-end

## <a name="url-generation-reference"></a>URL 생성 참조

다음 예제에서는 경로 값의 사전 및 <xref:Microsoft.AspNetCore.Routing.RouteCollection>이 지정된 경로에 대한 링크를 생성하는 방법을 보여줍니다.

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](routing/samples/2.x/RoutingSample/Startup.cs?name=snippet_Dictionary)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](routing/samples/1.x/RoutingSample/Startup.cs?name=snippet_Dictionary)]

::: moniker-end

위의 샘플 끝부분에서 생성된 `VirtualPath`는 `/package/create/123`입니다. 사전은 "추적 패키지 경로" 템플릿, `package/{operation}/{id}`의 `operation` 및 `id` 경로 값을 제공합니다. 자세한 내용은 [라우팅 미들웨어 사용](#use-routing-middleware) 섹션의 샘플 코드 또는 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/routing/samples)을 참조하세요.

`VirtualPathContext` 생성자에 대한 두 번째 매개 변수는 *앰비언트 값*의 컬렉션입니다. 앰비언트 값은 개발자가 특정 요청 컨텍스트 내에서 지정해야 하는 값의 수를 제한하여 편의를 제공합니다. 현재 요청의 현재 경로 값은 링크 생성에 대한 앰비언트 값으로 간주됩니다. ASP.NET Core MVC 앱에서 `HomeController`의 `About` 작업 중에 있는 경우 `Index` 작업에 연결하도록 컨트롤러 경로 값을 지정할 필요가 없습니다. &mdash;`Home`의 앰비언트 값이 사용됩니다.

매개 변수와 일치하지 않는 앰비언트 값은 무시되며 URL에서 왼쪽에서 오른쪽으로 이동하여 명시적으로 제공된 값이 재정의하는 경우 앰비언트 값도 무시됩니다.

명시적으로 제공되었지만 아무 것과도 일치하지 않는 값은 쿼리 문자열에 추가됩니다. 다음 표에서 경로 템플릿 `{controller}/{action}/{id?}`를 사용하는 경우 결과를 보여 줍니다.

| 앰비언트 값                | 명시적 값                   | 결과                  |
| ----------------------------- | --------------------------------- | ----------------------- |
| controller="Home"             | action="About"                    | `/Home/About`           |
| controller="Home"             | controller="Order",action="About" | `/Order/About`          |
| controller="Home",color="Red" | action="About"                    | `/Home/About`           |
| controller="Home"             | action="About",color="Red"        | `/Home/About?color=Red` |

경로에 매개 변수에 해당하지 않고 값이 명시적으로 제공된 기본값이 있는 경우 기본값과 일치해야 합니다.

```csharp
routes.MapRoute("blog_route", "blog/{*slug}",
    defaults: new { controller = "Blog", action = "ReadPost" });
```

링크 생성은 컨트롤러 및 작업에 대해 일치하는 값이 제공되는 경우에만 이 경로에 대한 링크를 생성합니다.
