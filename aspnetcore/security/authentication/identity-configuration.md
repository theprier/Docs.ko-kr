---
title: Configure ASP.NET Core Identity
author: AdrienTorris
description: "ASP.NET Core Id 기본값을 이해 하 고 사용자 지정 값을 사용 하도록 Id 속성을 구성 하는 방법에 알아봅니다."
manager: wpickett
ms.author: scaddie
ms.date: 03/06/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/identity-configuration
ms.openlocfilehash: 469068af2fc12627a0a5d1c5623eb60bef51cea0
ms.sourcegitcommit: 53ee14b9c8200f44705d8997c3619fa874192d45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="configure-identity"></a>Id 구성

ASP.NET Core Identity 쿠키 설정, 암호 정책 및 잠금 시간 등의 설정에 대 한 기본 구성을 사용합니다. 이러한 설정은 응용 프로그램에서 재정의할 수 있습니다 `Startup` 클래스입니다.

## <a name="identity-options"></a>Id 옵션

[IdentityOptions](/dotnet/api/microsoft.aspnetcore.identity.identityoptions) 클래스 Id 시스템을 구성 하는 데 사용할 수 있는 옵션을 나타냅니다.

### <a name="claims-identity"></a>클레임 Id

[IdentityOptions.ClaimsIdentity](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.claimsidentity) 지정는 [ClaimsIdentityOptions](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions) 표에 표시 된 속성을 사용 합니다.

| 속성 | 설명 | 기본 |
| -------- | ----------- | :-----: |
| [RoleClaimType](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions.roleclaimtype) | 클레임 유형이 역할 클레임에 대 한 사용을 가져오거나 설정 합니다. | [ClaimTypes.Role](/dotnet/api/system.security.claims.claimtypes.role) |
| [SecurityStampClaimType](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions.securitystampclaimtype) | 보안 스탬프 클레임에 사용 되는 클레임 형식을 가져오거나 설정 합니다. | `AspNet.Identity.SecurityStamp` |
| [UserIdClaimType](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions.useridclaimtype) | 사용자 식별자 클레임에 사용 되는 클레임 형식을 가져오거나 설정 합니다. | [ClaimTypes.NameIdentifier](/dotnet/api/system.security.claims.claimtypes.nameidentifier) |
| [UserNameClaimType](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions.usernameclaimtype) | 사용자 이름 클레임에 사용 되는 클레임 형식을 가져오거나 설정 합니다. | [ClaimTypes.Name](/dotnet/api/system.security.claims.claimtypes.name) |

### <a name="lockout"></a>잠금

[!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,39-42,50-52)]

[IdentityOptions.Lockout](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.lockout) 지정는 [LockoutOptions](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions) 표에 표시 된 속성을 사용 합니다.

| 속성 | 설명 | 기본 |
| -------- | ----------- | :-----: |
| [AllowedForNewUsers](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.allowedfornewusers) | 하는 경우 새 사용자를 잠글 수를 결정 합니다. | `true` |
| [DefaultLockoutTimeSpan](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan) | 시간의 양은 사용자가 잠겨 잠금이 발생 합니다. | 5 분 |
| [MaxFailedAccessAttempts](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts) | 실패 한 액세스 시도 사용자가 잠겨 될 때까지 잠금이 설정 된 경우. | 5 |

### <a name="password"></a>암호

기본적으로 Id는 암호에 대문자, 소문자, 숫자 및 영숫자가 아닌 문자를 포함 필요 합니다. 암호는 최소 6 자 여야 합니다. [PasswordOptions](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions) 에서 변경할 수 있습니다 `Startup.ConfigureServices`합니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

ASP.NET Core 추가 2.0는 [RequiredUniqueChars](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requireduniquechars) 속성입니다. 그렇지 않으면 옵션은 ASP.NET Core 동일 1.x 합니다.

[!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-37,50-52)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[!code-csharp[](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-65,84)]

---

[IdentityOptions.Password](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.password) 지정는 [PasswordOptions](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions) 표에 표시 된 속성을 사용 합니다.

| 속성 | 설명 | 기본 |
| -------- | ----------- | :-----: |
| [RequireDigit](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requiredigit) | 암호에 0-9 사이의 숫자를 여야 합니다. | `true` |
| [RequiredLength](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requiredlength) | 암호의 최소 길이입니다. | 6 |
| [RequiredUniqueChars](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requireduniquechars) | ASP.NET Core 2.0 이상에 적용 됩니다.<br><br> 암호에 고유한 문자 수가 필요합니다. | 1 |
| [RequireLowercase](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requirelowercase) | 암호에 소문자가 필요합니다. | `true` |
| [RequireNonAlphanumeric](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requirenonalphanumeric) | 암호에 영숫자가 아닌 문자가 필요합니다. | `true` |
| [RequireUppercase](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requireuppercase) | 암호에 대문자가 필요합니다. | `true` |

### <a name="sign-in"></a>로그인

[!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,44-46,50-52)]

[IdentityOptions.SignIn](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.signin) 지정는 [SignInOptions](/dotnet/api/microsoft.aspnetcore.identity.signinoptions) 표에 표시 된 속성을 사용 합니다.

| 속성 | 설명 | 기본 |
| -------- | ----------- | :-----: |
| [RequireConfirmedEmail](/dotnet/api/microsoft.aspnetcore.identity.signinoptions.requireconfirmedemail) | 확인 된 전자 메일에 로그인 할 필요 합니다. | `false` |
| [RequireConfirmedPhoneNumber](/dotnet/api/microsoft.aspnetcore.identity.signinoptions.requireconfirmedphonenumber) | 로그인에 확인 된 전화 번호가 필요 합니다. | `false` |

### <a name="tokens"></a>토큰

[IdentityOptions.Tokens](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.tokens) 지정는 [TokenOptions](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions) 표에 표시 된 속성을 사용 합니다.

| 속성 | 설명 |
| -------- | ----------- |
| [AuthenticatorTokenProvider](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.authenticatortokenprovider) | 가져오거나는 `AuthenticatorTokenProvider` 인증자와 함께 다단계 로그인의 유효성을 검사 하는 데 사용 합니다. |
| [ChangeEmailTokenProvider](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.changeemailtokenprovider) | 가져오거나는 `ChangeEmailTokenProvider` 전자 메일 변경 확인 전자 메일에 사용 되는 토큰을 생성 하는 데 사용 합니다. |
| [ChangePhoneNumberTokenProvider](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.changephonenumbertokenprovider) | 가져오거나는 `ChangePhoneNumberTokenProvider` 전화 번호를 변경할 때 사용 되는 토큰을 생성 하는 데 사용 합니다. |
| [EmailConfirmationTokenProvider](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.emailconfirmationtokenprovider) | 계정 확인 전자 메일에 사용 되는 토큰을 생성 하는 데 사용 되는 토큰 공급자를 가져오거나 설정 합니다. |
| [PasswordResetTokenProvider](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.passwordresettokenprovider) | 가져오거나는 [IUserTwoFactorTokenProvider<TUser> ](/dotnet/api/microsoft.aspnetcore.identity.iusertwofactortokenprovider-1) 암호 재설정 전자 메일에 사용 되는 토큰을 생성 하는 데 사용 합니다. |
| [ProviderMap](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.providermap) | 생성 하는 데는 [사용자 토큰 공급자](/dotnet/api/microsoft.aspnetcore.identity.tokenproviderdescriptor) 공급자의 이름으로 사용 된 키입니다. |

### <a name="user"></a>사용자

[!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,48-52)]

[IdentityOptions.User](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.user) 지정는 [UserOptions](/dotnet/api/microsoft.aspnetcore.identity.useroptions) 표에 표시 된 속성을 사용 합니다.

| 속성 | 설명 | 기본 |
| -------- | ----------- | :-----: |
| [AllowedUserNameCharacters](/dotnet/api/microsoft.aspnetcore.identity.useroptions.allowedusernamecharacters) | 사용자 이름에 허용된 되는 문자입니다. | abcdefghijklmnopqrstuvwxyz<br>ABCDEFGHIJKLMNOPQRSTUVWXYZ<br>0123456789<br>-._@+ |
| [RequireUniqueEmail](/dotnet/api/microsoft.aspnetcore.identity.useroptions.requireuniqueemail) | 각 사용자에 게 고유한 전자 메일 필요 합니다. | `false` |

## <a name="cookie-settings"></a>쿠키 설정

구성에서 응용 프로그램의 쿠키 `Startup.ConfigureServices`:

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?name=snippet_configurecookie)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[!code-csharp[](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-59,72-80,84)]

---

[CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions) 속성은 다음과 같습니다.

| 속성 | 설명 |
| -------- | ----------- |
| [AccessDeniedPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.accessdeniedpath) | 처리기에 나가는 변경 해야 함을 알립니다 *403 사용할 수 없음* 에 상태 코드는 *302 리디렉션* 지정된 된 경로에 있습니다.<br><br>기본값은 `/Account/AccessDenied`입니다. |
| [AuthenticationScheme](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.authenticationscheme) | ASP.NET Core에만 적용 됩니다 1.x 합니다.<br><br> 특정 인증 체계에 대 한 논리적 이름입니다. |
| [AutomaticAuthenticate](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.automaticauthenticate) | ASP.NET Core에만 적용 됩니다 1.x 합니다.<br><br> True 인 경우 쿠키 인증 모든 요청에서 실행 하 고 유효성 검사 하 고 자신이 만든 직렬화 된 모든 보안 주체를 다시 생성 해야 합니다. |
| [AutomaticChallenge](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.automaticchallenge) | ASP.NET Core에만 적용 됩니다 1.x 합니다.<br><br> True 이면 인증 미들웨어 자동 문제를 처리 합니다. 경우 false 이면 인증 미들웨어만 변경 하 여 명시적으로 지정 하는 경우 응답은 `AuthenticationScheme`합니다. |
| [ClaimsIssuer](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions.claimsissuer) | 생성 되는 모든 클레임을 사용 해야 하는 발급자를 가져오거나 설정 합니다. (에서 상속 되며, [AuthenticationSchemeOptions](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions)). |
| [Cookie.Domain](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.domain) | 쿠키와 연결할 도메인입니다. |
| [Cookie.Expiration](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.expiration) | HTTP 쿠키 (인증 쿠키 제외)의 수명을 가져오거나 설정 합니다. 이 속성을 재정의 하 여 [ExpireTimeSpan](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.expiretimespan)합니다. CookieAuthentication의 컨텍스트에서 사용할 수 없습니다. |
| [Cookie.HttpOnly](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.httponly) | 쿠키는 클라이언트 쪽 스크립트에서 액세스할 수 있는지 여부를 나타냅니다.<br><br>기본값은 `true`입니다. |
| [Cookie.Name](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.name) | 쿠키의 이름입니다.<br><br>기본값은 `.AspNetCore.Cookies`입니다. |
| [Cookie.Path](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.path) | 쿠키 경로입니다. |
| [Cookie.SameSite](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.samesite) | `SameSite` 쿠키의 특성입니다.<br><br>기본값은 [SameSiteMode.Lax](/dotnet/api/microsoft.aspnetcore.http.samesitemode)합니다. |
| [Cookie.SecurePolicy](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.securepolicy) | [CookieSecurePolicy](/dotnet/api/microsoft.aspnetcore.http.cookiesecurepolicy) 구성 합니다.<br><br>기본값은 [CookieSecurePolicy.SameAsRequest](/dotnet/api/microsoft.aspnetcore.http.cookiesecurepolicy)합니다. |
| [CookieDomain](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiedomain) | ASP.NET Core에만 적용 됩니다 1.x 합니다.<br><br> 쿠키 처리 되는 도메인 이름입니다. |
| [CookieHttpOnly](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiehttponly) | ASP.NET Core에만 적용 됩니다 1.x 합니다.<br><br> 쿠키를 서버에만 액세스할 수 있어야 하는 경우를 나타내는 플래그입니다.<br><br>기본값은 `true`입니다. |
| [CookiePath](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiepath) | ASP.NET Core에만 적용 됩니다 1.x 합니다.<br><br> 동일한 호스트 이름에서 실행 되는 앱을 격리 하는 데 사용 합니다. |
| [CookieSecure](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiesecure) | ASP.NET Core에만 적용 됩니다 1.x 합니다.<br><br> 만든 쿠키를 HTTPS로 제한 해야 하는 경우를 나타내는 플래그 (`CookieSecurePolicy.Always`), HTTP 또는 HTTPS (`CookieSecurePolicy.None`), 또는 요청와 동일한 프로토콜 (`CookieSecurePolicy.SameAsRequest`).<br><br>기본값은 `CookieSecurePolicy.SameAsRequest`입니다. |
| [CookieManager](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.cookiemanager) | 요청에서 쿠키를 가져오거나 응답에서 속성을 설정 하는 데 사용 하는 구성 요소입니다. | [ChunkingCookieManager](/dotnet/api/microsoft.aspnetcore.authentication.cookies.chunkingcookiemanager) |
| [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.dataprotectionprovider) | 으로 설정한 공급자 사용 하 여는 [CookieAuthenticationHandler](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationhandler) 데이터를 보호 합니다. |
| [설명](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.description) | ASP.NET Core에만 적용 됩니다 1.x 합니다.<br><br> 응용 프로그램에 사용할 수 있는 인증 형식에 대 한 추가 정보입니다. |
| [이벤트](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.events) | 처리기는 처리가 발생 하는 특정 시점에서 응용 프로그램 컨트롤을 제공 하는 공급자에 메서드를 호출 합니다. |
| [EventsType](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions.eventstype) | 설정, 서비스 입력 가져오려는 `Events` 속성 대신 인스턴스 (에서 상속 되며, [AuthenticationSchemeOptions](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions)). |
| [ExpireTimeSpan](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.expiretimespan) | 얼마나 때 만들어진 시점부터 유효 쿠키 유지에 저장 된 인증 티켓을 제어 합니다.<br><br>기본값은 14 일입니다. |
| [LoginPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.loginpath) | 사용자 권한이 없는 경우 로그인에이 경로 리디렉션됩니다 하 합니다.<br><br>기본값은 `/Account/Login`입니다. |
| [LogoutPath](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.logoutpath) | 사용자가 로그 아웃,이 경로에 리디렉션됩니다 하 합니다.<br><br>기본값은 `/Account/Logout`입니다. |
| [ReturnUrlParameter](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.returnurlparameter) | 미들웨어에서 추가 되는 쿼리 문자열 매개 변수의 이름을 결정 때는 *401 권한 없음* 으로 변경 된 상태 코드는 *302 리디렉션* 로그인 경로로 합니다.<br><br>기본값은 `ReturnUrl`입니다. |
| [SessionStore](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.sessionstore) | 요청 간에 id를 저장할 선택적 컨테이너입니다. |
| [SlidingExpiration](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.slidingexpiration) | True 인 경우 새 만료 시간 현재 쿠키 만료 창을 통해 중간 부분 이상으로 새 쿠키를 발급 됩니다.<br><br>기본값은 `true`입니다. |
| [TicketDataFormat](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.ticketdataformat) | `TicketDataFormat` 보호 및 id 및 쿠키 값에 저장 되는 기타 속성을 보호 해제 하는 데 사용 됩니다. |
