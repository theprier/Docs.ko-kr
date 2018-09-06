---
title: ASP.NET Core에서 HTTPS 적용
author: rick-anderson
description: 웹 앱을 ASP.NET Core에서 HTTPS/TLS를 요구 하는 방법에 보여 줍니다.
ms.author: riande
ms.date: 2/9/2018
uid: security/enforcing-ssl
ms.openlocfilehash: 838cd00545f36736461616f806942249aaf6eee0
ms.sourcegitcommit: 4cd8dce371d63a66d780e4af1baab2bcf9d61b24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893180"
---
# <a name="enforce-https-in-aspnet-core"></a><span data-ttu-id="84b7c-103">ASP.NET Core에서 HTTPS 적용</span><span class="sxs-lookup"><span data-stu-id="84b7c-103">Enforce HTTPS in ASP.NET Core</span></span>

<span data-ttu-id="84b7c-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="84b7c-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="84b7c-105">이 문서에서는 다음과 같은 내용을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-105">This document shows how to:</span></span>

* <span data-ttu-id="84b7c-106">모든 요청에 대 한 HTTPS가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-106">Require HTTPS for all requests.</span></span>
* <span data-ttu-id="84b7c-107">모든 HTTP 요청을 HTTPS로 리디렉션하는 방법.</span><span class="sxs-lookup"><span data-stu-id="84b7c-107">Redirect all HTTP requests to HTTPS.</span></span>

<span data-ttu-id="84b7c-108">API가 없습니다. 첫 번째 요청 시 중요 한 데이터를 보낸 클라이언트를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-108">No API can prevent a client from sending sensitive data on the first request.</span></span>

> [!WARNING]
> <span data-ttu-id="84b7c-109">수행할 **되지** 사용 하 여 [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) 중요 한 정보를 수신 하는 Web Api에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-109">Do **not** use [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) on Web APIs that receive sensitive information.</span></span> <span data-ttu-id="84b7c-110">`RequireHttpsAttribute` 브라우저는 HTTP에서 HTTPS로 리디렉션하 HTTP 상태 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-110">`RequireHttpsAttribute` uses HTTP status codes to redirect browsers from HTTP to HTTPS.</span></span> <span data-ttu-id="84b7c-111">API 클라이언트 이해 하지 못하거나 HTTP에서 HTTPS로 리디렉션 준수 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-111">API clients may not understand or obey redirects from HTTP to HTTPS.</span></span> <span data-ttu-id="84b7c-112">이러한 클라이언트는 HTTP를 통해 정보를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-112">Such clients may send information over HTTP.</span></span> <span data-ttu-id="84b7c-113">Web Api을 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-113">Web APIs should either:</span></span>
>
> * <span data-ttu-id="84b7c-114">HTTP에서 수신 대기할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-114">Not listen on HTTP.</span></span>
> * <span data-ttu-id="84b7c-115">상태 코드 400 (잘못 된 요청)를 사용 하 여 연결을 닫고 요청을 제공 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="84b7c-115">Close the connection with status code 400 (Bad Request) and not serve the request.</span></span>

<a name="require"></a>
## <a name="require-https"></a><span data-ttu-id="84b7c-116">HTTPS가 필요</span><span class="sxs-lookup"><span data-stu-id="84b7c-116">Require HTTPS</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="84b7c-117">모든 프로덕션 ASP.NET Core 웹 앱 호출을 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-117">We recommend all production ASP.NET Core web apps call:</span></span>

* <span data-ttu-id="84b7c-118">HTTPS 리디렉션을 미들웨어 ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) HTTPS로 모든 HTTP 요청을 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-118">The HTTPS Redirection Middleware ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) to redirect all HTTP requests to HTTPS.</span></span>
* <span data-ttu-id="84b7c-119">[UseHsts](#hsts), HTTP 엄격한 전송 보안 (HSTS) 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-119">[UseHsts](#hsts), HTTP Strict Transport Security Protocol (HSTS).</span></span>

### <a name="usehttpsredirection"></a><span data-ttu-id="84b7c-120">UseHttpsRedirection</span><span class="sxs-lookup"><span data-stu-id="84b7c-120">UseHttpsRedirection</span></span>

<span data-ttu-id="84b7c-121">다음 코드 호출 `UseHttpsRedirection` 에 `Startup` 클래스:</span><span class="sxs-lookup"><span data-stu-id="84b7c-121">The following code calls `UseHttpsRedirection` in the `Startup` class:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=13)]

<span data-ttu-id="84b7c-122">위의 강조 표시 된 코드:</span><span class="sxs-lookup"><span data-stu-id="84b7c-122">The preceding highlighted code:</span></span>

* <span data-ttu-id="84b7c-123">기본값을 사용 하 여 [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) (`Status307TemporaryRedirect`).</span><span class="sxs-lookup"><span data-stu-id="84b7c-123">Uses the default [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) (`Status307TemporaryRedirect`).</span></span>
* <span data-ttu-id="84b7c-124">기본값을 사용 하 여 [HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport) 의해 재정의 되지 않는 (null)은 `ASPNETCORE_HTTPS_PORT` 환경 변수 또는 [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-124">Uses the default [HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport) (null) unless overridden by the `ASPNETCORE_HTTPS_PORT` environment variable or [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature).</span></span>

> [!WARNING] 
><span data-ttu-id="84b7c-125">포트를 HTTPS로 리디렉션하는 미들웨어에 대 한 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-125">A port must be available for the middleware to redirect to HTTPS.</span></span> <span data-ttu-id="84b7c-126">사용 가능한 포트가 없는 경우 HTTPS로 리디렉션 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-126">If no port is available, redirection to HTTPS does not occur.</span></span> <span data-ttu-id="84b7c-127">다음 설정 중 하나에서 HTTPS 포트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-127">The HTTPS port can be specified by any of the following setting:</span></span>
> 
>* `HttpsRedirectionOptions.HttpsPort` 
>* <span data-ttu-id="84b7c-128">`ASPNETCORE_HTTPS_PORT` 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-128">The `ASPNETCORE_HTTPS_PORT` environment variable.</span></span> 
>* <span data-ttu-id="84b7c-129">HTTPS url 사용 하 여 개발에서 *launchsettings.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-129">In development, an HTTPS url in *launchsettings.json*.</span></span> 
>* <span data-ttu-id="84b7c-130">Kestrel 또는 HttpSys에 직접 구성 하는 HTTPS url입니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-130">An HTTPS url configured directly on Kestrel or HttpSys.</span></span> 

<span data-ttu-id="84b7c-131">다음 코드 호출을 강조 표시 [AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection) 미들웨어 옵션을 구성 하려면:</span><span class="sxs-lookup"><span data-stu-id="84b7c-131">The following highlighted code calls [AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection) to configure middleware options:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=14-99)]

<span data-ttu-id="84b7c-132">호출 `AddHttpsRedirection` 값을 변경 하는 데 필요한 전용인 ` HttpsPort` 또는 ` RedirectStatusCode`;</span><span class="sxs-lookup"><span data-stu-id="84b7c-132">Calling `AddHttpsRedirection` is only necessary to change the values of ` HttpsPort` or ` RedirectStatusCode`;</span></span>

<span data-ttu-id="84b7c-133">위의 강조 표시 된 코드:</span><span class="sxs-lookup"><span data-stu-id="84b7c-133">The preceding highlighted code:</span></span>

* <span data-ttu-id="84b7c-134">집합 [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) 에 `Status307TemporaryRedirect`, 기본 값입니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-134">Sets [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) to `Status307TemporaryRedirect`, which is the default value.</span></span>
* <span data-ttu-id="84b7c-135">HTTPS 포트를 5001로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-135">Sets the HTTPS port to 5001.</span></span> <span data-ttu-id="84b7c-136">기본값은 443입니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-136">The default value is 443.</span></span>

<span data-ttu-id="84b7c-137">다음과 같은 메커니즘 포트를 자동으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-137">The following mechanisms set the port automatically:</span></span>

* <span data-ttu-id="84b7c-138">미들웨어를 통해 포트를 검색할 수 있습니다 [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature) 다음 조건이 적용 되는 경우:</span><span class="sxs-lookup"><span data-stu-id="84b7c-138">The middleware can discover the ports via [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature) when the following conditions apply:</span></span>

   * <span data-ttu-id="84b7c-139">Kestrel 또는 HTTPS 끝점으로 직접 사용 됩니다 (Visual Studio Code의 디버거를 사용 하 여 앱을 실행 하도 적용 됨).</span><span class="sxs-lookup"><span data-stu-id="84b7c-139">Kestrel or HTTP.sys is used directly with HTTPS endpoints (also applies to running the app with Visual Studio Code's debugger).</span></span>
   * <span data-ttu-id="84b7c-140">만 **하나의 HTTPS 포트** 앱에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-140">Only **one HTTPS port** is used by the app.</span></span>

* <span data-ttu-id="84b7c-141">Visual Studio는 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-141">Visual Studio is used:</span></span>
   * <span data-ttu-id="84b7c-142">IIS Express에 HTTPS를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-142">IIS Express has HTTPS enabled.</span></span>
   * <span data-ttu-id="84b7c-143">*launchSettings.json* 설정의 `sslPort` IIS Express에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-143">*launchSettings.json* sets the `sslPort` for IIS Express.</span></span>

> [!NOTE]
> <span data-ttu-id="84b7c-144">앱 (예를 들어, IIS, IIS Express) 역방향 프록시 뒤에 실행 될 때 `IServerAddressesFeature` 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-144">When an app is run behind a reverse proxy (for example, IIS, IIS Express), `IServerAddressesFeature` isn't available.</span></span> <span data-ttu-id="84b7c-145">포트를 수동으로 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-145">The port must be manually configured.</span></span> <span data-ttu-id="84b7c-146">포트 설정 되지 않은 경우 요청을 리디렉션할 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-146">When the port isn't set, requests aren't redirected.</span></span>

<span data-ttu-id="84b7c-147">설정 하 여 포트를 구성할 수 있습니다 합니다 [https_port 웹 호스트 구성 설정을](xref:fundamentals/host/web-host#https-port):</span><span class="sxs-lookup"><span data-stu-id="84b7c-147">The port can be configured by setting the [https_port Web Host configuration setting](xref:fundamentals/host/web-host#https-port):</span></span>

<span data-ttu-id="84b7c-148">**키**: https_port</span><span class="sxs-lookup"><span data-stu-id="84b7c-148">**Key**: https_port</span></span>  
<span data-ttu-id="84b7c-149">**형식**: *string*</span><span class="sxs-lookup"><span data-stu-id="84b7c-149">**Type**: *string*</span></span>  
<span data-ttu-id="84b7c-150">**기본**: 기본값이 설정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-150">**Default**: A default value isn't set.</span></span>  
<span data-ttu-id="84b7c-151">**설정 방법**: `UseSetting`</span><span class="sxs-lookup"><span data-stu-id="84b7c-151">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="84b7c-152">**환경 변수**: `<PREFIX_>HTTPS_PORT` (접두사는 `ASPNETCORE_` 웹 호스트를 사용 하는 경우입니다.)</span><span class="sxs-lookup"><span data-stu-id="84b7c-152">**Environment variable**: `<PREFIX_>HTTPS_PORT` (The prefix is `ASPNETCORE_` when using the Web Host.)</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("https_port", "8080")
```

> [!NOTE]
> <span data-ttu-id="84b7c-153">URL을 설정 하 여 포트를 직접 구성할 수 있습니다는 `ASPNETCORE_URLS` 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-153">The port can be configured indirectly by setting the URL with the `ASPNETCORE_URLS` environment variable.</span></span> <span data-ttu-id="84b7c-154">환경 변수를 구성 서버에을 수행한 후 미들웨어 직접 검색 되지 HTTPS 포트를 통해 `IServerAddressesFeature`합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-154">The environment variable configures the server, and then the middleware indirectly discovers the HTTPS port via `IServerAddressesFeature`.</span></span>

<span data-ttu-id="84b7c-155">경우 포트가 없는 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-155">If no port is set:</span></span>

* <span data-ttu-id="84b7c-156">요청을 리디렉션할 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-156">Requests aren't redirected.</span></span>
* <span data-ttu-id="84b7c-157">미들웨어 "리디렉션에 대 한 https 포트를 확인 하지 못했습니다." 경고를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-157">The middleware logs the warning "Failed to determine the https port for redirect."</span></span>

> [!NOTE]
> <span data-ttu-id="84b7c-158">HTTPS 리디렉션을 미들웨어를 사용 하는 대신 (`UseHttpsRedirection`) URL 재작성 미들웨어를 사용 하는 것 (`AddRedirectToHttps`).</span><span class="sxs-lookup"><span data-stu-id="84b7c-158">An alternative to using HTTPS Redirection Middleware (`UseHttpsRedirection`) is to use URL Rewriting Middleware (`AddRedirectToHttps`).</span></span> <span data-ttu-id="84b7c-159">`AddRedirectToHttps` 리디렉션 실행 될 때 상태 코드 및 포트를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-159">`AddRedirectToHttps` can also set the status code and port when the redirect is executed.</span></span> <span data-ttu-id="84b7c-160">자세한 내용은 [URL 재작성 미들웨어](xref:fundamentals/url-rewriting)합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-160">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span>
>
> <span data-ttu-id="84b7c-161">추가 리디렉션 규칙을 요구 하지 않고 HTTPS로 리디렉션, 하는 경우 HTTPS 리디렉션을 미들웨어를 사용 하는 것이 좋습니다 (`UseHttpsRedirection`)이이 항목에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-161">When redirecting to HTTPS without the requirement for additional redirect rules, we recommend using HTTPS Redirection Middleware (`UseHttpsRedirection`) described in this topic.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.1"

<span data-ttu-id="84b7c-162">합니다 [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) HTTPS가 필요 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-162">The [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) is used to require HTTPS.</span></span> <span data-ttu-id="84b7c-163">`[RequireHttpsAttribute]` 컨트롤러 또는 메서드를 데코레이팅 할 수 있습니다 또는 전체적으로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-163">`[RequireHttpsAttribute]` can decorate controllers or methods, or can be applied globally.</span></span> <span data-ttu-id="84b7c-164">특성을 전역적으로 적용 하려면 다음 코드를 추가 합니다 `ConfigureServices` 에서 `Startup`:</span><span class="sxs-lookup"><span data-stu-id="84b7c-164">To apply the attribute globally, add the following code to `ConfigureServices` in `Startup`:</span></span>

[!code-csharp[](~/security/authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]

<span data-ttu-id="84b7c-165">위의 강조 표시된 코드는 모든 요청에 `HTTPS` 를 사용하도록 강제하며, 그 결과 HTTP 요청은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-165">The preceding highlighted code requires all requests use `HTTPS`; therefore, HTTP requests are ignored.</span></span> <span data-ttu-id="84b7c-166">다음에 강조 표시된 코드는 모든 HTTP 요청을 HTTPS로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-166">The following highlighted code redirects all HTTP requests to HTTPS:</span></span>

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]

<span data-ttu-id="84b7c-167">자세한 내용은 [URL 재작성 미들웨어](xref:fundamentals/url-rewriting)합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-167">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span> <span data-ttu-id="84b7c-168">또한 미들웨어 리디렉션 실행 될 때 상태 코드 또는 상태 코드와 포트를 설정 하려면 앱을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-168">The middleware also permits the app to set the status code or the status code and the port when the redirect is executed.</span></span>

<span data-ttu-id="84b7c-169">전역으로 HTTPS를 요구하는 것이 보안상 가장 안전한 모범 사례입니다 (`options.Filters.Add(new RequireHttpsAttribute());`).</span><span class="sxs-lookup"><span data-stu-id="84b7c-169">Requiring HTTPS globally (`options.Filters.Add(new RequireHttpsAttribute());`) is a security best practice.</span></span> <span data-ttu-id="84b7c-170">적용 된 `[RequireHttps]` 모든 컨트롤러/Razor 페이지에는 특성에 전역적으로 HTTPS를 요구 하는 것 만큼 안전로 간주 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-170">Applying the `[RequireHttps]` attribute to all controllers/Razor Pages isn't considered as secure as requiring HTTPS globally.</span></span> <span data-ttu-id="84b7c-171">보장할 수 없습니다는 `[RequireHttps]` 새 컨트롤러 및 Razor 페이지는 추가 특성이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-171">You can't guarantee the `[RequireHttps]` attribute is applied when new controllers and Razor Pages are added.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="hsts"></a>
## <a name="http-strict-transport-security-protocol-hsts"></a><span data-ttu-id="84b7c-172">HTTP 엄격한 전송 보안 프로토콜 (HSTS)</span><span class="sxs-lookup"><span data-stu-id="84b7c-172">HTTP Strict Transport Security Protocol (HSTS)</span></span>

<span data-ttu-id="84b7c-173">당 [OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project)하십시오 [HTTP 엄격한 전송 보안 (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) 응답 헤더를 사용 하 여 웹 앱에서 지정 하는 옵트인 보안 향상 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-173">Per [OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project), [HTTP Strict Transport Security (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) is an opt-in security enhancement that's specified by a web app through the use of a response header.</span></span> <span data-ttu-id="84b7c-174">경우는 [HSTS를 지 원하는 브라우저](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet#Browser_Support) 이 헤더를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-174">When a [browser that supports HSTS](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet#Browser_Support) receives this header:</span></span>

* <span data-ttu-id="84b7c-175">브라우저에는 모든 통신이 HTTP를 통해 보낼 수 없는 도메인에 대 한 구성을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-175">The browser stores configuration for the domain that prevents sending any communication over HTTP.</span></span> <span data-ttu-id="84b7c-176">브라우저 강제로 HTTPS를 통해 모든 통신을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-176">The browser forces all communication over HTTPS.</span></span>
* <span data-ttu-id="84b7c-177">브라우저에서 신뢰할 수 없거나 잘못 된 인증서를 사용 하 여 사용자를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-177">The browser prevents the user from using untrusted or invalid certificates.</span></span> <span data-ttu-id="84b7c-178">브라우저 사용자가 일시적으로 이러한 인증서를 신뢰 하는 프롬프트를 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-178">The browser disables prompts that allow a user to temporarily trust such a certificate.</span></span>

<span data-ttu-id="84b7c-179">HSTS는 클라이언트에서 적용 하기 때문에 몇 가지 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-179">Because HSTS is enforced by the client it has some limitations:</span></span>

* <span data-ttu-id="84b7c-180">클라이언트는 HSTS를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-180">The client must support HSTS.</span></span>
* <span data-ttu-id="84b7c-181">HSTS는 HSTS 정책을 설정 하려면 하나 이상의 성공적인 HTTPS 요청에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-181">HSTS requires at least one successful HTTPS request to establish the HSTS policy.</span></span>
* <span data-ttu-id="84b7c-182">응용 프로그램이 모든 HTTP 요청을 확인 하 고 리디렉션 하거나 HTTP 요청을 거부 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-182">The application must check every HTTP request and redirect or reject the HTTP request.</span></span>

<span data-ttu-id="84b7c-183">ASP.NET Core 2.1 이상을 사용 하 여 HSTS를 구현 합니다 `UseHsts` 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="84b7c-183">ASP.NET Core 2.1 or later implements HSTS with the `UseHsts` extension method.</span></span> <span data-ttu-id="84b7c-184">다음 코드 호출 `UseHsts` 에 앱이 없는 경우 [개발 모드](xref:fundamentals/environments):</span><span class="sxs-lookup"><span data-stu-id="84b7c-184">The following code calls `UseHsts` when the app isn't in [development mode](xref:fundamentals/environments):</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=10)]

<span data-ttu-id="84b7c-185">`UseHsts` 권장 되지 않습니다 개발에서 HSTS 설정이 항상 캐시할 수 있기 때문에 브라우저에서.</span><span class="sxs-lookup"><span data-stu-id="84b7c-185">`UseHsts` isn't recommended in development because the HSTS settings are highly cacheable by browsers.</span></span> <span data-ttu-id="84b7c-186">기본적으로 `UseHsts` 로컬 루프백 주소를 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-186">By default, `UseHsts` excludes the local loopback address.</span></span>

<span data-ttu-id="84b7c-187">처음에 대 한 HTTPS를 구현 하는 프로덕션 환경에서는 초기 HSTS 값을 작은 값으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-187">For production environments implementing HTTPS for the first time, set the initial HSTS value to a small value.</span></span> <span data-ttu-id="84b7c-188">값을 설정할 시간에서 전혀 보다 하루를 HTTP로 HTTPS 인프라를 되돌려야 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="84b7c-188">Set the value from hours to no more than a single day in case you need to revert the HTTPS infrastructure to HTTP.</span></span> <span data-ttu-id="84b7c-189">HTTPS 구성의 유지 가능성에 확신한 후 늘릴 HSTS 최대 처리 기간 값 자주 사용 되는 값은 1 년입니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-189">After you're confident in the sustainability of the HTTPS configuration, increase the HSTS max-age value; a commonly used value is one year.</span></span> 

<span data-ttu-id="84b7c-190">다음 예를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="84b7c-190">The following code:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=5-12)]

* <span data-ttu-id="84b7c-191">Strict-전송-보안 헤더의 미리 로드 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-191">Sets the preload parameter of the Strict-Transport-Security header.</span></span> <span data-ttu-id="84b7c-192">Preload의 일부가 아닌 합니다 [RFC HSTS 사양](https://tools.ietf.org/html/rfc6797), 있지만 HSTS 새로 설치할 때 사이트를 미리 로드 하려면 웹 브라우저에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-192">Preload isn't part of the [RFC HSTS specification](https://tools.ietf.org/html/rfc6797), but is supported by web browsers to preload HSTS sites on fresh install.</span></span> <span data-ttu-id="84b7c-193">자세한 내용은 [https://hstspreload.org/](https://hstspreload.org/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84b7c-193">See [https://hstspreload.org/](https://hstspreload.org/) for more information.</span></span>
* <span data-ttu-id="84b7c-194">사용 하도록 설정 [includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2), 호스트 하위 도메인에 HSTS 정책을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-194">Enables [includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2), which applies the HSTS policy to Host subdomains.</span></span> 
* <span data-ttu-id="84b7c-195">60 일로 Strict-전송-보안 헤더의 최대 처리 기간 매개 변수를 명시적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-195">Explicitly sets the max-age parameter of the Strict-Transport-Security header to 60 days.</span></span> <span data-ttu-id="84b7c-196">설정 하지 않으면 기본값은 30 일입니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-196">If not set, defaults to 30 days.</span></span> <span data-ttu-id="84b7c-197">참조 된 [최대 처리 기간 지시문](https://tools.ietf.org/html/rfc6797#section-6.1.1) 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-197">See the [max-age directive](https://tools.ietf.org/html/rfc6797#section-6.1.1) for more information.</span></span>
* <span data-ttu-id="84b7c-198">추가 `example.com` 를 제외 하는 호스트의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-198">Adds `example.com` to the list of hosts to exclude.</span></span>

<span data-ttu-id="84b7c-199">`UseHsts` 다음 루프백 호스트를 제외:</span><span class="sxs-lookup"><span data-stu-id="84b7c-199">`UseHsts` excludes the following loopback hosts:</span></span>

* <span data-ttu-id="84b7c-200">`localhost` : IPv4 루프백 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-200">`localhost` : The IPv4 loopback address.</span></span>
* <span data-ttu-id="84b7c-201">`127.0.0.1` : IPv4 루프백 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-201">`127.0.0.1` : The IPv4 loopback address.</span></span>
* <span data-ttu-id="84b7c-202">`[::1]` : IPv6 루프백 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-202">`[::1]` : The IPv6 loopback address.</span></span>

<span data-ttu-id="84b7c-203">앞의 예제에는 추가 호스트를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-203">The preceding example shows how to add additional hosts.</span></span>
::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="https"></a>
## <a name="opt-out-of-https-on-project-creation"></a><span data-ttu-id="84b7c-204">옵트아웃 https 프로젝트 생성 시</span><span class="sxs-lookup"><span data-stu-id="84b7c-204">Opt-out of HTTPS on project creation</span></span>

<span data-ttu-id="84b7c-205">ASP.NET Core 2.1 이상 웹 응용 프로그램 템플릿 (Visual Studio 또는 dotnet 명령 줄)에서 사용 하도록 설정 [HTTPS 간의 리디렉션으로](#require) 하 고 [HSTS](#hsts)합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-205">The ASP.NET Core 2.1 or later web application templates (from Visual Studio or the dotnet command line) enable [HTTPS redirection](#require) and [HSTS](#hsts).</span></span> <span data-ttu-id="84b7c-206">HTTPS를 요구 하지 않는 배포에 대 한 있습니다 옵트아웃할 수 https입니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-206">For deployments that don't require HTTPS, you can opt-out of HTTPS.</span></span> <span data-ttu-id="84b7c-207">예를 들어, 일부 백 엔드 서비스는 HTTPS 처리 되 고 외부 가장자리에 HTTPS를 사용 하 여 각 노드에서 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-207">For example, some backend services where HTTPS is being handled externally at the edge, using HTTPS at each node isn't needed.</span></span>

<span data-ttu-id="84b7c-208">옵트아웃 하려면 https:</span><span class="sxs-lookup"><span data-stu-id="84b7c-208">To opt-out of HTTPS:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="84b7c-209">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="84b7c-209">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="84b7c-210">선택 취소 합니다 **HTTPS에 대 한 구성** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-210">Uncheck the **Configure for HTTPS** checkbox.</span></span>

![엔터티 다이어그램](enforcing-ssl/_static/out.png)

#   <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="84b7c-212">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="84b7c-212">.NET Core CLI</span></span>](#tab/netcore-cli) 

<span data-ttu-id="84b7c-213">`--no-https` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-213">Use the `--no-https` option.</span></span> <span data-ttu-id="84b7c-214">예</span><span class="sxs-lookup"><span data-stu-id="84b7c-214">For example</span></span>

```console
dotnet new webapp --no-https
```

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

---

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="how-to-set-up-a-developer-certificate-for-docker"></a><span data-ttu-id="84b7c-215">Docker에 대 한 개발자 인증서를 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="84b7c-215">How to set up a developer certificate for Docker</span></span>

<span data-ttu-id="84b7c-216">참조 [이 GitHub 문제](https://github.com/aspnet/Docs/issues/6199)합니다.</span><span class="sxs-lookup"><span data-stu-id="84b7c-216">See [this GitHub issue](https://github.com/aspnet/Docs/issues/6199).</span></span>

::: moniker-end

## <a name="additional-information"></a><span data-ttu-id="84b7c-217">추가 정보</span><span class="sxs-lookup"><span data-stu-id="84b7c-217">Additional information</span></span>

* [<span data-ttu-id="84b7c-218">OWASP HSTS 브라우저 지원</span><span class="sxs-lookup"><span data-stu-id="84b7c-218">OWASP HSTS browser support</span></span>](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet#Browser_Support)
