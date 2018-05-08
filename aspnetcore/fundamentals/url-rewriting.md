---
title: ASP.NET Core에서 URL 재작성 미들웨어
author: guardrex
description: ASP.NET Core 응용 프로그램에서 URL 재작성 미들웨어로 URL 재작성 및 리디렉션에 대해 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 08/17/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/url-rewriting
ms.openlocfilehash: b6465aa7b56450f43be64da19f2e2228a5d68f50
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="url-rewriting-middleware-in-aspnet-core"></a>ASP.NET Core에서 URL 재작성 미들웨어

작성자: [Luke Latham](https://github.com/guardrex) 및 [Mikael Mengistu](https://github.com/mikaelm12)

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

URL 재작성은 하나 이상의 미리 정의된 규칙을 기반으로 하는 요청 URL을 수정하는 작업입니다. URL 재작성은 위치 및 주소가 밀접하게 연결되지 않도록 리소스 위치와 해당 주소 간의 추상화를 만듭니다. URL 재작성이 중요한 몇 가지 시나리오가 있습니다.
* 이러한 리소스에 대한 안정적인 로케이터를 유지 관리하는 동안 서버 리소스를 일시적 또는 영구적으로 이동 또는 대체
* 서로 다른 앱 또는 하나의 앱 영역에서 처리 중인 요청 분리
* 들어오는 요청에서 URL 세그먼트 제거, 추가 또는 다시 구성
* SEO(검색 엔진 최적화)에 대한 공용 URL 최적화
* 사용자가 링크를 따라 찾는 콘텐츠를 예측하는 데 도움이 되도록 친숙한 공용 URL의 사용을 허용
* 엔드포인트를 보호하도록 안전하지 않은 요청 리디렉션
* 이미지 핫링크 방지

정규식, Apache mod_rewrite 모듈 규칙, IIS 다시 쓰기 모듈 규칙 및 사용자 지정 규칙 논리를 사용하는 등의 여러 가지 방법으로 URL 변경을 위한 규칙을 정의할 수 있습니다. 이 문서는 ASP.NET Core 앱에서 URL 재작성 미들웨어를 사용하는 방법에 대한 지침이 포함된 URL 재작성을 소개합니다.

> [!NOTE]
> URL 재작성은 앱의 성능을 저하시킬 수 있습니다. 가능한 경우 규칙의 수와 복잡성을 제한해야 합니다.

## <a name="url-redirect-and-url-rewrite"></a>URL 리디렉션 및 URL 재작성
*URL 리디렉션* 및 *URL 재작성* 간 단어의 차이점은 처음에는 미묘해 보일 수 있지만 클라이언트에 리소스를 제공하는 데 중요한 의미가 있습니다. ASP.NET Core의 URL 재작성 미들웨어는 모두에 대한 필요성을 충족할 수 있습니다.

*URL 리디렉션*은 클라이언트 쪽 작업으로, 클라이언트는 다른 주소에서 리소스에 액세스하도록 지시됩니다. 서버에 대한 왕복 작업이 필요합니다. 클라이언트로 반환된 리디렉션 URL은 클라이언트가 리소스에 대한 새 요청을 만들 때 브라우저의 주소 표시줄에 나타납니다. 

`/resource`가 `/different-resource`로 *리디렉션*된 경우 클라이언트는 `/resource`를 요청합니다. 서버는 클라이언트가 리디렉션이 임시 또는 영구임을 나타내는 상태 코드와 함께 `/different-resource`에서 리소스를 가져와야 한다고 응답합니다. 클라이언트는 리디렉션 URL에서 리소스에 대한 새 요청을 실행합니다.

![WebAPI 서비스 엔드포인트는 서버에서 버전 1(v1)에서 버전 2(v2)로 임시적으로 변경되었습니다. 클라이언트는 버전 1 경로/v1/api에서 서비스에 대한 요청을 만듭니다. 서버는 버전 2/v2/api에서 서비스에 대한 새, 임시 경로로 302(있음) 응답을 보냅니다. 클라이언트는 리디렉션 URL에서 서비스에 대한 두 번째 요청을 만듭니다. 서버는 200(정상) 상태 코드로 응답합니다.](url-rewriting/_static/url_redirect.png)

요청을 다른 URL로 리디렉션하는 경우 리디렉션이 영구 또는 임시인지 여부를 나타냅니다. 301(영구적 이동) 상태 코드는 리소스에 새, 영구 URL이 있고 리소스에 대한 모든 향후 요청이 새 URL을 사용해야 함을 클라이언트에게 지시하려는 경우에 사용됩니다. *클라이언트는 301 상태 코드를 받을 때 응답을 캐시할 수 있습니다.* 302(있음) 상태 코드는 리디렉션이 임시이거나 일반적으로 변경될 수 있는 경우에 사용됩니다. 클라이언트는 향후에 리디렉션 URL을 저장 및 다시 사용하면 안 됩니다. 자세한 내용은 [RFC 2616: 상태 코드 정의](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)를 참조하세요.

*URL 재작성*은 다른 리소스 주소에서 리소스를 제공하는 서버 쪽 작업입니다. URL 재작성은 서버에 대한 왕복 작업이 필요하지 않습니다. 재작성된 URL은 클라이언트에 반환되지 않으며 브라우저의 주소 표시줄에 표시되지 않습니다. `/resource`가 `/different-resource`로 *재작성*되는 경우 클라이언트는 `/resource`를 요청하고, 서버는 *내부적으로* `/different-resource`에서 리소스를 페치합니다. 클라이언트는 재작성된 URL에서 리소스를 검색할 수 있지만 클라이언트는 해당 요청을 만들고 응답을 받을 때 리소스가 재작성된 URL에 있다는 것을 알림 받지 않습니다.

![WebAPI 서비스 엔드포인트는 서버에서 버전 1(v1)에서 버전 2(v2)로 변경되었습니다. 클라이언트는 버전 1 경로/v1/api에서 서비스에 대한 요청을 만듭니다. 요청 URL은 버전 2 경로/v2/api에서 서비스에 액세스하도록 재작성됩니다. 서비스는 200(정상) 상태 코드로 클라이언트에 응답합니다.](url-rewriting/_static/url_rewrite.png)

## <a name="url-rewriting-sample-app"></a>URL 재작성 샘플 앱
[URL 재작성 샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/sample/)을 사용하여 URL 재작성 미들웨어의 기능을 탐색할 수 있습니다. 앱은 재작성 및 리디렉션 규칙을 적용하고 재작성 또는 리디렉션된 URL을 보여 줍니다.

## <a name="when-to-use-url-rewriting-middleware"></a>URL 재작성 미들웨어를 사용하는 경우
Windows Server에서 IIS, Apache Server에서 [Apache mod_rewrite 모듈](https://httpd.apache.org/docs/2.4/rewrite/), [Nginx에서 URL 재작성](https://www.nginx.com/blog/creating-nginx-rewrite-rules/)으로 [URL 재작성 모듈](https://www.iis.net/downloads/microsoft/url-rewrite)을 사용할 수 없거나 앱이 [HTTP.sys 서버](xref:fundamentals/servers/httpsys)(이전에 [WebListener](xref:fundamentals/servers/weblistener)라고 함)에서 호스팅되는 경우 URL 재작성 미들웨어를 사용합니다. IIS, Apache 또는 Nginx에서 서버 기반 URL 재작성 기술을 사용하는 주된 이유는 미들웨어가 이러한 모듈의 전체 기능을 지원하지 않고 미들웨어의 성능이 아마도 모듈의 성능과 일치하지 않기 때문입니다. 그러나 IIS 재작성 모듈의 `IsFile` 및 `IsDirectory` 제약 조건과 같은 ASP.NET Core 프로젝트를 사용하지 않는 서버 모듈의 일부 기능이 있습니다. 이러한 시나리오에서 미들웨어를 대신 사용합니다.

## <a name="package"></a>패키지
미들웨어를 프로젝트에 포함하려면 [`Microsoft.AspNetCore.Rewrite`](https://www.nuget.org/packages/Microsoft.AspNetCore.Rewrite/) 패키지에 참조를 추가합니다. 이 기능은 ASP.NET Core 1.1 이상을 대상으로 하는 앱에 사용할 수 있습니다.

## <a name="extension-and-options"></a>확장 및 옵션
각 규칙에 대한 확장 메서드로 `RewriteOptions` 클래스의 인스턴스를 만들어 URL 재작성을 설정하고 규칙을 리디렉션합니다. 처리하려는 순서로 여러 규칙을 연결합니다. `RewriteOptions`는 `app.UseRewriter(options);`로 요청 파이프라인에 추가되므로 URL 재작성 미들웨어로 전달됩니다.

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    var options = new RewriteOptions()
        .AddRedirect("redirect-rule/(.*)", "redirected/$1")
        .AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", 
            skipRemainingRules: true)
        .AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt")
        .AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml")
        .Add(RedirectXMLRequests)
        .Add(new RedirectImageRequests(".png", "/png-images"))
        .Add(new RedirectImageRequests(".jpg", "/jpg-images"));

    app.UseRewriter(options);
}
```

* * *
### <a name="url-redirect"></a>URL 리디렉션
`AddRedirect`를 사용하여 요청을 리디렉션합니다. 첫 번째 매개 변수는 들어오는 URL의 경로에서 일치를 위해 정규식을 포함합니다. 두 번째 매개 변수는 대체 문자열입니다. 세 번째 매개 변수는 있는 경우 상태 코드를 지정합니다. 상태 코드를 지정하지 않는 경우 기본값을 리소스가 일시적으로 이동 또는 대체되었음을 나타내는 302(있음)로 지정합니다.

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=9)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRedirect("redirect-rule/(.*)", "redirected/$1");

    app.UseRewriter(options);
}
```

* * *
개발자 도구가 활성화된 브라우저에서 `/redirect-rule/1234/5678` 경로로 샘플 앱에 대한 요청을 만듭니다. 정규식은 `redirect-rule/(.*)`에서 요청 경로와 일치하고 경로는 `/redirected/1234/5678`로 바뀝니다. 리디렉션 URL은 302(있음) 상태 코드로 클라이언트에 다시 전송됩니다. 브라우저에서 브라우저의 주소 표시줄에 표시되는 리디렉션 URL에서 새 요청을 만듭니다. 샘플 앱의 규칙은 리디렉션 URL에서 일치하지 않으므로 두 번째 요청은 앱에서 200(정상) 응답을 수신하고 응답의 본문은 리디렉션 URL을 표시합니다. URL이 *리디렉션*될 때 서버에 대한 왕복 작업이 수행됩니다.

> [!WARNING]
> 리디렉션 규칙을 설정할 때 주의해야 합니다. 리디렉션 규칙은 리디렉션 후를 포함하여 앱에 대한 각 요청에서 평가됩니다. 실수로 무한 리디렉션의 루프를 생성하기 쉽습니다.

원래 요청: `/redirect-rule/1234/5678`

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect.png)

괄호 안에 포함된 식의 일부는 *캡처 그룹*이라고 합니다. 식의 점(`.`)은 *모든 문자 일치*를 의미합니다. 별표(`*`)는 *0회 이상 이전 문자와 일치*를 나타냅니다. 따라서 URL, `1234/5678`의 마지막 두 경로 세그먼트는 캡처 그룹 `(.*)`에 의해 캡처됩니다. `redirect-rule/` 후 요청 URL에서 제공하는 값은 이 단일 캡처 그룹에 의해 캡처됩니다.

대체 문자열에서 캡처된 그룹은 캡처의 시퀀스 번호가 뒤에 오는 달러 기호(`$`)를 사용하여 문자열에 삽입됩니다. 첫 번째 캡처 그룹 값은 `$1`로 획득되고, 두 번째는 `$2`로 획득되며, 정규식의 캡처 그룹에 대한 시퀀스에서 지속합니다. 샘플 앱의 리디렉션 규칙 정규식에 캡처된 그룹이 하나만 있으므로 대체 문자열에 삽입된 그룹은 하나입니다. 이는 `$1`입니다. 규칙이 적용되면 URL은 `/redirected/1234/5678`이 됩니다.

<a name="url-redirect-to-secure-endpoint"></a>
### <a name="url-redirect-to-a-secure-endpoint"></a>보안 엔드포인트에 대한 URL 리디렉션
`AddRedirectToHttps`를 사용하여 HTTP 요청을 동일한 호스트 및 HTTPS(`https://`)를 사용하는 경로에 리디렉션합니다. 상태 코드가 제공되지 않는 경우 미들웨어는 302(있음)로 기본값을 설정합니다. 포트가 제공되지 않는 경우 미들웨어는 기본값을 `null`로 설정합니다. 이는 프로토콜이 `https://`로 변경되고 클라이언트가 포트 443에서 리소스에 액세스하는 것을 의미합니다. 예제는 상태 코드를 301(영구적 이동)로 설정하고 포트를 5001로 변경하는 방법을 보여 줍니다.

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRedirectToHttps(301, 5001);

    app.UseRewriter(options);
}
```

`AddRedirectToHttpsPermanent`를 사용하여 안전하지 않은 요청을 동일한 호스트와 보안 HTTPS 프로토콜(포트 443의 `https://`)이 있는 경로로 리디렉션합니다. 미들웨어는 상태 코드를 301(영구적 이동)로 설정합니다.

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRedirectToHttpsPermanent();

    app.UseRewriter(options);
}
```

샘플 앱은 `AddRedirectToHttps` 또는 `AddRedirectToHttpsPermanent`를 사용하는 방법을 보여 줄 수 있습니다. 확장 메서드를 `RewriteOptions`에 추가합니다. 모든 URL에서 앱에 대한 안전하지 않은 요청을 만듭니다. 자체 서명된 인증서를 신뢰할 수 없다는 브라우저 보안 경고를 해제합니다.

`AddRedirectToHttps(301, 5001)`를 사용하는 원래 요청: `/secure`

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_to_https.png)

`AddRedirectToHttpsPermanent`를 사용하는 원래 요청: `/secure`

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_to_https_permanent.png)

### <a name="url-rewrite"></a>URL 재작성
`AddRewrite`를 사용하여 URL을 재작성하기 위한 규칙을 만듭니다. 첫 번째 매개 변수는 들어오는 URL 경로에서 일치를 위한 정규식을 포함합니다. 두 번째 매개 변수는 대체 문자열입니다. 세 번째 매개 변수, `skipRemainingRules: {true|false}`는 현재 규칙이 적용되는 경우에 추가 재작성 규칙을 건너뛸 것인지 여부를 미들웨어에 나타냅니다.

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=10-11)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", 
            skipRemainingRules: true);

    app.UseRewriter(options);
}
```

* * *
원래 요청: `/rewrite-rule/1234/5678`

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_rewrite.png)

정규식에서 발견한 첫 번째 사항은 식 시작 부분에 있는 캐럿(`^`)입니다. 이는 URL 경로의 시작 부분에서 일치하는 시작을 의미합니다.

리디렉션 규칙, `redirect-rule/(.*)`이 있는 앞의 예제에서 정규식의 시작 부분에 캐럿이 없으므로 모든 문자는 성공한 일치에 대한 경로에서 `redirect-rule/`을 앞설 수 있습니다.

| Path                               | 일치 |
| ---------------------------------- | :---: |
| `/redirect-rule/1234/5678`         | 예   |
| `/my-cool-redirect-rule/1234/5678` | 예   |
| `/anotherredirect-rule/1234/5678`  | 예   |

재작성 규칙, `^rewrite-rule/(\d+)/(\d+)`는 `rewrite-rule/`로 시작하는 경우에 경로와 일치합니다. 아래 재작성 규칙과 위의 리디렉션 규칙 간 일치에서 차이점을 확인합니다.

| Path                              | 일치 |
| --------------------------------- | :---: |
| `/rewrite-rule/1234/5678`         | 예   |
| `/my-cool-rewrite-rule/1234/5678` | 아니요    |
| `/anotherrewrite-rule/1234/5678`  | 아니요    |

식의 `^rewrite-rule/` 부분을 따릅니다. 두 개의 캡처 그룹, `(\d+)/(\d+)`가 있습니다. `\d`는 *숫자 일치*를 의미합니다. 더하기 기호(`+`)는 *하나 이상의 앞에 오는 문자와 일치*를 의미합니다. 따라서 URL은 슬래시와 다른 숫자가 잇따라 뒤에 오는 숫자를 포함해야 합니다. 이러한 캡처 그룹은 `$1` 및 `$2`로 재작성 URL에 삽입됩니다. 재작성 규칙 대체 문자열은 캡처된 그룹을 쿼리 문자열에 배치합니다. `/rewrite-rule/1234/5678`의 요청된 경로는 `/rewritten?var1=1234&var2=5678`에서 리소스를 가져오도록 재작성됩니다. 쿼리 문자열이 원래 요청에 있는 경우 URL이 재작성될 때 보존됩니다.

리소스를 가져오는 서버에 대한 왕복 작업이 없습니다. 리소스가 있는 경우 200(OK) 상태 코드로 클라이언트에 페치 및 반환됩니다. 클라이언트는 리디렉션되지 않기 때문에 브라우저 주소 표시줄의 URL은 변경되지 않습니다. 클라이언트가 관련되어 있는 한 URL 재작성 작업은 발생하지 않습니다.

> [!NOTE]
> 일치 규칙은 비용이 많이 드는 프로세스이며 앱 응답 시간을 단축시키므로 가능하면 항상 `skipRemainingRules: true`를 사용합니다. 가장 빠른 앱 응답의 경우:
> * 가장 자주 일치하는 규칙에서 가장 적게 일치하는 규칙으로 재작성 규칙을 정렬합니다.
> * 일치가 발생하고 추가 규칙 처리가 필요하지 않은 경우 나머지 규칙의 처리를 건너뜁니다.

### <a name="apache-modrewrite"></a>Apache mod_rewrite
`AddApacheModRewrite`를 사용하여 Apache mod_rewrite 규칙을 적용합니다. 규칙 파일이 앱으로 배포되고 있는지 확인합니다. mod_rewrite 규칙에 대한 자세한 내용 및 예제는 [Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/)를 참조하세요.

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
`StreamReader`는 *ApacheModRewrite.txt* 규칙 파일에서 규칙을 읽는 데 사용됩니다.

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=3-4,12)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
첫 번째 매개 변수는 [종속성 주입](dependency-injection.md)을 통해 제공되는 `IFileProvider`를 사용합니다. `IHostingEnvironment`는 `ContentRootFileProvider`를 제공하도록 삽입됩니다. 두 번째 매개 변수는 샘플 앱에서 *ApacheModRewrite.txt*인 규칙 파일에 대한 경로입니다.

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    var options = new RewriteOptions()
        .AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt");

    app.UseRewriter(options);
}
```

* * *
샘플 앱은 `/apache-mod-rules-redirect/(.\*)`에서 `/redirected?id=$1`로 요청을 리디렉션합니다. 응답 상태 코드는 302(있음)입니다.

[!code[](url-rewriting/sample/ApacheModRewrite.txt)]

원래 요청: `/apache-mod-rules-redirect/1234`

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_apache_mod_redirect.png)

##### <a name="supported-server-variables"></a>지원되는 서버 변수
미들웨어는 다음 Apache mod_rewrite 서버 변수를 지원합니다.
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
IIS URL 재작성 모듈에 적용되는 규칙을 사용하려면 `AddIISUrlRewrite`를 사용합니다. 규칙 파일이 앱으로 배포되고 있는지 확인합니다. Windows Server IIS에서 실행할 때 *web.config* 파일을 사용하도록 미들웨어에 지시하지 마십시오. IIS를 사용하는 경우 이러한 규칙은 IIS 재작성 모듈과 충돌을 피하도록 *web.config* 외부에 저장되어야 합니다. IIS URL 재작성 모듈 규칙에 대한 자세한 내용 및 예제는 [Url 재작성 모듈 2.0 사용](/iis/extensions/url-rewrite-module/using-url-rewrite-module-20) 및 [URL 재작성 모듈 구성 참조](/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference)를 참조하세요.

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
`StreamReader`는 *IISUrlRewrite.xml* 규칙 파일에서 규칙을 읽는 데 사용됩니다.

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=5-6,13)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
첫 번째 매개 변수는 `IFileProvider`를 사용하는 반면 두 번째 매개 변수는 XML 규칙 파일에 대한 경로입니다. 이는 샘플 앱에서 *IISUrlRewrite.xml*입니다.

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    var options = new RewriteOptions()
        .AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml");

    app.UseRewriter(options);
}
```

* * *
샘플 앱은 `/iis-rules-rewrite/(.*)`에서 `/rewritten?id=$1`로 요청을 재작성합니다. 응답은 200(정상) 상태 코드로 클라이언트에 전송됩니다.

[!code-xml[](url-rewriting/sample/IISUrlRewrite.xml)]

원래 요청: `/iis-rules-rewrite/1234`

![요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_iis_url_rewrite.png)

바람직하지 않은 방법으로 앱에 영향을 미치는 서버 수준 규칙으로 구성된 활성 IIS 재작성 모듈이 있는 경우 앱에 대해 IIS 재작성 모듈을 비활성화할 수 있습니다. 자세한 내용은 [IIS 모듈 비활성화](xref:host-and-deploy/iis/modules#disabling-iis-modules)를 참조하세요.

#### <a name="unsupported-features"></a>지원되지 않는 기능

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

ASP.NET Core 2.x로 출시된 미들웨어는 다음과 같은 IIS URL 재작성 모듈 기능을 지원하지 않습니다.
* 아웃바운드 규칙
* 사용자 지정 서버 변수
* 와일드카드
* LogRewrittenUrl

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

ASP.NET Core 1.x로 출시된 미들웨어는 다음과 같은 IIS URL 재작성 모듈 기능을 지원하지 않습니다.
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
미들웨어는 다음 IIS URL 재작성 모듈 서버 변수를 지원합니다.
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
> `PhysicalFileProvider`를 통해 `IFileProvider`를 가져올 수도 있습니다. 이 방법은 재작성 규칙 파일의 위치에 대해 더 큰 유연성을 제공할 수 있습니다. 재작성 규칙 파일이 제공한 경로에서 서버에 배포되는지 확인합니다.
> ```csharp
> PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
> ```

### <a name="method-based-rule"></a>메서드 기반 규칙
`Add(Action<RewriteContext> applyRule)`를 사용하여 메서드에서 사용자 고유의 규칙 논리를 구현합니다. `RewriteContext`는 메서드에서 사용하기 위해 `HttpContext`를 공개합니다. `context.Result`는 추가 파이프라인 처리가 처리되는 방법을 결정합니다.

| context.Result                       | 작업                                                          |
| ------------------------------------ | --------------------------------------------------------------- |
| `RuleResult.ContinueRules`(기본값) | 계속 규칙 적용                                         |
| `RuleResult.EndResponse`             | 규칙 적용을 중지하고 응답 보내기                       |
| `RuleResult.SkipRemainingRules`      | 규칙 적용을 중지하고 다음 미들웨어에 컨텍스트 보내기 |

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=14)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .Add(RedirectXMLRequests);

    app.UseRewriter(options);
}
```

* * *
샘플 앱은 *.xml*로 끝나는 경로에 대한 요청을 리디렉션하는 메서드를 보여 줍니다. `/file.xml`에 대한 요청을 만드는 경우 `/xmlfiles/file.xml`로 리디렉션됩니다. 상태 코드는 301(영구적 이동)로 설정됩니다. 리디렉션의 경우 응답의 상태 코드를 명시적으로 설정해야 합니다. 그렇지 않으면 200(정상) 상태 코드가 반환되고 클라이언트에서 리디렉션이 발생하지 않습니다.

[!code-csharp[](url-rewriting/sample/RewriteRules.cs?name=snippet1)]

원래 요청: `/file.xml`

![file.xml에 대한 요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_xml_requests.png)

### <a name="irule-based-rule"></a>IRule 기반 규칙
`Add(IRule)`를 사용하여 `IRule`에서 파생되는 클래스에서 사용자 고유의 규칙 논리를 구현합니다. `IRule`을 사용하면 메서드 기반 규칙 방식을 사용하는 것보다 큰 유연성을 제공합니다. 파생된 클래스는 `ApplyRule` 메서드에 대한 매개 변수를 전달할 수 있는 생성자를 포함할 수 있습니다.

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=15-16)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .Add(new RedirectImageRequests(".png", "/png-images"))
        .Add(new RedirectImageRequests(".jpg", "/jpg-images"));

    app.UseRewriter(options);
}
```

* * *
여러 조건을 충족하도록 `extension` 및 `newPath`에 대한 샘플 앱의 매개 변수 값이 선택됩니다. `extension`은 값을 포함해야 하며 값은 *.png*, *.jpg* 또는 *.gif*여야 합니다. `newPath`가 유효하지 않은 경우 `ArgumentException`이 throw됩니다. *image.png*에 대한 요청을 만드는 경우 `/png-images/image.png`로 리디렉션됩니다. *image.jpg*에 대한 요청을 만드는 경우 `/jpg-images/image.jpg`로 리디렉션됩니다. 상태 코드가 301(영구적 이동)로 설정되어 있고 `context.Result`가 규칙 처리를 중지하고 응답을 보내도록 설정됩니다.

[!code-csharp[](url-rewriting/sample/RewriteRules.cs?name=snippet2)]

원래 요청: `/image.png`

![image.png에 대한 요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_png_requests.png)

원래 요청: `/image.jpg`

![image.jpg에 대한 요청 및 응답을 추적하는 개발자 도구가 있는 브라우저 창](url-rewriting/_static/add_redirect_jpg_requests.png)

## <a name="regex-examples"></a>정규식 예제

| Goal | 정규식 문자열 및<br>일치 예제 | 대체 문자열 및<br>출력 예제 |
| ---- | :-----------------------------: | :------------------------------------: |
| 쿼리 문자열로 경로 재작성 | `^path/(.*)/(.*)`<br>`/path/abc/123` | `path?var1=$1&var2=$2`<br>`/path?var1=abc&var2=123` |
| 후행 슬래시 제거 | `(.*)/$`<br>`/path/` | `$1`<br>`/path` |
| 후행 슬래시 적용 | `(.*[^/])$`<br>`/path` | `$1/`<br>`/path/` |
| 특정 요청 재작성 방지 | `^(.*)(?<!\.axd)$` 또는 `^(?!.*\.axd$)(.*)$`<br>예: `/resource.htm`<br>아니요: `/resource.axd` | `rewritten/$1`<br>`/rewritten/resource.htm`<br>`/resource.axd` |
| URL 세그먼트 다시 정렬 | `path/(.*)/(.*)/(.*)`<br>`path/1/2/3` | `path/$3/$2/$1`<br>`path/3/2/1` |
| URL 세그먼트 대체 | `^(.*)/segment2/(.*)`<br>`/segment1/segment2/segment3` | `$1/replaced/$2`<br>`/segment1/replaced/segment3` |

## <a name="additional-resources"></a>추가 자료
* [응용 프로그램 시작](startup.md)
* [미들웨어](xref:fundamentals/middleware/index)
* [.NET에서의 정규식](/dotnet/articles/standard/base-types/regular-expressions)
* [정규식 언어 - 빠른 참조](/dotnet/articles/standard/base-types/quick-ref)
* [Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/)
* [Url 재작성 모듈 2.0 사용(IIS용)](/iis/extensions/url-rewrite-module/using-url-rewrite-module-20)
* [URL 재작성 모듈 구성 참조](/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference)
* [IIS URL 재작성 모듈 포럼](https://forums.iis.net/1152.aspx)
* [간단한 URL 구조 유지](https://support.google.com/webmasters/answer/76329?hl=en)
* [10가지 URL 재작성 팁과 요령](http://ruslany.net/2009/04/10-url-rewriting-tips-and-tricks/)
* [슬래시 여부](https://webmasters.googleblog.com/2010/04/to-slash-or-not-to-slash.html)
