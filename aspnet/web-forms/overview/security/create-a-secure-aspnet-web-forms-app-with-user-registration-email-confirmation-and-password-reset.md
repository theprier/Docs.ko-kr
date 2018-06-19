---
uid: web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
title: 확인 및 암호 재설정 (C#) 전자 메일 사용자 등록와 보안 ASP.NET Web Forms 응용 프로그램 만들기 | Microsoft Docs
author: Erikre
description: 이 자습서에서는 사용자 등록, 전자 메일 확인 및 암호 재설정 ASP.NET Identity 멤버를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 방법 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/02/2014
ms.topic: article
ms.assetid: 0a8d6044-5fab-4213-82d6-5618d5601358
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 1dc7ace69473b45432fd942b9cf1ba32332cb707
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30892701"
---
<a name="create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset-c"></a><span data-ttu-id="503ef-103">확인 및 암호 재설정 (C#) 전자 메일 사용자 등록와 보안 ASP.NET Web Forms 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="503ef-103">Create a secure ASP.NET Web Forms app with user registration, email confirmation and password reset (C#)</span></span>
====================
<span data-ttu-id="503ef-104">으로 [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="503ef-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

> <span data-ttu-id="503ef-105">이 자습서에서는 사용자 등록, 전자 메일 확인 및 암호 재설정 ASP.NET Identity 멤버 자격 시스템을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-105">This tutorial shows you how to build an ASP.NET Web Forms app with user registration, email confirmation and password reset using the ASP.NET Identity membership system.</span></span> <span data-ttu-id="503ef-106">이 자습서 Rick Anderson의 기반 [MVC 자습서](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-106">This tutorial was based on Rick Anderson's [MVC tutorial](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md).</span></span>


## <a name="introduction"></a><span data-ttu-id="503ef-107">소개</span><span class="sxs-lookup"><span data-stu-id="503ef-107">Introduction</span></span>

<span data-ttu-id="503ef-108">이 자습서에서는 Visual Studio 및 ASP.NET 4.5를 사용 하 여 사용자 등록 보안 Web Forms 응용 프로그램을 만들고, 확인 및 암호 재설정 전자 메일을 ASP.NET Web Forms 응용 프로그램을 만드는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-108">This tutorial guides you through the steps required to create an ASP.NET Web Forms application using Visual Studio and ASP.NET 4.5 to create a secure Web Forms app with user registration, email confirmation and password reset.</span></span>

### <a name="tutorial-tasks-and-information"></a><span data-ttu-id="503ef-109">자습서의 작업 및 정보:</span><span class="sxs-lookup"><span data-stu-id="503ef-109">Tutorial Tasks and Information:</span></span>

- [<span data-ttu-id="503ef-110">만들기는 ASP.NET Web Forms 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="503ef-110">Create an ASP.NET Web Forms app</span></span>](#createWebForms)
- [<span data-ttu-id="503ef-111">SendGrid 후크</span><span class="sxs-lookup"><span data-stu-id="503ef-111">Hook Up SendGrid</span></span>](#SG)
- [<span data-ttu-id="503ef-112">로그인 하기 전에 전자 메일 확인 필요</span><span class="sxs-lookup"><span data-stu-id="503ef-112">Require Email Confirmation Before Log In</span></span>](#require)
- [<span data-ttu-id="503ef-113">암호 복구 및 다시 설정</span><span class="sxs-lookup"><span data-stu-id="503ef-113">Password Recovery and Reset</span></span>](#reset)
- [<span data-ttu-id="503ef-114">전자 메일 확인 링크를 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-114">Resend Email Confirmation Link</span></span>](#rsend)
- [<span data-ttu-id="503ef-115">응용 프로그램 문제 해결</span><span class="sxs-lookup"><span data-stu-id="503ef-115">Troubleshooting the App</span></span>](#dbg)
- [<span data-ttu-id="503ef-116">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="503ef-116">Additional Resources</span></span>](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a><span data-ttu-id="503ef-117">ASP.NET Web Forms 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="503ef-117">Create an ASP.NET Web Forms App</span></span>

<span data-ttu-id="503ef-118">설치 하 고 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-118">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="503ef-119">설치 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상도 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-119">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher as well.</span></span>

> [!NOTE]
> <span data-ttu-id="503ef-120">경고:를 설치 해야 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 하려면이 자습서를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-120">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>


1. <span data-ttu-id="503ef-121">새 프로젝트를 만듭니다 (**파일**  - &gt; **새 프로젝트**)을 선택 하 고는 **ASP.NET 웹 응용 프로그램** 템플릿과 최신.NET Framework 버전은 **새 프로젝트** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="503ef-121">Create a new project (**File** -&gt; **New Project**) and select the **ASP.NET Web Application** template and the latest .NET Framework version from the **New Project** dialog box.</span></span>
2. <span data-ttu-id="503ef-122">**새 ASP.NET 프로젝트** 대화 상자는 **Web Forms** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="503ef-122">From the **New ASP.NET Project** dialog box, select the **Web Forms** template.</span></span> <span data-ttu-id="503ef-123">기본 인증을 두고 **개별 사용자 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-123">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="503ef-124">Azure에서 응용 프로그램 호스트 하려는 경우에 둡니다는 **클라우드의 호스트에에서** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-124">If you'd like to host the app in Azure, leave the **Host in the cloud** check box checked.</span></span>   
 <span data-ttu-id="503ef-125">클릭 **확인** 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-125">Then, click **OK** to create the new project.</span></span>  
    <span data-ttu-id="503ef-126">![새 ASP.NET 프로젝트 대화 상자](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="503ef-126">![New ASP.NET Project dialog box](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)</span></span>
3. <span data-ttu-id="503ef-127">프로젝트에 대 한 Secure Sockets Layer (SSL)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-127">Enable Secure Sockets Layer (SSL) for the project.</span></span> <span data-ttu-id="503ef-128">사용할 수 있는 단계에 따라는 **프로젝트에 대 한 SSL을 사용 하도록 설정** 의 섹션은 [Web Forms 자습서 시리즈 시작](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-128">Follow the steps available in the **Enable SSL for the Project** section of the [Getting Started with Web Forms tutorial series](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms).</span></span>
4. <span data-ttu-id="503ef-129">응용 프로그램 실행을 클릭는 **등록** 에 연결 하 고 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-129">Run the app, click the **Register** link and register a new user.</span></span> <span data-ttu-id="503ef-130">이 시점에서 전자 메일에만 유효성 검사는 기반는 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 특성을 전자 메일 주소 형식이 올바른지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-130">At this point, the only validation on the email is based on the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute to ensure the email address is well-formed.</span></span> <span data-ttu-id="503ef-131">전자 메일 확인을 추가 하는 코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-131">You will modify the code to add email confirmation.</span></span> <span data-ttu-id="503ef-132">브라우저 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-132">Close the browser window.</span></span>
5. <span data-ttu-id="503ef-133">**서버 탐색기** 의 Visual Studio (**보기**  - &gt; **서버 탐색기**)로 이동 **데이터 Connections\ DefaultConnection\Tables\AspNetUsers**를 마우스 오른쪽 단추로 클릭 하 고 **테이블 정의 열고**합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-133">In **Server Explorer** of Visual Studio (**View** -&gt; **Server Explorer**), navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span> 

    <span data-ttu-id="503ef-134">다음 그림에서는 `AspNetUsers` 테이블 스키마:</span><span class="sxs-lookup"><span data-stu-id="503ef-134">The following image shows the `AspNetUsers` table schema:</span></span>

    ![AspNetUsers 테이블 스키마](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="503ef-136">**서버 탐색기**를 마우스 오른쪽 단추로 클릭는 **AspNetUsers** 테이블을 선택한 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-136">In **Server Explorer**, right-click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
  
    ![AspNetUsers 테이블 데이터](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="503ef-138">이 시점에서 등록 된 사용자에 대 한 전자 메일 확인 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-138">At this point the email for the registered user has not been confirmed.</span></span>
7. <span data-ttu-id="503ef-139">행을 삭제 하려면 삭제 선택 사용자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-139">Click on the row and select delete to delete the user.</span></span> <span data-ttu-id="503ef-140">다음 단계에서이 전자 메일을 다시 추가 하 고 전자 메일 주소로 확인 메시지를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-140">You'll add this email again in the next step and send a confirmation message to the email address.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="503ef-141">전자 메일 확인</span><span class="sxs-lookup"><span data-stu-id="503ef-141">Email Confirmation</span></span>

<span data-ttu-id="503ef-142">다른 사용자에 가장 하지 않는 것을 확인 하려면 새 사용자를 등록 하는 동안 전자 메일을 확인 하는 것이 좋습니다 (즉, 이러한 하지 않은 등록 된 다른 사용자의 전자 메일).</span><span class="sxs-lookup"><span data-stu-id="503ef-142">It's a best practice to confirm the email during the registration of a new user to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="503ef-143">방지 하기 위해 원할 토론 포럼을 설치한 경우를 가정해 볼 `"bob@cpandl.com"` 등록에서 `"joe@contoso.com"`합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-143">Suppose you had a discussion forum, you would want to prevent `"bob@cpandl.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="503ef-144">전자 메일 확인 하지 않고 `"joe@contoso.com"` 원치 않는 전자 메일 앱에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-144">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="503ef-145">실수로 Bob로 등록 된 경우를 가정해 볼 `"bib@cpandl.com"` 를 발견 하지 않은 그 하는지 앱에 없는 올바른 전자 메일 때문에 암호 복구를 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-145">Suppose Bob accidently registered as `"bib@cpandl.com"` and hadn't noticed it, he wouldn't be able to use password recovery because the app doesn't have his correct email.</span></span> <span data-ttu-id="503ef-146">전자 메일 확인 bot에서만 제한 된 보호를 제공 하 고 결정된 된 스팸에서 보호를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-146">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers.</span></span>

<span data-ttu-id="503ef-147">일반적으로 새 사용자 메일, SMS 문자 메시지 또는 기타 메커니즘으로 확인 하기 전에 웹 사이트에 데이터를 게시 하는 것을 방지 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-147">You generally want to prevent new users from posting any data to your website before they have been confirmed by either email, an SMS text message or another mechanism.</span></span> <span data-ttu-id="503ef-148">아래 섹션에 전자 메일 확인을 사용 하도록 설정 하 고 새로 등록 된 사용자가 전자 메일 확인 될 때까지에 로그인 하지 못하도록 방지 하기 위해 코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-148">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span> <span data-ttu-id="503ef-149">이 자습서에서는 SendGrid에서 전자 메일 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-149">You'll use the email service SendGrid in this tutorial.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="503ef-150">SendGrid 후크</span><span class="sxs-lookup"><span data-stu-id="503ef-150">Hook up SendGrid</span></span>

<span data-ttu-id="503ef-151">이 자습서에서는 통해 전자 메일 알림을 추가 하는 방법을 보여 줍니다. 하지만 [SendGrid](http://sendgrid.com/), SMTP 및 다른 메커니즘을 사용 하 여 메일을 보낼 수 있습니다 (참조 [추가 리소스](#addRes)).</span><span class="sxs-lookup"><span data-stu-id="503ef-151">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="503ef-152">Visual Studio에서 열고는 **패키지 관리자 콘솔** (**도구**  - &gt; **NuGet 패키지 관리자**  - &gt; **패키지 관리자 콘솔**), 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-152">In Visual Studio, open the **Package Manager Console** (**Tools** -&gt; **NuGet Package Manger** -&gt; **Package Manager Console**), and enter the following command:</span></span>  
    `Install-Package SendGrid`
2. <span data-ttu-id="503ef-153">이동 하는 [Azure SendGrid 등록 페이지](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) 무료로 SendGrid 계정을 등록 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-153">Go to the [Azure SendGrid sign-up page](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) and register for free SendGrid account.</span></span> <span data-ttu-id="503ef-154">또한에서 직접 무료 SendGrid 계정을 등록 하면 [SendGrid의 사이트](http://www.sendgrid.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-154">You can also sign-up for a free SendGrid account directly on [SendGrid's site](http://www.sendgrid.com).</span></span>
3. <span data-ttu-id="503ef-155">**솔루션 탐색기** 열고는 *IdentityConfig.cs* 파일에 *앱\_시작* 폴더는 에노란색으로강조표시한다음코드를추가하고`EmailService` 구성 하는 클래스 **SendGrid**:</span><span class="sxs-lookup"><span data-stu-id="503ef-155">From **Solution Explorer** open the *IdentityConfig.cs* file in the *App\_Start* folder and add the following code highlighted in yellow to the `EmailService` class to configure **SendGrid**:</span></span>

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample1.cs?highlight=3,5,8-37)]
4. <span data-ttu-id="503ef-156">또한 다음 추가 `using` 문을의 시작 부분에는 *IdentityConfig.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="503ef-156">Also, add the following `using` statements to the beginning of the *IdentityConfig.cs* file:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample2.cs?highlight=1-4)]
5. <span data-ttu-id="503ef-157">이 예제를 단순하게 유지 하기 위해에 전자 메일 서비스 계정의 값을 저장 합니다는 `appSettings` 의 섹션은 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-157">To keep this sample simple, you'll store the email service account values in the `appSettings` section of the *web.config* file.</span></span> <span data-ttu-id="503ef-158">노란색으로 강조 표시 하는 다음 XML 추가 *web.config* 프로젝트의 루트에 파일:</span><span class="sxs-lookup"><span data-stu-id="503ef-158">Add the following XML highlighted in yellow to the *web.config* file at the root of your project:</span></span>

    [!code-xml[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample3.xml?highlight=2-5)]

    > [!WARNING]
    > <span data-ttu-id="503ef-159">보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-159">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="503ef-160">이 예제에서는 계정 및 자격 증명에 저장 됩니다는 **appSetting** 의 섹션은 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-160">In this example, the account and credentials are stored in the **appSetting** section of the *Web.config* file.</span></span> <span data-ttu-id="503ef-161">Azure에서 안전 하 게에 저장할 수 있습니다 이러한 값은 **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** Azure 포털에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-161">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="503ef-162">관련된 내용은 Rick Anderson의 항목을 참조 하세요. [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](https://go.microsoft.com/fwlink/?LinkId=513141)합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-162">For related information see Rick Anderson's topic titled [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](https://go.microsoft.com/fwlink/?LinkId=513141).</span></span>
6. <span data-ttu-id="503ef-163">SendGrid 인증 값 (사용자 이름 및 암호) 성공적으로 수행할 수 있도록 보낼 전자 메일 앱에서 반영 하기 위해 전자 메일 서비스 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-163">Add the email service values to reflect your SendGrid authentication values (User Name and Password) so that you can successful send email from your app.</span></span> <span data-ttu-id="503ef-164">SendGrid를 입력 한 전자 메일 주소 보다는 SendGrid 계정 이름을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-164">Be sure to use your SendGrid account name rather than the email address you provided SendGrid.</span></span>

### <a name="enable-email-confirmation"></a><span data-ttu-id="503ef-165">전자 메일 확인을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="503ef-165">Enable Email Confirmation</span></span>

 <span data-ttu-id="503ef-166">전자 메일 확인을 사용 하려면 다음 단계를 사용 하 여 등록 코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-166">To enable email confirmation, you'll modify the registration code using the following steps.</span></span>  
 

1. <span data-ttu-id="503ef-167">에 *계정* 폴더를 엽니다는 *Register.aspx.cs* 코드 숨김 및 업데이트는 `CreateUser_Click` 다음 강조 표시 된 변경할 수 있도록 메서드:</span><span class="sxs-lookup"><span data-stu-id="503ef-167">In the *Account* folder, open the *Register.aspx.cs* code-behind and update the `CreateUser_Click` method to enable the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample4.cs?highlight=9-11)]
2. <span data-ttu-id="503ef-168">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *Default.aspx* 선택 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-168">In **Solution Explorer**, right-click *Default.aspx* and select **Set As Start Page**.</span></span>
3. <span data-ttu-id="503ef-169">키를 눌러 앱을 실행 **F5 합니다.**</span><span class="sxs-lookup"><span data-stu-id="503ef-169">Run the app by pressing **F5.**</span></span> <span data-ttu-id="503ef-170">페이지 표시 되 면 클릭는 **등록** 링크 레지스터 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-170">After the page is displayed, click the **Register** link to display the Register page.</span></span>
4. <span data-ttu-id="503ef-171">전자 메일 및 암호를 입력 한 다음 클릭는 **등록** 단추 SendGrid 통해 전자 메일 메시지를 보내도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-171">Enter your email and password, then click the **Register** button to send an email message via SendGrid.</span></span>  
   <span data-ttu-id="503ef-172">프로젝트 및 코드의 현재 상태에는 사용자 계정으로를 확인 하지 않은 경우에 등록 양식을 완료 되 면에 로그인 할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-172">The current state of your project and code will allow the user to log in once they complete the registration form, even though they haven't confirmed their account.</span></span>
5. <span data-ttu-id="503ef-173">전자 메일 계정을 확인 하 고 사용자의 전자 메일을 확인 하려면 다음 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-173">Check your email account and click on the link to confirm your email.</span></span>  
   <span data-ttu-id="503ef-174">등록 양식을 전송 하면에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-174">Once you submit the registration form, you will be logged in.</span></span>  
    ![샘플 웹 사이트-로그인](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image4.png)

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="503ef-176">로그인 하기 전에 전자 메일 확인 필요</span><span class="sxs-lookup"><span data-stu-id="503ef-176">Require Email Confirmation Before Log In</span></span>

<span data-ttu-id="503ef-177">전자 메일 계정 확인 하지만 시점에서 하지 해야에 완전히 서명 확인 전자 메일에 포함 된 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-177">Although you have confirmed the email account, at this point you would not need to click on the link contained in the verification email to be fully signed-in.</span></span> <span data-ttu-id="503ef-178">다음 섹션에 새 사용자가을 기록 하기 전에 확인 된 전자 메일을 가질 (인증)를 요구 하는 코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-178">In the following section, you will modify the code requiring new users to have a confirmed email before they are logged in (authenticated).</span></span>

1. <span data-ttu-id="503ef-179">**솔루션 탐색기** Visual Studio의 업데이트는 `CreateUser_Click` 이벤트에는 *Register.aspx.cs* 코드 숨김에 포함 된는 *계정* 폴더는 다음 강조 표시 된 변경 내용:</span><span class="sxs-lookup"><span data-stu-id="503ef-179">In **Solution Explorer** of Visual Studio, update the `CreateUser_Click` event in the *Register.aspx.cs* code-behind contained in the *Accounts* folder with the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample5.cs?highlight=13-14,17-21)]
2. <span data-ttu-id="503ef-180">업데이트는 `LogIn` 에서 메서드는 *Login.aspx.cs* 다음 강조 표시 된 변경 내용으로 코드 숨김:</span><span class="sxs-lookup"><span data-stu-id="503ef-180">Update the `LogIn` method in the *Login.aspx.cs* code-behind with the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample6.cs?highlight=9-19,45-46)]

### <a name="run-the-application"></a><span data-ttu-id="503ef-181">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="503ef-181">Run the Application</span></span>

 <span data-ttu-id="503ef-182">사용자의 전자 메일 주소 확인 했는지를 확인 하는 코드를 구현한 했으므로 둘 다에서 기능을 확인할 수 있습니다는 **등록** 및 **로그인** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-182">Now that you have implemented the code to check whether a user's email address has been confirmed, you can check the functionality on both the **Register** and **Login** pages.</span></span> 

1. <span data-ttu-id="503ef-183">모든 계정을 삭제는 **AspNetUsers** 테스트 하려는 전자 메일 별칭을 포함 하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-183">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test.</span></span>
2. <span data-ttu-id="503ef-184">응용 프로그램을 실행 (**F5**) 하 고 확인 전자 메일 주소를 확인 한 될 때까지 사용자로 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-184">Run the app (**F5**) and verify you cannot register as a user until you have confirmed your email address.</span></span>
3. <span data-ttu-id="503ef-185">방금 전송 된 전자 메일을 통해 사용자는 새 계정을 결정 하기 전에 새 계정으로 로그인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-185">Before confirming your new account via the email that was just sent, attempt to log in with the new account.</span></span>  
 <span data-ttu-id="503ef-186">로그인 할 수 없는 및 확인 된 전자 메일 계정을 보유 해야 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-186">You'll see that you are unable to log in and that you must have a confirmed email account.</span></span>
4. <span data-ttu-id="503ef-187">전자 메일 주소를 확인 하 고 나면 응용 프로그램에에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-187">Once you confirm your email address, log in to the app.</span></span>

<a id="reset"></a>
## <a name="password-recovery-and-reset"></a><span data-ttu-id="503ef-188">암호 복구 및 다시 설정</span><span class="sxs-lookup"><span data-stu-id="503ef-188">Password Recovery and Reset</span></span>

1. <span data-ttu-id="503ef-189">Visual Studio에서 주석 문자를 제거는 `Forgot` 에서 메서드는 *Forgot.aspx.cs* 에 포함 된 코드 숨김의 *계정* 폴더 메서드가으로 나타나도록 따릅니다:</span><span class="sxs-lookup"><span data-stu-id="503ef-189">In Visual Studio, remove the comment characters from the `Forgot` method in the *Forgot.aspx.cs* code-behind contained in the *Account* folder, so that the method appears as follows:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample7.cs?highlight=16-18)]
2. <span data-ttu-id="503ef-190">열기는 *Login.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="503ef-190">Open the *Login.aspx* page.</span></span> <span data-ttu-id="503ef-191">대체의 끝 부분에서 태그는 **loginForm** 아래의 강조 표시 된 대로 섹션:</span><span class="sxs-lookup"><span data-stu-id="503ef-191">Replace the markup near the end of the **loginForm** section as highlighted below:</span></span> 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample8.aspx?highlight=52-53)]
3. <span data-ttu-id="503ef-192">열기는 *Login.aspx.cs* 코드 숨김 및에서 노란색으로 강조 표시 하는 코드의 다음 줄을 주석 처리 제거는 `Page_Load` 이벤트 처리기.</span><span class="sxs-lookup"><span data-stu-id="503ef-192">Open the *Login.aspx.cs* code-behind and uncomment the following line of code highlighted in yellow from the `Page_Load` event handler:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample9.cs?highlight=5)]
4. <span data-ttu-id="503ef-193">키를 눌러 앱을 실행 **F5 합니다.**</span><span class="sxs-lookup"><span data-stu-id="503ef-193">Run the app by pressing **F5.**</span></span> <span data-ttu-id="503ef-194">페이지 표시 되 면 클릭는 **로그인** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-194">After the page is displayed, click the **Log in** link.</span></span>
5. <span data-ttu-id="503ef-195">클릭는 **암호를 잊으셨습니까?** 표시 하려면 링크는 **암호를 잊으셨습니까** 페이지.</span><span class="sxs-lookup"><span data-stu-id="503ef-195">Click the **Forgot your password?** link to display the **Forgot Password** page.</span></span>
6. <span data-ttu-id="503ef-196">전자 메일 주소를 입력 하 고 클릭는 **전송** 암호를 다시 설정할 수 있는 주소로 전자 메일을 보내는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-196">Enter your email address and click the **Submit** button to send an email to your address which will allow you to reset your password.</span></span>   
   <span data-ttu-id="503ef-197">전자 메일 계정을 확인 하 고 표시 하려면 링크를 클릭는 **암호 재설정** 페이지.</span><span class="sxs-lookup"><span data-stu-id="503ef-197">Check your email account and click on the link to display the **Reset Password** page.</span></span>
7. <span data-ttu-id="503ef-198">에 **암호 재설정** 페이지에서 전자 메일, 암호 및 확인된 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-198">On the **Reset Password** page, enter your email, password, and confirmed password.</span></span> <span data-ttu-id="503ef-199">그런 다음 눌러는 **재설정** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-199">Then, press the **Reset** button.</span></span>  
   <span data-ttu-id="503ef-200">암호를 재설정할 때는 **암호가 변경** 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-200">When you successfully reset your password, the **Password Changed** page will be displayed.</span></span> <span data-ttu-id="503ef-201">이제 새 암호를 사용 하 여 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-201">Now you can log in with your new password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="503ef-202">전자 메일 확인 링크를 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-202">Resend Email Confirmation Link</span></span>

<span data-ttu-id="503ef-203">사용자는 새 로컬 계정을 만들고 나면은 로그온 할 수 전에 사용 하는 데 필요 확인 링크를 전자 메일로 전송 되 있습니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-203">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="503ef-204">실수로 삭제 확인 전자 메일 또는 전자 메일이 도착 하지 확인 링크 다시 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-204">If the user accidently deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="503ef-205">다음 코드 변경 내용에는이 기능을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-205">The following code changes show how to enable this.</span></span>

1. <span data-ttu-id="503ef-206">Visual Studio에서 열고는 **Login.aspx.cs** 후 다음 이벤트 처리기를 추가 하 고 코드 숨김의 `LogIn` 이벤트 처리기:</span><span class="sxs-lookup"><span data-stu-id="503ef-206">In Visual Studio, open the **Login.aspx.cs** code-behind and add the following event handler after the `LogIn` event handler:</span></span>   

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample10.cs)]
2. <span data-ttu-id="503ef-207">수정 된 `LogIn` 의 이벤트 처리기는 *Login.aspx.cs* 코드 숨김 다음과 같이 노란색으로 강조 표시 하는 코드를 변경 하 여:</span><span class="sxs-lookup"><span data-stu-id="503ef-207">Modify the `LogIn` event handler in the *Login.aspx.cs* code-behind by changing the code highlighted in yellow as follows:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample11.cs?highlight=15-17)]
3. <span data-ttu-id="503ef-208">업데이트는 *Login.aspx* 다음과 같이 노란색으로 강조 표시 하는 코드를 추가 하 여 페이지:</span><span class="sxs-lookup"><span data-stu-id="503ef-208">Update the *Login.aspx* page by adding the code highlighted in yellow as follows:</span></span> 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample12.aspx?highlight=45-46)]
4. <span data-ttu-id="503ef-209">모든 계정을 삭제는 **AspNetUsers** 테스트 하려는 전자 메일 별칭을 포함 하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-209">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test.</span></span>
5. <span data-ttu-id="503ef-210">응용 프로그램을 실행 (**F5**) 하 고 전자 메일 주소를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-210">Run the app (**F5**) and register your email address.</span></span>
6. <span data-ttu-id="503ef-211">방금 전송 된 전자 메일을 통해 사용자는 새 계정을 결정 하기 전에 새 계정으로 로그인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-211">Before confirming your new account via the email that was just sent, attempt to log in with the new account.</span></span>  
   <span data-ttu-id="503ef-212">로그인 할 수 없는 및 확인 된 전자 메일 계정을 보유 해야 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-212">You'll see that you are unable to log in and that you must have a confirmed email account.</span></span> <span data-ttu-id="503ef-213">또한 이제 다시 보낼 수 있습니다 확인 메시지를 전자 메일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-213">In addition, you can now resend a confirmation message to your email account.</span></span>
7. <span data-ttu-id="503ef-214">전자 메일 주소와 암호를 입력 누릅니다는 **확인을 다시 보낼** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-214">Enter your email address and password, then press the **Resend confirmation** button.</span></span>
8. <span data-ttu-id="503ef-215">새로 보낸된 전자 메일 메시지에 기반한 전자 메일 주소를 확인 하 고 나면 앱에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-215">Once you confirm your email address based on the newly sent email message, log in to the app.</span></span>

<a id="dbg"></a>
## <a name="troubleshooting-the-app"></a><span data-ttu-id="503ef-216">응용 프로그램 문제 해결</span><span class="sxs-lookup"><span data-stu-id="503ef-216">Troubleshooting the App</span></span>

<span data-ttu-id="503ef-217">자격 증명을 확인에 대 한 링크를 포함 된 메일을 수신 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-217">If you don't receive an email containing the link to verify your credentials:</span></span>

- <span data-ttu-id="503ef-218">정크 또는 스팸 폴더를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-218">Check your junk or spam folder.</span></span>
- <span data-ttu-id="503ef-219">SendGrid 계정에 로그인 하 고 클릭는 [전자 메일 작업 링크](https://sendgrid.com/logs/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-219">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>
- <span data-ttu-id="503ef-220">SendGrid 사용자 계정 이름으로 사용할 수는 *Web.config* SendGrid 계정 전자 메일 주소 대신 값입니다.</span><span class="sxs-lookup"><span data-stu-id="503ef-220">Be certain you used your SendGrid user account name as a *Web.config* value rather than your SendGrid account email address.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="503ef-221">추가 자료</span><span class="sxs-lookup"><span data-stu-id="503ef-221">Additional Resources</span></span>

- [<span data-ttu-id="503ef-222">ASP.NET Id에 대 한 링크 권장 리소스</span><span class="sxs-lookup"><span data-stu-id="503ef-222">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [<span data-ttu-id="503ef-223">계정 확인 및 ASP.NET Id와 암호 복구</span><span class="sxs-lookup"><span data-stu-id="503ef-223">Account Confirmation and Password Recovery with ASP.NET Identity</span></span>](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [<span data-ttu-id="503ef-224">ASP.NET Web Forms 자습서 시리즈-OAuth 2.0 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="503ef-224">ASP.NET Web Forms tutorial series - Add an OAuth 2.0 Provider</span></span>](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [<span data-ttu-id="503ef-225">Azure 앱 서비스에 멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET Web Forms 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="503ef-225">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [<span data-ttu-id="503ef-226">ASP.NET Web Forms 자습서 시리즈-프로젝트에 대 한 SSL 사용</span><span class="sxs-lookup"><span data-stu-id="503ef-226">ASP.NET Web Forms tutorial series - Enable SSL for the Project</span></span>](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
