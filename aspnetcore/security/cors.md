---
title: "교차 원본 요청(CORS) 활성화시키기"
author: rick-anderson
description: "본문에서는 ASP.NET Core 응용 프로그램에서 교차-원본 요청을 허용하거나 거부하는 표준 CORS를 소개합니다."
manager: wpickett
ms.author: riande
ms.date: 05/17/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/cors
ms.openlocfilehash: ee61798fc1bde89ca3712eae9b7c4413e58cf70d
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="enabling-cross-origin-requests-cors"></a>교차 원본 요청(CORS) 활성화시키기

작성자: [Mike Wasson](https://github.com/mikewasson), [Shayne Boyer](https://twitter.com/spboyer), 및 [Tom Dykstra](https://github.com/tdykstra)

브라우저의 보안 기능은 웹 페이지에서 다른 도메인으로 AJAX 요청을 전송하는 것을 막습니다. 이 제약 사항을 *동일 원본 정책(Same-Origin Policy)*이라고 부르며, 악의적인 사이트가 다른 사이트의 민감한 데이터를 무차별적으로 읽는 것을 방지합니다. 그러나 경우에 따라서는 다른 사이트가 여러분의 Web API에 교차 원본 요청(Cross-Origin Requests)을 전송하는 것을 허용해야 할 수도 있습니다.

[교차 원본 자원 공유](http://www.w3.org/TR/cors/) (CORS, Cross Origin Resource Sharing)는 서버 측에서 동일 원본 정책을 완화할 수 있게 해주는 W3C 표준입니다. CORS를 사용하면 서버가 명시적으로 특정 교차 원본 요청만 허용하고, 다른 요청은 거부할 수 있습니다. CORS는 [JSONP](https://wikipedia.org/wiki/JSONP) 같은 기존의 다른 기술보다 안전하고 유연합니다. 본문에서는 ASP.NET Core 응용 프로그램에서 CORS를 활성화시키는 방법을 알아봅니다.

## <a name="what-is-same-origin"></a>"동일 원본"이란?

두 URL의 스키마, 호스트 및 포트가 모두 동일한 경우, 두 URL의 원본이 동일하다고 말합니다. ([RFC 6454](http://tools.ietf.org/html/rfc6454))

다음 두 URL은 동일한 원본입니다.

* `http://example.com/foo.html`

* `http://example.com/bar.html`

반면, 다음 URL들은 위의 두 URL과는 다른 원본입니다.

* `http://example.net` -도메인이 다릅니다

* `http://www.example.com/foo.html` -하위 도메인이 다릅니다

* `https://example.com/foo.html` -스키마가 다릅니다

* `http://example.com:9000/foo.html` -포트가 다릅니다

> [!NOTE]
> Internet Explorer는 원본을 비교할 때 포트를 고려하지 않습니다.

## <a name="setting-up-cors"></a>CORS 설정하기

ASP.NET Core 응용 프로그램에 CORS를 설정하려면 프로젝트에 `Microsoft.AspNetCore.Cors` 패키지를 설치합니다.

그리고 Startup.cs에 CORS 서비스를 추가합니다.

[!code-csharp[](cors/sample/CorsExample1/Startup.cs?name=snippet_addcors)]

## <a name="enabling-cors-with-middleware"></a>미들웨어를 이용해서 CORS 활성화시키기

전체 응용 프로그램에서 CORS를 활성화시키려면 `UseCors` 확장 메서드를 이용해서 요청 파이프라인에 CORS 미들웨어를 추가합니다. 참고로 교차 원본 요청을 지원하고자 하는 응용 프로그램 내의 모든 정의된 끝점보다  `UseMvc` 를 호출하기 전에 CORS 미들웨어를 먼저 파이프라인에 추가해야 합니다.

CORS 미들웨어를 추가할 때, `CorsPolicyBuilder` 클래스를 이용해서 원본 간 정책을 지정할 수 있습니다. 구체적인 방법은 두 가지입니다. 먼저, 첫 번째 방법은 람다를 전달해서 `UseCors`를 호출하는 것입니다.

[!code-csharp[](cors/sample/CorsExample1/Startup.cs?highlight=11,12&range=22-38)]

**참고:** 반드시 후행 슬래시`/`가 없는 URL을 지정해야 합니다. 만약 URL이 `/` 로 끝나면, 비교 결과가 `false` 를 반환하여 아무런 헤더도 반환되지 않습니다.

람다는 `CorsPolicyBuilder` 개체를 전달받습니다. [구성 옵션](#cors-policy-options) 의 목록은 잠시 후 다시 살펴봅니다. 이 예제 코드의 정책은 `http://example.com` 에서 전달된 교차 원본 요청은 허용하지만, 다른 원본의 요청은 허용하지 않습니다.

CorsPolicyBuilder는 Fluent API를 지원하므로 다음과 같이 메서드 호출을 연결할 수 있습니다.

[!code-csharp[](../security/cors/sample/CorsExample3/Startup.cs?highlight=3&range=29-32)]

두 번째 방법은 미리 한 가지 이상의 명명된 CORS 정책을 정의한 다음, 런타임 시에 이름을 지정해서 정책을 선택하는 것입니다.

[!code-csharp[](cors/sample/CorsExample2/Startup.cs?name=snippet_begin)]

이 예제는 "AllowSpecificOrigin"이라는 CORS 정책을 추가합니다. 그리고 `UseCors` 메서드에 이름을 전달해서 정책을 선택합니다.

## <a name="enabling-cors-in-mvc"></a>MVC에서 CORS 활성화시키기

MVC를 이용해서 액션별, 컨트롤러별 또는 모든 컨트롤러에 대해 전역으로 특정 CORS를 적용할 수도 있습니다. MVC를 이용해서 CORS를 활성화시키는 경우에도 동일한 CORS 서비스가 사용되지만, 이 경우 CORS 미들웨어는 사용되지 않습니다.

### <a name="per-action"></a>액션 별

특정 액션에 CORS 정책을 지정하려면 해당 액션에 `[EnableCors]` 특성을 추가합니다. 이때 정책 이름을 전달합니다.

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnAction)]

### <a name="per-controller"></a>컨트롤러 별

특정 컨트롤러에 CORS 정책을 지정하려면 해당 컨트롤러에 `[EnableCors]` 특성을 추가합니다. 이때 정책 이름을 전달합니다.

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnController)]

### <a name="globally"></a>전역으로

모든 컨트롤러에서 전역으로 CORS를 활성화시키려면, 전역 필터 컬렉션에 `CorsAuthorizationFilterFactory` 필터를 추가합니다.

[!code-csharp[](cors/sample/CorsMVC/Startup2.cs?name=snippet_configureservices)]

특성의 우선 순위는 액션, 컨트롤러, 전역 순입니다. 다시 말해서, 액션 수준 정책은 컨트롤러 수준 정책보다 우선하며, 컨트롤러 수준 정책은 전역 정책보다 우선합니다.

### <a name="disable-cors"></a>CORS 비활성시키기

컨트롤러나 액션의 CORS를 비활성화시키려면, `[DisableCors]` 특성을 적용합니다.

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=DisableOnAction)]

## <a name="cors-policy-options"></a>CORS 정책 옵션

이번 섹션에서는 CORS 정책에서 설정할 수 있는 다양한 옵션들을 살펴봅니다.

* [허용되는 원본 설정하기](#set-the-allowed-origins)

* [허용되는 HTTP 메서드 설정하기](#set-the-allowed-http-methods)

* [허용되는 요청 헤더 설정하기](#set-the-allowed-request-headers)

* [노출되는 응답 헤더 설정하기](#set-the-exposed-response-headers)

* [교차 원본 요청의 자격 증명](#credentials-in-cross-origin-requests)

* [예비 요청 만료 시간 설정하기](#set-the-preflight-expiration-time)

일부 옵션의 경우, [CORS의 동작 방식](#how-cors-works) 섹션을 먼저 읽어보는 것이 이해에 도움이 됩니다.

### <a name="set-the-allowed-origins"></a>허용되는 원본 설정하기

하나 이상의 특정 원본을 허용하려면 다음과 같이 구성합니다.

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=19-23)]

모든 원본을 허용하려면 다음과 같이 구성합니다.

[!code-csharp[](cors/sample/CorsExample4/Startup.cs??range=27-31)]

모든 원본의 요청을 허용하기 전에 신중히 고민하시기 바랍니다. 이는 문자 그대로 모든 웹 사이트에서 응용 프로그램에 AJAX 호출을 전송할 수 있음을 뜻합니다.

### <a name="set-the-allowed-http-methods"></a>허용되는 HTTP 메서드 설정하기

모든 HTTP 메서드를 허용하려면 다음과 같이 구성합니다.

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=44-49)]

이 옵션은 예비 요청과 Access-Control-Allow-Methods 헤더에 영향을 줍니다.

### <a name="set-the-allowed-request-headers"></a>허용되는 요청 헤더 설정하기

CORS의 예비 요청에는 클라이언트 응용 프로그램에서 설정한 HTTP 헤더들이 나열된 Access-Control-Request-Headers 헤더가 포함되어 있을 수 있습니다. 이를 일명 "사용자 지정 요청 헤더(Author Request Headers)"라고 부릅니다.

특정 헤더들에 대한 허용 목록을 만들려면 다음과 같이 구성합니다.

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=53-58)]

모든 사용자 지정 요청 헤더를 허용하려면 다음과 같이 구성합니다.

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=62-67)]

브라우저가 Access-Control-Request-Headers를 설정하는 방법이 완전히 일관되지는 않습니다. 따라서, "*" 이외의 값으로 헤더를 설정할 때는, 지원하고자 하는 모든 사용자 정의 헤더 외에도 최소한 "accept", "content-type" 및 "origin"은 포함시켜야 합니다.

### <a name="set-the-exposed-response-headers"></a>노출되는 응답 헤더 설정하기

기본적으로 브라우저는 클라이언트 응용 프로그램에 모든 응답 헤더를 노출하지 않습니다. ([http://www.w3.org/TR/cors/#simple-response-header](http://www.w3.org/TR/cors/#simple-response-header) 참고). 기본적으로 사용 가능한 응답 헤더들은 다음과 같습니다.

* Cache-Control

* Content-language

* Content-Type

* Expires

* Last-Modified

* Pragma

CORS 명세에서는 이 헤더들을 *단순 응답 헤더(Simple Response Header)* 라고 부릅니다. 응용 프로그램에서 다른 헤더들을 사용할 수 있게 하려면 다음과 같이 구성합니다.

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=71-76)]

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

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=80-85)]

이 구성이 적용되면 HTTP 응답에 Access-Control-Allow-Credentials 헤더가 포함됩니다. 이 헤더는 서버가 교차 원본 요청에 대한 자격 증명을 허용한다는 것을 브라우저에 알려줍니다.

브라우저가 자격 증명을 전송하지만, 응답에 유효한 Access-Control-Allow-Credentials 헤더가 포함되어 있지 않다면, 브라우저가 응용 프로그램에게 응답을 노출하지 않으므로 AJAX 요청은 실패하게 됩니다.

크로스-원본 자격 증명을 허용할 때 주의 해야 합니다. 다른 도메인에서 웹 사이트에 로그인 한 사용자의 자격 증명에서 사용자 모르게 사용자 대신 응용 프로그램에 보낼 수 있습니다. CORS 사양에 해당 설정 설명과 함께 원본이 "*" (모든 원본을) 유효 하지 하는 경우는 `Access-Control-Allow-Credentials` 헤더가 있으면 헤더입니다.

### <a name="set-the-preflight-expiration-time"></a>예비 요청 만료 시간 설정하기

Access-Control-Max-Age 헤더는 예비 요청에 대한 응답을 캐시할 수 있는 기간을 지정합니다. 이 헤더를 설정하려면 다음과 같이 구성합니다.

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=89-94)]

<a name="cors-how-cors-works"></a>

## <a name="how-cors-works"></a>CORS의 동작 방식

이번 섹션에서는 CORS 요청 시 HTTP 메시지 수준에서 발생하는 일들을 살펴봅니다. CORS 정책을 올바르게 구성하기 위해서, 그리고 예상대로 동작하지 않는 경우 문제를 해결하기 위해서는 CORS가 동작하는 방식을 이해하는 것이 중요합니다.

CORS 명세에서는 교차 원본 요청을 활성화시키기 위한 용도로 몇 가지 새로운 HTTP 헤더들이 도입되었습니다. 그러나, 브라우저가 CORS를 지원할 경우, 교차 원본 요청 시 브라우저가 자동으로 이 헤더들을 설정해주므로 JavaScript 코드에서 직접 처리해줘야 할 작업은 전혀 없습니다.

크로스-원본 요청의 예를 들면 다음과 같습니다. `Origin` 헤더는 요청을 수행 하는 사이트의 도메인을 제공 합니다.

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

서버 요청을 허용 하는 경우 응답에 대 한 액세스 제어-허용-원본 헤더를 설정 합니다. 이 헤더의 값은 요청에서 원본 헤더 마치도록 와일드 카드 값 "*", 모든 원본을 허용 되는 의미 합니다.

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

응답에는 액세스 제어-허용-원본 헤더가 포함 되지 않은, AJAX 요청이 실패 합니다. 특히, 브라우저 요청을 허용 하지 않습니다. 성공적인 응답을 반환 하는 서버, 경우에 브라우저 하지 않는 응답을 사용할 수 있도록 클라이언트 응용 프로그램입니다.

### <a name="preflight-requests"></a>실행 전 요청

일부 CORS 요청에 대 한 브라우저의 리소스에 대 한 실제 요청을 보내기 전에 "실행 전 요청" 라는 추가 요청을 보냅니다. 다음 조건에 해당할 경우 브라우저에서 실행 전 요청을 건너뛸 수 있습니다.:

* 요청 메서드는 GET, HEAD 또는 POST 및

* 응용 프로그램 Accept, Accept-language, Content-language 이외의 모든 요청 헤더를 설정 하지 않는 콘텐츠 형식 또는 마지막-이벤트-ID 및

* 콘텐츠 형식 헤더 (하는 경우 설정) 다음 중 하나입니다.

  * application/x-www-form-urlencoded

  * multipart/폼 데이터

  * 텍스트/일반

요청 헤더에 대 한 규칙 setRequestHeader XMLHttpRequest 개체에서 호출 하 여 응용 프로그램을 설정 하는 헤더에 적용 됩니다. (이러한 작성자 요청 "헤더" CORS 사양을 호출합니다.) 규칙은 브라우저 등을 설정할 수, 사용자 에이전트, 호스트 또는 Content-length 헤더에 적용 되지 않습니다.

실행 전 요청의 예는 다음과 같습니다.

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

전 요청의 HTTP OPTIONS 메서드를 사용합니다. 두 개의 특수 헤더를 포함합니다.

* 액세스-컨트롤-요청-방법: 실제 요청에 사용할 HTTP 메서드.

* 액세스 제어-요청-헤더만: 응용 프로그램은 실제 요청에 설정 하는 요청 헤더의 목록. (다시 여기 포함 되지 않습니다 브라우저 설정 하는 헤더입니다.)

다음은 서버에서 요청을 허용 하는 것으로 가정 하는 예제 응답이입니다.

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

허용 되는 메서드를 나열 하는 액세스 제어-허용-방법 헤더 및 필요에 따라 허용된 된 헤더를 나열 하는 액세스 제어-허용-헤더만 헤더가 응답에 포함 되어 있습니다. 실행 전 요청이 성공 하면 앞에서 설명한 대로 브라우저 실제 요청을 보냅니다.
