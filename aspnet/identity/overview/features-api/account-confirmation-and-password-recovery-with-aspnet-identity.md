---
uid: identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
title: "계정 확인 및 ASP.NET Identity (C#) 사용 하 여 암호 복구 | Microsoft Docs"
author: HaoK
description: "먼저 완료 해야이 자습서를 수행 하기 전에 전자 메일 확인 및 암호 재설정에 대 한 로그와 함께 보안 ASP.NET MVC 5 웹 응용 프로그램을 만듭니다. 이 자습서 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/26/2015
ms.topic: article
ms.assetid: 8d54180d-f826-4df7-b503-7debf5ed9fb3
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 5fa7b6227eb88aa6766ab8776bc8a3cc1111b942
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="account-confirmation-and-password-recovery-with-aspnet-identity-c"></a>계정 확인 및 암호 복구 ASP.NET Identity (C#)
====================
여 [Hao 둘러싼](https://github.com/HaoK), [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://github.com/Rick-Anderson), [Suhas Joshi](https://github.com/suhasj)

> 이 자습서를 수행 하기 전에 먼저를 완료 해야 [전자 메일 확인 및 암호 재설정에 대 한 로그와 보안 ASP.NET MVC 5 웹 응용 프로그램을 만들](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)합니다. 이 자습서 자세한 세부 정보를 포함 하 고 로컬 계정 확인에 대 한 전자 메일을 설정 하 고 사용자가 ASP.NET Identity에서 잊은 암호를 재설정 하도록 허용 하는 방법을 표시 됩니다. 이 문서 Rick Anderson에 의해 작성 되었으므로 ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), Hao 둘러싼 및 Suhas Joshi 합니다. NuGet 샘플 Hao 둘러싼 주로 썼습니다.


로컬 사용자 계정을 사용자 계정에 대 한 암호를 만들기 위해 필요 하 고 해당 암호 web app에서 (안전 하 게) 저장 됩니다. ASP.NET Id는 소셜 계정, 사용자를 응용 프로그램에 대 한 암호를 만들 필요 하지도 지원 합니다. [소셜 계정](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 는 제 3 자 (예: Google, Twitter, Facebook 또는 Microsoft)를 사용 하 여 사용자를 인증 합니다. 이 항목에서는 다음에 대해 설명 합니다.

- [ASP.NET MVC 응용 프로그램을 만들](#createMvc) ASP.NET Id 기능을 탐색 하 고 있습니다.
- [Identity 샘플 빌드](#build)
- [전자 메일 확인 설정](#email)

새 사용자가 자신의 전자 메일 별칭을 로컬 계정을 만들고 등록 합니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image1.png)

레지스터 단추를 클릭 하는 전자 메일 주소가 유효성 검사 토큰을 포함 하는 확인 전자 메일을 보냅니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image2.png)

사용자는 자신의 계정에 대 한 확인 토큰 포함 된 메일이 전송 됩니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image3.png)

링크를 클릭 하는 계정을 확인 합니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image4.png)

<a id="passwordReset"></a>

## <a name="password-recoveryreset"></a>암호 복구/다시 설정

자신의 암호를 잊은 로컬 사용자 자신의 암호를 재설정할 수 있도록 전자 메일 계정으로 전송 하는 보안 토큰을 가질 수 있습니다.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image5.png)  
  
곧 사용자 암호를 재설정 하도록 허용 하는 링크와 전자 메일을 받게 됩니다.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image6.png)  
링크를 클릭 하면 재설정 페이지로 이동 합니다.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image7.png)  
  
클릭 하 고 **다시 설정** 암호를 다시 설정 단추는 확인 합니다.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image8.png)

<a id="createMvc"></a>

## <a name="create-an-aspnet-web-app"></a>ASP.NET 웹 앱 만들기

설치 하 고 실행 하 여 시작 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다. Visual Studio 설치 [2013 업데이트 2](https://go.microsoft.com/fwlink/?LinkId=390521) 이상.

> [!NOTE]
> 경고: Visual Studio를 설치 해야 [2013 업데이트 2](https://go.microsoft.com/fwlink/?LinkId=390521) 이 자습서를 완료 합니다.


1. 새 ASP.NET 웹 프로젝트를 만들고 MVC 템플릿을 선택 합니다. Web Forms web forms 응용 프로그램에서 비슷한 단계를 반영할 수 있도록 ASP.NET Id를도 지원 합니다.
2. 기본 인증을 두고 **개별 사용자 계정**합니다.
3. 응용 프로그램 실행을 클릭는 **등록** 에 연결 하 고 사용자를 등록 합니다. 전자 메일에만 유효성 검사와는 시점에서 [[EmailAddress]](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 특성입니다.
4. 서버 탐색기에서로 이동 **데이터 Connections\DefaultConnection\Tables\AspNetUsers**를 마우스 오른쪽 단추로 클릭 하 고 **테이블 정의 열고**합니다.

    다음 그림에서는 `AspNetUsers` 스키마:

    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image9.png)
5. 마우스 오른쪽 단추로 클릭는 **AspNetUsers** 테이블을 선택한 **테이블 데이터 표시**합니다.  
  
    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image10.png)  
  
 이 시점에서 전자 메일 확인 되지 않았습니다.

ASP.NET Id에 대 한 기본 데이터 저장소는 Entity Framework 하지만 다른 데이터 저장소를 사용 하 고 필드를 더 추가 하 고 구성할 수 있습니다. 참조 [추가 리소스](#addRes) 이 자습서의 마지막 부분에 있습니다.

[OWIN 시작 클래스](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) ( *Startup.cs* ) 응용 프로그램 시작 및 호출 될 때 호출 되는 `ConfigureAuth` 에서 메서드 *앱\_Start\Startup.Auth.cs*, OWIN 파이프라인을 구성 하 고 ASP.NET Identity를 초기화 합니다. 검사는 `ConfigureAuth` 메서드. 각 `CreatePerOwinContext` 호출 콜백을 등록 (에 저장 된 `OwinContext`) 지정 된 형식의 인스턴스를 만드는 요청당 한 번 호출 될 합니다. 생성자에 중단점을 설정할 수 있습니다 및 `Create` 각 유형의 메서드 (`ApplicationDbContext, ApplicationUserManager`)은 각 요청에서 호출을 확인 합니다. 인스턴스 `ApplicationDbContext` 및 `ApplicationUserManager` 응용 프로그램을 통해 액세스할 수 있는 OWIN 컨텍스트로 저장 됩니다. 쿠키 미들웨어를 통해 OWIN 파이프라인에 연결 하는 ASP.NET Identity입니다. 자세한 내용은 참조 [ASP.NET Identity에서 UserManager 클래스에 대 한 요청 수명 관리 당](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)합니다.

새 보안 스탬프를 생성 되 고에 저장 된 보안 프로필을 변경 하면는 `SecurityStamp` 필드는 *AspNetUsers* 테이블입니다. 단는 `SecurityStamp` 필드는 보안 쿠키와에서 다릅니다. 보안 쿠키에 저장 되지 않습니다는 `AspNetUsers` 테이블 (또는 Identity DB의 다른 곳). 사용 하 여 보안 쿠키 토큰 자체 서명 [DPAPI](https://msdn.microsoft.com/en-us/library/system.security.cryptography.protecteddata.aspx) 와 만들어집니다는 `UserId, SecurityStamp` 및 만료 시간 정보입니다.

쿠키 미들웨어 각 요청에 대해 쿠키를 확인합니다. `SecurityStampValidator` 에서 메서드는 `Startup` 클래스 DB에 도달 하 고 보안 스탬프를 주기적으로 확인 된 지정 된 대로 `validateInterval`합니다. 이 보안 프로필을 변경 하지 않는 한 (샘플)에서 30 분 마다만 발생 합니다. 30 분 간격 데이터베이스에 대 한 왕복을 최소화 하기 위해 선택 되었습니다. 참조 내 [자습서 2 단계 인증](index.md) 내용을 확인 합니다.

코드의 주석을 당는 `UseCookieAuthentication` 메서드 쿠키 인증을 지원 합니다. `SecurityStamp` 추가 계층을 제공 하는 필드와 연결 된 코드는 응용 프로그램에 보안을 암호를 변경 하면 경고가 기록 됩니다 로그인 사용한 브라우저 외부에서. `SecurityStampValidator.OnValidateIdentity` 메서드를 사용 하면 암호를 변경 하거나 외부 로그인을 사용할 때 사용 되는 응용 프로그램을 사용자가 로그인 할 때 보안 토큰의 유효성을 검사 합니다. 이 이전 암호를 사용 하 여 생성 중인 토큰 (쿠키)이 무효화 됩니다 되도록 필요 합니다. 샘플 프로젝트에 변경 하는 경우 사용자의 암호가 다음 새 토큰을 사용자에 대해 생성 되, 이전 모든 토큰이 무효화 되 고 `SecurityStamp` 필드가 업데이트 되 고 합니다.

Id 시스템 구성할 수 있도록 앱 하므로 사용자가 보안 프로필 변경 될 때 (사용자의 암호 또는 변경 내용이 변경 될 때 로그인을 연결 하는 예를 들어 (예: Facebook, Google, Microsoft 계정 등)에서 모든 사용자가 로그인 브라우저 인스턴스입니다. 예를 들어 다음 이미지는 [Single sign-out 샘플](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/SingleSignOutSample/readme.txt) 응용 프로그램에 사용 하면 한 개의 단추를 클릭 하 여 로그 아웃에 (이 경우 IE, Firefox 및 Chrome)에 있는 모든 브라우저 인스턴스를 합니다. 또는 샘플만에서 로그 아웃 특정 브라우저 인스턴스를 수 있습니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image11.png)

[Single sign-out 샘플](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/SingleSignOutSample/readme.txt) 앱은 ASP.NET Identity 허용 하는 보안 토큰을 다시 생성 하는 방법을 보여 줍니다. 이 이전 암호를 사용 하 여 생성 중인 토큰 (쿠키)이 무효화 됩니다 되도록 필요 합니다. 이 기능은 보안; 응용 프로그램에 추가적인을 제공합니다. 암호를 변경 하면이 응용 프로그램에 로그인 한 위치 아웃 기록 됩니다.

*앱\_Start\IdentityConfig.cs* 파일에 포함 되어는 `ApplicationUserManager`, `EmailService` 및 `SmsService` 클래스입니다. `EmailService` 및 `SmsService` 각 구현 클래스는 `IIdentityMessageService` 인터페이스, 전자 메일 및 SMS를 구성 하려면 각 클래스에 공용 메서드를 갖도록 합니다. 이 자습서에서는 통해 전자 메일 알림을 추가 하는 방법을 보여 줍니다. 하지만 [SendGrid](http://sendgrid.com/), SMTP 및 다른 메커니즘을 사용 하 여 메일을 보낼 수 있습니다.

`Startup` 클래스 (Facebook, Twitter, 등)에 소셜 로그인 내 자습서를 참조 하십시오. 추가할 보일 러 플레이트 포함 되어 [Facebook, Twitter, LinkedIn 및 Google OAuth2 로그온 된 MVC 5 앱](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 대 한 자세한 정보.

검사는 `ApplicationUserManager` 사용자 id 정보를 포함 하 고 다음과 같은 기능을 구성 하는 클래스:

- 암호 강도 요구 사항입니다.
- 사용자 잠금 (시도 및 시간)입니다.
- 2 단계 인증 (2FA)입니다. 사항이 2FA 및 SMS 다른 자습서입니다.
- 전자 메일 및 SMS 서비스를 연결 합니다. (하겠습니다 SMS 다른 자습서에).

`ApplicationUserManager` 제네릭에서 클래스 파생 `UserManager<ApplicationUser>` 클래스입니다. `ApplicationUser`파생 [IdentityUser](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.identity.entityframework.identityuser.aspx)합니다. `IdentityUser`원본에서 파생 `IdentityUser` 클래스:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample1.cs)]

위의 속성의 속성에 맞춰는 `AspNetUsers` 위에 표시 된 테이블입니다.

제네릭 인수에서 `IUser` 다양 한 종류를 사용 하 여 기본 키에 대 한 클래스를 파생 시킬 수 있도록 합니다. 참조는 [ChangePK](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/ChangePK/readme.txt) int 또는 GUID 문자열에서 기본 키를 변경 하는 방법을 보여 주는 샘플입니다.

### <a name="applicationuser"></a>ApplicationUser

`ApplicationUser`(`public class ApplicationUserManager : UserManager<ApplicationUser>`)에 정의 된 *Models\IdentityModels.cs* 로:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample2.cs?highlight=8-9)]

위의 강조 표시 된 코드를 생성 한 [ClaimsIdentity](https://msdn.microsoft.com/en-us/library/system.security.claims.claimsidentity.aspx)합니다. ASP.NET Identity OWIN 쿠키 인증 되며 클레임 기반, 프레임 워크 하므로 응용 프로그램에서 생성 한 `ClaimsIdentity` 사용자에 대 한 합니다. `ClaimsIdentity`정보가 사용자의 이름과 같은 사용자에 대 한 모든 클레임에 대 한 기간 및 해당 사용자가 역할에 속해 있습니다. 또한이 단계에서 사용자에 대 한 더 많은 클레임을 추가할 수 있습니다.

OWIN `AuthenticationManager.SignIn` 메서드에 전달 된 `ClaimsIdentity` 사용자가 로그인:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample3.cs?highlight=4-6)]

[Facebook, Twitter, LinkedIn 및 Google OAuth2 로그온 된 MVC 5 앱](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 추가 속성을 추가 하는 방법을 보여 줍니다.는 `ApplicationUser` 클래스입니다.

## <a name="email-confirmation"></a>전자 메일 확인

다른 사용자에 가장 하지 않는 것을 확인 하려면 새 사용자 등록 전자 메일을 확인 하는 것이 좋습니다 (즉, 이러한 하지 않은 등록 된 다른 사용자의 전자 메일). 방지 하기 위해 원할 토론 포럼을 설치한 경우를 가정해 볼 `"bob@example.com"` 등록에서 `"joe@contoso.com"`합니다. 전자 메일 확인 하지 않고 `"joe@contoso.com"` 원치 않는 전자 메일 앱에서 가져올 수 있습니다. 실수로 Bob로 등록 된 경우를 가정해 볼 `"bib@example.com"` 를 발견 하지 않은 그 하는지 앱에 없는 올바른 전자 메일 때문에 암호 복구를 사용할 수 없게 됩니다. 전자 메일 확인 bot에서 제한 된 보호만을 제공 하 고 결정된 된 스팸에서 보호를 제공 하지 않습니다, 그리고 등록 하는 데 사용할 수는 많은 작업 전자 메일 별칭을가지고 있습니다. 아래 예제에서 사용자 자신의 계정을 확인 될 때까지 암호를 변경할 수 없습니다 (타인이 등록 전자 메일 계정에 수신 확인 링크를 클릭 합니다.) 예를 확인 하 고 자신의 프로필에 변경 하는 경우 사용자는 메일을 보내 관리자가 만든 새 계정에 암호를 다시 설정에 대 한 링크를 보내는 다른 시나리오에이 작업 흐름을 적용할 수 있습니다. 일반적으로 새 사용자 전자 메일, SMS 문자 메시지 또는 기타 메커니즘 확인 하기 전에 모든 데이터 웹 사이트를 게시 하는 것을 방지 하려고 합니다. <a id="build"></a>

## <a name="building-a-more-complete-sample"></a>전체 샘플을 빌드

이 섹션으로 작업 하는 전체 예제를 다운로드 하려면 NuGet을 사용 합니다.

1. 새 ***빈*** ASP.NET 웹 프로젝트입니다.
2. 패키지 관리자 콘솔에서 다음을 입력 하면 다음 명령이 있습니다. 

    [!code-console[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample4.cmd)]

 이 자습서에서는 [SendGrid](http://sendgrid.com/) 전자 메일을 보내도록 합니다. `Identity.Samples` 패키지와 사용할 코드를 설치 합니다.
3. 설정의 [SSL을 사용 하도록 프로젝트](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.
4. 로컬 계정 만들기를 클릭 하 여 앱을 실행 하 여 테스트는 **등록** 에 연결 하 고 등록 양식을 게시 합니다.
5. 전자 메일 확인을 시뮬레이트하는 데모 전자 메일 링크를 클릭 합니다.
6. 이 샘플에서 데모 전자 메일 링크 확인 코드를 제거 (의 `ViewBag.Link` 계정 컨트롤러의 코드입니다. 참조는 `DisplayEmail` 및 `ForgotPasswordConfirmation` 작업 메서드 및 razor 뷰가).

> [!NOTE]
> 경고:이 샘플의 보안 설정을 변경 하면 프로덕션 응용 프로그램의 변경 내용을 명시적으로 호출 하는 보안 감사를 해야 합니다.


## <a name="examine-the-code-in-appstartidentityconfigcs"></a>응용 프로그램에서 코드를 검사할\_Start\IdentityConfig.cs

이 샘플에서는 계정을 만들고에 추가 하는 방법을 보여 줍니다.는 *Admin* 역할입니다. 관리자 계정에 사용 하려는 전자 메일을 가진 샘플에서 전자 메일을 바꿔야 합니다. 관리자 계정을 만들어야 하는 지금 바로 가장 쉬운 방법은 프로그래밍 방식으로 `Seed` 메서드. 도구가 나중에 만들고 사용자 및 역할을 관리할 수 있도록 하기 위해 노력 합니다. 샘플 코드에서는 수를 만들고 사용자 및 역할을 관리 하지만 역할 및 사용자 관리 페이지를 실행 하는 관리자 계정이 있어야 합니다. 이 샘플에서는 관리자 계정에는 DB 시드 된 때 만들어집니다.

암호를 변경 하 고 전자 메일 알림을 받을 수 있는 계정 이름을 변경 합니다.

> [!WARNING]
> 보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다.

앞에서 설명한 대로 `app.CreatePerOwinContext` 시작 클래스에서 호출에 대 한 콜백을 추가 하는 `Create` DB 응용 프로그램 콘텐츠, 사용자 관리자 및 역할 관리자 클래스의 메서드. OWIN 파이프라인 호출은 `Create` 이러한 이벤트에 대해 각 요청에 대 한 클래스 메서드와 각 클래스에 대 한 컨텍스트를 저장 합니다. 계정 컨트롤러 사용자 관리자는 HTTP 컨텍스트 (에서 OWIN 컨텍스트를 포함)를 노출 합니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample5.cs)]

로컬 계정, 사용자가 등록할 때는 `HTTP Post Register` 메서드를 호출 합니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample6.cs)]

위의 코드 모델 데이터를 사용 하 여 전자 메일 및 입력 한 암호를 사용 하 여 새 사용자 계정을 만듭니다. 전자 메일 별칭 데이터 저장소에 있으면 계정 만들기가 실패 하 고 양식을 다시 표시 됩니다. `GenerateEmailConfirmationTokenAsync` 메서드 보안 확인 토큰을 만드는 데 ASP.NET Identity 데이터 저장소에 저장 합니다. [Url.Action](https://msdn.microsoft.com/en-us/library/dd505232(v=vs.118).aspx) 메서드를 포함 하는 링크 만듭니다는 `UserId` 및 확인 토큰입니다. 이 링크는 사용자에 게 메일로 다음, 해당 계정을 확인 하는 전자 메일 앱의 링크에서 클릭할 수 있습니다.

<a id="email"></a>

## <a name="set-up-email-confirmation"></a>전자 메일 확인 설정

이동 하는 [Azure SendGrid 등록 페이지](https://azure.microsoft.com/en-us/gallery/store/sendgrid/sendgrid-azure/) 무료 계정을 등록 하 고 있습니다. SendGrid를 구성 하려면 다음과 유사한 코드를 추가 합니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample7.cs?highlight=5)]

> [!NOTE]
> 전자 메일 클라이언트에는 자주 텍스트 메시지 (HTML)만 허용 합니다. 메시지 텍스트와 HTML에 제공 해야 합니다. 위의 SendGrid 예제에서 이러한 용도로 `myMessage.Text` 및 `myMessage.Html` 위에 표시 된 코드입니다.


다음 코드를 사용 하 여 전자 메일을 전송 하는 방법을 보여 줍니다는 [MailMessage](https://msdn.microsoft.com/en-us/library/system.net.mail.mailmessage.aspx) 클래스 `message.Body` 링크만 반환 합니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample8.cs)]

> [!WARNING]
> 보안-소스 코드에서 중요 한 데이터 저장 되지 않습니다. 계정 및 자격 증명 appSetting에 저장 됩니다. Azure에서 안전 하 게에 저장할 수 있습니다 이러한 값은  **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)**  Azure 포털에서 탭 합니다. 참조 [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터 배포에 대 한 유용한](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)합니다.


SendGrid 자격 증명을 입력 앱을 실행 된 전자 메일 별칭 레지스터 수 링크를 클릭 하십시오 확인 전자 메일에 합니다. 이 작업을 수행 하는 방법을 보려면 프로그램 [Outlook.com](http://outlook.com) 전자 메일 계정, John Atten 참조 [Outlook.Com SMTP 호스트에 대 한 C# SMTP 구성](http://typecastexception.com/post/2013/12/20/C-SMTP-Configuration-for-OutlookCom-SMTP-Host.aspx) 및 이들의[ASP.NET Identity 2.0: 계정 구성 설정 유효성 검사 2 단계 인증 및](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) 게시 합니다.

사용자가 클릭 한 후의 **등록** 단추 확인 전자 메일 유효성 검사 토큰이 포함 된 해당 전자 메일 주소로 전송 됩니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image12.png)

사용자는 자신의 계정에 대 한 확인 토큰 포함 된 메일이 전송 됩니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image13.png)

## <a name="examine-the-code"></a>코드 검사

다음 코드는 `POST ForgotPassword` 메서드를 보여 줍니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample9.cs)]

사용자 전자 메일 확인 되지 않았습니다 메서드가 자동으로 실패 합니다. 오류가 잘못 된 전자 메일 주소에 대 한 게시 된 경우 악의적인 사용자가 해당 정보 공격에 올바른 사용자 Id (전자 메일 별칭)을 사용 합니다.

다음 코드는 `ConfirmEmail` 계정 컨트롤러을 보낼 전자 메일 확인 링크를 클릭할 때 호출 되는 메서드:

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample10.cs)]

잊어버린된 암호 토큰을 사용한 후에, 무효화 됩니다. 다음 코드 변경 내용을 `Create` 메서드 (에 *앱\_Start\IdentityConfig.cs* 파일) 토큰 3 시간에 만료 되도록 설정 합니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample11.cs?highlight=6-8)]

위의 코드와 함께 잊어버린된 암호 및 전자 메일 확인 토큰 3 시간에 만료 됩니다. 기본 `TokenLifespan` 은 1 일입니다.

다음 코드에는 전자 메일 확인 방법을 보여 줍니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample12.cs)]

 응용 프로그램을 보다 안전 하 게 ASP.NET Identity (2FA) 2 단계 인증을 지원 합니다. 참조 [ASP.NET Identity 2.0: 계정 유효성 검사 및 2 단계 인증을 설정](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) John Atten 여 합니다. 로그인 암호 시도 실패에 계정 잠금에 설정할 수 있지만 해당 접근 방식을 통해 사용자의 로그인에 취약 [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) 잠금을 수행 합니다. 계정 잠금 2FA에만 사용 하는 것이 좋습니다.  
<a id="addRes"></a>

## <a name="additional-resources"></a>추가 리소스

- [ASP.NET Id에 대 한 사용자 지정 저장소 공급자 개요](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)
- [Facebook, Twitter, LinkedIn 및 Google OAuth2 로그온 된 MVC 5 앱](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 사용자 테이블에 프로필 정보를 추가 하는 방법도 설명 합니다.
- [ASP.NET MVC 및 Id 2.0: 기본 사항을 이해](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) John Atten 여 합니다.
- [ASP.NET Id 소개](../getting-started/introduction-to-aspnet-identity.md)
- [ASP.NET Identity 2.0.0의 RTM 발표](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) Pranav Rastogi 여 합니다.
