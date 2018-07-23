---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: MVC 5 만들기 Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on (C#)를 사용 하 여 앱 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 사용자는 외부 인증에서 자격 증명을 사용 하 여 OAuth 2.0을 사용 하 여 로그인 할 수 있도록 하는 ASP.NET MVC 5 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다...
ms.author: aspnetcontent
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: f36b73aac2e7844367e1e52b2c721bfe6b3575e2
ms.sourcegitcommit: 7097dba14d5b858e82758ee031ac62dbe3611339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39138521"
---
<a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="d111f-103">Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on (C#)를 사용 하 여 ASP.NET MVC 5 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d111f-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>
====================
<span data-ttu-id="d111f-104">[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="d111f-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="d111f-105">이 자습서에서는 사용 하 여 사용자가 로그인 할 수 있도록 하는 ASP.NET MVC 5 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다 [OAuth 2.0](http://oauth.net/2/) 외부 인증 공급자, 예: Facebook, Twitter, LinkedIn, Microsoft 또는 Google에서에서 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="d111f-106">간단히 하기 위해이 자습서는 Facebook 및 Google에서 자격 증명을 사용 하 여 작업에 집중 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="d111f-107">수백만 명의 사용자는 이러한 외부 공급자를 사용 하 여 계정을 이미 있기 때문에 중요 한 장점을 제공 웹 사이트에서 이러한 자격 증명을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="d111f-108">이러한 사용자를 만들고 새 자격 증명 집합을 기억 없는 경우 사이트에 대 한 등록 싶다는 더욱 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="d111f-109">참고 항목 [SMS 및 전자 메일 2 단계 인증을 사용 하 여 ASP.NET MVC 5 앱](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="d111f-110">또한 자습서에는 사용자의 프로필 데이터를 추가 하는 방법 및 역할을 추가 하는 멤버 API를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="d111f-111">이 자습서를 통해 작성 했습니다 [Rick Anderson](https://blogs.msdn.com/rickAndy) (하세요 me Twitter에서 팔 로우: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="d111f-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>


<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="d111f-112">시작</span><span class="sxs-lookup"><span data-stu-id="d111f-112">Getting Started</span></span>

<span data-ttu-id="d111f-113">설치 및 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 하거나 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="d111f-114">Visual Studio를 설치 [2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390521) 이상.</span><span class="sxs-lookup"><span data-stu-id="d111f-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="d111f-115">Dropbox, GitHub, Linkedin, Instagram, 버퍼, Salesforce, 스트림, 스택 교환, Tripit, Twitch, Twitter, yahoo! 등을 사용 하 여 도움말을 참조 하세요 [샘플 프로젝트](https://github.com/matthewdunsdon/oauthforaspnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="d111f-116">Visual Studio를 설치 해야 합니다 [2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390521) 이상 Google OAuth 2를 사용 하 고 SSL 경고 없이 로컬로 디버그 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>


<span data-ttu-id="d111f-117">클릭 **새 프로젝트** 에서 합니다 **시작** 페이지 또는 사용자 메뉴를 사용 하 고 선택할 수 **파일**를 차례로 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  
 

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="d111f-118">응용 프로그램 처음 만들기</span><span class="sxs-lookup"><span data-stu-id="d111f-118">Creating Your First Application</span></span>

<span data-ttu-id="d111f-119">클릭 **새 프로젝트**을 선택한 후 **Visual C#** 한 다음 왼쪽의 **웹** 선택한 후 **ASP.NET 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="d111f-120">"MvcAuth" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="d111f-121">에 **새 ASP.NET 프로젝트** 대화 상자에서 클릭 **MVC**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="d111f-122">인증이 없는 경우 **개별 사용자 계정**를 클릭 합니다 **인증 변경** 단추를 선택 **개별 사용자 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="d111f-123">체크 인하여 **클라우드에서 호스트**, 앱은 매우 쉽게 Azure에서 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="d111f-124">선택한 경우 **클라우드에서 호스트**, 구성 대화 상자를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)


### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="d111f-125">NuGet을 사용 하 여 최신 OWIN 미들웨어를 업데이트 하려면</span><span class="sxs-lookup"><span data-stu-id="d111f-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="d111f-126">NuGet 패키지 관리자를 사용 하 여 업데이트 합니다 [OWIN 미들웨어](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="d111f-127">선택 **업데이트** 왼쪽된 메뉴에서.</span><span class="sxs-lookup"><span data-stu-id="d111f-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="d111f-128">클릭할 수 있습니다 합니다 **모두 업데이트** 단추나 있습니다 (다음 이미지에 표시 됨)만 OWIN 패키지를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="d111f-129">아래 이미지에서 OWIN 패키지만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="d111f-130">패키지 관리자 콘솔 (PMC)을 입력할 수 있습니다는 `Update-Package` 명령을 모든 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="d111f-131">키를 눌러 **F5** 하거나 **ctrl+f5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="d111f-132">아래 이미지에서 포트 번호가 1234입니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="d111f-133">응용 프로그램을 실행 하는 경우 다른 포트 번호를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="d111f-134">브라우저 창의 크기에 따라 탐색 아이콘을 클릭 해야 합니다 **홈**를 **에 대 한**를 **연락처**, **등록**하 고 **로그인** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="d111f-135">프로젝트의 SSL 설정</span><span class="sxs-lookup"><span data-stu-id="d111f-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="d111f-136">Google 및 Facebook과 같은 인증 공급자에 연결 하려면 IIS Express SSL을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="d111f-137">SSL을 사용 하 여 로그인 한 후 유지 하 고 HTTP로 다시 삭제 해야, 사용자 이름 및 암호와 네트워크를 통해 일반 텍스트로 전송 하는 SSL을 사용 하지 않고 암호 처럼 프로그램 로그인 쿠키는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="d111f-138">핸드셰이크를 수행 하 고 (즉, HTTPS HTTP 보다 느린 이유 대량의) 채널을 보호 하는 시간을 이미 사용 했습니다 외에, MVC 파이프라인 실행 되기 전에 미래를 현재 요청 확인 하지 않습니다 따라서 로그인 후 HTTP로 다시 리디렉션 요청을 훨씬 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="d111f-139">**솔루션 탐색기**를 클릭 합니다 **MvcAuth** 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="d111f-140">프로젝트 속성을 표시 하려면 F4 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="d111f-141">또는 합니다 **뷰** 메뉴를 선택할 수 있습니다 **속성 창**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="d111f-142">변경 **SSL 사용** True로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="d111f-143">SSL URL을 복사 (될 `https://localhost:44300/` 다른 SSL 프로젝트를 만든 하지 않는 한).</span><span class="sxs-lookup"><span data-stu-id="d111f-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="d111f-144">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **MvcAuth** 프로젝트를 마우스 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="d111f-145">선택 된 **웹** 탭을 선택한 다음 SSL URL을 붙여 넣습니다 합니다 **프로젝트 Url** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="d111f-146">파일을 저장 합니다 (Ctl + S).</span><span class="sxs-lookup"><span data-stu-id="d111f-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="d111f-147">이 URL을 Facebook 및 Google 인증 앱을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="d111f-148">추가 된 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 특성을 `Home` 모든 요청을 요구 하는 컨트롤러에서 HTTPS를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="d111f-149">추가 하는 것 보다 안전한 방법을 사용 합니다 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 응용 프로그램에는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="d111f-150">섹션을 참조 하세요 &quot;SSL 및 권한 부여 특성을 사용 하 여 응용 프로그램 보호&quot; tutoral 내에서 [인증 및 SQL DB를 사용 하 여 ASP.NET MVC 앱을 만들고 Azure App Service에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutoral [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="d111f-151">Home 컨트롤러의 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="d111f-152">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="d111f-153">이전에 인증서를 설치한 경우이 섹션의 나머지 부분을 건너뛰고 이동할 [OAuth 2 용 Google 앱 만들기 및 앱 프로젝트에 연결 하는](#goog), 그렇지 않은 경우 자체 서명 된 신뢰 지침에 따라 IIS Express에서 생성 하는 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="d111f-154">읽기를 **보안 경고** 대화 상자 및 클릭 **예** 나타내는 localhost 인증서를 설치 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="d111f-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="d111f-155">IE를 표시 합니다 *홈* 페이지 되며 SSL 경고가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="d111f-156">Google Chrome도 인증서를 수락 및 경고 없이 HTTPS 콘텐츠를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="d111f-157">Firefox에서 경고를 표시 하므로 자체 인증서 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="d111f-158">응용 프로그램에 대 한 안전 하 게 클릭할 수 **위험을 이해**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="d111f-159">OAuth 2 용 Google 앱 만들기 및 앱 프로젝트에 연결</span><span class="sxs-lookup"><span data-stu-id="d111f-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="d111f-160">현재 Google OAuth 지침은 [ASP.NET Core의 구성 Google 인증](/aspnet/core/security/authentication/social/google-logins)합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="d111f-161">로 이동 합니다 [Google 개발자 콘솔](https://console.developers.google.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="d111f-162">선택 하기 전에 프로젝트를 만들지 않은 경우 **자격 증명** 는 왼쪽된 탭을 선택한 후 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="d111f-163">왼쪽된 탭에서 클릭 **자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="d111f-164">클릭 **자격 증명을 만들어야** 한 다음 **OAuth 클라이언트 ID**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="d111f-165">에 **클라이언트 ID 만들기** 대화 상자에서 기본값을 그대로 **웹 응용 프로그램** 응용 프로그램 형식에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="d111f-166">설정 된 **권한이 부여 된 JavaScript** 위에서 사용 된 SSL URL 원본이 (`https://localhost:44300/` 다른 SSL 프로젝트를 만든 경우가 아니면)</span><span class="sxs-lookup"><span data-stu-id="d111f-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="d111f-167">설정 된 **권한이 부여 된 리디렉션 URI** 에:</span><span class="sxs-lookup"><span data-stu-id="d111f-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="d111f-168">OAuth 동의 화면 메뉴 항목을 클릭 한 다음에 전자 메일 주소 및 제품 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="d111f-169">양식을 클릭을 마쳤으면 **저장할**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="d111f-170">라이브러리 메뉴 항목 클릭, 검색 **Google + API**를 클릭 한 다음 활성화 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="d111f-171">아래 이미지에서는 사용 가능한 Api를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="d111f-172">Google Api API 관리자에서 참조를 **자격 증명** 가져오려고 탭의 **클라이언트 ID**.</span><span class="sxs-lookup"><span data-stu-id="d111f-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="d111f-173">응용 프로그램 비밀을 사용 하 여 JSON 파일을 저장 하는 다운로드.</span><span class="sxs-lookup"><span data-stu-id="d111f-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="d111f-174">복사 및 붙여넣기 합니다 **ClientId** 및 **ClientSecret** 에 `UseGoogleAuthentication` 메서드를 *Startup.Auth.cs* 파일을 *App_Start* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="d111f-175">합니다 **ClientId** 하 고 **ClientSecret** 아래 표시 된 값은 샘플 및 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="d111f-176">보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="d111f-177">계정 및 자격 증명을 단순하게 유지 하기 위해 샘플 위의 코드에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="d111f-178">참조 [ASP.NET 및 Azure App Service에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="d111f-179">키를 눌러 **ctrl+f5** 를 빌드하고 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="d111f-180">클릭 합니다 **로그인** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="d111f-181">아래 **다른 서비스를 사용 하 여 로그인 할**, 클릭 **Google**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="d111f-182">위의 단계를 하나라도 누락 되 면 HTTP 401 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="d111f-183">위의 단계를 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-183">Recheck your steps above.</span></span> <span data-ttu-id="d111f-184">필수 설정도 누락 되 면 (예를 들어 **제품 이름**); 인증이 작동 하려면 몇 분 정도 걸릴 수 있습니다, 누락 된 항목을 추가 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="d111f-185">자격 증명을 입력할 Google 사이트로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="d111f-186">자격 증명을 입력 한 후 방금 만든 웹 응용 프로그램에 권한을 부여 하려면 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="d111f-187">클릭 **수락**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-187">Click **Accept**.</span></span> <span data-ttu-id="d111f-188">이제 다시 이동 합니다는 **등록** Google 계정을 등록할 수 있는 MvcAuth 응용 프로그램의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="d111f-189">Gmail 계정에 사용 되는 로컬 전자 메일 등록 이름을 변경할 수 있지만 일반적으로 기본 전자 메일 별칭 (즉, 인증에 사용할 하나)를 유지 하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="d111f-190">**등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="d111f-191">Facebook에서 앱을 만들고 앱 프로젝트에 연결</span><span class="sxs-lookup"><span data-stu-id="d111f-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="d111f-192">현재 Facebook OAuth2 인증 지침을 참조 하세요. [구성 Facebook 인증](/aspnet/core/security/authentication/social/facebook-logins)</span><span class="sxs-lookup"><span data-stu-id="d111f-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>


<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="d111f-193">멤버 자격 데이터를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-193">Examine the Membership Data</span></span>

<span data-ttu-id="d111f-194">에 **뷰** 메뉴에서 클릭 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="d111f-195">확장 **DefaultConnection (MvcAuth)** 를 확장 하 고 **테이블**를 마우스 오른쪽 단추로 클릭 **AspNetUsers** 클릭 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers 테이블 데이터](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="d111f-197">사용자 클래스에 프로필 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="d111f-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="d111f-198">이 단원의 추가할 생년월일 및 홈 마을 사용자 데이터에 등록 하는 동안 다음 그림과에서 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![reg 홈 town과 Bday를 사용 하 여](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="d111f-200">엽니다는 *Models\IdentityModels.cs* 파일 및 birth date 및 홈 마을 속성 추가:</span><span class="sxs-lookup"><span data-stu-id="d111f-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="d111f-201">엽니다는 *Models\AccountViewModels.cs* 파일과 집합 birth date 및 홈 마을 속성 `ExternalLoginConfirmationViewModel`합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="d111f-202">열기는 *controllers\ accountcontroller.cs* 파일 및 birth date 및 홈 타운에 대 한 코드를 추가 합니다 `ExternalLoginConfirmation` 동작 메서드 같이:</span><span class="sxs-lookup"><span data-stu-id="d111f-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="d111f-203">생년월일 및 홈 마을에 추가 합니다 *Views\Account\ExternalLoginConfirmation.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="d111f-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="d111f-204">다시 응용 프로그램에 Facebook 계정을 등록 하 고 새 생년월일 및 홈 마 프로필 정보를 추가할 수 있습니다 확인 수 있도록 멤버 자격 데이터베이스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="d111f-205">**솔루션 탐색기**를 클릭 합니다 **모든 파일 표시** 아이콘을 마우스 오른쪽 단추로 클릭 *추가\_Data\aspnet-MvcAuth-&lt;날짜 스탬프&gt;.mdf* 누릅니다 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="d111f-206">**도구** 메뉴에서 클릭 **NuGet 패키지 관리자**, 클릭 **패키지 관리자 콘솔** (PMC).</span><span class="sxs-lookup"><span data-stu-id="d111f-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="d111f-207">PMC에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="d111f-208">Enable-migrations</span><span class="sxs-lookup"><span data-stu-id="d111f-208">Enable-Migrations</span></span>
2. <span data-ttu-id="d111f-209">Add-migration Init</span><span class="sxs-lookup"><span data-stu-id="d111f-209">Add-Migration Init</span></span>
3. <span data-ttu-id="d111f-210">데이터베이스 업데이트</span><span class="sxs-lookup"><span data-stu-id="d111f-210">Update-Database</span></span>

<span data-ttu-id="d111f-211">응용 프로그램을 실행 하 고 FaceBook 및 Google을 사용 하 여 로그인 하 고 일부 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="d111f-212">멤버 자격 데이터를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-212">Examine the Membership Data</span></span>

<span data-ttu-id="d111f-213">에 **뷰** 메뉴에서 클릭 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="d111f-214">마우스 오른쪽 단추로 클릭 **AspNetUsers** 누릅니다 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="d111f-215">합니다 `HomeTown` 고 `BirthDate` 필드 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="d111f-216">로그 오프 앱 및 다른 계정으로 로그인</span><span class="sxs-lookup"><span data-stu-id="d111f-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="d111f-217">그런 다음 로그 아웃 및 로그인 하려고 Facebook, 사용 하 여 앱에 로그온 하는 경우 다시 (동일한 브라우저 사용) 다른 Facebook 계정을 사용 하 여 있습니다 즉시에 기록 됩니다 사용한 이전 Facebook 계정.</span><span class="sxs-lookup"><span data-stu-id="d111f-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="d111f-218">다른 계정을 사용 하려면 Facebook에 이동 하 고 Facebook에서 로그 아웃 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="d111f-219">모든 다른 타사 인증 공급자에 동일한 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="d111f-220">또는 다른 브라우저를 사용 하 여 다른 계정으로 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d111f-221">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d111f-221">Next Steps</span></span>

<span data-ttu-id="d111f-222">참조 [Yahoo 및 LinkedIn OAuth 보안 공급자를 OWIN에 대 한 소개](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) Yahoo와 LinkedIn 지침은 Jerrie Pelser 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="d111f-223">Jerrie의를 참조 하세요. 소셜 로그인 단추 ASP.NET MVC 5의 소셜 로그인 단추 사용을 가져오려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="d111f-224">내 자습서를 따릅니다 [인증 및 SQL DB를 사용 하 여 ASP.NET MVC 앱을 만들고 Azure App Service에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data),이 자습서를 계속 하 고 다음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="d111f-225">Azure에 앱을 배포 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="d111f-226">역할을 사용 하 여 앱에 보안을 유지 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="d111f-227">사용 하 여 앱을 보호 하는 방법을 합니다 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) 하 고 [권한 부여](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="d111f-228">멤버 자격 API를 사용 하 여 사용자 및 역할을 추가 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="d111f-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="d111f-229">이 자습서를 연결 하는 방법을 개선할 수 것에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="d111f-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="d111f-230">새 항목을 요청할 수도 있습니다 [표시 코드 사용 방법 보기](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="d111f-231">에 대 한 요청 하 고 ASP.NET에 추가 될 새 기능에 투표도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="d111f-232">예를 들어를 도구용 투표할 수 있습니다 [사용자 및 역할 만들기 및 관리 합니다.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="d111f-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="d111f-233">ASP.NET 외부 인증 서비스가 작동 하는 방법의 좋은 설명 Robert McMurray의을 참조 하세요 [외부 인증 서비스](https://asp.net/web-api/overview/security/external-authentication-services)합니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="d111f-234">Robert의 기사는 Microsoft 및 Twitter 인증을 사용 하기 위한 세부 정보로도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="d111f-235">Tom Dykstra의 뛰어난 [EF/MVC 자습서](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Entity Framework를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d111f-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
