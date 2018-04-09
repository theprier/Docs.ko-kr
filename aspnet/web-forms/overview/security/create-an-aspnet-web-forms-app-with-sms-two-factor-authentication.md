---
uid: web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
title: ASP.NET 웹 만들 SMS 2 단계 인증 (C#)와 Forms 응용 프로그램 | Microsoft Docs
author: Erikre
description: 이 자습서 2 단계 인증으로 ASP.NET Web Forms 응용 프로그램을 구축 하는 방법을 보여 줍니다. 이 자습서는 Cr 이라는 자습서를 보완 하기 위해 설계 되었습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/09/2014
ms.topic: article
ms.assetid: 716264ae-ab72-45de-bfc5-53a6237089cf
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: 6c040fd3e0592b8cfd230dcd85ed3293f0a22ba7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="create-an-aspnet-web-forms-app-with-sms-two-factor-authentication-c"></a>만들기는 ASP.NET Web Forms 응용 프로그램 SMS 2 단계 인증 (C#)
====================
으로 [Erik Reitan](https://github.com/Erikre)

[전자 메일 및 SMS 2 단계 인증을 통해 ASP.NET Web Forms 응용 프로그램 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-App-with-5a0ff94e)

> 이 자습서 2 단계 인증으로 ASP.NET Web Forms 응용 프로그램을 구축 하는 방법을 보여 줍니다. 이 자습서는 라는 제목의 자습서를 보완 하기 위해 설계 되었습니다 [사용자 등록 보안 ASP.NET Web Forms 응용 프로그램 만들기, 확인 및 암호 재설정 전자 메일](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)합니다. 또한이 자습서 기반 Rick Anderson의 [MVC 자습서](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)합니다.


## <a name="introduction"></a>소개

이 자습서에서는 Visual Studio를 사용 하 여 2 단계 인증을 지 원하는 ASP.NET Web Forms 응용 프로그램을 만드는 데 필요한 단계를 안내 합니다. 2 단계 인증에 추가 되는 사용자 인증 단계입니다. 이 추가 단계에는 로그인 시 고유한 개인 식별 번호 (PIN)를 생성합니다. PIN은 일반적으로 전자 메일 또는 SMS 메시지 사용자에 게 전송 됩니다. 응용 프로그램의 사용자 다음가 PIN을 입력 추가 인증 수단으로 때에 로그인입니다.

### <a name="tutorial-tasks-and-information"></a>자습서의 작업 및 정보:

- [ASP.NET Web Forms 응용 프로그램 만들기](#createWebForms)
- [SMS 및 2 단계 인증을 설정 합니다.](#SMS)
- [등록 된 사용자에 대 한 2 단계 인증을 사용 하도록 설정](#use2FA)
- [추가 리소스](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>ASP.NET Web Forms 응용 프로그램 만들기

설치 하 고 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다. 설치 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상도 합니다. 또한 만들 해야 합니다는 [Twilio](https://www.twilio.com/try-twilio) 계정 아래에 설명 된 대로 합니다.

> [!NOTE]
> 중요:를 설치 해야 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 하려면이 자습서를 완료 합니다.


1. 새 프로젝트를 만듭니다 (**파일**  - &gt; **새 프로젝트**)을 선택 하 고는 **ASP.NET 웹 응용 프로그램** .NET Framework와 함께 서식 파일 버전 4.5.2에서는 **새 프로젝트** 대화 상자.
2. **새 ASP.NET 프로젝트** 대화 상자는 **Web Forms** 템플릿. 기본 인증을 두고 **개별 사용자 계정**합니다. 클릭 **확인** 새 프로젝트를 만듭니다.  
    ![새 ASP.NET 프로젝트 대화 상자](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image1.png)
3. 프로젝트에 대 한 Secure Sockets Layer (SSL)를 사용 합니다. 사용할 수 있는 단계에 따라는 **프로젝트에 대 한 SSL을 사용 하도록 설정** 의 섹션은 [Web Forms 자습서 시리즈 시작](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)합니다.
4. Visual Studio에서 열고는 **패키지 관리자 콘솔** (**도구**  - &gt; **NuGet 패키지 관리자**  - &gt; **패키지 관리자 콘솔**), 다음 명령을 입력 합니다.  
    `Install-Package Twilio`

<a id="SMS"></a>
## <a name="setup-sms-and-two-factor-authentication"></a>SMS 및 2 단계 인증을 설정 합니다.

이 자습서에서는 Twilio를 사용 하지만 모든 SMS 공급자를 사용할 수 있습니다.

1. 만들기는 [Twilio](https://www.twilio.com/try-twilio) 계정.
2. **대시보드** 복사 Twilio 계정 탭의 **계정 SID** 및 **인증 토큰입니다.** 됩니다 추가한 응용 프로그램에 나중에 있습니다.
3. **숫자** 탭에서 프로그램 Twilio 복사 **전화 번호** 도 합니다.
4. Twilio 확인 **계정 SID**, **인증 토큰** 및 **전화 번호** 응용 프로그램에 사용할 수 있습니다. 간단 하 게 저장 하는 이러한 값에는 *web.config* 파일입니다. Azure에 배포 하는 경우에 안전 하 게 값을 저장할 수 있습니다는 **appSettings** 웹 사이트에서 섹션 구성 탭 합니다. 또한, 전화 번호를 추가할 때만 번호를 사용 합니다.   
   SendGrid 자격 증명도 추가할 수 있는지를 확인 합니다. SendGrid 전자 메일 알림 서비스입니다. SendGrid를 설정 하는 방법에 대 한 내용은 이라는 자습서의 ' 후크를 SendGrid' 섹션을 참조 [Secure ASP.NET Web Forms App 사용자 등록 만들기, 확인 및 암호 재설정 전자 메일입니다.](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)

    [!code-xml[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample1.xml?highlight=2,6-10)]

    > [!WARNING]
    > 보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다. 이 예제에서는 계정 및 자격 증명에 저장 됩니다는 **appSettings** 의 섹션은 *Web.config* 파일입니다. Azure에서 안전 하 게에 저장할 수 있습니다 이러한 값은 **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** Azure 포털에서 탭 합니다. 관련된 내용은 Rick Anderson의 항목을 참조 하세요. [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](https://go.microsoft.com/fwlink/?LinkId=513141)합니다.
5. 구성에서 `SmsService` 클래스에 *앱\_Start\IdentityConfig.cs* 다음 하 여 파일 변경 내용은 모두 노란색으로 강조 표시: 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample2.cs?highlight=5-17)]
6. 다음 추가 `using` 문을의 시작 부분에는 *IdentityConfig.cs* 파일: 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample3.cs?highlight=1-4)]
7. 업데이트는 *Account/Manage.aspx* 노란색으로 강조 표시 하는 줄을 제거 하 여 파일:  

    [!code-aspx[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample4.aspx?highlight=38,53,57-60,63,66,70,73)]
8. 에 `Page_Load` 의 처리기는 *Manage.aspx.cs* 코드 숨김, 주석으로 표시 되도록 노란색으로 강조 표시 하는 코드 줄 뒤에 오는 처리를 제거 합니다. 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample5.cs?highlight=8)]
9. 코드 숨김에서 *계정*/*TwoFactorAuthenticationSignIn.aspx.cs*, 업데이트 된 `Page_Load` 노란색으로 강조 표시 한 다음 코드를 추가 하 여 처리기: 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample6.cs?highlight=3-4,13)]

   위의 코드를 변경 함으로써 인증 옵션을 포함 하는 "공급자" DropDownList 첫 번째 값으로 재설정 하지 됩니다. 이렇게 하면 사용자가 성공적으로 첫 번째 뿐 아니라를 인증할 때 사용 하는 모든 옵션을 선택할 수 있습니다.
10. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *Default.aspx* 선택 **시작 페이지로 설정**합니다.
11. 앱을 테스트 하 여 앱을 빌드할 먼저 (**Ctrl**+**Shift**+**B**) 후 앱을 실행 하 고 (**F5**) 및 선택 하거나 **등록** 새 사용자 계정을 만들거나 선택 **로그인** 사용자 계정에 이미 등록 된 경우.
12. 표시 하려면 탐색 모음에서 사용자 ID (전자 메일 주소)를 클릭 (사용자)로 로그인 한 후,는 **계정 관리** 페이지 (Manage.aspx).  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image2.png)
13. 클릭 **추가** 옆에 **전화 번호** 에 **계정 관리** 페이지.  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image3.png)
14. (사용자)로 넣을 누르고 SMS (문자 메시지) 메시지를 받을 전화 번호 추가 **전송** 단추입니다.   
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image4.png)  
    응용 프로그램을에서 자격 증명을 사용 하는 시점에서 *Web.config* Twilio 연결할 합니다. SMS 메시지 (문자 메시지)는 사용자 계정과 연결 된 휴대폰에 전송 됩니다. Twilio 대시보드를 확인 하 여 Twilio 메시지를 보낸 것을 확인할 수 있습니다.
15. 몇 초 후에 사용자 계정과 연결 된 전화는 확인 코드를 포함 하는 텍스트 메시지를 받게 됩니다. 확인 코드 및 키를 눌러 입력 **전송**합니다.  
     ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image5.png)

<a id="use2FA"></a>
## <a name="enable-two-factor-authentication-for-a-registered-user"></a>등록 된 사용자에 대 한 2 단계 인증을 사용 하도록 설정

이 시점에서 앱에 대 한 2 단계 인증을 설정한 합니다. 2 단계 인증을 사용 하도록 사용자에 대 한 UI를 사용 하 여 해당 설정을 변경 하면 됩니다. 

1. 응용 프로그램의 사용자로 하면 2 단계 인증을 사용할 수 특정 계정에 대 한 사용자 ID (전자 메일 별칭)을 클릭 하 여 표시 하려면 탐색 모음에서는 **계정 관리** 페이지. 클릭 합니다는 **사용** 계정에 대해 2 단계 인증을 사용 하는 링크입니다.![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image6.png)
2. 로그 오프 한 다음 다시 로그인 합니다. 전자 메일을 설정한 경우 2 단계 인증에 대 한 전자 메일 또는 SMS를 선택할 수 있습니다. 전자 메일을 활성화 하지 않은 경우 이라는 자습서를 참조 하십시오. [Secure ASP.NET Web Forms App 사용자 등록, 전자 메일 확인 및 암호 재설정 만들](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)합니다.![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image7.png)
3. SMS 또는 전자 메일) (에서 코드를 입력할 수 있는 다단계 인증 페이지가 표시 됩니다.![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image8.png)  
 클릭 하 고 **저장이 브라우저** 확인란 있습니다 사용할 브라우저와 장치 상자를 선택한 경우 로그인에 2 단계 인증 사용을에서 제외 됩니다. 악의적인 사용자가 장치에 액세스할 수 없습니다, 2 단계 인증을 사용 하도록 설정 되 고를 클릭 하 고 **저장이 브라우저** 알려 편리 하 게 한 번 암호 액세스 강력한를 유지 하면서 신뢰할 수 없는 장치에서 모든 액세스에 대 한 2 단계 인증 보호 합니다. 정기적으로 사용 하는 모든 개인 장치에서이 수행할 수 있습니다.

<a id="addRes"></a>
## <a name="additional-resources"></a>추가 자료

- [ASP.NET ID와 SMS 및 전자 메일을 사용한 2단계 인증](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [ASP.NET Id에 대 한 링크 권장 리소스](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET Web Forms 응용 프로그램을 Azure 웹 사이트 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [ASP.NET Web Forms 자습서 시리즈-OAuth 2.0 공급자 추가](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [ASP.NET Web Forms 자습서 시리즈-프로젝트에 대 한 SSL 사용](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
- [계정 확인 및 ASP.NET Id와 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [Facebook에서 앱을 만들기 및 앱 프로젝트에 연결](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
