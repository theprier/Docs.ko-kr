---
title: "ASP.NET Core로 특정 구성표-권한 부여"
author: rick-anderson
description: "이 문서에서는 여러 가지 인증 방법을 사용할 때 id는 특정 체계를 제한 하는 방법을 설명 합니다."
ms.author: riande
manager: wpickett
ms.date: 10/12/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/limitingidentitybyscheme
ms.openlocfilehash: 099dba1a4235ef62ea298748645b99e2d6d12d44
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="authorize-with-a-specific-scheme"></a><span data-ttu-id="502b1-103">특정 구성표로 권한 부여</span><span class="sxs-lookup"><span data-stu-id="502b1-103">Authorize with a specific scheme</span></span>

<span data-ttu-id="502b1-104">단일 페이지 응용 프로그램 (SPAs)와 같은 일부 시나리오에서는 일반적으로 여러 인증 방법을 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-104">In some scenarios, such as Single Page Applications (SPAs), it's common to use multiple authentication methods.</span></span> <span data-ttu-id="502b1-105">예를 들어 응용 프로그램 JavaScript 요청에 대 한 로그인 쿠키 기반 인증 및 JWT 전달자 인증 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-105">For example, the app may use cookie-based authentication to log in and JWT bearer authentication for JavaScript requests.</span></span> <span data-ttu-id="502b1-106">경우에 따라 응용 프로그램 인증 처리기를 여러 개 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-106">In some cases, the app may have multiple instances of an authentication handler.</span></span> <span data-ttu-id="502b1-107">예를 들어 기본적인 id를 포함 한 두 명의 쿠키 처리기와 multi-factor authentication (MFA)가 트리거되면 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-107">For example, two cookie handlers where one contains a basic identity and one is created when a multi-factor authentication (MFA) has been triggered.</span></span> <span data-ttu-id="502b1-108">사용자 추가 보안을 필요로 하는 작업을 요청 했으므로 MFA 트리거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-108">MFA may be triggered because the user requested an operation that requires extra security.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="502b1-109">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="502b1-109">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="502b1-110">인증 서비스를 인증 하는 동안 구성할 때 인증 체계 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-110">An authentication scheme is named when the authentication service is configured during authentication.</span></span> <span data-ttu-id="502b1-111">예:</span><span class="sxs-lookup"><span data-stu-id="502b1-111">For example:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Code omitted for brevity

    services.AddAuthentication()
        .AddCookie(options => {
            options.LoginPath = "/Account/Unauthorized/";
            options.AccessDeniedPath = "/Account/Forbidden/";
        })
        .AddJwtBearer(options => {
            options.Audience = "http://localhost:5001/";
            options.Authority = "http://localhost:5000/";
        });
```

<span data-ttu-id="502b1-112">위의 코드에서는 두 가지 인증 처리기 추가 되었습니다: 쿠키와 전달자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-112">In the preceding code, two authentication handlers have been added: one for cookies and one for bearer.</span></span>

>[!NOTE]
><span data-ttu-id="502b1-113">기본 스키마를 지정 하면는 `HttpContext.User` 속성이 해당 id로 설정 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-113">Specifying the default scheme results in the `HttpContext.User` property being set to that identity.</span></span> <span data-ttu-id="502b1-114">해당 동작이 필요 없는 경우 매개 변수가 없는 형식으로 호출 하 여 비활성화 `AddAuthentication`합니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-114">If that behavior isn't desired, disable it by invoking the parameterless form of `AddAuthentication`.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="502b1-115">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="502b1-115">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="502b1-116">인증 체계는 인증 middlewares 인증 하는 동안 구성 된 경우 이름이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-116">Authentication schemes are named when authentication middlewares are configured during authentication.</span></span> <span data-ttu-id="502b1-117">예:</span><span class="sxs-lookup"><span data-stu-id="502b1-117">For example:</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    // Code omitted for brevity

    app.UseCookieAuthentication(new CookieAuthenticationOptions()
    {
        AuthenticationScheme = "Cookie",
        LoginPath = "/Account/Unauthorized/",
        AccessDeniedPath = "/Account/Forbidden/",
        AutomaticAuthenticate = false
    });
    
    app.UseJwtBearerAuthentication(new JwtBearerOptions()
    {
        AuthenticationScheme = "Bearer",
        AutomaticAuthenticate = false,
        Audience = "http://localhost:5001/",
        Authority = "http://localhost:5000/",
        RequireHttpsMetadata = false
    });
```

<span data-ttu-id="502b1-118">위의 코드에서는 두 가지 인증 middlewares 추가 되었습니다: 쿠키와 전달자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-118">In the preceding code, two authentication middlewares have been added: one for cookies and one for bearer.</span></span>

>[!NOTE]
><span data-ttu-id="502b1-119">기본 스키마를 지정 하면는 `HttpContext.User` 속성이 해당 id로 설정 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-119">Specifying the default scheme results in the `HttpContext.User` property being set to that identity.</span></span> <span data-ttu-id="502b1-120">해당 동작이 필요 없는 경우 설정 하 여 비활성화 된 `AuthenticationOptions.AutomaticAuthenticate` 속성을 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-120">If that behavior isn't desired, disable it by setting the `AuthenticationOptions.AutomaticAuthenticate` property to `false`.</span></span>

---

## <a name="selecting-the-scheme-with-the-authorize-attribute"></a><span data-ttu-id="502b1-121">권한 부여 특성을 가진 구성표 선택</span><span class="sxs-lookup"><span data-stu-id="502b1-121">Selecting the scheme with the Authorize attribute</span></span>

<span data-ttu-id="502b1-122">권한 부여, 지점에서 응용 프로그램에 사용할 처리기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-122">At the point of authorization, the app indicates the handler to be used.</span></span> <span data-ttu-id="502b1-123">응용 프로그램에 인증 체계의 쉼표로 구분 된 목록을 전달 하 여 승인 된 처리기를 선택 `[Authorize]`합니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-123">Select the handler with which the app will authorize by passing a comma-delimited list of authentication schemes to `[Authorize]`.</span></span> <span data-ttu-id="502b1-124">`[Authorize]` 특성 인증 체계 또는 기본 구성 되어 있는지 여부에 관계 없이 사용 하는 구성표를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-124">The `[Authorize]` attribute specifies the authentication scheme or schemes to use regardless of whether a default is configured.</span></span> <span data-ttu-id="502b1-125">예:</span><span class="sxs-lookup"><span data-stu-id="502b1-125">For example:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="502b1-126">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="502b1-126">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
[Authorize(AuthenticationSchemes = AuthSchemes)]
public class MixedController : Controller
    // Requires the following imports:
    // using Microsoft.AspNetCore.Authentication.Cookies;
    // using Microsoft.AspNetCore.Authentication.JwtBearer;
    private const string AuthSchemes =
        CookieAuthenticationDefaults.AuthenticationScheme + "," +
        JwtBearerDefaults.AuthenticationScheme;
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="502b1-127">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="502b1-127">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
[Authorize(ActiveAuthenticationSchemes = AuthSchemes)]
public class MixedController : Controller
    // Requires the following imports:
    // using Microsoft.AspNetCore.Authentication.Cookies;
    // using Microsoft.AspNetCore.Authentication.JwtBearer;
    private const string AuthSchemes =
        CookieAuthenticationDefaults.AuthenticationScheme + "," +
        JwtBearerDefaults.AuthenticationScheme;
```

---

<span data-ttu-id="502b1-128">앞의 예에서 쿠키와 전달자 처리기 실행 하 고는 기회를 만들고 현재 사용자에 대 한 id를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-128">In the preceding example, both the cookie and bearer handlers run and have a chance to create and append an identity for the current user.</span></span> <span data-ttu-id="502b1-129">단일 구성표를 지정 하 여 해당 처리기를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-129">By specifying a single scheme only, the corresponding handler runs.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="502b1-130">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="502b1-130">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
[Authorize(AuthenticationSchemes = 
    JwtBearerDefaults.AuthenticationScheme)]
public class MixedController : Controller
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="502b1-131">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="502b1-131">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
[Authorize(ActiveAuthenticationSchemes = 
    JwtBearerDefaults.AuthenticationScheme)]
public class MixedController : Controller
```

---

<span data-ttu-id="502b1-132">위의 코드에서 "Bearer" 체계로 처리기만 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-132">In the preceding code, only the handler with the "Bearer" scheme runs.</span></span> <span data-ttu-id="502b1-133">모든 쿠키 기반 id는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-133">Any cookie-based identities are ignored.</span></span>

## <a name="selecting-the-scheme-with-policies"></a><span data-ttu-id="502b1-134">정책 사용 하 여 구성표 선택</span><span class="sxs-lookup"><span data-stu-id="502b1-134">Selecting the scheme with policies</span></span>

<span data-ttu-id="502b1-135">원하는 체계를 지정 하려는 경우 [정책](xref:security/authorization/policies)를 설정할 수 있습니다는 `AuthenticationSchemes` 정책에 추가할 때 컬렉션:</span><span class="sxs-lookup"><span data-stu-id="502b1-135">If you prefer to specify the desired schemes in [policy](xref:security/authorization/policies), you can set the `AuthenticationSchemes` collection when adding your policy:</span></span>

```csharp
services.AddAuthorization(options =>
{
    options.AddPolicy("Over18", policy =>
    {
        policy.AuthenticationSchemes.Add(JwtBearerDefaults.AuthenticationScheme);
        policy.RequireAuthenticatedUser();
        policy.Requirements.Add(new MinimumAgeRequirement());
    });
});
```

<span data-ttu-id="502b1-136">위의 예제에서는 "Over18" 정책 "Bearer" 처리기에 의해 생성 된 id에 대해만 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="502b1-136">In the preceding example, the "Over18" policy only runs against the identity created by the "Bearer" handler.</span></span> <span data-ttu-id="502b1-137">설정 하 여 정책을 사용 하 여는 `[Authorize]` 특성의 `Policy` 속성:</span><span class="sxs-lookup"><span data-stu-id="502b1-137">Use the policy by setting the `[Authorize]` attribute's `Policy` property:</span></span>

```csharp
[Authorize(Policy = "Over18")]
public class RegistrationController : Controller
```
