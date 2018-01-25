---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: "MVC 4와 함께 OAuth 공급자를 사용 하 여 | Microsoft Docs"
author: tfitzmac
description: "이 자습서에서는 사용자가 Facebo 같은 외부 공급자의 자격 증명으로 로그인 할 수 있는 ASP.NET MVC 4 웹 응용 프로그램을 작성 하는 방법..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/19/2013
ms.topic: article
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: f0d053cecbf9a59f258470ee370852e3f112908c
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="using-oauth-providers-with-mvc-4"></a><span data-ttu-id="c48c1-103">MVC 4와 함께 OAuth 공급자 사용</span><span class="sxs-lookup"><span data-stu-id="c48c1-103">Using OAuth Providers with MVC 4</span></span>
====================
<span data-ttu-id="c48c1-104">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c48c1-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c48c1-105">이 자습서에서는 사용자가 Facebook, Twitter, Microsoft 또는 Google, 같은 외부 공급자의 자격 증명으로 로그인 한 다음에 해당 공급자 로부터 기능 중 일부를 통합 수 있도록 ASP.NET MVC 4 웹 응용 프로그램을 빌드하는 방법을 사용자 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-105">This tutorial shows you how to build an ASP.NET MVC 4 web application that enables users to log in with credentials from an external provider, such as Facebook, Twitter, Microsoft, or Google, and then integrate some of the functionality from those providers into your web application.</span></span> <span data-ttu-id="c48c1-106">간단한 설명을 위해이 자습서에서 Facebook 자격 증명 사용에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-106">For simplicity, this tutorial focuses on working with credentials from Facebook.</span></span>
> 
> <span data-ttu-id="c48c1-107">ASP.NET MVC 5 웹 응용 프로그램에 외부 자격 증명을 사용 하려면 참조 [Facebook, Google OAuth2 및 OpenID 로그온 ASP.NET MVC 5 응용 프로그램을 만들](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-107">To use external credentials in an ASP.NET MVC 5 web application, see [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
> 
> <span data-ttu-id="c48c1-108">수백만 명 이상의 사용자 계정을 이러한 외부 공급자와 함께 이미 있기 때문에 중요 한 장점을 제공 웹 사이트에서 이러한 자격 증명을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-108">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="c48c1-109">이러한 사용자 더 만들고 새로운 자격 증명 집합을 기억 하지 않아도 되는 경우 사이트에 대 한 등록을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-109">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span> <span data-ttu-id="c48c1-110">또한 이러한 공급자 중 하나를 통해 사용자가 로그인 한 후 공급자에서 소셜 작업을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-110">Also, after a user has logged in through one of these providers, you can incorporate social operations from the provider.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="c48c1-111">만들 것인지</span><span class="sxs-lookup"><span data-stu-id="c48c1-111">What you'll build</span></span>

<span data-ttu-id="c48c1-112">이 자습서에서는 두 가지 주요 목표가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-112">There are two main goals in this tutorial:</span></span>

1. <span data-ttu-id="c48c1-113">OAuth 공급자 로부터 자격 증명으로 로그인 할 사용자를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-113">Enable a user to log in with credentials from an OAuth provider.</span></span>
2. <span data-ttu-id="c48c1-114">공급자에서 계정 정보를 검색 하 고 사이트에 대 한 계정 등록 정보를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-114">Retrieve account information from the provider and integrate that information with the account registration for your site.</span></span>

<span data-ttu-id="c48c1-115">이 자습서의 예제를 인증 공급자로 Facebook을 사용 하 여에 초점을 맞추고 있지만 공급자 중 하나를 사용 하는 코드를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-115">Although the examples in this tutorial focus on using Facebook as the authentication provider, you can modify the code to use any of the providers.</span></span> <span data-ttu-id="c48c1-116">모든 공급자를 구현 하는 단계는이 자습서에 표시 되는 단계와 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-116">The steps to implement any provider are very similar to the steps you will see in this tutorial.</span></span> <span data-ttu-id="c48c1-117">만 중요 한 차이점이 공급자의 API 직접 호출을 만들 때 설정으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-117">You will only notice significant differences when making direct calls to the provider's API set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c48c1-118">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c48c1-118">Prerequisites</span></span>

- <span data-ttu-id="c48c1-119">[Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) 또는 [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span><span class="sxs-lookup"><span data-stu-id="c48c1-119">[Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) or [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span></span>

<span data-ttu-id="c48c1-120">또는</span><span class="sxs-lookup"><span data-stu-id="c48c1-120">Or</span></span>

- <span data-ttu-id="c48c1-121">Microsoft Visual Studio 2010 SP1 또는 [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span><span class="sxs-lookup"><span data-stu-id="c48c1-121">Microsoft Visual Studio 2010 SP1 or [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span></span>
- [<span data-ttu-id="c48c1-122">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="c48c1-122">ASP.NET MVC 4</span></span>](https://go.microsoft.com/fwlink/?LinkId=243392)

<span data-ttu-id="c48c1-123">또한이 항목에서는 ASP.NET MVC 및 Visual Studio에 대 한 기본 지식이 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-123">Furthermore, this topic assumes you have basic knowledge about ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="c48c1-124">ASP.NET MVC 4에 대 한 소개를 보려면 참고 [ASP.NET MVC 4 소개](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-124">If you need an introduction to ASP.NET MVC 4, see [Intro to ASP.NET MVC 4](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md).</span></span>

## <a name="create-the-project"></a><span data-ttu-id="c48c1-125">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-125">Create the project</span></span>

<span data-ttu-id="c48c1-126">Visual Studio에서 새 ASP.NET MVC 4 웹 응용 프로그램을 만들고 이름을 &quot;OAuthMVC&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-126">In Visual Studio, create a new ASP.NET MVC 4 Web Application, and name it &quot;OAuthMVC&quot;.</span></span> <span data-ttu-id="c48c1-127">.NET Framework 4.5 또는 4 중 하나를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-127">You can target either .NET Framework 4.5 or 4.</span></span>

![프로젝트 만들기](using-oauth-providers-with-mvc/_static/image1.png)

<span data-ttu-id="c48c1-129">새 ASP.NET MVC 4 프로젝트 창에서 선택한 **인터넷 응용 프로그램** 둡니다 **Razor** 를 뷰 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-129">In the New ASP.NET MVC 4 Project window, select **Internet Application** and leave **Razor** as the view engine.</span></span>

![인터넷 응용 프로그램 선택](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a><span data-ttu-id="c48c1-131">공급자를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="c48c1-131">Enable a provider</span></span>

<span data-ttu-id="c48c1-132">인터넷 응용 프로그램 템플릿을 사용 하 여 MVC 4 웹 응용 프로그램을 만들 때는 프로젝트는 응용 프로그램에서 AuthConfig.cs 이라는 파일로 내보내집니다으로 생성\_시작 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-132">When you create an MVC 4 web application with the Internet Application template, the project is created with a file named AuthConfig.cs in the App\_Start folder.</span></span>

![AuthConfig 파일](using-oauth-providers-with-mvc/_static/image3.png)

<span data-ttu-id="c48c1-134">AuthConfig 파일 외부 인증 공급자에 대 한 클라이언트를 등록 하는 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-134">The AuthConfig file contains code to register clients for external authentication providers.</span></span> <span data-ttu-id="c48c1-135">기본적으로이 코드는 주석 처리를 외부 공급자의 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-135">By default, this code is commented out, so none of the external providers are enabled.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

<span data-ttu-id="c48c1-136">외부 인증 클라이언트를 사용 하려면이 코드 주석 처리를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-136">You must uncomment this code to use the external authentication client.</span></span> <span data-ttu-id="c48c1-137">사이트에 포함 하려는 공급자만 주석입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-137">You uncomment only the providers you want to include in your site.</span></span> <span data-ttu-id="c48c1-138">이 자습서에서는 Facebook 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-138">For this tutorial, you will only enable the Facebook credentials.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

<span data-ttu-id="c48c1-139">위의 예에서 메서드가 등록 매개 변수에 대해 빈 문자열이 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-139">Notice in the above example that the method includes empty strings for the registration parameters.</span></span> <span data-ttu-id="c48c1-140">이제 응용 프로그램을 실행 하려고 하면 응용 프로그램 매개 변수에 대해 빈 문자열이 허용 되지 않으므로 인수 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-140">If you try to run the application now, the application throws an argument exception because empty strings are not allowed for the parameters.</span></span> <span data-ttu-id="c48c1-141">유효한 값을 제공 하려면 다음 섹션에 나와 있는 것 처럼 외부 공급자와 웹 사이트 등록 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-141">To provide valid values, you must register your web site with the external providers, as shown in the next section.</span></span>

## <a name="registering-with-an-external-provider"></a><span data-ttu-id="c48c1-142">외부 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="c48c1-142">Registering with an external provider</span></span>

<span data-ttu-id="c48c1-143">외부 공급자의 자격 증명이 있는 사용자를 인증 하려면 공급자와 함께 웹 사이트를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-143">To authenticate users with credentials from an external provider, you must register your web site with the provider.</span></span> <span data-ttu-id="c48c1-144">사이트를 등록 하면 매개 변수 (예: 키 또는 id 및 암호) 클라이언트를 등록할 때를 포함 하도록 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-144">When you register your site, you will receive the parameters (such as key or id, and secret) to include when registering the client.</span></span> <span data-ttu-id="c48c1-145">사용 하려는 공급자와 함께 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-145">You must have an account with the providers you wish to use.</span></span>

<span data-ttu-id="c48c1-146">이 자습서에서는 이러한 공급자를 등록 하기 위해 수행 해야 하는 단계를 모두 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-146">This tutorial does not show all of the steps you must perform to register with these providers.</span></span> <span data-ttu-id="c48c1-147">단계는 일반적으로 어려운 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-147">The steps are typically not difficult.</span></span> <span data-ttu-id="c48c1-148">사이트를 성공적으로 등록 하려면 해당 사이트에 제공 된 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-148">To successfully register your site, follow the instructions provided on those sites.</span></span> <span data-ttu-id="c48c1-149">사이트에 등록을 시작 하려면에 대 한 개발자 사이트를 참조:</span><span class="sxs-lookup"><span data-stu-id="c48c1-149">To get started with registering your site, see the developer site for:</span></span>

- [<span data-ttu-id="c48c1-150">Facebook</span><span class="sxs-lookup"><span data-stu-id="c48c1-150">Facebook</span></span>](https://developers.facebook.com/)
- [<span data-ttu-id="c48c1-151">Google</span><span class="sxs-lookup"><span data-stu-id="c48c1-151">Google</span></span>](https://developers.google.com/)
- [<span data-ttu-id="c48c1-152">Microsoft</span><span class="sxs-lookup"><span data-stu-id="c48c1-152">Microsoft</span></span>](http://manage.dev.live.com/)
- [<span data-ttu-id="c48c1-153">Twitter</span><span class="sxs-lookup"><span data-stu-id="c48c1-153">Twitter</span></span>](https://dev.twitter.com/)

<span data-ttu-id="c48c1-154">사이트를 Facebook을 등록할 때 제공할 수 있습니다 &quot;localhost&quot; 사이트 도메인에 대 한 및 `&quot;http://localhost/&quot;` 아래 그림과 같이 URL에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-154">When registering your site with Facebook, you can provide &quot;localhost&quot; for the site domain and `&quot;http://localhost/&quot;` for the URL, as shown in the image below.</span></span> <span data-ttu-id="c48c1-155">Localhost를 사용 하 여 대부분의 공급자와 작동 하지만 현재 Microsoft 공급자와 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-155">Using localhost works with most providers, but currently does not work with the Microsoft provider.</span></span> <span data-ttu-id="c48c1-156">Microsoft 공급자에 대 한 올바른 웹 사이트 URL을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-156">For the Microsoft provider, you must include a valid web site URL.</span></span>

![사이트를 등록 합니다.](using-oauth-providers-with-mvc/_static/image4.png)

<span data-ttu-id="c48c1-158">위의 그림에서 응용 프로그램 id, 응용 프로그램 암호 및 연락처 전자 메일에 대 한 값 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-158">In the previous image, the values for the app id, app secret, and contact email have been removed.</span></span> <span data-ttu-id="c48c1-159">사이트를 실제로 등록 하면 해당 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-159">When you actually register your site, those values will be present.</span></span> <span data-ttu-id="c48c1-160">응용 프로그램에 추가 하기 때문에 앱 id와 응용 프로그램 암호에 대 한 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-160">You will want to note the values for app id and app secret because you will add them to your application.</span></span>

## <a name="creating-test-users"></a><span data-ttu-id="c48c1-161">테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c48c1-161">Creating test users</span></span>

<span data-ttu-id="c48c1-162">사이트를 테스트 하려면 기존 Facebook 계정을 사용 하 여 잘 해도 하는 경우에이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-162">If you do not mind using an existing Facebook account to test your site, you can skip this section.</span></span>

<span data-ttu-id="c48c1-163">Facebook 응용 프로그램 관리 페이지 내에서 응용 프로그램에 대 한 테스트 사용자를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-163">You can easily create test users for your application within the Facebook app management page.</span></span> <span data-ttu-id="c48c1-164">이 사용할 수 있습니다 사이트에 로그인 할 계정을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-164">You can use these test accounts to log in to your site.</span></span> <span data-ttu-id="c48c1-165">클릭 하 여 테스트 사용자를 만들면는 **역할** 클릭 하는 왼쪽된 탐색 창에서 링크는 **만들기** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-165">You create test users by clicking the **Roles** link in the left navigation pane and the clicking the **Create** link.</span></span>

![테스트 사용자 만들기](using-oauth-providers-with-mvc/_static/image5.png)

<span data-ttu-id="c48c1-167">Facebook 사이트 요청 하는 테스트 계정의 수를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-167">The Facebook site automatically creates the number of test accounts that you request.</span></span>

## <a name="adding-application-id-and-secret-from-the-provider"></a><span data-ttu-id="c48c1-168">공급자에서 응용 프로그램 id 및 암호 추가</span><span class="sxs-lookup"><span data-stu-id="c48c1-168">Adding application id and secret from the provider</span></span>

<span data-ttu-id="c48c1-169">이제 facebook에서 id와 암호를 수신 AuthConfig 파일로 돌아가서을 매개 변수 값으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-169">Now that you have received the id and secret from Facebook, go back to the AuthConfig file and add them as the parameter values.</span></span> <span data-ttu-id="c48c1-170">아래에 표시 된 값이 실제 값.</span><span class="sxs-lookup"><span data-stu-id="c48c1-170">The values shown below are not real values.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a><span data-ttu-id="c48c1-171">외부 자격 증명으로 로그인</span><span class="sxs-lookup"><span data-stu-id="c48c1-171">Log in with external credentials</span></span>

<span data-ttu-id="c48c1-172">사이트의 외부 자격 증명을 사용 하도록 설정 하기 위해 해야 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-172">That is all you have to do to enable external credentials in your site.</span></span> <span data-ttu-id="c48c1-173">응용 프로그램을 실행 하 고 오른쪽 위 모서리의 로그인 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-173">Run your application and click the login link in the upper right corner.</span></span> <span data-ttu-id="c48c1-174">자동으로 서식 파일에 인식 공급자로 Facebook을 등록 한 하 고 공급자에 대 한 단추가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-174">The template automatically recognizes that you have registered Facebook as a provider and includes a button for the provider.</span></span> <span data-ttu-id="c48c1-175">여러 공급자를 등록 하는 경우 각각에 대 한 단추는 자동으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-175">If you register multiple providers, a button for each one is automatically included.</span></span>

![외부 로그인](using-oauth-providers-with-mvc/_static/image6.png)

<span data-ttu-id="c48c1-177">이 자습서에는 외부 공급자에 대 한 로그인 단추를 사용자 지정 하는 방법을 설명 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-177">This tutorial does not cover how to customize the log in buttons for the external providers.</span></span> <span data-ttu-id="c48c1-178">해당 정보를 참조 하십시오. [OAuth/OpenID를 사용 하는 경우 로그인 UI를 사용자 지정](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-178">For that information, see [Customizing the login UI when using OAuth/OpenID](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx).</span></span>

<span data-ttu-id="c48c1-179">Facebook 자격 증명으로 로그인에 Facebook 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-179">Click on the Facebook button to log in with Facebook credentials.</span></span> <span data-ttu-id="c48c1-180">외부 공급자 중 하나를 선택 하면 해당 사이트로 리디렉션됩니다 하 고 해당 서비스에서 로그인 하 라는 메시지가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-180">When you select one of the external providers, you are redirected to that site and prompted by that service to log in.</span></span>

<span data-ttu-id="c48c1-181">다음 이미지는 facebook 로그인 화면을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-181">The following image shows the login screen for Facebook.</span></span> <span data-ttu-id="c48c1-182">이 oauthmvcexample 이라는 사이트에 로그인 할 Facebook 계정을 사용 하 고 있는지를 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-182">It notes that you are using your Facebook account to log in to a site named oauthmvcexample.</span></span>

![facebook 인증](using-oauth-providers-with-mvc/_static/image7.png)

<span data-ttu-id="c48c1-184">Facebook 자격 증명으로 로그인을 한 후 페이지에 사용자 사이트 기본 정보에 액세스할 수 있는지 알립니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-184">After logging in with Facebook credentials, a page informs the user that the site will have access to basic information.</span></span>

![사용 권한 요청](using-oauth-providers-with-mvc/_static/image8.png)

<span data-ttu-id="c48c1-186">선택한 후 **앱으로 이동**, 사용자는 사이트에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-186">After selecting **Go to App**, the user must register for the site.</span></span> <span data-ttu-id="c48c1-187">다음 이미지는 사용자가 Facebook 자격 증명으로 로그온 한 후 등록 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-187">The following image shows the registration page after a user has logged in with Facebook credentials.</span></span> <span data-ttu-id="c48c1-188">사용자 이름은 일반적으로 공급자에서 이름으로 미리 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-188">The user name is typically pre-filled with a name from the provider.</span></span>

![register](using-oauth-providers-with-mvc/_static/image9.png)

<span data-ttu-id="c48c1-190">클릭 **등록** 등록을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-190">Click **Register** to complete registration.</span></span> <span data-ttu-id="c48c1-191">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-191">Close the browser.</span></span>

<span data-ttu-id="c48c1-192">새 계정 범주가 데이터베이스에 추가 된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-192">You can see that the new account has been added to your database.</span></span> <span data-ttu-id="c48c1-193">서버 탐색기를 열고는 **DefaultConnection** 데이터베이스 및 열은 **테이블** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-193">In Server Explorer, open the **DefaultConnection** database and open the **Tables** folder.</span></span>

![데이터베이스 테이블](using-oauth-providers-with-mvc/_static/image10.png)

<span data-ttu-id="c48c1-195">마우스 오른쪽 단추로 클릭는 **UserProfile** 테이블을 선택한 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-195">Right-click the **UserProfile** table and select **Show Table Data**.</span></span>

![데이터 표시](using-oauth-providers-with-mvc/_static/image11.png)

<span data-ttu-id="c48c1-197">추가한 새 계정에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-197">You will see the new account you added.</span></span> <span data-ttu-id="c48c1-198">데이터를 살펴보고 **웹 페이지\_OAuthMembership** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-198">Look at the data in **webpage\_OAuthMembership** table.</span></span> <span data-ttu-id="c48c1-199">방금 추가한 계정에 대 한 외부 공급자와 관련 된 자세한 데이터가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-199">You will see more data related to the external provider for the account you just added.</span></span>

<span data-ttu-id="c48c1-200">외부 인증을 사용 하도록 설정 하려는 경우 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-200">If you only want to enable external authentication, you are done.</span></span> <span data-ttu-id="c48c1-201">다음 섹션에 나와 있는 것 처럼 새 사용자 등록 프로세스에 공급자 정보를에서, 통합할 더 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-201">However, you can further integrate information from the provider into the new user registration process, as shown in the following sections.</span></span>

## <a name="create-models-for-additional-user-information"></a><span data-ttu-id="c48c1-202">추가 사용자 정보에 대 한 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="c48c1-202">Create models for additional user information</span></span>

<span data-ttu-id="c48c1-203">에서 설명한 것 처럼 이전 섹션을 작동 하려면 기본 제공 계정 등록에 대 한 추가 정보를 검색할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-203">As you noticed in the previous sections, you do not need to retrieve any additional information for the built-in account registration to work.</span></span> <span data-ttu-id="c48c1-204">그러나 대부분의 외부 공급자의 사용자에 대 한 다시 추가 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-204">However, most external providers pass back additional information about the user.</span></span> <span data-ttu-id="c48c1-205">다음 섹션에는 해당 정보를 유지 하 고 데이터베이스에 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-205">The following sections show how to retain that information and save it to a database.</span></span> <span data-ttu-id="c48c1-206">특히, 사용자의 전체 이름, 사용자의 개인 웹 페이지의 URI에 대 한 값과 Facebook 계정을 확인 여부를 나타내는 값을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-206">Specifically, you will retain values for the user's full name, the URI of the user's personal web page, and a value that indicates whether Facebook has verified the account.</span></span>

<span data-ttu-id="c48c1-207">사용 하 여 [Code First 마이그레이션을](https://msdn.microsoft.com/data/jj591621) 추가 사용자 정보를 저장 하기 위한 테이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-207">You will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) to add a table for storing additional user information.</span></span> <span data-ttu-id="c48c1-208">되므로 현재 데이터베이스의 스냅숏을 만들 필요가 먼저 기존 데이터베이스에 테이블을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-208">You are adding the table to an existing database, so you will first need to create a snapshot of the current database.</span></span> <span data-ttu-id="c48c1-209">현재 데이터베이스의 스냅숏을 만들어서 마이그레이션 새 테이블만 포함 하는 나중에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-209">By creating a snapshot of the current database, you can later create a migration that contains only the new table.</span></span> <span data-ttu-id="c48c1-210">현재 데이터베이스의 스냅숏을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="c48c1-210">To create a snapshot of the current database:</span></span>

1. <span data-ttu-id="c48c1-211">열기는 **패키지 관리자 콘솔**</span><span class="sxs-lookup"><span data-stu-id="c48c1-211">Open the **Package Manager Console**</span></span>
2. <span data-ttu-id="c48c1-212">명령을 실행 **설정 마이그레이션**</span><span class="sxs-lookup"><span data-stu-id="c48c1-212">Run the command **enable-migrations**</span></span>
3. <span data-ttu-id="c48c1-213">명령을 실행 **IgnoreChanges 추가 마이그레이션 초기 –**</span><span class="sxs-lookup"><span data-stu-id="c48c1-213">Run the command **add-migration initial –IgnoreChanges**</span></span>
4. <span data-ttu-id="c48c1-214">명령을 실행 **데이터베이스 업데이트**</span><span class="sxs-lookup"><span data-stu-id="c48c1-214">Run the command **update-database**</span></span>

<span data-ttu-id="c48c1-215">이제 새 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-215">Now, you will add the new properties.</span></span> <span data-ttu-id="c48c1-216">모델 폴더에서 AccountModels.cs 파일을 열고 RegisterExternalLoginModel 클래스를 찾을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-216">In the Models folder, open the AccountModels.cs file, and find the RegisterExternalLoginModel class.</span></span> <span data-ttu-id="c48c1-217">다시 인증 공급자에서 제공 하는 값을 포함 하는 RegisterExternalLoginModel 클래스.</span><span class="sxs-lookup"><span data-stu-id="c48c1-217">The RegisterExternalLoginModel class holds values that come back from the authentication provider.</span></span> <span data-ttu-id="c48c1-218">FullName 및 링크를 아래 강조 표시 된 대로 명명 된 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-218">Add properties named FullName and Link, as highlighted below.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

<span data-ttu-id="c48c1-219">또한 AccountModels.cs, ExtraUserInformation 라는 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-219">Also in AccountModels.cs, add a new class called ExtraUserInformation.</span></span> <span data-ttu-id="c48c1-220">이 클래스는 데이터베이스에서 만들 수 있는 새 테이블을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-220">This class represents the new table which will be created in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

<span data-ttu-id="c48c1-221">UsersContext 클래스에서 새 클래스에 대 한 DbSet 속성을 생성 하려면 아래의 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-221">In the UsersContext class, add the highlighted code below to create a DbSet property for the new class.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

<span data-ttu-id="c48c1-222">이제 새 테이블을 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-222">You are now ready to create the new table.</span></span> <span data-ttu-id="c48c1-223">다시 패키지 관리자 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-223">Open the Package Manager Console again and this time:</span></span>

1. <span data-ttu-id="c48c1-224">명령을 실행 **추가 마이그레이션 AddExtraUserInformation**</span><span class="sxs-lookup"><span data-stu-id="c48c1-224">Run the command **add-migration AddExtraUserInformation**</span></span>
2. <span data-ttu-id="c48c1-225">명령을 실행 **데이터베이스 업데이트**</span><span class="sxs-lookup"><span data-stu-id="c48c1-225">Run the command **update-database**</span></span>

<span data-ttu-id="c48c1-226">새 테이블은 이제는 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-226">The new table now exists in the database.</span></span>

## <a name="retrieve-the-additional-data"></a><span data-ttu-id="c48c1-227">추가 데이터를 검색</span><span class="sxs-lookup"><span data-stu-id="c48c1-227">Retrieve the additional data</span></span>

<span data-ttu-id="c48c1-228">추가 사용자 데이터를 검색 하는 방법은 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-228">There are two ways to retrieve additional user data.</span></span> <span data-ttu-id="c48c1-229">첫 번째 방법은 인증 요청 하는 동안 기본적으로 다시 전달 되는 사용자 데이터를 유지 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-229">The first way is to retain user data that is passed back, by default, during the authentication request.</span></span> <span data-ttu-id="c48c1-230">두 번째 방법은 특히 공급자 API를 호출 하 고 추가 정보를 요청 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-230">The second way is to specifically call the provider API and request more information.</span></span> <span data-ttu-id="c48c1-231">FullName 및 링크 값에 대해 Facebook에서 다시 자동으로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-231">Values for FullName and Link are automatically passed back by Facebook.</span></span> <span data-ttu-id="c48c1-232">Facebook 계정을 확인 여부를 나타내는 값 Facebook API에 대 한 호출을 통해 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-232">A value that indicates whether Facebook has verified the account is retrieved through a call to the Facebook API.</span></span> <span data-ttu-id="c48c1-233">첫째, FullName 및 링크에 대 한 값을 채우는 됩니다 하 고 나중을 가져와서 확인 된 값.</span><span class="sxs-lookup"><span data-stu-id="c48c1-233">First, you will populate values for FullName and Link, and then later, you will get the verified value.</span></span>

<span data-ttu-id="c48c1-234">추가 사용자 데이터를 검색 하려면 열고는 **AccountController.cs** 파일에 **컨트롤러** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-234">To retrieve the additional user data, open the **AccountController.cs** file in the **Controllers** folder.</span></span>

<span data-ttu-id="c48c1-235">이 파일에는 로깅, 등록 및 계정 관리에 대 한 논리가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-235">This file contains the logic for logging, registering, and managing accounts.</span></span> <span data-ttu-id="c48c1-236">특히, 호출 하는 메서드를 확인할 **ExternalLoginCallback** 및 **ExternalLoginConfirmation**합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-236">In particular, notice the methods called **ExternalLoginCallback** and **ExternalLoginConfirmation**.</span></span> <span data-ttu-id="c48c1-237">이러한 메서드 내에서 응용 프로그램에 대 한 외부 로그인 작업을 지정 하기 위해 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-237">Within these methods, you can add code to customize external login operations for your application.</span></span> <span data-ttu-id="c48c1-238">첫 번째 줄은 **ExternalLoginCallback** 메서드에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-238">The first line of the **ExternalLoginCallback** method contains:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

<span data-ttu-id="c48c1-239">추가 사용자 데이터에 다시 전달 되는 **ExtraData** 의 속성은 **AuthenticationResult** 에서 반환 되는 개체는 **VerifyAuthentication** 메서드.</span><span class="sxs-lookup"><span data-stu-id="c48c1-239">Additional user data is passed back in the **ExtraData** property of the **AuthenticationResult** object that is returned from the **VerifyAuthentication** method.</span></span> <span data-ttu-id="c48c1-240">Facebook 클라이언트에 다음 값이 포함 된 **ExtraData** 속성:</span><span class="sxs-lookup"><span data-stu-id="c48c1-240">The Facebook client contains the following values in the **ExtraData** property:</span></span>

- <span data-ttu-id="c48c1-241">ID</span><span class="sxs-lookup"><span data-stu-id="c48c1-241">id</span></span>
- <span data-ttu-id="c48c1-242">name</span><span class="sxs-lookup"><span data-stu-id="c48c1-242">name</span></span>
- <span data-ttu-id="c48c1-243">선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-243">link</span></span>
- <span data-ttu-id="c48c1-244">성별</span><span class="sxs-lookup"><span data-stu-id="c48c1-244">gender</span></span>
- <span data-ttu-id="c48c1-245">accesstoken</span><span class="sxs-lookup"><span data-stu-id="c48c1-245">accesstoken</span></span>

<span data-ttu-id="c48c1-246">다른 공급자 ExtraData 속성에서 비슷하지만 약간 다른 데이터를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-246">Other providers will have similar but slightly different data in the ExtraData property.</span></span>

<span data-ttu-id="c48c1-247">사용자가 처음 사용 하 여 사이트에 일부 추가 데이터를 검색 및 확인 뷰에 해당 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-247">If the user is new to your site, you will retrieve some the additional data and pass that data to the confirmation view.</span></span> <span data-ttu-id="c48c1-248">메서드의 코드에서에서의 마지막 블록에는 사용자가 사이트를 처음 사용 하는 경우에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-248">The last block of code in the method is run only if the user is new to your site.</span></span> <span data-ttu-id="c48c1-249">다음 줄을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-249">Replace the following line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

<span data-ttu-id="c48c1-250">줄이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-250">With this line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

<span data-ttu-id="c48c1-251">이 변경에 FullName 및 링크 속성에 대 한 값만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-251">This change merely includes values for the FullName and Link properties.</span></span>

<span data-ttu-id="c48c1-252">에 **ExternalLoginConfirmation** 메서드를 코드 강조 표시 된 대로 추가 사용자 정보를 저장 하려면 아래를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-252">In the **ExternalLoginConfirmation** method, modify the code as highlighted below to save the additional user information.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a><span data-ttu-id="c48c1-253">보기 조정</span><span class="sxs-lookup"><span data-stu-id="c48c1-253">Adjusting the view</span></span>

<span data-ttu-id="c48c1-254">공급자에서 검색 하는 추가 사용자 데이터 등록 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-254">The additional user data that you retrieve from the provider will be displayed in the registration page.</span></span>

<span data-ttu-id="c48c1-255">에 **뷰**/**계정** 폴더를 엽니다 **ExternalLoginConfirmation.cshtml**합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-255">In the **Views**/**Account** folder, open **ExternalLoginConfirmation.cshtml**.</span></span> <span data-ttu-id="c48c1-256">사용자 이름에 대 한 기존 필드 아래 FullName, 링크 및 PictureLink에 대 한 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-256">Below the existing field for user name, add fields for FullName, Link, and PictureLink.</span></span>

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

<span data-ttu-id="c48c1-257">응용 프로그램을 실행 하 고 저장 한 추가 정보를 새 사용자 등록 거의 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-257">You are now almost ready to run the application and register a new user with the additional information saved.</span></span> <span data-ttu-id="c48c1-258">사이트에 등록 되지 않은 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-258">You must have an account that is not already registered with the site.</span></span> <span data-ttu-id="c48c1-259">다른 테스트 계정을 사용 하거나 행을 삭제할 수는 **UserProfile** 및 **웹 페이지\_OAuthMembership** 테이블을 다시 사용 하려는 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-259">You can either use a different test account, or delete the rows in the **UserProfile** and **webpages\_OAuthMembership** tables for the account you wish to reuse.</span></span> <span data-ttu-id="c48c1-260">이러한 행을 삭제 하 여 계정을 다시 등록 되어 있는지 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-260">By deleting those rows, you will ensure that the account is registered again.</span></span>

<span data-ttu-id="c48c1-261">응용 프로그램을 실행 하 고 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-261">Run the application and register the new user.</span></span> <span data-ttu-id="c48c1-262">이 시간 확인 페이지에 더 많은 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-262">Notice that this time the confirmation page contains more values.</span></span>

![register](using-oauth-providers-with-mvc/_static/image12.png)

<span data-ttu-id="c48c1-264">등록을 완료 한 후 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-264">After completing registration, close the browser.</span></span> <span data-ttu-id="c48c1-265">데이터베이스에 새 값이 표시를 찾는 위치는 **ExtraUserInformation** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-265">Look in the database to notice the new values in the **ExtraUserInformation** table.</span></span>

## <a name="install-nuget-package-for-facebook-api"></a><span data-ttu-id="c48c1-266">Facebook API에 대 한 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-266">Install NuGet package for Facebook API</span></span>

<span data-ttu-id="c48c1-267">Facebook에서 제공 된 [API](https://developers.facebook.com/docs/reference/apis/) 작업을 수행 하려면 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-267">Facebook provides an [API](https://developers.facebook.com/docs/reference/apis/) that you can call to perform operations.</span></span> <span data-ttu-id="c48c1-268">HTTP 요청을 보내 전달 하거나 해당 요청을 보내는 용이 하 게 하는 NuGet 패키지 설치를 사용 하 여 Facebook API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-268">You can call the Facebook API either by directing sending HTTP requests, or by using installing a NuGet package that facilitates sending those requests.</span></span> <span data-ttu-id="c48c1-269">이 자습서에 표시 되는 NuGet 패키지를 사용 하 여 하지만 NuGet 설치 패키지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-269">Using a NuGet package is shown in this tutorial, but installing NuGet package is not essential.</span></span> <span data-ttu-id="c48c1-270">이 자습서에서는 Facebook C# SDK 패키지를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-270">This tutorial shows how to use the Facebook C# SDK package.</span></span> <span data-ttu-id="c48c1-271">Facebook API 호출을 지원 하기 위해 다른 NuGet 패키지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-271">There are other NuGet packages that assist with calling the Facebook API.</span></span>

<span data-ttu-id="c48c1-272">**NuGet 패키지 관리** 창 Facebook C# SDK 패키지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-272">From the **Manage NuGet Packages** windows, select the Facebook C# SDK package.</span></span>

![패키지 설치](using-oauth-providers-with-mvc/_static/image13.png)

<span data-ttu-id="c48c1-274">사용자에 대 한 액세스 토큰을 필요로 하는 작업을 호출 하는 Facebook C# SDK를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-274">You will use the Facebook C# SDK to call an operation that requires the access token for the user.</span></span> <span data-ttu-id="c48c1-275">다음 섹션에는 액세스 토큰을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-275">The next section shows how to get the access token.</span></span>

## <a name="retrieve-access-token"></a><span data-ttu-id="c48c1-276">액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-276">Retrieve access token</span></span>

<span data-ttu-id="c48c1-277">대부분의 외부 공급자 사용자의 자격 증명이 확인 된 후에 액세스 토큰 다시 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-277">Most external providers pass back an access token after the user's credentials are verified.</span></span> <span data-ttu-id="c48c1-278">이 액세스 토큰을 사용 하면만 인증 된 사용자에 게 사용할 수 있는 작업을 호출할 수 있기 때문에 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-278">This access token is very important because it enables you to call operations that are only available to authenticated users.</span></span> <span data-ttu-id="c48c1-279">따라서 검색 하 고 액세스 토큰을 저장이 필수적 더 많은 기능을 제공 하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-279">Therefore, retrieving and storing the access token is essential when you want to provide more functionality.</span></span>

<span data-ttu-id="c48c1-280">외부 공급자에 따라 제한 된 양의 시간에 대 한 액세스 토큰 유효할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-280">Depending on the external provider, the access token may be valid for only a limited amount of time.</span></span> <span data-ttu-id="c48c1-281">유효한 액세스 토큰을 확보 됩니다 검색 하는 사용자, 로그인 및 세션 값으로 저장 하지 않고 데이터베이스에 저장 될 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-281">To ensure that you have a valid access token, you will retrieve it each time the user logs in, and store it as a session value rather than save it to a database.</span></span>

<span data-ttu-id="c48c1-282">에 **ExternalLoginCallback** 메서드, 액세스 토큰이 다시 전달 되는 **ExtraData** 속성의는 **AuthenticationResult** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-282">In the **ExternalLoginCallback** method, the access token is also passed back in the **ExtraData** property of the **AuthenticationResult** object.</span></span> <span data-ttu-id="c48c1-283">강조 표시 된 코드를 추가 **ExternalLoginCallback** 에서 액세스 토큰을 저장 하는 **세션** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-283">Add the highlighted code to **ExternalLoginCallback** to save the access token in the **Session** object.</span></span> <span data-ttu-id="c48c1-284">이 코드는 사용자가 Facebook 계정으로 로그온 할 때마다 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-284">This code is run every time the user logs in with a Facebook account.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

<span data-ttu-id="c48c1-285">이 예제에서는 facebook에서 액세스 토큰을 가져오고, 있지만 검색할 수 있습니다 액세스 토큰 외부 공급자에서 명명 된 동일한 키를 통해 &quot;accesstoken&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-285">Although this example retrieves an access token from Facebook, you can retrieve the access token from any external provider through the same key named &quot;accesstoken&quot;.</span></span>

## <a name="logging-off"></a><span data-ttu-id="c48c1-286">로그오프</span><span class="sxs-lookup"><span data-stu-id="c48c1-286">Logging off</span></span>

<span data-ttu-id="c48c1-287">기본 **로그 오프** 메서드가 응용 프로그램의 사용자를 로그 했지만 외부 공급자에서 사용자를 기록 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-287">The default **LogOff** method logs the user out of your application, but does not log the user out of the external provider.</span></span> <span data-ttu-id="c48c1-288">로그 아웃 Facebook, 토큰 사용자가 로그 오프 한 후 지속 되지 않도록을 강조 표시 된 다음 코드를 추가할 수 있습니다는 **로그 오프** 메서드는 AccountController에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-288">To log the user out of Facebook, and prevent the token from persisting after the user has logged off, you can add the following highlighted code to the **LogOff** method in the AccountController.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

<span data-ttu-id="c48c1-289">제공 하는 값은 `next` 매개 변수는 Facebook에서 사용자가 로그인 한 후 사용할 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-289">The value you provide in the `next` parameter is the URL to use after the user has logged out of Facebook.</span></span> <span data-ttu-id="c48c1-290">로컬 컴퓨터를 테스트할 때는 로컬 사이트에 대 한 올바른 포트 번호를 제공할 것 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-290">When testing on your local computer, you would provide the correct port number for your local site.</span></span> <span data-ttu-id="c48c1-291">프로덕션 환경에서 contoso.com 등의 기본 페이지에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-291">In production, you would provide a default page, such as contoso.com.</span></span>

## <a name="retrieve-user-information-that-requires-the-access-token"></a><span data-ttu-id="c48c1-292">액세스 토큰을 필요로 하는 사용자 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-292">Retrieve user information that requires the access token</span></span>

<span data-ttu-id="c48c1-293">액세스 토큰을 저장 하 고 Facebook C# SDK 패키지를 설치 했으므로 Facebook에서 추가 사용자 정보를 요청 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-293">Now that you have stored the access token and installed the Facebook C# SDK package, you can use them together to request additional user information from Facebook.</span></span> <span data-ttu-id="c48c1-294">에 **ExternalLoginConfirmation** 메서드를의 인스턴스를 만들고는 **FacebookClient** 액세스 토큰의 값을 전달 하 여 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-294">In the **ExternalLoginConfirmation** method, create an instance of the **FacebookClient** class by passing the value of the access token.</span></span> <span data-ttu-id="c48c1-295">값을 요청 된 **확인** 현재 인증 된 사용자에 대 한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-295">Request the value of the **verified** property for the current, authenticated user.</span></span> <span data-ttu-id="c48c1-296">**확인** 속성은 Facebook가 휴대 전화에 메시지를 보내는 등의 다른 수단을 통해 계정 확인 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-296">The **verified** property indicates whether Facebook has validated the account through some other means, such as sending a message to a cell phone.</span></span> <span data-ttu-id="c48c1-297">데이터베이스에이 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-297">Save this value in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

<span data-ttu-id="c48c1-298">다시 사용자에 대 한 데이터베이스의 레코드를 삭제 하거나 다른 Facebook 계정을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-298">You will again need to either delete the records in the database for the user, or use a different Facebook account.</span></span>

<span data-ttu-id="c48c1-299">응용 프로그램을 실행 하 고 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-299">Run the application, and register the new user.</span></span> <span data-ttu-id="c48c1-300">살펴보고는 **ExtraUserInformation** 표 확인 됨 속성에 대 한 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-300">Look at the **ExtraUserInformation** table to see the value for the Verified property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c48c1-301">결론</span><span class="sxs-lookup"><span data-stu-id="c48c1-301">Conclusion</span></span>

<span data-ttu-id="c48c1-302">이 자습서에서는 사용자 인증 및 등록 데이터에 대 한 Facebook과 통합 된 사이트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-302">In this tutorial, you created a site that is integrated with Facebook for user authentication and registration data.</span></span> <span data-ttu-id="c48c1-303">MVC 4 웹 응용 프로그램 및 해당 기본 동작을 사용자 지정 하는 방법에 대해 설정 된 기본 동작에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c48c1-303">You learned about the default behavior that is set up for MVC 4 web application, and how to customize that default behavior.</span></span>

## <a name="related-topics"></a><span data-ttu-id="c48c1-304">관련 항목</span><span class="sxs-lookup"><span data-stu-id="c48c1-304">Related topics</span></span>

- [<span data-ttu-id="c48c1-305">ASP.NET MVC 응용 프로그램 인증 및 SQL DB 만들기 및 Azure 앱 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="c48c1-305">Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service</span></span>](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
