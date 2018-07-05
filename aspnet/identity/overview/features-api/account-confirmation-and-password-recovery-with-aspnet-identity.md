---
uid: identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
title: 계정 확인 및 암호 복구 ASP.NET id (C#) | Microsoft Docs
author: HaoK
description: 먼저 완료 해야 하는이 자습서를 수행 하기 전에 로그인, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET MVC 5 웹 앱을 만듭니다. 이 자습서는 중...
ms.author: aspnetcontent
ms.date: 03/26/2015
ms.assetid: 8d54180d-f826-4df7-b503-7debf5ed9fb3
msc.legacyurl: /identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 08a954f8fab4a92b84bd79b4f644bcc1f55b1bc6
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37831085"
---
<a name="account-confirmation-and-password-recovery-with-aspnet-identity-c"></a>계정 확인 및 ASP.NET Id (C#)를 사용 하 여 암호 복구
====================
하 여 [Hao 둘러싼](https://github.com/HaoK)를 [Pranav Rastogi](https://github.com/rustd)하십시오 [Rick Anderson](https://github.com/Rick-Anderson), [Suhas Joshi](https://github.com/suhasj)

> 이 자습서를 수행 하기 전에 먼저를 완료 해야 [로그인, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET MVC 5 웹 앱을 만들기](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)합니다. 이 자습서는 자세한 세부 정보를 포함 하 고 로컬 계정 확인에 대 한 전자 메일을 설정 하 고 ASP.NET Id에서 잊어버린된 암호를 재설정할 수 있도록 하는 방법을 표시 됩니다. Rick anderson이 문서가 작성 된 ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), Hao 둘러싼 및 Suhas Joshi 합니다. NuGet 샘플 Hao 둘러싼 기본적 작성 되었습니다.


로컬 사용자 계정을 사용자 계정에 대 한 암호를 만들기 위해 필요 하 고 암호는 웹 앱에서 (안전 하 게) 저장 됩니다. ASP.NET Id는 소셜 계정 사용자가 앱에 대 한 암호를 만들도록 하려면 필요 없이 지원 합니다. [소셜 계정](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 를 제 3 자 (예: Google, Twitter, Facebook 또는 Microsoft)를 사용 하 여 사용자를 인증 합니다. 이 항목에서는 다음 다룹니다.

- [ASP.NET MVC 앱을 만들고](#createMvc) 및 ASP.NET Id 기능을 탐색 합니다.
- [Identity 샘플 빌드](#build)
- [전자 메일 확인 설정](#email)

새 사용자는 로컬 계정을 만들고 해당 전자 메일 별칭을 등록 합니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image1.png)

등록 단추를 클릭 하면 해당 전자 메일 주소에는 유효성 검사 토큰이 포함 된 확인 전자 메일을 보냅니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image2.png)

사용자 계정에 대 한 확인 토큰을 사용 하 여 전자 메일이 전송 됩니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image3.png)

계정을 확인 링크를 클릭 합니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image4.png)

<a id="passwordReset"></a>

## <a name="password-recoveryreset"></a>암호 복구/재설정

로컬 사용자가 암호를 잊은 암호를 재설정할 수 있도록 해당 전자 메일 계정으로 전송 하는 보안 토큰에 게 있습니다.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image5.png)  
  
곧 사용자 암호를 재설정할 수 있도록 링크가 포함 된 전자 메일을 받게 됩니다.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image6.png)  
링크를 클릭 하면 재설정 페이지로 이동 됩니다.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image7.png)  
  
클릭 하 여 **다시 설정** 단추는 암호가 재설정 되었습니다. 확인 됩니다.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image8.png)

<a id="createMvc"></a>

## <a name="create-an-aspnet-web-app"></a>ASP.NET 웹 앱 만들기

설치 및 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 하거나 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다. Visual Studio를 설치 [2013 업데이트 2](https://go.microsoft.com/fwlink/?LinkId=390521) 이상.

> [!NOTE]
> 경고: Visual Studio를 설치 해야 [2013 업데이트 2](https://go.microsoft.com/fwlink/?LinkId=390521) 이 자습서를 완료 합니다.


1. 새 ASP.NET 웹 프로젝트를 만들고 MVC 템플릿을 선택 합니다. 또한 web Forms web forms 앱에서 비슷한 단계를 수행할 수 있도록 ASP.NET Id를 지원 합니다.
2. 기본 인증을 유지 **개별 사용자 계정**합니다.
3. 앱 실행을 클릭 합니다 **등록** 에 연결 하 고 사용자를 등록 합니다. 이 시점에서 전자 메일에만 유효성 검사 된 합니다 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 특성입니다.
4. 서버 탐색기에서로 이동 **데이터 Connections\DefaultConnection\Tables\AspNetUsers**, 마우스 오른쪽 단추로 클릭 하 고 선택 **테이블 정의 열기**합니다.

    다음 이미지는 `AspNetUsers` 스키마:

    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image9.png)
5. 마우스 오른쪽 단추로 클릭 합니다 **AspNetUsers** 선택한 테이블 **테이블 데이터 표시**합니다.  
  
    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image10.png)  
  
   이 시점에서 전자 메일 확인 되지 않았습니다.

ASP.NET Id에 대 한 기본 데이터 저장소는 Entity Framework, 하지만 다른 데이터 저장소를 사용 하 고 추가 필드를 추가 하 고 구성할 수 있습니다. 참조 [레퍼런스](#addRes) 이 자습서의 끝에 있는 섹션입니다.

합니다 [OWIN startup 클래스](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) ( *Startup.cs* ) 앱 시작 및 호출 될 때 호출 되는 `ConfigureAuth` 에서 메서드 *앱\_Start\Startup.Auth.cs*, OWIN 파이프라인을 구성 하 고 ASP.NET Id를 초기화 합니다. `ConfigureAuth` 메서드를 검사합니다. 각 `CreatePerOwinContext` 호출 콜백을 등록 (에 저장 된 `OwinContext`) 지정 된 형식의 인스턴스를 만드는 요청당 한 번 호출 될 합니다. 생성자에 중단점을 설정할 수 있습니다 및 `Create` 형식별 메서드 (`ApplicationDbContext, ApplicationUserManager`) 하 고 각 요청에서 호출 될 확인 합니다. 인스턴스를 `ApplicationDbContext` 고 `ApplicationUserManager` 응용 프로그램에 걸쳐 액세스할 수 있는 OWIN 컨텍스트에서 저장 됩니다. ASP.NET Id는 쿠키 미들웨어를 통해 OWIN 파이프라인에 연결 합니다. 자세한 내용은 [UserManager 클래스 ASP.NET Id에 대 한 요청 수명 관리 당](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)합니다.

새 보안 스탬프를 보안 프로필을 변경 하면 생성 되 고 저장 합니다 `SecurityStamp` 필드를 *AspNetUsers* 테이블입니다. 에 `SecurityStamp` 필드 보안 쿠키와에서 다릅니다. 보안 쿠키에 저장 되어 있지는 `AspNetUsers` 테이블 (또는 Identity DB의 다른 곳). 보안 쿠키 토큰을 사용 하 여 자체 서명 됩니다 [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) 으로 생성 됩니다는 `UserId, SecurityStamp` 및 만료 시간 정보입니다.

쿠키 미들웨어는 각 요청에 쿠키를 확인 합니다. `SecurityStampValidator` 의 메서드를 `Startup` 클래스는 DB에 도달 하 고 보안 스탬프를 주기적으로 확인 지정 된 대로 `validateInterval`합니다. 이 보안 프로필을 변경 하지 않는 한 (샘플)에서 30 분 마다만 발생 합니다. 데이터베이스에 대 한 왕복을 최소화 하기 위해 30 분 간격을 선택 했습니다. 참조 내 [2 단계 인증 자습서](index.md) 대 한 자세한 내용은 합니다.

코드의 주석을 당는 `UseCookieAuthentication` 메서드 쿠키 인증을 지원 합니다. `SecurityStamp` 추가 계층을 제공 하는 필드 및 관련 된 코드를 앱에 보안, 암호를 변경 하면 로그인 됩니다에 로그인 할 때 브라우저에서. `SecurityStampValidator.OnValidateIdentity` 메서드를 사용 하면 암호를 변경 하거나 외부 로그인을 사용 하는 경우 사용 되는 앱을 사용자가 로그인 할 때 보안 토큰의 유효성을 검사 합니다. 이 이전 암호를 사용 하 여 생성 된 모든 토큰 (쿠키)를 무효화를 확인 해야 합니다. 샘플 프로젝트에서 변경 하는 경우 사용자에 대 한 사용자의 암호가 다음 새 토큰 생성 됩니다, 모든 이전 토큰이 유효 하지 않습니다 및 `SecurityStamp` 필드가 업데이트 됩니다.

Id 시스템 허용 앱을 구성할 수 있으므로 사용자 보안 프로필 변경 될 때 (사용자 암호 또는 변경 내용을 변경 하는 경우 로그인을 연결 하는 예를 들어, (예: Facebook, Google, Microsoft 계정 등)를 모두에서 사용자가 로그 브라우저 인스턴스입니다. 예를 들어 아래 이미지는 [Single sign-out 샘플](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/SingleSignOutSample/readme.txt) 단추 하나를 클릭 하 여 모든 브라우저 인스턴스 (이 예제의 경우 IE, Firefox 및 Chrome)에서 로그 아웃 수 있도록 하는 앱입니다. 또는 샘플을 사용 하면만 로그 아웃 특정 브라우저 인스턴스를 수 있습니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image11.png)

합니다 [Single sign-out 샘플](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/SingleSignOutSample/readme.txt) 앱 ASP.NET Id 보안 토큰을 다시 생성할 수 있습니다 하는 방법을 보여 줍니다. 이 이전 암호를 사용 하 여 생성 된 모든 토큰 (쿠키)를 무효화를 확인 해야 합니다. 이 기능은 응용 프로그램에 대 한 보안의 추가 계층을 제공 암호를 변경 하면이 응용 프로그램에 로그인 한 위치 아웃 기록 됩니다.

*앱\_Start\IdentityConfig.cs* 파일을 포함 합니다 `ApplicationUserManager`, `EmailService` 및 `SmsService` 클래스입니다. 합니다 `EmailService` 및 `SmsService` 각 구현 클래스는 `IIdentityMessageService` 인터페이스를 전자 메일 및 SMS를 구성 하려면 각 클래스에서 공용 메서드를 갖도록 합니다. 이 자습서에만 전자 메일 알림을 통해 추가 하는 방법을 보여 주지만 [SendGrid](http://sendgrid.com/), SMTP 및 다른 메커니즘을 사용 하 여 메일을 보낼 수 있습니다.

`Startup` 클래스도 포함 되어 있습니다 소셜 로그인 (Facebook, Twitter 등) 내 자습서를 참조 하십시오. 추가할 보일 러 접시 [Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on을 사용 하 여 MVC 5 앱](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 자세한 정보에 대 한 합니다.

검사는 `ApplicationUserManager` 사용자 id 정보를 포함 하 고 다음 기능을 구성 하는 클래스:

- 암호 강도 요구 사항입니다.
- 사용자 잠금 (시도 및 시간)입니다.
- 2 단계 인증 (2FA)입니다. 2FA 및 SMS에서에서 다룰 다른 자습서입니다.
- 전자 메일 및 SMS 서비스를 연결 합니다. (SMS에서에서 다룰 다른 자습서).

합니다 `ApplicationUserManager` 제네릭에서 클래스 파생 `UserManager<ApplicationUser>` 클래스입니다. `ApplicationUser` 파생 [IdentityUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser.aspx)합니다. `IdentityUser` 제네릭에서 파생 `IdentityUser` 클래스:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample1.cs)]

위의 속성의 속성에 맞춰는 `AspNetUsers` 위에 표시 된 테이블입니다.

제네릭 인수에서 `IUser` 기본 키에 대 한 다양 한 종류를 사용 하는 클래스를 파생 시킬 수 있도록 합니다. 참조 된 [ChangePK](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/ChangePK/readme.txt) int 또는 GUID 문자열에서 기본 키를 변경 하는 방법을 보여주는 샘플입니다.

### <a name="applicationuser"></a>ApplicationUser

`ApplicationUser` (`public class ApplicationUserManager : UserManager<ApplicationUser>`)에 정의 된 *Models\IdentityModels.cs* 으로:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample2.cs?highlight=8-9)]

위의 강조 표시 된 코드 생성을 [ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx)합니다. ASP.NET Id 및 OWIN 쿠키 인증 된 클레임 기반, 프레임 워크의 응용 프로그램에서 생성 하므로 한 `ClaimsIdentity` 사용자에 대 한 합니다. `ClaimsIdentity` 정보가 사용자의 이름과 같은 사용자에 대 한 모든 클레임에 대 한 수명 및 역할에 속해 있습니다. 또한이 단계에서 사용자에 대 한 더 많은 클레임을 추가할 수 있습니다.

OWIN `AuthenticationManager.SignIn` 메서드에 전달 된 `ClaimsIdentity` 사용자 로그인:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample3.cs?highlight=4-6)]

[Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on을 사용 하 여 MVC 5 앱](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 속성을 추가 하는 방법을 보여 줍니다는 `ApplicationUser` 클래스입니다.

## <a name="email-confirmation"></a>전자 메일 확인

새 사용자가 다른 사용자에 가장 하지 않는 것을 확인 하려면 등록 전자 메일을 확인 하는 것이 좋습니다 (즉, 다른 사용자의 전자 메일을 사용 하 여 등록 하지 않은). 방지 하려는 토론 포럼을 설치한 가정 `"bob@example.com"` 로 등록에서 `"joe@contoso.com"`합니다. 전자 메일 확인 하지 않고 `"joe@contoso.com"` 앱에서 원치 않는 전자 메일을 가져올 수 없습니다. Bob 실수로 등록 가정 `"bib@example.com"` 를 눈치채 및 그 앱에 올바른 전자 메일 없는 때문에 암호 복구를 사용할 수 있습니다. 전자 메일 확인은 봇부터에서만 제한 된 보호를 제공 하며 결정된 스패머가에서 보호를 제공 하지 않습니다, 그리고 여러 작업 전자 메일 별칭을 등록 하는 데 사용할 수 있는 합니다. 아래 샘플에서는 사용자가 계정을 확인 될 때까지 암호를 변경 하는 일을 할 수 없습니다 (이들에 의해 사용 하 여 등록할 전자 메일 계정에 수신 확인 링크를 클릭 합니다.) 예를 들어 확인 하 고 해당 프로필에 변경 된 경우 사용자 전자 메일을 보내거나, 관리자가 만든 새 계정에 암호 재설정에 대 한 링크를 보내는 다른 시나리오에이 작업 흐름을 적용할 수 있습니다. 일반적으로 새 사용자가 전자 메일, SMS 문자 메시지 또는 다른 메커니즘을 통해 학인합니다 전에 웹 사이트에 데이터를 게시 하지 못하도록 좋습니다. <a id="build"></a>

## <a name="building-a-more-complete-sample"></a>전체 샘플을 빌드하면

이 섹션에서는 노력할 전체 샘플을 다운로드 하려면 NuGet을 사용 합니다.

1. 새 ***빈*** ASP.NET 웹 프로젝트입니다.
2. 다음을 입력 하는 패키지 관리자 콘솔에서 다음 명령을: 

    [!code-console[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample4.cmd)]

   이 자습서에서는 [SendGrid](http://sendgrid.com/) 전자 메일을 보내도록 합니다. `Identity.Samples` 패키지에서는 사용할 코드를 설치 합니다.
3. 설정 된 [SSL을 사용 하도록 프로젝트](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.
4. 로컬 계정 만들기를 클릭 하 여 앱을 실행 하 여 테스트 합니다 **등록** 에 연결 하 고 등록 양식을 게시 합니다.
5. 전자 메일 확인을 시뮬레이션 하는 데모 전자 메일 링크를 클릭 합니다.
6. 이 샘플에서 데모 전자 메일 링크 확인 코드를 제거 (의 `ViewBag.Link` account 컨트롤러의 코드입니다. 참조 된 `DisplayEmail` 및 `ForgotPasswordConfirmation` razor 뷰와 작업 메서드).

> [!NOTE]
> 경고:이 샘플의 보안 설정을 변경 하면 프로덕션 앱 변경 내용을 명시적으로 호출 하는 보안 감사를 진행 해야 합니다.


## <a name="examine-the-code-in-appstartidentityconfigcs"></a>앱에서 코드를 검사할\_Start\IdentityConfig.cs

이 샘플에서는 계정을 만들고 추가 하는 방법을 보여줍니다. 합니다 *관리자* 역할입니다. 관리자 계정에 사용할 전자 메일을 통해 샘플 전자 메일을 바꿔야 합니다. 관리자 계정을 만들어야 하는 현재 가장 쉬운 방법은 프로그래밍 방식으로 `Seed` 메서드. 도구가 나중에 만들고 사용자 및 역할을 관리할 수 있도록 되기를 바랍니다. 샘플 코드에서는 수를 만들고 사용자 및 역할을 관리 하지만 먼저 역할 및 사용자 관리 페이지를 실행 하는 관리자 계정이 있어야 합니다. 이 샘플에서는 관리자 계정에 DB 시드 되는 경우 만들어집니다.

암호를 변경 하 고 전자 메일 알림을 받을 수 있는 계정으로 이름을 변경 합니다.

> [!WARNING]
> 보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다.

앞서 설명한 대로 합니다 `app.CreatePerOwinContext` startup 클래스의 호출에 대 한 콜백을 추가 `Create` DB 앱 콘텐츠, 사용자 관리자 및 역할 관리자 클래스의 메서드. OWIN 파이프라인 호출을 `Create` 에서 이러한 각 요청에 대 한 클래스 메서드와 각 클래스에 대 한 컨텍스트를 저장 합니다. Account 컨트롤러는 (OWIN 컨텍스트를 포함)는 HTTP 컨텍스트에서 사용자 관리자를 제공 합니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample5.cs)]

사용자가 로컬 계정을 등록 하면는 `HTTP Post Register` 메서드가 호출 됩니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample6.cs)]

위의 코드는 모델 데이터를 사용 하 여 전자 메일 및 암호 입력을 사용 하 여 새 사용자 계정을 만듭니다. 전자 메일 별칭에 있는 경우 데이터 저장소 계정 만들기 실패 하 고 양식을 다시 표시 됩니다. `GenerateEmailConfirmationTokenAsync` 메서드 보안 확인 토큰을 만들고 ASP.NET Id 데이터 저장소에 저장 합니다. 합니다 [Url.Action](https://msdn.microsoft.com/library/dd505232(v=vs.118).aspx) 메서드를 포함 하는 링크 만듭니다는 `UserId` 및 확인 토큰입니다. 이 링크는 사용자에 게 전자 메일로 다음, 해당 계정을 확인 하기 위해 해당 전자 메일 앱에서 링크를 클릭할 수 있습니다.

<a id="email"></a>

## <a name="set-up-email-confirmation"></a>전자 메일 확인 설정

로 이동 합니다 [SendGrid Azure 등록 페이지](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) 무료 계정을 등록 하 고 합니다. SendGrid를 구성 하려면 다음과 비슷한 코드를 추가 합니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample7.cs?highlight=5)]

> [!NOTE]
> 전자 메일 클라이언트에는 자주 텍스트 메시지 (HTML)만 수락합니다. 텍스트 및 HTML의 메시지를 제공 해야 합니다. 위의 SendGrid 샘플에서 사용 하 여 수행 됩니다이 `myMessage.Text` 고 `myMessage.Html` 위에 표시 된 코드입니다.


다음 코드에 사용 하 여 전자 메일을 보내는 방법을 보여 줍니다 합니다 [MailMessage](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx) where 클래스 `message.Body` 링크만 반환 합니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample8.cs)]

> [!WARNING]
> 보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다. 계정 및 자격 증명 appSetting에 저장 됩니다. Azure에서 안전 하 게에 저장할 수 있습니다 이러한 값을 **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** Azure portal에서 탭 합니다. 참조 [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.


SendGrid 자격 증명을 입력 앱을 실행 전자 메일 별칭을 사용 하 여 등록 수 링크를 클릭 확인 전자 메일에서입니다. 이 작업을 수행 하는 방법을 보려면 하 [Outlook.com](http://outlook.com) 전자 메일 계정, John Atten 참조 [Outlook.Com SMTP 호스트에 대 한 C# SMTP 구성](http://typecastexception.com/post/2013/12/20/C-SMTP-Configuration-for-OutlookCom-SMTP-Host.aspx) his 및[ASP.NET Identity 2.0: 계정 구성 설정 유효성 검사 2 단계 인증 및](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) 게시 합니다.

사용자가 클릭 한 후 합니다 **등록** 단추는 유효성 검사 토큰이 포함 된 확인 전자 메일을 해당 전자 메일 주소로 전송 됩니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image12.png)

사용자 계정에 대 한 확인 토큰을 사용 하 여 전자 메일이 전송 됩니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image13.png)

## <a name="examine-the-code"></a>코드 검사

다음 코드는 `POST ForgotPassword` 메서드를 보여 줍니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample9.cs)]

메서드는 사용자 전자 메일이 확인 되지 않았습니다 하는 경우 자동으로 실패 합니다. 오류가 잘못 된 전자 메일 주소에 대 한 게시 된, 악의적인 사용자가 해당 정보를 사용 하 여 공격에 유효한 사용자 Id (전자 메일 별칭)을 찾을 수 없습니다.

다음 코드에서는 `ConfirmEmail` 사용자에 게 보낸 전자 메일 확인 링크를 클릭할 때 호출 되는 account 컨트롤러의 메서드:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample10.cs)]

잊어버린된 암호 토큰을 사용한 후에, 무효화 됩니다. 다음 코드 변경을 `Create` 메서드 (에 *앱\_Start\IdentityConfig.cs* 파일) 3 시간에 만료 되도록 토큰을 설정 합니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample11.cs?highlight=6-8)]

위의 코드를 사용 하 여 암호를 잊은 및 전자 메일 확인 토큰 3 시간에 만료 됩니다. 기본 `TokenLifespan` 은 1 일입니다.

다음 코드는 전자 메일 확인 메서드를 보여 줍니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample12.cs)]

 앱을 더욱 안전 하 게 ASP.NET Id (2FA) 2 단계 인증을 지원 합니다. 참조 [ASP.NET Id 2.0: 계정 유효성 검사 및 2 단계 인증 설정](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) John Atten 여 합니다. 계정 잠금에 로그인 암호 시도 실패를 설정할 수 있지만 해당 방법을 사용 하면 로그인에 취약 [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) 잠금을 수행 합니다. 계정 잠금 2FA를 사용 하 여만 사용 하는 것이 좋습니다.  
<a id="addRes"></a>

## <a name="additional-resources"></a>추가 리소스

- [ASP.NET ID에 대한 사용자 지정 저장소 공급자 개요](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)
- [Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on을 사용 하 여 MVC 5 앱](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 또한 사용자가 테이블에 프로필 정보를 추가 하는 방법을 보여 줍니다.
- [ASP.NET MVC 및 Id 2.0: 기본 사항 이해](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) John Atten 여 합니다.
- [ASP.NET ID 소개](../getting-started/introduction-to-aspnet-identity.md)
- [ASP.NET Id 2.0.0의 RTM 발표](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) Pranav rastogi 합니다.
