---
uid: mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
title: SMS 및 전자 메일 2 단계 인증을 사용 하 여 ASP.NET MVC 5 앱 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 2 단계 인증을 사용 하 여 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다. 만들기는 보안 ASP.NET MVC 5 웹 앱을 완료 해야 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/20/2015
ms.topic: article
ms.assetid: f50a5cdb-c06a-46ed-aa14-fc5b049dc8dc
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: 7987953ae94105be8f4856069ce13b86aec7e7f9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37393959"
---
<a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a><span data-ttu-id="fc582-104">SMS 및 전자 메일 2 단계 인증을 사용 하 여 ASP.NET MVC 5 앱</span><span class="sxs-lookup"><span data-stu-id="fc582-104">ASP.NET MVC 5 app with SMS and email Two-Factor Authentication</span></span>
====================
<span data-ttu-id="fc582-105">[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="fc582-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="fc582-106">이 자습서에서는 2 단계 인증을 사용 하 여 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with Two-Factor Authentication.</span></span> <span data-ttu-id="fc582-107">완료 해야 [로그인, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET MVC 5 웹 앱을 만들기](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-107">You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="fc582-108">완성된 된 응용 프로그램을 다운로드할 수 있습니다 [여기](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-108">You can download the completed application [here](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="fc582-109">다운로드는 전자 메일 또는 SMS 공급자를 설정 하지 않고 SMS 및 전자 메일 확인을 테스트할 수 있도록 디버깅 도우미를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-109">The download contains debugging helpers that let you test email confirmation and SMS without setting up an email or SMS provider.</span></span>
> 
> <span data-ttu-id="fc582-110">이 자습서를 통해 작성 했습니다 [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="fc582-110">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>


- [<span data-ttu-id="fc582-111">ASP.NET MVC 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="fc582-111">Create an ASP.NET MVC app</span></span>](#createMvc)
- [<span data-ttu-id="fc582-112">SMS 2 단계 인증에 대 한 설정</span><span class="sxs-lookup"><span data-stu-id="fc582-112">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="fc582-113">2 단계 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="fc582-113">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="fc582-114">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="fc582-114">Additional Resources</span></span>](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="fc582-115">ASP.NET MVC 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="fc582-115">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="fc582-116">설치 및 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 하거나 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-116">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="fc582-117">설치할 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상.</span><span class="sxs-lookup"><span data-stu-id="fc582-117">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="fc582-118">경고: 완료 해야 [로그인, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET MVC 5 웹 앱을 만들기](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-118">Warning: You should complete [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) before proceeding.</span></span> <span data-ttu-id="fc582-119">설치 해야 합니다 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상이 자습서를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-119">You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>


1. <span data-ttu-id="fc582-120">새 ASP.NET 웹 프로젝트를 만들고 MVC 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-120">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="fc582-121">또한 web Forms web forms 앱에서 비슷한 단계를 수행할 수 있도록 ASP.NET Id를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-121">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. <span data-ttu-id="fc582-122">기본 인증을 유지 **개별 사용자 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-122">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="fc582-123">Azure에서 앱을 호스트 하려는 경우 확인란을 선택한 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-123">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="fc582-124">자습서의 뒷부분에 나오는 Azure에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-124">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="fc582-125">할 수 있습니다 [Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="fc582-126">설정 된 [SSL을 사용 하도록 프로젝트](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-126">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>

<a id="SMS"></a>
## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="fc582-127">SMS 2 단계 인증에 대 한 설정</span><span class="sxs-lookup"><span data-stu-id="fc582-127">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="fc582-128">이 자습서에서는 Twilio 또는 ASPSMS 중 하나를 사용 하 여에 대 한 지침을 제공 하지만 다른 SMS 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-128">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="fc582-129">**SMS 공급자를 사용 하 여 사용자 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="fc582-129">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="fc582-130">만들기는 [Twilio](https://www.twilio.com/try-twilio) 요소나 [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) 계정.</span><span class="sxs-lookup"><span data-stu-id="fc582-130">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="fc582-131">**추가 패키지를 설치 하거나 서비스 참조 추가**</span><span class="sxs-lookup"><span data-stu-id="fc582-131">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="fc582-132">Twilio:</span><span class="sxs-lookup"><span data-stu-id="fc582-132">Twilio:</span></span>  
   <span data-ttu-id="fc582-133">패키지 관리자 콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-133">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="fc582-134">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="fc582-134">ASPSMS:</span></span>  
   <span data-ttu-id="fc582-135">다음 서비스 참조를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-135">The following service reference needs to be added:</span></span>  
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   <span data-ttu-id="fc582-136">주소:</span><span class="sxs-lookup"><span data-stu-id="fc582-136">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="fc582-137">네임스페이스:</span><span class="sxs-lookup"><span data-stu-id="fc582-137">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="fc582-138">**SMS 공급자 사용자 자격 증명 확인**</span><span class="sxs-lookup"><span data-stu-id="fc582-138">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="fc582-139">Twilio:</span><span class="sxs-lookup"><span data-stu-id="fc582-139">Twilio:</span></span>  
   <span data-ttu-id="fc582-140">**대시보드** 탭의 Twilio 계정에 복사 합니다 **계정 SID** 및 **인증 토큰**합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-140">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="fc582-141">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="fc582-141">ASPSMS:</span></span>  
   <span data-ttu-id="fc582-142">계정 설정을에서 이동 **Userkey** 에 자체 정의 된 함께 복사해 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-142">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="fc582-143">저장 하겠습니다. 나중에 이러한 값을 *web.config* 키 파일 `"SMSAccountIdentification"` 고 `"SMSAccountPassword"` 입니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-143">We will later store these values in the *web.config* file within the keys `"SMSAccountIdentification"` and `"SMSAccountPassword"` .</span></span>
4. <span data-ttu-id="fc582-144">**SenderID 지정 / 송신자**</span><span class="sxs-lookup"><span data-stu-id="fc582-144">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="fc582-145">Twilio:</span><span class="sxs-lookup"><span data-stu-id="fc582-145">Twilio:</span></span>  
   <span data-ttu-id="fc582-146">**숫자** 탭, Twilio 전화 번호를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-146">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="fc582-147">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="fc582-147">ASPSMS:</span></span>  
   <span data-ttu-id="fc582-148">내 합니다 **보낸 사람 잠금 해제** 메뉴에서 하나 이상의 보낸 사람을 잠금 해제 또는 영숫자 송신자 (모든 네트워크에서 지원 되지 않음)를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-148">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="fc582-149">저장 하겠습니다. 나중에이 값은 *web.config* 내 키 파일 `"SMSAccountFrom"` 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-149">We will later store this value in the *web.config* file within the key `"SMSAccountFrom"` .</span></span>
5. <span data-ttu-id="fc582-150">**앱에 SMS 공급자 자격 증명 전송**</span><span class="sxs-lookup"><span data-stu-id="fc582-150">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="fc582-151">자격 증명 및 보낸 사람에 게 전화 번호를 앱에 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-151">Make the credentials and sender phone number available to the app.</span></span> <span data-ttu-id="fc582-152">간단 하 게 저장 하겠습니다. 이러한 값을 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-152">To keep things simple we will store these values in the *web.config* file.</span></span> <span data-ttu-id="fc582-153">Azure에 배포 했습니다 하는 경우에 안전 하 게 값을 저장할 수는 **앱 설정** 웹 사이트에서 섹션 구성 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-153">When we deploy to Azure, we can store the values securely in the **app settings** section on the web site configure tab.</span></span> 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > <span data-ttu-id="fc582-154">보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-154">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="fc582-155">계정 및 자격 증명을 단순하게 유지 하기 위해 샘플 위의 코드에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-155">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="fc582-156">참조 [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-156">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
6. <span data-ttu-id="fc582-157">**SMS 공급자 간 데이터 전송의 구현**</span><span class="sxs-lookup"><span data-stu-id="fc582-157">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="fc582-158">구성 된 `SmsService` 클래스를 *앱\_Start\IdentityConfig.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-158">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="fc582-159">사용 되는 SMS 공급자에 따라 하나를 활성화 합니다 **Twilio** 또는 **ASPSMS** 섹션:</span><span class="sxs-lookup"><span data-stu-id="fc582-159">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. <span data-ttu-id="fc582-160">업데이트를 *Views\Manage\Index.cshtml* Razor 뷰: (참고:만 기존 코드의 주석을 제거, 아래 코드를 사용 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="fc582-160">Update the *Views\Manage\Index.cshtml* Razor view: (note: don't just remove the comments in the exiting code, use the code below.)</span></span>  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. <span data-ttu-id="fc582-161">확인 합니다 `EnableTwoFactorAuthentication` 및 `DisableTwoFactorAuthentication` 의 작업 메서드는 `ManageController` 가[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) 특성:</span><span class="sxs-lookup"><span data-stu-id="fc582-161">Verify the `EnableTwoFactorAuthentication` and `DisableTwoFactorAuthentication` action methods in the `ManageController` have the[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) attribute:</span></span>  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. <span data-ttu-id="fc582-162">앱을 실행 하 고 이전에 등록 한 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-162">Run the app and log in with the account you previously registered.</span></span>
10. <span data-ttu-id="fc582-163">활성화 하는 사용자 ID를 클릭 합니다 `Index` 의 동작 메서드에 `Manage` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-163">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. <span data-ttu-id="fc582-164">추가 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-164">Click Add.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. <span data-ttu-id="fc582-165">`AddPhoneNumber` 작업 메서드는 SMS 메시지를 받을 수 있는 전화 번호를 입력 하는 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-165">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. <span data-ttu-id="fc582-166">몇 초 안에 확인 코드로 문자 메시지를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="fc582-167">Enter 키를 눌러 **제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-167">Enter it and press **Submit**.</span></span>  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. <span data-ttu-id="fc582-168">관리 보기를 보여 줍니다 전화 번호 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-168">The Manage view shows your phone number was added.</span></span>

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a><span data-ttu-id="fc582-169">2 단계 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="fc582-169">Enable two-factor authentication</span></span>

<span data-ttu-id="fc582-170">생성 된 템플릿 앱에서 UI를 사용 하 여 2 단계 인증 (2FA)를 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-170">In the template generated app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="fc582-171">2FA를 사용 하도록 설정 하려면 탐색 모음에서 사용자 ID (전자 메일 별칭)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-171">To enable 2FA, click on your user ID (email alias) in the navigation bar.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

<span data-ttu-id="fc582-172">Enable 2FA를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-172">Click on enable 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

<span data-ttu-id="fc582-173">로그 아웃 한 다음 다시 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-173">Logout, then log back in.</span></span> <span data-ttu-id="fc582-174">전자 메일을 사용 하도록 설정한 경우 (참조 내 [이전 자습서](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), SMS 또는 2FA 위한 전자 메일을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-174">If you've enabled email (see my [previous tutorial](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

<span data-ttu-id="fc582-175">확인 코드 페이지 (SMS 또는 전자 메일)에서 코드를 입력할 수 있는 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-175">The Verify Code page is displayed where you can enter the code (from SMS or email).</span></span>

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

<span data-ttu-id="fc582-176">클릭 하 여 **이 브라우저 기억** 확인란 있습니다 2FA를 사용 하 여 브라우저 및 장치 상자를 선택한 경우 로그에 기록 하는 데 필요한에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-176">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log in when using the browser and device where you checked the box.</span></span> <span data-ttu-id="fc582-177">악의적인 사용자가 장치에 액세스할 수 없습니다, 2FA를 사용 하도록 설정 하 고 클릭 하 여 **이 브라우저 기억** 하면 편리 하 게 한 번 암호 액세스가 있는 모든 액세스에 대 한 강력한 2FA 보호를 유지 하면서 트러스트 되지 않은 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-177">As long as malicious users can't gain access to your device, enabling 2FA and clicking on the **Remember this browser** will provide you with convenient one step password access, while still retaining strong 2FA protection for all access from non-trusted devices.</span></span> <span data-ttu-id="fc582-178">정기적으로 사용 하는 모든 개인 장치에서이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-178">You can do this on any private device you regularly use.</span></span>

<span data-ttu-id="fc582-179">이 자습서에서는 새 ASP.NET MVC 앱에서 2FA를 사용 하도록 설정 하는 빠른 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-179">This tutorial provides a quick introduction to enabling 2FA on a new ASP.NET MVC app.</span></span> <span data-ttu-id="fc582-180">내 자습서 [ASP.NET Id와 SMS 및 전자 메일을 사용 하 여 2 단계 인증](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) 샘플 코드에 대해 자세히입니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-180">My tutorial [Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) goes into detail on the code behind the sample.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="fc582-181">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="fc582-181">Additional Resources</span></span>

- <span data-ttu-id="fc582-182">[ASP.NET Id와 SMS 및 전자 메일을 사용 하 여 2 단계 인증](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) 2 단계 인증에서 세부 정보로 이동</span><span class="sxs-lookup"><span data-stu-id="fc582-182">[Two-factor authentication using SMS and email with ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) Goes into detail on Two-factor authentication</span></span>
- [<span data-ttu-id="fc582-183">링크를 ASP.NET Id 권장 리소스</span><span class="sxs-lookup"><span data-stu-id="fc582-183">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="fc582-184">[계정 확인 및 ASP.NET Id와 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 암호 복구 및 계정 확인에 대 한 자세한 내용으로 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-184">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="fc582-185">[Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on을 사용 하 여 MVC 5 앱](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 이 자습서에서는 Facebook 및 Google OAuth 2 권한 부여를 사용 하 여 ASP.NET MVC 5 앱을 작성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-185">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="fc582-186">또한 Id 데이터베이스에 데이터를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-186">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="fc582-187">[멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET MVC 앱을 Azure 웹 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-187">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="fc582-188">이 자습서는 Azure 배포 추가 역할을 사용 하 여 앱을 보호 하는 방법을 멤버 자격 API를 사용 하 여 사용자 및 역할 및 추가 보안 기능을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fc582-188">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="fc582-189">OAuth 2 용 Google 앱 만들기 및 앱 프로젝트에 연결</span><span class="sxs-lookup"><span data-stu-id="fc582-189">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="fc582-190">Facebook에서 앱을 만들고 앱 프로젝트에 연결</span><span class="sxs-lookup"><span data-stu-id="fc582-190">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="fc582-191">프로젝트의 SSL 설정</span><span class="sxs-lookup"><span data-stu-id="fc582-191">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
