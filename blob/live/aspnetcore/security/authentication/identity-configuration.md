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
ms.openlocfilehash: d3a13d1cef3417522460b44c52c1361c3e9d1162
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="configure-identity"></a><span data-ttu-id="5c114-103">Id 구성</span><span class="sxs-lookup"><span data-stu-id="5c114-103">Configure Identity</span></span>

<span data-ttu-id="5c114-104">ASP.NET Core Id 암호 정책, 잠금 시간 및 응용 프로그램에서 쉽게 재정의할 수 있는 쿠키 설정 등의 응용 프로그램에 대 한 일반적인 동작 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-104">ASP.NET Core Identity has common behaviors in applications such as password policy, lockout time, and cookie settings that you can override easily in your application's `Startup` class.</span></span>

## <a name="passwords-policy"></a><span data-ttu-id="5c114-105">암호 정책</span><span class="sxs-lookup"><span data-stu-id="5c114-105">Passwords policy</span></span>

<span data-ttu-id="5c114-106">기본적으로 Id는 암호에 대문자, 소문자, 숫자 및 영숫자가 아닌 문자를 포함 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-106">By default, Identity requires that passwords contain an uppercase character, lowercase character, a digit, and a non-alphanumeric character.</span></span> <span data-ttu-id="5c114-107">몇 가지 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-107">There are also some other restrictions.</span></span> <span data-ttu-id="5c114-108">암호 제한을 간단 하 게 하려면 수정 하는 `ConfigureServices` 의 메서드는 `Startup` 응용 프로그램의 클래스.</span><span class="sxs-lookup"><span data-stu-id="5c114-108">To simplify password restrictions, modify the `ConfigureServices` method of the `Startup` class of your application.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="5c114-109">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="5c114-109">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="5c114-110">ASP.NET Core 추가 2.0는 `RequiredUniqueChars` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-110">ASP.NET Core 2.0 added the `RequiredUniqueChars` property.</span></span> <span data-ttu-id="5c114-111">그렇지 않으면 옵션은 ASP.NET Core를 동일한 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-111">Otherwise, the options are the same from ASP.NET Core 1.x.</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-37,50-52)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="5c114-112">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="5c114-112">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-65,84)]

---

<span data-ttu-id="5c114-113">`IdentityOptions.Password`에 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-113">`IdentityOptions.Password` has the following properties:</span></span>

| <span data-ttu-id="5c114-114">속성</span><span class="sxs-lookup"><span data-stu-id="5c114-114">Property</span></span>                | <span data-ttu-id="5c114-115">설명</span><span class="sxs-lookup"><span data-stu-id="5c114-115">Description</span></span>                       | <span data-ttu-id="5c114-116">기본</span><span class="sxs-lookup"><span data-stu-id="5c114-116">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `RequireDigit`          | <span data-ttu-id="5c114-117">암호에 0-9 사이의 숫자를 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-117">Requires a number between 0-9 in the password.</span></span> | <span data-ttu-id="5c114-118">true</span><span class="sxs-lookup"><span data-stu-id="5c114-118">true</span></span> |
| `RequiredLength`        | <span data-ttu-id="5c114-119">암호의 최소 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-119">The minimum length of the password.</span></span> | <span data-ttu-id="5c114-120">6</span><span class="sxs-lookup"><span data-stu-id="5c114-120">6</span></span> |
| `RequireNonAlphanumeric`| <span data-ttu-id="5c114-121">암호에 영숫자가 아닌 문자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-121">Requires a non-alphanumeric character in the password.</span></span> | <span data-ttu-id="5c114-122">true</span><span class="sxs-lookup"><span data-stu-id="5c114-122">true</span></span> |
| `RequireUppercase`      | <span data-ttu-id="5c114-123">암호에는 대문자 문자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-123">Requires an upper case character in the password.</span></span> | <span data-ttu-id="5c114-124">true</span><span class="sxs-lookup"><span data-stu-id="5c114-124">true</span></span> |
| `RequireLowercase`      | <span data-ttu-id="5c114-125">암호에 소문자 문자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-125">Requires a lower case character in the password.</span></span> | <span data-ttu-id="5c114-126">true</span><span class="sxs-lookup"><span data-stu-id="5c114-126">true</span></span> |
| `RequiredUniqueChars`   | <span data-ttu-id="5c114-127">암호에 고유한 문자 수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-127">Requires the number of distinct characters in the password.</span></span> | <span data-ttu-id="5c114-128">1</span><span class="sxs-lookup"><span data-stu-id="5c114-128">1</span></span> |


## <a name="users-lockout"></a><span data-ttu-id="5c114-129">사용자의 잠금</span><span class="sxs-lookup"><span data-stu-id="5c114-129">User's lockout</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,39-42,50-52)]

<span data-ttu-id="5c114-130">`IdentityOptions.Lockout`에 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-130">`IdentityOptions.Lockout` has the following properties:</span></span>

| <span data-ttu-id="5c114-131">속성</span><span class="sxs-lookup"><span data-stu-id="5c114-131">Property</span></span>                | <span data-ttu-id="5c114-132">설명</span><span class="sxs-lookup"><span data-stu-id="5c114-132">Description</span></span>                       | <span data-ttu-id="5c114-133">기본</span><span class="sxs-lookup"><span data-stu-id="5c114-133">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `DefaultLockoutTimeSpan` | <span data-ttu-id="5c114-134">시간의 양은 사용자가 잠겨 잠금이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-134">The amount of time a user is locked out when a lockout occurs.</span></span>  | <span data-ttu-id="5c114-135">5 분</span><span class="sxs-lookup"><span data-stu-id="5c114-135">5 minutes</span></span>  |
| `MaxFailedAccessAttempts` | <span data-ttu-id="5c114-136">실패 한 액세스 시도 사용자가 잠겨 될 때까지 잠금이 설정 된 경우.</span><span class="sxs-lookup"><span data-stu-id="5c114-136">The number of failed access attempts until a user is locked out, if lockout is enabled.</span></span>  | <span data-ttu-id="5c114-137">5</span><span class="sxs-lookup"><span data-stu-id="5c114-137">5</span></span> |
| `AllowedForNewUsers` | <span data-ttu-id="5c114-138">하는 경우 새 사용자를 잠글 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-138">Determines if a new user can be locked out.</span></span>  | <span data-ttu-id="5c114-139">true</span><span class="sxs-lookup"><span data-stu-id="5c114-139">true</span></span> |

## <a name="sign-in-settings"></a><span data-ttu-id="5c114-140">로그인 설정</span><span class="sxs-lookup"><span data-stu-id="5c114-140">Sign in settings</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,44-46,50-52)]

<span data-ttu-id="5c114-141">`IdentityOptions.SignIn`에 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-141">`IdentityOptions.SignIn` has the following properties:</span></span>

| <span data-ttu-id="5c114-142">속성</span><span class="sxs-lookup"><span data-stu-id="5c114-142">Property</span></span>                | <span data-ttu-id="5c114-143">설명</span><span class="sxs-lookup"><span data-stu-id="5c114-143">Description</span></span>                       | <span data-ttu-id="5c114-144">기본</span><span class="sxs-lookup"><span data-stu-id="5c114-144">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `RequireConfirmedEmail` | <span data-ttu-id="5c114-145">확인 된 전자 메일에 로그인 할 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-145">Requires a confirmed email to sign in.</span></span> | <span data-ttu-id="5c114-146">False</span><span class="sxs-lookup"><span data-stu-id="5c114-146">false</span></span>  |
| `RequireConfirmedPhoneNumber` |  <span data-ttu-id="5c114-147">로그인에 확인 된 전화 번호가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-147">Requires a confirmed phone number to sign in.</span></span> | <span data-ttu-id="5c114-148">False</span><span class="sxs-lookup"><span data-stu-id="5c114-148">false</span></span>  |

## <a name="user-validation-settings"></a><span data-ttu-id="5c114-149">사용자 유효성 검사 설정</span><span class="sxs-lookup"><span data-stu-id="5c114-149">User validation settings</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,48-52)]

<span data-ttu-id="5c114-150">`IdentityOptions.User`에 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-150">`IdentityOptions.User` has the following properties:</span></span>

| <span data-ttu-id="5c114-151">속성</span><span class="sxs-lookup"><span data-stu-id="5c114-151">Property</span></span>                | <span data-ttu-id="5c114-152">설명</span><span class="sxs-lookup"><span data-stu-id="5c114-152">Description</span></span>                       | <span data-ttu-id="5c114-153">기본</span><span class="sxs-lookup"><span data-stu-id="5c114-153">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `RequireUniqueEmail`  | <span data-ttu-id="5c114-154">각 사용자에 게 고유한 전자 메일 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-154">Requires each User to have a unique email.</span></span> | <span data-ttu-id="5c114-155">False</span><span class="sxs-lookup"><span data-stu-id="5c114-155">false</span></span>  |
| `AllowedUserNameCharacters`  | <span data-ttu-id="5c114-156">사용자 이름에 허용된 되는 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-156">Allowed characters in the username.</span></span> | <span data-ttu-id="5c114-157">abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789-._@+</span><span class="sxs-lookup"><span data-stu-id="5c114-157">abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789-._@+</span></span> |


## <a name="applications-cookie-settings"></a><span data-ttu-id="5c114-158">응용 프로그램의 쿠키 설정</span><span class="sxs-lookup"><span data-stu-id="5c114-158">Application's cookie settings</span></span>

<span data-ttu-id="5c114-159">암호 정책와 같은 응용 프로그램의 쿠키의 모든 설정에서 변경할 수 있습니다는 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-159">Like the passwords policy, all the settings of the application's cookie can be changed in the `Startup` class.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="5c114-160">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="5c114-160">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="5c114-161">아래 `ConfigureServices` 에 `Startup` 클래스, 응용 프로그램의 쿠키를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-161">Under `ConfigureServices` in the `Startup` class, you can configure the application's cookie.</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?name=snippet_configurecookie)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="5c114-162">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="5c114-162">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-59,72-80,84)]

---

<span data-ttu-id="5c114-163">`CookieAuthenticationOptions`에 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-163">`CookieAuthenticationOptions` has the following properties:</span></span>

| <span data-ttu-id="5c114-164">속성</span><span class="sxs-lookup"><span data-stu-id="5c114-164">Property</span></span>                | <span data-ttu-id="5c114-165">설명</span><span class="sxs-lookup"><span data-stu-id="5c114-165">Description</span></span>                       | <span data-ttu-id="5c114-166">기본</span><span class="sxs-lookup"><span data-stu-id="5c114-166">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `Cookie.Name`  | <span data-ttu-id="5c114-167">쿠키의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-167">The name of the cookie.</span></span>  | <span data-ttu-id="5c114-168">.AspNetCore.Cookies.</span><span class="sxs-lookup"><span data-stu-id="5c114-168">.AspNetCore.Cookies.</span></span>  |
| `Cookie.HttpOnly`  | <span data-ttu-id="5c114-169">True 인 경우는 쿠키는 클라이언트 쪽 스크립트에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-169">When true, the cookie is not accessible from client-side scripts.</span></span>  |  <span data-ttu-id="5c114-170">true</span><span class="sxs-lookup"><span data-stu-id="5c114-170">true</span></span> |
| `ExpireTimeSpan`  | <span data-ttu-id="5c114-171">쿠키에 저장 된 인증 티켓 시간 유효 하 게 유지에서 만들어진 시점을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-171">Controls how much time the authentication ticket stored in the cookie will remain valid from the point it is created.</span></span>  | <span data-ttu-id="5c114-172">14 일</span><span class="sxs-lookup"><span data-stu-id="5c114-172">14 days</span></span>  |
| `LoginPath`  | <span data-ttu-id="5c114-173">사용자 권한이 없는 경우 로그인에이 경로로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-173">When a user is unauthorized, they will be redirected to this path to login.</span></span> | <span data-ttu-id="5c114-174">/ 계정/로그인</span><span class="sxs-lookup"><span data-stu-id="5c114-174">/Account/Login</span></span>  |
| `LogoutPath`  | <span data-ttu-id="5c114-175">사용자 로그 아웃 하는 경우이 경로로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-175">When a user is logged out, they will be redirected to this path.</span></span>  | <span data-ttu-id="5c114-176">/Account/Logout</span><span class="sxs-lookup"><span data-stu-id="5c114-176">/Account/Logout</span></span>  |
| `AccessDeniedPath`  | <span data-ttu-id="5c114-177">사용자 권한 확인에 실패 하면이 경로로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-177">When a user fails an authorization check, they will be redirected to this path.</span></span>  |   |
| `SlidingExpiration`  | <span data-ttu-id="5c114-178">True 인 경우 새 만료 시간 현재 쿠키 만료 창을 통해 중간 부분 이상으로 새로운 쿠키를 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-178">When true, a new cookie will be issued with a new expiration time when the current cookie is more than halfway through the expiration window.</span></span>  | <span data-ttu-id="5c114-179">/Account/AccessDenied</span><span class="sxs-lookup"><span data-stu-id="5c114-179">/Account/AccessDenied</span></span> |
| `ReturnUrlParameter`  | <span data-ttu-id="5c114-180">미들웨어는 401 권한이 없음된 상태 코드가 302 로그인 경로로 리디렉션으로 변경 되 면 추가 되는 쿼리 문자열 매개 변수의 이름을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-180">Determines the name of the query string parameter which is appended by the middleware when a 401 Unauthorized status code is changed to a 302 redirect onto the login path.</span></span>  |  <span data-ttu-id="5c114-181">true</span><span class="sxs-lookup"><span data-stu-id="5c114-181">true</span></span> |
| `AuthenticationScheme`  | <span data-ttu-id="5c114-182">이 ASP.NET Core에 대 한 관련만 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-182">This is only relevant for ASP.NET Core 1.x.</span></span> <span data-ttu-id="5c114-183">특정 인증 체계에 대 한 논리적 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-183">The logical name for a particular authentication scheme.</span></span> |  |
| `AutomaticAuthenticate`  | <span data-ttu-id="5c114-184">이 플래그는 ASP.NET Core에 대 한 관련만 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-184">This flag is only relevant for ASP.NET Core 1.x.</span></span> <span data-ttu-id="5c114-185">True 인 경우 쿠키 인증 모든 요청에서 실행 하 고 유효성 검사 하 고 자신이 만든 직렬화 된 모든 보안 주체를 다시 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c114-185">When true, cookie authentication should run on every request and attempt to validate and reconstruct any serialized principal it created.</span></span>  |  |
