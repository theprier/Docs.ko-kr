---
uid: mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
title: SMS 및 전자 메일 2 단계 인증을 사용 하 여 ASP.NET MVC 5 앱 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 2 단계 인증을 사용 하 여 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다. 만들기는 보안 ASP.NET MVC 5 웹 앱을 완료 해야 하는 중...
ms.author: riande
ms.date: 08/20/2015
ms.assetid: f50a5cdb-c06a-46ed-aa14-fc5b049dc8dc
msc.legacyurl: /mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: 97b73c5ae18a528d33b44a4de4afc434ac46af48
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577602"
---
<a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a>SMS 및 전자 메일 2 단계 인증을 사용 하 여 ASP.NET MVC 5 앱
====================
[Rick Anderson]((https://twitter.com/RickAndMSFT))

> 이 자습서에서는 2 단계 인증을 사용 하 여 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다. 완료 해야 [로그인, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET MVC 5 웹 앱을 만들기](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) 계속 하기 전에 합니다. 완성된 된 응용 프로그램을 다운로드할 수 있습니다 [여기](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)합니다. 다운로드는 전자 메일 또는 SMS 공급자를 설정 하지 않고 SMS 및 전자 메일 확인을 테스트할 수 있도록 디버깅 도우미를 포함 합니다.
> 
> 이 자습서를 통해 작성 했습니다 [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) ).


- [ASP.NET MVC 앱 만들기](#createMvc)
- [SMS 2 단계 인증에 대 한 설정](#SMS)
- [2 단계 인증을 사용 하도록 설정](#enable2)
- [추가 리소스](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>ASP.NET MVC 앱 만들기

설치 및 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 하거나 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다. 설치할 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상.

> [!NOTE]
> 경고: 완료 해야 [로그인, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET MVC 5 웹 앱을 만들기](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) 계속 하기 전에 합니다. 설치 해야 합니다 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상이 자습서를 완료 합니다.


1. 새 ASP.NET 웹 프로젝트를 만들고 MVC 템플릿을 선택 합니다. 또한 web Forms web forms 앱에서 비슷한 단계를 수행할 수 있도록 ASP.NET Id를 지원 합니다.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. 기본 인증을 유지 **개별 사용자 계정**합니다. Azure에서 앱을 호스트 하려는 경우 확인란을 선택한 상태로 둡니다. 자습서의 뒷부분에 나오는 Azure에 배포 됩니다. 할 수 있습니다 [Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)합니다.
3. 설정 된 [SSL을 사용 하도록 프로젝트](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.

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
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   주소:  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   네임스페이스:  
    `ASPSMSX2`
3. **SMS 공급자 사용자 자격 증명 확인**  
  
   Twilio:  
   **대시보드** 탭의 Twilio 계정에 복사 합니다 **계정 SID** 및 **인증 토큰**합니다.  
  
   ASPSMS:  
   계정 설정을에서 이동 **Userkey** 에 자체 정의 된 함께 복사해 **암호**합니다.  
  
   저장 하겠습니다. 나중에 이러한 값을 *web.config* 키 파일 `"SMSAccountIdentification"` 고 `"SMSAccountPassword"` 입니다.
4. **SenderID 지정 / 송신자**  
  
   Twilio:  
   **숫자** 탭, Twilio 전화 번호를 복사 합니다.  
  
   ASPSMS:  
   내 합니다 **보낸 사람 잠금 해제** 메뉴에서 하나 이상의 보낸 사람을 잠금 해제 또는 영숫자 송신자 (모든 네트워크에서 지원 되지 않음)를 선택 합니다.  
  
   저장 하겠습니다. 나중에이 값은 *web.config* 내 키 파일 `"SMSAccountFrom"` 합니다.
5. **앱에 SMS 공급자 자격 증명 전송**  
  
   자격 증명 및 보낸 사람에 게 전화 번호를 앱에 사용할 수 있도록 합니다. 간단 하 게 저장 하겠습니다. 이러한 값을 *web.config* 파일입니다. Azure에 배포 했습니다 하는 경우에 안전 하 게 값을 저장할 수는 **앱 설정** 웹 사이트에서 섹션 구성 탭 합니다. 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > 보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다. 계정 및 자격 증명을 단순하게 유지 하기 위해 샘플 위의 코드에 추가 됩니다. 참조 [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.
6. **SMS 공급자 간 데이터 전송의 구현**  
  
   구성 된 `SmsService` 클래스를 *앱\_Start\IdentityConfig.cs* 파일입니다.  
  
   사용 되는 SMS 공급자에 따라 하나를 활성화 합니다 **Twilio** 또는 **ASPSMS** 섹션: 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. 업데이트를 *Views\Manage\Index.cshtml* Razor 뷰: (참고:만 기존 코드의 주석을 제거, 아래 코드를 사용 하지 않습니다.)  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. 확인 합니다 `EnableTwoFactorAuthentication` 및 `DisableTwoFactorAuthentication` 의 작업 메서드는 `ManageController` 가[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) 특성:  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. 앱을 실행 하 고 이전에 등록 한 계정으로 로그인 합니다.
10. 활성화 하는 사용자 ID를 클릭 합니다 `Index` 의 동작 메서드에 `Manage` 컨트롤러입니다.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. 추가 클릭 합니다.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. `AddPhoneNumber` 작업 메서드는 SMS 메시지를 받을 수 있는 전화 번호를 입력 하는 대화 상자를 표시 합니다.

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. 몇 초 안에 확인 코드로 문자 메시지를 표시 됩니다. Enter 키를 눌러 **제출**합니다.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. 관리 보기를 보여 줍니다 전화 번호 추가 되었습니다.

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a>2 단계 인증을 사용 하도록 설정

생성 된 템플릿 앱에서 UI를 사용 하 여 2 단계 인증 (2FA)를 사용 하도록 설정 해야 합니다. 2FA를 사용 하도록 설정 하려면 탐색 모음에서 사용자 ID (전자 메일 별칭)를 클릭 합니다.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

Enable 2FA를 클릭 합니다.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

로그 아웃 한 다음 다시 로그인 합니다. 전자 메일을 사용 하도록 설정한 경우 (참조 내 [이전 자습서](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), SMS 또는 2FA 위한 전자 메일을 선택할 수 있습니다.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

확인 코드 페이지 (SMS 또는 전자 메일)에서 코드를 입력할 수 있는 표시 됩니다.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

클릭 하 여 **이 브라우저 기억** 확인란 있습니다 2FA를 사용 하 여 브라우저 및 장치 상자를 선택한 경우 로그에 기록 하는 데 필요한에서 제외 됩니다. 악의적인 사용자가 장치에 액세스할 수 없습니다, 2FA를 사용 하도록 설정 하 고 클릭 하 여 **이 브라우저 기억** 하면 편리 하 게 한 번 암호 액세스가 있는 모든 액세스에 대 한 강력한 2FA 보호를 유지 하면서 트러스트 되지 않은 장치입니다. 정기적으로 사용 하는 모든 개인 장치에서이 수행할 수 있습니다.

이 자습서에서는 새 ASP.NET MVC 앱에서 2FA를 사용 하도록 설정 하는 빠른 소개 합니다. 내 자습서 [ASP.NET Id와 SMS 및 전자 메일을 사용 하 여 2 단계 인증](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) 샘플 코드에 대해 자세히입니다.

<a id="addRes"></a>
## <a name="additional-resources"></a>추가 리소스

- [ASP.NET Id와 SMS 및 전자 메일을 사용 하 여 2 단계 인증](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) 2 단계 인증에서 세부 정보로 이동
- [링크를 ASP.NET Id 권장 리소스](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [계정 확인 및 ASP.NET Id와 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 암호 복구 및 계정 확인에 대 한 자세한 내용으로 이어집니다.
- [Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on을 사용 하 여 MVC 5 앱](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 이 자습서에서는 Facebook 및 Google OAuth 2 권한 부여를 사용 하 여 ASP.NET MVC 5 앱을 작성 하는 방법을 보여 줍니다. 또한 Id 데이터베이스에 데이터를 추가 하는 방법을 보여 줍니다.
- [멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET MVC 앱을 Azure 웹 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. 이 자습서는 Azure 배포 추가 역할을 사용 하 여 앱을 보호 하는 방법을 멤버 자격 API를 사용 하 여 사용자 및 역할 및 추가 보안 기능을 추가 하는 방법입니다.
- [OAuth 2 용 Google 앱 만들기 및 앱 프로젝트에 연결](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [Facebook에서 앱을 만들고 앱 프로젝트에 연결](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [프로젝트의 SSL 설정](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
