---
title: "마이그레이션 인증 및 ASP.NET 코어 2.0 Id"
author: scottaddie
description: "이 문서는 ASP.NET 코어 2.0으로 마이그레이션 ASP.NET Core 1.x 인증 및 Id에 대 한 가장 일반적인 단계를 간략하게 설명 합니다."
manager: wpickett
ms.author: scaddie
ms.date: 10/26/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: migration/1x-to-2x/identity-2x
ms.openlocfilehash: dd48b2b027d22b570aa182e748ca91738e935f49
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="migrating-authentication-and-identity-to-aspnet-core-20"></a><span data-ttu-id="9591f-103">마이그레이션 인증 및 ASP.NET 코어 2.0 Id</span><span class="sxs-lookup"><span data-stu-id="9591f-103">Migrating Authentication and Identity to ASP.NET Core 2.0</span></span>

<span data-ttu-id="9591f-104">여 [Scott Addie](https://github.com/scottaddie) 및 [Hao 둘러싼](https://github.com/HaoK)</span><span class="sxs-lookup"><span data-stu-id="9591f-104">By [Scott Addie](https://github.com/scottaddie) and [Hao Kung](https://github.com/HaoK)</span></span>

<span data-ttu-id="9591f-105">ASP.NET Core 2.0 인증을 위한 새 모델을 포함 하 고 [Identity](xref:security/authentication/identity) 서비스를 사용 하 여 구성을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-105">ASP.NET Core 2.0 has a new model for authentication and [Identity](xref:security/authentication/identity) which simplifies configuration by using services.</span></span> <span data-ttu-id="9591f-106">아래 설명 된 대로 새 모델을 사용 하도록 인증 또는 Id를 사용 하는 ASP.NET Core 1.x 응용 프로그램을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-106">ASP.NET Core 1.x applications that use authentication or Identity can be updated to use the new model as outlined below.</span></span>

<a name="auth-middleware"></a>

## <a name="authentication-middleware-and-services"></a><span data-ttu-id="9591f-107">인증 미들웨어 및 서비스</span><span class="sxs-lookup"><span data-stu-id="9591f-107">Authentication Middleware and services</span></span>
<span data-ttu-id="9591f-108">1.x 프로젝트에서 인증 미들웨어를 통해 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-108">In 1.x projects, authentication is configured via middleware.</span></span> <span data-ttu-id="9591f-109">미들웨어 메서드를 지원 하려면 각 인증 체계에 대해 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-109">A middleware method is invoked for each authentication scheme you want to support.</span></span>

<span data-ttu-id="9591f-110">에 Id를 가진 Facebook 인증을 구성 하는 다음 1.x 예제 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9591f-110">The following 1.x example configures Facebook authentication with Identity in *Startup.cs*:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddIdentity<ApplicationUser, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext>();
}

public void Configure(IApplicationBuilder app, ILoggerFactory loggerfactory)
{
    app.UseIdentity();
    app.UseFacebookAuthentication(new FacebookOptions { 
        AppId = Configuration["auth:facebook:appid"],
        AppSecret = Configuration["auth:facebook:appsecret"]
    });
} 
```

<span data-ttu-id="9591f-111">2.0 프로젝트에서 서비스를 통해 인증이 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-111">In 2.0 projects, authentication is configured via services.</span></span> <span data-ttu-id="9591f-112">에 등록 된 각 인증 체계는 `ConfigureServices` 방식의 *Startup.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-112">Each authentication scheme is registered in the `ConfigureServices` method of *Startup.cs*.</span></span> <span data-ttu-id="9591f-113">`UseIdentity` 메서드 아래 템플릿으로 바뀝니다 `UseAuthentication`합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-113">The `UseIdentity` method is replaced with `UseAuthentication`.</span></span>

<span data-ttu-id="9591f-114">에 Id를 가진 Facebook 인증을 구성 하는 다음 2.0 예제 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9591f-114">The following 2.0 example configures Facebook authentication with Identity in *Startup.cs*:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddIdentity<ApplicationUser, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext>();

    // If you want to tweak Identity cookies, they're no longer part of IdentityOptions.
    services.ConfigureApplicationCookie(options => options.LoginPath = "/Account/LogIn");
    services.AddAuthentication()
            .AddFacebook(options => 
            {
                options.AppId = Configuration["auth:facebook:appid"];
                options.AppSecret = Configuration["auth:facebook:appsecret"];
            });
}

public void Configure(IApplicationBuilder app, ILoggerFactory loggerfactory) {
    app.UseAuthentication();
}
```

<span data-ttu-id="9591f-115">`UseAuthentication` 메서드 자동 인증 및 원격 인증 요청 처리를 담당 하는 단일 인증 미들웨어 구성 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-115">The `UseAuthentication` method adds a single authentication middleware component which is responsible for automatic authentication and the handling of remote authentication requests.</span></span> <span data-ttu-id="9591f-116">단일의 공통 미들웨어 구성 요소와 개별 미들웨어 구성 요소를 모두 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-116">It replaces all of the individual middleware components with a single, common middleware component.</span></span>

<span data-ttu-id="9591f-117">다음은 각 주요 인증 체계에 대 한 마이그레이션 지침 2.0입니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-117">Below are 2.0 migration instructions for each major authentication scheme.</span></span>

### <a name="cookie-based-authentication"></a><span data-ttu-id="9591f-118">쿠키 기반 인증</span><span class="sxs-lookup"><span data-stu-id="9591f-118">Cookie-based authentication</span></span>
<span data-ttu-id="9591f-119">아래 두 옵션 중 하나를 선택 하 고에 필요한 사항을 변경한 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9591f-119">Select one of the two options below, and make the necessary changes in *Startup.cs*:</span></span>

1. <span data-ttu-id="9591f-120">Id 가진 쿠키 사용</span><span class="sxs-lookup"><span data-stu-id="9591f-120">Use cookies with Identity</span></span>
    - <span data-ttu-id="9591f-121">대체 `UseIdentity` 와 `UseAuthentication` 에 `Configure` 메서드:</span><span class="sxs-lookup"><span data-stu-id="9591f-121">Replace `UseIdentity` with `UseAuthentication` in the `Configure` method:</span></span>

        ```csharp
        app.UseAuthentication();
        ```

    - <span data-ttu-id="9591f-122">호출는 `AddIdentity` 에서 메서드는 `ConfigureServices` 메서드 쿠키 인증 서비스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-122">Invoke the `AddIdentity` method in the `ConfigureServices` method to add the cookie authentication services.</span></span>
    - <span data-ttu-id="9591f-123">필요에 따라 호출는 `ConfigureApplicationCookie` 또는 `ConfigureExternalCookie` 에서 메서드는 `ConfigureServices` 메서드 Id 쿠키 설정을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-123">Optionally, invoke the `ConfigureApplicationCookie` or `ConfigureExternalCookie` method in the `ConfigureServices` method to tweak the Identity cookie settings.</span></span>

        ```csharp
        services.AddIdentity<ApplicationUser, IdentityRole>()
                .AddEntityFrameworkStores<ApplicationDbContext>()
                .AddDefaultTokenProviders();
    
        services.ConfigureApplicationCookie(options => options.LoginPath = "/Account/LogIn");
        ```

2. <span data-ttu-id="9591f-124">Identity 없이 쿠키를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9591f-124">Use cookies without Identity</span></span>
    - <span data-ttu-id="9591f-125">대체는 `UseCookieAuthentication` 메서드 호출의 `Configure` 메서드 `UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="9591f-125">Replace the `UseCookieAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
  
        ```csharp
        app.UseAuthentication();
        ```
 
    - <span data-ttu-id="9591f-126">호출 된 `AddAuthentication` 및 `AddCookie` 의 메서드는 `ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="9591f-126">Invoke the `AddAuthentication` and `AddCookie` methods in the `ConfigureServices` method:</span></span>

        ```csharp
        // If you don't want the cookie to be automatically authenticated and assigned to HttpContext.User, 
        // remove the CookieAuthenticationDefaults.AuthenticationScheme parameter passed to AddAuthentication.
        services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
                .AddCookie(options => 
                {
                    options.LoginPath = "/Account/LogIn";
                    options.LogoutPath = "/Account/LogOff";
                });
        ```

### <a name="jwt-bearer-authentication"></a><span data-ttu-id="9591f-127">JWT 전달자 인증</span><span class="sxs-lookup"><span data-stu-id="9591f-127">JWT Bearer Authentication</span></span>
<span data-ttu-id="9591f-128">다음과 같이 변경 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9591f-128">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="9591f-129">대체는 `UseJwtBearerAuthentication` 메서드 호출의 `Configure` 메서드 `UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="9591f-129">Replace the `UseJwtBearerAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
 
    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="9591f-130">호출 된 `AddJwtBearer` 에서 메서드는 `ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="9591f-130">Invoke the `AddJwtBearer` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
            .AddJwtBearer(options => 
            {
                options.Audience = "http://localhost:5001/";
                options.Authority = "http://localhost:5000/";
            });
    ```

    <span data-ttu-id="9591f-131">전달 하 여 기본 체계를 설정 해야 하므로이 코드 조각은 Id를 사용 하지 않는 `JwtBearerDefaults.AuthenticationScheme` 에 `AddAuthentication` 메서드.</span><span class="sxs-lookup"><span data-stu-id="9591f-131">This code snippet doesn't use Identity, so the default scheme should be set by passing `JwtBearerDefaults.AuthenticationScheme` to the `AddAuthentication` method.</span></span>

### <a name="openid-connect-oidc-authentication"></a><span data-ttu-id="9591f-132">OpenID 연결 (OIDC) 인증</span><span class="sxs-lookup"><span data-stu-id="9591f-132">OpenID Connect (OIDC) authentication</span></span>
<span data-ttu-id="9591f-133">다음과 같이 변경 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9591f-133">Make the following changes in *Startup.cs*:</span></span>

- <span data-ttu-id="9591f-134">대체는 `UseOpenIdConnectAuthentication` 메서드 호출의 `Configure` 메서드 `UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="9591f-134">Replace the `UseOpenIdConnectAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>

    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="9591f-135">호출 된 `AddOpenIdConnect` 에서 메서드는 `ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="9591f-135">Invoke the `AddOpenIdConnect` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication(options => 
    {
        options.DefaultScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        options.DefaultChallengeScheme = OpenIdConnectDefaults.AuthenticationScheme;
    })
    .AddCookie()
    .AddOpenIdConnect(options => 
    {
        options.Authority = Configuration["auth:oidc:authority"];
        options.ClientId = Configuration["auth:oidc:clientid"];
    });
    ```

### <a name="facebook-authentication"></a><span data-ttu-id="9591f-136">facebook 인증</span><span class="sxs-lookup"><span data-stu-id="9591f-136">Facebook authentication</span></span>
<span data-ttu-id="9591f-137">다음과 같이 변경 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9591f-137">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="9591f-138">대체는 `UseFacebookAuthentication` 메서드 호출의 `Configure` 메서드 `UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="9591f-138">Replace the `UseFacebookAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
 
    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="9591f-139">호출 된 `AddFacebook` 에서 메서드는 `ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="9591f-139">Invoke the `AddFacebook` method in the `ConfigureServices` method:</span></span>
    
    ```csharp
    services.AddAuthentication()
            .AddFacebook(options => 
            {
                options.AppId = Configuration["auth:facebook:appid"];
                options.AppSecret = Configuration["auth:facebook:appsecret"];
            });
    ```

### <a name="google-authentication"></a><span data-ttu-id="9591f-140">Google 인증</span><span class="sxs-lookup"><span data-stu-id="9591f-140">Google authentication</span></span>
<span data-ttu-id="9591f-141">다음과 같이 변경 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9591f-141">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="9591f-142">대체는 `UseGoogleAuthentication` 메서드 호출의 `Configure` 메서드 `UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="9591f-142">Replace the `UseGoogleAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
 
    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="9591f-143">호출 된 `AddGoogle` 에서 메서드는 `ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="9591f-143">Invoke the `AddGoogle` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication()
            .AddGoogle(options => 
            {
                options.ClientId = Configuration["auth:google:clientid"];
                options.ClientSecret = Configuration["auth:google:clientsecret"];
            });    
    ```

### <a name="microsoft-account-authentication"></a><span data-ttu-id="9591f-144">Microsoft 계정 인증</span><span class="sxs-lookup"><span data-stu-id="9591f-144">Microsoft Account authentication</span></span>
<span data-ttu-id="9591f-145">다음과 같이 변경 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9591f-145">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="9591f-146">대체는 `UseMicrosoftAccountAuthentication` 메서드 호출의 `Configure` 메서드 `UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="9591f-146">Replace the `UseMicrosoftAccountAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>

    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="9591f-147">호출 된 `AddMicrosoftAccount` 에서 메서드는 `ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="9591f-147">Invoke the `AddMicrosoftAccount` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication()
            .AddMicrosoftAccount(options => 
            {
                options.ClientId = Configuration["auth:microsoft:clientid"];
                options.ClientSecret = Configuration["auth:microsoft:clientsecret"];
            });
    ``` 

### <a name="twitter-authentication"></a><span data-ttu-id="9591f-148">Twitter 인증</span><span class="sxs-lookup"><span data-stu-id="9591f-148">Twitter authentication</span></span>
<span data-ttu-id="9591f-149">다음과 같이 변경 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9591f-149">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="9591f-150">대체는 `UseTwitterAuthentication` 메서드 호출의 `Configure` 메서드 `UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="9591f-150">Replace the `UseTwitterAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
 
    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="9591f-151">호출 된 `AddTwitter` 에서 메서드는 `ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="9591f-151">Invoke the `AddTwitter` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication()
            .AddTwitter(options => 
            {
                options.ConsumerKey = Configuration["auth:twitter:consumerkey"];
                options.ConsumerSecret = Configuration["auth:twitter:consumersecret"];
            });
    ```

### <a name="setting-default-authentication-schemes"></a><span data-ttu-id="9591f-152">기본 인증 체계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-152">Setting default authentication schemes</span></span>
<span data-ttu-id="9591f-153">1.x에는 `AutomaticAuthenticate` 및 `AutomaticChallenge` 의 속성은 [AuthenticationOptions](https://docs.microsoft.com/dotnet/api/Microsoft.AspNetCore.Builder.AuthenticationOptions?view=aspnetcore-1.1) 하나의 인증 구성표에 설정 될 기본 클래스를 서로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-153">In 1.x, the `AutomaticAuthenticate` and `AutomaticChallenge` properties of the [AuthenticationOptions](https://docs.microsoft.com/dotnet/api/Microsoft.AspNetCore.Builder.AuthenticationOptions?view=aspnetcore-1.1) base class were intended to be set on a single authentication scheme.</span></span> <span data-ttu-id="9591f-154">이 적용할 수 있는 좋은 방법이 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-154">There was no good way to enforce this.</span></span>

<span data-ttu-id="9591f-155">2.0에서는 이러한 두 속성 제거한 개인에 대 한 속성으로 `AuthenticationOptions` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="9591f-155">In 2.0, these two properties have been removed as properties on the individual `AuthenticationOptions` instance.</span></span> <span data-ttu-id="9591f-156">구성할 수 있습니다는 `AddAuthentication` 내에서 메서드 호출에서 `ConfigureServices` 방식의 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9591f-156">They can be configured in the `AddAuthentication` method call within the `ConfigureServices` method of *Startup.cs*:</span></span>

```csharp
services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme);
```

<span data-ttu-id="9591f-157">위의 코드 조각에서는 기본 스키마로 설정 되어 `CookieAuthenticationDefaults.AuthenticationScheme` ("쿠키").</span><span class="sxs-lookup"><span data-stu-id="9591f-157">In the preceding code snippet, the default scheme is set to `CookieAuthenticationDefaults.AuthenticationScheme` ("Cookies").</span></span>

<span data-ttu-id="9591f-158">또는 오버 로드 된 버전의를 사용 하 여는 `AddAuthentication` 둘 이상의 속성을 설정 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="9591f-158">Alternatively, use an overloaded version of the `AddAuthentication` method to set more than one property.</span></span> <span data-ttu-id="9591f-159">다음 오버 로드 된 메서드 예제에서는 기본 스키마로 설정 되어 `CookieAuthenticationDefaults.AuthenticationScheme`합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-159">In the following overloaded method example, the default scheme is set to `CookieAuthenticationDefaults.AuthenticationScheme`.</span></span> <span data-ttu-id="9591f-160">인증 체계 또는 개별 내에서 지정할 수 있습니다 `[Authorize]` 특성 또는 권한 부여 정책.</span><span class="sxs-lookup"><span data-stu-id="9591f-160">The authentication scheme may alternatively be specified within your individual `[Authorize]` attributes or authorization policies.</span></span>

```csharp
services.AddAuthentication(options => 
{
    options.DefaultScheme = CookieAuthenticationDefaults.AuthenticationScheme;
    options.DefaultChallengeScheme = OpenIdConnectDefaults.AuthenticationScheme;
});
```

<span data-ttu-id="9591f-161">다음 조건 중 하나 이면 2.0에서 기본 체계를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-161">Define a default scheme in 2.0 if one of the following conditions is true:</span></span>
- <span data-ttu-id="9591f-162">사용자 자동으로 로그인 하려면</span><span class="sxs-lookup"><span data-stu-id="9591f-162">You want the user to be automatically signed in</span></span>
- <span data-ttu-id="9591f-163">사용 된 `[Authorize]` 구성표를 지정 하지 않고 특성 또는 권한 부여 정책</span><span class="sxs-lookup"><span data-stu-id="9591f-163">You use the `[Authorize]` attribute or authorization policies without specifying schemes</span></span>

<span data-ttu-id="9591f-164">이 규칙의 예외는 `AddIdentity` 메서드.</span><span class="sxs-lookup"><span data-stu-id="9591f-164">An exception to this rule is the `AddIdentity` method.</span></span> <span data-ttu-id="9591f-165">이 메서드는 쿠키 및 인증 하 고 인증 구성표는 응용 프로그램 쿠키를 기본 설정에 대 한 추가 `IdentityConstants.ApplicationScheme`합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-165">This method adds cookies for you and sets the default authenticate and challenge schemes to the application cookie `IdentityConstants.ApplicationScheme`.</span></span> <span data-ttu-id="9591f-166">또한 기본 로그인 구성표 외부 쿠키를 설정 `IdentityConstants.ExternalScheme`합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-166">Additionally, it sets the default sign-in scheme to the external cookie `IdentityConstants.ExternalScheme`.</span></span>

<a name="obsolete-interface"></a>

## <a name="use-httpcontext-authentication-extensions"></a><span data-ttu-id="9591f-167">HttpContext 인증 확장 프로그램을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9591f-167">Use HttpContext authentication extensions</span></span>
<span data-ttu-id="9591f-168">`IAuthenticationManager` 인터페이스는 1.x 인증 시스템의 주 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-168">The `IAuthenticationManager` interface is the main entry point into the 1.x authentication system.</span></span> <span data-ttu-id="9591f-169">새로운 집합으로 대체 되었습니다 `HttpContext` 의 확장 메서드는 `Microsoft.AspNetCore.Authentication` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-169">It has been replaced with a new set of `HttpContext` extension methods in the `Microsoft.AspNetCore.Authentication` namespace.</span></span>

<span data-ttu-id="9591f-170">예를 들어 1.x 프로젝트 참조는 `Authentication` 속성:</span><span class="sxs-lookup"><span data-stu-id="9591f-170">For example, 1.x projects reference an `Authentication` property:</span></span>

[!code-csharp[Main](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Controllers/AccountController.cs?name=snippet_AuthenticationProperty)]

<span data-ttu-id="9591f-171">2.0 프로젝트에서 가져올는 `Microsoft.AspNetCore.Authentication` 네임 스페이스를 삭제 하 고는 `Authentication` 속성 참조:</span><span class="sxs-lookup"><span data-stu-id="9591f-171">In 2.0 projects, import the `Microsoft.AspNetCore.Authentication` namespace, and delete the `Authentication` property references:</span></span>

[!code-csharp[Main](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Controllers/AccountController.cs?name=snippet_AuthenticationProperty)]

<a name="windows-auth-changes"></a>

## <a name="windows-authentication-httpsys--iisintegration"></a><span data-ttu-id="9591f-172">Windows 인증 (HTTP.sys / IISIntegration)</span><span class="sxs-lookup"><span data-stu-id="9591f-172">Windows Authentication (HTTP.sys / IISIntegration)</span></span>
<span data-ttu-id="9591f-173">Windows 인증의 두 가지 변형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-173">There are two variations of Windows authentication:</span></span>
1. <span data-ttu-id="9591f-174">호스트에는 인증 된 사용자만 허용</span><span class="sxs-lookup"><span data-stu-id="9591f-174">The host only allows authenticated users</span></span>
2. <span data-ttu-id="9591f-175">호스트는 수 있도록 모두 익명 및 인증 된 사용자</span><span class="sxs-lookup"><span data-stu-id="9591f-175">The host allows both anonymous and authenticated users</span></span>

<span data-ttu-id="9591f-176">위에서 설명한 첫 번째 변형 2.0 변경의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-176">The first variation described above is unaffected by the 2.0 changes.</span></span>

<span data-ttu-id="9591f-177">위에서 설명한 두 번째 변형은 2.0 변경의 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-177">The second variation described above is affected by the 2.0 changes.</span></span> <span data-ttu-id="9591f-178">예를 들어, 있습니다 수 허용 해서는 익명 사용자가 IIS에 응용 프로그램에 또는 [HTTP.sys](xref:fundamentals/servers/weblistener) 컨트롤러 수준에서 권한을 부여 하지만 사용자가 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-178">As an example, you may be allowing anonymous users into your application at the IIS or [HTTP.sys](xref:fundamentals/servers/weblistener) layer but authorizing users at the Controller level.</span></span> <span data-ttu-id="9591f-179">이 시나리오에서는 기본 스키마로 설정 `IISDefaults.AuthenticationScheme` 에 `ConfigureServices` 방식의 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9591f-179">In this scenario, set the default scheme to `IISDefaults.AuthenticationScheme` in the `ConfigureServices` method of *Startup.cs*:</span></span>

```csharp
services.AddAuthentication(IISDefaults.AuthenticationScheme);
```

<span data-ttu-id="9591f-180">기본 체계를 설정 하려면 그에 따라 제대로 수행 되지 않습니다 authorize 요청의 작동에서 보도록 하기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-180">Failure to set the default scheme accordingly prevents the authorize request to challenge from working.</span></span>

<a name="identity-cookie-options"></a>

## <a name="identitycookieoptions-instances"></a><span data-ttu-id="9591f-181">IdentityCookieOptions instances</span><span class="sxs-lookup"><span data-stu-id="9591f-181">IdentityCookieOptions instances</span></span>
<span data-ttu-id="9591f-182">2.0 변경의 부작용은 옵션 쿠키 옵션 인스턴스 대신 명명 된 사용으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-182">A side effect of the 2.0 changes is the switch to using named options instead of cookie options instances.</span></span> <span data-ttu-id="9591f-183">Identity 쿠키 구성표 이름을 사용자 지정 하는 기능이 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-183">The ability to customize the Identity cookie scheme names is removed.</span></span>

<span data-ttu-id="9591f-184">예를 들어 1.x 프로젝트 사용 [생성자 삽입](xref:mvc/controllers/dependency-injection#constructor-injection) 전달 하는 `IdentityCookieOptions` 매개 변수를 *AccountController.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-184">For example, 1.x projects use [constructor injection](xref:mvc/controllers/dependency-injection#constructor-injection) to pass an `IdentityCookieOptions` parameter into *AccountController.cs*.</span></span> <span data-ttu-id="9591f-185">외부 쿠키 인증 체계는에서 제공된 된 인스턴스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-185">The external cookie authentication scheme is accessed from the provided instance:</span></span>

[!code-csharp[Main](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Controllers/AccountController.cs?name=snippet_AccountControllerConstructor&highlight=4,11)]

<span data-ttu-id="9591f-186">앞에서 언급 한 생성자 삽입 2.0 프로젝트에서 불필요 하 게 만드는 및 `_externalCookieScheme` 필드를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-186">The aforementioned constructor injection becomes unnecessary in 2.0 projects, and the `_externalCookieScheme` field can be deleted:</span></span>

[!code-csharp[Main](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Controllers/AccountController.cs?name=snippet_AccountControllerConstructor)]

<span data-ttu-id="9591f-187">`IdentityConstants.ExternalScheme` 상수를 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-187">The `IdentityConstants.ExternalScheme` constant can be used directly:</span></span>

[!code-csharp[Main](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Controllers/AccountController.cs?name=snippet_AuthenticationProperty)]

<a name="navigation-properties"></a>

## <a name="add-identityuser-poco-navigation-properties"></a><span data-ttu-id="9591f-188">POCO IdentityUser 탐색 속성 추가</span><span class="sxs-lookup"><span data-stu-id="9591f-188">Add IdentityUser POCO navigation properties</span></span>
<span data-ttu-id="9591f-189">자료의 Entity Framework (EF) 핵심 탐색 속성 `IdentityUser` POCO (Plain Old CLR Object) 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-189">The Entity Framework (EF) Core navigation properties of the base `IdentityUser` POCO (Plain Old CLR Object) have been removed.</span></span> <span data-ttu-id="9591f-190">이러한 속성을 사용 하는 1.x 프로젝트에 수동으로 추가 다시 2.0 프로젝트에:</span><span class="sxs-lookup"><span data-stu-id="9591f-190">If your 1.x project used these properties, manually add them back to the 2.0 project:</span></span>

```csharp
/// <summary>
/// Navigation property for the roles this user belongs to.
/// </summary>
public virtual ICollection<IdentityUserRole<int>> Roles { get; } = new List<IdentityUserRole<int>>();

/// <summary>
/// Navigation property for the claims this user possesses.
/// </summary>
public virtual ICollection<IdentityUserClaim<int>> Claims { get; } = new List<IdentityUserClaim<int>>();

/// <summary>
/// Navigation property for this users login accounts.
/// </summary>
public virtual ICollection<IdentityUserLogin<int>> Logins { get; } = new List<IdentityUserLogin<int>>();
```

<span data-ttu-id="9591f-191">중복 된 외래 키 EF 코어 마이그레이션을 실행 하는 경우를 방지 하려면 다음을 추가 하면 `IdentityDbContext` 클래스의 `OnModelCreating` 메서드 (후의 `base.OnModelCreating();` 호출):</span><span class="sxs-lookup"><span data-stu-id="9591f-191">To prevent duplicate foreign keys when running EF Core Migrations, add the following to your `IdentityDbContext` class' `OnModelCreating` method (after the `base.OnModelCreating();` call):</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder builder)
{
    base.OnModelCreating(builder);
    // Customize the ASP.NET Identity model and override the defaults if needed.
    // For example, you can rename the ASP.NET Identity table names and more.
    // Add your customizations after calling base.OnModelCreating(builder);

    builder.Entity<ApplicationUser>()
        .HasMany(e => e.Claims)
        .WithOne()
        .HasForeignKey(e => e.UserId)
        .IsRequired()
        .OnDelete(DeleteBehavior.Cascade);

    builder.Entity<ApplicationUser>()
        .HasMany(e => e.Logins)
        .WithOne()
        .HasForeignKey(e => e.UserId)
        .IsRequired()
        .OnDelete(DeleteBehavior.Cascade);

    builder.Entity<ApplicationUser>()
        .HasMany(e => e.Roles)
        .WithOne()
        .HasForeignKey(e => e.UserId)
        .IsRequired()
        .OnDelete(DeleteBehavior.Cascade);
}
```

<a name="synchronous-method-removal"></a>

## <a name="replace-getexternalauthenticationschemes"></a><span data-ttu-id="9591f-192">GetExternalAuthenticationSchemes 바꾸기</span><span class="sxs-lookup"><span data-stu-id="9591f-192">Replace GetExternalAuthenticationSchemes</span></span>
<span data-ttu-id="9591f-193">동기 메서드로 `GetExternalAuthenticationSchemes` 비동기 버전 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-193">The synchronous method `GetExternalAuthenticationSchemes` was removed in favor of an asynchronous version.</span></span> <span data-ttu-id="9591f-194">1.x 프로젝트 다음 코드를 있는 *ManageController.cs*:</span><span class="sxs-lookup"><span data-stu-id="9591f-194">1.x projects have the following code in *ManageController.cs*:</span></span>

[!code-csharp[Main](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Controllers/ManageController.cs?name=snippet_GetExternalAuthenticationSchemes)]

<span data-ttu-id="9591f-195">이 메서드의 나타납니다 *Login.cshtml* 너무:</span><span class="sxs-lookup"><span data-stu-id="9591f-195">This method appears in *Login.cshtml* too:</span></span>

[!code-cshtml[Main](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Views/Account/Login.cshtml?range=62,75-84)]

<span data-ttu-id="9591f-196">2.0 프로젝트에서 사용 하 여는 `GetExternalAuthenticationSchemesAsync` 메서드:</span><span class="sxs-lookup"><span data-stu-id="9591f-196">In 2.0 projects, use the `GetExternalAuthenticationSchemesAsync` method:</span></span>

[!code-csharp[Main](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Controllers/ManageController.cs?name=snippet_GetExternalAuthenticationSchemesAsync)]

<span data-ttu-id="9591f-197">*Login.cshtml*, `AuthenticationScheme` 액세스 속성은 `foreach` 루프 변경 `Name`:</span><span class="sxs-lookup"><span data-stu-id="9591f-197">In *Login.cshtml*, the `AuthenticationScheme` property accessed in the `foreach` loop changes to `Name`:</span></span>

[!code-cshtml[Main](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Views/Account/Login.cshtml?range=62,75-84)]

<a name="property-change"></a>

## <a name="manageloginsviewmodel-property-change"></a><span data-ttu-id="9591f-198">ManageLoginsViewModel 속성 변경</span><span class="sxs-lookup"><span data-stu-id="9591f-198">ManageLoginsViewModel property change</span></span>
<span data-ttu-id="9591f-199">A `ManageLoginsViewModel` 개체가 사용 되는 `ManageLogins` 의 동작 *ManageController.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-199">A `ManageLoginsViewModel` object is used in the `ManageLogins` action of *ManageController.cs*.</span></span> <span data-ttu-id="9591f-200">1.x 프로젝트에서 개체의 `OtherLogins` 속성 반환 형식이 `IList<AuthenticationDescription>`합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-200">In 1.x projects, the object's `OtherLogins` property return type is `IList<AuthenticationDescription>`.</span></span> <span data-ttu-id="9591f-201">이 반환 형식은 가져오기를 `Microsoft.AspNetCore.Http.Authentication`:</span><span class="sxs-lookup"><span data-stu-id="9591f-201">This return type requires an import of `Microsoft.AspNetCore.Http.Authentication`:</span></span>

[!code-csharp[Main](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Models/ManageViewModels/ManageLoginsViewModel.cs?name=snippet_ManageLoginsViewModel&highlight=2,11)]

<span data-ttu-id="9591f-202">2.0 프로젝트에서 반환 형식으로 변경 `IList<AuthenticationScheme>`합니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-202">In 2.0 projects, the return type changes to `IList<AuthenticationScheme>`.</span></span> <span data-ttu-id="9591f-203">이 새로운 반환 형식을 바꿀 필요는 `Microsoft.AspNetCore.Http.Authentication` 를 가져오려면는 `Microsoft.AspNetCore.Authentication` 가져오기.</span><span class="sxs-lookup"><span data-stu-id="9591f-203">This new return type requires replacing the `Microsoft.AspNetCore.Http.Authentication` import with a `Microsoft.AspNetCore.Authentication` import.</span></span>

[!code-csharp[Main](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Models/ManageViewModels/ManageLoginsViewModel.cs?name=snippet_ManageLoginsViewModel&highlight=2,11)]

<a name="additional-resources"></a>

## <a name="additional-resources"></a><span data-ttu-id="9591f-204">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9591f-204">Additional resources</span></span>
<span data-ttu-id="9591f-205">추가 세부 정보 및 토론에 대 한 참조는 [Auth 2.0에 대 한 토론](https://github.com/aspnet/Security/issues/1338) GitHub에서 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="9591f-205">For additional details and discussion, see the [Discussion for Auth 2.0](https://github.com/aspnet/Security/issues/1338) issue on GitHub.</span></span>
