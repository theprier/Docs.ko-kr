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
ms.openlocfilehash: b153a7406ae1b31a2aa453135c6bd0e5ce0b2997
ms.sourcegitcommit: d45d766504c2c5aad2453f01f089bc6b696b5576
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="configure-aspnet-core-to-work-with-proxy-servers-and-load-balancers"></a><span data-ttu-id="2c8b3-103">ASP.NET Core 프록시 서버를 사용 하 고 부하 분산 장치를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-103">Configure ASP.NET Core to work with proxy servers and load balancers</span></span>

<span data-ttu-id="2c8b3-104">여 [Luke Latham](https://github.com/guardrex) 및 [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="2c8b3-104">By [Luke Latham](https://github.com/guardrex) and [Chris Ross](https://github.com/Tratcher)</span></span>

<span data-ttu-id="2c8b3-105">ASP.NET Core에 대 한 권장된 구성에서 iis/ASP.NET Core 모듈, Nginx, 또는 Apache를 사용 하 여 응용 프로그램 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-105">In the recommended configuration for ASP.NET Core, the app is hosted using IIS/ASP.NET Core Module, Nginx, or Apache.</span></span> <span data-ttu-id="2c8b3-106">프록시 서버, 부하 분산 장치, 및 기타 네트워크 장치 종종를 려 서 요청에 대 한 정보는 응용 프로그램에 도달 하기 전에:</span><span class="sxs-lookup"><span data-stu-id="2c8b3-106">Proxy servers, load balancers, and other network appliances often obscure information about the request before it reaches the app:</span></span>

* <span data-ttu-id="2c8b3-107">HTTPS 요청은 HTTP를 통해 프록시를 원본 구성표 (HTTPS) 삭제 되 고 헤더에 전달 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-107">When HTTPS requests are proxied over HTTP, the original scheme (HTTPS) is lost and must be forwarded in a header.</span></span>
* <span data-ttu-id="2c8b3-108">응용 프로그램 프록시와 인터넷 이나 회사 네트워크에 true의 원본이 아닌에서 요청 받으면 때문에 원래 클라이언트 IP 주소 헤더에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-108">Because an app receives a request from the proxy and not its true source on the Internet or corporate network, the originating client IP address must also be forwarded in a header.</span></span>

<span data-ttu-id="2c8b3-109">이 정보는 예를 들어 리디렉션을, 인증, 링크 생성, 정책 평가 및 클라이언트 geoloation에 처리 요청에 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-109">This information may be important in request processing, for example in redirects, authentication, link generation, policy evaluation, and client geoloation.</span></span>

## <a name="forwarded-headers"></a><span data-ttu-id="2c8b3-110">전달 된 헤더</span><span class="sxs-lookup"><span data-stu-id="2c8b3-110">Forwarded headers</span></span>

<span data-ttu-id="2c8b3-111">규칙에 따라 프록시는 HTTP 헤더에 대 한 정보를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-111">By convention, proxies forward information in HTTP headers.</span></span>

| <span data-ttu-id="2c8b3-112">Header</span><span class="sxs-lookup"><span data-stu-id="2c8b3-112">Header</span></span> | <span data-ttu-id="2c8b3-113">설명</span><span class="sxs-lookup"><span data-stu-id="2c8b3-113">Description</span></span> |
| ------ | ----------- |
| <span data-ttu-id="2c8b3-114">X-Forwarded-For</span><span class="sxs-lookup"><span data-stu-id="2c8b3-114">X-Forwarded-For</span></span> | <span data-ttu-id="2c8b3-115">요청을 후속 프록시의 체인에 시작한 클라이언트에 대 한 정보를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-115">Holds information about the client that initiated the request and subsequent proxies in a chain of proxies.</span></span> <span data-ttu-id="2c8b3-116">이 매개 변수는 IP 주소 (및 필요에 따라 포트 번호)에 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-116">This parameter may contain IP addresses (and, optionally, port numbers).</span></span> <span data-ttu-id="2c8b3-117">프록시 서버의 체인을 첫 번째 매개 변수는 요청이 처음으로 된 클라이언트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-117">In a chain of proxy servers, the first parameter indicates the client where the request was first made.</span></span> <span data-ttu-id="2c8b3-118">후속 프록시 식별자 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-118">Subsequent proxy identifiers follow.</span></span> <span data-ttu-id="2c8b3-119">체인에서 마지막 프록시 매개 변수 목록이 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-119">The last proxy in the chain isn't in the list of parameters.</span></span> <span data-ttu-id="2c8b3-120">마지막 프록시의 IP 주소 및 포트 번호를 필요에 따라 전송 계층에서의 원격 IP 주소로 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-120">The last proxy's IP address, and optionally a port number, are available as the remote IP address at the transport layer.</span></span> |
| <span data-ttu-id="2c8b3-121">X-Forwarded-Proto</span><span class="sxs-lookup"><span data-stu-id="2c8b3-121">X-Forwarded-Proto</span></span> | <span data-ttu-id="2c8b3-122">원래 체계 (HTTP/HTTPS)의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-122">The value of the originating scheme (HTTP/HTTPS).</span></span> <span data-ttu-id="2c8b3-123">값은 요청이 여러 프록시를 이동 하는 경우 스키마의 목록이 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-123">The value may also be a list of schemes if the request has traversed multiple proxies.</span></span> |
| <span data-ttu-id="2c8b3-124">X-Forwarded-Host</span><span class="sxs-lookup"><span data-stu-id="2c8b3-124">X-Forwarded-Host</span></span> | <span data-ttu-id="2c8b3-125">호스트 헤더 필드의 원래 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-125">The original value of the Host header field.</span></span> <span data-ttu-id="2c8b3-126">일반적으로 프록시 호스트 헤더를 수정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-126">Usually, proxies don't modify the Host header.</span></span> <span data-ttu-id="2c8b3-127">참조 [Microsoft 보안 권고 CVE-2018-0787](https://github.com/aspnet/Announcements/issues/295) 프록시 하지 않는 유효성을 검사 하는 시스템에 영향을 주는 권한 상승 취약점 또는 알려진된 좋은 값에 restict 호스트 헤더에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-127">See [Microsoft Security Advisory CVE-2018-0787](https://github.com/aspnet/Announcements/issues/295) for information on an elevation-of-privileges vulnerability that affects systems where the proxy doesn't validate or restict Host headers to known good values.</span></span> |

<span data-ttu-id="2c8b3-128">전달 헤더 미들웨어에서는 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 패키지, 이러한 헤더를 읽고,에 연결 된 필드에 입력 [HttpContext](/dotnet/api/microsoft.aspnetcore.http.httpcontext)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-128">The Forwarded Headers Middleware, from the [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) package, reads these headers and fills in the associated fields on [HttpContext](/dotnet/api/microsoft.aspnetcore.http.httpcontext).</span></span> 

<span data-ttu-id="2c8b3-129">미들웨어 업데이트:</span><span class="sxs-lookup"><span data-stu-id="2c8b3-129">The middleware updates:</span></span>

* <span data-ttu-id="2c8b3-130">[HttpContext.Connection.RemoteIpAddress](/dotnet/api/microsoft.aspnetcore.http.connectioninfo.remoteipaddress) &ndash; 사용 하 여 설정 된 `X-Forwarded-For` 헤더 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-130">[HttpContext.Connection.RemoteIpAddress](/dotnet/api/microsoft.aspnetcore.http.connectioninfo.remoteipaddress) &ndash; Set using the `X-Forwarded-For` header value.</span></span> <span data-ttu-id="2c8b3-131">미들웨어가 설정 하는 방법에 영향을 줄 추가 설정을 `RemoteIpAddress`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-131">Additional settings influence how the middleware sets `RemoteIpAddress`.</span></span> <span data-ttu-id="2c8b3-132">자세한 내용은 참조는 [전달 헤더 미들웨어 옵션입니다.](#forwarded-headers-middleware-options)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-132">For details, see the [Forwarded Headers Middleware options](#forwarded-headers-middleware-options).</span></span>
* <span data-ttu-id="2c8b3-133">[HttpContext.Request.Scheme](/dotnet/api/microsoft.aspnetcore.http.httprequest.scheme) &ndash; 사용 하 여 설정 된 `X-Forwarded-Proto` 헤더 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-133">[HttpContext.Request.Scheme](/dotnet/api/microsoft.aspnetcore.http.httprequest.scheme) &ndash; Set using the `X-Forwarded-Proto` header value.</span></span>
* <span data-ttu-id="2c8b3-134">[HttpContext.Request.Host](/dotnet/api/microsoft.aspnetcore.http.httprequest.host) &ndash; 사용 하 여 설정 된 `X-Forwarded-Host` 헤더 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-134">[HttpContext.Request.Host](/dotnet/api/microsoft.aspnetcore.http.httprequest.host) &ndash; Set using the `X-Forwarded-Host` header value.</span></span>

<span data-ttu-id="2c8b3-135">일부 네트워크 어플라이언스에 추가 참고는 `X-Forwarded-For` 및 `X-Forwarded-Proto` 추가 구성 없이 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-135">Note that not all network appliances add the `X-Forwarded-For` and `X-Forwarded-Proto` headers without additional configuration.</span></span> <span data-ttu-id="2c8b3-136">응용 프로그램에 도달 하면 프록시 요청 이러한 헤더를 포함 하지 않는 경우 기기 제조업체의 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-136">Consult your appliance manufacturer's guidance if the proxied requests don't contain these headers when they reach the app.</span></span>

<span data-ttu-id="2c8b3-137">헤더 미들웨어 전달 [기본 설정](#forwarded-headers-middleware-options) 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-137">Forwarded Headers Middleware [default settings](#forwarded-headers-middleware-options) can be configured.</span></span> <span data-ttu-id="2c8b3-138">기본 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-138">The default settings are:</span></span>

* <span data-ttu-id="2c8b3-139">뿐 *하나의 프록시* 응용 프로그램 사이의 요청의 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-139">There is only *one proxy* between the app and the source of the requests.</span></span>
* <span data-ttu-id="2c8b3-140">루프백 주소에만 알려진된 프록시에 대 한 구성 되 고 네트워크 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-140">Only loopback addresses are configured for known proxies and known networks.</span></span>

## <a name="iisiis-express-and-aspnet-core-module"></a><span data-ttu-id="2c8b3-141">IIS/IIS Express 및 ASP.NET Core 모듈</span><span class="sxs-lookup"><span data-stu-id="2c8b3-141">IIS/IIS Express and ASP.NET Core Module</span></span>

<span data-ttu-id="2c8b3-142">IIS 및 ASP.NET Core 모듈의 데이터로 응용 프로그램 실행 될 때 전달 된 헤더 미들웨어 IIS 통합 미들웨어에서 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-142">Forwarded Headers Middleware is enabled by default by IIS Integration Middleware when the app is run behind IIS and the ASP.NET Core Module.</span></span> <span data-ttu-id="2c8b3-143">전달 된 헤더 미들웨어에 전달 된 헤더와 신뢰 문제로 인해 ASP.NET Core 모듈에 특정 제한 된 구성으로 미들웨어 파이프라인에서 첫 번째로 실행 하기 위해 활성화 됩니다 (예를 들어 [IP 스푸핑](https://www.iplocation.net/ip-spoofing)).</span><span class="sxs-lookup"><span data-stu-id="2c8b3-143">Forwarded Headers Middleware is activated to run first in the middleware pipeline with a restricted configuration specific to the ASP.NET Core Module due to trust concerns with forwarded headers (for example, [IP spoofing](https://www.iplocation.net/ip-spoofing)).</span></span> <span data-ttu-id="2c8b3-144">미들웨어 전달 하도록 구성 된 `X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더 단일 localhost 프록시로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-144">The middleware is configured to forward the `X-Forwarded-For` and `X-Forwarded-Proto` headers and is restricted to a single localhost proxy.</span></span> <span data-ttu-id="2c8b3-145">추가 구성이 필요한 경우 참조는 [전달 헤더 미들웨어 옵션입니다.](#forwarded-headers-middleware-options)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-145">If additional configuration is required, see the [Forwarded Headers Middleware options](#forwarded-headers-middleware-options).</span></span>

## <a name="other-proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="2c8b3-146">다른 프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="2c8b3-146">Other proxy server and load balancer scenarios</span></span>

<span data-ttu-id="2c8b3-147">IIS 통합 미들웨어를 사용 하 여 외부에서 전달 헤더 미들웨어는 기본적으로 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-147">Outside of using IIS Integration Middleware, Forwarded Headers Middleware isn't enabled by default.</span></span> <span data-ttu-id="2c8b3-148">전달 된 헤더 미들웨어 앱이 전달 프로세스 헤더를 사용 하도록 설정 합니다 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-148">Forwarded Headers Middleware must be enabled for an app to process forwarded headers with [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders).</span></span> <span data-ttu-id="2c8b3-149">없는 경우에 미들웨어를 사용 하도록 설정한 후 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) 기본값 미들웨어 지정 [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) 는 [ForwardedHeaders.None ](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders).</span><span class="sxs-lookup"><span data-stu-id="2c8b3-149">After enabling the middleware if no [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) are specified to the middleware, the default [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) are [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders).</span></span>

<span data-ttu-id="2c8b3-150">사용 하 여 미들웨어 구성 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) 전달 하는 `X-Forwarded-For` 및 `X-Forwarded-Proto` 에 헤더 `Startup.ConfigureServices`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-150">Configure the middleware with [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) to forward the `X-Forwarded-For` and `X-Forwarded-Proto` headers in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="2c8b3-151">호출 된 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 메서드에서 `Startup.Configure` 다른 미들웨어를 호출 하기 전에:</span><span class="sxs-lookup"><span data-stu-id="2c8b3-151">Invoke the [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) method in `Startup.Configure` before calling other middleware:</span></span>

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
> <span data-ttu-id="2c8b3-152">없는 경우 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) 에 지정 된 `Startup.ConfigureServices` 또는으로 확장 메서드를 직접 [UseForwardedHeaders (IApplicationBuilder, ForwardedHeadersOptions)](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ForwardedHeadersExtensions_UseForwardedHeaders_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_ForwardedHeadersOptions_), 기본값 전달 하는 헤더는 [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-152">If no [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) are specified in `Startup.ConfigureServices` or directly to the extension method with [UseForwardedHeaders(IApplicationBuilder, ForwardedHeadersOptions)](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ForwardedHeadersExtensions_UseForwardedHeaders_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_ForwardedHeadersOptions_), the default headers to forward are [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders).</span></span> <span data-ttu-id="2c8b3-153">[ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) 전달 하도록 헤더와 속성을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-153">The [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) property must be configured with the headers to forward.</span></span>

## <a name="forwarded-headers-middleware-options"></a><span data-ttu-id="2c8b3-154">전달 된 헤더 미들웨어 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-154">Forwarded Headers Middleware options</span></span>

<span data-ttu-id="2c8b3-155">[ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) 전달 헤더 미들웨어의 동작을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-155">[ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) control the behavior of the Forwarded Headers Middleware:</span></span>

```csharp
services.Configure<ForwardedHeadersOptions>(options =>
{
    options.ForwardLimit = 2;
    options.KnownProxies.Add(IPAddress.Parse("127.0.10.1"));
    options.ForwardedForHeaderName = "X-Forwarded-For-Custom-Header-Name";
});
```

| <span data-ttu-id="2c8b3-156">옵션</span><span class="sxs-lookup"><span data-stu-id="2c8b3-156">Option</span></span> | <span data-ttu-id="2c8b3-157">설명</span><span class="sxs-lookup"><span data-stu-id="2c8b3-157">Description</span></span> |
| ------ | ----------- |
| [<span data-ttu-id="2c8b3-158">ForwardedForHeaderName</span><span class="sxs-lookup"><span data-stu-id="2c8b3-158">ForwardedForHeaderName</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedforheadername) | <span data-ttu-id="2c8b3-159">에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedforheadername)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-159">Use the header specified by this property instead of the one specified by [ForwardedHeadersDefaults.XForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedforheadername).</span></span><br><br><span data-ttu-id="2c8b3-160">기본값은 `X-Forwarded-For`입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-160">The default is `X-Forwarded-For`.</span></span> |
| [<span data-ttu-id="2c8b3-161">ForwardedHeaders</span><span class="sxs-lookup"><span data-stu-id="2c8b3-161">ForwardedHeaders</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) | <span data-ttu-id="2c8b3-162">전달자 어떤를 처리할지를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-162">Identifies which forwarders should be processed.</span></span> <span data-ttu-id="2c8b3-163">참조는 [ForwardedHeaders Enum](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders) 적용 되는 필드 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-163">See the [ForwardedHeaders Enum](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders) for the list of fields that apply.</span></span> <span data-ttu-id="2c8b3-164">이 속성에 할당 하는 일반적인 값은 <code>ForwardedHeaders.XForwardedFor &#124; ForwardedHeaders.XForwardedProto</code>합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-164">Typical values assigned to this property are <code>ForwardedHeaders.XForwardedFor &#124; ForwardedHeaders.XForwardedProto</code>.</span></span><br><br><span data-ttu-id="2c8b3-165">기본값은 [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-165">The default value is [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders).</span></span> |
| [<span data-ttu-id="2c8b3-166">ForwardedHostHeaderName</span><span class="sxs-lookup"><span data-stu-id="2c8b3-166">ForwardedHostHeaderName</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedhostheadername) | <span data-ttu-id="2c8b3-167">에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedhostheadername)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-167">Use the header specified by this property instead of the one specified by [ForwardedHeadersDefaults.XForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedhostheadername).</span></span><br><br><span data-ttu-id="2c8b3-168">기본값은 `X-Forwarded-Host`입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-168">The default is `X-Forwarded-Host`.</span></span> |
| [<span data-ttu-id="2c8b3-169">ForwardedProtoHeaderName</span><span class="sxs-lookup"><span data-stu-id="2c8b3-169">ForwardedProtoHeaderName</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedprotoheadername) | <span data-ttu-id="2c8b3-170">에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedprotoheadername)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-170">Use the header specified by this property instead of the one specified by [ForwardedHeadersDefaults.XForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedprotoheadername).</span></span><br><br><span data-ttu-id="2c8b3-171">기본값은 `X-Forwarded-Proto`입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-171">The default is `X-Forwarded-Proto`.</span></span> |
| [<span data-ttu-id="2c8b3-172">ForwardLimit</span><span class="sxs-lookup"><span data-stu-id="2c8b3-172">ForwardLimit</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardlimit) | <span data-ttu-id="2c8b3-173">처리 되는 헤더에 있는 항목의 수를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-173">Limits the number of entries in the headers that are processed.</span></span> <span data-ttu-id="2c8b3-174">로 설정 `null` 제한을 15, 하지만이 사용 하지 않도록 설정 하려면 수행 해야 하는 경우 `KnownProxies` 또는 `KnownNetworks` 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-174">Set to `null` to disable the limit, but this should only be done if `KnownProxies` or `KnownNetworks` are configured.</span></span><br><br><span data-ttu-id="2c8b3-175">기본값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-175">The default is 1.</span></span> |
| [<span data-ttu-id="2c8b3-176">KnownNetworks</span><span class="sxs-lookup"><span data-stu-id="2c8b3-176">KnownNetworks</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownnetworks) | <span data-ttu-id="2c8b3-177">주소 범위에서 전달 된 헤더를 허용 하도록 알려진 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-177">Address ranges of known proxies to accept forwarded headers from.</span></span> <span data-ttu-id="2c8b3-178">도메인간 CIDR (Classless Routing) 표기법을 사용 하는 IP 범위를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-178">Provide IP ranges using Classless Interdomain Routing (CIDR) notation.</span></span><br><br><span data-ttu-id="2c8b3-179">기본값은는 [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPNetwork](/dotnet/api/microsoft.aspnetcore.httpoverrides.ipnetwork)>에 대 한 단일 항목을 포함 하 `IPAddress.Loopback`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-179">The default is an [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPNetwork](/dotnet/api/microsoft.aspnetcore.httpoverrides.ipnetwork)> containing a single entry for `IPAddress.Loopback`.</span></span> |
| [<span data-ttu-id="2c8b3-180">KnownProxies</span><span class="sxs-lookup"><span data-stu-id="2c8b3-180">KnownProxies</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownproxies) | <span data-ttu-id="2c8b3-181">주소에서 전달 된 헤더를 허용 하도록 알려진된 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-181">Addresses of known proxies to accept forwarded headers from.</span></span> <span data-ttu-id="2c8b3-182">사용 하 여 `KnownProxies` 정확한 IP 주소를 지정 하기 위해 일치 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-182">Use `KnownProxies` to specify exact IP address matches.</span></span><br><br><span data-ttu-id="2c8b3-183">기본값은는 [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPAddress](/dotnet/api/system.net.ipaddress)>에 대 한 단일 항목을 포함 하 `IPAddress.IPv6Loopback`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-183">The default is an [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPAddress](/dotnet/api/system.net.ipaddress)> containing a single entry for `IPAddress.IPv6Loopback`.</span></span> |
| [<span data-ttu-id="2c8b3-184">OriginalForHeaderName</span><span class="sxs-lookup"><span data-stu-id="2c8b3-184">OriginalForHeaderName</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalforheadername) | <span data-ttu-id="2c8b3-185">에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XOriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalforheadername)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-185">Use the header specified by this property instead of the one specified by [ForwardedHeadersDefaults.XOriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalforheadername).</span></span><br><br><span data-ttu-id="2c8b3-186">기본값은 `X-Original-For`입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-186">The default is `X-Original-For`.</span></span> |
| [<span data-ttu-id="2c8b3-187">OriginalHostHeaderName</span><span class="sxs-lookup"><span data-stu-id="2c8b3-187">OriginalHostHeaderName</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalhostheadername) | <span data-ttu-id="2c8b3-188">에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XOriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalhostheadername)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-188">Use the header specified by this property instead of the one specified by [ForwardedHeadersDefaults.XOriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalhostheadername).</span></span><br><br><span data-ttu-id="2c8b3-189">기본값은 `X-Original-Host`입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-189">The default is `X-Original-Host`.</span></span> |
| [<span data-ttu-id="2c8b3-190">OriginalProtoHeaderName</span><span class="sxs-lookup"><span data-stu-id="2c8b3-190">OriginalProtoHeaderName</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalprotoheadername) | <span data-ttu-id="2c8b3-191">에 의해 지정 된 하는 대신이 속성에서 지정 된 헤더를 사용 하 여 [ForwardedHeadersDefaults.XOriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalprotoheadername)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-191">Use the header specified by this property instead of the one specified by [ForwardedHeadersDefaults.XOriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalprotoheadername).</span></span><br><br><span data-ttu-id="2c8b3-192">기본값은 `X-Original-Proto`입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-192">The default is `X-Original-Proto`.</span></span> |
| [<span data-ttu-id="2c8b3-193">RequireHeaderSymmetry</span><span class="sxs-lookup"><span data-stu-id="2c8b3-193">RequireHeaderSymmetry</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.requireheadersymmetry) | <span data-ttu-id="2c8b3-194">간의 동기화 되도록 헤더 값의 수는 수와 [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) 처리 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-194">Require the number of header values to be in sync between the [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) being processed.</span></span><br><br><span data-ttu-id="2c8b3-195">ASP.NET Core 1.x는에서 기본 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-195">The default in ASP.NET Core 1.x is `true`.</span></span> <span data-ttu-id="2c8b3-196">ASP.NET Core 2.0 이상 기본값은 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-196">The default in ASP.NET Core 2.0 or later is `false`.</span></span> |

## <a name="scenarios-and-use-cases"></a><span data-ttu-id="2c8b3-197">시나리오 및 사용 사례</span><span class="sxs-lookup"><span data-stu-id="2c8b3-197">Scenarios and use cases</span></span>

### <a name="when-it-isnt-possible-to-add-forwarded-headers-and-all-requests-are-secure"></a><span data-ttu-id="2c8b3-198">머리글 및 모든 요청은 보안 전달 추가할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="2c8b3-198">When it isn't possible to add forwarded headers and all requests are secure</span></span>

<span data-ttu-id="2c8b3-199">않을 경우에 따라 하지 수 있습니다 응용 프로그램에 프록시 요청에 전달 된 헤더를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-199">In some cases, it might not be possible to add forwarded headers to the requests proxied to the app.</span></span> <span data-ttu-id="2c8b3-200">체계를 수동으로 설정할 수 프록시 모든 공용 외부 요청은 HTTPS를 지정 하는, 경우 `Startup.Configure` 모든 종류의 미들웨어를 사용 하기 전에:</span><span class="sxs-lookup"><span data-stu-id="2c8b3-200">If the proxy is enforcing that all public external requests are HTTPS, the scheme can be manually set in `Startup.Configure` before using any type of middleware:</span></span>

```csharp
app.Use((context, next) =>
{
    context.Request.Scheme = "https";
    return next();
});
```

<span data-ttu-id="2c8b3-201">이 코드는 환경 변수 또는 개발 또는 스테이징 환경에서 다른 구성 설정을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-201">This code can be disabled with an environment variable or other configuration setting in a development or staging environment.</span></span>

### <a name="deal-with-path-base-and-proxies-that-change-the-request-path"></a><span data-ttu-id="2c8b3-202">기본 경로 요청 경로 변경 하는 프록시를 사용 처리</span><span class="sxs-lookup"><span data-stu-id="2c8b3-202">Deal with path base and proxies that change the request path</span></span>

<span data-ttu-id="2c8b3-203">일부 프록시 경로 그대로 전달 하지만 응용 프로그램과 함께 라우팅 않도록 제거 해야 하는 기본 경로 제대로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-203">Some proxies pass the path intact but with an app base path that should be removed so that routing works properly.</span></span> <span data-ttu-id="2c8b3-204">[UsePathBaseExtensions.UsePathBase](/dotnet/api/microsoft.aspnetcore.builder.usepathbaseextensions.usepathbase) 미들웨어에 대 한 경로 분할 [HttpRequest.Path](/dotnet/api/microsoft.aspnetcore.http.httprequest.path) 에 대 한 응용 프로그램 기본 경로가 [HttpRequest.PathBase](/dotnet/api/microsoft.aspnetcore.http.httprequest.pathbase)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-204">[UsePathBaseExtensions.UsePathBase](/dotnet/api/microsoft.aspnetcore.builder.usepathbaseextensions.usepathbase) middleware splits the path into [HttpRequest.Path](/dotnet/api/microsoft.aspnetcore.http.httprequest.path) and the app base path into [HttpRequest.PathBase](/dotnet/api/microsoft.aspnetcore.http.httprequest.pathbase).</span></span>

<span data-ttu-id="2c8b3-205">경우 `/foo` 변수로 전달 된 프록시 경로 대 한 응용 프로그램 기본 경로 `/foo/api/1`, 미들웨어 집합 `Request.PathBase` 를 `/foo` 및 `Request.Path` 를 `/api/1` 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="2c8b3-205">If `/foo` is the app base path for a proxy path passed as `/foo/api/1`, the middleware sets `Request.PathBase` to `/foo` and `Request.Path` to `/api/1` with the following command:</span></span>

```csharp
app.UsePathBase("/foo");
```

<span data-ttu-id="2c8b3-206">원래 경로 기본 경로 미들웨어를 반대 방향으로 다시 호출 하는 경우 다시 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-206">The original path and path base are reapplied when the middleware is called again in reverse.</span></span> <span data-ttu-id="2c8b3-207">미들웨어 주문 처리에 대 한 자세한 내용은 참조 하십시오. [미들웨어](xref:fundamentals/middleware/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-207">For more information on middleware order processing, see [Middleware](xref:fundamentals/middleware/index).</span></span>

<span data-ttu-id="2c8b3-208">프록시 경로 삭제 하는 경우 (예를 들어 전달 `/foo/api/1` 를 `/api/1`), 수정 프로그램은 요청을 설정 하 여 연결 리디렉션하고 [PathBase](/dotnet/api/microsoft.aspnetcore.http.httprequest.pathbase) 속성:</span><span class="sxs-lookup"><span data-stu-id="2c8b3-208">If the proxy trims the path (for example, forwarding `/foo/api/1` to `/api/1`), fix redirects and links by setting the request's [PathBase](/dotnet/api/microsoft.aspnetcore.http.httprequest.pathbase) property:</span></span>

```csharp
app.Use((context, next) =>
{
    context.Request.PathBase = new PathString("/foo");
    return next();
});
```

<span data-ttu-id="2c8b3-209">프록시 경로 데이터를 추가 하는 경우 리디렉션 및 링크를 사용 하 여 문제를 해결 하려면 경로의 일부가 삭제 [StartsWithSegments (PathString, PathString)](/dotnet/api/microsoft.aspnetcore.http.pathstring.startswithsegments#Microsoft_AspNetCore_Http_PathString_StartsWithSegments_Microsoft_AspNetCore_Http_PathString_Microsoft_AspNetCore_Http_PathString__) 할당 하는 데는 [경로](/dotnet/api/microsoft.aspnetcore.http.httprequest.path) 속성:</span><span class="sxs-lookup"><span data-stu-id="2c8b3-209">If the proxy is adding path data, discard part of the path to fix redirects and links by using [StartsWithSegments(PathString, PathString)](/dotnet/api/microsoft.aspnetcore.http.pathstring.startswithsegments#Microsoft_AspNetCore_Http_PathString_StartsWithSegments_Microsoft_AspNetCore_Http_PathString_Microsoft_AspNetCore_Http_PathString__) and assigning to the [Path](/dotnet/api/microsoft.aspnetcore.http.httprequest.path) property:</span></span>

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

## <a name="troubleshoot"></a><span data-ttu-id="2c8b3-210">문제 해결</span><span class="sxs-lookup"><span data-stu-id="2c8b3-210">Troubleshoot</span></span>

<span data-ttu-id="2c8b3-211">예상 대로 헤더가 전달 되지를 사용할 수 있는 [로깅](xref:fundamentals/logging/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-211">When headers aren't forwarded as expected, enable [logging](xref:fundamentals/logging/index).</span></span> <span data-ttu-id="2c8b3-212">로그 문제 해결을 위해 충분 한 정보를 제공 하지 않는 경우 서버에서 받은 요청 헤더를 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-212">If the logs don't provide sufficient information to troubleshoot the problem, enumerate the request headers received by the server.</span></span> <span data-ttu-id="2c8b3-213">인라인 미들웨어를 사용 하는 응용 프로그램 응답에 대 한 헤더를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-213">The headers can be written to an app response using inline middleware:</span></span>

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

<span data-ttu-id="2c8b3-214">X-전달 되도록 \* 예상 값을 사용 하 여 서버 헤더가 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-214">Ensure that the X-Forwarded-\* headers are received by the server with the expected values.</span></span> <span data-ttu-id="2c8b3-215">지정된 된 헤더 값이 여러 개인 경우 note 반대 순서로 오른쪽에서 왼쪽으로 헤더 미들웨어 전달 프로세스 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-215">If there are multiple values in a given header, note Forwarded Headers Middleware processes headers in reverse order from right to left.</span></span>

<span data-ttu-id="2c8b3-216">요청의 원래 원격 IP에 있는 항목과 일치 해야 합니다는 `KnownProxies` 또는 `KnownNetworks` X-전달 기능에 대 한 처리 되기 전에 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-216">The request's original remote IP must match an entry in the `KnownProxies` or `KnownNetworks` lists before X-Forwarded-For is processed.</span></span> <span data-ttu-id="2c8b3-217">이 헤더의 신뢰할 수 없는 프록시 전달자를 허용 하지 않음으로써 스푸핑 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c8b3-217">This limits header spoofing by not accepting forwarders from untrusted proxies.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2c8b3-218">추가 자료</span><span class="sxs-lookup"><span data-stu-id="2c8b3-218">Additional resources</span></span>

* [<span data-ttu-id="2c8b3-219">Microsoft 보안 권고 CVE-2018-0787: ASP.NET Core 권한 상승 취약점</span><span class="sxs-lookup"><span data-stu-id="2c8b3-219">Microsoft Security Advisory CVE-2018-0787: ASP.NET Core Elevation Of Privilege Vulnerability</span></span>](https://github.com/aspnet/Announcements/issues/295)
