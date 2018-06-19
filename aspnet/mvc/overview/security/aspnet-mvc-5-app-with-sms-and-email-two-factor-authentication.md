---
uid: mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
title: SMS 및 전자 메일 2 단계 인증을 사용 하는 ASP.NET MVC 5 앱 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 2 단계 인증을 사용 하 여 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다. 웹 앱을 만들기 보안 ASP.NET MVC 5 완료 해야...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/20/2015
ms.topic: article
ms.assetid: f50a5cdb-c06a-46ed-aa14-fc5b049dc8dc
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: 5e1c54b3901f2c8c85134445c1fa91ee9f2e0d59
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30873614"
---
<a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a>SMS 및 전자 메일 2 단계 인증을 사용 하는 ASP.NET MVC 5 앱
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서 2 단계 인증을 사용 하 여 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다. 완료 해야 [전자 메일 확인 및 암호 재설정에 대 한 로그와 보안 ASP.NET MVC 5 웹 응용 프로그램을 만들](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) 계속 진행 하기 전에. 완성 된 응용 프로그램을 다운로드할 수 있습니다 [여기](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)합니다. 다운로드는 전자 메일 또는 SMS 공급자를 설정 하지 않고 전자 메일 확인 및 SMS를 테스트할 수 있도록 하는 디버깅 도우미를 포함 합니다.
> 
> 이 자습서에 의해 작성 되었으므로 [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) ).


- [ASP.NET MVC 응용 프로그램 만들기](#createMvc)
- [2 단계 인증에 대 한 SMS를 설정 합니다.](#SMS)
- [2 단계 인증을 사용 하도록 설정](#enable2)
- [추가 리소스](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>ASP.NET MVC 응용 프로그램 만들기

설치 하 고 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다. 설치 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상.

> [!NOTE]
> 경고: 완료 해야 [전자 메일 확인 및 암호 재설정에 대 한 로그와 보안 ASP.NET MVC 5 웹 응용 프로그램을 만들](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) 계속 진행 하기 전에. 설치 해야 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 하려면이 자습서를 완료 합니다.


1. 새 ASP.NET 웹 프로젝트를 만들고 MVC 템플릿을 선택 합니다. Web Forms web forms 응용 프로그램에서 비슷한 단계를 반영할 수 있도록 ASP.NET Id를도 지원 합니다.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. 기본 인증을 두고 **개별 사용자 계정**합니다. Azure에서 응용 프로그램 호스트 하려는 경우 확인란을 선택한 상태로 둡니다. 이 자습서의 뒷부분에 나오는에서는 Azure에 배포 합니다. 있습니다 수 [무료로 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)합니다.
3. 설정의 [SSL을 사용 하도록 프로젝트](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.

<a id="SMS"></a>
## <a name="set-up-sms-for-two-factor-authentication"></a>2 단계 인증에 대 한 SMS를 설정 합니다.

이 자습서에서는 Twilio 또는 ASPSMS 중 하나를 사용 하기 위한 지침을 제공 하지만 다른 SMS 공급자를 사용할 수 있습니다.

1. **SMS 공급자를 사용 하 여 사용자 계정 만들기**  
  
   만들기는 [Twilio](https://www.twilio.com/try-twilio) 또는 [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) 계정.
2. **추가 패키지 설치 또는 서비스 참조 추가**  
  
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
3. **SMS 공급자 사용자 자격 증명을 파악**  
  
   Twilio:  
   **대시보드** 복사 Twilio 계정 탭의 **계정 SID** 및 **인증 토큰**합니다.  
  
   ASPSMS:  
   계정 설정을에서으로 이동 **사용자 키로** 자체 정의 함께 복사 및 **암호**합니다.  
  
   나중에 이러한 값에 저장할는 *web.config* 내 키 파일 `"SMSAccountIdentification"` 및 `"SMSAccountPassword"` 합니다.
4. **SenderID 지정 / 송신자**  
  
   Twilio:  
   **숫자** 탭, Twilio 전화 번호를 복사 합니다.  
  
   ASPSMS:  
   내에서 **잠금 해제 보낸 사람** 메뉴를 사용 하거나 하나 이상의 보낸 사람을 잠금 해제 (모든 네트워크에서 지원 되지 않음)에 영숫자 보낸 사람이 선택 합니다.  
  
   저장 하겠습니다. 나중에이 값은 *web.config* 내 키 파일 `"SMSAccountFrom"` 합니다.
5. **응용 프로그램에 SMS 공급자 자격 증명 전송**  
  
   자격 증명 및 보낸 사람에 게 전화 번호가 응용 프로그램에 사용할 수 있도록 합니다. 간단 하 게 저장 하겠습니다. 이러한 값에는 *web.config* 파일입니다. Azure에 배포 하기 하는 경우에 안전 하 게 값을 저장할 수 우리는 **앱 설정** 웹 사이트에서 섹션 구성 탭 합니다. 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > 보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다. 계정 및 자격 증명은 위의 예제를 단순하게 유지 하기 위해 코드에 추가 됩니다. 참조 [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.
6. **SMS 공급자에 데이터 전송의 구현**  
  
   구성에서 `SmsService` 클래스에 *앱\_Start\IdentityConfig.cs* 파일입니다.  
  
   사용 되는 SMS 공급자에 따라 활성화 중 하나는 **Twilio** 또는 **ASPSMS** 섹션: 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. 업데이트는 *Views\Manage\Index.cshtml* Razor 보기: (참고: 기존 코드에서 주석을 제거, 아래 코드를 사용 하 여 방금 하지 마십시오.)  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. 확인 된 `EnableTwoFactorAuthentication` 및 `DisableTwoFactorAuthentication` 의 작업 메서드는 `ManageController` 가[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) 특성:  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. 응용 프로그램을 실행 하 고 이전에 등록 하는 계정으로 로그인 합니다.
10. 활성화 하는 사용자 ID, 클릭는 `Index` 의 동작 메서드에 `Manage` 컨트롤러입니다.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. 추가 클릭 합니다.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. `AddPhoneNumber` 동작 메서드 SMS 메시지를 받을 수 있는 전화 번호를 입력 하는 대화 상자를 표시 합니다.

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. 몇 초 후에 확인 코드를 있는 문자 메시지를 받아볼 수 있습니다. 입력 하 고 키를 눌러 **전송**합니다.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. 관리 보기 표시 전화 번호가 추가 되었습니다.

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a>2 단계 인증을 사용 하도록 설정

서식 파일 생성 된 응용 프로그램에서 UI를 사용 하 여 2 단계 인증 (2FA)를 사용 하도록 설정 해야 합니다. 2FA를 활성화 하려면 탐색 모음에서 사용자 ID (전자 메일 별칭)을 클릭 합니다.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

Enable 2FA 클릭 합니다.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

로그 아웃 한 다음 다시 로그인 합니다. 전자 메일을 활성화 한 경우 (참조 내 [이전 자습서](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)), SMS 또는 2FA에 대 한 전자 메일을 선택할 수 있습니다.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

확인 코드 페이지 (SMS 또는 전자 메일)에서 코드를 입력할 수 있는 표시 됩니다.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

클릭 하 고 **저장이 브라우저** 확인란 있습니다 사용할 브라우저와 장치 상자를 선택한 경우 로그인에 2FA 사용 하지 않아도 제외 됩니다. 악의적인 사용자가 장치에 액세스할 수 없습니다,으로 2FA 활성화를 클릭 하 고 **저장이 브라우저** 알려 편리 하 게 한 번 암호 액세스할 모든 액세스에 대 한 강력한 2FA 보호를 유지 하면서 신뢰할 수 없는 장치입니다. 정기적으로 사용 하는 모든 개인 장치에서이 수행할 수 있습니다.

이 자습서에서는 새 ASP.NET MVC 응용 프로그램에 2FA 활성화 간략 한 소개를 제공 합니다. 내 자습서 [SMS 및 전자 메일을 사용 하 여 ASP.NET Identity와 2 단계 인증](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) 세부 뒤에 있는 샘플 코드에 들어갑니다.

<a id="addRes"></a>
## <a name="additional-resources"></a>추가 자료

- [SMS 및 전자 메일을 사용 하 여 ASP.NET Identity와 2 단계 인증](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) 에 2 단계 인증에 자세히 나와
- [ASP.NET Id에 대 한 링크 권장 리소스](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [계정 확인 및 ASP.NET Id와 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 암호 복구 및 계정 확인에 대 한 자세한 내용으로 이어집니다.
- [Facebook, Twitter, LinkedIn 및 Google OAuth2 로그온 된 MVC 5 앱](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 이 자습서에서는 Facebook 및 Google OAuth 2 인증을 사용 하 여 ASP.NET MVC 5 앱을 작성 하는 방법을 보여 줍니다. 또한 Id 데이터베이스에 데이터를 추가 하는 방법을 보여 줍니다.
- [멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET MVC 응용 프로그램을 Azure 웹 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. 이 자습서에서는 Azure 배포 추가 역할을 사용 하 여 앱을 보호 하는 방법을 사용자 및 역할 및 추가 보안 기능을 추가할 구성원 API를 사용 하는 방법.
- [OAuth 2에 대 한 Google 앱 만들기 및 앱 프로젝트 연결](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [Facebook에서 앱을 만들기 및 앱 프로젝트에 연결](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [프로젝트에서 SSL을 설정합니다.](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
