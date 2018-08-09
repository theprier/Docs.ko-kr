---
title: ASP.NET Core에서 HTTPS 적용
author: rick-anderson
description: 웹 앱을 ASP.NET Core에서 HTTPS/TLS를 요구 하는 방법에 보여 줍니다.
ms.author: riande
ms.date: 2/9/2018
uid: security/enforcing-ssl
ms.openlocfilehash: 3bea8661e17fec5128e822d98741d1f8ed7434e5
ms.sourcegitcommit: 028ad28c546de706ace98066c76774de33e4ad20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39655500"
---
# <a name="enforce-https-in-aspnet-core"></a><span data-ttu-id="e51eb-103">ASP.NET Core에서 HTTPS 적용</span><span class="sxs-lookup"><span data-stu-id="e51eb-103">Enforce HTTPS in ASP.NET Core</span></span>

<span data-ttu-id="e51eb-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="e51eb-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="e51eb-105">이 문서에서는 다음과 같은 내용을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-105">This document shows how to:</span></span>

* <span data-ttu-id="e51eb-106">모든 요청에 대 한 HTTPS가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-106">Require HTTPS for all requests.</span></span>
* <span data-ttu-id="e51eb-107">모든 HTTP 요청을 HTTPS로 리디렉션하는 방법.</span><span class="sxs-lookup"><span data-stu-id="e51eb-107">Redirect all HTTP requests to HTTPS.</span></span>

> [!WARNING]
> <span data-ttu-id="e51eb-108">수행할 **되지** 사용 하 여 [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) 중요 한 정보를 수신 하는 Web Api에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-108">Do **not** use [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) on Web APIs that receive sensitive information.</span></span> <span data-ttu-id="e51eb-109">`RequireHttpsAttribute` 브라우저는 HTTP에서 HTTPS로 리디렉션하 HTTP 상태 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-109">`RequireHttpsAttribute` uses HTTP status codes to redirect browsers from HTTP to HTTPS.</span></span> <span data-ttu-id="e51eb-110">API 클라이언트 이해 하지 못하거나 HTTP에서 HTTPS로 리디렉션 준수 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-110">API clients may not understand or obey redirects from HTTP to HTTPS.</span></span> <span data-ttu-id="e51eb-111">이러한 클라이언트는 HTTP를 통해 정보를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-111">Such clients may send information over HTTP.</span></span> <span data-ttu-id="e51eb-112">Web Api을 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-112">Web APIs should either:</span></span>
>
> * <span data-ttu-id="e51eb-113">HTTP에서 수신 대기할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-113">Not listen on HTTP.</span></span>
> * <span data-ttu-id="e51eb-114">상태 코드 400 (잘못 된 요청)를 사용 하 여 연결을 닫고 요청을 제공 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="e51eb-114">Close the connection with status code 400 (Bad Request) and not serve the request.</span></span>

<a name="require"></a>
## <a name="require-https"></a><span data-ttu-id="e51eb-115">HTTPS가 필요</span><span class="sxs-lookup"><span data-stu-id="e51eb-115">Require HTTPS</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="e51eb-116">모든 ASP.NET Core 웹 앱 HTTPS 리디렉션을 미들웨어를 호출 하는 것이 좋습니다 ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) HTTPS로 모든 HTTP 요청을 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-116">We recommend all ASP.NET Core web apps call HTTPS Redirection Middleware ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) to redirect all HTTP requests to HTTPS.</span></span>

<span data-ttu-id="e51eb-117">다음 코드 호출 `UseHttpsRedirection` 에 `Startup` 클래스:</span><span class="sxs-lookup"><span data-stu-id="e51eb-117">The following code calls `UseHttpsRedirection` in the `Startup` class:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=13)]

<span data-ttu-id="e51eb-118">위의 강조 표시 된 코드:</span><span class="sxs-lookup"><span data-stu-id="e51eb-118">The preceding highlighted code:</span></span>

* <span data-ttu-id="e51eb-119">기본값을 사용 하 여 [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) (`Status307TemporaryRedirect`).</span><span class="sxs-lookup"><span data-stu-id="e51eb-119">Uses the default [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) (`Status307TemporaryRedirect`).</span></span> <span data-ttu-id="e51eb-120">프로덕션 앱에서 호출 해야 [UseHsts](#hsts)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-120">Production apps should call [UseHsts](#hsts).</span></span>
* <span data-ttu-id="e51eb-121">기본값을 사용 하 여 [HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport) (443).</span><span class="sxs-lookup"><span data-stu-id="e51eb-121">Uses the default [HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport) (443).</span></span>

<span data-ttu-id="e51eb-122">다음 코드 호출 [AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection) 미들웨어 옵션을 구성 하려면:</span><span class="sxs-lookup"><span data-stu-id="e51eb-122">The following code calls [AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection) to configure middleware options:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=14-99)]

<span data-ttu-id="e51eb-123">위의 강조 표시 된 코드:</span><span class="sxs-lookup"><span data-stu-id="e51eb-123">The preceding highlighted code:</span></span>

* <span data-ttu-id="e51eb-124">집합 [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) 에 `Status307TemporaryRedirect`, 기본 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-124">Sets [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) to `Status307TemporaryRedirect`, which is the default value.</span></span> <span data-ttu-id="e51eb-125">프로덕션 앱에서 호출 해야 [UseHsts](#hsts)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-125">Production apps should call [UseHsts](#hsts).</span></span>
* <span data-ttu-id="e51eb-126">HTTPS 포트를 5001로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-126">Sets the HTTPS port to 5001.</span></span> <span data-ttu-id="e51eb-127">기본값은 443입니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-127">The default value is 443.</span></span>

<span data-ttu-id="e51eb-128">다음과 같은 메커니즘 포트를 자동으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-128">The following mechanisms set the port automatically:</span></span>

* <span data-ttu-id="e51eb-129">미들웨어를 통해 포트를 검색할 수 있습니다 [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature) 다음 조건이 적용 되는 경우:</span><span class="sxs-lookup"><span data-stu-id="e51eb-129">The middleware can discover the ports via [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature) when the following conditions apply:</span></span>
  - <span data-ttu-id="e51eb-130">Kestrel 또는 HTTPS 끝점으로 직접 사용 됩니다 (Visual Studio Code의 디버거를 사용 하 여 앱을 실행 하도 적용 됨).</span><span class="sxs-lookup"><span data-stu-id="e51eb-130">Kestrel or HTTP.sys is used directly with HTTPS endpoints (also applies to running the app with Visual Studio Code's debugger).</span></span>
  - <span data-ttu-id="e51eb-131">만 **하나의 HTTPS 포트** 앱에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-131">Only **one HTTPS port** is used by the app.</span></span>
* <span data-ttu-id="e51eb-132">Visual Studio는 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-132">Visual Studio is used:</span></span>
  - <span data-ttu-id="e51eb-133">IIS Express에 HTTPS를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-133">IIS Express has HTTPS enabled.</span></span>
  - <span data-ttu-id="e51eb-134">*launchSettings.json* 설정의 `sslPort` IIS Express에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-134">*launchSettings.json* sets the `sslPort` for IIS Express.</span></span>

> [!NOTE]
> <span data-ttu-id="e51eb-135">앱 (예를 들어, IIS, IIS Express) 역방향 프록시 뒤에 실행 될 때 `IServerAddressesFeature` 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-135">When an app is run behind a reverse proxy (for example, IIS, IIS Express), `IServerAddressesFeature` isn't available.</span></span> <span data-ttu-id="e51eb-136">포트를 수동으로 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-136">The port must be manually configured.</span></span> <span data-ttu-id="e51eb-137">포트 설정 되지 않은 경우 요청을 리디렉션할 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-137">When the port isn't set, requests aren't redirected.</span></span>

<span data-ttu-id="e51eb-138">설정 하 여 포트를 구성할 수 있습니다 합니다 [https_port 웹 호스트 구성 설정을](xref:fundamentals/host/web-host#https-port):</span><span class="sxs-lookup"><span data-stu-id="e51eb-138">The port can be configured by setting the [https_port Web Host configuration setting](xref:fundamentals/host/web-host#https-port):</span></span>

<span data-ttu-id="e51eb-139">**키**: https_port **형식**: ‘문자열’
**기본값**: 기본값이 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-139">**Key**: https_port **Type**: *string*
**Default**: A default value isn't set.</span></span>
<span data-ttu-id="e51eb-140">**사용 하 여 설정할**: `UseSetting` 
 **환경 변수**: `<PREFIX_>HTTPS_PORT` (접두사는 `ASPNETCORE_` 웹 호스트를 사용 하는 경우입니다.)</span><span class="sxs-lookup"><span data-stu-id="e51eb-140">**Set using**: `UseSetting`
**Environment variable**: `<PREFIX_>HTTPS_PORT` (The prefix is `ASPNETCORE_` when using the Web Host.)</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("https_port", "8080")
```

> [!NOTE]
> <span data-ttu-id="e51eb-141">URL을 설정 하 여 포트를 직접 구성할 수 있습니다는 `ASPNETCORE_URLS` 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-141">The port can be configured indirectly by setting the URL with the `ASPNETCORE_URLS` environment variable.</span></span> <span data-ttu-id="e51eb-142">환경 변수를 구성 서버에을 수행한 후 미들웨어 직접 검색 되지 HTTPS 포트를 통해 `IServerAddressesFeature`합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-142">The environment variable configures the server, and then the middleware indirectly discovers the HTTPS port via `IServerAddressesFeature`.</span></span>

<span data-ttu-id="e51eb-143">경우 포트가 없는 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-143">If no port is set:</span></span>

* <span data-ttu-id="e51eb-144">요청을 리디렉션할 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-144">Requests aren't redirected.</span></span>
* <span data-ttu-id="e51eb-145">미들웨어는 경고를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-145">The middleware logs a warning.</span></span>

> [!NOTE]
> <span data-ttu-id="e51eb-146">HTTPS 리디렉션을 미들웨어를 사용 하는 대신 (`UseHttpsRedirection`) URL 재작성 미들웨어를 사용 하는 것 (`AddRedirectToHttps`).</span><span class="sxs-lookup"><span data-stu-id="e51eb-146">An alternative to using HTTPS Redirection Middleware (`UseHttpsRedirection`) is to use URL Rewriting Middleware (`AddRedirectToHttps`).</span></span> <span data-ttu-id="e51eb-147">`AddRedirectToHttps` 리디렉션 실행 될 때 상태 코드 및 포트를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-147">`AddRedirectToHttps` can also set the status code and port when the redirect is executed.</span></span> <span data-ttu-id="e51eb-148">자세한 내용은 [URL 재작성 미들웨어](xref:fundamentals/url-rewriting)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-148">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span>
>
> <span data-ttu-id="e51eb-149">추가 리디렉션 규칙을 요구 하지 않고 HTTPS로 리디렉션, 하는 경우 HTTPS 리디렉션을 미들웨어를 사용 하는 것이 좋습니다 (`UseHttpsRedirection`)이이 항목에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-149">When redirecting to HTTPS without the requirement for additional redirect rules, we recommend using HTTPS Redirection Middleware (`UseHttpsRedirection`) described in this topic.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.1"

<span data-ttu-id="e51eb-150">합니다 [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) HTTPS가 필요 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-150">The [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) is used to require HTTPS.</span></span> <span data-ttu-id="e51eb-151">`[RequireHttpsAttribute]` 컨트롤러 또는 메서드를 데코레이팅 할 수 있습니다 또는 전체적으로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-151">`[RequireHttpsAttribute]` can decorate controllers or methods, or can be applied globally.</span></span> <span data-ttu-id="e51eb-152">특성을 전역적으로 적용 하려면 다음 코드를 추가 합니다 `ConfigureServices` 에서 `Startup`:</span><span class="sxs-lookup"><span data-stu-id="e51eb-152">To apply the attribute globally, add the following code to `ConfigureServices` in `Startup`:</span></span>

[!code-csharp[](~/security/authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]

<span data-ttu-id="e51eb-153">위의 강조 표시된 코드는 모든 요청에 `HTTPS` 를 사용하도록 강제하며, 그 결과 HTTP 요청은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-153">The preceding highlighted code requires all requests use `HTTPS`; therefore, HTTP requests are ignored.</span></span> <span data-ttu-id="e51eb-154">다음에 강조 표시된 코드는 모든 HTTP 요청을 HTTPS로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-154">The following highlighted code redirects all HTTP requests to HTTPS:</span></span>

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]

<span data-ttu-id="e51eb-155">자세한 내용은 [URL 재작성 미들웨어](xref:fundamentals/url-rewriting)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-155">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span> <span data-ttu-id="e51eb-156">또한 미들웨어 리디렉션 실행 될 때 상태 코드 또는 상태 코드와 포트를 설정 하려면 앱을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-156">The middleware also permits the app to set the status code or the status code and the port when the redirect is executed.</span></span>

<span data-ttu-id="e51eb-157">전역으로 HTTPS를 요구하는 것이 보안상 가장 안전한 모범 사례입니다 (`options.Filters.Add(new RequireHttpsAttribute());`).</span><span class="sxs-lookup"><span data-stu-id="e51eb-157">Requiring HTTPS globally (`options.Filters.Add(new RequireHttpsAttribute());`) is a security best practice.</span></span> <span data-ttu-id="e51eb-158">적용 된 `[RequireHttps]` 모든 컨트롤러/Razor 페이지에는 특성에 전역적으로 HTTPS를 요구 하는 것 만큼 안전로 간주 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-158">Applying the `[RequireHttps]` attribute to all controllers/Razor Pages isn't considered as secure as requiring HTTPS globally.</span></span> <span data-ttu-id="e51eb-159">보장할 수 없습니다는 `[RequireHttps]` 새 컨트롤러 및 Razor 페이지는 추가 특성이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-159">You can't guarantee the `[RequireHttps]` attribute is applied when new controllers and Razor Pages are added.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="hsts"></a>
## <a name="http-strict-transport-security-protocol-hsts"></a><span data-ttu-id="e51eb-160">HTTP 엄격한 전송 보안 프로토콜 (HSTS)</span><span class="sxs-lookup"><span data-stu-id="e51eb-160">HTTP Strict Transport Security Protocol (HSTS)</span></span>

<span data-ttu-id="e51eb-161">당 [OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project)하십시오 [HTTP 엄격한 전송 보안 (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) 응답 헤더를 사용 하 여 웹 앱에서 지정 하는 옵트인 보안 향상 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-161">Per [OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project), [HTTP Strict Transport Security (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) is an opt-in security enhancement that's specified by a web app through the use of a response header.</span></span> <span data-ttu-id="e51eb-162">경우 HSTS를 지 원하는 브라우저는이 헤더를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-162">When a browser that supports HSTS receives this header:</span></span>

* <span data-ttu-id="e51eb-163">브라우저에는 모든 통신이 HTTP를 통해 보낼 수 없는 도메인에 대 한 구성을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-163">The browser stores configuration for the domain that prevents sending any communication over HTTP.</span></span> <span data-ttu-id="e51eb-164">브라우저 강제로 HTTPS를 통해 모든 통신을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-164">The browser forces all communication over HTTPS.</span></span> 
* <span data-ttu-id="e51eb-165">브라우저에서 신뢰할 수 없거나 잘못 된 인증서를 사용 하 여 사용자를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-165">The browser prevents the user from using untrusted or invalid certificates.</span></span> <span data-ttu-id="e51eb-166">브라우저 사용자가 일시적으로 이러한 인증서를 신뢰 하는 프롬프트를 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-166">The browser disables prompts that allow a user to temporarily trust such a certificate.</span></span>

<span data-ttu-id="e51eb-167">ASP.NET Core 2.1 이상을 사용 하 여 HSTS를 구현 합니다 `UseHsts` 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="e51eb-167">ASP.NET Core 2.1 or later implements HSTS with the `UseHsts` extension method.</span></span> <span data-ttu-id="e51eb-168">다음 코드 호출 `UseHsts` 에 앱이 없는 경우 [개발 모드](xref:fundamentals/environments):</span><span class="sxs-lookup"><span data-stu-id="e51eb-168">The following code calls `UseHsts` when the app isn't in [development mode](xref:fundamentals/environments):</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=10)]

<span data-ttu-id="e51eb-169">`UseHsts` 권장 되지 않습니다 개발에서 HSTS 헤더 캐시가 이므로 브라우저에서.</span><span class="sxs-lookup"><span data-stu-id="e51eb-169">`UseHsts` isn't recommended in development because the HSTS header is highly cacheable by browsers.</span></span> <span data-ttu-id="e51eb-170">기본적으로 `UseHsts` 로컬 루프백 주소를 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-170">By default, `UseHsts` excludes the local loopback address.</span></span>

<span data-ttu-id="e51eb-171">처음에 대 한 HTTPS를 구현 하는 프로덕션 환경에서는 초기 HSTS 값을 작은 값으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-171">For production environments implementing HTTPS for the first time, set the initial HSTS value to a small value.</span></span> <span data-ttu-id="e51eb-172">값을 설정할 시간에서 전혀 보다 하루를 HTTP로 HTTPS 인프라를 되돌려야 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="e51eb-172">Set the value from hours to no more than a single day in case you need to revert the HTTPS infrastructure to HTTP.</span></span> <span data-ttu-id="e51eb-173">HTTPS 구성의 유지 가능성에 확신한 후 늘릴 HSTS 최대 처리 기간 값 자주 사용 되는 값은 1 년입니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-173">After you're confident in the sustainability of the HTTPS configuration, increase the HSTS max-age value; a commonly used value is one year.</span></span> 

<span data-ttu-id="e51eb-174">다음 예를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="e51eb-174">The following code:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=5-12)]

* <span data-ttu-id="e51eb-175">Strict-전송-보안 헤더의 미리 로드 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-175">Sets the preload parameter of the Strict-Transport-Security header.</span></span> <span data-ttu-id="e51eb-176">미리 로드 되지 부분 합니다 [RFC HSTS 사양](https://tools.ietf.org/html/rfc6797), 있지만 HSTS 새로 설치할 때 사이트를 미리 로드 하려면 웹 브라우저에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-176">Preload is not part of the [RFC HSTS specification](https://tools.ietf.org/html/rfc6797), but is supported by web browsers to preload HSTS sites on fresh install.</span></span> <span data-ttu-id="e51eb-177">자세한 내용은 [https://hstspreload.org/](https://hstspreload.org/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e51eb-177">See [https://hstspreload.org/](https://hstspreload.org/) for more information.</span></span>
* <span data-ttu-id="e51eb-178">사용 하도록 설정 [includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2), 호스트 하위 도메인에 HSTS 정책을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-178">Enables [includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2), which applies the HSTS policy to Host subdomains.</span></span> 
* <span data-ttu-id="e51eb-179">60 일로 Strict-전송-보안 헤더의 최대 처리 기간 매개 변수를 명시적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-179">Explicitly sets the max-age parameter of the Strict-Transport-Security header to to 60 days.</span></span> <span data-ttu-id="e51eb-180">설정 하지 않으면 기본값은 30 일입니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-180">If not set, defaults to 30 days.</span></span> <span data-ttu-id="e51eb-181">참조 된 [최대 처리 기간 지시문](https://tools.ietf.org/html/rfc6797#section-6.1.1) 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-181">See the [max-age directive](https://tools.ietf.org/html/rfc6797#section-6.1.1) for more information.</span></span>
* <span data-ttu-id="e51eb-182">추가 `example.com` 를 제외 하는 호스트의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-182">Adds `example.com` to the list of hosts to exclude.</span></span>

<span data-ttu-id="e51eb-183">`UseHsts` 다음 루프백 호스트를 제외:</span><span class="sxs-lookup"><span data-stu-id="e51eb-183">`UseHsts` excludes the following loopback hosts:</span></span>

* <span data-ttu-id="e51eb-184">`localhost` : IPv4 루프백 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-184">`localhost` : The IPv4 loopback address.</span></span>
* <span data-ttu-id="e51eb-185">`127.0.0.1` : IPv4 루프백 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-185">`127.0.0.1` : The IPv4 loopback address.</span></span>
* <span data-ttu-id="e51eb-186">`[::1]` : IPv6 루프백 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-186">`[::1]` : The IPv6 loopback address.</span></span>

<span data-ttu-id="e51eb-187">앞의 예제에는 추가 호스트를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-187">The preceding example shows how to add additional hosts.</span></span>
::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="https"></a>
## <a name="opt-out-of-https-on-project-creation"></a><span data-ttu-id="e51eb-188">옵트아웃 https 프로젝트 생성 시</span><span class="sxs-lookup"><span data-stu-id="e51eb-188">Opt-out of HTTPS on project creation</span></span>

<span data-ttu-id="e51eb-189">ASP.NET Core 2.1 이상 웹 응용 프로그램 템플릿 (Visual Studio 또는 dotnet 명령 줄)에서 사용 하도록 설정 [HTTPS 간의 리디렉션으로](#require) 하 고 [HSTS](#hsts)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-189">The ASP.NET Core 2.1 or later web application templates (from Visual Studio or the dotnet command line) enable [HTTPS redirection](#require) and [HSTS](#hsts).</span></span> <span data-ttu-id="e51eb-190">HTTPS를 요구 하지 않는 배포에 대 한 있습니다 옵트아웃할 수 https입니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-190">For deployments that don't require HTTPS, you can opt-out of HTTPS.</span></span> <span data-ttu-id="e51eb-191">예를 들어, 일부 백 엔드 서비스는 HTTPS 처리 되 고 외부 가장자리에 HTTPS를 사용 하 여 각 노드에서 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-191">For example, some backend services where HTTPS is being handled externally at the edge, using HTTPS at each node is not needed.</span></span>

<span data-ttu-id="e51eb-192">옵트아웃 하려면 https:</span><span class="sxs-lookup"><span data-stu-id="e51eb-192">To opt-out of HTTPS:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="e51eb-193">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e51eb-193">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="e51eb-194">선택 취소 합니다 **HTTPS에 대 한 구성** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-194">Uncheck the **Configure for HTTPS** checkbox.</span></span>

![엔터티 다이어그램](enforcing-ssl/_static/out.png)

#   <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="e51eb-196">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="e51eb-196">.NET Core CLI</span></span>](#tab/netcore-cli) 

<span data-ttu-id="e51eb-197">`--no-https` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-197">Use the `--no-https` option.</span></span> <span data-ttu-id="e51eb-198">예</span><span class="sxs-lookup"><span data-stu-id="e51eb-198">For example</span></span>

```console
dotnet new webapp --no-https
```

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

---

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="how-to-setup-a-developer-certificate-for-docker"></a><span data-ttu-id="e51eb-199">Docker에 대 한 개발자 인증서를 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="e51eb-199">How to setup a developer certificate for Docker</span></span>

<span data-ttu-id="e51eb-200">참조 [이 GitHub 문제](https://github.com/aspnet/Docs/issues/6199)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51eb-200">See [this GitHub issue](https://github.com/aspnet/Docs/issues/6199).</span></span>

::: moniker-end
