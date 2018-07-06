---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: 페이지 (Razor) 사이트를 외부 ASP.NET 웹 사이트를 사용 하 여 로그인 합니다. | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 Facebook, Google, Twitter, Yahoo 및 다른 사이트를 사용 하 여 ASP.NET Web Pages (Razor) 사이트에 로그인 하는 방법에 설명-즉, 지 원하는 방법...
ms.author: aspnetcontent
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: e6c5b578b4c74fd04136d31751d51b59ba9197ba
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825439"
---
<a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="68362-103">외부 사이트를 사용 하 여 ASP.NET 웹 페이지 (Razor) 사이트에 로그인</span><span class="sxs-lookup"><span data-stu-id="68362-103">Logging In Using External Sites in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="68362-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="68362-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="68362-105">이 문서에서는 Facebook, Google, Twitter, Yahoo 및 다른 사이트를 사용 하 여 ASP.NET Web Pages (Razor) 사이트에 로그인 하는 방법에 설명-즉, OAuth 및 OpenID 사이트에서 지 원하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-105">This article explains how to log in to your ASP.NET Web Pages (Razor) site using Facebook, Google, Twitter, Yahoo, and other sites — that is, how to support OAuth and OpenID in your site.</span></span>
> 
> <span data-ttu-id="68362-106">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="68362-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="68362-107">WebMatrix 시작 사이트 템플릿을 사용 하 여 다른 사이트에서 로그인을 사용 하도록 설정 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="68362-107">How to enable login from other sites when you use the WebMatrix Starter Site template.</span></span>
> 
> <span data-ttu-id="68362-108">문서에 도입 된 ASP.NET 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-108">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="68362-109">`OAuthWebSecurity` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-109">The `OAuthWebSecurity` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="68362-110">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="68362-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="68362-111">ASP.NET Web Pages (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="68362-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="68362-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="68362-112">WebMatrix 3</span></span>

<span data-ttu-id="68362-113">ASP.NET 웹 페이지에 대 한 지원도 [OAuth](http://oauth.net/) 하 고 [OpenID](http://openid.net/) 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-113">ASP.NET Web Pages includes support for [OAuth](http://oauth.net/) and [OpenID](http://openid.net/) providers.</span></span> <span data-ttu-id="68362-114">이러한 공급자를 사용 하 여, Facebook, Twitter, Microsoft 및 Google에서 자신의 기존 자격 증명을 사용 하 여 사이트에 사용자가 로그인을 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-114">Using these providers, you can let users log into your site using their existing credentials from Facebook, Twitter, Microsoft, and Google.</span></span> <span data-ttu-id="68362-115">예를 들어 Facebook 계정을 사용 하 여 로그인 하려면 사용자만 선택할 수 Facebook 아이콘을 사용자 정보를 입력할 있습니다 Facebook 로그인 페이지로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-115">For example, to log in using a Facebook account, users can just choose a Facebook icon, which redirects them to the Facebook login page where they enter their user information.</span></span> <span data-ttu-id="68362-116">그런 다음 사이트에서 자신의 계정으로 Facebook 로그인을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-116">They can then associate the Facebook login with their account on your site.</span></span> <span data-ttu-id="68362-117">웹 사이트에서 단일 계정을 사용 하 여 웹 페이지 멤버 자격 기능에 관련 된 향상 기능을는 사용자가 여러 번의 로그인 (소셜 네트워킹 사이트에서의 로그인 포함)를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-117">A related enhancement to the Web Pages membership features is that users can associate multiple logins (including logins from social networking sites) with a single account on your website.</span></span>

<span data-ttu-id="68362-118">이 이미지에서 로그인 페이지를 표시 합니다 **시작 사이트** 템플릿을, 사용자가 외부 계정의 로그인을 사용 하도록 설정 하려면 Facebook, Twitter, Google 또는 Microsoft 아이콘을 선택할 수 있는:</span><span class="sxs-lookup"><span data-stu-id="68362-118">This image shows the Login page from the **Starter Site** template, where a user can choose a Facebook, Twitter, Google or Microsoft icon to enable logging in with an external account:</span></span>

![외부 공급자](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

<span data-ttu-id="68362-120">몇 줄의 코드의 주석 처리를 제거 하 여 OAuth 및 OpenID 멤버 자격을 사용할 수 있습니다 합니다 **시작 사이트** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="68362-120">You can enable OAuth and OpenID membership by uncommenting a few lines of code in the **Starter Site** template.</span></span> <span data-ttu-id="68362-121">메서드 및 속성을 사용 하 여 OAuth를 사용 하 여 작업을 OpenID 공급자에는 `WebMatrix.Security.OAuthWebSecurity` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-121">The methods and properties you use to work with the OAuth and OpenID providers are in the `WebMatrix.Security.OAuthWebSecurity` class.</span></span> <span data-ttu-id="68362-122">합니다 **시작 사이트** 템플릿은 정식 멤버 자격 인프라를 포함 하면 로그인 페이지, 멤버 자격 데이터베이스 및 모든 코드를 사용 하 여 전체 로컬 자격 증명 또는 다른 사이트에서 해당 항목을 사용 하 여 사이트에 사용자가 로그인 수 .</span><span class="sxs-lookup"><span data-stu-id="68362-122">The **Starter Site** template includes a full membership infrastructure, complete with a login page, a membership database, and all the code you need to let users log into your site using either local credentials or those from another site.</span></span>

<span data-ttu-id="68362-123">이 섹션에서는 사용자를 기반으로 하는 사이트 외부 사이트에서 로그인 하는 방법의 예제를 제공 합니다 **시작 사이트** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="68362-123">This section provides an example of how to let users log in from external sites to a site that's based on the **Starter Site** template.</span></span> <span data-ttu-id="68362-124">시작 사이트를 만든 후 (세부 정보 수행) 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-124">After creating a starter site, you do this (details follow):</span></span>

- <span data-ttu-id="68362-125">OAuth 공급자 (Facebook, Twitter 및 Microsoft)를 사용 하는 사이트, 외부 사이트에서 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68362-125">For the sites that use an OAuth provider (Facebook, Twitter, and Microsoft), you create an application on the external site.</span></span> <span data-ttu-id="68362-126">이렇게 하면 해당 사이트에 대 한 로그인 기능을 호출 하기 위해 해야 하는 응용 프로그램 키입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-126">This gives you application keys that you'll need in order to invoke the login feature for those sites.</span></span>
- <span data-ttu-id="68362-127">OpenID 공급자 (Google)를 사용 하는 사이트에 대 한 응용 프로그램을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-127">For sites that use an OpenID provider (Google), you do not have to create an application.</span></span> <span data-ttu-id="68362-128">이러한 사이트의 모든 로그인 하 고 개발자 응용 프로그램을 만들려면 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-128">For all of these sites, you must have an account in order to log in and to create developer applications.</span></span>

    > [!NOTE]
    > <span data-ttu-id="68362-129">Microsoft 응용 프로그램 작업 웹 사이트에 대 한 라이브 URL에만 동의 로그인 테스트를 위해 로컬 웹 사이트 URL을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-129">Microsoft applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>
- <span data-ttu-id="68362-130">사용 하려는 사이트에 로그인을 제출 하 고 적절 한 인증 공급자를 지정 하기 위해 웹 사이트에서 몇 가지 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-130">Edit a few files in your website in order to specify the appropriate authentication provider and to submit a login to the site you want to use.</span></span>

<span data-ttu-id="68362-131">이 문서에서는 다음 작업에 대 한 별도 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-131">This article provides separate instructions for the following tasks:</span></span>

- [<span data-ttu-id="68362-132">Google 로그인을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="68362-132">Enabling Google logins</span></span>](#To_enable_Google_logins)
- [<span data-ttu-id="68362-133">Facebook 로그인을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="68362-133">Enabling Facebook logins</span></span>](#To_enable_Facebook_logins)
- [<span data-ttu-id="68362-134">Twitter 로그인을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="68362-134">Enabling Twitter logins</span></span>](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a><span data-ttu-id="68362-135">Google 로그인을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="68362-135">Enabling Google Logins</span></span>

1. <span data-ttu-id="68362-136">WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 열거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68362-136">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="68362-137">엽니다는  *\_AppStart.cshtml* 페이지 및 코드의 다음 줄을 주석 처리 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-137">Open the *\_AppStart.cshtml* page and uncomment the following line of code.</span></span> 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a><span data-ttu-id="68362-138">Google 로그인 테스트</span><span class="sxs-lookup"><span data-stu-id="68362-138">Testing Google login</span></span>

1. <span data-ttu-id="68362-139">실행 합니다 *default.cshtml* 사이트의 페이지 선택 합니다 **로그인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-139">Run the *default.cshtml* page of your site and choose the **Log in** button.</span></span>
2. <span data-ttu-id="68362-140">에 *로그인* 페이지를 **다른 서비스를 사용 하 여 로그인** 섹션 중 하나를 선택 합니다 **Google** 또는 **Yahoo** 제출 단추.</span><span class="sxs-lookup"><span data-stu-id="68362-140">On the *Login* page, in the **Use another service to log in** section, choose either the **Google** or **Yahoo** submit button.</span></span> <span data-ttu-id="68362-141">이 예제에서는 Google 로그인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-141">This example uses the Google login.</span></span> 

    <span data-ttu-id="68362-142">웹 페이지는 Google 로그인 페이지로 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-142">The web page redirects the request to the Google login page.</span></span>

    ![Google 로그인](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. <span data-ttu-id="68362-144">기존 Google 계정 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-144">Enter credentials for an existing Google account.</span></span>
4. <span data-ttu-id="68362-145">Google 묻는 허용 것인지 *Localhost* 계정에서 정보를 사용 하려면 **허용**합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-145">If Google asks you whether you want to allow *Localhost* to use information from the account, click **Allow**.</span></span>

    <span data-ttu-id="68362-146">코드를 Google 토큰을 사용 하 여 사용자를 인증 하 고 웹 사이트에이 페이지에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-146">The code uses the Google token to authenticate the user, and then returns to this page on your website.</span></span> <span data-ttu-id="68362-147">이 페이지에서는 사용자가 Google 로그인을 웹 사이트에서 기존 계정을 연결 하거나 사용한 외부 로그인을 연결할 사이트에서 새 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-147">This page lets users associate their Google login with an existing account on your website, or they can register a new account on your site to associate the external login with.</span></span>

    ![oauth 5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. <span data-ttu-id="68362-149">선택 된 **연결** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-149">Choose the **Associate** button.</span></span> <span data-ttu-id="68362-150">브라우저 응용 프로그램의 홈 페이지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-150">The browser returns to your application's home page.</span></span>

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a><span data-ttu-id="68362-151">Facebook 로그인을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="68362-151">Enabling Facebook Logins</span></span>

1. <span data-ttu-id="68362-152">로 이동 합니다 [Facebook 개발자 사이트](https://developers.facebook.com/apps) (로그인 하는 아직 로그인 하지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="68362-152">Go to the [Facebook developers site](https://developers.facebook.com/apps) (log in if you're not already logged in).</span></span>
2. <span data-ttu-id="68362-153">선택 합니다 **Create New App** 단추를 클릭 한 다음 새 응용 프로그램을 만들고 이름을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="68362-153">Choose the **Create New App** button, and then follow the prompts to name and create the new application.</span></span>
3. <span data-ttu-id="68362-154">단원의 **앱은 Facebook에 통합할 방법을 선택**를 선택 합니다 **웹 사이트** 섹션.</span><span class="sxs-lookup"><span data-stu-id="68362-154">In the section **Select how your app will integrate with Facebook**, choose the **Website** section.</span></span>
4. <span data-ttu-id="68362-155">입력 합니다 **사이트 URL** 사이트의 URL을 사용 하 여 필드 (예를 들어 `http://www.example.com`).</span><span class="sxs-lookup"><span data-stu-id="68362-155">Fill in the **Site URL** field with the URL of your site (for example, `http://www.example.com`).</span></span> <span data-ttu-id="68362-156">합니다 **도메인** 필드는 선택 사항 이지만 전체 도메인에 대 한 인증을 제공 하는 데 사용할 수 있습니다 (같은 *example.com*).</span><span class="sxs-lookup"><span data-stu-id="68362-156">The **Domain** field is optional; you can use this to provide authentication for an entire domain (such as *example.com*).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="68362-157">사이트 URL 사용 하 여 로컬 컴퓨터에서 실행 하는 경우와 같은 `http://localhost:12345` (여기서 번호는 로컬 포트 번호는)이이 값을 추가할 수 있습니다 합니다 **사이트 URL** 사이트 테스트에 대 한 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-157">If you are running a site on your local computer with a URL like `http://localhost:12345` (where the number is a local port number), you can add this value to the **Site URL** field for testing your site.</span></span> <span data-ttu-id="68362-158">그러나 언제 든 지 변경 내용을 로컬 사이트의 포트 번호를 업데이트 해야 합니다 **사이트 URL** 응용 프로그램의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-158">However, any time the port number of your local site changes, you will need to update the **Site URL** field of your application.</span></span>
5. <span data-ttu-id="68362-159">선택 된 **변경 내용 저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-159">Choose the **Save Changes** button.</span></span>
6. <span data-ttu-id="68362-160">선택 된 **앱** 다시 탭 한 다음 응용 프로그램에 대 한 시작 페이지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-160">Choose the **Apps** tab again, and then view the start page for your application.</span></span>
7. <span data-ttu-id="68362-161">복사 합니다 **앱 ID** 하 고 **앱 비밀** 응용 프로그램에 대 한 값 임시 텍스트 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-161">Copy the **App ID** and **App Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="68362-162">Facebook 공급자에 게 웹 사이트 코드에서 이러한 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-162">You will pass these values to the Facebook provider in your website code.</span></span>
8. <span data-ttu-id="68362-163">Facebook 개발자 사이트를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-163">Exit the Facebook developer site.</span></span>

<span data-ttu-id="68362-164">이제 변경 하면 두 페이지에 웹 사이트에서 사용자가 되도록 자신의 Facebook 계정을 사용 하 여 사이트에 로그인 할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68362-164">Now you make changes to two pages in your website so that users will able to log into the site using their Facebook accounts.</span></span>

1. <span data-ttu-id="68362-165">WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 열거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68362-165">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="68362-166">엽니다는  *\_AppStart.cshtml* 페이지 및 Facebook OAuth 공급자에 대 한 코드 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-166">Open the *\_AppStart.cshtml* page and uncomment the code for the Facebook OAuth provider.</span></span> <span data-ttu-id="68362-167">주석 처리가 제거 된 코드 블록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-167">The uncommented code block looks like the following:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. <span data-ttu-id="68362-168">복사 합니다 **앱 ID** 값으로 Facebook 응용 프로그램에서 값을 `appId` (따옴표 포함) 내부 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-168">Copy the **App ID** value from the Facebook application as the value of the `appId` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="68362-169">복사본 **앱 비밀** Facebook 응용 프로그램에서 값을 `appSecret` 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-169">Copy **App Secret** value from the Facebook application as the `appSecret` parameter value.</span></span>
5. <span data-ttu-id="68362-170">파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-170">Save and close the file.</span></span>

### <a name="testing-facebook-login"></a><span data-ttu-id="68362-171">Facebook 로그인 테스트</span><span class="sxs-lookup"><span data-stu-id="68362-171">Testing Facebook login</span></span>

1. <span data-ttu-id="68362-172">사이트의를 실행 *default.cshtml* 선택한 페이지의 **로그인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-172">Run the site's *default.cshtml* page and choose the **Login** button.</span></span>
2. <span data-ttu-id="68362-173">에 *로그인* 페이지를 **다른 서비스를 사용 하 여 로그인** 섹션을 선택 합니다 **Facebook** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-173">On the *Login* page, in the **Use another service to log in** section, choose the **Facebook** icon.</span></span> 

    <span data-ttu-id="68362-174">웹 페이지는 Facebook 로그인 페이지로 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-174">The web page redirects the request to the Facebook login page.</span></span>

    ![oauth 2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. <span data-ttu-id="68362-176">Facebook 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-176">Log into a Facebook account.</span></span> 

    <span data-ttu-id="68362-177">코드는 Facebook 토큰을 사용 하 여 사용자 인증을 위해를 페이지에 반환 합니다 사이트의 로그인을 사용 하 여 Facebook 로그인을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-177">The code uses the Facebook token to authenticate you and then returns to a page where you can associate your Facebook login with your site's login.</span></span> <span data-ttu-id="68362-178">사용자 이름 또는 전자 메일 주소에 채워집니다 합니다 **전자 메일** 양식의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-178">Your user name or email address is filled into the **Email** field on the form.</span></span>

    ![oauth 5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. <span data-ttu-id="68362-180">선택 된 **연결** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-180">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="68362-181">브라우저 홈 페이지로 돌아가고에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68362-181">The browser returns to the home page and you are logged in.</span></span>

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a><span data-ttu-id="68362-182">Twitter 로그인을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="68362-182">Enabling Twitter Logins</span></span>

1. <span data-ttu-id="68362-183">로 이동 합니다 [Twitter 개발자 사이트](https://dev.twitter.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-183">Browse to the [Twitter developers site](https://dev.twitter.com/).</span></span>
2. <span data-ttu-id="68362-184">선택 합니다 **앱 만들기** 에 연결 하 고 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-184">Choose the **Create an App** link and then log into the site.</span></span>
3. <span data-ttu-id="68362-185">에 **응용 프로그램을 만듭니다** 양식에서 입력 합니다 **이름** 및 **설명** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-185">On the **Create an Application** form, fill in the **Name** and **Description** fields.</span></span>
4. <span data-ttu-id="68362-186">에 **웹 사이트** 필드에 사이트의 URL을 입력 합니다 (예를 들어 `http://www.example.com`).</span><span class="sxs-lookup"><span data-stu-id="68362-186">In the **WebSite** field, enter the URL of your site (for example, `http://www.example.com`).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="68362-187">로컬 사이트를 테스트 하는 경우 (같은 URL을 사용 하 여 `http://localhost:12345`), Twitter URL을 허용 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-187">If you're testing your site locally (using a URL like `http://localhost:12345`), Twitter might not accept the URL.</span></span> <span data-ttu-id="68362-188">그러나 로컬 루프백 IP 주소를 사용할 수 있습니다 (예를 들어 `http://127.0.0.1:12345`).</span><span class="sxs-lookup"><span data-stu-id="68362-188">However, you might be able to use the local loopback IP address (for example `http://127.0.0.1:12345`).</span></span> <span data-ttu-id="68362-189">이 응용 프로그램을 로컬로 테스트 하는 과정을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-189">This simplifies the process of testing your application locally.</span></span> <span data-ttu-id="68362-190">그러나 로컬 사이트의 포트 번호를 변경할 때마다 있습니다 업데이트 해야 합니다 **웹 사이트** 응용 프로그램의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-190">However, every time the port number of your local site changes, you'll need to update the **WebSite** field of your application.</span></span>
5. <span data-ttu-id="68362-191">에 **콜백 URL** 필드, 사용자가 Twitter로 로그인 한 후에 반환 하려는 웹 사이트의 페이지에 대 한 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-191">In the **Callback URL** field, enter a URL for the page in your website that you want users to return to after logging into Twitter.</span></span> <span data-ttu-id="68362-192">예를 들어, 시작 사이트 (해당 로그인 상태 인식)의 홈 페이지에 사용자를 보낼에 입력 된 동일한 URL을 입력 합니다 **웹 사이트** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-192">For example, to send users to the home page of the Starter Site (which will recognize their logged-in status), enter the same URL that you entered in the **WebSite** field.</span></span>
6. <span data-ttu-id="68362-193">선택한 조건에 동의 합니다 **Twitter 응용 프로그램을 만드는** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-193">Accept the terms and choose the **Create your Twitter application** button.</span></span>
7. <span data-ttu-id="68362-194">에 **내 응용 프로그램** 방문 페이지에서 만든 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-194">On the **My Applications** landing page, choose the application you created.</span></span>
8. <span data-ttu-id="68362-195">에 **세부 정보** 탭, 아래쪽으로 스크롤하여 선택한 합니다 **내 액세스 토큰 만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-195">On the **Details** tab, scroll to the bottom and choose the **Create My Access Token** button.</span></span>
9. <span data-ttu-id="68362-196">에 **세부 정보** 탭에서 복사 합니다 **소비자 키** 및 **Consumer Secret** 응용 프로그램에 대 한 값 임시 텍스트 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-196">On the **Details** tab, copy the **Consumer Key** and **Consumer Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="68362-197">웹 사이트 코드에서 Twitter 공급자에 이러한 값을 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68362-197">You'll pass these values to the Twitter provider in your website code.</span></span>
10. <span data-ttu-id="68362-198">Twitter 사이트를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-198">Exit the Twitter site.</span></span>

<span data-ttu-id="68362-199">이제 변경한 두 페이지에 웹 사이트에서 사용자가 Twitter 계정을 사용 하 여 사이트에 로그인 할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-199">Now you make changes to two pages in your website so that users will be able to log into the site using their Twitter accounts.</span></span>

1. <span data-ttu-id="68362-200">WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 열거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68362-200">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="68362-201">엽니다는  *\_AppStart.cshtml* 페이지 및 Twitter OAuth 공급자에 대 한 코드 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-201">Open the *\_AppStart.cshtml* page and uncomment the code for the Twitter OAuth provider.</span></span> <span data-ttu-id="68362-202">주석 처리가 제거 된 코드 블록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-202">The uncommented code block looks like this:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. <span data-ttu-id="68362-203">복사 합니다 **소비자 키** 값으로 Twitter 응용 프로그램에서 값을 `consumerKey` (따옴표 포함) 내부 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-203">Copy the **Consumer Key** value from the Twitter application as the value of the `consumerKey` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="68362-204">복사 합니다 **Consumer Secret** 값으로 Twitter 응용 프로그램에서 값을 `consumerSecret` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-204">Copy the **Consumer Secret** value from the Twitter application as the value of the `consumerSecret` parameter.</span></span>
5. <span data-ttu-id="68362-205">파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="68362-205">Save and close the file.</span></span>

### <a name="testing-twitter-login"></a><span data-ttu-id="68362-206">Twitter 로그인 테스트</span><span class="sxs-lookup"><span data-stu-id="68362-206">Testing Twitter login</span></span>

1. <span data-ttu-id="68362-207">실행 합니다 *default.cshtml* 사이트의 페이지 선택 합니다 **로그인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-207">Run the *default.cshtml* page of your site and choose the **Login** button.</span></span>
2. <span data-ttu-id="68362-208">에 *로그인* 페이지를 **다른 서비스를 사용 하 여 로그인** 섹션을 선택 합니다 **Twitter** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-208">On the *Login* page, in the **Use another service to log in** section, choose the **Twitter** icon.</span></span> 

    <span data-ttu-id="68362-209">웹 페이지 요청을 만든 응용 프로그램에 대 한 Twitter 로그인 페이지로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-209">The web page redirects the request to a Twitter login page for the application you created.</span></span>

    ![oauth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. <span data-ttu-id="68362-211">Twitter 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-211">Log into a Twitter account.</span></span>
4. <span data-ttu-id="68362-212">코드는 Twitter 토큰을 사용 하 여 사용자를 인증 하 하 고 돌아갑니다 페이지로 연결할 수 있습니다 웹 사이트 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68362-212">The code uses the Twitter token to authenticate the user and then returns you to a page where you can associate your login with your website account.</span></span> <span data-ttu-id="68362-213">사용자 이름 또는 전자 메일 주소에 채워집니다 합니다 **전자 메일** 양식의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-213">Your name or email address is filled into the **Email** field on the form.</span></span>

    ![oauth 5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. <span data-ttu-id="68362-215">선택 된 **연결** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68362-215">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="68362-216">브라우저 홈 페이지로 돌아가고에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68362-216">The browser returns to the home page and you are logged in.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="68362-217">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="68362-217">Additional Resources</span></span>


- [<span data-ttu-id="68362-218">사이트 전체 동작 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="68362-218">Customizing Site-Wide Behavior</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="68362-219">ASP.NET 웹 페이지 사이트에 보안 및 멤버 자격 추가</span><span class="sxs-lookup"><span data-stu-id="68362-219">Adding Security and Membership to an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkID=202904)
