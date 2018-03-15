---
title: "ASP.NET 및 ASP.NET Core와 앱 간에 쿠키를 공유합니다."
author: rick-anderson
description: "ASP.NET 간에 인증 쿠키를 공유 하는 방법에 알아봅니다 4.x 및 ASP.NET Core 응용 프로그램입니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/19/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/cookie-sharing
ms.openlocfilehash: c2d022d8dc625d479bc690f410d4994a1d7e3d74
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="sharing-cookies-among-apps-with-aspnet-and-aspnet-core"></a><span data-ttu-id="3b3f8-103">ASP.NET 및 ASP.NET Core와 앱 간에 쿠키를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-103">Sharing cookies among apps with ASP.NET and ASP.NET Core</span></span>

<span data-ttu-id="3b3f8-104">여 [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="3b3f8-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="3b3f8-105">웹 사이트는 자주 함께 작동 하는 개별 웹 응용 프로그램의 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-105">Websites often consist of individual web apps working together.</span></span> <span data-ttu-id="3b3f8-106">환경을 제공 하기 위해 single sign on (SSO), 사이트 내에서 웹 앱 인증 쿠키를 공유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-106">To provide a single sign-on (SSO) experience, web apps within a site must share authentication cookies.</span></span> <span data-ttu-id="3b3f8-107">이런 시나리오에 대응하기 위해서, 데이터 보호 스택은 Katana 쿠키 인증 및 ASP.NET Core 쿠키 인증 티켓의 공유를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-107">To support this scenario, the data protection stack allows sharing Katana cookie authentication and ASP.NET Core cookie authentication tickets.</span></span>

<span data-ttu-id="3b3f8-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="3b3f8-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="3b3f8-109">이 샘플에서는 쿠키 인증을 사용 하는 세 개의 앱 간에 공유 되는 쿠키를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-109">The sample illustrates cookie sharing across three apps that use cookie authentication:</span></span>

* <span data-ttu-id="3b3f8-110">사용 하지 않고 ASP.NET 코어 2.0 Razor 페이지 앱 [ASP.NET 코어 Id](xref:security/authentication/identity)</span><span class="sxs-lookup"><span data-stu-id="3b3f8-110">ASP.NET Core 2.0 Razor Pages app without using [ASP.NET Core Identity](xref:security/authentication/identity)</span></span>
* <span data-ttu-id="3b3f8-111">ASP.NET Core Id 가진 ASP.NET Core 2.0 MVC 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="3b3f8-111">ASP.NET Core 2.0 MVC app with ASP.NET Core Identity</span></span>
* <span data-ttu-id="3b3f8-112">ASP.NET Id를 가진 ASP.NET Framework 4.6.1 MVC 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="3b3f8-112">ASP.NET Framework 4.6.1 MVC app with ASP.NET Identity</span></span>

<span data-ttu-id="3b3f8-113">다음에 나오는 예제:</span><span class="sxs-lookup"><span data-stu-id="3b3f8-113">In the examples that follow:</span></span>

* <span data-ttu-id="3b3f8-114">인증 쿠키 이름을 설정 하는 일반적인 값으로 `.AspNet.SharedCookie`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-114">The authentication cookie name is set to a common value of `.AspNet.SharedCookie`.</span></span>
* <span data-ttu-id="3b3f8-115">`AuthenticationType` 로 설정 된 `Identity.Application` 명시적으로 나 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-115">The `AuthenticationType` is set to `Identity.Application` either explicitly or by default.</span></span>
* <span data-ttu-id="3b3f8-116">[CookieAuthenticationDefaults.AuthenticationScheme](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationdefaults.authenticationscheme) 인증 스키마로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-116">[CookieAuthenticationDefaults.AuthenticationScheme](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationdefaults.authenticationscheme) is used as the authentication scheme.</span></span> <span data-ttu-id="3b3f8-117">상수 값으로 확인 `Cookies`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-117">The constant resolves to a value of `Cookies`.</span></span>
* <span data-ttu-id="3b3f8-118">쿠키 인증 미들웨어의 구현을 사용 하 여 [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-118">The cookie authentication middleware uses an implementation of [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider).</span></span> <span data-ttu-id="3b3f8-119">`DataProtectionProvider` 암호화 및 인증 쿠키 페이로드 데이터의 암호 해독에 대 한 데이터 보호 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-119">`DataProtectionProvider` provides data protection services for the encryption and decryption of authentication cookie payload data.</span></span> <span data-ttu-id="3b3f8-120">`DataProtectionProvider` 인스턴스 응용 프로그램의 다른 부분에서 사용 되는 데이터 보호 시스템에서 격리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-120">The `DataProtectionProvider` instance is isolated from the data protection system used by other parts of the app.</span></span>
  * <span data-ttu-id="3b3f8-121">공통 [데이터 보호 키](xref:security/data-protection/implementation/key-management) 저장소 위치가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-121">A common [data protection key](xref:security/data-protection/implementation/key-management) storage location is used.</span></span> <span data-ttu-id="3b3f8-122">샘플 응용 프로그램 폴더를 사용 하 여 *KeyRing* 데이터 보호 키를 저장할 솔루션의 루트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-122">The sample app uses a folder named *KeyRing* at the root of the solution to hold the data protection keys.</span></span>
  * <span data-ttu-id="3b3f8-123">[DataProtectionProvider.Create(System.IO.DirectoryInfo)](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider.create?view=aspnetcore-2.0#Microsoft_AspNetCore_DataProtection_DataProtectionProvider_Create_System_IO_DirectoryInfo_) 허용는 [DirectoryInfo](/dotnet/api/system.io.directoryinfo) 인증 쿠키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-123">[DataProtectionProvider.Create(System.IO.DirectoryInfo)](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider.create?view=aspnetcore-2.0#Microsoft_AspNetCore_DataProtection_DataProtectionProvider_Create_System_IO_DirectoryInfo_) accepts a [DirectoryInfo](/dotnet/api/system.io.directoryinfo) for use with authentication cookies.</span></span> <span data-ttu-id="3b3f8-124">경로 제공 하는 샘플 응용 프로그램은 *KeyRing* 폴더 `DirectoryInfo`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-124">The sample app provides the path of the *KeyRing* folder to `DirectoryInfo`.</span></span>
  * <span data-ttu-id="3b3f8-125">[DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider) 를 사용하려면 [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) NuGet 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-125">[DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionprovider) requires the [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) NuGet package.</span></span> <span data-ttu-id="3b3f8-126">ASP.NET Core 2.0 및 최신 앱에 대 한이 패키지를 가져오려면 참조는 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-126">To obtain this package for ASP.NET Core 2.0 and later apps, reference the [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage.</span></span> <span data-ttu-id="3b3f8-127">.NET Framework를 대상으로 하는 경우에 대 한 패키지 참조 추가 `Microsoft.AspNetCore.DataProtection.Extensions`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-127">When targeting .NET Framework, add a package reference to `Microsoft.AspNetCore.DataProtection.Extensions`.</span></span>

## <a name="share-authentication-cookies-among-aspnet-core-apps"></a><span data-ttu-id="3b3f8-128">ASP.NET Core 응용 프로그램 간에 인증 쿠키를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-128">Share authentication cookies among ASP.NET Core apps</span></span>

<span data-ttu-id="3b3f8-129">사용할 경우 ASP.NET Core Id:</span><span class="sxs-lookup"><span data-stu-id="3b3f8-129">When using ASP.NET Core Identity:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3b3f8-130">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3b3f8-130">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="3b3f8-131">에 `ConfigureServices` 메서드를 사용 하 여는 [ConfigureApplicationCookie](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.configureapplicationcookie) 확장 메서드를 쿠키에 대 한 데이터 보호 서비스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-131">In the `ConfigureServices` method, use the [ConfigureApplicationCookie](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.configureapplicationcookie) extension method to set up the data protection service for cookies.</span></span>

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.Core/Startup.cs?name=snippet1)]

<span data-ttu-id="3b3f8-132">참조는 *CookieAuthWithIdentity.Core* 프로젝트에 [샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="3b3f8-132">See the *CookieAuthWithIdentity.Core* project in the [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3b3f8-133">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3b3f8-133">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3b3f8-134">에 `Configure` 메서드를 사용 하 여는 [CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions) 를 설정 하려면:</span><span class="sxs-lookup"><span data-stu-id="3b3f8-134">In the `Configure` method, use the [CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions) to set up:</span></span>

* <span data-ttu-id="3b3f8-135">쿠키에 대 한 데이터 보호 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-135">The data protection service for cookies.</span></span>
* <span data-ttu-id="3b3f8-136">`AuthenticationScheme` ASP.NET에 맞게 4.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-136">The `AuthenticationScheme` to match ASP.NET 4.x.</span></span>

```csharp
app.AddIdentity<ApplicationUser, IdentityRole>(options =>
{
    options.Cookies.ApplicationCookie.AuthenticationScheme = 
        "ApplicationCookie";

    var protectionProvider = 
        DataProtectionProvider.Create(
            new DirectoryInfo(@"PATH_TO_KEY_RING_FOLDER"));

    options.Cookies.ApplicationCookie.DataProtectionProvider = 
        protectionProvider;

    options.Cookies.ApplicationCookie.TicketDataFormat = 
        new TicketDataFormat(protectionProvider.CreateProtector(
            "Microsoft.AspNetCore.Authentication.Cookies.CookieAuthenticationMiddleware", 
            "Cookies", 
            "v2"));
});
```

---

<span data-ttu-id="3b3f8-137">쿠키를 직접 사용 하 여 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="3b3f8-137">When using cookies directly:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3b3f8-138">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3b3f8-138">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[](cookie-sharing/sample/CookieAuth.Core/Startup.cs?name=snippet1)]

<span data-ttu-id="3b3f8-139">참조는 *CookieAuth.Core* 프로젝트에 [샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="3b3f8-139">See the *CookieAuth.Core* project in the [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3b3f8-140">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3b3f8-140">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    DataProtectionProvider = 
        DataProtectionProvider.Create(
            new DirectoryInfo(@"PATH_TO_KEY_RING_FOLDER"))
});
```

---

## <a name="encrypting-data-protection-keys-at-rest"></a><span data-ttu-id="3b3f8-141">미사용 데이터 보호 키를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-141">Encrypting data protection keys at rest</span></span>

<span data-ttu-id="3b3f8-142">프로덕션 배포에 구성 된 `DataProtectionProvider` DPAPI 또는 X509Certificate 저장 된 상태의 키를 암호화 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-142">For production deployments, configure the `DataProtectionProvider` to encrypt keys at rest with DPAPI or an X509Certificate.</span></span> <span data-ttu-id="3b3f8-143">참조 [휴지 키 암호화](xref:security/data-protection/implementation/key-encryption-at-rest) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-143">See [Key Encryption At Rest](xref:security/data-protection/implementation/key-encryption-at-rest) for more information.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3b3f8-144">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3b3f8-144">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
services.AddDataProtection()
    .ProtectKeysWithCertificate("thumbprint");
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3b3f8-145">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3b3f8-145">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    DataProtectionProvider = DataProtectionProvider.Create(
        new DirectoryInfo(@"PATH_TO_KEY_RING"),
        configure =>
        {
            configure.ProtectKeysWithCertificate("thumbprint");
        })
});
```

---

## <a name="sharing-authentication-cookies-between-aspnet-4x-and-aspnet-core-apps"></a><span data-ttu-id="3b3f8-146">ASP.NET 4.x 응용 프로그램과 ASP.NET Core 응용 프로그램 간 인증 쿠키 공유하기</span><span class="sxs-lookup"><span data-stu-id="3b3f8-146">Sharing authentication cookies between ASP.NET 4.x and ASP.NET Core apps</span></span>

<span data-ttu-id="3b3f8-147">Katana 쿠키 인증 미들웨어를 사용하는 ASP.NET 4.x 응용 프로그램은 ASP.NET Core 쿠키 인증 미들웨어와 호환되는 인증 쿠키를 생성하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-147">ASP.NET 4.x apps which use Katana cookie authentication middleware can be configured to generate authentication cookies that are compatible with the ASP.NET Core cookie authentication middleware.</span></span> <span data-ttu-id="3b3f8-148">이렇게 하면 사이트 전체에 원활한 SSO 환경을 제공 하면서 증분 대규모 사이트의 개별 응용 프로그램을 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-148">This allows upgrading a large site's individual apps piecemeal while providing a smooth SSO experience across the site.</span></span>

> [!TIP]
> <span data-ttu-id="3b3f8-149">응용 프로그램에서 Katana 쿠키 인증 미들웨어를 사용 하는 경우 호출 `UseCookieAuthentication` 프로젝트의 *Startup.Auth.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-149">When an app uses Katana cookie authentication middleware, it calls `UseCookieAuthentication` in the project's *Startup.Auth.cs* file.</span></span> <span data-ttu-id="3b3f8-150">ASP.NET 4.x 웹 앱 프로젝트는 Visual Studio 2013을 사용 하 여 만든 하 고 나중 Katana 쿠키 인증 미들웨어를 사용 하 여 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-150">ASP.NET 4.x web app projects created with Visual Studio 2013 and later use the Katana cookie authentication middleware by default.</span></span>

> [!NOTE]
> <span data-ttu-id="3b3f8-151">ASP.NET 4.x 앱.NET Framework 4.5.1을 대상 해야 이상.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-151">An ASP.NET 4.x app must target .NET Framework 4.5.1 or higher.</span></span> <span data-ttu-id="3b3f8-152">그렇지 않으면 필요한 NuGet 패키지 설치에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-152">Otherwise, the necessary NuGet packages fail to install.</span></span>

<span data-ttu-id="3b3f8-153">ASP.NET 4.x 앱 및 ASP.NET Core 응용 프로그램 간의 인증 쿠키를 공유 하려면 위에서 설명 했 듯이 ASP.NET Core 응용 프로그램을 구성 하 다음 아래 단계를 수행 하 여 ASP.NET 4.x 앱을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-153">To share authentication cookies among ASP.NET 4.x apps and ASP.NET Core apps, configure the ASP.NET Core app as stated above, then configure the ASP.NET 4.x apps by following the steps below.</span></span>

1. <span data-ttu-id="3b3f8-154">패키지 설치 [Microsoft.Owin.Security.Interop](https://www.nuget.org/packages/Microsoft.Owin.Security.Interop/) 각 ASP.NET 4.x 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-154">Install the package [Microsoft.Owin.Security.Interop](https://www.nuget.org/packages/Microsoft.Owin.Security.Interop/) into each ASP.NET 4.x app.</span></span>

2. <span data-ttu-id="3b3f8-155">*Startup.Auth.cs* 파일에서 `UseCookieAuthentication` 에 대한 호출을 찾고 다음과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-155">In *Startup.Auth.cs*, locate the call to `UseCookieAuthentication` and modify it as follows.</span></span> <span data-ttu-id="3b3f8-156">ASP.NET Core 쿠키 인증 미들웨어에서 사용 하는 이름과 일치 하도록 쿠키 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-156">Change the cookie name to match the name used by the ASP.NET Core cookie authentication middleware.</span></span> <span data-ttu-id="3b3f8-157">인스턴스를 제공는 `DataProtectionProvider` 공통 데이터 보호 키 저장소 위치를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-157">Provide an instance of a `DataProtectionProvider` initialized to the common data protection key storage location.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3b3f8-158">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3b3f8-158">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.NETFramework/CookieAuthWithIdentity.NETFramework/App_Start/Startup.Auth.cs?name=snippet1)]

<span data-ttu-id="3b3f8-159">참조는 *CookieAuthWithIdentity.NETFramework* 프로젝트에 [샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="3b3f8-159">See the *CookieAuthWithIdentity.NETFramework* project in the [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/cookie-sharing/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span>

<span data-ttu-id="3b3f8-160">인증 형식에 정의 된 형식과 일치 해야 사용자 id를 생성할 때 `AuthenticationType` 사용 하 여 설정 `UseCookieAuthentication`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-160">When generating a user identity, the authentication type must match the type defined in `AuthenticationType` set with `UseCookieAuthentication`.</span></span>

<span data-ttu-id="3b3f8-161">*Models/IdentityModels.cs*:</span><span class="sxs-lookup"><span data-stu-id="3b3f8-161">*Models/IdentityModels.cs*:</span></span>

[!code-csharp[](cookie-sharing/sample/CookieAuthWithIdentity.NETFramework/CookieAuthWithIdentity.NETFramework/Models/IdentityModels.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3b3f8-162">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3b3f8-162">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3b3f8-163">설정의 `CookieManager` interop `ChunkingCookieManager` 청크 형식이 호환 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-163">Set the `CookieManager` to interop `ChunkingCookieManager` so the chunking format is compatible.</span></span>

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    AuthenticationType = DefaultAuthenticationTypes.ApplicationCookie,
    CookieName = ".AspNetCore.Cookies",
    // CookieName = ".AspNetCore.ApplicationCookie", (if using ASP.NET Identity)
    // CookiePath = "...", (if necessary)
    // ...
    TicketDataFormat = new AspNetTicketDataFormat(
        new DataProtectorShim(
            DataProtectionProvider.Create(
                new DirectoryInfo(@"PATH_TO_KEY_RING_FOLDER"))
            .CreateProtector(
                "Microsoft.AspNetCore.Authentication.Cookies.CookieAuthenticationMiddleware",
                "Cookies", 
                "v2"))),
    CookieManager = new ChunkingCookieManager()
});
```

---

## <a name="use-a-common-user-database"></a><span data-ttu-id="3b3f8-164">일반 사용자 데이터베이스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3b3f8-164">Use a common user database</span></span>

<span data-ttu-id="3b3f8-165">동일한 사용자 데이터베이스에서 각 앱에 대 한 id 시스템 가리키고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-165">Confirm that the identity system for each app is pointed at the same user database.</span></span> <span data-ttu-id="3b3f8-166">그렇지 않으면 id 시스템 데이터베이스의 정보에 대해 인증 쿠키의 정보와 일치 하려고 할 때 런타임 시 오류를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3f8-166">Otherwise, the identity system produces failures at runtime when it attempts to match the information in the authentication cookie against the information in its database.</span></span>
