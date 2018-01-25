---
title: Configure ASP.NET Core Identity
author: AdrienTorris
description: "ASP.NET Core Id 기본값을 이해 하 고 사용자 지정 값을 사용 하도록 다양 한 Id 속성을 구성 합니다."
ms.author: scaddie
manager: wpickett
ms.date: 01/11/2018
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authentication/identity-configuration
ms.openlocfilehash: 9e79e670173952f1e791a0cefba61c41e1ad4437
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="configure-identity"></a>Id 구성

ASP.NET Core Id 암호 정책, 잠금 시간 및 응용 프로그램에서 쉽게 재정의할 수 있는 쿠키 설정 등의 응용 프로그램에 대 한 일반적인 동작 `Startup` 클래스입니다.

## <a name="passwords-policy"></a>암호 정책

기본적으로 Id는 암호에 대문자, 소문자, 숫자 및 영숫자가 아닌 문자를 포함 필요 합니다. 몇 가지 제한 사항이 있습니다. 암호 제한을 간단 하 게 하려면 수정 하는 `ConfigureServices` 의 메서드는 `Startup` 응용 프로그램의 클래스.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

ASP.NET Core 추가 2.0는 `RequiredUniqueChars` 속성입니다. 그렇지 않으면 옵션은 ASP.NET Core를 동일한 1.x 합니다.

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-37,50-52)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-65,84)]

---

`IdentityOptions.Password`에 다음과 같은 속성이 있습니다.

| 속성                | 설명                       | 기본 |
| ----------------------- | --------------------------------- | ------- |
| `RequireDigit`          | 암호에 0-9 사이의 숫자를 여야 합니다. | true |
| `RequiredLength`        | 암호의 최소 길이입니다. | 6 |
| `RequireNonAlphanumeric`| 암호에 영숫자가 아닌 문자가 필요합니다. | true |
| `RequireUppercase`      | 암호에는 대문자 문자가 필요합니다. | true |
| `RequireLowercase`      | 암호에 소문자 문자가 필요합니다. | true |
| `RequiredUniqueChars`   | 암호에 고유한 문자 수가 필요합니다. | 1 |


## <a name="users-lockout"></a>사용자의 잠금

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,39-42,50-52)]

`IdentityOptions.Lockout`에 다음과 같은 속성이 있습니다.

| 속성                | 설명                       | 기본 |
| ----------------------- | --------------------------------- | ------- |
| `DefaultLockoutTimeSpan` | 시간의 양은 사용자가 잠겨 잠금이 발생 합니다.  | 5 분  |
| `MaxFailedAccessAttempts` | 실패 한 액세스 시도 사용자가 잠겨 될 때까지 잠금이 설정 된 경우.  | 5 |
| `AllowedForNewUsers` | 하는 경우 새 사용자를 잠글 수를 결정 합니다.  | true |

## <a name="sign-in-settings"></a>로그인 설정

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,44-46,50-52)]

`IdentityOptions.SignIn`에 다음과 같은 속성이 있습니다.

| 속성                | 설명                       | 기본 |
| ----------------------- | --------------------------------- | ------- |
| `RequireConfirmedEmail` | 확인 된 전자 메일에 로그인 할 필요 합니다. | False  |
| `RequireConfirmedPhoneNumber` |  로그인에 확인 된 전화 번호가 필요 합니다. | False  |

## <a name="user-validation-settings"></a>사용자 유효성 검사 설정

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,48-52)]

`IdentityOptions.User`에 다음과 같은 속성이 있습니다.

| 속성                | 설명                       | 기본 |
| ----------------------- | --------------------------------- | ------- |
| `RequireUniqueEmail`  | 각 사용자에 게 고유한 전자 메일 필요 합니다. | False  |
| `AllowedUserNameCharacters`  | 사용자 이름에 허용된 되는 문자입니다. | abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789-._@+ |


## <a name="applications-cookie-settings"></a>응용 프로그램의 쿠키 설정

암호 정책와 같은 응용 프로그램의 쿠키의 모든 설정에서 변경할 수 있습니다는 `Startup` 클래스입니다.

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

아래 `ConfigureServices` 에 `Startup` 클래스, 응용 프로그램의 쿠키를 구성할 수 있습니다.

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?name=snippet_configurecookie)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-59,72-80,84)]

---

`CookieAuthenticationOptions`에 다음과 같은 속성이 있습니다.

| 속성                | 설명                       | 기본 |
| ----------------------- | --------------------------------- | ------- |
| `Cookie.Name`  | 쿠키의 이름입니다.  | .AspNetCore.Cookies.  |
| `Cookie.HttpOnly`  | True 인 경우 쿠키는 클라이언트 쪽 스크립트에서 액세스할 수 없습니다.  |  true |
| `ExpireTimeSpan`  | 쿠키에 저장 된 인증 티켓 시간 유효 하 게 유지에서 만들어진 시점을 제어 합니다.  | 14 일  |
| `LoginPath`  | 사용자 권한이 없는 경우 로그인에이 경로로 이동 합니다. | / 계정/로그인  |
| `LogoutPath`  | 사용자 로그 아웃 하는 경우이 경로로 이동 합니다.  | /Account/Logout  |
| `AccessDeniedPath`  | 사용자 권한 확인에 실패 하면이 경로로 이동 합니다.  |   |
| `SlidingExpiration`  | True 인 경우 새 만료 시간 현재 쿠키 만료 창을 통해 중간 부분 이상으로 새로운 쿠키를 발급 합니다.  | /Account/AccessDenied |
| `ReturnUrlParameter`  | 미들웨어는 401 권한이 없음된 상태 코드가 302 로그인 경로로 리디렉션으로 변경 되 면 추가 되는 쿼리 문자열 매개 변수의 이름을 결정 합니다.  |  true |
| `AuthenticationScheme`  | 이 ASP.NET Core에 대 한 관련만 1.x 합니다. 특정 인증 체계에 대 한 논리적 이름입니다. |  |
| `AutomaticAuthenticate`  | 이 플래그는 ASP.NET Core에 대 한 관련만 1.x 합니다. True 인 경우 쿠키 인증 모든 요청에서 실행 하 고 유효성 검사 하 고 자신이 만든 직렬화 된 모든 보안 주체를 다시 생성 해야 합니다.  |  |
