---
title: "Facebook, Google 및 기타 외부 공급자를 통해 인증 사용"
author: rick-anderson
description: "이 자습서에는 외부 인증 공급자에 OAuth 2.0을 사용하여 ASP.NET Core 2.x 앱을 빌드하는 방법을 보여줍니다."
ms.author: riande
manager: wpickett
ms.date: 11/01/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authentication/social/index
ms.openlocfilehash: 7d03998c82bf13976ec6157acb5c56c28e5c0d52
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="enabling-authentication-using-facebook-google-and-other-external-providers"></a><span data-ttu-id="dcf4f-103">Facebook, Google 및 기타 외부 공급자를 통해 인증 사용</span><span class="sxs-lookup"><span data-stu-id="dcf4f-103">Enabling authentication using Facebook, Google, and other external providers</span></span>

<a name="security-authentication-social-logins"></a>

<span data-ttu-id="dcf4f-104">작성자: [Valeriy Novytskyy](https://github.com/01binary) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="dcf4f-104">By [Valeriy Novytskyy](https://github.com/01binary) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="dcf4f-105">이 자습서에는 사용자가 외부 인증 공급자의 자격 증명으로 OAuth 2.0을 사용하여 로그인할 수 있도록 ASP.NET Core 2.x 앱을 빌드하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-105">This tutorial demonstrates how to build an ASP.NET Core 2.x app that enables users to log in using OAuth 2.0 with credentials from external authentication providers.</span></span>

<span data-ttu-id="dcf4f-106">[Facebook](facebook-logins.md), [Twitter](twitter-logins.md), [Google](google-logins.md) 및 [Microsoft](microsoft-logins.md) 공급자는 다음 섹션에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-106">[Facebook](facebook-logins.md), [Twitter](twitter-logins.md), [Google](google-logins.md), and [Microsoft](microsoft-logins.md) providers are covered in the following sections.</span></span> <span data-ttu-id="dcf4f-107">다른 공급자는 [AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers) 및 [AspNet.Security.OpenId.Providers](https://github.com/aspnet-contrib/AspNet.Security.OpenId.Providers)와 같은 타사 패키지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-107">Other providers are available in third-party packages such as [AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers) and [AspNet.Security.OpenId.Providers](https://github.com/aspnet-contrib/AspNet.Security.OpenId.Providers).</span></span>

![Facebook, Twitter, Google Plus 및 Windows용 소셜 미디어 아이콘](index/_static/social.png)

<span data-ttu-id="dcf4f-109">사용자가 자신의 기존 자격 증명을 사용하여 로그인할 수 있게 되면 사용자에게 편리하고 로그인 프로세스를 관리하는 복잡성을 타사에 양도합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-109">Enabling users to sign in with their existing credentials is convenient for the users and shifts many of the complexities of managing the sign-in process onto a third party.</span></span> <span data-ttu-id="dcf4f-110">소셜 로그인이 트래픽 및 고객 변환을 제공할 수 있는 방법에 대한 예제는 [Facebook](https://www.facebook.com/unsupportedbrowser) 및 [Twitter](https://dev.twitter.com/resources/case-studies)의 사례 연구를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-110">For examples of how social logins can drive traffic and customer conversions, see case studies by [Facebook](https://www.facebook.com/unsupportedbrowser) and [Twitter](https://dev.twitter.com/resources/case-studies).</span></span>

<span data-ttu-id="dcf4f-111">참고: 여기에 제공된 패키지는 OAuth 인증 흐름의 복잡성을 상당히 추상화하지만 문제를 해결하는 경우 자세히 이해해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-111">Note: Packages presented here abstract a great deal of complexity of the OAuth authentication flow, but understanding the details may become necessary when troubleshooting.</span></span> <span data-ttu-id="dcf4f-112">많은 리소스를 사용할 수 있습니다. 예를 들어 [OAuth 2 소개](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2) 또는 [OAuth 2 이해](http://www.bubblecode.net/2016/01/22/understanding-oauth2/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-112">Many resources are available; for example, see [Introduction to OAuth 2](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2) or [Understanding OAuth 2](http://www.bubblecode.net/2016/01/22/understanding-oauth2/).</span></span> <span data-ttu-id="dcf4f-113">[공급자 패키지의 ASP.NET Core 소스 코드](https://github.com/aspnet/Security/tree/dev/src)를 확인하여 몇 가지 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-113">Some issues can be resolved by looking at the [ASP.NET Core source code for the provider packages](https://github.com/aspnet/Security/tree/dev/src).</span></span>

## <a name="create-a-new-aspnet-core-project"></a><span data-ttu-id="dcf4f-114">새 ASP.NET Core 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="dcf4f-114">Create a New ASP.NET Core Project</span></span>

* <span data-ttu-id="dcf4f-115">Visual Studio 2017의 시작 페이지에서 또는 **파일 > 새로 만들기 > 프로젝트**를 통해 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-115">In Visual Studio 2017, create a new project from the Start Page, or via **File > New > Project**.</span></span>

* <span data-ttu-id="dcf4f-116">**Visual C# >.NET Core** 범주에서 사용할 수 있는 **ASP.NET Core 웹 응용 프로그램** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-116">Select the **ASP.NET Core Web Application** template available in **Visual C# > .NET Core** category:</span></span>

![새 프로젝트 대화 상자](index/_static/new-project.png)

* <span data-ttu-id="dcf4f-118">**웹 응용 프로그램**을 누르고 **인증**이 **개별 사용자 계정**으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-118">Tap **Web Application** and verify **Authentication** is set to **Individual User Accounts**:</span></span>

![새 웹 응용 프로그램 대화 상자](index/_static/select-project.png)

<span data-ttu-id="dcf4f-120">참고: 이 자습서에서는 마법사의 위쪽에서 선택할 수 있는 ASP.NET Core 2.0 SDK 버전에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-120">Note: This tutorial applies to ASP.NET Core 2.0 SDK version which can be selected at the top of the wizard.</span></span>

## <a name="apply-migrations"></a><span data-ttu-id="dcf4f-121">마이그레이션 적용</span><span class="sxs-lookup"><span data-stu-id="dcf4f-121">Apply migrations</span></span>

* <span data-ttu-id="dcf4f-122">앱을 실행하고 **로그인** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-122">Run the app and select the **Log in** link.</span></span>
* <span data-ttu-id="dcf4f-123">**Register as a new user**(새 사용자로 등록) 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-123">Select the **Register as a new user** link.</span></span>
* <span data-ttu-id="dcf4f-124">새 계정의 메일과 암호를 입력한 다음 **등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-124">Enter the email and password for the new account, and then select **Register**.</span></span>
* <span data-ttu-id="dcf4f-125">지침에 따라 마이그레이션을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-125">Follow the instructions to apply migrations.</span></span>

## <a name="require-ssl"></a><span data-ttu-id="dcf4f-126">SSL 필요</span><span class="sxs-lookup"><span data-stu-id="dcf4f-126">Require SSL</span></span>

<span data-ttu-id="dcf4f-127">OAuth 2.0은 HTTPS 프로토콜을 통한 인증을 위해 SSL을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-127">OAuth 2.0 requires the use of SSL for authentication over the HTTPS protocol.</span></span>

<span data-ttu-id="dcf4f-128">참고: 위에 표시된 대로 프로젝트 마법사의 **인증 변경 대화**에서 **개별 사용자 계정** 옵션을 선택한 경우 ASP.NET Core 2.x에 대한 **웹 응용 프로그램** 또는 **Web API** 프로젝트 템플릿를 사용하여 만든 프로젝트는 자동으로 SSL을 사용하고 https URL으로 시작하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-128">Note: Projects created using **Web Application** or **Web API** project templates for ASP.NET Core 2.x are automatically configured to enable SSL and launch with https URL if the **Individual User Accounts** option was selected on **Change Authentication dialog** in the project wizard as shown above.</span></span>

* <span data-ttu-id="dcf4f-129">[ASP.NET Core 앱에서 SSL 적용](xref:security/enforcing-ssl) 항목의 단계를 수행하여 사이트에서 SSL을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-129">Require SSL on your site by following the steps in [Enforcing SSL in an ASP.NET Core app](xref:security/enforcing-ssl) topic.</span></span>

## <a name="use-secretmanager-to-store-tokens-assigned-by-login-providers"></a><span data-ttu-id="dcf4f-130">SecretManager를 사용하여 로그인 공급자에 의해 할당된 토큰 저장</span><span class="sxs-lookup"><span data-stu-id="dcf4f-130">Use SecretManager to store tokens assigned by login providers</span></span>

<span data-ttu-id="dcf4f-131">소셜 로그인 공급자는 등록 프로세스 중에 **응용 프로그램 ID** 및 **응용 프로그램 암호** 토큰을 할당합니다(공급자에 따라 정확한 이름이 다름).</span><span class="sxs-lookup"><span data-stu-id="dcf4f-131">Social login providers assign **Application Id** and **Application Secret** tokens during the registration process (exact naming varies by provider).</span></span>

<span data-ttu-id="dcf4f-132">이러한 값은 해당 API에 액세스하기 위해 응용 프로그램이 사용하는 *사용자 이름* 및 *암호*를 효과적으로 지정하고 직접 구성 파일에 저장하거나 하드 코딩하는 대신 **암호 관리자**를 사용하여 응용 프로그램 구성에 연결될 수 있는 "비밀"을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-132">These values are effectively the *user name* and *password* your application uses to access their API, and constitute the "secrets" that can be linked to your application configuration with the help of **Secret Manager** instead of storing them in configuration files directly or hard-coding them.</span></span>

<span data-ttu-id="dcf4f-133">[ASP.NET Core에서 개발 중에 앱 암호의 안전한 저장소](xref:security/app-secrets) 항목의 단계에 따라 아래의 각 로그인 공급자에 의해 할당된 토큰을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-133">Follow the steps in [Safe storage of app secrets during development in ASP.NET Core](xref:security/app-secrets) topic so that you can store tokens assigned by each login provider below.</span></span>

## <a name="setup-login-providers-required-by-your-application"></a><span data-ttu-id="dcf4f-134">응용 프로그램에 필요한 로그인 공급자 설정</span><span class="sxs-lookup"><span data-stu-id="dcf4f-134">Setup login providers required by your application</span></span>

<span data-ttu-id="dcf4f-135">다음 항목을 사용하여 해당 공급자를 사용하도록 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-135">Use the following topics to configure your application to use the respective providers:</span></span>

* <span data-ttu-id="dcf4f-136">[Facebook](facebook-logins.md) 지침</span><span class="sxs-lookup"><span data-stu-id="dcf4f-136">[Facebook](facebook-logins.md) instructions</span></span>
* <span data-ttu-id="dcf4f-137">[Twitter](twitter-logins.md) 지침</span><span class="sxs-lookup"><span data-stu-id="dcf4f-137">[Twitter](twitter-logins.md) instructions</span></span>
* <span data-ttu-id="dcf4f-138">[Google](google-logins.md) 지침</span><span class="sxs-lookup"><span data-stu-id="dcf4f-138">[Google](google-logins.md) instructions</span></span>
* <span data-ttu-id="dcf4f-139">[Microsoft](microsoft-logins.md) 지침</span><span class="sxs-lookup"><span data-stu-id="dcf4f-139">[Microsoft](microsoft-logins.md) instructions</span></span>
* <span data-ttu-id="dcf4f-140">[다른 공급자](other-logins.md) 지침</span><span class="sxs-lookup"><span data-stu-id="dcf4f-140">[Other provider](other-logins.md) instructions</span></span>

## <a name="optionally-set-password"></a><span data-ttu-id="dcf4f-141">필요에 따라 암호 설정</span><span class="sxs-lookup"><span data-stu-id="dcf4f-141">Optionally set password</span></span>

<span data-ttu-id="dcf4f-142">외부 로그인 공급자를 등록하는 경우 앱에 암호를 등록하지 않은 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-142">When you register with an external login provider, you do not have a password registered with the app.</span></span> <span data-ttu-id="dcf4f-143">그러면 사이트에 암호를 만들고 기억하지 않아도 되지만 외부 로그인 공급자에 따라 다르게 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-143">This alleviates you from creating and remembering a password for the site, but it also makes you dependent on the external login provider.</span></span> <span data-ttu-id="dcf4f-144">외부 로그인 공급자를 사용할 수 없는 경우 웹 사이트에 로그인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-144">If the external login provider is unavailable, you won't be able to log in to the web site.</span></span>

<span data-ttu-id="dcf4f-145">외부 공급자로 로그인하는 프로세스 중에 설정한 전자 메일을 사용하여 암호를 만들고 로그인하려면:</span><span class="sxs-lookup"><span data-stu-id="dcf4f-145">To create a password and sign in using your email that you set during the sign in process with external providers:</span></span>

* <span data-ttu-id="dcf4f-146">오른쪽 위 모서리에 있는 **Hello<email alias>** 링크를 눌러 **관리** 뷰로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-146">Tap the **Hello <email alias>** link at the top right corner to navigate to the **Manage** view.</span></span>

![웹 응용 프로그램 관리 뷰](index/_static/pass1a.png)

* <span data-ttu-id="dcf4f-148">**만들기** 탭</span><span class="sxs-lookup"><span data-stu-id="dcf4f-148">Tap **Create**</span></span>

![암호 페이지 설정](index/_static/pass2a.png)

* <span data-ttu-id="dcf4f-150">올바른 암호를 설정하고 사용자의 전자 메일을 사용하여 로그인하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-150">Set a valid password and you can use this to sign in with your email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcf4f-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dcf4f-151">Next steps</span></span>

* <span data-ttu-id="dcf4f-152">이 문서는 외부 인증을 고새하고 ASP.NET Core 앱에 외부 로그인을 추가하는 데 필요한 필수 구성 요소를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-152">This article introduced external authentication and explained the prerequisites required to add external logins to your ASP.NET Core app.</span></span>

* <span data-ttu-id="dcf4f-153">앱에 필요한 공급자에 대한 로그인을 구성하기 위해 공급자 관련 페이지를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4f-153">Reference provider-specific pages to configure logins for the providers required by your app.</span></span>
