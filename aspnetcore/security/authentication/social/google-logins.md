---
title: ASP.NET Core에서 Google 외부 로그인 설정
author: rick-anderson
description: 이 자습서에서는 기존 ASP.NET Core 앱에 Google 계정 사용자 인증의 통합을 보여 줍니다.
ms.author: riande
ms.custom: mvc
ms.date: 11/11/2018
uid: security/authentication/google-logins
ms.openlocfilehash: dfda83e1d7cf3c5ff8e31de20c15d468de5d15c0
ms.sourcegitcommit: 09bcda59a58019fdf47b2db5259fe87acf19dd38
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51708454"
---
# <a name="google-external-login-setup-in-aspnet-core"></a>ASP.NET Core에서 Google 외부 로그인 설정

작성자: [Valeriy Novytskyy](https://github.com/01binary) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

이 자습서에서 만든 샘플 ASP.NET Core 2.0 프로젝트를 사용 하 여 Google + 계정으로 로그인 사용자가 사용 하도록 설정 하는 방법을 보여 줍니다.는 [이전 페이지](xref:security/authentication/social/index)합니다. 수행 하 여 시작 합니다 [공식 단계](https://developers.google.com/identity/sign-in/web/devconsole-project) Google API 콘솔에서 새 앱을 만듭니다.

## <a name="create-the-app-in-google-api-console"></a>Google API 콘솔에서 앱 만들기

* 이동할 [ https://console.developers.google.com/projectselector/apis/library ](https://console.developers.google.com/projectselector/apis/library) 에 로그인 합니다. 사용 하 여 Google 계정이 아직 없다면 **더 많은 옵션** > **[계정을 만들려면](https://accounts.google.com/SignUpWithoutGmail?service=cloudconsole&continue=https%3A%2F%2Fconsole.developers.google.com%2Fprojectselector%2Fapis%2Flibrary&ltmpl=api)**  만들려면 링크:

![Google API 콘솔](index/_static/GoogleConsoleLogin.png)

* 리디렉션됩니다 **API Manager 라이브러리** 페이지:

![API Manager 라이브러리 페이지](index/_static/GoogleConsoleSwitchboard.png)

* 탭 **Create** 입력 하 **프로젝트 이름을**:

![새 프로젝트 대화 상자](index/_static/GoogleConsoleNewProj.png)

* 대화 상자를 수락 하면 새 앱에 대 한 기능을 선택할 수 있도록 라이브러리 페이지로 다시 리디렉션됩니다. 찾을 **Google + API** 목록 및 API 기능을 추가 하려면 해당 링크를 클릭 합니다.

![API Manager 라이브러리 페이지](index/_static/GoogleConsoleChooseApi.png)

* 새로 추가 된 API에 대 한 페이지가 표시 됩니다. 탭 **사용** 기능에서 앱에 Google + 기호를 추가 하려면:

![API Manager Google + API 페이지](index/_static/GoogleConsoleEnableApi.png)

* API를 사용 하도록 설정한 후 탭 **자격 증명 만들기** 암호를 구성 하려면:

![API Manager Google + API 페이지](index/_static/GoogleConsoleGoCredentials.png)

* 다음 중 하나를 선택합니다.
  * **Google+ API**
  * **웹 서버 (예:: node.js, Tomcat)**, 및
  * **사용자 데이터**:

![API 관리자 자격 증명 페이지: 어떤 종류의 자격 증명에 대해 알아보세요 필요한 패널](index/_static/GoogleConsoleChooseCred.png)

* 탭 **어떤 자격 증명 필요 합니까?** 안내 하는 앱 구성의 두 번째 단계로 **OAuth 2.0 클라이언트 ID 만들기**:

![API 관리자 자격 증명 페이지: OAuth 2.0 클라이언트 ID 만들기](index/_static/GoogleConsoleCreateClient.png)

* 하나의 기능 (로그인)를 동일한 입력 수를 사용 하 여 Google + 프로젝트를 만드는 것 때문에 **이름을** 에서는 프로젝트에 대해 사용 되는 OAuth 2.0 클라이언트 ID에 대 한 합니다.

* 개발 URI를 입력으로 `/signin-google` 에 추가 합니다 **권한이 부여 된 리디렉션 Uri** 필드 (예를 들어: `https://localhost:44320/signin-google`). 이 자습서의 뒷부분에서 구성 된 Google 인증에서 요청을 자동으로 처리 됩니다 `/signin-google` OAuth 흐름을 구현 하는 경로입니다.

> [!NOTE]
> URI 세그먼트 `/signin-google` Google 인증 공급자의 기본 콜백으로 설정 됩니다. 상속을 통해 Google 인증 미들웨어를 구성 하는 동안 기본 콜백 URI를 변경할 수 있습니다 [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath) 의 속성을 [GoogleOptions](/dotnet/api/microsoft.aspnetcore.authentication.google.googleoptions) 클래스입니다.

* Tab 키를 추가 합니다 **권한이 부여 된 리디렉션 Uri** 항목입니다.

* 탭 **클라이언트 ID 만들기**, 세 번째 단계로, 그러면 **OAuth 2.0 동의 화면 설정**:

![API 관리자 자격 증명 페이지: OAuth 2.0 동의 화면 설정](index/_static/GoogleConsoleAddCred.png)

* 입력에 공개 **전자 메일 주소** 하며 **제품 이름** Google + 라는 로그인 할 때 앱에 대 한 표시 합니다. 추가 옵션을 사용할 수 있습니다 **더 많은 사용자 지정 옵션**합니다.

* 탭 **계속** 마지막 단계를 계속 하려면 **자격 증명 다운로드**:

![API 관리자 자격 증명 페이지: 자격 증명 다운로드](index/_static/GoogleConsoleFinish.png)

* 탭 **다운로드** 응용 프로그램 비밀을 사용 하 여 JSON 파일을 저장 하 고 **수행** 새 앱 만들기를 완료 합니다.

* 다시 방문 해야 사이트를 배포 하는 경우는 **Google 콘솔** 새 공용 url을 등록 합니다.

## <a name="store-google-clientid-and-clientsecret"></a>저장소 Google ClientID 및 ClientSecret

Google와 같은 중요 한 설정이 연결 `Client ID` 하 고 `Client Secret` 사용 하 여 응용 프로그램 구성에는 [암호 관리자](xref:security/app-secrets). 이 자습서에서는 이름을 토큰 `Authentication:Google:ClientId` 고 `Authentication:Google:ClientSecret`입니다.

이러한 토큰에 대 한 값에서 이전 단계에서 다운로드 한 JSON 파일에서 찾을 수 있습니다 `web.client_id` 고 `web.client_secret`입니다.

## <a name="configure-google-authentication"></a>Google 인증 구성

::: moniker range=">= aspnetcore-2.0"

Google 서비스에 추가 합니다 `ConfigureServices` 의 메서드 *Startup.cs* 파일:

```csharp
services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

services.AddAuthentication().AddGoogle(googleOptions =>
{
    googleOptions.ClientId = Configuration["Authentication:Google:ClientId"];
    googleOptions.ClientSecret = Configuration["Authentication:Google:ClientSecret"];
});
```

[!INCLUDE [default settings configuration](includes/default-settings.md)]

[!INCLUDE[](includes/chain-auth-providers.md)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

이 자습서에 사용 되는 프로젝트 템플릿이 되도록 [Microsoft.AspNetCore.Authentication.Google](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Google) 패키지를 설치 합니다.

* Visual Studio 2017을 사용 하 여이 패키지를 설치 하려면 마우스 오른쪽 단추로 클릭 프로젝트를 마우스 **NuGet 패키지 관리**합니다.
* .NET Core CLI를 설치 하려면 프로젝트 디렉터리에서 다음을 실행 합니다.

`dotnet add package Microsoft.AspNetCore.Authentication.Google`

Google 미들웨어를 추가 합니다 `Configure` 의 메서드 *Startup.cs* 파일:

```csharp
app.UseGoogleAuthentication(new GoogleOptions()
{
    ClientId = Configuration["Authentication:Google:ClientId"],
    ClientSecret = Configuration["Authentication:Google:ClientSecret"]
});
```

::: moniker-end

참조 된 [GoogleOptions](/dotnet/api/microsoft.aspnetcore.builder.googleoptions) Google 인증에서 지 원하는 구성 옵션에 대 한 자세한 내용은 API 참조. 이 사용 하 여 사용자에 대 한 다른 정보를 요청할 수 수 있습니다.

## <a name="sign-in-with-google"></a>Google로 로그인

응용 프로그램을 실행 하 고 클릭 **로그인**합니다. Google로 로그인 하는 옵션이 표시 됩니다.

![Microsoft Edge에서 실행 되는 웹 응용 프로그램: 인증 되지 않은 사용자](index/_static/DoneGoogle.png)

Google을 클릭할 때 리디렉션됩니다 Google 인증을 위해:

![Google 인증 대화 상자](index/_static/GoogleLogin.png)

Google 자격 증명을 입력 한 후 다음 리디렉션됩니다 전자 메일을 설정할 수 있는 웹 사이트로 다시 합니다.

이제 Google 자격 증명을 사용 하 여 로그인 됩니다.

![Microsoft Edge에서 실행 되는 웹 응용 프로그램: 사용자 인증](index/_static/Done.png)

[!INCLUDE[Forward request information when behind a proxy or load balancer section](includes/forwarded-headers-middleware.md)]

## <a name="troubleshooting"></a>문제 해결

* 표시 되 면을 `403 (Forbidden)` 개발 모드 (또는 동일한 오류로 디버거로 중단)에서 실행 되도록 하는 경우 사용자 고유의 앱에서 오류 페이지 **Google + API** 에서 설정 되어 있는지를 **APIManager라이브러리** 나열 된 단계를 수행 하 여 [이 페이지에서 이전](#create-the-app-in-google-api-console)합니다. 로그인 작동 하지 않습니다 하 고 오류를 가져오지 않음, 문제를 더 쉽게 디버그 하려면 개발 모드를 전환 합니다.
* **ASP.NET Core 2.x만:** 경우 Identity를 호출 하 여 구성 되지 않았습니다 `services.AddIdentity` 에 `ConfigureServices`에 인증 하려고 하면 *ArgumentException: 'SignInScheme' 옵션을 제공 해야*합니다. 이 자습서에 사용 되는 프로젝트 템플릿이이 수행 되도록 보장 합니다.
* 사이트 데이터베이스를 초기 마이그레이션을 적용 하 여 만들어지지 않은, 경우 받습니다 *요청을 처리 하는 동안 데이터베이스 작업이 실패 했습니다.* 오류입니다. 탭 **마이그레이션 적용** 데이터베이스를 만들고 오류 지 나 새로 고침 합니다.

## <a name="next-steps"></a>다음 단계

* 이 문서에서는 Google을 사용 하 여 인증 하는 보여 주었습니다. 에 나열 된 다른 공급자를 사용 하 여 인증 하는 유사한 방법을 따를 수 있습니다 합니다 [이전 페이지](xref:security/authentication/social/index)합니다.

* 다시 설정 해야 Azure 웹 앱에 웹 사이트를 게시 하면는 `ClientSecret` Google API 콘솔에서.

* 설정 된 `Authentication:Google:ClientId` 및 `Authentication:Google:ClientSecret` Azure portal에서 응용 프로그램 설정 합니다. 구성 시스템 환경 변수에서 키를 읽을 수 설정 됩니다.
