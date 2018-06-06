---
title: ASP.NET Core Id 없이 쿠키 인증을 사용 하 여
author: rick-anderson
description: ASP.NET Core Id 없이 쿠키 인증을 사용 하 여 설명
manager: wpickett
ms.author: riande
ms.date: 10/11/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/cookie
ms.openlocfilehash: f84d69f84cb0b80418bbb6de6bfcd7e2172f65ef
ms.sourcegitcommit: 726ffab258070b4fe6cf950bf030ce10c0c07bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34734616"
---
# <a name="use-cookie-authentication-without-aspnet-core-identity"></a>ASP.NET Core Id 없이 쿠키 인증을 사용 하 여

여 [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Luke Latham](https://github.com/guardrex)

이전 인증 항목에 나와 있는 것 처럼 [ASP.NET Core Id](xref:security/authentication/identity) 만들고 로그인 유지 하기 위한 완전 한 완전 한 기능의 인증 공급자입니다. 그러나 다음 쿠키 기반 인증에 사용자 고유의 사용자 지정 인증 논리를 사용 하는 것이 좋습니다. ASP.NET Core Id 없이 독립 실행형 인증 공급자로 쿠키 기반 인증을 사용할 수 있습니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/cookie/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

샘플 응용 프로그램에서 설명을 위해 Maria Rodriguez 가상의 사용자에 대 한 사용자 계정을 응용 프로그램에 하드 코딩 됩니다. 전자 메일 이름을 사용 하 여 "maria.rodriguez@contoso.com" 및 사용자를 로그인 할 암호입니다. 사용자가 인증 된 `AuthenticateUser` 에서 메서드는 *Pages/Account/Login.cshtml.cs* 파일입니다. 실제 예제에서 데이터베이스에 대해 사용자를 인증 합니다.

ASP.NET Core에서 마이그레이션 쿠키 기반 인증에 대 한 내용은 2.0으로 1.x 참조 [마이그레이션할 인증 및 ASP.NET 코어 2.0 (쿠키 기반 인증) 항목에 Id](xref:migration/1x-to-2x/identity-2x#cookie-based-authentication)합니다.

ASP.NET Core Id를 사용 하려면 참조는 [Id 소개](xref:security/authentication/identity) 항목입니다.

## <a name="configuration"></a>구성

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

응용 프로그램을 사용 하지 않는 경우는 [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app)에 대 한 프로젝트 파일에서 패키지 참조를 만들는 [Microsoft.AspNetCore.Authentication.Cookies](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Cookies/) 패키지 (2.1.0 버전 또는 나중에).

에 `ConfigureServices` 메서드를 사용 하 여 인증 미들웨어 서비스 만들기는 `AddAuthentication` 및 `AddCookie` 메서드:

[!code-csharp[](cookie/samples/2.x/CookieSample/Startup.cs?name=snippet1)]

`AuthenticationScheme` 에 전달 된 `AddAuthentication` 응용 프로그램에 대 한 기본 인증 체계를 설정 합니다. `AuthenticationScheme` 쿠키 인증의 여러 인스턴스가 있고 하려는 경우 유용 [특정 스키마를 가진 권한 부여](xref:security/authorization/limitingidentitybyscheme)합니다. 설정의 `AuthenticationScheme` 를 `CookieAuthenticationDefaults.AuthenticationScheme` 체계 "쿠키"의 값을 제공 합니다. 체계를 구별 하는 임의의 문자열 값을 제공할 수 있습니다.

에 `Configure` 메서드를 사용 하 여는 `UseAuthentication` 설정 하는 인증 미들웨어를 호출 하는 메서드는 `HttpContext.User` 속성입니다. 호출 된 `UseAuthentication` 메서드 호출 하기 전에 `UseMvcWithDefaultRoute` 또는 `UseMvc`:

[!code-csharp[](cookie/samples/2.x/CookieSample/Startup.cs?name=snippet2)]

**AddCookie 옵션**

[CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions?view=aspnetcore-2.0) 클래스는 인증 공급자 옵션을 구성 하는 데 사용 됩니다.

| 옵션 | 설명 |
| ------ | ----------- |
| [AccessDeniedPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.accessdeniedpath?view=aspnetcore-2.0) | 302 있음 (URL 리디렉션)와 제공에 대 한 경로 제공 하 여 트리거되면 `HttpContext.ForbidAsync`합니다. 기본값은 `/Account/AccessDenied`입니다. |
| [ClaimsIssuer](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions.claimsissuer?view=aspnetcore-2.0) | 에 사용할 발급자는 [발급자](/dotnet/api/system.security.claims.claim.issuer) 쿠키 인증 서비스에 의해 만들어진 모든 클레임에 대 한 속성입니다. |
| [Cookie.Domain](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.domain?view=aspnetcore-2.0) | 쿠키 처리 되는 도메인 이름입니다. 기본적으로 요청 호스트 이름입니다. 브라우저 쿠키 요청에서 일치 하는 호스트 이름에만 보냅니다. 이 도메인의 모든 호스트에 사용할 수 있는 쿠키를 조정할 수도 있습니다. 예를 들어 쿠키 도메인 설정 `.contoso.com` 를 사용할 수 있도록 `contoso.com`, `www.contoso.com`, 및 `staging.www.contoso.com`합니다. |
| [Cookie.Expiration](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.expiration?view=aspnetcore-2.0) | 쿠키의 수명을 가져오거나 설정 합니다. 현재 아니요 ops 옵션이 고 ASP.NET Core 2.1에서 사용 되지 않는 됩니다. 사용 하 여 `ExpireTimeSpan` 쿠키 만료를 설정 하는 옵션입니다. 자세한 내용은 참조 [CookieAuthenticationOptions.Cookie.Expiration의 동작을 명확 하 게](https://github.com/aspnet/Security/issues/1293)합니다. |
| [Cookie.HttpOnly](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.httponly?view=aspnetcore-2.0) | 쿠키를 서버에만 액세스할 수 있어야 하는 경우를 나타내는 플래그입니다. 이 값을 변경 `false` 쿠키에 액세스 하는 클라이언트 쪽 스크립트를 허용 하 고 표시 하며 열림 앱이 쿠키 도용 앱 있어야는 [교차 사이트 스크립팅 (XSS)](xref:security/cross-site-scripting) 취약점입니다. 기본값은 `true`입니다. |
| [Cookie.Name](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.name?view=aspnetcore-2.0) | 쿠키의 이름을 설정합니다. |
| [Cookie.Path](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.path?view=aspnetcore-2.0) | 동일한 호스트 이름에서 실행 되는 앱을 격리 하는 데 사용 합니다. 실행 중인 앱이 있는 경우 `/app1` 및 해당 응용 프로그램에 쿠키를 제한 하려면 설정는 `CookiePath` 속성을 `/app1`합니다. 이러한 작업을 통해 쿠키는 에서만 사용할 수에 대 한 요청 `/app1` 아래에 있는 모든 응용 프로그램 및입니다. |
| [Cookie.SameSite](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.samesite?view=aspnetcore-2.0) | 브라우저에서 동일한 사이트 요청에 연결 될 쿠키를 허용 하는지 여부를 나타냅니다 (`SameSiteMode.Strict`) 또는 안전 HTTP 메서드와 같은 사이트 요청을 사용 하 여 교차 사이트 요청 (`SameSiteMode.Lax`). 로 설정 하면 `SameSiteMode.None`, 쿠키 헤더 값이 설정 되어 있지 않습니다. [쿠키 정책 미들웨어](#cookie-policy-middleware) 제공 하는 값을 덮어쓸 수 있습니다. 기본값은 OAuth 인증을 지원 하려면 `SameSiteMode.Lax`합니다. 자세한 내용은 참조 [SameSite 쿠키 정책으로 인해 분할 하는 OAuth 인증](https://github.com/aspnet/Security/issues/1231)합니다. |
| [Cookie.SecurePolicy](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.securepolicy?view=aspnetcore-2.0) | 만든 쿠키를 HTTPS로 제한 해야 하는 경우를 나타내는 플래그 (`CookieSecurePolicy.Always`), HTTP 또는 HTTPS (`CookieSecurePolicy.None`), 또는 요청와 동일한 프로토콜 (`CookieSecurePolicy.SameAsRequest`). 기본값은 `CookieSecurePolicy.SameAsRequest`입니다. |
| [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.dataprotectionprovider?view=aspnetcore-2.0) | 설정의 `DataProtectionProvider` 기본값을 만드는 데 사용 되는 `TicketDataFormat`합니다. 경우는 `TicketDataFormat` 속성이 설정 되어는 `DataProtectionProvider` 옵션 사용 되지 않습니다. 을 지정 하지 않으면 응용 프로그램의 기본 데이터 보호 공급자가 사용 됩니다. |
| [이벤트](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.events?view=aspnetcore-2.0) | 특정 처리 시점에서 앱 제어를 제공 하는 공급자에서 메서드를 호출 하는 처리기. 경우 `Events` 는 메서드를 호출할 때 아무 작업도 수행 하는 기본 인스턴스가 제공이 제공 되지 않습니다. |
| [EventsType](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions.eventstype?view=aspnetcore-2.0) | 서비스 유형으로 가져오는 데 사용 된 `Events` 속성 대신 인스턴스. |
| [ExpireTimeSpan](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.expiretimespan?view=aspnetcore-2.0) | `TimeSpan` 쿠키 내부에 저장 된 인증 티켓이 만료 된 이후입니다. `ExpireTimeSpan` 티켓에 대 한 만료 시간을 생성 하는 현재 시간에 추가 됩니다. `ExpiredTimeSpan` 항상 서버에 의해 확인 된 암호화 된 AuthTicket 값에 들어갑니다. 에 들어갈 수 있습니다는 [Set-cookie](https://tools.ietf.org/html/rfc6265#section-4.1) 헤더가 없지만 경우에만 `IsPersistent` 설정 됩니다. 설정 하려면 `IsPersistent` 를 `true`, 구성에서 [AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.authentication.authenticationproperties) 에 전달 된 `SignInAsync`합니다. 기본값 `ExpireTimeSpan` 14 일입니다. |
| [LoginPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.loginpath?view=aspnetcore-2.0) | 302 있음 (URL 리디렉션)와 제공에 대 한 경로 제공 하 여 트리거되면 `HttpContext.ChallengeAsync`합니다. 생성 된 401는 현재 URL에 추가 되며는 `LoginPath` 의해 명명 된 쿼리 문자열 매개 변수로 `ReturnUrlParameter`합니다. 요청을 한 번의 `LoginPath` 부여 된 새 로그인 id는 `ReturnUrlParameter` 값 브라우저 원래 권한이 없음된 상태 코드를 발생 시킨 URL로 다시 리디렉션하는 데 사용 됩니다. 기본값은 `/Account/Login`입니다. |
| [LogoutPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.logoutpath?view=aspnetcore-2.0) | 경우는 `LogoutPath` 해당 경로에 대 한 요청을 리디렉션합니다 처리기에 제공 된 값에 따라는 `ReturnUrlParameter`합니다. 기본값은 `/Account/Logout`입니다. |
| [ReturnUrlParameter](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.returnurlparameter?view=aspnetcore-2.0) | 302 (URL 리디렉션) Found 응답에 대 한 처리기가 추가 되는 쿼리 문자열 매개 변수의 이름을 결정 합니다. `ReturnUrlParameter` 에 요청이 도착할 때 사용 되는 `LoginPath` 또는 `LogoutPath` 로그인 또는 로그 아웃 작업을 수행한 후 원래 URL로 브라우저 돌아갑니다. 기본값은 `ReturnUrl`입니다. |
| [SessionStore](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.sessionstore?view=aspnetcore-2.0) | 요청 간에 id를 저장 하는 데 사용 하는 선택적 컨테이너입니다. 을 사용 하는 세션 식별자만 클라이언트로 전송 됩니다. `SessionStore` 큰 id와 잠재적 문제를 완화 하기 위해 사용할 수 있습니다. |
| [SlidingExpiration](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.slidingexpiration?view=aspnetcore-2.0) | 업데이트 된 만료 시간이 새 쿠키를 동적으로 발급 해야 하는 경우를 나타내는 플래그입니다. 이 현재 쿠키 만료 기간 50% 이상의 만료 된 모든 요청에서 발생할 수 있습니다. 새로운 만료 날짜로 앞으로 이동 하는 현재 날짜와 `ExpireTimespan`합니다. [절대 쿠키 만료 시간](xref:security/authentication/cookie#absolute-cookie-expiration) 를 사용 하 여 설정할 수는 `AuthenticationProperties` 클래스를 호출할 때 `SignInAsync`합니다. 절대 만료 시간 인증 쿠키가 유효 하다는 시간의 양을 제한 하 여 응용 프로그램의 보안을 향상 시킬 수 있습니다. 기본값은 `true`입니다. |
| [TicketDataFormat](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.ticketdataformat?view=aspnetcore-2.0) | `TicketDataFormat` 보호 및 id 및 쿠키 값에 저장 되어 있는 기타 속성을 보호 해제 하는 데 사용 됩니다. 을 지정 하지 않으면는 `TicketDataFormat` 사용 하 여 만들어집니다는 [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.dataprotectionprovider?view=aspnetcore-2.0)합니다. |
| [유효성 검사](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions.validate?view=aspnetcore-2.0) | 옵션은 유효한 지 확인 하는 메서드. |

설정 `CookieAuthenticationOptions` 에서 인증을 위해 서비스 구성에는 `ConfigureServices` 메서드:

```csharp
services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
    .AddCookie(options =>
    {
        ...
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

ASP.NET Core 1.x 사용 하 여 쿠키 [미들웨어](xref:fundamentals/middleware/index) 암호화 된 쿠키에 사용자 계정을 serialize 하는 합니다. 이후 요청에서 쿠키의 유효성이 확인 되 고 주 서버는 다시에 할당 된 `HttpContext.User` 속성입니다.

설치는 [Microsoft.AspNetCore.Authentication.Cookies](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Cookies/) 프로젝트에서 NuGet 패키지 합니다. 이 패키지는 쿠키 미들웨어를 포함 합니다.

사용 하 여는 `UseCookieAuthentication` 에서 메서드는 `Configure` 메서드에서 프로그램 *Startup.cs* 하기 전에 파일 `UseMvc` 또는 `UseMvcWithDefaultRoute`:

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions()
{
    AccessDeniedPath = "/Account/Forbidden/",
    AuthenticationScheme = CookieAuthenticationDefaults.AuthenticationScheme,
    AutomaticAuthenticate = true,
    AutomaticChallenge = true,
    LoginPath = "/Account/Unauthorized/"
});
```

**CookieAuthenticationOptions 옵션**

[CookieAuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.CookieAuthenticationOptions?view=aspnetcore-1.1) 클래스는 인증 공급자 옵션을 구성 하는 데 사용 됩니다.

| 옵션 | 설명 |
| ------ | ----------- |
| [AuthenticationScheme](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.authenticationscheme?view=aspnetcore-1.1) | 인증 체계를 설정합니다. `AuthenticationScheme` 인증의 여러 인스턴스가 있는 하려는 경우 유용 [특정 스키마를 가진 권한 부여](xref:security/authorization/limitingidentitybyscheme)합니다. 설정의 `AuthenticationScheme` 를 `CookieAuthenticationDefaults.AuthenticationScheme` 체계 "쿠키"의 값을 제공 합니다. 체계를 구별 하는 임의의 문자열 값을 제공할 수 있습니다. |
| [AutomaticAuthenticate](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.automaticauthenticate?view=aspnetcore-1.1) | 쿠키 인증 모든 요청에 대해 실행 및 유효성 검사 하 고 자신이 만든 직렬화 된 모든 보안 주체를 재구성 있는지를 나타내는 값을 설정 합니다. |
| [AutomaticChallenge](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.automaticchallenge?view=aspnetcore-1.1) | True 이면 인증 미들웨어 자동 문제를 처리 합니다. 경우 false 이면 인증 미들웨어만 변경 하 여 명시적으로 지정 하는 경우 응답은 `AuthenticationScheme`합니다. |
| [ClaimsIssuer](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.claimsissuer?view=aspnetcore-1.1) | 에 사용할 발급자는 [발급자](/dotnet/api/system.security.claims.claim.issuer) 쿠키 인증 미들웨어에서 만든 클레임의 속성입니다. |
| [CookieDomain](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiedomain?view=aspnetcore-1.1) | 쿠키 처리 되는 도메인 이름입니다. 기본적으로 요청 호스트 이름입니다. 브라우저 쿠키를 일치 하는 호스트 이름으로 처리합니다. 이 도메인의 모든 호스트에 사용할 수 있는 쿠키를 조정할 수도 있습니다. 예를 들어 쿠키 도메인 설정 `.contoso.com` 를 사용할 수 있도록 `contoso.com`, `www.contoso.com`, 및 `staging.www.contoso.com`합니다. |
| [CookieHttpOnly](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiehttponly?view=aspnetcore-1.1) | 쿠키를 서버에만 액세스할 수 있어야 하는 경우를 나타내는 플래그입니다. 이 값을 변경 `false` 쿠키에 액세스 하는 클라이언트 쪽 스크립트를 허용 하 고 표시 하며 열림 앱이 쿠키 도용 앱 있어야는 [교차 사이트 스크립팅 (XSS)](xref:security/cross-site-scripting) 취약점입니다. 기본값은 `true`입니다. |
| [CookiePath](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiepath?view=aspnetcore-1.1) | 동일한 호스트 이름에서 실행 되는 앱을 격리 하는 데 사용 합니다. 실행 중인 앱이 있는 경우 `/app1` 및 해당 응용 프로그램에 쿠키를 제한 하려면 설정는 `CookiePath` 속성을 `/app1`합니다. 이러한 작업을 통해 쿠키는 에서만 사용할 수에 대 한 요청 `/app1` 아래에 있는 모든 응용 프로그램 및입니다. |
| [CookieSecure](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiesecure?view=aspnetcore-1.1) | 만든 쿠키를 HTTPS로 제한 해야 하는 경우를 나타내는 플래그 (`CookieSecurePolicy.Always`), HTTP 또는 HTTPS (`CookieSecurePolicy.None`), 또는 요청와 동일한 프로토콜 (`CookieSecurePolicy.SameAsRequest`). 기본값은 `CookieSecurePolicy.SameAsRequest`입니다. |
| [설명](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.description?view=aspnetcore-1.1) | 응용 프로그램에 사용할 수 있는 인증 형식에 대 한 추가 정보입니다. |
| [ExpireTimeSpan](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.expiretimespan?view=aspnetcore-1.1) | `TimeSpan` 인증 티켓이 만료 된 이후입니다. 티켓에 대 한 만료 시간을 생성 하는 현재 시간에 추가 됩니다. 사용 하도록 `ExpireTimeSpan`, 설정 해야 `IsPersistent` 를 `true` 에 `AuthenticationProperties` 에 전달 된 `SignInAsync`합니다. 기본값은 14 일입니다. |
| [SlidingExpiration](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.slidingexpiration?view=aspnetcore-1.1) | 이상의 절반 쿠키 만료 날짜를 다시 설정 하는지 여부를 나타내는 플래그는 `ExpireTimeSpan` 관리가 합니다. 새 exipiration 시간 앞으로 이동 하는 현재 날짜와 `ExpireTimespan`합니다. [절대 쿠키 만료 시간](xref:security/authentication/cookie#absolute-cookie-expiration) 를 사용 하 여 설정할 수는 `AuthenticationProperties` 클래스를 호출할 때 `SignInAsync`합니다. 절대 만료 시간 인증 쿠키가 유효 하다는 시간의 양을 제한 하 여 응용 프로그램의 보안을 향상 시킬 수 있습니다. 기본값은 `true`입니다. |

설정 `CookieAuthenticationOptions` 에서 쿠키 인증 미들웨어에 대 한는 `Configure` 메서드:

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    ...
});
```

---

## <a name="cookie-policy-middleware"></a>쿠키 정책 미들웨어입니다.

[쿠키 정책 미들웨어](/dotnet/api/microsoft.aspnetcore.cookiepolicy.cookiepolicymiddleware) 응용 프로그램의 쿠키 정책 기능을 사용할 수 있습니다. 중요 한; 순서는 응용 프로그램 처리 파이프라인에 미들웨어를 추가 또한 파이프라인에서 그 뒤에 등록 된 구성 요소를만 영향을 줍니다.

```csharp
app.UseCookiePolicy(cookiePolicyOptions);
```

 [CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions) 쿠키 정책 미들웨어에 제공 된 쿠키를 추가 하거나 삭제할 때 쿠키 처리 처리기에 쿠키 처리 및 후크의 전역 특성을 제어할 수 있습니다.

| 속성 | 설명 |
| -------- | ----------- |
| [HttpOnly](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.httponly) | 쿠키 HttpOnly 이어야 하는 여부를 나타내는 플래그 쿠키 서버에만 액세스할 수 있어야 하는 경우 영향을 줍니다. 기본값은 `HttpOnlyPolicy.None`입니다. |
| [MinimumSameSitePolicy](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.minimumsamesitepolicy) | 쿠키의 동일한 사이트 특성을 (아래 참조)에 영향을 줍니다. 기본값은 `SameSiteMode.Lax`입니다. 이 옵션은 ASP.NET Core 2.0 이상에 사용할 수 있습니다. |
| [OnAppendCookie](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.onappendcookie) | 에 쿠키를 추가 하는 경우 호출 됩니다. |
| [OnDeleteCookie](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.ondeletecookie) | 쿠키가 삭제 되 면 호출 됩니다. |
| [보안](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.secure) | 쿠키도 Secure 해야 하는지 여부를 영향을 줍니다. 기본값은 `CookieSecurePolicy.None`입니다. |

**MinimumSameSitePolicy** (ASP.NET 코어 2.0 +만)

기본 `MinimumSameSitePolicy` 값은 `SameSiteMode.Lax` OAuth2 인증을 허용 하도록 합니다. 엄격 하 게 하는 동일한 사이트 정책을 적용 하려면 `SameSiteMode.Strict`로 설정 된 `MinimumSameSitePolicy`합니다. 이 설정은 나누기 OAuth2 및 다른 크로스-원본 인증 체계, 하지만 다른 유형의 크로스-원본 요청을 처리 하지 않아도 되는 앱에 대 한 쿠키 보안 수준을 승격 시킵니다.

```csharp
var cookiePolicyOptions = new CookiePolicyOptions
{
    MinimumSameSitePolicy = SameSiteMode.Strict,
};
```

에 대 한 쿠키 정책 미들웨어 설정 `MinimumSameSitePolicy` 의 설정에 영향을 줄 수 `Cookie.SameSite` 에 `CookieAuthenticationOptions` 아래 표를 참조에 따라 설정 합니다.

| MinimumSameSitePolicy | Cookie.SameSite | 결과 Cookie.SameSite 설정 |
| --------------------- | --------------- | --------------------------------- |
| SameSiteMode.None     | SameSiteMode.None<br>SameSiteMode.Lax<br>SameSiteMode.Strict | SameSiteMode.None<br>SameSiteMode.Lax<br>SameSiteMode.Strict |
| SameSiteMode.Lax      | SameSiteMode.None<br>SameSiteMode.Lax<br>SameSiteMode.Strict | SameSiteMode.Lax<br>SameSiteMode.Lax<br>SameSiteMode.Strict |
| SameSiteMode.Strict   | SameSiteMode.None<br>SameSiteMode.Lax<br>SameSiteMode.Strict | SameSiteMode.Strict<br>SameSiteMode.Strict<br>SameSiteMode.Strict |

## <a name="create-an-authentication-cookie"></a>인증 쿠키를 만드는

사용자 정보를 보관 하는 쿠키를 만들려면 먼저 생성 해야는 [ClaimsPrincipal](/dotnet/api/system.security.claims.claimsprincipal)합니다. 사용자 정보 직렬화 되며 쿠키에 저장 됩니다. 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

만들기는 [ClaimsIdentity](/dotnet/api/system.security.claims.claimsidentity) 와 모든 필수 [클레임](/dotnet/api/system.security.claims.claim)s 및 호출 [SignInAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signinasync?view=aspnetcore-2.0) 사용자 로그인:

[!code-csharp[](cookie/samples/2.x/CookieSample/Pages/Account/Login.cshtml.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

호출 [SignInAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1.signinasync?view=aspnetcore-1.1) 사용자에 로그인 합니다.

```csharp
await HttpContext.Authentication.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity));
```

---

`SignInAsync` 암호화 된 쿠키를 만들어 현재 응답에 추가 합니다. 지정 하지 않으면 프로그램 `AuthenticationScheme`, 기본 체계를 사용 합니다.

내부적으로 사용 되는 암호화는 ASP.NET Core [데이터 보호](xref:security/data-protection/using-data-protection#security-data-protection-getting-started) 시스템입니다. 여러 컴퓨터, 앱, 부하 분산 또는 웹 팜을 사용 하 여 응용 프로그램을 호스트 하 고 있는 경우 다음을 수행 해야 [데이터 보호를 구성](xref:security/data-protection/configuration/overview) 동일한 키 링과 응용 프로그램 식별자를 사용 하도록 합니다.

## <a name="sign-out"></a>로그아웃

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

로그 아웃 현재 사용자를 해당 쿠키를 삭제 하려면 호출 [SignOutAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signoutasync?view=aspnetcore-2.0):

[!code-csharp[](cookie/samples/2.x/CookieSample/Pages/Account/Login.cshtml.cs?name=snippet2)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

로그 아웃 현재 사용자를 해당 쿠키를 삭제 하려면 호출 [SignOutAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1.signoutasync?view=aspnetcore-1.1):

```csharp
await HttpContext.Authentication.SignOutAsync(
    CookieAuthenticationDefaults.AuthenticationScheme);
```

---

사용 하지 않으려면 `CookieAuthenticationDefaults.AuthenticationScheme` (또는 "쿠키")의 체계 (예: "ContosoCookie")로 인증 공급자를 구성할 때 사용 하는 체계를 제공 합니다. 그렇지 않은 경우 기본 구성표가 사용 됩니다.

## <a name="react-to-back-end-changes"></a>백 엔드 변경 내용에 대응

쿠키를 만든 후에 id의 단일 원본이 됩니다. 백 엔드 시스템에 사용자를 비활성화 하는 경우에 쿠키 인증 시스템에이 알지 및 해당 쿠키의 유효으로 사용자 로그인 유지 합니다.

[ValidatePrincipal](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationevents.validateprincipal) 에서 ASP.NET Core 이벤트 2.x 또는 [ValidateAsync](/dotnet/api/microsoft.aspnetcore.identity.isecuritystampvalidator.validateasync?view=aspnetcore-1.1) 메서드에서 ASP.NET Core 1.x를 가로채 고 쿠키 id의 유효성 검사 재정의에 사용할 수 있습니다. 이 방법은 응용 프로그램에 액세스 하는 해지 된 사용자의 위험을 완화 합니다.

한 가지 방법은 쿠키 유효성 검사를 기반으로 사용자 데이터베이스 변경 된 경우에 추적 합니다. 데이터베이스 사용자의 쿠키에 발급 된 이후 변경 되지 않은 경우에 사용자를 해당 쿠키가 여전히 유효한 경우 다시 인증 필요가 없습니다. 이 시나리오에서 구현 되는 데이터베이스를 구현 하려면 `IUserRepository` 이 예제에서는 저장 한 `LastChanged` 값입니다. 모든 사용자는 데이터베이스에서 업데이트 될 때의 `LastChanged` 값이 현재 시간으로 설정 합니다.

데이터베이스 변경 내용을 기반으로 하는 경우 쿠키를 무효화 하기 위해는 `LastChanged` 값, 쿠키와 만들기는 `LastChanged` 현재 포함 된 클레임 `LastChanged` 데이터베이스에서 값:

```csharp
var claims = new List<Claim>
{
    new Claim(ClaimTypes.Name, user.Email),
    new Claim("LastChanged", {Database Value})
};

var claimsIdentity = new ClaimsIdentity(
    claims, 
    CookieAuthenticationDefaults.AuthenticationScheme);

await HttpContext.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme, 
    new ClaimsPrincipal(claimsIdentity));
```

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

에 대 한 재정의 구현 하는 `ValidatePrincipal` 이벤트, 메서드에서 파생 되는 클래스에 다음 서명 사용 하 여 쓰기 [CookieAuthenticationEvents](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationevents):

```csharp
ValidatePrincipal(CookieValidatePrincipalContext)
```

예제는 다음과 같습니다.

```csharp
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Authentication;
using Microsoft.AspNetCore.Authentication.Cookies;

public class CustomCookieAuthenticationEvents : CookieAuthenticationEvents
{
    private readonly IUserRepository _userRepository;

    public CustomCookieAuthenticationEvents(IUserRepository userRepository)
    {
        // Get the database from registered DI services.
        _userRepository = userRepository;
    }

    public override async Task ValidatePrincipal(CookieValidatePrincipalContext context)
    {
        var userPrincipal = context.Principal;

        // Look for the LastChanged claim.
        var lastChanged = (from c in userPrincipal.Claims
                           where c.Type == "LastChanged"
                           select c.Value).FirstOrDefault();

        if (string.IsNullOrEmpty(lastChanged) ||
            !_userRepository.ValidateLastChanged(lastChanged))
        {
            context.RejectPrincipal();

            await context.HttpContext.SignOutAsync(
                CookieAuthenticationDefaults.AuthenticationScheme);
        }
    }
}
```

쿠키 service 등록 하는 동안 이벤트 인스턴스를 등록 된 `ConfigureServices` 메서드. 에 대 한 범위 지정 된 서비스 등록을 제공 하면 `CustomCookieAuthenticationEvents` 클래스:

```csharp
services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
    .AddCookie(options =>
    {
        options.EventsType = typeof(CustomCookieAuthenticationEvents);
    });

services.AddScoped<CustomCookieAuthenticationEvents>();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

에 대 한 재정의 구현 하는 `ValidateAsync` 이벤트, 메서드는 다음 서명 가진 쓰기:

```csharp
ValidateAsync(CookieValidatePrincipalContext)
```

ASP.NET Core Id의 일부로이 검사를 구현 하는 [SecurityStampValidator](/dotnet/api/microsoft.aspnetcore.identity.securitystampvalidator-1.validateasync)합니다. 예제는 다음과 같습니다.

```csharp
public static class LastChangedValidator
{
    public static async Task ValidateAsync(CookieValidatePrincipalContext context)
    {
        // Pull database from registered DI services.
        var userRepository = 
            context.HttpContext.RequestServices
                .GetRequiredService<IUserRepository>();
        var userPrincipal = context.Principal;

        // Look for the last changed claim.
        var lastChanged = (from c in userPrincipal.Claims
                           where c.Type == "LastChanged"
                           select c.Value).FirstOrDefault();

        if (string.IsNullOrEmpty(lastChanged) ||
            !userRepository.ValidateLastChanged(lastChanged))
        {
            context.RejectPrincipal();

            await context.HttpContext.SignOutAsync(
                CookieAuthenticationDefaults.AuthenticationScheme);
        }
    }
}
```

쿠키 인증 구성 중 이벤트를 등록 된 `Configure` 메서드:

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    Events = new CookieAuthenticationEvents
    {
        OnValidatePrincipal = LastChangedValidator.ValidateAsync
    }
});
```

---

사용자의 이름이 업데이트 되는 상황을 생각해 봅시다 &mdash; 주는 작업에 어떤 방식으로든에서 보안에 영향을 주지 않습니다. 안전 하 게 사용자 계정이 업데이트 하려는 경우에 호출 `context.ReplacePrincipal` 설정 하 고는 `context.ShouldRenew` 속성을 `true`합니다.

> [!WARNING]
> 여기에서 설명 하는 방식은 모든 요청에 대해 발생 합니다. 이 앱에 대 한 성능이 크게 저하 될 수 있습니다.

## <a name="persistent-cookies"></a>영구 쿠키

쿠키 브라우저 세션 전체에서 유지 하도록 할 수 있습니다. 로그인 또는 유사한 메커니즘에서 "암호 저장" 확인란을 사용 하 여 명시적 사용자 동의와만이 지 속성을 설정 해야 합니다. 

다음 코드 조각 id 및 브라우저 클로저를 통해 되더라도 남아 있지만 해당 쿠키를 만듭니다. 이전에 구성 된 모든 상대 (sliding) 만료 설정은 적용 됩니다. 쿠키는 브라우저 종료 하는 동안 만료 되 면 다시 시작 되 면 브라우저 쿠키를 지웁니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
await HttpContext.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity),
    new AuthenticationProperties
    {
        IsPersistent = true
    });
```

[AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.authentication.authenticationproperties?view=aspnetcore-2.0) 에 위치 하는 클래스는 `Microsoft.AspNetCore.Authentication` 네임 스페이스입니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
await HttpContext.Authentication.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity),
    new AuthenticationProperties
    {
        IsPersistent = true
    });
```

[AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.http.authentication.authenticationproperties?view=aspnetcore-1.1) 에 위치 하는 클래스는 `Microsoft.AspNetCore.Http.Authentication` 네임 스페이스입니다.

---

## <a name="absolute-cookie-expiration"></a>절대 쿠키 만료 기한

와 절대 만료 시간을 설정할 수 있습니다 `ExpiresUtc`합니다. 설정 해야 `IsPersistent`, 그렇지 않으면 `ExpiresUtc` 는 무시 됩니다 단일 세션 쿠키를 생성 됩니다. 때 `ExpiresUtc` 에 설정 된 `SignInAsync`의 값이 재정의 `ExpireTimeSpan` 옵션의 `CookieAuthenticationOptions`경우 설정 합니다.

다음 코드 조각 id 및는 20 분 동안 지속 되는 해당 쿠키를 만듭니다. 이 이전에 구성 된 모든 상대 (sliding) 만료 설정을 무시 합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
await HttpContext.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity),
    new AuthenticationProperties
    {
        IsPersistent = true,
        ExpiresUtc = DateTime.UtcNow.AddMinutes(20)
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```csharp
await HttpContext.Authentication.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity),
    new AuthenticationProperties
    {
        IsPersistent = true,
        ExpiresUtc = DateTime.UtcNow.AddMinutes(20)
    });
```

---

## <a name="additional-resources"></a>추가 자료

* [Auth 2.0 변경 / 마이그레이션 알림](https://github.com/aspnet/Announcements/issues/262)
* [구성표로 ID 제한](xref:security/authorization/limitingidentitybyscheme)
* [클레임 기반 권한 부여](xref:security/authorization/claims)
* [정책 기반 역할 검사](xref:security/authorization/roles#policy-based-role-checks)
