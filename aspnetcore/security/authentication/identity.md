---
title: ASP.NET Core Identity 소개
author: rick-anderson
description: ASP.NET Core 앱을 사용 하 여 Id를 사용 합니다. 암호 요구 사항 (RequireDigit, RequiredLength, RequiredUniqueChars, 등)을 설정 하는 방법에 알아봅니다.
ms.author: riande
ms.date: 08/08/2018
uid: security/authentication/identity
ms.openlocfilehash: 96f446ad9ec1ef5d807a8648e68308ee20583365
ms.sourcegitcommit: 08bf41d4b3e696ab512b044970e8304816f8cc56
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "44040030"
---
# <a name="introduction-to-identity-on-aspnet-core"></a><span data-ttu-id="61534-104">ASP.NET Core Identity 소개</span><span class="sxs-lookup"><span data-stu-id="61534-104">Introduction to Identity on ASP.NET Core</span></span>

<span data-ttu-id="61534-105">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="61534-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="61534-106">ASP.NET Core Id는 ASP.NET Core 앱에 로그인 기능을 추가 하는 멤버 자격 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="61534-106">ASP.NET Core Identity is a membership system that adds login functionality to ASP.NET Core apps.</span></span> <span data-ttu-id="61534-107">사용자 Id에 저장 된 로그인 정보를 사용 하 여 계정을 만들 수 있습니다 하거나 외부 로그인 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61534-107">Users can create an account with the login information stored in Identity or they can use an external login provider.</span></span> <span data-ttu-id="61534-108">지원 되는 외부 로그인 공급자를 포함 [Facebook, Google, Microsoft 계정 및 Twitter](xref:security/authentication/social/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-108">Supported external login providers include [Facebook, Google, Microsoft Account, and Twitter](xref:security/authentication/social/index).</span></span>

<span data-ttu-id="61534-109">사용자 이름, 암호 및 프로필 데이터를 저장 하는 SQL Server 데이터베이스를 사용 하 여 id는 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61534-109">Identity can be configured using a SQL Server database to store user names, passwords, and profile data.</span></span> <span data-ttu-id="61534-110">또는 다른 영구 저장소 예를 들어, Azure Table Storage 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61534-110">Alternatively, another persistent store can be used, for example, Azure Table Storage.</span></span>

[<span data-ttu-id="61534-111">예제 코드 살펴보기 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="61534-111">View or download the sample code.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/identity/sample/src/ASPNETCore-IdentityDemoComplete/) [<span data-ttu-id="61534-112">(다운로드 방법)</span><span class="sxs-lookup"><span data-stu-id="61534-112">(How to download)</span></span>](xref:tutorials/index#how-to-download-a-sample)

<span data-ttu-id="61534-113">이 항목의 Id를 사용 하 여 등록, 로그인 하는 방법을 알아보고는 사용자를 로그 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-113">In this topic, you learn how to use Identity to register, log in, and log out a user.</span></span> <span data-ttu-id="61534-114">Identity를 사용 하는 앱을 만드는 방법에 대 한 자세한 내용은이 문서의 끝에 있는 다음 단계 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="61534-114">For more detailed instructions about creating apps that use Identity, see the Next Steps section at the end of this article.</span></span>

## <a name="create-a-web-app-with-authentication"></a><span data-ttu-id="61534-115">인증을 사용 하 여 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="61534-115">Create a Web app with authentication</span></span>

<span data-ttu-id="61534-116">개별 사용자 계정으로 새로운 ASP.NET Core 웹 응용 프로그램 생성하기.</span><span class="sxs-lookup"><span data-stu-id="61534-116">Create an ASP.NET Core Web Application project with Individual User Accounts.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="61534-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="61534-117">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="61534-118">**파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-118">Select **File** > **New** > **Project**.</span></span> 
* <span data-ttu-id="61534-119">**새 ASP.NET Core 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-119">Select **ASP.NET Core Web Application**.</span></span> <span data-ttu-id="61534-120">프로젝트 이름을 **WebApp1** 프로젝트 다운로드와 같은 네임 스페이스에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-120">Name the project **WebApp1** to have the same namespace as the project download.</span></span> <span data-ttu-id="61534-121">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-121">Click **OK**.</span></span>
* <span data-ttu-id="61534-122">ASP.NET Core를 선택 **웹 응용 프로그램** ASP.NET Core 2.1에 대 한 선택한 **인증 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-122">Select an ASP.NET Core **Web Application** for ASP.NET Core 2.1, then select **Change Authentication**.</span></span>
* <span data-ttu-id="61534-123">선택 **개별 사용자 계정** 누릅니다 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-123">Select **Individual User Accounts** and click **OK**.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="61534-124">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="61534-124">.NET Core CLI</span></span>](#tab/netcore-cli)

```cli
dotnet new webapp --auth Individual -o WebApp1
```

---

<span data-ttu-id="61534-125">생성된 된 프로젝트를 제공 [ASP.NET Core Id](xref:security/authentication/identity) 으로 [Razor 클래스 라이브러리](xref:razor-pages/ui-class)합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-125">The generated project provides [ASP.NET Core Identity](xref:security/authentication/identity) as a [Razor Class Library](xref:razor-pages/ui-class).</span></span>

### <a name="test-register-and-login"></a><span data-ttu-id="61534-126">테스트 등록 및 로그인</span><span class="sxs-lookup"><span data-stu-id="61534-126">Test Register and Login</span></span>

<span data-ttu-id="61534-127">앱을 실행 하 고 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-127">Run the app and register a user.</span></span> <span data-ttu-id="61534-128">화면 크기에 따라 탐색 설정/해제 단추를 선택 해야 합니다 **등록** 하 고 **로그인** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-128">Depending on your screen size, you might need to select the navigation toggle button to see the **Register** and **Login** links.</span></span>

![탐색 모음 설정/해제 단추](identity/_static/navToggle.png)

[!INCLUDE[](~/includes/view-identity-db.md)]

<a name="pw"></a>
### <a name="configure-identity-services"></a><span data-ttu-id="61534-130">Id 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-130">Configure Identity services</span></span>

<span data-ttu-id="61534-131">서비스에 추가 된 `ConfigureServices`합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-131">Services are added in `ConfigureServices`.</span></span> <span data-ttu-id="61534-132">일반적인 패턴은 모든 호출 하는 것은 `Add{Service}` 메서드 및 호출을 `services.Configure{Service}` 메서드.</span><span class="sxs-lookup"><span data-stu-id="61534-132">The typical pattern is to call all the `Add{Service}` methods, and then call all the `services.Configure{Service}` methods.</span></span> <span data-ttu-id="61534-133">다음 코드는 생성 된 템플릿을 포함 되지 않습니다 `CookiePolicyOptions`:</span><span class="sxs-lookup"><span data-stu-id="61534-133">The following code doesn't include the template generated `CookiePolicyOptions`:</span></span>

::: moniker range=">= aspnetcore-2.1"

   [!code-csharp[](identity/sample/src/ASPNETv2.1-IdentityDemo/Startup.cs?name=snippet_configureservices)]

<span data-ttu-id="61534-134">위의 코드는 기본 옵션 값을 사용 하 여 Identity를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-134">The preceding code configures Identity with default option values.</span></span> <span data-ttu-id="61534-135">서비스를 통해 앱에 제공 됩니다 [종속성 주입](xref:fundamentals/dependency-injection)합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-135">Services are made available to the app through [dependency injection](xref:fundamentals/dependency-injection).</span></span>

   <span data-ttu-id="61534-136">호출 하 여 id를 활성화 [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_)합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-136">Identity is enabled by calling [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_).</span></span> <span data-ttu-id="61534-137">`UseAuthentication`은 요청 파이프라인에 인증 [미들웨어](xref:fundamentals/middleware/index)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-137">`UseAuthentication` adds authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>

   [!code-csharp[](identity/sample/src/ASPNETv2.1-IdentityDemo/Startup.cs?name=snippet_configure&highlight=18)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-42)]

   <span data-ttu-id="61534-138">서비스를 통해 응용 프로그램에 제공 됩니다 [종속성 주입](xref:fundamentals/dependency-injection)합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-138">Services are made available to the application through [dependency injection](xref:fundamentals/dependency-injection).</span></span>

   <span data-ttu-id="61534-139">`Configure` 메서드에서 `UseAuthentication` 메서드를 호출하면 응용 프로그램에서 Identity가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="61534-139">Identity is enabled for the application by calling `UseAuthentication` in the `Configure` method.</span></span> <span data-ttu-id="61534-140">`UseAuthentication`은 요청 파이프라인에 인증 [미들웨어](xref:fundamentals/middleware/index)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-140">`UseAuthentication` adds authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>

   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configure&highlight=17)]

::: moniker-end

::: moniker range="= aspnetcore-1.1"

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,13-33)]

   <span data-ttu-id="61534-141">이 서비스들은 응용 프로그램에서 [종속성 주입](xref:fundamentals/dependency-injection)을 통해서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61534-141">These services are made available to the application through [dependency injection](xref:fundamentals/dependency-injection).</span></span>

   <span data-ttu-id="61534-142">`Configure` 메서드에서 `UseIdentity` 메서드를 호출하면 응용 프로그램에서 Identity가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="61534-142">Identity is enabled for the application by calling `UseIdentity` in the `Configure` method.</span></span> <span data-ttu-id="61534-143">`UseIdentity`는 요청 파이프라인에 쿠키 기반의 인증 [미들웨어](xref:fundamentals/middleware/index)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-143">`UseIdentity` adds cookie-based authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configure&highlight=21)]

::: moniker-end

<span data-ttu-id="61534-144">자세한 내용은 참조는 [IdentityOptions 클래스](/dotnet/api/microsoft.aspnetcore.identity.identityoptions) 하 고 [응용 프로그램 시작](xref:fundamentals/startup).</span><span class="sxs-lookup"><span data-stu-id="61534-144">For more information, see the [IdentityOptions Class](/dotnet/api/microsoft.aspnetcore.identity.identityoptions) and [Application Startup](xref:fundamentals/startup).</span></span>

## <a name="scaffold-register-login-and-logout"></a><span data-ttu-id="61534-145">스 캐 폴드 등록, 로그인 및 로그 아웃</span><span class="sxs-lookup"><span data-stu-id="61534-145">Scaffold Register, Login, and LogOut</span></span>

<span data-ttu-id="61534-146">수행 합니다 [identity 권한 부여를 사용 하 여 Razor 프로젝트에 스 캐 폴드](xref:security/authentication/scaffold-identity#scaffold-identity-into-a-razor-project-with-authorization) 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="61534-146">Follow the [Scaffold identity into a Razor project with authorization](xref:security/authentication/scaffold-identity#scaffold-identity-into-a-razor-project-with-authorization) instructions.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="61534-147">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="61534-147">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="61534-148">등록, 로그인 및 로그 아웃 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-148">Add the Register, Login, and LogOut files.</span></span>


# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="61534-149">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="61534-149">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="61534-150">이름으로 프로젝트를 만든 경우 **WebApp1**, 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-150">If you created the project with name **WebApp1**, run the following commands.</span></span> <span data-ttu-id="61534-151">그렇지 않은 경우에 대 한 올바른 네임 스페이스를 사용 합니다 `ApplicationDbContext`:</span><span class="sxs-lookup"><span data-stu-id="61534-151">Otherwise, use the correct namespace for the `ApplicationDbContext`:</span></span>


```cli
dotnet aspnet-codegenerator identity -dc WebApp1.Data.ApplicationDbContext --files "Account.Register;Account.Login;Account.Logout"

```

<span data-ttu-id="61534-152">PowerShell 명령 구분 기호로 세미콜론을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-152">PowerShell uses semicolon as a command separator.</span></span> <span data-ttu-id="61534-153">PowerShell을 사용 하는 경우 파일 목록에 세미콜론을 이스케이프 하거나 이전 예제와 같이 큰따옴표로 파일 목록을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-153">When using PowerShell, escape the semicolons in the file list or put the file list in double quotes, as the preceding example shows.</span></span>

---

### <a name="examine-register"></a><span data-ttu-id="61534-154">등록 확인</span><span class="sxs-lookup"><span data-stu-id="61534-154">Examine Register</span></span>

::: moniker range=">= aspnetcore-2.1"

   <span data-ttu-id="61534-155">클릭할 때 합니다 **등록** 링크를 `RegisterModel.OnPostAsync` 동작이 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-155">When a user clicks the **Register** link, the `RegisterModel.OnPostAsync` action is invoked.</span></span> <span data-ttu-id="61534-156">사용자가 만든 [CreateAsync](/dotnet/api/microsoft.aspnetcore.identity.usermanager-1.createasync#Microsoft_AspNetCore_Identity_UserManager_1_CreateAsync__0_System_String_) 에 `_userManager` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="61534-156">The user is created by [CreateAsync](/dotnet/api/microsoft.aspnetcore.identity.usermanager-1.createasync#Microsoft_AspNetCore_Identity_UserManager_1_CreateAsync__0_System_String_) on the `_userManager` object.</span></span> <span data-ttu-id="61534-157">`_userManager` 가 제공한 종속성 주입):</span><span class="sxs-lookup"><span data-stu-id="61534-157">`_userManager` is provided by dependency injection):</span></span>

   [!code-csharp[](identity/sample/src/ASPNETv2.1-IdentityDemo/Register.cshtml.cs?name=snippet&highlight=7,22)]

::: moniker-end
::: moniker range="= aspnetcore-2.0"

   <span data-ttu-id="61534-158">클릭할 때 합니다 **등록** 링크를 `Register` 에서 동작이 호출 될 `AccountController`.</span><span class="sxs-lookup"><span data-stu-id="61534-158">When a user clicks the **Register** link, the `Register` action is invoked on `AccountController`.</span></span> <span data-ttu-id="61534-159">`Register` 액션은 `_userManager` 개체의 (종속성 주입으로 `AccountController`에 제공된) `CreateAsync`를 호출해서 사용자를 생성합니다:</span><span class="sxs-lookup"><span data-stu-id="61534-159">The `Register` action creates the user by calling `CreateAsync` on the `_userManager` object (provided to `AccountController` by dependency injection):</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_register&highlight=11)]

::: moniker-end

   <span data-ttu-id="61534-160">사용자가 정상적으로 생성되면 `_signInManager.SignInAsync` 가 호출되어 사용자가 즉시 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="61534-160">If the user was created successfully, the user is logged in by the call to `_signInManager.SignInAsync`.</span></span>

   <span data-ttu-id="61534-161">**참고:** 사용자 등록 즉시 로그인을 방지하는 방법은 [계정 확인](xref:security/authentication/accconfirm#prevent-login-at-registration) 을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="61534-161">**Note:** See [account confirmation](xref:security/authentication/accconfirm#prevent-login-at-registration) for steps to prevent immediate login at registration.</span></span>

### <a name="log-in"></a><span data-ttu-id="61534-162">로그인</span><span class="sxs-lookup"><span data-stu-id="61534-162">Log in</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="61534-163">로그인 양식이 표시 되는 경우:</span><span class="sxs-lookup"><span data-stu-id="61534-163">The Login form is displayed when:</span></span>

* <span data-ttu-id="61534-164">합니다 **로그인** 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-164">The **Log in** link  is selected.</span></span>
* <span data-ttu-id="61534-165">사용자는 인증 되지 않은 페이지를 액세스 하는 경우 **또는** 로그인 페이지로 리디렉션되어 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-165">When a user accesses a page where they are not authenticated **or** authorized, they are redirected to the Login page.</span></span> 

<span data-ttu-id="61534-166">로그인 페이지의 양식을 제출 되 면는 `OnPostAsync` 작업 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-166">When the form on the Login page is submitted, the `OnPostAsync` action is called.</span></span> <span data-ttu-id="61534-167">`PasswordSignInAsync` 라고 하는 `_signInManager` 개체 (종속성 주입으로 제공 됨).</span><span class="sxs-lookup"><span data-stu-id="61534-167">`PasswordSignInAsync` is called on the `_signInManager` object (provided by dependency injection).</span></span>

   [!code-csharp[](identity/sample/src/ASPNETv2.1-IdentityDemo/Login.cshtml.cs?name=snippet&highlight=10-11)]

   <span data-ttu-id="61534-168">기본 `Controller` 클래스는 컨트롤러의 메서드에서 접근할 수 있는 `User` 속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-168">The base `Controller` class exposes a `User` property that you can access from controller methods.</span></span> <span data-ttu-id="61534-169">예를 들어, 열거할 수 있습니다 `User.Claims` 을 권한 부여 결정을 내립니다.</span><span class="sxs-lookup"><span data-stu-id="61534-169">For instance, you can enumerate `User.Claims` and make authorization decisions.</span></span> <span data-ttu-id="61534-170">자세한 내용은 [권한 부여](xref:security/authorization/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-170">For more information, see [Authorization](xref:security/authorization/index).</span></span>

::: moniker-end
::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="61534-171">사용자가 선택할 때 로그인 양식이 표시 되는 **로그인** 연결 또는 인증을 요구 하는 페이지에 액세스할 때 자동으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="61534-171">The Login form is displayed when users select the **Log in** link or are redirected when accessing a page that requires authentication.</span></span> <span data-ttu-id="61534-172">사용자가 Login 페이지의 양식을 제출하면 `AccountController`의 `Login` 액션이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="61534-172">When the user submits the form on the Login page, the `AccountController` `Login` action is called.</span></span>

<span data-ttu-id="61534-173">`Login` 액션은 `_signInManager` 개체의 (종속성 주입으로 `AccountController` 에 제공된) `PasswordSignInAsync`를 호출합니다. </span><span class="sxs-lookup"><span data-stu-id="61534-173">The `Login` action calls `PasswordSignInAsync` on the `_signInManager` object (provided to `AccountController` by dependency injection).</span></span>

[!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_login&highlight=13-14)]

<span data-ttu-id="61534-174">기본 (`Controller` 나 `PageModel`) 클래스는 `User` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="61534-174">The base (`Controller` or `PageModel`) class exposes a `User` property.</span></span> <span data-ttu-id="61534-175">예를 들어 `User.Claims` 권한 부여 결정을 열거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61534-175">For example, `User.Claims` can be enumerated to make authorization decisions.</span></span>

::: moniker-end

### <a name="log-out"></a><span data-ttu-id="61534-176">로그 아웃</span><span class="sxs-lookup"><span data-stu-id="61534-176">Log out</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="61534-177">합니다 **로그 아웃** 링크를 호출 하는 `LogoutModel.OnPost` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-177">The **Log out** link invokes the `LogoutModel.OnPost` action.</span></span> 

[!code-csharp[](identity/sample/src/ASPNETv2.1-IdentityDemo/Logout.cshtml.cs)]

<span data-ttu-id="61534-178">[SignOutAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.signoutasync#Microsoft_AspNetCore_Identity_SignInManager_1_SignOutAsync) 쿠키에 저장 하는 사용자의 클레임을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="61534-178">[SignOutAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.signoutasync#Microsoft_AspNetCore_Identity_SignInManager_1_SignOutAsync) clears the user's claims stored in a cookie.</span></span> <span data-ttu-id="61534-179">호출 후 리디렉션 하지 `SignOutAsync` 또는 사용자에 게 **하지** 로그 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-179">Don't redirect after calling `SignOutAsync` or the user will **not** be signed out.</span></span>

<span data-ttu-id="61534-180">게시물에 지정 된 *Pages/Shared/_LoginPartial.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="61534-180">Post is specified in the *Pages/Shared/_LoginPartial.cshtml*:</span></span>

[!code-csharp[](identity/sample/src/ASPNETv2.1-IdentityDemo/_LoginPartial.cshtml?highlight=10)]

::: moniker-end
::: moniker range="= aspnetcore-2.0"
   <span data-ttu-id="61534-181">**LogOut** 링크를 클릭하면 `LogOut` 액션이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="61534-181">Clicking the **Log out** link calls the `LogOut` action.</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_logout&highlight=7)]

   <span data-ttu-id="61534-182">이전 호출의 `_signInManager.SignOutAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="61534-182">The preceding code calls the `_signInManager.SignOutAsync` method.</span></span> <span data-ttu-id="61534-183">`SignOutAsync`메서드는 쿠키에 저장된 사용자의 클레임을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-183">The `SignOutAsync` method clears the user's claims stored in a cookie.</span></span>
::: moniker-end

## <a name="test-identity"></a><span data-ttu-id="61534-184">테스트 Id</span><span class="sxs-lookup"><span data-stu-id="61534-184">Test Identity</span></span>

<span data-ttu-id="61534-185">기본 웹 프로젝트 템플릿 홈 페이지에 대 한 익명 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-185">The default web project templates allow anonymous access to the home pages.</span></span> <span data-ttu-id="61534-186">Id를 테스트 하려면 추가 [ `[Authorize]` ](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute) 정보 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61534-186">To test Identity, add [`[Authorize]`](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute) to the About page.</span></span>

[!code-csharp[](identity/sample/src/ASPNETv2.1-IdentityDemo/About.cshtml.cs)]

<span data-ttu-id="61534-187">에 로그인 하는 경우 로그 아웃 합니다. 앱을 실행 하 고 선택 합니다 **에 대 한** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-187">If you are signed in, sign out. Run the app and select the **About** link.</span></span> <span data-ttu-id="61534-188">로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="61534-188">You are redirected to the login page.</span></span>

::: moniker range=">= aspnetcore-2.1"

### <a name="explore-identity"></a><span data-ttu-id="61534-189">Identity를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-189">Explore Identity</span></span>

<span data-ttu-id="61534-190">Identity를 자세히 탐색:</span><span class="sxs-lookup"><span data-stu-id="61534-190">To explore Identity in more detail:</span></span>

* [<span data-ttu-id="61534-191">전체 id UI 원본 만들기</span><span class="sxs-lookup"><span data-stu-id="61534-191">Create full identity UI source</span></span>](xref:security/authentication/scaffold-identity#create-full-identity-ui-source)
* <span data-ttu-id="61534-192">각 페이지 및 디버거를 단계별로의 소스를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-192">Examine the source of each page and step through the debugger.</span></span>

::: moniker-end

## <a name="identity-components"></a><span data-ttu-id="61534-193">Id 구성 요소</span><span class="sxs-lookup"><span data-stu-id="61534-193">Identity Components</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="61534-194">에 포함 된 모든 Identity 종속 된 NuGet 패키지를 [Microsoft.AspNetCore.App 메타 패키지](xref:fundamentals/metapackage-app)합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-194">All the Identity dependent NuGet packages are included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>
::: moniker-end

<span data-ttu-id="61534-195">Id에 대 한 기본 패키지가 [Microsoft.AspNetCore.Identity](https://www.nuget.org/packages/Microsoft.AspNetCore.Identity/)합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-195">The primary package for Identity is [Microsoft.AspNetCore.Identity](https://www.nuget.org/packages/Microsoft.AspNetCore.Identity/).</span></span> <span data-ttu-id="61534-196">ASP.NET Core Identity에 대한 주요 인터페이스 모음을 포함하고 있는 이 패키지는 `Microsoft.AspNetCore.Identity.EntityFrameworkCore`에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61534-196">This package contains the core set of interfaces for ASP.NET Core Identity, and is included by `Microsoft.AspNetCore.Identity.EntityFrameworkCore`.</span></span>

## <a name="migrating-to-aspnet-core-identity"></a><span data-ttu-id="61534-197">ASP.NET Identity로 마이그레이션하기</span><span class="sxs-lookup"><span data-stu-id="61534-197">Migrating to ASP.NET Core Identity</span></span>

<span data-ttu-id="61534-198">자세한 내용 및 기존 Id 저장소에 마이그레이션하는 방법에 대 한 지침을 참조 하세요 [인증 및 Id 마이그레이션](xref:migration/identity)합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-198">For more information and guidance on migrating your existing Identity store, see [Migrate Authentication and Identity](xref:migration/identity).</span></span>

## <a name="setting-password-strength"></a><span data-ttu-id="61534-199">암호 강도 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-199">Setting password strength</span></span>

<span data-ttu-id="61534-200">참조 [구성](#pw) 최소 암호 요구 사항을 설정 하는 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="61534-200">See [Configuration](#pw) for a sample that sets the minimum password requirements.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61534-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="61534-201">Next Steps</span></span>

* [<span data-ttu-id="61534-202">ID 구성</span><span class="sxs-lookup"><span data-stu-id="61534-202">Configure Identity</span></span>](xref:security/authentication/identity-configuration)
* <xref:security/authorization/secure-data>
* <xref:security/authentication/add-user-data>
* <xref:security/authentication/identity-enable-qrcodes>
* <span data-ttu-id="61534-203">[Id 기본 키 데이터 형식 구성](xref:security/authentication/identity-primary-key-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="61534-203">[Configure Identity primary keys data type](xref:security/authentication/identity-primary-key-configuration).</span></span>
* <xref:migration/identity>
* <xref:security/authentication/accconfirm>
* <xref:security/authentication/2fa>
* <xref:host-and-deploy/web-farm>
