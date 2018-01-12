---
title: "ASP.NET Core Id 구성"
author: AdrienTorris
description: "ASP.NET Core Id 기본값을 이해 하 고 사용자 지정 값을 사용 하도록 다양 한 Id 속성을 구성 합니다."
keywords: "ASP.NET Core, Identity, 인증, 보안"
ms.author: scaddie
manager: wpickett
ms.date: 01/11/2018
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authentication/identity-configuration
ms.openlocfilehash: ac204cb89aac1f90adc64c4f0bec4e946cb8c4d9
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2018
---
# <a name="configure-identity"></a><span data-ttu-id="12a74-104">Id 구성</span><span class="sxs-lookup"><span data-stu-id="12a74-104">Configure Identity</span></span>

<span data-ttu-id="12a74-105">ASP.NET Core Id 암호 정책, 잠금 시간 및 응용 프로그램에서 쉽게 재정의할 수 있는 쿠키 설정 등의 응용 프로그램에 대 한 일반적인 동작 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-105">ASP.NET Core Identity has common behaviors in applications such as password policy, lockout time, and cookie settings that you can override easily in your application's `Startup` class.</span></span>

## <a name="passwords-policy"></a><span data-ttu-id="12a74-106">암호 정책</span><span class="sxs-lookup"><span data-stu-id="12a74-106">Passwords policy</span></span>

<span data-ttu-id="12a74-107">기본적으로 Id는 암호에 대문자, 소문자, 숫자 및 영숫자가 아닌 문자를 포함 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-107">By default, Identity requires that passwords contain an uppercase character, lowercase character, a digit, and a non-alphanumeric character.</span></span> <span data-ttu-id="12a74-108">몇 가지 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-108">There are also some other restrictions.</span></span> <span data-ttu-id="12a74-109">암호 제한을 간단 하 게 하려면 수정 하는 `ConfigureServices` 의 메서드는 `Startup` 응용 프로그램의 클래스.</span><span class="sxs-lookup"><span data-stu-id="12a74-109">To simplify password restrictions, modify the `ConfigureServices` method of the `Startup` class of your application.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="12a74-110">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="12a74-110">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="12a74-111">ASP.NET Core 추가 2.0는 `RequiredUniqueChars` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-111">ASP.NET Core 2.0 added the `RequiredUniqueChars` property.</span></span> <span data-ttu-id="12a74-112">그렇지 않으면 옵션은 ASP.NET Core를 동일한 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-112">Otherwise, the options are the same from ASP.NET Core 1.x.</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-37,50-52)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="12a74-113">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="12a74-113">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-65,84)]

---

<span data-ttu-id="12a74-114">`IdentityOptions.Password`에 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-114">`IdentityOptions.Password` has the following properties:</span></span>

| <span data-ttu-id="12a74-115">속성</span><span class="sxs-lookup"><span data-stu-id="12a74-115">Property</span></span>                | <span data-ttu-id="12a74-116">설명</span><span class="sxs-lookup"><span data-stu-id="12a74-116">Description</span></span>                       | <span data-ttu-id="12a74-117">기본</span><span class="sxs-lookup"><span data-stu-id="12a74-117">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `RequireDigit`          | <span data-ttu-id="12a74-118">암호에 0-9 사이의 숫자를 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-118">Requires a number between 0-9 in the password.</span></span> | <span data-ttu-id="12a74-119">true</span><span class="sxs-lookup"><span data-stu-id="12a74-119">true</span></span> |
| `RequiredLength`        | <span data-ttu-id="12a74-120">암호의 최소 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-120">The minimum length of the password.</span></span> | <span data-ttu-id="12a74-121">6</span><span class="sxs-lookup"><span data-stu-id="12a74-121">6</span></span> |
| `RequireNonAlphanumeric`| <span data-ttu-id="12a74-122">암호에 영숫자가 아닌 문자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-122">Requires a non-alphanumeric character in the password.</span></span> | <span data-ttu-id="12a74-123">true</span><span class="sxs-lookup"><span data-stu-id="12a74-123">true</span></span> |
| `RequireUppercase`      | <span data-ttu-id="12a74-124">암호에는 대문자 문자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-124">Requires an upper case character in the password.</span></span> | <span data-ttu-id="12a74-125">true</span><span class="sxs-lookup"><span data-stu-id="12a74-125">true</span></span> |
| `RequireLowercase`      | <span data-ttu-id="12a74-126">암호에 소문자 문자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-126">Requires a lower case character in the password.</span></span> | <span data-ttu-id="12a74-127">true</span><span class="sxs-lookup"><span data-stu-id="12a74-127">true</span></span> |
| `RequiredUniqueChars`   | <span data-ttu-id="12a74-128">암호에 고유한 문자 수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-128">Requires the number of distinct characters in the password.</span></span> | <span data-ttu-id="12a74-129">1</span><span class="sxs-lookup"><span data-stu-id="12a74-129">1</span></span> |


## <a name="users-lockout"></a><span data-ttu-id="12a74-130">사용자의 잠금</span><span class="sxs-lookup"><span data-stu-id="12a74-130">User's lockout</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,39-42,50-52)]

<span data-ttu-id="12a74-131">`IdentityOptions.Lockout`에 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-131">`IdentityOptions.Lockout` has the following properties:</span></span>

| <span data-ttu-id="12a74-132">속성</span><span class="sxs-lookup"><span data-stu-id="12a74-132">Property</span></span>                | <span data-ttu-id="12a74-133">설명</span><span class="sxs-lookup"><span data-stu-id="12a74-133">Description</span></span>                       | <span data-ttu-id="12a74-134">기본</span><span class="sxs-lookup"><span data-stu-id="12a74-134">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `DefaultLockoutTimeSpan` | <span data-ttu-id="12a74-135">시간의 양은 사용자가 잠겨 잠금이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-135">The amount of time a user is locked out when a lockout occurs.</span></span>  | <span data-ttu-id="12a74-136">5 분</span><span class="sxs-lookup"><span data-stu-id="12a74-136">5 minutes</span></span>  |
| `MaxFailedAccessAttempts` | <span data-ttu-id="12a74-137">실패 한 액세스 시도 사용자가 잠겨 될 때까지 잠금이 설정 된 경우.</span><span class="sxs-lookup"><span data-stu-id="12a74-137">The number of failed access attempts until a user is locked out, if lockout is enabled.</span></span>  | <span data-ttu-id="12a74-138">5</span><span class="sxs-lookup"><span data-stu-id="12a74-138">5</span></span> |
| `AllowedForNewUsers` | <span data-ttu-id="12a74-139">하는 경우 새 사용자를 잠글 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-139">Determines if a new user can be locked out.</span></span>  | <span data-ttu-id="12a74-140">true</span><span class="sxs-lookup"><span data-stu-id="12a74-140">true</span></span> |

## <a name="sign-in-settings"></a><span data-ttu-id="12a74-141">로그인 설정</span><span class="sxs-lookup"><span data-stu-id="12a74-141">Sign in settings</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,44-46,50-52)]

<span data-ttu-id="12a74-142">`IdentityOptions.SignIn`에 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-142">`IdentityOptions.SignIn` has the following properties:</span></span>

| <span data-ttu-id="12a74-143">속성</span><span class="sxs-lookup"><span data-stu-id="12a74-143">Property</span></span>                | <span data-ttu-id="12a74-144">설명</span><span class="sxs-lookup"><span data-stu-id="12a74-144">Description</span></span>                       | <span data-ttu-id="12a74-145">기본</span><span class="sxs-lookup"><span data-stu-id="12a74-145">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `RequireConfirmedEmail` | <span data-ttu-id="12a74-146">확인 된 전자 메일에 로그인 할 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-146">Requires a confirmed email to sign in.</span></span> | <span data-ttu-id="12a74-147">False</span><span class="sxs-lookup"><span data-stu-id="12a74-147">false</span></span>  |
| `RequireConfirmedPhoneNumber` |  <span data-ttu-id="12a74-148">로그인에 확인 된 전화 번호가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-148">Requires a confirmed phone number to sign in.</span></span> | <span data-ttu-id="12a74-149">False</span><span class="sxs-lookup"><span data-stu-id="12a74-149">false</span></span>  |

## <a name="user-validation-settings"></a><span data-ttu-id="12a74-150">사용자 유효성 검사 설정</span><span class="sxs-lookup"><span data-stu-id="12a74-150">User validation settings</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,48-52)]

<span data-ttu-id="12a74-151">`IdentityOptions.User`에 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-151">`IdentityOptions.User` has the following properties:</span></span>

| <span data-ttu-id="12a74-152">속성</span><span class="sxs-lookup"><span data-stu-id="12a74-152">Property</span></span>                | <span data-ttu-id="12a74-153">설명</span><span class="sxs-lookup"><span data-stu-id="12a74-153">Description</span></span>                       | <span data-ttu-id="12a74-154">기본</span><span class="sxs-lookup"><span data-stu-id="12a74-154">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `RequireUniqueEmail`  | <span data-ttu-id="12a74-155">각 사용자에 게 고유한 전자 메일 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-155">Requires each User to have a unique email.</span></span> | <span data-ttu-id="12a74-156">False</span><span class="sxs-lookup"><span data-stu-id="12a74-156">false</span></span>  |
| `AllowedUserNameCharacters`  | <span data-ttu-id="12a74-157">사용자 이름에 허용된 되는 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-157">Allowed characters in the username.</span></span> | <span data-ttu-id="12a74-158">abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789-._@+</span><span class="sxs-lookup"><span data-stu-id="12a74-158">abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789-._@+</span></span> |


## <a name="applications-cookie-settings"></a><span data-ttu-id="12a74-159">응용 프로그램의 쿠키 설정</span><span class="sxs-lookup"><span data-stu-id="12a74-159">Application's cookie settings</span></span>

<span data-ttu-id="12a74-160">암호 정책와 같은 응용 프로그램의 쿠키의 모든 설정에서 변경할 수 있습니다는 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-160">Like the passwords policy, all the settings of the application's cookie can be changed in the `Startup` class.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="12a74-161">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="12a74-161">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="12a74-162">아래 `ConfigureServices` 에 `Startup` 클래스, 응용 프로그램의 쿠키를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-162">Under `ConfigureServices` in the `Startup` class, you can configure the application's cookie.</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?name=snippet_configurecookie)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="12a74-163">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="12a74-163">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-59,72-80,84)]

---

<span data-ttu-id="12a74-164">`CookieAuthenticationOptions`에 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-164">`CookieAuthenticationOptions` has the following properties:</span></span>

| <span data-ttu-id="12a74-165">속성</span><span class="sxs-lookup"><span data-stu-id="12a74-165">Property</span></span>                | <span data-ttu-id="12a74-166">설명</span><span class="sxs-lookup"><span data-stu-id="12a74-166">Description</span></span>                       | <span data-ttu-id="12a74-167">기본</span><span class="sxs-lookup"><span data-stu-id="12a74-167">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `Cookie.Name`  | <span data-ttu-id="12a74-168">쿠키의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-168">The name of the cookie.</span></span>  | <span data-ttu-id="12a74-169">. AspNetCore.Cookies 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-169">.AspNetCore.Cookies.</span></span>  |
| `Cookie.HttpOnly`  | <span data-ttu-id="12a74-170">True 인 경우는 쿠키는 클라이언트 쪽 스크립트에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-170">When true, the cookie is not accessible from client-side scripts.</span></span>  |  <span data-ttu-id="12a74-171">true</span><span class="sxs-lookup"><span data-stu-id="12a74-171">true</span></span> |
| `ExpireTimeSpan`  | <span data-ttu-id="12a74-172">쿠키에 저장 된 인증 티켓 시간 유효 하 게 유지에서 만들어진 시점을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-172">Controls how much time the authentication ticket stored in the cookie will remain valid from the point it is created.</span></span>  | <span data-ttu-id="12a74-173">14 일</span><span class="sxs-lookup"><span data-stu-id="12a74-173">14 days</span></span>  |
| `LoginPath`  | <span data-ttu-id="12a74-174">사용자 권한이 없는 경우 로그인에이 경로로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-174">When a user is unauthorized, they will be redirected to this path to login.</span></span> | <span data-ttu-id="12a74-175">/ 계정/로그인</span><span class="sxs-lookup"><span data-stu-id="12a74-175">/Account/Login</span></span>  |
| `LogoutPath`  | <span data-ttu-id="12a74-176">사용자 로그 아웃 하는 경우이 경로로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-176">When a user is logged out, they will be redirected to this path.</span></span>  | <span data-ttu-id="12a74-177">/ 계정/로그 아웃</span><span class="sxs-lookup"><span data-stu-id="12a74-177">/Account/Logout</span></span>  |
| `AccessDeniedPath`  | <span data-ttu-id="12a74-178">사용자 권한 확인에 실패 하면이 경로로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-178">When a user fails an authorization check, they will be redirected to this path.</span></span>  |   |
| `SlidingExpiration`  | <span data-ttu-id="12a74-179">True 인 경우 새 만료 시간 현재 쿠키 만료 창을 통해 중간 부분 이상으로 새로운 쿠키를 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-179">When true, a new cookie will be issued with a new expiration time when the current cookie is more than halfway through the expiration window.</span></span>  | <span data-ttu-id="12a74-180">/ 계정/액세스 실패</span><span class="sxs-lookup"><span data-stu-id="12a74-180">/Account/AccessDenied</span></span> |
| `ReturnUrlParameter`  | <span data-ttu-id="12a74-181">미들웨어는 401 권한이 없음된 상태 코드가 302 로그인 경로로 리디렉션으로 변경 되 면 추가 되는 쿼리 문자열 매개 변수의 이름을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-181">Determines the name of the query string parameter which is appended by the middleware when a 401 Unauthorized status code is changed to a 302 redirect onto the login path.</span></span>  |  <span data-ttu-id="12a74-182">true</span><span class="sxs-lookup"><span data-stu-id="12a74-182">true</span></span> |
| `AuthenticationScheme`  | <span data-ttu-id="12a74-183">이 ASP.NET Core에 대 한 관련만 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-183">This is only relevant for ASP.NET Core 1.x.</span></span> <span data-ttu-id="12a74-184">특정 인증 체계에 대 한 논리적 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-184">The logical name for a particular authentication scheme.</span></span> |  |
| `AutomaticAuthenticate`  | <span data-ttu-id="12a74-185">이 플래그는 ASP.NET Core에 대 한 관련만 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-185">This flag is only relevant for ASP.NET Core 1.x.</span></span> <span data-ttu-id="12a74-186">True 인 경우 쿠키 인증 모든 요청에서 실행 하 고 유효성 검사 하 고 자신이 만든 직렬화 된 모든 보안 주체를 다시 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12a74-186">When true, cookie authentication should run on every request and attempt to validate and reconstruct any serialized principal it created.</span></span>  |  |