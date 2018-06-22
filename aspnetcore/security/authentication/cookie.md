---
title: ASP.NET Core Id 없이 쿠키 인증을 사용 하 여
author: rick-anderson
description: ASP.NET Core Id 없이 쿠키 인증을 사용 하 여 설명
ms.author: riande
ms.date: 10/11/2017
uid: security/authentication/cookie
ms.openlocfilehash: 2064e4d6406ce3ca3ce28732f113e8c81447aace
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36275608"
---
# <a name="use-cookie-authentication-without-aspnet-core-identity"></a><span data-ttu-id="29a27-103">ASP.NET Core Id 없이 쿠키 인증을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="29a27-103">Use cookie authentication without ASP.NET Core Identity</span></span>

<span data-ttu-id="29a27-104">여 [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="29a27-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="29a27-105">이전 인증 항목에 나와 있는 것 처럼 [ASP.NET Core Id](xref:security/authentication/identity) 만들고 로그인 유지 하기 위한 완전 한 완전 한 기능의 인증 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-105">As you've seen in the earlier authentication topics, [ASP.NET Core Identity](xref:security/authentication/identity) is a complete, full-featured authentication provider for creating and maintaining logins.</span></span> <span data-ttu-id="29a27-106">그러나 다음 쿠키 기반 인증에 사용자 고유의 사용자 지정 인증 논리를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-106">However, you may want to use your own custom authentication logic with cookie-based authentication at times.</span></span> <span data-ttu-id="29a27-107">ASP.NET Core Id 없이 독립 실행형 인증 공급자로 쿠키 기반 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-107">You can use cookie-based authentication as a standalone authentication provider without ASP.NET Core Identity.</span></span>

<span data-ttu-id="29a27-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/cookie/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="29a27-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/cookie/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="29a27-109">샘플 응용 프로그램에서 설명을 위해 Maria Rodriguez 가상의 사용자에 대 한 사용자 계정을 응용 프로그램에 하드 코딩 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-109">For demonstration purposes in the sample app, the user account for the hypothetical user, Maria Rodriguez, is hardcoded into the app.</span></span> <span data-ttu-id="29a27-110">전자 메일 이름을 사용 하 여 "maria.rodriguez@contoso.com" 및 사용자를 로그인 할 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-110">Use the Email username "maria.rodriguez@contoso.com" and any password to sign in the user.</span></span> <span data-ttu-id="29a27-111">사용자가 인증 된 `AuthenticateUser` 에서 메서드는 *Pages/Account/Login.cshtml.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-111">The user is authenticated in the `AuthenticateUser` method in the *Pages/Account/Login.cshtml.cs* file.</span></span> <span data-ttu-id="29a27-112">실제 예제에서 데이터베이스에 대해 사용자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-112">In a real-world example, the user would be authenticated against a database.</span></span>

<span data-ttu-id="29a27-113">ASP.NET Core에서 마이그레이션 쿠키 기반 인증에 대 한 내용은 2.0으로 1.x 참조 [마이그레이션할 인증 및 ASP.NET 코어 2.0 (쿠키 기반 인증) 항목에 Id](xref:migration/1x-to-2x/identity-2x#cookie-based-authentication)합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-113">For information on migrating cookie-based authentication from ASP.NET Core 1.x to 2.0, see [Migrate Authentication and Identity to ASP.NET Core 2.0 topic (Cookie-based Authentication)](xref:migration/1x-to-2x/identity-2x#cookie-based-authentication).</span></span>

<span data-ttu-id="29a27-114">ASP.NET Core Id를 사용 하려면 참조는 [Id 소개](xref:security/authentication/identity) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-114">To use ASP.NET Core Identity, see the [Introduction to Identity](xref:security/authentication/identity) topic.</span></span>

## <a name="configuration"></a><span data-ttu-id="29a27-115">구성</span><span class="sxs-lookup"><span data-stu-id="29a27-115">Configuration</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="29a27-116">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="29a27-116">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="29a27-117">응용 프로그램을 사용 하지 않는 경우는 [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app)에 대 한 프로젝트 파일에서 패키지 참조를 만들는 [Microsoft.AspNetCore.Authentication.Cookies](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Cookies/) 패키지 (2.1.0 버전 또는 나중에).</span><span class="sxs-lookup"><span data-stu-id="29a27-117">If the app doesn't use the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app), create a package reference in the project file for the [Microsoft.AspNetCore.Authentication.Cookies](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Cookies/) package (version 2.1.0 or later).</span></span>

<span data-ttu-id="29a27-118">에 `ConfigureServices` 메서드를 사용 하 여 인증 미들웨어 서비스 만들기는 `AddAuthentication` 및 `AddCookie` 메서드:</span><span class="sxs-lookup"><span data-stu-id="29a27-118">In the `ConfigureServices` method, create the Authentication Middleware service with the `AddAuthentication` and `AddCookie` methods:</span></span>

[!code-csharp[](cookie/samples/2.x/CookieSample/Startup.cs?name=snippet1)]

<span data-ttu-id="29a27-119">`AuthenticationScheme` 에 전달 된 `AddAuthentication` 응용 프로그램에 대 한 기본 인증 체계를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-119">`AuthenticationScheme` passed to `AddAuthentication` sets the default authentication scheme for the app.</span></span> <span data-ttu-id="29a27-120">`AuthenticationScheme` 쿠키 인증의 여러 인스턴스가 있고 하려는 경우 유용 [특정 스키마를 가진 권한 부여](xref:security/authorization/limitingidentitybyscheme)합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-120">`AuthenticationScheme` is useful when there are multiple instances of cookie authentication and you want to [authorize with a specific scheme](xref:security/authorization/limitingidentitybyscheme).</span></span> <span data-ttu-id="29a27-121">설정의 `AuthenticationScheme` 를 `CookieAuthenticationDefaults.AuthenticationScheme` 체계 "쿠키"의 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-121">Setting the `AuthenticationScheme` to `CookieAuthenticationDefaults.AuthenticationScheme` provides a value of "Cookies" for the scheme.</span></span> <span data-ttu-id="29a27-122">체계를 구별 하는 임의의 문자열 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-122">You can supply any string value that distinguishes the scheme.</span></span>

<span data-ttu-id="29a27-123">에 `Configure` 메서드를 사용 하 여는 `UseAuthentication` 설정 하는 인증 미들웨어를 호출 하는 메서드는 `HttpContext.User` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-123">In the `Configure` method, use the `UseAuthentication` method to invoke the Authentication Middleware that sets the `HttpContext.User` property.</span></span> <span data-ttu-id="29a27-124">호출 된 `UseAuthentication` 메서드 호출 하기 전에 `UseMvcWithDefaultRoute` 또는 `UseMvc`:</span><span class="sxs-lookup"><span data-stu-id="29a27-124">Call the `UseAuthentication` method before calling `UseMvcWithDefaultRoute` or `UseMvc`:</span></span>

[!code-csharp[](cookie/samples/2.x/CookieSample/Startup.cs?name=snippet2)]

<span data-ttu-id="29a27-125">**AddCookie 옵션**</span><span class="sxs-lookup"><span data-stu-id="29a27-125">**AddCookie Options**</span></span>

<span data-ttu-id="29a27-126">[CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions?view=aspnetcore-2.0) 클래스는 인증 공급자 옵션을 구성 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-126">The [CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions?view=aspnetcore-2.0) class is used to configure the authentication provider options.</span></span>

| <span data-ttu-id="29a27-127">옵션</span><span class="sxs-lookup"><span data-stu-id="29a27-127">Option</span></span> | <span data-ttu-id="29a27-128">설명</span><span class="sxs-lookup"><span data-stu-id="29a27-128">Description</span></span> |
| ------ | ----------- |
| [<span data-ttu-id="29a27-129">AccessDeniedPath</span><span class="sxs-lookup"><span data-stu-id="29a27-129">AccessDeniedPath</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.accessdeniedpath?view=aspnetcore-2.0) | <span data-ttu-id="29a27-130">302 있음 (URL 리디렉션)와 제공에 대 한 경로 제공 하 여 트리거되면 `HttpContext.ForbidAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-130">Provides the path to supply with a 302 Found (URL redirect) when triggered by `HttpContext.ForbidAsync`.</span></span> <span data-ttu-id="29a27-131">기본값은 `/Account/AccessDenied`입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-131">The default value is `/Account/AccessDenied`.</span></span> |
| [<span data-ttu-id="29a27-132">ClaimsIssuer</span><span class="sxs-lookup"><span data-stu-id="29a27-132">ClaimsIssuer</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions.claimsissuer?view=aspnetcore-2.0) | <span data-ttu-id="29a27-133">에 사용할 발급자는 [발급자](/dotnet/api/system.security.claims.claim.issuer) 쿠키 인증 서비스에 의해 만들어진 모든 클레임에 대 한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-133">The issuer to use for the [Issuer](/dotnet/api/system.security.claims.claim.issuer) property on any claims created by the cookie authentication service.</span></span> |
| [<span data-ttu-id="29a27-134">Cookie.Domain</span><span class="sxs-lookup"><span data-stu-id="29a27-134">Cookie.Domain</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.domain?view=aspnetcore-2.0) | <span data-ttu-id="29a27-135">쿠키 처리 되는 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-135">The domain name where the cookie is served.</span></span> <span data-ttu-id="29a27-136">기본적으로 요청 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-136">By default, this is the host name of the request.</span></span> <span data-ttu-id="29a27-137">브라우저 쿠키 요청에서 일치 하는 호스트 이름에만 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-137">The browser only sends the cookie in requests to a matching host name.</span></span> <span data-ttu-id="29a27-138">이 도메인의 모든 호스트에 사용할 수 있는 쿠키를 조정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-138">You may wish to adjust this to have cookies available to any host in your domain.</span></span> <span data-ttu-id="29a27-139">예를 들어 쿠키 도메인 설정 `.contoso.com` 를 사용할 수 있도록 `contoso.com`, `www.contoso.com`, 및 `staging.www.contoso.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-139">For example, setting the cookie domain to `.contoso.com` makes it available to `contoso.com`, `www.contoso.com`, and `staging.www.contoso.com`.</span></span> |
| [<span data-ttu-id="29a27-140">Cookie.Expiration</span><span class="sxs-lookup"><span data-stu-id="29a27-140">Cookie.Expiration</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.expiration?view=aspnetcore-2.0) | <span data-ttu-id="29a27-141">쿠키의 수명을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-141">Gets or sets the lifespan of a cookie.</span></span> <span data-ttu-id="29a27-142">현재 아니요 ops 옵션이 고 ASP.NET Core 2.1에서 사용 되지 않는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-142">Currently, this option no-ops and will become obsolete in ASP.NET Core 2.1+.</span></span> <span data-ttu-id="29a27-143">사용 하 여 `ExpireTimeSpan` 쿠키 만료를 설정 하는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-143">Use the `ExpireTimeSpan` option to set cookie expiration.</span></span> <span data-ttu-id="29a27-144">자세한 내용은 참조 [CookieAuthenticationOptions.Cookie.Expiration의 동작을 명확 하 게](https://github.com/aspnet/Security/issues/1293)합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-144">For more information, see [Clarify behavior of CookieAuthenticationOptions.Cookie.Expiration](https://github.com/aspnet/Security/issues/1293).</span></span> |
| [<span data-ttu-id="29a27-145">Cookie.HttpOnly</span><span class="sxs-lookup"><span data-stu-id="29a27-145">Cookie.HttpOnly</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.httponly?view=aspnetcore-2.0) | <span data-ttu-id="29a27-146">쿠키를 서버에만 액세스할 수 있어야 하는 경우를 나타내는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-146">A flag indicating if the cookie should be accessible only to servers.</span></span> <span data-ttu-id="29a27-147">이 값을 변경 `false` 쿠키에 액세스 하는 클라이언트 쪽 스크립트를 허용 하 고 표시 하며 열림 앱이 쿠키 도용 앱 있어야는 [교차 사이트 스크립팅 (XSS)](xref:security/cross-site-scripting) 취약점입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-147">Changing this value to `false` permits client-side scripts to access the cookie and may open your app to cookie theft should your app have a [Cross-site scripting (XSS)](xref:security/cross-site-scripting) vulnerability.</span></span> <span data-ttu-id="29a27-148">기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-148">The default value is `true`.</span></span> |
| [<span data-ttu-id="29a27-149">Cookie.Name</span><span class="sxs-lookup"><span data-stu-id="29a27-149">Cookie.Name</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.name?view=aspnetcore-2.0) | <span data-ttu-id="29a27-150">쿠키의 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-150">Sets the name of the cookie.</span></span> |
| [<span data-ttu-id="29a27-151">Cookie.Path</span><span class="sxs-lookup"><span data-stu-id="29a27-151">Cookie.Path</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.path?view=aspnetcore-2.0) | <span data-ttu-id="29a27-152">동일한 호스트 이름에서 실행 되는 앱을 격리 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-152">Used to isolate apps running on the same host name.</span></span> <span data-ttu-id="29a27-153">실행 중인 앱이 있는 경우 `/app1` 및 해당 응용 프로그램에 쿠키를 제한 하려면 설정는 `CookiePath` 속성을 `/app1`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-153">If you have an app running at `/app1` and want to restrict cookies to that app, set the `CookiePath` property to `/app1`.</span></span> <span data-ttu-id="29a27-154">이러한 작업을 통해 쿠키는 에서만 사용할 수에 대 한 요청 `/app1` 아래에 있는 모든 응용 프로그램 및입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-154">By doing so, the cookie is only available on requests to `/app1` and any app underneath it.</span></span> |
| [<span data-ttu-id="29a27-155">Cookie.SameSite</span><span class="sxs-lookup"><span data-stu-id="29a27-155">Cookie.SameSite</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.samesite?view=aspnetcore-2.0) | <span data-ttu-id="29a27-156">브라우저에서 동일한 사이트 요청에 연결 될 쿠키를 허용 하는지 여부를 나타냅니다 (`SameSiteMode.Strict`) 또는 안전 HTTP 메서드와 같은 사이트 요청을 사용 하 여 교차 사이트 요청 (`SameSiteMode.Lax`).</span><span class="sxs-lookup"><span data-stu-id="29a27-156">Indicates whether the browser should allow the cookie to be attached to same-site requests only (`SameSiteMode.Strict`) or cross-site requests using safe HTTP methods and same-site requests (`SameSiteMode.Lax`).</span></span> <span data-ttu-id="29a27-157">로 설정 하면 `SameSiteMode.None`, 쿠키 헤더 값이 설정 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-157">When set to `SameSiteMode.None`, the cookie header value isn't set.</span></span> <span data-ttu-id="29a27-158">[쿠키 정책 미들웨어](#cookie-policy-middleware) 제공 하는 값을 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-158">Note that [Cookie Policy Middleware](#cookie-policy-middleware) might overwrite the value that you provide.</span></span> <span data-ttu-id="29a27-159">기본값은 OAuth 인증을 지원 하려면 `SameSiteMode.Lax`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-159">To support OAuth authentication, the default value is `SameSiteMode.Lax`.</span></span> <span data-ttu-id="29a27-160">자세한 내용은 참조 [SameSite 쿠키 정책으로 인해 분할 하는 OAuth 인증](https://github.com/aspnet/Security/issues/1231)합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-160">For more information, see [OAuth authentication broken due to SameSite cookie policy](https://github.com/aspnet/Security/issues/1231).</span></span> |
| [<span data-ttu-id="29a27-161">Cookie.SecurePolicy</span><span class="sxs-lookup"><span data-stu-id="29a27-161">Cookie.SecurePolicy</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.securepolicy?view=aspnetcore-2.0) | <span data-ttu-id="29a27-162">만든 쿠키를 HTTPS로 제한 해야 하는 경우를 나타내는 플래그 (`CookieSecurePolicy.Always`), HTTP 또는 HTTPS (`CookieSecurePolicy.None`), 또는 요청와 동일한 프로토콜 (`CookieSecurePolicy.SameAsRequest`).</span><span class="sxs-lookup"><span data-stu-id="29a27-162">A flag indicating if the cookie created should be limited to HTTPS (`CookieSecurePolicy.Always`), HTTP or HTTPS (`CookieSecurePolicy.None`), or the same protocol as the request (`CookieSecurePolicy.SameAsRequest`).</span></span> <span data-ttu-id="29a27-163">기본값은 `CookieSecurePolicy.SameAsRequest`입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-163">The default value is `CookieSecurePolicy.SameAsRequest`.</span></span> |
| [<span data-ttu-id="29a27-164">DataProtectionProvider</span><span class="sxs-lookup"><span data-stu-id="29a27-164">DataProtectionProvider</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.dataprotectionprovider?view=aspnetcore-2.0) | <span data-ttu-id="29a27-165">설정의 `DataProtectionProvider` 기본값을 만드는 데 사용 되는 `TicketDataFormat`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-165">Sets the `DataProtectionProvider` that's used to create the default `TicketDataFormat`.</span></span> <span data-ttu-id="29a27-166">경우는 `TicketDataFormat` 속성이 설정 되어는 `DataProtectionProvider` 옵션 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-166">If the `TicketDataFormat` property is set, the `DataProtectionProvider` option isn't used.</span></span> <span data-ttu-id="29a27-167">을 지정 하지 않으면 응용 프로그램의 기본 데이터 보호 공급자가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-167">If not provided, the app's default data protection provider is used.</span></span> |
| [<span data-ttu-id="29a27-168">이벤트</span><span class="sxs-lookup"><span data-stu-id="29a27-168">Events</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.events?view=aspnetcore-2.0) | <span data-ttu-id="29a27-169">특정 처리 시점에서 앱 제어를 제공 하는 공급자에서 메서드를 호출 하는 처리기.</span><span class="sxs-lookup"><span data-stu-id="29a27-169">The handler calls methods on the provider that give the app control at certain processing points.</span></span> <span data-ttu-id="29a27-170">경우 `Events` 는 메서드를 호출할 때 아무 작업도 수행 하는 기본 인스턴스가 제공이 제공 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-170">If `Events` aren't provided, a default instance is supplied that does nothing when the methods are called.</span></span> |
| [<span data-ttu-id="29a27-171">EventsType</span><span class="sxs-lookup"><span data-stu-id="29a27-171">EventsType</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions.eventstype?view=aspnetcore-2.0) | <span data-ttu-id="29a27-172">서비스 유형으로 가져오는 데 사용 된 `Events` 속성 대신 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="29a27-172">Used as the service type to get the `Events` instance instead of the property.</span></span> |
| [<span data-ttu-id="29a27-173">ExpireTimeSpan</span><span class="sxs-lookup"><span data-stu-id="29a27-173">ExpireTimeSpan</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.expiretimespan?view=aspnetcore-2.0) | <span data-ttu-id="29a27-174">`TimeSpan` 쿠키 내부에 저장 된 인증 티켓이 만료 된 이후입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-174">The `TimeSpan` after which the authentication ticket stored inside the cookie expires.</span></span> <span data-ttu-id="29a27-175">`ExpireTimeSpan` 티켓에 대 한 만료 시간을 생성 하는 현재 시간에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-175">`ExpireTimeSpan` is added to the current time to create the expiration time for the ticket.</span></span> <span data-ttu-id="29a27-176">`ExpiredTimeSpan` 항상 서버에 의해 확인 된 암호화 된 AuthTicket 값에 들어갑니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-176">The `ExpiredTimeSpan` value always goes into the encrypted AuthTicket verified by the server.</span></span> <span data-ttu-id="29a27-177">에 들어갈 수 있습니다는 [Set-cookie](https://tools.ietf.org/html/rfc6265#section-4.1) 헤더가 없지만 경우에만 `IsPersistent` 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-177">It may also go into the [Set-Cookie](https://tools.ietf.org/html/rfc6265#section-4.1) header, but only if `IsPersistent` is set.</span></span> <span data-ttu-id="29a27-178">설정 하려면 `IsPersistent` 를 `true`, 구성에서 [AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.authentication.authenticationproperties) 에 전달 된 `SignInAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-178">To set `IsPersistent` to `true`, configure the [AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.authentication.authenticationproperties) passed to `SignInAsync`.</span></span> <span data-ttu-id="29a27-179">기본값 `ExpireTimeSpan` 14 일입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-179">The default value of `ExpireTimeSpan` is 14 days.</span></span> |
| [<span data-ttu-id="29a27-180">LoginPath</span><span class="sxs-lookup"><span data-stu-id="29a27-180">LoginPath</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.loginpath?view=aspnetcore-2.0) | <span data-ttu-id="29a27-181">302 있음 (URL 리디렉션)와 제공에 대 한 경로 제공 하 여 트리거되면 `HttpContext.ChallengeAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-181">Provides the path to supply with a 302 Found (URL redirect) when triggered by `HttpContext.ChallengeAsync`.</span></span> <span data-ttu-id="29a27-182">생성 된 401는 현재 URL에 추가 되며는 `LoginPath` 의해 명명 된 쿼리 문자열 매개 변수로 `ReturnUrlParameter`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-182">The current URL that generated the 401 is added to the `LoginPath` as a query string parameter named by the `ReturnUrlParameter`.</span></span> <span data-ttu-id="29a27-183">요청을 한 번의 `LoginPath` 부여 된 새 로그인 id는 `ReturnUrlParameter` 값 브라우저 원래 권한이 없음된 상태 코드를 발생 시킨 URL로 다시 리디렉션하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-183">Once a request to the `LoginPath` grants a new sign-in identity, the `ReturnUrlParameter` value is used to redirect the browser back to the URL that caused the original unauthorized status code.</span></span> <span data-ttu-id="29a27-184">기본값은 `/Account/Login`입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-184">The default value is `/Account/Login`.</span></span> |
| [<span data-ttu-id="29a27-185">LogoutPath</span><span class="sxs-lookup"><span data-stu-id="29a27-185">LogoutPath</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.logoutpath?view=aspnetcore-2.0) | <span data-ttu-id="29a27-186">경우는 `LogoutPath` 해당 경로에 대 한 요청을 리디렉션합니다 처리기에 제공 된 값에 따라는 `ReturnUrlParameter`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-186">If the `LogoutPath` is provided to the handler, then a request to that path redirects based on the value of the `ReturnUrlParameter`.</span></span> <span data-ttu-id="29a27-187">기본값은 `/Account/Logout`입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-187">The default value is `/Account/Logout`.</span></span> |
| [<span data-ttu-id="29a27-188">ReturnUrlParameter</span><span class="sxs-lookup"><span data-stu-id="29a27-188">ReturnUrlParameter</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.returnurlparameter?view=aspnetcore-2.0) | <span data-ttu-id="29a27-189">302 (URL 리디렉션) Found 응답에 대 한 처리기가 추가 되는 쿼리 문자열 매개 변수의 이름을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-189">Determines the name of the query string parameter that's appended by the handler for a 302 Found (URL redirect) response.</span></span> <span data-ttu-id="29a27-190">`ReturnUrlParameter` 에 요청이 도착할 때 사용 되는 `LoginPath` 또는 `LogoutPath` 로그인 또는 로그 아웃 작업을 수행한 후 원래 URL로 브라우저 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-190">`ReturnUrlParameter` is used when a request arrives on the `LoginPath` or `LogoutPath` to return the browser to the original URL after the login or logout action is performed.</span></span> <span data-ttu-id="29a27-191">기본값은 `ReturnUrl`입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-191">The default value is `ReturnUrl`.</span></span> |
| [<span data-ttu-id="29a27-192">SessionStore</span><span class="sxs-lookup"><span data-stu-id="29a27-192">SessionStore</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.sessionstore?view=aspnetcore-2.0) | <span data-ttu-id="29a27-193">요청 간에 id를 저장 하는 데 사용 하는 선택적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-193">An optional container used to store identity across requests.</span></span> <span data-ttu-id="29a27-194">을 사용 하는 세션 식별자만 클라이언트로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-194">When used, only a session identifier is sent to the client.</span></span> <span data-ttu-id="29a27-195">`SessionStore` 큰 id와 잠재적 문제를 완화 하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-195">`SessionStore` can be used to mitigate potential problems with large identities.</span></span> |
| [<span data-ttu-id="29a27-196">SlidingExpiration</span><span class="sxs-lookup"><span data-stu-id="29a27-196">SlidingExpiration</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.slidingexpiration?view=aspnetcore-2.0) | <span data-ttu-id="29a27-197">업데이트 된 만료 시간이 새 쿠키를 동적으로 발급 해야 하는 경우를 나타내는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-197">A flag indicating if a new cookie with an updated expiration time should be issued dynamically.</span></span> <span data-ttu-id="29a27-198">이 현재 쿠키 만료 기간 50% 이상의 만료 된 모든 요청에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-198">This can happen on any request where the current cookie expiration period is more than 50% expired.</span></span> <span data-ttu-id="29a27-199">새로운 만료 날짜로 앞으로 이동 하는 현재 날짜와 `ExpireTimespan`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-199">The new expiration date is moved forward to be the current date plus the `ExpireTimespan`.</span></span> <span data-ttu-id="29a27-200">[절대 쿠키 만료 시간](xref:security/authentication/cookie#absolute-cookie-expiration) 를 사용 하 여 설정할 수는 `AuthenticationProperties` 클래스를 호출할 때 `SignInAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-200">An [absolute cookie expiration time](xref:security/authentication/cookie#absolute-cookie-expiration) can be set by using the `AuthenticationProperties` class when calling `SignInAsync`.</span></span> <span data-ttu-id="29a27-201">절대 만료 시간 인증 쿠키가 유효 하다는 시간의 양을 제한 하 여 응용 프로그램의 보안을 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-201">An absolute expiration time can improve the security of your app by limiting the amount of time that the authentication cookie is valid.</span></span> <span data-ttu-id="29a27-202">기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-202">The default value is `true`.</span></span> |
| [<span data-ttu-id="29a27-203">TicketDataFormat</span><span class="sxs-lookup"><span data-stu-id="29a27-203">TicketDataFormat</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.ticketdataformat?view=aspnetcore-2.0) | <span data-ttu-id="29a27-204">`TicketDataFormat` 보호 및 id 및 쿠키 값에 저장 되어 있는 기타 속성을 보호 해제 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-204">The `TicketDataFormat` is used to protect and unprotect the identity and other properties that are stored in the cookie value.</span></span> <span data-ttu-id="29a27-205">을 지정 하지 않으면는 `TicketDataFormat` 사용 하 여 만들어집니다는 [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.dataprotectionprovider?view=aspnetcore-2.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-205">If not provided, a `TicketDataFormat` is created using the [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.dataprotectionprovider?view=aspnetcore-2.0).</span></span> |
| [<span data-ttu-id="29a27-206">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="29a27-206">Validate</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions.validate?view=aspnetcore-2.0) | <span data-ttu-id="29a27-207">옵션은 유효한 지 확인 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="29a27-207">Method that checks that the options are valid.</span></span> |

<span data-ttu-id="29a27-208">설정 `CookieAuthenticationOptions` 에서 인증을 위해 서비스 구성에는 `ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="29a27-208">Set `CookieAuthenticationOptions` in the service configuration for authentication in the `ConfigureServices` method:</span></span>

```csharp
services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
    .AddCookie(options =>
    {
        ...
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="29a27-209">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="29a27-209">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="29a27-210">ASP.NET Core 1.x 사용 하 여 쿠키 [미들웨어](xref:fundamentals/middleware/index) 암호화 된 쿠키에 사용자 계정을 serialize 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-210">ASP.NET Core 1.x uses cookie [middleware](xref:fundamentals/middleware/index) that serializes a user principal into an encrypted cookie.</span></span> <span data-ttu-id="29a27-211">이후 요청에서 쿠키의 유효성이 확인 되 고 주 서버는 다시에 할당 된 `HttpContext.User` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-211">On subsequent requests, the cookie is validated, and the principal is recreated and assigned to the `HttpContext.User` property.</span></span>

<span data-ttu-id="29a27-212">설치는 [Microsoft.AspNetCore.Authentication.Cookies](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Cookies/) 프로젝트에서 NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-212">Install the [Microsoft.AspNetCore.Authentication.Cookies](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Cookies/) NuGet package in your project.</span></span> <span data-ttu-id="29a27-213">이 패키지는 쿠키 미들웨어를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-213">This package contains the cookie middleware.</span></span>

<span data-ttu-id="29a27-214">사용 하 여는 `UseCookieAuthentication` 에서 메서드는 `Configure` 메서드에서 프로그램 *Startup.cs* 하기 전에 파일 `UseMvc` 또는 `UseMvcWithDefaultRoute`:</span><span class="sxs-lookup"><span data-stu-id="29a27-214">Use the `UseCookieAuthentication` method in the `Configure` method in your *Startup.cs* file before `UseMvc` or `UseMvcWithDefaultRoute`:</span></span>

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions()
{
    AccessDeniedPath = "/Account/Forbidden/",
    AuthenticationScheme = CookieAuthenticationDefaults.AuthenticationScheme,
    AutomaticAuthenticate = true,
    AutomaticChallenge = true,
    LoginPath = "/Account/Unauthorized/"
});
```

<span data-ttu-id="29a27-215">**CookieAuthenticationOptions 옵션**</span><span class="sxs-lookup"><span data-stu-id="29a27-215">**CookieAuthenticationOptions Options**</span></span>

<span data-ttu-id="29a27-216">[CookieAuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.CookieAuthenticationOptions?view=aspnetcore-1.1) 클래스는 인증 공급자 옵션을 구성 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-216">The [CookieAuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.CookieAuthenticationOptions?view=aspnetcore-1.1) class is used to configure the authentication provider options.</span></span>

| <span data-ttu-id="29a27-217">옵션</span><span class="sxs-lookup"><span data-stu-id="29a27-217">Option</span></span> | <span data-ttu-id="29a27-218">설명</span><span class="sxs-lookup"><span data-stu-id="29a27-218">Description</span></span> |
| ------ | ----------- |
| [<span data-ttu-id="29a27-219">AuthenticationScheme</span><span class="sxs-lookup"><span data-stu-id="29a27-219">AuthenticationScheme</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.authenticationscheme?view=aspnetcore-1.1) | <span data-ttu-id="29a27-220">인증 체계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-220">Sets the authentication scheme.</span></span> <span data-ttu-id="29a27-221">`AuthenticationScheme` 인증의 여러 인스턴스가 있는 하려는 경우 유용 [특정 스키마를 가진 권한 부여](xref:security/authorization/limitingidentitybyscheme)합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-221">`AuthenticationScheme` is useful when there are multiple instances of authentication and you want to [authorize with a specific scheme](xref:security/authorization/limitingidentitybyscheme).</span></span> <span data-ttu-id="29a27-222">설정의 `AuthenticationScheme` 를 `CookieAuthenticationDefaults.AuthenticationScheme` 체계 "쿠키"의 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-222">Setting the `AuthenticationScheme` to `CookieAuthenticationDefaults.AuthenticationScheme` provides a value of "Cookies" for the scheme.</span></span> <span data-ttu-id="29a27-223">체계를 구별 하는 임의의 문자열 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-223">You can supply any string value that distinguishes the scheme.</span></span> |
| [<span data-ttu-id="29a27-224">AutomaticAuthenticate</span><span class="sxs-lookup"><span data-stu-id="29a27-224">AutomaticAuthenticate</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.automaticauthenticate?view=aspnetcore-1.1) | <span data-ttu-id="29a27-225">쿠키 인증 모든 요청에 대해 실행 및 유효성 검사 하 고 자신이 만든 직렬화 된 모든 보안 주체를 재구성 있는지를 나타내는 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-225">Sets a value to indicate that the cookie authentication should run on every request and attempt to validate and reconstruct any serialized principal it created.</span></span> |
| [<span data-ttu-id="29a27-226">AutomaticChallenge</span><span class="sxs-lookup"><span data-stu-id="29a27-226">AutomaticChallenge</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.automaticchallenge?view=aspnetcore-1.1) | <span data-ttu-id="29a27-227">True 이면 인증 미들웨어 자동 문제를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-227">If true, the authentication middleware handles automatic challenges.</span></span> <span data-ttu-id="29a27-228">경우 false 이면 인증 미들웨어만 변경 하 여 명시적으로 지정 하는 경우 응답은 `AuthenticationScheme`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-228">If false, the authentication middleware only alters responses when explicitly indicated by the `AuthenticationScheme`.</span></span> |
| [<span data-ttu-id="29a27-229">ClaimsIssuer</span><span class="sxs-lookup"><span data-stu-id="29a27-229">ClaimsIssuer</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.claimsissuer?view=aspnetcore-1.1) | <span data-ttu-id="29a27-230">에 사용할 발급자는 [발급자](/dotnet/api/system.security.claims.claim.issuer) 쿠키 인증 미들웨어에서 만든 클레임의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-230">The issuer to use for the [Issuer](/dotnet/api/system.security.claims.claim.issuer) property on any claims created by the cookie authentication middleware.</span></span> |
| [<span data-ttu-id="29a27-231">CookieDomain</span><span class="sxs-lookup"><span data-stu-id="29a27-231">CookieDomain</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiedomain?view=aspnetcore-1.1) | <span data-ttu-id="29a27-232">쿠키 처리 되는 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-232">The domain name where the cookie is served.</span></span> <span data-ttu-id="29a27-233">기본적으로 요청 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-233">By default, this is the host name of the request.</span></span> <span data-ttu-id="29a27-234">브라우저 쿠키를 일치 하는 호스트 이름으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-234">The browser only serves the cookie to a matching host name.</span></span> <span data-ttu-id="29a27-235">이 도메인의 모든 호스트에 사용할 수 있는 쿠키를 조정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-235">You may wish to adjust this to have cookies available to any host in your domain.</span></span> <span data-ttu-id="29a27-236">예를 들어 쿠키 도메인 설정 `.contoso.com` 를 사용할 수 있도록 `contoso.com`, `www.contoso.com`, 및 `staging.www.contoso.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-236">For example, setting the cookie domain to `.contoso.com` makes it available to `contoso.com`, `www.contoso.com`, and `staging.www.contoso.com`.</span></span> |
| [<span data-ttu-id="29a27-237">CookieHttpOnly</span><span class="sxs-lookup"><span data-stu-id="29a27-237">CookieHttpOnly</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiehttponly?view=aspnetcore-1.1) | <span data-ttu-id="29a27-238">쿠키를 서버에만 액세스할 수 있어야 하는 경우를 나타내는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-238">A flag indicating if the cookie should be accessible only to servers.</span></span> <span data-ttu-id="29a27-239">이 값을 변경 `false` 쿠키에 액세스 하는 클라이언트 쪽 스크립트를 허용 하 고 표시 하며 열림 앱이 쿠키 도용 앱 있어야는 [교차 사이트 스크립팅 (XSS)](xref:security/cross-site-scripting) 취약점입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-239">Changing this value to `false` permits client-side scripts to access the cookie and may open your app to cookie theft should your app have a [Cross-site scripting (XSS)](xref:security/cross-site-scripting) vulnerability.</span></span> <span data-ttu-id="29a27-240">기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-240">The default value is `true`.</span></span> |
| [<span data-ttu-id="29a27-241">CookiePath</span><span class="sxs-lookup"><span data-stu-id="29a27-241">CookiePath</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiepath?view=aspnetcore-1.1) | <span data-ttu-id="29a27-242">동일한 호스트 이름에서 실행 되는 앱을 격리 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-242">Used to isolate apps running on the same host name.</span></span> <span data-ttu-id="29a27-243">실행 중인 앱이 있는 경우 `/app1` 및 해당 응용 프로그램에 쿠키를 제한 하려면 설정는 `CookiePath` 속성을 `/app1`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-243">If you have an app running at `/app1` and want to restrict cookies to that app, set the `CookiePath` property to `/app1`.</span></span> <span data-ttu-id="29a27-244">이러한 작업을 통해 쿠키는 에서만 사용할 수에 대 한 요청 `/app1` 아래에 있는 모든 응용 프로그램 및입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-244">By doing so, the cookie is only available on requests to `/app1` and any app underneath it.</span></span> |
| [<span data-ttu-id="29a27-245">CookieSecure</span><span class="sxs-lookup"><span data-stu-id="29a27-245">CookieSecure</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiesecure?view=aspnetcore-1.1) | <span data-ttu-id="29a27-246">만든 쿠키를 HTTPS로 제한 해야 하는 경우를 나타내는 플래그 (`CookieSecurePolicy.Always`), HTTP 또는 HTTPS (`CookieSecurePolicy.None`), 또는 요청와 동일한 프로토콜 (`CookieSecurePolicy.SameAsRequest`).</span><span class="sxs-lookup"><span data-stu-id="29a27-246">A flag indicating if the cookie created should be limited to HTTPS (`CookieSecurePolicy.Always`), HTTP or HTTPS (`CookieSecurePolicy.None`), or the same protocol as the request (`CookieSecurePolicy.SameAsRequest`).</span></span> <span data-ttu-id="29a27-247">기본값은 `CookieSecurePolicy.SameAsRequest`입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-247">The default value is `CookieSecurePolicy.SameAsRequest`.</span></span> |
| [<span data-ttu-id="29a27-248">설명</span><span class="sxs-lookup"><span data-stu-id="29a27-248">Description</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.description?view=aspnetcore-1.1) | <span data-ttu-id="29a27-249">응용 프로그램에 사용할 수 있는 인증 형식에 대 한 추가 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-249">Additional information about the authentication type which is made available to the app.</span></span> |
| [<span data-ttu-id="29a27-250">ExpireTimeSpan</span><span class="sxs-lookup"><span data-stu-id="29a27-250">ExpireTimeSpan</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.expiretimespan?view=aspnetcore-1.1) | <span data-ttu-id="29a27-251">`TimeSpan` 인증 티켓이 만료 된 이후입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-251">The `TimeSpan` after which the authentication ticket expires.</span></span> <span data-ttu-id="29a27-252">티켓에 대 한 만료 시간을 생성 하는 현재 시간에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-252">It's added to the current time to create the expiration time for the ticket.</span></span> <span data-ttu-id="29a27-253">사용 하도록 `ExpireTimeSpan`, 설정 해야 `IsPersistent` 를 `true` 에 `AuthenticationProperties` 에 전달 된 `SignInAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-253">To use `ExpireTimeSpan`, you must set `IsPersistent` to `true` in the `AuthenticationProperties` passed to `SignInAsync`.</span></span> <span data-ttu-id="29a27-254">기본값은 14 일입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-254">The default value is 14 days.</span></span> |
| [<span data-ttu-id="29a27-255">SlidingExpiration</span><span class="sxs-lookup"><span data-stu-id="29a27-255">SlidingExpiration</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.slidingexpiration?view=aspnetcore-1.1) | <span data-ttu-id="29a27-256">이상의 절반 쿠키 만료 날짜를 다시 설정 하는지 여부를 나타내는 플래그는 `ExpireTimeSpan` 관리가 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-256">A flag indicating whether the cookie expiration date resets when more than half of the `ExpireTimeSpan` interval has passed.</span></span> <span data-ttu-id="29a27-257">새 exipiration 시간 앞으로 이동 하는 현재 날짜와 `ExpireTimespan`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-257">The new exipiration time is moved forward to be the current date plus the `ExpireTimespan`.</span></span> <span data-ttu-id="29a27-258">[절대 쿠키 만료 시간](xref:security/authentication/cookie#absolute-cookie-expiration) 를 사용 하 여 설정할 수는 `AuthenticationProperties` 클래스를 호출할 때 `SignInAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-258">An [absolute cookie expiration time](xref:security/authentication/cookie#absolute-cookie-expiration) can be set by using the `AuthenticationProperties` class when calling `SignInAsync`.</span></span> <span data-ttu-id="29a27-259">절대 만료 시간 인증 쿠키가 유효 하다는 시간의 양을 제한 하 여 응용 프로그램의 보안을 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-259">An absolute expiration time can improve the security of your app by limiting the amount of time that the authentication cookie is valid.</span></span> <span data-ttu-id="29a27-260">기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-260">The default value is `true`.</span></span> |

<span data-ttu-id="29a27-261">설정 `CookieAuthenticationOptions` 에서 쿠키 인증 미들웨어에 대 한는 `Configure` 메서드:</span><span class="sxs-lookup"><span data-stu-id="29a27-261">Set `CookieAuthenticationOptions` for the Cookie Authentication Middleware in the `Configure` method:</span></span>

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    ...
});
```

---

## <a name="cookie-policy-middleware"></a><span data-ttu-id="29a27-262">쿠키 정책 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-262">Cookie Policy Middleware</span></span>

<span data-ttu-id="29a27-263">[쿠키 정책 미들웨어](/dotnet/api/microsoft.aspnetcore.cookiepolicy.cookiepolicymiddleware) 응용 프로그램의 쿠키 정책 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-263">[Cookie Policy Middleware](/dotnet/api/microsoft.aspnetcore.cookiepolicy.cookiepolicymiddleware) enables cookie policy capabilities in an app.</span></span> <span data-ttu-id="29a27-264">중요 한; 순서는 응용 프로그램 처리 파이프라인에 미들웨어를 추가 또한 파이프라인에서 그 뒤에 등록 된 구성 요소를만 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-264">Adding the middleware to the app processing pipeline is order sensitive; it only affects components registered after it in the pipeline.</span></span>

```csharp
app.UseCookiePolicy(cookiePolicyOptions);
```

 <span data-ttu-id="29a27-265">[CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions) 쿠키 정책 미들웨어에 제공 된 쿠키를 추가 하거나 삭제할 때 쿠키 처리 처리기에 쿠키 처리 및 후크의 전역 특성을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-265">The [CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions) provided to the Cookie Policy Middleware allow you to control global characteristics of cookie processing and hook into cookie processing handlers when cookies are appended or deleted.</span></span>

| <span data-ttu-id="29a27-266">속성</span><span class="sxs-lookup"><span data-stu-id="29a27-266">Property</span></span> | <span data-ttu-id="29a27-267">설명</span><span class="sxs-lookup"><span data-stu-id="29a27-267">Description</span></span> |
| -------- | ----------- |
| [<span data-ttu-id="29a27-268">HttpOnly</span><span class="sxs-lookup"><span data-stu-id="29a27-268">HttpOnly</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.httponly) | <span data-ttu-id="29a27-269">쿠키 HttpOnly 이어야 하는 여부를 나타내는 플래그 쿠키 서버에만 액세스할 수 있어야 하는 경우 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-269">Affects whether cookies must be HttpOnly, which is a flag indicating if the cookie should be accessible only to servers.</span></span> <span data-ttu-id="29a27-270">기본값은 `HttpOnlyPolicy.None`입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-270">The default value is `HttpOnlyPolicy.None`.</span></span> |
| [<span data-ttu-id="29a27-271">MinimumSameSitePolicy</span><span class="sxs-lookup"><span data-stu-id="29a27-271">MinimumSameSitePolicy</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.minimumsamesitepolicy) | <span data-ttu-id="29a27-272">쿠키의 동일한 사이트 특성을 (아래 참조)에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-272">Affects the cookie's same-site attribute (see below).</span></span> <span data-ttu-id="29a27-273">기본값은 `SameSiteMode.Lax`입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-273">The default value is `SameSiteMode.Lax`.</span></span> <span data-ttu-id="29a27-274">이 옵션은 ASP.NET Core 2.0 이상에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-274">This option is available for ASP.NET Core 2.0+.</span></span> |
| [<span data-ttu-id="29a27-275">OnAppendCookie</span><span class="sxs-lookup"><span data-stu-id="29a27-275">OnAppendCookie</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.onappendcookie) | <span data-ttu-id="29a27-276">에 쿠키를 추가 하는 경우 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-276">Called when a cookie is appended.</span></span> |
| [<span data-ttu-id="29a27-277">OnDeleteCookie</span><span class="sxs-lookup"><span data-stu-id="29a27-277">OnDeleteCookie</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.ondeletecookie) | <span data-ttu-id="29a27-278">쿠키가 삭제 되 면 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-278">Called when a cookie is deleted.</span></span> |
| [<span data-ttu-id="29a27-279">보안</span><span class="sxs-lookup"><span data-stu-id="29a27-279">Secure</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.secure) | <span data-ttu-id="29a27-280">쿠키도 Secure 해야 하는지 여부를 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-280">Affects whether cookies must be Secure.</span></span> <span data-ttu-id="29a27-281">기본값은 `CookieSecurePolicy.None`입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-281">The default value is `CookieSecurePolicy.None`.</span></span> |

<span data-ttu-id="29a27-282">**MinimumSameSitePolicy** (ASP.NET 코어 2.0 +만)</span><span class="sxs-lookup"><span data-stu-id="29a27-282">**MinimumSameSitePolicy** (ASP.NET Core 2.0+ only)</span></span>

<span data-ttu-id="29a27-283">기본 `MinimumSameSitePolicy` 값은 `SameSiteMode.Lax` OAuth2 인증을 허용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-283">The default `MinimumSameSitePolicy` value is `SameSiteMode.Lax` to permit OAuth2 authentication.</span></span> <span data-ttu-id="29a27-284">엄격 하 게 하는 동일한 사이트 정책을 적용 하려면 `SameSiteMode.Strict`로 설정 된 `MinimumSameSitePolicy`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-284">To strictly enforce a same-site policy of `SameSiteMode.Strict`, set the `MinimumSameSitePolicy`.</span></span> <span data-ttu-id="29a27-285">이 설정은 나누기 OAuth2 및 다른 크로스-원본 인증 체계, 하지만 다른 유형의 크로스-원본 요청을 처리 하지 않아도 되는 앱에 대 한 쿠키 보안 수준을 승격 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-285">Although this setting breaks OAuth2 and other cross-origin authentication schemes, it elevates the level of cookie security for other types of apps that don't rely on cross-origin request processing.</span></span>

```csharp
var cookiePolicyOptions = new CookiePolicyOptions
{
    MinimumSameSitePolicy = SameSiteMode.Strict,
};
```

<span data-ttu-id="29a27-286">에 대 한 쿠키 정책 미들웨어 설정 `MinimumSameSitePolicy` 의 설정에 영향을 줄 수 `Cookie.SameSite` 에 `CookieAuthenticationOptions` 아래 표를 참조에 따라 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-286">The Cookie Policy Middleware setting for `MinimumSameSitePolicy` can affect your setting of `Cookie.SameSite` in `CookieAuthenticationOptions` settings according to the matrix below.</span></span>

| <span data-ttu-id="29a27-287">MinimumSameSitePolicy</span><span class="sxs-lookup"><span data-stu-id="29a27-287">MinimumSameSitePolicy</span></span> | <span data-ttu-id="29a27-288">Cookie.SameSite</span><span class="sxs-lookup"><span data-stu-id="29a27-288">Cookie.SameSite</span></span> | <span data-ttu-id="29a27-289">결과 Cookie.SameSite 설정</span><span class="sxs-lookup"><span data-stu-id="29a27-289">Resultant Cookie.SameSite setting</span></span> |
| --------------------- | --------------- | --------------------------------- |
| <span data-ttu-id="29a27-290">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="29a27-290">SameSiteMode.None</span></span>     | <span data-ttu-id="29a27-291">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="29a27-291">SameSiteMode.None</span></span><br><span data-ttu-id="29a27-292">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="29a27-292">SameSiteMode.Lax</span></span><br><span data-ttu-id="29a27-293">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="29a27-293">SameSiteMode.Strict</span></span> | <span data-ttu-id="29a27-294">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="29a27-294">SameSiteMode.None</span></span><br><span data-ttu-id="29a27-295">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="29a27-295">SameSiteMode.Lax</span></span><br><span data-ttu-id="29a27-296">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="29a27-296">SameSiteMode.Strict</span></span> |
| <span data-ttu-id="29a27-297">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="29a27-297">SameSiteMode.Lax</span></span>      | <span data-ttu-id="29a27-298">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="29a27-298">SameSiteMode.None</span></span><br><span data-ttu-id="29a27-299">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="29a27-299">SameSiteMode.Lax</span></span><br><span data-ttu-id="29a27-300">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="29a27-300">SameSiteMode.Strict</span></span> | <span data-ttu-id="29a27-301">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="29a27-301">SameSiteMode.Lax</span></span><br><span data-ttu-id="29a27-302">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="29a27-302">SameSiteMode.Lax</span></span><br><span data-ttu-id="29a27-303">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="29a27-303">SameSiteMode.Strict</span></span> |
| <span data-ttu-id="29a27-304">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="29a27-304">SameSiteMode.Strict</span></span>   | <span data-ttu-id="29a27-305">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="29a27-305">SameSiteMode.None</span></span><br><span data-ttu-id="29a27-306">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="29a27-306">SameSiteMode.Lax</span></span><br><span data-ttu-id="29a27-307">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="29a27-307">SameSiteMode.Strict</span></span> | <span data-ttu-id="29a27-308">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="29a27-308">SameSiteMode.Strict</span></span><br><span data-ttu-id="29a27-309">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="29a27-309">SameSiteMode.Strict</span></span><br><span data-ttu-id="29a27-310">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="29a27-310">SameSiteMode.Strict</span></span> |

## <a name="create-an-authentication-cookie"></a><span data-ttu-id="29a27-311">인증 쿠키를 만드는</span><span class="sxs-lookup"><span data-stu-id="29a27-311">Create an authentication cookie</span></span>

<span data-ttu-id="29a27-312">사용자 정보를 보관 하는 쿠키를 만들려면 먼저 생성 해야는 [ClaimsPrincipal](/dotnet/api/system.security.claims.claimsprincipal)합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-312">To create a cookie holding user information, you must construct a [ClaimsPrincipal](/dotnet/api/system.security.claims.claimsprincipal).</span></span> <span data-ttu-id="29a27-313">사용자 정보 직렬화 되며 쿠키에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-313">The user information is serialized and stored in the cookie.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="29a27-314">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="29a27-314">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="29a27-315">만들기는 [ClaimsIdentity](/dotnet/api/system.security.claims.claimsidentity) 와 모든 필수 [클레임](/dotnet/api/system.security.claims.claim)s 및 호출 [SignInAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signinasync?view=aspnetcore-2.0) 사용자 로그인:</span><span class="sxs-lookup"><span data-stu-id="29a27-315">Create a [ClaimsIdentity](/dotnet/api/system.security.claims.claimsidentity) with any required [Claim](/dotnet/api/system.security.claims.claim)s and call [SignInAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signinasync?view=aspnetcore-2.0) to sign in the user:</span></span>

[!code-csharp[](cookie/samples/2.x/CookieSample/Pages/Account/Login.cshtml.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="29a27-316">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="29a27-316">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="29a27-317">호출 [SignInAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1.signinasync?view=aspnetcore-1.1) 사용자에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-317">Call [SignInAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1.signinasync?view=aspnetcore-1.1) to sign in the user:</span></span>

```csharp
await HttpContext.Authentication.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity));
```

---

<span data-ttu-id="29a27-318">`SignInAsync` 암호화 된 쿠키를 만들어 현재 응답에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-318">`SignInAsync` creates an encrypted cookie and adds it to the current response.</span></span> <span data-ttu-id="29a27-319">지정 하지 않으면 프로그램 `AuthenticationScheme`, 기본 체계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-319">If you don't specify an `AuthenticationScheme`, the default scheme is used.</span></span>

<span data-ttu-id="29a27-320">내부적으로 사용 되는 암호화는 ASP.NET Core [데이터 보호](xref:security/data-protection/using-data-protection#security-data-protection-getting-started) 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-320">Under the covers, the encryption used is ASP.NET Core's [Data Protection](xref:security/data-protection/using-data-protection#security-data-protection-getting-started) system.</span></span> <span data-ttu-id="29a27-321">여러 컴퓨터, 앱, 부하 분산 또는 웹 팜을 사용 하 여 응용 프로그램을 호스트 하 고 있는 경우 다음을 수행 해야 [데이터 보호를 구성](xref:security/data-protection/configuration/overview) 동일한 키 링과 응용 프로그램 식별자를 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-321">If you're hosting app on multiple machines, load balancing across apps, or using a web farm, then you must [configure data protection](xref:security/data-protection/configuration/overview) to use the same key ring and app identifier.</span></span>

## <a name="sign-out"></a><span data-ttu-id="29a27-322">로그아웃</span><span class="sxs-lookup"><span data-stu-id="29a27-322">Sign out</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="29a27-323">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="29a27-323">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="29a27-324">로그 아웃 현재 사용자를 해당 쿠키를 삭제 하려면 호출 [SignOutAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signoutasync?view=aspnetcore-2.0):</span><span class="sxs-lookup"><span data-stu-id="29a27-324">To sign out the current user and delete their cookie, call [SignOutAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signoutasync?view=aspnetcore-2.0):</span></span>

[!code-csharp[](cookie/samples/2.x/CookieSample/Pages/Account/Login.cshtml.cs?name=snippet2)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="29a27-325">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="29a27-325">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="29a27-326">로그 아웃 현재 사용자를 해당 쿠키를 삭제 하려면 호출 [SignOutAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1.signoutasync?view=aspnetcore-1.1):</span><span class="sxs-lookup"><span data-stu-id="29a27-326">To sign out the current user and delete their cookie, call [SignOutAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1.signoutasync?view=aspnetcore-1.1):</span></span>

```csharp
await HttpContext.Authentication.SignOutAsync(
    CookieAuthenticationDefaults.AuthenticationScheme);
```

---

<span data-ttu-id="29a27-327">사용 하지 않으려면 `CookieAuthenticationDefaults.AuthenticationScheme` (또는 "쿠키")의 체계 (예: "ContosoCookie")로 인증 공급자를 구성할 때 사용 하는 체계를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-327">If you aren't using `CookieAuthenticationDefaults.AuthenticationScheme` (or "Cookies") as the scheme (for example, "ContosoCookie"), supply the scheme you used when configuring the authentication provider.</span></span> <span data-ttu-id="29a27-328">그렇지 않은 경우 기본 구성표가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-328">Otherwise, the default scheme is used.</span></span>

## <a name="react-to-back-end-changes"></a><span data-ttu-id="29a27-329">백 엔드 변경 내용에 대응</span><span class="sxs-lookup"><span data-stu-id="29a27-329">React to back-end changes</span></span>

<span data-ttu-id="29a27-330">쿠키를 만든 후에 id의 단일 원본이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-330">Once a cookie is created, it becomes the single source of identity.</span></span> <span data-ttu-id="29a27-331">백 엔드 시스템에 사용자를 비활성화 하는 경우에 쿠키 인증 시스템에이 알지 및 해당 쿠키의 유효으로 사용자 로그인 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-331">Even if you disable a user in your back-end systems, the cookie authentication system has no knowledge of this, and a user stays logged in as long as their cookie is valid.</span></span>

<span data-ttu-id="29a27-332">[ValidatePrincipal](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationevents.validateprincipal) 에서 ASP.NET Core 이벤트 2.x 또는 [ValidateAsync](/dotnet/api/microsoft.aspnetcore.identity.isecuritystampvalidator.validateasync?view=aspnetcore-1.1) 메서드에서 ASP.NET Core 1.x를 가로채 고 쿠키 id의 유효성 검사 재정의에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-332">The [ValidatePrincipal](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationevents.validateprincipal) event in ASP.NET Core 2.x or the [ValidateAsync](/dotnet/api/microsoft.aspnetcore.identity.isecuritystampvalidator.validateasync?view=aspnetcore-1.1) method in ASP.NET Core 1.x can be used to intercept and override validation of the cookie identity.</span></span> <span data-ttu-id="29a27-333">이 방법은 응용 프로그램에 액세스 하는 해지 된 사용자의 위험을 완화 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-333">This approach mitigates the risk of revoked users accessing the app.</span></span>

<span data-ttu-id="29a27-334">한 가지 방법은 쿠키 유효성 검사를 기반으로 사용자 데이터베이스 변경 된 경우에 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-334">One approach to cookie validation is based on keeping track of when the user database has been changed.</span></span> <span data-ttu-id="29a27-335">데이터베이스 사용자의 쿠키에 발급 된 이후 변경 되지 않은 경우에 사용자를 해당 쿠키가 여전히 유효한 경우 다시 인증 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-335">If the database hasn't been changed since the user's cookie was issued, there's no need to re-authenticate the user if their cookie is still valid.</span></span> <span data-ttu-id="29a27-336">이 시나리오에서 구현 되는 데이터베이스를 구현 하려면 `IUserRepository` 이 예제에서는 저장 한 `LastChanged` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-336">To implement this scenario, the database, which is implemented in `IUserRepository` for this example, stores a `LastChanged` value.</span></span> <span data-ttu-id="29a27-337">모든 사용자는 데이터베이스에서 업데이트 될 때의 `LastChanged` 값이 현재 시간으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-337">When any user is updated in the database, the `LastChanged` value is set to the current time.</span></span>

<span data-ttu-id="29a27-338">데이터베이스 변경 내용을 기반으로 하는 경우 쿠키를 무효화 하기 위해는 `LastChanged` 값, 쿠키와 만들기는 `LastChanged` 현재 포함 된 클레임 `LastChanged` 데이터베이스에서 값:</span><span class="sxs-lookup"><span data-stu-id="29a27-338">In order to invalidate a cookie when the database changes based on the `LastChanged` value, create the cookie with a `LastChanged` claim containing the current `LastChanged` value from the database:</span></span>

```csharp
var claims = new List<Claim>
{
    new Claim(ClaimTypes.Name, user.Email),
    new Claim("LastChanged", {Database Value})
};

var claimsIdentity = new ClaimsIdentity(
    claims, 
    CookieAuthenticationDefaults.AuthenticationScheme);

await HttpContext.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme, 
    new ClaimsPrincipal(claimsIdentity));
```

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="29a27-339">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="29a27-339">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="29a27-340">에 대 한 재정의 구현 하는 `ValidatePrincipal` 이벤트, 메서드에서 파생 되는 클래스에 다음 서명 사용 하 여 쓰기 [CookieAuthenticationEvents](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationevents):</span><span class="sxs-lookup"><span data-stu-id="29a27-340">To implement an override for the `ValidatePrincipal` event, write a method with the following signature in a class that you derive from [CookieAuthenticationEvents](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationevents):</span></span>

```csharp
ValidatePrincipal(CookieValidatePrincipalContext)
```

<span data-ttu-id="29a27-341">예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-341">An example looks like the following:</span></span>

```csharp
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Authentication;
using Microsoft.AspNetCore.Authentication.Cookies;

public class CustomCookieAuthenticationEvents : CookieAuthenticationEvents
{
    private readonly IUserRepository _userRepository;

    public CustomCookieAuthenticationEvents(IUserRepository userRepository)
    {
        // Get the database from registered DI services.
        _userRepository = userRepository;
    }

    public override async Task ValidatePrincipal(CookieValidatePrincipalContext context)
    {
        var userPrincipal = context.Principal;

        // Look for the LastChanged claim.
        var lastChanged = (from c in userPrincipal.Claims
                           where c.Type == "LastChanged"
                           select c.Value).FirstOrDefault();

        if (string.IsNullOrEmpty(lastChanged) ||
            !_userRepository.ValidateLastChanged(lastChanged))
        {
            context.RejectPrincipal();

            await context.HttpContext.SignOutAsync(
                CookieAuthenticationDefaults.AuthenticationScheme);
        }
    }
}
```

<span data-ttu-id="29a27-342">쿠키 service 등록 하는 동안 이벤트 인스턴스를 등록 된 `ConfigureServices` 메서드.</span><span class="sxs-lookup"><span data-stu-id="29a27-342">Register the events instance during cookie service registration in the `ConfigureServices` method.</span></span> <span data-ttu-id="29a27-343">에 대 한 범위 지정 된 서비스 등록을 제공 하면 `CustomCookieAuthenticationEvents` 클래스:</span><span class="sxs-lookup"><span data-stu-id="29a27-343">Provide a scoped service registration for your `CustomCookieAuthenticationEvents` class:</span></span>

```csharp
services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
    .AddCookie(options =>
    {
        options.EventsType = typeof(CustomCookieAuthenticationEvents);
    });

services.AddScoped<CustomCookieAuthenticationEvents>();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="29a27-344">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="29a27-344">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="29a27-345">에 대 한 재정의 구현 하는 `ValidateAsync` 이벤트, 메서드는 다음 서명 가진 쓰기:</span><span class="sxs-lookup"><span data-stu-id="29a27-345">To implement an override for the `ValidateAsync` event, write a method with the following signature:</span></span>

```csharp
ValidateAsync(CookieValidatePrincipalContext)
```

<span data-ttu-id="29a27-346">ASP.NET Core Id의 일부로이 검사를 구현 하는 [SecurityStampValidator](/dotnet/api/microsoft.aspnetcore.identity.securitystampvalidator-1.validateasync)합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-346">ASP.NET Core Identity implements this check as part of its [SecurityStampValidator](/dotnet/api/microsoft.aspnetcore.identity.securitystampvalidator-1.validateasync).</span></span> <span data-ttu-id="29a27-347">예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-347">An example looks like the following:</span></span>

```csharp
public static class LastChangedValidator
{
    public static async Task ValidateAsync(CookieValidatePrincipalContext context)
    {
        // Pull database from registered DI services.
        var userRepository = 
            context.HttpContext.RequestServices
                .GetRequiredService<IUserRepository>();
        var userPrincipal = context.Principal;

        // Look for the last changed claim.
        var lastChanged = (from c in userPrincipal.Claims
                           where c.Type == "LastChanged"
                           select c.Value).FirstOrDefault();

        if (string.IsNullOrEmpty(lastChanged) ||
            !userRepository.ValidateLastChanged(lastChanged))
        {
            context.RejectPrincipal();

            await context.HttpContext.SignOutAsync(
                CookieAuthenticationDefaults.AuthenticationScheme);
        }
    }
}
```

<span data-ttu-id="29a27-348">쿠키 인증 구성 중 이벤트를 등록 된 `Configure` 메서드:</span><span class="sxs-lookup"><span data-stu-id="29a27-348">Register the event during cookie authentication configuration in the `Configure` method:</span></span>

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    Events = new CookieAuthenticationEvents
    {
        OnValidatePrincipal = LastChangedValidator.ValidateAsync
    }
});
```

---

<span data-ttu-id="29a27-349">사용자의 이름이 업데이트 되는 상황을 생각해 봅시다 &mdash; 주는 작업에 어떤 방식으로든에서 보안에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-349">Consider a situation in which the user's name is updated &mdash; a decision that doesn't affect security in any way.</span></span> <span data-ttu-id="29a27-350">안전 하 게 사용자 계정이 업데이트 하려는 경우에 호출 `context.ReplacePrincipal` 설정 하 고는 `context.ShouldRenew` 속성을 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-350">If you want to non-destructively update the user principal, call `context.ReplacePrincipal` and set the `context.ShouldRenew` property to `true`.</span></span>

> [!WARNING]
> <span data-ttu-id="29a27-351">여기에서 설명 하는 방식은 모든 요청에 대해 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-351">The approach described here is triggered on every request.</span></span> <span data-ttu-id="29a27-352">이 앱에 대 한 성능이 크게 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-352">This can result in a large performance penalty for the app.</span></span>

## <a name="persistent-cookies"></a><span data-ttu-id="29a27-353">영구 쿠키</span><span class="sxs-lookup"><span data-stu-id="29a27-353">Persistent cookies</span></span>

<span data-ttu-id="29a27-354">쿠키 브라우저 세션 전체에서 유지 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-354">You may want the cookie to persist across browser sessions.</span></span> <span data-ttu-id="29a27-355">로그인 또는 유사한 메커니즘에서 "암호 저장" 확인란을 사용 하 여 명시적 사용자 동의와만이 지 속성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-355">This persistence should only be enabled with explicit user consent with a "Remember Me" checkbox on login or a similar mechanism.</span></span> 

<span data-ttu-id="29a27-356">다음 코드 조각 id 및 브라우저 클로저를 통해 되더라도 남아 있지만 해당 쿠키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-356">The following code snippet creates an identity and corresponding cookie that survives through browser closures.</span></span> <span data-ttu-id="29a27-357">이전에 구성 된 모든 상대 (sliding) 만료 설정은 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-357">Any sliding expiration settings previously configured are honored.</span></span> <span data-ttu-id="29a27-358">쿠키는 브라우저 종료 하는 동안 만료 되 면 다시 시작 되 면 브라우저 쿠키를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-358">If the cookie expires while the browser is closed, the browser clears the cookie once it's restarted.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="29a27-359">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="29a27-359">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
await HttpContext.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity),
    new AuthenticationProperties
    {
        IsPersistent = true
    });
```

<span data-ttu-id="29a27-360">[AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.authentication.authenticationproperties?view=aspnetcore-2.0) 에 위치 하는 클래스는 `Microsoft.AspNetCore.Authentication` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-360">The [AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.authentication.authenticationproperties?view=aspnetcore-2.0) class resides in the `Microsoft.AspNetCore.Authentication` namespace.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="29a27-361">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="29a27-361">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
await HttpContext.Authentication.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity),
    new AuthenticationProperties
    {
        IsPersistent = true
    });
```

<span data-ttu-id="29a27-362">[AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.http.authentication.authenticationproperties?view=aspnetcore-1.1) 에 위치 하는 클래스는 `Microsoft.AspNetCore.Http.Authentication` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-362">The [AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.http.authentication.authenticationproperties?view=aspnetcore-1.1) class resides in the `Microsoft.AspNetCore.Http.Authentication` namespace.</span></span>

---

## <a name="absolute-cookie-expiration"></a><span data-ttu-id="29a27-363">절대 쿠키 만료 기한</span><span class="sxs-lookup"><span data-stu-id="29a27-363">Absolute cookie expiration</span></span>

<span data-ttu-id="29a27-364">와 절대 만료 시간을 설정할 수 있습니다 `ExpiresUtc`합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-364">You can set an absolute expiration time with `ExpiresUtc`.</span></span> <span data-ttu-id="29a27-365">설정 해야 `IsPersistent`, 그렇지 않으면 `ExpiresUtc` 는 무시 됩니다 단일 세션 쿠키를 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-365">You must also set `IsPersistent`; otherwise, `ExpiresUtc` is ignored and a single-session cookie is created.</span></span> <span data-ttu-id="29a27-366">때 `ExpiresUtc` 에 설정 된 `SignInAsync`의 값이 재정의 `ExpireTimeSpan` 옵션의 `CookieAuthenticationOptions`경우 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-366">When `ExpiresUtc` is set on `SignInAsync`, it overrides the value of the `ExpireTimeSpan` option of `CookieAuthenticationOptions`, if set.</span></span>

<span data-ttu-id="29a27-367">다음 코드 조각 id 및는 20 분 동안 지속 되는 해당 쿠키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-367">The following code snippet creates an identity and corresponding cookie that lasts for 20 minutes.</span></span> <span data-ttu-id="29a27-368">이 이전에 구성 된 모든 상대 (sliding) 만료 설정을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="29a27-368">This ignores any sliding expiration settings previously configured.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="29a27-369">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="29a27-369">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
await HttpContext.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity),
    new AuthenticationProperties
    {
        IsPersistent = true,
        ExpiresUtc = DateTime.UtcNow.AddMinutes(20)
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="29a27-370">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="29a27-370">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
await HttpContext.Authentication.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity),
    new AuthenticationProperties
    {
        IsPersistent = true,
        ExpiresUtc = DateTime.UtcNow.AddMinutes(20)
    });
```

---

## <a name="additional-resources"></a><span data-ttu-id="29a27-371">추가 자료</span><span class="sxs-lookup"><span data-stu-id="29a27-371">Additional resources</span></span>

* [<span data-ttu-id="29a27-372">Auth 2.0 변경 / 마이그레이션 알림</span><span class="sxs-lookup"><span data-stu-id="29a27-372">Auth 2.0 Changes / Migration Announcement</span></span>](https://github.com/aspnet/Announcements/issues/262)
* [<span data-ttu-id="29a27-373">구성표로 ID 제한</span><span class="sxs-lookup"><span data-stu-id="29a27-373">Limit identity by scheme</span></span>](xref:security/authorization/limitingidentitybyscheme)
* [<span data-ttu-id="29a27-374">클레임 기반 권한 부여</span><span class="sxs-lookup"><span data-stu-id="29a27-374">Claims-Based Authorization</span></span>](xref:security/authorization/claims)
* [<span data-ttu-id="29a27-375">정책 기반 역할 검사</span><span class="sxs-lookup"><span data-stu-id="29a27-375">Policy-based role checks</span></span>](xref:security/authorization/roles#policy-based-role-checks)
