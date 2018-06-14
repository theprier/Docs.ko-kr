---
title: ASP.NET Core의 응답 캐싱 미들웨어
author: guardrex
description: ASP.NET Core에서 응답 캐싱 미들웨어를 구성하고 사용하는 방법을 알아봅니다.
manager: wpickett
monikerRange: '>= aspnetcore-1.1'
ms.author: riande
ms.custom: mvc
ms.date: 01/26/2017
ms.prod: asp.net-core
ms.topic: article
uid: performance/caching/middleware
ms.openlocfilehash: abf07ec2d2692a8504caea243eacead6aa6e1a62
ms.sourcegitcommit: 7e87671fea9a5f36ca516616fe3b40b537f428d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35341706"
---
# <a name="response-caching-middleware-in-aspnet-core"></a>ASP.NET Core의 응답 캐싱 미들웨어

작성자: [Luke Latham](https://github.com/guardrex) 및 [John Luo](https://github.com/JunTaoLuo)

[보기 또는 ASP.NET Core 2.1 샘플 코드를 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/middleware/samples) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample))

이 문서에서는 ASP.NET Core 응용 프로그램에서 응답 캐싱 미들웨어를 구성하는 방법을 알아봅니다. 미들웨어는 응답을 캐싱할 수 있는 시점을 결정하고 응답을 저장하고 캐시에서 가져온 응답을 제공합니다. HTTP 캐싱 및 `ResponseCache` 특성에 대한 소개는 [응답 캐싱](xref:performance/caching/response)을 참고하시기 바랍니다.

## <a name="package"></a>패키지

미들웨어를 프로젝트에 포함 하려면에 대 한 참조를 추가 [Microsoft.AspNetCore.ResponseCaching](https://www.nuget.org/packages/Microsoft.AspNetCore.ResponseCaching/) 패키지 하거나 사용 하 여는 [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app), ASP에서 사용 하기 위해 사용할 수 있습니다. NET 핵심 2.1 이상입니다.

## <a name="configuration"></a>구성

`ConfigureServices`에서 서비스 컬렉션에 미들웨어를 추가합니다.

[!code-csharp[](middleware/samples/2.x/ResponseCachingMiddleware/Startup.cs?name=snippet1&highlight=9)]

그리고 미들웨어를 요청 처리 파이프라인에 추가하는 `UseResponseCaching` 확장 메서드를 이용해서 응용 프로그램이 미들웨어를 사용하도록 구성합니다. 예제 응용 프로그램은 최대 10초 동안 캐시가 응답을 캐싱할 수 있도록 [`Cache-Control`](https://tools.ietf.org/html/rfc7234#section-5.2) 헤더를 응답에 추가합니다. 또한 [`Vary`](https://tools.ietf.org/html/rfc7231#section-7.1.4) 헤더를 전송해서 후속 요청의 [`Accept-Encoding`](https://tools.ietf.org/html/rfc7231#section-5.3.4) 헤더가 원본 요청과 일치하는 경우에만 캐시된 응답을 제공하도록 미들웨어를 구성합니다. 다음 예제 코드에서 [CacheControlHeaderValue](/dotnet/api/microsoft.net.http.headers.cachecontrolheadervalue) 및 [HeaderNames](/dotnet/api/microsoft.net.http.headers.headernames)를 사용하려면 [Microsoft.Net.Http.Headers](/dotnet/api/microsoft.net.http.headers) 네임스페이스에 대한 `using` 문이 필요합니다.

[!code-csharp[](middleware/samples/2.x/ResponseCachingMiddleware/Startup.cs?name=snippet2&highlight=17,21-28)]

응답 캐싱 미들웨어는 상태 코드가 200(정상)인 서버 응답만 캐시합니다. [오류 페이지](xref:fundamentals/error-handling)를 비롯한 다른 모든 응답은 미들웨어에 의해 무시됩니다.

> [!WARNING]
> 인증된 클라이언트에 대한 콘텐츠를 포함하고 있는 응답은 미들웨어가 해당 응답을 저장하거나 제공하는 것을 막을 수 있도록 반드시 캐시가 불가능한 것으로 표시해야 합니다. 미들웨어가 캐싱할 수 있는 응답인지 여부를 판단하는 방법에 대한 자세한 내용은 [캐싱 조건](#conditions-for-caching)을 참고하시기 바랍니다.

## <a name="options"></a>옵션

미들웨어는 응답 캐싱을 제어하기 위한 세 가지 옵션을 제공합니다.

| 옵션                | 설명 |
| --------------------- | ----------- |
| UseCaseSensitivePaths | 경로의 대/소문자를 구분해서 응답을 캐시할지 결정합니다. 기본값은 `false`입니다. |
| MaximumBodySize       | 캐시 가능한 응답 본문의 최대 바이트 크기입니다. 기본값은 `64 * 1024 * 1024`(64MB)입니다. |
| SizeLimit             | 응답 캐싱 미들웨어의 바이트 크기 제한입니다. 기본값은 `100 * 1024 * 1024`(100MB)입니다. |

아래 예제는 미들웨어를 다음과 같이 구성합니다.

* 1,024바이트 이하의 응답을 캐시합니다.
* 경로의 대/소문자를 구분해서 응답을 저장합니다(예를 들어 `/page1`과 `/Page1`을 별도로 저장합니다).

```csharp
services.AddResponseCaching(options =>
{
    options.UseCaseSensitivePaths = true;
    options.MaximumBodySize = 1024;
});
```

## <a name="varybyquerykeys"></a>VaryByQueryKeys

MVC/Web API 컨트롤러 또는 Razor Pages 페이지 모델을 사용할 때 `ResponseCache` 특성은 응답 캐싱을 위한 적절한 헤더를 설정하기 위해 필요한 매개 변수를 지정합니다. 미들웨어가 반드시 필요한 `ResponseCache` 특성의 유일한 매개 변수는 `VaryByQueryKeys`로, 이 매개 변수는 실제 HTTP 헤더와 일치하지 않습니다. 자세한 내용은 [ResponseCache 특성](xref:performance/caching/response#responsecache-attribute)을 참고하시기 바랍니다.

`ResponseCache` 특성을 사용하지 않을 경우, `VaryByQueryKeys` 기능을 사용해서 응답 캐싱을 변경할 수 있습니다. 사용 하 여 `ResponseCachingFeature` 에서 직접는 `IFeatureCollection` 의 `HttpContext`:

```csharp
var responseCachingFeature = context.HttpContext.Features.Get<IResponseCachingFeature>();
if (responseCachingFeature != null)
{
    responseCachingFeature.VaryByQueryKeys = new[] { "MyKey" };
}
```

`*`에 `VaryByQueryKeys` 와 동일한 단일 값을 지정하면 모든 요청 쿼리 매개 변수에 따라 캐시가 변경됩니다.

## <a name="http-headers-used-by-response-caching-middleware"></a>응답 캐싱 미들웨어에서 사용되는 HTTP 헤더

미들웨어에 의한 응답 캐싱은 HTTP 헤더를 이용해서 구성됩니다.

| 헤더 | 설명 |
| ------ | ------- |
| Authorization | 이 헤더가 존재할 경우 응답이 캐시되지 않습니다. |
| 캐시 제어 | 미들웨어는 `public` 캐시 지시문으로 표시된 캐싱 응답만 고려합니다. 다음 매개 변수로 캐싱을 제어하십시오.<ul><li>최대 처리 기간</li><li>max-stale&#8224;</li><li>최소 새로</li><li>must-revalidate</li><li>캐시 없음</li><li>저장소 아니요</li><li>전용-if-캐시</li><li>private</li><li>public</li><li>기간</li><li>proxy-revalidate&#8225;</li></ul>&#8224; `max-stale`에 제한이 지정되지 않으면 미들웨어는 아무런 작업도 하지 않습니다.<br>&#8225; `proxy-revalidate`는 `must-revalidate`와 동일한 효과를 갖습니다.<br><br>자세한 내용은 [RFC 7231: 요청 Cache-Control 지시문](https://tools.ietf.org/html/rfc7234#section-5.2.1)을 참고하시기 바랍니다. |
| Pragma | 요청에 지정된 `Pragma: no-cache` 헤더는 `Cache-Control: no-cache`와 동일한 효과를 갖습니다. 이 헤더는 `Cache-Control` 헤더가 존재할 경우, 지정된 관련 지시문에 의해 재정의됩니다. HTTP/1.0에 대한 하위 호환성을 감안하기 위한 헤더입니다. |
| Set-cookie | 이 헤더가 존재할 경우 응답이 캐시되지 않습니다. 하나 이상의 쿠키를 설정하는 요청 처리 파이프라인의 모든 미들웨어는 응답 캐싱 미들웨어가 응답을 캐싱하지 못하게 합니다(예를 들어 [쿠키 기반 TempData 공급자](xref:fundamentals/app-state#tempdata)).  |
| Vary | `Vary` 헤더는 다른 헤더를 이용해서 캐싱된 응답을 변경하기 위해서 사용됩니다. 예를 들어, `Vary: Accept-Encoding` 헤더가 지정된 요청과 `Accept-Encoding: gzip` 헤더가 지정된 요청에 대한 응답을 별도로 캐시하는 `Accept-Encoding: text/plain` 헤더를 지정해서 인코딩된 응답을 캐시할 수 있습니다. 헤더 값이 `*`인 응답은 절대로 저장되지 않습니다. |
| Expires | 이 헤더에 의해 낡은 것으로 간주되는 응답은 다른 `Cache-Control` 헤더에 의해서 재정의되지 않는 한 저장되거나 조회되지 않습니다. |
| None-If-match | 값이 `*`가 아니고 응답의 `ETag`가 제공된 모든 값과 일치하지 않으면 전체 응답이 캐시에서 제공됩니다. 그렇지 않으면 304(수정되지 않음) 응답이 제공됩니다. |
| If-수정-이후 | `If-None-Match` 헤더가 존재하지 않으면, 캐시된 응답 날짜가 제공된 값보다 새로운 경우 전체 응답이 캐시에서 제공됩니다. 그렇지 않으면 304(수정되지 않음) 응답이 제공됩니다. |
| Date | 캐시에서 응답을 제공할 때, 원본 응답이 `Date` 헤더를 제공하지 않으면 미들웨어에 의해 설정됩니다. |
| Content-Length | 캐시에서 응답을 제공할 때, 원본 응답이`Content-Length` 헤더를 제공하지 않으면 미들웨어에 의해 설정됩니다. |
| 보존 기간 | 원본 응답이 전송한 `Age` 헤더는 무시됩니다. 캐시된 응답을 제공할 때 미들웨어가 새로운 값을 계산합니다. |

## <a name="caching-respects-request-cache-control-directives"></a>캐싱에서 요청 Cache-Control 지시문 사용

미들웨어는 [HTTP 1.1 캐싱 사양](https://tools.ietf.org/html/rfc7234#section-5.2)의 규칙을 준수합니다. 그리고 이 규칙은 캐시가 클라이언트에 의해서 전송된 유효한 `Cache-Control` 헤더를 준수할 것을 요구합니다. 사양에 따라 클라이언트는`no-cache` 헤더 값을 설정한 요청을 전송함으로써 모든 요청에 대해 서버가 새로운 응답을 생성하도록 강제할 수 있습니다. 현재 미들웨어를 사용할 때 이 캐싱 동작을 개발자가 제어할 수 있는 방법은 없으며, 그 이유는 미들웨어가 공식 캐싱 사양을 따르고 있기 때문입니다.

캐싱 동작을 보다 세세히 제어하려면 ASP.NET Core의 다른 캐싱 기능을 살펴보십시오. 다음 항목을 참고하시기 바랍니다.

* [메모리 내 캐시](xref:performance/caching/memory)
* [분산 캐시 사용하기](xref:performance/caching/distributed)
* [ASP.NET Core MVC의 캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [분산 캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)

## <a name="troubleshooting"></a>문제 해결

캐싱이 예상과 다르게 동작한다면 응답이 캐싱 가능하고 캐시에서 제공될 수 있는지 확인하시기 바랍니다. 요청의 수신 헤더와 응답의 송신 헤더를 점검해보십시오. 디버깅에 도움이 되도록 [로깅](xref:fundamentals/logging/index)을 활성화하시기 바랍니다.

캐싱 동작을 테스트하거나 문제를 해결할 때, 브라우저가 원하지 않는 방식으로 캐싱에 영향을 주는 요청 헤더를 설정할 수도 있습니다. 예를 들어 페이지를 새로 고칠 때 브라우저가 `Cache-Control` 헤더를 `no-cache` 또는 `max-age=0`로 설정할 수 있습니다. 다음 도구를 사용하면 명시적으로 요청 헤더를 설정할 수 있고 캐싱 테스트에도 적합합니다.

* [Fiddler](https://www.telerik.com/fiddler)
* [Postman](https://www.getpostman.com/)

### <a name="conditions-for-caching"></a>캐싱 조건

* 요청의 결과로 200(OK) 상태 코드가 설정된 서버 응답을 받아야 합니다.
* 요청 메서드가 GET 또는 HEAD여야 합니다.
* [정적 파일 미들웨어](xref:fundamentals/static-files) 같은 터미널 미들웨어는 반드시 응답 캐싱 미들웨어보다 먼저 응답을 처리해야 합니다.
* `Authorization` 헤더가 없어야 합니다.
* `Cache-Control` 헤더의 매개 변수가 유효해야 하고 응답이 `public`으로 표시되어야 하며 `private`로 표시되지 않아야 합니다.
* `Pragma: no-cache`가 있으면 `Cache-Control` 헤더가 `Pragma` 헤더를 덮어쓰므로 `Cache-Control` 헤더가 없는 경우 no-cache header가 없어야 합니다.
* `Set-Cookie` 헤더가 없어야 합니다.
* `Vary` 헤더의 매개 변수가 유효해야 하고 `*`가 아니어야 합니다.
* `Content-Length` 헤더의 값이 (설정된 경우) 응답 본문의 크기와 일치해야 합니다.
* [IHttpSendFileFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpsendfilefeature) 가 사용되지 않아야 합니다.
* 응답이 `Expires` 헤더와 `max-age` 및 `s-maxage` 캐시 지시문에 지정된 것보다 오래되면 안 됩니다.
* 응답 버퍼링 성공 이어야 하며 응답 크기가 구성 된 보다 작은 또는 기본 `SizeLimit`합니다.
* 응답은 [RFC 7234](https://tools.ietf.org/html/rfc7234) 사양에 따라 캐시 가능해야 합니다. 예를 들어 `no-store` 지시문이 요청 또는 응답 헤더 필드에 없어야 합니다. 자세한 내용은 [RFC 7234](https://tools.ietf.org/html/rfc7234)의 *Section 3: Storing Responses in Caches*를 참고하시기 바랍니다.

> [!NOTE]
> 교차 사이트 요청 위조(CSRF, Cross-Site Request Forgery) 방지를 위한 보안 토큰을 생성하는 Antiforgery 시스템은 `Cache-Control` 및 `Pragma` 헤더를 `no-cache`로 설정하기 때문에 응답이 캐시되지 않습니다. HTML 폼 요소에 대한 Antiforgery 토큰을 비활성화시키는 방법에 대한 정보는 [ASP.NET Core Antiforgery 구성](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration)을 참고하시기 바랍니다.

## <a name="additional-resources"></a>추가 자료

* [응용 프로그램 시작](xref:fundamentals/startup)
* [미들웨어](xref:fundamentals/middleware/index)
* [메모리 내 캐시](xref:performance/caching/memory)
* [분산 캐시 사용하기](xref:performance/caching/distributed)
* [변경 토큰을 이용해서 변경 감지하기](xref:fundamentals/primitives/change-tokens)
* [응답 캐싱](xref:performance/caching/response)
* [캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [분산 캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
