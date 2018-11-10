---
title: ASP.NET Core에서 원본 간 요청 (CORS)를 사용 하도록 설정
author: rick-anderson
description: 에 대해 알아봅니다 어떻게 CORS 허용 하거나 거부 하는 ASP.NET Core 앱에서 크로스-원본 요청에 대 한 표준으로 합니다.
ms.author: riande
ms.custom: mvc
ms.date: 11/05/2018
uid: security/cors
ms.openlocfilehash: 8e5056b448d47d75272e9394b03ce8a58b05a0f4
ms.sourcegitcommit: 09affee3d234cb27ea6fe33bc113b79e68900d22
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51191323"
---
# <a name="enable-cross-origin-requests-cors-in-aspnet-core"></a><span data-ttu-id="7e842-103">ASP.NET Core에서 원본 간 요청 (CORS)를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7e842-103">Enable Cross-Origin Requests (CORS) in ASP.NET Core</span></span>

<span data-ttu-id="7e842-104">작성자: [Mike Wasson](https://github.com/mikewasson), [Shayne Boyer](https://twitter.com/spboyer), 및 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7e842-104">By [Mike Wasson](https://github.com/mikewasson), [Shayne Boyer](https://twitter.com/spboyer), and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="7e842-105">브라우저 보안 요청을 웹 페이지를 제공 하는 다른 도메인에서 웹 페이지를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-105">Browser security prevents a web page from making requests to a different domain than the one that served the web page.</span></span> <span data-ttu-id="7e842-106">이 제한은 라고 합니다 *동일 원본 정책*합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-106">This restriction is called the *same-origin policy*.</span></span> <span data-ttu-id="7e842-107">동일 원본 정책에서 다른 사이트의 중요 한 데이터를 읽을 악성 사이트를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-107">The same-origin policy prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="7e842-108">경우에 따라 다음 다른 사이트 앱 크로스-원본 요청을 허용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-108">Sometimes, you might want to allow other sites make cross-origin requests to your app.</span></span>

<span data-ttu-id="7e842-109">[교차 원본 자원 공유](https://www.w3.org/TR/cors/) (CORS, Cross Origin Resource Sharing)는 서버 측에서 동일 원본 정책을 완화할 수 있게 해주는 W3C 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-109">[Cross Origin Resource Sharing](https://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="7e842-110">CORS를 사용하면 서버가 명시적으로 특정 교차 원본 요청만 허용하고, 다른 요청은 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-110">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="7e842-111">와 같은 CORS는 안전 하 고 이전 기술 보다 더 유연한 [JSONP](https://wikipedia.org/wiki/JSONP)합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-111">CORS is safer and more flexible than earlier techniques, such as [JSONP](https://wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="7e842-112">이 항목에서는 ASP.NET Core 앱에서 CORS를 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-112">This topic shows how to enable CORS in an ASP.NET Core app.</span></span>

## <a name="same-origin"></a><span data-ttu-id="7e842-113">동일한 원본</span><span class="sxs-lookup"><span data-stu-id="7e842-113">Same origin</span></span>

<span data-ttu-id="7e842-114">동일한 구성표, 호스트 및 포트에 있는 경우 두 개의 Url가 동일한 원본 ([RFC 6454](https://tools.ietf.org/html/rfc6454)).</span><span class="sxs-lookup"><span data-stu-id="7e842-114">Two URLs have the same origin if they have identical schemes, hosts, and ports ([RFC 6454](https://tools.ietf.org/html/rfc6454)).</span></span>

<span data-ttu-id="7e842-115">다음 두 URL은 동일한 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-115">These two URLs have the same origin:</span></span>

* `https://example.com/foo.html`
* `https://example.com/bar.html`

<span data-ttu-id="7e842-116">이러한 Url에 이전 두 Url 보다 다양 한 원본:</span><span class="sxs-lookup"><span data-stu-id="7e842-116">These URLs have different origins than the previous two URLs:</span></span>

* <span data-ttu-id="7e842-117">`https://example.net` &ndash; 다른 도메인</span><span class="sxs-lookup"><span data-stu-id="7e842-117">`https://example.net` &ndash; Different domain</span></span>
* <span data-ttu-id="7e842-118">`https://www.example.com/foo.html` &ndash; 다른 하위 도메인</span><span class="sxs-lookup"><span data-stu-id="7e842-118">`https://www.example.com/foo.html` &ndash; Different subdomain</span></span>
* <span data-ttu-id="7e842-119">`http://example.com/foo.html` &ndash; 다른 구성표</span><span class="sxs-lookup"><span data-stu-id="7e842-119">`http://example.com/foo.html` &ndash; Different scheme</span></span>
* <span data-ttu-id="7e842-120">`https://example.com:9000/foo.html` &ndash; 다른 포트</span><span class="sxs-lookup"><span data-stu-id="7e842-120">`https://example.com:9000/foo.html` &ndash; Different port</span></span>

> [!NOTE]
> <span data-ttu-id="7e842-121">Internet Explorer는 원본을 비교할 때 포트를 고려하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-121">Internet Explorer doesn't consider the port when comparing origins.</span></span>

## <a name="register-cors-services"></a><span data-ttu-id="7e842-122">CORS 서비스 등록</span><span class="sxs-lookup"><span data-stu-id="7e842-122">Register CORS services</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="7e842-123">참조를 [Microsoft.AspNetCore.App 메타 패키지](xref:fundamentals/metapackage-app) 에 대 한 패키지 참조를 추가 하거나 합니다 [Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-123">Reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) or add a package reference to the [Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/) package.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="7e842-124">참조를 [Microsoft.AspNetCore.All 메타 패키지](xref:fundamentals/metapackage) 에 대 한 패키지 참조를 추가 하거나 합니다 [Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-124">Reference the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) or add a package reference to the [Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/) package.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="7e842-125">패키지 참조를 추가 합니다 [Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/) 패키지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-125">Add a package reference to the [Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/) package.</span></span>

::: moniker-end

<span data-ttu-id="7e842-126">호출 <xref:Microsoft.Extensions.DependencyInjection.MvcCorsMvcCoreBuilderExtensions.AddCors*> 에서 `Startup.ConfigureServices` CORS services 앱의 서비스 컨테이너를 추가 하려면:</span><span class="sxs-lookup"><span data-stu-id="7e842-126">Call <xref:Microsoft.Extensions.DependencyInjection.MvcCorsMvcCoreBuilderExtensions.AddCors*> in `Startup.ConfigureServices` to add CORS services to the app's service container:</span></span>

[!code-csharp[](cors/sample/CorsExample1/Startup.cs?name=snippet_addcors&highlight=3)]

## <a name="enable-cors"></a><span data-ttu-id="7e842-127">CORS를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7e842-127">Enable CORS</span></span>

<span data-ttu-id="7e842-128">CORS 서비스를 등록 한 후에 ASP.NET Core 앱에서 CORS를 사용 하도록 설정 하려면 다음 방법 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-128">After registering CORS services, use either of the following approaches to enable CORS in an ASP.NET Core app:</span></span>

* <span data-ttu-id="7e842-129">[CORS 미들웨어](#enable-cors-with-cors-middleware) &ndash; 전역적으로 미들웨어를 통해 앱에 적용할 CORS 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-129">[CORS Middleware](#enable-cors-with-cors-middleware) &ndash; Apply CORS policies globally to the app via middleware.</span></span>
* <span data-ttu-id="7e842-130">[MVC에서 CORS](#enable-cors-in-mvc) &ndash; 컨트롤러당 또는 작업당 적용할 CORS 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-130">[CORS in MVC](#enable-cors-in-mvc) &ndash; Apply CORS policies per action or per controller.</span></span> <span data-ttu-id="7e842-131">CORS 미들웨어를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-131">CORS Middleware isn't used.</span></span>

### <a name="enable-cors-with-cors-middleware"></a><span data-ttu-id="7e842-132">CORS 미들웨어를 사용 하 여 CORS를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7e842-132">Enable CORS with CORS Middleware</span></span>

<span data-ttu-id="7e842-133">CORS 미들웨어는 앱에 크로스-원본 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-133">CORS Middleware handles cross-origin requests to the app.</span></span> <span data-ttu-id="7e842-134">요청 처리 파이프라인에 CORS 미들웨어를 사용 하려면 호출을 <xref:Microsoft.AspNetCore.Builder.CorsMiddlewareExtensions.UseCors*> 확장 메서드 `Startup.Configure`합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-134">To enable CORS Middleware in the request processing pipeline, call the <xref:Microsoft.AspNetCore.Builder.CorsMiddlewareExtensions.UseCors*> extension method in `Startup.Configure`.</span></span>

<span data-ttu-id="7e842-135">CORS 미들웨어 앞에 야 정의 된 끝점이 모든 앱에서 크로스-원본 요청을 지원 하려면 (예를 들어 호출 하기 전에 `UseMvc` MVC/Razor 페이지 미들웨어에 대 한).</span><span class="sxs-lookup"><span data-stu-id="7e842-135">CORS Middleware must precede any defined endpoints in your app where you want to support cross-origin requests (for example, before the call to `UseMvc` for MVC/Razor Pages Middleware).</span></span>

<span data-ttu-id="7e842-136">A *원본 간 정책은* 사용 하 여 CORS 미들웨어를 추가 하는 경우에 지정할 수 있습니다는 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder> 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-136">A *cross-origin policy* can be specified when adding the CORS Middleware using the <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder> class.</span></span> <span data-ttu-id="7e842-137">CORS 정책을 정의 하는 방법은 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-137">There are two approaches for defining a CORS policy:</span></span>

* <span data-ttu-id="7e842-138">호출 `UseCors` 람다를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="7e842-138">Call `UseCors` with a lambda:</span></span>

  [!code-csharp[](cors/sample/CorsExample1/Startup.cs?highlight=11,12&range=22-38)]

  <span data-ttu-id="7e842-139">람다는 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder> 개체를 전달받습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-139">The lambda takes a <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder> object.</span></span> <span data-ttu-id="7e842-140">[구성 옵션](#cors-policy-options)와 같은 `WithOrigins`,이 항목의 뒷부분에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-140">[Configuration options](#cors-policy-options), such as `WithOrigins`, are described later in this topic.</span></span> <span data-ttu-id="7e842-141">앞의 예제는 정책에서 크로스-원본 요청 수 있습니다. `https://example.com` 및 다른 원본이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-141">In the preceding example, the policy allows cross-origin requests from `https://example.com` and no other origins.</span></span>

  <span data-ttu-id="7e842-142">후행 슬래시가 없는 URL을 지정 해야 합니다 (`/`).</span><span class="sxs-lookup"><span data-stu-id="7e842-142">The URL must be specified without a trailing slash (`/`).</span></span> <span data-ttu-id="7e842-143">URL을 사용 하 여 종료 되 면 `/`, 비교 반환 `false` 헤더가 없으면 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-143">If the URL terminates with `/`, the comparison returns `false` and no header is returned.</span></span>

  <span data-ttu-id="7e842-144">`CorsPolicyBuilder` fluent API에 있으므로 메서드 호출을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-144">`CorsPolicyBuilder` has a fluent API, so you can chain method calls:</span></span>

  [!code-csharp[](cors/sample/CorsExample3/Startup.cs?highlight=2-3&range=29-32)]

* <span data-ttu-id="7e842-145">하나 이상의 명명 된 CORS 정책을 정의 하 고 런타임에 이름별으로 정책을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-145">Define one or more named CORS policies and select the policy by name at runtime.</span></span> <span data-ttu-id="7e842-146">다음 예제에서는 라는 사용자 정의 CORS 정책을 *AllowSpecificOrigin*합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-146">The following example adds a user-defined CORS policy named *AllowSpecificOrigin*.</span></span> <span data-ttu-id="7e842-147">정책을 선택 하려면 이름을 전달 `UseCors`:</span><span class="sxs-lookup"><span data-stu-id="7e842-147">To select the policy, pass the name to `UseCors`:</span></span>

  [!code-csharp[](cors/sample/CorsExample2/Startup.cs?name=snippet_begin&highlight=5-6,21)]

### <a name="enable-cors-in-mvc"></a><span data-ttu-id="7e842-148">MVC에서 CORS를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7e842-148">Enable CORS in MVC</span></span>

<span data-ttu-id="7e842-149">또는 MVC를 사용 하 여 컨트롤러 또는 작업 별로 특정 CORS 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-149">You can alternatively use MVC to apply specific CORS policies per action or per controller.</span></span> <span data-ttu-id="7e842-150">CORS를 사용 하도록 MVC를 사용 하는 경우 등록된 된 CORS 서비스 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-150">When using MVC to enable CORS, the registered CORS services are used.</span></span> <span data-ttu-id="7e842-151">CORS 미들웨어를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-151">The CORS Middleware isn't used.</span></span>

### <a name="per-action"></a><span data-ttu-id="7e842-152">액션 별</span><span class="sxs-lookup"><span data-stu-id="7e842-152">Per action</span></span>

<span data-ttu-id="7e842-153">특정 작업에 대 한 CORS 정책을 지정 하려면 추가 합니다 [ &lbrack;EnableCors&rbrack; ](xref:Microsoft.AspNetCore.Cors.EnableCorsAttribute) 특성 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-153">To specify a CORS policy for a specific action, add the [&lbrack;EnableCors&rbrack;](xref:Microsoft.AspNetCore.Cors.EnableCorsAttribute) attribute to the action.</span></span> <span data-ttu-id="7e842-154">이때 정책 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-154">Specify the policy name.</span></span>

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnAction&highlight=2)]

### <a name="per-controller"></a><span data-ttu-id="7e842-155">컨트롤러 별</span><span class="sxs-lookup"><span data-stu-id="7e842-155">Per controller</span></span>

<span data-ttu-id="7e842-156">특정 컨트롤러에 대 한 CORS 정책을 지정 하려면 다음을 추가 합니다 [ &lbrack;EnableCors&rbrack; ](xref:Microsoft.AspNetCore.Cors.EnableCorsAttribute) 특성을 컨트롤러 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-156">To specify the CORS policy for a specific controller, add the [&lbrack;EnableCors&rbrack;](xref:Microsoft.AspNetCore.Cors.EnableCorsAttribute) attribute to the controller class.</span></span> <span data-ttu-id="7e842-157">이때 정책 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-157">Specify the policy name.</span></span>

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnController&highlight=2)]

<span data-ttu-id="7e842-158">우선 순위에 따라 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-158">The precedence order is:</span></span>

1. <span data-ttu-id="7e842-159">action</span><span class="sxs-lookup"><span data-stu-id="7e842-159">action</span></span>
1. <span data-ttu-id="7e842-160">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="7e842-160">controller</span></span>

### <a name="disable-cors"></a><span data-ttu-id="7e842-161">CORS 비활성시키기</span><span class="sxs-lookup"><span data-stu-id="7e842-161">Disable CORS</span></span>

<span data-ttu-id="7e842-162">컨트롤러 또는 작업에 대 한 CORS를 해제 하려면 사용 합니다 [ &lbrack;하도록 설정 하려면 DisableCors&rbrack; ](xref:Microsoft.AspNetCore.Cors.DisableCorsAttribute) 특성:</span><span class="sxs-lookup"><span data-stu-id="7e842-162">To disable CORS for a controller or action, use the [&lbrack;DisableCors&rbrack;](xref:Microsoft.AspNetCore.Cors.DisableCorsAttribute) attribute:</span></span>

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=DisableOnAction&highlight=2)]

## <a name="cors-policy-options"></a><span data-ttu-id="7e842-163">CORS 정책 옵션</span><span class="sxs-lookup"><span data-stu-id="7e842-163">CORS policy options</span></span>

<span data-ttu-id="7e842-164">이번 섹션에서는 CORS 정책에서 설정할 수 있는 다양한 옵션들을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-164">This section describes the various options that you can set in a CORS policy.</span></span>

* [<span data-ttu-id="7e842-165">허용되는 원본 설정하기</span><span class="sxs-lookup"><span data-stu-id="7e842-165">Set the allowed origins</span></span>](#set-the-allowed-origins)
* [<span data-ttu-id="7e842-166">허용되는 HTTP 메서드 설정하기</span><span class="sxs-lookup"><span data-stu-id="7e842-166">Set the allowed HTTP methods</span></span>](#set-the-allowed-http-methods)
* [<span data-ttu-id="7e842-167">허용되는 요청 헤더 설정하기</span><span class="sxs-lookup"><span data-stu-id="7e842-167">Set the allowed request headers</span></span>](#set-the-allowed-request-headers)
* [<span data-ttu-id="7e842-168">노출되는 응답 헤더 설정하기</span><span class="sxs-lookup"><span data-stu-id="7e842-168">Set the exposed response headers</span></span>](#set-the-exposed-response-headers)
* [<span data-ttu-id="7e842-169">교차 원본 요청의 자격 증명</span><span class="sxs-lookup"><span data-stu-id="7e842-169">Credentials in cross-origin requests</span></span>](#credentials-in-cross-origin-requests)
* [<span data-ttu-id="7e842-170">예비 요청 만료 시간 설정하기</span><span class="sxs-lookup"><span data-stu-id="7e842-170">Set the preflight expiration time</span></span>](#set-the-preflight-expiration-time)

<span data-ttu-id="7e842-171">일부 옵션에 대 한 읽기 하면 도움이 될 합니다 [CORS 어떻게 작동](#how-cors-works) 먼저 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-171">For some options, it may be helpful to read the [How CORS works](#how-cors-works) section first.</span></span>

### <a name="set-the-allowed-origins"></a><span data-ttu-id="7e842-172">허용되는 원본 설정하기</span><span class="sxs-lookup"><span data-stu-id="7e842-172">Set the allowed origins</span></span>

<span data-ttu-id="7e842-173">ASP.NET Core MVC에서 CORS 미들웨어에 허용 되는 원본을 지정 하는 방법에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-173">The CORS middleware in ASP.NET Core MVC has a few ways to specify allowed origins:</span></span>

* <span data-ttu-id="7e842-174"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithOrigins*>: 하나 이상의 Url을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-174"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithOrigins*>: Allows specifying one or more URLs.</span></span> <span data-ttu-id="7e842-175">URL은 구성표, 호스트 이름 및 경로 정보 없이 포트를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-175">The URL may include the scheme, host name, and port without any path information.</span></span> <span data-ttu-id="7e842-176">예를 들어, `https://example.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-176">For example, `https://example.com`.</span></span> <span data-ttu-id="7e842-177">후행 슬래시가 없는 URL을 지정 해야 합니다 (`/`).</span><span class="sxs-lookup"><span data-stu-id="7e842-177">The URL must be specified without a trailing slash (`/`).</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=20-24&highlight=4)]

* <span data-ttu-id="7e842-178"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyOrigin*>: 모든 체계를 사용 하 여 모든 원본에서 CORS 요청을 허용 합니다. (`http` 또는 `https`).</span><span class="sxs-lookup"><span data-stu-id="7e842-178"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyOrigin*>: Allows CORS requests from all origins with any scheme (`http` or `https`).</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=28-32&highlight=4)]

<span data-ttu-id="7e842-179">모든 원본의 요청을 허용하기 전에 신중히 고민하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-179">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="7e842-180">즉 모든 원본에서 요청할 수 있도록 *웹 사이트* 앱에 크로스-원본 요청을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-180">Allowing requests from any origin means that *any website* can make cross-origin requests to your app.</span></span>

::: moniker range=">= aspnetcore-2.2"

> [!NOTE]
> <span data-ttu-id="7e842-181">지정 `AllowAnyOrigin` 고 `AllowCredentials` 는 안전 하지 않은 구성 및 교차 사이트 요청 위조 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-181">Specifying `AllowAnyOrigin` and `AllowCredentials` is an insecure configuration and can result in cross-site request forgery.</span></span> <span data-ttu-id="7e842-182">CORS 서비스 앱은 두 개의 구성 된 경우 잘못 된 CORS 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-182">The CORS service returns an invalid CORS response when an app is configured with the two.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

> [!NOTE]
> <span data-ttu-id="7e842-183">지정 `AllowAnyOrigin` 고 `AllowCredentials` 는 안전 하지 않은 구성 및 교차 사이트 요청 위조 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-183">Specifying `AllowAnyOrigin` and `AllowCredentials` is an insecure configuration and can result in cross-site request forgery.</span></span> <span data-ttu-id="7e842-184">클라이언트에서 서버 리소스에 액세스 권한을 부여 해야 할 경우에 정확한 원본 목록이 올바르면을 지정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-184">Consider specifying an exact list of origins if your client needs to authorize to access server resources.</span></span>

::: moniker-end

<span data-ttu-id="7e842-185">이 설정은 영향을 줍니다 [요청 및 액세스 제어-허용-원본 헤더 실행 전](#preflight-requests) (이 항목의 뒷부분에 설명).</span><span class="sxs-lookup"><span data-stu-id="7e842-185">This setting affects [preflight requests and the Access-Control-Allow-Origin header](#preflight-requests) (described later in this topic).</span></span>

* <span data-ttu-id="7e842-186"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.SetIsOriginAllowedToAllowWildcardSubdomains*> -지정된 된 도메인의 모든 하위 도메인의 CORS 요청을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-186"><xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.SetIsOriginAllowedToAllowWildcardSubdomains*> - Allows CORS requests from any sub-domain of a given domain.</span></span> <span data-ttu-id="7e842-187">체계는 와일드 카드 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-187">The scheme cannot be a wildcard.</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=98-104&highlight=4)]

### <a name="set-the-allowed-http-methods"></a><span data-ttu-id="7e842-188">허용되는 HTTP 메서드 설정하기</span><span class="sxs-lookup"><span data-stu-id="7e842-188">Set the allowed HTTP methods</span></span>

<span data-ttu-id="7e842-189">모든 HTTP 메서드를 허용 하려면 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyMethod*>:</span><span class="sxs-lookup"><span data-stu-id="7e842-189">To allow all HTTP methods, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyMethod*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=45-50&highlight=5)]

<span data-ttu-id="7e842-190">이 설정은 영향을 줍니다 [요청 및 액세스-컨트롤-허용-Methods 헤더 실행 전](#preflight-requests) (이 항목의 뒷부분에 설명).</span><span class="sxs-lookup"><span data-stu-id="7e842-190">This setting affects [preflight requests and the Access-Control-Allow-Methods header](#preflight-requests) (described later in this topic).</span></span>

### <a name="set-the-allowed-request-headers"></a><span data-ttu-id="7e842-191">허용되는 요청 헤더 설정하기</span><span class="sxs-lookup"><span data-stu-id="7e842-191">Set the allowed request headers</span></span>

<span data-ttu-id="7e842-192">특정 헤더를 CORS 요청을 보낼 수 있도록 호출 *요청 헤더를 작성*, 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithHeaders*> 허용 되는 헤더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-192">To allow specific headers to be sent in a CORS request, called *author request headers*, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithHeaders*> and specify the allowed headers:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=54-59&highlight=5)]

<span data-ttu-id="7e842-193">요청 헤더에 모든 author 수 있도록 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyHeader*>:</span><span class="sxs-lookup"><span data-stu-id="7e842-193">To allow all author request headers, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyHeader*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=63-68&highlight=5)]

<span data-ttu-id="7e842-194">이 설정은 영향을 줍니다 [요청 및 액세스 제어-요청 헤더 헤더 실행 전](#preflight-requests) (이 항목의 뒷부분에 설명).</span><span class="sxs-lookup"><span data-stu-id="7e842-194">This setting affects [preflight requests and the Access-Control-Request-Headers header](#preflight-requests) (described later in this topic).</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="7e842-195">지정 된 특정 헤더에 CORS 미들웨어 정책 일치가 `WithHeaders` 은 헤더 전송 하는 경우에 가능 `Access-Control-Request-Headers` 에 명시 된 헤더와 정확히 일치 `WithHeaders`합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-195">A CORS Middleware policy match to specific headers specified by `WithHeaders` is only possible when the headers sent in `Access-Control-Request-Headers` exactly match the headers stated in `WithHeaders`.</span></span>

<span data-ttu-id="7e842-196">예를 들어 다음과 같이 구성 된 앱을 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-196">For instance, consider an app configured as follows:</span></span>

```csharp
app.UseCors(policy => policy.WithHeaders(HeaderNames.CacheControl));
```

<span data-ttu-id="7e842-197">CORS 미들웨어 때문에 다음 요청 헤더를 사용 하 여 실행 전 요청을 거절 `Content-Language` ([HeaderNames.ContentLanguage](xref:Microsoft.Net.Http.Headers.HeaderNames.ContentLanguage))에 나열 되지 않은 `WithHeaders`:</span><span class="sxs-lookup"><span data-stu-id="7e842-197">CORS Middleware declines a preflight request with the following request header because `Content-Language` ([HeaderNames.ContentLanguage](xref:Microsoft.Net.Http.Headers.HeaderNames.ContentLanguage)) isn't listed in `WithHeaders`:</span></span>

```
Access-Control-Request-Headers: Cache-Control, Content-Language
```

<span data-ttu-id="7e842-198">앱 반환을 *200 확인* 응답 하지만 CORS 헤더를 다시 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-198">The app returns a *200 OK* response but doesn't send the CORS headers back.</span></span> <span data-ttu-id="7e842-199">따라서 브라우저는 크로스-원본 요청을 시도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-199">Therefore, the browser doesn't attempt the cross-origin request.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="7e842-200">CORS 미들웨어의 네 가지 헤더를 항상 허용 된 `Access-Control-Request-Headers` CorsPolicy.Headers에 구성 된 값에 관계 없이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-200">CORS Middleware always allows four headers in the `Access-Control-Request-Headers` to be sent regardless of the values configured in CorsPolicy.Headers.</span></span> <span data-ttu-id="7e842-201">이 헤더 목록에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-201">This list of headers includes:</span></span>

* `Accept`
* `Accept-Language`
* `Content-Language`
* `Origin`

<span data-ttu-id="7e842-202">예를 들어 다음과 같이 구성 된 앱을 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-202">For instance, consider an app configured as follows:</span></span>

```csharp
app.UseCors(policy => policy.WithHeaders(HeaderNames.CacheControl));
```

<span data-ttu-id="7e842-203">CORS 미들웨어가 성공적으로 응답 다음 요청 헤더를 사용 하 여 실행 전 요청에 있으므로 `Content-Language` 은 항상 허용 목록에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-203">CORS Middleware responds successfully to a preflight request with the following request header because `Content-Language` is always whitelisted:</span></span>

```
Access-Control-Request-Headers: Cache-Control, Content-Language
```

::: moniker-end

### <a name="set-the-exposed-response-headers"></a><span data-ttu-id="7e842-204">노출되는 응답 헤더 설정하기</span><span class="sxs-lookup"><span data-stu-id="7e842-204">Set the exposed response headers</span></span>

<span data-ttu-id="7e842-205">브라우저는 기본적으로 모든 앱에 대 한 응답 헤더를 노출 하지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-205">By default, the browser doesn't expose all of the response headers to the app.</span></span> <span data-ttu-id="7e842-206">자세한 내용은 [W3C 크로스-원본 자원 공유 (용어): 간단한 응답 헤더](https://www.w3.org/TR/cors/#simple-response-header)합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-206">For more information, see [W3C Cross-Origin Resource Sharing (Terminology): Simple Response Header](https://www.w3.org/TR/cors/#simple-response-header).</span></span>

<span data-ttu-id="7e842-207">기본적으로 사용 가능한 응답 헤더들은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-207">The response headers that are available by default are:</span></span>

* `Cache-Control`
* `Content-Language`
* `Content-Type`
* `Expires`
* `Last-Modified`
* `Pragma`

<span data-ttu-id="7e842-208">이러한 헤더를 호출 하는 CORS 사양 *간단한 응답 헤더*합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-208">The CORS specification calls these headers *simple response headers*.</span></span> <span data-ttu-id="7e842-209">다른 헤더를 사용할 수 있도록 앱을 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithExposedHeaders*>:</span><span class="sxs-lookup"><span data-stu-id="7e842-209">To make other headers available to the app, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithExposedHeaders*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=72-77&highlight=5)]

### <a name="credentials-in-cross-origin-requests"></a><span data-ttu-id="7e842-210">교차 원본 요청의 자격 증명</span><span class="sxs-lookup"><span data-stu-id="7e842-210">Credentials in cross-origin requests</span></span>

<span data-ttu-id="7e842-211">CORS 요청에서 자격 증명(Credentials)은 특별한 처리를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-211">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="7e842-212">기본적으로 브라우저는 크로스-원본 요청을 사용 하 여 자격 증명을 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-212">By default, the browser doesn't send credentials with a cross-origin request.</span></span> <span data-ttu-id="7e842-213">자격 증명 쿠키 및 HTTP 인증 체계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-213">Credentials include cookies and HTTP authentication schemes.</span></span> <span data-ttu-id="7e842-214">크로스-원본 요청을 사용 하 여 자격 증명을 보내려면 클라이언트 설정 해야 합니다 `XMLHttpRequest.withCredentials` 에 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-214">To send credentials with a cross-origin request, the client must set `XMLHttpRequest.withCredentials` to `true`.</span></span>

<span data-ttu-id="7e842-215">사용 하 여 `XMLHttpRequest` 직접.</span><span class="sxs-lookup"><span data-stu-id="7e842-215">Using `XMLHttpRequest` directly:</span></span>

```javascript
var xhr = new XMLHttpRequest();
xhr.open('get', 'https://www.example.com/api/test');
xhr.withCredentials = true;
```

<span data-ttu-id="7e842-216">jQuery를 사용할 경우:</span><span class="sxs-lookup"><span data-stu-id="7e842-216">In jQuery:</span></span>

```jQuery
$.ajax({
  type: 'get',
  url: 'https://www.example.com/home',
  xhrFields: {
    withCredentials: true
}
```

<span data-ttu-id="7e842-217">또한 서버에서도 자격 증명을 허용해야만 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-217">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="7e842-218">크로스-원본 자격 증명을 허용 하려면 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowCredentials*>:</span><span class="sxs-lookup"><span data-stu-id="7e842-218">To allow cross-origin credentials, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowCredentials*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=81-86&highlight=5)]

<span data-ttu-id="7e842-219">HTTP 응답에 포함 됩니다는 `Access-Control-Allow-Credentials` 서버 크로스-원본 요청에 대 한 자격 증명을 허용 하는지 브라우저에 지시 하는 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-219">The HTTP response includes an `Access-Control-Allow-Credentials` header, which tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="7e842-220">경우 브라우저는 자격 증명을 보내지만 응답 유효한 없는 `Access-Control-Allow-Credentials` 헤더, 브라우저 앱에 대 한 응답을 제공 하지 않습니다 및 크로스-원본 요청에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-220">If the browser sends credentials but the response doesn't include a valid `Access-Control-Allow-Credentials` header, the browser doesn't expose the response to the app, and the cross-origin request fails.</span></span>

<span data-ttu-id="7e842-221">크로스-원본 자격 증명을 허용 하는 경우 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-221">Be careful when allowing cross-origin credentials.</span></span> <span data-ttu-id="7e842-222">다른 도메인에서 웹 사이트는 사용자의 지식 없이 사용자를 대신 하 여 앱에는 로그인 한 사용자의 자격 증명을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-222">A website at another domain can send a signed-in user's credentials to the app on the user's behalf without the user's knowledge.</span></span>

<span data-ttu-id="7e842-223">CORS 사양도 해당 설정에 따라 원본이 `"*"` (모든 원본) 올바르지 않습니다 경우는 `Access-Control-Allow-Credentials` 헤더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-223">The CORS specification also states that setting origins to `"*"` (all origins) is invalid if the `Access-Control-Allow-Credentials` header is present.</span></span>

### <a name="preflight-requests"></a><span data-ttu-id="7e842-224">실행 전 요청</span><span class="sxs-lookup"><span data-stu-id="7e842-224">Preflight requests</span></span>

<span data-ttu-id="7e842-225">브라우저는 일부 CORS 요청에 대 한 실제 요청 하기 전에 추가 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-225">For some CORS requests, the browser sends an additional request before making the actual request.</span></span> <span data-ttu-id="7e842-226">이 요청에서 호출 되는 *실행 전 요청*합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-226">This request is called a *preflight request*.</span></span> <span data-ttu-id="7e842-227">다음 조건이 true 인 경우 브라우저가 실행 전 요청을 건너뛸 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="7e842-227">The browser can skip the preflight request if the following conditions are true:</span></span>

* <span data-ttu-id="7e842-228">요청 메서드가 GET, HEAD 또는 POST 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-228">The request method is GET, HEAD, or POST.</span></span>
* <span data-ttu-id="7e842-229">앱 이외의 요청 헤더를 설정 하지 않는 `Accept`, `Accept-Language`를 `Content-Language`를 `Content-Type`, 또는 `Last-Event-ID`합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-229">The app doesn't set request headers other than `Accept`, `Accept-Language`, `Content-Language`, `Content-Type`, or `Last-Event-ID`.</span></span>
* <span data-ttu-id="7e842-230">`Content-Type` 헤더 경우 설정에 다음 값 중 하나:</span><span class="sxs-lookup"><span data-stu-id="7e842-230">The `Content-Type` header, if set, has one of the following values:</span></span>
  * `application/x-www-form-urlencoded`
  * `multipart/form-data`
  * `text/plain`

<span data-ttu-id="7e842-231">호출 하 여 앱을 설정 하는 헤더에 적용 되는 클라이언트 요청에 대 한 요청 헤더에는 규칙 집합 `setRequestHeader` 에 `XMLHttpRequest` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-231">The rule on request headers set for the client request applies to headers that the app sets by calling `setRequestHeader` on the `XMLHttpRequest` object.</span></span> <span data-ttu-id="7e842-232">이러한 헤더를 호출 하는 CORS 사양 *요청 헤더를 작성*합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-232">The CORS specification calls these headers *author request headers*.</span></span> <span data-ttu-id="7e842-233">헤더와 같은 브라우저 설정 수에 규칙 적용 되지 않습니다 `User-Agent`하십시오 `Host`, 또는 `Content-Length`합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-233">The rule doesn't apply to headers the browser can set, such as `User-Agent`, `Host`, or `Content-Length`.</span></span>

<span data-ttu-id="7e842-234">다음은 실행 전 요청의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-234">The following is an example of a preflight request:</span></span>

```
OPTIONS https://myservice.azurewebsites.net/api/test HTTP/1.1
Accept: */*
Origin: https://myclient.azurewebsites.net
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: accept, x-my-custom-header
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
Content-Length: 0
```

<span data-ttu-id="7e842-235">HTTP OPTIONS 메서드를 사용 하는 사전 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-235">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="7e842-236">두 가지 특수 헤더를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-236">It includes two special headers:</span></span>

* <span data-ttu-id="7e842-237">`Access-Control-Request-Method`실제 요청에 사용 됩니다: HTTP 메서드.</span><span class="sxs-lookup"><span data-stu-id="7e842-237">`Access-Control-Request-Method`: The HTTP method that will be used for the actual request.</span></span>
* <span data-ttu-id="7e842-238">`Access-Control-Request-Headers`: 목록에 대 한 실제 요청에서 앱을 설정 하는 요청 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-238">`Access-Control-Request-Headers`: A list of request headers that the app sets on the actual request.</span></span> <span data-ttu-id="7e842-239">여기와 같은 브라우저 설정 하는 헤더가 포함 되지 않습니다 앞에서 설명한 대로 `User-Agent`입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-239">As stated earlier, this doesn't include headers that the browser sets, such as `User-Agent`.</span></span>

<span data-ttu-id="7e842-240">CORS 실행 전 요청에 포함 될 수 있습니다는 `Access-Control-Request-Headers` 헤더로 실제 요청과 함께 전송 되는 헤더를 서버에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-240">A CORS preflight request might include an `Access-Control-Request-Headers` header, which indicates to the server the headers that are sent with the actual request.</span></span>

<span data-ttu-id="7e842-241">특정 헤더를 허용 하려면 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithHeaders*>:</span><span class="sxs-lookup"><span data-stu-id="7e842-241">To allow specific headers, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithHeaders*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=54-59&highlight=5)]

<span data-ttu-id="7e842-242">요청 헤더에 모든 author 수 있도록 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyHeader*>:</span><span class="sxs-lookup"><span data-stu-id="7e842-242">To allow all author request headers, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyHeader*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=63-68&highlight=5)]

<span data-ttu-id="7e842-243">브라우저 설정 하는 방법에 전적으로 일관 되지 `Access-Control-Request-Headers`합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-243">Browsers aren't entirely consistent in how they set `Access-Control-Request-Headers`.</span></span> <span data-ttu-id="7e842-244">이외의 헤더 값으로 설정 하면 `"*"` (사용할지 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicy.AllowAnyHeader*>)를 하나 이상 포함 해야 `Accept`, `Content-Type`, 및 `Origin`, 지원 하려는 모든 사용자 지정 헤더 및.</span><span class="sxs-lookup"><span data-stu-id="7e842-244">If you set headers to anything other than `"*"` (or use <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicy.AllowAnyHeader*>), you should include at least `Accept`, `Content-Type`, and `Origin`, plus any custom headers that you want to support.</span></span>

<span data-ttu-id="7e842-245">다음은 실행 전 요청 (서버 요청을 허용 하는지 가정할 경우)에 대 한 예제 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-245">The following is an example response to the preflight request (assuming that the server allows the request):</span></span>

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 0
Access-Control-Allow-Origin: https://myclient.azurewebsites.net
Access-Control-Allow-Headers: x-my-custom-header
Access-Control-Allow-Methods: PUT
Date: Wed, 20 May 2015 06:33:22 GMT
```

<span data-ttu-id="7e842-246">응답에 포함 되어는 `Access-Control-Allow-Methods` 허용 되는 메서드를 나열 하는 헤더 및 필요에 따라는 `Access-Control-Allow-Headers` 허용 되는 헤더를 나열 하는 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-246">The response includes an `Access-Control-Allow-Methods` header that lists the allowed methods and optionally an `Access-Control-Allow-Headers` header, which lists the allowed headers.</span></span> <span data-ttu-id="7e842-247">실행 전 요청이 성공 하면 브라우저는 실제 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-247">If the preflight request succeeds, the browser sends the actual request.</span></span>

<span data-ttu-id="7e842-248">실행 전 요청이 거부 되 면 앱에서 반환 된 *200 확인* 응답 CORS 헤더를 다시 보내지 않습니다. 하지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-248">If the preflight request is denied, the app returns a *200 OK* response but doesn't send the CORS headers back.</span></span> <span data-ttu-id="7e842-249">따라서 브라우저는 크로스-원본 요청을 시도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-249">Therefore, the browser doesn't attempt the cross-origin request.</span></span>

### <a name="set-the-preflight-expiration-time"></a><span data-ttu-id="7e842-250">예비 요청 만료 시간 설정하기</span><span class="sxs-lookup"><span data-stu-id="7e842-250">Set the preflight expiration time</span></span>

<span data-ttu-id="7e842-251">`Access-Control-Max-Age` 헤더 실행 전 요청에 응답을 캐시할 수 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-251">The `Access-Control-Max-Age` header specifies how long the response to the preflight request can be cached.</span></span> <span data-ttu-id="7e842-252">이 헤더를 설정 하려면 호출 <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.SetPreflightMaxAge*>:</span><span class="sxs-lookup"><span data-stu-id="7e842-252">To set this header, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.SetPreflightMaxAge*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=90-95&highlight=5)]

## <a name="how-cors-works"></a><span data-ttu-id="7e842-253">CORS의 동작 방식</span><span class="sxs-lookup"><span data-stu-id="7e842-253">How CORS works</span></span>

<span data-ttu-id="7e842-254">이번 섹션에서는 CORS 요청 시 HTTP 메시지 수준에서 발생하는 일들을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-254">This section describes what happens in a CORS request at the level of the HTTP messages.</span></span> <span data-ttu-id="7e842-255">CORS 정책을 올바르게 구성 하 고 예기치 않은 동작이 발생 하는 경우 디버깅할 수 있도록 CORS의 작동 방식을 이해 하는 것이 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-255">It's important to understand how CORS works so that the CORS policy can be configured correctly and debugged when unexpected behaviors occur.</span></span>

<span data-ttu-id="7e842-256">CORS 명세에서는 교차 원본 요청을 활성화시키기 위한 용도로 몇 가지 새로운 HTTP 헤더들이 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-256">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="7e842-257">브라우저에서 CORS를 지 원하는 경우 이러한 머리글 크로스-원본 요청을 자동으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-257">If a browser supports CORS, it sets these headers automatically for cross-origin requests.</span></span> <span data-ttu-id="7e842-258">CORS를 사용 하도록 사용자 지정 JavaScript 코드 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-258">Custom JavaScript code isn't required to enable CORS.</span></span>

<span data-ttu-id="7e842-259">다음은 원본 간 요청의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-259">The following is an example of a cross-origin request.</span></span> <span data-ttu-id="7e842-260">`Origin` 헤더는 요청 하는 사이트의 도메인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-260">The `Origin` header provides the domain of the site that's making the request:</span></span>

```
GET https://myservice.azurewebsites.net/api/test HTTP/1.1
Referer: https://myclient.azurewebsites.net/
Accept: */*
Accept-Language: en-US
Origin: https://myclient.azurewebsites.net
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
```

<span data-ttu-id="7e842-261">서버 요청을 허용 하는 경우에 설정의 `Access-Control-Allow-Origin` 헤더를 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-261">If the server allows the request, it sets the `Access-Control-Allow-Origin` header in the response.</span></span> <span data-ttu-id="7e842-262">이 헤더의 값이 일치 하거나 합니다 `Origin` 요청의 헤더 또는 와일드 카드 값 `"*"`, 모든 원본을 허용 되는 의미:</span><span class="sxs-lookup"><span data-stu-id="7e842-262">The value of this header either matches the `Origin` header from the request or is the wildcard value `"*"`, meaning that any origin is allowed:</span></span>

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Type: text/plain; charset=utf-8
Access-Control-Allow-Origin: https://myclient.azurewebsites.net
Date: Wed, 20 May 2015 06:27:30 GMT
Content-Length: 12

Test message
```

<span data-ttu-id="7e842-263">응답에 포함 되지 않은 경우는 `Access-Control-Allow-Origin` 헤더를 크로스-원본 요청에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-263">If the response doesn't include the `Access-Control-Allow-Origin` header, the cross-origin request fails.</span></span> <span data-ttu-id="7e842-264">특히 브라우저 요청을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-264">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="7e842-265">서버 성공적인 응답을 반환 하는 경우에 브라우저 되어도 응답이 클라이언트 앱에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e842-265">Even if the server returns a successful response, the browser doesn't make the response available to the client app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7e842-266">추가 자료</span><span class="sxs-lookup"><span data-stu-id="7e842-266">Additional resources</span></span>

* [<span data-ttu-id="7e842-267">크로스-원본 자원 공유 (CORS)</span><span class="sxs-lookup"><span data-stu-id="7e842-267">Cross-Origin Resource Sharing (CORS)</span></span>](https://developer.mozilla.org/docs/Web/HTTP/CORS)
