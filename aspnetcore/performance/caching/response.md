---
title: ASP.NET core에서 응답 캐싱
author: rick-anderson
description: 낮은 대역폭 요구 사항에 대응하고 ASP.NET Core 응용 프로그램의 성능을 향상시키기 위해 응답 캐싱을 사용하는 방법을 알아봅니다.
ms.author: riande
ms.date: 09/20/2017
uid: performance/caching/response
ms.openlocfilehash: 4bf61502738d70760679ec98c8f2f303eca9d504
ms.sourcegitcommit: f5d403004f3550e8c46585fdbb16c49e75f495f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2018
ms.locfileid: "49477491"
---
# <a name="response-caching-in-aspnet-core"></a>ASP.NET core에서 응답 캐싱

작성자: [John Luo](https://github.com/JunTaoLuo), [Rick Anderson](https://twitter.com/RickAndMSFT), [Steve Smith](https://ardalis.com/), 및 [Luke Latham](https://github.com/guardrex)

> [!NOTE]
> 응답에서 Razor 페이지 캐싱은 이상 ASP.NET Core 2.1에서 사용할 수 있습니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/response/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

응답 캐싱은 클라이언트나 프록시가 웹 서버에 요청하는 회수를 줄여줍니다. 또한 응답 캐싱은 웹 서버가 응답을 생성하기 위해 수행해야 하는 작업의 총량도 줄여줍니다. 응답 캐싱은 클라이언트, 프록시, 및 미들웨어가 응답을 캐싱해야 하는 방식을 지시하는 헤더에 의해 제어됩니다.

[응답 캐싱 미들웨어](xref:performance/caching/middleware)를 추가하면 웹 서버가 응답을 캐시할 수 있습니다.

## <a name="http-based-response-caching"></a>HTTP 기반 응답 캐싱

[HTTP 1.1 캐싱 사양](https://tools.ietf.org/html/rfc7234)은 인터넷 캐시가 동작해야 하는 방식을 기술합니다. 캐싱에 사용되는 가장 기본적인 HTTP 헤더는 [Cache-Control](https://tools.ietf.org/html/rfc7234#section-5.2)로 캐시 *지시문*을 지정하는 데 사용됩니다. 지시문은 요청이 클라이언트에서 서버로 전달될 때의 캐싱 동작과 응답이 서버에서 클라이언트로 되돌아올 때의 캐싱 동작을 제어합니다. 프록시 서버를 통해서 이동하는 요청 및 응답, 그리고 프록시 서버 역시 HTTP 1.1 캐싱 사양을 준수해야 합니다.

기본적인 `Cache-Control` 지시문은 다음 표와 같습니다.

| 지시문                                                       | 작업 |
| --------------------------------------------------------------- | ------ |
| [public](https://tools.ietf.org/html/rfc7234#section-5.2.2.5)   | 캐시에 응답을 저장할 수 있습니다. |
| [private](https://tools.ietf.org/html/rfc7234#section-5.2.2.6)  | 공유 캐시는 응답을 저장하지 않습니다. 사설 캐시는 응답을 저장하고 재사용할 수 있습니다. |
| [max-age](https://tools.ietf.org/html/rfc7234#section-5.2.1.1)  | 클라이언트는 지정된 초 수보다 오래된 응답을 수락하지 않습니다. 예: `max-age=60` (60초), `max-age=2592000` (1개월) |
| [no-cache](https://tools.ietf.org/html/rfc7234#section-5.2.1.4) | **요청 시**: 캐시는 저장된 응답을 사용해서 요청에 대응하면 안 됩니다. 주의: 원본 서버는 클라이언트에 대한 응답을 다시 생성하고 미들웨어는 캐시에 저장된 응답을 갱신해야 합니다.<br><br>**응답 시**: 원본 서버에서 유효성을 검사받지 않은 응답을 후속 요청에 사용하면 안 됩니다. |
| [no-store](https://tools.ietf.org/html/rfc7234#section-5.2.1.5) | **요청 시**: 캐시가 요청을 저장하지 않습니다.<br><br>**응답 시**: 캐시가 응답의 모든 부분에서 응답을 저장하지 않습니다. |

캐싱 역할을 수행하는 다른 캐시 헤더는 다음 표와 같습니다.

| 헤더                                                     | 기능 |
| ---------------------------------------------------------- | -------- |
| [Age](https://tools.ietf.org/html/rfc7234#section-5.1)     | 응답이 생성되거나 원본 서버에서 정상적으로 검증된 이후로부터 지난 초 단위의 총 추정 시간. |
| [Expires](https://tools.ietf.org/html/rfc7234#section-5.3) | 응답이 만료된 것으로 간주되는 날짜/시간. |
| [Pragma](https://tools.ietf.org/html/rfc7234#section-5.4)  | `no-cache` 동작 설정에 대한 HTTP/1.0 캐시와의 하위 호환성을 지원하기 위해 존재합니다. `Cache-Control` 헤더가 존재할 경우 `Pragma` 헤더는 무시됩니다.  |
| [Vary](https://tools.ietf.org/html/rfc7231#section-7.1.4)  | 모든 `Vary` 헤더 필드가 캐시된 응답의 원본 요청 및 새 요청 모두와 일치하지 않는 한 캐시된 응답이 전송되지 않도록 지정합니다. |

## <a name="http-based-caching-respects-request-cache-control-directives"></a>HTTP 기반 캐싱은 Cache-Control 지시문을 준수합니다

[Cache-Control 헤더에 대한 HTTP 1.1 캐싱 사양](https://tools.ietf.org/html/rfc7234#section-5.2)은 캐시에게 클라이언트가 전송하는 유효한 `Cache-Control` 헤더를 준수할 것을 요구합니다. 클라이언트는 `no-cache` 헤더 값을 설정한 요청을 전송함으로써 모든 요청에 대해 서버가 새로운 응답을 생성하도록 강제할 수 있습니다.

HTTP 캐싱의 목적을 고려했을 때 항상 클라이언트의 `Cache-Control` 요청 헤더를 준수하는 것이 이치에 맞습니다. 공식 사양에서 캐싱은 클라이언트, 프록시 및 서버 간의 네트워크에서 요청의 대기 시간 및 네트워크 오버헤드를 만족스럽게 줄이기 위한 것입니다. 원본 서버에서 부하를 제어하기 위한 방법이 필수적인 것은 아닙니다.

[응답 캐싱 미들웨어](xref:performance/caching/middleware)를 사용할 때 캐싱 동작에 관해서 개발자가 제어할 수 있는 부분은 현재 존재하지 않으며, 그 이유는 미들웨어가 공식 캐싱 사양을 따르고 있기 때문입니다. 캐시된 응답을 제공하기로 결정할 경우 미들웨어가 요청의 `Cache-Control`` 헤더를 무시하게 구성할 수 있도록 [향후에는 미들웨어를 개선](https://github.com/aspnet/ResponseCaching/issues/96)할 것입니다. 이렇게 하면 미들웨어를 사용할 때 서버의 부하를 보다 세밀하게 제어할 수 있습니다.

## <a name="other-caching-technology-in-aspnet-core"></a>ASP.NET Core의 다른 캐싱 기술

### <a name="in-memory-caching"></a>메모리 내 캐싱

메모리 내 캐싱은 서버의 메모리를 이용해서 캐시된 데이터를 저장합니다. 이 방식의 캐싱은 단일 서버나 *고정 세션*을 사용하는 복수의 서버에 적합합니다. 고정 세션은 클라이언트의 요청이 처리를 위해 항상 동일한 서버로 라우트된다는 것을 뜻합니다.

자세한 내용은 [메모리 내 캐시](xref:performance/caching/memory)를 참고하시기 바랍니다.

### <a name="distributed-cache"></a>분산 캐시

응용 프로그램이 클라우드나 서버 팜에서 호스팅될 때 메모리에 데이터를 저장하려면 분산 캐시를 사용합니다. 이 캐시는 요청을 처리하는 서버들 간에 서로 공유됩니다. 클라이언트에 대한 캐시 데이터를 사용할 수 있는 경우 클라이언트는 그룹의 어떤 서버에서나 처리할 수 있는 요청을 제출할 수 있습니다. ASP.NET Core는 SQL Server 및 Redis 분산 캐시를 제공합니다.

자세한 내용은 [분산 캐시 사용하기](xref:performance/caching/distributed)를 참고하시기 바랍니다.

### <a name="cache-tag-helper"></a>캐시 태그 도우미

캐시 태그 도우미를 사용하면 MVC 뷰 또는 Razor 페이지의 콘텐츠를 캐시할 수 있습니다. 캐시 태그 도우미는 메모리 내 캐시에 데이터를 저장합니다.

자세한 내용은 [ASP.NET Core MVC와 캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)를 참고하시기 바랍니다.

### <a name="distributed-cache-tag-helper"></a>분산 캐시 태그 도우미

분산 캐시 태그 도우미를 사용하면 분산 클라우드 또는 웹 팜 시나리오에서 MVC 뷰 또는 Razor 페이지의 콘텐츠를 캐시할 수 있습니다. 분산 캐시 태그 도우미는 SQL Server 또는 Redis에 데이터를 저장합니다.

자세한 내용은 [분산 캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)를 참고하시기 바랍니다.

## <a name="responsecache-attribute"></a>ResponseCache 특성

[ResponseCacheAttribute](/dotnet/api/Microsoft.AspNetCore.Mvc.ResponseCacheAttribute) 는 응답 캐싱이 적절한 헤더를 설정하기 위해서 필요한 매개 변수를 지정합니다.

> [!WARNING]
> 인증된 클라이언트의 정보를 포함하는 콘텐츠는 캐싱하면 안 됩니다. 사용자 ID 또는 사용자 로그인 여부와 무관하게 변경되지 않는 콘텐츠만 캐싱해야 합니다.

[VaryByQueryKeys](/dotnet/api/microsoft.aspnetcore.mvc.responsecacheattribute.varybyquerykeys) 속성은 지정한 쿼리 키 목록의 값에 따라 저장된 응답을 변경합니다. 단일 값으로 `*`를 지정하면 모든 쿼리 문자열 매개 변수별로 미들웨어의 응답이 달라집니다. `VaryByQueryKeys` 를 사용하려면 ASP.NET Core 1.1 이상이 필요합니다.

응답 캐싱 미들웨어는 반드시 `VaryByQueryKeys` 속성을 설정할 수 있어야 합니다. 그렇지 않을 경우 런타임 예외가 발생합니다. `VaryByQueryKeys` 속성에 대응하는 HTTP 헤더는 존재하지 않습니다. 이 속성은 응답 캐싱 미들웨어에 의해서 처리되는 HTTP 기능입니다. 미들웨어가 캐시된 응답을 제공하려면 쿼리 문자열 및 쿼리 문자열 값이 이전 요청과 동일해야 합니다. 예를 들어, 다음 표는 요청 순서에 따른 결과를 보여줍니다.

| 요청                          | 결과                   |
| -------------------------------- | ------------------------ |
| `http://example.com?key1=value1` | 서버에서 반환됨     |
| `http://example.com?key1=value1` | 미들웨어에서 반환됨 |
| `http://example.com?key1=value2` | 서버에서 반환됨     |

첫 번째 요청은 서버에서 반환되고 미들웨어에 캐시됩니다. 두 번째 요청은 쿼리 문자열이 이전 요청과 일치하기 때문에 미들웨어에서 반환됩니다. 세 번째 요청은 쿼리 문자열 값이 이전 요청과 일치하지 않기 때문에 미들웨어 캐시에 존재하지 않습니다. 

`ResponseCacheAttribute` 는 [ResponseCacheFilter](/dotnet/api/microsoft.aspnetcore.mvc.internal.responsecachefilter)를 구성하고 생성하기 위해서 (`IFilterFactory`를 통해서) 사용됩니다. `ResponseCacheFilter` 적절 한 HTTP 헤더 및 응답의 기능 업데이트 작업을 수행 합니다. 필터:

* 기존에 존재하는 `Vary`, `Cache-Control` 및 `Pragma` 헤더를 모두 제거합니다. 
* `ResponseCacheAttribute`에 설정된 속성을 기반으로 적절한 헤더를 작성합니다. 
* `VaryByQueryKeys` 속성이 설정된 경우 응답 캐싱 HTTP 기능을 갱신합니다.

### <a name="vary"></a>Vary

이 헤더는 `VaryByHeader` 속성이 설정된 경우에만 작성됩니다. 이 속성은 `Vary` 헤더의 값을 설정합니다. 다음 예제는 `VaryByHeader` 속성을 사용합니다:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_VaryByHeader&highlight=1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_VaryByHeader&highlight=1)]

::: moniker-end

브라우저의 네트워크 도구를 사용하면 응답 헤더를 확인할 수 있습니다. 다음 그림은 `About2` 액션 메서드를 갱신했을 때 Edge F12 개발자 도구의 **네트워크** 탭의 출력을 보여줍니다.

![About2 액션 메서드 호출 시 Edge F12 개발자 도구의 네트워크 탭의 출력](response/_static/vary.png)

### <a name="nostore-and-locationnone"></a>NoStore 및 Location.None

`NoStore` 속성은 다른 대부분의 속성을 덮어씁니다. 이 속성이 `true`로 설정되면 `Cache-Control` 헤더가 `no-store`로 설정됩니다. 만약 `Location`이 `None`으로 설정되면:

* `Cache-Control`이 `no-store,no-cache`로 설정됩니다.
* `Pragma`가 `no-cache`로 설정됩니다.

`NoStore`가 `false`로 그리고 `Location`이 `None`으로 설정되면, `Cache-Control` 및 `Pragma`가 `no-cache`로 설정됩니다.

일반적으로 오류 페이지에서 `NoStore`를 `true`로 설정하는 경우가 많습니다. 예를 들어:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet1&highlight=1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet1&highlight=1)]

::: moniker-end

그 결과 다음과 같은 헤더가 만들어집니다:

```
Cache-Control: no-store,no-cache
Pragma: no-cache
```

### <a name="location-and-duration"></a>Location 및 Duration

캐싱을 사용하기 위해서는 `Duration`을 양수 값으로 설정하고 `Location`이 `Any` (기본값) 또는 `Client`이어야 합니다. 이 경우 `Cache-Control` 헤더는 응답의 `max-age`가 뒤에 추가된 위치 값으로 설정됩니다.

> [!NOTE]
> `Location` 옵션의 `Any`와 `Client`는 각각 `Cache-Control` 헤더의 값, `public`과 `private`로 변환됩니다. 앞에서 설명한 것처럼 `Location`을 `None`으로 설정하면 `Cache-Control` 및 `Pragma` 헤더가 모두 `no-cache`로 설정됩니다.

다음은 `Duration`을 설정하고 `Location`을 기본 값 그대로 변경하지 않고 생성하는 헤더를 보여주는 예제입니다:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_duration&highlight=1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_duration&highlight=1)]

::: moniker-end

이 코드는 다음과 같은 헤더를 생성합니다.

```
Cache-Control: public,max-age=60
```

### <a name="cache-profiles"></a>캐시 프로필

수 많은 컨트롤러 액션 속성마다 `ResponseCache` 설정을 반복하는 대신, `Startup`의 `ConfigureServices` 메서드에서 MVC를 설정할 때 캐시 프로필을 옵션으로 설정할 수 있습니다. 참조된 캐시 프로필에 지정된 값은 `ResponseCache` 특성에 의해 기본값으로 사용되며 특성에 지정된 모든 속성에 의해 덮어써집니다.

먼저 캐시 프로필을 설정합니다.

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Startup.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Startup.cs?name=snippet1)]

::: moniker-end

그리고 캐시 프로필을 참조합니다:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_controller&highlight=1,4)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_controller&highlight=1,4)]

::: moniker-end

`ResponseCache` 특성은 액션(메서드) 및 컨트롤러(클래스) 모두에 적용할 수 있습니다. 메서드 수준 특성은 클래스 수준 특성에 지정된 설정을 덮어씁니다.

위의 예제에서는 클래스 수준 특성이 30초의 지속 시간을 지정하는 반면, 메서드 수준 특성은 지속 시간이 60초로 설정된 캐시 프로필을 참조하고 있습니다.

결과 헤더:

```
Cache-Control: public,max-age=60
```

## <a name="additional-resources"></a>추가 자료

* [캐시에 응답 저장하기](https://tools.ietf.org/html/rfc7234#section-3)
* [Cache-Control](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [메모리 내 캐시](xref:performance/caching/memory)
* [분산 캐시 사용하기](xref:performance/caching/distributed)
* [변경 토큰을 이용해서 변경 감지하기](xref:fundamentals/change-tokens)
* [응답 캐싱 미들웨어](xref:performance/caching/middleware)
* [캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [분산 캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
