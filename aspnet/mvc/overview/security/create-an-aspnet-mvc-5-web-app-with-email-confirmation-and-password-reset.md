---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: 확인 및 암호 재설정 (C#) 전자 메일을 로그와 함께 보안 ASP.NET MVC 5 웹 앱 만들기 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 전자 메일 확인 및 암호 재설정 ASP.NET Identity 멤버 자격 시스템을 사용 하 여 ASP.NET MVC 5 웹 응용 프로그램을 구축 하는 방법을 보여 줍니다. Ca 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/26/2015
ms.topic: article
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: bfa5d52019be81374c7a544e255ab7ffb301fa7b
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "34452570"
---
<a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a>확인 및 암호 재설정 (C#) 전자 메일을 로그와 함께 보안 ASP.NET MVC 5 웹 앱 만들기
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서에서는 전자 메일 확인 및 암호 재설정 ASP.NET Identity 멤버 자격 시스템을 사용 하 여 ASP.NET MVC 5 웹 응용 프로그램을 구축 하는 방법을 보여 줍니다. 완성 된 응용 프로그램을 다운로드할 수 있습니다 [여기](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)합니다. 다운로드는 전자 메일 또는 SMS 공급자를 설정 하지 않고 전자 메일 확인 및 SMS를 테스트할 수 있도록 하는 디버깅 도우미를 포함 합니다.
> 
> 이 자습서에 의해 작성 되었으므로 [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) ).


<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>ASP.NET MVC 응용 프로그램 만들기

설치 하 고 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다. 설치 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상.

> [!NOTE]
> 경고:를 설치 해야 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 하려면이 자습서를 완료 합니다.


1. 새 ASP.NET 웹 프로젝트를 만들고 MVC 템플릿을 선택 합니다. Web Forms web forms 응용 프로그램에서 비슷한 단계를 반영할 수 있도록 ASP.NET Id를도 지원 합니다.  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. 기본 인증을 두고 **개별 사용자 계정**합니다. Azure에서 응용 프로그램 호스트 하려는 경우 확인란을 선택한 상태로 둡니다. 이 자습서의 뒷부분에 나오는에서는 Azure에 배포 합니다. 있습니다 수 [무료로 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)합니다.
3. 설정의 [SSL을 사용 하도록 프로젝트](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.
4. 응용 프로그램 실행을 클릭는 **등록** 에 연결 하 고 사용자를 등록 합니다. 전자 메일에만 유효성 검사와는 시점에서 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 특성입니다.
5. 서버 탐색기에서로 이동 **데이터 Connections\DefaultConnection\Tables\AspNetUsers**를 마우스 오른쪽 단추로 클릭 하 고 **테이블 정의 열고**합니다.

    다음 그림에서는 `AspNetUsers` 스키마:

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. 마우스 오른쪽 단추로 클릭는 **AspNetUsers** 테이블을 선택한 **테이블 데이터 표시**합니다.  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 이 시점에서 전자 메일 확인 되지 않았습니다.
7. 행을 클릭 하 고 삭제를 선택 합니다. 다음 단계에서이 전자 메일을 다시 추가 하 고 확인 전자 메일을 보냅니다.

## <a name="email-confirmation"></a>전자 메일 확인

다른 사용자에 가장 하지 않는 것을 확인 하려면 새 사용자 등록의 전자 메일을 확인 하는 것이 좋습니다 (즉, 이러한 하지 않은 등록 된 다른 사용자의 전자 메일). 방지 하기 위해 원할 토론 포럼을 설치한 경우를 가정해 볼 `"bob@example.com"` 등록에서 `"joe@contoso.com"`합니다. 전자 메일 확인 하지 않고 `"joe@contoso.com"` 원치 않는 전자 메일 앱에서 가져올 수 있습니다. 실수로 Bob로 등록 된 경우를 가정해 볼 `"bib@example.com"` 를 발견 하지 않은 그 하는지 앱에 없는 올바른 전자 메일 때문에 암호 복구를 사용할 수 없게 됩니다. 전자 메일 확인 bot에서 제한 된 보호만을 제공 하 고 결정된 된 스팸에서 보호를 제공 하지 않습니다, 그리고 등록 하는 데 사용할 수는 많은 작업 전자 메일 별칭을가지고 있습니다.

일반적으로 새 사용자 전자 메일, SMS 문자 메시지 또는 기타 메커니즘 확인 하기 전에 모든 데이터 웹 사이트를 게시 하는 것을 방지 하려고 합니다. <a id="build"></a>아래 섹션에 전자 메일 확인을 사용 하도록 설정 하 고 새로 등록 된 사용자가 전자 메일 확인 될 때까지에 로그인 하지 못하도록 방지 하기 위해 코드를 수정 합니다.

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>SendGrid 후크

이 자습서에서는 통해 전자 메일 알림을 추가 하는 방법을 보여 줍니다. 하지만 [SendGrid](http://sendgrid.com/), SMTP 및 다른 메커니즘을 사용 하 여 메일을 보낼 수 있습니다 (참조 [추가 리소스](#addRes)).

1. 패키지 관리자 콘솔에서 다음 명령을 입력 합니다. 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. 이동 하는 [Azure SendGrid 등록 페이지](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) 무료 SendGrid 계정을 등록 합니다. 다음과 비슷한 코드를 추가 하 여 SendGrid 구성 *App_Start/IdentityConfig.cs*:

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

다음을 추가 해야 합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

이 예제를 단순하게 유지 하기 위해 응용 프로그램 설정에 저장할 것은 *web.config* 파일:

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> 보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다. 계정 및 자격 증명 appSetting에 저장 됩니다. Azure에서 안전 하 게에 저장할 수 있습니다 이러한 값은 **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** Azure 포털에서 탭 합니다. 참조 [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.


### <a name="enable-email-confirmation-in-the-account-controller"></a>계정 컨트롤러에서 전자 메일 확인을 사용 하도록 설정

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

확인 된 *Views\Account\ConfirmEmail.cshtml* 파일에 올바른 razor 구문입니다. (의 @ 첫 번째 범위에서 문자 줄 누락 될 수 있습니다. )

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

응용 프로그램을 실행 하 고 등록 링크를 클릭 합니다. 등록 양식을 전송 하면에 기록 됩니다.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

전자 메일 계정을 확인 하 고 사용자의 전자 메일을 확인 하려면 다음 링크를 클릭 합니다.

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>로그인 하기 전에 전자 메일 확인 필요

사용자는 등록 양식에 나와 완료 되 고 나면 현재으로 로그인 됩니다. 일반적으로 자신의 전자 메일 기록 하기 전에 확인 하려고 합니다. 아래 섹션에서는 새 사용자가 기록 하기 전에 확인 된 전자 메일을 가질 (인증) 코드를 수정 합니다. 업데이트는 `HttpPost Register` 다음 표시 된 변경 내용 사용 하 여 메서드:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

주석으로 처리 하는 여는 `SignInAsync` 메서드를 사용자 등록 하 여 로그인 하지 됩니다. `TempData["ViewBagLink"] = callbackUrl;` 줄에 사용할 수 있습니다 [응용 프로그램을 디버깅](#dbg) 및 전자 메일을 보내지 않고 등록을 테스트 합니다. `ViewBag.Message` 확인 지침을 표시 하는 데 사용 됩니다. [샘플 다운로드](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) 전자 메일을 설정 하지 않고 전자 메일 확인을 테스트 하는 코드가 포함 되어 있으며 응용 프로그램 디버깅을 사용할 수도 있습니다.

만들기는 `Views\Shared\Info.cshtml` 파일을 다음 razor 태그를 추가 합니다.

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

추가 [Authorize 특성](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) 에 `Contact` Home 컨트롤러의 동작 메서드. 클릭할 수는 **연락처** 익명 사용자가 액세스할 수 없는 및 인증 된 사용자가 액세스할 수 있는 권한이 확인 합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

업데이트 해야는 `HttpPost Login` 동작 메서드:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

업데이트는 *Views\Shared\Error.cshtml* 오류 메시지를 표시 하려면 보기:

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

모든 계정을 삭제는 **AspNetUsers** 와 테스트 하려는 전자 메일 별칭을 포함 하는 테이블입니다. 응용 프로그램을 실행 하 고 로그인 할 수 없는 전자 메일 주소를 확인 한 될 때까지 확인 합니다. 전자 메일 주소를 확인 하 고 나면 클릭는 **연락처** 링크 합니다.

<a id="reset"></a>
## <a name="password-recoveryreset"></a>암호 복구/다시 설정

주석 문자를 제거는 `HttpPost ForgotPassword` 계정 컨트롤러에서 동작 메서드:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

주석 문자를 제거는 `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) 에 *Views\Account\Login.cshtml* razor 파일 보기:

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

로그인 페이지에서 암호를 다시 설정에 대 한 링크를 표시 이제 됩니다.

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>전자 메일 확인 링크를 다시 보냅니다.

사용자는 새 로컬 계정을 만들고 나면은 로그온 할 수 전에 사용 하는 데 필요 확인 링크를 전자 메일로 전송 되 있습니다. 실수로 삭제 확인 전자 메일 또는 전자 메일이 도착 하지 확인 링크 다시 전송 해야 합니다. 다음 코드 변경 내용에는이 기능을 사용 하는 방법을 보여 줍니다.

맨 아래에 다음 도우미 메서드를 추가 합니다.는 *Controllers\AccountController.cs* 파일:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

새 도우미를 사용 하도록 Register 메서드를 업데이트 합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

사용자 계정을 확인 되지 경우 암호를 다시 보내도록 로그인 메서드를 업데이트 합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a>공유 및 로컬 로그인 계정을 결합합니다

사용자 전자 메일 링크를 클릭 하 여 로컬 및 소셜 계정을 결합할 수 있습니다. 다음 순서로 **RickAndMSFT@gmail.com** 처음에 로컬 로그인으로 만들면 하지만 로컬 로그인을 추가 다음에서 첫 번째로, 소셜 로그로 계정을 만들 수 있습니다.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

클릭는 **관리** 링크 합니다. 참고는 **외부 로그인: 0** 이 계정과 연결 된 합니다.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

서비스에서 다른 로그에 대 한 링크를 클릭 하 고 응용 프로그램 요청을 수락 합니다. 두 개의 계정을 결합 되어, 두 계정으로 로그온 할 수 있습니다. 경우에 대비 다운 되는 인증 서비스에서 소셜의 로그 또는 쓰지만 대개은 स ॅ स 소셜 계정으로 로컬 계정을 추가 하려면 사용자가 할 수 있습니다.

다음 그림에서는 Tom는 소셜 로그인 (에서 볼 수 있는 **외부 로그인: 1** 페이지에 표시).

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

클릭 하면 **암호** 동일한 계정에 연결 된 로컬 로그에 추가할 수 있습니다.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a>좀 더 깊이 전자 메일 확인

내 자습서 [계정 확인 및 ASP.NET Id와 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 자세한 정보와 함께이 항목으로 이동 합니다.

<a id="dbg"></a>
## <a name="debugging-the-app"></a>응용 프로그램 디버깅

링크가 포함 된 전자 메일 얻지 못한 경우:

- 정크 또는 스팸 폴더를 확인 합니다.
- SendGrid 계정에 로그인 하 고 클릭는 [전자 메일 작업 링크](https://sendgrid.com/logs/index)합니다.

전자 메일 하지 않고 확인 링크를 테스트 하려면 다운로드는 [완성 된 샘플](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)합니다. 확인 링크 및 확인 코드 페이지에 표시 됩니다.

<a id="addRes"></a>
## <a name="additional-resources"></a>추가 리소스

- [ASP.NET Id에 대 한 링크 권장 리소스](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [계정 확인 및 ASP.NET Id와 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 암호 복구 및 계정 확인에 대 한 자세한 내용으로 이어집니다.
- [Facebook, Twitter, LinkedIn 및 Google OAuth2 로그온 된 MVC 5 앱](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 이 자습서에서는 Facebook 및 Google OAuth 2 인증을 사용 하 여 ASP.NET MVC 5 앱을 작성 하는 방법을 보여 줍니다. 또한 Id 데이터베이스에 데이터를 추가 하는 방법을 보여 줍니다.
- [멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET MVC 응용 프로그램을 Azure에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. 이 자습서에서는 Azure 배포 추가 역할을 사용 하 여 앱을 보호 하는 방법을 사용자 및 역할 및 추가 보안 기능을 추가할 구성원 API를 사용 하는 방법.
- [OAuth 2에 대 한 Google 앱 만들기 및 앱 프로젝트 연결](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [Facebook에서 앱을 만들기 및 앱 프로젝트에 연결](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [프로젝트에서 SSL을 설정합니다.](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
