---
title: ASP.NET Core에서는 Ws-federation로 사용자를 인증
author: chlowell
description: 이 자습서에서는 ASP.NET Core 응용 프로그램의 Ws-federation을 사용 하는 방법을 설명 합니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 02/27/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/ws-federation
ms.openlocfilehash: d4621c7b97678903b9f2562e353da3883334b599
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30898806"
---
# <a name="authenticate-users-with-ws-federation-in-aspnet-core"></a><span data-ttu-id="852b4-103">ASP.NET Core에서는 Ws-federation로 사용자를 인증</span><span class="sxs-lookup"><span data-stu-id="852b4-103">Authenticate users with WS-Federation in ASP.NET Core</span></span>

<span data-ttu-id="852b4-104">이 자습서에서는 사용자가 WS-페더레이션 인증 공급자와 같은 페더레이션 서비스 ADFS (Active Directory)로 로그인 할 수 있도록 하는 방법을 설명 또는 [Azure Active Directory](/azure/active-directory/) (AAD).</span><span class="sxs-lookup"><span data-stu-id="852b4-104">This tutorial demonstrates how to enable users to sign in with a WS-Federation authentication provider like Active Directory Federation Services (ADFS) or [Azure Active Directory](/azure/active-directory/) (AAD).</span></span> <span data-ttu-id="852b4-105">에 설명 된 ASP.NET 코어 2.0 샘플 응용 프로그램을 사용 하 여 [Facebook, Google, 및 외부 공급자 인증](xref:security/authentication/social/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-105">It uses the ASP.NET Core 2.0 sample app described in [Facebook, Google, and external provider authentication](xref:security/authentication/social/index).</span></span>

<span data-ttu-id="852b4-106">ASP.NET Core 2.0 응용 프로그램의 경우 Ws-federation 지원은가 제공 [Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation)합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-106">For ASP.NET Core 2.0 apps, WS-Federation support is provided by [Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation).</span></span> <span data-ttu-id="852b4-107">이 구성 요소에서 이식는 [Microsoft.Owin.Security.WsFederation](https://www.nuget.org/packages/Microsoft.Owin.Security.WsFederation) 및 해당 구성 요소의 메커니즘을 많이 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-107">This component is ported from [Microsoft.Owin.Security.WsFederation](https://www.nuget.org/packages/Microsoft.Owin.Security.WsFederation) and shares many of that component's mechanics.</span></span> <span data-ttu-id="852b4-108">그러나 구성 요소는 몇 가지 중요 한 방법으로 다.</span><span class="sxs-lookup"><span data-stu-id="852b4-108">However, the components differ in a couple of important ways.</span></span>

<span data-ttu-id="852b4-109">기본적으로 새 미들웨어:</span><span class="sxs-lookup"><span data-stu-id="852b4-109">By default, the new middleware:</span></span>

* <span data-ttu-id="852b4-110">원치 않는 로그인을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-110">Doesn't allow unsolicited logins.</span></span> <span data-ttu-id="852b4-111">이 Ws-federation 프로토콜 기능은 XSRF 공격에 취약 합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-111">This feature of the WS-Federation protocol is vulnerable to XSRF attacks.</span></span> <span data-ttu-id="852b4-112">그러나으로 사용할 수 있습니다는 `AllowUnsolicitedLogins` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-112">However, it can be enabled with the `AllowUnsolicitedLogins` option.</span></span>
* <span data-ttu-id="852b4-113">로그인 메시지에 대 한 모든 폼 게시를 검사 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-113">Doesn't check every form post for sign-in messages.</span></span> <span data-ttu-id="852b4-114">만 요청을 `CallbackPath` 기호 기능에 대 한 검사 `CallbackPath` 기본값으로 `/signin-wsfed` 되지만 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-114">Only requests to the `CallbackPath` are checked for sign-ins. `CallbackPath` defaults to `/signin-wsfed` but can be changed.</span></span> <span data-ttu-id="852b4-115">이 경로 사용 하 여 다른 인증 공급자와 공유할 수는 `SkipUnrecognizedRequests` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-115">This path can be shared with other authentication providers by enabling the `SkipUnrecognizedRequests` option.</span></span>

## <a name="register-the-app-with-active-directory"></a><span data-ttu-id="852b4-116">Active Directory에 앱 등록</span><span class="sxs-lookup"><span data-stu-id="852b4-116">Register the app with Active Directory</span></span>

### <a name="active-directory-federation-services"></a><span data-ttu-id="852b4-117">Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="852b4-117">Active Directory Federation Services</span></span>

* <span data-ttu-id="852b4-118">서버를 열고 **신뢰 당사자 트러스트 추가 마법사** ADFS 관리 콘솔에서:</span><span class="sxs-lookup"><span data-stu-id="852b4-118">Open the server's **Add Relying Party Trust Wizard** from the ADFS Management console:</span></span>

![신뢰 당사자 트러스트 마법사 추가: 시작](ws-federation/_static/AdfsAddTrust.png)

* <span data-ttu-id="852b4-120">데이터를 수동으로 입력 하려면 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-120">Choose to enter data manually:</span></span>

![데이터 원본을 선택 신뢰 당사자 트러스트 추가 마법사:](ws-federation/_static/AdfsSelectDataSource.png)

* <span data-ttu-id="852b4-122">신뢰 당사자에 대 한 표시 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-122">Enter a display name for the relying party.</span></span> <span data-ttu-id="852b4-123">이름이는 ASP.NET Core 응용 프로그램에 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-123">The name isn't important to the ASP.NET Core app.</span></span>

* <span data-ttu-id="852b4-124">[Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation) 토큰 암호화 인증서를 구성 하지 않으면 하므로 토큰 암호화에 대 한 지원이 부족 합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-124">[Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation) lacks support for token encryption, so don't configure a token encryption certificate:</span></span>

![인증서를 구성 신뢰 당사자 트러스트 추가 마법사:](ws-federation/_static/AdfsConfigureCert.png)

* <span data-ttu-id="852b4-126">응용 프로그램의 URL을 사용 하 여 Ws-federation 수동 프로토콜 지원을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-126">Enable support for WS-Federation Passive protocol, using the app's URL.</span></span> <span data-ttu-id="852b4-127">응용 프로그램에 대 한 올바른 포트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-127">Verify the port is correct for the app:</span></span>

![URL 구성 신뢰 당사자 트러스트 추가 마법사:](ws-federation/_static/AdfsConfigureUrl.png)

> [!NOTE]
> <span data-ttu-id="852b4-129">HTTPS URL 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-129">This must be an HTTPS URL.</span></span> <span data-ttu-id="852b4-130">IIS Express 응용 프로그램을 개발 하는 동안 호스트 하는 경우 자체 서명 된 인증서를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-130">IIS Express can provide a self-signed certificate when hosting the app during development.</span></span> <span data-ttu-id="852b4-131">Kestrel은 인증서를 수동으로 구성을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-131">Kestrel requires manual certificate configuration.</span></span> <span data-ttu-id="852b4-132">참조는 [Kestrel 설명서](xref:fundamentals/servers/kestrel) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-132">See the [Kestrel documentation](xref:fundamentals/servers/kestrel) for more details.</span></span>

* <span data-ttu-id="852b4-133">클릭 **다음** 마법사의 나머지 부분을 및 **닫기** 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-133">Click **Next** through the rest of the wizard and **Close** at the end.</span></span>

* <span data-ttu-id="852b4-134">ASP.NET Core Id 필요는 **이름 ID** 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-134">ASP.NET Core Identity requires a **Name ID** claim.</span></span> <span data-ttu-id="852b4-135">추가 된 **클레임 규칙 편집** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="852b4-135">Add one from the **Edit Claim Rules** dialog:</span></span>

![클레임 규칙 편집](ws-federation/_static/EditClaimRules.png)

* <span data-ttu-id="852b4-137">에 **변환 클레임 규칙 추가 마법사**, 기본값을 그대로 적용 **LDAP 특성을 클레임으로 보내기** 서식 파일을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-137">In the **Add Transform Claim Rule Wizard**, leave the default **Send LDAP Attributes as Claims** template selected, and click **Next**.</span></span> <span data-ttu-id="852b4-138">규칙 매핑을 추가 **SAM 계정 이름을** LDAP 특성을는 **이름 ID** 나가는 클레임:</span><span class="sxs-lookup"><span data-stu-id="852b4-138">Add a rule mapping the **SAM-Account-Name** LDAP attribute to the **Name ID** outgoing claim:</span></span>

![클레임 규칙 구성 변환 클레임 규칙 추가 마법사:](ws-federation/_static/AddTransformClaimRule.png)

* <span data-ttu-id="852b4-140">클릭 **마침** > **확인** 에 **클레임 규칙 편집** 창.</span><span class="sxs-lookup"><span data-stu-id="852b4-140">Click **Finish** > **OK** in the **Edit Claim Rules** window.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="852b4-141">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="852b4-141">Azure Active Directory</span></span>

* <span data-ttu-id="852b4-142">AAD 테 넌 트의 응용 프로그램 등록 블레이드로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-142">Navigate to the AAD tenant's app registrations blade.</span></span> <span data-ttu-id="852b4-143">클릭 **새 응용 프로그램 등록**:</span><span class="sxs-lookup"><span data-stu-id="852b4-143">Click **New application registration**:</span></span>

![Azure Active Directory: 응용 프로그램 등록](ws-federation/_static/AadNewAppRegistration.png)

* <span data-ttu-id="852b4-145">앱 등록에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-145">Enter a name for the app registration.</span></span> <span data-ttu-id="852b4-146">이 ASP.NET Core 응용 프로그램에 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-146">This isn't important to the ASP.NET Core app.</span></span>
* <span data-ttu-id="852b4-147">로 응용 프로그램에서 수신 대기 하는 URL을 입력에서 **로그온 URL**:</span><span class="sxs-lookup"><span data-stu-id="852b4-147">Enter the URL the app listens on as the **Sign-on URL**:</span></span>

![Azure Active Directory: 응용 프로그램 등록 만들기](ws-federation/_static/AadCreateAppRegistration.png)

* <span data-ttu-id="852b4-149">클릭 **끝점** 확인는 **페더레이션 메타 데이터 문서** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-149">Click **Endpoints** and note the **Federation Metadata Document** URL.</span></span> <span data-ttu-id="852b4-150">이 Ws-federation 미들웨어 `MetadataAddress`:</span><span class="sxs-lookup"><span data-stu-id="852b4-150">This is the WS-Federation middleware's `MetadataAddress`:</span></span>

![Azure Active Directory: 끝점](ws-federation/_static/AadFederationMetadataDocument.png)

* <span data-ttu-id="852b4-152">새 응용 프로그램 등록으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-152">Navigate to the new app registration.</span></span> <span data-ttu-id="852b4-153">클릭 **설정** > **속성** 를 기록 하 고는 **앱 ID URI**합니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-153">Click **Settings** > **Properties** and make note of the **App ID URI**.</span></span> <span data-ttu-id="852b4-154">이 Ws-federation 미들웨어 `Wtrealm`:</span><span class="sxs-lookup"><span data-stu-id="852b4-154">This is the WS-Federation middleware's `Wtrealm`:</span></span>

![Azure Active Directory: 응용 프로그램 등록 속성](ws-federation/_static/AadAppIdUri.png)

## <a name="add-ws-federation-as-an-external-login-provider-for-aspnet-core-identity"></a><span data-ttu-id="852b4-156">WS-페더레이션 ASP.NET Core Id에 대 한 외부 로그인 공급자로 추가</span><span class="sxs-lookup"><span data-stu-id="852b4-156">Add WS-Federation as an external login provider for ASP.NET Core Identity</span></span>

* <span data-ttu-id="852b4-157">대 한 종속성 추가 [Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation) 프로젝트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-157">Add a dependency on [Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation) to the project.</span></span>
* <span data-ttu-id="852b4-158">Ws-federation을 추가 `Configure` 메서드에서 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="852b4-158">Add WS-Federation to the `Configure` method in *Startup.cs*:</span></span>

    ```csharp
    services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

    services.AddAuthentication()
        .AddWsFederation(options =>
        {
            // MetadataAddress represents the Active Directory instance used to authenticate users.
            options.MetadataAddress = "https://<ADFS FQDN or AAD tenant>/FederationMetadata/2007-06/FederationMetadata.xml";

            // Wtrealm is the app's identifier in the Active Directory instance.
            // For ADFS, use the relying party's identifier, its WS-Federation Passive protocol URL:
            options.Wtrealm = "https://localhost:44307/";

            // For AAD, use the App ID URI from the app registration's Properties blade:
            options.Wtrealm = "https://wsfedsample.onmicrosoft.com/bf0e7e6d-056e-4e37-b9a6-2c36797b9f01";
        });

    services.AddMvc()
     // ...
    ```

[!INCLUDE [default settings configuration](social/includes/default-settings.md)]

### <a name="log-in-with-ws-federation"></a><span data-ttu-id="852b4-159">Ws-federation 로그인</span><span class="sxs-lookup"><span data-stu-id="852b4-159">Log in with WS-Federation</span></span>

<span data-ttu-id="852b4-160">응용 프로그램 찾아서 클릭은 **로그인** nav 헤더의 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-160">Browse to the app and click the **Log in** link in the nav header.</span></span> <span data-ttu-id="852b4-161">WsFederation으로 로그인 하는 옵션은: ![로그인 페이지](ws-federation/_static/WsFederationButton.png)</span><span class="sxs-lookup"><span data-stu-id="852b4-161">There's an option to log in with WsFederation: ![Log in page](ws-federation/_static/WsFederationButton.png)</span></span>

<span data-ttu-id="852b4-162">Ad FS 로그인 페이지를 리디렉션합니다 단추 공급자로 adfs를: ![ADFS 로그인 페이지](ws-federation/_static/AdfsLoginPage.png)</span><span class="sxs-lookup"><span data-stu-id="852b4-162">With ADFS as the provider, the button redirects to an ADFS sign-in page: ![ADFS sign-in page](ws-federation/_static/AdfsLoginPage.png)</span></span>

<span data-ttu-id="852b4-163">공급자와 Azure Active Directory와 단추를 AAD에 로그인 페이지로 리디렉션합니다: ![AAD 로그인 페이지](ws-federation/_static/AadSignIn.png)</span><span class="sxs-lookup"><span data-stu-id="852b4-163">With Azure Active Directory as the provider, the button redirects to an AAD sign-in page: ![AAD sign-in page](ws-federation/_static/AadSignIn.png)</span></span>

<span data-ttu-id="852b4-164">한 성공적인 로그인에서 새 사용자에 대 한 응용 프로그램의 사용자 등록 페이지를 리디렉션합니다: ![등록 페이지](ws-federation/_static/Register.png)</span><span class="sxs-lookup"><span data-stu-id="852b4-164">A successful sign-in for a new user redirects to the app's user registration page: ![Register page](ws-federation/_static/Register.png)</span></span>

## <a name="use-ws-federation-without-aspnet-core-identity"></a><span data-ttu-id="852b4-165">ASP.NET Core Identity 없이 Ws-federation을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="852b4-165">Use WS-Federation without ASP.NET Core Identity</span></span>

<span data-ttu-id="852b4-166">WS-페더레이션 미들웨어 Identity 없이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="852b4-166">The WS-Federation middleware can be used without Identity.</span></span> <span data-ttu-id="852b4-167">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="852b4-167">For example:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddAuthentication(sharedOptions =>
    {
        sharedOptions.DefaultScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        sharedOptions.DefaultSignInScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        sharedOptions.DefaultChallengeScheme = WsFederationDefaults.AuthenticationScheme;
    })
    .AddWsFederation(options =>
    {
        options.Wtrealm = Configuration["wsfed:realm"];
        options.MetadataAddress = Configuration["wsfed:metadata"];
    })
    .AddCookie();
}

public void Configure(IApplicationBuilder app)
{
    app.UseAuthentication();
        // …
}
```
