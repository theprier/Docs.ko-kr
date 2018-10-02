---
title: ASP.NET Core에서 원본 간 요청 (CORS)를 사용 하도록 설정
author: rick-anderson
description: 에 대해 알아봅니다 어떻게 CORS 허용 하거나 거부 하는 ASP.NET Core 앱에서 크로스-원본 요청에 대 한 표준으로 합니다.
ms.author: riande
ms.custom: mvc
ms.date: 09/05/2018
uid: security/cors
ms.openlocfilehash: cfbf24edb1dae76f676d51738b0d57266688d53e
ms.sourcegitcommit: 317f9be24db600499e79d25872d743af74bd86c0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48045590"
---
# <a name="enable-cross-origin-requests-cors-in-aspnet-core"></a>ASP.NET Core에서 원본 간 요청 (CORS)를 사용 하도록 설정

작성자: [Mike Wasson](https://github.com/mikewasson), [Shayne Boyer](https://twitter.com/spboyer), 및 [Tom Dykstra](https://github.com/tdykstra)

브라우저 보안 요청을 웹 페이지를 제공 하는 다른 도메인에서 웹 페이지를 방지 합니다. 이 제한은 라고 합니다 *동일 원본 정책*합니다. 동일 원본 정책에서 다른 사이트의 중요 한 데이터를 읽을 악성 사이트를 방지 합니다. 경우에 따라 다음 다른 사이트 앱 크로스-원본 요청을 허용 하는 것이 좋습니다.

[교차 원본 자원 공유](https://www.w3.org/TR/cors/) (CORS, Cross Origin Resource Sharing)는 서버 측에서 동일 원본 정책을 완화할 수 있게 해주는 W3C 표준입니다. CORS를 사용하면 서버가 명시적으로 특정 교차 원본 요청만 허용하고, 다른 요청은 거부할 수 있습니다. 와 같은 CORS는 안전 하 고 이전 기술 보다 더 유연한 [JSONP](https://wikipedia.org/wiki/JSONP)합니다. 이 항목에서는 ASP.NET Core 앱에서 CORS를 사용 하도록 설정 하는 방법을 보여 줍니다.

## <a name="same-origin"></a>동일한 원본

동일한 구성표, 호스트 및 포트에 있는 경우 두 개의 Url가 동일한 원본 ([RFC 6454](https://tools.ietf.org/html/rfc6454)).

다음 두 URL은 동일한 원본입니다.

* `https://example.com/foo.html`
* `https://example.com/bar.html`

이러한 Url에 이전 두 Url 보다 다양 한 원본:

* `https://example.net` &ndash; 다른 도메인
* `https://www.example.com/foo.html` &ndash; 다른 하위 도메인
* `http://example.com/foo.html` &ndash; 다른 구성표
* `https://example.com:9000/foo.html` &ndash; 다른 포트

> [!NOTE]
> Internet Explorer는 원본을 비교할 때 포트를 고려하지 않습니다.

## <a name="register-cors-services"></a>CORS 서비스 등록

::: moniker range=">= aspnetcore-2.1"

참조를 [Microsoft.AspNetCore.App 메타 패키지](xref:fundamentals/metapackage-app) 에 대 한 패키지 참조를 추가 하거나 합니다 [Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/) 패키지 합니다.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

참조를 [Microsoft.AspNetCore.All 메타 패키지](xref:fundamentals/metapackage) 에 대 한 패키지 참조를 추가 하거나 합니다 [Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/) 패키지 합니다.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

패키지 참조를 추가 합니다 [Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/) 패키지 있습니다.

::: moniker-end

호출 <xref:Microsoft.Extensions.DependencyInjection.MvcCorsMvcCoreBuilderExtensions.AddCors*> 에서 `Startup.ConfigureServices` CORS services 앱의 서비스 컨테이너를 추가 하려면:

[!code-csharp[](cors/sample/CorsExample1/Startup.cs?name=snippet_addcors&highlight=3)]

## <a name="enable-cors"></a>CORS를 사용 하도록 설정

CORS 서비스를 등록 한 후에 ASP.NET Core 앱에서 CORS를 사용 하도록 설정 하려면 다음 방법 중 하나를 사용 합니다.

* [CORS 미들웨어](#enable-cors-with-cors-middleware) &ndash; 전역적으로 미들웨어를 통해 앱에 적용할 CORS 정책입니다.
* [MVC에서 CORS](#enable-cors-in-mvc) &ndash; 컨트롤러당 또는 작업당 적용할 CORS 정책입니다. CORS 미들웨어를 사용 하지 않습니다.

### <a name="enable-cors-with-cors-middleware"></a>CORS 미들웨어를 사용 하 여 CORS를 사용 하도록 설정

CORS 미들웨어는 앱에 크로스-원본 요청을 처리합니다. 요청 처리 파이프라인에 CORS 미들웨어를 사용 하려면 호출을 <xref:Microsoft.AspNetCore.Builder.CorsMiddlewareExtensions.UseCors*> 확장 메서드 `Startup.Configure`합니다.

CORS 미들웨어 앞에 야 정의 된 끝점이 모든 앱에서 크로스-원본 요청을 지원 하려면 (예를 들어 호출 하기 전에 `UseMvc` MVC/Razor 페이지 미들웨어에 대 한).

A *원본 간 정책은* 사용 하 여 CORS 미들웨어를 추가 하는 경우에 지정할 수 있습니다는 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder> 클래스입니다. CORS 정책을 정의 하는 방법은 두 가지가 있습니다.

* 호출 `UseCors` 람다를 사용 하 여:

  [!code-csharp[](cors/sample/CorsExample1/Startup.cs?highlight=11,12&range=22-38)]

  람다는 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder> 개체를 전달받습니다. [구성 옵션](#cors-policy-options)와 같은 `WithOrigins`,이 항목의 뒷부분에 설명 되어 있습니다. 앞의 예제는 정책에서 크로스-원본 요청 수 있습니다. `https://example.com` 및 다른 원본이 없습니다.

  후행 슬래시가 없는 URL을 지정 해야 합니다 (`/`). URL을 사용 하 여 종료 되 면 `/`, 비교 반환 `false` 헤더가 없으면 반환 됩니다.

  `CorsPolicyBuilder` fluent API에 있으므로 메서드 호출을 연결할 수 있습니다.

  [!code-csharp[](cors/sample/CorsExample3/Startup.cs?highlight=2-3&range=29-32)]

* 하나 이상의 명명 된 CORS 정책을 정의 하 고 런타임에 이름별으로 정책을 선택 합니다. 다음 예제에서는 라는 사용자 정의 CORS 정책을 *AllowSpecificOrigin*합니다. 정책을 선택 하려면 이름을 전달 `UseCors`:

  [!code-csharp[](cors/sample/CorsExample2/Startup.cs?name=snippet_begin&highlight=5-6,21)]

### <a name="enable-cors-in-mvc"></a>MVC에서 CORS를 사용 하도록 설정

또는 MVC를 사용 하 여 컨트롤러 또는 작업 별로 특정 CORS 정책을 적용할 수 있습니다. CORS를 사용 하도록 MVC를 사용 하는 경우 등록된 된 CORS 서비스 사용 됩니다. CORS 미들웨어를 사용 하지 않습니다.

### <a name="per-action"></a>액션 별

특정 작업에 대 한 CORS 정책을 지정 하려면 추가 합니다 [ &lbrack;EnableCors&rbrack; ](xref:Microsoft.AspNetCore.Cors.EnableCorsAttribute) 특성 작업을 합니다. 이때 정책 이름을 전달합니다.

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnAction&highlight=2)]

### <a name="per-controller"></a>컨트롤러 별

특정 컨트롤러에 대 한 CORS 정책을 지정 하려면 다음을 추가 합니다 [ &lbrack;EnableCors&rbrack; ](xref:Microsoft.AspNetCore.Cors.EnableCorsAttribute) 특성을 컨트롤러 클래스입니다. 이때 정책 이름을 전달합니다.

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnController&highlight=2)]

우선 순위에 따라 다음과 같습니다.

1. action
1. 컨트롤러

### <a name="disable-cors"></a>CORS 비활성시키기

컨트롤러 또는 작업에 대 한 CORS를 해제 하려면 사용 합니다 [ &lbrack;하도록 설정 하려면 DisableCors&rbrack; ](xref:Microsoft.AspNetCore.Cors.DisableCorsAttribute) 특성:

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=DisableOnAction&highlight=2)]

## <a name="cors-policy-options"></a>CORS 정책 옵션

이번 섹션에서는 CORS 정책에서 설정할 수 있는 다양한 옵션들을 살펴봅니다.

* [허용되는 원본 설정하기](#set-the-allowed-origins)
* [허용되는 HTTP 메서드 설정하기](#set-the-allowed-http-methods)
* [허용되는 요청 헤더 설정하기](#set-the-allowed-request-headers)
* [노출되는 응답 헤더 설정하기](#set-the-exposed-response-headers)
* [교차 원본 요청의 자격 증명](#credentials-in-cross-origin-requests)
* [예비 요청 만료 시간 설정하기](#set-the-preflight-expiration-time)

일부 옵션에 대 한 읽기 하면 도움이 될 합니다 [CORS 어떻게 작동](#how-cors-works) 먼저 섹션입니다.

### <a name="set-the-allowed-origins"></a>허용되는 원본 설정하기

하나 이상의 특정 원본에 허용 하려면 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithOrigins*>:

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=20-24&highlight=4)]

모든 원본을 허용할지, 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyOrigin*>:

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=28-32&highlight=4)]

모든 원본의 요청을 허용하기 전에 신중히 고민하시기 바랍니다. 즉 모든 원본에서 요청할 수 있도록 *웹 사이트* 앱에 크로스-원본 요청을 수행할 수 있습니다.

이 설정은 영향을 줍니다 [요청 및 액세스 제어-허용-원본 헤더 실행 전](#preflight-requests) (이 항목의 뒷부분에 설명).

### <a name="set-the-allowed-http-methods"></a>허용되는 HTTP 메서드 설정하기

모든 HTTP 메서드를 허용 하려면 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyMethod*>:

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=45-50&highlight=5)]

이 설정은 영향을 줍니다 [요청 및 액세스-컨트롤-허용-Methods 헤더 실행 전](#preflight-requests) (이 항목의 뒷부분에 설명).

### <a name="set-the-allowed-request-headers"></a>허용되는 요청 헤더 설정하기

특정 헤더를 CORS 요청을 보낼 수 있도록 호출 *요청 헤더를 작성*, 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithHeaders*> 허용 되는 헤더를 지정 합니다.

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=54-59&highlight=5)]

요청 헤더에 모든 author 수 있도록 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyHeader*>:

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=63-68&highlight=5)]

이 설정은 영향을 줍니다 [요청 및 액세스 제어-요청 헤더 헤더 실행 전](#preflight-requests) (이 항목의 뒷부분에 설명).

::: moniker range=">= aspnetcore-2.2"

지정 된 특정 헤더에 CORS 미들웨어 정책 일치가 `WithHeaders` 은 헤더 전송 하는 경우에 가능 `Access-Control-Request-Headers` 에 명시 된 헤더와 정확히 일치 `WithHeaders`합니다.

예를 들어 다음과 같이 구성 된 앱을 고려해 야 합니다.

```csharp
app.UseCors(policy => policy.WithHeaders(HeaderNames.CacheControl));
```

CORS 미들웨어 때문에 다음 요청 헤더를 사용 하 여 실행 전 요청을 거절 `Content-Language` ([HeaderNames.ContentLanguage](xref:Microsoft.Net.Http.Headers.HeaderNames.ContentLanguage))에 나열 되지 않은 `WithHeaders`:

```
Access-Control-Request-Headers: Cache-Control, Content-Language
```

앱 반환을 *200 확인* 응답 하지만 CORS 헤더를 다시 보내지 않습니다. 따라서 브라우저는 크로스-원본 요청을 시도 하지 않습니다.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

CORS 미들웨어의 네 가지 헤더를 항상 허용 된 `Access-Control-Request-Headers` CorsPolicy.Headers에 구성 된 값에 관계 없이 전송 됩니다. 이 헤더 목록에는 다음이 포함 됩니다.

* `Accept`
* `Accept-Language`
* `Content-Language`
* `Origin`

예를 들어 다음과 같이 구성 된 앱을 고려해 야 합니다.

```csharp
app.UseCors(policy => policy.WithHeaders(HeaderNames.CacheControl));
```

CORS 미들웨어가 성공적으로 응답 다음 요청 헤더를 사용 하 여 실행 전 요청에 있으므로 `Content-Language` 은 항상 허용 목록에 추가 합니다.

```
Access-Control-Request-Headers: Cache-Control, Content-Language
```

::: moniker-end

### <a name="set-the-exposed-response-headers"></a>노출되는 응답 헤더 설정하기

브라우저는 기본적으로 모든 앱에 대 한 응답 헤더를 노출 하지 합니다. 자세한 내용은 [W3C 크로스-원본 자원 공유 (용어): 간단한 응답 헤더](https://www.w3.org/TR/cors/#simple-response-header)합니다.

기본적으로 사용 가능한 응답 헤더들은 다음과 같습니다.

* `Cache-Control`
* `Content-Language`
* `Content-Type`
* `Expires`
* `Last-Modified`
* `Pragma`

이러한 헤더를 호출 하는 CORS 사양 *간단한 응답 헤더*합니다. 다른 헤더를 사용할 수 있도록 앱을 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithExposedHeaders*>:

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=72-77&highlight=5)]

### <a name="credentials-in-cross-origin-requests"></a>교차 원본 요청의 자격 증명

CORS 요청에서 자격 증명(Credentials)은 특별한 처리를 해야 합니다. 기본적으로 브라우저는 크로스-원본 요청을 사용 하 여 자격 증명을 보내지 않습니다. 자격 증명 쿠키 및 HTTP 인증 체계를 포함합니다. 크로스-원본 요청을 사용 하 여 자격 증명을 보내려면 클라이언트 설정 해야 합니다 `XMLHttpRequest.withCredentials` 에 `true`입니다.

사용 하 여 `XMLHttpRequest` 직접.

```javascript
var xhr = new XMLHttpRequest();
xhr.open('get', 'https://www.example.com/api/test');
xhr.withCredentials = true;
```

jQuery를 사용할 경우:

```jQuery
$.ajax({
  type: 'get',
  url: 'https://www.example.com/home',
  xhrFields: {
    withCredentials: true
}
```

또한 서버에서도 자격 증명을 허용해야만 합니다. 크로스-원본 자격 증명을 허용 하려면 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowCredentials*>:

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=81-86&highlight=5)]

HTTP 응답에 포함 됩니다는 `Access-Control-Allow-Credentials` 서버 크로스-원본 요청에 대 한 자격 증명을 허용 하는지 브라우저에 지시 하는 헤더입니다.

경우 브라우저는 자격 증명을 보내지만 응답 유효한 없는 `Access-Control-Allow-Credentials` 헤더, 브라우저 앱에 대 한 응답을 제공 하지 않습니다 및 크로스-원본 요청에 실패 합니다.

크로스-원본 자격 증명을 허용 하는 경우 주의 해야 합니다. 다른 도메인에서 웹 사이트는 사용자의 지식 없이 사용자를 대신 하 여 앱에는 로그인 한 사용자의 자격 증명을 보낼 수 있습니다.

CORS 사양도 해당 설정에 따라 원본이 `"*"` (모든 원본) 올바르지 않습니다 경우는 `Access-Control-Allow-Credentials` 헤더가 있습니다.

### <a name="preflight-requests"></a>실행 전 요청

브라우저는 일부 CORS 요청에 대 한 실제 요청 하기 전에 추가 요청을 보냅니다. 이 요청에서 호출 되는 *실행 전 요청*합니다. 다음 조건이 true 인 경우 브라우저가 실행 전 요청을 건너뛸 수 있습니다.:

* 요청 메서드가 GET, HEAD 또는 POST 됩니다.
* 앱 이외의 요청 헤더를 설정 하지 않는 `Accept`, `Accept-Language`를 `Content-Language`를 `Content-Type`, 또는 `Last-Event-ID`합니다.
* `Content-Type` 헤더 경우 설정에 다음 값 중 하나:
  * `application/x-www-form-urlencoded`
  * `multipart/form-data`
  * `text/plain`

호출 하 여 앱을 설정 하는 헤더에 적용 되는 클라이언트 요청에 대 한 요청 헤더에는 규칙 집합 `setRequestHeader` 에 `XMLHttpRequest` 개체입니다. 이러한 헤더를 호출 하는 CORS 사양 *요청 헤더를 작성*합니다. 헤더와 같은 브라우저 설정 수에 규칙 적용 되지 않습니다 `User-Agent`하십시오 `Host`, 또는 `Content-Length`합니다.

다음은 실행 전 요청의 예입니다.

```
OPTIONS https://myservice.azurewebsites.net/api/test HTTP/1.1
Accept: */*
Origin: https://myclient.azurewebsites.net
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: accept, x-my-custom-header
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
Content-Length: 0
```

HTTP OPTIONS 메서드를 사용 하는 사전 요청 합니다. 두 가지 특수 헤더를 포함합니다.

* `Access-Control-Request-Method`실제 요청에 사용 됩니다: HTTP 메서드.
* `Access-Control-Request-Headers`: 목록에 대 한 실제 요청에서 앱을 설정 하는 요청 헤더입니다. 여기와 같은 브라우저 설정 하는 헤더가 포함 되지 않습니다 앞에서 설명한 대로 `User-Agent`입니다.

CORS 실행 전 요청에 포함 될 수 있습니다는 `Access-Control-Request-Headers` 헤더로 실제 요청과 함께 전송 되는 헤더를 서버에 알립니다.

특정 헤더를 허용 하려면 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithHeaders*>:

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=54-59&highlight=5)]

요청 헤더에 모든 author 수 있도록 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyHeader*>:

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=63-68&highlight=5)]

브라우저 설정 하는 방법에 전적으로 일관 되지 `Access-Control-Request-Headers`합니다. 이외의 헤더 값으로 설정 하면 `"*"` (사용할지 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicy.AllowAnyHeader*>)를 하나 이상 포함 해야 `Accept`, `Content-Type`, 및 `Origin`, 지원 하려는 모든 사용자 지정 헤더 및.

다음은 실행 전 요청 (서버 요청을 허용 하는지 가정할 경우)에 대 한 예제 응답입니다.

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 0
Access-Control-Allow-Origin: https://myclient.azurewebsites.net
Access-Control-Allow-Headers: x-my-custom-header
Access-Control-Allow-Methods: PUT
Date: Wed, 20 May 2015 06:33:22 GMT
```

응답에 포함 되어는 `Access-Control-Allow-Methods` 허용 되는 메서드를 나열 하는 헤더 및 필요에 따라는 `Access-Control-Allow-Headers` 허용 되는 헤더를 나열 하는 헤더입니다. 실행 전 요청이 성공 하면 브라우저는 실제 요청을 보냅니다.

실행 전 요청이 거부 되 면 앱에서 반환 된 *200 확인* 응답 CORS 헤더를 다시 보내지 않습니다. 하지만 합니다. 따라서 브라우저는 크로스-원본 요청을 시도 하지 않습니다.

### <a name="set-the-preflight-expiration-time"></a>예비 요청 만료 시간 설정하기

`Access-Control-Max-Age` 헤더 실행 전 요청에 응답을 캐시할 수 기간을 지정 합니다. 이 헤더를 설정 하려면 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.SetPreflightMaxAge*>:

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=90-95&highlight=5)]

## <a name="how-cors-works"></a>CORS의 동작 방식

이번 섹션에서는 CORS 요청 시 HTTP 메시지 수준에서 발생하는 일들을 살펴봅니다. CORS 정책을 올바르게 구성 하 고 예기치 않은 동작이 발생 하는 경우 디버깅할 수 있도록 CORS의 작동 방식을 이해 하는 것이 반드시 합니다.

CORS 명세에서는 교차 원본 요청을 활성화시키기 위한 용도로 몇 가지 새로운 HTTP 헤더들이 도입되었습니다. 브라우저에서 CORS를 지 원하는 경우 이러한 머리글 크로스-원본 요청을 자동으로 설정 합니다. CORS를 사용 하도록 사용자 지정 JavaScript 코드 필요는 없습니다.

다음은 원본 간 요청의 예입니다. `Origin` 헤더는 요청 하는 사이트의 도메인을 제공 합니다.

```
GET https://myservice.azurewebsites.net/api/test HTTP/1.1
Referer: https://myclient.azurewebsites.net/
Accept: */*
Accept-Language: en-US
Origin: https://myclient.azurewebsites.net
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
```

서버 요청을 허용 하는 경우에 설정의 `Access-Control-Allow-Origin` 헤더를 응답 합니다. 이 헤더의 값이 일치 하거나 합니다 `Origin` 요청의 헤더 또는 와일드 카드 값 `"*"`, 모든 원본을 허용 되는 의미:

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Type: text/plain; charset=utf-8
Access-Control-Allow-Origin: https://myclient.azurewebsites.net
Date: Wed, 20 May 2015 06:27:30 GMT
Content-Length: 12

Test message
```

응답에 포함 되지 않은 경우는 `Access-Control-Allow-Origin` 헤더를 크로스-원본 요청에 실패 합니다. 특히 브라우저 요청을 허용 하지 않습니다. 서버 성공적인 응답을 반환 하는 경우에 브라우저 되어도 응답이 클라이언트 앱에 사용할 수 있습니다.

## <a name="additional-resources"></a>추가 자료

* [크로스-원본 자원 공유 (CORS)](https://developer.mozilla.org/docs/Web/HTTP/CORS)
