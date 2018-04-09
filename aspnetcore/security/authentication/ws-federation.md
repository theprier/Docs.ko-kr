---
title: ASP.NET Core에서는 Ws-federation로 사용자를 인증
author: chlowell
description: 이 자습서에서는 ASP.NET Core 응용 프로그램의 Ws-federation을 사용 하는 방법을 설명 합니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 02/27/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/ws-federation
ms.openlocfilehash: d4621c7b97678903b9f2562e353da3883334b599
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="authenticate-users-with-ws-federation-in-aspnet-core"></a>ASP.NET Core에서는 Ws-federation로 사용자를 인증

이 자습서에서는 사용자가 WS-페더레이션 인증 공급자와 같은 페더레이션 서비스 ADFS (Active Directory)로 로그인 할 수 있도록 하는 방법을 설명 또는 [Azure Active Directory](/azure/active-directory/) (AAD). 에 설명 된 ASP.NET 코어 2.0 샘플 응용 프로그램을 사용 하 여 [Facebook, Google, 및 외부 공급자 인증](xref:security/authentication/social/index)합니다.

ASP.NET Core 2.0 응용 프로그램의 경우 Ws-federation 지원은가 제공 [Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation)합니다. 이 구성 요소에서 이식는 [Microsoft.Owin.Security.WsFederation](https://www.nuget.org/packages/Microsoft.Owin.Security.WsFederation) 및 해당 구성 요소의 메커니즘을 많이 공유 합니다. 그러나 구성 요소는 몇 가지 중요 한 방법으로 다.

기본적으로 새 미들웨어:

* 원치 않는 로그인을 허용 하지 않습니다. 이 Ws-federation 프로토콜 기능은 XSRF 공격에 취약 합니다. 그러나으로 사용할 수 있습니다는 `AllowUnsolicitedLogins` 옵션입니다.
* 로그인 메시지에 대 한 모든 폼 게시를 검사 하지 않습니다. 만 요청을 `CallbackPath` 기호 기능에 대 한 검사 `CallbackPath` 기본값으로 `/signin-wsfed` 되지만 변경할 수 있습니다. 이 경로 사용 하 여 다른 인증 공급자와 공유할 수는 `SkipUnrecognizedRequests` 옵션입니다.

## <a name="register-the-app-with-active-directory"></a>Active Directory에 앱 등록

### <a name="active-directory-federation-services"></a>Active Directory Federation Services

* 서버를 열고 **신뢰 당사자 트러스트 추가 마법사** ADFS 관리 콘솔에서:

![신뢰 당사자 트러스트 마법사 추가: 시작](ws-federation/_static/AdfsAddTrust.png)

* 데이터를 수동으로 입력 하려면 선택 합니다.

![데이터 원본을 선택 신뢰 당사자 트러스트 추가 마법사:](ws-federation/_static/AdfsSelectDataSource.png)

* 신뢰 당사자에 대 한 표시 이름을 입력 합니다. 이름이는 ASP.NET Core 응용 프로그램에 중요 하지 않습니다.

* [Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation) 토큰 암호화 인증서를 구성 하지 않으면 하므로 토큰 암호화에 대 한 지원이 부족 합니다.

![인증서를 구성 신뢰 당사자 트러스트 추가 마법사:](ws-federation/_static/AdfsConfigureCert.png)

* 응용 프로그램의 URL을 사용 하 여 Ws-federation 수동 프로토콜 지원을 사용 하도록 설정 합니다. 응용 프로그램에 대 한 올바른 포트를 확인 합니다.

![URL 구성 신뢰 당사자 트러스트 추가 마법사:](ws-federation/_static/AdfsConfigureUrl.png)

> [!NOTE]
> HTTPS URL 이어야 합니다. IIS Express 응용 프로그램을 개발 하는 동안 호스트 하는 경우 자체 서명 된 인증서를 제공할 수 있습니다. Kestrel은 인증서를 수동으로 구성을 해야합니다. 참조는 [Kestrel 설명서](xref:fundamentals/servers/kestrel) 내용을 확인 합니다.

* 클릭 **다음** 마법사의 나머지 부분을 및 **닫기** 끝입니다.

* ASP.NET Core Id 필요는 **이름 ID** 클레임입니다. 추가 된 **클레임 규칙 편집** 대화 상자:

![클레임 규칙 편집](ws-federation/_static/EditClaimRules.png)

* 에 **변환 클레임 규칙 추가 마법사**, 기본값을 그대로 적용 **LDAP 특성을 클레임으로 보내기** 서식 파일을 선택 하 고 클릭 **다음**합니다. 규칙 매핑을 추가 **SAM 계정 이름을** LDAP 특성을는 **이름 ID** 나가는 클레임:

![클레임 규칙 구성 변환 클레임 규칙 추가 마법사:](ws-federation/_static/AddTransformClaimRule.png)

* 클릭 **마침** > **확인** 에 **클레임 규칙 편집** 창.

### <a name="azure-active-directory"></a>Azure Active Directory

* AAD 테 넌 트의 응용 프로그램 등록 블레이드로 이동 합니다. 클릭 **새 응용 프로그램 등록**:

![Azure Active Directory: 응용 프로그램 등록](ws-federation/_static/AadNewAppRegistration.png)

* 앱 등록에 대 한 이름을 입력 합니다. 이 ASP.NET Core 응용 프로그램에 중요 하지 않습니다.
* 로 응용 프로그램에서 수신 대기 하는 URL을 입력에서 **로그온 URL**:

![Azure Active Directory: 응용 프로그램 등록 만들기](ws-federation/_static/AadCreateAppRegistration.png)

* 클릭 **끝점** 확인는 **페더레이션 메타 데이터 문서** URL입니다. 이 Ws-federation 미들웨어 `MetadataAddress`:

![Azure Active Directory: 끝점](ws-federation/_static/AadFederationMetadataDocument.png)

* 새 응용 프로그램 등록으로 이동 합니다. 클릭 **설정** > **속성** 를 기록 하 고는 **앱 ID URI**합니다. 이 Ws-federation 미들웨어 `Wtrealm`:

![Azure Active Directory: 응용 프로그램 등록 속성](ws-federation/_static/AadAppIdUri.png)

## <a name="add-ws-federation-as-an-external-login-provider-for-aspnet-core-identity"></a>WS-페더레이션 ASP.NET Core Id에 대 한 외부 로그인 공급자로 추가

* 대 한 종속성 추가 [Microsoft.AspNetCore.Authentication.WsFederation](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.WsFederation) 프로젝트에 있습니다.
* Ws-federation을 추가 `Configure` 메서드에서 *Startup.cs*:

    ```csharp
    services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

    services.AddAuthentication()
        .AddWsFederation(options =>
        {
            // MetadataAddress represents the Active Directory instance used to authenticate users.
            options.MetadataAddress = "https://<ADFS FQDN or AAD tenant>/FederationMetadata/2007-06/FederationMetadata.xml";

            // Wtrealm is the app's identifier in the Active Directory instance.
            // For ADFS, use the relying party's identifier, its WS-Federation Passive protocol URL:
            options.Wtrealm = "https://localhost:44307/";

            // For AAD, use the App ID URI from the app registration's Properties blade:
            options.Wtrealm = "https://wsfedsample.onmicrosoft.com/bf0e7e6d-056e-4e37-b9a6-2c36797b9f01";
        });

    services.AddMvc()
     // ...
    ```

[!INCLUDE [default settings configuration](social/includes/default-settings.md)]

### <a name="log-in-with-ws-federation"></a>Ws-federation 로그인

응용 프로그램 찾아서 클릭은 **로그인** nav 헤더의 링크입니다. WsFederation으로 로그인 하는 옵션은: ![로그인 페이지](ws-federation/_static/WsFederationButton.png)

Ad FS 로그인 페이지를 리디렉션합니다 단추 공급자로 adfs를: ![ADFS 로그인 페이지](ws-federation/_static/AdfsLoginPage.png)

공급자와 Azure Active Directory와 단추를 AAD에 로그인 페이지로 리디렉션합니다: ![AAD 로그인 페이지](ws-federation/_static/AadSignIn.png)

한 성공적인 로그인에서 새 사용자에 대 한 응용 프로그램의 사용자 등록 페이지를 리디렉션합니다: ![등록 페이지](ws-federation/_static/Register.png)

## <a name="use-ws-federation-without-aspnet-core-identity"></a>ASP.NET Core Identity 없이 Ws-federation을 사용 하 여

WS-페더레이션 미들웨어 Identity 없이 사용할 수 있습니다. 예를 들어:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddAuthentication(sharedOptions =>
    {
        sharedOptions.DefaultScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        sharedOptions.DefaultSignInScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        sharedOptions.DefaultChallengeScheme = WsFederationDefaults.AuthenticationScheme;
    })
    .AddWsFederation(options =>
    {
        options.Wtrealm = Configuration["wsfed:realm"];
        options.MetadataAddress = Configuration["wsfed:metadata"];
    })
    .AddCookie();
}

public void Configure(IApplicationBuilder app)
{
    app.UseAuthentication();
        // …
}
```
