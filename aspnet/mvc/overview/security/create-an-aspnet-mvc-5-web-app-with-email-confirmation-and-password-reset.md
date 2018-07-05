---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: 전자 메일 확인 및 암호 재설정 기능이 (C#), 로그를 사용 하 여 보안 ASP.NET MVC 5 웹 앱 만들기 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 전자 메일 확인 및 ASP.NET Id 멤버 자격 시스템을 사용 하 여 암호를 사용 하 여 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다. Ca는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/26/2015
ms.topic: article
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 56c1a5c414fdcece8d827d1187144b4948d8eb93
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37387045"
---
<a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a>전자 메일 확인 및 암호 재설정 기능이 (C#), 로그를 사용 하 여 보안 ASP.NET MVC 5 웹 앱 만들기
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서에서는 전자 메일 확인 및 ASP.NET Id 멤버 자격 시스템을 사용 하 여 암호를 사용 하 여 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다. 완성된 된 응용 프로그램을 다운로드할 수 있습니다 [여기](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)합니다. 다운로드는 전자 메일 또는 SMS 공급자를 설정 하지 않고 SMS 및 전자 메일 확인을 테스트할 수 있도록 디버깅 도우미를 포함 합니다.
> 
> 이 자습서를 통해 작성 했습니다 [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) ).


<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>ASP.NET MVC 앱 만들기

설치 및 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 하거나 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다. 설치할 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상.

> [!NOTE]
> : 경고를 설치 해야 합니다 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상이 자습서를 완료 합니다.


1. 새 ASP.NET 웹 프로젝트를 만들고 MVC 템플릿을 선택 합니다. 또한 web Forms web forms 앱에서 비슷한 단계를 수행할 수 있도록 ASP.NET Id를 지원 합니다.  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. 기본 인증을 유지 **개별 사용자 계정**합니다. Azure에서 앱을 호스트 하려는 경우 확인란을 선택한 상태로 둡니다. 자습서의 뒷부분에 나오는 Azure에 배포 됩니다. 할 수 있습니다 [Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)합니다.
3. 설정 된 [SSL을 사용 하도록 프로젝트](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.
4. 앱 실행을 클릭 합니다 **등록** 에 연결 하 고 사용자를 등록 합니다. 이 시점에서 전자 메일에만 유효성 검사 된 합니다 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 특성입니다.
5. 서버 탐색기에서로 이동 **데이터 Connections\DefaultConnection\Tables\AspNetUsers**, 마우스 오른쪽 단추로 클릭 하 고 선택 **테이블 정의 열기**합니다.

    다음 이미지는 `AspNetUsers` 스키마:

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. 마우스 오른쪽 단추로 클릭 합니다 **AspNetUsers** 선택한 테이블 **테이블 데이터 표시**합니다.  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 이 시점에서 전자 메일 확인 되지 않았습니다.
7. 행을 클릭 하 고 삭제를 선택 합니다. 다음 단계에서는이 전자 메일을 다시 추가 하 고 확인 전자 메일을 보냅니다.

## <a name="email-confirmation"></a>전자 메일 확인

다른 사용자에 가장 하지 않는 것을 확인 하려면 새 사용자 등록 전자 메일을 확인 하는 것이 좋습니다 (즉, 다른 사용자의 전자 메일을 사용 하 여 등록 하지 않은). 방지 하려는 토론 포럼을 설치한 가정 `"bob@example.com"` 로 등록에서 `"joe@contoso.com"`합니다. 전자 메일 확인 하지 않고 `"joe@contoso.com"` 앱에서 원치 않는 전자 메일을 가져올 수 없습니다. Bob 실수로 등록 가정 `"bib@example.com"` 를 눈치채 및 그 앱에 올바른 전자 메일 없는 때문에 암호 복구를 사용할 수 있습니다. 전자 메일 확인은 봇부터에서만 제한 된 보호를 제공 하며 결정된 스패머가에서 보호를 제공 하지 않습니다, 그리고 여러 작업 전자 메일 별칭을 등록 하는 데 사용할 수 있는 합니다.

일반적으로 새 사용자가 전자 메일, SMS 문자 메시지 또는 다른 메커니즘을 통해 학인합니다 전에 웹 사이트에 데이터를 게시 하지 못하도록 좋습니다. <a id="build"></a>아래 섹션에서 전자 메일 확인을 사용 하도록 설정 하 고 새로 등록 된 사용자가 자신의 전자 메일 확인 될 때까지 로그인 하지 못하도록 하려면 코드를 수정 합니다.

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>SendGrid 연결

이 자습서에만 전자 메일 알림을 통해 추가 하는 방법을 보여 주지만 [SendGrid](http://sendgrid.com/), SMTP 및 다른 메커니즘을 사용 하 여 메일을 보낼 수 있습니다 (참조 [추가 리소스](#addRes)).

1. 패키지 관리자 콘솔에서 다음 명령을 입력 합니다. 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. 로 이동 합니다 [Azure SendGrid 등록 페이지](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) 무료 SendGrid 계정을 등록 합니다. 에 다음과 비슷한 코드를 추가 하 여 SendGrid 구성할 *App_Start/IdentityConfig.cs*:

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

다음 include 추가 해야 합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

간단히 유지 하기 위해이 샘플의 앱 설정을 저장 합니다 *web.config* 파일:

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> 보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다. 계정 및 자격 증명 appSetting에 저장 됩니다. Azure에서 안전 하 게에 저장할 수 있습니다 이러한 값을 **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** Azure portal에서 탭 합니다. 참조 [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.


### <a name="enable-email-confirmation-in-the-account-controller"></a>Account 컨트롤러의 전자 메일 확인을 사용 하도록 설정

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

확인 합니다 *Views\Account\ConfirmEmail.cshtml* 파일에 올바른 razor 구문입니다. (의 첫 번째에서 문자 @ 줄 누락 될 수 있습니다. )

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

앱을 실행 하 고 등록 링크를 클릭 합니다. 등록 양식을 제출 하면 로그인 됩니다.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

전자 메일 계정을 확인 하 고 전자 메일을 확인 하려면 링크를 클릭 합니다.

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>로그인 하기 전에 전자 메일 확인 필요

사용자 등록 양식을 완료 된 후에 현재으로 로그인 됩니다. 일반적으로 기록 하기 전에 전자 메일을 확인 하려고 합니다. 아래 섹션에서 새 사용자 기록 하기 전에 전자 메일을 확인된 하도록 (인증)를 요구 하도록 코드를 수정 하겠습니다. 업데이트 된 `HttpPost Register` 메서드를 다음 강조 표시 된 변경 내용으로:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

주석는 `SignInAsync` 메서드, 사용자를 등록 하 여 로그인 하지 됩니다. `TempData["ViewBagLink"] = callbackUrl;` 줄에 사용할 수 있습니다 [앱을 디버그할](#dbg) 및 전자 메일을 보내지 않고 등록을 테스트 합니다. `ViewBag.Message` 확인 지침을 표시 하는 데 사용 됩니다. 합니다 [샘플을 다운로드](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) 전자 메일을 설정 하지 않고 전자 메일 확인을 테스트 하는 코드를 포함 하 고 응용 프로그램 디버깅에 사용할 수도 있습니다.

만들기는 `Views\Shared\Info.cshtml` 파일과 다음 razor 태그를 추가 합니다.

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

추가 된 [Authorize 특성](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) 에 `Contact` Home 컨트롤러의 동작 메서드. 클릭할 수 있습니다 합니다 **연락처** 익명 사용자가 액세스할 수 없는 및 인증 된 사용자에 대 한 액세스 권한이 확인 하기 위한 링크입니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

업데이트 해야 합니다 `HttpPost Login` 작업 메서드:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

업데이트를 *Views\Shared\Error.cshtml* 오류 메시지를 표시 하려면 보기:

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

모든 계정을 삭제 합니다 **AspNetUsers** 테스트 하려는 전자 메일 별칭을 포함 하는 테이블입니다. 앱을 실행 하 고 전자 메일 주소 확인 될 때까지 로그인 할 수 없습니다 확인 합니다. 전자 메일 주소 확인을 클릭 합니다 **연락처** 링크 합니다.

<a id="reset"></a>
## <a name="password-recoveryreset"></a>암호 복구/재설정

주석 문자를 제거 합니다 `HttpPost ForgotPassword` account 컨트롤러의 동작 메서드:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

주석 문자를 제거 합니다 `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) 에 *Views\Account\Login.cshtml* razor 뷰 파일:

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

로그인 페이지가 암호 재설정에 대 한 링크가 표시 됩니다.

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>전자 메일 확인 링크 다시 보내기

사용자는 새 로컬 계정을 만들고 나면 로그온 하기 전에 사용 해야 하는 확인 링크를 전자 메일로 전송 되는 합니다. 사용자 실수로 삭제 확인 전자 메일 또는 전자 메일 절대 도착 하는 경우 확인 링크 다시 전송 해야 합니다. 코드 변경에는이 기능을 사용 하는 방법을 보여 줍니다.

맨 아래에 다음 도우미 메서드를 추가 합니다 *controllers\ accountcontroller.cs* 파일:

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

새 도우미를 사용 하도록 등록 메서드를 업데이트 합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

사용자 계정이 확인 되지 않았습니다 하는 경우 암호를 다시 보내려고 로그인 메서드를 업데이트 합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a>로컬 및 소셜 로그인 계정을 병합합니다

로컬 및 소셜 계정 전자 메일 링크를 클릭 하 여 결합할 수 있습니다. 다음 순서로 **RickAndMSFT@gmail.com** 로컬 로그인으로 처음 만들어질가 첫 번째는 소셜 로그인으로 계정을 만든 다음 로컬 로그인을 추가 하지만 합니다.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

클릭 합니다 **관리** 링크 합니다. 참고 합니다 **외부 로그인: 0** 이 계정과 사용 하 여 연결 합니다.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

서비스에서 다른 로그에 대 한 링크를 클릭 하 고 앱 요청을 수락 합니다. 두 개의 계정을 결합 되었습니다, 그리고 두 계정으로 로그온 할 수 있습니다. 사용자가 소셜 로그인 인증 서비스를 중단 되었거나 가능성이 소셜 계정에 대 한 액세스를 손실가 되는 경우 로컬 계정에 추가할 수 있습니다.

다음 그림과에서 Tom은 소셜 로그인 (에서 볼 수 있는 합니다 **외부 로그인: 1** 페이지에 표시).

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

클릭할 **암호 선택** 동일한 계정에 연결 된 로컬 로그에 추가할 수 있습니다.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a>좀 더 깊이 전자 메일 확인

내 자습서 [계정 확인 및 ASP.NET Id와 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 자세한 세부 정보를 사용 하 여이 항목을 살펴봅니다.

<a id="dbg"></a>
## <a name="debugging-the-app"></a>앱 디버깅

링크를 포함 하는 전자 메일을 얻지 못한 경우:

- 정크 또는 스팸 폴더를 확인 합니다.
- SendGrid 계정에 로그인 하 고 클릭 합니다 [전자 메일 작업 링크](https://sendgrid.com/logs/index)합니다.

전자 메일 주소가 없음 확인 링크를 테스트 하려면 다운로드 합니다 [완성 된 샘플](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)합니다. 확인 링크 및 확인 코드 페이지에 표시 됩니다.

<a id="addRes"></a>
## <a name="additional-resources"></a>추가 리소스

- [링크를 ASP.NET Id 권장 리소스](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [계정 확인 및 ASP.NET Id와 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 암호 복구 및 계정 확인에 대 한 자세한 내용으로 이어집니다.
- [Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on을 사용 하 여 MVC 5 앱](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 이 자습서에서는 Facebook 및 Google OAuth 2 권한 부여를 사용 하 여 ASP.NET MVC 5 앱을 작성 하는 방법을 보여 줍니다. 또한 Id 데이터베이스에 데이터를 추가 하는 방법을 보여 줍니다.
- [멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET MVC 앱을 Azure에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. 이 자습서는 Azure 배포 추가 역할을 사용 하 여 앱을 보호 하는 방법을 멤버 자격 API를 사용 하 여 사용자 및 역할 및 추가 보안 기능을 추가 하는 방법입니다.
- [OAuth 2 용 Google 앱 만들기 및 앱 프로젝트에 연결](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [Facebook에서 앱을 만들고 앱 프로젝트에 연결](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [프로젝트의 SSL 설정](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
