---
title: 프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성
author: guardrex
description: 중요한 요청 정보를 종종 숨기는 프록시 서버 및 부하 분산 장치 뒤에 호스트되는 앱의 구성에 대해 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 03/26/2018
uid: host-and-deploy/proxy-load-balancer
ms.openlocfilehash: 1797962d6eada9c48b31cd94e2c7481380301a0d
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276778"
---
# <a name="configure-aspnet-core-to-work-with-proxy-servers-and-load-balancers"></a>프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성

작성자: [Luke Latham](https://github.com/guardrex) 및 [Chris Ross](https://github.com/Tratcher)

ASP.NET Core의 권장 구성에서 앱은 IIS/ASP.NET Core 모듈, Nginx 또는 Apache를 사용하여 호스트됩니다. 프록시 서버, 부하 분산 장치 및 기타 네트워크 어플라이언스는 종종 앱에 도달하기 전에 요청에 대한 정보를 숨깁니다.

* HTTPS 요청이 HTTP를 통해 프록시된 경우 원래 스키마(HTTPS)가 손실되므로 헤더에서 전달되어야 합니다.
* 앱은 프록시에서 요청을 수신하고 인터넷 또는 회사 네트워크의 실제 소스를 수신하는 것이 아니므로 원래 클라이언트 IP 주소도 헤더에서 전달되어야 합니다.

이 정보는 요청 처리 시 중요할 수 있습니다(예: 리디렉션, 인증, 링크 생성, 정책 평가 및 클라이언트 지리적 위치).

## <a name="forwarded-headers"></a>전달된 헤더

규칙에 따라 프록시는 HTTP 헤더에서 정보를 전달합니다.

| Header | 설명 |
| ------ | ----------- |
| X-Forwarded-For | 요청 및 프록시 체인의 후속 프록시를 시작한 클라이언트에 대한 정보를 포함합니다. 이 매개 변수에는 IP 주소(및 선택적으로 포트 번호)가 포함될 수 있습니다. 프록시 서버의 체인에서 첫 번째 매개 변수는 요청이 처음 만들어진 클라이언트를 나타냅니다. 그 뒤에 후속 프록시 식별자가 추가됩니다. 체인의 마지막 프록시는 매개 변수 목록에 없습니다. 마지막 프록시의 IP 주소 및 선택적으로 포트 번호는 전송 계층에서 원격 IP 주소로 사용할 수 있습니다. |
| X-Forwarded-Proto | 원래 체계(HTTP/HTTPS)의 값입니다. 요청이 여러 프록시를 트래버스한 경우에는 값이 체계 목록일 수도 있습니다. |
| X-Forwarded-Host | 호스트 헤더 필드의 원래 값입니다. 일반적으로 프록시는 호스트 헤더를 수정하지 않습니다. 프록시가 호스트 헤더를 유효성 검사하거나 알려진 정상 값으로 제한하지 않는 시스템에 영향을 미치는 권한 상승 취약성에 대한 자세한 내용은 [Microsoft 보안 공지 CVE-2018-0787](https://github.com/aspnet/Announcements/issues/295)을 참조하세요. |

[Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 패키지의 전달된 헤더 미들웨어는 이러한 헤더를 읽고 [HttpContext](/dotnet/api/microsoft.aspnetcore.http.httpcontext)의 연결된 필드를 채웁니다.

미들웨어가 다음을 업데이트합니다.

* [HttpContext.Connection.RemoteIpAddress](/dotnet/api/microsoft.aspnetcore.http.connectioninfo.remoteipaddress) &ndash; `X-Forwarded-For` 헤더 값을 사용하여 설정합니다. 추가 설정은 미들웨어가 `RemoteIpAddress`를 설정하는 방법에 영향을 줍니다. 자세한 내용은 [전달된 헤더 미들웨어 옵션](#forwarded-headers-middleware-options)을 참조하세요.
* [HttpContext.Request.Scheme](/dotnet/api/microsoft.aspnetcore.http.httprequest.scheme) &ndash; `X-Forwarded-Proto` 헤더 값을 사용하여 설정합니다.
* [HttpContext.Request.Host](/dotnet/api/microsoft.aspnetcore.http.httprequest.host) &ndash; `X-Forwarded-Host` 헤더 값을 사용하여 설정합니다.

일부 네트워크 어플라이언스는 `X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더를 추가하려면 추가 구성이 필요합니다. 프록시된 요청이 앱에 도달할 때 이러한 헤더를 포함하지 않는 경우에는 어플라이언스 제조업체의 지침을 참조하세요.

전달된 헤더 미들웨어 [기본 설정](#forwarded-headers-middleware-options)을 구성할 수 있습니다. 기본 설정은 다음과 같습니다.

* 앱과 요청 소스 사이에는 ‘하나의 프록시’만 있습니다.
* 알려진 프록시 및 알려진 네트워크의 경우 루프백 주소만 구성됩니다.

## <a name="iisiis-express-and-aspnet-core-module"></a>IIS/IIS Express 및 ASP.NET Core 모듈

전달된 헤더 미들웨어는 앱이 IIS 및 ASP.NET Core 모듈 뒤에서 실행되는 경우 IIS 통합 미들웨어에서 기본적으로 사용하도록 설정됩니다. 전달된 헤더 미들웨어는 전달된 헤더 관련 신뢰 문제(예: [IP 스푸핑](https://www.iplocation.net/ip-spoofing))로 인해 ASP.NET Core 모듈에 특정한 제한된 구성을 사용하여 미들웨어 파이프라인에서 첫 번째로 실행될 수 있도록 활성화됩니다. 미들웨어는 `X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더를 전달하도록 구성되고 단일 localhost 프록시로 제한됩니다. 추가 구성이 필요한 경우 [전달된 헤더 미들웨어 옵션](#forwarded-headers-middleware-options)을 참조하세요.

## <a name="other-proxy-server-and-load-balancer-scenarios"></a>기타 프록시 서버 및 부하 분산 장치 시나리오

IIS 통합 미들웨어 사용 외에는 전달된 헤더 미들웨어가 기본적으로 사용되지 않습니다. 앱이 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders)를 사용하여 전달된 헤더를 처리하려면 전달된 헤더 미들웨어가 사용하도록 설정되어야 합니다. [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)가 미들웨어에 대해 지정되지 않은 경우 미들웨어를 사용하도록 설정한 후 기본 [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders)는 [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders)입니다.

`Startup.ConfigureServices`에서 `X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더를 전달하도록 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)를 사용하여 미들웨어를 구성합니다. 다른 미들웨어를 호출하기 전에 `Startup.Configure`에서 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 메서드를 호출합니다.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.Configure<ForwardedHeadersOptions>(options =>
    {
        options.ForwardedHeaders = 
            ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto;
    });
}

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseForwardedHeaders();

    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Home/Error");
    }

    app.UseStaticFiles();
    // In ASP.NET Core 1.x, replace the following line with: app.UseIdentity();
    app.UseAuthentication();
    app.UseMvc();
}
```

> [!NOTE]
> [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)가 `Startup.ConfigureServices`에서 지정되지 않거나 [UseForwardedHeaders(IApplicationBuilder, ForwardedHeadersOptions)](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ForwardedHeadersExtensions_UseForwardedHeaders_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_ForwardedHeadersOptions_)를 사용하여 확장 메서드에 대해 직접 지정되지 않은 경우 전달할 기본 헤더는 [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders)입니다. [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) 속성은 전달할 헤더를 사용하여 구성되어야 합니다.

## <a name="nginx-configuration"></a>Nginx 구성

`X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더를 전달하려면 [Nginx를 사용하여 Linux에서 호스트: Nginx 구성](xref:host-and-deploy/linux-nginx#configure-nginx)을 참조하세요. 자세한 내용은 [NGINX: 전달된 헤더 사용](https://www.nginx.com/resources/wiki/start/topics/examples/forwarded/)을 참조하세요.

## <a name="apache-configuration"></a>Apache 구성

`X-Forwarded-For`가 자동으로 추가됩니다( [Apache 모듈 mod_proxy: 역방향 프록시 요청 헤더](https://httpd.apache.org/docs/2.4/mod/mod_proxy.html#x-headers) 참조). `X-Forwarded-Proto`를 헤더 전달하는 방법에 대한 자세한 내용은 [Apache를 사용하여 Linux에서 호스트: Apache 구성](xref:host-and-deploy/linux-apache#configure-apache)을 참조하세요.

## <a name="forwarded-headers-middleware-options"></a>전달된 헤더 미들웨어 옵션

[ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)는 전달된 헤더 미들웨어의 동작을 제어합니다.

```csharp
services.Configure<ForwardedHeadersOptions>(options =>
{
    options.ForwardLimit = 2;
    options.KnownProxies.Add(IPAddress.Parse("127.0.10.1"));
    options.ForwardedForHeaderName = "X-Forwarded-For-Custom-Header-Name";
});
```

::: moniker range="<= aspnetcore-2.0"
| 옵션 | 설명 |
| ------ | ----------- |
| [ForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedforheadername) | [ForwardedHeadersDefaults.XForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedforheadername)에서 지정된 헤더 대신 이 속성에서 지정된 헤더를 사용합니다.<br><br>기본값은 `X-Forwarded-For`입니다. |
| [ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) | 처리해야 할 전달자를 알려줍니다. 적용되는 필드 목록은 [ForwardedHeaders 열거형](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders)을 참조하세요. 이 속성에 할당된 일반적인 값은 <code>ForwardedHeaders.XForwardedFor &#124; ForwardedHeaders.XForwardedProto</code>입니다.<br><br>기본값은 [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders)입니다. |
| [ForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedhostheadername) | [ForwardedHeadersDefaults.XForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedhostheadername)에서 지정된 헤더 대신 이 속성에서 지정된 헤더를 사용합니다.<br><br>기본값은 `X-Forwarded-Host`입니다. |
| [ForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedprotoheadername) | [ForwardedHeadersDefaults.XForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedprotoheadername)에서 지정된 헤더 대신 이 속성에서 지정된 헤더를 사용합니다.<br><br>기본값은 `X-Forwarded-Proto`입니다. |
| [ForwardLimit](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardlimit) | 처리되는 헤더의 항목 수를 제한합니다. 제한을 사용하지 않도록 `null`로 설정하지만, `KnownProxies` 또는 `KnownNetworks`가 구성된 경우에만 사용해야 합니다.<br><br>기본값은 1입니다. |
| [KnownNetworks](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownnetworks) | 전달된 헤더를 허용하기 위한 알려진 프록시의 주소 범위입니다. CIDR(Classless Interdomain Routing) 표기법을 사용하여 IP 범위를 제공합니다.<br><br>기본값은 `IPAddress.Loopback`에 대한 단일 항목을 포함하는 [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPNetwork](/dotnet/api/microsoft.aspnetcore.httpoverrides.ipnetwork)>입니다. |
| [KnownProxies](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownproxies) | 전달된 헤더를 허용하기 위한 알려진 프록시의 주소입니다. `KnownProxies`를 사용하여 정확한 IP 주소 일치 항목을 지정합니다.<br><br>기본값은 `IPAddress.IPv6Loopback`에 대한 단일 항목을 포함하는 [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPAddress](/dotnet/api/system.net.ipaddress)>입니다. |
| [OriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalforheadername) | [ForwardedHeadersDefaults.XOriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalforheadername)에서 지정된 헤더 대신 이 속성에서 지정된 헤더를 사용합니다.<br><br>기본값은 `X-Original-For`입니다. |
| [OriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalhostheadername) | [ForwardedHeadersDefaults.XOriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalhostheadername)에서 지정된 헤더 대신 이 속성에서 지정된 헤더를 사용합니다.<br><br>기본값은 `X-Original-Host`입니다. |
| [OriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalprotoheadername) | [ForwardedHeadersDefaults.XOriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalprotoheadername)에서 지정된 헤더 대신 이 속성에서 지정된 헤더를 사용합니다.<br><br>기본값은 `X-Original-Proto`입니다. |
| [RequireHeaderSymmetry](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.requireheadersymmetry) | 처리 중인 [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) 간에 동기화할 헤더 값 수가 필요합니다.<br><br>ASP.NET Core 1.x의 기본값은 `true`입니다. ASP.NET Core 2.0 이상의 기본값은 `false`입니다. |
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
| 옵션 | 설명 |
| ------ | ----------- |
| AllowedHosts | `X-Forwarded-Host` 헤더에 의한 호스트를 제공된 값으로 제한합니다.<ul><li>값은 ordinal-ignore-case를 사용하여 비교됩니다.</li><li>포트 번호는 제외해야 합니다.</li><li>목록이 비어 있으면 모든 호스트가 허용됩니다.</li><li>최상위 수준 와일드카드 `*`는 비어 있지 않은 모든 호스트를 허용합니다.</li><li>하위 도메인 와일드카드는 허용되지만 루트 도메인과 일치하지 않습니다. 예를 들어 `*.contoso.com`은 하위 도메인 `foo.contoso.com`과 일치하지만 루트 도메인 `contoso.com`과 일치하지 않습니다.</li><li>유니코드 호스트 이름은 허용되지만 일치시킬 [Punycode](https://tools.ietf.org/html/rfc3492)로 변환됩니다.</li><li>[IPv6 주소](https://tools.ietf.org/html/rfc4291)는 경계 대괄호를 포함하고 [기존 형식](https://tools.ietf.org/html/rfc4291#section-2.2)이어야 합니다(예: `[ABCD:EF01:2345:6789:ABCD:EF01:2345:6789]`). IPv6 주소는 서로 다른 형식 간에 논리적 같음을 확인하기 위해 특별히 처리되지 않으며 정규화가 수행되지 않습니다.</li><li>허용된 호스트를 제한하지 못하면 공격자가 서비스에서 생성된 링크를 스푸핑할 수 있습니다.</li></ul>기본값은 빈 [IList\<string>](/dotnet/api/system.collections.generic.ilist-1)입니다. |
| [ForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedforheadername) | [ForwardedHeadersDefaults.XForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedforheadername)에서 지정된 헤더 대신 이 속성에서 지정된 헤더를 사용합니다.<br><br>기본값은 `X-Forwarded-For`입니다. |
| [ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) | 처리해야 할 전달자를 알려줍니다. 적용되는 필드 목록은 [ForwardedHeaders 열거형](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders)을 참조하세요. 이 속성에 할당된 일반적인 값은 <code>ForwardedHeaders.XForwardedFor &#124; ForwardedHeaders.XForwardedProto</code>입니다.<br><br>기본값은 [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders)입니다. |
| [ForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedhostheadername) | [ForwardedHeadersDefaults.XForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedhostheadername)에서 지정된 헤더 대신 이 속성에서 지정된 헤더를 사용합니다.<br><br>기본값은 `X-Forwarded-Host`입니다. |
| [ForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedprotoheadername) | [ForwardedHeadersDefaults.XForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedprotoheadername)에서 지정된 헤더 대신 이 속성에서 지정된 헤더를 사용합니다.<br><br>기본값은 `X-Forwarded-Proto`입니다. |
| [ForwardLimit](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardlimit) | 처리되는 헤더의 항목 수를 제한합니다. 제한을 사용하지 않도록 `null`로 설정하지만, `KnownProxies` 또는 `KnownNetworks`가 구성된 경우에만 사용해야 합니다.<br><br>기본값은 1입니다. |
| [KnownNetworks](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownnetworks) | 전달된 헤더를 허용하기 위한 알려진 프록시의 주소 범위입니다. CIDR(Classless Interdomain Routing) 표기법을 사용하여 IP 범위를 제공합니다.<br><br>기본값은 `IPAddress.Loopback`에 대한 단일 항목을 포함하는 [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPNetwork](/dotnet/api/microsoft.aspnetcore.httpoverrides.ipnetwork)>입니다. |
| [KnownProxies](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownproxies) | 전달된 헤더를 허용하기 위한 알려진 프록시의 주소입니다. `KnownProxies`를 사용하여 정확한 IP 주소 일치 항목을 지정합니다.<br><br>기본값은 `IPAddress.IPv6Loopback`에 대한 단일 항목을 포함하는 [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPAddress](/dotnet/api/system.net.ipaddress)>입니다. |
| [OriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalforheadername) | [ForwardedHeadersDefaults.XOriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalforheadername)에서 지정된 헤더 대신 이 속성에서 지정된 헤더를 사용합니다.<br><br>기본값은 `X-Original-For`입니다. |
| [OriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalhostheadername) | [ForwardedHeadersDefaults.XOriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalhostheadername)에서 지정된 헤더 대신 이 속성에서 지정된 헤더를 사용합니다.<br><br>기본값은 `X-Original-Host`입니다. |
| [OriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalprotoheadername) | [ForwardedHeadersDefaults.XOriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalprotoheadername)에서 지정된 헤더 대신 이 속성에서 지정된 헤더를 사용합니다.<br><br>기본값은 `X-Original-Proto`입니다. |
| [RequireHeaderSymmetry](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.requireheadersymmetry) | 처리 중인 [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) 간에 동기화할 헤더 값 수가 필요합니다.<br><br>ASP.NET Core 1.x의 기본값은 `true`입니다. ASP.NET Core 2.0 이상의 기본값은 `false`입니다. |
::: moniker-end

## <a name="scenarios-and-use-cases"></a>시나리오 및 사용 사례

### <a name="when-it-isnt-possible-to-add-forwarded-headers-and-all-requests-are-secure"></a>전달된 헤더를 추가할 수 없고 모든 요청이 안전한 경우

일부 경우에는 앱으로 프록시된 요청에 전달된 헤더를 추가할 수 없습니다. 모든 공용 외부 요청이 HTTPS가 되도록 프록시가 적용되는 경우 미들웨어를 사용하기 전에 `Startup.Configure`에서 체계를 수동으로 설정할 수 있습니다.

```csharp
app.Use((context, next) =>
{
    context.Request.Scheme = "https";
    return next();
});
```

이 코드는 개발 또는 스테이징 환경에서 환경 변수 또는 기타 구성 설정을 통해 사용하지 않도록 설정될 수 있습니다.

### <a name="deal-with-path-base-and-proxies-that-change-the-request-path"></a>요청 경로를 변경하는 프록시 및 경로 기준을 처리합니다.

일부 프록시는 경로를 그대로 전달하지만 라우팅이 제대로 작동하도록 제거해야 하는 앱 기본 경로를 포함합니다. [UsePathBaseExtensions.UsePathBase](/dotnet/api/microsoft.aspnetcore.builder.usepathbaseextensions.usepathbase) 미들웨어는 경로를 [HttpRequest.Path](/dotnet/api/microsoft.aspnetcore.http.httprequest.path)로 분할하고 앱 기본 경로를 [HttpRequest.PathBase](/dotnet/api/microsoft.aspnetcore.http.httprequest.pathbase)로 분할합니다.

`/foo`가 `/foo/api/1`로 전달되는 프록시 경로의 앱 기본 경로인 경우 미들웨어는 다음 명령을 사용하여 `Request.PathBase`를 `/foo`로 설정하고 `Request.Path`를 `/api/1`로 설정합니다.

```csharp
app.UsePathBase("/foo");
```

미들웨어가 역방향으로 다시 호출되면 원래 경로 및 경로 기준이 다시 적용됩니다. 미들웨어 순서 처리에 대한 자세한 내용은 [미들웨어](xref:fundamentals/middleware/index)를 참조하세요.

프록시가 경로를 자르는 경우(예: `/foo/api/1`을 `/api/1`에 전달) 요청의 [PathBase](/dotnet/api/microsoft.aspnetcore.http.httprequest.pathbase) 속성을 설정하여 리디렉션 및 링크를 수정합니다.

```csharp
app.Use((context, next) =>
{
    context.Request.PathBase = new PathString("/foo");
    return next();
});
```

프록시가 경로 데이터를 추가하는 경우 경로의 파트를 무시하고 [StartsWithSegments(PathString, PathString)](/dotnet/api/microsoft.aspnetcore.http.pathstring.startswithsegments#Microsoft_AspNetCore_Http_PathString_StartsWithSegments_Microsoft_AspNetCore_Http_PathString_Microsoft_AspNetCore_Http_PathString__)를 [Path](/dotnet/api/microsoft.aspnetcore.http.httprequest.path) 속성에 할당하여 리디렉션 및 링크를 수정합니다.

```csharp
app.Use((context, next) =>
{
    if (context.Request.Path.StartsWithSegments("/foo", out var remainder))
    {
        context.Request.Path = remainder;
    }

    return next();
});
```

## <a name="troubleshoot"></a>문제 해결

헤더가 예상대로 전달되지 않으면 [로깅](xref:fundamentals/logging/index)을 사용하도록 설정합니다. 로그가 문제를 해결하기에 충분한 정보를 제공하지 않으면 서버가 수신하는 요청 헤더를 열거합니다. 인라인 미들웨어를 사용하여 앱 응답에 헤더를 기록할 수 있습니다.

```csharp
public void Configure(IApplicationBuilder app, ILoggerFactory loggerfactory)
{
    app.Run(async (context) =>
    {
        context.Response.ContentType = "text/plain";

        // Request method, scheme, and path
        await context.Response.WriteAsync(
            $"Request Method: {context.Request.Method}{Environment.NewLine}");
        await context.Response.WriteAsync(
            $"Request Scheme: {context.Request.Scheme}{Environment.NewLine}");
        await context.Response.WriteAsync(
            $"Request Path: {context.Request.Path}{Environment.NewLine}");

        // Headers
        await context.Response.WriteAsync($"Request Headers:{Environment.NewLine}");

        foreach (var header in context.Request.Headers)
        {
            await context.Response.WriteAsync($"{header.Key}: " +
                $"{header.Value}{Environment.NewLine}");
        }

        await context.Response.WriteAsync(Environment.NewLine);

        // Connection: RemoteIp
        await context.Response.WriteAsync(
            $"Request RemoteIp: {context.Connection.RemoteIpAddress}");
    }
}
```

X-Forwarded-* 헤더가 서버에서 예상한 값으로 수신되는지 확인합니다. 제공된 헤더에 여러 값이 있는 경우 전달된 헤더 미들웨어는 오른쪽에서 왼쪽으로 역순으로 헤더를 처리합니다.

요청의 원래 원격 IP는 X-Forwarded-For가 처리되기 전에 `KnownProxies` 또는 `KnownNetworks` 목록의 항목과 일치해야 합니다. 이렇게 하면 신뢰할 수 없는 프록시에서 전달자가 허용되지 않아 헤더 스푸핑이 제한됩니다.

## <a name="additional-resources"></a>추가 자료

* [Microsoft Security Advisory CVE-2018-0787: ASP.NET Core Elevation Of Privilege Vulnerability](https://github.com/aspnet/Announcements/issues/295)(Microsoft 보안 공지 CVE-2018-0787: ASP.NET Core 권한 상승 취약성)
