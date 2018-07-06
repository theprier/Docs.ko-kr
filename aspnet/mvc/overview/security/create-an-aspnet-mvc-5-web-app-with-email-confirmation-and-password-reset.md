---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: 전자 메일 확인 및 암호 재설정 기능이 (C#), 로그를 사용 하 여 보안 ASP.NET MVC 5 웹 앱 만들기 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 전자 메일 확인 및 ASP.NET Id 멤버 자격 시스템을 사용 하 여 암호를 사용 하 여 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다. Ca는 중...
ms.author: aspnetcontent
ms.date: 03/26/2015
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 1387c3e9c03e011b610a070aa0c273ded23b463e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823549"
---
<a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a><span data-ttu-id="e62c8-104">전자 메일 확인 및 암호 재설정 기능이 (C#), 로그를 사용 하 여 보안 ASP.NET MVC 5 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e62c8-104">Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset (C#)</span></span>
====================
<span data-ttu-id="e62c8-105">[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="e62c8-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="e62c8-106">이 자습서에서는 전자 메일 확인 및 ASP.NET Id 멤버 자격 시스템을 사용 하 여 암호를 사용 하 여 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with email confirmation and password reset using the ASP.NET Identity membership system.</span></span> <span data-ttu-id="e62c8-107">완성된 된 응용 프로그램을 다운로드할 수 있습니다 [여기](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-107">You can download the completed application [here](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="e62c8-108">다운로드는 전자 메일 또는 SMS 공급자를 설정 하지 않고 SMS 및 전자 메일 확인을 테스트할 수 있도록 디버깅 도우미를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-108">The download contains debugging helpers that let you test email confirmation and SMS without setting up an email or SMS provider.</span></span>
> 
> <span data-ttu-id="e62c8-109">이 자습서를 통해 작성 했습니다 [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="e62c8-109">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>


<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="e62c8-110">ASP.NET MVC 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e62c8-110">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="e62c8-111">설치 및 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 하거나 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-111">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="e62c8-112">설치할 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상.</span><span class="sxs-lookup"><span data-stu-id="e62c8-112">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="e62c8-113">: 경고를 설치 해야 합니다 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상이 자습서를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-113">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>


1. <span data-ttu-id="e62c8-114">새 ASP.NET 웹 프로젝트를 만들고 MVC 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-114">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="e62c8-115">또한 web Forms web forms 앱에서 비슷한 단계를 수행할 수 있도록 ASP.NET Id를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-115">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. <span data-ttu-id="e62c8-116">기본 인증을 유지 **개별 사용자 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-116">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="e62c8-117">Azure에서 앱을 호스트 하려는 경우 확인란을 선택한 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-117">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="e62c8-118">자습서의 뒷부분에 나오는 Azure에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-118">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="e62c8-119">할 수 있습니다 [Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-119">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="e62c8-120">설정 된 [SSL을 사용 하도록 프로젝트](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-120">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="e62c8-121">앱 실행을 클릭 합니다 **등록** 에 연결 하 고 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-121">Run the app, click the **Register** link and register a user.</span></span> <span data-ttu-id="e62c8-122">이 시점에서 전자 메일에만 유효성 검사 된 합니다 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-122">At this point, the only validation on the email is with the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute.</span></span>
5. <span data-ttu-id="e62c8-123">서버 탐색기에서로 이동 **데이터 Connections\DefaultConnection\Tables\AspNetUsers**, 마우스 오른쪽 단추로 클릭 하 고 선택 **테이블 정의 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-123">In Server Explorer, navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span>

    <span data-ttu-id="e62c8-124">다음 이미지는 `AspNetUsers` 스키마:</span><span class="sxs-lookup"><span data-stu-id="e62c8-124">The following image shows the `AspNetUsers` schema:</span></span>

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="e62c8-125">마우스 오른쪽 단추로 클릭 합니다 **AspNetUsers** 선택한 테이블 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-125">Right click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="e62c8-126">이 시점에서 전자 메일 확인 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-126">At this point the email has not been confirmed.</span></span>
7. <span data-ttu-id="e62c8-127">행을 클릭 하 고 삭제를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-127">Click on the row and select delete.</span></span> <span data-ttu-id="e62c8-128">다음 단계에서는이 전자 메일을 다시 추가 하 고 확인 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-128">You'll add this email again in the next step, and send a confirmation email.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="e62c8-129">전자 메일 확인</span><span class="sxs-lookup"><span data-stu-id="e62c8-129">Email confirmation</span></span>

<span data-ttu-id="e62c8-130">다른 사용자에 가장 하지 않는 것을 확인 하려면 새 사용자 등록 전자 메일을 확인 하는 것이 좋습니다 (즉, 다른 사용자의 전자 메일을 사용 하 여 등록 하지 않은).</span><span class="sxs-lookup"><span data-stu-id="e62c8-130">It's a best practice to confirm the email of a new user registration to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="e62c8-131">방지 하려는 토론 포럼을 설치한 가정 `"bob@example.com"` 로 등록에서 `"joe@contoso.com"`합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-131">Suppose you had a discussion forum, you would want to prevent `"bob@example.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="e62c8-132">전자 메일 확인 하지 않고 `"joe@contoso.com"` 앱에서 원치 않는 전자 메일을 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-132">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="e62c8-133">Bob 실수로 등록 가정 `"bib@example.com"` 를 눈치채 및 그 앱에 올바른 전자 메일 없는 때문에 암호 복구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-133">Suppose Bob accidently registered as `"bib@example.com"` and hadn't noticed it, he wouldn't be able to use password recover because the app doesn't have his correct email.</span></span> <span data-ttu-id="e62c8-134">전자 메일 확인은 봇부터에서만 제한 된 보호를 제공 하며 결정된 스패머가에서 보호를 제공 하지 않습니다, 그리고 여러 작업 전자 메일 별칭을 등록 하는 데 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-134">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers, they have many working email aliases they can use to register.</span></span>

<span data-ttu-id="e62c8-135">일반적으로 새 사용자가 전자 메일, SMS 문자 메시지 또는 다른 메커니즘을 통해 학인합니다 전에 웹 사이트에 데이터를 게시 하지 못하도록 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-135">You generally want to prevent new users from posting any data to your web site before they have been confirmed by email, a SMS text message or another mechanism.</span></span> <a id="build"></a><span data-ttu-id="e62c8-136">아래 섹션에서 전자 메일 확인을 사용 하도록 설정 하 고 새로 등록 된 사용자가 자신의 전자 메일 확인 될 때까지 로그인 하지 못하도록 하려면 코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-136">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="e62c8-137">SendGrid 연결</span><span class="sxs-lookup"><span data-stu-id="e62c8-137">Hook up SendGrid</span></span>

<span data-ttu-id="e62c8-138">이 자습서에만 전자 메일 알림을 통해 추가 하는 방법을 보여 주지만 [SendGrid](http://sendgrid.com/), SMTP 및 다른 메커니즘을 사용 하 여 메일을 보낼 수 있습니다 (참조 [추가 리소스](#addRes)).</span><span class="sxs-lookup"><span data-stu-id="e62c8-138">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="e62c8-139">패키지 관리자 콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-139">In the Package Manager Console, enter the following command:</span></span> 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. <span data-ttu-id="e62c8-140">로 이동 합니다 [Azure SendGrid 등록 페이지](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) 무료 SendGrid 계정을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-140">Go to the [Azure SendGrid sign up page](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) and register for a free SendGrid account.</span></span> <span data-ttu-id="e62c8-141">에 다음과 비슷한 코드를 추가 하 여 SendGrid 구성할 *App_Start/IdentityConfig.cs*:</span><span class="sxs-lookup"><span data-stu-id="e62c8-141">Configure SendGrid by adding code similar to the following in *App_Start/IdentityConfig.cs*:</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

<span data-ttu-id="e62c8-142">다음 include 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-142">You'll need to add the following includes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

<span data-ttu-id="e62c8-143">간단히 유지 하기 위해이 샘플의 앱 설정을 저장 합니다 *web.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="e62c8-143">To keep this sample simple, we'll store the app settings in the *web.config* file:</span></span>

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> <span data-ttu-id="e62c8-144">보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-144">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="e62c8-145">계정 및 자격 증명 appSetting에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-145">The account and credentials are stored in the appSetting.</span></span> <span data-ttu-id="e62c8-146">Azure에서 안전 하 게에 저장할 수 있습니다 이러한 값을 **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** Azure portal에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-146">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="e62c8-147">참조 [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-147">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>


### <a name="enable-email-confirmation-in-the-account-controller"></a><span data-ttu-id="e62c8-148">Account 컨트롤러의 전자 메일 확인을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="e62c8-148">Enable email confirmation in the Account controller</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

<span data-ttu-id="e62c8-149">확인 합니다 *Views\Account\ConfirmEmail.cshtml* 파일에 올바른 razor 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-149">Verify the *Views\Account\ConfirmEmail.cshtml* file has correct razor syntax.</span></span> <span data-ttu-id="e62c8-150">(의 첫 번째에서 문자 @ 줄 누락 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-150">( The @ character in the first line might be missing.</span></span> <span data-ttu-id="e62c8-151">)</span><span class="sxs-lookup"><span data-stu-id="e62c8-151">)</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="e62c8-152">앱을 실행 하 고 등록 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-152">Run the app and click the Register link.</span></span> <span data-ttu-id="e62c8-153">등록 양식을 제출 하면 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-153">Once you submit the registration form, you are logged in.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

<span data-ttu-id="e62c8-154">전자 메일 계정을 확인 하 고 전자 메일을 확인 하려면 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-154">Check your email account and click on the link to confirm your email.</span></span>

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="e62c8-155">로그인 하기 전에 전자 메일 확인 필요</span><span class="sxs-lookup"><span data-stu-id="e62c8-155">Require email confirmation before log in</span></span>

<span data-ttu-id="e62c8-156">사용자 등록 양식을 완료 된 후에 현재으로 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-156">Currently once a user completes the registration form, they are logged in.</span></span> <span data-ttu-id="e62c8-157">일반적으로 기록 하기 전에 전자 메일을 확인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-157">You generally want to confirm their email before logging them in.</span></span> <span data-ttu-id="e62c8-158">아래 섹션에서 새 사용자 기록 하기 전에 전자 메일을 확인된 하도록 (인증)를 요구 하도록 코드를 수정 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-158">In the section below, we will modify the code to require new users to have a confirmed email before they are logged in (authenticated).</span></span> <span data-ttu-id="e62c8-159">업데이트 된 `HttpPost Register` 메서드를 다음 강조 표시 된 변경 내용으로:</span><span class="sxs-lookup"><span data-stu-id="e62c8-159">Update the `HttpPost Register` method with the following highlighted changes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

<span data-ttu-id="e62c8-160">주석는 `SignInAsync` 메서드, 사용자를 등록 하 여 로그인 하지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-160">By commenting out the `SignInAsync` method, the user will not be signed in by the registration.</span></span> <span data-ttu-id="e62c8-161">`TempData["ViewBagLink"] = callbackUrl;` 줄에 사용할 수 있습니다 [앱을 디버그할](#dbg) 및 전자 메일을 보내지 않고 등록을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-161">The `TempData["ViewBagLink"] = callbackUrl;` line can be used to [debug the app](#dbg) and test registration without sending email.</span></span> <span data-ttu-id="e62c8-162">`ViewBag.Message` 확인 지침을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-162">`ViewBag.Message` is used to display the confirm instructions.</span></span> <span data-ttu-id="e62c8-163">합니다 [샘플을 다운로드](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) 전자 메일을 설정 하지 않고 전자 메일 확인을 테스트 하는 코드를 포함 하 고 응용 프로그램 디버깅에 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-163">The [download sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) contains code to test email confirmation without setting up email, and can also be used to debug the application.</span></span>

<span data-ttu-id="e62c8-164">만들기는 `Views\Shared\Info.cshtml` 파일과 다음 razor 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-164">Create a `Views\Shared\Info.cshtml` file and add the following razor markup:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

<span data-ttu-id="e62c8-165">추가 된 [Authorize 특성](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) 에 `Contact` Home 컨트롤러의 동작 메서드.</span><span class="sxs-lookup"><span data-stu-id="e62c8-165">Add the [Authorize attribute](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) to the `Contact` action method of the Home controller.</span></span> <span data-ttu-id="e62c8-166">클릭할 수 있습니다 합니다 **연락처** 익명 사용자가 액세스할 수 없는 및 인증 된 사용자에 대 한 액세스 권한이 확인 하기 위한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-166">You can click on the **Contact** link to verify anonymous users don't have access and authenticated users do have access.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

<span data-ttu-id="e62c8-167">업데이트 해야 합니다 `HttpPost Login` 작업 메서드:</span><span class="sxs-lookup"><span data-stu-id="e62c8-167">You must also update the `HttpPost Login` action method:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

<span data-ttu-id="e62c8-168">업데이트를 *Views\Shared\Error.cshtml* 오류 메시지를 표시 하려면 보기:</span><span class="sxs-lookup"><span data-stu-id="e62c8-168">Update the *Views\Shared\Error.cshtml* view to display the error message:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

<span data-ttu-id="e62c8-169">모든 계정을 삭제 합니다 **AspNetUsers** 테스트 하려는 전자 메일 별칭을 포함 하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-169">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test with.</span></span> <span data-ttu-id="e62c8-170">앱을 실행 하 고 전자 메일 주소 확인 될 때까지 로그인 할 수 없습니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-170">Run the app and verify you can't log in until you have confirmed your email address.</span></span> <span data-ttu-id="e62c8-171">전자 메일 주소 확인을 클릭 합니다 **연락처** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-171">Once you confirm your email address, click the **Contact** link.</span></span>

<a id="reset"></a>
## <a name="password-recoveryreset"></a><span data-ttu-id="e62c8-172">암호 복구/재설정</span><span class="sxs-lookup"><span data-stu-id="e62c8-172">Password recovery/reset</span></span>

<span data-ttu-id="e62c8-173">주석 문자를 제거 합니다 `HttpPost ForgotPassword` account 컨트롤러의 동작 메서드:</span><span class="sxs-lookup"><span data-stu-id="e62c8-173">Remove the comment characters from the `HttpPost ForgotPassword` action method in the account controller:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

<span data-ttu-id="e62c8-174">주석 문자를 제거 합니다 `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) 에 *Views\Account\Login.cshtml* razor 뷰 파일:</span><span class="sxs-lookup"><span data-stu-id="e62c8-174">Remove the comment characters from the `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) in the *Views\Account\Login.cshtml* razor view file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

<span data-ttu-id="e62c8-175">로그인 페이지가 암호 재설정에 대 한 링크가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-175">The Log in page will now show a link to reset the password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="e62c8-176">전자 메일 확인 링크 다시 보내기</span><span class="sxs-lookup"><span data-stu-id="e62c8-176">Resend email confirmation link</span></span>

<span data-ttu-id="e62c8-177">사용자는 새 로컬 계정을 만들고 나면 로그온 하기 전에 사용 해야 하는 확인 링크를 전자 메일로 전송 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-177">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="e62c8-178">사용자 실수로 삭제 확인 전자 메일 또는 전자 메일 절대 도착 하는 경우 확인 링크 다시 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-178">If the user accidently deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="e62c8-179">코드 변경에는이 기능을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-179">The following code changes show how to enable this.</span></span>

<span data-ttu-id="e62c8-180">맨 아래에 다음 도우미 메서드를 추가 합니다 *controllers\ accountcontroller.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="e62c8-180">Add the following helper method to the bottom of the *Controllers\AccountController.cs* file:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

<span data-ttu-id="e62c8-181">새 도우미를 사용 하도록 등록 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-181">Update the Register method to use the new helper:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

<span data-ttu-id="e62c8-182">사용자 계정이 확인 되지 않았습니다 하는 경우 암호를 다시 보내려고 로그인 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-182">Update the Login method to resend the password if the user account has not been confirmed:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="e62c8-183">로컬 및 소셜 로그인 계정을 병합합니다</span><span class="sxs-lookup"><span data-stu-id="e62c8-183">Combine social and local login accounts</span></span>

<span data-ttu-id="e62c8-184">로컬 및 소셜 계정 전자 메일 링크를 클릭 하 여 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-184">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="e62c8-185">다음 순서로 **RickAndMSFT@gmail.com** 로컬 로그인으로 처음 만들어질가 첫 번째는 소셜 로그인으로 계정을 만든 다음 로컬 로그인을 추가 하지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-185">In the following sequence **RickAndMSFT@gmail.com** is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

<span data-ttu-id="e62c8-186">클릭 합니다 **관리** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-186">Click on the **Manage** link.</span></span> <span data-ttu-id="e62c8-187">참고 합니다 **외부 로그인: 0** 이 계정과 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-187">Note the **External Logins: 0** associated with this account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

<span data-ttu-id="e62c8-188">서비스에서 다른 로그에 대 한 링크를 클릭 하 고 앱 요청을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-188">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="e62c8-189">두 개의 계정을 결합 되었습니다, 그리고 두 계정으로 로그온 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-189">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="e62c8-190">사용자가 소셜 로그인 인증 서비스를 중단 되었거나 가능성이 소셜 계정에 대 한 액세스를 손실가 되는 경우 로컬 계정에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-190">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="e62c8-191">다음 그림과에서 Tom은 소셜 로그인 (에서 볼 수 있는 합니다 **외부 로그인: 1** 페이지에 표시).</span><span class="sxs-lookup"><span data-stu-id="e62c8-191">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

<span data-ttu-id="e62c8-192">클릭할 **암호 선택** 동일한 계정에 연결 된 로컬 로그에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-192">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a><span data-ttu-id="e62c8-193">좀 더 깊이 전자 메일 확인</span><span class="sxs-lookup"><span data-stu-id="e62c8-193">Email confirmation in more depth</span></span>

<span data-ttu-id="e62c8-194">내 자습서 [계정 확인 및 ASP.NET Id와 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 자세한 세부 정보를 사용 하 여이 항목을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-194">My tutorial [Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) goes into this topic with more details.</span></span>

<a id="dbg"></a>
## <a name="debugging-the-app"></a><span data-ttu-id="e62c8-195">앱 디버깅</span><span class="sxs-lookup"><span data-stu-id="e62c8-195">Debugging the app</span></span>

<span data-ttu-id="e62c8-196">링크를 포함 하는 전자 메일을 얻지 못한 경우:</span><span class="sxs-lookup"><span data-stu-id="e62c8-196">If you don't get an email containing the link:</span></span>

- <span data-ttu-id="e62c8-197">정크 또는 스팸 폴더를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-197">Check your junk or spam folder.</span></span>
- <span data-ttu-id="e62c8-198">SendGrid 계정에 로그인 하 고 클릭 합니다 [전자 메일 작업 링크](https://sendgrid.com/logs/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-198">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>

<span data-ttu-id="e62c8-199">전자 메일 주소가 없음 확인 링크를 테스트 하려면 다운로드 합니다 [완성 된 샘플](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-199">To test the verification link without email, download the [completed sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="e62c8-200">확인 링크 및 확인 코드 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-200">The confirmation link and confirmation codes will be displayed on the page.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="e62c8-201">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e62c8-201">Additional Resources</span></span>

- [<span data-ttu-id="e62c8-202">링크를 ASP.NET Id 권장 리소스</span><span class="sxs-lookup"><span data-stu-id="e62c8-202">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="e62c8-203">[계정 확인 및 ASP.NET Id와 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 암호 복구 및 계정 확인에 대 한 자세한 내용으로 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-203">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="e62c8-204">[Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on을 사용 하 여 MVC 5 앱](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 이 자습서에서는 Facebook 및 Google OAuth 2 권한 부여를 사용 하 여 ASP.NET MVC 5 앱을 작성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-204">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="e62c8-205">또한 Id 데이터베이스에 데이터를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-205">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="e62c8-206">[멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET MVC 앱을 Azure에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-206">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="e62c8-207">이 자습서는 Azure 배포 추가 역할을 사용 하 여 앱을 보호 하는 방법을 멤버 자격 API를 사용 하 여 사용자 및 역할 및 추가 보안 기능을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e62c8-207">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="e62c8-208">OAuth 2 용 Google 앱 만들기 및 앱 프로젝트에 연결</span><span class="sxs-lookup"><span data-stu-id="e62c8-208">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="e62c8-209">Facebook에서 앱을 만들고 앱 프로젝트에 연결</span><span class="sxs-lookup"><span data-stu-id="e62c8-209">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="e62c8-210">프로젝트의 SSL 설정</span><span class="sxs-lookup"><span data-stu-id="e62c8-210">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
