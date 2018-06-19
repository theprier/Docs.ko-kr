---
uid: web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
title: 확인 및 암호 재설정 (C#) 전자 메일 사용자 등록와 보안 ASP.NET Web Forms 응용 프로그램 만들기 | Microsoft Docs
author: Erikre
description: 이 자습서에서는 사용자 등록, 전자 메일 확인 및 암호 재설정 ASP.NET Identity 멤버를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 방법 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/02/2014
ms.topic: article
ms.assetid: 0a8d6044-5fab-4213-82d6-5618d5601358
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 1dc7ace69473b45432fd942b9cf1ba32332cb707
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30892701"
---
<a name="create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset-c"></a>확인 및 암호 재설정 (C#) 전자 메일 사용자 등록와 보안 ASP.NET Web Forms 응용 프로그램 만들기
====================
으로 [Erik Reitan](https://github.com/Erikre)

> 이 자습서에서는 사용자 등록, 전자 메일 확인 및 암호 재설정 ASP.NET Identity 멤버 자격 시스템을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 방법을 보여 줍니다. 이 자습서 Rick Anderson의 기반 [MVC 자습서](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)합니다.


## <a name="introduction"></a>소개

이 자습서에서는 Visual Studio 및 ASP.NET 4.5를 사용 하 여 사용자 등록 보안 Web Forms 응용 프로그램을 만들고, 확인 및 암호 재설정 전자 메일을 ASP.NET Web Forms 응용 프로그램을 만드는 데 필요한 단계를 안내 합니다.

### <a name="tutorial-tasks-and-information"></a>자습서의 작업 및 정보:

- [만들기는 ASP.NET Web Forms 응용 프로그램](#createWebForms)
- [SendGrid 후크](#SG)
- [로그인 하기 전에 전자 메일 확인 필요](#require)
- [암호 복구 및 다시 설정](#reset)
- [전자 메일 확인 링크를 다시 보냅니다.](#rsend)
- [응용 프로그램 문제 해결](#dbg)
- [추가 리소스](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>ASP.NET Web Forms 응용 프로그램 만들기

설치 하 고 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다. 설치 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상도 합니다.

> [!NOTE]
> 경고:를 설치 해야 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 하려면이 자습서를 완료 합니다.


1. 새 프로젝트를 만듭니다 (**파일**  - &gt; **새 프로젝트**)을 선택 하 고는 **ASP.NET 웹 응용 프로그램** 템플릿과 최신.NET Framework 버전은 **새 프로젝트** 대화 상자.
2. **새 ASP.NET 프로젝트** 대화 상자는 **Web Forms** 템플릿. 기본 인증을 두고 **개별 사용자 계정**합니다. Azure에서 응용 프로그램 호스트 하려는 경우에 둡니다는 **클라우드의 호스트에에서** 확인란을 선택 합니다.   
 클릭 **확인** 새 프로젝트를 만듭니다.  
    ![새 ASP.NET 프로젝트 대화 상자](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)
3. 프로젝트에 대 한 Secure Sockets Layer (SSL)를 사용 합니다. 사용할 수 있는 단계에 따라는 **프로젝트에 대 한 SSL을 사용 하도록 설정** 의 섹션은 [Web Forms 자습서 시리즈 시작](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)합니다.
4. 응용 프로그램 실행을 클릭는 **등록** 에 연결 하 고 새 사용자를 등록 합니다. 이 시점에서 전자 메일에만 유효성 검사는 기반는 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 특성을 전자 메일 주소 형식이 올바른지 확인 합니다. 전자 메일 확인을 추가 하는 코드를 수정 합니다. 브라우저 창을 닫습니다.
5. **서버 탐색기** 의 Visual Studio (**보기**  - &gt; **서버 탐색기**)로 이동 **데이터 Connections\ DefaultConnection\Tables\AspNetUsers**를 마우스 오른쪽 단추로 클릭 하 고 **테이블 정의 열고**합니다. 

    다음 그림에서는 `AspNetUsers` 테이블 스키마:

    ![AspNetUsers 테이블 스키마](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image2.png)
6. **서버 탐색기**를 마우스 오른쪽 단추로 클릭는 **AspNetUsers** 테이블을 선택한 **테이블 데이터 표시**합니다.  
  
    ![AspNetUsers 테이블 데이터](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image3.png)  
 이 시점에서 등록 된 사용자에 대 한 전자 메일 확인 되지 않았습니다.
7. 행을 삭제 하려면 삭제 선택 사용자를 클릭 합니다. 다음 단계에서이 전자 메일을 다시 추가 하 고 전자 메일 주소로 확인 메시지를 전송 합니다.

## <a name="email-confirmation"></a>전자 메일 확인

다른 사용자에 가장 하지 않는 것을 확인 하려면 새 사용자를 등록 하는 동안 전자 메일을 확인 하는 것이 좋습니다 (즉, 이러한 하지 않은 등록 된 다른 사용자의 전자 메일). 방지 하기 위해 원할 토론 포럼을 설치한 경우를 가정해 볼 `"bob@cpandl.com"` 등록에서 `"joe@contoso.com"`합니다. 전자 메일 확인 하지 않고 `"joe@contoso.com"` 원치 않는 전자 메일 앱에서 가져올 수 있습니다. 실수로 Bob로 등록 된 경우를 가정해 볼 `"bib@cpandl.com"` 를 발견 하지 않은 그 하는지 앱에 없는 올바른 전자 메일 때문에 암호 복구를 사용할 수 없게 됩니다. 전자 메일 확인 bot에서만 제한 된 보호를 제공 하 고 결정된 된 스팸에서 보호를 제공 하지 않습니다.

일반적으로 새 사용자 메일, SMS 문자 메시지 또는 기타 메커니즘으로 확인 하기 전에 웹 사이트에 데이터를 게시 하는 것을 방지 하려고 합니다. 아래 섹션에 전자 메일 확인을 사용 하도록 설정 하 고 새로 등록 된 사용자가 전자 메일 확인 될 때까지에 로그인 하지 못하도록 방지 하기 위해 코드를 수정 합니다. 이 자습서에서는 SendGrid에서 전자 메일 서비스를 사용 합니다.

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>SendGrid 후크

이 자습서에서는 통해 전자 메일 알림을 추가 하는 방법을 보여 줍니다. 하지만 [SendGrid](http://sendgrid.com/), SMTP 및 다른 메커니즘을 사용 하 여 메일을 보낼 수 있습니다 (참조 [추가 리소스](#addRes)).

1. Visual Studio에서 열고는 **패키지 관리자 콘솔** (**도구**  - &gt; **NuGet 패키지 관리자**  - &gt; **패키지 관리자 콘솔**), 다음 명령을 입력 합니다.  
    `Install-Package SendGrid`
2. 이동 하는 [Azure SendGrid 등록 페이지](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) 무료로 SendGrid 계정을 등록 하 고 있습니다. 또한에서 직접 무료 SendGrid 계정을 등록 하면 [SendGrid의 사이트](http://www.sendgrid.com)합니다.
3. **솔루션 탐색기** 열고는 *IdentityConfig.cs* 파일에 *앱\_시작* 폴더는 에노란색으로강조표시한다음코드를추가하고`EmailService` 구성 하는 클래스 **SendGrid**:

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample1.cs?highlight=3,5,8-37)]
4. 또한 다음 추가 `using` 문을의 시작 부분에는 *IdentityConfig.cs* 파일: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample2.cs?highlight=1-4)]
5. 이 예제를 단순하게 유지 하기 위해에 전자 메일 서비스 계정의 값을 저장 합니다는 `appSettings` 의 섹션은 *web.config* 파일입니다. 노란색으로 강조 표시 하는 다음 XML 추가 *web.config* 프로젝트의 루트에 파일:

    [!code-xml[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample3.xml?highlight=2-5)]

    > [!WARNING]
    > 보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다. 이 예제에서는 계정 및 자격 증명에 저장 됩니다는 **appSetting** 의 섹션은 *Web.config* 파일입니다. Azure에서 안전 하 게에 저장할 수 있습니다 이러한 값은 **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** Azure 포털에서 탭 합니다. 관련된 내용은 Rick Anderson의 항목을 참조 하세요. [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](https://go.microsoft.com/fwlink/?LinkId=513141)합니다.
6. SendGrid 인증 값 (사용자 이름 및 암호) 성공적으로 수행할 수 있도록 보낼 전자 메일 앱에서 반영 하기 위해 전자 메일 서비스 값을 추가 합니다. SendGrid를 입력 한 전자 메일 주소 보다는 SendGrid 계정 이름을 사용 해야 합니다.

### <a name="enable-email-confirmation"></a>전자 메일 확인을 사용 하도록 설정

 전자 메일 확인을 사용 하려면 다음 단계를 사용 하 여 등록 코드를 수정 합니다.  
 

1. 에 *계정* 폴더를 엽니다는 *Register.aspx.cs* 코드 숨김 및 업데이트는 `CreateUser_Click` 다음 강조 표시 된 변경할 수 있도록 메서드: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample4.cs?highlight=9-11)]
2. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *Default.aspx* 선택 **시작 페이지로 설정**합니다.
3. 키를 눌러 앱을 실행 **F5 합니다.** 페이지 표시 되 면 클릭는 **등록** 링크 레지스터 페이지를 표시 합니다.
4. 전자 메일 및 암호를 입력 한 다음 클릭는 **등록** 단추 SendGrid 통해 전자 메일 메시지를 보내도록 합니다.  
   프로젝트 및 코드의 현재 상태에는 사용자 계정으로를 확인 하지 않은 경우에 등록 양식을 완료 되 면에 로그인 할 수 있게 됩니다.
5. 전자 메일 계정을 확인 하 고 사용자의 전자 메일을 확인 하려면 다음 링크를 클릭 합니다.  
   등록 양식을 전송 하면에 기록 됩니다.  
    ![샘플 웹 사이트-로그인](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image4.png)

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>로그인 하기 전에 전자 메일 확인 필요

전자 메일 계정 확인 하지만 시점에서 하지 해야에 완전히 서명 확인 전자 메일에 포함 된 링크를 클릭 합니다. 다음 섹션에 새 사용자가을 기록 하기 전에 확인 된 전자 메일을 가질 (인증)를 요구 하는 코드를 수정 합니다.

1. **솔루션 탐색기** Visual Studio의 업데이트는 `CreateUser_Click` 이벤트에는 *Register.aspx.cs* 코드 숨김에 포함 된는 *계정* 폴더는 다음 강조 표시 된 변경 내용: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample5.cs?highlight=13-14,17-21)]
2. 업데이트는 `LogIn` 에서 메서드는 *Login.aspx.cs* 다음 강조 표시 된 변경 내용으로 코드 숨김: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample6.cs?highlight=9-19,45-46)]

### <a name="run-the-application"></a>응용 프로그램 실행

 사용자의 전자 메일 주소 확인 했는지를 확인 하는 코드를 구현한 했으므로 둘 다에서 기능을 확인할 수 있습니다는 **등록** 및 **로그인** 페이지입니다. 

1. 모든 계정을 삭제는 **AspNetUsers** 테스트 하려는 전자 메일 별칭을 포함 하는 테이블입니다.
2. 응용 프로그램을 실행 (**F5**) 하 고 확인 전자 메일 주소를 확인 한 될 때까지 사용자로 등록할 수 없습니다.
3. 방금 전송 된 전자 메일을 통해 사용자는 새 계정을 결정 하기 전에 새 계정으로 로그인 하려고 합니다.  
 로그인 할 수 없는 및 확인 된 전자 메일 계정을 보유 해야 하는지 확인할 수 있습니다.
4. 전자 메일 주소를 확인 하 고 나면 응용 프로그램에에 로그인 합니다.

<a id="reset"></a>
## <a name="password-recovery-and-reset"></a>암호 복구 및 다시 설정

1. Visual Studio에서 주석 문자를 제거는 `Forgot` 에서 메서드는 *Forgot.aspx.cs* 에 포함 된 코드 숨김의 *계정* 폴더 메서드가으로 나타나도록 따릅니다: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample7.cs?highlight=16-18)]
2. 열기는 *Login.aspx* 페이지. 대체의 끝 부분에서 태그는 **loginForm** 아래의 강조 표시 된 대로 섹션: 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample8.aspx?highlight=52-53)]
3. 열기는 *Login.aspx.cs* 코드 숨김 및에서 노란색으로 강조 표시 하는 코드의 다음 줄을 주석 처리 제거는 `Page_Load` 이벤트 처리기. 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample9.cs?highlight=5)]
4. 키를 눌러 앱을 실행 **F5 합니다.** 페이지 표시 되 면 클릭는 **로그인** 링크 합니다.
5. 클릭는 **암호를 잊으셨습니까?** 표시 하려면 링크는 **암호를 잊으셨습니까** 페이지.
6. 전자 메일 주소를 입력 하 고 클릭는 **전송** 암호를 다시 설정할 수 있는 주소로 전자 메일을 보내는 단추입니다.   
   전자 메일 계정을 확인 하 고 표시 하려면 링크를 클릭는 **암호 재설정** 페이지.
7. 에 **암호 재설정** 페이지에서 전자 메일, 암호 및 확인된 암호를 입력 합니다. 그런 다음 눌러는 **재설정** 단추입니다.  
   암호를 재설정할 때는 **암호가 변경** 페이지가 표시 됩니다. 이제 새 암호를 사용 하 여 기록할 수 있습니다.

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>전자 메일 확인 링크를 다시 보냅니다.

사용자는 새 로컬 계정을 만들고 나면은 로그온 할 수 전에 사용 하는 데 필요 확인 링크를 전자 메일로 전송 되 있습니다. 실수로 삭제 확인 전자 메일 또는 전자 메일이 도착 하지 확인 링크 다시 전송 해야 합니다. 다음 코드 변경 내용에는이 기능을 사용 하는 방법을 보여 줍니다.

1. Visual Studio에서 열고는 **Login.aspx.cs** 후 다음 이벤트 처리기를 추가 하 고 코드 숨김의 `LogIn` 이벤트 처리기:   

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample10.cs)]
2. 수정 된 `LogIn` 의 이벤트 처리기는 *Login.aspx.cs* 코드 숨김 다음과 같이 노란색으로 강조 표시 하는 코드를 변경 하 여: 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample11.cs?highlight=15-17)]
3. 업데이트는 *Login.aspx* 다음과 같이 노란색으로 강조 표시 하는 코드를 추가 하 여 페이지: 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample12.aspx?highlight=45-46)]
4. 모든 계정을 삭제는 **AspNetUsers** 테스트 하려는 전자 메일 별칭을 포함 하는 테이블입니다.
5. 응용 프로그램을 실행 (**F5**) 하 고 전자 메일 주소를 등록 합니다.
6. 방금 전송 된 전자 메일을 통해 사용자는 새 계정을 결정 하기 전에 새 계정으로 로그인 하려고 합니다.  
   로그인 할 수 없는 및 확인 된 전자 메일 계정을 보유 해야 하는지 확인할 수 있습니다. 또한 이제 다시 보낼 수 있습니다 확인 메시지를 전자 메일에 있습니다.
7. 전자 메일 주소와 암호를 입력 누릅니다는 **확인을 다시 보낼** 단추입니다.
8. 새로 보낸된 전자 메일 메시지에 기반한 전자 메일 주소를 확인 하 고 나면 앱에 로그인 합니다.

<a id="dbg"></a>
## <a name="troubleshooting-the-app"></a>응용 프로그램 문제 해결

자격 증명을 확인에 대 한 링크를 포함 된 메일을 수신 하지 않습니다.

- 정크 또는 스팸 폴더를 확인 합니다.
- SendGrid 계정에 로그인 하 고 클릭는 [전자 메일 작업 링크](https://sendgrid.com/logs/index)합니다.
- SendGrid 사용자 계정 이름으로 사용할 수는 *Web.config* SendGrid 계정 전자 메일 주소 대신 값입니다.

<a id="addRes"></a>
## <a name="additional-resources"></a>추가 자료

- [ASP.NET Id에 대 한 링크 권장 리소스](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [계정 확인 및 ASP.NET Id와 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET Web Forms 자습서 시리즈-OAuth 2.0 공급자 추가](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [Azure 앱 서비스에 멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET Web Forms 응용 프로그램 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [ASP.NET Web Forms 자습서 시리즈-프로젝트에 대 한 SSL 사용](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
