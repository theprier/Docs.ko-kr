---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: MVC 4와 함께 OAuth 공급자 사용 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Facebo 같은 외부 공급자가 자격 증명으로 로그인 할 수 있는 ASP.NET MVC 4 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다...
ms.author: riande
ms.date: 06/19/2013
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: d0203b62c911056fc56ed103c1c42f67816cbbf0
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021757"
---
<a name="using-oauth-providers-with-mvc-4"></a><span data-ttu-id="64689-103">MVC 4와 함께 OAuth 공급자 사용</span><span class="sxs-lookup"><span data-stu-id="64689-103">Using OAuth Providers with MVC 4</span></span>
====================
<span data-ttu-id="64689-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="64689-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="64689-105">이 자습서에서는 사용자가 외부 공급자, Facebook, Twitter, Microsoft, Google 등의 자격 증명으로 로그인 하 고 다음에 해당 공급자의 기능 중 일부를 통합할 수 있는 ASP.NET MVC 4 웹 응용 프로그램을 빌드하는 방법에 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="64689-105">This tutorial shows you how to build an ASP.NET MVC 4 web application that enables users to log in with credentials from an external provider, such as Facebook, Twitter, Microsoft, or Google, and then integrate some of the functionality from those providers into your web application.</span></span> <span data-ttu-id="64689-106">간단히 하기 위해이 자습서에서 Facebook 자격 증명을 사용 하 여 작업에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="64689-106">For simplicity, this tutorial focuses on working with credentials from Facebook.</span></span>
> 
> <span data-ttu-id="64689-107">ASP.NET MVC 5 웹 응용 프로그램에서 외부 자격 증명을 사용 하려면 참조 [Facebook 및 Google OAuth2 및 OpenID Sign on을 사용 하 여 ASP.NET MVC 5 앱 만들기](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-107">To use external credentials in an ASP.NET MVC 5 web application, see [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
> 
> <span data-ttu-id="64689-108">수백만 명의 사용자는 이러한 외부 공급자를 사용 하 여 계정을 이미 있기 때문에 중요 한 장점을 제공 웹 사이트에서 이러한 자격 증명을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-108">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="64689-109">이러한 사용자를 만들고 새 자격 증명 집합을 기억 없는 경우 사이트에 대 한 등록 싶다는 더욱 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-109">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span> <span data-ttu-id="64689-110">또한 사용자가 이러한 공급자 중 하나를 통해 로그인 한 후 공급자에서 소셜 작업을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-110">Also, after a user has logged in through one of these providers, you can incorporate social operations from the provider.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="64689-111">만들 내용</span><span class="sxs-lookup"><span data-stu-id="64689-111">What you'll build</span></span>

<span data-ttu-id="64689-112">이 자습서에서는 두 가지 주요 목표는</span><span class="sxs-lookup"><span data-stu-id="64689-112">There are two main goals in this tutorial:</span></span>

1. <span data-ttu-id="64689-113">OAuth 공급자에서 자격 증명으로 로그인 할 사용자를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-113">Enable a user to log in with credentials from an OAuth provider.</span></span>
2. <span data-ttu-id="64689-114">공급자에서 계정 정보를 검색 하 고 사이트에 대 한 계정 등록을 사용 하 여 해당 정보를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-114">Retrieve account information from the provider and integrate that information with the account registration for your site.</span></span>

<span data-ttu-id="64689-115">이 자습서의 예제에서 Facebook 인증 공급자로 사용 하 여에 집중 하지만 공급자 중 하나를 사용 하는 코드를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-115">Although the examples in this tutorial focus on using Facebook as the authentication provider, you can modify the code to use any of the providers.</span></span> <span data-ttu-id="64689-116">모든 공급자를 구현 하는 단계는이 자습서에서 단계와 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-116">The steps to implement any provider are very similar to the steps you will see in this tutorial.</span></span> <span data-ttu-id="64689-117">만 중요 한 차이점은 공급자의 API 직접 호출 시 설정으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="64689-117">You will only notice significant differences when making direct calls to the provider's API set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64689-118">전제 조건</span><span class="sxs-lookup"><span data-stu-id="64689-118">Prerequisites</span></span>

- <span data-ttu-id="64689-119">[Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) 또는 [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span><span class="sxs-lookup"><span data-stu-id="64689-119">[Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) or [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span></span>

<span data-ttu-id="64689-120">또는</span><span class="sxs-lookup"><span data-stu-id="64689-120">Or</span></span>

- <span data-ttu-id="64689-121">Microsoft Visual Studio 2010 SP1 또는 [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span><span class="sxs-lookup"><span data-stu-id="64689-121">Microsoft Visual Studio 2010 SP1 or [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span></span>
- [<span data-ttu-id="64689-122">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="64689-122">ASP.NET MVC 4</span></span>](https://go.microsoft.com/fwlink/?LinkId=243392)

<span data-ttu-id="64689-123">또한이 항목에서는 ASP.NET MVC 및 Visual Studio에 대 한 기본 지식이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-123">Furthermore, this topic assumes you have basic knowledge about ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="64689-124">ASP.NET MVC 4 소개를 참조 하세요 [ASP.NET MVC 4 소개](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-124">If you need an introduction to ASP.NET MVC 4, see [Intro to ASP.NET MVC 4](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md).</span></span>

## <a name="create-the-project"></a><span data-ttu-id="64689-125">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64689-125">Create the project</span></span>

<span data-ttu-id="64689-126">Visual Studio에는 새 ASP.NET MVC 4 웹 응용 프로그램을 만들고 이름을 &quot;OAuthMVC&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-126">In Visual Studio, create a new ASP.NET MVC 4 Web Application, and name it &quot;OAuthMVC&quot;.</span></span> <span data-ttu-id="64689-127">.NET Framework 4.5 또는 4를 대상 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-127">You can target either .NET Framework 4.5 or 4.</span></span>

![프로젝트 만들기](using-oauth-providers-with-mvc/_static/image1.png)

<span data-ttu-id="64689-129">새 ASP.NET MVC 4 프로젝트 창에서 선택 **인터넷 응용 프로그램** 두고 **Razor** 를 뷰 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="64689-129">In the New ASP.NET MVC 4 Project window, select **Internet Application** and leave **Razor** as the view engine.</span></span>

![인터넷 응용 프로그램 선택](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a><span data-ttu-id="64689-131">공급자를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="64689-131">Enable a provider</span></span>

<span data-ttu-id="64689-132">앱에서 AuthConfig.cs 라는 파일을 사용 하 여 프로젝트가 생성 되는 인터넷 응용 프로그램 템플릿을 사용 하 여 MVC 4 웹 응용 프로그램을 만들 때\_시작 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="64689-132">When you create an MVC 4 web application with the Internet Application template, the project is created with a file named AuthConfig.cs in the App\_Start folder.</span></span>

![AuthConfig 파일](using-oauth-providers-with-mvc/_static/image3.png)

<span data-ttu-id="64689-134">AuthConfig 파일은 외부 인증 공급자에 대 한 클라이언트를 등록 하는 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-134">The AuthConfig file contains code to register clients for external authentication providers.</span></span> <span data-ttu-id="64689-135">기본적으로이 코드는 주석에서 어떤 외부 공급자를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-135">By default, this code is commented out, so none of the external providers are enabled.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

<span data-ttu-id="64689-136">외부 인증 클라이언트를 사용 하도록이 코드 주석 처리를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-136">You must uncomment this code to use the external authentication client.</span></span> <span data-ttu-id="64689-137">사이트에서 포함 하려는 공급자만 주석 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-137">You uncomment only the providers you want to include in your site.</span></span> <span data-ttu-id="64689-138">이 자습서에서는 Facebook 자격 증명을 사용할가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-138">For this tutorial, you will only enable the Facebook credentials.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

<span data-ttu-id="64689-139">메서드는 등록 매개 변수에 대 한 빈 문자열에 위의 예제에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-139">Notice in the above example that the method includes empty strings for the registration parameters.</span></span> <span data-ttu-id="64689-140">이제 응용 프로그램을 실행 하려고 하면 응용 프로그램 매개 변수에 대해 빈 문자열이 없으므로 인수 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-140">If you try to run the application now, the application throws an argument exception because empty strings are not allowed for the parameters.</span></span> <span data-ttu-id="64689-141">유효한 값을 제공 하려면 다음 섹션에 나와 있는 것 처럼 외부 공급자를 사용 하 여 웹 사이트 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-141">To provide valid values, you must register your web site with the external providers, as shown in the next section.</span></span>

## <a name="registering-with-an-external-provider"></a><span data-ttu-id="64689-142">외부 공급자를 사용 하 여 등록</span><span class="sxs-lookup"><span data-stu-id="64689-142">Registering with an external provider</span></span>

<span data-ttu-id="64689-143">외부 공급자의 자격 증명을 사용 하 여 사용자를 인증 하려면 공급자를 사용 하 여 웹 사이트를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-143">To authenticate users with credentials from an external provider, you must register your web site with the provider.</span></span> <span data-ttu-id="64689-144">사이트를 등록 하면을 받게 됩니다 (예: 키 또는 id 및 암호) 매개 변수를 클라이언트를 등록 하는 경우를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-144">When you register your site, you will receive the parameters (such as key or id, and secret) to include when registering the client.</span></span> <span data-ttu-id="64689-145">계정을 사용 하려면 공급자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-145">You must have an account with the providers you wish to use.</span></span>

<span data-ttu-id="64689-146">이 자습서에서는 이러한 공급자를 등록 하기 위해 필요한 단계를 모두 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-146">This tutorial does not show all of the steps you must perform to register with these providers.</span></span> <span data-ttu-id="64689-147">단계는 일반적으로 어렵습니다 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-147">The steps are typically not difficult.</span></span> <span data-ttu-id="64689-148">사이트를 성공적으로 등록 하려면 해당 사이트에 제공 된 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="64689-148">To successfully register your site, follow the instructions provided on those sites.</span></span> <span data-ttu-id="64689-149">등록 사이트 사용을 시작 하는 개발자 사이트를 참조:</span><span class="sxs-lookup"><span data-stu-id="64689-149">To get started with registering your site, see the developer site for:</span></span>

- [<span data-ttu-id="64689-150">Facebook</span><span class="sxs-lookup"><span data-stu-id="64689-150">Facebook</span></span>](https://developers.facebook.com/)
- [<span data-ttu-id="64689-151">Google</span><span class="sxs-lookup"><span data-stu-id="64689-151">Google</span></span>](https://developers.google.com/)
- [<span data-ttu-id="64689-152">Microsoft</span><span class="sxs-lookup"><span data-stu-id="64689-152">Microsoft</span></span>](http://manage.dev.live.com/)
- [<span data-ttu-id="64689-153">Twitter</span><span class="sxs-lookup"><span data-stu-id="64689-153">Twitter</span></span>](https://dev.twitter.com/)

<span data-ttu-id="64689-154">Facebook을 사용 하 여 사이트를 등록할 때 제공할 수 있습니다 &quot;localhost&quot; 사이트 도메인 및 `&quot; http://localhost/&quot;` 아래 이미지에 표시 된 것과 같이 URL에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-154">When registering your site with Facebook, you can provide &quot;localhost&quot; for the site domain and `&quot;http://localhost/&quot;` for the URL, as shown in the image below.</span></span> <span data-ttu-id="64689-155">Localhost를 사용 하 여 대부분의 공급자를 사용 하 여 작동 하지만 현재 Microsoft 공급자와 함께 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-155">Using localhost works with most providers, but currently does not work with the Microsoft provider.</span></span> <span data-ttu-id="64689-156">Microsoft 공급자에 대 한 유효한 웹 사이트 URL을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-156">For the Microsoft provider, you must include a valid web site URL.</span></span>

![사이트를 등록 합니다.](using-oauth-providers-with-mvc/_static/image4.png)

<span data-ttu-id="64689-158">이전 이미지에서 앱 id, 앱 암호 및 연락처 전자 메일에 대 한 값을 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-158">In the previous image, the values for the app id, app secret, and contact email have been removed.</span></span> <span data-ttu-id="64689-159">실제로 사이트를 등록 하면 해당 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64689-159">When you actually register your site, those values will be present.</span></span> <span data-ttu-id="64689-160">응용 프로그램에 추가할 것 이므로 앱 id 및 앱 암호에 대 한 값을 확인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-160">You will want to note the values for app id and app secret because you will add them to your application.</span></span>

## <a name="creating-test-users"></a><span data-ttu-id="64689-161">테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="64689-161">Creating test users</span></span>

<span data-ttu-id="64689-162">사이트를 테스트 하도록 기존 Facebook 계정을 사용 하 여를 고려해 하지 않습니다, 경우에이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-162">If you do not mind using an existing Facebook account to test your site, you can skip this section.</span></span>

<span data-ttu-id="64689-163">Facebook 앱 관리 페이지 내에서 응용 프로그램에 대 한 테스트 사용자를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-163">You can easily create test users for your application within the Facebook app management page.</span></span> <span data-ttu-id="64689-164">사용할 수 있습니다 사이트에 로그인 할 계정을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-164">You can use these test accounts to log in to your site.</span></span> <span data-ttu-id="64689-165">클릭 하 여 테스트 사용자를 만듭니다는 **역할** 링크를 클릭 하 고 왼쪽된 탐색 창에는 **만들기** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-165">You create test users by clicking the **Roles** link in the left navigation pane and the clicking the **Create** link.</span></span>

![테스트 사용자 만들기](using-oauth-providers-with-mvc/_static/image5.png)

<span data-ttu-id="64689-167">Facebook 사이트를 요청 하는 테스트 계정 수를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64689-167">The Facebook site automatically creates the number of test accounts that you request.</span></span>

## <a name="adding-application-id-and-secret-from-the-provider"></a><span data-ttu-id="64689-168">공급자에서 응용 프로그램 id 및 암호 추가</span><span class="sxs-lookup"><span data-stu-id="64689-168">Adding application id and secret from the provider</span></span>

<span data-ttu-id="64689-169">Facebook에서 id 및 암호를 수신 했으므로 AuthConfig 파일로 돌아가서 매개 변수 값으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-169">Now that you have received the id and secret from Facebook, go back to the AuthConfig file and add them as the parameter values.</span></span> <span data-ttu-id="64689-170">아래 표시 된 값은 실제 값이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-170">The values shown below are not real values.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a><span data-ttu-id="64689-171">외부 자격 증명으로 로그인</span><span class="sxs-lookup"><span data-stu-id="64689-171">Log in with external credentials</span></span>

<span data-ttu-id="64689-172">사이트의 외부 자격 증명을 사용 하도록 설정 하기 위해 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-172">That is all you have to do to enable external credentials in your site.</span></span> <span data-ttu-id="64689-173">응용 프로그램을 실행 하 고 오른쪽 위 모서리의 로그인 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-173">Run your application and click the login link in the upper right corner.</span></span> <span data-ttu-id="64689-174">템플릿을 공급자로 Facebook을 등록 한 공급자의 단추를 포함 하에 자동으로 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-174">The template automatically recognizes that you have registered Facebook as a provider and includes a button for the provider.</span></span> <span data-ttu-id="64689-175">여러 공급자를 등록 하는 경우 각각에 대 한 단추를 자동으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64689-175">If you register multiple providers, a button for each one is automatically included.</span></span>

![외부 로그인](using-oauth-providers-with-mvc/_static/image6.png)

<span data-ttu-id="64689-177">이 자습서 외부 공급자에 대 한 로그인 단추를 사용자 지정 하는 방법을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-177">This tutorial does not cover how to customize the log in buttons for the external providers.</span></span> <span data-ttu-id="64689-178">해당 정보를 참조 하세요 [OAuth/OpenID를 사용 하는 경우에 로그인 UI를 사용자 지정](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-178">For that information, see [Customizing the login UI when using OAuth/OpenID](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx).</span></span>

<span data-ttu-id="64689-179">Facebook 자격 증명으로 로그인 하려면 Facebook 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-179">Click on the Facebook button to log in with Facebook credentials.</span></span> <span data-ttu-id="64689-180">외부 공급자 중 하나를 선택 하면 해당 사이트에 리디렉션 되며 해당 서비스에 로그인 하 라는 메시지가 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-180">When you select one of the external providers, you are redirected to that site and prompted by that service to log in.</span></span>

<span data-ttu-id="64689-181">다음 이미지는 facebook 로그인 화면을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="64689-181">The following image shows the login screen for Facebook.</span></span> <span data-ttu-id="64689-182">이 정보 oauthmvcexample 이라는 사이트에 로그인 하려면 Facebook 계정을 사용 한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-182">It notes that you are using your Facebook account to log in to a site named oauthmvcexample.</span></span>

![facebook 인증](using-oauth-providers-with-mvc/_static/image7.png)

<span data-ttu-id="64689-184">Facebook 자격 증명으로 로그인 한 후 페이지를 사용자 사이트 기본 정보에 액세스할 수 있는지 알립니다.</span><span class="sxs-lookup"><span data-stu-id="64689-184">After logging in with Facebook credentials, a page informs the user that the site will have access to basic information.</span></span>

![권한을 요청](using-oauth-providers-with-mvc/_static/image8.png)

<span data-ttu-id="64689-186">선택한 후 **앱으로 이동**, 사용자는 사이트에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-186">After selecting **Go to App**, the user must register for the site.</span></span> <span data-ttu-id="64689-187">다음 이미지는 사용자가 Facebook 자격 증명을 사용 하 여 로그온 한 후 등록 페이지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="64689-187">The following image shows the registration page after a user has logged in with Facebook credentials.</span></span> <span data-ttu-id="64689-188">사용자 이름은 일반적으로 공급자의 이름으로 미리 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="64689-188">The user name is typically pre-filled with a name from the provider.</span></span>

![register](using-oauth-providers-with-mvc/_static/image9.png)

<span data-ttu-id="64689-190">클릭 **등록** 등록을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-190">Click **Register** to complete registration.</span></span> <span data-ttu-id="64689-191">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-191">Close the browser.</span></span>

<span data-ttu-id="64689-192">새 계정 데이터베이스에 추가한는 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-192">You can see that the new account has been added to your database.</span></span> <span data-ttu-id="64689-193">서버 탐색기에서 엽니다는 **DefaultConnection** 연 데이터베이스 합니다 **테이블** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="64689-193">In Server Explorer, open the **DefaultConnection** database and open the **Tables** folder.</span></span>

![데이터베이스 테이블](using-oauth-providers-with-mvc/_static/image10.png)

<span data-ttu-id="64689-195">마우스 오른쪽 단추로 클릭 합니다 **UserProfile** 선택한 테이블 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-195">Right-click the **UserProfile** table and select **Show Table Data**.</span></span>

![데이터를 표시 합니다.](using-oauth-providers-with-mvc/_static/image11.png)

<span data-ttu-id="64689-197">추가한 새 계정이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64689-197">You will see the new account you added.</span></span> <span data-ttu-id="64689-198">데이터를 살펴봅니다 **웹 페이지\_OAuthMembership** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="64689-198">Look at the data in **webpage\_OAuthMembership** table.</span></span> <span data-ttu-id="64689-199">방금 추가한 계정에 대 한 외부 공급자와 관련 된 자세한 데이터를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64689-199">You will see more data related to the external provider for the account you just added.</span></span>

<span data-ttu-id="64689-200">외부 인증을 사용 하도록 설정 하려는 경우 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64689-200">If you only want to enable external authentication, you are done.</span></span> <span data-ttu-id="64689-201">다음 섹션에 표시 된 대로 새 사용자 등록 프로세스에 공급자의에서 정보를, 통합할 더 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-201">However, you can further integrate information from the provider into the new user registration process, as shown in the following sections.</span></span>

## <a name="create-models-for-additional-user-information"></a><span data-ttu-id="64689-202">추가 사용자 정보에 대 한 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="64689-202">Create models for additional user information</span></span>

<span data-ttu-id="64689-203">이전 섹션에서 설명한 것 처럼 작동 하도록 기본 제공 계정 등록에 대 한 추가 정보를 검색할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-203">As you noticed in the previous sections, you do not need to retrieve any additional information for the built-in account registration to work.</span></span> <span data-ttu-id="64689-204">그러나 대부분의 외부 공급자를 사용자에 대 한 다시 추가 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-204">However, most external providers pass back additional information about the user.</span></span> <span data-ttu-id="64689-205">다음 섹션에서는 해당 정보를 유지 하 고 데이터베이스에 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="64689-205">The following sections show how to retain that information and save it to a database.</span></span> <span data-ttu-id="64689-206">특히, 사용자의 전체 이름, 사용자의 개인 웹 페이지의 URI에 대 한 값 및 Facebook 계정을 확인 여부를 나타내는 값을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-206">Specifically, you will retain values for the user's full name, the URI of the user's personal web page, and a value that indicates whether Facebook has verified the account.</span></span>

<span data-ttu-id="64689-207">사용할지 [Code First 마이그레이션을](https://msdn.microsoft.com/data/jj591621) 추가 사용자 정보를 저장 하는 것에 대 한 테이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-207">You will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) to add a table for storing additional user information.</span></span> <span data-ttu-id="64689-208">현재 데이터베이스의 스냅숏을 만들려면 먼저 해야 하므로 기존 데이터베이스에 테이블을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64689-208">You are adding the table to an existing database, so you will first need to create a snapshot of the current database.</span></span> <span data-ttu-id="64689-209">현재 데이터베이스의 스냅숏을 만들어 나중에 새 테이블을 포함 하는 마이그레이션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-209">By creating a snapshot of the current database, you can later create a migration that contains only the new table.</span></span> <span data-ttu-id="64689-210">현재 데이터베이스의 스냅숏을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="64689-210">To create a snapshot of the current database:</span></span>

1. <span data-ttu-id="64689-211">열기는 **패키지 관리자 콘솔**</span><span class="sxs-lookup"><span data-stu-id="64689-211">Open the **Package Manager Console**</span></span>
2. <span data-ttu-id="64689-212">명령을 실행 하 여 **마이그레이션을 사용 하도록 설정**</span><span class="sxs-lookup"><span data-stu-id="64689-212">Run the command **enable-migrations**</span></span>
3. <span data-ttu-id="64689-213">명령을 실행 하 여 **IgnoreChanges 추가 마이그레이션 초기 –**</span><span class="sxs-lookup"><span data-stu-id="64689-213">Run the command **add-migration initial –IgnoreChanges**</span></span>
4. <span data-ttu-id="64689-214">명령을 실행 하 여 **데이터베이스 업데이트**</span><span class="sxs-lookup"><span data-stu-id="64689-214">Run the command **update-database**</span></span>

<span data-ttu-id="64689-215">이제 새 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-215">Now, you will add the new properties.</span></span> <span data-ttu-id="64689-216">Models 폴더에서 AccountModels.cs 파일을 열고 하 고 RegisterExternalLoginModel 클래스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-216">In the Models folder, open the AccountModels.cs file, and find the RegisterExternalLoginModel class.</span></span> <span data-ttu-id="64689-217">RegisterExternalLoginModel 클래스는 인증 공급자에서 반환 되는 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-217">The RegisterExternalLoginModel class holds values that come back from the authentication provider.</span></span> <span data-ttu-id="64689-218">FullName 및 링크를 아래 강조 표시 된 대로 라는 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-218">Add properties named FullName and Link, as highlighted below.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

<span data-ttu-id="64689-219">또한 AccountModels.cs, ExtraUserInformation 라는 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-219">Also in AccountModels.cs, add a new class called ExtraUserInformation.</span></span> <span data-ttu-id="64689-220">이 클래스는 데이터베이스에 만들어지는 새 테이블을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="64689-220">This class represents the new table which will be created in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

<span data-ttu-id="64689-221">UsersContext 클래스의 새 클래스에 대 한 DbSet 속성을 만들려면 아래 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-221">In the UsersContext class, add the highlighted code below to create a DbSet property for the new class.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

<span data-ttu-id="64689-222">이제 새 테이블을 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-222">You are now ready to create the new table.</span></span> <span data-ttu-id="64689-223">다시 패키지 관리자 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64689-223">Open the Package Manager Console again and this time:</span></span>

1. <span data-ttu-id="64689-224">명령을 실행 하 여 **추가 마이그레이션 AddExtraUserInformation**</span><span class="sxs-lookup"><span data-stu-id="64689-224">Run the command **add-migration AddExtraUserInformation**</span></span>
2. <span data-ttu-id="64689-225">명령을 실행 하 여 **데이터베이스 업데이트**</span><span class="sxs-lookup"><span data-stu-id="64689-225">Run the command **update-database**</span></span>

<span data-ttu-id="64689-226">이제 새 테이블 데이터베이스에 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-226">The new table now exists in the database.</span></span>

## <a name="retrieve-the-additional-data"></a><span data-ttu-id="64689-227">추가 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-227">Retrieve the additional data</span></span>

<span data-ttu-id="64689-228">추가 사용자 데이터를 검색 하는 방법은 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-228">There are two ways to retrieve additional user data.</span></span> <span data-ttu-id="64689-229">첫 번째 방법은 인증 요청 하는 동안 기본적으로 다시 전달 되는 사용자 데이터를 유지 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="64689-229">The first way is to retain user data that is passed back, by default, during the authentication request.</span></span> <span data-ttu-id="64689-230">두 번째 방법은 특히 공급자 API를 호출 하 고 추가 정보를 요청 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="64689-230">The second way is to specifically call the provider API and request more information.</span></span> <span data-ttu-id="64689-231">FullName 및 링크에 대 한 값은 자동으로 Facebook로 다시 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64689-231">Values for FullName and Link are automatically passed back by Facebook.</span></span> <span data-ttu-id="64689-232">Facebook 계정 확인에 있는지 여부를 나타내는 값을 Facebook API 호출을 통해 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64689-232">A value that indicates whether Facebook has verified the account is retrieved through a call to the Facebook API.</span></span> <span data-ttu-id="64689-233">첫째, FullName 및 링크에 대 한 값을 채웁니다 수 있으며 다음 나중에 확인 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="64689-233">First, you will populate values for FullName and Link, and then later, you will get the verified value.</span></span>

<span data-ttu-id="64689-234">추가 사용자 데이터를 검색 하려면 엽니다는 **AccountController.cs** 파일을 **컨트롤러** 폴더.</span><span class="sxs-lookup"><span data-stu-id="64689-234">To retrieve the additional user data, open the **AccountController.cs** file in the **Controllers** folder.</span></span>

<span data-ttu-id="64689-235">이 파일에는 로깅, 등록 및 계정 관리에 대 한 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-235">This file contains the logic for logging, registering, and managing accounts.</span></span> <span data-ttu-id="64689-236">특히, 호출 된 메서드를 확인할 수 있습니다 **ExternalLoginCallback** 하 고 **ExternalLoginConfirmation**합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-236">In particular, notice the methods called **ExternalLoginCallback** and **ExternalLoginConfirmation**.</span></span> <span data-ttu-id="64689-237">이러한 메서드 내에서 응용 프로그램에 대 한 외부 로그인 작업을 사용자 지정 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-237">Within these methods, you can add code to customize external login operations for your application.</span></span> <span data-ttu-id="64689-238">첫 번째 줄을 **ExternalLoginCallback** 메서드에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-238">The first line of the **ExternalLoginCallback** method contains:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

<span data-ttu-id="64689-239">추가 사용자 데이터에 다시 전달 됩니다는 **ExtraData** 의 속성을 **AuthenticationResult** 에서 반환 되는 개체를 **VerifyAuthentication** 메서드.</span><span class="sxs-lookup"><span data-stu-id="64689-239">Additional user data is passed back in the **ExtraData** property of the **AuthenticationResult** object that is returned from the **VerifyAuthentication** method.</span></span> <span data-ttu-id="64689-240">Facebook 클라이언트에서 다음 값이 포함 된 **ExtraData** 속성:</span><span class="sxs-lookup"><span data-stu-id="64689-240">The Facebook client contains the following values in the **ExtraData** property:</span></span>

- <span data-ttu-id="64689-241">ID</span><span class="sxs-lookup"><span data-stu-id="64689-241">id</span></span>
- <span data-ttu-id="64689-242">name</span><span class="sxs-lookup"><span data-stu-id="64689-242">name</span></span>
- <span data-ttu-id="64689-243">선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-243">link</span></span>
- <span data-ttu-id="64689-244">성별</span><span class="sxs-lookup"><span data-stu-id="64689-244">gender</span></span>
- <span data-ttu-id="64689-245">accesstoken</span><span class="sxs-lookup"><span data-stu-id="64689-245">accesstoken</span></span>

<span data-ttu-id="64689-246">다른 공급자 ExtraData 속성에서 유사 하지만 약간 다른 데이터를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-246">Other providers will have similar but slightly different data in the ExtraData property.</span></span>

<span data-ttu-id="64689-247">사이트에 새 사용자 인 경우 일부 추가 데이터를 검색 및 확인 보기로 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-247">If the user is new to your site, you will retrieve some the additional data and pass that data to the confirmation view.</span></span> <span data-ttu-id="64689-248">메서드에서 코드의 마지막 블록은 사용자가 사이트에 새 하는 경우에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64689-248">The last block of code in the method is run only if the user is new to your site.</span></span> <span data-ttu-id="64689-249">다음 줄을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="64689-249">Replace the following line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

<span data-ttu-id="64689-250">이 줄:</span><span class="sxs-lookup"><span data-stu-id="64689-250">With this line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

<span data-ttu-id="64689-251">이 변경은 단순히 FullName 및 링크 속성 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-251">This change merely includes values for the FullName and Link properties.</span></span>

<span data-ttu-id="64689-252">에 **ExternalLoginConfirmation** 메서드를 코드 강조 표시 된 대로 추가 사용자 정보를 저장 하려면 아래를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-252">In the **ExternalLoginConfirmation** method, modify the code as highlighted below to save the additional user information.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a><span data-ttu-id="64689-253">뷰를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-253">Adjusting the view</span></span>

<span data-ttu-id="64689-254">공급자에서 검색 하는 추가 사용자 데이터를 등록 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64689-254">The additional user data that you retrieve from the provider will be displayed in the registration page.</span></span>

<span data-ttu-id="64689-255">에 **뷰**/**계정** 폴더를 열고 **ExternalLoginConfirmation.cshtml**합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-255">In the **Views**/**Account** folder, open **ExternalLoginConfirmation.cshtml**.</span></span> <span data-ttu-id="64689-256">사용자 이름에 대 한 기존 필드를 아래 FullName, 링크 및 PictureLink에 대 한 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-256">Below the existing field for user name, add fields for FullName, Link, and PictureLink.</span></span>

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

<span data-ttu-id="64689-257">준비가 이제 거의 응용 프로그램을 실행 하 고 저장 하는 추가 정보를 사용 하 여 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-257">You are now almost ready to run the application and register a new user with the additional information saved.</span></span> <span data-ttu-id="64689-258">사이트를 사용 하 여 이미 등록 되지 않은 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-258">You must have an account that is not already registered with the site.</span></span> <span data-ttu-id="64689-259">다른 테스트 계정을 사용 하거나의 행을 삭제 합니다 **UserProfile** 및 **웹 페이지\_OAuthMembership** 다시 사용 하려는 계정에 대 한 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="64689-259">You can either use a different test account, or delete the rows in the **UserProfile** and **webpages\_OAuthMembership** tables for the account you wish to reuse.</span></span> <span data-ttu-id="64689-260">이러한 행을 삭제 하 여 계정을 다시 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-260">By deleting those rows, you will ensure that the account is registered again.</span></span>

<span data-ttu-id="64689-261">응용 프로그램을 실행 하 고 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-261">Run the application and register the new user.</span></span> <span data-ttu-id="64689-262">이 시간 확인 페이지에는 더 많은 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-262">Notice that this time the confirmation page contains more values.</span></span>

![register](using-oauth-providers-with-mvc/_static/image12.png)

<span data-ttu-id="64689-264">등록을 완료 한 후 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-264">After completing registration, close the browser.</span></span> <span data-ttu-id="64689-265">데이터베이스에서 새 값이 표시를 확인 합니다 **ExtraUserInformation** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="64689-265">Look in the database to notice the new values in the **ExtraUserInformation** table.</span></span>

## <a name="install-nuget-package-for-facebook-api"></a><span data-ttu-id="64689-266">Facebook API에 대 한 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-266">Install NuGet package for Facebook API</span></span>

<span data-ttu-id="64689-267">Facebook은는 [API](https://developers.facebook.com/docs/reference/apis/) 작업을 수행 하려면 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-267">Facebook provides an [API](https://developers.facebook.com/docs/reference/apis/) that you can call to perform operations.</span></span> <span data-ttu-id="64689-268">보내는 HTTP 요청을 전달 하거나 해당 요청을 보내는 용이 하 게 하는 NuGet 패키지 설치를 사용 하 여 Facebook API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-268">You can call the Facebook API either by directing sending HTTP requests, or by using installing a NuGet package that facilitates sending those requests.</span></span> <span data-ttu-id="64689-269">이 자습서의 예제는 NuGet 패키지를 사용 하 여 아닌 NuGet을 설치 패키지 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-269">Using a NuGet package is shown in this tutorial, but installing NuGet package is not essential.</span></span> <span data-ttu-id="64689-270">이 자습서에서는 Facebook C# SDK 패키지를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="64689-270">This tutorial shows how to use the Facebook C# SDK package.</span></span> <span data-ttu-id="64689-271">Facebook API 호출에 도움이 되는 다른 NuGet 패키지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-271">There are other NuGet packages that assist with calling the Facebook API.</span></span>

<span data-ttu-id="64689-272">**NuGet 패키지 관리** windows Facebook C# SDK 패키지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-272">From the **Manage NuGet Packages** windows, select the Facebook C# SDK package.</span></span>

![패키지 설치](using-oauth-providers-with-mvc/_static/image13.png)

<span data-ttu-id="64689-274">사용자에 대 한 액세스 토큰이 필요한 작업을 호출 하는 Facebook C# SDK를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-274">You will use the Facebook C# SDK to call an operation that requires the access token for the user.</span></span> <span data-ttu-id="64689-275">다음 섹션에는 액세스 토큰을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="64689-275">The next section shows how to get the access token.</span></span>

## <a name="retrieve-access-token"></a><span data-ttu-id="64689-276">액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="64689-276">Retrieve access token</span></span>

<span data-ttu-id="64689-277">대부분의 외부 공급자 사용자의 자격 증명이 확인 된 후에 액세스 토큰을 다시 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-277">Most external providers pass back an access token after the user's credentials are verified.</span></span> <span data-ttu-id="64689-278">이 액세스 토큰은 인증 된 사용자만 사용할 수 있는 작업을 호출할 수 있기 때문에 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-278">This access token is very important because it enables you to call operations that are only available to authenticated users.</span></span> <span data-ttu-id="64689-279">따라서 검색 하 고 액세스 토큰을 저장 반드시 더 많은 기능을 제공 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="64689-279">Therefore, retrieving and storing the access token is essential when you want to provide more functionality.</span></span>

<span data-ttu-id="64689-280">외부 공급자에 따라 제한 된 기간 동안에 대 한 액세스 토큰 유효할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-280">Depending on the external provider, the access token may be valid for only a limited amount of time.</span></span> <span data-ttu-id="64689-281">유효한 액세스 토큰을 갖도록를 검색 합니다 것 될 때마다 사용자, 로그인 및 세션 값으로 저장 하지 않고 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-281">To ensure that you have a valid access token, you will retrieve it each time the user logs in, and store it as a session value rather than save it to a database.</span></span>

<span data-ttu-id="64689-282">에 **ExternalLoginCallback** 메서드를 액세스 토큰은에 다시 전달도 **ExtraData** 의 속성을 **AuthenticationResult** 개체.</span><span class="sxs-lookup"><span data-stu-id="64689-282">In the **ExternalLoginCallback** method, the access token is also passed back in the **ExtraData** property of the **AuthenticationResult** object.</span></span> <span data-ttu-id="64689-283">강조 표시 된 코드를 추가 합니다 **ExternalLoginCallback** 액세스 토큰을 저장 하는 **세션** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="64689-283">Add the highlighted code to **ExternalLoginCallback** to save the access token in the **Session** object.</span></span> <span data-ttu-id="64689-284">이 코드는 사용자가 Facebook 계정에 로그인 할 때마다 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64689-284">This code is run every time the user logs in with a Facebook account.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

<span data-ttu-id="64689-285">하지만 Facebook에서 액세스 토큰을 검색 하는이 예제를 통해 검색할 수 있는 액세스 토큰 외부 공급자에서 명명 된 동일한 키 &quot;accesstoken&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-285">Although this example retrieves an access token from Facebook, you can retrieve the access token from any external provider through the same key named &quot;accesstoken&quot;.</span></span>

## <a name="logging-off"></a><span data-ttu-id="64689-286">로그오프</span><span class="sxs-lookup"><span data-stu-id="64689-286">Logging off</span></span>

<span data-ttu-id="64689-287">기본값 **로그 오프** 메서드가 응용 프로그램에서 사용자를 로그 했지만 사용자를 외부 공급자 로그 아웃을 기록 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-287">The default **LogOff** method logs the user out of your application, but does not log the user out of the external provider.</span></span> <span data-ttu-id="64689-288">Facebook에서 사용자를 로그 사용자가 로그온 한 후 유지 토큰을 방지를 다음 강조 표시 된 코드를 추가할 수 있습니다 합니다 **로그 오프** 메서드는 AccountController에서.</span><span class="sxs-lookup"><span data-stu-id="64689-288">To log the user out of Facebook, and prevent the token from persisting after the user has logged off, you can add the following highlighted code to the **LogOff** method in the AccountController.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

<span data-ttu-id="64689-289">제공한 값을 `next` 매개 변수는 Facebook에서 사용자가 로그온 한 후 사용할 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="64689-289">The value you provide in the `next` parameter is the URL to use after the user has logged out of Facebook.</span></span> <span data-ttu-id="64689-290">로컬 컴퓨터에 테스트 하는 경우 로컬 사이트에 대 한 올바른 포트 번호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-290">When testing on your local computer, you would provide the correct port number for your local site.</span></span> <span data-ttu-id="64689-291">프로덕션 환경에서 contoso.com과 같은 기본 페이지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-291">In production, you would provide a default page, such as contoso.com.</span></span>

## <a name="retrieve-user-information-that-requires-the-access-token"></a><span data-ttu-id="64689-292">액세스 토큰이 필요한 사용자 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-292">Retrieve user information that requires the access token</span></span>

<span data-ttu-id="64689-293">액세스 토큰을 저장 하 고 Facebook C# SDK 패키지를 설치 했으므로 Facebook에서 추가 사용자 정보를 요청 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-293">Now that you have stored the access token and installed the Facebook C# SDK package, you can use them together to request additional user information from Facebook.</span></span> <span data-ttu-id="64689-294">에 **ExternalLoginConfirmation** 메서드를의 인스턴스를 만들 합니다 **FacebookClient** 액세스 토큰의 값을 전달 하 여 클래스.</span><span class="sxs-lookup"><span data-stu-id="64689-294">In the **ExternalLoginConfirmation** method, create an instance of the **FacebookClient** class by passing the value of the access token.</span></span> <span data-ttu-id="64689-295">값을 요청 합니다 **확인할** 현재 인증 된 사용자에 대 한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="64689-295">Request the value of the **verified** property for the current, authenticated user.</span></span> <span data-ttu-id="64689-296">합니다 **확인할** 속성 Facebook에 휴대 전화에 메시지를 보내는 등의 다른 수단을 통해 계정 유효성 검사가 수행 되는지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="64689-296">The **verified** property indicates whether Facebook has validated the account through some other means, such as sending a message to a cell phone.</span></span> <span data-ttu-id="64689-297">데이터베이스에서이 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-297">Save this value in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

<span data-ttu-id="64689-298">다시 사용자에 대 한 데이터베이스의 레코드를 삭제 하거나 다른 Facebook 계정을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-298">You will again need to either delete the records in the database for the user, or use a different Facebook account.</span></span>

<span data-ttu-id="64689-299">응용 프로그램을 실행 하 고 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="64689-299">Run the application, and register the new user.</span></span> <span data-ttu-id="64689-300">확인 합니다 **ExtraUserInformation** 테이블을 참조 하는 확인 된 속성의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="64689-300">Look at the **ExtraUserInformation** table to see the value for the Verified property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="64689-301">결론</span><span class="sxs-lookup"><span data-stu-id="64689-301">Conclusion</span></span>

<span data-ttu-id="64689-302">이 자습서에서는 Facebook을 사용 하 여 사용자 인증 및 등록 데이터에 대 한 통합 된 사이트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-302">In this tutorial, you created a site that is integrated with Facebook for user authentication and registration data.</span></span> <span data-ttu-id="64689-303">MVC 4 웹 응용 프로그램 및 해당 기본 동작을 사용자 지정 하는 방법에 대 한 설정 된 기본 동작에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="64689-303">You learned about the default behavior that is set up for MVC 4 web application, and how to customize that default behavior.</span></span>

## <a name="related-topics"></a><span data-ttu-id="64689-304">관련 항목</span><span class="sxs-lookup"><span data-stu-id="64689-304">Related topics</span></span>

- [<span data-ttu-id="64689-305">인증 및 SQL DB를 사용 하 여 ASP.NET MVC 앱을 만들고 Azure App Service에 배포</span><span class="sxs-lookup"><span data-stu-id="64689-305">Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service</span></span>](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
