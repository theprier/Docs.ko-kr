---
uid: identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
title: ASP.NET Id와 SMS 및 전자 메일을 사용 하 여 2 단계 인증 | Microsoft Docs
author: HaoK
description: 이 자습서에서는 SMS 및 전자 메일을 사용 하 여 2 단계 인증 (2FA)을 설정 하는 방법을 보여줍니다. Rick anderson이 문서가 작성 된 ( @RickAndMSFT ) Pr.,...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/15/2015
ms.topic: article
ms.assetid: 053e23c4-13c9-40fa-87cb-3e9b0823b31e
ms.technology: ''
msc.legacyurl: /identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0519ae69b3d2ef129d206a936b199f781fef5bf6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399681"
---
<a name="two-factor-authentication-using-sms-and-email-with-aspnet-identity"></a>ASP.NET Id와 SMS 및 전자 메일을 사용 하 여 2 단계 인증
====================
하 여 [Hao 둘러싼](https://github.com/HaoK)를 [Pranav Rastogi](https://github.com/rustd)하십시오 [Rick Anderson](https://github.com/Rick-Anderson), [Suhas Joshi](https://github.com/suhasj)

> 이 자습서에서는 SMS 및 전자 메일을 사용 하 여 2 단계 인증 (2FA)을 설정 하는 방법을 보여줍니다.
> 
> Rick anderson이 문서가 작성 된 ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), Hao 둘러싼 및 Suhas Joshi 합니다. NuGet 샘플 Hao 둘러싼 기본적 작성 되었습니다.


이 항목에서는 다음 다룹니다.

- [Identity 샘플 빌드](#build)
- [SMS 2 단계 인증에 대 한 설정](#SMS)
- [2 단계 인증을 사용 하도록 설정](#enable2)
- [2 단계 인증 공급자를 등록 하는 방법](#reg)
- [로컬 및 소셜 로그인 계정을 병합합니다](#combine)
- [무작위 공격 으로부터 계정 잠금](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a>Identity 샘플 빌드

이 섹션에서는 노력할 샘플을 다운로드 하려면 NuGet을 사용 합니다. 설치 및 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 하거나 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다. Visual Studio를 설치 [2013 업데이트 2](https://go.microsoft.com/fwlink/?LinkId=390521) 이상.

> [!NOTE]
> 경고: Visual Studio를 설치 해야 [2013 업데이트 2](https://go.microsoft.com/fwlink/?LinkId=390521) 이 자습서를 완료 합니다.


1. 새 ***빈*** ASP.NET 웹 프로젝트입니다.
2. 다음을 입력 하는 패키지 관리자 콘솔에서 다음 명령을:  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   이 자습서에서는 [SendGrid](http://sendgrid.com/) 전자 메일을 보내는 하 고 [Twilio](https://www.twilio.com/) 하거나 [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) sms 문자 보내기에 대 한 합니다. `Identity.Samples` 패키지에서는 사용할 코드를 설치 합니다.
3. 설정 된 [SSL을 사용 하도록 프로젝트](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.
4. *선택적*:의 지침에 따라 내 [전자 메일 확인 자습서](account-confirmation-and-password-recovery-with-aspnet-identity.md) SendGrid 후크 다음 앱을 실행 및 전자 메일 계정을 등록 합니다.
5. * 선택 사항: * 샘플에서 데모 전자 메일 링크 확인 코드를 제거 (의 `ViewBag.Link` account 컨트롤러의 코드입니다. 참조 된 `DisplayEmail` 및 `ForgotPasswordConfirmation` razor 뷰와 작업 메서드).
6. <em>선택 사항: * 제거 합니다 `ViewBag.Status` 코드는 *Views\Account\VerifyCode.cshtml 관리 및 계정 컨트롤러에서 들어오고</em> 및 <em>Views\Manage\VerifyPhoneNumber.cshtml</em> razor 뷰. 유지할 수 있습니다는 `ViewBag.Status` 후크 및 전자 메일 및 SMS 메시지를 보낼 필요 없이 로컬에서이 앱은 작동 하는 방법을 테스트 하려면 표시 합니다.

> [!NOTE]
> 경고:이 샘플의 보안 설정을 변경 하면 프로덕션 앱 변경 내용을 명시적으로 호출 하는 보안 감사를 진행 해야 합니다.


<a id="SMS"></a>

## <a name="set-up-sms-for-two-factor-authentication"></a>SMS 2 단계 인증에 대 한 설정

이 자습서에서는 Twilio 또는 ASPSMS 중 하나를 사용 하 여에 대 한 지침을 제공 하지만 다른 SMS 공급자를 사용할 수 있습니다.

1. **SMS 공급자를 사용 하 여 사용자 계정 만들기**  
  
   만들기는 [Twilio](https://www.twilio.com/try-twilio) 요소나 [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) 계정.
2. **추가 패키지를 설치 하거나 서비스 참조 추가**  
  
   Twilio:  
   패키지 관리자 콘솔에서 다음 명령을 입력 합니다.  
    `Install-Package Twilio`  
  
   ASPSMS:  
   다음 서비스 참조를 추가 해야 합니다.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   주소:  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   네임스페이스:  
    `ASPSMSX2`
3. **SMS 공급자 사용자 자격 증명 확인**  
  
   Twilio:  
   **대시보드** 탭의 Twilio 계정에 복사 합니다 **계정 SID** 및 **인증 토큰**합니다.  
  
   ASPSMS:  
   계정 설정을에서 이동 **Userkey** 에 자체 정의 된 함께 복사해 **암호**합니다.  
  
   나중에 이러한 값 변수에 저장 됩니다 `SMSAccountIdentification` 고 `SMSAccountPassword` 입니다.
4. **SenderID 지정 / 송신자**  
  
   Twilio:  
   **숫자** 탭, Twilio 전화 번호를 복사 합니다.  
  
   ASPSMS:  
   내 합니다 **보낸 사람 잠금 해제** 메뉴에서 하나 이상의 보낸 사람을 잠금 해제 또는 영숫자 송신자 (모든 네트워크에서 지원 되지 않음)를 선택 합니다.  
  
   변수이 값이 나중에 저장할 `SMSAccountFrom` 합니다.
5. **앱에 SMS 공급자 자격 증명 전송**  
  
   자격 증명 및 보낸 사람에 게 전화 번호를 앱에 사용할 수 있도록 합니다.

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > 보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다. 계정 및 자격 증명을 단순하게 유지 하기 위해 샘플 위의 코드에 추가 됩니다. Jon Atten의를 참조 하세요 [ASP.NET MVC: 소스 제어의 개인 설정 확장 유지](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)합니다.
6. **SMS 공급자 간 데이터 전송의 구현**  
  
   구성 된 `SmsService` 클래스를 *앱\_Start\IdentityConfig.cs* 파일입니다.  
  
   사용 되는 SMS 공급자에 따라 하나를 활성화 합니다 **Twilio** 또는 **ASPSMS** 섹션: 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. 앱을 실행 하 고 이전에 등록 한 계정으로 로그인 합니다.
8. 활성화 하는 사용자 ID를 클릭 합니다 `Index` 의 동작 메서드에 `Manage` 컨트롤러입니다.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. 추가 클릭 합니다.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. 몇 초 안에 확인 코드로 문자 메시지를 표시 됩니다. Enter 키를 눌러 **제출**합니다.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. 관리 보기를 보여 줍니다 전화 번호 추가 되었습니다.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a>코드 검사

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

합니다 `Index` 의 동작 메서드에 `Manage` 컨트롤러 이전 작업을 기반으로 상태 메시지를 설정 하 고 로컬 암호를 변경 하거나 로컬 계정을 추가에 대 한 링크를 제공 합니다. `Index` 메서드 또한 상태를 표시 하거나에 2fa가 전화 번호, 외부 로그인, 2FA를 사용 하도록 설정 하 고 (나중에 설명)이이 브라우저에 대 한 2FA 메서드. 제목 표시줄에 프로그램 사용자 ID (메일)를 클릭 하면 메시지를 전달 하지 않습니다. 클릭 하 여 **전화 번호: 제거** 전달 링크 `Message=RemovePhoneSuccess` 쿼리 문자열로.  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]

`AddPhoneNumber` 작업 메서드는 SMS 메시지를 받을 수 있는 전화 번호를 입력 하는 대화 상자를 표시 합니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

클릭 하는 **확인 코드 보내기** HTTP POST로 전화 번호를 게시 하는 단추 `AddPhoneNumber` 작업 메서드.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

`GenerateChangePhoneNumberTokenAsync` 메서드 SMS 메시지에서 설정할 수 있는 보안 토큰을 생성 합니다. SMS 서비스를 구성한 경우 토큰 문자열로 보내집니다 &quot;보안 코드가 &lt;토큰&gt;&quot;합니다. `SmsService.SendAsync` 메서드를 비동기적으로 라고 한 다음 앱의 리디렉션는 `VerifyPhoneNumber` 작업 메서드 (다음 대화 상자를 표시 하는), 확인 코드를 입력할 수 있습니다.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

코드는 HTTP POST에 게시 된 코드를 입력 하 고 제출을 클릭 `VerifyPhoneNumber` 작업 메서드.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

`ChangePhoneNumberAsync` 메서드는 게시 된 보안 코드를 확인 합니다. 전화 번호를 추가할 코드를 올바른 경우 합니다 `PhoneNumber` 필드는 `AspNetUsers` 테이블입니다. 해당 호출에 성공 하면는 `SignInAsync` 메서드가 호출 됩니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

`isPersistent` 매개 변수 인증 세션이 여러 요청 간에 지속가 있는지 여부를 설정 합니다.

새 보안 스탬프를 보안 프로필을 변경 하면 생성 되 고 저장 합니다 `SecurityStamp` 필드를 *AspNetUsers* 테이블입니다. 에 `SecurityStamp` 필드 보안 쿠키와에서 다릅니다. 보안 쿠키에 저장 되어 있지는 `AspNetUsers` 테이블 (또는 Identity DB의 다른 곳). 보안 쿠키 토큰을 사용 하 여 자체 서명 됩니다 [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) 으로 생성 됩니다는 `UserId, SecurityStamp` 및 만료 시간 정보입니다.

쿠키 미들웨어는 각 요청에 쿠키를 확인 합니다. `SecurityStampValidator` 의 메서드를 `Startup` 클래스는 DB에 도달 하 고 보안 스탬프를 주기적으로 확인 지정 된 대로 `validateInterval`합니다. 이 보안 프로필을 변경 하지 않는 한 (샘플)에서 30 분 마다만 발생 합니다. 데이터베이스에 대 한 왕복을 최소화 하기 위해 30 분 간격을 선택 했습니다.

`SignInAsync` 메서드를 보안 프로필에 변경 될 때 호출 해야 합니다. 보안 프로필 변경 되 면 데이터베이스가 업데이트를 `SecurityStamp` 필드 및 호출 하지 않고는 `SignInAsync` 메서드는 로그인 유지 *만* 다음 OWIN 파이프라인을 시간까지 데이터베이스에 연결 (합니다 `validateInterval`). 변경 하 여 테스트할 수 있습니다 합니다 `SignInAsync` 즉시 반환 하는 방법 및 쿠키 설정 `validateInterval` 속성 30 분을 5 초에서:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

위의 코드 변경 내용을 사용 하 여 보안 프로필을 변경할 수 있습니다 (의 상태를 변경 하는 예를 들어 **두 개의 요소 사용**) 및 5 초 이내에 로그인 됩니다 때는 `SecurityStampValidator.OnValidateIdentity` 메서드가 실패 하면 합니다. 반환 하는 줄을 제거 합니다 `SignInAsync` 메서드를 변경 하는 다른 보안 프로필을 만들고 없습니다 수 로그 아웃 됩니다. `SignInAsync` 메서드는 새 보안 쿠키를 생성 합니다.

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a>2 단계 인증을 사용 하도록 설정

샘플 앱에서 UI를 사용 하 여 2 단계 인증 (2FA)를 사용 하도록 설정 해야 합니다. 2FA를 사용 하도록 설정 하려면 탐색 모음에서 사용자 ID (전자 메일 별칭)를 클릭 합니다.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)  
Enable 2FA를 클릭 합니다.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png) 로그 아웃 한 다음 다시 로그인 합니다. 전자 메일을 사용 하도록 설정한 경우 (참조 내 [이전 자습서](account-confirmation-and-password-recovery-with-aspnet-identity.md)), SMS 또는 2FA 위한 전자 메일을 선택할 수 있습니다.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png) 확인 코드 페이지 (SMS 또는 전자 메일)에서 코드를 입력할 수 있는 표시 됩니다.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png) 클릭 하 여 **이 브라우저 기억** 확인란 있습니다 2FA를 사용 하 여 해당 컴퓨터 및 브라우저를 사용 하 여 로그온 할 필요가에서 제외 됩니다. 2FA를 사용 하도록 설정 하 고 클릭 하 여 **이 브라우저 기억** 하면 강력한 2FA 보호를 사용 하 여 컴퓨터에 액세스할 수 있다면 사용자 계정에 액세스 하려고 하는 악의적인 사용자 로부터 합니다. 정기적으로 사용 하는 모든 개인 컴퓨터에서이 수행할 수 있습니다. 설정 하 여 **이 브라우저 기억**정기적으로 사용 하지 않는 컴퓨터에서 추가 보안을 2FA 얻게 하 고 고유한 컴퓨터 2FA를 통해 이동 하지 않아도에서 편리 하 게 표시 합니다. 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a>2 단계 인증 공급자를 등록 하는 방법

새 MVC 프로젝트를 만들 때 합니다 *IdentityConfig.cs* 파일 2 단계 인증 공급자를 등록 하려면 다음 코드를 포함 합니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a>2FA 위한 전화 번호 추가

합니다 `AddPhoneNumber` 의 동작 메서드에 `Manage` 컨트롤러 보안 토큰을 생성 및 전송 수를 숫자 전화를 제공 합니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

토큰을 보낸 후 리디렉션됩니다는 `VerifyPhoneNumber` 작업 메서드를 2FA에 대 한 SMS를 등록 하는 코드를 입력할 수 있습니다. 전화 번호를 확인 하기 전에 SMS 2fa가 사용 되지 않습니다.

## <a name="enabling-2fa"></a>2FA를 사용 하도록 설정

`EnableTFA` 작업 메서드는 2FA를 사용 합니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

참고는 `SignInAsync` 사용 2FA 보안 프로필에 대 한 변경 이므로 호출 해야 합니다. 2FA를 사용 하는 경우 사용자 해야 2FA를 사용 하 여 로그인 (SMS 및 전자 메일 샘플에서) 등록 하는 2FA 방법을 사용 하 합니다.

QR 코드 생성기 같은 자세한 2FA 공급자를 추가 하거나 자신이 작성할 수 있습니다 (참조 [ASP.NET Id를 사용 하 여 Google 인증자를 사용 하 여](http://www.beabigrockstar.com/blog/using-google-authenticator-asp-net-identity/)).

> [!NOTE]
> 2FA 코드를 사용 하 여 생성 됩니다 [일회용 암호 알고리즘 시간 기반](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) 및 6 분 후 코드 유효 합니다. 코드를 입력 하는 데 6 분 넘게를 사용 하는 경우 잘못 된 코드 오류 메시지가 표시 됩니다.


<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a>로컬 및 소셜 로그인 계정을 병합합니다

로컬 및 소셜 계정 전자 메일 링크를 클릭 하 여 결합할 수 있습니다. 다음 순서로 &quot; RickAndMSFT@gmail.com &quot; 로컬 로그인으로 처음 만들어질가 첫 번째는 소셜 로그인으로 계정을 만든 다음 로컬 로그인을 추가 하지만 합니다.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

클릭 합니다 **관리** 링크 합니다. 이 계정과 연결 된 참고 0 외부 (소셜 로그인)

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

서비스에서 다른 로그에 대 한 링크를 클릭 하 고 앱 요청을 수락 합니다. 두 개의 계정을 결합 되었습니다, 그리고 두 계정으로 로그온 할 수 있습니다. 사용자가 소셜 로그인 인증 서비스를 중단 되었거나 가능성이 소셜 계정에 대 한 액세스를 손실가 되는 경우 로컬 계정에 추가할 수 있습니다.

다음 그림과에서 Tom은 소셜 로그인 (에서 볼 수 있는 합니다 **외부 로그인: 1** 페이지에 표시).

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

클릭할 **암호 선택** 동일한 계정에 연결 된 로컬 로그에 추가할 수 있습니다.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a>무작위 공격 으로부터 계정 잠금

사용자 잠금 사용 하 여 사전 공격 으로부터 앱에서 계정을 보호할 수 있습니다. 다음 코드는 `ApplicationUserManager Create` 메서드 구성 잠금:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

위의 코드에만 2 단계 인증에 대 한 잠금 수 있습니다. 로그인에 대 한 잠금 변경 하 여 설정할 수 있습니다. 하지만 `shouldLockout` 를 true로 합니다 `Login` account 컨트롤러의 메서드를 권장 만들므로 계정에 취약 하지 로그인에 대 한 잠금 사용 [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) 로그인 공격입니다. 만든 관리자 계정에 대 한 샘플 코드에서 잠금 해제 되어를 `ApplicationDbInitializer Seed` 메서드:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a>유효성이 검사 된 전자 메일 계정이 사용자 요청

다음 코드에 사용자를를 로그인 할 수 있는 전에 유효성이 검사 된 전자 메일 계정이 필요 합니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a>SignInManager는 2FA 요구 사항을 확인 하는 방법

로컬 로그인와 소셜 로그인 2FA를 설정할지 여부를 확인 합니다. 2FA를 사용 하는 경우는 `SignInManager` 로그온 메서드 반환 `SignInStatus.RequiresVerification`, 사용자가 리디렉션됩니다는 `SendCode` 동작 메서드에 있는 순서로 로그를 완료 하는 코드를 입력 해야 합니다. RememberMe 있으면 사용자가 로컬 쿠키에 설정 되어는 `SignInManager` 돌아갑니다 `SignInStatus.Success` 을 2FA를 통해 이동할 수 없습니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

다음 코드에서는 `SendCode` 동작 메서드가 있습니다. A [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) 사용자에 대해 사용 하도록 설정 하는 모든 2FA 메서드를 사용 하 여 만들어집니다. 합니다 [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) 에 전달 되는 [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) 2FA 접근 방식 (일반적으로 전자 메일 및 SMS)를 선택할 수 있는 도우미입니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

2FA 방법은 사용자가 게시 되 면를 `HTTP POST SendCode` 동작 메서드가 호출 되는 `SignInManager` 2FA 코드와 사용자가 리디렉션됩니다 보냅니다는 `VerifyCode` 로그인을 완료 하는 코드를 입력할 수 있는 작업 메서드.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a>2FA 잠금

계정 잠금에 로그인 암호 시도 실패를 설정할 수 있지만 해당 방법을 사용 하면 로그인에 취약 [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) 잠금을 수행 합니다. 계정 잠금 2FA를 사용 하 여만 사용 하는 것이 좋습니다. 경우는 `ApplicationUserManager` 는 샘플 코드는 2FA 잠금 설정 생성 및 `MaxFailedAccessAttemptsBeforeLockout` 5입니다. 사용자가 로컬 계정 또는 소셜 계정) (통해 로그인, 2FA에서 연결 시도가 실패할된 때마다 저장 되 고 최대 시도 횟수에 도달 하는 경우 사용자가 잠길 5 분 (잠금 시간을 설정할 수 있습니다 `DefaultAccountLockoutTimeSpan`).

<a id="addRes"></a>

## <a name="additional-resources"></a>추가 리소스

- [ASP.NET Id 권장 리소스](../getting-started/aspnet-identity-recommended-resources.md) Id 블로그, 비디오, 자습서 및 유용한의 전체 목록은 지금 연결 합니다.
- [Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on을 사용 하 여 MVC 5 앱](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 또한 사용자가 테이블에 프로필 정보를 추가 하는 방법을 보여 줍니다.
- [ASP.NET MVC 및 Id 2.0: 기본 사항 이해](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) John Atten 여 합니다.
- [계정 확인 및 ASP.NET Id와 암호 복구](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET ID 소개](../getting-started/introduction-to-aspnet-identity.md)
- [ASP.NET Id 2.0.0의 RTM 발표](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) Pranav rastogi 합니다.
- [ASP.NET Id 2.0: 계정 유효성 검사 및 2 단계 인증 설정](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) John Atten 여 합니다.
