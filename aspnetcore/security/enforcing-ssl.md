---
title: ASP.NET Core에 HTTPS를 적용 합니다.
author: rick-anderson
description: 웹 응용 프로그램에서 ASP.NET Core HTTPS/TLS를 요청 하는 방법을 보여 줍니다.
manager: wpickett
ms.author: riande
ms.date: 2/9/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/enforcing-ssl
ms.openlocfilehash: 0433ddb3bf1ef0074c683903ad4553cd6a0b4741
ms.sourcegitcommit: 545ff5a632e2281035c1becec1f99137298e4f5c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2018
ms.locfileid: "34687820"
---
# <a name="enforce-https-in-an-aspnet-core"></a><span data-ttu-id="f527f-103">ASP.NET Core에 HTTPS를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-103">Enforce HTTPS in an ASP.NET Core</span></span>

<span data-ttu-id="f527f-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="f527f-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="f527f-105">이 문서에서는 다음과 같은 내용을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-105">This document shows how to:</span></span>

- <span data-ttu-id="f527f-106">모든 요청에 대 한 HTTPS가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-106">Require HTTPS for all requests.</span></span>
- <span data-ttu-id="f527f-107">모든 HTTP 요청을 HTTPS로 리디렉션하는 방법.</span><span class="sxs-lookup"><span data-stu-id="f527f-107">Redirect all HTTP requests to HTTPS.</span></span>

> [!WARNING]
> <span data-ttu-id="f527f-108">수행 **하지** 사용 `RequireHttpsAttribute` 중요 한 정보를 수신 하는 웹 Api에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-108">Do **not** use `RequireHttpsAttribute` on Web APIs that receive sensitive information.</span></span> <span data-ttu-id="f527f-109">`RequireHttpsAttribute` HTTP 상태 코드를 사용 하 여 HTTP에서 HTTPS로 브라우저를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-109">`RequireHttpsAttribute` uses HTTP status codes to redirect browsers from HTTP to HTTPS.</span></span> <span data-ttu-id="f527f-110">API 클라이언트 이해 하지 못하거나 리디렉션을 HTTP에서 HTTPS로 준수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-110">API clients may not understand or obey redirects from HTTP to HTTPS.</span></span> <span data-ttu-id="f527f-111">이러한 클라이언트는 HTTP를 통해 정보를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-111">Such clients may send information over HTTP.</span></span> <span data-ttu-id="f527f-112">웹 Api 하거나 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-112">Web APIs should either:</span></span>
>
>* <span data-ttu-id="f527f-113">HTTP에서 수신 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-113">Not listen on HTTP.</span></span>
>* <span data-ttu-id="f527f-114">상태 코드 400 (잘못 된 요청)와 연결을 닫고 요청을 처리 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="f527f-114">Close the connection with status code 400 (Bad Request) and not serve the request.</span></span>

<a name="require"></a>
## <a name="require-https"></a><span data-ttu-id="f527f-115">HTTPS가 필요</span><span class="sxs-lookup"><span data-stu-id="f527f-115">Require HTTPS</span></span>

::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="f527f-116">모든 ASP.NET Core 웹 앱 호출 권장 `UseHttpsRedirection` HTTPS로 모든 HTTP 요청을 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-116">We recommend all ASP.NET Core web apps call `UseHttpsRedirection` to redirect all HTTP requests to HTTPS.</span></span> <span data-ttu-id="f527f-117">경우 `UseHsts` 호출 되는 앱에서 호출 해야 하기 전에 `UseHttpsRedirection`합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-117">If `UseHsts` is called in the app, it must be called before `UseHttpsRedirection`.</span></span>

<span data-ttu-id="f527f-118">다음 호출 코드 `UseHttpsRedirection` 에 `Startup` 클래스:</span><span class="sxs-lookup"><span data-stu-id="f527f-118">The following code calls `UseHttpsRedirection` in the `Startup` class:</span></span>

<span data-ttu-id="f527f-119">[!code-csharp[sample](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=13)]</span><span class="sxs-lookup"><span data-stu-id="f527f-119">[!code-csharp[sample](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=13)]</span></span>


<span data-ttu-id="f527f-120">다음 예를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="f527f-120">The following code:</span></span>

<span data-ttu-id="f527f-121">[!code-csharp[sample](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=14-99)]</span><span class="sxs-lookup"><span data-stu-id="f527f-121">[!code-csharp[sample](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=14-99)]</span></span>

* <span data-ttu-id="f527f-122">집합 `RedirectStatusCode`합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-122">Sets `RedirectStatusCode`.</span></span>
* <span data-ttu-id="f527f-123">5001를 HTTPS 포트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-123">Sets the HTTPS port to 5001.</span></span>

::: moniker-end


::: moniker range="< aspnetcore-2.1"

<span data-ttu-id="f527f-124">[RequireHttpsAttribute](/dotnet/api/Microsoft.AspNetCore.Mvc.RequireHttpsAttribute) HTTPS가 필요 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-124">The [RequireHttpsAttribute](/dotnet/api/Microsoft.AspNetCore.Mvc.RequireHttpsAttribute) is used to require HTTPS.</span></span> <span data-ttu-id="f527f-125">`[RequireHttpsAttribute]` 컨트롤러 또는 메서드를 데코레이팅 할 수 있습니다 또는 전역으로 적용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-125">`[RequireHttpsAttribute]` can decorate controllers or methods, or can be applied globally.</span></span> <span data-ttu-id="f527f-126">특성을 전역으로 적용 하려면 다음 코드를 추가 `ConfigureServices` 에 `Startup`:</span><span class="sxs-lookup"><span data-stu-id="f527f-126">To apply the attribute globally, add the following code to `ConfigureServices` in `Startup`:</span></span>

<span data-ttu-id="f527f-127">[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]</span><span class="sxs-lookup"><span data-stu-id="f527f-127">[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]</span></span>

<span data-ttu-id="f527f-128">위의 강조 표시된 코드는 모든 요청에 `HTTPS` 를 사용하도록 강제하며, 그 결과 HTTP 요청은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-128">The preceding highlighted code requires all requests use `HTTPS`; therefore, HTTP requests are ignored.</span></span> <span data-ttu-id="f527f-129">다음에 강조 표시된 코드는 모든 HTTP 요청을 HTTPS로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-129">The following highlighted code redirects all HTTP requests to HTTPS:</span></span>

<span data-ttu-id="f527f-130">[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]</span><span class="sxs-lookup"><span data-stu-id="f527f-130">[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]</span></span>

<span data-ttu-id="f527f-131">자세한 내용은 참조 [URL 다시 쓰기 미들웨어](xref:fundamentals/url-rewriting)합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-131">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span>

<span data-ttu-id="f527f-132">전역으로 HTTPS를 요구하는 것이 보안상 가장 안전한 모범 사례입니다 (`options.Filters.Add(new RequireHttpsAttribute());`).</span><span class="sxs-lookup"><span data-stu-id="f527f-132">Requiring HTTPS globally (`options.Filters.Add(new RequireHttpsAttribute());`) is a security best practice.</span></span> <span data-ttu-id="f527f-133">적용 된 `[RequireHttps]` 모든 컨트롤러/Razor 페이지에는 특성으로 전체적으로 HTTPS를 필요로 하는 컨트롤로 안전 하다 고 간주 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-133">Applying the `[RequireHttps]` attribute to all controllers/Razor Pages isn't considered as secure as requiring HTTPS globally.</span></span> <span data-ttu-id="f527f-134">보장할 수는 `[RequireHttps]` 특성은 새 컨트롤러 및 Razor 페이지 추가 될 때 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-134">You can't guarantee the `[RequireHttps]` attribute is applied when new controllers and Razor Pages are added.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"
<a name="hsts"></a>
## <a name="http-strict-transport-security-protocol-hsts"></a><span data-ttu-id="f527f-135">HTTP 엄격한 전송 보안 프로토콜 (HSTS)</span><span class="sxs-lookup"><span data-stu-id="f527f-135">HTTP Strict Transport Security Protocol (HSTS)</span></span>

<span data-ttu-id="f527f-136">당 [OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project), [HTTP 엄격한 전송 보안 (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) 는 특별 한 응답 헤더를 사용 하 여 웹 응용 프로그램에 의해 지정 된 옵트인 보안 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-136">Per [OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project), [HTTP Strict Transport Security (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) is an opt-in security enhancement that is specified by a web application through the use of a special response header.</span></span> <span data-ttu-id="f527f-137">지원 되는 브라우저는이 헤더를 수신 되 면 해당 브라우저의 통신을 지정한 도메인에 HTTP를 통해 보낼 수 없게 됩니다 및 HTTPS를 통해 모든 통신 송신할 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-137">Once a supported browser receives this header that browser will prevent any communications from being sent over HTTP to the specified domain and will instead send all communications over HTTPS.</span></span> <span data-ttu-id="f527f-138">또한 브라우저에 대 한 프롬프트를 통해 HTTPS 클릭을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-138">It also prevents HTTPS click through prompts on browsers.</span></span>

<span data-ttu-id="f527f-139">ASP.NET Core 2.1 이상 HSTS와 구현 하는 `UseHsts` 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="f527f-139">ASP.NET Core 2.1 or later implements HSTS with the `UseHsts` extension method.</span></span> <span data-ttu-id="f527f-140">다음 호출 코드 `UseHsts` 앱에 없는 경우 [개발 모드](xref:fundamentals/environments):</span><span class="sxs-lookup"><span data-stu-id="f527f-140">The following code calls `UseHsts` when the app isn't in [development mode](xref:fundamentals/environments):</span></span>

<span data-ttu-id="f527f-141">[!code-csharp[sample](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=10)]</span><span class="sxs-lookup"><span data-stu-id="f527f-141">[!code-csharp[sample](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=10)]</span></span>

<span data-ttu-id="f527f-142">`UseHsts` 않으므로 개발에 권장 되는 HSTS 헤더는 항상 브라우저에서 캐시할.</span><span class="sxs-lookup"><span data-stu-id="f527f-142">`UseHsts` is not recommend in development because the HSTS header is highly cachable by browsers.</span></span> <span data-ttu-id="f527f-143">기본적으로 UseHsts 로컬 루프백 주소를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-143">By default, UseHsts excludes the local loopback address.</span></span>

<span data-ttu-id="f527f-144">다음 예를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="f527f-144">The following code:</span></span>

<span data-ttu-id="f527f-145">[!code-csharp[sample](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=5-12)]</span><span class="sxs-lookup"><span data-stu-id="f527f-145">[!code-csharp[sample](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=5-12)]</span></span>

* <span data-ttu-id="f527f-146">Strict-전송-보안 헤더의 미리 로드 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-146">Sets the preload parameter of the Strict-Transport-Security header.</span></span> <span data-ttu-id="f527f-147">미리 로드를가의 일부가 [RFC HSTS 사양](https://tools.ietf.org/html/rfc6797), 있지만 HSTS 사이트 설치에 미리 로드 하려면 웹 브라우저에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-147">Preload is not part of the [RFC HSTS specification](https://tools.ietf.org/html/rfc6797), but is supported by web browsers to preload HSTS sites on fresh install.</span></span> <span data-ttu-id="f527f-148">자세한 내용은 [https://hstspreload.org/](https://hstspreload.org/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f527f-148">See [https://hstspreload.org/](https://hstspreload.org/) for more information.</span></span>
* <span data-ttu-id="f527f-149">수 있도록 [includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2), 하위 도메인의 호스트에 HSTS 정책을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-149">Enables [includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2), which applies the HSTS policy to Host subdomains.</span></span> 
* <span data-ttu-id="f527f-150">60 일 Strict-전송-보안 헤더의 최대 처리 기간 매개 변수를 명시적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-150">Explicitly sets the max-age parameter of the Strict-Transport-Security header to to 60 days.</span></span> <span data-ttu-id="f527f-151">그렇지 않은 경우 30 일에 기본값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-151">If not set, defaults to 30 days.</span></span> <span data-ttu-id="f527f-152">참조는 [최대 처리 기간 지시문](https://tools.ietf.org/html/rfc6797#section-6.1.1) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-152">See the [max-age directive](https://tools.ietf.org/html/rfc6797#section-6.1.1) for more information.</span></span>
* <span data-ttu-id="f527f-153">추가 `example.com` 제외 하는 호스트의 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-153">Adds `example.com` to the list of hosts to exclude.</span></span>

<span data-ttu-id="f527f-154">`UseHsts` 다음과 같은 루프백 호스트는 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-154">`UseHsts` excludes the following loopback hosts:</span></span>

* <span data-ttu-id="f527f-155">`localhost` : IPv4 루프백 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-155">`localhost` : The IPv4 loopback address.</span></span>
* <span data-ttu-id="f527f-156">`127.0.0.1` : IPv4 루프백 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-156">`127.0.0.1` : The IPv4 loopback address.</span></span>
* <span data-ttu-id="f527f-157">`[::1]` : IPv6 루프백 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-157">`[::1]` : The IPv6 loopback address.</span></span>

<span data-ttu-id="f527f-158">앞의 예제에는 추가 호스트를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-158">The preceding example shows how to add additional hosts.</span></span>
::: moniker-end


::: moniker range=">= aspnetcore-2.1"
<a name="https"></a>
## <a name="opt-out-of-https-on-project-creation"></a><span data-ttu-id="f527f-159">옵트아웃 HTTPS의 프로젝트 생성 시</span><span class="sxs-lookup"><span data-stu-id="f527f-159">Opt-out of HTTPS on project creation</span></span>

<span data-ttu-id="f527f-160">ASP.NET Core 2.1와 (Visual Studio 또는 dotnet 명령줄)에서 최신 웹 응용 프로그램 템플릿을 사용 하면 [HTTPS 리디렉션](#require) 및 [HSTS](#hsts)합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-160">The ASP.NET Core 2.1 and later web application templates (from Visual Studio or the dotnet command line) enable [HTTPS redirection](#require) and [HSTS](#hsts).</span></span> <span data-ttu-id="f527f-161">HTTPS를 필요로 하지 않는 배포의 경우 있습니다 수 옵트아웃 https입니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-161">For deployments that don't require HTTPS, you can opt-out of HTTPS.</span></span> <span data-ttu-id="f527f-162">예를 들어 일부 백 엔드 서비스에 HTTPS 처리 되 고 외부에서 경계 면 HTTPS를 사용 하 여 각 노드에서 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-162">For example, some backend services where HTTPS is being handled externally at the edge, using HTTPS at each node is not needed.</span></span>

<span data-ttu-id="f527f-163">되지 않게 하려면 https:</span><span class="sxs-lookup"><span data-stu-id="f527f-163">To opt-out of HTTPS:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="f527f-164">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f527f-164">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="f527f-165">취소는 **HTTPS에 대 한 구성** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-165">Uncheck the **Configure for HTTPS** checkbox.</span></span>

![엔터티 다이어그램](enforcing-ssl/_static/out.png)

#   <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="f527f-167">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="f527f-167">.NET Core CLI</span></span>](#tab/netcore-cli) 

<span data-ttu-id="f527f-168">`--no-https` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-168">Use the `--no-https` option.</span></span> <span data-ttu-id="f527f-169">예</span><span class="sxs-lookup"><span data-stu-id="f527f-169">For example</span></span>

```console
dotnet new webapp --no-https
```

---

::: moniker-end

::: moniker range=">= aspnetcore-2.1"
## <a name="how-to-setup-a-developer-certificate-for-docker"></a><span data-ttu-id="f527f-170">Docker에 대 한 개발자 인증서를 설치 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f527f-170">How to setup a developer certificate for Docker</span></span>

<span data-ttu-id="f527f-171">참조 [이 GitHub 문제](https://github.com/aspnet/Docs/issues/6199)합니다.</span><span class="sxs-lookup"><span data-stu-id="f527f-171">See [this GitHub issue](https://github.com/aspnet/Docs/issues/6199).</span></span>

::: moniker-end
