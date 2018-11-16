---
title: ASP.NET Core를 사용 하 여 Microsoft 계정 외부 로그인 설정
author: rick-anderson
description: 이 자습서에서는 기존 ASP.NET Core 앱에 Microsoft 계정 사용자 인증의 통합을 보여 줍니다.
ms.author: riande
ms.custom: mvc
ms.date: 11/11/2018
uid: security/authentication/microsoft-logins
ms.openlocfilehash: 89969370cea66b7b6632f1b0be59e135767c831e
ms.sourcegitcommit: 09bcda59a58019fdf47b2db5259fe87acf19dd38
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51708402"
---
# <a name="microsoft-account-external-login-setup-with-aspnet-core"></a><span data-ttu-id="97fdd-103">ASP.NET Core를 사용 하 여 Microsoft 계정 외부 로그인 설정</span><span class="sxs-lookup"><span data-stu-id="97fdd-103">Microsoft Account external login setup with ASP.NET Core</span></span>

<span data-ttu-id="97fdd-104">작성자: [Valeriy Novytskyy](https://github.com/01binary) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="97fdd-104">By [Valeriy Novytskyy](https://github.com/01binary) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="97fdd-105">이 자습서에서 만든 샘플 ASP.NET Core 2.0 프로젝트를 사용 하 여 Microsoft 계정으로 로그인 사용자가 사용 하도록 설정 하는 방법을 보여 줍니다.는 [이전 페이지](xref:security/authentication/social/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-105">This tutorial shows you how to enable your users to sign in with their Microsoft account using a sample ASP.NET Core 2.0 project created on the [previous page](xref:security/authentication/social/index).</span></span>

## <a name="create-the-app-in-microsoft-developer-portal"></a><span data-ttu-id="97fdd-106">Microsoft 개발자 포털에서 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="97fdd-106">Create the app in Microsoft Developer Portal</span></span>

* <span data-ttu-id="97fdd-107">이동할 [ https://apps.dev.microsoft.com ](https://apps.dev.microsoft.com) 만들거나 Microsoft 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-107">Navigate to [https://apps.dev.microsoft.com](https://apps.dev.microsoft.com) and create or sign into a Microsoft account:</span></span>

![로그인 대화 상자](index/_static/MicrosoftDevLogin.png)

<span data-ttu-id="97fdd-109">Microsoft 계정이 아직 없다면 탭  **[만드세요!](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=13&ct=1478151035&rver=6.7.6643.0&wp=SAPI_LONG&wreply=https%3a%2f%2fapps.dev.microsoft.com%2fLoginPostBack&id=293053&aadredir=1&contextid=D70D4F21246BAB50&bk=1478151036&uiflavor=web&uaid=f0c3de863a914c358b8dc01b1ff49e85&mkt=EN-US&lc=1033&lic=1)**</span><span class="sxs-lookup"><span data-stu-id="97fdd-109">If you don't already have a Microsoft account, tap **[Create one!](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=13&ct=1478151035&rver=6.7.6643.0&wp=SAPI_LONG&wreply=https%3a%2f%2fapps.dev.microsoft.com%2fLoginPostBack&id=293053&aadredir=1&contextid=D70D4F21246BAB50&bk=1478151036&uiflavor=web&uaid=f0c3de863a914c358b8dc01b1ff49e85&mkt=EN-US&lc=1033&lic=1)**</span></span> <span data-ttu-id="97fdd-110">로그인 한 후 리디렉션됩니다 **내 응용 프로그램** 페이지:</span><span class="sxs-lookup"><span data-stu-id="97fdd-110">After signing in you are redirected to **My applications** page:</span></span>

![Microsoft Edge에서 열린 Microsoft 개발자 포털](index/_static/MicrosoftDev.png)

* <span data-ttu-id="97fdd-112">탭 **앱 추가** 오른쪽 상단 모서리에 입력 하 **응용 프로그램 이름** 하 고 **Contact Email**:</span><span class="sxs-lookup"><span data-stu-id="97fdd-112">Tap **Add an app** in the upper right corner and enter your **Application Name** and **Contact Email**:</span></span>

![새 응용 프로그램 등록 대화 상자](index/_static/MicrosoftDevAppCreate.png)

* <span data-ttu-id="97fdd-114">이 자습서에서는 선택을 취소 합니다 **안내식 설정** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-114">For the purposes of this tutorial, clear the **Guided Setup** check box.</span></span>

* <span data-ttu-id="97fdd-115">탭 **Create** 를 계속 합니다 **등록** 페이지.</span><span class="sxs-lookup"><span data-stu-id="97fdd-115">Tap **Create** to continue to the **Registration** page.</span></span> <span data-ttu-id="97fdd-116">제공을 **이름** 의 값을 확인 합니다 **응용 프로그램 Id**,으로 사용 하는 `ClientId` 자습서의에서 뒷부분에서:</span><span class="sxs-lookup"><span data-stu-id="97fdd-116">Provide a **Name** and note the value of the **Application Id**, which you use as `ClientId` later in the tutorial:</span></span>

![등록 페이지](index/_static/MicrosoftDevAppReg.png)

* <span data-ttu-id="97fdd-118">탭 **플랫폼 추가** 에 **플랫폼** 섹션을 선택 합니다 **웹** 플랫폼:</span><span class="sxs-lookup"><span data-stu-id="97fdd-118">Tap **Add Platform** in the **Platforms** section and select the **Web** platform:</span></span>

![추가 플랫폼 대화 상자](index/_static/MicrosoftDevAppPlatform.png)

* <span data-ttu-id="97fdd-120">새 **웹** 플랫폼 섹션에서 사용 하 여 개발 URL 입력 `/signin-microsoft` 에 추가 합니다 **리디렉션 Url** 필드 (예를 들어: `https://localhost:44320/signin-microsoft`).</span><span class="sxs-lookup"><span data-stu-id="97fdd-120">In the new **Web** platform section, enter your development URL with `/signin-microsoft` appended into the **Redirect URLs** field (for example: `https://localhost:44320/signin-microsoft`).</span></span> <span data-ttu-id="97fdd-121">이 자습서의 뒷부분에서 구성 된 Microsoft 인증 체계에서 요청을 자동으로 처리 됩니다 `/signin-microsoft` OAuth 흐름을 구현 하는 경로:</span><span class="sxs-lookup"><span data-stu-id="97fdd-121">The Microsoft authentication scheme configured later in this tutorial will automatically handle requests at `/signin-microsoft` route to implement the OAuth flow:</span></span>

![웹 플랫폼 섹션](index/_static/MicrosoftRedirectUri.png)

> [!NOTE]
> <span data-ttu-id="97fdd-123">URI 세그먼트 `/signin-microsoft` Microsoft 인증 공급자의 기본 콜백으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-123">The URI segment `/signin-microsoft` is set as the default callback of the Microsoft authentication provider.</span></span> <span data-ttu-id="97fdd-124">상속을 통해 Microsoft 인증 미들웨어를 구성 하는 동안 기본 콜백 URI를 변경할 수 있습니다 [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath) 의 속성을 [MicrosoftAccountOptions](/dotnet/api/microsoft.aspnetcore.authentication.microsoftaccount.microsoftaccountoptions) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-124">You can change the default callback URI while configuring the Microsoft authentication middleware via the inherited [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath) property of the [MicrosoftAccountOptions](/dotnet/api/microsoft.aspnetcore.authentication.microsoftaccount.microsoftaccountoptions) class.</span></span>

* <span data-ttu-id="97fdd-125">탭 **URL 추가** URL가 추가 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-125">Tap **Add URL** to ensure the URL was added.</span></span>

* <span data-ttu-id="97fdd-126">필요한 경우 다른 응용 프로그램 설정 작성 하 고 탭 **저장할** 앱 구성에 변경 내용을 저장 하려면 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-126">Fill out any other application settings if necessary and tap **Save** at the bottom of the page to save changes to app configuration.</span></span>

* <span data-ttu-id="97fdd-127">다시 방문 해야 사이트를 배포 하는 경우는 **등록** 페이지 및 새 공용 URL을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-127">When deploying the site you'll need to revisit the **Registration** page and set a new public URL.</span></span>

## <a name="store-microsoft-application-id-and-password"></a><span data-ttu-id="97fdd-128">Microsoft 응용 프로그램 Id 및 암호를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-128">Store Microsoft Application Id and Password</span></span>

* <span data-ttu-id="97fdd-129">참고 합니다 `Application Id` 에 표시 합니다 **등록** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-129">Note the `Application Id` displayed on the **Registration** page.</span></span>

* <span data-ttu-id="97fdd-130">탭 **새 암호 생성** 에 **응용 프로그램 비밀** 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-130">Tap **Generate New Password** in the **Application Secrets** section.</span></span> <span data-ttu-id="97fdd-131">이 응용 프로그램 암호를 복사할 수 있는 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-131">This displays a box where you can copy the application password:</span></span>

![새 암호가 생성 대화 상자](index/_static/MicrosoftDevPassword.png)

<span data-ttu-id="97fdd-133">Microsoft와 같은 중요 한 설정이 연결 `Application ID` 하 고 `Password` 사용 하 여 응용 프로그램 구성에는 [암호 관리자](xref:security/app-secrets)합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-133">Link sensitive settings like Microsoft `Application ID` and `Password` to your application configuration using the [Secret Manager](xref:security/app-secrets).</span></span> <span data-ttu-id="97fdd-134">이 자습서에서는 이름을 토큰 `Authentication:Microsoft:ApplicationId` 고 `Authentication:Microsoft:Password`입니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-134">For the purposes of this tutorial, name the tokens `Authentication:Microsoft:ApplicationId` and `Authentication:Microsoft:Password`.</span></span>

## <a name="configure-microsoft-account-authentication"></a><span data-ttu-id="97fdd-135">Microsoft 계정 인증 구성</span><span class="sxs-lookup"><span data-stu-id="97fdd-135">Configure Microsoft Account Authentication</span></span>

<span data-ttu-id="97fdd-136">이 자습서에 사용 되는 프로젝트 템플릿이 되도록 [Microsoft.AspNetCore.Authentication.MicrosoftAccount](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.MicrosoftAccount) 패키지가 이미 설치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-136">The project template used in this tutorial ensures that [Microsoft.AspNetCore.Authentication.MicrosoftAccount](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.MicrosoftAccount) package is already installed.</span></span>

* <span data-ttu-id="97fdd-137">Visual Studio 2017을 사용 하 여이 패키지를 설치 하려면 마우스 오른쪽 단추로 클릭 프로젝트를 마우스 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-137">To install this package with Visual Studio 2017, right-click on the project and select **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="97fdd-138">.NET Core CLI를 설치 하려면 프로젝트 디렉터리에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-138">To install with .NET Core CLI, execute the following in your project directory:</span></span>

   `dotnet add package Microsoft.AspNetCore.Authentication.MicrosoftAccount`

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="97fdd-139">Microsoft 계정 서비스에 추가 합니다 `ConfigureServices` 의 메서드 *Startup.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="97fdd-139">Add the Microsoft Account service in the `ConfigureServices` method in *Startup.cs* file:</span></span>

```csharp
services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

services.AddAuthentication().AddMicrosoftAccount(microsoftOptions =>
{
    microsoftOptions.ClientId = Configuration["Authentication:Microsoft:ApplicationId"];
    microsoftOptions.ClientSecret = Configuration["Authentication:Microsoft:Password"];
});
```

[!INCLUDE [default settings configuration](includes/default-settings.md)]

[!INCLUDE[](includes/chain-auth-providers.md)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="97fdd-140">Microsoft 계정 미들웨어를 추가 합니다 `Configure` 의 메서드 *Startup.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="97fdd-140">Add the Microsoft Account middleware in the `Configure` method in *Startup.cs* file:</span></span>

```csharp
app.UseMicrosoftAccountAuthentication(new MicrosoftAccountOptions()
{
    ClientId = Configuration["Authentication:Microsoft:ApplicationId"],
    ClientSecret = Configuration["Authentication:Microsoft:Password"]
});
```

::: moniker-end

<span data-ttu-id="97fdd-141">하지만 Microsoft 개발자 포털에서 사용 되는 용어 이름은 이러한 토큰 `ApplicationId` 하 고 `Password`,으로 노출 하는 `ClientId` 및 `ClientSecret` 구성 API에.</span><span class="sxs-lookup"><span data-stu-id="97fdd-141">Although the terminology used on Microsoft Developer Portal names these tokens `ApplicationId` and `Password`, they're exposed as `ClientId` and `ClientSecret` to the configuration API.</span></span>

<span data-ttu-id="97fdd-142">참조 된 [MicrosoftAccountOptions](/dotnet/api/microsoft.aspnetcore.builder.microsoftaccountoptions) Microsoft 계정 인증에서 지 원하는 구성 옵션에 대 한 자세한 내용은 API 참조.</span><span class="sxs-lookup"><span data-stu-id="97fdd-142">See the [MicrosoftAccountOptions](/dotnet/api/microsoft.aspnetcore.builder.microsoftaccountoptions) API reference for more information on configuration options supported by Microsoft Account authentication.</span></span> <span data-ttu-id="97fdd-143">이 사용 하 여 사용자에 대 한 다른 정보를 요청할 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-143">This can be used to request different information about the user.</span></span>

## <a name="sign-in-with-microsoft-account"></a><span data-ttu-id="97fdd-144">Microsoft 계정으로 로그인</span><span class="sxs-lookup"><span data-stu-id="97fdd-144">Sign in with Microsoft Account</span></span>

<span data-ttu-id="97fdd-145">응용 프로그램을 실행 하 고 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-145">Run your application and click **Log in**.</span></span> <span data-ttu-id="97fdd-146">Microsoft에 로그인 하는 옵션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-146">An option to sign in with Microsoft appears:</span></span>

![웹 페이지에서 응용 프로그램 로그: 인증 되지 않은 사용자](index/_static/DoneMicrosoft.png)

<span data-ttu-id="97fdd-148">Microsoft를 클릭 하면 리디렉션됩니다 Microsoft 인증에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-148">When you click on Microsoft, you are redirected to Microsoft for authentication.</span></span> <span data-ttu-id="97fdd-149">(아직 로그인 하지 않은) 하는 경우 Microsoft 계정으로 로그인 한 후 앱 정보에 액세스할 수 있도록 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-149">After signing in with your Microsoft Account (if not already signed in) you will be prompted to let the app access your info:</span></span>

![Microsoft 인증 대화 상자](index/_static/MicrosoftLogin.png)

<span data-ttu-id="97fdd-151">탭 **예** 및 전자 메일을 설정할 수 있는 웹 사이트로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-151">Tap **Yes** and you will be redirected back to the web site where you can set your email.</span></span>

<span data-ttu-id="97fdd-152">이제 Microsoft 자격 증명을 사용 하 여 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-152">You are now logged in using your Microsoft credentials:</span></span>

![웹 응용 프로그램: 사용자 인증](index/_static/Done.png)

[!INCLUDE[Forward request information when behind a proxy or load balancer section](includes/forwarded-headers-middleware.md)]

## <a name="troubleshooting"></a><span data-ttu-id="97fdd-154">문제 해결</span><span class="sxs-lookup"><span data-stu-id="97fdd-154">Troubleshooting</span></span>

* <span data-ttu-id="97fdd-155">Microsoft 계정 공급자는 로그인 오류 페이지로 리디렉션됩니다, 하는 경우 오류 제목과 설명을 쿼리 문자열 매개 변수 바로 다음을 유의 합니다 `#` (해시 태그) Uri에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-155">If the Microsoft Account provider redirects you to a sign in error page, note the error title and description query string parameters directly following the `#` (hashtag) in the Uri.</span></span>

  <span data-ttu-id="97fdd-156">가장 일반적인 원인은 응용 프로그램의 모든 일치 하지 않는 Uri 오류 메시지는 Microsoft 인증에 문제가 있음을 나타낼 것 처럼 보이지만, 합니다 **리디렉션 Uri** 에 대해 지정 된 된 **웹** 플랫폼 .</span><span class="sxs-lookup"><span data-stu-id="97fdd-156">Although the error message seems to indicate a problem with Microsoft authentication, the most common cause is your application Uri not matching any of the **Redirect URIs** specified for the **Web** platform.</span></span>
* <span data-ttu-id="97fdd-157">**ASP.NET Core 2.x만:** 경우 Identity를 호출 하 여 구성 되지 않았습니다 `services.AddIdentity` 에 `ConfigureServices`에 인증 하려고 하면 *ArgumentException: 'SignInScheme' 옵션을 제공 해야*합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-157">**ASP.NET Core 2.x only:** If Identity isn't configured by calling `services.AddIdentity` in `ConfigureServices`, attempting to authenticate will result in *ArgumentException: The 'SignInScheme' option must be provided*.</span></span> <span data-ttu-id="97fdd-158">이 자습서에 사용 되는 프로젝트 템플릿이이 수행 되도록 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-158">The project template used in this tutorial ensures that this is done.</span></span>
* <span data-ttu-id="97fdd-159">사이트 데이터베이스를 초기 마이그레이션을 적용 하 여 만들어지지 않은, 경우 받습니다 *요청을 처리 하는 동안 데이터베이스 작업이 실패 했습니다.* 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-159">If the site database has not been created by applying the initial migration, you will get *A database operation failed while processing the request* error.</span></span> <span data-ttu-id="97fdd-160">탭 **마이그레이션 적용** 데이터베이스를 만들고 오류 지 나 새로 고침 합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-160">Tap **Apply Migrations** to create the database and refresh to continue past the error.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97fdd-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="97fdd-161">Next steps</span></span>

* <span data-ttu-id="97fdd-162">이 문서에서는 Microsoft를 사용 하 여 인증 하는 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-162">This article showed how you can authenticate with Microsoft.</span></span> <span data-ttu-id="97fdd-163">에 나열 된 다른 공급자를 사용 하 여 인증 하는 유사한 방법을 따를 수 있습니다 합니다 [이전 페이지](xref:security/authentication/social/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-163">You can follow a similar approach to authenticate with other providers listed on the [previous page](xref:security/authentication/social/index).</span></span>

* <span data-ttu-id="97fdd-164">새 만들어야 Azure 웹 앱에 웹 사이트를 게시 하면 `Password` Microsoft 개발자 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-164">Once you publish your web site to Azure web app, you should create a new `Password` in the Microsoft Developer Portal.</span></span>

* <span data-ttu-id="97fdd-165">설정 된 `Authentication:Microsoft:ApplicationId` 및 `Authentication:Microsoft:Password` Azure portal에서 응용 프로그램 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-165">Set the `Authentication:Microsoft:ApplicationId` and `Authentication:Microsoft:Password` as application settings in the Azure portal.</span></span> <span data-ttu-id="97fdd-166">구성 시스템 환경 변수에서 키를 읽을 수 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97fdd-166">The configuration system is set up to read keys from environment variables.</span></span>
