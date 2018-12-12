---
title: ASP.NET Core에서 Google 외부 로그인 설정
author: rick-anderson
description: 이 자습서에서는 기존 ASP.NET Core 앱에 Google 계정 사용자 인증의 통합을 보여 줍니다.
ms.author: riande
ms.custom: mvc, seodec18
ms.date: 11/11/2018
uid: security/authentication/google-logins
ms.openlocfilehash: 372504eb4f6fea412b5b160e0d5e9251dafe0d56
ms.sourcegitcommit: b34b25da2ab68e6495b2460ff570468f16a9bf0d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53284496"
---
# <a name="google-external-login-setup-in-aspnet-core"></a><span data-ttu-id="a2599-103">ASP.NET Core에서 Google 외부 로그인 설정</span><span class="sxs-lookup"><span data-stu-id="a2599-103">Google external login setup in ASP.NET Core</span></span>

<span data-ttu-id="a2599-104">작성자: [Valeriy Novytskyy](https://github.com/01binary) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a2599-104">By [Valeriy Novytskyy](https://github.com/01binary) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="a2599-105">이 자습서에서 만든 샘플 ASP.NET Core 2.0 프로젝트를 사용 하 여 Google + 계정으로 로그인 사용자가 사용 하도록 설정 하는 방법을 보여 줍니다.는 [이전 페이지](xref:security/authentication/social/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-105">This tutorial shows you how to enable your users to sign in with their Google+ account using a sample ASP.NET Core 2.0 project created on the [previous page](xref:security/authentication/social/index).</span></span> <span data-ttu-id="a2599-106">수행 하 여 시작 합니다 [공식 단계](https://developers.google.com/identity/sign-in/web/devconsole-project) Google API 콘솔에서 새 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-106">We start by following the [official steps](https://developers.google.com/identity/sign-in/web/devconsole-project) to create a new app in Google API Console.</span></span>

## <a name="create-the-app-in-google-api-console"></a><span data-ttu-id="a2599-107">Google API 콘솔에서 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="a2599-107">Create the app in Google API Console</span></span>

* <span data-ttu-id="a2599-108">이동할 [ https://console.developers.google.com/projectselector/apis/library ](https://console.developers.google.com/projectselector/apis/library) 에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-108">Navigate to [https://console.developers.google.com/projectselector/apis/library](https://console.developers.google.com/projectselector/apis/library) and sign in.</span></span> <span data-ttu-id="a2599-109">사용 하 여 Google 계정이 아직 없다면 **더 많은 옵션** > **[계정을 만들려면](https://accounts.google.com/SignUpWithoutGmail?service=cloudconsole&continue=https%3A%2F%2Fconsole.developers.google.com%2Fprojectselector%2Fapis%2Flibrary&ltmpl=api)**  만들려면 링크:</span><span class="sxs-lookup"><span data-stu-id="a2599-109">If you don't already have a Google account, use **More options** > **[Create account](https://accounts.google.com/SignUpWithoutGmail?service=cloudconsole&continue=https%3A%2F%2Fconsole.developers.google.com%2Fprojectselector%2Fapis%2Flibrary&ltmpl=api)** link to create one:</span></span>

![Google API 콘솔](index/_static/GoogleConsoleLogin.png)

* <span data-ttu-id="a2599-111">리디렉션됩니다 **API Manager 라이브러리** 페이지:</span><span class="sxs-lookup"><span data-stu-id="a2599-111">You are redirected to **API Manager Library** page:</span></span>

![API Manager 라이브러리 페이지 방문](index/_static/GoogleConsoleSwitchboard.png)

* <span data-ttu-id="a2599-113">탭 **Create** 입력 하 **프로젝트 이름을**:</span><span class="sxs-lookup"><span data-stu-id="a2599-113">Tap **Create** and enter your **Project name**:</span></span>

![새 프로젝트 대화 상자](index/_static/GoogleConsoleNewProj.png)

* <span data-ttu-id="a2599-115">대화 상자를 수락 하면 새 앱에 대 한 기능을 선택할 수 있도록 라이브러리 페이지로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-115">After accepting the dialog, you are redirected back to the Library page allowing you to choose features for your new app.</span></span> <span data-ttu-id="a2599-116">찾을 **Google + API** 목록 및 API 기능을 추가 하려면 해당 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-116">Find **Google+ API** in the list and click on its link to add the API feature:</span></span>

![API Manager 라이브러리 페이지에서 "Google + API"에 대 한 검색](index/_static/GoogleConsoleChooseApi.png)

* <span data-ttu-id="a2599-118">새로 추가 된 API에 대 한 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-118">The page for the newly added API is displayed.</span></span> <span data-ttu-id="a2599-119">탭 **사용** 기능에서 앱에 Google + 기호를 추가 하려면:</span><span class="sxs-lookup"><span data-stu-id="a2599-119">Tap **Enable** to add Google+ sign in feature to your app:</span></span>

![API Manager Google + API 페이지 방문](index/_static/GoogleConsoleEnableApi.png)

* <span data-ttu-id="a2599-121">API를 사용 하도록 설정한 후 탭 **자격 증명 만들기** 암호를 구성 하려면:</span><span class="sxs-lookup"><span data-stu-id="a2599-121">After enabling the API, tap **Create credentials** to configure the secrets:</span></span>

![API Manager Google + API 페이지에서 자격 증명 단추 만들기](index/_static/GoogleConsoleGoCredentials.png)

* <span data-ttu-id="a2599-123">다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-123">Choose:</span></span>
  * <span data-ttu-id="a2599-124">**Google+ API**</span><span class="sxs-lookup"><span data-stu-id="a2599-124">**Google+ API**</span></span>
  * <span data-ttu-id="a2599-125">**웹 서버 (예:: node.js, Tomcat)**, 및</span><span class="sxs-lookup"><span data-stu-id="a2599-125">**Web server (e.g. node.js, Tomcat)**, and</span></span>
  * <span data-ttu-id="a2599-126">**사용자 데이터**:</span><span class="sxs-lookup"><span data-stu-id="a2599-126">**User data**:</span></span>

![API 관리자 자격 증명 페이지: 어떤 종류의 자격 증명에 대해 알아보세요 필요한 패널](index/_static/GoogleConsoleChooseCred.png)

* <span data-ttu-id="a2599-128">탭 **어떤 자격 증명 필요 합니까?** 안내 하는 앱 구성의 두 번째 단계로 **OAuth 2.0 클라이언트 ID 만들기**:</span><span class="sxs-lookup"><span data-stu-id="a2599-128">Tap **What credentials do I need?** which takes you to the second step of app configuration, **Create an OAuth 2.0 client ID**:</span></span>

![API 관리자 자격 증명 페이지: OAuth 2.0 클라이언트 ID 만들기](index/_static/GoogleConsoleCreateClient.png)

* <span data-ttu-id="a2599-130">하나의 기능 (로그인)를 동일한 입력 수를 사용 하 여 Google + 프로젝트를 만드는 것 때문에 **이름을** 에서는 프로젝트에 대해 사용 되는 OAuth 2.0 클라이언트 ID에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-130">Because we are creating a Google+ project with just one feature (sign in), we can enter the same **Name** for the OAuth 2.0 client ID as the one we used for the project.</span></span>

* <span data-ttu-id="a2599-131">개발 URI를 입력으로 `/signin-google` 에 추가 합니다 **권한이 부여 된 리디렉션 Uri** 필드 (예를 들어: `https://localhost:44320/signin-google`).</span><span class="sxs-lookup"><span data-stu-id="a2599-131">Enter your development URI with `/signin-google` appended into the **Authorized redirect URIs** field (for example: `https://localhost:44320/signin-google`).</span></span> <span data-ttu-id="a2599-132">이 자습서의 뒷부분에서 구성 된 Google 인증에서 요청을 자동으로 처리 됩니다 `/signin-google` OAuth 흐름을 구현 하는 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-132">The Google authentication configured later in this tutorial will automatically handle requests at `/signin-google` route to implement the OAuth flow.</span></span>

> [!NOTE]
> <span data-ttu-id="a2599-133">URI 세그먼트 `/signin-google` Google 인증 공급자의 기본 콜백으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-133">The URI segment `/signin-google` is set as the default callback of the Google authentication provider.</span></span> <span data-ttu-id="a2599-134">상속을 통해 Google 인증 미들웨어를 구성 하는 동안 기본 콜백 URI를 변경할 수 있습니다 [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath) 의 속성을 [GoogleOptions](/dotnet/api/microsoft.aspnetcore.authentication.google.googleoptions) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-134">You can change the default callback URI while configuring the Google authentication middleware via the inherited [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath) property of the [GoogleOptions](/dotnet/api/microsoft.aspnetcore.authentication.google.googleoptions) class.</span></span>

* <span data-ttu-id="a2599-135">Tab 키를 추가 합니다 **권한이 부여 된 리디렉션 Uri** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-135">Press TAB to add the **Authorized redirect URIs** entry.</span></span>

* <span data-ttu-id="a2599-136">탭 **클라이언트 ID 만들기**, 세 번째 단계로, 그러면 **OAuth 2.0 동의 화면 설정**:</span><span class="sxs-lookup"><span data-stu-id="a2599-136">Tap **Create client ID**, which takes you to the third step, **Set up the OAuth 2.0 consent screen**:</span></span>

![API 관리자 자격 증명 페이지: OAuth 2.0 동의 화면 설정](index/_static/GoogleConsoleAddCred.png)

* <span data-ttu-id="a2599-138">입력에 공개 **전자 메일 주소** 하며 **제품 이름** Google + 라는 로그인 할 때 앱에 대 한 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-138">Enter your public facing **Email address** and the **Product name** shown for your app when Google+ prompts the user to sign in.</span></span> <span data-ttu-id="a2599-139">추가 옵션을 사용할 수 있습니다 **더 많은 사용자 지정 옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-139">Additional options are available under **More customization options**.</span></span>

* <span data-ttu-id="a2599-140">탭 **계속** 마지막 단계를 계속 하려면 **자격 증명 다운로드**:</span><span class="sxs-lookup"><span data-stu-id="a2599-140">Tap **Continue** to proceed to the last step, **Download credentials**:</span></span>

![API 관리자 자격 증명 페이지: 자격 증명 다운로드](index/_static/GoogleConsoleFinish.png)

* <span data-ttu-id="a2599-142">탭 **다운로드** 응용 프로그램 비밀을 사용 하 여 JSON 파일을 저장 하 고 **수행** 새 앱 만들기를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-142">Tap **Download** to save a JSON file with application secrets, and **Done** to complete creation of the new app.</span></span>

* <span data-ttu-id="a2599-143">다시 방문 해야 사이트를 배포 하는 경우는 **Google 콘솔** 새 공용 url을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-143">When deploying the site you'll need to revisit the **Google Console** and register a new public url.</span></span>

## <a name="store-google-clientid-and-clientsecret"></a><span data-ttu-id="a2599-144">저장소 Google ClientID 및 ClientSecret</span><span class="sxs-lookup"><span data-stu-id="a2599-144">Store Google ClientID and ClientSecret</span></span>

<span data-ttu-id="a2599-145">Google와 같은 중요 한 설정이 연결 `Client ID` 하 고 `Client Secret` 사용 하 여 응용 프로그램 구성에는 [암호 관리자](xref:security/app-secrets).</span><span class="sxs-lookup"><span data-stu-id="a2599-145">Link sensitive settings like Google `Client ID` and `Client Secret` to your application configuration using the [Secret Manager](xref:security/app-secrets).</span></span> <span data-ttu-id="a2599-146">이 자습서에서는 이름을 토큰 `Authentication:Google:ClientId` 고 `Authentication:Google:ClientSecret`입니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-146">For the purposes of this tutorial, name the tokens `Authentication:Google:ClientId` and `Authentication:Google:ClientSecret`.</span></span>

<span data-ttu-id="a2599-147">이러한 토큰에 대 한 값에서 이전 단계에서 다운로드 한 JSON 파일에서 찾을 수 있습니다 `web.client_id` 고 `web.client_secret`입니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-147">The values for these tokens can be found in the JSON file downloaded in the previous step under `web.client_id` and `web.client_secret`.</span></span>

## <a name="configure-google-authentication"></a><span data-ttu-id="a2599-148">Google 인증 구성</span><span class="sxs-lookup"><span data-stu-id="a2599-148">Configure Google Authentication</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="a2599-149">Google 서비스에 추가 합니다 `ConfigureServices` 의 메서드 *Startup.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="a2599-149">Add the Google service in the `ConfigureServices` method in *Startup.cs* file:</span></span>

```csharp
services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

services.AddAuthentication().AddGoogle(googleOptions =>
{
    googleOptions.ClientId = Configuration["Authentication:Google:ClientId"];
    googleOptions.ClientSecret = Configuration["Authentication:Google:ClientSecret"];
});
```

[!INCLUDE [default settings configuration](includes/default-settings.md)]

[!INCLUDE[](includes/chain-auth-providers.md)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="a2599-150">이 자습서에 사용 되는 프로젝트 템플릿이 되도록 [Microsoft.AspNetCore.Authentication.Google](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Google) 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-150">The project template used in this tutorial ensures that [Microsoft.AspNetCore.Authentication.Google](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Google) package is installed.</span></span>

* <span data-ttu-id="a2599-151">Visual Studio 2017을 사용 하 여이 패키지를 설치 하려면 마우스 오른쪽 단추로 클릭 프로젝트를 마우스 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-151">To install this package with Visual Studio 2017, right-click on the project and select **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="a2599-152">.NET Core CLI를 설치 하려면 프로젝트 디렉터리에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-152">To install with .NET Core CLI, execute the following in your project directory:</span></span>

`dotnet add package Microsoft.AspNetCore.Authentication.Google`

<span data-ttu-id="a2599-153">Google 미들웨어를 추가 합니다 `Configure` 의 메서드 *Startup.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="a2599-153">Add the Google middleware in the `Configure` method in *Startup.cs* file:</span></span>

```csharp
app.UseGoogleAuthentication(new GoogleOptions()
{
    ClientId = Configuration["Authentication:Google:ClientId"],
    ClientSecret = Configuration["Authentication:Google:ClientSecret"]
});
```

::: moniker-end

<span data-ttu-id="a2599-154">참조 된 [GoogleOptions](/dotnet/api/microsoft.aspnetcore.builder.googleoptions) Google 인증에서 지 원하는 구성 옵션에 대 한 자세한 내용은 API 참조.</span><span class="sxs-lookup"><span data-stu-id="a2599-154">See the [GoogleOptions](/dotnet/api/microsoft.aspnetcore.builder.googleoptions) API reference for more information on configuration options supported by Google authentication.</span></span> <span data-ttu-id="a2599-155">이 사용 하 여 사용자에 대 한 다른 정보를 요청할 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-155">This can be used to request different information about the user.</span></span>

## <a name="sign-in-with-google"></a><span data-ttu-id="a2599-156">Google로 로그인</span><span class="sxs-lookup"><span data-stu-id="a2599-156">Sign in with Google</span></span>

<span data-ttu-id="a2599-157">응용 프로그램을 실행 하 고 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-157">Run your application and click **Log in**.</span></span> <span data-ttu-id="a2599-158">Google로 로그인 하는 옵션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-158">An option to sign in with Google appears:</span></span>

![Microsoft Edge에서 실행 중인 웹 응용 프로그램: 인증 되지 않은 사용자](index/_static/DoneGoogle.png)

<span data-ttu-id="a2599-160">Google을 클릭할 때 리디렉션됩니다 Google 인증을 위해:</span><span class="sxs-lookup"><span data-stu-id="a2599-160">When you click on Google, you are redirected to Google for authentication:</span></span>

![Google 인증 대화 상자](index/_static/GoogleLogin.png)

<span data-ttu-id="a2599-162">Google 자격 증명을 입력 한 후 다음 리디렉션됩니다 전자 메일을 설정할 수 있는 웹 사이트로 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-162">After entering your Google credentials, then you are redirected back to the web site where you can set your email.</span></span>

<span data-ttu-id="a2599-163">이제 Google 자격 증명을 사용 하 여 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-163">You are now logged in using your Google credentials:</span></span>

![Microsoft Edge에서 실행 중인 웹 응용 프로그램: 인증 된 사용자](index/_static/Done.png)

[!INCLUDE[Forward request information when behind a proxy or load balancer section](includes/forwarded-headers-middleware.md)]

## <a name="troubleshooting"></a><span data-ttu-id="a2599-165">문제 해결</span><span class="sxs-lookup"><span data-stu-id="a2599-165">Troubleshooting</span></span>

* <span data-ttu-id="a2599-166">표시 되 면을 `403 (Forbidden)` 개발 모드 (또는 동일한 오류로 디버거로 중단)에서 실행 되도록 하는 경우 사용자 고유의 앱에서 오류 페이지 **Google + API** 에서 설정 되어 있는지를 **APIManager라이브러리** 나열 된 단계를 수행 하 여 [이 페이지에서 이전](#create-the-app-in-google-api-console)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-166">If you receive a `403 (Forbidden)` error page from your own app when running in development mode (or break into the debugger with the same error), ensure that **Google+ API** has been enabled in the **API Manager Library** by following the steps listed [earlier on this page](#create-the-app-in-google-api-console).</span></span> <span data-ttu-id="a2599-167">로그인 작동 하지 않습니다 하 고 오류를 가져오지 않음, 문제를 더 쉽게 디버그 하려면 개발 모드를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-167">If the sign in doesn't work and you aren't getting any errors, switch to development mode to make the issue easier to debug.</span></span>
* <span data-ttu-id="a2599-168">**ASP.NET Core 2.x만:** 호출 하 여 구성 되어 있지 않으면 Identity `services.AddIdentity` 에 `ConfigureServices`를 인증 하려고 하면 *ArgumentException: 'SignInScheme' 옵션을 제공 해야*합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-168">**ASP.NET Core 2.x only:** If Identity isn't configured by calling `services.AddIdentity` in `ConfigureServices`, attempting to authenticate will result in *ArgumentException: The 'SignInScheme' option must be provided*.</span></span> <span data-ttu-id="a2599-169">이 자습서에 사용 되는 프로젝트 템플릿이이 수행 되도록 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-169">The project template used in this tutorial ensures that this is done.</span></span>
* <span data-ttu-id="a2599-170">사이트 데이터베이스를 초기 마이그레이션을 적용 하 여 만들어지지 않은, 경우 받습니다 *요청을 처리 하는 동안 데이터베이스 작업이 실패 했습니다.* 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-170">If the site database has not been created by applying the initial migration, you will get *A database operation failed while processing the request* error.</span></span> <span data-ttu-id="a2599-171">탭 **마이그레이션 적용** 데이터베이스를 만들고 오류 지 나 새로 고침 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-171">Tap **Apply Migrations** to create the database and refresh to continue past the error.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2599-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a2599-172">Next steps</span></span>

* <span data-ttu-id="a2599-173">이 문서에서는 Google을 사용 하 여 인증 하는 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-173">This article showed how you can authenticate with Google.</span></span> <span data-ttu-id="a2599-174">에 나열 된 다른 공급자를 사용 하 여 인증 하는 유사한 방법을 따를 수 있습니다 합니다 [이전 페이지](xref:security/authentication/social/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-174">You can follow a similar approach to authenticate with other providers listed on the [previous page](xref:security/authentication/social/index).</span></span>

* <span data-ttu-id="a2599-175">다시 설정 해야 Azure 웹 앱에 웹 사이트를 게시 하면는 `ClientSecret` Google API 콘솔에서.</span><span class="sxs-lookup"><span data-stu-id="a2599-175">Once you publish your web site to Azure web app, you should reset the `ClientSecret` in the Google API Console.</span></span>

* <span data-ttu-id="a2599-176">설정 된 `Authentication:Google:ClientId` 및 `Authentication:Google:ClientSecret` Azure portal에서 응용 프로그램 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-176">Set the `Authentication:Google:ClientId` and `Authentication:Google:ClientSecret` as application settings in the Azure portal.</span></span> <span data-ttu-id="a2599-177">구성 시스템 환경 변수에서 키를 읽을 수 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2599-177">The configuration system is set up to read keys from environment variables.</span></span>
