---
title: ASP.NET Core에서 Facebook 외부 로그인 설정
author: rick-anderson
description: 이 자습서는 기존 ASP.NET Core 응용 프로그램에 Facebook 계정 사용자 인증의 통합을 보여 줍니다.
ms.author: riande
ms.date: 08/01/2017
uid: security/authentication/facebook-logins
ms.openlocfilehash: 53e5fa3ccee44451646c84e58260db23e59d6cbd
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36273401"
---
# <a name="facebook-external-login-setup-in-aspnet-core"></a><span data-ttu-id="f5ff4-103">ASP.NET Core에서 Facebook 외부 로그인 설정</span><span class="sxs-lookup"><span data-stu-id="f5ff4-103">Facebook external login setup in ASP.NET Core</span></span>

<span data-ttu-id="f5ff4-104">작성자: [Valeriy Novytskyy](https://github.com/01binary) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="f5ff4-104">By [Valeriy Novytskyy](https://github.com/01binary) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="f5ff4-105">이 자습서에서 만든 샘플 ASP.NET 코어 2.0 프로젝트를 사용 하 여 들이 Facebook 계정으로 로그인 할 사용자를 활성화 하는 방법을 보여 줍니다.는 [이전 페이지](xref:security/authentication/social/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-105">This tutorial shows you how to enable your users to sign in with their Facebook account using a sample ASP.NET Core 2.0 project created on the [previous page](xref:security/authentication/social/index).</span></span> <span data-ttu-id="f5ff4-106">Facebook 인증에 필요한는 [Microsoft.AspNetCore.Authentication.Facebook](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Facebook) NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-106">Facebook authentication requires the [Microsoft.AspNetCore.Authentication.Facebook](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Facebook) NuGet package.</span></span> <span data-ttu-id="f5ff4-107">Facebook 응용 프로그램 ID에 따라 만들어서 시작는 [공식 단계](https://developers.facebook.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-107">We start by creating a Facebook App ID by following the [official steps](https://developers.facebook.com).</span></span>

## <a name="create-the-app-in-facebook"></a><span data-ttu-id="f5ff4-108">Facebook에서 앱을 만들</span><span class="sxs-lookup"><span data-stu-id="f5ff4-108">Create the app in Facebook</span></span>

* <span data-ttu-id="f5ff4-109">로 이동는 [Facebook Developers 앱](https://developers.facebook.com/apps/) 페이지 하 고 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-109">Navigate to the [Facebook Developers app](https://developers.facebook.com/apps/) page and sign in.</span></span> <span data-ttu-id="f5ff4-110">Facebook 계정 없는 경우 사용 하 여는 **Facebook에 등록** 새로 만들려면 로그인 페이지에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-110">If you don't already have a Facebook account, use the **Sign up for Facebook** link on the login page to create one.</span></span>

* <span data-ttu-id="f5ff4-111">탭의 **새 앱 추가** 는 새 응용 프로그램 ID를 만들려면 오른쪽 위 모퉁이의 단추</span><span class="sxs-lookup"><span data-stu-id="f5ff4-111">Tap the **Add a New App** button in the upper right corner to create a new App ID.</span></span>

   ![Facebook 개발자 포털에 대 한 Microsoft Edge에서 열기](index/_static/FBMyApps.png)

* <span data-ttu-id="f5ff4-113">양식을 작성 하 고 탭는 **응용 프로그램 ID 만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-113">Fill out the form and tap the **Create App ID** button.</span></span>

   ![새 앱 ID 양식 만들기](index/_static/FBNewAppId.png)

* <span data-ttu-id="f5ff4-115">에 **제품 선택** 페이지에서 클릭 **Set Up** 에 **Facebook 로그인** 카드입니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-115">On the **Select a product** page, click **Set Up** on the **Facebook Login** card.</span></span>

   ![제품 설치 페이지](index/_static/FBProductSetup.png)

* <span data-ttu-id="f5ff4-117">**퀵 스타트** 마법사가 시작 됩니다 **플랫폼 선택** 의 첫 번째 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-117">The **Quickstart** wizard will launch with **Choose a Platform** as the first page.</span></span> <span data-ttu-id="f5ff4-118">마법사를 클릭 하 여 지금은 무시는 **설정을** 왼쪽 메뉴에서 링크:</span><span class="sxs-lookup"><span data-stu-id="f5ff4-118">Bypass the wizard for now by clicking the **Settings** link in the menu on the left:</span></span>

   ![Skip 빠른 시작](index/_static/FBSkipQuickStart.png)

* <span data-ttu-id="f5ff4-120">표시 되는 **클라이언트 OAuth 설정** 페이지:</span><span class="sxs-lookup"><span data-stu-id="f5ff4-120">You are presented with the **Client OAuth Settings** page:</span></span>

![클라이언트 OAuth 설정 페이지](index/_static/FBOAuthSetup.png)

* <span data-ttu-id="f5ff4-122">개발 URI를 입력으로 */signin-facebook* 에 추가 **유효한 OAuth 리디렉션 Uri** 필드 (예: `https://localhost:44320/signin-facebook`).</span><span class="sxs-lookup"><span data-stu-id="f5ff4-122">Enter your development URI with */signin-facebook* appended into the **Valid OAuth Redirect URIs** field (for example: `https://localhost:44320/signin-facebook`).</span></span> <span data-ttu-id="f5ff4-123">이 자습서의 뒷부분에 나오는 구성 된 Facebook 인증에는 요청을 자동으로 처리할 */signin-facebook* OAuth 흐름을 구현 하는 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-123">The Facebook authentication configured later in this tutorial will automatically handle requests at */signin-facebook* route to implement the OAuth flow.</span></span>

> [!NOTE]
> <span data-ttu-id="f5ff4-124">URI */signin-facebook* Facebook 인증 공급자의 기본 콜백으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-124">The URI */signin-facebook* is set as the default callback of the Facebook authentication provider.</span></span> <span data-ttu-id="f5ff4-125">상속 된 통해 Facebook 인증 미들웨어를 구성 하는 동안 기본 콜백 URI를 변경할 수 있습니다 [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath) 의 속성은 [FacebookOptions](/dotnet/api/microsoft.aspnetcore.authentication.facebook.facebookoptions) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-125">You can change the default callback URI while configuring the Facebook authentication middleware via the inherited [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath) property of the [FacebookOptions](/dotnet/api/microsoft.aspnetcore.authentication.facebook.facebookoptions) class.</span></span>

* <span data-ttu-id="f5ff4-126">클릭 **ब ा ळ**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-126">Click **Save Changes**.</span></span>

* <span data-ttu-id="f5ff4-127">클릭는 **대시보드** 왼쪽된 탐색 창에서 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-127">Click the **Dashboard** link in the left navigation.</span></span> 

    <span data-ttu-id="f5ff4-128">이 페이지에서 적어 프로그램 `App ID` 하였고 `App Secret`합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-128">On this page, make a note of your `App ID` and your `App Secret`.</span></span> <span data-ttu-id="f5ff4-129">다음 섹션에서 ASP.NET Core 응용 프로그램에 둘 다를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-129">You will add both into your ASP.NET Core application in the next section:</span></span>

   ![Facebook 개발자 대시보드](index/_static/FBDashboard.png)

* <span data-ttu-id="f5ff4-131">다시 방문 해야 하는 사이트를 배포 하는 경우는 **Facebook 로그인** 페이지를 설치 하 고 새 공용 URI를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-131">When deploying the site you need to revisit the **Facebook Login** setup page and register a new public URI.</span></span>

## <a name="store-facebook-app-id-and-app-secret"></a><span data-ttu-id="f5ff4-132">Facebook 응용 프로그램 ID 및 응용 프로그램 암호 저장</span><span class="sxs-lookup"><span data-stu-id="f5ff4-132">Store Facebook App ID and App Secret</span></span>

<span data-ttu-id="f5ff4-133">Facebook와 같은 중요 한 설정이 연결 `App ID` 및 `App Secret` 사용 하 여 응용 프로그램 구성에는 [암호 관리자](xref:security/app-secrets)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-133">Link sensitive settings like Facebook `App ID` and `App Secret` to your application configuration using the [Secret Manager](xref:security/app-secrets).</span></span> <span data-ttu-id="f5ff4-134">이 자습서에서는 이름을 토큰 `Authentication:Facebook:AppId` 및 `Authentication:Facebook:AppSecret`합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-134">For the purposes of this tutorial, name the tokens `Authentication:Facebook:AppId` and `Authentication:Facebook:AppSecret`.</span></span>

<span data-ttu-id="f5ff4-135">안전 하 게 저장 하려면 다음 명령을 실행 `App ID` 및 `App Secret` 암호 관리자를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f5ff4-135">Execute the following commands to securely store `App ID` and `App Secret` using Secret Manager:</span></span>

```console
dotnet user-secrets set Authentication:Facebook:AppId <app-id>
dotnet user-secrets set Authentication:Facebook:AppSecret <app-secret>
```

## <a name="configure-facebook-authentication"></a><span data-ttu-id="f5ff4-136">Facebook 인증 구성</span><span class="sxs-lookup"><span data-stu-id="f5ff4-136">Configure Facebook Authentication</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="f5ff4-137">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="f5ff4-137">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="f5ff4-138">Facebook 서비스에 추가 된 `ConfigureServices` 에서 메서드는 *Startup.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="f5ff4-138">Add the Facebook service in the `ConfigureServices` method in the *Startup.cs* file:</span></span>

```csharp
services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

services.AddAuthentication().AddFacebook(facebookOptions =>
{
    facebookOptions.AppId = Configuration["Authentication:Facebook:AppId"];
    facebookOptions.AppSecret = Configuration["Authentication:Facebook:AppSecret"];
});
```

[!INCLUDE [default settings configuration](includes/default-settings.md)]

[!INCLUDE[](~/includes/chain-auth-providers.md)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="f5ff4-139">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="f5ff4-139">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="f5ff4-140">설치는 [Microsoft.AspNetCore.Authentication.Facebook](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Facebook) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-140">Install the [Microsoft.AspNetCore.Authentication.Facebook](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Facebook) package.</span></span>

* <span data-ttu-id="f5ff4-141">Visual Studio 2017으로이 패키지를 설치 하려면 마우스 오른쪽 단추로 클릭 프로젝트와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-141">To install this package with Visual Studio 2017, right-click on the project and select **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="f5ff4-142">.NET Core CLI를 설치 하려면 다음 프로젝트 디렉터리에 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-142">To install with .NET Core CLI, execute the following in your project directory:</span></span>

   `dotnet add package Microsoft.AspNetCore.Authentication.Facebook`

<span data-ttu-id="f5ff4-143">Facebook 미들웨어에서 추가 된 `Configure` 에서 메서드 *Startup.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="f5ff4-143">Add the Facebook middleware in the `Configure` method in *Startup.cs* file:</span></span>

```csharp
app.UseFacebookAuthentication(new FacebookOptions()
{
    AppId = Configuration["Authentication:Facebook:AppId"],
    AppSecret = Configuration["Authentication:Facebook:AppSecret"]
});
```

---

<span data-ttu-id="f5ff4-144">참조는 [FacebookOptions](/dotnet/api/microsoft.aspnetcore.builder.facebookoptions) Facebook 인증에서 지 원하는 구성 옵션에 대 한 자세한 내용은 API 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-144">See the [FacebookOptions](/dotnet/api/microsoft.aspnetcore.builder.facebookoptions) API reference for more information on configuration options supported by Facebook authentication.</span></span> <span data-ttu-id="f5ff4-145">구성 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-145">Configuration options can be used to:</span></span>

* <span data-ttu-id="f5ff4-146">사용자에 대 한 다른 정보를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-146">Request different information about the user.</span></span>
* <span data-ttu-id="f5ff4-147">로그인 환경을 사용자 지정 하는 쿼리 문자열 인수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-147">Add query string arguments to customize the login experience.</span></span>

## <a name="sign-in-with-facebook"></a><span data-ttu-id="f5ff4-148">Facebook으로 로그인</span><span class="sxs-lookup"><span data-stu-id="f5ff4-148">Sign in with Facebook</span></span>

<span data-ttu-id="f5ff4-149">응용 프로그램을 실행 하 고 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-149">Run your application and click **Log in**.</span></span> <span data-ttu-id="f5ff4-150">Facebook으로 로그인 하는 옵션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-150">You see an option to sign in with Facebook.</span></span>

![웹 응용 프로그램: 인증 되지 않은 사용자](index/_static/DoneFacebook.png)

<span data-ttu-id="f5ff4-152">클릭 **Facebook**, 인증에 대 한 Facebook으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-152">When you click on **Facebook**, you are redirected to Facebook for authentication:</span></span>

![Facebook 인증 페이지](index/_static/FBLogin.png)

<span data-ttu-id="f5ff4-154">기본적으로 공개 프로필 및 전자 메일 주소를 요청 하는 Facebook 인증:</span><span class="sxs-lookup"><span data-stu-id="f5ff4-154">Facebook authentication requests public profile and email address by default:</span></span>

![Facebook 인증 페이지](index/_static/FBLoginDone.png)

<span data-ttu-id="f5ff4-156">Facebook 사용자의 자격 증명을 입력 하면 사용자의 전자 메일을 설정할 수 있는 사이트로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-156">Once you enter your Facebook credentials you are redirected back to your site where you can set your email.</span></span>

<span data-ttu-id="f5ff4-157">이제 Facebook 자격 증명을 사용 하 여 로그인:</span><span class="sxs-lookup"><span data-stu-id="f5ff4-157">You are now logged in using your Facebook credentials:</span></span>

![웹 응용 프로그램: 인증 된 사용자](index/_static/Done.png)

## <a name="troubleshooting"></a><span data-ttu-id="f5ff4-159">문제 해결</span><span class="sxs-lookup"><span data-stu-id="f5ff4-159">Troubleshooting</span></span>

* <span data-ttu-id="f5ff4-160">**ASP.NET Core 2.x만:** 경우 Identity를 호출 하 여 구성 되지 않았습니다 `services.AddIdentity` 에 `ConfigureServices`, 인증을 시도 하면 *ArgumentException: 'SignInScheme' 옵션을 제공 해야*합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-160">**ASP.NET Core 2.x only:** If Identity isn't configured by calling `services.AddIdentity` in `ConfigureServices`, attempting to authenticate will result in *ArgumentException: The 'SignInScheme' option must be provided*.</span></span> <span data-ttu-id="f5ff4-161">이 자습서에 사용 된 프로젝트 템플릿을 확인이 수행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-161">The project template used in this tutorial ensures that this is done.</span></span>
* <span data-ttu-id="f5ff4-162">사이트 데이터베이스 초기 마이그레이션을 적용 하 여 생성 되지 않은 경우 메시지가 *요청을 처리 하는 동안 데이터베이스 작업이 실패 했습니다* 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-162">If the site database has not been created by applying the initial migration, you get *A database operation failed while processing the request* error.</span></span> <span data-ttu-id="f5ff4-163">탭 **적용 마이그레이션** 는 데이터베이스를 만들고 오류 지 나 새로 고침 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-163">Tap **Apply Migrations** to create the database and refresh to continue past the error.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5ff4-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5ff4-164">Next steps</span></span>

* <span data-ttu-id="f5ff4-165">이 문서를 Facebook 인증 방법에 대해 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-165">This article showed how you can authenticate with Facebook.</span></span> <span data-ttu-id="f5ff4-166">이와 비슷한 방식에 제시 된 다른 공급자를 사용 하 여 인증을 따를 수 있습니다는 [이전 페이지](xref:security/authentication/social/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-166">You can follow a similar approach to authenticate with other providers listed on the [previous page](xref:security/authentication/social/index).</span></span>

* <span data-ttu-id="f5ff4-167">다시 설정 해야 Azure 웹 앱에 웹 사이트를 게시 한 후의 `AppSecret` Facebook 개발자 포털에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-167">Once you publish your web site to Azure web app, you should reset the `AppSecret` in the Facebook developer portal.</span></span>

* <span data-ttu-id="f5ff4-168">설정의 `Authentication:Facebook:AppId` 및 `Authentication:Facebook:AppSecret` Azure 포털에서 응용 프로그램 설정으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-168">Set the `Authentication:Facebook:AppId` and `Authentication:Facebook:AppSecret` as application settings in the Azure portal.</span></span> <span data-ttu-id="f5ff4-169">구성 시스템 환경 변수에서 키를 읽을 수 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5ff4-169">The configuration system is set up to read keys from environment variables.</span></span>
