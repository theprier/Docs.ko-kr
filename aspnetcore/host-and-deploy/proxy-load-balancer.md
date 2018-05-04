---
title: ASP.NET Core 프록시 서버를 사용 하 고 부하 분산 장치를 구성 합니다.
author: guardrex
description: 프록시 서버 뒤에 호스트 되는 앱에 대 한 구성을 확인 하 고 부하 분산 장치, 종종 중요가 려 서 정보를 요청 합니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/26/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/proxy-load-balancer
ms.openlocfilehash: f18a5c518edc739e0fe667f3aef6ffd38c06366c
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-aspnet-core-to-work-with-proxy-servers-and-load-balancers"></a>ASP.NET Core 프록시 서버를 사용 하 고 부하 분산 장치를 구성 합니다.

여 [Luke Latham](https://github.com/guardrex) 및 [Chris Ross](https://github.com/Tratcher)

ASP.NET Core에 대 한 권장된 구성에서 iis/ASP.NET Core 모듈, Nginx, 또는 Apache를 사용 하 여 응용 프로그램 호스트 됩니다. 프록시 서버, 부하 분산 장치, 및 기타 네트워크 장치 종종를 려 서 요청에 대 한 정보는 응용 프로그램에 도달 하기 전에:

* HTTPS 요청은 HTTP를 통해 프록시를 원본 구성표 (HTTPS) 삭제 되 고 헤더에 전달 되어야 합니다.
* 응용 프로그램 프록시와 인터넷 이나 회사 네트워크에 true의 원본이 아닌에서 요청 받으면 때문에 원래 클라이언트 IP 주소 헤더에 전달 합니다.

이 정보는 예를 들어 리디렉션을, 인증, 링크 생성, 정책 평가 및 클라이언트 geoloation에 처리 요청에 중요할 수 있습니다.

## <a name="forwarded-headers"></a>전달 된 헤더

규칙에 따라 프록시는 HTTP 헤더에 대 한 정보를 전달합니다.

| Header | 설명 |
| ------ | ----------- |
| X-전달 기능에 대 한 | 요청을 후속 프록시의 체인에 시작한 클라이언트에 대 한 정보를 보유 합니다. 이 매개 변수는 IP 주소 (및 필요에 따라 포트 번호)에 포함 될 수 있습니다. 프록시 서버의 체인을 첫 번째 매개 변수는 요청이 처음으로 된 클라이언트를 나타냅니다. 후속 프록시 식별자 따라야 합니다. 체인에서 마지막 프록시 매개 변수 목록이 잘못 되었습니다. 마지막 프록시의 IP 주소 및 포트 번호를 필요에 따라 전송 계층에서의 원격 IP 주소로 나와 있습니다. |
| X-Forwarded-Proto | 원래 체계 (HTTP/HTTPS)의 값입니다. 값은 요청이 여러 프록시를 이동 하는 경우 스키마의 목록이 수도 있습니다. |
| X 전달 호스트 | 호스트 헤더 필드의 원래 값입니다. 일반적으로 프록시 호스트 헤더를 수정 하지 마십시오. 참조 [Microsoft 보안 권고 CVE-2018-0787](https://github.com/aspnet/Announcements/issues/295) 프록시 하지 않는 유효성을 검사 하는 시스템에 영향을 주는 권한 상승 취약점 또는 알려진된 좋은 값에 restict 호스트 헤더에 대 한 내용은 합니다. |

전달 헤더 미들웨어에서는 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 패키지, 이러한 헤더를 읽고,에 연결 된 필드에 입력 [HttpContext](/dotnet/api/microsoft.aspnetcore.http.httpcontext)합니다. 

미들웨어 업데이트:

* [HttpContext.Connection.RemoteIpAddress](/dotnet/api/microsoft.aspnetcore.http.connectioninfo.remoteipaddress) &ndash; 사용 하 여 설정 된 `X-Forwarded-For` 헤더 값입니다. 미들웨어가 설정 하는 방법에 영향을 줄 추가 설정을 `RemoteIpAddress`합니다. 자세한 내용은 참조는 [전달 헤더 미들웨어 옵션입니다.](#forwarded-headers-middleware-options)합니다.
* [HttpContext.Request.Scheme](/dotnet/api/microsoft.aspnetcore.http.httprequest.scheme) &ndash; 사용 하 여 설정 된 `X-Forwarded-Proto` 헤더 값입니다.
* [HttpContext.Request.Host](/dotnet/api/microsoft.aspnetcore.http.httprequest.host) &ndash; 사용 하 여 설정 된 `X-Forwarded-Host` 헤더 값입니다.

일부 네트워크 어플라이언스에 추가 참고는 `X-Forwarded-For` 및 `X-Forwarded-Proto` 추가 구성 없이 헤더입니다. 응용 프로그램에 도달 하면 프록시 요청 이러한 헤더를 포함 하지 않는 경우 기기 제조업체의 설명서를 참조 하십시오.

헤더 미들웨어 전달 [기본 설정](#forwarded-headers-middleware-options) 구성할 수 있습니다. 기본 설정은 다음과 같습니다.

* 뿐 *하나의 프록시* 응용 프로그램 사이의 요청의 소스입니다.
* 루프백 주소에만 알려진된 프록시에 대 한 구성 되 고 네트워크 알 수 있습니다.

## <a name="iisiis-express-and-aspnet-core-module"></a>IIS/IIS Express 및 ASP.NET Core 모듈

IIS 및 ASP.NET Core 모듈의 데이터로 응용 프로그램 실행 될 때 전달 된 헤더 미들웨어 IIS 통합 미들웨어에서 기본적으로 사용 됩니다. 전달 된 헤더 미들웨어에 전달 된 헤더와 신뢰 문제로 인해 ASP.NET Core 모듈에 특정 제한 된 구성으로 미들웨어 파이프라인에서 첫 번째로 실행 하기 위해 활성화 됩니다 (예를 들어 [IP 스푸핑](https://www.iplocation.net/ip-spoofing)). 미들웨어 전달 하도록 구성 된 `X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더 단일 localhost 프록시로 제한 됩니다. 추가 구성이 필요한 경우 참조는 [전달 헤더 미들웨어 옵션입니다.](#forwarded-headers-middleware-options)합니다.

## <a name="other-proxy-server-and-load-balancer-scenarios"></a>다른 프록시 서버 및 부하 분산 장치 시나리오

IIS 통합 미들웨어를 사용 하 여 외부에서 전달 헤더 미들웨어는 기본적으로 사용 되지 않습니다. 전달 된 헤더 미들웨어 앱이 전달 프로세스 헤더를 사용 하도록 설정 합니다 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders)합니다. 없는 경우에 미들웨어를 사용 하도록 설정한 후 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) 기본값 미들웨어 지정 [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) 는 [ForwardedHeaders.None ](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders).

사용 하 여 미들웨어 구성 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) 전달 하는 `X-Forwarded-For` 및 `X-Forwarded-Proto` 에 헤더 `Startup.ConfigureServices`합니다. 호출 된 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 메서드에서 `Startup.Configure` 다른 미들웨어를 호출 하기 전에:

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
> 없는 경우 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) 에 지정 된 `Startup.ConfigureServices` 또는으로 확장 메서드를 직접 [UseForwardedHeaders (IApplicationBuilder, ForwardedHeadersOptions)](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ForwardedHeadersExtensions_UseForwardedHeaders_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_ForwardedHeadersOptions_), 기본값 전달 하는 헤더는 [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders)합니다. [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) 전달 하도록 헤더와 속성을 구성 해야 합니다.

## <a name="forwarded-headers-middleware-options"></a>전달 된 헤더 미들웨어 옵션입니다.

[ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) 전달 헤더 미들웨어의 동작을 제어 합니다.

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
| [ForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedforheadername) | 에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedforheadername)합니다.<br><br>기본값은 `X-Forwarded-For`입니다. |
| [ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) | 전달자 어떤를 처리할지를 식별 합니다. 참조는 [ForwardedHeaders Enum](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders) 적용 되는 필드 목록에 대 한 합니다. 이 속성에 할당 하는 일반적인 값은 <code>ForwardedHeaders.XForwardedFor &#124; ForwardedHeaders.XForwardedProto</code>합니다.<br><br>기본값은 [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders)합니다. |
| [ForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedhostheadername) | 에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedhostheadername)합니다.<br><br>기본값은 `X-Forwarded-Host`입니다. |
| [ForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedprotoheadername) | 에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedprotoheadername)합니다.<br><br>기본값은 `X-Forwarded-Proto`입니다. |
| [ForwardLimit](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardlimit) | 처리 되는 헤더에 있는 항목의 수를 제한 합니다. 로 설정 `null` 제한을 15, 하지만이 사용 하지 않도록 설정 하려면 수행 해야 하는 경우 `KnownProxies` 또는 `KnownNetworks` 구성 됩니다.<br><br>기본값은 1입니다. |
| [KnownNetworks](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownnetworks) | 주소 범위에서 전달 된 헤더를 허용 하도록 알려진 프록시입니다. 도메인간 CIDR (Classless Routing) 표기법을 사용 하는 IP 범위를 제공 합니다.<br><br>기본값은는 [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPNetwork](/dotnet/api/microsoft.aspnetcore.httpoverrides.ipnetwork)>에 대 한 단일 항목을 포함 하 `IPAddress.Loopback`합니다. |
| [KnownProxies](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownproxies) | 주소에서 전달 된 헤더를 허용 하도록 알려진된 프록시입니다. 사용 하 여 `KnownProxies` 정확한 IP 주소를 지정 하기 위해 일치 시킵니다.<br><br>기본값은는 [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPAddress](/dotnet/api/system.net.ipaddress)>에 대 한 단일 항목을 포함 하 `IPAddress.IPv6Loopback`합니다. |
| [OriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalforheadername) | 에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XOriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalforheadername)합니다.<br><br>기본값은 `X-Original-For`입니다. |
| [OriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalhostheadername) | 에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XOriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalhostheadername)합니다.<br><br>기본값은 `X-Original-Host`입니다. |
| [OriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalprotoheadername) | 에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XOriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalprotoheadername)합니다.<br><br>기본값은 `X-Original-Proto`입니다. |
| [RequireHeaderSymmetry](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.requireheadersymmetry) | 간의 동기화 되도록 헤더 값의 수는 수와 [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) 처리 되 고 있습니다.<br><br>ASP.NET Core 1.x는에서 기본 `true`합니다. ASP.NET Core 2.0 이상 기본값은 `false`합니다. |
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
| 옵션 | 설명 |
| ------ | ----------- |
| AllowedHosts | 제한 하 여 호스트의 `X-Forwarded-Host` 헤더를 제공 하는 값입니다.<ul><li>값은 서 수를 무시 사례를 사용 하 여 비교 됩니다.</li><li>포트 번호를 제외 되어야 합니다.</li><li>목록이 비어 있으면 모든 호스트 허용 됩니다.</li><li>최상위 와일드 카드 `*` 모든 비어 있지 않은 호스트를 허용 합니다.</li><li>하위 도메인 와일드 카드는 사용할 수 있지만 루트 도메인에 일치 하지 않습니다. 예를 들어 `*.contoso.com` 하위 도메인을 일치 `foo.contoso.com` 하지만 루트 도메인이 아닌 `contoso.com`합니다.</li><li>유니코드 호스트 이름 변경이 허용 되지만로 변환할지 [Punycode](https://tools.ietf.org/html/rfc3492) 일치에 대 한 합니다.</li><li>[IPv6 주소](https://tools.ietf.org/html/rfc4291) 대괄호 경계를 포함 하 고에 해야 [기존 폼](https://tools.ietf.org/html/rfc4291#section-2.2) (예를 들어 `[ABCD:EF01:2345:6789:ABCD:EF01:2345:6789]`). IPv6 주소가 않습니다 특별 하 게 처리를 다른 형식 간의 논리 일치성 확인 하 고 없는 정형화 수행 됩니다.</li><li>허용 되는 호스트를 제한 하지 않으면 공격자가 스푸핑할 서비스에서 생성 된 링크를 허용할 수 있습니다.</li></ul>기본값은 빈 [IList\<문자열 >](/dotnet/api/system.collections.generic.ilist-1)합니다. |
| [ForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedforheadername) | 에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedforheadername)합니다.<br><br>기본값은 `X-Forwarded-For`입니다. |
| [ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) | 전달자 어떤를 처리할지를 식별 합니다. 참조는 [ForwardedHeaders Enum](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders) 적용 되는 필드 목록에 대 한 합니다. 이 속성에 할당 하는 일반적인 값은 <code>ForwardedHeaders.XForwardedFor &#124; ForwardedHeaders.XForwardedProto</code>합니다.<br><br>기본값은 [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders)합니다. |
| [ForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedhostheadername) | 에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedhostheadername)합니다.<br><br>기본값은 `X-Forwarded-Host`입니다. |
| [ForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedprotoheadername) | 에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedprotoheadername)합니다.<br><br>기본값은 `X-Forwarded-Proto`입니다. |
| [ForwardLimit](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardlimit) | 처리 되는 헤더에 있는 항목의 수를 제한 합니다. 로 설정 `null` 제한을 15, 하지만이 사용 하지 않도록 설정 하려면 수행 해야 하는 경우 `KnownProxies` 또는 `KnownNetworks` 구성 됩니다.<br><br>기본값은 1입니다. |
| [KnownNetworks](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownnetworks) | 주소 범위에서 전달 된 헤더를 허용 하도록 알려진 프록시입니다. 도메인간 CIDR (Classless Routing) 표기법을 사용 하는 IP 범위를 제공 합니다.<br><br>기본값은는 [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPNetwork](/dotnet/api/microsoft.aspnetcore.httpoverrides.ipnetwork)>에 대 한 단일 항목을 포함 하 `IPAddress.Loopback`합니다. |
| [KnownProxies](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownproxies) | 주소에서 전달 된 헤더를 허용 하도록 알려진된 프록시입니다. 사용 하 여 `KnownProxies` 정확한 IP 주소를 지정 하기 위해 일치 시킵니다.<br><br>기본값은는 [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPAddress](/dotnet/api/system.net.ipaddress)>에 대 한 단일 항목을 포함 하 `IPAddress.IPv6Loopback`합니다. |
| [OriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalforheadername) | 에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XOriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalforheadername)합니다.<br><br>기본값은 `X-Original-For`입니다. |
| [OriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalhostheadername) | 에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XOriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalhostheadername)합니다.<br><br>기본값은 `X-Original-Host`입니다. |
| [OriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalprotoheadername) | 에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XOriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalprotoheadername)합니다.<br><br>기본값은 `X-Original-Proto`입니다. |
| [RequireHeaderSymmetry](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.requireheadersymmetry) | 간의 동기화 되도록 헤더 값의 수는 수와 [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) 처리 되 고 있습니다.<br><br>ASP.NET Core 1.x는에서 기본 `true`합니다. ASP.NET Core 2.0 이상 기본값은 `false`합니다. |
::: moniker-end

## <a name="scenarios-and-use-cases"></a>시나리오 및 사용 사례

### <a name="when-it-isnt-possible-to-add-forwarded-headers-and-all-requests-are-secure"></a>머리글 및 모든 요청은 보안 전달 추가할 수 없는 경우

않을 경우에 따라 하지 수 있습니다 응용 프로그램에 프록시 요청에 전달 된 헤더를 추가할 수 있습니다. 체계를 수동으로 설정할 수 프록시 모든 공용 외부 요청은 HTTPS를 지정 하는, 경우 `Startup.Configure` 모든 종류의 미들웨어를 사용 하기 전에:

```csharp
app.Use((context, next) =>
{
    context.Request.Scheme = "https";
    return next();
});
```

이 코드는 환경 변수 또는 개발 또는 스테이징 환경에서 다른 구성 설정을 해제할 수 있습니다.

### <a name="deal-with-path-base-and-proxies-that-change-the-request-path"></a>기본 경로 요청 경로 변경 하는 프록시를 사용 처리

일부 프록시 경로 그대로 전달 하지만 응용 프로그램과 함께 라우팅 않도록 제거 해야 하는 기본 경로 제대로 작동 합니다. [UsePathBaseExtensions.UsePathBase](/dotnet/api/microsoft.aspnetcore.builder.usepathbaseextensions.usepathbase) 미들웨어에 대 한 경로 분할 [HttpRequest.Path](/dotnet/api/microsoft.aspnetcore.http.httprequest.path) 에 대 한 응용 프로그램 기본 경로가 [HttpRequest.PathBase](/dotnet/api/microsoft.aspnetcore.http.httprequest.pathbase)합니다.

경우 `/foo` 변수로 전달 된 프록시 경로 대 한 응용 프로그램 기본 경로 `/foo/api/1`, 미들웨어 집합 `Request.PathBase` 를 `/foo` 및 `Request.Path` 를 `/api/1` 다음 명령을 사용 하 여:

```csharp
app.UsePathBase("/foo");
```

원래 경로 기본 경로 미들웨어를 반대 방향으로 다시 호출 하는 경우 다시 적용 됩니다. 미들웨어 주문 처리에 대 한 자세한 내용은 참조 하십시오. [미들웨어](xref:fundamentals/middleware/index)합니다.

프록시 경로 삭제 하는 경우 (예를 들어 전달 `/foo/api/1` 를 `/api/1`), 수정 프로그램은 요청을 설정 하 여 연결 리디렉션하고 [PathBase](/dotnet/api/microsoft.aspnetcore.http.httprequest.pathbase) 속성:

```csharp
app.Use((context, next) =>
{
    context.Request.PathBase = new PathString("/foo");
    return next();
});
```

프록시 경로 데이터를 추가 하는 경우 리디렉션 및 링크를 사용 하 여 문제를 해결 하려면 경로의 일부가 삭제 [StartsWithSegments (PathString, PathString)](/dotnet/api/microsoft.aspnetcore.http.pathstring.startswithsegments#Microsoft_AspNetCore_Http_PathString_StartsWithSegments_Microsoft_AspNetCore_Http_PathString_Microsoft_AspNetCore_Http_PathString__) 할당 하는 데는 [경로](/dotnet/api/microsoft.aspnetcore.http.httprequest.path) 속성:

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

예상 대로 헤더가 전달 되지를 사용할 수 있는 [로깅](xref:fundamentals/logging/index)합니다. 로그 문제 해결을 위해 충분 한 정보를 제공 하지 않는 경우 서버에서 받은 요청 헤더를 열거 합니다. 인라인 미들웨어를 사용 하는 응용 프로그램 응답에 대 한 헤더를 작성할 수 있습니다.

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

X-전달 되도록 * 예상 값을 사용 하 여 서버 헤더가 수신 합니다. 지정된 된 헤더 값이 여러 개인 경우 note 반대 순서로 오른쪽에서 왼쪽으로 헤더 미들웨어 전달 프로세스 헤더입니다.

요청의 원래 원격 IP에 있는 항목과 일치 해야 합니다는 `KnownProxies` 또는 `KnownNetworks` X-전달 기능에 대 한 처리 되기 전에 나열 합니다. 이 헤더의 신뢰할 수 없는 프록시 전달자를 허용 하지 않음으로써 스푸핑 제한 됩니다.

## <a name="additional-resources"></a>추가 자료

* [Microsoft 보안 권고 CVE-2018-0787: ASP.NET Core 권한 상승 취약점](https://github.com/aspnet/Announcements/issues/295)
