---
title: ASP.NET Core를 사용 하 여 Microsoft 계정 외부 로그인 설정
author: rick-anderson
description: 이 자습서에서는 기존 ASP.NET Core 앱에 Microsoft 계정 사용자 인증의 통합을 보여 줍니다.
ms.author: riande
ms.custom: mvc
ms.date: 11/11/2018
uid: security/authentication/microsoft-logins
ms.openlocfilehash: 1733d049d6752c24d7749b5b5ae2a4b866492358
ms.sourcegitcommit: 3e9e1f6d572947e15347e818f769e27dea56b648
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2019
ms.locfileid: "58751002"
---
# <a name="microsoft-account-external-login-setup-with-aspnet-core"></a>ASP.NET Core를 사용 하 여 Microsoft 계정 외부 로그인 설정

작성자: [Valeriy Novytskyy](https://github.com/01binary) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

이 자습서에서 만든 샘플 ASP.NET Core 2.0 프로젝트를 사용 하 여 Microsoft 계정으로 로그인 사용자가 사용 하도록 설정 하는 방법을 보여 줍니다.는 [이전 페이지](xref:security/authentication/social/index)합니다.

## <a name="create-the-app-in-microsoft-developer-portal"></a>Microsoft 개발자 포털에서 앱 만들기

* 이동할 [ https://apps.dev.microsoft.com ](https://apps.dev.microsoft.com) 만들거나 Microsoft 계정으로 로그인 합니다.

![로그인 대화 상자](index/_static/MicrosoftDevLogin.png)

Microsoft 계정이 아직 없다면 탭  **[만드세요!](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=13&ct=1478151035&rver=6.7.6643.0&wp=SAPI_LONG&wreply=https%3a%2f%2fapps.dev.microsoft.com%2fLoginPostBack&id=293053&aadredir=1&contextid=D70D4F21246BAB50&bk=1478151036&uiflavor=web&uaid=f0c3de863a914c358b8dc01b1ff49e85&mkt=EN-US&lc=1033&lic=1)** 로그인 한 후 리디렉션됩니다 **내 응용 프로그램** 페이지:

![Microsoft Edge에서 열린 Microsoft 개발자 포털](index/_static/MicrosoftDev.png)

* 탭 **앱 추가** 오른쪽 상단 모서리에 입력 하 **응용 프로그램 이름** 하 고 **Contact Email**:

![새 응용 프로그램 등록 대화 상자](index/_static/MicrosoftDevAppCreate.png)

* 이 자습서에서는 선택을 취소 합니다 **안내식 설정** 확인란 합니다.

* 탭 **Create** 를 계속 합니다 **등록** 페이지. 제공을 **이름** 의 값을 확인 합니다 **응용 프로그램 Id**,으로 사용 하는 `ClientId` 자습서의에서 뒷부분에서:

![등록 페이지](index/_static/MicrosoftDevAppReg.png)

* 탭 **플랫폼 추가** 에 **플랫폼** 섹션을 선택 합니다 **웹** 플랫폼:

![추가 플랫폼 대화 상자](index/_static/MicrosoftDevAppPlatform.png)

* 새 **웹** 플랫폼 섹션에서 사용 하 여 개발 URL 입력 `/signin-microsoft` 에 추가 합니다 **리디렉션 Url** 필드 (예를 들어: `https://localhost:44320/signin-microsoft`). 이 자습서의 뒷부분에서 구성 된 Microsoft 인증 체계에서 요청을 자동으로 처리 됩니다 `/signin-microsoft` OAuth 흐름을 구현 하는 경로:

![웹 플랫폼 섹션](index/_static/MicrosoftRedirectUri.png)

> [!NOTE]
> URI 세그먼트 `/signin-microsoft` Microsoft 인증 공급자의 기본 콜백으로 설정 됩니다. 상속을 통해 Microsoft 인증 미들웨어를 구성 하는 동안 기본 콜백 URI를 변경할 수 있습니다 [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath) 의 속성을 [MicrosoftAccountOptions](/dotnet/api/microsoft.aspnetcore.authentication.microsoftaccount.microsoftaccountoptions) 클래스입니다.

* 탭 **URL 추가** URL가 추가 되도록 합니다.

* 필요한 경우 다른 응용 프로그램 설정 작성 하 고 탭 **저장할** 앱 구성에 변경 내용을 저장 하려면 페이지 맨 아래에 있습니다.

* 다시 방문 해야 사이트를 배포 하는 경우는 **등록** 페이지 및 새 공용 URL을 설정 합니다.

## <a name="store-microsoft-application-id-and-password"></a>Microsoft 응용 프로그램 Id 및 암호를 저장 합니다.

* 참고 합니다 `Application Id` 에 표시 합니다 **등록** 페이지입니다.

* 탭 **새 암호 생성** 에 **응용 프로그램 비밀** 섹션입니다. 이 응용 프로그램 암호를 복사할 수 있는 상자를 표시 합니다.

![새 암호가 생성 대화 상자](index/_static/MicrosoftDevPassword.png)

Microsoft와 같은 중요 한 설정이 연결 `Application ID` 하 고 `Password` 사용 하 여 응용 프로그램 구성에는 [암호 관리자](xref:security/app-secrets)합니다. 이 자습서에서는 이름을 토큰 `Authentication:Microsoft:ApplicationId` 고 `Authentication:Microsoft:Password`입니다.

[!INCLUDE[](~/includes/environmentVarableColon.md)]

## <a name="configure-microsoft-account-authentication"></a>Microsoft 계정 인증 구성

이 자습서에 사용 되는 프로젝트 템플릿이 되도록 [Microsoft.AspNetCore.Authentication.MicrosoftAccount](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.MicrosoftAccount) 패키지가 이미 설치 되었습니다.

* Visual Studio 2017을 사용 하 여이 패키지를 설치 하려면 마우스 오른쪽 단추로 클릭 프로젝트를 마우스 **NuGet 패키지 관리**합니다.
* .NET Core CLI를 설치 하려면 프로젝트 디렉터리에서 다음을 실행 합니다.

   `dotnet add package Microsoft.AspNetCore.Authentication.MicrosoftAccount`

::: moniker range=">= aspnetcore-2.0"

Microsoft 계정 서비스에 추가 합니다 `ConfigureServices` 의 메서드 *Startup.cs* 파일:

```csharp
services.AddDefaultIdentity<IdentityUser>()
        .AddDefaultUI(UIFramework.Bootstrap4)
        .AddEntityFrameworkStores<ApplicationDbContext>();

services.AddAuthentication().AddMicrosoftAccount(microsoftOptions =>
{
    microsoftOptions.ClientId = Configuration["Authentication:Microsoft:ApplicationId"];
    microsoftOptions.ClientSecret = Configuration["Authentication:Microsoft:Password"];
});
```

[!INCLUDE [default settings configuration](includes/default-settings.md)]

[!INCLUDE[](includes/chain-auth-providers.md)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

Microsoft 계정 미들웨어를 추가 합니다 `Configure` 의 메서드 *Startup.cs* 파일:

```csharp
app.UseMicrosoftAccountAuthentication(new MicrosoftAccountOptions()
{
    ClientId = Configuration["Authentication:Microsoft:ApplicationId"],
    ClientSecret = Configuration["Authentication:Microsoft:Password"]
});
```

::: moniker-end

하지만 Microsoft 개발자 포털에서 사용 되는 용어 이름은 이러한 토큰 `ApplicationId` 하 고 `Password`,으로 노출 하는 `ClientId` 및 `ClientSecret` 구성 API에.

참조 된 [MicrosoftAccountOptions](/dotnet/api/microsoft.aspnetcore.builder.microsoftaccountoptions) Microsoft 계정 인증에서 지 원하는 구성 옵션에 대 한 자세한 내용은 API 참조. 이 사용 하 여 사용자에 대 한 다른 정보를 요청할 수 수 있습니다.

## <a name="sign-in-with-microsoft-account"></a>Microsoft 계정으로 로그인

응용 프로그램을 실행 하 고 클릭 **로그인**합니다. Microsoft에 로그인 하는 옵션이 표시 됩니다.

![웹 페이지 응용 프로그램 로그: 인증 되지 않은 사용자](index/_static/DoneMicrosoft.png)

Microsoft를 클릭 하면 리디렉션됩니다 Microsoft 인증에 대 한 합니다. (아직 로그인 하지 않은) 하는 경우 Microsoft 계정으로 로그인 한 후 앱 정보에 액세스할 수 있도록 라는 메시지가 표시 됩니다.

![Microsoft 인증 대화 상자](index/_static/MicrosoftLogin.png)

탭 **예** 및 전자 메일을 설정할 수 있는 웹 사이트로 다시 리디렉션됩니다.

이제 Microsoft 자격 증명을 사용 하 여 로그인 됩니다.

![웹 응용 프로그램: 인증 된 사용자](index/_static/Done.png)

[!INCLUDE[Forward request information when behind a proxy or load balancer section](includes/forwarded-headers-middleware.md)]

## <a name="troubleshooting"></a>문제 해결

* Microsoft 계정 공급자는 로그인 오류 페이지로 리디렉션됩니다, 하는 경우 오류 제목과 설명을 쿼리 문자열 매개 변수 바로 다음을 유의 합니다 `#` (해시 태그) Uri에 있습니다.

  가장 일반적인 원인은 응용 프로그램의 모든 일치 하지 않는 Uri 오류 메시지는 Microsoft 인증에 문제가 있음을 나타낼 것 처럼 보이지만, 합니다 **리디렉션 Uri** 에 대해 지정 된 된 **웹** 플랫폼 .
* **ASP.NET Core 2.x만:** 호출 하 여 구성 되어 있지 않으면 Identity `services.AddIdentity` 에 `ConfigureServices`를 인증 하려고 하면 *ArgumentException: 'SignInScheme' 옵션을 제공 해야*합니다. 이 자습서에 사용 되는 프로젝트 템플릿이이 수행 되도록 보장 합니다.
* 사이트 데이터베이스를 초기 마이그레이션을 적용 하 여 만들어지지 않은, 경우 받습니다 *요청을 처리 하는 동안 데이터베이스 작업이 실패 했습니다.* 오류입니다. 탭 **마이그레이션 적용** 데이터베이스를 만들고 오류 지 나 새로 고침 합니다.

## <a name="next-steps"></a>다음 단계

* 이 문서에서는 Microsoft를 사용 하 여 인증 하는 보여 주었습니다. 에 나열 된 다른 공급자를 사용 하 여 인증 하는 유사한 방법을 따를 수 있습니다 합니다 [이전 페이지](xref:security/authentication/social/index)합니다.

* 새 만들어야 Azure 웹 앱에 웹 사이트를 게시 하면 `Password` Microsoft 개발자 포털에서 합니다.

* 설정 된 `Authentication:Microsoft:ApplicationId` 및 `Authentication:Microsoft:Password` Azure portal에서 응용 프로그램 설정 합니다. 구성 시스템 환경 변수에서 키를 읽을 수 설정 됩니다.
