---
title: "ASP.NET Core 미들웨어 기본 사항"
author: rick-anderson
description: "ASP.NET Core의 미들웨어와 요청 파이프라인에 관해서 알아봅니다."
keywords: "ASP.NET Core, 미들웨어, 파이프라인, 대리자"
ms.author: riande
manager: wpickett
ms.date: 10/14/2017
ms.topic: article
ms.assetid: db9a86ab-46c2-40e0-baed-86e38c16af1f
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/middleware
ms.openlocfilehash: 730b4c281a766059b16ca1c36bbeb9611b979b72
ms.sourcegitcommit: 0f23400cae837e90927043aa0dfd6c31108a4e2c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2017
---
# <a name="aspnet-core-middleware-fundamentals"></a>ASP.NET Core 미들웨어 기본 사항

<a name=fundamentals-middleware></a>

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Steve Smith](https://ardalis.com/)

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="what-is-middleware"></a>미들웨어란?

미들웨어는 응용 프로그램의 파이프라인으로 조립되어 요청 및 응답을 처리하는 소프트웨어입니다. 각 구성 요소는.

* 파이프라인의 다음 구성 요소로 요청을 전달할지 여부를 선택합니다.
* 파이프라인의 다음 구성 요소가 호출되기 이전 및 이후에 특정 동작을 수행할 수 있습니다. 

요청 파이프라인은 요청 대리자를 통해서 구축됩니다. 그리고 요청 대리자는 각각의 HTTP 요청을 처리합니다. 

요청 대리자는 [Run](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.runextensions), [Map](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapextensions) 및 [Use](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.useextensions) 확장 메서드를 이용해서 구성됩니다. 각각의 요청 대리자는 인라인 익명 메서드로 지정될 수도 있고 (이를 인라인 미들웨어라고 합니다), 재사용 가능한 별도의 클래스로 정의될 수도 있습니다. 이런 재사용 가능한 클래스와 인라인 익명 메서드를 *미들웨어* 또는 *미들웨어 구성 요소*라고 합니다. 요청 파이프라인의 각 미들웨어 구성 요소는 파이프라인의 다음 구성 요소를 호출하거나, 필요한 경우 적절한 방식으로 호출 체인을 중단하고 빠져나가야 (Short-Circuiting) 합니다.

[HTTP 모듈을 미들웨어로 마이그레이션하기](../migration/http-modules.md)에서는 ASP.NET Core 및 이전 버전의 요청 파이프라인의 차이점을 설명하고, 다양한 미들웨어 예제를 살펴봅니다.

## <a name="creating-a-middleware-pipeline-with-iapplicationbuilder"></a>IApplicationBuilder로 미들웨어 파이프라인 생성하기

ASP.NET Core의 요청 파이프라인은 다음 다이어그램에서 볼 수 있는 것처럼, 순차적으로 다른 요청 대리자를 호출하는 일련의 요청 대리자들로 구성됩니다 (실행 흐름은 검은색 화살표를 따릅니다).

![요청이 전달되고, 세 가지 미들웨어를 통해서 처리된 다음, 응용 프로그램에서 응답이 나가는 요청 처리 패턴을 보여줍니다. 각각의 미들웨어는 자신의 로직을 실행하고 next() 구문을 통해서 다음 미들웨어로 요청을 전달합니다. 세 번째 미들웨어가 요청을 처리하고 나면, 클라이언트에 대한 응답이 응용 프로그램을 떠나기 전에, 다시 차례대로 next () 구문 이후의 추가적인 처리를 위해, 이전 두 개의 미들웨어를 통해서 다시 전달됩니다.](middleware/_static/request-delegate-pipeline.png)

각각의 대리자는 다음 대리자가 호출되기 전이나 후에 작업을 수행할 수 있습니다. 또한 대리자는 요청을 다음 대리자로 전달하지 않기로 결정할 수도 있는데, 이를 요청 파이프라인을 중단하고 빠져나간다(Short-Circuiting)고 합니다. 불필요한 작업을 수행할 필요가 없으면 요청 파이프라인을 중단하고 빠져나가는 것이 바람직한 경우가 많습니다. 예를 들어, 정적 파일 미들웨어는 정적 파일에 대한 요청을 반환한 다음, 파이프라인의 나머지 미들웨어를 실행하지 않고 그대로 빠져나갑니다. 그리고 예외 처리 대리자는 파이프라인의 초기에 호출돼야 하는데, 그래야만 파이프라인의 이후 단계에서 발생하는 예외를 잡을 수 있기 때문입니다.

가장 간단한 ASP.NET Core 응용 프로그램은 모든 요청을 처리하는 단일 요청 대리자만 설정하는 경우입니다. 이 경우에는 사실상 요청 파이프라인이 존재하지 않는 것으로 봐도 무방합니다. 대신, 모든 HTTP 요청에 대한 응답으로 단일 익명 함수가 호출됩니다.

[!code-csharp[Main](middleware/sample/Middleware/Startup.cs)]

이 첫 번째 [app.Run](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.runextensions) 대리자는 파이프라인을 그대로 종료합니다.

반면 [app.Use](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.useextensions)를 사용하면 다수의 요청 대리자를 서로 연결할 수 있습니다. 이때, `next` 매개 변수는 파이프라인의 다음 대리자를 나타냅니다. (*next* 매개 변수를 *호출하지 않음*으로써 파이프라인을 중단하고 빠져나갈 수 있다는 점을 기억해두시기 바랍니다.) 다음 예제에서 볼 수 있는 것처럼, 일반적으로 다음 대리자를 호출하기 전과 후에 필요한 작업을 수행합니다.

[!code-csharp[Main](middleware/sample/Chain/Startup.cs?name=snippet1)]

>[!WARNING]
> 일단 응답이 클라이언트로 전송된 후에는 `next.Invoke`를 호출하면 안됩니다. 응답이 전송되기 시작된 뒤에 `HttpResponse`를 변경하면 예외가 발생합니다. 예를 들어, 헤더나 상태 코드 등을 설정하면 예외가 발생합니다. 또한 `next`를 호출한 뒤에 응답 본문을 작성하면 다음과 같은 사항이 발생합니다.
> - 프로토콜 위반이 발생할 수 있습니다. 예를 들어, 명시된 `content-length`보다 긴 내용이 작성될 수 있습니다.
> - 본문의 형식이 손상될 수 있습니다. 예를 들어, CSS 파일에 HTML 바닥글이 작성될 수 있습니다.
>
> [HttpResponse.HasStarted](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.features.httpresponsefeature#Microsoft_AspNetCore_Http_Features_HttpResponseFeature_HasStarted)는 헤더가 이미 전송됐는지 또는 본문이 이미 작성됐는지 여부를 나타내는 유용한 힌트를 제공해줍니다.

## <a name="ordering"></a>순서

`Configure` 메서드에서 미들웨어 구성 요소가 추가되는 순서에 의해 미들웨어의 호출 순서가 결정되는데, 요청 시에는 추가된 순서대로 호출되고 응답 시에는 그 역순으로 호출됩니다. 이 순서 지정은 보안, 성능 및 기능에 민감한 영향을 줍니다.

다음 예제의 `Configure` 메서드는 다음과 같은 미들웨어 구성 요소들를 추가합니다:

1. 예외/오류 처리
2. 정적 파일 서버
3. 인증
4. MVC

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)


```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseExceptionHandler("/Home/Error"); // Call first to catch exceptions
                                            // thrown in the following middleware.

    app.UseStaticFiles();                   // Return static files and end pipeline.

    app.UseAuthentication();                // Authenticate before you access
                                            // secure resources.

    app.UseMvcWithDefaultRoute();           // Add MVC to the request pipeline.
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseExceptionHandler("/Home/Error"); // Call first to catch exceptions
                                            // thrown in the following middleware.

    app.UseStaticFiles();                   // Return static files and end pipeline.

    app.UseIdentity();                      // Authenticate before you access
                                            // secure resources.

    app.UseMvcWithDefaultRoute();           // Add MVC to the request pipeline.
}
```

-----------

위의 코드에서 파이프라인에 추가되는 첫 번째 미들웨어 구성 요소는 `UseExceptionHandler`입니다. 따라서 이후에 호출되는 모든 미들웨어에서 발생하는 모든 예외를 잡을 수 있습니다.

정적 파일 미들웨어는 파이프라인의 초기에 호출되어 정적 파일에 대한 요청을 처리한 다음, 나머지 구성 요소를 거치지 않고 파이프라인을 중단하고 빠져나갑니다. 또한 정적 파일 미들웨어는 권한 부여 검사를 **제공하지 않습니다**. *wwwroot* 디렉터리 하위의 파일을 비롯해서 이 미들웨어가 제공하는 모든 파일은 공개적으로 사용 가능합니다. 정적 파일의 보안 방법에 대해서는 [정적 파일 작업하기](xref:fundamentals/static-files)를 참고하시기 바랍니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

정적 파일 미들웨어에 의해서 처리되지 않은 요청은 인증을 수행하는 Identity 미들웨어로 (`app.UseAuthentication`) 전달됩니다. 그러나 Identity 미들웨어가 인증되지 않은 요청을 중단하고 빠져나가는 것은 아닙니다. Identity가 요청을 인증하기는 하지만, MVC가 특정 Razor 페이지 또는 컨트롤러 및 액션을 선택한 뒤에야 권한 부여가 (또는 거부가) 발생합니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

정적 파일 미들웨어에 의해서 처리되지 않은 요청은 인증을 수행하는 Identity 미들웨어로 (`app.UseIdentity`) 전달됩니다. 그러나 Identity 미들웨어가 인증되지 않은 요청을 중단하고 빠져나가는 것은 아닙니다. Identity가 요청을 인증하기는 하지만, MVC가 특정 컨트롤러 및 액션을 선택한 뒤에야 권한 부여가 (또는 거부가) 발생합니다.

-----------

다음 예제는 응답 압축 미들웨어 이전에 정적 파일 미들웨어에 의해서 정적 파일에 대한 요청이 처리되는 미들웨어 순서를 보여줍니다. 미들웨어의 순서가 이렇게 구성된 상태에서는 정적 파일이 압축되지 않습니다. 반면 [UseMvcWithDefaultRoute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_)의 응답은 압축될 수 있습니다.

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseStaticFiles();         // Static files not compressed
                                  // by middleware.
    app.UseResponseCompression();
    app.UseMvcWithDefaultRoute();
}
```

<a name=middleware-run-map-use></a>

### <a name="use-run-and-map"></a>Run, Map 및 Use

HTTP 파이프라인은 `Use`, `Run`, 및 `Map`을 이용해서 구성합니다. `Use`는 파이프라인을 중단하고 빠져나갈 수 있습니다 (즉, next 요청 대리자를 호출하지 않을 수 있습니다). `Run`이라는 이름은 규약으로, 일부 미들웨어 구성 요소는 파이프라인의 가장 마지막에 실행되는 `Run[Middleware]` 메서드를 노출합니다.

`Map*` 확장은 파이프라인을 분기하기 위한 규약으로 사용됩니다. [Map](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapextensions)은 지정한 요청 경로와 일치하는지 여부에 따라 요청 파이프라인을 분기합니다. 만약 요청 경로가 지정한 경로로 시작하면 해당 분기가 실행됩니다.

[!code-csharp[Main](middleware/sample/Chain/StartupMap.cs?name=snippet1)]

다음 표는 위의 코드를 사용할 경우, `http://localhost:1234`에 대한 요청 및 응답을 보여줍니다.

| 요청 | 응답 |
| --- | --- |
| localhost:1234 | Hello from non-Map delegate. |
| localhost:1234/map1 | Map Test 1 |
| localhost:1234/map2 | Map Test 2 |
| localhost:1234/map3 | Hello from non-Map delegate. |

`Map`을 사용하면, 각 요청마다 일치하는 경로 세그먼트가 `HttpRequest.Path`에서 제거되고 `HttpRequest.PathBase`에 추가됩니다.

[MapWhen](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapwhenextensions)은 지정한 조건자의 결과에 따라서 요청 파이프라인을 분기합니다. `Func<HttpContext, bool>` 형식의 조건자를 지정해서 파이프라인의 새로운 분기로 요청을 맵핑할 수 있습니다. 다음 예제는 조건자를 이용해서 `branch`라는 쿼리 문자열 변수가 존재하는지 여부를 감지합니다.

[!code-csharp[Main](middleware/sample/Chain/StartupMapWhen.cs?name=snippet1)]

다음 표는 위의 코드를 사용할 경우, `http://localhost:1234`에 대한 요청 및 응답을 보여줍니다.

| 요청 | 응답 |
| --- | --- |
| localhost:1234 | Hello from non-Map delegate. |
| localhost:1234/?branch=master | Branch used = master |

다음 예제와 같이 `Map`은 중첩도 지원합니다.

```csharp
app.Map("/level1", level1App => {
       level1App.Map("/level2a", level2AApp => {
           // "/level1/level2a"
           //...
       });
       level1App.Map("/level2b", level2BApp => {
           // "/level1/level2b"
           //...
       });
   });
   ```

`Map`은 한 번에 여러 단계로 구성된 세그먼트도 지원합니다.

 ```csharp
app.Map("/level1/level2", HandleMultiSeg);
```

## <a name="built-in-middleware"></a>기본 제공 미들웨어

ASP.NET Core는 기본적으로 다음과 같은 미들웨어 구성 요소를 제공합니다.

| 미들웨어 | 설명 |
| ----- | ------- |
| [인증](xref:security/authentication/identity) | 인증 기능을 제공합니다. |
| [CORS](xref:security/cors) | 원본간 리소스 공유(CORS)를 구성합니다. |
| [응답 캐싱](xref:performance/caching/middleware) | 응답을 캐시하는 기능을 제공합니다. |
| [응답 압축](xref:performance/response-compression) | 응답을 압축하는 기능을 제공합니다. |
| [라우팅](xref:fundamentals/routing) | 요청 경로를 정의하고 제한합니다. |
| [세션](xref:fundamentals/app-state) | 사용자 세션 관리 기능을 제공합니다. |
| [정적 파일](xref:fundamentals/static-files) | 정적 파일 및 디렉터리 브라우징 기능을 제공합니다. |
| [URL 재작성 미들웨어](xref:fundamentals/url-rewriting) | URL 재작성 및 요청 리디렉션 기능을 제공합니다. |

<a name=middleware-writing-middleware></a>

## <a name="writing-middleware"></a>미들웨어 구현하기

일반적으로 미들웨어는 클래스로 캡슐화되어 확장 메서드와 함께 제공됩니다. 쿼리 문자열에 지정된 정보를 이용해서 현재 요청에 대한 문화권을 설정하는 다음 미들웨어를 살펴보시기 바랍니다.

[!code-csharp[Main](middleware/sample/Culture/StartupCulture.cs?name=snippet1)]

참고: 위의 예제 코드는 미들웨어 구성 요소를 생성하는 방법을 보여주기 위한 용도로 작성된 것입니다. ASP.NET Core의 기본 제공 지역화 기능에 관해서는 [전역화 및 지역화](xref:fundamentals/localization)를 참고하시기 바랍니다.

`http://localhost:7997/?culture=no` 같이 쿼리 문자열에 문화권을 지정해서 미들웨어를 테스트해 볼 수 있습니다.

계속해서 다음 코드는 이 미들웨어 대리자를 클래스로 구현한 것입니다.

[!code-csharp[Main](middleware/sample/Culture/RequestCultureMiddleware.cs)]

그리고 다음 확장 메서드는 [IApplicationBuilder](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.iapplicationbuilder)를 통해서 이 미들웨어를 노출합니다.

[!code-csharp[Main](middleware/sample/Culture/RequestCultureMiddlewareExtensions.cs)]

마지막으로 다음 코드는 `Configure` 메서드에서 미들웨어를 호출합니다.

[!code-csharp[Main](middleware/sample/Culture/Startup.cs?name=snippet1&highlight=5)]

미들웨어는 자신의 종속성을 생성자에 명시함으로써 [명시적 종속성 원칙](http://deviq.com/explicit-dependencies-principle/)을 준수해야 합니다. 기본적으로 미들웨어는 *응용 프로그램의 수명* 당 단 한 번만 생성됩니다. 요청 내에서 미들웨어와 서비스를 공유해야 한다면, 아래의 *요청별 종속성*을 참고하시기 바랍니다.

미들웨어 구성 요소는 생성자 매개 변수를 통해서 종속성 주입으로 자신의 종속성을 해결할 수 있습니다. 또한 [`UseMiddleware<T>`](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.usemiddlewareextensions#methods_summary)를 이용해서 추가적인 매개 변수를 직접 전달받을 수도 있습니다.

### <a name="per-request-dependencies"></a>요청별 종속성

미들웨어는 매번 요청이 전달될 때가 아닌, 응용 프로그램이 구동되는 시점에 생성되기 때문에, 미들웨어 생성자에 의해서 사용되는 *범위(Scoped)* 수명 서비스는 각 요청 동안 주입된 다른 종속성 형식과 공유되지 않습니다. 미들웨어와 다른 형식 간에 *범위* 서비스를 공유해야 한다면, 해당 서비스를 `Invoke` 메서드의 시그니처에 추가하십시오. 다음 예제와 같이 `Invoke` 메서드는 종속성 주입으로 만들어진 추가적인 매개 변수를 전달받을 수 있습니다.

```c#
public class MyMiddleware
{
    private readonly RequestDelegate _next;

    public MyMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task Invoke(HttpContext httpContext, IMyScopedService svc)
    {
        svc.MyProperty = 1000;
        await _next(httpContext);
    }
}
```

## <a name="resources"></a>자료

* [본문의 예제 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/sample)
* [HTTP 모듈을 미들웨어로 마이그레이션하기](../migration/http-modules.md)
* [응용 프로그램 시작](startup.md)
* [요청 기능](request-features.md)
