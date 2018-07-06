---
uid: web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
title: 전자 메일 확인 및 암호 재설정 기능이 (C#) 사용자 등록을 사용 하 여 보안 ASP.NET Web Forms 앱 만들기 | Microsoft Docs
author: Erikre
description: 이 자습서에서는 사용자 등록, 전자 메일 확인 및 ASP.NET Id 멤버를 사용 하 여 암호를 사용 하 여 ASP.NET Web Forms 앱을 빌드하는 방법을 보여 줍니다...
ms.author: aspnetcontent
ms.date: 10/02/2014
ms.assetid: 0a8d6044-5fab-4213-82d6-5618d5601358
msc.legacyurl: /web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 1c230c3f33bd8261312485e9d77f6f88adb49e9e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37812771"
---
<a name="create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset-c"></a><span data-ttu-id="0bd72-103">전자 메일 확인 및 암호 재설정 기능이 (C#) 사용자 등록을 사용 하 여 보안 ASP.NET Web Forms 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0bd72-103">Create a secure ASP.NET Web Forms app with user registration, email confirmation and password reset (C#)</span></span>
====================
<span data-ttu-id="0bd72-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="0bd72-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

> <span data-ttu-id="0bd72-105">이 자습서에서는 사용자 등록, 전자 메일 확인 및 ASP.NET Id 멤버 자격 시스템을 사용 하 여 암호를 사용 하 여 ASP.NET Web Forms 앱을 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-105">This tutorial shows you how to build an ASP.NET Web Forms app with user registration, email confirmation and password reset using the ASP.NET Identity membership system.</span></span> <span data-ttu-id="0bd72-106">이 자습서 Rick Anderson의 기반한 [MVC 자습서](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-106">This tutorial was based on Rick Anderson's [MVC tutorial](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md).</span></span>


## <a name="introduction"></a><span data-ttu-id="0bd72-107">소개</span><span class="sxs-lookup"><span data-stu-id="0bd72-107">Introduction</span></span>

<span data-ttu-id="0bd72-108">이 자습서에서는 Visual Studio 및 ASP.NET 4.5를 사용 하 여 사용자 등록을 사용 하 여 안전 Web Forms 앱 만들기, 확인 및 암호 재설정 전자 메일에 ASP.NET Web Forms 응용 프로그램을 만드는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-108">This tutorial guides you through the steps required to create an ASP.NET Web Forms application using Visual Studio and ASP.NET 4.5 to create a secure Web Forms app with user registration, email confirmation and password reset.</span></span>

### <a name="tutorial-tasks-and-information"></a><span data-ttu-id="0bd72-109">자습서의 작업 및 정보:</span><span class="sxs-lookup"><span data-stu-id="0bd72-109">Tutorial Tasks and Information:</span></span>

- [<span data-ttu-id="0bd72-110">만들 ASP.NET Web Forms 앱</span><span class="sxs-lookup"><span data-stu-id="0bd72-110">Create an ASP.NET Web Forms app</span></span>](#createWebForms)
- [<span data-ttu-id="0bd72-111">SendGrid 연결</span><span class="sxs-lookup"><span data-stu-id="0bd72-111">Hook Up SendGrid</span></span>](#SG)
- [<span data-ttu-id="0bd72-112">로그인 하기 전에 전자 메일 확인 필요</span><span class="sxs-lookup"><span data-stu-id="0bd72-112">Require Email Confirmation Before Log In</span></span>](#require)
- [<span data-ttu-id="0bd72-113">암호 복구 및 다시 설정</span><span class="sxs-lookup"><span data-stu-id="0bd72-113">Password Recovery and Reset</span></span>](#reset)
- [<span data-ttu-id="0bd72-114">전자 메일 확인 링크 다시 보내기</span><span class="sxs-lookup"><span data-stu-id="0bd72-114">Resend Email Confirmation Link</span></span>](#rsend)
- [<span data-ttu-id="0bd72-115">앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="0bd72-115">Troubleshooting the App</span></span>](#dbg)
- [<span data-ttu-id="0bd72-116">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0bd72-116">Additional Resources</span></span>](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a><span data-ttu-id="0bd72-117">ASP.NET Web Forms 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0bd72-117">Create an ASP.NET Web Forms App</span></span>

<span data-ttu-id="0bd72-118">설치 및 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 하거나 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-118">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="0bd72-119">설치할 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-119">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher as well.</span></span>

> [!NOTE]
> <span data-ttu-id="0bd72-120">: 경고를 설치 해야 합니다 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상이 자습서를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-120">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>


1. <span data-ttu-id="0bd72-121">새 프로젝트를 만듭니다 (**파일**  - &gt; **새 프로젝트**) 선택 합니다 **ASP.NET 웹 응용 프로그램** 템플릿과 최신.NET Framework 버전을 **새 프로젝트** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="0bd72-121">Create a new project (**File** -&gt; **New Project**) and select the **ASP.NET Web Application** template and the latest .NET Framework version from the **New Project** dialog box.</span></span>
2. <span data-ttu-id="0bd72-122">**새 ASP.NET 프로젝트** 대화 상자를 선택 합니다 **Web Forms** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="0bd72-122">From the **New ASP.NET Project** dialog box, select the **Web Forms** template.</span></span> <span data-ttu-id="0bd72-123">기본 인증을 유지 **개별 사용자 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-123">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="0bd72-124">Azure에서 앱을 호스트 하려는 경우는 **클라우드에서 호스트** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-124">If you'd like to host the app in Azure, leave the **Host in the cloud** check box checked.</span></span>   
 <span data-ttu-id="0bd72-125">클릭 **확인** 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-125">Then, click **OK** to create the new project.</span></span>  
    <span data-ttu-id="0bd72-126">![새 ASP.NET 프로젝트 대화 상자](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0bd72-126">![New ASP.NET Project dialog box](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)</span></span>
3. <span data-ttu-id="0bd72-127">프로젝트에 대 한 Secure Sockets Layer (SSL)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-127">Enable Secure Sockets Layer (SSL) for the project.</span></span> <span data-ttu-id="0bd72-128">사용할 수 있는 단계를 수행 합니다 **프로젝트에 대 한 SSL을 사용 하도록 설정** 부분을 [Web Forms 자습서 시리즈를 시작 하기](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-128">Follow the steps available in the **Enable SSL for the Project** section of the [Getting Started with Web Forms tutorial series](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms).</span></span>
4. <span data-ttu-id="0bd72-129">앱 실행을 클릭 합니다 **등록** 에 연결 하 고 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-129">Run the app, click the **Register** link and register a new user.</span></span> <span data-ttu-id="0bd72-130">이 시점에서 전자 메일에만 유효성 검사는 기반으로 합니다 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 특성을 전자 메일 주소 형식이 올바른지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-130">At this point, the only validation on the email is based on the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute to ensure the email address is well-formed.</span></span> <span data-ttu-id="0bd72-131">전자 메일 확인을 추가 하는 코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-131">You will modify the code to add email confirmation.</span></span> <span data-ttu-id="0bd72-132">브라우저 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-132">Close the browser window.</span></span>
5. <span data-ttu-id="0bd72-133">**서버 탐색기** Visual studio (**뷰**  - &gt; **서버 탐색기**), 이동할 **데이터 Connections\ DefaultConnection\Tables\AspNetUsers**를 마우스 오른쪽 단추로 클릭 하 고 선택 **테이블 정의 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-133">In **Server Explorer** of Visual Studio (**View** -&gt; **Server Explorer**), navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span> 

    <span data-ttu-id="0bd72-134">다음 이미지는 `AspNetUsers` 테이블 스키마:</span><span class="sxs-lookup"><span data-stu-id="0bd72-134">The following image shows the `AspNetUsers` table schema:</span></span>

    ![AspNetUsers 테이블 스키마](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="0bd72-136">**서버 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **AspNetUsers** 선택한 테이블 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-136">In **Server Explorer**, right-click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
  
    ![AspNetUsers 테이블 데이터](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="0bd72-138">이 시점에서 등록 된 사용자에 대 한 전자 메일 확인 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-138">At this point the email for the registered user has not been confirmed.</span></span>
7. <span data-ttu-id="0bd72-139">행 및 삭제 하려면 삭제 선택에 사용자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-139">Click on the row and select delete to delete the user.</span></span> <span data-ttu-id="0bd72-140">다음 단계에서는이 전자 메일을 다시 추가 하 고 전자 메일 주소로 확인 메시지를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-140">You'll add this email again in the next step and send a confirmation message to the email address.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="0bd72-141">전자 메일 확인</span><span class="sxs-lookup"><span data-stu-id="0bd72-141">Email Confirmation</span></span>

<span data-ttu-id="0bd72-142">다른 사용자에 가장 하지 않는 것을 확인 하려면 새 사용자를 등록 하는 동안 전자 메일을 확인 하는 것이 좋습니다 (즉, 다른 사용자의 전자 메일을 사용 하 여 등록 하지 않은).</span><span class="sxs-lookup"><span data-stu-id="0bd72-142">It's a best practice to confirm the email during the registration of a new user to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="0bd72-143">방지 하려는 토론 포럼을 설치한 가정 `"bob@cpandl.com"` 로 등록에서 `"joe@contoso.com"`합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-143">Suppose you had a discussion forum, you would want to prevent `"bob@cpandl.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="0bd72-144">전자 메일 확인 하지 않고 `"joe@contoso.com"` 앱에서 원치 않는 전자 메일을 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-144">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="0bd72-145">Bob 실수로 등록 가정 `"bib@cpandl.com"` 를 눈치채 및 그 앱에 올바른 전자 메일 없는 때문에 암호 복구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-145">Suppose Bob accidently registered as `"bib@cpandl.com"` and hadn't noticed it, he wouldn't be able to use password recovery because the app doesn't have his correct email.</span></span> <span data-ttu-id="0bd72-146">전자 메일 확인은 봇부터에서만 제한 된 보호를 제공 하 고 결정된 스패머가에서 보호를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-146">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers.</span></span>

<span data-ttu-id="0bd72-147">일반적으로 새 사용자가 메일, SMS 문자 메시지 또는 다른 메커니즘 학인합니다 전에 웹 사이트에 데이터를 게시 하지 못하도록 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-147">You generally want to prevent new users from posting any data to your website before they have been confirmed by either email, an SMS text message or another mechanism.</span></span> <span data-ttu-id="0bd72-148">아래 섹션에서 전자 메일 확인을 사용 하도록 설정 하 고 새로 등록 된 사용자가 자신의 전자 메일 확인 될 때까지 로그인 하지 못하도록 하려면 코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-148">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span> <span data-ttu-id="0bd72-149">이 자습서에서는 SendGrid 메일 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-149">You'll use the email service SendGrid in this tutorial.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="0bd72-150">SendGrid 연결</span><span class="sxs-lookup"><span data-stu-id="0bd72-150">Hook up SendGrid</span></span>

<span data-ttu-id="0bd72-151">이 자습서에만 전자 메일 알림을 통해 추가 하는 방법을 보여 주지만 [SendGrid](http://sendgrid.com/), SMTP 및 다른 메커니즘을 사용 하 여 메일을 보낼 수 있습니다 (참조 [추가 리소스](#addRes)).</span><span class="sxs-lookup"><span data-stu-id="0bd72-151">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="0bd72-152">Visual Studio에서 엽니다는 **패키지 관리자 콘솔** (**도구**  - &gt; **NuGet 패키지 관리자**  - &gt; **패키지 관리자 콘솔**), 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-152">In Visual Studio, open the **Package Manager Console** (**Tools** -&gt; **NuGet Package Manger** -&gt; **Package Manager Console**), and enter the following command:</span></span>  
    `Install-Package SendGrid`
2. <span data-ttu-id="0bd72-153">로 이동 합니다 [Azure SendGrid 등록 페이지](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) SendGrid 계정을 무료로 등록 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-153">Go to the [Azure SendGrid sign-up page](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) and register for free SendGrid account.</span></span> <span data-ttu-id="0bd72-154">직접 무료 SendGrid 계정에도 등록할 수 있습니다 [SendGrid의 사이트](http://www.sendgrid.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-154">You can also sign-up for a free SendGrid account directly on [SendGrid's site](http://www.sendgrid.com).</span></span>
3. <span data-ttu-id="0bd72-155">**솔루션 탐색기** 열을 *IdentityConfig.cs* 파일을 *앱\_시작* 폴더 합니다 를노란색으로강조표시하는다음코드를추가`EmailService` 구성 하는 클래스 **SendGrid**:</span><span class="sxs-lookup"><span data-stu-id="0bd72-155">From **Solution Explorer** open the *IdentityConfig.cs* file in the *App\_Start* folder and add the following code highlighted in yellow to the `EmailService` class to configure **SendGrid**:</span></span>

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample1.cs?highlight=3,5,8-37)]
4. <span data-ttu-id="0bd72-156">또한 다음을 추가 `using` 명령문의 시작 부분에는 *IdentityConfig.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="0bd72-156">Also, add the following `using` statements to the beginning of the *IdentityConfig.cs* file:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample2.cs?highlight=1-4)]
5. <span data-ttu-id="0bd72-157">간단히 유지 하기 위해이 샘플에서 전자 메일 서비스 계정의 값을 저장 합니다 `appSettings` 의 섹션을 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-157">To keep this sample simple, you'll store the email service account values in the `appSettings` section of the *web.config* file.</span></span> <span data-ttu-id="0bd72-158">다음 XML을 노란색으로 강조 표시를 추가 합니다 *web.config* 프로젝트의 루트에 있는 파일:</span><span class="sxs-lookup"><span data-stu-id="0bd72-158">Add the following XML highlighted in yellow to the *web.config* file at the root of your project:</span></span>

    [!code-xml[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample3.xml?highlight=2-5)]

    > [!WARNING]
    > <span data-ttu-id="0bd72-159">보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-159">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="0bd72-160">이 예제에서는 계정 및 자격 증명에 저장 됩니다는 **appSetting** 섹션을 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-160">In this example, the account and credentials are stored in the **appSetting** section of the *Web.config* file.</span></span> <span data-ttu-id="0bd72-161">Azure에서 안전 하 게에 저장할 수 있습니다 이러한 값을 **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** Azure portal에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-161">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="0bd72-162">관련된 내용은 Rick Anderson의 항목을 참조 하세요 [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](https://go.microsoft.com/fwlink/?LinkId=513141)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-162">For related information see Rick Anderson's topic titled [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](https://go.microsoft.com/fwlink/?LinkId=513141).</span></span>
6. <span data-ttu-id="0bd72-163">SendGrid 인증 값 (사용자 이름 및 암호)을 수행할 수 있도록 성공적인에서 전자 메일 보내기 앱에 맞게 전자 메일 서비스 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-163">Add the email service values to reflect your SendGrid authentication values (User Name and Password) so that you can successful send email from your app.</span></span> <span data-ttu-id="0bd72-164">SendGrid를 제공한 전자 메일 주소가 아니라 SendGrid 계정 이름을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-164">Be sure to use your SendGrid account name rather than the email address you provided SendGrid.</span></span>

### <a name="enable-email-confirmation"></a><span data-ttu-id="0bd72-165">전자 메일 확인을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="0bd72-165">Enable Email Confirmation</span></span>

 <span data-ttu-id="0bd72-166">전자 메일 확인을 사용 하려면 다음 단계를 사용 하 여 등록 코드를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-166">To enable email confirmation, you'll modify the registration code using the following steps.</span></span>  
 

1. <span data-ttu-id="0bd72-167">에 *계정* 폴더를 열고 합니다 *Register.aspx.cs* 코드 숨김 및 업데이트는 `CreateUser_Click` 다음 강조 표시 된 변경 내용을 사용 하도록 설정 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="0bd72-167">In the *Account* folder, open the *Register.aspx.cs* code-behind and update the `CreateUser_Click` method to enable the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample4.cs?highlight=9-11)]
2. <span data-ttu-id="0bd72-168">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *Default.aspx* 선택한 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-168">In **Solution Explorer**, right-click *Default.aspx* and select **Set As Start Page**.</span></span>
3. <span data-ttu-id="0bd72-169">키를 눌러 앱을 실행 **F5입니다.**</span><span class="sxs-lookup"><span data-stu-id="0bd72-169">Run the app by pressing **F5.**</span></span> <span data-ttu-id="0bd72-170">페이지 표시 되 면 클릭 합니다 **등록** 등록 페이지를 표시 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-170">After the page is displayed, click the **Register** link to display the Register page.</span></span>
4. <span data-ttu-id="0bd72-171">전자 메일 및 암호를 입력 한 다음 클릭 합니다 **등록** 단추 SendGrid 통해 전자 메일 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-171">Enter your email and password, then click the **Register** button to send an email message via SendGrid.</span></span>  
   <span data-ttu-id="0bd72-172">프로젝트 및 코드의 현재 상태에는 로그인 등록 양식을 완료 되 면 해당 계정을 확인 하지 않은 것도 사용자 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-172">The current state of your project and code will allow the user to log in once they complete the registration form, even though they haven't confirmed their account.</span></span>
5. <span data-ttu-id="0bd72-173">전자 메일 계정을 확인 하 고 전자 메일을 확인 하려면 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-173">Check your email account and click on the link to confirm your email.</span></span>  
   <span data-ttu-id="0bd72-174">등록 양식을 제출 하면에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-174">Once you submit the registration form, you will be logged in.</span></span>  
    ![샘플 웹 사이트에 로그인](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image4.png)

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="0bd72-176">로그인 하기 전에 전자 메일 확인 필요</span><span class="sxs-lookup"><span data-stu-id="0bd72-176">Require Email Confirmation Before Log In</span></span>

<span data-ttu-id="0bd72-177">전자 메일 계정에 확인 했으면 있지만 이때 하지 해야에 완전히 서명 된 확인 전자 메일에 포함 된 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-177">Although you have confirmed the email account, at this point you would not need to click on the link contained in the verification email to be fully signed-in.</span></span> <span data-ttu-id="0bd72-178">다음 섹션에서는 새 사용자 기록 하기 전에 전자 메일을 확인된 하도록 (인증)를 요구 하는 코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-178">In the following section, you will modify the code requiring new users to have a confirmed email before they are logged in (authenticated).</span></span>

1. <span data-ttu-id="0bd72-179">**솔루션 탐색기** Visual Studio의 업데이트를 `CreateUser_Click` 이벤트에는 *Register.aspx.cs* 코드 숨김에 포함 된 합니다 *계정* 폴더는 다음 강조 표시 된 변경 내용:</span><span class="sxs-lookup"><span data-stu-id="0bd72-179">In **Solution Explorer** of Visual Studio, update the `CreateUser_Click` event in the *Register.aspx.cs* code-behind contained in the *Accounts* folder with the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample5.cs?highlight=13-14,17-21)]
2. <span data-ttu-id="0bd72-180">업데이트를 `LogIn` 의 메서드를 *Login.aspx.cs* 다음 강조 표시 된 변경 내용으로 코드 숨김:</span><span class="sxs-lookup"><span data-stu-id="0bd72-180">Update the `LogIn` method in the *Login.aspx.cs* code-behind with the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample6.cs?highlight=9-19,45-46)]

### <a name="run-the-application"></a><span data-ttu-id="0bd72-181">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="0bd72-181">Run the Application</span></span>

 <span data-ttu-id="0bd72-182">사용자의 전자 메일 주소 확인 되었는지 여부를 확인 하는 코드를 구현한 했으므로 둘 다에서 기능을 확인할 수 있습니다는 **등록할** 하 고 **로그인** 페이지.</span><span class="sxs-lookup"><span data-stu-id="0bd72-182">Now that you have implemented the code to check whether a user's email address has been confirmed, you can check the functionality on both the **Register** and **Login** pages.</span></span> 

1. <span data-ttu-id="0bd72-183">모든 계정을 삭제 합니다 **AspNetUsers** 테스트 하려는 전자 메일 별칭을 포함 하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-183">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test.</span></span>
2. <span data-ttu-id="0bd72-184">앱을 실행 합니다 (**F5**) 확인 전자 메일 주소 확인 될 때까지 사용자로 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-184">Run the app (**F5**) and verify you cannot register as a user until you have confirmed your email address.</span></span>
3. <span data-ttu-id="0bd72-185">방금 보낸 전자 메일을 통해 새 계정의 확인 하기 전에 새 계정으로 로그인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-185">Before confirming your new account via the email that was just sent, attempt to log in with the new account.</span></span>  
 <span data-ttu-id="0bd72-186">로그인 할 수 없는 확인된 전자 메일 계정이 있어야 하 고 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-186">You'll see that you are unable to log in and that you must have a confirmed email account.</span></span>
4. <span data-ttu-id="0bd72-187">전자 메일 주소를 확인 하 고 나면 앱에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-187">Once you confirm your email address, log in to the app.</span></span>

<a id="reset"></a>
## <a name="password-recovery-and-reset"></a><span data-ttu-id="0bd72-188">암호 복구 및 다시 설정</span><span class="sxs-lookup"><span data-stu-id="0bd72-188">Password Recovery and Reset</span></span>

1. <span data-ttu-id="0bd72-189">Visual Studio에서 주석 문자를 제거 합니다 `Forgot` 에서 메서드를 *Forgot.aspx.cs* 코드 숨김에 포함 된를 *계정* 폴더 메서드도 나타나도록 따릅니다:</span><span class="sxs-lookup"><span data-stu-id="0bd72-189">In Visual Studio, remove the comment characters from the `Forgot` method in the *Forgot.aspx.cs* code-behind contained in the *Account* folder, so that the method appears as follows:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample7.cs?highlight=16-18)]
2. <span data-ttu-id="0bd72-190">엽니다는 *Login.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-190">Open the *Login.aspx* page.</span></span> <span data-ttu-id="0bd72-191">끝 태그를 대체 합니다 **loginForm** 아래 강조 표시 된 대로 섹션:</span><span class="sxs-lookup"><span data-stu-id="0bd72-191">Replace the markup near the end of the **loginForm** section as highlighted below:</span></span> 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample8.aspx?highlight=52-53)]
3. <span data-ttu-id="0bd72-192">엽니다는 *Login.aspx.cs* 코드 숨김 및에서 노란색으로 강조 표시 하는 코드의 다음 줄을 주석 처리 제거를 `Page_Load` 이벤트 처리기:</span><span class="sxs-lookup"><span data-stu-id="0bd72-192">Open the *Login.aspx.cs* code-behind and uncomment the following line of code highlighted in yellow from the `Page_Load` event handler:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample9.cs?highlight=5)]
4. <span data-ttu-id="0bd72-193">키를 눌러 앱을 실행 **F5입니다.**</span><span class="sxs-lookup"><span data-stu-id="0bd72-193">Run the app by pressing **F5.**</span></span> <span data-ttu-id="0bd72-194">페이지 표시 되 면 클릭 합니다 **로그인** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-194">After the page is displayed, click the **Log in** link.</span></span>
5. <span data-ttu-id="0bd72-195">클릭 합니다 **암호를 잊으셨나요?** 표시할 링크는 **암호를 잊으셨습니까** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-195">Click the **Forgot your password?** link to display the **Forgot Password** page.</span></span>
6. <span data-ttu-id="0bd72-196">전자 메일 주소를 입력 하 고 클릭 합니다 **제출** 단추 암호를 재설정할 수 있는 주소로 전자 메일을 보내려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-196">Enter your email address and click the **Submit** button to send an email to your address which will allow you to reset your password.</span></span>   
   <span data-ttu-id="0bd72-197">전자 메일 계정을 확인 하 고 표시할 링크를 클릭 합니다 **암호 재설정** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-197">Check your email account and click on the link to display the **Reset Password** page.</span></span>
7. <span data-ttu-id="0bd72-198">에 **암호 재설정** 페이지에서 사용자 전자 메일, 암호 및 확인된 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-198">On the **Reset Password** page, enter your email, password, and confirmed password.</span></span> <span data-ttu-id="0bd72-199">그런 다음 키를 눌러 합니다 **재설정** 단추.</span><span class="sxs-lookup"><span data-stu-id="0bd72-199">Then, press the **Reset** button.</span></span>  
   <span data-ttu-id="0bd72-200">성공적으로 암호를 재설정 하는 경우는 **암호가 변경** 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-200">When you successfully reset your password, the **Password Changed** page will be displayed.</span></span> <span data-ttu-id="0bd72-201">이제 새 암호를 사용 하 여 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-201">Now you can log in with your new password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="0bd72-202">전자 메일 확인 링크 다시 보내기</span><span class="sxs-lookup"><span data-stu-id="0bd72-202">Resend Email Confirmation Link</span></span>

<span data-ttu-id="0bd72-203">사용자는 새 로컬 계정을 만들고 나면 로그온 하기 전에 사용 해야 하는 확인 링크를 전자 메일로 전송 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-203">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="0bd72-204">사용자 실수로 삭제 확인 전자 메일 또는 전자 메일 절대 도착 하는 경우 확인 링크 다시 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-204">If the user accidently deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="0bd72-205">코드 변경에는이 기능을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-205">The following code changes show how to enable this.</span></span>

1. <span data-ttu-id="0bd72-206">Visual Studio에서 엽니다는 **Login.aspx.cs** 코드 숨김 및 후 다음 이벤트 처리기를 추가 합니다 `LogIn` 이벤트 처리기:</span><span class="sxs-lookup"><span data-stu-id="0bd72-206">In Visual Studio, open the **Login.aspx.cs** code-behind and add the following event handler after the `LogIn` event handler:</span></span>   

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample10.cs)]
2. <span data-ttu-id="0bd72-207">수정 된 `LogIn` 이벤트 처리기는 *Login.aspx.cs* 같이 노란색으로 강조 표시 된 코드를 변경 하 여 코드 숨김:</span><span class="sxs-lookup"><span data-stu-id="0bd72-207">Modify the `LogIn` event handler in the *Login.aspx.cs* code-behind by changing the code highlighted in yellow as follows:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample11.cs?highlight=15-17)]
3. <span data-ttu-id="0bd72-208">업데이트를 *Login.aspx* 같이 노란색으로 강조 표시 된 코드를 추가 하 여 페이지:</span><span class="sxs-lookup"><span data-stu-id="0bd72-208">Update the *Login.aspx* page by adding the code highlighted in yellow as follows:</span></span> 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample12.aspx?highlight=45-46)]
4. <span data-ttu-id="0bd72-209">모든 계정을 삭제 합니다 **AspNetUsers** 테스트 하려는 전자 메일 별칭을 포함 하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-209">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test.</span></span>
5. <span data-ttu-id="0bd72-210">앱을 실행 합니다 (**F5**) 및 전자 메일 주소를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-210">Run the app (**F5**) and register your email address.</span></span>
6. <span data-ttu-id="0bd72-211">방금 보낸 전자 메일을 통해 새 계정의 확인 하기 전에 새 계정으로 로그인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-211">Before confirming your new account via the email that was just sent, attempt to log in with the new account.</span></span>  
   <span data-ttu-id="0bd72-212">로그인 할 수 없는 확인된 전자 메일 계정이 있어야 하 고 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-212">You'll see that you are unable to log in and that you must have a confirmed email account.</span></span> <span data-ttu-id="0bd72-213">또한 이제 다시 보낼 수 있습니다 확인 메시지를 전자 메일 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-213">In addition, you can now resend a confirmation message to your email account.</span></span>
7. <span data-ttu-id="0bd72-214">전자 메일 주소와 암호를 입력 누릅니다 합니다 **확인 다시 전송** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-214">Enter your email address and password, then press the **Resend confirmation** button.</span></span>
8. <span data-ttu-id="0bd72-215">새로 보낸된 전자 메일 메시지에 따라 전자 메일 주소를 확인 하 고 나면 앱에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-215">Once you confirm your email address based on the newly sent email message, log in to the app.</span></span>

<a id="dbg"></a>
## <a name="troubleshooting-the-app"></a><span data-ttu-id="0bd72-216">앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="0bd72-216">Troubleshooting the App</span></span>

<span data-ttu-id="0bd72-217">자격 증명을 확인 링크가 포함 된 전자 메일을 받지 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="0bd72-217">If you don't receive an email containing the link to verify your credentials:</span></span>

- <span data-ttu-id="0bd72-218">정크 또는 스팸 폴더를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-218">Check your junk or spam folder.</span></span>
- <span data-ttu-id="0bd72-219">SendGrid 계정에 로그인 하 고 클릭 합니다 [전자 메일 작업 링크](https://sendgrid.com/logs/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-219">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>
- <span data-ttu-id="0bd72-220">SendGrid 사용자 계정 이름으로 사용한 특정 수를 *Web.config* SendGrid 계정 전자 메일 주소 대신 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0bd72-220">Be certain you used your SendGrid user account name as a *Web.config* value rather than your SendGrid account email address.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="0bd72-221">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0bd72-221">Additional Resources</span></span>

- [<span data-ttu-id="0bd72-222">링크를 ASP.NET Id 권장 리소스</span><span class="sxs-lookup"><span data-stu-id="0bd72-222">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [<span data-ttu-id="0bd72-223">계정 확인 및 ASP.NET Id와 암호 복구</span><span class="sxs-lookup"><span data-stu-id="0bd72-223">Account Confirmation and Password Recovery with ASP.NET Identity</span></span>](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [<span data-ttu-id="0bd72-224">ASP.NET Web Forms 자습서 시리즈-OAuth 2.0 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="0bd72-224">ASP.NET Web Forms tutorial series - Add an OAuth 2.0 Provider</span></span>](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [<span data-ttu-id="0bd72-225">멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET Web Forms 앱을 Azure App Service에 배포</span><span class="sxs-lookup"><span data-stu-id="0bd72-225">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [<span data-ttu-id="0bd72-226">ASP.NET Web Forms 자습서 시리즈-프로젝트에 대 한 SSL을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="0bd72-226">ASP.NET Web Forms tutorial series - Enable SSL for the Project</span></span>](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
