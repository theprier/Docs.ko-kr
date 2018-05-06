---
title: "ASP.NET Core와 URL 재작성 미들웨어"
author: guardrex
description: "ASP.NET Core 응용 프로그램에서 URL 재작성 미들웨어로 URL 재작성 및 리디렉션 하는 방법에 대해 알아봅니다."
manager: wpickett
ms.author: riande
ms.date: 08/17/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/url-rewriting
ms.openlocfilehash: ca1f2f366bcf12cd3df83c3cdefa460cb9a68e2a
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="url-rewriting-middleware-in-aspnet-core"></a>ASP.NET Core와 URL 재작성 미들웨어

작성자: [Luke Latham](https://github.com/guardrex) 및 [Mikael Mengistu](https://github.com/mikaelm12)

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

URL 재작성은 미리 정의한 하나 이상의 규칙을 기반으로 요청받은 URL을 수정하는 작업입니다. URL 재작성은 리소스의 위치와 주소 간의 관계를 추상화함으로써 위치와 주소가 강력하게 연결되지 않게 해줍니다. 다음은 URL 재작성이 유용한 몇 가지 시나리오입니다: 
* 서버 리소스에 대한 안정적인 로케이터를 유지하는 동시에 임시 또는 영구적으로 해당 리소스를 이동하거나 교체하기 
* 다른 응용 프로그램 간에 또는 한 응용 프로그램의 여러 영역 간에 요청 처리 분리하기 
* 들어오는 요청의 URL 세그먼트를 제거, 추가, 또는 재구성하기 
* 검색 엔진 최적화(SEO, Search Engine Optimization)를 위해 공개 URL 최적화하기 
* 링크로 이동했을 때 제공되는 콘텐츠를 사용자가 예측할 수 있도록 친숙한 공개 URL 사용하기 
* 안전하지 않은 요청을 보안 끝점으로 리디렉션하기 
* 이미지 핫링크 방지하기 

URL을 변경하기 위한 규칙은 정규식, Apache mod_rewrite 모듈 규칙, IIS 재작성 모듈 규칙, 그리고 사용자 지정 규칙 로직 사용 등의 다양한 방법으로 정의할 수 있습니다. 본문에서는 ASP.NET Core 응용 프로그램에서 URL 재작성 미들웨어를 사용하는 방법에 관한 지침과 URL 재작성에 관해서 살펴봅니다.

> [!NOTE]
> URL 재작성은 응용 프로그램의 성능을 저하시킬 수 있습니다. 가능한 한 규칙의 수와 복잡성을 제한해야 합니다. 

## <a name="url-redirect-and-url-rewrite"></a>URL 리디렉션 및 URL 재작성
*URL 리디렉션*과 *URL 재작성* 간의 단어 차이는 언뜻 보기에는 대단한 것 같지 않지만, 클라이언트에게 리소스를 제공할 때 많은 영향을 미칩니다. ASP.NET Core의 URL 재작성 미들웨어는 두 가지 모두에 대한 요구를 만족합니다. 

*URL 리디렉션*은 클라이언트 측 작업으로, 클라이언트는 다른 주소를 통해서 리소스에 접근하도록 지시받게 됩니다. 이 방식은 서버를 한 번 더 왕복해야만 합니다. 클라이언트로 반환된 리디렉션 URL은 클라이언트가 리소스에 대한 새로운 요청을 만들 때 브라우저의 주소 표시줄에 나타나게 됩니다. 

`/resource`가 `/different-resource`로 리디렉션 된다고 가정하면, 먼저 클라이언트가 `/resource`를 요청합니다. 그러면 서버는 리디렉션이 임시 또는 영구적임을 나타내는 상태 코드와 함께 해당 리소스를 `/different-resource`에서 가져가야 한다고 클라이언트에게 응답합니다. 마지막으로 클라이언트는 리디렉션 URL로 리소스에 대한 새로운 요청을 실행합니다. 

![WebAPI 서비스 끝점은 서버 측에서 버전 1(v1)에서 버전 2(v2)로 임시 변경됩니다. 클라이언트는 버전 1의 경로 /v1/api로 서비스를 요청합니다. 서버는 다시 버전 2의 /v2/api라는 서비스의 임시 경로로 302 (임시 이동) 응답을 보냅니다. 클라이언트는 리디렉션 URL로 서비스에 대한 두 번째 요청을 만듭니다. 서버는 200 (정상) 상태 코드를 응답합니다.](url-rewriting/_static/url_redirect.png)

요청을 다른 URL로 리디렉션 할 때 서버는 리디렉션이 영구적인지 또는 임시적인지 여부를 지정할 수 있습니다. 301 (영구 이동) 상태 코드는 클라이언트에게 리소스에 새로운 영구적인 URL이 존재하며 앞으로 이 리소스에 대한 모든 요청은 새로운 URL을 사용해야 한다고 지시하고자 하는 경우에 사용됩니다. *이렇게 301 상태 코드가 수신되면 클라이언트는 응답을 캐시 할 수 있습니다.* 반면 302 (임시 이동) 상태 코드는 리디렉션이 임시적이거나 일반적으로 변경될 수 있는 경우에 사용되므로, 클라이언트는 리디렉션 URL을 저장했다가 나중에 다시 사용하거나 해서는 안됩니다. 보다 자세한 정보는 [RFC 2616: 상태 코드 정의](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)를 참고하시기 바랍니다.

*URL 재작성*은 요청받은 리소스를 다른 리소스 주소에서 제공하는 서버 측 작업입니다. URL 재작성 방식은 서버를 한 번 더 왕복할 필요가 없습니다. 재작성된 URL은 클라이언트로 반환되지 않고 브라우저의 주소 표시줄에 나타나지도 않습니다. `/resource`가 `/different-resource`로 *재작성* 된다고 가정할 때, 클라이언트는 `/resource`를 요청하지만 서버는 *내부적으로* `/different-resource`에서 리소스를 가져옵니다. 클라이언트는 재작성된 URL에서 리소스를 조회할 수는 있지만, 해당 요청을 만들고 응답을 받을 때 실재로는 리소스가 재작성된 URL에 존재한다는 정보는 알 수 없습니다. 

![WebAPI 서비스 끝점은 서버 측에서 버전 1(v1)에서 버전 2(v2)로 변경됩니다. 클라이언트는 버전 1의 경로 /v1/api로 서비스를 요청합니다. 요청 URL은 버전 2의 경로 /v2/api에서 서비스에 접근하도록 재작성됩니다. 서비스는 200 (정상) 상태 코드를 클라이언트에 응답합니다.](url-rewriting/_static/url_rewrite.png)

## <a name="url-rewriting-sample-app"></a>URL 재작성 예제 응용 프로그램
[URL 재작성 예제 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/)은 URL 재작성 미들웨어의 기능을 보여줍니다. 예제 응용 프로그램은 재작성 및 리디렉션 규칙을 적용하고 재작성 또는 리디렉션된 URL을 보여줍니다. 

## <a name="when-to-use-url-rewriting-middleware"></a>URL 재작성 미들웨어를 사용해야 하는 경우
Windows Server에서 IIS의 [URL 재작성 모듈](https://www.iis.net/downloads/microsoft/url-rewrite)을 사용할 수 없거나, Apache Server에서 [Apache mod_rewrite 모듈](https://httpd.apache.org/docs/2.4/rewrite/)을 사용할 수 없거나, [Nginx에서 URL 재작성](https://www.nginx.com/blog/creating-nginx-rewrite-rules/)을 사용할 수 없거나, 또는 응용 프로그램이 [HTTP.sys 서버](xref:fundamentals/servers/httpsys)(기존의 [WebListener](xref:fundamentals/servers/weblistener))에서 호스팅 되는 경우에 URL 재작성 미들웨어를 사용해야 합니다. IIS, Apache 또는 Nginx에서 서버 기반의 URL 재작성 기술을 사용하는 가장 큰 이유는 미들웨어가 이런 모듈들의 모든 기능을 지원하지 않고 대부분 미들웨어의 성능이 모듈의 성능을 따라가지 못하기 때문입니다. 그러나 IIS 재작성 모듈의 `IsFile` 및 `IsDirectory` 제약 조건 같이 ASP.NET Core 프로젝트에서 동작하지 않는 일부 서버 모듈 기능도 존재합니다. 바로 이런 시나리오에서 대신 미들웨어를 사용합니다. 

## <a name="package"></a>패키지
프로젝트에 URL 재작성 미들웨어를 추가하려면 [`Microsoft.AspNetCore.Rewrite`](https://www.nuget.org/packages/Microsoft.AspNetCore.Rewrite/) 패키지를 참조해야 합니다. 미들웨어의 기능은 ASP.NET Core 1.1 이상을 대상으로 하는 응용 프로그램에서 사용할 수 있습니다. 

## <a name="extension-and-options"></a>확장 및 옵션
URL 재작성 및 리디렉션 규칙은 각 규칙에 대한 확장 메서드를 이용해서 `RewriteOptions` 클래스의 인스턴스를 생성하는 방식으로 설정합니다. 처리하고자 하는 순서대로 여러 규칙을 연결하면 됩니다. 그리고 `RewriteOptions`는 URL 재작성 미들웨어가 `app.UseRewriter(options);`으로 요청 파이프라인에 추가될 때 URL 재작성 미들웨어에 전달됩니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1)]

---

### <a name="url-redirect"></a>URL 리디렉션
요청을 리디렉션하려면 `AddRedirect`를 사용합니다. 첫 번째 매개 변수에는 들어오는 URL의 경로와 일치하는 부분을 찾기 위한 정규식을 지정합니다. 두 번째 매개 변수는 대체 문자열입니다. 필요한 경우 세 번째 매개 변수로 상태 코드를 지정할 수 있습니다. 상태 코드를 지정하지 않으면 기본값으로 리소스가 임시로 이동하거나 대체되었음을 의미하는 302 (임시 이동) 상태 코드가 지정됩니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=5)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=2)]

---

개발자 도구가 활성화된 브라우저에서 예제 응용 프로그램에 `/redirect-rule/1234/5678` 경로를 요청합니다. 그러면 정규식이 `redirect-rule/(.*)`의 요청 경로와 일치하므로 `/redirected/1234/5678`로 경로가 치환됩니다. 이 리디렉션 URL은 302 (임시 이동) 상태 코드와 함께 클라이언트로 재전송됩니다. 브라우저는 리디렉션 URL에 대한 새로운 요청을 만들고 이 주소는 브라우저의 주소 표시줄에 출력됩니다. 리디렉션 URL과 일치하는 예제 응용 프로그램의 규칙은 존재하지 않기 때문에 두 번째 요청은 응용 프로그램에서 200 (정상) 응답을 수신하고 응답 본문은 리디렉션 URL을 보여줍니다. URL이 *리디렉션* 될 때 서버에 대한 왕복이 수행됩니다.

> [!WARNING]
> 리디렉션 규칙을 설정할 때 주의하시기 바랍니다. 리디렉션 규칙은 리디렉션 된 후를 비롯해서 응용 프로그램에 대한 각각의 요청을 대상으로 평가됩니다. 따라서 실수로 무한히 리디렉션 되는 루프를 만들기 쉽습니다. 

원본 요청: `/redirect-rule/1234/5678`

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect.png)

표현식에서 괄호로 둘러쌓인 부분을 *캡처 그룹(Capture Group)*이라고 합니다. 그리고 표현식에서 마침표(`.`)는 모든 문자와 일치함을 뜻합니다. 마지막으로 별표(`*`)는 앞의 문자와 0번 이상 일치함을 나타냅니다. 따라서 URL의 마지막 두 세그먼트, `1234/5678`은 캡쳐 그룹 `(.*)`에 의해 캡쳐됩니다. 즉 요청 URL에서 `redirect-rule/` 이후에 제공하는 모든 값이 이 단일 캡처 그룹에 의해서 캡처됩니다. 

대체 문자열에서, 캡처된 그룹은 캡처의 일련 번호가 뒤에 붙는 달러 기호(`$`)를 통해서 문자열에 삽입됩니다. 첫 번째 캡처 그룹 값은 `$1`으로 얻을 수 있고, 두 번째 캡처 그룹 값은 `$2`으로 얻을 수 있으며, 이는 정규식에 포함된 캡처 그룹에 대해 순차적으로 계속됩니다. 예제 응용 프로그램에서 리디렉션 규칙의 정규식에 캡처된 그룹은 단 하나뿐이므로 대체 문자열에 삽입되는 그룹도 `$1` 하나뿐입니다. 규칙이 적용되고 나면 URL은 `/redirected/1234/5678`로 변환됩니다.

<a name="url-redirect-to-secure-endpoint"></a>
### <a name="url-redirect-to-a-secure-endpoint"></a>보안 끝점에 대한 URL 리디렉션
`AddRedirectToHttps`를 사용하면 HTTP 요청을 HTTPS(`https://`)를 사용하는 동일한 호스트 및 경로로 리디렉션 할 수 있습니다. 상태 코드를 지정하지 않으면 미들웨어가 기본값인 302(임시 이동)을 설정합니다. 그리고 포트를 지정하지 않으면 미들웨어가 기본값인 `null`을 설정하는데, 이는 프로토콜이 `https://`로 변경되고 클라이언트가 포트 443을 통해서 리소스에 접근함을 뜻합니다. 예제에서는 상태 코드를 301(영구 이동)로 설정하고 포트를 5001로 변경하는 방법을 보여줍니다.

```csharp
var options = new RewriteOptions()
    .AddRedirectToHttps(301, 5001);

app.UseRewriter(options);
```

`AddRedirectToHttpsPermanent`를 사용하면 안전하지 않은 요청을 HTTPS 프로토콜을 사용하는 (포트 443에서 `https://`를 사용하는) 동일한 호스트 및 경로로 리디렉션 할 수 있습니다. 미들웨어는 상태 코드를 301(영구 이동)로 설정합니다.

예제 응용 프로그램을 통해서 `AddRedirectToHttps` 또는 `AddRedirectToHttpsPermanent`의 사용 방법을 확인해 볼 수 있습니다. 먼저 `RewriteOptions`에 이 확장 메서드를 추가합니다. 그리고 응용 프로그램에 대해 아무 경로로나 안전하지 않은 요청을 만듭니다. 자체 서명된 인증서를 신뢰할 수 없다는 브라우저 보안 경고는 무시하면 됩니다.

`AddRedirectToHttps(301, 5001)`에 대한 원본 요청: `/secure`

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_to_https.png)

`AddRedirectToHttpsPermanent`에 대한 원본 요청: `/secure`

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_to_https_permanent.png)

### <a name="url-rewrite"></a>URL 재작성
URL을 재작성하는 규칙을 만들려면 `AddRewrite`를 사용합니다. 첫 번째 매개 변수에는 들어오는 URL의 경로와 일치하는 부분을 찾기 위한 정규식을 지정합니다. 두 번째 매개 변수는 대체 문자열입니다. 세 번째 매개 변수, `skipRemainingRules: {true|false}`는 현재 규칙이 적용된 경우 이후의 추가적인 재작성 규칙을 무시할지 여부를 미들웨어에게 지시합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=6)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=3)]

---

원본 요청: `/rewrite-rule/1234/5678`

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_rewrite.png)

이 정규식에서 가장 먼저 주목해야 할 부분은 식의 가장 첫 문자로 위치한 캐럿(`^`)입니다. 이는 URL 경로의 시작 부분에서부터 일치가 시작된다는 것을 의미합니다. 

`redirect-rule/(.*)` 리디렉션 규칙에 대한 이전 예제에서는 정규식 시작 부분에 캐럿이 없기 때문에, 경로의 `redirect-rule/` 앞 부분에 어떤 문자가 나타나더라도 정상적으로 일치합니다.

| Path                               | 일치 |
| ---------------------------------- | :---: |
| `/redirect-rule/1234/5678`         | 예   |
| `/my-cool-redirect-rule/1234/5678` | 예   |
| `/anotherredirect-rule/1234/5678`  | 예   |

반면 `^rewrite-rule/(\d+)/(\d+)` 재작성 규칙의 경우에는 오로지 `rewrite-rule/`로 시작하는 경로만 일치합니다. 위의 리디렉션 규칙과 다음 재작성 규칙 간의 일치 여부의 차이를 비교해보시기 바랍니다.

| Path                              | 일치 |
| --------------------------------- | :---: |
| `/rewrite-rule/1234/5678`         | 예   |
| `/my-cool-rewrite-rule/1234/5678` | 아니요    |
| `/anotherrewrite-rule/1234/5678`  | 아니요    |

표현식의 `^rewrite-rule/` 부분 뒤에는 계속해서 두 개의 캡처 그룹, `(\d+)/(\d+)`이 위치해 있습니다. 여기서 `\d`는 *숫자 하나와 일치*함을 뜻합니다. 그리고 더하기 기호(`+`)는 *앞의 문자와 한 번 이상 일치*함을 나타냅니다. 따라서 URL은 반드시 숫자 쉬에 슬래시와 다른 숫자가 연이어 나타나는 부분을 포함해야 합니다. 이 캡쳐 그룹들은 `$1` 및 `$2`를 통해서 재작성 URL에 삽입됩니다. 이 재작성 규칙의 대체 문자열은 캡처된 그룹을 쿼리 문자열에 배치합니다. 즉, 요청 경로 `/rewrite-rule/1234/5678`은 `/rewritten?var1=1234&var2=5678`에서 리소스를 가져오도록 재작성됩니다. 원본 요청에 쿼리 문자열이 존재할 경우 URL이 재작성될 때 보존됩니다.

이때 리소스를 가져오기 위해서 서버를 왕복하지 않습니다. 리소스가 존재할 경우 가져온 다음 200 (정상) 상태 코드와 함께 클라이언트에 반환됩니다. 클라이언트는 리디렉션 되지 않기 때문에 브라우저 주소 표시줄의 URL은 변경되지 않습니다. 클라이언트와 관련된 URL 재작성 작업은 전혀 발생하지 않습니다.

> [!NOTE]
> 일치 규칙은 비용이 많이 드는 작업이며 응용 프로그램의 응답 속도를 늦추므로 가능하면 `항상 skipRemainingRules: true`를 사용하는 것이 좋습니다. 최대한 빠른 응용 프로그램 응답을 위해서는:
> * 가장 자주 일치하는 규칙부터 가장 적게 일치하는 규칙 순으로 재작성 규칙을 정렬합니다.
> * 일치가 발생하고 추가적인 규칙 처리가 필요하지 않다면 나머지 규칙의 처리를 생략합니다.

### <a name="apache-modrewrite"></a>Apache mod_rewrite
`AddApacheModRewrite`를 사용하면 Apache mod_rewrite 규칙을 적용할 수 있습니다. 규칙 파일이 응용 프로그램과 함께 배포되고 있는지 확인하시기 바랍니다. mod_rewrite 규칙에 대한 보다 자세한 내용과 예제는 [Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/)를 참고하시기 바랍니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

예제 코드에서 `StreamReader`는 *ApacheModRewrite.txt* 규칙 파일에서 규칙을 읽기 위해 사용됩니다. 

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=1,7)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

첫 번째 매개 변수에는 [종속성 주입](dependency-injection.md)을 통해서 제공되는 `IFileProvider`가 사용됩니다. `IHostingEnvironment`는 `ContentRootFileProvider`를 제공하기 위해서 삽입됩니다. 두 번째 매개 변수는 규칙 파일, 즉 예제 응용 프로그램의 경우 *ApacheModRewrite.txt*에 대한 경로입니다.

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=4)]

---

예제 응용 프로그램은 `/apache-mod-rules-redirect/(.\*)`에서 `/redirected?id=$1`로 요청을 리디렉션합니다. 그리고 응답 상태 코드는 302 (임시 이동) 입니다.

[!code[Main](url-rewriting/samples/2.x/ApacheModRewrite.txt)]

원본 요청: `/apache-mod-rules-redirect/1234`

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_apache_mod_redirect.png)

##### <a name="supported-server-variables"></a>지원되는 서버 변수
미들웨어는 다음과 같은 Apache mod_rewrite 서버 변수를 지원합니다:
* CONN_REMOTE_ADDR
* HTTP_ACCEPT
* HTTP_CONNECTION
* HTTP_COOKIE
* HTTP_FORWARDED
* HTTP_HOST
* HTTP_REFERER
* HTTP_USER_AGENT
* HTTPS
* IPV6
* QUERY_STRING
* REMOTE_ADDR
* REMOTE_PORT
* REQUEST_FILENAME
* REQUEST_METHOD
* REQUEST_SCHEME
* REQUEST_URI
* SCRIPT_FILENAME
* SERVER_ADDR
* SERVER_PORT
* SERVER_PROTOCOL
* TIME
* TIME_DAY
* TIME_HOUR
* TIME_MIN
* TIME_MON
* TIME_SEC
* TIME_WDAY
* TIME_YEAR

### <a name="iis-url-rewrite-module-rules"></a>IIS URL 재작성 모듈 규칙
`AddIISUrlRewrite`를 사용하면 IIS URL 재작성 모듈에 적용되는 규칙을 사용할 수 있습니다. 규칙 파일이 응용 프로그램과 함께 배포되고 있는지 확인하시기 바랍니다. 응용 프로그램을 Windows Server의 IIS에서 실행하고 있다면 미들웨어가 *web.config* 파일을 사용하도록 지정하지 마십시오. IIS를 사용할 경우, IIS 재작성 모듈과 충돌을 피할 수 있도록 규칙을 *web.config* 외부에 저장해야 합니다. IIS URL 재작성 모듈 규칙에 대한 보다 자세한 내용 및 예제는 [Url 재작성 모듈 2.0 사용](https://docs.microsoft.com/iis/extensions/url-rewrite-module/using-url-rewrite-module-20)과 [URL 재작성 모듈 구성 참조](https://docs.microsoft.com/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference)를 참고하시기 바랍니다. 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

예제 코드에서 `StreamReader`는 *IISUrlRewrite.xml* 규칙 파일에서 규칙을 읽기 위해 사용됩니다.

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=2,8)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

첫 번째 매개 변수는 `IFileProvider`를 전달받는 반면, 두 번째 매개 변수는 XML 규칙 파일, 즉 예제 응용 프로그램의 경우 *IISUrlRewrite.xml*에 대한 경로입니다. 

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=5)]

---

예제 응용 프로그램은 `/iis-rules-rewrite/(.*)`에서 `/rewritten?id=$1`로 요청을 재작성합니다. 그리고 응답은 200 (정상) 상태 코드로 클라이언트에 전송됩니다. 

[!code-xml[Main](url-rewriting/samples/2.x/IISUrlRewrite.xml)]

원본 요청: `/iis-rules-rewrite/1234`

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_iis_url_rewrite.png)

원하지 않는 방식으로 응용 프로그램에 영향을 주는 서버 수준 규칙이 구성된 활성 IIS 재작성 모듈이 존재할 경우 응용 프로그램에 대한 IIS 재작성 모듈을 비활성화 할 수 있습니다. 보다 자세한 내용은 [IIS 모듈 비활성화](xref:host-and-deploy/iis/modules#disabling-iis-modules)를 참고하시기 바랍니다.

#### <a name="unsupported-features"></a>지원되지 않는 기능

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

ASP.NET Core 2.x와 함께 출시된 미들웨어는 다음과 같은 IIS URL 재작성 모듈 기능을 지원하지 않습니다: 
* 아웃바운드 규칙
* 사용자 지정 서버 변수
* 와일드카드
* LogRewrittenUrl

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

ASP.NET Core 1.x와 함께 출시된 미들웨어는 다음과 같은 IIS URL 재작성 모듈 기능을 지원하지 않습니다: 
* 전역 규칙
* 아웃바운드 규칙
* 재작성 맵
* CustomResponse 작업
* 사용자 지정 서버 변수
* 와일드카드
* Action:CustomResponse
* LogRewrittenUrl

---

#### <a name="supported-server-variables"></a>지원되는 서버 변수
미들웨어는 다음과 같은 IIS URL 재작성 모듈 서버 변수를 지원합니다: 
* CONTENT_LENGTH
* CONTENT_TYPE
* HTTP_ACCEPT
* HTTP_CONNECTION
* HTTP_COOKIE
* HTTP_HOST
* HTTP_REFERER
* HTTP_URL
* HTTP_USER_AGENT
* HTTPS
* LOCAL_ADDR
* QUERY_STRING
* REMOTE_ADDR
* REMOTE_PORT
* REQUEST_FILENAME
* REQUEST_URI

> [!NOTE]
> `PhysicalFileProvider`를 이용해서 `IFileProvider`를 가져올 수도 있습니다. 이 방식이 재작성 규칙 파일의 위치에 대해 보다 큰 유연성을 제공할 수 있습니다. 재작성 규칙 파일이 서버의 지정한 경로에 배포되는지 확인하시기 바랍니다.
> ```csharp
> PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
> ```

### <a name="method-based-rule"></a>메서드 기반 규칙
메서드를 이용해서 직접 규칙 로직을 구현하고 싶다면 `Add(Action<RewriteContext> applyRule)`을 사용하면 됩니다. `RewriteContext`는 메서드에서 사용할 수 있는 `HttpContext`를 노출합니다. `context.Result`는 추가적인 파이프라인 처리가 수행되는 방법을 결정합니다. 

| context.Result                       | 작업                                                          |
| ------------------------------------ | --------------------------------------------------------------- |
| `RuleResult.ContinueRules`(기본값) | 계속 규칙을 적용합니다.                                         |
| `RuleResult.EndResponse`             | 규칙 적용을 중지하고 응답을 전송합니다.                       |
| `RuleResult.SkipRemainingRules`      | 규칙 적용을 중지하고 다음 미들웨어에 컨텍스트 전달합니다. |

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=9)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=6)]

---

예제 응용 프로그램은 *.xml*로 끝나는 경로 요청을 리디렉션 하는 메서드를 보여줍니다. 가령 `/file.xml`을 요청할 경우 `/xmlfiles/file.xml`로 리디렉션됩니다. 상태 코드는 301 (영구 이동)으로 설정하고 있습니다. 리디렉션의 경우 명시적으로 응답의 상태 코드를 설정해야 하며, 그렇지 않으면 200 (정상) 상태 코드가 반환되고 클라이언트에서 리디렉션이 발생하지 않습니다. 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/RewriteRules.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet2)]

---

원본 요청: `/file.xml`

![file.xml에 대한 요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_xml_requests.png)

### <a name="irule-based-rule"></a>IRule 기반 규칙
`Add(IRule)`을 사용하면 `IRule`을 구현하는 클래스로 직접 규칙 로직을 구현할 수 있습니다. `IRule`을 사용하면 메서드 기반 규칙 방식을 사용하는 것보다 더 많은 유연성을 얻을 수 있습니다. 파생된 클래스는 `ApplyRule` 메서드에서 사용할 매개 변수를 전달할 수 있는 생성자를 포함할 수 있습니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/Program.cs?name=snippet1&highlight=10-11)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/Startup.cs?name=snippet1&highlight=7-8)]

---

예제 응용 프로그램은 `extension` 및 `newPath` 매개 변수 값들이 다양한 조건을 만족하는지 검사합니다. `extension` 매개 변수는 값을 포함하고 있어야 하고, 그 값은 *.png*, *.jpg*, 또는 *.gif* 중 하나이어야 합니다. 만약 `newPath`가 유효하지 않으면 `ArgumentException`이 던져집니다. *image.png*를 요청하면 `/png-images/image.png`로 요청이 리디렉션 됩니다. 그리고 *image.jpg*를 요청하면 `/jpg-images/image.jpg`로 요청이 리디렉션 됩니다. 상태 코드는 301 (영구 이동)으로 설정하고 규칙 처리를 중지하고 응답을 전송하도록 `context.Result`를 설정합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[!code-csharp[Main](url-rewriting/samples/2.x/RewriteRules.cs?name=snippet2)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[!code-csharp[Main](url-rewriting/samples/1.x/RewriteRule.cs?name=snippet1)]

---

원본 요청: `/image.png`

![image.png에 대한 요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_png_requests.png)

원본 요청: `/image.jpg`

![image.jpg에 대한 요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_jpg_requests.png)

## <a name="regex-examples"></a>정규식 예제

| Goal | 정규식 문자열 및<br>일치 예제 | 대체 문자열 및<br>출력 예제 |
| ---- | :-----------------------------: | :------------------------------------: |
| 경로를 쿼리 문자열로 제작성 | `^path/(.*)/(.*)`<br>`/path/abc/123` | `path?var1=$1&var2=$2`<br>`/path?var1=abc&var2=123` |
| 후행 슬래시 제거 | `(.*)/$`<br>`/path/` | `$1`<br>`/path` |
| 후행 슬래시 적용 | `(.*[^/])$`<br>`/path` | `$1/`<br>`/path/` |
| 특정 요청 재작성 방지 | `^(.*)(?<!\.axd)$` 또는 `^(?!.*\.axd$)(.*)$`<br>예: `/resource.htm`<br>아니요: `/resource.axd` | `rewritten/$1`<br>`/rewritten/resource.htm`<br>`/resource.axd` |
| URL 세그먼트 재정렬 | `path/(.*)/(.*)/(.*)`<br>`path/1/2/3` | `path/$3/$2/$1`<br>`path/3/2/1` |
| URL 세그먼트 대체 | `^(.*)/segment2/(.*)`<br>`/segment1/segment2/segment3` | `$1/replaced/$2`<br>`/segment1/replaced/segment3` |

## <a name="additional-resources"></a>추가 리소스
* [응용 프로그램 시작](startup.md)
* [미들웨어](xref:fundamentals/middleware/index)
* [.NET에서의 정규식](/dotnet/articles/standard/base-types/regular-expressions)
* [정규식 언어 - 빠른 참조](/dotnet/articles/standard/base-types/quick-ref)
* [Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/)
* [Url 재작성 모듈 2.0 사용(IIS용)](https://docs.microsoft.com/iis/extensions/url-rewrite-module/using-url-rewrite-module-20)
* [URL 재작성 모듈 구성 참조](https://docs.microsoft.com/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference)
* [IIS URL 재작성 모듈 포럼](https://forums.iis.net/1152.aspx)
* [간단한 URL 구조 유지](https://support.google.com/webmasters/answer/76329?hl=en)
* [10가지 URL 재작성 팁과 요령](http://ruslany.net/2009/04/10-url-rewriting-tips-and-tricks/)
* [슬래시 여부](https://webmasters.googleblog.com/2010/04/to-slash-or-not-to-slash.html)
