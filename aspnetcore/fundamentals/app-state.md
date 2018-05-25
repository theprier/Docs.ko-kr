---
title: ASP.NET Core에서 세션 및 응용 프로그램 상태
author: rick-anderson
description: 요청 간에 응용 프로그램 및 사용자(세션) 상태를 유지하는 접근 방법입니다.
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 11/27/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/app-state
ms.openlocfilehash: 887aefdeaa45957f7b95bfe8df342eb34d267e3a
ms.sourcegitcommit: 3a893ae05f010656d99d6ddf55e82f1b5b6933bc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/18/2018
---
# <a name="session-and-application-state-in-aspnet-core"></a>ASP.NET Core에서 세션 및 응용 프로그램 상태

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [Steve Smith](https://ardalis.com/) 및 [Diana LaRose](https://github.com/DianaLaRose)

HTTP는 상태 비저장 프로토콜입니다. 웹 서버는 독립적인 요청으로 각 HTTP 요청을 처리하고 이전 요청에서 사용자 값을 유지하지 않습니다. 이 문서에서는 요청 간에 응용 프로그램 및 세션 상태를 유지하기 위한 다양한 방법을 설명합니다.

## <a name="session-state"></a>세션 상태

세션 상태는 사용자가 웹 앱을 탐색하는 동안 사용자의 데이터를 저장하기 위해서 사용할 수 있는 ASP.NET Core의 기능입니다. 서버에서 사전 또는 해시 테이블로 구성하여 세션 상태는 브라우저에서 요청 간 데이터를 유지합니다. 세션 데이터는 캐시에 의해 지원됩니다.

ASP.NET Core는 클라이언트에 각 요청과 함께 서버에 전송된 세션 ID를 포함하는 쿠키를 제공하여 세션 상태를 유지합니다. 서버는 세션 ID를 사용하여 세션 데이터를 가져옵니다. 세션 쿠키는 브라우저와 관련되기 때문에 브라우저에서 세션을 공유할 수 없습니다. 세션 쿠키는 브라우저 세션이 끝나면 삭제됩니다. 쿠키가 만료된 세션에 대해 수신되면 동일한 세션 쿠키를 사용하는 새 세션이 생성됩니다.

서버는 마지막 요청 이후 제한된 시간에 대한 세션을 유지합니다. 세션 제한 시간을 설정하거나 20분의 기본값을 사용합니다. 세션 상태는 특정 세션에 고유한 사용자 데이터를 저장하는 데 이상적이지만 영구적으로 유지될 필요가 없습니다. 데이터는 `Session.Clear`를 호출하거나 세션이 데이터 저장소에서 만료될 때 백업 저장소에서 삭제됩니다. 서버는 브라우저가 닫히는 경우 또는 세션 쿠키가 삭제되는 경우를 알지 못합니다.

> [!WARNING]
> 세션에 중요한 데이터를 저장하지 마십시오. 클라이언트는 브라우저를 닫거나 세션 쿠키를 삭제하지 못할 수 있습니다(일부 브라우저는 창에서 세션 쿠키를 활성 상태로 유지). 또한 세션은 단일 사용자로 제한될 수 없습니다. 다음 사용자는 동일한 세션으로 계속할 수 있습니다.

메모리 내 세션 공급자는 로컬 서버에 세션 데이터를 저장합니다. 서버 팜에서 웹앱을 실행하려는 경우 특정 서버에 각 세션을 연결하도록 고정 세션을 사용해야 합니다. Windows Azure 웹 사이트 플랫폼은 고정 세션을 기본값으로 설정합니다(응용 프로그램 요청 라우팅 또는 ARR). 그러나 고정 세션은 확장성에 영향을 주고 웹앱 업데이트를 복잡하게 만들 수 있습니다. 더 나은 옵션은 고정 세션이 필요하지 않은 Redis 또는 SQL Server 분산 캐시를 사용하는 것입니다. 자세한 내용은 [분산 캐시 사용](xref:performance/caching/distributed)을 참조하세요. 서비스 공급자 설정에 대한 자세한 내용은 이 문서의 뒷부분에 나오는 [세션 구성](#configuring-session)을 참조하세요.

## <a name="tempdata"></a>TempData

ASP.NET Core MVC는 [컨트롤러](/dotnet/api/microsoft.aspnetcore.mvc.controller?view=aspnetcore-2.0)에서 [TempData](/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) 속성을 노출합니다. 이 속성은 판독될 때까지 데이터를 저장합니다. `Keep` 및 `Peek` 메서드를 사용하여 삭제 없이 데이터를 검사할 수 있습니다. `TempData`는 두 개 이상의 요청에 대한 데이터가 필요할 경우 리디렉션에 특히 유용합니다. `TempData`는 TempData 공급자에 의해 구현됩니다(예: 쿠키 또는 세션 상태 사용).

### <a name="tempdata-providers"></a>TempData 공급자

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

ASP.NET Core 2.0 이상에서 쿠키 기반 TempData 공급자는 TempData를 쿠키에 저장하는 데 기본적으로 사용됩니다.

쿠키 데이터는 [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector)를 사용하여 암호화되고, [Base64UrlTextEncoder](/dotnet/api/microsoft.aspnetcore.webutilities.base64urltextencoder)로 인코딩된 후 청크 분할됩니다. 쿠키가 청크 분할되므로 ASP.NET Core 1.x에서 확인한 단일 쿠키 크기 제한은 적용되지 않습니다. 암호화된 데이터를 압축하는 것은 [범죄](https://wikipedia.org/wiki/CRIME_(security_exploit)) 및 [위반](https://wikipedia.org/wiki/BREACH_(security_exploit)) 공격과 같은 보안 문제를 일으킬 수 있으므로 쿠키 데이터는 압축되지 않습니다. 쿠키 기반 TempData 공급자에 대한 자세한 내용은 [CookieTempDataProvider](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.ViewFeatures/ViewFeatures/CookieTempDataProvider.cs)를 참조하세요.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

ASP.NET Core 1.0 및 1.1에서는 세션 상태 TempData 공급자가 기본값입니다.

---

### <a name="choosing-a-tempdata-provider"></a>TempData 공급자 선택

TempData 공급자를 선택하는 데는 다음과 같은 몇 가지 고려 사항이 수반됩니다.

1. 응용 프로그램이 이미 다른 용도에 세션 상태를 사용합니까? 그런 경우 세션 상태 TempData 공급자 사용에는 응용 프로그램에 대한 추가 비용이 없습니다(데이터 크기 외에).
2. 응용 프로그램은 상대적으로 적은 양의 데이터에 TempData만 제한적으로 사용합니까(최대 500바이트)? 그런 경우 쿠키 TempData 공급자는 TempData를 전달하는 각 요청에 적은 비용을 추가합니다. 그렇지 않은 경우 세션 상태 TempData 공급자는 TempData가 사용될 때까지 각 요청에서 많은 양의 데이터를 왕복 작업하지 않도록 하는 데 도움이 될 수 있습니다.
3. 응용 프로그램은 웹 팜(다중 서버)에서 실행됩니까? 그런 경우 쿠키 TempData 공급자를 사용하는 데 필요한 추가 구성이 없습니다.

> [!NOTE]
> 대부분의 웹 클라이언트(예: 웹 브라우저)는 각 쿠키의 최대 크기, 쿠키의 총 수 또는 둘 다에 제한을 적용합니다. 따라서 쿠키 TempData 공급자를 사용하는 경우 앱이 이러한 제한을 초과하지 않는지 확인합니다. 암호화의 오버헤드 및 청크를 확인하여 데이터의 전체 크기를 고려합니다.

### <a name="configure-the-tempdata-provider"></a>TempData 공급자 구성

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

쿠키 기반 TempData 공급자는 기본적으로 활성화됩니다. 다음 `Startup` 클래스 코드는 세션 기반 TempData 공급자를 구성합니다.

[!code-csharp[](app-state/sample/src/WebAppSessionDotNetCore2.0App/StartupTempDataSession.cs?name=snippet_TempDataSession&highlight=4,6,11)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

다음 `Startup` 클래스 코드는 세션 기반 TempData 공급자를 구성합니다.

[!code-csharp[](app-state/sample/src/WebAppSession/StartupTempDataSession.cs?name=snippet_TempDataSession&highlight=4,9)]

---

순서 지정은 미들웨어 구성 요소에 중요합니다. 위의 예에서 `UseMvcWithDefaultRoute` 후에 `UseSession`이 호출되는 경우 형식 `InvalidOperationException`의 예외가 발생합니다. 자세한 내용은 [미들웨어 순서 지정](xref:fundamentals/middleware/index#ordering)을 참조하세요.

> [!IMPORTANT]
> .NET Framework를 대상으로 하고 세션 기반 공급자를 사용하는 경우 [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session) NuGet 패키지를 프로젝트에 추가합니다.

## <a name="query-strings"></a>쿼리 문자열

새 요청의 쿼리 문자열에 추가하여 한 요청에서 다른 요청으로 제한된 양의 데이터를 전달할 수 있습니다. 이는 이메일 또는 소셜 네트워크를 통해 공유되도록 포함된 상태가 있는 링크를 허용하는 영구적인 방식으로 상태를 캡처하는 데 유용합니다. 그러나 이러한 이유로 중요한 데이터에 쿼리 문자열을 절대 사용하면 안 됩니다. 쉽게 공유되는 것 뿐만 아니라 쿼리 문자열에 데이터를 포함하면 사용자가 인증되는 동안 악성 사이트를 방문하도록 유도할 수 있는 [CSRF(교차 사이트 요청 위조)](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) 공격에 대한 기회를 만들 수 있습니다. 공격자는 앱에서 사용자 데이터를 도용하거나 사용자를 대신하여 악의적인 작업을 수행할 수 있습니다. 유지된 모든 응용 프로그램 또는 세션 상태를 CSRF 공격으로부터 보호해야 합니다. CSRF 공격에 대한 자세한 내용은 [교차 사이트 요청 위조(XSRF/CSRF) 공격 방지](xref:security/anti-request-forgery)를 참조하세요.

## <a name="post-data-and-hidden-fields"></a>데이터 게시 및 숨겨진 필드

데이터는 숨겨진 양식 필드에 저장되고 다음 요청에서 다시 게시될 수 있습니다. 이는 다중 페이지 폼에서 일반적입니다. 그러나 클라이언트는 잠재적으로 데이터를 변조할 수 있으므로 서버는 항상 유효성을 다시 검사해야 합니다.

## <a name="cookies"></a>쿠키

쿠키는 웹 응용 프로그램에서 사용자 관련 데이터를 저장하는 방법을 제공합니다. 쿠키는 모든 요청과 함께 전송되므로 해당 크기는 최소로 유지되어야 합니다. 이상적으로 식별자만 서버에 저장된 실제 데이터와 함께 쿠키에 저장되어야 합니다. 대부분의 브라우저는 4096바이트로 쿠키를 제한합니다. 또한 제한된 개수의 쿠키를 각 도메인에 대해 사용할 수 있습니다.

쿠키는 변조될 수 있기 때문에 서버에서 유효성을 검사해야 합니다. 클라이언트에서 쿠키의 지속성은 사용자 작업 및 만료에 종속되지만 일반적으로 클라이언트에서 데이터 지속성의 가장 영구적인 형식입니다.

쿠키는 종종 개인 설정에 사용됩니다. 여기서 콘텐츠는 알려진 사용자에 대해 사용자 지정됩니다. 사용자만 식별되고 대부분의 경우에서 인증되지 않기 때문에 사용자 이름, 계정 이름 또는 고유한 사용자 ID(예: GUID)를 쿠키에 저장하여 쿠키를 일반적으로 보호할 수 있습니다. 그런 다음, 쿠키를 사용하여 사이트의 사용자 개인 설정 인프라에 액세스할 수 있습니다.

## <a name="httpcontextitems"></a>HttpContext.Items

`Items` 컬렉션은 하나의 특정 요청을 처리하는 동안에만 필요한 데이터를 저장하기 위한 좋은 위치입니다. 컬렉션의 콘텐츠는 각 요청 후 삭제됩니다. `Items` 컬렉션은 요청 중에 다른 시점에서 작동하고 매개 변수를 전달할 직접 방법이 없는 경우에 통신하는 구성 요소 또는 미들웨어에 대한 방법으로 가장 잘 사용됩니다. 자세한 내용은 이 아티클의 뒷부분에 나오는 [HttpContext.Items 작업](#working-with-httpcontextitems)을 참조하세요.

## <a name="cache"></a>캐시

캐싱은 데이터 저장 및 검색하는 효율적인 방법입니다. 시간 및 기타 고려 사항에 따라 캐시된 항목의 수명을 제어할 수 있습니다. [캐시하는 방법](../performance/caching/index.md)에 대해 자세히 알아봅니다.

## <a name="working-with-session-state"></a>세션 상태 사용

### <a name="configuring-session"></a>세션 구성

`Microsoft.AspNetCore.Session` 패키지는 세션 상태를 관리하기 위한 미들웨어를 제공합니다. 세션 미들웨어를 활성화하려면 `Startup`은 다음을 포함해야 합니다.

- [IDistributedCache](/dotnet/api/microsoft.extensions.caching.distributed.idistributedcache) 메모리 캐시 중 하나 `IDistributedCache` 구현은 세션에 대한 백업 저장소로 사용됩니다.
- NuGet 패키지 "Microsoft.AspNetCore.Session"이 필요한 [AddSession](/dotnet/api/microsoft.extensions.dependencyinjection.sessionservicecollectionextensions#Microsoft_Extensions_DependencyInjection_SessionServiceCollectionExtensions_AddSession_Microsoft_Extensions_DependencyInjection_IServiceCollection_) 호출
- [UseSession](/dotnet/api/microsoft.aspnetcore.builder.sessionmiddlewareextensions#methods_) 호출

다음 코드에서는 메모리 내 세션 공급자를 설정하는 방법을 보여 줍니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](app-state/sample/src/WebAppSessionDotNetCore2.0App/Startup.cs?highlight=11-19,24)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[!code-csharp[](app-state/sample/src/WebAppSession/Startup.cs?highlight=11-19,24)]

---

설치되고 구성되면 `HttpContext`에서 세션을 참조할 수 있습니다.

`UseSession`이 호출되기 전에 `Session`에 액세스하려는 경우 예외 `InvalidOperationException: Session has not been configured for this application or request`가 throw됩니다.

`Response` 스트림에 이미 작성을 시작한 후 새 `Session`을 만들려는 경우(즉, 세션 쿠키가 만들어지지 않음) 예외 `InvalidOperationException: The session cannot be established after the response has started`가 throw됩니다. 웹 서버 로그에서 예외를 확인할 수 있습니다. 브라우저에 표시되지 않습니다.

### <a name="loading-session-asynchronously"></a>세션을 비동기적으로 로드

ASP.NET Core에서 기본 세션 공급자는 [ISession.LoadAsync](/dotnet/api/microsoft.aspnetcore.http.isession#Microsoft_AspNetCore_Http_ISession_LoadAsync) 메서드가 `TryGetValue`, `Set` 또는 `Remove` 메서드 전에 명시적으로 호출된 경우에만 기본 [IDistributedCache](/dotnet/api/microsoft.extensions.caching.distributed.idistributedcache) 저장소에서 비동기적으로 세션 레코드를 로드합니다. `LoadAsync`가 먼저 호출되지 않은 경우 기본 세션 레코드가 동기적으로 로드되며 이는 크기를 조정하는 앱의 기능에 잠재적으로 영향을 줄 수 있습니다.

이 패턴을 응용 프로그램에 적용하려면 `LoadAsync` 메서드가 `TryGetValue`, `Set` 또는 `Remove` 이전에 호출되지 않은 경우 예외를 throw하는 버전으로 [DistributedSessionStore](/dotnet/api/microsoft.aspnetcore.session.distributedsessionstore) 및 [DistributedSession](/dotnet/api/microsoft.aspnetcore.session.distributedsession) 구현을 래핑합니다. 서비스 컨테이너에 래핑된 버전을 등록합니다.

### <a name="implementation-details"></a>구현 세부 정보

세션은 쿠키를 사용하여 단일 브라우저에서 요청을 추적하고 식별합니다. 기본적으로 이 쿠키는 ".AspNet.Session"이라고 하며 "/"의 경로를 사용합니다. 쿠키 기본값은 도메인을 지정하지 않으므로 페이지에서 클라이언트 쪽 스크립트에 사용할 수 없습니다(`CookieHttpOnly`는 `true`를 기본값으로 설정하므로).

세션 기본값을 재정의하려면 `SessionOptions`를 사용합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](app-state/sample/src/WebAppSessionDotNetCore2.0App/StartupCopy.cs?name=snippet1&highlight=8-12)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[!code-csharp[](app-state/sample/src/WebAppSession/StartupCopy.cs?name=snippet1&highlight=8-12)]

---

서버는 `IdleTimeout` 속성을 사용하여 해당 콘텐츠가 중단되기 전에 유휴 상태일 수 있는 세션의 기간을 결정합니다. 이 속성은 쿠키 만료와 무관합니다. 세션 미들웨어(읽거나 쓰는)를 통해 전달되는 각 요청은 시간 제한을 다시 설정합니다.

`Session`은 *잠기지 않으므로* 두 요청이 모두 세션의 콘텐츠를 수정하려고 하는 경우 마지막 요청이 첫 번째 요청을 재정의합니다. `Session`은 *일관된 세션*으로 구현됩니다. 즉, 모든 콘텐츠는 함께 저장됩니다. 세션의 다른 부분(다른 키)을 수정하는 두 요청은 여전히 서로 영향을 줄 수 있습니다.

### <a name="set-and-get-session-values"></a>세션 값 설정 및 가져오기

`Context.Session`을 사용하여 Razor 페이지 또는 보기에서 세션에 액세스합니다.

[!code-cshtml[](app-state/sample/src/WebAppSessionDotNetCore2.0App/Views/Home/About.cshtml)]

`HttpContext.Session`을 사용하여 `PageModel` 클래스 또는 컨트롤러에서 세션에 액세스합니다. 이 속성은 [ISession](/dotnet/api/microsoft.aspnetcore.http.isession) 구현입니다.

다음 예제에서는 int 및 문자열 설정 및 가져오기를 보여 줍니다.

[!code-csharp[](app-state/sample/src/WebAppSession/Controllers/HomeController.cs?range=8-27,49)]

다음 확장 메서드를 추가하는 경우 세션에 직렬화 가능 개체를 설정하고 가져올 수 있습니다.

[!code-csharp[](app-state/sample/src/WebAppSession/Extensions/SessionExtensions.cs)]

다음 샘플에서는 직렬화 가능 개체를 설정하고 가져오는 방법을 보여 줍니다.

[!code-csharp[](app-state/sample/src/WebAppSession/Controllers/HomeController.cs?name=snippet2)]

## <a name="working-with-httpcontextitems"></a>HttpContext.Items 작업

`HttpContext` 추상화는 `Items`라는 형식 `IDictionary<object, object>`의 사전 컬렉션에 대한 지원을 제공합니다. 이 컬렉션은 *HttpRequest*의 시작부터 사용할 수 있으며 각 요청의 끝에서 삭제됩니다. 키가 지정된 항목에 값을 지정하거나 특정 키에 대한 값을 요청하여 액세스할 수 있습니다.

다음 샘플에서 [미들웨어](xref:fundamentals/middleware/index)는 `Items` 컬렉션에 `isVerified`를 추가합니다.

```csharp
app.Use(async (context, next) =>
{
    // perform some verification
    context.Items["isVerified"] = true;
    await next.Invoke();
});
```

파이프라인의 뒷부분에서 다른 미들웨어는 액세스할 수 있습니다.

```csharp
app.Run(async (context) =>
{
    await context.Response.WriteAsync("Verified request? " +
        context.Items["isVerified"]);
});
```

단일 앱에서만 사용되는 미들웨어의 경우 `string` 키가 허용됩니다. 그러나 응용 프로그램 간에 공유되는 미들웨어는 키가 충돌될 가능성을 방지하기 위해 고유한 개체 키를 사용해야 합니다. 여러 응용 프로그램에서 사용해야 하는 미들웨어를 개발하는 경우 아래와 같이 미들웨어 클래스에서 정의된 고유한 개체 키를 사용합니다.

```csharp
public class SampleMiddleware
{
    public static readonly object SampleKey = new Object();

    public async Task Invoke(HttpContext httpContext)
    {
        httpContext.Items[SampleKey] = "some value";
        // additional code omitted
    }
}
```

다른 코드는 미들웨어 클래스에 의해 노출된 키를 사용하여 `HttpContext.Items`에 저장된 값에 액세스할 수 있습니다.

```csharp
public class HomeController : Controller
{
    public IActionResult Index()
    {
        string value = HttpContext.Items[SampleMiddleware.SampleKey];
    }
}
```

이 방법은 또한 코드의 여러 위치에서 "매직 문자열"의 반복을 제거하는 이점이 있습니다.

## <a name="application-state-data"></a>응용 프로그램 상태 데이터

[종속성 주입](xref:fundamentals/dependency-injection)을 사용하여 모든 사용자에게 데이터를 사용할 수 있도록 합니다.

1. 데이터를 포함하는 서비스를 정의합니다(예: `MyAppData`라는 클래스).

    ```csharp
    public class MyAppData
    {
        // Declare properties/methods/etc.
    } 
    ```

2. `ConfigureServices`에 서비스 클래스를 추가합니다(예: `services.AddSingleton<MyAppData>();`).

3. 각 컨트롤러에서 데이터 서비스 클래스를 사용합니다.

    ```csharp
    public class MyController : Controller
    {
        public MyController(MyAppData myService)
        {
            // Do something with the service (read some data from it, 
            // store it in a private field/property, etc.)
        }
    } 
    ```

## <a name="common-errors-when-working-with-session"></a>세션을 작업할 때 일반적인 오류

* "'Microsoft.AspNetCore.Session.DistributedSessionStore'를 활성화하려고 시도하는 동안 'Microsoft.Extensions.Caching.Distributed.IDistributedCache' 형식에 대한 서비스를 확인할 수 없습니다."

  이는 일반적으로는 하나 이상의 `IDistributedCache` 구현을 구성하는 데 실패하여 발생됩니다. 자세한 내용은 [분산 캐시 사용](xref:performance/caching/distributed) 및 [메모리 내 캐싱](xref:performance/caching/memory)을 참조하세요.

* 세션 미들웨어가 세션 유지에 실패하는 이벤트에서(예: 데이터베이스를 사용할 수 없는 경우) 예외를 기록하고 숨깁니다. 그런 다음, 요청은 정상적으로 계속합니다. 이로 인해 매우 예기치 않은 동작이 발생합니다.

일반적인 예:

일부 사용자는 세션에 장바구니를 저장합니다. 사용자는 항목을 추가하지만 커밋이 실패합니다. 앱은 실패에 대해 알지 못하므로 true가 아닌 "항목이 추가되었습니다." 메시지를 보고합니다.

이러한 오류를 확인하는 권장 방법은 세션에 작성을 완료하면 앱 코드에서 `await feature.Session.CommitAsync();`를 호출하는 것입니다. 그런 다음, 오류에 대해 원하는 작업을 수행할 수 있습니다. `LoadAsync`를 호출할 때 동일한 방식으로 작동합니다.

### <a name="additional-resources"></a>추가 자료

* [ASP.NET Core 1.x: 이 문서에 사용되는 코드 샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/app-state/sample/src/WebAppSession)
* [ASP.NET Core 2.x: 이 문서에 사용되는 코드 샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/app-state/sample/src/WebAppSessionDotNetCore2.0App)
