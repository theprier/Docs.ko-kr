---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: "확인 및 암호 재설정 (C#) 전자 메일을 로그와 함께 보안 ASP.NET MVC 5 웹 앱 만들기 | Microsoft Docs"
author: Rick-Anderson
description: "이 자습서에서는 전자 메일 확인 및 암호 재설정 ASP.NET Identity 멤버 자격 시스템을 사용 하 여 ASP.NET MVC 5 웹 응용 프로그램을 구축 하는 방법을 보여 줍니다. Ca 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/26/2015
ms.topic: article
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: e3d8ad6e00b7fcb95f1c9bbe556021269c1a0624
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a><span data-ttu-id="15d9a-104">확인 및 암호 재설정 (C#) 전자 메일을 로그와 함께 보안 ASP.NET MVC 5 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="15d9a-104">Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset (C#)</span></span>
====================
<span data-ttu-id="15d9a-105">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="15d9a-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="15d9a-106">이 자습서에서는 전자 메일 확인 및 암호 재설정 ASP.NET Identity 멤버 자격 시스템을 사용 하 여 ASP.NET MVC 5 웹 응용 프로그램을 구축 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with email confirmation and password reset using the ASP.NET Identity membership system.</span></span> <span data-ttu-id="15d9a-107">완성 된 응용 프로그램을 다운로드할 수 있습니다 [여기](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-107">You can download the completed application [here](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="15d9a-108">다운로드는 전자 메일 또는 SMS 공급자를 설정 하지 않고 전자 메일 확인 및 SMS를 테스트할 수 있도록 하는 디버깅 도우미를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-108">The download contains debugging helpers that let you test email confirmation and SMS without setting up an email or SMS provider.</span></span>
> 
> <span data-ttu-id="15d9a-109">이 자습서에 의해 작성 되었으므로 [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="15d9a-109">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>


<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="15d9a-110">ASP.NET MVC 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="15d9a-110">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="15d9a-111">설치 하 고 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-111">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="15d9a-112">설치 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상.</span><span class="sxs-lookup"><span data-stu-id="15d9a-112">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="15d9a-113">경고:를 설치 해야 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 하려면이 자습서를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-113">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>


1. <span data-ttu-id="15d9a-114">새 ASP.NET 웹 프로젝트를 만들고 MVC 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-114">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="15d9a-115">Web Forms web forms 응용 프로그램에서 비슷한 단계를 반영할 수 있도록 ASP.NET Id를도 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-115">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. <span data-ttu-id="15d9a-116">기본 인증을 두고 **개별 사용자 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-116">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="15d9a-117">Azure에서 응용 프로그램 호스트 하려는 경우 확인란을 선택한 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-117">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="15d9a-118">이 자습서의 뒷부분에 나오는에서는 Azure에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-118">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="15d9a-119">있습니다 수 [무료로 Azure 계정을 개설](https://azure.microsoft.com/en-us/pricing/free-trial/?WT.mc_id=A261C142F)합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-119">You can [open an Azure account for free](https://azure.microsoft.com/en-us/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="15d9a-120">설정의 [SSL을 사용 하도록 프로젝트](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-120">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="15d9a-121">응용 프로그램 실행을 클릭는 **등록** 에 연결 하 고 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-121">Run the app, click the **Register** link and register a user.</span></span> <span data-ttu-id="15d9a-122">전자 메일에만 유효성 검사와는 시점에서 [[EmailAddress]](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-122">At this point, the only validation on the email is with the [[EmailAddress]](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute.</span></span>
5. <span data-ttu-id="15d9a-123">서버 탐색기에서로 이동 **데이터 Connections\DefaultConnection\Tables\AspNetUsers**를 마우스 오른쪽 단추로 클릭 하 고 **테이블 정의 열고**합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-123">In Server Explorer, navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span>

    <span data-ttu-id="15d9a-124">다음 그림에서는 `AspNetUsers` 스키마:</span><span class="sxs-lookup"><span data-stu-id="15d9a-124">The following image shows the `AspNetUsers` schema:</span></span>

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="15d9a-125">마우스 오른쪽 단추로 클릭는 **AspNetUsers** 테이블을 선택한 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-125">Right click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="15d9a-126">이 시점에서 전자 메일 확인 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-126">At this point the email has not been confirmed.</span></span>
7. <span data-ttu-id="15d9a-127">행을 클릭 하 고 삭제를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-127">Click on the row and select delete.</span></span> <span data-ttu-id="15d9a-128">다음 단계에서이 전자 메일을 다시 추가 하 고 확인 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-128">You'll add this email again in the next step, and send a confirmation email.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="15d9a-129">전자 메일 확인</span><span class="sxs-lookup"><span data-stu-id="15d9a-129">Email confirmation</span></span>

<span data-ttu-id="15d9a-130">다른 사용자에 가장 하지 않는 것을 확인 하려면 새 사용자 등록의 전자 메일을 확인 하는 것이 좋습니다 (즉, 이러한 하지 않은 등록 된 다른 사용자의 전자 메일).</span><span class="sxs-lookup"><span data-stu-id="15d9a-130">It's a best practice to confirm the email of a new user registration to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="15d9a-131">방지 하기 위해 원할 토론 포럼을 설치한 경우를 가정해 볼 `"bob@example.com"` 등록에서 `"joe@contoso.com"`합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-131">Suppose you had a discussion forum, you would want to prevent `"bob@example.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="15d9a-132">전자 메일 확인 하지 않고 `"joe@contoso.com"` 원치 않는 전자 메일 앱에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-132">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="15d9a-133">실수로 Bob로 등록 된 경우를 가정해 볼 `"bib@example.com"` 를 발견 하지 않은 그 하는지 앱에 없는 올바른 전자 메일 때문에 암호 복구를 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-133">Suppose Bob accidently registered as `"bib@example.com"` and hadn't noticed it, he wouldn't be able to use password recover because the app doesn't have his correct email.</span></span> <span data-ttu-id="15d9a-134">전자 메일 확인 bot에서 제한 된 보호만을 제공 하 고 결정된 된 스팸에서 보호를 제공 하지 않습니다, 그리고 등록 하는 데 사용할 수는 많은 작업 전자 메일 별칭을가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-134">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers, they have many working email aliases they can use to register.</span></span>

<span data-ttu-id="15d9a-135">일반적으로 새 사용자 전자 메일, SMS 문자 메시지 또는 기타 메커니즘 확인 하기 전에 모든 데이터 웹 사이트를 게시 하는 것을 방지 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-135">You generally want to prevent new users from posting any data to your web site before they have been confirmed by email, a SMS text message or another mechanism.</span></span> <a id="build"></a><span data-ttu-id="15d9a-136">아래 섹션에 전자 메일 확인을 사용 하도록 설정 하 고 새로 등록 된 사용자가 전자 메일 확인 될 때까지에 로그인 하지 못하도록 방지 하기 위해 코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-136">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="15d9a-137">SendGrid 후크</span><span class="sxs-lookup"><span data-stu-id="15d9a-137">Hook up SendGrid</span></span>

<span data-ttu-id="15d9a-138">이 자습서에서는 통해 전자 메일 알림을 추가 하는 방법을 보여 줍니다. 하지만 [SendGrid](http://sendgrid.com/), SMTP 및 다른 메커니즘을 사용 하 여 메일을 보낼 수 있습니다 (참조 [추가 리소스](#addRes)).</span><span class="sxs-lookup"><span data-stu-id="15d9a-138">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="15d9a-139">패키지 관리자 콘솔에서 다음을 입력 다음 명령을:</span><span class="sxs-lookup"><span data-stu-id="15d9a-139">In the Package Manager Console, enter the following the following command:</span></span> 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. <span data-ttu-id="15d9a-140">이동 하는 [Azure SendGrid 등록 페이지](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) 무료로 SendGrid 계정을 등록 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-140">Go to the [Azure SendGrid sign up page](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) and register for free SendGrid account.</span></span> <span data-ttu-id="15d9a-141">SendGrid를 구성 하려면 다음과 유사한 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-141">Add code similar to the following to configure SendGrid:</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

<span data-ttu-id="15d9a-142">다음을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-142">You'll need to add the following includes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

<span data-ttu-id="15d9a-143">이 예제를 단순하게 유지 하기 위해 응용 프로그램 설정에 저장할 것은 *web.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="15d9a-143">To keep this sample simple, we'll store the app settings in the *web.config* file:</span></span>

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> <span data-ttu-id="15d9a-144">보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-144">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="15d9a-145">계정 및 자격 증명 appSetting에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-145">The account and credentials are stored in the appSetting.</span></span> <span data-ttu-id="15d9a-146">Azure에서 안전 하 게에 저장할 수 있습니다 이러한 값은  **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)**  Azure 포털에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-146">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="15d9a-147">참조 [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-147">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>


### <a name="enable-email-confirmation-in-the-account-controller"></a><span data-ttu-id="15d9a-148">계정 컨트롤러에서 전자 메일 확인을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="15d9a-148">Enable email confirmation in the Account controller</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

<span data-ttu-id="15d9a-149">확인 된 *Views\Account\ConfirmEmail.cshtml* 파일에 올바른 razor 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-149">Verify the *Views\Account\ConfirmEmail.cshtml* file has correct razor syntax.</span></span> <span data-ttu-id="15d9a-150">(의 @ 첫 번째 범위에서 문자 줄 누락 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-150">( The @ character in the first line might be missing.</span></span> <span data-ttu-id="15d9a-151">)</span><span class="sxs-lookup"><span data-stu-id="15d9a-151">)</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="15d9a-152">응용 프로그램을 실행 하 고 등록 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-152">Run the app and click the Register link.</span></span> <span data-ttu-id="15d9a-153">등록 양식을 전송 하면에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-153">Once you submit the registration form, you are logged in.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

<span data-ttu-id="15d9a-154">전자 메일 계정을 확인 하 고 사용자의 전자 메일을 확인 하려면 다음 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-154">Check your email account and click on the link to confirm your email.</span></span>

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="15d9a-155">로그인 하기 전에 전자 메일 확인 필요</span><span class="sxs-lookup"><span data-stu-id="15d9a-155">Require email confirmation before log in</span></span>

<span data-ttu-id="15d9a-156">사용자는 등록 양식에 나와 완료 되 고 나면 현재으로 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-156">Currently once a user completes the registration form, they are logged in.</span></span> <span data-ttu-id="15d9a-157">일반적으로 자신의 전자 메일 기록 하기 전에 확인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-157">You generally want to confirm their email before logging them in.</span></span> <span data-ttu-id="15d9a-158">아래 섹션에서는 새 사용자가 기록 하기 전에 확인 된 전자 메일을 가질 (인증) 코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-158">In the section below, we will modify the code to require new users to have a confirmed email before they are logged in (authenticated).</span></span> <span data-ttu-id="15d9a-159">업데이트는 `HttpPost Register` 다음 표시 된 변경 내용 사용 하 여 메서드:</span><span class="sxs-lookup"><span data-stu-id="15d9a-159">Update the `HttpPost Register` method with the following highlighted changes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

<span data-ttu-id="15d9a-160">주석으로 처리 하는 여는 `SignInAsync` 메서드를 사용자 등록 하 여 로그인 하지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-160">By commenting out the `SignInAsync` method, the user will not be signed in by the registration.</span></span> <span data-ttu-id="15d9a-161">`TempData["ViewBagLink"] = callbackUrl;` 줄에 사용할 수 있습니다 [응용 프로그램을 디버깅](#dbg) 및 전자 메일을 보내지 않고 등록을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-161">The `TempData["ViewBagLink"] = callbackUrl;` line can be used to [debug the app](#dbg) and test registration without sending email.</span></span> <span data-ttu-id="15d9a-162">`ViewBag.Message`확인 지침을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-162">`ViewBag.Message` is used to display the confirm instructions.</span></span> <span data-ttu-id="15d9a-163">[샘플 다운로드](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) 전자 메일을 설정 하지 않고 전자 메일 확인을 테스트 하는 코드가 포함 되어 있으며 응용 프로그램 디버깅을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-163">The [download sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) contains code to test email confirmation without setting up email, and can also be used to debug the application.</span></span>

<span data-ttu-id="15d9a-164">만들기는 `Views\Shared\Info.cshtml` 파일을 다음 razor 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-164">Create a `Views\Shared\Info.cshtml` file and add the following razor markup:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

<span data-ttu-id="15d9a-165">추가 [Authorize 특성](https://msdn.microsoft.com/en-us/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) 에 `Contact` Home 컨트롤러의 동작 메서드.</span><span class="sxs-lookup"><span data-stu-id="15d9a-165">Add the [Authorize attribute](https://msdn.microsoft.com/en-us/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) to the `Contact` action method of the Home controller.</span></span> <span data-ttu-id="15d9a-166">클릭을 사용할 수 있습니다는 **연락처** 익명 사용자가 액세스할 수 없는 및 인증 된 사용자가 액세스할 수 있는 권한이 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-166">You can use click on the **Contact** link to verify anonymous users don't have access and authenticated users do have access.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

<span data-ttu-id="15d9a-167">업데이트 해야는 `HttpPost Login` 동작 메서드:</span><span class="sxs-lookup"><span data-stu-id="15d9a-167">You must also update the `HttpPost Login` action method:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

<span data-ttu-id="15d9a-168">업데이트는 *Views\Shared\Error.cshtml* 오류 메시지를 표시 하려면 보기:</span><span class="sxs-lookup"><span data-stu-id="15d9a-168">Update the *Views\Shared\Error.cshtml* view to display the error message:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

<span data-ttu-id="15d9a-169">모든 계정을 삭제는 **AspNetUsers** 와 테스트 하려는 전자 메일 별칭을 포함 하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-169">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test with.</span></span> <span data-ttu-id="15d9a-170">응용 프로그램을 실행 하 고 로그인 할 수 없는 전자 메일 주소를 확인 한 될 때까지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-170">Run the app and verify you can't log in until you have confirmed your email address.</span></span> <span data-ttu-id="15d9a-171">전자 메일 주소를 확인 하 고 나면 클릭는 **연락처** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-171">Once you confirm your email address, click the **Contact** link.</span></span>

<a id="reset"></a>
## <a name="password-recoveryreset"></a><span data-ttu-id="15d9a-172">암호 복구/다시 설정</span><span class="sxs-lookup"><span data-stu-id="15d9a-172">Password recovery/reset</span></span>

<span data-ttu-id="15d9a-173">주석 문자를 제거는 `HttpPost ForgotPassword` 계정 컨트롤러에서 동작 메서드:</span><span class="sxs-lookup"><span data-stu-id="15d9a-173">Remove the comment characters from the `HttpPost ForgotPassword` action method in the account controller:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

<span data-ttu-id="15d9a-174">주석 문자를 제거는 `ForgotPassword` [ActionLink](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) 에 *Views\Account\Login.cshtml* razor 파일 보기:</span><span class="sxs-lookup"><span data-stu-id="15d9a-174">Remove the comment characters from the `ForgotPassword` [ActionLink](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) in the *Views\Account\Login.cshtml* razor view file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

<span data-ttu-id="15d9a-175">로그인 페이지에서 암호를 다시 설정에 대 한 링크를 표시 이제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-175">The Log in page will now show a link to reset the password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="15d9a-176">전자 메일 확인 링크를 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-176">Resend email confirmation link</span></span>

<span data-ttu-id="15d9a-177">사용자는 새 로컬 계정을 만들고 나면은 로그온 할 수 전에 사용 하는 데 필요 확인 링크를 전자 메일로 전송 되 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-177">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="15d9a-178">실수로 삭제 확인 전자 메일 또는 전자 메일이 도착 하지 확인 링크 다시 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-178">If the user accidently deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="15d9a-179">다음 코드 변경 내용에는이 기능을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-179">The following code changes show how to enable this.</span></span>

<span data-ttu-id="15d9a-180">맨 아래에 다음 도우미 메서드를 추가 합니다.는 *Controllers\AccountController.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="15d9a-180">Add the following helper method to the bottom of the *Controllers\AccountController.cs* file:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

<span data-ttu-id="15d9a-181">새 도우미를 사용 하도록 Register 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-181">Update the Register method to use the new helper:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

<span data-ttu-id="15d9a-182">암호를 다시 보내도록 로그인 메서드를 업데이트 하는 경우 사용자 계정을 확인 되지 경우:</span><span class="sxs-lookup"><span data-stu-id="15d9a-182">Update the Login method to resend the password when if the user account has not been confirmed:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="15d9a-183">공유 및 로컬 로그인 계정을 결합합니다</span><span class="sxs-lookup"><span data-stu-id="15d9a-183">Combine social and local login accounts</span></span>

<span data-ttu-id="15d9a-184">사용자 전자 메일 링크를 클릭 하 여 로컬 및 소셜 계정을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-184">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="15d9a-185">다음 순서로  **RickAndMSFT@gmail.com**  처음에 로컬 로그인으로 만들면 하지만 로컬 로그인을 추가 다음에서 첫 번째로, 소셜 로그로 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-185">In the following sequence **RickAndMSFT@gmail.com** is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

<span data-ttu-id="15d9a-186">클릭는 **관리** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-186">Click on the **Manage** link.</span></span> <span data-ttu-id="15d9a-187">이 계정에 연결 된 참고 0 외부 (소셜 로그인)</span><span class="sxs-lookup"><span data-stu-id="15d9a-187">Note the 0 external (social logins) associated with this account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

<span data-ttu-id="15d9a-188">서비스에서 다른 로그에 대 한 링크를 클릭 하 고 응용 프로그램 요청을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-188">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="15d9a-189">두 개의 계정을 결합 되어, 두 계정으로 로그온 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-189">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="15d9a-190">경우에 대비 다운 되는 인증 서비스에서 소셜의 로그 또는 쓰지만 대개은 स ॅ स 소셜 계정으로 로컬 계정을 추가 하려면 사용자가 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-190">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="15d9a-191">다음 그림에서는 Tom는 소셜 로그인 (에서 볼 수 있는 **외부 로그인: 1** 페이지에 표시).</span><span class="sxs-lookup"><span data-stu-id="15d9a-191">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

<span data-ttu-id="15d9a-192">클릭 하면 **암호** 동일한 계정에 연결 된 로컬 로그에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-192">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a><span data-ttu-id="15d9a-193">좀 더 깊이 전자 메일 확인</span><span class="sxs-lookup"><span data-stu-id="15d9a-193">Email confirmation in more depth</span></span>

<span data-ttu-id="15d9a-194">내 자습서 [계정 확인 및 ASP.NET Id와 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 자세한 정보와 함께이 항목으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-194">My tutorial [Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) goes into this topic with more details.</span></span>

<a id="dbg"></a>
## <a name="debugging-the-app"></a><span data-ttu-id="15d9a-195">응용 프로그램 디버깅</span><span class="sxs-lookup"><span data-stu-id="15d9a-195">Debugging the app</span></span>

<span data-ttu-id="15d9a-196">링크가 포함 된 전자 메일 얻지 못한 경우:</span><span class="sxs-lookup"><span data-stu-id="15d9a-196">If you don't get an email containing the link:</span></span>

- <span data-ttu-id="15d9a-197">정크 또는 스팸 폴더를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-197">Check your junk or spam folder.</span></span>
- <span data-ttu-id="15d9a-198">SendGrid 계정에 로그인 하 고 클릭는 [전자 메일 작업 링크](https://sendgrid.com/logs/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-198">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>

<span data-ttu-id="15d9a-199">전자 메일 하지 않고 확인 링크를 테스트 하려면 다운로드는 [완성 된 샘플](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-199">To test the verification link without email, download the [completed sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="15d9a-200">확인 링크 및 확인 코드 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-200">The confirmation link and confirmation codes will be displayed on the page.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="15d9a-201">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="15d9a-201">Additional Resources</span></span>

- [<span data-ttu-id="15d9a-202">ASP.NET Id에 대 한 링크 권장 리소스</span><span class="sxs-lookup"><span data-stu-id="15d9a-202">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="15d9a-203">[계정 확인 및 ASP.NET Id와 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 암호 복구 및 계정 확인에 대 한 자세한 내용으로 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-203">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="15d9a-204">[Facebook, Twitter, LinkedIn 및 Google OAuth2 로그온 된 MVC 5 앱](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 이 자습서에서는 Facebook 및 Google OAuth 2 인증을 사용 하 여 ASP.NET MVC 5 앱을 작성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-204">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="15d9a-205">또한 Id 데이터베이스에 데이터를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-205">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="15d9a-206">[멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET MVC 응용 프로그램을 Azure에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-206">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="15d9a-207">이 자습서에서는 Azure 배포 추가 역할을 사용 하 여 앱을 보호 하는 방법을 사용자 및 역할 및 추가 보안 기능을 추가할 구성원 API를 사용 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="15d9a-207">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="15d9a-208">OAuth 2에 대 한 Google 앱 만들기 및 앱 프로젝트 연결</span><span class="sxs-lookup"><span data-stu-id="15d9a-208">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="15d9a-209">Facebook에서 앱을 만들기 및 앱 프로젝트에 연결</span><span class="sxs-lookup"><span data-stu-id="15d9a-209">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="15d9a-210">프로젝트에서 SSL을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="15d9a-210">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
