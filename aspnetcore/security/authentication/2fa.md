---
title: ASP.NET Core에서 SMS로 2 단계 인증
author: rick-anderson
description: ASP.NET Core 응용 프로그램과 (2FA) 2 단계 인증을 설정 하는 방법을 알아봅니다.
monikerRange: < aspnetcore-2.0
ms.author: riande
ms.date: 08/15/2017
uid: security/authentication/2fa
ms.openlocfilehash: 0308b05ebcda1af7f6850549d7a33f1df1a912a0
ms.sourcegitcommit: 1faf2525902236428dae6a59e375519bafd5d6d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37089986"
---
# <a name="two-factor-authentication-with-sms-in-aspnet-core"></a><span data-ttu-id="ec42b-103">ASP.NET Core에서 SMS로 2 단계 인증</span><span class="sxs-lookup"><span data-stu-id="ec42b-103">Two-factor authentication with SMS in ASP.NET Core</span></span>

<span data-ttu-id="ec42b-104">여 [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [스위스 빌드하도록](https://github.com/Swiss-Devs)</span><span class="sxs-lookup"><span data-stu-id="ec42b-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Swiss-Devs](https://github.com/Swiss-Devs)</span></span>

 <span data-ttu-id="ec42b-105">시간 기반 일회용 암호 알고리즘 (TOTP)를 사용 하 여 요소 인증 (2FA) 인증자 앱, 두 가지 권장 접근법 2FA에 대 한 업계 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-105">Two factor authentication (2FA) authenticator apps, using a Time-based One-time Password Algorithm (TOTP), are the industry recommended approach for 2FA.</span></span> <span data-ttu-id="ec42b-106">2FA TOTP를 사용 하 여는 SMS 2FA 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-106">2FA using TOTP is preferred to SMS 2FA.</span></span> <span data-ttu-id="ec42b-107">자세한 내용은 참조 [에서 ASP.NET Core TOTP authenticator 앱에 대 한 QR 코드를 사용 하도록 설정 생성](xref:security/authentication/identity-enable-qrcodes) 이상 ASP.NET 코어 2.0에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-107">For more information, see [Enable QR Code generation for TOTP authenticator apps in ASP.NET Core](xref:security/authentication/identity-enable-qrcodes) for ASP.NET Core 2.0 and later.</span></span>

<span data-ttu-id="ec42b-108">이 자습서에는 SMS를 사용 하 여 2 단계 인증 (2FA)을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-108">This tutorial shows how to set up two-factor authentication (2FA) using SMS.</span></span> <span data-ttu-id="ec42b-109">에 대 한 지침이 제공 됩니다 [twilio](https://www.twilio.com/) 및 [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/), 하지만 다른 SMS 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-109">Instructions are given for [twilio](https://www.twilio.com/) and [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/), but you can use any other SMS provider.</span></span> <span data-ttu-id="ec42b-110">완료 하는 것이 좋습니다 [계정 확인 및 암호 복구](xref:security/authentication/accconfirm) 이 자습서를 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="ec42b-110">We recommend you complete [Account Confirmation and Password Recovery](xref:security/authentication/accconfirm) before starting this tutorial.</span></span>

<span data-ttu-id="ec42b-111">보기는 [완성 된 샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/2fa/sample/Web2FA)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-111">View the [completed sample](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/2fa/sample/Web2FA).</span></span> <span data-ttu-id="ec42b-112">[다운로드 하는 방법](xref:tutorials/index#how-to-download-a-sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-112">[How to download](xref:tutorials/index#how-to-download-a-sample).</span></span>

## <a name="create-a-new-aspnet-core-project"></a><span data-ttu-id="ec42b-113">새 ASP.NET Core 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="ec42b-113">Create a new ASP.NET Core project</span></span>

<span data-ttu-id="ec42b-114">라는 새 ASP.NET Core 웹 앱 만들기 `Web2FA` 개별 사용자 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-114">Create a new ASP.NET Core web app named `Web2FA` with individual user accounts.</span></span> <span data-ttu-id="ec42b-115">지침에 따라 [ASP.NET Core 응용 프로그램에서 SSL 적용](xref:security/enforcing-ssl) 를 설정 하 고 SSL이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-115">Follow the instructions in [Enforce SSL in an ASP.NET Core app](xref:security/enforcing-ssl) to set up and require SSL.</span></span>

### <a name="create-an-sms-account"></a><span data-ttu-id="ec42b-116">SMS 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="ec42b-116">Create an SMS account</span></span>

<span data-ttu-id="ec42b-117">예를 들어, SMS 계정을에서 만들고 [twilio](https://www.twilio.com/) 또는 [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-117">Create an SMS account, for example, from [twilio](https://www.twilio.com/) or [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/).</span></span> <span data-ttu-id="ec42b-118">인증 자격 증명 기록 (twilio 용: accountSid 및 ASPSMS에 대 한 authToken: 사용자 키로 및 암호).</span><span class="sxs-lookup"><span data-stu-id="ec42b-118">Record the authentication credentials (for twilio: accountSid and authToken, for ASPSMS: Userkey and Password).</span></span>

#### <a name="figuring-out-sms-provider-credentials"></a><span data-ttu-id="ec42b-119">SMS 공급자 자격 증명을 파악</span><span class="sxs-lookup"><span data-stu-id="ec42b-119">Figuring out SMS Provider credentials</span></span>

<span data-ttu-id="ec42b-120">**Twilio:** Twilio 계정 대시보드 탭에서 복사 된 **계정 SID** 및 **인증 토큰**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-120">**Twilio:** From the Dashboard tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>

<span data-ttu-id="ec42b-121">**ASPSMS:** 계정 설정을에서으로 이동 **사용자 키로** 와 함께 복사 및 프로그램 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-121">**ASPSMS:** From your account settings, navigate to **Userkey** and copy it together with your **Password**.</span></span>

<span data-ttu-id="ec42b-122">이러한 값을 키에 암호 관리자 도구를 사용 하 여 나중에 저장할 `SMSAccountIdentification` 및 `SMSAccountPassword`합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-122">We will later store these values in with the secret-manager tool within the keys `SMSAccountIdentification` and `SMSAccountPassword`.</span></span>

#### <a name="specifying-senderid--originator"></a><span data-ttu-id="ec42b-123">SenderID 지정 / 송신자</span><span class="sxs-lookup"><span data-stu-id="ec42b-123">Specifying SenderID / Originator</span></span>

<span data-ttu-id="ec42b-124">**Twilio:** 숫자 탭에서 프로그램 Twilio 복사 **전화 번호**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-124">**Twilio:** From the Numbers tab, copy your Twilio **phone number**.</span></span>

<span data-ttu-id="ec42b-125">**ASPSMS:** 보낸 사람 잠금 해제 메뉴 내에서 하나 이상의 보낸 사람을 잠금 해제 하거나 (모든 네트워크에서 지원 되지 않음)는 영숫자 송신자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-125">**ASPSMS:** Within the Unlock Originators Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>

<span data-ttu-id="ec42b-126">나중에이 값의 키 아래에 보안 관리자 도구로 저장할 `SMSAccountFrom`합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-126">We will later store this value with the secret-manager tool within the key `SMSAccountFrom`.</span></span>


### <a name="provide-credentials-for-the-sms-service"></a><span data-ttu-id="ec42b-127">SMS 서비스에 대 한 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-127">Provide credentials for the SMS service</span></span>

<span data-ttu-id="ec42b-128">에서는 [옵션 패턴](xref:fundamentals/configuration/options) 사용자 계정 및 키 설정에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-128">We'll use the [Options pattern](xref:fundamentals/configuration/options) to access the user account and key settings.</span></span>

   * <span data-ttu-id="ec42b-129">보안 SMS 키를 인출 하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-129">Create a class to fetch the secure SMS key.</span></span> <span data-ttu-id="ec42b-130">이 샘플은 `SMSoptions` 클래스에 만들어집니다는 *Services/SMSoptions.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-130">For this sample, the `SMSoptions` class is created in the *Services/SMSoptions.cs* file.</span></span>

[!code-csharp[](2fa/sample/Web2FA/Services/SMSoptions.cs)]

<span data-ttu-id="ec42b-131">설정의 `SMSAccountIdentification`, `SMSAccountPassword` 및 `SMSAccountFrom` 와 [암호 관리자 도구](xref:security/app-secrets)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-131">Set the `SMSAccountIdentification`, `SMSAccountPassword` and `SMSAccountFrom` with the [secret-manager tool](xref:security/app-secrets).</span></span> <span data-ttu-id="ec42b-132">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="ec42b-132">For example:</span></span>

```none
C:/Web2FA/src/WebApp1>dotnet user-secrets set SMSAccountIdentification 12345
info: Successfully saved SMSAccountIdentification = 12345 to the secret store.
```
* <span data-ttu-id="ec42b-133">SMS 공급자에 대 한 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-133">Add the NuGet package for the SMS provider.</span></span> <span data-ttu-id="ec42b-134">패키지 관리자 콘솔 (PMC) 실행:</span><span class="sxs-lookup"><span data-stu-id="ec42b-134">From the Package Manager Console (PMC) run:</span></span>

<span data-ttu-id="ec42b-135">**Twilio:**
`Install-Package Twilio`</span><span class="sxs-lookup"><span data-stu-id="ec42b-135">**Twilio:**
`Install-Package Twilio`</span></span>

<span data-ttu-id="ec42b-136">**ASPSMS:**
`Install-Package ASPSMS`</span><span class="sxs-lookup"><span data-stu-id="ec42b-136">**ASPSMS:**
`Install-Package ASPSMS`</span></span>


* <span data-ttu-id="ec42b-137">코드를 추가 *Services/MessageServices.cs* SMS를 사용 하도록 설정할 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-137">Add code in the *Services/MessageServices.cs* file to enable SMS.</span></span> <span data-ttu-id="ec42b-138">Twilio 또는 ASPSMS 섹션 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-138">Use either the Twilio or the ASPSMS section:</span></span>


<span data-ttu-id="ec42b-139">**Twilio:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_twilio.cs)]</span><span class="sxs-lookup"><span data-stu-id="ec42b-139">**Twilio:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_twilio.cs)]</span></span>

<span data-ttu-id="ec42b-140">**ASPSMS:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_ASPSMS.cs)]</span><span class="sxs-lookup"><span data-stu-id="ec42b-140">**ASPSMS:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_ASPSMS.cs)]</span></span>

### <a name="configure-startup-to-use-smsoptions"></a><span data-ttu-id="ec42b-141">사용 하는 시작 구성 `SMSoptions`</span><span class="sxs-lookup"><span data-stu-id="ec42b-141">Configure startup to use `SMSoptions`</span></span>

<span data-ttu-id="ec42b-142">추가 `SMSoptions` 서비스 컨테이너에 `ConfigureServices` 에서 메서드는 *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="ec42b-142">Add `SMSoptions` to the service container in the `ConfigureServices` method in the *Startup.cs*:</span></span>

[!code-csharp[](2fa/sample/Web2FA/Startup.cs?name=snippet1&highlight=4)]

### <a name="enable-two-factor-authentication"></a><span data-ttu-id="ec42b-143">2 단계 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="ec42b-143">Enable two-factor authentication</span></span>

<span data-ttu-id="ec42b-144">열기는 *Views/Manage/Index.cshtml* Razor 파일 보기 및 주석 문자 (태그 없음 주석으로 처리 하므로) 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-144">Open the *Views/Manage/Index.cshtml* Razor view file and remove the comment characters (so no markup is commnted out).</span></span>

## <a name="log-in-with-two-factor-authentication"></a><span data-ttu-id="ec42b-145">2 단계 인증으로 로그인</span><span class="sxs-lookup"><span data-stu-id="ec42b-145">Log in with two-factor authentication</span></span>

* <span data-ttu-id="ec42b-146">응용 프로그램을 실행 하 고 새 사용자 등록</span><span class="sxs-lookup"><span data-stu-id="ec42b-146">Run the app and register a new user</span></span>

![Microsoft Edge에서 열려 있는 웹 응용 프로그램 등록 보기](2fa/_static/login2fa1.png)

* <span data-ttu-id="ec42b-148">탭을 활성화 하는 사용자 이름에는 `Index` 관리 컨트롤러의 동작 메서드에 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-148">Tap on your user name, which activates the `Index` action method in Manage controller.</span></span> <span data-ttu-id="ec42b-149">전화 번호를 탭 합니다 **추가** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-149">Then tap the phone number **Add** link.</span></span>

![보기를 관리](2fa/_static/login2fa2.png)

* <span data-ttu-id="ec42b-151">확인 코드를 수신 하 고 누릅니다 하 전화 번호 추가 **확인 코드를 보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-151">Add a phone number that will receive the verification code, and tap **Send verification code**.</span></span>

![전화 번호 페이지 추가](2fa/_static/login2fa3.png)

* <span data-ttu-id="ec42b-153">확인 코드가 있는 문자 메시지를 받아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-153">You will get a text message with the verification code.</span></span> <span data-ttu-id="ec42b-154">입력 하 고 탭 **제출**</span><span class="sxs-lookup"><span data-stu-id="ec42b-154">Enter it and tap **Submit**</span></span>

![전화 번호 페이지 확인](2fa/_static/login2fa4.png)

<span data-ttu-id="ec42b-156">문자 메시지를 얻지 못하면 twilio 로그 페이지를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ec42b-156">If you don't get a text message, see twilio log page.</span></span>

* <span data-ttu-id="ec42b-157">관리 보기는 성공적으로 추가 전화 번호를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-157">The Manage view shows your phone number was added successfully.</span></span>

![보기를 관리](2fa/_static/login2fa5.png)

* <span data-ttu-id="ec42b-159">탭 **사용** 2 단계 인증을 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-159">Tap **Enable** to enable two-factor authentication.</span></span>

![보기를 관리](2fa/_static/login2fa6.png)

### <a name="test-two-factor-authentication"></a><span data-ttu-id="ec42b-161">2 단계 인증 테스트</span><span class="sxs-lookup"><span data-stu-id="ec42b-161">Test two-factor authentication</span></span>

* <span data-ttu-id="ec42b-162">로그 오프 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-162">Log off.</span></span>

* <span data-ttu-id="ec42b-163">로그인</span><span class="sxs-lookup"><span data-stu-id="ec42b-163">Log in.</span></span>

* <span data-ttu-id="ec42b-164">2 단계 인증을 제공 해야 하므로 사용자 계정 2 단계 인증이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-164">The user account has enabled two-factor authentication, so you have to provide the second factor of authentication .</span></span> <span data-ttu-id="ec42b-165">이 자습서에서는 전화 확인 사용 하도록 설정한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-165">In this tutorial you have enabled phone verification.</span></span> <span data-ttu-id="ec42b-166">템플릿이 제공된은 두 번째 요소로 전자 메일을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-166">The built in templates also allow you to set up email as the second factor.</span></span> <span data-ttu-id="ec42b-167">QR 코드와 같은 인증에 대 한 추가 두 번째 요소를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-167">You can set up additional second factors for authentication such as QR codes.</span></span> <span data-ttu-id="ec42b-168">탭 **제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-168">Tap **Submit**.</span></span>

![확인 코드 보기 보내기](2fa/_static/login2fa7.png)

* <span data-ttu-id="ec42b-170">SMS 메시지에 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-170">Enter the code you get in the SMS message.</span></span>

* <span data-ttu-id="ec42b-171">클릭 하 고 **저장이 브라우저** 확인란 있습니다 2FA를 사용 하 여 동일한 장치 및 브라우저를 사용 하는 경우 로그온 하에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-171">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log on when using the same device and browser.</span></span> <span data-ttu-id="ec42b-172">2FA를 사용 하도록 설정 하 고 클릭 하 **저장이 브라우저** 알려 강력한 2FA 보호 장치에 액세스할 수 없는 상태로 회원님의 계정에 액세스 하려고 하는 악의적인 사용자 로부터 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-172">Enabling 2FA and clicking on **Remember this browser** will provide you with strong 2FA protection from malicious users trying to access your account, as long as they don't have access to your device.</span></span> <span data-ttu-id="ec42b-173">정기적으로 사용 하는 모든 개인 장치에서이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-173">You can do this on any private device you regularly use.</span></span> <span data-ttu-id="ec42b-174">설정 하 여 **저장이 브라우저**, 정기적으로 사용 하지 않는 장치에서 2FA의 강화 된 보안을 얻게 및에 자신의 장치에 2FA를 통과 하지 않아도 되는 편의성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-174">By setting  **Remember this browser**, you get the added security of 2FA from devices you don't regularly use, and you get the convenience on not having to go through 2FA on your own devices.</span></span>

![보기를 확인 합니다.](2fa/_static/login2fa8.png)

## <a name="account-lockout-for-protecting-against-brute-force-attacks"></a><span data-ttu-id="ec42b-176">무차별 암호 대입 공격 으로부터 보호 하기 위한 계정 잠금</span><span class="sxs-lookup"><span data-stu-id="ec42b-176">Account lockout for protecting against brute force attacks</span></span>

<span data-ttu-id="ec42b-177">계정 잠금은 2FA 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-177">Account lockout is recommended with 2FA.</span></span> <span data-ttu-id="ec42b-178">사용자가 로컬 계정 또는 소셜 계정을 통해 로그인 2FA에서 연결 시도가 실패할된 때마다 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-178">Once a user signs in through a local account or social account, each failed attempt at 2FA is stored.</span></span> <span data-ttu-id="ec42b-179">사용자를 잠그기 실패 한 최대 액세스 시도 횟수에 도달 하면 (기본값: 5에 대 한 액세스 시도가 실패 한 잠금 5 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-179">If the maximum failed access attempts is reached, the user is locked out (default: 5 minute lockout after 5 failed access attempts).</span></span> <span data-ttu-id="ec42b-180">실패 한 액세스 시도 횟수를 다시 설정 하 고 클록을 기본값으로 다시 설정 하는 성공적으로 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-180">A successful authentication resets the failed access attempts count and resets the clock.</span></span> <span data-ttu-id="ec42b-181">최대 액세스 시도 하지 못했습니다. 잠금 시간으로 설정할 수 있습니다 및 [MaxFailedAccessAttempts](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts) 및 [DefaultLockoutTimeSpan](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-181">The maximum failed access attempts and lockout time can be set with [MaxFailedAccessAttempts](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts) and [DefaultLockoutTimeSpan](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan).</span></span> <span data-ttu-id="ec42b-182">다음 계정 잠금 10 액세스 시도 실패 한 후 10 분 동안으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec42b-182">The following configures account lockout for 10 minutes after 10 failed access attempts:</span></span>

[!code-csharp[](2fa/sample/Web2FA/Startup.cs?name=snippet2&highlight=13-17)]

<span data-ttu-id="ec42b-183">확인 [PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync) 설정 `lockoutOnFailure` 를 `true`:</span><span class="sxs-lookup"><span data-stu-id="ec42b-183">Confirm that [PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync) sets `lockoutOnFailure` to `true`:</span></span>

```csharp
var result = await _signInManager.PasswordSignInAsync(
                 Input.Email, Input.Password, Input.RememberMe, lockoutOnFailure: true);
```
