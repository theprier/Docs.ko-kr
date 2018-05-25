---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: MVC 5 만들기 Facebook, Twitter, LinkedIn 및 Google OAuth2 로그온 (C#)로 앱 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 사용자가 OAuth 2.0을 사용 하 여 외부 인증의 자격 증명으로 로그인 할 수 있는 ASP.NET MVC 5 웹 응용 프로그램을 작성 하는 방법...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/03/2015
ms.topic: article
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: c289c209b50f0c2c1f2d8b15a3aedeaebf671d0b
ms.sourcegitcommit: 24c32648ab0c6f0be15333d7c23c1bf680858c43
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2018
---
<a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="ff5e8-103">Facebook, Twitter, LinkedIn 및 Google OAuth2 로그온 (C#)으로 ASP.NET MVC 5 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ff5e8-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>
====================
<span data-ttu-id="ff5e8-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="ff5e8-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="ff5e8-105">이 자습서를 사용 하 여 사용자가 로그인 할 수 있는 ASP.NET MVC 5 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다. [OAuth 2.0](http://oauth.net/2/) 외부 인증 공급자는 Facebook, Twitter, LinkedIn, Microsoft 또는 Google 등에서 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="ff5e8-106">간단한 설명을 위해이 자습서에서는 Facebook 및 Google 자격 증명 사용에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="ff5e8-107">수백만 명 이상의 사용자 계정을 이러한 외부 공급자와 함께 이미 있기 때문에 중요 한 장점을 제공 웹 사이트에서 이러한 자격 증명을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="ff5e8-108">이러한 사용자 더 만들고 새로운 자격 증명 집합을 기억 하지 않아도 되는 경우 사이트에 대 한 등록을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="ff5e8-109">참고 항목 [SMS 및 전자 메일 2 단계 인증을 사용 하는 ASP.NET MVC 5 앱](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="ff5e8-110">또한 자습서에는 사용자에 대 한 프로필 데이터를 추가 하는 방법 및 역할을 추가 하는 멤버 API를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="ff5e8-111">이 자습서에 의해 작성 되었으므로 [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter에 따라 me: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="ff5e8-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>


<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="ff5e8-112">시작</span><span class="sxs-lookup"><span data-stu-id="ff5e8-112">Getting Started</span></span>

<span data-ttu-id="ff5e8-113">설치 하 고 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="ff5e8-114">Visual Studio 설치 [2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390521) 이상.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="ff5e8-115">이 참조에 대 한 도움말 Dropbox, GitHub, Linkedin, Instagram, 버퍼, Salesforce, 스트림을, 스택 Exchange, Tripit, Twitch, Twitter, yahoo! 등, [샘플 프로젝트](https://github.com/matthewdunsdon/oauthforaspnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="ff5e8-116">Visual Studio를 설치 해야 [2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390521) 또는 Google OAuth 2를 사용 하 고 SSL 경고 없이 로컬로 디버깅할 이상.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>


<span data-ttu-id="ff5e8-117">클릭 **새 프로젝트** 에서 **시작** 페이지 또는 있습니다 메뉴를 사용 하 고 선택할 수 **파일**, 차례로 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  
 

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="ff5e8-118">응용 프로그램 처음 만들기</span><span class="sxs-lookup"><span data-stu-id="ff5e8-118">Creating Your First Application</span></span>

<span data-ttu-id="ff5e8-119">클릭 **새 프로젝트**을 선택한 후 **Visual C#** 다음 왼쪽에 **웹** 선택한 후 **ASP.NET 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="ff5e8-120">"MvcAuth" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="ff5e8-121">에 **새 ASP.NET 프로젝트** 대화 상자를 클릭 하 여 **MVC**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="ff5e8-122">인증이 없으면 **개별 사용자 계정**, 클릭는 **인증 변경** 선택한 단추 **개별 사용자 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="ff5e8-123">확인 하 여 **클라우드의 호스트에에서**, 앱에서 Azure에서 호스팅할 매우 쉽게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="ff5e8-124">선택한 경우 **클라우드의 호스트에에서**, 구성 대화 상자를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)


### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="ff5e8-125">NuGet을 사용 하 여 최신 OWIN 미들웨어를 업데이트 하려면</span><span class="sxs-lookup"><span data-stu-id="ff5e8-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="ff5e8-126">NuGet 패키지 관리자를 사용 하 여 업데이트 하는 [OWIN 미들웨어](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="ff5e8-127">선택 **업데이트** 왼쪽된 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="ff5e8-128">클릭할 수는 **모두 업데이트** 단추나 있습니다 (다음 그림에 표시) OWIN 패키지만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="ff5e8-129">아래 이미지에는 OWIN 패키지에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="ff5e8-130">패키지 관리자 콘솔 (PMC)에서 입력할 수 있는 `Update-Package` 명령을 모든 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="ff5e8-131">키를 눌러 **F5** 또는 **Ctrl + f 5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="ff5e8-132">아래 이미지에 포트 번호가 1234입니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="ff5e8-133">응용 프로그램을 실행 하는 경우에 다른 포트 번호를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="ff5e8-134">브라우저 창의 크기에 따라 탐색 아이콘을 클릭 해야 할 수 있습니다는 **홈**, **에 대 한**, **연락처**, **등록**및 **로그인** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="ff5e8-135">프로젝트에서 SSL을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="ff5e8-136">같은 Google Facebook 인증 공급자에 연결 하려면 IIS Express SSL을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="ff5e8-137">SSL을 사용 하 여 로그인 한 후 유지 하 고 HTTP로 다시 삭제 해야로, 로그인 쿠키는 암호와 마찬가지로 사용자 이름 및 암호를으로 보내는 일반 텍스트에서 네트워크를 통해 SSL을 사용 하지 않고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="ff5e8-138">게다가 이미 수행 하는 데 핸드셰이크를 수행 하 고 (즉, HTTPS HTTP 보다 느린 있기 때문에 대량의) 채널을 보호 하는 데 시간이 MVC 파이프라인을 실행 하기 전에 현재 요청 또는 미래 확인 되지 않습니다 있으므로 로그인 한 후을 HTTP로 리디렉션 요청 훨씬 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="ff5e8-139">**솔루션 탐색기**, 클릭는 **MvcAuth** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="ff5e8-140">프로젝트 속성을 표시 하려면 F4 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="ff5e8-141">또는 **보기** 메뉴를 선택할 수 있습니다 **속성 창**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="ff5e8-142">변경 **SSL 사용 가능** True로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="ff5e8-143">SSL URL 복사 (될 `https://localhost:44300/` 다른 SSL 프로젝트 생성 하지 않는 한).</span><span class="sxs-lookup"><span data-stu-id="ff5e8-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="ff5e8-144">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **MvcAuth** 프로젝트를 마우스 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="ff5e8-145">선택 된 **웹** 탭을 클릭 한 다음에 SSL URL을 붙여는 **프로젝트 Url** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="ff5e8-146">파일 저장 합니다 (Ctl + S).</span><span class="sxs-lookup"><span data-stu-id="ff5e8-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="ff5e8-147">이 URL을 Facebook 및 Google 인증 앱을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="ff5e8-148">추가 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 특성을 `Home` 모든 요청을 요구 하도록 컨트롤러는 HTTPS를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="ff5e8-149">추가 하는 것 보다 안전한 방법은 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 응용 프로그램에는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="ff5e8-150">섹션을 참조 &quot;SSL과 인증 특성을 사용 응용 프로그램을 보호&quot; tutoral 내에서 [인증 및 SQL DB ASP.NET MVC 응용 프로그램 만들기 및 Azure 앱 서비스 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutoral [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="ff5e8-151">Home 컨트롤러의 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="ff5e8-152">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="ff5e8-153">이전에 인증서를 설치한 경우이 섹션의 나머지 부분을 건너뛰고 이동할 [OAuth 2에 대 한 Google 앱을 만들고 응용 프로그램 프로젝트에 연결할](#goog), 그렇지 않으면 자체 서명 된 신뢰 하도록 지시에 따라 IIS Express에서 생성 하는 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="ff5e8-154">읽기는 **보안 경고** 대화 상자와 클릭 **예** 나타내는 localhost 인증서를 설치 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="ff5e8-155">IE 표시는 *홈* 페이지 및 SSL 경고가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="ff5e8-156">Google Chrome 인증서도 받아들이고 경고 HTTPS 콘텐츠만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="ff5e8-157">Firefox에서 경고를 표시 하므로 인증서 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="ff5e8-158">응용 프로그램에 대해 클릭할 수 있는 안전 하 게 **위험을 이해**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="ff5e8-159">OAuth 2에 대 한 Google 앱 만들기 및 앱 프로젝트 연결</span><span class="sxs-lookup"><span data-stu-id="ff5e8-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="ff5e8-160">현재 Google OAuth 지침은 [에서 ASP.NET Core 구성 Google 인증](/aspnet/core/security/authentication/social/google-logins)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="ff5e8-161">탐색 하 고 [Google 개발자 콘솔](https://console.developers.google.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="ff5e8-162">이전 프로젝트를 만들지 않은 경우 선택 **자격 증명** 왼쪽된 탭 한 다음 선택에서 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="ff5e8-163">왼쪽된 탭에서 클릭 **자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="ff5e8-164">클릭 **자격 증명을 만들어** 다음 **OAuth 클라이언트 ID**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="ff5e8-165">에 **클라이언트 ID 만들기** 대화 상자에서 기본값을 그대로 두고 **웹 응용 프로그램** 응용 프로그램 종류에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="ff5e8-166">설정의 **권한이 JavaScript** 위에서 사용한 SSL URL 원본이 (`https://localhost:44300/` 다른 SSL 프로젝트 생성 하지 않는 한)</span><span class="sxs-lookup"><span data-stu-id="ff5e8-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="ff5e8-167">설정의 **권한이 부여 된 리디렉션 URI** 에:</span><span class="sxs-lookup"><span data-stu-id="ff5e8-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="ff5e8-168">OAuth 동의 화면 메뉴 항목을 클릭 한 다음 전자 메일 주소 및 제품 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="ff5e8-169">양식 클릭을 완료 한 경우 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="ff5e8-170">라이브러리 메뉴 항목을 클릭, 검색 **Google + API**를 클릭 한 다음 활성화 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="ff5e8-171">아래 이미지에서는 활성화 된 Api를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="ff5e8-172">Google Api API 관리자에서 참조 된 **자격 증명** 얻으려고 탭은 **클라이언트 ID**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="ff5e8-173">응용 프로그램 암호 있는 JSON 파일을 저장 하려면 다운로드 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="ff5e8-174">복사 및 붙여넣기의 **ClientId** 및 **ClientSecret** 에 `UseGoogleAuthentication` 에 있는 메서드가 *Startup.Auth.cs* 파일에 *App_Start* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="ff5e8-175">**ClientId** 및 **ClientSecret** 아래 표시 된 값은 샘플 및 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="ff5e8-176">보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="ff5e8-177">계정 및 자격 증명은 위의 예제를 단순하게 유지 하기 위해 코드에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="ff5e8-178">참조 [ASP.NET 및 Azure 앱 서비스에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="ff5e8-179">키를 눌러 **CTRL + f 5** 작성 하 고 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="ff5e8-180">클릭는 **로그인** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="ff5e8-181">아래 **다른 서비스를 사용 하 여 로그인 할**, 클릭 **Google**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="ff5e8-182">위의 단계를 수행 하지 HTTP 401 오류를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="ff5e8-183">위의 단계를 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-183">Recheck your steps above.</span></span> <span data-ttu-id="ff5e8-184">필수 설정 수행 되지 않은 경우 (예를 들어 **제품 이름**), 누락 된 항목을 추가 하 고 저장; 인증이 작동 하려면 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="ff5e8-185">자격 증명을 입력할 Google 사이트로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="ff5e8-186">자격 증명을 입력 한 후 방금 만든 웹 응용 프로그램에 권한을 부여 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="ff5e8-187">클릭 **수락**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-187">Click **Accept**.</span></span> <span data-ttu-id="ff5e8-188">이제 다시 이동 합니다는 **등록** Google 계정을 등록할 수 있는 MvcAuth 응용 프로그램의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="ff5e8-189">Gmail 계정에 사용 되는 로컬 전자 메일 등록 이름을 변경할 수 있지만 일반적으로 기본 전자 메일 별칭 (즉, 인증에 사용할 하나)을 유지 하려면.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="ff5e8-190">**등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="ff5e8-191">Facebook에서 앱을 만들기 및 앱 프로젝트에 연결</span><span class="sxs-lookup"><span data-stu-id="ff5e8-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="ff5e8-192">현재 Facebook OAuth2 인증 지침은 [구성 Facebook 인증](/aspnet/core/security/authentication/social/facebook-logins)</span><span class="sxs-lookup"><span data-stu-id="ff5e8-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<span data-ttu-id="ff5e8-193">Facebook OAuth2 인증에 대 한 Facebook에서 만드는 응용 프로그램에서 일부 설정의 프로젝트에 복사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-193">For Facebook OAuth2 authentication, you need to copy to your project some settings from an application that you create in Facebook.</span></span>

1. <span data-ttu-id="ff5e8-194">브라우저에서로 이동 [ https://developers.facebook.com/apps ](https://developers.facebook.com/apps) Facebook 자격 증명을 입력 하 여 로그인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-194">In your browser, navigate to [https://developers.facebook.com/apps](https://developers.facebook.com/apps) and log in by entering your Facebook credentials.</span></span>
2. <span data-ttu-id="ff5e8-195">Facebook 개발자 아직 등록 되지 경우 클릭 **개발자 등록** 등록 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-195">If you aren't already registered as a Facebook developer, click **Register as a Developer** and follow the directions to register.</span></span>
3. <span data-ttu-id="ff5e8-196">에 **앱** 탭을 클릭 **Create New App**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-196">On the **Apps** tab, click **Create New App**.</span></span>

    ![새 앱 만들기](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image22.png)
4. <span data-ttu-id="ff5e8-198">입력 한 **응용 프로그램 이름** 및 **범주**, 클릭 **앱 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-198">Enter an **App Name** and **Category**, then click **Create App**.</span></span>

    <span data-ttu-id="ff5e8-199">Facebook에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-199">This must be unique across Facebook.</span></span> <span data-ttu-id="ff5e8-200"><strong>앱 Namespace</strong> 앱 하는 인증에 대 한 Facebook 응용 프로그램에 액세스 하는 데 사용할 URL의 일부 (예를 들어 https://apps.facebook.com/{App Namespace}).</span><span class="sxs-lookup"><span data-stu-id="ff5e8-200">The <strong>App Namespace</strong> is the part of the URL that your App will use to access the Facebook application for authentication (for example, https://apps.facebook.com/{App Namespace}).</span></span> <span data-ttu-id="ff5e8-201">지정 하지 않으면는 <strong>앱 Namespace</strong>, <strong>앱 ID</strong> URL에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-201">If you don't specify an <strong>App Namespace</strong>, the <strong>App ID</strong> will be used for the URL.</span></span> <span data-ttu-id="ff5e8-202"><strong>앱 ID</strong> 긴 시스템에서 생성 된 번호는 다음 단계에 표시 되는입니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-202">The <strong>App ID</strong> is a long system-generated number that you will see in the next step.</span></span>

    ![새 응용 프로그램 대화 상자 만들기](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image23.png)
5. <span data-ttu-id="ff5e8-204">표준 보안 검사를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-204">Submit the standard security check.</span></span>

    ![보안 검사](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image24.png)
6. <span data-ttu-id="ff5e8-206">선택 **설정** 왼쪽된 메뉴 모음의![ Facebook 개발자의 메뉴 모음](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="ff5e8-206">Select **Settings** for the left menu bar.![Facebook Developer's menu bar](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image25.png)</span></span>
7. <span data-ttu-id="ff5e8-207">에 **기본** 페이지의 설정 섹션을 선택 **추가 플랫폼** 웹 사이트 응용 프로그램을 추가 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-207">On the **Basic** settings section of the page select **Add Platform** to specify that you are adding a website application.</span></span> <span data-ttu-id="ff5e8-208">![기본 설정](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image26.png)</span><span class="sxs-lookup"><span data-stu-id="ff5e8-208">![Basic Settings](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image26.png)</span></span>
8. <span data-ttu-id="ff5e8-209">선택 **웹 사이트** 플랫폼 선택 항목 중에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-209">Select **Website** from the platform choices.</span></span>  
  
    ![플랫폼 선택](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image27.png)
9. <span data-ttu-id="ff5e8-211">메모 프로그램 **앱 ID** 하였고 **응용 프로그램 암호** 이 자습서의 뒷부분에 나오는 모두 MVC 응용 프로그램에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-211">Make a note of your **App ID** and your **App Secret** so that you can add both into your MVC application later in this tutorial.</span></span> <span data-ttu-id="ff5e8-212">또한 사이트 URL을 추가 (`https://localhost:44300/`) MVC 응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-212">Also, Add your Site URL (`https://localhost:44300/`) to test your MVC application.</span></span> <span data-ttu-id="ff5e8-213">또한 추가 된 **Contact Email**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-213">Also, add a **Contact Email**.</span></span> <span data-ttu-id="ff5e8-214">그런 다음 선택 **변경 내용 저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-214">Then, select **Save Changes**.</span></span>   

    ![기본 응용 프로그램 세부 정보 페이지](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image28.png)

    > [!NOTE]
    > <span data-ttu-id="ff5e8-216">Note 등록 전자 메일 별칭을 사용 하 여 인증할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-216">Note that you will only be able to authenticate using the email alias you have registered.</span></span> <span data-ttu-id="ff5e8-217">다른 사용자와 테스트 계정이 됩니다 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-217">Other users and test accounts will not be able to register.</span></span> <span data-ttu-id="ff5e8-218">Facebook에서 응용 프로그램에 대 한 다른 Facebook 계정 액세스 권한을 부여할 수 있습니다 **개발자 역할** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-218">You can grant other Facebook accounts access to the application on the Facebook **Developer Roles** tab.</span></span>
10. <span data-ttu-id="ff5e8-219">Visual Studio에서 열고 *앱\_Start\Startup.Auth.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-219">In Visual Studio, open *App\_Start\Startup.Auth.cs*.</span></span>
11. <span data-ttu-id="ff5e8-220">복사 및 붙여넣기의 **AppId** 및 **응용 프로그램 암호** 에 `UseFacebookAuthentication` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-220">Copy and paste the **AppId** and **App Secret** into the `UseFacebookAuthentication` method.</span></span> <span data-ttu-id="ff5e8-221">**AppId** 및 **응용 프로그램 암호** 아래 표시 된 값은 샘플 및 작동 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-221">The **AppId** and **App Secret** values shown below are samples and will not work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample3.cs?highlight=33-35,38-39)]
12. <span data-ttu-id="ff5e8-222">클릭 **ब ा ळ**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-222">Click **Save Changes**.</span></span>
13. <span data-ttu-id="ff5e8-223">키를 눌러 **CTRL + f 5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-223">Press **CTRL+F5** to run the application.</span></span>


<span data-ttu-id="ff5e8-224">선택 **로그인** 로그인 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-224">Select **Log in** to display the Login page.</span></span> <span data-ttu-id="ff5e8-225">클릭 **Facebook** 아래 **필요한 다른 서비스가 사용 하 여 로그인 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ff5e8-225">Click **Facebook** under **Use another service to log in.**</span></span>

<span data-ttu-id="ff5e8-226">Facebook 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-226">Enter your Facebook credentials.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image29.png)

<span data-ttu-id="ff5e8-227">공개 프로필 및 친구 목록에 액세스 하는 응용 프로그램에 대 한 권한을 부여 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-227">You will be prompted to grant permission for the application to access your public profile and friend list.</span></span>

![Facebook 응용 프로그램 세부 정보](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image30.png)

<span data-ttu-id="ff5e8-229">이제 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-229">You are now logged in.</span></span> <span data-ttu-id="ff5e8-230">이제 응용 프로그램과 함께이 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-230">You can now register this account with the application.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image31.png)

<span data-ttu-id="ff5e8-231">등록 하면 항목에 추가 됩니다는 *사용자* 멤버 자격 데이터베이스의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-231">When you register, an entry is added to the *Users* table of the membership database.</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="ff5e8-232">멤버 자격 데이터를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-232">Examine the Membership Data</span></span>

<span data-ttu-id="ff5e8-233">에 **보기** 메뉴를 클릭 하 여 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-233">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="ff5e8-234">확장 **DefaultConnection (MvcAuth)** 를 확장 하 고 **테이블**를 마우스 오른쪽 단추로 클릭 **AspNetUsers** 클릭 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-234">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers 테이블 데이터](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="ff5e8-236">프로필 데이터를 사용자 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-236">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="ff5e8-237">이 섹션에 추가 합니다 생년월일 및 홈 도시 사용자 데이터를 등록 하는 동안 다음 그림에 나와 있는 것 처럼.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-237">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![홈 동 및 Bday reg](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="ff5e8-239">열기는 *Models\IdentityModels.cs* 파일 및 birth date 및 홈 동 속성 추가:</span><span class="sxs-lookup"><span data-stu-id="ff5e8-239">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="ff5e8-240">열기는 *Models\AccountViewModels.cs* 파일 및 집합에서 날짜 및 홈 동 속성 birth `ExternalLoginConfirmationViewModel`합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-240">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="ff5e8-241">열기는 *Controllers\AccountController.cs* 파일 및 코드의 날짜 및 홈 동 생년월일에 대 한 추가 `ExternalLoginConfirmation` 동작 메서드 같이:</span><span class="sxs-lookup"><span data-stu-id="ff5e8-241">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="ff5e8-242">생년월일 및 홈 도시에 추가 된 *Views\Account\ExternalLoginConfirmation.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="ff5e8-242">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="ff5e8-243">다시 응용 프로그램과 함께 Facebook 계정을 등록 하 고 새 생년월일 및 홈 동 프로필 정보를 추가할 수 있습니다 확인 수 있도록 멤버 자격 데이터베이스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-243">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="ff5e8-244">**솔루션 탐색기**, 클릭는 **모든 파일 표시** 아이콘을 다음 마우스 오른쪽 단추로 클릭 *추가\_Data\aspnet-MvcAuth-&lt;날짜 스탬프&gt;.mdf* 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-244">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="ff5e8-245">**도구** 메뉴를 클릭 하 여 **NuGet 패키지 관리자**, 클릭 **패키지 관리자 콘솔** (PMC).</span><span class="sxs-lookup"><span data-stu-id="ff5e8-245">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="ff5e8-246">PMC에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-246">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="ff5e8-247">Enable-migrations</span><span class="sxs-lookup"><span data-stu-id="ff5e8-247">Enable-Migrations</span></span>
2. <span data-ttu-id="ff5e8-248">추가 마이그레이션 초기화</span><span class="sxs-lookup"><span data-stu-id="ff5e8-248">Add-Migration Init</span></span>
3. <span data-ttu-id="ff5e8-249">데이터베이스 업데이트</span><span class="sxs-lookup"><span data-stu-id="ff5e8-249">Update-Database</span></span>

<span data-ttu-id="ff5e8-250">응용 프로그램을 실행 하 고 FaceBook 및 Google에 로그인 하 고 일부 사용자를 등록에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-250">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="ff5e8-251">멤버 자격 데이터를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-251">Examine the Membership Data</span></span>

<span data-ttu-id="ff5e8-252">에 **보기** 메뉴를 클릭 하 여 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-252">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="ff5e8-253">마우스 오른쪽 단추로 클릭 **AspNetUsers** 클릭 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-253">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="ff5e8-254">`HomeTown` 및 `BirthDate` 필드 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-254">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="ff5e8-255">로그 앱 오프 하 고 다른 계정으로 로그인</span><span class="sxs-lookup"><span data-stu-id="ff5e8-255">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="ff5e8-256">Facebook, 사용 하 여 앱에 로그온 하 고 다음 로그 아웃 및 로그인 하려고 하는 경우 다시 (동일한 브라우저 사용), 다른 Facebook 계정으로 있습니다 즉시에 기록 됩니다 사용한 Facebook 계정 이전 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-256">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="ff5e8-257">다른 계정을 사용 하려면 Facebook을 찾아 Facebook에서 로그 아웃 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-257">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="ff5e8-258">모든 다른 타사 인증 공급자에 동일한 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-258">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="ff5e8-259">또는 다른 브라우저를 사용 하 여 다른 계정으로 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-259">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff5e8-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff5e8-260">Next Steps</span></span>

<span data-ttu-id="ff5e8-261">참조 [Yahoo 및 LinkedIn OAuth 보안 공급자 OWIN에 대 한 소개](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) Yahoo 및 LinkedIn 지침은 Jerrie Pelser 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-261">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="ff5e8-262">Jerrie의 참조 사용 소셜 로그인 단추를 가져오려는 ASP.NET MVC 5에 대 한 소셜 로그인 단추가 정말 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-262">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="ff5e8-263">내 자습서에 따라 [인증 및 SQL DB ASP.NET MVC 응용 프로그램 만들기 및 Azure 앱 서비스 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data),이 자습서를 계속 하 고 다음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-263">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="ff5e8-264">Azure에 응용 프로그램을 배포 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-264">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="ff5e8-265">역할과 응용 프로그램을 보호 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-265">How to secure you app with roles.</span></span>
3. <span data-ttu-id="ff5e8-266">응용 프로그램을 보호 하는 방법의 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) 및 [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-266">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="ff5e8-267">사용자 및 역할에 추가할 구성원 API를 사용 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-267">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="ff5e8-268">이 자습서를 연결 하는 방법 및 향상 될 수 있습니다에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-268">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="ff5e8-269">새 항목을 요청할 수도 있습니다 [Me 방법으로 코드 보기](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-269">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="ff5e8-270">에 게 요청 하 고 ASP.NET에 추가할 수 있는 새로운 기능에 대해 투표도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-270">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="ff5e8-271">예를 들어를 도구에 대 한 투표 수 [만들고 사용자 및 역할을 관리 합니다.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="ff5e8-271">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="ff5e8-272">ASP.NET 외부 인증 서비스가 작동 하는 방법의 좋은 설명 Robert McMurray의을 참조 하십시오. [외부 인증 서비스](https://asp.net/web-api/overview/security/external-authentication-services)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-272">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="ff5e8-273">Microsoft 및 Twitter 인증을 사용 하기 위한 정보를 확인할 Robert의 문서도 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-273">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="ff5e8-274">Tom Dykstra의 뛰어난 [EF/MVC 자습서](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Entity Framework와 함께 작업 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ff5e8-274">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
