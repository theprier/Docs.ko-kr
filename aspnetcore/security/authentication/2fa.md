---
title: ASP.NET Core에서 SMS로 2 단계 인증
author: rick-anderson
description: ASP.NET Core 응용 프로그램과 (2FA) 2 단계 인증을 설정 하는 방법을 알아봅니다.
manager: wpickett
monikerRange: < aspnetcore-2.0
ms.author: riande
ms.date: 08/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/2fa
ms.openlocfilehash: 20f00c2307e140d81e716304c96a143340d934d0
ms.sourcegitcommit: 477d38e33530a305405eaf19faa29c6d805273aa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/08/2018
---
# <a name="two-factor-authentication-with-sms-in-aspnet-core"></a><span data-ttu-id="19aff-103">ASP.NET Core에서 SMS로 2 단계 인증</span><span class="sxs-lookup"><span data-stu-id="19aff-103">Two-factor authentication with SMS in ASP.NET Core</span></span>

<span data-ttu-id="19aff-104">여 [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [스위스 빌드하도록](https://github.com/Swiss-Devs)</span><span class="sxs-lookup"><span data-stu-id="19aff-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Swiss-Devs](https://github.com/Swiss-Devs)</span></span>

<span data-ttu-id="19aff-105">참조 [ASP.NET Core에서 인증자 앱에 대 한 QR 코드를 사용 하도록 설정 생성](xref:security/authentication/identity-enable-qrcodes) 이상 ASP.NET 코어 2.0에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-105">See [Enable QR Code generation for authenticator apps in ASP.NET Core](xref:security/authentication/identity-enable-qrcodes) for ASP.NET Core 2.0 and later.</span></span>

<span data-ttu-id="19aff-106">이 자습서에는 SMS를 사용 하 여 2 단계 인증 (2FA)을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-106">This tutorial shows how to set up two-factor authentication (2FA) using SMS.</span></span> <span data-ttu-id="19aff-107">에 대 한 지침이 제공 됩니다 [twilio](https://www.twilio.com/) 및 [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/), 하지만 다른 SMS 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-107">Instructions are given for [twilio](https://www.twilio.com/) and [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/), but you can use any other SMS provider.</span></span> <span data-ttu-id="19aff-108">완료 하는 것이 좋습니다 [계정 확인 및 암호 복구](xref:security/authentication/accconfirm) 이 자습서를 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="19aff-108">We recommend you complete [Account Confirmation and Password Recovery](xref:security/authentication/accconfirm) before starting this tutorial.</span></span>

<span data-ttu-id="19aff-109">보기는 [완성 된 샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/2fa/sample/Web2FA)합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-109">View the [completed sample](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/2fa/sample/Web2FA).</span></span> <span data-ttu-id="19aff-110">[다운로드 하는 방법](xref:tutorials/index#how-to-download-a-sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-110">[How to download](xref:tutorials/index#how-to-download-a-sample).</span></span>

## <a name="create-a-new-aspnet-core-project"></a><span data-ttu-id="19aff-111">새 ASP.NET Core 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="19aff-111">Create a new ASP.NET Core project</span></span>

<span data-ttu-id="19aff-112">라는 새 ASP.NET Core 웹 앱 만들기 `Web2FA` 개별 사용자 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-112">Create a new ASP.NET Core web app named `Web2FA` with individual user accounts.</span></span> <span data-ttu-id="19aff-113">지침에 따라 [ASP.NET Core 응용 프로그램에서 SSL 적용](xref:security/enforcing-ssl) 를 설정 하 고 SSL이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-113">Follow the instructions in [Enforce SSL in an ASP.NET Core app](xref:security/enforcing-ssl) to set up and require SSL.</span></span>

### <a name="create-an-sms-account"></a><span data-ttu-id="19aff-114">SMS 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="19aff-114">Create an SMS account</span></span>

<span data-ttu-id="19aff-115">예를 들어, SMS 계정을에서 만들고 [twilio](https://www.twilio.com/) 또는 [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/)합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-115">Create an SMS account, for example, from [twilio](https://www.twilio.com/) or [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/).</span></span> <span data-ttu-id="19aff-116">인증 자격 증명 기록 (twilio 용: accountSid 및 ASPSMS에 대 한 authToken: 사용자 키로 및 암호).</span><span class="sxs-lookup"><span data-stu-id="19aff-116">Record the authentication credentials (for twilio: accountSid and authToken, for ASPSMS: Userkey and Password).</span></span>

#### <a name="figuring-out-sms-provider-credentials"></a><span data-ttu-id="19aff-117">SMS 공급자 자격 증명을 파악</span><span class="sxs-lookup"><span data-stu-id="19aff-117">Figuring out SMS Provider credentials</span></span>

<span data-ttu-id="19aff-118">**Twilio:**</span><span class="sxs-lookup"><span data-stu-id="19aff-118">**Twilio:**</span></span>  
<span data-ttu-id="19aff-119">Twilio 계정 대시보드 탭에서 복사 된 **계정 SID** 및 **인증 토큰**합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-119">From the Dashboard tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>

<span data-ttu-id="19aff-120">**ASPSMS:**</span><span class="sxs-lookup"><span data-stu-id="19aff-120">**ASPSMS:**</span></span>  
<span data-ttu-id="19aff-121">계정 설정을에서으로 이동 **사용자 키로** 와 함께 복사 및 프로그램 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-121">From your account settings, navigate to **Userkey** and copy it together with your **Password**.</span></span>

<span data-ttu-id="19aff-122">이러한 값을 키에 암호 관리자 도구를 사용 하 여 나중에 저장할 `SMSAccountIdentification` 및 `SMSAccountPassword`합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-122">We will later store these values in with the secret-manager tool within the keys `SMSAccountIdentification` and `SMSAccountPassword`.</span></span>

#### <a name="specifying-senderid--originator"></a><span data-ttu-id="19aff-123">SenderID 지정 / 송신자</span><span class="sxs-lookup"><span data-stu-id="19aff-123">Specifying SenderID / Originator</span></span>

<span data-ttu-id="19aff-124">**Twilio:**</span><span class="sxs-lookup"><span data-stu-id="19aff-124">**Twilio:**</span></span>  
<span data-ttu-id="19aff-125">숫자 탭에서 프로그램 Twilio 복사 **전화 번호**합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-125">From the Numbers tab, copy your Twilio **phone number**.</span></span> 

<span data-ttu-id="19aff-126">**ASPSMS:**</span><span class="sxs-lookup"><span data-stu-id="19aff-126">**ASPSMS:**</span></span>  
<span data-ttu-id="19aff-127">보낸 사람 잠금 해제 메뉴 내에서 하나 이상의 보낸 사람을 잠금 해제 하거나 (모든 네트워크에서 지원 되지 않음)는 영숫자 송신자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-127">Within the Unlock Originators Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span> 

<span data-ttu-id="19aff-128">나중에이 값의 키 아래에 보안 관리자 도구로 저장할 `SMSAccountFrom`합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-128">We will later store this value with the secret-manager tool within the key `SMSAccountFrom`.</span></span>


### <a name="provide-credentials-for-the-sms-service"></a><span data-ttu-id="19aff-129">SMS 서비스에 대 한 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-129">Provide credentials for the SMS service</span></span>

<span data-ttu-id="19aff-130">에서는 [옵션 패턴](xref:fundamentals/configuration/options) 사용자 계정 및 키 설정에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-130">We'll use the [Options pattern](xref:fundamentals/configuration/options) to access the user account and key settings.</span></span> 

   * <span data-ttu-id="19aff-131">보안 SMS 키를 인출 하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-131">Create a class to fetch the secure SMS key.</span></span> <span data-ttu-id="19aff-132">이 샘플은 `SMSoptions` 클래스에 만들어집니다는 *Services/SMSoptions.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-132">For this sample, the `SMSoptions` class is created in the *Services/SMSoptions.cs* file.</span></span>

[!code-csharp[](2fa/sample/Web2FA/Services/SMSoptions.cs)]

<span data-ttu-id="19aff-133">설정의 `SMSAccountIdentification`, `SMSAccountPassword` 및 `SMSAccountFrom` 와 [암호 관리자 도구](xref:security/app-secrets)합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-133">Set the `SMSAccountIdentification`, `SMSAccountPassword` and `SMSAccountFrom` with the [secret-manager tool](xref:security/app-secrets).</span></span> <span data-ttu-id="19aff-134">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="19aff-134">For example:</span></span>

```none
C:/Web2FA/src/WebApp1>dotnet user-secrets set SMSAccountIdentification 12345
info: Successfully saved SMSAccountIdentification = 12345 to the secret store.
```
* <span data-ttu-id="19aff-135">SMS 공급자에 대 한 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-135">Add the NuGet package for the SMS provider.</span></span> <span data-ttu-id="19aff-136">패키지 관리자 콘솔 (PMC) 실행:</span><span class="sxs-lookup"><span data-stu-id="19aff-136">From the Package Manager Console (PMC) run:</span></span>

<span data-ttu-id="19aff-137">**Twilio:**</span><span class="sxs-lookup"><span data-stu-id="19aff-137">**Twilio:**</span></span>  
`Install-Package Twilio`

<span data-ttu-id="19aff-138">**ASPSMS:**</span><span class="sxs-lookup"><span data-stu-id="19aff-138">**ASPSMS:**</span></span>  
`Install-Package ASPSMS`


* <span data-ttu-id="19aff-139">코드를 추가 *Services/MessageServices.cs* SMS를 사용 하도록 설정할 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-139">Add code in the *Services/MessageServices.cs* file to enable SMS.</span></span> <span data-ttu-id="19aff-140">Twilio 또는 ASPSMS 섹션 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-140">Use either the Twilio or the ASPSMS section:</span></span>


<span data-ttu-id="19aff-141">**Twilio:**</span><span class="sxs-lookup"><span data-stu-id="19aff-141">**Twilio:**</span></span>  
[!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_twilio.cs)]

<span data-ttu-id="19aff-142">**ASPSMS:**</span><span class="sxs-lookup"><span data-stu-id="19aff-142">**ASPSMS:**</span></span>  
[!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_ASPSMS.cs)]

### <a name="configure-startup-to-use-smsoptions"></a><span data-ttu-id="19aff-143">사용 하는 시작 구성 `SMSoptions`</span><span class="sxs-lookup"><span data-stu-id="19aff-143">Configure startup to use `SMSoptions`</span></span>

<span data-ttu-id="19aff-144">추가 `SMSoptions` 서비스 컨테이너에 `ConfigureServices` 에서 메서드는 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="19aff-144">Add `SMSoptions` to the service container in the `ConfigureServices` method in the *Startup.cs*:</span></span>

[!code-csharp[](2fa/sample/Web2FA/Startup.cs?name=snippet1&highlight=4)]

### <a name="enable-two-factor-authentication"></a><span data-ttu-id="19aff-145">2 단계 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="19aff-145">Enable two-factor authentication</span></span>

<span data-ttu-id="19aff-146">열기는 *Views/Manage/Index.cshtml* Razor 파일 보기 및 주석 문자 (태그 없음 주석으로 처리 하므로) 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-146">Open the *Views/Manage/Index.cshtml* Razor view file and remove the comment characters (so no markup is commnted out).</span></span>

## <a name="log-in-with-two-factor-authentication"></a><span data-ttu-id="19aff-147">2 단계 인증으로 로그인</span><span class="sxs-lookup"><span data-stu-id="19aff-147">Log in with two-factor authentication</span></span>

* <span data-ttu-id="19aff-148">응용 프로그램을 실행 하 고 새 사용자 등록</span><span class="sxs-lookup"><span data-stu-id="19aff-148">Run the app and register a new user</span></span>

![Microsoft Edge에서 열려 있는 웹 응용 프로그램 등록 보기](2fa/_static/login2fa1.png)

* <span data-ttu-id="19aff-150">탭을 활성화 하는 사용자 이름에는 `Index` 관리 컨트롤러의 동작 메서드에 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-150">Tap on your user name, which activates the `Index` action method in Manage controller.</span></span> <span data-ttu-id="19aff-151">전화 번호를 탭 합니다 **추가** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-151">Then tap the phone number **Add** link.</span></span>

![보기를 관리](2fa/_static/login2fa2.png)

* <span data-ttu-id="19aff-153">확인 코드를 수신 하 고 누릅니다 하 전화 번호 추가 **확인 코드를 보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-153">Add a phone number that will receive the verification code, and tap **Send verification code**.</span></span>

![전화 번호 페이지 추가](2fa/_static/login2fa3.png)

* <span data-ttu-id="19aff-155">확인 코드가 있는 문자 메시지를 받아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-155">You will get a text message with the verification code.</span></span> <span data-ttu-id="19aff-156">입력 하 고 탭 **제출**</span><span class="sxs-lookup"><span data-stu-id="19aff-156">Enter it and tap **Submit**</span></span>

![전화 번호 페이지 확인](2fa/_static/login2fa4.png)

<span data-ttu-id="19aff-158">문자 메시지를 얻지 못하면 twilio 로그 페이지를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="19aff-158">If you don't get a text message, see twilio log page.</span></span>

* <span data-ttu-id="19aff-159">관리 보기는 성공적으로 추가 전화 번호를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-159">The Manage view shows your phone number was added successfully.</span></span>

![보기를 관리](2fa/_static/login2fa5.png)

* <span data-ttu-id="19aff-161">탭 **사용** 2 단계 인증을 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-161">Tap **Enable** to enable two-factor authentication.</span></span>

![보기를 관리](2fa/_static/login2fa6.png)

### <a name="test-two-factor-authentication"></a><span data-ttu-id="19aff-163">2 단계 인증 테스트</span><span class="sxs-lookup"><span data-stu-id="19aff-163">Test two-factor authentication</span></span>

* <span data-ttu-id="19aff-164">로그 오프 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-164">Log off.</span></span>

* <span data-ttu-id="19aff-165">로그인</span><span class="sxs-lookup"><span data-stu-id="19aff-165">Log in.</span></span>

* <span data-ttu-id="19aff-166">2 단계 인증을 제공 해야 하므로 사용자 계정 2 단계 인증이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-166">The user account has enabled two-factor authentication, so you have to provide the second factor of authentication .</span></span> <span data-ttu-id="19aff-167">이 자습서에서는 전화 확인 사용 하도록 설정한 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-167">In this tutorial you have enabled phone verification.</span></span> <span data-ttu-id="19aff-168">템플릿이 제공된은 두 번째 요소로 전자 메일을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-168">The built in templates also allow you to set up email as the second factor.</span></span> <span data-ttu-id="19aff-169">QR 코드와 같은 인증에 대 한 추가 두 번째 요소를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-169">You can set up additional second factors for authentication such as QR codes.</span></span> <span data-ttu-id="19aff-170">탭 **제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-170">Tap **Submit**.</span></span>

![확인 코드 보기 보내기](2fa/_static/login2fa7.png)

* <span data-ttu-id="19aff-172">SMS 메시지에 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-172">Enter the code you get in the SMS message.</span></span>

* <span data-ttu-id="19aff-173">클릭 하 고 **저장이 브라우저** 확인란 있습니다 2FA를 사용 하 여 동일한 장치 및 브라우저를 사용 하는 경우 로그온 하에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-173">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log on when using the same device and browser.</span></span> <span data-ttu-id="19aff-174">2FA를 사용 하도록 설정 하 고 클릭 하 **저장이 브라우저** 알려 강력한 2FA 보호 장치에 액세스할 수 없는 상태로 회원님의 계정에 액세스 하려고 하는 악의적인 사용자 로부터 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-174">Enabling 2FA and clicking on **Remember this browser** will provide you with strong 2FA protection from malicious users trying to access your account, as long as they don't have access to your device.</span></span> <span data-ttu-id="19aff-175">정기적으로 사용 하는 모든 개인 장치에서이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-175">You can do this on any private device you regularly use.</span></span> <span data-ttu-id="19aff-176">설정 하 여 **저장이 브라우저**, 정기적으로 사용 하지 않는 장치에서 2FA의 강화 된 보안을 얻게 및에 자신의 장치에 2FA를 통과 하지 않아도 되는 편의성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-176">By setting  **Remember this browser**, you get the added security of 2FA from devices you don't regularly use, and you get the convenience on not having to go through 2FA on your own devices.</span></span>

![보기를 확인 합니다.](2fa/_static/login2fa8.png)

## <a name="account-lockout-for-protecting-against-brute-force-attacks"></a><span data-ttu-id="19aff-178">무차별 암호 대입 공격 으로부터 보호 하기 위한 계정 잠금</span><span class="sxs-lookup"><span data-stu-id="19aff-178">Account lockout for protecting against brute force attacks</span></span>

<span data-ttu-id="19aff-179">계정 잠금은 2FA 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-179">Account lockout is recommended with 2FA.</span></span> <span data-ttu-id="19aff-180">사용자가 로컬 계정 또는 소셜 계정을 통해 로그인 2FA에서 연결 시도가 실패할된 때마다 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-180">Once a user signs in through a local account or social account, each failed attempt at 2FA is stored.</span></span> <span data-ttu-id="19aff-181">사용자를 잠그기 실패 한 최대 액세스 시도 횟수에 도달 하면 (기본값: 5에 대 한 액세스 시도가 실패 한 잠금 5 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-181">If the maximum failed access attempts is reached, the user is locked out (default: 5 minute lockout after 5 failed access attempts).</span></span> <span data-ttu-id="19aff-182">실패 한 액세스 시도 횟수를 다시 설정 하 고 클록을 기본값으로 다시 설정 하는 성공적으로 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-182">A successful authentication resets the failed access attempts count and resets the clock.</span></span> <span data-ttu-id="19aff-183">최대 액세스 시도 하지 못했습니다. 잠금 시간으로 설정할 수 있습니다 및 [MaxFailedAccessAttempts](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts) 및 [DefaultLockoutTimeSpan](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan)합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-183">The maximum failed access attempts and lockout time can be set with [MaxFailedAccessAttempts](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts) and [DefaultLockoutTimeSpan](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan).</span></span> <span data-ttu-id="19aff-184">다음 계정 잠금 10 액세스 시도 실패 한 후 10 분 동안으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="19aff-184">The following configures account lockout for 10 minutes after 10 failed access attempts:</span></span>

[!code-csharp[](2fa/sample/Web2FA/Startup.cs?name=snippet2&highlight=13-17)]

<span data-ttu-id="19aff-185">확인 [PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync) 설정 `lockoutOnFailure` 를 `true`:</span><span class="sxs-lookup"><span data-stu-id="19aff-185">Confirm that [PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync) sets `lockoutOnFailure` to `true`:</span></span>

```csharp
var result = await _signInManager.PasswordSignInAsync(
                 Input.Email, Input.Password, Input.RememberMe, lockoutOnFailure: true);
```
