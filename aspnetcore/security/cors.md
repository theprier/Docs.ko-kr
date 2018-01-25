---
title: "교차 원본 요청(CORS) 활성화시키기"
author: rick-anderson
description: "본문에서는 ASP.NET Core 응용 프로그램에서 교차-원본 요청을 허용하거나 거부하는 표준 CORS를 소개합니다."
ms.author: riande
manager: wpickett
ms.date: 05/17/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/cors
ms.openlocfilehash: e6b49b9dde94cc7d035ea91b992a13df8cb8caf2
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="enabling-cross-origin-requests-cors"></a>교차 원본 요청(CORS) 활성화시키기

작성자: [Mike Wasson](https://github.com/mikewasson), [Shayne Boyer](https://twitter.com/spboyer), 및 [Tom Dykstra](https://github.com/tdykstra)

브라우저의 보안 기능은 웹 페이지에서 다른 도메인으로 AJAX 요청을 전송하는 것을 막습니다. 이 제약 사항을 *동일 원본 정책(Same-Origin Policy)*이라고 부르며, 악의적인 사이트가 다른 사이트의 민감한 데이터를 무차별적으로 읽는 것을 방지합니다. 그러나 경우에 따라서는 다른 사이트가 여러분의 Web API에 교차 원본 요청(Cross-Origin Requests)을 전송하는 것을 허용해야 할 수도 있습니다.

[교차 원본 자원 공유](http://www.w3.org/TR/cors/)(CORS, Cross Origin Resource Sharing)는 서버 측에서 동일 원본 정책을 완화할 수 있게 해주는 W3C 표준입니다. CORS를 사용하면 서버가 명시적으로 특정 교차 원본 요청만 허용하고, 다른 요청은 거부할 수 있습니다. CORS는 [JSONP](https://wikipedia.org/wiki/JSONP) 같은 기존의 다른 기술보다 안전하고 유연합니다. 본문에서는 ASP.NET Core 응용 프로그램에서 CORS를 활성화시키는 방법을 알아봅니다.

## <a name="what-is-same-origin"></a>"동일 원본"이란?

두 URL의 스키마, 호스트 및 포트가 모두 동일한 경우, 두 URL의 원본이 동일하다고 말합니다. ([RFC 6454](http://tools.ietf.org/html/rfc6454))

다음 두 URL은 동일한 원본입니다.

* `http://example.com/foo.html`

* `http://example.com/bar.html`

반면, 다음 URL들은 위의 두 URL과는 다른 원본입니다.

* `http://example.net`-도메인이 다릅니다.

* `http://www.example.com/foo.html`-하위 도메인이 다릅니다.

* `https://example.com/foo.html`-스키마가 다릅니다.

* `http://example.com:9000/foo.html`-포트가 다릅니다.

> [!NOTE]
> Internet Explorer는 원본을 비교할 때 포트를 고려하지 않습니다.

## <a name="setting-up-cors"></a>CORS 설정하기

ASP.NET Core 응용 프로그램에 CORS를 설정하려면 프로젝트에 `Microsoft.AspNetCore.Cors` 패키지를 설치합니다.

그리고 Startup.cs에 CORS 서비스를 추가합니다.

[!code-csharp[Main](cors/sample/CorsExample1/Startup.cs?name=snippet_addcors)]

## <a name="enabling-cors-with-middleware"></a>미들웨어를 이용해서 CORS 활성화시키기

전체 응용 프로그램에서 CORS를 활성화시키려면 `UseCors` 확장 메서드를 이용해서 요청 파이프라인에 CORS 미들웨어를 추가합니다. 참고로 교차 원본 요청을 지원하고자 하는 응용 프로그램 내의 모든 정의된 끝점보다 `UseMvc`를 호출하기 전에 CORS 미들웨어를 먼저 파이프라인에 추가해야 합니다.

CORS 미들웨어를 추가할 때, `CorsPolicyBuilder` 클래스를 이용해서 원본 간 정책을 지정할 수 있습니다. 구체적인 방법은 두 가지입니다. 먼저, 첫 번째 방법은 람다를 전달해서 `UseCors`를 호출하는 것입니다.

[!code-csharp[Main](cors/sample/CorsExample1/Startup.cs?highlight=11,12&range=22-38)]

**참고:** 반드시 후행 슬래시(`/`)가 없는 URL을 지정해야 합니다. 만약 URL이 `/`로 끝나면, 비교 결과가 `false`를 반환하여 아무런 헤더도 반환되지 않습니다.

람다는 `CorsPolicyBuilder` 개체를 전달받습니다. [구성 옵션](#cors-policy-options)의 목록은 잠시 후 다시 살펴봅니다. 이 예제 코드의 정책은 `http://example.com`에서 전달된 교차 원본 요청은 허용하지만, 다른 원본의 요청은 허용하지 않습니다.

CorsPolicyBuilder는 Fluent API를 지원하므로 다음과 같이 메서드 호출을 연결할 수 있습니다.

[!code-csharp[Main](../security/cors/sample/CorsExample3/Startup.cs?highlight=3&range=29-32)]

두 번째 방법은 미리 한 가지 이상의 명명된 CORS 정책을 정의한 다음, 런타임 시에 이름을 지정해서 정책을 선택하는 것입니다.

[!code-csharp[Main](cors/sample/CorsExample2/Startup.cs?name=snippet_begin)]

이 예제는 "AllowSpecificOrigin"이라는 CORS 정책을 추가합니다. 그리고 `UseCors` 메서드에 이름을 전달해서 정책을 선택합니다.

## <a name="enabling-cors-in-mvc"></a>MVC에서 CORS 활성화시키기

MVC를 이용해서 액션별, 컨트롤러별 또는 모든 컨트롤러에 대해 전역으로 특정 CORS를 적용할 수도 있습니다. MVC를 이용해서 CORS를 활성화시키는 경우에도 동일한 CORS 서비스가 사용되지만, 이 경우 CORS 미들웨어는 사용되지 않습니다.

### <a name="per-action"></a>액션 별

특정 액션에 CORS 정책을 지정하려면 해당 액션에 `[EnableCors]` 특성을 추가합니다. 이때 정책 이름을 전달합니다.

[!code-csharp[Main](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnAction)]

### <a name="per-controller"></a>컨트롤러 별

특정 컨트롤러에 CORS 정책을 지정하려면 해당 컨트롤러에 `[EnableCors]` 특성을 추가합니다. 이때 정책 이름을 전달합니다.

[!code-csharp[Main](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnController)]

### <a name="globally"></a>전역으로

모든 컨트롤러에서 전역으로 CORS를 활성화시키려면, 전역 필터 컬렉션에 `CorsAuthorizationFilterFactory` 필터를 추가합니다.

[!code-csharp[Main](cors/sample/CorsMVC/Startup2.cs?name=snippet_configureservices)]

특성의 우선 순위는 액션, 컨트롤러, 전역 순입니다. 다시 말해서, 액션 수준 정책은 컨트롤러 수준 정책보다 우선하며, 컨트롤러 수준 정책은 전역 정책보다 우선합니다.

### <a name="disable-cors"></a>CORS 비활성시키기

컨트롤러나 액션의 CORS를 비활성화시키려면, `[DisableCors]` 특성을 적용합니다.

[!code-csharp[Main](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=DisableOnAction)]

## <a name="cors-policy-options"></a>CORS 정책 옵션

이번 섹션에서는 CORS 정책에서 설정할 수 있는 다양한 옵션들을 살펴봅니다.

* [허용되는 원본 설정하기](#set-the-allowed-origins)

* [허용되는 HTTP 메서드 설정하기](#set-the-allowed-http-methods)

* [허용되는 요청 헤더 설정하기](#set-the-allowed-request-headers)

* [노출되는 응답 헤더 설정하기](#set-the-exposed-response-headers)

* [교차 원본 요청의 자격 증명](#credentials-in-cross-origin-requests)

* [예비 요청 (Preflight Requests) 만료 시간 설정하기](#set-the-preflight-expiration-time)

일부 옵션의 경우, [CORS의 동작 방식](#how-cors-works) 섹션을 먼저 읽어보는 것이 이해에 도움이 됩니다.

### <a name="set-the-allowed-origins"></a>허용되는 원본 설정하기

하나 이상의 특정 원본을 허용하려면 다음과 같이 구성합니다.

[!code-csharp[Main](cors/sample/CorsExample4/Startup.cs?range=19-23)]

모든 원본을 허용하려면 다음과 같이 구성합니다:

[!code-csharp[Main](cors/sample/CorsExample4/Startup.cs??range=27-31)]

모든 원본의 요청을 허용하기 전에 신중히 고민하시기 바랍니다. 이는 문자 그대로 모든 웹 사이트에서 응용 프로그램에 AJAX 호출을 전송할 수 있음을 뜻합니다.

### <a name="set-the-allowed-http-methods"></a>허용되는 HTTP 메서드 설정하기

모든 HTTP 메서드를 허용하려면 다음과 같이 구성합니다.

[!code-csharp[Main](cors/sample/CorsExample4/Startup.cs?range=44-49)]

이 옵션은 예비 요청과 Access-Control-Allow-Methods 헤더에 영향을 줍니다.

### <a name="set-the-allowed-request-headers"></a>허용되는 요청 헤더 설정하기

CORS의 예비 요청에는 클라이언트 응용 프로그램에서 설정한 HTTP 헤더들이 나열된 Access-Control-Request-Headers 헤더가 포함되어 있을 수 있습니다. 이를 일명 "사용자 지정 요청 헤더(Author Request Headers)"라고 부릅니다.

특정 헤더들에 대한 허용 목록을 만들려면 다음과 같이 구성합니다.

[!code-csharp[Main](cors/sample/CorsExample4/Startup.cs?range=53-58)]

모든 사용자 지정 요청 헤더를 허용하려면 다음과 같이 구성합니다.

[!code-csharp[Main](cors/sample/CorsExample4/Startup.cs?range=62-67)]

브라우저가 Access-Control-Request-Headers를 설정하는 방법이 완전히 일관되지는 않습니다. 따라서, "*" 이외의 값으로 헤더를 설정할 때는, 지원하고자 하는 모든 사용자 정의 헤더 외에도 최소한 "accept", "content-type" 및 "origin"은 포함시켜야 합니다.

### <a name="set-the-exposed-response-headers"></a>노출되는 응답 헤더 설정하기

기본적으로 브라우저 노출 하지 않습니다 모든 응용 프로그램에 대 한 응답 헤더입니다. (See [http://www.w3.org/TR/cors/#simple-response-header](http://www.w3.org/TR/cors/#simple-response-header).) 기본적으로 사용할 수 있는 응답 헤더에는

* Cache-Control

* Content-Language

* Content-Type

* Expires

* Last-Modified

* Pragma

CORS 명세에서는 이 헤더들을 *단순 응답 헤더(Simple Response Header)*라고 부릅니다. 응용 프로그램에서 다른 헤더들을 사용할 수 있게 하려면 다음과 같이 구성합니다.

[!code-csharp[Main](cors/sample/CorsExample4/Startup.cs?range=71-76)]

### <a name="credentials-in-cross-origin-requests"></a>교차 원본 요청의 자격 증명

CORS 요청에서 자격 증명(Credentials)은 특별한 처리를 해야 합니다. 교차 원본 요청 시, 기본적으로 브라우저는 어떠한 자격 증명도 전송하지 않습니다. 여기에서 말하는 자격 증명에는 쿠키뿐만 아니라 HTTP 인증 스킴도 포함됩니다. 교차 원본 요청 시 자격 증명을 함께 전송하려면, 클라이언트에서 XMLHttpRequest.withCredentials 속성을 true로 설정해야 합니다.

직접 XMLHttpRequest를 사용할 경우:

```javascript
var xhr = new XMLHttpRequest();
xhr.open('get', 'http://www.example.com/api/test');
xhr.withCredentials = true;
```

jQuery를 사용할 경우:

```jQuery
$.ajax({
  type: 'get',
  url: 'http://www.example.com/home',
  xhrFields: {
    withCredentials: true
}
```

또한 서버에서도 자격 증명을 허용해야만 합니다. 교차 원본 자격 증명을 허용하려면 다음과 같이 구성합니다.

[!code-csharp[Main](cors/sample/CorsExample4/Startup.cs?range=80-85)]

이 구성이 적용되면 HTTP 응답에 Access-Control-Allow-Credentials 헤더가 포함됩니다. 이 헤더는 서버가 교차 원본 요청에 대한 자격 증명을 허용한다는 것을 브라우저에 알려줍니다.

브라우저가 자격 증명을 전송하지만, 응답에 유효한 Access-Control-Allow-Credentials 헤더가 포함되어 있지 않다면, 브라우저가 응용 프로그램에게 응답을 노출하지 않으므로 AJAX 요청은 실패하게 됩니다.

사용자가 전혀 의식하지 못하는 사이에, 다른 도메인의 웹 사이트가 사용자 대신 로그인 된 사용자의 자격 증명을 응용 프로그램에 전송할 수도 있으므로, 교차 원본 자격 증명을 허용할지 여부는 대단히 심사숙고해서 결정해야만 합니다. 또한, CORS 명세서에 따라서 Access-Control-Allow-Credentials 헤더가 제공될 경우, 원본을 "*" 로 설정하는 것은 유효하지 않다는 점도 기억해두시기 바랍니다.

### <a name="set-the-preflight-expiration-time"></a>예비 요청 만료 시간 설정하기

Access-Control-Max-Age 헤더는 예비 요청에 대한 응답을 캐시할 수 있는 기간을 지정합니다. 이 헤더를 설정하려면 다음과 같이 구성합니다.

[!code-csharp[Main](cors/sample/CorsExample4/Startup.cs?range=89-94)]

<a name="cors-how-cors-works"></a>

## <a name="how-cors-works"></a>CORS의 동작 방식

이번 섹션에서는 CORS 요청 시 HTTP 메시지 수준에서 발생하는 일들을 살펴봅니다. CORS 정책을 올바르게 구성하기 위해서, 그리고 예상대로 동작하지 않는 경우 문제를 해결하기 위해서는 CORS가 동작하는 방식을 이해하는 것이 중요합니다.

CORS 명세에서는 교차 원본 요청을 활성화시키기 위한 용도로 몇 가지 새로운 HTTP 헤더들이 도입되었습니다. 그러나, 브라우저가 CORS를 지원할 경우, 교차 원본 요청 시 브라우저가 자동으로 이 헤더들을 설정해주므로 JavaScript 코드에서 직접 처리해줘야 할 작업은 전혀 없습니다.

다음은 교차 원본 요청의 실제 사례입니다. 브라우저가 요청을 생성한 사이트의 도메인이 지정된 "Origin" 헤더를 자동으로 추가해줍니다.

```
GET http://myservice.azurewebsites.net/api/test HTTP/1.1
Referer: http://myclient.azurewebsites.net/
Accept: */*
Accept-Language: en-US
Origin: http://myclient.azurewebsites.net
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
```

서버는 요청을 허용하는 경우에 한해서 Access-Control-Allow-Origin 헤더를 지정해서 응답을 반환합니다. 이 헤더의 값은 Origin 헤더 값과 동일하거나, 모든 원본이 허용됨을 뜻하는 와일드카드 값인 "*" 이어야 합니다.

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Type: text/plain; charset=utf-8
Access-Control-Allow-Origin: http://myclient.azurewebsites.net
Date: Wed, 20 May 2015 06:27:30 GMT
Content-Length: 12

Test message
```

만약, 응답에 Access-Control-Allow-Origin 헤더가 포함되어 있지 않다면 AJAX 요청은 실패합니다. 보다 구체적으로 말해서 브라우저가 요청을 허용하지 않는 것입니다. 설령 서버가 정상적인 응답을 반환하더라도, 브라우저가 그 응답을 클라이언트 응용 프로그램에서 사용할 수 있도록 허용하지 않습니다.

### <a name="preflight-requests"></a>예비 요청

브라우저는 일부 CORS 요청에 대해서, 리소스에 대한 실제 요청을 전송하기 전에, "예비 요청(Preflight Requests)"이라고 부르는 별도의 요청을 전송합니다. 다음과 같은 조건들을 만족할 경우, 브라우저는 예비 요청을 생략할 수 있습니다.

* 요청 메서드가 GET, HEAD 또는 POST 이고,

* 클라이언트 응용 프로그램이 Accept, Accept-Language, Content-Language, Content-Type 및 Last-Event-ID 이외에 다른 요청 헤더를 지정하지 않고,

* Content-Type 헤더가 (지정된 경우) 다음 중 하나인 경우:

  * application/x-www-form-urlencoded

  * multipart/form-data

  * text/plain

이 예비 요청의 헤더 관련 규칙은 `XMLHttpRequest` 개체의 `setRequestHeader`를 호출해서 클라이언트 응용 프로그램이 설정한 헤더들만을 대상으로 합니다. (CORS 명세서에서는 이런 헤더들을 "사용자 지정 요청 헤더(Author Request Headers)"라고 부릅니다.) 이 규칙은 User-Agent, Host 또는 Content-Length 같이 브라우저가 지정한 헤더에는 적용되지 않습니다.

다음은 예비 요청의 실제 사례입니다.

```
OPTIONS http://myservice.azurewebsites.net/api/test HTTP/1.1
Accept: */*
Origin: http://myclient.azurewebsites.net
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: accept, x-my-custom-header
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
Content-Length: 0
```

예비 요청에는 HTTP OPTIONS 메서드가 사용됩니다. 그리고 이 요청에는 두 가지 특별한 헤더가 존재합니다.

* Access-Control-Request-Method: 실제 요청에 사용될 HTTP 메서드가 지정됩니다.

* Access-Control-Request-Headers: 실제 요청에서 응용 프로그램이 설정할 요청 헤더들의 목록입니다. (역시 이번에도 브라우저가 설정한 헤더는 해당되지 않습니다.)

다음은 서버가 이 요청을 허용한다고 가정한 경우의 예제 응답입니다.

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 0
Access-Control-Allow-Origin: http://myclient.azurewebsites.net
Access-Control-Allow-Headers: x-my-custom-header
Access-Control-Allow-Methods: PUT
Date: Wed, 20 May 2015 06:33:22 GMT
```

이 응답에는 허용되는 메서드들의 목록이 담겨 있는 Access-Control-Allow-Methods 헤더가 포함되어 있으며, 허가된 헤더들의 목록이 지정된 Access-Control-Allow-Headers 헤더가 선택적으로 포함되어 있을 수 있습니다. 이 예비 요청이 성공한 경우, 브라우저는 앞에서 살펴봤던 것과 같은 실제 요청을 전송합니다.
